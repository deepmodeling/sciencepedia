## Introduction
The numerical simulation of plasma flows is a cornerstone of modern [computational fusion science](@entry_id:1122784), but it presents a significant challenge. Governed by [hyperbolic conservation laws](@entry_id:147752) like the [magnetohydrodynamics](@entry_id:264274) (MHD) equations, these flows often feature shocks and sharp discontinuities. Traditional numerical methods face a fundamental trade-off: [high-order schemes](@entry_id:750306) produce unphysical oscillations near these features, while low-order schemes excessively smear them out. This article introduces the Flux-Corrected Transport (FCT) method, a pioneering nonlinear technique designed specifically to resolve this conflict. By adaptively blending the stability of a low-order scheme with the accuracy of a high-order one, FCT provides robust and precise solutions for complex plasma phenomena. This text will guide you through the FCT framework, beginning with the fundamental **Principles and Mechanisms** that overcome the limitations of linear schemes. We will then explore its diverse **Applications and Interdisciplinary Connections** in high-fidelity MHD simulations and [multi-physics modeling](@entry_id:1128279). Finally, a series of **Hands-On Practices** will provide concrete exercises to reinforce these advanced computational concepts.

## Principles and Mechanisms

The accurate numerical simulation of plasma flows, particularly in the context of magnetic fusion energy research, presents a formidable challenge. These flows are governed by systems of [hyperbolic conservation laws](@entry_id:147752), such as the equations of magnetohydrodynamics (MHD), which admit discontinuous solutions like shocks and [contact discontinuities](@entry_id:747781). A central difficulty in designing numerical methods for these systems is the inherent conflict between accuracy and stability. High-order linear schemes, while accurate in smooth regions, tend to produce unphysical, [spurious oscillations](@entry_id:152404) near steep gradients (a manifestation of the Gibbs phenomenon). Conversely, low-order linear schemes can suppress these oscillations but at the cost of excessive numerical diffusion, which smears out important physical features.

This chapter delves into the principles and mechanisms of Flux-Corrected Transport (FCT), a foundational and powerful technique designed to navigate this dilemma. FCT constructs a nonlinear, hybrid scheme that adaptively combines the best attributes of both low- and [high-order methods](@entry_id:165413), yielding a method that is high-order accurate in smooth regions of the flow while remaining robust and non-oscillatory at discontinuities.

### The Order Barrier and the Necessity of Nonlinearity

To appreciate the motivation behind FCT, let us first consider the simplest relevant model: the one-dimensional [linear advection](@entry_id:636928) of a scalar quantity $u(x,t)$, such as the density of a plasma species along a magnetic field line, with a constant velocity $a > 0$. The governing equation is a conservation law:

$$
\frac{\partial u}{\partial t} + a \frac{\partial u}{\partial x} = 0
$$

A simple, explicit finite-volume scheme on a uniform grid with cell width $\Delta x$ and time step $\Delta t$ can be written as $u_i^{n+1} = \sum_{j} c_{ij} u_j^n$. A desirable property for such a scheme is **[monotonicity](@entry_id:143760)**, which means it is order-preserving: if one initial data set is pointwise greater than or equal to another ($u^n \ge v^n$), then the solution after one time step preserves this ordering ($u^{n+1} \ge v^{n+1}$). This property forbids the creation of new maxima or minima in the solution, thereby preventing spurious oscillations. A linear scheme of the form above is monotone if and only if all its coefficients are non-negative ($c_{ij} \ge 0$) and, for consistency, sum to one ($\sum_j c_{ij} = 1$). Such a scheme is a convex averaging operator and is guaranteed to satisfy a **[discrete maximum principle](@entry_id:748510) (DMP)**, where the updated value $u_i^{n+1}$ is bounded by the minimum and maximum of the values in its stencil at the previous time step .

The [first-order upwind scheme](@entry_id:749417) is a canonical example of a monotone scheme. For $a > 0$, its update formula is:

$$
u_i^{n+1} = u_i^n - \frac{a \Delta t}{\Delta x} (u_i^n - u_{i-1}^n) = (1 - \lambda) u_i^n + \lambda u_{i-1}^n
$$

where $\lambda = a \Delta t / \Delta x$ is the Courant number. The coefficients are $1-\lambda$ and $\lambda$. They are non-negative, and thus the scheme is monotone, if and only if the Courant-Friedrichs-Lewy (CFL) condition $0 \le \lambda \le 1$ is satisfied. This scheme is robust but highly diffusive.

In contrast, a second-order linear scheme like the Lax-Wendroff method can be shown to have at least one negative coefficient for any Courant number $\lambda \in (0, 1)$, and it is therefore not monotone. While it accurately represents smooth waves, it produces pronounced oscillations near sharp gradients.

This dichotomy is not a coincidence; it is a fundamental limitation of linear schemes, formalized by **Godunov's Theorem**. The theorem states that any linear monotone scheme for the [linear advection equation](@entry_id:146245) can be at most first-order accurate. This order barrier forces us to abandon linearity to achieve our goal. Methods that are both high-order accurate and non-oscillatory must be inherently **nonlinear**, meaning their effective coefficients depend on the solution itself. FCT is a pioneering approach to constructing such a scheme .

### The Flux-Corrected Transport Paradigm

The core idea of FCT is to blend a low-order, monotone (but diffusive) numerical flux, denoted $F^L$, with a high-order, accurate (but potentially oscillatory) numerical flux, $F^H$. The blending is done in a conservative and locally controlled manner.

The general, one-dimensional conservative finite-volume update for a cell average $u_i$ is:

$$
u_i^{n+1} = u_i^n - \frac{\Delta t}{\Delta x} \left( F_{i+1/2} - F_{i-1/2} \right)
$$

The brilliance of FCT lies in its construction of the final [numerical flux](@entry_id:145174), $F_{i+1/2}$. The procedure, originally conceived by Boris and Book, can be described in a few conceptual steps :

1.  **Define Low- and High-Order Fluxes**: First, one must define two consistent [numerical fluxes](@entry_id:752791) at each cell interface $x_{i+1/2}$.
    -   $F^L_{i+1/2}$: A low-order flux that guarantees [monotonicity](@entry_id:143760) and positivity under an appropriate CFL condition. The first-order [upwind flux](@entry_id:143931) is a common choice. Another is the Local Lax-Friedrichs (or Rusanov) flux, which has the form $F^L_{i+1/2} = \frac{1}{2}(f(u_i) + f(u_{i+1})) - \frac{1}{2}\lambda_{\max}(u_{i+1} - u_i)$, where $\lambda_{\max}$ is a local [wave speed](@entry_id:186208) estimate . The second term represents [artificial diffusion](@entry_id:637299).
    -   $F^H_{i+1/2}$: A high-order flux that provides better accuracy in smooth regions. This could be, for example, a Lax-Wendroff flux or a flux derived from a [higher-order reconstruction](@entry_id:750332) of the data (e.g., using MUSCL techniques). For the candidate flux to be able to recover high-order accuracy, it must be consistent with the physical flux and be based on a reconstruction that is at least second-order accurate in smooth regions .

2.  **Define Antidiffusive Flux**: The difference between the high- and low-order fluxes is defined as the **antidiffusive flux**:

    $$
    A_{i+1/2} = F^H_{i+1/2} - F^L_{i+1/2}
    $$
    
    This quantity represents the [artificial diffusion](@entry_id:637299) inherent in the low-order flux. If this antidiffusive flux were applied fully, it would cancel the artificial diffusion of $F^L$ and recover the high-order scheme $F^H$. For this structure to work, the high-order update must be expressible as the low-order update plus a sum of these antidiffusive interface flux corrections .

3.  **Limit the Antidiffusive Flux**: This is the crucial "flux correction" step. The raw antidiffusive flux is multiplied by a **limiter coefficient** $\alpha_{i+1/2}$, which takes values in $[0, 1]$.

    $$
    A^C_{i+1/2} = \alpha_{i+1/2} A_{i+1/2}
    $$
    
    The limiter $\alpha_{i+1/2}$ is calculated based on the local solution profile to ensure that the application of the corrected antidiffusive flux $A^C$ does not create new extrema. If $\alpha_{i+1/2} = 1$, the scheme is locally high-order. If $\alpha_{i+1/2} = 0$, the scheme locally reverts to the robust low-order method.

4.  **Apply the Corrected Flux**: The final numerical flux is a convex combination of the low- and high-order fluxes: $F_{i+1/2} = F^L_{i+1/2} + A^C_{i+1/2}$. The full time-step update can be written as a two-stage process: first, compute a temporary low-order solution, then apply the limited antidiffusive correction. Combining these into a single update gives the canonical FCT formula:

    $$
    u_i^{n+1} = \left( u_i^n - \frac{\Delta t}{\Delta x} \left( F^L_{i+1/2} - F^L_{i-1/2} \right) \right) - \frac{\Delta t}{\Delta x} \left( \alpha_{i+1/2} A_{i+1/2} - \alpha_{i-1/2} A_{i-1/2} \right)
    $$
    
    This formulation is manifestly **conservative**. The update for each cell is written as a difference of fluxes at its boundaries. When summed over the entire domain, the internal fluxes cancel in a [telescoping sum](@entry_id:262349), ensuring that the total amount of the quantity $u$ is conserved. This property is essential for capturing the correct physics of discontinuous flows, as it ensures that the numerical solution, if it converges, will satisfy the correct Rankine-Hugoniot jump conditions governing the speed and strength of shocks . For complex systems like ideal MHD, only a fully conservative formulation for mass, momentum, and total energy can guarantee correct shock speeds . FCT is designed to preserve this vital property .

### The Limiter Mechanism: A Closer Look

The nonlinear intelligence of FCT resides entirely within the limiter. The most influential and general limiter is that developed by Zalesak, which works for multiple dimensions and unstructured grids. Its logic is based on ensuring that the antidiffusive step does not push the solution outside of local bounds.

Let's dissect the limiter mechanism in detail  :

1.  **Compute a Low-Order Solution**: First, a provisional solution is computed using only the low-order monotone flux, $F^L$. Let's call this $u_i^*$.
    
    $$
    u_i^* = u_i^n - \frac{\Delta t}{\Delta x} (F^L_{i+1/2} - F^L_{i-1/2})
    $$
    
    Because $F^L$ is monotone, if the initial data $u^n$ is positive, the provisional solution $u^*$ will also be positive (under the appropriate CFL condition).

2.  **Define Local Bounds**: The goal is to ensure the final solution $u_i^{n+1}$ does not create new extrema relative to its neighbors. The bounds are therefore defined based on the local neighborhood of the provisional solution $u^*$:
    
    $$
    u_i^{\max} = \max(u_{i-1}^*, u_i^*, u_{i+1}^*)
    $$
    $$
    u_i^{\min} = \min(u_{i-1}^*, u_i^*, u_{i+1}^*)
    $$
    
    It is critical that these bounds are computed from $u^*$, not from the original data $u^n$. The antidiffusive step is correcting $u^*$, so the bounds must be relevant to it .

3.  **Calculate Cell Capacities**: For each cell $i$, we determine the maximum possible increase ($P_i^+$) and decrease ($P_i^-$) it can tolerate without violating the local bounds:
    
    $$
    P_i^+ = u_i^{\max} - u_i^* \quad (\ge 0)
    $$
    $$
    P_i^- = u_i^* - u_i^{\min} \quad (\ge 0)
    $$

4.  **Sum Raw Antidiffusive Fluxes**: For each cell $i$, we sum up all the "raw" (unlimited) antidiffusive fluxes that would enter or leave it. This gives the total potential increase ($Q_i^+$) and total potential decrease ($Q_i^-$) for the cell. In 1D:
    
    $$
    Q_i^+ = \max \left(0, \frac{\Delta t}{\Delta x} A_{i-1/2} \right) - \min \left(0, \frac{\Delta t}{\Delta x} A_{i+1/2} \right)
    $$
    $$
    Q_i^- = \max \left(0, -\frac{\Delta t}{\Delta x} A_{i-1/2} \right) - \min \left(0, -\frac{\Delta t}{\Delta x} A_{i+1/2} \right)
    $$
    
    This generalizes to multiple dimensions by summing over all faces of a cell .

5.  **Compute Nodal Correction Factors**: We compute the fraction of the total incoming/outgoing raw antidiffusive flux that is permissible for each cell:
    
    $$
    R_i^+ = \min \left(1, \frac{P_i^+}{Q_i^+} \right) \quad \text{if } Q_i^+ > 0, \text{ else } 1
    $$
    $$
    R_i^- = \min \left(1, \frac{P_i^-}{Q_i^-} \right) \quad \text{if } Q_i^- > 0, \text{ else } 1
    $$

6.  **Limit Each Flux**: The final, crucial step is to limit each individual antidiffusive flux $A_{i+1/2}$. This flux acts as a donor to one cell and a receiver to another. To maintain conservation, the amount of antidiffusion must be acceptable to *both*. Therefore, the flux is limited by the more restrictive of the two relevant correction factors. For a flux $A_{i+1/2}$ that, if positive, transports quantity from cell $i$ to cell $i+1$:
    
    -   It depletes cell $i$, so it is limited by $R_i^-$.
    -   It fills cell $i+1$, so it is limited by $R_{i+1}^+$.
    
    The limited flux is thus $A^C_{i+1/2} = A_{i+1/2} \times \min(R_i^-, R_{i+1}^+)$. A general formula for the limited flux between any two neighboring cells $i$ and $j$, $A_{ij}$, can be written as :
    
    $$
    A_{ij}^{\mathrm{lim}} = \begin{cases} A_{ij} \min(R_i^{-}, R_j^{+})  &\text{if } A_{ij} > 0 \\ A_{ij} \min(R_i^{+}, R_j^{-})  &\text{if } A_{ij} < 0 \\ 0  &\text{if } A_{ij} = 0 \end{cases}
    $$
    
    Here, $A_{ij} > 0$ denotes a flux from cell $i$ to cell $j$. This careful, symmetric limiting process guarantees that the final update $u_i^{n+1} = u_i^* + \delta_i$ (where $\delta_i$ is the net limited antidiffusive increment) will satisfy the [discrete maximum principle](@entry_id:748510) and, as a consequence, preserve positivity if the low-order solution $u^*$ is positive  .

### Extensions and Practical Considerations

#### Application to Systems and Characteristic Limiting

When applying FCT to a system of coupled conservation laws, such as the equations of ideal MHD, simply limiting each equation's antidiffusive flux independently is generally incorrect. This would ignore the physical coupling between the [conserved variables](@entry_id:747720) (e.g., mass, momentum, and energy).

The physically correct approach is to perform the limiting process in **characteristic space**. At each cell interface, the system is locally linearized (for example, using a Roe average state). This [diagonalization](@entry_id:147016) of the flux Jacobian reveals the local wave structure of the system: a set of characteristic waves, each with a corresponding propagation speed (eigenvalue) and polarization (eigenvector). The limiting procedure is then as follows :

1.  At a given interface, compute the vector of raw antidiffusive fluxes, $\mathbf{A}$.
2.  Project this vector onto the basis of right eigenvectors of the local Jacobian. This yields a set of scalar antidiffusive wave strengths, one for each characteristic field.
3.  Apply a scalar FCT limiter (like the one described above) to each of these scalar wave strengths independently.
4.  Reconstruct the final, limited antidiffusive flux vector, $\mathbf{A}^C$, by multiplying the limited scalar strengths by their corresponding eigenvectors and summing the results.

This process ensures that the corrections applied to the solution are consistent with the physical wave propagation of the system. For instance, in an isothermal plasma flow described by density and momentum, a correction to a sound wave is properly projected onto changes in both density and momentum .

#### Time Integration and Stability

FCT is a [spatial discretization](@entry_id:172158). For the full scheme, it must be coupled with a [time integration](@entry_id:170891) method. For explicit methods, stability is governed by a CFL condition. A key property of FCT is that its stability is determined by the underlying low-order scheme. For an advection equation discretized with a first-order [upwind flux](@entry_id:143931), the forward Euler time-stepping method is stable and positivity-preserving for a Courant number $\lambda = |a|\Delta t/\Delta x \le 1$ .

For higher-order accuracy in time, one can employ multi-stage Runge-Kutta methods. A particularly suitable class of methods are the **Strongly Stability Preserving (SSP)** schemes. An SSP method can be written as a convex combination of forward Euler steps. This structure guarantees that if the forward Euler step is stable under a certain property (e.g., positivity, Total Variation Diminishing (TVD), or the DMP) for a time step $\Delta t_{FE}$, the full multi-stage SSP scheme will also preserve that property for a time step $\Delta t \le C_{SSP} \Delta t_{FE}$. The constant $C_{SSP}$ is the "SSP coefficient" of the method.

A popular choice is the third-order, three-stage SSPRK(3,3) method, which has an SSP coefficient of $C_{SSP}=1$. When used with an FCT [spatial discretization](@entry_id:172158) (which is designed to be DMP- and TVD-preserving), the entire scheme remains stable and bound-preserving under the same CFL condition as the simple forward-Euler upwind scheme, i.e., $\Delta t \le \Delta x/|a|$ .

#### Multidimensional FCT

In two or more dimensions, FCT can be implemented using an **unsplit** update, where fluxes from all directions are considered simultaneously. As alluded to earlier, the Zalesak limiter is naturally suited for this. When computing the total potential increase ($Q_{i,j}^+$) and decrease ($Q_{i,j}^-$) for a cell $(i,j)$, one must sum the raw antidiffusive contributions from *all* its faces (e.g., four faces in 2D Cartesian geometry). The subsequent calculation of nodal correction factors $R^\pm_{i,j}$ and the symmetric limiting of each face flux proceeds as in the 1D case. This unsplit approach is generally more isotropic and accurate for multidimensional flows than operator-splitting (directional splitting) approaches .

By adhering to these principles—conservative formulation, nonlinear blending via limited antidiffusion, and respecting system physics through [characteristic decomposition](@entry_id:747276)—Flux-Corrected Transport provides a robust and widely applicable framework for simulating complex plasma flows with sharp features.