## 引言
在大脑错综复杂的网络中，单个[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)是一个精密的决策者，不断地解读来自成千上万个同伴的大量信号。神经科学的根本挑战在于理解这些独立的细胞如何倾听、处理并回应这复杂的信息合唱。本文将深入探讨这场神经对话的核心：[突触后电位](@keyword=postsynaptic_potentials|lang=zh-CN|style=Feynman)（PSP）。我们将探索神经系统的语言，解码突触处短暂的电学变化如何决定从简单反射到意识思维的一切。

旅程始于第一章**原理与机制**，我们将在此剖析PSP的生物物理基础。我们将揭示[神经递质](@keyword=neurotransmitter|lang=zh-CN|style=Feynman)如何以离散的包被形式释放，是什么决定了一个信号是兴奋性还是抑制性，以及[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)用于整合这些信息的优雅的[时间总和](@keyword=temporal_summation|lang=zh-CN|style=Feynman)与[空间总和](@keyword=spatial_summation|lang=zh-CN|style=Feynman)[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)。随后，**应用与跨学科联系**一章将把这个细胞世界与其宏观后果联系起来。我们将看到这些基本原理如何应用于[神经计算](@keyword=neural_computation|lang=zh-CN|style=Feynman)，它们如何被调控以改变大脑状态，以及它们的失调如何导致毁灭性的[神经系统疾病](@keyword=nervous_system_diseases|lang=zh-CN|style=Feynman)。通过理解一个[突触后电位](@keyword=postsynaptic_potentials|lang=zh-CN|style=Feynman)从在突触诞生到对[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)发放的最终影响的生命历程，我们得以深刻洞察大脑的计算能力。

## 原理与机制

想象一个[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)是一个微观的、高度精密的倾听者。它坐落在大脑广阔、噼啪作响的网络中，不断接收来自成千上万个其他[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)的信息。但这些信息不是文字，而是微小的电脉冲。这个[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)的艰巨任务是倾听这电信号低语和呐喊的嘈杂合奏，然后在几分之一秒内决定这条信息是否重要到足以传递下去。这个倾听、整合和决策的过程受一套既优雅又强大的物理原理支配。在本章中，我们将进入[突触后电位](@keyword=postsynaptic_potentials|lang=zh-CN|style=Feynman)的世界，这是这场神经对话的基本货币。

在我们深入之前，让我们先明确我们在谈论什么。神经系统在许多方面都使用电信号。当你触摸一个热炉子时，特化的感觉细胞将热量转化为一种称为**发生器电位**的电信号。这个信号是对物理刺激的直接转译。我们在此关心的是下一步：[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)之间在一个称为突触的连接点进行的通讯。跨越这些[突触传递](@keyword=synaptic_transmission|lang=zh-CN|style=Feynman)的信号就是**[突触后电位](@keyword=postsynaptic_potentials|lang=zh-CN|style=Feynman)**（PSP），这正是[神经回路](@keyword=neural_circuits|lang=zh-CN|style=Feynman)的语言[@problem_id:2337903]。

### 突触的低语：量子包

人们可能会天真地想象，一个传递信息的[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)会持续地向接收信息的[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)“喷洒”化学信使（[神经递质](@keyword=neurotransmitter|lang=zh-CN|style=Feynman)）。但大自然以其智慧，选择了一种更优雅、更稳健的方法。[Bernard Katz](@keyword=bernard_katz|lang=zh-CN|style=Feynman)等人在[神经肌肉接点](@keyword=neuromuscular_junction|lang=zh-CN|style=Feynman)——神经与肌肉之间的特化突触——的研究揭示了一个惊人的事实。即使在突触前神经完全静息时，他们也能在突触后肌细胞中检测到微小的、自发的电学波动。这些他们称为**[微终板电位](@keyword=mepps|lang=zh-CN|style=Feynman)（MEPPs）**的波动，其大小并非随机。它们的大小非常一致，仿佛是由一个基本的、不可分割的单位构成的[@problem_id:1722607]。

这一发现是革命性的。它意味着[神经递质](@keyword=neurotransmitter|lang=zh-CN|style=Feynman)不是像从软管中连续喷出的水流一样释放，而是被包装成离散的束，或称**量子**。每个量子都容纳在一个称为[突触囊泡](@keyword=synaptic_vesicles|lang=zh-CN|style=Feynman)的微小泡状结构中。自发的MEPPs是单个囊泡随机与突触前膜融合并释放其内容物的结果。

对单个[神经递质](@keyword=neurotransmitter|lang=zh-CN|style=Feynman)量子的电学响应称为**[量子大小](@keyword=quantal_size|lang=zh-CN|style=Feynman)（$q$）**。它代表了一个突触能产生的最小“低语”。当突触前[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)发放动作电位时，它不只释放一个量子，而是触发一整批量子的释放。由此产生的总[突触后电位](@keyword=postsynaptic_potentials|lang=zh-CN|style=Feynman)，在很大程度上是这个基本[量子大小](@keyword=quantal_size|lang=zh-CN|style=Feynman)的整数倍。这个“[量子假说](@keyword=quantal_hypothesis|lang=zh-CN|style=Feynman)”揭示了大脑的通讯系统在其最基本层面上是数字化的——由离散的信息包构成。

### 对话的性质：兴奋与抑制

所以，突触前[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)以包的形式发送信息。但这些信息说了什么？广义上讲，它们表达了两种意思之一：“行动！”或“停止！”。这分别对应**[兴奋性突触后电位](@keyword=excitatory_postsynaptic_potentials|lang=zh-CN|style=Feynman)（EPSP）**，它推动[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)更接近发放自身信号，和**[抑制性突触后电位](@keyword=inhibitory_postsynaptic_potentials|lang=zh-CN|style=Feynman)（IPSP）**，它阻止[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)发放信号。

EPSP是一个小的去极化，使[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)内部稍微变得更正。IPSP通常是一个[超极化](@keyword=hyperpolarization|lang=zh-CN|style=Feynman)，使其变得更负。是什么决定了一条信息是“行动”还是“停止”呢？人们可能以为是[神经递质](@keyword=neurotransmitter|lang=zh-CN|style=Feynman)分子本身，但并非如此。像乙酰胆碱这样的分子在一个地方可以是兴奋性的（如在肌肉中，使其收缩），而在另一个地方是抑制性的（如在心脏中，使其减速）。

信息意义的真正裁决者是突触后膜上的**受体**。当[神经递质](@keyword=neurotransmitter|lang=zh-CN|style=Feynman)结合时，受体打开一个通道，这是一个允许特定离子穿过膜的微小孔道。离子流动的方向不仅取决于其浓度梯度，还取决于跨[膜电位](@keyword=membrane_potential|lang=zh-CN|style=Feynman)。对于每种[离子通道](@keyword=ion_channel|lang=zh-CN|style=Feynman)，都存在一个特定的[膜电位](@keyword=membrane_potential|lang=zh-CN|style=Feynman)，在该电位下，电场力与[浓度梯度](@keyword=concentration_gradient|lang=zh-CN|style=Feynman)的力完美平衡。在这个电压下，即使通道完全打开，也没有离子的净流动。这就是**翻转电位（$E_{rev}$）**。

当一个通道打开时，就像在两个不同高度的水池之间打开了一扇门。[膜电位](@keyword=membrane_potential|lang=zh-CN|style=Feynman)总是会被拉向开放通道的翻转电位。
*   如果一个通道的$E_{rev}$比[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)的[静息电位](@keyword=resting_potential|lang=zh-CN|style=Feynman)更正（例如，对于同时通透$\text{Na}^+$和$\text{K}^+$的通道，约为$0$ mV），打开它将导致正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)内流和去极化。这是一个**EPSP**。
*   如果一个通道的$E_{rev}$比静息电位更负（例如，对于许多$\text{K}^+$通道，约为$-80$ mV），打开它将导致正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)外流（或负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)[内流](@keyword=internal_flow|lang=zh-CN|style=Feynman)）和[超极化](@keyword=hyperpolarization|lang=zh-CN|style=Feynman)。这是一个**IPSP**。

这个原理解释了为什么有些突触坚定地只起单向作用。在[神经肌肉接点](@keyword=neuromuscular_junction|lang=zh-CN|style=Feynman)，[乙酰胆碱受体](@keyword=acetylcholine_receptor|lang=zh-CN|style=Feynman)是一种对$\text{Na}^+$和$\text{K}^+$都通透的非选择性阳[离子通道](@keyword=ion_channel|lang=zh-CN|style=Feynman)。其翻转电位约为$0$ mV，远高于肌细胞约$-90$ mV的[静息电位](@keyword=resting_potential|lang=zh-CN|style=Feynman)。因此，打开这些通道*总是*导致强烈的[去极化](@keyword=depolarization|lang=zh-CN|style=Feynman)——一个确保[肌肉收缩](@keyword=muscle_contraction|lang=zh-CN|style=Feynman)的可靠的“行动！”信号[@problem_id:2335467]。然而，在大脑中，具有不同翻转电位的丰富多样的受体，使得“行动”和“停止”信号的细致对话成为可能。

### [神经元](@keyword=neurons|lang=zh-CN|style=Feynman)[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)：总和的艺术

单个EPSP通常只是一个微弱的低语，远不足以说服[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)发放动作电位。为了达到发放**阈值**（通常是从$-70$ mV的[静息电位](@keyword=resting_potential|lang=zh-CN|style=Feynman)到约$-55$ mV），[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)必须将其接收到的无数信号进行加总或整合。这种[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)主要有两种形式。

**[时间总和](@keyword=temporal_summation|lang=zh-CN|style=Feynman)**是在*时间*上的总和。想象一下敲鼓。如果你敲得慢，每一击的声音在下一次敲击前都已完全消失。但如果你快速连续地敲击，声音会相互叠加，形成响亮的滚奏。[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)的膜行为类似。一个EPSP不会瞬间消失；它会以由**[膜时间常数](@keyword=membrane_time_constant|lang=zh-CN|style=Feynman)（$\tau_m$）**决定的特征时间衰减。这个常数代表了膜的“渗漏”程度。如果第二个EPSP在第一个消失前从同一个突触到达，它们的效果会相加，使[膜电位](@keyword=membrane_potential|lang=zh-CN|style=Feynman)更接近阈值[@problem_id:2317767]。因此，[时间常数](@keyword=time_constant|lang=zh-CN|style=Feynman)$\tau_m$定义了时间整合的关键“机会窗口”。在这个窗口内到达的两个信号可以有效地相互叠加；如果它们相隔时间太长，第一个信号会衰减太多，以至于它们的总和不足以产生显著效果[@problem_id:2353046]。

**[空间总和](@keyword=spatial_summation|lang=zh-CN|style=Feynman)**是在*空间*上的总和。一个[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)不只监听一个输入；它有一个巨大的[树突](@keyword=dendrites|lang=zh-CN|style=Feynman)树，从成千上万个突触收集信号。[空间总和](@keyword=spatial_summation|lang=zh-CN|style=Feynman)是将在树上不同位置大致同时到达的信号相加的过程。这是一个简单的代数过程：去极化的EPSP使电位增加，而超极化的IPSP使其减少[@problem_id:1709874]。如果所有EPSP和IPSP的总和足以使轴丘（[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)的决策点）去极化至其阈值，就会发放一个动作电位。一个[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)可能在一个树突上接收到$+18$ mV的EPSP，在另一个[树突](@keyword=dendrites|lang=zh-CN|style=Feynman)上接收到另一个$+18$ mV的EPSP。单独任何一个都不足以跨越从[静息电位](@keyword=resting_potential|lang=zh-CN|style=Feynman)（$-70$ mV）到阈值（$-55$ mV）的$15$ mV差距，但它们的综合效应，即使在衰减一些后，也可能成功[@problem_id:2320906]。

### 超越简单加总：位置、几何结构与分路的否决权

简单代数加总的想法是一个美好的初步近似，但现实要有趣得多。并非所有突触的“投票”都被同等计票。[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)的几何结构起着至关重要的作用。

[树突](@keyword=dendrites|lang=zh-CN|style=Feynman)不是完美的电线；它们是会漏电的电缆。当一个[突触后电位](@keyword=postsynaptic_potentials|lang=zh-CN|style=Feynman)从树突上的一个遥远突触向轴丘传播时，其振幅会逐渐衰减。这类似于水压沿着漏水的花园软管下降的方式。[信号衰减](@keyword=signal_attenuation|lang=zh-CN|style=Feynman)的特征距离由**[膜长度常数](@keyword=membrane_length_constant|lang=zh-CN|style=Feynman)（$\lambda$）**描述。这个常数取决于膜电阻（阻止泄漏的能力）与内部细胞质电阻（沿其长度传导电流的能力）的比率[@problem_id:2718307]。

这带来了一个深远的影响：位置决定一切。在远离胞体的远端[树突](@keyword=dendrites|lang=zh-CN|style=Feynman)上产生的EPSP，到达轴丘时将仅是其初始强度的影子。相比之下，直接位于胞体上的突触具有强大的、有特权的声音，因为其信号几乎没有衰减[@problem_id:2337906]。这就是为什么抑制性突触常常策略性地放置在胞体上或其附近。胞体上一个位置恰当的IPSP可以有效地否决掉数十个较弱的、远端EPSP的总和合唱。

这引出了[神经生理学](@keyword=neurophysiology|lang=zh-CN|style=Feynman)中最微妙且强大的概念之一：**分路抑制**。我们倾向于认为抑制是主动地将[膜电位](@keyword=membrane_potential|lang=zh-CN|style=Feynman)拉低，远离阈值。但还有另一种说“停止”的方式。想象一下你正试图给一个有大洞的轮胎充气。无论你打入多少空气（兴奋性电流），压力（[膜电位](@keyword=membrane_potential|lang=zh-CN|style=Feynman)）都无法建立起来。

这就是分路抑制。它发生在当一个抑制性突触打开的通道，其翻转电位非常接近[静息膜电位](@keyword=resting_membrane_potential|lang=zh-CN|style=Feynman)时。在某些情况下，例如当氯离子平衡电位略*高于*[静息电位](@keyword=resting_potential|lang=zh-CN|style=Feynman)时，激活这些通道甚至可能导致一个小的*去极化*。然而，这却是深度抑制性的。为什么？因为打开这些通道会极大地增加膜的[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)，有效地在膜上打了个“洞”。这种增加的[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)会分流或短路任何同时到达的兴奋性电流。EPSP被急剧衰减，使其永远无法到达轴丘并触发一个峰电位[@problem_id:2715410]。这是一种优雅而高效的否决机制，它不需要强烈的超极化，而只是动态地改变细胞的整合特性。

### 可塑的突触：通过调节音量来学习

也许整个系统最奇妙的方面是它不是静态的。这场对话的规则可以改变。大脑通过修改其突触连接的强度来学习和记忆，这个过程被称为**[突触可塑性](@keyword=synaptic_plasticity|lang=zh-CN|style=Feynman)**。我们对[突触后电位](@keyword=postsynaptic_potentials|lang=zh-CN|style=Feynman)的理解为解开这个谜团提供了钥匙。

一个突触如何变得“更强”？一种方法是增加其**[量子大小](@keyword=quantal_size|lang=zh-CN|style=Feynman)（$q$）**。突触后[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)可以响应特定的活动模式，在突触膜中插入更多的受体通道。有了更多的可用受体，对单个量子（单个囊泡）[神经递质](@keyword=neurotransmitter|lang=zh-CN|style=Feynman)的响应就会变大。“低语”变成了“说话”。这是**[长时程增强](@keyword=long_term_potentiation|lang=zh-CN|style=Feynman)（LTP）**背后的一个主要机制，LTP是学习和记忆的细胞关联物。经历过这种LTP的突触，对于相同的突触前刺激会产生更大的EPSP，因为其响应的[基本单位](@keyword=fundamental_units|lang=zh-CN|style=Feynman)被放大了[@problem_id:2349671]。

此外，[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)可以改变自身的整合特性。通过调节其膜上“漏”通道的数量，[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)可以改变其膜电阻（$R_m$）。正如我们所见，这直接影响[长度常数](@keyword=space_constant|lang=zh-CN|style=Feynman)（$\lambda = \sqrt{a R_m / 2 R_i}$）。增加膜电阻使[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)“渗漏”减少，从而增加[长度常数](@keyword=space_constant|lang=zh-CN|style=Feynman)。这使得即使来自遥远树突的信号也能以更高的保真度传播到胞体，有效地让那些远端突触在决策过程中拥有了更大的发言权[@problem_id:2718307]。

从离散的[神经递质](@keyword=neurotransmitter|lang=zh-CN|style=Feynman)包到优雅的总和代数，从距离的暴政到分路否决的微妙力量，支配[突触后电位](@keyword=postsynaptic_potentials|lang=zh-CN|style=Feynman)的原理描绘了一幅[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)作为一种极其复杂的计算装置的图景。它不仅能实时执行复杂的计算，还能根据经验不断地重新布线，改变自己游戏规则。正是在这些动态的、短暂的电位中，思想、记忆和意识的基础得以建立。