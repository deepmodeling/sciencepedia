## Introduction
In the study of dynamic systems, a robust mathematical model is essential for analysis and control. While classical control theory often views systems as 'black boxes' defined by their input-output relationships, this perspective can obscure the rich internal dynamics that govern system behavior. Modern control theory addresses this limitation by introducing the [state-space representation](@entry_id:147149), a powerful framework that provides a complete internal description of a system.

This article delves into the foundational elements of this approach: the state variable and the [state vector](@entry_id:154607). It bridges the gap between abstract differential equations and the physical reality of dynamic systems, showing how to select a minimal set of variables that encapsulate a system's entire history and dictate its future trajectory.

You will begin by exploring the core **Principles and Mechanisms** behind state variables, learning how to derive them from physical laws and higher-order equations. Next, the article showcases the framework's versatility through a tour of **Applications and Interdisciplinary Connections**, demonstrating how the same concepts model everything from robotic arms to economic trends. Finally, you will apply your knowledge with a series of **Hands-On Practices** designed to solidify these essential modeling skills. By the end, you will have a firm grasp of how to translate complex dynamic phenomena into the structured, universal language of [state-space analysis](@entry_id:266177).

## Principles and Mechanisms

The analysis and design of [control systems](@entry_id:155291) are predicated on a robust mathematical description of the system's behavior. While classical control theory often relies on input-output relationships, such as [transfer functions](@entry_id:756102), modern control theory adopts a more comprehensive internal perspective through the [state-space representation](@entry_id:147149). This approach centers on the concept of the system's **state**, a powerful construct that provides a complete summary of the system's history, enabling the prediction of its future evolution. This chapter elucidates the fundamental principles underlying the selection and use of state variables and the formulation of the state vector.

### The Concept of System State

At any moment in time, a dynamic system possesses an internal condition that is the result of its past inputs and evolution. The **state** of a system is defined as the minimal set of variables, known as **state variables**, whose values at a time $t_0$, in conjunction with the system's input for all subsequent times $t \ge t_0$, are sufficient to uniquely determine the system's behavior for all $t \ge t_0$. The key elements of this definition are "minimal" and "sufficient." The set must contain enough information to be predictive, but no more than is necessary, avoiding redundancy.

These state variables, denoted as $x_1(t), x_2(t), \ldots, x_n(t)$, are collected into a column vector called the **state vector**, $\mathbf{x}(t)$.

$$
\mathbf{x}(t) = \begin{pmatrix} x_1(t) \\ x_2(t) \\ \vdots \\ x_n(t) \end{pmatrix}
$$

The number of state variables, $n$, is the **order** of the system and defines the dimensionality of the **state space**, which is the $n$-dimensional vector space where the state vector "lives." The evolution of the [state vector](@entry_id:154607) is described by a first-order vector differential equation known as the **state equation**, which, for a linear time-invariant (LTI) system, takes the form:

$$
\dot{\mathbf{x}}(t) = A\mathbf{x}(t) + B\mathbf{u}(t)
$$

Here, $\mathbf{u}(t)$ is the vector of control inputs, $A$ is the **state matrix**, and $B$ is the **input matrix**. The system's measurable outputs, $\mathbf{y}(t)$, are related to the state and input through the **output equation**:

$$
\mathbf{y}(t) = C\mathbf{x}(t) + D\mathbf{u}(t)
$$

where $C$ is the **output matrix** and $D$ is the **feedthrough matrix**. The primary task in modeling is to select a valid set of [state variables](@entry_id:138790) and then derive these four matrices.

### State Variables in Physical Systems

For systems grounded in physical laws, a powerful heuristic for selecting [state variables](@entry_id:138790) is to identify the system's independent [energy storage](@entry_id:264866) elements. The variables that characterize the energy stored in these elements are excellent candidates for [state variables](@entry_id:138790) because they typically cannot change instantaneously. An abrupt change in stored energy would imply infinite power, which is physically impossible.

#### Mechanical Systems

In mechanical systems, energy is stored in elements that have mass (kinetic energy, $\frac{1}{2}mv^2$) and in compliant elements like springs (potential energy, $\frac{1}{2}kx^2$). Consequently, variables like position and velocity are natural choices.

Consider a simplified model of a car with mass $m$ moving along a straight line [@problem_id:1614433]. Its kinetic energy depends on its velocity, $v(t)$, and its position, $p(t)$, is the integral of its velocity. These two quantities are independent and capture the dynamic history of the vehicle. Let's define the [state vector](@entry_id:154607) as $\mathbf{x}(t) = \begin{pmatrix} p(t) \\ v(t) \end{pmatrix}$. The system is influenced by an engine thrust $F(t)$ (the input) and a drag force $-bv(t)$. The first state equation is purely kinematic: the rate of change of position is velocity.

$$
\dot{p}(t) = v(t)
$$

The second equation comes from Newton's Second Law, $\sum F = ma$:

$$
m \dot{v}(t) = F(t) - b v(t) \implies \dot{v}(t) = -\frac{b}{m} v(t) + \frac{1}{m} F(t)
$$

Arranging these into the [standard state](@entry_id:145000)-[space form](@entry_id:203017) $\dot{\mathbf{x}} = A\mathbf{x} + B u$ gives:

$$
\frac{d}{dt} \begin{pmatrix} p(t) \\ v(t) \end{pmatrix} = \begin{pmatrix} 0 & 1 \\ 0 & -\frac{b}{m} \end{pmatrix} \begin{pmatrix} p(t) \\ v(t) \end{pmatrix} + \begin{pmatrix} 0 \\ \frac{1}{m} \end{pmatrix} F(t)
$$

Thus, the state matrix is $A = \begin{pmatrix} 0 & 1 \\ 0 & -b/m \end{pmatrix}$ and the input matrix is $B = \begin{pmatrix} 0 \\ 1/m \end{pmatrix}$. This illustrates a direct path from first principles of physics to a [state-space representation](@entry_id:147149).

#### Electrical Circuits

In electrical circuits, energy is stored in capacitors (electric field, $E = \frac{1}{2}CV^2$) and inductors (magnetic field, $E = \frac{1}{2}LI^2$). The voltage across a capacitor and the current through an inductor cannot change instantaneously. This makes them the default choice for [state variables](@entry_id:138790).

For a circuit with multiple energy storage elements, the number of independent elements determines the order of the system. In a two-stage RC filter, there are two capacitors, $C_1$ and $C_2$. Their stored energies are independent. Therefore, the system is second-order, and a valid state vector is formed by the two capacitor voltages: $\mathbf{x}(t) = \begin{pmatrix} v_{C1}(t) \\ v_{C2}(t) \end{pmatrix}$ [@problem_id:1614448]. Any other choice, such as the currents through the resistors, would be insufficient or invalid because resistor currents can change instantaneously and are algebraically dependent on the capacitor voltages and the input.

Let's develop a full [state-space model](@entry_id:273798) for a classic series RLC circuit [@problem_id:1614492]. The energy storage elements are the inductor $L$ and capacitor $C$. We select the inductor current $i_L(t)$ and the capacitor voltage $v_C(t)$ as our [state variables](@entry_id:138790). Let the [state vector](@entry_id:154607) be $\mathbf{x}(t) = \begin{pmatrix} v_C(t) \\ i_L(t) \end{pmatrix}$.

The first state equation is derived from the [constitutive relation](@entry_id:268485) for the capacitor. In a [series circuit](@entry_id:271365), the current flowing into the capacitor is the same as the inductor current, $i_C(t) = i_L(t)$.

$$
i_C(t) = C \frac{dv_C(t)}{dt} \implies \frac{dv_C(t)}{dt} = \frac{1}{C} i_L(t)
$$

The second state equation comes from applying Kirchhoff's Voltage Law (KVL) around the loop and using the inductor's [constitutive relation](@entry_id:268485). The sum of voltages must equal the input voltage $u(t) = v_{in}(t)$.

$$
u(t) = v_R(t) + v_L(t) + v_C(t) = R i_L(t) + L \frac{di_L(t)}{dt} + v_C(t)
$$

Solving for $\frac{di_L(t)}{dt}$:

$$
\frac{di_L(t)}{dt} = -\frac{1}{L} v_C(t) - \frac{R}{L} i_L(t) + \frac{1}{L} u(t)
$$

Combining these two first-order equations yields the state matrix $A$ and input matrix $B$:

$$
A = \begin{pmatrix} 0 & \frac{1}{C} \\ -\frac{1}{L} & -\frac{R}{L} \end{pmatrix}, \quad B = \begin{pmatrix} 0 \\ \frac{1}{L} \end{pmatrix}
$$

If the output $y(t)$ is defined as the voltage across the resistor, $v_R(t) = R i_L(t)$, the output equation becomes:

$$
y(t) = \begin{pmatrix} 0 & R \end{pmatrix} \begin{pmatrix} v_C(t) \\ i_L(t) \end{pmatrix} + \begin{pmatrix} 0 \end{pmatrix} u(t)
$$

This yields $C = \begin{pmatrix} 0 & R \end{pmatrix}$ and $D=0$, completing the model.

### State Variables from Higher-Order Differential Equations

Many systems, particularly in signal processing and mechanics, are initially described by a single $n$-th order linear ordinary differential equation (ODE) relating the output $y(t)$ to the input $u(t)$. A key technique in [state-space analysis](@entry_id:266177) is the conversion of this single ODE into a system of $n$ first-order ODEs.

A standard and systematic method is to choose the output and its first $n-1$ derivatives as the state variables. This is often called the **phase-variable** or **[controllable canonical form](@entry_id:165254)** realization.

For a simple [second-order system](@entry_id:262182) described by $\frac{d^2y}{dt^2} = u(t)$, we need two [state variables](@entry_id:138790) [@problem_id:1614473]. Following the convention, we choose:

$$
x_1(t) = y(t) \quad \text{and} \quad x_2(t) = \frac{dy(t)}{dt}
$$

Now we find their derivatives. The derivative of $x_1$ is simply $x_2$ by definition.

$$
\dot{x}_1(t) = \frac{dy(t)}{dt} = x_2(t)
$$

The derivative of $x_2$ is the second derivative of $y$, which is given by the original ODE.

$$
\dot{x}_2(t) = \frac{d^2y(t)}{dt^2} = u(t)
$$

The [state equations](@entry_id:274378) are therefore:

$$
\frac{d}{dt} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} + \begin{pmatrix} 0 \\ 1 \end{pmatrix} u(t)
$$

This procedure generalizes directly. Consider a third-order LTI system [@problem_id:1614455]:

$$
\frac{d^3y}{dt^3} + a_2 \frac{d^2y}{dt^2} + a_1 \frac{dy}{dt} + a_0 y = u(t)
$$

We define the [state variables](@entry_id:138790) according to the same convention:

$$
x_1 = y, \quad x_2 = \dot{y}, \quad x_3 = \ddot{y}
$$

The derivatives are:
$\dot{x}_1 = \dot{y} = x_2$
$\dot{x}_2 = \ddot{y} = x_3$
To find $\dot{x}_3 = \dddot{y}$, we rearrange the original ODE:
$\dot{x}_3 = -a_0 y - a_1 \dot{y} - a_2 \ddot{y} + u(t) = -a_0 x_1 - a_1 x_2 - a_2 x_3 + u(t)$

This results in the state matrix known as the [controllable canonical form](@entry_id:165254):

$$
A = \begin{pmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ -a_0 & -a_1 & -a_2 \end{pmatrix}
$$

For a concrete example, a filter with the dynamics $\frac{d^2y}{dt^2} + 3\frac{dy}{dt} + 2y(t) = u(t)$ has coefficients $a_1=3$ and $a_0=2$ [@problem_id:1614500]. Applying the same method with $x_1 = y$ and $x_2 = \dot{y}$ leads to the state matrix:

$$
A = \begin{pmatrix} 0 & 1 \\ -2 & -3 \end{pmatrix}
$$

### Non-Uniqueness and Transformation of State Variables

A critical insight is that the choice of state variables for a given system is not unique. Any set of variables that satisfies the definition of state is valid. This flexibility can be exploited to choose a state vector that simplifies analysis or corresponds to more intuitive physical quantities.

#### Alternative Physical Variables

In our RL circuit example, we chose inductor current $i_L$ as a state variable. However, we could instead choose the magnetic flux in the inductor's core, $\Phi(t)$, as the state variable $x(t)$ [@problem_id:1614444]. From Faraday's law of induction and the definition of [inductance](@entry_id:276031), the inductor voltage is $v_L = N \frac{d\Phi}{dt} = N \dot{x}$, and the flux linkage is $\lambda = N\Phi = Li_L$. From these, we can express the current as $i_L = (N/L)x$. Applying KVL to the series RL circuit gives $u(t) = v_R + v_L = R i_L + N \dot{x}$. Substituting for $i_L$ and solving for $\dot{x}$ yields a valid first-order state equation:

$$
\dot{x}(t) = -\frac{R}{L}x(t) + \frac{1}{N}u(t)
$$

This demonstrates that different, but related, [physical quantities](@entry_id:177395) can serve as state variables.

#### State Variables in Nonlinear Systems

The state-space concept extends naturally to nonlinear systems. Consider a mobile robot moving on a plane [@problem_id:1614453]. Its configuration is given by its Cartesian coordinates $(x, y)$ and its orientation angle $\phi$. If its control inputs are its forward speed $v$ and angular velocity $\omega$, its motion is described by the nonlinear [kinematic equations](@entry_id:173032):

$$
\dot{x} = v \cos(\phi) \\
\dot{y} = v \sin(\phi) \\
\dot{\phi} = \omega
$$

The vector $\mathbf{z} = \begin{pmatrix} x & y & \phi \end{pmatrix}^T$ is a valid [state vector](@entry_id:154607) because its time derivative, $\dot{\mathbf{z}}$, is expressed entirely as a function of the state $\mathbf{z}$ and the inputs $v$ and $\omega$. This shows the broad applicability of the state concept beyond LTI systems.

#### Linear Transformations of State

If $\mathbf{x}(t)$ is a valid [state vector](@entry_id:154607) for an LTI system, then any new vector $\mathbf{z}(t)$ created by an [invertible linear transformation](@entry_id:149915), $\mathbf{z}(t) = T \mathbf{x}(t)$, is also a valid [state vector](@entry_id:154607). The dynamics for the new state vector $\mathbf{z}$ are given by:

$$
\dot{\mathbf{z}} = T \dot{\mathbf{x}} = T(A\mathbf{x} + B\mathbf{u}) = T A (T^{-1}\mathbf{z}) + T B \mathbf{u}
$$

The new [state-space representation](@entry_id:147149) is $\dot{\mathbf{z}} = A' \mathbf{z} + B' \mathbf{u}$ and $y = C' \mathbf{z} + D' \mathbf{u}$, where $A' = TAT^{-1}$, $B' = TB$, $C' = CT^{-1}$, and $D'=D$.

This principle can be used to transform a system into a more convenient coordinate system. For instance, in a system of two magnetically coupled inductors, the [stored magnetic energy](@entry_id:274401) is $E = \frac{1}{2}\mathbf{i}^T L \mathbf{i}$, where $L$ is the [symmetric positive definite](@entry_id:139466) inductance matrix [@problem_id:1614480]. One might choose a new state vector $\mathbf{x} = A\mathbf{i}$ such that the energy is expressed in the simple Euclidean form $E = \frac{1}{2}\mathbf{x}^T \mathbf{x}$. This requires finding a matrix $A$ such that $L = A^T A$. If we constrain $A$ to be symmetric and [positive definite](@entry_id:149459), the solution is the unique principal [matrix square root](@entry_id:158930) of $L$, $A = L^{1/2}$. This change of variables transforms the state into a basis where the energy contributions are decoupled, akin to finding the principal axes of an [inertia tensor](@entry_id:178098).

#### Invariance of Characteristic Properties

Although the state matrices $A$ and $A'$ are different for different choices of state variables, they are related by a similarity transformation ($A' = TAT^{-1}$). A fundamental property of similarity transformations is that they preserve the matrix's eigenvalues. The eigenvalues of the state matrix $A$ are the poles of the system, which are intrinsic properties of the system's dynamics. Consequently, the characteristic polynomial, $\det(sI-A)$, is invariant under any choice of [state variables](@entry_id:138790).

This implies that [matrix invariants](@entry_id:195012) like the trace and determinant, which are related to the coefficients of the [characteristic polynomial](@entry_id:150909), are also independent of the chosen [state-space realization](@entry_id:166670). For a second-order system, $\det(sI-A) = s^2 - \text{Tr}(A)s + \det(A)$. For the RLC circuit discussed earlier, the governing ODE leads to a [characteristic polynomial](@entry_id:150909) of $s^2 + (R/L)s + (1/LC)$ [@problem_id:1614434]. By comparing coefficients, we see that $\text{Tr}(A) = -R/L$. This value remains the same whether we use physical variables ($v_C, i_L$), canonical variables, or any other valid set of state variables. This remarkable property provides a powerful consistency check and highlights the deep connection between different system representations.