## 引言
我们宏观世界的法则似乎与支配其构成要素的量子规则有着根本的不同。我们看到咖啡冷却、鸡蛋被炒熟——这些都是[不可逆过程](@keyword=irreversible_processes|lang=zh-CN|style=Feynman)，系统在其中忘记了它的过去，并最终达到[热平衡](@keyword=thermal_balance|lang=zh-CN|style=Feynman)。然而，由Schrödinger方程支配的底层量子力学却是完全可逆的；一个量子系统从未真正忘记过去。不可逆的、抹去记忆的时间之箭，如何能从完美保留记忆的量子王国法则中涌现出来？这个深刻的悖论——一个孤立的纯[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)如何能表现出热化特征——代表了现代物理学基础中的一个重大知识空白。

本文将探讨解决这一难题的主要方案：本征态热化假说（[ETH](@keyword=eigenstate_thermalization_hypothesis|lang=zh-CN|style=Feynman)）。它如同一把万能钥匙，将微观的量子世界与宏观的热力学定律联系起来。在第一章 **原理与机制** 中，我们将剖析[ETH](@keyword=eigenstate_thermalization_hypothesis|lang=zh-CN|style=Feynman)的大胆主张——即单个[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)本身就可以是其自身的热综集——并理解允许系统表现出向平衡态弛豫的[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)机制。随后，在 **应用与跨学科联系** 一章中，我们将看到这一个思想如何为[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学提供统一的基础，解释[热化](@keyword=thermalization|lang=zh-CN|style=Feynman)的极限，并搭建起通往量子信息和神秘[黑洞物理学](@keyword=black_hole_physics|lang=zh-CN|style=Feynman)的惊人桥梁。

## 原理与机制

### 一个量子难题：[热化](@keyword=thermalization|lang=zh-CN|style=Feynman)悖论

想象一下你桌上的一杯热咖啡。它会逐渐冷却，向房间散发热量，直到其温度与周围环境相同。它达到了“[热平衡](@keyword=thermal_balance|lang=zh-CN|style=Feynman)”。这个过程似乎是不可逆的；如果房间突然变冷，而你的咖啡自己开始沸腾，你一定会大吃一惊！这种直觉是[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)（研究热与能量的科学）的基石，它支配着从发动机到恒星的一切。这是一个关于遗忘的故事。咖啡忘记了它最初的热状态，进入了一个仅由室温描述的普通“温”状态。

现在，让我们把目[光放大](@keyword=optical_amplification|lang=zh-CN|style=Feynman)，放大到极微观的层面。咖啡和空气由无数原子构成，它们都遵循量子力学的法则。根据Schrödinger方程，一个孤立量子系统的演化是完全可逆的。如果你能追踪每一个粒子并逆转其运动，系统将完美地回溯其历史。一个量子系统从未真正忘记它的过去。

这里存在一个深刻而美丽的悖论。不可逆的、抹去记忆的[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)世界，如何能从完美可逆的、保留记忆的量子力学法则中涌现？如果一个孤立的量子系统从一个特定的构型——一个“纯态”——开始，它必须永远保持在[纯态](@keyword=pure_states|lang=zh-CN|style=Feynman)。它怎么可能[热化](@keyword=thermalization|lang=zh-CN|style=Feynman)，并被一个简单的温度（对应于一个混乱、概率性的“混合态”）所描述呢？这是现代物理学中最深刻的问题之一。事实证明，其答案充满了精妙之处，它的名字叫做**本征态热化假说（Eigenstate Thermalization Hypothesis, ETH）**。

### 经典弯路与量子障碍

在探讨量子世界之前，让我们先看看经典的图景。经典[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学用**[遍历性假说](@keyword=ergodic_hypothesis|lang=zh-CN|style=Feynman)**解决了它的版本的问题。这个思想是，经过很长一段时间，一个[混沌系统](@keyword=chaotic_systems|lang=zh-CN|style=Feynman)（比如盒子里的气体分子）将访问与其总能量相符的每一个可能的构型（位置和动量）。一个属性的[时间平均](@keyword=time_averaging|lang=zh-CN|style=Feynman)——比如某个壁面上的压力——等同于在该能量下对所有可能状态的平均。系统通过其自身的混沌之舞，充当了自己的统计取样器。

将这个想法应用于量子力学很诱人，但我们几乎立刻就撞了南墙。具有确定能量的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)是**能量本征态**——Schrödinger方程的[定态](@keyword=stationary_state|lang=zh-CN|style=Feynman)。而“[定态](@keyword=stationary_state|lang=zh-CN|style=Feynman)”是关键词。如果你将一个系统制备在单个能量本征态，比如$|E_{\alpha}\rangle$，它会永远停留在那里。唯一改变的是一个[整体相位](@keyword=global_phase|lang=zh-CN|style=Feynman)因子$\exp(-iE_{\alpha}t)$，这在物理上是不可观测的。任何可观测量$\hat{O}$的[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman)是完全静态的：$\langle E_{\alpha}|\hat{O}|E_{\alpha}\rangle$不随时间改变。系统根本不会“探索”其他状态。它被冻结了。[@problem_id:2000781]

这似乎是遍历行为的对立面！一个“卡”在单一状态的系统怎么可能被认为是[热化](@keyword=thermalization|lang=zh-CN|style=Feynman)的？要解决这个问题，需要一个惊人而大胆的概念飞跃。

### 本征态热化假说：简而言之的一场革命

本征态热化假说从根本上颠覆了这个问题。它提出了一个真正激进的观点：一个混沌的量子系统不需要探索所有可及的状态才能看起来是[热化](@keyword=thermalization|lang=zh-CN|style=Feynman)的。相反，*每一个[能量本征态](@keyword=energy_eigenstates|lang=zh-CN|style=Feynman)，其自身就已经看起来是[热化](@keyword=thermalization|lang=zh-CN|style=Feynman)的*。

仔细体会一下这句话。[ETH](@keyword=eigenstate_thermalization_hypothesis|lang=zh-CN|style=Feynman)表明，如果你能将一个巨大的、孤立的、混沌的系统精确地制备到单个纯能量本征态$|E_{\alpha}\rangle$中，然后你去测量一个简单的**局域**性质（比如盒子一角中的温度，或少数几个原子的磁化强度），你得到的值将与系统处于一个温度对应于能量$E_{\alpha}$的热[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)中的情况相同。[@problem_id:2984530] 每个本征态都是一个量子全息图；一个单一的[纯态](@keyword=pure_states|lang=zh-CN|style=Feynman)，却编码了一个热综集的所有统计性质。

这个假说阐明了我们所说的混沌量子系统的含义。在这样的系统中，关于系统全局状态的信息被如此复杂地加扰并分布在整个[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)中，以至于任何局域探针只能接触到粗略的、平均的性质——也就是[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)性质。这并非适用于所有系统或所有可观测量。这是一个关于特定类型系统的假说：那些“非可积的”（除了能量之外没有特殊对称性和[守恒量](@keyword=conserved_quantity|lang=zh-CN|style=Feynman)）系统；以及针对特定类型的测量：那些“局域的”或“少体的”测量。[@problem_id:2984452]

### 一个算符的剖析：[ETH](@keyword=eigenstate_thermalization_hypothesis|lang=zh-CN|style=Feynman)的两大支柱

一个单一的纯[本征态](@keyword=eigenstates|lang=zh-CN|style=Feynman)如何能伪装成一团[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)上的混乱？魔法在于从[能量本征态](@keyword=energy_eigenstates|lang=zh-CN|style=Feynman)的角度来看物理可观量的结构。让我们将可观测量$\hat{O}$表示为一个矩阵，其[矩阵元](@keyword=matrix_elements|lang=zh-CN|style=Feynman)为 $O_{mn} = \langle E_m | \hat{O} | E_n \rangle$。ETH对这个矩阵提出了两个明确的主张。[@problem_id:3004216] [@problem_id:2984470]

1.  **对角元：热平均**。对角元$O_{nn} = \langle E_n | \hat{O} | E_n \rangle$正是我们讨论过的[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman)。[ETH](@keyword=eigenstate_thermalization_hypothesis|lang=zh-CN|style=Feynman)指出，这些值不是随机或不规则的。相反，它们构成了一个**关于能量的[光滑函数](@keyword=smooth_functions|lang=zh-CN|style=Feynman)**，$O_{nn} \approx f_{\hat{O}}(E_n)$。这个光滑函数$f_{\hat{O}}(E)$恰好是你在能量为$E$时使用[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的标准[微正则系综](@keyword=nve_ensemble|lang=zh-CN|style=Feynman)计算出的值。因此，你在一个窄能量范围内选择的任何本征态，对于可观测量$\hat{O}$，都会给出基本相同的热[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman)。

2.  **非对角元：被抑制的噪声**。那么非对角元 $O_{mn}$（其中 $m \neq n$）呢？这些元素支配着跃迁和动力学。[ETH](@keyword=eigenstate_thermalization_hypothesis|lang=zh-CN|style=Feynman)假定它们实际上是随机的，平均值为零，更重要的是，它们是**指数级小的**。它们的大小被一个与[热力学熵](@keyword=thermodynamic_entropy|lang=zh-CN|style=Feynman)$S(E)$相关的因子所抑制：
    $|O_{mn}| \sim \exp(-S(E)/2)$。
    
    为什么会有如此剧烈的抑制？这源于一个优美的自洽性论证。给定能量范围内的态数以$\exp(S(E))$的速度增长。如果非[对角矩阵](@keyword=diagonal_matrix|lang=zh-CN|style=Feynman)元不是极其微小，那些对它们求和的量（如热关联函数）在系统尺寸增大时就会发散，这在物理上是荒谬的。为了在大系统中保持物理行为的良好性，这些跃迁元素*必须*是极其微小的。[@problem_id:2984470]

因此，一个[混沌系统](@keyword=chaotic_systems|lang=zh-CN|style=Feynman)中局域可观量的矩阵具有一种非常特殊的结构：一个平滑、缓变的对角线，以及由近乎为零、随机的非对角噪声构成的海洋。

### 退相干的交响曲：平衡如何涌现

现在我们拥有了解决最初难题的所有碎片。让我们将系统制备在一个初始状态$|\psi(0)\rangle$中，它*不是*单个能量本征态，而是许多能量本征态的叠加，$|\psi(0)\rangle = \sum_n c_n |E_n\rangle$。我们的可观测量$\hat{O}$在时间$t$的[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman)为：
$$
\langle \hat{O} \rangle_t = \sum_{m,n} c_m^* c_n O_{mn} e^{i(E_m-E_n)t}
$$
我们可以将其分为两部分：
$$
\langle \hat{O} \rangle_t = \sum_n |c_n|^2 O_{nn} + \sum_{m \neq n} c_m^* c_n O_{mn} e^{i(E_m-E_n)t}
$$
第一项是**对角系综**的平均值。由于ETH告诉我们，在[相关能](@keyword=correlation_energy|lang=zh-CN|style=Feynman)量窗口内所有的$O_{nn}$都约等于[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)值$\langle \hat{O} \rangle_{\text{thermal}}$，所以这一整项就是热平均值。[@problem_id:2984516]

第二项包含了所有的非对角元。它是一个由巨量项组成的和，每一项都以不同的频率$(E_m - E_n)$[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。在一个[混沌系统](@keyword=chaotic_systems|lang=zh-CN|style=Feynman)中，这些能量差都是不同且无结构的。这就像一个音乐厅里坐满了数百万名音乐家，每个人都在演奏一个随机的音符。最初可能有一些相干性，但很快，它们的相位就会变得混乱，最终的结果是寂静。这种相位的快速抵消被称为**退相干**。由于非对角元$O_{mn}$本身就已经是指数级小了，这些涨落项的总和不仅小，而且是**双指数级小**。我们可以计算这些时间涨落的方差；它按$\exp(-S)$的比例缩减，对于任何宏观系统来说，这都是一个天文数字般的小数。[@problem_id:2111303]

所以，经过一段非常短的时间后，涨落的非对角部分就消失了，[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman)稳定到由对角元决定的恒定[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)值。系统热化了。它并没有忘记它的初始状态——信息仍然存在，隐藏在本征态之间极其复杂的相位关系中。但对于任何简单的局域测量来说，这些信息都完全无法获取。

### 混沌的边缘：[热化](@keyword=thermalization|lang=zh-CN|style=Feynman)失效之处

[ETH](@keyword=eigenstate_thermalization_hypothesis|lang=zh-CN|style=Feynman)是一个强有力的假说，但它并非普适定律。它的失效之处和它的成功之处同样具有启发性。

-   **对称性与可积性**：对称性导致[守恒量](@keyword=conserved_quantity|lang=zh-CN|style=Feynman)，守恒量又导致能谱的简并。如果在完全相同的能量下存在多个本征态，你可以构建它们的组合，从而对一个可观测量给出不同的[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman)，这直接违反了[ETH](@keyword=eigenstate_thermalization_hypothesis|lang=zh-CN|style=Feynman)的“一个能量，一个值”的原则。一个具有简并能级的简单[四能级系统](@keyword=four_level_system|lang=zh-CN|style=Feynman)可以明确地证明这一点：你可以在*相同能量*下构造出两个不同的本征态，它们对一个局域[可观测量](@keyword=observables|lang=zh-CN|style=Feynman)产生截然不同的值。[@problem_id:2008398] 这就是为什么高度对称或“可积”的系统（它们有许多[守恒量](@keyword=conserved_quantity|lang=zh-CN|style=Feynman)）不会以通常的方式[热化](@keyword=thermalization|lang=zh-CN|style=Feynman)。对称性的存在要求将[ETH](@keyword=eigenstate_thermalization_hypothesis|lang=zh-CN|style=Feynman)限制在各个对称性扇区内。[@problem_id:2984462]

-   **观测者的性质**：[ETH](@keyword=eigenstate_thermalization_hypothesis|lang=zh-CN|style=Feynman)只对局域的、“简单的”可观测量有效。如果你设计一个极其复杂、非局域的算符——一个能同时探测整个系统的算符，比如投影到某个特定[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)上的投影算符——你就能区分开一个复杂的[本征态](@keyword=eigenstates|lang=zh-CN|style=Feynman)与另一个。这样一个算符的[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman)会在不同本征态之间表现出高度的不规则性，并且不会遵守ETH。[@problem_id:2984452]

-   **[多体局域化](@keyword=many_body_localization|lang=zh-CN|style=Feynman)（MBL）**：也许最令人惊讶的是，存在一类[无序系统](@keyword=disordered_systems|lang=zh-CN|style=Feynman)，尽管存在强相互作用，[热化](@keyword=thermalization|lang=zh-CN|style=Feynman)却完全失败。在这些MBL系统中，粒子被复杂的能量景观所困住，阻碍了信息的加扰。这些系统强烈违反ETH，并能无限期地保留其初始状态的局域记忆。[@problem_id:3004216]

目前，勾勒这些边界，区分强ETH（每个[本征态](@keyword=eigenstates|lang=zh-CN|style=Feynman)都是[热化](@keyword=thermalization|lang=zh-CN|style=Feynman)的）和弱ETH（只有“几乎所有”[本征态](@keyword=eigenstates|lang=zh-CN|style=Feynman)是热化的）的努力正处于物理研究的最前沿，推动着我们对日常世界量子基础的理解。[@problem_id:2984482]