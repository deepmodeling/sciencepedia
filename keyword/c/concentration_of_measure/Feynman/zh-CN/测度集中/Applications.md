## 应用与跨学科联系：从我们世界的确定性到可能性的空泛

既然我们已经了解了高维空间奇特而美丽的几何学，现在让我们穿越科学的各个领域，看看测度集中这一现象在何处留下了它的印记。你可能会惊讶地发现，这一个抽象的概念，既是塑造我们日常经验中可预测世界的无形之手，又是在我们计算机中制造恼人悖论的根源，更是在[量子技术](@keyword=quantum_technology|lang=zh-CN|style=Feynman)前沿构成一道巨大障碍的挑战。它是一个统一的原则，揭示了那些表面上看起来毫无关联的领域之间深刻的联系。

### [热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)的基石：为何宏观世界是可预测的

让我们从一个司空见惯却又极其深刻的观察开始：大型物体的世界是异常稳定和可预测的。你桌上的一杯咖啡会以平稳、有序的方式冷却下来；它不会自发地沸腾或结冰。你房间里的气压是恒定的；它不会突然在某个角落消失，而在另一个角落加倍。为什么？毕竟，这些物体是由天文数字般的分子组成的，每一个分子都是一个微小的混乱因子，在疯狂的随机运动中嗡嗡作响、相互碰撞。为什么秩序能从这种微观的混乱中涌现出来？

答案就是测度集中。考虑一个房间里气体的总能量。这个宏观能量是无数单个分子能量的总和。虽然任何单个分子的能量波动剧烈，但许多[随机变量之和](@keyword=sums_of_random_variables|lang=zh-CN|style=Feynman)的性质受大数定律支配。总能量的[标准差](@keyword=standard_deviation|lang=zh-CN|style=Feynman)，即其典型波动的量度，随粒子数 $N$ 的增长而增长，即 $\sigma_E \propto \sqrt{N}$。然而，总能量本身是一个[广延性质](@keyword=extensive_properties|lang=zh-CN|style=Feynman)，意味着它与粒子数成正比，即 $\langle E \rangle \propto N$。

那么，*相对*涨落会发生什么？能量通常会偏离其总值的多少比例？这个比率是
$$
\frac{\sigma_E}{\langle E \rangle} \propto \frac{\sqrt{N}}{N} = \frac{1}{\sqrt{N}}
$$
当粒子数 $N$ 变得天文数字般巨大——达到 $10^{23}$ 的量级时——这个比率变得小到可以忽略不计。总能量的[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)变得极其、异常地尖锐，“集中”在其平均值周围。这意味着，对于一个宏观系统，几乎其粒子的任何微观构型都会产生一个与平均能量无法区分的总能量。这个性质，被称为**自平均性**，是整个平衡[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学建立的基础[@problem_id:2946253]。这就是为什么温度和压强是定义明确、稳定的量，也是为什么[微正则系综](@keyword=nve_ensemble|lang=zh-CN|style=Feynman)和[正则系综](@keyword=nvt_ensemble|lang=zh-CN|style=Feynman)提供的系统图像在[热力学极限](@keyword=thermodynamic_limit|lang=zh-CN|style=Feynman)下会变得等价。我们世界中令人安心的可预测性，是其由众多部分组成的直接统计后果。

### 硬币的另一面：[维度灾难](@keyword=curse_of_dimensionality|lang=zh-CN|style=Feynman)

测度集中通过揭示在高维空间中几乎所有点都是“典型的”，从而给予我们确定性。但如果我们寻找的是*非典型*的东西呢？如果我们关心的性质并非绝大多数点所共有，那会怎样？在这里，同样的原理从福音变成了诅咒。

想象你是一位试图为一个国家[经济建模](@keyword=economic_modeling|lang=zh-CN|style=Feynman)的经济学家。经济状态可以用一个包含数千个变量的向量来描述——利率、失业率、生产水平、股价等等。让我们将这个[状态表示](@keyword=state_representation|lang=zh-CN|style=Feynman)为一个高维空间中的点，比如一个[超立方体](@keyword=hypercube|lang=zh-CN|style=Feynman) $[0,1]^d$，其中 $d$ 非常大。现在，假设经济的[动态稳定](@keyword=dynamic_stabilization|lang=zh-CN|style=Feynman)、健康的状态并不占据整个空间，而是被限制在其中一个更小、更低维的区域——也许是一条薄薄的“管道”或[流形](@keyword=manifold|lang=zh-CN|style=Feynman)，其中某些经济关系成立[@problem_id:2439730]。

你将如何找到这样的状态？一种天真的方法可能是在状态空间中[随机抽样](@keyword=random_sampling|lang=zh-CN|style=Feynman)，直到你幸运地落在一个好的点上。这个策略注定要失败。这个稳定管道的体积只占超立方体总体积的无限小的一部分。随着维度 $d$ 的增长，一个随机点落入你目标区域的概率会以指数速率消失。

测度集中给了我们更深层次的直觉。问题不仅在于空间很大；还在于其结构是反直觉的。高维超立方体中的随机点并非[均匀分布](@keyword=uniform_distribution|lang=zh-CN|style=Feynman)。它们倾向于聚集在一个远离中心和角落的狭窄带内——一种“中纬度”区域。你所关心的那个特殊的、低维的稳定状态[流形](@keyword=manifold|lang=zh-CN|style=Feynman)几乎肯定不位于这个典型区域。实际上，高维空间大部分是空的，而随机点都挤在一个你并不关心的区域。

这就是臭名昭著的**维度灾难**。它困扰着机器学习、数据分析和数值计算。它告诉我们，我们不能指望通过简单地随机探索来理解高维系统。唯一的前进道路是发现隐藏的、低维的结构——就像那个稳定状态的管道一样——并将我们的努力集中在那里。

同样的原理也可能以更微妙的方式表现出来。在有许多输入的复杂模型中，任何单个输入的影响都可能被“冲淡”。如果一个系统的行为取决于 $d$ 个不同因素的平均值，根据链式法则，系统对其中任何一个因素的敏感度都会被稀释一个因子 $1/d$。随着 $d$ 的增长，模型会变得异常“平坦”，对单个变量的变化不敏感[@problem_id:2439739]。这可能是一个真实的结构性效应，或者，令人不安的是，它可能是我们[数值方法](@keyword=numerical_methods|lang=zh-CN|style=Feynman)的人为产物，这些方法因维度灾难而失效，可能过于粗糙而无法解析系统的真实复杂性。

### 一个现代前沿：[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的[贫瘠高原](@keyword=barren_plateaus|lang=zh-CN|style=Feynman)

我们的旅程在现代科学最激动人心的前沿之一达到高潮：[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)。在这里，[测度集中现象](@keyword=concentration_of_measure|lang=zh-CN|style=Feynman)不再是历史的解释或[数据科学](@keyword=data_science|lang=zh-CN|style=Feynman)的麻烦，而是阻碍进步的一个核心且强大的障碍。

许多[量子算法](@keyword=quantum_algorithms|lang=zh-CN|style=Feynman)，如[变分量子本征求解器](@keyword=variational_quantum_eigensolver|lang=zh-CN|style=Feynman)（VQE），旨在找到分子的最低能量状态——这是化学和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)中的一个关键问题。其方法在概念上很简单：你使用一个带有可调“旋钮”（参数）的[量子线路](@keyword=quantum_circuits|lang=zh-CN|style=Feynman)来创建一个[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，测量其能量，然后根据梯度（能量景观的斜率）调整旋钮以找到最小值。

麻烦在于，在许多现实场景中，这个[能量景观](@keyword=energy_landscape|lang=zh-CN|style=Feynman)几乎是完全平坦的。梯度处处为零，无法提供任何关于该朝哪个方向转动旋钮的指导。你迷失在一片广阔、毫无特征的沙漠中。这种现象被称为**[贫瘠高原](@keyword=barren_plateaus|lang=zh-CN|style=Feynman)**[@problem_id:2917634]。

原因再次是测度集中。$n$ 个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的状态是[希尔伯特空间](@keyword=hilbert_spaces|lang=zh-CN|style=Feynman)中的一个向量，该空间的维度为 $D = 2^n$。这个维度是双[指数增长](@keyword=exponential_growth|lang=zh-CN|style=Feynman)的，其增长速度令人难以置信。一个具有类随机结构且深度足够的变分线路，实际上是在这个巨大的空间中制备一个“随机”态。正如我们所学到的，高维空间中随机态的性质是高度集中的。你能够创建的几乎任何状态的[能量期望值](@keyword=expectation_value_of_energy|lang=zh-CN|style=Feynman)，都将无限接近于整个空间的[平均能量](@keyword=average_energy|lang=zh-CN|style=Feynman)。在可能状态构成的景观中，能量的方差随着 $n$ 指数级缩小，其标度为 $1/D = 2^{-n}$。

由于梯度与能量差有关，它也指数级地消失。优化景观之所以平坦，不是因为它简单，而是因为它过于复杂和高维，以至于从一个随机的起点出发，所有方向看起来都一样[@problem_id:2917634] [@problem_id:2439739]。

有办法走出这片沙漠吗？值得注意的是，解释这个问题的理论本身也指明了解决方案。[贫瘠高原](@keyword=barren_plateaus|lang=zh-CN|style=Feynman)的出现是因为我们在一个过大的空间中进行搜索。如果我们能限制搜索范围呢？对于化学系统，我们有强大的物理原理可供利用：对称性。例如，我们知道在任何[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)中，电子数 $N$ 是守恒的。

通过设计我们的[量子线路](@keyword=quantum_circuits|lang=zh-CN|style=Feynman)来内在地尊重这种对称性，我们就不再是在探索完整的、$2^n$ 维的希尔伯特空间。相反，我们将搜索限制在恰好有 $N$ 个电子的状态子空间内。这个子空间的维度要小得多：它由二项式系数 $\binom{n}{N}$ 给出。如果 $N$ 是一个小的常数，这个维度只随 $n$ [多项式增长](@keyword=polynomial_growth|lang=zh-CN|style=Feynman)，如同 $\Theta(n^N)$。

效果是显著的。梯度方差不再按 $2^{-n}$ 标度，而是按反多项式 $\Theta(n^{-N})$ 标度。指数级的[贫瘠高原](@keyword=barren_plateaus|lang=zh-CN|style=Feynman)消失了，取而代之的是一个梯度虽然可能很小但不再被指数级抑制的景观。我们有了一线机会去找到最小值[@problem_id:2823855]。这提供了一个深刻的教训：要驯服数学上的[维度灾难](@keyword=curse_of_dimensionality|lang=zh-CN|style=Feynman)，我们必须挥舞物理上的对称性之剑。

从[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)的钟表般精确到现代计算的棘手挑战，测度集中是一个深刻且反复出现的主题。它是一个鲜明的提醒，告诉我们多维度的世界是一个我们才刚刚开始完全理解的陌生领域。对它的研究揭示了科学版图美丽而又常常令人惊讶的统一性，一个单一的几何思想便能阐明一个咖啡杯、一个国民经济和一个[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的奥秘。