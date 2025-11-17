## Introduction
The synthesis of [fatty acids](@entry_id:145414) and [phospholipids](@entry_id:141501) represents one of the most fundamental anabolic processes in all of life. These pathways are responsible for constructing the cell membrane, the essential lipid bilayer that defines the cell's physical boundary, maintains cellular integrity, and mediates interactions with the outside world. Understanding how cells build this complex and dynamic structure from simple metabolic precursors is central to microbiology, [cell biology](@entry_id:143618), and medicine. This article addresses the key questions of how these lipid building blocks are made, how the process is energetically driven and regulated, and why this pathway is so critical for cellular function, adaptation, and survival.

This article is structured to guide you from foundational principles to broad applications. The first chapter, **"Principles and Mechanisms,"** deconstructs the core [biochemical pathway](@entry_id:184847) in bacteria, detailing the generation of building blocks, the iterative enzymatic cycle of chain elongation, and the final assembly of [phospholipids](@entry_id:141501). The second chapter, **"Applications and Interdisciplinary Connections,"** explores the profound impact of this pathway beyond basic [cell structure](@entry_id:266491), examining its role as a major antibiotic target, its importance in [microbial physiology](@entry_id:202702) and [biophysics](@entry_id:154938), and its connections to human disease and evolutionary theory. Finally, **"Hands-On Practices"** offers a series of problems designed to solidify your understanding and challenge you to apply these concepts to practical scenarios in metabolic analysis.

## Principles and Mechanisms

The biosynthesis of fatty acids and [phospholipids](@entry_id:141501) is a cornerstone of microbial life, essential for the construction of the cell membrane that defines the boundary between the cell and its environment. This chapter delves into the fundamental principles and intricate molecular mechanisms that govern this vital anabolic pathway in bacteria. We will deconstruct the process, starting from the generation of core building blocks from central metabolism, proceeding through the iterative elongation of the acyl chain, and culminating in the assembly of diverse [phospholipid](@entry_id:165385) species. We will also explore the bioenergetic strategies and regulatory circuits that ensure this process is both efficient and exquisitely responsive to the cell's metabolic state.

### The Building Blocks: Primers, Extenders, and the Glycerol Backbone

Before a complex lipid can be assembled, the cell must prepare the fundamental chemical units. This involves activating a simple two-carbon precursor to create a high-energy extender unit for chain elongation and synthesizing the glycerol backbone to which the fatty acid tails will be attached.

#### The Committed Step: Synthesis of Malonyl-CoA

The [biosynthesis](@entry_id:174272) of [fatty acids](@entry_id:145414) begins with the [carboxylation](@entry_id:169430) of **acetyl-CoA**, a central metabolite derived from glycolysis and other catabolic pathways. This reaction, which produces the three-carbon compound **malonyl-CoA**, is the committed step of the entire pathway. It is catalyzed by the enzyme **acetyl-CoA carboxylase** (ACC). In most bacteria, ACC is a multi-subunit complex typically composed of three key components: a **biotin carboxylase** (BC) subunit, a **biotin carboxyl carrier protein** (BCCP), and a **carboxyltransferase** (CT) subunit.

The overall reaction is a marvel of enzymatic coordination, proceeding in two distinct [half-reactions](@entry_id:266806) occurring at separate active sites [@problem_id:2492938]:

1.  **Carboxylation of Biotin:** At the BC active site, the process begins. The substrate for [carboxylation](@entry_id:169430) is not gaseous carbon dioxide ($CO_2$), but its hydrated and more abundant form at physiological pH, bicarbonate ($HCO_3^{-}$). The [carboxylation](@entry_id:169430) of biotin is an energetically unfavorable process, so it is coupled to the hydrolysis of **[adenosine triphosphate](@entry_id:144221)** (ATP). The BC subunit uses ATP to activate bicarbonate, forming a transient, high-energy **carboxyphosphate** intermediate. This activated [carboxyl group](@entry_id:196503) is then immediately transferred to the N1 position of the [biotin](@entry_id:166736) ring, which is covalently tethered to a specific lysine residue on the BCCP. This step produces **carboxybiotin-BCCP**, releasing **adenosine diphosphate** (ADP) and inorganic phosphate ($P_i$). The entire process requires the presence of a divalent cation, typically $Mg^{2+}$, to coordinate the phosphate groups of ATP.

    $Biotin-BCCP + HCO_{3}^{-} + ATP \xrightarrow{Mg^{2+}, BC} Carboxybiotin-BCCP + ADP + P_i$

2.  **Transfer to Acetyl-CoA:** The BCCP, bearing the biotinyl-lysine [prosthetic group](@entry_id:174921), acts as a flexible "swinging arm" that translocates the activated carboxyl group from the BC active site to the CT active site. Here, the carboxyl group is transferred from carboxybiotin to the $\alpha$-carbon of acetyl-CoA, yielding malonyl-CoA and regenerating the [biotin](@entry_id:166736)-BCCP for the next [catalytic cycle](@entry_id:155825).

    $Carboxybiotin-BCCP + Acetyl-CoA \xrightarrow{CT} Biotin-BCCP + Malonyl-CoA$

The overall [stoichiometry](@entry_id:140916), representing the net transformation, is thus:

$Acetyl-CoA + HCO_{3}^{-} + ATP \rightarrow Malonyl-CoA + ADP + P_i$

This reaction effectively "charges" an acetyl-CoA unit with a [carboxyl group](@entry_id:196503) at the cost of one ATP molecule, preparing it to serve as the two-carbon extender unit for all subsequent elongation steps.

#### The Bioenergetic Strategy of Chain Elongation

One might ask why the cell undergoes this seemingly circuitous process of adding a carboxyl group only to remove it later. The answer lies in the thermodynamics of [carbon-carbon bond formation](@entry_id:198613). A direct Claisen [condensation](@entry_id:148670) between two acetyl-CoA molecules is a reversible reaction with a Gibbs free energy change near zero, making it unsuitable for driving a robust, unidirectional biosynthetic pathway.

The cell employs a powerful two-part energetic strategy [@problem_id:2492960] [@problem_id:2492984]. First, as we have just seen, it invests energy from ATP hydrolysis to carboxylate acetyl-CoA, creating malonyl-CoA. This step is endergonic on its own and is made favorable only by coupling to ATP cleavage. The energy invested is effectively stored in the newly formed carboxyl group of the malonyl moiety.

Second, during the subsequent chain elongation step—the **decarboxylative Claisen condensation**—this stored energy is released. The decarboxylation of the malonyl group to release $CO_2$ is a highly exergonic process, driven by both favorable enthalpy and a significant increase in entropy as a gaseous molecule is produced. This large, negative free-energy change is coupled to the formation of the new carbon-carbon bond, pulling the entire [condensation](@entry_id:148670) reaction irreversibly in the forward direction. Thus, the initial investment of ATP is "cashed in" to ensure that each two-carbon extension of the fatty acid chain is thermodynamically favorable and essentially unidirectional under physiological conditions.

#### The Glycerol Backbone: Synthesis of sn-Glycerol-3-Phosphate

Parallel to the synthesis of the fatty acyl chains, the cell must produce the hydrophilic backbone onto which these chains will be mounted. In bacteria, the universal precursor for the glycerophospholipid backbone is **sn-[glycerol-3-phosphate](@entry_id:165400)** (G3P). The cell has distinct pathways to generate G3P, depending on the available carbon sources and metabolic state [@problem_id:2492915].

*   **From Glycolysis (Biosynthetic Route):** When growing on sugars like glucose, the glycolytic intermediate **dihydroxyacetone phosphate** (DHAP) serves as the precursor. The cytosolic enzyme **[glycerol-3-phosphate](@entry_id:165400) [dehydrogenase](@entry_id:185854) (GpsA)** catalyzes the reduction of the ketone group of DHAP to a [hydroxyl group](@entry_id:198662), forming G3P. This reductive step consumes a molecule of **NADH**. This is the primary biosynthetic route under glycolytic or fermentative conditions.

    $DHAP + NADH + H^{+} \xrightarrow{GpsA} sn\text{-Glycerol-3-Phosphate} + NAD^{+}$

*   **From Glycerol (Catabolic Entry/Biosynthetic Route):** When [glycerol](@entry_id:169018) is the sole carbon source, it must first be brought into central metabolism. This is achieved by the enzyme **glycerol kinase (GlpK)**, which phosphorylates glycerol at the expense of ATP to directly produce G3P. A portion of this G3P can be immediately channeled into [phospholipid synthesis](@entry_id:162906), while the rest can be oxidized for energy.

    $Glycerol + ATP \xrightarrow{GlpK} sn\text{-Glycerol-3-Phosphate} + ADP$

*   **Catabolic Oxidation of G3P:** There exists another [glycerol-3-phosphate](@entry_id:165400) dehydrogenase, **GlpD**. Unlike the cytosolic GpsA, GlpD is an [integral membrane protein](@entry_id:176600) whose active site faces the cytoplasm. It functions primarily in catabolism, oxidizing G3P back to DHAP. The electrons from this oxidation are not passed to $NAD^{+}$ but are instead donated directly to the quinone pool of the aerobic respiratory chain. This pathway is active during [aerobic respiration](@entry_id:152928) on [glycerol](@entry_id:169018), feeding both electrons into energy production and carbon into glycolysis/gluconeogenesis. Because its physiological role is oxidative, GlpD is not a source of G3P for [biosynthesis](@entry_id:174272).

The cell's choice of pathway is metabolically logical. During growth on glucose, G3P is synthesized reductively from a glycolytic intermediate via GpsA. During growth on [glycerol](@entry_id:169018), G3P is synthesized directly via GlpK, with the excess being oxidized by GlpD to fuel central metabolism.

### The Core Machinery: The Acyl Carrier Protein and the Elongation Cycle

With the building blocks prepared, we now turn to the central machinery of [fatty acid synthesis](@entry_id:171770). In bacteria, this is the Type II [fatty acid synthase](@entry_id:177530) (FAS II) system, a collection of discrete, soluble enzymes that catalyze the iterative steps of chain elongation. The key to this process is the **Acyl Carrier Protein (ACP)**, which acts as a mobile scaffold, shuttling the growing acyl chain between the different [active sites](@entry_id:152165).

#### The Acyl Carrier Protein: A Mobile Scaffold

ACP is a small, acidic protein that functions as the covalent carrier of all acyl intermediates during [fatty acid synthesis](@entry_id:171770). However, the protein as it is first translated, known as **apo-ACP**, is inactive. It lacks the crucial [prosthetic group](@entry_id:174921) required to carry an acyl chain. Activation requires the enzyme **holo-[acyl-carrier-protein] synthase (AcpS)**, a type of phosphopantetheinyl transferase [@problem_id:2492916].

AcpS catalyzes the transfer of the **4'-phosphopantetheine** (PPant) moiety from a molecule of coenzyme A (CoA) to the hydroxyl group of a conserved serine residue on apo-ACP. This reaction forms a phosphodiester bond, releasing **adenosine 3',5'-diphosphate** as a byproduct. The result is **holo-ACP**, a protein now equipped with a long, flexible arm that terminates in a reactive thiol (-SH) group. It is this terminal thiol that forms a high-energy **[thioester](@entry_id:199403)** bond with malonyl and the growing acyl chain, the chemical handle essential for all subsequent enzymatic steps. Without this modification, apo-ACP cannot be acylated and cannot participate in [fatty acid synthesis](@entry_id:171770).

#### The Substrate Channeling Mechanism

The FAS II system presents a fascinating challenge: how do discrete, non-associated enzymes achieve the efficiency of a multienzyme complex? The answer lies in the dynamic role of the PPant arm of holo-ACP, which enables a process known as **kinetic [substrate channeling](@entry_id:142007)** [@problem_id:2492942].

The PPant arm is approximately $18$ Å long and acts as a flexible tether. When ACP forms a transient, specific complex with one of the FAS enzymes, this tether confines the attached acyl intermediate to a small volume around the enzyme's active site. This dramatically increases the **effective concentration** of the substrate. For instance, confining the intermediate to a sphere of radius $15$ Å results in an effective [local concentration](@entry_id:193372) of approximately $0.1$ M. This is orders of magnitude higher than the typical micromolar concentration of a free metabolite in the cytosol. This immense [proximity effect](@entry_id:139932) ensures that the rate of the intramolecular or pseudo-[intramolecular reaction](@entry_id:204579) is vastly accelerated compared to a diffusion-limited [bimolecular reaction](@entry_id:142883) in bulk solution.

Furthermore, ACP's interaction with its partner enzymes is highly specific, driven by complementary electrostatic surfaces. Upon binding, the flexible PPant arm can deliver the acyl chain, which may be sequestered in a hydrophobic pocket of ACP, directly into the active site of the partner enzyme. This prevents the loss of hydrophobic intermediates to the bulk solvent or to non-specific reactions. In this way, ACP chaperones the growing chain from one active site to the next, achieving high efficiency and fidelity without the need for a permanent, static protein tunnel.

#### The Iterative Cycle of Fatty Acid Elongation

Each cycle of [fatty acid elongation](@entry_id:178004) extends the acyl chain by two carbons through a conserved four-step sequence of reactions: condensation, reduction, dehydration, and a second reduction [@problem_id:2492917]. Let us consider the initiation cycle, starting with an acetyl primer and the malonyl-ACP extender unit.

1.  **Condensation:** The cycle begins with a decarboxylative Claisen [condensation](@entry_id:148670) catalyzed by a **$\beta$-ketoacyl-ACP synthase** (KS). For initiation, this is often **FabH**, which specifically uses acetyl-CoA as the primer and malonyl-ACP as the extender. The reaction involves the decarboxylation of malonyl-ACP to generate a potent nucleophilic [carbanion](@entry_id:194580), which then attacks the acetyl-CoA [thioester](@entry_id:199403) carbonyl. The result is a four-carbon **$\beta$-ketoacyl-ACP** (acetoacetyl-ACP), with the release of $CO_2$ and CoA.
    $Acetyl-CoA + Malonyl-ACP \xrightarrow{FabH} Acetoacetyl-ACP + CO_2 + CoA$

2.  **First Reduction:** The keto group at the $\beta$-position of acetoacetyl-ACP is reduced to a hydroxyl group. This reaction is catalyzed by **$\beta$-ketoacyl-ACP reductase (FabG)** and requires the hydride donor **NADPH**. The product is a D-$\beta$-hydroxyacyl-ACP.
    $Acetoacetyl-ACP + NADPH + H^{+} \xrightarrow{FabG} D-\beta-hydroxybutyryl-ACP + NADP^{+}$

3.  **Dehydration:** A molecule of water is eliminated from the $\beta$-hydroxyacyl-ACP to create a double bond between the $\alpha$ and $\beta$ carbons. This is catalyzed by **$\beta$-hydroxyacyl-ACP dehydratase (FabZ or FabA)**. The product is a *trans*-2-enoyl-ACP.
    $D-\beta-hydroxybutyryl-ACP \xrightarrow{FabZ/A} trans\text{-2-butenoyl-ACP} + H_2O$

4.  **Second Reduction:** The double bond of the *trans*-2-enoyl-ACP is reduced (saturated) to complete the cycle. This reaction is catalyzed by **enoyl-ACP reductase (FabI)**. In many bacteria like *E. coli*, the specific [cofactor](@entry_id:200224) for this step is **NADH**, distinct from the NADPH used in the first reduction.
    $trans\text{-2-butenoyl-ACP} + NADH + H^{+} \xrightarrow{FabI} Butyryl-ACP + NAD^{+}$

The product, butyryl-ACP, is a saturated four-carbon acyl chain, now ready to serve as the primer for the next round of elongation. It will be condensed with another molecule of malonyl-ACP (this time by a different ketosynthase, such as FabB or FabF), and the four-step cycle repeats, adding two carbons with each turn until the desired chain length is reached.

### Generating Diversity: The Synthesis of Unsaturated Fatty Acids

Cell membranes require fluidity, which is conferred by the presence of [unsaturated fatty acids](@entry_id:173895) containing *cis* double bonds. Bacteria have evolved two primary strategies to introduce these bonds: an anaerobic pathway that operates during elongation and an aerobic pathway that modifies completed chains [@problem_id:2492913].

#### The Anaerobic Pathway: A Branch within Elongation

Many facultative and [obligate anaerobes](@entry_id:163957) utilize a clever mechanism that introduces a double bond as an integral part of the FAS II cycle. This pathway hinges on the bifunctional enzyme **FabA**. At a specific chain length, typically when the intermediate is a 10-carbon $\beta$-hydroxyacyl-ACP ($3$-hydroxydecanoyl-ACP), FabA catalyzes not only the standard dehydration to a *trans*-2-enoyl-ACP but also the isomerization of this intermediate to a *cis*-3-enoyl-ACP.

This *cis*-3-enoyl-ACP intermediate represents a critical [branch point](@entry_id:169747). It is a poor substrate for the standard enoyl-reductase (FabI), so it escapes the final reduction step. Instead, it is specifically recognized and elongated by a dedicated $\beta$-ketoacyl-ACP synthase, **FabB**. FabB catalyzes the condensation of the *cis*-3-enoyl-ACP with malonyl-ACP, extending the chain while preserving the *cis* double bond. Subsequent rounds of elongation, catalyzed by the standard FAS enzymes, add two-carbon units to the carboxyl end, effectively shifting the position of the pre-existing double bond further into the chain. For example, a $\Delta^3$ double bond introduced at the C10 stage becomes a $\Delta^9$ bond in a C16 [fatty acid](@entry_id:153334) (palmitoleic acid) or a $\Delta^{11}$ bond in a C18 [fatty acid](@entry_id:153334) (vaccenic acid). This entire process is oxygen-independent.

#### The Aerobic Pathway: Post-Synthetic Modification

In contrast, many aerobic bacteria use a completely different, post-synthetic strategy. After a full-length saturated [fatty acid](@entry_id:153334) (e.g., palmitoyl-ACP or stearoyl-ACP) has been synthesized, an **acyl-ACP desaturase** acts upon it. These enzymes are **mixed-function oxidases** that catalyze the direct dehydrogenation of the saturated acyl chain.

The reaction requires molecular oxygen ($O_2$) as the [terminal electron acceptor](@entry_id:151870). Electrons are extracted from the substrate and, along with electrons from a reduced donor like **NAD(P)H**, are used to reduce $O_2$ to two molecules of water. The electrons are shuttled from NAD(P)H to the desaturase via electron [carrier proteins](@entry_id:140486) such as ferredoxin. This mechanism directly introduces a *cis* double bond into a pre-formed saturated acyl chain. The key distinctions are clear: the aerobic pathway is post-synthetic, acts on saturated substrates, and is absolutely dependent on molecular oxygen, while the anaerobic pathway is co-synthetic, acts on an unsaturated intermediate, and is oxygen-independent.

### From Fatty Acids to Phospholipids: Assembly of the Membrane

Once fatty acids of the appropriate length and saturation are synthesized, they must be assembled into [phospholipids](@entry_id:141501). This process begins by attaching the fatty acid tails to the G3P backbone, followed by the addition of a polar head group.

#### The First Acylation: Attaching the Tail to the Backbone

The first committed step in [phospholipid synthesis](@entry_id:162906) is the acylation of the *sn*-1 position of G3P to form **lysophosphatidic acid** (LPA). Bacteria employ at least two distinct strategies for this crucial step [@problem_id:2492920].

*   **The PlsB Pathway:** In organisms like *E. coli*, the integral membrane enzyme **[glycerol-3-phosphate](@entry_id:165400) acyltransferase (PlsB)** catalyzes the direct transfer of a fatty [acyl group](@entry_id:204156) from acyl-ACP to G3P. The reaction is driven by the cleavage of the high-energy [thioester bond](@entry_id:173810) in acyl-ACP and does not require ATP. The active site of PlsB faces the cytosol to access its substrates, G3P and acyl-ACP, and it deposits the LPA product into the inner leaflet of the membrane. This pathway creates a tight [kinetic coupling](@entry_id:150387) between [fatty acid synthesis](@entry_id:171770) and [phospholipid synthesis](@entry_id:162906), as the protein-bound acyl-ACP product of one must be delivered directly to the other at the membrane surface.

*   **The PlsX-PlsY Pathway:** Many other bacteria utilize a two-step process. First, a soluble cytosolic enzyme, **PlsX**, catalyzes the conversion of acyl-ACP to a diffusible intermediate, **acyl-phosphate**. This transacylation reaction requires inorganic phosphate ($P_i$). The acyl-phosphate, a high-energy mixed anhydride, can then diffuse through the cytosol to the membrane. There, a different integral membrane [glycerol-3-phosphate](@entry_id:165400) acyltransferase, **PlsY**, transfers the [acyl group](@entry_id:204156) from acyl-phosphate to G3P to form LPA, releasing $P_i$. This pathway uncouples the timing and location of [fatty acid synthesis](@entry_id:171770) from [phospholipid](@entry_id:165385) assembly, allowing the cell to build a buffer pool of the acyl-phosphate intermediate.

The second acylation, at the *sn*-2 position of LPA, is catalyzed by an acyltransferase (PlsC in *E. coli*) to form **[phosphatidic acid](@entry_id:173659)** (PA), the central branch-point intermediate in [phospholipid synthesis](@entry_id:162906).

#### Activation and Head Group Attachment

In bacteria, the synthesis of the major phospholipids—phosphatidylethanolamine (PE), phosphatidylglycerol (PG), and [cardiolipin](@entry_id:181083) (CL)—proceeds via an activated [diacylglycerol](@entry_id:169338) intermediate, **CDP-[diacylglycerol](@entry_id:169338)** (CDP-DAG) [@problem_id:2492957].

1.  **Activation of Phosphatidic Acid:** The integral membrane enzyme **phosphatidate cytidylyltransferase (CdsA)** activates PA by reacting it with **cytidine triphosphate** (CTP). This reaction forms the high-energy intermediate CDP-DAG and releases inorganic pyrophosphate ($PP_i$). The subsequent hydrolysis of $PP_i$ by [pyrophosphatase](@entry_id:177161) provides a strong thermodynamic drive for this activation step.
    $PA + CTP \rightarrow CDP-DAG + PP_i$

2.  **Synthesis of PS and PE:** CDP-DAG is the substrate for **[phosphatidylserine](@entry_id:172518) synthase (PssA)**. The hydroxyl group of the amino acid L-serine attacks CDP-DAG, displacing **cytidine monophosphate** (CMP) to form **[phosphatidylserine](@entry_id:172518)** (PS). PS is then rapidly decarboxylated by **[phosphatidylserine](@entry_id:172518) decarboxylase (Psd)**, releasing $CO_2$ to produce the most abundant phospholipid in many Gram-negative bacteria, **phosphatidylethanolamine** (PE).
    $CDP-DAG + L-serine \xrightarrow{PssA} PS + CMP$
    $PS \xrightarrow{Psd} PE + CO_2$

3.  **Synthesis of PG and Cardiolipin:** In a parallel branch, CDP-DAG is the substrate for **phosphatidylglycerophosphate synthase (PgsA)**. This enzyme uses G3P as the nucleophile to attack CDP-DAG, displacing CMP and forming **phosphatidylglycerophosphate** (PGP). A specific [phosphatase](@entry_id:142277) (**Pgp**) then hydrolyzes the terminal phosphate from PGP, releasing $P_i$ to yield **phosphatidylglycerol** (PG). PG is a major anionic [phospholipid](@entry_id:165385). It can be further modified, for example, by condensing two molecules of PG to form [cardiolipin](@entry_id:181083).
    $CDP-DAG + sn\text{-Glycerol-3-Phosphate} \xrightarrow{PgsA} PGP + CMP$
    $PGP + H_2O \xrightarrow{Pgp} PG + P_i$

Through these pathways, the cell generates the primary [glycerophospholipids](@entry_id:163114) required for [membrane structure](@entry_id:183960) and function.

### Regulation of the Pathway: A Systems-Level View

To maintain membrane [homeostasis](@entry_id:142720) and conserve energy, bacteria must tightly regulate the flux through the fatty acid biosynthetic pathway. This is achieved primarily at the level of transcription, coupling the expression of *fab* (biosynthesis) and *fad* (degradation) genes to the availability of fatty acids in the environment [@problem_id:2492948]. In *E. coli*, this intricate control is orchestrated by two key transcription factors, FadR and FabR.

*   **FadR: The Global Sensor of Acyl-CoAs:** **FadR** is a masterful dual-function regulator that coordinates synthesis and degradation. In the absence of exogenous [fatty acids](@entry_id:145414), intracellular levels of long-chain acyl-CoAs are low. Under these conditions, FadR binds to DNA. It acts as a **repressor** for the *fad* genes, shutting down the degradation pathway. Simultaneously, it acts as a **transcriptional activator** for key *fab* genes, including *fabA* (required for unsaturation) and *fabB*, turning on the synthesis pathway. When the cell encounters external fatty acids (e.g., from the medium), they are imported and activated to form long-chain acyl-CoAs. These molecules act as the signaling ligand, binding to FadR and causing an allosteric change that abolishes its DNA-[binding affinity](@entry_id:261722). As a result, FadR dissociates from the DNA. Repression of the *fad* genes is lifted, allowing the cell to catabolize the external [fatty acids](@entry_id:145414). Concurrently, activation of the *fab* genes is lost, shutting down [de novo synthesis](@entry_id:150941). This elegant switch allows the cell to prioritize the use of available resources over energetically expensive synthesis.

*   **FabR: The Feedback Sensor for Unsaturation:** **FabR** provides a more specialized layer of feedback control, specifically for unsaturated [fatty acid synthesis](@entry_id:171770). It functions as a **repressor** for the *fabA* and *fabB* genes. Its repressive activity is modulated by the cellular pool of acyl-ACPs. Critically, its ligand and co-repressor is an unsaturated acyl-ACP. When the cell has produced a sufficient amount of [unsaturated fatty acids](@entry_id:173895), the resulting high levels of unsaturated acyl-ACPs bind to FabR, enhancing its DNA-binding and repressive function. This end-product feedback mechanism specifically throttles the production of more [unsaturated fatty acids](@entry_id:173895), thereby maintaining the proper ratio of saturated to unsaturated lipids in the membrane.

Together, these regulatory circuits allow bacteria to sense both external [fatty acid](@entry_id:153334) availability (via FadR and acyl-CoAs) and the internal status of the biosynthetic pathway (via FabR and unsaturated acyl-ACPs), ensuring a robust and efficient system for building and maintaining their cellular membranes.