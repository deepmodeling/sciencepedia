## Introduction
Dislocations are line defects within [crystalline solids](@entry_id:140223) that are fundamental to understanding their mechanical behavior. The presence of a single dislocation profoundly alters a material's properties, not at the line itself, but through the long-range stress and displacement fields it projects into the surrounding lattice. Mastering the mechanics of these fields is the cornerstone for explaining phenomena from [plastic deformation](@entry_id:139726) to the strengthening of advanced alloys. This article addresses the challenge of quantitatively describing these fields and their consequences.

Across the following chapters, you will gain a comprehensive understanding of [dislocation theory](@entry_id:160051). We will begin by deriving the stress, displacement, and energy expressions for fundamental dislocation types using [continuum elasticity](@entry_id:182845). We will then explore the practical applications of these principles, examining how dislocations interact with each other and other defects to govern plasticity, microstructural evolution, and a variety of [materials engineering](@entry_id:162176) strategies. Finally, a set of hands-on problems will allow you to apply these theoretical concepts to practical scenarios. This journey will take you from the mathematical foundation of a single defect to its role in complex material phenomena.

## Principles and Mechanisms

The presence of dislocations fundamentally alters the mechanical and physical properties of crystalline materials. This is a direct consequence of the long-range displacement and stress fields that emanate from the dislocation line. In this chapter, we will develop a quantitative understanding of these fields using the framework of [continuum elasticity](@entry_id:182845) theory. We will begin by establishing the fundamental definition of a dislocation through its displacement field and Burgers vector, then proceed to derive the specific stress and energy expressions for the primary types of dislocations. Finally, we will explore more advanced topics, including the interaction between dislocations, the structure of the [dislocation core](@entry_id:201451), and the effects of [material anisotropy](@entry_id:204117), culminating in a continuum description of dislocation ensembles.

### The Burgers Vector and the Displacement Field

A dislocation is a line defect that creates a **displacement field**, denoted by the vector $\mathbf{u}(\mathbf{r})$, throughout the surrounding crystal. This field describes the vector displacement of any point $\mathbf{r}$ from its position in a perfect, undeformed lattice. The most crucial characteristic of a dislocation, which quantifies the magnitude and direction of the permanent lattice distortion it introduces, is the **Burgers vector**, $\mathbf{b}$.

Formally, the Burgers vector is defined by a [line integral](@entry_id:138107) of the differential displacement, $d\mathbf{u}$, around any closed loop $C$ that encloses the dislocation line. This loop is known as a **Burgers circuit**.

$$ \mathbf{b} = \oint_C d\mathbf{u} $$

In a perfect crystal, the displacement field $\mathbf{u}$ is single-valued, and this integral would be zero for any closed path. However, the presence of a dislocation renders the displacement field multi-valued. This means that traversing a closed loop around the dislocation line results in a net change in the [displacement vector](@entry_id:262782), a "closure failure," which is precisely the Burgers vector. The Burgers vector is a constant for a given dislocation, independent of the specific path of the Burgers circuit, making it a [topological invariant](@entry_id:142028) of the defect.

To understand how different parts of a displacement field contribute to the Burgers vector, let's analyze a hypothetical [displacement field](@entry_id:141476) surrounding a straight dislocation aligned with the $z$-axis [@problem_id:216612]. The field is given by:

$$ \mathbf{u}(x,y) = \left( A \arctan\left(\frac{y}{x}\right) + B \frac{xy}{x^2+y^2} \right) \hat{\mathbf{i}} + \left( E \arctan\left(\frac{y}{x}\right) + C \ln(x^2+y^2) + D \frac{y^2-x^2}{x^2+y^2} \right) \hat{\mathbf{j}} $$

To calculate the Burgers vector, we evaluate the change in $\mathbf{u}$ over a complete counter-clockwise circle around the origin. It is convenient to switch to [polar coordinates](@entry_id:159425), where $x=r\cos\theta$, $y=r\sin\theta$, and the multi-valued term $\arctan(y/x)$ becomes the polar angle $\theta$. The [displacement field](@entry_id:141476) transforms to:

$$ u_x(r,\theta) = A\theta + \frac{B}{2}\sin(2\theta) $$
$$ u_y(r,\theta) = E\theta + 2C\ln r - D\cos(2\theta) $$

We evaluate the displacement at a starting point, say $(r, \theta=0)$, and an ending point which is geometrically identical but corresponds to $\theta=2\pi$. The Burgers vector $\mathbf{b} = \mathbf{u}(r, 2\pi) - \mathbf{u}(r, 0)$.
For the $x$-component:
$$ b_x = u_x(r, 2\pi) - u_x(r, 0) = \left( A(2\pi) + \frac{B}{2}\sin(4\pi) \right) - \left( A(0) + \frac{B}{2}\sin(0) \right) = 2\pi A $$
For the $y$-component:
$$ b_y = u_y(r, 2\pi) - u_y(r, 0) = \left( E(2\pi) + 2C\ln r - D\cos(4\pi) \right) - \left( E(0) + 2C\ln r - D\cos(0) \right) = 2\pi E $$

The resulting Burgers vector is $\mathbf{b} = 2\pi A \hat{\mathbf{i}} + 2\pi E \hat{\mathbf{j}}$. This calculation reveals a critical principle: only the terms that are inherently multi-valued, those proportional to the angle $\theta$, contribute to the Burgers vector. The other terms, which represent single-valued elastic distortions of the lattice (like the terms with coefficients $B$, $C$, and $D$), return to their original values after a full circle and thus do not contribute.

### Elastic Fields of Straight Dislocations in Isotropic Media

Within the framework of linear [isotropic elasticity](@entry_id:203237), we can derive analytical expressions for the displacement and stress fields of simple straight dislocations. A straight dislocation is characterized by its line vector $\mathbf{t}$, a [unit vector](@entry_id:150575) parallel to the dislocation line, and its Burgers vector $\mathbf{b}$. The orientation of $\mathbf{b}$ relative to $\mathbf{t}$ defines the dislocation's character.

#### The Fundamental Types: Edge, Screw, and Mixed

There are two fundamental types of dislocations:

1.  **Edge Dislocation**: The Burgers vector is perpendicular to the dislocation line ($\mathbf{b} \perp \mathbf{t}$). This can be visualized as the edge of an extra half-plane of atoms inserted into the crystal.
2.  **Screw Dislocation**: The Burgers vector is parallel to the dislocation line ($\mathbf{b} \parallel \mathbf{t}$). This transforms the [crystal planes](@entry_id:142849) into a single helical surface, or helicoid.

A general dislocation line that is not perfectly straight or whose Burgers vector is neither parallel nor perpendicular to the line vector can be described locally as a **[mixed dislocation](@entry_id:191088)**. A straight [mixed dislocation](@entry_id:191088) has a Burgers vector with both edge and screw components relative to the line vector.

#### The Screw Dislocation

The screw dislocation is the simplest case. For a [screw dislocation](@entry_id:161513) along the $z$-axis with Burgers vector $\mathbf{b} = b\hat{\mathbf{z}}$, the only non-zero displacement is in the $z$-direction:

$$ u_z = \frac{b}{2\pi}\theta = \frac{b}{2\pi}\arctan\left(\frac{y}{x}\right) $$

The displacement components $u_x$ and $u_y$ are zero. The [strain tensor](@entry_id:193332) components are found by differentiating the displacement field. The only non-zero components are the shear strains $\epsilon_{\theta z}$ and $\epsilon_{z\theta}$. In cylindrical coordinates, this gives:
$$ \epsilon_{\theta z} = \frac{1}{2r}\frac{\partial u_z}{\partial \theta} = \frac{b}{4\pi r} $$
Using Hooke's Law for an isotropic solid, $\sigma_{ij} = 2G\epsilon_{ij}$ for shear components, where $G$ is the shear modulus (sometimes denoted $\mu$), we find the only non-zero stress components:
$$ \sigma_{\theta z} = \sigma_{z\theta} = 2G\epsilon_{\theta z} = \frac{Gb}{2\pi r} $$

The stress field of a [screw dislocation](@entry_id:161513) is one of pure shear, is cylindrically symmetric, and diverges as $1/r$ as one approaches the [dislocation core](@entry_id:201451) ($r \to 0$). This singularity is an artifact of linear elasticity theory, which we will address later.

To appreciate the magnitude of this stress state, we can compute the **von Mises [equivalent stress](@entry_id:749064)**, $\sigma_v$, a scalar quantity used to predict yielding in ductile materials. For the [screw dislocation](@entry_id:161513)'s stress tensor, with all normal stresses and other shear stresses being zero [@problem_id:216620], the von Mises stress simplifies to:
$$ \sigma_v = \sqrt{3(\sigma_{\theta z}^2)} = \sqrt{3} |\sigma_{\theta z}| = \frac{\sqrt{3} G b}{2\pi r} $$
This confirms that the effective stress also decays as $1/r$ from the dislocation line.

#### The Edge Dislocation

For an [edge dislocation](@entry_id:160353) along the $z$-axis with $\mathbf{b} = b\hat{\mathbf{x}}$, the displacement field is more complex and involves both $x$ and $y$ components. As demonstrated by applying the Burgers circuit definition [@problem_id:216687], the displacement in the direction of the Burgers vector, $u_x$, contains the multi-valued $\theta$ term required to produce the closure failure:

$$ u_x(r, \theta) = \frac{b}{2\pi} \left[ \theta + \frac{\sin(2\theta)}{4(1-\nu)} \right] $$

Here, $\nu$ is the Poisson's ratio. The net change $\Delta u_x$ after one circuit ($\theta$ from $0$ to $2\pi$) is precisely $b$, while the other displacement component, $u_y$, is single-valued and has no net change.

The stress field of an [edge dislocation](@entry_id:160353) is also more complex than that of a screw dislocation. It has both normal and shear components, and lacks [cylindrical symmetry](@entry_id:269179). In Cartesian coordinates, the key stress components are [@problem_id:216544]:

$$ \sigma_{xx} = -\frac{G b}{2\pi(1-\nu)} \frac{y(3x^2 + y^2)}{(x^2+y^2)^2} $$
$$ \sigma_{yy} = \frac{G b}{2\pi(1-\nu)} \frac{y(x^2 - y^2)}{(x^2+y^2)^2} $$
$$ \sigma_{xy} = \frac{G b}{2\pi(1-\nu)} \frac{x(x^2 - y^2)}{(x^2+y^2)^2} $$

These equations reveal a state of tension ($\sigma_{xx} > 0$) for $y  0$ and compression ($\sigma_{xx}  0$) for $y > 0$ (assuming $b>0$), corresponding to the region below and above the extra half-plane, respectively. The shear stress $\sigma_{xy}$ is concentrated on the [slip plane](@entry_id:275308) ($y=0$). All stress components again exhibit the characteristic $1/r$ divergence at the core.

#### The Mixed Dislocation

The power of [linear elasticity](@entry_id:166983) lies in the **principle of superposition**. The total stress or displacement field from multiple sources is simply the sum of the fields from each source individually. This principle allows us to easily determine the field of a [mixed dislocation](@entry_id:191088). A [mixed dislocation](@entry_id:191088) with Burgers vector $\mathbf{b}$ and line vector $\mathbf{t}$ can be decomposed into a pure screw component with Burgers vector $\mathbf{b}_s = (\mathbf{b} \cdot \mathbf{t})\mathbf{t}$ and a pure edge component with Burgers vector $\mathbf{b}_e = \mathbf{b} - \mathbf{b}_s$.

Let $\beta$ be the angle between $\mathbf{b}$ and $\mathbf{t}$. Then the magnitudes of the component Burgers vectors are $b_s = b\cos\beta$ and $b_e = b\sin\beta$. The total stress field is $\boldsymbol{\sigma}^{\text{mixed}} = \boldsymbol{\sigma}^{\text{screw}}(\mathbf{b}_s) + \boldsymbol{\sigma}^{\text{edge}}(\mathbf{b}_e)$. As a direct illustration [@problem_id:216660], let's find the shear stress component $\sigma_{\theta z}$ for a [mixed dislocation](@entry_id:191088).
The screw component contributes:
$$ \sigma_{\theta z}^s = \frac{G b_s}{2\pi r} = \frac{G b \cos\beta}{2\pi r} $$
The edge component, by its nature, produces no stresses in the $z$-direction (i.e., $\sigma_{xz}^e = \sigma_{yz}^e = 0$). Therefore, its contribution to $\sigma_{\theta z}$ is zero. By superposition, the total stress is:
$$ \sigma_{\theta z}^{\text{mixed}} = \sigma_{\theta z}^s + \sigma_{\theta z}^e = \frac{G b \cos\beta}{2\pi r} $$
This result elegantly shows that this particular shear stress component depends only on the screw character of the [mixed dislocation](@entry_id:191088).

### The Strain Energy of Dislocations

The elastic distortion of the lattice surrounding a dislocation stores energy. This **[elastic strain energy](@entry_id:202243)** is a primary factor governing [dislocation motion](@entry_id:143448), interaction, and stability. We can calculate this energy by integrating the [strain energy density](@entry_id:200085), $w = \frac{1}{2}\sigma_{ij}\epsilon_{ij}$, over the volume of the material.

Let us perform this calculation for a screw dislocation per unit length [@problem_id:216679]. The [strain energy density](@entry_id:200085) is:
$$ w = \frac{1}{2} (\sigma_{\theta z}\epsilon_{\theta z} + \sigma_{z\theta}\epsilon_{z\theta}) = \sigma_{\theta z}\epsilon_{\theta z} = \left(\frac{Gb}{2\pi r}\right)\left(\frac{b}{4\pi r}\right) = \frac{G b^2}{8\pi^2 r^2} $$
To find the energy per unit length, $E$, we integrate $w$ over an [area element](@entry_id:197167) $dA = 2\pi r dr$. The integral must exclude the [dislocation core](@entry_id:201451), where linear elasticity breaks down, and is typically taken over an [annulus](@entry_id:163678) from an inner core radius $r_0$ to an outer [cutoff radius](@entry_id:136708) $R$ (e.g., the crystal size).
$$ E = \int_{r_0}^{R} w(r) \, (2\pi r \, dr) = \int_{r_0}^{R} \frac{G b^2}{8\pi^2 r^2} \, (2\pi r \, dr) = \frac{G b^2}{4\pi} \int_{r_0}^{R} \frac{dr}{r} $$
$$ E_{\text{screw}} = \frac{G b^2}{4\pi} \ln\left(\frac{R}{r_0}\right) $$
The energy is proportional to $G$ and $b^2$, a general result indicating that stiffer materials and larger lattice distortions store more energy. The logarithmic dependence on the crystal dimensions signifies the long-range nature of the strain field. A similar calculation for an [edge dislocation](@entry_id:160353) yields:
$$ E_{\text{edge}} = \frac{G b^2}{4\pi(1-\nu)} \ln\left(\frac{R}{r_0}\right) $$
Since $0 \lt \nu \lt 0.5$, the term $(1-\nu)$ is less than 1, meaning that an [edge dislocation](@entry_id:160353) generally has a higher energy per unit length than a [screw dislocation](@entry_id:161513) of the same Burgers vector magnitude.

### Interaction of Dislocations and Dislocation Structures

The stress field of one dislocation extends throughout the crystal and will exert a force on any other dislocation it encounters. This interaction is governed by the superposition of their stress fields.

#### Superposition of Stress Fields

To find the total stress field of a group of dislocations, one simply sums the stress tensors from each individual dislocation, taking care to express them in a common coordinate system.

For example, consider a **climb dipole**, consisting of two parallel [edge dislocations](@entry_id:191098) with opposite Burgers vectors $\mathbf{b}_1 = b\hat{\mathbf{x}}$ and $\mathbf{b}_2 = -b\hat{\mathbf{x}}$, located at $(0, -d/2)$ and $(0, d/2)$ respectively [@problem_id:216544]. To find the total stress $\sigma_{xx}$ at a point $(x_0, 0)$ on the axis midway between them, we sum their contributions.
The stress from dislocation 1 at $(x_0, 0)$ is found by shifting the coordinates in the standard formula: $x \to x_0$, $y \to 0 - (-d/2) = d/2$.
$$ \sigma_{xx}^{(1)} = -\frac{G b}{2\pi(1-\nu)} \frac{(d/2)(3x_0^2 + (d/2)^2)}{(x_0^2+(d/2)^2)^2} $$
The stress from dislocation 2 (with Burgers vector $-b$) is found by shifting $y \to 0 - (d/2) = -d/2$.
$$ \sigma_{xx}^{(2)} = -\frac{G (-b)}{2\pi(1-\nu)} \frac{(-d/2)(3x_0^2 + (-d/2)^2)}{(x_0^2+(-d/2)^2)^2} = -\frac{G b}{2\pi(1-\nu)} \frac{(d/2)(3x_0^2 + (d/2)^2)}{(x_0^2+(d/2)^2)^2} $$
The total stress is the sum, $\sigma_{xx} = \sigma_{xx}^{(1)} + \sigma_{xx}^{(2)}$, which is simply twice the contribution from one. This demonstrates how stress fields can reinforce each other.

Conversely, stress fields can also cancel. Consider two parallel [screw dislocations](@entry_id:182908) with identical Burgers vectors, located at $(0, d)$ and $(0, -d)$ [@problem_id:216632]. The total shear stress $\sigma_{xz}^{\text{total}}$ at an arbitrary point $(x,y)$ is the sum of the individual stresses:
$$ \sigma_{xz}^{\text{total}} = -\frac{Gb}{2\pi} \left[ \frac{y-d}{x^2 + (y-d)^2} + \frac{y+d}{x^2 + (y+d)^2} \right] $$
Setting this to zero yields the condition $y(x^2+y^2-d^2) = 0$. This implies that the stress component $\sigma_{xz}$ vanishes along the entire $x$-axis ($y=0$) and also on a circle of radius $d$ centered at the origin ($x^2+y^2=d^2$). Such cancellation is the basis for the formation of low-energy dislocation structures.

#### Advanced Tools: The Airy Stress Function

For two-dimensional [plane strain](@entry_id:167046) problems, such as those involving straight [edge dislocations](@entry_id:191098), the stress components can be derived from a [scalar potential](@entry_id:276177) known as the **Airy stress function**, $\chi(x,y)$. The relations are:
$$ \sigma_{xx} = \frac{\partial^2 \chi}{\partial y^2}, \quad \sigma_{yy} = \frac{\partial^2 \chi}{\partial x^2}, \quad \sigma_{xy} = -\frac{\partial^2 \chi}{\partial x \partial y} $$
The Airy function for a single [edge dislocation](@entry_id:160353) at the origin is $\chi_{\text{single}} = -D y \ln(x^2+y^2)$, where $D = \frac{Gb}{2\pi(1-\nu)}$.

The principle of superposition applies directly to the Airy function, which is often simpler than superposing the tensor components of stress. This approach is particularly powerful for analyzing dislocation dipoles. For instance, one can find the Airy function for an infinitesimal edge dipole by superposing the functions for two closely spaced dislocations of opposite sign and taking the limit as their separation $d \to 0$ while keeping the dipole moment $P=bd$ constant [@problem_id:216673]. This procedure leads to the stress function of a [point dipole](@entry_id:261850), a fundamental building block for describing more complex internal stress states.

### Beyond the Isotropic Continuum Model

The simple elastic model provides invaluable insight but relies on assumptions that break down in specific regimes. We now address some of these limitations and introduce more refined concepts.

#### The Peierls-Nabarro Model and Core Structure

Linear elasticity predicts an unphysical $1/r$ [stress singularity](@entry_id:166362) at the dislocation line. The **Peierls-Nabarro model** resolves this by incorporating the discrete nature of the crystal lattice on the slip plane. It models the dislocation as two elastic half-spaces separated by a [slip plane](@entry_id:275308) where a periodic **misfit energy** exists, resisting the slip [@problem_id:216590]. The equilibrium displacement profile across the slip plane, $u_x(x)$, is found by balancing the elastic shear stress $\sigma_{xy}$ in the continuum with the restoring force from this misfit potential.

This balance leads to a continuous, spread-out transition of displacement across the [slip plane](@entry_id:275308), rather than an abrupt cut. The characteristic **half-width of the [dislocation core](@entry_id:201451)**, $\zeta$, is found to be:
$$ \zeta = \frac{d}{2(1-\nu)} $$
where $d$ is the [interplanar spacing](@entry_id:138338) of the [slip planes](@entry_id:158709). This important result shows that the [dislocation core](@entry_id:201451) is not a mathematical line but has a finite physical width, determined by both [lattice parameters](@entry_id:191810) ($d$) and elastic properties ($\nu$). The stress is finite everywhere in this model.

#### Anisotropy

Real crystals are generally **anisotropic**, meaning their elastic properties depend on direction. The isotropic assumption simplifies calculations but can be inaccurate. For instance, consider a [screw dislocation](@entry_id:161513) along the $x_3$-axis in an **orthotropic** material, which has different [elastic constants](@entry_id:146207) along its principal axes ($C_{44}$ and $C_{55}$ being the relevant shear moduli) [@problem_id:216606]. The [equilibrium equation](@entry_id:749057) for the displacement $u_3(x_1, x_2)$ becomes $C_{55}u_{3,11} + C_{44}u_{3,22}=0$.

This anisotropic equation can be solved by an affine transformation of the coordinates. By defining a [stretched coordinate](@entry_id:196374) $y = \sqrt{C_{55}/C_{44}} \, x_2$, the governing equation transforms into the standard Laplace equation, $u_{3,11} + u_{3,yy} = 0$. Solving this and transforming back yields the stress field in the original coordinates. For example, the shear stress $\sigma_{23}$ becomes:
$$ \sigma_{23} = \frac{b_3 \sqrt{C_{44}C_{55}} \, x_1}{2\pi\left(x_1^2 + \frac{C_{55}}{C_{44}}x_2^2\right)} $$
Compared to the isotropic case ($\sigma_{yz} \propto x/(x^2+y^2)$), the lines of constant stress are no longer circles but ellipses, reflecting the directional dependence of the material's stiffness.

#### Continuum Description of Dislocation Ensembles: The Nye Tensor

When a material contains a high density of dislocations, it becomes practical to move from describing individual defects to a [continuum field theory](@entry_id:154108) of defects. The **Nye [dislocation density](@entry_id:161592) tensor**, $\alpha_{ij}$, provides this description. It is a state variable that measures the net character of the dislocations threading a given area. It is defined through the relation $\alpha_{ij} = -\epsilon_{jkl} (\partial_k \beta^e_{li})$, where $\epsilon_{jkl}$ is the Levi-Civita [permutation symbol](@entry_id:193594) and $\beta^e$ is the elastic distortion tensor. In simpler terms, it quantifies the local density of the Burgers vector.

A classic example is the modeling of a low-angle [symmetric tilt boundary](@entry_id:187640) (LASTB) as a wall of [edge dislocations](@entry_id:191098) [@problem_id:216526]. A LASTB with misorientation angle $\theta$ about the $x_3$-axis, lying in the $x_1=0$ plane, can be represented as a vertical array of [edge dislocations](@entry_id:191098) with line direction $\mathbf{t}=(0,0,1)$ and Burgers vector $\mathbf{b}=(b,0,0)$. The dislocations are spaced by a distance $D$, related to the tilt angle by **Frank's formula**, $b \approx D\theta$ for small $\theta$.

By averaging the contribution of the discrete dislocations over the boundary, we obtain a continuous [surface density](@entry_id:161889). The only non-zero component of the Nye tensor for this configuration is found to be:
$$ \alpha_{13} = \frac{b}{D} \delta(x_1) $$
where $\delta(x_1)$ is the Dirac [delta function](@entry_id:273429), indicating the dislocation content is localized to the boundary plane $x_1=0$. Substituting Frank's formula yields a remarkably elegant result:
$$ \alpha_{13} = \theta \, \delta(x_1) $$
This expression forms a cornerstone of the continuum theory of defects, directly linking a macroscopic, geometric property of the crystal (the misorientation angle $\theta$) to a continuum field representing the density of microscopic lattice defects.