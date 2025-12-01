## Introduction
In modern scientific inquiry, particularly in fields like systems biomedicine, computational models have become indispensable tools for understanding complex systems. These models, however, are often defined by numerous parameters whose values are uncertain. Understanding how this input uncertainty propagates to the model's predictions is a critical challenge. While simple local sensitivity analyses offer a glimpse into a model's behavior, they are fundamentally limited and often misleading when applied to the nonlinear, [high-dimensional systems](@entry_id:750282) that are now commonplace. This creates a significant knowledge gap: how can we robustly and comprehensively quantify the influence of each input on a model's behavior across the entire space of its uncertainty?

This article addresses that gap by providing a thorough exploration of Global Sensitivity Analysis (GSA), a suite of powerful techniques designed to analyze the entire input-output relationship of a model. Over the following chapters, you will embark on a journey from foundational theory to practical application. The "Principles and Mechanisms" chapter will lay the groundwork, dissecting the mathematical underpinnings of variance-based methods like Sobol' indices, exploring complementary techniques, and introducing advanced solutions like Shapley effects for handling dependent inputs. Next, the "Applications and Interdisciplinary Connections" chapter will demonstrate how these tools are used to solve real-world problems, from guiding experimental design in pharmacology to engineering robust [biological circuits](@entry_id:272430). Finally, a series of "Hands-On Practices" will allow you to solidify your understanding by applying these concepts to concrete computational problems, bridging the gap between theory and practical implementation.

## Principles and Mechanisms

This chapter delves into the fundamental principles and diverse mechanisms of Global Sensitivity Analysis (GSA). Moving beyond the introductory concepts, we will systematically dissect the theoretical underpinnings of various GSA methodologies, explore their assumptions, and establish a framework for selecting the appropriate method for a given scientific problem. Our focus will be on understanding not just *what* each method calculates, but *why* it is designed that way and what its results truly signify.

### The Fundamental Dichotomy: Local versus Global Analysis

Before exploring the landscape of GSA, it is essential to distinguish it from its more classical counterpart, **Local Sensitivity Analysis (LSA)**. In many modeling applications, particularly in systems biomedicine, we are initially concerned with how a model's output responds to small changes in its inputs around a specific, nominal [operating point](@entry_id:173374). This is the domain of LSA.

LSA quantifies sensitivity by using the partial derivatives of the output function $Y = f(\mathbf{X})$ with respect to each input $X_i$, evaluated at a single nominal point $\mathbf{x}^\star$. The local sensitivity of the $i$-th input is thus given by $\frac{\partial Y}{\partial X_i}\Big|_{\mathbf{x}=\mathbf{x}^\star}$. This approach is computationally efficient and provides precise information about the model's behavior in an infinitesimal neighborhood of $\mathbf{x}^\star$. However, its utility is fundamentally limited. The results are entirely local and may not be representative of the model's behavior elsewhere in the input space, especially for [nonlinear systems](@entry_id:168347). Furthermore, LSA is coordinate- and scale-dependent; a simple change of units for an input (e.g., from molar to millimolar) will alter the numerical value of its sensitivity index, complicating comparisons.

**Global Sensitivity Analysis (GSA)**, in contrast, adopts a fundamentally different perspective. It does not focus on a single point but instead considers the entire range of variation for each input, as defined by their [joint probability distribution](@entry_id:264835) $p_{\mathbf{X}}$. The objective of GSA is to apportion the uncertainty in the model output $Y$ to the uncertainty in the different inputs $X_i$ and their interactions [@problem_id:4348248]. It achieves this by integrating information over the global input space, weighted by the specified probability measure. This global perspective makes GSA methodologies far more robust for analyzing complex, nonlinear models where the influence of an input can vary dramatically across the input space. As we will see, many GSA methods possess desirable invariance properties that LSA lacks.

### The Cornerstone of GSA: Variance-Based Methods for Independent Inputs

Among the most widely used and rigorously developed GSA techniques are the variance-based methods, often associated with the work of Ilya M. Sobol'. These methods provide a way to decompose the total variance of the model output, $\mathrm{Var}(Y)$, into contributions from individual inputs and their interactions.

#### Foundational Assumptions

The validity and unique interpretability of the classical variance-based framework rest on two critical assumptions [@problem_id:4081398].

1.  **Square-Integrability of the Output:** The model output $Y=f(\mathbf{X})$ must be a square-integrable random variable, meaning its second moment is finite: $\mathbb{E}[Y^2] \lt \infty$. This is often written as $Y \in L^2(\Omega, \mathcal{F}, \mathbb{P})$. This condition is necessary to ensure that the variance of the output, $\mathrm{Var}(Y) = \mathbb{E}[Y^2] - (\mathbb{E}[Y])^2$, is a well-defined, finite quantity.

2.  **Mutual Independence of Inputs:** The input random variables $X_1, \dots, X_d$ must be mutually independent. This implies that their joint probability law is the product of their marginal laws: $\mathbb{P}_\mathbf{X} = \prod_{i=1}^d \mathbb{P}_i$. As we will demonstrate, this assumption is essential for the orthogonality of the functional decomposition that underpins the method, allowing the total variance to be partitioned into a unique sum of contributions.

#### The Law of Total Variance and Functional ANOVA Decomposition

The conceptual basis for [variance decomposition](@entry_id:272134) is the **law of total variance**. For any input $X_i$, this law states:

$$
\mathrm{Var}(Y) = \mathrm{Var}(\mathbb{E}[Y \mid X_i]) + \mathbb{E}[\mathrm{Var}(Y \mid X_i)]
$$

Let us carefully interpret the two terms on the right-hand side [@problem_id:4348284].
- The first term, $\mathrm{Var}(\mathbb{E}[Y \mid X_i])$, measures the variance of the [conditional expectation](@entry_id:159140) of $Y$ given $X_i$. The inner term, $\mathbb{E}[Y \mid X_i]$, represents the expected value of the output if we were to fix the input $X_i$ at a specific value. Since this conditional expectation is a function of the random variable $X_i$, it has a variance. This variance quantifies the expected reduction in output variance we would achieve by learning the true value of $X_i$. It is therefore identified as the **main effect** of $X_i$ on $Y$.

- The second term, $\mathbb{E}[\mathrm{Var}(Y \mid X_i)]$, is the expected value of the remaining variance. The inner term, $\mathrm{Var}(Y \mid X_i)$, is the variance of $Y$ that persists even after $X_i$ is fixed. This remaining variance is due to the variation in all other inputs, $X_j$ (where $j \neq i$). The outer expectation averages this residual variance over all possible values of $X_i$. This term thus captures the contributions from all other inputs as well as any **interactions** between $X_i$ and the other inputs.

Under the assumption of mutual input independence, any square-[integrable function](@entry_id:146566) $f(\mathbf{X})$ can be uniquely decomposed into a sum of orthogonal terms, a structure known as the **functional ANOVA (Analysis of Variance)** or **High-Dimensional Model Representation (HDMR)**:

$$
f(\mathbf{X}) = f_0 + \sum_{i=1}^{d} f_i(X_i) + \sum_{1 \le i \lt j \le d} f_{ij}(X_i, X_j) + \dots + f_{1, \dots, d}(X_1, \dots, X_d)
$$

The orthogonality of these terms (with respect to the product input measure) implies that the total variance of the output can be additively decomposed into the sum of the variances of each term:

$$
\mathrm{Var}(Y) = \sum_{i=1}^{d} V_i + \sum_{1 \le i \lt j \le d} V_{ij} + \dots + V_{1, \dots, d}
$$

where $V_i = \mathrm{Var}(f_i(X_i))$, $V_{ij} = \mathrm{Var}(f_{ij}(X_i, X_j))$, and so on. These partial variances can be expressed in terms of conditional expectations, linking back to the law of total variance. For instance, $V_i = \mathrm{Var}(\mathbb{E}[Y \mid X_i])$.

#### The Sobol' Indices

The Sobol' indices are simply these partial variances normalized by the total variance, providing a set of dimensionless sensitivity measures between 0 and 1.

The **first-order Sobol' index**, $S_i$, quantifies the main effect of an input $X_i$. It is the fraction of the total output variance that can be attributed to the variation in $X_i$ alone [@problem_id:4348251]:

$$
S_i = \frac{V_i}{\mathrm{Var}(Y)} = \frac{\mathrm{Var}(\mathbb{E}[Y \mid X_i])}{\mathrm{Var}(Y)}
$$

The sum of all first-order indices, $\sum_i S_i$, is less than or equal to 1. The deficit, $1 - \sum_i S_i$, represents the portion of the output variance that arises from interactions among the inputs.

To capture the total influence of an input, including its main effect and all its interactions (of all orders), we use the **total-effect Sobol' index**, $T_i$. It is most conveniently defined by considering the set of all inputs *except* $X_i$, denoted $X_{\sim i}$. The [variance explained](@entry_id:634306) by all inputs in $X_{\sim i}$ is $\mathrm{Var}(\mathbb{E}[Y \mid X_{\sim i}])$. The total effect of $X_i$ is everything else [@problem_id:4348251]:

$$
T_i = 1 - \frac{\mathrm{Var}(\mathbb{E}[Y \mid X_{\sim i}])}{\mathrm{Var}(Y)} = \frac{\mathbb{E}[\mathrm{Var}(Y \mid X_{\sim i})]}{\mathrm{Var}(Y)}
$$

The total-effect index $T_i$ measures the expected residual variance in $Y$ that would remain if we could fix all inputs *except* for $X_i$. A key property is that $T_i \ge S_i$. The difference, $T_i - S_i$, provides a measure of how strongly $X_i$ is involved in interactions with other inputs. If $T_i = S_i$, the input $X_i$ has a purely additive effect and does not interact with any other inputs.

### Alternative and Complementary GSA Methodologies

While variance-based methods are powerful, they are not the only approach to GSA. Other methods exist with different goals, assumptions, and computational costs.

#### Screening with the Morris Method

In models with a very large number of parameters (high $d$), computing Sobol' indices can be computationally prohibitive. In such cases, a preliminary **screening** is often performed to identify the most influential inputs, which can then be subjected to a more detailed analysis. The **Morris method** is a highly popular technique for this purpose [@problem_id:4348264].

The method explores the input space by constructing a set of trajectories, where each step in a trajectory involves changing only one input at a time (One-At-a-Time, or OAT). For each input $X_i$, this process generates a distribution of **elementary effects**. An elementary effect, $EE_i$, is essentially a local [finite-difference](@entry_id:749360) approximation of the gradient, computed at various points in the input space:

$$
EE_i(\mathbf{x}) = \frac{f(\mathbf{x} + \Delta e_i) - f(\mathbf{x})}{\Delta}
$$

where $\Delta$ is a step size defined on a discrete grid of input values. From the resulting distribution of elementary effects for each input, two key measures are calculated:

1.  **The mean of absolute elementary effects ($\mu_i^*$):** This measure is used to rank inputs by their overall influence. A high $\mu_i^*$ indicates that, on average, perturbing $X_i$ causes a large change in the output. The absolute value is crucial to prevent the cancellation of effects that have opposite signs in different regions of the input space.

2.  **The standard deviation of elementary effects ($\sigma_i$):** This measure quantifies the variability of the effect of $X_i$. A high $\sigma_i$ indicates that the influence of $X_i$ changes significantly depending on the values of the other inputs. This is a strong indicator of **interactions** with other factors or a highly **nonlinear** relationship between $X_i$ and the output. Conversely, an input with a high $\mu_i^*$ but a low $\sigma_i$ is influential and acts in a nearly linear and additive manner.

#### Derivative-Based Global Sensitivity Measures (DGSMs)

Another class of methods, known as DGSMs, also aggregates local sensitivity information to form a global picture. Instead of using [finite differences](@entry_id:167874) like the Morris method, they use the partial derivatives themselves. To create a global measure that avoids the cancellation of positive and negative gradients, a common approach is to average the *squared* partial derivative over the entire input space, weighted by the input probability distribution $p_X(\mathbf{x})$ [@problem_id:4348283]:

$$
G_i = \mathbb{E}\left[\left(\frac{\partial f(\mathbf{X})}{\partial X_i}\right)^2\right] = \int_{\mathcal{D}}\left(\frac{\partial f(\mathbf{x})}{\partial X_i}\right)^2 p_X(\mathbf{x})\,d\mathbf{x}
$$

This measure effectively quantifies the average magnitude (squared) of the local sensitivity to input $X_i$. It is sensitive to the input distribution, giving more weight to gradients in more probable regions of the input space. This measure is straightforward to interpret and is particularly useful when gradients can be computed efficiently, for example from an adjoint model or a differentiable surrogate.

#### Moment-Independent Methods: The Borgonovo $\delta$ Measure

Variance-based and derivative-based methods are powerful but inherently tied to specific moments or features of the output distribution (variance, mean gradient). In some applications, an input might have a significant impact on the shape, skewness, or modality of the output distribution without strongly affecting its variance. To capture such effects, **moment-independent** sensitivity measures are needed.

The **Borgonovo $\delta$ measure** provides such a framework [@problem_id:4348224]. It defines the sensitivity of an input $X_i$ as the expected difference between the entire probability distribution of the output $Y$ and the distribution of $Y$ conditioned on knowing $X_i$. The difference between distributions is measured by the [total variation distance](@entry_id:143997). The $\delta_i$ index is formally defined as:

$$
\delta_i = \frac{1}{2} \mathbb{E}_{X_i}\left[\int_{-\infty}^{\infty} |f_Y(y) - f_{Y|X_i}(y)|\,dy\right]
$$

where $f_Y(y)$ is the unconditional probability density function (PDF) of the output, and $f_{Y|X_i}(y)$ is the conditional PDF. The $\delta_i$ index possesses several powerful properties:
-   It is zero if and only if $Y$ and $X_i$ are statistically independent.
-   It is invariant under any monotonic, [one-to-one transformation](@entry_id:148028) of the output $Y$. This means the sensitivity ranking of inputs does not depend on the scale used to measure the output (e.g., linear vs. logarithmic), a highly desirable feature.
-   It provides a comprehensive measure of influence that accounts for any and all changes to the output distribution. For instance, in a clinical setting with a binary outcome ($Y \in \{0, 1\}$), $\delta_i$ reduces to the expected absolute shift in outcome probability given knowledge of $X_i$.

### The Challenge of Dependent Inputs

A critical limitation of the classical GSA methods discussed so far (Sobol', Morris, eFAST) is their reliance on the assumption of mutual input independence. In many real-world systems, such as the interacting pathways of systems biomedicine, input parameters are often correlated due to shared underlying physiological or [biochemical processes](@entry_id:746812) [@problem_id:4348239].

#### Modeling Dependence with Copulas

When inputs are dependent, their joint probability distribution can no longer be factored into a product of marginals. A powerful tool for describing and simulating such distributions is the **copula**. **Sklar's theorem** states that any multivariate joint distribution can be decomposed into its marginal distributions and a copula function $C$, which describes the dependence structure between the variables. For a random vector $\mathbf{X}$ with continuous marginal CDFs $F_1, \dots, F_d$, the joint CDF is given by:

$$
F_{\mathbf{X}}(x_1, \dots, x_d) = C(F_1(x_1), \dots, F_d(x_d))
$$

This separation is immensely useful. It allows us to model the marginal uncertainty of each input and their dependence structure independently. For simulation, one can draw a sample $\mathbf{u}$ from the copula $C$ and then transform each component via the inverse marginal CDF: $x_i = F_i^{-1}(u_i)$ [@problem_id:4348239].

#### Why Classical GSA Fails

When inputs are dependent, the functional ANOVA decomposition is no longer orthogonal with respect to the true joint probability measure. This means the covariance between different functional terms is generally non-zero, and the simple additive decomposition of variance ($\mathrm{Var}(Y) = \sum V_u$) breaks down. The very notion of attributing a unique "share" of the variance to a specific input or interaction becomes ambiguous and order-dependent. Naively applying standard estimators for Sobol' indices to data with dependent inputs is a serious error; the resulting numerical values lose their interpretation as fractions of variance and can even fall outside the $[0, 1]$ range [@problem_id:4348239].

#### A Principled Solution: Shapley Effects

To perform a principled [variance decomposition](@entry_id:272134) for models with dependent inputs, a different framework is needed. Drawing from cooperative game theory, **Shapley effects** provide a unique and fair way to attribute the total output variance to the inputs, regardless of their dependence structure [@problem_id:4348278], [@problem_id:4348239].

The approach analogizes inputs to "players" in a cooperative game, where the "value" of a coalition of players (a subset of inputs $S$) is the amount of output variance they collectively explain. This value function, $v(S)$, is defined as:

$$
v(S) = \mathrm{Var}(\mathbb{E}[Y \mid X_S])
$$

The Shapley effect of an input $X_i$, denoted $\mathcal{S}_i$, is its average marginal contribution to the value, averaged over all possible orders in which the inputs could be considered:

$$
\mathcal{S}_i = \sum_{S \subseteq \{1,\dots,d\}\setminus\{i\}} \frac{|S|!\,(d-|S|-1)!}{d!} \left( v(S \cup \{i\}) - v(S) \right)
$$

The Shapley effects are the unique attribution scheme that satisfies a set of fairness axioms, the most important of which is **efficiency**. For variance-based GSA, this means the sum of the Shapley effects for all inputs is exactly equal to the total output variance [@problem_id:4348278]:

$$
\sum_{i=1}^{d} \mathcal{S}_i = \mathrm{Var}(Y)
$$

This property restores the ability to perform a full and unique decomposition of variance, even in the presence of complex, arbitrary dependence structures among the inputs. For example, in a symmetric model where two inputs are exchangeable, the symmetry axiom of Shapley effects guarantees they will be assigned equal sensitivity, regardless of their correlation [@problem_id:4348278].

### Synthesis: A Principled Workflow for Method Selection

The diversity of GSA methods underscores that there is no single "best" method for all problems. Selecting an appropriate GSA workflow requires a careful mapping of method assumptions to the specific features of the model and its uncertain inputs. Consider a realistic scenario from systems biomedicine: a nonlinear, nonmonotonic ODE model of a cytokine response, where some parameters are known to be strongly correlated, and the computational cost of each model run is significant [@problem_id:4348286]. A principled GSA workflow for such a problem would involve several stages:

1.  **Problem Characterization:** The first step is to thoroughly understand the model and its uncertainty. Is the model nonlinear or nonmonotonic? Are the inputs independent or dependent? What is the computational budget? In our example, the model is nonmonotonic, and the inputs are dependent.

2.  **Method Matching and Screening:** Based on this characterization, select appropriate methods. The presence of **dependent inputs** immediately rules out standard Sobol', Morris, and eFAST methods. Instead, methods robust to dependence, like extensions of the Morris method for correlated inputs or DGSMs, can be used for an initial screening. The **nonmonotonicity** rules out methods that assume a [monotonic relationship](@entry_id:166902) for interpretability, such as Partial Rank Correlation Coefficients (PRCC).

3.  **Surrogate Modeling:** Given a moderate computational budget, it is highly efficient to build a statistical [surrogate model](@entry_id:146376) (or metamodel) that accurately mimics the original expensive model. A flexible model like a **Gaussian Process (GP)** is an excellent choice, as it can capture complex nonlinear and nonmonotonic behavior. The surrogate must be trained on a set of input-output pairs generated while respecting the known dependence structure (e.g., using a copula-based sampling design). The accuracy of the surrogate must be rigorously validated on a held-out [test set](@entry_id:637546).

4.  **Definitive Sensitivity Analysis:** Once a validated surrogate is available, definitive GSA can be performed at negligible computational cost. For the dependent-input problem, **Shapley effects** should be computed from the surrogate to obtain a fair and complete attribution of the output variance. To gain a more complete picture, especially if the output distribution is skewed, this variance-based analysis can be complemented with a **moment-independent measure** like the Borgonovo $\delta$ index.

This systematic approach—characterize, screen, build surrogate, and analyze with appropriate methods—ensures that the conclusions of the [sensitivity analysis](@entry_id:147555) are robust, rigorous, and directly relevant to the scientific question at hand. It avoids the common pitfalls of misapplied methods and provides a comprehensive understanding of how input uncertainties drive model behavior.