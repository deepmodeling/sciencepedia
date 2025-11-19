## Introduction
Flows past corners and free jets represent a class of phenomena fundamental to fluid mechanics, with profound implications across science and engineering. The behavior of a fluid as it navigates a sharp geometric feature or emerges into an open space is critical to countless applications, from industrial [extrusion](@entry_id:157962) and ink-jet printing to the dispersal of pollutants and the dynamics of [astrophysical jets](@entry_id:266808). However, accurately describing these flows presents a significant challenge, requiring a bridge between elegant but simplified ideal models and the complex realities of viscosity, compressibility, and non-Newtonian effects. This article provides a comprehensive exploration of these topics, guiding the reader from foundational theory to practical application.

To build this understanding, we will first delve into the foundational 'Principles and Mechanisms,' starting with [potential flow theory](@entry_id:267452) and powerful analytical tools like [conformal mapping](@entry_id:144027) before incorporating the effects of viscosity through [self-similar solutions](@entry_id:164839) and examining flow instabilities. Subsequently, the 'Applications and Interdisciplinary Connections' chapter will demonstrate how these core concepts are applied across diverse fields, from materials science and aeronautics to geophysics and [microfluidics](@entry_id:269152). Finally, the 'Hands-On Practices' section provides an opportunity to apply these theoretical insights to concrete problems, solidifying your grasp of the subject.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms governing flows past corners and the formation and dynamics of free jets. We will progress from the elegant constructs of ideal fluid theory to the more complex realities introduced by viscosity, [compressibility](@entry_id:144559), and non-Newtonian fluid behavior. Throughout, we will employ powerful analytical and [asymptotic methods](@entry_id:177759) to dissect these phenomena, revealing the underlying physics that dictate [flow patterns](@entry_id:153478), stability, and structure.

### Ideal Fluid Models: Potential Flow in Corners and Free Surfaces

In the realm of high-Reynolds-number flows, away from solid boundaries, the effects of viscosity are often negligible. This allows us to model the fluid as **ideal**: inviscid, incompressible, and irrotational. Such flows are known as **potential flows**, as the velocity field $\mathbf{u}$ can be expressed as the gradient of a scalar [velocity potential](@entry_id:262992) $\phi$, i.e., $\mathbf{u} = \nabla\phi$. For an incompressible fluid, the [continuity equation](@entry_id:145242) $\nabla \cdot \mathbf{u} = 0$ reduces to the Laplace equation for the potential, $\nabla^2\phi=0$.

For two-dimensional flows, the mathematical framework becomes particularly powerful through the use of complex analysis. The flow is described by a **[complex potential](@entry_id:162103)** $w(z) = \phi(x,y) + i\psi(x,y)$, where $z=x+iy$ is the position in the complex plane and $\psi$ is the stream function. The complex potential is an [analytic function](@entry_id:143459) of $z$, and its derivative yields the [complex velocity](@entry_id:201810), $\frac{dw}{dz} = u - iv$.

#### Conformal Mapping and Corner Flows

A key challenge in [potential flow](@entry_id:159985) is satisfying the boundary condition of no penetration ($\psi = \text{constant}$) on complex geometries. **Conformal mapping** is a formidable technique that transforms a complex domain into a simpler one, such as a half-plane, where the problem is easier to solve.

Consider the flow within a 90-degree corner, defined by the first quadrant ($x \ge 0, y \ge 0$), containing a line sink of strength $m$ at a point $z_0 = a+ib$. The rigid walls along the positive x and y axes impose boundary conditions. The mapping $Z = z^2$ elegantly "unfolds" this corner: the positive x-axis ($z=x$) maps to the positive real axis in the $Z$-plane ($Z=x^2$), while the positive y-axis ($z=iy$) maps to the negative real axis ($Z=-y^2$). The entire corner boundary becomes the real axis in the $Z$-plane.

The problem is now transformed into finding the potential for a sink at $Z_0 = z_0^2$ in the [upper half-plane](@entry_id:199119) above a solid wall. This is readily solved using the **[method of images](@entry_id:136235)**. To ensure the real axis is a streamline, we place an image sink of the same strength at the conjugate position $\bar{Z_0}$. The [complex potential](@entry_id:162103) for a sink of strength $m$ at $Z_s$ is $-m \ln(Z - Z_s)$. Thus, the total potential in the $Z$-plane is the sum of the potentials from the source and its image:

$w(Z) = -m \ln(Z - Z_0) - m \ln(Z - \bar{Z_0}) = -m \ln((Z - Z_0)(Z - \bar{Z_0}))$

Transforming back to the physical $z$-plane by substituting $Z=z^2$, $Z_0=z_0^2$, and $\bar{Z_0} = \bar{z_0}^2$, we obtain the complex potential for the sink in the corner:

$w(z) = -m \ln((z^2 - z_0^2)(z^2 - \bar{z_0}^2))$

Stagnation points, where the velocity is zero, are found by setting the [complex velocity](@entry_id:201810) $\frac{dw}{dz}$ to zero. Differentiating the potential gives:

$\frac{dw}{dz} = -2mz \frac{2z^2 - (z_0^2 + \bar{z_0}^2)}{(z^2 - z_0^2)(z^2 - \bar{z_0}^2)}$

Setting the numerator to zero reveals [stagnation points](@entry_id:276398) at $z=0$ (the corner itself) and at locations satisfying $2z^2 - (z_0^2 + \bar{z_0}^2) = 0$. Using $z_0=a+ib$, we find $z_0^2 + \bar{z_0}^2 = 2(a^2 - b^2)$. This gives the location of the second stagnation point as $z_s^2 = a^2 - b^2$. The distance $d$ of this point from the origin is therefore $d = |z_s| = \sqrt{|a^2-b^2|}$. If $a \gt b$, the stagnation point lies on the x-axis; if $b \gt a$, it lies on the y-axis. This elegant solution demonstrates the power of [conformal mapping](@entry_id:144027) in handling intricate boundary geometries [@problem_id:512825].

The concept of corner flows can be extended to three dimensions. Consider a flow in a rigid trihedral corner formed by three orthogonal planes ($x,y,z \gt 0$). Here, the velocity potential $\Phi$ must satisfy Laplace's equation $\nabla^2\Phi=0$ with no-[flux boundary conditions](@entry_id:749481) ($\frac{\partial\Phi}{\partial n}=0$) on the walls. Solutions near the corner can be sought in the form of separable solutions in [spherical coordinates](@entry_id:146054), $\Phi(r,\theta,\phi) = r^\nu F(\theta,\phi)$. The lowest-order regular, non-trivial solution that is also antisymmetric upon exchanging $x$ and $y$ corresponds to an eddy-like motion. By solving the associated Laplace-Beltrami equation for the angular function $F(\theta,\phi)$ with the appropriate boundary and symmetry conditions, this mode is found to have an exponent $\nu=2$. The corresponding potential is given by:

$\Phi(r, \theta, \phi) = C r^2 \sin^2\theta \cos(2\phi)$

where $C$ is an arbitrary constant. This solution represents the weakest possible regular flow that can exist deep within such a 3D corner [@problem_id:512828].

#### Free-Surface Jets and the Hodograph Method

When a liquid jet issues into a region of constant pressure, its boundary is a **free streamline**, the shape of which is not known in advance. This poses a significant challenge for [potential flow theory](@entry_id:267452). The **[hodograph](@entry_id:195718) method** provides a path forward by transforming the problem from the physical plane ($z$-plane) to the velocity plane ($u-iv$ plane), where the free [streamlines](@entry_id:266815) become known curves. This is often accomplished using the **Schwarz-Christoffel transformation**.

A classic application is the determination of the **contraction coefficient** $C_c$ for a jet issuing from a channel. Consider a symmetric 2D jet emerging from a converging channel with a half-angle $\alpha=\pi/2$. The flow is analyzed using an auxiliary complex plane $s$ and the [hodograph](@entry_id:195718) variable $\Omega = \ln(U_j^{-1} dw/dz)$, where $U_j$ is the final jet velocity. The problem can be parameterized such that the complex potential is $w(s) = -\frac{Q}{\pi} \ln s$ and the [hodograph](@entry_id:195718) variable is $\Omega(s) = (1-\frac{\alpha}{\pi}) \cosh^{-1}(1-2s)$, with $Q$ being the flow rate in the upper half-domain.

To find the jet's shape, we must relate the physical coordinate $z$ to the parameter $s$. This is done via the relation $\frac{dz}{ds} = \frac{dz}{dw}\frac{dw}{ds}$. Using $\frac{dw}{dz} = U_j e^{\Omega(s)}$, we have:

$\frac{dz}{ds} = U_j^{-1}e^{-\Omega(s)} \left(-\frac{Q}{\pi s}\right)$

For the case $\alpha = \pi/2$, this simplifies to $\Omega(s) = \frac{i}{2} \arccos(1-2s)$ on the free [streamline](@entry_id:272773) ($s \in (0,1)$). By integrating $dz$ from the point of detachment ($s=1$) to a point far downstream in the jet ($s=0$), we can find the total change in the jet's half-width. This integration is simplified by a [change of variables](@entry_id:141386) $s = \sin^2\theta$. The imaginary part of the resulting integral gives the difference between the final jet half-width, $h_f = Q/U_j$, and the channel exit half-width, $h_0$. The calculation yields the relation $h_f - h_0 = -2h_f/\pi$. The contraction coefficient $C_c = h_f/h_0$ is then found to be:

$C_c = \frac{\pi}{\pi+2}$

This result, derived purely from [potential flow theory](@entry_id:267452), provides a precise prediction for the narrowing of the jet, a phenomenon known as the *[vena contracta](@entry_id:273611)* [@problem_id:512869].

### Viscous Flows and Self-Similarity

When [viscous forces](@entry_id:263294) are significant, the governing equations are the Navier-Stokes equations. While analytically complex, certain flow configurations admit **[self-similar solutions](@entry_id:164839)**, where the velocity profile shape remains constant along the flow direction, while its characteristic length and velocity scales evolve according to power laws. This powerful concept reduces the partial differential equations of motion to more tractable ordinary differential equations (ODEs).

#### Creeping Flow from a Point Source of Momentum

In the limit of very low Reynolds number ([creeping flow](@entry_id:263844) or Stokes flow), inertial terms in the Navier-Stokes equations are negligible. A fundamental solution in this regime is the flow produced by a point source of momentum (a Stokeslet), which is a cornerstone of [creeping flow](@entry_id:263844) analysis. Consider a submerged axisymmetric jet issuing from a [point source](@entry_id:196698) into a highly viscous fluid. The flow exhibits self-similarity, with the velocity decaying as $1/r$ from the source. This behavior is captured by a [stream function](@entry_id:266505) of the form $\psi(r, \theta) = r f(\cos\theta)$.

For a jet injected into a quiescent fluid, the appropriate angular function is $f(\cos\theta) = K(1-\cos^2\theta)$, where $K$ is a constant. The velocity components are derived from the [stream function](@entry_id:266505):

$u_r = \frac{1}{r^2 \sin\theta} \frac{\partial \psi}{\partial \theta} = \frac{2K\cos\theta}{r}$

$u_\theta = -\frac{1}{r \sin\theta} \frac{\partial \psi}{\partial r} = -\frac{K\sin\theta}{r}$

The constant $K$ can be determined from a physical measurement. If the velocity along the jet axis ($\theta=0$) is measured to be $U_0$ at a distance $r_0$, we have $u_r(r_0, 0) = U_0 = 2K/r_0$, which gives $K = U_0 r_0 / 2$. Substituting this back allows us to express the entire velocity field in terms of the measured parameters. For instance, the tangential velocity is:

$u_\theta(r, \theta) = -\frac{U_0 r_0}{2r}\sin\theta$

This example illustrates how a simple self-similar form can fully characterize a [creeping flow](@entry_id:263844) field based on a single measurement [@problem_id:512794].

#### The Laminar Wall Jet

Another canonical example of [self-similarity](@entry_id:144952) is the two-dimensional laminar [wall jet](@entry_id:261586), where a jet spreads along a solid surface. The flow is described by the boundary-layer equations. A [similarity solution](@entry_id:152126) can be found by introducing the [stream function](@entry_id:266505) $\psi(x,y) = 4\nu D x^{1/4} F(\eta)$ with a similarity variable $\eta = D y x^{-3/4}$. Here, $x$ is the distance along the plate, $y$ is the normal distance, $\nu$ is the [kinematic viscosity](@entry_id:261275), and $D$ is a constant. This transformation collapses the boundary-layer equations into a single ODE for the dimensionless function $F(\eta)$:

$F'''(\eta) + F(\eta)F''(\eta) + 2(F'(\eta))^2 = 0$

with boundary conditions $F(0)=0$, $F'(0)=0$ (no-slip at the wall), and $F'(\infty)=0$ (quiescent fluid far away). Remarkably, we can derive a universal relationship between key physical quantities without solving this ODE explicitly. The wall shear stress $\tau_w(x)$ and the kinematic [momentum flux](@entry_id:199796) $K(x) = \int_0^\infty u^2 dy$ can be expressed in terms of $F$ and its derivatives. The dimensionless parameter $\Pi = \frac{\tau_w(x) x}{\rho K(x)}$ is found to be $\Pi = \frac{F''(0)}{4I}$, where $I = \int_0^\infty (F')^2 d\eta$.

An elegant trick reveals the value of this parameter. By integrating the [self-similar](@entry_id:274241) ODE itself with respect to $\eta$ from $0$ to $\infty$ and applying the boundary conditions, we find a direct relationship: $I = F''(0)$. Substituting this into the expression for $\Pi$ yields a constant value:

$\Pi = \frac{\tau_w(x) x}{\rho K(x)} = \frac{1}{4}$

This result is universal for all such laminar wall jets, regardless of the [fluid viscosity](@entry_id:261198) or jet strength, showcasing the profound predictive power of similarity analysis [@problem_id:512820].

### Corner Flows in Real Fluids: Singularities and Their Resolution

The [ideal flow](@entry_id:261917) solutions for corners predict finite velocities. However, when viscosity is included, the [no-slip condition](@entry_id:275670) on the walls can lead to mathematical singularities in the stress field, particularly at re-entrant corners (corner angle $\alpha > \pi$). The nature of these singularities depends critically on the physical model of the fluid and its environment.

#### Darcy Flow in a Porous Corner

Consider [creeping flow](@entry_id:263844) in a porous medium, governed by the Brinkman equation: $\mu \nabla^2 \mathbf{u} - \nabla p - \frac{\mu}{K} \mathbf{u} = \mathbf{0}$, where $K$ is the medium's permeability. In the **Darcian limit** of very low permeability ($K \to 0$), the viscous term $\mu \nabla^2 \mathbf{u}$ is negligible compared to the porous drag term $\frac{\mu}{K}\mathbf{u}$, and the equation simplifies to Darcy's Law: $\mathbf{u} = -\frac{K}{\mu}\nabla p$.

Substituting this into the incompressibility condition $\nabla \cdot \mathbf{u}=0$ yields the Laplace equation for the pressure, $\nabla^2 p = 0$. The problem of flow in a corner is thus transformed into a potential problem for pressure. The [no-penetration condition](@entry_id:191795) on the walls ($\mathbf{u} \cdot \mathbf{n} = 0$) translates into a Neumann boundary condition on the pressure ($\frac{\partial p}{\partial n}=0$).

For a re-entrant corner with angle $\alpha$, we can find separable solutions for the pressure of the form $p \sim r^s \cos(s\theta)$. Applying the boundary conditions reveals the eigenvalues $s_n = n\pi/\alpha$. The corresponding [stream function](@entry_id:266505) modes are found to be $\psi_n \sim r^{n\pi/\alpha} \sin(\frac{n\pi\theta}{\alpha})$. The flow behavior near the corner tip ($r \to 0$) is dominated by the mode with the smallest positive exponent. This leading-order exponent is therefore:

$\lambda = \frac{\pi}{\alpha}$

This result is markedly different from the exponents found for standard Stokes flow in the same geometry, demonstrating how the physics of the porous medium fundamentally alters the structure of the corner flow [@problem_id:512873].

#### Regularization by Non-Newtonian Rheology

Another way to alter corner singularities is through non-Newtonian fluid behavior. A **Bingham plastic**, for example, is a material that behaves like a rigid solid below a certain **[yield stress](@entry_id:274513)** and flows like a viscous fluid above it. It has been hypothesized that in a re-entrant corner, a small region of yielded fluid near the tip can regularize the [stress singularity](@entry_id:166362) predicted by Newtonian models.

This regularization can be modeled by forcing the stream function to have a regular behavior, specifically $\psi \sim r^\lambda$ with $\lambda=2$. For a slow, [two-dimensional flow](@entry_id:266853), the stream function in the yielded region must still satisfy the [biharmonic equation](@entry_id:165706), $\nabla^4\psi=0$. Substituting $\psi = A r^2 f(\theta)$ into this equation leads to the surprisingly simple ODE: $f'''' + 4f'' = 0$.

For an anti-symmetric flow pattern in a symmetric corner of half-angle $\alpha$, the solution for $f(\theta)$ must be odd, taking the form $f(\theta) = K_2 \sin(2\theta) + K_3 \theta$. Applying the no-slip boundary conditions ($u_r=u_\theta=0$) at the wall $\theta=\alpha$ requires both $f(\alpha)=0$ and $f'(\alpha)=0$. For a non-trivial flow to exist (i.e., for constants $K_2$ and $K_3$ not both to be zero), the determinant of the resulting linear system must vanish. This leads to a remarkable [transcendental equation](@entry_id:276279) for the corner angle itself:

$\tan(2\alpha) = 2\alpha$

This equation implies that such a regularized Bingham flow is only possible for specific discrete corner angles. The smallest positive, non-trivial solution for the full corner angle $2\alpha$ is found numerically to be $2\alpha_0 \approx 4.4934$ radians (about 257.5 degrees). This indicates a deep connection between fluid [rheology](@entry_id:138671), flow [kinematics](@entry_id:173318), and the geometry of the domain [@problem_id:512796].

### Stability and Coherent Structures in Free Jets

Free jets are not static entities; they are susceptible to various instabilities that lead to the formation of complex structures. The study of these instabilities is crucial for understanding jet breakup, mixing, and noise generation.

#### Capillary and Thermocapillary Instabilities

An everyday phenomenon is the breakup of a liquid stream into droplets, driven by the celebrated **Rayleigh-Plateau instability**. Surface tension acts to minimize surface area, causing long-wavelength disturbances on a cylindrical jet to grow. For a highly viscous jet, this instability can be analyzed using a one-dimensional slender jet model.

This instability can be modified by other physical effects, such as a temperature-dependent surface tension, known as the **Marangoni effect** or thermocapillarity. Consider a viscous jet where surface tension decreases with temperature ($\sigma = \sigma_0 - \gamma(T_s - T_{s,0})$) and where a thinning of the jet ($\eta  0$) leads to local cooling ($T_s - T_{s,0} = \beta (R-R_0) = \beta \eta$). Linearizing the 1D momentum and continuity equations for small, long-wavelength axisymmetric perturbations of the form $\eta \sim \exp(\omega t + ikz)$ leads to a [dispersion relation](@entry_id:138513) for the growth rate $\omega$ as a function of the [wavenumber](@entry_id:172452) $k$. The derivation shows that the perturbation pressure contains an extra term due to the [surface tension gradient](@entry_id:156138). The resulting growth rate is:

$\omega(k) = \frac{\sigma_0}{6\mu R_0} \left( 1 + \frac{\gamma\beta R_0}{\sigma_0} - (kR_0)^2 \right)$

Compared to the standard viscous Rayleigh-Plateau instability (where the term in parentheses would be $1-(kR_0)^2$), we see a new term, $\frac{\gamma\beta R_0}{\sigma_0}$, representing the [thermocapillary effect](@entry_id:155513). Since $\gamma$ and $\beta$ are positive, this term enhances the growth rate, demonstrating that Marangoni stresses can be a potent destabilizing mechanism, accelerating the breakup of the jet [@problem_id:512871].

#### Inertial and Rotational Instabilities

Inviscid jets are prone to shear-driven instabilities, such as the Kelvin-Helmholtz instability. The dynamics become richer when additional effects like rotation and density stratification are present. Consider an infinite cylindrical jet with a [solid-body rotation](@entry_id:191086) core, moving through a quiescent ambient fluid of a different density. The stability of this complex vortex to small axisymmetric disturbances is governed by a dispersion relation linking the frequency $\omega$ and [wavenumber](@entry_id:172452) $k$.

In the limit of very short wavelengths ($kR \gg 1$), a neutral stability mode (a non-growing wave) can exist if the densities and flow parameters satisfy a specific condition. For a given relation between the axial flow and rotation, $kW_0 = 2\Omega$, and a disturbance frequency equal to the rotation rate, $\omega = \Omega$, we can investigate the required density ratio $\rho_2/\rho_1$ for such a neutral mode. The Doppler-shifted frequencies in the jet core ($\sigma_1 = \omega - kW_0$) and the surrounding fluid ($\sigma_2 = \omega$) become $\sigma_1 = -\Omega$ and $\sigma_2 = \Omega$. Substituting these into the short-[wave dispersion relation](@entry_id:270310) for this flow leads to a precise condition on the density ratio:

$\frac{\rho_2}{\rho_1} = \sqrt{5}$

This result signifies a delicate balance of inertial, pressure, and centrifugal forces that allows a specific disturbance to propagate without growing or decaying, highlighting the intricate interplay of forces in the stability of structured jets [@problem_id:512822].

#### Cellular Structures in Supersonic Jets

When a [supersonic jet](@entry_id:165155) is imperfectly expanded (i.e., its exit pressure $p_e$ does not match the ambient pressure $p_b$), it develops a quasi-periodic pattern of [shock waves](@entry_id:142404) and expansion fans, often visible as "shock diamonds." We can model the length of the first of these cells for a slightly underexpanded 2D jet ($p_e  p_b$) using linearized gas dynamics.

The process begins with **Prandtl-Meyer expansion fans** originating at the nozzle lips, which turn the flow outward by a small angle $\delta$ to match the lower ambient pressure. This outward-moving flow then over-expands (its pressure drops below $p_b$) and is redirected back toward the axis by a symmetric pair of weak [oblique shock waves](@entry_id:201575). The first shock cell length, $L$, is defined as the distance from the nozzle exit to the point where these two shocks intersect on the centerline.

Using a simplified geometric model where the jet boundary is a straight line for the first half-cell, the maximum half-width is $y_{max} = h + \frac{L}{2}\tan\delta$. This must equal the height reached by the shock propagating from the centerline, $y_{max} = \frac{L}{2}\tan\beta$, where $\beta$ is the shock wave angle. For weak shocks, $\beta$ is approximately the Mach angle, $\mu_e = \arcsin(1/M_e)$. For small angles, this gives $\tan\beta \approx 1/\sqrt{M_e^2-1}$. The initial turning angle $\delta$ can be found from the linearized Prandtl-Meyer relation. Equating the expressions for $y_{max}$ allows us to solve for the cell length $L$:

$L = \frac{2h}{\tan\beta - \delta} = \frac{2h}{\frac{1}{\sqrt{M_e^2 - 1}} - \frac{\sqrt{M_e^2 - 1}}{\gamma M_e^2}\left(\frac{p_e}{p_b} - 1\right)}$

This expression captures the essential physics: the cell length depends on the initial expansion (driven by the [pressure ratio](@entry_id:137698)) and the subsequent re-compression (governed by the Mach number). It provides a quantitative estimate for a key feature of supersonic jets, derived from a tractable analytical model [@problem_id:512885].