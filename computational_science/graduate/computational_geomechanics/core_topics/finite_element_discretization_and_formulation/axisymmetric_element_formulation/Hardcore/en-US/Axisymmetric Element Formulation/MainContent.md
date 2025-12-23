## Introduction
The axisymmetric element formulation stands as a cornerstone of [computational mechanics](@entry_id:174464), offering a powerful method to simplify complex three-dimensional problems into a more computationally tractable two-dimensional domain. By exploiting rotational symmetry in geometry, material properties, and loading, engineers and scientists can achieve accurate solutions with significantly reduced computational cost. However, this simplification is not trivial; it rests on specific kinematic assumptions and requires a nuanced numerical implementation that differs fundamentally from plane stress or [plane strain](@entry_id:167046) conditions. A thorough understanding of these principles is crucial for the correct application and interpretation of results in fields like [computational geomechanics](@entry_id:747617).

This article provides a comprehensive guide to the theory and practice of the axisymmetric element formulation. We will bridge the gap between the abstract concept of axisymmetry and its concrete implementation within the Finite Element Method (FEM). You will gain a deep understanding of the unique mechanical behaviors, numerical challenges, and vast application potential of this essential analytical tool.

The journey begins in the "Principles and Mechanisms" chapter, where we will deconstruct the formulation from its kinematic foundations, exploring the critical role of [hoop strain](@entry_id:174548) and its effect on the constitutive response. We will then detail its integration into the FEM framework, covering the variational form, the unique [strain-displacement matrix](@entry_id:163451), and special considerations for numerical integration and handling singularities at the axis of symmetry. Following this, the "Applications and Interdisciplinary Connections" chapter will showcase the formulation's versatility by exploring its use in core geotechnical problems, dynamic analyses, and advanced coupled multi-[physics simulations](@entry_id:144318) involving fluid flow, heat, and chemical processes. Finally, the "Hands-On Practices" section offers targeted implementation exercises, allowing you to solidify your understanding by tackling practical challenges like the patch test and volumetric locking.

## Principles and Mechanisms

The axisymmetric formulation represents a powerful analytical and computational tool, enabling the reduction of a class of three-dimensional problems into a more tractable two-dimensional framework. This simplification is not merely a geometric convenience; it rests upon specific kinematic assumptions that give rise to unique mechanical behaviors and require careful consideration in their numerical implementation. This chapter elucidates the fundamental principles governing the axisymmetric formulation, from its kinematic origins to the nuances of its implementation within the Finite Element Method (FEM).

### Kinematic Foundations of Axisymmetry

An axisymmetric problem is one where the geometry of the body, its material properties, and the applied loads and boundary conditions are all symmetric with respect to an axis, which we define as the $z$-axis in a [cylindrical coordinate system](@entry_id:266798) $(r, \theta, z)$. This symmetry implies that the resulting deformation and stress fields must also be independent of the circumferential coordinate $\theta$. Consequently, all partial derivatives with respect to $\theta$ vanish, i.e., $\partial(\cdot)/\partial\theta = 0$.

Furthermore, for a standard axisymmetric analysis (as opposed to torsional problems), there are no applied forces that would induce a twisting or circumferential motion. This leads to the fundamental kinematic assumption that the circumferential component of the displacement vector is zero everywhere: $u_\theta = 0$. The [displacement field](@entry_id:141476) is therefore fully described by the radial and axial components, which are functions of $r$ and $z$ only:

$\boldsymbol{u}(r, z) = (u_r(r, z), 0, u_z(r, z))$

To understand the mechanical consequences of this assumption, we examine the [small-strain tensor](@entry_id:754968) components in [cylindrical coordinates](@entry_id:271645). The general expressions are:

$\varepsilon_{rr} = \frac{\partial u_r}{\partial r}$

$\varepsilon_{\theta\theta} = \frac{1}{r}\frac{\partial u_\theta}{\partial \theta} + \frac{u_r}{r}$

$\varepsilon_{zz} = \frac{\partial u_z}{\partial z}$

$\gamma_{rz} = 2\varepsilon_{rz} = \frac{\partial u_z}{\partial r} + \frac{\partial u_r}{\partial z}$

$\gamma_{r\theta} = 2\varepsilon_{r\theta} = \frac{1}{r}\frac{\partial u_r}{\partial \theta} + \frac{\partial u_\theta}{\partial r} - \frac{u_\theta}{r}$

$\gamma_{\theta z} = 2\varepsilon_{\theta z} = \frac{\partial u_\theta}{\partial z} + \frac{1}{r}\frac{\partial u_z}{\partial \theta}$

Applying the axisymmetric conditions ($\partial(\cdot)/\partial\theta = 0$ and $u_\theta = 0$) simplifies this set of relations considerably . The shear strains involving the circumferential direction vanish entirely: $\gamma_{r\theta} = 0$ and $\gamma_{\theta z} = 0$. The remaining four strain components are generally non-zero:

$\varepsilon_{rr} = \frac{\partial u_r}{\partial r}$

$\varepsilon_{zz} = \frac{\partial u_z}{\partial z}$

$\gamma_{rz} = \frac{\partial u_z}{\partial r} + \frac{\partial u_r}{\partial z}$

$\varepsilon_{\theta\theta} = \frac{u_r}{r}$

The first three are the in-plane strains within the meridional $(r,z)$ plane. The fourth, the **[hoop strain](@entry_id:174548)** $\varepsilon_{\theta\theta}$, is a crucial feature of the axisymmetric formulation. It represents the stretching of a circumferential material fiber due to a radial displacement $u_r$. Its presence signifies that even though the problem is modeled in a 2D domain, the out-of-plane deformation is not zero; it is intrinsically coupled to the in-plane radial motion. This distinguishes the axisymmetric state from plane strain, where the out-of-plane [normal strain](@entry_id:204633) is constrained to be zero. Imposing a plane strain condition ($\varepsilon_{\theta\theta}=0$) on an axisymmetric problem would require $u_r/r=0$, which implies $u_r=0$ for all $r>0$, an overly restrictive constraint that is physically incorrect for most problems .

### The Role of Hoop Strain in Constitutive Response

The presence of the non-zero [hoop strain](@entry_id:174548) has a profound effect on the stress state and the apparent stiffness of the material . For a linear, isotropic, elastic material described by Hooke's Law, the stress components are related to the strain components via the Lamé parameters $(\lambda, G)$ or, equivalently, Young's modulus $E$ and Poisson's ratio $\nu$. The normal stresses are given by:

$\sigma_{ij} = \lambda \varepsilon_v \delta_{ij} + 2G \varepsilon_{ij}$

where $\varepsilon_v = \text{tr}(\boldsymbol{\varepsilon})$ is the volumetric strain. In an axisymmetric formulation, the [volumetric strain](@entry_id:267252) includes the [hoop strain](@entry_id:174548):

$\varepsilon_v = \varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta}$

The [normal stresses](@entry_id:260622) are therefore:

$\sigma_{rr} = \lambda(\varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta}) + 2G \varepsilon_{rr}$

$\sigma_{zz} = \lambda(\varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta}) + 2G \varepsilon_{zz}$

$\sigma_{\theta\theta} = \lambda(\varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta}) + 2G \varepsilon_{\theta\theta}$

This coupling demonstrates that the [hoop strain](@entry_id:174548) $\varepsilon_{\theta\theta}$ contributes to all three [normal stress](@entry_id:184326) components, not just the [hoop stress](@entry_id:190931) $\sigma_{\theta\theta}$. A radial displacement $u_r$ generates a [hoop strain](@entry_id:174548) $\varepsilon_{\theta\theta}$, which in turn contributes to the [radial stress](@entry_id:197086) $\sigma_{rr}$ and axial stress $\sigma_{zz}$ through the volumetric term $\lambda \varepsilon_v$. This effect can be visualized as the material's resistance to being stretched or compressed circumferentially, which acts to restrain radial motion. Consequently, an axisymmetric body generally exhibits a higher apparent stiffness compared to a corresponding plane strain body subjected to the same in-plane deformations .

### Variational Formulation and the Axisymmetric Weighting Factor

The finite element method is built upon a weak, or variational, formulation of the governing [equilibrium equations](@entry_id:172166), typically derived from the Principle of Virtual Work. The [internal virtual work](@entry_id:172278) (IVW) is expressed as an integral over the body's volume $V$:

$\text{IVW} = \int_V \delta\boldsymbol{\varepsilon} : \boldsymbol{\sigma} \, dV$

To evaluate this integral for an axisymmetric body, we must express the differential volume element $dV$ in cylindrical coordinates. The transformation from Cartesian coordinates $(x,y,z)$ to [cylindrical coordinates](@entry_id:271645) $(r,\theta,z)$ is given by $x = r \cos\theta$, $y = r \sin\theta$, $z = z$. The differential [volume element](@entry_id:267802) is transformed using the determinant of the Jacobian of this mapping, which is found to be $r$. Thus, $dV = r \, dr \, d\theta \, dz$.

The IVW integral becomes:

$\text{IVW} = \int_{z_{min}}^{z_{max}} \int_{r_{min}}^{r_{max}} \int_0^{2\pi} (\delta\boldsymbol{\varepsilon} : \boldsymbol{\sigma}) \, r \, d\theta \, dr \, dz$

Since all field variables in an axisymmetric problem are independent of $\theta$, the integrand is constant with respect to $\theta$. The integration over the circumferential angle can therefore be performed directly, yielding a factor of $2\pi$. This reduces the 3D [volume integral](@entry_id:265381) to a 2D area integral over the meridional cross-section $A$ in the $(r,z)$ plane :

$\text{IVW} = \int_A (\delta\boldsymbol{\varepsilon} : \boldsymbol{\sigma}) (2\pi r) \, dA$

where $dA = dr \, dz$. This derivation reveals a critical aspect of the formulation: all element-level integrals (for stiffness matrices, force vectors, etc.) must include a multiplicative weighting factor of $2\pi r$. This factor, arising directly from the geometry of revolution, ensures that the contribution of material at a larger radius $r$ is appropriately weighted by its larger circumferential extent.

### Finite Element Discretization and the Strain-Displacement Matrix

In the finite element method, the continuous displacement field within an element is interpolated from the nodal values. For an $n$-node axisymmetric element, the displacement at any point $(r,z)$ is given by:

$u_r(r,z) = \sum_{i=1}^{n} N_i(r,z) u_{ri}$

$u_z(r,z) = \sum_{i=1}^{n} N_i(r,z) u_{zi}$

Here, $N_i$ are the [shape functions](@entry_id:141015), and $(u_{ri}, u_{zi})$ are the nodal displacement degrees of freedom (DOFs) for node $i$. This confirms that a standard axisymmetric element has two translational DOFs per node .

The relationship between the strain vector $\boldsymbol{\varepsilon} = [\varepsilon_{rr}, \varepsilon_{zz}, \varepsilon_{\theta\theta}, \gamma_{rz}]^T$ and the element's nodal [displacement vector](@entry_id:262782) $\boldsymbol{d}_e = [u_{r1}, u_{z1}, \dots, u_{rn}, u_{zn}]^T$ is defined by the [strain-displacement matrix](@entry_id:163451), $\boldsymbol{B}$, such that $\boldsymbol{\varepsilon} = \boldsymbol{B} \boldsymbol{d}_e$. By substituting the interpolated displacement fields into the strain definitions, we can construct the $\boldsymbol{B}$ matrix . For a generic node $i$, its contribution to the $\boldsymbol{B}$ matrix is a $4 \times 2$ sub-matrix, $\boldsymbol{B}_i$:

$\boldsymbol{B}_i = \begin{pmatrix}
\frac{\partial N_i}{\partial r} & 0 \\
0 & \frac{\partial N_i}{\partial z} \\
\frac{N_i}{r} & 0 \\
\frac{\partial N_i}{\partial z} & \frac{\partial N_i}{\partial r}
\end{pmatrix}$

The full $\boldsymbol{B}$ matrix is formed by concatenating these sub-matrices: $\boldsymbol{B} = [\boldsymbol{B}_1, \boldsymbol{B}_2, \dots, \boldsymbol{B}_n]$. The presence of the shape function $N_i$ divided by the [radial coordinate](@entry_id:165186) $r$ in the third row, corresponding to the [hoop strain](@entry_id:174548), is a unique and challenging feature of this matrix. It indicates that the strain field explicitly depends on the radial position, not just on the derivatives of the shape functions. As we will see, this term requires special attention near the [axis of symmetry](@entry_id:177299).

### Isoparametric Formulation and Numerical Integration

For elements with curved boundaries, an [isoparametric formulation](@entry_id:171513) is typically employed, where both the geometry and the [displacement field](@entry_id:141476) are interpolated using the same [shape functions](@entry_id:141015), defined over a master element in [natural coordinates](@entry_id:176605) $(\xi, \eta)$. The mapping from natural to physical coordinates is:

$r(\xi, \eta) = \sum_{i=1}^{n} N_i(\xi, \eta) r_i$

$z(\xi, \eta) = \sum_{i=1}^{n} N_i(\xi, \eta) z_i$

Since the shape functions are functions of $(\xi, \eta)$, while the strains are defined by derivatives with respect to $(r, z)$, we use the chain rule of differentiation. This relationship is expressed via the Jacobian matrix $\boldsymbol{J}$ of the [coordinate mapping](@entry_id:156506):

$\begin{pmatrix} \frac{\partial f}{\partial \xi} \\ \frac{\partial f}{\partial \eta} \end{pmatrix} = \begin{pmatrix} \frac{\partial r}{\partial \xi} & \frac{\partial z}{\partial \xi} \\ \frac{\partial r}{\partial \eta} & \frac{\partial z}{\partial \eta} \end{pmatrix} \begin{pmatrix} \frac{\partial f}{\partial r} \\ \frac{\partial f}{\partial z} \end{pmatrix} = \boldsymbol{J} \begin{pmatrix} \frac{\partial f}{\partial r} \\ \frac{\partial f}{\partial z} \end{pmatrix}$

The required physical derivatives are then found using the inverse of the Jacobian: $\begin{pmatrix} \partial f/\partial r \\ \partial f/\partial z \end{pmatrix} = \boldsymbol{J}^{-1} \begin{pmatrix} \partial f/\partial \xi \\ \partial f/\partial \eta \end{pmatrix}$. This allows the $\boldsymbol{B}$ matrix to be expressed entirely in terms of natural coordinate derivatives, which are readily available, and the inverse of the Jacobian matrix, which is computed at each integration point .

The [element stiffness matrix](@entry_id:139369) is computed by numerically integrating the [weak form](@entry_id:137295) over the element's area. This involves transforming the integral to the master element domain and using Gaussian quadrature:

$\mathbf{k}^e = \int_{A_e} \boldsymbol{B}^T \boldsymbol{D} \boldsymbol{B} (2\pi r) \, dA = \int_{-1}^1 \int_{-1}^1 \boldsymbol{B}(\xi, \eta)^T \boldsymbol{D} \boldsymbol{B}(\xi, \eta) (2\pi r(\xi, \eta)) \det(\boldsymbol{J}(\xi, \eta)) \, d\xi \, d\eta$

This integral is approximated as a weighted sum of the integrand evaluated at a set of Gauss points $(\xi_g, \eta_g)$. The effective quadrature weight at each Gauss point is a composite term: $w_g \cdot (2\pi r_g) \cdot \det(\boldsymbol{J}_g)$, where $w_g$ is the standard Gauss weight, $r_g = r(\xi_g, \eta_g)$ is the interpolated radius at the Gauss point, and $\det(\boldsymbol{J}_g)$ is the Jacobian determinant at that point . This procedure must be followed consistently for all integrals, including those for [consistent nodal forces](@entry_id:204135) arising from body forces or boundary tractions . For [finite deformation](@entry_id:172086) problems analyzed with an Updated Lagrangian formulation, the current [radial coordinate](@entry_id:165186) $r$ must be used in this integration, reflecting the evolving geometry .

### Special Considerations for the Axis of Symmetry ($r=0$)

The term $1/r$ in the definition of [hoop strain](@entry_id:174548) ($\varepsilon_{\theta\theta}=u_r/r$) and in the third row of the $\boldsymbol{B}$ matrix introduces a potential singularity at the [axis of symmetry](@entry_id:177299), $r=0$. This requires careful theoretical and numerical treatment to ensure a physically meaningful and computationally stable solution  .

For the strain and stress fields to remain finite and single-valued at the axis, the displacement field must satisfy certain **regularity conditions**. Specifically, the radial displacement must be zero on the axis: $u_r(0,z) = 0$. A Taylor series expansion of $u_r$ around $r=0$ shows that for the ratio $u_r/r$ to be finite, $u_r$ must be at least of order $\mathcal{O}(r)$ near the axis.

In the finite element context, these conditions are enforced through specific modeling practices:
1.  **Geometric Constraint**: Any element edge that lies on the [axis of symmetry](@entry_id:177299) must be defined by nodes that all have a [radial coordinate](@entry_id:165186) of zero, i.e., $r_i=0$.
2.  **Kinematic Constraint**: For all nodes located on the axis of symmetry, the radial displacement degree of freedom must be constrained to zero ($u_{ri}=0$) as an [essential boundary condition](@entry_id:162668).

When these two conditions are met, the potential singularity is resolved. Consider the contribution to [hoop strain](@entry_id:174548), $\varepsilon_{\theta\theta} = \frac{1}{r} \sum N_i u_{ri}$. For nodes on the axis, $u_{ri}=0$, so their contribution is zero despite $N_i$ being non-zero. For nodes *not* on the axis, their [shape functions](@entry_id:141015) $N_i$ are designed to be zero on the element edges they do not belong to. Thus, for an element with an edge on the axis, the [shape functions](@entry_id:141015) of the off-axis nodes vanish as $r \to 0$. In fact, for common [isoparametric elements](@entry_id:173863), both the interpolated radius $r(\xi,\eta)$ and the interpolated radial displacement $u_r(\xi,\eta)$ become proportional to the distance from the axis, and their ratio remains finite . This ensures that all entries of the $\boldsymbol{B}$ matrix are bounded everywhere within the element, and the [stiffness matrix](@entry_id:178659) integral is well-defined.

### Volumetric Locking in Nearly Incompressible Materials

In geomechanics, many problems involve saturated soils under undrained conditions, where the material behaves as [nearly incompressible](@entry_id:752387) (effective Poisson's ratio $\nu_u \to 0.5$). For such materials, standard displacement-based low-order [axisymmetric elements](@entry_id:163652) (like the 4-node quadrilateral with full integration) suffer from **[volumetric locking](@entry_id:172606)** .

Locking occurs because the element's kinematic field, as dictated by its shape functions, is not rich enough to satisfy the [incompressibility constraint](@entry_id:750592) ($\varepsilon_v = \varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta} = 0$) at all integration points without trivializing the solution. The element becomes artificially stiff, leading to an over-prediction of stresses and an under-prediction of deformations.

To overcome this, **[mixed formulations](@entry_id:167436)** are often employed, where the pressure field (pore pressure $p$ in [poromechanics](@entry_id:175398)) is introduced as an independent field variable. However, the choice of interpolation spaces for displacement and pressure is critical. They must satisfy the Ladyzhenskaya-Babuška-Brezzi (LBB) stability condition to avoid spurious pressure oscillations ([checkerboarding](@entry_id:747311)). Equal-order interpolations (e.g., bilinear for both displacement and pressure) violate the LBB condition and are unstable. Stable choices often involve using a lower-order interpolation for pressure than for displacement (e.g., bilinear displacement and constant pressure), often augmented with stabilization techniques to pass the LBB condition. These advanced formulations are essential for obtaining accurate results in axisymmetric simulations of [nearly incompressible materials](@entry_id:752388) .