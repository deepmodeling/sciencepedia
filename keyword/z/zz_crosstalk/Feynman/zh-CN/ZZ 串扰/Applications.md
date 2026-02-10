## 应用与跨学科联系

在上一章中，我们深入量子领域，理解了 ZZ [串扰](@keyword=crosstalk|lang=zh-CN|style=Feynman)的物理起源。我们看到，它源于一个简单的事实：我们的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，这些承载量子信息的脆弱岛屿，从不真正孤单。它们相互耦合，这种耦合产生了 $Z \otimes Z$ 相互作用，这是哈密顿量中的一个项，使得一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的能量依赖于其邻居的状态。这是许多[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)架构中一个基本的，且往往不可避免的特性。

现在，理解了*是什么*之后，我们准备好提出一个更有趣的问题：*那又怎样*？这个看似简单的相互作用实际上*做*了什么？你可能会倾向于认为它只是一个微小、讨厌的瑕疵，是一台原本完美的机器中的一个小故障。但这将是一个严重的低估。在构建功能性[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的宏伟戏剧中，ZZ [串扰](@keyword=crosstalk|lang=zh-CN|style=Feynman)不是一个小角色；它是一个中心人物，扮演着反派、挑战者，甚至在一个令人惊讶的转折中，扮演英雄的角色。本章讲述的就是这段旅程的故事，从一个有害的误差源头到一个强大的计算工具。

### 不速之客：作为误差的 ZZ 串扰

我们与 ZZ 串扰的初次相遇几乎总把它看作是一种恶意力量，一个在机器中无声地破坏我们计算的幽灵。但在我们与之对抗之前，我们必须首先证明它的存在。

#### 探测机器中的幽灵

你如何探测一个本质上不会将[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)从 $|0\rangle$ 翻转到 $|1\rangle$ 的相互作用？你无法通过简单地测量[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)来直接看到它。相反，我们必须更加巧妙。我们必须在一个[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)的精细相位中寻找它的踪迹。用于此的首要工具是拉姆齐实验。

想象我们有两个相邻的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，一个是我们正在操作的“目标”[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，另一个是我们希望保持不变的“旁观”[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)。它们之间的 ZZ 相互作用意味着旁观[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的[谐振频率](@keyword=resonant_frequency|lang=zh-CN|style=Feynman)会根据目标[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)处于 $|0\rangle$ 态还是 $|1\rangle$ 态而发生轻微的上移或下移。这就是关键。我们可以对旁观[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)进行拉姆齐实验——将其置于叠加态，让其演化，然后将其旋转回来——并测量结果。如果我们重复这个实验，一次让目标处于 $|0\rangle$ 态，另一次让其处于 $|1\rangle$ 态，ZZ [串扰](@keyword=crosstalk|lang=zh-CN|style=Feynman)将导致旁观[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的“内部时钟”在这两种情况下以略微不同的速率滴答。结果是我们能够测量到的一个[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman)。

在某些物理系统中，这种效应甚至更为显著。[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)速率可能与频率有关。如果 ZZ 相互作用将旁观者的频率移到一个它[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)更快或更慢的区域，这将表现为[拉姆齐条纹](@keyword=ramsey_fringes|lang=zh-CN|style=Feynman)*对比度*的变化。通过观察旁观[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)根据其邻居的状态发生不同的[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)，我们不仅可以探测到 ZZ [串扰](@keyword=crosstalk|lang=zh-CN|style=Feynman)，还可以精确地量化其强度，给出耦合常数 $\zeta_{ZZ}$ 的值 [@problem_id:65720]。我们找到了那个幽灵。

#### 对量子算法的破坏

现在我们知道串扰存在了，我们可以开始认识到它造成的损害。量子算法是干涉的交响乐。它们通过精心编排大量的计算路径，让这些路径以恰到好处的方式相互抵消和加强，最终留下正确的答案。ZZ 串扰是这场交响乐中的破坏者。

通过向[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)添加一个不必要的、依赖于状态的相位“踢”，它破坏了这种精巧的干涉模式。考虑 Deutsch-Jozsa [算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，这是[量子加速](@keyword=quantum_speedup|lang=zh-CN|style=Feynman)的一个经典例子。对于一个常数函数，该[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)被设计成以 100% 的确定性产生全零状态 $|00\dots0\rangle$。干涉是完美的。但如果在神谕（oracle）操作期间在输入[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)之间引入 ZZ [串扰](@keyword=crosstalk|lang=zh-CN|style=Feynman)，这种完美就被打破了。由 $U_{err} = \exp(-i \theta \sum_{j} Z_j Z_{j+1})$ 这样的幺[正算符](@keyword=positive_operator|lang=zh-CN|style=Feynman)描述的寄生相位，意味着路径不再完美抵消。突然之间，测量到*非* $|00\dots0\rangle$ 状态的概率变为非零，从而导致我们错误地断定函数是平衡的 [@problem_id:151393]。

这种破坏是一个普遍的特征。在任何涉及多个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)中，例如[量子傅里叶变换](@keyword=quantum_fourier_transform|lang=zh-CN|style=Feynman)，应用于一对[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的门可能会在旁观者身上引起串扰[相位误差](@keyword=phase_error|lang=zh-CN|style=Feynman)。这个误差可以填充在理想执行中本应为零幅度的计算状态，实际上导致[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)“泄漏”到[希尔伯特空间](@keyword=hilbert_spaces|lang=zh-CN|style=Feynman)的错误部分。最终结果是正确答案与一系列错误答案的叠加，看到错误答案的概率随着串扰的强度和持续时间而增长，通常为 $\sin^2(\phi_{err})$，其中 $\phi_{err}$ 是累积的误差相位 [@problem_id:65620]。

#### 更深层次的威胁：误导搜索

对于当今的含噪声中等规模量子（NISQ）计算机而言，问题甚至更深。许多流行的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，如[变分量子本征求解器](@keyword=variational_quantum_eigensolver|lang=zh-CN|style=Feynman)（VQE），并不遵循一个单一的、预先写好的乐谱。相反，它们是探索性的。它们的工作方式是制备一个参数化的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，测量一个[代价函数](@keyword=loss_functions|lang=zh-CN|style=Feynman)（如分子的能量），然后使用一个经典优化器来“引导”参数走向最小代价。这个“引导指令”就是[代价函数](@keyword=loss_functions|lang=zh-CN|style=Feynman)相对于电路参数的梯度。

在这里，ZZ 串扰揭示了其最阴险的本性。它不仅仅是在最终答案中增加噪声；它破坏了引导指令本身。像 CNOT 门期间的 ZZ 相互作用这样的[相干误差](@keyword=coherent_error|lang=zh-CN|style=Feynman)，可以系统地偏置测量的梯度。依赖于这个错误信息的优化器会被引向歧途，就像一个使用系统性倾斜的指南针的徒步旅行者。它可能会被困在错误的峡谷中，或者在景观上漫无目的地徘徊，永远找不到真正的解。这种梯度偏置是变分[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)成功的一个关键障碍，将本应是引导下降的过程变成了一场令人沮丧的误导性搜索 [@problem_id:102824]。

#### 终极挑战：破坏[容错](@keyword=fault_tolerance|lang=zh-CN|style=Feynman)性

克服所有量子误差的宏伟愿景，当然是[量子纠错](@keyword=quantum_error_correction|lang=zh-CN|style=Feynman)（QEC）。通过将单个逻辑量子比特编码到许多物理量子比特的集体状态中，我们可以在错误发生时检测并纠正它们。像[表面码](@keyword=surface_codes|lang=zh-CN|style=Feynman)这样的编码旨在防护局部的、不相关的物理错误。但 ZZ [串扰](@keyword=crosstalk|lang=zh-CN|style=Feynman)直击这一策略的核心。

首先，QEC 过程本身涉及电路——用于测量错误诊断信息（syndrome）的电路。这些电路使用[辅助量子比特](@keyword=ancilla_qubit|lang=zh-CN|style=Feynman)来检查像 $Z_1 Z_2$ 这样的[稳定子算符](@keyword=stabilizer_operators|lang=zh-CN|style=Feynman)。如果在这次测量过程中，数据[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)和[辅助量子比特](@keyword=ancilla_qubit|lang=zh-CN|style=Feynman)之间存在 ZZ 串扰，会发生什么？[辅助量子比特](@keyword=ancilla_qubit|lang=zh-CN|style=Feynman)可能被欺骗，报告错误的诊断值。一个已经发生的错误可能被错过，或者一个不存在的错误可能被“检测”到，导致一次实际上是附加错误的“纠正”。看门狗本身正在被腐化 [@problem_id:119662]。

更可怕的是相关逻辑错误的威胁。许多 QEC 码的力量来自于物理错误是局部的和独立的这一假设。这里一个比特翻转，那里一个相位翻转。编码可以处理这些。但 ZZ 串扰是一个*相关*错误；它天生就涉及两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)。想象一个场景，受串扰影响的两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，比如 $q_1$ 和 $q_2$，恰好是定义该编码的一个逻辑算符的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，例如 $Z_L = Z_1 Z_2$。在门操作期间的一个寄生 ZZ 相互作用，$H_{err} = J_{ZZ} Z_1 Z_2$，在数学上就与在编码[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)上的一个非预期的*逻辑旋转*无法区分。一个单一的物理故障事件就产生了一个编码完全无法察觉的高权重逻辑错误。这是[容错](@keyword=fault_tolerance|lang=zh-CN|style=Feynman)的噩梦场景，噪声的结构与编码的结构完美对齐，导致一个无法检测的失败 [@problem_id:84695]。

### 驯服野兽：从缓解到操控

到目前为止，情况似乎很黯淡。ZZ 串扰似乎是一头多头蛇，攻击着我们的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)、我们的优化例程以及我们对容错的希望。但这并不是故事的结局。物理学带来的每一个挑战，它也提供了解决方案。我们旅程的下一部分是学习如何反击。

#### 软件补丁：[量子误差缓解](@keyword=quantum_error_mitigation|lang=zh-CN|style=Feynman)

第一道防线是软件。如果我们不能建造一台完美的机器，也许我们可以聪明地使用我们不完美的机器。这就是[量子误差缓解](@keyword=quantum_error_mitigation|lang=zh-CN|style=Feynman)（QEM）的哲学。这个想法既简单又强大：如果你能表征一个误差，你就可以尝试在计算上逆转它的影响。

通过我们的表征实验，我们可以建立一个非常精确的[串扰](@keyword=crosstalk|lang=zh-CN|style=Feynman)误差模型，比如 $U_{err} = \exp(-i\alpha Z_c Z_s)$。我们知道这个误差将会发生。所以，与其尝试测量我们[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的[可观测量](@keyword=observables|lang=zh-CN|style=Feynman) $O$，我们可以选择测量一个不同的、“修正后”的[可观测量](@keyword=observables|lang=zh-CN|style=Feynman) $\tilde{O}$。这个新的可观测量被构造成，它在*含噪声*最终态中的[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman)等于*原始*可观测量在*理想*最终态中的[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman)。我们[实质](@keyword=parenchyma|lang=zh-CN|style=Feynman)上是在预先扭曲我们的测量，以抵消来自噪声的扭曲。这涉及到将修正后的可观测量表示为其他易于测量的泡利算符的[线性组合](@keyword=linear_combinations|lang=zh-CN|style=Feynman)。例如，为了在测量 $X_c$ 时校正一个 $Z_c Z_s$ 误差，我们可能需要测量 $X_c$ 和 $Y_c Z_s$ 的组合 [@problem_id:121313]。这是一个利用我们对误差的知识在后处理中撤销它的绝佳例子。

#### 以物理对抗物理：主动误差消除

软件缓解是一个出色的补丁，但它有其代价。一个更优雅的解决方案是在硬件层面防止误差。在这里，我们真正开始驯服这头野兽，用我们对物理的理解来以火攻火。

许多量子系统有一个静态的、始终存在的 ZZ 相互作用 $\zeta_0$，我们很想摆脱它。同时，我们用来执行门的微波脉冲本身可以通过[交流斯塔克效应](@keyword=ac_stark_effect|lang=zh-CN|style=Feynman)引入新的相互作用。这种效应会响应驱动而移动[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的能级。关键是，施加在一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)上的驱动可以产生一个新的 ZZ 相互作用项 $\chi_{AC}$，其强度取决于驱动幅度。机会就在这里。我们能否选择我们的驱动参数，不仅执行[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的门（如 iSWAP），而且还产生一个与静态 ZZ 项大小相等、方向相反的斯塔克位移诱导的 ZZ 项？也就是说，我们能否设计我们的驱动，使得 $\chi_{tot} = \zeta_0 + \chi_{AC} = 0$？

答案是肯定的。通过仔细选择双音驱动的幅度和频率，我们可以同时实现两个目标：驱动[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的双[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)门动力学，*并且*让物理学的一部分（[交流斯塔克位移](@keyword=ac_stark_shift|lang=zh-CN|style=Feynman)）的不良副作用，精确地抵消另一部分（静态耦合）的不良副作用。这是一项惊人的[量子控制](@keyword=quantum_control|lang=zh-CN|style=Feynman)壮举，将控制场变成了一个实时主动塑造系统哈密顿量的工具 [@problem_id:70618]。

#### 英雄的转变：Bug 变成 Feature

我们已经追踪了反派，见证了他的破坏力，并学会了用软件和硬件来对付他。但物理学中最深刻的教训往往是，没有真正的反派，只有力和相互作用。我们称之为“bug”或“feature”的，仅仅是视角和控制方式的问题。我们故事的最后一部分证明了这一思想。

让我们停止试图消灭 ZZ 相互作用，而是问：我们能*利用*它吗？

想象一下，我们用一种特殊的方式来编码我们的逻辑量子比特，使用一个“退相干自由子空间”（DFS）。例如，我们可以将我们的逻辑态定义为 $|0_L\rangle = |01\rangle$ 和 $|1_L\rangle = |10\rangle$ 。这种聪明的编码方式天然地对某些类型的噪声免疫。现在，如果我们的系统中有一个自然的 $ZZ$ 相互作用 $H_{ZZ} = J Z_1 Z_2$ 会发生什么？这正是我们一直在对抗的那个项。但作用在我们的逻辑态上时，它虽然对两个逻辑[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)施加相同的相位（在逻辑层面是一个[全局相位](@keyword=global_phase|lang=zh-CN|style=Feynman)），但它为通过外部场进行逻辑操作提供了必要的[能谱](@keyword=energy_spectrum|lang=zh-CN|style=Feynman)结构。

通过将这种在 ZZ 相互作用下的“自由”演化与简单的全局脉冲（如同时旋转两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)）相结合，我们可以合成一整套*[逻辑门](@keyword=logic_gates|lang=zh-CN|style=Feynman)*。这个曾经不受欢迎的相互作用，成为了驱动我们在受保护子空间内进行计算的引擎。我们不再是消除[串扰](@keyword=crosstalk|lang=zh-CN|style=Feynman)，而是将其作为一种计算资源来利用。问题变成了解决方案。一个全局脉冲、一段 ZZ 演化时间、再加一个全局脉冲的序列，可以创造一个逻辑 $\sqrt{\mathrm{NOT}}$ 门，将 bug 变成了我们量子处理器的一个基本特性 [@problem_id:176786]。

### 一个相互联系的故事

ZZ 相互作用的旅程，从拉姆齐实验中的一个微小偏移，到逻辑门的引擎，是整个[量子工程](@keyword=quantum_engineering|lang=zh-CN|style=Feynman)领域的缩影。它教导我们，构建[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的道路并非是寻找完美的、孤立的组件。而是要深入理解支配量子世界的丰富而复杂的相互作用网络，并学会以日益精湛的技巧来驾驭和操控这个网络。我们对现实的物理描述中完全相同的项，$Z \otimes Z$，可以是一个失败的根源，一个需要克服的挑战，或者一个可以挥舞的工具。它的故事有力地提醒我们物理学内在的美和统一性，并激动人心地预示了将[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的全部力量变为现实所需的那种独创性。