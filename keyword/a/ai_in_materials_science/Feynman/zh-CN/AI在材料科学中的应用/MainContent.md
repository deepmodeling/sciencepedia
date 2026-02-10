## 引言
在历史上，探索具有非凡性能的新材料一直是一个依赖直觉、试错的缓慢过程。如今，人工智能的融合正在改变这一[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)，有望极大地加快发现的步伐。但是，一个只理解数字和逻辑的机器，如何能掌握支配原子世界的复杂物理和化学规律？这个问题代表了计算机科学与物理科学[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)领域的一个关键知识空白。本文将描绘从抽象数据到实际发现的完整历程，全面概述我们如何教导人工智能去理解、预测乃至创造新材料。

第一部分“原理与机制”将阐释基础概念。我们将探讨[原子结构](@keyword=atomic_structure|lang=zh-CN|style=Feynman)如何被转化为数学语言，以及像[图神经网络](@keyword=graph_neural_networks|lang=zh-CN|style=Feynman)这样的机器学习架构如何从这些数据中学习预测复杂的[材料属性](@keyword=material_properties|lang=zh-CN|style=Feynman)。我们还将讨论通过强制施加物理定律和量化[模型不确定性](@keyword=model_uncertainty|lang=zh-CN|style=Feynman)来建立模型信任度的关键方面。

随后，“应用与跨学科联系”部分将展示这些原理的实际应用。我们将看到人工智能驱动的策略如何指导实验探索，如何通过保护隐私的技术实现全球合作，并最终汇聚成“自驱动实验室”这一革命性概念——一个用于[材料发现](@keyword=materials_discovery|lang=zh-CN|style=Feynman)的自主平台。读完本文后，读者将对驱动[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)新时代的方法有清晰的理解。

## 原理与机制

那么，这一切是如何运作的呢？我们如何将材料那纷繁而优美的复杂性——晶体中混乱的原子、缠结的聚合物链——教给机器去理解、预测其行为，甚至构想出前所未见的新材料？这不是魔法，但类似于教一门新语言。我们必须首先为原子世界创造一套字母表和语法，然后构建一台能够阅读这种语言的机器，并最终确保这台机器在阅读时能够理解、保持谦逊，并有能力解释其推理过程。

### 物质的字母表：将原子转化为数字

在人工智能学习之前，它需要能够处理的数据。你不能直接把一块晶体喂给计算机。你必须首先将其结构转化为计算的原生语言：数字。将材料看作一个**图**（graph）是最自然的方式，即一个由边连接的节点的集合。在这个视图中，原子是节点，它们之间的[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)是边。这是一个极其简洁而强大的起点。

但是，计算机不理解图的绘制形式，它理解的是矩阵——即数字的数组。因此，我们将图转化为两个关键矩阵。第一个是**[邻接矩阵](@keyword=adjacency_matrix|lang=zh-CN|style=Feynman)**（Adjacency Matrix）$A$。它是一个简单的记录，告诉我们哪些原子相互成键。如果原子 $i$ 与原子 $j$ 成键，则[矩阵元素](@keyword=matrix_elements|lang=zh-CN|style=Feynman) $A_{ij}$ 为 1；否则为 0。第二个是**度矩阵**（Degree Matrix）$D$，这是一个对角矩阵，其中每个对角元素 $D_{ii}$ 简单地记录了原子 $i$ 拥有的[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)数量。

利用这两个简单的矩阵，我们可以构建该领域中最重要的对象之一：**[图拉普拉斯算子](@keyword=graph_laplacian|lang=zh-CN|style=Feynman)**（Graph Laplacian），定义为 $L = D - A$。这个矩阵看似抽象，但它是解锁材料几何结构和连通性的关键。它编码了信息——或称“信号”——如何在原[子网](@keyword=subnets|lang=zh-CN|style=Feynman)络中传播。

事实上，[拉普拉斯算子](@keyword=divergence_of_the_gradient|lang=zh-CN|style=Feynman)是如此基础，以至于其基本性质揭示了关于材料结构的深层真理。对于任何连通的材料（即没有分离、漂浮的碎片），其拉普拉斯矩阵恰好有一个等于零的[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)。与此零[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)对应的[特征向量](@keyword=eigenvector|lang=zh-CN|style=Feynman)并非随机；它就是一个所有元素为1的向量，再乘以一个常数[@problem_id:90098]。这看似只是一个数学上的奇特现象，但它蕴含着深刻的意义：在整个连通结构中唯一保持不变的东西就是结构*本身*。这个[特征向量](@keyword=eigenvector|lang=zh-CN|style=Feynman)充当了图的统一性的数学签名。

对于更复杂的人工智能模型，我们通常使用一个稍作修改的版本，称为**对称[归一化](@keyword=normalization|lang=zh-CN|style=Feynman)[图拉普拉斯算子](@keyword=graph_laplacian|lang=zh-CN|style=Feynman)**（symmetrically normalized graph Laplacian），$L_{\text{norm}} = I - D^{-1/2} A D^{-1/2}$，其中 $I$ 是[单位矩阵](@keyword=identity_matrix|lang=zh-CN|style=Feynman)。这个归一化过程有点像是在调整一个事实，即某些原子比其他原子更“受欢迎”（拥有更多的键），从而确保网络在更平等的地位上处理每次相互作用。对于一个简单的、假设有四个原子的方形分子，这个优雅的矩阵能够在一个简洁的 $4 \times 4$ 数字数组中捕捉分子的完整拓扑结构，为人工智能的处理做好了准备[@problem_id:90228]。这种从物理对象到结构化数值表示的转化，是整个事业中第一步，或许也是最关键的一步。

### 描述原子邻域：不变性指纹

仅仅知道谁与谁相连是不够的。金刚石中的碳原子以完美的四面体结构与另外四个碳原子成键。[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)[片层](@keyword=lamellae|lang=zh-CN|style=Feynman)中的碳原子则在平面上与另外三个碳原子成键。它们的连通性不同，但更重要的是，它们的局域几何构型根本不同，这导致了它们截然不同的性质。我们需要捕捉这种局域环境。

在这里我们面临一个关键挑战：我们的描述必须遵循物理定律。如果我们在空间中旋转一个材料，它仍然是*同一个*材料，其性质不会改变。同样，如果我们有两个相同的邻近原子，交换它们的标签也不应改变我们的描述。我们的数学表示必须在旋转、平移和相同邻居的[置换](@keyword=permutation|lang=zh-CN|style=Feynman)下保持**[不变性](@keyword=invariance|lang=zh-CN|style=Feynman)**（invariant）。

创建这样一个不变性“指纹”的一个直观方法是观察几何结构。对于一个原子，我们可以计算其所有邻居形成的键角。对于一个完美的四面体环境（如金刚石），所有键角约为 $109.5^\circ$。对于一个平面四方环境，键角则为 $90^{\circ}$ 和 $180^{\circ}$。一个简单而强大的描述符是**键角方差**（bond-angle variance）[@problem_id:90104]。键角均匀的环境其方差为零，而扭曲或复杂的环境则方差较大。这个本身就具有[旋转不变性](@keyword=rotational_invariance|lang=zh-CN|style=Feynman)的单一数字，已经能告诉人工智能关于局域形状的重要信息。

为了构建一个更完整、更鲁棒的指纹，我们可以转向更强大的技术，如**原子位置平滑重叠（SOAP）**描述符[@problem_id:301452]。其思想非常优雅。想象每个邻近原子都贡献一团以其位置为中心的密度“云”。局域环境就是所有这些云的总和。现在，为了使这个描述具有[旋转不变性](@keyword=rotational_invariance|lang=zh-CN|style=Feynman)，我们借鉴了物理学和信号处理中的一个技巧。就像音乐声可以分解为其基频（傅里叶级数）一样，我们可以使用称为[球谐函数](@keyword=y_l^m_functions|lang=zh-CN|style=Feynman)的函数将这个三维密度云分解为一组基本的三维形状。每个基本形状的“功率”或强度构成一个向量，即SOAP[功率谱](@keyword=power_spectrum|lang=zh-CN|style=Feynman)。这个谱是该环境的一个丰富、详细的指纹，它在旋转时保持不变，为人工智能提供了关于每个原子局域世界的高度[信息量](@keyword=surprisal|lang=zh-CN|style=Feynman)和物理上合理的描述。

甚至还有其他的哲学思想。**[核方法](@keyword=kernel_methods|lang=zh-CN|style=Feynman)**（kernel methods）不创建显式的[特征向量](@keyword=eigenvector|lang=zh-CN|style=Feynman)，而是定义一个“相似度函数”，直接计算两个原子环境的相似程度。其技巧在于设计这个核函数，使其自然地满足所需的物理对称性，例如，通过在所有可能的旋转和[置换](@keyword=permutation|lang=zh-CN|style=Feynman)上进行数学平均[@problem_id:90120]。

### 进行学习的网络：从图到性质

一旦我们有了我们的语言——原子及其环境的数值表示——我们就可以构建学习机器。完成这项任务最成功的架构是**[图神经网络](@keyword=graph_neural_networks|lang=zh-CN|style=Feynman)**（Graph Neural Network, GNN）。GNN背后的核心思想是**[消息传递](@keyword=message_passing|lang=zh-CN|style=Feynman)**（message passing）。可以把它想象成原子之间在进行对话。

在这个过程的每一步，每个原子（节点）做两件事：
1.  它从所有直接邻居那里收集“消息”。消息通常基于邻居的当前状态和连接它们的[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)的性质。
2.  它通过聚合这些消息，并将其与自身先前的状态相结合，来更新自己的状态。

这个过程会重复几次。在第一轮中，一个原子只了解其直接邻居。在第二轮中，它了解其邻居的邻居，以此类推。几轮过后，每个原子的状态向量都包含了对其一定距离内局域环境的丰富、多层次的描述。决定这些消息如何聚合的数学算子通常直接源于我们之前遇到的图拉普拉斯算子[@problem_id:90228]。最后，所有的原子状态被结合起来，对整个材料的性质做出单一的预测。

但是，对于比简单的原子-键对更复杂的结构该怎么办？在许多材料中，诸如分子中的环或多面体的三角形面等基元，才是决定性质的基本构筑单元。标准的GNN只看到键（一维连接）和原子（零维点）。为了捕捉这些关键的高阶结构，研究人员将GNN推广为**单纯形神经网络**（Simplicial Neural Networks, SNNs）[@problem_id:90171]。这些网络在一个**[单纯复形](@keyword=simplicial_complexes|lang=zh-CN|style=Feynman)**（simplicial complex）上运行，这是一个不仅包含节点和边，还明确包括三角形（2-单纯形）、四面体（3-单纯形）等的数学对象。在这个框架中，[消息传递](@keyword=message_passing|lang=zh-CN|style=Feynman)可以发生在键之间，或者键与它们所属的三角形之间。支配这种扩展通信的算子是**[霍奇拉普拉斯算子](@keyword=hodge_laplacian|lang=zh-CN|style=Feynman)**（Hodge Laplacian），它是[图拉普拉斯算子](@keyword=graph_laplacian|lang=zh-CN|style=Feynman)的强大推广，使人工智能能够对这些至关重要的[多体相互作用](@keyword=many_body_interaction|lang=zh-CN|style=Feynman)进行推理。

### 构建可信赖的人工智能：物理、谦逊与洞察力

一个强大的模型不一定是一个有用的模型。要让人工智能成为科学发现中真正的伙伴，它必须可靠、可信赖且富有洞察力。这要求我们为其内置最后三个关键要素。

首先，人工智能必须尊重**物理定律**。一个幼稚的模型可能会预测出一种[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)上不稳定的材料，使其在现实世界中毫无用处。我们可以通过将物理定律构建到模型的训练目标，即**损失函数**（loss function）中来强制执行。例如，[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)的一个基本原理是，稳定材料的自由能表面必须是局部凸的。我们可以在[损失函数](@keyword=loss_functions|lang=zh-CN|style=Feynman)中增加一个惩罚项，每当模型预测的能量表面违反此[凸性](@keyword=convexity|lang=zh-CN|style=Feynman)条件时就对其进行惩罚[@problem_id:90246]。这就像给了人工智能一本物理教科书，并告诉它：“我不管你对数据的拟合有多好，你的答案*必须*在物理上是合理的。”

其次，人工智能必须有**谦逊**感。在一个有限的数据集上训练得过于激进的模型可能会陷入**[过拟合](@keyword=overfitting|lang=zh-CN|style=Feynman)**（overfitting）的陷阱：它记住了训练数据，包括其中的[随机噪声](@keyword=stochastic_noise|lang=zh-CN|style=Feynman)，从而失去了对新的、未见过样本的泛化能力。这就是经典的**偏差-方差权衡**（bias-variance tradeoff）。过于简单的模型会“有偏”（biased），无法捕捉潜在趋势；而过于复杂的模型则“方差”高，容易被数据中的每一个微小噪声点所干扰。我们使用称为**[正则化](@keyword=regularization|lang=zh-CN|style=Feynman)**（regularization）的技术来找到最佳[平衡点](@keyword=equilibrium_points|lang=zh-CN|style=Feynman)。例如，**[早停](@keyword=early_stopping|lang=zh-CN|style=Feynman)**（Early stopping）正如其名：我们监控模型在一个独立的[验证集](@keyword=validation_set|lang=zh-CN|style=Feynman)上的表现，当表现开始下降时就停止训练，从而将模型从[过拟合](@keyword=overfitting|lang=zh-CN|style=Feynman)的边缘[拉回](@keyword=pullback|lang=zh-CN|style=Feynman)来[@problem_id:2479745]。另一种方法，**[权重衰减](@keyword=weight_decay|lang=zh-CN|style=Feynman)**（weight decay），对大的参数值施加惩罚，从而有效地保持模型更简单。这些方法对于产生一个具有泛化能力和鲁棒性的模型至关重要。

此外，一个没有[误差棒](@keyword=error_bars|lang=zh-CN|style=Feynman)的科学预测是不完整的。我们需要知道：模型对其预测有多大的信心？像**蒙特卡洛（MC）丢弃**（Monte Carlo (MC) dropout）这样的技术提供了一种巧妙的方法来估计这种**预测不确定性**（predictive uncertainty）[@problem_id:90073]。在预测时，我们将同一个输入多次通过网络，每次都随机“丢弃”（忽略）不同的[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)。这会产生一个输出分布。该分布的离散程度为我们提供了[模型不确定性](@keyword=model_uncertainty|lang=zh-CN|style=Feynman)（**认知不确定性**，epistemic uncertainty）的度量。如果预测结果分散，说明模型告诉我们它正处于一个不熟悉的领域。模型也可以被训练来预测数据本身的内在噪声（**[偶然不确定性](@keyword=aleatory_uncertainty|lang=zh-CN|style=Feynman)**，aleatoric uncertainty）。以这种方式分解不确定性对于指导未来的实验至关重要。

最后，如果一个人工智能模型预测出一种革命性的新材料，科学家会问的第一个问题是：*为什么*？是什么样的原子和结构的特定组合赋予了它这种惊人的性质？回答这个问题需要通过**[可解释人工智能](@keyword=explainable_ai|lang=zh-CN|style=Feynman)（XAI）**来打开“黑箱”。基于合作[博弈论](@keyword=game_theory|lang=zh-CN|style=Feynman)的**[沙普利值](@keyword=shapley_values|lang=zh-CN|style=Feynman)**（Shapley values）提供了一种严谨的方法来做到这一点[@problem_id:2837963]。其思想是将每个输入特征（例如，“含有锂”、“平均[键长](@keyword=bond_length|lang=zh-CN|style=Feynman)为2.1 Å”）视为一场游戏中的玩家，游戏的目标是产生最终的预测。[沙普利值](@keyword=shapley_values|lang=zh-CN|style=Feynman)为在玩家之间分配“收益”（即预测结果）提供了一种独特而公平的方式，准确地告诉我们每个特征贡献了多少。这将人工智能从一个单纯的预测引擎转变为一个能够帮助我们建立新的科学理解和直觉的工具。