## Introduction
The behavior of a flame—its structure, stability, propagation speed, and emissions—is fundamentally determined by a single preceding condition: the state of mixing between fuel and oxidizer. While combustion appears in countless forms, from a simple candle flame to the complex [reacting flows](@entry_id:1130631) inside a jet engine, these phenomena can be systematically understood by classifying them into distinct regimes. However, moving beyond a purely descriptive classification requires a rigorous framework based on the underlying physics of transport and chemical reaction. This article addresses this need by providing a comprehensive overview of the three primary combustion modes: premixed, non-premixed, and partially premixed.

This exploration is structured to build a complete understanding from first principles to practical application. The first chapter, **Principles and Mechanisms**, establishes the foundational definitions using conserved scalars like the mixture fraction, explores the distinct physical processes governing each flame type, and introduces quantitative tools for analysis. Building on this, the second chapter, **Applications and Interdisciplinary Connections**, demonstrates how this classification informs advanced diagnostics, drives the development of sophisticated computational models, and underpins the design of modern engines and gas turbines. Finally, the **Hands-On Practices** chapter provides opportunities to apply these theoretical concepts to solve practical problems in [combustion analysis](@entry_id:144338). Together, these sections offer a graduate-level guide to classifying and understanding the multifaceted nature of flames.

## Principles and Mechanisms

The state of mixing between fuel and oxidizer prior to reaction fundamentally dictates the structure, propagation mechanisms, and dynamics of a flame. This chapter elucidates the principles that underpin the classification of combustion into three primary modes: **premixed**, **non-premixed**, and **partially premixed**. We will establish rigorous definitions based on conserved scalars, explore the distinct physical mechanisms governing each mode, and introduce quantitative tools used to analyze and classify [combustion regimes](@entry_id:1122679) in complex flows.

### The Foundational Classification: Premixed, Non-premixed, and Partially Premixed Flames

The most elementary classification of flames is based on the spatial distribution of fuel and oxidizer in the unburned gas upstream of the main reaction zone. This initial state of the reactants determines whether the rate of combustion is controlled primarily by chemical kinetics, by molecular mixing, or by a combination of both.

Let $Y_F(\mathbf{x})$ and $Y_O(\mathbf{x})$ denote the local mass fractions of fuel and oxidizer, respectively. We can also define a **mixture fraction**, $Z(\mathbf{x}, t)$, a conserved scalar that tracks the proportion of mass at a given point that originated from the fuel stream versus the oxidizer stream. By convention, $Z=1$ in the pure fuel stream and $Z=0$ in the pure oxidizer stream. Under the common assumption of equal mass and thermal diffusivities (unity Lewis number), $Z$ is governed by a sourceless [advection-diffusion equation](@entry_id:144002), making it an ideal tracer for the mixing process. Using these quantities, we can define the three canonical combustion modes :

*   **Premixed Flames:** In an ideal premixed flame, fuel and oxidizer are mixed homogeneously at a molecular level before entering the reaction zone. This corresponds to a state where both $Y_F(\mathbf{x}) > 0$ and $Y_O(\mathbf{x}) > 0$ within the unburned reactant stream, and their ratio is constant everywhere. Consequently, the mixture fraction is spatially uniform, $Z(\mathbf{x}) = Z_0$, and the [equivalence ratio](@entry_id:1124617) is also constant, $\phi(\mathbf{x}) = \phi_0$. Combustion occurs as a thin reaction-diffusion front that propagates into this quiescent, uniform mixture. Canonical laboratory examples include the one-dimensional flat flame stabilized on a porous plug burner and the conical flame of a Bunsen burner.

*   **Non-premixed Flames:** Also known as **diffusion flames**, this mode occurs when fuel and oxidizer are supplied in separate streams and are not mixed prior to reaction. They mix and react simultaneously. In the unburned regions, fuel and oxidizer are segregated, a condition mathematically expressed as $Y_F(\mathbf{x}) Y_O(\mathbf{x}) = 0$ almost everywhere. Mixing creates spatial gradients in the mixture fraction, which varies continuously from $Z=0$ in the oxidizer stream to $Z=1$ in the fuel stream. The chemical reaction is confined to the region where the reactants meet. Classic examples include a fuel jet issuing into an oxidizing atmosphere (like a candle flame) and the [counterflow diffusion flame](@entry_id:1123127) stabilized in the stagnation plane between two opposed jets.

*   **Partially Premixed Flames:** This is a hybrid mode exhibiting features of both premixed and [non-premixed combustion](@entry_id:1128819). Here, the reactants are partially mixed upstream, meaning there are regions where $Y_F(\mathbf{x}) > 0$ and $Y_O(\mathbf{x}) > 0$. However, unlike a purely premixed system, the mixture is not homogeneous. The equivalence ratio $\phi(\mathbf{x})$ and mixture fraction $Z(\mathbf{x})$ vary spatially within the reactant stream. This complex state gives rise to multifaceted flame structures where both premixed-like propagation and mixing-controlled diffusion combustion can occur simultaneously. A lifted jet flame, where fuel and air partially mix before stabilizing downstream, is a prime example of this mode.

### The Mixture Fraction and its Stoichiometric Value

The mixture fraction $Z$ is a powerful conceptual tool, particularly for non-premixed and partially premixed systems. While simple definitions based on two-stream mixing exist, a more robust and general formulation is based on the conservation of chemical elements. Bilger's formulation provides such a definition for hydrocarbon fuels . A conserved scalar $\beta$ is defined based on the elemental mass fractions of carbon ($Y_C$), hydrogen ($Y_H$), and oxygen ($Y_O$), and their respective atomic weights ($W_C, W_H, W_O$):
$$
\beta \equiv 2\frac{Y_C}{W_C} + \frac{1}{2}\frac{Y_H}{W_H} - \frac{Y_O}{W_O}
$$
This specific combination of element mass fractions is conserved during chemical reactions. The mixture fraction $Z$ is then defined as a normalized version of $\beta$:
$$
Z \equiv \frac{\beta - \beta_{\mathrm{ox}}}{\beta_{\mathrm{f}} - \beta_{\mathrm{ox}}}
$$
where the subscripts 'f' and 'ox' denote the values in the pure fuel and pure oxidizer streams, respectively. This definition ensures that $Z=0$ in the oxidizer stream and $Z=1$ in the fuel stream.

A pivotal concept in this framework is the **[stoichiometric mixture fraction](@entry_id:1132448), $Z_{st}$**. This is the specific value of $Z$ at which the amounts of fuel and oxidizer are in exact stoichiometric proportion for complete combustion. For hydrocarbon combustion, the major products are $\mathrm{CO_2}$ and $\mathrm{H_2O}$. The scalar $\beta$ is constructed to be zero for these products (and for inert species like $\mathrm{N_2}$). Therefore, the stoichiometric condition corresponds to $\beta_{st} = 0$. Substituting this into the definition of $Z$ gives:
$$
Z_{st} = \frac{0 - \beta_{\mathrm{ox}}}{\beta_{\mathrm{f}} - \beta_{\mathrm{ox}}} = \frac{-\beta_{\mathrm{ox}}}{\beta_{\mathrm{f}} - \beta_{\mathrm{ox}}}
$$
As an example, for a non-premixed methane ($\mathrm{CH_4}$) flame with air as the oxidizer (mole fractions $x_{O_2}=0.21$, $x_{N_2}=0.79$), one can calculate the values of $\beta$ in the pure fuel stream ($\beta_f = 0.25$) and the air stream ($\beta_{ox} \approx -0.01456$). This yields a [stoichiometric mixture fraction](@entry_id:1132448) of $Z_{st} \approx 0.05505$ . This value is small, indicating that a stoichiometric methane-air mixture is composed of only about 5.5% mass from the fuel stream and 94.5% mass from the air stream.

In the limit of infinitely fast chemistry, a [non-premixed flame](@entry_id:1128820) collapses to an infinitesimally thin reaction sheet. This sheet must be located precisely on the isosurface in the flow where the mixture fraction equals its stoichiometric value, $Z(\mathbf{x}, t) = Z_{st}$. In real flames with finite-rate chemistry, the reaction zone has a finite thickness, but its peak temperature and heat release are still found very close to this stoichiometric surface. Thus, $Z_{st}$ is the single most important parameter determining the location and organizing the structure of a [non-premixed flame](@entry_id:1128820).

### Distinct Mechanisms of Premixed and Non-premixed Combustion

The initial state of the reactants leads to fundamentally different mechanisms for heat release and [flame propagation](@entry_id:1125066) in the premixed and non-premixed limits .

#### Premixed Flames: The Propagating Reaction-Diffusion Wave

A premixed flame is a self-propagating wave sustained by a delicate balance between chemical reaction and [molecular transport](@entry_id:195239). The reaction releases heat, which is conducted upstream into the unburned mixture. This [preheating](@entry_id:159073) raises the temperature of the reactants, exponentially increasing the reaction rate until a [self-sustaining cycle](@entry_id:191058) is established.

The speed at which this wave propagates relative to the unburned gas is the **[laminar burning velocity](@entry_id:1127023), $S_L$**. For a given mixture composition, temperature, and pressure, $S_L$ is an intrinsic physical property. Mathematically, it emerges as an **eigenvalue** from the solution of the coupled conservation equations for species and energy. A steady, one-dimensional flame structure connecting the unburned and burned states exists only for a unique value of $S_L$.

From dimensional analysis, the burning velocity scales with the square root of the product of a characteristic diffusivity and a characteristic reaction rate: $S_L \sim \sqrt{\alpha \cdot \bar{\omega}}$, where $\alpha$ is the [thermal diffusivity](@entry_id:144337) and $\bar{\omega}$ is the reaction rate. The heat release is distributed over a finite thickness, $\delta_L \sim \alpha / S_L$. Crucially, $S_L$ is determined by the internal thermochemical and [transport properties](@entry_id:203130) of the mixture and is independent of large-scale external fluid motion or mixing processes.

#### Non-premixed Flames: Mixing-Controlled Combustion and Extinction

In a non-premixed flame, the rate of combustion is governed by the rate at which fuel and oxidizer can be brought together by [molecular diffusion](@entry_id:154595). The chemical kinetics are often so fast at typical flame temperatures that the overall process is limited by this mixing rate.

The intensity of molecular mixing is quantified by the **scalar dissipation rate, $\chi$**, defined as:
$$
\chi \equiv 2 D |\nabla Z|^2
$$
where $D$ is the molecular diffusivity of the mixture fraction. With units of $\mathrm{s}^{-1}$, $\chi$ can be interpreted as the inverse of a characteristic mixing timescale, $t_{mix} \sim \chi^{-1}$. A high value of $\chi$ implies steep gradients in the mixture fraction and thus rapid mixing.

This parameter plays a dual role. While mixing is necessary to bring reactants together, excessive mixing can extinguish the flame. A [non-premixed flame](@entry_id:1128820) resides in a thin layer where heat is generated. If the [scalar dissipation](@entry_id:1131248) rate becomes too high, the mixing layer becomes very thin, $\ell_Z \sim \sqrt{D/\chi}$ . The steep gradients enhance the diffusive loss of heat and reactive chemical species (radicals) away from the reaction zone. If these losses exceed the rate of heat production by chemistry, the flame temperature drops and the flame extinguishes.

This leads to the concept of **extinction**, which can be understood by comparing the mixing timescale ($t_{mix} \sim \chi^{-1}$) with a characteristic chemical timescale ($t_{chem}$). A stable flame exists when chemistry is faster than mixing ($t_{chem}  t_{mix}$). Extinction is approached when mixing becomes much faster than chemistry ($t_{mix} \ll t_{chem}$), which corresponds to the scalar dissipation rate exceeding a critical value, $\chi > \chi_{q}$. For instance, a hypothetical flame with a chemical time of $t_{chem} = 10^{-3}$ s would be stable at a moderate [scalar dissipation](@entry_id:1131248) of $\chi = 5 \ \mathrm{s}^{-1}$ (where $t_{mix} = 0.2 \ \mathrm{s} \gg t_{chem}$), but prone to extinction at a high [scalar dissipation](@entry_id:1131248) of $\chi = 4500 \ \mathrm{s}^{-1}$ (where $t_{mix} \approx 2.2 \times 10^{-4} \ \mathrm{s}  t_{chem}$) .

### The Realm of Partial Premixing

Most practical combustion systems are neither perfectly premixed nor purely non-premixed, but fall into the intermediate category of partially [premixed combustion](@entry_id:1130127). This regime is characterized by an inhomogeneous mixture of fuel and oxidizer entering the reaction zone.

The relationship between the local [equivalence ratio](@entry_id:1124617), $\phi$, and the mixture fraction, $Z$, provides a precise way to understand partial premixing . For a general two-stream mixing problem, where Stream 1 (fuel stream) has mass fractions ($Y_{F,1}, Y_{O_2,1}$) and Stream 2 (oxidizer stream) has ($Y_{F,2}, Y_{O_2,2}$), the local equivalence ratio is given by:
$$
\phi(Z) = s \frac{Y_F(Z)}{Y_{O_2}(Z)} = s \frac{Z Y_{F,1} + (1-Z) Y_{F,2}}{Z Y_{O_2,1} + (1-Z) Y_{O_2,2}}
$$
where $s$ is the stoichiometric oxygen-to-fuel mass ratio. In the ideal non-premixed case ($Y_{O_2,1} = 0, Y_{F,2} = 0$), $\phi$ spans from $0$ to $\infty$. However, if some fuel is added to the oxidizer stream ($Y_{F,2} > 0$), the mixture is flammable even at $Z=0$. This is partial premixing.

This inhomogeneity can lead to complex flame structures. A canonical example is the **triple flame**, which often forms at the stabilization point of lifted jet flames . A triple flame consists of three distinct parts: a fuel-rich premixed "wing," a fuel-lean premixed "wing," and a trailing non-premixed (diffusion) flame that connects them. This structure arises at the edge of a mixing layer where the mixture fraction gradient, $\nabla Z$, is non-zero and the $Z=Z_{st}$ isosurface exists. The gradient in $Z$ creates a flammable mixture on both the rich ($Z > Z_{st}$) and lean ($Z  Z_{st}$) sides of the stoichiometric line. This allows two [premixed flame](@entry_id:203757) fronts to anchor onto the central diffusion flame, propagating outwards into the partially premixed reactants. The overall structure is a robust hybrid of both premixed and [non-premixed combustion](@entry_id:1128819) modes  .

### Quantitative Classification in Complex Flows

Analyzing flames in turbulent flows, where multiple combustion modes can coexist and interact, requires more sophisticated quantitative tools for classification.

#### Regime Diagrams for Turbulent Premixed Combustion

For turbulent [premixed combustion](@entry_id:1130127), the interaction between turbulence and the flame is often categorized using a regime diagram, most famously the **Borghi-Peters diagram**. This diagram is plotted using two key dimensionless numbers that compare the characteristic scales of turbulence and chemistry .

1.  The **Damköhler number ($Da$)** is the ratio of a large-scale turbulent timescale ($\tau_t = l/u'$, where $l$ is the integral length scale and $u'$ is the RMS velocity fluctuation) to the chemical timescale ($\tau_c = \delta_L/S_L$).
    $$ Da \equiv \frac{\tau_t}{\tau_c} = \frac{l/u'}{\delta_L/S_L} $$
    When $Da \gg 1$, turbulence is slow compared to chemistry, and the flame front remains a thin, continuous, but wrinkled surface. When $Da \ll 1$, turbulence is so fast that it can disrupt the flame structure and distribute the reaction over a broad volume.

2.  The **Karlovitz number ($Ka$)** is the ratio of the chemical timescale to the smallest turbulent timescale, the Kolmogorov time ($\tau_\eta = (\nu/\epsilon)^{1/2}$, where $\epsilon$ is the [turbulent dissipation rate](@entry_id:756234)).
    $$ Ka \equiv \frac{\tau_c}{\tau_\eta} $$
    When $Ka \ll 1$, even the smallest eddies are too slow to affect the flame's internal structure. When $Ka \gg 1$, the smallest eddies are faster than the chemistry and can penetrate and disrupt the inner layers of the flame front.

Using these numbers, a flame can be classified into regimes such as **wrinkled flamelets** ($u'  S_L, Ka \ll 1$), **corrugated flamelets** ($u' > S_L, Ka  1$), **[thin reaction zones](@entry_id:1133103)** ($Ka > 1$), and the **distributed reaction zone** ($Da  1$). For example, a flame with $S_L=0.4 \ \mathrm{m/s}$, $\delta_L=0.5 \ \mathrm{mm}$ in a turbulent flow with $u'=2.0 \ \mathrm{m/s}$ and $l=5 \ \mathrm{mm}$ would have $Da \approx 2$ and $Ka \approx 13$. This combination of $Da = \mathcal{O}(1)$ and $Ka \gg 1$ places it in the thin reaction zones regime .

#### Local Pointwise Classification using Scalar Gradients

In partially premixed or stratified turbulent flames, a single regime classification is insufficient. Instead, local, pointwise metrics are used to identify the combustion mode at each point in the flow field from simulation or experimental data. This requires defining a **reaction progress variable, $c$**, a scalar that monotonically increases from $0$ in unburned reactants to $1$ in fully burned products. A robust definition, insensitive to mixture fraction variations, is based on the normalized mass fraction of major products :
$$
c=\frac{\left(Y_{\mathrm{CO_{2}}}+Y_{\mathrm{H_{2}O}}\right)-\left(Y_{\mathrm{CO_{2}}}+Y_{\mathrm{H_{2}O}}\right)_{\mathrm{ub}}}{\left(Y_{\mathrm{CO_{2}}}+Y_{\mathrm{H_{2}O}}\right)_{\mathrm{ad}}-\left(Y_{\mathrm{CO_{2}}}+Y_{\mathrm{H_{2}O}}\right)_{\mathrm{ub}}}
$$
where 'ub' and 'ad' refer to unburned and adiabatic burned reference states at the local mixture fraction.

The local burning mode can then be classified by analyzing the geometric alignment of the gradients of the reactant mass fractions, $\nabla Y_F$ and $\nabla Y_O$. The **Takeno flame index**, $I_T = \nabla Y_F \cdot \nabla Y_O$, provides a first-order classification :
*   **Premixed Mode ($I_T > 0$):** Fuel and oxidizer are consumed concurrently. Their concentrations both decrease across the flame front, so their gradients are aligned, pointing from the burned side to the unburned side.
*   **Non-premixed Mode ($I_T  0$):** Fuel and oxidizer diffuse towards the reaction zone from opposite sides. Their gradients are anti-aligned.

A more rigorous classification also incorporates the gradient of the [progress variable](@entry_id:1130223), $\nabla c$, which defines the local flame-normal direction (pointing from reactants to products) . The following rules, based on the physics of reactant transport, can be formulated:
*   **Premixed:** Characterized by simultaneous consumption of both reactants. This requires that the gradients of both fuel and oxidizer are anti-aligned with the [progress variable](@entry_id:1130223) gradient.
    $$ \nabla Y_F \cdot \nabla Y_O > 0 \quad \text{and} \quad \nabla Y_F \cdot \nabla c  0 \quad \text{and} \quad \nabla Y_O \cdot \nabla c  0 $$
*   **Non-premixed:** Characterized by segregated reactants, where one is consumed while the other diffuses towards the reaction zone. This results in an asymmetric relationship with the progress variable.
    $$ \nabla Y_F \cdot \nabla Y_O  0 \quad \text{and} \quad \mathrm{sign}(\nabla Y_F \cdot \nabla c) = - \mathrm{sign}(\nabla Y_O \cdot \nabla c) $$

Points within active reaction zones ($\|\nabla c\| > 0$) that do not fit these strict criteria are classified as partially premixed. To improve robustness, especially in complex partially premixed zones where tangential gradients can cause ambiguity, augmented flame indices have been proposed. A successful index should be selective to the reaction zone and depend only on the components of the reactant gradients normal to the flame front, ensuring that the classification reflects the physics of consumption across the flame rather than tangential mixing effects .