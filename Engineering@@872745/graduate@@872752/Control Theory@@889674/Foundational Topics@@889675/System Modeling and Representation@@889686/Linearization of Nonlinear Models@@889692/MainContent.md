## Introduction
Nonlinear systems are ubiquitous in science and engineering, from the flight dynamics of an aircraft to the spread of a disease. However, their inherent complexity often renders them analytically intractable. The analysis of such systems presents a significant challenge, creating a knowledge gap that hinders our ability to predict their behavior and design effective controllers. Linearization offers a powerful and systematic approach to bridge this gap, approximating complex nonlinear dynamics with well-understood linear models in the vicinity of a specific operating point. This method unlocks the vast and powerful toolkit of [linear systems theory](@entry_id:172825) for local analysis and design.

This article provides a graduate-level exploration of linearization, structured to build both theoretical understanding and practical skill.
- The first chapter, **"Principles and Mechanisms,"** lays the mathematical groundwork, detailing the process of [linearization](@entry_id:267670) around [equilibrium points](@entry_id:167503) using Taylor series and Jacobian matrices, and discussing the rigorous conditions for its validity.
- The second chapter, **"Applications and Interdisciplinary Connections,"** showcases the immense utility of [linearization](@entry_id:267670) across diverse fields, including control design for aerospace and robotic systems, stability analysis in [epidemiology](@entry_id:141409), and [state estimation](@entry_id:169668) via the Extended Kalman Filter.
- The final chapter, **"Hands-On Practices,"** provides guided problems to solidify these concepts, tackling challenges from aerodynamic modeling to analyzing [actuator saturation](@entry_id:274581).

We will begin by delving into the core principles of [linearization](@entry_id:267670), starting with its most fundamental application: the analysis of a system's behavior around a [steady-state equilibrium](@entry_id:137090).

## Principles and Mechanisms

Linearization is a cornerstone of modern control theory and [system analysis](@entry_id:263805), providing a powerful bridge between the complex, often intractable world of nonlinear dynamics and the well-developed, systematic toolkit of [linear systems theory](@entry_id:172825). By approximating a nonlinear system with a linear one in the vicinity of a specific operating condition, we can analyze [local stability](@entry_id:751408), design controllers, and assess system properties like [observability](@entry_id:152062) and [controllability](@entry_id:148402) using established linear methods. This chapter delves into the fundamental principles and mechanisms of [linearization](@entry_id:267670), from its formal mathematical definition to its application in analyzing both static equilibria and dynamic orbits.

### The Foundation: Linearization around an Equilibrium Point

The most common application of [linearization](@entry_id:267670) is the analysis of a system's behavior near a steady-state condition, known as an equilibrium point. This forms the basis for much of local [stability theory](@entry_id:149957) and linear control design.

#### The Concept of an Equilibrium Point

Consider a general nonlinear time-invariant (NTI) system described by the [state-space equations](@entry_id:266994):
$$
\begin{aligned}
\dot{x} = f(x, u) \\
y = h(x, u)
\end{aligned}
$$
where $x(t) \in \mathbb{R}^n$ is the state vector, $u(t) \in \mathbb{R}^m$ is the input vector, and $y(t) \in \mathbb{R}^p$ is the output vector. The functions $f$ and $h$ are mappings that define the system's dynamics and output, respectively.

A crucial first step in linearization is to identify a time-invariant operating condition. Such a condition is defined by a constant state $x^\star$ and a constant input $u^\star$ for which the system is at rest. This leads to the formal definition of an **[equilibrium point](@entry_id:272705)**.

An **equilibrium point** (or [operating point](@entry_id:173374)) of the system is a pair $(x^\star, u^\star)$ such that if the input is held constant at $u(t) = u^\star$ and the initial state is $x(0) = x^\star$, the state remains constant for all future time. This implies that the time derivative of the state must be zero, $\dot{x}(t) = 0$. From the state equation, this requires that the pair $(x^\star, u^\star)$ satisfies the algebraic equation:
$$
f(x^\star, u^\star) = 0
$$
This condition is fundamental. Linearizing around a point $(x^\star, u^\star)$ where $f(x^\star, u^\star) \neq 0$ would result in a linearized model with a constant "drift" or "offset" term, complicating the analysis and deviating from the standard linear time-invariant (LTI) state-space form. By choosing an [equilibrium point](@entry_id:272705), we ensure that the resulting linear model describes dynamics purely in terms of deviations from this steady state [@problem_id:2720600].

Corresponding to the [equilibrium state](@entry_id:270364) and input is a **nominal output**, $y^\star$, which is the output produced by the system in this steady state:
$$
y^\star = h(x^\star, u^\star)
$$
This choice ensures consistency, such that zero deviations in state and input correspond to zero deviation in the output.

#### The Taylor Series Approximation and Jacobian Matrices

To understand the system's behavior for small deviations from the equilibrium, we define **perturbation variables**:
$$
\delta x(t) = x(t) - x^\star, \quad \delta u(t) = u(t) - u^\star, \quad \delta y(t) = y(t) - y^\star
$$
Since $x^\star$ is a constant, we have $\dot{x}(t) = \frac{d}{dt}(x^\star + \delta x(t)) = \dot{\delta x}(t)$. Substituting this into the state equation yields:
$$
\dot{\delta x} = f(x^\star + \delta x, u^\star + \delta u)
$$
Assuming the function $f$ is sufficiently smooth (a condition we will formalize later), we can approximate it using a first-order multivariate **Taylor [series expansion](@entry_id:142878)** around the point $(x^\star, u^\star)$:
$$
f(x, u) \approx f(x^\star, u^\star) + \left.\frac{\partial f}{\partial x}\right|_{(x^\star, u^\star)}(x - x^\star) + \left.\frac{\partial f}{\partial u}\right|_{(x^\star, u^\star)}(u - u^\star)
$$
Here, $\frac{\partial f}{\partial x}$ and $\frac{\partial f}{\partial u}$ are the **Jacobian matrices** of the vector function $f$ with respect to the vectors $x$ and $u$.

By definition of the equilibrium, $f(x^\star, u^\star) = 0$. Substituting the perturbation variables and the Jacobian matrix definitions, we arrive at the **linearized state equation**:
$$
\dot{\delta x} \approx A \delta x + B \delta u
$$
where the system matrices $A$ and $B$ are the Jacobians evaluated at the equilibrium:
$$
A = \left.\frac{\partial f}{\partial x}\right|_{(x^\star, u^\star)} \in \mathbb{R}^{n \times n}, \quad B = \left.\frac{\partial f}{\partial u}\right|_{(x^\star, u^\star)} \in \mathbb{R}^{n \times m}
$$
A similar procedure applies to the output equation [@problem_id:2909775]. We have $\delta y = y - y^\star = h(x^\star + \delta x, u^\star + \delta u) - h(x^\star, u^\star)$. The first-order Taylor expansion of $h$ is:
$$
h(x, u) \approx h(x^\star, u^\star) + \left.\frac{\partial h}{\partial x}\right|_{(x^\star, u^\star)}(x - x^\star) + \left.\frac{\partial h}{\partial u}\right|_{(x^\star, u^\star)}(u - u^\star)
$$
This leads directly to the **linearized output equation**:
$$
\delta y \approx C \delta x + D \delta u
$$
where the output matrices $C$ and $D$ are also Jacobian matrices:
$$
C = \left.\frac{\partial h}{\partial x}\right|_{(x^\star, u^\star)} \in \mathbb{R}^{p \times n}, \quad D = \left.\frac{\partial h}{\partial u}\right|_{(x^\star, u^\star)} \in \mathbb{R}^{p \times m}
$$
The resulting set of equations,
$$
\begin{aligned}
\dot{\delta x} = A \delta x + B \delta u \\
\delta y = C \delta x + D \delta u
\end{aligned}
$$
is an LTI [state-space model](@entry_id:273798) that approximates the behavior of the original [nonlinear system](@entry_id:162704) for small perturbations around the equilibrium $(x^\star, u^\star)$. This model is linear because the operations of [matrix-vector multiplication](@entry_id:140544) and addition satisfy the principle of superposition.

#### A Concrete Example of Linearization

To illustrate the process, consider the nonlinear system from [@problem_id:2909775]:
$$
\begin{aligned}
\dot{x}_{1} = -2 x_{1} + \sin(x_{2}) + u \\
\dot{x}_{2} = x_{1}^{2} - x_{2} + u^{3} \\
y = x_{1} + x_{2}^{2}
\end{aligned}
$$
Let us linearize this system around the [equilibrium point](@entry_id:272705) $(x_e, u_e) = ((0,0)^\top, 0)$. First, we confirm it is an equilibrium: $f((0,0)^\top, 0) = (-2(0)+\sin(0)+0, 0^2-0+0^3)^\top = (0,0)^\top$. The nominal output is $y_e = 0+0^2 = 0$.

Next, we compute the four Jacobian matrices at this point.
The Jacobian of the dynamics $f$ with respect to the state $x$ is:
$$
A = \left.\frac{\partial f}{\partial x}\right|_{x_e,u_e} = \left.\begin{pmatrix} -2 & \cos(x_{2}) \\ 2x_{1} & -1 \end{pmatrix}\right|_{(0,0,0)} = \begin{pmatrix} -2 & 1 \\ 0 & -1 \end{pmatrix}
$$
The Jacobian of $f$ with respect to the input $u$ is:
$$
B = \left.\frac{\partial f}{\partial u}\right|_{x_e,u_e} = \left.\begin{pmatrix} 1 \\ 3u^{2} \end{pmatrix}\right|_{(0,0,0)} = \begin{pmatrix} 1 \\ 0 \end{pmatrix}
$$
The Jacobian of the output $h$ with respect to the state $x$ is:
$$
C = \left.\frac{\partial h}{\partial x}\right|_{x_e,u_e} = \left.\begin{pmatrix} 1 & 2x_{2} \end{pmatrix}\right|_{(0,0,0)} = \begin{pmatrix} 1 & 0 \end{pmatrix}
$$
The Jacobian of $h$ with respect to the input $u$ is:
$$
D = \left.\frac{\partial h}{\partial u}\right|_{x_e,u_e} = \left. 0 \right|_{(0,0,0)} = 0
$$
The linearized model for perturbations $(\delta x, \delta u, \delta y)$ around the origin is:
$$
\begin{aligned}
\dot{\delta x} = \begin{pmatrix} -2 & 1 \\ 0 & -1 \end{pmatrix} \delta x + \begin{pmatrix} 1 \\ 0 \end{pmatrix} \delta u \\
\delta y = \begin{pmatrix} 1 & 0 \end{pmatrix} \delta x
\end{aligned}
$$
From this LTI model, we can compute a transfer function $G(s) = C(sI-A)^{-1}B+D$, which for this example evaluates to $G(s) = \frac{1}{s+2}$. This demonstrates how a complex [nonlinear system](@entry_id:162704) can be locally represented by a simple, first-order linear transfer function.

### Mathematical Rigor and Practical Considerations

The validity and accuracy of a linearized model depend on the mathematical properties of the underlying nonlinear functions and the size of the perturbations. A graduate-level understanding requires precision about these details.

#### The Role of Differentiability

The existence of the Jacobian matrices as [linear operators](@entry_id:149003) that accurately represent the system's local behavior is guaranteed by the concept of **Fréchet differentiability**. A function $f$ is Fréchet differentiable at a point $(x^\star, u^\star)$ if its change can be approximated by a [linear map](@entry_id:201112), with an error that vanishes faster than the magnitude of the perturbation. Formally, the [remainder term](@entry_id:159839) $r(\delta x, \delta u) = f(x^\star+\delta x, u^\star+\delta u) - f(x^\star, u^\star) - A\delta x - B\delta u$ must satisfy $\lim_{\|(\delta x, \delta u)\| \to 0} \frac{\|r(\delta x, \delta u)\|}{\|(\delta x, \delta u)\|} = 0$. This is often written as the error being of order **little-o**, denoted $o(\|(\delta x, \delta u)\|)$.

While Fréchet differentiability is the precise requirement, a more practical and commonly used sufficient condition is that the functions $f$ and $h$ are **continuously differentiable** (class $C^1$) in a neighborhood of the [operating point](@entry_id:173374). This means that all first-order [partial derivatives](@entry_id:146280) exist and are continuous, which guarantees Fréchet [differentiability](@entry_id:140863) [@problem_id:2720583].

The accuracy of the [linear approximation](@entry_id:146101) depends on [higher-order derivatives](@entry_id:140882). If $f$ and $h$ are twice continuously differentiable (class $C^2$), Taylor's theorem provides a stronger statement about the [remainder term](@entry_id:159839): its magnitude can be bounded by a quadratic function of the perturbation size, i.e., $\|r(\delta x, \delta u)\| \le M \|(\delta x, \delta u)\|^2$ for some constant $M$. This is an error of order **big-O**, denoted $\mathcal{O}(\|(\delta x, \delta u)\|^2)$. This quadratic bound is crucial for rigorously analyzing the region of validity for the [linearization](@entry_id:267670).

#### Estimating the Region of Validity

A natural question is: how small must the perturbations be for the linear model to be a "good" approximation? We can quantify this by defining a region where the neglected nonlinear terms are small relative to the linear terms [@problem_id:2720579].

Let's consider the state equation $\dot{\tilde{x}} = A\tilde{x} + r(\tilde{x})$ (using $\tilde{x}$ for perturbations). Suppose we can bound the [remainder term](@entry_id:159839) by a [quadratic form](@entry_id:153497), $\|r(\tilde{x})\| \le \frac{1}{2}\tilde{x}^\top H \tilde{x}$, where $H$ is a symmetric [positive semidefinite matrix](@entry_id:155134) related to the second derivatives (Hessian) of $f$. We can define the [linear approximation](@entry_id:146101) as valid if the remainder is a small fraction $\varepsilon$ of the linear part:
$$
\|r(\tilde{x})\| \le \varepsilon \|A\tilde{x}\|
$$
To find a radius $r$ of a ball of [initial conditions](@entry_id:152863) $\mathcal{B}_r = \{\tilde{x} : \|\tilde{x}\| \le r\}$ where this holds, we combine the inequalities. We seek the largest $r$ such that for all $\tilde{x} \in \mathcal{B}_r$:
$$
\frac{1}{2}\tilde{x}^\top H \tilde{x} \le \varepsilon \|A\tilde{x}\|
$$
Using standard norm inequalities, $\tilde{x}^\top H \tilde{x} \le \lambda_{\max}(H)\|\tilde{x}\|^2$ and $\|A\tilde{x}\| \ge \sigma_{\min}(A)\|\tilde{x}\|$, where $\lambda_{\max}$ is the maximum eigenvalue and $\sigma_{\min}$ is the minimum singular value, we can establish a [sufficient condition](@entry_id:276242):
$$
\frac{1}{2}\lambda_{\max}(H)\|\tilde{x}\|^2 \le \varepsilon \sigma_{\min}(A)\|\tilde{x}\|
$$
For $\tilde{x} \neq 0$, this simplifies to $\|\tilde{x}\| \le \frac{2\varepsilon\sigma_{\min}(A)}{\lambda_{\max}(H)}$. To guarantee this for the entire ball, the radius $r$ must satisfy this bound. The largest such radius is therefore:
$$
r = \frac{2\varepsilon\sigma_{\min}(A)}{\lambda_{\max}(H)}
$$
This important result shows that the region of validity is larger when:
*   The desired tolerance $\varepsilon$ is larger.
*   The system is "strongly linear" in that direction (large $\sigma_{\min}(A)$).
*   The system has low "curvature" (small $\lambda_{\max}(H)$).

#### Handling Structural Nonlinearities: The Chain Rule

In many physical systems, nonlinearities appear in a structured way, for instance, as a static function of the input. Consider a system of the form $\dot{x} = f(x, \phi(u))$, where $\phi$ is a nonlinear function [@problem_id:2720562]. A naive computation of the input matrix $B$ might be incorrect. The correct approach requires a careful application of the **[multivariate chain rule](@entry_id:635606)**.

Let $v = \phi(u)$. The dynamics are $f(x,v)$. To find the Jacobian with respect to $u$, we compute:
$$
B = \frac{\partial}{\partial u} f(x, \phi(u)) = \frac{\partial f}{\partial v} \frac{\partial v}{\partial u} = \frac{\partial f}{\partial v} \phi'(u)
$$
All derivatives must be evaluated at the operating point $(x^\star, u^\star)$. Let $v^\star = \phi(u^\star)$. Then the input matrix is:
$$
B = \left.\frac{\partial f}{\partial v}\right|_{(x^\star, v^\star)} \cdot \phi'(u^\star)
$$
For example, if $\dot{x} = -x + (\arctan(u))^2$, with $u^\star=1$, then $v = \arctan(u)$ and $f(x,v) = -x+v^2$. We have $v^\star = \arctan(1) = \frac{\pi}{4}$. The [equilibrium state](@entry_id:270364) is $x^\star = (v^\star)^2 = \frac{\pi^2}{16}$. The derivatives are $\frac{\partial f}{\partial v} = 2v$ and $\phi'(u) = \frac{1}{1+u^2}$. Evaluating at the operating point gives $\left.\frac{\partial f}{\partial v}\right|^\star = 2(\frac{\pi}{4}) = \frac{\pi}{2}$ and $\phi'(u^\star) = \frac{1}{1+1^2} = \frac{1}{2}$. The input "matrix" (a scalar in this case) is $B = (\frac{\pi}{2})(\frac{1}{2}) = \frac{\pi}{4}$. This rigorous application of the [chain rule](@entry_id:147422) is essential for correctly modeling the system's local input-output sensitivity.

### Applications of Linearization in System Analysis

Once a valid LTI approximation is obtained, it can be used to analyze various properties of the original nonlinear system in the local vicinity of the equilibrium.

#### Local Stability Analysis: Lyapunov's Indirect Method

**Lyapunov's indirect method** (or the [linearization](@entry_id:267670) method) provides a direct link between the stability of the LTI approximation and the [local stability](@entry_id:751408) of the nonlinear system. The method states that if the equilibrium point $(x^\star, u^\star)$ is **hyperbolic**—meaning the Jacobian matrix $A$ has no eigenvalues with a zero real part—then the qualitative stability behavior of the [nonlinear system](@entry_id:162704) in a small neighborhood of $x^\star$ is the same as that of the linearized system.
Specifically:
1.  If all eigenvalues of $A$ have strictly negative real parts ($\text{Re}(\lambda_i)  0$), the equilibrium $x^\star$ is **locally asymptotically stable**.
2.  If at least one eigenvalue of $A$ has a strictly positive real part ($\text{Re}(\lambda_i) > 0$), the equilibrium $x^\star$ is **unstable**.

This theorem is immensely powerful as it allows us to use linear stability tests (like checking eigenvalues) to draw conclusions about [nonlinear systems](@entry_id:168347). However, its applicability is limited to hyperbolic equilibria.

#### Local Observability

Observability is the ability to determine the state of a system from its output measurements. For nonlinear systems, this property can be state-dependent. Linearization allows us to assess **local [observability](@entry_id:152062)** near an equilibrium.

A linearized system $(\dot{\delta x} = A\delta x, \delta y = C\delta x)$ is observable if and only if the **[observability matrix](@entry_id:165052)** has full column rank:
$$
\mathcal{O} = \begin{pmatrix} C \\ CA \\ \vdots \\ CA^{n-1} \end{pmatrix}, \quad \text{rank}(\mathcal{O}) = n
$$
For a [nonlinear system](@entry_id:162704), the matrices $A$ and $C$ are Jacobians evaluated at a point $\hat{x}$, i.e., $A(\hat{x})$ and $C(\hat{x})$. The system is locally observable at $\hat{x}$ if the [observability matrix](@entry_id:165052) $\mathcal{O}(\hat{x})$ has full rank.

Consider a pendulum with angle $x_1$ and [angular velocity](@entry_id:192539) $x_2$. The measured output is $y = \sin(x_1)$ [@problem_id:2720575]. The output Jacobian is $C(\hat{x}) = [\cos(\hat{x}_1) \quad 0]$. The state Jacobian $A(\hat{x})$ can also be computed. The resulting [observability matrix](@entry_id:165052) for the linearized system has a determinant of $\det(\mathcal{O}(\hat{x})) = \cos^2(\hat{x}_1)$.
This determinant is zero when $\hat{x}_1 = \pi/2 + k\pi$ for any integer $k$. At these points (the top and bottom of the swing, if the sensor was aligned differently), the [observability matrix](@entry_id:165052) loses rank, and the system becomes locally unobservable. The physical intuition is clear: at the peak of the $\sin$ function, small changes in the angle $x_1$ produce almost no change in the output $y$, making the angle instantaneously unobservable from the measurement.

#### The Direct Feedthrough Term (D Matrix)

The matrix $D$ in the linearized model is called the **direct feedthrough** matrix because it represents an algebraic path from the input perturbation $\delta u$ to the output perturbation $\delta y$. As derived previously, $D = \left.\frac{\partial h}{\partial u}\right|_{(x^\star, u^\star)}$.

The direct feedthrough term vanishes, i.e., $D=0$, if and only if the partial derivative of the output function with respect to the input is zero at the operating point [@problem_id:2720606]. It is critical to understand that this is a local condition. A system can have $D=0$ at one operating point but not another. Furthermore, the function $h$ may depend strongly on $u$ globally, but if the [operating point](@entry_id:173374) $u^\star$ happens to be a location where the sensitivity is zero (e.g., a local extremum of $h$ with respect to $u$), then the linearized model at that point will have $D=0$. For example, if $h(u) = u^2$, the system has direct feedthrough in general, but at the operating point $u^\star=0$, the Jacobian $D = \left.2u\right|_{u=0} = 0$, and the linearized model shows no direct feedthrough.

### Beyond Equilibrium Points: Advanced Topics and Limitations

Linearization is not confined to equilibrium points, nor is it universally applicable. Understanding its limitations and extensions is crucial for advanced analysis.

#### When Linearization Fails: Non-hyperbolic Equilibria

Lyapunov's indirect method is silent when the equilibrium is **non-hyperbolic**, meaning the Jacobian matrix $A$ has one or more eigenvalues on the [imaginary axis](@entry_id:262618) ($\text{Re}(\lambda_i) = 0$). In this critical case, the neglected higher-order terms of the Taylor expansion determine the stability, and the linear model is an unreliable predictor.

As a classic example, consider the system [@problem_id:2720587]:
$$
\begin{aligned}
\dot{x} = -y - \alpha x(x^2+y^2) \\
\dot{y} = x - \alpha y(x^2+y^2)
\end{aligned}
$$
The [linearization](@entry_id:267670) at the origin $(0,0)$ gives $A = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}$, with eigenvalues $\lambda = \pm i$. The linear system is a center, exhibiting neutral stability (circles). The stability of the [nonlinear system](@entry_id:162704), however, depends entirely on the sign of $\alpha$. By analyzing the dynamics of the radius $r = \sqrt{x^2+y^2}$, we find the exact relation $\dot{r} = -\alpha r^3$.
*   If $\alpha > 0$, then $\dot{r}  0$, and trajectories spiral into the origin (asymptotically stable).
*   If $\alpha  0$, then $\dot{r} > 0$, and trajectories spiral away from the origin (unstable).
*   If $\alpha = 0$, the system is purely linear, and trajectories are circles (neutrally stable).

This example definitively shows that for non-hyperbolic cases, the nonlinear terms are not just small errors; they are the deciding factor for stability.

When faced with an inconclusive [linearization](@entry_id:267670), especially in control design, more advanced techniques are required. Linear controllers designed for the inconclusive linear model may fail. A powerful approach is to construct a **Control Lyapunov Function (CLF)** that explicitly incorporates the critical nonlinearities. For a system like $\dot{x}_1 = x_2, \dot{x}_2 = -x_1^3+u$, whose linearization at the origin is a double integrator with eigenvalues $\lambda=0,0$, a linear controller may be insufficient. Instead, one can propose a CLF candidate like $V(x) = \frac{1}{4}x_1^4 + \frac{1}{2}x_2^2$. This "energy-like" function is built from the nonlinear potential term. Choosing a [nonlinear control](@entry_id:169530) law such as $u=-kx_2$ can then be shown to render $\dot{V} \le 0$, proving stability where linear methods could not [@problem_id:2721954].

#### Linearization around Trajectories: The Poincaré Map

Linearization can be extended from [static equilibrium](@entry_id:163498) points to dynamic **periodic orbits** (or [limit cycles](@entry_id:274544)). To analyze the stability of an orbit $\Gamma$, we introduce a tool from [dynamical systems theory](@entry_id:202707): the **Poincaré map**.

Imagine a local, [codimension](@entry_id:273141)-one surface $\Sigma$, called a **Poincaré section**, that is transverse to the flow of the system. A trajectory starting at a point $x_k$ on $\Sigma$ will, after some time, return to intersect $\Sigma$ at a new point $x_{k+1}$. The **Poincaré map** $P$ is the function that maps $x_k$ to $x_{k+1}$, i.e., $x_{k+1} = P(x_k)$.

A periodic orbit $\Gamma$ that intersects $\Sigma$ at a point $x^\star$ corresponds to a **fixed point** of the Poincaré map, since $P(x^\star) = x^\star$. The stability of the continuous-time orbit $\Gamma$ is equivalent to the stability of the discrete-time fixed point $x^\star$ under the map $P$. We can now apply linearization to this map. The behavior of the map near the fixed point is approximated by its Jacobian:
$$
\delta x_{k+1} \approx DP(x^\star) \delta x_k
$$
where $\delta x_k = x_k - x^\star$ and $DP(x^\star)$ is the Jacobian of $P$ at $x^\star$. The stability of the orbit is then determined by the eigenvalues of $DP(x^\star)$:
1.  If all eigenvalues of $DP(x^\star)$ have magnitude less than 1 ($|\lambda_i|  1$), the fixed point is stable, and the [periodic orbit](@entry_id:273755) $\Gamma$ is **asymptotically stable**.
2.  If any eigenvalue has magnitude greater than 1 ($|\lambda_i| > 1$), the orbit is **unstable**.

For the system $\dot{r} = -k_r(r-r_0), \dot{\theta}=\omega_0, \dot{z}=-k_z z$ [@problem_id:2720593], there is a circular orbit at $r=r_0, z=0$. Choosing the Poincaré section at $\theta=0$, the return map for perturbations $(\delta r, \delta z)$ can be found by integrating the decoupled equations for one full period $T_0 = 2\pi/\omega_0$. The map is $P(\delta r, \delta z) = (\delta r \cdot e^{-k_r T_0}, \delta z \cdot e^{-k_z T_0})$. This map is already linear, so its Jacobian is simply $DP = \text{diag}(e^{-k_r T_0}, e^{-k_z T_0})$. Since $k_r, k_z, T_0 > 0$, both eigenvalues have magnitude less than 1, proving the orbit is asymptotically stable. This powerful technique reduces the stability problem of a continuous trajectory to the stability problem of a discrete map at a single point.