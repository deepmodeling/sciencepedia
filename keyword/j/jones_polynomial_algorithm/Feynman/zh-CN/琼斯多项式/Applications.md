## 应用与跨学科联系

你可能会和我一样觉得，一个相当抽象的数学思想，先在一个科学领域出现，然后仿佛变魔术一般，又在另一个完全不同的领域现身，这是一件奇特的事。这就像在山花的图案中发现了来自海滩的奇特贝壳。当这种情况发生时，它总是一个线索。它告诉我们，世界的深层结构，即游戏规则，比我们最初想象的要更加统一和优雅。[琼斯多项式](@keyword=jones_polynomial|lang=zh-CN|style=Feynman)正是这种统一思想最壮观的例子之一。它诞生于纯粹数学，作为一种区分缠绕绳线的巧妙技巧，结果却被证明是自然界在其某些最神秘和最激动人心的领域中所说的一种语言。

让我们踏上穿越这些领域的旅程，看看我们的[纽结多项式](@keyword=knot_polynomials|lang=zh-CN|style=Feynman)一直隐藏在何处。

### [时空](@keyword=space_time|lang=zh-CN|style=Feynman)之声：量子场论

也许最深刻、最惊人的联系是由物理学家[Edward Witten](@keyword=edward_witten|lang=zh-CN|style=Feynman)发现的。他当时正在研究一种被称为[Chern-Simons理论](@keyword=chern_simons_theory|lang=zh-CN|style=Feynman)的量子场论。你可以把这个理论看作是描述三维空间中几何本身量子规则的一种方式。在这个世界里，一个[亚原子粒子](@keyword=subatomic_particles|lang=zh-CN|style=Feynman)在时间中移动的路径在[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中描绘出一条线。如果你有几个相互作用的粒子，它们的路径就描绘出一组交织的线——一个辫子或一个环链！

Witten表明，与描绘这样一条纽结路径相关的算子——一个“Wilson圈”——的“[真空期望值](@keyword=vacuum_expectation_value|lang=zh-CN|style=Feynman)”，正是[琼斯多项式](@keyword=jones_polynomial|lang=zh-CN|style=Feynman)。这意味着什么？在量子场论中，为了找到一个实验最可能的结果，你必须对*所有可能的历史*进行求和，或者说积分。计算Wilson圈涉及到在底层量子场的所有可能构型上对某个量进行平均。他发现，如果理论的[规范群](@keyword=gauge_group|lang=zh-CN|style=Feynman)是[特殊酉群](@keyword=special_unitary_group|lang=zh-CN|style=Feynman)$SU(2)$，你得到的平均值*就是*[琼斯多项式](@keyword=jones_polynomial|lang=zh-CN|style=Feynman)，其中变量 $t$ 不再只是一个形式化的符号，而是与理论的基本常数直接相关。

这不仅仅是一个模糊的类比。我们实际上可以进行计算。对于一个给定的纽结，比如8字结，我们可以基于其多项式定义一个函数，并使用该群的自然测度——[Haar测度](@keyword=haar_measure|lang=zh-CN|style=Feynman)——在整个$SU(2)$群上对这个函数进行平均。这个过程，作为[路径积分](@keyword=path_integration|lang=zh-CN|style=Feynman)的精确数学体现，会得出一个具体的数值，通常是一个简单的整数，就好像宇宙将纽结和[量子涨落](@keyword=quantum_fluctuations|lang=zh-CN|style=Feynman)的所有复杂性提炼成了一个单一、优雅的数字。事实证明，纽结的抽象代数就是[量子真空](@keyword=quantum_vacuum|lang=zh-CN|style=Feynman)的物理学。

### 编织[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)：[拓扑量子计算](@keyword=topological_quantum_computing|lang=zh-CN|style=Feynman)

这种深刻的物理意义立即催生了一个惊人的应用。如果宇宙已经知道如何计算[琼斯多项式](@keyword=jones_polynomial|lang=zh-CN|style=Feynman)，也许我们可以 coax 它为我们计算东西！这就是[拓扑量子计算](@keyword=topological_quantum_computing|lang=zh-CN|style=Feynman)（TQC）的核心思想。

想象一个奇异的二维世界，里面居住着被称为“[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)”的奇异粒子。当这些任意子相互绕行时，它们在三维[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中的世界线形成了辫子。在TQC中，一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)——一个qubit——不是存储在单个粒子中，而是非局域地存储在几个[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)的集体状态中。[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)是通过物理地编织它们的[世界线](@keyword=worldline|lang=zh-CN|style=Feynman)来执行的。一个特定的辫[子序列](@keyword=subsequences|lang=zh-CN|style=Feynman)对应于一个特定的量子算法。

这为什么如此令人兴奋？一个常规的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)是脆弱的；来[自环](@keyword=self_loop|lang=zh-CN|style=Feynman)境的微小扰动就可能破坏其信息。但在TQC中，状态存储在辫子的*拓扑结构*中。你可以摆动和变形[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)的路径，只要你不打断一股线或让一股线穿过另一股，其本质的纽结性——也即其计算——就保持不变。它是内在[容错](@keyword=fault_tolerance|lang=zh-CN|style=Feynman)的。

[琼斯多项式](@keyword=jones_polynomial|lang=zh-CN|style=Feynman)是这场秀的主角。对于某些类型的任意子，特别是希望在实验系统中实现的“斐波那契”任意子，描述这些编织操作的酉矩阵与在特定 $t$ 值（一个单位根，如 $t = \exp(i 2\pi/5)$）下计算[琼斯多项式](@keyword=jones_polynomial|lang=zh-CN|style=Feynman)直接相关。编织任意子以在[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机中执行一个门的操作，其本身就等同于为该辫子“计算”[琼斯多项式](@keyword=jones_polynomial|lang=zh-CN|style=Feynman)。我们甚至可以深入细节，计算当两个[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)交换时，一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)从 $|0\rangle$ 翻转到 $|1\rangle$ 的[量子力学概率](@keyword=quantum_mechanics_probability|lang=zh-CN|style=Feynman)，我们发现它由一个与[黄金比例](@keyword=golden_ratio|lang=zh-CN|style=Feynman)相关的美丽数字给出，这是这些辫子底层数学结构的直接结果。这种联系不是单向的；我们也可以从拓扑的角度看待标准的量子电路，比如那些由CNOT门构建的电路，将它们与作为[琼斯多项式](@keyword=jones_polynomial|lang=zh-CN|style=Feynman)推广的环链[不变量](@keyword=invariant|lang=zh-CN|style=Feynman)联系起来。

### 懂得纽结理论的磁体：[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学

现在，让我们转向一幅完全不同的画面。暂时忘记[时空](@keyword=space_time|lang=zh-CN|style=Feynman)和量子场，想象一个简单的棋盘，一个格点。在格点的每个位置，想象有一个微小的磁铁，或“自旋”，可以指向上或下。这些自旋与它们的邻居相互作用，试图对齐或反对齐。这是[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的领域，研究大量相互作用部分产生集体现象（如磁性或水结冰）的物理学。

在1980年代，一个非凡的发现被做出。对于某些“精确可解”模型，如著名的[XXZ自旋链](@keyword=xxz_spin_chain|lang=zh-CN|style=Feynman)或[六顶点模型](@keyword=six_vertex_model|lang=zh-CN|style=Feynman)，解的关键是一个称为R-矩阵的数学对象。这个R-矩阵描述了两个粒子在格点上如何相互散射。令人惊讶的是，人们发现这些R-矩阵满足与辫[群生成元](@keyword=group_generators|lang=zh-CN|style=Feynman)相同的代数关系！这就是著名的[Yang-Baxter方程](@keyword=yang_baxter_equation|lang=zh-CN|style=Feynman)。

其结果是，描述微观自旋如何在二维网格上[排列](@keyword=permutation|lang=zh-CN|style=Feynman)的数学，与描述三维环圈缠结的数学是*相同*的。你可以使用一个统计模型的R-矩阵来构建[辫群的表示](@keyword=representations_of_the_braid_group|lang=zh-CN|style=Feynman)，并由此计算你想要的任何纽结的[琼斯多项式](@keyword=jones_polynomial|lang=zh-CN|style=Feynman)。三叶结的多项式值可以从[六顶点模型](@keyword=six_vertex_model|lang=zh-CN|style=Feynman)的[转移矩阵](@keyword=transition_matrix|lang=zh-CN|style=Feynman)计算出来，而Hopf环链的[不变量](@keyword=invariant|lang=zh-CN|style=Feynman)可以通过研究XXZ磁性模型找到。这是一种近乎诡异的对应关系。研究一块磁性材料的物理学家和打结的数学家，在某种意义上，正在解决同一个谜题。

### 宏大统一：共形场论

一个三维[量子真空](@keyword=quantum_vacuum|lang=zh-CN|style=Feynman)（Chern-Simons）的物理学如何能与一个二维自旋格点（[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学）的物理学如此紧密地联系在一起？连接这两个世界的桥梁是共形场论（CFT）。CFT是一种特殊的量子场论，它描述了处于[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)的系统，例如，水恰好在沸点时，液体和蒸汽以所有可能的尺度在波动的斑块中并存。这种“[标度不变性](@keyword=scaling_invariance|lang=zh-CN|style=Feynman)”赋予了CFT一个极其严格和强大的数学结构。

存在一个深刻的对应关系：三维[Chern-Simons理论](@keyword=chern_simons_theory|lang=zh-CN|style=Feynman)的物理学等价于其边界上存在的[二维共形场论](@keyword=2d_conformal_field_theory|lang=zh-CN|style=Feynman)的物理学。这意味着我们可以将一个语言中的问题翻译成另一种语言。事实证明，许多可解的统计模型在其[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)上是由CFT描述的。例如，临界3-态[Potts模型](@keyword=potts_model|lang=zh-CN|style=Feynman)（一种简单磁体模型的推广）由一个特定的CFT描述。这个CFT的[基本数](@keyword=q_number|lang=zh-CN|style=Feynman)据，例如其“模S-矩阵”，包含了重新推导[琼斯多项式](@keyword=jones_polynomial|lang=zh-CN|style=Feynman)所需的所有信息。人们可以使用该理论中场的[量子维度](@keyword=quantum_dimension|lang=zh-CN|style=Feynman)来确定正确的 $t$ 值，并为像[三叶结](@keyword=trefoil_knot|lang=zh-CN|style=Feynman)这样的纽结计算多项式。这是最终的综合：[纽结不变量](@keyword=knot_invariants|lang=zh-CN|style=Feynman)被编码在一个系统处于[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)时的标度行为中。

### 数学与随机性的内在世界

尽管与物理学有这些壮观的联系，我们不应忘记，[琼斯多项式](@keyword=jones_polynomial|lang=zh-CN|style=Feynman)在其核心是一个纯粹数学的对象，拥有其自身的内在美和结构。对于整族的纽结，比如可以画在甜甜圈表面上的环面纽结，该多项式可以用其他著名的数学函数——切比雪夫多项式——以一种非常紧凑的形式表达出来。它拥有自己独立的生命和丰富性。

此外，它的代数性质可以以令人惊讶的方式应用。对于仅在一个区域的扭转次数上有所不同的纽结，其多项式通常遵循一个简单的[线性递推关系](@keyword=linear_recurrence_relations|lang=zh-CN|style=Feynman)。这种结构非常适合使用概率论的工具进行分析。我们可以想象这样的场景，也许是在模拟长而缠结的聚合物链时，其中扭转的次数不是固定的，而是一个[随机变量](@keyword=random_variable|lang=zh-CN|style=Feynman)。通过使用[生成函数](@keyword=generator_function|lang=zh-CN|style=Feynman)的数学技术，我们可以计算[琼斯多项式](@keyword=jones_polynomial|lang=zh-CN|style=Feynman)在一个随机纽结系综上的*[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)*值。[纽结多项式](@keyword=knot_polynomials|lang=zh-CN|style=Feynman)变成了一个统计工具。

从量子真空到[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机，从[冰箱](@keyword=refrigerators|lang=zh-CN|style=Feynman)磁铁到随机聚合物，我们这套简单的缠结图规则带我们进行了一次盛大的巡礼。琼斯多-项式证明了宇宙并没有为数学、量子引力和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)设置独立的部门。最美丽的思想是那些无视这些界限，揭示其下简单、统一真理的思想。