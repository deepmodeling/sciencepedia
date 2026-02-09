## 引言
机器学习不仅仅是[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)的集合，更是一系列深刻的思维[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)——它们是关于如何从数据中提取知识、做出决策和发现规律的根本性“哲学”。从区分猫狗图像到在保护隐私的同时协同全球智慧，每一种方法的背后都有一种独特的学习[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)在驱动。然而，面对层出不穷的模型和技术，我们往往容易迷失在具体的实现细节中，而忽略了它们背后共通或对立的核心思想。

本文旨在填补这一认知鸿沟，带领读者超越单个[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，去探索和理解塑造了人工智能领域的关键学习[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)。我们将揭示这些[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)如何定义了机器“学习”的不同姿态，它们各自的优势、局限以及它们之间深刻的联系与权衡。

为了系统地展开这场探索之旅，本文将分为三个核心部分。在“原理与机制”一章中，我们将深入各种[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)的内部，剖析它们的核心思想，从经典的监督与[无监督学习](@keyword=unsupervised_learning|lang=zh-CN|style=Feynman)，到颠覆性的神经普通[微分方程](@keyword=differential_equation|lang=zh-CN|style=Feynman)与[自监督学习](@keyword=self_supervised_learning|lang=zh-CN|style=Feynman)。接着，在“应用与跨学科连接”一章中，我们将走出理论的殿堂，看这些[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)如何在生物信息学、金融、物理学等真实世界问题中大放异彩，并与其他学科的智慧碰撞出火花。最后，在“动手实践”部分，您将有机会通过具体的编程练习，亲手实现和体验不同[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)在解决问题时的差异与魅力，从而将理论知识转化为实践能力。

## 原理与机制

在“引言”中，我们已经对机器学习的不同[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)有了初步的印象。现在，让我们像物理学家探索自然法则一样，深入到这些[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)的核心，去欣赏它们背后的原理、机制以及它们所揭示的关于“学习”这一概念本身的美丽与统一。我们将开启一场发现之旅，看看机器是如何从数据中学习，又是如何构建起它们的“世界观”的。

### 有监督与无监督：学习的两种基本姿态

想象一下厨房里的两位厨师。第一位厨师品尝一道菜，然后根据他脑中已有的“菜品分类大全”（比如“川菜”、“粤菜”），给这道菜贴上一个标签。第二位厨师也品尝一道菜，但他没有预设的分类，而是发现了一种前所未有的、令人惊喜的风味组合，从而开创了一个新的“流派”。

这两种行为，恰如其分地描绘了机器学习最基本的两种[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)：**[有监督学习](@keyword=supervised_learning|lang=zh-CN|style=Feynman)（Supervised Learning）**与**[无监督学习](@keyword=unsupervised_learning|lang=zh-CN|style=Feynman)（Unsupervised Learning）**。

[有监督学习](@keyword=supervised_learning|lang=zh-CN|style=Feynman)就像第一位厨师。我们给机器提供大量带有“正确答案”的例子，比如一张张标好“猫”或“狗”的图片。机器的任务是学习一个函数 $f$，这个函数能够将新的输入 $x$（一张未见过的图片）映射到正确的标签 $y$（“猫”或“狗”）。在生物信息学中，科学家们可以利用已知细胞类型的基因表达数据（带有标签的数据集）来训练一个分类器，用以识别新样本中的细胞类型。这本质上是在学习一个已知的“菜品分类大全”[@problem_id:2432871]。

而[无监督学习](@keyword=unsupervised_learning|lang=zh-CN|style=Feynman)则更像是那位富有创造力的第二位厨师。我们只给机器一堆数据，不给任何标签。机器的任务是在数据中自己发现“有趣的结构”。这可能是在庞杂的客户数据中发现隐藏的群体，或是在一片未经探索的[单细胞测序](@keyword=single_cell_sequencing|lang=zh-CN|style=Feynman)数据中，通过[聚类](@keyword=clustering|lang=zh-CN|style=Feynman)发现一种全新的、前所未见的细胞亚群 [@problem_id:2432871]。这并非为了验证已知，而是为了探索未知，发现“新大陆”。

这两种[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)回答了一个根本问题：我们是想让机器复制我们已有的知识，还是去发现我们尚未知晓的规律？

### 判别与生成：画出边界，还是理解世界？

即使在[有监督学习](@keyword=supervised_learning|lang=zh-CN|style=Feynman)的框架内，也存在着不同的“学习哲学”。假设我们的任务是区分“正常”网络流量和“入侵”行为。我们有两种截然不同的策略。

第一种是**[判别模型](@keyword=discriminative_models|lang=zh-CN|style=Feynman)（Discriminative Models）**。这种模型的目标非常直接：学习一个[决策边界](@keyword=decision_boundary|lang=zh-CN|style=Feynman)，将两[类数](@keyword=class_number|lang=zh-CN|style=Feynman)据点分开。它直接对条件概率 $p(y|\mathbf{x})$ 建模，即“给定一个数据点 $\mathbf{x}$，它是入侵行为（$y=1$）的概率是多少？”。逻辑回归就是一个典型的例子。它不关心“正常”流量具体长什么样，也不关心“入侵”行为的千变万化，它只专注于找到那条能将两者最有效分开的线 [@problem_id:3160913]。这就像一个学生为了考试，只学习如何解答题，而不去深究题目背后的原理。

第二种是**[生成模型](@keyword=generative_models|lang=zh-CN|style=Feynman)（Generative Models）**或基于[密度估计](@keyword=density_estimation|lang=zh-CN|style=Feynman)的方法。这种模型试图理解数据是如何“生成”的。它会去学习每个类别的数据分布，即 $p(\mathbf{x}|y)$。例如，我们可以用一个高斯分布去描绘所有“正常”流量的特征。然后，当一个新数据点出现时，我们就计算它由这个“正常”模型生成的概率。如果概率极低，我们便有理由认为它是一个“异常”或“入侵”行为 [@problem_id:3160913]。这就像一个真正理解了物理学的学生，他不仅能解题，还能描述出物理现象的全貌。

这两种[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)在实际应用中各有千秋。当“入侵”行为的数据非常稀少时，[判别模型](@keyword=discriminative_models|lang=zh-CN|style=Feynman)可能难以学习，因为它没有足够多的反例。而[密度估计](@keyword=density_estimation|lang=zh-CN|style=Feynman)方法，只需充分学习“正常”是什么样，就能有效地识别出所有“不正常”。这揭示了一个更深层次的道理：有时候，要识别敌人，最好的方法是先深刻地理解自己。

### 归纳偏见与注意力：内置的直觉 vs. 灵活的思考

当我们设计一个学习模型时，我们面临一个选择：是给它一些“与生俱来”的知识，还是让它从零开始、完全自由地学习？

一种强大的[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)是**归纳偏见（Inductive Bias）**。这指的是我们将关于问题结构的先验知识硬编码到模型架构中。[卷积神经网络](@keyword=convolutional_neural_networks|lang=zh-CN|style=Feynman)（CNN）就是一个杰作。它的核心操作——卷积，具有**[平移等变性](@keyword=translational_equivariance|lang=zh-CN|style=Feynman)（Translation Equivariance）**。这意味着，无论图片中的一只猫出现在左上角还是右下角，卷积层处理它的方式都是一样的。模型不必在每个位置重新学习“猫”的概念。这种“内置的直觉”使得CNN在处理图像等具有空间结构的数据时极为高效和强大 [@problem_id:3160958]。

而另一种新兴的[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)则走向了另一个极端：**注意力机制（Attention Mechanism）**，尤其是[Transformer架构](@keyword=transformer_architecture|lang=zh-CN|style=Feynman)中的[自注意力](@keyword=self_attention|lang=zh-CN|style=Feynman)。它放弃了大部分的结构化偏见，允许模型在计算每个位置的输出时，“关注”到输入中的任何其他位置，并根据数据动态地计算它们之间的关系权重。它不像CNN那样被预设为只能处理局部信息。原则上，它足够灵活，可以学习任何类型的依赖关系 [@problem_id:3160958]。

这两种[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)的差异在一个思想实验中体现得淋漓尽致：对于一个在空间中平移或旋转的信号，一个精心设计的、具有[旋转对称](@keyword=rotational_symmetry|lang=zh-CN|style=Feynman)性的卷积核能够完美地保持[等变性](@keyword=equivariance|lang=zh-CN|style=Feynman)——也就是说，对输入进行变换再送入模型，其结果和先将输入送入模型再对输出进[行变换](@keyword=row_operations|lang=zh-CN|style=Feynman)，是完全一样的，两者之差的范数几乎为零。然而，一个使用了绝对[位置编码](@keyword=positional_encodings|lang=zh-CN|style=Feynman)（即告诉模型每个像素点的绝对坐标）的注意力模型则会“困惑”。当信号被移动后，信号特征和它的绝对[位置编码](@keyword=positional_encodings|lang=zh-CN|style=Feynman)之间的关系就改变了，模型无法再保证[等变性](@keyword=equivariance|lang=zh-CN|style=Feynman)，导致其输出与预期产生显著差异 [@problem_id:3160958]。

这就像教一个孩子认识世界。我们可以教他一些普适的规则（归纳偏见），比如“物体的大小不随位置改变”，这很高效。或者，我们也可以给他一个超级大脑（[注意力机制](@keyword=attention_mechanism|lang=zh-CN|style=Feynman)），让他自己观察成千上万个例子，自己去悟出这些规则。前者有保证，但可能存在局限；后者更灵活、更强大，但也更需要数据，且没有保证。

### 从离散到连续：构建机器心智的全新思路

我们通常认为神经网络是由一层层离散的计算单元堆叠而成的。例如，一个深度[残差网络](@keyword=residual_networks|lang=zh-CN|style=Feynman)（[ResNet](@keyword=resnets|lang=zh-CN|style=Feynman)）可以看作是一系列状态的演化：$\mathbf{x}_{k+1} = \mathbf{x}_k + g_\theta(\mathbf{x}_k)$。这实际上可以被视为用一种简单的数值方法（前向欧拉法）在离散的时间步长上模拟一个连续的动力学系统 [@problem_id:3160861]。

这启发了一个革命性的想法：为什么不直接在**连续**的维度上对模型进行定义呢？这就是**神经普通[微分方程](@keyword=differential_equation|lang=zh-CN|style=Feynman)（Neural ODEs）**[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)的诞生。它不再定义离散的层，而是用一个[神经网络](@keyword=neural_networks|lang=zh-CN|style=Feynman) $f_\theta$ 来[参数化](@keyword=parametrization|lang=zh-CN|style=Feynman)状态 $\mathbf{x}$ 随“深度”（可以看作是连续的时间 $t$）变化的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)：$d\mathbf{x}/dt = f_\theta(\mathbf{x}, t)$。模型的最终输出是通过一个[数值求解器](@keyword=numerical_solvers|lang=zh-CN|style=Feynman)，从初始状态 $\mathbf{x}(0)$ 积分到某个终止时间 $\mathbf{x}(T)$ 得到的 [@problem_id:3160861]。

这种从离散到连续的转变带来了深刻的理论和实践意义。
- **稳定性**：离散的[ResNet](@keyword=resnets|lang=zh-CN|style=Feynman)块，如果步长 $h$（可以类比于层的影响力）设置不当，对于某些动态系统可能会变得不稳定，就像用粗糙的步[子模](@keyword=submodule|lang=zh-CN|style=Feynman)拟一个快速变化的物理过程一样，最终会导致结果发散 [@problem_id:3160861]。而Neural ODE可以使用自适应的求解器，根据动态的复杂程度自动调整“步长”，从而在数值上更精确、更稳定地模拟复杂变换。
- **表达能力与拓扑约束**：一个标准的Neural ODE，如果其定义的[向量场](@keyword=vector_field|lang=zh-CN|style=Feynman) $f_\theta$ 满足某些光滑性条件（利普希茨连续），那么它所描述的变换（从 $\mathbf{x}(0)$到$\mathbf{x}(T)$）是可逆的。这意味着两个不同的输入点永远不会被映射到同一个输出点。这是一种拓扑上的限制，使得它本身无法完成像分类这样需要将许多不同输入“合并”到少数几个类别输出的任务。相比之下，离散的[ResNet](@keyword=resnets|lang=zh-CN|style=Feynman)没有这个限制。这揭示了模型架构如何深刻地影响其所能学习的函数类别 [@problem_id:3160861]。

这个[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)转变，让我们不再将[深度学习](@keyword=deep_learning|lang=zh-CN|style=Feynman)模型看作一个固定的、分层的结构，而是看作一个连续演化的流场。这不仅在数学上更为优雅，也为我们处理不规则采样的[时间序列数据](@keyword=time_series_data|lang=zh-CN|style=Feynman)、学习物理系统的内在规律等问题打开了全新的大门。

### 自我监督：当数据成为自己的老师

[有监督学习](@keyword=supervised_learning|lang=zh-CN|style=Feynman)威力巨大，但它最大的瓶颈在于对海量标注数据的依赖。标注数据是昂贵且稀缺的。那么，机器能否从海量的、无标签的数据中自己学习到有用的知识呢？**[自监督学习](@keyword=self_supervised_learning|lang=zh-CN|style=Feynman)（Self-supervised Learning, SSL）**[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)为此提供了一个绝妙的答案。

其核心思想是：从数据本身创造出“伪任务”（pretext task）。我们人为地对数据进行某种变换，然后让模型去预测这个变换的属性。例如，我们可以随机旋转一张图片，然后让模型去预测这张图片被旋转了多少度（例如，0、90、180还是270度）。为了完成这个任务，模型被迫去理解图像的内容——它必须识别出物体的朝向、什么是“正”的，什么是“倒”的 [@problem_id:3160860]。

这个过程的巧妙之处在于，我们关心的并非模型在伪任务上的表现，而是它在这个过程中学到的**表示（representation）**。一个好的伪任务，会迫使模型学习到对下游真实任务（如下游的分类、检测任务）有用的通用特征。

我们可以用一个精巧的数学模型来理解这一点。假设有一个我们关心的潜在变量，比如一个物体的真实旋转角度 $\theta$。我们设计了两个伪任务：一个是预测离散化的旋转角度（旋转预测任务），另一个是预测一个与 $\theta$ 无关的拼图[排列](@keyword=permutation|lang=zh-CN|style=Feynman)（拼图任务）。通过计算可以发现，旋转预测任务所产生的标签 $Y_{\mathrm{rot}}$ 与真实角度 $\theta$ 之间保留了更多的信息（即互信息 $I(\theta; Y_{\mathrm{rot}})$ 更高），并且用它来估计 $\theta$ 的理论最小误差（[贝叶斯风险](@keyword=bayes_risk|lang=zh-CN|style=Feynman)）也更低 [@problem_id:3160860]。这精确地量化了我们的直觉：一个与下游任务“对齐”的伪任务，能够更好地保存对下游任务有用的信息。

[自监督学习](@keyword=self_supervised_learning|lang=zh-CN|style=Feynman)的[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)，让机器得以从互联网上无尽的文本、图片和视频中汲取养分，成为一个“无师自通”的学习者。

### [双下降](@keyword=double_descent|lang=zh-CN|style=Feynman)之谜：为何模型越大，有时反而越好？

经典的统计学理论告诉我们一个关于[模型复杂度](@keyword=model_complexity|lang=zh-CN|style=Feynman)的“U型”法则：模型太简单（[欠拟合](@keyword=underfitting|lang=zh-CN|style=Feynman)），误差很高；随着模型变复杂，误差下降；但如果模型过于复杂（过拟合），它会开始学习训练数据中的噪声，导致在未见过的数据上表现很差，误差再次上升。这就是著名的**偏差-方差权衡（Bias-Variance Tradeoff）**。

然而，在现代[深度学习](@keyword=deep_learning|lang=zh-CN|style=Feynman)中，人们观察到了一个令人困惑的现象：随着模型参数量不断增加，远超训练样本的数量，[测试误差](@keyword=test_error|lang=zh-CN|style=Feynman)在经历了经典的“U型”上升后，竟然会再次下降。这就是**[双下降](@keyword=double_descent|lang=zh-CN|style=Feynman)（Double Descent）**现象 [@problem_id:3160865]。这似乎与我们的传统观念背道而驰。

这个谜题的答案，指向了一个被称为**[隐式偏见](@keyword=implicit_bias|lang=zh-CN|style=Feynman)（Implicit Bias）**的深刻概念。在模型极度过参数化（参数远多于数据点）的 regime 中，能够完美拟合训练数据（即[训练误差](@keyword=training_error|lang=zh-CN|style=Feynman)为零）的解有无穷多个。那么，我们最终得到的到底是哪一个解呢？答案取决于我们的训练[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)。像[随机梯度下降](@keyword=stochastic_gradient_descent|lang=zh-CN|style=Feynman)（SGD）这样的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，在从小的初始值开始训练时，会“偏爱”某些特定的解——通常是那些具有更小范数、“更平滑”的解。

这种由[优化算法](@keyword=optimization_algorithms|lang=zh-CN|style=Feynman)带来的无形约束，就像一种隐式的[正则化](@keyword=regularization|lang=zh-CN|style=Feynman)，它在无数个“完美”解中，挑选出了一个泛化能力更好的解。因此，在过[参数化](@keyword=parametrization|lang=zh-CN|style=Feynman)的世界里，模型的泛化能力不再仅仅由其参数数量（容量）决定，而是由模型架构、[优化算法](@keyword=optimization_algorithms|lang=zh-CN|style=Feynman)和数据之间复杂的相互作用共同决定 [@problem_id:3160865]。[双下降现象](@keyword=double_descent_phenomenon|lang=zh-CN|style=Feynman)的发现，标志着我们对[机器学习泛化](@keyword=machine_learning_generalization|lang=zh-CN|style=Feynman)理论的理解进入了一个全新的、更深刻的阶段。

### 走向现实：与人类和社会共生的学习[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)

最后，让我们将目光从抽象的数学原理投向机器学习在现实世界中面临的挑战。一系列新的[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)正在涌现，它们旨在让机器学习模型更值得信赖、更具适应性、更尊重社会规范。

#### [可解释性](@keyword=interpretability|lang=zh-CN|style=Feynman)：打开“黑箱”

[深度学习](@keyword=deep_learning|lang=zh-CN|style=Feynman)模型常被诟病为“黑箱”，我们知其然，但不知其所以然。**可解释性（Interpretability）**[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)致力于解决这个问题，它也分化出两种主流思想。第一种是**事后解释（Post-hoc Explanation）**，即在训练好一个[黑箱模型](@keyword=black_box_model|lang=zh-CN|style=Feynman)后，用一些外部工具去探究它的决策依据，比如计算输入特征对输出的贡献度（特征归因）[@problem_id:3160876]。

第二种思想则更为彻底：**“白盒”设计（Interpretable by Design）**。它主张在模型设计之初就将可解释性作为核心约束。**概念瓶颈模型（Concept Bottleneck Models, CBM）**是其典范。这类模型被要求先将输入映射到一组人类可以理解的、高级的“概念”上，然后再基于这些概念做出最终预测。例如，在诊断一张[X光](@keyword=x_ray|lang=zh-CN|style=Feynman)片时，模型可能被强制要求先判断是否存在“肺部结节”、“胸腔[积液](@keyword=effusion|lang=zh-CN|style=Feynman)”等概念，然后再给出最终的诊断结果。这种设计不仅让模型的决策过程变得透明，还允许领域专家通过干预概念值来与模型交互、纠正模型的错误，这在事后解释方法中是难以实现的 [@problem_id:3160876]。

#### 持续学习：如何不遗忘？

人类可以不断学习新知识而不会轻易忘记旧的技能。但标准的[神经网络](@keyword=neural_networks|lang=zh-CN|style=Feynman)在学习新任务时，往往会严重损害在旧任务上的表现，这种现象被称为**[灾难性遗忘](@keyword=catastrophic_forgetting|lang=zh-CN|style=Feynman)（Catastrophic Forgetting）**。

**持续学习（Continual Learning）**[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)旨在让模型具备“终身学习”的能力。从数学上看，[灾难性遗忘](@keyword=catastrophic_forgetting|lang=zh-CN|style=Feynman)发生的原因在于，新任务的梯度更新，可能会改变那些对旧任务至关重要的参数。这些“重要参数”的方向，正是旧任务[损失函数](@keyword=loss_functions|lang=zh-CN|style=Feynman)曲率（由[Hessian矩阵](@keyword=hessian_matrix|lang=zh-CN|style=Feynman) $H_i$ 描述）非常大的方向。在这些方向上哪怕做出微小的改动，也会导致旧任务的损失 $L_i$ 急剧增加（变化量 $\Delta L_i \approx \frac{1}{2} \Delta \theta^T H_i \Delta \theta$）[@problem_id:3160930]。

为了解决这个问题，研究者们提出了多种策略。**排演（Rehearsal）**策略就像人类复习功课，模型在学习新任务的同时，会用一个缓冲区存储的旧任务样本进行“回放”练习。而**参数隔离（Parameter Isolation）**策略则更为直接，它会识别并“冻结”那些对旧任务重要的参数，或者将新任务的更新投影到一个与重要参数方向正交的“安全”子空间中，从而避免干扰 [@problem_id:3160930]。

#### 联邦与隐私：在数据孤岛上构建智慧

在许多现实场景中，数据因为隐私、安全或商业原因，被分散在无数的“数据孤岛”上（例如，我们每个人的手机）。**[联邦学习](@keyword=federated_learning|lang=zh-CN|style=Feynman)（Federated Learning）**[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)应运而生，它旨在不移动原始数据的情况下，协同多个数据持有方共同训练一个模型。其基本流程是：服务器将模型分发给各个客户端，客户端在本地数据上进行训练，然后只将模型的更新（而非数据本身）发送回服务器进行聚合 [@problem_id:3160939]。

然而，仅仅不传输原始数据并不足以保证隐私，模型的更新本身也可能泄露个人信息。因此，[联邦学习](@keyword=federated_learning|lang=zh-CN|style=Feynman)常常与**[差分隐私](@keyword=differential_privacy|lang=zh-CN|style=Feynman)（Differential Privacy, DP）**相结合。DP提供了一种严格的、可量化的隐私保护承诺。在[联邦学习](@keyword=federated_learning|lang=zh-CN|style=Feynman)中，这通常通过两种手段实现：在客户端上传更新之前，对其范数进行**裁剪（Clipping）**，以限制单个用户的影响力；在服务器聚合更新之后，注入经过精心校准的**高斯噪声（Gaussian Noise）**，以模糊个体贡献 [@problem_id:3160939]。

这引入了一系列复杂的权衡。增加噪声可以提供更强的隐私保护（更小的[隐私预算](@keyword=privacy_budget|lang=zh-CN|style=Feynman) $\varepsilon$），但会降低模型的精度。减少每轮参与的客户端比例，可以通过“[隐私放大](@keyword=privacy_amplification|lang=zh-CN|style=Feynman)”效应增强隐私，但又会因为梯度的方差增大而损害训练效果。有趣的是，DP的这些操作（裁剪和加噪）有时也像一种正则化手段，在某些情况下可以防止[模型过拟合](@keyword=model_overfitting|lang=zh-CN|style=Feynman)，甚至提高其在测试集上的泛化能力 [@problem_id:3160939]。

从区分猫狗，到在保护个人隐私的同时协同全球智慧，机器学习的[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)之旅远未结束。每一个[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)，都是我们对“学习”这一古老概念的一次全新探索，它们共同谱写着人工智能时代最激动人心的乐章。