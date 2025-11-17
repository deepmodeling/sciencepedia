## Introduction
Hyperbolic conservation laws are foundational to modeling a vast range of physical phenomena, from fluid dynamics to traffic flow. However, their mathematical theory admits non-unique, [weak solutions](@entry_id:161732), some of which are physically impossible. The key to selecting the physically correct solution lies in the [entropy condition](@entry_id:166346), a mathematical embodiment of the [second law of thermodynamics](@entry_id:142732). This article addresses the critical challenge of how to design numerical schemes that not only approximate the conservation law but also rigorously satisfy a discrete version of this [entropy condition](@entry_id:166346), guaranteeing stability and physical realism.

This article provides a comprehensive guide to the theory and application of entropy-stable numerical methods. In the first chapter, **Principles and Mechanisms**, we will explore the continuous [entropy condition](@entry_id:166346) and detail the systematic construction of entropy-conservative and [entropy-stable fluxes](@entry_id:749015) from first principles. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the power and flexibility of this framework by applying it to complex systems like the Euler equations, incorporating source terms for geophysical flows, and extending it to [curvilinear grids](@entry_id:748121). Finally, the **Hands-On Practices** chapter offers guided problems to build practical skills in designing and analyzing these robust numerical schemes.

## Principles and Mechanisms

The theoretical framework of [hyperbolic conservation laws](@entry_id:147752) admits [weak solutions](@entry_id:161732) that may not be unique or physically relevant. To select the physically admissible solution, we rely on the concept of an **[entropy condition](@entry_id:166346)**, which serves as a mathematical proxy for the second law of thermodynamics. This chapter elucidates the principles underlying entropy conditions and details the mechanisms by which modern [numerical schemes](@entry_id:752822) are constructed to satisfy a discrete analogue of these conditions, ensuring their stability and robustness.

### The Continuous Entropy Condition

For a system of $m$ conservation laws in one dimension,
$$
\partial_t u + \partial_x f(u) = 0, \quad u \in \mathbb{R}^m,
$$
a solution is deemed physically admissible if it satisfies an additional inequality involving an **entropy pair** $(U, F)$. An entropy function $U: \mathbb{R}^m \to \mathbb{R}$ must be a **strictly convex** function of the conservative variables $u$. The corresponding **entropy flux** $F: \mathbb{R}^m \to \mathbb{R}$ is determined by the **compatibility condition**, which demands that for any smooth solution, an additional conservation law holds.

For smooth solutions, the chain rule applied to $U(u(x,t))$ yields $U(u)_t = (\nabla U)^\top u_t$. Substituting $u_t = -f(u)_x = -f'(u) u_x$, where $f'(u)$ is the flux Jacobian, gives $U(u)_t = -(\nabla U)^\top f'(u) u_x$. For the pair $(U,F)$ to satisfy its own conservation law, $U(u)_t + F(u)_x = 0$, we must have $F(u)_x = (\nabla F)^\top u_x = (\nabla U)^\top f'(u) u_x$. This equality must hold for arbitrary spatial gradients $u_x$, which leads to the [compatibility condition](@entry_id:171102) [@problem_id:3386398]:
$$
\nabla F(u) = (\nabla U(u))^\top f'(u).
$$

While smooth solutions conserve both the state variables $u$ and the entropy $U$, physical reality dictates that entropy is not conserved across shock discontinuities. Instead, it must be produced. This physical principle is formalized as the **[entropy inequality](@entry_id:184404)**, which must be satisfied by all admissible [weak solutions](@entry_id:161732) in the sense of distributions:
$$
\partial_t U(u) + \partial_x F(u) \le 0.
$$
This inequality ensures that the total entropy in a [closed system](@entry_id:139565), $\int U(u) \, dx$, is a non-increasing function of time. Note the sign convention: for [thermodynamic systems](@entry_id:188734) like the compressible Euler equations, the physical entropy increases. The mathematical entropy is often defined as the negative of the physical entropy (e.g., $U = -\rho s$, where $s$ is the specific [thermodynamic entropy](@entry_id:155885)), so that its [convexity](@entry_id:138568) property holds and the inequality takes the form above [@problem_id:3386389]. This single inequality, enforced for a strictly convex entropy function, is sufficient to rule out non-physical phenomena such as expansion shocks.

The fundamental justification for this inequality stems from the **[vanishing viscosity method](@entry_id:177856)** [@problem_id:3386390]. If we consider a regularized equation $u^\varepsilon_t + f(u^\varepsilon)_x = \varepsilon u^\varepsilon_{xx}$, its solutions $u^\varepsilon$ are smooth. Multiplying by $(\nabla U(u^\varepsilon))^\top$ and applying the [compatibility condition](@entry_id:171102) yields:
$$
\partial_t U(u^\varepsilon) + \partial_x F(u^\varepsilon) = \varepsilon (\nabla U(u^\varepsilon))^\top u^\varepsilon_{xx} = \varepsilon \partial_x ((\nabla U)^\top u^\varepsilon_x) - \varepsilon (u^\varepsilon_x)^\top (\nabla^2 U) u^\varepsilon_x.
$$
The crucial insight is that if $U$ is convex, its Hessian matrix $\nabla^2 U$ is [positive semi-definite](@entry_id:262808). Consequently, the final term is non-positive, $-\varepsilon (u^\varepsilon_x)^\top (\nabla^2 U) u^\varepsilon_x \le 0$. As the viscosity $\varepsilon \to 0$, the solutions $u^\varepsilon$ converge to a [weak solution](@entry_id:146017) $u$ of the original conservation law, and the inequality is preserved in the limit, yielding $\partial_t U(u) + \partial_x F(u) \le 0$. This argument highlights that the **convexity of the entropy function is essential** for establishing a well-defined entropy dissipation direction and selecting admissible [weak solutions](@entry_id:161732) [@problem_id:3386390]. For scalar laws, requiring this inequality for all convex entropies is equivalent to the celebrated Kružkov theory, which guarantees the existence and uniqueness of the entropy solution [@problem_id:3386389].

### Entropy-Conservative Fluxes

The goal of modern numerical methods is to construct schemes that satisfy a discrete version of the [entropy inequality](@entry_id:184404). The first step in this construction is to design a numerical flux that exactly conserves the discrete total entropy. Such a flux is termed **entropy-conservative (EC)**.

Consider a semi-discrete finite volume scheme on a uniform grid:
$$
\frac{d u_i}{dt} + \frac{1}{\Delta x}(\hat{f}_{i+1/2} - \hat{f}_{i-1/2}) = 0,
$$
where $\hat{f}_{i+1/2} = \hat{f}(u_i, u_{i+1})$ is a two-point [numerical flux](@entry_id:145174). The rate of change of the total discrete entropy $\mathcal{U} = \sum_i U(u_i)$ is found by multiplying the scheme by the **entropy variables**, defined as $v_i = \nabla U(u_i)$:
$$
\frac{d \mathcal{U}}{dt} = \sum_i \frac{d U(u_i)}{dt} = \sum_i (\nabla U(u_i))^\top \frac{d u_i}{dt} = \sum_i v_i^\top \frac{d u_i}{dt}.
$$
Substituting the scheme and performing a [summation by parts](@entry_id:139432) (assuming periodic boundary conditions) yields [@problem_id:3386437] [@problem_id:3386398]:
$$
\frac{d \mathcal{U}}{dt} = \frac{1}{\Delta x} \sum_i (v_{i+1} - v_i)^\top \hat{f}_{i+1/2}.
$$
For the total entropy to be conserved, this sum must vanish. This is achieved if each term can be written as a difference of a function evaluated at cell centers, allowing the sum to telescope to zero. This requirement leads to the discovery of the **entropy potential**, $\psi(u) = (\nabla U(u))^\top f(u) - F(u)$. A two-point flux $\hat{f}^{ec}$ is defined as entropy-conservative if it satisfies **Tadmor's condition** [@problem_id:3386437]:
$$
(v_R - v_L)^\top \hat{f}^{ec}(u_L, u_R) = \psi(u_R) - \psi(u_L).
$$
When this condition holds, the rate of change of total entropy becomes $\frac{1}{\Delta x} \sum_i (\psi_{i+1} - \psi_i)$, which is a [telescoping sum](@entry_id:262349) that vanishes under periodic boundary conditions, thus guaranteeing $\frac{d\mathcal{U}}{dt}=0$.

To make these concepts concrete, let us construct an EC flux for the scalar Burgers' equation, $u_t + (\frac{1}{2}u^2)_x = 0$, with the quadratic entropy $U(u) = \frac{1}{2}u^2$ [@problem_id:3386399] [@problem_id:3386409].
1.  **Entropy Variable**: $v(u) = U'(u) = u$.
2.  **Entropy Flux**: From $F'(u) = v(u) f'(u) = u \cdot u = u^2$, we integrate to get $F(u) = \frac{1}{3}u^3$.
3.  **Entropy Potential**: $\psi(u) = v(u)f(u) - F(u) = u(\frac{1}{2}u^2) - \frac{1}{3}u^3 = \frac{1}{6}u^3$.
4.  **Tadmor's Condition**: $(u_R - u_L) \hat{f}^{ec}(u_L, u_R) = \frac{1}{6}u_R^3 - \frac{1}{6}u_L^3$.
Solving for the flux (for $u_L \ne u_R$) gives:
$$
\hat{f}^{ec}(u_L, u_R) = \frac{1}{6} \frac{u_R^3 - u_L^3}{u_R - u_L} = \frac{1}{6}(u_L^2 + u_L u_R + u_R^2).
$$
This specific flux, built from first principles, exactly conserves the discrete entropy for Burgers' equation.

### Entropy-Stable Fluxes

Entropy-[conservative schemes](@entry_id:747715) are non-dissipative and thus cannot capture the [entropy production](@entry_id:141771) at shocks. To create a physically correct and robust numerical method, we must introduce numerical dissipation in a way that is consistent with the [entropy inequality](@entry_id:184404). This leads to the concept of **entropy-stable (ES) fluxes**.

An ES flux is constructed by adding a carefully designed dissipation term to an EC flux [@problem_id:3386398] [@problem_id:3386389]:
$$
\hat{f}^{es}(u_L, u_R) = \hat{f}^{ec}(u_L, u_R) - \frac{1}{2} D (v_R - v_L).
$$
Here, $D$ is a symmetric [positive semi-definite](@entry_id:262808) (SPSD) matrix representing the numerical dissipation. The dissipation is scaled by the jump in the entropy variables, $(v_R - v_L)$.

Revisiting the rate of change of total discrete entropy with this new flux, the EC part again contributes zero to the sum. The dissipation term remains:
$$
\frac{d \mathcal{U}}{dt} = - \frac{1}{2\Delta x} \sum_i (v_{i+1} - v_i)^\top D_{i+1/2} (v_{i+1} - v_i).
$$
Since each matrix $D_{i+1/2}$ is SPSD, the [quadratic form](@entry_id:153497) $(v_{i+1} - v_i)^\top D_{i+1/2} (v_{i+1} - v_i)$ is non-negative. Therefore, the total entropy is guaranteed to be non-increasing: $\frac{d\mathcal{U}}{dt} \le 0$. The scheme is provably stable in the entropy norm.

Continuing our example with Burgers' equation, we can construct an ES flux by choosing a dissipation matrix $D$ [@problem_id:3386409]. For a scalar problem, $D$ is a non-negative scalar, $\alpha \ge 0$. A physically motivated choice for $\alpha$ is the magnitude of the local characteristic speed. For Burgers' equation, the Roe-average speed is $\frac{u_L+u_R}{2}$. We choose $\alpha = |\frac{u_L+u_R}{2}|$. The resulting entropy-stable flux is:
$$
\hat{f}^{es}(u_L, u_R) = \frac{1}{6}(u_L^2 + u_L u_R + u_R^2) - \frac{1}{2} \left|\frac{u_L + u_R}{2}\right| (u_R - u_L).
$$
This flux not only guarantees stability but also introduces the necessary dissipation to capture shocks correctly.

### Deeper Principles and Advanced Implementations

The framework of [entropy-stable schemes](@entry_id:749017) rests on several profound mathematical properties and allows for sophisticated implementations.

#### The Role of Convexity and Coercivity

The [strict convexity](@entry_id:193965) of the entropy function $U$ is not merely a convenience for the vanishing viscosity argument; it is the structural bedrock of [entropy stability](@entry_id:749023). Strict convexity guarantees that the Hessian matrix $H(u) = \nabla^2 U(u)$ is symmetric and [positive definite](@entry_id:149459). On any compact set of states $\mathcal{K}$, the eigenvalues of $H(u)$ are uniformly bounded away from zero. This property, known as **[coercivity](@entry_id:159399)**, establishes a [norm equivalence](@entry_id:137561) between the Euclidean norm of jumps in the conservative variables, $\Delta u = u_R - u_L$, and jumps in the entropy variables, $\Delta v = v_R - v_L$ [@problem_id:3386449]. Specifically, the Mean Value Theorem gives:
$$
\Delta v = \left( \int_0^1 H(u_L + \theta \Delta u) \, d\theta \right) \Delta u = \bar{H} \Delta u.
$$
Coercivity of $H$ implies that the matrix $\bar{H}$ is invertible and its inverse is bounded. This means that a non-zero jump in the conservative variables ($\Delta u \ne 0$) implies a non-zero jump in the entropy variables ($\Delta v \ne 0$). Consequently, the entropy dissipation term, which is a quadratic form in $\Delta v$, effectively "senses" and damps oscillations in the solution $u$, providing [robust control](@entry_id:260994) over numerical stability [@problem_id:3386449].

#### Design of the Dissipation Matrix

The dissipation matrix $D$ can be tailored to the physics of the system.
-   **Scalar Dissipation**: The simplest choice is $D = \alpha I$, where $\alpha$ is a scalar coefficient, typically related to the maximum local wave speed. This adds dissipation isotropically, meaning it affects all characteristic fields equally [@problem_id:3386446]. While simple and effective, it can be overly dissipative for slower wave families.
-   **Matrix Dissipation**: A more refined approach is to use a matrix $D$ that reflects the characteristic structure of the hyperbolic system. By symmetrizing the flux Jacobian $f'(u)$ with the entropy Hessian $H(u)$, one obtains a [symmetric matrix](@entry_id:143130) $A^s$ which has a real [eigendecomposition](@entry_id:181333) $A^s = R \Lambda R^\top$. A powerful choice for the dissipation matrix is $D = R |\Lambda| R^\top$, where $|\Lambda|$ is the diagonal matrix of absolute eigenvalues. The resulting entropy dissipation at an interface is $\frac{1}{2} \sum_k |\lambda_k| \gamma_k^2$, where $\gamma = R^\top \Delta v$ are the jumps projected onto the characteristic fields. This method provides anisotropic dissipation, scaled precisely for each wave family by its speed, adding only the minimum amount of dissipation necessary for stability [@problem_id:3386446].

#### Entropy Fix for Sonic Points

Matrix-based dissipation using $D = R|\Lambda|R^\top$ is highly effective but has a critical failure mode. For [transonic rarefaction](@entry_id:756129) waves, a characteristic speed $\lambda_k$ can pass through zero. At the point where the averaged eigenvalue is zero, $|\lambda_k|=0$, and the scheme provides no dissipation for that wave family. This can allow the formation of physically incorrect expansion shocks. The solution is an **[entropy fix](@entry_id:749021)**. A common approach, due to Harten, is to modify the [absolute value function](@entry_id:160606) locally. For instance, $|\lambda_k|$ is replaced by a function $\phi(\lambda_k)$ such that $\phi(\lambda_k) \ge |\lambda_k|$ and $\phi(0) > 0$ in the vicinity of a [sonic point](@entry_id:755066), but $\phi(\lambda_k) \approx |\lambda_k|$ elsewhere. A typical choice is [@problem_id:3386422]:
$$
\phi_{\delta_k}(\lambda_k) =\begin{cases} \frac{1}{2}\left(\frac{\lambda_k^2}{\delta_k} + \delta_k\right),  &|\lambda_k| < \delta_k \\ |\lambda_k|,  &|\lambda_k| \ge \delta_k \end{cases}
$$
where $\delta_k$ is a small parameter that senses the presence of a transonic wave. This local modification adds the necessary dissipation to prevent expansion shocks while preserving the high accuracy of the scheme in other regions.

#### Application to Complex Systems: The Euler Equations

Constructing an entropy-conservative flux for a complex system like the compressible Euler equations is a non-trivial task. It requires finding a specific form of averaging for the [state variables](@entry_id:138790) that satisfies Tadmor's condition. Prominent examples include the fluxes developed by Ismail and Roe and by Chandrashekar. These methods identify auxiliary variables (e.g., $z_1=\sqrt{\rho/p}, z_2=\sqrt{\rho p}$ for Ismail-Roe) such that the entropy becomes a [linear combination](@entry_id:155091) of their logarithms. Then, by using logarithmic means for these auxiliary variables and arithmetic means for velocities, they construct averaged density and pressure that satisfy the EC condition precisely [@problem_id:3386415]. For example, the Ismail-Roe mass flux uses an averaged density $\bar{\rho} = \{\sqrt{\rho/p}\}_{\ln} \{\sqrt{\rho p}\}_{\ln}$, while the Chandrashekar flux uses $\bar{\rho} = \{\rho\}_{\ln}$. These elegant constructions demonstrate the practical power of the theoretical framework, enabling the design of provably stable and accurate schemes for real-world fluid dynamics problems.