## 应用与跨学科联系

在上一章中，我们穿过了[运动学](@keyword=kinematics|lang=zh-CN|style=Feynman)中那些微妙且常常令人困惑的水域，最终得出了一个连旋转小行星上的观察者都能认同的应力变化率定义。我们构建了几种“客观”率，包括[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman) $\overset{\mathrm{T}}{\boldsymbol{\sigma}}$。但一个定义，无论多么优雅，仅仅是一个承诺。任何科学概念的真正考验在于它描述世界、解释实验和构建可靠工具的能力。[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)仅仅是一个数学上的奇物，还是一个真正有用的物理概念？俗话说，实践是检验真理的唯一标准。让我们来应用一下[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)。

### 简[单剪切](@keyword=simple_shear|lang=zh-CN|style=Feynman)的严峻考验：两种模型的故事

检验任何力学理论的一个绝妙方法是将其置于一种描述简单但揭示性惊人的情境中：**简[单剪切](@keyword=simple_shear|lang=zh-CN|style=Feynman)**。想象一下用手摊开一副扑克牌。每张牌相对于其下面的一张都发生轻微的滑动。整副牌被变形了，但没有一张牌被拉伸。这个运动是[纯剪切](@keyword=simple_shear|lang=zh-CN|style=Feynman)和连续内旋转的组合，使其成为检验构造不良理论的完美陷阱。

让我们做一个思想实验。假设我们发明一种简单的、理想化的材料，称之为“次弹性”（hypoelastic）固体。对于这种材料，我们假设一个非常简单的定律：其[客观应力率](@keyword=objective_stress_rates|lang=zh-CN|style=Feynman)与其拉伸率成正比。用数学术语来说，我们写作 $\overset{\circ}{\boldsymbol{\sigma}} = 2G\,\boldsymbol{D}$，其中 $\boldsymbol{D}$ 是[拉伸张量](@keyword=stretch_tensor|lang=zh-CN|style=Feynman)，$G$ 是[剪切模量](@keyword=shear_modulus|lang=zh-CN|style=Feynman)，一个衡量刚度的指标。现在关键的选择来了：我们应该使用哪种[客观率](@keyword=objective_rates|lang=zh-CN|style=Feynman) $\overset{\circ}{\boldsymbol{\sigma}}$？

一个自然的第一选择可能是[Jaumann率](@keyword=jaumann_rate|lang=zh-CN|style=Feynman)，这是一个修正了材料平均自旋的流行选择。如果我们将[Jaumann率](@keyword=jaumann_rate|lang=zh-CN|style=Feynman)代入我们的简单定律并模拟简[单剪切](@keyword=simple_shear|lang=zh-CN|style=Feynman)实验，会发生一些奇怪的事情。预测的[剪切应力](@keyword=shear_stress|lang=zh-CN|style=Feynman)并不仅仅是如你所[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的那样增加，而是会[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，随着剪切的继续而上升和下降 [@problem_id:2647754] [@problem_id:2905969]。就好像这种材料正在经历一场良心危机，周期性地变强，然后变弱，再变强。这并不是我们在大多数真实材料中看到的现象。[Jaumann率](@keyword=jaumann_rate|lang=zh-CN|style=Feynman)，尽管其直观上很有吸引力，但似乎被简[单剪切](@keyword=simple_shear|lang=zh-CN|style=Feynman)中固有的连续旋转所误导。

现在，让我们重复这个实验，但这次我们将使用[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)。我们设 $\overset{\mathrm{T}}{\boldsymbol{\sigma}} = 2G\,\boldsymbol{D}$ 并施加相同的[稳态](@keyword=steady_state_2|lang=zh-CN|style=Feynman)剪切。结果完全不同。预测的[剪切应力](@keyword=shear_stress|lang=zh-CN|style=Feynman)随着剪切量的增加而平稳、光滑地增长 [@problem_id:2647754] [@problem_id:2905969]。对于一个被剪切的固体来说，这是一种在物理上更为合理的行为。如果我们观察[正应力](@keyword=normal_stresses|lang=zh-CN|style=Feynman)——即压在“扑克牌”上的应力，同样的故事也会发生。[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)预测了一个合理的、不断增长的[正应力](@keyword=normal_stresses|lang=zh-CN|style=Feynman)，而[Jaumann率](@keyword=jaumann_rate|lang=zh-CN|style=Feynman)再次预测了奇特的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman) [@problem_id:2647763]。

这个测试告诉了我们一些深刻的道理。并不是说[Jaumann率](@keyword=jaumann_rate|lang=zh-CN|style=Feynman)在数学上是“错误”的——它完全是客观的。但是作为构建简单、可预测的材料模型的工具，它可能会惨败。[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)以其更复杂的结构，被证明是一个更稳健、更具物理洞察力的选择。这是一个强有力的提醒：我们的数学选择具有真实的、可测量的物理后果 [@problem_id:2872325]。

### 可压缩性的秘密与Kirchhoff应力的优雅

在这些测试中，是什么赋予了[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)卓越的预测能力？答案的一个关键部分在于一个将它与更简单的随动率区分开来的项：$(\mathrm{tr}\,\boldsymbol{L})\boldsymbol{\sigma}$。量 $\mathrm{tr}\,\boldsymbol{L}$ 衡量的是材料体积的变化率。因此，这一项明确地将应力率与材料的膨胀或压缩联系起来。

想象一个承受一定压力的泡沫块。如果我们突然让它向所有方向膨胀，内力会分布在更大的体积上。应力，即单位*当前*面积上的力，仅仅因为这种几何上的“稀释”效应就会自然下降，甚至在材料内部结构来得及松弛之前。[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)通过其 $(\mathrm{tr}\,\boldsymbol{L})\boldsymbol{\sigma}$ 项，自动且正确地捕捉了这一基本效应 [@problem_id:2666109] [@problem_id:2666480]。缺少这一项的更简单的率基本上对可压缩[材料物理学](@keyword=materials_physics|lang=zh-CN|style=Feynman)中这一重要部分视而不见。

这可能看起来只是又一个修正，但它指向一个更深刻、更优雅的真理。在大变形中，[Cauchy应力](@keyword=cauchy_stress|lang=zh-CN|style=Feynman) $\boldsymbol{\sigma}$（单位当前面积上的力）可能是一个棘手的量，正是因为“当前面积”是一个移动的目标。如果我们转而定义一个相对于*初始*未变形状态的应力呢？这个想法引出了**Kirchhoff应力**，记为 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$，其中 $J$ 是当前体积与初始体积之比。Kirchhoff应力本质上是一种经过缩放以消除体积变化影响的力测量。

在这里，一个美妙的统一时刻出现了。如果我们寻求这个更自然的Kirchhoff应力的最简单[客观率](@keyword=objective_rates|lang=zh-CN|style=Feynman)，我们会得到Oldroyd率 $\boldsymbol{\tau}^{\nabla}$。事实证明，这个简洁明了的 $\boldsymbol{\tau}$ 率与看起来更复杂的 $\boldsymbol{\sigma}$ 的[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)直接相关。其关系惊人地简单 [@problem_id:2610447]：

$$
\overset{\mathrm{T}}{\boldsymbol{\sigma}} = \frac{1}{J} \boldsymbol{\tau}^{\nabla}
$$

[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)的表面复杂性，仅仅是支配Kirchhoff应力的更简单物理学所投下的阴影！[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)中那个“杂乱的”体积项，恰恰是将在参考构型中的简洁物理学转换成变形中的当前构型语言所必需的。

### 从理论到模拟：计算力学的引擎

这种理论上的优雅并不仅仅是作秀，它具有巨大的实际意义。如今，工程师们很少需要建造并摧毁成千上万个汽车或飞机的原型。相反，他们使用基于**[有限元法](@keyword=finite_element_method|lang=zh-CN|style=Feynman)（FEM）**的强大软件来模拟复杂系统在极端条件下的行为——从摩天大楼在地震中的响应到汽车碰撞中安全气囊的充气。

这些模拟必须精确地模拟经历巨大拉伸、扭曲和压缩的材料。为此，它们在时间上一步步地求解基本运动方程和材料的[本构定律](@keyword=constitutive_laws|lang=zh-CN|style=Feynman)。在这里，[客观应力率](@keyword=objective_stress_rates|lang=zh-CN|style=Feynman)的选择不是一个学术细节，而是[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)的核心。

由于其与未变形状态的深刻而清晰的联系（通过Kirchhoff应力），[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)构成了最稳健和广泛使用的计算方法的支柱，尤其适用于**[超弹性](@keyword=superelasticity|lang=zh-CN|style=Feynman)**（hyperelastic）材料——那些能像橡胶一样几乎完美地储存和释放[应变能](@keyword=strain_energy|lang=zh-CN|style=Feynman)的材料 [@problem_id:2709106]。用[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)构建的[本构定律](@keyword=constitutive_laws|lang=zh-CN|style=Feynman)可以通过[时间积分](@keyword=time_integration|lang=zh-CN|style=Feynman)，并与材料潜在的[储能函数](@keyword=energy_storage_function|lang=zh-CN|style=Feynman)保持一致。这确保了模拟不会人为地创造或毁灭能量，否则将导致荒谬的结果 [@problemid:2610447]。

此外，该率的形式对模拟本身的稳定性有直接影响。当这些方程用显式时间步长[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)（就像对[演化过程](@keyword=evolutionary_process|lang=zh-CN|style=Feynman)进行多次快速抓拍）求解时，每个时间步长 $\Delta t$ 必须足够小，以防止[数值解](@keyword=numerical_solution|lang=zh-CN|style=Feynman)“爆炸”。[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)方程的结构本身决定了最大允许时间步长。通过分析与[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)相关的算子的数学特性，工程师可以精确地确定这些稳定性极限。他们发现，例如，快速膨胀可能需要比缓慢剪切小得多、更谨慎的时间步长 [@problem_id:2666517]。这种分析对于创建不仅准确，而且能够运行的模拟至关重要。

### 超越固体：随流而动

我们讨论的这些原理是如此基本，以至于它们的影响从固体力学波及到其他领域。考虑一下**[非牛顿流体](@keyword=non_newtonian_fluids|lang=zh-CN|style=Feynman)**这个奇特而迷人的世界。这些物质，如[聚合物熔体](@keyword=polymer_melts|lang=zh-CN|style=Feynman)、油漆、番茄酱和生物流体，都与水或空气的简单线性行为不同。当你搅拌它们时，它们可以爬上搅拌棒；当你剪切它们时，它们可以在垂直于流动的方向上产生力。

为了描述这种复杂的行为，流变学家们建立的[本构模型](@keyword=constitutive_models|lang=zh-CN|style=Feynman)常常借鉴固体力学的思路。这些流体具有“记忆性”，并能表现出“类弹性”响应。它们的行为通常由关联[应力张量](@keyword=stress_tensor|lang=zh-CN|style=Feynman)与变形率的率型方程来捕捉。与固体中一样，为了具有物理意义，这些方程必须是客观的。因此，毫不奇怪，像[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)这样的[客观率](@keyword=objective_rates|lang=zh-CN|style=Feynman)出现在高级流体模型中，帮助捕捉在这些复杂材料中观察到的奇特而美妙的现象 [@problem_id:472142]。这展示了连续介质力学的统一力量：为理解钢[梁弯曲](@keyword=beam_bending|lang=zh-CN|style=Feynman)而锻造出来的同样深刻的原理，也能够阐明[聚合物熔体](@keyword=polymer_melts|lang=zh-CN|style=Feynman)的流动。

### 结论：一个优选的工具

我们回到最初的问题：[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)是一个*好*的定义吗？证据不言自明。它不仅仅是数学可能性目录中的又一个条目。它是一个经过精心打造、并被反复检验证明其价值的工具。在更简单的率可能导致悖论的情况下，它提供了物理上合理的预测 [@problem_id:2647754]。它通过揭示其与更基本的Kirchhoff应力的联系，优雅地解释了可压缩性的物理学 [@problem_id:2610447]。它为现代科学和工程中不可或缺的计算模拟提供了一个稳健、稳定且一致的基础 [@problem_id:2666517] [@problem_id:2709106]。其概念框架甚至在[复杂流体](@keyword=complex_fluids|lang=zh-CN|style=Feynman)的研究中找到了回响 [@problem_id:472142]。定义“应力变化率”的旅程不仅带领我们找到了一个正确的答案，更获得了一个具有非凡力量和智慧之美的工具——这证明了我们对一个既客观、一致又具有深刻统一性的自然描述的追求。