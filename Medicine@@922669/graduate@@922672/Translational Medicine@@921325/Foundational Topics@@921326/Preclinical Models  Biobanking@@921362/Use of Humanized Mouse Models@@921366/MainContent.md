## Introduction
The ability to accurately model human biological systems, especially the immune system, in a controlled preclinical setting is a central challenge in translational medicine. Humanized mice—immunodeficient rodents engrafted with human cells, tissues, or genes—have emerged as a powerful solution, providing an invaluable *in vivo* platform to bridge the gap between laboratory research and clinical application. However, the utility of these models is not absolute; their successful implementation depends on a deep understanding of their underlying biological principles, specific applications, and inherent limitations.

This article provides a comprehensive guide to the use of [humanized mouse](@entry_id:184283) models for the graduate-level translational scientist. The first chapter, **Principles and Mechanisms**, will dissect the foundational requirements for creating these models, from the genetic engineering of immunodeficient hosts to the molecular hurdles of human cell engraftment and immune reconstitution. Next, the **Applications and Interdisciplinary Connections** chapter will explore how these models are strategically deployed across key research areas like [immuno-oncology](@entry_id:190846), infectious disease, and pharmacology, highlighting their transformative impact and practical challenges. Finally, the **Hands-On Practices** section will present practical problems designed to hone the critical thinking skills needed to select appropriate models, design robust experiments, and correctly interpret complex data. By navigating these chapters, you will gain the expertise to critically evaluate and effectively utilize [humanized mouse](@entry_id:184283) models in your own research.

## Principles and Mechanisms

The capacity to model human biological systems, particularly the immune system, within a tractable small animal is a cornerstone of modern translational medicine. Humanized mice—rodents engrafted with human cells, tissues, or genes—provide this capacity. This chapter delineates the fundamental principles governing the creation and function of these models, from the essential genetic modifications of the host mouse to the complex cellular and [molecular interactions](@entry_id:263767) that determine the fidelity of the reconstituted human system.

### Fundamental Prerequisites for Humanization

The successful engraftment and maintenance of foreign (xenogeneic) human cells and tissues in a mouse is not trivial; it requires overcoming formidable immunological barriers. The primary prerequisite is a host mouse that is profoundly immunodeficient, rendering it incapable of rejecting the human graft.

#### The Immunodeficient Host Environment

Standard laboratory mice possess a fully competent immune system that would rapidly identify and destroy human cells. To circumvent this, [humanized mouse](@entry_id:184283) models are built upon host strains harboring specific genetic mutations that cripple the immune system. The development of these strains has progressed through stages of increasing immunodeficiency.

A foundational level of [immunodeficiency](@entry_id:204322) is achieved by ablating [adaptive immunity](@entry_id:137519)—the specific, memory-forming arm of the immune system mediated by **T lymphocytes** and **B lymphocytes**. The development of these cells is contingent upon the successful rearrangement of gene segments to form a functional antigen receptor, a process known as **V(D)J recombination**. Two classes of mutations are commonly used to disrupt this process [@problem_id:5074118]:
1.  **Mutations in DNA Repair:** The [severe combined immunodeficiency](@entry_id:180887), or **scid**, mutation is a loss-of-function allele in the gene encoding the protein kinase, DNA-activated, catalytic polypeptide ($\mathrm{Prkdc}$). This enzyme is essential for repairing the DNA double-strand breaks created during V(D)J recombination. In its absence, developing lymphocytes undergo apoptosis, resulting in mice that lack functional T and B cells.
2.  **Mutations in Recombination Machinery:** The **Recombination Activating Genes**, $\mathrm{RAG}1$ and $\mathrm{RAG}2$, encode the enzymatic machinery that initiates V(D)J recombination. A genetic knockout of $\mathrm{RAG}1$ or $\mathrm{RAG}2$ completely prevents the formation of antigen receptors, arresting [lymphocyte development](@entry_id:194643) at an early stage and likewise resulting in a lack of mature T and B cells.

While these mutations effectively eliminate adaptive immunity, they leave key components of the [innate immune system](@entry_id:201771) intact. Notably, both $\mathrm{Prkdc^{scid}}$ and $\mathrm{RAG}^{-/-}$ mice retain functional **Natural Killer (NK) cells**, which are potent killers of xenogeneic cells and pose a significant barrier to human cell engraftment.

A more profound level of [immunodeficiency](@entry_id:204322) is achieved by targeting a crucial [cytokine signaling](@entry_id:151814) pathway. Many [interleukins](@entry_id:153619)—cytokines critical for [lymphocyte development](@entry_id:194643), survival, and function—signal through receptors that share a common subunit, the **[interleukin-2](@entry_id:193984) receptor [common gamma chain](@entry_id:204728) ($IL2RG$ or $\gamma_c$)**. A null mutation in the $\mathrm{Il2rg}$ gene abrogates signaling by multiple cytokines, including IL-2, IL-4, IL-7, IL-9, IL-15, and IL-21. As IL-7 is essential for T-cell development and IL-15 is required for NK cell development, an **$\mathrm{Il2rg^{null}}$** mutation results in the additional loss of NK cells, on top of the T and B cell deficiency. This triple-deficient phenotype makes strains like the widely used **NOD-scid IL2R$\gamma$null (NSG)** mouse a far more permissive host for human xenografts [@problem_id:5074118].

### Mechanisms of Human Hematopoietic Engraftment

Introducing human **Hematopoietic Stem and Progenitor Cells (HSPCs)**, typically isolated as $\mathrm{CD34}^{+}$ cells, into an immunodeficient mouse is the first step toward building a human hematopoietic system *de novo*. However, the success of this process is governed by a series of mechanistic hurdles related to the murine host environment.

#### Niche Competition and Myeloablation

The bone marrow contains specialized microenvironments, or **niches**, that support the survival and self-renewal of HSPCs. These niches have a finite carrying capacity. For human HSPCs to successfully engraft, they must be able to access and occupy these niches, which may be already populated by residual host HSPCs. To "make space," host mice are often preconditioned with sublethal irradiation or myeloablative chemotherapy agents like busulfan. This process depletes the endogenous murine hematopoiesis, vacating niche space and dramatically improving the efficiency of human HSPC engraftment [@problem_id:5074092].

#### Overcoming Innate Immune Barriers

Even in hosts lacking T, B, and NK cells, other innate immune cells, particularly **macrophages**, remain a barrier to engraftment. Macrophages are [phagocytes](@entry_id:199861) that survey the body for foreign or damaged cells. Healthy "self" cells display a "do-not-eat-me" signal on their surface, the protein **CD47**. This signal is recognized by the **Signal Regulatory Protein alpha (SIRP$\alpha$)** on macrophages, which triggers an inhibitory signaling cascade that prevents phagocytosis.

This interaction exhibits species specificity. Murine SIRP$\alpha$ on host macrophages binds weakly to human CD47 on engrafted cells. This insufficient inhibitory signal leads to the phagocytic clearance of human cells, limiting engraftment. Fortuitously, the SIRP$\alpha$ allele from the Non-Obese Diabetic (NOD) mouse strain background exhibits a significantly higher binding affinity for human CD47 compared to alleles from other common strains like C57BL/6. For instance, the dissociation constant ($K_D$) for the human CD47–NOD SIRP$\alpha$ interaction may be orders of magnitude lower (stronger binding) than for the human CD47–C57BL/6 SIRP$\alpha$ interaction. This superior binding crosses the signaling threshold required to suppress [phagocytosis](@entry_id:143316), making the NOD genetic background a critical component of most successful [humanized mouse](@entry_id:184283) platforms [@problem_id:5074090].

#### The Challenge of Species-Specific Cytokines

The survival, proliferation, and differentiation of human HSPCs into mature blood lineages are dependent on a continuous supply of specific cytokines. However, many murine cytokines bind poorly to their cognate human receptors, leading to insufficient signaling. This species-specific cytokine incompatibility is a major bottleneck.

This is particularly evident for the **myeloid lineages** ([monocytes](@entry_id:201982), macrophages, [granulocytes](@entry_id:191554)) and for **NK cells**. The development of human myeloid progenitors depends on cytokines like Granulocyte-Macrophage Colony-Stimulating Factor (GM-CSF), Interleukin-3 (IL-3), and Macrophage Colony-Stimulating Factor (M-CSF). Human NK cell development is critically dependent on Interleukin-15 (IL-15). In a standard HSPC-engrafted mouse, the murine versions of these cytokines are unable to provide adequate support for their respective human lineages. As a result, while human B-cell development is relatively robust, the reconstitution of human myeloid and NK cell compartments is typically poor. This leads to an immune system that is lymphoid-skewed and deficient in key innate effector cells [@problem_id:5074087].

### Major Categories of Humanized Mouse Models

Based on the nature of the engrafted human component, [humanized mouse](@entry_id:184283) models can be broadly classified into several categories, each with distinct advantages, limitations, and applications.

#### PBMC-Engrafted Models

The simplest and most rapid method of humanization involves the intravenous injection of human **Peripheral Blood Mononuclear Cells (PBMCs)** into a severely immunodeficient host (e.g., NSG). The PBMC inoculum contains mature human T cells, B cells, NK cells, and [monocytes](@entry_id:201982).

-   **Immune Profile:** This model provides a quick reconstitution of mature, functional human effector cells, especially T cells.
-   **Primary Limitation and Application:** The key feature of this model is the rapid onset of **xenogeneic Graft-versus-Host Disease (xeno-GVHD)** [@problem_id:5074114]. The mature donor T cells in the PBMC graft recognize the mouse's tissues as foreign. This recognition can occur via two pathways: a **direct pathway**, where human T-[cell receptors](@entry_id:147810) (TCRs) recognize intact murine Major Histocompatibility Complex (MHC) molecules on host cells, and an **indirect pathway**, where human APCs from the graft process murine proteins and present them on human MHC (known as Human Leukocyte Antigen, or HLA). Both pathways trigger a massive T-cell activation and proliferation, leading to a "[cytokine storm](@entry_id:148778)"—a positive feedback loop where pro-inflammatory cytokines like [interferon-gamma](@entry_id:203536) (IFN-$\gamma$) and [tumor necrosis factor-alpha](@entry_id:194965) (TNF-$\alpha$) activate host cells to amplify inflammation, culminating in systemic tissue damage [@problem_id:5074152]. Due to this pathology, PBMC models have a short experimental window but are invaluable for studying the mechanisms of T-cell-mediated alloreactivity and GVHD itself.

#### HSPC-Engrafted Models

In this model, human $\mathrm{CD34}^{+}$ HSPCs are engrafted, leading to the *de novo* development of a multi-lineage human immune system from stem cells. This process takes several weeks and avoids the immediate, lethal GVHD seen in PBMC models.

-   **Immune Profile:** These models generate a diverse population of human immune cells, including T cells, B cells, and some myeloid and NK cells, that are self-tolerant.
-   **Primary Limitation 1: T-cell Education and MHC Restriction:** A fundamental challenge arises from the site of T-cell development. Human T cells mature in the host's murine thymus. There, they undergo **[positive selection](@entry_id:165327)**, a process where only T cells that can weakly recognize self-peptides presented on MHC molecules are allowed to survive. Because this selection occurs on murine thymic epithelial cells expressing murine MHC, the resulting human T-cell repertoire is **mouse MHC-restricted** [@problem_id:5074133]. This creates a critical mismatch. When these T cells encounter a human antigen-presenting cell (e.g., a B cell or dendritic cell) in the periphery, which presents antigens on **human HLA**, the T cells are unable to recognize the complex effectively. This "MHC restriction mismatch" cripples T-cell help to other immune cells. A major consequence is the failure to mount effective T-dependent antibody responses; although initial IgM production may occur, the formation of **germinal centers**—the microstructures required for B-cell class-switching and affinity maturation—is profoundly impaired, leading to suboptimal IgG responses [@problem_id:5074148].
-   **Primary Limitation 2: Lineage Skew:** As discussed previously, the lack of cross-reactive murine cytokines results in poor reconstitution of myeloid and NK cell lineages, creating an immune system biased toward lymphoid cells [@problem_id:5074087].

#### The BLT Model

The **Bone Marrow, Liver, Thymus (BLT)** model was developed specifically to overcome the MHC restriction mismatch of HSPC-only models.

-   **Construction:** This model involves the surgical implantation of human fetal thymus and liver tissue (a source of HSPCs) under the kidney capsule of an immunodeficient mouse, often followed by an injection of additional autologous HSPCs.
-   **Key Advantage: HLA-Restricted T-cell Development:** The implanted human thymus tissue provides a complete human [thymic microenvironment](@entry_id:181339), including human thymic epithelial cells that express HLA. Developing human T cells now undergo positive selection on human HLA molecules. This generates a mature T-cell repertoire that is correctly **HLA-restricted**. These T cells are fully capable of recognizing and interacting with human APCs, enabling robust cell-mediated immunity and significantly improved T-dependent B-cell responses, including better germinal center formation and [mucosal immunity](@entry_id:173219) [@problem_id:5074114] [@problem_id:5074133]. While more complex to create, BLT mice represent a higher-fidelity model for studying human adaptive immunity.

### Advanced Models: Genetic Engineering of the Host

To address the remaining limitations, particularly the poor development of non-lymphoid lineages, the latest generation of humanized mice involves the genetic modification of the host to provide critical human-specific factors.

#### Targeted Support for Specific Lineages

By introducing the genes for human cytokines into the mouse genome, researchers can create a more supportive environment for human [hematopoiesis](@entry_id:156194). This "human [gene knock-in](@entry_id:195029)" strategy can be tailored to boost specific lineages [@problem_id:5074105]:

-   **Myeloid and Erythroid Support:** Strains have been engineered to express a suite of human cytokines critical for myelopoiesis and erythropoiesis, such as M-CSF, IL-3, GM-CSF, and Thrombopoietin (TPO).
-   **NK Cell Support:** Expressing human IL-15 is the key to achieving robust development and functional maturation of human NK cells.

#### Contrasting Expression Strategies

The method of transgene expression has important consequences.
-   **Constitutive Overexpression:** Some models, like the **NSG-SGM3** strain (expressing human SCF, GM-CSF, and IL-3), use strong, constitutively active promoters. This results in very high, supraphysiological levels of cytokines. While this potently drives myeloid expansion, it can also lead to artifacts, such as the exhaustion and depletion of the human HSPC pool over time [@problem_id:5074105].
-   **Physiological Knock-in:** A more refined approach involves "knocking in" the human gene into the corresponding mouse [gene locus](@entry_id:177958). This places the human gene under the control of the endogenous mouse promoter, resulting in expression at the right time, in the right place, and at more physiological levels. The **MISTRG** strain, for example, combines knock-ins for human M-CSF, IL-3/GM-CSF, TPO, and SIRP$\alpha$. This strategy supports broad, multi-lineage reconstitution of human myeloid, erythroid, and platelet lineages in a more balanced and sustained manner [@problem_id:5074105].

By combining these advanced genetic modifications with superior immunodeficient backgrounds, researchers are continuously developing higher-fidelity models that more accurately recapitulate the complexity of the human immune system.