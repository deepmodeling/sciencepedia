## Introduction
The expansion of our universe is one of the most profound discoveries in modern science, and describing its evolution is the central task of cosmology. The primary tools for this task are the Friedmann equations, a set of dynamical equations that govern the scale of the cosmos over time. But where do these critical equations come from? They are not ad-hoc postulates but are deeply rooted in the fundamental principles of Albert Einstein's theory of General Relativity. This article addresses the knowledge gap between knowing the Friedmann equations and understanding their rigorous origin, providing a comprehensive guide to their derivation.

Over the next chapters, we will embark on a journey from first principles to practical application. The first chapter, **Principles and Mechanisms**, will lay the geometric and physical groundwork, deriving the equations step-by-step from the Einstein Field Equations applied to a homogeneous and isotropic universe. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the power of these equations, showing how they are used to characterize dark energy, understand [structure formation](@entry_id:158241), and even test [alternative theories of gravity](@entry_id:158668). Finally, **Hands-On Practices** will offer the opportunity to solidify your understanding through targeted exercises. We begin by establishing the geometric stage upon which the cosmic drama unfolds: the spacetime of a universe governed by the [cosmological principle](@entry_id:158425).

## Principles and Mechanisms

The evolution of the universe on its largest scales is governed by the principles of General Relativity. To describe this evolution mathematically, we must construct a model that reflects the observed large-scale [homogeneity and isotropy](@entry_id:158336) of the cosmos. This chapter details the derivation of the fundamental equations of cosmology—the Friedmann equations—by applying the machinery of General Relativity to a universe described by the Friedmann-Lemaître-Robertson-Walker (FLRW) metric and filled with a simplified, idealized matter content.

### The Geometry of a Homogeneous and Isotropic Spacetime

The cornerstone of [modern cosmology](@entry_id:752086) is the **[cosmological principle](@entry_id:158425)**, which posits that, on sufficiently large scales, the universe is both homogeneous (the same at every point) and isotropic (the same in every direction). The unique geometry that satisfies these symmetries is described by the **Friedmann-Lemaître-Robertson-Walker (FLRW) metric**. The line element $ds^2$, which represents the infinitesimal [spacetime interval](@entry_id:154935) between two nearby events, is given by:
$$
ds^2 = g_{\mu\nu}dx^\mu dx^\nu = -c^2 dt^2 + a(t)^2 \gamma_{ij} dx^i dx^j
$$
Here, $t$ is the **cosmic time**, the [proper time](@entry_id:192124) measured by observers who are at rest with respect to the large-scale [expansion of the universe](@entry_id:160481) (comoving observers). The function $a(t)$ is the dimensionless **[scale factor](@entry_id:157673)**, which describes the expansion or contraction of space itself. The constant $c$ is the speed of light. The spatial coordinates $x^i$ are [comoving coordinates](@entry_id:271238), meaning that galaxies remain at fixed coordinate positions as the universe expands.

The term $\gamma_{ij}$ represents the metric tensor of a 3-dimensional, maximally symmetric spatial hypersurface. In spherical [comoving coordinates](@entry_id:271238) $(r, \theta, \phi)$, the spatial line element $d\ell^2 = \gamma_{ij} dx^i dx^j$ takes the form:
$$
d\ell^2 = \frac{dr^2}{1-kr^2} + r^2 d\theta^2 + r^2 \sin^2\theta d\phi^2
$$
The constant $k$ is the **[spatial curvature](@entry_id:755140) parameter**. It can take one of three normalized values:
*   $k = +1$: A closed universe with positive [spatial curvature](@entry_id:755140) (like the surface of a 3-sphere).
*   $k = 0$: A [flat universe](@entry_id:183782) with zero [spatial curvature](@entry_id:755140) (Euclidean space).
*   $k = -1$: An open universe with negative [spatial curvature](@entry_id:755140) (a 3-[hyperboloid](@entry_id:170736)).

To apply Einstein's equations, we must first compute the geometric properties of this spacetime, which are encoded in the **Christoffel symbols** (or [connection coefficients](@entry_id:157618)) $\Gamma^\lambda_{\mu\nu}$. These symbols quantify how basis vectors change from point to point and are essential for defining covariant derivatives and curvature. They are calculated from the derivatives of the metric tensor:
$$
\Gamma^\lambda_{\mu\nu} = \frac{1}{2}g^{\lambda\sigma}(\partial_\mu g_{\nu\sigma} + \partial_\nu g_{\mu\sigma} - \partial_\sigma g_{\mu\nu})
$$
The FLRW metric's high degree of symmetry simplifies these calculations significantly. For instance, the purely spatial components depend only on the spatial metric $\gamma_{ij}$. As an illustrative calculation, the component $\Gamma^r_{\theta\theta}$ of the spatial connection can be found by focusing on the spatial metric $\gamma_{ij}$ alone [@problem_id:820083]. With $\gamma_{\theta\theta} = r^2$ and $\gamma^{rr} = 1 - kr^2$, the formula yields:
$$
\Gamma^r_{\theta\theta} = -\frac{1}{2}\gamma^{rr}(\partial_r \gamma_{\theta\theta}) = -\frac{1}{2}(1-kr^2)(2r) = -r(1-kr^2)
$$
Of particular importance for cosmology are the mixed time-space components, which link the expansion of space to the geometry. A direct calculation reveals a simple and profound result [@problem_id:820041]:
$$
\Gamma^i_{0j} = \frac{\dot{a}}{a} \delta^i_j = H \delta^i_j
$$
where $\dot{a} = da/dt$, $\delta^i_j$ is the Kronecker delta, and $H(t) \equiv \dot{a}/a$ is the **Hubble parameter**, which measures the rate of cosmic expansion. This result elegantly shows that the "mixing" of space and time in the connection is directly proportional to the expansion rate.

From the Christoffel symbols, one can construct the **Ricci [curvature tensor](@entry_id:181383)** $R_{\mu\nu}$ and the **Ricci scalar** $R = g^{\mu\nu}R_{\mu\nu}$. These tensors describe the local [curvature of spacetime](@entry_id:189480). A crucial simplification arises because the 3D spatial sections of the FLRW metric are maximally symmetric. For any $n$-dimensional maximally symmetric space, the Ricci tensor is proportional to the metric tensor: $^{(n)}R_{ij} = (n-1)k \gamma_{ij}$. For our 3-dimensional space ($n=3$), this means the spatial Ricci tensor is simply related to the spatial metric itself [@problem_id:820093]:
$$
^{(3)}R_{ij} = 2k \gamma_{ij}
$$
This property allows for a straightforward computation of the full 4D Ricci tensor components for the FLRW metric. The non-zero components are found to be:
$$
R_{00} = -3 \frac{\ddot{a}}{a}
$$
$$
R_{ij} = \left( \frac{a\ddot{a}}{c^2} + \frac{2\dot{a}^2}{c^2} + 2k \right) g_{ij}
$$
These components, encoding the geometry of our model universe, form one side of the Einstein Field Equations. We now turn to the other side: the matter and energy that fill this universe.

### The Matter Content: The Perfect Fluid Model

In General Relativity, the distribution of matter and energy is described by the **stress-energy tensor**, $T_{\mu\nu}$. Given the [homogeneity and isotropy](@entry_id:158336) of our spacetime, the matter distribution must also possess these symmetries. The simplest form of matter that satisfies this is a **perfect fluid**, characterized by its proper energy density $\rho$ and [isotropic pressure](@entry_id:269937) $p$. Its stress-energy tensor is given by:
$$
T^{\mu\nu} = (\rho + p) u^\mu u^\nu + p g^{\mu\nu}
$$
Here, $u^\mu$ is the [4-velocity](@entry_id:261095) of the fluid elements. A fundamental question is what form this [4-velocity](@entry_id:261095) must take. While one might assume *a priori* that the fluid is comoving with the cosmic coordinates (i.e., $u^\mu = (c, 0, 0, 0)$ in $(ct, x, y, z)$ coordinates), this can be rigorously proven. The symmetry of the FLRW metric dictates that the off-diagonal time-space components of the Einstein tensor, $G_{0i}$, are zero. The Einstein Field Equations, $G_{\mu\nu} \propto T_{\mu\nu}$, therefore require that $T_{0i} = 0$. For a [perfect fluid](@entry_id:161909) with $\rho+p \neq 0$, this condition enforces that the spatial components of the [4-velocity](@entry_id:261095) must vanish, $u_i = 0$, and consequently $u^i=0$ [@problem_id:820020]. Thus, the [cosmological principle](@entry_id:158425) forces the [cosmic fluid](@entry_id:161445) to be **comoving**; observers who see the universe as isotropic are necessarily at rest with respect to the fluid.

With this established, the stress-energy tensor for the cosmic fluid in [comoving coordinates](@entry_id:271238) $(x^0=t, x^i)$ simplifies significantly. In the [comoving frame](@entry_id:266800), the covariant components are:
$$
T_{00} = \rho, \quad T_{ij} = p g_{ij}, \quad T_{0i} = 0
$$

### Newtonian Analogy: An Intuitive First Step

Before diving into the full relativistic derivation, it is immensely instructive to consider a Newtonian analogue [@problem_id:820062]. Imagine a spherical region of uniform, [pressureless dust](@entry_id:269682) (matter) expanding in empty space. By Birkhoff's theorem (in GR) or the [shell theorem](@entry_id:157834) (in Newtonian gravity), the [gravitational force](@entry_id:175476) on a test particle of mass $m$ at the edge of this sphere, at a physical radius $r(t)$, depends only on the mass $M(r)$ enclosed within the sphere.

The total energy $E$ of the test particle is the sum of its kinetic and potential energies, and this energy is conserved:
$$
E = \frac{1}{2}m\dot{r}^2 - \frac{G M(r) m}{r} = \text{constant}
$$
The radius can be written in terms of [comoving coordinates](@entry_id:271238) as $r(t) = a(t)r_0$, where $r_0$ is a constant reference radius. The enclosed mass is $M(r) = \frac{4\pi}{3} r(t)^3 \rho_{mass}(t)$. Substituting these into the [energy equation](@entry_id:156281) and dividing by $\frac{1}{2}mr_0^2a^2$, we get:
$$
\left(\frac{\dot{a}}{a}\right)^2 = \frac{8\pi G}{3}\rho_{mass}(t) + \frac{2E/m}{r_0^2 a^2}
$$
This is the Newtonian analogue of the Friedmann equation. It correctly relates the expansion rate ($H = \dot{a}/a$) to the matter density $\rho_{mass}$. By relating energy density $\rho$ to mass density via $\rho = \rho_{mass} c^2$, this equation becomes $\left(\frac{\dot{a}}{a}\right)^2 = \frac{8\pi G}{3c^2}\rho(t) - \frac{k c^2}{a^2}$, where the constant energy term has been identified with curvature. This simple model provides powerful intuition for the dynamics we are about to derive more rigorously.

### Derivation from the Einstein Field Equations

We now apply the full **Einstein Field Equations (EFE)**:
$$
R_{\mu\nu} - \frac{1}{2} R g_{\mu\nu} = \frac{8\pi G}{c^4} T_{\mu\nu}
$$
Let's evaluate the $00$ component of this equation. We need the relevant geometric quantities: $R_{00}=-3\ddot{a}/a$, $g_{00}=-c^2$, and the Ricci scalar $R = \frac{6}{c^2}\left(\frac{\ddot{a}}{a} + \left(\frac{\dot{a}}{a}\right)^2 + \frac{kc^2}{a^2}\right)$. For the matter source, we have $T_{00}=\rho$.

The left-hand side of the EFE, the Einstein tensor component $G_{00}$, becomes:
$$
G_{00} = R_{00} - \frac{1}{2} R g_{00} = -3\frac{\ddot{a}}{a} - \frac{1}{2} \left[\frac{6}{c^2}\left(\frac{\ddot{a}}{a} + \left(\frac{\dot{a}}{a}\right)^2 + \frac{kc^2}{a^2}\right)\right](-c^2)
$$
$$
G_{00} = -3\frac{\ddot{a}}{a} + 3\left(\frac{\ddot{a}}{a} + \left(\frac{\dot{a}}{a}\right)^2 + \frac{kc^2}{a^2}\right) = 3\left(\left(\frac{\dot{a}}{a}\right)^2 + \frac{kc^2}{a^2}\right)
$$
The right-hand side is $\frac{8\pi G}{c^4}T_{00} = \frac{8\pi G \rho}{c^4}$. Equating the two sides gives:
$$
3\left(\left(\frac{\dot{a}}{a}\right)^2 + \frac{kc^2}{a^2}\right) = \frac{8\pi G \rho}{c^4}
$$
Dividing by 3 and rearranging gives the **First Friedmann Equation**:
$$
\left(\frac{\dot{a}}{a}\right)^2 = \frac{8\pi G}{3c^4}\rho - \frac{kc^2}{a^2}
$$
This equation is the primary result, governing the expansion rate of the universe based on its energy density $\rho$ and [spatial curvature](@entry_id:755140) $k$. It is the relativistic counterpart to our Newtonian energy equation.

To find the second key equation, which governs the acceleration of the expansion, we combine the first Friedmann equation with the law of energy conservation. Differentiating the first Friedmann equation with respect to time gives (after multiplying by $a^2$):
$$
\frac{d}{dt}(\dot{a}^2) = \frac{d}{dt}\left(\frac{8\pi G}{3c^4}\rho a^2 - kc^2\right) \implies 2\dot{a}\ddot{a} = \frac{8\pi G}{3c^4}(\dot{\rho}a^2 + 2a\dot{a}\rho)
$$
Dividing by $2a\dot{a}$ yields:
$$
\frac{\ddot{a}}{a} = \frac{4\pi G}{3c^4}\left(\frac{a}{\dot{a}}\dot{\rho} + 2\rho\right)
$$
From the fluid [continuity equation](@entry_id:145242) (derived below), we have $\dot{\rho} = -3\frac{\dot{a}}{a}(\rho+p)$. Substituting this in gives:
$$
\frac{\ddot{a}}{a} = \frac{4\pi G}{3c^4}\left(\frac{a}{\dot{a}}(-3\frac{\dot{a}}{a}(\rho+p)) + 2\rho\right) = \frac{4\pi G}{3c^4}(-3(\rho+p) + 2\rho) = \frac{4\pi G}{3c^4}(-\rho-3p)
$$
This simplifies to the **Second Friedmann Equation**, or the **Acceleration Equation**:
$$
\frac{\ddot{a}}{a} = -\frac{4\pi G}{3c^4}(\rho + 3p)
$$
This equation shows that the acceleration of the cosmic expansion is determined by the combination $\rho + 3p$. It reveals a remarkable feature of General Relativity: not only does energy density ($\rho$) cause gravitational attraction, but pressure ($p$) does as well. A large positive pressure contributes to the deceleration of the expansion. Conversely, a sufficiently large *negative* pressure can lead to [accelerated expansion](@entry_id:159601) ($\ddot{a}>0$), a concept central to the theory of cosmic inflation and the nature of dark energy.

### Consistency, Conservation, and the Bianchi Identity

We now have three key equations: the two Friedmann equations describing the gravitational dynamics, and a third equation describing the behavior of the matter itself. The local [conservation of energy and momentum](@entry_id:193044) is expressed by the vanishing [covariant divergence](@entry_id:275039) of the [stress-energy tensor](@entry_id:146544), $\nabla_\mu T^{\mu\nu} = 0$. For the [perfect fluid](@entry_id:161909) in an FLRW background, the $\nu=0$ component of this equation gives the **Fluid Continuity Equation**:
$$
\dot{\rho} + 3\frac{\dot{a}}{a}\left(\rho + p\right) = 0
$$
This equation describes how the energy density of the cosmic fluid dilutes as the universe expands.

Interestingly, these three equations are not independent. Any two of them can be used to derive the third. For example, by differentiating the first Friedmann equation with respect to time and using the fluid [continuity equation](@entry_id:145242) to substitute for $\dot{\rho}$, one can precisely recover the second Friedmann equation (the acceleration equation) [@problem_id:820137]. This demonstrates the deep self-consistency of the framework.

This interdependence is not a coincidence; it is a fundamental consequence of the mathematical structure of General Relativity. The Einstein tensor $G_{\mu\nu}$ is constructed from the metric in such a way that its [covariant divergence](@entry_id:275039) is always zero, a property known as the **contracted Bianchi identity**:
$$
\nabla_\mu G^{\mu\nu} \equiv 0
$$
This is a purely geometric identity, holding true for any metric. When we impose the Einstein Field Equations, $G^{\mu\nu} \propto T^{\mu\nu}$, this identity automatically implies that the [stress-energy tensor](@entry_id:146544) must be conserved: $\nabla_\mu T^{\mu\nu} = 0$. Thus, the law of local [energy-momentum conservation](@entry_id:191061) is built into the very fabric of Einstein's theory of gravity. One can explicitly verify that $\nabla_\mu G^{\mu 0} = 0$ for the FLRW metric by a direct, albeit lengthy, calculation involving the Christoffel symbols and the components of the Einstein tensor [@problem_id:820107]. This confirms that the fluid equation is not an additional assumption, but a necessary consequence of the gravitational dynamics.

This conservation law provides a powerful tool. For instance, if we consider a more complex fluid model, such as one including **[bulk viscosity](@entry_id:187773)** $\zeta$, the stress-energy tensor is modified, and the effective pressure becomes $p_{eff} = p - 3\zeta H$. Applying the conservation law $\nabla_\mu T^{\mu 0} = 0$ to this more general fluid directly yields the modified continuity equation for the viscous fluid [@problem_id:820078].

### The Action Principle and the Hamiltonian Constraint

An alternative and more profound derivation of the Friedmann equations stems from the **Einstein-Hilbert action principle**. The total action for gravity coupled to matter is:
$$
S = S_{EH} + S_m = \frac{c^4}{16\pi G} \int d^4x \sqrt{-g} R + S_m
$$
The equations of motion are found by demanding that the action is stationary ($\delta S = 0$) with respect to variations of the metric $g_{\mu\nu}$.

To apply this to cosmology, we can use a formulation that makes the [time-slicing](@entry_id:755996) of spacetime explicit. We introduce a **[lapse function](@entry_id:751141)** $N(t)$ into the FLRW metric:
$$
ds^2 = -N(t)^2 c^2 dt^2 + a(t)^2 \gamma_{ij} dx^i dx^j
$$
The standard FLRW metric corresponds to the choice $N=1$, which fixes the time coordinate to be the proper cosmic time. Varying the action with respect to the dynamical field $a(t)$ yields the second Friedmann equation. However, a special result comes from varying the action with respect to the non-dynamical [lapse function](@entry_id:751141) $N(t)$ [@problem_id:820123].

In the Hamiltonian formulation of General Relativity, the [lapse function](@entry_id:751141) acts as a Lagrange multiplier that enforces a constraint—the **Hamiltonian constraint**. Performing the variation $\delta S / \delta N = 0$ yields an equation that does not contain any second-order time derivatives. After substituting the reduced action for the FLRW metric and an appropriate matter action, this procedure yields an equation equivalent to:
$$
-\frac{3c^4}{8\pi G} \frac{a \dot{a}^2}{N^2} + \frac{3c^4}{8\pi G} k c^2 a - \rho a^3 = 0
$$
This is the Hamiltonian constraint for the FLRW universe. If we now make the gauge choice $N=1$ (i.e., we choose our time coordinate to be cosmic time), and rearrange the terms, we recover precisely the first Friedmann equation:
$$
\left(\frac{\dot{a}}{a}\right)^2 = \frac{8\pi G}{3c^2}\rho - \frac{kc^2}{a^2}
$$
This elegant derivation highlights the special status of the first Friedmann equation. It is not a true dynamical equation of motion in the same way the acceleration equation is; rather, it is a constraint equation that the state of the universe must satisfy at every instant in time.