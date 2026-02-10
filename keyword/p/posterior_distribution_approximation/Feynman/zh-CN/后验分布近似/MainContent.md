## 引言
在现代统计学领域，[贝叶斯推断](@keyword=bayesian_inference|lang=zh-CN|style=Feynman)为我们根据新证据更新信念提供了一个强大的框架。其目标是计算后验分布，这是我们在观测到数据后对模型参数所知信息的完整总结。然而，一个重大的障碍常常挡在面前：一个被称为边缘[似然](@keyword=likelihood|lang=zh-CN|style=Feynman)的[归一化常数](@keyword=normalizing_constant|lang=zh-CN|style=Feynman)的计算，它涉及一个高维且通常难以处理的积分。这个计算瓶颈使我们无法直接处理[后验分布](@keyword=posterior_distribution|lang=zh-CN|style=Feynman)，从而在贝叶斯理论及其实际应用之间造成了关键的知识鸿沟。

本文旨在直面这一挑战，全面概述为近似[后验分布](@keyword=posterior_distribution|lang=zh-CN|style=Feynman)而发展出的主要策略。第一章“原理与机制”将深入探讨四类主要近似方法背后的核心思想：[拉普拉斯近似](@keyword=laplace_approximation|lang=zh-CN|style=Feynman)、[变分推断](@keyword=variational_inference|lang=zh-CN|style=Feynman)（VI）、[马尔可夫链蒙特卡洛](@keyword=markov_chain_monte_carlo|lang=zh-CN|style=Feynman)（MCMC）和[近似贝叶斯计算](@keyword=approximate_bayesian_computation|lang=zh-CN|style=Feynman)（ABC）。随后的“应用与跨学科联系”一章将展示这些强大的技术如何应用于物理学、生物学和机器学习等不同领域，以解锁新的科学见解。

## 原理与机制

贝叶斯推断的核心是一个简洁而优美的公式：[贝叶斯定理](@keyword=bayes__theorem|lang=zh-CN|style=Feynman)。它告诉我们如何根据新证据（**[似然](@keyword=likelihood|lang=zh-CN|style=Feynman)**）来更新我们的信念（**先验**[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)），从而形成一个新的、更完备的信念（**后验**[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)）。[后验分布](@keyword=posterior_distribution|lang=zh-CN|style=Feynman)包含了我们在观测数据后可能知道的关于未知参数的一切。在某种意义上，它是我们推断问题的完整答案。

那么，问题出在哪里？为什么我们需要一个完整的领域来*近似*这个答案？困难并不潜藏在[贝叶斯定理](@keyword=bayes__theorem|lang=zh-CN|style=Feynman)的分子中（它只是[似然](@keyword=likelihood|lang=zh-CN|style=Feynman)和先验的乘积），而是在分母中。这个被称为**边缘[似然](@keyword=likelihood|lang=zh-CN|style=Feynman)**或**证据**的项，涉及一个特别棘手的计算：分子对所有可能的参数值进行积分。在任何现实的复杂问题中，我们的参数并非存在于一条简单的数轴上，而是位于一个高维空间中，这使得该计算成为一个艰巨的、往往不可能完成的[高维积分](@keyword=high_dimensional_integration|lang=zh-CN|style=Feynman)。

没有这个归一化常数，我们只知道后验分布的*形状*，但不知道其绝对尺度。想象一下，你精确地知道一个山脉的地形，却不知道海平面在哪里。你可以找到最高峰，但你无法说出它的绝对海拔，也无法计算出山脉在某一高度以上的总体积。同样，没有证据项，我们就无法为参数空间的某些区域赋予确切的概率，也无法计算有意义的平均值。我们被迫寻找巧妙的方法来处理这个未归一化的后验分布，而这种必要性催生了三种巧妙的发明：确定性近似、[变分方法](@keyword=variational_methods|lang=zh-CN|style=Feynman)和[随机模拟](@keyword=stochastic_simulation|lang=zh-CN|style=Feynman)。

### 山之巅峰：[拉普拉斯近似](@keyword=laplace_approximation|lang=zh-CN|style=Feynman)

最简单、最直接的方法是找到唯一最可信的一组参数，并围绕它建立我们的近似。这个最可信的点就是我们[后验概率](@keyword=posterior_probability|lang=zh-CN|style=Feynman)山峰的顶峰，即[后验概率](@keyword=posterior_probability|lang=zh-CN|style=Feynman)密度最高的地方。我们称之为**最大后验**（MAP）估计。

**[拉普拉斯近似](@keyword=laplace_approximation|lang=zh-CN|style=Feynman)**正是基于这一思想。它做出了一个大胆但通常有效的假设：在其峰值附近，后验分布看起来很像一个[高斯分布](@keyword=gaussian_distribution|lang=zh-CN|style=Feynman)，或称“钟形曲线”。我们如何找到合适的那个高斯分布呢？我们求助于数学家工具库中最强大的工具之一：[泰勒级数](@keyword=taylor_series|lang=zh-CN|style=Feynman)。通过分析后验密度的对数并在[MAP估计](@keyword=map_estimation|lang=zh-CN|style=Feynman)点附近进行展开，我们可以为局部地形创建一个简化的蓝图。根据定义，[一阶导数](@keyword=first_derivative|lang=zh-CN|style=Feynman)在峰值处为零。神奇之处在于[二阶导数](@keyword=second_derivative|lang=zh-CN|style=Feynman)，即**Hessian**矩阵，它描述了峰值的曲率[@problem_id:3289090]。一个急剧弯曲的峰意味着后验非常集中，对应于一个[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)较小的[高斯分布](@keyword=gaussian_distribution|lang=zh-CN|style=Feynman)。一个平缓圆润、宽阔的峰则意味着我们的信念更为分散，对应于一个[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)较大的[高斯分布](@keyword=gaussian_distribution|lang=zh-CN|style=Feynman)[@problem_id:3395937]。

例如，假设我们试图估计一枚硬币的偏差 $\theta$。我们从一个先验信念（比如一个Beta[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)）开始，然后抛硬币200次，观察到120次正面。[拉普拉斯近似](@keyword=laplace_approximation|lang=zh-CN|style=Feynman)允许我们找到 $\theta$ 的[MAP估计](@keyword=map_estimation|lang=zh-CN|style=Feynman)以及该点对数后验的曲率。这为我们提供了一个高斯分布的均值和[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)，该[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)近似于我们更新后的信念，然后我们可以用它来计算概率，比如真实偏差 $\theta$ 大于0.5的几率[@problem_id:3281857]。

[拉普拉斯近似](@keyword=laplace_approximation|lang=zh-CN|style=Feynman)的优点在于其速度和简单性。它将一个棘手的积分问题转化为一个容易得多的[优化问题](@keyword=optimization_problem|lang=zh-CN|style=Feynman)（寻找峰值），然后再计算局部曲率。然而，其优点也正是其弱点。它本质上是一种*局部*近似。如果真实的[后验分布](@keyword=posterior_distribution|lang=zh-CN|style=Feynman)不是对称的——如果它是偏斜的或呈香蕉状（这在[非线性模型](@keyword=nonlinear_models|lang=zh-CN|style=Feynman)中很常见）——那么对称的高斯分布将是对事实的拙劣描摹。由[拉普拉斯方法](@keyword=laplace_s_method|lang=zh-CN|style=Feynman)生成的椭球形“可信区域”将与真实的、弯曲且不对称的**最高后验密度（HPD）**区域不匹配，而后者包含了最可能的参数值，并代表了我们信念的真实几何形状[@problem_id:3383384]。

### 雕刻复制品：[变分推断](@keyword=variational_inference|lang=zh-CN|style=Feynman)

如果我们不只是近似峰值，而是尝试创建一个更简单、更易于管理的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)，并将其塑造得尽可能接近整个复杂的[后验分布](@keyword=posterior_distribution|lang=zh-CN|style=Feynman)，那会怎样？这就是**[变分推断](@keyword=variational_inference|lang=zh-CN|style=Feynman)（VI）**背后的哲学。

其策略是选择一个易于处理的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)族，比如高斯分布，我们称之为**变分族**，记作 $q(\theta)$。然后我们试图在该族中找到一个成员，使其成为对我们真实的、难以处理的后验 $p(\theta | y)$ 的“最佳”近似。我们的近似 $q$ 与真实后验 $p$ 之间的“距离”或不相似性由**库尔贝克-莱布勒（KL）散度**来衡量。我们的目标是调整 $q$ 的参数以最小化此散度。

直接最小化KL散度是不可能的，因为它需要知道我们正试图近似的那个后验分布！VI的天才之处在于它通过优化一个替代目标来回避这个问题：**[证据下界](@keyword=evidence_lower_bound|lang=zh-CN|style=Feynman)（ELBO）**。事实证明，最大化ELBO完全等同于最小化KL散度。真实的对数边缘似然与ELBO之间的差值恰好是[KL散度](@keyword=kullback_leibler_divergence|lang=zh-CN|style=Feynman)，而[KL散度](@keyword=kullback_leibler_divergence|lang=zh-CN|style=Feynman)总是一个非负值。这个差值通常被称为**变分间隙**[@problem_id:3184459]。

通过最大化ELBO，我们同时在推动我们的近似 $q$ 更接近真实后验，并为证据本身找到了一个下界。这将原始的积分问题重构为了一个[优化问题](@keyword=optimization_problem|lang=zh-CN|style=Feynman)：我们搜索变分族的最优参数，使我们的复制品尽可能忠实。一个常见的简化假设，被称为平均场近似，是假设在我们的近似后验中参数是独立的，即使它们在真实后验中并非如此[@problem_id:691486]。

VI通常比其他方法快得多，尤其是在大数据和[深度学习](@keyword=deep_learning|lang=zh-CN|style=Feynman)时代，使用共享的“推断网络”进行**摊销推断**可以为新数据点提供闪电般快速的[后验近似](@keyword=posterior_approximation|lang=zh-CN|style=Feynman)。然而，就像一个使用有限工具的雕塑家一样，VI近似的质量从根本上受到所选变分族灵活性的限制。如果真实的后验是一个复杂的多峰形状，而我们试图用一个简单的高斯分布来近似它，那么无论我们如何优化，都不可避免地会存在差距[@problem_id:3184459]。

### 在山上[随机游走](@keyword=random_walk|lang=zh-CN|style=Feynman)：马尔可夫链蒙特卡洛

第三种截然不同的哲学是放弃寻找一个简洁的解析公式来表示[后验分布](@keyword=posterior_distribution|lang=zh-CN|style=Feynman)。相反，我们可以尝试去*探索*它。这就是**[马尔可夫链蒙特卡洛](@keyword=markov_chain_monte_carlo|lang=zh-CN|style=Feynman)（MCMC）**方法的世界。

其直觉引人入胜：想象一个徒步者在我们的后验分布山脉的表面上进行[随机游走](@keyword=random_walk|lang=zh-CN|style=Feynman)。如果我们巧妙地设计徒步者的移动规则，我们就能确保他们在任何给定区域花费的时间与该区域的海拔（后验概率）成正比。通过定期记录徒步者的位置，我们可以收集到一个参数值列表，即样本。一旦徒步者有足够的时间忘记其起点（一个“预烧期”），这个样本集合就构成了整个后验分布的[忠实表示](@keyword=faithful_representation|lang=zh-CN|style=Feynman)。

这不仅仅是一个比喻，它是一个数学上严谨的过程。“[随机游走](@keyword=random_walk|lang=zh-CN|style=Feynman)”是一个**[马尔可夫链](@keyword=markov_chains|lang=zh-CN|style=Feynman)**，而“巧妙的规则”是一个转移核，其设计具有一个关键属性：它的**[平稳分布](@keyword=stationary_distributions|lang=zh-CN|style=Feynman)**必须与我们的目标后验分布完全相同[@problem_id:1920349]。这保证了从长远来看，该链将产生如同直接从[后验分布](@keyword=posterior_distribution|lang=zh-CN|style=Feynman)中抽取的样本。

这从根本上将MCMC与基于优化的方法区分开来。像[期望最大化](@keyword=expectation_maximization|lang=zh-CN|style=Feynman)（Expectation-Maximization）这样的算法可能会找到[MAP估计](@keyword=map_estimation|lang=zh-CN|style=Feynman)——山脉的唯一峰值——但像**[吉布斯采样](@keyword=gibbs_sampling|lang=zh-CN|style=Feynman)（Gibbs sampler）**这样的[MCMC采样](@keyword=mcmc_sampling|lang=zh-CN|style=Feynman)器提供了一整片点云，描绘出山脉的整个形状，包括其山谷、山脊和次级峰[@problem_id:1920326]。从这些样本中，我们不仅可以计算出单一的最佳猜测，还可以计算[后验均值](@keyword=posterior_mean|lang=zh-CN|style=Feynman)、可信区间以及任何其他关于我们不确定性的总结。

[MCMC方法](@keyword=mcmc_methods|lang=zh-CN|style=Feynman)通常被认为是“黄金标准”，因为只要有足够的时间，它们可以以任何期望的精度近似后验分布。当然，这里的关键是“足够的时间”。运行这些链条在计算上可能非常昂贵，而且诊断链条是否真正收敛到其平稳分布是一门微妙的艺术。

### 当你连山都看不见时：[近似贝叶斯计算](@keyword=approximate_bayesian_computation|lang=zh-CN|style=Feynman)

最后，我们考虑最富挑战性的情景：如果我们甚至无法写出[似然函数](@keyword=likelihood_function|lang=zh-CN|style=Feynman)，该怎么办？这种情况出现在许多领域，从生态学到宇宙学，在这些领域中，我们的模型是复杂的计算机模拟，充当“黑箱”：我们可以输入参数并得到模拟数据，但我们无法写出定义此过程的数学函数 $p(\text{data} | \text{parameters})$。

在这里，一种名为**[近似贝叶斯计算](@keyword=approximate_bayesian_computation|lang=zh-CN|style=Feynman)（ABC）**的非凡技术应运而生。其思想非常简单，近乎幼稚。如果我们无法计算出哪些参数使我们观测到的数据具有高可能性，我们可以转而尝试大量来自先验分布的参数值，为每一个参数值生成一个“伪”数据集，然后看看哪些参数值产生的数据集与我们的真实数据*看起来相似*。那些成功的参数值的集合就是我们对[后验分布](@keyword=posterior_distribution|lang=zh-CN|style=Feynman)的近似。

这引入了两层近似[@problem_id:2521316]。首先，比较整个高维数据集通常是不切实际的。取而代之，我们比较少数几个**摘要统计量**（如均值和[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)）。其次，即使在这些摘要统计量上要求完全匹配也过于严格。因此，如果模拟统计量与观测统计量之间的距离小于某个微小的**容差** $\epsilon$，我们就接受该参数抽样。

ABC是一种“双重近似”方法，但它也是一个不可或缺的工具，使我们能够对那些其他所有方法都束手无策的最复杂的[生成模型](@keyword=generative_models|lang=zh-CN|style=Feynman)进行贝叶斯推断。它证明了驱动现代统计学的实用主义和创造力，即使在山脉本身被迷雾笼罩时，也能找到前进的道路。

