## Introduction
The Hamiltonian formulation of mechanics represents a profound shift in perspective from the Lagrangian approach, revealing deep geometric structures, unifying symmetries with conservation laws, and providing a phase space framework that is central to both classical and quantum physics. However, extending this powerful formalism to classical field theory presents a fundamental challenge: the standard canonical approach breaks the inherent unity of spacetime by singling out time as a special direction for evolution. This forfeits the manifest Lorentz covariance that is essential to relativistic theories.

This article addresses this knowledge gap by introducing multisymplectic geometry, a mathematical framework designed to provide a fully covariant Hamiltonian description of classical fields. By treating space and time on an equal footing, this approach generalizes the familiar symplectic structure of mechanics to a "multisymplectic" structure suitable for the infinite-dimensional phase spaces of field theory. The result is a richer, more unified understanding of field dynamics, constraints, and conservation laws.

In the following sections, you will gain a comprehensive understanding of this elegant formalism. The "Principles and Mechanisms" section will build the theory from first principles, establishing the language of jet bundles and deriving the central Hamilton-De Donder-Weyl (HDW) equations. Following this, "Applications and Interdisciplinary Connections" will demonstrate the theory's utility by applying it to fundamental physical theories like electromagnetism and Yang-Mills theory, as well as to problems in continuum mechanics and computational science. Finally, the "Hands-On Practices" section will offer concrete problems to solidify your technical mastery of the core concepts, preparing you to apply these powerful geometric tools in your own work.

## Principles and Mechanisms

The transition from a Lagrangian to a Hamiltonian description is a cornerstone of theoretical physics, offering deeper insights into the symmetries and geometric structures of a system. For classical field theories, this transition requires moving beyond the familiar symplectic geometry of finite-dimensional mechanics into the richer world of multisymplectic geometry. This section lays out the principles and mechanisms of this covariant Hamiltonian framework, building the necessary geometric structures from first principles.

### The Geometric Arena: Fiber Bundles and Jet Bundles

The modern language of classical field theory is the language of differential geometry. We begin by establishing this foundational vocabulary.

#### Fields as Sections of Fiber Bundles

A **classical field** is properly understood as a **section** of a **fiber bundle**. Let $X$ be an $(n+1)$-dimensional manifold, representing spacetime, which serves as our base manifold. The fields themselves take values in another manifold, the fiber $F$. The total space of the theory is a fiber bundle $\pi: Y \to X$, where each fiber $\pi^{-1}(x)$ for $x \in X$ is diffeomorphic to $F$. The dimension of $Y$ is $\dim(X) + \dim(F) = (n+1) + m$.

A specific configuration of the field is a smooth map $\phi: X \to Y$ that satisfies the section condition $\pi \circ \phi = \mathrm{id}_X$. This condition ensures that for each point $x$ in spacetime, the field $\phi$ assigns a unique value $\phi(x)$ in the fiber over that point.

To perform calculations, we use **bundle-adapted local coordinates** $(x^\mu, y^A)$ on an open subset of $Y$, where $(x^\mu)$ for $\mu = 0, \dots, n$ are coordinates on the base manifold $X$, and $(y^A)$ for $A = 1, \dots, m$ are coordinates on the fibers. In these coordinates, the projection map is simply $\pi(x^\mu, y^A) = (x^\mu)$, and a section $\phi$ is represented by a set of $m$ functions of $n+1$ variables, $y^A = \phi^A(x^\mu)$.

#### Tangent Vectors: Vertical and Horizontal Directions

The tangent bundle $TY$ of the total space possesses a canonical geometric structure inherited from the projection $\pi$. At any point $y \in Y$, the tangent space $T_yY$ can be analyzed by considering the differential of the projection, $d\pi_y: T_yY \to T_{\pi(y)}X$.

The **vertical subbundle** $VY$ is defined as the kernel of this differential: $V_yY = \ker(d\pi_y)$. A tangent vector is **vertical** if it is tangent to the fiber. In local coordinates, the basis vectors $\{\partial/\partial y^A\}$ span the vertical space $V_yY$, as $d\pi(\partial/\partial y^A) = 0$.

Conversely, a direction is considered "horizontal" if it projects non-trivially onto the base space. The basis vectors $\partial/\partial x^\mu$ in a local chart are examples of vectors that are not vertical, as $d\pi(\partial/\partial x^\mu) = \partial/\partial x^\mu$ at the corresponding point on $X$. However, it is crucial to recognize that there is **no canonical horizontal subbundle** that is complementary to $VY$. The notion of a "horizontal vector" is coordinate-dependent. Defining a global, coordinate-independent horizontal distribution requires additional structure, namely an **Ehresmann connection**.

When we consider the differential of a section, $d\phi_x: T_xX \to T_{\phi(x)}Y$, it maps vectors on the base manifold into the tangent space of the total space. The section condition $\pi \circ \phi = \mathrm{id}_X$ has a profound consequence. Applying the chain rule gives $d\pi_{\phi(x)} \circ d\phi_x = \mathrm{id}_{T_xX}$. This implies that the map $d\phi_x$ is always injective, and its image, the $(n+1)$-dimensional subspace $\mathrm{Im}(d\phi_x) \subset T_{\phi(x)}Y$, is always transverse to the vertical space $V_{\phi(x)}Y$. Specifically, $\mathrm{Im}(d\phi_x) \oplus V_{\phi(x)}Y = T_{\phi(x)}Y$. In local coordinates, the image of a basis vector $\partial/\partial x^\mu$ under $d\phi_x$ is:
$$
d\phi_x\left(\frac{\partial}{\partial x^\mu}\right) = \frac{\partial}{\partial x^\mu}\bigg|_{\phi(x)} + \frac{\partial \phi^A}{\partial x^\mu}(x) \frac{\partial}{\partial y^A}\bigg|_{\phi(x)}
$$
This expression shows that the tangent space to the graph of a section has both "horizontal" and "vertical" components, with the vertical components being the partial derivatives of the field.

#### The First Jet Bundle and Jet Prolongation

Field theories typically involve derivatives of fields. The proper geometric arena for a first-order field theory is not the bundle $Y$ itself, but its **first jet bundle**, denoted $J^1Y$. The jet bundle is constructed to incorporate the field's value and its first derivatives as independent coordinates.

Formally, the first jet bundle $J^1Y$ is the space of equivalence classes of sections of $\pi$ that have first-order contact at a point. Two sections $\phi_1$ and $\phi_2$ have first-order contact at $x \in X$ if they have the same value and the same first derivative at $x$; that is, $\phi_1(x) = \phi_2(x)$ and $d\phi_{1,x} = d\phi_{2,x}$. The equivalence class is called the **1-jet** of a section $\phi$ at $x$, denoted $j^1_x\phi$.

The set of all such jets, $J^1Y = \bigsqcup_{x \in X} \{j^1_x\phi\}$, forms a smooth manifold. Given bundle-adapted coordinates $(x^\mu, y^A)$ for $Y$, there is an induced coordinate chart on $J^1Y$ given by $(x^\mu, y^A, y^A_\mu)$, where the new coordinates $y^A_\mu$ correspond to the partial derivatives of the section, $y^A_\mu \leftrightarrow \partial_\mu \phi^A(x)$. These coordinates are well-defined because all sections in an equivalence class $j^1_x\phi$ share the same derivatives at $x$. The dimension of the first jet bundle is therefore $\dim(J^1Y) = \dim(X) + \dim(F) + \dim(X)\dim(F) = (n+1) + m + m(n+1)$.

Any section $\phi: X \to Y$ has a canonical lift to its **first jet prolongation** $j^1\phi: X \to J^1Y$, which is a section of the projection $\pi_1: J^1Y \to X$. In coordinates, this lift is given by the map $x \mapsto (x^\mu, \phi^A(x^\nu), \partial_\mu \phi^A(x^\nu))$. The image of this map is a submanifold of $J^1Y$ that is said to be **holonomic**, as the coordinates $y^A_\mu$ are not independent but are constrained to be the derivatives of the functions $y^A(x)$.

### Lagrangian Field Theory on Jet Bundles

With the jet bundle as our kinematic space, we can formulate the principle of least action in a geometric language.

#### Differential Forms on Jet Bundles

The calculus of variations is naturally expressed using differential forms. On the jet bundle $J^1Y$, we distinguish two particularly important types of forms.
- A $k$-form $\omega$ on $J^1Y$ is **horizontal** if it is annihilated by any vertical vector. A vector $V \in T(J^1Y)$ is vertical with respect to the projection $\pi_1: J^1Y \to X$ if $d\pi_1(V)=0$. The condition is $\iota_V \omega = 0$ for all vertical $V$. Locally, a horizontal form is built from wedges of the base differentials $dx^\mu$, with coefficients that can be functions on all of $J^1Y$: $\omega = \sum f_{I}(x,y,y_\nu) dx^{i_1} \wedge \dots \wedge dx^{i_k}$.
- A form $\alpha$ on $J^1Y$ is a **contact form** if its pullback along any jet prolongation vanishes: $(j^1\phi)^*\alpha = 0$ for all sections $\phi$. The set of contact forms forms a differential ideal, generated by the **basic contact 1-forms**, which in local coordinates are given by $\theta^A = dy^A - y^A_\mu dx^\mu$. On the image of a prolonged section, $y^A = \phi^A(x)$ and $y^A_\mu = \partial_\mu\phi^A(x)$, so $(j^1\phi)^*\theta^A = d\phi^A - (\partial_\mu\phi^A)dx^\mu = 0$.

#### The Lagrangian Density as a Horizontal Form

In this geometric framework, the **Lagrangian density** is a horizontal $(n+1)$-form $\mathcal{L}$ on $J^1Y$. It is typically written as:
$$
\mathcal{L} = L(x^\mu, y^A, y^A_\mu) \, d^{n+1}x
$$
where $L: J^1Y \to \mathbb{R}$ is the Lagrangian function and $d^{n+1}x = dx^0 \wedge \dots \wedge dx^n$ is a local volume form on the $(n+1)$-dimensional spacetime $X$. The form $\mathcal{L}$ is horizontal because its pullback via $\pi_1$ to $J^1Y$ is built only from differentials on the base manifold $X$, which annihilate vertical vectors.

The **action functional** for a field configuration $\phi$ is the integral of the pullback of the Lagrangian density along the jet prolongation of $\phi$:
$$
S[\phi] = \int_X (j^1\phi)^* \mathcal{L} = \int_X L(x^\mu, \phi^A(x), \partial_\mu\phi^A(x)) \, d^{n+1}x
$$
This geometric formulation correctly ensures that the action is an integral over spacetime and provides the foundation for a coordinate-free treatment of variational principles. The Euler-Lagrange equations are then derived by finding sections $\phi$ that are stationary points of this action functional.

### The Covariant Hamiltonian Formalism

The Hamiltonian formalism offers an alternative, often more powerful, perspective. Its covariant formulation for field theory is built upon a phase space endowed with a multisymplectic structure.

#### The Multimomentum Phase Space

While several "phase spaces" can be constructed, a central one is the **multimomentum phase space**. For a first-order field theory, this is a manifold $Z$ equipped with local coordinates $(x^\mu, y^A, p^\mu_A)$, where $(x^\mu, y^A)$ are coordinates on the configuration bundle $Y$, and the $p^\mu_A$ are the **polymomenta** conjugate to the field derivatives $y^A_\mu$. This space is the natural home for the field variables $y^A$ and their conjugate polymomenta. It can be identified with a sub-bundle of the dual of the first jet bundle, $J^1Y^*$.

### Hamilton-De Donder-Weyl (HDW) Theory

With the multimomentum phase space established, we can now formulate the Hamiltonian dynamics for fields, known as the Hamilton-De Donder-Weyl (HDW) theory.

#### The Legendre Transform and the HDW Hamiltonian

The bridge between the Lagrangian and Hamiltonian worlds is the **covariant Legendre transform**. Given a Lagrangian function $L(x^\mu, y^A, y^A_\mu)$, we define the **polymomenta** $p^\mu_A$ as:
$$
p^\mu_A := \frac{\partial L}{\partial y^A_\mu}
$$
The **De Donder-Weyl (HDW) Hamiltonian** function $H$ is defined by a generalization of the standard Legendre transform in mechanics:
$$
H(x^\mu, y^A, p^\mu_A) = p^\mu_A y^A_\mu - L(x^\mu, y^A, y^A_\mu)
$$
This definition assumes that the theory is **hyperregular**, meaning the definition of the polymomenta can be inverted to solve for the velocities $y^A_\mu$ as functions of the momenta, $y^A_\mu = y^A_\mu(x, y, p)$. This allows $H$ to be expressed purely as a function on the momentum phase space, with coordinates $(x^\mu, y^A, p^\mu_A)$.

#### The Hamilton-De Donder-Weyl Equations

The equations of motion in this Hamiltonian framework, the **Hamilton-De Donder-Weyl (HDW) equations**, can be derived in two complementary ways.

First, starting from the Euler-Lagrange equations and the definitions of $p^\mu_A$ and $H$, one can show via direct calculation using the chain rule that the dynamics are governed by the following system of first-order partial differential equations:
$$
\partial_\mu y^A = \frac{\partial H}{\partial p^\mu_A}
$$
$$
\partial_\mu p^\mu_A = -\frac{\partial H}{\partial y^A}
$$
These are the HDW equations. The first equation defines the relationship between the field gradients and the momenta, while the second provides the dynamical evolution of the momenta.

A more profound derivation reveals their geometric origin. We can define a **Hamiltonian $(n+1)$-form** $\Theta_H$ on the momentum phase space $Z$. In local coordinates, this form is given by:
$$
\Theta_H = p^\mu_A dy^A \wedge d^n x_\mu - H d^{n+1}x
$$
where $d^{n+1}x = dx^0 \wedge \dots \wedge dx^n$ is the spacetime volume form and $d^n x_\mu = \iota_{\partial/\partial x^\mu}d^{n+1}x$ is the interior product of the volume form with a basis vector.
The dynamics of the system can be derived from the variational principle that physical field histories $\sigma: X \to Z$ are stationary points of the action:
$$
S[\sigma] = \int_X \sigma^* \Theta_H = \int_X (p^\mu_A \partial_\mu y^A - H(x,y,p)) \, d^{n+1}x
$$
By varying this action with respect to both $y^A(x)$ and $p^\mu_A(x)$ independently and setting the variation to zero, one recovers precisely the Hamilton-De Donder-Weyl equations. This demonstrates that the HDW equations arise from a fundamental variational principle on the multimomentum phase space.

### Advanced Topics and Generalizations

The HDW framework admits several powerful generalizations and provides deep insights into the structure of field theories.

#### The Abstract Multisymplectic Field Equation

The HDW equations can be expressed in a more abstract, coordinate-free manner. The central object is the **multisymplectic form**, which for this formalism is the $(n+2)$-form $\Omega_H = -d\Theta_H$. In local coordinates, it reads:
$$
\Omega_H = -dp^\mu_A \wedge dy^A \wedge d^n x_\mu + dH \wedge d^{n+1}x
$$
This form is exact by construction and therefore closed ($d\Omega_H=0$). It is also non-degenerate in a specific sense relevant to field theory. The dynamics of the theory are encoded by the condition that for a physical field history (represented as an $(n+1)$-dimensional submanifold $\mathcal{S}$ in the phase space $Z$), the pullback of the multisymplectic form to that submanifold vanishes:
$$
\Omega_H |_\mathcal{S} = 0
$$
This single, elegant geometric equation contains the full set of HDW equations. The well-posedness of the theory—the existence of such solution submanifolds for a given Hamiltonian $H$—is guaranteed in hyperregular systems by the non-degeneracy properties of $\Omega_H$.

#### Symmetries and Conservation Laws

The multisymplectic framework provides a beautiful formulation of Noether's theorem. A Lie group $G$ is a **symmetry** of the system if its action on the phase space $Z$ preserves the Hamiltonian $(n+1)$-form $\Theta_H$ (up to an exact form). Infinitesimally, this means the Lie derivative of $\Theta_H$ along the vector field $\xi_Z$ generated by any element of the Lie algebra vanishes (or is exact).

This symmetry implies the existence of a conserved **Noether current**. For each symmetry generator $\xi \in \mathfrak{g}$, there exists a corresponding current $n$-form $j_\xi$ on spacetime. For fields that satisfy the equations of motion (i.e., on-shell), this current is conserved, meaning its exterior derivative vanishes:
$$
dj_\xi = 0
$$
This equation expresses a local conservation law (e.g., conservation of charge, energy, or momentum) in a fully covariant, geometric language.

#### Singular Systems and Constraints

The entire discussion of the HDW formalism has so far relied on the assumption of hyperregularity. When the Lagrangian is **singular**, the Legendre transform $F_L: J^1Y \to J^1Y^\star$ is not a local diffeomorphism. Its image is a submanifold $\mathcal{C} = \mathrm{Im}(F_L)$ of the multimomentum phase space. This is the **primary constraint submanifold**.

The Hamiltonian dynamics must be restricted to this submanifold. The geometric structure on $\mathcal{C}$ is inherited from the ambient space. The restricted form, however, is typically **degenerate**—it is a **pre-multisymplectic form**. Its kernel describes directions of gauge symmetry, and a full analysis of the dynamics requires a systematic procedure (like the Dirac-Bergmann algorithm) to handle these constraints and identify the true physical degrees of freedom. This is the geometric origin of gauge theories.