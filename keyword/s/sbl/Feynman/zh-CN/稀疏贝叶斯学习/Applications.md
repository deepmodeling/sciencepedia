## 应用与跨学科联系

我们花了一些时间来理解[稀疏贝叶斯学习](@keyword=sparse_bayesian_learning|lang=zh-CN|style=Feynman)（SBL）的内部机制。我们已经看到，在[证据最大化](@keyword=evidence_maximization|lang=zh-CN|style=Feynman)的引导下，[自动相关性确定](@keyword=automatic_relevance_determination|lang=zh-CN|style=Feynman)（ARD）这一巧妙的原则如何通过剪除不必要的组件来自动简化模型。这是一项优雅的数学工程。但一个科学原理的真正美妙之处，不仅在于观察其齿轮和杠杆，更在于驾驶它上路，看看它能驶向何方。我们能用这个想法*做*什么？它又与哪些其他思想领域相连？事实证明，这一个简单的想法——让数据来决定模型的哪些部分是相关的——在机器学习、信号处理甚至科学哲学本身都产生了深远的影响。让我们开始我们的巡礼。

### 相关向量机：由[稀疏性](@keyword=sparsity|lang=zh-CN|style=Feynman)驱动的核学习器

SBL 最著名的应用之一是一个被称为**相关向量机（RVM）**的模型。这段旅程始于机器学习世界中一个强大的思想：核（kernels）。想象一下，你想对某个复杂的[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)函数建模。一个巧妙的技巧是将你的输入数据投影到一个更高维的空间，希望在这个空间里关系变得更简单。[核函数](@keyword=kernel_function|lang=zh-CN|style=Feynman)使我们能够隐式地做到这一点，而无需实际构建那个高维空间。

RVM 采纳了这个想法，并以一种优美的方式将其与 ARD 结合起来。它提出了一个模型，其中每个[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)都以*每一个训练数据点*为中心 [@problem_id:3433905]。如果你有一千个数据点，你就会从一个包含一千个[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)的模型开始。这听起来像是灾难的配方，一个无可救药的过拟合案例！但 SBL 的魔力就在于此。通过在每个[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)的权重上设置一个独立的[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)超参数，ARD 自动确定哪些[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)对于解释数据是真正“相关的”。在[证据最大化](@keyword=evidence_maximization|lang=zh-CN|style=Feynman)过程中，大多数这些权重的[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)被推向零，从而有效地将它们对应的[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)从模型中剪除。最终你得到的是原始数据点的一个小[子集](@keyword=subset|lang=zh-CN|style=Feynman)——“相关向量”——它们足以定义所学到的函数。

这种方法为著名的[支持向量机](@keyword=support_vector_machines|lang=zh-CN|style=Feynman)（SVM）提供了一个引人入胜的贝叶斯替代方案。虽然 SVM 也能识别出一个“[支持向量](@keyword=support_vectors|lang=zh-CN|style=Feynman)”的[子集](@keyword=subset|lang=zh-CN|style=Feynman)，但 RVM 是从一个完全概率化的角度来做这件事的。这意味着它不仅给你一个预测，还给出了对自己不确定性的度量——即[误差棒](@keyword=error_bars|lang=zh-CN|style=Feynman)。此外，RVM 通常比 SVM 稀疏得多，意味着它使用的相关向量要少得多，从而在预测时得到一个更紧凑、计算速度更快的模型。

而且这个想法不仅仅适用于回归。通过一些数学上的技巧，我们可以将其扩展到[分类问题](@keyword=classification_problems|lang=zh-CN|style=Feynman)。分类的[似然函数](@keyword=likelihood_function|lang=zh-CN|style=Feynman)（例如，逻辑斯蒂回归）不是简单的高斯分布，这使得贝叶斯推断中的积分变得难以处理。然而，通过使用一种称为[拉普拉斯近似](@keyword=laplace_approximation|lang=zh-CN|style=Feynman)的技术，我们可以用一个[高斯分布](@keyword=gaussian_distribution|lang=zh-CN|style=Feynman)来近似非高斯[后验分布](@keyword=posterior_distribution|lang=zh-CN|style=Feynman)，从而将整个 SBL 机制应用到这个新情境中，构建一个稀疏的[概率分类](@keyword=probabilistic_classification|lang=zh-CN|style=Feynman)器 [@problem_id:3433909]。

你可能会想，这个寻找相关向量的过程实际上是如何工作的？我们是否必须测试所有可能的[子集](@keyword=subset|lang=zh-CN|style=Feynman)？不，而且其算法和模型一样优雅。我们可以贪心地构建模型，从一个空的[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)集开始，迭代地添加那个能最大程度增加边缘[似然](@keyword=likelihood|lang=zh-CN|style=Feynman)的[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)。得益于线性代数中的一些优美结果，如 Sherman-Morrison-Woodbury 公式，我们可以极其高效地计算任何候选[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)带来的证据增量，而无需从头重新拟合整个模型 [@problem_id:3433897]。该算法逐个“嗅出”最相关的[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)，以一种高效的方式构建一个稀疏模型。

### 学习特征本身

到目前为止，我们让 SBL 从一个大型的、预定义的池中选择要包含哪些[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)。但如果我们也能学习[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)本身的*形状*呢？例如，如果我们使用高斯核，那么最佳的宽度或“长度尺度”是多少？窄核捕捉精细细节，而宽核则模拟平滑趋势。

令人难以置信的是，完全相同的[证据最大化](@keyword=evidence_maximization|lang=zh-CN|style=Feynman)原则可以回答这个问题。核超参数，如长度尺度，可以被视为与 ARD [方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)一起优化的[附加参数](@keyword=accessory_parameters|lang=zh-CN|style=Feynman)。通过计算对数边缘[似然](@keyword=likelihood|lang=zh-CN|style=Feynman)相对于这些核参数的梯度，我们可以使用[基于梯度的优化](@keyword=gradient_based_optimization|lang=zh-CN|style=Feynman)来自动调整它们。这意味着 SBL 提供了一个单一、统一的框架，不仅用于选择一组稀疏的特征，还用于从数据中学习这些特征的最优形式 [@problem_id:3433902]。这是自动化方面的一个巨大进步，使我们从模型选择走向了一种更广义的*模型发现*。我们付出的代价是[优化问题](@keyword=optimization_problem|lang=zh-CN|style=Feynman)通常是非凸的，意味着我们可能会找到局部最优解，但通过仔细的初始化和优化策略，这种方法在实践中非常强大。

### 从机器学习到信号处理：学习字典

现在让我们把注意力从机器学习转向信号处理的世界。在这里，一个核心思想是信号——无论是音频、图像还是传感器读数——通常可以表示为来自一个“字典”的基本“原子”的稀疏组合。这是压缩感知的基础。通常，这个字典是预先定义的（例如，使用傅里叶或[小波基](@keyword=wavelet_basis|lang=zh-CN|style=Feynman)）。

但如果我们不知道哪种字典最适合某一类信号呢？我们能从样本中学习它吗？SBL 提供了一个绝佳的答案。我们可以将 ARD 应用于*字典原子*本身，而不是信号的*系数*。我们从一个包含大量潜在原子的超完备字典开始。当我们向算法输入样本信号时，它会尝试用这些原子的稀疏组合来解释它们。如果某个特定的字典原子总是被忽略，如果它对于解释数据从来不是“相关的”，那么 ARD 机制就会通过将其相关的精度超参数推向无穷大来自动剪除它 [@problem_id:3433914]。

从数据中浮现出来的是一个紧凑、定制化的字典，完美地适用于手头的信号。这是一个极其强大的思想。它使我们能够，例如，自动学习自然图像的基本组成部分或脑电图（EEG）信号中的[特征模式](@keyword=characteristic_modes|lang=zh-CN|style=Feynman)。当然，现实世界也带来了挑战。如果字典原子高度相似或相关，标准的 SBL 算法可能难以决定保留哪一个。这促进了更复杂算法的发展，例如块坐标更新，它会同时考虑和更新一组相关的原子，从而实现更快、更有效的剪枝 [@problem_id:3433872]。这展示了[统计建模](@keyword=statistical_modeling|lang=zh-CN|style=Feynman)和[数值优化](@keyword=numerical_optimization|lang=zh-CN|style=Feynman)之间美妙的相互作用。

### [结构化稀疏性](@keyword=structured_sparsity|lang=zh-CN|style=Feynman)：洞察全局

我们的世界充满了结构化数据。一幅图像不仅仅是一个长长的像素向量；它是一个具有相关行和列的网格。一个视频在空间和时间上都有相关性。一个将每个变量都独立对待的简单稀疏模型可能会忽略这个更大的图景。

再一次，SBL 的贝叶斯框架证明其足够灵活，可以融入这种结构性知识。对于像图像这样的矩阵形状信号，我们可以设计一个尊重其二维性质的先验。利用[克罗内克积](@keyword=tensor_product_of_matrices|lang=zh-CN|style=Feynman)的代数，我们可以构建一个可分离的协[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)，其中一部分描述沿行的相关性，另一部分描述沿列的相关性。然后我们可以将 SBL 的原理应用于这个结构化先验。由此产生的算法可以学习，例如，图像的哪些行或列最重要，同时利用克罗内克代数的数学优雅性来保持[计算效率](@keyword=computational_efficiency|lang=zh-CN|style=Feynman)，避免处理庞大无比的[协方差矩阵](@keyword=covariance_matrix|lang=zh-CN|style=Feynman) [@problem_id:3493468]。这一扩展使我们能够将[稀疏性](@keyword=sparsity|lang=zh-CN|style=Feynman)的力量带到成像、[遥感](@keyword=remote_sensing|lang=zh-CN|style=Feynman)和[多维数据分析](@keyword=multi_dimensional_data_analysis|lang=zh-CN|style=Feynman)等广泛的问题领域。

### 贝叶斯[稀疏性](@keyword=sparsity|lang=zh-CN|style=Feynman)的统一观点

我们已经看到，源于[高斯先验](@keyword=gaussian_priors|lang=zh-CN|style=Feynman)和 ARD 的 SBL 可以以多种方式应用。但它是在贝叶斯稀疏性领域里唯一的选择吗？或者它是否与其他看似不同的思想有所联系？故事在这里变得真正有趣起来。

一种最流行的诱导[稀疏性](@keyword=sparsity|lang=zh-CN|style=Feynman)的方法是使用一个类似于[绝对值函数](@keyword=absolute_value_function|lang=zh-CN|style=Feynman)的先验，即[拉普拉斯分布](@keyword=laplace_distribution|lang=zh-CN|style=Feynman)，它是著名的 [LASSO](@keyword=least_absolute_shrinkage_and_selection_operator|lang=zh-CN|style=Feynman) 中使用的 L1 范数的贝叶斯对应物。乍一看，它在零点的尖峰似乎与高斯分布的平滑形状截然不同。然而，如果我们构建一个层级模型，其拉普拉斯先验的尺度由一个伽马[超先验](@keyword=hyperpriors|lang=zh-CN|style=Feynman)控制，我们就可以推导出一个类 EM 算法来找到最优参数。而当我们这样做时，我们发现一个更新规则看起来异常熟悉：新的超参数是信号幅度当前估计值的一个[简单函数](@keyword=simple_functions|lang=zh-CN|style=Feynman) [@problem_id:3494719]。这揭示了一个深层的联系：许多诱导稀疏性的先验都会导致迭代重加权算法，其中系数的影响力由其当前估计的相关性决定。

最终的比较是与所谓的贝叶斯变量选择的“黄金标准”：**尖峰-厚板**先验。这个模型在哲学上非常直接。它假设每个系数来自两种状态之一：一个“尖峰”（它精确为零）或一个“厚板”（它从一个宽[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)中抽取，如高斯分布）。然后模型计算处于任一状态的[后验概率](@keyword=posterior_probability|lang=zh-CN|style=Feynman)。这似乎与 SBL 的平滑收缩[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)过程相去甚远。

但它们真的如此不同吗？让我们考虑最简单的情况：一个正交标准测量矩阵，此时问题分解为一组独立的标量问题。我们可以推导出尖峰-厚板模型选择一个系数的精确条件——它归结为对与该系数对应的测量值平方的一个阈值。我们也可以推导出 SBL 的[选择规则](@keyword=selection_rules|lang=zh-CN|style=Feynman)；正如我们所见，它也涉及对测量值平方的一个阈值 [@problem_id:3433917]。现在是美妙的部分：我们可以让这两个阈值相等。通过这样做，我们可以在尖峰-厚板模型的参数（[先验几率](@keyword=prior_odds|lang=zh-CN|style=Feynman)和厚板[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)）与 SBL 模型的参数（噪声[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)）之间推导出一个精确的数学关系。在此条件下，这两种方法，尽管其概念起源完全不同，但在决定包含哪些系数和剪除哪些系数方面将做出*完全相同*的决策 [@problem_id:3433946]。

这是一个惊人的统一。它揭示了 SBL，通过其对边缘[似然](@keyword=likelihood|lang=zh-CN|style=Feynman)的平滑优化，实际上在隐式地进行着与尖峰-厚板显式执行的相同的离散[模型比较](@keyword=model_comparison|lang=zh-CN|style=Feynman)。这就像发现两台机器，一台用齿轮，一台用液压，实际上是在实现同一个基本蓝图。这种联系让我们更深刻地体会到贝叶斯推断原则的力量和普适性。一个始于实用工程选择——使用 ARD——的方法，最终与[贝叶斯模型选择](@keyword=bayesian_model_selection|lang=zh-CN|style=Feynman)最严格的基础产生了深刻的联系。而这确实是一件非常美妙的事情。