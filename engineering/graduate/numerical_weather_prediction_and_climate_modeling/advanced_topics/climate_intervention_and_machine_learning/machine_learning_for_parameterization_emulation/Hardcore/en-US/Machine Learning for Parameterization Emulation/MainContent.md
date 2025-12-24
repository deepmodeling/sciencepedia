## Introduction
In the vast and complex world of [numerical weather prediction](@entry_id:191656) and climate modeling, subgrid-scale parameterizations represent a fundamental compromise. These schemes approximate the collective effects of crucial physical processes like clouds, radiation, and turbulence that are too small or intricate to be explicitly resolved, but they are often the most computationally expensive part of a simulation. Machine learning (ML) has emerged as a revolutionary approach to this challenge, offering the potential to create data-driven "emulators" that can replicate these complex processes at a fraction of the computational cost. However, replacing a physics-based scheme with a [black-box model](@entry_id:637279) introduces significant risks, from numerical instability to unphysical climate drift. The central question this article addresses is: how can we build ML emulators that are not only fast but also robust, physically consistent, and scientifically sound?

This article provides a comprehensive guide to the theory and practice of machine learning for [parameterization emulation](@entry_id:1129324). The journey begins in the **Principles and Mechanisms** chapter, where we will delve into the theoretical foundation of the closure problem, explore the critical design principles for ensuring causal closure and enforcing physical conservation laws, and confront the challenges of online coupling and numerical stability. Next, the **Applications and Interdisciplinary Connections** chapter will ground these concepts in practice, showcasing how emulators are successfully applied to core atmospheric processes like radiation and turbulence, and demonstrating how these methods bridge to other scientific fields. Finally, the **Hands-On Practices** section offers practical exercises to translate theory into tangible skills, guiding the reader through the validation and implementation of these powerful tools. Together, these sections will equip you with the knowledge to develop and deploy trustworthy ML emulators in [scientific computing](@entry_id:143987).

## Principles and Mechanisms

### The Closure Problem and the Role of Parameterization

The governing equations of atmospheric and oceanic motion—the [primitive equations](@entry_id:1130162)—are a set of nonlinear partial differential equations (PDEs) that describe the conservation of mass, momentum, and energy for a fluid on a rotating sphere. In their continuous form, these equations encompass a vast range of spatial and temporal scales, from planetary-scale waves down to microscopic turbulent eddies. A complete numerical solution that resolves all of these scales, known as Direct Numerical Simulation (DNS), is computationally intractable for realistic geophysical flows. Consequently, numerical weather and climate models must operate on a discretized grid with a finite resolution, for example, with a horizontal grid spacing $\Delta$.

This necessity of finite resolution introduces a fundamental challenge known as the **closure problem**. To formalize this, we can introduce a coarse-graining or filtering operator, denoted $\mathcal{G}_\Delta$, which averages a field over a grid cell of size $\Delta$. Let us denote the resolved (or filtered) component of a field $\phi$ as $\overline{\phi} = \mathcal{G}_\Delta(\phi)$. This operator is linear and, for simplicity, is assumed to commute with spatial and temporal derivatives.

Consider a generic conservation law for a quantity $\phi$, which is nonlinear in the state variables, such as the advection of potential temperature $\theta$ by the velocity field $\mathbf{u}$:
$$
\frac{\partial \theta}{\partial t} + \nabla \cdot (\mathbf{u} \theta) = S
$$
where $S$ represents source and sink terms. Applying the filter operator $\mathcal{G}_\Delta$ to this equation yields:
$$
\frac{\partial \overline{\theta}}{\partial t} + \nabla \cdot \overline{(\mathbf{u} \theta)} = \overline{S}
$$
The equation now describes the evolution of the resolved potential temperature, $\overline{\theta}$. However, a problem immediately arises in the [flux divergence](@entry_id:1125154) term. Because the governing equations are nonlinear, the filter operator does not commute with products of variables. In general, the filtered product is not equal to the product of the filtered variables:
$$
\overline{\mathbf{u} \theta} \neq \overline{\mathbf{u}} \overline{\theta}
$$
To make this explicit, we can decompose any field into its resolved part and a subgrid part, e.g., $\mathbf{u} = \overline{\mathbf{u}} + \mathbf{u}'$. The filtered flux term then contains correlations involving these unresolved subgrid-scale fluctuations:
$$
\overline{\mathbf{u} \theta} = \overline{(\overline{\mathbf{u}} + \mathbf{u}')(\overline{\theta} + \theta')} = \overline{\mathbf{u}}\overline{\theta} + \overline{\overline{\mathbf{u}}\theta'} + \overline{\mathbf{u}'\overline{\theta}} + \overline{\mathbf{u}'\theta'}
$$
The equation for the resolved field $\overline{\theta}$ becomes:
$$
\frac{\partial \overline{\theta}}{\partial t} + \nabla \cdot (\overline{\mathbf{u}} \overline{\theta}) = \overline{S} - \nabla \cdot (\overline{\mathbf{u} \theta} - \overline{\mathbf{u}} \overline{\theta})
$$
The final term on the right-hand side represents the divergence of the **subgrid-scale (SGS) flux**, $\boldsymbol{\tau}_\theta = \overline{\mathbf{u} \theta} - \overline{\mathbf{u}} \overline{\theta}$. This term quantifies the net effect of unresolved motions on the evolution of the resolved state. Because it depends on unknown subgrid quantities (like $\mathbf{u}'$ and $\theta'$), the system of equations for the resolved variables ($\overline{\mathbf{u}}$, $\overline{\theta}$, etc.) is not closed; there are more unknowns than equations.

**Subgrid parameterization** is the procedure of closing this system by positing a functional relationship between the unknown subgrid tendencies and the known resolved state variables $\mathbf{X} = \{\overline{\mathbf{u}}, \overline{\theta}, \dots\}$. A parameterization, $\mathcal{P}$, provides a model for the subgrid tendency: $\mathcal{P}(\mathbf{X}) \approx - \nabla \cdot \boldsymbol{\tau}_\theta$. These parameterizations represent the collective effects of crucial but unresolved physical processes like cloud formation, [moist convection](@entry_id:1128092), radiation, and turbulence.

**Machine learning (ML) emulation** is a modern approach to this problem . Instead of deriving a parameterization from physical theory, one learns it from data. High-resolution simulations or observational data can be used to compute both the resolved state $\mathbf{X}$ and the "true" subgrid tendencies $\mathbf{T}$ that the parameterization should represent. An ML model, $\widehat{\mathcal{F}}_\phi$, is then trained to learn the mapping from inputs to outputs, $\widehat{\mathcal{F}}_\phi: \mathbf{X} \mapsto \mathbf{T}$. This is typically framed as a [supervised learning](@entry_id:161081) problem where the model parameters $\phi$ are optimized to minimize a loss function, such as the [mean squared error](@entry_id:276542) between the predicted and true tendencies.

### Designing Physically Consistent Emulators

Building a successful emulator requires more than just predictive accuracy on a test dataset. For stable and meaningful integration within a climate model, the emulator must be designed to respect the fundamental physical and causal principles of the system it represents.

#### Causal Closure: Selecting Emulator Inputs

The first step in designing an emulator is to determine its input features. A critical principle here is **causal closure**: the inputs must contain all the information upon which the true physical tendency depends at a given moment in time. This ensures the learned mapping is well-posed and Markovian with respect to its inputs, meaning the predicted tendency depends only on the current state provided, not on its history .

To achieve this, it is essential to distinguish between two types of variables in a climate model:
- **Prognostic variables** are those that are time-integrated by the model's dynamical core. They satisfy their own prognostic differential equations (e.g., $\partial_t \mathbf{x} = \dots$) and collectively define the model's state $\mathbf{x}$. Examples include velocity components, potential temperature, and mixing ratios of various water species ($q_v$, $q_c$).
- **Diagnostic variables** are quantities that are calculated algebraically from the prognostic state at a given instant. Examples include pressure (from density and temperature via the [ideal gas law](@entry_id:146757)), cloud fraction, or [static stability](@entry_id:1132318).

The true physical tendencies, $\mathcal{P}_{\mathrm{phys}}$, are a function of the full prognostic state $\mathbf{x}$, its spatial gradients $\nabla \mathbf{x}$, and any external forcings $\mathbf{b}$ (like solar radiation). Therefore, to ensure causal closure, the emulator must be provided with, at a minimum, the complete set of prognostic variables $\mathbf{x}$ and relevant forcings $\mathbf{b}$. While providing diagnostic variables as inputs might be helpful as a form of [feature engineering](@entry_id:174925) to simplify the learning task, it is not strictly necessary for information completeness, as a sufficiently complex model could learn to compute them internally. Omitting a prognostic variable that influences the physics (e.g., omitting wind shear when emulating turbulence) would violate causal closure and lead to an ill-posed learning problem. Furthermore, if the original [parameterization scheme](@entry_id:1129328) has its own internal memory or prognostic states (e.g., a prognostic turbulence kinetic energy), these "hidden" states must also be included as inputs to the emulator to maintain the Markov property.

#### Enforcing Physical Conservation Laws

Physical parameterizations, no matter how complex, must adhere to fundamental conservation laws. An emulator that violates these laws can lead to unrealistic model drift, such as a continuous, unphysical gain or loss of total energy or water in the simulated climate. Therefore, a crucial aspect of emulator design is the enforcement of these conservation principles .

For a single atmospheric column in a model, the key conservation laws are:
1.  **Conservation of Mass**: The sum of all mass mixing ratios (dry air, water vapor, liquid, ice) within any given model layer must equal one at all times. This implies that the sum of their tendencies must be zero. If an emulator predicts the tendencies of water species $(\dot{q}_{v,k}, \dot{q}_{l,k}, \dot{q}_{i,k})$ for a layer $k$, the dry air tendency must be diagnosed as $\dot{q}_{\text{dry},k} = -(\dot{q}_{v,k} + \dot{q}_{l,k} + \dot{q}_{i,k})$ to conserve mass.

2.  **Conservation of Total Water**: The rate of change of the total water mass in the column (summed over all layers and phases) must equal the net flux of water across the column boundaries. This balance connects the integrated water tendencies to surface fluxes (evaporation $F_E$, precipitation $F_p$) and top-of-atmosphere fluxes. For a column with layer masses $m_k$, the constraint is:
    $$
    \sum_{k=1}^{N} m_k (\dot{q}_{v,k} + \dot{q}_{l,k} + \dot{q}_{i,k}) = \frac{F_E}{L_v} - F_p - F_{\text{top,w}}
    $$
    where $L_v$ is the [latent heat of vaporization](@entry_id:142174) and $F_{\text{top,w}}$ is any water flux at the top of the atmosphere.

3.  **Conservation of Energy**: According to the First Law of Thermodynamics, the rate of change of the total energy in the column must equal the net flow of energy across its boundaries. Using moist enthalpy, this budget links the tendencies of temperature and water phases to radiative fluxes ($F_R$), surface sensible and latent heat fluxes ($F_H, F_E$), and the energy removed by precipitation. The constraint takes the form:
    $$
    \sum_{k=1}^{N} m_k (c_p \dot{T}_k + L_v \dot{q}_{v,k} - L_f \dot{q}_{i,k}) = (F_R^{\text{surf}} - F_R^{\text{TOA}}) + F_H + F_E - h_p F_p - F_{\text{top,E}}
    $$
    where $c_p$ is the specific heat, $L_f$ is the [latent heat of fusion](@entry_id:144988), and $h_p F_p$ and $F_{\text{top,E}}$ are energy fluxes associated with precipitation and escaping at the model top, respectively.

An emulator's outputs for all tendency and flux terms must collectively satisfy these algebraic budget equations at every time step.

#### Architectural and Methodological Approaches to Conservation

Ensuring that an emulator respects conservation laws can be approached in several ways, primarily categorized as "hard" or "soft" constraints.

A powerful **hard constraint** is to design the emulator's architecture such that it is structurally conservative. Instead of directly predicting local tendencies like $\dot{T}(z)$ and $\dot{q}(z)$, which can easily violate integrated budgets, the emulator can be trained to predict the vertical fluxes of energy and water, such as the subgrid flux of moist static energy $F_m(z)$ and total water $F_q(z)$. The tendencies are then computed in a separate, non-learnable step as the divergence of these predicted fluxes :
$$
\rho \dot{m}(z) = -\frac{\partial F_m}{\partial z}, \quad \rho \dot{q}(z) = -\frac{\partial F_q}{\partial z}
$$
where $\dot{m}$ is the tendency of moist static energy. If the emulator is constrained to predict zero fluxes at the top and bottom boundaries of a closed domain, then the column-integrated tendencies will be exactly zero, guaranteeing conservation by construction. This method mirrors how conservation laws are discretized in many dynamical cores.

In contrast, **soft constraints** involve guiding the training process toward a conservative solution without strictly forcing it. This is achieved by using a **composite loss function** that penalizes violations of the conservation laws . The total loss, $L$, is a weighted sum of an accuracy term (e.g., Mean Squared Error, MSE) and one or more physics-based penalty terms:
$$
L(\theta) = L_{\text{MSE}} + \lambda_{\text{en}} L_{\text{en-resid}} + \lambda_{\text{wat}} L_{\text{wat-resid}}
$$
Here, $L_{\text{en-resid}}$ and $L_{\text{wat-resid}}$ are the squared residuals of the energy and water budget equations, respectively, and $\lambda_{\text{en}}$ and $\lambda_{\text{wat}}$ are weights that control the trade-off between pointwise accuracy and physical consistency. A key challenge is choosing these weights. A principled approach requires ensuring all terms are dimensionally consistent (e.g., by non-dimensionalizing the residuals with characteristic physical scales) and using a strategy to balance their contributions. Valid strategies include:
-   Dynamically adapting the weights during training to equalize the gradient magnitudes of each loss component.
-   Using an **Augmented Lagrangian** method, which treats the problem as a constrained optimization and systematically updates Lagrange multipliers to drive the conservation residuals to zero.
-   Interpreting the composite loss from a probabilistic perspective as a [negative log-likelihood](@entry_id:637801), where the weights are inverse variances that can be learned as part of the optimization.

### Coupling, Stability, and Online Performance

Once an emulator is trained, it must be integrated into the host climate model. This coupling process introduces new challenges related to [numerical stability](@entry_id:146550) and the complex feedback between the data-driven component and the physics-based [dynamical core](@entry_id:1124042).

#### Hybrid Modeling: Offline Training vs. Online Integration

The combination of a traditional PDE-based model with an ML component is known as a **hybrid ML-PDE model**. The workflow for developing and using such a model involves two distinct phases :

1.  **Offline Training and Evaluation**: This is the standard [supervised learning](@entry_id:161081) phase. A static dataset of input states and output tendencies is generated from the original, high-cost parameterization. The emulator is trained to minimize a loss function on this dataset. Offline evaluation measures the emulator's performance (e.g., MSE, $R^2$) on a held-out portion of this static dataset. In this phase, there is no feedback; the emulator's predictions do not influence the input states it is shown.

2.  **Online Integration and Evaluation**: In this phase, the trained emulator replaces the original parameterization inside the prognostic time-stepping loop of the climate model. A common technique for this coupling is **operator splitting**, where the update to the state vector $x$ over a time step $\Delta t$ is performed in sequential steps: one for the resolved dynamics ($F$) and one for the [subgrid physics](@entry_id:755602), which is now provided by the emulator ($\hat{P}$):
    $$
    x_{k+1} = x_k + \Delta t [F(x_k) + \hat{P}(x_k)]
    $$
    In this closed-loop configuration, the emulator's output directly alters the model state, which in turn becomes the input for the emulator at the next time step. Online evaluation assesses the performance of the full hybrid model over long simulations, focusing on metrics like numerical stability, climate drift, and the realism of simulated phenomena.

#### The Challenge of Numerical Stability: Stiffness

A critical problem that arises during online integration is **numerical stiffness**. A [system of differential equations](@entry_id:262944) is stiff if its solution involves processes that occur on widely different time scales . This is ubiquitous in climate models, where slow dynamical processes (e.g., large-scale advection, with timescales of hours to days) coexist with fast subgrid processes (e.g., [cloud microphysics](@entry_id:1122517) or convective adjustment, with timescales of seconds to minutes).

The [numerical stability](@entry_id:146550) of explicit time-stepping schemes, like the forward Euler method often used for emulator updates, is constrained by the fastest timescale in the system. For a simple relaxation process with timescale $\tau_m$, the [stable time step](@entry_id:755325) $\Delta t$ for a forward Euler update must satisfy $\Delta t \leq 2\tau_m$. However, the global time step of a climate model is chosen to satisfy the stability condition (e.g., the CFL condition) for the *slow* resolved dynamics, meaning $\Delta t$ is typically much larger than the fast physical timescales ($\Delta t \gg \tau_m$).

When an explicit ML emulator for a fast process is coupled with this large $\Delta t$, the stability condition is violated. The numerical update will overshoot the equilibrium state, leading to rapidly growing oscillations that can destroy the simulation. This demonstrates that even a perfectly accurate emulator (one with zero offline error) can be catastrophically unstable when coupled online if the issue of stiffness is not addressed, for example, by using [implicit time-stepping](@entry_id:172036) or sub-stepping the fast process with a smaller $\Delta t$.

#### The Problem of Feedback and Online Evaluation

The closed-loop nature of online integration gives rise to complex feedbacks that are entirely absent in offline evaluation. Low offline error is a necessary but not [sufficient condition](@entry_id:276242) for good online performance .

The core issue is that small, [systematic errors](@entry_id:755765) in the emulator can accumulate over time. The emulator produces a slightly incorrect tendency, which leads to a slightly incorrect model state. This new, slightly incorrect state is then fed back into the emulator as input, which may produce another error, potentially leading to a slow drift of the entire model climate away from the true solution, or even to a rapid instability.

This can be formalized by considering the effect of a small, constant bias $b$ in an emulator, $\hat{P} = P + b$, on the equilibrium state of a simple system. If the original system has a stable fixed point $x^\star$ where the total tendency is zero, $F(x^\star) + P(x^\star) = 0$, the new fixed point with the biased emulator will be shifted by an amount $\delta x$. A first-order analysis shows that this shift is approximately:
$$
\delta x \approx -[D(F+P)(x^\star)]^{-1} b
$$
where $D(F+P)(x^\star)$ is the Jacobian of the system dynamics at the fixed point. The term $[D(F+P)(x^\star)]^{-1}$ represents the sensitivity of the climate model's equilibrium state to a persistent forcing. For [chaotic systems](@entry_id:139317) like the atmosphere, this sensitivity can be very large, meaning even a tiny local bias $b$ (which might be undetectable with offline metrics) can be amplified into a large, physically significant shift $\delta x$ in the model's mean climate.

This amplification of error through feedback makes **online testing indispensable**. It is the only way to assess the true stability of the coupled system, diagnose climate drift, and verify that the hybrid model produces a scientifically credible simulation.

### Generalization and the Challenge of a Changing Climate

The ultimate goal for many [climate model emulators](@entry_id:1122468) is to accelerate projections of future climate change. This poses a profound challenge for machine learning: the model is trained on data from a historical climate but deployed in a future, unseen climate. This is a problem of **[distribution shift](@entry_id:638064)**.

#### Distribution Shift: The Core Challenge

In [statistical learning theory](@entry_id:274291), we distinguish between different types of risk, or expected loss . The **[empirical risk](@entry_id:633993)**, $\hat{R}_s(f)$, is the average loss of an emulator $f$ computed on the finite training dataset, drawn from a source distribution $p_s(x,y)$ (e.g., the historical climate). The **[expected risk](@entry_id:634700)**, $R_s(f)$, is the true average loss over the entire source distribution. The standard [generalization error](@entry_id:637724) measures the gap between these two, $R_s(f) - \hat{R}_s(f)$.

However, in deployment, the emulator will encounter data from a [target distribution](@entry_id:634522), $p_t(x,y)$ (e.g., a future climate), which is different from the source, $p_t \neq p_s$. The true performance is the **deployment [expected risk](@entry_id:634700)**, $R_t(f)$. The most relevant measure of generalization for [climate projection](@entry_id:1122479) is the gap between the performance we can measure ([empirical risk](@entry_id:633993) on historical data) and the performance we care about ([expected risk](@entry_id:634700) on future data): $R_t(f) - \hat{R}_s(f)$. This gap arises from both standard sampling error and the fundamental mismatch between the training and deployment distributions.

#### Types of Distribution Shift: Covariate Shift vs. Concept Drift

The problem of [distribution shift](@entry_id:638064) in climate emulation can be broken down into two main categories, based on how the [joint distribution](@entry_id:204390) $P(X,Y) = P(Y|X)P(X)$ changes between the training (source, $s$) and deployment (target, $t$) domains .

1.  **Covariate Shift**: This occurs when the distribution of input states changes, but the physical relationship between states and tendencies remains the same. Mathematically, $P_t(X) \neq P_s(X)$, but the conditional probability is invariant, $P_t(Y|X) = P_s(Y|X)$. In a climate context, this means that while the fundamental physics has not changed, a warmer world might exhibit different weather patterns more or less frequently. The emulator may be forced to extrapolate to unseen combinations of input variables, potentially leading to large errors. Under the assumption of covariate shift, the deployment risk can be formally related to the source risk through [importance weighting](@entry_id:636441): $R_t(f) = \mathbb{E}_{(x,y)\sim p_s}[w(x)\ell(f(x),y)]$, where $w(x) = p_t(x)/p_s(x)$ is the density ratio.

2.  **Concept Drift**: This is a more severe form of shift where the underlying physical "concept" itself changes. The conditional relationship between inputs and outputs is altered: $P_t(Y|X) \neq P_s(Y|X)$. This could happen, for example, if changes in atmospheric composition (like aerosols) alter cloud microphysical processes in a way that is not captured by the emulator's input variables. In this case, the mapping learned by the emulator from the historical climate is no longer physically correct for the future climate, leading to fundamentally flawed predictions.

Distinguishing and preparing for these types of [distribution shift](@entry_id:638064) is a critical frontier of research, essential for building trustworthy ML emulators for long-term [climate projection](@entry_id:1122479).