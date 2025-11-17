## Introduction
Lipid-derived signaling molecules are no longer viewed as simple metabolic byproducts but as potent, locally-acting autacoids that orchestrate a vast array of physiological and pathological processes. Among the most studied are the [eicosanoids](@entry_id:167274) and [endocannabinoids](@entry_id:169270), two distinct families that share a common origin in the [polyunsaturated fatty acids](@entry_id:180977) of our cell membranes. Understanding how these molecules are synthesized, how they signal, and how their actions are terminated is fundamental to deciphering the complexities of inflammation, pain, synaptic communication, and homeostasis.

Despite their importance, the intricate control mechanisms governing these pathways—from [on-demand synthesis](@entry_id:190081) to precise receptor activation—present a complex puzzle. This article aims to assemble this puzzle, providing a graduate-level biochemical framework for understanding these critical [signaling networks](@entry_id:754820).

We will embark on this exploration in three stages. The first chapter, "Principles and Mechanisms," lays the biochemical foundation, detailing the enzymatic pathways for synthesis and degradation, the receptors that mediate their effects, and the core principles of their regulation. The second chapter, "Applications and Interdisciplinary Connections," broadens our view to see how these principles manifest in pharmacology, immunology, and neuroscience, explaining everything from the action of aspirin to the basis of [synaptic plasticity](@entry_id:137631). Finally, the "Hands-On Practices" chapter provides an opportunity to apply these concepts through quantitative problem-solving, solidifying your understanding of [enzyme kinetics](@entry_id:145769) and receptor interactions in this dynamic field.

## Principles and Mechanisms

This chapter delineates the core biochemical principles and mechanisms governing the synthesis, function, and [catabolism](@entry_id:141081) of [eicosanoids](@entry_id:167274) and [endocannabinoids](@entry_id:169270). We will proceed from the management of their shared lipid precursors within cellular membranes to the distinct enzymatic pathways that generate these potent signaling molecules, the receptors through which they mediate their effects, and the processes that terminate their signals.

### Precursor Sourcing and Management

The [biosynthesis](@entry_id:174272) of both [eicosanoids](@entry_id:167274) and [endocannabinoids](@entry_id:169270) begins with [polyunsaturated fatty acids](@entry_id:180977) (PUFAs) that are stored within the [phospholipid](@entry_id:165385) bilayers of cellular membranes. The identity, abundance, and regulated release of these precursors are critical [determinants](@entry_id:276593) of the signaling landscape.

#### The Polyunsaturated Fatty Acid Reservoir

The primary precursors for this diverse family of lipid mediators are long-chain PUFAs. The three most significant are:
- **Arachidonic Acid (AA)**, a 20-carbon omega-6 fatty acid ($20{:}4\,n\text{-}6$).
- **Eicosapentaenoic Acid (EPA)**, a 20-carbon omega-3 [fatty acid](@entry_id:153334) ($20{:}5\,n\text{-}3$).
- **Docosahexaenoic Acid (DHA)**, a 22-carbon omega-3 [fatty acid](@entry_id:153334) ($22{:}6\,n\text{-}3$).

The nomenclature of these molecules can be specified in two ways. The **omega ($n\text{-}\omega$) notation** counts from the methyl ($\omega$) end of the acyl chain, identifying the position of the first double bond. The **delta ($\Delta$) notation** counts from the carboxyl ($C_1$) end. For naturally occurring PUFAs, which are typically all-*cis* and have [methylene](@entry_id:200959)-interrupted double bonds (i.e., double bonds separated by a single $CH_2$ group, or 3 carbon atoms apart), one can convert between these systems. For example, for [arachidonic acid](@entry_id:162954) ($20{:}4\,n\text{-}6$), with $N=20$ carbons, the first double bond from the methyl end is between $C_{20-6}$ and $C_{20-6+1}$, which is $C_{14}$ and $C_{15}$. This corresponds to a $\Delta^{14}$ bond. The other three bonds are found at positions $14-3=11$, $11-3=8$, and $8-3=5$. Thus, [arachidonic acid](@entry_id:162954) is $\Delta^{5,8,11,14}$. [@problem_id:2573906]

A fundamental question is why cells go to the trouble of storing these PUFAs in an esterified form within membrane phospholipids rather than maintaining a ready pool of free [fatty acids](@entry_id:145414) in the cytosol. The answer lies in thermodynamics and [cytotoxicity](@entry_id:193725) [@problem_id:2573947]. PUFAs are [amphipathic molecules](@entry_id:143410), with a polar carboxylate head group and a long, nonpolar hydrocarbon tail. The transfer of such a nonpolar chain from the hydrophobic interior of a membrane bilayer to the aqueous environment of the cytosol is thermodynamically highly unfavorable, with a large positive standard Gibbs free energy of transfer ($\Delta G^\circ_{\mathrm{bilayer}\to \mathrm{water}}$). The equilibrium partition coefficient, which can be expressed as $K_{\mathrm{w/b}} = \exp(-\frac{\Delta G^\circ}{RT})$, is therefore exceptionally small (on the order of $10^{-9}$). This means that at equilibrium, the concentration of free PUFA monomers in the cytosol would be vanishingly low compared to that in membranes.

Furthermore, if a cell were to accumulate a high concentration of free PUFAs in its cytosol, the concentration could exceed the **[critical micelle concentration](@entry_id:139804) (CMC)**. Above the CMC, these [amphipathic molecules](@entry_id:143410) self-assemble into [micelles](@entry_id:163245), which act as detergents, solubilizing and disrupting the integrity of cellular membranes, leading to cell lysis. By esterifying the PUFA's [carboxyl group](@entry_id:196503) to a glycerol backbone, the cell neutralizes its [amphipathic](@entry_id:173547) character and safely sequesters the hydrophobic acyl chain within the bilayer. This creates a vast, stable reservoir that can be tapped on-demand through regulated enzymatic hydrolysis. In extracellular fluids like blood plasma, this same challenge is overcome by high-affinity binding to [carrier proteins](@entry_id:140486) such as **human serum albumin (HSA)**, which sequesters the vast majority of non-esterified [fatty acids](@entry_id:145414), keeping the free monomer concentration orders of magnitude below the CMC. [@problem_id:2573947]

#### Regulated Release by Phospholipase A2 Enzymes

The release of PUFAs from membrane [phospholipids](@entry_id:141501) is the [rate-limiting step](@entry_id:150742) in the generation of most [eicosanoids](@entry_id:167274). This is primarily accomplished by the action of **[phospholipase](@entry_id:175333) A2 (PLA2)** enzymes, which hydrolyze the ester bond at the stereospecific numbering position 2 ($sn\text{-}2$) of [glycerophospholipids](@entry_id:163114)—the position where PUFAs like [arachidonic acid](@entry_id:162954) are predominantly located. The PLA2 superfamily is diverse, with several key families contributing to PUFA release in distinct ways [@problem_id:2573911].

- **Cytosolic PLA2$\alpha$ (cPLA2$\alpha$)**: This is the principal enzyme responsible for rapid, stimulus-coupled release of [arachidonic acid](@entry_id:162954). It is a cytosolic enzyme that contains a **C2 domain**, which acts as a $Ca^{2+}$ sensor. Upon cellular stimulation that elicits a rise in intracellular free calcium concentration ($[\mathrm{Ca}^{2+}]_i$) into the micromolar range, cPLA2$\alpha$ translocates from the cytosol to the nuclear envelope and endoplasmic reticulum (ER) membranes. Its activity is also enhanced by phosphorylation by **mitogen-activated [protein kinases](@entry_id:171134) (MAPKs)**. cPLA2$\alpha$ exhibits a marked preference for hydrolyzing phospholipids containing [arachidonic acid](@entry_id:162954) at the $sn\text{-}2$ position, particularly **phosphatidylcholine (PC)**.

- **Calcium-Independent PLA2 (iPLA2)**: As its name implies, this enzyme family does not require $Ca^{2+}$ for activity and is not involved in rapid, signal-induced PUFA release. Instead, iPLA2 enzymes are thought to play a "housekeeping" role in basal membrane homeostasis and remodeling. This includes their participation in the **Lands cycle**, which we will discuss next.

- **Secreted PLA2 (sPLA2)**: These are a family of relatively small, secreted enzymes that function extracellularly. They require high (millimolar) levels of $Ca^{2+}$ (as found in the extracellular environment) for catalysis. While not the initiators of the [intracellular signaling](@entry_id:170800) cascade, sPLA2s can act on the outer leaflet of the plasma membrane to amplify the release of [arachidonic acid](@entry_id:162954) and other PUFAs, often being localized to the cell surface by binding to [heparan sulfate](@entry_id:164971) [proteoglycans](@entry_id:140275).

The distinct localization, regulation, and substrate preferences of these PLA2 families allow for precise spatial and temporal control over which PUFAs are released, where, and when. [@problem_id:2573911]

#### The Lands Cycle and Steady-State Membrane Composition

The composition of fatty acids at the $sn\text{-}2$ position is not static but is dynamically maintained by a process of deacylation and reacylation known as the **Lands cycle**. In this cycle, a [fatty acid](@entry_id:153334) is removed from the $sn\text{-}2$ position by a PLA2 (such as iPLA2 in its housekeeping role), generating a lysophospholipid. This lysophospholipid is then reacylated by a **lysophospholipid acyltransferase (LPLAT)** using an acyl-Coenzyme A (acyl-CoA) substrate.

At steady state, the rate of incorporation of each PUFA species into the membrane must equal its rate of removal. If we consider a simplified model where the deacylation rate by PLA2 is independent of the [fatty acid](@entry_id:153334) identity, the determining factor for the steady-state abundance of a given PUFA in the membrane becomes the reacylation step. This is a competitive process where different acyl-CoA species compete for the LPLAT enzyme. The rate of incorporation for a specific PUFA, say PUFA$_i$, will be proportional to the product of its acyl-CoA concentration, $[\text{PUFA}_i\text{-CoA}]$, and the [catalytic efficiency](@entry_id:146951) of the LPLAT for that substrate, $\alpha_i$ (where $\alpha_i = k_{\text{cat}}/K_M$).

Therefore, the mole fraction ($x_i$) of a given PUFA in the membrane's $sn\text{-}2$ position at steady state is directly proportional to the product $\alpha_i [\text{PUFA}_i\text{-CoA}]$. Consequently, the rate at which that PUFA is released by a non-specific PLA2 during signaling will also be proportional to this product. This principle demonstrates that the availability of a PUFA for signaling is not solely dependent on its cellular concentration, but is a kinetically controlled outcome of the competing reacylation fluxes within the Lands cycle. For instance, even if EPA-CoA is less efficiently used by LPLAT than AA-CoA (lower $\alpha$), a sufficiently higher concentration of EPA-CoA could lead to EPA being more abundant in the membrane and thus released at a higher rate upon stimulation. [@problem_id:2573906]

### The Eicosanoid Branch: Pro-Inflammatory and Pro-Resolving Mediators

Once released from the membrane, [arachidonic acid](@entry_id:162954) and other PUFAs can be metabolized by several enzymatic pathways, leading to the formation of [eicosanoids](@entry_id:167274) and other related autacoids.

#### The Cyclooxygenase (COX) Pathway and Prostanoids

The cyclooxygenase pathway is responsible for the synthesis of **prostanoids**, which include [prostaglandins](@entry_id:201770), prostacyclins, and thromboxanes. The key enzymes are **cyclooxygenase-1 (COX-1)** and **cyclooxygenase-2 (COX-2)**. These enzymes are bifunctional, possessing two distinct catalytic activities residing in separate [active sites](@entry_id:152165). [@problem_id:2573881]

1.  **Cyclooxygenase (COX) activity**: The reaction is initiated by the oxidation of the enzyme's heme [cofactor](@entry_id:200224) by a hydroperoxide, which generates a tyrosyl radical within the active site. This radical abstracts a hydrogen atom from C-13 of [arachidonic acid](@entry_id:162954), creating a carbon-centered arachidonyl radical. This radical then undergoes a series of cyclizations and reactions with two molecules of molecular oxygen ($O_2$) to form **prostaglandin G2 (PGG2)**. PGG2 is an unstable intermediate that contains both a cyclic endoperoxide bridge and a hydroperoxide group at C-15.

2.  **Peroxidase (POX) activity**: In the second step, the peroxidase active site of the same enzyme reduces the hydroperoxide group of PGG2 to a hydroxyl group, yielding the more stable endoperoxide **prostaglandin H2 (PGH2)**. PGH2 is the central precursor from which all other prostanoids are synthesized by specific downstream synthases.

While COX-1 and COX-2 perform the same biochemical reaction, their regulation and physiological roles are profoundly different.
-   **COX-1** is considered a **housekeeping gene**. It is constitutively expressed in most tissues and is responsible for producing prostanoids that regulate basal physiological processes, such as gastric mucosal protection and platelet aggregation. Its gene promoter is typical of [housekeeping genes](@entry_id:197045): TATA-less, GC-rich, and driven by transcription factors like Sp1.
-   **COX-2** is an **inducible, immediate-early gene**. Its expression is normally low but is rapidly and dramatically upregulated by inflammatory stimuli, cytokines, and growth factors. It is the primary source of prostanoids during inflammation and cancer. Its gene promoter contains response elements for inflammatory transcription factors like **NF-$\kappa$B**, and its mRNA contains AU-rich elements in the 3' untranslated region, which target it for rapid degradation, ensuring a transient response. [@problem_id:2573881]

#### The Lipoxygenase (LOX) Pathway and Leukotrienes

The lipoxygenase pathways involve a family of enzymes that insert molecular oxygen into PUFAs to form hydroperoxy [fatty acids](@entry_id:145414). The most studied of these pathways in the context of inflammation is the **5-lipoxygenase (5-LOX)** pathway, which produces **[leukotrienes](@entry_id:190987)**. [@problem_id:2573925]

The activation of this pathway in leukocytes is a highly orchestrated process. Similar to cPLA2$\alpha$, 5-LOX is a cytosolic enzyme that, upon a stimulus-induced rise in intracellular $Ca^{2+}$, translocates to the nuclear envelope. There, it forms a complex with an [integral membrane protein](@entry_id:176600) called the **5-lipoxygenase-activating protein (FLAP)**. FLAP is not an enzyme itself but is thought to function by binding [arachidonic acid](@entry_id:162954) and "presenting" it to 5-LOX for efficient catalysis.

Like COX enzymes, 5-LOX is also bifunctional:
1.  First, its dioxygenase activity catalyzes the regio- and stereospecific insertion of $O_2$ at C-5 of [arachidonic acid](@entry_id:162954), yielding **5(S)-hydroperoxyeicosatetraenoic acid (5(S)-HPETE)**.
2.  Second, its dehydratase activity converts 5(S)-HPETE into an unstable epoxide intermediate, **leukotriene A4 (LTA4)**.

LTA4 is a critical branch point. It can be metabolized via two distinct routes:
-   In the cytosol, the enzyme **LTA4 hydrolase** converts LTA4 into the dihydroxy fatty acid **leukotriene B4 (LTB4)**, a potent chemoattractant for [neutrophils](@entry_id:173698).
-   On the nuclear and ER membranes, the integral membrane enzyme **LTC4 synthase** conjugates LTA4 with the tripeptide glutathione (GSH) to form **leukotriene C4 (LTC4)**. LTC4 is then exported from the cell and sequentially processed by extracellular peptidases into **LTD4** and **LTE4**. These three molecules (LTC4, LTD4, LTE4) are collectively known as the **cysteinyl [leukotrienes](@entry_id:190987)** and are powerful mediators of bronchoconstriction and vascular permeability. [@problem_id:2573925]

#### Specialized Pro-Resolving Mediators (SPMs)

In contrast to the classical pro-inflammatory [eicosanoids](@entry_id:167274) derived from [arachidonic acid](@entry_id:162954), the omega-3 PUFAs EPA and DHA are precursors to a class of molecules with potent anti-inflammatory and **pro-resolving** properties. These **[specialized pro-resolving mediators](@entry_id:169750) (SPMs)**, which include **[resolvins](@entry_id:188202)**, **protectins**, and **maresins**, are actively synthesized during the resolution phase of inflammation and signal to halt [neutrophil](@entry_id:182534) infiltration and stimulate the clearance of apoptotic cells and debris ([efferocytosis](@entry_id:191608)). [@problem_id:2573904]

Their biosynthesis involves lipoxygenase enzymes and, in a special case, aspirin-acetylated COX-2. A key feature is their precise stereochemistry, which is essential for their biological activity.
-   **E-series Resolvins (from EPA)**: Biosynthesis can be initiated by COX-2 that has been acetylated by aspirin. This "reprogrammed" enzyme acts as a lipoxygenase, converting EPA to an $18R$-hydroxy precursor. This intermediate is then transferred to a nearby cell (e.g., a [neutrophil](@entry_id:182534)) and acted upon by 5-LOX to produce **resolvin E1**, with a characteristic $(5S,12R,18R)$ trihydroxy configuration.
-   **Protectins (from DHA)**: The native pathway involves a 15-lipoxygenase generating a $17S$-hydroperoxy intermediate from DHA. This is converted to an epoxide and then hydrolyzed to form **protectin D1** ($(10R,17S)$-dihydroxy-DHA). Aspirin-acetylated COX-2 can initiate a parallel pathway by producing a $17R$ intermediate, leading to an epimeric, aspirin-triggered protectin.
-   **Maresins (from DHA)**: These are typically synthesized in [macrophages](@entry_id:172082) via the action of 12-lipoxygenase, which converts DHA to a $14S$-hydroperoxy intermediate, ultimately yielding **maresin 1** ($(7R,14S)$-dihydroxy-DHA).

The crucial distinction lies in both their precursors (n-3 vs. n-6 PUFAs) and their function: SPMs actively orchestrate the termination of inflammation, whereas classical [eicosanoids](@entry_id:167274) often initiate and amplify it. [@problem_id:2573904] [@problem_id:2573904]

### The Endocannabinoid Branch: On-Demand Neuromodulators

Endocannabinoids are [lipid signaling](@entry_id:172144) molecules that act upon cannabinoid receptors, the same receptors targeted by the psychoactive components of *Cannabis*. Unlike [classical neurotransmitters](@entry_id:168730), they are not stored in vesicles but are synthesized "on-demand" from membrane [phospholipid](@entry_id:165385) precursors in response to specific stimuli.

#### Biosynthesis of Anandamide and 2-Arachidonoylglycerol

The two major [endocannabinoids](@entry_id:169270) are [anandamide](@entry_id:189997) (N-arachidonoylethanolamine, AEA) and [2-arachidonoylglycerol](@entry_id:182696) (2-AG). Their synthetic pathways are distinct and are activated by different upstream signals. [@problem_id:2573876]

-   **2-Arachidonoylglycerol (2-AG) Synthesis**: This is the canonical pathway for activity-dependent endocannabinoid production in the brain. It is initiated by the activation of G-protein coupled receptors (GPCRs) coupled to the **$G_{q/11}$** family of G-proteins (e.g., group I [metabotropic glutamate receptors](@entry_id:172407)). $G_{q/11}$ activates **[phospholipase](@entry_id:175333) C$\beta$ (PLC$\beta$)**, which hydrolyzes the membrane lipid phosphatidylinositol 4,5-bisphosphate (PIP2) into two second messengers: inositol 1,4,5-trisphosphate (IP3) and **[diacylglycerol](@entry_id:169338) (DAG)**. While IP3 mobilizes $Ca^{2+}$ from intracellular stores, the DAG, which must contain an arachidonyl group at the $sn\text{-}2$ position, is hydrolyzed by **[diacylglycerol](@entry_id:169338) lipase (DAGL)** to produce 2-AG.

-   **Anandamide (AEA) Synthesis**: AEA synthesis is more complex, with multiple proposed routes. All routes begin with the formation of **N-acyl-phosphatidylethanolamine (NAPE)** from phosphatidylethanolamine, a reaction catalyzed by a $Ca^{2+}$-dependent N-acyltransferase. Thus, a rise in intracellular $Ca^{2+}$ is the primary stimulus. From NAPE, AEA can be generated by:
    1.  The **canonical route**: A single-step hydrolysis of NAPE by a specific [phospholipase](@entry_id:175333) D, **NAPE-PLD**.
    2.  **Alternative routes**: Multi-step pathways involving other [hydrolases](@entry_id:178373). For example, enzymes like **ABHD4** or a PLA2 can process NAPE to glycerophospho-N-acylethanolamine (GP-NAE), which is then hydrolyzed by the [phosphodiesterase](@entry_id:163729) **GDE1** to yield AEA. These alternative pathways may be important when NAPE-PLD activity is low or under specific physiological conditions.

#### Signal Termination by Hydrolytic Enzymes

The signaling actions of AEA and 2-AG are terminated by enzymatic hydrolysis, which breaks them down into [arachidonic acid](@entry_id:162954) and either ethanolamine or glycerol. This [catabolism](@entry_id:141081) is carried out by specific enzymes with distinct substrate preferences and subcellular localizations, allowing for differential control over the two endocannabinoid systems. [@problem_id:2573941]

-   **Fatty Acid Amide Hydrolase (FAAH)**: This is the primary enzyme for AEA degradation. FAAH is an [integral membrane protein](@entry_id:176600) of the endoplasmic reticulum with its active site facing the cytosol. It is a serine hydrolase, but it belongs to the "amidase signature" family, utilizing a unique **Ser-Ser-Lys [catalytic triad](@entry_id:177957)** and having an alkaline pH optimum. Its localization allows it to terminate AEA signaling near its sites of synthesis and action.

-   **Monoacylglycerol Lipase (MAGL)**: This is the principal enzyme for 2-AG degradation, responsible for hydrolyzing over 85% of 2-AG in the brain. MAGL is primarily a cytosolic enzyme that associates with membranes and is highly expressed in presynaptic nerve terminals. It is a classical serine hydrolase with a canonical **Ser-His-Asp [catalytic triad](@entry_id:177957)** and a neutral pH optimum. Its presynaptic localization is ideal for rapidly terminating the retrograde signal carried by 2-AG after it has acted on presynaptic cannabinoid receptors.

-   **N-Acylethanolamine Acid Amidase (NAAA)**: This enzyme also hydrolyzes AEA and other N-acylethanolamines, but its properties are distinct from FAAH. NAAA is a lysosomal enzyme with an acidic pH optimum (around 4.5). It is not a serine hydrolase but an **N-terminal nucleophile (Ntn) hydrolase**, using a catalytically active N-terminal [cysteine](@entry_id:186378) residue. Its location within lysosomes means it is not involved in rapid [synaptic signal termination](@entry_id:176965) but rather in the degradation of N-acylethanolamines that have been internalized and trafficked to the endolysosomal pathway.

This [division of labor](@entry_id:190326)—FAAH for AEA postsynaptically, MAGL for 2-AG presynaptically, and NAAA in [lysosomes](@entry_id:168205)—provides exquisite spatial and temporal control over endocannabinoid signaling. [@problem_id:2573941]

### Receptors and Downstream Signaling

Both [eicosanoids](@entry_id:167274) and [endocannabinoids](@entry_id:169270) exert their biological effects by binding to and activating specific G-protein coupled receptors on the surface of target cells.

#### Eicosanoid Receptors

The vast family of [eicosanoids](@entry_id:167274) signals through an equally diverse array of GPCRs. These receptors couple to different classes of heterotrimeric G-proteins, leading to distinct downstream second messenger cascades. The primary G-protein families and their canonical effects are:
- **G$_s$**: Stimulates [adenylyl cyclase](@entry_id:146140) (AC), increasing cyclic AMP (cAMP).
- **G$_i/o$**: Inhibits [adenylyl cyclase](@entry_id:146140), decreasing cAMP. The released $\beta\gamma$ subunits can also modulate other effectors.
- **G$_{q/11}$**: Activates [phospholipase](@entry_id:175333) C$\beta$ (PLC$\beta$), leading to IP3-mediated $Ca^{2+}$ mobilization and DAG-mediated [protein kinase](@entry_id:146851) C (PKC) activation.
- **G$_{12/13}$**: Activates the RhoA-ROCK pathway, involved in cytoskeletal regulation and [smooth muscle contraction](@entry_id:155142).

By systematically applying selective agonists and pharmacological inhibitors (e.g., pertussis toxin for G$_{i/o}$, PLC inhibitors like U73122 for G$_{q/11}$), one can deduce the coupling of each receptor [@problem_id:2573918].
-   **Prostanoid Receptors**: The prostaglandin $E_2$ ($PGE_2$) receptors provide a classic example of diversity: **EP1** couples to $G_{q/11}$ (increasing $Ca^{2+}$); **EP2** and **EP4** couple to G$_s$ (increasing cAMP); and **EP3** couples to G$_i/o$ (decreasing cAMP). Other prostanoid receptors show similar specificity, such as the prostacyclin receptor **IP** (G$_s$), the prostaglandin F2$\alpha$ receptor **FP** ($G_{q/11}$), and the thromboxane receptor **TP**, which often co-couples to both $G_{q/11}$ and $G_{12/13}$ to cause potent [smooth muscle contraction](@entry_id:155142).
-   **Leukotriene Receptors**: The LTB4 receptors, **BLT1** and **BLT2**, and the cysteinyl leukotriene receptors, **$CysLT_1$** and **$CysLT_2$**, primarily mediate inflammatory responses. BLT1 is a classic G$_{i/o}$-coupled receptor whose activation leads to both cAMP inhibition and $Ca^{2+}$ mobilization (via $\beta\gamma$ subunits). $CysLT_1$ is a $G_{q/11}$-coupled receptor, mediating bronchoconstriction through $Ca^{2+}$ mobilization.

#### Cannabinoid Receptors

The effects of [endocannabinoids](@entry_id:169270) are mediated primarily by two GPCRs, **cannabinoid receptor type 1 ($CB_1$)** and **type 2 ($CB_2$)**. [@problem_id:2573897] Both receptors couple canonically to the **G$_{i/o}$** family of G-proteins. This coupling leads to a characteristic suite of inhibitory downstream effects:
1.  **Inhibition of Adenylyl Cyclase**: The activated G$\alpha_i$ subunit inhibits AC, leading to a decrease in intracellular cAMP levels.
2.  **Modulation of Ion Channels**: The released G$\beta\gamma$ dimer directly interacts with ion channels. It **activates G-protein-activated inwardly rectifying potassium (GIRK) channels**, causing $K^+$ efflux and [membrane hyperpolarization](@entry_id:195828). It also **inhibits presynaptic voltage-gated calcium channels (VGCCs)** of the N- and P/Q-types, reducing $Ca^{2+}$ influx.

This combination of effects is powerfully inhibitory. In the central nervous system, $CB_1$ receptors are one of the most abundant GPCRs and are densely concentrated on **presynaptic terminals**. When a postsynaptic neuron is strongly depolarized, it synthesizes and releases [endocannabinoids](@entry_id:169270) (like 2-AG), which travel "retrogradely" across the synapse to activate presynaptic $CB_1$ receptors. This activation inhibits further [neurotransmitter release](@entry_id:137903) from the presynaptic terminal, a process known as **depolarization-induced suppression of inhibition/excitation (DSI/DSE)**. This is a key mechanism of [synaptic plasticity](@entry_id:137631).

In contrast to $CB_1$, **$CB_2$ receptors** are expressed at very low levels in the healthy brain but are found predominantly on cells of the **immune system**, including [macrophages](@entry_id:172082), [microglia](@entry_id:148681), B-cells, and T-cells, where they play a role in modulating inflammation and immune responses. [@problem_id:2573897]