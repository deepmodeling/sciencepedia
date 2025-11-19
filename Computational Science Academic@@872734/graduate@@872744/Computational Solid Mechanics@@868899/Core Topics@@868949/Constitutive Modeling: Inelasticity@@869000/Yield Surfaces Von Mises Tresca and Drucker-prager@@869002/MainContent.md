## Introduction
The transition from [elastic deformation](@entry_id:161971) to permanent [plastic flow](@entry_id:201346), known as yielding, is a critical phenomenon in [solid mechanics](@entry_id:164042) that dictates the limits of a material's structural integrity. Predicting the complex stress state at which yielding begins is essential for the safe and efficient design of everything from aerospace components to geological foundations. Yield surfaces are the elegant mathematical constructs that define this threshold, forming a boundary in [stress space](@entry_id:199156) that separates elastic from plastic behavior.

However, different materials yield in fundamentally different ways. The [plastic flow](@entry_id:201346) of a ductile metal is driven by shear and is largely unaffected by hydrostatic pressure, while the failure of soil or rock is strongly dependent on it. This article addresses this crucial distinction by exploring three cornerstone [yield criteria](@entry_id:178101) that form the basis of modern [plasticity theory](@entry_id:177023).

Across three chapters, you will gain a deep understanding of these models. The first chapter, "Principles and Mechanisms," deconstructs the von Mises, Tresca, and Drucker-Prager criteria, grounding them in the fundamental concept of [stress decomposition](@entry_id:272862). The second chapter, "Applications and Interdisciplinary Connections," demonstrates how these theoretical models are applied in engineering design, [geomechanics](@entry_id:175967), and advanced computational mechanics. Finally, "Hands-On Practices" offers a bridge from theory to practice with challenging exercises focused on [model calibration](@entry_id:146456) and numerical implementation.

## Principles and Mechanisms

The onset of [plastic deformation](@entry_id:139726) in a material marks a fundamental transition from reversible elastic behavior to irreversible flow. Predicting the stress state at which this transition, known as yielding, occurs is a cornerstone of solid mechanics. The criteria that define this threshold are represented by **yield surfaces** in stress space. For [isotropic materials](@entry_id:170678), these criteria can be formulated in terms of [stress invariants](@entry_id:170526), which are independent of the chosen coordinate system. This chapter explores the principles and mechanisms underpinning three of the most foundational [yield criteria](@entry_id:178101): the von Mises, Tresca, and Drucker-Prager models. We will see that the key to understanding their structure and differences lies in the decomposition of stress and the material's sensitivity to hydrostatic pressure.

### The Volumetric-Deviatoric Decomposition of Stress

A general state of stress at a point, described by the second-order Cauchy stress tensor $\boldsymbol{\sigma}$, can be uniquely decomposed into two distinct components: a **hydrostatic** part and a **deviatoric** part. This decomposition is not merely a mathematical convenience; it separates the stress components responsible for volume change from those responsible for shape change (distortion).

The hydrostatic component is represented by the [mean stress](@entry_id:751819), which is the average of the [normal stresses](@entry_id:260622) on any three mutually perpendicular planes. It is proportional to the first invariant of the stress tensor, $I_1 = \operatorname{tr}(\boldsymbol{\sigma})$. The **hydrostatic pressure**, $p$, is conventionally defined as the negative of the mean stress (with tension being positive):
$$
p = -\frac{1}{3} I_1 = -\frac{1}{3}(\sigma_{11} + \sigma_{22} + \sigma_{33})
$$
With this definition, pressure is positive in compression. The part of the stress tensor corresponding to this mean stress is the spherical or [hydrostatic stress](@entry_id:186327) tensor, $-p\boldsymbol{I}$, where $\boldsymbol{I}$ is the second-order identity tensor. Applying a purely hydrostatic stress state, $\boldsymbol{\sigma} = -p\boldsymbol{I}$, tends to cause a uniform change in the volume of a material element without altering its shape.

The remaining part of the stress tensor is the **[deviatoric stress tensor](@entry_id:267642)**, $\boldsymbol{s}$, defined as:
$$
\boldsymbol{s} = \boldsymbol{\sigma} + p\boldsymbol{I} = \boldsymbol{\sigma} - \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})\boldsymbol{I}
$$
By its construction, the [deviatoric stress tensor](@entry_id:267642) is traceless, i.e., $\operatorname{tr}(\boldsymbol{s})=0$. This tensor represents a state of pure shear and is responsible for the distortion or change in shape of a material element at constant volume. The complete stress state is thus given by the sum $\boldsymbol{\sigma} = \boldsymbol{s} - p\boldsymbol{I}$.

The intensity of the deviatoric stress is quantified by its second invariant, $J_2$, defined as:
$$
J_2 = \frac{1}{2} \boldsymbol{s}:\boldsymbol{s} = \frac{1}{2} s_{ij}s_{ij}
$$
where the [double dot product](@entry_id:748648) denotes the double contraction of the tensors. This scalar quantity is a measure of the magnitude of the shear stresses in the material. For instance, in a state of pure hydrostatic stress, the [deviatoric stress tensor](@entry_id:267642) is the zero tensor ($\boldsymbol{s}=\mathbf{0}$), and consequently, $J_2 = 0$. This implies that a purely [hydrostatic stress](@entry_id:186327) state induces no distortion [@problem_id:3610539].

The fundamental distinction between different classes of [yield criteria](@entry_id:178101) hinges on whether yielding is influenced by the hydrostatic component of stress ($p$ or $I_1$) or is driven solely by the deviatoric component ($\boldsymbol{s}$ or $J_2$) [@problem_id:3610469].

### Pressure-Insensitive Yield Criteria for Ductile Metals

A vast body of experimental evidence shows that for most ductile metals under moderate pressure, the onset of yielding is almost entirely independent of the applied hydrostatic stress. Yielding in these materials is a shear-driven phenomenon. Consequently, the [yield criteria](@entry_id:178101) designed for them are formulated to be independent of $I_1$ and depend only on the deviatoric stress, most commonly through the invariant $J_2$.

#### The von Mises Criterion: A Model of Distortional Energy

The von Mises [yield criterion](@entry_id:193897), also known as $J_2$-plasticity, is one of the most widely used models for ductile metals. It postulates that yielding begins when the second invariant of the [deviatoric stress](@entry_id:163323), $J_2$, reaches a critical value. The yield function, $f$, which defines the boundary of the elastic region, is conventionally written as:
$$
f(\boldsymbol{\sigma}) = \sqrt{3J_2} - \sigma_y = 0
$$
Here, $\sigma_y$ is the material's yield strength as measured in a simple [uniaxial tension test](@entry_id:195375). The term $\sigma_e = \sqrt{3J_2}$ is known as the **von Mises [equivalent stress](@entry_id:749064)**.

The constant $\sqrt{3}$ is a calibration factor that ensures consistency with the [uniaxial tension test](@entry_id:195375). In such a test, at the point of yield, the stress tensor has only one non-zero component, $\sigma_{11} = \sigma_y$. A step-by-step calculation reveals that for this stress state, $J_2 = \frac{1}{3}\sigma_y^2$. Substituting this into the yield condition $f=0$ gives $\sqrt{3(\frac{1}{3}\sigma_y^2)} - \sigma_y = \sigma_y - \sigma_y = 0$, confirming the formulation [@problem_id:3610525].

The pressure-insensitivity of the von Mises criterion is inherent in its definition. Since the function depends only on $J_2$, and $J_2$ is an invariant of the [deviatoric stress tensor](@entry_id:267642) $\boldsymbol{s}$, we need only show that $\boldsymbol{s}$ is unaffected by hydrostatic pressure. If we superimpose a hydrostatic stress $p_0\boldsymbol{I}$ onto an existing stress state $\boldsymbol{\sigma}$, the new stress state is $\boldsymbol{\sigma}' = \boldsymbol{\sigma} + p_0\boldsymbol{I}$. The new [deviatoric stress tensor](@entry_id:267642), $\boldsymbol{s}'$, is found to be identical to the original, $\boldsymbol{s}' = \boldsymbol{s}$. Therefore, $J_2$ remains unchanged, and the von Mises [yield criterion](@entry_id:193897) is completely independent of [hydrostatic pressure](@entry_id:141627) [@problem_id:3610525].

The von Mises criterion admits several profound physical interpretations [@problem_id:3610498]:
1.  **Distortional Strain Energy**: In linear elasticity, the [strain energy density](@entry_id:200085) stored in a material can be split into a volumetric part and a distortional part, $U_d$. The distortional [strain energy density](@entry_id:200085) is given by $U_d = \frac{J_2}{2G}$, where $G$ is the [shear modulus](@entry_id:167228). The von Mises criterion is thus equivalent to the postulate that yielding occurs when the distortional [strain energy](@entry_id:162699) per unit volume reaches a critical value, $U_{d,y} = \frac{\sigma_y^2}{6G}$.
2.  **Octahedral Shear Stress**: The shear stress acting on a specific set of planes, known as octahedral planes, which are equally inclined to the principal stress axes, can be shown to be directly related to $J_2$. The magnitude of this stress, the **[octahedral shear stress](@entry_id:200691)** $\tau_{\text{oct}}$, is given by $\tau_{\text{oct}} = \sqrt{\frac{2}{3}J_2}$. The von Mises criterion can therefore be restated as yielding occurring when the [octahedral shear stress](@entry_id:200691) reaches a critical value, $\tau_{\text{oct},y} = \frac{\sqrt{2}}{3}\sigma_y$.

#### The Tresca Criterion: A Model of Maximum Shear Stress

An alternative criterion, proposed by Henri Tresca, is based on a more direct physical intuition: yielding occurs when the maximum shear stress anywhere in the material, $\tau_{\text{max}}$, reaches a critical value. This critical value is the material's yield strength in pure shear, denoted by $k$.

The maximum shear stress in a 3D stress state is given by half the difference between the largest and smallest [principal stresses](@entry_id:176761) ($\sigma_1 \ge \sigma_2 \ge \sigma_3$):
$$
\tau_{\text{max}} = \frac{\sigma_1 - \sigma_3}{2}
$$
The Tresca [yield function](@entry_id:167970) is thus formulated as $f(\boldsymbol{\sigma}) = \tau_{\text{max}} - k = 0$. Like the von Mises criterion, the Tresca criterion is independent of hydrostatic pressure, as it depends only on the *differences* between principal stresses. Adding a hydrostatic component shifts all [principal stresses](@entry_id:176761) by the same amount, leaving their differences, and thus $\tau_{\text{max}}$, unchanged [@problem_id:3610533].

To relate the shear [yield strength](@entry_id:162154) $k$ to the uniaxial tensile yield strength $\sigma_y$, we again consider the [uniaxial tension test](@entry_id:195375). At yield, the [principal stresses](@entry_id:176761) are $(\sigma_y, 0, 0)$. The maximum shear stress is $\tau_{\text{max}} = \frac{\sigma_y - 0}{2} = \frac{\sigma_y}{2}$. Since at yield $\tau_{\text{max}} = k$, we find the important relation $k = \frac{\sigma_y}{2}$. The Tresca criterion can therefore be written in terms of $\sigma_y$ as:
$$
2\tau_{\text{max}} = \max(|\sigma_1-\sigma_2|, |\sigma_2-\sigma_3|, |\sigma_3-\sigma_1|) = \sigma_y
$$

### Pressure-Sensitive Yield Criteria for Frictional Materials

In contrast to ductile metals, many other materials, such as soils, rocks, concrete, and polymers, exhibit a yield behavior that is strongly dependent on hydrostatic pressure. For these **frictional materials**, compressive [hydrostatic stress](@entry_id:186327) increases their resistance to shear failure. Their [yield criteria](@entry_id:178101) must therefore incorporate a dependence on both a deviatoric measure like $J_2$ and a hydrostatic measure like $I_1$.

#### The Drucker-Prager Criterion: A Conical Generalization

The Drucker-Prager criterion is a simple and widely used model for [pressure-sensitive materials](@entry_id:753710). It can be viewed as a modification of the von Mises criterion that includes a linear dependence on the hydrostatic stress. A common form of the [yield function](@entry_id:167970) is written in terms of [stress invariants](@entry_id:170526):
$$
f(\boldsymbol{\sigma}) = \sqrt{J_2} + \alpha I_1 - k = 0
$$
Here, $\alpha$ and $k$ are material constants [@problem_id:3610517]. To better understand its physical meaning, this can be expressed using the pressure $p = -I_1/3$ (positive in compression) and the von Mises [equivalent stress](@entry_id:749064) $q = \sqrt{3J_2}$. Substituting $I_1 = -3p$ and $\sqrt{J_2} = q/\sqrt{3}$ into the yield condition gives a linear relationship in the $p-q$ plane (the meridional plane):
$$
q = (3\sqrt{3}\alpha)p + \sqrt{3}k
$$
*   The parameter $k$ is related to the material's **[cohesion](@entry_id:188479)**. Cohesion is the [shear strength](@entry_id:754762) at zero confining pressure ($p=0$), which from the equation is $q_{\text{cohesion}} = \sqrt{3}k$.
*   The parameter $\alpha$ is the **pressure-sensitivity** coefficient, often related to the internal friction of the material. The linear equation shows that the shear strength $q$ required to cause yielding increases linearly with the confining pressure $p$.

The von Mises criterion is a special case of the Drucker-Prager criterion where the pressure sensitivity is zero ($\alpha=0$), reducing the equation to $\sqrt{J_2} = k$, where $k$ would be identified with $\sigma_y/\sqrt{3}$. Because of its pressure dependence, the Drucker-Prager model can predict failure under purely hydrostatic loading, unlike the von Mises and Tresca models. For example, a version of the model can be formulated to include a "tensile cutoff," predicting failure under sufficient hydrostatic tension, a mode of failure relevant for brittle materials [@problem_id:3610539].

### Geometric Interpretation of Yield Surfaces

Each yield criterion $f(\boldsymbol{\sigma})=0$ defines a surface in the six-dimensional space of symmetric stress tensors. For intuition, these surfaces are visualized in the three-dimensional [principal stress space](@entry_id:184388) $(\sigma_1, \sigma_2, \sigma_3)$. The concepts of pressure-independence and Lode angle dependence give these surfaces distinct and characteristic shapes.

A particularly illuminating framework for this visualization is the **Haigh-Westergaard coordinate system** [@problem_id:3610474]. This is a [cylindrical coordinate system](@entry_id:266798) in [principal stress space](@entry_id:184388) where the axial coordinate, $\xi$, is aligned with the hydrostatic axis ($\sigma_1=\sigma_2=\sigma_3$).
*   The axial coordinate $\xi = I_1 / \sqrt{3}$ measures the hydrostatic component of stress.
*   The [radial coordinate](@entry_id:165186) $\rho = \sqrt{2J_2}$ measures the magnitude of the [deviatoric stress](@entry_id:163323).
*   The angular coordinate $\theta$, the **Lode angle**, describes the type of deviatoric stress state (e.g., distinguishing between triaxial tension and triaxial compression).

In this space, the geometry of the yield surfaces becomes clear:
*   **von Mises**: The condition $\sqrt{3J_2}=\sigma_y$ is equivalent to $\rho = \sqrt{2/3}\sigma_y$, which is a constant. This is the equation of a **right circular cylinder** coaxial with the hydrostatic ($\xi$) axis. Its independence from both $\xi$ and $\theta$ reflects that it is insensitive to both pressure and the Lode parameter.
*   **Tresca**: The Tresca criterion is independent of hydrostatic pressure, so its surface is also a cylinder parallel to the $\xi$-axis. However, its dependence on the maximum difference between [principal stresses](@entry_id:176761) makes it dependent on the Lode angle $\theta$. Its cross-section in the deviatoric ($\rho$-$\theta$) plane is a **regular hexagon**. The full surface is a hexagonal prism.
*   **Drucker-Prager**: Being pressure-sensitive, the surface is not a cylinder. The linear relation between $q$ and $p$ translates to a linear relation between $\rho$ and $\xi$. Since the simplest form of the criterion is independent of the Lode angle $\theta$, revolving this straight line about the $\xi$-axis generates a **right circular cone**.

A 2D visualization in **[plane stress](@entry_id:172193)** (where one [principal stress](@entry_id:204375), say $\sigma_3$, is zero) is also highly instructive [@problem_id:3610538]. In the $(\sigma_1, \sigma_2)$-plane:
*   The von Mises yield surface is an **ellipse** described by $\sigma_1^2 - \sigma_1\sigma_2 + \sigma_2^2 = \sigma_y^2$.
*   The Tresca yield surface is a **hexagon**.
The von Mises ellipse circumscribes the Tresca hexagon, touching it at points corresponding to pure shear states. This shows that for most multiaxial stress states, the Tresca criterion is more conservative, predicting yield at a lower [equivalent stress](@entry_id:749064) than the von Mises criterion.

### Mechanisms of Plastic Flow: The Flow Rule

The [yield surface](@entry_id:175331) defines the *onset* of plasticity. The *evolution* of plastic strain is dictated by a **[flow rule](@entry_id:177163)**, which specifies the direction of the plastic strain increment tensor, $d\boldsymbol{\epsilon}^p$.

#### The Associated Flow Rule and Normality

A widely adopted hypothesis, grounded in thermodynamic principles of stable materials, is the **[associated flow rule](@entry_id:201731)**. It states that the direction of the plastic strain increment is normal to the yield surface at the current stress state. Mathematically, this is expressed as:
$$
d\boldsymbol{\epsilon}^p = d\lambda \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$
where $f$ is the [yield function](@entry_id:167970) and $d\lambda \ge 0$ is a scalar known as the [plastic multiplier](@entry_id:753519), which determines the magnitude of the plastic strain increment. This geometric property is known as the **[normality rule](@entry_id:182635)** [@problem_id:3610491].

The physical consequences of this rule are profound and depend on the geometry of the [yield surface](@entry_id:175331):
*   For the **von Mises** criterion, the gradient $\partial f / \partial \boldsymbol{\sigma}$ is proportional to the [deviatoric stress tensor](@entry_id:267642) $\boldsymbol{s}$. Since $\operatorname{tr}(\boldsymbol{s})=0$, it follows that $\operatorname{tr}(d\boldsymbol{\epsilon}^p)=0$. This means that associated von Mises plasticity predicts that [plastic flow](@entry_id:201346) is **isochoric**, or volume-preserving. This is an excellent approximation for the plastic deformation of metals.
*   For the **Drucker-Prager** criterion, using the form $f = \sqrt{J_2} + \alpha I_1 - k$, the gradient $\partial f / \partial \boldsymbol{\sigma} = \boldsymbol{s}/(2\sqrt{J_2}) + \alpha\boldsymbol{I}$ has both a deviatoric component and a hydrostatic component. The trace of the plastic strain increment is $\operatorname{tr}(d\boldsymbol{\epsilon}^p) = d\lambda (3\alpha)$. Since $\alpha>0$ for frictional materials, the model predicts a positive volumetric plastic strain during yielding, a phenomenon known as **[plastic dilatancy](@entry_id:188905)**. This volume increase is characteristic of the shearing of [granular materials](@entry_id:750005) like sand.

#### Non-Associated Flow and Complexities

In some cases, the [associated flow rule](@entry_id:201731) can predict behavior that deviates from experimental observation (e.g., predicting excessive dilatancy in soils). To provide more modeling flexibility, a **[non-associated flow rule](@entry_id:172454)** can be introduced:
$$
d\boldsymbol{\epsilon}^p = d\lambda \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$
Here, $g(\boldsymbol{\sigma})$ is a **[plastic potential](@entry_id:164680)** function that is different from the yield function $f(\boldsymbol{\sigma})$. In this case, the plastic flow is normal to the [level surfaces](@entry_id:196027) of the potential $g$, not the [yield surface](@entry_id:175331) $f$ [@problem_id:3610491]. While offering more flexibility, non-associated models can lead to mathematical complexities and potential material instabilities under certain conditions [@problem_id:3610514].

Finally, for yield surfaces with sharp corners and edges, like the Tresca surface, the gradient is not uniquely defined. At these non-smooth points, the [normality rule](@entry_id:182635) is generalized using the concept of the **subdifferential**, which defines a 'cone' of possible normal directions. This allows for a non-unique direction of plastic flow at these specific stress states [@problem_id:3610491]. The numerical treatment of these corners presents a challenge in [computational plasticity](@entry_id:171377), often addressed by using smooth approximations of the yield surface [@problem_id:3610485].