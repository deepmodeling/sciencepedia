## Introduction
In the study of [computational geomechanics](@entry_id:747617), understanding how materials like soil and rock deform under load is paramount. While the overall movement of a body is described by its displacement field, the internal changes in shape and size—the very phenomena that generate stress and lead to failure—are captured by the concept of strain. The fundamental challenge lies in establishing a precise mathematical link between the macroscopic displacement of material points and the localized deformation they experience. This article addresses this foundational knowledge gap by systematically deriving the principles of [infinitesimal strain](@entry_id:197162) and the [strain-displacement relations](@entry_id:173321).

The following chapters are structured to guide the reader from first principles to advanced applications.
- **Principles and Mechanisms** will establish the theoretical groundwork, starting with the [displacement gradient tensor](@entry_id:748571) and decomposing it into the [infinitesimal strain](@entry_id:197162) and rotation tensors. We will explore the physical meaning of each strain component and introduce critical concepts such as volumetric strain, [strain invariants](@entry_id:190518), and the compatibility equations that ensure a physically possible deformation.
- **Applications and Interdisciplinary Connections** will demonstrate the power of this theory by exploring its use in geomechanics, the interpretation of laboratory experiments, and its central role in the Finite Element Method (FEM). We will also examine how strain acts as a key coupling variable in multiphysics problems like [poroelasticity](@entry_id:174851) and [thermoelasticity](@entry_id:158447).
- **Hands-On Practices** will offer a series of computational exercises designed to solidify these concepts, bridging the gap between theoretical knowledge and practical implementation in geomechanics analysis.

This structure will provide a comprehensive understanding of how strain is defined, calculated, and applied, forming an indispensable cornerstone for further study in [continuum mechanics](@entry_id:155125) and computational modeling.

## Principles and Mechanisms

The motion of a continuum, such as a soil or rock mass, is described by a displacement field, $\mathbf{u}$, which maps each material point from its initial position, $\mathbf{x}$, to its current position, $\mathbf{x}' = \mathbf{x} + \mathbf{u}(\mathbf{x})$. While the displacement field itself describes the overall translation and deformation of the body, the local changes in shape and size—the quantities directly related to stress and [material failure](@entry_id:160997)—are governed by the spatial derivatives of this field. This chapter elucidates the fundamental principles that connect displacement to strain and introduces the kinematic mechanisms that define deformation.

### The Displacement Gradient Tensor

The cornerstone for describing local kinematics is the **[displacement gradient tensor](@entry_id:748571)**, a second-order tensor denoted by $\mathbf{H}$ or $\nabla \mathbf{u}$. Its components in a Cartesian coordinate system are given by $H_{ij} = \frac{\partial u_i}{\partial x_j}$. This tensor contains all the information about the local, first-order transformation of the material.

To understand its role, consider an infinitesimal material line element, $d\mathbf{x}$, in the reference configuration. Under the deformation, this element is mapped to a new line element, $d\mathbf{x}'$. By applying the differential of the mapping function, we find the relationship:

$d\mathbf{x}' = \frac{\partial \mathbf{x}'}{\partial \mathbf{x}} d\mathbf{x} = \frac{\partial (\mathbf{x} + \mathbf{u})}{\partial \mathbf{x}} d\mathbf{x} = \left(\frac{\partial \mathbf{x}}{\partial \mathbf{x}} + \frac{\partial \mathbf{u}}{\partial \mathbf{x}}\right) d\mathbf{x} = (\mathbf{I} + \nabla \mathbf{u}) d\mathbf{x}$

Here, $\mathbf{I}$ is the identity tensor. This fundamental result, $d\mathbf{x}' = (\mathbf{I} + \mathbf{H}) d\mathbf{x}$, shows that the [displacement gradient tensor](@entry_id:748571) governs the linear transformation of infinitesimal line elements. The key question in [kinematics](@entry_id:173318) is how to dissect this transformation to distinguish between true deformation (changes in length and angle) and mere [rigid-body motion](@entry_id:265795) (translation and rotation). 

### Decomposition: Infinitesimal Strain and Rotation

Any second-order tensor can be uniquely decomposed into the sum of a symmetric part and a skew-symmetric (or antisymmetric) part. Applying this mathematical decomposition to the [displacement gradient tensor](@entry_id:748571) $\mathbf{H}$ provides profound physical insight.

We define the **[infinitesimal strain tensor](@entry_id:167211)**, $\boldsymbol{\varepsilon}$, as the symmetric part of $\mathbf{H}$:
$$ \boldsymbol{\varepsilon} = \frac{1}{2}(\mathbf{H} + \mathbf{H}^T) = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^T) $$

In component form, this is written as:
$$ \varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i}) $$

Conversely, we define the **[infinitesimal rotation tensor](@entry_id:192754)**, $\boldsymbol{\omega}$, as the skew-symmetric part of $\mathbf{H}$:
$$ \boldsymbol{\omega} = \frac{1}{2}(\mathbf{H} - \mathbf{H}^T) = \frac{1}{2}(\nabla \mathbf{u} - (\nabla \mathbf{u})^T) $$

In component form:
$$ \omega_{ij} = \frac{1}{2}(u_{i,j} - u_{j,i}) $$

The [displacement gradient](@entry_id:165352) is thus the sum of these two tensors, $\mathbf{H} = \boldsymbol{\varepsilon} + \boldsymbol{\omega}$, separating the [kinematics](@entry_id:173318) into a deformative part and a rotational part. 

To illustrate this, consider a general linear displacement field, often used to approximate the kinematics within a single finite element: $\mathbf{u}(\mathbf{x}) = \mathbf{a} + \mathbf{B}\mathbf{x}$. Here, $\mathbf{a}$ is a constant vector representing a uniform **rigid-body translation**, and $\mathbf{B}$ is a constant tensor. The [displacement gradient](@entry_id:165352) is simply $\nabla \mathbf{u} = \mathbf{B}$. The motion is decomposed by calculating the symmetric and skew-symmetric parts of $\mathbf{B}$. For instance, for a matrix such as $\mathbf{B}=\begin{pmatrix} 0  2  -1 \\ -1  0  3 \\ 4  -2  1 \end{pmatrix}$, the [infinitesimal strain](@entry_id:197162) and rotation tensors are found to be: 

$$ \boldsymbol{\varepsilon} = \frac{1}{2}(\mathbf{B} + \mathbf{B}^T) = \begin{pmatrix} 0  \frac{1}{2}  \frac{3}{2} \\ \frac{1}{2}  0  \frac{1}{2} \\ \frac{3}{2}  \frac{1}{2}  1 \end{pmatrix} $$

$$ \boldsymbol{\omega} = \frac{1}{2}(\mathbf{B} - \mathbf{B}^T) = \begin{pmatrix} 0  \frac{3}{2}  -\frac{5}{2} \\ -\frac{3}{2}  0  \frac{5}{2} \\ \frac{5}{2}  -\frac{5}{2}  0 \end{pmatrix} $$

The tensor $\boldsymbol{\varepsilon}$ captures the pure deformation, while $\boldsymbol{\omega}$ captures the local [rigid-body rotation](@entry_id:268623). A pure [rigid-body motion](@entry_id:265795), described by a displacement field like $\mathbf{u}(\mathbf{x}) = \boldsymbol{\Omega}\mathbf{x} + \mathbf{c}$ where $\boldsymbol{\Omega}$ is a constant [skew-symmetric tensor](@entry_id:199349), correctly yields a zero [infinitesimal strain tensor](@entry_id:167211) ($\boldsymbol{\varepsilon}=\mathbf{0}$) and an [infinitesimal rotation tensor](@entry_id:192754) equal to $\boldsymbol{\Omega}$ ($\boldsymbol{\omega}=\boldsymbol{\Omega}$), confirming the physical meaning of the decomposition. 

### Physical Interpretation of Strain Components

The power of the [strain tensor](@entry_id:193332) lies in its direct connection to physical measures of deformation. Let's examine the change in squared length, $ds^2$, of an infinitesimal [line element](@entry_id:196833) $d\mathbf{x}$. The initial squared length is $ds^2 = d\mathbf{x}^T d\mathbf{x}$. The new squared length is $ds'^2 = d\mathbf{x}'^T d\mathbf{x}'$. Using the mapping $d\mathbf{x}' \approx (\mathbf{I} + \mathbf{H}) d\mathbf{x}$ and neglecting terms quadratic in $\mathbf{H}$ (a step valid for small deformations), we find:

$ds'^2 \approx ((\mathbf{I} + \mathbf{H}) d\mathbf{x})^T ((\mathbf{I} + \mathbf{H}) d\mathbf{x}) = d\mathbf{x}^T (\mathbf{I} + \mathbf{H}^T)(\mathbf{I} + \mathbf{H}) d\mathbf{x} \approx d\mathbf{x}^T (\mathbf{I} + \mathbf{H}^T + \mathbf{H}) d\mathbf{x}$

The change in squared length is therefore $ds'^2 - ds^2 \approx d\mathbf{x}^T (\mathbf{H}^T + \mathbf{H}) d\mathbf{x} = 2 d\mathbf{x}^T \boldsymbol{\varepsilon} d\mathbf{x}$. The skew-symmetric part $\boldsymbol{\omega}$ makes no contribution. The **fractional change in length** for a [line element](@entry_id:196833) of initial unit direction $\mathbf{n}$ is found to be $\frac{ds' - ds}{ds} \approx \mathbf{n}^T \boldsymbol{\varepsilon} \mathbf{n}$. 

This leads to the direct physical interpretation of the [strain tensor](@entry_id:193332)'s components:
-   **Normal Strains**: The diagonal components, such as $\varepsilon_{xx} = \mathbf{e}_x^T \boldsymbol{\varepsilon} \mathbf{e}_x$, represent the fractional change in length of line elements oriented along the coordinate axes.
-   **Shear Strains**: The off-diagonal components govern the change in angles between line elements. A detailed derivation shows that the change in the angle between two initially orthogonal material lines is determined exclusively by the off-diagonal components of $\boldsymbol{\varepsilon}$. The [rotation tensor](@entry_id:191990) $\boldsymbol{\omega}$ rotates both lines together, preserving the relative angle between them. 

A common point of ambiguity is the distinction between tensorial and engineering [shear strain](@entry_id:175241). The **tensorial [shear strain](@entry_id:175241)** components are simply the off-diagonal elements of $\boldsymbol{\varepsilon}$, such as $\varepsilon_{xy}$. The **engineering [shear strain](@entry_id:175241)**, denoted $\gamma_{xy}$, is defined as the total decrease in the angle between two lines initially along the $x$ and $y$ axes. A first-principles derivation shows that for small deformations, $\gamma_{xy} \approx u_{x,y} + u_{y,x}$.  Comparing this with the definition $\varepsilon_{xy} = \frac{1}{2}(u_{x,y} + u_{y,x})$, we arrive at the crucial kinematic relationship:
$$ \gamma_{ij} = 2\varepsilon_{ij} \quad (\text{for } i \neq j) $$
This relationship is a matter of definition and geometry, independent of any material properties.

### Strain-Displacement Relations and Volumetric Strain

The definitions above can be written out explicitly as the six independent **[strain-displacement relations](@entry_id:173321)** in Cartesian coordinates:

$$ \varepsilon_{xx} = \frac{\partial u_x}{\partial x} $$
$$ \varepsilon_{yy} = \frac{\partial u_y}{\partial y} $$
$$ \varepsilon_{zz} = \frac{\partial u_z}{\partial z} $$
$$ \varepsilon_{xy} = \frac{1}{2}\left(\frac{\partial u_x}{\partial y} + \frac{\partial u_y}{\partial x}\right) $$
$$ \varepsilon_{xz} = \frac{1}{2}\left(\frac{\partial u_x}{\partial z} + \frac{\partial u_z}{\partial x}\right) $$
$$ \varepsilon_{yz} = \frac{1}{2}\left(\frac{\partial u_y}{\partial z} + \frac{\partial u_z}{\partial y}\right) $$

Given any displacement field, these equations allow for the direct computation of the strain state. For example, for a field containing both deformative and rotational parts, such as $u_x = 0.02x + 0.015y + (0.01+\theta)z$ and $u_z = -\theta x + 0.004y + 0.03z$, the rotational component $\theta$ appears in the [displacement gradient](@entry_id:165352) ($u_{x,z} = 0.01+\theta$, $u_{z,x} = -\theta$) but is eliminated from the strain component $\varepsilon_{xz}$ due to the symmetrization process. 

A particularly important scalar measure derived from the strain tensor is the **[volumetric strain](@entry_id:267252)**, $\varepsilon_v$, defined as the trace of the strain tensor:
$$ \varepsilon_v = \text{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{xx} + \varepsilon_{yy} + \varepsilon_{zz} = \frac{\partial u_x}{\partial x} + \frac{\partial u_y}{\partial y} + \frac{\partial u_z}{\partial z} = \nabla \cdot \mathbf{u} $$
The [volumetric strain](@entry_id:267252) represents the infinitesimal change in volume per unit volume. 

### Deviatoric Strain and Strain Invariants

The total strain $\boldsymbol{\varepsilon}$ can be decomposed into a part that causes volume change (isotropic) and a part that causes shape change or distortion (deviatoric). The **[deviatoric strain](@entry_id:201263) tensor**, denoted $\mathbf{s}$ or $\mathbf{e}$, is defined by removing the isotropic part from the total strain:
$$ \mathbf{s} = \boldsymbol{\varepsilon} - \frac{1}{3}\varepsilon_v \mathbf{I} $$
where $\varepsilon_v = \text{tr}(\boldsymbol{\varepsilon})$ and $\mathbf{I}$ is the identity tensor. By construction, the [deviatoric strain](@entry_id:201263) tensor is traceless ($\text{tr}(\mathbf{s})=0$), signifying that it represents deformation at constant volume. 

To characterize a strain state independently of the coordinate system used, one can compute its **[strain invariants](@entry_id:190518)**. These are scalar quantities derived from the tensor's components that remain unchanged under [coordinate rotation](@entry_id:164444). A particularly significant invariant in [geomechanics](@entry_id:175967) and [plasticity theory](@entry_id:177023) is the **second invariant of the [deviatoric strain](@entry_id:201263) tensor**, $J_2$:
$$ J_2 = \frac{1}{2}\mathbf{s}:\mathbf{s} = \frac{1}{2}s_{ij}s_{ij} $$
Here, the double-dot product indicates the sum of the squares of all components of the tensor. This invariant is related to the elastic shear or [distortion energy](@entry_id:198925) stored in the material and is a key ingredient in many [yield criteria](@entry_id:178101). Its computation, following from a given displacement field, involves a systematic procedure: calculate $\nabla \mathbf{u}$, find $\boldsymbol{\varepsilon}$, compute $\varepsilon_v$, construct $\mathbf{s}$, and finally compute $J_2$.  

### The Tensorial Nature of Strain

The statement that strain is a second-order tensor is not merely a classification; it prescribes how its components must transform under a change of basis. For a passive rotation of the coordinate system described by an orthogonal matrix $\mathbf{Q}$ (where the new basis vectors are $\mathbf{e}'_i = Q_{ij}\mathbf{e}_j$), the components of the strain tensor in the new system, $\boldsymbol{\varepsilon}'$, are related to the old components, $\boldsymbol{\varepsilon}$, by the transformation law:
$$ \boldsymbol{\varepsilon}' = \mathbf{Q} \boldsymbol{\varepsilon} \mathbf{Q}^T $$
This rule is essential for expressing strain in a coordinate system that is aligned with principal stress directions or geological features. 

For example, given a 2D strain state $\boldsymbol{\varepsilon} = \begin{pmatrix} a  b \\ b  d \end{pmatrix}$ and a counter-clockwise rotation of the axes by an angle $\theta$, the new shear component $\varepsilon'_{12}$ can be calculated using this rule. For a rotation of $\theta = 30^\circ$, one would use the matrix $\mathbf{Q} = \begin{pmatrix} \cos 30^\circ  \sin 30^\circ \\ -\sin 30^\circ  \cos 30^\circ \end{pmatrix}$ to find the transformed components. The calculation yields $\varepsilon'_{12} = \frac{a-d}{2}\sin(2\theta) + b\cos(2\theta)$, demonstrating how the components mix under rotation. 

### Theoretical Foundations and Limitations

#### The Infinitesimal Strain Assumption

The entire framework presented here is based on the **[infinitesimal strain](@entry_id:197162) assumption**. It is crucial to understand the limits of this approximation. The "exact" measure of strain for large deformations is the **Green-Lagrange [strain tensor](@entry_id:193332)**, $\mathbf{E} = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I})$, where $\mathbf{F} = \mathbf{I} + \nabla \mathbf{u}$ is the [deformation gradient](@entry_id:163749). Substituting the expression for $\mathbf{F}$, we can relate the finite and [infinitesimal strain](@entry_id:197162) measures:

$$ \mathbf{E} = \frac{1}{2}((\mathbf{I}+\mathbf{H})^T(\mathbf{I}+\mathbf{H}) - \mathbf{I}) = \frac{1}{2}(\mathbf{H}+\mathbf{H}^T + \mathbf{H}^T\mathbf{H}) = \boldsymbol{\varepsilon} + \frac{1}{2}\mathbf{H}^T\mathbf{H} $$

The [infinitesimal strain tensor](@entry_id:167211) $\boldsymbol{\varepsilon}$ is a valid first-order approximation to $\mathbf{E}$ only if the quadratic term $\frac{1}{2}\mathbf{H}^T\mathbf{H}$ is negligible compared to the linear term $\boldsymbol{\varepsilon}$. This requires that the norm of the [displacement gradient tensor](@entry_id:748571) itself must be small, i.e., $\|\mathbf{H}\| \ll 1$. Since $\|\mathbf{H}\|^2 = \|\boldsymbol{\varepsilon}\|^2 + \|\boldsymbol{\omega}\|^2$, this condition implies that **both the infinitesimal strains and the [infinitesimal rotations](@entry_id:166635) must be small**. A common misconception is that the theory applies to scenarios of small strain but arbitrarily large rotation; this is false. The [infinitesimal strain tensor](@entry_id:167211) is not objective under finite rotations, and the [linearization](@entry_id:267670) breaks down. 

#### Strain Compatibility

A final, profound question arises in continuum mechanics: if one is given a smooth, [symmetric tensor](@entry_id:144567) field $\boldsymbol{\varepsilon}(\mathbf{x})$, does it represent a physically possible deformation? That is, does a single-valued, continuous [displacement field](@entry_id:141476) $\mathbf{u}(\mathbf{x})$ exist that generates this strain field via the [strain-displacement relations](@entry_id:173321)?

The answer is not always yes. For a strain field to be integrable to a valid displacement field, its components must satisfy a set of differential constraints known as the **Saint-Venant compatibility equations**. In [index notation](@entry_id:191923), for a three-dimensional body, these are:
$$ \varepsilon_{ij,kl} + \varepsilon_{kl,ij} - \varepsilon_{ik,jl} - \varepsilon_{jl,ik} = 0 $$
This expression must hold for all combinations of indices $(i,j,k,l)$. These equations are a necessary consequence of the assumed smoothness of the [displacement field](@entry_id:141476) (i.e., that [mixed partial derivatives](@entry_id:139334) commute, e.g., $u_{i,jk} = u_{i,kj}$). For a [simply connected domain](@entry_id:197423) (one without holes), these conditions are also sufficient to guarantee the existence of a single-valued [displacement field](@entry_id:141476), unique up to a [rigid-body motion](@entry_id:265795). These equations ensure that a proposed strain field does not contain "gaps" or "overlaps" when integrated. They are purely kinematic conditions, independent of material properties or forces. 