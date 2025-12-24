## Introduction
Mathematical modeling is an indispensable tool for the design, analysis, and operation of modern energy systems. From optimizing power grids to designing next-generation reactors, high-fidelity simulations provide crucial insights. However, these full-order models (FOMs) often come with a prohibitive computational cost, making them impractical for time-sensitive tasks like real-time control, comprehensive uncertainty quantification, or large-scale design optimization. This article addresses this critical gap by introducing surrogate and [reduced-order modeling](@entry_id:177038), a suite of powerful techniques designed to create computationally efficient yet accurate representations of complex physical systems.

Across the following chapters, you will gain a comprehensive understanding of this field. The first chapter, **Principles and Mechanisms**, delves into the foundational concepts, contrasting projection-based methods that preserve physical structure with data-driven approaches that learn from simulation outputs. The second chapter, **Applications and Interdisciplinary Connections**, showcases how these models are applied to solve real-world challenges in areas ranging from [multiphysics simulation](@entry_id:145294) and control theory to digital twins. Finally, **Hands-On Practices** will guide you through practical exercises to build core skills in model reduction and sampling. By exploring both the theory and application, this article equips you with the knowledge to leverage these fast models for advanced [computational engineering](@entry_id:178146).

## Principles and Mechanisms

The "Introduction" chapter established the critical role of mathematical modeling in the design, analysis, and operation of modern energy systems. It also highlighted a fundamental challenge: the high computational cost associated with high-fidelity, or **full-order models (FOMs)**, which often renders them impractical for many-query applications such as optimization, uncertainty quantification, and real-time control. This chapter delves into the principles and mechanisms of two powerful families of techniques designed to overcome this computational barrier: **[reduced-order modeling](@entry_id:177038)** and **surrogate modeling**. We will explore how these methods systematically create computationally tractable yet accurate representations of complex energy systems.

### The Computational Burden of High-Fidelity Models

To appreciate the need for model reduction, we must first quantify the cost of full-order simulation. Energy systems are typically described by conservation laws (e.g., of mass, momentum, and energy), which manifest as coupled, [nonlinear partial differential equations](@entry_id:168847) (PDEs) or [differential-algebraic equations](@entry_id:748394) (DAEs). To solve these equations numerically, they are discretized in space and time. Spatial discretization, using methods like finite elements or finite volumes, transforms the PDE system into a large system of [ordinary differential equations](@entry_id:147024) (ODEs) or DAEs of the form $\dot{\mathbf{x}} = \mathbf{f}(\mathbf{x}, \mathbf{p}, t)$, where $\mathbf{x} \in \mathbb{R}^n$ is the state vector (e.g., temperatures and pressures at all grid points), $\mathbf{p}$ represents inputs and parameters, and $n$ is the number of degrees of freedom.

The computational cost of solving this system is often formidable. Consider a common scenario where an [implicit time integration](@entry_id:171761) scheme, such as a Backward Differentiation Formula (BDF), is used for stability. At each of the $T$ time steps, a [nonlinear system](@entry_id:162704) of equations must be solved. This is typically done using Newton's method, which may require $m$ iterations to converge. Each Newton iteration involves three main computational phases :

1.  **Residual Assembly**: Evaluating the function $\mathbf{f}(\mathbf{x}, \mathbf{p}, t)$ for a given state $\mathbf{x}$. For systems derived from local physical laws on a grid, this cost typically scales linearly with the number of degrees of freedom, i.e., $\mathcal{O}(n)$.

2.  **Jacobian Assembly**: Constructing the Jacobian matrix, $\mathbf{J} = \frac{\partial \mathbf{f}}{\partial \mathbf{x}}$, which is an $n \times n$ matrix of partial derivatives. For local operators, the Jacobian is sparse, and its assembly cost is also often $\mathcal{O}(n)$.

3.  **Linear System Solution**: Solving the linear system $\mathbf{J} \Delta \mathbf{x} = -\mathbf{f}$ for the Newton update $\Delta \mathbf{x}$. This is frequently the most expensive step. The cost scales as $\mathcal{O}(n^{\gamma})$, where $\gamma$ ranges from just above $1$ for optimal [iterative solvers](@entry_id:136910) on structured grids to as high as $3$ for [direct solvers](@entry_id:152789) on dense matrices.

The total runtime for a single simulation is therefore approximately $R_{\text{total}} \approx T \times m \times (c_R n + c_J n + c_S n^{\gamma})$, where $c_R, c_J, c_S$ are constants related to processor speed and implementation. Since $\gamma > 1$, the leading-order runtime scaling is $\mathcal{O}(T n^{\gamma})$. For a large-scale energy model where $n$ can be in the millions, a single simulation can take hours or days. For a task like uncertainty propagation, which might require thousands of such simulations, the total time becomes prohibitive, creating a clear and compelling need for faster models .

### A Taxonomy of Fast Models: Intrusive and Non-Intrusive Approaches

The strategies developed to address this computational bottleneck broadly fall into two categories: projection-based **Reduced-Order Models (ROMs)** and data-driven **Surrogate Models**.

*   A **projection-based ROM** seeks to approximate the dynamics of the high-dimensional state $\mathbf{x} \in \mathbb{R}^n$ within a low-dimensional subspace of dimension $r \ll n$. It is constructed by projecting the governing equations of the FOM onto this subspace. As a result, ROMs often retain a strong connection to the underlying physics and can inherit properties like energy conservation. Their [state variables](@entry_id:138790) are typically interpretable as amplitudes of dominant physical patterns or modes .

*   A **data-driven surrogate model** (or emulator) learns a direct input-output mapping from system parameters $\mathbf{p}$ to quantities of interest $\mathbf{y}$ from a set of training data generated by the FOM. These models, which include techniques like Gaussian processes and neural networks, often treat the FOM as a "black box." They are typically very fast to evaluate but provide less physical insight, and their accuracy can degrade significantly when queried with inputs outside the domain covered by the training data .

This distinction is closely related to the concepts of **intrusive** and **non-intrusive** modeling .

*   **Intrusive methods** require access to and modification of the FOM's source code. Projection-based ROMs are typically intrusive because constructing the reduced system requires access to the internal operators (e.g., the matrices and function handles that define $\mathbf{f}$) to perform projections. For [nonlinear systems](@entry_id:168347), this often involves significant code rewriting to implement techniques like **[hyper-reduction](@entry_id:163369)**, which are necessary for [computational efficiency](@entry_id:270255).

*   **Non-intrusive methods** treat the FOM solver as a black box, interacting with it only by providing inputs and receiving outputs. Most data-driven surrogate models are non-intrusive, as they are trained on input-output data pairs generated by running the original, unmodified solver. This makes them easier to implement in many practical settings where the FOM code is complex, proprietary, or otherwise difficult to modify.

A third category, **gray-box models**, occupies the middle ground. These models exploit some known physical structure of the system but use data to calibrate unknown parameters or components. For example, one might assume the form of the governing equations but leave physical constants like heat transfer coefficients as parameters to be learned from experimental data. Gray-box models are partially intrusive, as they require knowledge of the model's structure but may not require a full rewrite of the solver code .

### Principle I: Projection-Based Reduced-Order Modeling

Projection-based ROMs build a computationally cheap model by restricting the dynamics of the FOM to a carefully chosen low-dimensional subspace. This process involves three key steps: constructing the subspace, projecting the governing equations, and, for nonlinear systems, efficiently evaluating the projected nonlinear terms.

#### Constructing the Subspace: Proper Orthogonal Decomposition

The cornerstone of many data-driven ROMs is **Proper Orthogonal Decomposition (POD)**, a technique for finding a low-dimensional basis that is optimal for representing a given set of [high-dimensional data](@entry_id:138874). In the context of dynamical systems, we first generate a set of "snapshots" of the system's [state evolution](@entry_id:755365), $\mathbf{x}(t_1), \mathbf{x}(t_2), \dots, \mathbf{x}(t_m)$, by running a full-order simulation under representative conditions. These snapshots, after being centered by subtracting their temporal mean, form the columns of a **[snapshot matrix](@entry_id:1131792)** $\mathbf{X} \in \mathbb{R}^{n \times m}$.

POD seeks an orthonormal basis $\{\mathbf{v}_i\}_{i=1}^r$ that maximizes the average squared projection of the snapshot data onto that basis. This is mathematically equivalent to **Principal Component Analysis (PCA)**, which seeks the directions of maximal variance in the data. Both problems lead to finding the eigenvectors of the spatial covariance matrix $\mathbf{C} = \frac{1}{m-1}\mathbf{X}\mathbf{X}^\top$. The POD basis vectors are simply the principal components of the snapshot data .

Directly computing eigenvectors of the $n \times n$ matrix $\mathbf{C}$ is infeasible if $n$ is large. However, the **Singular Value Decomposition (SVD)** of the [snapshot matrix](@entry_id:1131792), $\mathbf{X} = \mathbf{U} \mathbf{\Sigma} \mathbf{V}^\top$, provides a direct and powerful connection. The columns of the matrix $\mathbf{U} \in \mathbb{R}^{n \times n}$ are precisely the eigenvectors of $\mathbf{X}\mathbf{X}^\top$. Therefore, the POD basis vectors (or spatial modes) are the first $r$ columns of $\mathbf{U}$, corresponding to the $r$ largest singular values $\sigma_i$. These singular values quantify the importance of each mode; the fraction of the total data energy (squared Frobenius norm) captured by an $r$-dimensional POD basis is given by $\frac{\sum_{i=1}^{r} \sigma_{i}^{2}}{\sum_{i=1}^{\min(n,m)} \sigma_{i}^{2}}$ .

When the number of snapshots $m$ is much smaller than the state dimension $n$ ($m \ll n$), the **[method of snapshots](@entry_id:168045)** provides an efficient computational shortcut. Instead of solving the large $n \times n$ [eigenvalue problem](@entry_id:143898) for $\mathbf{X}\mathbf{X}^\top$, one solves the small $m \times m$ eigenvalue problem for the temporal Gramian matrix $\mathbf{X}^\top\mathbf{X}$. The POD modes (columns of $\mathbf{U}$) can then be recovered from the eigenvectors of this small matrix, drastically reducing the cost of constructing the basis .

#### Projecting the Dynamics: Galerkin and Petrov-Galerkin Methods

Once a low-rank basis, represented by the matrix $\mathbf{V} \in \mathbb{R}^{n \times r}$ whose columns are the POD modes, has been constructed, the state is approximated as a [linear combination](@entry_id:155091) of these basis vectors: $\mathbf{x}(t) \approx \mathbf{V}\mathbf{z}(t)$, where $\mathbf{z}(t) \in \mathbb{R}^r$ is the vector of reduced coordinates.

The next step is to derive the governing equations for $\mathbf{z}(t)$. This is achieved by substituting the approximation into the FOM equations and enforcing that the resulting residual is orthogonal to a chosen test subspace. This is the **[method of weighted residuals](@entry_id:169930)**. Let the FOM be the linear time-invariant (LTI) system $\dot{\mathbf{x}} = \mathbf{A}\mathbf{x} + \mathbf{B}\mathbf{u}$. Substituting the approximation yields the residual $\mathbf{R}(t) = \mathbf{V}\dot{\mathbf{z}}(t) - \mathbf{A}\mathbf{V}\mathbf{z}(t) - \mathbf{B}\mathbf{u}(t)$. We enforce orthogonality with respect to a test basis $\mathbf{W} \in \mathbb{R}^{n \times r}$ by setting $\mathbf{W}^\top \mathbf{R}(t) = \mathbf{0}$. This yields the general projected system :
$$ \dot{\mathbf{z}} = (\mathbf{W}^\top \mathbf{V})^{-1} \mathbf{W}^\top \mathbf{A} \mathbf{V} \mathbf{z} + (\mathbf{W}^\top \mathbf{V})^{-1} \mathbf{W}^\top \mathbf{B} \mathbf{u} $$
This can be written as $\dot{\mathbf{z}} = \mathbf{A}_r \mathbf{z} + \mathbf{B}_r \mathbf{u}$, where $\mathbf{A}_r$ and $\mathbf{B}_r$ are the reduced system matrices of size $r \times r$ and $r \times m$, respectively.

The choice of the test basis $\mathbf{W}$ defines the type of projection:

*   **Galerkin Projection**: Here, the test basis is chosen to be the same as the trial basis, i.e., $\mathbf{W} = \mathbf{V}$. This means the residual is made orthogonal to the approximation subspace itself. If the basis $\mathbf{V}$ is orthonormal ($\mathbf{V}^\top\mathbf{V} = \mathbf{I}$), the reduced matrices simplify to $\mathbf{A}_r = \mathbf{V}^\top \mathbf{A} \mathbf{V}$ and $\mathbf{B}_r = \mathbf{V}^\top \mathbf{B}$. This corresponds to an [orthogonal projection](@entry_id:144168) of the dynamics.

*   **Petrov-Galerkin Projection**: Here, the test basis is chosen to be different from the trial basis, $\mathbf{W} \neq \mathbf{V}$. This corresponds to an [oblique projection](@entry_id:752867). This additional freedom in choosing $\mathbf{W}$ is powerful and can be used to enforce specific desirable properties in the ROM, such as preserving stability or system structure.

#### The Nonlinear Bottleneck and Hyper-reduction

For a nonlinear FOM $\dot{\mathbf{x}} = \mathbf{f}(\mathbf{x})$, a Galerkin-projected ROM takes the form $\dot{\mathbf{z}} = \mathbf{V}^\top \mathbf{f}(\mathbf{V}\mathbf{z})$. Evaluating the right-hand side of this equation presents a major computational challenge. One must first reconstruct the full-dimensional state approximation $\mathbf{x}_{approx} = \mathbf{V}\mathbf{z}$ (an $\mathcal{O}(nr)$ operation), then evaluate the nonlinear function $\mathbf{f}(\mathbf{x}_{approx})$ at all $n$ components (an $\mathcal{O}(n)$ operation), and finally project the result back down (an $\mathcal{O}(nr)$ operation). The cost of evaluating the nonlinearity, which scales with the FOM dimension $n$, persists and becomes a bottleneck, negating the benefits of reduction.

**Hyper-reduction** techniques are designed to overcome this bottleneck by approximating the nonlinear term without computing all its components. Two prominent methods are the **Discrete Empirical Interpolation Method (DEIM)** and **Gappy POD** . Both begin by constructing a low-dimensional basis $\mathbf{U} \in \mathbb{R}^{n \times m}$ for the nonlinear term itself, using POD on snapshots of $\mathbf{f}(\mathbf{x})$. The goal is then to find the coefficients $\mathbf{c}$ in the approximation $\mathbf{f}(\mathbf{x}) \approx \mathbf{U}\mathbf{c}$ by only evaluating $\mathbf{f}$ at a small number of $p$ "magic points" or indices.

*   **DEIM** is an interpolation-based method. It uses a [greedy algorithm](@entry_id:263215) to select exactly $m$ interpolation points, where $m$ is the dimension of the basis $\mathbf{U}$. It then computes the coefficients $\mathbf{c}$ by enforcing that the approximation $\mathbf{U}\mathbf{c}$ exactly matches the true values of $\mathbf{f}(\mathbf{x})$ at these $m$ points. This involves solving a small $m \times m$ linear system.

*   **Gappy POD** is a [least-squares](@entry_id:173916)-based method. It typically uses more sample points than basis vectors ($p \ge m$) and finds the coefficients $\mathbf{c}$ that best fit the sampled values in a [least-squares](@entry_id:173916) sense. This approach is generally more robust to noise or approximation errors than interpolation.

In both cases, the online cost of evaluating the nonlinear term is reduced from $\mathcal{O}(n)$ to one that scales with the much smaller numbers $m$ and $p$, making the ROM truly fast even for nonlinear problems.

#### The Importance of Structure Preservation

For models of physical systems, accuracy and speed are not the only concerns. It is often critical that the reduced model inherits fundamental physical properties of the full model, such as conservation of energy, passivity, and stability. A naive projection can easily destroy these properties, leading to a ROM that is unreliable, produces non-physical results, or even becomes unstable.

A powerful framework for analyzing and preserving such properties is that of **port-Hamiltonian systems** . These systems explicitly model the [energy flow](@entry_id:142770) through a system via ports. The [state equations](@entry_id:274378) are structured to reflect the energy storage (Hamiltonian $H$), energy-conserving interconnection (a skew-symmetric matrix $\mathbf{J}$), and [energy dissipation](@entry_id:147406) (a [positive semi-definite matrix](@entry_id:155265) $\mathbf{R}$). The time evolution of the stored energy $H(\mathbf{x})$ is then given by the energy balance:
$$ \frac{d}{dt} H(\mathbf{x}) = -\text{dissipated energy} + \text{supplied energy} $$
This structure guarantees that the unforced ($\mathbf{u}=\mathbf{0}$) system cannot spontaneously generate energy ($\frac{d}{dt}H \le 0$), making the stored energy $H$ a natural Lyapunov function that proves the system's stability. It also ensures the system is **passive**, meaning it cannot deliver more energy to its environment than has been supplied to it, a fundamental property of physical systems.

**Structure-preserving [model reduction](@entry_id:171175)** aims to construct a ROM that retains this port-Hamiltonian structure. This is often achieved using a carefully chosen Petrov-Galerkin projection where the test basis $\mathbf{W}$ is constructed to ensure that the reduced matrices $\mathbf{J}_r$ and $\mathbf{R}_r$ remain skew-symmetric and positive semi-definite, respectively. By preserving the underlying physical structure, these ROMs are guaranteed to be passive and stable, making them far more reliable for long-time simulation and control design than non-structure-preserving alternatives .

### Principle II: Data-Driven and Physics-Informed Surrogate Modeling

This second family of methods constructs fast models by learning input-output relationships directly from data, often without direct reference to the governing equations during the prediction phase.

#### Gaussian Process Regression

**Gaussian Process (GP) regression**, also known as [kriging](@entry_id:751060), is a probabilistic, non-intrusive [surrogate modeling](@entry_id:145866) technique. A GP defines a [prior distribution](@entry_id:141376) over functions. It is fully specified by a **mean function** $\mu(x)$, which represents the expected output before any data is observed, and a **covariance function** or **kernel** $k(x, x')$, which models the correlation between the function's outputs at two different input points $x$ and $x'$ .

The power of GPs lies in their application of Bayesian inference. Given a set of $n$ noisy training observations $\{(x_i, y_i)\}$, where $y_i = f(x_i) + \varepsilon_i$, we can condition the GP prior on this data to obtain a posterior distribution over functions. This posterior is also a Gaussian process. For any new test point $x_*$, the posterior provides not just a single point prediction but a full predictive probability distribution for the output $f(x_*)$.

The key results of this conditioning are the formulas for the [posterior mean](@entry_id:173826) and variance:
*   **Posterior Mean**: This is the optimal point prediction for $f(x_*)$ and is a weighted average of the observed training outputs, corrected by the prior mean. The weights depend on the covariance between the test point and the training points, as defined by the kernel.
*   **Posterior Variance**: This provides a measure of uncertainty in the prediction. The variance is typically smallest near the training data points and grows larger as one moves away from them, providing a principled way to quantify the surrogate's confidence.

The [posterior mean](@entry_id:173826) derived from this Bayesian framework is identical to the predictor obtained from the frequentist approach of finding the **Best Linear Unbiased Predictor (BLUP)**. This dual interpretation solidifies GP regression as a robust and theoretically sound method for surrogate modeling .

#### Polynomial Chaos Expansions

For problems in **Uncertainty Quantification (UQ)**, where inputs are described by probability distributions, **Polynomial Chaos Expansion (PCE)** provides a powerful surrogate modeling framework. PCE represents the model output $Y$, which is a random variable, as a spectral expansion in polynomials that are orthogonal with respect to the probability measure of the uncertain inputs $\mathbf{X}$ :
$$ Y = f(\mathbf{X}) = \sum_{j=0}^{\infty} c_j \Psi_j(\mathbf{X}) $$
The crucial property is the **orthogonality** of the basis polynomials $\Psi_j$, which means the expectation of their product is zero: $\mathbb{E}[\Psi_j(\mathbf{X}) \Psi_k(\mathbf{X})] = 0$ for $j \neq k$. This orthogonality allows the deterministic coefficients $c_j$ to be computed easily via projection.

The choice of orthogonal polynomial family is dictated by the probability distribution of the inputs, a relationship described by the **Wiener-Askey scheme**. For example:
*   Uniformly distributed inputs correspond to Legendre polynomials.
*   Normally (Gaussian) distributed inputs correspond to Hermite polynomials.
*   Gamma-distributed inputs correspond to Laguerre polynomials.

If the inputs are independent, the multivariate [orthogonal basis](@entry_id:264024) can be constructed as a [tensor product](@entry_id:140694) of the appropriate univariate polynomial families. Once the PCE is constructed, it can be used as an extremely fast surrogate. Furthermore, statistical moments like the mean and variance of the output $Y$ can be computed analytically from the PCE coefficients, avoiding the need for expensive Monte Carlo sampling.

#### Neural Network Surrogates: Data-Driven vs. Physics-Informed

Neural networks have emerged as a highly flexible and powerful class of function approximators for [surrogate modeling](@entry_id:145866). Two main paradigms exist in the context of physical systems .

1.  **Feedforward Neural Network (FFNN) Surrogates**: This is the standard, non-intrusive, data-driven approach. An FFNN is trained to learn the black-box mapping from system inputs (e.g., design parameters $\theta$) to outputs (e.g., a quantity of interest $y$). The training process minimizes a loss function that measures the misfit between the network's predictions and a set of "ground truth" data generated by the FOM. The physics of the problem is only implicitly learned through this data. A well-trained FFNN can be extremely fast, but it offers no guarantee of physical consistency and its accuracy depends entirely on the quality and coverage of the training data.

2.  **Physics-Informed Neural Networks (PINNs)**: PINNs represent a paradigm shift toward gray-box or white-box neural [network modeling](@entry_id:262656). Instead of learning an input-output map, a PINN is trained to directly approximate the solution field of a PDE itself, for example, the temperature field $T(\mathbf{x}, t)$. The network's inputs are the [independent variables](@entry_id:267118) (position $\mathbf{x}$ and time $t$), and its output is the predicted temperature.

The key innovation of PINNs lies in the construction of the loss function. The network is trained not primarily on solution data, but by penalizing violations of the governing physical laws. The total loss function is a weighted sum of:
*   The **PDE residual loss**: The governing PDE is evaluated using the network's output, and the squared residual is minimized at a set of "collocation points" throughout the space-time domain.
*   The **boundary condition loss**: The mismatch between the network's prediction and the prescribed boundary conditions is penalized.
*   The **initial condition loss**: The mismatch with the initial state is penalized.

This is made possible by **automatic differentiation (AD)**, a technique that allows for the exact computation of the derivatives of the neural network's output with respect to its inputs. AD enables the evaluation of the [differential operators](@entry_id:275037) in the PDE without resorting to numerical approximations like [finite differences](@entry_id:167874). Because the physics itself provides the supervisory signal, PINNs can, in principle, be trained with very little or even no solution data from a FOM, learning the solution directly from the governing equations . Practical considerations such as normalization of variables, adaptive weighting of loss terms, and careful sampling of collocation points are crucial for the successful training of PINNs .