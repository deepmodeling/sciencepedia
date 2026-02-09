## 应用与交叉学科联系

在前面的章节中，我们已经深入探讨了范德华（van der Waals）相互作用的物理起源，并了解了其简洁而优美的数学形式——伦纳德-琼斯（Lennard-Jones, LJ）势。我们看到，这个简单的$U(r) = 4\epsilon [(\sigma/r)^{12} - (\sigma/r)^{6}]$公式，如何通过一项排斥力和一项吸[引力](@keyword=gravitation|lang=zh-CN|style=Feynman)的微妙平衡，捕捉了中性原子间“既相互排斥又相互吸引”的普遍行为。您可能会想，这样一个看起来如此简化的[唯象模型](@keyword=phenomenological_models|lang=zh-CN|style=Feynman)，在真实而复杂的科学世界里究竟有多大用处？

答案是：它的用处超乎想象。[伦纳德-琼斯势](@keyword=lennard_jones_potential|lang=zh-CN|style=Feynman)的美妙之处，恰恰在于其简洁性与普适性的完美结合。它并非自然界的基本定律，而是一个极其有效的近似。正因如此，它成为了连接不同学科、贯穿从微观到宏观不同尺度的“通用语言”。本章，我们将开启一段探索之旅，看一看这个简单的物理思想如何在[结构生物学](@keyword=structural_biology|lang=zh-CN|style=Feynman)、药物设计、材料科学和先进的计算方法中大放异彩，展现出物理学内在的和谐与统一。

### 生命的蓝图：生物世界中的[范德华力](@keyword=van_der_waals_forces|lang=zh-CN|style=Feynman)

生命并非一堆随机堆砌的原子，而是由无数个如同精密机械般运作的分子构成的。这些分子，尤其是蛋白质，其功能的实现与其三维结构的精确性密不可分。而范德华力，正是这些结构背后的“隐形建筑师”。

#### 蛋白质的折叠与稳定

想象一下将一堆杂乱的物品装进一个行李箱。为了尽可能多地装东西，你会将它们紧密地堆叠在一起，填满所有空隙。蛋白质的折叠也遵循着类似的原则。在其非极性核心中，[氨基酸侧链](@keyword=amino_acid_side_chains|lang=zh-CN|style=Feynman)像玩俄罗斯方块一样紧密地堆积在一起。这种致密的堆积，正是为了最大化有利的[范德华吸引力](@keyword=van_der_waals_attraction|lang=zh-CN|style=Feynman)。[伦纳德-琼斯势](@keyword=lennard_jones_potential|lang=zh-CN|style=Feynman)告诉我们，当两个原子处于能量最低点的距离$r_{\min}$时，吸[引力](@keyword=gravitation|lang=zh-CN|style=Feynman)最强。蛋白质内部的原子正是通过紧[密堆积](@keyword=close_packing|lang=zh-CN|style=Feynman)，使尽可能多的原子对处于这个“最佳距离”附近。

然而，伦纳德-琼斯势的能量井并非对称的。当两个原子被压缩到比$r_{\min}$更近的距离时，由于$r^{-12}$排斥项的急剧上升，能量会迅速增加，产生巨大的“[空间位阻](@keyword=steric_hindrance|lang=zh-CN|style=Feynman)”或“ steric clash”。相比之下，将它们拉开同样的距离，能量的增加则要平缓得多。这意味着，过度压缩的代价远高于轻度分离。因此，蛋白质的折叠是一个精妙的平衡艺术：既要最大化色散吸[引力](@keyword=gravitation|lang=zh-CN|style=Feynman)（通过紧密堆积），又要不惜一切代价避免原子间的“碰撞”[@problem_id:2565616]。这种由范德华力主导的“软球”物理学，是理解蛋白质为何能形成如此致密且特异结构的关键。

人们常说“疏水效应”驱动了蛋白质的折叠，这当然没错。水分子倾向于彼此聚集，从而将[非极性侧链](@keyword=nonpolar_side_chains|lang=zh-CN|style=Feynman)“挤”到蛋白质内部。但是，疏水效应更多地是提供一种折叠的驱动力（主要是熵的贡献）。当这些[非极性侧链](@keyword=nonpolar_side_chains|lang=zh-CN|style=Feynman)进入蛋白质核心后，是什么将它们稳定地“粘合”在一起呢？答案正是[伦敦色散力](@keyword=london_dispersion_forces|lang=zh-CN|style=Feynman)。每一对非极性原子之间微弱的吸[引力](@keyword=gravitation|lang=zh-CN|style=Feynman)累加起来，为折叠好的蛋白质提供了至关重要的焓稳定化能。我们可以通过一个简化的模型来估算这种能量：每当[非极性侧链](@keyword=nonpolar_side_chains|lang=zh-CN|style=Feynman)埋藏到核心中，新形成的接触面积就对应着一定数量的新范德华作用对，从而贡献一份稳定的[结合能](@keyword=binding_energy|lang=zh-CN|style=Feynman)。反之，如果在蛋白质核心中产生一个空腔（cavity），就意味着损失了这部分宝贵的色散稳定化能，从而对蛋白质的稳定性造成惩罚[@problem_id:3869519]。

不幸的是，这种高效的堆积原则有时也会走向“黑暗面”。在一些[神经退行性疾病](@keyword=neurodegenerative_diseases|lang=zh-CN|style=Feynman)中，如[阿尔茨海默病](@keyword=alzheimer_s_disease|lang=zh-CN|style=Feynman)，特定的蛋白质片段会错误折叠并聚集成高度有序的[淀粉](@keyword=starch|lang=zh-CN|style=Feynman)样纤维（amyloid fibrils）。这些纤维的核心结构，被称为“[空间拉链](@keyword=steric_zipper|lang=zh-CN|style=Feynman)”（steric zipper），是[范德华力](@keyword=van_der_waals_forces|lang=zh-CN|style=Feynman)完美堆积的极致体现，但却带来了灾难性的后果。在这里，来自不同肽链的[氨基酸侧链](@keyword=amino_acid_side_chains|lang=zh-CN|style=Feynman)像拉链的齿一样相互啮合，形成了几乎没有空隙的致密界面，最大化了[范德华吸引力](@keyword=van_der_waals_attraction|lang=zh-CN|style=Feynman)和[氢键网络](@keyword=hydrogen_bond_network|lang=zh-CN|style=Feynman)，从而使纤维异常稳定，难以被机体清除[@problem_id:3853924]。

#### [氢键](@keyword=hydrogen_bond|lang=zh-CN|style=Feynman)的微妙之处

[氢键](@keyword=hydrogen_bond|lang=zh-CN|style=Feynman)在生物学中无处不在，通常被认为是一种特殊且具有方向性的[强相互作用](@keyword=strong_nuclear_force|lang=zh-CN|style=Feynman)。然而，在许多标准的[分子力](@keyword=molecular_forces|lang=zh-CN|style=Feynman)场中，[氢键](@keyword=hydrogen_bond|lang=zh-CN|style=Feynman)并非一个独立的能量项，而是作为一种“涌现”（emergent）的性质，由更基本的静电和[范德华相互作用](@keyword=van_der_waals_interactions|lang=zh-CN|style=Feynman)共同产生。

这是一个非常深刻且优美的思想。考虑一个典型的肽链[氢键](@keyword=hydrogen_bond|lang=zh-CN|style=Feynman)$N-H \cdots O=C$。氢原子$H$带正电，氧原子$O$带负电，它们之间存在强大的[静电吸引](@keyword=electrostatic_attraction|lang=zh-CN|style=Feynman)力。这解释了[氢键](@keyword=hydrogen_bond|lang=zh-CN|style=Feynman)的主要能量来源。但氢[键的方[向](@keyword=directional_bonding|lang=zh-CN|style=Feynman)性](@entry_id:144651)——为什么$N-H \cdots O$倾向于形成一条直线——又从何而来呢？答案就藏在范德华排斥力中。在许多[力场参数化](@keyword=force_field_parameterization|lang=zh-CN|style=Feynman)方案中，与电负性原子相连的氢原子非常小，其伦纳德-琼斯参数几乎为零。因此，$H$和$O$之间几乎没有范德华排斥。然而，作为[氢键供体](@keyword=hydrogen_bond_donor|lang=zh-CN|style=Feynman)的氮原子$N$和作为受体的氧原子$O$都有不可忽略的[范德华半径](@keyword=van_der_waals_radius|lang=zh-CN|style=Feynman)。如果[氢键](@keyword=hydrogen_bond|lang=zh-CN|style=Feynman)弯曲，$N$和$O$的距离就会变近，从而进入[伦纳德-琼斯势](@keyword=lennard_jones_potential|lang=zh-CN|style=Feynman)的排斥区，导致能量迅速升高。因此，系统为了最小化这两个“大原子”之间的范德华排斥能，会自发地采取线性的几何构型[@problem_id:5254453]。这再次证明了，看似复杂的生物学现象，其背后可能只是几条简单的物理规则在起作用。

#### [超越标准模型](@keyword=beyond_the_standard_model|lang=zh-CN|style=Feynman)：前沿与局限

当然，我们这个简单的模型并非万能。一个典型的例子是[卤键](@keyword=halogen_bonding|lang=zh-CN|style=Feynman)（halogen bond），这是一种在药物设计中日益重要的[非共价相互作用](@keyword=noncovalent_interactions|lang=zh-CN|style=Feynman)。实验发现，当一个卤原子（如$Cl, Br, I$）与一个[路易斯碱](@keyword=lewis_base|lang=zh-CN|style=Feynman)（如羰基氧）相互作用时，会表现出强烈的方向性，倾向于形成线性构型。其物理根源在于卤原子周围电子云的各向异性分布：在[共价键](@keyword=covalent_bond|lang=zh-CN|style=Feynman)的延长线上，电子云密度较低，形成一个带正电的区域，被称为“$\sigma$-空洞”（sigma-hole）。

然而，我们标准的、各项同性的伦纳-琼斯势加上一个位于原子中心的[点电荷](@keyword=point_charges|lang=zh-CN|style=Feynman)模型，完全无法描述这种现象。因为无论是[范德华力](@keyword=van_der_waals_forces|lang=zh-CN|style=Feynman)还是[点电荷](@keyword=point_charges|lang=zh-CN|style=Feynman)[静电力](@keyword=electrostatic_forces|lang=zh-CN|style=Feynman)，在这个模型中都是球对称的。如果卤原子被赋予一个通常的负电荷，它与带负电的氧原子之间在所有方向上都只会表现为排斥。

这恰恰体现了科学的进步方式：认识到模型的局限性，并发展出更完善的理论。为了解决这个问题，研究人员提出了多种方案，例如，在卤原子[共价键](@keyword=covalent_bond|lang=zh-CN|style=Feynman)的延长线上放置一个带正电的“虚拟位点”（virtual site）来模拟$\sigma$-空洞；或者使用更复杂的分布式[多极矩](@keyword=multipole_moments|lang=zh-CN|style=Feynman)模型来描述非球形的[电荷分布](@keyword=charge_distribution|lang=zh-CN|style=Feynman)；或者引入极化效应，让原子的[电荷分布](@keyword=charge_distribution|lang=zh-CN|style=Feynman)能够响应环境电场而变化[@problem_id:3869539]。这些前沿的[力场](@keyword=force_field|lang=zh-CN|style=Feynman)发展，正是为了让我们对分子世界的描述更加精确，也再次提醒我们，任何物理模型都只是对真实世界特定层面的近似。

### 盒子里的世界：模拟物质的宏观性质

[伦纳德-琼斯势](@keyword=lennard_jones_potential|lang=zh-CN|style=Feynman)不仅能描述生物大分子内部的精细结构，还能解释物质的宏观性质。通过在计算机中构建一个包含成千上万个遵循LJ势相互作用的粒子的“盒子”，我们可以模拟液体、固体和气体的行为。

#### 从微观规则到宏观性质

以最常见也最重要的液体——水为例。不同的[水模型](@keyword=water_models|lang=zh-CN|style=Feynman)（如[TIP3P](@keyword=tip3p|lang=zh-CN|style=Feynman), [TIP4P](@keyword=tip4p|lang=zh-CN|style=Feynman)/2005等）在计算机模拟中被广泛使用。这些模型之间的一个关键区别，就在于赋予氧原子的伦纳德-琼斯参数$\epsilon$和$\sigma$的微小差异。$\sigma$决定了水分子的“有效尺寸”，而$\epsilon$决定了它们之间吸[引力](@keyword=gravitation|lang=zh-CN|style=Feynman)的强弱。

实验表明，仅仅对这两个参数进行微调，就能显著改变模拟出的水的宏观性质。例如，从[TIP3P](@keyword=tip3p|lang=zh-CN|style=Feynman)模型变为[TIP4P](@keyword=tip4p|lang=zh-CN|style=Feynman)/2005模型，氧原子的$\epsilon$值增大了约$20\%$, $\sigma$值也略有增加。这微小的改变，导致了更强的分子间吸[引力](@keyword=gravitation|lang=zh-CN|style=Feynman)，使得模拟出的水分子堆积得更紧密，从而得到了更准确的液体密度。同时，这种更强的吸[引力](@keyword=gravitation|lang=zh-CN|style=Feynman)也使得水分子的第一[配位层](@keyword=coordination_sphere|lang=zh-CN|style=Feynman)结构更加清晰，这在径向分布函数$g(r)$的第一峰变得更高更尖锐上得到了体现[@problem_id:3869555]。这种从微观参数到宏观性质的直接联系，是分子模拟的魅力所在，也彰显了伦纳德-琼斯势作为构建物质模型基石的强大能力。

#### [粗粒化](@keyword=coarse_graining|lang=zh-CN|style=Feynman)的艺术

有时，我们并不关心系统中每个原子的细节。例如，在研究[细胞膜](@keyword=cell_membrane|lang=zh-CN|style=Feynman)的大尺度形变或蛋白质的自组装时，我们更关心的是分子作为一个整体的行为。这时，就可以采用“[粗粒化](@keyword=coarse_graining|lang=zh-CN|style=Feynman)”（coarse-graining）的策略，将一组原子（如一个[氨基酸侧链](@keyword=amino_acid_side_chains|lang=zh-CN|style=Feynman)或一个脂质分子尾巴）打包成一个单一的“珠子”（bead）。

那么，这些“珠子”之间的相互作用该如何描述呢？[伦纳德-琼斯势](@keyword=lennard_jones_potential|lang=zh-CN|style=Feynman)再次成为了理想的选择。但问题是，我们如何为这些虚构的珠子确定合适的$\epsilon$和$\sigma$参数呢？这里就涉及到一个“逆向问题”（inverse problem）：我们不是用势能函数去预测结构，而是从已知的结构信息中反推出势能函数。

一个强大的工具是“[平均力势](@keyword=potential_of_mean_force|lang=zh-CN|style=Feynman)”（potential of mean force, PMF）。统计力学告诉我们，两个粒子在液体中的径向分布函数$g(r)$与它们之间的[平均力势](@keyword=potential_of_mean_force|lang=zh-CN|style=Feynman)$W(r)$存在直接关系：$W(r) = -k_B T \ln g(r)$。在很多情况下，我们可以近似认为这个平均力势就是粒子间的有效相互作用势。因此，通过分析全原子模拟或实验得到的$g(r)$，我们可以直接“读取”出[粗粒化](@keyword=coarse_graining|lang=zh-CN|style=Feynman)珠子间的有效相互作用：$g(r)$第一峰的位置近似对应于LJ势的能量最低点$r_{\min}$，从而确定$\sigma$；而峰的高度则反映了能量井的深度$\epsilon$[@problem_id:3869556]。这种从结构到能量的映射，是多尺度模拟领域的核心思想之一，它允许我们在不同细节层次上对复杂系统进行建模。

#### 混合物与界面的挑战

当系统变得更复杂，例如包含多种不同类型的分子，或者存在不同相之间的界面（如脂膜与水），我们需要更加小心地处理[范德华相互作用](@keyword=van_der_waals_interactions|lang=zh-CN|style=Feynman)。

在模拟混合物时，我们知道同种原子间的LJ参数（如$\sigma_{AA}, \epsilon_{AA}$），但如何确定不同种类原子间（如$A-B$）的参数$\sigma_{AB}$和$\epsilon_{AB}$呢？最简单直观的方法是采用“混合规则”（combining rules）。例如，洛伦兹-贝特洛（Lorentz-Berthelot）规则使用算术平均来混合尺寸（$\sigma_{AB} = (\sigma_A + \sigma_B)/2$），用几何平均来混合能量（$\epsilon_{AB} = \sqrt{\epsilon_A \epsilon_B}$）。然而，更深入的物理理论，如[伦敦色散](@keyword=london_dispersion|lang=zh-CN|style=Feynman)理论，为我们提供了更严格的约束。为了更好地满足这些物理约束，研究者发展出了更复杂的混合规则，如Kong规则或[Waldman-Hagler规则](@keyword=waldman_hagler_rules|lang=zh-CN|style=Feynman)。这些不同的规则会对模拟出的混合物性质（如[第二维里系数](@keyword=second_virial_coefficient|lang=zh-CN|style=Feynman)）产生可观测的影响，选择哪种规则本身就是[力场](@keyword=force_field|lang=zh-CN|style=Feynman)开发中的一个重要课题[@problem_id:3869550] [@problem_id:3869579]。

当模拟一个不均匀的系统，如水中的[生物膜](@keyword=biological_membranes|lang=zh-CN|style=Feynman)时，另一个挑战来自于[范德华力](@keyword=van_der_waals_forces|lang=zh-CN|style=Feynman)的“长程”部分。由于计算资源的限制，我们通常只计算一个[截断半径](@keyword=cutoff_radius|lang=zh-CN|style=Feynman)$r_c$以内的相互作用。对于均匀的液体，我们可以通过一个简单的数学公式（长程[色散校正](@keyword=dispersion_correction|lang=zh-CN|style=Feynman), LRC）来估算并补偿被截断掉的能量和压力贡献。然而，这个校正公式假设系统在[截断半径](@keyword=cutoff_radius|lang=zh-CN|style=Feynman)之外是均匀的。对于一个包含脂膜、水和真空层的非均匀体系，这个假设显然不成立，从而导致表面张力等界面性质的计算产生严重的人为误差。为了解决这个问题，必须采用更先进的、能够处理非均匀性的方法，例如专门为平板系统设计的各向异性校正方案，或者通过格点求和（如LJ-PME）来精确计算完整的[长程相互作用](@keyword=long_range_interactions|lang=zh-CN|style=Feynman)，就像处理[静电相互作用](@keyword=electrostatic_interactions|lang=zh-CN|style=Feynman)一样[@problem_-id:3857706]。

### 跨越尺度：从量子到经典，从原子到材料

伦纳德-琼斯势的应用远不止于生物和[软物质模拟](@keyword=soft_matter_simulation|lang=zh-CN|style=Feynman)，它在材料科学和连接量子与经典世界的[混合方法](@keyword=mixed_methods|lang=zh-CN|style=Feynman)中也扮演着核心角色。

#### 石墨的层间结合

石墨烯是单层的碳原子构成的[二维材料](@keyword=2d_materials|lang=zh-CN|style=Feynman)，而我们日常接触的石墨则是无数层石墨烯通过微弱的范德华力堆叠而成的。每一层内部的碳原子由强大的[共价键](@keyword=covalent_bond|lang=zh-CN|style=Feynman)连接，而层与层之间的结[合力](@keyword=net_force|lang=zh-CN|style=Feynman)则完全来自于范德华吸引。

我们可以用伦纳德-琼斯势来计算这个层间结合能。这是一个非常优美的物理学问题：将一个碳原子与另一片无限大的石墨烯平板上所有碳原子之间的$r^{-12} - r^{-6}$成对势进行积分。计算结果表明，这个积分最终会得到一个与层间距$d$相关的$d^{-10} - d^{-4}$形式的[势能函数](@keyword=potential_energy_functions|lang=zh-CN|style=Feynman)。这个简单的推导，完美地展示了微观的成对相互作用规律是如何通[过积分](@keyword=over_integration|lang=zh-CN|style=Feynman)“放大”成为宏观材料性质的[@problem_id:3737814]。它告诉我们，铅笔芯之所以能写字（石墨层间可以轻易滑脱），其背后的物理根源与蛋白质内部的原子堆积是相同的。

#### 混合模型：QM/MM

在某些情况下，例如模拟酶催化反应时，[反应中心](@keyword=reaction_centers|lang=zh-CN|style=Feynman)的化学键断裂与形成必须用量子力学（QM）来精确描述。但整个酶和周围的溶剂分子数量庞大，全部用QM计算是不现实的。于是，科学家们发明了[量子力学/分子力学](@keyword=quantum_mechanics_molecular_mechanics|lang=zh-CN|style=Feynman)（QM/MM）的[混合方法](@keyword=mixed_methods|lang=zh-CN|style=Feynman)。

其核心思想是，将系统划分为两部分：一个小的、关键的QM区域（如酶的活性位点）和一个大的、作为环境的MM区域。MM区域就用我们熟悉的经典力场（LJ势+[库仑势](@keyword=coulomb_potential|lang=zh-CN|style=Feynman)）来描述。这两个区域之间并非彼此隔绝，而是通过能量项相互“沟通”。MM区域的原子[点电荷](@keyword=point_charges|lang=zh-CN|style=Feynman)会产生一个[静电场](@keyword=electrostatic_field|lang=zh-CN|style=Feynman)，从而影响QM区域的电子云分布（即“[静电嵌入](@keyword=electrostatic_embedding|lang=zh-CN|style=Feynman)”）。同时，MM区域的原子也通过[范德华力](@keyword=van_der_waals_forces|lang=zh-CN|style=Feynman)与QM区域的原子相互作用，为QM区域提供一个真实的、具有[空间排斥](@keyword=steric_repulsion|lang=zh-CN|style=Feynman)和色散吸引的物理环境[@problem_id:2664100]。LJ势在这里充当了连接量子世界与经典世界的桥梁。

#### [计算炼金术](@keyword=computational_alchemy|lang=zh-CN|style=Feynman)的艺术

预测药物分子与靶点蛋白的[结合亲和力](@keyword=binding_affinity|lang=zh-CN|style=Feynman)，是[计算化学](@keyword=computational_chemistry|lang=zh-CN|style=Feynman)中的“圣杯”之一。一种强大的方法被称为“[炼金术自由能计算](@keyword=alchemical_free_energy_calculations|lang=zh-CN|style=Feynman)”（alchemical free energy calculation）。其思想是在计算机中将一个分子“缓慢”地、可逆地转变为另一个分子，或者将一个分子在溶剂中“变没”，再在蛋白口袋中“变出来”，然后通过统计力学计算这个非物理过程的自由能变化，从而得到结合自由能。

在这个“炼金”过程中，当一个原子被逐渐“变没”时（通过一个耦合参数$\lambda$从1变到0），它的[范德华相互作用](@keyword=van_der_waals_interactions|lang=zh-CN|style=Feynman)也随之减弱。如果我们天真地用$\lambda$线性地缩放整个LJ势，当$\lambda$趋近于0时，就会遇到一个被称为“终点灾难”（end-point catastrophe）的严重问题。因为当$\lambda$很小时，LJ势的排斥墙变得非常“软”，模拟中的其他原子就可能与这个正在消失的原子发生灾难性的碰撞（$r \to 0$）。虽然碰撞本身能量不高（因为被$\lambda$缩放了），但我们用来计算自由能的某个量（能量对$\lambda$的导数）却会在此时发生数值爆炸，导致计算失败。这个问题的根源，正是LJ势中那个陡峭的$r^{-12}$项。为了解决这个问题，研究人员设计了巧妙的“[软核势](@keyword=soft_core_potentials|lang=zh-CN|style=Feynman)”（soft-core potential），它修改了$\lambda$趋近于0时的[势能函数](@keyword=potential_energy_functions|lang=zh-CN|style=Feynman)形式，避免了奇异点的出现，从而使得“炼金术”得以顺利进行[@problem_id:3869517]。这再次说明，即使是使用一个简单的模型，也需要深刻的物理洞察力和数学技巧。

### 结语

回顾我们的旅程，从蛋白质的精[密堆积](@keyword=close_packing|lang=zh-CN|style=Feynman)，到水的宏观性质，再到石墨的层间结合；从模拟方法的精妙技巧，到连接量子与经典的混合模型。我们看到，伦纳德-琼斯势这个看似简单的公式，以其惊人的普适性，为我们理解和模拟从生命到材料的广阔世界提供了统一的语言。

它提醒我们，物理学模型的价值不仅在于其精确性，更在于其解释力和启发性。与那些从海量数据中“学习”出来的、高度依赖于训练环境的“知识库势”不同，一个基于物理原理的模型（即使是简化的）具有更强的可移植性和适应性。当我们需要探索一个全新的环境，例如设计一个能在非[极性溶剂](@keyword=polar_solvent|lang=zh-CN|style=Feynman)中工作的酶时，一个可以调整物理参数（如介[电常数](@keyword=permittivity_of_free_space|lang=zh-CN|style=Feynman)）的物理模型，远比一个被“锁死”在水环境数据中的[统计模型](@keyword=statistical_models|lang=zh-CN|style=Feynman)更为可靠[@problem_id:2027324]。

伦纳德-琼斯势或许不是描述原子间相互作用的最终答案，但它无疑是物理学、化学和生物学工具箱中最美丽、最强大、最富有启发性的工具之一。它完美地诠释了科学的精髓：用最简单的思想，解释最丰富的世界。