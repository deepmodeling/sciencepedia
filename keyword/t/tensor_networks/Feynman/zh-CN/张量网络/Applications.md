## 应用与跨学科联系

现在，你可能会想，这一整套[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)——这些由相互连接的[张量](@keyword=tensor|lang=zh-CN|style=Feynman)组成的优雅图示——对于研究抽象[量子自旋链](@keyword=quantum_spin_chain|lang=zh-CN|style=Feynman)的物理学家来说，是一个非常聪明的工具。你说得对。故事就是从那里开始的。但[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)的故事是科学中那些美妙的实例之一，一个为解决特定深层问题而生的想法，最终被证明具有惊人的普适性。就好像在试图破译一个神秘的句子时，我们无意中发现了一种复杂性本身的基本语言。

在本章中，我们将从量子物理的发源地出发，去看看这种语言如何被用来重新表述和解决化学、计算机科学乃至人工智能等不同领域的问题。这些应用不仅仅是类比；它们是深层次的结构等价，揭示了科学领域间非凡的统一性。

### 发源地：[量子多体物理](@keyword=quantum_many_body_physics|lang=zh-CN|style=Feynman)

[量子多体物理](@keyword=quantum_many_body_physics|lang=zh-CN|style=Feynman)学的主要挑战是驯服指数级复杂性这头猛兽。一个包含 $N$ 个粒子的系统的希尔伯特空间随 $N$ 指数增长，使得除了极小的系统外，蛮力描述都变得不可能。[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)的成功之处在于它甚至不去尝试描述整个空间。相反，它提供了一种语言来描述那个自然界实际栖息的、物理上相关的微小角落。这种相关性是由[量子纠缠](@keyword=quantum_entanglement|lang=zh-CN|style=Feynman)的结构决定的。

最简单也最成功的[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)是[矩阵乘积态 (MPS)](@keyword=matrix_product_state_(mps)|lang=zh-CN|style=Feynman)，它是[密度矩阵重整化群](@keyword=density_matrix_renormalization_group|lang=zh-CN|style=Feynman) (DMRG) 方法的引擎。对于具有“有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)”[能谱](@keyword=energy_spectrum|lang=zh-CN|style=Feynman)（意味着产生一个激发需要有限的能量）的[一维量子系统](@keyword=one_dimensional_quantum_systems|lang=zh-CN|style=Feynman)，系统一半与另一半之间的纠缠出人意料地有限——它遵循“[面积定律](@keyword=area_law|lang=zh-CN|style=Feynman)”，即它与边界的大小（在一维中只是一个点）成比例，而不是与体积成比例。MPS 的内在构造正是为了捕捉这种局域纠缠结构。这就是为什么 DMRG 能够以惊人的精度找到一维模型的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)，通过只关注具有物理上现实的纠缠的态来规避指数级的噩梦 [@problem_id:2454742]。这种能力在[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)中找到了关键应用，它能够捕捉描述拉伸分子时困扰传统方法的“强静态关联”，为旧的近似方法提供了可系统性改进的替代方案 [@problem_id:2453965]。

但对于那些不是简单一维链的系统呢？或者那些处于“[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)”、纠缠是长程且不遵循简单[面积定律](@keyword=area_law|lang=zh-CN|style=Feynman)的系统呢？在这里，MPS 的固定拓扑不再是最佳选择。[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)框架的美妙之处在于其灵活性。我们可以设计不同的[网络架构](@keyword=network_architecture|lang=zh-CN|style=Feynman)来匹配不同的纠缠模式。
-   对于具有分支、非线性几何形状的分子，[树张量网络](@keyword=tree_tensor_networks|lang=zh-CN|style=Feynman)态 (TTNS) 可能远为高效。通过将[张量](@keyword=tensor|lang=zh-CN|style=Feynman)[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成一棵能反映分子结构的树，我们可以比将其强行置于一维线上创建出更忠实、更紧凑的[量子态表示](@keyword=quantum_state_representation|lang=zh-CN|style=Feynman) [@problem_id:2929052]。
-   对于表现出[分形](@keyword=fractal|lang=zh-CN|style=Feynman)般自相似性的临界系统，多尺度纠缠重整化拟设 (MERA) 提供了一个优美的解决方案。其分层、等级的结构是专门为处理标度不变性而设计的。在 MERA 中，计算像长程关联函数这样的物理性质变成了一个系统地将算符“推”过网络各层的过程，每一步都有效地放大到更粗糙的尺度 [@problem_id:142109]。

该框架甚至超越了对零温[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的探索。对于有限温度下的系统，[量子涨落](@keyword=quantum_fluctuations|lang=zh-CN|style=Feynman)和[热涨落](@keyword=thermal_fluctuations|lang=zh-CN|style=Feynman)混合在一起，又该如何处理？此类系统由[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)或[密度算符](@keyword=density_operator|lang=zh-CN|style=Feynman)描述，而非纯[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)。**纯化**这一绝妙技巧使我们能够处理这种情况。通过引入一个虚构的“辅助”系统——可以看作一个孪生宇宙——我们可以将我们物理系统的混乱混合态表示为这个组合系统中一个纯净、纠缠的纯态的一半。然后，我们可以通过从一个最大[纠缠态](@keyword=entangled_state|lang=zh-CN|style=Feynman)（代表无限温度）开始，并用算符 $\exp(-\beta H/2)$ 进行[虚时演化](@keyword=imaginary_time_evolution|lang=zh-CN|style=Feynman)，来获得所需温度 $\beta$ 下的[热态](@keyword=thermal_states|lang=zh-CN|style=Feynman) [@problem_id:2812515]。由此浮现出一个深刻的联系：这个[纯化态](@keyword=purified_states|lang=zh-CN|style=Feynman)的范数直接与系统的[配分函数](@keyword=sum_over_states_2|lang=zh-CN|style=Feynman)有关，后者是[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的核心对象。

为了使这些方法真正实用，我们还必须教会我们的[张量](@keyword=tensor|lang=zh-CN|style=Feynman)关于自然界的[基本对称性](@keyword=fundamental_symmetries|lang=zh-CN|style=Feynman)。如果一个系统守恒总粒子数或[总自旋](@keyword=total_spin|lang=zh-CN|style=Feynman)，它的哈密顿量就具有对称性。通过将这种对称性直接构建到我们的[张量](@keyword=tensor|lang=zh-CN|style=Feynman)中——使它们成为块稀疏的，只连接具有正确量子数的态——我们可以显著降低[计算成本](@keyword=computational_cost|lang=zh-CN|style=Feynman)。这就像在开始搭建之前，先把一大堆乐高积木按颜色分类；你只需要处理相关的子集 [@problem_id:2812491]。此外，对于电子和其他[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)系统，还必须教会[张量](@keyword=tensor|lang=zh-CN|style=Feynman)[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)。这是通过在[张量](@keyword=tensor|lang=zh-CN|style=Feynman)指标上编码一个“[费米子宇称](@keyword=fermion_parity|lang=zh-CN|style=Feynman)”来完成的，确保每当网络中两条[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)路径交换时，都会出现正确的负号，正如自然所要求的那样 [@problem_id:3018455]。这显示了该框架吸收量子力学最深层规则的强大能力。

### 通往抽象的桥梁：计算机科学与逻辑学

从量子物理到逻辑谜题的飞跃似乎很大，但[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)轻松地架起了这座桥梁。思考一下我们熟悉的数独游戏。其核心是一个[约束满足问题](@keyword=constraint_satisfaction_problems|lang=zh-CN|style=Feynman)。你有一个变量网格（空格），每个变量都有一组可能的值，以及它们必须遵守的规则列表。

我们可以将一个数独谜题直接翻译成[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)的语言。每一条局部规则——“这两个单元格必须不同”，“这个单元格必须是4”——都变成一个小[张量](@keyword=tensor|lang=zh-CN|style=Feynman)，其元素对于允许的赋值为1，对于禁止的赋值为0。整个谜题变成了一个由这些简单的约束[张量](@keyword=tensor|lang=zh-CN|style=Feynman)构成的大型网络。缩并这个网络这一行为，即根据图的连接对所有共享变量求和，会产生一个单一的数字。这个数字并非任意；它是该谜题有效解的总数 [@problem_id:2445481]。无解的谜题会产生0的结果。

这种联系比单纯的谜题要深刻得多。它触及了计算复杂性理论的基础。某些计算问题被认为是“困难的”。其中最著名之一是计算矩阵的**积和式** (permanent)，它是[行列式](@keyword=determinant|lang=zh-CN|style=Feynman)一个鲜为人知的表亲。虽然[行列式](@keyword=determinant|lang=zh-CN|style=Feynman)可以被高效计算，但计算积和式是一个所谓的 `#P`-难问题，据信需要随矩阵大小指数增长的资源。

任何这样的计数问题都可以表示为一次[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)缩并。缩并的计算成本主要由 $\chi^{tw}$ 决定，其中 $\chi$ 是最大键维数，而 $tw$ 是网络图的“[树宽](@keyword=treewidth|lang=zh-CN|style=Feynman)”。这意味着一个根本性的权衡。如果我们被告知一个问题是指数级困难的，那么没有任何神奇的[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)可以使它变得容易。如果一个聪明的新网络设计降低了[树宽](@keyword=treewidth|lang=zh-CN|style=Feynman) $tw$，它的键维数 $\chi$ *必须*[指数增长](@keyword=exponential_growth|lang=zh-CN|style=Feynman)来补偿，从而保持总体复杂性不变。这表明，[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)不仅仅是一种模拟工具；它们是一种[计算模型](@keyword=models_of_computation|lang=zh-CN|style=Feynman)，其结构和成本与其所代表问题的内在复杂性紧密相连 [@problem_id:1461326]。

### 新前沿：机器学习与[数据科学](@keyword=data_science|lang=zh-CN|style=Feynman)

[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)故事中最新、或许也是最激动人心的篇章是它们进入了机器学习和人工智能领域。在这里，对应关系同样不是类比，而是数学上的恒等。

对序列数据——如语音、[金融时间序列](@keyword=financial_time_series|lang=zh-CN|style=Feynman)或DNA序列——进行建模的一个基石是[隐马尔可夫模型](@keyword=hidden_markov_models|lang=zh-CN|style=Feynman) (HMM)。HMM 假设存在一个未被观测到的隐藏“状态”序列，它生成了我们所看到的数据。一个基本任务是根据观测数据推断这些[隐藏状态](@keyword=hidden_state|lang=zh-CN|style=Feynman)的概率。

事实证明，用于求解 HMM 的[前向-后向算法](@keyword=forward_backward_algorithm|lang=zh-CN|style=Feynman)的数学结构与[矩阵乘积态](@keyword=matrix_product_states|lang=zh-CN|style=Feynman)的缩并是相同的。HMM 的转移概率构成一个[矩阵乘积算符](@keyword=matrix_product_operator|lang=zh-CN|style=Feynman) (MPO)，而[隐藏状态](@keyword=hidden_state|lang=zh-CN|style=Feynman)上的[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)是一个 MPS。物理学家的 MPS 的“键维数”找到了新的含义，即统计模型的“记忆”或信息容量。在物理学中为 DMRG 截断键维数而开发的技术，在创建压缩的、近似的统计模型中有着直接的类比，使我们能够处理那些拥有巨大[状态空间](@keyword=state_space_2|lang=zh-CN|style=Feynman)、否则将难以处理的 HMM [@problem_id:2385337]。

这一发现打开了[闸门](@keyword=sluice_gate|lang=zh-CN|style=Feynman)。源于量子世界的[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)语言，为设计新的机器学习架构提供了一个系统性的、有物理动机的、计算能力强大的框架。目前正在探索使用二维[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman) (PEPS) 进行图像分析和分类，以及使用网络作为强大的生成模型，能够学习和从复杂的数据分布中采样的想法。

从[量子纠缠](@keyword=quantum_entanglement|lang=zh-CN|style=Feynman)最深刻的规律，到数独谜题的逻辑，再到我们数据中的模式，[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)为描述和驾驭复杂性提供了一种统一的图形化语言。这段旅程远未结束，但已经清楚的是，这是科学史上最美丽、最出人意料的成功故事之一。