## 引言
在量子领域，描述一个由许多相互作用的粒子组成的系统，会带来一个被称为“维度灾难”的驚人挑战。描述哪怕是数量不多的粒子的状态所需的信息量都会呈指数级增长，很快就变得过于庞大而无法存储或处理。这一根本性障碍限制了我们理解和预测复杂[量子材料](@keyword=quantum_materials|lang=zh-CN|style=Feynman)行为的能力，从新型磁体到[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机所需的奇异物质。那么，我们如何才能打造一种实用的语言来描述这些错综复杂的量子织锦呢？

本文将深入探讨[投影纠缠对态](@keyword=projected_entangled_pair_states|lang=zh-CN|style=Feynman) (Projected Entangled Pair States, PEPS)，这是一种强大的理论和计算框架，专门为解决二维系统中的这一问题而设计。通过用一个由简单、局域的构件（称为[张量](@keyword=tensor|lang=zh-CN|style=Feynman)）组成的网络来构建全局[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，PEPS 提供了一种既有物理动机又具计算效率的描述方式。读者将踏上一段旅程，探索这一革命性方法背后的核心思想。第一章“原理与机制”将解析 PEPS 是如何构建的，为什么它们能自然地捕捉到纠缠的本质物理，以及它们需要做出哪些计算上的权衡。随后的“应用与跨学科联系”一章将展示 PEPS 在实践中的巨大威力，从模拟真实材料、发现新的[物相](@keyword=phases_of_matter|lang=zh-CN|style=Feynman)，到提供一种甚至超越量子世界的、[描述复杂性](@keyword=descriptive_complexity|lang=zh-CN|style=Feynman)的通用语言。


*图 1：PEPS 构造。每个[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)位置上的[张量](@keyword=tensor|lang=zh-CN|style=Feynman)（圆圈）有一个物理指标 $s$（指向上方的腿）和几个虚拟指标（平面内的腿），用于连接邻居。*

## 原理与机制

想象一下，你想描述一幅画。原则上，你可以逐一列出每个像素的确切颜色。对于一幅高分辨率图像来说，这将是一份天文数字般冗长且基本无用的清单。一个更好的方法是描述画中的物体——一个“红色的球”、“蓝色的天空”。你已经将海量信息压缩成了一组有意义的概念及其相互关系。

描述一个多粒子[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，比如磁体中的电子，也面临类似的挑战，但甚至更为艰巨。描述“像素”——即电子自旋每种可能构型的[复振幅](@keyword=complex_amplitude|lang=zh-CN|style=Feynman)——的数量随粒子数呈[指数增长](@keyword=exponential_growth|lang=zh-CN|style=Feynman)。即使只有少数几个原子，这个数字也超过了宇宙中的原子总数。这就是臭名昭著的“维度灾难”。我们如何才能[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)描述，更不用说理解这样一个庞然大物呢？这正是**[投影纠缠对态](@keyword=projected_entangled_pair_states|lang=zh-CN|style=Feynman) (PEPS)** 这一优美思想大显身手的地方。

### [量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)的“原子”

PEPS 方法认为：我们不要试图写下整个数字列表。相反，我们应该用小型的、局域的构件来构建[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，就像用砖块砌墙一样。这些构件是被称为**[张量](@keyword=tensor|lang=zh-CN|style=Feynman)**的数学对象。

你可以将[张量](@keyword=tensor|lang=zh-CN|style=Feynman)看作一个[多维数组](@keyword=multidimensional_arrays|lang=zh-CN|style=Feynman)。为了我们的目的，我们在粒子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的每个位置上放置一个[张量](@keyword=tensor|lang=zh-CN|style=Feynman)，就像该位置的一个量子“原子”。每个[张量](@keyword=tensor|lang=zh-CN|style=Feynman)有几条“臂”或称**指标**。其中一条臂是特殊的：它是**物理指标**。该指标对应于该位置的实际物理状态——对于一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，它可能取值为 0（表示“自旋向下”）或 1（表示“自旋向上”）。

其他的臂被称为**虚拟指标**。它们是整个构造的秘密所在。它们不代表可直接观测的属性；相反，它们充当将一个[张量](@keyword=tensor|lang=zh-CN|style=Feynman)与其邻居连接起来的“胶水”。每个虚拟指标可以取的不同值的数量被称为**键维**，用 $D$ 表示。这个数字至关重要：它决定了相邻位置之间可以共享多少纠缠或[量子关联](@keyword=quantum_correlations|lang=zh-CN|style=Feynman)。

想象一下用乐高積木搭建模型。每块积木就是一个[张量](@keyword=tensor|lang=zh-CN|style=Feynman)。积木的颜色是它的物理状态。积木上的凸点和凹孔是它的虚拟指标，使其能够连接到其他积木上。完整而复杂的乐高模型就是全局[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，由简单、相同的部件构建而成。