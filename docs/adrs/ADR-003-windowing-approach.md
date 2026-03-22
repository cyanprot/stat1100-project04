# ADR-003: Windowing Approach
**Date:** 2026-03-14
**Status:** Accepted

## Context
CMAPSS data is a multivariate time series: each engine has a sequence of rows (one per cycle), with 21 sensor readings and 3 operational settings per row. To capture temporal degradation patterns, we need to encode "how sensors have been changing" into each row, not just their instantaneous values. The standard approaches are: (1) explicit sliding windows that flatten multiple timesteps into a single feature vector, or (2) rolling statistics that summarize recent history into compact aggregates.

FD001 has only 100 training engines with ~17,000 total rows. Feature dimensionality must be carefully controlled.

## Decision
Use rolling statistics (mean, standard deviation, slope over a window of 5 cycles) computed per sensor, per engine. Each row gets 3 additional features per sensor: rolling_mean, rolling_std, and rolling_slope (linear regression coefficient over the window).

For 14 usable sensors (after dropping 7 constant sensors per ADR-006), this produces:
- 14 raw sensor values
- 14 rolling means
- 14 rolling stds
- 14 rolling slopes
- Total: ~56 features (plus 3 operational settings if retained)

The first 4 rows of each engine (where the window is incomplete) use expanding-window statistics rather than being dropped.

## Alternatives Considered
- **Explicit sliding window + flatten:** With sequence_length=30 (common in literature) and 14 sensors, each sample becomes a 30x14=420-dimensional vector. With ~17,000 training samples, this creates a high-dimensional space where overfitting is near-certain for classical ML models. Would require aggressive PCA or feature selection, adding pipeline complexity.
- **Raw features only (no temporal encoding):** Each row is treated independently. Loses all temporal context -- the model cannot distinguish "sensor X is at value Y and rising" from "sensor X is at value Y and falling." Significantly worse RMSE in literature.
- **LSTM with 3D input (samples, timesteps, features):** The natural approach for sequence data, but (a) deep learning is only covered as a Week 12 overview, (b) GPU Docker is unavailable (ADR-007), and (c) it's overkill for an intro course project.
- **Larger window (w=10 or w=20):** More temporal context but heavier smoothing. w=5 is a balance between noise reduction and preserving short-term degradation signals. Can be tuned via cross-validation if needed.

## Course Reference
Week 5: EDA and Visualization. Rolling aggregation functions (mean, std) are core EDA techniques covered in the EDA lecture and notebook. The slope feature extends this with a simple linear regression over the window, connecting to Week 7 (Regression) concepts.

## Consequences
- Feature count is manageable (~56) for classical ML models on 17,000 samples.
- Rolling statistics are interpretable: "sensor 7 average is increasing and variance is spiking" maps to intuitive degradation narratives for the presentation.
- The window size (w=5) becomes a hyperparameter that could be tuned, but we fix it to keep the pipeline simple and document why.
- First few rows per engine have less reliable statistics (expanding window), but this is a minor edge effect on ~400 rows out of 17,000.
- This approach is explicitly chosen over LSTM windowing to stay within the course's taught methods.
