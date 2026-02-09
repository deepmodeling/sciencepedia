## 应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系

好了，我们已经花了不少时间来讨论[量子信道](@keyword=quantum_channels|lang=zh-CN|style=Feynman)如何工作的细节……但这到底是为了什么呢？你可能会觉得这不过是理论家们的一些抽象游戏。但是，我在这里想告诉你，这个“信息能多好地被保存下来？”的问题，几乎是我们对量子未来所有梦想的核心。不仅如此，它还是一根金线，将工程师的工作室、物理学家的黑板和宇宙最深邃的奥秘联系在一起。让我们拉一拉这根线，看看它会把我们带向何方。

### [量子工程](@keyword=quantum_engineering|lang=zh-CN|style=Feynman)师的试炼场：构建[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机

我们旅程的第一站是[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的前沿。建造一台功能强大的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机是这个时代的伟大梦想之一。但现实是，我们的基本构件——量子门——并非完美无瑕。

#### 计算的原子：不完美的门

拿[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的主力“[受控非门](@keyword=cnot_gate|lang=zh-CN|style=Feynman) (CNOT)”来说。当你试图在实验室里实现它时，它并不会完美地执行任务。它可能会有点“[抖动](@keyword=dither|lang=zh-CN|style=Feynman)”。我们可以将这种[抖动](@keyword=dither|lang=zh-CN|style=Feynman)建模为`退偏振噪声`（depolarizing noise）：在一定的概率下，[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的状态会被[随机化](@keyword=randomization|lang=zh-CN|style=Feynman)，就像一个微弱的广播信号消失在静电噪声中一样 [@problem_id:92547]。或者，错误之间可能是`关联的`（correlated）——一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)上的错误会使其邻居上发生错误的可能性增加 [@problem_id:92483]。

更微妙的是，错误可能是`相干的`（coherent）。想象一下，你试图将一个旋钮精确地旋转90度，但你总是系统性地转到91度。这不是随机的，而是一个系统性的偏差。在[量子门](@keyword=quantum_computing_gates|lang=zh-CN|style=Feynman)中，这种“过旋转”错误同样具有破坏性 [@problem_id:92445]。像`平均门保真度`（average gate fidelity）这样的工具，为我们提供了一种精确评估这些不完美构件性能的方法。

#### 运行程序：嘈杂世界中的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)

一个门的微小瑕疵似乎无伤大雅，但一个量子算法是成千上万个门的序列。想象一场精密的芭蕾舞，每一步都必须完美无缺。几个小小的失误就可能毁掉整场演出。我们可以在一个有缺陷的Grover[搜索算法](@keyword=search_algorithms|lang=zh-CN|style=Feynman)中看到这一点：如果“标记”目标的“神谕”（oracle）操作有一个微小的相干错误，整个[搜索算法](@keyword=search_algorithms|lang=zh-CN|style=Feynman)的性能就会下降，而我们可以用`[纠缠保真度](@keyword=entanglement_fidelity|lang=zh-CN|style=Feynman)`（entanglement fidelity）来量化这种性能的衰减 [@problem_id:92525]。

#### 量子安全网：纠错码

那么工程师该怎么办？放弃吗？不！我们编织了一张安全网：量子纠错。我们把自己宝贵的一个[逻辑量子比特](@keyword=logical_qubits|lang=zh-CN|style=Feynman)的信息，“涂抹”在多个[物理量子比特](@keyword=physical_qubit|lang=zh-CN|style=Feynman)上，就像把一句秘密信息编码在一个冗长、重复的句子里一样。以简单的三比特“比特翻转码”为例，即使其中一个物理量子比特被意外翻转，我们仍然可以检测到并修正这个错误。但如果我们的*纠错设备本身*也是嘈杂的呢？例如，用于恢复操作的[Toffoli门](@keyword=toffoli_gate|lang=zh-CN|style=Feynman)可能自身就受到退偏振噪声的影响。此时，我们可以计算`逻辑保真度`（logical fidelity），来评估我们所*保护*的信息在经历了这整个充满噪声的过程后幸存得如何 [@problem_id:92493]。这正是[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的终极目标：构建[容错](@keyword=fault_tolerance|lang=zh-CN|style=Feynman)系统，即使物理部件性能平平，逻辑信息的保真度也能达到极高水平。

#### 更深层次的保护：自然的智慧

还有没有更巧妙的方法呢？我们能否找到一些系统，让大自然亲自为我们提供保护？在奇异的[拓扑物质](@keyword=topological_matter|lang=zh-CN|style=Feynman)世界中，存在着这样一种[物态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)：[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)被非局域地编码在系统纠缠的“纹理”之中。例如，在[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，电子的`[费米子宇称](@keyword=fermion_parity|lang=zh-CN|style=Feynman)`（fermion parity）是一个[守恒量](@keyword=conserved_quantity|lang=zh-CN|style=Feynman)，它创造了一个`[超选择定则](@keyword=superselection_rules|lang=zh-CN|style=Feynman)`（superselection rule）。这个定则就像一条神圣的法令，禁止任何局域的、保持宇称的噪声将我们的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)踢出其受保护的逻辑空间 [@problem_id:3021975]。这是一个美妙的想法：在希尔伯特空间中找到一个安静的避风港，由自然法则亲自站岗。

### 超越计算机：编织[量子网络](@keyword=quantum_networks|lang=zh-CN|style=Feynman)与锐化我们的感官

现在，让我们把视野从计算扩展到通信和测量。

#### 发送一封量子信：距离的挑战

我们不仅想计算，还想通信。但将一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)通过[光纤](@keyword=optical_fiber|lang=zh-CN|style=Feynman)发送出去并非易事。信号会被吸收（一个`纯粹损耗[信道](@keyword=information_channel|lang=zh-CN|style=Feynman)`），而[信号放大](@keyword=signal_amplification|lang=zh-CN|style=Feynman)器又会引入自身的噪声。我们可以通过级联这些[信道](@keyword=information_channel|lang=zh-CN|style=Feynman)来模拟一个真实的[光纤](@keyword=optical_fiber|lang=zh-CN|style=Feynman)链路，并计算其最终的`经典容量`（classical capacity）——即每秒可以可靠地传输多少经典比特 [@problem_id:92386]。为了实现长距离通信，我们需要量子中继器。它们不是放大信号，而是在中间节点执行一种名为`[纠缠交换](@keyword=entanglement_swapping|lang=zh-CN|style=Feynman)`（entanglement swapping）的量子魔法。通过分析每一段链路的保真度，我们可以确定整个中继器链的`[量子容量](@keyword=quantum_capacity|lang=zh-CN|style=Feynman)`（quantum capacity），它告诉我们每秒钟可以分发多少纠缠 [@problem_id:92572]。

#### 测量艺术：推动精度的极限

让我们反过来思考这个问题。与其保护一个已知的状态，不如尝试从一个状态中提取未知的信息。假设一个[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)被一个微小的、未知的角度 $\theta$ 旋转了。我们希望尽可能精确地测量 $\theta$。我们的测量精度极限由`[量子费雪信息](@keyword=quantum_fisher_information|lang=zh-CN|style=Feynman)`（Quantum Fisher Information）决定。如果制备我们探测态的[信道](@keyword=information_channel|lang=zh-CN|style=Feynman)本身就是嘈杂的，比如在旋转发生*之前*就遭受了`振幅阻尼`（amplitude damping），那么我们估计 $\theta$ 的能力就会下降 [@problem_id:92408]。因此，[信息保存](@keyword=information_preservation|lang=zh-CN|style=Feynman)的能力与测量的精度直接相关。

#### 记忆的阴影：当过去徘徊不散

如果引起噪声的“环境”有记忆，情况会怎样？例如，如果一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)与环境中的某个粒子相互作用了两次，而这个粒子在两次相互作用之间没有被重置，那么第二次错误就会“记住”第一次错误。这种非马尔可夫（non-Markovian）的记忆效应使问题变得更加复杂，但也更加贴近现实。我们可以计算`[相干信息](@keyword=coherent_information|lang=zh-CN|style=Feynman)`（coherent information），来研究这种记忆效应如何影响[信道](@keyword=information_channel|lang=zh-CN|style=Feynman)传输[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)的能力 [@problem_id:92381]。或者，错误可能在空间和时间上都是关联的，就像在一个嘈杂的[量子存储器](@keyword=quantum_memory|lang=zh-CN|style=Feynman)中一样，我们同样可以计算其容量来理解这些记忆效应 [@problem_id:92451]。

### 物理学家的游乐场：从[量子物质](@keyword=quantum_matter|lang=zh-CN|style=Feynman)到浩瀚宇宙

现在，让我们进入最激动人心的部分，将我们的主题与物理学的前沿联系起来。

#### 窃听量子世界：作为[信道](@keyword=information_channel|lang=zh-CN|style=Feynman)的环境

环境并非一个没有面孔的、被动的“浴缸”，它本身就是一个迷人的量子系统！想象一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)与一块量子磁铁相互作用，这块磁铁可以用著名的`[横场伊辛模型](@keyword=transverse_field_ising_model|lang=zh-CN|style=Feynman)`（transverse-field Ising model）来描述。[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)信息的衰减过程——用`[纠缠保真度](@keyword=entanglement_fidelity|lang=zh-CN|style=Feynman)`来衡量——就成了一个探测这块磁铁复杂动力学的探针，尤其是在其`[量子临界点](@keyword=quantum_critical_point|lang=zh-CN|style=Feynman)`附近 [@problem_id:92444]。或者，这个环境可能是一团囚禁在[光晶格](@keyword=optical_lattices|lang=zh-CN|style=Feynman)中的超冷原子，一个`玻色-哈勃`（Bose-Hubbard）系统。我们的探测[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的保真度损失，同样揭示了这种奇异物态的性质 [@problem_id:92489]。在这里，[信息损失](@keyword=information_loss|lang=zh-CN|style=Feynman)本身变成了一种科学发现的工具。

#### 知识的代价：信息与[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)

纠正错误是免费的吗？当然不。[Landauer原理](@keyword=landauer_s_principle|lang=zh-CN|style=Feynman)告诉我们，擦除一个经典比特需要消耗能量。在量子世界里，情况也是如此。为了逆转一个`振幅阻尼[信道](@keyword=information_channel|lang=zh-CN|style=Feynman)`的影响——即将状态的保真度恢复到接近其原始值——我们必须执行一个恢复操作。这个操作降低了[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的熵，而这些熵必须被“倾倒”到某个地方。我们可以计算出，为了达到某个目标保真度，所需要的最小`[热力学熵](@keyword=thermodynamic_entropy|lang=zh-CN|style=Feynman)产生`是多少。这构成了[信息论与热力学](@keyword=information_theory_and_thermodynamics|lang=zh-CN|style=Feynman)之间一道美丽的桥梁 [@problem_id:92420]。更有甚者，我们愿意对一个热环境做多少`功`，与我们能实现的[信道](@keyword=information_channel|lang=zh-CN|style=Feynman)的`[纠缠保真度](@keyword=entanglement_fidelity|lang=zh-CN|style=Feynman)`之间，存在着一种明确的权衡关系 [@problem_id:92482]。[信息是物理的](@keyword=information_is_physical|lang=zh-CN|style=Feynman)，操纵它必然有物理代价。

#### [时空](@keyword=space_time|lang=zh-CN|style=Feynman)边缘的信息：引力、加速与[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)

最后，让我们仰望宇宙本身。想象你正坐在一艘飞船里猛烈加速。[Unruh效应](@keyword=unruh_effect|lang=zh-CN|style=Feynman)告诉你，在一位惯性观察者看来空无一物的空间，在你看来却是一个温暖的[热浴](@keyword=heat_bath|lang=zh-CN|style=Feynman)。这种热噪声就像一个[量子信道](@keyword=quantum_channels|lang=zh-CN|style=Feynman)。如果一位惯性系的朋友Alice试图向你发送一个纠缠[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，这个纠缠会因为你的加速而退化 [@problem_id:92567]。你们之间通信的`私密经典容量`（private classical capacity）也是有限的 [@problem_id:92528]。[时空](@keyword=space_time|lang=zh-CN|style=Feynman)本身的结构，就是一个嘈杂的[量子信道](@keyword=quantum_channels|lang=zh-CN|style=Feynman)！

这自然而然地将我们引向了终极[信道](@keyword=information_channel|lang=zh-CN|style=Feynman)：[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)。当你把一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)扔进[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)，它的信息是永恒地消失了，还是以某种方式保存了下来？这就是著名的[信息佯谬](@keyword=information_paradox|lang=zh-CN|style=Feynman)。我们可以构建简单的玩具模型来探索它。一个`置乱[酉演化](@keyword=unitary_evolution|lang=zh-CN|style=Feynman)`（scrambling unitary）将[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的信息与[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)内部的[状态混合](@keyword=state_mixing|lang=zh-CN|style=Feynman)在一起。然后我们可以问：有多少信息保留在了[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)内部（$F_{int}$），又有多少信息可以从出射的“[霍金辐射](@keyword=hawking_radiation|lang=zh-CN|style=Feynman)”中重建（$F_{rad}$）？一个简单的计算揭示了一种非平凡的权衡关系，表明信息被同时分割在了内外两部分 [@problem_id:514585]。

更进一步，我们可以用一个*随机*的[酉变换](@keyword=unitary_transformation|lang=zh-CN|style=Feynman)来[模拟黑洞](@keyword=analogue_black_holes|lang=zh-CN|style=Feynman)的混沌置乱行为，这是由Don Page开创的模型。然后，我们可以计算这个“平均[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)[信道](@keyword=information_channel|lang=zh-CN|style=Feynman)”的`[相干信息](@keyword=coherent_information|lang=zh-CN|style=Feynman)`。结果令人震惊：对于一个“年老”的[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)（一个已经辐射掉超过一半质量的[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)），其[相干信息](@keyword=coherent_information|lang=zh-CN|style=Feynman)是负的 [@problem_id:92561]。这意味着没有新的[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)可以通过[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)传输；它所有的信息都已经在辐射中了。一个为量子通信设计的概念，为我们理解引力与量子力学的本质，提供了深刻的线索。

从一个嘈杂的量子门到[宇宙的终极命运](@keyword=fate_of_the_universe|lang=zh-CN|style=Feynman)——这就是思考“信息能多好地被保存下来”这一问题所蕴含的力量与美。