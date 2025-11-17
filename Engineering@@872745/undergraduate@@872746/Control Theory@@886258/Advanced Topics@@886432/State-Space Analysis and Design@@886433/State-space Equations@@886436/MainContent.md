## Introduction
In the study of dynamic systems, the transfer function offers a powerful input-output perspective. However, it often treats the system as a "black box," obscuring the rich internal dynamics that govern its behavior. To gain deeper insight and to effectively control more complex, multi-input, multi-output (MIMO) systems, we turn to the [state-space representation](@entry_id:147149)—a time-domain framework that provides a complete and transparent model of a system's internal state. This approach forms the bedrock of modern control theory, enabling sophisticated analysis and design techniques that are impossible with classical methods alone.

This article provides a comprehensive exploration of state-space equations. In "Principles and Mechanisms," we will dissect the core theory, learning how to construct [state-space models](@entry_id:137993) from physical principles and [transfer functions](@entry_id:756102), solve the [state equations](@entry_id:274378), and analyze fundamental properties like stability, controllability, and [observability](@entry_id:152062). Following this, "Applications and Interdisciplinary Connections" will demonstrate the immense practical power of this framework by showcasing its use in modeling and controlling systems across electrical, mechanical, economic, and biological domains. Finally, "Hands-On Practices" will provide guided problems to help you apply these concepts and solidify your understanding of this essential control engineering tool.

## Principles and Mechanisms

While the transfer function provides a concise input-output description of a linear time-invariant (LTI) system, it treats the system as a "black box." It reveals how the output responds to an input but offers limited insight into the internal workings of the system. To overcome this limitation and to facilitate the analysis and design of more complex systems—particularly those with multiple inputs and outputs (MIMO)—we turn to the [state-space representation](@entry_id:147149). This powerful time-domain framework provides a complete description of a system's internal dynamic behavior.

### The State-Space Representation

The core idea of the [state-space](@entry_id:177074) approach is to describe the system's dynamics using a set of [first-order differential equations](@entry_id:173139). This is accomplished by defining a **state vector**, denoted by $\mathbf{x}(t)$, which is a column vector of the smallest set of variables, known as **[state variables](@entry_id:138790)**, whose values at any time $t_0$, combined with knowledge of the input signal for all $t \ge t_0$, are sufficient to uniquely determine the behavior of the system for all $t \ge t_0$. Intuitively, the [state vector](@entry_id:154607) captures the "memory" or internal condition of the system at any instant.

For an LTI system with $n$ [state variables](@entry_id:138790), $m$ inputs, and $p$ outputs, the standard [state-space representation](@entry_id:147149) consists of two equations:

1.  The **State Equation**, which describes the evolution of the state variables:
    $$ \dot{\mathbf{x}}(t) = \mathbf{A}\mathbf{x}(t) + \mathbf{B}\mathbf{u}(t) $$

2.  The **Output Equation**, which relates the [state variables](@entry_id:138790) and inputs to the system's measurable outputs:
    $$ \mathbf{y}(t) = \mathbf{C}\mathbf{x}(t) + \mathbf{D}\mathbf{u}(t) $$

Here, $\mathbf{x}(t)$ is the $n \times 1$ state vector, $\mathbf{u}(t)$ is the $m \times 1$ input vector, and $\mathbf{y}(t)$ is the $p \times 1$ output vector. The matrices are constant and have dimensions that ensure compatibility:
*   $\mathbf{A}$ is the $n \times n$ **state matrix** (or [system matrix](@entry_id:172230)). It governs the internal dynamics of the system and determines its stability.
*   $\mathbf{B}$ is the $n \times m$ **input matrix** (or control matrix). It specifies how the inputs affect the state variables.
*   $\mathbf{C}$ is the $p \times n$ **output matrix**. It determines how the state variables are combined to form the outputs.
*   $\mathbf{D}$ is the $p \times m$ **feedthrough matrix** (or direct transmission matrix). It represents a direct connection from the system's input to its output, which is often zero for strictly proper physical systems.

### Constructing State-Space Models

A [state-space model](@entry_id:273798) can be derived from the system's governing differential equations or from its transfer function.

#### From Differential Equations

The most direct method for obtaining a [state-space model](@entry_id:273798) is to start from the system's physical laws, which are typically expressed as high-order differential equations. A common and systematic approach is to choose the output variable and its successive derivatives as the [state variables](@entry_id:138790). This leads to a specific structure known as the **controller canonical form**.

Consider a general $n$-th order single-input, single-output (SISO) system described by the differential equation:
$$ \frac{d^n y}{dt^n} + a_{n-1} \frac{d^{n-1} y}{dt^{n-1}} + \dots + a_1 \frac{dy}{dt} + a_0 y = b_0 u(t) $$
We can define a set of state variables, known as phase variables, as follows:
$$ x_1 = y, \quad x_2 = \dot{y}, \quad x_3 = \ddot{y}, \quad \dots, \quad x_n = y^{(n-1)} $$
Differentiating these definitions, we get the first $n-1$ [state equations](@entry_id:274378):
$$ \dot{x}_1 = \dot{y} = x_2 $$
$$ \dot{x}_2 = \ddot{y} = x_3 $$
$$ \vdots $$
$$ \dot{x}_{n-1} = y^{(n-1)} = x_n $$
The final state equation, for $\dot{x}_n$, is obtained by rearranging the original differential equation to solve for the highest derivative, $y^{(n)}$:
$$ \dot{x}_n = y^{(n)} = -a_0 x_1 - a_1 x_2 - \dots - a_{n-1} x_n + b_0 u(t) $$

As an illustration, let's model a chemical process whose dynamics are given by a third-order differential equation [@problem_id:1614939]:
$$ \frac{d^3y}{dt^3} + 5 \frac{d^2y}{dt^2} + 8 \frac{dy}{dt} + 4y = 2u(t) $$
Following the phase-variable convention, we set $x_1 = y$, $x_2 = \dot{y}$, and $x_3 = \ddot{y}$. The [state equations](@entry_id:274378) are:
$$ \dot{x}_1 = x_2 $$
$$ \dot{x}_2 = x_3 $$
$$ \dot{x}_3 = -4x_1 - 8x_2 - 5x_3 + 2u(t) $$
The output is simply $y = x_1$. Writing these equations in matrix form yields:
$$ \dot{\mathbf{x}} = \begin{pmatrix} 0  1  0 \\ 0  0  1 \\ -4  -8  -5 \end{pmatrix} \mathbf{x} + \begin{pmatrix} 0 \\ 0 \\ 2 \end{pmatrix} u(t) $$
$$ y = \begin{pmatrix} 1  0  0 \end{pmatrix} \mathbf{x} + [0] u(t) $$
This gives the matrices $\mathbf{A}$, $\mathbf{B}$, $\mathbf{C}$, and $\mathbf{D}$ for the controller [canonical form](@entry_id:140237).

State-space models can also be constructed directly from a system's [block diagram](@entry_id:262960) or [signal-flow graph](@entry_id:173950), often described in the Laplace domain. One must simply translate the relationships between variables back to the time domain, recalling that multiplication by $s$ in the Laplace domain corresponds to differentiation in the time domain (assuming zero [initial conditions](@entry_id:152863)) [@problem_id:1614957].

#### From Transfer Functions

It is often necessary to find a [state-space realization](@entry_id:166670) for a given transfer function $G(s) = Y(s)/U(s)$. It's important to recognize that for any given transfer function, there exist infinitely many valid state-space representations. The controller canonical form provides a standardized method for this conversion.

For a strictly proper transfer function with a monic denominator:
$$ G(s) = \frac{b_{n-1}s^{n-1} + \dots + b_1s + b_0}{s^n + a_{n-1}s^{n-1} + \dots + a_1s + a_0} $$
The controller [canonical form](@entry_id:140237) is given by:
$$ \mathbf{A} = \begin{pmatrix} 0  1  0  \cdots  0 \\ 0  0  1  \cdots  0 \\ \vdots  \vdots  \vdots  \ddots  \vdots \\ 0  0  0  \cdots  1 \\ -a_0  -a_1  -a_2  \cdots  -a_{n-1} \end{pmatrix}, \quad \mathbf{B} = \begin{pmatrix} 0 \\ 0 \\ \vdots \\ 0 \\ 1 \end{pmatrix} $$
$$ \mathbf{C} = \begin{pmatrix} b_0  b_1  \cdots  b_{n-1} \end{pmatrix}, \quad \mathbf{D} = [0] $$
Notice that the coefficients of the denominator polynomial form the last row of $\mathbf{A}$ (negated), while the coefficients of the numerator polynomial form the $\mathbf{C}$ matrix.

For example, consider the transfer function [@problem_id:1614923]:
$$ G(s) = \frac{1}{s^3 + 3s^2 + 2s + 1} $$
Here, $n=3$, the denominator coefficients are $a_2=3, a_1=2, a_0=1$, and the numerator is $q(s) = 1$, which means $b_2=0, b_1=0, b_0=1$. Applying the formula for the controller canonical form, we immediately obtain the state-space matrices:
$$ \mathbf{A} = \begin{pmatrix} 0  1  0 \\ 0  0  1 \\ -1  -2  -3 \end{pmatrix}, \quad \mathbf{B} = \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix}, \quad \mathbf{C} = \begin{pmatrix} 1  0  0 \end{pmatrix}, \quad \mathbf{D} = [0] $$

### The Relationship to Transfer Functions

We can reverse the process and derive the transfer function from a [state-space model](@entry_id:273798). This demonstrates the fundamental equivalence of the input-output behavior described by both representations. We start by taking the Laplace transform of the state and output equations, assuming zero [initial conditions](@entry_id:152863):
$$ s\mathbf{X}(s) = \mathbf{A}\mathbf{X}(s) + \mathbf{B}\mathbf{U}(s) $$
$$ \mathbf{Y}(s) = \mathbf{C}\mathbf{X}(s) + \mathbf{D}\mathbf{U}(s) $$
From the state equation, we can solve for the [state vector](@entry_id:154607) $\mathbf{X}(s)$:
$$ (s\mathbf{I} - \mathbf{A})\mathbf{X}(s) = \mathbf{B}\mathbf{U}(s) \implies \mathbf{X}(s) = (s\mathbf{I} - \mathbf{A})^{-1}\mathbf{B}\mathbf{U}(s) $$
Substituting this into the output equation gives:
$$ \mathbf{Y}(s) = \mathbf{C}\left[(s\mathbf{I} - \mathbf{A})^{-1}\mathbf{B}\mathbf{U}(s)\right] + \mathbf{D}\mathbf{U}(s) = \left[\mathbf{C}(s\mathbf{I} - \mathbf{A})^{-1}\mathbf{B} + \mathbf{D}\right]\mathbf{U}(s) $$
The term in the brackets is the [transfer function matrix](@entry_id:271746) $\mathbf{G}(s)$. For a SISO system, this is a scalar transfer function $G(s)$.

Let's apply this formula to find the transfer function for a system defined by the matrices [@problem_id:1614943]:
$$ \mathbf{A} = \begin{pmatrix} -3  1 \\ 0  -2 \end{pmatrix}, \quad \mathbf{B} = \begin{pmatrix} 0 \\ 1 \end{pmatrix}, \quad \mathbf{C} = \begin{pmatrix} 1  0 \end{pmatrix}, \quad \mathbf{D} = [0] $$
First, we compute the matrix $(s\mathbf{I} - \mathbf{A})$ and its inverse:
$$ s\mathbf{I} - \mathbf{A} = \begin{pmatrix} s+3  -1 \\ 0  s+2 \end{pmatrix} $$
$$ (s\mathbf{I} - \mathbf{A})^{-1} = \frac{1}{(s+3)(s+2)} \begin{pmatrix} s+2  1 \\ 0  s+3 \end{pmatrix} = \begin{pmatrix} \frac{1}{s+3}  \frac{1}{(s+3)(s+2)} \\ 0  \frac{1}{s+2} \end{pmatrix} $$
Now, we pre-multiply by $\mathbf{C}$ and post-multiply by $\mathbf{B}$:
$$ G(s) = \begin{pmatrix} 1  0 \end{pmatrix} \begin{pmatrix} \frac{1}{s+3}  \frac{1}{(s+3)(s+2)} \\ 0  \frac{1}{s+2} \end{pmatrix} \begin{pmatrix} 0 \\ 1 \end{pmatrix} + 0 $$
$$ G(s) = \begin{pmatrix} \frac{1}{s+3}  \frac{1}{(s+3)(s+2)} \end{pmatrix} \begin{pmatrix} 0 \\ 1 \end{pmatrix} = \frac{1}{(s+3)(s+2)} = \frac{1}{s^2 + 5s + 6} $$
The denominator of the transfer function, $s^2 + 5s + 6$, is the characteristic polynomial of the matrix $\mathbf{A}$, $\det(s\mathbf{I} - \mathbf{A})$. This is a general property: the poles of the transfer function are a subset of the eigenvalues of the state matrix $\mathbf{A}$.

### Solving the State Equation

Solving the state differential equation gives us the trajectory of the state vector over time.

#### The State Transition Matrix

Let's first consider the unforced (or homogeneous) system, where the input $\mathbf{u}(t)$ is zero:
$$ \dot{\mathbf{x}}(t) = \mathbf{A}\mathbf{x}(t) $$
This is a vector-matrix version of the simple scalar equation $\dot{x} = ax$, whose solution is $x(t) = e^{at}x(0)$. By analogy, the solution to the matrix equation is:
$$ \mathbf{x}(t) = e^{\mathbf{A}t} \mathbf{x}(0) $$
The matrix $e^{\mathbf{A}t}$, often denoted $\mathbf{\Phi}(t)$, is called the **[state transition matrix](@entry_id:267928)**. It "transitions" the state from its initial value $\mathbf{x}(0)$ to its value at time $t$. The [matrix exponential](@entry_id:139347) is defined by its Taylor [series expansion](@entry_id:142878), which is analogous to the scalar case:
$$ e^{\mathbf{A}t} = \mathbf{I} + \mathbf{A}t + \frac{(\mathbf{A}t)^2}{2!} + \frac{(\mathbf{A}t)^3}{3!} + \dots = \sum_{k=0}^{\infty} \frac{\mathbf{A}^k t^k}{k!} $$
For a [diagonal matrix](@entry_id:637782) $\mathbf{A}$, the calculation is simple. However, for more general matrices, other techniques are required. For example, if a matrix $\mathbf{A}$ can be decomposed as $\mathbf{A} = -\mathbf{aI} + \mathbf{N}$, where $\mathbf{N}$ is a [nilpotent matrix](@entry_id:152732) (i.e., $\mathbf{N}^k = \mathbf{0}$ for some integer $k$), the series may truncate. Consider the [system matrix](@entry_id:172230) for a damped system [@problem_id:1614977]:
$$ \mathbf{A} = \begin{pmatrix} -a  1 \\ 0  -a \end{pmatrix} $$
We can write $\mathbf{A} = -a\mathbf{I} + \mathbf{N}$, where $\mathbf{N} = \begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix}$. Since $\mathbf{I}$ and $\mathbf{N}$ commute, $e^{\mathbf{A}t} = e^{(-a\mathbf{I} + \mathbf{N})t} = e^{-a\mathbf{I}t}e^{\mathbf{N}t}$. The first term is $e^{-at}\mathbf{I}$. For the second term, we note that $\mathbf{N}^2 = \mathbf{0}$, so the series for $e^{\mathbf{N}t}$ truncates:
$$ e^{\mathbf{N}t} = \mathbf{I} + \mathbf{N}t + \frac{(\mathbf{N}t)^2}{2!} + \dots = \mathbf{I} + \mathbf{N}t = \begin{pmatrix} 1  t \\ 0  1 \end{pmatrix} $$
Combining these results, the [state transition matrix](@entry_id:267928) is:
$$ \mathbf{\Phi}(t) = e^{\mathbf{A}t} = e^{-at}\mathbf{I} (\mathbf{I} + \mathbf{N}t) = e^{-at}\begin{pmatrix} 1  t \\ 0  1 \end{pmatrix} = \begin{pmatrix} e^{-at}  t e^{-at} \\ 0  e^{-at} \end{pmatrix} $$

#### The Complete Solution

To find the solution for the full, forced LTI system $\dot{\mathbf{x}} = \mathbf{A}\mathbf{x} + \mathbf{B}\mathbf{u}$, we can use a method analogous to the [variation of parameters](@entry_id:173919) for scalar ODEs. This leads to the complete solution, which is the sum of the response to the [initial conditions](@entry_id:152863) and the response to the input signal [@problem_id:1614961]:
$$ \mathbf{x}(t) = \underbrace{e^{\mathbf{A}t}\mathbf{x}(0)}_{\text{Zero-Input Response}} + \underbrace{\int_{0}^{t} e^{\mathbf{A}(t-\tau)}\mathbf{B}\mathbf{u}(\tau) d\tau}_{\text{Zero-State Response}} $$
This fundamental equation is known as the [variation of constants](@entry_id:196393) formula. The first term, the **[zero-input response](@entry_id:274925)**, describes how the system evolves from its initial state $\mathbf{x}(0)$ in the absence of any input. The second term, the **[zero-state response](@entry_id:273280)**, describes the system's evolution due to the input $\mathbf{u}(t)$, assuming it started from a zero initial state ($\mathbf{x}(0) = \mathbf{0}$). The integral in this term is a **convolution integral**, representing the cumulative effect of the input signal over the interval $[0, t]$, with each input "impulse" $u(\tau)$ being propagated forward in time by the [state transition matrix](@entry_id:267928) $e^{\mathbf{A}(t-\tau)}$.

### Fundamental System Properties

The [state-space representation](@entry_id:147149) allows us to analyze key structural properties of a system, namely stability, [controllability](@entry_id:148402), and observability.

#### Stability

For an LTI system, stability refers to the behavior of the unforced response. An [equilibrium point](@entry_id:272705) (e.g., $\mathbf{x}=\mathbf{0}$) is **asymptotically stable** if any trajectory starting near it converges to it as $t \to \infty$. This behavior is determined entirely by the eigenvalues of the state matrix $\mathbf{A}$. The modes of the system's free response are combinations of terms like $e^{\lambda_i t}$, where $\lambda_i$ are the eigenvalues of $\mathbf{A}$. For the state vector to decay to zero, all these modal terms must decay. This leads to the fundamental stability theorem for LTI systems:

The system $\dot{\mathbf{x}} = \mathbf{A}\mathbf{x}$ is asymptotically stable if and only if all eigenvalues of $\mathbf{A}$ have strictly negative real parts.

If any eigenvalue has a positive real part, the system is unstable. If one or more non-[repeated eigenvalues](@entry_id:154579) have zero real parts while all others have negative real parts, the system is marginally stable.

To determine the stability of a system with the state matrix [@problem_id:1614921]:
$$ \mathbf{A} = \begin{pmatrix} 0  1 \\ -8  -6 \end{pmatrix} $$
we find its eigenvalues by solving the [characteristic equation](@entry_id:149057) $\det(\lambda\mathbf{I} - \mathbf{A}) = 0$:
$$ \det \begin{pmatrix} \lambda  -1 \\ 8  \lambda+6 \end{pmatrix} = \lambda(\lambda+6) - (-1)(8) = \lambda^2 + 6\lambda + 8 = 0 $$
This equation factors as $(\lambda+2)(\lambda+4) = 0$, giving eigenvalues $\lambda_1 = -2$ and $\lambda_2 = -4$. Since both eigenvalues are real and strictly negative, the system is asymptotically stable.

#### Controllability

Controllability addresses the question: Is it possible to steer the state of a system from any initial state $\mathbf{x}(0)$ to any desired final state $\mathbf{x}(t_f)$ in a finite time $t_f$ by applying some control input $\mathbf{u}(t)$? A system for which this is possible is said to be **completely state controllable**.

The ability to control a system depends on whether the input $\mathbf{B}$ can influence all the system's dynamic modes (related to the eigenvectors of $\mathbf{A}$). The definitive test is the **Kalman rank condition for controllability**. An $n$-dimensional system $(\mathbf{A}, \mathbf{B})$ is controllable if and only if its **[controllability matrix](@entry_id:271824)**, $\mathcal{C}$, has full rank ($n$):
$$ \mathcal{C} = \begin{pmatrix} \mathbf{B}  \mathbf{A}\mathbf{B}  \mathbf{A}^2\mathbf{B}  \cdots  \mathbf{A}^{n-1}\mathbf{B} \end{pmatrix} $$
If the rank of $\mathcal{C}$ is less than $n$, the system is uncontrollable. This means there are certain states or combinations of states that cannot be affected by the input, regardless of how the control signal is chosen.

Consider a simplified model of a satellite's attitude dynamics [@problem_id:1614945] with matrices:
$$ \mathbf{A} = \begin{pmatrix} 0  1  0 \\ 0  0  0 \\ 0  0  0 \end{pmatrix}, \quad \mathbf{B} = \begin{pmatrix} 0 \\ -\alpha \\ 1 \end{pmatrix} $$
where $\alpha > 0$. The state vector represents angle, angular velocity, and [reaction wheel](@entry_id:178763) momentum. To check for [controllability](@entry_id:148402), we construct the [controllability matrix](@entry_id:271824) for this $n=3$ system:
$$ \mathbf{A}\mathbf{B} = \begin{pmatrix} -\alpha \\ 0 \\ 0 \end{pmatrix}, \quad \mathbf{A}^2\mathbf{B} = \mathbf{A}\begin{pmatrix} -\alpha \\ 0 \\ 0 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \\ 0 \end{pmatrix} $$
The [controllability matrix](@entry_id:271824) is:
$$ \mathcal{C} = \begin{pmatrix} \mathbf{B}  \mathbf{A}\mathbf{B}  \mathbf{A}^2\mathbf{B} \end{pmatrix} = \begin{pmatrix} 0  -\alpha  0 \\ -\alpha  0  0 \\ 1  0  0 \end{pmatrix} $$
The third column is all zeros, and the first two columns are not parallel (since $\alpha>0$). Therefore, the columns span a two-dimensional space, and $\text{rank}(\mathcal{C}) = 2$. Since the rank is less than the state dimension $n=3$, the system is uncontrollable. There is an underlying physical reason: from the [state equations](@entry_id:274378) $\dot{x}_2 = -\alpha u$ and $\dot{x}_3 = u$, we see that $\frac{d}{dt}(x_2 + \alpha x_3) = \dot{x}_2 + \alpha \dot{x}_3 = -\alpha u + \alpha u = 0$. The quantity $x_2 + \alpha x_3$ is conserved, meaning the input cannot change its value. The system is constrained to a subspace, and arbitrary states are unreachable.

#### Observability

Observability is the dual concept to [controllability](@entry_id:148402). It addresses the question: Is it possible to determine the initial state of the system, $\mathbf{x}(0)$, by observing the system's output $\mathbf{y}(t)$ over a finite time interval $[0, t_f]$? A system for which this is possible is said to be **observable**. If a system is not observable, it means some of its internal states or dynamic modes have no effect on the output and are therefore "hidden" from the observer.

The test for observability is the **Kalman rank condition for observability**. A system $(\mathbf{A}, \mathbf{C})$ is observable if and only if its **[observability matrix](@entry_id:165052)**, $\mathcal{O}$, has full rank ($n$):
$$ \mathcal{O} = \begin{pmatrix} \mathbf{C} \\ \mathbf{C}\mathbf{A} \\ \mathbf{C}\mathbf{A}^2 \\ \vdots \\ \mathbf{C}\mathbf{A}^{n-1} \end{pmatrix} $$
Unobservability arises when a specific mode of the system is orthogonal to the output mapping. This can happen if sensors are placed at the nodes of a particular vibrational [mode shape](@entry_id:168080). Consider a two-[mass-spring system](@entry_id:267496) where the output is a weighted difference of the positions, $y(t) = x_1(t) - \gamma x_2(t)$ [@problem_id:1614927]. This system has [natural modes](@entry_id:277006) of vibration, each with a characteristic shape (a ratio of displacements $v_1/v_2$). If the sensor parameter $\gamma$ is chosen such that it equals the [mode shape](@entry_id:168080) ratio for a particular mode, i.e., $\gamma = v_1/v_2$, then for that mode of vibration, the output will be $y(t) = v_1 - (v_1/v_2)v_2 = 0$ at all times. This specific mode is rendered unobservable by this choice of sensor configuration. For the lower frequency mode of the system in the problem, this critical value is $\gamma = (\sqrt{5}-1)/2$. This demonstrates that observability is a joint property of the [system dynamics](@entry_id:136288) ($\mathbf{A}$) and the sensor configuration ($\mathbf{C}$).

### Non-Uniqueness and State Transformations

As mentioned, the choice of [state variables](@entry_id:138790) for a system is not unique. Any [invertible linear transformation](@entry_id:149915) of the state vector, $\mathbf{z} = \mathbf{T}\mathbf{x}$, results in a new, valid state vector $\mathbf{z}$ and an equivalent [state-space representation](@entry_id:147149).

If we substitute $\mathbf{x} = \mathbf{T}^{-1}\mathbf{z}$ into the original [state-space](@entry_id:177074) equations, we can find the new system matrices $(\mathbf{A}_z, \mathbf{B}_z, \mathbf{C}_z, \mathbf{D}_z)$:
$$ \dot{\mathbf{z}} = \mathbf{T}\dot{\mathbf{x}} = \mathbf{T}(\mathbf{A}\mathbf{x} + \mathbf{B}u) = \mathbf{T}\mathbf{A}(\mathbf{T}^{-1}\mathbf{z}) + \mathbf{T}\mathbf{B}u $$
$$ y = \mathbf{C}\mathbf{x} + \mathbf{D}u = \mathbf{C}(\mathbf{T}^{-1}\mathbf{z}) + \mathbf{D}u $$
This yields the transformation rules:
$$ \mathbf{A}_z = \mathbf{T}\mathbf{A}\mathbf{T}^{-1} $$
$$ \mathbf{B}_z = \mathbf{T}\mathbf{B} $$
$$ \mathbf{C}_z = \mathbf{C}\mathbf{T}^{-1} $$
$$ \mathbf{D}_z = \mathbf{D} $$
The transformation on the state matrix, $\mathbf{A}_z = \mathbf{T}\mathbf{A}\mathbf{T}^{-1}$, is a **[similarity transformation](@entry_id:152935)**. A key property of similarity transformations is that they preserve eigenvalues. This means that although the matrices $\mathbf{A}$ and $\mathbf{A}_z$ may look very different, their eigenvalues are identical. Consequently, fundamental system properties that depend on these eigenvalues, such as stability, are invariant under a change of [state variables](@entry_id:138790). The input-output relationship, i.e., the transfer function, is also preserved.

For instance, consider a system with the controller [canonical form](@entry_id:140237) [@problem_id:1614950]:
$$ \mathbf{A} = \begin{pmatrix} 0  1 \\ -6  -5 \end{pmatrix} $$
If we apply the state transformation with $\mathbf{T} = \begin{pmatrix} 2  1 \\ 3  1 \end{pmatrix}$, we must first find its inverse, $\mathbf{T}^{-1} = \begin{pmatrix} -1  1 \\ 3  -2 \end{pmatrix}$. The new state matrix $\mathbf{A}_z$ is then calculated as:
$$ \mathbf{A}_z = \mathbf{T}\mathbf{A}\mathbf{T}^{-1} = \begin{pmatrix} 2  1 \\ 3  1 \end{pmatrix} \begin{pmatrix} 0  1 \\ -6  -5 \end{pmatrix} \begin{pmatrix} -1  1 \\ 3  -2 \end{pmatrix} = \begin{pmatrix} -3  0 \\ 0  -2 \end{pmatrix} $$
The transformation has diagonalized the state matrix. This new representation, called the **diagonal canonical form**, is particularly insightful because the system's eigenvalues, $\lambda_1 = -3$ and $\lambda_2 = -2$, appear directly on the diagonal. The dynamics of the new state variables $z_1$ and $z_2$ are decoupled: $\dot{z}_1 = -3z_1$ and $\dot{z}_2 = -2z_2$. This demonstrates the power of state transformations in simplifying analysis and revealing the underlying structure of a system.