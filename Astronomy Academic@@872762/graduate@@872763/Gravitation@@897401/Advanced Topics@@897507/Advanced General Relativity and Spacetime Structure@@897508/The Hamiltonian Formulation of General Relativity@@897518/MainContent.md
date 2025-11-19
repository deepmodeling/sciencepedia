## Introduction
General Relativity describes gravity not as a force, but as the [curvature of spacetime](@entry_id:189480). While Einstein's field equations masterfully connect this geometry to the distribution of matter and energy, their four-dimensional, covariant nature can make it challenging to understand the evolution of spacetime as a dynamical system. How does "space" evolve in "time"? This question lies at the heart of many profound problems in gravitational physics, from simulating [black hole mergers](@entry_id:159861) to quantizing gravity itself. The Hamiltonian formulation of General Relativity, developed by Richard Arnowitt, Stanley Deser, and Charles W. Misner (ADM), provides a powerful answer by recasting the theory into a framework analogous to classical Hamiltonian mechanics.

This article delves into the elegant structure and profound implications of the ADM formalism. By decomposing spacetime into a "3+1" structure—a stack of three-dimensional spatial slices evolving through time—this approach transforms General Relativity into an initial value problem. You will learn how the geometry of space becomes the fundamental configuration variable and how its evolution is governed by a set of powerful [constraint equations](@entry_id:138140). This reformulation is not merely a mathematical exercise; it is the bedrock of modern [numerical relativity](@entry_id:140327), a key gateway to canonical [quantum gravity](@entry_id:145111), and a source of deep insights into the nature of time and energy in the cosmos.

Across the following chapters, we will build a complete picture of this essential theoretical tool. The "Principles and Mechanisms" chapter will lay the groundwork, introducing the [3+1 decomposition](@entry_id:140329), the canonical variables, and the crucial Hamiltonian and momentum constraints. Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate the formalism's power by exploring its use in cosmology, black hole physics, and the numerical simulation of gravitational phenomena. Finally, the "Hands-On Practices" section will offer you the chance to solidify your understanding by working through concrete problems that showcase the core techniques of the Hamiltonian approach.

## Principles and Mechanisms

The Hamiltonian formulation of General Relativity, developed by Arnowitt, Deser, and Misner (ADM), recasts Einstein's field equations into a framework analogous to classical mechanics. This "3+1" decomposition of spacetime provides powerful tools for understanding the [initial value problem](@entry_id:142753), defining global quantities like mass and momentum, and forms the foundation for both [numerical relativity](@entry_id:140327) and canonical [quantum gravity](@entry_id:145111). This chapter elucidates the core principles and mechanisms of this formalism, building from its geometric underpinnings to its dynamical consequences.

### The 3+1 Decomposition of Spacetime

The central idea of the ADM formalism is the **[foliation](@entry_id:160209)** of four-dimensional (4D) spacetime into a one-parameter family of three-dimensional (3D) spacelike [hypersurfaces](@entry_id:159491), denoted $\Sigma_t$. Imagine spacetime as a loaf of bread; this [foliation](@entry_id:160209) is akin to slicing the loaf, where each slice represents all of "space" at a particular "moment" $t$. The coordinate $t$ labels the slices.

To describe the geometry of this sliced spacetime, we decompose the 4D spacetime metric $g_{\mu\nu}$ into quantities that have direct meaning with respect to this [foliation](@entry_id:160209). In a coordinate system $(t, x^i)$, where $x^i$ (for $i=1, 2, 3$) are coordinates on the slices $\Sigma_t$, the general [line element](@entry_id:196833) $ds^2 = g_{\mu\nu} dx^\mu dx^\nu$ can be expressed as:

$$ds^2 = (-N^2 + \gamma_{ij} N^i N^j) dt^2 + 2 \gamma_{ij} N^j dt dx^i + \gamma_{ij} dx^i dx^j$$

Here, the quantities $N$, $N^i$, and $\gamma_{ij}$ are the fundamental building blocks of the 3+1 geometry:

1.  The **induced spatial metric** $\gamma_{ij}$ is the metric on each 3D hypersurface $\Sigma_t$. It measures spatial distances *within* a slice for observers who are instantaneously at rest on that slice. Its determinant is denoted by $\gamma = \det(\gamma_{ij})$.

2.  The **[lapse function](@entry_id:751141)** $N(t, x^i)$ measures the rate of flow of proper time relative to the [coordinate time](@entry_id:263720) $t$ for a family of "Eulerian" observers who move along trajectories normal (perpendicular) to each slice. Specifically, the proper time interval $d\tau$ between two adjacent slices $\Sigma_t$ and $\Sigma_{t+dt}$ for such an observer is $d\tau = N dt$. The [lapse function](@entry_id:751141) can be thought of as governing the "spacing" between the slices.

3.  The **[shift vector](@entry_id:754781)** $N^i(t, x^i)$ describes how the spatial coordinates $x^i$ are "dragged" from one slice to the next. If an observer at $(t, x^i)$ moves purely normal to the slice, they will arrive at the next slice $\Sigma_{t+dt}$ at a different spatial coordinate position, $x^i - N^i dt$. The [shift vector](@entry_id:754781) thus describes the tangential component of the [time evolution](@entry_id:153943) vector.

To make these definitions concrete, consider the Rindler spacetime, which describes the viewpoint of a uniformly [accelerating observer](@entry_id:158352) in flat spacetime. The line element is given by $ds^2 = -(ax)^2 dt^2 + dx^2 + dy^2 + dz^2$, for a constant acceleration $a$. By direct comparison with the general 3+1 form, we can identify the components. The purely spatial part, $\gamma_{ij} dx^i dx^j$, is simply $dx^2 + dy^2 + dz^2$, implying that the spatial metric is the flat Euclidean metric, $\gamma_{ij} = \delta_{ij}$. There are no cross-terms of the form $dt dx^i$, which means the coefficient $2 \gamma_{ij} N^j$ must be zero. Since $\gamma_{ij}$ is invertible, this forces the [shift vector](@entry_id:754781) to be zero: $N^i = 0$. Finally, comparing the $dt^2$ coefficient, we have $-N^2 = -(ax)^2$, which, taking $N>0$, gives the [lapse function](@entry_id:751141) $N = ax$ [@problem_id:1865094]. This example illustrates that the [lapse and shift](@entry_id:140910) are not necessarily constant; they are fields on spacetime that encode our choice of coordinates and slicing.

Geometrically, the [foliation](@entry_id:160209) is defined by the family of [hypersurfaces](@entry_id:159491), which in turn defines a field of future-pointing, timelike unit normal vectors $n^\mu$. A vector is normal to a surface of constant $t$ if it is proportional to the gradient of the time coordinate function, $\partial_\mu t$. The [normalization condition](@entry_id:156486) $n_\mu n^\mu = -1$ (in the $-,+,+,+$ signature) fixes the proportionality factor, which is related to the [lapse function](@entry_id:751141), $N = (-g^{\mu\nu} \partial_\mu t \partial_\nu t)^{-1/2}$. Once $n^\mu$ is known, it serves as the foundation for defining the dynamics. For instance, in the Gullstrand-Painlevé coordinates for a Schwarzschild black hole, one can compute the components of this [normal vector](@entry_id:264185) directly from the spacetime metric, yielding $n^\mu = (1, -\sqrt{2GM/r}, 0, 0)$ [@problem_id:1865096]. This vector represents the four-velocity of an observer freely falling into the black hole, and the slices of constant $t$ are the rest spaces of these observers.

### Canonical Variables and the Phase Space

The ADM formalism transitions from this geometric picture to a Hamiltonian description. In this framework, the configuration variable of the gravitational field at a given time is the 3-metric of the spatial slice, $h_{ij}(x)$. (We will henceforth use $h_{ij}$ for the spatial metric to align with standard literature.) The corresponding canonical momentum is a [symmetric tensor](@entry_id:144567) density $\pi^{ij}(x)$. The pair $(h_{ij}, \pi^{ij})$ defines the state of the gravitational field on the slice $\Sigma_t$ and constitutes the **phase space** of the theory.

These canonical variables obey a set of fundamental **Poisson bracket relations**, analogous to $\{q, p\} = 1$ in classical mechanics. For fields, these relations are defined at every spatial point and involve the Dirac [delta function](@entry_id:273429):
$$ \{h_{ij}(\mathbf{x}), \pi^{kl}(\mathbf{y})\} = \frac{1}{2} (\delta_i^k \delta_j^l + \delta_i^l \delta_j^k) \delta^{(3)}(\mathbf{x} - \mathbf{y}) $$
$$ \{h_{ij}(\mathbf{x}), h_{kl}(\mathbf{y})\} = 0 $$
$$ \{\pi^{ij}(\mathbf{x}), \pi^{kl}(\mathbf{y})\} = 0 $$
The factor involving Kronecker deltas ensures that the bracket is symmetric under the exchange of indices $(k,l)$, reflecting the symmetry of $\pi^{kl}$. These relations form the algebraic backbone of the classical theory and are the starting point for [canonical quantization](@entry_id:148501), where the Poisson brackets are promoted to commutators.

These abstract relations can be used to compute the brackets of more complex quantities. For instance, we can compute the bracket between the determinant of the metric, $h = \det(h_{ij})$, and the trace of the momentum, $\pi = h_{ij}\pi^{ij}$. Using the functional [chain rule](@entry_id:147422) and the fundamental brackets, one finds that $\{h(\mathbf{x}), \pi(\mathbf{y})\} = 3 h(\mathbf{x}) \delta^{(3)}(\mathbf{x}-\mathbf{y})$ [@problem_id:1865086]. This exercise demonstrates how the canonical structure operates on functions over the phase space.

### The Dynamics of Geometry

The evolution from one slice to the next involves the change of the spatial metric $h_{ij}$. This change is captured by two key concepts: the time derivative of the metric and the extrinsic curvature.

The time derivative of the spatial metric, $\dot{h}_{ij} \equiv \partial_t h_{ij}$, is more precisely defined as the Lie derivative of $h_{ij}$ along the time-flow vector field $\vec{t} = N\vec{n} + \vec{N}$:
$$ \dot{h}_{ij} = \mathcal{L}_{\vec{t}} h_{ij} = \mathcal{L}_{N\vec{n} + \vec{N}} h_{ij} $$
The **extrinsic curvature** tensor, $K_{ij}$, measures the failure of vectors parallel-transported on the slice to remain tangent to the slice. It quantifies how the 3D slice $\Sigma_t$ is "curved" or "embedded" within the 4D spacetime. It is formally defined as the projection onto the slice of the covariant derivative of the normal vector, or equivalently, as half the Lie derivative of the spatial metric along the [normal vector](@entry_id:264185):
$$ K_{ij} = \frac{1}{2} \mathcal{L}_{\vec{n}} h_{ij} $$
By using the properties of the Lie derivative, we can relate the time evolution of the metric to the [extrinsic curvature](@entry_id:160405) and the shift. The total Lie derivative splits into two parts:
$$ \dot{h}_{ij} = \mathcal{L}_{N\vec{n}} h_{ij} + \mathcal{L}_{\vec{N}} h_{ij} = N (\mathcal{L}_{\vec{n}} h_{ij}) + \mathcal{L}_{\vec{N}} h_{ij} $$
Substituting the definition of $K_{ij}$, we arrive at a fundamental kinematic equation:
$$ \dot{h}_{ij} = 2 N K_{ij} + \mathcal{L}_{\vec{N}} h_{ij} $$
The term $\mathcal{L}_{\vec{N}} h_{ij}$ can be written explicitly using the spatial [covariant derivative](@entry_id:152476) $D_i$ compatible with $h_{ij}$ as $D_i N_j + D_j N_i$. This equation shows that the change in the spatial metric has two sources: a "stretching" normal to the slice, proportional to the extrinsic curvature and governed by the lapse $N$, and a "dragging" along the slice, described by the Lie derivative along the [shift vector](@entry_id:754781) $\vec{N}$ [@problem_id:1865105].

### The Hamiltonian and its Constraints

The transition to the Hamiltonian framework reveals one of the most profound features of General Relativity. When deriving the [canonical momenta](@entry_id:150209) from the Einstein-Hilbert Lagrangian written in 3+1 form, one finds that the Lagrangian contains no time derivatives of the lapse $N$ or the shift $N^i$. As a result, their conjugate momenta are identically zero:
$$ p_N = \frac{\delta \mathcal{L}}{\delta \dot{N}} = 0, \qquad p_{N^i} = \frac{\delta \mathcal{L}}{\delta \dot{N}^i} = 0 $$
In the theory of constrained Hamiltonian systems, these are called **[primary constraints](@entry_id:168143)**. Their physical interpretation is crucial: $N$ and $N^i$ are not true dynamical degrees of freedom of the gravitational field. Instead, they are arbitrary, user-specified functions that reflect the gauge freedom of General Relativity—the freedom to choose one's coordinate system, specifically the slicing and the spatial coordinate evolution [@problem_id:1865095]. They act as Lagrange multipliers in the Hamiltonian.

The total ADM Hamiltonian, which generates the time evolution of the system, is constructed as a linear combination of constraints weighted by these Lagrange multipliers:
$$ H_{ADM} = \int d^3x \, \left( N \mathcal{H} + N_i \mathcal{H}^i \right) $$
The quantities $\mathcal{H}$ and $\mathcal{H}^i$ are the **constraint densities**. They are functions of the canonical variables $(h_{ij}, \pi^{ij})$ and must vanish for any physical solution to Einstein's equations.

1.  The **Momentum Constraint** (or Diffeomorphism Constraint):
    $$ \mathcal{H}^i = -2 D_j \pi^{ji} $$
    The condition $\mathcal{H}^i=0$ is a set of three equations that ensure the theory is invariant under spatial [coordinate transformations](@entry_id:172727) (diffeomorphisms) on each slice. As we will see, the functional $H_{\vec{N}} = \int N_i \mathcal{H}^i d^3x$ is the generator of these transformations.

2.  The **Hamiltonian Constraint** (or Scalar Constraint):
    $$ \mathcal{H} = \frac{1}{\sqrt{h}} \left( \pi_{ij}\pi^{ij} - \frac{1}{d-1}(\pi)^2 \right) - \sqrt{h} R^{(3)} $$
    where $d=3$ is the spatial dimension, $\pi_{ij} = h_{ik}h_{jl}\pi^{kl}$, $\pi = h_{ij}\pi^{ij}$ is the trace of the momentum, and $R^{(3)}$ is the Ricci scalar of the 3-metric $h_{ij}$. The condition $\mathcal{H}=0$ is related to the freedom of time [reparameterization](@entry_id:270587) and encapsulates the most complex dynamics of the theory.

The time evolution of any phase space variable $F$ is given by Hamilton's equation, $\dot{F} = \{F, H_{ADM}\}$. Applying this to the spatial metric itself, we find:
$$ \dot{h}_{ij} = \{h_{ij}, H_{ADM}\} = \frac{\delta H_{ADM}}{\delta \pi^{ij}} = \frac{2N}{\sqrt{h}}\left(\pi_{ij}-\frac{1}{2}h_{ij}\pi\right) + D_{i}N_{j}+D_{j}N_{i} $$
This result, derived purely from the Hamiltonian structure [@problem_id:1865120], is the dynamical counterpart to the kinematic equation derived earlier. By inverting the relationship between momentum and [extrinsic curvature](@entry_id:160405), $\pi^{ij} = \sqrt{h}(K^{ij} - h^{ij}K)$, one can verify that these two expressions for $\dot{h}_{ij}$ are identical.

The structure of the Hamiltonian constraint density $\mathcal{H}$ is reminiscent of an [energy equation](@entry_id:156281). The first part is quadratic in the momenta and represents the kinetic energy density. This term can be written more elegantly using the **DeWitt supermetric**, $G_{ijkl}$, which defines a metric on the space of all 3-metrics ("[superspace](@entry_id:155405)"):
$$ \mathcal{H}_{kinetic} = \frac{1}{\sqrt{h}} G_{ijkl} \pi^{ij} \pi^{kl} $$
The DeWitt supermetric has the explicit form [@problem_id:1865108]:
$$ G_{ijkl} = \frac{1}{2} \left( h_{ik}h_{jl} + h_{il}h_{jk} - \frac{2}{d-1} h_{ij}h_{kl} \right) $$
The second part of $\mathcal{H}$, namely $-\sqrt{h}R^{(3)}$, depends only on the spatial metric $h_{ij}$ and acts as a potential energy density arising from the curvature of space. The Hamiltonian constraint $\mathcal{H}=0$ can thus be interpreted as a local "zero energy" condition, where the kinetic energy of the geometry's evolution is balanced by its potential energy from [spatial curvature](@entry_id:755140).

### Physical Consequences and Applications

The rich structure of the ADM formalism leads to profound physical insights.

#### Degrees of Freedom of Gravity
The canonical variables $(h_{ij}, \pi^{ij})$ consist of 6 components each (since they are symmetric $3\times3$ tensors), for a total of 12 phase space variables per spatial point. However, not all of these represent physical degrees of freedom. The four constraints $(\mathcal{H}, \mathcal{H}^i)$ impose four relations on these variables. Furthermore, the [gauge freedom](@entry_id:160491) associated with these [first-class constraints](@entry_id:164534) (the freedom to choose the four functions $N, N^i$) means that four additional variables are pure gauge. The counting is therefore:
$$ \text{Physical Phase Space DoF} = 12 (\text{initial}) - 4 (\text{constraints}) - 4 (\text{gauge}) = 4 $$
A physical system with 4 phase space dimensions has $4/2 = 2$ physical configuration degrees of freedom. These are the two propagating polarizations of gravitational waves [@problem_id:1865104]. The entire complex machinery of the ADM formalism correctly reproduces this fundamental result.

#### Total Energy: The ADM Mass
For spacetimes that are asymptotically flat (approaching Minkowski spacetime at spatial infinity), the Hamiltonian formalism provides a definition for the total mass-energy of the system. The **ADM mass** is defined by a [surface integral](@entry_id:275394) at spatial infinity, which can be related to the value of the Hamiltonian constraint. For a static, spherically symmetric spacetime, this simplifies to a limit involving the radial component of the spatial metric:
$$ M_{ADM} = \frac{1}{2} \lim_{r\to\infty} \left[ r \left( 1 - \frac{1}{h_{rr}(r)} \right) \right] $$
This formula shows that the total mass is determined by the $1/r$ deviation of the spatial geometry from flatness. For example, for a hypothetical metric with $h_{rr} = 1 + \beta/r + \gamma/r^2$, the ADM mass is simply $M_{ADM} = \beta/2$ [@problem_id:1865109]. The ADM mass is a conserved quantity and represents the total energy content of the spacetime as measured by a distant observer.

#### Cosmology and the Zero-Energy Universe
The interpretation of the Hamiltonian constraint as a zero-energy condition becomes particularly vivid in cosmology. For a homogeneous and isotropic Friedmann-Lemaître-Robertson-Walker (FLRW) universe, the complexities of the ADM formalism simplify dramatically. The Hamiltonian constraint $\mathcal{H}=0$ becomes equivalent to the first Friedmann equation:
$$ H^2 + \frac{k}{a^2} = \frac{8\pi G}{3}\rho_m $$
where $H$ is the Hubble parameter, $a$ is the scale factor, $k$ is the curvature index, and $\rho_m$ is the matter-energy density. This equation can be rearranged to state that the total energy density is zero: $\rho_g + \rho_m = 0$, where we have defined an "effective [gravitational energy](@entry_id:193726) density" as $\rho_g = -\frac{3}{8\pi G}\left(H^2 + \frac{k}{a^2}\right)$ [@problem_id:1865115]. This suggests the striking picture of the universe having zero total energy, with the positive energy of matter and radiation being perfectly balanced by the [negative energy](@entry_id:161542) associated with the gravitational field itself.

#### Symmetries and Conservation Laws
The constraint formalism provides an elegant realization of Noether's theorem. The [momentum constraint](@entry_id:160112), in particular, acts as the generator of spatial diffeomorphisms. If a spatial slice admits a [geometric symmetry](@entry_id:189059), such as a Killing vector field $\xi^i$ satisfying $\mathcal{L}_\xi h_{ij} = 0$, there is an associated conserved quantity. The phase space functional $P[\xi] = \int \xi^i \mathcal{H}_i d^3x$ generates the infinitesimal spatial displacement along $\xi^i$. Its time evolution is given by the Poisson bracket $\{P[\xi], H_{ADM}\}$. Using the known algebra of the constraints, this bracket evaluates to zero if the [lapse and shift](@entry_id:140910) functions are also symmetric with respect to the Killing vector (i.e., $\mathcal{L}_\xi N = 0$ and $\mathcal{L}_\xi N^i=0$). This confirms that the quantity associated with the spatial symmetry is indeed conserved during the evolution [@problem_id:1865090].

#### The Problem of Time
The fact that the total Hamiltonian is a sum of constraints that must vanish, $H_{ADM} \approx 0$, leads to deep conceptual issues in [quantum gravity](@entry_id:145111), collectively known as the **[problem of time](@entry_id:202825)**. If the Hamiltonian is zero, what generates evolution? In the classical theory, the non-zero [lapse and shift](@entry_id:140910) functions drive the dynamics. However, a physical observable, in the strictest sense (a **Dirac observable**), should have a vanishing Poisson bracket with all constraints. Most quantities one might think of as observable, such as the total volume of space, $V = \int \sqrt{h} d^3x$, are not Dirac [observables](@entry_id:267133). A direct calculation shows that the Poisson bracket with the Hamiltonian is non-zero [@problem_id:1865123]:
$$ \{H_{ADM}, V\} = \int \left( \frac{N}{2} h_{ij}\pi^{ij} - \sqrt{h} D_i N^i \right) d^3x $$
This means that the change in the volume of the universe depends on the arbitrary choice of the [lapse function](@entry_id:751141) $N$. How to define time and evolution in a quantum theory where the Hamiltonian vanishes and simple quantities like volume are not well-defined [observables](@entry_id:267133) remains one of the central unresolved challenges in theoretical physics, a challenge laid bare by the elegant structure of the Hamiltonian formulation.