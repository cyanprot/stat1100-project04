# ADR-007: LSTM Decision
**Date:** 2026-03-14
**Status:** Accepted

## Context
LSTM (Long Short-Term Memory) networks are the state-of-the-art approach for CMAPSS RUL prediction in research literature, achieving RMSE values of 12-14 on FD001 compared to 16-20 for classical ML. As a time-series prediction problem, CMAPSS is a natural fit for recurrent architectures. The question is whether implementing an LSTM is appropriate for this project.

Four factors inform this decision:

1. **Course coverage:** Week 12 covers "Basic Deep Learning Concept" as a conceptual overview. There is no hands-on deep learning notebook, no neural network coding exercise, and the lecture explicitly frames deep learning as an awareness topic, not an implementation skill.

2. **Infrastructure:** The development server has an NVIDIA GPU accessible from the host, but nvidia-container-toolkit is not installed, so GPU acceleration is unavailable inside the Docker container where our Jupyter environment runs. CPU-only LSTM training on CMAPSS FD001 would take minutes (feasible) but introduces a dependency (TensorFlow/PyTorch) that complicates environment reproducibility.

3. **Performance context:** Classical ML models (Linear Regression, Random Forest, KNN with rolling features) achieve RMSE 16-20 on FD001, which is competitive. LSTM's advantage is primarily on FD002-FD004 where multiple operating conditions create complex temporal patterns that benefit from learned sequence representations. On FD001 (single condition), the marginal gain is modest.

4. **Assessment criteria:** The project rubric (inferred from course structure) prioritizes justification quality, methodological rigor, and course alignment over raw model performance. A well-justified decision NOT to use LSTM demonstrates more understanding than a poorly explained LSTM implementation.

## Decision
LSTM is discussed in the report as a "future work / known better approach" but is NOT implemented.

The report section will:
- Acknowledge LSTM as the literature standard for CMAPSS RUL prediction
- Explain why it was not implemented (course scope, infrastructure constraints)
- Compare our classical ML results against published LSTM benchmarks to contextualize performance
- Frame this as a deliberate scope decision, not an oversight

## Alternatives Considered
- **Implement minimal LSTM with tf.keras on CPU:** Feasible on FD001 (~3-5 minutes training time). However, (a) requires installing TensorFlow in the Docker environment, (b) the implementation would be copied from tutorials rather than derived from course content, (c) explaining LSTM architecture in a 15-minute presentation consumes time better spent on methodology and results, and (d) grading criteria likely do not reward going beyond course scope without strong justification.
- **Implement on host Python with GPU:** Bypasses the Docker container entirely. Breaks environment reproducibility for the project partner and for any Colab-based demonstration. Creates a "works on my machine" situation.
- **Use a pre-trained LSTM model:** Defeats the purpose of the project (building and understanding the pipeline end-to-end). Would be flagged as intellectually dishonest even in an AI-allowed course.
- **Use a simple dense neural network (MLP) instead of LSTM:** Avoids the sequence modeling complexity but still requires TensorFlow/PyTorch. An MLP on flattened features is essentially a non-linear regression -- Random Forest already serves this role without the deep learning dependency.

## Course Reference
Week 12: Basic Deep Learning Concept. The lecture introduces neural network fundamentals (perceptrons, layers, activation functions, backpropagation) as conceptual background. LSTM is a specific recurrent architecture that goes well beyond this introductory coverage.

## Consequences
- The report explicitly addresses LSTM as a known stronger approach, demonstrating literature awareness.
- Our RMSE results (likely 16-20) can be presented alongside published LSTM benchmarks (12-14) with honest analysis of the gap.
- No TensorFlow/PyTorch dependency in the project environment, keeping the setup simple (scikit-learn + pandas + matplotlib only).
- The decision reinforces the project narrative: "we chose methods we can fully explain and justify from course content, and we know what we would do differently with more advanced tools."
- If the instructor asks "why not deep learning?" during the presentation, we have a prepared, multi-faceted answer.
