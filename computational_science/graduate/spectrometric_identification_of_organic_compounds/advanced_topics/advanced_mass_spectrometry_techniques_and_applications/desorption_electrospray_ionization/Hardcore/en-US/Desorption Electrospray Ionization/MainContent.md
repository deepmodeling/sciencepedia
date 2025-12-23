## Introduction
Desorption Electrospray Ionization (DESI) has emerged as a transformative analytical technique in mass spectrometry, fundamentally changing how scientists can interact with and analyze the world around them. Its significance lies in its ability to perform direct chemical analysis on a vast array of surfaces in their native, ambient environment. This capability addresses a long-standing challenge in analytical science: the need for complex, time-consuming, and often destructive sample preparation protocols that can alter or destroy the very information being sought. By bringing the mass spectrometer directly to the sample, DESI opens a window into the molecular composition of objects with unprecedented ease and speed.

This article provides a comprehensive exploration of DESI, guiding you from its foundational concepts to its advanced applications. In the following chapters, you will gain a deep understanding of this powerful method. "Principles and Mechanisms" will dissect the core process, from the physics of droplet impact to the intricate chemistry of ion formation. "Applications and Interdisciplinary Connections" will showcase the versatility of DESI through its use in [chemical imaging](@entry_id:159551), [quantitative analysis](@entry_id:149547), and real-time reaction monitoring across fields like [forensic science](@entry_id:173637), clinical research, and pharmaceutical development. Finally, "Hands-On Practices" will challenge you to apply this knowledge through practical problems focused on compound identification, method optimization, and quantitative analysis.

## Principles and Mechanisms

Desorption Electrospray Ionization (DESI) is an [ambient ionization](@entry_id:190468) method that enables the direct analysis of analytes on surfaces with minimal to no sample preparation. This is achieved by directing a pneumatically assisted electrospray of charged solvent droplets onto the sample surface. The impact of these primary droplets desorbs analyte molecules into a thin [liquid film](@entry_id:260769), from which secondary, analyte-containing droplets are ejected and subsequently sampled by a mass spectrometer. The principles governing this complex sequence of events span fluid dynamics, surface science, electrostatics, and solution-phase chemistry. This chapter elucidates the fundamental mechanisms of DESI, from the physics of droplet impact to the chemistry of ion formation and the practical considerations for optimizing analysis.

### The Core Mechanism: From Primary Droplets to Analyte Ions

The overall process of DESI can be deconstructed into a sequence of distinct physical and chemical events. It begins with the generation of a high-velocity spray of charged **primary droplets**, typically composed of a solvent mixture such as methanol/water, from an emitter held at a high electrical potential. Unlike conventional **Electrospray Ionization (ESI)**, where the spray is directed straight into the [mass spectrometer](@entry_id:274296), in DESI this primary spray is aimed at a solid surface bearing the analyte.

The core distinction of DESI lies in its mechanism of **surface-assisted desorption**. The sequence of events is as follows :
1.  **Impact and Film Formation:** High-velocity primary droplets strike the surface, transferring momentum and kinetic energy. This impact causes the droplet to splash and spread, forming a transient, thin [liquid film](@entry_id:260769) over the sample.
2.  **Analyte Desorption and Dissolution:** The solvent in this transient film rapidly dissolves (extracts) analyte molecules from the surface.
3.  **Secondary Droplet Ejection:** The energy of the primary droplet impact is sufficient to cause the ejection of smaller, **secondary microdroplets** from the [liquid film](@entry_id:260769). These secondary droplets carry away the dissolved analyte along with a portion of the charge from the primary spray.
4.  **Ion Formation:** The charged secondary droplets travel through the ambient atmosphere toward the [mass spectrometer](@entry_id:274296) inlet. During this flight, solvent evaporation concentrates the charge, leading to the formation of gas-phase analyte ions through processes analogous to those in ESI.
5.  **Mass Analysis:** The resulting gas-phase ions are guided into the mass spectrometer for mass-to-charge ratio analysis.

This mechanism fundamentally differs from classic ESI, where ions are formed from a pre-made solution sprayed directly from a capillary, without any interaction with a sample surface. It also differs profoundly from matrix-assisted techniques like **Matrix-Assisted Laser Desorption/Ionization (MALDI)**, which involves laser-induced [sublimation](@entry_id:139006) from a solid, co-crystallized matrix and typically produces singly charged ions .

### The Physics of Droplet-Surface Interaction

The initial impact of the primary droplet on the surface is the critical step that initiates the entire DESI process. The outcome of this interaction—whether the droplet splashes or gently spreads—is determined by a competition between the droplet's inertia and [cohesive forces](@entry_id:274824) like surface tension and viscosity. This competition is quantified by two key dimensionless numbers: the **Reynolds number ($Re$)** and the **Weber number ($We$)**.

The Reynolds number represents the ratio of [inertial forces](@entry_id:169104) to [viscous forces](@entry_id:263294):
$$ \mathrm{Re} = \frac{\rho U L}{\mu} $$
where $\rho$ is the solvent density, $U$ is the droplet impact velocity, $L$ is a [characteristic length](@entry_id:265857) scale (such as the droplet radius or diameter), and $\mu$ is the dynamic viscosity. A high $Re$ indicates that inertia dominates viscosity, favoring [turbulent flow](@entry_id:151300) and splashing.

The Weber number represents the ratio of inertial forces to surface tension forces:
$$ \mathrm{We} = \frac{\rho U^2 L}{\gamma} $$
where $\gamma$ is the solvent surface tension. A high $We$ signifies that the droplet's kinetic energy upon impact overcomes the [cohesive forces](@entry_id:274824) of surface tension that seek to maintain its spherical shape. For a droplet impact, splashing is generally expected when $We$ is significantly greater than 1.

In a typical DESI experiment, conditions are set to ensure a splashing regime. For instance, consider a primary droplet of a water:methanol mixture with a diameter $d = 3\,\mu\mathrm{m}$, velocity $v = 100\,\mathrm{m/s}$, density $\rho = 1000\,\mathrm{kg/m^3}$, and surface tension $\gamma = 0.072\,\mathrm{N/m}$. The Weber number is approximately $417$ , a value far exceeding the threshold for splashing. A more formal criterion for the onset of splashing on a smooth surface combines both effects into a splashing parameter, $K_D = \mathrm{We}_D^{1/2} \mathrm{Re}_D^{1/4}$, where splashing is expected if $K_D$ exceeds a critical value (empirically found to be $\approx 57.7$). For typical DESI parameters ($U \approx 120\,\mathrm{m/s}$, $R \approx 15\,\mu\mathrm{m}$), $K_D$ can be on the order of $700$, confirming that the process is well into the splashing regime . This violent splashing is essential for the efficient generation of secondary droplets.

The properties of the spray solvent directly influence the dynamics of both primary droplet formation and surface impact :
- **Surface Tension ($\gamma$):** A higher surface tension resists the hydrodynamic breakup of the liquid jet from the emitter, leading to the formation of larger primary droplets. It also provides a stronger cohesive force opposing splashing, though this is typically overcome by the high impact velocity.
- **Viscosity ($\mu$):** A higher viscosity [damps](@entry_id:143944) instabilities in the liquid jet and during the impact process. This slows ligament thinning, reducing fine fragmentation and decreasing the number of secondary droplets produced in a splash.
- **Volatility ($p_{sat}$):** A higher solvent [vapor pressure](@entry_id:136384) (volatility) leads to more rapid evaporation of primary droplets during their flight to the surface. For a fixed flight time, this results in smaller droplets arriving at the surface, which can alter the impact dynamics.

### Desorption and Ionization Chemistry in the Droplets

Once the transient liquid film is formed, a series of chemical processes unfolds. The overall rate of ion production is often not limited by the raw energy of the impact, but rather by the kinetics of [mass transfer](@entry_id:151080) and chemical reactions within the brief lifetime of the film.

#### The Rate-Limiting Step: Analyte Extraction

An analysis of the energy budget and characteristic timescales reveals that the dissolution of the analyte into the liquid film is frequently the slowest, and therefore **rate-limiting, step** in DESI . The kinetic energy of an impacting droplet (on the order of $10^{-10}\,\mathrm{J}$) is typically several orders of magnitude greater than the chemical work required to desorb the analyte molecules underneath it (on the order of $10^{-13}\,\mathrm{J}$). Thus, the process is not energy-limited.

However, a comparison of timescales is more revealing. The impact itself is incredibly fast ($\sim 50\,\mathrm{ns}$). Solution-phase reactions like protonation are also extremely rapid ($\sim 10\,\mathrm{ns}$). In contrast, the time required for analyte molecules to diffuse from the surface through the thickness of the transient film (e.g., $0.5\,\mu\mathrm{m}$) can be on the order of hundreds of microseconds ($\sim 0.25\,\mathrm{ms}$). This diffusion time is often comparable to the [residence time](@entry_id:177781) of the liquid on the surface before it is ejected as secondary droplets ($\sim 1\,\mathrm{ms}$). Because mass transfer is not completed within the available time, it acts as a bottleneck, controlling the amount of analyte that is successfully captured and ultimately ionized.

#### Solution-Phase Ionization Pathways

The [ionization](@entry_id:136315) process in DESI is fundamentally a solution-phase phenomenon occurring within the secondary microdroplets, mechanistically analogous to ESI. The composition of the primary spray solvent can be tailored to favor specific [ionization](@entry_id:136315) pathways, providing a powerful means of experimental control. Two common pathways are [proton transfer](@entry_id:143444) and [charge transfer](@entry_id:150374) .

- **Proton Transfer:** This is the most common mechanism in positive-ion mode. By adding a small amount of acid (e.g., formic acid or [acetic acid](@entry_id:154041)) to the spray solvent, a reservoir of protons is created. Basic analytes ($B$) dissolved in the secondary droplets can be protonated to form $[B+\text{H}]^+$ ions. The feasibility of this reaction is governed by the relative basicities (or, conversely, the $pK_a$ values of the conjugate acids). For protonation to be favorable, the analyte must be more basic than the solvent species. For example, in a spray containing acid $HA$ and a proton scavenger base $S$, an analyte $B$ will only be significantly protonated if it can effectively compete for protons against the much more concentrated scavenger $S$.

- **Charge Transfer (Electron Transfer):** This pathway is useful for analytes that are not easily protonated but have a relatively low ionization potential. A radical cation dopant ($R^{+\bullet}$) with a high [redox potential](@entry_id:144596) is added to the spray solvent. If the standard redox potential of the dopant, $E^\circ(R^{+\bullet}/R)$, is higher than that of the analyte, $E^\circ(B^{+\bullet}/B)$, then electron transfer from the analyte to the [dopant](@entry_id:144417) radical cation is thermodynamically favorable, forming the analyte radical cation $B^{+\bullet}$:
$$ B + R^{+\bullet} \rightarrow B^{+\bullet} + R $$
The dominant pathway is determined by both thermodynamics (differences in $pK_a$ and $E^\circ$) and kinetics ([reaction rate constants](@entry_id:187887) and concentrations). In many cases, [proton transfer](@entry_id:143444) is kinetically faster than [charge transfer](@entry_id:150374) in the condensed phase.

### From Secondary Droplets to Gas-Phase Ions

The charged secondary droplets ejected from the surface contain the dissolved and now-ionized analyte. To be detected by the [mass spectrometer](@entry_id:274296), these ions must be liberated from the solvent into the gas phase. This process is governed by the principles of electrostatics and mass transfer established for ESI.

#### The Rayleigh Limit and Coulomb Fission

As a secondary droplet travels toward the [mass spectrometer](@entry_id:274296) inlet, the solvent evaporates. Since the charge $q$ on the droplet remains largely constant while its radius $R$ decreases, the density of charge on its surface increases. This increases the [electrostatic repulsion](@entry_id:162128) among the charges, which counteracts the cohesive force of surface tension. A droplet becomes unstable when this repulsion exceeds the surface tension. The maximum charge a droplet of radius $R$ and surface tension $\gamma$ can hold is known as the **Rayleigh limit** :
$$ q_{Rayleigh} = 8\pi\sqrt{\epsilon_0 \gamma R^3} $$
where $\epsilon_0$ is the [permittivity of free space](@entry_id:272823).

Once a droplet evaporates to the point where its charge exceeds this limit, it undergoes **Coulomb fission**, ejecting a stream of smaller, highly charged "offspring" droplets. This process repeats in a cascade, leading to the formation of extremely small, nanometer-scale droplets. The stability of droplets against fission is enhanced by solvents with higher surface tension, as $q_{Rayleigh} \propto \sqrt{\gamma}$ .

#### Final Ion Generation: IEM and CRM

From these final nanodroplets, gas-phase ions are produced by two primary mechanisms:

1.  **Ion Evaporation Model (IEM):** This model is dominant for smaller molecules and ions. The electric field at the surface of a highly charged nanodroplet becomes extraordinarily intense. For a droplet of radius $R=75\,\mathrm{nm}$ carrying a charge of $q=5.0 \times 10^{-16}\,\mathrm{C}$, the surface electric field, given by $E = q/(4\pi\epsilon_0 R^2)$, reaches approximately $8 \times 10^8\,\mathrm{V/m}$ . This immense field is strong enough to overcome the [solvation energy](@entry_id:178842) and directly eject individual, solvated ions from the droplet surface into the gas phase.

2.  **Charge Residue Model (CRM):** This model is more applicable to large macromolecules like proteins and peptides. In this scenario, the charged droplet continues to evaporate until all solvent is gone. The remaining non-volatile analyte molecule is left behind, retaining some or all of the droplet's residual charge.

The interplay of these mechanisms explains the characteristic charge states observed in DESI (and ESI) spectra . Small organic molecules, which typically have only one or a few basic sites, are generally observed as **singly charged ions**, such as $[M+\text{H}]^+$. Their formation is well-described by the IEM. In contrast, large [biomolecules](@entry_id:176390) like peptides contain multiple basic residues (e.g., lysine, arginine, histidine, and the N-terminus) and can therefore stably accommodate multiple protons. These analytes are observed as a distribution of **multiply charged ions**, such as $[M+n\text{H}]^{n+}$ where $n \ge 2$. Their formation is better described by the CRM.

This difference in charging behavior has a direct and important consequence on the appearance of the mass spectrum. A mass spectrometer measures the mass-to-charge ratio ($m/z$). The spacing between adjacent [isotopic peaks](@entry_id:750872) in a mass spectrum is given by $\Delta(m/z) \approx 1/z$.
- For singly charged small molecules ($z=1$), the [isotopic peaks](@entry_id:750872) are separated by $\approx 1.00\, m/z$ unit.
- For multiply charged peptides ($z \ge 2$), the [isotopic peaks](@entry_id:750872) are compressed, separated by $1/z$, i.e., $0.50\, m/z$ for $z=2$, $0.33\, m/z$ for $z=3$, and so on.

### Practical Considerations: Geometry and Fragmentation

The successful application of DESI requires careful optimization of the experimental setup and awareness of potential artifacts like in-source fragmentation.

#### Source Geometry and Ion Capture

The efficiency of ion capture is critically dependent on the geometric arrangement of the sprayer, the sample surface, and the mass spectrometer inlet. This geometry is typically defined by four parameters: the **sprayer-to-surface distance ($d_s$)**, the **surface-to-inlet distance ($d_i$)**, the **sprayer angle ($\theta_s$)**, and the **inlet angle ($\theta_i$)**, where angles are measured relative to the surface plane .

The impact of the primary spray creates a secondary plume of ion-bearing droplets that ejects from the surface at a characteristic angle, $\theta_p$. This plume has an angular distribution, often modeled as a Gaussian function. For maximum signal, the mass spectrometer inlet must be positioned to intercept the largest possible fraction of this ion plume. The **angular misalignment**, defined as the difference between the inlet axis angle and the plume's central axis angle, $\Delta = \theta_i - \theta_p$, is a critical parameter. The fraction of captured ions is determined by the overlap of the plume's [angular distribution](@entry_id:193827) with the inlet's [acceptance cone](@entry_id:199847). Even a modest misalignment of a few degrees can drastically reduce the captured ion signal, as the inlet only samples a small solid angle. For example, with a misalignment of $\Delta = -15^\circ$ and a plume with an angular standard deviation of $\sigma = 10^\circ$, the captured ion fraction can drop to less than $30\%$.

#### In-Source Fragmentation

A common phenomenon in DESI and other ESI-based techniques is **in-source fragmentation**, also known as in-source [collision-induced dissociation](@entry_id:167315) (CID) or declustering fragmentation. This is the unintentional fragmentation of analyte ions within the atmospheric pressure interface of the [mass spectrometer](@entry_id:274296), before they are mass-analyzed .

This fragmentation occurs in the region between the sampling orifice and the skimmer, where ions are accelerated by a potential difference (the **orifice potential** or **declustering potential**, $\Delta V$) while traversing a region of intermediate pressure. At these pressures (from atmospheric down to several Torr), the ion mean free path is very short (e.g., $\sim 70\,\mathrm{nm}$ at 1 atm). As ions are accelerated by the electric field, they undergo thousands of low-energy collisions with neutral gas molecules (e.g., nitrogen). In each collision, a fraction of the ion's kinetic energy is converted into internal (rovibrational) energy. Through this "collisional heating" process, an ion can accumulate enough internal energy to surpass the [activation barrier](@entry_id:746233) for its lowest-energy fragmentation pathways. This often results in the loss of small, stable neutral molecules like water or ammonia.

It is crucial to distinguish this from intentional **[tandem mass spectrometry](@entry_id:148596) (MS/MS)**. In MS/MS, precursor ions are mass-selected, isolated, and then deliberately fragmented in a low-pressure collision cell. Here, ions are accelerated to a specific kinetic energy and undergo a small number of higher-energy collisions. This controlled process often opens up different, higher-energy fragmentation channels than the gentle heating of in-source CID. The definitive diagnostic is to vary the source parameters: the intensity of an in-source fragment is highly dependent on the orifice potential ($\Delta V$) and capillary temperature, whereas a true MS/MS fragment is generated only after precursor isolation and depends on the [collision energy](@entry_id:183483) set for the collision cell.