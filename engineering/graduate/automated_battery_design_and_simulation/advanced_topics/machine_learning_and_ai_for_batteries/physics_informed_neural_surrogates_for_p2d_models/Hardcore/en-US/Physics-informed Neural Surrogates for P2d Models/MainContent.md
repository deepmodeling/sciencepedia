## Introduction
The pseudo-two-dimensional (P2D) model, pioneered by John Newman, stands as a cornerstone of lithium-ion battery simulation, offering high-fidelity insights into the complex electrochemical processes that govern cell performance. However, its computational intensity poses a significant bottleneck, hindering its use in applications that require rapid iteration, such as design optimization, real-time control, and extensive lifetime prediction studies. This gap between physical fidelity and computational tractability has motivated the development of a new class of models: physics-informed neural surrogates. By integrating the governing differential equations directly into the training process of neural networks, these surrogates learn to approximate the P2D model's behavior with the accuracy of a physics-based model but at a fraction of the computational cost.

This article provides a comprehensive overview of this powerful methodology. Across three chapters, you will gain a deep understanding of how to build, apply, and validate these advanced models. The journey begins in the "Principles and Mechanisms" chapter, which lays the theoretical foundation, detailing how the P2D model is framed as a system of partial differential equations and how physics-informed neural networks are constructed to solve them. Next, "Applications and Interdisciplinary Connections" explores the transformative impact of these surrogates on engineering workflows, from accelerating design optimization and parameter estimation to enabling reinforcement learning for advanced battery control. Finally, the "Hands-On Practices" section offers concrete exercises to translate theory into practice, guiding you through the implementation of these cutting-edge techniques.

## Principles and Mechanisms

The development of physics-informed neural surrogates for complex multiphysics systems, such as the pseudo-two-dimensional (P2D) model of a lithium-ion battery, rests on a synthesis of electrochemical engineering, numerical analysis, and machine learning. This chapter elucidates the core principles and mechanisms that enable neural networks to not only approximate the solutions of the governing partial differential equations (PDEs) but also to learn the underlying solution operator, paving the way for accelerated simulation and design. We will begin by formally establishing the P2D model as a system of coupled PDEs, then detail how physics-informed neural networks (PINNs) are constructed to solve this system, and finally, explore the advanced paradigms of operator learning and the critical challenge of parameter identifiability.

### The Pseudo-Two-Dimensional Model as a Coupled PDE System

The P2D model, pioneered by John Newman and his collaborators, offers a high-fidelity description of a lithium-ion cell by coupling transport phenomena across multiple domains and scales. To construct a physics-informed surrogate, we must first have a precise mathematical representation of this model. The model's state is described by a set of coupled fields that evolve in time and space.

Consider a one-dimensional cell sandwich structure along the through-thickness coordinate $x$, comprising a negative electrode ($x \in [0, L_n]$), a separator ($x \in [L_n, L_n + L_s]$), and a positive electrode ($x \in [L_n + L_s, L]$). The "pseudo-two-dimensional" nature arises from resolving lithium concentration gradients within spherical active material particles, which have an internal radial coordinate $r \in [0, R_s(x)]$, at each macroscopic point $x$ within the electrodes. The fundamental state variables and their domains are defined as follows [@problem_id:3941043]:

*   **Electrolyte-phase concentration, $c_e(x,t)$, and potential, $\phi_e(x,t)$**: These variables describe the state of the liquid electrolyte, which permeates the porous structure of the entire cell. They are therefore defined across all three subdomains, for all $x \in [0, L]$.

*   **Solid-phase potential, $\phi_s(x,t)$**: This variable describes the electric potential within the electronically conductive solid matrix of the electrodes. It is defined only where this solid phase exists, i.e., in the negative and positive electrodes, for $x \in [0, L_n]$ and $x \in [L_n + L_s, L]$. It is undefined in the electronically insulating separator.

*   **Solid-phase lithium concentration, $c_s(r,x,t)$**: This variable describes the concentration of intercalated lithium inside the active material particles. It is defined on the microscopic radial coordinate $r$ within particles located at each macroscopic position $x$ in the electrodes. Thus, its domain is $r \in [0, R_s(x)]$ for $x$ in the electrodes.

These disparate fields are coupled through the **interfacial molar flux**, $j(x,t)$, which represents the rate of lithium ions leaving the solid particles and entering the electrolyte at a given position $x$ and time $t$. This flux is non-zero only within the electrodes. The coupling is enforced by fundamental conservation laws:

1.  **Conservation of Mass**: The flux of lithium at the surface of a particle is dictated by the interfacial reaction. This is expressed as a Neumann boundary condition on the solid-phase diffusion equation: $-D_s(x) \frac{\partial c_s}{\partial r}\big|_{r=R_s(x)} = j(x,t)$, where $D_s$ is the solid diffusion coefficient. Due to spherical symmetry, the flux at the particle center is zero: $\frac{\partial c_s}{\partial r}\big|_{r=0} = 0$.

2.  **Conservation of Charge**: The electrochemical reaction is a transfer of charge between the solid and electrolyte phases. The total charge must be conserved. This means that the divergence of the electronic current, $i_s$, in the solid phase must be equal and opposite to the divergence of the ionic current, $i_e$, in the electrolyte phase. This relationship is mediated by the interfacial flux:
    $$ \nabla \cdot i_s(x,t) = -a_s(x) F j(x,t) $$
    $$ \nabla \cdot i_e(x,t) = +a_s(x) F j(x,t) $$
    where $a_s(x)$ is the specific interfacial area and $F$ is the Faraday constant. The sum of these divergences is zero, $\nabla \cdot (i_s + i_e) = 0$, enforcing total current conservation at every point.

A physics-informed surrogate must be architected to respect these distinct domains and intricate coupling mechanisms.

### Physics-Informed Neural Networks for the P2D Model

A Physics-Informed Neural Network (PINN) is a neural network trained to solve a system of PDEs by minimizing a loss function that penalizes deviations from the governing laws. Instead of being trained solely on data, a PINN is trained to satisfy the physics itself.

For the P2D model, we define neural networks that take coordinates as inputs and approximate the state variables as outputs, for example, $\hat{c}_e(x,t; \theta) \approx c_e(x,t)$. The key innovation is the use of **automatic differentiation (AD)** to compute the exact derivatives of the network's outputs with respect to its inputs (e.g., $\partial \hat{c}_e / \partial t$, $\partial^2 \hat{c}_e / \partial x^2$) [@problem_id:3941019]. These derivatives are then substituted into the governing PDEs to form **residuals**, which are functions that should be zero if the equation is satisfied.

The PINN loss function, $\mathcal{L}_{\text{total}}$, is the sum of the mean squared errors of these residuals evaluated at a large number of random points (collocation points) in the spatiotemporal domain, plus terms for boundary and initial conditions [@problem_id:3926924]:
$$ \mathcal{L}_{\text{total}} = \mathcal{L}_{\text{PDE}} + \mathcal{L}_{\text{BC}} + \mathcal{L}_{\text{IC}} $$

The PDE loss, $\mathcal{L}_{\text{PDE}}$, includes terms for each governing equation. For instance, the residuals for the primary P2D equations are:
*   **Solid Diffusion Residual ($r_s$)**: This penalizes violations of Fick's second law in spherical coordinates within the particles.
    $$r_s = \frac{\partial c_s}{\partial t} - D_s \frac{1}{r^2}\frac{\partial}{\partial r}\left(r^2\frac{\partial c_s}{\partial r}\right)$$
*   **Electrolyte Transport Residual ($r_e$)**: This enforces mass balance in the electrolyte, accounting for diffusion and generation from reactions.
    $$r_e = \varepsilon \frac{\partial c_e}{\partial t} - \frac{\partial}{\partial x}\left(D_e^{\text{eff}}\frac{\partial c_e}{\partial x}\right) - \frac{1 - t_+^0}{F}a_s j$$
*   **Charge Balance Residuals ($r_{\phi_s}, r_{\phi_e}$)**: These enforce charge conservation in the solid and electrolyte phases.
    $$ r_{\phi_s} = \frac{\partial}{\partial x}\left(-\sigma_s^{\text{eff}}\frac{\partial \phi_s}{\partial x}\right) + a_s F j $$
    $$ r_{\phi_e} = \frac{\partial}{\partial x}\left(-\kappa_e^{\text{eff}}\frac{\partial \phi_e}{\partial x} + 2\kappa_e^{\text{eff}}\frac{RT}{F}(1 - t_+^0)\frac{\partial \ln c_e}{\partial x}\right) - a_s F j $$
Here, $\varepsilon$ is porosity, $t_+^0$ is the transference number, and the `eff` superscript denotes effective properties in the porous medium. The PINN is trained by finding the network parameters $\theta$ that minimize the sum of the squared values of these residuals over all collocation points.

The computational backbone of this process is automatic differentiation. AD applies the chain rule algorithmically to the sequence of elementary operations within the neural network, yielding exact derivatives without incurring the truncation errors of finite difference methods. First derivatives (gradients) are efficiently computed using a single reverse-mode AD pass (backpropagation). Second-order derivatives, such as those in the diffusion equations, are computed via nested AD, for example, by applying AD to the output of a first-derivative computation [@problem_id:3941019]. Modern AD frameworks implement highly efficient methods, such as forward-over-reverse AD for Hessian-vector products, which allow for the computation of second-derivative terms with memory complexity that scales linearly with the network size and batch size, i.e., $\mathcal{O}(S \cdot B)$, where $S$ is activations per sample and $B$ is batch size. This makes the training of PINNs for complex models like P2D computationally feasible.

### Enforcing Boundary Conditions by Architectural Design

The boundary condition loss, $\mathcal{L}_{\text{BC}}$, is typically formulated by adding penalty terms for any mismatch at the boundaries (soft constraints). However, this approach can lead to slow convergence and inaccurate enforcement. A more elegant and robust method is to enforce boundary conditions by architectural design, creating so-called **hard-constrained** networks.

The core idea is to construct a trial solution, $\hat{f}(x; \theta)$, that satisfies the boundary conditions for *any* choice of the neural network's parameters $\theta$. This is achieved by combining the unconstrained output of a neural network, $N(x; \theta)$, with auxiliary functions.

#### Dirichlet Boundary Conditions

For a **Dirichlet boundary condition**, which specifies the value of the function at the boundary (e.g., $\phi_s(0)=V_-$ and $\phi_s(L)=V_+$), the trial solution can be formulated as the sum of a simple function that already satisfies the conditions and a neural network term that is guaranteed to be zero at the boundaries [@problem_id:3941047]. A common construction is:
$$ \hat{\phi}_s(x; \theta) = \left( V_- + (V_+ - V_-)\frac{x}{L} \right) + x(L-x)N_s(x; \theta) $$
The first term is a linear interpolation that matches the boundary values exactly. The second term multiplies the raw network output $N_s(x; \theta)$ by a **boundary distance function**, $d(x)=x(L-x)$, which is zero at $x=0$ and $x=L$. This structure ensures that $\hat{\phi}_s(0) = V_-$ and $\hat{\phi}_s(L) = V_+$ by construction, irrespective of the output of $N_s$. The network is then free to learn the complex interior behavior of the solution.

#### Neumann Boundary Conditions

For **Neumann boundary conditions**, which specify the derivative of the function at the boundary, a different trial solution is required. Consider the boundary conditions for solid-phase diffusion in a particle: a symmetry condition, $\frac{\partial c_s}{\partial r}(0,t) = 0$, and a surface flux condition, $-D_s\frac{\partial c_s}{\partial r}(R_p,t) = j_s(t)$. A trial solution for $c_s(r,t)$ can be constructed to satisfy these derivative constraints exactly [@problem_id:3941089]:
$$ \hat{c}_s(r,t; \theta) = A(r,t) + g(r) N_s(r,t; \theta) $$
Here, $A(r,t)$ is a function whose derivative satisfies the inhomogeneous boundary conditions (e.g., $A(r,t) = - \frac{j_s(t)}{2 R_p D_s} r^2$), and $g(r)$ is a construction function whose derivative is zero at the boundaries, ensuring the neural network term does not violate the conditions. A suitable choice is $g(r)=r^2(R_p-r)^2$, which has double roots at both $r=0$ and $r=R_p$, making both $g(r)$ and its derivative zero at the boundaries. This architectural enforcement transforms the constrained optimization problem into an unconstrained one, often leading to more stable and accurate training.

### From Solving to Emulating: The Role of Operator Learning

While a PINN can effectively solve the P2D equations for a *single* set of parameters and inputs, the goal of automated design and simulation requires rapid evaluation across a vast space of possible designs and operating conditions. Training a new PINN for each case is computationally prohibitive. This motivates a shift in perspective: from learning a single solution function to learning the **solution operator** itself [@problem_id:3940624].

A neural operator, such as a DeepONet or Fourier Neural Operator (FNO), is a network trained to approximate the mapping $\mathcal{G}$ from input functions and parameters to solution functions. For the P2D model, this operator can be formally defined as [@problem_id:3941024]:
$$ \mathcal{G}: (I(t), T(t), \theta_{\text{design}}) \mapsto (V(t), c_s, c_e, \phi_s, \phi_e) $$
This operator maps an input current profile $I(t)$, temperature profile $T(t)$, and a vector of design parameters $\theta_{\text{design}}$ (e.g., electrode thickness, porosity) to the output voltage function $V(t)$ and the full internal state fields.

The need for operator learning is deeply rooted in the physical and mathematical structure of the P2D model [@problem_id:3926889]. The governing equations are non-local. For instance, the potential $\phi_s(x,t)$ at a single point $x$ depends on the reaction current $j(y,t)$ over the entire electrode domain $y \in [0,L]$ due to the elliptic nature of the charge balance equation. Similarly, the concentration $c_s(r;x,t)$ depends on the entire history of the current, $I(\tau)$ for $\tau \in [0,t]$, due to the parabolic nature of the diffusion equation. Simple models like pointwise regression, which map local inputs to local outputs, are fundamentally incapable of capturing these non-local spatial and temporal dependencies. Furthermore, operator learning is better suited to respect global integral constraints, such as the total reaction current integrating to the applied cell current, $I(t) = A F \int_0^L a_s(x) j(x,t) dx$.

By training on a dataset of input-output function pairs generated by a high-fidelity solver, a neural operator learns a generalized surrogate. Once trained, it can predict the entire spatiotemporal solution for a new, unseen input function in a single forward pass, achieving speedups of several orders of magnitude. This "amortized inference" is what makes neural operators transformative for design optimization, uncertainty quantification, and real-time control.

### The Challenge of Parameter Identifiability

A key application of physics-informed surrogates is **parameter estimation**, where the goal is to identify unknown physical parameters (e.g., diffusion coefficients, reaction rates) by fitting the model's output to experimental data. A fundamental prerequisite for this task is **structural identifiability**: the property of a model that, in principle, allows for the unique determination of its parameters from perfect, noise-free input-output data [@problem_id:3941071]. If different parameter combinations produce the exact same observable output, the parameters are structurally unidentifiable.

For the P2D model, when only terminal voltage $V(t)$ and current $I(t)$ are measured, not all parameters are structurally identifiable. For example:
*   The solid-phase diffusion coefficient ($D_s$) and the kinetic rate constant ($k$) are generally **identifiable** because they govern processes with distinct timescales that leave different signatures on the voltage curve.
*   The electrolyte conductivity ($\kappa$) is also **identifiable** as it primarily determines the instantaneous ohmic drop at the start of a current pulse.
*   However, the electrolyte diffusion coefficient ($D_e$) and the transference number ($t_+^0$) are notoriously **unidentifiable** from voltage data alone. Their effects on the concentration polarization part of the voltage are coupled, with the voltage response being sensitive to the combination $(1 - t_+^0)^2/D_e$.

This non-identifiability can be demonstrated with a concrete counterexample. Consider the effective properties in the porous electrode, which are often modeled using a Bruggeman relation involving a tortuosity exponent $b$, e.g., $D_{e,\text{eff}} = D_e \varepsilon^b$. If we assume the ohmic drop is negligible, the voltage response is determined by the concentration profile, which is governed by $D_{e,\text{eff}}$. One can construct a transformation where the tracer diffusivity $D_e$ is scaled by a factor $\lambda$ and the exponent $b$ is adjusted such that the effective diffusivity $D_{e,\text{eff}}$ remains invariant [@problem_id:3941084]. Specifically, the parameter sets $(D_e, b)$ and $(\lambda D_e, b + \frac{\ln(1/\lambda)}{\ln \varepsilon})$ will produce identical voltage outputs, making them indistinguishable.

Resolving such ambiguities requires introducing additional, independent physical measurements that break the symmetry. For the $D_e$-$b$ ambiguity, one could use a three-electrode cell or high-frequency Electrochemical Impedance Spectroscopy (EIS) to independently measure the effective electrolyte conductivity, $\kappa_{\text{eff}} = \kappa \varepsilon^b$. Since $\kappa_{\text{eff}}$ depends on $b$ but not $D_e$, this measurement allows for the unique determination of $b$, which in turn allows $D_e$ to be uniquely identified from the voltage data. This highlights a crucial synergy: physics-informed models not only accelerate simulation but also guide experimental design for robust parameterization.