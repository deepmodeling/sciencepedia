## Introduction
While the Einstein field equations provide a concise description of how matter curves spacetime, a deeper understanding of gravity's dynamics, its symmetries, and its path toward a quantum theory requires a more fundamental perspective. The Lagrangian and Hamiltonian formulations of General Relativity offer precisely this insight, recasting the theory in the powerful language of classical mechanics. This approach uncovers the true degrees of freedom of the gravitational field and addresses foundational questions about the nature of time and evolution in a relativistic context. It reveals that the standard Einstein-Hilbert action is incomplete and requires modification, leading to a framework where spacetime dynamics are governed by a set of profound constraint equations.

This article will guide you through this elegant and powerful reformulation of Einstein's theory. In **Principles and Mechanisms**, we will deconstruct the action principle, introduce the 3+1 decomposition of spacetime, and derive the pivotal Hamiltonian and momentum constraints. Next, in **Applications and Interdisciplinary Connections**, we will explore how this formalism is the essential toolkit for modern research in cosmology, black hole physics, numerical relativity, and quantum gravity. Finally, **Hands-On Practices** will provide you with the opportunity to apply these concepts to concrete physical problems, solidifying your understanding of the dynamics of spacetime itself.

## Principles and Mechanisms

Having established the foundational role of the Einstein-Hilbert action in the previous chapter, we now delve into the deeper structural properties of general relativity revealed through the Lagrangian and Hamiltonian formulations. This analysis is not merely a mathematical repackaging; it is essential for understanding the theory's constraint structure, the nature of time, and provides the bedrock for canonical quantization and numerical relativity. We will proceed by first addressing a subtlety in the action principle itself, then reformulating the theory by decomposing spacetime into space and time—the celebrated 3+1 formalism—and finally, constructing the Hamiltonian framework that exposes the true dynamical content of gravity.

### The Action Principle and the Gibbons-Hawking-York Boundary Term

The standard Einstein-Hilbert action is given by:
$$
S_{EH} = \frac{1}{2\kappa} \int_{\mathcal{M}} R \sqrt{-g} \, d^4x
$$
where $R$ is the four-dimensional Ricci scalar, $g$ is the determinant of the metric $g_{\mu\nu}$, and $\kappa = 8\pi G$ (in units where $c=1$). Variation of this action with respect to the metric $g_{\mu\nu}$ is intended to yield the vacuum Einstein field equations, $R_{\mu\nu} - \frac{1}{2}g_{\mu\nu}R = 0$. However, a careful analysis of the variation reveals a complication. The Ricci scalar contains second derivatives of the metric, which, upon integration by parts, produce a boundary term in addition to the bulk term yielding the field equations.

Specifically, the variation $\delta S_{EH}$ contains a surface integral over the boundary $\partial\mathcal{M}$ of the spacetime manifold $\mathcal{M}$. For a well-posed variational principle under Dirichlet boundary conditions—where the metric variation $\delta g_{\mu\nu}$ is specified to vanish on the boundary—this boundary term must also vanish. Unfortunately, the boundary term resulting from the Einstein-Hilbert action involves not only $\delta g_{\mu\nu}$ but also its normal derivatives. Consequently, fixing the metric on the boundary is insufficient to make the action stationary.

To see this more clearly, the boundary term that arises from varying $S_{EH}$ can be expressed as an integral whose integrand involves variations of the Christoffel symbols, $\delta\Gamma^\lambda_{\mu\nu}$. As explored in [@problem_id:983242], this integrand can be written as $\mathcal{I} = n_\alpha (g^{\mu\nu}\delta\Gamma^\alpha_{\mu\nu} - g^{\mu\alpha}\delta\Gamma^\beta_{\mu\beta})$, where $n^\alpha$ is the unit normal to the boundary. In a special coordinate system adapted to the boundary (Gaussian Normal Coordinates), this expression can be shown to be proportional to the variation of the trace of the **extrinsic curvature**, $\delta K$.

The extrinsic curvature, $K_{\mu\nu}$, measures how the boundary hypersurface is curved with respect to the embedding 4D spacetime. The presence of its variation in the boundary term shows that the Einstein-Hilbert action, on its own, is not suitable for a variational principle where we fix only the metric on the boundary.

To resolve this issue, one must add a counter-term to the action whose variation precisely cancels this problematic boundary term. This is the **Gibbons-Hawking-York (GHY) boundary term**:
$$
S_{GHY} = \frac{1}{\kappa} \int_{\partial\mathcal{M}} K \sqrt{|h|} \, d^3y
$$
Here, the integral is over the boundary $\partial\mathcal{M}$, $h$ is the determinant of the induced metric $h_{\mu\nu}$ on the boundary, and $K$ is the trace of the boundary's extrinsic curvature. The total action, $S = S_{EH} + S_{GHY}$, now has the desired property: its variation yields the Einstein equations in the bulk, and the boundary terms cancel out, provided that the variation of the induced metric $\delta h_{\mu\nu}$ vanishes on the boundary. This renders the variational problem well-posed. The calculation in [@problem_id:983316] of the residual boundary term for a variation on the boundary of Anti-de Sitter space illustrates how such terms are computed and underscores their non-trivial nature.

It is worth noting that this entire discussion presumes that the connection is the Levi-Civita connection, determined uniquely by the metric. An alternative approach, the **Palatini formalism**, treats the metric $g_{\mu\nu}$ and the connection $\Gamma^\lambda_{\mu\nu}$ as independent fields. Varying the action with respect to the connection then yields an equation of motion for $\Gamma$. As demonstrated in [@problem_id:983423], for the action $S = \int \sqrt{-g} R(\Gamma) d^4x$, the solution to this equation is precisely that $\Gamma$ must be the Levi-Civita connection of $g_{\mu\nu}$. This justifies, a posteriori, the standard assumption made in the metric formulation.

### The 3+1 Decomposition of Spacetime

The Hamiltonian formulation of any field theory requires a distinction between "space" and "time". In general relativity, such a split is not God-given; it must be introduced by the observer. This is achieved by foliating the 4-dimensional spacetime manifold $\mathcal{M}$ into a one-parameter family of spacelike hypersurfaces $\Sigma_t$, parameterized by a global time coordinate $t$. This procedure is known as the **3+1 decomposition** or the **Arnowitt-Deser-Misner (ADM) formalism**.

This decomposition allows us to describe the 4D spacetime geometry using three fundamental objects defined with respect to this foliation:

1.  The **Lapse Function**, $N(t, x^i)$: A scalar field that measures the proper time interval $d\tau$ between two adjacent hypersurfaces, $\Sigma_t$ and $\Sigma_{t+dt}$, for an observer moving along the normal to the hypersurfaces. As shown in [@problem_id:983318], the worldline of such a "normal" or "Eulerian" observer satisfies $dx^i + N^i dt = 0$. Substituting this into the general line element (presented below) gives $ds^2 = -N^2 dt^2$. Since for a timelike path $ds^2 = -d\tau^2$, we find the crucial physical interpretation of the lapse:
    $$
    d\tau = N dt
    $$
    The lapse function dictates the rate at which physical time flows relative to the coordinate time $t$.

2.  The **Shift Vector**, $N^i(t, x^j)$: A vector field within each hypersurface $\Sigma_t$. It describes the spatial displacement between the point on $\Sigma_t$ with spatial coordinates $x^i$ and the point on $\Sigma_{t+dt}$ that lies on the same normal line. In essence, it describes how the spatial coordinate grid is "dragged along" from one slice to the next.

3.  The **Spatial Metric**, $\gamma_{ij}(t, x^k)$: The 3-dimensional Riemannian metric induced on each spacelike hypersurface $\Sigma_t$. It measures intrinsic distances within each slice.

With these variables, the 4-dimensional spacetime line element $ds^2 = g_{\mu\nu}dx^\mu dx^\nu$ can be written in the ADM form:
$$
ds^2 = -N^2 dt^2 + \gamma_{ij} (dx^i + N^i dt)(dx^j + N^j dt)
$$
Expanding this expression allows us to read off the components of the 4D metric tensor $g_{\mu\nu}$ in the $(t, x^i)$ coordinate system:
$$
g_{00} = -N^2 + N_k N^k, \quad g_{0i} = N_i, \quad g_{ij} = \gamma_{ij}
$$
where $N_i = \gamma_{ij}N^j$ and $N_k N^k = \gamma_{ij}N^i N^j$. Conversely, given a 4D metric and a choice of time foliation, we can extract the ADM variables.

For instance, consider the spacetime described by the line element $ds^2 = -(a\rho)^2 d\eta^2 + d\rho^2 + dy^2 + dz^2$ and a new time coordinate $t = \eta - k\rho$, as in [@problem_id:983300]. By expressing $d\eta$ in terms of $dt$ and $d\rho$ and substituting into the line element, we can rewrite it in the ADM form. Comparing the resulting components $g_{tt}$, $g_{t\rho}$, and $g_{\rho\rho}$ with the general ADM metric components allows us to solve for the lapse function, yielding $N = a\rho / \sqrt{1 - k^2(a\rho)^2}$. This exercise demonstrates the concrete procedure for performing the 3+1 split and reveals that the lapse and shift are not fixed properties of spacetime, but depend on our choice of slicing.

### The ADM Lagrangian and Hamiltonian

The next step is to express the total gravitational action $S = S_{EH} + S_{GHY}$ in terms of the ADM variables. This requires rewriting the 4D Ricci scalar $R$ in terms of the intrinsic curvature of the 3-slices and their extrinsic curvature. The intrinsic curvature is captured by the 3D Ricci scalar ${}^{(3)}R$ computed from the spatial metric $\gamma_{ij}$. The extrinsic curvature, $K_{ij}$, measures the failure of a vector normal to the slice to remain normal when parallel transported along a direction within the slice. It describes how the 3-slice is embedded in the 4D spacetime and is defined as:
$$
K_{ij} = \frac{1}{2N} \left( \dot{\gamma}_{ij} - D_i N_j - D_j N_i \right)
$$
Here, a dot represents a partial derivative with respect to time, $\partial/\partial t$, and $D_i$ is the covariant derivative compatible with the spatial metric $\gamma_{ij}$. The term $\dot{\gamma}_{ij}$ captures the change in the spatial metric between slices, while the terms involving the shift vector account for changes due to the shifting of the coordinate system. Thus, $K_{ij}$ represents the "velocity" of the spatial geometry.

Through a substantial calculation (the Gauss-Codazzi relations), the 4D action can be rewritten in the ADM form:
$$
S_{ADM} = \frac{1}{16\pi G} \int dt d^3x \, N \sqrt{\gamma} \left( {}^{(3)}R + K_{ij}K^{ij} - K^2 \right)
$$
where $K = \gamma^{ij}K_{ij}$ is the trace of the extrinsic curvature. This Lagrangian has a clear structure. The term ${}^{(3)}R$ acts as a potential energy density, depending only on the configuration of the spatial metric $\gamma_{ij}$. The terms quadratic in the extrinsic curvature, $K_{ij}K^{ij} - K^2$, act as a kinetic energy density, as $K_{ij}$ is linear in the "velocity" $\dot{\gamma}_{ij}$. The lapse function $N$ and the shift vector $N^i$ (hidden inside $K_{ij}$) appear without time derivatives.

### The Constraint Structure of General Relativity

The absence of time derivatives $\dot{N}$ and $\dot{N}_i$ in the ADM Lagrangian is a profound feature with far-reaching consequences. In the language of Lagrangian mechanics, it means that $N$ and $N_i$ are not dynamical degrees of freedom. Instead, they function as Lagrange multipliers.

To move to the Hamiltonian formulation, we first define the canonical momentum $\pi^{ij}$ conjugate to the spatial metric $\gamma_{ij}$:
$$
\pi^{ij} = \frac{\delta \mathcal{L}_{ADM}}{\delta \dot{\gamma}_{ij}} = \frac{\sqrt{\gamma}}{16\pi G} (K^{ij} - \gamma^{ij}K)
$$
The momenta conjugate to the lapse and shift are, due to the structure of the Lagrangian:
$$
\pi_N = \frac{\delta \mathcal{L}_{ADM}}{\delta \dot{N}} = 0, \quad \pi^i = \frac{\delta \mathcal{L}_{ADM}}{\delta \dot{N}_i} = 0
$$
These equations, $\pi_N \approx 0$ and $\pi^i \approx 0$, are known as **primary constraints** of the theory. The symbol $\approx$ denotes a "weak equality," meaning the relation holds on the constraint surface of the phase space, where physical states lie. It is crucial to note that these constraints arise from the specific form of the standard ADM action. As illustrated in [@problem_id:983370], one could add a total time derivative term to the Lagrangian density, which would not change the equations of motion but would lead to a non-zero canonical momentum for the shift vector. This highlights that the constraint structure is tied to a specific canonical representation of the dynamics.

The Hamiltonian is constructed via the Legendre transform, $H = \int d^3x (\pi^{ij}\dot{\gamma}_{ij} - \mathcal{L}_{ADM})$. After expressing $\dot{\gamma}_{ij}$ in terms of $\pi^{ij}$, the Hamiltonian density $\mathcal{H}$ takes the form:
$$
\mathcal{H} = N\mathcal{H}_{\perp} + N_i\mathcal{H}^{i}
$$
where
$$
\mathcal{H}_{\perp} = \frac{16\pi G}{\sqrt{\gamma}}\left(\pi_{ij}\pi^{ij} - \frac{1}{2}\pi^2\right) - \frac{\sqrt{\gamma}}{16\pi G} {}^{(3)}R
$$
$$
\mathcal{H}^{i} = -2D_j \pi^{ij}
$$
The total Hamiltonian is $H_c = \int d^3x (N\mathcal{H}_{\perp} + N_i\mathcal{H}^{i})$.

Since $N$ and $N_i$ are Lagrange multipliers, varying the action (or the Hamiltonian) with respect to them imposes constraints on the dynamical variables $(\gamma_{ij}, \pi^{ij})$. Varying with respect to $N$ yields the **Hamiltonian constraint** (or energy constraint), $\mathcal{H}_{\perp} \approx 0$. Varying with respect to $N_i$ yields the **momentum constraint**, $\mathcal{H}^i \approx 0$. The momentum constraint equation, $D_j(K^{ij} - \gamma^{ij}K) = 0$, derived from varying the action [@problem_id:983346], is a statement of the conservation of a specific spatial tensor related to the canonical momentum. The structure of the Hamiltonian constraint, involving spatial derivatives of the metric (in ${}^{(3)}R$) and quadratic momentum terms, is foreshadowed by the structure of the $G_{00}=0$ Einstein equation, which can be seen to contain spatial Laplacian terms when analyzed directly from the Lagrangian [@problem_id:983416].

A more rigorous derivation of these constraints comes from Dirac's procedure for constrained systems. The primary constraints must be preserved under time evolution, which is governed by the Poisson bracket with the total Hamiltonian. The condition $\dot{\pi}^i = \{\pi^i, H_c\} \approx 0$ leads directly to the secondary constraint $\mathcal{H}^i \approx 0$. As shown explicitly in [@problem_id:98251], the evaluation of this Poisson bracket yields $\mathcal{H}^i = -2D_j\pi^{ij}$, thus re-deriving the momentum constraint from the consistency of the Hamiltonian evolution. A similar procedure for $\pi_N$ yields the Hamiltonian constraint $\mathcal{H}_\perp \approx 0$.

### Constraints as Generators and the Path to Quantum Gravity

The Hamiltonian and momentum constraints are not merely restrictions; they are the generators of the fundamental symmetries of general relativity. The momentum constraint, $\mathcal{H}_i$, generates infinitesimal spatial coordinate transformations (diffeomorphisms) on the 3-slice. The Hamiltonian constraint, $\mathcal{H}_{\perp}$, generates infinitesimal time evolution, deforming the 3-slice in the direction normal to itself. The fact that the Hamiltonian is a sum of constraints implies that the dynamics of GR is pure gauge—the "evolution" is simply a relabeling of coordinates and a choice of time slicing. The true, physical degrees of freedom are those quantities that are invariant under these transformations.

This perspective is the gateway to the canonical quantization of gravity. In this approach, the phase space variables $(\gamma_{ij}, \pi^{ij})$ are promoted to quantum operators, and the state of the universe is described by a wave functional $\Psi[\gamma_{ij}]$. The classical constraints become operator equations that annihilate the physical state:
$$
\hat{\mathcal{H}}_i \Psi[\gamma_{ij}] = 0
$$
$$
\hat{\mathcal{H}}_{\perp} \Psi[\gamma_{ij}] = 0
$$
The first set of equations ensures the wave functional is independent of the choice of spatial coordinates on the slice. The second equation, known as the **Wheeler-DeWitt equation**, is the central equation of canonical quantum gravity. It encapsulates the dynamics of the theory and famously lacks an explicit time parameter, leading to the "problem of time" in quantum gravity.

In general, the Wheeler-DeWitt equation is an intractable functional differential equation. However, for highly symmetric spacetimes, the infinite degrees of freedom of the gravitational field can be truncated to a finite number, a procedure that leads to **minisuperspace models**. For example, in the case of a vacuum Bianchi I universe [@problem_id:983254], the geometry is described by three scale factors, which can be parameterized by variables $(\alpha, \beta_+, \beta_-)$ describing the volume and anisotropy. For this model, the kinetic part of the Hamiltonian constraint operator remarkably simplifies to the form of a 2+1 dimensional wave operator on this minisuperspace:
$$
\hat{H}_{kin} = \frac{\partial^2}{\partial \alpha^2} - \frac{\partial^2}{\partial \beta_+^2} - \frac{\partial^2}{\partial \beta_-^2}
$$
The Wheeler-DeWitt equation becomes a partial differential equation on the space of possible 3-geometries, and its solutions, like the wave function analyzed in [@problem_id:983254], describe the quantum behavior of the universe's volume and shape. This application to quantum cosmology demonstrates the profound power and utility of the Hamiltonian formulation, which transforms our understanding of Einstein's theory from a set of spacetime field equations into a framework describing the evolution of spatial geometry itself.