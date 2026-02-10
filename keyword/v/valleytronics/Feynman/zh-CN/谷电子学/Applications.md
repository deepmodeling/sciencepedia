## 应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系

现在我们已经熟悉了电子谷的奇妙世界，我们可能会忍不住问一个非常实际的问题：那又怎样？知道某些晶体中的电子生活在这些分离的[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)“谷”中有什么好处？这是一个合理的问题，而答案正是将这个领域从科学奇观推向技术前沿的动力所在。在学习了这场新游戏的规则——如何创建、操控和读取电子的谷态之后——我们现在准备看看我们能玩出什么精彩的游戏。[谷电子学](@keyword=valleytronics|lang=zh-CN|style=Feynman)的应用不仅仅是对现有技术的增量改进；它们预示着处理、存储和通信信息的全新方式，连接了从电子学和光学到拓扑学和[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)等不同领域。

### 谷晶体管与逻辑

现代电子学的核心是晶体管，一种控制[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)流动的开关。[谷电子学](@keyword=valleytronics|lang=zh-CN|style=Feynman)的梦想是构建一个控制谷[量子数](@keyword=quantum_numbers|lang=zh-CN|style=Feynman)流动的“谷晶体管”。它不再仅仅基于[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的“开”和“关”，我们可以拥有基于谷的“K”和“K'”。要构建这样的设备，我们首先需要一个“谷滤波器”——一个可以分离来自K谷和K'谷的电子的门。

怎么可能构建这样的东西呢？大自然的精妙之处提供了一种方法。正如我们所学，能量-动量关系$E(\mathbf{k})$的景观并非总是完全对称的。电子的有效质量可以是各向异性的；也就是说，电子可能会发现在一个方向上[加速比](@keyword=speedup|lang=zh-CN|style=Feynman)在另一个方向上“更容易”。在某些材料中，K谷和K'谷的质量各向异性“椭圆”的取向不同。想象一个谷，其中电子沿x轴质量轻，沿y轴质量重，而另一个谷则相反。

如果我们在x轴方向施加电场，来自第一个谷的电子，由于在该方向上更轻，会更容易响应并对电流做出更大贡献。*瞧*！我们得到了一个“谷极化”的电流。通过巧妙地选择我们沟道的方向，我们可以优先过滤一个谷。这一原理可以被进一步增强；通过对晶体施加机械应变，我们可以扭曲[能量景观](@keyword=energy_landscape|lang=zh-CN|style=Feynman)，夸大质量各向异性，使我们的谷滤波器更加高效[@problem_id:2482609]。在一个更量子力学的视角下，甚至可以设计一个薄的势垒。来自沿势垒方向[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)较轻的谷的电子更有可能发生量子隧穿，提供了另一种优雅的过滤机制。

当然，一旦我们创造了一股谷极化的电子流，我们必须担心这些珍贵的信息在丢失前能传播多远。电子不断地与杂质和[晶格振动](@keyword=crystal_lattice_vibrations|lang=zh-CN|style=Feynman)发生散射，其中一些散射事件可以将电子从K谷撞到K'谷，反之亦然。这个过程，即[谷间散射](@keyword=intervalley_scattering|lang=zh-CN|style=Feynman)，会随机化或“[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)”谷信息。一个谷极化的电子包在其极化衰减前可以行进的典型距离被称为谷[扩散长度](@keyword=diffusion_length|lang=zh-CN|style=Feynman) $\lambda_v$。这个长度由电子[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)的速度（$D$）和它们在谷之间跳跃的速度（$\tau_{iv}$）之间的拉锯战决定，可以简洁地由关系式 $\lambda_v = \sqrt{D \tau_{iv}}$ 概括[@problem_id:3023556]。就像在相关的自旋电子学领域中，[自旋扩散长度](@keyword=spin_diffusion_length|lang=zh-CN|style=Feynman)是一个关键参数一样，设计具有长谷[扩散长度](@keyword=diffusion_length|lang=zh-CN|style=Feynman)的材料是构建实用谷电子逻辑器件的核心挑战。

### 光学中的[谷电子学](@keyword=valleytronics|lang=zh-CN|style=Feynman)：[光电子学](@keyword=optoelectronics|lang=zh-CN|style=Feynman)与精巧控制

光与谷之间的联系也许是最直接和最直观的。我们看到，我们可以使用[圆偏振光](@keyword=circularly_polarized_light|lang=zh-CN|style=Feynman)“写入”谷信息。那么，很自然地就会想到能够将这种信息“读取”为电信号的设备。考虑一个由单层MoS$_2$等材料制成的光电探测器。当我们用右旋圆偏振光照射该设备时，我们优先在K谷中产生电子-空穴对。这些载流子随后被电场扫走，产生[光电流](@keyword=photocurrent|lang=zh-CN|style=Feynman)。

这个最终电流的谷极化讲述了一个引人入胜的动力学故事；它是一场与时间赛跑的结果。一方面，我们有载流子收集时间 $\tau_c$，即我们能多快地提取电子以产生信号。另一方面，我们有[电子-空穴复合](@keyword=electron_hole_recombination|lang=zh-CN|style=Feynman)时间 $\tau_r$，以及最关键的[谷间散射](@keyword=intervalley_scattering|lang=zh-CN|style=Feynman)时间 $\tau_{iv}$。最终的极化是一种折衷，是衡量我们能在谷信息通过复合消失或被散射打乱之前多有效地读出它的一个指标[@problem_id:989565]。因此，要构建一个好的谷光电器件，就需要对这些时间尺度进行工程设计：使收集变快，使[谷间散射](@keyword=intervalley_scattering|lang=zh-CN|style=Feynman)变慢。

这种控制水平可以达到惊人的精确度。我们不仅仅是这些过程的被动观察者；我们是积极的设计者。想象一下，我们希望获得一个非常特定的谷极化度，比如说90%。我们可以使用多种工具的组合。我们从[椭圆偏振光](@keyword=elliptically_polarized_light|lang=zh-CN|style=Feynman)开始，这给了我们对一个谷的初始偏好。然后，我们对材料施加精确量的单轴应变。这种应变打破了K谷和K'谷的[能量简并](@keyword=energy_degeneracy|lang=zh-CN|style=Feynman)，使一个能量升高，另一个降低。通过将我们的激光能量精确调谐到与现在能量较低的谷共振，我们使得该谷的吸收效率远高于另一个现在已偏离共振的谷。结果是一种高度有效的方法来“纯化”谷态，使我们能够以非凡的精度调入目标极化[@problem_id:2234907]。这就是[量子工程](@keyword=quantum_engineering|lang=zh-CN|style=Feynman)的实际应用。

### 谷存储：一种磁性类比

除了处理信息，我们能用谷来*存储*信息吗？答案似乎是肯定的，而这个概念最好通过与磁性的强大类比来理解。在铁磁体中，电子自旋之间的相互作用导致它们自发[排列](@keyword=permutation|lang=zh-CN|style=Feynman)，产生持久的磁矩。类似的集体现象是否可能发生在谷自由度上？

确实，模型表明，在某些系统（如双层[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)）中，谷之间也可能存在类似的“类交换”相互作用。这种相互作用倾向于使谷“[赝自旋](@keyword=pseudospin|lang=zh-CN|style=Feynman)”全部对齐的状态，导致自发谷极化[@problem_id:51119]。

真正非凡的是如何控制这样一个谷磁体。事实证明，面内电场对谷[赝自旋](@keyword=pseudospin|lang=zh-CN|style=Feynman)的作用，很像外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)对真实自旋的作用。这是K谷和K'谷中[贝里曲率](@keyword=berry_curvature|lang=zh-CN|style=Feynman)不同的一个微妙结果。通过施加一个强的正电场，我们可以迫使系统进入，比如说，$P=+1$ 状态（全K谷）。如果我们然后反转电场，我们可以将其翻转到 $P=-1$ 状态（全K'谷）。由于集体相互作用，系统可以表现出[磁滞](@keyword=magnetic_hysteresis|lang=zh-CN|style=Feynman)——即使在电场减小后，它也“记住”了以前的状态。迫使转换所需的场被称为“矫顽电场”，与磁性直接类比。这种[双稳态](@keyword=bistability|lang=zh-CN|style=Feynman)是非易失性存储比特的基本先决条件，但这个比特是用电场而非[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)写入的，这可能导致更快、更节能的数据存储。

### 深层联系：拓扑与受保护的电子高速公路

在这里，我们的故事发生了一个引人入胜的转变，从实际工程转向了深刻而美丽的物理学领域：拓扑学。拓扑学是研究在连续变形下保持不变的性质的数学分支。一个咖啡杯和一个甜甜圈在拓扑上是相同的，因为它们都有一个孔。这与晶体中的电子有什么关系呢？

在某些[二维材料](@keyword=2d_materials|lang=zh-CN|style=Feynman)中，例如精心[排列](@keyword=permutation|lang=zh-CN|style=Feynman)在[六方氮化硼](@keyword=hexagonal_boron_nitride|lang=zh-CN|style=Feynman)（hBN）衬底上的石墨烯，谷自由度被赋予了拓扑特性。衬底打破了石墨烯两个碳亚[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)之间的对称性，打开了一个小[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，并赋予电子“质量”。关键的是，这个质量项赋予了每个谷的电子[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)一个非平凡的拓扑不变量——一个称为陈数（Chern number）的整数。K谷和K'谷获得了相反的[陈数](@keyword=chern_number|lang=zh-CN|style=Feynman)，例如 $C_K = +1/2$ 和 $C_{K'} = -1/2$（这里的“半整数”是这个特定模型的一个特点）[@problem_id:2535583]。

这个隐藏的[拓扑荷](@keyword=topological_charge|lang=zh-CN|style=Feynman)产生了一个惊人的物理后果：**[谷霍尔效应](@keyword=valley_hall_effect|lang=zh-CN|style=Feynman)**。当电场施加在材料上时，来自两个谷的电子都会向侧面偏转。然而，由于它们的[拓扑荷](@keyword=topological_charge|lang=zh-CN|style=Feynman)相反，它们会向*相反*的方向偏转！这在材料体相中产生了一个横向的“谷电流”，K谷的电子流向一个边缘，K'谷的电子流向另一个。虽然横向的净*[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)*电流为零（两种[流动相](@keyword=mobile_phase|lang=zh-CN|style=Feynman)互抵消），但谷量子数的流动却是真实且非零的[@problem_id:2535583]。

拓扑的真正魔力在边界处显现。想象一下，在材料中创建一个[畴壁](@keyword=domain_walls|lang=zh-CN|style=Feynman)，使得拓扑质量项的符号发生翻转。[体-边对应](@keyword=bulk_edge_correspondence|lang=zh-CN|style=Feynman)原理——[拓扑物理学](@keyword=topological_physics|lang=zh-CN|style=Feynman)中的一个深刻定理——保证了受保护的导电态必须存在于这条线状界面上。在我们的例子中，这意味着一条K谷电子的单向电子“高速公路”和一条K'谷电子的反向传播高速公路。沿着K谷高速公路巡航的电子在拓扑上被禁止简单地掉头；没有可供其反向散射的态。它被散射的唯一方式是如果它被撞到动量空间的另一端，进入K'高速公路——我们知道这种[谷间散射](@keyword=intervalley_scattering|lang=zh-CN|style=Feynman)事件可能很少发生。因此，这些通道对缺陷和无序具有非凡的鲁棒性[@problem_id:2535583]。

这就引出了一个诱人的问题。[谷霍尔效应](@keyword=valley_hall_effect|lang=zh-CN|style=Feynman)是“隐藏的”，因为两个谷的贡献相互抵消。如果我们能打破它们之间的对称性呢？这正是在[莫尔超晶格](@keyword=moiré_superlattices|lang=zh-CN|style=Feynman)中可能发生的情况，例如在扭转的[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)层中。在这些系统中，由“平坦”电子[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的形成而放大的强[电子-电子相互作用](@keyword=electron_electron_interactions|lang=zh-CN|style=Feynman)，可能导致系统自发地打破[时间反演对称性](@keyword=time_reversal_symmetry|lang=zh-CN|style=Feynman)。例如，系统可能选择只填充一个谷。现在，那个单一谷的拓扑荷不再被其伙伴抵消，因而占据主导地位。系统获得了一个净的非零[陈数](@keyword=chern_number|lang=zh-CN|style=Feynman)。这导致了**[量子反常霍尔效应](@keyword=quantum_anomalous_hall_effect|lang=zh-CN|style=Feynman)**（QAHE）：一个完美量子化的[霍尔电阻](@keyword=hall_resistance|lang=zh-CN|style=Feynman)和无耗散的手性边缘电流，就像在[整数量子霍尔效应](@keyword=integer_quantum_hall_effect|lang=zh-CN|style=Feynman)中一样，但是在*零*外[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)下[@problem_id:2830178]。这是凝聚态物理学的圣杯之一，预示着无电阻的电子学，而谷物理学为其实现提供了一条关键途径。

### 作为[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的谷：[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)一瞥

谷自由度的离散、双能级特性使其成为[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)（qubit）的天然候选者，[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)是[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的基本单位。我们可以将纯谷态表示为 $|K\rangle \equiv |0\rangle$ 和 $|K'\rangle \equiv |1\rangle$。

为了理解这如何运作，让我们想象一个经典的量子干涉实验。我们将一个激子——一个继承了谷指数的[电子-空穴对](@keyword=electron_hole_pair|lang=zh-CN|style=Feynman)——送入一个干涉仪，它被分成两条路径然后重新组合。如果我们在[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)的一个臂中放置一个[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，由于谷固有的[轨道磁矩](@keyword=orbital_magnetic_moment|lang=zh-CN|style=Feynman)，处于 $|K\rangle$ 态的激子将获得与处于 $|K'\rangle$ 态的激子不同的量子相位。当路径重新组合时，产生的干涉图样对这个相位非常敏感。事实上，干涉条纹的可见度成为谷态相干性的直接度量。如果我们有办法知道[激子](@keyword=excitons|lang=zh-CN|style=Feynman)在哪一个“谷”中，干涉就会消失——这是[量子互补性](@keyword=quantum_complementarity|lang=zh-CN|style=Feynman)的一个完美展示[@problem_id:786581]。这简单的思想实验表明，谷指数可以被相干地操纵和读出，满足了[量子信息处理](@keyword=quantum_information_processing|lang=zh-CN|style=Feynman)的基本要求。

谷不仅仅是理论上的幻想；它们的存在被铭刻在材料的可测量属性中。例如，谷独特的磁特性在实验数据中留下了各种印记。一个足以完全清空一个谷的强[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，会导致材料[磁化率](@keyword=susceptibility|lang=zh-CN|style=Feynman)的突然变化——一个“扭折”。这个扭折可以在灵敏的扭矩磁力测量中看到，也可以在核磁共振（NMR）测量的奈特位移中看到。量子[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)（[舒布尼科夫-德哈斯效应](@keyword=shubnikov_de_haas_effect|lang=zh-CN|style=Feynman)）的频率也讲述了这个故事，显示出由两个不同谷布居引起的“[拍频](@keyword=beats_frequency|lang=zh-CN|style=Feynman)”图案，一旦一个谷被清空，该图案就坍缩为单一频率。这一系列实验探针提供了[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)印证的证据，证实我们确实在观察和控制这个新的量子自由度[@problem_id:3008862]。

从晶体管到拓扑高速公路和[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，谷自由度开辟了一个极其丰富的游乐场。它证明了在晶体看似刚性有序的结构中，隐藏着等待被发现、理解和利用于未来技术的量子行为世界。