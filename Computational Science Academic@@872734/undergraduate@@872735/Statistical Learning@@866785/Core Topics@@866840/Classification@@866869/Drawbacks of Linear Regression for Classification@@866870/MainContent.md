## Introduction
Linear regression is a foundational tool in statistics, celebrated for its simplicity and effectiveness in modeling continuous outcomes. However, a common but misguided practice is to repurpose this tool for [binary classification](@entry_id:142257) tasks. This direct application, known as the Linear Probability Model, appears straightforward but conceals fundamental theoretical and practical problems that can lead to incorrect conclusions and poor predictive performance. This article addresses this knowledge gap by systematically deconstructing why linear regression is a flawed choice for classification. In the chapters that follow, you will first delve into the core **Principles and Mechanisms** of its failure, from producing impossible probability predictions to its mismatched loss function. Next, we will explore the tangible consequences of these issues across various **Applications and Interdisciplinary Connections**, including finance, medicine, and machine learning. Finally, you will solidify your understanding through **Hands-On Practices**, engaging with coding exercises that vividly demonstrate the model's critical shortcomings.

## Principles and Mechanisms

While linear regression is a cornerstone of [statistical modeling](@entry_id:272466) for continuous outcomes, its direct application to [binary classification](@entry_id:142257) tasks—a practice often termed the **Linear Probability Model (LPM)**—is fraught with fundamental theoretical and practical drawbacks. This chapter systematically dissects these shortcomings, moving from the most apparent failures in prediction to more subtle, yet critical, issues in optimization, [statistical efficiency](@entry_id:164796), and [model interpretation](@entry_id:637866). By understanding these limitations, we motivate the need for models specifically designed for classification, such as [logistic regression](@entry_id:136386).

### The Problem of Prediction Range: Non-Probabilistic Outputs

The most immediate and conspicuous flaw of using Ordinary Least Squares (OLS) for a [binary classification](@entry_id:142257) problem, where the response variable $y_i$ is encoded as $0$ or $1$, is that the model's predictions are not constrained to the valid probability interval of $[0, 1]$. OLS seeks to find the coefficient vector $\beta$ that minimizes the [sum of squared residuals](@entry_id:174395) (SSR):

$$
\text{SSR}(\beta) = \sum_{i=1}^{n} (y_i - \mathbf{x}_i^\top \beta)^2
$$

The optimization is performed over the unconstrained parameter space $\beta \in \mathbb{R}^d$. Nothing in this [objective function](@entry_id:267263) inherently forces the fitted values, $\hat{y} = \mathbf{x}^\top \hat{\beta}$, to lie within the $[0,1]$ range. As a result, the model can, and often does, produce "probability" estimates that are less than zero or greater than one.

Consider a simple hypothetical dataset with a single feature $z$ and a [binary outcome](@entry_id:191030) $y$: points at $(z_1,y_1) = (0,0)$, $(z_2,y_2) = (1,0)$, and $(z_3,y_3) = (2,1)$. Fitting a linear model $\hat{p}(z) = \beta_0 + \beta_1 z$ via OLS yields coefficients $\hat{\beta}_0 = -1/6$ and $\hat{\beta}_1 = 1/2$. The predicted value at $z=0$ is therefore $\hat{p}(0) = -1/6$, a nonsensical probability [@problem_id:3117134]. While one might consider post-hoc fixes, such as clipping the predictions to $[0,1]$ or formulating a [constrained least squares](@entry_id:634563) problem, these are merely patches. A constrained problem, for instance, becomes a computationally more expensive Quadratic Programming (QP) problem and does not remedy the other underlying issues discussed below.

The consequences of such invalid predictions are not merely aesthetic. In many real-world applications, from finance to medicine, probability estimates are fed into downstream decision-making frameworks. For instance, a decision to intervene might be based on an [expected utility](@entry_id:147484) calculation, where an action is taken if its [expected utility](@entry_id:147484), say $p \cdot B - C$, is positive, where $p$ is the probability of a positive outcome, $B$ is the benefit, and $C$ is the cost. This is equivalent to acting when $p > C/B$. If the model produces an estimate like $\hat{p}(x) = 1.3$, this would trigger an intervention even if the true probability is, for example, $0.8$, and the cost-benefit threshold is $0.9$. Conversely, a prediction of $\hat{p}(x) = -0.2$ would fail to trigger an intervention even if the true probability is $0.15$ and the threshold is $0.1$. In both scenarios, the OLS model's out-of-range predictions lead to suboptimal, and potentially harmful, decisions [@problem_id:3117108].

### The Mechanism of Extreme Predictions: The Role of Leverage

To understand *how* OLS generates these out-of-range predictions, we must look at the mechanics of the fitting process. The vector of OLS fitted values, $\hat{\mathbf{y}}$, is a linear transformation of the observed response vector, $\mathbf{y}$, via the **[hat matrix](@entry_id:174084)**, $H$:

$$
\hat{\mathbf{y}} = H \mathbf{y} \quad \text{where} \quad H = X(X^\top X)^{-1}X^\top
$$

Each individual fitted value is a [linear combination](@entry_id:155091) of *all* observed responses: $\hat{y}_i = \sum_{j=1}^n h_{ij} y_j$. The diagonal elements of the [hat matrix](@entry_id:174084), $h_{ii}$, are known as the **leverages** of each observation. A leverage $h_{ii}$ quantifies the influence of the observation $y_i$ on its own fitted value, $\hat{y}_i$. For a model with an intercept, the rows of $H$ sum to one ($\sum_j h_{ij} = 1$), meaning $\hat{y}_i$ is an [affine combination](@entry_id:276726) of the $y_j$ values.

In a [binary classification](@entry_id:142257) setting where $y_j \in \{0, 1\}$, if all weights $h_{ij}$ were non-negative, $\hat{y}_i$ would be a convex combination and thus guaranteed to be in $[0, 1]$. However, the off-diagonal elements $h_{ij}$ (for $i \neq j$) can be negative. This is particularly likely to occur for observations with **high leverage**. Points that are far from the center of the feature space (i.e., "[outliers](@entry_id:172866)" in $X$) exert high leverage.

A high-leverage point can effectively cause the model to extrapolate far beyond the data cloud. For example, consider a dataset where a point $(x_e, y_e)$ has an $x_e$ value far from the other points. This point will have a high leverage $h_{ee}$. The weights $h_{ej}$ that it applies to other points $y_j$ can become negative, especially for points on the opposite side of the feature mean. If the corresponding $y_j$ values are predominantly $1$s, the sum $\sum_{j \neq e} h_{ej} y_j$ can become a large negative number. If $y_e=0$, the resulting prediction $\hat{y}_e$ can easily be driven below zero. Symmetrically, a high-leverage point with $y_e=1$ can have its prediction $\hat{y}_e$ driven above one [@problem_id:3117177]. This reveals that the unbounded nature of OLS predictions is not just a theoretical possibility but a direct mechanical consequence of its projection geometry, especially in the presence of [influential data points](@entry_id:164407).

### The Mismatch of the Loss Function

The core of OLS is the minimization of squared error. While this loss is statistically optimal for a Gaussian error distribution, it is fundamentally ill-suited for [binary classification](@entry_id:142257) for several reasons.

#### Sensitivity to Margin and Outliers

A more advanced perspective on classifiers involves analyzing their associated [loss functions](@entry_id:634569) in terms of the **margin**, defined as $m = y f(\mathbf{x})$ for labels $y \in \{-1, 1\}$ and a [score function](@entry_id:164520) $f(\mathbf{x}) = \mathbf{w}^\top \mathbf{x}$. A large positive margin signifies a confident and correct classification.

The squared loss, when using the $\{-1, 1\}$ label encoding, can be expressed as a function of the margin:

$$
L_{\text{sq}}(y, f(\mathbf{x})) = (y - f(\mathbf{x}))^2 = (1 - m)^2
$$

This [loss function](@entry_id:136784) is a parabola with its minimum at $m=1$. This has a perverse consequence: the model penalizes not only misclassifications ($m  1$) but also *correct classifications that are too confident* ($m > 1$). A point that is correctly classified and far from the decision boundary will have a large margin and thus contribute a large loss. The optimization process will actively try to reduce this point's margin, pulling it closer to the boundary.

This is in stark contrast to well-behaved classification losses like the [logistic loss](@entry_id:637862), $L_{\text{log}}(m) = \ln(1 + \exp(-m))$, or the [hinge loss](@entry_id:168629), $L_{\text{hinge}}(m) = \max(0, 1-m)$, used by Support Vector Machines. Both of these losses are monotonically decreasing functions of the margin; they assign zero or negligible penalty to correctly classified points with large margins. This allows them to focus on the points that are truly ambiguous or misclassified—the essence of a large-margin classifier. The squared loss's peculiar sensitivity makes OLS fragile, as a few "easy" but distant points can unduly influence the decision boundary, potentially worsening its performance on the more difficult, overlapping points near the boundary [@problem_id:3117091] [@problem_id:3117170].

#### Inadequate Penalty for Confident Misclassifications

The squared error loss is also inadequate for probabilistic assessment. When a model makes a highly confident but incorrect prediction, a good probabilistic loss function should assign a very high penalty. Consider a true label $y=1$. If a model predicts a probability $p=0.01$, it is very wrong and very confident. The **Binary Cross-Entropy (BCE)** or log loss, given by $-[y \ln(p) + (1-y)\ln(1-p)]$, captures this intuition: the loss for this example would be $-\ln(0.01) \approx 4.6$. As $p \to 0$, the loss approaches infinity.

The Mean Squared Error (MSE), however, is much more forgiving. The squared error for this example is $(1 - 0.01)^2 = 0.99^2 \approx 0.98$. This penalty is bounded and does not reflect the severity of the probabilistic miscalibration. It is therefore possible to construct scenarios where a model has a lower MSE than another model but a catastrophically higher BCE, because the MSE fails to severely penalize confident errors [@problem_id:3117164].

This difference in penalties is also reflected in the gradients used for optimization. The gradient of the [logistic loss](@entry_id:637862) with respect to the pre-sigmoid score $f$ is simply $\sigma(f) - y$. The gradient of the squared loss on the probability, $\frac{1}{2}(\sigma(f) - y)^2$, is $(\sigma(f) - y) \sigma(f)(1-\sigma(f))$. The term $\sigma(f)(1-\sigma(f))$ acts as an attenuation factor. This factor is maximized at $1/4$ (when $\sigma(f)=0.5$) and approaches zero when the prediction is very confident (near 0 or 1). This means that for a confident but incorrect prediction, where the gradient *should* be largest to provide a strong corrective signal, the squared loss gradient is severely diminished. This hinders the model's ability to learn from its worst mistakes [@problem_id:3117151].

### The Flawed Statistical Assumption: Heteroskedasticity

One of the classical assumptions for the optimality of OLS (as the Best Linear Unbiased Estimator, or BLUE) is **homoscedasticity**: the variance of the error term is constant across all levels of the predictors. In the context of a binary response, this assumption is inherently violated.

If the true data-generating process is $Y_i \sim \text{Bernoulli}(p(\mathbf{x}_i))$, then the [conditional variance](@entry_id:183803) of the response is:

$$
\text{Var}(Y_i | \mathbf{x}_i) = p(\mathbf{x}_i)(1 - p(\mathbf{x}_i))
$$

This variance is clearly not constant; it is a function of the predictors $\mathbf{x}_i$ via the probability $p(\mathbf{x}_i)$. This phenomenon is known as **inherent [heteroskedasticity](@entry_id:136378)**. Because the OLS estimator does not account for this non-constant variance, it is no longer the most efficient linear estimator. Methods that do account for it, such as Weighted Least Squares (WLS) or, more generally, Generalized Linear Models (GLMs) like [logistic regression](@entry_id:136386), can produce estimates with lower [asymptotic variance](@entry_id:269933). The inefficiency of OLS relative to a correctly specified model can be quantified by comparing their asymptotic variances, demonstrating that OLS yields less precise coefficient estimates due to its failure to model the correct variance structure of the binary response [@problem_id:3117093].

### Misinterpretation and Miscalibration

Finally, even if one were to ignore the aforementioned issues, using linear regression for classification leads to severe problems in [model interpretation](@entry_id:637866) and application.

#### Misleading Coefficient Interpretation

In [logistic regression](@entry_id:136386), the coefficient $\beta_1$ for a predictor $x_1$ has a clear and powerful interpretation: a one-unit increase in $x_1$ is associated with a multiplicative change of $e^{\beta_1}$ in the odds of the outcome, holding other predictors constant. This [odds ratio](@entry_id:173151) is constant across all levels of $x_1$.

Practitioners may be tempted to apply a similar interpretation to the slope coefficient $b_1$ from an OLS fit. This is fundamentally incorrect. The OLS model implies a relationship between the probability and the predictors, not the [log-odds](@entry_id:141427). The implied [odds ratio](@entry_id:173151) from an OLS model, comparing $x$ and $x+\Delta$, is:

$$
\mathrm{OR}_{\mathrm{OLS}}(x, \Delta) = \frac{(a + b(x+\Delta)) / (1 - a - b(x+\Delta))}{(a + bx) / (1 - a - bx)}
$$

This expression clearly depends on the baseline value of $x$. Therefore, unlike in logistic regression, there is no constant [odds ratio](@entry_id:173151). Attempting to interpret the OLS slope as a log-odds coefficient is a conceptual error that leads to quantitatively incorrect and inconsistent conclusions about the effect of a predictor on the outcome [@problem_id:3117163].

#### Poor Calibration and Risk-Sensitive Decisions

A key virtue of a good classification model is **calibration**. A model is well-calibrated if, among the events to which it assigns a probability of, say, $0.7$, the actual frequency of those events occurring is indeed $70\%$. By construction, logistic regression is designed to produce well-calibrated probabilities. OLS has no such mechanism.

It is possible to construct datasets where an OLS model and a [logistic regression model](@entry_id:637047) have the exact same 0/1 classification accuracy (using a standard $0.5$ threshold). However, the OLS model's predicted probabilities will be poorly calibrated; for instance, the average of its predictions for a group of points may not match the empirical frequency of positive outcomes in that group.

This lack of calibration becomes critically important in risk-sensitive applications. In medical diagnosis or [credit scoring](@entry_id:136668), the decision threshold is rarely $0.5$. It is determined by the relative costs of false positives versus false negatives. A well-calibrated model allows one to set an optimal, risk-minimizing threshold based on these costs. A poorly calibrated model, like OLS, provides misleading probability estimates, causing the chosen threshold to be suboptimal and leading to higher overall costs. Even with identical accuracy, the OLS model is less useful and potentially more dangerous in practice because its outputs do not faithfully represent probabilities [@problem_id:3117104]. This failure undermines its utility in any application that requires more than just a binary prediction.