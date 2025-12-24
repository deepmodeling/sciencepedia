## Introduction
Magnetic components, such as inductors and transformers, are indispensable in power electronic systems, yet they are often a primary source of energy loss that compromises efficiency and complicates thermal management. These losses, originating within the magnetic core, are driven by two principal mechanisms: hysteresis and [eddy currents](@entry_id:275449). A thorough grasp of these phenomena is no longer an academic exercise but a critical requirement for designing high-performance, power-dense converters. This article addresses the knowledge gap between basic concepts and advanced engineering application by providing a comprehensive exploration of core losses.

Over the next three chapters, you will build a robust understanding of this topic. The first chapter, **Principles and Mechanisms**, will dissect the fundamental physics of hysteresis and eddy current losses, starting from Maxwell's equations and delving into the microscopic world of [magnetic domains](@entry_id:147690). The second chapter, **Applications and Interdisciplinary Connections**, will bridge theory and practice by demonstrating how these principles guide the design of magnetic components, inform material selection, and connect to diverse fields like [thermal engineering](@entry_id:139895) and [medical physics](@entry_id:158232). Finally, **Hands-On Practices** will provide opportunities to apply this knowledge through targeted design and analysis problems. We begin by examining the thermodynamic and microscopic origins of [energy dissipation](@entry_id:147406) in magnetic materials.

## Principles and Mechanisms

In the design and operation of power electronic converters, the magnetic components—inductors and transformers—are often critical sources of energy loss, directly impacting system efficiency and thermal management. These losses, originating within the magnetic core material, arise from the irreversible conversion of [electromagnetic energy](@entry_id:264720) into heat during each cycle of magnetization. A comprehensive understanding of the physical mechanisms responsible for these losses is paramount for material selection, component design, and performance optimization. Core losses can be broadly categorized into two principal types: **hysteresis loss**, which is present even at quasi-static frequencies, and **[eddy current loss](@entry_id:1124138)**, a dynamic effect inherent to conductive magnetic materials. This chapter elucidates the fundamental principles governing these loss mechanisms, from macroscopic thermodynamic descriptions to microscopic domain-level physics.

### Energy Dissipation in Magnetic Materials: A Thermodynamic Perspective

The foundation for understanding magnetic losses lies in the energy exchange between an electromagnetic field and a material. This can be rigorously derived from Maxwell's equations. The law of conservation of energy for an electromagnetic field is expressed by Poynting's theorem. In its differential form, the theorem states:

$$ -\nabla \cdot \mathbf{S} = \mathbf{E} \cdot \mathbf{J}_{\mathrm{f}} + \mathbf{H} \cdot \frac{\partial \mathbf{B}}{\partial t} + \mathbf{E} \cdot \frac{\partial \mathbf{D}}{\partial t} $$

Here, $\mathbf{S} = \mathbf{E} \times \mathbf{H}$ is the Poynting vector representing the [energy flux](@entry_id:266056), $-\nabla \cdot \mathbf{S}$ is the rate at which energy flows into a unit volume, $\mathbf{E} \cdot \mathbf{J}_{\mathrm{f}}$ is the power dissipated by [free currents](@entry_id:191634) (Joule heating), and the final two terms represent the rate of work done on the magnetic and electric fields, respectively.

Within a magnetic material subjected to an external field, where displacement current effects are negligible (a common [quasi-static approximation](@entry_id:167818) in magnetics), this energy balance simplifies. The power supplied per unit volume to the magnetic medium itself is given by the term $\mathbf{H} \cdot \frac{\partial \mathbf{B}}{\partial t}$. Consequently, the incremental work $dW_v$ done by the external field source on the material to change its magnetic state by $d\mathbf{B}$ over a time interval $dt$ is:

$$ dW_v = \left(\mathbf{H} \cdot \frac{\partial \mathbf{B}}{\partial t}\right) dt = \mathbf{H} \cdot d\mathbf{B} $$

This work contributes to both the change in stored magnetic energy and any energy dissipated irreversibly. To find the net energy dissipated per unit volume over one complete, periodic magnetization cycle, we integrate this expression over the path traced in the $\mathbf{B}$-$\mathbf{H}$ plane. If the material were ideal and lossless, the path from minimum to maximum flux and back would be identical, and the net work would be zero. However, in real magnetic materials, the path is not reversible and forms a closed loop, known as the **[hysteresis loop](@entry_id:160173)**. The net energy dissipated per unit volume per cycle, $W_{\text{cycle}}$, is the [line integral](@entry_id:138107) around this closed path :

$$ W_{\text{cycle}} = \oint_{\mathcal{C}} \mathbf{H} \cdot d\mathbf{B} $$

This integral is geometrically equivalent to the area enclosed by the [hysteresis loop](@entry_id:160173). This dissipated energy manifests as heat within the core. The total power loss per unit volume, often called core loss density, is the energy per cycle multiplied by the operating frequency, $f$.

### Hysteresis Loss: The Quasi-Static Limit

Hysteresis loss is the energy dissipated due to the irreversible nature of magnetization processes, which persists even at infinitesimally slow cycling rates. Its origins are deeply rooted in the microscopic structure of magnetic materials.

#### Microscopic Origins of Hysteresis

Ferromagnetic materials are composed of **[magnetic domains](@entry_id:147690)**, which are small regions within which the [atomic magnetic moments](@entry_id:173739) are spontaneously aligned. These domains are separated by thin transition regions called **domain walls**. When an external magnetic field is applied, the material's overall magnetization changes primarily through two mechanisms: the motion of these [domain walls](@entry_id:144723) (causing favorably oriented domains to grow at the expense of others) and the rotation of the magnetization direction within the domains.

The key to hysteresis is that [domain wall motion](@entry_id:1123909) is not a smooth, frictionless process. The crystal lattice of the material is never perfect; it contains a variety of microstructural defects such as impurities, grain boundaries, voids, and dislocations in the crystal structure. These defects create local variations in magnetic energy, acting as **pinning sites** where a [domain wall](@entry_id:156559) can become temporarily trapped. To move a wall past a pinning site, the external field must supply a finite amount of energy, $E_b$, to overcome this local energy barrier. This process is inherently irreversible; the energy is not recovered when the field is reversed but is dissipated into the lattice as heat, often through [phonon excitations](@entry_id:159714). This abrupt, irreversible motion of [domain walls](@entry_id:144723) over pinning sites is observable as a series of small, discrete jumps in magnetization known as **Barkhausen jumps**.

From this microscopic viewpoint, the total hysteresis energy dissipated per cycle per unit volume, $W_{hyst}$, is the sum of the energies dissipated at all pinning sites crossed during one full magnetization cycle. If we consider $n_p$ to be the [number density](@entry_id:268986) of pinning sites overcome during a single sweep of magnetization (e.g., from negative to positive saturation), the energy dissipated in this half-cycle is $n_p E_b$. A full cycle involves a forward and a reverse sweep, with energy being dissipated in both directions. Therefore, the total [hysteresis loop](@entry_id:160173) area is directly related to the microscopic pinning barriers :

$$ W_{hyst} = \oint \mathbf{H} \cdot d\mathbf{B} = 2 n_p E_b $$

This powerful result connects a macroscopic, measurable quantity (the loop area) to the microscopic properties of the material (the density and strength of defect pinning sites).

#### Macroscopic Manifestation: The B-H Loop

The B-H hysteresis loop graphically represents this irreversible behavior. Key parameters characterize the loop's shape and, consequently, the material's properties:
- **Saturation Flux Density ($B_s$):** The maximum possible flux density in the material, achieved when all magnetic domains are aligned with the strong external field.
- **Remanence ($B_r$):** The residual flux density remaining in the material after the external field is removed ($H=0$).
- **Coercivity ($H_c$):** The magnitude of the reverse magnetic field required to reduce the flux density to zero after saturation. Coercivity is a direct measure of the opposition to demagnetization and is strongly related to the strength of [domain wall pinning](@entry_id:138291).

The area of the loop, and thus the hysteresis energy per cycle, is directly determined by these parameters. For instance, in a simplified model where the B-H loop is approximated as a rectangle with corners at $(\pm H_c, \pm B_r)$, the area can be calculated straightforwardly as the sum of the work done on the two vertical segments of the loop :

$$ W_{h, \text{major}} = \int_{-B_r}^{B_r} H_c \, dB + \int_{B_r}^{-B_r} (-H_c) \, dB = 2 H_c B_r - (-2 H_c B_r) = 4 H_c B_r $$

This simple model clearly illustrates that the hysteresis energy per cycle is proportional to both the coercivity and the remanent flux density. The corresponding average hysteresis power loss per unit volume is then linearly proportional to frequency:

$$ P_h = W_h \cdot f $$

#### Influence of Mechanical Stress: Magnetostriction

The magnetic properties of a material are not independent of its mechanical state. **Magnetostriction** is the phenomenon where a [ferromagnetic material](@entry_id:271936) changes its shape or dimensions during the process of magnetization. The inverse effect, known as the **Villari effect**, is that applying a mechanical stress to the material induces a [magnetic anisotropy](@entry_id:138218), altering its magnetic behavior.

This **magnetoelastic energy** density, $E_\sigma$, in a material with an isotropic [magnetostriction](@entry_id:143327) coefficient $\lambda_s$ under a uniaxial stress $\sigma$ is given by:

$$ E_\sigma = -\frac{3}{2} \lambda_s \sigma \cos^2\theta $$

where $\theta$ is the angle between the [magnetization vector](@entry_id:180304) and the stress axis. This stress-induced anisotropy adds to the material's intrinsic [magnetocrystalline anisotropy](@entry_id:144488). The total effective anisotropy determines the energy landscape for [domain wall motion](@entry_id:1123909) and rotation, thereby influencing [coercivity](@entry_id:159399) and hysteresis loss.

The effect depends critically on the signs of $\lambda_s$ and $\sigma$ (tensile stress is positive, compressive is negative) .
- If $\lambda_s \sigma > 0$ (e.g., tensile stress on a material with positive $\lambda_s$), $E_\sigma$ is minimized when $\cos^2\theta = 1$, meaning the magnetization preferentially aligns *parallel* to the stress axis. If the stress is applied along the intended flux path, this reinforces the desired domain alignment, but it also increases the overall anisotropy, which typically increases [coercivity](@entry_id:159399) and hysteresis loss.
- If $\lambda_s \sigma  0$ (e.g., compressive stress on a material with positive $\lambda_s$), $E_\sigma$ is minimized when $\cos^2\theta = 0$, favoring magnetization alignment *perpendicular* to the stress axis. This makes it harder to magnetize the material along the stress axis and can lead to complex changes in the domain structure and loss characteristics.

Therefore, clamping a core or subjecting it to mechanical loads during operation can significantly alter its hysteresis loss.

#### Aging and Lifetime Effects

The microscopic origins of hysteresis also explain how core losses can change over a component's lifetime. Power electronic components are often subjected to significant [thermal cycling](@entry_id:913963) and mechanical vibration. These stressors can lead to [thermo-mechanical fatigue](@entry_id:1133040), causing an accumulation of microstructural defects like dislocations and microcracks.

As established, these defects act as [domain wall pinning](@entry_id:138291) sites. An increase in [defect density](@entry_id:1123482) over the lifetime of a component means that [domain walls](@entry_id:144723) encounter more obstacles, increasing the overall pinning force. This translates directly to an increase in the [coercivity](@entry_id:159399) $H_c$. Consequently, the B-H loop widens, and the hysteresis loss per cycle increases, leading to a degradation in component efficiency and increased heat generation over time .

### Eddy Current Loss: The Dynamic Contribution

While [hysteresis loss](@entry_id:266219) is present at any non-zero frequency, **[eddy current loss](@entry_id:1124138)** is a purely dynamic effect that becomes increasingly dominant as frequency rises.

#### Physical Mechanism

According to Faraday's Law of Induction, a time-varying magnetic flux density, $\frac{\partial \mathbf{B}}{\partial t}$, induces an [electromotive force](@entry_id:203175) (EMF) and a corresponding electric field, $\mathbf{E}$, within any conducting material. If the material is a conductor (as all metallic magnetic materials are), this electric field will drive currents, known as **[eddy currents](@entry_id:275449)**, in planes perpendicular to the changing magnetic flux.

These [eddy currents](@entry_id:275449), governed by Ohm's Law $\mathbf{J} = \sigma \mathbf{E}$ (where $\sigma$ is the [electrical conductivity](@entry_id:147828)), flow through the resistive material and dissipate energy as Joule heat. The local power density is given by $p_e = \mathbf{J} \cdot \mathbf{E} = \sigma |\mathbf{E}|^2$.

To understand the scaling of this loss, consider a thin lamination of thickness $t$ subjected to a uniform, sinusoidal magnetic field $B(t) = B_{\mathrm{pk}} \sin(2\pi f t)$ parallel to its surface. The induced E-field is proportional to the rate of change of B, so $E \propto f B_{\mathrm{pk}}$. The power density is proportional to $E^2$, and integrating this over the lamination's cross-section yields the average eddy current power loss per unit volume, $P_e$ :

$$ P_e = \frac{\pi^2}{6 \rho} t^2 f^2 B_{\mathrm{pk}}^2 = \frac{\pi^2 \sigma}{6} t^2 f^2 B_{\mathrm{pk}}^2 $$

where $\rho = 1/\sigma$ is the electrical resistivity. This is the **classical [eddy current loss](@entry_id:1124138) formula**. It reveals several critical dependencies:
- A strong quadratic dependence on frequency ($f^2$).
- A strong quadratic dependence on lamination thickness ($t^2$).
- A direct proportionality to electrical conductivity ($\sigma$, or inverse proportionality to resistivity $\rho$).

#### Mitigation Strategies: Lamination and Material Selection

The classical loss formula immediately points to the primary strategies for mitigating eddy current losses. The most effective method is **lamination**: constructing the core from a stack of thin, electrically insulated sheets. The $t^2$ dependence means that halving the lamination thickness reduces the [eddy current loss](@entry_id:1124138) by a factor of four.

The second key strategy is material selection. The formula shows that materials with high [electrical resistivity](@entry_id:143840) (low conductivity) are highly desirable. This is the fundamental reason why different materials are chosen for different frequency ranges.
- **Silicon Steels:** These are iron alloys with a few percent of silicon, which increases resistivity and reduces losses compared to pure iron. They have high saturation flux densities but also relatively high conductivity ($\sigma \sim 2 \times 10^6$ S/m). They are cost-effective and dominate low-frequency applications (e.g., 50/60 Hz transformers), where their high conductivity can be managed with laminations of moderate thickness.
- **Soft Ferrites:** These are ceramic magnetic materials (e.g., MnZn, NiZn [ferrites](@entry_id:271668)) with exceptionally high electrical resistivity ($\sigma \sim 1$ S/m or less). This is many orders of magnitude lower conductivity than silicon steel. Due to their high resistivity, [eddy currents](@entry_id:275449) are intrinsically suppressed, making [ferrites](@entry_id:271668) the material of choice for high-frequency applications (tens of kHz to several MHz), often without the need for lamination  .

#### The Skin Effect at High Frequencies

The classical [eddy current loss](@entry_id:1124138) formula is derived under the assumption that the magnetic field is uniform throughout the conductor's cross-section. However, the eddy currents themselves generate a magnetic field that, by Lenz's law, opposes the change in the applied field. At high frequencies, this counter-field becomes strong enough to shield the interior of the conductor, confining the AC magnetic flux to a thin layer near the surface. This phenomenon is known as the **[skin effect](@entry_id:181505)**.

The characteristic depth to which the field penetrates is called the **skin depth** or **penetration depth**, $\delta$. For a good conductor, it is given by:

$$ \delta = \sqrt{\frac{2}{\omega \mu \sigma}} = \sqrt{\frac{\rho}{\pi f \mu}} $$

where $\mu$ is the magnetic permeability of the material. The skin depth decreases with increasing frequency, permeability, and conductivity. The behavior of eddy current losses is dictated by the ratio of the material's characteristic dimension (e.g., lamination thickness $t$) to the [skin depth](@entry_id:270307) $\delta$ .

1.  **Uniform Field Regime ($t \ll \delta$):** When the lamination is much thinner than the skin depth, the field is nearly uniform, and the classical [eddy current loss](@entry_id:1124138) formula ($P_e \propto f^2 t^2 \sigma$) applies. This is the desired operating regime for high-frequency laminated cores. The design goal is to choose a lamination thickness $t$ that is significantly smaller than the skin depth calculated at the *maximum* operating frequency, $f_{\text{max}}$ .

2.  **Skin Effect Regime ($t \gg \delta$):** When the material is thick compared to the [skin depth](@entry_id:270307), the flux is confined to the surface. The loss is no longer a bulk phenomenon but a surface one. In this regime, the power loss per unit surface area scales differently, typically as $P_s \propto \sqrt{f} |H_{\text{surface}}|^2$. This change in frequency dependence is crucial for understanding losses in bulk conductors or in laminations used beyond their effective frequency range.

### Integrated Models and Advanced Concepts

In practice, hysteresis and eddy current losses occur simultaneously. For engineering purposes, models are needed that can capture the total core loss across a range of operating conditions.

#### Loss Separation and the Steinmetz Equation

A common approach to modeling core loss is to sum the contributions from the different mechanisms. The total loss power density, $P_v$, is often separated into three components: hysteresis, classical eddy current, and a third term called excess loss.

$$ P_v = P_h + P_e + P_{ex} $$

While this separation is physically meaningful, measuring each component individually is difficult. A widely used alternative is the empirical **Steinmetz equation**, which models the total core loss density with a single power-law expression :

$$ P_v = k f^\alpha B_{\mathrm{pk}}^\beta $$

The parameters $k$, $\alpha$ (the frequency exponent), and $\beta$ (the flux density exponent) are not [fundamental physical constants](@entry_id:272808) but are coefficients obtained by fitting this equation to measured loss data for a specific material under sinusoidal excitation.
- In operating regimes where [hysteresis loss](@entry_id:266219) dominates ($P_h \propto f^1$), the fitted exponent $\alpha$ will be close to 1.
- In regimes where classical [eddy current loss](@entry_id:1124138) dominates ($P_e \propto f^2$), the fitted exponent $\alpha$ will be close to 2.
- The exponent $\beta$, often called the Steinmetz exponent, typically falls in the range of 1.6 to 2.5 for steels, reflecting the nonlinear nature of the B-H loop.

The Steinmetz equation is a powerful tool for interpolation within the measurement range but must be used with caution. Its parameters are valid only for the conditions under which they were fitted, particularly the waveform shape. Applying it to non-sinusoidal waveforms, common in switched-mode power converters, requires significant modifications (e.g., the Generalized Steinmetz Equation, GSE).

#### Excess Loss: The Statistical Domain Theory

Careful measurements often reveal a discrepancy between the measured total loss and the sum of the quasi-static [hysteresis loss](@entry_id:266219) ($P_h$) and the classical [eddy current loss](@entry_id:1124138) ($P_e$). This discrepancy is termed **excess loss** or anomalous loss.

Its physical origin lies in the failure of the classical eddy current model's assumption of uniform magnetization reversal. In reality, magnetization changes are localized around a finite number of moving [domain walls](@entry_id:144723). This heterogeneous dynamic process creates microscopic eddy current fields that are more intense than the classical model predicts.

The statistical theory of losses, developed by Giorgio Bertotti, provides a physical model for this phenomenon. It treats the magnetization process as the collective behavior of a large number of stochastically activated magnetic objects (domain walls). The interaction between the local eddy currents generated by each moving wall leads to a self-consistent dynamic behavior for the ensemble. A key prediction of this theory is that the excess loss power density scales with the rate of change of magnetization as :

$$ P_{ex} \propto |\dot{M}|^{3/2} $$

For sinusoidal excitation, where the rate of change is proportional to frequency ($|\dot{M}| \propto f$), this predicts a frequency scaling of:

$$ P_{ex} \propto f^{3/2} $$

This $f^{3/2}$ scaling provides a physical basis for the frequency exponents often observed experimentally to be between the [linear dependence](@entry_id:149638) of hysteresis and the quadratic dependence of classical [eddy currents](@entry_id:275449), thereby accounting for a significant portion of what was previously just an "anomalous" discrepancy.