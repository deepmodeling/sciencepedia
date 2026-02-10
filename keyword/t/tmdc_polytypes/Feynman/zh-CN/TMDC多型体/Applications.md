## 应用与跨学科联系

在探讨了控制过渡金属硫族化合物[多型体](@keyword=polytypes|lang=zh-CN|style=Feynman)结构和电子性质的基本原理之后，一个关键问题随之而来：我们能用它们来*做*什么？事实证明，我们所讨论的堆叠和对称性上的微妙差异并非仅仅是晶体学上的奇特现象。它们是一系列惊人物理现象的控制旋钮，为新技术打开了大门，并提供了一个让物理学、化学和工程学交汇的舞台。让我们踏上这段应用之旅，看看这些原子级薄层将如何改变我们的世界。

### 光与对称之舞：[光电子学](@keyword=optoelectronics|lang=zh-CN|style=Feynman)与[谷电子学](@keyword=valleytronics|lang=zh-CN|style=Feynman)

当我们用光照射这些材料时，多型现象最直接、最显著的后果之一便显现出来。您可能还记得，像MoS₂这样的材料，其单层是[直接带隙半导体](@keyword=direct_gap_semiconductor|lang=zh-CN|style=Feynman)，这意味着它能非常有效地吸收和发射光。这使其成为发光二极管 (LED)、激光器和高灵敏度光电探测器的绝佳候选者。但当我们堆叠两层形成常见的2H[多型体](@keyword=polytypes|lang=zh-CN|style=Feynman)时会发生什么呢？情况完全改变了。由于相邻层[电子轨道](@keyword=electron_orbitals|lang=zh-CN|style=Feynman)的相互作用方式，[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的特性发生转变，变为间接带隙。这种由面外轨道的[强耦合](@keyword=strong_coupling|lang=zh-CN|style=Feynman)驱动的转变，极大地降低了材料的[发光效率](@keyword=luminous_efficacy|lang=zh-CN|style=Feynman)。因此，整个[光电子学](@keyword=optoelectronics|lang=zh-CN|style=Feynman)领域都建立在[堆叠顺序](@keyword=stacking_sequence|lang=zh-CN|style=Feynman)这个简单而深刻的后果之上：要制造一个好的基于[TMDC](@keyword=tmdcs|lang=zh-CN|style=Feynman)的LED，通常必须精确地使用单层材料 [@problem_id:3022483]。

但光与层的故事变得更加错综复杂。具有三棱柱结构的单层缺乏反演[对称中心](@keyword=center_of_inversion|lang=zh-CN|style=Feynman)。然而，在2H构型中堆叠两层（其中一层相对于另一层旋转180度）则恢复了这种[反演对称性](@keyword=inversion_symmetry|lang=zh-CN|style=Feynman)。这个看似简单的几何事实具有巨大的影响。许多物理现象，包括[压电效应](@keyword=piezoelectric_effect|lang=zh-CN|style=Feynman)（受压时产生电压）和[二次谐波产生 (SHG)](@keyword=second_harmonic_generation_(shg)|lang=zh-CN|style=Feynman)，在任何具有反演对称性的材料中都是严格禁止的。SHG是一种非线性光学效应，即材料将两个特定频率的[光子](@keyword=photon|lang=zh-CN|style=Feynman)转换为一个双倍频率的[光子](@keyword=photon|lang=zh-CN|style=Feynman)——例如，将红光变为蓝光。

因此，单层MoS₂可以产生二[次谐波](@keyword=subharmonic|lang=zh-CN|style=Feynman)光，但完美堆叠的双层则不能。三层可以，但四层堆叠则不能。这种“奇偶”效应非常稳健，以至于用激光照射样品并寻找SHG的蓝色辉光，已成为识别奇数层厚度区域最可靠的方法之一 [@problem_id:2867622]。我们甚至是如何知道这些材料的结构的呢？最强大的工具之一是拉曼光谱，我们用激光探测[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的特征[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)——[声子](@keyword=phonons|lang=zh-CN|style=Feynman)。特定[多型体](@keyword=polytypes|lang=zh-CN|style=Feynman)的对称性决定了哪些[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)是“[拉曼活性](@keyword=raman_activity|lang=zh-CN|style=Feynman)”的，以及它们将如何散射[偏振光](@keyword=polarized_light|lang=zh-CN|style=Feynman)，从而为底层原子[排列](@keyword=permutation|lang=zh-CN|style=Feynman)提供了丰富的指纹信息 [@problem_id:2495746]。

单层中缺乏反演对称性开启了一种更为奇特的可能性：[谷电子学](@keyword=valleytronics|lang=zh-CN|style=Feynman)。在这些材料中，电子可以存在于两个不同的、[能量简并](@keyword=energy_degeneracy|lang=zh-CN|style=Feynman)的动量空间“谷”中，标记为 $\mathbf{K}$ 和 $\mathbf{K}'$。缺乏反演对称性产生了一个称为[贝里曲率](@keyword=berry_curvature|lang=zh-CN|style=Feynman)的量，它在动量空间中起到微小内置[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的作用，在两个谷中符号相反。这使我们能够使用圆偏振光选择性地激发 $\mathbf{K}$ 谷或 $\mathbf{K}'$ 谷中的电子。因此，谷指数可以成为一种新型的信息载体，类似于自旋电子学中的电子自旋。在对称的双层结构中，这种谷选择性响应会消失。然而，在一个漂亮的外部控制演示中，我们可以对双层施加一个垂直电场。该电场打破了[反演对称性](@keyword=inversion_symmetry|lang=zh-CN|style=Feynman)，并“复活”了谷对比物理，使我们能够随心所欲地开启和关闭这些量子特性 [@problem_id:3022387]。

### 塑造物质：相工程与可重构器件

到目前为止，我们都将[多型体](@keyword=polytypes|lang=zh-CN|style=Feynman)视为固定结构。但如果我们能说服原子按指令重新[排列](@keyword=permutation|lang=zh-CN|style=Feynman)，从一种[多型体](@keyword=polytypes|lang=zh-CN|style=Feynman)切换到另一种，会怎么样呢？这就是“相工程”的革命性概念。最著名的例子是从[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)性的2H相到金属性的1T或1T'相的转变。其核心是能量竞争的故事。在自然状态下，2H相更稳定。然而，如果我们向材料中注入高密度的额外电子，总能量平衡便开始发生变化。

原因非常微妙。2H相的[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)大多是非简并的，而1T相中相应的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)是三重简并的。这意味着1T结构能以更低的总动能成本容纳新增的电子。在某个临界电子密度下，这种电子能量的节省，加上轻微[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)畸变到1T'相带来的额外能量增益，压倒了2H相的初始稳定性。材料会自发地进行重构 [@problem_id:3022487]。

这不仅仅是一个理论构想。通过使用诸如[离子液体](@keyword=ionic_liquids|lang=zh-CN|style=Feynman)静电门控等技术——本质上是构建一个用[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)载流子淹没材料的晶体管——科学家们可以局部并可逆地触发这种[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)。通过对栅极电极进行图案化，人们可以真正地在[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)2H薄片上直接“写入”金属性的1T'导线和电路。其他控制[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)的巧妙策略包括使用纳米图案化的衬底施加精确的应变场，或通过使用[六方氮化硼](@keyword=hexagonal_boron_nitride|lang=zh-CN|style=Feynman)等其他晶体作为模板来引导特定[多型体](@keyword=polytypes|lang=zh-CN|style=Feynman)的生长。这个强大的工具箱使我们能够创造具有空间定制性质的材料，为[相变存储器](@keyword=phase_change_memory|lang=zh-CN|style=Feynman)、可重构电子器件和高效电接触开辟了道路 [@problem_id:3022364]。

### 电子的交响乐：金属[多型体](@keyword=polytypes|lang=zh-CN|style=Feynman)中的集体现象

在金属性的1T[多型体](@keyword=polytypes|lang=zh-CN|style=Feynman)中，电子现在可以自由移动，并参与一场集体的“舞蹈”，从而催生了凝聚态物理学中一些最引人入胜的现象。一个典型的例子是在像 1T-TaS₂ 这样的材料中形成电荷密度波 (CDW)。在这里，电子和[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)自发地协同作用，创造出一个新的、更大的周期性图案——一个“晶中之晶”。

随着材料冷却，它会经历一系列惊人复杂的[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)。首先，出现一个“非公度”CDW，这是一种平滑的[正弦波](@keyword=sinusoid|lang=zh-CN|style=Feynman)纹，其波长与底层原子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)并不[完美匹配](@keyword=perfect_matching|lang=zh-CN|style=Feynman)。进一步冷却后，它进入一个“近公度”相，在该相中，系统通过形成由锁定的公度结构组成的大畴区来做出妥协，这些畴区被蜂窝状的“失配”或畴壁网络隔开。最后，在低温下，它锁定到一个完全“公度”的CDW中，形成一个由13个原子组成的簇（被称为“大卫之星”）构成的美丽的 $\sqrt{13} \times \sqrt{13}$ [超晶格](@keyword=superlattices|lang=zh-CN|style=Feynman) [@problem_id:2495672]。

1T-TaS₂ 的故事甚至更为深刻。“大卫之星”CDW的形成创造了一个窄的电子[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)。被限制在这些星形簇内的电子现在能非常强烈地感受到它们之间的库仑排斥。当这个排斥能 ($U$) 大于它们通过在簇之间跳跃所能节省的能量（带宽 $W$）时，电子就会被“卡住”。它们会定域化，每个星形簇一个，并拒绝移动，从而将本应是金属的材料变成一种特殊的绝缘体，即莫特绝缘体。这是一个深刻的[多体效应](@keyword=many_body_effects|lang=zh-CN|style=Feynman)，与传统的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)绝缘体（其[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)由简单的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)周期性打开）有根本的不同。这种莫特-CD[W态](@keyword=w_state|lang=zh-CN|style=Feynman)的输运性质和光谱特征，例如其特有的[Hubbard带](@keyword=hubbard_bands|lang=zh-CN|style=Feynman)，是独一无二的，并为研究[强关联电子](@keyword=strongly_correlated_electrons|lang=zh-CN|style=Feynman)物理提供了一个丰富的平台 [@problem_id:3022416]。

### 跨学科的桥梁：催化与更清洁的未来

[TMDC多型体](@keyword=tmdc_polytypes|lang=zh-CN|style=Feynman)的影响远远超出了电子学领域，延伸到了化学和清洁能源的关键领域。我们时代的一大挑战是从水中高效生产氢燃料，这一过程被称为[析氢反应](@keyword=hydrogen_evolution_reaction|lang=zh-CN|style=Feynman) (HER)。关键是找到一种能够结合氢原子既不太强也不太弱的[催化剂](@keyword=catalyst|lang=zh-CN|style=Feynman)——这是一种由[Sabatier原理](@keyword=sabatier_s_principle|lang=zh-CN|style=Feynman)描述的“金发姑娘”条件。

常见的2H-MoS₂[多型体](@keyword=polytypes|lang=zh-CN|style=Feynman)的基面是催化惰性的。然而，自然产生的缺陷，例如缺失的硫原子，可以充当[活性位点](@keyword=active_site|lang=zh-CN|style=Feynman)。即便如此，这些原始的[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)点也并非完美；它们与氢的结合往往略微偏弱，无法达到最佳性能。在这里，我们对电子结构的理解成为理性设计[催化剂](@keyword=catalyst|lang=zh-CN|style=Feynman)的强大工具。通过用像铼（rhenium）这样能提供一个电子的元素取代邻近的钼原子，我们可以轻微提高局域金属$d$-轨道的能量。这种微小的能量移动增强了该位点与氢成键的能力，加强了相互作用，并将[吸附能](@keyword=adsorption_energy|lang=zh-CN|style=Feynman)移近理想值。相反，用吸电子的元素如铌（niobium）进行掺杂会进一步削弱结合，使[催化剂](@keyword=catalyst|lang=zh-CN|style=Feynman)性能变差。

其他策略，例如创建形成局域金属性Mo-Mo键的重构双[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)，可以在[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)处产生尖锐的态密度共振峰，从而极大地提升活性。这种通过掺杂和缺陷设计可控地工程化材料局域[电子结构](@keyword=electronic_structure|lang=zh-CN|style=Feynman)来微调其催化性能的能力，展示了凝聚态物理与化学之间美妙的协同作用，为下一代[催化剂](@keyword=catalyst|lang=zh-CN|style=Feynman)铺平了道路 [@problem_id:3022331]。

从发光体和[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)载体到可重构电路、复杂的电子相和绿色能源[催化剂](@keyword=catalyst|lang=zh-CN|style=Feynman)，[TMDC多型体](@keyword=tmdc_polytypes|lang=zh-CN|style=Feynman)的世界证明了一个思想：巨大的复杂性和实用性可以源于简单而优雅的原理。原子层如何相互堆叠这个看似微不足道的细节，开启了一个充满可能性的宇宙，而我们才刚刚开始探索这个宇宙。