## 引言
在现代科学与工程中，[计算模型](@entry_id:637456)是理解和预测复杂现象不可或缺的工具。然而，这些模型的输入参数，无论是源于测量误差、自然变异性还是知识的缺乏，都不可避免地带有不确定性。仅依赖于确定性预测，即给出单一的最佳猜测结果，已无法满足在航空航天、材料设计、气候科学和生物医学等高风险领域进行[稳健决策](@entry_id:184609)的需求。因此，量化这种输入不确定性如何传播至模型输出，并最终影响预测结果的可信度，成为了一个核心的科学挑战。前向不确定性传播正是解决这一问题的基础。

本文旨在系统性地介绍前向不确定性传播的理论、方法与应用。我们的学习旅程将分为三个部分。首先，在“原理与机制”一章中，我们将深入探讨不确定性传播的数学基础，剖析其核心计算方法，如近似方法、采样技术和先进的[谱方法](@entry_id:141737)，为您构建坚实的理论知识体系。接着，在“应用与交叉学科联系”一章中，我们将展示这些原理如何在材料科学、地球物理、多尺度建模和贝叶斯推断等前沿领域中得到应用，揭示其作为一种通用分析工具的强大能力。最后，通过“动手实践”部分，您将有机会通过解决具体问题来巩固所学知识。通过这一结构化的学习路径，您将能够掌握将输入不确定性转化为可信预测的关键技能。

## 原理与机制

本章深入探讨前向不确定性传播的核心原理与计算机制。我们将从不确定性传播的数学形式化定义出发，逐步介绍不确定性的分类、建模策略，并系统性地阐述一系列用于量化和传播不确定性的关键计算方法。本章旨在为读者构建一个坚实的基础，使其能够理解和应用现代不确定性量化（UQ）框架来解决复杂的科学与工程问题。

### [前向传播](@entry_id:193086)的数学基础

在科学建模中，我们通常使用一个确定性的数学模型，记作函数 $f$，来描述输入参数 $\boldsymbol{\xi}$ 与我们感兴趣的输出量（Quantity of Interest, QoI）$Q$ 之间的关系，即 $Q = f(\boldsymbol{\xi})$。在前向[不确定性传播](@entry_id:146574)的设定中，我们不再将输入 $\boldsymbol{\xi}$ 视为固定的值，而是将其看作一个定义在某个[概率空间](@entry_id:201477)上的[随机变量](@entry_id:195330)（或向量），其不确定性由一个概率律 $P_{\boldsymbol{\xi}}$ 来刻画。我们的核心任务是：给定模型 $f$ 和输入 $\boldsymbol{\xi}$ 的概率律 $P_{\boldsymbol{\xi}}$，确定输出量 $Q$ 的概率分布。

从数学角度看，这个过程被精确地定义为计算**[前推测度](@entry_id:201640)**（pushforward measure）。如果我们将输入 $\boldsymbol{\xi}$ 的概率律 $P_{\boldsymbol{\xi}}$ 视为定义在输入空间上的一个测度，那么输出 $Q$ 的概率律 $P_Q$ 就是 $P_{\boldsymbol{\xi}}$ 通过映射 $f$ 在输出空间上诱导出的测度。只要模型 $f$ 是一个从输入空间到输出空间的可测映射，这个[前推测度](@entry_id:201640)就是唯一且良定义的，我们记为 $P_Q = f_* P_{\boldsymbol{\xi}}$ 。

[前推测度](@entry_id:201640)可以通过两种等价的方式来定义：

1.  **通过[集合的原像](@entry_id:138126)**：对于输出空间中的任意一个可测集（[Borel集](@entry_id:144507)）$B$，输出量 $Q$ 落在该集合内的概率，等于输入量 $\boldsymbol{\xi}$ 落在 $B$ 在映射 $f$ 下的[原像](@entry_id:150899)（preimage）$f^{-1}(B)$ 内的概率。数学上表示为：
    $$
    P_Q(B) = P(Q \in B) = P(f(\boldsymbol{\xi}) \in B) = P(\boldsymbol{\xi} \in f^{-1}(B)) = P_{\boldsymbol{\xi}}(f^{-1}(B))
    $$
    这里，$f^{-1}(B) = \{\mathbf{x} \mid f(\mathbf{x}) \in B\}$。值得强调的是，这里的[原像](@entry_id:150899) $f^{-1}(B)$ 是为集合定义的，它并不要求函数 $f$ 本身是可逆的。即使多个不同的输入 $\mathbf{x}$ 映射到同一个输出，这个定义依然成立 。

2.  **通过[检验函数](@entry_id:166589)的期望**：对于任意有界可测的检验函数 $\varphi$，其作用于输出 $Q$ 上的[期望值](@entry_id:150961)，可以通过在输入空间上对[复合函数](@entry_id:147347) $\varphi(f(\boldsymbol{\xi}))$ 求期望来计算。这被称为**无意识统计学家定律**（Law of the Unconscious Statistician, LOTUS）：
    $$
    \mathbb{E}[\varphi(Q)] = \int \varphi(q) \, \mathrm{d}P_Q(q) = \int \varphi(f(\mathbf{x})) \, \mathrm{d}P_{\boldsymbol{\xi}}(\mathbf{x})
    $$
    这个定律极为重要，因为它允许我们直接通过已知的输入分布 $P_{\boldsymbol{\xi}}$ 来计算输出 $Q$ 的各种统计矩（如均值、方差等），而无需显式地求出 $P_Q$ 本身。例如，取 $\varphi(q)=q$ 可得均值，取 $\varphi(q)=q^2$ 可得二阶矩。

在这一数学框架下，区分**测度的前推**（pushforward）和**函数的拉回**（pullback）至关重要。前推是将输入空间上的一个测度（如 $P_{\boldsymbol{\xi}}$）“推”到输出空间，生成一个新的测度（$P_Q$）。而拉回则是将一个定义在输出空间上的函数（如 $g: \mathcal{Y} \to \mathbb{R}$）“拉”回到输入空间，生成一个新的函数 $g \circ f: \mathcal{X} \to \mathbb{R}$。这两个概念通过上述的LOTUS公式联系在一起：对一个函数 $g$ 关于[前推测度](@entry_id:201640)求积分，等价于对 $g$ 的拉回函数关于原测度求积分 。

一个关键的现象是，即使输入变量是[相互独立](@entry_id:273670)的，[非线性](@entry_id:637147)、非可分的模型 $f$ 也会在输出中引入统计相关性。例如，若输入 $X_1, X_2$ 独立，但模型为 $Y=f(X_1, X_2) = X_1 X_2$。我们观察两个输出量 $Z_1 = h_1(Y)$ 和 $Z_2 = h_2(Y)$。由于 $Z_1$ 和 $Z_2$ 共享同一个随机源 $Y$，它们通常是相关的。这是因为 $f$ 的等值线 $\{ (x_1, x_2) \mid x_1 x_2 = c \}$ 在输入空间中并非矩形，这表明 $f$ “混合”了独立输入的信息，从而导致其输出的多个不同观测值之间产生依赖关系 。这一现象凸显了对复杂模型进行不确定性传播分析的必要性。

### 不确定性的分类：[偶然不确定性与认知不确定性](@entry_id:1120923)

在进行[不确定性量化](@entry_id:138597)时，区分[不确定性的来源](@entry_id:164809)至关重要。通常，我们将不确定性分为两大类：

*   **[偶然不确定性](@entry_id:634772)（Aleatory Uncertainty）**：这是系统固有的、不可约减的随机性。即使我们对系统的物理规律和参数有完美的认知，这种不确定性依然存在。例如，在材料科学中，即使宏观参数固定，不同微观样本的内部结构依然存在随机变化。这种不确定性通常用一个概率分布来描述。

*   **认知不确定性（Epistemic Uncertainty）**：这源于我们知识的缺乏，例如对模型形式的不确定或对模型参数的不精确了解。原则上，通过收集更多的数据或信息，认知不确定性是可以被减小的。例如，通过实验测量来估计一个材料的[弹性模量](@entry_id:198862)，由于数据有限，估计值本身就存在不确定性。

为了在一个统一的框架内处理这两种不确定性，**[分层贝叶斯模型](@entry_id:169496)（Hierarchical Bayesian Model）**提供了一个强大的工具 。该模型通常包含两个层面：
1.  **第一层（[偶然不确定性](@entry_id:634772)）**：建立一个由参数 $\boldsymbol{\theta}$ 控制的概率模型来描述系统的固有随机性。例如，一个微观随机场 $X$ 可以被建模为一个以超参数 $\boldsymbol{\theta}$ 为条件的高斯过程，$X \mid \boldsymbol{\theta} \sim \mathcal{GP}(m_{\boldsymbol{\theta}}, k_{\boldsymbol{\theta}})$。
2.  **第二层（认知不确定性）**：由于参数 $\boldsymbol{\theta}$ 本身是不确定的，我们用一个概率分布来刻画我们对 $\boldsymbol{\theta}$ 的认知。通过贝叶斯法则，我们可以结合先验知识 $\pi(\boldsymbol{\theta})$ 和观测数据 $D$ 来得到 $\boldsymbol{\theta}$ 的[后验分布](@entry_id:145605) $\pi(\boldsymbol{\theta} \mid D) \propto \pi(D \mid \boldsymbol{\theta})\pi(\boldsymbol{\theta})$。

当这两种不确定性通过模型 $Y=\mathcal{H}(X)$ 向前传播时，我们可以使用**[全期望定律](@entry_id:265946)**和**[全方差定律](@entry_id:184705)**来分解输出 $Y$ 的总不确定性。给定数据 $D$，输出 $Y$ 的期望和方差可以表示为：
$$
\mathbb{E}[Y \mid D] = \mathbb{E}_{\boldsymbol{\theta} \mid D} \big[ \mathbb{E}[Y \mid \boldsymbol{\theta}] \big]
$$
$$
\mathrm{Var}(Y \mid D) = \underbrace{\mathbb{E}_{\boldsymbol{\theta} \mid D} \big[ \mathrm{Var}(Y \mid \boldsymbol{\theta}) \big]}_{\text{传播的偶然不确定性}} + \underbrace{\mathrm{Var}_{\boldsymbol{\theta} \mid D} \big( \mathbb{E}[Y \mid \boldsymbol{\theta}] \big)}_{\text{传播的认知不确定性}}
$$
在[方差分解](@entry_id:912477)的公式中，第一项是“[条件方差](@entry_id:183803)的期望”，它代表了由系统固有随机性（[偶然不确定性](@entry_id:634772)）引起的输出方差，并在我们对参数的认知不确定性上进行了平均。第二项是“[条件期望](@entry_id:159140)的方差”，它量化了由于参数 $\boldsymbol{\theta}$ 本身的不确定性（认知不确定性）所导致的输出[期望值](@entry_id:150961)的变化。这种分解对于理解和报告最终预测的不确定性来源至关重要。

### [前向传播](@entry_id:193086)的计算方法

直接根据[前推测度](@entry_id:201640)的定义来解析地计算输出分布，通常只对非常简单的模型和输入分布才可行。在大多数实际应用中，我们依赖于数值计算方法。这些方法大致可分为**侵入式（intrusive）**和**非侵入式（non-intrusive）**两大类 。

*   **非侵入式方法**：将已有的[确定性计算](@entry_id:271608)模型（求解器）视为一个“黑箱”，通过多次调用该模型来探索不确定性的影响。这类方法易于实施，特别是对于复杂的“遗留代码”。
*   **侵入式方法**：需要修改原确定性模型的控制方程，将随机性直接整合到方程中，然后求解一个更大的、耦合的[确定性系统](@entry_id:174558)。这类方法通常计算效率更高，但实现难度大。

#### 近似方法：[Delta方法](@entry_id:276272)

**[Delta方法](@entry_id:276272)**是一种基于[泰勒级数展开](@entry_id:138468)的简单近似方法 。假设输出 $Y = f(X)$，其中 $X$ 是一个随机向量，均值为 $\boldsymbol{\mu}_X$，[协方差矩阵](@entry_id:139155)为 $\boldsymbol{\Sigma}_X$。如果函数 $f$ 在 $\boldsymbol{\mu}_X$ 附近是光滑的，且 $X$ 的方差较小，我们可以将 $f$ 在 $\boldsymbol{\mu}_X$ 处进行一阶泰勒展开：
$$
Y = f(X) \approx f(\boldsymbol{\mu}_X) + \nabla f(\boldsymbol{\mu}_X)^{\top} (X - \boldsymbol{\mu}_X)
$$
基于这个线性近似，我们可以得到 $Y$ 的均值和方差的近似值：
$$
\mathbb{E}[Y] \approx \mathbb{E}[f(\boldsymbol{\mu}_X) + \nabla f(\boldsymbol{\mu}_X)^{\top} (X - \boldsymbol{\mu}_X)] = f(\boldsymbol{\mu}_X)
$$
$$
\mathrm{Var}(Y) \approx \mathrm{Var}(f(\boldsymbol{\mu}_X) + \nabla f(\boldsymbol{\mu}_X)^{\top} (X - \boldsymbol{\mu}_X)) = \nabla f(\boldsymbol{\mu}_X)^{\top} \boldsymbol{\Sigma}_X \nabla f(\boldsymbol{\mu}_X)
$$
其中 $\nabla f(\boldsymbol{\mu}_X)$ 是 $f$ 在 $\boldsymbol{\mu}_X$ 处的梯度。[Delta方法](@entry_id:276272)的优点是计算简单，只需要输入的一阶和二阶矩以及模型在均值处的梯度。然而，它的精度依赖于线性假设，对于高度[非线性](@entry_id:637147)的模型或输入方差较大的情况，其结果可能会有显著偏差。例如，一阶均值近似忽略了由函数曲率（二阶导数）引起的偏差项。

#### 基于采样的方法（非侵入式）

最直观的非侵入式方法是**蒙特卡洛（Monte Carlo, MC）**采样。该方法通过以下步骤进行：
1.  根据输入分布 $P_{\boldsymbol{\xi}}$ 生成 $N$ 个独立的随机样本 $\{\boldsymbol{\xi}^{(1)}, \boldsymbol{\xi}^{(2)}, \dots, \boldsymbol{\xi}^{(N)}\}$。
2.  对于每个样本 $\boldsymbol{\xi}^{(i)}$，调用确定性求解器计算对应的输出 $Q^{(i)} = f(\boldsymbol{\xi}^{(i)})$。
3.  利用得到的输出样本集 $\{Q^{(1)}, \dots, Q^{(N)}\}$ 来估计统计特性，例如样本均值 $\hat{\mathbb{E}}[Q] = \frac{1}{N} \sum_{i=1}^N Q^{(i)}$。

根据中心极限定理，MC估计的统计误差收敛速度为 $O(N^{-1/2})$。这个[收敛率](@entry_id:146534)不依赖于随机输入的维度 $d$，这使得MC方法在处理高维问题时非常稳健。然而，其[收敛速度](@entry_id:636873)较慢，为了获得高精度结果通常需要大量的[模型评估](@entry_id:164873)，当模型 $f$ 计算昂贵时，这可能是不可接受的。为了提高效率，发展了许多高级采样技术，如**拟蒙特卡洛（Quasi-Monte Carlo）**、**拉丁超立方采样（Latin Hypercube Sampling）**以及利用模型层次结构的**[多层蒙特卡洛](@entry_id:170851)（Multilevel [Monte Carlo](@entry_id:144354), MLMC）**方法  。

#### 谱方法（侵入式与非侵入式）

**[谱方法](@entry_id:141737)**是一类强大的技术，其核心思想是将随机输出量 $Q(\boldsymbol{\xi})$ 展开为一系列关于输入[随机变量](@entry_id:195330) $\boldsymbol{\xi}$ 的正交多项式基函数 $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$ 的级数，这被称为**[广义多项式混沌](@entry_id:749788)展开（generalized Polynomial Chaos Expansion, gPCE）**：
$$
Q(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathbb{N}_0^d} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})
$$
其中 $\boldsymbol{\alpha}$ 是多重指标， $c_{\boldsymbol{\alpha}}$ 是展开系数 。

为了使展开具有最优的收敛性，基函数 $\Psi_{\boldsymbol{\alpha}}$ 的选择至关重要。**Wiener-Askey对应关系**为不同类型的输入概率分布指定了相应的最佳[正交多项式](@entry_id:146918)族。例如：
*   [标准正态分布](@entry_id:184509) ($\mathcal{N}(0,1)$) 对应 **Hermite** 多项式。
*   均匀分布 ($\mathrm{Uniform}(-1,1)$) 对应 **Legendre** 多项式。
*   Gamma分布 ($\mathrm{Gamma}(k, \theta)$) 对应 **Laguerre** 多项式。

当输入是多维[独立随机变量](@entry_id:273896)时，多变量基函数 $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$ 通过[张量积](@entry_id:140694)的方式由相应的一元正交多项式构造而成。由于基[函数的正交性](@entry_id:160337)（$\mathbb{E}[\Psi_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\beta}}] = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$），展开系数可以通过[投影积分](@entry_id:1130229)计算：
$$
c_{\boldsymbol{\alpha}} = \mathbb{E}[Q(\boldsymbol{\xi}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})] = \int Q(\boldsymbol{\xi}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \rho(\boldsymbol{\xi}) \mathrm{d}\boldsymbol{\xi}
$$
一旦获得了PCE系数，输出的统计矩就可以非常廉价地计算出来。例如，均值为 $\mathbb{E}[Q] = c_{\mathbf{0}}$，方差为 $\mathrm{Var}(Q) = \sum_{\boldsymbol{\alpha} \neq \mathbf{0}} c_{\boldsymbol{\alpha}}^2$。

计算PCE系数的方法决定了谱方法是侵入式还是非侵入式：
*   **侵入式谱方法（[随机伽辽金法](@entry_id:178148)）**：将PCE代入模型的控制方程（如一个[偏微分](@entry_id:194612)方程），然后利用[伽辽金投影](@entry_id:145611)，得到一个关于所有未知系数 $c_{\boldsymbol{\alpha}}$ 的大规模、耦合的确定性方程组。求解这个系统可以一次性得到所有系数。这种方法通常效率很高，但需要深度修改现有求解器，实施复杂 。
*   **非侵入式谱方法**：将系数的[投影积分](@entry_id:1130229)通过数值积分（求积）来近似。这通常通过**[随机配置法](@entry_id:174778)（Stochastic Collocation）**实现。

#### [随机配置法](@entry_id:174778)（非侵入式）

**[随机配置法](@entry_id:174778)**通过在随机空间中选取一组离散的**[配置点](@entry_id:169000)（collocation points）**，在这些点上运行确定性模型 $f$，然后基于这些评估结果构建一个代理模型（通常是[多项式插值](@entry_id:145762)），最后通过对这个代理模型进行分析来计算统计矩 。

最直接的[配置点](@entry_id:169000)选择方式是**[张量积网格](@entry_id:755861)**。即在每个维度上选择一组一维的求积节点，然后通过[笛卡尔积](@entry_id:154642)形成高维网格。如果每个维度使用 $m$ 个点，那么在 $d$ 维空间中，总点数将是 $m^d$。这种指数级的增长被称为**[维数灾难](@entry_id:143920)（curse of dimensionality）**，使得[张量积网格](@entry_id:755861)在维度稍高时就变得不可行。

为了克服维数灾难，**[稀疏网格](@entry_id:139655)（Sparse Grids）**，特别是基于**[Smolyak算法](@entry_id:139824)**构造的[稀疏网格](@entry_id:139655)，提供了一个高效的替代方案。其核心思想是，对于光滑的函数，高阶的混合导数通常很小，这意味着高阶的交互作用对函数值的贡献不大。[稀疏网格](@entry_id:139655)通过一种精巧的组合方式，只保留那些“最重要”的[张量积网格](@entry_id:755861)点，而舍弃那些贡献较小的点。它不是简单地在每个维度上使用相同数量的点，而是组合了不同维度上具有不同分辨率的低阶[张量积网格](@entry_id:755861)。

对于具有足够[光滑性](@entry_id:634843)（例如，[解析性](@entry_id:140716)）的函数 $Q(\boldsymbol{\xi})$，[稀疏网格](@entry_id:139655)能够在保持近似[指数收敛](@entry_id:142080)率的同时，显著减少所需的[配置点](@entry_id:169000)数量。对于一个$L$级的[稀疏网格](@entry_id:139655)，其节点数大致按 $\mathcal{O}(2^L L^{d-1})$ 增长，远优于全张量网格的 $\mathcal{O}((2^L)^d)$。因此，[稀疏网格方法](@entry_id:755101)有效地“缓解”而非“消除”了[维数灾难](@entry_id:143920)，使其成为处理中等维度光滑问题的强大[非侵入式UQ](@entry_id:1128801)工具 。

### 进阶主题与实践考量

#### 使用[Copula函数](@entry_id:269548)建模相关性输入

许多标准UQ方法都假设输入[随机变量](@entry_id:195330)是相互独立的。然而，在现实世界中，输入参数之间常常存在复杂的依赖关系。**[Copula理论](@entry_id:142319)**为处理这种情况提供了一个强大而灵活的框架，它允许我们将多变量[联合分布](@entry_id:263960)的建模分解为两个独立的部分：各个变量的**边缘分布**和描述它们之间依赖结构的**[Copula函数](@entry_id:269548)** 。

**[Sklar定理](@entry_id:143965)**是[Copula理论](@entry_id:142319)的基石。该定理指出，对于任意一个[联合累积分布函数](@entry_id:262093)（CDF）$H(x_1, \dots, x_d)$，其边缘CDF为 $F_1(x_1), \dots, F_d(x_d)$，都存在一个[Copula函数](@entry_id:269548) $C: [0,1]^d \to [0,1]$，使得：
$$
H(x_1, \dots, x_d) = C(F_1(x_1), \dots, F_d(x_d))
$$
如果所有边缘分布都是连续的，那么这个[Copula函数](@entry_id:269548) $C$ 是唯一的。反之，给定任意一个[Copula函数](@entry_id:269548) $C$ 和一组边缘分布 $F_1, \dots, F_d$，上述公式构造出的 $H$ 必然是一个具有这些指定边缘分布的有效联合CDF。

这一定理提供了一个实用的工作流程来生成具有特定依赖结构的随机样本：
1.  根据问题的背景知识或数据，选择一个合适的[Copula函数](@entry_id:269548) $C$（例如，[Gaussian copula](@entry_id:141291), [Clayton copula](@entry_id:143723)等）来描述变量间的依赖结构。
2.  从所选的Copula分布 $C$ 中生成一个样本 $(u_1, \dots, u_d)$。这是一个在 $[0,1]^d$ 单位[超立方体](@entry_id:273913)内的随机向量。
3.  使用边缘分布的逆CDF（或[分位数函数](@entry_id:271351)）将该样本从单位立方体映射回物理空间：
    $$
    x_i = F_i^{-1}(u_i), \quad i=1, \dots, d
    $$
通过重复此过程，我们可以生成一组具有预设边缘分布和依赖结构的输入样本，然后将这些样本用于任何非侵入式的前向传播方法（如[蒙特卡洛](@entry_id:144354)）。

#### 不确定性归因：敏感度分析

前向[不确定性传播](@entry_id:146574)回答了“输出的不确定性有多大？”，而**全局敏感度分析（Global Sensitivity Analysis, GSA）**则进一步回答了“哪个输入对输出的不确定性贡献最大？”。

**[方差分析](@entry_id:275547)（[ANOVA](@entry_id:275547)）**或**Hoeffding-Sobol分解**提供了一个严谨的框架来解决这个问题 。对于一个函数 $Y=f(X_1, \dots, X_d)$，如果输入变量是[相互独立](@entry_id:273670)的，该函数可以被唯一地分解为一组具有正交性的分量函数之和：
$$
f(X_1, \dots, X_d) = f_0 + \sum_{i=1}^d f_i(X_i) + \sum_{1 \le i  j \le d} f_{ij}(X_i, X_j) + \dots + f_{1 \dots d}(X_1, \dots, X_d)
$$
其中，$f_0$ 是常数（即 $f$ 的期望），$f_i$ 描述了输入 $X_i$ 的**主效应**，$f_{ij}$ 描述了 $X_i$ 和 $X_j$ 的**交互效应**，以此类推。这些分量函数是正交的，即任意两个不同分量函数的乘[积的期望](@entry_id:190023)为零。

由于正交性，输出的总方差可以被分解为各个分量方差之和：
$$
\mathrm{Var}(Y) = V = \sum_{i=1}^d V_i + \sum_{1 \le i  j \le d} V_{ij} + \dots + V_{1 \dots d}
$$
其中 $V_i = \mathrm{Var}(f_i)$, $V_{ij} = \mathrm{Var}(f_{ij})$ 等。

基于此[方差分解](@entry_id:912477)，**[Sobol指数](@entry_id:156558)**被定义为每个分量方差占总方差的比例：
*   **一阶[Sobol指数](@entry_id:156558)**（主效应指数）：$S_i = \frac{V_i}{V}$，量化了输入 $X_i$ 单独对总方差的贡献。
*   **二阶[Sobol指数](@entry_id:156558)**（交互效应指数）：$S_{ij} = \frac{V_{ij}}{V}$，量化了 $X_i$ 和 $X_j$ 之间的[交互作用](@entry_id:164533)对总方差的贡献。

这些指数的总和为1，提供了一种将输出不确定性精确归因于各个输入及其交互作用的方法。值得注意的是，如果已经计算了模型的PCE，那么[Sobol指数](@entry_id:156558)可以直接从PCE系数中高效地计算出来，这使得谱方法成为进行敏感度分析的极具吸[引力](@entry_id:189550)的工具。