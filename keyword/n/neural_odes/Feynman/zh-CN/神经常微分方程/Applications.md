## 应用与跨学科联系

在领略了[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)优雅的力学原理之后，我们现在来到了探索中最激动人心的部分：我们能用它们来*做什么*？如果说上一章是关于理解一种新型强大科学仪器的设计，那么这一章就是将该仪器指向宇宙，看看我们能发现什么。我们将看到，[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)不仅仅是[深度学习](@keyword=deep_learning|lang=zh-CN|style=Feynman)中的一个 clever trick；它们代表了数据驱动建模与第一性原理科学的深刻融合，在从生物学到物理学的各个领域开辟了新的前沿。

### 从观察中学习运动定律

从本质上讲，大部分科学都是一场“系统辨识”的游戏。我们观察一个系统——一颗围绕恒星运行的行星、一个在烧杯中嘶嘶作响的[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)、一个在培养皿中生长的细胞群——然后我们试图推断出支配其行为的 underlying rules，即“运动定律”。传统上，这涉及到基于理论提出一个数学模型，然后将其参数与数据进行拟合。但如果系统过于复杂，我们甚至不知道这些规则应该采取何种数学形式呢？

这就是[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)首次展示其威力的地方。想象一下，你是一名系统生物学家，正在研究一种导致酵母细胞产生[荧光蛋白](@keyword=fluorescent_proteins|lang=zh-CN|style=Feynman)的合成[基因线路](@keyword=gene_circuits|lang=zh-CN|style=Feynman)。你可以测量蛋白质随时间变化的浓度，但生产、降解和调控的复杂网络使得写出其变化率的精确方程 $\frac{dP}{dt} = F(P)$ 几乎是不可能的。

与其猜测 $F(P)$ 的形式，我们可以简单地告诉[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)：“帮我学会它。”我们假设动力学由 $\frac{dP}{dt} = NN_{\theta}(P)$ 控制，然后我们训练[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络 $NN_{\theta}$，直到它产生的轨迹与我们的实验数据相匹配。训练结束后，[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络不会直接给我们[蛋白质浓度](@keyword=protein_concentration|lang=zh-CN|style=Feynman) $P(t)$。相反，它成为了未知生物学定律本身的一个具体、可计算的表示。训练好的网络*就是*我们对函数 $F(P)$ 的近似，一个学到的向量场，它告诉我们对于任何给定的[蛋白质浓度](@keyword=protein_concentration|lang=zh-CN|style=Feynman)，该浓度将会以怎样的[瞬时速率](@keyword=instantaneous_rate|lang=zh-CN|style=Feynman)变化 [@problem_id:1453777]。我们实际上是利用数据发现了系统基本规则手册的一部分。

### 不间断的时间流

传统的离散时间模型，如[循环神经网络](@keyword=recurrent_neural_networks|lang=zh-CN|style=Feynman)（RNN），以一系列离散的步骤思考世界：第1步、第2步、第3步。但自然界并非按部就班地运行。疾病的进展、森林的生长、河流的流动——这些都是连续的过程。[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)正是建立在同样的连续性原则之上。

这不仅仅是一个哲学观点；它具有深刻的实际优势。考虑通过跟踪患者的[生物标志物](@keyword=biomarkers|lang=zh-CN|style=Feynman)来模拟慢性病的进展。医生就诊的时间间隔是不规则的——一个月，然后三个月，然后两周。离散模型会遇到困难，被迫要么丢弃数据，要么对步骤之间的时间做出尴尬的假设。然而，[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)以极其优雅的方式处理了这个问题。因为它定义了一条连续的轨迹，所以可以在任何时间点进行查询，无缝地匹配真实世界测量的任意时间戳 [@problem_id:1453819]。

这不仅使我们能够处理不规则数据，还能让我们自信地进行插值。如果我们有一个关于[细菌生长](@keyword=bacterial_growth|lang=zh-CN|style=Feynman)的[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)模型，该模型是基于每隔几小时的测量数据训练的，那么我们可以求解学到的[微分方程](@keyword=differential_equation|lang=zh-CN|style=Feynman)，从而得到对*任何*中间分钟或秒的人口大小的有意义的预测 [@problem_id:1453829]。该模型提供了系统演化的一个完整的、连续的故事，而不仅仅是一系列离散快照的幻灯片。

### 混合建模：站在巨人的肩膀上

虽然从零开始学习动态令人印象深刻，但这通常是低效的。我们常常对系统*某些*部分的物理学有非常确切的了解。火箭的轨迹受到众所周知[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)和推力定律的支配，但大气阻力可能是一个关于速度和高度的复杂、不可预测的函数。为什么强迫[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络去重新学习[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)呢？

这引出了**[混合模型](@keyword=mixture_models|lang=zh-CN|style=Feynman)**的强大思想，即我们将已知与未知相结合。我们可以写下一个[微分方程](@keyword=differential_equation|lang=zh-CN|style=Feynman)系统，其中一些项是我们教科书中熟悉的方程，而另一些则是[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络，任务是学习那些 messy、难以建模的部分。

想象一下模拟一个用于培养微生物的[生物反应器](@keyword=bioreactors|lang=zh-CN|style=Feynman)。我们确切地知道，随着我们泵入营养物质，培养基的体积如何变化；这只是简单的算术，$\frac{dV}{dt} = F$。我们对营养物浓度如何因细胞消耗和进料补充而变化也有很好的把握。真正复杂的部分是生物生长速率 $\mu$，它[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)地依赖于可用的底物。在混合[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)中，我们可以硬编码体积和底物稀释的已知物理学，并使用[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络仅学习生长函数 $\mu(S) = NN_{\theta}(S)$ [@problem_id:1453813]。这种方法将[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络的学习能力精确地集中在最需要的地方，从而产生既更准确又需要更少数据的模型。

### 教会[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络物理学

一个[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络本身是一个通用逼近器，但它是一个极其天真的逼近器。它没有关于质量守恒或[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)等基本物理原理的 innate 概念。如果我们用一个“天真”的[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)来训练一个应该遵循此类 법칙的系统，我们只能希望它能从数据中学会这个约束。但有更好的方法：我们可以将物理定律直接构建到模型本身中。

主要有两种方法可以做到这一点：通过架构和通过训练。

**1. 通过设计施加约束（架构）：** 这个领域最 beautiful 的方面之一是能够设计模型的结构，使其*无法*违反物理定律。

考虑一个化学物质相互转化的代谢网络。[质量守恒定律](@keyword=law_of_conservation_of_mass|lang=zh-CN|style=Feynman)规定了严格的核算：每消失一个反应物A的分子，就必须出现相应数量的产物B和C的分子。这种关系被一个**化学计量矩阵** $S$ 所捕捉。我们可以构建一个**[化学计量](@keyword=chemical_stoichiometry|lang=zh-CN|style=Feynman)约束的[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)**（SC-Neural ODE），其中系统的动力学被*定义*为 $\frac{d\mathbf{c}}{dt} = S \cdot \mathbf{v}$。在这里，已知的、固定的矩阵 $S$ 强制执行质量守恒定律，而[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络则用于学习[反应速率](@keyword=reaction_rate|lang=zh-CN|style=Feynman) $\mathbf{v}$ 作为浓度 $\mathbf{c}$ 的函数 [@problem_id:1453787]。因此，该模型通过其自身的构造就保证了质量守恒。

这一原则也扩展到物理学的其他领域。在哈密顿力学中，[保守系统](@keyword=conservative_systems|lang=zh-CN|style=Feynman)由[零散度](@keyword=divergence_free|lang=zh-CN|style=Feynman)的向量场描述。我们可以构建一个[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)，其雅可比矩阵在设计上就是[斜对称矩阵](@keyword=skew_symmetric_matrix|lang=zh-CN|style=Feynman)。这类矩阵的一个基本性质是其迹为零，这意味着该模型的向量场保证是[无散度](@keyword=divergence_free|lang=zh-CN|style=Feynman)的。虽然这本身不足以保证[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)，但这个性质是哈密顿系统的一个关键特征。基于这一原理构建的架构可以确保一个学到的类似于能量的量（[哈密顿量](@keyword=hamiltonian_function|lang=zh-CN|style=Feynman)）是完美守恒的 [@problem_id:3187135]。

**2. 通过引导施加约束（损失函数）：** 另一种方法是让模型拥有灵活的架构，但在训练过程中每当它违反已知定律时就“惩罚”它。假设我们正在为一个酶反应建模，我们知道酶的总量（游离酶加[底物结合](@keyword=substrate_binding|lang=zh-CN|style=Feynman)酶）必须是恒定的。这意味着这个总量的時間導數 $\frac{d}{dt}(E(t) + ES(t))$ 必须为零。我们可以在我们的损失函数中添加一个惩罚项，当这个導數偏离零时，该惩罚项会变大。在训练过程中，优化过程将被迫寻找不仅拟[合数](@keyword=composite_numbers|lang=zh-CN|style=Feynman)据而且遵守这一[守恒定律](@keyword=conservation_law|lang=zh-CN|style=Feynman)的网络参数 [@problem_id:1453797]。

### 从黑箱到科学洞见

对机器学习的一个常见批评是它产生“黑箱”模型：它们可能做出很好的预测，但它们不给我们提供基本的理解。[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)对这一批评提出了强有力的反驳。因为学到的对象是一个透明的数学函数——向量场——我们可以运用动力系统理论的全部武器库来分析它。

一旦我们训练了一个[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)来描述，比如说，一个[基因开关](@keyword=genetic_switches|lang=zh-CN|style=Feynman)，我们就拥有了一个显式函数 $\frac{dy}{dt} = f(y, p)$，其中 $p$ 可能是一个外部诱导物分子的浓度。我们现在可以分析这个函数以找到它的[稳态](@keyword=steady_states|lang=zh-CN|style=Feynman)（其中 $f(y,p)=0$）并确定它们的稳定性。更令人兴奋的是，我们可以问：是否存在任何“[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)”？通过寻找[不动点](@keyword=fixed_point|lang=zh-CN|style=Feynman)在何处产生或消失——一种称为**分岔**的现象——我们可以识别出导致[基因开关](@keyword=genetic_switches|lang=zh-CN|style=Feynman)行为发生戏剧性变化的关键诱导物 $p$ 值 [@problem_id:1453779]。模型从一个被动的数据拟合器转变为一个主动的科学发现工具。

### 终极目标：计算机模拟实验

也许这个框架最具未来感的应用是在计算机上完全执行反事实或“what if”实验。在系统生物学中，理解基因功能的一个关键工具是基因敲除实验，即沉默一个特定的基因以观察细胞会发生什么。这些实验可能缓慢且昂贵。

有了一个训练精良的[基因调控网络](@keyword=gene_regulatory_networks|lang=zh-CN|style=Feynman)[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)模型，我们就可以*在计算机上*进行这些实验。如果我们的模型已经学会了基因之间的影响网络，我们可以通过修改模型来模拟基因敲除——例如，通过将网络中对应于被沉默基因影响的部分置零——然后计算系统的新[稳态](@keyword=steady_states|lang=zh-CN|style=Feynman) [@problem_id:3333119]。这使得科学家能够快速测试假说，筛选出最具影响力的干预措施，并对系统的线路图获得深刻的、因果性的理解。

在这次宏大的巡礼中，我们看到了[神经常微分方程](@keyword=neural_ordinary_differential_equations|lang=zh-CN|style=Feynman)的真正前景。它们是连接两个世界的桥梁：一个是 messy、[高维数据](@keyword=high_dimensional_data|lang=zh-CN|style=Feynman)的世界，另一个是优雅、有原则的数学定律的世界。它们提供了一种语言，用于构建能从观察中学习、尊重现实基本约束的模型，并最终赋予我们对周围世界提出更深刻、更有洞察力问题的能力。