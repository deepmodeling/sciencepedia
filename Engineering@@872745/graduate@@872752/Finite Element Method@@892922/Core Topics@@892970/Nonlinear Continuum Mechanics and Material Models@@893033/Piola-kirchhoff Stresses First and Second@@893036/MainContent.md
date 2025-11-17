## Introduction
In the analysis of materials undergoing [large deformations](@entry_id:167243), describing the state of stress presents a fundamental challenge. While the familiar Cauchy stress accurately describes forces in the current, deformed state, it is cumbersome for formulations based on the initial, undeformed geometry—a cornerstone of solid mechanics and the finite element method. This gap necessitates the use of alternative [stress measures](@entry_id:198799) that connect the deformed and reference configurations. This article introduces the first and second Piola-Kirchhoff stress tensors, essential tools for a Lagrangian description of [continuum mechanics](@entry_id:155125). In the following chapters, you will gain a comprehensive understanding of these concepts. The "Principles and Mechanisms" chapter will establish their theoretical foundation, exploring their definitions, physical interpretations, and relationships with Cauchy stress. Next, "Applications and Interdisciplinary Connections" will demonstrate their crucial role in solving real-world problems in [computational mechanics](@entry_id:174464), materials science, and [biomechanics](@entry_id:153973). Finally, the "Hands-On Practices" section will provide practical exercises to reinforce these theoretical and applied concepts, bridging the gap between theory and implementation.

## Principles and Mechanisms

In the study of [large deformations](@entry_id:167243), the familiar Cauchy stress tensor, while fundamental to the description of the stress state in the current (deformed) configuration, presents significant challenges when formulating problems in a Lagrangian or material framework. When we wish to describe the behavior of a body with respect to its initial, undeformed state—a common requirement in solid mechanics and essential for the Total Lagrangian formulation in the finite element method—we need [stress measures](@entry_id:198799) that connect forces in the deformed body to the geometry of the original body. This chapter introduces two such measures: the **first and second Piola-Kirchhoff stress tensors**. We will explore their definitions, physical interpretations, key properties, and their indispensable roles in [constitutive modeling](@entry_id:183370) and computational mechanics.

### The First Piola-Kirchhoff Stress Tensor

The primary motivation for a new stress measure arises from the need to express the [equilibrium equations](@entry_id:172166) over the known reference volume. To achieve this, we require a quantity that relates the true force acting on a surface in the current configuration to the area of that surface in the reference configuration. This leads to the concept of **nominal traction**.

#### Definition and Physical Interpretation

Let us consider a surface element in the reference configuration, $\mathcal{B}_0$, with area $dA$ and outward unit normal $\mathbf{N}$. Under a deformation $\boldsymbol{\varphi}$, this surface element is mapped to one in the current configuration, $\mathcal{B}_t$, with area $da$ and normal $\mathbf{n}$. A force vector $d\mathbf{f}$ acts on this current surface element. The **nominal traction**, denoted $\mathbf{T}_0$, is defined as the force per unit *reference* area:

$$
d\mathbf{f} = \mathbf{T}_0 \, dA
$$

Just as Cauchy's stress theorem posits a [linear relationship](@entry_id:267880) between the true traction $\mathbf{t}$ and the spatial normal $\mathbf{n}$ (i.e., $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$), we define the **first Piola-Kirchhoff stress tensor**, $\mathbf{P}$, as the linear operator that maps the material normal $\mathbf{N}$ to the nominal traction $\mathbf{T}_0$ [@problem_id:2641039]:

$$
\mathbf{T}_0 = \mathbf{P}\mathbf{N}
$$

From these definitions, we see that the force vector is given by $d\mathbf{f} = \mathbf{P}\mathbf{N} \, dA$. It is crucial to recognize the nature of $\mathbf{P}$: it maps a vector from the reference configuration ($\mathbf{N}$) to a force vector that exists in the current spatial configuration ($d\mathbf{f}$). For this reason, $\mathbf{P}$ is known as a **two-point tensor** [@problem_id:2587891].

#### Relation to Cauchy Stress

To be a valid stress measure, $\mathbf{P}$ must be consistent with the Cauchy stress $\boldsymbol{\sigma}$. The force element $d\mathbf{f}$ is the same regardless of description: $d\mathbf{f} = \mathbf{t} \, da = \boldsymbol{\sigma}\mathbf{n} \, da$. Equating this with the expression involving $\mathbf{P}$ gives:

$$
\mathbf{P}\mathbf{N} \, dA = \boldsymbol{\sigma}\mathbf{n} \, da
$$

To proceed, we need the relationship between the oriented area elements in the two configurations. This is given by **Nanson's formula**, a direct consequence of the [kinematics of deformation](@entry_id:189142) [@problem_id:2640987]:

$$
\mathbf{n} \, da = J \mathbf{F}^{-T} \mathbf{N} \, dA
$$

Here, $\mathbf{F} = \nabla_{\mathbf{X}} \boldsymbol{\varphi}$ is the deformation gradient, $J = \det \mathbf{F}$ is the Jacobian determinant representing the local volume ratio, and $\mathbf{F}^{-T}$ is the inverse transpose of $\mathbf{F}$. Substituting Nanson's formula into the [force balance](@entry_id:267186) equation yields:

$$
\mathbf{P}\mathbf{N} \, dA = \boldsymbol{\sigma} (J \mathbf{F}^{-T} \mathbf{N} \, dA)
$$

Since this must hold for any surface element, we can deduce the fundamental relationship between the first Piola-Kirchhoff stress and the Cauchy stress [@problem_id:2641039]:

$$
\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-T}
$$

This important relation is sometimes called the **Piola transform**.

#### The Question of Symmetry

A defining property of the Cauchy stress tensor $\boldsymbol{\sigma}$, in the absence of body couples, is its symmetry ($\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$), which arises from the [balance of angular momentum](@entry_id:181848). A natural question is whether $\mathbf{P}$ shares this property. Let's examine its transpose:

$$
\mathbf{P}^T = (J \boldsymbol{\sigma} \mathbf{F}^{-T})^T = J (\mathbf{F}^{-T})^T \boldsymbol{\sigma}^T = J \mathbf{F}^{-1} \boldsymbol{\sigma}
$$

We can see that $\mathbf{P} \neq \mathbf{P}^T$ in general. The first Piola-Kirchhoff stress tensor is **not symmetric** for an arbitrary deformation, even when the underlying Cauchy stress is symmetric [@problem_id:2640989] [@problem_id:2641039]. Its asymmetry does not imply a violation of angular momentum balance. Rather, the [balance of angular momentum](@entry_id:181848), when pulled back to the reference configuration, manifests differently. It can be shown that the correct condition is the symmetry of the tensor $\mathbf{P}\mathbf{F}^T$:

$$
(\mathbf{P}\mathbf{F}^T)^T = (J \boldsymbol{\sigma} \mathbf{F}^{-T} \mathbf{F}^T)^T = (J \boldsymbol{\sigma})^T = J \boldsymbol{\sigma}^T = J \boldsymbol{\sigma} = \mathbf{P}\mathbf{F}^T
$$

Since $J\boldsymbol{\sigma}$ is symmetric (assuming $\boldsymbol{\sigma}$ is symmetric), $\mathbf{P}\mathbf{F}^T$ must also be symmetric. This condition, $\mathbf{P}\mathbf{F}^T = \mathbf{F}\mathbf{P}^T$, represents the satisfaction of [moment equilibrium](@entry_id:752138) in the material description [@problem_id:2640989]. The physical reason for the non-symmetry of $\mathbf{P}$ is that it relates a force in the current configuration to an area in the reference configuration. The lever arms associated with these forces are different in the two configurations, and the asymmetry of $\mathbf{P}$ accounts for this difference in the moment balance.

### The Second Piola-Kirchhoff Stress Tensor

The non-symmetry of $\mathbf{P}$ and its nature as a two-point tensor can be inconvenient for [constitutive modeling](@entry_id:183370). It is desirable to have a stress measure that is fully Lagrangian (i.e., defined entirely with respect to the reference configuration) and symmetric. This motivates the introduction of the **second Piola-Kirchhoff stress tensor**, $\mathbf{S}$.

#### Definition from Force Transformation

The tensor $\mathbf{S}$ is defined by "pulling back" the force element $d\mathbf{f}$ from the current configuration to the reference configuration using the inverse of the deformation gradient, $\mathbf{F}^{-1}$. We define a pseudo-force vector in the material frame, $d\mathbf{f}_0 = \mathbf{F}^{-1} d\mathbf{f}$, and postulate that this pseudo-force is related to the material normal $\mathbf{N}$ via the tensor $\mathbf{S}$:

$$
d\mathbf{f}_0 = \mathbf{S}\mathbf{N} \, dA \quad \implies \quad \mathbf{F}^{-1} d\mathbf{f} = \mathbf{S}\mathbf{N} \, dA
$$

Recalling that $d\mathbf{f} = \mathbf{P}\mathbf{N} \, dA$, we have:

$$
\mathbf{F}^{-1} (\mathbf{P}\mathbf{N} \, dA) = \mathbf{S}\mathbf{N} \, dA
$$

This must hold for any $\mathbf{N}$, leading to the defining relationship between $\mathbf{S}$ and $\mathbf{P}$ [@problem_id:2641038]:

$$
\mathbf{S} = \mathbf{F}^{-1}\mathbf{P} \quad \text{or equivalently} \quad \mathbf{P} = \mathbf{F}\mathbf{S}
$$

#### Physical Interpretation and Properties

The vector $\mathbf{S}\mathbf{N}$ can be interpreted as a pseudo-[traction vector](@entry_id:189429) in the reference configuration. To obtain the true physical traction per unit reference area, $\mathbf{T}_0$, one must "push" this vector forward to the current configuration via the deformation gradient: $\mathbf{T}_0 = \mathbf{F}(\mathbf{S}\mathbf{N})$ [@problem_id:2587891].

By combining the definitions, we can relate $\mathbf{S}$ directly to the Cauchy stress $\boldsymbol{\sigma}$:

$$
\mathbf{S} = \mathbf{F}^{-1} (J \boldsymbol{\sigma} \mathbf{F}^{-T}) = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T}
$$

A key advantage of $\mathbf{S}$ is its symmetry. If the Cauchy stress $\boldsymbol{\sigma}$ is symmetric, then $\mathbf{S}$ is also symmetric, as shown by taking the transpose [@problem_id:2641038]:

$$
\mathbf{S}^T = (J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T})^T = J (\mathbf{F}^{-T})^T \boldsymbol{\sigma}^T (\mathbf{F}^{-1})^T = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T} = \mathbf{S}
$$

This symmetry makes $\mathbf{S}$ an ideal candidate for use in [constitutive equations](@entry_id:138559) for materials whose response is described relative to the material frame.

### Energetic Conjugacy and Virtual Work

The different [stress and strain](@entry_id:137374) measures are not independent but are linked through the principle of work. The rate of internal work done per unit volume, or [stress power](@entry_id:182907), provides a rigorous way to identify which stress measure is "energetically conjugate" to which strain rate measure.

The [stress power](@entry_id:182907) per unit *current* volume is given by the contraction of the Cauchy stress and the [rate of deformation tensor](@entry_id:182598), $\mathbf{d} = \mathrm{sym}(\nabla_{\mathbf{x}}\mathbf{v})$:

$$
\dot{w}_{current} = \boldsymbol{\sigma} : \mathbf{d}
$$

To find the power per unit *reference* volume, we multiply by the volume ratio $J$: $\dot{w}_{ref} = J (\boldsymbol{\sigma} : \mathbf{d})$. Through kinematic manipulation, this can be shown to be equivalent to two other important forms [@problem_id:2525704]:

$$
\dot{w}_{ref} = \mathbf{P} : \dot{\mathbf{F}} = \mathbf{S} : \dot{\mathbf{E}}
$$

where $\dot{\mathbf{F}}$ is the [material time derivative](@entry_id:190892) of the [deformation gradient](@entry_id:163749), and $\dot{\mathbf{E}}$ is the [material time derivative](@entry_id:190892) of the **Green-Lagrange [strain tensor](@entry_id:193332)** $\mathbf{E} = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I})$. The equivalence $\mathbf{P} : \dot{\mathbf{F}} = \mathbf{S} : \dot{\mathbf{E}}$ can be demonstrated directly by substituting $\mathbf{P} = \mathbf{F}\mathbf{S}$ and noting the definition of $\dot{\mathbf{E}}$ [@problem_id:2641038].

These relationships establish the fundamental work-conjugate pairs:
- $(\boldsymbol{\sigma}, \mathbf{d})$ in the spatial description.
- $(\mathbf{P}, \mathbf{F})$ in the material description.
- $(\mathbf{S}, \mathbf{E})$ in the material description.

The pair $(\mathbf{S}, \mathbf{E})$ is particularly significant. Since both tensors are fully material and symmetric, they form the natural basis for defining hyperelastic [constitutive laws](@entry_id:178936), where a [strain energy function](@entry_id:170590) $\Psi$ is defined such that $\mathbf{S} = \partial\Psi / \partial\mathbf{E}$.

As an illustrative example, consider the calculation of the [internal virtual work](@entry_id:172278) density, $\delta w_{int} = \mathbf{P} : \delta\mathbf{F}$, for a material point with a given state. Suppose the state is defined by [@problem_id:1549744]:
$$
\mathbf{F} = \begin{pmatrix} 1.5  -0.5  0 \\ 1.0  1.0  0 \\ 0  0  1.2 \end{pmatrix}, \quad
\mathbf{S} = \begin{pmatrix} 200  50  0 \\ 50  100  0 \\ 0  0  80 \end{pmatrix} \text{ MPa}
$$
and a virtual deformation is $\delta\mathbf{F} = \begin{pmatrix} 0.02  0.01  0 \\ -0.01  0.03  0 \\ 0  0  -0.02 \end{pmatrix}$.
First, we compute $\mathbf{P} = \mathbf{F}\mathbf{S}$:
$$
\mathbf{P} = \begin{pmatrix} 1.5  -0.5  0 \\ 1.0  1.0  0 \\ 0  0  1.2 \end{pmatrix} \begin{pmatrix} 200  50  0 \\ 50  100  0 \\ 0  0  80 \end{pmatrix} = \begin{pmatrix} 275  25  0 \\ 250  150  0 \\ 0  0  96 \end{pmatrix} \text{ MPa}
$$
The virtual work density is then the Frobenius inner product $\mathbf{P} : \delta\mathbf{F}$:
$$
\delta w_{int} = (275)(0.02) + (25)(0.01) + (250)(-0.01) + (150)(0.03) + (96)(-0.02) = 5.83 \, \text{MPa}
$$

### Objectivity and Material Frame-Indifference

A crucial requirement for any constitutive law is that the material response should not depend on the observer; specifically, it must be independent of superposed [rigid body motions](@entry_id:200666). This principle is known as **[material frame-indifference](@entry_id:178419)** or **objectivity**. Let's examine how the different stress tensors behave under a [rigid body rotation](@entry_id:167024) $\mathbf{Q}$ applied to the current configuration, such that the new spatial position is $\mathbf{x}^* = \mathbf{Q}\mathbf{x}$.

The corresponding transformation rules for the [deformation gradient](@entry_id:163749) and Cauchy stress are:
$$
\mathbf{F}^* = \mathbf{Q}\mathbf{F} \quad \text{and} \quad \boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T
$$

The transformation for the first Piola-Kirchhoff stress is [@problem_id:2641039]:
$$
\mathbf{P}^* = J^* \boldsymbol{\sigma}^* (\mathbf{F}^*)^{-T} = J (\mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T)(\mathbf{F}^{-T}\mathbf{Q}^T) = \mathbf{Q} (J \boldsymbol{\sigma}\mathbf{F}^{-T}) = \mathbf{Q}\mathbf{P}
$$
Since $\mathbf{P}^* \neq \mathbf{P}$, the first Piola-Kirchhoff stress is **not objective**. It rotates with the superposed rigid motion.

Now, consider the second Piola-Kirchhoff stress [@problem_id:2587891]:
$$
\mathbf{S}^* = (\mathbf{F}^*)^{-1}\mathbf{P}^* = (\mathbf{F}^{-1}\mathbf{Q}^{-1})(\mathbf{Q}\mathbf{P}) = \mathbf{F}^{-1}(\mathbf{Q}^{-1}\mathbf{Q})\mathbf{P} = \mathbf{F}^{-1}\mathbf{P} = \mathbf{S}
$$
The second Piola-Kirchhoff stress remains unchanged, $\mathbf{S}^* = \mathbf{S}$. It is therefore an **objective** tensor. This invariance is a primary reason for its widespread use in developing constitutive theories. Any physically realistic [strain energy function](@entry_id:170590) must depend on objective kinematic quantities, and the pair $(\mathbf{S}, \mathbf{E})$ satisfies this requirement, as both are objective.

A concrete calculation from problem [@problem_id:1549814] demonstrates this invariance. Given an initial deformation and stress state, one can calculate $\mathbf{S}$. If a rigid rotation $\mathbf{Q}$ is then applied, the new deformation is $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$ and the new Cauchy stress is $\boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T$. Computing the new second Piola-Kirchhoff stress $\mathbf{S}^* = J^* (\mathbf{F}^*)^{-1} \boldsymbol{\sigma}^* (\mathbf{F}^*)^{-T}$ will yield a result identical to the original $\mathbf{S}$, confirming its objectivity.

### Summary of Relations and Computational Aspects

The relationships between the various [stress measures](@entry_id:198799) can be summarized as a series of pull-back (from current to reference) and push-forward (from reference to current) operations [@problem_id:2887012]. Let $\boldsymbol{\tau} = J\boldsymbol{\sigma}$ be the Kirchhoff stress tensor.

- **From S to other measures (Push-forward):**
  - $\mathbf{P} = \mathbf{F}\mathbf{S}$
  - $\boldsymbol{\tau} = \mathbf{F}\mathbf{S}\mathbf{F}^T$
  - $\boldsymbol{\sigma} = \frac{1}{J}\mathbf{F}\mathbf{S}\mathbf{F}^T$

- **From $\boldsymbol{\sigma}$ to other measures (Pull-back):**
  - $\mathbf{P} = J\boldsymbol{\sigma}\mathbf{F}^{-T}$
  - $\mathbf{S} = J\boldsymbol{F}^{-1}\boldsymbol{\sigma}\mathbf{F}^{-T}$

These relations are fundamental to formulating and solving problems in [finite elasticity](@entry_id:181775). The [constitutive law](@entry_id:167255) is typically defined in the material frame as a relationship between $\mathbf{S}$ and a material strain measure like $\mathbf{E}$ (or equivalently, the right Cauchy-Green tensor $\mathbf{C} = \mathbf{F}^T\mathbf{F}$). For instance, for an isotropic [hyperelastic material](@entry_id:195319), the [strain energy](@entry_id:162699) is a function of the invariants of $\mathbf{C}$, which implies that the principal axes of $\mathbf{S}$ must coincide with the principal axes of $\mathbf{C}$ [@problem_id:2587891]. Once $\mathbf{S}$ is computed from the constitutive law, the other [stress measures](@entry_id:198799) needed for [equilibrium equations](@entry_id:172166) or post-processing can be found using the push-forward operations.

Finally, a critical physical constraint underpinning all of [continuum mechanics](@entry_id:155125) is the **impenetrability of matter**. This translates to the mathematical requirement that the local volume ratio must remain positive, $J = \det \mathbf{F} > 0$. A state where $J \le 0$ is non-physical, implying either infinite compression or a material element turning itself inside out. Physically meaningful [strain energy](@entry_id:162699) functions enforce this by construction, for example by including terms like $\ln J$, which create an infinite energy barrier as $J \to 0^+$ [@problem_id:2587867]. Consequently, both $\mathbf{P}$ and $\mathbf{S}$ are undefined for $J \le 0$. In computational methods like FEM, where iterative solvers may produce trial steps that violate this condition, robust algorithms employ strategies such as line searches or trust regions to ensure that all computed states remain in the physically admissible domain where $J > 0$.