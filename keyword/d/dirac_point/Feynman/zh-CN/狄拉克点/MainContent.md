## 引言
在[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)的世界里，电子通常存在于由[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)隔开的明确[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)中，这是支配现代电子学的基本原理。然而，某些非凡的材料打破了这一常规，承载着一种被称为狄拉克点的迷人现象。在材料电子结构的这些[奇异点](@keyword=exceptional_points|lang=zh-CN|style=Feynman)上，规则发生了戏剧性的变化：电子摆脱了它们的[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)，开始表现得像光粒子一样，遵循[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)的原理。这就提出了一个关键问题：被束缚在固体中的电子如何能模拟无质量粒子？这种奇异行为对科学技术又有哪些深远的影响？

本文将对狄拉克点进行全面探索，引导读者从其基本起源走向其变革性应用。第一章 **“原理与机制”** 将揭示[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)等材料中锥形[能带结构](@keyword=e_k_diagram|lang=zh-CN|style=Feynman)背后的物理学。我们将探讨独特的[蜂窝晶格](@keyword=honeycomb_lattice|lang=zh-CN|style=Feynman)如何产生[无质量狄拉克费米子](@keyword=massless_dirac_fermions|lang=zh-CN|style=Feynman)，介绍[赝自旋](@keyword=pseudospin|lang=zh-CN|style=Feynman)和拓扑[贝里相位](@keyword=berry_s_phase|lang=zh-CN|style=Feynman)的关键概念，并考察这些思想如何从二维平面延伸到三维固体。随后，**“应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系”** 章节将重点转向这一物理学现象的实际影响。我们将发现狄拉克点如何成为下一代晶体管的关键，如何通过“转角电子学”实现新材料的设计，并推动自旋电子学和拓扑器件的创新，甚至在[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)领域也能找到其惊人的相似之处。

## 原理与机制

想象你是一名探险家，正在绘制一种材料中电子的能量景观。在你遇到的大多数材料中，比如你电脑芯片里的硅，这个景观是可预测的。那里有充满电子的低洼平原，即**价带**，和高耸空旷的高原，即**[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)**。它们之间是一片广阔平坦的沙漠——**[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)**——一个不允许任何电子存在的能量范围。要让一个电子导电，你必须给它足够的能量，让它完成一次跨越这个[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的巨大飞跃。

但随后你来到了[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)的世界，这是一个由碳原子以完美蜂窝状[排列](@keyword=permutation|lang=zh-CN|style=Feynman)构成的非凡“平面国度”。这里的景象全然不同。低洼的平原和高耸的高原依然存在，但它们之间的沙漠却缩小到几乎为零。取而代之的是，价带和导带相互靠拢，并在离散的奇异点上相遇。在这些特殊的位置，景观不再平坦，而是锐化成一个完美的、无限尖锐的点，就像一个圆锥体的顶点。这些[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的交汇点就是著名的**[狄拉克点](@keyword=dirac_points|lang=zh-CN|style=Feynman)**。

### 石墨烯的锥形世界

为什么会形成这种奇特的锥形？秘密在于电子在石墨烯[蜂窝晶格](@keyword=honeycomb_lattice|lang=zh-CN|style=Feynman)上的优雅舞蹈。这并非一个简单的网格，它有两种不同类型的格点，我们可以称之为A子[晶格和](@keyword=lattice_sums|lang=zh-CN|style=Feynman)B子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。一个电子的命运不仅取决于它要去哪里，还取决于它位于哪个子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)上。描述这一现象的最简单且出奇有效的方法是**[紧束缚模型](@keyword=tight_binding_model|lang=zh-CN|style=Feynman)** [@problem_id:1195456]。想象一个电子可以从一个碳原子“跃迁”到其最近邻的原子。电子的能量则取决于其所有可能跃迁路径之间的量子力学干涉。

当我们进行数学计算时，一个优美的结果出现了。电子的能量 $E$ 并不像普通有质量粒子那样依赖于其动量 $k$ 的平方（$E \propto k^2$）。相反，在狄拉克点附近，能量与相对于该点的动量大小成正比 [@problem_id:1195456]：

$$
E(\mathbf{q}) = \pm \hbar v_F |\mathbf{q}|
$$

在这里，$\mathbf{q}$ 是电子相对于[狄拉克点](@keyword=dirac_points|lang=zh-CN|style=Feynman)的动量矢量，$\hbar$ 是[约化普朗克常数](@keyword=reduced_planck_constant|lang=zh-CN|style=Feynman)，$v_F$ 是一个称为**费米速度**的常数。$\pm$ 符号给了我们两个尖端对尖端相接的圆锥：一个能量为正的“导带”锥和一个能量为负的“[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)”锥。这些锥体就是著名的**[狄拉克锥](@keyword=dirac_cones|lang=zh-CN|style=Feynman)**。常数 $v_F$ 可以直接通过跃迁强度和晶格间距计算得出 [@problem_id:1195456]，它扮演着这些电子的光速角色，通常在 $10^6 \text{ m/s}$ 左右，大约是真空中实际光速的 $1/300$。这些狄拉克点在动量空间中的具体位置并非任意，而是由蜂窝几何结构精确决定的，正好落在六边形[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)的顶点上 [@problem_id:49301]。

### 无质量生存

这种能量和动量之间线性的、类似圆锥的关系是无质量粒子的标志。思考一下爱因斯坦的方程 $E = \sqrt{(mc^2)^2 + (pc)^2}$。对于一个静止的粒子（$p=0$），我们有 $E=mc^2$。对于像[光子](@keyword=photon|lang=zh-CN|style=Feynman)这样的无质量粒子（$m=0$），方程简化为 $E = pc$。我们在石墨烯中的方程 $E = v_F p$（其中 $p = \hbar |\mathbf{q}|$）看起来完全一样！

这带来了一个奇异的后果。在普通材料中，我们为电子定义了一个**有效质量** $m^*$。它衡量电子在电场作用下抵抗加速的程度，并由[能量景观](@keyword=energy_landscape|lang=zh-CN|style=Feynman)的曲率决定：$m^* = \hbar^2 / (\partial^2 E / \partial k^2)$。一个高度弯曲的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)意味着一个小的[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)（易于加速），而一个平坦的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)则意味着一个巨大的[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)。但我们的[狄拉克锥](@keyword=dirac_cones|lang=zh-CN|style=Feynman)呢？一个圆锥在任何径向方向上都是一条直线。直线的曲率为零！如果你试图计算[狄拉克点](@keyword=dirac_points|lang=zh-CN|style=Feynman)处的[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)，你会发现能量对动量的二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)为零，导致在公式中出现除以零的情况 [@problem_id:1780059]。

$$
\frac{\partial^2 E}{\partial k^2} = \frac{\partial^2}{\partial k^2}(\hbar v_F k) = 0 \implies m^* = \frac{\hbar^2}{0} \quad (\text{Undefined!})
$$

[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)这一半导体物理学的基石概念，在此处完全失效。这不仅仅是一个数学上的怪癖，而是物理学在告诉我们，我们正在处理一种新型粒子——**[无质量狄拉克费米子](@keyword=massless_dirac_fermions|lang=zh-CN|style=Feynman)**——一种行为像光粒子，却被困在固体中的实体。

### 机器中的幽灵：[赝自旋](@keyword=pseudospin|lang=zh-CN|style=Feynman)

是什么导致了这种“[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)性”行为？是[蜂窝晶格](@keyword=honeycomb_lattice|lang=zh-CN|style=Feynman)的双子[晶格结构](@keyword=crystal_lattice_structure|lang=zh-CN|style=Feynman)（A和B）。[狄拉克点](@keyword=dirac_points|lang=zh-CN|style=Feynman)附近电子的状态不仅由其动量描述，还由一个双分量[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)描述，这个态告诉我们它在A子[晶格和](@keyword=lattice_sums|lang=zh-CN|style=Feynman)B子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)上的振幅。这个[二能级系统](@keyword=two_level_systems|lang=zh-CN|style=Feynman)在数学上与电子的自旋1/2（自旋向上 vs 自旋向下）完全相同。为了与电子*真实*的内禀自旋区分开来，我们称这个新属性为**[赝自旋](@keyword=pseudospin|lang=zh-CN|style=Feynman)** [@problem_id:2805103]。

低能物理由一个极其简洁的方程——**狄拉克哈密顿量**——所支配：

$$
H = \hbar v_F (\sigma_x q_x + \sigma_y q_y)
$$

在这里，$q_x$ 和 $q_y$ 是动量的分量，而 $\sigma_x$ 和 $\sigma_y$ 是著名的泡利矩阵。但在这里，它们作用的不是真实自旋，而是[赝自旋](@keyword=pseudospin|lang=zh-CN|style=Feynman)，混合了A和B子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的分量。这个方程揭示了一个深刻的联系：电子的运动方向（其动量 $\mathbf{q}$）与其[赝自旋](@keyword=pseudospin|lang=zh-CN|style=Feynman)的取向是锁定的。动量与内部子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)自由度之间的这种紧密耦合，是锥形能带结构及其所有奇特后果的根本机制。电子的真实自旋，在大多数情况下，只是“随波逐流”，为所有事物增加了一个额外的二重简并。

### [狄拉克锥](@keyword=dirac_cones|lang=zh-CN|style=Feynman)的推论

这种独特的锥形结构具有直接可观测的后果，使石墨烯与任何其他材料都截然不同。

首先，让我们问：在给定的能量 $E$ 下，有多少可用的电子态？这个量，即**[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)**（DOS），告诉你电子有多少可用的“停车位”。对于二维传统材料，其[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)为抛物线形（$E \propto k^2$），态密度是恒定的。但对于[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)，一个简单的计算表明，态密度与能量本身成正比 [@problem_id:1765992] [@problem_id:2480704]：

$$
g(E) = \frac{2|E|}{\pi (\hbar v_{F})^{2}}
$$

这种V形分布意味着在狄拉克点（$E=0$），恰好有零个态！因此，如果你将材料的费米能级（电子的“海平面”）精确调谐到狄拉克点，你可能会[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)它是一个电导率为零的完美绝缘体。

但自然界更为微妙。实验表明，即使在最纯净的[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)样品中，在最低温度下，电导率也不会降至零。它会稳定在一个神秘的最小值，约为 $e^2/h$ 的量级。为什么？即使在载流子的真空中，不确定性原理也允许短暂的、“虚”的[电子-空穴对](@keyword=electron_hole_pair|lang=zh-CN|style=Feynman)瞬间产生和消失。这些瞬态[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)可以携带电流，从而导致[电导率](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)存在一个下限 [@problem_id:1774221]。这种最小[电导率](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)是一种基本的量子现象，是窥探固体内[量子真空](@keyword=quantum_vacuum|lang=zh-CN|style=Feynman)蓬勃活动的直接窗口。

### 动量空间中的扭曲：贝里相位

[狄拉克锥](@keyword=dirac_cones|lang=zh-CN|style=Feynman)还隐藏着一个更深的秘密，一个在其[能谱](@keyword=energy_spectrum|lang=zh-CN|style=Feynman)中无法看到的秘密。它具有隐藏的拓扑特性。想象一下，迫使一个电子的动量在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中沿着一个闭合回路运动，环绕狄拉克点。当它完成这个回路时，它的[量子力学波函数](@keyword=quantum_mechanics_wavefunctions|lang=zh-CN|style=Feynman)并不会回到其原始状态，而是获得了一个额外的相位因子。这个相位并非源于时间的流逝，而仅仅取决于在动量空间中所取路径的几何形状。它被称为**贝里相位**。

对于环绕石墨烯中单个狄拉克点的回路，直接计算表明这个相位恰好是 $\pi$（或180度） [@problem_id:3022810]。这个非平庸相位是一个拓扑不变量；你无法通过平滑地变形哈密顿量来消除它，除非你闭合因破坏锥结构而形成的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。这就像电子态的织物上存在一个永久的扭曲。

这个抽象概念有一个惊人具体的后果：**反常量子霍尔效应**。当强[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)施加于二维电子气时，电子被迫进入称为朗道能级的量子化[圆形轨道](@keyword=circular_orbits|lang=zh-CN|style=Feynman)，霍尔电导率以 $e^2/h$ 的整数步长进行量子化。在[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)中，$\pi$ [贝里相位](@keyword=berry_s_phase|lang=zh-CN|style=Feynman)修正了量子化规则，使整个步长序列移动了半个整数：$\sigma_{xy} = 4(N + 1/2)e^2/h$，其中 $N$ 是一个整数。这种[半整数](@keyword=half_integers|lang=zh-CN|style=Feynman)平移在实验中被直接测量到，是石墨烯电子[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)中存在拓扑扭曲的确凿证据。

### 超越完美锥体：从二维到三维

当然，完美对称、无质量的[狄拉克锥](@keyword=dirac_cones|lang=zh-CN|style=Feynman)是一种理想化模型。在真实的[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)中，其他效应也会发挥作用。例如，允许电子跃迁到其次近邻原子（$t'$）会打破简单模型中完美的电子-空穴对称性。这导致V形的态密度变得不对称，并将狄拉克点本身的能量从零点移开，尽管它并不会打开一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) [@problem_id:2471755]。

然而，狄拉克点的概念远比[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)更具普遍性。在某些被称为**[狄拉克半金属](@keyword=dirac_semimetals|lang=zh-CN|style=Feynman)**的三维材料中，也会出现类似的线性[能带交叉](@keyword=band_crossing|lang=zh-CN|style=Feynman)。这些三维狄拉克点甚至更为非凡。它们的存在通常受到晶体最基本对称性的保护：**时间反演对称性**（物理定律在时间正向和反向运行时相同）和**空间[反演对称性](@keyword=inversion_symmetry|lang=zh-CN|style=Feynman)**（晶体颠倒看时保持不变）[@problem_id:1827867]。在这里，一个狄拉克点是四重简并的[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)点，同时考虑了[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)简并和真实自旋简并。

如果我们打破这些保护性对称性中的一个会发生什么？例如，通过施加应力破坏空间[反演对称性](@keyword=inversion_symmetry|lang=zh-CN|style=Feynman) [@problem_id:1827839]？[狄拉克点](@keyword=dirac_points|lang=zh-CN|style=Feynman)会变得不稳定。由于其[拓扑性质](@keyword=topological_property|lang=zh-CN|style=Feynman)，它不能简单地消失。相反，它会分裂成一对在动量空间中分离的二重简并点。这些新的、更基本的粒子被称为**外尔点**。一个狄拉克点可以被看作是两个具有相反拓扑荷（手性）的外尔点，因对称性而被迫重叠在一起。打破对称性使它们得以分开，揭示出它们各自的身份。

这段旅程，从[蜂窝晶格](@keyword=honeycomb_lattice|lang=zh-CN|style=Feynman)中的一个奇特特征到一个由[基本对称性](@keyword=fundamental_symmetries|lang=zh-CN|style=Feynman)支配的普适概念，展示了物理学深刻的美和统一性。狄拉克点不仅仅是某一种材料的特性；它是量子力学、[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)和拓扑学深层原理的体现，被书写在物质的结构之中。