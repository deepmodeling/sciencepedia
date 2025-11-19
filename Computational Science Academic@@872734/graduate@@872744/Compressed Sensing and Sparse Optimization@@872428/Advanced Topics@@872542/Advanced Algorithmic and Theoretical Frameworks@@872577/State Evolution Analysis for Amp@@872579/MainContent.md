## Introduction
Analyzing the performance of iterative algorithms in [high-dimensional inference](@entry_id:750277) problems is notoriously difficult due to the complex, coupled dynamics between the iterates. Approximate Message Passing (AMP) algorithms, while empirically successful, present such a challenge. How can we precisely predict their performance, understand their failure modes, and optimize their design without resorting to exhaustive simulations? The answer lies in the powerful analytical framework of **State Evolution (SE)**. This theory reveals a remarkable simplification: in the large-system limit, the behavior of the entire high-dimensional AMP algorithm is exactly described by a simple, one-dimensional deterministic recursion. This allows for the precise, analytical characterization of macroscopic quantities like [mean squared error](@entry_id:276542).

This article provides a comprehensive exploration of the State Evolution framework for AMP. Across three chapters, you will gain a deep understanding of this essential tool for modern signal processing and machine learning.

First, in **Principles and Mechanisms**, we will dissect the core of the SE phenomenon. We will introduce the AMP algorithm and its corresponding SE [recursion](@entry_id:264696), demystify the decoupling principle enabled by the critical Onsager term, and explore the stability of the [recursion](@entry_id:264696)'s fixed points, which dictate the algorithm's ultimate success or failure.

Next, under **Applications and Interdisciplinary Connections**, we will showcase the practical power and broad relevance of SE. You will learn how it serves as a design tool for creating adaptive algorithms, how it predicts sharp phase transitions in performance, and how it connects AMP to foundational concepts in optimization, [statistical physics](@entry_id:142945), and information theory.

Finally, the **Hands-On Practices** section will provide you with the opportunity to apply these concepts directly. Through a series of guided problems, you will move from theory to practice, deriving fixed-point equations, optimizing denoisers, and connecting SE dynamics to the underlying [free energy landscape](@entry_id:141316).

By the end of this article, you will not only understand how State Evolution works but also how to leverage it to analyze, design, and reason about high-dimensional estimation algorithms.

## Principles and Mechanisms

The analysis of Approximate Message Passing (AMP) algorithms hinges on a remarkable phenomenon known as **State Evolution (SE)**. In the high-dimensional limit, the complex, coupled, and [nonlinear dynamics](@entry_id:140844) of the AMP iterates collapse into a simple, deterministic, one-dimensional [recursion](@entry_id:264696). This [recursion](@entry_id:264696), the [state evolution](@entry_id:755365), precisely tracks macroscopic performance metrics such as [mean squared error](@entry_id:276542) (MSE), allowing for an exact asymptotic characterization of the algorithm's behavior. This chapter elucidates the core principles and mechanisms that give rise to this powerful analytical framework. We will dissect the AMP algorithm, understand the [decoupling](@entry_id:160890) principle that enables its simplification, formalize the notion of convergence, explore the boundaries of its validity, and connect its fixed points to fundamental concepts of optimality and stability.

### The AMP Algorithm and State Evolution Recursion

We begin with the canonical linear observation model, $y = A x_0 + w$, where $y \in \mathbb{R}^m$ represents the measurements, $A \in \mathbb{R}^{m \times n}$ is a known sensing matrix, $x_0 \in \mathbb{R}^n$ is the unknown signal to be recovered, and $w \in \mathbb{R}^m$ is [additive noise](@entry_id:194447). A standard setting for analysis assumes that the entries of the matrix $A$ are independent and identically distributed (i.i.d.) Gaussian random variables, $A_{ij} \sim \mathcal{N}(0, 1/n)$, the signal $x_0$ has components drawn i.i.d. from a [prior distribution](@entry_id:141376) $P_{X_0}$, and the noise $w$ has i.i.d. components with variance $\sigma_w^2$. The system is analyzed in the large-system limit, where $n, m \to \infty$ such that the measurement ratio $m/n \to \delta \in (0, \infty)$.

The AMP algorithm generates a sequence of estimates $\{x^t\}_{t \ge 0}$ for $x_0$ via an iterative process. At each iteration $t$, the algorithm updates the signal estimate $x^t$ and a residual vector $z^t$. The standard AMP iteration, consistent with the matrix normalization $A_{ij} \sim \mathcal{N}(0, 1/n)$, is defined as follows [@problem_id:3481468]:

For $t \ge 0$, with initializations $x^0 = 0$ and $z^{-1} = 0$:
$$
x^{t+1} = \eta_t(A^\top z^t + x^t)
$$
$$
z^t = y - A x^t + \frac{1}{\delta} z^{t-1} \langle \eta'_{t-1}(A^\top z^{t-1} + x^{t-1}) \rangle
$$
Here, $\eta_t: \mathbb{R} \to \mathbb{R}$ is a **[denoising](@entry_id:165626) function** applied component-wise to its vector argument. The term $A^\top z^t + x^t$ serves as an effective observation for the denoiser. The derivative $\eta'_t$ is also applied component-wise, and $\langle v \rangle$ denotes the empirical average of the components of a vector $v \in \mathbb{R}^n$, i.e., $\langle v \rangle = \frac{1}{n} \sum_{i=1}^n v_i$. The second term in the update for the residual $z^t$ is the crucial **Onsager reaction term**. Its role is to cancel statistical dependencies that arise from reusing the matrix $A$ across iterations.

The central result of [state evolution](@entry_id:755365) is that in the large-system limit, the statistical properties of the effective observation vector, $r^t \equiv A^\top z^t + x^t$, can be described by a simple scalar model. Specifically, for any fixed iteration $t$, the joint [empirical distribution](@entry_id:267085) of the pairs $(x_{0,i}, r^t_i)$ across all components $i=1, \dots, n$ converges to the distribution of a pair of random variables $(X_0, X_0 + \tau_t Z)$, where $X_0 \sim P_{X_0}$ is a random variable representing a component of the true signal, $Z \sim \mathcal{N}(0,1)$ is a standard Gaussian variable independent of $X_0$, and $\tau_t^2$ is a deterministic scalar parameter representing the **effective noise variance**.

This parameter $\tau_t^2$ evolves according to a scalar [recursion](@entry_id:264696), the [state evolution](@entry_id:755365). For the AMP algorithm defined above, the SE [recursion](@entry_id:264696) is [@problem_id:3481468]:
$$
\tau_{t+1}^2 = \sigma_w^2 + \frac{1}{\delta} \mathbb{E}\left[ (\eta_t(X_0 + \tau_t Z) - X_0)^2 \right]
$$
The expectation $\mathbb{E}[\cdot]$ is taken over the joint distribution of $X_0$ and $Z$. The term $\mathbb{E}[(\eta_t(X_0 + \tau_t Z) - X_0)^2]$ is the predicted [mean squared error](@entry_id:276542) (MSE) of the denoiser $\eta_t$ when applied to a signal $X_0$ corrupted by Gaussian noise of variance $\tau_t^2$. The recursion is initialized with $\tau_0^2$, which depends on the noise variance and the initial guess $x^0$:
$$
\tau_0^2 = \sigma_w^2 + \frac{1}{\delta} \mathbb{E}[(X_0 - x^0_\star)^2]
$$
where $x^0_\star$ is the deterministic limit of the components of the initial guess $x^0$ (e.g., $x^0_\star = 0$ if $x^0=0$). This simple, deterministic, scalar [recursion](@entry_id:264696) fully characterizes the asymptotic performance of the complex, high-dimensional, stochastic AMP algorithm.

### The Decoupling Principle: The Mechanism Behind State Evolution

The surprising simplification from the AMP algorithm to its scalar [state evolution](@entry_id:755365) is not magic; it is a consequence of a deep **[decoupling](@entry_id:160890) principle** that emerges in high dimensions. This principle is underpinned by two key mechanisms: the role of the Gaussian matrix and the Onsager term at a microscopic level, and the [concentration of measure](@entry_id:265372) at a macroscopic level [@problem_id:3481532].

**Microscopic Mechanism: Gaussian Conditioning and the Onsager Term**

The core of the [decoupling](@entry_id:160890) lies in the properties of large Gaussian matrices. Consider the term $A^\top z^t$ that appears in the effective observation. The residual $z^t$ depends on the matrix $A$ through all previous iterates, creating a complex web of statistical dependencies. A naive analysis would be immediately intractable. However, for a matrix $A$ with i.i.d. Gaussian entries, a special property can be leveraged. A rigorous analysis using conditioning arguments reveals that the conditional distribution of $A^\top z^t$, given the history of the algorithm up to iteration $t$, can be decomposed into two distinct parts:
1.  A "bias" term that is deterministic when conditioned on the past and lies in the subspace spanned by vectors from previous iterations.
2.  A fluctuation term that is statistically independent of the past and has an i.i.d. Gaussian distribution.

The Onsager correction term is meticulously designed to be an asymptotically exact estimate of this bias term. By adding it to the residual update (effectively subtracting the bias), its influence is cancelled out. What remains is a term that behaves like a fresh, independent Gaussian noise vector at each iteration. This cancellation is the critical step that breaks the memory of the iteration and ensures the effective observation $r^t$ behaves as the simple sum of the true signal and a new Gaussian noise term, thus enabling the scalar [state evolution](@entry_id:755365) characterization [@problem_id:3481532].

**Macroscopic Mechanism: Concentration of Measure**

The state [evolution equations](@entry_id:268137) predict population quantities, such as the expected MSE, $\mathbb{E}[(\eta_t - X_0)^2]$. For this theoretical prediction to be meaningful, the corresponding empirical quantities computed from the algorithm's iterates, such as the empirical MSE $\frac{1}{n}\|x^{t+1}-x_0\|^2$, must converge to these theoretical values. This convergence is guaranteed by the phenomenon of **[concentration of measure](@entry_id:265372)**.

The modern proofs of [state evolution](@entry_id:755365) show that for any function $\psi$ belonging to a class of so-called **pseudo-Lipschitz functions**, the empirical average of $\psi$ applied to the algorithm's iterates converges in probability to the expectation of $\psi$ under the [state evolution](@entry_id:755365) model. The functions that define common performance metrics like MSE are members of this class. Therefore, this concentration result provides the bridge from the microscopic, per-coordinate [decoupling](@entry_id:160890) to the predictable behavior of macroscopic performance indicators, validating the SE predictions [@problem_id:3481532].

To make this rigorous, one defines a function $\psi: \mathbb{R}^d \to \mathbb{R}$ to be **pseudo-Lipschitz of order 2** if there exists a constant $L  \infty$ such that for all $u, v \in \mathbb{R}^d$:
$$
|\psi(u) - \psi(v)| \le L (1 + \|u\| + \|v\|) \|u - v\|
$$
This class of functions is rich enough to characterize convergence in a topology (related to the Wasserstein-2 metric) that controls not only [weak convergence](@entry_id:146650) but also the convergence of second moments. Proving that the empirical averages $\frac{1}{n} \sum_i \psi(x_{0,i}, r^t_i)$ converge to their SE-predicted expectations for all such functions $\psi$ provides a formal and powerful certification of the [state evolution](@entry_id:755365) phenomenon [@problem_id:3481508].

### Universality and Boundaries of the SE Framework

A natural and crucial question is whether [state evolution](@entry_id:755365) is a fragile phenomenon, restricted only to matrices with i.i.d. Gaussian entries. The concept of **universality** addresses this, showing that the same SE formalism often holds for broader classes of random matrices, provided their moments match those of a Gaussian matrix.

**Sub-Gaussian Matrices:**
For a matrix $A$ with i.i.d. entries that are not Gaussian but are **sub-Gaussian** (meaning their tails decay at least as fast as a Gaussian's) and have matching first two moments (mean 0, variance $1/n$), the same AMP algorithm and the same SE [recursion](@entry_id:264696) remain valid. However, the proof technique must change. The Gaussian-specific proof relies on a property called Stein's lemma ([integration by parts](@entry_id:136350)). For the universality proof, this is replaced by the more general **Lindeberg's replacement method**. This technique shows that the behavior of the system is asymptotically identical if the non-Gaussian matrix is swapped with a Gaussian one, provided their entries have uniformly bounded moments up to order four [@problem_id:3481477].

**Orthogonally Invariant Matrices:**
The situation is different for matrices with strong structural correlations, such as **orthogonally invariant ensembles**. These are matrices of the form $A = USV^\top$, where $U$ and $V$ are random [orthogonal matrices](@entry_id:153086) (e.g., drawn from the Haar distribution) and $S$ is a deterministic matrix of singular values. For this class, the standard AMP algorithm typically fails. A different class of algorithms, such as **Vector AMP (VAMP)** or **Orthogonal AMP (OAMP)**, is required. These algorithms explicitly leverage the [rotational invariance](@entry_id:137644) of the matrix ensemble. Consequently, their [state evolution](@entry_id:755365) is also different, often taking a vector- or function-valued form that tracks parameters related to the singular value distribution of $A$ using tools from random matrix theory [@problem_id:3481477]. This illustrates that while universality is a powerful concept, it is not a blanket guarantee; the matrix structure deeply influences both the correct algorithm and its corresponding analysis.

**Non-Gaussian Noise:**
The SE framework for AMP is surprisingly robust to the distribution of the [additive noise](@entry_id:194447) $w$. As long as the noise components $w_i$ are i.i.d. with [zero mean](@entry_id:271600) and [finite variance](@entry_id:269687) $\sigma_w^2$, and are independent of the matrix $A$, the standard SE recursion holds. This is because the contribution of the noise to the effective observation also undergoes a Gaussianizing effect due to the multiplication by $A^\top$, a consequence of the Central Limit Theorem. The SE equations only depend on the noise through its variance $\sigma_w^2$ [@problem_id:3481539].

However, this robustness has limits. If the observation model is not one of [additive noise](@entry_id:194447) (e.g., for Poisson statistics, [logistic regression](@entry_id:136386), or quantized outputs), the standard AMP algorithm is mismatched to the problem. In these cases, a more general framework called **Generalized AMP (GAMP)** is necessary. GAMP is designed to handle arbitrary separable output channels $p(y_i|z_i)$ and has its own corresponding [state evolution](@entry_id:755365), which requires certain regularity conditions on the channel likelihood (such as being twice differentiable with [bounded curvature](@entry_id:183139)) [@problem_id:3481539].

### Optimality and Stability of Fixed Points

State evolution not only describes the transient dynamics of AMP but, more importantly, it predicts the algorithm's final performance. Convergence occurs when the effective noise variance reaches a **fixed point** of the SE map, i.e., a value $\tau^{\star 2}$ such that $\tau^{\star 2} = F(\tau^{\star 2})$, where $F$ is the SE update function. The nature and stability of these fixed points determine whether AMP succeeds or fails.

**The Bayes-Optimal Setting and the Nishimori Identity**
A particularly insightful scenario is the **Bayes-optimal** setting, where the true signal prior $P_{X_0}$ is known and used to construct the denoiser. The optimal denoiser that minimizes the [mean squared error](@entry_id:276542) is the posterior mean estimator, $\eta(y) = \mathbb{E}[X | Y=y]$, for the scalar channel $Y=X+\tau Z$. In this setting, a special property known as the **Nishimori identity** holds:
$$
\mathbb{E}[X \eta(Y)] = \mathbb{E}[\eta(Y)^2]
$$
This identity is a direct consequence of the law of total expectation when the estimator matches the true posterior. Applying this identity to the definition of the MMSE, $\mathrm{mmse}(\tau^2) = \mathbb{E}[(X - \eta(Y))^2]$, simplifies the SE [fixed-point equation](@entry_id:203270) to a direct relationship between the effective noise and the fundamental [estimation error](@entry_id:263890) of the problem [@problem_id:3481521]:
$$
\tau^{\star 2} = \sigma_w^2 + \frac{1}{\delta} \mathrm{mmse}(\tau^{\star 2})
$$
This equation elegantly links the performance of an algorithm (AMP) to a fundamental information-theoretic quantity (the MMSE).

**The Free Energy Perspective and Stability**
The SE fixed points have a deep connection to statistical physics. They correspond to the stationary points of a thermodynamic potential known as the **Replica-Symmetric (RS) potential** or Bethe free energy density, denoted $\Phi(E)$, where $E$ is the MSE. A fixed point $E^\star$ of SE is a [stationary point](@entry_id:164360) of the potential, $\Phi'(E^\star)=0$. Furthermore, the stability of the fixed point is directly related to the geometry of this potential [@problem_id:3481535].

A **[stable fixed point](@entry_id:272562)** of the SE [recursion](@entry_id:264696), where the algorithm can converge, corresponds to a **local minimum** of the RS potential. This occurs when the derivative of the SE map has a magnitude less than one, $|F'(E^\star)|  1$. Conversely, an [unstable fixed point](@entry_id:269029) corresponds to a local maximum.

This perspective provides a powerful visualization of the algorithm's behavior. For example, some problems exhibit a "[first-order phase transition](@entry_id:144521)," where the RS potential $\Phi(E)$ has two local minima: one at a high MSE and one at a low (or zero) MSE, separated by an energy barrier. The global minimum corresponds to the true Bayes-optimal performance. However, AMP initialized with high error (e.g., $x^0=0$) will get trapped in the basin of attraction of the suboptimal, high-error minimum. To reach the [optimal solution](@entry_id:171456), the algorithm must be initialized "informatively" within the basin of the good minimum [@problem_id:3481535]. In more complex scenarios, the entire RS description may break down (a phenomenon called **Replica Symmetry Breaking** or RSB), signaling a "hard" phase where AMP is predicted to fail to find the optimal solution.

**Controlling Stability: Phase Transitions and Damping**
The stability condition provides a concrete tool for analyzing algorithmic performance. For example, in noiseless sparse recovery with a signal of sparsity $\rho$ and a denoiser with derivative $\eta'(0)=b$ at zero, the "perfect recovery" fixed point $\tau^2=0$ is stable if and only if the sampling ratio $\delta$ is above a critical threshold. By linearizing the SE map around $\tau^2=0$, one can derive this threshold precisely [@problem_id:3481530]:
$$
\delta > \delta_c(\rho, b) = \rho + (1-\rho)b^2
$$
This equation defines an algorithmic phase transition: for $\delta > \delta_c$, AMP succeeds, and for $\delta  \delta_c$, it fails.

When an SE fixed point is found to be unstable, it is sometimes possible to stabilize the algorithm's convergence through **damping**. A damped AMP update modifies the SE recursion to:
$$
\tau_{t+1} = (1 - \gamma)\tau_t + \gamma F(\tau_t)
$$
where $\gamma \in (0, 1]$ is a [damping parameter](@entry_id:167312). The stability of a fixed point $\tau^\star$ is now governed by the derivative of this new map, which is $J = 1 - \gamma + \gamma F'(\tau^\star)$. The stability condition becomes $|J|  1$. If the original map has an [unstable fixed point](@entry_id:269029) with $F'(\tau^\star)  -1$, one can often find a [damping parameter](@entry_id:167312) $\gamma  1$ that brings the new Jacobian into the stable region $(-1, 1)$, thus forcing the algorithm to converge. For instance, if analysis reveals $F'(\tau^\star) = -1.6$, solving $|1 - \gamma(1 - (-1.6))|  1$ shows that any [damping parameter](@entry_id:167312) $\gamma  10/13 \approx 0.7692$ will stabilize the fixed point, providing a practical method to ensure convergence [@problem_id:3481538].