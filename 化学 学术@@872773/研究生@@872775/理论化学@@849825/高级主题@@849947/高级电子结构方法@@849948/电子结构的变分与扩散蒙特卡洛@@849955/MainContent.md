## 引言
在量子力学的世界里，精确求解多电子体系的薛定谔方程是理论化学与凝聚态物理的核心挑战。[变分蒙特卡罗](@entry_id:141537)（VMC）和[扩散](@entry_id:141445)蒙特卡罗（DMC）方法，统称为量子蒙特卡罗（QMC），是应对这一挑战的最强大、最精确的数值工具之一。这些方法不依赖于传统的[基组展开](@entry_id:204251)，而是通过[随机采样](@entry_id:175193)（“行走者”）直接模拟[多体波函数](@entry_id:203043)，从而能够以多项式级的计算成本捕获绝大部分电子关联能，为从第一性原理出发理解和预测分子与材料的性质提供了可能。

然而，[QMC方法](@entry_id:753887)的强大能力也伴随着独特的理论复杂性和计算挑战。其核心问题在于如何高效地在巨大的多[电子构型](@entry_id:272104)空间中进行采样，以及如何处理[费米子](@entry_id:146235)[波函数](@entry_id:147440)固有的反对称性所带来的“[符号问题](@entry_id:155213)”。本文旨在系统性地揭示[QMC方法](@entry_id:753887)的内在逻辑与实践智慧，填补从基础理论到前沿应用之间的知识鸿沟。

通过本文，读者将踏上一段从原理到实践的旅程。在“原理与机制”一章中，我们将奠定QMC的理论基石，从变分原理和蒙特卡罗积分出发，详细阐释试探波函数的构建、[费米子符号问题](@entry_id:144472)的起源以及[固定节点近似](@entry_id:145482)这一核心解决方案。接着，在“应用与跨学科联系”一章中，我们将展示这些方法如何在[量子化学](@entry_id:140193)和[材料科学](@entry_id:152226)的真实问题中大放异彩，从为[密度泛函理论](@entry_id:139027)提供基准，到精确[计算化学](@entry_id:143039)[反应势垒](@entry_id:168490)和固体[带隙](@entry_id:191975)。最后，“动手实践”部分将引导读者通过具体的计算练习，将理论知识转化为解决实际问题的能力。

## 原理与机制

本章将深入探讨[变分蒙特卡罗](@entry_id:141537)（Variational [Monte Carlo](@entry_id:144354), VMC）与[扩散](@entry_id:141445)蒙特卡罗（Diffusion [Monte Carlo](@entry_id:144354), DMC）方法的核心科学原理与计算机制。我们将从支撑这些方法的变分原理和蒙特卡罗积分的统计基础出发，系统地构建一个用于精确计算分子和材料[电子结构](@entry_id:145158)的理论框架。我们将阐明如何构建和优化[试探波函数](@entry_id:142892)，如何处理[费米子](@entry_id:146235)体系固有的[符号问题](@entry_id:155213)，以及在实际应用中如何应对非局域赝势和[有限尺寸效应](@entry_id:155681)等高级挑战。

### 变分原理与蒙特卡罗积分

量子蒙特卡罗方法的基础是量子力学的[变分原理](@entry_id:198028)。该原理指出，对于任意一个归一化的试探波函数 $|\Psi_T\rangle$，其[哈密顿量](@entry_id:172864) $\hat{H}$ 的[期望值](@entry_id:153208)（即变分能 $E_V$）是系统真实[基态能量](@entry_id:263704) $E_0$ 的一个上界：

$$E_V = \frac{\langle\Psi_T|\hat{H}|\Psi_T\rangle}{\langle\Psi_T|\Psi_T\rangle} \ge E_0$$

VMC 方法的策略就是通过优化一个参数化的[试探波函数](@entry_id:142892) $\Psi_T(\mathbf{R}, \boldsymbol{\alpha})$（其中 $\mathbf{R}$ 代表所有电子的坐标，$\boldsymbol{\alpha}$ 是变分参数），来最小化变分能 $E_V$，从而获得对基态能量和[波函数](@entry_id:147440)的最佳近似。

变分能的表达式是一个[高维积分](@entry_id:143557)。对于一个包含 $N$ 个电子的体系，其[构型空间](@entry_id:149531)是 $3N$ 维的。解析地计算这个积分几乎是不可能的。蒙特卡罗方法为此提供了一个强大的数值解决方案。我们将积分表达式重写为：

$$E_V = \frac{\int |\Psi_T(\mathbf{R})|^2 \left( \frac{\hat{H}\Psi_T(\mathbf{R})}{\Psi_T(\mathbf{R})} \right) d\mathbf{R}}{\int |\Psi_T(\mathbf{R})|^2 d\mathbf{R}}$$

这里，我们定义了两个关键量。第一个是概率密度函数 $\pi(\mathbf{R}) = \frac{|\Psi_T(\mathbf{R})|^2}{\int |\Psi_T(\mathbf{R})|^2 d\mathbf{R}}$，它对应于量子力学中的玻恩几率密度。第二个是**局域能量 (local energy)** $E_L(\mathbf{R})$：

$$E_L(\mathbf{R}) = \frac{\hat{H}\Psi_T(\mathbf{R})}{\Psi_T(\mathbf{R})}$$

于是，变分能 $E_V$ 就变成了局域能量 $E_L(\mathbf{R})$ 在[概率密度](@entry_id:175496) $\pi(\mathbf{R})$ 下的[期望值](@entry_id:153208)：$E_V = \langle E_L \rangle_{\pi}$。

蒙特卡罗积分的核心思想是用在一个[分布](@entry_id:182848)中抽取的样本均值来近似该[分布](@entry_id:182848)下的[期望值](@entry_id:153208)。如果我们能从 $\pi(\mathbf{R})$ [分布](@entry_id:182848)中生成一系列电子构型样本 $\{ \mathbf{R}_1, \mathbf{R}_2, \dots, \mathbf{R}_M \}$，那么变分能的**蒙特卡罗估计量** $\hat{E}_M$ 就是这些构型上局域能量的样本均值：

$$\hat{E}_M = \frac{1}{M} \sum_{i=1}^{M} E_L(\mathbf{R}_i)$$

这个简单的估计量之所以有效，是基于概率论中两个强大的基本定理 [@problem_id:2828296]。**[大数定律](@entry_id:140915) (Law of Large Numbers, LLN)** 保证了只要样本是根据 $\pi(\mathbf{R})$ [独立同分布](@entry_id:169067)地抽取（或来自具有[平稳分布](@entry_id:194199) $\pi(\mathbf{R})$ 的[遍历马尔可夫链](@entry_id:266539)），并且局域能量的[期望值](@entry_id:153208)有限（即 $E_L \in L^1(\pi)$），那么当样本数量 $M \to \infty$ 时，估计量 $\hat{E}_M$ 将收敛到真实的[期望值](@entry_id:153208) $E_V$。

而**[中心极限定理](@entry_id:143108) (Central Limit Theorem, CLT)** 则描述了估计的[统计误差](@entry_id:755391)。它指出，在 LLN 的条件之外，如果局域能量的[方差](@entry_id:200758)也有限（即 $E_L \in L^2(\pi)$），那么对于足够大的 $M$，估计量 $\hat{E}_M$ 的[分布](@entry_id:182848)将近似于一个[正态分布](@entry_id:154414)，其均值为 $E_V$，[方差](@entry_id:200758)为 $\sigma^2_{E_L}/M$。这为我们量化计算结果的不确定性提供了理论依据。因此，VMC 计算的有效性依赖于能够有效地从 $|\Psi_T|^2$ [分布](@entry_id:182848)中抽样，并确保局域能量具有有限的均值和[方差](@entry_id:200758)。

### 生成构型：Metropolis 算法

为了实现上述蒙特卡罗积分，我们需要一种能够从目标概率密度 $\pi(\mathbf{R}) \propto |\Psi_T(\mathbf{R})|^2$ 中高效采样的算法。由于 $\pi(\mathbf{R})$ 的形式复杂且归一化因子未知，直接采样非常困难。**[马尔可夫链](@entry_id:150828)蒙特卡罗 (Markov Chain [Monte Carlo](@entry_id:144354), MCMC)** 方法，特别是 Metropolis 算法及其推广形式 Metropolis-Hastings 算法，为解决这一问题提供了通用方案 [@problem_id:2828329]。

MCMC 的核心思想是构建一个[马尔可夫链](@entry_id:150828)，使其稳态分布恰好是我们想要采样的目标分布 $\pi(\mathbf{R})$。一个确保此条件的充分条件是**[细致平衡条件](@entry_id:265158) (detailed balance condition)**。该条件要求对于任意两个构型 $\mathbf{R}$ 和 $\mathbf{R}'$，从 $\mathbf{R}$ 转移到 $\mathbf{R}'$ 的速率等于从 $\mathbf{R}'$ 转移回 $\mathbf{R}$ 的速率：

$$\pi(\mathbf{R}) K(\mathbf{R} \to \mathbf{R}') = \pi(\mathbf{R}') K(\mathbf{R}' \to \mathbf{R})$$

其中 $K(\mathbf{R} \to \mathbf{R}')$ 是[马尔可夫链](@entry_id:150828)的转移核（转移概率）。

Metropolis-Hastings 算法将转移过程分解为两步：**提议 (proposal)** 和 **接受 (acceptance)**。
1.  **提议**：从当前构型 $\mathbf{R}$，根据一个提议分布 $q(\mathbf{R}'|\mathbf{R})$ 生成一个新的候选构型 $\mathbf{R}'$。一个简单的例子是，在一个以 $\mathbf{R}$ 为中心的小球内均匀地选择一个新点。
2.  **接受**：以一定的接受概率 $\alpha(\mathbf{R} \to \mathbf{R}')$ 接受这个移动。如果接受，则新构型为 $\mathbf{R}'$；否则，[新构型](@entry_id:199611)仍为 $\mathbf{R}$。

将转移核写作 $K(\mathbf{R} \to \mathbf{R}') = q(\mathbf{R}'|\mathbf{R}) \alpha(\mathbf{R} \to \mathbf{R}')$ 并代入[细致平衡条件](@entry_id:265158)，可以推导出 Metropolis-Hastings [接受概率](@entry_id:138494)：

$$\alpha(\mathbf{R} \to \mathbf{R}') = \min\left(1, \frac{\pi(\mathbf{R}') q(\mathbf{R}|\mathbf{R}')}{\pi(\mathbf{R}) q(\mathbf{R}'|\mathbf{R})}\right)$$

对于我们的 VMC 计算，$\pi(\mathbf{R}) \propto |\Psi_T(\mathbf{R})|^2$。由于我们只关心比值，未知的[归一化常数](@entry_id:752675)被消掉了：

$$\alpha(\mathbf{R} \to \mathbf{R}') = \min\left(1, \frac{|\Psi_T(\mathbf{R}')|^2}{|\Psi_T(\mathbf{R})|^2} \frac{q(\mathbf{R}|\mathbf{R}')}{q(\mathbf{R}'|\mathbf{R})}\right)$$

如果提议分布是对称的，即 $q(\mathbf{R}'|\mathbf{R}) = q(\mathbf{R}|\mathbf{R}')$（例如，简单的[随机游走](@entry_id:142620)），则该公式简化为最初的 Metropolis 形式：

$$\alpha(\mathbf{R} \to \mathbf{R}') = \min\left(1, \frac{|\Psi_T(\mathbf{R}')|^2}{|\Psi_T(\mathbf{R})|^2}\right)$$

这个算法非常直观：如果移动到一个[波函数](@entry_id:147440)幅值更大的区域（概率更高），则总是接受；如果移动到幅值更小的区域，则以一个正比于概率比值的概率接受。通过重复这个过程，我们生成的“行走者”(walker) 序列就会逐渐收敛并最终在整个构型空间中以 $|\Psi_T|^2$ 的概率密度进行采样。为了保证算法的正确性，[马尔可夫链](@entry_id:150828)还必须满足**遍历性 (ergodicity)**，即从任何一个非零概率的构型出发，都有可能在有限步内到达其他任何非零概率的构型。这通常通过确保[提议分布](@entry_id:144814) $q$ 在 $\pi$ 的支撑集上是正的来实现。

### 试探波函数：艺术与科学的结合

VMC 和 DMC 的准确性在很大程度上取决于[试探波函数](@entry_id:142892)的质量。一个好的试探波函数应该能够以紧凑的解析形式尽可能精确地捕捉到体系复杂的物理特性。在[电子结构计算](@entry_id:748901)中，最成功和广泛使用的形式是 **Slater-Jastrow [波函数](@entry_id:147440)** [@problem_id:2828276]。

$$\Psi_T(\mathbf{R}) = e^{J(\mathbf{R})} D(\mathbf{R})$$

该[波函数](@entry_id:147440)由两部分组成：一个 Slater [行列式](@entry_id:142978) $D(\mathbf{R})$ 和一个 [Jastrow 因子](@entry_id:158362) $e^{J(\mathbf{R})}$。这两部分扮演着截然不同但互补的角色。

#### Slater [行列式](@entry_id:142978)与反对称性

**Slater [行列式](@entry_id:142978) (Slater determinant)** $D(\mathbf{R})$ 是由单粒子[轨道](@entry_id:137151) $\phi_k$ 构成的[行列式](@entry_id:142978)：

$$D(\mathbf{R}) = \det[\phi_k(\mathbf{r}_i, \sigma_i)]$$

其中 $(\mathbf{r}_i, \sigma_i)$ 是第 $i$ 个电子的空间和自旋坐标。根据[行列式](@entry_id:142978)的性质，交换任意两行（对应于交换两个电子的坐标）会使[行列式](@entry_id:142978)的值变为[相反数](@entry_id:151709)。因此，Slater [行列式](@entry_id:142978)天然地满足了[费米子](@entry_id:146235)[波函数](@entry_id:147440)所必须的**反对称性原理 (Antisymmetry Principle)**。这种[反对称性](@entry_id:261893)是[泡利不相容原理](@entry_id:141850)的直接体现，它阻止了具有相同自旋的电子占据相同的空间位置，从而引入了所谓的交换关联或费米关联。

至关重要的是，Slater [行列式](@entry_id:142978)的值可以为零。这些为零的点 $\mathbf{R}$ 在 $3N$ 维[构型空间](@entry_id:149531)中构成了一个 $(3N-1)$ 维的[超曲面](@entry_id:159491)，即**节面 (nodal surface)**。

#### [Jastrow 因子](@entry_id:158362)与电子关联

**[Jastrow 因子](@entry_id:158362) (Jastrow factor)** $e^{J(\mathbf{R})}$ 是一个实值的、对称的、恒正的函数，其作用是显式地描述电子之间的**动力学关联 (dynamical correlation)**。由于电子之间存在[库仑排斥](@entry_id:181876)，它们倾向于相互躲避。[Jastrow 因子](@entry_id:158362)通过引入依赖于电子间距离 $r_{ij} = |\mathbf{r}_i - \mathbf{r}_j|$ 的项来实现这一点。一个典型的 Jastrow 指数 $J(\mathbf{R})$ 包含[单体](@entry_id:136559)（电子-核）、二体（电子-电子）甚至更高阶的关联项。

由于 [Jastrow 因子](@entry_id:158362) $e^{J(\mathbf{R})}$ 是对称且恒正的，它不会改变整个[波函数](@entry_id:147440)的反对称性（[对称函数](@entry_id:177113)乘以反[对称函数](@entry_id:177113)仍为反[对称函数](@entry_id:177113)），也不会改变[波函数](@entry_id:147440)的[节面结构](@entry_id:151019)（因为 $e^{J(\mathbf{R})} D(\mathbf{R}) = 0$ 当且仅当 $D(\mathbf{R}) = 0$）。因此，在一个 Slater-Jastrow [波函数](@entry_id:147440)中，**[节面结构](@entry_id:151019)完全由 Slater [行列式](@entry_id:142978)部分决定** [@problem_id:2828276]。

[Jastrow 因子](@entry_id:158362)还可以包含依赖于[电子自旋](@entry_id:137016)的项，例如对平行自旋和反平行自旋电子对使用不同的关联函数。这在物理上是合理的，因为平行自旋电子已经由于[泡利不相容原理](@entry_id:141850)而相互排斥（形成[费米洞](@entry_id:137389)），而反平行自旋电子则主要通过[库仑排斥](@entry_id:181876)来躲避彼此（形成[库仑洞](@entry_id:199132)）。一个设计良好的自旋依赖 [Jastrow 因子](@entry_id:158362)能够精确地描述这两种不同的关联行为，同时不改变节面 [@problem_id:2828276]。

#### Kato [尖点条件](@entry_id:190416)与零[方差](@entry_id:200758)原理

[Jastrow 因子](@entry_id:158362)还有一个至关重要的作用，即满足 **Kato [尖点条件](@entry_id:190416) (Kato cusp conditions)**。该条件描述了当两个[带电粒子](@entry_id:160311)（如两个电子，或一个电子和一个[原子核](@entry_id:167902)）相互靠近时，[波函数](@entry_id:147440)的正确解析行为。具体来说，当两个粒子重合时，[哈密顿量](@entry_id:172864)中的[库仑势能](@entry_id:263842)项会发散。为了使局域能量 $E_L(\mathbf{R})$ 在这些点保持有限，动能项的发散必须精确地抵消[势能](@entry_id:748988)项的发散。一个标准的 Slater [行列式](@entry_id:142978)通常无法满足这个条件，导致局域能量在粒子重合点发散，从而使得 VMC 能量估计的[方差](@entry_id:200758)变为无穷大。

通过在 [Jastrow 因子](@entry_id:158362)中引入正确的[短程关联](@entry_id:158693)形式（例如，包含线性的 $r_{ij}$ 项），我们可以强制[试探波函数](@entry_id:142892)满足[尖点条件](@entry_id:190416)。这使得局域能量 $E_L(\mathbf{R})$ 在整个构型空间中变得更加平滑，从而极大地减小了统计[方差](@entry_id:200758)，提高了 VMC 计算的效率。

这一观察引出了一个更普遍的**零[方差](@entry_id:200758)原理 (zero-variance principle)** [@problem_id:2828298]。如果我们的[试探波函数](@entry_id:142892) $\Psi_T$ 恰好是[哈密顿量](@entry_id:172864)的一个[精确本征态](@entry_id:138620) $\Psi_0$（即 $\hat{H}\Psi_0 = E_0\Psi_0$），那么局域能量在任何非节面点上都将是一个常数：

$$E_L(\mathbf{R}) = \frac{\hat{H}\Psi_0(\mathbf{R})}{\Psi_0(\mathbf{R})} = \frac{E_0\Psi_0(\mathbf{R})}{\Psi_0(\mathbf{R})} = E_0$$

在这种理想情况下，局域能量的[方差](@entry_id:200758)为零。这个原理有两个重要推论：
1.  VMC 能量的[方差](@entry_id:200758)可以作为衡量试探波函数质量的一个指标。[方差](@entry_id:200758)越小，$\Psi_T$ 在某种意义上就越接近某个精确的本征态。
2.  我们可以将最小化[能量方差](@entry_id:156656)作为优化[波函数](@entry_id:147440)参数的目标，而不是最小化能量本身。[方差](@entry_id:200758)最小化是一个稳健的优化策略，并且由于其目标值（零）是已知的，因此具有一些数值优势。然而，需要注意的是，任何本征态（包括[激发态](@entry_id:261453)）的[方差](@entry_id:200758)都为零，因此[方差](@entry_id:200758)最小化本身并不保证收敛到[基态](@entry_id:150928) [@problem_id:2828298]。

### 投影方法与[费米子符号问题](@entry_id:144472)

尽管 VMC 是一种强大的方法，但其准确性完全受限于我们所选择的[试探波函数](@entry_id:142892)的函数形式。为了超越这一限制，**[扩散](@entry_id:141445)蒙特卡罗 (DMC)** 等投影方法被引入。DMC 的核心思想是利用**虚时[演化算符](@entry_id:182628)** $e^{-\tau \hat{H}}$ 将一个初始的试探态 $|\Psi_T\rangle$ 投影到[哈密顿量](@entry_id:172864)的[基态](@entry_id:150928) $|\Phi_0\rangle$。

将 $|\Psi_T\rangle$ 按 $\hat{H}$ 的本征态 $\{|\Phi_n\rangle, E_n\}$ 展开：$|\Psi_T\rangle = \sum_n c_n |\Phi_n\rangle$。经过虚时演化后，我们得到：

$$|\Psi(\tau)\rangle = e^{-\tau \hat{H}} |\Psi_T\rangle = \sum_n c_n e^{-\tau E_n} |\Phi_n\rangle = c_0 e^{-\tau E_0} |\Phi_0\rangle + c_1 e^{-\tau E_1} |\Phi_1\rangle + \dots$$

当虚时 $\tau$ 足够大时，能量最低的项 $e^{-\tau E_0}$ 将会呈指数级地主导整个级数（假设 $c_0 = \langle\Phi_0|\Psi_T\rangle \neq 0$）。因此，$\lim_{\tau \to \infty} |\Psi(\tau)\rangle \propto |\Phi_0\rangle$。

虚时薛定谔方程在数学上等价于一个漂移-[扩散](@entry_id:141445)-反应方程，可以由一个“行走者”系综的[随机过程](@entry_id:159502)来模拟。然而，对于[费米子](@entry_id:146235)体系，一个严重的问题阻碍了这种直接模拟，这就是著名的**[费米子符号问题](@entry_id:144472) (fermion sign problem)** [@problem_id:2828323]。

问题根源在于，对于一个给定的[粒子系统](@entry_id:180557)，其[哈密顿量](@entry_id:172864)的绝对[基态](@entry_id:150928)（能量最低的[本征态](@entry_id:149904)）是一个全对称的、无[节面](@entry_id:752526)的“[玻色子](@entry_id:138266)”[基态](@entry_id:150928) $|\Phi_B\rangle$，其能量为 $E_B$。而我们感兴趣的、满足[反对称性](@entry_id:261893)原理的[费米子](@entry_id:146235)[基态](@entry_id:150928) $|\Phi_F\rangle$（能量为 $E_F$）实际上是 $\hat{H}$ 的一个[激发态](@entry_id:261453)，因此其能量必然高于[玻色子](@entry_id:138266)[基态](@entry_id:150928)：$E_F > E_B$。

在一个无约束的投影模拟中，任何由于数值噪声或初始态不完美而引入的微小玻色对称性分量，都会随着虚时演化被指数放大，其幅度与[费米子](@entry_id:146235)信号的幅度之比将以 $\exp[-(E_B - E_F)\tau] = \exp[(E_F - E_B)\tau]$ 的形式增长。最终，全正的[玻色子](@entry_id:138266)[基态](@entry_id:150928)将完全“淹没”具有正负区域的[费米子](@entry_id:146235)[基态](@entry_id:150928)信号。

从统计角度看，这意味着代表[波函数](@entry_id:147440)正负部分的行走者数量将趋于相等，导致[期望值](@entry_id:153208)的计算涉及两个巨大数值的相消，信噪比随之指数衰减。维持固定统计精度所需的样本数量将随投影时间 $\tau$ 和能量差 $E_F - E_B$ 指数增长，其形式为 $\exp[2(E_F - E_B)\tau]$ [@problem_id:2828323]。这使得对中等或更大体系的精确计算在计算上变得不可行。

### [固定节点近似](@entry_id:145482)：一个实用的解决方案

解决[费米子符号问题](@entry_id:144472)的标准方法是**[固定节点近似](@entry_id:145482) (fixed-node approximation, FN)** [@problem_id:2810551]。这个近似的核心思想是，我们不让[波函数演化](@entry_id:273614)到其真实的[节面结构](@entry_id:151019)，而是强制演化后的[波函数](@entry_id:147440) $\Psi(\mathbf{R}, \tau)$ 的节面与我们预先给定的一个[试探波函数](@entry_id:142892) $\Psi_T(\mathbf{R})$ 的节面完全相同。

在实践中，这相当于在试探波函数的[节面](@entry_id:752526) $\Gamma_T = \{\mathbf{R} | \Psi_T(\mathbf{R})=0\}$ 上施加一个**狄利克雷边界条件 (Dirichlet boundary condition)**，即 $\Psi(\mathbf{R}, \tau) = 0$ for $\mathbf{R} \in \Gamma_T$。这个边界条件将整个构型空间分割成多个互不连通的**节苞 (nodal pockets)**。每个行走者被限制在它初始所在的节苞内，不允许穿越[节面](@entry_id:752526)。由于在单个节苞内，[波函数](@entry_id:147440)的符号是恒定的（全正或全负），我们可以简单地模拟其[绝对值](@entry_id:147688)，从而完全消除了[符号问题](@entry_id:155213)。

[固定节点近似](@entry_id:145482)带来了两个关键结果：
1.  **它是一个近似**：由于我们强制使用了不精确的节面，DMC 计算的结果将包含一个**固定节点误差 (fixed-node error)**。
2.  **它具有变分性**：固定节点能量 $E_{FN}$ 是对真实[费米子](@entry_id:146235)基态能量 $E_F$ 的一个严格**[上界](@entry_id:274738)**，即 $E_{FN} \ge E_F$。这是因为固定节点约束相当于在变分法中限制了[希尔伯特空间](@entry_id:261193)的搜索范围。

[固定节点近似](@entry_id:145482)的质量完全取决于试探波函数[节面](@entry_id:752526)的质量。如果试探[节面](@entry_id:752526)与真实节面完全一致，固定节点 DMC 将给出精确的基态能量 [@problem_id:2810551]。这凸显了发展高精度[试探波函数](@entry_id:142892)（特别是其[行列式](@entry_id:142978)部分）的重要性，例如使用多[行列式](@entry_id:142978)展开或回流 (backflow) 变换等方法来系统地改善[节面结构](@entry_id:151019) [@problem_id:2828276]。

一个与直觉可能相悖的重要性质是，固定节点能量与[节面](@entry_id:752526)几何结构之间的关系遵循**[定义域单调性](@entry_id:174788) (domain monotonicity)** [@problem_id:2828275]。如果一个节面 $\Gamma_2$ 包含了另一个节面 $\Gamma_1$ 以及一些额外的[节面](@entry_id:752526)（即 $\Gamma_1 \subset \Gamma_2$），这意味着 $\Gamma_2$ 将构型空间划分成了更小、更多的节苞。这种更强的约束会提高体系的动能（类似于“无限深势阱”中尺寸越小能量越高的效应），从而导致更高的固定节点能量：$E_{FN}[\Gamma_2] > E_{FN}[\Gamma_1]$。因此，一个“更好”的[节面](@entry_id:752526)并非指节面更多或更复杂，而是指其位置和拓扑结构更接近于真实[节面](@entry_id:752526)，从而能够给出更低的固定节点能量。值得强调的是，固定节点能量 $E_{FN}$ 仅是[节面](@entry_id:752526)的泛函，与试探波函数在节苞内的具体幅值无关，并且 VMC 能量的高低与 FN 能量的高低之间没有必然的联系。

### 高级主题与实践考量

在将 VMC 和 DMC 应用于实际问题时，还会遇到其他一些重要的理论和技术挑战。

#### DMC 中的[期望值](@entry_id:153208)估计

在固定节点 DMC 中，由于使用了[重要性采样](@entry_id:145704)，行走者的稳态分布是[混合分布](@entry_id:276506) $f(\mathbf{R}) \propto \Phi_0(\mathbf{R})\Psi_T(\mathbf{R})$，其中 $\Phi_0$ 是真实的固定[节点基](@entry_id:752522)态。对于与[哈密顿量](@entry_id:172864) $\hat{H}$ 对易的算符 $\hat{O}$（如能量本身），其[期望值](@entry_id:153208)的**混合估计量 (mixed estimator)** 是无偏的 [@problem_id:2828274]。

$$\langle \hat{O} \rangle_{\mathrm{mix}} = \frac{\langle \Phi_0 | \hat{O} | \Psi_T \rangle}{\langle \Phi_0 | \Psi_T \rangle} = \langle \hat{O} \rangle_{\mathrm{exact}}$$

然而，对于大多数其他[物理可观测量](@entry_id:154692)（如密度、偶极矩等），它们与 $\hat{H}$ 不对易，其混合估计量是有偏的。如果试探波函数与真实[基态](@entry_id:150928)的误差为一阶小量 $\mathcal{O}(\epsilon)$，即 $|\Psi_T\rangle \approx |\Phi_0\rangle + \epsilon |\Phi_\perp\rangle$，那么混合[估计量的偏差](@entry_id:168594)也是一阶的 $\mathcal{O}(\epsilon)$。

一种简单的修正方法是**外推估计 (extrapolated estimation)**。可以证明，VMC 估计量 $\langle \hat{O} \rangle_{VMC} = \langle \Psi_T | \hat{O} | \Psi_T \rangle / \langle \Psi_T | \Psi_T \rangle$ 的偏差通常是混合估计量偏差的两倍。因此，可以通过线性组合来消除一阶误差：

$$\langle \hat{O} \rangle_{\mathrm{extr}} = 2 \langle \hat{O} \rangle_{\mathrm{mix}} - \langle \hat{O} \rangle_{\mathrm{VMC}} = \langle \hat{O} \rangle_{\mathrm{exact}} + \mathcal{O}(\epsilon^2)$$

这种外推方法将偏差减小到二阶，大大提高了计算精度。更精确的方法，如**前向行走 (forward walking)** 或 **后代加权 (descendant weighting)**，旨在直接从纯[分布](@entry_id:182848) $\Phi_0^2$ 中采样，从而原则上可以完全消除这种偏差，但计算成本也更高 [@problem_id:2828274]。

#### 非局域[赝势](@entry_id:170389)的处理

在对含有重元素的体系进行计算时，通常使用**[赝势](@entry_id:170389) (pseudopotential)** 来替代核心电子，从而只须处理价电子。现代赝势通常包含一个**非局域 (nonlocal)** 部分 $\hat{V}^{\mathrm{NL}}$，它是一个积分算符。在 DMC 这种实空间方法中，非局域算符会导致行走者在构型空间中进行“跳跃”，这给[随机过程](@entry_id:159502)的模拟带来了困难。

一个简单的处理方法是**局域近似 (locality approximation, LA)** [@problem_id:2828284]。它将非局域算符对演化[波函数](@entry_id:147440) $\Psi$ 的作用近似为对已知[试探波函数](@entry_id:142892) $\Psi_T$ 的作用，从而得到一个等效的局域势 $V^{\mathrm{LA}}(\mathbf{R}) = (\hat{V}^{\mathrm{NL}}\Psi_T)/\Psi_T$。这种做法虽然简便，但引入了一个非厄米的等效[哈密顿量](@entry_id:172864)，破坏了 DMC 能量的变分[上界](@entry_id:274738)性质，可能导致结果偏高或偏低。更严重的是，在 $\Psi_T$ 的节面附近，$V^{\mathrm{LA}}$ 可能会发散，导致行走者权重爆炸，引发[数值不稳定性](@entry_id:137058)。

一个更严格的处理方案是 **T-moves 方案**。该方案将非局域算符的贡献精确地映射到行走者的[转移矩阵](@entry_id:145510)中。它将[转移矩阵](@entry_id:145510)中可能导致负概率的部分识别出来，并将其作为一组离散的、概率非负的“跳跃”（即 T-moves）进行采样，同时将剩余部分合并到对角项的权重因子中。这种方法保证了转移概率的非负性，从而稳定了模拟，并且最关键的是，它恢复了 DMC 能量的变分性质，为处理非局域赝势提供了可靠的框架 [@problem_id:2828284]。

#### 周期性体系中的[有限尺寸效应](@entry_id:155681)

当模拟晶体等周期性体系时，我们通常采用一个有限的**超胞 (supercell)** 并施加[周期性边界条件](@entry_id:147809)。这种做法会引入**[有限尺寸效应](@entry_id:155681) (finite-size effects)**。其中，**[单体](@entry_id:136559)[有限尺寸效应](@entry_id:155681)**尤为突出，它源于在有限超胞中，单粒子动量（即波矢 $\mathbf{k}$）只能取一系列离散值，这相当于用一个稀疏的 $\mathbf{k}$ 点网格来近似[热力学极限](@entry_id:143061)下连续的[布里渊区积分](@entry_id:188454)。这种离散化会导致能量计算出现与超胞尺寸和形状相关的“壳层填充”[振荡](@entry_id:267781)。

为了减小这种误差，**[扭转平均边界条件](@entry_id:756245) (twist-averaged boundary conditions, TABC)** 被广泛采用 [@problem_id:2828314]。其思想是在[多体波函数](@entry_id:203043)上施加一个广义的边界条件：

$$\Psi(\ldots, \mathbf{r}_i + \mathbf{L}, \ldots) = e^{i\boldsymbol{\theta} \cdot \mathbf{L}} \Psi(\ldots, \mathbf{r}_i, \ldots)$$

其中 $\mathbf{L}$ 是超胞的[晶格矢量](@entry_id:161583)，$\boldsymbol{\theta}$ 是一个“扭转角”矢量。施加一个扭转角 $\boldsymbol{\theta}$ 等效于将整个 $\mathbf{k}$ 点网格在[动量空间](@entry_id:148936)中平移一个固定的偏移量。通过对多个不同的扭转角 $\boldsymbol{\theta}$ 分别进行独立的 QMC 计算，然后将结果平均，就可以有效地模拟对[布里渊区](@entry_id:142395)的积分，从而极大地抑制壳层填充效应，加速向[热力学极限](@entry_id:143061)的收敛。对于给定的计算资源，扭转平均通常是减小[单体](@entry_id:136559)[有限尺寸效应](@entry_id:155681)最有效的方法。