## 引言
在[量子物质](@keyword=quantum_matter|lang=zh-CN|style=Feynman)的奇异世界中，一些材料表现出一种被称为[拓扑序](@keyword=topological_order|lang=zh-CN|style=Feynman)的隐藏且稳健的属性，其中信息被全局编码，而非存储于任何局部。这种奇异的序与系统的长程量子纠缠密切相关，但测量其普适指纹一直是一大挑战。拓扑序的微弱普适信号通常被与系统局域细节相关的、大得多的非普适贡献所淹没。我们如何才能分离出这一本质特征呢？本文深入探讨了解决方案：Kitaev-Preskill 公式，这是一个为测量[拓扑纠缠熵](@keyword=topological_entanglement_entropy|lang=zh-CN|style=Feynman)而设计的强大工具。在接下来的章节中，我们将首先探索该公式背后的基本**原理与机制**，从纠缠的[面积定律](@keyword=area_law|lang=zh-CN|style=Feynman)到分离出普适值的几何技巧。随后，我们将考察其广泛的**应用与跨学科联系**，展示物理学家如何将其用作一种石蕊试纸，以识别从简单模型到现代研究的混沌前沿等各种系统中的[拓扑相](@keyword=topological_phases|lang=zh-CN|style=Feynman)。

## 原理与机制

想象你有一张织工精美的挂毯。从远处看，你看到的是宏大而连贯的图案。但如果你仔细观察任何一根纱线，你不可能知道整个图案是什么。信息并非储存在某个单一位置；它被编码在所有纱线错综复杂的全局交织方式中。这就是**拓扑序**的本质——一种微妙而稳健的序，远超晶体或磁体等传统材料。但我们如何把握这种“交织性”呢？我们如何测量它？答案就在于量子纠缠那奇异而美丽的世界。

### [面积定律](@keyword=area_law|lang=zh-CN|style=Feynman)与一个令人困惑的修正项

在我们遇到的大多数材料中，即便是[量子材料](@keyword=quantum_materials|lang=zh-CN|style=Feynman)，纠缠也只是局域性的。如果我们想象画一条线将材料分成 A 和 B 两个区域，它们之间的纠缠实际上只是边界上原子之间的对话。深处 A 区域的原子对 B 区域一无所知。由于这种“纠缠作用”局限于边界，纠缠的总量——我们用一个称为**von Neumann [纠缠熵](@keyword=entanglement_entropy|lang=zh-CN|style=Feynman)** $S(A)$ 的数值来量化——应与该边界的大小成正比。对于二维材料，边界是一条长度为 $L$ 的线，因此我们[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)熵遵循“[面积定律](@keyword=area_law|lang=zh-CN|style=Feynman)”（这是一个源于三维的用词不当，这里实为边界定律）：

$S(A) \approx \alpha L$

系数 $\alpha$ 是一个非普适的数值，取决于材料所有杂乱的微观细节——原子的精确间距、它们的[相互作用强度](@keyword=interaction_strength|lang=zh-CN|style=Feynman)等等。这就像我们那张挂毯中纱线的具体颜色和粗细。

在很长一段时间里，这被认为是任何“有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)”系统所应有的行为。“有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)”系统指的是创建一个激发需要消耗能量，从而使其在低温下稳定而平静的系统。但随后，物理学家发现在某些有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的状态下，会发生一些非同寻常的事情。[纠缠熵](@keyword=entanglement_entropy|lang=zh-CN|style=Feynman)遵循以下规则：

$S(A) = \alpha L - \gamma$

这里出现了一个恒定的负修正项 $\gamma$。这不仅仅是任意一个数字。$\gamma$ 是一个**普适**常数。它不关心微观的细节；对于处于同一拓扑相的所有材料，它的值都是相同的。一个非零的 $\gamma$ 就是确凿的证据，一个明确的指纹，告诉我们偶然发现了一个具有长程纠缠的状态——一个[拓扑序](@keyword=topological_order|lang=zh-CN|style=Feynman)相。这个常数是我们的关键：**[拓扑纠缠熵](@keyword=topological_entanglement_entropy|lang=zh-CN|style=Feynman) (TEE)**。

### 一种几何上的巧计：分离不可见之物

现在我们面临一个巨大的挑战。这个普适的宝藏 $\gamma$ 被埋藏在巨大的、非普适的边界项 $\alpha L$ 之下。测量 $\gamma$ 就像试图称量一根羽毛的重量，方法是把它放在一辆巨大的卡车上，然后称量整体的重量。卡车重量的波动会完全淹没羽毛的重量。我们到底如何才能分离出它呢？

这正是物理学家 Alexei Kitaev 和 John Preskill 的天才之处。他们设计了一个绝妙的几何方案。想象将你的二维平面划分为三个相邻的大区域：A、B 和 C，像[饼图](@keyword=circle_graph|lang=zh-CN|style=Feynman)的扇区一样[排列](@keyword=permutation|lang=zh-CN|style=Feynman)。诀窍不仅在于测量每一块的[纠缠熵](@keyword=entanglement_entropy|lang=zh-CN|style=Feynman)，还在于测量它们各种组合的纠缠熵。我们测量 $S(A)$, $S(B)$, $S(C)$，然后是它们的并集 $S(A \cup B)$, $S(B \cup C)$, $S(C \cup A)$ 的熵，最后是整个区域 $S(A \cup B \cup C)$ 的熵。

然后，我们以一种非常特殊的方式，即一个容斥组合，将这些值结合起来：

$S_{\text{topo}} = S(A) + S(B) + S(C) - S(A \cup B) - S(B \cup C) - S(C \cup A) + S(A \cup B \cup C)$

当我们将我们的熵公式 $S(X) = \alpha |\partial X| - \gamma$ 代入这个组合时，一个奇迹般的抵消发生了。考虑任何一段边界，比如 A 区域与外部世界之间的边界。它对 $S(A)$ 有正贡献，对 $S(A \cup B)$ 和 $S(C \cup A)$ 有负贡献，对 $S(A \cup B \cup C)$ 又有正贡献。将这些加起来，它的总贡献为零！这种情况对*每一段*边界都成立。整个非普适的 $\alpha L$ 项，也就是那辆卡车，从方程中完全消失了。

那么我们的羽毛，$\gamma$ 呢？七个区域中的每一个在拓扑上都是一个简单的圆盘，所以每一个都贡献一个 $-\gamma$ 项。这个组合变成了：

$(-\gamma) \times (1+1+1 - 1-1-1 + 1) = -\gamma$

整个宏伟的构造优雅地[凝结](@keyword=coagulation|lang=zh-CN|style=Feynman)成一个单一的值：$-\gamma$。我们设计了一把忽略了卡车、只称量羽毛的秤。这个巧妙的组合就是**Kitaev-Preskill 公式**的核心，它为我们提供了直接通过实验和数值研究[拓扑序](@keyword=topological_order|lang=zh-CN|style=Feynman)隐藏世界的途径。

### $\gamma$ 的意义：任意子动物园的熵

所以，我们分离出了这个神奇的数字 $\gamma$。但它在物理上*是*什么？它代表什么？事实证明，$\gamma$ 是一种名为**[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)**的奇异粒子“幽灵之舞”的熵。

在[拓扑相](@keyword=topological_phases|lang=zh-CN|style=Feynman)中，[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)——也就是真空——并非空无一物。它是一锅翻滚着虚粒子-[反粒子](@keyword=antiparticles|lang=zh-CN|style=Feynman)对的量子汤。当我们进行纠缠切割，将区域 A 与世界其他部分分开时，我们实际上是在边界处将这些粒子对拉开。边界被装饰上一种量子叠加态，包含了该相所能具有的所有可能类型的任意子。$\gamma$ 的值衡量了我们对当前哪种任意子装饰着边界的无知程度——它是这种“任意子不确定性”的[信息熵](@keyword=shannon_s_entropy|lang=zh-CN|style=Feynman)。

令人难以置信的是，这个熵可以直接从这个[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)“动物园”的属性中计算出来。结果是一个深刻的公式：

$\gamma = \ln \mathcal{D}$

在这里，$\mathcal{D}$ 是该相的**总[量子维度](@keyword=quantum_dimension|lang=zh-CN|style=Feynman)**，一个概括了所有[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)类型丰富性和复杂性的数字。它被定义为 $\mathcal{D} = \sqrt{\sum_a d_a^2}$，其中求和遍历所有[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)种类 $a$，而 $d_a$ 是单个[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)类型 $a$ 的**[量子维度](@keyword=quantum_dimension|lang=zh-CN|style=Feynman)**。

对于像电子这样我们熟悉的粒子， $d_a=1$。[量子维度](@keyword=quantum_dimension|lang=zh-CN|style=Feynman) $d_a=1$ 的[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)被称为**阿贝尔任意子**。但是[拓扑相](@keyword=topological_phases|lang=zh-CN|style=Feynman)也可以容纳更奇异的生物，即**[非阿贝尔任意子](@keyword=non_abelian_anyons|lang=zh-CN|style=Feynman)**，它们的 $d_a > 1$（例如，$d_a = \sqrt{2}$）。这些粒子具有更丰富的内部结构，是构建[容错量子计算机](@keyword=fault_tolerant_quantum_computer|lang=zh-CN|style=Feynman)的关键成分。体系中[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)的[量子维度](@keyword=quantum_dimension|lang=zh-CN|style=Feynman)越大，总[量子维度](@keyword=quantum_dimension|lang=zh-CN|style=Feynman) $\mathcal{D}$ 就越大，[拓扑纠缠熵](@keyword=topological_entanglement_entropy|lang=zh-CN|style=Feynman) $\gamma$ 也越大。

### 标志性例子：一个 $\gamma = \ln(2)$ 的世界

让我们用最著名的拓扑相——**$\mathbb{Z}_2$ [自旋液体](@keyword=spin_liquids|lang=zh-CN|style=Feynman)**来使这个概念具体化，它的行为可以通过一个名为**[环面码](@keyword=toric_code|lang=zh-CN|style=Feynman)**的模型完美地捕捉。这个相是[拓扑物质](@keyword=topological_matter|lang=zh-CN|style=Feynman)的“氢原子”。它拥有四种不同类型的阿贝尔[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)（通常标记为 $1, e, m, \epsilon$）。由于是阿贝尔型的，它们的[量子维度](@keyword=quantum_dimension|lang=zh-CN|style=Feynman)都是 1：$d_a=1$。

让我们来计算它的总[量子维度](@keyword=quantum_dimension|lang=zh-CN|style=Feynman)：

$\mathcal{D}^2 = d_1^2 + d_e^2 + d_m^2 + d_\epsilon^2 = 1^2 + 1^2 + 1^2 + 1^2 = 4$

这得出 $\mathcal{D} = \sqrt{4} = 2$。现在，我们可以求出它的[拓扑纠缠熵](@keyword=topological_entanglement_entropy|lang=zh-CN|style=Feynman)：

$\gamma = \ln \mathcal{D} = \ln(2)$

这个优美而简单的数字是该领域最著名的结果之一。它是一个普适的标志。如果一位实验物理学家研究一种奇怪的新材料，并使用 Kitaev-Preskill 构造测量出一个非常接近 $\ln(2) \approx 0.693$ 的 TEE 值，他们就可以非常自信地断定，他们发现了一个实现 $\mathbb{Z}_2$ 拓扑序的真实世界系统。它提供了一种明确无疑的方式来区分这种奇异状态与常规的绝缘体或磁体，对于后者，$\mathcal{D}=1$ 因而 $\gamma = \ln(1) = 0$。

### 不可动摇的[不变量](@keyword=invariant|lang=zh-CN|style=Feynman)

拼图还有最后一块，也是至关重要的一块。为什么我们称 $\gamma$ 为“拓扑”[不变量](@keyword=invariant|lang=zh-CN|style=Feynman)？这个术语意味着一种在平滑形变下保持稳定的性质。对于 $\gamma$ 来说，这种稳定性甚至更为深刻。

想象你处于 $\mathbb{Z}_2$ 拓扑液体中，其特征 TEE 为 $\gamma = \ln(2)$。现在，假设你进行一个微小的局域实验——你用一个磁探针在一个位置测量单个自旋。这个动作会使[波函数坍缩](@keyword=wavefunction_collapse|lang=zh-CN|style=Feynman)，并产生一对局域化的、有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的激发。你无疑扰动了系统。那么 $\gamma$ 会发生什么变化？

绝对没有变化。它顽固地保持在 $\ln(2)$。

一个局域的扰动无法改变定义整个[物相](@keyword=phases_of_matter|lang=zh-CN|style=Feynman)的全局、长程纠缠模式。要改变 $\gamma$，你需要从根本上改变系统的相，例如，通过增强相互作用，直到在量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)中“熔化”这个拓扑液体。这种令人难以置信的稳健性使得 $\gamma$ 成为一个真正的[拓扑不变量](@keyword=topological_invariants|lang=zh-CN|style=Feynman)。它是集体整体的涌现属性，不受局域事件混乱的影响。正是这种[免疫性](@keyword=immunity|lang=zh-CN|style=Feynman)，使得其底层的拓扑序成为构建未来容错量子计算机的有希望的基石。