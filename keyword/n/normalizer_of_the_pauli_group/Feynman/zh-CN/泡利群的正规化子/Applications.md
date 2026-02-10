## 应用与跨学科联系

既然我们已经领略了[泡利群](@keyword=pauli_group|lang=zh-CN|style=Feynman)及其[正规化子](@keyword=normalizer|lang=zh-CN|style=Feynman)——[克利福德群](@keyword=clifford_group|lang=zh-CN|style=Feynman)——的形式之舞，你可能会问：这到底有什么用？毫无疑问，这是一段优美的数学，但它仅仅是供理论家消遣的好奇心之物吗？答案是一个响亮的“不”，我希望你会和我一样觉得这个答案令人愉悦。这个优雅的[代数结构](@keyword=algebraic_structure|lang=zh-CN|style=Feynman)并非只是装饰品；它是我们希望能借以构建功能性[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的基石。它是量子领域中保护、计算乃至噪声的秘密语言。现在让我们来探索几个让这个思想大放异彩的领域。

### [量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)的守护者

[正规化子](@keyword=normalizer|lang=zh-CN|style=Feynman)最直接、最关键的作用在于保护脆弱的[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)。[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)是个精细的东西，极易被与外界最微小的相互作用所干扰。量子纠错的绝妙思想并非阻止错误发生，而是巧妙地编码信息，使得错误可以被检测和逆转，而无需查看信息本身。

这就是我们的朋友——[稳定子群](@keyword=stabilizer_subgroup|lang=zh-CN|style=Feynman) $S$ 及其[正规化子](@keyword=normalizer|lang=zh-CN|style=Feynman) $N(S)$ ——登场的地方。把[稳定子群](@keyword=stabilizer_subgroup|lang=zh-CN|style=Feynman)想象成一套“规则”或“检查”。我们受保护的编[码空间](@keyword=codespace|lang=zh-CN|style=Feynman)中的任何状态都必须是“有效信息”，这意味着它通过了所有这些检查（它被 $S$ 中的每个算子所稳定）。错误是某个意外作用于我们状态的泡利算子。我们的任务是看这个错误是否扰乱了我们的检查。

逻辑算子——即允许我们操纵编码后[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的操作——位于[正规化子](@keyword=normalizer|lang=zh-CN|style=Feynman) $N(S)$ 中。为什么？因为来自 $N(S)$ 的算子具有一个特殊性质：当它作用于一个状态时，会将其转换为另一个 *同样* 遵守编码规则的状态。换句话说，它将有效信息映射到有效信息。其中一些是“平凡”的逻辑操作；这些就是稳定子本身，它们根本不改变编码的信息。真正有趣的是在集合 $N(S) \setminus S$ 中找到的非平凡逻辑算子。这些就是作用于我们编码后[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的逻辑 $X_L$、$Y_L$ 和 $Z_L$ 算子。

一个编码的强度由它无法检测的最小错误的“大小”决定，这对应于最小的非平凡逻辑算子。例如，在著名的 Shor 九[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)码中，你能构建的最简单的逻辑算子是作用于三个不同[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的泡利串。这意味着任何单位[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)错误，甚至是双[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)错误，都将是可检测和可纠正的。$N(S) \setminus S$ 中算子的最小权重，即所谓的码距，是其恢复能力的直接度量。

真正非凡的是，由[商群](@keyword=factor_groups|lang=zh-CN|style=Feynman) $N(S)/S$ 表示的这些逻辑算子集合，其本身构成了一个群，其行为就像一个受到良好保护的单[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的[泡利群](@keyword=pauli_group|lang=zh-CN|style=Feynman)一样。我们利用了一个由许多[物理量子比特](@keyword=physical_qubit|lang=zh-CN|style=Feynman)及其相关算子组成的复杂系统，提炼出了一个单一、鲁棒的[逻辑量子比特](@keyword=logical_qubits|lang=zh-CN|style=Feynman)的精髓。

这个思想最令人惊叹的应用体现在[拓扑码](@keyword=topological_codes|lang=zh-CN|style=Feynman)中。在这里，编码信息并非存储在任意一小组[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)中，而是存储在一个大[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的全局拓扑性质中，就像画在甜甜圈表面上的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)一样。逻辑算子不再是小的、局域的物体，而是环绕甜甜圈孔洞的、广阔的、非局域的泡利算子“带”或“环”。要造成一个逻辑错误，你必须创建一个环绕整个表面的相关错误串——这是一个极不可能发生的事件。对于一个有 $g$ 个孔的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)（亏格为 $g$ 的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)），你可以编码 $2g$ 个逻辑量子比特，从而产生一个大小为 $4^{2g}$ 的非等价逻辑泡利算[子群](@keyword=subgroup|lang=zh-CN|style=Feynman)。在这里，[正规化子](@keyword=normalizer|lang=zh-CN|style=Feynman)的[抽象代数](@keyword=abstract_algebra|lang=zh-CN|style=Feynman)与[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的几何学完美结合，创造出一种近乎诗意的信息保护形式。

### 量子会计师的工具箱

构建一台能够解决现实世界问题——例如为药物发现或[材料科学模拟](@keyword=materials_science_simulation|lang=zh-CN|style=Feynman)复杂分子的行为——的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机是一项艰巨的任务。即使是一个中等大小分子的量子描述，也可能涉及一个由成千上万甚至数百万个不同泡利串项组成的哈密顿量（能量算子）。为了找到基态能量，就像在[变分量子本征求解器](@keyword=variational_quantum_eigensolver|lang=zh-CN|style=Feynman)（VQE）[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)中所做的那样，必须测量这个庞大总[和的期望值](@keyword=expected_value_of_sum|lang=zh-CN|style=Feynman)。

一个天真的方法是逐一测量每个泡利项。这将慢得令人无法接受。但在这里，[克利福德群](@keyword=clifford_group|lang=zh-CN|style=Feynman)前来救场。关键的洞见是，如果一组泡利算子都相互对易，它们就可以被同时测量。但“同时”意味着什么？这意味着存在一个单一的[基变换](@keyword=change_of_basis|lang=zh-CN|style=Feynman)，能使它们全部[同时对角化](@keyword=simultaneous_diagonalization|lang=zh-CN|style=Feynman)。神奇的是，这个[基变换](@keyword=change_of_basis|lang=zh-CN|style=Feynman)操作总是一个克利福德酉操作！

于是，策略便是将庞大的哈密顿量项列表分割成多个相互对易算子的小组。对每个小组，我们可以计算一个特定的[克利福德电路](@keyword=clifford_circuits|lang=zh-CN|style=Feynman)，它将整个小组旋转成仅由 $Z$s 和 $I$s 组成的算子。应用此电路后，在计算基下对所有[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)进行单次测量，会得到一个比特串。通过简单的经典后处理，我们可以从这一个比特串中计算出该组中 *每一个算子* 的测量结果。这个过程不仅提供了小幅加速；它将我们需要运行的不同量子电路的数量减少了几个数量级，将一项不可能的任务变成了一项仅仅是非常、非常困难的任务。[泡利群的正规化子](@keyword=normalizer_of_the_pauli_group|lang=zh-CN|style=Feynman)不仅仅是一个理论概念；它是一个实用工具，使在[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机上进行[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)成为一项可行的事业。

### 通往[通用计算](@keyword=universal_computation|lang=zh-CN|style=Feynman)的门户

[克利福德群](@keyword=clifford_group|lang=zh-CN|style=Feynman)非常有用，但它有一个局限：任何完全由[克利福德门](@keyword=clifford_gates|lang=zh-CN|style=Feynman)组成的量子电路都可以在[经典计算](@keyword=classical_computation|lang=zh-CN|style=Feynman)机上被高效模拟。要释放[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的全部指数级威力，我们至少需要一个“非克利福德”门，例如著名的 $T$ 门。这带来一个难题：使得[克利福德门](@keyword=clifford_gates|lang=zh-CN|style=Feynman)易于[容错](@keyword=fault_tolerance|lang=zh-CN|style=Feynman)实现的那些特性，恰恰与使它们经典可模拟的结构相关联。我们如何在不破坏保护的情况下，在精心保护的逻辑量子比特上实现一个[非克利福德门](@keyword=non_clifford_gates|lang=zh-CN|style=Feynman)呢？

答案是一种名为“魔术态注入”的巧妙协议。策略是把所有“危险”的工作离线完成。我们准备一个[辅助量子比特](@keyword=ancilla_qubit|lang=zh-CN|style=Feynman)，使其处于一个特殊的、非[稳定子态](@keyword=stabilizer_states|lang=zh-CN|style=Feynman)，称为魔术态。然后，仅使用“安全”的[容错](@keyword=fault_tolerance|lang=zh-CN|style=Feynman)克利福德操作（如[CNOT门](@keyword=cnot_gate|lang=zh-CN|style=Feynman)）和对我们[逻辑量子比特](@keyword=logical_qubits|lang=zh-CN|style=Feynman)的投影测量，我们就可以有效地将非克利福德 $T$ 门的作用“传送”到我们的数据上。如果测量得到一种结果，门就完美地应用了。如果得到另一种结果，数据会得到一个不想要的、但已知的克利福德副产物。我们只需应用另一个[克利福德门](@keyword=clifford_gates|lang=zh-CN|style=Feynman)来纠正它！[正规化子](@keyword=normalizer|lang=zh-CN|style=Feynman)提供了实现那些超出其自身计算能力的门所需的容错脚手架。它给了我们一个由“简单”操作组成的鲁棒框架，然后我们用它作为资源，通过[自举](@keyword=bootstrapping|lang=zh-CN|style=Feynman)的方式达到完全的、通用的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)。

### 结构与对称性的语言

一个强大的科学思想很少局限于其原始领域。它的回响常常在不同领域中被听到，揭示出一种潜在的统一性。[泡利群](@keyword=pauli_group|lang=zh-CN|style=Feynman)[正规化子](@keyword=normalizer|lang=zh-CN|style=Feynman)的数学就是这样一个思想。

在[纠错码](@keyword=error_correcting_codes|lang=zh-CN|style=Feynman)的形式理论中，存在着被称为 [MacWilliams 恒等式](@keyword=macwilliams_identity|lang=zh-CN|style=Feynman)的深刻数学关系。这些源于[经典信息论](@keyword=classical_information_theory|lang=zh-CN|style=Feynman)的恒等式，在量子世界中找到了美丽的新生。它们在[稳定子群](@keyword=stabilizer_subgroup|lang=zh-CN|style=Feynman) $S$ 和其[正规化子](@keyword=normalizer|lang=zh-CN|style=Feynman) $N(S)$ 之间建立了一种深刻的对偶性。[正规化子](@keyword=normalizer|lang=zh-CN|style=Feynman)的权重枚举子——一个追踪每个可能权重下算子数量的多项式——可以直接从稳定子的权重枚举子计算出来。这意味着所有逻辑算子和可检测错误的完整分布，在数学上受到编码初始定义的约束，并可由其推导出来。这就像通过研究投射影子的物体来理解影子的详细属性一样。

更为精妙的是，[正规化子](@keyword=normalizer|lang=zh-CN|style=Feynman)的结构帮助我们理解和表征真实量子设备中的噪声。当一个量子[系统与环境](@keyword=system_and_surroundings|lang=zh-CN|style=Feynman)相互作用时，产生的[信道](@keyword=information_channel|lang=zh-CN|style=Feynman)并不总是完全随机的。系统动力学中的对称性约束了噪声的形式。一个“克利福德协变”[信道](@keyword=information_channel|lang=zh-CN|style=Feynman)是一个尊重[克利福德群](@keyword=clifford_group|lang=zh-CN|style=Feynman)对称性的噪声过程。对于一个 $d$ 维 qudit，存在多少种这种对称噪声的基本“类型”？令人惊讶的是，答案与[泡利群](@keyword=pauli_group|lang=zh-CN|style=Feynman)在[克利福德群](@keyword=clifford_group|lang=zh-CN|style=Feynman)[共轭作用](@keyword=action_by_conjugation|lang=zh-CN|style=Feynman)下的轨道数有关。而这个数字又等于维度 $d$ 的因子数。这个惊人的结果将[正规化子](@keyword=normalizer|lang=zh-CN|style=Feynman)的[抽象代数](@keyword=abstract_algebra|lang=zh-CN|style=Feynman)结构与建模和缓解困扰当今量子硬件的操作错误的极其务实的任务联系起来。

从利用[拓扑保护](@keyword=topological_protection|lang=zh-CN|style=Feynman)信息，到在近期设备上运行[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，甚至表征噪声本身的性质，[泡利群的正规化子](@keyword=normalizer_of_the_pauli_group|lang=zh-CN|style=Feynman)被证明远不止是一个数学注脚。它是[量子信息科学](@keyword=quantum_information_science|lang=zh-CN|style=Feynman)的统一概念之一，证明了对抽象、优雅结构的追求如何能直接引导我们找到构建新科技世界所需的工具。