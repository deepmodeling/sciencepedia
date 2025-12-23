## Introduction
The numerical simulation of reacting flows, such as those in combustion engines and chemical reactors, presents a formidable challenge in computational fluid dynamics (CFD). A central difficulty, particularly in the low-Mach-number regime typical of many combustion processes, is the intricate coupling between the velocity field and the pressure field. Unlike high-speed flows where pressure is directly tied to density through an equation of state, the pressure in low-speed flows acts as a mechanical constraint to ensure the conservation of mass. This subtle but critical role creates a numerical obstacle that [standard solution](@entry_id:183092) algorithms struggle to overcome.

To address this knowledge gap, a family of robust numerical methods known as the Semi-Implicit Method for Pressure-Linked Equations (SIMPLE) was developed. These algorithms provide an effective framework for resolving the [pressure-velocity coupling](@entry_id:155962) and have become a cornerstone of modern CFD. This article offers a comprehensive exploration of the SIMPLE family of algorithms tailored for reacting flows. Over the next three chapters, you will gain a deep understanding of these powerful techniques.

We will begin by exploring the **Principles and Mechanisms** of pressure correction, deriving the governing equations and the core predictor-corrector procedure. Next, in **Applications and Interdisciplinary Connections**, we will examine how these methods are extended to tackle real-world complexities like turbulence, buoyancy, and [multiphysics coupling](@entry_id:171389). Finally, the **Hands-On Practices** section will provide you with practical problems to solidify your understanding of the algorithm's stability, accuracy, and implementation. Our journey starts with the foundational theory that underpins this entire class of solvers.

## Principles and Mechanisms

In the numerical simulation of [reacting flows](@entry_id:1130631), particularly at low Mach numbers, the coupling between pressure and velocity presents a unique and central challenge. Unlike in high-speed, fully compressible flows where density is a direct function of pressure and an equation of state provides a direct link, in low-Mach-number flows, the role of pressure is more subtle. This chapter delineates the fundamental principles governing this coupling and describes the mechanisms of the Semi-Implicit Method for Pressure-Linked Equations (SIMPLE) family of algorithms, which were developed to resolve this challenge.

### Governing Equations for Low-Mach-Number Reacting Flows

To understand the pressure-velocity coupling problem, we must first establish the system of governing equations. For a multicomponent, reacting gas mixture in the low-Mach-number limit, we can write the conservation laws in a form that separates the thermodynamic and hydrodynamic effects. Here, the pressure $p(\mathbf{x}, t)$ is decomposed into a spatially uniform thermodynamic background pressure, $p_0(t)$, and a small hydrodynamic pressure perturbation, $\pi(\mathbf{x}, t)$, such that $p(\mathbf{x}, t) = p_0(t) + \pi(\mathbf{x}, t)$. The governing equations, derived from the fundamental principles of conservation of mass, momentum, species, and energy, are as follows :

**Mixture Mass Continuity:**
The total mass of the mixture is conserved. As chemical reactions rearrange atoms but do not create or destroy mass, the net mass production rate from chemistry is zero. The continuity equation is:
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) = 0
$$
where $\rho$ is the mixture density and $\mathbf{u}$ is the fluid velocity vector.

**Species Transport:**
For each of the $N_s$ species in the mixture, its mass is conserved subject to transport by convection and diffusion, and production or destruction by chemical reactions:
$$
\frac{\partial (\rho Y_k)}{\partial t} + \nabla \cdot (\rho \mathbf{u} Y_k) = -\nabla \cdot \mathbf{J}_k + \dot{\omega}_k, \quad k=1, \dots, N_s
$$
Here, $Y_k$ is the [mass fraction](@entry_id:161575) of species $k$, $\mathbf{J}_k$ is its diffusive mass flux, and $\dot{\omega}_k$ is its net mass production rate from chemical reactions. These terms must satisfy the constraints $\sum_{k=1}^{N_s} \mathbf{J}_k = \mathbf{0}$ and $\sum_{k=1}^{N_s} \dot{\omega}_k = 0$, ensuring consistency with total mass conservation .

**Momentum Conservation:**
The momentum equation expresses Newton's second law for a fluid element. Under the low-Mach-number approximation, the pressure gradient term is driven solely by the [hydrodynamic pressure](@entry_id:1126255) perturbation $\pi$:
$$
\frac{\partial (\rho \mathbf{u})}{\partial t} + \nabla \cdot (\rho \mathbf{u} \mathbf{u}) = -\nabla \pi + \nabla \cdot \boldsymbol{\tau} + \rho \mathbf{g}
$$
where $\boldsymbol{\tau}$ is the [viscous stress](@entry_id:261328) tensor and $\mathbf{g}$ is the [body force](@entry_id:184443) per unit mass. For a Newtonian fluid, $\boldsymbol{\tau} = \mu \left[ \nabla \mathbf{u} + (\nabla \mathbf{u})^{\top} \right] - \frac{2}{3} \mu (\nabla \cdot \mathbf{u}) \mathbf{I}$.

**Sensible Enthalpy Transport:**
An [energy equation](@entry_id:156281) is required to determine the temperature field. A common form is the transport equation for sensible enthalpy, $h_s = \sum_k Y_k h_{s,k}(T)$:
$$
\frac{\partial (\rho h_s)}{\partial t} + \nabla \cdot (\rho \mathbf{u} h_s) = \frac{d p_0}{d t} + \nabla \cdot (\lambda \nabla T) - \nabla \cdot \left( \sum_{k=1}^{N_s} h_{s,k} \mathbf{J}_k \right) + \Phi + \dot{q}_{chem}
$$
Here, $\lambda$ is the thermal conductivity, $\Phi = \boldsymbol{\tau} : \nabla \mathbf{u}$ is the viscous dissipation, and the term $\frac{dp_0}{dt}$ represents work done by the evolving background pressure. The [chemical heat release](@entry_id:1122340), $\dot{q}_{chem}$, is often implicitly included by using total enthalpies in the diffusion and source terms. For instance, a common formulation replaces the explicit heat release with source and diffusion terms derived from total species enthalpies .

**Equation of State:**
Finally, an equation of state relates the [thermodynamic variables](@entry_id:160587). For an [ideal gas mixture](@entry_id:149212), density depends on the background pressure, temperature $T$, and the local composition (via the mixture molecular weight $W_{\text{mix}}$):
$$
\rho = \frac{p_0 W_{\text{mix}}}{R_u T}, \quad \text{where} \quad W_{\text{mix}} = \left( \sum_{k=1}^{N_s} \frac{Y_k}{W_k} \right)^{-1}
$$
where $R_u$ is the [universal gas constant](@entry_id:136843) and $W_k$ is the molecular weight of species $k$ .

### The Dual Role of Pressure: Thermodynamic versus Hydrodynamic

A critical feature of the low-Mach-number formulation is that the [hydrodynamic pressure](@entry_id:1126255) $\pi$ does not appear in the equation of state. Its value is not determined by local thermodynamics. Instead, its role is purely mechanical: **the hydrodynamic pressure field adjusts itself globally to ensure that the resulting velocity field satisfies the mass continuity equation at all points in space and time** .

The momentum equation only contains the gradient of pressure, $\nabla \pi$. This means the momentum equation, by itself, cannot determine the absolute value of pressure. More importantly, if we were to solve the momentum equation for velocity using a guessed pressure field, there is no guarantee that the resulting velocity field would satisfy the continuity equation, $\nabla \cdot (\rho \mathbf{u}) = -\frac{\partial \rho}{\partial t}$. This incompatibility lies at the heart of the pressure-velocity coupling problem. The pressure field acts as a Lagrange multiplier to enforce the kinematic constraint of mass conservation.

### Derivation of the Pressure-Correction Equation

Pressure-based segregated solvers, such as the SIMPLE family, address this coupling through a **predictor-corrector** procedure. The general idea is to split the process into two stages:

1.  **Prediction:** A provisional or "predicted" velocity field, $\mathbf{u}^*$, is computed by solving the discretized momentum equation using a pressure field from the previous iteration or time step, $p^*$. This velocity field, $\mathbf{u}^*$, will generally not conserve mass.

2.  **Correction:** A correction for the pressure, $p'$, is sought such that the corrected velocity field, $\mathbf{u} = \mathbf{u}^* + \mathbf{u}'$, satisfies the continuity equation. The velocity correction, $\mathbf{u}'$, is related to the pressure correction, $p'$, through the momentum equation.

Let's formalize this. The discrete momentum equation relates the velocity correction to the [pressure correction](@entry_id:753714). A simplified form of this relationship is:
$$
\mathbf{u} = \mathbf{u}^* - d \nabla p'
$$
where $d$ is a coefficient representing the influence of the pressure gradient on the velocity, derived from the momentum equation discretization. The continuity equation that the final velocity field must satisfy is:
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) = 0
$$
Substituting the expression for the corrected velocity $\mathbf{u}$ into this equation gives:
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot \left( \rho (\mathbf{u}^* - d \nabla p') \right) = 0
$$
Rearranging to solve for the unknown [pressure correction](@entry_id:753714) $p'$ yields a Poisson-type equation:
$$
\nabla \cdot (\rho d \nabla p') = \nabla \cdot (\rho \mathbf{u}^*) + \frac{\partial \rho}{\partial t}
$$
The right-hand side represents the **mass imbalance** or **mass residual** of the predicted field. It is the amount by which the predicted fluxes and density evolution fail to satisfy continuity. The solution of this [elliptic equation](@entry_id:748938) provides a pressure correction field $p'$ that, when used to correct the velocity, drives this mass imbalance to zero .

### The Elliptic Nature of the Pressure Constraint

The pressure-correction equation is fundamentally **elliptic**. This is true for both constant-density incompressible flow and for variable-density low-Mach-number flow . In the constant-density case, $\rho$ is constant and $\partial \rho / \partial t = 0$, simplifying the equation to $\nabla \cdot (d \nabla p') = \nabla \cdot \mathbf{u}^*$, a classic Poisson equation.

In the variable-density [reacting flow](@entry_id:754105) case, the equation is $\nabla \cdot (\rho d \nabla p') = \nabla \cdot (\rho \mathbf{u}^*) + \frac{\partial \rho}{\partial t}$. Although a time derivative, $\partial \rho / \partial t$, appears, it does not act on the unknown variable $p'$. In the low-Mach-number framework, density $\rho$ is a function of temperature and composition, not pressure. Therefore, when solving for $p'$ at a given instant, the term $\partial \rho / \partial t$ is treated as a known source term, calculated from the solution of the energy and species equations. The [differential operator](@entry_id:202628) acting on $p'$ remains $\nabla \cdot (\rho d \nabla(\cdot))$, which is an [elliptic operator](@entry_id:191407).

The elliptic nature implies that the value of the pressure correction $p'$ at any point is influenced by the mass imbalance sources and boundary conditions throughout the entire domain. This reflects the physical reality of low-Mach-number flows, where pressure signals propagate effectively instantaneously (at the speed of sound, which is considered infinite in this limit), establishing a global balance to ensure mass conservation.

### The SIMPLE Family of Algorithms

The SIMPLE, SIMPLEC, and SIMPLER algorithms are all based on the predictor-corrector framework but differ in their specific approximations of the velocity correction, leading to variations in stability and convergence speed .

Let the discretized momentum equation for a cell $P$ be written abstractly as $a_P \mathbf{u}_P = \sum_{N} a_N \mathbf{u}_N + \mathbf{H}_P - V_P \nabla p_P$, where $a_P$ and $a_N$ are coefficients from the discretization of transient, convective, and diffusive terms. The exact relation for the velocity correction $\mathbf{u}'$ is $a_P \mathbf{u}'_P = \sum_{N} a_N \mathbf{u}'_N - V_P \nabla p'_P$.

#### The SIMPLE Algorithm

The original **SIMPLE** algorithm makes the most significant approximation by neglecting the influence of neighboring velocity corrections ($\sum_N a_N \mathbf{u}'_N$). This yields a simple, local relationship:
$$
\mathbf{u}'_P \approx - \frac{V_P}{a_P} \nabla p'_P
$$
This approximation leads to a pressure-correction equation that tends to over-predict the correction, necessitating small [under-relaxation](@entry_id:756302) factors for pressure to maintain stability. The pressure-velocity coupling is relatively weak.

#### The SIMPLEC Algorithm

The **SIMPLEC** (SIMPLE-Consistent) algorithm provides a more accurate approximation. It accounts for the neighbor velocity corrections by assuming $\mathbf{u}'_N \approx \mathbf{u}'_P$. This leads to the relation:
$$
\mathbf{u}'_P \approx - \frac{V_P}{a_P - \sum_N a_N} \nabla p'_P
$$
Since $a_P - \sum_N a_N \le a_P$, the velocity correction in SIMPLEC is larger for the same pressure gradient, implying a **stronger pressure-velocity coupling**. This often allows for faster convergence and larger under-relaxation factors.

#### The SIMPLER Algorithm

The **SIMPLER** (SIMPLE-Revised) algorithm takes a different approach. Instead of solving for a pressure *correction*, it solves for the pressure *field* itself.
1.  A "pseudo-velocity" field $\hat{\mathbf{u}}$ is first calculated from the momentum equation with the pressure gradient term omitted.
2.  A pressure equation is then constructed by substituting a velocity expression derived from $\hat{\mathbf{u}}$ into the continuity equation. This yields a Poisson equation for the full pressure field $p$, where the source term is based on the fluxes of the pseudo-velocity field.
3.  Once the pressure field $p$ is obtained, it is used to solve the full momentum equations for the final, mass-conserving velocity field.

SIMPLER provides the strongest coupling as it uses a more physically complete velocity field to construct the pressure equation, typically resulting in a more accurate pressure field in a single step.

### Coupling Challenges in Reacting Flows

The standard SIMPLE framework must be carefully adapted to handle the strong, nonlinear couplings inherent in reacting flows.

#### Strong Coupling of Flow and Thermochemistry

In [reacting flows](@entry_id:1130631), density is a strong function of temperature and composition: $\rho = \rho(T, \{Y_k\})$. The energy and species equations, which determine $T$ and $\{Y_k\}$, contain advection terms ($\rho \mathbf{u}$) and source terms ($\dot{\omega}_k$) that depend on the flow and [thermodynamic state](@entry_id:200783). This creates a tight, two-way feedback loop:
- The flow field transports scalars ($T, Y_k$).
- The [scalar fields](@entry_id:151443), through chemical reaction and heat release, alter the temperature and composition.
- These changes alter the density, $\rho$.
- The change in density directly impacts the continuity and momentum equations, altering the flow field.

A robust algorithm must handle this coupling correctly. Specifically, when solving the [scalar transport](@entry_id:150360) equations, it is crucial to use a mass-conserving velocity field. Using the non-conservative predicted velocity $\mathbf{u}^*$ for scalar advection would violate the fundamental conservation laws for species and energy  .

#### Treatment of the Transient Density Term

For transient simulations, the temporal derivative $\partial \rho / \partial t$ in the pressure-correction equation source term presents a numerical challenge . Discretized as $(\rho^{n+1} - \rho^n)/\Delta t$, the new-time density $\rho^{n+1}$ depends on the yet-unknown $T^{n+1}$ and $\{Y_k\}^{n+1}$.
- **Lagged Treatment:** One can treat this term explicitly, using a density value from a previous iteration or the previous time step. This approach is simpler but can become unstable if density changes rapidly, as is common during ignition or in sharp flame fronts. It is suitable only for small time steps or weak heat release.
- **Iterated Treatment:** A more robust approach is to iterate within the time step. After an initial pressure-velocity correction, the scalar equations are solved to find new values for $T$ and $\{Y_k\}$. Density is then updated, and the pressure-correction step is repeated to enforce mass conservation with the new density. This iterative process, characteristic of PISO-like algorithms, is essential for stability and accuracy in stiff [reacting flow](@entry_id:754105) problems.

### A Complete Algorithmic Cycle for Reacting Flows

A single time step of a robust, segregated pressure-correction algorithm for a transient, variable-density reacting flow typically proceeds as follows :

1.  **Initialize:** Start with the known solution fields ($\rho^n, \mathbf{u}^n, p^n, T^n, Y_k^n$) at time $t^n$.

2.  **Momentum Prediction:** Solve the discretized momentum equations using the old pressure $p^n$ and density $\rho^n$ to obtain the predicted velocity field $\mathbf{u}^*$.

3.  **First Pressure Correction:** Construct and solve the pressure-correction equation using the mass imbalance from the predicted fluxes and the old density $\rho^n$. This yields an intermediate corrected pressure $p^{(1)}$ and a mass-conserving velocity field $\mathbf{u}^{(1)}$ (which satisfies continuity for density $\rho^n$).

4.  **Scalar Transport:** Solve the species transport and energy equations to obtain the new temperature $T^{n+1}$ and mass fractions $\{Y_k\}^{n+1}$. **Crucially, the advective fluxes in these equations must be computed using the mass-conserving field $\mathbf{u}^{(1)}$** to ensure conservation of species and energy.

5.  **Density Update:** Update the density field to $\rho^{n+1}$ using the new [scalar fields](@entry_id:151443) $T^{n+1}$, $\{Y_k\}^{n+1}$ and the equation of state.

6.  **Second Pressure Correction (Optional but Recommended):** The velocity field $\mathbf{u}^{(1)}$ is no longer consistent with the new density field $\rho^{n+1}$. To enforce the full transient continuity equation, $\partial\rho/\partial t + \nabla \cdot (\rho \mathbf{u}) = 0$, a second pressure correction must be performed. A new mass residual is calculated using $\mathbf{u}^{(1)}$ and the density change $(\rho^{n+1} - \rho^n)/\Delta t$. Solving a second pressure-correction equation yields the final end-of-step fields $p^{n+1}$ and $\mathbf{u}^{n+1}$. For highly stiff problems, this outer loop (Steps 3-6) may be repeated several times.

### The Imperative of Discrete Mass Conservation

The entire pressure-correction machinery exists to enforce the discrete mass continuity equation in each and every control volume of the computational mesh . For a [finite volume](@entry_id:749401) $V_P$, the discrete mass balance reads:
$$
\frac{(\rho_P^{n+1} - \rho_P^n)V_P}{\Delta t} + \sum_{f \in \partial P} \dot{m}_f^{n+1} = 0
$$
where $\dot{m}_f$ are the face mass fluxes. The goal of the pressure-correction step is to adjust the fluxes such that the mass residual, i.e., the left-hand side of the equation, is driven to zero (within a tolerance).

Failure to enforce this constraint, due to an inconsistent algorithm or numerical errors, has severe physical consequences. A non-zero mass residual acts as a spurious local source or sink of mass. In a flame simulation, this unphysical dilatation will distort the velocity field, alter the balance between heat release and thermal expansion, and ultimately lead to incorrect predictions of flame speed, structure, and stability. On [collocated grids](@entry_id:1122659), this inconsistency can also trigger non-physical, checkerboard-like oscillations in the pressure field, further degrading the solution. Therefore, the rigorous and consistent implementation of a pressure-correction algorithm is not merely a numerical detail but a prerequisite for the physically meaningful simulation of reacting flows.