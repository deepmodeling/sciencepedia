## Introduction
Modeling fracture in brittle [geomaterials](@entry_id:749838) like rock and concrete is a persistent challenge in engineering and earth sciences. Classical [continuum mechanics](@entry_id:155125), the traditional tool for such analyses, falters at its core when faced with cracks, as its mathematical framework relies on smooth, continuous material displacement that is fundamentally broken by a fracture. This limitation necessitates complex, supplementary theories to track crack growth, often with significant restrictions. Peridynamics offers a revolutionary alternative, reformulating the laws of mechanics to inherently accommodate discontinuities, making it an exceptionally powerful tool for simulating fracture from initiation to propagation.

This article provides a comprehensive guide to understanding and applying [peridynamic modeling](@entry_id:753345) for brittle [geomaterials](@entry_id:749838). It bridges the gap between the foundational theory and its practical application, offering a structured learning path for graduate-level researchers and engineers. This article is structured in three main parts. First, **"Principles and Mechanisms"** will deconstruct the fundamental theory, from the nonlocal equation of motion and [constitutive models](@entry_id:174726) to the essential details of numerical implementation. Next, **"Applications and Interdisciplinary Connections"** will demonstrate how these principles are applied to solve complex problems in [fracture mechanics](@entry_id:141480), [multiphysics coupling](@entry_id:171389), and microstructural analysis. Finally, **"Hands-On Practices"** will provide practical exercises to solidify your knowledge on [model calibration](@entry_id:146456), formulation choices, and computational efficiency.

## Principles and Mechanisms

This section delineates the fundamental principles and theoretical underpinnings of the peridynamic theory, a nonlocal continuum framework particularly well-suited for modeling fracture in brittle [geomaterials](@entry_id:749838). We will move from the foundational equation of motion to [constitutive modeling](@entry_id:183370) for brittle failure, and conclude with key aspects of numerical implementation and advanced modeling techniques.

### The Peridynamic Equation of Motion: A Nonlocal Perspective

Classical [continuum mechanics](@entry_id:155125), as described by Cauchy's laws of motion, provides a powerful framework for analyzing [deformable bodies](@entry_id:201887). Its governing equation for the [balance of linear momentum](@entry_id:193575) is expressed as a partial differential equation:
$$
\rho(\mathbf{x})\ddot{\mathbf{u}}(\mathbf{x},t) = \nabla \cdot \boldsymbol{\sigma}(\mathbf{x},t) + \mathbf{b}(\mathbf{x},t)
$$
Here, $\rho(\mathbf{x})$ is the mass density at a point $\mathbf{x}$, $\mathbf{u}(\mathbf{x},t)$ is the displacement vector, $\mathbf{b}(\mathbf{x},t)$ is a [body force](@entry_id:184443) density field (such as gravity), and $\boldsymbol{\sigma}(\mathbf{x},t)$ is the Cauchy stress tensor. The [internal forces](@entry_id:167605) within the material are represented by the divergence of the stress tensor, $\nabla \cdot \boldsymbol{\sigma}$. A critical feature of this formulation is its reliance on spatial derivatives of the [displacement field](@entry_id:141476), as stress is constitutively related to strain, which is itself defined by displacement gradients. This mathematical structure presumes that the displacement field is smooth and differentiable. However, in the context of [brittle fracture](@entry_id:158949), this assumption breaks down. A crack is, by definition, a displacement discontinuity, where spatial derivatives are singular or undefined. This renders the classical [equation of motion](@entry_id:264286) ill-posed at crack tips and necessitates separate, supplementary theories, such as [linear elastic fracture mechanics](@entry_id:172400), to handle crack growth.

Peridynamics (PD) reformulates the principles of continuum mechanics to circumvent this fundamental limitation. Instead of relying on local stress gradients, [peridynamics](@entry_id:191791) postulates that material points interact directly with other points over a finite distance. The internal force at a point is calculated by summing up **pairwise forces** exerted by all other points within a prescribed neighborhood. This nonlocal approach is expressed through an integro-differential equation of motion [@problem_id:3549602]:
$$
\rho(\mathbf{x})\ddot{\mathbf{u}}(\mathbf{x},t) = \int_{H_{\mathbf{x}}} \mathbf{f}(\mathbf{u}(\mathbf{x}',t) - \mathbf{u}(\mathbf{x},t), \mathbf{x}' - \mathbf{x}) \, dV_{\mathbf{x}'} + \mathbf{b}(\mathbf{x},t)
$$
In this equation, the [divergence of stress](@entry_id:185633) is replaced by an integral term. The domain of integration, $H_{\mathbf{x}}$, is a finite-sized region surrounding the point $\mathbf{x}$, known as the **horizon**. The integrand contains the **pairwise force function**, $\mathbf{f}$, which represents the force density (force per unit volume squared) that a point $\mathbf{x}'$ exerts on point $\mathbf{x}$. This function depends on two key arguments: the relative displacement vector $\boldsymbol{\eta} = \mathbf{u}(\mathbf{x}',t) - \mathbf{u}(\mathbf{x},t)$, and the initial [relative position](@entry_id:274838) vector (or **bond**) $\boldsymbol{\xi} = \mathbf{x}' - \mathbf{x}$.

Because the peridynamic equation of motion is based on an integral and does not involve spatial derivatives of the displacement field, it remains valid even when the [displacement field](@entry_id:141476) $\mathbf{u}$ contains discontinuities. This allows fracture to be modeled as a natural outcome of the simulation, arising from the progressive failure of bonds, rather than requiring an external crack-tracking algorithm. For [conservation of linear momentum](@entry_id:165717), the pairwise force function must satisfy the [action-reaction principle](@entry_id:195494), expressed as an antisymmetry condition: $\mathbf{f}(\boldsymbol{\eta}, \boldsymbol{\xi}) = -\mathbf{f}(-\boldsymbol{\eta}, -\boldsymbol{\xi})$.

### The Horizon and Material Length Scale

The concept of the horizon is central to [peridynamics](@entry_id:191791). The horizon, typically a sphere of radius $\delta$ centered at $\mathbf{x}$, defines the range of nonlocal interactions. Any material point $\mathbf{x}'$ outside of this sphere does not exert a direct force on $\mathbf{x}$. The horizon radius, $\delta$, is not merely a numerical parameter but is considered an intrinsic **[material length scale](@entry_id:197771)** that reflects the scale of microstructural interactions within the material.

The presence of this length scale has profound implications for modeling [material failure](@entry_id:160997) [@problem_id:3549612]. In local [continuum models](@entry_id:190374), strain can localize into zones of zero thickness, leading to [pathological mesh dependency](@entry_id:184469) and incorrect energy dissipation during failure. The nonlocal integral in the peridynamic equation acts as a spatial filter on the deformation field. This filtering effect regularizes the solution by preventing [strain localization](@entry_id:176973) to widths smaller than the order of the horizon size, $O(\delta)$. Consequently, fracture process zones in peridynamic simulations naturally acquire a finite width related to $\delta$.

Furthermore, the horizon size $\delta$ governs the geometric regularity of predicted crack paths. By averaging deformation information over the horizon, the formulation promotes the development of smoother crack patterns, disfavoring the formation of crack features with a radius of curvature smaller than $\delta$. This regularizing effect helps to produce more physically realistic and less mesh-dependent crack morphologies, especially in materials with complex microstructures.

### Constitutive Modeling: From Bonds to Material Response

The predictive power of [peridynamics](@entry_id:191791) lies in the formulation of the pairwise force function $\mathbf{f}$, which serves as the [constitutive model](@entry_id:747751). Different formulations have been developed to capture a range of material behaviors.

#### Bond-Based vs. State-Based Formulations

The earliest and simplest peridynamic formulation is known as **[bond-based peridynamics](@entry_id:188457) (BB-PD)**. Its defining characteristic is the assumption that the force interaction between any two points, $\mathbf{x}$ and $\mathbf{x}'$, is independent of all other bonds and acts collinearly with the bond vector $\boldsymbol{\xi} = \mathbf{x}' - \mathbf{x}$. This is analogous to modeling the material as a network of central-force springs.

While simple and effective for many problems, BB-PD has a significant limitation when modeling isotropic linear elastic materials. Because the central-force assumption inherently couples the material's response to shear and volumetric deformations, it cannot represent an arbitrary pair of [elastic constants](@entry_id:146207). For a 3D isotropic material, the BB-PD formulation enforces a fixed relationship between the Lamé parameters, $\lambda = \mu$, which corresponds to a **Poisson's ratio** of $\nu = 1/4$. Similarly, for 2D [plane strain](@entry_id:167046), it results in $\nu = 1/3$. This restriction prevents the accurate modeling of many real-world [geomaterials](@entry_id:749838) whose Poisson's ratio differs from this fixed value [@problem_id:3549599].

To overcome this limitation, **[state-based peridynamics](@entry_id:190841) (SB-PD)** was introduced. In this more general framework, the force in a bond is allowed to depend on the collective deformation of all bonds within the horizon. In **ordinary [state-based peridynamics](@entry_id:190841) (OSB-PD)**, the force vector is no longer constrained to be collinear with the bond vector, though the pairwise forces remain antisymmetric to conserve angular momentum. This additional freedom allows for the design of [constitutive models](@entry_id:174726) that decouple the material's dilatational (volumetric) and deviatoric (shear) responses. By calibrating these two responses independently, OSB-PD can represent any physically admissible pair of elastic constants ($E, \nu$), thus providing a much more versatile framework for modeling a wide range of materials.

#### Modeling Brittle Fracture: The Microelastic Brittle Model

For brittle materials, the most fundamental [constitutive model](@entry_id:747751) is the **microelastic brittle model**, often implemented within a bond-based framework for simplicity. In this model, each bond is treated as a linear elastic spring that can break. The deformation of a bond is quantified by the scalar **bond stretch**, $s$, defined as the change in length divided by the initial length:
$$
s = \frac{|\boldsymbol{\xi} + \boldsymbol{\eta}| - |\boldsymbol{\xi}|}{|\boldsymbol{\xi}|}
$$
A positive stretch corresponds to tension, while a negative stretch corresponds to compression.

The "brittle" nature of the model is captured by introducing a material property known as the **[critical stretch](@entry_id:200184)**, $s_c$ [@problem_id:3549611]. This value represents the maximum tensile stretch a bond can withstand before it fails. When the stretch $s$ in a bond reaches or exceeds $s_c$, the bond breaks irreversibly and can no longer transmit force. This microscopic bond failure is the peridynamic mechanism for the [nucleation and growth](@entry_id:144541) of macroscopic cracks.

The micro-[scale parameter](@entry_id:268705) $s_c$ must be related to a measurable macro-scale material property. For [brittle fracture](@entry_id:158949), this property is the **fracture energy**, $G_c$ (also known as the critical [energy release rate](@entry_id:158357)). The value of $s_c$ is calibrated by equating the total energy required to break all the bonds that cross a hypothetical crack surface of unit area to the material's macroscopic [fracture energy](@entry_id:174458) $G_c$. This energetic consistency ensures that the model dissipates the correct amount of energy during [crack propagation](@entry_id:160116).

#### The Formalism of Irreversible Bond Failure

To implement the concept of irreversible fracture, the failure rule must be history-dependent. A bond that has broken must not be allowed to "heal" if the load is reversed and the stretch drops below the critical value. This is accomplished by introducing a **binary [damage variable](@entry_id:197066)** and tracking the loading history of each bond [@problem_id:3549624].

Let us define a [damage variable](@entry_id:197066) $\mu(t)$ for a given bond, where $\mu=1$ signifies an intact bond and $\mu=0$ signifies a broken bond. A simple rule like $\mu(t) = 1$ if $s(t)  s_c$ and $\mu(t) = 0$ otherwise would be incorrect, as it would allow the bond to heal. To enforce [irreversibility](@entry_id:140985), we must track the maximum stretch that the bond has ever experienced. Let this be $s_{\max}(t) = \sup_{\tau \in [0,t]} s(\tau)$. The [damage evolution](@entry_id:184965) rule is then defined based on this history variable: a bond breaks permanently if its maximum experienced stretch ever exceeds the [critical stretch](@entry_id:200184). This is expressed by updating the damage state variable $\mu$ at each time $t$:
$$
\mu(t) = 
\begin{cases}
1  \text{if } s(\tau)  s_c \text{ for all } \tau \le t \\
0  \text{otherwise}
\end{cases}
$$
This ensures that once the stretch exceeds $s_c$ at any point in time, the [damage variable](@entry_id:197066) $\mu$ switches permanently to $0$. The pairwise force function is then modified to include this damage state, for example, $\mathbf{f} = \mu \cdot \mathbf{f}_{\text{elastic}}$, where $\mathbf{f}_{\text{elastic}}$ is the force law for an intact bond. When $\mu=0$, the force contribution from that bond vanishes forever. This formulation is consistent with thermodynamic principles, as it ensures that damage is a non-decreasing process.

### Numerical Implementation and Discretization

To solve engineering problems, the peridynamic integro-differential equation must be discretized in both space and time.

#### Spatial Discretization

Peridynamics is typically implemented using a "meshfree" particle method. The material domain is discretized into a collection of nodes or particles, each representing a small volume of material, $\Delta V$. The integral in the equation of motion is then approximated by a finite sum over all particles within the horizon of a given particle $\mathbf{x}_i$. A common one-point quadrature scheme (a Riemann sum) takes the form [@problem_id:3549607]:
$$
\int_{H_{\mathbf{x}_i}} \mathbf{f}(\mathbf{u}(\mathbf{x}',t) - \mathbf{u}(\mathbf{x}_i,t), \mathbf{x}' - \mathbf{x}_i) \, dV_{\mathbf{x}'} \approx \sum_{j \in \mathcal{N}_i} \mathbf{f}(\mathbf{u}_j(t) - \mathbf{u}_i(t), \mathbf{x}_j - \mathbf{x}_i) \Delta V_j
$$
Here, the sum is over all particles $j$ in the **[neighbor list](@entry_id:752403)**, $\mathcal{N}_i$, of particle $i$. This [neighbor list](@entry_id:752403) contains all particles whose centers fall within the horizon of particle $i$.

For [computational efficiency](@entry_id:270255), constructing these [neighbor lists](@entry_id:141587) is a critical step. A brute-force search comparing every particle to every other particle would be prohibitively expensive. On a [structured grid](@entry_id:755573) with spacing $h$, an efficient algorithm involves first identifying a square or cubic [bounding box](@entry_id:635282) around particle $i$ with a side length of approximately $2\delta$. All particles within this box are considered candidates. Then, a final, precise check of the Euclidean distance is performed on these candidates to populate the final [neighbor list](@entry_id:752403), retaining only those for which $\|\mathbf{x}_j - \mathbf{x}_i\| \le \delta$.

#### The Micro-Modulus Function

In bond-based models, the pairwise force is often expressed as $\mathbf{f} = c(\boldsymbol{\xi}) s(\boldsymbol{\eta}, \boldsymbol{\xi}) \frac{\boldsymbol{\xi}+\boldsymbol{\eta}}{|\boldsymbol{\xi}+\boldsymbol{\eta}|}$, where $c(\boldsymbol{\xi})$ is a **micro-modulus function** that represents the stiffness of the bond. For [isotropic materials](@entry_id:170678), $c$ depends only on the initial [bond length](@entry_id:144592), $r = |\boldsymbol{\xi}|$. The function $c(r)$ acts as a kernel or [influence function](@entry_id:168646), weighting the interaction strength of bonds based on their length, and it must have [compact support](@entry_id:276214) (i.e., $c(r) = 0$ for $r > \delta$).

Several choices for this kernel function are common [@problem_id:3549632]:
*   **Constant Kernel:** $c(r) = c_0$ for $r  \delta$. This is the simplest choice but has a [jump discontinuity](@entry_id:139886) at the edge of the horizon ($r=\delta$).
*   **Conical Kernel:** $c(r) = c_1(1-r/\delta)$ for $r  \delta$. This kernel tapers linearly to zero, making it continuous ($C^0$) but not differentiable at $r=\delta$.
*   **Truncated Gaussian Kernel:** $c(r) = c_2\exp(-r^2/\sigma^2)$ for $r  \delta$. This kernel is smooth inside the horizon but, like the constant kernel, generally has a discontinuity at $r=\delta$.

The smoothness of the micro-modulus function has a significant impact on the quality of the numerical solution, particularly in dynamic simulations. Kernels with discontinuities, like the constant kernel, can introduce spurious high-frequency oscillations known as **numerical dispersion**, which contaminates wave propagation results. Smoother kernels, like the conical or a well-chosen truncated Gaussian, suppress these artifacts and generally lead to more accurate dynamic simulations.

#### Time Integration

The spatially discretized peridynamic equations form a large system of [ordinary differential equations](@entry_id:147024) in time. Since the "meshfree" discretization naturally leads to a diagonal (or "lumped") mass matrix, [explicit time integration](@entry_id:165797) schemes are highly efficient and widely used.

A common choice is the **explicit central difference** method [@problem_id:3549610]. At each time step $n$, with step size $\Delta t$, the algorithm proceeds as follows:
1.  Compute accelerations at time $t^n$ from the known forces:
    $$
    \mathbf{a}^n = \mathbf{M}^{-1}(\mathbf{f}^{\mathrm{int},n} + \mathbf{b}^n)
    $$
    where $\mathbf{M}$ is the [diagonal mass matrix](@entry_id:173002), and $\mathbf{f}^{\mathrm{int},n}$ is the vector of internal peridynamic forces calculated at time $t^n$.
2.  Update displacements to time $t^{n+1}$:
    $$
    \mathbf{u}^{n+1} = 2 \mathbf{u}^n - \mathbf{u}^{n-1} + (\Delta t)^2 \mathbf{a}^n
    $$
3.  Update velocities to time $t^n$ (if needed for output or other calculations):
    $$
    \mathbf{v}^n = \frac{\mathbf{u}^{n+1} - \mathbf{u}^{n-1}}{2 \Delta t}
    $$
This scheme is computationally inexpensive as it requires no [matrix inversion](@entry_id:636005) (since $\mathbf{M}$ is diagonal), but it is conditionally stable, meaning the time step $\Delta t$ must be smaller than a critical value determined by the material properties, horizon size, and particle spacing.

### Advanced Modeling Concepts for Geomaterials

To accurately capture the complex behavior of real [geomaterials](@entry_id:749838), the basic peridynamic framework can be extended with more sophisticated models for material properties and boundary interactions.

#### Incorporating Material Heterogeneity

Geomaterials such as rock and concrete are rarely homogeneous. Their [mechanical properties](@entry_id:201145) vary in space due to the presence of different mineral grains, aggregates, pores, and microcracks. This heterogeneity can be incorporated into peridynamic models by treating material parameters, such as the [critical stretch](@entry_id:200184) $s_c$, as a **spatially random field** [@problem_id:3549628].

A physically motivated choice for the statistical distribution of brittle strength is the **Weibull distribution**, which arises from weakest-link theory. To generate a spatially heterogeneous field of $s_c$ values, one can follow a procedure known as the Nataf transformation. First, a standard Gaussian random field with a prescribed spatial **correlation length**, $\ell_c$, is generated. The [correlation length](@entry_id:143364) is a physical parameter representing the characteristic size of microstructural features (e.g., average grain size) and must be independent of numerical parameters like the mesh spacing. Then, a probability [integral transform](@entry_id:195422) is used to map the values of the Gaussian field to a Weibull distribution with the desired mean and variance.

Once the point-wise field $s_c(\mathbf{x})$ is generated, a rule is needed to define the [critical stretch](@entry_id:200184) for a bond connecting two points, $\mathbf{x}$ and $\mathbf{x}'$. A consistent choice based on the weakest-link concept is to set the bond's [critical stretch](@entry_id:200184) to the minimum of the values at its two endpoints: $s_c(\mathbf{x}, \mathbf{x}') = \min\{s_c(\mathbf{x}), s_c(\mathbf{x}')\}$. This approach allows for the simulation of realistic fracture patterns that meander through clusters of weaker material, a phenomenon that cannot be captured by homogeneous models.

#### Boundary Conditions in a Nonlocal Framework

Applying boundary conditions in a [nonlocal theory](@entry_id:752667) like [peridynamics](@entry_id:191791) presents a unique challenge not found in local models. Material points located within a distance $\delta$ of a physical boundary have their horizons truncated, as there are no interacting points outside the domain. This is often called the **"surface effect"**. If unaddressed, this truncation leads to an unphysical reduction in stiffness for near-boundary points, as they have fewer bonds than interior points.

This means that classical (local) boundary conditions, such as the Neumann condition which prescribes the [traction vector](@entry_id:189429) $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$ on the boundary surface, cannot be applied directly. Instead, **nonlocal traction conditions** must be formulated [@problem_id:3549672]. One principled approach is to introduce fictitious forces in a boundary layer of thickness $\delta$ that effectively compensate for the missing interactions from the truncated part of the horizon.

For a prescribed traction $\mathbf{T}(\mathbf{s})$ on a boundary surface $S$, one applies a nonlocal boundary force density $\mathbf{g}_{\mathrm{BC}}(\mathbf{x}, t)$ to material points $\mathbf{x}$ in the boundary layer. This force is defined as an integral of interactions with the "missing" neighbors that would have existed outside the domain. The magnitude and distribution of these interactions are chosen such that the total resultant force applied over the boundary layer equals the total resultant of the desired traction on the surface $S$:
$$
\int_{B_\delta} \mathbf{g}_{\mathrm{BC}}(\mathbf{x}, t) \, dV_{\mathbf{x}} \approx \int_{S} \mathbf{T}(\mathbf{s}, t) \, dS
$$
where $B_{\delta}$ is the boundary layer. Unlike the pointwise local Neumann condition, the peridynamic traction condition is inherently nonlocal, depending on the geometry of the truncated horizon and requiring forces to be applied over a volume rather than just on a surface. A traction-free (natural) boundary condition is simpler to implement: one simply applies no compensating forces, reflecting the physical reality that there are no material bonds outside the body to exert forces.