## Introduction
The time-dependent deformation of geomaterials, manifesting as creep and stress relaxation, is a central concern in computational geomechanics, dictating the long-term safety, stability, and serviceability of countless engineering projects. From the slow settlement of foundations to the gradual closure of underground tunnels, understanding and predicting these phenomena is not merely an academic exercise but a practical necessity. This article addresses the critical knowledge gap between simplified elastic assumptions and the complex reality of time-dependent material behavior. It provides a structured journey through the theoretical foundations and practical applications of creep and stress relaxation, designed for graduate-level engineers and scientists.

The following chapters will equip you with a robust understanding of this field. First, in **Principles and Mechanisms**, we will establish the fundamental language of viscoelasticity, deriving the concepts of creep compliance and relaxation modulus, and building intuition through canonical rheological models like the Maxwell and Zener models. We will progress to advanced formulations including Prony series, nonlinearity, and multi-physics coupling. Next, **Applications and Interdisciplinary Connections** will translate this theory into practice, exploring how these models are used to solve critical problems in geotechnical engineering, from slope stability and creep buckling to the design of underground structures in rock salt, and demonstrating connections to materials science and geophysics. Finally, **Hands-On Practices** will provide a set of guided computational problems, allowing you to implement the constitutive models and numerical methods essential for modern geomechanical simulation.

## Principles and Mechanisms

The time-dependent deformation of geomaterials under sustained loading is a critical consideration in geotechnical engineering and geophysics. Phenomena such as the long-term settlement of foundations, the closure of underground openings, and the flow of rock salt in diapirs are governed by the mechanisms of creep and stress relaxation. This chapter elucidates the fundamental principles and constitutive models used to describe these behaviors, progressing from linear viscoelasticity to more advanced concepts including nonlinearity, damage, and hydromechanical coupling.

### Fundamental Concepts: Creep and Stress Relaxation

At the heart of time-dependent material behavior are two canonical phenomena: **creep** and **stress relaxation**. Creep is the progressive increase in strain over time when a material is subjected to a constant stress. Conversely, stress relaxation is the gradual decrease in stress over time required to maintain a constant strain in the material.

To quantify these behaviors within a consistent mathematical framework, we introduce two fundamental material functions for linear viscoelastic materials. These functions are defined based on the material's response to an idealized step input in either stress or strain [@problem_id:3513945].

The **creep compliance**, denoted by $J(t)$, characterizes the strain response to a unit step in stress. For a uniaxial test where a constant stress $\sigma_0$ is applied at time $t=0$ (represented by a Heaviside step function, $\sigma(t) = \sigma_0 H(t)$), the resulting time-dependent strain $\varepsilon(t)$ is given by $\varepsilon(t) = J(t)\sigma_0$. The creep compliance is therefore experimentally determined as the ratio of strain to the constant applied stress:

$J(t) = \frac{\varepsilon(t)}{\sigma_0}$

The function $J(t)$ encapsulates the material's increasing deformability over time. Its initial value, $J(0^+)$, represents the instantaneous elastic compliance, and its evolution for $t>0$ describes the delayed or viscous deformation.

The **relaxation modulus**, denoted by $G(t)$ for shear or $E(t)$ for uniaxial stress, characterizes the stress response to a unit step in strain. In a shear test where a constant shear strain $\gamma_0$ is imposed at $t=0$ (i.e., $\gamma(t) = \gamma_0 H(t)$), the resulting shear stress $\tau(t)$ decays over time. The shear relaxation modulus $G(t)$ is defined as the ratio of this decaying stress to the constant applied strain:

$G(t) = \frac{\tau(t)}{\gamma_0}$

The function $G(t)$ represents the material's diminishing stiffness over time. Its initial value, $G(0^+)$, is the instantaneous elastic modulus, and its decay reflects the internal relaxation of mechanical energy.

These definitions are cornerstones of **linear viscoelasticity**, which is built upon the **Boltzmann superposition principle**. This principle states that the response to a complex loading history is the linear sum of responses to infinitesimal increments of loading applied throughout that history. For an arbitrary strain history $\varepsilon(t)$, the stress $\sigma(t)$ is given by a hereditary integral:

$\sigma(t) = \int_{-\infty}^{t} E(t-t') \frac{d\varepsilon(t')}{dt'} dt'$

Similarly, for an arbitrary stress history $\sigma(t)$, the strain $\varepsilon(t)$ is:

$\varepsilon(t) = \int_{-\infty}^{t} J(t-t') \frac{d\sigma(t')}{dt'} dt'$

The experimental determination of these functions requires meticulous care. As detailed in advanced testing protocols, it is crucial to control environmental factors such as temperature and moisture, which can significantly alter the viscoelastic response of geomaterials. Furthermore, obtaining the material's true response requires applying strain or stress steps that are rapid compared to the material's characteristic relaxation times, while avoiding inertial oscillations. For a uniaxial test, deriving the fundamental shear modulus $G(t)$ necessitates measuring both axial stress and lateral strain to determine the time-dependent Poisson's ratio, $\nu(t)$, and subsequently solving an inversion problem [@problem_id:3513993].

### Rheological Models of Linear Viscoelasticity

To gain physical insight into viscoelastic behavior, it is useful to represent materials as combinations of idealized mechanical elements: linear elastic **springs** (obeying $\sigma = E\varepsilon$) and linear viscous **dashpots** (obeying $\sigma = \eta\dot{\varepsilon}$, where $\eta$ is viscosity and $\dot{\varepsilon}$ is the strain rate). Different arrangements of these elements produce models that capture distinct aspects of creep and relaxation [@problem_id:3513936].

#### The Maxwell Model

The **Maxwell model** consists of a spring and a dashpot connected in series. Because the elements are in series, the stress is the same in both, and the total strain rate is the sum of the individual strain rates. This arrangement leads to the governing differential equation [@problem_id:3513961]:

$\dot{\varepsilon}(t) = \frac{\dot{\sigma}(t)}{E} + \frac{\sigma(t)}{\eta}$

Under a constant stress $\sigma_0$ (creep), the strain rate is constant, $\dot{\varepsilon} = \sigma_0/\eta$, leading to strain that grows linearly with time without bound: $\varepsilon(t) = \sigma_0/E + (\sigma_0/\eta)t$. This behavior is characteristic of a viscous fluid. Under a constant strain $\varepsilon_0$ (stress relaxation), the stress decays exponentially to zero: $\sigma(t) = E\varepsilon_0 \exp(-t/\tau_{rel})$, where $\tau_{rel} = \eta/E$ is the relaxation time. The Maxwell model is thus a simple model of a viscoelastic fluid that exhibits complete stress relaxation.

#### The Kelvin-Voigt Model

The **Kelvin-Voigt model** connects a spring and a dashpot in parallel. In this case, the strain is the same in both elements, and the total stress is the sum of the stresses. This leads to the governing equation:

$\sigma(t) = E\varepsilon(t) + \eta\dot{\varepsilon}(t)$

Under a constant stress $\sigma_0$ (creep), the strain approaches a finite limit, $\varepsilon(\infty) = \sigma_0/E$, exponentially. However, this model cannot exhibit an instantaneous elastic strain, and more problematically, it cannot exhibit stress relaxation under a step strain. Applying an instantaneous strain would require an infinite stress to move the dashpot, making it an inadequate model for solids that show both instantaneous elasticity and stress relaxation.

#### The Standard Linear Solid (Zener) Model

To create a more realistic model for a viscoelastic solid, we can combine the previous elements. The **Standard Linear Solid (SLS) model**, also known as the **Zener model**, is often constructed by placing a Maxwell element in parallel with a spring. This three-parameter model successfully captures the key features of many geomaterials. Its governing differential equation is more complex, but its behavior is insightful.

Under a constant stress (creep), the SLS model exhibits an instantaneous elastic strain, followed by transient creep that exponentially approaches a finite long-term strain. This represents a solid that creeps but does not flow indefinitely. Under a constant strain (stress relaxation), the model shows an instantaneous stress, which then exponentially decays to a finite, non-zero equilibrium stress. This reflects a solid that can relax some of its stress but maintains a permanent elastic resistance to the deformation. The SLS model provides a far better, albeit still simplified, representation of geomaterial behavior than the two-element models.

### Advanced and Generalized Models

#### The Generalized Maxwell Model and Prony Series

Real geomaterials do not relax with a single relaxation time but exhibit a **spectrum of relaxation times**. To capture this, we can extend the SLS model to the **Generalized Maxwell Model**. This model consists of an equilibrium spring (with modulus $G_\infty$) in parallel with multiple Maxwell branches, each with its own spring modulus $G_i$ and dashpot viscosity $\eta_i$.

For a step strain, the total stress is the sum of the stress in the equilibrium spring and the stresses in each Maxwell branch. As each branch's stress decays exponentially with its own characteristic relaxation time, $\tau_i = \eta_i/G_i$, the total relaxation modulus of the system takes the form of a **Prony series** [@problem_id:3514008]:

$G(t) = G_{\infty} + \sum_{i=1}^{n} G_{i} \exp\left(-\frac{t}{\tau_{i}}\right)$

This representation is extremely powerful. It is thermodynamically consistent and can approximate any physically reasonable relaxation behavior by including a sufficient number of terms. The Prony series is the standard functional form used in computational mechanics codes to represent linear viscoelastic materials, as it allows the hereditary integral to be computed efficiently via recursive update algorithms.

#### Fractional Viscoelasticity and Power-Law Behavior

Over wide ranges of time, the creep and relaxation behaviors of many geomaterials (such as salt rock, shale, and concrete) are better described by power laws than by sums of exponentials. For example, creep strain may follow $\varepsilon(t) \propto t^{\alpha}$ with $0  \alpha  1$. This behavior, lacking a characteristic time scale, is difficult to model with a discrete Prony series.

**Fractional viscoelasticity** offers a compelling mathematical framework to capture such behavior. By replacing the integer-order time derivatives in rheological models with fractional derivatives, we can naturally generate power-law responses. A fundamental element is the **Scott-Blair fractional element**, defined by the constitutive law $\sigma(t) = \eta_{\alpha} {}^{C}D_{t}^{\alpha}\varepsilon(t)$, where ${}^{C}D_{t}^{\alpha}$ is the Caputo fractional derivative of order $\alpha$.

This simple model, which interpolates between a pure spring ($\alpha \to 0$) and a pure dashpot ($\alpha \to 1$), gives rise to a power-law creep compliance $J(t) \propto t^{\alpha}$ and a power-law relaxation modulus $G(t) \propto t^{-\alpha}$ [@problem_id:3513952]. These models are thermodynamically consistent and provide a compact description of the broad-spectrum, self-similar relaxation processes often observed in complex, multiscale materials.

### Extensions of the Viscoelastic Framework

#### Nonlinearity: Quasi-Linear Viscoelasticity (QLV)

The models discussed thus far are linear, meaning their response is directly proportional to the magnitude of the input. This assumption is often violated in geomaterials, even at modest strain levels. **Quasi-Linear Viscoelasticity (QLV)**, pioneered by Y.C. Fung, provides a practical extension to account for nonlinear elasticity while retaining the mathematical convenience of linear superposition in time [@problem_id:3513988].

The core assumption of QLV is that the relaxation response can be factorized into a strain-dependent part and a time-dependent part. For a step strain $\varepsilon_0$, the stress is given by:

$\sigma(t) = G(t) \sigma^e(\varepsilon_0)$

Here, $\sigma^e(\varepsilon_0)$ is the nonlinear instantaneous elastic response (the stress at time $t=0^+$), and $G(t)$ is a *reduced relaxation function* (with $G(0)=1$) that is assumed to be independent of the strain magnitude. This separability can be tested experimentally: if relaxation curves from different strain levels collapse onto a single master curve when normalized by their initial stress, the QLV model is applicable. For general loading histories, the QLV model is expressed through a hereditary integral involving the nonlinear elastic stress function, demonstrating that linear viscoelasticity is the special case of QLV where the instantaneous response is linear.

#### Viscoelasticity vs. Viscoplasticity

It is crucial to distinguish **viscoelasticity** from **viscoplasticity**. While both involve time-dependent, inelastic strain, their physical underpinnings differ fundamentally. Viscoelasticity describes recoverable (or partially recoverable) deformation with memory, occurring at any stress level. Viscoplasticity, conversely, is a rate-dependent form of plasticity that involves permanent, irrecoverable flow [@problem_id:3A4061].

**Perzyna-type viscoplasticity** models are founded on the concept of an **overstress**. Flow does not occur so long as the stress state is within a static **yield surface**, defined by a function $f(\boldsymbol{\sigma}, p) \le 0$, where $p$ is a hardening variable. When the stress exceeds this surface ($f > 0$), a viscoplastic strain rate $\dot{\boldsymbol{\varepsilon}}^{vp}$ is generated, whose magnitude depends on the magnitude of the overstress (e.g., $\dot{\boldsymbol{\varepsilon}}^{vp} \propto \langle f \rangle^m$) and whose direction is given by a flow potential.

This leads to a key difference in stress relaxation: a viscoelastic solid can relax continuously as long as it is held at a fixed strain. A viscoplastic solid, however, will only relax until its stress state recedes to the boundary of the yield surface ($f=0$). At that point, the overstress vanishes, and all time-dependent flow ceases.

#### Coupling with Pore Fluids: Poroviscoelasticity

The behavior of fluid-saturated geomaterials like soils and clays is governed by the strong coupling between the deformation of the solid skeleton and the flow of pore fluid. This is classically described by Biot's theory of **poroelasticity**. This framework can be extended to **poroviscoelasticity** by replacing the elastic constitutive law for the drained solid skeleton with a viscoelastic one [@problem_id:3513934].

Following the principles of linear viscoelasticity, the effective stress $\boldsymbol{\sigma}'$ on the skeleton is related to the strain history through hereditary integrals involving the drained relaxation moduli, $K_d(t)$ and $G_d(t)$. This viscoelastic constitutive law is then incorporated into the overall momentum balance equation for the mixture. The fluid flow is governed by Darcy's law, and its mass conservation is coupled to the skeleton's volumetric strain. This results in a system of two coupled integro-differential field equations for the solid displacement $\mathbf{u}$ and the pore pressure $p$:

Momentum Balance:
$\nabla \cdot \left[ 2\int_{0}^{t} G_d(t-\tau) \dot{\mathbf{e}}(\tau) d\tau + \int_{0}^{t} K_d(t-\tau) \dot{\varepsilon}_v(\tau) \mathbf{I} d\tau \right] - \alpha\nabla p + \rho\mathbf{b} = \mathbf{0}$

Fluid Mass Balance:
$\frac{1}{M}\dot{p} + \alpha\dot{\varepsilon}_v - \nabla \cdot \left(\frac{k}{\mu}\nabla p\right) = s$

This framework is essential for analyzing problems such as long-term consolidation settlement, where the time scale of viscous creep in the soil skeleton can be comparable to the time scale of pore pressure dissipation.