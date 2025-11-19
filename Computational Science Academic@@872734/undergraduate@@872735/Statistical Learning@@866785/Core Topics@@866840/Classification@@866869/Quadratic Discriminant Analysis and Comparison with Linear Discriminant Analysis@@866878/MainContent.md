## Introduction
In the realm of [statistical learning](@entry_id:269475), [generative models](@entry_id:177561) offer a powerful approach to classification by modeling the underlying probability distribution of the data within each class. Among the most foundational of these are Linear Discriminant Analysis (LDA) and Quadratic Discriminant Analysis (QDA). While both operate on the principle of fitting Gaussian distributions to the data, they diverge on a single, crucial assumption regarding the covariance structure of the classes. This distinction gives rise to profoundly different model behaviors, geometric properties, and practical performance characteristics.

This article addresses the fundamental knowledge gap between knowing that LDA and QDA exist and understanding precisely how and why to choose between them. It demystifies their core mechanisms, illuminating the trade-offs inherent in their respective assumptions. By navigating through their theoretical underpinnings and practical applications, you will gain a robust framework for deploying these essential classification tools effectively.

The following chapters will guide you on this journey. The first chapter, **Principles and Mechanisms**, delves into the mathematical derivations of both models from Bayes' rule, exposing how their assumptions lead to linear versus quadratic decision boundaries and exploring the critical [bias-variance trade-off](@entry_id:141977). The second chapter, **Applications and Interdisciplinary Connections**, grounds these theories in real-world scenarios across fields like finance, medicine, and genomics, showing how the choice of model can make or break a classification task. Finally, **Hands-On Practices** provides a series of targeted exercises to solidify your understanding of the geometric and mathematical concepts discussed.

## Principles and Mechanisms

In the preceding chapter, we introduced the concept of generative models for classification, where we model the probability distribution of the data within each class. This chapter delves into the principles and mechanisms of two of the most fundamental generative classifiers: **Linear Discriminant Analysis (LDA)** and **Quadratic Discriminant Analysis (QDA)**. Both models assume that the class-conditional densities, $p(\mathbf{x}|Y=k)$, are multivariate Gaussian distributions. Their primary distinction, which has profound theoretical and practical consequences, lies in their assumptions about the covariance structure of these distributions.

### From Bayes' Rule to Discriminant Functions

The foundation for both LDA and QDA is Bayes' rule for classification. For a $K$-class problem with a feature vector $\mathbf{x} \in \mathbb{R}^p$, the [posterior probability](@entry_id:153467) of class $k$ is given by:

$$
P(Y=k|X=\mathbf{x}) = \frac{p(\mathbf{x}|Y=k) \pi_k}{\sum_{j=1}^K p(\mathbf{x}|Y=j) \pi_j}
$$

where $p(\mathbf{x}|Y=k)$ is the class-conditional density for class $k$ and $\pi_k$ is the [prior probability](@entry_id:275634) of class $k$. The Bayes classifier assigns an observation $\mathbf{x}$ to the class for which this [posterior probability](@entry_id:153467) is maximized.

Since the denominator is the same for all classes, we only need to maximize the numerator, $p(\mathbf{x}|Y=k) \pi_k$. Furthermore, because the logarithm is a strictly [monotonic function](@entry_id:140815), maximizing the posterior is equivalent to maximizing its logarithm. This leads us to define a **[discriminant function](@entry_id:637860)**, $g_k(\mathbf{x})$, for each class:

$$
g_k(\mathbf{x}) = \ln(p(\mathbf{x}|Y=k)) + \ln(\pi_k)
$$

The classification rule is then to assign $\mathbf{x}$ to the class $k$ that maximizes $g_k(\mathbf{x})$.

The core assumption of LDA and QDA is that each class-conditional density is a multivariate normal (Gaussian) distribution:

$$
p(\mathbf{x}|Y=k) = \frac{1}{(2\pi)^{p/2} |\mathbf{\Sigma}_k|^{1/2}} \exp\left(-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu}_k)^\top \mathbf{\Sigma}_k^{-1} (\mathbf{x}-\boldsymbol{\mu}_k)\right)
$$

Here, $\boldsymbol{\mu}_k$ is the [mean vector](@entry_id:266544) and $\mathbf{\Sigma}_k$ is the covariance matrix for class $k$. The term $(\mathbf{x}-\boldsymbol{\mu}_k)^\top \mathbf{\Sigma}_k^{-1} (\mathbf{x}-\boldsymbol{\mu}_k)$ is the squared **Mahalanobis distance** from $\mathbf{x}$ to the class mean $\boldsymbol{\mu}_k$. Unlike Euclidean distance, Mahalanobis distance accounts for the variance and correlation within the data, effectively measuring distance in terms of standard deviations.

By substituting the logarithm of this Gaussian density into our definition of $g_k(\mathbf{x})$, we can derive the specific forms of the QDA and LDA [discriminant](@entry_id:152620) functions.

### Quadratic Discriminant Analysis (QDA): The General Case

QDA makes no simplifying assumptions about the covariance matrices; each class $k$ is permitted to have its own unique covariance matrix $\mathbf{\Sigma}_k$. Taking the logarithm of the Gaussian density and adding the log prior, we obtain:

$$
g_k(\mathbf{x}) = -\frac{p}{2}\ln(2\pi) - \frac{1}{2}\ln|\mathbf{\Sigma}_k| - \frac{1}{2}(\mathbf{x}-\boldsymbol{\mu}_k)^\top \mathbf{\Sigma}_k^{-1} (\mathbf{x}-\boldsymbol{\mu}_k) + \ln \pi_k
$$

Since the term $-\frac{p}{2}\ln(2\pi)$ is a constant with respect to the class index $k$, it does not affect the classification decision and can be dropped. This leaves the final QDA [discriminant function](@entry_id:637860) [@problem_id:3164372]:

$$
g_k(\mathbf{x}) = -\frac{1}{2}\ln|\mathbf{\Sigma}_k| - \frac{1}{2}(\mathbf{x}-\boldsymbol{\mu}_k)^\top \mathbf{\Sigma}_k^{-1} (\mathbf{x}-\boldsymbol{\mu}_k) + \ln \pi_k
$$

Let's analyze the components of this function. The classification score for class $k$ depends on three elements:
1.  **The Prior Probability ($\ln \pi_k$)**: This biases the decision towards classes that are more common a priori.
2.  **The Mahalanobis Distance**: The term $-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu}_k)^\top \mathbf{\Sigma}_k^{-1} (\mathbf{x}-\boldsymbol{\mu}_k)$ measures the proximity of $\mathbf{x}$ to the center of class $k$, scaled by the class's own covariance structure. A smaller distance yields a higher score.
3.  **The Log-Determinant Penalty ($-\frac{1}{2}\ln|\mathbf{\Sigma}_k|$)**: The determinant $|\mathbf{\Sigma}_k|$ is a measure of the volume of the data cloud for class $k$. The term $-\frac{1}{2}\ln|\mathbf{\Sigma}_k|$ thus penalizes classes with larger volumes. Intuitively, if a point falls within the distribution of a class with a very wide spread, its membership is considered less "certain" compared to falling within a very compact, concentrated distribution. This term effectively adjusts the intercept of the [discriminant function](@entry_id:637860) for each class.

If we expand the quadratic term, the [discriminant function](@entry_id:637860) becomes:
$$
g_k(\mathbf{x}) = -\frac{1}{2}\mathbf{x}^\top \mathbf{\Sigma}_k^{-1} \mathbf{x} + \mathbf{x}^\top \mathbf{\Sigma}_k^{-1} \boldsymbol{\mu}_k - \frac{1}{2}\boldsymbol{\mu}_k^\top \mathbf{\Sigma}_k^{-1} \boldsymbol{\mu}_k - \frac{1}{2}\ln|\mathbf{\Sigma}_k| + \ln \pi_k
$$
The presence of the term $-\frac{1}{2}\mathbf{x}^\top \mathbf{\Sigma}_k^{-1} \mathbf{x}$, where the matrix $\mathbf{\Sigma}_k^{-1}$ is specific to class $k$, makes $g_k(\mathbf{x})$ a **quadratic** function of $\mathbf{x}$. This is the origin of the name "Quadratic Discriminant Analysis".

### Linear Discriminant Analysis (LDA): A Shared Covariance Assumption

LDA introduces a significant simplification: it assumes that all classes share a single, common covariance matrix, i.e., $\mathbf{\Sigma}_k = \mathbf{\Sigma}$ for all $k=1, \dots, K$. This assumption dramatically changes the [discriminant function](@entry_id:637860). Starting from the QDA form and setting all $\mathbf{\Sigma}_k$ to $\mathbf{\Sigma}$:

$$
g_k(\mathbf{x}) = -\frac{1}{2}\ln|\mathbf{\Sigma}| - \frac{1}{2}(\mathbf{x}-\boldsymbol{\mu}_k)^\top \mathbf{\Sigma}^{-1} (\mathbf{x}-\boldsymbol{\mu}_k) + \ln \pi_k
$$

Let's expand the quadratic term as before:
$$
g_k(\mathbf{x}) = -\frac{1}{2}\ln|\mathbf{\Sigma}| - \frac{1}{2}(\mathbf{x}^\top \mathbf{\Sigma}^{-1} \mathbf{x} - 2\mathbf{x}^\top \mathbf{\Sigma}^{-1} \boldsymbol{\mu}_k + \boldsymbol{\mu}_k^\top \mathbf{\Sigma}^{-1} \boldsymbol{\mu}_k) + \ln \pi_k
$$

Now, observe which terms depend on the class index $k$. The terms $-\frac{1}{2}\ln|\mathbf{\Sigma}|$ and $-\frac{1}{2}\mathbf{x}^\top \mathbf{\Sigma}^{-1} \mathbf{x}$ are now identical for all classes. Since we only care about which $g_k(\mathbf{x})$ is largest, any terms that do not depend on $k$ can be discarded without changing the classification result. Removing these constant terms leaves us with the simplified and conventional LDA [discriminant function](@entry_id:637860) [@problem_id:3164372]:

$$
g_k(\mathbf{x}) = \mathbf{x}^\top \mathbf{\Sigma}^{-1} \boldsymbol{\mu}_k - \frac{1}{2}\boldsymbol{\mu}_k^\top \mathbf{\Sigma}^{-1} \boldsymbol{\mu}_k + \ln \pi_k
$$

This function is a **linear** function of $\mathbf{x}$. All the quadratic terms have been eliminated, which gives the method its name, "Linear Discriminant Analysis".

### The Geometry of Decision Boundaries

The crucial difference between LDA and QDA manifests in the geometry of their decision boundaries. The decision boundary between any two classes, say class $i$ and class $j$, is the set of points $\mathbf{x}$ where their [discriminant](@entry_id:152620) scores are equal: $g_i(\mathbf{x}) = g_j(\mathbf{x})$.

#### LDA: Linear Boundaries

For LDA, the decision boundary is defined by the equation $g_i(\mathbf{x}) - g_j(\mathbf{x}) = 0$. Substituting the linear [discriminant function](@entry_id:637860) gives:
$$
(\mathbf{x}^\top \mathbf{\Sigma}^{-1} \boldsymbol{\mu}_i - \frac{1}{2}\boldsymbol{\mu}_i^\top \mathbf{\Sigma}^{-1} \boldsymbol{\mu}_i + \ln \pi_i) - (\mathbf{x}^\top \mathbf{\Sigma}^{-1} \boldsymbol{\mu}_j - \frac{1}{2}\boldsymbol{\mu}_j^\top \mathbf{\Sigma}^{-1} \boldsymbol{\mu}_j + \ln \pi_j) = 0
$$
$$
\mathbf{x}^\top \mathbf{\Sigma}^{-1}(\boldsymbol{\mu}_i - \boldsymbol{\mu}_j) - \frac{1}{2}(\boldsymbol{\mu}_i^\top \mathbf{\Sigma}^{-1} \boldsymbol{\mu}_i - \boldsymbol{\mu}_j^\top \mathbf{\Sigma}^{-1} \boldsymbol{\mu}_j) + \ln\left(\frac{\pi_i}{\pi_j}\right) = 0
$$
This is an equation of the form $\mathbf{b}^\top \mathbf{x} + c = 0$, which defines a **[hyperplane](@entry_id:636937)** (a line in $\mathbb{R}^2$, a plane in $\mathbb{R}^3$, etc.). The decision boundaries of LDA are therefore always linear, with zero curvature.

#### QDA: Quadratic Boundaries

For QDA, the equation $g_i(\mathbf{x}) - g_j(\mathbf{x}) = 0$ does not simplify as neatly. The quadratic terms in $\mathbf{x}$ do not cancel because $\mathbf{\Sigma}_i \neq \mathbf{\Sigma}_j$. This leads to an equation of the general [quadratic form](@entry_id:153497) [@problem_id:3164342]:

$$
\mathbf{x}^\top \mathbf{A} \mathbf{x} + \mathbf{b}^\top \mathbf{x} + c = 0
$$

where the crucial matrix $\mathbf{A}$ is given by $\mathbf{A} = \frac{1}{2}(\mathbf{\Sigma}_j^{-1} - \mathbf{\Sigma}_i^{-1})$. As long as $\mathbf{\Sigma}_i \neq \mathbf{\Sigma}_j$, the matrix $\mathbf{A}$ is non-zero, and the decision boundary is a **quadratic surface**. In two dimensions ($p=2$), these boundaries are [conic sections](@entry_id:175122): ellipses, parabolas, or hyperbolas. The specific type of conic is determined by the properties of the matrix $\mathbf{A}$, specifically its eigenvalues [@problem_id:3164378].
*   If the eigenvalues of $\mathbf{A}$ have the same sign ($\det(\mathbf{A}) > 0$), the boundary is an ellipse.
*   If they have opposite signs ($\det(\mathbf{A})  0$), the boundary is a hyperbola.
*   If one eigenvalue is zero ($\det(\mathbf{A}) = 0$), the boundary is a parabola.

This flexibility allows QDA to capture more complex relationships between classes. Consider a scenario where two classes have different covariance structures even if their means are close. For example, in a celestial survey trying to distinguish Pulsars from Quasars, one class might have features that are highly correlated (an elliptical data cloud) while the other has uncorrelated features (a circular data cloud). LDA, constrained to a linear boundary, might struggle to separate them effectively. QDA, by fitting a curved boundary, can better respect the distinct shapes of each class's distribution [@problem_id:1914063].

A particularly striking illustration of this difference occurs when two classes have the exact same mean, $\boldsymbol{\mu}_1 = \boldsymbol{\mu}_2$, but different covariances, for instance $\mathbf{\Sigma}_1 = \mathbf{I}$ and $\mathbf{\Sigma}_2 = 2\mathbf{I}$ [@problem_id:3164283]. LDA is completely blind in this situation. Its [discriminant function](@entry_id:637860) only depends on differences between class means, so if the means are identical, it assigns the same score to both classes everywhere. LDA fails to produce any separating boundary. QDA, however, can still distinguish the classes. Its decision is based on both the Mahalanobis distance and the volume penalty. For points close to the common mean, the smaller covariance of Class 1 makes it a better fit. For points far from the mean, the larger covariance of Class 2 makes it a better fit, as it allows for greater spread. The resulting QDA decision boundary is a circle (or hypersphere) centered at the common mean, successfully partitioning the space.

### The Bias-Variance Trade-off: Choosing the Right Model

QDA's flexibility comes at a cost. Since it fits a separate covariance matrix for each class, it has significantly more parameters to estimate from the data than LDA. For a problem with $p$ features and $K$ classes:
*   A single symmetric $p \times p$ covariance matrix has $\frac{p(p+1)}{2}$ unique parameters to estimate.
*   LDA estimates one such matrix for all classes.
*   QDA estimates $K$ such matrices, for a total of $K \times \frac{p(p+1)}{2}$ covariance parameters [@problem_id:1914084].

This leads to a classic **[bias-variance trade-off](@entry_id:141977)**:
*   **LDA** is a simple, low-flexibility model. It has **high bias** because its assumption of a common covariance is likely incorrect in many real-world settings. However, by estimating fewer parameters, its parameter estimates have **low variance**—they are more stable and less sensitive to the specific training data.
*   **QDA** is a complex, high-flexibility model. It has **low bias** as it can capture a wider range of true data-generating processes. But by estimating many more parameters, its estimates suffer from **high variance**, especially when the amount of training data is limited.

This trade-off is exacerbated by the **curse of dimensionality**. As the number of features $p$ grows, the number of parameters in the covariance matrices ($O(p^2)$) explodes. To get reliable estimates for these parameters, an enormous amount of data is required. In a typical high-dimension, low-sample-size setting (large $p$, small $n$), QDA often performs poorly. The high variance of its parameter estimates (the [estimation error](@entry_id:263890)) can completely dominate its advantage of low bias (the approximation error). In such cases, the simpler, more stable LDA model often yields better out-of-sample prediction accuracy, even if the true decision boundary is known to be non-linear [@problem_id:3181701].

A critical technical issue arises when the number of samples in a class, $n_k$, is less than the number of features, $p$. In this scenario, the [sample covariance matrix](@entry_id:163959) $\hat{\mathbf{\Sigma}}_k$ will be singular (rank-deficient), meaning its inverse is undefined. Standard QDA, which requires this inverse, cannot even be computed. LDA is more robust because it estimates its single pooled covariance matrix using all $n = \sum n_k$ samples, making it more likely that $n > p$ and the resulting matrix is invertible [@problem_id:3181701].

Given this trade-off, how does one make a principled choice between LDA and QDA?
1.  **Hypothesis Testing**: One can frame the decision as a formal statistical test. The null hypothesis, $H_0: \mathbf{\Sigma}_1 = \mathbf{\Sigma}_2 = \dots = \mathbf{\Sigma}_K$, corresponds to the LDA model being sufficient. The alternative, $H_1$, is that at least one covariance matrix is different, warranting QDA. A **Likelihood Ratio Test** can be used to compare the maximized likelihood of the data under both models. A significant result suggests that the added complexity of QDA is justified by a superior fit to the data [@problem_id:3164293]. Committing a Type I error (choosing QDA when LDA is sufficient) risks overfitting, while a Type II error (choosing LDA when QDA is needed) introduces bias.

2.  **Information Criteria**: Alternatively, one can use [model selection criteria](@entry_id:147455) like the **Akaike Information Criterion (AIC)** or the **Bayesian Information Criterion (BIC)**. These criteria balance [goodness of fit](@entry_id:141671) (measured by the maximized log-likelihood) with model complexity (the number of estimated parameters). The model with the lower AIC or BIC score is preferred. Because BIC's penalty for complexity, which includes a $\ln(n)$ term, is stronger than AIC's for any reasonable sample size $n$, it tends to favor simpler models more than AIC does. It is thus common for AIC to select QDA while BIC selects the more parsimonious LDA on the same dataset [@problem_id:3164315].

Finally, it is insightful to consider a limiting case. If we take our observed data and add a large amount of independent, isotropic Gaussian noise, $\mathbf{x}_{\text{obs}} = \mathbf{x} + \boldsymbol{\epsilon}$ where $\boldsymbol{\epsilon} \sim \mathcal{N}(\mathbf{0}, \tau^2 \mathbf{I})$, the new effective covariance for each class becomes $\mathbf{\Sigma}'_k = \mathbf{\Sigma}_k + \tau^2 \mathbf{I}$. As the noise level $\tau^2$ grows very large, it "washes out" the original differences between the covariance matrices $\mathbf{\Sigma}_k$. The matrices $\mathbf{\Sigma}'_k$ all become very similar to $\tau^2 \mathbf{I}$. In this high-noise limit, the QDA model's behavior converges to that of an LDA model, and its quadratic decision boundary flattens into a [hyperplane](@entry_id:636937). This demonstrates that LDA can be seen as a special, constrained case within the broader family of QDA classifiers [@problem_id:3164350].