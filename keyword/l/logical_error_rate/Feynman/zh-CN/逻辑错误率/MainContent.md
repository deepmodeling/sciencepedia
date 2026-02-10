## 引言
[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的巨大挑战在于一个基本悖论：我们如何用本质上充满噪声且不可靠的部件来构建一台完全可靠的机器？[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的构件——[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) (qubit)——对其环境极为敏感，这使得它们容易出错，而这些错误可能会破坏任何有意义的计算。解决方法不是制造完美的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，而是通过一种称为[量子纠错](@keyword=quantum_error_correction|lang=zh-CN|style=Feynman)的过程，巧妙地管理其不完美之处。这项工作的核心成功指标是**[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)**——即一个经过编码的、稳健的逻辑量子比特最终失效的概率。本文旨在填补[物理量子比特](@keyword=physical_qubit|lang=zh-CN|style=Feynman)固有的脆弱性与[逻辑量子比特](@keyword=logical_qubits|lang=zh-CN|style=Feynman)所要求的稳定性之间的关键知识鸿沟。

在接下来的章节中，我们将揭示这一强大概念背后的原理。首先，在“原理与机制”一章中，我们将探讨[纠错](@keyword=error_correction|lang=zh-CN|style=Feynman)的[基本权](@keyword=fundamental_weights|lang=zh-CN|style=Feynman)衡，建立物理错误与逻辑错误之间的关系，阐明错误阈值的关键概念，以及使容错成为可能的标度定律。然后，在“应用与跨学科联系”一章中，我们将了解[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)在真实[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机中如何作为一个核心设计参数，并发现它在合成生物学和先进[癌症疗法](@keyword=cancer_therapy|lang=zh-CN|style=Feynman)等不同领域中的惊人关联性，揭示出支配复杂系统中可靠性的[普适逻辑](@keyword=universal_logic|lang=zh-CN|style=Feynman)。

## 原理与机制

那么，我们如何用不可靠的部件构建一台可靠的机器呢？这不是一个新问题。几个世纪以来，工程师们一直在努力解决这个问题。如果一颗螺丝失效的概率是百万分之一，而你的飞机上有一百万颗螺丝，你不会只是[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)手指祈祷好运。你会构建冗余。你设计的系统，要能保证一个甚至几个小故障不会导致灾难性后果。

量子纠错也是同样的想法，但其舞台要精妙和怪异得多。我们的“部件”是[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，而我们的“故障”不仅仅是简单的损坏，而是来自宇宙的微弱噪声——一个杂散[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)、一次热扰动、一束[宇宙射线](@keyword=cosmic_rays|lang=zh-CN|style=Feynman)——这些都可能破坏脆弱的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。单个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)在短时间内发生此类故障的概率就是**[物理错误率](@keyword=physical_error_rate|lang=zh-CN|style=Feynman)**，我们称之为 $p$。我们的目标是利用这种不可靠的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)来构建一个高度可靠的**逻辑量子比特**，其失效概率，即**[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)** $P_L$，要远小于 $p$。小多少呢？这正是整个问题的关键所在。

### 基本权衡：秩序与混沌之争

让我们从最简单的想法开始。如果我们只进行复制会怎样？我们不用一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)存储信息，而是用三个。我们可以规定，逻辑态 $|\overline{0}\rangle$ 用三个都处于 $|000\rangle$ 态的[物理量子比特](@keyword=physical_qubit|lang=zh-CN|style=Feynman)表示，逻辑态 $|\overline{1}\rangle$ 用 $|111\rangle$ 态表示。

现在，假设我们的敌人是“比特翻转”错误——一个 $X$ 操作——它以概率 $p$ 发生在任何单个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)上。一段时间后，我们回来检查这三个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)。如果发现它们处于 $|010\rangle$ 态，那么最有可能的原始状态是什么呢？嗯，$|000\rangle$ 态中发生单个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)翻转的概率，要远大于 $|111\rangle$ 态中发生两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)翻转的概率（概率大约是 $p$ 对 $p^2$，而 $p$ 很小）。因此，我们可以根据概率进行“多数表决”纠正：我们将那个与众不同的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)翻转回来，使其与另外两个一致。

这个简单的方案，即**3[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)[重复码](@keyword=repetition_code|lang=zh-CN|style=Feynman)**，可以修正任何单个比特翻转。但如果两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)翻转了呢？如果 $|000\rangle$ 变成了 $|011\rangle$，我们的多数表决会看到两个 1 和一个 0。它会得出结论：“啊，这肯定原本是 $|111\rangle$ 态，发生了一个错误”，于是它翻转第一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)。结果是 $|111\rangle$——我们最初的 $|\overline{0}\rangle$ 变成了一个 $|\overline{1}\rangle$。一个逻辑错误发生了！

所以，如果两个或三个物理量子比特发生翻转，我们这个简单的编码就失效了。这种情况发生的概率是多少？假设每个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)上的错误是独立的，那么两个特定的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)翻转（而一个没有翻转）的概率是 $p^2(1-p)$。由于有三种方式选择哪两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)翻转，所以发生两次翻转的总概率是 $3p^2(1-p)$。三个都翻转的概率是 $p^3$。因此，总的[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)是：

$$P_L = 3p^2(1-p) + p^3 = 3p^2 - 2p^3$$

这个简单的公式掌握着一切的关键。让我们仔细看看 [@problem_id:66326] [@problem_id:174959]。如果 $p$ 非常小，比如 $0.01$，那么 $P_L$ 大约是 $3p^2 = 0.0003$。这太棒了！我们的[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)远低于[物理错误率](@keyword=physical_error_rate|lang=zh-CN|style=Feynman)。我们用不太可靠的部件制造出了更可靠的东西。

但如果物理错误变得更普遍会怎么样呢？让我们画出 $P_L$ 对 $p$ 的图。我们会发现一个奇特的现象：两条[曲线相交](@keyword=intersection_of_curves|lang=zh-CN|style=Feynman)了。在某一点，[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)*恰好等于*[物理错误率](@keyword=physical_error_rate|lang=zh-CN|style=Feynman)。我们可以通过求解 $3p^2 - 2p^3 = p$ 来找到这个点。这给出了一个非平凡解 $p=\frac{1}{2}$。

这是一个深刻的结果。如果你的[物理错误率](@keyword=physical_error_rate|lang=zh-CN|style=Feynman)低于这个 $\frac{1}{2}$ 的**阈值**，那么[纠错](@keyword=error_correction|lang=zh-CN|style=Feynman)对你有帮助 ($P_L \lt p$)。但如果你的[物理错误率](@keyword=physical_error_rate|lang=zh-CN|style=Feynman)*高于*这个阈值，应用这种“纠错”程序实际上会让事情变得更糟 ($P_L \gt p$)！你还不如只用一个未编码的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)。这是一个基本的权衡：只有当你的底层硬件已经“足够好”时，[量子纠错](@keyword=quantum_error_correction|lang=zh-CN|style=Feynman)才是一个制胜策略。

### 递归的魔力：如何赢得战斗

所以，我们有了一种降低错误率的方法，只要 $p$ 低于某个阈值。对于一个小的 $p$，我们可以将其变成一个更小的 $P_L \approx 3p^2$。这很好，但对于需要执行数万亿次操作的计算机来说，这足够好吗？我们需要做得更好。如何做呢？

答案是计算机科学中最美的思想之一：**级联（concatenation）**。如果一个过程能将一个小的错误 $p$ 转化为一个更小的错误 $h(p) = 3p^2 - 2p^3$，那么如果我们将这个过程应用于它自身的输出，会发生什么呢？

让我们构建一个两级编码。我们从一个顶层的[逻辑量子比特](@keyword=logical_qubits|lang=zh-CN|style=Feynman)开始。我们用我们的 3 [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)码对其进行编码。但现在，这三个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)中的每一个都不是物理量子比特。每一个都是一个“第一级”[逻辑量子比特](@keyword=logical_qubits|lang=zh-CN|style=Feynman)。然后我们再次使用 3 [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)码对这些第一级逻辑量子比特中的每一个进行编码。这样我们总共得到了 $3 \times 3 = 9$ 个[物理量子比特](@keyword=physical_qubit|lang=zh-CN|style=Feynman)。

现在的[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)是多少？嗯，一个第一级模块的错误率是 $p_L^{(1)} = h(p)$。这些第一级模块对于顶层编码来说就是“物理”[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)。所以，我们两次级联后的编码的最终[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)就是 $p_L^{(2)} = h(p_L^{(1)}) = h(h(p))$ [@problem_id:1651100]。

让我们看看这带来了什么效果。如果 $p$ 低于我们的阈值 $\frac{1}{2}$，我们已经知道 $h(p) \lt p$。由于 $h(p)$ 只是另一个小于 $\frac{1}{2}$ 的数，再次应用这个函数会得到 $h(h(p)) \lt h(p)$。我们进一步抑制了错误！我们可以重复这个过程，创建 3 级、4 级、5 级的编码……每一次，错误率都会以惊人的速度下降。如果我们的[物理错误率](@keyword=physical_error_rate|lang=zh-CN|style=Feynman) $p$ 低于阈值，我们就有一个可靠的方法，可以将[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)降到我们想要的任何小的值。这就是**[阈值定理](@keyword=threshold_theorem|lang=zh-CN|style=Feynman)**的核心思想。

这种标度效应是戏剧性的。对于像 [[7,1,3]] Steane 码这样的简单距离为 3 的编码，单级编码的[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)标度为 $p_L^{(1)} \approx C p^2$，其中 $C$ 是某个常数。如果你将其级联一次，新的[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)将变为 $p_L^{(2)} \approx C(p_L^{(1)})^2 \approx C(Cp^2)^2 = C^3 p^4$ [@problem_id:62300]。如果你的[物理错误率](@keyword=physical_error_rate|lang=zh-CN|style=Feynman)是 $p = 10^{-3}$，单级编码能让你的[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)达到约 $10^{-6}$。但第二级编码能让它达到约 $10^{-12}$！每增加一级级联，错误抑制的指数就会翻倍。

### 构建真正的堡垒：[表面码](@keyword=surface_codes|lang=zh-CN|style=Feynman)

级联是一个优美的理论工具，但在实践中，人们对另一类编码更感兴趣：**[拓扑码](@keyword=topological_codes|lang=zh-CN|style=Feynman)**，特别是**[表面码](@keyword=surface_codes|lang=zh-CN|style=Feynman)**。

想象一下，你的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)[排列](@keyword=permutation|lang=zh-CN|style=Feynman)在一个二维网格上，就像一个棋盘。编码的规则不是关于“多数表决”，而是关于检查相邻[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)之间的局部关系。一个错误，比如一个翻转的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，会违反一些局部检查规则，产生一对我们可以探测到的“激发”。解码器的工作就是找出最有可能产生我们所观察到的激发的错误链，然后撤销它。

[表面码](@keyword=surface_codes|lang=zh-CN|style=Feynman)的能力由其**码距** $d$ 决定。对于一个方形区域， $d$ 就是其边长。当物理错误的模式形成一条从网格的一个边界一直延伸到相对边界的链时，就会发生逻辑错误。这种链的最短长度为 $d$。

对于每个错误以概率 $p$ 发生的简单错误模型，逻辑错误发生的最可能方式就是形成一条这种最小长度的错误链。这大约需要 $t = (d+1)/2$ 个错误以恰当的方式发生，才能混淆解码器。这种情况发生的概率标度为 $P_L \propto p^t = p^{(d+1)/2}$ [@problem_id:110078] [@problem_id:177896]。

这为我们指明了一条非常清晰的胜利之路：要获得更低的[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)，我们只需要构建一个具有更大码距 $d$ 的更大面积的[表面码](@keyword=surface_codes|lang=zh-CN|style=Feynman)。随着码距的增加，错误抑制效果呈指数级增强。

### 现实世界的反击

当然，宇宙从不那么简单。我们那些简洁的模型终究只是模型。一台真实的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机面临着一个远为复杂和恶劣的环境。

首先，并非所有错误都是生而平等的。一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)可能在门操作作用于其上时出错（门错误，$p_g$），也可能其状态在测量时被错误识别（测量错误，$p_m$）。一个实际的[表面码](@keyword=surface_codes|lang=zh-CN|style=Feynman)周期模型必须考虑所有这些情况。我们通常可以将这些错误归总为一个单一的**有效[物理错误率](@keyword=physical_error_rate|lang=zh-CN|style=Feynman)** $p_{eff}$，它是所有可能出错方式的[加权平均](@keyword=weighted_average|lang=zh-CN|style=Feynman)值 [@problem_id:175884]。这场战斗不仅仅是对抗一个数字 $p$，而是对抗它们的整个集合。

其次，我们假设错误在每个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)上是独立出现的。但如果不是呢？如果一个单一高能事件，比如一束[宇宙射线](@keyword=cosmic_rays|lang=zh-CN|style=Feynman)击中芯片，同时在两个*相邻*的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)上引起错误怎么办？这是一种**关联错误**。如果我们有一个码距 $d=3$ 的编码，它被设计用来处理单个错误。一个双错误事件几乎肯定会击败它。在这种情况下，[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)将不再像 $p^2$ 那样标度。相反，它将与这些关联事件的发生率 $p_{corr}$ 成正比 [@problem_id:175862]。强大的标度效应消失了！这告诉我们一些至关重要的事情：[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的物理设计必须旨在最小化错误，不仅是单个错误，更重要的是关联错误。

最后，我们关于[纠错](@keyword=error_correction|lang=zh-CN|style=Feynman)的图景——测量、思考、纠正——假设“思考”部分是瞬时完成的。但事实并非如此。分析错误伴随式的[经典计算](@keyword=classical_computation|lang=zh-CN|style=Feynman)机需要时间来运行其解码[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)。对于一个码距为 $d$ 的[表面码](@keyword=surface_codes|lang=zh-CN|style=Feynman)，一个好的解码器可能需要 $T_D$ 的时间，这个时间随码距呈[多项式增长](@keyword=polynomial_growth|lang=zh-CN|style=Feynman)，比如 $T_D \propto d^\beta$。在这段时间里，物理量子比特只是静静地待着，容易受到存储错误的影响。这意味着逻辑错误不仅可能因为初始状态噪声太大而发生，也可能因为状态本是*可纠正的*，但在我们忙于*思考*如何纠正它时，又发生了一个额外的错误。这在我们的[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)中引入了一个新的、隐蔽的项——一个实际上可能随着码距 $d$ 增长而增长的项 [@problem_id:175963]。这是对现实世界权衡取舍的一个迷人一瞥：使编码更强（增加 $d$）也使其解码更慢，这可能会带来新的漏洞。

### 更深层次的统一性：阈值、解码器与[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)

让我们回到宏观层面。我们已经看到，对于任何给定的编码和噪声环境，都存在一个临界[物理错误率](@keyword=physical_error_rate|lang=zh-CN|style=Feynman)，即**阈值** $p_{th}$，当[物理错误率](@keyword=physical_error_rate|lang=zh-CN|style=Feynman)低于此阈值时，我们可以通过增加编码的资源（如码距 $d$）来使[逻辑错误率](@keyword=logical_error_rate|lang=zh-CN|style=Feynman)任意小。高于此阈值，则希望尽失。

关键是，这个阈值不是一个单一的、普适的数字。它依赖于一切：编码族（[表面码](@keyword=surface_codes|lang=zh-CN|style=Feynman)等）、物理噪声模型（是独立的？关联的？还是有偏的？），以及最重要的是，我们**解码器**的巧妙程度 [@problem_id:3022097]。如果我们知道相位翻转（$Z$）错误比比特翻转（$X$）错误要常见得多，一个考虑到这一点的“偏置感知”解码器可以 achieving一个比对所有错误一视同仁的通用解码器高得多的阈值。优秀的工程设计和对噪声物理的深刻理解会带来巨大的回报。

现在来看最美妙的部分。[量子纠错](@keyword=quantum_error_correction|lang=zh-CN|style=Feynman)问题与物理学的一个完全不同的领域——研究磁体、液体和气体等系统的[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学——有着惊人的联系。

对于[表面码](@keyword=surface_codes|lang=zh-CN|style=Feynman)而言，寻找导致给定伴随式的最可能错误链的问题，在数学上等同于寻找一个被称为**随机键伊辛模型 (random-bond Ising model)** 的二维磁体能量最低的状态。量子问题中的[物理错误率](@keyword=physical_error_rate|lang=zh-CN|style=Feynman) $p$ 直接对应于磁体问题中的温度。

那么错误阈值呢？它是一个**[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)**。

对于[物理错误率](@keyword=physical_error_rate|lang=zh-CN|style=Feynman) $p \lt p_{th}$（低温），相应的磁体处于有序的铁磁相。错误就像指[向错](@keyword=disclinations|lang=zh-CN|style=Feynman)误方向的、小而孤立的[磁畴](@keyword=magnetic_domains|lang=zh-CN|style=Feynman)。它们是局域性的，容易发现并“翻转”回来。我们的纠错机制是有效的。

对于 $p \gt p_{th}$（高温），磁体处于无序的顺[磁相](@keyword=magnetic_phases|lang=zh-CN|style=Feynman)。[磁畴](@keyword=magnetic_domains|lang=zh-CN|style=Feynman)是遍布整个系统的混沌、[渗透](@keyword=permeation|lang=zh-CN|style=Feynman)的混乱状态。没有长程有序性。无法判断最初的整体磁化强度是多少。在量子世界中，这意味着物理错误已经压垮了编码，产生了无法解开的逻辑错误。

这不仅仅是一个类比，而是一个深刻的数学等价。在某种非常真实的意义上，构建[容错量子计算机](@keyword=fault_tolerant_quantum_computer|lang=zh-CN|style=Feynman)的追求，就是一场将计算系统冷却到一种深刻信息有序状态的探索，以对抗宇宙的热混沌。这是对自然法则惊人且意想不到的统一性的证明。