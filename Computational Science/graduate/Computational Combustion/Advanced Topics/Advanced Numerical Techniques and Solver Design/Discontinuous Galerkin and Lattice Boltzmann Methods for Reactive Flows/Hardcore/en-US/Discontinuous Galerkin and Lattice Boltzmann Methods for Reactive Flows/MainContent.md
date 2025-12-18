## Introduction
Simulating [reactive flows](@entry_id:190684), particularly in the field of combustion, is a cornerstone of modern engineering and scientific research. The ability to accurately predict phenomena like [flame propagation](@entry_id:1125066), detonation, and [pollutant formation](@entry_id:1129911) is critical for designing more efficient and cleaner energy systems. However, these flows present a formidable computational challenge. They are governed by the compressible Navier-Stokes equations, which couple fluid dynamics, multi-species transport, and highly nonlinear chemical kinetics. The core difficulty stems from the multi-scale nature of the problem: the hyperbolic character of fluid advection, which gives rise to shock waves and sharp gradients, must be resolved alongside chemical reactions that occur on timescales many orders of magnitude faster, a property known as stiffness.

This article provides a detailed examination of two powerful numerical frameworks designed to tackle these challenges: the Discontinuous Galerkin (DG) and the Lattice Boltzmann (LBM) methods. Instead of presenting a surface-level survey, we will dive deep into the theoretical and practical aspects that make these methods suitable for simulating stiff, compressible [reactive flows](@entry_id:190684). The reader will gain a robust understanding of not only the methods themselves but also the physical and mathematical problems they are designed to solve.

The discussion is structured across three core chapters. The first chapter, **"Principles and Mechanisms"**, lays the mathematical groundwork by dissecting the governing equations and exploring the concepts of hyperbolicity and [chemical stiffness](@entry_id:1122356). It then systematically builds the DG and LBM frameworks, detailing how each method discretizes the convective, diffusive, and reactive components of the flow. The second chapter, **"Applications and Interdisciplinary Connections"**, transitions from theory to practice, showcasing how these methods are applied to canonical combustion problems such as laminar flames and detonations and discussing advanced techniques for ensuring robustness and physical accuracy. Finally, the **"Hands-On Practices"** chapter offers targeted exercises designed to solidify the key theoretical concepts through practical implementation and analysis. By progressing through these sections, the reader will develop a comprehensive understanding of DG and LBM for [reactive flow](@entry_id:1130651) simulation.

## Principles and Mechanisms

This chapter delves into the fundamental principles and numerical mechanisms underpinning the simulation of [reactive flows](@entry_id:190684) using the Discontinuous Galerkin (DG) and Lattice Boltzmann (LBM) methods. We begin by establishing the governing mathematical framework—the compressible Navier-Stokes equations for multi-component reacting gases. We then analyze the intrinsic mathematical properties of these equations, namely their hyperbolic character and the numerical stiffness introduced by chemical kinetics. With this foundation, we will systematically construct the DG and LBM frameworks, detailing how each method addresses the challenges of discretizing convective, diffusive, and reactive phenomena.

### The Governing Equations of Reactive Flows

The dynamics of a compressible, multi-component, reacting fluid are described by a set of coupled partial differential equations that express the conservation of total mass, momentum, total energy, and the mass of each individual chemical species. For a system with $N_s$ species, these laws can be written in a compact, [conservative form](@entry_id:747710) suitable for [numerical discretization](@entry_id:752782) :

$$
\partial_t \mathbf{U} + \nabla \cdot \mathbf{F}^c(\mathbf{U}) = \nabla \cdot \mathbf{F}^v(\mathbf{U}, \nabla \mathbf{U}) + \mathbf{S}(\mathbf{U}, T)
$$

Here, $\mathbf{U}$ is the vector of conserved [state variables](@entry_id:138790), $\mathbf{F}^c$ is the convective (or inviscid) flux tensor, $\mathbf{F}^v$ is the viscous (or diffusive) flux tensor, and $\mathbf{S}$ is the vector of source terms, which includes contributions from [body forces](@entry_id:174230) and chemical reactions.

#### State Vector and Convective Fluxes

The state vector $\mathbf{U}$ contains the densities of the conserved quantities:

$$
\mathbf{U} = \begin{bmatrix} \rho \\ \rho \mathbf{u} \\ \rho E \\ \rho Y_1 \\ \vdots \\ \rho Y_{N_s} \end{bmatrix}
$$

where $\rho$ is the total mixture density, $\mathbf{u}$ is the mass-averaged fluid velocity vector, $Y_k$ is the mass fraction of species $k$ (with $\sum_{k=1}^{N_s} Y_k = 1$), and $E$ is the total specific energy. The total energy is the sum of the specific internal energy, $e$, and the specific kinetic energy: $E = e + \frac{1}{2} |\mathbf{u}|^2$.

The [convective flux](@entry_id:158187) tensor, $\mathbf{F}^c$, represents the transport of these conserved quantities with the bulk fluid motion. It is given by:

$$
\mathbf{F}^c(\mathbf{U}) = \begin{bmatrix}
\rho \mathbf{u} \\
\rho \mathbf{u} \otimes \mathbf{u} + p \mathbf{I} \\
(\rho E + p) \mathbf{u} \\
\rho Y_1 \mathbf{u} \\
\vdots \\
\rho Y_{N_s} \mathbf{u}
\end{bmatrix}
$$

where $p$ is the thermodynamic pressure and $\mathbf{I}$ is the identity tensor. The term $\rho \mathbf{u} \otimes \mathbf{u}$ represents the [convective transport](@entry_id:149512) of momentum, while $p \mathbf{I}$ accounts for the pressure forces. The total [energy flux](@entry_id:266056), $(\rho E + p) \mathbf{u}$, can be recognized as the advection of total enthalpy, $H = E + p/\rho$.

#### Viscous Fluxes and Transport Properties

The viscous flux tensor, $\mathbf{F}^v$, accounts for dissipative processes driven by gradients in velocity, temperature, and species concentration. It is structured as:

$$
\mathbf{F}^v(\mathbf{U}, \nabla \mathbf{U}) = \begin{bmatrix}
\mathbf{0} \\
\boldsymbol{\tau} \\
\boldsymbol{\tau} \cdot \mathbf{u} - \mathbf{q} - \sum_{k=1}^{N_s} h_k \mathbf{J}_k \\
\mathbf{J}_1 \\
\vdots \\
\mathbf{J}_{N_s}
\end{bmatrix}
$$

The components of this tensor are defined by physical models for transport phenomena:
- **Viscous Stress Tensor ($\boldsymbol{\tau}$):** For a Newtonian fluid, the stress is proportional to the rate of strain. Assuming Stokes' hypothesis (zero [bulk viscosity](@entry_id:187773)), the tensor is given by $\boldsymbol{\tau} = \mu \left[ \nabla \mathbf{u} + (\nabla \mathbf{u})^\top - \frac{2}{3} (\nabla \cdot \mathbf{u}) \mathbf{I} \right]$, where $\mu$ is the [dynamic viscosity](@entry_id:268228) of the mixture.

- **Heat Flux Vector ($\mathbf{q}$):** This is typically modeled by Fourier's law of heat conduction, $\mathbf{q} = -k \nabla T$, where $k$ is the thermal conductivity of the mixture and $T$ is the temperature.

- **Species Diffusive Flux Vector ($\mathbf{J}_k$):** This vector represents the mass flux of species $k$ relative to the [mass-averaged velocity](@entry_id:149575) $\mathbf{u}$. A common simplified model is the mixture-averaged formulation, where Fick's law is a primary component. A consistent formulation must ensure that [mass diffusion](@entry_id:149532) does not generate a net mass flux, i.e., $\sum_{k=1}^{N_s} \mathbf{J}_k = \mathbf{0}$. This constraint is satisfied, for example, by a form such as $\mathbf{J}_k = - \rho D_{k,m} \nabla Y_k + \rho Y_k \sum_{\ell=1}^{N_s} D_{\ell,m} \nabla Y_\ell$, where $D_{k,m}$ is the [mixture-averaged diffusion](@entry_id:1127972) coefficient of species $k$.

A critical component in the [energy equation](@entry_id:156281) for [reacting flows](@entry_id:1130631) is the term $\sum_{k=1}^{N_s} h_k \mathbf{J}_k$. This represents the transport of energy due to the diffusion of species, where each species $k$ carries its [specific enthalpy](@entry_id:140496) $h_k$. Neglecting this term can lead to significant errors in predicting flame structures and temperatures.

#### Chemical Source Terms

The source term vector $\mathbf{S}$ contains contributions from body forces (e.g., gravity) and, most importantly for combustion, chemical reactions:

$$
\mathbf{S}(\mathbf{U}, T) = \begin{bmatrix}
0 \\
\rho \mathbf{f} \\
\rho \mathbf{u} \cdot \mathbf{f} \\
\dot{\omega}_1 \\
\vdots \\
\dot{\omega}_{N_s}
\end{bmatrix}
$$

Here, $\mathbf{f}$ is the [body force](@entry_id:184443) per unit mass. The term $\dot{\omega}_k$ is the mass production rate of species $k$ per unit volume due to chemical reactions. The total mass must be conserved by the chemistry, which imposes the constraint $\sum_{k=1}^{N_s} \dot{\omega}_k = 0$.

The species production rate $\dot{\omega}_k$ is determined by the [chemical kinetic mechanism](@entry_id:1122345). For a set of elementary, [reversible reactions](@entry_id:202665) of the form $\sum_j \nu_{j,r}' X_j \rightleftharpoons \sum_j \nu_{j,r}'' X_j$, the law of [mass action](@entry_id:194892) states that the [rate of reaction](@entry_id:185114) depends on the product of the molar concentrations of the reactants (for the forward reaction) and products (for the backward reaction). The net rate of progress of reaction $r$ (in moles per unit volume per unit time) is given by:

$$
q_r = k_{f,r} \prod_{j} C_{j}^{\nu_{j,r}'} - k_{b,r} \prod_{j} C_{j}^{\nu_{j,r}''}
$$

where $C_j$ is the [molar concentration](@entry_id:1128100) of species $j$, $k_{f,r}$ and $k_{b,r}$ are the forward and backward [rate constants](@entry_id:196199), and $\nu_{j,r}'$ and $\nu_{j,r}''$ are the stoichiometric coefficients.

The total molar production rate of species $k$ is the sum of its production rates over all reactions. This is found by multiplying $q_r$ by the net stoichiometric coefficient of species $k$ in reaction $r$, defined as $\nu_{k,r} = \nu_{k,r}'' - \nu_{k,r}'$. To obtain the mass production rate $\dot{\omega}_k$, we multiply the total molar rate by the molecular weight of species $k$, $W_k$ :

$$
\dot{\omega}_k = W_k \sum_{r} \nu_{k,r} q_r = W_k \sum_{r} \nu_{k,r} \left(k_{f,r} \prod_{j} C_{j}^{\nu_{j,r}'} - k_{b,r} \prod_{j} C_{j}^{\nu_{j,r}''}\right)
$$

These source terms are highly nonlinear functions of species concentrations and temperature (through the rate constants $k_f$ and $k_b$), and they are the origin of the profound numerical challenges in simulating [reactive flows](@entry_id:190684).

### Hyperbolic Structure and Chemical Stiffness

To devise robust numerical methods, we must first understand the mathematical character of the governing equations. The structure is determined by the convective part, the Euler equations, while the source terms introduce the challenge of stiffness.

#### Hyperbolicity of the Euler Equations

The system of conservation laws is hyperbolic if the flux Jacobian matrix, $\mathbf{A}(\mathbf{U}) = \partial \mathbf{F}^c / \partial \mathbf{U}$, has a complete set of real eigenvalues and [linearly independent](@entry_id:148207) eigenvectors. These eigenvalues represent the [characteristic speeds](@entry_id:165394) at which information propagates through the fluid.

For the one-dimensional reactive Euler system, the flux Jacobian can be shown to have the eigenvalues $\{u-c, u, u, u+c\}$ . These are all real provided the physical state is well-defined (e.g., positive density and non-[negative pressure](@entry_id:161198)). These eigenvalues correspond to:
- **Acoustic waves:** Two waves traveling at speeds $u-c$ and $u+c$ relative to a stationary observer, representing the propagation of pressure disturbances. Here, $c = \sqrt{\gamma p / \rho}$ is the *frozen* speed of sound, where $\gamma$ is the ratio of specific heats of the fixed local mixture.
- **Entropy wave:** A wave traveling at the local fluid speed $u$, which carries disturbances in entropy.
- **Composition wave(s):** For a multi-species mixture, discontinuities in species concentrations also travel with the fluid speed $u$. This is why the eigenvalue $u$ has a [multiplicity](@entry_id:136466) corresponding to the number of independent species variables plus one (for entropy).

The existence of this wave structure is fundamental. Numerical methods like DG must be designed to correctly capture the interactions of these waves at element interfaces.

#### The Challenge of Chemical Stiffness

While the convective terms define the hyperbolic structure, the chemical source terms $\dot{\omega}_k$ introduce a different kind of numerical difficulty known as **stiffness**. Stiffness arises from the presence of widely disparate timescales in the problem. In combustion, the chemical reaction timescales can be many orders of magnitude smaller than the fluid transport (advective or diffusive) timescales.

The origin of this stiffness lies in the Arrhenius form of the [reaction rate constants](@entry_id:187887), typically written as $k_f = A T^n \exp(-E_a/(R T))$, where $E_a$ is the activation energy. The exponential dependence on temperature makes the reaction rate extremely sensitive to temperature changes. A small increase in temperature can cause the reaction rate to increase dramatically, and consequently, the chemical timescale, which can be defined as $\tau_{\text{chem}} \propto 1/k_f$, can decrease by orders of magnitude .

We can quantify this timescale separation using the **Damköhler number**, defined as the ratio of a characteristic flow timescale to a characteristic chemical timescale:

$$
Da = \frac{\tau_{\text{flow}}}{\tau_{\text{chem}}}
$$

For example, a flow with a characteristic velocity $U=1 \, \mathrm{m/s}$ and length scale $L=10^{-2} \, \mathrm{m}$ has a flow timescale $\tau_{\text{flow}} = L/U = 10^{-2} \, \mathrm{s}$. A typical high-temperature reaction might have a timescale of $\tau_{\text{chem}} \approx 10^{-6} \, \mathrm{s}$. This results in a very large Damköhler number, $Da \approx 10^4$.

This large [separation of timescales](@entry_id:191220) ($ \tau_{\text{chem}} \ll \tau_{\text{flow}} $) is the hallmark of a stiff system. When integrating such a system with a standard [explicit time-stepping](@entry_id:168157) scheme, the stability of the method is dictated by the fastest timescale, requiring a time step $\Delta t \lesssim \tau_{\text{chem}}$. This can be computationally prohibitive, as one would need millions of tiny time steps to simulate the evolution of the flow over a single characteristic flow time. This challenge motivates the use of specialized numerical techniques, such as [implicit time integration](@entry_id:171761) or operator splitting, which will be discussed later.

### The Discontinuous Galerkin Method for Reactive Flows

The Discontinuous Galerkin (DG) method is a powerful finite element technique that is particularly well-suited for [hyperbolic conservation laws](@entry_id:147752). It combines the geometric flexibility of [finite element methods](@entry_id:749389) with the [high-order accuracy](@entry_id:163460) and shock-capturing capabilities of [finite volume methods](@entry_id:749402).

#### Foundational Concepts: Weak Form and Numerical Flux

The DG method begins by partitioning the domain $\Omega$ into a mesh of non-overlapping elements $K$. Unlike traditional continuous [finite element methods](@entry_id:749389), the solution approximation $u_h$ is allowed to be discontinuous across element boundaries. Within each element $K$, the solution is represented as a polynomial of degree $p$.

The governing PDE is multiplied by a [test function](@entry_id:178872) $\varphi_h$ (also a polynomial of degree $p$) and integrated over a single element $K$. For a [scalar conservation law](@entry_id:754531) $\partial_t u + \nabla \cdot \boldsymbol{f}(u) = 0$, this gives:

$$
\int_K (\partial_t u_h) \varphi_h \, dV + \int_K (\nabla \cdot \boldsymbol{f}(u_h)) \varphi_h \, dV = 0
$$

Applying [integration by parts](@entry_id:136350) to the flux term transfers the spatial derivative onto the test function and introduces an integral over the element boundary $\partial K$:

$$
\int_K (\partial_t u_h) \varphi_h \, dV - \int_K \boldsymbol{f}(u_h) \cdot \nabla \varphi_h \, dV + \int_{\partial K} (\boldsymbol{f}(u_h) \cdot \mathbf{n}_K) \varphi_h \, dS = 0
$$

where $\mathbf{n}_K$ is the outward-pointing unit normal on $\partial K$. Since the solution $u_h$ is discontinuous, the flux $\boldsymbol{f}(u_h)$ is not uniquely defined on the element faces. The key idea in DG is to replace the physical flux $\boldsymbol{f}(u_h) \cdot \mathbf{n}_K$ with a **numerical flux**, denoted $\widehat{\boldsymbol{f}}(u_h^-, u_h^+)$, which depends on the solution values from both sides of the face ($u_h^-$ and $u_h^+$). This [numerical flux](@entry_id:145174) provides the coupling between adjacent elements.

To formalize this, we introduce the **jump** and **average** operators on an interior face $F$ separating elements $K^-$ and $K^+$, with normal $\mathbf{n}$ pointing from $K^-$ to $K^+$ . For a scalar function $v$, the jump is $[v] = v^- - v^+$ and the average is $\{v\} = (v^- + v^+)/2$. The contribution from the interior faces to the global [weak form](@entry_id:137295) can be written compactly using these operators. For a consistent [numerical flux](@entry_id:145174), this contribution takes the form $\int_F \widehat{f_n} [ \varphi_h ] \, dS$, where $\widehat{f_n}$ is the normal component of the [numerical flux](@entry_id:145174).

#### Discretization of Hyperbolic Terms

The choice of [numerical flux](@entry_id:145174) is critical to the stability and accuracy of the DG scheme. The flux must be consistent with the physical flux and must introduce sufficient dissipation to handle shocks and other discontinuities.

- **Lax–Friedrichs Flux:** A simple and robust choice is the local Lax–Friedrichs flux, which for a scalar problem is $\widehat{f_n} = \{\boldsymbol{f}(u) \cdot \mathbf{n}\} + \frac{\lambda}{2} [u]$, where $\lambda$ is a [stabilization parameter](@entry_id:755311) related to the maximum characteristic speed. This flux is dissipative but easy to implement.

- **Approximate Riemann Solvers:** For systems like the Euler equations, more sophisticated fluxes based on approximate Riemann solvers are preferred . These solvers provide a more physically-based model of the wave interactions at element interfaces.
    - The **HLL (Harten-Lax-van Leer)** flux is a robust two-wave solver that uses estimates of the fastest left- and right-propagating wave speeds ($S_L, S_R$) to construct the flux. It is very diffusive at contact discontinuities, which is a drawback for resolving species concentration gradients.
    - The **HLLC (Harten-Lax-van Leer-Contact)** flux improves upon HLL by reintroducing the missing contact wave (traveling at speed $S_M$). This makes it much better at resolving contact discontinuities and is therefore highly recommended for multi-species [reactive flows](@entry_id:190684) where sharp resolution of composition is important.
    - The **Roe flux** is a linearized Riemann solver based on a special "Roe-averaged" state at the interface. For multicomponent ideal-gas mixtures, these averages are computed using $\sqrt{\rho}$-weighting for velocity, enthalpy, and species mass fractions (e.g., $\tilde{u} = (\sqrt{\rho_L}u_L + \sqrt{\rho_R}u_R) / (\sqrt{\rho_L} + \sqrt{\rho_R})$). The Roe solver sharply resolves all waves but may require an "[entropy fix](@entry_id:749021)" to prevent unphysical expansion shocks.

#### Discretization of Parabolic (Viscous) Terms

Discretizing second-order terms like viscosity and diffusion in DG is more complex than for first-order hyperbolic terms. A naive application of [integration by parts](@entry_id:136350) leads to an unstable scheme. Several methods have been developed to create stable and consistent discretizations.

One prominent approach is the **Bassi–Rebay 2 (BR2)** scheme . It achieves a symmetric and stable formulation for the diffusive operator $-\nabla \cdot (\kappa \nabla Y)$ by introducing **lifting operators**. A [lifting operator](@entry_id:751273), $\mathbf{r}_e$, takes the jump of the scalar solution, $[Y_h]$, on a face $e$ and "lifts" it into a vector-valued polynomial field supported on the two elements adjacent to that face. This lifted field serves as a correction to the gradient of the solution.

The BR2 scheme constructs a [bilinear form](@entry_id:140194) $a_{\text{BR2}}(Y_h, v_h)$ that contains three main parts:
1. The standard weak Laplacian term: $\sum_K \int_K \kappa \nabla Y_h \cdot \nabla v_h \, dV$.
2. Symmetric coupling terms on faces that connect the gradient of the solution to the jump of the test function, and vice-versa: $-\sum_e \int_e \kappa \{\nabla Y_h\} \cdot \mathbf{n}_e [v_h] \, dS - \sum_e \int_e \kappa \{\nabla v_h\} \cdot \mathbf{n}_e [Y_h] \, dS$.
3. A penalty term constructed from the lifted jumps: $\sum_e \eta_e \sum_{K \in \mathcal{N}(e)} \int_K \kappa \, \mathbf{r}_e([Y_h]) \cdot \mathbf{r}_e([v_h]) \, dV$.

This penalty term, which is a sum of volumetric inner products, is manifestly symmetric and, with a sufficiently large [penalty parameter](@entry_id:753318) $\eta_e$, provides the necessary stability (coercivity) for the entire scheme.

#### Handling Nonlinear Source Terms

The evaluation of the integral of the chemical source term, $\int_K \mathbf{S}(u_h) \varphi_h \, dV$, poses a unique challenge in DG methods. Since $u_h$ is a polynomial and the source $\mathbf{S}$ is typically a highly nonlinear function (e.g., a [rational function](@entry_id:270841) of polynomials due to Arrhenius kinetics), the integrand $\mathbf{S}(u_h) \varphi_h$ is not a polynomial. Therefore, it cannot be integrated exactly with standard Gaussian quadrature.

Using an insufficient number of quadrature points leads to **[aliasing error](@entry_id:637691)**, where high-frequency content in the integrand is incorrectly represented as low-frequency contributions, polluting the solution and potentially causing instability . For a [polynomial approximation](@entry_id:137391) of degree $p$ and a source term like $\omega(c)=c^2$, the integrand for the weak form can have a degree of $3p$. Standard quadrature with $p+1$ points is only exact up to degree $2p+1$, leading to significant error. For example, for $p=2$ with a source $\omega(c)=c^2$ and test function $\varphi=P_2(x)$, the [aliasing error](@entry_id:637691) from using 3-point Gauss quadrature can be explicitly calculated as $-27/175$.

Two common strategies to mitigate aliasing are:
1.  **Over-integration:** Use a higher number of quadrature points, $N_q$, sufficient to integrate the source term integrand exactly or with high accuracy. For a power-law source $\omega(c)=c^m$, the integrand has degree $(m+1)p$, requiring at least $N_q \ge ((m+1)p + 1)/2$ quadrature points.
2.  **Projection (De-aliasing):** Before computing the weak form integral, project the nonlinear term $\omega(u_h)$ onto the [polynomial space](@entry_id:269905) $\mathbb{P}_p$. The new integrand, being a product of two polynomials of degree $p$, has a maximum degree of $2p$. This can be integrated exactly using the standard $p+1$ quadrature points.

### The Lattice Boltzmann Method for Reactive Flows

The Lattice Boltzmann Method (LBM) offers an alternative to solving the macroscopic Navier-Stokes equations directly. It is a mesoscopic method derived from discrete kinetic theory, where the fluid is described by particle distribution functions $f_i$ that evolve on a discrete lattice.

#### Foundational Concepts: Lattices and Equilibria

The LBM discretizes [velocity space](@entry_id:181216) into a small set of vectors $\{\mathbf{c}_i\}$, for $i=1, \dots, Q$. For two-dimensional simulations, the **D2Q9 lattice** is standard. It consists of a particle at rest ($\mathbf{c}_0 = (0,0)$) and particles moving to nearest and next-nearest neighbors on a square grid: $\mathbf{c}_{1-4} = c(\pm 1, 0), c(0, \pm 1)$ and $\mathbf{c}_{5-8} = c(\pm 1, \pm 1)$, where $c = \Delta x/\Delta t$ is the lattice speed .

Associated with each velocity is a weight $w_i$. For D2Q9, these are $w_0=4/9$, $w_{1-4}=1/9$, and $w_{5-8}=1/36$. These weights and velocities are not arbitrary; they are carefully chosen as a [quadrature rule](@entry_id:175061) that correctly recovers the moments of the underlying continuous Maxwell-Boltzmann distribution up to a certain order. This property ensures that the macroscopic hydrodynamic equations (Navier-Stokes) are recovered in the low-Mach-number limit. A key consequence of this choice for the D2Q9 lattice is the relation between the lattice speed and the isothermal speed of sound, $c_s$: $c_s^2 = c^2/3$.

The core of the LBM is the evolution toward a local **[equilibrium distribution](@entry_id:263943) function**, $f_i^{\text{eq}}$. This function depends only on the local macroscopic properties (density $\rho$ and velocity $\mathbf{u}$). For low-Mach-number isothermal flows, it is derived by a second-order Taylor expansion of the Maxwell-Boltzmann distribution:

$$
f_i^{\text{eq}} = w_i \rho \left[ 1 + \frac{\mathbf{c}_i \cdot \mathbf{u}}{c_s^2} + \frac{(\mathbf{c}_i \cdot \mathbf{u})^2}{2 c_s^4} - \frac{\mathbf{u} \cdot \mathbf{u}}{2 c_s^2} \right]
$$

Macroscopic quantities are recovered as moments of the distribution functions: $\rho = \sum_i f_i$ and $\rho\mathbf{u} = \sum_i \mathbf{c}_i f_i$. The form of $f_i^{\text{eq}}$ is constructed precisely so that its moments recover the desired macroscopic equilibrium state (i.e., $\sum_i f_i^{\text{eq}}=\rho$, $\sum_i \mathbf{c}_i f_i^{\text{eq}}=\rho\mathbf{u}$, and $\sum_i \mathbf{c}_i \otimes \mathbf{c}_i f_i^{\text{eq}} = \rho\mathbf{u} \otimes \mathbf{u} + p\mathbf{I}$).

#### The LBM Algorithm and Source Terms

The LBM algorithm consists of two main steps performed at each time step $\Delta t$:
1.  **Streaming:** The particle populations $f_i$ move to adjacent lattice nodes according to their discrete velocities: $f_i(\mathbf{x}+\mathbf{c}_i \Delta t, t+\Delta t) = f_i^*(\mathbf{x}, t)$, where $f_i^*$ is the post-collision distribution.
2.  **Collision:** At each node, the populations relax toward the local equilibrium $f_i^{\text{eq}}$. The simplest and most common model is the Bhatnagar-Gross-Krook (BGK) operator, which assumes a linear relaxation process with a single relaxation time $\tau$:
    $$f_i^*(\mathbf{x}, t) = f_i(\mathbf{x}, t) - \frac{1}{\tau} [f_i(\mathbf{x}, t) - f_i^{\text{eq}}(\mathbf{x}, t)]$$

To simulate [reactive flows](@entry_id:190684), source terms must be added to this algorithm. For example, to model heat release in a thermal LBM, a source term must be designed at the kinetic level to correctly reproduce the macroscopic heat source $\dot{Q}$ . A simple explicit source term added to the LBM equation is only first-order accurate in time. To achieve second-order accuracy, a more sophisticated formulation, such as the **Guo-type forcing scheme**, is required. This involves defining a kinetic source $\Phi_i$ that satisfies the correct moment constraints (e.g., $\sum_i \Phi_i = \dot{Q}$ and $\sum_i \mathbf{c}_i \Phi_i = \mathbf{0}$ for an isotropic energy source) and applying a correction factor of $(1 - \frac{1}{2\tau})$ to the source term in the collision step. This precisely cancels the leading-order error term that arises from the explicit discretization.

#### Coupling LBM with Stiff Chemistry

The issue of [chemical stiffness](@entry_id:1122356) is as critical for LBM as it is for DG. An explicit treatment of the chemical source term in the LBM equation imposes a severe stability constraint $\Delta t \ll \tau_{\text{chem}}$. Since LBM is typically used for low-Mach-number flows where the flow timescale is large, this constraint is untenable.

The [standard solution](@entry_id:183092) is **operator splitting**. The evolution over one time step $\Delta t$ is split into a transport step (solved by LBM) and a reaction step (a system of stiff ODEs solved at each lattice node). To maintain stability, the reaction step must be solved with a stiff ODE solver, such as an implicit method (e.g., implicit Euler) that is stable for time steps much larger than $\tau_{\text{chem}}$.

For global second-order accuracy, a symmetric splitting scheme like **Strang splitting** is necessary:
1.  Perform a half-step of transport (e.g., LBM for $\Delta t/2$).
2.  Perform a full step of reaction (solve the reaction ODEs over $\Delta t$).
3.  Perform the second half-step of transport (LBM for $\Delta t/2$).

This combination of LBM for transport, Strang splitting for coupling, and an implicit solver for chemistry provides a robust and accurate framework for simulating stiff [reactive flows](@entry_id:190684).