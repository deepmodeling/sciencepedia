## Introduction
In the realm of [computational geomechanics](@entry_id:747617), the ability to simplify complex three-dimensional problems into manageable two-dimensional representations is fundamental to efficient and insightful analysis. The idealizations of [plane stress and plane strain](@entry_id:172357) stand as the most common and powerful of these simplifications. However, their application is fraught with nuance; an incorrect choice or misunderstanding of their underlying assumptions can lead to grossly inaccurate predictions of stress, deformation, and failure. This article addresses this critical knowledge gap by providing a rigorous examination of these 2D conditions.

Across the following chapters, you will gain a comprehensive understanding of these foundational concepts. The journey begins in **"Principles and Mechanisms,"** which deconstructs the kinematic and static constraints that define plane strain and plane stress, deriving the respective 2D governing equations and constitutive laws from first principles. Next, **"Applications and Interdisciplinary Connections"** demonstrates the profound impact of these idealizations in diverse fields, from fracture mechanics and structural analysis to advanced geotechnical engineering and coupled thermo-poro-mechanical problems. Finally, **"Hands-On Practices"** offers a series of guided problems to solidify your theoretical knowledge and build practical skills in applying and verifying these concepts in computational models. By the end, you will be equipped to judiciously apply these essential tools in your own research and engineering practice.

## Principles and Mechanisms

The reduction of three-dimensional continuum mechanics problems to two-dimensional idealizations is a cornerstone of computational analysis, offering significant savings in computational cost while retaining physical fidelity for certain classes of problems. Among the most common of these idealizations are the conditions of **[plane stress](@entry_id:172193)** and **[plane strain](@entry_id:167046)**. Understanding their definitions, the assumptions that underpin them, and their consequences on the governing equations is critical for any practitioner of [computational geomechanics](@entry_id:747617). This chapter delineates the principles and mechanisms of these two-dimensional states, starting from fundamental definitions and progressing to the subtleties of their application in advanced models.

### Fundamental Definitions: Kinematic and Static Constraints

At its core, the distinction between [plane stress and plane strain](@entry_id:172357) lies in which components of the stress or [strain tensor](@entry_id:193332) are assumed to be zero. Let us consider a Cartesian coordinate system $(x,y,z)$, where the problem is to be simplified to the $x,y$-plane. The $z$-direction is referred to as the out-of-plane direction.

**Plane Strain**

The **[plane strain](@entry_id:167046)** condition is a *kinematic* constraint. It is defined by the assumption that all strain components associated with the out-of-plane direction are zero. In [index notation](@entry_id:191923), with $(x_1, x_2, x_3)$ corresponding to $(x,y,z)$, this is expressed as:
$$
\varepsilon_{i3} = 0 \quad \text{for } i \in \{1,2,3\}
$$
This means $\varepsilon_{xx}$, $\varepsilon_{yy}$, and $\varepsilon_{xy}$ may be non-zero, but the out-of-plane [normal strain](@entry_id:204633) and shear strains must vanish:
$$
\varepsilon_{zz} = 0, \quad \varepsilon_{xz} = 0, \quad \varepsilon_{yz} = 0
$$
Since the engineering shear strains are simply $\gamma_{ij} = 2\varepsilon_{ij}$ for $i \neq j$, this also implies $\gamma_{xz}=0$ and $\gamma_{yz}=0$.

These kinematic constraints have direct implications for the displacement field $\boldsymbol{u} = (u_x, u_y, u_z)$. For the strain field to be independent of the $z$-coordinate, a common requirement for 2D problems, we typically assume that the in-plane displacements are functions of $x$ and $y$ only, i.e., $u_x = u_x(x,y)$ and $u_y = u_y(x,y)$. Given the small-strain definition $\varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})$, where $u_{i,j} = \partial u_i / \partial x_j$, we can deduce the constraints on $u_z$:
- $\varepsilon_{zz} = \partial u_z / \partial z = 0 \implies u_z$ does not depend on $z$, so $u_z=u_z(x,y)$.
- $\varepsilon_{xz} = \frac{1}{2}(\partial u_x / \partial z + \partial u_z / \partial x) = \frac{1}{2}(0 + \partial u_z / \partial x) = 0 \implies \partial u_z / \partial x = 0$.
- $\varepsilon_{yz} = \frac{1}{2}(\partial u_y / \partial z + \partial u_z / \partial y) = \frac{1}{2}(0 + \partial u_z / \partial y) = 0 \implies \partial u_z / \partial y = 0$.

Taken together, these conditions imply that $u_z$ must be constant. Since a constant displacement is a [rigid body motion](@entry_id:144691) that typically does not affect the [stress analysis](@entry_id:168804), it is common to set this constant to zero, leading to the sufficient kinematic conditions for plane strain [@problem_id:3550706]:
$$
u_x = u_x(x,y), \quad u_y = u_y(x,y), \quad u_z = 0
$$
The [plane strain assumption](@entry_id:186003) is physically appropriate for long prismatic bodies where the geometry, material properties, and loading do not vary along the length (the $z$-axis). The end faces are constrained from axial movement, preventing deformation in the axial direction. Examples in geomechanics include long retaining walls, tunnels, pipelines, and dams.

**Plane Stress**

In contrast, the **[plane stress](@entry_id:172193)** condition is a *static* constraint. It is defined by the assumption that all stress components acting on planes normal to the $z$-direction are zero:
$$
\sigma_{i3} = 0 \quad \text{for } i \in \{1,2,3\}
$$
This implies that the out-of-plane normal stress and shear stresses are zero:
$$
\sigma_{zz} = 0, \quad \sigma_{xz} = 0, \quad \sigma_{yz} = 0
$$
For a linear elastic isotropic material, the relationship between shear stress and shear strain is $\sigma_{ij} = 2\mu\varepsilon_{ij}$ for $i \neq j$, where $\mu$ is the shear modulus. Since $\mu > 0$, the conditions $\sigma_{xz}=0$ and $\sigma_{yz}=0$ directly imply $\varepsilon_{xz}=0$ and $\varepsilon_{yz}=0$. However, the out-of-plane [normal strain](@entry_id:204633) $\varepsilon_{zz}$ is generally **non-zero**. Using the generalized Hooke's law, we find:
$$
\varepsilon_{zz} = \frac{1}{E} \left[ \sigma_{zz} - \nu (\sigma_{xx} + \sigma_{yy}) \right] = -\frac{\nu}{E}(\sigma_{xx} + \sigma_{yy})
$$
This non-zero strain represents the change in thickness of the body due to the Poisson effect.

The [plane stress assumption](@entry_id:184389) is physically relevant for thin, plate-like structures loaded only in their plane. The "thinness" of the body in the $z$-direction prevents the buildup of significant stresses through the thickness. A sufficient set of simplifying kinematic assumptions that are consistent with a 2D formulation is that the in-plane displacements do not vary through the thickness, $u_x=u_x(x,y)$ and $u_y=u_y(x,y)$, and that the out-of-plane displacement is only a function of $z$, $u_z=u_z(z)$ [@problem_id:3550706].

### Derivation of Two-Dimensional Governing Equations

The reduction to a two-dimensional framework requires not only defining the kinematic or static state but also reformulating the governing equations of mechanics in two dimensions. This is most elegantly achieved using variational principles, which are the foundation of the finite element method.

**Strain-Displacement Relations**

The in-plane strains depend only on the in-plane displacements. Assuming the displacement field is independent of the $z$-coordinate, $u_x = u_x(x,y)$ and $u_y = u_y(x,y)$, the [infinitesimal strain](@entry_id:197162) definitions directly yield the familiar 2D [strain-displacement relations](@entry_id:173321) [@problem_id:3550759]:
$$
\varepsilon_{xx} = \frac{\partial u_x}{\partial x}, \quad \varepsilon_{yy} = \frac{\partial u_y}{\partial y}, \quad \gamma_{xy} = 2\varepsilon_{xy} = \frac{\partial u_x}{\partial y} + \frac{\partial u_y}{\partial x}
$$
Notably, the out-of-plane displacement component, $u_z(x,y)$, does not appear in these expressions. The justification for its omission from the final 2D formulation depends on the specific idealization ([plane stress](@entry_id:172193) or [plane strain](@entry_id:167046)) and is best understood through the Principle of Virtual Work (PVW).

**Weak Form and Variational Principles**

The 3D PVW states that for a body in equilibrium, the [internal virtual work](@entry_id:172278) equals the external virtual work for any kinematically admissible [virtual displacement](@entry_id:168781) field $\delta \boldsymbol{u}$:
$$
\int_{V} \boldsymbol{\sigma} : \delta\boldsymbol{\varepsilon} \, dV = \int_{V} \boldsymbol{b} \cdot \delta \boldsymbol{u} \, dV + \int_{S_t} \boldsymbol{t} \cdot \delta \boldsymbol{u} \, dS
$$
The term on the left is the [internal virtual work](@entry_id:172278) (IVW), and its integrand can be expanded as:
$$
\boldsymbol{\sigma} : \delta\boldsymbol{\varepsilon} = \sigma_{xx}\delta\varepsilon_{xx} + \sigma_{yy}\delta\varepsilon_{yy} + \sigma_{zz}\delta\varepsilon_{zz} + 2\sigma_{xy}\delta\varepsilon_{xy} + 2\sigma_{xz}\delta\varepsilon_{xz} + 2\sigma_{yz}\delta\varepsilon_{yz}
$$

**Reduction to Plane Strain:** Under the plane strain kinematic constraint, any admissible [virtual displacement](@entry_id:168781) field must also satisfy $\delta u_z = 0$, which in turn implies that the virtual out-of-plane strains are zero: $\delta\varepsilon_{zz} = 0$, $\delta\varepsilon_{xz} = 0$, and $\delta\varepsilon_{yz} = 0$. The IVW integrand simplifies to contain only in-plane terms. This leads to a crucial insight: in [plane strain](@entry_id:167046), the out-of-plane stress $\sigma_{zz}$ is generally non-zero (as it is required to enforce $\varepsilon_{zz}=0$), but it performs no [virtual work](@entry_id:176403) because its corresponding virtual strain, $\delta\varepsilon_{zz}$, is identically zero. The problem is thus governed entirely by the in-plane displacements and their corresponding virtual counterparts [@problem_id:3550713].

**Reduction to Plane Stress:** Under the [plane stress](@entry_id:172193) static constraint, the out-of-plane stresses are zero: $\sigma_{zz} = \sigma_{xz} = \sigma_{yz} = 0$. These terms therefore drop out of the IVW integrand directly. The resulting IVW term again depends only on the in-plane stresses and strains. In this case, the out-of-plane [virtual displacement](@entry_id:168781) $\delta u_z$ is not necessarily zero, but because its work-conjugate stresses are zero, the in-plane equilibrium problem for $(u_x, u_y)$ completely decouples from the out-of-plane displacement $u_z$ [@problem_id:3550759].

**Reduction of External Work:** To complete the 2D formulation, the 3D external work integrals must be reduced. Consider a prismatic body of constant thickness $h$. If the body forces $\boldsymbol{b}$ and boundary tractions $\boldsymbol{t}$ are assumed to be uniform through the thickness and act in the $x,y$-plane, the 3D volume and [surface integrals](@entry_id:144805) can be explicitly integrated with respect to $z$. This process reveals that the effective 2D [body force](@entry_id:184443) (per unit area) and line traction (per unit length) are the original 3D quantities multiplied by the thickness $h$. Consequently, the 2D external [load vector](@entry_id:635284) in a [finite element formulation](@entry_id:164720) is scaled by this factor $h$ [@problem_id:3550779].

### Two-Dimensional Constitutive Relations

The effective stiffness of a material in a 2D representation is different for [plane stress and plane strain](@entry_id:172357). These relationships are derived by applying the respective constraints to the 3D Hooke's Law. For a homogeneous, isotropic material with Young's modulus $E$ and Poisson's ratio $\nu$, the 2D constitutive matrices $\mathbf{D}$ relate the in-plane stress vector $\boldsymbol{\sigma}' = [\sigma_{xx}, \sigma_{yy}, \tau_{xy}]^T$ to the in-plane strain vector $\boldsymbol{\varepsilon}' = [\varepsilon_{xx}, \varepsilon_{yy}, \gamma_{xy}]^T$ via $\boldsymbol{\sigma}' = \mathbf{D} \boldsymbol{\varepsilon}'$.

**Plane Stress Constitutive Matrix**

Starting from the 3D compliance (strain-stress) relations and imposing $\sigma_{zz} = 0$, we find the strains in terms of in-plane stresses [@problem_id:3550715]:
$$
\varepsilon_{xx} = \frac{1}{E}(\sigma_{xx} - \nu\sigma_{yy}), \quad \varepsilon_{yy} = \frac{1}{E}(\sigma_{yy} - \nu\sigma_{xx}), \quad \gamma_{xy} = \frac{2(1+\nu)}{E}\tau_{xy}
$$
Inverting this relationship yields the plane stress [stiffness matrix](@entry_id:178659) $\mathbf{D}_{ps}$ [@problem_id:3550742]:
$$
\mathbf{D}_{ps} = \frac{E}{1-\nu^2}
\begin{pmatrix} 
1  \nu  0 \\
\nu  1  0 \\
0  0  \frac{1-\nu}{2} 
\end{pmatrix}
$$

**Plane Strain Constitutive Matrix**

Starting from the 3D stiffness (stress-strain) relations and imposing $\varepsilon_{zz} = 0$, we find the in-plane stresses. The constraint $\varepsilon_{zz}=0$ induces an out-of-plane stress $\sigma_{zz} = \nu(\sigma_{xx}+\sigma_{yy})$. This stress contributes to the in-plane strains through the Poisson effect, stiffening the response. The resulting [plane strain](@entry_id:167046) stiffness matrix $\mathbf{D}_{pe}$ is [@problem_id:3550713]:
$$
\mathbf{D}_{pe} = \frac{E}{(1+\nu)(1-2\nu)}
\begin{pmatrix} 
1-\nu  \nu  0 \\
\nu  1-\nu  0 \\
0  0  \frac{1-2\nu}{2} 
\end{pmatrix}
$$
This matrix can also be expressed in terms of the Lamé parameters $\lambda$ and $\mu$ as:
$$
\mathbf{D}_{pe} = 
\begin{pmatrix} 
\lambda + 2\mu  \lambda  0 \\
\lambda  \lambda + 2\mu  0 \\
0  0  \mu
\end{pmatrix}
$$

### Consequences and Practical Implications

The choice between [plane stress and plane strain](@entry_id:172357) is not merely a modeling convenience; it reflects a physical assumption that has profound implications for the predicted mechanical response.

**Apparent Material Properties and the Perils of Equivalence**

The increased constraint in plane strain makes the material behave as if it were stiffer. We can quantify this by examining the "apparent in-plane Poisson's ratio" under a uniaxial stress state ($\sigma_{xx} = \sigma_0, \sigma_{yy}=0$).
- In plane stress, the [transverse strain](@entry_id:157965) is $\varepsilon_{yy} = -\nu\sigma_{xx}/E$, so the ratio $-\varepsilon_{yy}/\varepsilon_{xx}$ is simply $\nu$.
- In plane strain, the same stress state produces a ratio $-\varepsilon_{yy}/\varepsilon_{xx}$ that evaluates to $\nu/(1-\nu)$.

Since $0  \nu  0.5$ for most materials, the apparent Poisson's ratio is always larger in [plane strain](@entry_id:167046), reflecting the greater resistance to lateral deformation [@problem_id:3550715]. This leads to the observation that it's possible to find a set of "effective" material parameters $(E', \nu')$ that makes the [plane stress](@entry_id:172193) [stiffness matrix](@entry_id:178659), $\mathbf{D}_{ps}(E', \nu')$, numerically identical to the plane strain matrix $\mathbf{D}_{pe}(E, \nu)$. The required parameters are $\nu' = \nu/(1-\nu)$ and $E' = E/(1-\nu^2)$ [@problem_id:3550742].

While this mathematical equivalence is tempting, using it to model a plane strain problem in a code designed for plane stress is **highly misleading and dangerous** in [geomechanics](@entry_id:175967). The equivalence holds only for the in-[plane stress](@entry_id:172193)-strain relationship. It creates a fictitious 3D state that is fundamentally incorrect:
1.  **Mean Stress and Plasticity:** The true [plane strain](@entry_id:167046) state has a non-zero out-of-plane stress $\sigma_{zz}$. The "equivalent" plane stress model assumes $\sigma'_{zz}=0$. The first stress invariant, $I_1 = \sigma_{xx}+\sigma_{yy}+\sigma_{zz}$, which governs the [mean stress](@entry_id:751819) or pressure, will be grossly underestimated. Since the yield and failure of [geomaterials](@entry_id:749838) are highly dependent on pressure, a model using this equivalence will incorrectly predict the onset of [plastic deformation](@entry_id:139726) and failure.
2.  **Volumetric Response and Poromechanics:** The true volumetric strain in [plane strain](@entry_id:167046) is $\varepsilon_v = \varepsilon_{xx}+\varepsilon_{yy}$. The equivalent plane stress model predicts a non-zero out-of-plane strain $\varepsilon'_{zz}$, leading to a different [volumetric strain](@entry_id:267252) $\varepsilon'_v$. In [poromechanics](@entry_id:175398) (Biot theory), [pore pressure](@entry_id:188528) generation is coupled to the change in volumetric strain of the solid skeleton. Using the $(E', \nu')$ substitution would lead to an entirely erroneous prediction of the pore pressure response, a critical aspect of many geotechnical problems [@problem_id:3550742].

**The Full Three-Dimensional Stress State**

A 2D analysis only computes the in-plane stress components. However, the full 3D stress state is required to evaluate against 3D [failure criteria](@entry_id:195168). For a given in-[plane stress](@entry_id:172193) state $(\sigma_{xx}, \sigma_{yy}, \tau_{xy})$, the in-plane [principal stresses](@entry_id:176761) $\sigma_1$ and $\sigma_2$ are identical for both idealizations. The difference lies entirely in the third, out-of-plane principal stress, $\sigma_3 = \sigma_{zz}$.
- In **plane stress**, $\sigma_3 = \sigma_{zz} = 0$ by definition.
- In **plane strain**, $\sigma_3 = \sigma_{zz} = \nu(\sigma_{xx} + \sigma_{yy})$.

Consider a soil element with $\sigma_{xx}=64\,\text{MPa}$, $\sigma_{yy}=12\,\text{MPa}$, $\tau_{xy}=20\,\text{MPa}$, and $\nu=0.327$. The in-plane principal stresses are $\sigma_1 \approx 70.8\,\text{MPa}$ and $\sigma_2 \approx 5.2\,\text{MPa}$. In a plane stress scenario, the three [principal stresses](@entry_id:176761) are $\{70.8, 5.2, 0\}$ MPa. In a [plane strain](@entry_id:167046) scenario, the out-of-[plane stress](@entry_id:172193) is $\sigma_3 = 0.327(64+12) \approx 24.9\,\text{MPa}$. The three [principal stresses](@entry_id:176761) are thus $\{70.8, 24.9, 5.2\}$ MPa. The intermediate [principal stress](@entry_id:204375) is significantly different, which can alter the predicted [factor of safety](@entry_id:174335) against failure when using a 3D criterion like Mohr-Coulomb or Drucker-Prager [@problem_id:3550778].

**Applicability and Saint-Venant's Principle**

A crucial question is when these idealizations are valid. A [plane strain](@entry_id:167046) analysis of a long embankment, for instance, implicitly assumes the embankment is infinitely long. For a real, finite-length structure, this is an approximation. **Saint-Venant's principle** provides the justification. It states that the effects of a localized, statically [self-equilibrated load](@entry_id:181309) distribution decay with distance, over a characteristic length scale comparable to the cross-sectional dimensions of the body.

For a rectangular load of length $L$ and width $B$ on a [soil profile](@entry_id:195342), the finite length creates "end effects." These effects decay as one moves away from the ends. A plane strain analysis is considered accurate in the central region of the structure if the length $L$ is much larger than the [characteristic decay length](@entry_id:183295), which is on the order of the width $B$ and the depth to significant features (like a stiff layer), $\max(B, H_1)$. A common rule of thumb is that [plane strain](@entry_id:167046) is applicable if $L/\max(B,H_1)  5 \text{ or } 10$. If this condition is not met, the end effects from both ends overlap, and a full 3D analysis is necessary.

The validity of the [plane strain assumption](@entry_id:186003) is weakened by:
- **Low [aspect ratio](@entry_id:177707) ($L/B$):** When the structure is not "long."
- **High stiffness contrast:** A very stiff layer over a soft layer can transmit shear stresses over long distances (shear lag), increasing the decay length of end effects.
- **Near-[incompressibility](@entry_id:274914) ($\nu \to 0.5$):** Under short-term, undrained conditions in saturated soils, the material is [nearly incompressible](@entry_id:752387). The strong kinematic coupling allows stress perturbations to propagate further, again increasing the decay length of end effects. In such cases, a larger [aspect ratio](@entry_id:177707) is required to justify a plane strain analysis [@problem_id:3550702].

### Advanced Topics and Extensions

The classical definitions can be extended to more complex and realistic scenarios.

**Generalized Plane Strain**

The classical plane strain condition ($\varepsilon_{zz}=0$) can be overly restrictive. **Generalized [plane strain](@entry_id:167046)** is a more flexible assumption that allows for a uniform [axial strain](@entry_id:160811), $\varepsilon_{zz} = \bar{\varepsilon}_{zz}$, where $\bar{\varepsilon}_{zz}$ is a constant. This corresponds to a displacement field of the form $u_x=u_x(x,y)$, $u_y=u_y(x,y)$, and $w = \bar{\varepsilon}_{zz}z + c$. The out-of-plane shear strains $\gamma_{xz}$ and $\gamma_{yz}$ remain zero. This model is particularly useful for problems involving uniform axial extension, such as thermal loading of a constrained pipeline or the response of a long tunnel to a uniform change in axial stress. For this kinematic assumption to represent a valid (compatible) deformation, the in-plane strains must still satisfy the 2D compatibility equation, and the condition that $\varepsilon_{zz}$ is uniform across the cross-section is itself a satisfaction of the relevant 3D compatibility requirements [@problem_id:3550719].

**Anisotropy: Orthotropic Materials**

The principles of plane strain and [plane stress](@entry_id:172193) are not limited to [isotropic materials](@entry_id:170678). In [geomechanics](@entry_id:175967), sedimentary rock and soil deposits often exhibit [orthotropy](@entry_id:196967) or [transverse isotropy](@entry_id:756140). For an [orthotropic material](@entry_id:191640) with principal axes aligned with $(x,y,z)$, the [plane strain](@entry_id:167046) condition $\varepsilon_{zz}=0$ still applies, but the resulting out-of-[plane stress](@entry_id:172193) $\sigma_{zz}$ is more complex. By solving the 3D orthotropic compliance relations, one can find $\sigma_{zz}$ in terms of the in-plane strains and a larger set of material constants [@problem_id:3550763]:
$$
\sigma_{zz} = C_{31}\varepsilon_{xx} + C_{32}\varepsilon_{yy}
$$
where the stiffness coefficients $C_{31}$ and $C_{32}$ depend on all three Young's moduli ($E_x, E_y, E_z$) and all three independent Poisson's ratios ($\nu_{xy}, \nu_{xz}, \nu_{yz}$). A [sensitivity analysis](@entry_id:147555) shows that $\sigma_{zz}$ is, as expected, highly sensitive to the out-of-plane stiffness $E_z$ and the coupling Poisson's ratios $\nu_{xz}$ and $\nu_{yz}$. This underscores the importance of proper material characterization when applying 2D idealizations to [anisotropic media](@entry_id:260774).