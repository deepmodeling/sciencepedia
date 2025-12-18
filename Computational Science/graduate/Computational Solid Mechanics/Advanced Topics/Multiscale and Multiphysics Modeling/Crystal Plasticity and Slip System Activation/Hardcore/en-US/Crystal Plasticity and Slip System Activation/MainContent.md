## Introduction
The mechanical behavior of [crystalline materials](@entry_id:157810), from the strength of jet engine turbine blades to the formability of automotive steel sheets, is dictated by their response to stress at the microscopic level. When subjected to sufficient load, these materials deform permanently through a process known as [plastic deformation](@entry_id:139726). Crystal plasticity is the theoretical framework that connects this macroscopic behavior to its fundamental origins: the discrete, crystallographically-defined shearing events called slip. Understanding and predicting which slip systems will activate, and how they interact, is crucial for designing materials and structures with enhanced performance and reliability. This article bridges the gap between the abstract concept of dislocations and the quantitative prediction of material response, providing a detailed guide to the mechanics of [slip system activation](@entry_id:754950).

This article is structured to build a comprehensive understanding from the ground up. In the "Principles and Mechanisms" chapter, we will dissect the fundamental concepts, from the geometry of a [slip system](@entry_id:155264) and the driving force of [resolved shear stress](@entry_id:201022) to the intricate physics of work hardening and non-Schmid effects. The subsequent chapter, "Applications and Interdisciplinary Connections," demonstrates how these core principles are applied to model the behavior of engineering [polycrystals](@entry_id:139228) and are coupled with other physical domains like [damage mechanics](@entry_id:178377) and thermodynamics. Finally, the "Hands-On Practices" section offers practical exercises to translate these theoretical models into computational reality. We begin by exploring the fundamental principles governing how [crystalline solids](@entry_id:140223) accommodate plastic strain through the process of localized [crystallographic slip](@entry_id:196486).

## Principles and Mechanisms

The [plastic deformation](@entry_id:139726) of crystalline materials is fundamentally a process of shear, localized onto specific [crystallographic planes](@entry_id:160667) and directions. Unlike [amorphous materials](@entry_id:143499), which deform more homogeneously, the regular atomic arrangement of a crystal lattice dictates that slip is easiest along directions and on planes of high atomic density. This chapter elucidates the core principles and mechanisms governing this process, from the kinematic description of a [slip system](@entry_id:155264) to the stress-based criteria for its activation and the evolution of its resistance to flow.

### The Kinematic Basis of Crystallographic Slip

At the heart of [crystal plasticity](@entry_id:141273) is the concept of the **[slip system](@entry_id:155264)**. This represents a distinct mode of [shear deformation](@entry_id:170920) available to the crystal. The [kinematics](@entry_id:173318) of [plastic flow](@entry_id:201346) are described by the aggregate motion on these systems.

#### The Geometry of a Slip System

A [crystallographic slip](@entry_id:196486) system, denoted by an index $\alpha$, is defined by an [ordered pair](@entry_id:148349) of orthogonal [unit vectors](@entry_id:165907), $(\boldsymbol{s}^\alpha, \boldsymbol{m}^\alpha)$. 

*   The vector $\boldsymbol{s}^\alpha$ is the **slip direction**, a unit vector pointing along the direction of shear.
*   The vector $\boldsymbol{m}^\alpha$ is the **[slip plane](@entry_id:275308) normal**, a [unit vector](@entry_id:150575) perpendicular to the plane on which shear occurs.

The fundamental geometric constraint is that the slip direction must lie within the [slip plane](@entry_id:275308). This implies that the two vectors defining the system must be orthogonal:
$$
\boldsymbol{s}^\alpha \cdot \boldsymbol{m}^\alpha = 0
$$
From a physical standpoint, the slip direction $\boldsymbol{s}^\alpha$ corresponds to the normalized **Burgers vector** $\boldsymbol{b}^\alpha$, which represents the magnitude and direction of the lattice distortion caused by a dislocation. Thus, $\boldsymbol{s}^\alpha = \boldsymbol{b}^\alpha / |\boldsymbol{b}^\alpha|$. The slip direction is therefore determined by the character of the dislocation's [displacement field](@entry_id:141476), not its line direction $\boldsymbol{l}^\alpha$. A single dislocation loop may consist of segments with different line directions (edge, screw, and mixed character), but all segments share the same Burgers vector and thus contribute to slip in the same direction $\boldsymbol{s}^\alpha$. 

The contribution of a single active [slip system](@entry_id:155264) to the plastic velocity gradient, $\boldsymbol{L}^p$, is given by the [dyadic product](@entry_id:748716) of its defining vectors, weighted by the rate of shearing on that system, $\dot{\gamma}^\alpha$:
$$
\boldsymbol{L}^p = \sum_{\alpha} \dot{\gamma}^\alpha \boldsymbol{s}^\alpha \otimes \boldsymbol{m}^\alpha
$$
The tensor $\boldsymbol{s}^\alpha \otimes \boldsymbol{m}^\alpha$ is often referred to as the **Schmid tensor** for system $\alpha$. Note that the pair $(-\boldsymbol{s}^\alpha, -\boldsymbol{m}^\alpha)$ produces the same Schmid tensor, $(-\boldsymbol{s}^\alpha) \otimes (-\boldsymbol{m}^\alpha) = \boldsymbol{s}^\alpha \otimes \boldsymbol{m}^\alpha$, and thus represents the same physical [slip system](@entry_id:155264). Reversing only one of the vectors, e.g., to $(-\boldsymbol{s}^\alpha, \boldsymbol{m}^\alpha)$, corresponds to shear in the opposite sense on the same crystallographic system.

#### Slip Systems in Common Crystal Structures

The specific slip systems available are determined by the [crystal lattice structure](@entry_id:185398).

For **Face-Centered Cubic (FCC)** metals, such as aluminum, copper, and nickel, slip occurs most readily on the close-packed $\{111\}$ planes and in the close-packed $\langle 110 \rangle$ directions. To enumerate the systems in this family, we identify the unique planes and the unique directions within them.  The [family of planes](@entry_id:171035) $\{111\}$ contains four distinct planes, which can be represented by the normals $(111)$, $(1\bar{1}1)$, $(\bar{1}11)$, and $(11\bar{1})$ and their negatives. Each of these planes contains three distinct slip directions from the $\langle 110 \rangle$ family. For example, the $(111)$ plane, with normal $\boldsymbol{m} \propto [111]$, contains directions $[uvw]$ that satisfy the [orthogonality condition](@entry_id:168905) $u \cdot 1 + v \cdot 1 + w \cdot 1 = 0$. The $\langle 110 \rangle$ directions satisfying this are $[1\bar{1}0]$, $[10\bar{1}]$, and $[01\bar{1}]$ (and their negatives). By pairing each of the four planes with its three contained directions, we arrive at a total of $4 \times 3 = 12$ distinct [slip systems](@entry_id:136401) for the $\{111\}\langle 110 \rangle$ family.

For **Body-Centered Cubic (BCC)** metals, like iron and [tungsten](@entry_id:756218), the close-packed slip direction is unambiguously of the $\langle 111 \rangle$ type. However, the [slip plane](@entry_id:275308) is less well-defined, and slip can be observed on planes of the $\{110\}$, $\{112\}$, and $\{123\}$ families. A common choice for modeling is the $\{110\}\langle 111 \rangle$ family. There are six distinct $\{110\}$ planes, each containing two $\langle 111 \rangle$ directions, which yields $6 \times 2 = 12$ slip systems. 

For **Hexagonal Close-Packed (HCP)** metals, such as magnesium, titanium, and zinc, the lower symmetry leads to crystallographically distinct types of [slip systems](@entry_id:136401) with vastly different activation characteristics. It is useful here to distinguish between a **slip family** and a **slip set**. A slip family comprises all crystallographically equivalent systems (e.g., $\{111\}\langle 110 \rangle$ in FCC). A slip set is a modeling construct, a group of systems that are assigned a common set of material properties, such as the resistance to slip. For HCP, we typically define several sets:
*   **Basal slip**: 3 systems of the type $\{0001\}\langle 11\bar{2}0 \rangle$.
*   **Prismatic slip**: 3 systems of the type $\{10\bar{1}0\}\langle 11\bar{2}0 \rangle$.
*   **Pyramidal $\langle a \rangle$ slip**: 6 systems of the type $\{10\bar{1}1\}\langle 11\bar{2}0 \rangle$.
*   **Pyramidal $\langle c+a \rangle$ slip**: 12 systems of the type $\{10\bar{1}1\}\langle 11\bar{2}3 \rangle$, which are necessary to accommodate arbitrary plastic deformation.

### The Driving Force for Slip: Resolved Shear Stress

For a [slip system](@entry_id:155264) to become active, a sufficient driving force must be present. This force is provided by the component of the applied stress that acts to shear the crystal along the [slip system](@entry_id:155264).

#### Schmid's Law

The driving force for slip on system $\alpha$ is the **[resolved shear stress](@entry_id:201022) (RSS)**, denoted $\tau^\alpha$. It is defined as the [scalar projection](@entry_id:148823) of the [traction vector](@entry_id:189429) acting on the slip plane, $\boldsymbol{t}^\alpha = \boldsymbol{\sigma}\boldsymbol{m}^\alpha$, onto the slip direction, $\boldsymbol{s}^\alpha$. Here, $\boldsymbol{\sigma}$ is the Cauchy stress tensor. This definition is known as **Schmid's Law**:

$$
\tau^\alpha = \boldsymbol{s}^\alpha \cdot \boldsymbol{t}^\alpha = \boldsymbol{s}^\alpha \cdot (\boldsymbol{\sigma} \boldsymbol{m}^\alpha)
$$

Consider, for example, an FCC crystal under a general stress state. For the [slip system](@entry_id:155264) with $\boldsymbol{m}^\alpha = \frac{1}{\sqrt{3}}[1, 1, 1]^T$ and $\boldsymbol{s}^\alpha = \frac{1}{\sqrt{2}}[1, -1, 0]^T$, subjected to a stress tensor $\boldsymbol{\sigma}$, the [resolved shear stress](@entry_id:201022) can be calculated directly. If the stress is given by $\boldsymbol{\sigma} = \begin{pmatrix} 200 & 50 & 0 \\ 50 & 100 & 0 \\ 0 & 0 & 50 \end{pmatrix} \text{ MPa}$, the traction on the plane is $\boldsymbol{t}^\alpha = \frac{1}{\sqrt{3}}[250, 150, 50]^T \text{ MPa}$. The [resolved shear stress](@entry_id:201022) is then $\tau^\alpha = \boldsymbol{s}^\alpha \cdot \boldsymbol{t}^\alpha = \frac{1}{\sqrt{6}}(250 - 150) = \frac{100}{\sqrt{6}} \approx 40.82 \text{ MPa}$. 

For the special case of [uniaxial tension](@entry_id:188287) of magnitude $\sigma$ along a direction given by the [unit vector](@entry_id:150575) $\boldsymbol{d}$, the stress tensor is $\boldsymbol{\sigma} = \sigma (\boldsymbol{d} \otimes \boldsymbol{d})$. The [resolved shear stress](@entry_id:201022) becomes:
$$
\tau^\alpha = \boldsymbol{s}^\alpha \cdot (\sigma (\boldsymbol{d} \otimes \boldsymbol{d}) \boldsymbol{m}^\alpha) = \sigma (\boldsymbol{d} \cdot \boldsymbol{s}^\alpha)(\boldsymbol{d} \cdot \boldsymbol{m}^\alpha)
$$
The product of the two cosines, $m^\alpha = (\boldsymbol{d} \cdot \boldsymbol{s}^\alpha)(\boldsymbol{d} \cdot \boldsymbol{m}^\alpha)$, is known as the **Schmid factor**. It represents the geometric effectiveness of a given loading orientation in resolving a shear stress onto a particular [slip system](@entry_id:155264). The Schmid factor has a maximum theoretical value of $0.5$.

#### Example: Slip System Activation in a Uniaxially Loaded Crystal

To illustrate the principle of slip activation, consider an FCC single crystal subjected to [uniaxial tension](@entry_id:188287) of $\sigma = 200$ MPa. The crystal's orientation relative to the loading axis determines the [resolved shear stress](@entry_id:201022) on each of its 12 slip systems. Let the loading axis in the crystal's reference frame be $\boldsymbol{d}_c = [-\frac{1}{\sqrt{2}}, \frac{1}{2}, \frac{1}{2}]^T$. 

The [resolved shear stress](@entry_id:201022) on any system $\alpha$ is $\tau^\alpha = \sigma (\boldsymbol{s}_c^\alpha \cdot \boldsymbol{d}_c)(\boldsymbol{m}_c^\alpha \cdot \boldsymbol{d}_c)$. We must compute the Schmid factor for all 12 systems to find the one(s) with the highest magnitude.

For instance, for the system with plane normal $\boldsymbol{m}_c = \frac{1}{\sqrt{3}}[1,1,-1]$ and slip direction $\boldsymbol{s}_c = \frac{1}{\sqrt{2}}[1,-1,0]$:
*   $\cos(\phi) = \boldsymbol{m}_c \cdot \boldsymbol{d}_c = \frac{1}{\sqrt{3}}(-\frac{1}{\sqrt{2}} + \frac{1}{2} - \frac{1}{2}) = -\frac{1}{\sqrt{6}}$
*   $\cos(\lambda) = \boldsymbol{s}_c \cdot \boldsymbol{d}_c = \frac{1}{\sqrt{2}}(-\frac{1}{\sqrt{2}} - \frac{1}{2} + 0) = -\frac{1}{2} - \frac{1}{2\sqrt{2}}$
*   The Schmid factor is $m = (-\frac{1}{\sqrt{6}})(-\frac{1}{2} - \frac{1}{2\sqrt{2}}) = \frac{\sqrt{2}+1}{4\sqrt{3}} \approx 0.3485$.

By systematically evaluating all 12 systems, this value is found to be the maximum. The maximum [resolved shear stress](@entry_id:201022) is therefore:
$$
\tau_{\text{max}} = \sigma |m|_{\text{max}} = 200 \text{ MPa} \times 0.3485 \approx 69.69 \text{ MPa}
$$
Assuming all systems have the same resistance to slip, [plastic deformation](@entry_id:139726) will initiate on the system(s) experiencing this maximum [resolved shear stress](@entry_id:201022).

### Activation Criteria and Plastic Flow

#### The Critical Resolved Shear Stress

Slip does not occur for any non-zero shear stress. Rather, it initiates only when the [resolved shear stress](@entry_id:201022) $\tau^\alpha$ reaches a critical threshold value, known as the **[critical resolved shear stress](@entry_id:159240) (CRSS)**, which we denote as $g^\alpha$. The criterion for slip activation is therefore:
$$
|\tau^\alpha| \ge g^\alpha
$$
The CRSS, $g^\alpha$, is a material property that represents the [intrinsic resistance](@entry_id:166682) of the crystal lattice to dislocation motion. It is influenced by temperature, [strain rate](@entry_id:154778), and the density and arrangement of defects in the crystal. In the example from , with $\tau^\alpha \approx 40.82 \text{ MPa}$ and an initial CRSS of $g_0^\alpha = 30 \text{ MPa}$, the condition is met, and slip is predicted to occur.

#### Deviations from Schmid's Law: Non-Schmid Effects

A direct consequence of the definition of RSS is that it is sensitive only to the deviatoric part of the stress tensor. The hydrostatic part, or pressure $p = -\frac{1}{3}\text{tr}(\boldsymbol{\sigma})$, does not contribute to the driving force for slip. This is because its contribution to the RSS is:
$$
\boldsymbol{s}^\alpha \cdot ((-p \boldsymbol{I}) \boldsymbol{m}^\alpha) = -p (\boldsymbol{s}^\alpha \cdot \boldsymbol{m}^\alpha) = 0
$$
due to the orthogonality of the [slip system](@entry_id:155264) vectors. 

If the CRSS, $g^\alpha$, is a constant for a given slip family, then Schmid's law fully determines slip activation, and deformation is insensitive to pressure. However, for many materials, this is not the case. **Non-Schmid effects** refer to any deviation from this simple picture, where the activation of slip is influenced by stress components other than the [resolved shear stress](@entry_id:201022) $\tau^\alpha$. These effects arise not because the *driving force* changes, but because the *resistance* $g^\alpha$ becomes a function of the full stress state.

The most prominent examples are found in BCC metals. The core of a $\langle 111 \rangle$ [screw dislocation](@entry_id:161513) in a BCC lattice is non-planar, spreading across several planes. The energy and mobility of this core structure are sensitive to the full stress tensor, including pressure and so-called **non-glide stresses** (e.g., shear components on the [slip plane](@entry_id:275308) but not in the slip direction). This leads to a CRSS that depends on these other stress components, and it is the physical origin of the [tension-compression asymmetry](@entry_id:201728) observed in BCC metals. 

This behavior can be captured by a generalized activation criterion. For instance, the effective driving stress can be written as a function of $\tau^\alpha$, the pressure $p$, and a non-glide shear stress $\tau_{ng}^\alpha$. One such linear model is:
$$
\text{Activation occurs when: } \tau^\alpha + a p + b \tau_{ng}^\alpha \ge g^\alpha
$$
where $a$ and $b$ are material-specific non-Schmid parameters. 

Consider a BCC crystal where the Schmid stress is $\tau^\alpha = 120$ MPa, but the CRSS is $g^\alpha = 150$ MPa. Under Schmid's law, no slip would occur. However, if the crystal is also under a compressive pressure of $p=200$ MPa and a non-glide stress of $\tau_{ng}^\alpha = 80$ MPa, with non-Schmid coefficients $a=0.25$ and $b=0.15$, the effective driving stress is $120 + 0.25(200) + 0.15(80) = 120 + 50 + 12 = 182$ MPa. Since $182 \text{ MPa} > 150 \text{ MPa}$, the generalized criterion correctly predicts slip activation. It is crucial to recognize that the non-Schmid terms $ap$ and $b\tau_{ng}^\alpha$ modify the energetic barrier for dislocation motion but are not work-conjugate to the slip rate $\dot{\gamma}^\alpha$; they do not contribute to plastic [power dissipation](@entry_id:264815).

In FCC metals, by contrast, dislocation cores are typically planar, and Schmid's law is a much better approximation. However, even in FCC metals, pressure can have indirect effects by altering the [stacking fault energy](@entry_id:145736), which in turn influences the propensity for [screw dislocations](@entry_id:182908) to **[cross-slip](@entry_id:195437)**—change from one [slip plane](@entry_id:275308) to another that shares the same slip direction. This ability is geometrically restricted to [screw dislocations](@entry_id:182908), for which the line direction is parallel to the Burgers vector ($\boldsymbol{l}^\alpha \parallel \boldsymbol{b}^\alpha$), making the slip plane geometrically non-unique. 

### The Evolution of Slip Resistance: Work Hardening

As a crystal deforms plastically, its resistance to further slip, the CRSS $g^\alpha$, typically increases. This phenomenon is known as **[work hardening](@entry_id:142475)** or strain hardening. The evolution of $g^\alpha$ is a central part of [crystal plasticity](@entry_id:141273) models and is physically rooted in the interactions between dislocations.

We can distinguish two primary modes of hardening: 
*   **Self-hardening**: The increase in resistance on a [slip system](@entry_id:155264) $\alpha$ due to the accumulation of slip on that same system.
*   **Latent hardening**: The increase in resistance on a [slip system](@entry_id:155264) $\alpha$ due to the accumulation of slip on *other* systems $\beta \ne \alpha$.

This is often modeled with a [hardening law](@entry_id:750150) of the form:
$$
\dot{g}^\alpha = \sum_{\beta} h^{\alpha\beta} |\dot{\gamma}^\beta|
$$
where $h^{\alpha\beta}$ is the hardening matrix. The diagonal terms $h^{\alpha\alpha}$ represent self-hardening, while the off-diagonal terms $h^{\alpha\beta}$ ($\alpha \ne \beta$) represent latent hardening.

#### The Microstructural Origin of Hardening

Hardening arises from dislocations impeding each other's motion. The [flow stress](@entry_id:198884) is therefore related to the total dislocation density, $\rho_{total}$. The widely used **Taylor [hardening law](@entry_id:750150)** captures this relationship:
$$
g^\alpha = g_0^\alpha + A \mu b \sqrt{\rho_{total}}
$$
where $g_0^\alpha$ is the initial CRSS, $A$ is a dimensionless factor, $\mu$ is the shear modulus, and $b$ is the Burgers vector magnitude.

In modern plasticity theories, it is useful to partition the total dislocation population into two types: 
*   **Statistically Stored Dislocations (SSDs)**, $\rho_{SSD}$: These arise from the random trapping and multiplication of dislocations, even during spatially uniform deformation. They typically exist as dipoles or multipoles with no net Burgers vector over a small volume and are the primary source of hardening in uniform plasticity.
*   **Geometrically Necessary Dislocations (GNDs)**, $\rho_{GND}$: These are required by crystal geometry to accommodate gradients in [plastic deformation](@entry_id:139726), i.e., to maintain lattice compatibility across a region of non-uniform slip. They represent a net Burgers vector content and are directly associated with lattice curvature.

The density of GNDs is mathematically related to the curl of the plastic distortion tensor, which defines the **Nye dislocation density tensor** $\boldsymbol{\alpha}$. In small-strain theory, where plastic distortion is $\boldsymbol{\beta}^p = \sum_\alpha \gamma^\alpha \boldsymbol{s}^\alpha \otimes \boldsymbol{m}^\alpha$, the Nye tensor is $\boldsymbol{\alpha} = \nabla \times \boldsymbol{\beta}^p$. The [scalar density](@entry_id:161438) of GNDs is then proportional to its norm: $\rho_{GND} \propto |\boldsymbol{\alpha}|/b$. If plastic deformation is uniform, the gradient vanishes, and $\rho_{GND}=0$. 

The total dislocation density is the sum $\rho_{total} = \rho_{SSD} + \rho_{GND}$. The Taylor law becomes:
$$
g^\alpha = g_0^\alpha + A \mu b \sqrt{\rho_{SSD} + \rho_{GND}}
$$
This framework naturally introduces a length scale into plasticity. Consider a thin foil of thickness $L=1$ μm where slip varies linearly from $0$ to $\gamma_{max}=0.02$ across the thickness.  The constant slip gradient is $|\frac{d\gamma}{dy}| = \frac{\gamma_{max}}{L}$. The density of GNDs required to accommodate this is $\rho_{GND} = \frac{1}{b}|\frac{d\gamma}{dy}| = \frac{0.02}{(0.25 \times 10^{-9} \text{ m})(1 \times 10^{-6} \text{ m})} = 8.0 \times 10^{13} \text{ m}^{-2}$. If the SSD density is $\rho_{SSD} = 5.0 \times 10^{13} \text{ m}^{-2}$, the total density is $1.3 \times 10^{14} \text{ m}^{-2}$. The resulting increase in CRSS is $\Delta g = A \mu b \sqrt{\rho_{total}} \approx 49.9$ MPa (for typical parameters). Because $\rho_{GND} \propto 1/L$, the hardening becomes size-dependent: smaller specimens exhibit stronger hardening for the same overall strain. This "smaller is stronger" phenomenon is a key motivation for **[strain-gradient plasticity](@entry_id:172852)** theories.

### Considerations for Finite Strain Formulations

When deformations are large, the formulation of [crystal plasticity](@entry_id:141273) becomes more complex. The deformation gradient is multiplicatively decomposed, $\boldsymbol{F} = \boldsymbol{F}^e \boldsymbol{F}^p$, and care must be taken to define stress and kinematic quantities in appropriate reference frames.

A key issue is the definition of the driving stress for slip. While the Cauchy stress $\boldsymbol{\sigma}$ and a Schmid tensor in the current configuration provide an objective measure, many computational frameworks operate in the reference or an intermediate (plastically deformed) configuration. This leads to alternative, equally objective, definitions of the [resolved shear stress](@entry_id:201022). 

One common alternative is based on the **Mandel stress**, $\boldsymbol{M} = \boldsymbol{C}\boldsymbol{S}$, where $\boldsymbol{C}=\boldsymbol{F}^T\boldsymbol{F}$ is the right Cauchy-Green tensor and $\boldsymbol{S}$ is the second Piola-Kirchhoff stress. The Mandel-based RSS, $\tau_M$, is work-conjugate to the slip rate in the intermediate configuration. For a Saint Venant-Kirchhoff elastic material under simple shear of amount $\gamma$, the Cauchy-based and Mandel-based measures are not identical:
$$
\tau_{\sigma} = \mu\gamma + \frac{\lambda}{2}\gamma^{3}
$$
$$
\tau_M = \mu\gamma + \frac{2\mu+\lambda}{2}\gamma^{3}
$$
where $\mu$ and $\lambda$ are Lamé parameters. The difference, $\tau_M - \tau_{\sigma} = \mu\gamma^3$, arises from finite-strain [kinematics](@entry_id:173318). Although both measures are objective (invariant to superposed rigid-body rotations), their different functional forms mean they can predict slip activation at different levels of deformation. For instance, for $\gamma=0.5$ and typical [elastic constants](@entry_id:146207), it is possible for $\tau_M$ to exceed the CRSS while $\tau_{\sigma}$ does not. This highlights that the choice of driving stress measure is a critical constitutive decision in [finite strain](@entry_id:749398) computational [crystal plasticity](@entry_id:141273). 