## Introduction
The [numerical simulation](@entry_id:137087) of [hyperbolic conservation laws](@entry_id:147752), which govern phenomena from supersonic gas flow to [tsunami propagation](@entry_id:203810), presents a significant computational challenge. At the heart of modern [finite volume methods](@entry_id:749402) for these equations lies the Riemann problem—a local, idealized discontinuity that dictates the flow of information between computational cells. While exact solutions to the Riemann problem provide maximum accuracy, their complexity motivates the development of simpler, more efficient, and highly robust alternatives. The Harten–Lax–van Leer (HLL) solver stands out as one of the most fundamental and widely used approximate Riemann solvers, prized for its stability and straightforward implementation. This article provides a comprehensive exploration of this pivotal numerical tool.

This article will guide you through the theory, application, and practice of the HLL solver. In "Principles and Mechanisms," we will derive the solver from the first principles of conservation laws, explore its mathematical properties, and discuss its strengths and inherent limitations. Following this, "Applications and Interdisciplinary Connections" will showcase the remarkable versatility of the HLL scheme, demonstrating its use in [computational fluid dynamics](@entry_id:142614), [geophysics](@entry_id:147342), astrophysics, and even non-traditional fields like crowd dynamics. Finally, "Hands-On Practices" will offer a series of targeted problems designed to solidify your understanding and provide practical experience in applying the HLL method to canonical fluid dynamics problems.

## Principles and Mechanisms

The formulation of a numerical scheme for [hyperbolic conservation laws](@entry_id:147752) hinges upon the accurate and stable computation of fluxes at the interfaces between computational cells. As established in the "Introduction" chapter, the Godunov method provides a foundational framework by proposing that this numerical flux should be determined by solving a local Riemann problem at each interface. While an exact Riemann solver yields the most accurate flux (the Godunov flux), its complexity, particularly for systems like the Euler equations, motivates the development of approximate Riemann solvers. The Harten–Lax–van Leer (HLL) solver is one of the most fundamental and robust approximate solvers, distinguished by its simplicity and strong stability properties. This chapter delves into the principles and mechanisms of the HLL solver.

### The Godunov Method and the Role of the Numerical Flux

We begin by recalling the semi-discrete [finite volume](@entry_id:749401) formulation for a one-dimensional system of conservation laws, $\partial_t \boldsymbol{U} + \partial_x \boldsymbol{F}(\boldsymbol{U}) = 0$. By integrating the PDE over a computational cell $[x_{i-1/2}, x_{i+1/2}]$ and applying the divergence theorem, we arrive at an [ordinary differential equation](@entry_id:168621) for the cell-averaged state $\boldsymbol{U}_i(t)$:

$$
\frac{d\boldsymbol{U}_i}{dt} = -\frac{1}{\Delta x} \left( \boldsymbol{F}( \boldsymbol{U}(x_{i+1/2}, t) ) - \boldsymbol{F}( \boldsymbol{U}(x_{i-1/2}, t) ) \right)
$$

where $\Delta x = x_{i+1/2} - x_{i-1/2}$ is the cell width. Integrating this from time $t^n$ to $t^{n+1} = t^n + \Delta t$ yields the explicit update formula:

$$
\boldsymbol{U}_i^{n+1} = \boldsymbol{U}_i^n - \frac{\Delta t}{\Delta x} \left( \boldsymbol{F}_{i+1/2} - \boldsymbol{F}_{i-1/2} \right)
$$

Here, the numerical flux $\boldsymbol{F}_{i+1/2}$ represents the time-averaged physical flux at the interface $x_{i+1/2}$ over the time step $\Delta t$. The central idea of the Godunov method is to obtain this flux by solving the local Riemann problem defined at each interface . At time $t^n$, we assume a [piecewise-constant reconstruction](@entry_id:753441) of the solution, such that the initial condition for the Riemann problem at interface $x_{i+1/2}$ is:

$$
\boldsymbol{U}(x, t^n) = 
\begin{cases}
\boldsymbol{U}_L = \boldsymbol{U}_i^n, & x  x_{i+1/2} \\
\boldsymbol{U}_R = \boldsymbol{U}_{i+1}^n,  x > x_{i+1/2}
\end{cases}
$$

For a strictly hyperbolic system—one whose flux Jacobian $\boldsymbol{A}(\boldsymbol{U}) = \partial \boldsymbol{F}/\partial \boldsymbol{U}$ possesses a complete set of real, distinct eigenvalues—the solution to this problem is self-similar, depending only on the coordinate $\xi = (x - x_{i+1/2}) / (t-t^n)$. The flux at the interface, $\boldsymbol{F}(\boldsymbol{U}(x_{i+1/2}, t))$, is therefore constant in time for $t \in (t^n, t^{n+1}]$, and the numerical flux is simply $\boldsymbol{F}_{i+1/2} = \boldsymbol{F}(\boldsymbol{U}(\xi=0))$ . Approximate Riemann solvers like HLL provide computationally efficient ways to estimate this interfacial flux.

### The Two-Wave HLL Approximation

The exact solution to a Riemann problem can consist of a complex fan of waves, including shocks, rarefactions, and [contact discontinuities](@entry_id:747781). The Harten–Lax–van Leer solver drastically simplifies this picture by assuming the solution consists of only three constant states: the initial left state $\boldsymbol{U}_L$, the initial right state $\boldsymbol{U}_R$, and a single intermediate "star" state, denoted $\boldsymbol{U}^*$. These states are separated by two bounding waves propagating at speeds $S_L$ and $S_R$ . The approximate solution is thus:

$$
\boldsymbol{U}_{HLL}(\xi) = 
\begin{cases}
\boldsymbol{U}_L,  \xi  S_L \\
\boldsymbol{U}^*,  S_L \le \xi \le S_R \\
\boldsymbol{U}_R,  \xi > S_R
\end{cases}
$$

For this two-wave model to be physically consistent, the chosen wave speeds $S_L$ and $S_R$ must enclose the entire true Riemann fan. This means $S_L$ must be less than or equal to the slowest physical [wave speed](@entry_id:186208), and $S_R$ must be greater than or equal to the fastest physical wave speed. The physical wave speeds are given by the eigenvalues $\lambda_k(\boldsymbol{U})$ of the flux Jacobian, evaluated for all states $\boldsymbol{U}$ that appear in the exact solution. A [sufficient condition](@entry_id:276242) is therefore:

$$
S_L \le \min_{k, \boldsymbol{U} \in \mathcal{P}} \lambda_k(\boldsymbol{U}) \quad \text{and} \quad S_R \ge \max_{k, \boldsymbol{U} \in \mathcal{P}} \lambda_k(\boldsymbol{U})
$$

where $\mathcal{P}$ is the set of all intermediate states connecting $\boldsymbol{U}_L$ to $\boldsymbol{U}_R$ in the exact solution . This bracketing of all characteristic signals is the fundamental principle of the HLL construction.

### Derivation of the HLL State and Flux

The intermediate state $\boldsymbol{U}^*$ and its corresponding flux $\boldsymbol{F}^*$ are derived by enforcing the [integral conservation law](@entry_id:175062) over the space-time region defined by the HLL wave structure. This is equivalent to applying the Rankine–Hugoniot [jump conditions](@entry_id:750965) across the two discontinuities at speeds $S_L$ and $S_R$.

Across the left wave with speed $S_L$:
$$
\boldsymbol{F}^* - \boldsymbol{F}(\boldsymbol{U}_L) = S_L (\boldsymbol{U}^* - \boldsymbol{U}_L)
$$

Across the right wave with speed $S_R$:
$$
\boldsymbol{F}(\boldsymbol{U}_R) - \boldsymbol{F}^* = S_R (\boldsymbol{U}_R - \boldsymbol{U}^*)
$$

These two vector equations form a linear system for the two unknown vectors $\boldsymbol{U}^*$ and $\boldsymbol{F}^*$. Solving for $\boldsymbol{U}^*$ yields:

$$
\boldsymbol{U}^* = \frac{S_R \boldsymbol{U}_R - S_L \boldsymbol{U}_L - (\boldsymbol{F}(\boldsymbol{U}_R) - \boldsymbol{F}(\boldsymbol{U}_L))}{S_R - S_L}
$$

Solving for $\boldsymbol{F}^*$ gives the flux in the star region:

$$
\boldsymbol{F}^* = \frac{S_R \boldsymbol{F}(\boldsymbol{U}_L) - S_L \boldsymbol{F}(\boldsymbol{U}_R) + S_L S_R (\boldsymbol{U}_R - \boldsymbol{U}_L)}{S_R - S_L}
$$

The HLL [numerical flux](@entry_id:145174), $\boldsymbol{F}_{HLL}$, is the flux from this approximate solution evaluated at the interface, $\xi=0$. Its value depends on the position of the interface relative to the wave fan  :

$$
\boldsymbol{F}_{HLL}(\boldsymbol{U}_L, \boldsymbol{U}_R) = 
\begin{cases}
\boldsymbol{F}(\boldsymbol{U}_L),  0 \le S_L \\
\dfrac{S_R \boldsymbol{F}(\boldsymbol{U}_L) - S_L \boldsymbol{F}(\boldsymbol{U}_R) + S_L S_R (\boldsymbol{U}_R - \boldsymbol{U}_L)}{S_R - S_L},  S_L  0  S_R \\
\boldsymbol{F}(\boldsymbol{U}_R),  S_R \le 0
\end{cases}
$$

If all waves move to the right ($0 \le S_L$), the state at the interface is $\boldsymbol{U}_L$, and the flux is simply the [upwind flux](@entry_id:143931) $\boldsymbol{F}(\boldsymbol{U}_L)$. Conversely, if all waves move to the left ($S_R \le 0$), the flux is $\boldsymbol{F}(\boldsymbol{U}_R)$. If the interface lies within the star region ($S_L  0  S_R$), the flux is $\boldsymbol{F}^*$.

A crucial property of any valid [numerical flux](@entry_id:145174) is **consistency**, meaning that if the left and right states are identical ($\boldsymbol{U}_L = \boldsymbol{U}_R = \boldsymbol{U}$), the numerical flux must reduce to the physical flux, $\boldsymbol{F}(\boldsymbol{U})$. The HLL flux satisfies this property; substituting $\boldsymbol{U}_L = \boldsymbol{U}_R = \boldsymbol{U}$ into the formula for the central case yields $\boldsymbol{F}_{HLL} = \boldsymbol{F}(\boldsymbol{U})$ .

### Wave Speed Estimation and Application

The HLL formulation is general, but its performance depends critically on the estimates for the wave speeds $S_L$ and $S_R$. For the one-dimensional Euler equations, a common and simple choice is **Davis's estimates**, which are based on the local [characteristic speeds](@entry_id:165394), $u \pm c$, where $u$ is the fluid velocity and $c$ is the sound speed . The estimates are:

$$
S_L = \min(u_L - c_L, u_R - c_R)
$$
$$
S_R = \max(u_L + c_L, u_R + c_R)
$$

Let's illustrate the complete calculation of an HLL flux with a worked example for the Euler equations with $\gamma = 1.4$ .

**Example**: Consider a Riemann problem with the following left and right states in primitive variables $(\rho, u, p)$:
-   $\boldsymbol{U}_L$: $\rho_L = 1.0 \, \mathrm{kg/m^3}$, $u_L = 50 \, \mathrm{m/s}$, $p_L = 1.0 \times 10^5 \, \mathrm{Pa}$
-   $\boldsymbol{U}_R$: $\rho_R = 0.5 \, \mathrm{kg/m^3}$, $u_R = -20 \, \mathrm{m/s}$, $p_R = 0.8 \times 10^5 \, \mathrm{Pa}$

We aim to find the HLL mass flux, which is the first component of the flux vector $\boldsymbol{F}_{HLL}$.

1.  **Compute Sound Speeds**: Using $c = \sqrt{\gamma p / \rho}$:
    $c_L = \sqrt{1.4 \times (1.0 \times 10^5) / 1.0} \approx 374.17 \, \mathrm{m/s}$
    $c_R = \sqrt{1.4 \times (0.8 \times 10^5) / 0.5} \approx 473.29 \, \mathrm{m/s}$

2.  **Estimate Wave Speeds**: Using Davis's estimates:
    $S_L = \min(50 - 374.17, -20 - 473.29) = \min(-324.17, -493.29) = -493.29 \, \mathrm{m/s}$
    $S_R = \max(50 + 374.17, -20 + 473.29) = \max(424.17, 453.29) = 453.29 \, \mathrm{m/s}$

3.  **Compute Mass Flux**: Since $S_L  0  S_R$, we use the central HLL formula. The first component of $\boldsymbol{U}$ is $\rho$ and the first component of $\boldsymbol{F}$ is the mass flux $\rho u$. Let's denote the mass flux as $F_1$.
    $F_{1,L} = \rho_L u_L = 1.0 \times 50 = 50 \, \mathrm{kg \, m^{-2} \, s^{-1}}$
    $F_{1,R} = \rho_R u_R = 0.5 \times (-20) = -10 \, \mathrm{kg \, m^{-2} \, s^{-1}}$

    The first component of the HLL flux vector is:
    $$
    F_{HLL, 1} = \frac{S_R F_{1,L} - S_L F_{1,R} + S_L S_R (\rho_R - \rho_L)}{S_R - S_L}
    $$
    Plugging in the values:
    $$
    F_{HLL, 1} = \frac{(453.29)(50) - (-493.29)(-10) + (-493.29)(453.29)(0.5 - 1.0)}{453.29 - (-493.29)}
    $$
    $$
    F_{HLL, 1} = \frac{22664.5 - 4932.9 + 111797.1}{946.58} \approx \frac{129528.7}{946.58} \approx 136.8 \, \mathrm{kg \, m^{-2} \, s^{-1}}
    $$
    The HLL mass flux across the interface is approximately $136.8 \, \mathrm{kg \, m^{-2} \, s^{-1}}$.

### Properties, Robustness, and Limitations

The HLL solver's appeal lies not just in its simplicity but also in its remarkable robustness. This robustness stems from several key properties.

#### Relation to Other Solvers and Numerical Dissipation

The HLL flux formula provides a bridge to other well-known schemes. If we choose symmetric wave speeds $S_L = -\alpha$ and $S_R = \alpha$, where $\alpha$ is an estimate of the maximum local wave speed (e.g., $\alpha = \max(|\lambda(\boldsymbol{U}_L)|, |\lambda(\boldsymbol{U}_R)|)$), the HLL flux simplifies to:

$$
\boldsymbol{F}_{HLL} = \frac{1}{2}(\boldsymbol{F}_L + \boldsymbol{F}_R) - \frac{\alpha}{2}(\boldsymbol{U}_R - \boldsymbol{U}_L)
$$

This is the **Local Lax–Friedrichs (LLF)** or **Rusanov** flux  . This form clearly shows the [numerical flux](@entry_id:145174) as an average of the physical fluxes plus a dissipation term, $-\frac{\alpha}{2}(\boldsymbol{U}_R - \boldsymbol{U}_L)$. The term $\alpha$ acts as a scalar [numerical viscosity](@entry_id:142854). If we were to take the limit $\alpha \to 0$, the flux would become the non-dissipative central flux $\frac{1}{2}(\boldsymbol{F}_L + \boldsymbol{F}_R)$, which is notoriously unstable for hyperbolic problems with discontinuities .

The dissipation in HLL/LLF is **isotropic**; it applies the same [damping coefficient](@entry_id:163719) $\alpha$ to all characteristic fields. This contrasts with more sophisticated solvers like Roe's, which provides **anisotropic** dissipation tailored to each characteristic wave speed. While Roe's method is less dissipative and more accurate for certain features, HLL's strong, simple dissipation is a key source of its stability .

#### Positivity Preservation

For systems like the Euler equations, it is crucial that the numerical solution maintains the positivity of [physical quantities](@entry_id:177395) like density $\rho$ and pressure $p$. A significant challenge arises in high-Mach-number flows, where kinetic energy vastly exceeds internal energy. The pressure is then calculated as a small difference between two large numbers, $p = (\gamma - 1)(E - \frac{1}{2}\rho u^2)$, making it susceptible to [catastrophic cancellation](@entry_id:137443) errors that can result in unphysical negative pressures .

The HLL scheme, when equipped with appropriate wave speed estimates, can guarantee positivity. A solver using **Einfeldt's wave speed estimates** (often called an **HLLE** solver) is guaranteed to produce an intermediate state $\boldsymbol{U}^*$ with positive density and pressure, provided the initial states are positive . Furthermore, for the full finite volume update to preserve positivity, the time step must satisfy a Courant–Friedrichs–Lewy (CFL) condition, which for the HLL scheme is typically of the form:

$$
\frac{\Delta t}{\Delta x} \left( \max\{0, S_R\} - \min\{0, S_L\} \right) \le 1
$$

This robust positivity preservation is a major advantage of HLL-type schemes over linearized solvers like Roe's, which are known to fail (i.e., produce negative pressures) in challenging situations without special "fixes"  .

#### Entropy Condition

Weak solutions to [hyperbolic conservation laws](@entry_id:147752) are not unique. The physically correct solution is selected by an **[entropy condition](@entry_id:166346)**, which for a strictly convex entropy function $\eta(\boldsymbol{U})$ requires that $\partial_t \eta(\boldsymbol{U}) + \partial_x q(\boldsymbol{U}) \le 0$ in a distributional sense. This condition forbids the formation of "expansion shocks"—discontinuities that should physically be smooth [rarefaction waves](@entry_id:168428).

Approximate solvers like HLL can sometimes violate this condition, particularly in **transonic rarefactions**, where a [characteristic speed](@entry_id:173770) passes through zero. A naive choice of wave speeds can fail to provide enough [numerical dissipation](@entry_id:141318) at the [sonic point](@entry_id:755066), causing the smooth rarefaction to collapse into an unphysical shock. To remedy this, an **[entropy fix](@entry_id:749021)** is applied, which typically involves modifying the wave speed estimates to ensure they bracket the [sonic point](@entry_id:755066). A common fix is to enforce:

$$
S_L = \min\{\lambda_{\min}(\boldsymbol{U}_L), \lambda_{\min}(\boldsymbol{U}_R), 0\} \quad \text{and} \quad S_R = \max\{\lambda_{\max}(\boldsymbol{U}_L), \lambda_{\max}(\boldsymbol{U}_R), 0\}
$$

By including $0$ in the min/max operations, this ensures that if the physical wave fan crosses the $\xi=0$ axis, the HLL fan does as well, adding the necessary dissipation to smooth out the unphysical shock .

### Limitation and the HLLC Extension

The primary weakness of the HLL solver stems directly from its greatest strength: its simplicity. By modeling the entire Riemann fan with a single intermediate state, HLL is structurally incapable of resolving waves that lie strictly between the fastest and slowest characteristics. For the Euler equations, the eigenstructure includes a linearly degenerate wave family propagating at the [fluid velocity](@entry_id:267320), $\lambda=u$. This family carries **[contact discontinuities](@entry_id:747781)** (jumps in density and temperature) and **shear waves** (jumps in tangential velocity) .

Since HLL replaces the region containing this middle wave with a single, constant averaged state $\boldsymbol{U}^*$, it cannot represent the jumps associated with contacts and shears. Instead, it smears them out through numerical diffusion. For a problem involving a pure contact wave, an HLL-based method will produce a thick, ramp-like transition instead of a sharp interface .

This limitation motivated the development of the **Harten–Lax–van Leer–Contact (HLLC)** solver. The HLLC solver enriches the HLL model by reintroducing the missing middle wave. It assumes a four-state, three-wave structure ($S_L, S_M, S_R$), where the middle wave at speed $S_M$ is specifically designed to represent the contact/shear family. The key assumption is that pressure and normal velocity are constant across this middle wave. This allows the HLLC solver to resolve contact and shear waves with minimal diffusion, dramatically improving solution accuracy for a wide range of fluid dynamics problems, while retaining much of the robustness of the original HLL scheme .