## Introduction
The functional plasticity of macrophages and myeloid cells is a cornerstone of the immune system, enabling them to orchestrate responses ranging from aggressive host defense to delicate tissue repair. It is now clear that this adaptability is not merely a matter of genetic programming but is inextricably linked to profound shifts in cellular metabolism. The metabolic state of a myeloid cell dictates its functional capacity, creating an integrated system where metabolic pathways fuel immune activities and metabolites themselves act as signals to direct cellular fate. This article addresses the critical knowledge gap between cellular metabolism and immune function, providing a detailed framework for understanding this interplay.

This article will guide you through the fundamental concepts and cutting-edge applications of myeloid cell immunometabolism. In the **Principles and Mechanisms** chapter, we will dissect the core metabolic paradigms of M1 and M2 macrophage activation and explore the molecular machinery that drives these distinct states. Following this, the chapter on **Applications and Interdisciplinary Connections** will demonstrate how these principles apply to the pathogenesis of major human diseases, including cardiovascular disease, cancer, and infection, highlighting myeloid metabolism as a therapeutic target. Finally, the **Hands-On Practices** section provides exercises to reinforce these theoretical concepts, bridging the gap between knowledge and practical application.

## Principles and Mechanisms

The functional plasticity of macrophages and other myeloid cells is central to their roles in host defense, tissue homeostasis, and pathology. This plasticity is not merely a matter of altered gene expression but is deeply intertwined with profound shifts in cellular metabolism. The metabolic state of a macrophage is both a determinant and a consequence of its activation status, creating a tightly integrated system where metabolic pathways provide the necessary energy and biosynthetic precursors for specific immune functions, while key metabolites themselves act as signaling molecules that regulate gene expression and cellular programming. This chapter will dissect the core principles and mechanisms governing the immunometabolism of myeloid cells, focusing on the distinct metabolic paradigms of classically and alternatively activated macrophages and the advanced concept of metabolically-driven innate immune memory.

### The Metabolic Dichotomy of Macrophage Polarization

Macrophages exhibit a spectrum of activation states, classically simplified into two opposing phenotypes: the pro-inflammatory, microbicidal "M1" state and the anti-inflammatory, tissue-reparative "M2" state. These functional programs are underpinned by distinct and mutually exclusive metabolic signatures.

**Classical (M1) Activation: The Glycolytic Shift for Acute Defense**

Classical activation is induced by microbial products, such as **lipopolysaccharide (LPS)**, often in concert with pro-inflammatory cytokines like **interferon-gamma (IFN-γ)**. This program equips the macrophage for an aggressive, short-term response: killing pathogens and amplifying inflammation. To support these demanding functions, M1 macrophages undergo a dramatic metabolic reprogramming towards **aerobic glycolysis**, a phenomenon analogous to the Warburg effect observed in cancer cells. Instead of fully oxidizing glucose in the mitochondria, the cell rapidly converts it to lactate, even in the presence of ample oxygen. This shift prioritizes metabolic speed over efficiency; while glycolysis yields only 2 ATP per glucose molecule compared to ~30 from oxidative phosphorylation (OXPHOS), it generates ATP at a much faster rate. Furthermore, this high glycolytic flux provides a rich supply of biosynthetic intermediates necessary for producing inflammatory mediators [@problem_id:2860423].

This glycolytic state is characterized by several key features:
-   A high rate of glucose uptake and lactate secretion.
-   A disrupted or "broken" **tricarboxylic acid (TCA) cycle**.
-   An enhanced **pentose phosphate pathway (PPP)** flux.
-   Active suppression of mitochondrial **oxidative phosphorylation (OXPHOS)**.

**Alternative (M2) Activation: Oxidative Metabolism for Sustained Repair**

In contrast, alternative activation, driven by T-helper 2 (Th2) cytokines such as **interleukin-4 (IL-4)** and **interleukin-13 (IL-13)**, promotes functions related to the resolution of inflammation, wound healing, and tissue remodeling. These are sustained, long-term processes that demand a continuous and efficient supply of energy. Consequently, M2 macrophages adopt a metabolic profile centered on an intact and fully functional TCA cycle fueled by **oxidative phosphorylation**. A key feature of this state is its reliance on **fatty acid oxidation (FAO)** as a primary energy source, which provides a dense and lasting supply of acetyl-CoA to power the TCA cycle and electron transport chain [@problem_id:2860423, @problem_id:2860468]. The M2 metabolic program is characterized by increased mitochondrial biogenesis, a high respiratory capacity, and robust FAO.

### The Molecular Machinery of M1 Reprogramming

The shift to aerobic glycolysis in M1 macrophages is not a passive default but an actively orchestrated program involving multi-layered regulation, from receptor signaling to transcriptional control and direct enzymatic modulation.

#### Driving and Sustaining High Glycolytic Flux

The signaling cascades initiated by **Toll-like receptor 4 (TLR4)** engagement by LPS and the IFN-γ receptor converge on key transcription factors and signaling hubs. Pathways such as the **phosphoinositide 3-kinase (PI3K)-AKT-mechanistic Target Of Rapamycin complex 1 (mTORC1)** axis are strongly activated. These pathways, together with transcription factors like **Nuclear Factor κB (NF-κB)** and **Hypoxia-Inducible Factor-1α (HIF-1α)**, drive a transcriptional program that massively upregulates the cell's capacity for glycolysis [@problem_id:2860485]. This includes increased expression of:
-   Glucose transporters, such as **GLUT1**, to enhance glucose uptake.
-   Key glycolytic enzymes, most notably **6-phosphofructo-2-kinase/fructose-2,6-bisphosphatase 3 (PFKFB3)**. The primary kinase activity of PFKFB3 generates high levels of fructose-2,6-bisphosphate, a potent allosteric activator of phosphofructokinase-1 (PFK-1), the main gatekeeper of glycolysis [@problem_id:2860428].
-   **Lactate dehydrogenase A (LDHA)**, which converts pyruvate to lactate, regenerating the $NAD^+$ required to sustain high glycolytic rates.

This pro-glycolytic drive is counter-regulated by the cellular energy sensor **AMP-activated protein kinase (AMPK)**. AMPK is activated by a low cellular energy charge (i.e., high AMP/ATP ratio) and acts as a homeostatic brake, inhibiting anabolic processes like those driven by mTORC1 and promoting energy-efficient catabolic pathways like FAO. In the M1 context, the drive from mTORC1 and HIF-1α typically overrides the influence of AMPK [@problem_id:2860428].

#### Fueling Effector Functions via the Pentose Phosphate Pathway

The effector functions of M1 macrophages, particularly the production of microbicidal reactive oxygen species (ROS) and reactive nitrogen species (RNS), create a high demand for the reduced cofactor **nicotinamide adenine dinucleotide phosphate (NADPH)**. NADPH is the essential electron donor for **NADPH oxidase 2 (NOX2)**, which generates superoxide, and for **inducible nitric oxide synthase (iNOS)**, which produces nitric oxide (NO). This demand is met by shunting glucose-6-phosphate into the **pentose phosphate pathway (PPP)**.

The PPP has two distinct branches with complementary roles [@problem_id:2860391]:
1.  The **oxidative PPP**, initiated by **glucose-6-phosphate dehydrogenase (G6PD)**, is an effectively irreversible pathway that generates two molecules of NADPH for each molecule of glucose-6-phosphate that enters. Its primary role in M1 macrophages is to supply the large quantities of NADPH needed for ROS/RNS production.
2.  The **non-oxidative PPP**, mediated by enzymes like **transketolase**, consists of a series of reversible carbon-shuffling reactions. It provides metabolic flexibility, allowing the cell to either produce nucleotide precursors (like **ribose-5-phosphate**) for DNA/RNA synthesis or to recycle excess pentose phosphates back into glycolytic intermediates (fructose-6-phosphate and glyceraldehyde-3-phosphate). In situations where the oxidative PPP is impaired, the non-oxidative branch can run in reverse to generate ribose-5-phosphate from glycolytic intermediates, thus decoupling nucleotide synthesis from NADPH production.

### Active Suppression of Mitochondrial Metabolism in M1 Macrophages

A defining feature of the M1 phenotype is the active dismantling of mitochondrial oxidative metabolism. This occurs through a multi-pronged attack on the TCA cycle and the electron transport chain (ETC).

#### The "Broken" TCA Cycle and Metabolites as Signals

In M1 macrophages, the normally cyclical flow of the TCA cycle is interrupted at two specific points, leading to the accumulation of key intermediates that are repurposed as signaling molecules [@problem_id:2860396].

The first breakpoint occurs after citrate. Upon LPS stimulation, macrophages robustly induce the expression of **Immune-Responsive Gene 1 (IRG1)**, also known as **aconitate decarboxylase 1 (ACOD1)**. This enzyme diverts the TCA cycle intermediate **cis-aconitate** (which is in equilibrium with citrate) away from its conversion to isocitrate and instead decarboxylates it to produce **itaconate**. This metabolite accumulates to millimolar concentrations and has direct antimicrobial properties, as well as immunomodulatory functions.

The second breakpoint occurs at **succinate dehydrogenase (SDH)**, which is also Complex II of the ETC. SDH is inhibited by itaconate. This inhibition, combined with other metabolic shifts like glutamine influx, leads to a massive accumulation of **succinate**.

These accumulating metabolites, citrate and succinate, are not mere byproducts but assume critical signaling roles:

-   **Succinate as a Pro-inflammatory Signal**: The accumulated succinate acts as a potent signaling molecule primarily by inhibiting a class of α-ketoglutarate-dependent dioxygenases, including the **prolyl hydroxylase domain (PHD)** enzymes [@problem_id:2860444]. PHDs normally mark the transcription factor **HIF-1α** for degradation in the presence of oxygen. By competitively inhibiting PHDs, succinate stabilizes HIF-1α protein even under normoxic conditions—a state often called "pseudohypoxia." Stabilized HIF-1α then drives the expression of numerous pro-inflammatory and glycolytic genes, including the gene for the pro-inflammatory cytokine **interleukin-1β (IL-1β)**, creating a powerful positive feedback loop that solidifies the M1 phenotype. Furthermore, the high rate of succinate oxidation by the residual SDH activity can lead to a highly reduced coenzyme Q pool, driving **reverse electron transport (RET)** at Complex I of the ETC. This process is a major source of mitochondrial ROS, which can further contribute to PHD inhibition and inflammatory signaling [@problem_id:2860444].

-   **Citrate as an Epigenetic Link**: The citrate that accumulates from the first TCA cycle breakpoint is exported to the cytosol. There, the enzyme **ATP-citrate lyase (ACLY)** cleaves it to generate a pool of **acetyl-CoA** in the cytosol and nucleus. This acetyl-CoA is the universal acetyl-group donor for protein acetylation, including histone acetylation [@problem_id:2860447]. In LPS-stimulated macrophages, transcription factors like NF-κB recruit **histone acetyltransferases (HATs)**, such as p300/CBP, to the enhancers and promoters of inflammatory genes. The increased availability of the substrate acetyl-CoA, supplied by the metabolic shift, boosts the activity of these recruited HATs by mass action. This results in increased deposition of activating epigenetic marks like **histone H3 lysine 27 acetylation (H3K27ac)**, which helps to open the chromatin structure and promote the transcription of pro-inflammatory genes. This provides a direct, elegant mechanism linking cellular metabolic state to the epigenetic control of gene expression.

#### Direct Inhibition of the Electron Transport Chain

In addition to disrupting the TCA cycle, M1 activation actively shuts down the ETC. The high expression of iNOS leads to the production of large amounts of **nitric oxide (NO)**. NO is a potent inhibitor of the ETC, as it can bind to and inhibit **cytochrome c oxidase (Complex IV)**, the terminal enzyme of the respiratory chain. This further dampens oxygen consumption. Concurrently, the HIF-1α stabilization driven by succinate leads to the induction of **pyruvate dehydrogenase kinase 1 (PDK1)**. PDK1 phosphorylates and inhibits the **pyruvate dehydrogenase (PDH)** complex, the critical enzyme that converts pyruvate to acetyl-CoA for entry into the TCA cycle. This phosphorylation effectively closes the main gate for glycolytic carbon to enter the mitochondria, forcing pyruvate to be converted to lactate in the cytosol [@problem_id:2860485].

### The M2 Metabolic Program: Engineered for Endurance

The metabolic strategy of M2 macrophages is the inverse of the M1 program. Activated by IL-4/IL-13, these cells engage signaling through the transcription factor **STAT6**. STAT6 orchestrates a transcriptional program that prepares the cell for sustained, energy-efficient function. It induces key regulators of mitochondrial metabolism, including **peroxisome proliferator-activated receptor γ (PPARγ)** and its coactivator, **PGC-1β** [@problem_id:2860468].

This signaling cascade results in:
-   **Enhanced Mitochondrial Biogenesis**: PGC-1β is a master regulator of mitochondrial biogenesis. Its induction leads to an increase in mitochondrial mass, mitochondrial DNA content, and expression of key mitochondrial proteins like **mitochondrial transcription factor A (TFAM)**.
-   **Upregulation of Fatty Acid Oxidation**: M2 macrophages increase their expression of fatty acid transporters like **CD36** for uptake and the enzyme **carnitine palmitoyltransferase 1α (CPT1α)**, which controls the import of long-chain fatty acids into mitochondria for β-oxidation.
-   **High Oxidative Capacity**: The result of this reprogramming is a cell with a large and robust mitochondrial network, a high basal oxygen consumption rate, and a large spare respiratory capacity. This allows the M2 macrophage to efficiently generate ATP from fatty acids to sustain long-term functions like tissue remodeling and efferocytosis.

### Advanced Concepts: Metabolism in Lipid Homeostasis and Innate Memory

The principles of myeloid immunometabolism extend beyond the simple M1/M2 dichotomy, influencing complex pathologies and long-term immune states.

#### Lipid Metabolism and Foam Cell Formation

Macrophage lipid handling is central to diseases like atherosclerosis. The formation of "foam cells"—macrophages laden with cholesteryl esters—is a hallmark of atherosclerotic plaques. This process is governed by a balance of lipid influx, synthesis, esterification for storage, and efflux. Macrophages take up modified lipoproteins via scavenger receptors like **CD36**. The cholesterol within is esterified by **acyl-coenzyme A:cholesterol acyltransferase 1 (ACAT1)** and stored in lipid droplets. In parallel, cells can synthesize their own fatty acids via **de novo lipogenesis (DNL)**, a process controlled by enzymes like **acetyl-CoA carboxylase (ACC)**. To prevent lipid overload, macrophages efflux excess cholesterol via transporters like **ABCA1** and **ABCG1**, which are transcriptionally regulated by the **Liver X receptor (LXR)**. A disruption in this delicate balance, favoring uptake and storage over efflux, leads to foam cell formation [@problem_id:2860435].

#### Trained Immunity: A Metabolically-Encoded Memory

While the innate immune system was once thought to lack memory, it is now clear that myeloid cells can develop a long-lasting state of heightened responsiveness after an initial stimulus, a phenomenon termed **trained immunity**. This "memory" is not based on antigen receptors but is encoded at the epigenetic level, and its establishment and maintenance are critically dependent on metabolic reprogramming [@problem_id:2860459].

The key metabolic pathways underpinning trained immunity include:
-   A long-term shift to aerobic glycolysis, sustained by signaling through the **mevalonate pathway** and **mTOR**. The mevalonate pathway, responsible for cholesterol synthesis, acts as a signaling hub to maintain this glycolytic state.
-   The persistent glycolytic flux provides the acetyl-CoA needed for HATs to deposit activating marks like **H3K27ac** at inflammatory gene loci.
-   Accumulation of the TCA cycle intermediate **fumarate**. Similar to succinate, fumarate inhibits α-ketoglutarate-dependent dioxygenases. Specifically, it inhibits **KDM5 histone lysine demethylases**, which normally remove the activating histone mark H3K4 trimethylation (H3K4me3). Fumarate-mediated inhibition of KDM5 leads to the preservation of H3K4me3 at gene promoters.

Together, the persistent deposition of H3K27ac and preservation of H3K4me3 maintain an open, accessible chromatin state at inflammatory genes, "training" the macrophage to mount a faster and more robust response upon a secondary, unrelated challenge. This demonstrates how metabolic rewiring can establish durable epigenetic states that shape long-term immune function.