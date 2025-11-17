## Introduction
The accurate simulation of wave propagation is fundamental to progress in fields ranging from [computational fluid dynamics](@entry_id:142614) to electromagnetics and seismology. High-order numerical methods, such as spectral and discontinuous Galerkin (DG) methods, are increasingly favored for these tasks due to their ability to achieve high accuracy with fewer degrees of freedom compared to their low-order counterparts. However, this potential for high fidelity is not automatic. The process of [discretization](@entry_id:145012) invariably introduces non-physical artifacts—[numerical dispersion and dissipation](@entry_id:752783)—which can distort wave shapes, alter their speeds, and spuriously damp their amplitudes over time. Without a deep understanding of these error mechanisms, even a formally high-order simulation can produce physically meaningless results, especially for long-time integrations.

This article provides a comprehensive guide to the analysis of [numerical dispersion and dissipation](@entry_id:752783). It bridges the gap between the theoretical promise of [high-order methods](@entry_id:165413) and their practical, robust implementation. You will learn not only what these errors are but also how to precisely quantify and control them. The following chapters are structured to build this expertise systematically. The **Principles and Mechanisms** chapter lays the theoretical groundwork, introducing Fourier and energy analysis to dissect the behavior of discrete operators. Next, **Applications and Interdisciplinary Connections** demonstrates how these analytical tools are used in practice to compare schemes, make informed implementation choices, and solve complex problems in various scientific domains. Finally, the **Hands-On Practices** section offers targeted exercises to translate theoretical knowledge into practical skill. By mastering this material, you will be equipped to design, analyze, and deploy more accurate and reliable numerical simulations for wave-dominated phenomena.

## Principles and Mechanisms

Having established the context and motivation for [high-order methods](@entry_id:165413), we now delve into the core principles and mechanisms governing their accuracy for [wave propagation](@entry_id:144063) phenomena. The fidelity of a [numerical simulation](@entry_id:137087) is not merely a question of formal order of accuracy; it is critically dependent on how well the scheme approximates the physical processes of [wave dispersion](@entry_id:180230) and dissipation. When a numerical method fails to do so accurately, it introduces non-physical artifacts known as **numerical dispersion** and **[numerical dissipation](@entry_id:141318)**. This chapter provides a systematic framework for analyzing these errors, starting from first principles and extending to the complex scenarios encountered in practical applications.

### The Continuous Ideal: Non-Dispersive Wave Propagation

To understand numerical errors, we must first characterize the exact behavior of the system we aim to model. Let us consider the simplest model for wave propagation, the one-dimensional [linear advection equation](@entry_id:146245) with constant speed $a$:
$$
\frac{\partial u}{\partial t} + a \frac{\partial u}{\partial x} = 0, \quad x \in \mathbb{R}, t \ge 0
$$

A powerful method for analyzing such linear, constant-coefficient partial differential equations (PDEs) is to study their response to a single Fourier mode, or a **plane wave**. We assume a solution of the form:
$$
u(x,t) = \hat{u} \exp(i(kx - \omega t))
$$
where $\hat{u}$ is a constant [complex amplitude](@entry_id:164138), $k$ is the **wavenumber** (spatial frequency), and $\omega$ is the **[angular frequency](@entry_id:274516)** (temporal frequency). Substituting this [ansatz](@entry_id:184384) into the PDE yields an algebraic relationship between $\omega$ and $k$, known as the **[dispersion relation](@entry_id:138513)**.

For the [linear advection equation](@entry_id:146245), the partial derivatives are $\frac{\partial u}{\partial t} = -i\omega u$ and $\frac{\partial u}{\partial x} = iku$. The PDE thus becomes:
$$
-i\omega u + a(iku) = 0 \implies -i(\omega - ak)u = 0
$$
For a non-trivial solution ($u \neq 0$), we must have $\omega - ak = 0$. This gives the exact [dispersion relation](@entry_id:138513) for the continuous problem [@problem_id:3404817]:
$$
\omega(k) = ak
$$

This linear relationship between frequency and [wavenumber](@entry_id:172452) has profound physical implications. Two key velocities characterize wave propagation:

1.  The **phase velocity**, $c_p(k) = \omega(k)/k$, is the speed at which a point of constant phase on a single sinusoidal wave propagates. For the [advection equation](@entry_id:144869), $c_p(k) = \frac{ak}{k} = a$.

2.  The **group velocity**, $c_g(k) = \frac{d\omega(k)}{dk}$, is the speed at which the envelope of a [wave packet](@entry_id:144436) (a superposition of waves with wavenumbers centered around $k$) propagates. For the advection equation, $c_g(k) = \frac{d}{dk}(ak) = a$.

The fact that both the phase and group velocities are constant and equal to the advection speed $a$ for all wavenumbers $k$ is the defining characteristic of a **non-dispersive** system. In such a system, any wave profile, no matter how complex, is translated at speed $a$ without changing its shape. Furthermore, since the exact dispersion relation is purely real, the amplitude of any Fourier mode remains constant in time; the system is non-dissipative. This ideal, shape-preserving transport is the benchmark against which we measure our numerical methods.

### The Semi-Discrete Approximation: Emergence of Numerical Errors

When we discretize the spatial derivatives in a PDE, we obtain a system of [ordinary differential equations](@entry_id:147024) (ODEs) in time, known as a **semi-discrete** system. For a linear PDE on a uniform periodic mesh, this system can often be written as:
$$
\frac{d\mathbf{U}}{dt} = \mathcal{L}_h \mathbf{U}
$$
where $\mathbf{U}$ is the vector of all degrees of freedom in the simulation and $\mathcal{L}_h$ is the semi-discrete spatial operator.

We can analyze this system using the same Fourier techniques as for the continuous PDE. For a single Fourier mode, the operator $\mathcal{L}_h$ acts as multiplication by a complex number $\lambda_h(k)$, which is the **Fourier symbol** (or eigenvalue) of the semi-discrete operator corresponding to wavenumber $k$. The semi-discrete ODE for the amplitude of this mode becomes:
$$
\frac{d\hat{u}(k, t)}{dt} = \lambda_h(k) \hat{u}(k, t)
$$
The solution is $\hat{u}(k,t) = \hat{u}(k,0) \exp(\lambda_h(k)t)$. The complex-valued symbol $\lambda_h(k)$ governs the entire behavior of the numerical solution for that mode. We can decompose it into its real and imaginary parts: $\lambda_h(k) = \sigma_h(k) - i\omega_h(k)$.

The solution's evolution is then $\exp((\sigma_h(k) - i\omega_h(k))t) = \exp(\sigma_h(k)t) \exp(-i\omega_h(k)t)$. This reveals two distinct types of [numerical error](@entry_id:147272) [@problem_id:3404801]:

1.  **Numerical Dissipation**: The term $\exp(\sigma_h(k)t)$ controls the amplitude of the numerical solution. The quantity $\sigma_h(k) = \operatorname{Re}(\lambda_h(k))$ is the temporal growth/decay rate. For the exact advection equation, the amplitude is constant, corresponding to an exact rate of zero. Any deviation of $\sigma_h(k)$ from zero represents a [numerical error](@entry_id:147272) in amplitude.
    -   If $\sigma_h(k) < 0$, the mode's amplitude decays over time. This is **[numerical dissipation](@entry_id:141318)** (or [artificial dissipation](@entry_id:746522)).
    -   If $\sigma_h(k) > 0$, the mode's amplitude grows exponentially. This is **[numerical instability](@entry_id:137058)**.
    A scheme is defined as **non-dissipative** if $\sigma_h(k) = 0$ for all $k$.

2.  **Numerical Dispersion**: The term $\exp(-i\omega_h(k)t)$ controls the phase of the numerical solution. The function $\omega_h(k) = -\operatorname{Im}(\lambda_h(k))$ is the **[numerical dispersion relation](@entry_id:752786)**. In general, $\omega_h(k)$ will not be a linear function of $k$. This nonlinearity gives rise to [numerical dispersion](@entry_id:145368). We define the numerical [phase velocity](@entry_id:154045) as $c_{p,h}(k) = \omega_h(k)/k$ and the numerical [group velocity](@entry_id:147686) as $c_{g,h}(k) = d\omega_h(k)/dk$.
    -   When $c_{p,h}(k)$ is not constant, different Fourier modes travel at different speeds, causing an initially coherent wave profile to disperse into a train of oscillations.
    -   When $c_{g,h}(k)$ deviates from the exact [group velocity](@entry_id:147686) $a$, [wave packets](@entry_id:154698) travel at the wrong speed.

The practical consequence of these errors is a loss of simulation fidelity over time. The **phase velocity error**, $\epsilon_{\text{phase}}(k) = c_{p,h}(k) - a$, causes the [carrier wave](@entry_id:261646) within a packet to drift out of sync with the true solution. The **[group velocity](@entry_id:147686) error**, $\epsilon_g(k) = c_{g,h}(k) - a$, causes the entire packet envelope to be displaced from its correct position. For a narrowband [wave packet](@entry_id:144436) centered at wavenumber $k_0$, the envelope displacement error grows linearly with time as $t \cdot \epsilon_g(k_0)$ [@problem_id:3404860]. For long-time simulations, even small dispersion errors can accumulate and lead to a completely incorrect solution.

### A Concrete Case: Fourier Analysis of the Discontinuous Galerkin Method

Let's apply these concepts to the Discontinuous Galerkin (DG) method. A key feature of DG methods is the use of multiple degrees of freedom (e.g., coefficients of a polynomial basis) within each element. For a degree-$p$ approximation on a uniform periodic mesh, a Fourier [ansatz](@entry_id:184384) of the form $U_j(t) = \hat{U}(t) e^{ij\theta}$ (where $\theta=kh$ is the non-dimensional wavenumber and $U_j$ is the vector of $p+1$ coefficients in cell $j$) reveals that the semi-discrete operator does not have a single scalar symbol. Instead, it has a $(p+1) \times (p+1)$ **Fourier symbol matrix**, $\mathsf{A}(\theta)$ [@problem_id:3404871].
$$
\frac{d\hat{U}}{dt} = \mathsf{A}(\theta) \hat{U}
$$
The eigenvalues of this matrix, $\{\lambda_m(\theta)\}_{m=0}^p$, are the semi-discrete amplification exponents for the system. Each eigenvalue corresponds to a different numerical mode, some of which are physical approximations to the true solution, while others are [spurious modes](@entry_id:163321) arising from the high-degree polynomial basis. Analyzing the real and imaginary parts of these eigenvalues reveals the dissipative and dispersive properties of the DG scheme.

To make this tangible, consider the simplest DG method: degree $p=0$, where the solution is piecewise constant in each cell of size $h$. This is equivalent to a [finite volume method](@entry_id:141374). For the [linear advection equation](@entry_id:146245), the semi-discrete update for cell $j$ depends on a **numerical flux**, $\hat{f}$, at the interfaces. A common family of fluxes is the Lax-Friedrichs flux, parameterized by $\beta \in [0, 1]$ [@problem_id:3404841, @problem_id:3404878]:
$$
\hat{f}(u^-, u^+) = a \frac{u^- + u^+}{2} - \beta \frac{a}{2} (u^+ - u^-)
$$
Here, $u^-$ and $u^+$ are the solution values to the left and right of the interface. $\beta=0$ gives the **central flux**, while for $a>0$, $\beta=1$ gives the **[upwind flux](@entry_id:143931)**.

Performing a von Neumann analysis for this DG($p=0$) scheme yields the scalar Fourier symbol (since $p=0$, the symbol matrix is $1\times 1$):
$$
\lambda(\theta; \beta) = -\frac{a\beta}{h}(1 - \cos(\theta)) - i\frac{a}{h}\sin(\theta)
$$
From this, we can directly read off the dissipation and dispersion characteristics [@problem_id:3404841]:
-   **Numerical Dissipation Rate**: $\sigma_h(\theta) = \operatorname{Re}(\lambda(\theta)) = -\frac{a\beta}{h}(1 - \cos(\theta))$ [@problem_id:3404878].
-   **Numerical Angular Frequency**: $\omega_h(\theta) = -\operatorname{Im}(\lambda(\theta)) = \frac{a}{h}\sin(\theta)$.

This explicit result demonstrates a fundamental principle:
-   For the central flux ($\beta=0$), the [dissipation rate](@entry_id:748577) is $\sigma_h(\theta)=0$. The scheme is non-dissipative but remains dispersive, as the numerical [phase velocity](@entry_id:154045) $c_{p,h} = \frac{\omega_h}{k} = a \frac{\sin(kh)}{kh}$ is not constant.
-   For the [upwind flux](@entry_id:143931) ($\beta=1$, with $a>0$), the [dissipation rate](@entry_id:748577) is $\sigma_h(\theta) = -\frac{a}{h}(1-\cos(\theta))$, which is strictly negative for all non-zero wavenumbers. The scheme is dissipative.
-   Notably, the dispersion term, related to $\operatorname{Im}(\lambda)$, is independent of $\beta$. This shows that the penalty term in the flux is a pure dissipation mechanism in this case, allowing dissipation to be controlled without altering the scheme's dispersive error.

### An Alternative Perspective: Energy Analysis and Numerical Fluxes

Fourier analysis is exceptionally powerful but is formally restricted to linear, constant-coefficient problems on periodic, uniform meshes. An alternative and more general approach to analyzing stability and dissipation is **energy analysis**. For many physical systems, a quantity like energy is conserved. For the [advection equation](@entry_id:144869), the total "energy" $E(t) = \frac{1}{2} \int u^2 dx$ is conserved. A stable numerical scheme should, at a minimum, ensure that this discrete energy does not grow unbounded.

For a DG method, we can derive an exact expression for the [time evolution](@entry_id:153943) of the discrete energy $E_h(t) = \frac{1}{2}\sum_K \int_K u_h^2 dx$. By choosing the [test function](@entry_id:178872) to be the solution itself ($v_h=u_h$) in the [weak formulation](@entry_id:142897) and summing over all elements, one can show that the rate of change of total energy is determined solely by contributions at the inter-element faces [@problem_id:3404852]:
$$
\frac{dE_h}{dt} = \sum_{\text{faces}} (\hat{f} - a\{u_h\})[\![u_h]\!]
$$
where $\{u_h\} = \frac{1}{2}(u_h^- + u_h^+)$ is the average and $[\![u_h]\!] = u_h^+ - u_h^-$ is the jump in the solution at a face.

This powerful result links the abstract choice of a [numerical flux](@entry_id:145174) directly to the scheme's energy behavior. Consider again the general [flux form](@entry_id:273811) $\hat{f} = a\{u_h\} - \frac{\lambda}{2}[\![u_h]\!]$. Substituting this into the energy equation gives:
$$
\frac{dE_h}{dt} = - \sum_{\text{faces}} \frac{\lambda}{2} [\![u_h]\!]^2
$$
This demonstrates that the parameter $\lambda$ controls energy dissipation [@problem_id:3404852]:
-   For the **central flux** ($\lambda=0$), $\frac{dE_h}{dt} = 0$. The scheme is perfectly energy-conserving, mirroring the continuous PDE. Such schemes are often termed **skew-adjoint** and are non-dissipative [@problem_id:3404801].
-   For the **[upwind flux](@entry_id:143931)** ($\lambda=|a|>0$), $\frac{dE_h}{dt} = -\sum \frac{|a|}{2}[\![u_h]\!]^2 \le 0$. The scheme removes energy whenever there is a jump in the solution at an interface, making it **energy-dissipative** and robustly stable.
-   The parameter $\lambda$ provides a "penalty" on the jumps, acting as a tunable [artificial dissipation](@entry_id:746522) that does not compromise the consistency of the flux.

This energy-based view confirms the conclusions from Fourier analysis in a more general setting, showing that central fluxes are non-dissipative while upwind fluxes add dissipation proportional to the square of the solution jumps.

### The Fully-Discrete System: The Influence of Time Integration

So far, our analysis has focused on the semi-discrete system, where space is discretized but time remains continuous. In practice, the system of ODEs must also be integrated in time, typically with a method like an explicit Runge-Kutta (RK) scheme. This adds another layer of approximation and potential error.

When an RK method is applied to the modal ODE $\frac{d\hat{u}}{dt} = \lambda_h \hat{u}$, the one-step update is given by $\hat{u}_{n+1} = R(\Delta t \lambda_h) \hat{u}_n$, where $R(z)$ is the **[stability function](@entry_id:178107)** of the RK method, a polynomial in $z=\Delta t \lambda_h$ whose degree depends on the number of stages [@problem_id:3404797].

The complex number $G_h(k) = R(\Delta t \lambda_h(k))$ is the **fully-discrete amplification factor**. The total numerical error is now a combination of the [spatial discretization](@entry_id:172158) error (encoded in $\lambda_h$) and the [temporal discretization](@entry_id:755844) error (encoded in $R(z)$). The goal is for $G_h(k)$ to be a good approximation of the exact continuous [propagator](@entry_id:139558), $e^{-i ak \Delta t}$.

We can define per-step amplitude and phase errors for the fully-discrete scheme [@problem_id:3404797]:
-   **Fully-discrete amplitude error** is the deviation of $|R(\Delta t \lambda_h)|$ from the target amplitude $|\exp(\Delta t \lambda_h)| = \exp(\Delta t \operatorname{Re}(\lambda_h))$.
-   **Fully-discrete [phase error](@entry_id:162993)** is the deviation of $\arg(R(\Delta t \lambda_h))$ from the target phase $\arg(\exp(\Delta t \lambda_h)) = \Delta t \operatorname{Im}(\lambda_h)$.

For an RK method of order $p$, its stability function approximates the exponential function such that $R(z) = e^z + \mathcal{O}(z^{p+1})$ for small $z$. This implies that for sufficiently small time steps $\Delta t$, the temporal [phase error](@entry_id:162993) is of order $\mathcal{O}((\Delta t)^{p+1})$ [@problem_id:3404797]. However, it is crucial to recognize that no explicit RK method can be perfectly non-dissipative. For a non-dissipative [semi-discretization](@entry_id:163562) ($\lambda_h$ is purely imaginary), any explicit RK method will introduce some amount of amplitude error ($|R(\Delta t \lambda_h)| \neq 1$), adding its own [numerical dissipation](@entry_id:141318) to the system.

### Advanced Topics in Dispersion and Dissipation Analysis

The framework established above provides the foundation for analyzing more complex and realistic scenarios.

#### Nonlinearity and Aliasing Instability

For [nonlinear conservation laws](@entry_id:170694), such as $u_t + \partial_x f(u) = 0$, a new source of error emerges. Consider a quadratic flux $f(u) = \frac{1}{2}u^2$. If the solution $u_h$ is represented by a polynomial of degree $p$, the flux term $f(u_h)$ is a polynomial of degree $2p$. In a nodal [collocation method](@entry_id:138885), this flux is represented only by its values at the $p+1$ nodes. This is equivalent to creating a degree-$p$ interpolant of the true degree-$2p$ flux. The high-frequency content of the true flux is not lost but is instead spuriously "folded down" onto the lower, resolved frequencies. This phenomenon is called **[aliasing](@entry_id:146322)** [@problem_id:3404818].

Aliasing is fundamentally different from linear dispersion. It represents a spurious transfer of energy between modes and is a primary cause of [nonlinear instability](@entry_id:752642) in [high-order methods](@entry_id:165413). To combat this, two main strategies are employed:
1.  **Dealiasing**: Methods like **over-integration** (using a [quadrature rule](@entry_id:175061) exact for the higher-degree polynomial flux) can completely remove [aliasing](@entry_id:146322) errors.
2.  **Filtering**: Explicitly adding [artificial dissipation](@entry_id:746522) via **modal filtering** or **[spectral vanishing viscosity](@entry_id:755188)** (SVV) can damp the high-frequency modes that are most susceptible to aliasing-driven growth.

Crucially, [dealiasing](@entry_id:748248) techniques are inactive for linear problems, as no polynomial degree growth occurs. In contrast, filters add dissipation regardless of linearity, modifying the operator's spectrum even for linear problems [@problem_id:3404818].

#### Multi-Dimensional Effects: Numerical Anisotropy

In multiple spatial dimensions, the use of tensor-product grids (e.g., Cartesian meshes) and tensor-product basis functions introduces another artifact: **[numerical anisotropy](@entry_id:752775)**. While the continuous [advection equation](@entry_id:144869) $\partial_t u + \boldsymbol{a} \cdot \nabla u = 0$ is isotropic (its [wave propagation](@entry_id:144063) speed depends only on the angle between $\boldsymbol{a}$ and $\boldsymbol{k}$), the discrete operator is not.

For a 2D DG method on a Cartesian grid, the Fourier symbol of the semi-discrete operator depends separately on the non-dimensional wavenumbers in each direction, $\theta_x = k_x h$ and $\theta_y = k_y h$, rather than solely on the magnitude $|\boldsymbol{k}|$. Consequently, the numerical phase speed $c_{p,h}$ depends on the direction of the [wavevector](@entry_id:178620) $\boldsymbol{k}$ relative to the grid axes. Waves propagating along the grid axis ($\theta=0$) will have a different [dispersion error](@entry_id:748555) than waves propagating along the grid diagonal ($\theta=\pi/4$) [@problem_id:3404845]. This directional dependency of [wave speed](@entry_id:186208) is a purely numerical artifact and can lead to significant distortion of wave fronts over time.

#### Curvilinear Meshes and the Geometric Conservation Law

To model problems in complex geometries, meshes with [curved elements](@entry_id:748117) are necessary. In an isoparametric DG method, elements are mapped from a simple [reference element](@entry_id:168425) (e.g., a cube) to the physical curved element via a polynomial mapping. This mapping introduces geometric factors, or **metric terms** (such as the Jacobian determinant $J$ and contravariant basis vectors $\boldsymbol{a}^m$), into the transformed PDE.

A critical property that the discrete operators must satisfy is the **Geometric Conservation Law (GCL)**. In its continuous form, the GCL states that the divergence of the metric terms is zero. Its discrete counterpart requires that the discrete [divergence operator](@entry_id:265975), when applied to the [discrete metric](@entry_id:154658) terms, also yields zero. Satisfying the discrete GCL ensures that the numerical scheme can exactly preserve a constant-flow state ("free-stream preservation") [@problem_id:3404864].

If the metric terms are not computed and discretized in a way that respects the GCL, the discrete operator will contain spurious source terms. These sources corrupt the operator's eigenvalues, altering the [numerical dispersion and dissipation](@entry_id:752783) in an unphysical manner and preventing the scheme from even preserving a constant solution. Modern high-order DG methods employ special constructions (e.g., a "discrete curl form" for the metrics) to ensure the GCL is satisfied, thereby guaranteeing a stable and accurate foundation for wave propagation analysis on complex grids [@problem_id:3404864].