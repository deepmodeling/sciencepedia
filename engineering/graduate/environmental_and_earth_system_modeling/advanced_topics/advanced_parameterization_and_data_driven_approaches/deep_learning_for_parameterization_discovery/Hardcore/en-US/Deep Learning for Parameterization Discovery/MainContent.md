## Introduction
The predictive power of complex physical simulations, such as Earth System Models (ESMs), is fundamentally limited by their inability to resolve all relevant physical processes. Processes occurring at scales smaller than the model's grid—from turbulent eddies to cloud formation—must be represented through simplified formulas known as parameterizations. For decades, these parameterizations have been a primary source of [model uncertainty](@entry_id:265539) and bias. This article introduces a paradigm shift in addressing this challenge: using deep learning to discover these subgrid-scale [closures](@entry_id:747387) directly from high-fidelity data. Instead of relying on hand-crafted, often overly simplistic equations, we can now leverage the power of neural networks to learn the complex, nonlinear relationships governing unresolved physics, a process known as parameterization discovery.

This article provides a comprehensive guide to this data-driven approach. First, in "Principles and Mechanisms," we will dissect the parameterization problem, distinguishing it from numerical error, and detail the methodologies for building robust, [physics-informed machine learning](@entry_id:137926) models. We will explore how to infuse deep learning with physical knowledge through hybrid modeling, architectural design, and targeted [loss functions](@entry_id:634569). Next, "Applications and Interdisciplinary Connections" will showcase how these techniques are being used to tackle long-standing problems in atmospheric science, oceanography, and cryospheric modeling, and how the same principles are being applied in fields like systems biology and engineering. Finally, "Hands-On Practices" will translate theory into action, providing practical exercises for developing and validating these learned parameterizations. By the end, you will understand the workflow for creating scientifically sound, stable, and accurate data-driven models that can be trusted for scientific discovery.

## Principles and Mechanisms

The replacement of traditional, often empirically derived, parameterizations with those discovered from data using deep learning represents a paradigm shift in Earth system modeling. This chapter elucidates the fundamental principles and mechanisms underpinning this approach. We will begin by precisely defining the parameterization problem itself, distinguishing it from numerical artifacts. Subsequently, we will explore the core methodologies for integrating deep learning with physics-based models, focusing on the critical role of physical constraints. Finally, we will outline the complete workflow, from selecting appropriate training data and model architectures to quantifying uncertainty and performing rigorous, multi-stage validation.

### The Parameterization Problem in Earth System Models

Earth System Models (ESMs) are built upon fundamental conservation laws of physics—conservation of mass, momentum, and energy. These laws are expressed as continuous partial differential equations (PDEs). For instance, the conservation of a scalar tracer concentration, $q(\mathbf{x}, t)$, can be written in a general form:
$$
\partial_t q + \nabla \cdot (\mathbf{u}\, q) = \nabla \cdot \left(K\, \nabla q\right) + S
$$
where $\mathbf{u}$ is the velocity field, $K$ is a diffusivity, and $S$ represents [sources and sinks](@entry_id:263105).

Because digital computers can only operate on discrete data, ESMs solve these equations on a finite grid with a characteristic spacing, $\Delta$. This act of discretization means the model cannot explicitly resolve physical processes that occur on scales smaller than $\Delta$. Instead, the model solves for variables that represent an average or filtered state over a grid cell. Let us denote this filtering operation by an overbar, e.g., $\bar{q}$. When we apply this filter to the governing equations, a fundamental problem arises due to nonlinear terms. For example, the filtered advection term becomes $\overline{\mathbf{u} q}$. If we decompose the variables into their resolved (filtered) and unresolved (subgrid-scale, SGS) components, so that $q = \bar{q} + q'$ and $\mathbf{u} = \bar{\mathbf{u}} + \mathbf{u}'$, the term expands:
$$
\overline{\mathbf{u} q} = \overline{(\bar{\mathbf{u}} + \mathbf{u}')(\bar{q} + q')} = \bar{\mathbf{u}} \bar{q} + \overline{\bar{\mathbf{u}}q'} + \overline{\mathbf{u}'\bar{q}} + \overline{\mathbf{u}'q'}
$$
The governing equation for the resolved field $\bar{q}$ then takes the form:
$$
\partial_t \bar{q} + \nabla \cdot (\bar{\mathbf{u}} \bar{q}) = \dots - \nabla \cdot (\overline{\mathbf{u}'q'} + \dots)
$$
The terms involving correlations of subgrid-scale fluctuations, such as the subgrid flux $\overline{\mathbf{u}'q'}$, are **unclosed**. They represent the influence of real, unresolved physical processes (like small turbulent eddies or convective plumes) on the resolved scales, but they cannot be computed directly from the resolved variables $\bar{q}$ and $\bar{\mathbf{u}}$.

A **parameterization** is a model, or functional relationship, designed to represent these unclosed terms as a function of the available resolved-scale variables. It is a physical closure that aims to capture the missing physics. This is fundamentally distinct from **[numerical discretization](@entry_id:752782) error**, which is the mathematical error introduced when we approximate the continuous [differential operators](@entry_id:275037) (like $\partial_t$ or $\nabla$) with discrete algorithms (like [finite differences](@entry_id:167874)). A parameterization represents unresolved physics; discretization error is an artifact of the numerical solution method . The goal of deep learning for parameterization discovery is to learn this functional relationship directly from high-resolution data.

### Methodological Approaches to Closure Modeling

Historically, developing parameterizations has involved proposing a simplified physical model and then tuning its free parameters. Machine learning opens the door to a more data-driven approach.

#### Parameter Calibration vs. Parameterization Discovery

It is crucial to distinguish two paradigms :
1.  **Parameter Calibration**: In this traditional approach, the physicist first posits a fixed structural form for the closure. For example, the subgrid flux $\mathbf{F}_{\text{sub}}$ might be modeled using an eddy-diffusivity hypothesis, $\mathbf{F}_{\text{sub}} = - K \nabla q$. The functional form of the eddy diffusivity $K$ might then be assumed to be a power law of some stability measure $N$, such as $K(N) = \alpha N^\beta$. The task is then reduced to **calibrating** the coefficients $\alpha$ and $\beta$ using data. The primary limitation of this approach is **[structural error](@entry_id:1132551)**: if the true physical relationship is not a power law, the model will be inaccurate, especially when extrapolating to regimes beyond the training data.

2.  **Parameterization Discovery**: This is the deep learning approach. Here, we do not assume a rigid functional form. Instead, we use a flexible function approximator, such as a neural network, to learn the entire mapping from resolved [state variables](@entry_id:138790) to the subgrid tendency, i.e., $\mathbf{F}_{\text{sub}} = \mathbf{F}_\phi(q, \nabla q, N)$, where $\phi$ represents the network's trainable parameters. This approach has the potential to discover more accurate and complex physical relationships than simple prescribed forms. However, its flexibility comes at the cost of requiring larger datasets and a higher risk of learning unphysical relationships or failing to generalize if not properly constrained.

The success of parameterization discovery, especially its ability to extrapolate plausibly, hinges not on its raw fitting power but on the extent to which it is infused with physical knowledge.

### The Central Role of Physics in Data-Driven Discovery

A naive application of machine learning to a physics problem is unlikely to succeed. A neural network trained purely to minimize mean squared error on a finite dataset has no inherent knowledge of fundamental principles like conservation of energy or the symmetries of the physical system. A robust data-driven parameterization must therefore be built upon a foundation of physics. This can be achieved through several complementary strategies.

#### Hybrid Modeling: Retaining Known Physics

The most effective strategy for building scientifically sound models is **hybrid modeling**, where a machine learning component is coupled with a traditional physics-based solver . The governing equations can be partitioned into a resolved dynamics operator, $\mathcal{F}(\mathbf{q})$, and the unresolved tendencies, $\mathbf{s}_{\text{sgs}}$:
$$
\partial_t \mathbf{q} = \mathcal{F}(\mathbf{q}) + \mathbf{s}_{\text{sgs}}
$$
The operator $\mathcal{F}(\mathbf{q})$ encapsulates the parts of the physics that are well-understood and can be expressed in [closed form](@entry_id:271343), such as large-scale advection or pressure gradient forces. Crucially, these operators are constructed to directly enforce fundamental conservation laws. The term $\mathbf{s}_{\text{sgs}}$ represents the complex, uncertain physics that is the target for parameterization.

The optimal hybrid modeling strategy is to **retain the physics-based operator $\mathcal{F}(\mathbf{q})$ and use the neural network solely to replace or augment the unresolved tendency term $\mathbf{s}_{\text{sgs}}$**. The hybrid model equation becomes:
$$
\partial_t \mathbf{q} = \mathcal{F}(\mathbf{q}) + \hat{\mathbf{s}}(\mathbf{q}; \boldsymbol{\theta})
$$
where $\hat{\mathbf{s}}(\mathbf{q}; \boldsymbol{\theta})$ is the learned parameterization. This approach leverages the best of both worlds: the physics-based component provides a robust backbone that guarantees the enforcement of fundamental invariants and enhances [numerical stability](@entry_id:146550), while the machine learning component provides a flexible and powerful way to represent complex, poorly understood processes. Attempting to learn the entire operator, including the known physics in $\mathcal{F}(\mathbf{q})$, is inefficient and dangerous, as it risks violating fundamental laws that the data may not be sufficient to fully specify.

#### Hard Constraints: Enforcing Physics by Architectural Design

Even when learning only the closure term, it is often possible and desirable to enforce physical properties directly through the architecture of the neural network. These are known as **hard constraints** because they hold true for any value of the network's parameters.

A prime example is ensuring **local mass or energy conservation**. In a finite-volume numerical scheme, conservation is guaranteed if the flux across any interior face between two cells is single-valued, contributing equally and oppositely to the tendencies of the two cells . This can be enforced by designing the neural network to predict a single, unique flux for each face based on the states of the two adjacent cells. An effective way to achieve this is to enforce an **antisymmetric** structure. For instance, if a network encoder $h_{\boldsymbol{\theta}}$ processes features from the left ($\mathbf{z}_L$) and right ($\mathbf{z}_R$) sides of a face, a [scalar flux](@entry_id:1131249) defined as $\widehat{\phi}_f = h_{\boldsymbol{\theta}}(\mathbf{z}_L) - h_{\boldsymbol{\theta}}(\mathbf{z}_R)$ is guaranteed to be antisymmetric. Swapping the left and right perspectives reverses the sign of the scalar flux, but when combined with the reversed face normal, it yields the exact same physical flux vector, thus guaranteeing local conservation by construction. Another approach is to have the network predict a [scalar potential](@entry_id:276177) at cell centers, with the flux being proportional to the difference in potential across the face, which is also inherently antisymmetric.

Another powerful class of hard constraints involves **geometric [equivariance](@entry_id:636671)** . The laws of physics should not depend on the coordinate system in which they are expressed. A learned parameterization should respect the same symmetries as the physical system it represents.
*   On a uniform Cartesian grid, the physics are typically invariant to translation. A **Convolutional Neural Network (CNN)**, with its shared-weight kernels, has a built-in **[translation equivariance](@entry_id:634519)**, making it a natural choice for such grids.
*   On the sphere, the relevant symmetry is rotation, described by the group $\mathrm{SO}(3)$. A standard CNN applied to a latitude-longitude projection of the sphere would produce coordinate-dependent artifacts (e.g., treating the poles differently from the equator). To respect this symmetry, specialized architectures like **spherical CNNs** are required.
*   On unstructured meshes, such as icosahedral grids, there may be no global symmetries, but the physics should be independent of how the nodes are arbitrarily numbered. **Graph Neural Networks (GNNs)**, which operate on local neighborhoods defined by mesh connectivity and use permutation-invariant aggregation functions, are designed to respect this very property.

Matching the inductive bias of the architecture to the physical symmetries of the problem is a critical design choice for building robust and generalizable models .

#### Soft Constraints: Enforcing Physics via Regularization

When hard constraints are difficult to implement, an alternative is to use **soft constraints** by adding a physics-based penalty term to the training loss function . This encourages the network to learn solutions that respect the desired physical properties, although it does not strictly guarantee them.

For example, a regularizer $R(\boldsymbol{\theta})$ can be constructed to penalize two types of violations:
1.  **PDE Residual**: The governing PDE itself can be used as a constraint. We can evaluate the full PDE, substituting the network's output $\boldsymbol{q}_{\boldsymbol{\theta}}$, and compute a residual. To avoid differentiating the network output, which can be numerically unstable, this is typically done in a **[weak form](@entry_id:137295)**. The PDE residual is multiplied by a set of smooth test functions and integrated over the domain. A non-zero result for any [test function](@entry_id:178872) indicates a violation of the PDE, which is then added to the loss.
2.  **Thermodynamic Constraints**: Many physical processes must obey [thermodynamic laws](@entry_id:202285), such as the [second law of thermodynamics](@entry_id:142732). For instance, subgrid turbulence is expected to be a dissipative process, meaning it should remove energy from the resolved scales or transfer it downscale. This translates to mathematical constraints, such as requiring the globally averaged production of tracer variance by the subgrid flux to be non-positive, i.e., $\int_{\Omega} \boldsymbol{q}_{\boldsymbol{\theta}} \cdot \nabla \bar{T} \, d\boldsymbol{x} \leq 0$. Violations of this inequality (i.e., positive values) can be penalized in the loss function.

A combined regularizer might look like:
$$
R(\boldsymbol{\theta}) = \frac{1}{N} \sum_{n=1}^{N} \left[ \sum_{m=1}^{M} (\text{weak residual}_m^n)^2 + \alpha \left( \left[ \langle \boldsymbol{q}_{\boldsymbol{\theta}}^n, \nabla \bar{T}^n \rangle \right]_+ \right)^{2} \right]
$$
where the first term penalizes the squared weak PDE residual against $M$ test functions, and the second term, using the positive-part operator $[x]_+ = \max(x, 0)$, penalizes any positive (unphysical) tracer variance production, weighted by a hyperparameter $\alpha$.

### The Data-Driven Discovery Workflow

Developing a robust data-driven parameterization is a systematic process that extends from [data acquisition](@entry_id:273490) to final validation.

#### Sourcing High-Fidelity Training Data

The quality of a learned parameterization is fundamentally limited by the quality of its training data. The goal is to train a model to predict the true subgrid tendency, $\mathbf{s}_{\text{sgs}}$. To generate training pairs of (resolved state, true subgrid tendency), we need access to simulations or observations that resolve the physics we wish to parameterize . The most common data sources have distinct advantages and disadvantages:
*   **Direct Numerical Simulation (DNS)**: Resolves all scales of motion. It is the highest-fidelity source but is computationally feasible only for small domains and idealized physics (e.g., low Reynolds numbers, simple geometries). It often suffers from poor **representativeness** for real-world atmospheric conditions.
*   **Large Eddy Simulation (LES)**: Resolves the large, energy-containing eddies and models only the smallest, most isotropic subgrid scales. LES can be run over larger domains with more realistic physics (e.g., [moist convection](@entry_id:1128092), radiation) than DNS. For many parameterization tasks, such as for clouds and turbulence, LES is considered the **"gold standard"** for generating training data. By explicitly simulating the processes to be parameterized, it can provide direct, low-bias targets for the learning algorithm.
*   **Reanalysis Products**: These are global datasets produced by assimilating observations into a weather forecast model. While they offer global coverage, they do not resolve subgrid scales. Any "tendency" derived from reanalysis is contaminated by the forecast model's own parameterizations and the complex adjustments made by the data assimilation system. They are therefore generally unsuitable for learning the underlying physics of a subgrid process.
*   **Satellite Observations**: These provide vast global coverage but typically measure radiances, not the model's [state variables](@entry_id:138790) directly. Retrieving physical quantities from these measurements is an [ill-posed inverse problem](@entry_id:901223) that introduces its own biases. Furthermore, satellites provide sparse snapshots in time and space, making it impossible to compute the tendencies needed for training.

For these reasons, high-resolution, process-resolving simulations like LES are the most reliable source for generating labels for [supervised learning](@entry_id:161081) of parameterizations.

#### Selecting an Appropriate Architecture

The choice of neural network architecture should be guided by the physical nature of the closure being modeled, a principle known as incorporating **inductive biases** .
*   For **local [closures](@entry_id:747387)**, where the subgrid tendency at a point depends only on the state in its immediate neighborhood (e.g., local turbulent mixing), **CNNs** are a natural fit due to their [local receptive fields](@entry_id:634395) and [translation equivariance](@entry_id:634519).
*   For **non-local closures**, where the tendency at a point depends on the state over a large region or the entire domain (e.g., radiative transfer), architectures with global receptive fields are needed. **Transformers**, with their [self-attention mechanism](@entry_id:638063), can model all-to-all interactions. **Neural Operators**, such as the Fourier Neural Operator (FNO), are explicitly designed to learn mappings between [function spaces](@entry_id:143478) and have a strong bias toward learning global [integral operators](@entry_id:187690), making them highly suitable for non-local physics and offering the benefit of zero-shot generalization across different grid resolutions.
*   For [closures](@entry_id:747387) with **[temporal memory](@entry_id:1132929)**, where the tendency depends on the history of the state (e.g., some microphysical processes), **Recurrent Neural Networks (RNNs)**, which maintain an internal state that evolves over a sequence, are the most natural choice.

#### Quantifying Uncertainty

A deterministic prediction from a neural network provides no information about its confidence. A complete data-driven parameterization should also quantify its uncertainty, which can be decomposed into two types :
1.  **Aleatoric Uncertainty**: This is the inherent, irreducible randomness in the physical process itself. For a given resolved state, there may be a distribution of possible subgrid outcomes due to stochastic turbulence or microphysics. This uncertainty can be captured by training a **heteroscedastic** network that predicts not just a mean tendency $\mu_{\boldsymbol{\theta}}(s)$ but also its variance $\sigma_{\boldsymbol{\theta}}^2(s)$. The network is trained by minimizing the [negative log-likelihood](@entry_id:637801), which encourages it to learn the true, input-dependent variance of the data. This allows for the creation of **stochastic parameterizations** that sample from the predicted distribution $\mathcal{N}(\mu_{\boldsymbol{\theta}}(s), \sigma_{\boldsymbol{\theta}}^2(s))$, re-introducing realistic variability into the model.
2.  **Epistemic Uncertainty**: This is uncertainty due to the model's lack of knowledge, arising from limited or biased training data. It can be estimated using an **ensemble** of models. By training multiple networks on different subsets of the data (e.g., via bootstrapping) or from different random initializations, the spread in their predictions provides a measure of epistemic uncertainty. Where data is plentiful, the ensemble members will agree; in regions far from the training data (out-of-distribution), their predictions will diverge. High epistemic uncertainty is a warning sign that the model is extrapolating and its predictions are unreliable. This information can be used to build safer models that, for instance, revert to a simpler, more robust parameterization when epistemic uncertainty is high.

Using the law of total variance, the total predictive uncertainty can be decomposed into the average of the predicted aleatoric variances and the variance of the ensemble mean predictions (epistemic).

#### The Hierarchy of Validation

Finally, a learned parameterization cannot be considered robust until it has passed a rigorous, multi-stage validation process . Offline accuracy is a necessary but profoundly insufficient condition for success.
1.  **Offline Validation**: This is the standard supervised learning test. The network's predictions for the subgrid tendency are compared against a held-out [test set](@entry_id:637546) of true tendencies from high-resolution data. This tests the model's ability to make accurate instantaneous predictions but provides no information about how it will behave when coupled to a time-evolving dynamical system.
2.  **Partially Coupled Validation**: This is an intermediate step where the parameterization is tested in a simplified but prognostic setting. A common example is a Single Column Model (SCM), where the learned closure for vertical processes is run in a single atmospheric column, with large-scale horizontal forcing prescribed. This test is critical for identifying instabilities and biases that arise from feedback between the closure and the [thermodynamic state](@entry_id:200783), without the complicating factors of a full 3D model.
3.  **Online Validation**: This is the ultimate test. The learned parameterization is fully integrated into the complete Earth System Model, which is then run for long periods (years to centuries). The simulation is assessed for numerical stability (i.e., it doesn't crash), conservation of key quantities over long timescales, and the fidelity of its **emergent statistics**. The model's "climate"—its mean state, variability (e.g., El Niño-Southern Oscillation), and distribution of extremes—must be realistic.

A closure can perform perfectly in offline tests yet cause the online model to become unstable or drift to a completely unphysical climate. Only by successfully passing through this entire hierarchy of validation can a data-driven parameterization be deemed robust and trustworthy for scientific use.