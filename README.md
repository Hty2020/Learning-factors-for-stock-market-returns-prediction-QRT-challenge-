# Learning-factors-for-stock-market-returns-prediction-QRT-challenge-
- The detailed description can be found on <https://challengedata.ens.fr/challenges/72>, and the training data can also be obtained there after registration.

## Overview

**Challenge:** ENS Challenge Data 2022 (Qube Research & Technologies). Given three years of daily returns for 50 anonymous stocks, predict the next-day cross-sectional return vector. The submission is a pair $(A,\beta)$ where $A \in \mathbb{R}^{250 \times 10}$ is a Stiefel matrix ($A^\top A = I_{10}$) and $\beta \in \mathbb{R}^{10}$: the prediction for stock $i$ at date $t$ is $\hat{y}_{i,t} = [\mathbf{X}_\text{reshape}\,A\,\beta]_{(t,i)}$, with $\mathbf{X}_\text{reshape}$ containing the 250-day lag window for every (date, stock) pair. Performance is the mean cosine overlap between predicted and realised return vectors.

**Approaches explored:**

| Method | In-sample overlap |
|---|:---:|
| AR(10) — autoregressive baseline | 0.0240 |
| 5-day return + momentum (2-factor) | 0.0195 |
| Fourier bases (10 frequencies) | 0.0301 |
| PCA on $X_\text{reshape}^\top X_\text{reshape}$ | 0.0387 |
| Random search benchmark (QRT) | 0.0458 |
| **Alternating Stiefel optimisation** | **0.1302** |

**Key finding:** Alternating projected gradient descent on the Stiefel manifold — PCA-initialised, $\beta$-step via closed-form optimization, $A$-step via Euclidean gradient + SVD projection — achieves an in-sample overlap of **0.1302**, nearly 3× the random-search benchmark. The train/validation split in the *Additional Work* section quantifies the degree of in-sample overfitting.

**Submission:** The public benchmark score in the challenge test data set is 0.0354. My score is 0.0821.
