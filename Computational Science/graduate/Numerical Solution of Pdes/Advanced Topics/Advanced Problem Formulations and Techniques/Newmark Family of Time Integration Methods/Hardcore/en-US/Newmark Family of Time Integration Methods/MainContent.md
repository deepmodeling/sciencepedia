## Introduction
The Newmark family of [time integration methods](@entry_id:136323) stands as a cornerstone in computational science and engineering, providing a powerful and versatile framework for solving the second-order [ordinary differential equations](@entry_id:147024) (ODEs) that govern dynamic systems. These equations frequently arise from the [spatial discretization](@entry_id:172158) of physical phenomena, such as the vibration of structures, the propagation of waves, or the motion of mechanical systems. The challenge lies in advancing the solution through time accurately and stably, a problem the Newmark method elegantly addresses. This article provides a comprehensive exploration of this indispensable numerical tool, bridging theory and practical application.

The following chapters are structured to build a complete understanding of the Newmark family. The first chapter, "Principles and Mechanisms," delves into the fundamental formulation of the method, analyzing how the choice of its defining parameters, $\beta$ and $\gamma$, dictates its accuracy, stability, and dissipative properties. The second chapter, "Applications and Interdisciplinary Connections," demonstrates the method's versatility by exploring its use in solving real-world problems in structural and geotechnical engineering, [nonlinear dynamics](@entry_id:140844), wave propagation, and even abstract network analysis. Finally, "Hands-On Practices" offers practical problems to solidify the concepts discussed, guiding you from theoretical derivation to computational implementation.

## Principles and Mechanisms

The Newmark family of methods represents a cornerstone of [numerical time integration](@entry_id:752837) for second-order [ordinary differential equations](@entry_id:147024) (ODEs), which frequently arise from the semi-[discretization of partial differential equations](@entry_id:748527) governing [structural dynamics](@entry_id:172684), [wave propagation](@entry_id:144063), and other areas of [computational mechanics](@entry_id:174464). This chapter elucidates the fundamental principles of the Newmark family, from its core formulation to its properties of accuracy, stability, and [algorithmic damping](@entry_id:167471), and explores its implementation in both linear and nonlinear contexts.

### The Newmark Formulation

Consider a system of second-order ODEs, typically obtained from a [spatial discretization](@entry_id:172158) method like the Finite Element Method (FEM), written in the general form:
$$
M \ddot{q}(t) + C \dot{q}(t) + K q(t) = f(t)
$$
Here, $q(t)$ is the vector of generalized displacements, with $\dot{q}(t)$ and $\ddot{q}(t)$ being the corresponding velocities and accelerations. $M$, $C$, and $K$ are the mass, damping, and stiffness matrices, respectively, and $f(t)$ is the vector of external forces. We assume $M$ is symmetric and positive-definite, while $C$ and $K$ are symmetric and [positive semi-definite](@entry_id:262808).

The Newmark family of methods provides a step-by-step procedure to advance the solution from a known state $(q_n, \dot{q}_n, \ddot{q}_n)$ at time $t_n$ to the new state at time $t_{n+1} = t_n + \Delta t$. The method is defined by two update equations that approximate the displacement and velocity at the new time step. These equations are formulated as weighted averages of the accelerations at the beginning and end of the time step .

The displacement update is given by:
$$
q_{n+1} = q_{n} + \Delta t \dot{q}_{n} + \Delta t^{2} \left( \left(\frac{1}{2} - \beta\right) \ddot{q}_{n} + \beta \ddot{q}_{n+1} \right)
$$

The velocity update is given by:
$$
\dot{q}_{n+1} = \dot{q}_{n} + \Delta t \left( (1 - \gamma) \ddot{q}_{n} + \gamma \ddot{q}_{n+1} \right)
$$

These two kinematic relations are supplemented by the enforcement of the system's equation of motion at the end of the time step:
$$
M \ddot{q}_{n+1} + C \dot{q}_{n+1} + K q_{n+1} = f(t_{n+1})
$$

The constants $\beta$ and $\gamma$ are the **Newmark parameters**. They define a specific integrator within the broader family. The parameter $\beta$ weights the contribution of the new-step acceleration $\ddot{q}_{n+1}$ in the displacement update, while $\gamma$ performs the same role for the velocity update. As will be shown, the choice of these parameters governs all [critical properties](@entry_id:260687) of the integrator, including its accuracy, stability, and dissipative characteristics.

### Analysis of Accuracy

The accuracy of a numerical method is quantified by its **local truncation error (LTE)**, which is the error incurred in a single step assuming the solution is exact at the beginning of that step. The [order of accuracy](@entry_id:145189) is determined by how this error scales with the time step $\Delta t$. We can determine the LTE of the Newmark method by comparing its update equations to the Taylor series expansions of the exact solution around time $t_n$ .

Let us assume the exact solution $q(t)$ is sufficiently smooth. The Taylor expansions for velocity and acceleration are:
$$
\dot{q}(t_{n+1}) = \dot{q}(t_n) + \Delta t \ddot{q}(t_n) + \frac{\Delta t^2}{2} \dddot{q}(t_n) + \mathcal{O}(\Delta t^3)
$$
$$
\ddot{q}(t_{n+1}) = \ddot{q}(t_n) + \Delta t \dddot{q}(t_n) + \mathcal{O}(\Delta t^2)
$$

Substituting the expansion for $\ddot{q}(t_{n+1})$ into the Newmark velocity update reveals its LTE:
$$
\dot{q}_{n+1} = \dot{q}_{n} + \Delta t \ddot{q}_{n} + \gamma \Delta t^2 \dddot{q}_{n} + \mathcal{O}(\Delta t^3)
$$
The difference between the numerical velocity $\dot{q}_{n+1}$ and the exact velocity $\dot{q}(t_{n+1})$ is the LTE for velocity:
$$
\boldsymbol{\tau}_{v, n+1} = \dot{q}(t_{n+1}) - \dot{q}_{n+1} = \left(\frac{1}{2} - \gamma\right) \Delta t^2 \dddot{q}_n + \mathcal{O}(\Delta t^3)
$$
For the method to be **second-order accurate** for velocity, the LTE must be of order $\mathcal{O}(\Delta t^3)$. This requires the coefficient of the $\Delta t^2$ term to be zero, which leads to the critical condition:
$$
\gamma = \frac{1}{2}
$$

If $\gamma \neq \frac{1}{2}$, the LTE for velocity is $\mathcal{O}(\Delta t^2)$, making the velocity update only first-order accurate. For a stable method, this results in a [global error](@entry_id:147874) in velocity of $\mathcal{O}(\Delta t)$.

A similar analysis for the displacement update shows its LTE is:
$$
\boldsymbol{\tau}_{q, n+1} = q(t_{n+1}) - q_{n+1} = \left(\frac{1}{6} - \frac{\beta}{2}\right) \Delta t^3 \dddot{q}_n + \mathcal{O}(\Delta t^4)
$$
This assumes we have already set $\gamma=1/2$. The displacement update is at least second-order accurate (LTE is $\mathcal{O}(\Delta t^3)$) for any reasonable choice of $\beta$. Therefore, the overall order of the Newmark method is dictated by the choice of $\gamma$. To achieve [second-order accuracy](@entry_id:137876) in both displacement and velocity, the choice $\gamma = 1/2$ is necessary.

### Analysis of Stability and Algorithmic Damping

**Stability** refers to the ability of a numerical method to prevent the growth of errors over time. For an oscillatory system, this means the numerical solution should not exhibit unbounded amplitude growth when the true solution is bounded. The stability of the Newmark family is typically analyzed using the undamped single-degree-of-freedom (SDOF) model equation: $\ddot{u}(t) + \omega^2 u(t) = 0$.

For [linear systems](@entry_id:147850), the Newmark method is **unconditionally stable**, meaning it is stable for any choice of time step $\Delta t > 0$, if and only if the parameters satisfy:
$$
2\beta \ge \gamma \ge \frac{1}{2}
$$
If these conditions are not met, the method is **conditionally stable**, meaning it is stable only if the time step is sufficiently small, typically satisfying a condition of the form $\omega_{\max} \Delta t \le C$, where $\omega_{\max}$ is the highest natural frequency in the system.

A highly desirable property for many applications in [structural dynamics](@entry_id:172684) is **[algorithmic damping](@entry_id:167471)** (or numerical dissipation). High-frequency modes resulting from [spatial discretization](@entry_id:172158) are often physically inaccurate and can pollute the numerical solution. An integrator with [algorithmic damping](@entry_id:167471) can selectively dissipate the energy of these spurious [high-frequency modes](@entry_id:750297) without significantly affecting the accuracy of the lower-frequency modes of interest.

In the Newmark family, [algorithmic damping](@entry_id:167471) is controlled by the parameter $\gamma$. Specifically:
- If $\gamma = 1/2$, the method is non-dissipative for [linear systems](@entry_id:147850). It conserves energy.
- If $\gamma > 1/2$, the method introduces [numerical damping](@entry_id:166654) that increases with frequency.

This behavior can be quantified by examining the **asymptotic [spectral radius](@entry_id:138984)**, $\rho_\infty$, of the [amplification matrix](@entry_id:746417) in the limit of infinite frequency ($\omega \Delta t \to \infty$) . For a scheme with $\beta = \gamma/2$ (a choice that satisfies [unconditional stability](@entry_id:145631) for $\gamma \ge 1/2$), the [spectral radius](@entry_id:138984) of the physical mode has the limit:
$$
\rho_{\infty} = \left| \frac{\gamma-1}{\gamma} \right| = \left| 1 - \frac{1}{\gamma} \right|
$$
For $\gamma = 1/2$, $\rho_\infty = 1$, indicating no damping. As $\gamma$ increases from $1/2$, $\rho_\infty$ decreases, reaching $\rho_\infty = 0$ at $\gamma = 1$. This provides a mechanism to control the amount of [high-frequency dissipation](@entry_id:750292). A larger $\gamma$ implies stronger damping.

It is crucial to note that stability is an intrinsic property of the numerical algorithm. While physical damping (represented by the matrix $C$) will naturally dissipate energy in the system, its presence does not alter the stability requirements on the Newmark parameters $\beta$ and $\gamma$. An analysis of a system with proportional (Rayleigh) damping, $C = \alpha M + \beta_K K$, shows that the region of [unconditional stability](@entry_id:145631) in the $(\beta, \gamma)$ [parameter space](@entry_id:178581) is not enlarged. A scheme that is conditionally stable for an undamped system remains conditionally stable regardless of the amount of physical damping added .

### Important Members of the Newmark Family

Different choices of $(\beta, \gamma)$ lead to methods with distinct characteristics.

#### The Average Acceleration Method ($\beta = 1/4, \gamma = 1/2$)

This is one of the most widely used [implicit methods](@entry_id:137073). Its properties are:
- **Unconditionally stable:** The parameters satisfy $2\beta = 1/2$ and $\gamma = 1/2$.
- **Second-order accurate:** Since $\gamma=1/2$.
- **Non-dissipative:** Since $\gamma=1/2$, it introduces no [algorithmic damping](@entry_id:167471) and is energy-conserving for linear undamped systems .

This method is equivalent to applying the [trapezoidal rule](@entry_id:145375) to the first-order form of the system. For Hamiltonian systems like the undamped oscillator, the Newmark [average acceleration method](@entry_id:169724) is **symplectic**. This means it preserves a fundamental geometric property of the phase space, which leads to excellent long-term energy behavior. While the discrete energy is exactly conserved for the linear oscillator, for nonlinear Hamiltonian systems, a symplectic integrator guarantees that the energy error remains bounded for all time, without secular drift. This is a significant advantage over non-symplectic methods .

A closely related [symplectic integrator](@entry_id:143009) is the **Störmer-Verlet method**. While both methods are second-order accurate and exhibit excellent long-term [energy stability](@entry_id:748991), their amplification matrices and phase error characteristics differ. For a step size $h$ and frequency $\omega$, the discrete rotation angle $\theta(\lambda)$ for $\lambda = h\omega$ is given by:
- Newmark Average Acceleration: $\cos(\theta_N(\lambda)) = \frac{1 - \lambda^2/4}{1 + \lambda^2/4}$
- Störmer-Verlet: $\cos(\theta_V(\lambda)) = 1 - \frac{\lambda^2}{2}$
This difference in phase error is a key distinction between the two methods .

#### The Linear Acceleration Method ($\beta = 1/6, \gamma = 1/2$)

This method assumes that the acceleration varies linearly over a time step.
- **Conditionally stable:** It does not satisfy $2\beta \ge \gamma$. Stability requires $\omega \Delta t \le \sqrt{12} \approx 3.46$.
- **Second-order accurate:** Since $\gamma=1/2$.
- **Non-dissipative:** Since $\gamma=1/2$.

#### The Central Difference Method ($\beta = 0, \gamma = 1/2$)

This is an explicit method, provided the [mass matrix](@entry_id:177093) $M$ is diagonal (or "lumped").
- **Conditionally stable:** Stability requires $\omega_{\max} \Delta t \le 2$.
- **Second-order accurate:** Since $\gamma=1/2$.
- **Non-dissipative:** Since $\gamma=1/2$.

The explicit nature of this method avoids the need to solve a system of equations at each step, making it computationally efficient, but the stability constraint on $\Delta t$ can be severe for systems with high frequencies.

### Implementation and Application

#### One-Step Method Formulation

A common point of confusion is whether the Newmark method is a "one-step" or "multistep" method, as it uses accelerations from both time $t_n$ and $t_{n+1}$. A method is classified as **one-step** if the state at step $n+1$ depends only on the state at step $n$. In the phase space $(q, \dot{q})$, the state is defined by the displacement and velocity. Although the Newmark updates use $\ddot{q}_n$, this acceleration is not an independent historical variable. It is fully determined by the state $(q_n, \dot{q}_n)$ via the equation of motion at time $t_n$:
$$
\ddot{q}_n = M^{-1}(f_n - C\dot{q}_n - Kq_n)
$$
Because $\ddot{q}_n$ can be computed from the state at the beginning of the step, the entire update procedure to find $(q_{n+1}, \dot{q}_{n+1})$ depends only on $(q_n, \dot{q}_n)$ and forcing data. Therefore, for all choices of $(\beta, \gamma)$, the Newmark method is fundamentally a one-step method in the phase space $(q, \dot{q})$ .

#### Predictor-Corrector Implementation

For implicit cases ($\beta \neq 0$), a system of equations must be solved for $\ddot{q}_{n+1}$ (or equivalently, $q_{n+1}$). A highly effective structure for this is the **predictor-corrector** format .

1.  **Predictor Stage:** Compute predicted displacement and velocity at $t_{n+1}$ using only information from $t_n$. This is an explicit extrapolation.
    $$
    q_{n+1}^{p} = q_n + \Delta t \dot{q}_n + \Delta t^2 \left(\frac{1}{2} - \beta\right) \ddot{q}_n
    $$
    $$
    \dot{q}_{n+1}^{p} = \dot{q}_n + \Delta t (1 - \gamma) \ddot{q}_n
    $$

2.  **Acceleration Solve Stage:** Substitute the predicted values into the equation of motion at $t_{n+1}$ and solve for the unknown acceleration $\ddot{q}_{n+1}$. This involves solving the linear system:
    $$
    (M + \gamma \Delta t C + \beta \Delta t^2 K) \ddot{q}_{n+1} = f_{n+1} - C \dot{q}_{n+1}^{p} - K q_{n+1}^{p}
    $$
    The matrix on the left is often called the [effective stiffness matrix](@entry_id:164384).

3.  **Corrector Stage:** Update the displacement and velocity with the newly computed acceleration $\ddot{q}_{n+1}$.
    $$
    q_{n+1} = q_{n+1}^{p} + \beta \Delta t^2 \ddot{q}_{n+1}
    $$
    $$
    \dot{q}_{n+1} = \dot{q}_{n+1}^{p} + \gamma \Delta t \ddot{q}_{n+1}
    $$

#### Application to Nonlinear Systems

The true power of implicit Newmark methods lies in their application to [nonlinear dynamics](@entry_id:140844), where the internal forces and their corresponding stiffness depend on the displacement: $f_{\text{int}}(q)$. The [equation of motion](@entry_id:264286) at $t_{n+1}$ becomes a nonlinear algebraic system:
$$
R(q_{n+1}) = M \ddot{q}_{n+1}(q_{n+1}) + C \dot{q}_{n+1}(q_{n+1}) + f_{\text{int}}(q_{n+1}) - f_{\text{ext}}^{n+1} = 0
$$
This system is typically solved using a Newton-Raphson iterative procedure. To achieve the quadratic convergence rate of this procedure, one must compute the exact Jacobian of the residual $R$ with respect to the solution variable $q_{n+1}$. This Jacobian is known as the **[consistent algorithmic tangent](@entry_id:166068) matrix**, $K_{\text{alg}}$.

By applying the [chain rule](@entry_id:147422) to the residual, and using the derivatives of the Newmark relations, we find the expression for this crucial matrix :
$$
K_{\text{alg}} = \frac{\partial R}{\partial q_{n+1}} = \frac{1}{\beta \Delta t^2} M + \frac{\gamma}{\beta \Delta t} C + K_T(q_{n+1})
$$
where $K_T(q_{n+1}) = \partial f_{\text{int}}(q_{n+1}) / \partial q_{n+1}$ is the material tangent stiffness matrix. Using this exact tangent in the Newton solver ensures that the dynamic problem converges quadratically at each time step.

#### Application to PDEs and Practical Considerations

When solving PDEs, the interaction between spatial and [temporal discretization](@entry_id:755844) errors determines the overall accuracy. This can be studied via a **[numerical dispersion](@entry_id:145368) analysis**. For the 1D wave equation $u_{tt} = c^2 u_{xx}$ discretized with linear finite elements and the Newmark [average acceleration method](@entry_id:169724), the [numerical dispersion relation](@entry_id:752786) $\omega_{\text{num}}(k)$ relates the numerical frequency to the physical wavenumber $k$. It is given by :
$$
\omega_{\text{num}}(k;h,\Delta t) = \frac{2}{\Delta t} \arctan\left(\frac{\sqrt{3} c \Delta t}{h} \frac{\sin(kh/2)}{\sqrt{\cos(kh)+2}}\right)
$$
where $h$ is the mesh size. The exact relation is $\omega = ck$. Taylor expansion of this expression reveals that the spatial FEM discretization introduces a [phase lead](@entry_id:269084) (numerical waves travel too fast), while the temporal Newmark [discretization](@entry_id:145012) introduces a phase lag (waves travel too slow). The overall accuracy depends on the balance between these competing error sources.

A final practical consideration in FEM is the choice of the mass matrix. The **[consistent mass matrix](@entry_id:174630)** $M_c$ is derived from the FEM basis functions and is non-diagonal. The **[lumped mass matrix](@entry_id:173011)** $M_l$ is a [diagonal approximation](@entry_id:270948) that preserves total mass. This choice has significant consequences :
- **Spectrum:** Mass lumping typically lowers the maximum natural frequency of the semi-discrete system ($\omega_{l,\max} \le \omega_{c,\max}$).
- **Stability:** For conditionally stable explicit methods (like central differences), using a [lumped mass matrix](@entry_id:173011) allows for a larger [critical time step](@entry_id:178088) $\Delta t_{\text{crit}} = 2/\omega_{\max}$, improving [computational efficiency](@entry_id:270255).
- **Algorithmic Damping:** For dissipative Newmark schemes ($\gamma > 1/2$), the amount of damping is a function of $\omega_j \Delta t$. Since [mass lumping](@entry_id:175432) reduces the high-end frequencies, the most oscillatory modes experience weaker [numerical damping](@entry_id:166654) compared to a system with a [consistent mass matrix](@entry_id:174630) at the same $\Delta t$.

This trade-off between stability, accuracy, and efficiency is a central theme in the application of the Newmark family of methods to complex engineering problems.