## 引言
在[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)这支错综复杂的舞蹈中，单个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)必须相互作用，才能执行那些有望解决棘手问题的复杂运算。但这种相互作用由什么主导？这些与经典世界隔离的量子实体之间如何进行交流？本文将深入探讨[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)耦合中最基本、最普遍的一种形式：ZZ 相互作用。它旨在解决物理学家和工程师共同面临的关键挑战：理解这种相互作用的双重性——它既是强大的计算工具，又是持续存在的误差来源。为了揭示其复杂性，我们将首先探索其底层的**原理与机制**，剖析 ZZ 相互作用是如何从奇特的量子力学定律中产生的。随后，本文将拓宽视野，审视其实际**应用与跨学科联系**，展示这一概念如何在物理学领域中被驾驭、被抗衡，并被视为一种普适的模式。通过探究其原理和应用，读者将对这一关键的量子力学效应获得深刻的理解。

## 原理与机制

我们已经铺设好了舞台。我们知道，[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，作为我们量子戏剧中的基本角色，必须能够相互作用。但它们是如何做到的呢？它们没有小手可以互相推搡。它们的相互作用远为微妙、奇特和优美。我们将深入探讨一种最基本的量子“握手”方式：**ZZ 相互作用**。理解它就像学习量子语言的语法；它是编写量子句子（门）和理解误差来源（噪声）的关键。

### 无形的握手：什么是 ZZ 相互作用？

想象有两个完全相同、完美隔离的钟摆，悬挂在一根巨大而刚性的钢梁上。如果你让其中一个开始摆动，另一个仍然浑然不觉。现在，我们用一根稍有弹性的木杆替换钢梁。如果你推动一个钟摆，它的运动会使木杆产生极其微小的摆动。这个摆动沿着木杆传播，并开始影响第二个钟摆。它们现在耦合了。它们能感觉到彼此。

ZZ 相互作用就是这种现象的量子等价物。它是一种由共享媒介介导的“超距作用”。在数学上，它由系统哈密顿量（或能量函数）中一个优美而简单的项来描述：

$$
H_{ZZ} = \hbar \zeta \sigma_z^{(1)}\sigma_z^{(2)}
$$

我们不要被这些符号吓到。$\sigma_z^{(1)}$ 和 $\sigma_z^{(2)}$ 是我们两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)——[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 1 和[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 2——的泡利算符。你可以把 $\sigma_z$ 算符看作一个问题：“这个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)是处于[基态](@keyword=basis_states|lang=zh-CN|style=Feynman) $|0\rangle$ 还是[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman) $|1\rangle$？”它为 $|0\rangle$ 态赋予值 $+1$，为 $|1\rangle$ 态赋予值 $-1$。所以，$\sigma_z^{(1)}\sigma_z^{(2)}$ 这一项只是检查两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的状态并将它们的值相乘。符号 $\zeta$ (zeta) 是 **ZZ [耦合强度](@keyword=coupling_strength|lang=zh-CN|style=Feynman)**，它告诉我们这种无形的握手有多强大。

这个项到底*做什么*？它不会将[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)从 $|0\rangle$ 翻转到 $|1\rangle$。相反，它会根据状态的组合来改变系统的*能量*。如果两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)处于相同的状态（都是 $|0\rangle$ 或都是 $|1\rangle$），该项会给能量增加 $+\hbar \zeta$。如果它们处于不同的状态（$|01\rangle$ 或 $|10\rangle$），它会减少 $-\hbar \zeta$。

这种能量移动带来了一个深远的结果：它使得一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的跃迁频率依赖于另一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的状态。将[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 1 从 $|0\rangle_1$ 激发到 $|1\rangle_1$ 所需的能量，在[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 2 处于 $|0\rangle_2$ 态和 $|1\rangle_2$ 态时是不同的。这种条件频率移动是许多双[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)门的绝对基石。它是一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)“知道”另一个在做什么的方式。正如在[量子比特串扰](@keyword=qubit_crosstalk|lang=zh-CN|style=Feynman)分析的背景下所做的优雅定义[@problem_id:70593]，这种移动可以通过比较[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)来精确测量：

$$
\hbar \zeta = (E_{11} - E_{01}) - (E_{10} - E_{00})
$$

这个表达式非常直观。它计算了当[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 2 被激发时[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 1 的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)（$E_{11} - E_{01}$），减去当[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 2 处于[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)时[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 1 的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)（$E_{10} - E_{00}$），其差值正是[相互作用能](@keyword=interaction_energy|lang=zh-CN|style=Feynman)。

### 量子信使：虚粒子

这种信息是如何从一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)传递到另一个的？量子世界中的“柔性杆”通常是一种共享资源——一个腔谐振器（一个“光盒”）、一条[传输线](@keyword=transmission_lines|lang=zh-CN|style=Feynman)，甚至是共享的环境缺陷浴。但量子魔力就在于：这个介体实际上不必像经典意义上那样被“使用”。

海森堡不确定性原理允许能量在瞬间被“借用”，只要它能被迅速归还。这使得**[虚粒子](@keyword=virtual_particles|lang=zh-CN|style=Feynman)**得以产生。一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)可以向腔中发射一个[虚光子](@keyword=virtual_photons|lang=zh-CN|style=Feynman)，然后被第二个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)吸收，而这个[光子](@keyword=photon|lang=zh-CN|style=Feynman)从未真正作为长寿命粒子“存在”过。这种通过暂时的、不可观测的中间状态进行的交换过程，是物理学家称之为**[微扰理论](@keyword=perturbation_theory|lang=zh-CN|style=Feynman)**的核心。

一个经典的例子出现在[电路量子电动力学](@keyword=circuit_qed|lang=zh-CN|style=Feynman)（cQED）中，其中两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)位于一个共享的[微波腔](@keyword=microwave_cavity|lang=zh-CN|style=Feynman)内[@problem_id:773294]。如果[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的频率与腔的频率相差很大（即**[色散区](@keyword=dispersive_regime|lang=zh-CN|style=Feynman)域**），它们无法[直接交换](@keyword=direct_exchange|lang=zh-CN|style=Feynman)一个实[光子](@keyword=photon|lang=zh-CN|style=Feynman)。取而代之的是，它们进行这种虚交换。这个过程是一个优美的因果链：
1. [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 1 的状态会轻微改变腔的有效[谐振频率](@keyword=resonant_frequency|lang=zh-CN|style=Feynman)。就好像光盒的“颜色”会根据[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 1 是开启还是关闭而改变。
2. 同样与这个腔对话的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 2，会看到这个轻微移动的频率。
3. 腔频率的这种变化改变了[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 2 的能级（这种效应被称为[兰姆位移](@keyword=lamb_shift|lang=zh-CN|style=Feynman)）。
4. 结果呢？[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 2 的能量现在依赖于[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 1 的状态。

这整个交换都是通过腔以虚拟方式发生的，导致了两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)之间产生有效的 ZZ 相互作用。其强度 $\zeta$ 取决于各个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)-腔的耦合强度（$g_1, g_2$）以及它们偏离共振的程度（$\Delta_1, \Delta_2$）。

### 各种各样的介体

具体的“信使”可能各不相同，但虚交换的原理却具有惊人的普适性。这一个观点解释了表面上看起来截然不同的多种现象。

- **嘈杂的环境：**如果介体不是一个纯净的腔，而是一个混乱无序的环境，比如芯片材料中由微小缺陷构成的浴（双能级系统或 TLS）呢？如果两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)足够近，都能感受到同一组缺陷，这个共享的浴就可以充当一个通信通道[@problem_id:102914]。一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)介导的 TLS 虚激发可以被另一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)感受到。由此产生的 ZZ 相互作用通常是不受欢迎的；它是一种**关联噪声**，即影响一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的随机涨落与另一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的涨落存在[统计关联](@keyword=statistical_association|lang=zh-CN|style=Feynman)。这显示了 ZZ 相互作用的双重性：当受控时是强大的资源，但当它源于不受控的环境时则成为破坏性的误差来源。

- **双[光子](@keyword=photon|lang=zh-CN|style=Feynman)信使：**在具有极高阻抗谐振器的系统中，耦合可能非常强，以至于主导的相互作用涉及*成对*虚光子的交换[@problem_id:651535]。[相互作用哈密顿量](@keyword=interaction_hamiltonian|lang=zh-CN|style=Feynman)看起来不同，涉及到算符 $(\hat{a} + \hat{a}^\dagger)^2$，但再次地，二阶微扰计算揭示了我们熟悉的 $\sigma_z^{(1)}\sigma_z^{(2)}$ 形式。大自然总有办法建立这种条件性能量移动，即使它不得不成对地派遣信使！

- **超强信使：**进入**超[强耦合区域](@keyword=strong_coupling_regime|lang=zh-CN|style=Feynman)**，其中[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)-腔的[耦合强度](@keyword=coupling_strength|lang=zh-CN|style=Feynman) $g$ 成为频率本身的重要组成部[分时](@keyword=time_sharing|lang=zh-CN|style=Feynman)，我们简单的近似就失效了。例如，我们再也不能忽略那些对应于同时产生一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)激发和一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)的项。然而，即使在这个狂野的区域，经过更仔细的分析，考虑了所有这些额外的过程之后，[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的[有效哈密顿量](@keyword=effective_hamiltonian|lang=zh-CN|style=Feynman)仍然包含一个 ZZ 相互作用项[@problem_id:785767]。值得注意的是，在这个特定情况下，这种相互作用的强度竟然与腔中已有的实[光子](@keyword=photon|lang=zh-CN|style=Feynman)数量无关，这是一个由各项巧妙抵消而产生的非凡结果。

### [量子工程](@keyword=quantum_engineering|lang=zh-CN|style=Feynman)的艺术：构建与规避相互作用

如果 ZZ 相互作用如此基本，我们能否按需构建它？同样重要的是，我们能否防止它出现在我们不希望的地方？这就是[量子工程](@keyword=quantum_engineering|lang=zh-CN|style=Feynman)的艺术。

**构建相互作用：**想象你需要在一对没有天然介体的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)之间产生 ZZ 耦合。解决方案是构建一个。利用**哈密顿量构件**，我们可以引入第三个[辅助量子比特](@keyword=ancilla_qubit|lang=zh-CN|style=Feynman)（“ancilla”），并精心设计它与前两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的耦合[@problem_id:43227]。通过对辅助比特的[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)施加一个巨大的能量惩罚，我们确保它只会被虚拟地占据。然后，通过设计一个特定的操作链——例如，一个特定的三步虚拟过程，其中[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 1 翻转辅助比特，辅助比特的状态触发一个能量移动，然后[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 2 将辅助比特翻转回来——我们可以在计算[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的低能空间中工程化出所需的相互作用。这是最高水平的量子架构，需要更高阶（本例中为三阶）的微扰路径来实现目标。

**规避相互作用：**在设计量子处理器时，我们通常将[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)以线性或网格状[排列](@keyword=permutation|lang=zh-CN|style=Feynman)，并设置近邻耦合。一个关键问题是：[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 1 和 2 之间的耦合是否会在[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 1 和 3 之间引入不希望的“串扰”相互作用？微扰计算给出了答案。对于一条线上的三个典型 transmon [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，次近邻之间的寄生 ZZ 相互作用，在[二阶近似](@keyword=second_order_approximation|lang=zh-CN|style=Feynman)下，恰好为零[@problem_id:70593]！这对于硬件设计师来说是一个极好的结果，因为它意味着这种误差最主要的来源被自然抑制了。在某些原子系统中也出现了类似的“零结果”，其中一种特定的耦合方案在最低微扰阶数下也不会导致 ZZ 相互作用 [@problem_id:1197594]。这给我们一个深刻的教训：这些相互作用的存在与否及其强度，对耦合的几何结构和路径极为敏感。

但我们必须小心。物理学中的“零”通常是一种近似。在二阶消失的效应可能会以一个更小的四阶项出现。在对两个耦合的 fluxonium [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的详细分析中，我们恰好看到了这一点[@problem_id:139450]。一次直到四阶的计算揭示，ZZ 耦合有一个主导的二阶项，但也有一个非零的四阶修正。在追求越来越高的保真度的过程中，物理学家必须追查这些微小的高阶效应，它们可能是一个[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)成功与失败之间的区别。

### 现实世界：不完美与不确定性

到目前为止，我们一直将我们的参数——频率、耦合强度——视为完美的、上帝赋予的数字。但在真实的量子处理器中，这些值受到制备过程中混乱现实的影响。每个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)都略有不同。频率可能会根据某种统计分布偏离其设计值。

这会产生实际后果。我们精心设计的 ZZ [耦合强度](@keyword=coupling_strength|lang=zh-CN|style=Feynman) $J_{ZZ}$ 依赖于这些频率。如果频率是[随机变量](@keyword=random_variable|lang=zh-CN|style=Feynman)，那么[耦合强度](@keyword=coupling_strength|lang=zh-CN|style=Feynman)也是。这是构建可扩展[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的一个关键挑战。我们可以使用统计学工具来理解这些基本的不确定性如何传播到我们工程化的相互作用中[@problem_id:70718]。通过对 ZZ 耦合公式应用一阶[不确定性分析](@keyword=uncertainty_analysis|lang=zh-CN|style=Feynman)，可以根据已知的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)频率制备方差，推导出 $J_{ZZ}$ *方差*的表达式。这将一个深刻的量子力学原理直接与[纳米加工](@keyword=nanofabrication|lang=zh-CN|style=Feynman)设施中[过程控制](@keyword=process_control|lang=zh-CN|style=Feynman)这一具体、现实的工程问题联系起来。

因此，ZZ 相互作用是一个具有优美统一性的概念。它是一种源于量子信使虚交换的能量移动。它是我们用来构建双[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)门的基本资源。它是我们必须通过系统工程来避免的寄生串扰。它是由混乱环境产生的关联噪声。它也是一个敏感的过程变量，我们必须控制其波动才能构建可靠的量子机器。简而言之，它就是量子力学在工作。