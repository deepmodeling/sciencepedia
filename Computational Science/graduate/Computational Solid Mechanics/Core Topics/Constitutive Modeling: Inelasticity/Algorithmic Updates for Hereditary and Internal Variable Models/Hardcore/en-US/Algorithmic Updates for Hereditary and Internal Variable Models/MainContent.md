## Introduction
In the field of [computational solid mechanics](@entry_id:169583), accurately predicting the behavior of materials whose response depends on their deformation history is a paramount challenge. Materials such as polymers, metals at high temperatures, and biological tissues exhibit hereditary effects like [viscoelasticity](@entry_id:148045) and plasticity, where the current stress is a function of the entire path of past strains. While these behaviors can be described elegantly by [hereditary integrals](@entry_id:186265), their direct numerical implementation is often computationally prohibitive, requiring the storage and processing of extensive historical data at every point in a simulation. This creates a critical knowledge gap between the physical theory and its practical, efficient application in [finite element analysis](@entry_id:138109).

This article addresses this challenge by providing a comprehensive guide to the algorithmic updates for hereditary and [internal variable models](@entry_id:750757). It bridges the gap between theory and computation by focusing on the development of robust, stable, and thermodynamically consistent numerical methods. The reader will gain a deep understanding of how to transform complex, history-dependent [constitutive laws](@entry_id:178936) into a form suitable for modern simulation software.

The article is structured to build knowledge progressively. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, explaining how to convert [hereditary integrals](@entry_id:186265) into local internal variable formulations and detailing the derivation of the discrete update algorithms and the crucial [consistent tangent modulus](@entry_id:168075). Following this, "Applications and Interdisciplinary Connections" demonstrates the practical utility of these methods across various material models, including [linear viscoelasticity](@entry_id:181219), [rate-independent plasticity](@entry_id:754082), and extensions to finite strains and advanced phenomena like fractional relaxation and damage. Finally, "Hands-On Practices" offers concrete problems to solidify the reader's understanding and implementation skills. We begin by exploring the fundamental principles that enable the efficient computation of history-dependent material responses.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms governing the computational treatment of hereditary material models. Building upon the introductory concepts, we will establish the theoretical and algorithmic foundation for transforming history-dependent constitutive laws into a computationally tractable form. Our focus will be on developing robust, accurate, and thermodynamically consistent numerical update procedures for [internal variable models](@entry_id:750757), which are essential for modern [finite element analysis](@entry_id:138109) of materials like viscoelastic polymers and viscoplastic metals.

### From Hereditary Integrals to Internal Variable Models

Many materials exhibit **hereditary** behavior, where the current stress state depends not just on the current strain, but on the entire history of deformation. For a linear, time-invariant, and causal material under small strains, this relationship can be expressed by the **Boltzmann superposition principle**. This principle states that the stress $\boldsymbol{\sigma}(t)$ is a convolution of a material-specific kernel with the history of the [strain rate](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}(t)$. This gives rise to the [hereditary integral](@entry_id:199438) formulation .

If we consider the stress response to strain history, the governing relation is the **relaxation integral**:
$$
\boldsymbol{\sigma}(t) = \int_0^t \mathbf{G}(t-s) : \dot{\boldsymbol{\varepsilon}}(s) \, \mathrm{d}s
$$
Here, $\mathbf{G}(t)$ is the fourth-order **[relaxation modulus](@entry_id:189592) tensor**, which physically represents the stress response at time $t$ to a unit step strain applied at time $s=0$. Conversely, if we consider the strain response to stress history, we have the **creep integral**:
$$
\boldsymbol{\varepsilon}(t) = \int_0^t \mathbf{J}(t-s) : \dot{\boldsymbol{\sigma}}(s) \, \mathrm{d}s
$$
where $\mathbf{J}(t)$ is the **[creep compliance](@entry_id:182488) tensor**, representing the strain response to a unit step stress. These two descriptions are intrinsically linked; for [isotropic materials](@entry_id:170678), their scalar counterparts in the Laplace domain satisfy the relation $s^2 G(s) J(s) = 1$, where $s$ is the Laplace variable .

While elegant, the direct numerical evaluation of these [hereditary integrals](@entry_id:186265) is computationally prohibitive. It would require storing the entire strain (or stress) history at every material point and re-evaluating the integral at each time step. To overcome this, we seek a representation that depends only on the current state. This is achieved by converting the hereditary model into an **internal state variable (ISV)** formulation.

The key lies in the functional form of the [relaxation modulus](@entry_id:189592). For many [viscoelastic materials](@entry_id:194223), $G(t)$ can be well-approximated by a **Prony series** (or Dirichlet-Prony series), which is a sum of decaying exponential functions:
$$
G(t) = G_\infty + \sum_{i=1}^{N} G_i \exp\left(-\frac{t}{\tau_i}\right)
$$
Here, $G_\infty$ is the long-term or equilibrium modulus, while each pair $(G_i, \tau_i)$ represents the modulus and [relaxation time](@entry_id:142983) of a single relaxation mode. This representation is physically motivated by the generalized Maxwell model, which consists of an equilibrium spring in parallel with $N$ Maxwell elements (a spring and dashpot in series).

Substituting the Prony series into the relaxation integral yields:
$$
\boldsymbol{\sigma}(t) = G_\infty \boldsymbol{\varepsilon}(t) + \sum_{i=1}^{N} \int_0^t G_i \exp\left(-\frac{t-s}{\tau_i}\right) \dot{\boldsymbol{\varepsilon}}(s) \, \mathrm{d}s
$$
We can now define a set of **internal variables**, $\boldsymbol{\xi}_i(t)$, each representing the stress-like contribution from one of the decaying modes:
$$
\boldsymbol{\xi}_i(t) := \int_0^t G_i \exp\left(-\frac{t-s}{\tau_i}\right) \dot{\boldsymbol{\varepsilon}}(s) \, \mathrm{d}s
$$
The total stress is then simply the sum of the equilibrium response and the contributions from these internal variables:
$$
\boldsymbol{\sigma}(t) = G_\infty \boldsymbol{\varepsilon}(t) + \sum_{i=1}^{N} \boldsymbol{\xi}_i(t)
$$
The crucial insight is that each internal variable $\boldsymbol{\xi}_i(t)$ obeys a first-order ordinary differential equation (ODE). By differentiating the definition of $\boldsymbol{\xi}_i(t)$ with respect to time using the Leibniz rule, we find  :
$$
\dot{\boldsymbol{\xi}}_i(t) + \frac{1}{\tau_i} \boldsymbol{\xi}_i(t) = G_i \dot{\boldsymbol{\varepsilon}}(t)
$$
This transformation is profound. We have replaced a non-local-in-time [hereditary integral](@entry_id:199438) with a system of local-in-time first-order ODEs. The state of the material at time $t$ is now fully captured by the current strain $\boldsymbol{\varepsilon}(t)$ and the current values of the internal variables $\{\boldsymbol{\xi}_i(t)\}_{i=1}^N$. The memory of the past is encapsulated within these internal variables, eliminating the need to store the entire deformation history.

### Algorithmic Updates for Internal Variables

With the constitutive behavior expressed as a system of ODEs, the next step is to develop a numerical algorithm to integrate these equations over a discrete time step, from a known state at time $t_n$ to an unknown state at $t_{n+1} = t_n + \Delta t$.

Let's focus on the ODE for a single internal variable:
$$
\dot{\boldsymbol{\xi}}_i(t) + \frac{1}{\tau_i} \boldsymbol{\xi}_i(t) = G_i \dot{\boldsymbol{\varepsilon}}(t)
$$
The exact solution to this linear ODE over the interval $[t_n, t_{n+1}]$, found using an integrating factor, is:
$$
\boldsymbol{\xi}_i(t_{n+1}) = \boldsymbol{\xi}_i(t_n) \exp\left(-\frac{\Delta t}{\tau_i}\right) + \int_{t_n}^{t_{n+1}} G_i \exp\left(-\frac{t_{n+1}-s}{\tau_i}\right) \dot{\boldsymbol{\varepsilon}}(s) \, \mathrm{d}s
$$
The challenge now becomes evaluating the integral, which depends on the assumed behavior of the [strain rate](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}(s)$ within the time step. A common and effective choice for strain-driven problems is to assume that the strain varies linearly over the step, which implies a **constant strain rate**   :
$$
\dot{\boldsymbol{\varepsilon}}(s) = \frac{\boldsymbol{\varepsilon}_{n+1} - \boldsymbol{\varepsilon}_n}{\Delta t} = \frac{\Delta \boldsymbol{\varepsilon}}{\Delta t} \quad \text{for} \quad s \in [t_n, t_{n+1}]
$$
Under this assumption, the driving term in the integral is constant and can be taken out. The remaining [exponential integral](@entry_id:187288) can be evaluated exactly:
$$
\int_{t_n}^{t_{n+1}} \exp\left(-\frac{t_{n+1}-s}{\tau_i}\right) \, \mathrm{d}s = \tau_i \left(1 - \exp\left(-\frac{\Delta t}{\tau_i}\right)\right)
$$
Substituting this back gives the **exact algorithmic update** for the internal variable, consistent with the piecewise linear strain assumption:
$$
\boldsymbol{\xi}_{i, n+1} = \boldsymbol{\xi}_{i,n} \exp\left(-\frac{\Delta t}{\tau_i}\right) + G_i \frac{\tau_i}{\Delta t} \left(1 - \exp\left(-\frac{\Delta t}{\tau_i}\right)\right) \Delta\boldsymbol{\varepsilon}
$$
The first term represents the [exponential decay](@entry_id:136762) of the historical state, while the second term represents the new contribution generated during the current time step. The total stress at the end of the step is then assembled as:
$$
\boldsymbol{\sigma}_{n+1} = G_\infty \boldsymbol{\varepsilon}_{n+1} + \sum_{i=1}^{N} \boldsymbol{\xi}_{i, n+1}
$$
It is important to recognize that different assumptions about the within-step evolution of strain will lead to different update formulas. For instance, a fully implicit or **backward Euler** scheme might approximate the strain itself as constant over the interval, $\varepsilon(s) \approx \varepsilon_{n+1}$, which for an alternative form of the governing ODE leads to a different update rule . The choice of integration scheme is a critical part of the modeling process.

### The Algorithmic Consistent Tangent Modulus

In the context of a [nonlinear finite element analysis](@entry_id:167596), the material point update algorithm is embedded within a global [iterative solver](@entry_id:140727), typically the Newton-Raphson method. This method solves the global system of [equilibrium equations](@entry_id:172166), $\boldsymbol{R}(\boldsymbol{u}) = \boldsymbol{0}$, by iteratively finding corrections to the [displacement field](@entry_id:141476) $\boldsymbol{u}$. The efficiency of this global solver depends critically on the **tangent stiffness matrix**, $\boldsymbol{K}_T = \mathrm{d}\boldsymbol{R} / \mathrm{d}\boldsymbol{u}$.

For optimal (quadratic) convergence, $\boldsymbol{K}_T$ must be the exact Jacobian of the global residual. This requires a material point tangent modulus that is the exact linearization of the discrete [stress update algorithm](@entry_id:181937) used to compute the residual. This specific tangent is known as the **[algorithmic consistent tangent modulus](@entry_id:180789)**, defined as :
$$
\mathbb{C}^{\text{alg}} := \frac{\mathrm{d}\boldsymbol{\sigma}_{n+1}}{\mathrm{d}\boldsymbol{\varepsilon}_{n+1}}
$$
Crucially, this derivative must account for the full dependency of $\boldsymbol{\sigma}_{n+1}$ on $\boldsymbol{\varepsilon}_{n+1}$, including the implicit dependence through the updated internal variables $\boldsymbol{\xi}_{i, n+1}$. Using an approximation, such as the [continuum tangent modulus](@entry_id:201751) ($\dot{\boldsymbol{\sigma}}/\dot{\boldsymbol{\varepsilon}}$) or a purely elastic tangent, will destroy the quadratic convergence of the Newton method.

For the explicit update rule derived in the previous section, the consistent tangent can be found by direct differentiation. Differentiating the expressions for $\boldsymbol{\sigma}_{n+1}$ and $\boldsymbol{\xi}_{i, n+1}$ with respect to $\boldsymbol{\varepsilon}_{n+1}$ (noting that $\partial\Delta\boldsymbol{\varepsilon}/\partial\boldsymbol{\varepsilon}_{n+1} = \mathbb{I}$, the fourth-order identity tensor) yields  :
$$
\mathbb{C}^{\text{alg}} = \frac{\partial \boldsymbol{\sigma}_{n+1}}{\partial \boldsymbol{\varepsilon}_{n+1}} = G_\infty \mathbb{I} + \sum_{i=1}^{N} \frac{\partial \boldsymbol{\xi}_{i, n+1}}{\partial \boldsymbol{\varepsilon}_{n+1}} = G_\infty \mathbb{I} + \sum_{i=1}^{N} G_i \frac{\tau_i}{\Delta t} \left(1 - \exp\left(-\frac{\Delta t}{\tau_i}\right)\right) \mathbb{I}
$$
More generally, if the local update involves solving a nonlinear system for the internal variables, $\boldsymbol{r}(\boldsymbol{\alpha}_{n+1}, \boldsymbol{\varepsilon}_{n+1}) = \boldsymbol{0}$, the consistent tangent is given by the [implicit function theorem](@entry_id:147247) as :
$$
\mathbb{C}^{\text{alg}} = \frac{\partial \hat{\boldsymbol{\sigma}}}{\partial \boldsymbol{\varepsilon}} - \frac{\partial \hat{\boldsymbol{\sigma}}}{\partial \boldsymbol{\alpha}} \left( \frac{\partial \boldsymbol{r}}{\partial \boldsymbol{\alpha}} \right)^{-1} \frac{\partial \boldsymbol{r}}{\partial \boldsymbol{\varepsilon}}
$$
where all partial derivatives are evaluated at the end-of-step state.

### Stability and Thermodynamic Consistency of Algorithms

A numerical algorithm must not only be accurate but also stable. An unstable algorithm can produce [spurious oscillations](@entry_id:152404) or unbounded growth in the solution, rendering it useless. The stability of time-integration schemes for ODEs is often analyzed by examining how they treat the [homogeneous equation](@entry_id:171435). For a Maxwell mode, this is the simple relaxation equation $\dot{\sigma} = -\sigma/\tau$ .

Applying the simple **forward Euler** (explicit) scheme, $\sigma_{n+1} = \sigma_n + \Delta t(-\sigma_n/\tau)$, gives the update $\sigma_{n+1} = (1 - \Delta t/\tau)\sigma_n$. The [amplification factor](@entry_id:144315) is $A = 1 - \Delta t/\tau$. For stability, we require $|A| \le 1$, which leads to the condition $\Delta t/\tau \le 2$. This means the forward Euler scheme is only **conditionally stable**; the time step must be smaller than twice the material's [relaxation time](@entry_id:142983). For materials with very fast relaxation processes (small $\tau$), this can impose an unacceptably small time step.

In contrast, the **backward Euler** (implicit) scheme, $\sigma_{n+1} = \sigma_n + \Delta t(-\sigma_{n+1}/\tau)$, yields the update $\sigma_{n+1} = (1 + \Delta t/\tau)^{-1}\sigma_n$. The amplification factor is $A = 1/(1 + \Delta t/\tau)$. Since $\Delta t$ and $\tau$ are positive, we have $0  A \le 1$ for any choice of $\Delta t > 0$. The backward Euler scheme is therefore **unconditionally stable** from a linear stability perspective, making it far more robust for [stiff systems](@entry_id:146021) with a wide range of relaxation times.

A deeper and more powerful concept is **[thermodynamic consistency](@entry_id:138886)**. A physically realistic [constitutive model](@entry_id:747751) and its numerical implementation must obey the [second law of thermodynamics](@entry_id:142732). For isothermal processes, this is expressed by the **Clausius-Duhem inequality**, which states that the [dissipation rate](@entry_id:748577) must be non-negative . For a material with free energy density $\psi$, the dissipation $\mathcal{D}$ is given by:
$$
\mathcal{D} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0
$$
By applying the Coleman-Noll procedure, this inequality can be used to derive constraints on the constitutive functions. For example, for a Maxwell model, it leads to the standard stress-strain relation and an evolution equation for the internal variable, while requiring positive definite [elastic moduli](@entry_id:171361) and positive viscosities to ensure non-negative dissipation .

An ideal numerical scheme should preserve this fundamental property at the discrete level. That is, the **algorithmic dissipation** over a time step must be non-negative. This is a criterion for [unconditional stability](@entry_id:145631). It can be rigorously proven that for a large class of [internal variable models](@entry_id:750757), the backward Euler integration scheme satisfies a discrete version of the [dissipation inequality](@entry_id:188634) . This means the algorithmic dissipation over a time step—defined as the incremental work done on the material point minus the change in its stored free energy—is guaranteed to be non-negative. For an increment of strain $\Delta\boldsymbol{\varepsilon}$, this can be expressed as:
$$
D^{\text{alg}} = (\boldsymbol{\sigma}_{n+1}:\Delta\boldsymbol{\varepsilon}) - \Delta\psi \ge 0
$$
where $\Delta\psi$ is the change in the free energy density $\psi$ over the step. This property guarantees that the numerical scheme will not spuriously generate energy, ensuring its robustness regardless of the time step size. This [thermodynamic consistency](@entry_id:138886) is the primary reason for the widespread use of implicit integration schemes in [computational solid mechanics](@entry_id:169583) for hereditary materials.