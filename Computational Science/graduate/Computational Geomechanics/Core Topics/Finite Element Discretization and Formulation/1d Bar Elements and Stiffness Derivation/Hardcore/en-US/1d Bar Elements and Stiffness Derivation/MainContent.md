## Introduction
The one-dimensional (1D) [bar element](@entry_id:746680) is a fundamental building block in the study and application of the Finite Element Method (FEM). While deceptively simple, its formulation encapsulates the core theoretical journey from the continuous laws of physics to the discrete algebraic equations solved by computers. This article bridges the often-challenging conceptual gap between continuum mechanics theory and practical FEM implementation. It provides a detailed, first-principles-based walkthrough of the derivation and application of the 1D [bar element](@entry_id:746680), designed for graduate students and researchers in [computational mechanics](@entry_id:174464).

The first chapter, "Principles and Mechanisms," lays the theoretical groundwork. We will start with the continuum description of deformation and stress, then use the Principle of Virtual Work to derive the integral-based [weak form](@entry_id:137295). This leads to the discretization of the problem using two-node [isoparametric elements](@entry_id:173863) and the systematic derivation of the [element stiffness matrix](@entry_id:139369) and consistent load vectors.

Building on this foundation, the "Applications and Interdisciplinary Connections" chapter explores the versatility of the 1D [bar element](@entry_id:746680). It demonstrates how the basic framework is extended to tackle complex, real-world engineering challenges, including material and geometric nonlinearities, dynamic vibrations, time-dependent behavior, and [coupled multiphysics](@entry_id:747969) problems like [thermo-mechanical analysis](@entry_id:755904).

Finally, "Hands-On Practices" provides a set of targeted problems. These exercises are designed to solidify theoretical understanding and provide experience in verifying numerical implementations and quantifying the accuracy of the [finite element approximation](@entry_id:166278) against analytical solutions.

## Principles and Mechanisms

This chapter delineates the fundamental principles and mechanics governing the formulation of one-dimensional (1D) bar elements, a cornerstone of [computational mechanics](@entry_id:174464). We will begin by establishing the continuum mechanics framework, including the definitions of strain, stress, and equilibrium. Subsequently, we will transition from the strong form of the governing equations to the weak form via the Principle of Virtual Work, which provides the theoretical basis for the Finite Element Method (FEM). The chapter will then detail the [discretization](@entry_id:145012) process using a two-node [isoparametric element](@entry_id:750861), leading to the systematic derivation of the [element stiffness matrix](@entry_id:139369) and consistent load vectors. Finally, we will address critical aspects of numerical implementation, including numerical integration and the enforcement of boundary conditions.

### Foundational Concepts from Continuum Mechanics

Before discretizing a problem, we must first understand its continuum description. This involves defining measures of deformation (kinematics), material response ([constitutive laws](@entry_id:178936)), and the conditions of equilibrium.

#### Kinematics: From Finite to Infinitesimal Strain

Consider a 1D bar initially occupying the domain defined by the material coordinate $X \in [0,L]$. When subjected to loads, a point at $X$ moves to a new spatial position $x$. This relationship, or motion, is described by the mapping $x = \chi(X, t)$. We can express this motion in terms of a displacement field $u(X)$ as $x = X + u(X)$.

The local deformation is quantified by the **deformation gradient**, $F$, defined as the rate of change of the current position with respect to the reference position:
$$
F = \frac{dx}{dX} = \frac{d}{dX}(X + u(X)) = 1 + \frac{du}{dX}
$$
The deformation gradient measures the local stretch of the material. A value of $F=1$ indicates no deformation.

For problems involving large deformations, a strain measure that is objective (i.e., invariant to [rigid body motions](@entry_id:200666)) is required. The **Green-Lagrange [strain tensor](@entry_id:193332)**, $E$, is such a measure. In one dimension, it is defined in terms of the deformation gradient as:
$$
E = \frac{1}{2}(F^2 - 1)
$$
Substituting our expression for $F$, we obtain the exact, geometrically nonlinear strain in terms of the [displacement gradient](@entry_id:165352):
$$
E = \frac{1}{2}\left( \left(1 + \frac{du}{dX}\right)^2 - 1 \right) = \frac{1}{2}\left( 1 + 2\frac{du}{dX} + \left(\frac{du}{dX}\right)^2 - 1 \right) = \frac{du}{dX} + \frac{1}{2}\left(\frac{du}{dX}\right)^2
$$
This expression is fundamental in geometrically [nonlinear analysis](@entry_id:168236).

However, in many engineering applications, including numerous problems in [geomechanics](@entry_id:175967), deformations are small. This corresponds to the assumption of **small strains**, where the [displacement gradient](@entry_id:165352) is much less than unity, i.e., $|\frac{du}{dX}| \ll 1$. In this regime, the quadratic term $(\frac{du}{dX})^2$ is negligible compared to the linear term. By linearizing the Green-Lagrange strain, we arrive at the widely used **[infinitesimal strain](@entry_id:197162)** or **engineering strain**, denoted by $\epsilon$:
$$
\epsilon = \frac{du}{dX}
$$
The relationship between the finite and [infinitesimal strain](@entry_id:197162) measures is therefore $E = \epsilon + \frac{1}{2}\epsilon^2$ . The small-strain assumption is valid when the error introduced by neglecting the quadratic term is acceptable. For example, for a uniform stretch where $u(X) = \alpha X$, we have $\epsilon = \alpha$. The relative difference between the two measures is $(E-\epsilon)/\epsilon = \frac{1}{2}\alpha$. For a strain of $\alpha = 0.05$ (or 5%), the Green-Lagrange strain is only $2.5\%$ larger than the [infinitesimal strain](@entry_id:197162). For a larger strain of $\alpha = 0.20$, the difference grows to $10\%$. This highlights that the [infinitesimal strain](@entry_id:197162) measure $\epsilon$ is an accurate approximation of the true kinematic state only when displacement gradients are small .

#### The Constitutive Law: A Thermodynamic Perspective

The [constitutive law](@entry_id:167255) describes the material's mechanical response, relating stress to strain. For a simple **linear elastic** material, this relationship is given by Hooke's Law. In one dimension, this is $\sigma = E\epsilon$, where $\sigma$ is the axial stress and $E$ is the Young's modulus.

While often presented as an empirical law, this relationship can be rigorously derived from the principles of thermodynamics for a specific class of materials . For an isothermal (constant temperature) and reversible (no [energy dissipation](@entry_id:147406)) process, the mechanical behavior can be described by the **Helmholtz free-energy density**, $\psi$, which is a function of the strain state. The stress is derivable from this potential:
$$
\sigma = \frac{\partial \psi}{\partial \epsilon}
$$
This relation is a direct consequence of the [second law of thermodynamics](@entry_id:142732) (Clausius-Duhem inequality) under the assumption of reversibility. For a material to be linear elastic, the stress must be a linear function of strain. To achieve this, the Helmholtz free-energy density must be a quadratic function of strain:
$$
\psi(\epsilon) = \frac{1}{2} E \epsilon^2
$$
Differentiating this potential with respect to $\epsilon$ recovers Hooke's Law, $\sigma = E\epsilon$. The condition for [material stability](@entry_id:183933) requires the [strain energy](@entry_id:162699) to be positive-definite, which implies that the Young's modulus must be positive, $E > 0$. Therefore, within the framework of small-strain, isothermal, [reversible processes](@entry_id:276625), Hooke's law is the thermodynamically consistent [constitutive relation](@entry_id:268485) for a material with a quadratic free energy potential .

### The Principle of Virtual Work and the Weak Formulation

The governing equation for our 1D bar can be expressed in a "strong form" as a differential equation with associated boundary conditions. For [static equilibrium](@entry_id:163498), the sum of forces on any infinitesimal segment must be zero. Considering an axial force resultant $N(x) = A(x)\sigma(x)$ and an applied distributed axial load $\bar{q}(x)$ (force per unit length), the [equilibrium equation](@entry_id:749057) is:
$$
\frac{dN}{dx} + \bar{q}(x) = 0
$$
Substituting the [constitutive law](@entry_id:167255) ($\sigma = E\epsilon$) and the kinematic relation ($\epsilon = du/dx$), we obtain the strong form of the governing equation in terms of displacement $u(x)$:
$$
\frac{d}{dx}\left(A(x)E(x)\frac{du}{dx}\right) + \bar{q}(x) = 0
$$

#### From Strong Form to Weak Form

The Finite Element Method is not typically based on solving this differential equation directly. Instead, it solves an equivalent integral form known as the **weak form**. This form is derived using the Principle of Virtual Work (or as a direct mathematical consequence via the [method of weighted residuals](@entry_id:169930)). We multiply the [equilibrium equation](@entry_id:749057) by an arbitrary, admissible "virtual" displacement, $v(x)$, and integrate over the domain $(0, L)$ :
$$
\int_0^L \left(\frac{d}{dx}\left(AE\frac{du}{dx}\right) + \bar{q}(x)\right) v(x) \, dx = 0
$$
Applying [integration by parts](@entry_id:136350) to the first term yields:
$$
\int_0^L \left(-AE\frac{du}{dx}\frac{dv}{dx}\right) dx + \left[AE\frac{du}{dx}v(x)\right]_0^L + \int_0^L \bar{q}(x) v(x) \, dx = 0
$$
Recognizing that the axial force is $N(x) = AE \frac{du}{dx}$ and rearranging the terms, we arrive at the weak form: Find the displacement $u(x)$ such that for all admissible virtual displacements $v(x)$:
$$
\int_0^L A(x)E(x)\frac{du}{dx}\frac{dv}{dx} \, dx = \int_0^L \bar{q}(x)v(x) \, dx + N(L)v(L) - N(0)v(0)
$$
This equation represents a balance of [virtual work](@entry_id:176403): the [internal virtual work](@entry_id:172278) (left-hand side) equals the external virtual work done by [distributed loads](@entry_id:162746) and boundary forces (right-hand side). The key advantage of the weak form is that it reduces the differentiation requirement on the displacement field $u(x)$ from second order to first order, allowing for a broader class of functions as potential solutions.

#### Essential and Natural Boundary Conditions

The integration by parts procedure naturally separates the boundary conditions into two distinct types :

1.  **Essential Boundary Conditions (Dirichlet type):** These are conditions imposed on the primary field variable, which in our case is the displacement $u(x)$. An example is a fixed end, $u(0) = \bar{u}_0$. These conditions must be explicitly enforced on the space of possible solutions. For the weak form, the [virtual displacement](@entry_id:168781) $v(x)$ must vanish at any point where an essential condition is prescribed (e.g., if $u(0)$ is prescribed, we must have $v(0)=0$). This causes the corresponding boundary term in the [weak form](@entry_id:137295) (e.g., $-N(0)v(0)$) to vanish automatically. The reaction force $N(0)$ becomes an unknown of the problem, to be solved for after the [displacement field](@entry_id:141476) is found.

2.  **Natural Boundary Conditions (Neumann type):** These are conditions on the secondary variables that appear naturally in the boundary terms of the weak form. In this problem, the secondary variable is the axial force $N(x)$. An example is a prescribed traction at an end, $N(L) = \bar{N}_L$. These conditions are satisfied by substituting the prescribed values directly into the weak form. The term $N(L)v(L)$ becomes $\bar{N}_L v(L)$ and contributes to the external virtual work. The displacement $u(L)$ at this boundary is not prescribed and becomes an unknown to be solved for.

#### Well-Posedness and the Role of Function Spaces

For a solution to exist and be unique, the [boundary value problem](@entry_id:138753) must be well-posed. From a functional analytic perspective, the [weak form](@entry_id:137295) requires us to find a solution $u$ in a suitable **[trial space](@entry_id:756166)** $V$ that satisfies the equation for all functions $v$ in a **[test space](@entry_id:755876)** $V_0$. The [weak form](@entry_id:137295) involves first derivatives, so the natural setting for these functions is the **Sobolev space** $H^1(0,L)$, which contains functions that are square-integrable and have square-integrable first derivatives .

The [essential boundary conditions](@entry_id:173524) are fundamental to defining these spaces. For a bar fixed at $x=0$ ($u(0)=0$), the [trial space](@entry_id:756166) becomes $V = \{ u \in H^1(0,L) : u(0)=0 \}$. The [test space](@entry_id:755876) consists of functions satisfying the homogeneous version of the essential BCs, so $V_0 = V$ in this case.

The [existence and uniqueness](@entry_id:263101) of a solution are guaranteed by the **Lax-Milgram Theorem**, provided that the [bilinear form](@entry_id:140194) $a(u,v) = \int AE u'v' dx$ is continuous and **coercive** on the [trial space](@entry_id:756166), and the linear functional for the external work is continuous. Coercivity means that $a(u,u) \ge c \|u\|_{H^1}^2$ for some constant $c>0$. For the 1D bar, the [bilinear form](@entry_id:140194) is $a(u,u) = \int AE (u')^2 dx$. This term is zero for any constant displacement $u(x)=C$, which represents a rigid-body mode. If only [natural boundary conditions](@entry_id:175664) are applied, this rigid-body mode is admissible and the solution is not unique (it is defined only up to an arbitrary constant displacement). Correspondingly, the [global stiffness matrix](@entry_id:138630) will be **positive-semidefinite** and singular .

By enforcing at least one [essential boundary condition](@entry_id:162668) (e.g., $u(0)=0$), we eliminate the rigid-body mode. For any function $u$ in the constrained [trial space](@entry_id:756166), $u(x)=C$ is only possible if $C=0$. The Poincaré-Friedrichs inequality then ensures that the [bilinear form](@entry_id:140194) is coercive on this constrained space, guaranteeing a unique solution. The resulting [global stiffness matrix](@entry_id:138630) for the unconstrained degrees of freedom becomes **positive-definite** and invertible  .

### The Two-Node Isoparametric Bar Element

The [finite element method](@entry_id:136884) approximates the continuous solution $u(x)$ with a [piecewise polynomial](@entry_id:144637) function. This is achieved by dividing the domain into discrete elements and defining the solution within each element in terms of values at nodes.

#### Shape Functions and the Isoparametric Mapping

For the 1D bar, the simplest and most common element is the **two-node linear element**. We define this element in a normalized **parent coordinate** system $\xi \in [-1, 1]$. The displacement $u(\xi)$ within the element is interpolated from the nodal displacements, $u_1$ and $u_2$, using linear **[shape functions](@entry_id:141015)** (or interpolation functions), $N_1(\xi)$ and $N_2(\xi)$:
$$
u(\xi) = N_1(\xi) u_1 + N_2(\xi) u_2
$$
The linear shape functions are:
$$
N_1(\xi) = \frac{1-\xi}{2}, \quad N_2(\xi) = \frac{1+\xi}{2}
$$
These functions have the property that $N_i$ is equal to one at node $i$ and zero at the other node.

The **isoparametric concept** is a powerful idea in FEM where the same [shape functions](@entry_id:141015) used to interpolate the displacement field are also used to map the element's geometry from the [parent domain](@entry_id:169388) to the physical domain. The physical coordinate $x$ is interpolated from the nodal coordinates $x_1$ and $x_2$:
$$
x(\xi) = N_1(\xi) x_1 + N_2(\xi) x_2
$$
This mapping allows for the straightforward handling of elements of any length and orientation (in higher dimensions). This same interpolation strategy can also be applied to material properties that vary across the element, such as a linearly varying axial rigidity $R(\xi) = N_1(\xi)R_1 + N_2(\xi)R_2$ .

#### Kinematics within the Element: The Strain-Displacement Matrix

To evaluate the weak form integrals, we need the strain within the element. Strain is the derivative of displacement with respect to the physical coordinate $x$, but our [shape functions](@entry_id:141015) are defined in $\xi$. We use the chain rule to relate the derivatives:
$$
\frac{d}{d\xi} = \frac{dx}{d\xi} \frac{d}{dx} = J \frac{d}{dx}
$$
where $J = dx/d\xi$ is the **Jacobian** of the transformation. For the linear [isoparametric element](@entry_id:750861), the Jacobian is a constant:
$$
J = \frac{dx}{d\xi} = \frac{d}{d\xi}\left(\frac{1-\xi}{2}x_1 + \frac{1+\xi}{2}x_2\right) = \frac{x_2-x_1}{2} = \frac{L}{2}
$$
where $L$ is the element length.

The strain $\epsilon = du/dx$ can now be expressed in terms of nodal displacements. Let $\mathbf{u}_e = \begin{pmatrix} u_1  u_2 \end{pmatrix}^T$ be the vector of nodal displacements.
$$
\epsilon = \frac{du}{dx} = \frac{1}{J} \frac{du}{d\xi} = \frac{1}{J} \frac{d}{d\xi} \left( \mathbf{N}(\xi) \mathbf{u}_e \right) = \left( \frac{1}{J} \frac{d\mathbf{N}}{d\xi} \right) \mathbf{u}_e
$$
This defines the **[strain-displacement matrix](@entry_id:163451)** (often called the **B-matrix**):
$$
\mathbf{B} = \frac{1}{J} \frac{d\mathbf{N}}{d\xi}
$$
For the linear [bar element](@entry_id:746680), the derivatives of the shape functions are $\frac{dN_1}{d\xi} = -1/2$ and $\frac{dN_2}{d\xi} = 1/2$. The B-matrix is therefore constant:
$$
\mathbf{B} = \frac{1}{L/2} \begin{pmatrix} -1/2  1/2 \end{pmatrix} = \frac{1}{L} \begin{pmatrix} -1  1 \end{pmatrix}
$$
This shows that a two-node linear element assumes a state of **constant strain** throughout the element.

### Derivation of Element Matrices

Substituting the finite element approximations into the [weak form](@entry_id:137295) allows us to derive the algebraic equations that govern the discrete system.

#### The Element Stiffness Matrix

The [internal virtual work](@entry_id:172278) term in the weak form, $\int_V \delta\epsilon^T \sigma dV$, gives rise to the [stiffness matrix](@entry_id:178659). For a single element, we substitute $\epsilon = \mathbf{B}\mathbf{u}_e$ and $\sigma = E\epsilon$, and the virtual strain $\delta\epsilon = \mathbf{B}\delta\mathbf{u}_e$:
$$
\delta W_{int} = \int_{V_e} (\mathbf{B}\delta\mathbf{u}_e)^T (E \mathbf{B}\mathbf{u}_e) dV = \delta\mathbf{u}_e^T \left( \int_{V_e} \mathbf{B}^T E \mathbf{B} A \, dx \right) \mathbf{u}_e
$$
By definition, the [internal virtual work](@entry_id:172278) is also $\delta W_{int} = \delta\mathbf{u}_e^T \mathbf{k}_e \mathbf{u}_e$, where $\mathbf{k}_e$ is the **[element stiffness matrix](@entry_id:139369)**. Thus, we identify:
$$
\mathbf{k}_e = \int_{x_1}^{x_2} \mathbf{B}^T E(x) A(x) \mathbf{B} \, dx
$$
To evaluate this integral, we change to the parent coordinate system using $dx = J d\xi$:
$$
\mathbf{k}_e = \int_{-1}^{1} \mathbf{B}^T E(\xi) A(\xi) \mathbf{B} J \, d\xi
$$
This is the master formula for the stiffness matrix of a 1D [isoparametric element](@entry_id:750861) .

**Case 1: Constant Properties.** If $E$ and $A$ are constant, they can be taken outside the integral. As $\mathbf{B}$ and $J$ are also constant for a linear element, the integral becomes trivial:
$$
\mathbf{k}_e = \mathbf{B}^T E A \mathbf{B} \int_{x_1}^{x_2} dx = \mathbf{B}^T E A \mathbf{B} L
$$
Substituting $\mathbf{B} = \frac{1}{L} \begin{pmatrix} -1  1 \end{pmatrix}$:
$$
\mathbf{k}_e = \left(\frac{1}{L}\begin{pmatrix}-1 \\ 1\end{pmatrix}\right) E A \left(\frac{1}{L}\begin{pmatrix}-1  1\end{pmatrix}\right) L = \frac{EA}{L} \begin{pmatrix} 1  -1 \\ -1  1 \end{pmatrix}
$$
This is the famous [stiffness matrix](@entry_id:178659) for a 1D [bar element](@entry_id:746680) with constant properties .

**Case 2: Spatially Varying Properties.** If the axial rigidity $R(x) = E(x)A(x)$ varies along the element, it cannot be removed from the integral . For a linear element, $\mathbf{B}$ is still constant, so the formula simplifies to:
$$
\mathbf{k}_e = \mathbf{B}^T \left(\int_{x_1}^{x_2} R(x) dx\right) \mathbf{B}
$$
The stiffness is determined by the integral of the rigidity over the element length. If we assume the rigidity varies linearly between the nodes, $R(\xi) = N_1(\xi)R_1 + N_2(\xi)R_2$, the integral becomes :
$$
\int_{x_1}^{x_2} R(x) dx = \int_{-1}^{1} R(\xi) J d\xi = \frac{L}{2} \int_{-1}^{1} (N_1 R_1 + N_2 R_2) d\xi = \frac{L}{2}(R_1+R_2)
$$
This integral is simply the area of a trapezoid with height $L$ and parallel sides $R_1$ and $R_2$. The [stiffness matrix](@entry_id:178659) is then:
$$
\mathbf{k}_e = \frac{(R_1+R_2)/2}{L} \begin{pmatrix} 1  -1 \\ -1  1 \end{pmatrix}
$$
This elegantly shows that for a linear element with linearly varying rigidity, the effective rigidity is simply the average of the nodal values.

#### The Consistent Nodal Load Vector

The external [virtual work](@entry_id:176403) done by [body forces](@entry_id:174230), $\int_V \delta u^T b dV$, gives rise to the **consistent nodal [load vector](@entry_id:635284)**. Substituting the FE approximation for the [virtual displacement](@entry_id:168781), $\delta u = \mathbf{N}\delta\mathbf{u}_e$:
$$
\delta W_{ext,b} = \int_{V_e} (\mathbf{N}\delta\mathbf{u}_e)^T b dV = \delta\mathbf{u}_e^T \left( \int_{V_e} \mathbf{N}^T b A \, dx \right)
$$
By comparing this with the definition $\delta W_{ext,b} = \delta\mathbf{u}_e^T \mathbf{f}_b$, we identify the [consistent load vector](@entry_id:163156) due to body forces:
$$
\mathbf{f}_b = \int_{x_1}^{x_2} \mathbf{N}(x)^T b A \, dx
$$
For a uniform [body force](@entry_id:184443) $b$ and constant area $A$, we can evaluate this integral in the parent coordinate system :
$$
\mathbf{f}_b = \int_{-1}^{1} \mathbf{N}(\xi)^T b A J \, d\xi = bA \frac{L}{2} \int_{-1}^{1} \begin{pmatrix} N_1(\xi) \\ N_2(\xi) \end{pmatrix} d\xi
$$
Since $\int_{-1}^1 N_1(\xi) d\xi = 1$ and $\int_{-1}^1 N_2(\xi) d\xi = 1$, the integral evaluates to $\begin{pmatrix} 1  1 \end{pmatrix}^T$. The resulting [load vector](@entry_id:635284) is:
$$
\mathbf{f}_b = bA \frac{L}{2} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} bAL/2 \\ bAL/2 \end{pmatrix}
$$
This result is intuitive: the total [body force](@entry_id:184443) on the element, $b \times (AL)$, is distributed equally to the two nodes. This "consistent" method of lumping loads is derived directly from the [principle of virtual work](@entry_id:138749) and preserves the [order of accuracy](@entry_id:145189) of the method.

### Numerical Implementation and Practical Considerations

The final steps in a [finite element analysis](@entry_id:138109) involve numerically evaluating the element integrals, assembling the global system of equations, and applying boundary conditions to solve for the unknown nodal displacements.

#### Numerical Integration: Gauss-Legendre Quadrature

While the integrals for a linear element with constant or linearly varying properties can be solved analytically, this is often not the case for more complex property variations or for [higher-order elements](@entry_id:750328). In general, these integrals are evaluated numerically using **Gauss-Legendre quadrature**. This method approximates an integral over $\xi \in [-1, 1]$ as a weighted sum of the integrand's values at specific points, called Gauss points:
$$
\int_{-1}^1 f(\xi) d\xi \approx \sum_{i=1}^{n_p} w_i f(\xi_i)
$$
where $n_p$ is the number of integration points. The power of Gauss quadrature lies in its efficiency: an $n_p$-point rule can integrate any polynomial of degree up to $2n_p - 1$ exactly.

To determine the required number of points, we must find the polynomial degree of the integrand in the [stiffness matrix](@entry_id:178659) expression, $k(\xi) = \mathbf{B}^T E(\xi) A(\xi) \mathbf{B} J(\xi)$.
-   For a linear element with constant $E$ and $A$, we found that $\mathbf{B}$, $J$, $E$, and $A$ are all constants (degree 0 polynomials). The integrand is therefore a constant (degree 0). A 1-point Gauss rule ($n_p=1$) is exact for polynomials up to degree $2(1)-1=1$. Thus, a single integration point is sufficient to exactly integrate the stiffness matrix .
-   Consider a more complex case: a linear element ($J$ and $\mathbf{B}$ are constant) with linearly varying area $A(\xi)$ (degree 1) and a Young's modulus $E(\xi)$ that is a polynomial of degree $m$ . The integrand's degree is determined by the product $E(\xi)A(\xi)$, which has degree $m+1$. If we use a 2-point Gauss rule ($n_p=2$), we can integrate polynomials up to degree $2(2)-1=3$ exactly. Therefore, we must have $m+1 \le 3$, which means $m \le 2$. The 2-point rule is exact as long as the Young's modulus is at most a quadratic function of $\xi$.

#### Assembly and Enforcement of Essential Boundary Conditions

Once the element matrices ($\mathbf{k}_e$) and vectors ($\mathbf{f}_e$) are computed for all elements, they are **assembled** into a global system of equations, $\mathbf{K}\mathbf{u} = \mathbf{f}$. The global matrix $\mathbf{K}$ is formed by summing the contributions from each [element stiffness matrix](@entry_id:139369) into the appropriate rows and columns corresponding to their global node numbers.

The final critical step is the enforcement of essential (Dirichlet) boundary conditions, such as a prescribed displacement $u_i = \bar{u}_i$ at a node $i$. The raw assembled matrix $\mathbf{K}$ is singular if the structure is not yet constrained. Applying essential BCs removes the rigid-body modes and makes the system solvable. There are several ways to do this, but a valid method must yield the correct solution while preferably maintaining the symmetry of the [stiffness matrix](@entry_id:178659) .

Two common and correct methods are:

1.  **Partitioning and Static Condensation:** This is the most theoretically direct method. The global system is partitioned into free ($F$) and constrained ($C$) degrees of freedom:
    $$
    \begin{pmatrix} \mathbf{K}_{FF}  \mathbf{K}_{FC} \\ \mathbf{K}_{CF}  \mathbf{K}_{CC} \end{pmatrix} \begin{pmatrix} \mathbf{u}_F \\ \mathbf{u}_C \end{pmatrix} = \begin{pmatrix} \mathbf{f}_F \\ \mathbf{f}_R \end{pmatrix}
    $$
    Since $\mathbf{u}_C = \bar{\mathbf{u}}_C$ is known, the first row of equations can be rearranged to solve for the unknown free displacements $\mathbf{u}_F$:
    $$
    \mathbf{K}_{FF} \mathbf{u}_F = \mathbf{f}_F - \mathbf{K}_{FC} \bar{\mathbf{u}}_C
    $$
    The reduced system involves the symmetric and [positive-definite matrix](@entry_id:155546) $\mathbf{K}_{FF}$ and yields the exact solution for $\mathbf{u}_F$.

2.  **Modification of Rows and Columns (Exact):** A common implementation approach that avoids explicit partitioning is to modify the full matrix $\mathbf{K}$ and vector $\mathbf{f}$. For each constrained degree of freedom $i$ with $u_i = \bar{u}_i$:
    a.  Modify the [load vector](@entry_id:635284): For all free rows $j \in F$, update the force $f_j = f_j - K_{ji}\bar{u}_i$. This transfers the effect of the prescribed displacement onto the right-hand side.
    b.  Zero out the row and column corresponding to the constrained DOF: Set all elements in row $i$ and column $i$ of $\mathbf{K}$ to zero.
    c.  Place a 1 on the diagonal: Set $K_{ii} = 1$.
    d.  Set the corresponding force entry: Set $f_i = \bar{u}_i$.
    This procedure effectively replaces the original [equilibrium equation](@entry_id:749057) at row $i$ with the simple constraint equation $1 \cdot u_i = \bar{u}_i$. The modifications to the columns preserve the symmetry of the final system, and the modification to the [load vector](@entry_id:635284) ensures that the solution for the free DOFs is identical to that from the partitioning method .

Incorrect methods, such as zeroing out only the rows (which destroys symmetry) or using the [penalty method](@entry_id:143559) (which is an approximation and can cause [ill-conditioning](@entry_id:138674)), should be avoided when an exact, symmetric solution is desired.