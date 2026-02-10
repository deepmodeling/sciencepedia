## 应用与跨学科联系

我们已经看到，物理学可以用一种非常抽象和强大的方式重新表述。与其思考力的推拉，我们可以想象大自然，以其无穷的智慧，是极其“懒惰”的。它审视一个系统从A点到B点可能采取的每一条路径，并只选择那条使一个特殊量——*作用量*——最小化的路径。这就是[最小作用量原理](@keyword=principle_of_least_action|lang=zh-CN|style=Feynman)。计算这个作用量的秘诀是一个叫做[拉格朗日量](@keyword=lagrangian|lang=zh-CN|style=Feynman)的函数，而对于遍布我们宇宙的连续场，我们使用它的密度，$\mathcal{L}$。

你可能会想，“这是一个聪明的数学技巧，但它到底有什么*用*？”这是一个公平且至关重要的问题。答案是惊人的。事实证明，这个单一的原理不仅仅是对旧力学的一种重新表述；它是一条金线，贯穿几乎所有物理学分支，从吉他弦的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)到宇宙的结构。理论物理学的游戏，在很大程度上，变成了一场探索：为一种现象猜测正确的[拉格朗日密度](@keyword=lagrangian_density|lang=zh-CN|style=Feynman)。如果你猜对了，欧拉-拉格朗日方程将自动为你提供正确的[运动方程](@keyword=equations_of_motion|lang=zh-CN|style=Feynman)。让我们踏上一段旅程，看看这一个想法[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)我们走多远。

### 经典场的交响曲

我们的第一步将我们带入连续材料的真实世界，一个充满波、[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)和流动的世界。想象一根又长又细的金属杆。如果你敲击一端，一个压缩波会沿着它的长度传播。我们如何描述这个过程？我们不需要追踪每一个原子。相反，我们可以把材料的位移 $\eta(x, t)$ 看作一个场。这个场的[拉格朗日密度](@keyword=lagrangian_density|lang=zh-CN|style=Feynman)，一如既往，是动能和势能之间的较量。动能密度来自于质量元的运动，而势能密度来自于材料的弹性拉伸。通过写下一个简单的表达式 $\mathcal{L} = \mathcal{T} - \mathcal{V}$，并转动[欧拉-拉格朗日方程](@keyword=euler_lagrange_equations|lang=zh-CN|style=Feynman)的“曲柄”，正确的波动方程就奇迹般地出现了。这个过程甚至告诉我们波的速度，揭示了它由材料的刚度（[杨氏模量](@keyword=young_s_modulus|lang=zh-CN|style=Feynman)，$E$）和其惯性（质量密度，$\rho$）决定 [@problem_id:1250336]。描述这根简单杆的相同原理也支配着小提琴弦的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)、穿过地壳的[地震波](@keyword=seismic_waves|lang=zh-CN|style=Feynman)，以及将这些话语传到你耳朵里的声音本身。

这个想法不仅限于一维。考虑一个鼓面。它是一个在[张力](@keyword=tension_force|lang=zh-CN|style=Feynman)下伸展的二维膜。当鼓手敲击它时，运动的涟漪向外扩散。在这里，我们同样可以定义一个[拉格朗日密度](@keyword=lagrangian_density|lang=zh-CN|style=Feynman)。动能密度与膜表面的速度有关，而势能密度储存在膜对抗其[张力](@keyword=tension_force|lang=zh-CN|style=Feynman)的拉伸中 [@problem_id:2056521]。[最小作用量原理](@keyword=principle_of_least_action|lang=zh-CN|style=Feynman)随后决定了[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)鼓面美丽而复杂的图案。这不仅仅关乎音乐；同样的物理学也描述了麦克风和扬声器中[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)的振膜，甚至现代超声成像设备（CMUTs）中那些微小而巧妙设计的薄膜。

让我们再大胆一点。我们能描述流体的流动吗，比如掠过飞机机翼的空气？这似乎异常复杂。然而，对于一大类流动，可以定义一个速度势场 $\Phi$。在一个非凡的转折中，事实证明这个场的[拉格朗日密度](@keyword=lagrangian_density|lang=zh-CN|style=Feynman)就是流体的压强 $p$！“自然最小化作用量”的陈述等同于“压强在体积上的积分是[稳态](@keyword=steady_state_2|lang=zh-CN|style=Feynman)的”陈述。从这个优雅的起点，人们可以推导出流体运动的方程。这种方法是如此强大，以至于它甚至可以驾驭[跨音速流](@keyword=transonic_flow|lang=zh-CN|style=Feynman)这个臭名昭著的难题，在[跨音速流](@keyword=transonic_flow|lang=zh-CN|style=Feynman)中，流体速度接近声速，并且可能形成冲击波。可以找到一个简化但仍然极具洞察力的拉格朗日量，它给出了该状态下正确的[非线性方程](@keyword=nonlinear_equations|lang=zh-CN|style=Feynman)，指导着现代飞机的设计 [@problem_id:631067]。

### 基本力的架构

到目前为止，我们描述了*物质*的行为。但是，支配物质相互作用的基本力又如何呢？在这里，[拉格朗日方法](@keyword=lagrangian_method|lang=zh-CN|style=Feynman)揭示了其真正的力量和优雅，将看似不相关的现象统一在一个旗帜下。

19世纪物理学的最高成就是麦克斯韦的电磁理论，它用一套四个相互关联的方程描述了电、磁和光。在拉格朗日的图景中，整个结构坍缩成一行惊人简洁的公式。我们假定，基本的实体不是电场和磁场，而是一个更原始的对象：四维势 $A_\mu$。这个场扮演着电磁宇宙“[广义坐标](@keyword=generalized_coordinates|lang=zh-CN|style=Feynman)”的角色 [@problem_id:1562418]。[拉格朗日密度](@keyword=lagrangian_density|lang=zh-CN|style=Feynman)由一个称为[场强张量](@keyword=field_strength_tensor|lang=zh-CN|style=Feynman) $F_{\mu\nu}$ 的量构成，它衡量了[势场](@keyword=potential_field|lang=zh-CN|style=Feynman)的“旋度”。作用量由你能构建的最简单的标量构成：$\mathcal{L} = -\frac{1}{4} F_{\mu\nu} F^{\mu\nu}$。当我们要求由此拉格朗日量构建的作用量最小化时，麦克斯韦的四个方程就完全呈现出来。整个光的理论，从[无线电波](@keyword=radio_frequency_waves|lang=zh-CN|style=Feynman)到伽马射线，都包含在那一个简单的表达式中。

这一成功如此深远，以至于它成为了描述其他基本力的蓝图。在原子核内部运作的弱核力和强核力，通过一个称为[杨-米尔斯理论](@keyword=yang_mills_theory|lang=zh-CN|style=Feynman)的推广思想来描述。在这里，场不仅仅是数字，而是矩阵，它们拥有一个称为规范不变性的深刻内部对称性。这种对称性是一个物理要求：我们对世界的描述不应该依赖于我们在空间每一点选择的任意内部“[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)”。奇迹在于，我们可以写下一个[拉格朗日量](@keyword=lagrangian|lang=zh-CN|style=Feynman) $\mathcal{L} \propto \text{Tr}(F_{\mu\nu} F^{\mu\nu})$，它*自动*尊重这种对称性。这种[不变性](@keyword=invariance|lang=zh-CN|style=Feynman)由矩阵乘法的一个简单、基本的性质保证：迹运算的循环性 [@problem_id:1563571]。粒子物理学最深刻的原理，用这种语言来说，被编码在代数的基本规则之中。

### 从量子领域到宇宙

[拉格朗日密度](@keyword=lagrangian_density|lang=zh-CN|style=Feynman)的[影响范围](@keyword=range_of_influence|lang=zh-CN|style=Feynman)延伸到无穷小和宇宙之大。在量子世界中，粒子由[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman) $\psi$ 描述，其演化由薛定谔方程决定。这似乎与经典场相去甚远。但如果我们*将*[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman) $\psi$ 视为一个经典的[复标量场](@keyword=complex_scalar_field|lang=zh-CN|style=Feynman)呢？我们能为它找到一个[拉格朗日密度](@keyword=lagrangian_density|lang=zh-CN|style=Feynman)吗？

确实可以。通过写下一个涉及 $\psi$ 及其[导数](@keyword=derivative|lang=zh-CN|style=Feynman)的貌似合理的[拉格朗日量](@keyword=lagrangian|lang=zh-CN|style=Feynman)，并应用欧拉-拉格朗日方程，我们可以推导出[含时薛定谔方程](@keyword=time_dependent_schrödinger_equation|lang=zh-CN|style=Feynman)本身 [@problem_id:1092854]。这是一个令人震惊且深刻的结果。它表明，量子力学在其核心上是一种[场论](@keyword=field_theory|lang=zh-CN|style=Feynman)。这个观点是通往量子[场论](@keyword=field_theory|lang=zh-CN|style=Feynman)（QFT）的门户，这是我们描述粒子物理学最成功的框架，其中粒子被视为其底层量子场的激发。

在这些高等理论中，[拉格朗日密度](@keyword=lagrangian_density|lang=zh-CN|style=Feynman)是万能钥匙。它不仅给出[运动方程](@keyword=equations_of_motion|lang=zh-CN|style=Feynman)，还告诉我们如何计算系统的能量和动量。通过对[拉格朗日密度](@keyword=lagrangian_density|lang=zh-CN|style=Feynman)进行勒让德变换，我们得到哈密顿密度，它代表了场的能量密度 [@problem_id:392042]。更普遍地，[拉格朗日密度](@keyword=lagrangian_density|lang=zh-CN|style=Feynman)允许我们构建*[应力-能量-动量张量](@keyword=stress_energy_momentum_tensor|lang=zh-CN|style=Feynman)* $T^{\mu\nu}$。这个至关重要的对象告诉我们关于系统中能量和动量流动的一切。它是爱因斯坦广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)中的源项——正是它告诉[时空](@keyword=space_time|lang=zh-CN|style=Feynman)如何弯曲的“东西” [@problem_id:1843609]。

这把我们带到了最宏大的舞台：宇宙本身。我们有描述宇宙物质和能量含量的[应力-能量张量](@keyword=stress_energy_tensor|lang=zh-CN|style=Feynman) $T^{\mu\nu}$，它从其自身的[拉格朗日量](@keyword=lagrangian|lang=zh-CN|style=Feynman)导出。但是什么支配着[时空](@keyword=space_time|lang=zh-CN|style=Feynman)——这个万物上演的舞台——的动力学呢？在爱因斯坦的构想中，[时空](@keyword=space_time|lang=zh-CN|style=Feynman)不是一个静态的背景，而是一个动态的场，即度规[张量](@keyword=tensor|lang=zh-CN|style=Feynman) $g_{\mu\nu}$。如果它是一个动态场，它必须有一个拉格朗日量。

[爱因斯坦-希尔伯特作用量](@keyword=einstein_hilbert_action|lang=zh-CN|style=Feynman)正是为此而生。真空中引力的[拉格朗日密度](@keyword=lagrangian_density|lang=zh-CN|style=Feynman)被提议为能从[时空几何](@keyword=spacetime_geometry|lang=zh-CN|style=Feynman)中构建出的最简单的标量：[里奇标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman) $R$ [@problem_id:1881216]。最小作用量原理，应用于引力拉格朗日量和物质[拉格朗日量](@keyword=lagrangian|lang=zh-CN|style=Feynman)之和，得出了[爱因斯坦场方程](@keyword=einstein_s_field_equations|lang=zh-CN|style=Feynman)。自然的“懒惰”编排了物质与几何之间的宇宙之舞。

如果我们对宇宙的观测需要新的物理学怎么办？当天文学家发现宇宙的膨胀正在加速时，他们需要对理论进行修正。在[拉格朗日](@keyword=lagrange|lang=zh-CN|style=Feynman)框架中，解决方案异常简单。我们只需添加最简单的一项：一个常数。在引力[拉格朗日密度](@keyword=lagrangian_density|lang=zh-CN|style=Feynman)中加入一个宇宙学常数 $\Lambda$，会修改得到的场方程，使其包含一种宇宙斥力，从而驱动我们今天观察到的加速膨胀 [@problem_id:1881243]。

### 现实的代码

从[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)的杆到宇宙的加速膨胀，由[拉格朗日密度](@keyword=lagrangian_density|lang=zh-CN|style=Feynman)驱动的[最小作用量原理](@keyword=principle_of_least_action|lang=zh-CN|style=Feynman)提供了一个统一且惊人优雅的框架。它允许我们通过猜测一个单一、简单的函数来推导自然法则。它将深刻的物理对称性与简单的数学性质联系起来。它是一种工具、一种语言和一种哲学指南。这一个原理能在如此广阔的尺度和现象范围内奏效，是我们已经揭示的关于宇宙最深刻的真理之一。物理学正在进行的探索可以被看作是寻找终极[拉格朗日密度](@keyword=lagrangian_density|lang=zh-CN|style=Feynman)——一个有朝一日可能从中推导出所有自然法则的单一表达式。