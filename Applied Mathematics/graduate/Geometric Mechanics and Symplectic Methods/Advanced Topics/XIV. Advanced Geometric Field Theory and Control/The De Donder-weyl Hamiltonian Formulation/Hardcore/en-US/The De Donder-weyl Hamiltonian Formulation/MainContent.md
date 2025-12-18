## Introduction
In the transition from point-particle mechanics to field theory, preserving the manifest [spacetime symmetry](@entry_id:179029) of the relativistic world poses a significant challenge. The standard canonical Hamiltonian formalism forces a "3+1" split of spacetime, treating time as a special coordinate and thereby obscuring the inherent Lorentz covariance of the physics. This creates a gap between the Lagrangian description, which is naturally covariant, and the Hamiltonian one. The De Donder-Weyl (DDW) Hamiltonian formulation elegantly bridges this gap, offering a fully covariant phase space description for classical field theories from the outset.

This article provides a comprehensive exploration of this powerful formalism. In the first chapter, **Principles and Mechanisms**, we will delve into the core mathematical machinery, introducing the concepts of polymomenta, the Legendre-De Donder transform, and the covariant [field equations](@entry_id:1124935) derived from the DDW Hamiltonian. We will also uncover the rich geometric structure of the [polymomentum](@entry_id:1129922) phase space. In the second chapter, **Applications and Interdisciplinary Connections**, we will see the formalism in action, applying it to fundamental physical theories like [scalar fields](@entry_id:151443) and gauge theories, exploring its connections to fluid dynamics and continuum mechanics, and highlighting its crucial role in modern computational science. Finally, the **Hands-On Practices** chapter will offer concrete problems to solidify your understanding of these abstract concepts. We begin by dissecting the fundamental principles that define this elegant approach.

## Principles and Mechanisms

The transition from the Hamiltonian formulation of point-particle mechanics to that of field theory presents a fundamental challenge: preserving the manifest [spacetime covariance](@entry_id:1132006) of the relativistic framework. The standard canonical Hamiltonian formalism necessitates a "3+1" split of spacetime, singling out a time coordinate and treating it differently from spatial coordinates. This procedure obscures the inherent Lorentz symmetry of the underlying physics. The De Donder-Weyl (DDW) Hamiltonian formulation resolves this issue by providing a fully covariant phase space description for classical field theories. This chapter elucidates the core principles and mathematical mechanisms of this powerful formalism.

### The Legendre-De Donder Transform and Polymomentum Phase Space

Let us consider a first-order [classical field theory](@entry_id:149475) defined on a smooth, oriented $n$-dimensional [spacetime manifold](@entry_id:262092) $X$. The fields are represented as sections of a configuration bundle $\pi: Y \to X$. In local coordinates, we denote the spacetime coordinates by $x^\mu$ (where $\mu = 1, \dots, n$) and the field components by $y^a$ (where $a = 1, \dots, m$). The dynamics of the theory are encoded in a Lagrangian $n$-form, typically written as $\mathcal{L}_{\text{form}} = L(x^\mu, y^a, \partial_\mu y^a) \omega$, where $L$ is the Lagrangian density and $\omega$ is a local [volume form](@entry_id:161784) on $X$. The variables $v^a_\mu = \partial_\mu y^a$ are [local coordinates](@entry_id:181200) on the first [jet bundle](@entry_id:158903) $J^1Y$.

The central idea of the De Donder-Weyl formulation is to treat all [partial derivatives](@entry_id:146280) $\partial_\mu y^a$ on an equal footing when performing the Legendre transformation. This leads to the definition of the **polymomenta** (or multimomenta), a set of momentum variables $p_a^\mu$, one for each field component $y^a$ and each spacetime direction $x^\mu$:

$$
p_a^\mu := \frac{\partial L}{\partial (\partial_\mu y^a)}
$$

These polymomenta are the coordinates of a new space, the **[polymomentum](@entry_id:1129922) phase space**, which is a [fiber bundle](@entry_id:153776) over spacetime locally coordinatized by $(x^\mu, y^a, p_a^\mu)$. The transition from the [jet bundle](@entry_id:158903) variables $(x^\mu, y^a, \partial_\mu y^a)$ to the [polymomentum](@entry_id:1129922) phase space variables $(x^\mu, y^a, p_a^\mu)$ is known as the **Legendre-De Donder map**.

For this map to be locally invertible, allowing us to express the velocities $\partial_\mu y^a$ as functions of the polymomenta, the Lagrangian must satisfy a regularity condition. The theory is called **hyperregular** if the matrix of second derivatives, $\frac{\partial^2 L}{\partial (\partial_\mu y^a) \partial (\partial_\nu y^b)}$, is non-degenerate. This ensures that the Legendre-De Donder map is a [local diffeomorphism](@entry_id:203529).

### The De Donder-Weyl Hamiltonian and Covariant Field Equations

With the polymomenta defined, we can introduce the **De Donder-Weyl (DDW) Hamiltonian density** $H$ via a generalized Legendre transform:

$$
H(x^\mu, y^a, p_a^\mu) := p_a^\mu (\partial_\mu y^a) - L(x^\mu, y^a, \partial_\mu y^a)
$$

Here, it is understood that the velocities $\partial_\mu y^a$ on the right-hand side are expressed in terms of the polymomenta using the inverted Legendre-De Donder map.

A significant class of physical systems involves Lagrangians with a kinetic term quadratic in the derivatives and a potential term. For instance, consider a Lagrangian for fields $y^a$ mapping from a spacetime with metric $g^{\mu\nu}(x)$ to a target manifold with metric $h_{ab}(y)$, with an added potential $U(y)$ :

$$
L(x,y,v) = \frac{1}{2} h_{ab}(y) g^{\mu\nu}(x) v^a_\mu v^b_\nu - U(y)
$$

Following the definitions, the polymomenta are $p_a^\mu = h_{ab}(y) g^{\mu\nu}(x) v^b_\nu$. Inverting this gives $v^a_\mu = h^{ab}(y) g_{\mu\nu}(x) p_b^\nu$. Substituting these into the definition of $H$ yields a simple and elegant form for the DDW Hamiltonian density:

$$
H(x,y,p) = \frac{1}{2} g_{\mu\nu}(x) h^{ab}(y) p_a^\mu p_b^\nu + U(y)
$$

This Hamiltonian density governs the dynamics through the **De Donder-Weyl field equations**, a set of first-order partial differential equations that are manifestly covariant:

$$
\partial_\mu y^a = \frac{\partial H}{\partial p_a^\mu} \quad \text{and} \quad \partial_\mu p_a^\mu = -\frac{\partial H}{\partial y^a}
$$

The first equation is often called the "velocity-momentum relation" and typically recovers the inverse Legendre-De Donder map. The second equation contains the core dynamics. For any hyperregular Lagrangian, this system of equations is fully equivalent to the second-order Euler-Lagrange equations .

As a concrete example, consider the real scalar Klein-Gordon field on a 2D spacetime, with Lagrangian density $L = \frac{1}{2}((\partial_x \phi)^2 + (\partial_y \phi)^2) - \frac{1}{2}m^2\phi^2$ . The polymomenta are $p^x = \partial_x \phi$ and $p^y = \partial_y \phi$. The DDW Hamiltonian is $H = \frac{1}{2}((p^x)^2 + (p^y)^2) + \frac{1}{2}m^2\phi^2$. The DDW equations are $\partial_x \phi = p^x$, $\partial_y \phi = p^y$, and $\partial_x p^x + \partial_y p^y = -m^2\phi$. If we analyze solutions that are independent of $y$, these equations reduce to a system of ODEs along characteristics defined by $dx/ds=1$: $\frac{d\phi}{ds} = p^x$ and $\frac{dp^x}{ds} = -m^2\phi$. This system describes [simple harmonic motion](@entry_id:148744), yielding solutions of the form $\phi(s) = \phi_0 \cos(ms) + \frac{\pi_0}{m} \sin(ms)$ for initial data $(\phi_0, \pi_0)$.

### Covariance and Comparison with the Canonical Formulation

The primary virtue of the DDW formalism is its manifest covariance. All fundamental objects—the polymomenta $p_a^\mu$, the Hamiltonian density $H$, and the [field equations](@entry_id:1124935)—transform appropriately under spacetime [coordinate transformations](@entry_id:172727). This can be seen explicitly by analyzing how these quantities behave under scaling transformations .

The distinction between the DDW and the standard canonical Hamiltonian formulation is crucial. The canonical formalism singles out time $x^0 = t$ and defines a single [momentum density](@entry_id:271360) $\pi_a = \frac{\partial L}{\partial(\partial_0 y^a)}$ conjugate to the time-velocity $\partial_0 y^a$. The canonical Hamiltonian density is then $\mathcal{H}_{\text{can}} = \pi_a(\partial_0 y^a) - L$.

Notice that the canonical momentum $\pi_a$ is just the time component of the [polymomentum](@entry_id:1129922), $\pi_a = p_a^0$. We can therefore relate the two Hamiltonian densities directly :

$$
H = p_a^\mu \partial_\mu y^a - L = p_a^0 \partial_0 y^a + p_a^i \partial_i y^a - L = \mathcal{H}_{\text{can}} + p_a^i \partial_i y^a
$$

Here, the index $i$ runs over spatial dimensions. The difference, $H - \mathcal{H}_{\text{can}} = p_a^i \partial_i y^a$, depends on the [spatial derivatives](@entry_id:1132036) and spatial momenta. For the Klein-Gordon field in Minkowski space, where $p^i = -\partial_i\phi$, this difference becomes $-\sum_i (\partial_i\phi)^2$. This calculation highlights that $H$ is a true [scalar density](@entry_id:161438), whereas $\mathcal{H}_{\text{can}}$ is the time-component of a current, the [stress-energy tensor](@entry_id:146544).

### The Geometry of the Polymomentum Phase Space

The DDW formalism is endowed with a rich geometric structure that generalizes the familiar symplectic geometry of classical mechanics. This structure is described by two related objects: the multisymplectic form and the polysymplectic form.

#### The Multisymplectic Form

On the [polymomentum](@entry_id:1129922) phase space, one can define a canonical $n$-form known as the **Poincaré-Cartan form**:

$$
\Theta = p_a^\mu dy^a \wedge \omega_\mu - H \omega
$$

Here, $\omega$ is the spacetime volume $n$-form (e.g., $\omega = dx^1 \wedge \dots \wedge dx^n$), and $\omega_\mu$ is the $(n-1)$-form obtained by contracting $\omega$ with the [basis vector](@entry_id:199546) field $\partial/\partial x^\mu$, i.e., $\omega_\mu := i_{\partial/\partial x^\mu} \omega$.

The exterior derivative of the Poincaré-Cartan form (with a conventional minus sign) defines the **multisymplectic form** $\Omega$, which is an $(n+1)$-form on the [polymomentum](@entry_id:1129922) phase space:

$$
\Omega = -d\Theta = dp_a^\mu \wedge dy^a \wedge \omega_\mu - dH \wedge \omega
$$

By construction, $\Omega$ is exact and therefore closed ($d\Omega = 0$). The DDW [field equations](@entry_id:1124935) can be expressed elegantly in terms of this form. The dynamics are described by a special class of $n$-dimensional submanifolds of the phase space, whose [tangent vectors](@entry_id:265494) are related to the Hamiltonian. More precisely, one can seek a **Hamiltonian [multivector](@entry_id:203525) field** $X_H$, which is an $n$-vector field (a section of $\Lambda^n TZ$) satisfying the fundamental equation :

$$
i_{X_H} \Omega = dH
$$

The integral submanifolds of this [multivector](@entry_id:203525) field correspond to the solutions of the [field theory](@entry_id:155241).

#### The Polysymplectic Form

An alternative, though related, geometric structure is the **polysymplectic form**. This is not a scalar-valued [differential form](@entry_id:174025) like $\Omega$, but rather a vector-bundle-valued 2-form. It is a section of $\Lambda^2 T_V^*Z \otimes \Lambda^{n-1}T^*X$, where $T_V Z$ is the vertical tangent bundle of $Z \to X$. In local coordinates, it is given by :

$$
\hat{\Omega} = dy^a \wedge dp_a^\mu \otimes \omega_\mu
$$

This object is nondegenerate on the vertical bundle, meaning that for any non-zero vertical [tangent vector](@entry_id:264836) $v$, the contraction $i_v \hat{\Omega}$ is non-zero. The polysymplectic form is fundamental to certain [geometric numerical integration](@entry_id:164206) methods (multisymplectic integrators), as it captures the "symplectic" nature of the phase space in each spacetime direction separately. It is crucial to distinguish $\hat{\Omega}$ from the multisymplectic form $\Omega$; they are mathematically different types of objects and cannot be directly compared.

The algebraic structure associated with the multisymplectic form can be captured by the **Poisson-Gerstenhaber bracket**. This bracket is defined for horizontal forms on the phase space. For two horizontal $(n-1)$-forms $f$ and $g$, the bracket is another horizontal $(n-1)$-form defined as $\{f,g\} := i_{X_f} dg$, where $X_f$ is the vertical vector field associated with $f$ via $i_{X_f}\Omega = df$. For instance, in a 1+1 dimensional theory, for the horizontal [1-forms](@entry_id:157984) $f = y\,dx^1$ and $g = p^0\,dx^1$, a direct calculation shows that $\{f,g\} = dx^1$ .

### Connections to Other Formalisms and Applications

The DDW formalism provides a powerful unifying framework that connects to several other areas of [mathematical physics](@entry_id:265403).

#### Relation to the Covariant Phase Space

The Covariant Phase Space (CPS) method is another approach to building a covariant Hamiltonian structure, but it is constructed directly on the space of solutions to the [field equations](@entry_id:1124935). The two formalisms are deeply connected. The key link is the **presymplectic current**. The variation of the Lagrangian $n$-form can be written as $\delta L_{\text{form}} = (\text{E-L}) \delta y^a \omega + d\theta$, where E-L are the Euler-Lagrange expressions and $\theta$ is the presymplectic potential $(n-1)$-form. On the space of solutions (on-shell), the E-L term vanishes, leaving $d\theta = 0$. This implies that the exterior derivative of $\theta$ in field space, $\omega_{\text{current}} = \delta\theta$, is a [closed form](@entry_id:271343). This $\omega_{\text{current}}$ is the presymplectic current. In components, its density is $\omega^\mu = \delta p_a^\mu \wedge \delta y^a$.

The conservation of this current, $\partial_\mu \omega^\mu = 0$ on-shell, ensures that the integral $\int_\Sigma \omega^\mu d^{n-1}x_\mu$ over any Cauchy surface $\Sigma$ is independent of the choice of $\Sigma$. This integral defines the symplectic 2-form on the space of solutions .

The profound connection is that this presymplectic current density can be obtained directly from the DDW multisymplectic form $\Omega$. Specifically, contracting $\Omega$ with two vertical vector fields (representing two variations of the fields, $\delta_1$ and $\delta_2$) yields precisely the presymplectic current $(n-1)$-form evaluated on these variations . This demonstrates that the DDW formalism on the finite-dimensional [polymomentum](@entry_id:1129922) phase space contains all the information needed to construct the infinite-dimensional symplectic geometry of the space of solutions  .

#### Singular Systems and Constraints

The DDW formalism is particularly well-suited to theories with singular Lagrangians, which are characteristic of gauge theories. A Lagrangian is **singular** if its Legendre-De Donder map is not invertible. This occurs when the polymomenta are not independent functions of the velocities, leading to **[primary constraints](@entry_id:168143)** on the [polymomentum](@entry_id:1129922) phase space—equations of the form $\phi(y, p) \approx 0$ that must hold regardless of the dynamics.

A prime example is a theory with a Lagrangian density $L = \lambda_\mu (\partial_\mu y - C_\mu(y))$, where $\lambda_\mu$ is a Lagrange multiplier field . The momenta conjugate to $\lambda_\mu$ are identically zero ($\pi^{\mu\nu} \approx 0$), and the momenta conjugate to $y$ are equal to the multipliers ($p_y^\mu - \lambda_\mu \approx 0$). These are the [primary constraints](@entry_id:168143).

The DDW Hamiltonian for such a system is derived from the full Legendre transform $H = p_y^\mu \partial_\mu y - L$, which for this specific Lagrangian becomes $H = (p_y^\mu - \lambda_\mu)\partial_\mu y + \lambda_\mu C_\mu(y)$. On the constraint submanifold where the [constraint equations](@entry_id:138140) hold, the term multiplying the indeterminate velocity $\partial_\mu y$ vanishes. The remaining term, $\mathcal{H}_{\text{red}} = p_y^\mu C_\mu(y)$ (after eliminating $\lambda_\mu$), becomes the **reduced Hamiltonian** that generates the dynamics on the [reduced phase space](@entry_id:165136). This procedure, known as a **multi-Dirac reduction**, systematically handles the constraints and reveals the true dynamical degrees of freedom of the gauge system.