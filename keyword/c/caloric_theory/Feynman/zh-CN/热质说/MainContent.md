## 引言
认为热是一种物质实体——一种名为“热质”的、从高温物体流向低温物体的无形、无重量的流体——是一个直观而优雅的概念。几个世纪以来，它主导了科学思想，但它在根本上是错误的。本文探讨了从这个简单而有缺陷的模型到我们当前对热现象更细致入微的理解这一引人入胜的历程。它记录了用能量转移取代流动物质的智识转变，并在此过程中揭示了物理学的深刻原理。

在接下来的章节中，您将首先深入探讨“原理与机制”，这些内容瓦解了旧理论，确立了温度、能量和[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)的现代概念，甚至还会探索像[负热容](@keyword=negative_heat_capacity|lang=zh-CN|style=Feynman)这样的奇特现象。随后的“应用与跨学科联系”部分将展示热质概念令人惊讶的后续影响，揭示它在生物学、计算机科学和基础量子物理学等不同领域中的作用。

## 原理与机制

你可能认为自己知道什么是热。它让你的咖啡变热，让你杯中的冰块变冷。几个世纪以来，一个非常直观的图景占据了主导地位：科学家们将热想象成一种名为**热质**的、无形、无重量的流体。当你把一个热物体放在一个冷物体旁边时，这种热质流体就会从流体较多的一方流向较少的一方，直到两者的水平相当。这是一个简单、优雅的想法。但它错得深刻，错得漂亮。

从那个简单的图景到我们现代理解的这段历程，揭示了整个物理学中最深刻的一些原理。这是一个关于什么真正在流动、某物“热”意味着什么，以及在宇宙最奇特的角落里，增加能量如何反而能使物体变冷的故事。

### 第零定律的灵魂：温度不是热

让我们前往一个想象中的世界，拜访一个刚开始探索热现象的物理学文明。就像我们自己 18 世纪的科学家一样，他们识别出一种他们称之为“热荷”的、类似物质的广延量。他们知道，如果把两个物体放在一起，这种荷就会在它们之间流动。他们将没有净流动的状态称为“热静态”。

现在，他们用 A、B、C 三个物体进行一个经典实验 [@problem_id:1897083]。首先，他们将 A 和 C 接触，等待它们达到热静态。然后，他们将两者分开。接下来，他们将 B 和 C 接触，观察到它们也达到了热静态。一个简单的问题出现了：如果他们现在将 A 和 B 接触，会发生什么？

我们的直觉，以及他们的直觉，都会强烈地告诉我们什么都不会发生。它们将已经处于静态。这个看似微不足道的结论，实际上是所有[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)的基础。它被称为**[热力学第零定律](@keyword=transitive_property_in_thermodynamics|lang=zh-CN|style=Feynman)**。它陈述如下：如果 A 与 C 处于热平衡状态，B 与 C 也处于[热平衡](@keyword=thermal_balance|lang=zh-CN|style=Feynman)状态，那么 A 与 B 也处于[热平衡](@keyword=thermal_balance|lang=zh-CN|style=Feynman)状态。

为什么这如此重要？因为它意味着存在一种新的属性。达到相等的并不是“热质的量”。毕竟，一个巨大的冰山和一个小冰块都可以与一杯冰水处于热静态，但它们所含的“热质”量肯定不同。第零定律告诉我们，所有彼此处于[热平衡](@keyword=thermal_balance|lang=zh-CN|style=Feynman)的物体都共享一个共同的属性，一个状态函数，我们称之为**温度**。温度是我们为每个平衡类别所贴的标签。

这是与旧[热质说](@keyword=caloric_theory|lang=zh-CN|style=Feynman)的第一次重大分离。达到均衡的不是像体积或质量那样的广延量（热的“物质”），而是一个**强度**量。[温度测量](@keyword=thermometry|lang=zh-CN|style=Feynman)的不是一个物体拥有多少热能，而是它给出这些能量的*意愿*。它是能量的压强，而不是能量的总量。

### 伪装的能量：现代的“热质”

那么，如果热质不是一种流体，从热物体流向冷物体的是什么呢？答案是在 19 世纪由 James Prescott Joule 等人通过细致的实验发现的：是**能量**。热不是一种物质，而是因温差而转移能量的过程。旧的[热质说](@keyword=caloric_theory|lang=zh-CN|style=Feynman)并非完全无用，它为一个尚未被完全理解的概念提供了占位符。

旧理论的幽灵存活在我们的语言中。我们仍然谈论食物中的“卡路里”，科学家在某些情境下也仍在使用这个单位。但今天，它有了一个精确的定义。我们确切地知道一个“卡路里”代表多少能量：$1 \text{ calorie} = 4.184 \text{ Joules}$。这座桥梁让我们能够将热的宏观世界与原子和能量的微观世界联系起来。

例如，考虑像[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)这样的现代奇迹 [@problem_id:1902788]。在这种奇特的物质状态下，电子形成称为**[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)**的对。要打破一个[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)，使材料变回正常导体，需要一个微小而特定的能量，称为**[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)**，$2\Delta$。假设我们有一摩尔这种处于绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)的材料，我们想提供恰好足够的热量来打破所有的库珀对。我们可以根据量子基本原理、[阿伏伽德罗常数](@keyword=avogadro_s_constant|lang=zh-CN|style=Feynman)和[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta$ 计算出这个总能量。结果是一个以焦耳为单位的数字，这是能量的标准单位。但为了与[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)的历史语言联系起来，我们可以毫不费力地将这个量转换成卡路里。

这样做揭示了一种深刻的统一性。在高科技材料中触发量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)所需的能量，可以用两百年前用来测量燃烧一块煤所释放能量的完全相同的单位来表示。作为一种物质的“热质”*概念*已经消亡，但其作为**能量**的精确量度的现代体现，比以往任何时候都更加强大。

### 能量大劫案：热量去哪儿了？

当我们向一种物质添加能量时，它的温度通常会上升。但会上升多少呢？将等量的热量倒入一公斤水和一公斤铜中，水的温度变化要小得多。我们说水有更高的**[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)**。从旧[热质说](@keyword=caloric_theory|lang=zh-CN|style=Feynman)的角度来看，这令人费解。为什么一种物质比另一种物质更“渴求”热质呢？

[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学给了我们一个异常清晰的答案，这与分子自身的行为有关。让我们想象一个盒子里的简单气体 [@problem_id:2924172]。盒子壁上的压力来自于无数分子撞击它们。对于这种[动量传递](@keyword=momentum_transfer|lang=zh-CN|style=Feynman)，唯一重要的是分子从一个地方移动到另一个地方的速度——它们的**平动**。这种[平动动能](@keyword=translational_kinetic_energy|lang=zh-CN|style=Feynman)的平均值*就是*温度。这就是为什么从简单的单原子氩气到复杂的二氧化碳，各种不同的气体都遵循同一个简单的**[理想气体定律](@keyword=ideal_gas_law|lang=zh-CN|style=Feynman)**，$pV = N k_B T$，该定律关联了压力（$p$）、体积（$V$）和温度（$T$）。分子的内部结构与这种力学关系无关。

然而，关于能量——即“热质”——的故事则不同。当你加热时，你是在增加能量。这些能量去了哪里？一部分用于加速分子的[平动](@keyword=translational_motion|lang=zh-CN|style=Feynman)，这会提高温度。但如果分子比一个简单的球体更复杂，它就有其他地方可以隐藏能量。像氧气（$O_2$）这样的[双原子分子](@keyword=diatomic_molecules|lang=zh-CN|style=Feynman)可以像哑铃一样旋转。像水（$H_2O$）这样的[三原子分子](@keyword=triatomic_molecules|lang=zh-CN|style=Feynman)可以[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，其原子在[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)上来回摆动。这些旋转和[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)被称为**内自由度**。

当你加热多原子气体时，你不仅为更快的移动付费，还为更剧烈的旋转和摆动付费。能量被分流到这些内禀模式中，所以你必须添加更多的能量才能获得相同的温度（[平动](@keyword=translational_motion|lang=zh-CN|style=Feynman)）增量。这就是为什么作为**热学状态方程**（内能 $U$ 与温度 $T$ 之间的关系）一部分的[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)，对[分子结构](@keyword=molecular_structure|lang=zh-CN|style=Feynman)非常敏感，而力学[状态方程](@keyword=state_equations|lang=zh-CN|style=Feynman)（$pV=N k_B T$）则不然。热量，可以说，被分子私有的内部银行账户“偷走”了。

### 扭曲规则：[负热容](@keyword=negative_heat_capacity|lang=zh-CN|style=Feynman)的奇特案例

我们的直觉源于日常经验，告诉我们能量和温度之间的关系是一条单行道：增加能量，温度就会上升。绘制温度对能量的图应该得到一条总是上升的曲线。这条曲线被物理学家称为**[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)曲线** (caloric curve)。

对于大多数系统来说，这是对的。但是当发生[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)时，比如冰融化时，会发生什么？当你向一桶 $0^\circ\text{C}$ 的冰加热时，温度并不会上升。相反，能量被用来打破冰晶体的[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)，将其变成液态水。[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)曲线 $T(E)$ 在熔化温度处有一个完全平坦的平台。所有增加的能量都是**潜热**；它改变的是相，而不是温度。

这种行为在模拟以能量为控制参数的[孤立系统](@keyword=isolated_systems|lang=zh-CN|style=Feynman)时可以清楚地看到 [@problem_id:2453050]，这已经超出了我们简单的直觉。但在像原子核这样的有限、孤立系统的世界里，自然还准备了一个更大的惊喜。

想象一下，在粒子加速器中将两个重[离子对](@keyword=ion_pair|lang=zh-CN|style=Feynman)撞。在极短的瞬间，你创造出一个高度“激发”的原子核——一滴微小、炽热、孤立的[核物质](@keyword=nuclear_matter|lang=zh-CN|style=Feynman)。研究接下来会发生什么的物理学家发现了[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)中最奇特的现象之一。通过测量飞出的碎片的能量，并重建原子核在分裂前的温度，他们绘制出了原子核的[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)曲线。而这些曲线可以*向后弯曲* [@problem_id:376887]。

这种“后弯”对应一个**[负热容](@keyword=negative_heat_capacity|lang=zh-CN|style=Feynman)**区域。想想这意味着什么：在这个特定的能量范围内，如果你向原子核增加更多能量，它的温度*会下降*。这怎么可能呢？这就像往火里扔一根木头，火焰却变暗了。

关键在于该系统是微小的、孤立的，并且正在经历[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)——就像一滴液体沸腾成气体。当你增加能量时，你会达到一个[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，系统可以通过分裂获得大量熵。这个“蒸发”过程需要大量能量从定义温度的粒子动能转换成解绑原子核所需的势能。这个过程中消耗了如此多的动能，以至于[平均动能](@keyword=average_kinetic_energy|lang=zh-CN|style=Feynman)——也就是温度——瞬间下降。系统变得更冷，正是因为它在用增加的能量来撕裂自己。

这一惊人的发现，是通过追踪能量和温度之间的关系才得以实现的，它是对旧热质思想的终极实现和颠覆。“物质”是能量，而它与温度——这个为解释它而被发明的属性——之间的关系，远比 18 世纪的任何人所能想象的更为精妙、复杂和奇妙。