## 引言
在原子尺度的世界里，理解和预测物质的行为依赖于我们对原子间相互作用力的精确描述，这通常由[原子间势](@keyword=interatomic_potentials|lang=zh-CN|style=Feynman)函数（简称“势函数”）来定义。传统上，开发精确的势函数是一个耗时耗力的“炼金”过程，而直接使用高精度的第一性原理计算（如密度泛函理论，DFT）来进行大规模分子动力学模拟又因其高昂的计算成本而受到极大限制。近年来，机器学习（ML）为这一困境带来了曙光，它能够从DFT数据中学习，以接近量子力学的精度和远超传统[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)的计算速度来预测原子间的能量和力。然而，一个根本性的问题依然存在：我们应该选择哪些原子构型来训练ML模型，才能以最少的DFT计算量获得最强大、最通用的[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)？

本文正是为了解答这一问题，将深入探讨“用于[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)开发的主动学习工作流”。主动学习（Active Learning, AL）是一种智能的[数据采集](@keyword=data_acquisition|lang=zh-CN|style=Feynman)策略，它将[机器学习模型](@keyword=machine_learning_models|lang=zh-CN|style=Feynman)从被动的数据接收者转变为一个主动的“提问者”。它能够自主识别自身知识的薄弱环节，并“请求”更高精度的计算来填补这些知识空白。通过本篇文章，你将踏上一场从基本原理到前沿应用的探索之旅。

在第一章“原理与机制”中，我们将解构[主动学习](@keyword=active_learning|lang=zh-CN|style=Feynman)的核心框架，理解它如何将物理对称性原则融入模型架构，并通过一个优雅的认知循环实现自我完善。接着，在第二章“应用与[交叉](@keyword=chiasmata|lang=zh-CN|style=Feynman)学科联系”中，我们将见证这一强大方法如何在广阔的科学领域大显身手，从预测材料的宏观力学性质，到探索[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)的复杂路径，再到将量子效应纳入经典模型。最后，在第三章“动手实践”中，你将有机会通过一系列精心设计的练习，将理论知识转化为解决实际问题的能力，亲身体验如何[量化不确定性](@keyword=quantifying_uncertainty|lang=zh-CN|style=Feynman)并做出智能决策。让我们开始吧！

## 原理与机制

在引言中，我们已经对主动学习（Active Learning, AL）构建[原子间势](@keyword=interatomic_potentials|lang=zh-CN|style=Feynman)函数的工作流程有了一个鸟瞰式的了解。现在，让我们像物理学家一样，深入其内部，探究其运转的核心原理与机制。这趟旅程将向我们揭示，一个优雅的计算框架如何将基础物理定律、统计学思想和计算策略融为一体，将繁重的“炼丹”过程转变为一场高效、智能的科学发现之旅。

### 万物有理：物理定律的对称性

我们的宇宙遵循着一些美妙而深刻的对称性原则。无论你将一个孤立的原子系统平移到太空的哪个角落，或是将它旋转一个任意的角度，其内在的物理规律，尤其是它的总能量，都保持不变。此外，如果你交换两个同种类的原子（比如两个氢原子）的标签，物理系统本身并不会有任何实质性的改变。物理学中，我们称之为**[平移不变性](@keyword=translational_invariance|lang=zh-CN|style=Feynman)**、**[旋转不变性](@keyword=rotational_invariance|lang=zh-CN|style=Feynman)**和**[置换不变性](@keyword=permutation_invariance|lang=zh-CN|style=Feynman)**。

任何一个忠实于物理现实的[原子间势](@keyword=interatomic_potentials|lang=zh-CN|style=Feynman)函数，都必须无条件地遵守这些对称性。如果一个模型做不到这一点，那么它在[分子动力学模拟](@keyword=molecular_dynamics_simulations|lang=zh-CN|style=Feynman)中就会产生荒谬的结果——比如，一个分子仅仅因为在模拟盒子里的位置不同，或者朝向不同，就会拥有不同的能量，这显然是错误的。

那么，我们如何在[机器学习模型](@keyword=machine_learning_models|lang=zh-CN|style=Feynman)中注入这些物理学知识呢？这引出了两种绝妙的设计哲学：**[不变性](@keyword=invariance|lang=zh-CN|style=Feynman)描述符（invariant descriptors）**和**[等变性](@keyword=equivariance|lang=zh-CN|style=Feynman)架构（equivariant architectures）**。

第一种思路，即[不变性](@keyword=invariance|lang=zh-CN|style=Feynman)描述符，非常直观：我们不要直接把原子的三维[笛卡尔坐标](@keyword=cartesian_coordinates|lang=zh-CN|style=Feynman)（它们会随着[旋转和平移](@keyword=rotation_and_translation|lang=zh-CN|style=Feynman)而改变）喂给[机器学习模型](@keyword=machine_learning_models|lang=zh-CN|style=Feynman)，而是先将这些坐标“预处理”成一组不随[刚性运动](@keyword=rigid_motions|lang=zh-CN|style=Feynman)变化的“指纹”。想象一下，要描述一个原子周围的环境，我们不关心这个环境的绝对朝向，只关心它内部的几何关系。我们可以计算该原子与邻近原子之间的所有**距离**，以及由原子三元组构成的所有**键角**。这些量天然地满足旋转和平移不变性。通过对同种类的邻居原子求和，我们又能满足[置换不变性](@keyword=permutation_invariance|lang=zh-CN|style=Feynman)。诸如**[原子中心对称函数](@keyword=atom_centered_symmetry_functions|lang=zh-CN|style=Feynman)（ACSF）**和**原子位置光滑重叠（SOAP）**这样的著名描述符，正是基于这一思想构建的。[@problem_id:3394167] 它们将每个原子的局部环境编码成一个固定的向量，这个向量就像是原子的“身份证”，无论系统如何旋转平移，这张身份证上的信息都不会改变。然后，机器学习模型（比如[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络）的任务就简化为学习从这张“身份证”到原子能量的映射关系。

第二种思路，即[等变性](@keyword=equivariance|lang=zh-CN|style=Feynman)架构，则更为精巧和深入。它不要求输入是完全不变的，而是构建一个能够理解并处理对称性变换的[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络。这里的核心概念是**[等变性](@keyword=equivariance|lang=zh-CN|style=Feynman)（equivariance）**。一个函数$f$如果对于变换$g$是等变的，意味着先对输入$x$做变换再送入函数，其结果$f(g(x))$与先计算函数值再对输出做变换$g(f(x))$是完全一样的。对于力而言，它就是一个矢量。当我们旋转整个原子系统时，作用在每个原子上的力矢量也应该随之旋转，而不是保持不变或随意改变。一个**[SE(3)等变图神经网络](@keyword=se(3)_equivariant_gnn|lang=zh-CN|style=Feynman)**正是为此而生。[@problem_id:3394205] 它在网络层之间传递的不仅仅是标量信息（如能量），还包括矢量（如力、偶极矩）甚至更高阶的张量信息。网络的每一层操作（如卷积）都被精心设计，以保证这些带方向性的信息能够按照物理规律正确地变换。

这两种方法都确保了最终的能量预测是严格不变的，而力的预测是严格等变的。这不仅使得模型物理上正确，还极大地提升了学习效率。模型不再需要从数据中“猜测”[旋转不变性](@keyword=rotational_invariance|lang=zh-CN|style=Feynman)这一基本事实，而是将其作为先验知识内置于结构之中。更有趣的是，这种内置的对称性保证了模型的[不确定性估计](@keyword=uncertainty_estimation|lang=zh-CN|style=Feynman)也同样遵守对称性。例如，对于一个等变模型，一个原子构型和它旋转后的版本，其预测力的不确定性（例如通过系综模型计算的协方差矩阵）也会相应地旋转，而衡量不确定性大小的标量值（如协方差矩阵的迹）则会保持不变。[@problem_id:3394205] 这意味着[主动学习](@keyword=active_learning|lang=zh-CN|style=Feynman)在选择下一个采样点时，不会因为构型的朝向不同而做出不同的判断，保证了决策的物理一致性。

### 认知循环：在模拟中学习

构建了物理上自洽的模型架构后，我们如何高效地喂给它数据呢？这便是主动学习的核心——一个模仿人类科学发现过程的**认知循环（epistemic cycle）**。[@problem_id:3394145] [@problem_id:3394132] 我们可以将这个[循环分解](@keyword=cycle_decomposition|lang=zh-CN|style=Feynman)为四个关键步骤：**假设**、**实验**、**证据**和**更新**。

1.  **假设 (Hypothesis)**：我们当前拥有的[原子间势](@keyword=interatomic_potentials|lang=zh-CN|style=Feynman)函数$U(\mathbf{R}; \theta)$就是我们的“假设”。它代表了我们目前对原子间相互作用规律的最佳理解，由参数$\theta$所定义。在贝叶斯视角下，这个假设更是一个关于参数$\theta$的[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)$p(\theta \mid \mathcal{D}_t)$，反映了在已有数据集$\mathcal{D}_t$下参数的不确定性。

2.  **实验 (Experiment)**：我们如何检验这个假设？答案是让它动起来！我们将当前的势函数作为分子动力学（MD）模拟的引擎，通过求解[牛顿第二定律](@keyword=newton_s_second_law|lang=zh-CN|style=Feynman) $m_i \ddot{\mathbf{r}}_i(t) = -\nabla_{\mathbf{r}_i} U(\mathbf{R}(t); \theta)$ 来生成原子运动的轨迹。这个过程被称为“**采样器（Sampler）**”。MD模拟就像一场计算实验，它探索着在当前“物理定律”（即我们的势函数）下，系统会自然演化到哪些新的、可能前所未见的状态。

3.  **证据 (Evidence)**：在实验过程中，我们的“**学习器（Learner）**”（即机器学习模型）会持续监控模拟，并对自己说：“对于轨迹上的这个[新构型](@keyword=newforms|lang=zh-CN|style=Feynman)，我的预测有多大的把握？” 这就引出了“**不确定性**”的概念。当学习器发现某个构型的**[认知不确定性](@keyword=epistemic_uncertainty|lang=zh-CN|style=Feynman)（epistemic uncertainty）**非常高，意味着它进入了知识的“无人区”，它的预测很可能是错误的。此时，学习器会触发一次“提问”。它将这个高不确定性的构型$\mathbf{R}_q$提交给一个更高精度的“**神谕（Oracle）**”，通常是昂贵的量子力学计算方法，如[密度泛函理论](@keyword=density_functional_theory|lang=zh-CN|style=Feynman)（DFT）。神谕会返回该构型下“真实”的能量和力。这些新获得的、带有精确标签的数据，就是我们用来挑战和完善旧假设的“**证据**”。

4.  **更新 (Update)**：学习器将新证据（新的DFT数据点）并入现有的训练数据集$\mathcal{D}_t$中，形成新的数据集$\mathcal{D}_{t+1}$。然后，它通过重新训练或使用[贝叶斯更新](@keyword=bayesian_updating|lang=zh-CN|style=Feynman)规则来调整模型参数$\theta$，得到一个更精确、更可靠的新假设$p(\theta \mid \mathcal{D}_{t+1})$。这个新模型在新证据点上的预测会更准确，[认知不确定性](@keyword=epistemic_uncertainty|lang=zh-CN|style=Feynman)也会相应降低。

就这样，循环往复。[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)在探索中驱动模拟，模拟在不确定处触发学习，学习在证据上完善[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)。这是一个自洽且不断自我改进的闭环系统，它让计算资源能够“好钢用在刀刃上”，只在最需要的地方进行昂贵的DFT计算。

### 提问的艺术：如何高效地探索未知

认知循环的效率在很大程度上取决于第三步——如何聪明地“提问”。一个好的提问策略（即**[采集函数](@keyword=acquisition_function|lang=zh-CN|style=Feynman), acquisition function**）能让我们用最少的DFT计算，最大程度地提升势函数的精度和泛化能力。这背后，是对“不确定性”更深层次的理解和运用。[@problem_id:3394195]

#### 不确定性的两种面孔：无知与随机

首先，我们必须严格区分两种性质截然不同的不确定性。[@problem_id:3394170]

*   **[认知不确定性](@keyword=epistemic_uncertainty|lang=zh-CN|style=Feynman) (Epistemic Uncertainty)**：源于我们知识的匮乏。它是因为我们的训练数据有限，模型参数$\theta$未能被唯一确定而产生的。这种不确定性是可以通过增加更多（有信息量的）数据来降低的。它本质上是模型的“无知”。

*   **偶然不确定性 (Aleatoric Uncertainty)**：源于数据生成过程内在的随机性或噪声。例如，DFT计算本身存在数值[收敛容差](@keyword=convergence_tolerance|lang=zh-CN|style=Feynman)，或者我们描述的物理过程本身就包含随机涨落。这种不确定性是系统固有的“噪音”，即使拥有无限的数据也无法消除。

[主动学习](@keyword=active_learning|lang=zh-CN|style=Feynman)的核心目标是**降低认知不确定性**。我们想要探索的是模型未知的领域，而不是反复去测量那些本身就充满噪音的区域。如果一个[采集函数](@keyword=acquisition_function|lang=zh-CN|style=Feynman)错误地将偶然不确定性当作[认知不确定性](@keyword=epistemic_uncertainty|lang=zh-CN|style=Feynman)来追逐，就会导致所谓的“追逐噪音”——在一些本质上就模糊不清的区域浪费大量的计算资源，而对提升模型的全局认知毫无帮助。[@problem_id:3394131]

#### 从[分歧](@keyword=ramification|lang=zh-CN|style=Feynman)到共识：量化模型的“无知”

那么，我们如何定量地估算一个模型的[认知不确定性](@keyword=epistemic_uncertainty|lang=zh-CN|style=Feynman)呢？一个非常直观且强大的方法是**深度系综（deep ensembles）**。[@problem_id:3394138] 想象一下，我们不只训练一个神经[网络模型](@keyword=network_models|lang=zh-CN|style=Feynman)，而是独立地训练多个（比如5个或10个）结构相同但初始权重随机化的模型。对于一个给定的原子构型，如果所有模型都给出了非常接近的预测，我们就说模型系综达成了“共识”，[认知不确定性](@keyword=epistemic_uncertainty|lang=zh-CN|style=Feynman)很低。反之，如果它们的预测五花八门、[分歧](@keyword=ramification|lang=zh-CN|style=Feynman)很大，那么这恰恰说明模型系综对这个区域感到“困惑”，认知不确定性很高。这个“分歧”的大小（例如，通过计算预测值的[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)）就成了衡量认知不确定性的绝佳指标。

另一种更轻量级的方法是**[蒙特卡洛](@keyword=monte_carlo|lang=zh-CN|style=Feynman) Dropout (MC Dropout)**。在训练[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络时，Dropout是一种[防止过拟合](@keyword=prevent_overfitting|lang=zh-CN|style=Feynman)的技术，它会在每次训练迭代中随机“关闭”一部分神经元。在预测时，我们通常会关闭Dropout功能。但MC Dropout反其道而行之：在预测时，我们保持Dropout开启，并对同一个输入进行多次（例如几十次）随机[前向传播](@keyword=forward_pass|lang=zh-CN|style=Feynman)。每次传播由于随机关闭的神经元不同，会得到一个略微不同的结果。这一系列结果的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)，可以被看作是对模型[后验分布](@keyword=posterior_distribution|lang=zh-CN|style=Feynman)的一种近似采样，其[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)同样可以用来估计[认知不确定性](@keyword=epistemic_uncertainty|lang=zh-CN|style=Feynman)。

然而，仅仅得到一个不确定性的数值是不够的。我们还需要保证这个数值是**校准过（calibrated）**的。一个良好校准的模型，当它预测某个值的[标准差](@keyword=standard_deviation|lang=zh-CN|style=Feynman)为$\hat{\sigma}$时，其真实误差的[均方根](@keyword=root_mean_square|lang=zh-CN|style=Feynman)也应该约等于$\hat{\sigma}$。换句话说，模型的“自信程度”应该与它的“实际能力”相匹配。我们可以通过在一个独立的[验证集](@keyword=validation_set|lang=zh-CN|style=Feynman)上绘制校准图，或者计算[标准化残差](@keyword=standardized_residuals|lang=zh-CN|style=Feynman)的统计量，来检验和修正模型的[不确定性估计](@keyword=uncertainty_estimation|lang=zh-CN|style=Feynman)，确保我们的“提问”是基于可靠的“自我认知”。[@problem_id:3394138] [@problem_id:3394131]

#### 最佳提问策略：不确定性，多样性，还是[信息增益](@keyword=information_gain|lang=zh-CN|style=Feynman)？

有了量化不确定性的方法，我们就可以设计[采集函数](@keyword=acquisition_function|lang=zh-CN|style=Feynman)了。最简单的策略是**最大[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)（Maximum Variance）**，即选择模型系综预测[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)最大的构型进行标注。但这一定是最好的策略吗？

思考这样一个场景：在主动学习的初期，我们的训练数据非常稀少。此时模型的[不确定性估计](@keyword=uncertainty_estimation|lang=zh-CN|style=Feynman)本身可能就非常不可靠。如果完全信任这个不靠谱的“向导”，我们可能会过早地聚焦于某个它碰巧认为不确定的狭窄区域，而忽略了广阔的未知世界。在这种情况下，一个更稳健的策略是**仅考虑多样性（diversity-only）**，例如**最远点采样（Farthest Point Sampling, FPS）**。[@problem_id:3394176] 这种策略完全不看模型的预测或不确定性，它只在描述符空间中选择与现有训练数据点距离最远的新点。它的目标是尽快地、尽可能均匀地“铺满”整个[构型空间](@keyword=configuration_space|lang=zh-CN|style=Feynman)，建立一个最基本的[认知地图](@keyword=cognitive_maps|lang=zh-CN|style=Feynman)。这对于保证早期MD模拟的稳定性至关重要，因为它能有效降低遇到灾难性外推（即走到离所有已知数据都极远的区域）的风险。

随着数据的增多，模型逐渐变得可靠，纯粹基于不确定性的采样开始展现其威力。然而，更深思熟虑的策略会问一个更本质的问题：“标注哪个点能带给我关于模型参数**最大的[信息增益](@keyword=information_gain|lang=zh-CN|style=Feynman) (information gain)**？”

从信息论的角度看，最优的选择是能最大程度降低后验分布$p(\theta \mid \mathcal{D})$熵的点。一个漂亮的近似结果是，[信息增益](@keyword=information_gain|lang=zh-CN|style=Feynman)正比于$\log(1 + \sigma_{\text{ep}}^{2} / \sigma_{\text{al}}^{2})$。[@problem_id:3394131] 这个公式告诉我们，最有价值的点，是那些认知不确定性$\sigma_{\text{ep}}^{2}$相对于偶然不确定性$\sigma_{\text{al}}^{2}$的比值最大的地方。这完美地契合了我们的直觉：我们应该在“信号”（我们的无知）远大于“噪音”（系统内在随机性）的地方进行测量。

最终，一个先进的、鲁棒的[主动学习](@keyword=active_learning|lang=zh-CN|style=Feynman)工作流，其[采集函数](@keyword=acquisition_function|lang=zh-CN|style=Feynman)往往是多种思想的融合。例如，一个综合性的[采集函数](@keyword=acquisition_function|lang=zh-CN|style=Feynman)可能会是这样：
$$
a(x) = \underbrace{\frac{1}{2}\log\left(1 + \frac{\hat{\sigma}_{\text{ep}}^{2}(x)}{\hat{\sigma}_{\text{al}}^{2}(x)}\right)}_{\text{校准后的信息增益}} + \underbrace{\lambda d(x)}_{\text{探索奖励}}
$$
这里，第一项是基于校准后[不确定性估计](@keyword=uncertainty_estimation|lang=zh-CN|style=Feynman)的[信息增益](@keyword=information_gain|lang=zh-CN|style=Feynman)，它负责“深度挖掘”；第二项$d(x)$是一个**探索奖励（exploration bonus）**，它奖励那些远离现有数据点的新构型，确保了探索的“广度”；$\lambda$则是一个平衡两者的超参数。

通过这样精巧的设计，主动学习工作流就像一位经验丰富的探险家，既有勇气深入未知洞穴的腹地，又不忘时时回顾地图，确保没有遗漏任何一片广袤的森林。正是这种原理与策略的精妙结合，使得我们能够以前所未有的效率和精度，构建出描绘原子世界的强大势函数。