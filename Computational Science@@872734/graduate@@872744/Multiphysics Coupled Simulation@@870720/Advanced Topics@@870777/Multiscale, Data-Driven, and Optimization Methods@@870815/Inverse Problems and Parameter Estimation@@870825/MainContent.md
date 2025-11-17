## Introduction
Inverse problems and [parameter estimation](@entry_id:139349) form a critical bridge between computational modeling and experimental reality, allowing us to infer the hidden properties and governing laws of a system from observed data. In the realm of multiphysics simulations, where complex interactions defy direct measurement, this inverse task is both indispensable and challenging. While a forward simulation predicts an observable outcome from a known set of parameters, the inverse problem seeks the parameters that best explain the measurements. This process is fundamentally difficult, often suffering from issues of [ill-posedness](@entry_id:635673), where solutions can be non-unique or catastrophically sensitive to [measurement noise](@entry_id:275238). This article provides a comprehensive guide to navigating these challenges. The first chapter, **'Principles and Mechanisms,'** dissects the mathematical foundations of [inverse problems](@entry_id:143129), exploring [ill-posedness](@entry_id:635673), sensitivity analysis, and the core deterministic and Bayesian solution frameworks. The second chapter, **'Applications and Interdisciplinary Connections,'** illustrates the power of these methods through a survey of real-world examples across science and engineering. Finally, the **'Hands-On Practices'** section offers concrete problems to solidify the reader's understanding of these critical concepts.

## Principles and Mechanisms

Having introduced the concept of [inverse problems](@entry_id:143129) in the context of multiphysics simulations, we now turn to a systematic examination of the underlying principles and mechanisms that govern their formulation and solution. This chapter will dissect the fundamental challenges inherent in [inverse problems](@entry_id:143129), introduce the mathematical tools required for their analysis, and outline the principal methodologies for their solution and the quantification of associated uncertainties.

### The Forward Problem and the Inverse Problem

At the heart of any [parameter estimation](@entry_id:139349) task lies the **forward problem**. This is typically represented by a **forward map**, a mathematical operator denoted by $F$, which translates a set of model parameters, $\theta$, into a set of observable outputs, $y$. We write this relationship as:

$y = F(\theta)$

In the context of [multiphysics](@entry_id:164478) simulations, the parameter $\theta$ can represent a diverse collection of quantities: a finite-dimensional vector of scalar constants (e.g., material properties like thermal conductivity or [elastic modulus](@entry_id:198862)), or an infinite-dimensional function representing a spatially varying field (e.g., a permeability field $\kappa(x)$). The output $y$ represents the quantities that can be measured experimentally, such as temperature readings at specific sensor locations, displacements, or concentrations. The forward map $F$ itself encapsulates the entire simulation workflow, which involves solving a system of governing Partial Differential Equations (PDEs) for a given $\theta$ and then applying an [observation operator](@entry_id:752875) to the solution fields.

The **inverse problem** reverses this logic. It begins with a set of measured data, denoted $y^\delta$ (where the superscript $\delta$ indicates the data are inevitably corrupted by noise), and seeks to infer the parameter vector $\theta$ that best explains these observations.

A critical prerequisite for a meaningful [inverse problem](@entry_id:634767) is a **well-posed [forward problem](@entry_id:749531)**. That is, for every admissible parameter vector $\theta$, the governing PDEs must have a unique solution that depends continuously on the input data of the PDE (such as sources or boundary conditions). If the forward map $F$ were not well-defined—for instance, if a given $\theta$ could produce multiple different solutions or no solution at all—the very question of finding the $\theta$ that corresponds to a measurement $y^\delta$ would be ill-conceived [@problem_id:3511246]. Throughout this chapter, we will assume the forward problem is well-posed.

### Fundamental Challenges: The Nature of Ill-Posedness

While the forward problem in physics and engineering is often well-posed, the corresponding [inverse problem](@entry_id:634767) is frequently not. The concept of a [well-posed problem](@entry_id:268832) was formalized by the mathematician Jacques Hadamard. A problem is said to be **Hadamard well-posed** if it satisfies three fundamental conditions [@problem_id:3511167]:

1.  **Existence**: A solution exists for every admissible set of data.
2.  **Uniqueness**: The solution is unique.
3.  **Stability**: The solution depends continuously on the data; small perturbations in the data should lead to only small changes in the solution.

Inverse problems often violate one or more of these conditions, in which case they are termed **ill-posed**.

#### Uniqueness and Structural Identifiability

The uniqueness condition is directly related to the concept of **[structural identifiability](@entry_id:182904)**. A parameter vector $\theta$ is said to be globally structurally identifiable if the forward map $F$ is **injective** on the set of admissible parameters $\Theta$. In simple terms, this means that two different parameter vectors, $\theta_1 \neq \theta_2$, will always produce different observable outputs, $F(\theta_1) \neq F(\theta_2)$. If this condition holds, then in a world of perfect, noise-free measurements, the equation $y = F(\theta)$ has at most one solution for $\theta$ [@problem_id:3511246].

In many physical systems, this ideal is not met due to symmetries. For instance, it might be possible to change two parameters in a compensatory way that leaves the observable output unchanged. This results in a non-injective forward map and a structurally non-identifiable problem. In such cases, one might still be able to identify certain combinations of parameters or [equivalence classes](@entry_id:156032) of parameters [@problem_id:3511246].

In practice, we often analyze **local [structural identifiability](@entry_id:182904)**, which asks whether a parameter vector $\theta_0$ can be uniquely determined within a small neighborhood. This is typically assessed by examining the Fréchet derivative (or Jacobian) of the forward map, a concept we will develop in Section 2.3. If the derivative is injective, the [inverse function theorem](@entry_id:138570) provides conditions under which the map is locally injective, implying local identifiability [@problem_id:3511246].

#### Stability and the Role of Compactness

The most pervasive form of [ill-posedness](@entry_id:635673) in [inverse problems](@entry_id:143129) for PDEs is the failure of the stability condition. The solution's sensitivity to data noise can be so extreme that any small [measurement error](@entry_id:270998) is amplified into an unacceptably large error in the estimated parameters. This instability often has a deep mathematical origin in the **compactness** of the forward map.

To understand this, consider an [inverse problem](@entry_id:634767) where the unknown parameter is an infinite-dimensional function, such as the spatially varying conductivity $k(x)$ in the elliptic PDE $-\nabla \cdot (k(x) \nabla u) = f$. The forward map $F$ takes the function $k(x)$ and maps it to an observation, for example, the solution field $u(x)$ itself, viewed as an element of an appropriate [function space](@entry_id:136890). Let's formalize this: the parameter $k(x)$ is in a space like $H^1(\Omega)$, and the observation $u(k)$ is in $L^2(\Omega)$. The forward map can be viewed as a composition of two steps [@problem_id:3511173]:

1.  The **solution map** $S: k \mapsto u(k)$, which maps the conductivity field to the temperature field solution of the PDE. For elliptic PDEs, one can typically show that this map takes [bounded sets](@entry_id:157754) of parameters into [bounded sets](@entry_id:157754) of solutions in the Sobolev space $H_0^1(\Omega)$. This is a consequence of the energy estimates derived from the PDE's [weak form](@entry_id:137295).

2.  The **observation map** $B$, which in this case embeds the solution from $H_0^1(\Omega)$ into the observation space $L^2(\Omega)$. For bounded domains, the famous **Rellich-Kondrachov theorem** states that this embedding is a **[compact operator](@entry_id:158224)**.

A compact operator is one that maps [bounded sets](@entry_id:157754) into pre-compact sets (sets whose closure is compact). Intuitively, a compact operator "squeezes" an infinite-dimensional set into something that is "almost" finite-dimensional. The composition of a [bounded operator](@entry_id:140184) ($S$) and a [compact operator](@entry_id:158224) ($B$) results in a compact forward map $F = B \circ S$.

The consequence of this compactness is severe. A fundamental theorem of [functional analysis](@entry_id:146220) states that a [compact linear operator](@entry_id:267666) between [infinite-dimensional spaces](@entry_id:141268) cannot have a bounded inverse. For nonlinear problems, the same principle holds for the linearized operator. This lack of a bounded inverse is precisely the mathematical formulation of instability. It implies that no matter how small we make the noise $\delta y$ in our data, the error in the reconstructed parameter $\delta k$ can be arbitrarily large. The operator effectively loses information in a way that cannot be stably recovered. This is the hallmark of an ill-posed [inverse problem](@entry_id:634767) [@problem_id:3511173].

#### Distinguishing Ill-Posedness from Ill-Conditioning

It is crucial to distinguish the intrinsic [ill-posedness](@entry_id:635673) of the continuous problem from the **[numerical ill-conditioning](@entry_id:169044)** of its discretized counterpart. When we solve an inverse problem on a computer, we work with a finite-dimensional algebraic system, often a linear system involving a Jacobian (or sensitivity) matrix $J_h$, where $h$ is a measure of the discretization mesh size.

-   **Ill-posedness** is a property of the infinite-dimensional, [continuous operator](@entry_id:143297) $F$. It reflects a fundamental lack of stability, often due to compactness.

-   **Ill-conditioning** is a property of a specific matrix $J_h$. An [ill-conditioned matrix](@entry_id:147408) has a large condition number $\kappa(J_h)$, meaning the solution to a linear system is highly sensitive to perturbations in the right-hand side.

A large condition number for a single, fixed [discretization](@entry_id:145012) does not, by itself, prove that the underlying problem is ill-posed. The problem might be well-posed but "stiff." The definitive diagnostic is to observe the behavior of the condition number under [mesh refinement](@entry_id:168565). Consider a sequence of consistent discretizations with mesh size $h \to 0$.

-   If the smallest singular value of the Jacobian, $\sigma_{\min}(J_h)$, tends to zero as $h \to 0$, causing the condition number $\kappa(J_h) = \sigma_{\max}(J_h) / \sigma_{\min}(J_h)$ to diverge to infinity, this is the signature of an **ill-posed** continuous problem. The [discrete systems](@entry_id:167412) are becoming progressively more unstable as they better approximate the unstable continuous problem.

-   If, after appropriate [non-dimensionalization](@entry_id:274879), $\kappa(J_h)$ is large but remains bounded as $h \to 0$, the problem is likely well-posed but **numerically ill-conditioned** [@problem_id:3511167].

### Sensitivity Analysis: The Fréchet Derivative and the Jacobian

To solve [nonlinear inverse problems](@entry_id:752643), especially with [gradient-based optimization](@entry_id:169228) methods, we must understand how the output $y$ changes in response to small changes in the parameters $\theta$. This is the domain of sensitivity analysis.

#### The Fréchet Derivative

For a forward map $F$ between Banach spaces, the relevant concept is the **Fréchet derivative**. The Fréchet derivative of $F$ at a point $\theta_*$, denoted $J(\theta_*)$ or $F'(\theta_*)$, is the unique [bounded linear operator](@entry_id:139516) that provides the [best linear approximation](@entry_id:164642) of $F$ near $\theta_*$:

$F(\theta_* + \delta\theta) \approx F(\theta_*) + J(\theta_*)(\delta\theta)$

More formally, it is the operator satisfying $\|F(\theta_* + \delta\theta) - F(\theta_*) - J(\theta_*)\delta\theta\|_Y = o(\|\delta\theta\|_X)$ as $\|\delta\theta\|_X \to 0$.

When the forward map is defined implicitly via a PDE, such as a residual equation $R(u, \theta) = 0$, we can derive an expression for the action of the Fréchet derivative without needing an explicit formula for $F$. Let $u(\theta)$ be the state solution for a given $\theta$. The equation $R(u(\theta), \theta) = 0$ holds for all $\theta$ in a neighborhood. Differentiating this identity with respect to $\theta$ using the [chain rule](@entry_id:147422) gives:

$R_u(u_*, \theta_*) u'(\theta_*) + R_\theta(u_*, \theta_*) = 0$

Here, $R_u$ and $R_\theta$ are the partial Fréchet derivatives of the residual with respect to the state and parameters, evaluated at the point of linearization $(u_*, \theta_*)$. The term $u'(\theta_*)$ is the derivative of the state with respect to the parameters. Assuming the state derivative $R_u$ is invertible (a key condition of the Implicit Function Theorem), we can solve for $u'(\theta_*)$.

Let $\delta\theta$ be a small perturbation in the parameters. The corresponding first-order change in the state, $\delta u = u'(\theta_*)\delta\theta$, is found by solving the **[tangent linear model](@entry_id:275849)** or **sensitivity equation**:

$R_u(u_*, \theta_*) \delta u + R_\theta(u_*, \theta_*) \delta\theta = 0$

The final observable is typically a function of the state, $y = M(u)$, where $M$ is an [observation operator](@entry_id:752875). If $M$ is linear, the change in the observable is $\delta y = M(\delta u)$. The action of the full forward map's Fréchet derivative is thus $J(\theta_*)\delta\theta = \delta y = M(\delta u)$, where $\delta u$ is the solution to the sensitivity equation [@problem_id:3511236].

#### Concrete Example: The Sensitivity Equation in an Electrothermal Problem

Let's make this abstract derivation concrete with a 1D steady-state electrothermal problem [@problem_id:3511169]. Consider a rod where an [electric potential](@entry_id:267554) $v(x)$ drives a current, causing Joule heating that determines a temperature field $u(x)$. The governing equation for temperature is:

$-\frac{d}{dx}\left(\theta \frac{du}{dx}\right) = \sigma\left(\frac{dv}{dx}\right)^{2}$

Here, $\theta$ is the unknown thermal conductivity. The term on the right is a heat source, which we can determine by first solving for $v(x)$. The residual for the thermal problem is $A(u, \theta) = -\frac{d}{dx}\left(\theta \frac{du}{dx}\right) - \sigma\left(\frac{dv}{dx}\right)^{2} = 0$.

To find the sensitivity of the temperature $u$ with respect to the parameter $\theta$, we define the [sensitivity function](@entry_id:271212) $s(x) = \frac{\partial u}{\partial \theta}(x)$ and differentiate the residual equation with respect to $\theta$:

$\frac{\partial}{\partial \theta} \left[ -\frac{d}{dx}\left(\theta \frac{du}{dx}\right) - \sigma\left(\frac{dv}{dx}\right)^{2} \right] = 0$

Applying the product rule and interchanging derivatives, we obtain:

$-\frac{d}{dx} \left( \frac{du}{dx} + \theta \frac{d}{dx}\left(\frac{\partial u}{\partial \theta}\right) \right) = 0 \implies -\frac{d^2u}{dx^2} - \frac{d}{dx}\left(\theta \frac{ds}{dx}\right) = 0$

This is the sensitivity equation. By substituting the expression for $\frac{d^2u}{dx^2}$ from the original state equation, we arrive at a well-defined [boundary value problem](@entry_id:138753) for the [sensitivity function](@entry_id:271212) $s(x)$. Once $s(x)$ is found, the derivative of any measurement that depends on $u$ can be computed. For example, if a measurement is $m(\theta) = \int_0^1 x u(x; \theta) dx$, its derivative (the Jacobian entry) is simply $\frac{dm}{d\theta} = \int_0^1 x s(x) dx$. This demonstrates the "direct method" of sensitivity analysis: solve one linear PDE for the sensitivity field $s(x)$ for each parameter.

#### The Jacobian Matrix and Cross-Sensitivity

When we discretize the parameters and [observables](@entry_id:267133), the Fréchet derivative is represented by a **Jacobian matrix**, $J$, where the entry $J_{ij}$ is the partial derivative of the $i$-th measurement with respect to the $j$-th parameter, $J_{ij} = \frac{\partial y_i}{\partial \theta_j}$.

In multiphysics problems, the Jacobian often reveals important couplings. For example, in a thermo-fluid system, the outlet temperature $F_1$ might depend not only on a thermal parameter like the heat source $\theta_1=q$, but also on a fluid parameter like viscosity $\theta_2=\mu$, because viscosity affects the flow rate, which in turn affects [heat transport](@entry_id:199637). The term $\frac{\partial F_1}{\partial \theta_2}$ is known as a **cross-sensitivity**. The existence of non-zero cross-sensitivities means the subsystems are coupled from an inverse problem perspective. While this coupling can make parameters harder to disentangle, it also means that measurements of one physical field (e.g., temperature) can provide information about parameters of another physical field (e.g., fluid mechanics) [@problem_id:3511211].

### Solving the Inverse Problem: Optimization and Statistical Frameworks

Armed with the forward map and its sensitivities, we can now formulate methods to solve the [inverse problem](@entry_id:634767). The two dominant frameworks are optimization-based (often deterministic) and statistical (Bayesian).

#### Least-Squares Formulation

The most common approach to [parameter estimation](@entry_id:139349) is to find the parameter vector $\theta$ that minimizes the discrepancy between the model predictions $F(\theta)$ and the measured data $y^\delta$. This is typically formulated as a **[least-squares problem](@entry_id:164198)**:

$\min_{\theta} \Phi(\theta) = \frac{1}{2} \| y^\delta - F(\theta) \|^2$

The norm $\|\cdot\|$ can be a simple Euclidean norm (Ordinary Least Squares, OLS) or a weighted norm that accounts for measurement uncertainties. If the measurement noise is Gaussian with covariance matrix $\Sigma$, the appropriate [objective function](@entry_id:267263) is based on the Mahalanobis distance, which weights the residuals by the inverse of the noise covariance:

$\min_{\theta} \Phi(\theta) = \frac{1}{2} (y^\delta - F(\theta))^T \Sigma^{-1} (y^\delta - F(\theta)) = \frac{1}{2} \| \Sigma^{-1/2} (y^\delta - F(\theta)) \|_2^2$

This approach is equivalent to finding the **Maximum Likelihood Estimate (MLE)** under the Gaussian noise assumption. It gives higher weight to more certain measurements (those with smaller variance) and properly accounts for correlations in the noise [@problem_id:3511247].

#### The Gauss-Newton Method

Since the forward map $F(\theta)$ is typically nonlinear, the least-squares [objective function](@entry_id:267263) $\Phi(\theta)$ is non-quadratic, requiring an [iterative optimization](@entry_id:178942) algorithm. The **Gauss-Newton method** is a popular choice specifically tailored for [least-squares problems](@entry_id:151619).

At each iteration $k$, starting from a guess $\theta_k$, the algorithm approximates the forward map with its first-order Taylor expansion around $\theta_k$: $F(\theta) \approx F(\theta_k) + J_k(\theta - \theta_k)$, where $J_k = J(\theta_k)$. Substituting this linear approximation into the [least-squares](@entry_id:173916) objective yields a quadratic function of the step $\delta\theta = \theta - \theta_k$. Minimizing this quadratic objective with respect to $\delta\theta$ leads to a linear system for the optimal step, known as the **Gauss-Newton [normal equations](@entry_id:142238)**:

$(J_k^T \Sigma^{-1} J_k) \delta\theta = -J_k^T \Sigma^{-1} r_k$

where $r_k = F(\theta_k) - y^\delta$ is the residual at the current iterate. The algorithm proceeds by solving this system for the step $\delta\theta$, updating the parameter guess $\theta_{k+1} = \theta_k + \delta\theta$, and iterating until convergence [@problem_id:3511191] [@problem_id:3511247].

The Gauss-Newton method is derived by approximating the true Hessian (second derivative matrix) of the [objective function](@entry_id:267263), $H = J^T \Sigma^{-1} J + S$, by only its first term, $H \approx J^T \Sigma^{-1} J$. The neglected term $S$ involves second derivatives of the forward map. This approximation is accurate under two conditions: (1) **small residuals** (i.e., the model fits the data well), as the term $S$ is multiplied by the residuals; and (2) **mild nonlinearity**, where the second derivatives of the forward map are small [@problem_id:3511191].

#### Bayesian Formulation

The Bayesian framework offers a powerful way to incorporate prior knowledge and rigorously characterize uncertainty. It treats the parameters $\theta$ as random variables and uses Bayes' theorem to update our belief about them in light of the data:

$p(\theta | y^\delta) \propto p(y^\delta | \theta) p(\theta)$

Here:
-   $p(\theta | y^\delta)$ is the **[posterior probability](@entry_id:153467) density function (PDF)**, representing our updated knowledge of $\theta$ after seeing the data.
-   $p(y^\delta | \theta)$ is the **[likelihood function](@entry_id:141927)**, which is the probability of observing the data $y^\delta$ given a parameter value $\theta$. It is the same function that underpins the MLE approach. For additive Gaussian noise, it is given by $p(y^\delta | \theta) \propto \exp\left(-\frac{1}{2} \| \Sigma^{-1/2}(y^\delta - F(\theta)) \|_2^2\right)$ [@problem_id:3511247].
-   $p(\theta)$ is the **prior PDF**, which encodes our beliefs about $\theta$ before observing the data.

The solution to the Bayesian [inverse problem](@entry_id:634767) is the entire posterior PDF, which provides a complete description of the parameter uncertainties and correlations. A common point estimate is the **Maximum A Posteriori (MAP)** estimate, which is the value of $\theta$ that maximizes the posterior PDF. This is equivalent to minimizing the negative log-posterior:

$\min_{\theta} \left( \frac{1}{2} \| \Sigma^{-1/2}(y^\delta - F(\theta)) \|_2^2 - \log p(\theta) \right)$

This reveals a profound connection: the MAP estimate is equivalent to solving a regularized [least-squares problem](@entry_id:164198), where the negative log-prior acts as a **regularization term**. For a Gaussian prior, $p(\theta) \propto \exp\left(-\frac{1}{2} \| \Gamma^{-1/2}(\theta - \theta_0) \|_2^2\right)$, where $\theta_0$ is the prior mean and $\Gamma$ is the prior covariance, the MAP estimation problem becomes:

$\min_{\theta} \left( \frac{1}{2} \| \Sigma^{-1/2}(y^\delta - F(\theta)) \|_2^2 + \frac{1}{2} \| \Gamma^{-1/2}(\theta - \theta_0) \|_2^2 \right)$

This is a form of Tikhonov regularization, where the prior penalizes deviations from the prior mean $\theta_0$. The prior covariance $\Gamma$ structures this penalty. For spatially distributed parameters, $\Gamma$ can be designed to enforce properties like smoothness by creating correlations between adjacent nodes. A powerful technique for this is the SPDE approach, which defines a Gaussian field by specifying its precision matrix (the inverse of $\Gamma$) as a differential operator, such as a power of the Helmholtz operator $(\alpha^2 I - \Delta)$. This allows for the generation of Matérn-class [random fields](@entry_id:177952) with controllable smoothness and can be extended to model physical inter-field correlations in [multiphysics](@entry_id:164478) problems [@problem_id:3511216].

### Quantifying Uncertainty and Information Content

A key advantage of statistical frameworks is the ability to quantify the uncertainty in the estimated parameters. Even in a deterministic setting, we can analyze the [information content](@entry_id:272315) of an experiment.

#### The Fisher Information Matrix (FIM)

The **Fisher Information Matrix (FIM)**, denoted $I(\theta)$, quantifies the amount of information that the observable data $y$ carry about the unknown parameter vector $\theta$. For a data model with additive Gaussian noise $\epsilon \sim \mathcal{N}(0, \Sigma)$, the FIM is given by:

$I(\theta) = J(\theta)^T \Sigma^{-1} J(\theta)$

where $J(\theta)$ is the Jacobian of the forward map [@problem_id:3511170]. Notice that this is exactly the (approximate) Hessian matrix from the Gauss-Newton method. It elegantly combines sensitivity information ($J$) with [measurement uncertainty](@entry_id:140024) information ($\Sigma^{-1}$). A key property is that for independent measurement modalities, the total information is the sum of the information from each modality: $I_{total} = I_1 + I_2$ [@problem_id:3511243].

#### Identifiability Analysis using the FIM

The FIM is a powerful tool for local [identifiability analysis](@entry_id:182774).
-   If the FIM is singular (i.e., has a zero eigenvalue), the problem is locally structurally non-identifiable. The eigenvector corresponding to the zero eigenvalue defines a direction in parameter space along which the parameters can be changed without affecting the measurements at all.
-   If the FIM is non-singular but has very small eigenvalues, this indicates weakly identifiable parameter combinations. The corresponding eigenvectors represent "sloppy" directions in parameter space where the data provide very little constraint. These directions are associated with high uncertainty and strong trade-offs (correlations) between parameters [@problem_id:3511170].

#### The Cramér-Rao Bound (CRB)

The FIM's importance is cemented by the **Cramér-Rao Bound (CRB)**. This fundamental theorem of [estimation theory](@entry_id:268624) states that for any **unbiased estimator** $\hat{\theta}$ (an estimator whose expected value is the true parameter value), its covariance matrix is bounded from below by the inverse of the FIM:

$\mathrm{Cov}(\hat{\theta}) \succeq I(\theta)^{-1}$

The notation $\succeq$ means the difference between the two matrices is positive semidefinite. This implies that the variance of the estimate for any single parameter $\theta_i$ has a lower limit: $\mathrm{Var}(\hat{\theta}_i) \ge (I(\theta)^{-1})_{ii}$. No unbiased estimation procedure can achieve a better precision than this bound. The CRB thus provides a theoretical benchmark for the best possible performance of an experiment and is an indispensable tool in [experimental design](@entry_id:142447) [@problem_id:3511243].

### A Note on Model Discrepancy

Our discussion so far has assumed that the mathematical model $F(\theta)$ used for the inversion is a perfect representation of reality. In practice, this is never the case. All models are approximations. This leads to **[model discrepancy](@entry_id:198101)** or **model error**.

Let's decompose the total error between the data $y$ and the prediction from our numerical model $F_h(\theta)$ (where $h$ denotes the discretization) at the true parameter value $\theta_\star$:

$y = F_h(\theta_\star) + \delta + \epsilon$

Here, $\epsilon$ is the random measurement noise, and $\delta$ is the deterministic model error vector, which combines both structural [model discrepancy](@entry_id:198101) (e.g., missing physics) and [numerical discretization](@entry_id:752782) error.

If we ignore this [model error](@entry_id:175815) $\delta$ and proceed with a standard least-squares estimation, our estimator will be **biased**. The expected value of the estimate, $\mathbb{E}[\widehat{\theta}_h]$, will not equal the true value $\theta_\star$. Under a [local linearization](@entry_id:169489), the bias can be shown to be:

$\mathbb{E}[\widehat{\theta}_h] - \theta_\star = (A_h^T A_h)^{-1} A_h^T \delta$

where $A_h$ is the Jacobian of the numerical model $F_h$ [@problem_id:3511257]. This important result shows that bias is introduced when the model error vector $\delta$ has a component that lies in the range of the Jacobian. A fascinating special case occurs if the [model error](@entry_id:175815) vector $\delta$ is orthogonal to the [column space](@entry_id:150809) of the Jacobian, i.e., $A_h^T \delta = 0$. In this case, the bias is zero, and the model error, though present, does not corrupt the parameter estimate. This highlights the critical interplay between the nature of the model's inadequacies and the sensitivity of its predictions to the parameters being estimated [@problem_id:3511257].