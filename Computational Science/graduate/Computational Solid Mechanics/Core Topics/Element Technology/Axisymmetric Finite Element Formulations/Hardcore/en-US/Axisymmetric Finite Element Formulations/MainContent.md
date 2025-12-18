## Introduction
The axisymmetric [finite element formulation](@entry_id:164720) is a cornerstone of [computational solid mechanics](@entry_id:169583), offering an elegant and efficient method for analyzing three-dimensional bodies that possess rotational symmetry. By reducing the problem's dimensionality from three to two, it enables accurate and computationally inexpensive analysis of a vast range of engineering components, from pressure vessels and pipes to geotechnical foundations. However, this simplification is not trivial; it requires a specialized theoretical framework that correctly captures the unique kinematics and stress state, particularly the development of [hoop stress](@entry_id:190931), which fundamentally differentiates it from 2D [plane strain](@entry_id:167046) or [plane stress analysis](@entry_id:193362). This article bridges the gap between general 3D continuum mechanics and this powerful specialized technique.

This comprehensive guide will walk you through the theory, application, and implementation of axisymmetric finite elements. The first chapter, **Principles and Mechanisms**, establishes the theoretical foundation, detailing the kinematic assumptions, deriving the governing equations via the Principle of Virtual Work, and explaining the isoparametric [finite element discretization](@entry_id:193156). The second chapter, **Applications and Interdisciplinary Connections**, explores the method's versatility by showcasing its use in advanced [structural dynamics](@entry_id:172684), fracture mechanics, [geomechanics](@entry_id:175967), and [coupled multiphysics](@entry_id:747969) problems. Finally, the **Hands-On Practices** section provides targeted exercises to solidify understanding of key concepts like [hoop strain](@entry_id:174548), [numerical integration](@entry_id:142553), and [matrix conditioning](@entry_id:634316), preparing you to develop and apply robust axisymmetric models.

## Principles and Mechanisms

The formulation of finite elements for axisymmetric problems represents a powerful and efficient specialization of general three-dimensional [continuum mechanics](@entry_id:155125). By exploiting [rotational symmetry](@entry_id:137077), the dimensionality of the problem is reduced from three to two, leading to significant computational savings without loss of accuracy for an important class of engineering components, such as pressure vessels, pipes, rotating disks, and certain geotechnical structures. This chapter details the fundamental principles and mechanical formulations that underpin the axisymmetric finite element method.

### Kinematics of Axisymmetric Deformation

The cornerstone of an axisymmetric formulation is the kinematic simplification that arises from the assumption of rotational symmetry. In a [cylindrical coordinate system](@entry_id:266798) $(r, \theta, z)$, a problem is defined as **axisymmetric** if the geometry of the solid, its material properties, and the applied loads are all independent of the circumferential coordinate $\theta$. This symmetry in the problem's definition implies that the resulting response—the displacement, strain, and stress fields—must also be independent of $\theta$. Consequently, all [partial derivatives](@entry_id:146280) with respect to $\theta$ vanish, i.e., $\frac{\partial}{\partial \theta}(\cdot) = 0$.

In the simplest and most common case, known as pure axisymmetry, the loading is confined to meridional planes (planes of constant $\theta$). As a result, material points only displace radially and axially. The displacement vector $\mathbf{u}$ is thus simplified to:
$u_r = u_r(r, z)$
$u_z = u_z(r, z)$
$u_{\theta} = 0$

Starting from the general [small-strain tensor](@entry_id:754968) definitions in cylindrical coordinates, we can deduce the specific strain components for this kinematic state. The six components of the [small-strain tensor](@entry_id:754968) $\boldsymbol{\varepsilon}$ are:
$$ \varepsilon_{rr} = \frac{\partial u_r}{\partial r} $$
$$ \varepsilon_{\theta\theta} = \frac{1}{r}\frac{\partial u_{\theta}}{\partial \theta} + \frac{u_r}{r} $$
$$ \varepsilon_{zz} = \frac{\partial u_z}{\partial z} $$
$$ \varepsilon_{rz} = \frac{1}{2} \left( \frac{\partial u_r}{\partial z} + \frac{\partial u_z}{\partial r} \right) $$
$$ \varepsilon_{r\theta} = \frac{1}{2} \left( \frac{1}{r}\frac{\partial u_r}{\partial \theta} + \frac{\partial u_{\theta}}{\partial r} - \frac{u_{\theta}}{r} \right) $$
$$ \varepsilon_{\theta z} = \frac{1}{2} \left( \frac{\partial u_{\theta}}{\partial z} + \frac{1}{r}\frac{\partial u_z}{\partial \theta} \right) $$

Applying the axisymmetric conditions $u_\theta = 0$ and $\frac{\partial}{\partial \theta}(\cdot) = 0$, we find that the shear strains involving the circumferential direction, $\varepsilon_{r\theta}$ and $\varepsilon_{\theta z}$, become identically zero. However, four strain components remain potentially non-zero :
- **Radial Strain:** $\varepsilon_{rr} = \frac{\partial u_r}{\partial r}$
- **Axial Strain:** $\varepsilon_{zz} = \frac{\partial u_z}{\partial z}$
- **Meridional Shear Strain:** $\varepsilon_{rz} = \frac{1}{2} \left( \frac{\partial u_r}{\partial z} + \frac{\partial u_z}{\partial r} \right)$
- **Circumferential or Hoop Strain:** $\varepsilon_{\theta\theta} = \frac{u_r}{r}$

The existence of the **[hoop strain](@entry_id:174548)**, $\varepsilon_{\theta\theta}$, is a defining feature of the axisymmetric formulation and the primary point of distinction from a two-dimensional plane strain analysis in the $r-z$ plane. In plane strain, the out-of-plane strain is, by definition, zero. In axisymmetry, any radial displacement $u_r$ at a radius $r$ will stretch or compress the circumference of the material ring at that location. This change in circumference, normalized by the original circumference, is the [hoop strain](@entry_id:174548). For an initial circumference $C_0 = 2\pi r$, a radial displacement $u_r$ leads to a new circumference $C_f = 2\pi(r+u_r)$. The [hoop strain](@entry_id:174548) is thus $\varepsilon_{\theta\theta} = (C_f - C_0)/C_0 = u_r/r$. This strain is generally non-zero and gives rise to a corresponding non-zero **hoop stress**, $\sigma_{\theta\theta}$, which is crucial for equilibrium. For instance, in a pressurized cylinder, the hoop stress is the primary stress component resisting the [internal pressure](@entry_id:153696). Because of this, axisymmetry is fundamentally a three-dimensional stress state reduced to a two-dimensional geometric domain, not a true two-dimensional theory like plane stress or plane strain .

In some problems, such as the torsion of a shaft, a circumferential displacement $u_{\theta}(r,z)$ may exist while the problem remains axisymmetric (independent of $\theta$). This leads to an **axisymmetric-with-torsion** formulation, where the shear strains $\gamma_{r\theta} = 2\varepsilon_{r\theta}$ and $\gamma_{\theta z} = 2\varepsilon_{\theta z}$ can be non-zero .

### Governing Equations for Axisymmetric Analysis

To develop a finite element model, we must establish the governing equations in a form suitable for discretization. This involves defining the [weak form](@entry_id:137295) of equilibrium and the appropriate constitutive relationship.

#### The Principle of Virtual Work

The [weak form](@entry_id:137295) of the [equilibrium equations](@entry_id:172166) is given by the Principle of Virtual Work (PVW), which states that for any kinematically admissible [virtual displacement](@entry_id:168781) field $\delta\mathbf{u}$, the [internal virtual work](@entry_id:172278) equals the external [virtual work](@entry_id:176403). For a three-dimensional continuum, this is expressed as:
$$ \int_{V} \boldsymbol{\sigma}:\delta\boldsymbol{\varepsilon}\, \mathrm{d}V = \int_{V} \mathbf{b}\cdot \delta\mathbf{u}\, \mathrm{d}V + \int_{S_t} \mathbf{t}\cdot \delta\mathbf{u}\, \mathrm{d}S $$
where $\boldsymbol{\sigma}$ is the stress tensor, $\delta\boldsymbol{\varepsilon}$ is the virtual [strain tensor](@entry_id:193332), $\mathbf{b}$ is the [body force](@entry_id:184443) per unit volume, $\mathbf{t}$ is the traction vector on the surface $S_t$, and $V$ is the volume of the body.

For an axisymmetric body, we can simplify this 3D integral into a 2D integral over the meridional cross-section, which we denote $\Omega$. The key is to correctly express the differential [volume element](@entry_id:267802) $\mathrm{d}V$ and surface element $\mathrm{d}S$. In [cylindrical coordinates](@entry_id:271645), $\mathrm{d}V = r\,\mathrm{d}r\,\mathrm{d}\theta\,\mathrm{d}z$. A differential area in the meridional plane is $\mathrm{d}\Omega = \mathrm{d}r\,\mathrm{d}z$. Thus, $\mathrm{d}V = r\,\mathrm{d}\Omega\,\mathrm{d}\theta$. Since all integrands are independent of $\theta$ under axisymmetry, the integration over the circumference from $0$ to $2\pi$ can be performed directly:
$$ \int_V (\cdot) \,\mathrm{d}V = \int_{\Omega} \int_0^{2\pi} (\cdot) \, r\,\mathrm{d}\theta\,\mathrm{d}\Omega = \int_{\Omega} (\cdot) \, 2\pi r \,\mathrm{d}\Omega $$
A similar argument applies to the [surface integral](@entry_id:275394). A differential arc length $\mathrm{d}\Gamma$ on the boundary of the meridional section generates a differential surface area $\mathrm{d}S = r\,\mathrm{d}\Gamma\,\mathrm{d}\theta$ when revolved around the $z$-axis. Integrating over $\theta$ also yields a factor of $2\pi r$.

Therefore, the PVW for an axisymmetric body reduces to integrals over the 2D meridional domain $\Omega$ and its boundary $\Gamma_t$ :
$$ \int_{\Omega} (\boldsymbol{\sigma}:\delta\boldsymbol{\varepsilon}) \, 2\pi r \,\mathrm{d}\Omega = \int_{\Omega} (\mathbf{b}\cdot \delta\mathbf{u}) \, 2\pi r \,\mathrm{d}\Omega + \int_{\Gamma_t} (\mathbf{t}\cdot \delta\mathbf{u}) \, 2\pi r \,\mathrm{d}\Gamma $$
The factor $2\pi r$ is a geometric weight that accounts for the integration over the circumference and is a critical component of the axisymmetric [finite element formulation](@entry_id:164720).

#### Axisymmetric Constitutive Law

For an isotropic, linear elastic material, the 3D stress-strain relationship is given by Hooke's Law, often expressed using Lamé parameters $\lambda$ and $G$: $\sigma_{ij} = \lambda \operatorname{tr}(\boldsymbol{\varepsilon})\delta_{ij} + 2G\varepsilon_{ij}$. In an axisymmetric formulation, we have four relevant stress components ($\sigma_{rr}, \sigma_{zz}, \sigma_{\theta\theta}, \tau_{rz}$) and four corresponding strain components ($\varepsilon_{rr}, \varepsilon_{zz}, \varepsilon_{\theta\theta}, \gamma_{rz}=2\varepsilon_{rz}$). By expanding the 3D law for these components, we can derive the specific $4 \times 4$ [constitutive matrix](@entry_id:164908) $\mathbf{D}_{\text{axisym}}$ that relates the [stress and strain](@entry_id:137374) vectors .

Let the stress vector be $\boldsymbol{\sigma} = \begin{pmatrix} \sigma_{rr}  \sigma_{zz}  \sigma_{\theta\theta}  \tau_{rz} \end{pmatrix}^{\mathsf{T}}$ and the strain vector be $\boldsymbol{\epsilon} = \begin{pmatrix} \varepsilon_{rr}  \varepsilon_{zz}  \varepsilon_{\theta\theta}  \gamma_{rz} \end{pmatrix}^{\mathsf{T}}$. The relation is $\boldsymbol{\sigma} = \mathbf{D}_{\text{axisym}} \boldsymbol{\epsilon}$. The resulting matrix, expressed in terms of Young's modulus $E$ and Poisson's ratio $\nu$, is:
$$ \mathbf{D}_{\text{axisym}} = \frac{E}{(1+\nu)(1-2\nu)}
\begin{pmatrix}
1-\nu  \nu  \nu  0 \\
\nu  1-\nu  \nu  0 \\
\nu  \nu  1-\nu  0 \\
0  0  0  \frac{1-2\nu}{2}
\end{pmatrix} $$
It is important to note that this matrix is derived directly from the full 3D [constitutive law](@entry_id:167255) without a priori assumptions on stress components (unlike plane stress, where $\sigma_{zz}=0$ is enforced to reduce the material law). This again underscores the 3D nature of the stress state in axisymmetric problems .

### Isoparametric Finite Element Discretization

The continuous weak form is discretized using finite elements. The **isoparametric** formulation is standard, where the same set of [shape functions](@entry_id:141015) is used to interpolate both the element's geometry and the [displacement field](@entry_id:141476). For a 4-node [quadrilateral element](@entry_id:170172) in the $r-z$ plane, the mapping from the parent element domain $(\xi, \eta) \in [-1, 1] \times [-1, 1]$ to the physical domain and the interpolation of displacements are given by:
$$ r(\xi,\eta) = \sum_{i=1}^{4} N_i(\xi,\eta) r_i, \qquad z(\xi,\eta) = \sum_{i=1}^{4} N_i(\xi,\eta) z_i $$
$$ u_r(\xi,\eta) = \sum_{i=1}^{4} N_i(\xi,\eta) u_{ri}, \qquad u_z(\xi,\eta) = \sum_{i=1}^{4} N_i(\xi,\eta) u_{zi} $$
where $(r_i, z_i)$ are the nodal coordinates and $(u_{ri}, u_{zi})$ are the nodal displacement degrees of freedom .

#### The Strain-Displacement Matrix ($\mathbf{B}$)

The relationship between the element strain vector $\boldsymbol{\epsilon}$ and the element nodal displacement vector $\mathbf{d}_e$ is defined by the [strain-displacement matrix](@entry_id:163451) $\mathbf{B}$, such that $\boldsymbol{\epsilon} = \mathbf{B}\mathbf{d}_e$. We construct $\mathbf{B}$ by substituting the interpolated displacements into the strain definitions. For a 4-node element with nodal displacements ordered as $\mathbf{d}_e = [u_{r1}, u_{z1}, u_{r2}, u_{z2}, u_{r3}, u_{z3}, u_{r4}, u_{z4}]^{\mathsf{T}}$, the $4 \times 8$ matrix $\mathbf{B}$ is :
$$ \mathbf{B} = 
\begin{pmatrix}
\frac{\partial N_1}{\partial r}  0  \frac{\partial N_2}{\partial r}  0  \frac{\partial N_3}{\partial r}  0  \frac{\partial N_4}{\partial r}  0 \\
0  \frac{\partial N_1}{\partial z}  0  \frac{\partial N_2}{\partial z}  0  \frac{\partial N_3}{\partial z}  0  \frac{\partial N_4}{\partial z} \\
\frac{N_1}{r}  0  \frac{N_2}{r}  0  \frac{N_3}{r}  0  \frac{N_4}{r}  0 \\
\frac{\partial N_1}{\partial z}  \frac{\partial N_1}{\partial r}  \frac{\partial N_2}{\partial z}  \frac{\partial N_2}{\partial r}  \frac{\partial N_3}{\partial z}  \frac{\partial N_3}{\partial r}  \frac{\partial N_4}{\partial z}  \frac{\partial N_4}{\partial r}
\end{pmatrix}
$$
The derivatives of the shape functions with respect to physical coordinates, $\partial N_i / \partial r$ and $\partial N_i / \partial z$, are computed from their derivatives in the [parent domain](@entry_id:169388) using the inverse of the Jacobian matrix of the [coordinate mapping](@entry_id:156506). The third row, corresponding to the [hoop strain](@entry_id:174548) $\varepsilon_{\theta\theta} = u_r/r$, is a unique feature. It contains the shape functions themselves, not their derivatives, and is inversely proportional to the radius $r$. For instance, at the center of a bilinear element where $(\xi, \eta) = (0,0)$ and $N_i = 1/4$ for all $i$, the [hoop strain](@entry_id:174548) evaluates to the ratio of the average nodal radial displacement to the average nodal radius: $\varepsilon_{\theta\theta}(0,0) = \frac{\sum u_{ri}}{\sum r_i}$ .

#### The Element Stiffness Matrix and Numerical Integration

Substituting the discretized quantities into the PVW yields the [element stiffness matrix](@entry_id:139369) $\mathbf{K}_e$:
$$ \mathbf{K}_e = \int_{\Omega_e} \mathbf{B}^{\mathsf{T}} \mathbf{D}_{\text{axisym}} \mathbf{B} \, 2\pi r \,\mathrm{d}\Omega $$
This integral is evaluated numerically using Gauss quadrature. The integral is first transformed to the [parent domain](@entry_id:169388), where $\mathrm{d}\Omega = \det(\mathbf{J})\,\mathrm{d}\xi\,\mathrm{d}\eta$, with $\mathbf{J}$ being the Jacobian of the mapping from $(\xi, \eta)$ to $(r,z)$. The final quadrature formula for the [stiffness matrix](@entry_id:178659) is a weighted sum over the Gauss points $(\xi_i, \eta_i)$  :
$$ \mathbf{K}_e \approx \sum_{i} w_i \left( \mathbf{B}(\xi_i, \eta_i)^{\mathsf{T}} \mathbf{D}_{\text{axisym}} \mathbf{B}(\xi_i, \eta_i) \right) 2\pi r(\xi_i, \eta_i) \det(\mathbf{J}(\xi_i, \eta_i)) $$
where $w_i$ are the Gauss weights. Critically, the radius $r$ and the Jacobian determinant $\det(\mathbf{J})$ are evaluated at each Gauss point, reflecting their variation across the element. The term $2\pi r(\xi_i, \eta_i)$ is part of the quadrature weight, stemming directly from the geometry of revolution, and is distinct from the Jacobian determinant $\det(\mathbf{J})$, which only accounts for the mapping distortion within the meridional plane .

### Advanced Topics and Implementation Details

#### Conditions at the Axis of Symmetry ($r=0$)

A crucial implementation detail is the treatment of the axis of symmetry at $r=0$. The presence of $1/r$ in the [hoop strain](@entry_id:174548) definition $\varepsilon_{\theta\theta} = u_r/r$ and in the [equilibrium equations](@entry_id:172166) indicates a [coordinate singularity](@entry_id:159160). For the strain and stress fields to remain finite and physically meaningful, certain **regularity conditions** must be met.

From considerations of geometric continuity, the displacement field must be smooth across the $z$-axis. This implies that the radial displacement must be an [odd function](@entry_id:175940) of $r$ and the axial displacement must be an [even function](@entry_id:164802) of $r$. These symmetry arguments lead to two essential kinematic conditions at $r=0$:
1.  $u_r(0, z) = 0$
2.  $\frac{\partial u_z}{\partial r}(0, z) = 0$

The first condition ensures that no hole or overlap opens up at the axis. This condition is sufficient to ensure the [hoop strain](@entry_id:174548) remains finite. Applying L'Hôpital's rule, we find that the [hoop strain](@entry_id:174548) at the axis becomes equal to the radial strain:
$$ \lim_{r \to 0} \varepsilon_{\theta\theta} = \lim_{r \to 0} \frac{u_r}{r} = \frac{\partial u_r}{\partial r}\bigg|_{r=0} = \varepsilon_{rr}(0,z) $$
For an isotropic material, this equality of strains implies an equality of stresses: $\sigma_{rr}(0,z) = \sigma_{\theta\theta}(0,z)$.

In a finite element implementation, the condition $u_r(0,z)=0$ is enforced as an essential (Dirichlet) boundary condition on all nodes that lie on the [axis of symmetry](@entry_id:177299) ($r=0$). The axial displacement $u_z$ at these nodes is left free, as axial motion is physically permissible. It is important to recognize that the axis is not a physical boundary where tractions are applied; the surface area of the axis is zero. Therefore, no [traction boundary conditions](@entry_id:167112) are specified at $r=0$ .

#### Volumetric Locking in Nearly Incompressible Materials

When modeling [nearly incompressible materials](@entry_id:752388) (where Poisson's ratio $\nu \to 0.5$, or the [bulk modulus](@entry_id:160069) $K$ is much larger than the [shear modulus](@entry_id:167228) $G$), standard displacement-based [axisymmetric elements](@entry_id:163652) can suffer from **[volumetric locking](@entry_id:172606)**. This numerical artifact manifests as an overly stiff response, yielding strains and displacements that are erroneously small.

The phenomenon arises from the penalty-like enforcement of the [incompressibility constraint](@entry_id:750592), $\varepsilon_v = \varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta} \approx 0$. In a standard, fully integrated element, the formulation attempts to satisfy this constraint at each Gauss point. However, the kinematic freedom of a low-order element (like a bilinear quadrilateral) is insufficient to satisfy this constraint at multiple points simultaneously for arbitrary deformations. The complex form of the volumetric strain, $\varepsilon_v = \frac{\partial u_r}{\partial r} + \frac{\partial u_z}{\partial z} + \frac{u_r}{r}$, poses a particularly severe constraint on the interpolated displacement field. The element 'locks up' because any physically reasonable deformation generates some [volumetric strain](@entry_id:267252), which is then heavily penalized by the large [bulk modulus](@entry_id:160069) $K$, leading to an artificially high stiffness.

To remedy this, **mixed displacement-pressure ($u-p$) formulations** are employed. In this approach, the hydrostatic pressure $p$ is introduced as an independent field variable. The pressure acts as a Lagrange multiplier that enforces the [incompressibility constraint](@entry_id:750592) in a weak, integral sense, rather than pointwise. This leads to a saddle-point system of equations that avoids the large penalty term in the [stiffness matrix](@entry_id:178659). For such a formulation to be stable and accurate, the interpolation spaces for displacement and pressure must satisfy the Ladyzhenskaya–Babuška–Brezzi (LBB) or inf-sup condition, which typically requires using a higher-order interpolation for displacements than for pressure .