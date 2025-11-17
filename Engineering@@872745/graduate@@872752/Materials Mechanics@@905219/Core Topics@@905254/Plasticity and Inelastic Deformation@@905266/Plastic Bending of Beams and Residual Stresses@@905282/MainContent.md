## Introduction
While many engineering designs are based on elastic behavior, the ability of a material to deform plastically provides a crucial reserve of strength and [ductility](@entry_id:160108). Understanding what happens after a beam begins to yield is fundamental to assessing its true failure limits, designing more efficient and robust structures, and predicting its behavior under extreme or [cyclic loading](@entry_id:181502) conditions. This article addresses the knowledge gap between purely elastic analysis and ultimate structural collapse. It answers key questions: How does plasticity spread across a beam's cross-section? What is the true moment-carrying capacity of a beam? What are the consequences of loading a beam into the plastic range and then unloading it?

To explore these questions, we will first delve into the **Principles and Mechanisms** of [plastic bending](@entry_id:197427), establishing the theoretical framework from kinematic assumptions to the formation of residual stresses and the effects of cyclic behavior. Next, in **Applications and Interdisciplinary Connections**, we will see how these principles are applied in [limit analysis](@entry_id:188743), [structural design](@entry_id:196229), and materials science, considering real-world complexities like shear interaction and thermal loading. Finally, you will solidify your understanding through a series of **Hands-On Practices**, applying the theory to solve practical engineering problems. We begin by building the foundation of our analysis: the core principles that govern how a beam deforms when pushed beyond its [elastic limit](@entry_id:186242).

## Principles and Mechanisms

This chapter elucidates the fundamental principles governing the behavior of beams subjected to [bending moments](@entry_id:202968) large enough to induce plastic deformation. We will build a theoretical framework starting from the kinematic assumptions that underpin beam theory, proceeding to the initiation and evolution of plastic zones, and culminating in an analysis of residual stresses and the effects of cyclic loading. Throughout, we will dissect the interplay between geometric constraints, material constitution, and static equilibrium that dictates the response of the structure.

### Kinematic Foundations of Plastic Bending

The analysis of [beam bending](@entry_id:200484), both elastic and plastic, is predicated on a simplifying kinematic assumption that describes how the cross-sections of the beam deform. The most common and foundational of these is the **Bernoulli-Euler hypothesis** (also known as the Kirchhoff-Love hypothesis in the context of plates and shells). This hypothesis posits that [cross-sections](@entry_id:168295) that are initially plane and perpendicular to the beam's longitudinal axis remain plane and perpendicular to the deformed axis after bending.

This geometric constraint has a profound and direct mathematical consequence. Let us consider a beam whose longitudinal axis is aligned with the $x$-axis, with the cross-section lying in the $y$-$z$ plane. If bending occurs about the $z$-axis, causing curvature $\kappa$ in the $x$-$y$ plane, the Bernoulli-Euler assumption dictates that the [axial strain](@entry_id:160811), $\varepsilon_x$, at a distance $y$ from the neutral axis is a linear function of $y$. Specifically, for a beam that is initially straight, the axial displacement field $u_x$ can be described in a way that leads directly to the strain field. For instance, a [displacement field](@entry_id:141476) of the form $u_x(x,y) = -\kappa x y$ for [pure bending](@entry_id:202969), when used with the small-strain definition $\varepsilon_x = \frac{\partial u_x}{\partial x}$, immediately yields:

$$
\varepsilon_x(y) = \frac{\partial}{\partial x}(-\kappa x y) = -\kappa y
$$

This linear strain distribution, $\varepsilon_x(y) = -\kappa y$, is the cornerstone of classical [beam theory](@entry_id:176426). It is crucial to recognize that this relationship is purely kinematic; it arises directly from the geometric assumption about how cross-sections move and is independent of the material's [constitutive law](@entry_id:167255). Therefore, this linear strain profile remains valid whether the material is behaving elastically or has undergone plastic yielding, provided the underlying Bernoulli-Euler hypothesis itself remains a valid approximation of the beam's deformation [@problem_id:2908869].

The validity of the Bernoulli-Euler hypothesis, which is equivalent to assuming zero transverse [shear strain](@entry_id:175241) ($\gamma_{xy}=0$), hinges on several conditions [@problem_id:2908811]:
1.  **Slenderness**: The beam must be slender (i.e., its length must be much greater than its depth). For "deep" beams, deformation due to transverse shear forces becomes significant, causing [cross-sections](@entry_id:168295) to warp and violating the "plane sections" assumption.
2.  **Small Strains**: The entire formulation relies on the premise of small strains. This can be expressed by the dimensionless condition $|\kappa|h \ll 1$, where $h$ is the beam depth. Large strains would necessitate a more complex geometric treatment. The hypothesis is, however, compatible with [large rotations](@entry_id:751151) of the beam axis, provided strains remain small.
3.  **Dominance of Axial Plasticity**: When extending the hypothesis into the plastic regime, its validity requires that [plastic flow](@entry_id:201346) be driven predominantly by the axial stress $\sigma_x$. If significant transverse shear stresses are present, they may induce plastic shear strains, $\gamma_{xy}^p$, which would directly contradict the zero-shear-strain assumption. In most bending-dominated problems involving slender beams, this condition is reasonably met.

### The Onset and Progression of Plasticity

Let us now consider a beam made of an **elastic-perfectly plastic** material, characterized by a Young's modulus $E$ and a [yield stress](@entry_id:274513) $\sigma_y$, which is the same in tension and compression.

As a [bending moment](@entry_id:175948) $M$ is applied, the beam initially deforms elastically. The stress at any fiber is given by Hooke's Law, $\sigma_x(y) = E\varepsilon_x(y)$. Combining this with the linear strain distribution gives a linear stress distribution:

$$
\sigma_x(y) = -E \kappa y
$$

The magnitude of the stress is greatest at the fibers most distant from the neutral axis, known as the extreme fibers (at $y=\pm h/2$ for a rectangular beam of height $h$). Yielding initiates when the stress at these extreme fibers first reaches the [yield stress](@entry_id:274513) $\sigma_y$. This is the **onset of plasticity**. The local yield condition is simply the uniaxial yield criterion, $|\sigma_x(y)| = \sigma_y$ [@problem_id:2908865].

As the applied moment and corresponding curvature are increased beyond this initial [yield point](@entry_id:188474), the stress at the extreme fibers cannot increase further (due to the assumption of [perfect plasticity](@entry_id:753335)). These fibers form thin **plastic zones**. To accommodate the increasing curvature, these plastic zones must grow in thickness, propagating from the outer surfaces inward toward the neutral axis. The central portion of the beam, where the strain is still below the yield strain ($\varepsilon_y = \sigma_y/E$), remains elastic. This region is referred to as the **elastic core**. The cross-section is thus in a partially plastic state, with yielded zones "sandwiching" a shrinking elastic core.

### The Moment-Curvature Relationship

The relationship between the applied [bending moment](@entry_id:175948) $M$ and the resulting curvature $\kappa$ is a defining characteristic of a beam's response. For an elastic-perfectly plastic rectangular section of width $b$ and height $h$, this relationship can be derived by considering three distinct regimes [@problem_id:2908781].

#### Purely Elastic Regime

For small curvatures, the entire cross-section is elastic. The moment is related to the curvature by the familiar formula $M = EI\kappa$, where $I = \frac{bh^3}{12}$ is the [second moment of area](@entry_id:190571). This [linear relationship](@entry_id:267880) holds until yielding begins at the extreme fibers. The moment at which this occurs is the **[yield moment](@entry_id:182231)**, $M_y$.

$$
M_y = \frac{\sigma_y I}{h/2} = \frac{\sigma_y (bh^3/12)}{h/2} = \frac{\sigma_y b h^2}{6}
$$

The curvature at this point is $\kappa_y = M_y / (EI) = \frac{2\sigma_y}{Eh}$.

#### Elastic-Plastic Regime

For curvatures $\kappa > \kappa_y$, the section is partially plastic. Let the elastic-plastic interface be at a distance $y_e$ from the neutral axis. Within the elastic core ($|y| \le y_e$), the stress is linear: $\sigma_x(y) = -E\kappa y$. In the plastic zones ($y_e  |y| \le h/2$), the stress is constant: $\sigma_x(y) = -\text{sign}(y)\sigma_y$. The location of the interface is determined by the condition that strain at $y_e$ is the yield strain: $\kappa y_e = \varepsilon_y = \sigma_y/E$, so $y_e = \frac{\sigma_y}{E\kappa}$.

The total moment is found by integrating this piecewise stress distribution over the cross-section, $M = -\int_A y \sigma_x(y) dA$. This integration yields:

$$
M(\kappa) = \frac{\sigma_{y} b h^{2}}{4} - \frac{b \sigma_{y}^{3}}{3 E^{2} \kappa^{2}} \quad \text{for } \kappa > \kappa_y
$$

This expression shows that as curvature increases, the moment asymptotically approaches a limiting value.

#### Fully Plastic Limit

The theoretical limit of the moment-[carrying capacity](@entry_id:138018) is reached as the curvature approaches infinity ($\kappa \to \infty$). In this limit, the elastic core vanishes ($y_e \to 0$) and the entire cross-section is at the yield stress. The stress distribution is a simple pair of rectangular blocks: $\sigma_x = \sigma_y$ over the tensile half of the section and $\sigma_x = -\sigma_y$ over the compressive half.

The axis separating the tension and compression zones is called the **Plastic Neutral Axis (PNA)**. Its location is determined by the equilibrium condition of zero net axial force on the cross-section: $\int_A \sigma_x dA = 0$. For a fully plastic section with symmetric [yield stress](@entry_id:274513), this simplifies to the geometric condition that the area in compression, $A_C$, must equal the area in tension, $A_T$ [@problem_id:2908852]. For a symmetric rectangular section, the PNA therefore coincides with the geometric centroidal axis.

The moment corresponding to this fully plastic state is the **fully [plastic moment](@entry_id:182387)**, $M_p$. It can be calculated by integrating the fully plastic stress distribution or simply by taking the limit of the elastic-[plastic moment](@entry_id:182387) expression as $\kappa \to \infty$:

$$
M_p = \lim_{\kappa\to\infty} \left( \frac{\sigma_{y} b h^{2}}{4} - \frac{b \sigma_{y}^{3}}{3 E^{2} \kappa^{2}} \right) = \frac{\sigma_{y} b h^{2}}{4}
$$

This represents the ultimate bending moment that the cross-section can sustain under the idealizations of [perfect plasticity](@entry_id:753335) [@problem_id:2908815].

### Quantifying Plastic Capacity: The Shape Factor

We have identified two key moments: the [yield moment](@entry_id:182231) $M_y$, marking the end of the elastic regime, and the [plastic moment](@entry_id:182387) $M_p$, representing the ultimate capacity. The ratio of these two moments is a dimensionless quantity called the **shape factor**, $f$.

$$
f = \frac{M_p}{M_y}
$$

For the rectangular section we have been considering, the shape factor is:

$$
f = \frac{\sigma_y b h^2 / 4}{\sigma_y b h^2 / 6} = \frac{6}{4} = 1.5
$$

The [shape factor](@entry_id:149022) has a clear physical interpretation: it quantifies the reserve moment capacity of a beam's cross-section beyond the [elastic limit](@entry_id:186242) [@problem_id:2908825]. A value of $f=1.5$ means a rectangular beam can withstand a 50% greater [bending moment](@entry_id:175948) than the moment that first caused it to yield. This reserve strength arises from the **redistribution of stress** that occurs as plasticity spreads through the section. In the elastic state, stress is inefficiently concentrated at the extreme fibers. Plasticity allows the under-stressed inner fibers to contribute more to the moment resistance, unlocking the full capacity of the material across the section. The shape factor is a purely geometric property of the cross-section; sections with more material concentrated near the neutral axis (like a solid rectangle or circle) have larger shape factors than sections where material is concentrated far from the neutral axis (like an I-beam).

### Unloading and the Formation of Residual Stresses

When a beam that has been bent into the plastic regime is unloaded, it does not return to its original straight configuration. The "locked-in" [plastic deformation](@entry_id:139726) leads to the formation of a self-equilibrating internal stress field, known as **residual stress**, and a permanent curvature, known as **residual curvature**.

The process of unloading is assumed to be purely elastic. We can conceptualize this by superimposing a fictitious elastic unloading process onto the plastically deformed state. If the beam was loaded to a maximum moment $M_{\text{max}}$ and curvature $\kappa_{\text{max}}$, unloading to $M=0$ is equivalent to applying a moment of $-M_{\text{max}}$. The change in stress during this unloading is calculated elastically:

$$
\Delta\sigma_{\text{unload}}(y) = -\frac{(-M_{\text{max}})y}{I} = \frac{M_{\text{max}}y}{I}
$$

The final [residual stress](@entry_id:138788), $\sigma_r(y)$, is the sum of the stress at peak load, $\sigma_{\text{max}}(y)$, and this elastic change in stress:

$$
\sigma_r(y) = \sigma_{\text{max}}(y) + \Delta\sigma_{\text{unload}}(y)
$$

This resulting stress field is self-equilibrating, meaning it produces zero net force and zero net moment. Characteristically, fibers that were yielded in tension will have compressive residual stress, and fibers that were yielded in compression will have tensile residual stress.

Similarly, the change in curvature during elastic unloading is $\Delta\kappa = -M_{\text{max}}/(EI)$. The final, **residual curvature** is therefore $\kappa_r = \kappa_{\text{max}} + \Delta\kappa = \kappa_{\text{max}} - M_{\text{max}}/(EI)$. This phenomenon, where the beam partially "springs back" upon unloading, is termed **springback**.

A more advanced consideration arises when we scrutinize the "plane sections remain plane" assumption during this elastic unloading phase. If the plastic strain $\varepsilon^p(y)$ locked into the section after loading is a non-linear function of $y$, then forcing the total strain to remain linear during unloading (as the Bernoulli-Euler hypothesis dictates) is a kinematic constraint. It is possible for the beam to find a lower [elastic strain energy](@entry_id:202243) state by allowing the cross-sections to warp slightly. In such cases, the simple Bernoulli-Euler model can actually overpredict the amount of springback (residual curvature) and the magnitude of the residual stresses [@problem_id:2908833]. This highlights that while the classical theory is powerful, it is an idealization whose limitations must be understood in precision applications.

### Beyond Perfect Plasticity: Hardening and Cyclic Behavior

Real materials do not exhibit [perfect plasticity](@entry_id:753335); after yielding, the stress required for further plastic deformation typically increases, a phenomenon known as **[strain hardening](@entry_id:160233)**. Two common idealizations of this behavior are [isotropic and kinematic hardening](@entry_id:195752).

-   **Isotropic Hardening (IH)** models the yield surface in stress space as expanding uniformly, maintaining its center at the origin. This implies that the yield strength increases equally in all directions after [plastic flow](@entry_id:201346).

-   **Kinematic Hardening (KH)** models the [yield surface](@entry_id:175331) as translating in stress space, maintaining its size. This is achieved by introducing a **backstress**, $\alpha$, which tracks the center of the [yield surface](@entry_id:175331). The [yield criterion](@entry_id:193897) becomes $|\sigma - \alpha| \le \sigma_y$.

The crucial difference between these models emerges upon load reversal. Kinematic hardening is designed to capture the **Bauschinger effect**, which is the observed reduction in [yield strength](@entry_id:162154) in the reverse direction of loading after [plastic deformation](@entry_id:139726) has occurred in the forward direction. Isotropic hardening does not capture this effect [@problem_id:2908821].

Consider a beam subjected to a bending cycle. After initial [plastic bending](@entry_id:197427) and unloading, the response to a reversed moment is markedly different for the two material models. Due to the Bauschinger effect, the fibers of a KH beam will yield at a much lower magnitude of reverse moment compared to their initial [yield moment](@entry_id:182231). In contrast, an IH beam, having "hardened," will require an even larger moment than the initial [yield moment](@entry_id:182231) to yield in the reverse direction [@problem_id:2908821]. It is noteworthy, however, that for the *first* loading-unloading cycle from a virgin state, the monotonic stress-strain curve is the same for both models. Consequently, the stress distribution at peak load and the resulting residual stress field after one unloading are identical for both IH and KH models with the same hardening modulus [@problem_id:2908821].

The differences become dramatic under repeated [cyclic loading](@entry_id:181502), such as symmetric curvature-controlled cycling.
-   A beam with **[kinematic hardening](@entry_id:172077)** will exhibit **shakedown** or **cyclic stabilization**. After a few initial cycles, the moment-curvature ($M$-$\kappa$) response settles into a stable, closed hysteresis loop. At the material level, the stress-strain loops of the fibers stabilize, a process involving [mean stress relaxation](@entry_id:197977). The residual stress field at the mean point of the cycle (e.g., $\kappa=0$) also evolves and then stabilizes [@problem_id:2908796].
-   A beam with **[isotropic hardening](@entry_id:164486)** predicts a non-physical response of continuous **cyclic hardening**. With each cycle, the [yield surface](@entry_id:175331) expands, and the peak moment required to achieve the same curvature amplitude increases indefinitely. This model is ill-suited for predicting material behavior under symmetric cyclic loading.

The Bauschinger effect, captured by [kinematic hardening](@entry_id:172077), manifests at the section level as a translated elastic range in the $M$-$\kappa$ loop, signifying earlier onset of plasticity upon load reversal. This realistic modeling is essential for accurately predicting the [fatigue life](@entry_id:182388) and long-term deformation of structures subjected to cyclic loads.