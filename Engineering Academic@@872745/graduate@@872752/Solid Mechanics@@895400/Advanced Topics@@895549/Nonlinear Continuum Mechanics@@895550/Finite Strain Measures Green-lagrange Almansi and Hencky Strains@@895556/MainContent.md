## Introduction
In the study of [deformable bodies](@entry_id:201887), the concept of strain quantifies the local change in shape and size. While [infinitesimal strain](@entry_id:197162) theory provides a simple and powerful tool for many engineering problems, its linear assumptions break down when a body undergoes large displacements, rotations, or stretches. This creates a critical knowledge gap, as phenomena from [metal forming](@entry_id:188560) and rubber elasticity to the function of biological tissues are fundamentally governed by large deformations. Addressing this requires a move to the more general and physically robust framework of [finite strain theory](@entry_id:176941). This article provides a graduate-level exploration of the essential measures used to quantify [finite strain](@entry_id:749398).

The journey begins in the "Principles and Mechanisms" chapter, where we will derive the most important strain tensors—the Green-Lagrange, Almansi, and Hencky strains—from the fundamental concept of the deformation gradient. We will dissect their mathematical properties, including the crucial [principle of objectivity](@entry_id:185412), and compare their physical interpretations. Following this theoretical foundation, the "Applications and Interdisciplinary Connections" chapter demonstrates the practical power of these tools, showing how the choice of strain measure influences [constitutive modeling](@entry_id:183370) in [hyperelasticity](@entry_id:168357) and plasticity, drives computational strategies in the Finite Element Method, and enables the analysis of complex systems in [biomechanics](@entry_id:153973) and materials science. Finally, the "Hands-On Practices" section offers a series of targeted problems designed to solidify your understanding of these concepts through direct application, bridging the gap between theory and practice.

## Principles and Mechanisms

The transition from infinitesimal to [finite strain theory](@entry_id:176941) marks a significant conceptual shift in [continuum mechanics](@entry_id:155125). While [infinitesimal strain](@entry_id:197162) theory benefits from the mathematical convenience of [linearization](@entry_id:267670), it is fundamentally restricted to deformations where both displacements and displacement gradients are small. In contrast, many engineering and scientific problems—spanning from the manufacturing of metals to the biomechanics of soft tissues—involve [large deformations](@entry_id:167243), necessitating a more robust kinematic framework. This chapter delves into the principles and mechanisms underpinning the most common and significant measures of [finite strain](@entry_id:749398). We will construct these measures from first principles, explore their mathematical properties, and establish criteria for their appropriate use in [constitutive modeling](@entry_id:183370).

### Measuring Deformation: From Line Elements to Strain Tensors

The cornerstone of [finite deformation kinematics](@entry_id:195826) is the **[deformation gradient](@entry_id:163749)**, a second-order tensor denoted by $\mathbf{F}$. It describes how a material body maps from a **reference configuration**, $\mathcal{B}_0$, to a **current configuration**, $\mathcal{B}$. For a material point with [position vector](@entry_id:168381) $\mathbf{X}$ in $\mathcal{B}_0$ that moves to position $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X})$ in $\mathcal{B}$, the [deformation gradient](@entry_id:163749) is defined as the gradient of the motion with respect to the material coordinates:

$$
\mathbf{F} = \nabla_{\mathbf{X}}\boldsymbol{\varphi}(\mathbf{X})
$$

The primary role of $\mathbf{F}$ is to act as the [linear map](@entry_id:201112) that transforms infinitesimal material line elements, $d\mathbf{X}$, in the neighborhood of $\mathbf{X}$ into their corresponding spatial line elements, $d\mathbf{x}$, in the neighborhood of $\mathbf{x}$ [@problem_id:2640367]. This fundamental relationship, a [local linearization](@entry_id:169489) of the deformation map, is expressed as:

$$
d\mathbf{x} = \mathbf{F} \, d\mathbf{X}
$$

A direct measure of deformation, or strain, must quantify the change in the geometry of the material, such as changes in length and angle between material fibers. A powerful way to capture this is to compare the squared length of a [line element](@entry_id:196833) before and after deformation. Let $dS^2$ be the squared length of the material [line element](@entry_id:196833) $d\mathbf{X}$ and $ds^2$ be the squared length of the spatial line element $d\mathbf{x}$. In a Euclidean space, these are given by the standard inner product:

$$
dS^2 = d\mathbf{X} \cdot d\mathbf{X}
$$
$$
ds^2 = d\mathbf{x} \cdot d\mathbf{x}
$$

Strain, in its essence, is related to the difference $ds^2 - dS^2$. If this difference is zero for all material line elements emanating from a point, then no local deformation (stretching or shearing) has occurred; the motion is locally a [rigid body motion](@entry_id:144691). The various [finite strain measures](@entry_id:185716) are distinguished by how they formalize this comparison.

### The Lagrangian Perspective: The Green–Lagrange Strain Tensor

A **Lagrangian** (or **material**) description of motion tracks all physical quantities with respect to the fixed reference configuration $\mathcal{B}_0$. To formulate a strain measure within this framework, we must express the change in length, $ds^2 - dS^2$, purely in terms of quantities defined on the reference configuration, specifically the material line element $d\mathbf{X}$.

We begin by expressing the deformed squared length $ds^2$ in terms of $d\mathbf{X}$:
$$
ds^2 = d\mathbf{x} \cdot d\mathbf{x} = (\mathbf{F} \, d\mathbf{X}) \cdot (\mathbf{F} \, d\mathbf{X})
$$
Using the property of the transpose, $(\mathbf{A}\mathbf{u}) \cdot \mathbf{v} = \mathbf{u} \cdot (\mathbf{A}^{\mathsf{T}}\mathbf{v})$, we can rewrite this as:
$$
ds^2 = d\mathbf{X} \cdot (\mathbf{F}^{\mathsf{T}} \mathbf{F} \, d\mathbf{X})
$$
This expression introduces a crucial symmetric tensor, the **right Cauchy–Green deformation tensor** $\mathbf{C}$:

$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}} \mathbf{F}
$$

The tensor $\mathbf{C}$ is a fundamental material measure of deformation. It contains all the information about the local change in metric properties of the material. The relation $ds^2 = d\mathbf{X} \cdot \mathbf{C} \, d\mathbf{X}$ can be interpreted as stating that $\mathbf{C}$ represents the "pulled-back" metric of the deformed configuration onto the reference configuration.

The change in squared length is then:
$$
ds^2 - dS^2 = d\mathbf{X} \cdot (\mathbf{C} \, d\mathbf{X}) - d\mathbf{X} \cdot (\mathbf{I} \, d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{C} - \mathbf{I}) \, d\mathbf{X}
$$
where $\mathbf{I}$ is the identity tensor, representing the metric of the undeformed reference configuration.

The **Green–Lagrange strain tensor**, $\mathbf{E}$, is defined as the unique [symmetric tensor](@entry_id:144567) that satisfies the relation [@problem_id:2640392]:
$$
\frac{1}{2}(ds^2 - dS^2) = d\mathbf{X} \cdot \mathbf{E} \, d\mathbf{X}
$$
By comparing this definition with the previous expression, we arrive at the explicit form of the Green–Lagrange [strain tensor](@entry_id:193332) [@problem_id:2640367]:

$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^{\mathsf{T}} \mathbf{F} - \mathbf{I})
$$

This tensor is unequivocally a Lagrangian measure: it is defined on the reference configuration, it is expressed in terms of material kinematic quantities, and it operates on material vectors like $d\mathbf{X}$.

### The Eulerian Perspective: The Almansi Strain Tensor

In contrast, an **Eulerian** (or **spatial**) description tracks quantities with respect to the current, deformed configuration $\mathcal{B}$. This perspective is natural for problems in fluid dynamics or situations where tracking individual material points is impractical. To formulate a strain measure in this framework, we must express the change in length, $ds^2 - dS^2$, in terms of the spatial [line element](@entry_id:196833) $d\mathbf{x}$.

Assuming the deformation is locally invertible (i.e., $\det \mathbf{F} > 0$), we can write $d\mathbf{X} = \mathbf{F}^{-1} d\mathbf{x}$. We now express the undeformed squared length $dS^2$ in terms of $d\mathbf{x}$:
$$
dS^2 = d\mathbf{X} \cdot d\mathbf{X} = (\mathbf{F}^{-1} d\mathbf{x}) \cdot (\mathbf{F}^{-1} d\mathbf{x}) = d\mathbf{x} \cdot (\mathbf{F}^{-\mathsf{T}} \mathbf{F}^{-1} d\mathbf{x})
$$
This naturally introduces the inverse of the **left Cauchy–Green deformation tensor** (also known as the Finger tensor), $\mathbf{b} = \mathbf{F}\mathbf{F}^{\mathsf{T}}$. The tensor $\mathbf{b}^{-1} = \mathbf{F}^{-\mathsf{T}}\mathbf{F}^{-1}$ is called the **Cauchy deformation tensor**.

The change in squared length is:
$$
ds^2 - dS^2 = d\mathbf{x} \cdot (\mathbf{I} \, d\mathbf{x}) - d\mathbf{x} \cdot (\mathbf{b}^{-1} d\mathbf{x}) = d\mathbf{x} \cdot (\mathbf{I} - \mathbf{b}^{-1}) \, d\mathbf{x}
$$

The **Euler–Almansi [strain tensor](@entry_id:193332)**, $\mathbf{e}$, is defined as the unique symmetric tensor satisfying the relation [@problem_id:2640421]:
$$
\frac{1}{2}(ds^2 - dS^2) = d\mathbf{x} \cdot \mathbf{e} \, d\mathbf{x}
$$
This leads to the explicit form for the Almansi strain tensor:

$$
\mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{b}^{-1}) = \frac{1}{2}(\mathbf{I} - \mathbf{F}^{-\mathsf{T}}\mathbf{F}^{-1})
$$

The tensor $\mathbf{e}$ is an Eulerian measure as it is defined on the current configuration and operates on spatial vectors. It is crucial not to confuse this with the tensor $\frac{1}{2}(\mathbf{b} - \mathbf{I})$, which is a different strain measure often called the Finger strain tensor [@problem_id:2640367].

The Green-Lagrange and Almansi strain tensors are not independent but are kinematically linked. The Lagrangian tensor $\mathbf{E}$ can be "pushed forward" to the spatial configuration to obtain $\mathbf{e}$, and conversely, $\mathbf{e}$ can be "pulled back" to the [material configuration](@entry_id:183091) to yield $\mathbf{E}$. These fundamental relations are [@problem_id:2640367] [@problem_id:2640421]:

$$
\mathbf{e} = \mathbf{F}^{-\mathsf{T}} \mathbf{E} \mathbf{F}^{-1} \quad \text{(push-forward)}
$$
$$
\mathbf{E} = \mathbf{F}^{\mathsf{T}} \mathbf{e} \mathbf{F} \quad \text{(pull-back)}
$$

### The Principle of Objectivity and Frame-Indifference

A fundamental requirement for any physically meaningful constitutive law is the **[principle of material frame-indifference](@entry_id:188488)**, or **objectivity**. This principle asserts that the material response should not depend on the observer. An observer is characterized by their reference frame, and any two observers' frames are related by a time-dependent [rigid body motion](@entry_id:144691).

If a body undergoes a motion $\boldsymbol{\varphi}$, an observer in a different frame will perceive the motion as $\boldsymbol{\varphi}^*(\mathbf{X},t) = \mathbf{c}(t) + \mathbf{Q}(t)\boldsymbol{\varphi}(\mathbf{X},t)$, where $\mathbf{c}(t)$ is a time-dependent translation and $\mathbf{Q}(t)$ is a time-dependent proper orthogonal tensor ($\mathbf{Q}^{\mathsf{T}}\mathbf{Q}=\mathbf{I}, \det\mathbf{Q}=+1$). This is known as a **superposed [rigid body motion](@entry_id:144691)**. The deformation gradient transforms accordingly:

$$
\mathbf{F}^* = \nabla_{\mathbf{X}} \boldsymbol{\varphi}^* = \mathbf{Q} \nabla_{\mathbf{X}} \boldsymbol{\varphi} = \mathbf{Q}\mathbf{F}
$$

A quantity is said to be **objective** if its value is independent of the observer (for a material quantity) or transforms according to the rules of [tensor transformation](@entry_id:161187) (for a spatial quantity).

For a **material strain measure** $\boldsymbol{S}(\mathbf{F})$, objectivity requires invariance under this transformation [@problem_id:2640387]:
$$
\boldsymbol{S}(\mathbf{F}^*) = \boldsymbol{S}(\mathbf{F}) \quad \Rightarrow \quad \boldsymbol{S}(\mathbf{Q}\mathbf{F}) = \boldsymbol{S}(\mathbf{F}) \quad \forall \mathbf{Q} \in \mathrm{SO}(3)
$$
This condition has profound consequences. It precludes any strain measure that depends linearly on $\mathbf{F}$ itself, such as a naive generalization of the [infinitesimal strain tensor](@entry_id:167211), $\frac{1}{2}(\mathbf{F}+\mathbf{F}^{\mathsf{T}})-\mathbf{I}$. Such a measure is not objective [@problem_id:2640387].

Let's test the right Cauchy-Green tensor $\mathbf{C}$. Under a superposed rigid motion [@problem_id:2640340]:
$$
\mathbf{C}^* = (\mathbf{F}^*)^{\mathsf{T}}\mathbf{F}^* = (\mathbf{Q}\mathbf{F})^{\mathsf{T}}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^{\mathsf{T}}\mathbf{Q}^{\mathsf{T}}\mathbf{Q}\mathbf{F} = \mathbf{F}^{\mathsf{T}}\mathbf{I}\mathbf{F} = \mathbf{C}
$$
The right Cauchy-Green tensor is invariant under superposed rigid motions. Consequently, any strain measure that is a function of $\mathbf{C}$ alone, such as the Green-Lagrange strain $\mathbf{E} = \frac{1}{2}(\mathbf{C}-\mathbf{I})$, is an objective material measure of strain [@problem_id:2640340] [@problem_id:2640392] [@problem_id:2640387].

For a **spatial strain measure** $\boldsymbol{s}(\mathbf{F})$, objectivity requires that it transforms as a proper [spatial tensor](@entry_id:185799):
$$
\boldsymbol{s}(\mathbf{F}^*) = \mathbf{Q} \boldsymbol{s}(\mathbf{F}) \mathbf{Q}^{\mathsf{T}}
$$
Let's test the left Cauchy-Green tensor $\mathbf{b}$ [@problem_id:2640340]:
$$
\mathbf{b}^* = \mathbf{F}^*(\mathbf{F}^*)^{\mathsf{T}} = (\mathbf{Q}\mathbf{F})(\mathbf{Q}\mathbf{F})^{\mathsf{T}} = \mathbf{Q}\mathbf{F}\mathbf{F}^{\mathsf{T}}\mathbf{Q}^{\mathsf{T}} = \mathbf{Q}\mathbf{b}\mathbf{Q}^{\mathsf{T}}
$$
The tensor $\mathbf{b}$ transforms covariantly with the spatial frame. This is the correct transformation for an objective [spatial tensor](@entry_id:185799). As a result, any **[isotropic tensor](@entry_id:189108) function** of $\mathbf{b}$, such as the Almansi strain $\mathbf{e} = \frac{1}{2}(\mathbf{I}-\mathbf{b}^{-1})$, is an objective spatial measure of strain [@problem_id:2640387] [@problem_id:2640421]. The scalar [principal invariants](@entry_id:193522) of $\mathbf{b}$ (e.g., $\mathrm{tr}\,\mathbf{b}$, $\det\mathbf{b}$) are, of course, invariant under this transformation and are thus objective scalars [@problem_id:2640340].

A necessary condition for any valid strain measure is that it must vanish for a pure [rigid body motion](@entry_id:144691). For such a motion, $\mathbf{F}=\mathbf{Q}$, where $\mathbf{Q}$ is a constant orthogonal tensor. In this case, $\mathbf{C} = \mathbf{Q}^{\mathsf{T}}\mathbf{Q} = \mathbf{I}$ and $\mathbf{b} = \mathbf{Q}\mathbf{Q}^{\mathsf{T}} = \mathbf{I}$. It follows immediately that $\mathbf{E} = \frac{1}{2}(\mathbf{I}-\mathbf{I})=\mathbf{0}$ and $\mathbf{e} = \frac{1}{2}(\mathbf{I}-\mathbf{I}^{-1})=\mathbf{0}$, satisfying this crucial requirement [@problem_id:2640367].

### Physical Decomposition of Deformation: Stretch, Rotation, and the Hencky Strain

While the Cauchy-Green tensors are mathematically convenient for establishing objectivity, they conflate stretching and rotation. The **[polar decomposition theorem](@entry_id:753554)** provides a powerful tool to separate these two distinct physical aspects of deformation. The theorem states that for any invertible deformation gradient $\mathbf{F}$ (with $\det \mathbf{F} > 0$), there exist unique decompositions [@problem_id:2640372]:
$$
\mathbf{F} = \mathbf{R}\mathbf{U} \quad \text{(right polar decomposition)}
$$
$$
\mathbf{F} = \mathbf{V}\mathbf{R} \quad \text{(left polar decomposition)}
$$
Here, $\mathbf{R}$ is a proper orthogonal tensor ($\mathbf{R} \in \mathrm{SO}(3)$) representing the rigid rotation of the material element, while $\mathbf{U}$ and $\mathbf{V}$ are [symmetric positive-definite](@entry_id:145886) (SPD) tensors known as the **[right stretch tensor](@entry_id:193756)** and **[left stretch tensor](@entry_id:197330)**, respectively.

Physically, $\mathbf{F}=\mathbf{R}\mathbf{U}$ can be interpreted as a pure stretch $\mathbf{U}$ in the [material configuration](@entry_id:183091), followed by a rigid rotation $\mathbf{R}$ into the spatial configuration. Conversely, $\mathbf{F}=\mathbf{V}\mathbf{R}$ represents the same rotation $\mathbf{R}$ followed by a pure stretch $\mathbf{V}$ in the spatial configuration. The stretch tensors are directly related to the Cauchy-Green tensors:
$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = (\mathbf{R}\mathbf{U})^{\mathsf{T}}(\mathbf{R}\mathbf{U}) = \mathbf{U}^{\mathsf{T}}\mathbf{R}^{\mathsf{T}}\mathbf{R}\mathbf{U} = \mathbf{U}^2
$$
$$
\mathbf{b} = \mathbf{F}\mathbf{F}^{\mathsf{T}} = (\mathbf{V}\mathbf{R})(\mathbf{V}\mathbf{R})^{\mathsf{T}} = \mathbf{V}\mathbf{R}\mathbf{R}^{\mathsf{T}}\mathbf{V}^{\mathsf{T}} = \mathbf{V}^2
$$
Thus, $\mathbf{U}$ and $\mathbf{V}$ are the unique SPD square roots of $\mathbf{C}$ and $\mathbf{b}$, respectively:
$$
\mathbf{U} = \sqrt{\mathbf{C}} \quad \text{and} \quad \mathbf{V} = \sqrt{\mathbf{b}}
$$
The two stretch tensors are related by a [similarity transformation](@entry_id:152935) via the [rotation tensor](@entry_id:191990), $\mathbf{V} = \mathbf{R}\mathbf{U}\mathbf{R}^{\mathsf{T}}$, which implies they share the same eigenvalues. These eigenvalues, $\lambda_i > 0$, are the **[principal stretches](@entry_id:194664)** and represent the ratio of deformed length to original length along three mutually orthogonal directions (the [principal axes of strain](@entry_id:188315)) [@problem_id:2640372].

This decomposition motivates a strain measure based purely on stretch, removing the rotational part of the deformation. The **Hencky strain** (or **[logarithmic strain](@entry_id:751438)**) is defined as the natural logarithm of the [stretch tensor](@entry_id:193200). The **material Hencky strain tensor** is:
$$
\mathbf{H} = \ln \mathbf{U}
$$
The **spatial Hencky [strain tensor](@entry_id:193332)** is:
$$
\mathbf{h} = \ln \mathbf{V}
$$
Since $\mathbf{U}=\sqrt{\mathbf{C}}$ and $\mathbf{V}=\sqrt{\mathbf{b}}$, these can also be written as [@problem_id:2640367] [@problem_id:2640338]:
$$
\mathbf{H} = \frac{1}{2}\ln\mathbf{C} \quad \text{and} \quad \mathbf{h} = \frac{1}{2}\ln\mathbf{b}
$$
The tensor logarithm is defined via [spectral decomposition](@entry_id:148809). If a symmetric tensor $\mathbf{T}$ has eigenvalues $\mu_i$ and corresponding orthonormal eigenvectors $\mathbf{n}_i$, so that $\mathbf{T} = \sum_i \mu_i \mathbf{n}_i \otimes \mathbf{n}_i$, then any function $f(\mathbf{T})$ is defined as $f(\mathbf{T}) = \sum_i f(\mu_i) \mathbf{n}_i \otimes \mathbf{n}_i$. For the Hencky strain, this means its [principal values](@entry_id:189577) (eigenvalues) are the natural logarithms of the [principal stretches](@entry_id:194664), $\ln \lambda_i$ [@problem_id:2640338]. Because $\mathbf{U}$ is invariant under superposed rigid motions, so is $\mathbf{H}$. Because $\mathbf{V}$ transforms as $\mathbf{V}^* = \mathbf{Q}\mathbf{V}\mathbf{Q}^{\mathsf{T}}$, the spatial Hencky strain transforms as $\mathbf{h}^*=\mathbf{Q}\mathbf{h}\mathbf{Q}^{\mathsf{T}}$, ensuring its objectivity [@problem_id:2640340]. As required, Hencky strain also vanishes for any [rigid body motion](@entry_id:144691), since in that case $\mathbf{U}=\mathbf{I}$ and $\ln \mathbf{I} = \mathbf{0}$ [@problem_id:2640367].

### A Comparative Analysis of Finite Strain Measures

The Green-Lagrange, Almansi, and Hencky strains provide different, non-equivalent ways to quantify [finite deformation](@entry_id:172086). Their differences become apparent when we analyze their behavior in specific scenarios.

#### A One-Dimensional Case Study

Consider a simple homogeneous uniaxial stretch, where a material line of initial length $X$ is stretched to a final length $x = \lambda X$. Here, the stretch $\lambda > 0$ is the sole kinematic variable. The deformation gradient and Cauchy-Green tensors become scalars: $F=\lambda$, $C=b=\lambda^2$. The three [strain measures](@entry_id:755495) simplify to [@problem_id:2640403]:

-   Green-Lagrange strain: $E = \frac{1}{2}(\lambda^2 - 1)$
-   Almansi strain: $e = \frac{1}{2}(1 - \lambda^{-2})$
-   Hencky strain: $H = \ln \lambda$

All three measures are zero for no deformation ($\lambda=1$) and are strictly increasing functions of $\lambda$. However, their quantitative values and behavior diverge significantly as the deformation becomes large.

For any deformation ($\lambda \neq 1$), the values are ordered: $E \ge H \ge e$. The equality holds only at $\lambda=1$. For instance, in tension ($\lambda > 1$), $E$ is the largest measure, while in compression ($0  \lambda  1$), $e$ is the most negative (largest compressive strain). As compression becomes extreme ($\lambda \to 0^+$), $E$ approaches a finite limit of $-1/2$, whereas both $e$ and $H$ diverge to $-\infty$. This highlights that $E$ is less sensitive to large compressive strains.

Crucially, in the limit of small strains, where $\lambda = 1 + \varepsilon$ with $|\varepsilon| \ll 1$, all three measures converge to the familiar infinitesimal engineering strain $\varepsilon$:
$$
E = \frac{1}{2}((1+\varepsilon)^2 - 1) = \varepsilon + O(\varepsilon^2)
$$
$$
e = \frac{1}{2}(1 - (1+\varepsilon)^{-2}) = \varepsilon + O(\varepsilon^2)
$$
$$
H = \ln(1+\varepsilon) = \varepsilon + O(\varepsilon^2)
$$
This demonstrates that all three are valid extensions of the infinitesimal theory, but they disagree at second-order and higher terms in strain [@problem_id:2640403]. A noteworthy relationship in this 1D case is $E = \lambda^2 e$, which is a specialization of the general pull-back/push-forward relation [@problem_id:2640403].

#### Additivity Under Composition

A highly desirable property for a strain measure, particularly in incremental plasticity or viscoelasticity, is additivity. If a body undergoes a deformation $F_1$ followed by a second deformation $F_2$, the total deformation is $F=F_2F_1$. Is the total strain the sum of the individual strains?

To investigate this, consider a sequence of two coaxial pure stretches along the $\mathbf{e}_1$ axis: $F_1 = \mathrm{diag}(a,1,1)$ and $F_2 = \mathrm{diag}(b,1,1)$. The total deformation is $F = F_2F_1 = \mathrm{diag}(ab,1,1)$ [@problem_id:2640405].

-   **Green-Lagrange Strain**: The total strain is $E(F) = \frac{1}{2}\mathrm{diag}(a^2b^2-1,0,0)$. The sum of individual strains is $E(F_1)+E(F_2) = \frac{1}{2}\mathrm{diag}(a^2+b^2-2,0,0)$. These are not equal unless $a=1$ or $b=1$. The non-additivity arises directly from the quadratic nature of the definition $E \propto F^{\mathsf{T}}F$, which introduces cross-terms.

-   **Almansi Strain**: A similar analysis shows that $e$ is also not additive, again due to its quadratic dependence on $F^{-1}$.

-   **Hencky Strain**: The total strain is $H(F) = \ln(\mathrm{diag}(ab,1,1)) = \mathrm{diag}(\ln(ab),0,0)$. The sum of individual strains is $H(F_1)+H(F_2) = \mathrm{diag}(\ln a + \ln b, 0, 0)$. Due to the fundamental property of the logarithm, $\ln(ab) = \ln a + \ln b$, the Hencky strain is perfectly additive for this sequence of coaxial stretches [@problem_id:2640405]. This property holds generally for any sequence of deformations where the right stretch tensors commute [@problem_id:2640338].

This unique additive property makes the Hencky strain the most "physical" or "true" strain, as it accumulates naturally under successive deformations in the same way that infinitesimal strains do.

#### The Volumetric-Deviatoric Split

In many material models, it is essential to separate the deformation into a part that changes volume (volumetric) and a part that distorts the shape at constant volume (deviatoric or isochoric). The volume change is quantified by the Jacobian, $J = \det \mathbf{F} = \lambda_1 \lambda_2 \lambda_3$.

Again, the Hencky strain stands out. The trace of the material Hencky [strain tensor](@entry_id:193332) is directly related to the logarithm of the volume change [@problem_id:2640409]:
$$
\mathrm{tr}(\mathbf{H}) = \mathrm{tr}(\ln \mathbf{U}) = \sum_i \ln \lambda_i = \ln(\prod_i \lambda_i) = \ln J
$$
This provides an exact, additive decomposition of the strain into a volumetric part, represented by its trace, and a deviatoric part, $\mathbf{H}^{\mathrm{dev}} = \mathbf{H} - \frac{1}{3}(\mathrm{tr}\mathbf{H})\mathbf{I}$, which represents pure distortion [@problem_id:2640338].

In contrast, the traces of the Green-Lagrange and Almansi strains do not have a simple, direct relationship to $J$:
$$
\mathrm{tr}(\mathbf{E}) = \frac{1}{2}(\lambda_1^2 + \lambda_2^2 + \lambda_3^2 - 3)
$$
$$
\mathrm{tr}(\mathbf{e}) = \frac{1}{2}(3 - (\lambda_1^{-2} + \lambda_2^{-2} + \lambda_3^{-2}))
$$
While these can be related to volume change under certain assumptions (e.g., small volumetric strains), the relationship is not as clean or exact as for the Hencky strain.

### Practical Considerations for Constitutive Modeling

The choice among $E$, $e$, and $H$ is not merely a matter of academic preference but has significant practical implications in the formulation and computational implementation of material models. The selection should be guided by the physics of the problem and the structure of the numerical framework [@problem_id:2640409].

-   **The Green–Lagrange [strain tensor](@entry_id:193332) ($E$)** is the natural choice for **total Lagrangian** finite element formulations, particularly in **[hyperelasticity](@entry_id:168357)**. In this context, a [stored energy function](@entry_id:166355) $W$ is often postulated as a function of the invariants of $\mathbf{C}$ (or, equivalently, of $\mathbf{E}$). The [work-conjugate stress](@entry_id:182069) measure is the 2nd Piola-Kirchhoff stress tensor $\mathbf{S}$, leading to the elegant [constitutive relation](@entry_id:268485) $\mathbf{S} = 2 \frac{\partial W}{\partial \mathbf{C}}$. This creates a self-consistent and computationally convenient framework entirely within the reference configuration.

-   **The Euler–Almansi strain tensor ($e$)** is best suited for **Eulerian** or **updated Lagrangian** formulations, where [state variables](@entry_id:138790) are stored and updated in the current configuration. This is typical in [fluid mechanics](@entry_id:152498), [fluid-structure interaction](@entry_id:171183) problems, or in [solid mechanics](@entry_id:164042) simulations involving frequent remeshing. The [work-conjugate stress](@entry_id:182069) is the Cauchy stress $\boldsymbol{\sigma}$, which is also a [spatial tensor](@entry_id:185799), making $\mathbf{e}$ a natural kinematic partner.

-   **The Hencky [strain tensor](@entry_id:193332) ($H$ or $h$)** is often preferred in theories of **large-strain plasticity** and **[viscoelasticity](@entry_id:148045)**. Its additivity for coaxial stretches is invaluable for developing incremental update algorithms. The [multiplicative decomposition](@entry_id:199514) of the deformation gradient into elastic and plastic parts, $F=F^e F^p$, is handled more naturally in a [logarithmic space](@entry_id:270258). Furthermore, its exact volumetric-deviatoric split is crucial for material models that treat bulk (volumetric) and shear (deviatoric) responses differently, as is common for metals and polymers. Despite the higher computational cost of evaluating the tensor logarithm, these theoretical advantages often make it the superior choice for complex inelastic [material modeling](@entry_id:173674).

In summary, while all three measures are valid and reduce to the same [infinitesimal strain](@entry_id:197162), their distinct properties in the [finite deformation](@entry_id:172086) regime make them suitable for different classes of problems. A deep understanding of these properties is essential for the modern practitioner of [computational solid mechanics](@entry_id:169583).