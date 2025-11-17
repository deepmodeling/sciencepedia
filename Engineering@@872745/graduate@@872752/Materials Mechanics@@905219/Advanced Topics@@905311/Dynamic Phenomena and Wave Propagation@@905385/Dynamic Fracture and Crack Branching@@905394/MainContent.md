## Introduction
The catastrophic failure of structures often involves cracks that propagate at speeds approaching the speed of sound in the material. Under these extreme conditions, the principles of static fracture mechanics break down, as inertial forces become dominant. This field of **Dynamic Fracture** seeks to explain the complex and often counter-intuitive behaviors of rapidly moving cracks, addressing a critical knowledge gap left by quasi-static approximations. Why is there a physical speed limit for cracks? What causes a single crack to violently split into multiple branches? This article provides a comprehensive exploration of these questions. The first chapter, **Principles and Mechanisms**, will build the theoretical foundation, examining the elastodynamic stress fields and [energy balance](@entry_id:150831) that govern high-speed fracture. Following this, the **Applications and Interdisciplinary Connections** chapter will demonstrate how these concepts are applied to explain material behavior, guide computational simulations, and connect with experimental observations. Finally, the **Hands-On Practices** section offers practical problems to reinforce these advanced concepts. We begin by delving into the fundamental principles that define the behavior of a crack in motion.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms governing the behavior of rapidly propagating cracks. Moving beyond the [quasi-static approximation](@entry_id:167818), we incorporate inertial effects to build a framework for understanding the unique phenomena of dynamic fracture, including the existence of a limiting crack speed and the complex instability of [crack branching](@entry_id:193371). We will begin by examining the stress and energy fields around a moving [crack tip](@entry_id:182807), and from these foundations, we will deduce the conditions that lead to, and govern, crack path instabilities.

### The Elastodynamic Crack Tip Field

In quasi-static fracture mechanics, the stress field near the tip of a crack in a linear elastic material exhibits a characteristic inverse-square-root singularity, with its amplitude governed by the stress intensity factor, $K$. A natural first question in dynamic fracture is how this picture is altered by motion. When a crack propagates at a significant fraction of the material's wave speeds, the material particles surrounding the tip undergo rapid acceleration, and the associated [inertial forces](@entry_id:169104) can no longer be neglected.

The governing equations of linear [elastodynamics](@entry_id:175818) show that, for a crack propagating at any sub-Rayleigh speed, the fundamental $r^{-1/2}$ singularity in the [near-tip stress field](@entry_id:191574) is preserved. This is a remarkable and powerful result, as it allows for the extension of the [stress intensity factor](@entry_id:157604) concept to the dynamic regime. We thus define a **dynamic [stress intensity factor](@entry_id:157604)**, which may be time-dependent, $K(t)$, as the amplitude of this singular field. For a Mode I crack moving with an instantaneous speed $v(t)$, the near-tip stress tensor $\sigma_{ij}$ can be written as:

$$
\sigma_{ij}(r,\theta,t) \sim \frac{K_I(t)}{\sqrt{2\pi r}}\,\Phi^{(I)}_{ij}\!\left(\theta;\frac{v(t)}{c_L},\frac{v(t)}{c_S}\right) + \text{less singular terms}
$$

Here, $(r,\theta)$ are polar coordinates centered on the moving [crack tip](@entry_id:182807), $c_L$ and $c_S$ are the material's longitudinal and shear wave speeds, respectively. The crucial difference from the static case lies in the dimensionless angular functions, $\Phi^{(I)}_{ij}$. In dynamic fracture, these functions depend not only on the angle $\theta$ but also on the instantaneous crack speed $v(t)$ [@problem_id:2879600]. Inertia distorts the stress field, breaking the simple symmetry observed in the static case.

This framework extends naturally to in-plane shear (Mode II) and anti-plane shear (Mode III) loading. The dynamic [stress intensity factors](@entry_id:183032) $K_{II}(t)$ and $K_{III}(t)$ are defined analogously as the amplitudes of the $r^{-1/2}$ singularity in their respective stress fields. For example, $K_{II}(t)$ is conventionally defined from the shear stress directly ahead of the crack tip:

$$
K_{II}(t) = \lim_{r\to 0} \sqrt{2\pi r}\,\sigma_{r\theta}(r,0,t)
$$

The corresponding near-tip stress fields for each mode are then described by their own set of velocity-dependent angular functions, $f_{ij}^{(II)}(\theta;v)$ and $f_{ij}^{(III)}(\theta;v)$ [@problem_id:2879570].

While the singular term dominates the physics of [energy flow](@entry_id:142770) into the crack tip, less singular terms in the [asymptotic expansion](@entry_id:149302) also play a critical role, particularly in determining the stability of the crack's path. The first non-singular (or $r^0$) term in this expansion is a constant stress that acts parallel to the crack flanks, known as the **T-stress**. This term, while bounded, modifies the [angular distribution](@entry_id:193827) of the [hoop stress](@entry_id:190931) around the crack tip and, as we will see, serves as a key parameter in predicting the onset of kinking and branching [@problem_id:2626627].

### Energy Balance in Dynamic Fracture

The propagation of a crack is fundamentally an [energy conversion](@entry_id:138574) process: the [elastic potential energy](@entry_id:164278) stored in the body is released and converted into the energy required to create new surfaces. The Griffith criterion for static fracture, $G = \Gamma_c$, represents this balance. For a moving crack, this principle is generalized to account for both kinetic energy and potential rate-dependence in the material's [fracture resistance](@entry_id:197108).

We define the **[dynamic energy release rate](@entry_id:202588)**, $G(v)$, as the rate of energy flow into the [crack tip](@entry_id:182807) per unit of crack advance at speed $v$. The material's resistance to fracture, or its fracture energy, may also depend on the crack speed, denoted as $\Gamma(v)$. The generalized energy balance condition for steady propagation at speed $v$ is therefore:

$$
G(v) = \Gamma(v)
$$

This equation forms the dynamic Griffith criterion for fracture [@problem_id:2626646]. A central and perhaps counter-intuitive principle of dynamic fracture is that the [energy release rate](@entry_id:158357) $G(v)$, for a given level of remote loading, is a monotonically decreasing function of crack speed $v$. As the crack moves faster, it becomes an increasingly efficient source of [elastic waves](@entry_id:196203) that radiate energy away from the crack tip into the bulk of the material. This radiated energy is unavailable to drive the fracture process itself. Consequently, a smaller fraction of the globally available energy actually reaches the crack tip [@problem_id:2879603].

The relationship between the dynamic and static energy release rates can be expressed as $G(v) = A(v) G_0$, where $G_0$ is the static energy release rate for the same crack length and loading, and $A(v)$ is a universal, dimensionless function of speed that captures the effects of inertia. For Mode I, $A_I(v)$ is a strictly decreasing function with $A_I(0) = 1$ and, as we will explore next, $A_I(v) \to 0$ as the crack speed approaches the Rayleigh [wave speed](@entry_id:186208), $c_R$.

### The Limiting Speed of a Crack

The fact that $G(v)$ decreases with increasing speed has a profound consequence: it implies the existence of a maximum attainable crack speed. For a Mode I crack in a homogeneous, isotropic elastic solid, this limiting speed is the **Rayleigh surface wave speed**, $c_R$.

The reason for this limit is intimately connected to the physics of [surface waves](@entry_id:755682). The Rayleigh [wave speed](@entry_id:186208) is defined as the speed at which a stress wave can propagate along a traction-free surface. The faces of a crack are, by definition, traction-free surfaces. As the crack speed $v$ approaches $c_R$, the elastodynamic solution for the near-tip field becomes degenerate. The mathematical structure of the field becomes such that its ability to transport energy to the crack tip vanishes. In essence, as $v \to c_R$, the energy supplied from the far field is almost entirely radiated away, starving the crack tip of the energy needed for bond breaking [@problem_id:2632582].

This physical reasoning is captured by the fact that the universal function $g_I(v)$ in the relation $G(v) \propto g_I(v) K_I^2(v)$ goes to zero as $v \to c_R^{-}$. To satisfy the propagation condition $G(v) = \Gamma > 0$ at or very near $c_R$, the dynamic [stress intensity factor](@entry_id:157604) $K_I(v)$ would have to become unboundedly large. Since finite remote loading can only produce a finite [stress intensity factor](@entry_id:157604), this means that a crack cannot, within the confines of [linear elastic fracture mechanics](@entry_id:172400), attain the Rayleigh wave speed. It is an asymptotic upper bound that cannot be reached [@problem_id:2632582].

### The Onset of Instability: Crack Branching

The existence of a limiting speed presents an "energy paradox." Consider a large brittle structure under high load, where the available static [energy release rate](@entry_id:158357) $G_0$ is far greater than the material's [fracture toughness](@entry_id:157609) $\Gamma_c$. A crack will accelerate, but it cannot exceed $c_R$. In fact, experiments show that long before a crack approaches $c_R$, a new phenomenon occurs: **dynamic [crack branching](@entry_id:193371)**.

This instability provides a mechanism for the system to dissipate energy at a much higher rate. When the energy supplied from the remote elastic field far exceeds what a single, fast-moving [crack tip](@entry_id:182807) can absorb and convert into surface energy, the system may find it energetically favorable to create additional energy sinks. By splitting into two or more "daughter" cracks, the total area of new surface created per unit time increases dramatically, providing a more efficient pathway for the release of the stored [elastic potential energy](@entry_id:164278) [@problem_id:2824794].

This leads to an energetic criterion for the onset of macro-branching. For a single crack to bifurcate into two symmetric branches, the [energy release rate](@entry_id:158357) available at the parent [crack tip](@entry_id:182807), $G(v_b)$, must be sufficient to power the creation of two new cracks. This is often expressed as an instability condition:

$$
G(v_b) \gtrsim 2 \Gamma(v_b)
$$

where $v_b$ is the branching speed. This is a condition for instability, not steady propagation. It signifies that at speed $v_b$, there is twice as much energy flowing to the tip as is needed to sustain a single crack's growth.

Combining this with our simplified models, we can determine the required level of [far-field](@entry_id:269288) loading for branching to occur. For instance, using a simple linear model for the dynamic reduction factor, $\varphi(v) = 1 - v/c_R$, and a constant fracture toughness $G_c$, the steady-state condition is $(1 - v_0/c_R)G_0 = G_c$. If branching is known to occur at a critical speed $v_0 = \alpha c_R$, we can solve for the necessary far-field drive $G_0$. This yields $G_0 = G_c / (1 - \alpha)$. This shows that the remote loading $G_0$ must exceed the fracture toughness $G_c$ by a critical multiple $\Lambda_c = 1/(1-\alpha)$ to drive the crack fast enough to trigger the branching instability [@problem_id:2793782]. Extensive experiments on various brittle materials confirm that this instability typically occurs when the crack speed reaches approximately $0.4c_R$ to $0.5c_R$ [@problem_id:2824794]. Furthermore, if the material's [fracture energy](@entry_id:174458) itself increases with speed ($\Gamma'(v) > 0$), this acts as a stabilizing factor, raising the energetic cost of fracture and thus delaying the onset of branching to higher speeds or requiring a larger driving force [@problem_id:2626646].

### Path Selection in Dynamic Fracture

Once the energetic conditions for branching are met, a crucial question remains: in which direction do the new cracks propagate? The selection of the branching angle is a complex problem involving a competition between local stress states and global energy considerations.

In the quasi-[static limit](@entry_id:262480) ($v \to 0$), a pure Mode I crack will always propagate straight ahead, as this is the path of both maximum hoop stress and maximum [energy release rate](@entry_id:158357) [@problem_id:2626639]. At high speeds, however, this is no longer the case. The distortion of the [near-tip stress field](@entry_id:191574) can make the straight path unstable. The **T-stress**, the non-singular stress acting parallel to the crack, plays a key role here. A compressive (negative) T-stress is known to be a powerful destabilizing agent. It modifies the angular distribution of the [hoop stress](@entry_id:190931), shifting its maximum away from the $\theta=0$ direction and thereby promoting kinking or branching at an angle [@problem_id:2626627].

Two classical criteria have been proposed to predict the branching angle:

1.  **Yoffe's Maximum Hoop Stress Criterion:** This is a purely local criterion. It postulates that branching occurs in the direction where the circumferential (hoop) stress, $\sigma_{\theta\theta}$, of the *unbranched* moving crack is maximum. As crack speed increases, the location of this maximum moves to significant off-axis angles. For a crack moving at $v \approx 0.6c_R$, this criterion predicts very large branching angles, often in the range of $60^\circ-70^\circ$.

2.  **Maximum Energy Release Rate (MERR) Criterion:** This is a global [energy criterion](@entry_id:748980). It postulates that the system will select the branching angle $\theta$ that maximizes the total [energy release rate](@entry_id:158357) into the newly formed pair of daughter cracks. This calculation, which considers the energetics of the final bifurcated state, consistently predicts much smaller, more realistic branching angles, typically in the range of $20^\circ-40^\circ$ for similar speeds.

The discrepancy arises because the Yoffe criterion is local and "unaware" of the final branched state, whereas the MERR criterion explicitly optimizes the energy partitioning for that state. The smaller angles predicted by MERR are in much better agreement with experimental observations, suggesting that global energy considerations are dominant in path selection during branching [@problem_id:2626639]. The inclusion of a negative T-stress in the local analysis can reduce the angle predicted by the Yoffe criterion, bringing it into closer alignment with MERR and experiments [@problem_id:2626639].

### Micro- versus Macro-Branching: The Role of Three-Dimensionality

Finally, it is important to recognize that "branching" is not a single phenomenon. We must distinguish between two primary morphologies:
*   **Macro-branching:** The in-plane splitting of a crack into two or more long, running daughter cracks, as discussed above.
*   **Micro-branching:** The formation of a dense network of short, out-of-plane side branches that do not propagate far but significantly increase the roughness of the fracture surface.

The transition between these two regimes is governed by a competition between an [internal material length scale](@entry_id:197915) and an external geometric length scale. The key internal scale is the size of the **process zone**, $\ell_{\mathrm{pz}}$, at the crack tip, where dissipative processes occur. A standard estimate for this length is $\ell_{\mathrm{pz}}(v) \sim E' \Gamma(v) / \sigma_c^2$, where $E'$ is the [elastic modulus](@entry_id:198862) and $\sigma_c$ is a characteristic [cohesive strength](@entry_id:194858). The key external scale is the plate thickness, $B$.

The transition is governed by the ratio of these two lengths:
*   In **thick plates**, where $B \gg \ell_{\mathrm{pz}}(v)$, the [crack tip](@entry_id:182807) is in a state of effective [plane strain](@entry_id:167046). The unconstrained third dimension allows for the development of out-of-plane instabilities, favoring micro-branching.
*   In **thin plates**, where $B \ll \ell_{\mathrm{pz}}(v)$, the proximity of the free surfaces suppresses out-of-plane excursions and enforces a state of [plane stress](@entry_id:172193). This frustrates micro-branching. If the energetic and velocity conditions for in-plane splitting are met ($G(v) \gtrsim 2\Gamma(v)$ and $v \ge v_b^{2D}$), the system will instead opt for macro-branching.

Therefore, the transition from a micro-branching regime to a macro-branching regime is favored by decreasing the plate thickness $B$ relative to the velocity-dependent [material length scale](@entry_id:197771) $\ell_{\mathrm{pz}}(v)$ [@problem_id:2879590]. This highlights the crucial role of three-dimensional effects and material-structure interaction in determining the ultimate morphology of dynamic fracture.