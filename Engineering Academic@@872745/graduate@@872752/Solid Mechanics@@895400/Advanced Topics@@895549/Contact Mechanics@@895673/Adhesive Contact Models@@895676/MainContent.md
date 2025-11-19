## Introduction
The forces that cause surfaces to stick together are fundamental to phenomena ranging from the grip of a gecko's foot to the reliability of micro-electromechanical systems (MEMS). While classical [contact mechanics](@entry_id:177379), exemplified by Hertz theory, provides a robust framework for non-adhesive interactions, it fails to capture the ubiquitous effects of adhesion. This omission represents a significant knowledge gap, as attractive [interfacial forces](@entry_id:184024) can dramatically alter contact area, deformation, and the force required for separation. This article bridges that gap by providing a graduate-level exploration of the primary models used to describe adhesive contact between elastic bodies.

This guide is structured to build a comprehensive understanding from first principles to practical application. The first chapter, **Principles and Mechanisms**, establishes the thermodynamic basis of adhesion and derives the two cornerstone theories: the Johnson-Kendall-Roberts (JKR) and Derjaguin-Muller-Toporov (DMT) models. It introduces the critical [dimensionless parameters](@entry_id:180651) that unify these seemingly disparate frameworks. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the power of these models by exploring their use in nanoscale [materials characterization](@entry_id:161346), [tribology](@entry_id:203250), thermal engineering, and [biomechanics](@entry_id:153973). Finally, in **Hands-On Practices**, you will have the opportunity to solidify your understanding by working through problems that apply these theoretical concepts.

## Principles and Mechanisms

This chapter delves into the core principles and mechanical models that describe adhesive contact between elastic bodies. Building upon the non-adhesive Hertzian framework, we will establish the thermodynamic basis for adhesion, explore the two canonical limiting models for adhesive contact—the Johnson-Kendall-Roberts (JKR) and Derjaguin-Muller-Toporov (DMT) theories—and introduce the [dimensionless parameters](@entry_id:180651) that unify these regimes into a single, cohesive picture.

### The Thermodynamic Foundation of Adhesion

At the heart of any adhesive phenomenon is the interplay of surface and interfacial energies. When two bodies are brought into contact, the free surfaces that once existed are replaced by an interface. The net change in the system's energy associated with this process governs the strength of the resulting adhesion.

#### The Work of Adhesion

To formalize this, consider a reversible, [isothermal process](@entry_id:143096) in which two distinct, atomically smooth solids, labeled 1 and 2, are in intimate contact over an area $A$. The system possesses an [interfacial free energy](@entry_id:183036), which is an excess Helmholtz free energy contribution proportional to the contact area, $F_{interface} = \gamma_{12} A$, where $\gamma_{12}$ is the **[interfacial free energy](@entry_id:183036)** per unit area. Now, imagine an external device that quasi-statically separates these two solids, destroying the interface of area $A$ and creating two new free surfaces of area $A$, one for each solid. The free energy of the final state is $F_{surfaces} = \gamma_1 A + \gamma_2 A$, where $\gamma_1$ and $\gamma_2$ are the respective **surface free energies** per unit area.

For an isothermal, reversible process, the minimum external work required, $W_{\text{rev}}$, is equal to the change in the system's Helmholtz free energy, $\Delta F$. The work required per unit area of separation is therefore:

$w = \frac{W_{\text{rev}}}{A} = \frac{\Delta F}{A} = \frac{F_{\text{surfaces}} - F_{interface}}{A} = \gamma_1 + \gamma_2 - \gamma_{12}$

This fundamental quantity, $w$, is known as the **[work of adhesion](@entry_id:181907)** or the Dupré energy of adhesion [@problem_id:2613391]. It represents the reversible [thermodynamic work](@entry_id:137272) per unit area required to separate an interface into two free surfaces. For spontaneous adhesion to occur (i.e., for the formation of an interface to be energetically favorable), the free energy must decrease, which implies that the work of separation, $w$, must be positive ($w > 0$). Its units are energy per area ($\mathrm{J}\cdot\mathrm{m}^{-2}$), which is equivalent to force per length ($\mathrm{N}\cdot\mathrm{m}^{-1}$).

The process of separating the bodies must be idealized as perfectly reversible to equate the measured work with the [thermodynamic work](@entry_id:137272) of adhesion. This means the process must be quasi-static and isothermal, with no energy dissipated through mechanisms like plasticity, viscoelasticity, or defect creation [@problem_id:2613437].

It is crucial to distinguish the [work of adhesion](@entry_id:181907) from related concepts. If the two solids are of the same material (solid 1 in contact with solid 1), the process of separation is one of [cohesion](@entry_id:188479). In this case, $\gamma_1 = \gamma_2$, and the interfacial energy $\gamma_{11}$ for a perfect, seamless interface is zero. The [work of adhesion](@entry_id:181907) becomes the **work of cohesion**, $w_{\text{coh},1}$:

$w_{\text{coh},1} = \gamma_1 + \gamma_1 - \gamma_{11} = 2\gamma_1$

Another important distinction, particularly for solids, is between [surface free energy](@entry_id:159200), $\gamma$, and **[surface stress](@entry_id:191241)** (or surface tension), $\sigma_s$. Surface free energy is the work done to *create* a new unit area of surface (e.g., by cleavage), whereas [surface stress](@entry_id:191241) is the work done to elastically *stretch* an existing unit area of surface. For liquids, these two quantities are identical due to molecular mobility. For solids, they are generally different, as described by the Shuttleworth equation. The [work of adhesion](@entry_id:181907), $w$, is a function of the surface free energies, as it involves the creation of new surfaces [@problem_id:2613391].

Remarkably, all the complex thermodynamics of the interface are captured by this single scalar parameter, $w$. As we will see, both the JKR and DMT models of adhesive contact rely solely on $w$ to characterize the adhesive properties of the interface, rather than the individual values of $\gamma_1$, $\gamma_2$, and $\gamma_{12}$ [@problem_id:2613391].

### From Hertz to Adhesive Contact: Modifying the Foundation

The classical Hertz theory provides an elegant solution for the contact of non-adhesive, frictionless, elastic bodies. It is built on several key assumptions, including [linear elasticity](@entry_id:166983) and a unilateral constraint on the normal traction, $p(\mathbf{x}) \ge 0$, meaning the surfaces can only push against each other, not pull.

The introduction of adhesion fundamentally alters this picture. Attractive forces between the surfaces allow the interface to sustain tensile (negative) tractions. This directly violates the Hertzian unilateral constraint and necessitates a new formulation. However, the Hertzian solution remains an indispensable foundation for adhesive contact models [@problem_id:2613411]. Key elements that are carried over include:

1.  **Linear Elasticity**: Both JKR and DMT models are built upon the theory of linear elasticity to describe the deformation of the bodies. The elastic response is characterized by the same **effective modulus**, $E^*$, used in Hertz theory, where $\frac{1}{E^*} = \frac{1-\nu_1^2}{E_1} + \frac{1-\nu_2^2}{E_2}$.

2.  **Elastic Compliance**: The relationship between applied forces and resulting displacements, which forms the basis of the Hertzian solution, is used to calculate the stored elastic strain energy in the system. This energetic component is crucial for both JKR and DMT models.

3.  **Local Geometry**: The approximation of the contacting bodies' shapes as locally parabolic remains a valid starting point for describing the geometry near the contact zone.

The core task of adhesive contact models, therefore, is to incorporate the [work of adhesion](@entry_id:181907), $w$, into this established elastic framework, replacing the simple unilateral constraint with a more sophisticated condition that allows for tensile tractions.

### Two Limiting Regimes: JKR and DMT Models

Adhesive contact behavior typically falls into one of two limiting regimes, depending on material properties and the nature of the [adhesive forces](@entry_id:265919). The Johnson-Kendall-Roberts (JKR) model is suited for compliant materials with strong, short-range adhesion, while the Derjaguin-Muller-Toporov (DMT) model applies to stiff materials with weaker, long-range adhesion.

#### The DMT Model: Long-Range Forces and Stiff Materials

The DMT model is founded on a simple and physically intuitive hypothesis: the [contact mechanics](@entry_id:177379) *within* the contact area are identical to a non-adhesive Hertzian contact, and the [adhesive forces](@entry_id:265919) act as an additional attractive load applied *outside* the contact area [@problem_id:2613420, @problem_id:2613369].

This separation of effects is possible when materials are stiff and adhesion is long-ranged. The deformation caused by [adhesive forces](@entry_id:265919) is considered negligible compared to the overall contact deformation. The total adhesive force is calculated using the **Derjaguin approximation** (or [proximity force approximation](@entry_id:201747)). This powerful tool relates the force $F(D)$ between two curved surfaces at a minimum separation $D$ to the interaction free energy per unit area, $W(h)$, between two parallel flat plates. For a sphere of radius $R$ near a plane, the approximation yields:

$F(D) \approx 2\pi R W(D)$

This result is derived by integrating the pressure $p(h) = -dW/dh$ over the entire curved geometry, assuming the [radius of curvature](@entry_id:274690) $R$ is much larger than the characteristic range of the interaction forces [@problem_id:2613393]. When the sphere makes contact ($D=0$) and we identify the interaction energy at contact with the [work of adhesion](@entry_id:181907) ($W(0)=-w$), the net adhesive force becomes a constant attractive pull of magnitude $2\pi R w$.

In the DMT model, this adhesive force acts in addition to the externally applied load $P$. The elastic bodies respond to an effective compressive load of $P_{eff} = P + 2\pi R w$. Since the contact response is assumed to be Hertzian, we can substitute this effective load into the Hertzian equations. This leads directly to the governing equations of the DMT model [@problem_id:2613420]:

- **Load-Radius Relation**: $a^3 = \frac{3R}{4E^*}(P + 2\pi R w)$
- **Indentation-Radius Relation**: $\delta = \frac{a^2}{R}$

A key feature of the DMT model is that the pressure distribution inside the contact ($r  a$) is purely compressive and identical to the Hertzian distribution. The adhesive tensile forces are confined to the region outside the contact, where the surfaces are close but not touching. This leads to a singular stress at the edge of the contact, but it is an attractive (tensile) stress of infinite magnitude, which is a non-physical artifact of the model's assumption that forces act only outside the contact zone. The contact area vanishes at a finite tensile [pull-off force](@entry_id:194410) of $P_c = -2\pi R w$. This [pull-off force](@entry_id:194410) is notably independent of the [elastic modulus](@entry_id:198862) $E^*$.

#### The JKR Model: Short-Range Forces and Compliant Materials

In contrast to the DMT model, the Johnson-Kendall-Roberts (JKR) model assumes that [adhesive forces](@entry_id:265919) are short-ranged and act only *within* the area of intimate contact [@problem_id:2613422, @problem_id:2613411]. This approach is better suited for compliant materials where the elastic deformation caused by [adhesive forces](@entry_id:265919) is significant.

The JKR theory is elegantly formulated using an [energy balance](@entry_id:150831) approach inspired by fracture mechanics. The edge of the contact area is treated as the tip of a crack. For the contact area to change, this "crack" must either advance (contact area shrinks) or recede (contact area grows). The condition for equilibrium is that the **[energy release rate](@entry_id:158357)**, $G$, which is the elastic energy released per unit area of crack advance, must be equal to the [work of adhesion](@entry_id:181907), $w$.
$$G=w$$
This is analogous to the Griffith criterion for fracture.

This [energy balance](@entry_id:150831) leads to a different set of governing equations:

- **Load-Radius Relation**: $P = \frac{4E^*a^3}{3R} - \sqrt{8\pi E^* w a^3}$
- **Indentation-Radius Relation**: $\delta = \frac{a^2}{R} - \sqrt{\frac{2\pi w a}{E^*}}$

A striking prediction of the JKR model is the stress distribution. The stress at the center of the contact is compressive, similar to Hertz, but it becomes tensile and theoretically infinite at the contact edge, mimicking the [stress singularity](@entry_id:166362) at a crack tip. This tensile ring at the periphery is what holds the surfaces together.

Upon pull-off, the JKR model predicts a finite contact radius, unlike the DMT model where the radius goes to zero. The [pull-off force](@entry_id:194410) is given by:
$$P_c = -\frac{3}{2}\pi R w$$
This force is 25% smaller than the DMT prediction. This difference arises because in the JKR model, the compliance of the material allows it to store elastic energy. This stored energy aids in the separation process, meaning a smaller external force is required to achieve the critical energy release rate for detachment [@problem_id:2613421].

### Unifying the Regimes: The Tabor and Maugis Parameters

For a long time, the JKR and DMT models were seen as competing descriptions of adhesion. The resolution came with the understanding that they are two asymptotic limits of a more general theory. David Tabor first proposed a dimensionless parameter, now known as the **Tabor parameter** $\mu$, to determine which regime is more appropriate for a given system.

The Tabor parameter compares the elastic deformation at the contact edge due to adhesion with the characteristic range of the [adhesive forces](@entry_id:265919), $z_0$. It is defined as [@problem_id:2613368]:
$$\mu = \left( \frac{R w^2}{E^{*2} z_0^3} \right)^{1/3}$$
where $R$ is the reduced [radius of curvature](@entry_id:274690), $w$ is the [work of adhesion](@entry_id:181907), $E^*$ is the effective modulus, and $z_0$ is the equilibrium separation distance or range of [surface forces](@entry_id:188034) (e.g., the Lennard-Jones equilibrium separation).

The value of $\mu$ serves as a criterion:
- **JKR Regime ($\mu \gg 1$)**: When $\mu$ is large, the elastic deformation is significant compared to the range of [surface forces](@entry_id:188034). This corresponds to compliant systems with strong, short-range adhesion. The JKR model provides an accurate description.
- **DMT Regime ($\mu \ll 1$)**: When $\mu$ is small, the elastic deformation is negligible. This corresponds to [stiff systems](@entry_id:146021) with weak, long-range adhesion. The DMT model is appropriate.
- **Transition Regime ($\mu \approx 1$)**: For intermediate values, neither model is sufficient. The behavior is described by more complex "bridging" models, most notably the Maugis-Dugdale model, which parametrically interpolates between the JKR and DMT limits.

The Tabor parameter thus provides a powerful, unified framework for understanding adhesive contact, allowing researchers to select the correct physical model based on material properties and geometry.