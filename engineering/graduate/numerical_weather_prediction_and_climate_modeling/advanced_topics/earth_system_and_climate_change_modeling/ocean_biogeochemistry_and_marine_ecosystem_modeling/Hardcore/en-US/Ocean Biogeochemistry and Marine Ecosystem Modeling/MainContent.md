## Introduction
The ocean's vast [biogeochemical cycles](@entry_id:147568) and teeming ecosystems play a pivotal role in regulating Earth's climate and supporting global [food webs](@entry_id:140980). Understanding and predicting the behavior of this complex system requires translating the intricate interplay of physics, chemistry, and biology into a quantitative framework. This is the central challenge addressed by [ocean biogeochemistry](@entry_id:1129047) and marine [ecosystem modeling](@entry_id:191400). These models serve as virtual laboratories, allowing scientists to explore everything from plankton blooms to the long-term [sequestration](@entry_id:271300) of atmospheric carbon dioxide. However, constructing these models is a formidable task, demanding a deep understanding of the underlying principles and their mathematical representation.

This article provides a comprehensive guide to the foundations of marine [ecosystem modeling](@entry_id:191400), designed for graduate-level students and researchers. It bridges the gap between theoretical concepts and practical application across three interconnected chapters. First, in **Principles and Mechanisms**, we will deconstruct the core of these models, starting with the universal [advection-diffusion-reaction equation](@entry_id:156456) and examining the parameterizations for key physical and biological processes. Next, **Applications and Interdisciplinary Connections** will demonstrate how these building blocks are assembled to investigate real-world scientific questions, from the dynamics of the [biological carbon pump](@entry_id:140846) to the ocean's role in the global climate system. Finally, **Hands-On Practices** will provide concrete exercises to solidify your understanding of model construction, stability analysis, and [steady-state solutions](@entry_id:200351), equipping you with the foundational skills for computational oceanography.

## Principles and Mechanisms

The dynamics of marine biogeochemical tracers, from dissolved nutrients to plankton biomass, are governed by the interplay of physical transport and biological or chemical transformations. Ocean [biogeochemical models](@entry_id:1121600) are, at their core, numerical implementations of a set of governing equations that describe these processes. This chapter elucidates the fundamental principles and mechanisms that form the building blocks of these models, from the universal laws of transport to the specific parameterizations of ecosystem interactions.

### The Advection-Diffusion-Reaction Framework

The evolution of any biogeochemical substance in the ocean can be described by a master equation rooted in the principle of mass conservation. We consider a tracer with a concentration $C(\mathbf{x}, t)$, representing the amount of the substance per unit volume at position $\mathbf{x}$ and time $t$. The total amount of this tracer within any fixed control volume $V$ can only change due to two processes: the net flux of the tracer across the volume's boundary $\partial V$, and the net effect of [sources and sinks](@entry_id:263105) within the volume.

This principle is expressed mathematically as the **[advection-diffusion-reaction](@entry_id:746316) (ADR) equation**. In its most general local form, it is written as:
$$ \frac{\partial C}{\partial t} + \nabla \cdot (\mathbf{u} C) = \nabla \cdot (\mathbf{K} \nabla C) + S $$
Here, $\frac{\partial C}{\partial t}$ is the local rate of change of the tracer concentration. The term $\nabla \cdot (\mathbf{u} C)$ represents the divergence of the advective flux, where $\mathbf{u}(\mathbf{x}, t)$ is the fluid velocity field; this term quantifies how the ocean's currents concentrate or dilute the tracer at a point. The term $\nabla \cdot (\mathbf{K} \nabla C)$ represents the divergence of the [diffusive flux](@entry_id:748422), which parameterizes the effects of sub-grid-scale turbulent motions. This is a **Fickian closure**, where $\mathbf{K}$ is a tensor of eddy diffusivities and mixing is assumed to act down the mean concentration gradient. Finally, $S(C, \ldots)$ is the net source-sink term, encapsulating all biogeochemical transformations—such as biological uptake, [remineralization](@entry_id:194757), or chemical reactions—that produce or consume the tracer.

In large-scale ocean models, the flow field $\mathbf{u}$ is often assumed to be incompressible, a condition mathematically stated as $\nabla \cdot \mathbf{u} = 0$. This greatly simplifies the advection term, as the [vector calculus](@entry_id:146888) identity $\nabla \cdot (\mathbf{u} C) = (\nabla \cdot \mathbf{u})C + \mathbf{u} \cdot \nabla C$ reduces to $\nabla \cdot (\mathbf{u} C) = \mathbf{u} \cdot \nabla C$. The ADR equation then takes its "advective form" :
$$ \frac{\partial C}{\partial t} + \mathbf{u} \cdot \nabla C = \nabla \cdot (\mathbf{K} \nabla C) + S $$

The left side of this equation is the **material derivative**, often denoted $\frac{DC}{Dt}$. It represents the rate of change of concentration experienced by an observer moving with the fluid parcel. The distinction between the local rate of change $\frac{\partial C}{\partial t}$ (what happens at a fixed geographical point) and the material derivative is crucial.

Tracer behavior is classified based on the source-sink term $S$.
- A **[conservative tracer](@entry_id:1122920)** is one with no internal sources or sinks ($S=0$). Its concentration is altered only by physical transport (advection and diffusion). In the idealized case of pure advection (no diffusion), the governing equation becomes $\frac{DC}{Dt} = 0$, meaning the concentration of the tracer is conserved along the flow path of each fluid parcel. 
- A **reactive tracer** is one that is transformed by biogeochemical processes ($S \neq 0$). Nearly all tracers of biological interest—nutrients, oxygen, plankton biomass—are reactive.

The integral form of the conservation law is particularly insightful for understanding budgets in a closed or semi-enclosed domain. For a volume $V$ with no-flux boundaries (i.e., no transport of the tracer across its edges), the rate of change of the total tracer inventory, $\int_V C \, dV$, is solely determined by the domain-integrated source-sink term, $\int_V S \, dV$. For a [conservative tracer](@entry_id:1122920) in such a closed domain, the total inventory is strictly conserved, even if diffusion internally redistributes the tracer. For a reactive tracer, such as one subject to first-order decay $S = -\lambda C$, the total inventory in a closed domain will decrease exponentially over time. 

### Physical Forcing and Transport Parameterization

The velocity field $\mathbf{u}$ and the eddy diffusivity tensor $\mathbf{K}$ are not arbitrary; they are provided by the physical component of the Earth System Model. These terms represent the physical environment that shapes biogeochemical patterns. Two transport processes are of paramount importance: vertical mixing in the upper ocean and [air-sea gas exchange](@entry_id:1120896) at the surface.

#### Vertical Mixing

Vertical mixing in the upper ocean is a critical gateway process. It governs the flux of light into the ocean and the flux of nutrients from the resource-rich deep waters into the sunlit euphotic zone, thereby controlling the overall productivity of most of the world's oceans. This vertical [turbulent flux](@entry_id:1133512), arising from the correlation between fluctuations in vertical velocity ($w'$) and tracer concentration ($C'$), is a sub-grid-scale process that must be parameterized. The most common approach is the **downgradient K-theory closure**:
$$ \overline{w'C'} = -K_z \frac{\partial \overline{C}}{\partial z} $$
Here, the overbar denotes a Reynolds average, and $K_z$ is the vertical eddy diffusivity, a parameter that represents the intensity of vertical turbulent mixing. Unlike molecular diffusivity, $K_z$ is not a property of the fluid but of the flow's turbulent state, varying by many orders of magnitude in space and time. Two major families of parameterization schemes are used to determine $K_z$ .

1.  **K-Profile Parameterization (KPP):** This is a widely used diagnostic scheme. It is built around the concept of a distinct ocean surface boundary layer. The scheme first diagnoses the depth of this layer, $h$, typically by finding the depth where a bulk Richardson number (comparing buoyancy to shear) exceeds a critical value. Then, it prescribes a specific vertical shape (a "profile") for $K_z$ within this layer, with its magnitude dependent on surface forcing (wind and buoyancy fluxes). A key feature of KPP is its inclusion of a **nonlocal transport** term. This term accounts for the action of large, coherent eddies in a convectively driven (unstable) boundary layer, which can transport tracers directly from the surface to the base of the layer, a process that cannot be represented by a purely local, downgradient flux.  

2.  **Turbulent Kinetic Energy (TKE) Closures:** These are prognostic schemes (e.g., the Mellor-Yamada family) that solve a transport equation for the [turbulent kinetic energy](@entry_id:262712), $e$. The TKE equation includes terms for production by velocity shear, production or destruction by buoyancy, and dissipation. The vertical eddy diffusivity $K_z$ is then calculated at each point as a function of the local TKE and a turbulent mixing length scale. These schemes are inherently local and do not require an *a priori* diagnosis of the boundary layer depth; instead, the turbulence "finds its own depth" by decaying where production terms vanish. 

#### Air-Sea Gas Exchange

For volatile tracers like carbon dioxide ($\text{CO}_2$), oxygen ($\text{O}_2$), or dimethyl sulfide (DMS), exchange with the atmosphere is a critical flux. This flux, $F$, is parameterized using a bulk formula that expresses it as the product of a kinetic coefficient and a concentration difference:
$$ F = k (c_{eq} - c_w) $$
Here, $c_w$ is the concentration of the dissolved gas in the bulk surface water, and $c_{eq}$ is the concentration the water would have if it were in thermodynamic equilibrium with the atmosphere. The two coefficients, $k$ and $c_{eq}$ (determined by solubility), encapsulate distinct physical and chemical principles.

-   **Solubility ($K_0$):** The equilibrium concentration $c_{eq}$ is determined by Henry's Law, which states that $c_{eq} = K_0 \cdot p_g$, where $p_g$ is the [partial pressure](@entry_id:143994) of the gas in the air. The solubility coefficient, $K_0$, is a thermodynamic property of the gas-water system, depending strongly on temperature and salinity. It sets the chemical potential driving the flux but does not influence the rate of transport itself. 

-   **Gas Transfer Velocity ($k$):** The kinetic coefficient $k$, known as the [gas transfer velocity](@entry_id:1125498) or piston velocity, has units of speed (e.g., cm/hr). It quantifies the rate of physical transport across the air-sea interface. In conceptual models like the "[two-film theory](@entry_id:152747)," transport is limited by molecular diffusion across a thin, stagnant boundary layer of thickness $\delta$ on the water side, such that $k = D/\delta$, where $D$ is the molecular diffusivity. The value of $k$ is therefore determined not by thermodynamics but by [hydrodynamics](@entry_id:158871) and molecular properties. It is strongly dependent on:
    -   **Wind Speed ($U$):** Higher wind speeds drive near-surface turbulence, which thins the boundary layer $\delta$ and thus increases $k$. This relationship is highly nonlinear, often parameterized with a quadratic or cubic dependence ($k \propto U^2$ or $U^3$). 
    -   **Schmidt Number ($Sc$):** The Schmidt number, $Sc = \nu/D$, is the dimensionless ratio of the kinematic viscosity of water ($\nu$) to the molecular diffusivity of the gas ($D$). Since $k$ is proportional to $D$, it is inversely related to $Sc$. Theoretical models and empirical data support a power-law relationship of the form $k \propto Sc^{-n}$, where $n$ is typically between $1/2$ and $2/3$. 

### Biogeochemical Reactions and Ecosystem Structure

The source-sink term, $S$, represents the rich web of biogeochemical transformations that occur in the ocean. Modeling this term involves describing the structure of the ecosystem and the functional forms of the processes that link its components.

#### Stoichiometry: The Elemental Composition of Life

A powerful organizing principle in [ocean biogeochemistry](@entry_id:1129047) is **stoichiometry**, the study of the elemental ratios in chemical reactions. In the 1930s, Alfred Redfield observed that the average [elemental composition](@entry_id:161166) of marine plankton and the ratios of dissolved nutrients in the deep ocean converged on a remarkably consistent [molar ratio](@entry_id:193577) of approximately $C:N:P = 106:16:1$. This **Redfield ratio** became a cornerstone of biogeochemical modeling. Models differ in how strictly they adhere to this principle.

-   **Fixed Stoichiometry Models:** These models assume that the elemental ratios within all phytoplankton biomass are constant and fixed at the Redfield ratio (or some other specified value). A direct consequence is that [nutrient uptake](@entry_id:191018) from the environment must also occur in this fixed proportion. While computationally simple, this approach cannot capture the observed flexibility of phytoplankton physiology. 

-   **Variable Stoichiometry (Quota) Models:** These models treat the internal cellular elemental ratios as dynamic variables. For example, the nitrogen-to-carbon ratio (the N-quota) within a phytoplankton cell is a state variable that changes in response to environmental conditions. Under [nitrogen limitation](@entry_id:1128726), a cell may continue to fix carbon, leading to a higher C:N ratio. This flexibility allows for phenomena like "luxury uptake" (storing nutrients when abundant) and is more ecologically realistic. 

The choice of stoichiometric model has profound consequences for elemental cycles. For instance, the amount of oxygen consumed during the [remineralization](@entry_id:194757) of organic matter depends on its [elemental composition](@entry_id:161166). The complete [aerobic respiration](@entry_id:152928) of organic matter with composition $C_x N_y P_z$ to $\text{CO}_2$ and $\text{NO}_3^-$ requires an amount of oxygen given by the [redox balance](@entry_id:166906) $\Delta O_2 / \Delta C = 1 + 2(y/x)$, where $y/x$ is the molar N:C ratio. In a fixed stoichiometry model, this oxygen demand is constant. In a variable stoichiometry model, organic matter produced under [nitrogen limitation](@entry_id:1128726) will have a lower N:C ratio and consequently a lower oxygen demand upon [remineralization](@entry_id:194757). 

#### Functional Forms for Biological Processes

The rates of biological processes like growth, grazing, and mortality are represented by mathematical functions that depend on environmental variables and the concentrations of the ecosystem components themselves.

A key function is the dependence of phytoplankton growth on a [limiting nutrient](@entry_id:148834). This is most often described by the **Monod equation**, an empirical saturating function:
$$ \mu(N) = \mu_{\max} \frac{N}{K_N + N} $$
where $\mu(N)$ is the [specific growth rate](@entry_id:170509), $\mu_{\max}$ is the maximum possible growth rate, $N$ is the ambient nutrient concentration, and $K_N$ is the **[half-saturation constant](@entry_id:1125887)**—the nutrient concentration at which the growth rate is half of its maximum.

This empirical form has a strong mechanistic basis in **Michaelis-Menten enzyme kinetics**. If we model [nutrient uptake](@entry_id:191018) as an enzyme-like process where a membrane transporter ($E$) binds an external nutrient ($N$) to form a complex ($EN$) which is then translocated, the steady-state uptake rate $V(N)$ can be derived as:
$$ V(N) = \frac{V_{\max} N}{K_M + N} $$
where $V_{\max}$ is the maximum uptake rate (proportional to the total number of transporters) and $K_M = (k_{-1} + k_{cat})/k_1$ is the Michaelis-Menten constant, depending on the rate constants for binding ($k_1$), unbinding ($k_{-1}$), and [translocation](@entry_id:145848) ($k_{cat}$) . The empirical Monod [half-saturation constant](@entry_id:1125887) for growth, $K_N$, is equivalent to the mechanistic Michaelis-Menten constant for uptake, $K_M$, only under the simplifying assumption that growth rate is a direct, constant multiple of uptake rate—that is, uptake is the sole [rate-limiting step](@entry_id:150742) in a [complex series](@entry_id:191035) of metabolic processes. 

In the real ocean, growth is often limited by multiple factors simultaneously (e.g., light, nitrate, phosphate, iron). Models must combine these individual limitations. For essential, non-substitutable resources, where the underlying acquisition processes are assumed to be independent, a **multiplicative formulation** is often used :
$$ \mu = \mu_{\max} \cdot f_{\text{light}}(I) \cdot f_N(N) \cdot f_P(P) \cdot f_{Fe}(Fe) $$
where each $f_i$ is a dimensionless limitation term (typically a Monod function) ranging from 0 to 1. This formulation ensures that if any single resource is completely absent, growth ceases entirely.

#### Ecosystem Structure and Trophic Dynamics: The NPZD Model

To explore the interactions between different parts of the ecosystem, even simple "box models" with a few interacting compartments can be highly instructive. A classic example is the **Nutrient-Phytoplankton-Zooplankton-Detritus (NPZD) model**. This model tracks the flow of a limiting element (e.g., nitrogen) through four pools: dissolved inorganic nutrients ($N$), phytoplankton ($P$), zooplankton ($Z$), and dead organic matter or detritus ($D$). 

Steady-state analysis of such a model reveals fundamental modes of ecosystem control.
-   **Bottom-Up Control:** In a scenario with low nutrient supply or inefficient grazing, zooplankton may be absent ($Z^* = 0$, where the star denotes a steady state). In this regime, phytoplankton growth is limited by nutrient availability. The steady-state nutrient concentration $N^*$ is set at a constant level determined by phytoplankton mortality. Any increase in the external nutrient supply ($\sigma$) leads directly to a proportional increase in phytoplankton biomass ($P^*$).

-   **Top-Down Control:** When nutrient supply is sufficient to support a grazer population ($Z^* > 0$), a "[trophic cascade](@entry_id:144973)" emerges. The phytoplankton biomass $P^*$ is no longer controlled by nutrients but is instead held constant by the grazing pressure of zooplankton. The level of $P^*$ is determined by the parameters governing zooplankton metabolism and mortality. In this regime, an increase in the external nutrient supply bypasses the phytoplankton pool and instead flows up the [food chain](@entry_id:143545), leading to an increase in zooplankton ($Z^*$) and, through their [excretion](@entry_id:138819) and mortality, an increase in detritus ($D^*$). This demonstrates how [predator-prey dynamics](@entry_id:276441) can fundamentally alter the ecosystem's response to changes in resource availability. 

### Connecting Ecosystem Processes to Global Cycles

Marine ecosystems are not isolated; they are integral components of [global biogeochemical cycles](@entry_id:149408). Two key examples are the [biological carbon pump](@entry_id:140846) and the internal [nitrogen cycle](@entry_id:140589), which have profound implications for climate and ocean chemistry.

#### The Biological Carbon Pump

The **biological pump** is the suite of biological processes that transports carbon from the sunlit surface ocean to the deep sea, where it can be sequestered from the atmosphere for centuries or longer. It has two main components with surprisingly different effects on surface ocean chemistry .

1.  **The Soft-Tissue Pump:** This refers to the photosynthetic fixation of dissolved inorganic carbon (DIC) into particulate organic carbon (POC), which then sinks out of the euphotic zone. This process consumes DIC from the surface water. While nitrate uptake slightly increases [total alkalinity](@entry_id:1133258) (TA), the primary effect is a drawdown of DIC. A reduction in DIC at nearly constant TA causes a decrease in the partial pressure of surface $\text{CO}_2$ ($p\text{CO}_2$), enhancing the ocean's uptake of $\text{CO}_2$ from the atmosphere.

2.  **The Carbonate Pump:** This refers to the formation of [calcium carbonate](@entry_id:190858) ($\text{CaCO}_3$) shells by organisms like coccolithophores and [foraminifera](@entry_id:141700). This process forms particulate inorganic carbon (PIC), which also sinks. The chemical reaction is $\mathrm{Ca^{2+} + CO_3^{2-} \rightarrow CaCO_3(s)}$. For every mole of $\text{CaCO}_3$ formed, one mole of DIC is consumed. However, the removal of the carbonate ion ($\text{CO}_3^{2-}$) reduces [total alkalinity](@entry_id:1133258) by two equivalents. The strong reduction in TA has a larger effect on the carbonate system than the reduction in DIC. It shifts the carbonate equilibria, causing a net release of aqueous $\text{CO}_2$ and thus an *increase* in surface $p\text{CO}_2$. Counter-intuitively, the carbonate pump makes the surface ocean a stronger source of $\text{CO}_2$ to the atmosphere.

The net effect of the biological pump on atmospheric $\text{CO}_2$ depends on the balance between these two competing processes, often expressed as the "rain ratio" of exported PIC to POC.

#### Key Nitrogen Transformations and Their Chemical Signatures

The nitrogen cycle is intimately linked to the carbon cycle, as nitrogen is a key [limiting nutrient](@entry_id:148834) for photosynthesis. Microbial transformations of nitrogen not only control the availability of fixed nitrogen but also impact oceanic oxygen and alkalinity budgets.

-   **Nitrification:** The aerobic oxidation of ammonium ($\text{NH}_4^+$) to nitrate ($\text{NO}_3^-$) is a two-step process carried out by chemoautotrophic microbes. The overall reaction is $\text{NH}_4^+ + 2\text{O}_2 \rightarrow \text{NO}_3^- + \text{H}_2\text{O} + 2\text{H}^+$. This process is a major sink for oxygen in the ocean interior. Crucially, it produces 2 moles of protons for every mole of ammonium oxidized, making it a significant source of oceanic [acidity](@entry_id:137608) (a sink for alkalinity). Per mole of N transformed, the change vector $\Delta(\text{NH}_4^+, \text{NO}_3^-, \text{O}_2, \text{TA})$ is $(-1, +1, -2, -2)$. 

-   **Denitrification:** Under low-oxygen (suboxic) conditions, heterotrophic microbes can use nitrate as an electron acceptor to respire organic matter, reducing it to dinitrogen gas ($\text{N}_2$). This is a major pathway for the loss of fixed nitrogen from the ocean. The reaction consumes protons, and therefore increases alkalinity. Per mole of N atom processed, the change vector $\Delta(\text{NO}_3^-, \text{N}_2, \text{TA})$ is $(-1, +0.5, +1)$. 

-   **Anaerobic Ammonium Oxidation (Anammox):** In this autotrophic process, microbes anaerobically "burn" ammonium with nitrite ($\text{NO}_2^-$) to produce dinitrogen gas: $\text{NH}_4^+ + \text{NO}_2^- \rightarrow \text{N}_2 + 2\text{H}_2\text{O}$. This is another major loss pathway for fixed nitrogen. Notably, this reaction has no net effect on the proton balance, and therefore does not change alkalinity. Per mole of N atom processed, the change vector $\Delta(\text{NH}_4^+, \text{N}_2, \text{TA})$ is $(-0.5, +0.5, 0)$. 

The balance between these pathways in oxygen minimum zones shapes the ocean's nitrogen inventory and its capacity to buffer changes in acidity.

### Model Structure and Complexity

A central challenge in marine [ecosystem modeling](@entry_id:191400) is representing the immense biological diversity of plankton. There are two main paradigms for tackling this complexity, each with its own trade-offs regarding realism, computational cost, and the ability to be constrained by observations.

#### Plankton Functional Types (PFTs)

The most common approach is to classify plankton into a finite number of **Plankton Functional Types (PFTs)**. PFTs are groups of organisms that share a key ecological function, such as [nitrogen fixation](@entry_id:138960) ([diazotrophs](@entry_id:165206)), calcification (coccolithophores), or silica shell formation ([diatoms](@entry_id:144872)). The model then tracks the biomass of each of these $N$ discrete types as separate [state variables](@entry_id:138790). This approach reduces the complexity of the real ecosystem to a manageable, finite-dimensional system. 

#### Trait-Based Models

An alternative is the continuous **trait-based model**. Instead of pre-defining a few types, this approach represents the phytoplankton community as a continuous biomass distribution over a space of key physiological traits, such as cell size or maximum growth rate. The state of the system is not a vector of biomasses, but a function $n(\theta, t)$ that describes the biomass density at trait value $\theta$ and time $t$. This approach is formally infinite-dimensional. It offers greater flexibility, allowing the [community structure](@entry_id:153673) to emerge dynamically from the interplay of growth, mortality, and competition along the trait axis. In practice, these models are often reduced to a finite system by tracking the moments of the trait distribution. 

#### The Challenge of Parameter Identifiability

A key consideration in choosing model complexity is **[parameter identifiability](@entry_id:197485)**: can the model's parameters be uniquely determined from the available observational data? Complex models with many parameters may be under-constrained, meaning different combinations of parameter values can produce equally good fits to the data.

This challenge is acute in marine [ecosystem modeling](@entry_id:191400), where many observations (e.g., satellite-derived chlorophyll) are aggregated signals that do not resolve the contributions of individual plankton types.
-   In a discrete PFT model with $N$ types, if the only observation is total chlorophyll (the sum of all PFTs' chlorophyll), it becomes difficult or impossible to identify the individual growth rates or [mortality rates](@entry_id:904968) of the $N$ different types. Fundamentally, one cannot uniquely determine more parameters than there are independent measurements. 
-   The problem is even more profound in [trait-based models](@entry_id:1133293). If only the total integrated biomass is observed over time, there is a fundamental ambiguity. Many different combinations of the growth-[rate function](@entry_id:154177) $\mu(\theta)$ and the initial trait distribution $n(\theta,0)$ could produce the exact same time series of total biomass. The observation operator irretrievably destroys the information linking a specific trait to a [specific growth rate](@entry_id:170509). In practice, only low-order, aggregated properties of the trait distribution (like its mean and variance) can be robustly identified from such data. 

The development of modern ocean [biogeochemical models](@entry_id:1121600) therefore involves a continuous negotiation between the desire for ecological realism, which pushes for greater complexity, and the constraints of computational feasibility and [parameter identifiability](@entry_id:197485), which favor simpler, more robust representations.