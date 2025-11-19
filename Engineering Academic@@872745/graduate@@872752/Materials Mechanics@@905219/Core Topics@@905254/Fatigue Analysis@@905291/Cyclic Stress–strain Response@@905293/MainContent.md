## Introduction
The behavior of materials under repeated, or cyclic, loading is a cornerstone of modern materials science and [structural engineering](@entry_id:152273). Unlike a single, monotonic load, cyclic stresses and strains induce complex microstructural changes that govern a component's long-term performance and durability. Understanding this response is paramount for preventing [fatigue failure](@entry_id:202922), which remains a primary cause of structural collapse in everything from aircraft to medical implants. A significant knowledge gap exists between a material's well-understood monotonic [stress-strain curve](@entry_id:159459) and its far more complex behavior after repeated plastic deformation. Simple models based on initial properties fail to capture critical phenomena like cyclic hardening, softening, and [mean stress relaxation](@entry_id:197977), which can dramatically alter a component's life.

This article provides a comprehensive overview of the [cyclic stress-strain response](@entry_id:193327) to bridge this gap. We will begin in "Principles and Mechanisms" by dissecting the fundamental concepts of [hysteresis](@entry_id:268538), the Bauschinger effect, and the [constitutive models](@entry_id:174726), like [isotropic and kinematic hardening](@entry_id:195752), used to describe them. Following this theoretical foundation, "Applications and Interdisciplinary Connections" will demonstrate how these principles are applied in practical engineering for [fatigue life prediction](@entry_id:197711) and [structural analysis](@entry_id:153861), and even in fields like biomechanics and astrophysics. Finally, "Hands-On Practices" will offer concrete problems to solidify your understanding of these critical concepts.

## Principles and Mechanisms

The response of ductile materials to cyclic loading is fundamentally different from their behavior under monotonic loading. Repeated plastic deformation introduces complex evolutions in the material's internal microstructural state, leading to a rich set of phenomena including cyclic hardening, softening, the Bauschinger effect, and ratcheting. Understanding these behaviors is critical for predicting the [fatigue life](@entry_id:182388) and ensuring the structural integrity of components subjected to vibrations or fluctuating service loads. This chapter elucidates the core principles and mechanistic models used to describe the [cyclic stress-strain response](@entry_id:193327) of metals.

### The Hysteresis Loop and its Characterization

When a metallic specimen is subjected to cyclic loading that induces [plastic deformation](@entry_id:139726), its stress-strain response does not trace a single curve. Instead, upon load reversal, the path deviates from the initial loading curve, forming a closed loop known as a **hysteresis loop**. This loop is the fundamental signature of [cyclic plasticity](@entry_id:176411). The area enclosed by the loop represents the plastic work dissipated as heat per unit volume during one cycle, a direct measure of the irreversible nature of the deformation.

After a certain number of initial transient cycles, the shape of the [hysteresis loop](@entry_id:160173) for a given strain or [stress amplitude](@entry_id:191678) often stabilizes. A stabilized loop provides a consistent measure of the material's mechanical state under that specific cyclic condition. To quantify the characteristics of such a loop, we define several key parameters based on the cycle's [extrema](@entry_id:271659) in stress and strain [@problem_id:2876258]. Let $\sigma_{\max}$ and $\sigma_{\min}$ be the maximum and minimum stresses in a cycle, and let $\varepsilon_{\max}$ and $\varepsilon_{\min}$ be the corresponding maximum and minimum strains.

The **stress range** $\Delta\sigma$ and **strain range** $\Delta\varepsilon$ define the total extent of the loop:
$$ \Delta\sigma = \sigma_{\max} - \sigma_{\min} $$
$$ \Delta\varepsilon = \varepsilon_{\max} - \varepsilon_{\min} $$

More commonly used in [fatigue analysis](@entry_id:191624) are the amplitudes, which represent half of the range. The **[stress amplitude](@entry_id:191678)** $\sigma_a$ and **strain amplitude** $\varepsilon_a$ are defined as:
$$ \sigma_a = \frac{\Delta\sigma}{2} = \frac{\sigma_{\max} - \sigma_{\min}}{2} $$
$$ \varepsilon_a = \frac{\Delta\varepsilon}{2} = \frac{\varepsilon_{\max} - \varepsilon_{\min}}{2} $$

The midpoint of the cyclic excursion is described by the mean values. The **[mean stress](@entry_id:751819)** $\sigma_m$ and **mean strain** $\varepsilon_m$ are:
$$ \sigma_m = \frac{\sigma_{\max} + \sigma_{\min}}{2} $$
$$ \varepsilon_m = \frac{\varepsilon_{\max} + \varepsilon_{\min}}{2} $$

Geometrically, the point $(\varepsilon_m, \sigma_m)$ corresponds to the center of the bounding rectangle that encloses the [hysteresis loop](@entry_id:160173), while $\varepsilon_a$ and $\sigma_a$ represent the horizontal and vertical half-spans of this rectangle, respectively [@problem_id:2876258].

Finally, the asymmetry of the stress cycle is conveniently captured by the **[stress ratio](@entry_id:195276)**, or **R-ratio**, defined as:
$$ R = \frac{\sigma_{\min}}{\sigma_{\max}} $$
A cycle with $R=-1$ is fully reversed and has zero [mean stress](@entry_id:751819) ($\sigma_m=0$). A cycle with $R=0$ involves loading from zero to a maximum stress and back.

### Monotonic versus Cyclic Stress-Strain Behavior

A material's initial, or **monotonic**, stress-strain curve describes its response to a single, unidirectional loading from a virgin (e.g., annealed) state. However, the internal dislocation structure evolves differently under cyclic loading than it does under monotonic straining. Consequently, the stabilized cyclic response is generally not the same as the monotonic one.

To characterize this, a series of strain-controlled tests are performed at different strain amplitudes $\varepsilon_a$. For each $\varepsilon_a$, the material is cycled until the corresponding [stress amplitude](@entry_id:191678) $\sigma_a$ stabilizes. The locus of the tips of these stabilized hysteresis loops, when plotted as $\sigma_a$ versus $\varepsilon_a$, forms the **Cyclic Stress-Strain Curve (CSSC)**.

Comparing the CSSC to the monotonic curve reveals two primary behaviors [@problem_id:2876342]:
1.  **Cyclic Hardening**: For many materials in an initially soft or annealed state (e.g., copper, some stainless steels), the CSSC lies above the monotonic curve. This means that to achieve a given strain amplitude, a higher [stress amplitude](@entry_id:191678) is required after cyclic stabilization. This hardening is due to a progressive increase in [dislocation density](@entry_id:161592) and the formation of stable, dense dislocation substructures (like cells or veins) that impede further [dislocation motion](@entry_id:143448).
2.  **Cyclic Softening**: For materials that are initially in a cold-worked or hardened state, the CSSC may lie below the monotonic curve. The cyclic deformation can induce [dynamic recovery](@entry_id:200182) mechanisms that rearrange and annihilate dislocations, leading to a "softer" structure and a lower stress response for a given strain amplitude.

These distinct behaviors are often modeled using a Ramberg-Osgood type power-law relationship. The monotonic curve is described by parameters $(K, n)$, while the CSSC is described by cyclic parameters $(K', n')$. The fundamental reason for the difference between $(K,n)$ and $(K',n')$ is that they represent two physically distinct microstructural states: one evolved under a single loading path, and the other a saturated state resulting from a specific cyclic history [@problem_id:2876342] [@problem_id:2876317].

### Mechanistic Modeling: Isotropic and Kinematic Hardening

To build predictive models of cyclic behavior, we must formalize the evolution of the material's internal state. In the framework of continuum plasticity, this is achieved by defining a **yield surface**, which delineates the boundary between elastic and plastic response in [stress space](@entry_id:199156). For metals, the pressure-insensitive von Mises [yield criterion](@entry_id:193897) is commonly used. Hardening is described by the evolution of this surface. Two fundamental types of hardening are distinguished: [isotropic and kinematic hardening](@entry_id:195752) [@problem_id:2876325].

#### Isotropic Hardening

**Isotropic hardening** corresponds to a uniform expansion of the [yield surface](@entry_id:175331), without any change in its center. The size of the elastic domain, characterized by the current yield stress $\sigma_y$, increases with [plastic deformation](@entry_id:139726). The yield condition is simply $|\sigma| \le \sigma_y(p)$, where $p$ is a measure of accumulated plastic strain. This model is associated with an increase in the overall resistance to dislocation motion, such as an increase in the total dislocation density (forest hardening).

#### Kinematic Hardening and the Bauschinger Effect

**Kinematic hardening** describes a translation of the [yield surface](@entry_id:175331) in [stress space](@entry_id:199156), without a change in its size. The center of the yield surface is no longer at the origin but is described by a tensor known as the **backstress**, $\boldsymbol{\alpha}$. The yield condition becomes $f(\boldsymbol{\sigma} - \boldsymbol{\alpha}) \le 0$. The [backstress](@entry_id:198105) represents the development of directional internal stresses within the material's [microstructure](@entry_id:148601), for example due to dislocation pile-ups at grain boundaries or the heterogeneous stress fields between hard and soft phases.

The crucial experimental observation that differentiates these two hardening types is the **Bauschinger effect**: a reduction in the [yield strength](@entry_id:162154) upon load reversal. After deforming a material plastically in one direction (e.g., tension), it is found to yield at a lower stress magnitude when subsequently loaded in the opposite direction (compression) [@problem_id:2876325].

A pure [isotropic hardening](@entry_id:164486) model cannot capture this phenomenon. For instance, a material with $\sigma_{y0} = 250\,\mathrm{MPa}$ that hardens isotropically to a current yield stress of $274\,\mathrm{MPa}$ is predicted to have a reverse yield stress of $-274\,\mathrm{MPa}$. If the experiment shows reverse yielding at $-180\,\mathrm{MPa}$, the isotropic model is clearly inadequate.

Kinematic hardening, however, naturally reproduces the Bauschinger effect. During tensile loading, the yield surface shifts in the direction of the applied stress, developing a positive backstress $\alpha > 0$. In a [combined hardening](@entry_id:186067) model, the backstress required to account for a forward [flow stress](@entry_id:198884) of $274\,\mathrm{MPa}$ and a reverse yield of $-180\,\mathrm{MPa}$ would be $\alpha = (274 - 180)/2 = 47\,\mathrm{MPa}$. This positive [backstress](@entry_id:198105) is what captures the Bauschinger effect by shifting the elastic range, demonstrating its essential role [@problem_id:2876318].

### Advanced Constitutive Laws for Cyclic Plasticity

Real materials exhibit a combination of [isotropic and kinematic hardening](@entry_id:195752), and the evolution of these internal variables can be complex. Advanced models aim to capture this complexity with physically motivated evolution laws.

#### Evolution of Isotropic Hardening

The change in the [yield surface](@entry_id:175331) size, $\sigma_y$, can be related to the evolution of the overall [dislocation density](@entry_id:161592), $\rho$. A common micro-mechanical model is the Kocks-Mecking equation, which posits that the rate of change of dislocation density with accumulated plastic strain $p$ is a balance between a storage term (often proportional to $\sqrt{\rho}$) and a [dynamic recovery](@entry_id:200182) term (proportional to $\rho$). When combined with the Taylor relation, which links [flow stress](@entry_id:198884) to [dislocation density](@entry_id:161592) ($\sigma_f \propto \sqrt{\rho}$), this leads to a macroscopic evolution law for the [isotropic hardening](@entry_id:164486) variable [@problem_id:2876317]. A widely used form is the Voce law, which expresses an exponential approach to a saturation value:
$$ \sigma_y(p) = \sigma_{y0} + Q\left(1 - \exp(-bp)\right) $$
Here, $Q$ represents the total amount of hardening available, and $b$ controls the rate at which saturation is approached. This form correctly captures the diminishing rate of hardening observed at [large strains](@entry_id:751152).

#### Evolution of Kinematic Hardening

Modeling the evolution of the backstress $\boldsymbol{\alpha}$ is key to accurately predicting cyclic behavior.

A simple **linear [kinematic hardening](@entry_id:172077)** model (Prager's rule) proposes that the [backstress](@entry_id:198105) increment is proportional to the plastic strain increment: $d\boldsymbol{\alpha} = C d\boldsymbol{\varepsilon}^p$. While simple, this model predicts that under certain loading paths, the backstress can grow without bound. This leads to the prediction of a constant, non-decaying rate of plastic strain accumulation (ratcheting) under asymmetric stress cycling, a behavior often termed **pathological ratcheting** as it is physically unrealistic for most materials [@problem_id:2876297].

To correct this, **nonlinear [kinematic hardening](@entry_id:172077)** models were introduced. The most influential is the **Armstrong-Frederick (AF)** model, which adds a "[dynamic recovery](@entry_id:200182)" term to the evolution law:
$$ d\boldsymbol{\alpha} = C d\boldsymbol{\varepsilon}^p - \gamma \boldsymbol{\alpha} dp $$
where $dp$ is the increment of accumulated plastic strain and $\gamma$ is a material constant. The recovery term, $-\gamma \boldsymbol{\alpha} dp$, opposes the growth of [backstress](@entry_id:198105) and causes it to saturate at a value proportional to $C/\gamma$. This saturation is crucial. It ensures that the ratcheting rate decays over time and allows the model to predict shakedown. A simple calculation using the AF law demonstrates its ability to capture the Bauschinger effect quantitatively [@problem_id:2876313]. Furthermore, the saturation property resolves the issue of pathological ratcheting, providing a much more realistic prediction of long-term cyclic response [@problem_id:2876297].

To capture the complex shape of [hysteresis](@entry_id:268538) loops, which often show a sharp "knee" upon reversal followed by a more gradual approach to the peak stress, a single AF component is often insufficient. The **Chaboche model** extends this concept by representing the total backstress as a superposition of several AF components [@problem_id:2876330]:
$$ \boldsymbol{\alpha} = \sum_{i=1}^{N} \boldsymbol{\alpha}_i, \quad \text{with} \quad d\boldsymbol{\alpha}_i = C_i d\boldsymbol{\varepsilon}^p - \gamma_i \boldsymbol{\alpha}_i dp $$
By selecting components with different parameters, one can model behavior across multiple time scales. A component with a large $\gamma_i$ value will saturate quickly over a small plastic strain range, capturing the rapid transient and the sharp initial curvature of the stress-strain curve. A component with a small $\gamma_i$ will saturate slowly, capturing the gradual evolution of the loop shape towards its stabilized state over many cycles. This superposition of exponential responses provides a powerful and flexible tool for fitting and predicting complex cyclic phenomena.

### Advanced Cyclic Phenomena

#### Ratcheting and Shakedown

When a material is subjected to stress-controlled cycling with a non-zero [mean stress](@entry_id:751819) ($\sigma_m \neq 0$), it may exhibit **ratcheting**, which is a progressive, cycle-by-cycle accumulation of plastic strain in the direction of the mean stress. If this accumulation ceases after a number of cycles, the material is said to have achieved **shakedown**. Shakedown can be **elastic** (the subsequent response is purely elastic) or **plastic** (a stable, closed hysteresis loop is formed with no net strain gain per cycle).

Using a model like Armstrong-Frederick, it is possible to derive criteria that separate these regimes. For a given [stress amplitude](@entry_id:191678) $\sigma_a$, there exists a critical [mean stress](@entry_id:751819) beyond which shakedown is not possible and ratcheting will occur indefinitely. For the AF model, the boundary between shakedown and ratcheting in the $(\sigma_m, \sigma_a)$ plane is given by the condition $|\sigma_m| + \sigma_a = \sigma_y + C/\gamma$, where $C/\gamma$ is the saturation limit of the backstress [@problem_id:2876316]. This highlights the predictive capability of these [constitutive models](@entry_id:174726) for [structural design](@entry_id:196229) against cyclic failure.

#### Nonproportional Hardening

The discussion so far has implicitly assumed uniaxial or proportional multiaxial loading. In **[proportional loading](@entry_id:191744)**, all components of the stress (or strain) tensor vary in constant ratio, meaning the [principal directions](@entry_id:276187) of the stress/[strain tensor](@entry_id:193332) remain fixed. In many real-world applications, however, components experience **nonproportional loading**, where the ratios between stress components change during a cycle, causing the principal axes to rotate.

A classic example is out-of-phase tension-torsion, where [axial strain](@entry_id:160811) varies as $\sin(\omega t)$ and [shear strain](@entry_id:175241) as $\sin(\omega t + \phi)$ with $\phi = \pi/2$ [@problem_id:2876268]. Experiments consistently show that materials exhibit significantly more cyclic hardening under nonproportional loading paths compared to proportional paths, even when the von Mises equivalent strain amplitude is identical.

The physical origin of this **nonproportional hardening** lies in the activation of slip systems at the crystal level. Under [proportional loading](@entry_id:191744), a fixed set of slip systems is primarily active, allowing dislocations to organize into relatively stable, low-energy patterns. Under nonproportional loading, the rotation of the principal stress axes continuously changes the set of most highly stressed slip systems. This forces dislocations to move through and interact with "forest" dislocations created on different systems in a previous part of the cycle. This process, known as **latent hardening**, is highly effective at creating complex, high-energy dislocation tangles that strongly resist further plastic flow. This increased microscopic resistance manifests as a larger macroscopic [stress response](@entry_id:168351), providing a powerful demonstration of the path-dependent nature of [plastic deformation](@entry_id:139726) [@problem_id:2876268].