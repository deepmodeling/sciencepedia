## 应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系

你可能想知道，[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)——这门关于蒸汽、热量和无序的科学——究竟与[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机那纯净、相干且无疑是冰冷的世界有什么关系。答案竟然是，几乎所有方面都有关系。这并非说[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机是秘密的蒸汽机，而是说[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的强大语言为我们描述、构建并最终检验这些非凡的机器提供了最深刻、最实用的工具。统计、温度和系综这些概念远非麻烦，它们构成了一个统一的视角，揭示了量子信息基础中一种深刻而出人意料的美。那么，让我们踏上旅程，看看那些描述水沸腾的思想如何也能帮助我们驾驭现实最深层的规则。

### 作为经典项链的量子世界

让我们从物理学中最神奇的思想之一开始，这是理查德·费曼本人开创的：[路径积分](@keyword=path_integration|lang=zh-CN|style=Feynman)。想象一个单一的量子粒子。与经典的台球不同，它没有确定的位置。它存在于一片可能性的云中。当它与其周围环境处于热平衡时，我们如何描述它的性质，比如它的平均位置或其分布范围？

路径积分形式主义提供了一个惊人的答案。它告诉我们，我们可以通过研究一个完全不同的*经典*对象来计算这个单一粒子的[量子统计](@keyword=quantum_statistics|lang=zh-CN|style=Feynman)性质：一个“[环状聚合物](@keyword=ring_polymer|lang=zh-CN|style=Feynman)”。想象一条由大量珠子（比如 $P$ 个）组成的项链，这些珠子由微小、相同的弹簧连接。每个珠子代表粒子在[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)的不同“切片”上的位置。整条项链现在生活在一个经典世界中，我们可以使用熟悉的经典[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学工具来研究它。[@problem_id:2921744]

这不仅仅是一个可爱的类比；在珠子数量无限多（$P \to \infty$）的极限下，这个映射在数学上是精确的。粒子的量子不确定性——它的波状延展——表现为经典项链的物理尺寸和形状。一个被势紧紧束缚的粒子对应于一条小而刚性的项链。一个自由粒子则对应于一条大而松软的项链。

真正非凡的是纯粹的量子现象是如何被捕捉的。珠子之间相互[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)的“内部模式”在某种意义上是虚构的。没有额外的粒子。它们是[路径积分](@keyword=path_integration|lang=zh-CN|style=Feynman)构造中的数学产物。然而，这些虚构的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)是绝对必要的。它们的能量，按经典能量均分定理计算，恰好使得模型能够再现像[零点能](@keyword=zero_point_energy|lang=zh-CN|style=Feynman)和隧穿这样的量子效应。这条经典项链的统计涨落完美地再现了原始粒子的量子涨落。这种强大的同构，连接了量子统计世界和经典统计世界，是众多高级模拟技术的基础，更重要的是，它为我们理解[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)的本质提供了深刻的直觉。

### 用磁性物理学守护[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)

现在让我们从一个粒子扩展到一台完整的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机。这项工作的最大挑战是退相干——嘈杂的外部世界无情地破坏脆弱[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)的倾向。解决方案是[量子纠错](@keyword=quantum_error_correction|lang=zh-CN|style=Feynman)，其基础稳固地建立在[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的原理之上。

考虑一个流行的方案，如[表面码](@keyword=surface_codes|lang=zh-CN|style=Feynman)，其中[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)被非局域地编码在一个二维的物理量子比特网格上。我们可以将保护这些信息的问题映射到一个[三维晶格](@keyword=3d_lattices|lang=zh-CN|style=Feynman)上的经典[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学问题（二维空间，一维时间）。在这个类比中，“正确的”编码态，即没有错误存在的状态，对应于磁体的*有序相*，就像所有原子自旋都对齐的铁磁体。一个破坏计算的逻辑错误等同于一个破坏这种原始秩序的大尺度缺陷，即“[畴壁](@keyword=domain_walls|lang=zh-CN|style=Feynman)”。[@problem_id:175861]

来自环境和有缺陷的门的噪声就像一个随机、波动的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，试图翻转自旋并破坏[磁序](@keyword=magnetic_ordering|lang=zh-CN|style=Feynman)。关键问题——“是否存在[容错阈值](@keyword=error_threshold|lang=zh-CN|style=Feynman)？”——直接转化为凝聚态物理学中的一个经典问题：“有序相在非零温度下是否保持稳定？”磁体在热扰动的冲击下能否保持其[排列](@keyword=permutation|lang=zh-CN|style=Feynman)？

利用[统计物理学](@keyword=statistical_physics|lang=zh-CN|style=Feynman)中研究[无序系统](@keyword=disordered_systems|lang=zh-CN|style=Feynman)的工具，可以分析[纠错码](@keyword=error_correcting_codes|lang=zh-CN|style=Feynman)的稳定性。在这种观点下，一个逻辑错误（对应于一个大尺度的“缺陷”或“[畴壁](@keyword=domain_walls|lang=zh-CN|style=Feynman)”）的能量成本，必须与可能由噪声驱动产生的“熵”或随机能量增益相抗衡。系统的容错能力取决于这种成本是否能战胜随机性的影响，从而保持有序的编码状态。

分析表明，这个结果对噪声的性质非常敏感，尤其是噪声在空间上的关联性。可以证明，如果噪声的[空间相关性](@keyword=spatial_correlation|lang=zh-CN|style=Feynman)随距离 $r$ 衰减得足够快（例如，在[表面码](@keyword=surface_codes|lang=zh-CN|style=Feynman)的情况下，比 $r^{-2}$ 更快），那么[容错阈值](@keyword=error_threshold|lang=zh-CN|style=Feynman)就可以存在。如果噪声关联衰减得更慢（即长程相关噪声），它们将总是会压倒纠错码，使得大规模[容错量子计算](@keyword=fault_tolerant_quantum_computing|lang=zh-CN|style=Feynman)变得不可能。因此，在这个模型中，构建一台可扩展[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的可能性，变成了一个关于无序[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学系统中[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)和[临界现象](@keyword=critical_phenomena|lang=zh-CN|style=Feynman)的根本问题。

### 拓扑计算机的[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)身份

一些最有前途的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机蓝图是基于被称为[拓扑相](@keyword=topological_phases|lang=zh-CN|style=Feynman)的奇异[物质状态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)。在这里，量子信息存储在系统的全局“拓扑”性质中，使其天生对局域噪声具有抵抗力。这些系统中的基本计算粒子不是电子或[光子](@keyword=photon|lang=zh-CN|style=Feynman)，而是被称为“[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)”的演生实体。一个关键问题是：对于给定的材料，它支持多少种不同类型的任意子？这个数字决定了计算空间的维度。

[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学如何帮助我们数清它们？我们可以借用其最基本的工具之一：[配分函数](@keyword=sum_over_states_2|lang=zh-CN|style=Feynman)，$Z = \mathrm{Tr}(e^{-\beta H})$，其中 $H$ 是系统的哈密顿量，$\beta$ 是[逆温](@keyword=temperature_inversion|lang=zh-CN|style=Feynman)度。在普通[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)中，这个函数是通往一切的门户：能量、熵、压强。但对于描述我们系统在环面空间上的[拓扑量子场论](@keyword=topological_quantum_field_theory|lang=zh-CN|style=Feynman)（TQFT）而言，在[低温极限](@keyword=low_temperature_limit|lang=zh-CN|style=Feynman)（$\beta \to \infty$）下，会发生神奇的事情。[@problem_id:3021929]

在这个极限下，我们只关心系统的简并[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。在这个空间内，哈密顿量实际上为零，所以 $e^{-\beta H}$ 变成了单位算符。迹（对角元素之和）就简化为这个[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)空间的维度。而 TQFT 的一个基石性结果表明，环面上[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)希尔伯特空间的维度恰好是不同任意子类型的数量 $N$。

于是，宏大的[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)[配分函数](@keyword=sum_over_states_2|lang=zh-CN|style=Feynman)简化为一个整数：$Z = N$。一个来自19世纪热学理论的概念，变成了一个为21世纪计算机基本构件进行简单*计数*的工具。这是物理学统一性的一个惊人例子，一个领域的工具在另一个领域找到了新的、深刻的意义。

### 量子取证：[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)是否正确运行？

假设我们已经造好了我们的机器——无论是拓扑的还是其他的——然后我们运行一个[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，比如，寻找一个复杂分子的[基态能量](@keyword=ground_state_energy_2|lang=zh-CN|style=Feynman)。[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机执行其操作并给出一个答案。我们怎么知道它是否正确？这个设备是有噪声的，而且计算过于复杂，无法在经典计算机上核对（这正是其意义所在！）。再一次，[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学为我们所谓的“量子取证”提供了工具箱。

一个旨在寻找能量本征态的理想[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)，如果成功，应使系统处于[问题哈密顿量](@keyword=problem_hamiltonian|lang=zh-CN|style=Feynman) $H$ 的一个真实本征态 $|\psi\rangle$。这样一个态具有确定的能量，因此其能量的*方差*为零：$\sigma^2(H) = \langle H^2 \rangle - \langle H \rangle^2 = 0$。一个现实世界中的设备会产生一个既包含正确态又包含许多其他错误态的混乱叠加态。这个受污染的态将具有非零的[能量方差](@keyword=energy_variance|lang=zh-CN|style=Feynman)。因此，通过使用我们的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机测量其产生的状态的[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman) $\langle H \rangle$ 和 $\langle H^2 \rangle$，我们可以计算出方差的估计值。如果这个方差显著大于零，那么这个结果就被标记为不可信。这是对我们计算结果纯度的一个直接统计检验。[@problem_id:2931318]

另一个强大的技术涉及对称性。如果分子的哈密顿量具有某些对称性（例如，电子数量固定，[总自旋](@keyword=total_spin|lang=zh-CN|style=Feynman)特定），那么任何真实的能量本征态也必须是这些对称性算符的本征态。我们可以进行一个快速检查：在主计算之后，我们测量这些对称性。如果输出态未能通过测试——例如，如果它的电子数量不对——我们就知道计算被错误破坏了，可以丢弃那次运行。[@problem_id:2931318]

对于像[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)这样要求极高的应用，我们需要更详细的“尸检”。分子电子的完整[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)是一个极其复杂的对象。一个完整的统计描述包含在其[约化密度矩阵](@keyword=reduced_density_matrix|lang=zh-CN|style=Feynman)（RDM）中，这些矩阵描述了所有电子对、电子三联体等的关联。一次高保真度的量子模拟不仅要得到正确的能量，还必须正确地再现这些[统计关联](@keyword=statistical_association|lang=zh-CN|style=Feynman)。严格的验证涉及从[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的最终状态测量1-粒子和2-粒子RDM，并使用基不变的范数将它们与可信的参考态（如果可用）进行比较。此外，物理上有效的RDM必须满足一套严格的内部一致性规则，称为 $N$-[可表示性](@keyword=representability|lang=zh-CN|style=Feynman)条件（例如，[1-RDM](@keyword=1_rdm|lang=zh-CN|style=Feynman)的迹必须等于电子数 $N$）。检查是否违反这些条件，为认证量[子模](@keyword=submodule|lang=zh-CN|style=Feynman)拟的质量提供了一种深刻的、结构性的、纯粹基于[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的方法。[@problem_id:2797569]

从提供描述量子涨落的语言，到支撑我们硬件的稳定性，再到审查我们[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)的答案，[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的原理不仅仅是[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的附件——它们被编织进了其根本结构之中。构建[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的旅程，在许多方面，就是一场掌握一个复杂的、相互作用的、多体量子世界的统计物理学的旅程。