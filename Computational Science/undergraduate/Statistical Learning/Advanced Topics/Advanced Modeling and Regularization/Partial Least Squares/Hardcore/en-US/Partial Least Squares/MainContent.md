## Introduction
In the age of big data, scientists and analysts frequently encounter datasets where the number of predictor variables far exceeds the number of observations, and these predictors are often highly intercorrelated. This scenario, common in fields from genomics to economics, poses a significant challenge for traditional statistical methods like Ordinary Least Squares (OLS) regression, which can fail entirely or produce unreliable models. Partial Least Squares (PLS) regression emerges as a powerful and flexible solution to this problem. It is a supervised [dimensionality reduction](@entry_id:142982) technique that skillfully navigates high-dimensional spaces by constructing a small set of [latent variables](@entry_id:143771) that are optimally related to the response variable.

This article provides a thorough exploration of Partial Least Squares, designed to build a strong foundational and practical understanding. We will embark on a journey through three distinct chapters. First, in **Principles and Mechanisms**, we will dissect the core algorithm, contrasting its supervised approach with other methods and detailing the iterative process of component extraction. Next, in **Applications and Interdisciplinary Connections**, we will see PLS in action, exploring its transformative impact in diverse fields such as [chemometrics](@entry_id:154959), ecology, and [systems biology](@entry_id:148549), and examining advanced extensions like PLS-DA and Kernel PLS. Finally, the **Hands-On Practices** section will offer opportunities to solidify this knowledge through practical, guided exercises. By the end, you will not only grasp the theory behind PLS but also appreciate its versatility as a key tool in the modern data scientist's toolkit.

## Principles and Mechanisms

Having established the contexts in which Partial Least Squares (PLS) regression is applied, we now turn to a rigorous examination of its underlying principles and the algorithmic mechanisms that enable its function. This chapter will deconstruct PLS, contrasting it with related methods, detailing its iterative procedure, and exploring the practical considerations essential for its successful application.

### Supervised Dimensionality Reduction: The Core Principle of PLS

The challenge of building predictive models from [high-dimensional data](@entry_id:138874), where the number of predictor variables is large and often highly correlated, necessitates a strategy of [dimensionality reduction](@entry_id:142982). The goal is to distill the complex information from the predictor matrix $X$ into a small number of informative [latent variables](@entry_id:143771), or components, which can then be used in a simpler [regression model](@entry_id:163386). The manner in which these components are constructed is the defining feature of the method.

A familiar approach is **Principal Component Regression (PCR)**. In PCR, one first performs Principal Component Analysis (PCA) on the predictor matrix $X$. PCA is an **unsupervised** method; it seeks to find directions, or principal components, that capture the maximum variance within the predictor data $X$ itself. The response variable $Y$ plays no role in this component-finding process. The first principal component is the linear combination of the predictors that has the highest variance; the second is the one with the next-highest variance, subject to being orthogonal to the first, and so on. Only after these components are determined is the response variable $Y$ introduced to build a regression model using a subset of the components as predictors. 

**Partial Least Squares (PLS)** regression operates on a fundamentally different, **supervised** principle. Rather than seeking directions of maximum variance in $X$, PLS seeks directions in the $X$-space that are maximally relevant for predicting $Y$. It achieves this by constructing [latent variables](@entry_id:143771) that maximize the **covariance** between the predictor variables and the response variables. This subtle but critical distinction means that the construction of each PLS component is guided by the response variable from the very beginning.

To appreciate the significance of this difference, consider a hypothetical scenario. Suppose our predictor data $X$ consists of two variables, $x_1$ and $x_2$. Let $x_1$ possess a very large variance but be entirely uncorrelated with the response $y$. Conversely, let $x_2$ have a very small variance but contain all the predictive information, such that the true relationship is $y = \alpha x_2 + \varepsilon$.

*   A PCR model, in its quest to explain the variance in $X$, would identify the direction of $x_1$ as its first and most important principal component. A low-dimensional PCR model using only the first component would be dominated by this irrelevant information and would consequently have very poor predictive power for $y$.

*   A PLS model, by contrast, would seek the direction in the $X$-space that maximizes covariance with $y$. It would detect the strong relationship between $x_2$ and $y$, despite the low variance of $x_2$, and would orient its first latent variable along the direction of $x_2$. A one-component PLS model would therefore be highly predictive.

This example illustrates the central advantage of PLS: by directly incorporating the response variable into the dimensionality reduction step, it can identify and prioritize low-variance directions in the predictor space that are nonetheless highly predictive of the outcome. PCR, being blind to the response during this critical step, is liable to discard such directions.  

### The PLS Algorithm: Iterative Component Extraction

The mechanism by which PLS achieves its objective is an elegant iterative algorithm. While several variants exist, the most conceptually transparent is the NIPALS (Non-linear Iterative Partial Least Squares) algorithm, which we will explore for the common case of a single response variable (a model often denoted PLS1). For simplicity, we assume the predictor matrix $X$ and the response vector $y$ have been **mean-centered**.

#### The First Component: Maximizing Covariance

The first step is to find the direction in the $X$-space that is most relevant to $y$. This direction is defined by a **weight vector**, $w_1$. The projection of the data onto this direction forms the first **score vector**, $t_1 = Xw_1$. The PLS criterion dictates that $w_1$ must be chosen to maximize the squared sample covariance between the score $t_1$ and the response $y$. For centered data, this is equivalent to solving the optimization problem:
$$
\underset{\|w_1\|=1}{\text{maximize}} \quad (\text{Cov}(Xw_1, y))^2 \propto ((Xw_1)^T y)^2 = (w_1^T X^T y)^2
$$
By the properties of vector projections, this expression is maximized when the [unit vector](@entry_id:150575) $w_1$ is chosen to be collinear with the vector $X^T y$. This leads to a beautifully simple result for the direction of the first weight vector:
$$
w_1 \propto X^T y
$$
The vector $X^T y$ contains the sample covariance of each original predictor in $X$ with the response vector $y$. The PLS weight vector $w_1$ is therefore a weighted combination of the original predictor directions, where the weights are determined by their relevance to the response. After normalizing, we have $w_1 = \frac{X^T y}{\|X^T y\|_2}$.

For instance, given a simple centered dataset $X = \begin{pmatrix} -1  -1 \\ 0  1 \\ 1  0 \end{pmatrix}$ and $y = \begin{pmatrix} -2 \\ 3 \\ -1 \end{pmatrix}$, the vector governing the weights is $X^T y = \begin{pmatrix} 1 \\ 5 \end{pmatrix}$. This immediately tells us that in constructing the first latent variable, the algorithm will give five times more importance to the second predictor than the first, as its covariance with the response is five times greater. 

#### Weights, Loadings, and Their Distinct Roles

The PLS literature uses several terms—weights, scores, and loadings—that must be carefully distinguished.

*   **Weights ($w_k$)**: These are vectors in the predictor space ($p$-dimensional) that define the direction for constructing the scores. As we have seen, they are chosen to maximize covariance with the response. Their role is transformative: $t_k = X_{k-1} w_k$.

*   **Scores ($t_k$)**: These are vectors in the sample space ($n$-dimensional) representing the projected values of the samples onto the latent variable direction. They form the new predictor variables for the final, simplified [regression model](@entry_id:163386).

*   **Loadings ($p_k$ and $q_k$)**: These are vectors that describe how the original variables relate to the scores. They are best understood as [regression coefficients](@entry_id:634860).
    *   The **$X$-loading vector** ($p_k$) is found by regressing the columns of the predictor matrix $X_{k-1}$ onto the score vector $t_k$. It is calculated as $p_k = \frac{X_{k-1}^T t_k}{t_k^T t_k}$. The [outer product](@entry_id:201262) $t_k p_k^T$ represents the [rank-one matrix](@entry_id:199014) that best approximates $X_{k-1}$ in the least-squares sense, using the information from $t_k$.
    *   The **$Y$-loading** (a scalar $q_k$ in PLS1) is found by regressing the response vector $y_{k-1}$ onto the score vector $t_k$: $q_k = \frac{y_{k-1}^T t_k}{t_k^T t_k}$. It quantifies how much the score $t_k$ explains of the response.

Clarifying these roles is essential for a deep understanding of the PLS mechanism. The weights construct, and the loadings reconstruct and relate. 

#### Iterative Deflation

After extracting the first component ($w_1, t_1, p_1, q_1$), we cannot simply repeat the process on the original data, as this would trivially yield the same component. We must first remove, or **deflate**, the information that has just been modeled. The algorithm proceeds by computing residual matrices:
$$
X_1 = X_0 - t_1 p_1^T
$$
$$
y_1 = y_0 - t_1 q_1
$$
Here, $X_0$ and $y_0$ are the initial centered matrices. The next component is then found by applying the same logic to the residual matrices $X_1$ and $y_1$, yielding $w_2 \propto X_1^T y_1$, and so on for $K$ components.

This deflation step is not arbitrary; it has a crucial geometric property. By subtracting the projection $t_1 p_1^T$, the resulting residual matrix $X_1$ is rendered orthogonal to the score vector $t_1$. That is, every column of $X_1$ is orthogonal to $t_1$, which implies $X_1^T t_1 = \mathbf{0}$.  This, in turn, ensures that the subsequent score vector, $t_2 = X_1 w_2$, will be orthogonal to $t_1$. A key result of the NIPALS algorithm is that the full set of score vectors, $T = [t_1, t_2, \dots, t_K]$, are mutually orthogonal.  This orthogonality is highly desirable as it means the scores are uncorrelated, simplifying the final regression step.

### Model Construction and Practical Application

#### From Scores to Predictions

Once $K$ [latent variables](@entry_id:143771) have been extracted, we have a score matrix $T \in \mathbb{R}^{n \times K}$ and a vector of $Y$-loadings $q \in \mathbb{R}^{K}$. The final PLS predictive model is a simple [multiple linear regression](@entry_id:141458) of the original response $y$ on the orthogonal scores $T$:
$$
\hat{y} = Tq
$$
Because the columns of $T$ are orthogonal, the coefficients in $q$ are stable and can be determined one by one during each iteration of the algorithm.

While the model is built in the low-dimensional space of the scores, it is often useful to express the prediction in terms of the original predictors, i.e., in the form $\hat{y} = X\beta_{\text{PLS}}$. This overall regression vector $\beta_{\text{PLS}}$ can be calculated from the full set of weights ($W$), $X$-loadings ($P$), and $Y$-loadings ($q$) as:
$$
\beta_{\text{PLS}} = W(P^T W)^{-1} q
$$
This demonstrates that although PLS is constructed through an iterative, component-wise process, it ultimately corresponds to a linear model in the original feature space. 

#### Handling High-Dimensional Data ($p > n$)

One of the most compelling reasons to use PLS is its natural ability to handle datasets where the number of predictors $p$ is much greater than the number of samples $n$. Such "fat" data matrices are common in fields like [chemometrics](@entry_id:154959), genomics, and text analysis.

Traditional Multiple Linear Regression, solved via Ordinary Least Squares (OLS), seeks to compute the coefficient vector as $\beta_{\text{OLS}} = (X^T X)^{-1} X^T y$. This computation requires the inversion of the $p \times p$ matrix $X^T X$. When $p > n$, the rank of the $n \times p$ matrix $X$ cannot exceed $n$. Consequently, the rank of $X^T X$ is also at most $n$, which is strictly less than its dimension $p$. A matrix whose rank is less than its dimension is singular and does not have an inverse. Thus, the OLS solution is not uniquely defined, and the method fails. This problem is exacerbated by multicollinearity (high correlation between predictors), which makes $X^T X$ ill-conditioned or singular even when $p \le n$.

PLS elegantly bypasses this problem. It never attempts to compute $(X^T X)^{-1}$. Instead, it projects the data onto a small number ($K$) of [latent variables](@entry_id:143771). The final regression step involves the $K \times K$ score matrix $T^T T$. Since the scores are constructed to be orthogonal, $T^T T$ is a [diagonal matrix](@entry_id:637782), which is trivial to invert. By working in this much smaller, well-behaved latent space, PLS provides a stable and effective solution for regression problems that are intractable for OLS. 

#### Selecting Model Complexity with Cross-Validation

A critical decision in any PLS analysis is selecting the number of [latent variables](@entry_id:143771), $K$, to include in the model. This is a classic [bias-variance trade-off](@entry_id:141977). A model with too few components ($K$ is too small) will be underfit, failing to capture the true predictive relationship (high bias). A model with too many components ($K$ is too large) will be overfit; it will begin to model random noise in the training data, leading to poor predictive performance on new, unseen data (high variance).

Simply choosing the value of $K$ that maximizes a [goodness-of-fit](@entry_id:176037) metric on the training data (like the [coefficient of determination](@entry_id:168150), $R^2$) is incorrect, as this will always lead to selecting the most complex model possible. The correct approach is to estimate the model's [generalization error](@entry_id:637724).

The standard technique for this is **cross-validation**. The calibration dataset is divided into several "folds". The PLS model is then repeatedly built using all but one fold (the training portion) and used to predict the responses for the held-out fold (the validation portion). This process is repeated for a range of possible values of $K$. For each $K$, the errors from the validation folds are aggregated into a single metric, such as the **Predicted Residual Error Sum of Squares (PRESS)**. The optimal number of components, $K^*$, is then chosen as the value that minimizes this cross-validated error, representing the best compromise between [model complexity](@entry_id:145563) and predictive power. 

#### The Importance of Feature Scaling

The PLS algorithm, in its standard form, is not [scale-invariant](@entry_id:178566). The core of the algorithm, the calculation of the weight vector direction via $X^T y$, is based on the covariance between predictors and the response. Covariance, unlike correlation, is dependent on the units and scale of the variables. A predictor variable with a numerically large variance can disproportionately influence the calculation of the first weight vector, even if its underlying correlation with the response is modest.

To prevent variables with arbitrary large scales from dominating the model, it is standard and highly recommended practice to **standardize** the predictors before applying the PLS algorithm. This typically involves mean-centering each predictor and then scaling it to have unit variance. By putting all predictors on a common scale, standardization ensures that the weight vectors are determined by the strength of the correlation structure between the predictors and the response, not by their arbitrary units. This generally leads to more stable, robust, and [interpretable models](@entry_id:637962). The choice of whether to scale the data will affect the computed weights, scores, and ultimately, the final predictions. 