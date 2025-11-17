## Introduction
Plastic deformation in [crystalline materials](@entry_id:157810) like metals is not a result of atomic planes shearing simultaneously, but rather the sequential movement of linear defects known as dislocations. While these defects are microscopic, their collective behavior dictates macroscopic properties like strength and ductility. A central challenge in materials science is to bridge this scale gap, connecting the physics of a single defect to the observable mechanical response of a material. The concept of a [configurational force](@entry_id:187765) acting on the dislocation provides this crucial link.

This article provides a comprehensive overview of [dislocation mechanics](@entry_id:203892), focusing on the central concept of the Peach-Koehler force. In the first chapter, **Principles and Mechanisms**, we will establish the fundamental continuum description of a dislocation, exploring its geometry, its associated elastic fields, and the formal derivation of the force that governs its motion. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the power of this framework by applying the Peach-Koehler force to explain a wide range of [critical phenomena](@entry_id:144727), from [dislocation interactions](@entry_id:181480) and multiplication to the various [strengthening mechanisms](@entry_id:158922) that are key to engineering advanced materials. Finally, the **Hands-On Practices** section will allow you to solidify your understanding by applying these principles to solve canonical problems in [dislocation theory](@entry_id:160051).

## Principles and Mechanisms

### Defining the Dislocation: Geometry and Topology

Dislocations are linear defects in a [crystalline lattice](@entry_id:196752), and their existence and motion are the primary mechanisms responsible for [plastic deformation in metals](@entry_id:180560) and other crystalline materials. While they are discrete defects at the atomic scale, their influence extends over macroscopic distances through long-range elastic fields. Continuum mechanics provides a powerful framework for understanding this behavior by modeling the dislocation as a line singularity within an elastic medium.

#### The Burgers Circuit and Burgers Vector

The defining characteristic of a dislocation is the lattice distortion it creates. This distortion can be precisely quantified by a topological invariant known as the **Burgers vector**, denoted by $\mathbf{b}$. To determine the Burgers vector, we employ a conceptual tool called the **Burgers circuit**.

Imagine a perfect, defect-free crystal serving as a reference lattice. Within this reference lattice, we can trace a closed loop by taking a sequence of discrete lattice steps (e.g., 10 steps right, 10 steps up, 10 steps left, 10 steps down), returning precisely to the starting point. Now, we attempt to replicate this exact same sequence of lattice steps in the real, defective crystal, ensuring the path encloses the dislocation line. Due to the distortion caused by the dislocation, this path will fail to close. The vector required to close the loop—that is, the vector from the finish point back to the start point—is the Burgers vector $\mathbf{b}$.

To make this definition unambiguous, we must establish a convention relating the direction of the dislocation line to the sense in which the Burgers circuit is traversed. A widely adopted standard is the **FS/RH (Finish-to-Start/Right-Hand) convention**. First, we assign a sense or direction to the dislocation line, represented by a [unit tangent vector](@entry_id:262985) $\boldsymbol{\xi}$. Then, with the thumb of the right hand pointing in the direction of $\boldsymbol{\xi}$, the fingers curl in the direction that the Burgers circuit should be traversed. With this established, the Burgers vector $\mathbf{b}$ is defined as the vector drawn from the finish point (F) of the circuit to the start point (S) [@problem_id:2630988].

The Burgers vector is a fundamental property of a dislocation. Its magnitude and direction are conserved along the dislocation line, meaning a dislocation line cannot end inside a crystal; it must either form a closed loop, terminate at a free surface, or end at a [grain boundary](@entry_id:196965) or another dislocation node. For a crystalline solid, $\mathbf{b}$ must be a lattice translation vector, as a displacement by $\mathbf{b}$ must bring the lattice back into registry with itself.

#### The Volterra Construction

The concept of the Burgers vector can be visualized elegantly through the **Volterra construction**, a process in [continuum elasticity](@entry_id:182845) for creating a dislocation. The process involves three steps:

1.  **Cut:** Imagine making a cut into a continuous elastic body along a surface $A$. The boundary of this cut surface is the dislocation line, $\boldsymbol{\xi}$.
2.  **Displace:** The two faces of the cut are rigidly displaced relative to one another by the Burgers vector, $\mathbf{b}$.
3.  **Weld:** Material is added or removed as necessary to fill any gaps or remove overlaps, and the faces are welded back together.

Upon releasing the body, it settles into a new equilibrium state characterized by an [internal stress](@entry_id:190887) field. This final state contains a dislocation along the boundary of the original cut. The choice of the cut surface $A$ is arbitrary; any surface bounded by the line $\boldsymbol{\xi}$ will produce the same dislocation and the same long-range elastic fields. The displacement jump across the cut surface, however, is what defines the dislocation's character [@problem_id:2630988].

#### Types of Dislocations: Edge, Screw, and Mixed

The geometric relationship between the Burgers vector $\mathbf{b}$ and the line tangent vector $\boldsymbol{\xi}$ determines the character of the dislocation.

An **edge dislocation** is characterized by a Burgers vector that is perpendicular to the dislocation line, i.e., $\mathbf{b} \perp \boldsymbol{\xi}$. In the Volterra construction, this corresponds to a displacement normal to the line, which can be visualized as inserting or removing an extra half-plane of atoms. The edge of this half-plane constitutes the dislocation line.

A **[screw dislocation](@entry_id:161513)** is characterized by a Burgers vector that is parallel to the dislocation line, i.e., $\mathbf{b} \parallel \boldsymbol{\xi}$. The Volterra construction involves a displacement parallel to the line, creating a shear-like offset. This transforms the parallel atomic planes of the crystal into a single helical surface, or ramp, centered on the dislocation line.

Most dislocations in real materials are neither pure edge nor pure screw but have a **mixed character**. For a [mixed dislocation](@entry_id:191088), the Burgers vector lies at an angle to the line tangent. We can define the **character angle**, $\chi$, as the angle between the Burgers vector and the line direction:
$$
\chi = \arccos\left(\frac{\mathbf{b} \cdot \boldsymbol{\xi}}{||\mathbf{b}||}\right)
$$
A pure screw dislocation corresponds to $\chi = 0$, and a pure [edge dislocation](@entry_id:160353) corresponds to $\chi = \pi/2$. For any [mixed dislocation](@entry_id:191088) ($0  \chi  \pi$), the Burgers vector $\mathbf{b}$ can be uniquely decomposed into a **screw component**, $\mathbf{b}_s$, parallel to $\boldsymbol{\xi}$, and an **edge component**, $\mathbf{b}_e$, perpendicular to $\boldsymbol{\xi}$ [@problem_id:2630959].
$$
\mathbf{b} = \mathbf{b}_s + \mathbf{b}_e
$$
Using [vector projection](@entry_id:147046), we find:
$$
\mathbf{b}_s = (\mathbf{b} \cdot \boldsymbol{\xi}) \boldsymbol{\xi} \implies ||\mathbf{b}_s|| = |\mathbf{b} \cdot \boldsymbol{\xi}| = ||\mathbf{b}|| |\cos\chi|
$$
$$
\mathbf{b}_e = \mathbf{b} - \mathbf{b}_s \implies ||\mathbf{b}_e|| = \sqrt{||\mathbf{b}||^2 - ||\mathbf{b}_s||^2} = ||\mathbf{b}|| |\sin\chi|
$$
This decomposition is powerful because the elastic fields of a [mixed dislocation](@entry_id:191088) can often be approximated by the superposition of the fields of its pure screw and pure edge components.

It is important to note that the character angle $\chi$ depends on the chosen line sense $\boldsymbol{\xi}$. If the line sense is reversed, $\boldsymbol{\xi} \mapsto -\boldsymbol{\xi}$, the Burgers vector $\mathbf{b}$ remains unchanged. The new character angle $\chi'$ becomes $\chi' = \arccos(-\cos\chi) = \pi - \chi$ [@problem_id:2630959]. This sign convention is crucial for the consistent calculation of forces on dislocations.

### The Elastic Fields of Dislocations

The lattice distortion created by a dislocation does not remain localized to the core. It gives rise to long-range strain and stress fields that permeate the surrounding crystal. These fields decay slowly with distance, typically as $1/r$, where $r$ is the distance from the dislocation line. It is through these elastic fields that dislocations interact with each other, with external applied stresses, and with other crystal defects like precipitates and [grain boundaries](@entry_id:144275).

#### The Screw Dislocation Field

The screw dislocation provides the simplest case for analysis. For a straight screw dislocation along the $z$-axis with Burgers vector $\mathbf{b} = b\,\mathbf{e}_z$, the [displacement field](@entry_id:141476) in [cylindrical coordinates](@entry_id:271645) $(r, \theta, z)$ is purely axial:
$$
u_r = 0, \quad u_\theta = 0, \quad u_z = \frac{b}{2\pi}\theta
$$
This displacement field describes the helical ramp structure. The field is multi-valued due to the term $\theta$; each full circuit around the origin increases or decreases $u_z$ by $b$. However, [physical quantities](@entry_id:177395) like strain and stress must be single-valued. The strain components are found by differentiating the displacement field. The only non-zero strain component is:
$$
\varepsilon_{\theta z} = \frac{1}{2}\left(\frac{1}{r}\frac{\partial u_z}{\partial \theta} + \frac{\partial u_\theta}{\partial z}\right) = \frac{1}{2r}\left(\frac{b}{2\pi}\right) = \frac{b}{4\pi r}
$$
Using Hooke's law for an [isotropic material](@entry_id:204616) in shear, $\sigma_{ij} = 2\mu\varepsilon_{ij}$ (where $\mu$ is the shear modulus), the only non-zero stress component is:
$$
\sigma_{\theta z} = 2\mu\varepsilon_{\theta z} = \frac{\mu b}{2\pi r}
$$
This is the fundamental stress field of a screw dislocation. It is a pure shear stress acting on radial planes in the axial direction, and it decays as $1/r$ from the dislocation line [@problem_id:2631026].

#### The Edge Dislocation Field

The fields of an edge dislocation are more complex as they involve both shear and [normal stress](@entry_id:184326) components, requiring a [plane strain](@entry_id:167046) analysis. Consider a positive edge dislocation with line sense $\boldsymbol{\xi} = \mathbf{e}_z$ and Burgers vector $\mathbf{b} = b\,\mathbf{e}_x$.

A key feature of the edge dislocation's [displacement field](@entry_id:141476), $\mathbf{u}(x,y)$, is its discontinuity across the [slip plane](@entry_id:275308). The Volterra construction specifies that a cut is made on a surface and a relative displacement of $\mathbf{b}$ is imposed. For a positive [edge dislocation](@entry_id:160353), this cut can be taken along the negative $x$-axis ($y=0, x0$). The displacement jump across this cut is exactly the Burgers vector: $\Delta\mathbf{u}(x) = \mathbf{u}(x, 0^+) - \mathbf{u}(x, 0^-) = \mathbf{b}$ for $x0$. Where there is no cut ($x>0$), the material is continuous, so the jump is zero. This can be expressed concisely for the $x$-component of displacement using the Heaviside [step function](@entry_id:158924) $H(\cdot)$:
$$
\Delta u_x(x) = b H(-x)
$$
This expression captures that the jump of magnitude $b$ occurs only for $x0$ [@problem_id:2630989].

The [displacement field](@entry_id:141476) itself is multi-valued, typically containing a term proportional to the [polar angle](@entry_id:175682) $\theta = \arctan(y/x)$. However, as with the [screw dislocation](@entry_id:161513), the strain and stress fields are derivatives of displacement and are consequently single-valued everywhere away from the core singularity ($r>0$). The [strain tensor](@entry_id:193332) $\boldsymbol{\varepsilon} = \frac{1}{2}[\nabla\mathbf{u} + (\nabla\mathbf{u})^T]$ is single-valued because the gradient of the multi-valued part of the displacement is itself a single-valued function. Since stress is linearly related to strain via Hooke's Law, $\boldsymbol{\sigma}$ is also single-valued [@problem_id:2630989].

To find the stress field, one can use an **Airy stress function**, $\Phi$, which automatically satisfies the [equilibrium equations](@entry_id:172166) ($\nabla \cdot \boldsymbol{\sigma} = 0$) in [plane strain](@entry_id:167046). For an [edge dislocation](@entry_id:160353), the appropriate function that respects the problem's symmetry and singularity is of the form $\Phi(x,y) = -D y \ln(r^2)$, where $D$ is a constant related to the material properties and Burgers vector. The stress components are derived from second derivatives of $\Phi$, such as $\sigma_{xx} = \partial^2\Phi/\partial y^2$ and $\sigma_{yy} = \partial^2\Phi/\partial x^2$. These stresses exhibit the characteristic $1/r$ decay. A particularly important quantity is the hydrostatic stress, which is the trace of the in-plane stress tensor. In [polar coordinates](@entry_id:159425), this is found to be [@problem_id:2631038]:
$$
\sigma_{xx} + \sigma_{yy} = -\frac{\mu b \sin\theta}{\pi(1-\nu)r}
$$
where $\nu$ is Poisson's ratio. This result reveals a fundamental property of [edge dislocations](@entry_id:191098): there is a region of compression ($\sin\theta > 0$, or $0  \theta  \pi$) above the [slip plane](@entry_id:275308) where the extra half-plane resides, and a region of tension ($\sin\theta  0$, or $\pi  \theta  2\pi$) below it. This hydrostatic field is responsible for the interaction of [edge dislocations](@entry_id:191098) with solute atoms, leading to phenomena like [solid-solution strengthening](@entry_id:137856).

### The Elastic Energy of Dislocations

The [stress and strain](@entry_id:137374) fields surrounding a dislocation represent stored elastic energy. This energy is a crucial aspect of [dislocation theory](@entry_id:160051), influencing dislocation stability, interactions, and the formation of dislocation patterns. The [elastic strain energy](@entry_id:202243) per unit volume is given by $w = \frac{1}{2}\sigma_{ij}\varepsilon_{ij}$.

#### The Core Cutoff and Logarithmic Divergence

A direct calculation of the total energy by integrating $w$ over all space runs into a problem. Since stress fields vary as $1/r$, the [strain energy density](@entry_id:200085) $w$ varies as $1/r^2$. The integral of energy per unit length involves an area element $dA = r\,dr\,d\theta$, leading to a radial integral of the form $\int (1/r^2) r\,dr = \int (1/r)dr = \ln(r)$. This integral diverges logarithmically at both small and large distances.

This divergence is handled by introducing two cutoff radii:
1.  An **inner core [cutoff radius](@entry_id:136708), $r_0$**, typically on the order of a few Burgers vector magnitudes. This excludes the region near the line where strains are enormous and linear elasticity breaks down. The energy within this core region, the **core energy**, is a separate, constant contribution.
2.  An **outer [cutoff radius](@entry_id:136708), $R$**, which represents a physical length scale like the crystal size or the average distance to a neighboring dislocation that screens the stress field.

The elastic energy is then calculated by integrating from $r_0$ to $R$. This regularization procedure correctly captures the dominant contribution to the dislocation's energy [@problem_id:2630961].

#### Energy of a Screw Dislocation

For a straight [screw dislocation](@entry_id:161513), integrating the energy density $w = \mu b^2 / (8\pi^2 r^2)$ over the [annulus](@entry_id:163678) from $r_0$ to $R$ yields the elastic energy per unit length [@problem_id:2631026]:
$$
U_{\text{screw}} = \int_0^{2\pi}\int_{r_0}^R \frac{\mu b^2}{8\pi^2 r^2} r\,dr\,d\theta = \frac{\mu b^2}{4\pi} \ln\left(\frac{R}{r_0}\right)
$$

#### Energy of an Edge Dislocation

The same procedure can be applied to an edge dislocation. The calculation is more complex due to the multiple stress components, but it yields a similar logarithmic form. A convenient way to derive the result is to equate the stored energy with the work done to create the dislocation. The energy is one-half the work done by the final shear stress $\tau(x)$ on the [slip plane](@entry_id:275308) acting over the displacement $b$. This gives [@problem_id:2631021]:
$$
U_{\text{edge}} = \frac{1}{2} \int_{r_0}^R \tau(x) b\,dx
$$
Using the known shear stress on the slip plane for an edge dislocation, $\tau(x) = \sigma_{xy}(x,0) = \frac{\mu b}{2\pi(1-\nu)x}$, integration gives:
$$
U_{\text{edge}} = \frac{\mu b^2}{4\pi(1-\nu)} \ln\left(\frac{R}{r_0}\right)
$$
Comparing the energies of [screw and edge dislocations](@entry_id:146151), we see the term $1/(1-\nu)$. Since $0  \nu  0.5$ for most materials, this factor is greater than 1, meaning that an [edge dislocation](@entry_id:160353) has a higher elastic energy per unit length than a screw dislocation of the same Burgers vector. The presence of Poisson's ratio $\nu$ reflects the fact that the [edge dislocation](@entry_id:160353)'s field involves volume changes (compression and tension), and the plane strain constraint ($\varepsilon_{zz}=0$) imposes an additional stiffness to this mode of deformation [@problem_id:2631021].

### The Peach-Koehler Force: Driving Dislocation Motion

The central question in plasticity is what causes dislocations to move. The answer lies in the concept of a [configurational force](@entry_id:187765), a [thermodynamic force](@entry_id:755913) that acts on defects to lower the total energy of the system. For dislocations, this is known as the **Peach-Koehler force**.

#### Conceptual Derivation from Virtual Work

The Peach-Koehler force can be derived by considering the virtual work done by a stress field $\boldsymbol{\sigma}$ when a dislocation segment moves. Consider an infinitesimal dislocation element $d\mathbf{l} = \boldsymbol{\xi}\,ds$, where $\boldsymbol{\xi}$ is the local tangent vector. If this element undergoes a [virtual displacement](@entry_id:168781) $\delta\mathbf{x}$, it sweeps out an area $d\mathbf{A} = d\mathbf{l} \times \delta\mathbf{x}$. This movement corresponds to the extension of the slip surface, across which there is a displacement discontinuity of $\mathbf{b}$. The work done by the traction $\boldsymbol{\sigma}\cdot\mathbf{n}$ on this new surface element is $\delta W = (\boldsymbol{\sigma}\cdot\mathbf{n})\cdot\mathbf{b}\,dA = (\boldsymbol{\sigma}\mathbf{b})\cdot d\mathbf{A}$.

By relating this work to the definition of force, $\delta W = \mathbf{f} \cdot \delta\mathbf{x} \,ds$, one arrives at the celebrated **Peach-Koehler formula** for the local force per unit length on a potentially curved dislocation line [@problem_id:2631018]:
$$
\mathbf{f}(s) = (\boldsymbol{\sigma}\mathbf{b}) \times \boldsymbol{\xi}(s)
$$
Here, $\boldsymbol{\sigma}$ is the stress tensor evaluated at the position of the line element, and it includes stresses from all sources *except* the self-stress of the element itself. The force is always perpendicular to the dislocation line, as evident from the [cross product](@entry_id:156749) with $\boldsymbol{\xi}$. Rigorous derivations based on principles of [material frame indifference](@entry_id:166014) confirm that this tensorial structure is essentially unique, given certain physical axioms like the force being orthogonal to the line tangent [@problem_id:2631027].

For a straight dislocation, $\boldsymbol{\xi}$ is constant, and the formula simplifies to $\mathbf{f} = (\boldsymbol{\sigma}\mathbf{b}) \times \boldsymbol{\xi}$. If the line is curved, the force $\mathbf{f}(s)$ varies along its length because the [tangent vector](@entry_id:264836) $\boldsymbol{\xi}(s)$ changes, even if the stress $\boldsymbol{\sigma}$ is uniform. Curvature does not appear explicitly in the formula, but it determines the local orientation of the line, which in turn determines the force [@problem_id:2631018].

#### Dislocation Glide and Resolved Shear Stress

Dislocation motion is most commonly **glide**, where the dislocation moves within its **slip plane**, the plane containing both its line tangent $\boldsymbol{\xi}$ and its Burgers vector $\mathbf{b}$ (for an edge dislocation) or any plane containing the line (for a screw dislocation). Motion out of the slip plane, called **climb**, is a much slower, [thermally activated process](@entry_id:274558) requiring diffusion of vacancies or [interstitials](@entry_id:139646).

Glide is driven by the component of the Peach-Koehler force lying in the [slip plane](@entry_id:275308). This force component is directly related to the **[resolved shear stress](@entry_id:201022)** ($\tau_{RSS}$ or simply $\tau$), a concept central to [crystal plasticity](@entry_id:141273) known as **Schmid's Law**. For a given [slip system](@entry_id:155264) defined by a slip plane normal $\mathbf{n}$ and a slip direction $\mathbf{s}$, the [resolved shear stress](@entry_id:201022) is the scalar component of the [traction vector](@entry_id:189429) on the slip plane, $\mathbf{T} = \boldsymbol{\sigma}\mathbf{n}$, projected onto the slip direction:
$$
\tau = \mathbf{s} \cdot \mathbf{T} = \mathbf{s} \cdot (\boldsymbol{\sigma}\mathbf{n}) = s_i \sigma_{ij} n_j
$$
Now, consider the component of the Peach-Koehler force that drives glide. This **glide force**, $f_g$, performs work as the dislocation moves. By equating the work done by the glide force, $f_g\,dx$, with the work done by the external stress field as the slip surface is created, $(\mathbf{b}\cdot(\boldsymbol{\sigma}\mathbf{n}))\,dA$, it can be shown that the magnitude of the glide force per unit length is simply [@problem_id:2631012]:
$$
f_g = \tau b
$$
where $b$ is the magnitude of the Burgers vector and $\tau$ is the [resolved shear stress](@entry_id:201022) in the direction of the Burgers vector. This is a cornerstone equation of [dislocation mechanics](@entry_id:203892), directly linking the macroscopic stress state ($\boldsymbol{\sigma}$), the crystal orientation ($\mathbf{n}, \mathbf{s}$), and the microscopic force driving plastic deformation ($f_g$). Plastic deformation occurs when $\tau$ reaches a critical value, the **[critical resolved shear stress](@entry_id:159240)** ($\tau_{CRSS}$), sufficient to move dislocations through the crystal lattice.

For example, consider a [mixed dislocation](@entry_id:191088) under a state of pure shear stress $\boldsymbol{\sigma}=\tau_{ext}(\mathbf{e}_2\otimes\mathbf{e}_3+\mathbf{e}_3\otimes\mathbf{e}_2)$. If the dislocation line is along $\mathbf{e}_3$, the force is $\mathbf{f} = (\boldsymbol{\sigma}\mathbf{b}) \times \mathbf{e}_3$. The term $\boldsymbol{\sigma}\mathbf{b}$ depends only on the component of $\mathbf{b}$ along $\mathbf{e}_3$, i.e., the screw component $b_s = b_0\cos\chi$. The resulting glide force is found to be $f_g = \tau_{ext} b_0 \cos\chi = \tau_{ext} b_s$. This demonstrates how different components of the applied stress interact with different components of the Burgers vector to produce a force [@problem_id:2630959].

Crucially, the Peach-Koehler force from an externally applied stress field $\boldsymbol{\sigma}_{ext}$ is independent of the dislocation's own complex stress field and its core structure. Therefore, the force $f_g = b\tau_{ext}$ does not depend on the core radius $r_0$ or material parameters like $\mu$ and $\nu$ that govern the self-energy. It is a direct interaction between the defect, characterized by $\mathbf{b}$, and the external field [@problem_id:2630961].