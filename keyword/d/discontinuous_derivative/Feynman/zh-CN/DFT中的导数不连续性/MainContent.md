## 引言
[密度泛函理论 (DFT)](@keyword=density_functional_theory_dft|lang=zh-CN|style=Feynman) 是量子模拟中最强大和应用最广泛的工具之一，它使科学家能够从第一性原理预测分子和材料的性质。然而，几十年来，它一直存在一个重大缺陷：在预测物质最基本的性质之一——[电子带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)时，会出现系统性且往往是灾难性的失败。这种被称为“[带隙问题](@keyword=band_gap_problem|lang=zh-CN|style=Feynman)”的差异常常错误地将绝缘体预测为金属，削弱了人们对该理论预测能力的信心。该问题的根源在于一个被常见近似所忽略的、电子[能量景观](@keyword=energy_landscape|lang=zh-CN|style=Feynman)中一个微妙但深刻的特性。

本文深入探讨了这个问题及其解决方案的根源：[导数](@keyword=derivative|lang=zh-CN|style=Feynman)[不连续性](@keyword=discontinuity|lang=zh-CN|style=Feynman)。它解决了简单DFT模型失败所造成的基础知识空白。在接下来的两章中，您将对这一关键概念有清晰的理解。在“原理与机制”一章中，我们将探索[基态能量](@keyword=ground_state_energy_2|lang=zh-CN|style=Feynman)令人惊讶的[分段线性](@keyword=piecewise_linearity|lang=zh-CN|style=Feynman)特性，揭示在整数电子数处的“扭折”如何产生一种[不连续性](@keyword=discontinuity|lang=zh-CN|style=Feynman)，而这种不连续性对于准确描述量子系统至关重要。随后，“应用与跨学科联系”将展示这一看似抽象的概念如何在计算[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)、描述[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)中的电荷转移过程、理解溶液中的化学以及开发下一代计算方法等方面具有深远的实际意义。

## 原理与机制

想象一下，你想计算一颗钻石的颜色。这似乎是个简单的问题，对吗？物体的颜色由它吸收的光决定，而这又取决于将一个电子从其舒适的占据态踢到一个更高的空态所需的能量。这个能量差被称为**基本[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)**。几十年来，我们最强大的量[子模](@keyword=submodule|lang=zh-CN|style=Feynman)拟工具——[密度泛函理论 (DFT)](@keyword=density_functional_theory_dft|lang=zh-CN|style=Feynman) 的一大长期困扰与尴尬是，它在预测这些[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)方面惊人的失败。它常常会预测像金刚石这样的绝缘体应该是金属！要理解原因，我们必须踏上一段旅程，进入量子系统奇特而美丽的能量景观。

### 一个电子的能量，多一点或少一点

让我们从一个简单的想法开始。对于任何原子、分子或一块材料，都有一个特定的总能量，我们可以称之为 $E$。如果我们增加或减少电子，这个能量会发生什么变化？我们用 $E(N)$ 表示一个有 $N$ 个电子的系统的能量。如果我们移走一个电子，能量变为 $E(N-1)$。这样做的能量成本就是我们所说的**电离势**，$I = E(N-1) - E(N)$。如果我们增加一个电子，能量变为 $E(N+1)$，释放的能量是**[电子亲和能](@keyword=electron_affinity|lang=zh-CN|style=Feynman)**，$A = E(N) - E(N+1)$。基本[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，即产生一个电子-空穴对的能量，就是移除一个电子的成本与增加一个电子所[获能](@keyword=capacitation|lang=zh-CN|style=Feynman)量之差：$E_g = I - A$ [@2821197] [@2088818]。

到目前为止，这只是简单的计算。但如果我们考虑一个*分数*数量的电子呢？一个有，比如说，$N + \frac{1}{2}$ 个电子的系统能量是多少？这听起来像是无稽之谈。你不可能有半个电子！但在[量子理论](@keyword=quantum_theory|lang=zh-CN|style=Feynman)的世界里，特别是当考虑一个与大电子库接触的系统时，我们可以将这种状态想象成一种统计混合，或称**系综**。一个含有 $N + \alpha$ 个电子的系统可以被看作是在 $(1-\alpha)$ 的时间里是 $N$ 电子系统，在 $\alpha$ 的时间里是 $(N+1)$ 电子系统。

这样一个含分数电子的系统的能量会是多少？由Perdew、Parr、Levy和Balduz首次证明的，整个DFT中最深刻和非直觉的结果之一是，[基态能量](@keyword=ground_state_energy_2|lang=zh-CN|style=Feynman)就是简单的[加权平均](@keyword=weighted_average|lang=zh-CN|style=Feynman)值。总能量 $E$ 对电子数 $N$ 的图像是一系列连接整数电子数点的直线段 [@2821197] [@2639036]。