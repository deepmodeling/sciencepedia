## Introduction
Turbulent jets and wakes are among the most fundamental and pervasive phenomena in fluid mechanics, appearing everywhere from the exhaust of a jet engine and the plume of a smokestack to the propulsive water streams of a squid. Despite their seemingly chaotic nature, their behavior is governed by a set of elegant and powerful physical principles. This article addresses the challenge of demystifying these complex flows by breaking them down into their core components. It bridges the gap between abstract theory and practical application, providing a comprehensive framework for understanding how these flows evolve and interact with their surroundings.

Over the next three chapters, you will embark on a structured exploration of turbulent free shear flows. The journey begins with **Principles and Mechanisms**, where we will uncover the foundational laws of conservation, the remarkable concept of [self-similarity](@entry_id:144952), and the crucial role of entrainment in driving flow spreading. We will examine various modeling approaches, from integral methods to the [eddy viscosity](@entry_id:155814) hypothesis, and consider the underlying physics of [turbulent transport](@entry_id:150198). Next, in **Applications and Interdisciplinary Connections**, we will see these principles in action, applying them to solve real-world problems in [aerodynamics](@entry_id:193011), [environmental science](@entry_id:187998), combustion, and even biology. Finally, **Hands-On Practices** will provide a series of targeted problems designed to solidify your understanding and develop your analytical skills in a practical context. Let's begin by delving into the governing invariants that form the bedrock of jet and wake theory.

## Principles and Mechanisms

### Conservation Laws: The Governing Invariants of Free Shear Flows

The intricate, seemingly chaotic motion of turbulent jets and wakes is underpinned by the fundamental conservation laws of mass and momentum. In the far-field, far from the geometric complexities of the flow's origin, the flow dynamics become governed by certain integral quantities that remain constant, or "invariant," in the streamwise direction. These invariants dictate the large-scale evolution of the flow, such as its rate of spreading and the decay of its characteristic velocity.

A **[turbulent wake](@entry_id:202019)** is the [velocity deficit](@entry_id:269642) that persists downstream of a body immersed in a moving fluid. The primary characteristic of a wake is its link to the drag force experienced by the body. By applying [momentum conservation](@entry_id:149964) to a large [control volume](@entry_id:143882) enclosing the body, we can establish a profound and direct relationship between the drag force and the structure of the far-wake. The drag force, $D$, exerted by the fluid on the body is precisely equal to the rate at which momentum is lost from the mean flow. This loss is quantified by the **momentum flux deficit**, $M$, integrated across the wake profile at a downstream station where the pressure has recovered to the ambient value, $p_{\infty}$. For a two-dimensional body in a stream of velocity $U_{\infty}$, this relationship is given by:

$D = M = \int_{-\infty}^{\infty} \rho U(y) (U_{\infty} - U(y)) \, dy$

where $\rho$ is the fluid density, $U(y)$ is the streamwise [velocity profile](@entry_id:266404) in the wake, and $y$ is the transverse coordinate. This equality [@problem_id:490343] is a cornerstone principle, demonstrating that the drag on an object is permanently encoded in the momentum deficit of the wake it leaves behind. The quantity $M$ is conserved in the far-wake, providing a crucial constraint on how the wake may evolve.

In contrast, a **[turbulent jet](@entry_id:271164)** introduces momentum into a quiescent fluid. For a jet issuing from an orifice, the governing invariant is the **kinematic [momentum flux](@entry_id:199796)**, $J$, which is the excess [momentum flux](@entry_id:199796) supplied by the source. Unlike the wake's momentum deficit, the jet's momentum flux is a property of the source itself. For a two-dimensional (or planar) jet, the kinematic momentum flux per unit span is defined by the integral of the square of the velocity across the jet:

$J = \int_{-\infty}^{\infty} U(x,y)^2 \, dy$

This quantity remains constant with downstream distance, $x$, assuming no external forces act on the jet. The conservation of momentum flux serves as a powerful constraint that interrelates the jet's decaying centerline velocity and its increasing width.

### The Emergence of Self-Similarity

One of the most remarkable features of turbulent jets and wakes is their tendency to evolve towards a **self-similar** state. Far downstream from the source, the flow 'forgets' the specific details of its origin—be it a sharp-edged orifice, a smooth nozzle, or a complex bluff body. Instead, the transverse profile of the [mean velocity](@entry_id:150038), when appropriately scaled, collapses onto a single, universal curve.

This behavior is captured by a [similarity solution](@entry_id:152126), where the [velocity profile](@entry_id:266404) $U(x,y)$ is expressed as the product of a characteristic velocity scale $U_c(x)$ (typically the centerline velocity or [velocity deficit](@entry_id:269642)) and a dimensionless shape function $f$ that depends on a scaled transverse coordinate $\eta = y/\delta(x)$:

$U(x,y) = U_c(x) f(\eta)$

Here, $\delta(x)$ is a characteristic width of the [shear layer](@entry_id:274623) that grows with the downstream distance $x$. The conservation of [momentum flux](@entry_id:199796) (or momentum deficit) directly links the decay of the velocity scale $U_c(x)$ to the growth of the length scale $\delta(x)$.

For instance, consider a planar jet whose velocity profile is well-described by the hyperbolic secant squared function, a known exact solution to the boundary-layer equations for this flow. The profile can be written as:

$U(x, y) = U_c(x) \text{sech}^2\left(A \frac{y}{\delta(x)}\right)$

If we define the jet's half-width $\delta(x)$ as the transverse distance where the velocity falls to half its centerline value, i.e., $U(x, \delta) = \frac{1}{2} U_c(x)$, we can determine the constant $A = \text{arccosh}(\sqrt{2}) = \ln(1+\sqrt{2})$. By substituting this profile into the integral for the [conserved momentum](@entry_id:177921) flux $J_0 = \int_{-\infty}^{\infty} \rho U^2 dy$, one can rigorously show that the flux is related to the local scales by $J_0 = K \rho U_c(x)^2 \delta(x)$, where $K = \frac{4}{3A} = \frac{4}{3 \ln(1+\sqrt{2})}$. This calculation [@problem_id:660460] exemplifies how the principle of [momentum conservation](@entry_id:149964) forces a specific algebraic relationship between the jet's width and its centerline velocity.

A simpler, though approximate, profile often used for its mathematical convenience is the Gaussian function. For a self-similar 2D jet described by $U(x,y) = \frac{A}{\sqrt{x}} \exp(-\frac{y^2}{B^2 x^2})$, the conserved kinematic momentum flux $J$ can be calculated by integrating $U^2$ across the profile. The result is a constant value, $J = A^2 B \sqrt{\pi/2}$, which depends only on the parameters defining the jet's strength ($A$) and spreading rate ($B$) [@problem_id:490454].

### Integral Models and the Entrainment Hypothesis

While solving the full governing equations for [self-similar](@entry_id:274241) profiles provides detailed insight, a simpler and often very effective approach is to use integral analysis. This method involves integrating the conservation equations across the [shear layer](@entry_id:274623), working with simplified "top-hat" profiles, which assume a uniform velocity $U(x)$ within a width $b(x)$ and zero velocity outside.

The key physical concept enabling this approach is the **[entrainment hypothesis](@entry_id:191683)**, formulated by Morton, Taylor, and Turner. It postulates that a [turbulent shear flow](@entry_id:267529) grows by engulfing, or **entraining**, ambient fluid from its surroundings. The velocity at which this fluid is drawn into the jet, $v_e$, is assumed to be proportional to the characteristic velocity of the jet itself, $U(x)$. This is expressed as:

$v_e = \alpha U(x)$

where $\alpha$ is a dimensionless empirical constant known as the **entrainment coefficient**. This hypothesis provides a closure for the [mass conservation](@entry_id:204015) equation, linking the growth in mass flux to the local jet velocity.

Let us apply this framework to a turbulent round (axisymmetric) jet. Conservation of axial [momentum flux](@entry_id:199796) $M_0$ for a top-hat profile of radius $b(x)$ and velocity $U(x)$ requires $M_0 = \rho (\pi b^2) U^2 = \text{constant}$, which implies $U b = \text{constant}$, or $U \propto b^{-1}$. The rate of increase of mass flux, $\frac{dQ}{dx}$, must equal the rate of entrainment, $E = \rho (2\pi b) v_e = \rho (2\pi b) (\alpha U)$. By writing the mass flux as $Q = \rho (\pi b^2) U$ and differentiating with respect to $x$, we can equate this to the entrainment rate. Combining the results from mass and [momentum conservation](@entry_id:149964) yields a remarkably simple result for the jet's growth: the radius of the jet grows linearly with downstream distance [@problem_id:490416]. The spreading rate is given by:

$\frac{db}{dx} = 2\alpha$

A similar analysis can be performed for a two-dimensional planar jet. In this case, conservation of momentum flux per unit span gives $M_p = \rho (2b) U_c^2 = \text{constant}$, leading to the scaling $U_c \sqrt{b} = \text{constant}$. Applying the [entrainment hypothesis](@entry_id:191683) to the sides of the planar jet and combining it with the momentum relation again reveals a linear spreading rate [@problem_id:660444]. The half-spreading angle $\theta$, defined by $\tan(\theta) = db/dx$, is found to be:

$\tan(\theta) = \frac{db}{dx} = 2\alpha$

These results highlight the power of the [entrainment hypothesis](@entry_id:191683) in predicting the universal linear spreading of turbulent jets, a key experimental observation. The spreading rate is directly determined by the efficiency of [turbulent entrainment](@entry_id:187545), encapsulated in the constant $\alpha$.

### Mechanisms of Turbulent Spreading

#### Gradient Diffusion and the Eddy Viscosity Concept

To understand the physical mechanism of [entrainment](@entry_id:275487) and spreading on a more fundamental level, we must consider the nature of [turbulent transport](@entry_id:150198). Turbulence enhances the transport of momentum and scalars (like heat or concentration) far beyond the rates of molecular diffusion. In the context of the Reynolds-Averaged Navier-Stokes (RANS) equations, this enhanced transport appears in the form of the **Reynolds stress** tensor, e.g., $-\rho\overline{u'v'}$.

The **[eddy viscosity](@entry_id:155814) hypothesis**, first proposed by Boussinesq, provides a simple model for the Reynolds shear stress by drawing an analogy to [viscous stress](@entry_id:261328) in laminar flow. It assumes that the turbulent stress is proportional to the local mean [velocity gradient](@entry_id:261686):

$-\overline{u'v'} = \nu_t \frac{\partial U}{\partial y}$

where $\nu_t$ is the **turbulent eddy viscosity**. Similarly, the turbulent flux of a scalar quantity like temperature, $-\overline{v'T'}$, can be modeled using a **turbulent [eddy diffusivity](@entry_id:149296)**, $\alpha_t$:

$-\overline{v'T'} = \alpha_t \frac{\partial T}{\partial y}$

The ratio of these two diffusivities is the **turbulent Prandtl number**, $Pr_t = \nu_t / \alpha_t$. This dimensionless number compares the efficiency with which turbulence transports momentum relative to its transport of a scalar. If $Pr_t > 1$, momentum diffuses more effectively than the scalar; if $Pr_t  1$, the scalar spreads more widely.

The turbulent Prandtl number has a direct and observable consequence on the relative widths of velocity and scalar profiles in a shear flow. For example, in the far-wake of a heated cylinder, both the [velocity deficit](@entry_id:269642) and the temperature excess profiles can be approximated by Gaussian functions, but with different characteristic widths, $l_u$ and $l_T$. By substituting these profiles into the respective simplified [transport equations](@entry_id:756133) and requiring that the flow remain [self-similar](@entry_id:274241), one can derive a direct relationship between the profile widths and the turbulent Prandtl number [@problem_id:490430]:

$\frac{l_u}{l_T} = \sqrt{Pr_t}$

For most free shear flows, experiments show that $Pr_t$ is a constant of order unity, typically in the range of 0.5 to 0.9. This implies that the temperature profile in a wake is wider than the [velocity deficit](@entry_id:269642) profile, a result of the different physical mechanisms by which momentum and scalars are transported by [turbulent eddies](@entry_id:266898).

#### Coherent Structures and Vortex Pairing

While the eddy viscosity model provides a useful mathematical framework, it can obscure the underlying physical reality. Turbulent mixing is not a purely diffusive process but is often dominated by the dynamics of large-scale, **[coherent structures](@entry_id:182915)**. A prime example is the planar mixing layer between two streams of different velocities, which is characterized by the formation of large vortices via the Kelvin-Helmholtz instability.

The growth of this layer can be visualized as a hierarchical process of **vortex pairing**. Initially, a row of small vortices forms. Subsequently, adjacent pairs of vortices orbit each other and merge into larger vortices. This pairing event effectively doubles the spacing between vortices and, consequently, doubles the thickness of the mixing layer. By modeling this process as a discrete sequence of pairing events where circulation is conserved, and by postulating a scaling for the time required for a pairing event, one can derive the macroscopic growth rate of the layer from these microscopic dynamics [@problem_id:490360]. This model predicts that the layer thickness, $\delta$, grows linearly with downstream distance, $x$, and that the growth rate is proportional to the velocity difference across the layer, $\Delta U$, and inversely proportional to the mean convection velocity, $U_c$:

$\frac{d\delta}{dx} \propto \frac{\Delta U}{U_c}$

This result, derived from a physical model of [vortex dynamics](@entry_id:145644), correctly captures the experimentally observed linear growth of mixing layers and provides a compelling alternative to the abstract concept of eddy viscosity.

#### A Critical Look at Simple Models

It is crucial for the student of turbulence to recognize that all models are approximations with inherent limitations. The eddy viscosity concept, particularly in its simplest form where $\nu_t$ is assumed constant, can lead to inconsistencies.

This can be demonstrated by a careful analysis of the two-dimensional far-wake. If one assumes a Gaussian [velocity deficit](@entry_id:269642) profile and a constant [eddy viscosity](@entry_id:155814) $\nu_t$, it is possible to derive the required functional form of the wake width $\delta(x)$ from two different conservation principles: the mean [momentum equation](@entry_id:197225) and the integral mean kinetic energy equation. The [momentum equation](@entry_id:197225) yields a relationship for the growth of the wake, $\delta^2(x) = C_M \frac{\nu_T x}{U_1}$. A similar analysis based on the budget of mean kinetic energy also yields a linear growth law, but with a different coefficient: $\delta^2(x) = C_E \frac{\nu_T x}{U_1}$. A rigorous derivation shows that the ratio of these coefficients is $\lambda = C_M / C_E = 3$ [@problem_id:499138].

The fact that these two fundamental conservation laws yield conflicting requirements for the flow's evolution under the constant [eddy viscosity](@entry_id:155814) model proves that the model itself is physically inconsistent for this flow. It highlights that the true eddy viscosity in a self-similar wake cannot be constant across the profile but must have a specific spatial variation. This serves as a cautionary tale about the naive application of simplified [turbulence models](@entry_id:190404).

### Competing Effects: The Buoyant Jet

The principles developed for simple jets and wakes can be synthesized to analyze more complex flows where multiple physical effects compete. A canonical example is the **[buoyant jet](@entry_id:275883)**, or forced plume, which is a flow that possesses both an initial source of kinematic momentum flux, $J_0$, and a source of [buoyancy flux](@entry_id:261821), $F_0$. The [buoyancy flux](@entry_id:261821) represents the rate at which buoyancy is introduced into the system, for example, by releasing a light fluid into a heavier ambient fluid.

Such a flow exhibits two distinct behaviors. In the [near-field](@entry_id:269780), close to the source, the initial momentum dominates. The flow behaves like a pure non-[buoyant jet](@entry_id:275883), with its centerline velocity $u_c$ decaying as $z^{-1}$, where $z$ is the vertical distance. In the [far-field](@entry_id:269288), the cumulative effect of the persistent [buoyancy force](@entry_id:154088) becomes dominant. The flow transitions to behave like a pure plume, with a slower velocity decay, $u_c \propto z^{-1/3}$.

The transition between these two regimes occurs at a characteristic vertical length scale, often called the **jet-to-plume transition length**, $L_{jb}$. This scale can be estimated by finding the height $z$ where the velocity scalings for the two asymptotic regimes become equal. By equating the jet velocity scale, $u_{c, \text{jet}} \propto J_0^{1/2} z^{-1}$, and the plume velocity scale, $u_{c, \text{plume}} \propto F_0^{1/3} z^{-1/3}$, we can solve for this characteristic length [@problem_id:490383]:

$L_{jb} \propto \frac{J_0^{3/4}}{F_0^{1/2}}$

This length scale neatly encapsulates the competition between momentum and [buoyancy](@entry_id:138985). For a given [buoyancy flux](@entry_id:261821) $F_0$, a stronger initial [momentum flux](@entry_id:199796) $J_0$ will delay the transition to a plume, resulting in a larger $L_{jb}$. Conversely, for a given momentum flux, a stronger [buoyancy flux](@entry_id:261821) will cause a more rapid transition. This type of scaling analysis is an indispensable tool for understanding the behavior of complex turbulent flows where multiple physical mechanisms are at play.