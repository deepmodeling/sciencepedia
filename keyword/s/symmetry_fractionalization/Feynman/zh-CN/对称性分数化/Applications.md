## 应用与跨学科联系

在我们迄今的旅程中，我们探索了[对称性分数化](@keyword=symmetry_fractionalization|lang=zh-CN|style=Feynman)这种奇特而美妙的逻辑——即量子材料内部的基本激发，或称任意子，可以以一种被修改的、“分数的”方式体验自然的基要对称性。自由空间中的一个电子知道，将它旋转 $360$ 度会使其回到初始状态。但量子自旋液体深处的一个[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)可能会发现，一次完整的旋转会给它留下一个负号，仿佛它只被转了一半。这似乎仅仅是一个奇闻，是物理学家黑板上的一个怪癖。但事实远非如此。

本节旨在探讨这种现实的哈哈镜版本在何处展露其迹。[对称性分数化](@keyword=symmetry_fractionalization|lang=zh-CN|style=Feynman)的原理不仅仅是用来分类奇异可能性的工具，它也是审视真实世界的锐利透镜。它使我们能为一些最神秘的量子物相提供指纹，为设计新[物相](@keyword=phases_of_matter|lang=zh-CN|style=Feynman)提供配方，重新定义我们对“金属”等熟悉概念的理解，甚至将物理学的边界推向新的领域，如时间本身的有序化。

### 为量子荒野提供指纹
想象一下，作为一名地图绘制者，正在绘制一块新发现的大陆。你不会只描绘海岸线；你还想了解气候、植物和动物。在凝聚态物理学中，我们是广阔量子相大陆的探索者。[对称性分数化](@keyword=symmetry_fractionalization|lang=zh-CN|style=Feynman)提供了表征栖息在这些奇异景观中的独特“动物”——任意子——的工具。

#### 任意子的内部罗盘：[晶体对称性](@keyword=crystal_symmetry|lang=zh-CN|style=Feynman)

这些思想最直接的应用是在[量子自旋液体](@keyword=quantum_spin_liquids|lang=zh-CN|style=Feynman)的研究中。[量子自旋液体](@keyword=quantum_spin_liquids|lang=zh-CN|style=Feynman)是一种物质状态，其中电子的磁矩即使在绝对零度也拒绝有序化，而是形成一个深度纠缠、涨落的“液体”。为了区分一种[自旋液体](@keyword=spin_liquids|lang=zh-CN|style=Feynman)与另一种，我们需要知道其任意子激发的性质。一个强有力的方法是观察它们如何响应[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)本身的对称性。

考虑一个存在于 kagome [晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)（一种由共角三角形构成的美丽网络）上的维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)——一种磁通任意子。如果我们在一个六边形的中心“捕获”一个维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)，并将整个晶体旋转 $360$ 度，常识告诉我们维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)应该回到其初始状态。然而，[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)的代数规则预示着某种更为奇异的事情。在某些 $\mathbb{Z}_2$ [自旋液体](@keyword=spin_liquids|lang=zh-CN|style=Feynman)中，将此旋转执行六次（总共 $360$ 度）会给维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)带来一个 $-1$ 的相位[@problem_id:3012576]。就好像这个维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)相对于[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)旋转是一种[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)！这不是魔法，而是自洽性的深刻结果。维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)奇特的旋转性质与其如何经历平移紧密相连。因为维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)从背景[自旋液体](@keyword=spin_liquids|lang=zh-CN|style=Feynman)中看到了一个有效磁场，所以先沿 x 轴移动再沿 y 轴移动，与以相反顺序移动是不同的。这种平移的[非对易性](@keyword=non_commutativity|lang=zh-CN|style=Feynman)被印刻在其旋转性质上，为该物相提供了一个清晰、可计算的指纹。我们甚至可以通过将[自旋液体](@keyword=spin_liquids|lang=zh-CN|style=Feynman)想象成自旋单态对或“二聚体”的共振海洋来发展一个更微观的图像。维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)对应于这种模式中的一个扰动，其独特的对称性质可以通过观察这些二聚体模式如何在其周围变换和共振来诊断[@problem_id:3013830]。

#### 分数化的语法：对称性缺陷与融合规则

当我们考虑其他类型的对称性时，比如一个简单的翻转系统中所有自旋的全局操作，故事就变得更加丰富了。[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)提供了一套严格的“语法”，规定了任意子如何携带这些对称性荷。例如，如果我们知道一个 $\epsilon$ [任意子](@keyword=anyons|lang=zh-CN|style=Feynman)是电性 $e$ 任意子和磁性 $m$ 任意子的[束缚态](@keyword=bound_states|lang=zh-CN|style=Feynman)（$\epsilon = e \times m$），那么它的对称性荷就由其组分的荷所确定[@problem_id:1202594]。

探测这些荷的一个强有力的方法是创建一个“对称性缺陷”。想象一下，将材料切开，对切口一侧的所有物体施加对称性操作，然后将其缝合。切口所在的接缝是一种拓扑[线缺陷](@keyword=line_defects|lang=zh-CN|style=Feynman)。如果我们接着取一个[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)，并让它环绕这条线运动，它的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)会获得一个相位。这个类 Aharonov-Bohm 相位是对任意子分数对称荷的直接测量。

有时，对称性的作用甚至更为戏剧性。对称性操作可能不仅仅是给[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)一个相位，它实际上可以将一种类型的[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)嬗变为另一种——例如，将一个 $e$ 任意子变成一个 $m$ 任意子。在这种情况下，对称性缺陷线的端点本身就像一种新型的拓扑粒子。将一个 $e$ [任意子](@keyword=anyons|lang=zh-CN|style=Feynman)与这个缺陷端点融合，可能会产生一个 $m$ [任意子](@keyword=anyons|lang=zh-CN|style=Feynman)，这是对称性变换的物理体现[@problem_id:178663]。这些规则并非任意的；它们形成了一个自洽的数学结构，使我们能够对所有可能的对称性与拓扑交织的方式进行分类。

#### 从理论到测量：眼见为实

我们如何确定这些奇异的性质是真实存在的，而不仅仅是理论上的幻想？物理学家们已经设计出巧妙的方法——无论是理论上的还是潜在的实验方法——来探测[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)的特征。

一个聪明的想法是把我们的[二维材料](@keyword=2d_materials|lang=zh-CN|style=Feynman)薄片卷成一个环面。在具有[拓扑序](@keyword=topological_order|lang=zh-CN|style=Feynman)的相中，[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)不是唯一的；它具有内在的简并度。对于 $\mathbb{Z}_2$ [自旋液体](@keyword=spin_liquids|lang=zh-CN|style=Feynman)，有四个简并的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)，对应于是否有维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)穿过环面的“甜甜圈孔”。一个卓越的见解是，我们可以通过在形成环面时在边界条件中引入一个*扭曲*——例如，在环绕时将[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)平移一个[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)——来探测维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)的分数化模式。这种对称性扭曲就像一个缠绕在环面上的缺陷线。它影响了维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)在环面周围进行[量子隧穿](@keyword=quantum_mechanical_tunneling|lang=zh-CN|style=Feynman)的能力，以一种非常特定的方式解除了四重简并。通过测量[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的有限尺寸能级分裂，原则上可以读出维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)的[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)量子数[@problem_id:3013873]。

一个更现代的方法来自量子信息领域。[拓扑相](@keyword=topological_phases|lang=zh-CN|style=Feynman)的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)是一张长程纠缠的织锦。如果我们将材料切成两半，两半之间的纠缠将包含拓扑序的完整全息印记。我们可以通过想象“穿过”一个对称性通量量子（比如说，一个守恒自旋旋转的 $2\pi$ 通量）来探测这一点，此时系统被塑造成一个圆柱体。这个过程改变了切口处的纠缠，一个称为“纠缠极化”的量的总变化是量子化的。令人惊讶的是，这个量子化的值直接揭示了维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)所携带的分数荷[@problem_id:3012606]。携带半个单位自旋荷的维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)会产生 $\pi$ 的极化变化，而中性维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)则为零。这在对称性的抽象代数和[量子纠缠](@keyword=quantum_entanglement|lang=zh-CN|style=Feynman)的具体、可测量的结构之间提供了一个深刻的联系。

### 创造性破坏：重塑物质与概念

[对称性分数化](@keyword=symmetry_fractionalization|lang=zh-CN|style=Feynman)不仅仅是一种描述性工具，它也是一种创造性工具。它为一个物相如何转变为另一个[物相](@keyword=phases_of_matter|lang=zh-CN|style=Feynman)提供了蓝图，并为我们描述那些我们曾以为已经理解的物相提供了新的语言。

#### 熔化一个[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)态

如果我们取一个量子自旋液体并将其“熔化”，会发生什么？答案在于其分数化任意子的性质。考虑一个[自旋液体](@keyword=spin_liquids|lang=zh-CN|style=Feynman)，其中维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)携带一种分数化的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)动量，这是它们投影平移代数（$T_x T_y = -T_y T_x$）的直接结果。如果我们调整一个参数（如压力或外场）使这些维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)的产生在能量上变得廉价，它们最终会“凝聚”，就像水蒸气凝结成液体一样。

但是，因为这些凝聚的维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)携带动量，它们的凝聚会自发地破坏[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的[平移对称性](@keyword=translational_symmetry|lang=zh-CN|style=Feynman)。系统会冻结成一种有序的自旋单态晶体模式，称为[价键固体](@keyword=valence_bond_solid|lang=zh-CN|style=Feynman)（VBS）。同时，磁通（维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)）的凝聚会引发一种演生的[希格斯机制](@keyword=higgs_mechanism|lang=zh-CN|style=Feynman)：它会禁闭与维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)有非平凡[编织统计](@keyword=braiding_statistics|lang=zh-CN|style=Feynman)的电性[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)。先前[退禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)的分数自旋-1/2自旋子现在被锁在整数自旋的激发内部。这个被称为[退禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)[量子临界点](@keyword=quantum_critical_point|lang=zh-CN|style=Feynman)的优美机制，展示了一个从奇异拓扑液体到更常规有序固体的转变完全由凝聚的[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)的[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)性质所支配 [@problem_id:3012627]。

#### 炼金术士的梦想：规范化对称性

一种更强大的创造工具是“规范化”。这是一个理论过程，我们将一个全局对称性（一个在任何地方都同样适用的规则）提升为一个局域对称性（一个可以在每个点独立遵循、由新的[力场](@keyword=force_field|lang=zh-CN|style=Feynman)介导的规则）。在一个普通系统中规范化一个对称性会得到一个[规范理论](@keyword=gauge_theory|lang=zh-CN|style=Feynman)，比如[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)。但在一个对称性已经*分数化*的系统中进行规范化，则会引发一种量子炼金术。

所产生的相是一个新的[拓扑序](@keyword=topological_order|lang=zh-CN|style=Feynman)，其中原始的[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)已经嬗变并与新规范场的通量结合，形成了一套全新的激发[@problem_id:2990908]。例如，人们可以从著名的[斐波那契任意子](@keyword=fibonacci_anyons|lang=zh-CN|style=Feynman)——[容错量子计算](@keyword=fault_tolerant_quantum_computing|lang=zh-CN|style=Feynman)的关键资源——开始，并用一个简单的、在非平凡[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)上[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)的 $\mathbb{Z}_2$ 对称性来丰富它们。规范化这个 $\mathbb{Z}_2$ 对称性会得到一个具有更多[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)类型的更复杂的理论，这个过程可以被精确计算和分类[@problem_id:140739]。这为设计具有所需性质的新型[拓扑相](@keyword=topological_phases|lang=zh-CN|style=Feynman)以用于[量子信息处理](@keyword=quantum_information_processing|lang=zh-CN|style=Feynman)开辟了一条诱人的途径。

#### 重新定义“金属”

或许[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)最深刻的后果之一是它迫使我们重新思考金属的定义。凝聚态物理学的一个里程碑式成果——Luttinger 定理——为传统金属提供了一个严格的规则：[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)——[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中移动电子的海洋——的体积与电子总数成正比。

现在，考虑一个“[分数化费米液体](@keyword=fractionalized_fermi_liquid|lang=zh-CN|style=Feynman)”（FL*），在这个相中，电子本身分裂成一个荷子（携带[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)）和一个自旋子（携带自旋），它们由一个演生规范场耦合。人们可以通过一个思想实验来检验 Luttinger 定理：将一个[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)穿过一个金属环面。规范不变性要求这必须使系统的[总动量](@keyword=total_linear_momentum|lang=zh-CN|style=Feynman)改变一个与电子总数成比例的量。在正常金属中，这个动量由费米面上的电子吸收，从而强制执行该定理。

但在 FL* 相中，可能会发生新的情况。穿过的通量也可以激发理论的拓扑部分——例如，通过创建一个维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)。如果这个维[相子](@keyword=phasons|lang=zh-CN|style=Feynman)携带自己的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)动量（[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)的标志！），它可以吸收一部分来自通量穿透的动量。这意味着电子[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)不再是唯一负责动量平衡的。其后果是惊人的：[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)可以是“小的”，只计算了电子的一部分（例如，添加到绝缘体中的掺杂剂密度），而其余电子的动量则“隐藏”在底层的拓扑液体中。这种对传统 Luttinger 定理的违背并非物理学的失败，而是一个更深层次、分数化现实的标志。它是解释从[重费米子系统](@keyword=heavy_fermion_systems_2|lang=zh-CN|style=Feynman)到高温超导体等材料神秘性质的主要[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)之一[@problem_id:3002360]。

### 超越固态：一种新的时间

[对称性分数化](@keyword=symmetry_fractionalization|lang=zh-CN|style=Feynman)的影响甚至超出了[平衡态](@keyword=equilibrium_states|lang=zh-CN|style=Feynman)材料的领域，延伸到了动态的、非平衡的世界。它的原理现在正被用来理解现代物理学中最令人匪夷所思的概念之一：[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)。

[离散时间晶体](@keyword=discrete_time_crystals|lang=zh-CN|style=Feynman)是一种自发破坏[周期性驱动](@keyword=periodic_driving|lang=zh-CN|style=Feynman)的[时间平移对称性](@keyword=time_translation_symmetry_2|lang=zh-CN|style=Feynman)的物质相。如果你以周期 $T$ “踢”系统，它会以周期 $2T$、$3T$ 或更长的时间响应，就像空间晶体破坏连续[平移对称性](@keyword=translational_symmetry|lang=zh-CN|style=Feynman)一样。挑战在于，这样的系统不断被注入能量，并倾向于加热到一个无特征的、无限温度的状态。如此精巧的亚谐波序如何能够存活？

答案再次可以在拓扑和[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)中找到。考虑一个[一维系统](@keyword=one_dimensional_systems|lang=zh-CN|style=Feynman)，它在时间上被[周期性驱动](@keyword=periodic_driving|lang=zh-CN|style=Feynman)，以至于实现了一个“Floquet”对称性保护拓拓扑（SPT）相。这些是我们从[平衡态](@keyword=equilibrium_states|lang=zh-CN|style=Feynman)中得知的拓扑绝缘体的动态类似物。一个非平凡 Floquet SPT 相的关键特征是，对称性在其边缘处发生了[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)。对于一个具有[守恒荷](@keyword=conserved_charges|lang=zh-CN|style=Feynman)的系统，这可能意味着在每个驱动周期，一个有效电荷 $1/2$ 被泵送到边缘。这个分数化的边缘[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)产生了一个稳健的边缘模式，其量子相位以一种特殊的方式演化。具体来说，它有一个 $\pi/T$ 的[准能量](@keyword=quasi_energy|lang=zh-CN|style=Feynman)，意味着它的状态在每个驱动周期后都会乘以 $-1$。

这个受保护的 $\pi/T$ 模式是[倍周期](@keyword=period_doubling|lang=zh-CN|style=Feynman)[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)的完美构件。如果系统还自发地破坏了与此模式相关的对称性，那么相应的序参量将自然地在每个周期翻转其符号，以恰好是驱动周期两倍的周期[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。这种不可思议的时间有序性的稳定性是边缘[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)的直接结果，它保护了 $\pi/T$ 模式免受扰动。最初为理解静态[量子物质](@keyword=quantum_matter|lang=zh-CN|style=Feynman)而发展的[对称性分数化](@keyword=symmetry_fractionalization|lang=zh-CN|style=Feynman)的抽象机制，为稳定一种有史以来最奇异的非平衡物相提供了关键[@problem_id:3021714]。

从晶体中的静态图案到[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)的节律性舞蹈，[对称性分数化](@keyword=symmetry_fractionalization|lang=zh-CN|style=Feynman)的原理揭示了一个物理学基本规则变得灵活且充满新可能性的宇宙。它证明了演生的力量，展示了简单的成分在复杂的量子汤中汇集时，如何能产生一个拥有自身奇特、美丽且极其新颖法则的世界。