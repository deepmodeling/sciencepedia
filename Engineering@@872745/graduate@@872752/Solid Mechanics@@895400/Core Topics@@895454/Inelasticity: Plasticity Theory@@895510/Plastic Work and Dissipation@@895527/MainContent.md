## Introduction
Plastic deformation is a fundamentally irreversible process, a cornerstone of ductility in engineering materials. While this permanence is observable, the underlying energetic transformations are more subtle. When a material is plastically deformed, the external mechanical work done is not lost; it is converted into dissipated heat and stored in the material's evolving [microstructure](@entry_id:148601). This article addresses the critical question of how to rigorously account for this [energy flow](@entry_id:142770) within the framework of continuum [thermomechanics](@entry_id:180251).

First, in **Principles and Mechanisms**, we will establish the theoretical foundation, starting from the laws of thermodynamics and principles of [work conjugacy](@entry_id:194957) to derive the essential equations for [plastic dissipation](@entry_id:201273) and stored energy. Next, **Applications and Interdisciplinary Connections** will demonstrate the profound impact of these energetic principles, showing how [plastic dissipation](@entry_id:201273) governs everything from the [fracture toughness](@entry_id:157609) of materials and [fatigue life](@entry_id:182388) of structures to the stability of high-strain-rate processes. Finally, **Hands-On Practices** will provide a set of guided problems, allowing you to apply these concepts to analyze material behavior in realistic engineering scenarios and solidify your understanding of this vital topic in solid mechanics.

## Principles and Mechanisms

The irreversible nature of [plastic deformation](@entry_id:139726) is fundamentally a [thermodynamic process](@entry_id:141636). The mechanical work expended to permanently deform a material is not fully recoverable; a significant portion is converted into heat, while a smaller fraction is stored within the material's [microstructure](@entry_id:148601), elevating its internal energy. This chapter elucidates the principles governing this [energy conversion](@entry_id:138574), starting from the foundational laws of continuum [thermomechanics](@entry_id:180251) and culminating in specific expressions for [plastic work](@entry_id:193085) and dissipation used in modern [plasticity theory](@entry_id:177023).

### Mechanical Power and Work Conjugacy

The concept of work requires a force and a corresponding displacement. In a continuum, this is expressed as a stress tensor acting over a corresponding rate of deformation. The **[stress power](@entry_id:182907)** per unit volume, which is the rate at which mechanical work is done by the stresses on the material, is a central quantity. Its form depends on the kinematic framework and the choice of [stress and strain](@entry_id:137374) measures.

A cornerstone principle is that the total internal power, $W_{int}$, is an objective quantity, meaning its value does not depend on the reference frame or the specific configuration (reference or current) used for its calculation. In the current configuration of a body, the stress power density (power per unit current volume) is given by the double contraction of the **Cauchy stress tensor**, $\boldsymbol{\sigma}$, and the **[rate-of-deformation tensor](@entry_id:184787)**, $\mathbf{D}$:

$w_i = \boldsymbol{\sigma} : \mathbf{D}$

where $\mathbf{D}$ is the symmetric part of the velocity gradient, $\mathbf{L} = \nabla \mathbf{v}$.

To express this power in terms of the reference configuration, we use the relationship between current and reference volume elements, $dv = J \, dV_0$, where $J = \det(\mathbf{F})$ is the determinant of the **[deformation gradient](@entry_id:163749)** $\mathbf{F}$. The [power density](@entry_id:194407) per unit reference volume, $w_{i,0}$, is thus $w_{i,0} = J w_i = J (\boldsymbol{\sigma} : \mathbf{D})$. This leads to several equivalent and important pairings of [stress and strain](@entry_id:137374)-rate measures, known as **work-conjugate pairs** [@problem_id:2671338].

By introducing the **Kirchhoff stress**, $\boldsymbol{\tau} = J \boldsymbol{\sigma}$, the power per reference volume becomes:

$w_{i,0} = \boldsymbol{\tau} : \mathbf{D}$

This shows that $(\boldsymbol{\tau}, \mathbf{D})$ is a work-conjugate pair with respect to the reference volume. Through standard kinematic and stress-measure transformations, we can establish other fundamental pairs. It can be shown that the power per reference volume is also given by:

$w_{i,0} = \mathbf{P} : \dot{\mathbf{F}}$

where $\mathbf{P}$ is the **first Piola-Kirchhoff stress tensor** and $\dot{\mathbf{F}}$ is the [material time derivative](@entry_id:190892) of the [deformation gradient](@entry_id:163749). This pairing is particularly useful in formulations where the [deformation gradient](@entry_id:163749) is a primary variable.

Furthermore, using the relation $\mathbf{P} = \mathbf{F} \mathbf{S}$, where $\mathbf{S}$ is the symmetric **second Piola-Kirchhoff stress tensor**, another crucial conjugate pair is revealed:

$w_{i,0} = \mathbf{S} : \dot{\mathbf{E}}$

Here, $\dot{\mathbf{E}}$ is the [material time derivative](@entry_id:190892) of the **Green-Lagrange [strain tensor](@entry_id:193332)**, $\mathbf{E} = \frac{1}{2}(\mathbf{F}^{\mathsf{T}}\mathbf{F} - \mathbf{I})$. The pair $(\mathbf{S}, \mathbf{E})$ is fundamental to many theories of finite-strain elasticity and plasticity due to the symmetry of both tensors and their reference to the undeformed configuration [@problem_id:2671338].

In the specialized, yet widely applicable, context of **small-strain theory**, where deformations and rotations are small, these relationships simplify considerably. The [deformation gradient](@entry_id:163749) approaches the identity tensor, $J \approx 1$, and the [rate-of-deformation tensor](@entry_id:184787) becomes the [material time derivative](@entry_id:190892) of the [small-strain tensor](@entry_id:754968), $\mathbf{D} \approx \dot{\boldsymbol{\varepsilon}}$. Consequently, the Cauchy and Kirchhoff stresses are nearly identical, and the [stress power](@entry_id:182907) per unit volume is simply:

$w_i \approx \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}$

This expression forms the basis for the energetic analysis of most engineering plasticity models.

### Thermodynamic Framework: The Clausius-Duhem Inequality

The laws of thermodynamics impose strict constraints on any [constitutive model](@entry_id:747751). The first law ([energy conservation](@entry_id:146975)) and the second law (entropy production) are combined into a single, powerful statement: the **Clausius-Duhem inequality**. For a general thermomechanical process, the local form of this inequality, which represents the rate of dissipation, can be derived from the local balances of energy and entropy [@problem_id:2671356].

Let $\psi = e - T s$ be the **Helmholtz free energy** per unit mass, where $e$ is the specific internal energy, $T$ is the absolute temperature, and $s$ is the specific entropy. The Clausius-Duhem inequality states that the total dissipation density, $\mathcal{D}$, must be non-negative. This dissipation arises from two sources: intrinsic [mechanical dissipation](@entry_id:169843) and thermal dissipation due to heat flow down a temperature gradient. The full inequality is:

$\mathcal{D} = \boldsymbol{\sigma}:\mathbf{D} - \rho (\dot{\psi} + s \dot{T}) - \frac{1}{T}\mathbf{q} \cdot \nabla T \ge 0$

where $\rho$ is the mass density and $\mathbf{q}$ is the heat [flux vector](@entry_id:273577) [@problem_id:2671356]. The term $\boldsymbol{\sigma}:\mathbf{D}$ is the [stress power](@entry_id:182907), $\rho\dot{\psi}$ is the rate of change of stored free energy, $\rho s \dot{T}$ is the thermal power associated with temperature change, and $-\frac{1}{T}\mathbf{q} \cdot \nabla T$ is the dissipation due to heat conduction (which is non-negative by Fourier's law).

The rate of [entropy production](@entry_id:141771) per unit volume, $\xi$, is directly related to this total dissipation:

$\xi = \frac{\mathcal{D}_{\text{mech}}}{T} - \frac{1}{T^2}\mathbf{q} \cdot \nabla T = \frac{\mathcal{D}_{\text{mech}}}{T} + \mathbf{q} \cdot \nabla\left(\frac{1}{T}\right) \ge 0$

where $\mathcal{D}_{\text{mech}} = \boldsymbol{\sigma}:\mathbf{D} - \rho (\dot{\psi} + s \dot{T})$ is the mechanical part of the dissipation. The heat generated per unit volume due to these irreversible processes is $T\xi$ [@problem_id:2671321].

### Elastoplasticity and the Sources of Dissipation

To understand [plastic dissipation](@entry_id:201273), we consider an elastoplastic material. A fundamental postulate for small-strain plasticity is the **additive decomposition** of the total strain tensor $\boldsymbol{\varepsilon}$ into a recoverable elastic part $\boldsymbol{\varepsilon}^e$ and an irreversible plastic part $\boldsymbol{\varepsilon}^p$ [@problem_id:2671362]:

$\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p$

The state of the material is assumed to be fully described by observable variables like temperature and [elastic strain](@entry_id:189634), and a set of **[internal state variables](@entry_id:750754)**, collectively denoted as $\boldsymbol{\alpha}$, which describe the evolution of the material's internal structure (e.g., dislocation density, back stress). The Helmholtz free energy is thus a function of these state variables, $\psi = \psi(\boldsymbol{\varepsilon}^e, \boldsymbol{\alpha}, T)$.

By substituting the rate form of the strain split, $\dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^e + \dot{\boldsymbol{\varepsilon}}^p$, and the chain rule for $\dot{\psi}$ into the general [dissipation inequality](@entry_id:188634), and applying the **Coleman-Noll argument**, we can systematically derive [constitutive relations](@entry_id:186508). This argument posits that since the inequality must hold for all possible processes, the coefficients of terms that can be varied arbitrarily (like $\dot{\boldsymbol{\varepsilon}}^e$ and $\dot{T}$) must be zero. This procedure yields the standard hyperelastic stress relation and the expression for entropy:

$\boldsymbol{\sigma} = \rho \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^e}$

$s = - \frac{\partial \psi}{\partial T}$

After enforcing these, the [dissipation inequality](@entry_id:188634) is reduced to a form that constrains only the irreversible processes [@problem_id:2671356] [@problem_id:2671375]:

$\mathcal{D}_{\text{mech}} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p - \rho \frac{\partial \psi}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}} \ge 0$

This is the **reduced [dissipation inequality](@entry_id:188634)** for [elastoplasticity](@entry_id:193198). It states that the portion of mechanical work associated with [plastic flow](@entry_id:201346) must be sufficient to account for both the energy dissipated as heat and the energy stored in the changing [microstructure](@entry_id:148601).

### The Partition of Plastic Work: Stored Energy and the Taylor-Quinney Factor

The reduced [dissipation inequality](@entry_id:188634) provides profound insight into the fate of energy during plastic deformation. We define the **[plastic work](@entry_id:193085) rate** per unit volume as the [stress power](@entry_id:182907) associated with the plastic strain rate:

$\dot{W}_p := \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p$

The term $\rho \frac{\partial \psi}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}}$ represents the rate at which free energy is stored in the material's evolving microstructure. This is the **rate of [stored energy of cold work](@entry_id:200373)**, denoted $\dot{W}_{\text{stored}}$ [@problem_id:2671333]. The remainder of the plastic work is converted into heat, $\dot{Q}_{\text{plastic}}$. The reduced [dissipation inequality](@entry_id:188634) is precisely the statement that this heat generation rate must be non-negative:

$\dot{Q}_{\text{plastic}} = \dot{W}_p - \dot{W}_{\text{stored}} \ge 0$

This gives us the fundamental partition of plastic work:

$\dot{W}_p = \dot{W}_{\text{stored}} + \dot{Q}_{\text{plastic}}$

The fraction of [plastic work](@entry_id:193085) converted directly into heat is quantified by the **Taylor-Quinney factor**, $\beta$:

$\beta := \frac{\dot{Q}_{\text{plastic}}}{\dot{W}_p} = 1 - \frac{\dot{W}_{\text{stored}}}{\dot{W}_p}$

For a material that exhibits work hardening, energy must be stored in the [microstructure](@entry_id:148601) ($\dot{W}_{\text{stored}} > 0$), which implies that $\beta  1$. Since dissipation must be non-negative ($\dot{Q}_{\text{plastic}} \ge 0$), we also have $\beta \ge 0$. Thus, for a hardening material, $0 \le \beta  1$. In the idealized case of **[perfect plasticity](@entry_id:753335)** (no hardening), there is no change in the internal state, so $\dot{W}_{\text{stored}} = 0$ and $\beta = 1$. In this case, all plastic work is dissipated as heat [@problem_id:2671333].

For a specific model, such as linear [isotropic hardening](@entry_id:164486) where the yield stress evolves as $\sigma_y = \sigma_{y0} + H\alpha$ and the hardening energy is $\psi_{\text{hard}}(\alpha) = \frac{1}{2}H\alpha^2$, we can derive an explicit expression for $\beta$. In this case, $\dot{W}_{\text{stored}} = (d\psi_{\text{hard}}/d\alpha)\dot{\alpha} = H\alpha\dot{\alpha}$ and $\dot{W}_p = \sigma_y \dot{\alpha} = (\sigma_{y0} + H\alpha)\dot{\alpha}$. The Taylor-Quinney factor becomes [@problem_id:2671333]:

$\beta = 1 - \frac{H\alpha}{\sigma_{y0} + H\alpha}$

This shows that $\beta$ is close to 1 at the onset of yielding ($\alpha=0$) and decreases as the material hardens.

### The Flow Rule and Conditions for Plasticity

The evolution of plastic strain is governed by a set of mathematical rules. Central to this is the concept of a **[yield surface](@entry_id:175331)**, a surface in stress space defined by an equation $f(\boldsymbol{\sigma}, \kappa) = 0$, where $\kappa$ represents the current state of hardening. This surface encloses the domain of purely elastic behavior. The set of all allowable stress states is $\mathcal{E}(\kappa) = \{\boldsymbol{\sigma} | f(\boldsymbol{\sigma}, \kappa) \le 0\}$ [@problem_id:2671346].

Plastic deformation can only occur if the stress state is on the yield surface ($f=0$). This "switching" behavior is formally described by the **Kuhn-Tucker complementarity conditions**:

$\lambda \ge 0, \quad f(\boldsymbol{\sigma}, \kappa) \le 0, \quad \lambda f(\boldsymbol{\sigma}, \kappa) = 0$

Here, $\lambda$ is the **[plastic multiplier](@entry_id:753519)** or consistency parameter. The conditions state that plastic flow is irreversible ($\lambda \ge 0$), the stress state cannot be outside the [yield surface](@entry_id:175331) ($f \le 0$), and [plastic flow](@entry_id:201346) can only happen ($\lambda > 0$) if the stress state is exactly on the [yield surface](@entry_id:175331) ($f=0$).

During a [plastic loading](@entry_id:753518) process, the stress state must remain on the evolving yield surface. This imposes a further constraint known as the **[consistency condition](@entry_id:198045)**:

$\lambda \dot{f}(\boldsymbol{\sigma}, \kappa) = 0$

If $\lambda > 0$, then $\dot{f}$ must be zero, ensuring the stress point "sticks" to the yield surface as it moves [@problem_id:2671346].

The direction of plastic flow is given by a **[flow rule](@entry_id:177163)**, which takes the general form:

$\dot{\boldsymbol{\varepsilon}}^p = \lambda \frac{\partial g}{\partial \boldsymbol{\sigma}}$

where $g(\boldsymbol{\sigma}, \kappa)$ is a **[plastic potential](@entry_id:164680)** function. If the potential is the same as the [yield function](@entry_id:167970) ($g=f$), the flow is termed **associated**. If they differ ($g \neq f$), the flow is **non-associated**.

### Dissipation in Associated J2 Plasticity

For metals, [plastic flow](@entry_id:201346) is often assumed to be volume-preserving, i.e., $\text{tr}(\dot{\boldsymbol{\varepsilon}}^p) = 0$. This implies that the hydrostatic component of stress does no plastic work. The plastic work rate depends only on the **[deviatoric stress tensor](@entry_id:267642)**, $\boldsymbol{s} = \boldsymbol{\sigma} - \frac{1}{3}\text{tr}(\boldsymbol{\sigma})\mathbf{I}$:

$\dot{W}_p = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p = (\boldsymbol{s} + \frac{1}{3}\text{tr}(\boldsymbol{\sigma})\mathbf{I}):\dot{\boldsymbol{\varepsilon}}^p = \boldsymbol{s}:\dot{\boldsymbol{\varepsilon}}^p + \frac{1}{3}\text{tr}(\boldsymbol{\sigma})\text{tr}(\dot{\boldsymbol{\varepsilon}}^p) = \boldsymbol{s}:\dot{\boldsymbol{\varepsilon}}^p$ [@problem_id:2671362]

The most common model for [metal plasticity](@entry_id:176585) is the **von Mises ($J_2$) theory** with an [associated flow rule](@entry_id:201731). The yield function is $f = \sigma_{\text{eq}} - \sigma_y(\kappa)$, where $\sigma_{\text{eq}} = \sqrt{\frac{3}{2}\boldsymbol{s}:\boldsymbol{s}}$ is the von Mises [equivalent stress](@entry_id:749064) and $\sigma_y(\kappa)$ is the current [yield stress](@entry_id:274513).

For this model, the [associated flow rule](@entry_id:201731) dictates that the plastic strain rate is proportional to the [deviatoric stress](@entry_id:163323), $\dot{\boldsymbol{\varepsilon}}^p \propto \boldsymbol{s}$. A remarkable and highly useful result can be derived by combining the [flow rule](@entry_id:177163) with the definitions of [equivalent stress](@entry_id:749064) and equivalent plastic [strain rate](@entry_id:154778) ($\dot{\bar{\varepsilon}}^p = \sqrt{\frac{2}{3}\dot{\boldsymbol{\varepsilon}}^p : \dot{\boldsymbol{\varepsilon}}^p}$). The [plastic work](@entry_id:193085) rate simplifies to the product of these two scalar measures [@problem_id:2671344]:

$\dot{W}_p = \sigma_{\text{eq}} \dot{\bar{\varepsilon}}^p$

This elegant expression connects the macroscopic work rate to the [equivalent stress](@entry_id:749064) and [strain measures](@entry_id:755495) that are ubiquitously used in engineering analysis. For this specific framework, it can also be shown that the [plastic multiplier](@entry_id:753519) $\lambda$ is identical to the equivalent plastic [strain rate](@entry_id:154778) $\dot{\bar{\varepsilon}}^p$. Thus, the plastic work rate during [plastic loading](@entry_id:753518) ($\sigma_{\text{eq}} = \sigma_y$) is simply $\dot{W}_p = \sigma_y \lambda$.

As an example, consider a material obeying the von Mises criterion with a yield stress $\sigma_y = 290 \text{ MPa}$. If the material is subjected to a stress state that lies on the yield surface and the [plastic multiplier](@entry_id:753519) is found to be $\lambda = 4.37 \text{ s}^{-1}$, the plastic power density (assuming [perfect plasticity](@entry_id:753335) where $\dot{W}_p = \dot{Q}_{\text{plastic}}$) is simply [@problem_id:2671319]:

$\mathcal{D}_p = \dot{W}_p = \lambda \sigma_y = (4.37 \text{ s}^{-1})(290 \text{ MPa}) \approx 1267 \text{ MW/m}^3$

### Dissipation in Non-Associated Plasticity

While associated flow is standard for metals, many other materials like soils, rocks, and concrete exhibit **non-associated** behavior, where the [plastic potential](@entry_id:164680) $g$ differs from the [yield function](@entry_id:167970) $f$. This is common in [pressure-sensitive materials](@entry_id:753710) where friction plays a major role.

In this case, the [plastic dissipation](@entry_id:201273) (power) is given by:

$\mathcal{D}_p = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p = \lambda \left(\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}}\right)$

Crucially, the second law's requirement that $\mathcal{D}_p \ge 0$ is no longer automatically satisfied, as it is in associated flow with a [convex yield surface](@entry_id:203690). Thermodynamic admissibility now imposes a strong restriction on the choice of the [plastic potential](@entry_id:164680) $g$: for all stress states on the [yield surface](@entry_id:175331), the condition $\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}} \ge 0$ must hold [@problem_id:2671382].

Failure to satisfy this condition can lead to models that predict negative [plastic dissipation](@entry_id:201273), which is physically impossible and often corresponds to [material instability](@entry_id:172649). For example, consider a pressure-sensitive material modeled with a Drucker-Prager-type [plastic potential](@entry_id:164680) $g = q + \beta p$, where $q$ is the von Mises stress and $p = -\frac{1}{3}\text{tr}(\boldsymbol{\sigma})$ is the [hydrostatic pressure](@entry_id:141627). The plastic power is $\mathcal{D}_p = \lambda (\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}})$. Since $g$ is homogeneous of degree one in stress, Euler's theorem gives $\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}} = g$. Thus, $\mathcal{D}_p = \lambda(q + \beta p)$. For a state of high confinement (large positive pressure $p$), this term is positive. However, under high tensile [mean stress](@entry_id:751819) ($p  0$), it is possible for $\beta|p| > q$, which would result in $\mathcal{D}_p  0$ [@problem_id:2671382]. Such a situation can be linked to the onset of unstable failure modes like cracking. Therefore, the study of [plastic dissipation](@entry_id:201273) provides not only a picture of [energy conversion](@entry_id:138574) but also a fundamental tool for assessing the stability of materials.