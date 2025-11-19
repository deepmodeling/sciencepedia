## Introduction
De novo [fatty acid synthesis](@entry_id:171770) (DNFS) is a cornerstone of central metabolism, representing the cell's primary mechanism for converting excess carbohydrate-derived energy into storable, energy-dense lipids. This fundamental anabolic process is not merely a route for fat storage; it is critical for generating the building blocks required for [membrane biogenesis](@entry_id:186881), the production of signaling molecules, and maintaining [cellular homeostasis](@entry_id:149313). While seemingly a straightforward process of carbon-chain elongation, DNFS is governed by a sophisticated and tightly regulated network of enzymes and signals that ensure its activity is precisely matched to the cell's nutritional and energetic state. Understanding how the cell orchestrates this synthesis, partitions it from opposing catabolic pathways, and adapts its function across different physiological contexts is a central challenge in biochemistry.

This article provides a graduate-level exploration of this vital pathway, bridging molecular mechanisms with physiological significance. Across three comprehensive chapters, you will gain a deep, integrated understanding of DNFS.
First, under **"Principles and Mechanisms,"** we will dissect the core biochemical machinery, exploring the spatial and regulatory separation from [fatty acid oxidation](@entry_id:153280), the elegant shuttles that supply cytosolic precursors, and the intricate catalytic and allosteric functions of the key enzymes, Acetyl-CoA Carboxylase and Fatty Acid Synthase.
Next, in **"Applications and Interdisciplinary Connections,"** we will zoom out to examine the pathway's broader impact. We will investigate its integration with organismal nutrition, its specialized roles in different tissues, its pathological dysregulation in prevalent diseases like metabolic syndrome and cancer, and its emergence as a key therapeutic target.
Finally, the **"Hands-On Practices"** section will challenge you to apply this knowledge through quantitative problems, solidifying your grasp of the pathway's [stoichiometry](@entry_id:140916), [enzymology](@entry_id:181455), and integration with [central carbon metabolism](@entry_id:188582).

## Principles and Mechanisms

### Anabolic and Catabolic Partitioning: The Identity of De Novo Fatty Acid Synthesis

In [cellular metabolism](@entry_id:144671), the synthesis and degradation of key biomolecules are managed through distinct, often spatially and regulatorily segregated, pathways. This fundamental principle of **[metabolic partitioning](@entry_id:163316)** is elegantly exemplified by the metabolism of [fatty acids](@entry_id:145414). To understand **de novo [fatty acid synthesis](@entry_id:171770)** (DNFS), the process of building [fatty acids](@entry_id:145414) from non-lipid precursors, it is essential to first distinguish it from the related pathways of [fatty acid elongation](@entry_id:178004) and [fatty acid oxidation](@entry_id:153280). These pathways, while all manipulating acyl chain length, serve different physiological purposes and are executed by different enzymatic machinery in distinct subcellular compartments [@problem_id:2554219].

**De novo [fatty acid synthesis](@entry_id:171770)** is a cytosolic process that is primarily active in the **fed state**, when there is an excess of carbohydrates and energy. Under these conditions, high insulin levels promote the conversion of surplus glucose-derived acetyl-coenzyme A (acetyl-CoA) into fat for long-term storage. The entire process, culminating in the synthesis of the 16-carbon saturated fatty acid **palmitate**, is catalyzed by a large multifunctional enzyme complex called **[fatty acid synthase](@entry_id:177530)** (FASN). A key feature of DNFS is its use of a specific carrier molecule, the **[acyl carrier protein](@entry_id:162837)** (ACP), to which the growing [fatty acid](@entry_id:153334) chain is covalently tethered. The two-carbon donor for chain elongation is not acetyl-CoA itself, but an "activated" form, **malonyl-CoA**. Furthermore, the reductive steps required to build the saturated hydrocarbon chain exclusively utilize **nicotinamide adenine dinucleotide phosphate** ($NADPH$) as the electron donor.

In contrast, **[fatty acid oxidation](@entry_id:153280)**, or **$\beta$-oxidation**, is a catabolic process that breaks down [fatty acids](@entry_id:145414) to produce energy. It is dominant during the **fasted state** or periods of high energy demand, such as exercise. This pathway occurs primarily within the **mitochondrial matrix**. Long-chain fatty acids must first be activated to acyl-CoA esters in the cytosol and then transported into the mitochondria via the [carnitine shuttle](@entry_id:176194). Within the matrix, a series of enzymes sequentially cleaves two-carbon units from the acyl-CoA, generating acetyl-CoA, which can enter the tricarboxylic acid (TCA) cycle, as well as the reduced cofactors **nicotinamide adenine dinucleotide** ($NADH$) and **flavin adenine dinucleotide** ($FADH_2$), which fuel ATP synthesis via oxidative phosphorylation.

Finally, **[fatty acid elongation](@entry_id:178004)** systems are responsible for extending [fatty acid](@entry_id:153334) chains beyond the C16 palmitate produced by DNFS. These elongation reactions occur predominantly on the cytosolic face of the **endoplasmic reticulum (ER)** membrane, with a separate system also present in mitochondria. These systems use an existing acyl-CoA (e.g., palmitoyl-CoA) as a substrate, extend it using malonyl-CoA as the two-carbon donor (in the ER), and also utilize $NADPH$ as the reductant. Unlike DNFS, the intermediates are CoA [esters](@entry_id:182671), not ACP-bound thioesters. The resulting [very-long-chain fatty acids](@entry_id:145068) (VLCFAs) are not primarily for energy storage but are destined for specific structural and signaling roles, such as the synthesis of [sphingolipids](@entry_id:171301) for [myelin](@entry_id:153229) sheaths or the [modulation](@entry_id:260640) of [membrane fluidity](@entry_id:140767).

This partitioning—synthesis in the cytosol using $NADPH$ in the fed state, versus oxidation in the mitochondria generating $NADH$/$FADH_2$ in the fasted state—is a cornerstone of metabolic control, preventing a futile cycle where newly synthesized fatty acids are immediately degraded.

### The Supply of Cytosolic Precursors: Acetyl-CoA and NADPH

De novo [fatty acid synthesis](@entry_id:171770) is an energetically demanding anabolic process that requires a substantial and continuous supply of two key cytosolic molecules: acetyl-CoA as the fundamental carbon building block, and $NADPH$ as the reductant. The cell employs elegant and integrated pathways to meet these demands.

#### The Citrate Shuttle: Exporting Carbon from Mitochondria

The primary source of acetyl-CoA for [fatty acid synthesis](@entry_id:171770) is the mitochondrial pool, generated from [pyruvate oxidation](@entry_id:139126) (via the [pyruvate dehydrogenase complex](@entry_id:150942)) and [amino acid catabolism](@entry_id:174904). However, the inner mitochondrial membrane is impermeable to acetyl-CoA. To overcome this barrier, the cell utilizes the **[citrate shuttle](@entry_id:151222)** to effectively transport acetyl-CoA carbon units into the cytosol [@problem_id:2554301].

The process begins in the mitochondrial matrix. When cellular energy levels are high (high ATP/ADP ratio), the TCA cycle slows down at the level of the enzyme isocitrate [dehydrogenase](@entry_id:185854). This causes an accumulation of the upstream intermediate, **citrate**. This excess citrate is then transported out of the mitochondria into the cytosol by the **tricarboxylate carrier**, an [antiporter](@entry_id:138442) in the inner mitochondrial membrane that typically exchanges citrate for malate.

Once in the cytosol, citrate is acted upon by the enzyme **ATP-citrate lyase**. In an ATP-dependent reaction, this enzyme cleaves citrate into two products: acetyl-CoA and oxaloacetate.

$$ \text{Citrate} + \text{ATP} + \text{CoA} \rightarrow \text{Acetyl-CoA} + \text{Oxaloacetate} + \text{ADP} + P_i $$

This reaction regenerates the acetyl-CoA in the cytosol, where it is now available for [fatty acid synthesis](@entry_id:171770). The other product, [oxaloacetate](@entry_id:171653), must be returned to the mitochondrial matrix to sustain the shuttle. It is first reduced to malate by cytosolic malate dehydrogenase. This malate can either be directly transported back into the mitochondrion in exchange for more citrate or be utilized in a pathway that contributes to the second critical requirement for [lipogenesis](@entry_id:178687): $NADPH$.

#### Sourcing the Reductant: The Generation of NADPH

The synthesis of one molecule of palmitate from acetyl-CoA requires 14 molecules of $NADPH$. The cell has several pathways to generate this crucial reductant in the cytosol, with their relative contributions shifting depending on the metabolic state and substrate availability [@problem_id:2554286].

1.  **The Pentose Phosphate Pathway (PPP):** The oxidative branch of the PPP is a major source of cytosolic $NADPH$. It begins with glucose-6-phosphate, an intermediate of glycolysis. Two successive oxidation steps, catalyzed by **[glucose-6-phosphate dehydrogenase](@entry_id:171482)** ($G6PD$) and **6-phosphogluconate dehydrogenase**, each produce one molecule of $NADPH$. In a high-glucose, insulin-stimulated state (Condition H), glycolytic flux is high, providing abundant substrate for the PPP and making it a dominant source of $NADPH$ for [lipogenesis](@entry_id:178687).

2.  **Cytosolic Malic Enzyme (ME1):** This enzyme provides a direct link between the [citrate shuttle](@entry_id:151222) and $NADPH$ production. The malate produced from oxaloacetate by ATP-citrate lyase can be oxidatively decarboxylated by cytosolic **$NADP^+$-dependent malic enzyme** ($ME1$) to produce [pyruvate](@entry_id:146431), $CO_2$, and $NADPH$.

    $$ \text{Malate} + \text{NADP}^+ \rightarrow \text{Pyruvate} + CO_2 + \text{NADPH} $$

    The [pyruvate](@entry_id:146431) can then re-enter the mitochondrion to be converted back to oxaloacetate or acetyl-CoA. This pathway is particularly significant because for every molecule of acetyl-CoA brought into the cytosol via the [citrate shuttle](@entry_id:151222), one molecule of $NADPH$ can be generated. In a high-glucose state, this pathway is a major contributor alongside the PPP.

3.  **Cytosolic Isocitrate Dehydrogenase (IDH1):** The cytosol contains an $NADP^+$-dependent isoform of isocitrate [dehydrogenase](@entry_id:185854) ($IDH1$) that catalyzes the same reaction as its mitochondrial counterpart: the [oxidative decarboxylation](@entry_id:142442) of isocitrate to $\alpha$-ketoglutarate, producing $NADPH$. Cytosolic isocitrate can be formed from the citrate exported from mitochondria. While a potential source, its contribution to the high demands of [lipogenesis](@entry_id:178687) is generally considered minor compared to the PPP and malic enzyme.

The flexibility of this system is highlighted when glucose is scarce but other substrates like glutamine are abundant (Condition L). In this scenario, PPP flux is greatly diminished. However, glutamine can enter the TCA cycle as $\alpha$-ketoglutarate and be converted to malate, which is then exported to the cytosol. This glutamine-derived malate can fuel NADPH production via malic enzyme, allowing [lipogenesis](@entry_id:178687) to proceed even in the absence of high glucose, a strategy often exploited by proliferating cancer cells.

### The Committed Step: Regulation and Mechanism of Acetyl-CoA Carboxylase

The first committed step of de novo [fatty acid synthesis](@entry_id:171770) is the [carboxylation](@entry_id:169430) of acetyl-CoA to form malonyl-CoA. This irreversible reaction is catalyzed by **acetyl-CoA carboxylase (ACC)** and represents the primary site of regulation for the entire pathway.

#### The Biotin-Dependent Carboxylation Mechanism

ACC is a member of the family of **[biotin-dependent carboxylases](@entry_id:173305)**. The overall reaction consumes one molecule of ATP to add a carboxyl group from bicarbonate ($\text{HCO}_3^-$) to acetyl-CoA.

$$ \text{Acetyl-CoA} + \text{HCO}_3^- + \text{ATP} \rightarrow \text{Malonyl-CoA} + \text{ADP} + P_i $$

This seemingly simple transformation is achieved through a sophisticated two-step mechanism that occurs at two distinct [active sites](@entry_id:152165) within the enzyme [@problem_id:2554313].

1.  **First Half-Reaction (at the Biotin Carboxylase, BC, site):** Bicarbonate is activated by ATP to form a transient, high-energy intermediate, **carboxyphosphate**. This unstable compound decomposes to $CO_2$ and inorganic phosphate. The $CO_2$ is immediately captured by the biotin cofactor, which is covalently attached to a mobile domain of the enzyme called the **biotin carboxyl carrier protein (BCCP)**. The [biotin](@entry_id:166736) acts as a nucleophile, forming a covalent **carboxybiotin** intermediate. All ATP consumption occurs in this step.

2.  **Second Half-Reaction (at the Carboxyltransferase, CT, site):** The BCCP domain acts as a long, flexible "swinging arm," physically moving the carboxybiotin intermediate from the BC active site to the spatially separate CT active site. Here, the activated carboxyl group is transferred from biotin to the methyl carbon of acetyl-CoA, which has been deprotonated to form a reactive [enolate nucleophile](@entry_id:188643). This transfer yields the final product, malonyl-CoA, and regenerates the biotin cofactor for the next catalytic cycle.

#### The Thermodynamic Imperative for Malonyl-CoA

A key question is why [fatty acid synthesis](@entry_id:171770) evolved to use the ATP-dependent formation of malonyl-CoA as the two-carbon donor, rather than simply condensing acetyl-CoA units directly. The answer lies in thermodynamics and reaction mechanism [@problem_id:2554292].

A standard Claisen [condensation](@entry_id:148670) between two [thioester](@entry_id:199403) molecules (e.g., acyl-KS and acetyl-ACP) is a reversible reaction with a Gibbs free energy change close to zero, meaning it does not strongly favor product formation. By "activating" acetyl-CoA to malonyl-CoA, the cell couples the energetically unfavorable [carbon-carbon bond formation](@entry_id:198613) to a highly favorable decarboxylation reaction.

The [condensation](@entry_id:148670) step catalyzed by [fatty acid synthase](@entry_id:177530) involves the attack of a [carbanion](@entry_id:194580) derived from malonyl-ACP onto an acyl thioester. This reaction is accompanied by the release of $CO_2$. The overall free energy change can be considered the sum of the condensation and the decarboxylation: $\Delta G^{\circ\prime}_{\text{overall}} = \Delta G^{\circ\prime}_{\text{condensation}} + \Delta G^{\circ\prime}_{\text{decarboxylation}}$. Since decarboxylation is highly exergonic ($\Delta G^{\circ\prime}_{\text{decarboxylation}} \ll 0$), it provides a powerful thermodynamic driving force that renders the entire elongation step effectively irreversible. Furthermore, the loss of $CO_2$ as a gaseous product pulls the reaction forward according to Le Chatelier's principle. In essence, the ATP energy invested by ACC to carboxylate acetyl-CoA is "cashed in" at the condensation step to ensure the unidirectional synthesis of the [fatty acid](@entry_id:153334) chain.

Mechanistically, the carboxyl group also facilitates the reaction by making the $\alpha$-protons of malonyl-ACP more acidic (lower $pK_a$) than those of acetyl-ACP. This makes it easier for the enzyme to generate the required carbanion nucleophile for the condensation reaction.

#### Allosteric Regulation of ACC Activity and Polymerization

As the gatekeeper of [fatty acid synthesis](@entry_id:171770), ACC is subject to exquisite [allosteric regulation](@entry_id:138477) that integrates signals of cellular energy status and carbon availability. This regulation is remarkably coupled to the enzyme's [quaternary structure](@entry_id:137176) [@problem_id:2554229]. ACC exists in a dynamic equilibrium between an inactive, protomeric or dimeric form and a catalytically active, filamentous polymer.

**Citrate**, the product of the first step of the TCA cycle, serves as a powerful **feed-forward activator**. When citrate levels are high in the cytosol, it signals an abundance of carbon building blocks and a high energy state. Citrate binds to an allosteric site on ACC, stabilizing a conformation that promotes its polymerization into long, active filaments. Structural studies reveal that the polyanionic citrate molecule acts as an electrostatic "glue," bridging positively charged patches at the interfaces between ACC protomers. This binding lowers the free energy of association, reduces the critical concentration required for [polymerization](@entry_id:160290), and enhances the [cooperativity](@entry_id:147884) of assembly, leading to a dramatic increase in [enzyme activity](@entry_id:143847).

Conversely, **palmitoyl-CoA**, the end product of the pathway, acts as a **feedback inhibitor**. When levels of long-chain fatty acyl-CoAs rise, palmitoyl-CoA binds to a separate [allosteric site](@entry_id:139917) on ACC. This site is an amphipathic groove that accommodates the long, hydrophobic acyl chain. Binding of palmitoyl-CoA stabilizes a compact, inactive conformation of the enzyme that is incompatible with filament formation. This causes the active filaments to depolymerize back into inactive protomers, shutting down the pathway. The effectiveness of this inhibition is dependent on the length of the acyl chain, with longer chains like palmitoyl-CoA (C16) and stearoyl-CoA (C18) being much more potent inhibitors than shorter chains due to more extensive hydrophobic interactions within the binding pocket.

### The Elongation Machinery: Structure and Function of Fatty Acid Synthase (FASN)

Once malonyl-CoA is produced, the iterative process of chain elongation is carried out by the remarkable molecular machine, [fatty acid synthase](@entry_id:177530) (FASN). In mammals, this is a Type I FASN, a single massive polypeptide chain containing seven distinct catalytic domains plus the [acyl carrier protein](@entry_id:162837) (ACP).

#### The Iterative Four-Step Elongation Cycle

Starting with an acetyl group (the "primer") loaded onto the enzyme, FASN extends the chain by two carbons in each cycle through a recurring sequence of four reactions [@problem_id:2554189]. Let's consider one cycle extending an acyl chain of length $n$ (Acyl$_n$) already attached to the enzyme.

1.  **Condensation (catalyzed by $\beta$-Ketoacyl Synthase, KS):** First, a malonyl group is loaded from malonyl-CoA onto the ACP domain. Then, the KS domain catalyzes a decarboxylative Claisen [condensation](@entry_id:148670). The Acyl$_n$ group is reacted with the malonyl-ACP, releasing $CO_2$ and forming a $\beta$-ketoacyl$_{n+2}$-ACP intermediate. This is the chain-lengthening step.

2.  **Reduction (catalyzed by $\beta$-Ketoacyl Reductase, KR):** The $\beta$-keto group of the intermediate is reduced to a [hydroxyl group](@entry_id:198662) using $NADPH$ as the electron donor, yielding a $\beta$-hydroxyacyl$_{n+2}$-ACP.

3.  **Dehydration (catalyzed by Dehydratase, DH):** A molecule of water is eliminated from the $\beta$-hydroxyacyl intermediate to create a carbon-carbon double bond, forming a *trans*-$\Delta^2$-enoyl$_{n+2}$-ACP.

4.  **Reduction (catalyzed by Enoyl Reductase, ER):** The double bond is reduced (saturated) using a second molecule of $NADPH$, producing a fully saturated acyl$_{n+2}$-ACP.

The elongated acyl$_{n+2}$ chain is now ready for the next cycle of elongation. This four-step process is repeated six more times, adding two carbons per cycle, until a 16-carbon palmitoyl-ACP is formed. At this point, the final catalytic domain, **Thioesterase (TE)**, hydrolyzes the [thioester bond](@entry_id:173810), releasing the final product, free palmitate.

#### Substrate Channeling and the Acyl Carrier Protein (ACP)

The efficiency of the FASN complex is largely due to the function of the **Acyl Carrier Protein (ACP)** and its [prosthetic group](@entry_id:174921), a long, flexible **4'-phosphopantetheine** arm [@problem_id:2554298]. This arm, derived from coenzyme A, terminates in a thiol (-SH) group that forms a [thioester bond](@entry_id:173810) with the growing acyl chain.

The ACP acts as a swinging arm that covalently tethers the [reaction intermediates](@entry_id:192527) and shuttles them between the spatially distinct active sites of the FASN domains. This process, known as **[substrate channeling](@entry_id:142007)**, confers several critical advantages:

*   **Enhanced Efficiency:** By converting a series of [bimolecular reactions](@entry_id:165027) into effectively intramolecular transfers, the local concentration of the substrate at the next active site is dramatically increased. This overcomes diffusion limits and greatly enhances the overall catalytic rate.
*   **Sequestration of Intermediates:** The intermediates of [fatty acid synthesis](@entry_id:171770) are kept bound to the enzyme complex, preventing their diffusion away into the cytosol or their participation in competing side reactions.
*   **Protection from Hydrolysis:** The thioester intermediates are chemically labile and would be susceptible to hydrolysis if released into the aqueous environment of the cytosol. Channeling protects these intermediates, preventing waste of energy and material.
*   **Enforced Order:** The sequential nature of the cycle is enforced by specific docking interactions between the ACP domain and each catalytic partner domain. These interactions correctly orient the tethered substrate for the specific chemistry of that active site, ensuring that reduction only occurs after condensation, and so on. This "spatial gating" confers vectoriality to the process [@problem_id:2554298].

#### The Dimeric Architecture of Mammalian FASN

The structural organization of mammalian FASN is key to its function. The enzyme operates as a large **homodimer**, where the two identical polypeptide chains are arranged in an antiparallel, "head-to-tail" fashion. This dimerization is not merely for stability; it is an absolute requirement for catalysis [@problem_id:2554334].

The arrangement creates two independent reaction chambers. Crucially, each reaction chamber is a hybrid, formed from domains contributed by *both* protomers. The N-terminal "condensing module" (containing the KS and MAT domains) of one polypeptide is juxtaposed with the central "reductive module" (DH, ER, KR) and C-terminal "termination module" (TE) of the other polypeptide.

This inter-protomer collaboration is essential for [substrate channeling](@entry_id:142007). For instance, after the KS domain on protomer A catalyzes condensation, the ACP domain (also part of protomer A) must swing its cargo—the $\beta$-ketoacyl intermediate—across the dimer interface to reach the KR, DH, and ER active sites, which are located on protomer B. Without [dimerization](@entry_id:271116), this physical handoff is impossible. A monomeric FASN, even though it possesses all seven catalytic domains, is catalytically dead because its ACP cannot access the reductive domains on the same [polypeptide chain](@entry_id:144902) due to structural constraints. This has been confirmed experimentally: mutants that disrupt the dimer interface are monomeric and show virtually no [palmitate synthesis](@entry_id:167744), despite having intact catalytic domains and a properly modified ACP. Dimerization, therefore, creates the essential three-dimensional architecture required for the ACP swinging arm to complete its journey through the [catalytic cycle](@entry_id:155825).

### Integrated Regulation: Coupling Synthesis and Oxidation

The cell employs multiple layers of regulation to ensure that [fatty acid synthesis](@entry_id:171770) is tightly controlled and coordinated with the cell's overall metabolic state. A critical aspect of this control is the prevention of the [futile cycle](@entry_id:165033) between synthesis and oxidation. This is primarily achieved through the dual role of malonyl-CoA [@problem_id:2554275].

As we have seen, malonyl-CoA is the committed precursor for [fatty acid synthesis](@entry_id:171770). In addition to this role, it acts as a powerful [allosteric inhibitor](@entry_id:166584) of **Carnitine Palmitoyltransferase 1 (CPT1)**. CPT1 is the enzyme on the outer mitochondrial membrane that catalyzes the first committed step of long-chain [fatty acid oxidation](@entry_id:153280): the conversion of acyl-CoA to acylcarnitine for transport into the mitochondrion.

When [fatty acid synthesis](@entry_id:171770) is active in the fed state, cytosolic malonyl-CoA levels rise. This malonyl-CoA binds to CPT1 and inhibits its activity, effectively shutting down the entry of fatty acids into the mitochondria for oxidation. This ensures that newly synthesized [fatty acids](@entry_id:145414) are not immediately degraded but are instead directed toward storage (as [triacylglycerols](@entry_id:155359)) or incorporation into membranes.

This regulatory mechanism exhibits important tissue-specific differences. The liver primarily expresses the **CPT1A** isoform, while skeletal and [cardiac muscle](@entry_id:150153) express the **CPT1B** isoform. Experimental data show that the muscle isoform, CPT1B, is approximately 10-fold more sensitive to inhibition by malonyl-CoA than the hepatic isoform, CPT1A. This means that even small increases in malonyl-CoA in muscle can strongly suppress [fatty acid oxidation](@entry_id:153280), reserving [fatty acids](@entry_id:145414) for other purposes.

This entire regulatory axis is responsive to the energy status of the cell. During fasting or exercise, the cellular energy sensor, **AMP-activated protein kinase (AMPK)**, becomes active. AMPK phosphorylates and inhibits ACC, leading to a drop in malonyl-CoA levels. This drop relieves the inhibition on CPT1, thereby "opening the gate" to the mitochondria and allowing [fatty acid oxidation](@entry_id:153280) to proceed at a high rate to generate the needed ATP. The high sensitivity of muscle CPT1B ensures that this switch is particularly rapid and pronounced in [muscle tissue](@entry_id:145481) during exercise.