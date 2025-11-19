## Introduction
The numerical simulation of [incompressible fluid](@entry_id:262924) flow presents a formidable challenge centered on the intricate relationship between pressure and velocity. Unlike [compressible flows](@entry_id:747589), where an [equation of state](@entry_id:141675) directly links thermodynamic properties, pressure in an [incompressible fluid](@entry_id:262924) emerges as a mathematical constraint to ensure a [divergence-free velocity](@entry_id:192418) field. This phenomenon, known as [pressure-velocity coupling](@entry_id:155962), requires specialized [numerical algorithms](@entry_id:752770) to resolve. This article provides a graduate-level examination of the two most foundational and widely used pressure-correction methods in [computational fluid dynamics](@entry_id:142614) (CFD): the SIMPLE (Semi-Implicit Method for Pressure-Linked Equations) and PISO (Pressure-Implicit with Splitting of Operators) algorithms.

This article systematically demystifies these powerful techniques across three chapters. In "Principles and Mechanisms," we will delve into the mathematical nature of pressure in incompressible flow, explore [discretization](@entry_id:145012) strategies like staggered and collocated grids, and detail the step-by-step procedures of the SIMPLE and PISO algorithms. Following this, "Applications and Interdisciplinary Connections" will bridge theory and practice by discussing algorithm selection for steady versus transient flows and examining how these methods are coupled with advanced physical models for turbulence, [buoyancy](@entry_id:138985), and variable density. Finally, "Hands-On Practices" offers a series of guided exercises designed to solidify your understanding of the core concepts, from deriving the pressure-correction equation to implementing boundary conditions.

## Principles and Mechanisms

The numerical simulation of incompressible fluid flow presents a unique set of challenges that distinguish it from the simulation of [compressible flows](@entry_id:747589). The core of this challenge lies in the intricate relationship between the velocity and pressure fields, a phenomenon known as **[pressure-velocity coupling](@entry_id:155962)**. This chapter elucidates the fundamental principles governing this coupling and details the mechanisms of the seminal algorithms developed to address it, namely the SIMPLE and PISO methods.

### The Nature of Pressure in Incompressible Flow

In the mathematical description of [incompressible flow](@entry_id:140301), governed by the Navier-Stokes equations, there is no explicit, independent equation for pressure, such as an [equation of state](@entry_id:141675) that links pressure to density and temperature. Instead, the pressure field emerges as a mathematical necessity to enforce the kinematic [constraint of incompressibility](@entry_id:190758). The [continuity equation](@entry_id:145242) for a constant-density fluid,

$$
\nabla \cdot \mathbf{u} = 0
$$

is a [divergence-free constraint](@entry_id:748603) on the velocity field $\mathbf{u}$. From a physical standpoint, pressure gradients are the forces that accelerate fluid elements. From a mathematical viewpoint, pressure acts as a **Lagrange multiplier**. It is a scalar field that dynamically adjusts itself at every point in space and time to ensure that the resulting velocity field remains divergence-free [@problem_id:2516608].

To understand the nature of this coupling, consider the [momentum equation](@entry_id:197225) for an incompressible Newtonian fluid:

$$
\rho \left( \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla)\mathbf{u} \right) = -\nabla p + \mu \nabla^2 \mathbf{u} + \mathbf{f}
$$

where $\rho$ is the constant density, $\mu$ is the [dynamic viscosity](@entry_id:268228), $p$ is the pressure, and $\mathbf{f}$ represents body forces. If we take the divergence of this entire equation and apply the incompressibility constraint $\nabla \cdot \mathbf{u} = 0$ (and assume constant viscosity), the unsteady and viscous terms vanish, i.e., $\nabla \cdot (\partial_t \mathbf{u}) = \partial_t (\nabla \cdot \mathbf{u}) = 0$. This manipulation yields a **Poisson equation for pressure**:

$$
\nabla^2 p = -\rho \nabla \cdot ((\mathbf{u} \cdot \nabla)\mathbf{u}) + \nabla \cdot \mathbf{f}
$$

The Laplacian operator $\nabla^2$ is an **[elliptic operator](@entry_id:191407)**. A key property of [elliptic equations](@entry_id:141616) is that the solution at any point in the domain depends on the source terms and boundary conditions over the entire domain simultaneously. This means that a change in the flow field anywhere in the domain has an instantaneous effect on the pressure field everywhere. This global, implicit dependence is the mathematical root of the [pressure-velocity coupling](@entry_id:155962) problem [@problem_id:2516608].

A final important characteristic of pressure in [incompressible flow](@entry_id:140301) is that only its gradient, $\nabla p$, appears in the [momentum equation](@entry_id:197225). This implies that if a pressure field $p(\mathbf{x}, t)$ is a solution, then so is $p(\mathbf{x}, t) + C$ for any arbitrary constant $C$. The [absolute pressure](@entry_id:144445) level is undetermined. When discretized, this manifests as a singular linear system for the pressure. To obtain a unique solution, the pressure must be fixed at a single reference point or cell in the computational domain [@problem_id:2516608].

### Discretization Strategies and Numerical Artifacts

In the Finite Volume Method (FVM), the choice of where to store the discrete variables (pressure and velocity components) on the computational grid has profound consequences.

#### Staggered vs. Collocated Grids

The original and most robust solution to the [pressure-velocity coupling](@entry_id:155962) problem at the [discretization](@entry_id:145012) level is the **[staggered grid](@entry_id:147661)**. In this arrangement, scalar quantities like pressure are stored at the center of a [control volume](@entry_id:143882), while vector components (velocities) are stored at the centers of the faces of the [control volume](@entry_id:143882) [@problem_id:2516606]. For instance, the $x$-velocity component would be stored on the faces perpendicular to the $x$-axis.

The [staggered grid](@entry_id:147661)'s primary advantage is that it provides a naturally strong and direct coupling between pressure and velocity. When the [momentum equation](@entry_id:197225) for a face-centered velocity is discretized, the pressure gradient term is naturally approximated using the two adjacent cell-center pressures. This creates a direct link between the velocity at a face and the pressure difference across it. When these face velocities are used in the discrete [continuity equation](@entry_id:145242), the resulting equation for pressure robustly couples adjacent pressure nodes, naturally suppressing spurious oscillations [@problem_id:2516606] [@problem_id:2516595].

Despite its robustness, the [staggered grid](@entry_id:147661) arrangement becomes complex to implement for unstructured grids or complex geometries. This has led to the widespread adoption of the **[collocated grid](@entry_id:175200)**, where all variables—pressure and all velocity components—are stored at the same location, typically the cell center. While simplifying the data structure, this arrangement introduces a significant numerical challenge known as **[pressure-velocity decoupling](@entry_id:167545)** or **[checkerboarding](@entry_id:747311)** [@problem_id:2516608].

This decoupling arises because simple linear interpolation of cell-center velocities to the faces can make the discrete continuity equation insensitive to a high-frequency, non-physical "checkerboard" pressure field. For example, a pressure field that alternates between high and low values at adjacent cell centers can produce a near-zero pressure gradient at the cell faces, thus satisfying the discrete [momentum equation](@entry_id:197225) for a zero-velocity field. Such a solution is physically meaningless but is admitted by the naive numerical scheme [@problem_id:2516606].

#### The Rhie-Chow Interpolation

To overcome the [checkerboarding](@entry_id:747311) problem on collocated grids, a special momentum-weighted interpolation technique is required. The most famous and widely used of these is the **Rhie-Chow interpolation** [@problem_id:2516606]. The core idea is to construct the velocity at a [control volume](@entry_id:143882) face not by simply interpolating the cell-center velocities, but by interpolating the [momentum equation](@entry_id:197225) itself. This re-introduces the strong [pressure coupling](@entry_id:753717) that was lost.

Consider a 1D [collocated grid](@entry_id:175200). The discretized [momentum equation](@entry_id:197225) at a cell center $P$ can be written as $a_P u_P = \sum_{nb} a_{nb} u_{nb} + S_u + (\nabla p)_P \Delta V_P$. This can be rearranged to express the velocity $u_P$ in terms of a pseudo-velocity $\hat{u}_P$ (which groups all terms except the pressure gradient) and the pressure gradient itself:

$$
u_P = \hat{u}_P - d_P (\nabla p)_P
$$

where $d_P$ is related to the inverse of the main diagonal coefficient $a_P$. A simple linear interpolation of $u_P$ and $u_E$ to the face 'e' between them leads to [decoupling](@entry_id:160890). The Rhie-Chow method instead computes the face velocity $u_e$ as:

$$
u_e = \overline{\hat{u}}_e - \overline{d}_e (\nabla p)_e
$$

Here, the overbar $\overline{(\cdot)}$ denotes interpolation to the face. The crucial step is that the pressure gradient term $(\nabla p)_e$ is not interpolated, but is computed directly using the adjacent cell-center pressures, e.g., $(p_E - p_P)/\Delta x$. This introduces a term proportional to the pressure difference between adjacent cells directly into the face velocity expression, effectively adding a numerical pressure dissipation that [damps](@entry_id:143944) high-frequency oscillations and mimics the favorable properties of the [staggered grid](@entry_id:147661) [@problem_id:2516548] [@problem_id:2516595].

### The SIMPLE Algorithm

For a given grid arrangement (typically collocated with Rhie-Chow interpolation), an iterative algorithm is needed to solve the coupled system of non-linear algebraic equations. The **Semi-Implicit Method for Pressure-Linked Equations (SIMPLE)**, proposed by Patankar and Spalding, is the canonical iterative [predictor-corrector algorithm](@entry_id:753695).

The SIMPLE algorithm proceeds through the following sequence of steps within each iteration [@problem_id:2516552]:

1.  **Guess the Pressure Field:** Start with an initial guess for the pressure field, $p^*$.

2.  **Momentum Predictor:** Solve the discretized momentum equations using the guessed pressure field $p^*$ to obtain a provisional, or "predicted," [velocity field](@entry_id:271461), $\mathbf{u}^*$.
    $$
    A(\mathbf{u}^*) \mathbf{u}^* = \mathbf{b} - G p^*
    $$
    Here, $A(\mathbf{u}^*)$ is the momentum matrix, $\mathbf{b}$ contains source and neighbor terms, and $G$ is the [discrete gradient](@entry_id:171970) operator. Because $\mathbf{u}^*$ is computed with an incorrect pressure field, it will not satisfy the [continuity equation](@entry_id:145242), i.e., $D \mathbf{u}^* \neq 0$, where $D$ is the discrete [divergence operator](@entry_id:265975) [@problem_id:2516561].

3.  **Pressure-Correction Equation:** The goal is to find corrections for pressure, $p'$, and velocity, $\mathbf{u}'$, such that the final fields $\mathbf{u} = \mathbf{u}^* + \mathbf{u}'$ and $p = p^* + p'$ satisfy the governing equations. The key approximation of the SIMPLE algorithm is to relate the velocity correction directly to the pressure-correction gradient by simplifying the [momentum equation](@entry_id:197225) for the corrections, neglecting the influence of neighboring velocity corrections. This yields a local, explicit relationship [@problem_id:2516561]:
    $$
    \mathbf{u}' \approx - \mathbf{D} \nabla p'
    $$
    where $\mathbf{D}$ is a tensor constructed from the inverse of the main diagonal coefficients of the momentum matrix $A$. By enforcing that the corrected velocity field must satisfy continuity, $\nabla \cdot (\mathbf{u}^* + \mathbf{u}') = 0$, we substitute the expression for $\mathbf{u}'$ to obtain a Poisson-like equation for the [pressure correction](@entry_id:753714) $p'$:
    $$
    \nabla \cdot (\mathbf{D} \nabla p') = \nabla \cdot \mathbf{u}^*
    $$
    The source term for this equation is the divergence of the predicted [velocity field](@entry_id:271461), which represents the local mass imbalance that needs to be corrected [@problem_id:2516605]. For impermeable solid walls, the appropriate boundary condition for the [pressure correction](@entry_id:753714) is a zero-gradient (homogeneous Neumann) condition, $\partial p' / \partial n = 0$ [@problem_id:2516561].

4.  **Update and Relaxation:** Once the pressure-correction equation is solved for $p'$, the pressure and velocity fields are updated. Due to the approximations made, applying the full correction can lead to oscillatory divergence. To stabilize the iteration, **[under-relaxation](@entry_id:756302)** is crucial. The pressure is updated as:
    $$
    p^{k+1} = p^k + \alpha_p p'
    $$
    where $p^k$ is the pressure from the previous iteration and $\alpha_p$ is the pressure [under-relaxation](@entry_id:756302) factor, typically between $0.3$ and $0.8$. The velocity field is also corrected to satisfy continuity and is typically under-relaxed implicitly when solving the momentum equations in the next iteration's predictor step [@problem_id:2516561] [@problem_id:2516552].

This iterative cycle is repeated until convergence. Robust **convergence criteria** include ensuring that the residuals of all solved equations (mass, momentum, etc.) fall below a small tolerance, that global conservation laws are satisfied (e.g., mass entering the domain equals mass leaving), and that monitored quantities of interest (like drag or total heat transfer) become stationary [@problem_id:2516552].

The choice of [under-relaxation](@entry_id:756302) factors significantly impacts convergence. There often exists an optimal velocity [under-relaxation](@entry_id:756302) factor $\alpha_u$; choosing a value that is too small can severely slow convergence by weakening the [pressure-velocity coupling](@entry_id:155962) mechanism and inhibiting the damping of low-frequency, continuity-dominated error modes [@problem_id:2516586].

### Advanced Algorithms: PISO and Other SIMPLE Variants

The basic SIMPLE algorithm has inspired several enhancements designed to improve its robustness and efficiency.

#### SIMPLEC and SIMPLER

The **SIMPLEC (SIMPLE-Consistent)** algorithm modifies the velocity-correction relationship ($\mathbf{u}' \approx - \mathbf{D} \nabla p'$) to be more "consistent" with the [momentum equation](@entry_id:197225) by accounting for the influence of neighbor velocity corrections in an approximate way. This often leads to a slightly better pressure-correction equation and can accelerate convergence, allowing for larger [under-relaxation](@entry_id:756302) factors [@problem_id:2516549].

The **SIMPLER (SIMPLE-Revised)** algorithm takes a different approach. In each iteration, it first solves a pressure equation (derived by omitting the pressure gradient from the momentum equation) to obtain a better pressure field. This revised pressure is then used to solve the momentum equations. A final velocity-correction step (without a pressure update) is performed to ensure the [velocity field](@entry_id:271461) is divergence-free at the end of the iteration. The main benefit is that the momentum equations are solved with a more accurate pressure field, which can improve the overall stability and robustness of the solution process [@problem_id:2516549].

#### The PISO Algorithm

The **Pressure-Implicit with Splitting of Operators (PISO)** algorithm is an extension of SIMPLE primarily developed for transient (unsteady) simulations. Its main distinguishing feature is the inclusion of one or more additional corrector steps within a single time step [@problem_id:2516563] [@problem_id:2516595].

The PISO procedure within one time step is as follows:
1.  **Momentum Predictor:** Same as in SIMPLE, a provisional velocity $\mathbf{u}^*$ is computed using the pressure from the previous time step.
2.  **First Corrector:** A pressure-correction equation is solved for $p'$, and the pressure and velocity are updated to $p^*$ and $\mathbf{u}^{**}$. This is identical to the correction step in SIMPLE.
3.  **Second (and subsequent) Corrector(s):** PISO performs a second correction. A new pressure-correction equation is formed based on the once-corrected [velocity field](@entry_id:271461) $\mathbf{u}^{**}$ and solved for a second [pressure correction](@entry_id:753714), $p''$. This is then used to correct the velocity field again.

The efficiency of PISO comes from the "Splitting of Operators" concept. The expensive assembly and solution of the full momentum matrix system is performed only once in the predictor step. The subsequent corrector steps are computationally cheap because they reuse the main diagonal of the (now frozen) momentum matrix to relate velocity corrections to pressure-gradient corrections [@problem_id:2516563].

These additional corrector steps provide a much tighter approximation of the true [pressure-velocity coupling](@entry_id:155962) (formally, a better approximation to the inverse of the discrete Schur complement operator). This enhanced coupling allows PISO to take larger, stable time steps in transient simulations, often without requiring any [under-relaxation](@entry_id:756302) ($\alpha_p \approx 1$) or inner iterations within the time step [@problem_id:2516586]. It is crucial to note, however, that while PISO addresses stability related to the pressure-wave propagation, it does not remove the Courant-Friedrichs-Lewy (CFL) stability restriction associated with the explicit treatment of advection terms [@problem_id:2516595] [@problem_id:2516563].