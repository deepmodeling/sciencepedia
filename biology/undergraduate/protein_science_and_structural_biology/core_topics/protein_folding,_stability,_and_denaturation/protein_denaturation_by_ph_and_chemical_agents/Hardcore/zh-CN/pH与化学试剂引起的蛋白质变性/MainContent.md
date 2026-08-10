## 引言
蛋白质是生命的基石，其特定的三维结构决定了其多样化的生物学功能。然而，这种精密的结构非常脆弱，容易受到环境变化的干扰。蛋白质高级结构的解体，即变性，是一个在生物学和[生物技术](@keyword=biotechnology|lang=zh-CN|style=Feynman)中具有核心重要性的过程。理解pH值和化学试剂等因素如何精确地诱导[蛋白质变性](@keyword=protein_denaturation|lang=zh-CN|style=Feynman)，不仅是[蛋白质科学](@keyword=protein_science|lang=zh-CN|style=Feynman)的基础，也是控制蛋白质行为、开发新技术以及理解疾病的关键。

本文将系统地探讨这一主题。在“原理与机制”一章中，我们将深入研究[蛋白质变性](@keyword=protein_denaturation|lang=zh-CN|style=Feynman)的[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)基础以及不同[变性](@keyword=denaturation|lang=zh-CN|style=Feynman)剂的分子作用方式。接着，在“应用与跨学科联系”一章中，我们将展示这些基本原理如何在食品科学、实验室分析和医学等领域得到广泛应用。最后，“动手实践”部分将提供一系列问题，帮助您将理论知识应用于解决实际的生化难题。

让我们首先从[蛋白质稳定性](@keyword=protein_stability|lang=zh-CN|style=Feynman)的基本[物理化学](@keyword=physical_chemistry|lang=zh-CN|style=Feynman)原理出发，揭示变性过程的内在机制。

## 原理与机制

蛋白质的生物学功能与其精确的三维结构密不可分。这种被称为天然构象（native conformation）的结构，是通过一系列相对较弱的[非共价相互作用](@keyword=noncovalent_interactions|lang=zh-CN|style=Feynman)（如[疏水效应](@entry_id:146085)、[氢键](@keyword=hydrogen_bonding|lang=zh-CN|style=Feynman)、静电相互作用和[范德华力](@keyword=van_der_waals_forces|lang=zh-CN|style=Feynman)）以及在某些情况下的共价二硫键共同维持的。然而，这种功能性结构的[热力学稳定性](@keyword=thermodynamic_stability|lang=zh-CN|style=Feynman)通常是边际的，意味着它很容易被环境条件的改变所破坏。蛋白质高级结构（即二级、三级和[四级结构](@keyword=quaternary_structure|lang=zh-CN|style=Feynman)）的丧失，而其[一级结构](@keyword=primary_structure|lang=zh-CN|style=Feynman)（由共价肽键连接的[氨基酸序列](@keyword=amino_acid_sequence|lang=zh-CN|style=Feynman)）保持不变的过程，被称为**变性（denaturation）**。理解变性的原理与机制，对于蛋白质研究、生物技术应用以及揭示与[蛋白质错误折叠](@keyword=protein_misfolding|lang=zh-CN|style=Feynman)相关的疾病至关重要。[@problem_id:2127262]

### [蛋白质稳定性](@keyword=protein_stability|lang=zh-CN|style=Feynman)的[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)视角

从[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)的角度来看，蛋白质在溶液中的折叠与去折叠可以被视为一个在天然态（Native, N）和去折叠态（Unfolded, U）之间的平衡过程：$N \rightleftharpoons U$。这个平衡的位置由去折叠过程的[吉布斯自由能变](@keyword=change_in_gibbs_free_energy|lang=zh-CN|style=Feynman)（Gibbs free energy of unfolding），即 $\Delta G_{\text{unfolding}}$，所决定。

在生理条件下，$\Delta G_{\text{unfolding}}$ 通常是一个小的正值（例如，对于一个典型的小蛋白，其值可能在 $+20$ 到 $+60 \text{ kJ/mol}$ 之间），这表明天然态（N）在能量上比去折叠态（U）更有利，平衡偏向于折叠的、具有功能的蛋白质。[变性](@keyword=denaturation|lang=zh-CN|style=Feynman)剂（denaturants）的作用，无论是化学物质还是pH值的极端变化，都是通过改变溶剂环境来降低 $\Delta G_{\text{unfolding}}$ 的值，从而使去折叠态在能量上变得相对更有利，最终将平衡推向去折叠态（U）。[@problem_id:2127263]

对于[化学变性](@keyword=chemical_denaturation|lang=zh-CN|style=Feynman)剂，$\Delta G_{\text{unfolding}}$ 与变性剂浓度 $[D]$ 之间的关系通常可以用**线性外推模型（Linear Extrapolation Model, LEM）**来近似描述：

$$ \Delta G_{\text{unfolding}}([D]) = \Delta G^{\circ}_{\text{unfolding}, H_2O} - m[D] $$

在此模型中，$\Delta G^{\circ}_{\text{unfolding}, H_2O}$ 是蛋白质在纯水[缓冲液](@keyword=buffer_solutions|lang=zh-CN|style=Feynman)中的固有稳定性（即 $[D]=0$ 时的自由能变）。$m$ 值则是一个经验参数，它量化了蛋白质的稳定性随[变性](@keyword=denaturation|lang=zh-CN|style=Feynman)剂浓度增加而降低的程度，反映了蛋白质对该变性剂的敏感性。一个较大的 $m$ 值意味着蛋白质的稳定性对[变性](@keyword=denaturation|lang=zh-CN|style=Feynman)剂浓度更敏感。利用该模型，我们可以精确预测在特定变性剂浓度下，蛋白质群体中处于去折叠状态的比例。例如，对于一个在水溶液中稳定性 $\Delta G^{\circ}_{\text{unfolding}, H_2O}$ 为 $+25.0 \text{ kJ/mol}$、对尿素的 $m$ 值为 $8.00 \mathrm{kJ/(mol\cdot M)}$ 的蛋白质，通过计算可以得出，需要大约 $4.04 \text{ M}$ 的尿素浓度才能使其达到 $95\%$ 的去折叠。[@problem_id:2127263]

这个过程也是可逆的。如果将一个在例如 $6.00 \text{ M}$ 盐酸胍（GdmCl）中几乎完全变性的蛋白质溶液，通过稀释将其浓度降低到 $1.20 \text{ M}$，$\Delta G_{\text{unfolding}}$ 将会增加，平衡会向天然折叠态移动，使得大部分蛋白质恢复其天然构象。[@problem_id:2127243]

### pH值对[蛋白质稳定性](@keyword=protein_stability|lang=zh-CN|style=Feynman)的影响

溶液的pH值是影响蛋白质结构稳定性的一个关键物理化学参数。pH值的极端变化主要通过改变蛋白质表面可电离基团的质子化状态来破坏其结构，其机制主要包括以下两点：

**1. 盐桥的破坏**
**盐桥（salt bridges）**是在蛋白质内部或表面，由带相反[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的[氨基酸侧链](@keyword=amino_acid_side_chains|lang=zh-CN|style=Feynman)（如天冬氨酸/谷氨酸的负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)[羧基](@keyword=carboxyl_group|lang=zh-CN|style=Feynman)与赖氨酸/精氨酸的正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)氨基）之间形成的静电吸引作用。这种相互作用对维持蛋白质的特定三维折叠至关重要。当环境pH值远低于酸性残基[侧链](@keyword=side_chains|lang=zh-CN|style=Feynman)的 $pK_a$ 值（例如pH  3）时，其羧基会被质子化（-COOH），失去负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。反之，当pH值远高于碱性残基侧链的 $pK_a$ 值（例如pH > 11）时，其氨基会去质子化（-NH2），失去正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。在这两种情况下，盐桥中的一个带电伙伴被中和，导致[静电吸引](@keyword=electrostatic_attraction|lang=zh-CN|style=Feynman)力消失，从而破坏了对结构的稳定作用。蛋白质的稳定性因此仅限于一个特定的pH范围内，在此范围内，形成盐桥的关键残基能够维持其互补的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)状态。我们可以利用[Henderson-Hasselbalch方程](@keyword=henderson_hasselbalch_equation|lang=zh-CN|style=Feynman)来精确计算维持一个功能性盐桥（例如，要求双方至少95%处于正确[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)状态）所需的pH范围。[@problem_id:2127244]

**2. 静电排斥的增强**
当pH值变得非常低时（例如pH = 2.0），蛋白质中几乎所有的酸性侧链（如天冬氨酸和谷氨酸）都被质子化而呈[电中性](@keyword=electroneutrality|lang=zh-CN|style=Feynman)，而所有的碱性侧链（如赖氨酸和精氨酸）则几乎完全质子化，携带正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。如果一个蛋白质表面富含这类碱性残基，那么在极低pH下，其表面将积累大量的正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。这些同种[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)之间会产生强烈的**静电排斥力（electrostatic repulsion）**。这种排斥力作用于蛋白质的不同部分，会像一个强大的[内力](@keyword=internal_forces|lang=zh-CN|style=Feynman)一样将肽链推开，足以克服维持蛋白质紧密折叠的疏水作用和[氢键](@keyword=hydrogen_bonding|lang=zh-CN|style=Feynman)等吸[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)，最终导致[蛋白质解折叠](@keyword=protein_unfolding|lang=zh-CN|style=Feynman)。[@problem_id:2127283] 同样地，在非常高的pH值下，酸性残基会携带大量的负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，也会因[静电排斥](@keyword=electrostatic_repulsion|lang=zh-CN|style=Feynman)而引起类似的变性效应。

### [化学变性](@keyword=chemical_denaturation|lang=zh-CN|style=Feynman)剂的作用机制

多种化学试剂能够诱导[蛋白质变性](@keyword=protein_denaturation|lang=zh-CN|style=Feynman)，它们通过不同的分子机制来破坏稳定天然构象的各种作用力。

#### [离液剂](@keyword=chaotropic_agents|lang=zh-CN|style=Feynman)（尿素与盐酸胍）

**尿素（Urea）**和**盐酸胍（Guanidinium Chloride, GdmCl）**是两种最常用的**[离液剂](@keyword=chaotropic_agents|lang=zh-CN|style=Feynman)（chaotropic agents）**。它们的主要变性机制是间接的，即通过破坏水分子的[氢键网络](@keyword=hydrogen_bond_network|lang=zh-CN|style=Feynman)结构来削弱**疏水效应（hydrophobic effect）**。疏水效应是驱动水溶性[球状蛋白折叠](@keyword=globular_protein_folding|lang=zh-CN|style=Feynman)的主要力量，它促使[非极性氨基酸](@keyword=nonpolar_amino_acids|lang=zh-CN|style=Feynman)侧链埋藏在蛋白质内部，以减少与水接触造成的不利的熵损失。[离液剂](@keyword=chaotropic_agents|lang=zh-CN|style=Feynman)通过扰乱水的有序结构，使得将[非极性侧链](@keyword=nonpolar_side_chains|lang=zh-CN|style=Feynman)暴露于溶剂中的能量代价降低。这样一来，去折叠态（[非极性侧链](@keyword=nonpolar_side_chains|lang=zh-CN|style=Feynman)暴露）就变得在能量上更有利，从而促进了蛋白质的解折叠。[@problem_id:2127257]

除了削弱疏水效应，高浓度的尿素和盐酸胍分子也能直接与[蛋白质相互作用](@keyword=protein_protein_interactions|lang=zh-CN|style=Feynman)。它们可以作为[氢键](@keyword=hydrogen_bonding|lang=zh-CN|style=Feynman)的供体和受体，与蛋白质骨架上的[肽键](@keyword=peptide_bond|lang=zh-CN|style=Feynman)以及[极性侧链](@keyword=polar_side_chains|lang=zh-CN|style=Feynman)竞争形成[氢键](@keyword=hydrogen_bonding|lang=zh-CN|style=Feynman)，从而破坏了对二级和[三级结构](@keyword=tertiary_structure|lang=zh-CN|style=Feynman)至关重要的内部氢键网络。[@problem_id:2127262] 值得注意的是，[离液剂](@keyword=chaotropic_agents|lang=zh-CN|style=Feynman)只破坏非共价相互作用，它们不能切断[共价键](@keyword=covalent_bonding|lang=zh-CN|style=Feynman)，如肽键或二硫键。

#### 有机溶剂

乙醇、丙酮等有机溶剂也能有效地使[蛋白质变性](@keyword=protein_denaturation|lang=zh-CN|style=Feynman)，但其机理与[离液剂](@keyword=chaotropic_agents|lang=zh-CN|style=Feynman)有本质区别。这些溶剂的极性低于水。当它们与水混合时，会降低整个溶剂体系的极性。对于一个以疏水效应为主要稳定力的蛋白质而言，其非极性核心之所以埋藏起来，是因为在水环境中这样做在能量上是有利的。当溶剂环境的非极性增加时，将[非极性侧链](@keyword=nonpolar_side_chains|lang=zh-CN|style=Feynman)暴露出来的“惩罚”就减小了。有机溶剂分子（如乙醇的乙基）可以有效地“溶解”或**[溶剂化](@keyword=solvation|lang=zh-CN|style=Feynman)（solvate）**这些[非极性侧链](@keyword=nonpolar_side_chains|lang=zh-CN|style=Feynman)，为它们提供一个比纯水更有利的微环境。这实质上是“引诱”蛋白质的疏水核心向外翻转，从而导致其结构解体。[@problem_id:2127257]

#### 去垢剂（[十二烷基硫酸钠](@keyword=sodium_dodecyl_sulfate|lang=zh-CN|style=Feynman)）

**[十二烷基硫酸钠](@keyword=sodium_dodecyl_sulfate|lang=zh-CN|style=Feynman)（Sodium Dodecyl Sulfate, SDS）**是一种阴离子去垢剂，也是一种极其强大的变性剂。它的作用机理源于其**双亲性（amphipathic）**结构：一个长的、疏水的烷基链尾部和一个带负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的[硫酸](@keyword=sulfuric_acid|lang=zh-CN|style=Feynman)根头部。

当[SDS](@keyword=sodium_dodecyl_sulfate|lang=zh-CN|style=Feynman)与蛋白质作用时，其疏水尾部会插入并结合到蛋白质的[疏水核心](@keyword=hydrophobic_core|lang=zh-CN|style=Feynman)以及沿多肽链[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)的非极性区域。这种结合有效地破坏了维持天然[三级结构](@keyword=tertiary_structure|lang=zh-CN|style=Feynman)的内部[疏水相互作用](@keyword=hydrophobic_interaction|lang=zh-CN|style=Feynman)。与此同时，大量的[SDS](@keyword=sodium_dodecyl_sulfate|lang=zh-CN|style=Feynman)分子结合到[多肽链](@keyword=polypeptide_chain|lang=zh-CN|style=Feynman)上，其带负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的头部暴露在外。这使得整个蛋白质-SDS复合物表面覆盖了一层密集的负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，这些同种[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)间的强烈[静电排斥](@keyword=electrostatic_repulsion|lang=zh-CN|style=Feynman)力会迫使[多肽链](@keyword=polypeptide_chain|lang=zh-CN|style=Feynman)解开其折叠结构，伸展成一个近似的棒状形态。这种双重作用（破坏[疏水核心](@keyword=hydrophobic_core|lang=zh-CN|style=Feynman)和引入静电排斥）非常高效，能够瓦解绝大多数二级和[三级结构](@keyword=tertiary_structure|lang=zh-CN|style=Feynman)。最终得到的蛋白质-[SDS](@keyword=sodium_dodecyl_sulfate|lang=zh-CN|style=Feynman)复合物具有大致均匀的负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)/质量比，这是其在[SDS](@keyword=sodium_dodecyl_sulfate|lang=zh-CN|style=Feynman)-[聚丙烯酰胺凝胶电泳](@keyword=polyacrylamide_gel_electrophoresis|lang=zh-CN|style=Feynman)（[SDS-PAGE](@keyword=sds_page|lang=zh-CN|style=Feynman)）技术中能够按分子量大小进行分离的基础。[@problem_id:2127272]

#### [重金属](@keyword=heavy_metals|lang=zh-CN|style=Feynman)离子

一些[重金属](@keyword=heavy_metals|lang=zh-CN|style=Feynman)离子，如铅（$Pb^{2+}$）、汞（$Hg^{2+}$）和镉（$Cd^{2+}$），可以通过与特定的氨基酸侧链发生[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)来使[蛋白质变性](@keyword=protein_denaturation|lang=zh-CN|style=Feynman)。它们对**半胱氨酸残基的巯基（sulfhydryl group, -SH）**具有极高的亲和力。重金属离子可以与一个或多个巯基形成非常稳定的[共价键](@keyword=covalent_bonding|lang=zh-CN|style=Feynman)或[配位键](@keyword=coordinate_dative_bond|lang=zh-CN|style=Feynman)（称为硫[醇盐](@keyword=alkoxide|lang=zh-CN|style=Feynman)，mercaptide）。

如果一个或多个自由的巯基对于维持酶的活性构象是必需的，那么重金属离子的结合将直接破坏这一结构。例如，一个[二价金属](@keyword=divalent_metals|lang=zh-CN|style=Feynman)离子（$M^{2+}$）可能会与两个巯基发生[化学计量](@keyword=chemical_stoichiometry|lang=zh-CN|style=Feynman)反应，形成一个桥联，从而扰乱蛋白质的局部或整体折叠。这种[变性作用](@keyword=denaturation|lang=zh-CN|style=Feynman)是基于特定的[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)，其程度与[重金属](@keyword=heavy_metals|lang=zh-CN|style=Feynman)离子的浓度和可用巯基的数量直接相关。例如，要完全[变性](@keyword=denaturation|lang=zh-CN|style=Feynman)一个含有6个关键半胱氨酸残基的酶，且[反应化学计量](@keyword=reaction_stoichiometry|lang=zh-CN|style=Feynman)为每1个 $Pb^{2+}$ 离子结合2个巯基，则需要精确计算并加入足够量的含铅化合物。[@problem_id:2127248]

### [共价键](@keyword=covalent_bonding|lang=zh-CN|style=Feynman)的破坏：还原剂的角色

前面讨论的大多数变性剂主要破坏的是[非共价相互作用](@keyword=noncovalent_interactions|lang=zh-CN|style=Feynman)。然而，许多分泌蛋白和胞外蛋白的[结构稳定性](@keyword=structural_stability|lang=zh-CN|style=Feynman)还依赖于**二硫键（disulfide bonds）**。二硫键是在两个半胱氨酸残基的巯基之间通过氧化形成的[共价键](@keyword=covalent_bonding|lang=zh-CN|style=Feynman)（-S-S-）。这种共价交联可以像“锁扣”一样将多肽链的不同部分牢牢固定在一起，极大地增强了蛋白质的[结构稳定性](@keyword=structural_stability|lang=zh-CN|style=Feynman)。

像尿素这样的[离液剂](@keyword=chaotropic_agents|lang=zh-CN|style=Feynman)虽然能破坏[氢键](@keyword=hydrogen_bonding|lang=zh-CN|style=Feynman)和疏水作用，但无法切断共价的[二硫键](@keyword=disulfide_bridge|lang=zh-CN|style=Feynman)。因此，对于一个含有[二硫键](@keyword=disulfide_bridge|lang=zh-CN|style=Feynman)的蛋白质，单独使用高浓度的尿素或盐酸胍只能使其部分解折叠，而无法使其完全伸展为线性随机卷曲。

要断裂[二硫键](@keyword=disulfide_bridge|lang=zh-CN|style=Feynman)，必须使用**[还原剂](@keyword=reducing_agent|lang=zh-CN|style=Feynman)（reducing agents）**，如**二硫苏糖醇（Dithiothreitol, DTT）**或 $\beta$-巯基乙醇。这些试剂可以将稳定的[二硫键](@keyword=disulfide_bridge|lang=zh-CN|style=Feynman)还原为两个自由的巯基（-SH）。因此，要将一个由非共价作用和二硫键共同稳定的蛋白质**完全变性**，通常需要同时使用两种试剂：一种[离液剂](@keyword=chaotropic_agents|lang=zh-CN|style=Feynman)（如尿素）来破坏所有的非共价相互作用，以及一种还原剂（如DTT）来切断所有的二硫键。只有这样，才能确保蛋白质被还原成一个完全线性的多肽链。[@problem_id:2127277]

### 变性的[可逆性](@keyword=invertibility|lang=zh-CN|style=Feynman)与中间态

[蛋白质变性](@keyword=protein_denaturation|lang=zh-CN|style=Feynman)是否可逆，取决于变性的方式和蛋白质本身的特性。根据Anfinsen的经典实验，[蛋白质的一级结构](@keyword=primary_structure_of_proteins|lang=zh-CN|style=Feynman)包含了其折叠成天然构象所需的全部信息。理论上，只要缓慢、温和地移除变性剂，蛋白质应该能够自发地重新折叠，这个过程称为**[复性](@keyword=renaturation|lang=zh-CN|style=Feynman)（renaturation）**。[@problem_id:2127243]

然而，在实践中，复性往往是一个低效的过程，变性常常是**不可逆的（irreversible）**。这是因为在去折叠状态下，蛋白质链上原本埋藏在内部的疏水残基暴露出来。在尝试复性时，这些暴露的[疏水表面](@keyword=hydrophobic_surfaces|lang=zh-CN|style=Feynman)很容易在不同分子之间发生非特异性的相互作用，导致**聚集（aggregation）**，形成无功能的沉淀。

不同[变性](@keyword=denaturation|lang=zh-CN|style=Feynman)方法的[可逆性](@keyword=invertibility|lang=zh-CN|style=Feynman)也存在差异。通常，由pH剧变引起的变性比由[SDS](@keyword=sodium_dodecyl_sulfate|lang=zh-CN|style=Feynman)引起的[变性](@keyword=denaturation|lang=zh-CN|style=Feynman)更容易逆转。这是因为pH值的改变主要扰乱的是蛋白质表面的[静电相互作用](@keyword=electrostatic_interactions|lang=zh-CN|style=Feynman)，而驱动折叠的主要引擎——[疏水核心](@keyword=hydrophobic_core|lang=zh-CN|style=Feynman)——在很大程度上仍保持完整。一旦pH值恢复正常，电荷分布复原，[疏水核心](@keyword=hydrophobic_core|lang=zh-CN|style=Feynman)可以有效地引导蛋白质重新折叠。相比之下，SDS分子会深度侵入并包裹疏水核心，彻底瓦解折叠的核心驱动力。即使通过[透析](@keyword=dialysis|lang=zh-CN|style=Feynman)等方法将SDS去除，已经解离的多肽链也极易发生错误折叠和聚集，很难再找到正确的折叠路径。[@problem_id:2127233]

此外，蛋白质的去折叠过程并不总是一个简单的“[两态模型](@keyword=two_state_model|lang=zh-CN|style=Feynman)”（天然态 $\leftrightarrow$ 去折叠态）。在某些温和的[变性](@keyword=denaturation|lang=zh-CN|style=Feynman)条件下（如[弱酸](@keyword=weak_acid|lang=zh-CN|style=Feynman)性pH或较低浓度的[变性](@keyword=denaturation|lang=zh-CN|style=Feynman)剂），蛋白质可以形成一种被称为**[熔球态](@keyword=molten_globule|lang=zh-CN|style=Feynman)（molten globule）**的稳定中间态。[熔球态](@keyword=molten_globule|lang=zh-CN|style=Feynman)具有以下鲜明特征，这些特征可以通过[光谱学](@keyword=optical_spectroscopy|lang=zh-CN|style=Feynman)和层析技术来表征：
*   **保留了大部分二级结构**：其[远紫外圆二色谱](@keyword=far_uv_cd|lang=zh-CN|style=Feynman)（Far-UV CD）与天然态蛋白非常相似，表明其 $\alpha$-螺旋和 $\beta$-折叠等[二级结构](@keyword=secondary_structure|lang=zh-CN|style=Feynman)单元基本完整。
*   **丧失了特定的[三级结构](@keyword=tertiary_structure|lang=zh-CN|style=Feynman)**：其[近紫外圆二色谱](@keyword=near_uv_cd|lang=zh-CN|style=Feynman)（Near-UV CD）信号几乎消失，类似于完全变性的蛋白质。这表明[芳香族氨基酸](@keyword=aromatic_amino_acids|lang=zh-CN|style=Feynman)[侧链](@keyword=side_chains|lang=zh-CN|style=Feynman)所处的刚性、不对称的微环境已经丧失，侧链堆积变得松散和动态。
*   **结构紧凑但有所膨胀**：其[流体动力学半径](@keyword=hydrodynamic_radius|lang=zh-CN|style=Feynman)（通过[体积排阻色谱法](@keyword=size_exclusion_chromatography_(sec)|lang=zh-CN|style=Feynman)测定）大于天然态，但显著小于完全去折叠的随机卷曲，表明它仍是一个紧凑的球状实体，但比天然态要“疏松”或“膨胀”。
*   **没有生物学活性**：由于精确的[三级结构](@keyword=tertiary_structure|lang=zh-CN|style=Feynman)被破坏，[熔球态](@keyword=molten_globule|lang=zh-CN|style=Feynman)通常不具有生物学功能。

[熔球态](@keyword=molten_globule|lang=zh-CN|style=Feynman)是理解[蛋白质折叠](@keyword=protein_folding|lang=zh-CN|style=Feynman)路径和稳定性机制的一个重要概念，它证明了[蛋白质结构层次](@keyword=protein_structure_hierarchy|lang=zh-CN|style=Feynman)的瓦解可以分步进行。[@problem_id:2127274]