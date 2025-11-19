## Introduction
In high-[performance engineering](@entry_id:270797), pushing the limits of materials is a constant challenge. Components like gun barrels, fuel injectors, and chemical reactors must withstand extreme internal pressures, often cyclically, making them susceptible to failure by [plastic deformation](@entry_id:139726), fracture, or fatigue. While simply using stronger materials or thicker walls is an option, it often comes with prohibitive weight, cost, or manufacturing constraints. This creates a critical need for methods that can enhance component performance without changing its basic material or dimensions. A powerful solution lies in strategically engineering the material's internal state through the introduction of residual stresses.

This article provides a comprehensive exploration of **Residual Stresses and Autofrettage**, a powerful technique for prestressing high-pressure vessels to dramatically improve their performance and service life. By delving into the mechanics of this process, readers will gain a deep understanding of how to turn internal stresses from a potential liability into a significant design asset.

The journey begins in the **Principles and Mechanisms** chapter, where we will establish a rigorous definition of [residual stress](@entry_id:138788), explore its origins using the concept of eigenstrain, and conduct a detailed elastoplastic analysis of the autofrettage process in a [thick-walled cylinder](@entry_id:189222). Next, the **Applications and Interdisciplinary Connections** chapter will bridge theory and practice, demonstrating how autofrettage enhances [fracture resistance](@entry_id:197108) and [fatigue life](@entry_id:182388), and exploring its connections to materials science, experimental measurement techniques, and engineering design codes. Finally, the **Hands-On Practices** chapter will solidify your understanding through guided problems that apply these core concepts to practical design scenarios. This structured approach will equip you with the theoretical foundation and practical insight needed to analyze and leverage autofrettage in advanced [mechanical design](@entry_id:187253).

## Principles and Mechanisms

This chapter delineates the fundamental principles governing the formation of residual stresses and the mechanisms through which they can be engineered for structural benefit. We will first establish a rigorous mechanical definition of residual stress, explore its origins through the concept of eigenstrain, and then apply these principles to the detailed analysis of autofrettage in thick-walled cylinders—the canonical example of engineered [residual stress](@entry_id:138788) for performance enhancement.

### The Nature of Residual Stress

In continuum mechanics, a stress field is typically associated with the action of external forces, such as applied [surface tractions](@entry_id:169207) or [body forces](@entry_id:174230). However, it is possible for a body to exist in a state of stress even after all external loads and supports have been removed. Such stresses, which are locked into the material by its thermomechanical history, are known as **residual stresses**.

Formally, a residual stress field $\boldsymbol{\sigma}(\mathbf{x})$ is a stress field that persists in a body in the absence of externally applied actions. For this stress field to exist in a state of static equilibrium, it must be **self-equilibrated**. This imposes strict mathematical conditions. In the absence of [body forces](@entry_id:174230), the stress field must satisfy the local [balance of linear momentum](@entry_id:193575) within the body's domain $\Omega$:

$$
\nabla \cdot \boldsymbol{\sigma} = \mathbf{0} \quad \text{in } \Omega
$$

Furthermore, the [balance of angular momentum](@entry_id:181848) requires that the stress tensor be symmetric, $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$. On any portion of the boundary $\partial\Omega$ that is free from external tractions, the Cauchy traction vector must vanish. If $\mathbf{n}$ is the outward unit normal to the boundary, this condition is expressed as:

$$
\boldsymbol{\sigma} \mathbf{n} = \mathbf{0} \quad \text{on free surfaces}
$$

These local conditions have important global consequences. By the divergence theorem, the requirement that $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$ implies that the net force exerted by the internal stresses across any arbitrary closed surface within the body is zero. Similarly, the net moment of these internal tractions must also vanish. These integral statements formalize the notion that a residual stress field is "self-balancing," containing regions of tension that are equilibrated by regions of compression, without producing any [net force](@entry_id:163825) or moment on the body as a whole [@problem_id:2680719]. It is crucial to recognize that no general restrictions apply to the nature of [residual stress](@entry_id:138788); it can be multiaxial and vary spatially in complex ways, comprising both hydrostatic and deviatoric components.

### The Concept of Eigenstrain as a Source of Stress

The existence of a non-zero stress field in the absence of external loads may seem counterintuitive. The physical origin of such stresses lies in local, non-elastic deformations that are incompatible with each other. In solid mechanics, this concept is formalized through the idea of **[eigenstrain](@entry_id:198120)**, denoted by $\boldsymbol{\varepsilon}^*$. Eigenstrain (also known as transformation strain or stress-free strain) represents any local deformation that a material element would undergo if it were free from its surroundings. Common physical sources of [eigenstrain](@entry_id:198120) include:

*   **Plastic Strain**: Permanent deformation resulting from loading beyond the [elastic limit](@entry_id:186242).
*   **Thermal Strain**: Expansion or contraction due to temperature changes, given by $\boldsymbol{\varepsilon}^* = \alpha \Delta T \mathbf{I}$, where $\alpha$ is the [coefficient of thermal expansion](@entry_id:143640).
*   **Phase Transformation Strain**: Volumetric and/or shape changes associated with a change in the material's crystal structure.

To understand how eigenstrain generates stress, we decompose the total strain $\boldsymbol{\varepsilon}$ into an elastic part $\boldsymbol{\varepsilon}^e$ and the [eigenstrain](@entry_id:198120) $\boldsymbol{\varepsilon}^*$:

$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^*
$$

According to Hooke's Law, stress is generated only by the elastic part of the strain: $\boldsymbol{\sigma} = \mathbf{C} : \boldsymbol{\varepsilon}^e$, where $\mathbf{C}$ is the [fourth-order elasticity tensor](@entry_id:188318). Therefore, we can write the stress as:

$$
\boldsymbol{\sigma} = \mathbf{C} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^*)
$$

The total strain field $\boldsymbol{\varepsilon}$ must be **kinematically compatible**, meaning it can be derived from a continuous, single-valued [displacement field](@entry_id:141476) $\mathbf{u}$ as $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^{\mathsf{T}})$. The crucial insight is that stress arises if the eigenstrain field $\boldsymbol{\varepsilon}^*$ is itself **incompatible**, or if a compatible [eigenstrain](@entry_id:198120) field is constrained from deforming freely.

*   If an eigenstrain field is **compatible** (i.e., it could be produced by a single-valued displacement field) and the body is unconstrained, the body can deform such that the total strain equals the eigenstrain ($\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^*$). In this case, the [elastic strain](@entry_id:189634) is zero ($\boldsymbol{\varepsilon}^e = \mathbf{0}$), and no stress develops. For example, a uniform thermal expansion in a free, homogeneous body produces no stress [@problem_id:2680759].
*   If a compatible eigenstrain is **constrained**, stress will develop. For instance, if a bar undergoing a uniform thermal [eigenstrain](@entry_id:198120) $\varepsilon^* = \alpha \Delta T$ is fixed at both ends, its total strain must be zero ($\varepsilon = 0$). This forces an elastic strain $\varepsilon^e = -\varepsilon^*$, resulting in a compressive stress $\sigma = -E \alpha \Delta T$ upon heating [@problem_id:2680759].
*   If an [eigenstrain](@entry_id:198120) field is **incompatible**, it is impossible for the body to deform to accommodate it without generating elastic strains. A non-[uniform distribution](@entry_id:261734) of plastic strain, such as that induced during autofrettage, is a prime example of an incompatible [eigenstrain](@entry_id:198120) field that inherently generates a residual stress field upon removal of the external load [@problem_id:2680759].

### Elastoplastic Analysis of a Thick-Walled Cylinder: Autofrettage

Autofrettage (literally "self-hooping") is an engineering process used to introduce beneficial compressive residual stresses at the inner surface of a high-pressure vessel, such as a gun barrel or fuel injector. This is achieved by pressurizing the cylinder to a level that causes [plastic deformation](@entry_id:139726) to initiate at the bore and propagate part-way through the cylinder wall. Upon release of this pressure, a self-equilibrated residual stress field remains.

#### Elastic Response and Onset of Yield

Consider a long, [thick-walled cylinder](@entry_id:189222) with inner radius $a$ and outer radius $b$. Under an [internal pressure](@entry_id:153696) $p$, the elastic stress distribution is given by the well-known Lamé equations. For a closed-end cylinder, where a uniform axial stress $\sigma_z$ balances the pressure on the end caps, the [principal stresses](@entry_id:176761) are [@problem_id:2680737]:

$$
\sigma_r(r) = \frac{p a^2}{b^2 - a^2} \left( 1 - \frac{b^2}{r^2} \right)
$$
$$
\sigma_\theta(r) = \frac{p a^2}{b^2 - a^2} \left( 1 + \frac{b^2}{r^2} \right)
$$
$$
\sigma_z = \frac{p a^2}{b^2 - a^2}
$$

Plastic yielding will initiate where the [effective stress](@entry_id:198048) first reaches the material's [yield strength](@entry_id:162154), $\sigma_Y$. The von Mises [equivalent stress](@entry_id:749064), $\sigma_v = \sqrt{\frac{1}{2}[(\sigma_r-\sigma_\theta)^2 + (\sigma_\theta-\sigma_z)^2 + (\sigma_z-\sigma_r)^2]}$, is largest at the inner radius $r=a$. For the closed-end case, the von Mises stress at the bore simplifies significantly. The pressure $p_y$ at which yielding first occurs is found by setting $\sigma_v(a) = \sigma_Y$, which yields [@problem_id:2680737]:

$$
p_y = \frac{\sigma_Y}{\sqrt{3}} \left(1 - \frac{a^2}{b^2}\right)
$$

For an open-ended cylinder where $\sigma_z=0$, the Tresca [yield criterion](@entry_id:193897) ($\sigma_\theta - \sigma_r = \sigma_Y$) is often used and also predicts yielding at the bore. The corresponding initiation pressure is $p_y = \frac{\sigma_Y}{2} \left(1 - \frac{a^2}{b^2}\right)$ [@problem_id:2633870].

#### Stresses During Plastic Loading (Autofrettage)

When the [internal pressure](@entry_id:153696) $p$ exceeds $p_y$, a plastic zone develops, spanning from the inner radius $a$ to an elastic-plastic interface radius, $r_p$. The region $r_p \le r \le b$ remains elastic. To determine the stress state, we must solve the equilibrium and yield equations in both zones and enforce continuity at the interface.

In the **plastic zone** ($a \le r \le r_p$), the stresses must satisfy both the [equilibrium equation](@entry_id:749057) $\frac{d\sigma_r}{dr} + \frac{\sigma_r - \sigma_\theta}{r} = 0$ and the [yield criterion](@entry_id:193897).
*   For a **Tresca material** (assuming $\sigma_\theta - \sigma_r = \sigma_Y$), substituting the yield condition into the [equilibrium equation](@entry_id:749057) gives $\frac{d\sigma_r}{dr} = \frac{\sigma_Y}{r}$.
*   For a **von Mises material** under plane strain, [plasticity theory](@entry_id:177023) shows that $\sigma_z = \frac{1}{2}(\sigma_r + \sigma_\theta)$, and the yield condition reduces to $\sigma_\theta - \sigma_r = \frac{2}{\sqrt{3}}\sigma_Y$. Substituting this into the [equilibrium equation](@entry_id:749057) gives $\frac{d\sigma_r}{dr} = \frac{2\sigma_Y}{\sqrt{3}r}$ [@problem_id:2680756].

In both cases, we obtain a simple differential equation for $\sigma_r(r)$ in the [plastic zone](@entry_id:191354), which can be integrated. For the von Mises [plane strain](@entry_id:167046) case, integrating from the bore gives:

$$
\sigma_r(r) = \frac{2\sigma_Y}{\sqrt{3}} \ln\left(\frac{r}{a}\right) - p
$$
$$
\sigma_\theta(r) = \sigma_r(r) + \frac{2\sigma_Y}{\sqrt{3}} = \frac{2\sigma_Y}{\sqrt{3}} \left(1 + \ln\left(\frac{r}{a}\right)\right) - p
$$

In the **elastic zone** ($r_p \le r \le b$), the stresses follow the Lamé form. The constants are found by applying the boundary condition $\sigma_r(b)=0$ and enforcing that the stresses at the interface $r=r_p$ satisfy the yield criterion. Matching the [radial stress](@entry_id:197086) from the elastic solution at $r=r_p$ with the value from the plastic solution allows for the determination of the relationship between the applied pressure $p$ and the plastic radius $r_p$. For the Tresca criterion (open-end cylinder), this relationship is [@problem_id:2680723]:

$$
p(r_p) = \sigma_Y \left(\ln\left(\frac{r_p}{a}\right) + \frac{1}{2} \left(1 - \frac{r_p^2}{b^2}\right)\right)
$$
This equation shows that a greater [internal pressure](@entry_id:153696) is required to drive the plastic zone deeper into the cylinder wall.

#### Unloading and the Principle of Superposition

The creation of [residual stress](@entry_id:138788) occurs upon unloading. If the unloading process is purely elastic (an assumption we will revisit), we can use the **[principle of superposition](@entry_id:148082)**. The final residual stress state ($\boldsymbol{\sigma}^{\text{res}}$) is the sum of the elastoplastic stress state at the peak autofrettage pressure $p_a$ ($\boldsymbol{\sigma}^{\text{EP}}$) and the purely elastic stress change associated with removing that pressure. This stress change is simply the negative of the Lamé solution for a pressure $p_a$, which we denote as $\boldsymbol{\sigma}^{\text{unload}}$.

$$
\boldsymbol{\sigma}^{\text{res}}(r) = \boldsymbol{\sigma}^{\text{EP}}(r) - \boldsymbol{\sigma}^{\text{unload}}(r)
$$

Let's calculate the residual hoop stress at the bore, $\sigma_\theta^{\text{res}}(a)$, which is of primary interest. At the peak pressure $p_a$, the bore is plastic, and for a Tresca material, $\sigma_\theta^{\text{EP}}(a) = \sigma_r^{\text{EP}}(a) + \sigma_Y = -p_a + \sigma_Y$. The unloading [hoop stress](@entry_id:190931) at the bore is $\sigma_\theta^{\text{unload}}(a) = p_a \frac{b^2+a^2}{b^2-a^2}$. The residual [hoop stress](@entry_id:190931) at the bore is therefore [@problem_id:2680688]:

$$
\sigma_\theta^{\text{res}}(a) = (\sigma_Y - p_a) - p_a \frac{b^2+a^2}{b^2-a^2} = \sigma_Y - p_a \frac{2b^2}{b^2-a^2}
$$

Since $p_a$ must be large enough to cause plastic flow, this residual hoop stress is compressive. This compressive stress at the bore is balanced by tensile residual hoop stresses in the outer, formerly elastic region, ensuring the field is self-equilibrated. A key check is that the residual [radial stress](@entry_id:197086) is zero at the free inner and outer surfaces, as required: $\sigma_r^{\text{res}}(a) = \sigma_r^{\text{EP}}(a) - \sigma_r^{\text{unload}}(a) = (-p_a) - (-p_a) = 0$, and similarly $\sigma_r^{\text{res}}(b) = 0 - 0 = 0$ [@problem_id:2680688].

### Mechanical Consequences and Design Principles

#### Enhancement of Load-Carrying Capacity

The primary benefit of autofrettage is the significant increase in the pressure-carrying capacity of the cylinder. When the autofrettaged cylinder is re-pressurized, the applied tensile hoop stress at the bore is counteracted by the pre-existing compressive residual [hoop stress](@entry_id:190931). Yielding will not re-initiate until the total [hoop stress](@entry_id:190931) reaches the material's yield strength.

For an elastic-perfectly plastic material with no Bauschinger effect, re-loading is purely elastic. The total stress state is the sum of the residual field and the new elastic field from re-pressurization. Re-yield occurs at the bore when the re-applied pressure is equal to the original autofrettage pressure, $p_{\text{ry}} = p_a$. Since $p_a$ is, by definition, greater than the initial [elastic limit](@entry_id:186242) pressure $p_{\text{EL}}$, the operational pressure range of the vessel is extended. For a cylinder with $b=2a$ pressurized until the [plastic zone](@entry_id:191354) reaches $c=1.6a$, the re-yield pressure is over 70% higher than the initial [elastic limit](@entry_id:186242) pressure ($p_{\text{ry}} / p_{\text{EL}} \approx 1.733$) [@problem_id:2633870].

#### Limitations: Reverse Yielding

The assumption of purely elastic unloading is not always valid. If the autofrettage pressure $p_a$ is too high, the compressive stress that develops during unloading can be large enough to cause yielding in compression at the bore. This is known as **reverse yielding**.

To find the limit, we examine the residual stress state. Reverse yielding at the bore occurs if the [effective stress](@entry_id:198048) of the residual field reaches the [yield strength](@entry_id:162154). For a Tresca material, this happens when the magnitude of the compressive residual hoop stress at the bore equals the yield strength, i.e., $-\sigma_\theta^{\text{res}}(a) = \sigma_Y$. Using the expression for $\sigma_\theta^{\text{res}}(a)$ derived previously, this condition can be solved for the limiting pressure $p_a$. The maximum pressure that can be applied without causing reverse yielding upon unloading is [@problem_id:2680698]:

$$
p_{a, \max} = \sigma_Y \left(1 - \frac{a^2}{b^2}\right)
$$

This pressure is exactly twice the initial yield pressure $p_y$ for an open-ended cylinder. Pressurizing beyond this limit offers [diminishing returns](@entry_id:175447) and can be detrimental to the fatigue life of the component.

#### The Role of Material Hardening

The analysis so far has assumed an elastic-perfectly plastic material model ($H=0$). Real materials exhibit strain hardening, which alters the autofrettage response.

**Isotropic Hardening:** In this model, the [yield surface](@entry_id:175331) expands uniformly as plastic strain accumulates. A material with [isotropic hardening](@entry_id:164486) ($H>0$) becomes stronger as it deforms plastically. Consequently, for the same peak pressure $p_{\max}$, a hardening material will experience less plastic deformation: the plastic zone radius $c$ will be smaller, and the accumulated plastic strains will be lower compared to a perfectly plastic material. Since residual stresses are a direct result of these inelastic strains, the magnitude of the [residual stress](@entry_id:138788) field will be smaller. The residual hoop stress at the bore will be less compressive, and the balancing tensile stresses in the outer region will be lower. The crossover point where the residual hoop stress changes sign will move closer to the bore [@problem_id:2702715].

**Kinematic Hardening and the Bauschinger Effect:** A more realistic model for many metals is [kinematic hardening](@entry_id:172077), which accounts for the **Bauschinger effect**: a reduction in yield strength in the reverse direction of loading after initial plastic deformation. In this model, the yield surface translates in [stress space](@entry_id:199156) in the direction of plastic flow, but does not change size.

During autofrettage, the tensile plastic flow in the hoop direction at the bore shifts the [yield surface](@entry_id:175331), increasing the tensile yield strength but *decreasing* the compressive yield strength. This makes the material more susceptible to reverse yielding upon unloading or when subjected to external pressure. If an autofrettaged cylinder is subsequently subjected to external pressure, the [kinematic hardening](@entry_id:172077) model predicts that re-yielding in compression will occur at a significantly lower pressure than would be predicted by an [isotropic hardening](@entry_id:164486) model. This is because the compressive yield limit has been lowered by the Bauschinger effect, a critical consideration in the design of components that may experience load reversals [@problem_id:2633864].