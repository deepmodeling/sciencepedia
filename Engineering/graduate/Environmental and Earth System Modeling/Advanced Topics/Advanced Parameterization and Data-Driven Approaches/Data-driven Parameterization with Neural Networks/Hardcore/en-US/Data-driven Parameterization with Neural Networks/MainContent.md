## Introduction
Earth System Models (ESMs) are the cornerstone of modern climate science, yet their accuracy is fundamentally limited by a persistent challenge: the representation of physical processes occurring at scales too small to be explicitly resolved. From turbulent eddies to cloud microphysics, these subgrid-scale processes exert a crucial influence on the large-scale climate. The necessity of representing their collective effect using only resolved-scale information gives rise to the "closure problem," a knowledge gap that traditional parameterizations, often based on simplified heuristics, struggle to bridge effectively. As computational power increases and models enter the "gray zone" where process scales and grid scales overlap, these traditional methods can fail, motivating the search for more flexible, data-driven solutions.

This article provides a graduate-level introduction to using neural networks for data-driven parameterization, a powerful approach for learning these complex subgrid-scale relationships directly from high-resolution data. Over the next three chapters, you will gain a comprehensive understanding of this rapidly evolving field. We will begin by exploring the **Principles and Mechanisms**, dissecting the closure problem and the theoretical foundations that allow neural networks to act as function approximators, while highlighting the critical need to enforce physical consistency and numerical stability. Next, we will survey a wide range of **Applications and Interdisciplinary Connections**, demonstrating how these methods are applied to model atmospheric, oceanic, and land-surface processes, and how the same principles extend to computational mechanics and [systems biology](@entry_id:148549). Finally, a series of **Hands-On Practices** will offer opportunities to engage with key design choices in building robust and physically sound neural network parameterizations.

This structure is designed to build from foundational theory to practical application, equipping you with the knowledge to develop and critically evaluate data-driven parameterizations in your own scientific domain. Let's start by examining the fundamental principles that govern this approach.

## Principles and Mechanisms

### The Closure Problem in Earth System Models

Earth System Models (ESMs) are founded upon fundamental conservation laws of physics, such as the conservation of mass, momentum, and energy. These laws are expressed as continuous partial differential equations (PDEs). For instance, the evolution of a conserved scalar quantity $\phi(\mathbf{x}, t)$, such as temperature or the concentration of a chemical tracer, advected by a velocity field $\mathbf{u}(\mathbf{x}, t)$ and influenced by sources and sinks $\mathcal{S}$, can be described by:

$$
\frac{\partial \phi}{\partial t} + \nabla \cdot (\mathbf{u}\phi) = \mathcal{S}(\phi, \mathbf{x}, t)
$$

Due to computational constraints, ESMs cannot resolve all scales of motion, from millimeters to thousands of kilometers. Instead, they solve these equations on a discrete grid with a characteristic spacing, $\Delta x$. This act of discretization implicitly involves a **[spatial filtering](@entry_id:202429)** operation. We can formalize this by defining a filtering operator $\mathcal{F}_\Delta[\cdot]$, which separates the fields into a **resolved-scale** component (the overbar) and an **unresolved-scale** or **subgrid-scale** component (the prime), such that $\phi = \overline{\phi} + \phi'$ and $\mathbf{u} = \overline{\mathbf{u}} + \mathbf{u}'$.

Applying this filtering operator to the governing conservation law reveals the central challenge of parameterization. Because the filtering operator does not commute with nonlinear terms, unclosed terms emerge. Focusing on the nonlinear advection term, $\nabla \cdot (\mathbf{u}\phi)$, we find:

$$
\frac{\partial \overline{\phi}}{\partial t} + \nabla \cdot (\overline{\mathbf{u}}\overline{\phi}) = \overline{\mathcal{S}} - \nabla \cdot (\overline{\mathbf{u'}\phi'} + \overline{\mathbf{u}\phi'} + \overline{\mathbf{u}'\overline{\phi}})
$$

This equation for the resolved field $\overline{\phi}$ is not closed because it depends on correlations involving the unresolved fluctuations $\phi'$ and $\mathbf{u}'$. This entire unclosed portion, which represents the net effect of subgrid-scale processes on the resolved flow, is often consolidated into a **subgrid-scale (SGS) flux** term, $\boldsymbol{\tau}_\Delta = \overline{\mathbf{u}\phi} - \overline{\mathbf{u}}\overline{\phi}$ . The filtered equation then highlights the **closure problem**:

$$
\frac{\partial \overline{\phi}}{\partial t} + \nabla \cdot (\overline{\mathbf{u}}\overline{\phi}) = \overline{\mathcal{S}} - \nabla \cdot \boldsymbol{\tau}_\Delta
$$

To solve for the evolution of $\overline{\phi}$, we must find a way to represent, or **parameterize**, the subgrid [flux divergence](@entry_id:1125154) $\nabla \cdot \boldsymbol{\tau}_\Delta$ using only the known, resolved-scale variables.

To make this more concrete, consider a one-dimensional tracer $q(x,t)$ governed by $\partial_{t} q + \partial_{x} (u q) = S(q)$, where $S(q) = -\lambda q + \alpha q^2$ is a nonlinear source term. Applying a Reynolds averaging operator (a type of filter) and decomposing the fields into mean ($\overline{q}, \overline{u}$) and fluctuating ($q', u'$) parts yields the averaged equation :

$$
\partial_{t} \overline{q} + \partial_{x} (\overline{u}\overline{q}) = S(\overline{q}) - \partial_{x}(\overline{u'q'}) + \alpha\overline{q'^2}
$$

Here, we see two distinct unclosed terms that arise from the nonlinearities: the divergence of the **eddy flux**, $-\partial_{x}(\overline{u'q'})$, and a correction to the source term, $\alpha\overline{q'^2}$, which depends on the subgrid tracer variance. The sum of these terms, $\mathcal{T}(x) = -\partial_{x}(\overline{u'q'}) + \alpha\overline{q'^2}$, is the total unresolved tendency that a parameterization must represent.

It is critical to distinguish this physical closure problem from two other sources of error in ESMs :
1.  **Numerical Discretization Error**: This is a mathematical error that arises from approximating continuous derivatives with discrete formulas on the model grid. This error, often characterized by a truncation residual $T_{\Delta x}$, depends on the grid spacing and the order of the numerical scheme, and it would exist even if the governing equations were linear and fully resolved.
2.  **Model Structural Error**: This is an error in the physical formulation of the model itself. It occurs if the governing equations are incomplete (e.g., missing key chemical reactions in $\mathcal{S}$) or if the functional forms of existing parameterizations are incorrect.

Data-driven parameterization with neural networks is a modern approach to tackling the physical closure problem—that is, to learn a representation for terms like $\boldsymbol{\tau}_\Delta$ from data. It is not designed to eliminate numerical discretization error.

### The Role of Parameterization and the Data-Driven Approach

A **parameterization** is a model that provides the missing subgrid-scale tendency as a function of the resolved state. Traditional parameterizations are often based on simplified physical reasoning and heuristic arguments. A common underlying assumption is that of **scale separation**, which posits that the [characteristic length scales](@entry_id:266383) of the subgrid processes are much smaller than the model grid spacing ($L_{process} \ll \Delta x$).

Deep [moist convection](@entry_id:1128092) provides a classic example. Individual convective updrafts have characteristic radii of $L_c \approx 2$ km. In a [global climate model](@entry_id:1125665) with a grid spacing of $\Delta x = 25$ km, the condition $L_c \ll \Delta x$ holds. Convection is entirely unresolved, and a parameterization must represent its bulk statistical effect on the grid cell. However, as [model resolution](@entry_id:752082) increases, we enter a **gray zone** where the grid spacing becomes comparable to the process scale ($L_{process} \approx \Delta x$). For instance, in a regional model with $\Delta x = 3$ km, the scale separation assumption is violated. The model's resolved dynamics will begin to explicitly simulate parts of the convective motion. A traditional parameterization, if applied unchanged, would "double-count" the [convective transport](@entry_id:149512), leading to significant errors .

This challenge motivates the need for more flexible, **scale-aware** parameterizations that can adapt their behavior as resolution changes. Neural networks (NNs), as powerful and versatile function approximators, are well-suited for this task. The objective of a data-driven approach is to learn the mapping from the resolved [state variables](@entry_id:138790) (and potentially grid-scale information like $\Delta x$) to the true subgrid tendency. This "ground truth" target for training is defined by the budget of the filtered equations. It is the residual required to close the budget:

$$
\text{SGS Tendency} = \left( \frac{\partial \overline{\phi}}{\partial t} \right)_{\text{True}} - \left( \frac{\partial \overline{\phi}}{\partial t} \right)_{\text{Resolved}}
$$

The true tendency of the filtered field, $(\partial_t \overline{\phi})_{\text{True}}$, is calculated by running a very high-resolution, ground-truth simulation and explicitly filtering its output. The resolved tendency, $(\partial_t \overline{\phi})_{\text{Resolved}}$, is calculated by applying the resolved dynamical operators of the coarse model to the filtered state. The difference between the two is precisely the subgrid tendency that the NN must learn .

### Theoretical Foundations of Neural Network Parameterizations

The primary theoretical justification for using NNs as parameterizations is the **Universal Approximation Theorem (UAT)**. In essence, the UAT states that a standard [feedforward neural network](@entry_id:637212) with a single hidden layer containing a finite number of neurons and a suitable non-polynomial [activation function](@entry_id:637841) can approximate any continuous function on a compact (i.e., closed and bounded) subset of $\mathbb{R}^d$ to an arbitrary degree of accuracy .

This theorem provides confidence that, in principle, an NN possesses the expressive power to represent the complex, nonlinear relationship between the resolved state and the subgrid tendency. However, a graduate-level understanding requires appreciating what the UAT does *not* guarantee:

*   **Physical Constraints**: The UAT is a purely mathematical statement about [function approximation](@entry_id:141329). It provides no guarantee that the learned function will obey fundamental physical principles like the conservation of energy, mass, or momentum. A standard NN trained to minimize a simple loss function like mean squared error may produce tendencies that spuriously create or destroy conserved quantities. These constraints must be explicitly enforced through the network's architecture or the training process .

*   **Dynamical Stability**: The UAT concerns the static approximation of a function. It offers no assurance that when the NN is coupled interactively within a prognostic model and integrated forward in time, the resulting dynamical system will be stable. Even small approximation errors can be amplified over time, leading to explosive instabilities or unphysical [model drift](@entry_id:916302) .

*   **Generalization**: The UAT guarantees approximation on a *[compact set](@entry_id:136957)*. In practice, this means the NN can be expected to perform well on inputs that are similar to those seen during training. It provides no guarantees for out-of-distribution (OOD) generalization, i.e., for inputs far from the training [data manifold](@entry_id:636422). NNs are known to be unreliable extrapolators.

*   **Stochasticity and Memory**: The UAT applies to deterministic, memoryless (Markovian) functions. However, many subgrid processes are inherently stochastic and may depend on their history (non-Markovian). To apply the UAT, the problem must be reformulated. A common approach is to have the NN learn the *conditional mean* of the subgrid tendency, $\mathbb{E}[\mathbf{t} | \mathbf{x}]$, which is a deterministic function of the current resolved state $\mathbf{x}$. This effectively averages out the unresolved randomness and history, a point to which we will return .

### Practical Implementation: Ensuring Physical Consistency

The theoretical limitations of NNs necessitate careful design choices to ensure that a data-driven parameterization is physically consistent and numerically robust when coupled to an ESM.

#### Conservation Laws

The conservation of scalar quantities like water vapor or energy is a cornerstone of [geophysical modeling](@entry_id:749869). A parameterization representing subgrid transport must not act as an artificial source or sink of these quantities. In a finite-volume model, this is achieved by formulating the parameterization in a **flux-divergence** form.

Consider the three main strategies for an NN's output :

1.  **Cell Tendencies**: The NN predicts a single tendency value, $T_i^{\mathrm{sg}}$, for each grid cell $i$. This tendency is added directly to the right-hand side of the prognostic equation. This is the simplest approach but is **not conservative**. Conservation requires that the total mass-weighted tendency over the domain sums to zero, $\sum_i V_i T_i^{\mathrm{sg}} = 0$. A standard NN has no mechanism to enforce this global constraint, leading to spurious creation or destruction of the conserved quantity.

2.  **Face Fluxes**: The NN predicts the subgrid flux, $\Delta F_f^{\mathrm{sg}}$, at each face $f$ between adjacent grid cells. The subgrid tendency for cell $i$ is then computed as the divergence of these fluxes: $-\frac{1}{V_i} \sum_{f \in \partial i} A_f \Delta F_f^{\mathrm{sg}}$. If the flux leaving cell $i$ through face $f$ is defined to be equal and opposite to the flux entering cell $j$ through the same face, the scheme is **exactly conservative** by construction. The sum of fluxes over all interior faces in a closed domain forms a [telescoping sum](@entry_id:262349) that cancels to zero. This is the physically correct approach for parameterizing [transport processes](@entry_id:177992)  .

3.  **Closure Coefficients**: The NN predicts physical coefficients, such as an eddy diffusivity $\kappa_f$, which are then used in a physically-based flux formula (e.g., $\Delta F_f^{\mathrm{sg}} = -\kappa_f A_f (q_j - q_i)/d_f$). This is also a flux-based, conservative approach that has the added benefit of being more physically interpretable.

Furthermore, flux-based approaches (2 and 3) reduce **operator-[splitting error](@entry_id:755244)**. By combining the parameterized subgrid fluxes with the resolved dynamical fluxes *before* computing the divergence, the model executes a single, unified update. The tendency-based approach (1) constitutes a split scheme, which can introduce [numerical errors](@entry_id:635587) of order $\Delta t$ and compromise the simulation's accuracy and stability .

#### Numerical Stability

A common failure mode of NN parameterizations is causing the host model to become numerically unstable. This occurs if the NN produces excessively large tendencies in response to small changes in the input state.

We can analyze this by considering a simple ODE model, $\frac{dq}{dt} = g(q) + f_{\theta}(q)$, where $g(q)$ is a stable physical relaxation process (e.g., $g'(q^*) = -\lambda  0$) and $f_{\theta}(q)$ is the NN tendency. Using a forward Euler time-stepping scheme, the update is $q_{n+1} = q_n + h(g(q_n) + f_{\theta}(q_n))$. A linear stability analysis shows that the amplification factor for small perturbations is $1 + h(k-\lambda)$, where $k = f'_{\theta}(q^*)$ is the gradient of the NN at the fixed point. For stability, we need $|1 + h(k-\lambda)|  1$, which leads to the constraint $\lambda - 2/h  k  \lambda$ .

This reveals a critical insight: if the NN's local gradient $k$ is positive and large, it can counteract the physical damping $\lambda$ and destabilize the system. For example, if $\lambda = 1/(7200 \text{ s})$ and the NN learns a gradient $k = 0.7\lambda$, the stability analysis dictates that the maximum stable timestep is $h_{max} = 4.8 \times 10^4$ s. If the NN learned an even steeper gradient, this limit would shrink further, potentially making the model unusable .

This concept can be generalized using **Lipschitz continuity**. A function $P_\theta(x)$ is Lipschitz continuous with constant $L_P$ if $\|P_\theta(x) - P_\theta(y)\| \le L_P \|x - y\|$ for all $x, y$. The Lipschitz constant bounds the maximum "steepness" of the function. For the coupled system $\frac{dx}{dt} = F(x) + P_\theta(x)$, the Lipschitz constant of the one-step Euler map, $G(x) = x + \Delta t(F(x) + P_\theta(x))$, is bounded by $L_G \le 1 + \Delta t(L_F + L_P)$, where $L_F$ and $L_P$ are the Lipschitz constants of the resolved dynamics and the NN, respectively. To prevent explosive growth of perturbations, $L_G$ must be kept close to 1, which requires controlling $L_P$ .

For an MLP composed of alternating weight matrices ($W_i$) and $1$-Lipschitz activation functions (like ReLU or tanh), an upper bound on its Lipschitz constant can be estimated as the product of the spectral norms of its weight matrices: $L_P \le \prod_i \|W_i\|_2$. This provides a practical tool for monitoring and constraining the NN's steepness during training to promote online stability .

### Advanced Topics: Stochasticity and Uncertainty

#### Stochastic Parameterization

Deterministic NNs trained on the conditional mean tendency, $\mathbb{E}[\mathbf{t} | \mathbf{x}]$, capture the average effect of subgrid processes but miss their inherent variability. This missing variability can be crucial for triggering large-scale transitions or for correctly representing extreme events. This motivates the development of **stochastic parameterizations**, which represent the subgrid tendency not as a single value but as a probability distribution.

The **Mori-Zwanzig formalism** provides a rigorous theoretical foundation for this. It shows that when a high-dimensional dynamical system is projected onto a low-dimensional subspace of resolved variables, the resulting evolution equation for the resolved variables is not a simple ODE. Instead, it takes the form of a Generalized Langevin Equation, which includes a memory term (depending on the history of the resolved state) and a [stochastic noise](@entry_id:204235) term .

In many physical systems, the unresolved processes are much faster than the resolved ones. Under this assumption, the memory effects are short-lived, and the equation simplifies to a **Stochastic Differential Equation (SDE)**. For a simple bilinear system where a resolved variable $x$ interacts with a fast, unresolved variable $y$, the resulting SDE for $x$ might take the form:

$$
dx = (-\alpha x) dt + \sqrt{2D(x)} \circ dW_t
$$

Here, the unresolved variability manifests as a **[multiplicative noise](@entry_id:261463)** term, where the strength of the random forcing, $D(x)$, depends on the resolved state $x$. The diffusion coefficient $D(x)$ is given by the time integral of the autocorrelation function of the noise—a result analogous to the Green-Kubo relations. For the bilinear system where the noise arises from the coupling term $\beta x y$, the diffusion coefficient can be shown to be $D(x) = \frac{\beta^2 \sigma_y^2}{\lambda} x^2$, where $\sigma_y^2$ is the variance and $1/\lambda$ is the [correlation time](@entry_id:176698) of the unresolved process . This provides a clear physical link: the variance and memory time of the subgrid process dictate the form and magnitude of the stochastic forcing on the resolved scales.

#### Uncertainty Quantification

A trustworthy NN parameterization must not only provide a prediction but also an estimate of its own uncertainty. This uncertainty can be decomposed into two types :

1.  **Aleatoric Uncertainty**: This is the inherent, irreducible randomness or noise in the data-generating process. Even with a perfect model and infinite data, if the subgrid tendency $y$ is intrinsically stochastic for a given resolved state $\mathbf{x}$, this uncertainty would remain.

2.  **Epistemic Uncertainty**: This is the model's uncertainty due to limited knowledge. It arises from having a finite amount of training data, leading to uncertainty in the optimal model parameters, and from potential inadequacies in the model architecture itself. In principle, epistemic uncertainty can be reduced by collecting more data.

A powerful technique for separating and quantifying both types of uncertainty is to train an ensemble of NNs. Specifically, one can train an ensemble of $M$ models, $\{f_i\}_{i=1}^M$, where each model is trained on a slightly different subset of the data (bootstrapping) and with different random initializations. Furthermore, each network is designed to be **heteroscedastic**, meaning it predicts both the mean $\mu_i(\mathbf{x})$ and the variance $\sigma_i^2(\mathbf{x})$ of the [conditional distribution](@entry_id:138367) $p(y | \mathbf{x})$.

Using the law of total variance, the total predictive uncertainty can be decomposed. The ensemble statistics provide estimates for each component:

*   **Aleatoric Uncertainty** is estimated by the average of the predicted variances:
    $\text{Aleatoric} \approx \frac{1}{M} \sum_{i=1}^M \sigma_i^2(\mathbf{x})$

*   **Epistemic Uncertainty** is estimated by the variance of the predicted means across the ensemble:
    $\text{Epistemic} \approx \operatorname{Var}_i(\mu_i(\mathbf{x})) = \frac{1}{M}\sum_{i=1}^M \mu_i^2(\mathbf{x}) - \left(\frac{1}{M}\sum_{i=1}^M \mu_i(\mathbf{x})\right)^2$

This decomposition is practically useful. For out-of-distribution (OOD) inputs, epistemic uncertainty tends to increase significantly as the ensemble members extrapolate in divergent ways, providing a valuable flag that the model is operating outside its comfort zone. Aleatoric uncertainty, in contrast, is learned from the noise levels in the training data and may not reliably increase for OOD inputs . Other methods, such as **[quantile regression](@entry_id:169107)**, can also be used to characterize the aleatoric uncertainty by directly modeling the [conditional distribution](@entry_id:138367) of the output without requiring an ensemble.