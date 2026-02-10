## 应用与跨学科联系

在我们游览了[非凸优化](@keyword=non_convex_optimization|lang=zh-CN|style=Feynman)的形式化原理之后，你可能会感到一丝不安。我们了解到一个充满陷阱的世界：险峻的景观，有无数的山谷和山峰，我们可信赖的向导——梯度——只能承诺将我们带到最近的平地，那可能是一个深渊，也可能只是[山坡](@keyword=hill_slope|lang=zh-CN|style=Feynman)上的一个小凹坑。这是否意味着我们的数学工具正在失效？恰恰相反。这正是故事变得激动人心的地方。

凸优化就像研究一个完美的球体在一个完美光滑的碗中滚动时的物理学。它优美、可预测，并具有深刻的洞察力。但真实世界不是一个光滑的碗。它是一个由锯齿状山脉、复杂机械、活细胞、智能体组成的世界。非[凸性](@keyword=convexity|lang=zh-CN|style=Feynman)不是一种需要避免的病态；它是复杂性和丰富性的数学印记。在本章中，我们将踏上一场探险，看看非[凸性](@keyword=convexity|lang=zh-CN|style=Feynman)的挑战如何不仅是理论上的奇特现象，而且是当今科学和工程中最迷人问题的本质所在。

### 数字心智：机器学习与[数据科学](@keyword=data_science|lang=zh-CN|style=Feynman)

也许没有任何地方比重塑我们现代世界的领域——机器学习——更能体现非[凸性](@keyword=convexity|lang=zh-CN|style=Feynman)的创造性[张力](@keyword=tension_force|lang=zh-CN|style=Feynman)了。

[深度学习](@keyword=deep_learning|lang=zh-CN|style=Feynman)革命的核心是[人工神经网络](@keyword=artificial_neural_networks|lang=zh-CN|style=Feynman)。我们一层一层地构建这些网络，希望它们能学会看、说、推理。是什么赋予[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)力量？是决定输入信号是否足够强以传递下去的非线性“火花”——[激活函数](@keyword=activation_functions|lang=zh-CN|style=Feynman)。一个纯线性[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)组成的网络将只是一个复杂的线性函数，无法学习世界的丰富模式。但我们引入这个关键的非线性的那一刻，我们就离开了凸性的纯净世界。训练网络——即最小化其预测与现实之间误差的任务——变成了一场穿越令人难以置信的高维、非凸景观的旅程 [@problem_id:3108395]。每个局部最小值代表一组不同的已学“概念”，而我们的训练[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，如[梯度下降](@keyword=gradient_descent|lang=zh-CN|style=Feynman)，本质上是在这片复杂的地形中摸索着下山，希望能落入一个对应于有用模型的山谷中。深度学习的巨大成功证明了一个惊人的事实：在这些特定的非凸景观中，即使是局部最小值也可以非常强大。

但非[凸性](@keyword=convexity|lang=zh-CN|style=Feynman)甚至出现在更经典的[数据科学](@keyword=data_science|lang=zh-CN|style=Feynman)任务中。考虑主成分分析（PCA），这是一种用于在数据集中找到最重要模式的基石方法。其目标是找到一组新的坐标轴，以最好地捕捉数据的方差。一个基本要求是这些新轴必须相互垂直，即*标准正交*。这个看似简单的几何约束——轴矩阵 $U$ 必须满足 $U^{\top}U = I$——迫使我们的解生活在一个被称为[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)上。这个可行集不是一个平坦、凸的空间；它更像是球体的表面。试图在这样一个[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)上进行优化，本质上是一个非凸问题 [@problem_id:3108377]。在这里，非凸性并非源于复杂的[目标函数](@keyword=objective_function|lang=zh-CN|style=Feynman)，而是源于问题约束的优雅几何形状。

当我们要求机器不仅从静态数据中学习，而且在一个变化的世界中行动和学习时，挑战就加深了。在[强化学习](@keyword=reinforcement_learning|lang=zh-CN|style=Feynman)（RL）中，一个智能体的策略（其由 $\theta$ 参数化的策略）决定了它的行动。这些行动反过来又影响了它接下来会遇到的世界状态。这就产生了一个反馈循环：智能体学习所依据的数据分布是它试[图优化](@keyword=graph_optimization|lang=zh-CN|style=Feynman)的参数 $\theta$ 本身的函数。这种自指的动态将一个可能简单的优化景观扭曲成一个复杂的、非凸的景观 [@problem_id:3108426]。寻找最优策略就像试图在一个其形状会随着你每走一步而变化的山谷中找到最低点。

非[凸性](@keyword=convexity|lang=zh-CN|style=Feynman)的层次甚至延伸到构建模型本身的过程。我们如何为学习[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)选择最佳的*超参数*，例如[正则化](@keyword=regularization|lang=zh-CN|style=Feynman)强度 $\alpha$？这是一个“元问题”，通常被构建为[双层优化](@keyword=bilevel_optimization|lang=zh-CN|style=Feynman)：上层寻求最佳的 $\alpha$ 以最小化验证误差，而下层则为给定的 $\alpha$ 训练一个模型 $w(\alpha)$。即使下层训练是一个完美的凸问题，连接这两个层次的数学条件（特别是[Karush-Kuhn-Tucker条件](@keyword=karush_kuhn_tucker_conditions|lang=zh-CN|style=Feynman)）也会引入变量的乘积。这些乘积在上层造成了非[凸性](@keyword=convexity|lang=zh-CN|style=Feynman)，使得寻找最佳学习“配方”本身就是一个非凸问题 [@problem_id:3192346]。

### 构建物理世界

如果数字世界是非凸的，那么物理世界更是如此。物理定律和现实的约束很少像我们希望的那样简单。

想象一下，编程一架无人机从A点飞到B点。最小化燃料可能是一个凸目标。但现在，在其路径上放置一座摩天大楼。无人机必须避开这个障碍物。无人机所有“安全”位置的集合现在是整个天空*减去*摩天大楼的体积。这个“禁入”区使得轨迹的可行空间从根本上变得非凸。你不能简单地在建筑物的两侧各取一个安全点，然后假设它们之间的直线也是安全的 [@problem_id:3108319]。这个直观的[碰撞避免](@keyword=collision_avoidance|lang=zh-CN|style=Feynman)例子是[机器人学](@keyword=robotics|lang=zh-CN|style=Feynman)和控制领域中非凸性最常见的来源之一。为了解决这类问题，工程师们经常使用巧妙的迭代技术，如序列凸规划（SCP），其中艰巨的非凸问题通过解决一系列更简单的、局部凸的近似问题来处理——就像通过规划一系列短的、直线的徒步来穿越山脉一样。

这一原则可以扩展到为我们整个社会提供动力的系统。最优潮流（OPF）问题每天都在被解决，以便廉价而可靠地输送电力。然而，交流电（AC）的物理学由三角函数（[相角](@keyword=phase_angle|lang=zh-CN|style=Feynman)差的正弦和余弦）和双线性项（电压幅值的乘积）控制。这些关系正非凸性的定义 [@problem_id:3108414]。为完整的交流最优潮流（AC-OPF）问题找到全局最优解是NP难问题，是工程学中的一个巨大挑战。实践中经常使用的著名的“直流近似”无非是一个战略决策，即忽略[无功功率](@keyword=reactive_power|lang=zh-CN|style=Feynman)和其他非线性因素，有效地假装问题是凸的，以获得一个快速的近似解。

有时，非凸性并非源于自然，而是源于我们对实用性的渴望。经典的[线性二次调节器](@keyword=lqr_controller|lang=zh-CN|style=Feynman)（LQR）是控制理论的一颗明珠，是一个动态控制问题中罕见而美丽的实例，它是凸的并且可以被精确求解。但最优的[LQR控制器](@keyword=lqr_controller|lang=zh-CN|style=Feynman)通常是一个“稠密”矩阵，意味着每个传感器都必须能够影响每个执行器。在一个大型复杂系统中——比如电网或卫星星座——这可能是不可能的或成本高昂的。如果我们施加一个实际要求，即控制器必须是*稀疏的*或*分散的*（例如，增益矩阵 $K$ 的某些项必须为零），我们就打破了问题优雅的[凸性](@keyword=convexity|lang=zh-CN|style=Feynman)。同时满足这种结构约束的[稳定控制器](@keyword=stabilizing_controllers|lang=zh-CN|style=Feynman)集合变成了一个奇异、不连通、非凸的形状，问题变得极其难以解决 [@problem_id:2913473]。在这里，我们看到了一个深刻的教训：对设计简单性的追求可能导致优化中的巨大复杂性。

### 从离散选择到量子力学

非[凸性](@keyword=convexity|lang=zh-CN|style=Feynman)的触角远远超出了工程和机器学习的连续世界。

考虑组合问题，这些问题是关于做出离散选择的。想象一下，将一组工人分配给一组任务以最大化整体效率（二次[分配问题](@keyword=assignment_problem|lang=zh-CN|style=Feynman)），或者试图匹配两个不同图像之间的特征（图匹配）。这里的可行集不是一个连续空间，而是一个有限的、由不同可能性组成的集合——[置换矩阵](@keyword=permutation_matrix|lang=zh-CN|style=Feynman)。你不能处于“将工人A分配给任务1”和“将工人B分配给任务2”的“中间”状态。这种离散性使得可行集本质上是非凸的 [@problem_id:3108368]。这类问题通常是NP难的，它们的非凸性质是其困难的根源。这里一个强大的思想是*松弛*：我们可以将离散的、非凸的[置换矩阵](@keyword=permutation_matrix|lang=zh-CN|style=Feynman)集合[嵌入](@keyword=embedding|lang=zh-CN|style=Feynman)到一个更大的、连续的、凸的集合（双[随机矩阵](@keyword=stochastic_matrix|lang=zh-CN|style=Feynman)的Birkhoff多胞体）中。在这个松弛集上解决问题可以得到真实最优值的界限，并可以为找到原始更难问题的良好解提供线索。

最后，我们来到了最终的前沿：量子领域。化学和物理学中最基本的挑战之一是找到分子的基态能量。这个值决定了[化学反应性](@keyword=chemical_reactivity|lang=zh-CN|style=Feynman)、材料性质，并且是药物发现的关键。量子力学的变分原理为我们的主题提供了一个美丽的联系：它指出*任何*试验[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)的[能量期望值](@keyword=expectation_value_of_energy|lang=zh-CN|style=Feynman)都是真实[基态能量](@keyword=ground_state_energy_2|lang=zh-CN|style=Feynman)的上界。[变分量子本征求解器](@keyword=variational_quantum_eigensolver|lang=zh-CN|style=Feynman)（VQE），一种用于近期[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的旗舰[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，将此转化为一个优化任务。一个量子电路准备一个由经典参数 $\theta$ 控制的试验态 $| \psi(\theta) \rangle$。能量 $E(\theta) = \langle \psi(\theta) | H | \psi(\theta) \rangle$ 被测量，一个经典优化器调整 $\theta$ 以找到可能的最低能量。这个[能量景观](@keyword=energy_landscape|lang=zh-CN|style=Feynman) $E(\theta)$ 总的来说是一个高度非凸的函数 [@problem_id:2917666]。因此，找到一个分子的真实[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)等同于在一个复杂的、非凸的景观中找到[全局最小值](@keyword=global_minimum|lang=zh-CN|style=Feynman)——这是物理学、化学、计算机科学和优化理论[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)领域的一个巨大挑战。

从数字大脑中的[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)到分子中的电子，非[凸性](@keyword=convexity|lang=zh-CN|style=Feynman)是规则，而非例外。它是反馈、物理约束、离散选择和量子力学的数学语言。科学和工程的持续旅程，在许多方面，是一场寻求开发更聪明、更强大的工具来驾驭这些美丽而崎岖的景观的征途，不是为了夷平它们，而是为了在它们的山谷中找到隐藏的深刻而强大的解决方案。