## 引言
在数据规模和[模型复杂度](@entry_id:145563)持续激增的时代，开发能够高效处理大规模、[分布](@entry_id:182848)式数据的优化算法已成为现代计算科学的核心挑战。交替方向乘子法（ADMM）作为一种强大而灵活的算法框架，应运而生。它通过将一个大的全局[问题分解](@entry_id:272624)为多个更小、更易于处理的子问题，并以迭代方式协调它们的解，从而在[分布式优化](@entry_id:170043)、[统计学习](@entry_id:269475)和信号处理等领域取得了巨大成功。

本文深入探讨ADMM的两种基础且影响深远的变体：**共识（consensus）** 和 **共享（sharing）**。尽管[ADMM](@entry_id:163024)的通用框架广为人知，但其在这两种特定结构下的精妙机制、理论保证以及实际应用中的细微差别，构成了从理论到实践的关键知识缺口。本文旨在填补这一缺口，为读者提供一个关于[ADMM](@entry_id:163024)共识与共享变体的全面、深入的指南。

为实现这一目标，本文将分为三个紧密相连的章节：
*   在**“原理与机制”**一章中，我们将从第一性原理出发，系统地推导共识与[共享ADMM](@entry_id:754745)的迭代格式，阐明[近端算子](@entry_id:635396)在其中的核心作用，并探讨其收敛特性、[停止准则](@entry_id:136282)以及多块扩展的理论陷阱。
*   在**“应用与交叉学科联系”**一章中，我们将展示这些理论如何在不同领域落地生根，探索[ADMM](@entry_id:163024)在[分布](@entry_id:182848)式机器学习、[图像处理](@entry_id:276975)、网络科学中的具体应用，并讨论其与[差分隐私](@entry_id:261539)、[随机优化](@entry_id:178938)等前沿方向的交叉融合。
*   最后，在**“动手实践”**一章中，我们将通过一系列精心设计的计算和分析练习，引导读者将理论知识转化为解决实际问题的能力，从性能分析到参数调优，亲身体验和掌握[ADMM](@entry_id:163024)的实践要领。

通过这一结构化的学习路径，读者将不仅理解[ADMM](@entry_id:163024)“是什么”和“为什么”有效，更能掌握“如何”将其应用于解决自己领域内的复杂[优化问题](@entry_id:266749)。

## 原理与机制

继前一章介绍之后，本章将深入探讨[交替方向乘子法](@entry_id:163024)（[ADMM](@entry_id:163024)）在[分布](@entry_id:182848)式[稀疏优化](@entry_id:166698)中的两种核心变体——**全局共识（global consensus）** 和 **共享（sharing）**——的数学原理和算法机制。我们将从第一性原理出发，推导这些算法的迭代步骤，阐明其与[近端算子](@entry_id:635396)（proximal operator）的深刻联系，并探讨它们的收敛特性、实际应用中的诊断方法以及更深层次的理论基础。

### 全局共识 ADMM

在许多[分布](@entry_id:182848)式学习和信号处理问题中，目标是最小化[分布](@entry_id:182848)在多个代理（或计算节点）上的局部函数之和，同时要求所有代理就一个共同的决策变量达成一致。这就是**全局[共识问题](@entry_id:637652)**。

#### 问题表述与[增广拉格朗日量](@entry_id:177042)

假设有 $N$ 个代理，每个代理 $i$ 持有一个私有的凸函数 $f_i: \mathbb{R}^p \to \mathbb{R} \cup \{+\infty\}$。全局目标是在强制所有局部决策变量 $x_i \in \mathbb{R}^p$ 相等的前提下，最小化这些函数的总和。为了实现这一点，我们引入一个全局共识变量 $v \in \mathbb{R}^p$，并将问题表述为以下约束优化形式：
$$
\min_{\{x_i\}_{i=1}^N,\,v \in \mathbb{R}^p} \sum_{i=1}^N f_i(x_i) \quad \text{subject to} \quad x_i=v, \quad \forall i \in \{1,\dots,N\}.
$$
这是一个具有 $N$ 个[等式约束](@entry_id:175290) $x_i - v = 0$ 的问题。为了使用 ADMM 求解，我们首先构造其**增广拉格朗日函数**（augmented Lagrangian）。对每个约束引入一个[拉格朗日乘子](@entry_id:142696)（或称**[对偶变量](@entry_id:143282)**）$\lambda_i \in \mathbb{R}^p$，并加入一个二次惩罚项，其强度由惩罚参数 $\rho > 0$ 控制。增广[拉格朗日函数](@entry_id:174593) $\mathcal{L}_\rho$ 定义为：
$$
\mathcal{L}_\rho(\{x_i\}, v, \{\lambda_i\}) = \sum_{i=1}^N f_i(x_i) + \sum_{i=1}^N \lambda_i^\top (x_i - v) + \frac{\rho}{2} \sum_{i=1}^N \|x_i - v\|_2^2.
$$
通过分配律，我们可以将求和合并，得到 [@problem_id:3438208]：
$$
\mathcal{L}_\rho(\{x_i\}, v, \{\lambda_i\}) = \sum_{i=1}^N \left( f_i(x_i) + \lambda_i^\top (x_i - v) + \frac{\rho}{2} \|x_i - v\|_2^2 \right).
$$
在实践中，使用**缩放[对偶变量](@entry_id:143282)**（scaled dual variable）$u_i = (1/\rho)\lambda_i$ 通常更为方便。通过代入 $\lambda_i = \rho u_i$ 并对二次项进行配方，增广拉格朗日函数可以等价地写为（忽略与优化变量无关的项）：
$$
\mathcal{L}_\rho(\{x_i\}, v, \{u_i\}) \propto \sum_{i=1}^N \left( f_i(x_i) + \frac{\rho}{2}\|x_i - v + u_i\|_2^2 \right).
$$
这个**缩放形式**是推导 ADMM 迭代步骤的出发点 [@problem_id:3438197]。

#### 共识 ADMM 算法

[ADMM](@entry_id:163024) 算法通过[交替最小化](@entry_id:198823)增广拉格朗日函数来求解问题，其变量被分为两个（或多个）块。在[共识问题](@entry_id:637652)中，我们将局部变量 $\{x_i\}$ 作为一个块，全局变量 $v$ 作为另一个块。在第 $k+1$ 次迭代中，算法执行以下三个步骤：

1.  **$x$-更新（局部变量更新）**：固定 $v=v^k$ 和 $\{u_i\}=\{u_i^k\}$，关于 $\{x_i\}$ 最小化 $\mathcal{L}_\rho$。由于目标函数关于各个 $x_i$ 是可分的，这个联合最小化可以分解为 $N$ 个独立的、可并行的子问题：
    $$
    x_i^{k+1} \in \arg\min_{x_i} \left( f_i(x_i) + \frac{\rho}{2} \|x_i - v^k + u_i^k\|_2^2 \right), \quad \text{for } i=1, \dots, N.
    $$
    这个更新步骤具有一种特殊结构，我们将在后续小节中详细阐述，它与**[近端算子](@entry_id:635396)**密切相关 [@problem_id:3438208, 3438239]。

2.  **$v$-更新（全局变量更新）**：固定 $\{x_i\}=\{x_i^{k+1}\}$ 和 $\{u_i\}=\{u_i^k\}$，关于 $v$ 最小化 $\mathcal{L}_\rho$。此时，我们求解：
    $$
    v^{k+1} = \arg\min_v \sum_{i=1}^N \frac{\rho}{2} \|x_i^{k+1} - v + u_i^k\|_2^2 = \arg\min_v \sum_{i=1}^N \|v - (x_i^{k+1} + u_i^k)\|_2^2.
    $$
    这是一个标准的[最小二乘问题](@entry_id:164198)，其解是各个点 $(x_i^{k+1} + u_i^k)$ 的[算术平均值](@entry_id:165355)。通过对 $v$ 求导并令其为零，我们得到全局变量的更新规则，这是一个**平均步骤** [@problem_id:3438197, 3438239]：
    $$
    v^{k+1} = \frac{1}{N} \sum_{i=1}^N (x_i^{k+1} + u_i^k).
    $$

3.  **$u$-更新（对偶变量更新）**：最后，我们使用标准的对偶上升步骤来更新缩放[对偶变量](@entry_id:143282)。更新规则是当前对偶变量加上当前迭代的**原始残差**（primal residual）$r_i^{k+1} = x_i^{k+1} - v^{k+1}$：
    $$
    u_i^{k+1} = u_i^k + x_i^{k+1} - v^{k+1}.
    $$
    值得注意的是，[ADMM](@entry_id:163024) 在迭代过程中并不严格强制 $x_i = v$。相反，共识是作为算法收敛的**[渐近性质](@entry_id:177569)**实现的，即当 $k \to \infty$ 时，原始残差 $x_i^k - v^k$ 趋向于零 [@problem_id:3438208]。

### 共享 ADMM

第二种重要的变体是**共享问题**，它出现在多个局部变量通过一个耦合项（通常是一个正则化项或一个共享的约束）相互关联的场景中。

#### 问题表述与[解耦](@entry_id:637294)

假设有 $N$ 个局部变量 $x_i \in \mathbb{R}^{n_i}$，它们通过一个共同的函数 $g$ 耦合。问题的一般形式为：
$$
\min_{\{x_i\}} \sum_{i=1}^{N} f_i(x_i) + g\left(\sum_{i=1}^{N} H_i x_i\right),
$$
其中 $f_i$ 是局部[凸函数](@entry_id:143075)，$H_i$ 是线性映射，$g$ 是耦合的[凸函数](@entry_id:143075)。这种结构中的难点在于 $g$ 函数的参数是所有 $x_i$ 的和，这使得问题不可分。

[ADMM](@entry_id:163024) 的一个巧妙技巧是通过引入一个辅助变量 $z \in \mathbb{R}^p$ 来**[解耦](@entry_id:637294)**（decouple）这个问题。我们令 $z = \sum_{i=1}^N H_i x_i$，从而将原问题转化为等价的约束形式：
$$
\min_{\{x_i\}, z} \sum_{i=1}^{N} f_i(x_i) + g(z) \quad \text{subject to} \quad \sum_{i=1}^{N} H_i x_i - z = 0.
$$
现在，[目标函数](@entry_id:267263)是可分的（一部分只依赖于 $\{x_i\}$，另一部分只依赖于 $z$），代价是引入了一个线性耦合约束 [@problem_id:3438199]。

#### 共享 ADMM 算法

我们对转化后的问题应用 ADMM。这里的变量块是 $\{x_i\}$ 和 $z$。

1.  **增广[拉格朗日函数](@entry_id:174593)**：对于单个耦合约束，我们引入一个对偶变量 $y \in \mathbb{R}^p$（或其缩放版本 $u = y/\rho$）。增广拉格朗日函数为：
    $$
    \mathcal{L}_\rho(\{x_i\}, z, y) = \sum_{i=1}^{N} f_i(x_i) + g(z) + y^\top\left(\sum_{i=1}^{N} H_i x_i - z\right) + \frac{\rho}{2}\left\| \sum_{i=1}^{N} H_i x_i - z \right\|_2^2.
    $$
    需要注意的是，惩罚项作用于整个和的残差，而不是每个 $H_i x_i - z$ [@problem_id:3438199]。

2.  **ADMM 迭代**：
    *   **$x$-更新**：固定 $z=z^k$ 和 $u=u^k$，求解关于 $\{x_i\}$ 的子问题。
        $$
        \{x_i^{k+1}\} \in \arg\min_{\{x_i\}} \left\{ \sum_{i=1}^{N} f_i(x_i) + \frac{\rho}{2}\left\| \sum_{i=1}^{N} H_i x_i - z^k + u^k \right\|_2^2 \right\}.
        $$
        这个子问题通常是耦合的，因为二次项中存在交叉项 $x_i^\top H_i^\top H_j x_j$。可以采用并行（Jacobi）或序贯（Gauss-Seidel）更新方式来近似求解，或者在某些特殊情况下，它可能有一个[闭式](@entry_id:271343)解 [@problem_id:3438244]。

    *   **$z$-更新**：固定 $\{x_i\}=\{x_i^{k+1}\}$ 和 $u=u^k$，求解关于 $z$ 的子问题。
        $$
        z^{k+1} \in \arg\min_{z} \left\{ g(z) + \frac{\rho}{2}\left\| \sum_{i=1}^{N} H_i x_i^{k+1} - z + u^k \right\|_2^2 \right\}.
        $$
        这个更新步骤通常可以表示为一个**[近端算子](@entry_id:635396)**的求值，我们将在下一节中看到 [@problem_id:3438199]。

    *   **$u$-更新**：对偶更新规则与共识 [ADMM](@entry_id:163024) 类似，即累加当前的原始残差：
        $$
        u^{k+1} = u^k + \sum_{i=1}^{N} H_i x_i^{k+1} - z^{k+1}.
        $$

通过引入辅助变量 $z$，共享 ADMM 成功地将复杂的耦合项 $g$ 从 $\{x_i\}$ 中分离出来，使得 $z$ 的更新可以独立进行，这正是 ADMM 强大功能的核心体现 [@problem_id:3438199]。

### [近端算子](@entry_id:635396)在 [ADMM](@entry_id:163024) 中的核心作用

[ADMM](@entry_id:163024) 算法的许多子问题都可以优雅地用**[近端算子](@entry_id:635396)**（proximal operator）来表达。这一概念是现代凸优化理论的基石。

#### 定义与性质

对于一个正常、闭、[凸函数](@entry_id:143075) $h: \mathbb{R}^p \to \mathbb{R} \cup \{+\infty\}$ 和一个参数 $\gamma > 0$，其[近端算子](@entry_id:635396) $\mathrm{prox}_{\gamma h}$ 定义为 [@problem_id:3438194, 3438239]：
$$
\mathrm{prox}_{\gamma h}(v) = \arg\min_{x \in \mathbb{R}^p} \left\{ \gamma h(x) + \frac{1}{2} \|x - v\|_2^2 \right\}.
$$
这个算子接受一个点 $v$，并返回一个点 $x$，该点是原函数 $h(x)$ 的值与到 $v$ 的二次距离之间的一个折衷。当 $h$ 是一个集合的指示函数时，[近端算子](@entry_id:635396)就简化为到该集合的**欧氏投影**（Euclidean projection）。例如，如果 $g$ 是一个[凸集](@entry_id:155617) $C$ 的[指示函数](@entry_id:186820)（即 $z \in C$ 时 $g(z)=0$，否则 $g(z)=+\infty$），那么共享 [ADMM](@entry_id:163024) 中的 $z$-更新就变成了一个投影操作 [@problem_id:3438199]：
$$
z^{k+1} = \Pi_{C}\left(\sum_{i=1}^{N} H_i x_i^{k+1} + u^k\right).
$$

#### 在 [ADMM](@entry_id:163024) 更新中的应用

现在我们可以重新审视 [ADMM](@entry_id:163024) 的更新步骤：

*   在**共识 ADMM** 中，局部 $x_i$-更新可以写成 [@problem_id:3438239]：
    $$
    x_i^{k+1} = \arg\min_{x_i} \left\{ \frac{1}{\rho} f_i(x_i) + \frac{1}{2} \|x_i - (v^k - u_i^k)\|_2^2 \right\} = \mathrm{prox}_{\frac{1}{\rho}f_i}(v^k - u_i^k).
    $$
*   在**共享 ADMM** 中，$z$-更新可以写成 [@problem_id:3438244]：
    $$
    z^{k+1} = \arg\min_{z} \left\{ \frac{1}{\rho}g(z) + \frac{1}{2} \left\| z - \left(\sum_{i=1}^{N} H_i x_i^{k+1} + u^k\right) \right\|_2^2 \right\} = \mathrm{prox}_{g/\rho}\left( \sum_{i=1}^{N} H_i x_i^{k+1} + u^{k} \right).
    $$

这种表达方式不仅简洁，而且揭示了 [ADMM](@entry_id:163024) 的模块化结构。对于许多在[稀疏优化](@entry_id:166698)和机器学习中常见的函数，其[近端算子](@entry_id:635396)都有高效的解析解或[数值算法](@entry_id:752770)。

*   **$\ell_1$ 范数与[软阈值](@entry_id:635249)**：当正则化项为 $\ell_1$ 范数 $h(x) = \lambda \|x\|_1$ 时，其[近端算子](@entry_id:635396)是**[软阈值算子](@entry_id:755010)**（soft-thresholding operator），它将输入向量的每个分量向零收缩一个固定的量 $\lambda$。这与硬阈值（hard-thresholding）不同，后者直接将小于阈值的分量设为零 [@problem_id:3438194]。例如，在 `problem_id:3438244` 的具体算例中，$g(z)=\lambda|z|$ 的[近端算子](@entry_id:635396)求值就是[软阈值](@entry_id:635249)操作。

*   **[组套索](@entry_id:170889)与[块软阈值](@entry_id:746891)**：当使用[组套索](@entry_id:170889)（group lasso）惩罚 $\phi(z) = \sum_{g \in \mathcal{G}} \|z_g\|_2$ 时，[近端算子](@entry_id:635396)可以按组分解，并对每个组 $z_g$ 应用**[块软阈值](@entry_id:746891)**（block soft-thresholding）。如果一个组的范数 $\|v_g\|_2$ 小于阈值，整个组的向量将被设为零；否则，该组向量将被整体缩放，使其范数减小 [@problem_id:3438194]。

### 实际实现与诊断

在实际部署 ADMM 算法时，必须考虑如何判断算法是否收敛以及如何处理潜在的问题。

#### [停止准则](@entry_id:136282)

ADMM 的收敛通常通过监控**原始残差**（primal residual）和**对偶残差**（dual residual）的范数来判断。这些残差衡量了算法离满足原始可行性（共识）和对偶可行性（[最优性条件](@entry_id:634091)的一部分）的距离。

对于共识 ADMM，在第 $k$ 次迭[代时](@entry_id:173412)：
*   **原始残差** $r^k$ 衡量了局部变量与全局变量之间的不一致性：
    $$
    r^k = \begin{pmatrix} x_1^k - v^k \\ \vdots \\ x_N^k - v^k \end{pmatrix} \in \mathbb{R}^{Nn}.
    $$
*   **对偶残差** $s^k$ 与[最优性条件](@entry_id:634091)的平稳性有关，可以方便地通过全局变量的变化来衡量：
    $$
    s^k = \rho (v^k - v^{k-1}) \in \mathbb{R}^{n}.
    $$
理想的[停止准则](@entry_id:136282)是当这两个残差的范数都足够小时，即 $\|r^k\|_2 \leq \varepsilon_{\mathrm{pri}}$ 和 $\|s^k\|_2 \leq \varepsilon_{\mathrm{dual}}$。为了使阈值 $\varepsilon_{\mathrm{pri}}$ 和 $\varepsilon_{\mathrm{dual}}$ 不受问题规模和变量尺度的影响，通常会将它们设置为一个绝对容忍度 $\varepsilon_{\mathrm{abs}}$ 和一个相对容忍度 $\varepsilon_{\mathrm{rel}}$ 的组合。一个好的实践是 [@problem_id:3438236]：
$$
\varepsilon_{\mathrm{pri}} = \sqrt{Nn}\,\varepsilon_{\mathrm{abs}} + \varepsilon_{\mathrm{rel}} \max\left\{ \|X^k\|_2,\; \sqrt{N}\,\|v^k\|_2 \right\}
$$
$$
\varepsilon_{\mathrm{dual}} = \sqrt{n}\,\varepsilon_{\mathrm{abs}} + \varepsilon_{\mathrm{rel}}\|\rho U^k\|_2 \quad (\text{其中 } U^k \text{ 是对偶变量的堆叠})
$$
这些准则中的 $\sqrt{Nn}$ 和 $\sqrt{n}$ 因子考虑了残差向量的维度，而相对项则根据迭代过程中变量的范数进行调整。

#### [不可行问题](@entry_id:635482)的诊断

当 [ADMM](@entry_id:163024) 应用于一个**不可行**（infeasible）问题时，例如，由于模型错误或测量不一致，导致共识约束无法满足（如 $\bigcap_i C_i = \emptyset$），算法不会收敛到一个可行解。然而，其残差的行为可以作为诊断这种[不可行性](@entry_id:164663)的有力工具 [@problem_id:3438207]。

在这种情况下，典型的行为是：
*   **原始[残差范数](@entry_id:754273) $\|r^k\|_2$ 不会收敛到零**。它可能会收敛到一个严格为正的常数或在一个非零[极限环](@entry_id:274544)中[振荡](@entry_id:267781)。这直接表明共识无法达成。
*   **对偶[残差范数](@entry_id:754273) $\|s^k\|_2$ 仍然可能收敛到零**。这通常发生在全局变量 $v^k$ 稳定下来时。
*   **对偶变量 $\|u_i^k\|$ 通常会发散到无穷大**。

因此，观测到非零的原始残差和趋于零的对偶残差的组合，是 ADMM 算法给出的一个强有力的**[不可行性证书](@entry_id:635369)**（certificate of infeasibility）。这表明原问题的约束条件本身是不相容的 [@problem_id:3438207]。

### 理论基础与收敛性

最后，我们探讨 ADMM 的一些更深层次的理论性质，包括其收敛保证的范围和收敛速度的决定因素。

#### 收敛保证与多块 ADMM 的陷阱

ADMM 的一个美妙之处在于其对**两块**（two-block）凸问题的强大收敛保证。我们讨论的共识 [ADMM](@entry_id:163024)（分组为 $\{x_i\}$ 和 $v$）和共享 [ADMM](@entry_id:163024)（分组为 $\{x_i\}$ 和 $z$）都属于这种两块结构，因此在非常温和的条件下，它们都被证明是收敛的。

然而，一个常见的误区是认为这种收敛性可以被直接推广到三个或更多块的变量。当我们天真地将 [ADMM](@entry_id:163024) 扩展为按序更新三个或更多块（所谓的**直接多块 [ADMM](@entry_id:163024)** 或 **Gauss-Seidel [ADMM](@entry_id:163024)**）时，即使对于简单的凸问题，算法也**不保证收敛**。存在已知的反例，表明对于 $p \ge 3$ 个块，这种直接扩展可能会发散 [@problem_id:3438191]。

例如，在[共识问题](@entry_id:637652)中，如果我们将每个 $u_i$ 和 $x$ 都视为独立的块，进行 $(p+1)$-块的序贯更新，并且函数 $f$ 包含 $u_i$ 之间的耦合项（即 $f$ 不可分），那么这个算法就可能发散。与之相对，将所有 $u_i$ 分组为一个大块，从而保持两块结构，则可以保证收敛。只有当 $f$ 是可分的（$f(u_1, \dots, u_p) = \sum f_i(u_i)$）时，多块序贯更新才恰好等价于分组的并行更新，从而继承了两块 ADMM 的收敛性。

为了修复多块 ADMM 的收敛性问题，一种常见的策略是引入**近端正则化**（proximal regularization），即在每次更新时，在最小化目标中加入一个惩罚项，如 $\frac{\tau}{2}\|u_i - u_i^k\|_2^2$。只要[正则化参数](@entry_id:162917) $\tau$ 足够大，这种**近端 ADMM** 就可以恢复对多块凸问题的收敛保证 [@problem_id:3438191]。

#### [收敛速度](@entry_id:636873)与图[拉普拉斯谱](@entry_id:275024)

对于收敛的 [ADMM](@entry_id:163024) 算法，其收敛速度是一个关键的性能指标。在共识 [ADMM](@entry_id:163024) 中，[收敛速度](@entry_id:636873)与代理之间信息交换的拓扑结构密切相关。这种结构可以用一个图来表示，其中节点是代理，边表示它们之间的直接通信或约束。

对于一个定义在图上的二次[共识问题](@entry_id:637652)，可以证明 [ADMM](@entry_id:163024) 的[收敛速度](@entry_id:636873)由图的**拉普拉斯矩阵**（Graph Laplacian）$L$ 的谱特性决定。具体来说，最慢收敛的“不一致模式”的收敛因子由 $L$ 的**谱隙**（spectral gap），即其第二小的[特征值](@entry_id:154894) $\lambda_2(L)$，所控制。

分析表明，每个与正[特征值](@entry_id:154894) $\lambda > 0$ 相关的“不一致模式”在每次迭代中以因子 $\frac{\alpha}{\alpha+\rho\lambda}$ 收缩（其中 $\alpha$ 和 $\rho$ 是问题参数）。最坏情况下的收缩因子（决定整体[收敛速度](@entry_id:636873)）对应于最小的正[特征值](@entry_id:154894) $\lambda_2(L)$。因此，[收敛速度](@entry_id:636873)的界为 $\frac{\alpha}{\alpha+\rho\lambda_2(L)}$ [@problem_id:3438219]。

这个结果的直观含义是：**一个更大的[谱隙](@entry_id:144877) $\lambda_2(L)$ 意味着图的连通性更好，信息在网络中传播得更快，从而导致 [ADMM](@entry_id:163024) 更快地达成共识**。

#### 与[算子分裂](@entry_id:634210)方法的关系

ADMM 可以被视为更广泛的**[算子分裂](@entry_id:634210)**（operator splitting）方法家族的一员。从这个更抽象的视角看，[优化问题](@entry_id:266749) $\min F(y) + G(y)$ 的[最优性条件](@entry_id:634091)是 $0 \in \partial F(y^\star) + \partial G(y^\star)$，这是一个**[单调算子](@entry_id:637459)包含**（monotone operator inclusion）问题。

[ADMM](@entry_id:163024) 实际上是应用于对偶问题的 **Douglas-Rachford 分裂**（Douglas-Rachford splitting）算法。对于原始问题，[ADMM](@entry_id:163024) 的[不动点方程](@entry_id:203270)与[最优性条件](@entry_id:634091)紧密相关。以[共识问题](@entry_id:637652)为例，其中 $G(y) = \iota_{\mathcal{C}}(y)$ 是共识[子空间](@entry_id:150286)的指示函数，[最优性条件](@entry_id:634091)为 $0 \in \partial F(y^\star) + N_{\mathcal{C}}(y^\star)$，其中 $N_{\mathcal{C}}$ 是[法锥](@entry_id:272387)算子。

通过分析 Douglas-Rachford 算子的[不动点方程](@entry_id:203270)，我们可以推导出 [ADMM](@entry_id:163024) 的收敛点必须满足**原始可行性**（$y^\star \in \mathcal{C}$）和**对偶最优性**（对偶变量满足的关系，如 $\sum \mu_{x_i}^\star + \mu_v^\star = 0$）。这种方法提供了一条从根本上理解 [ADMM](@entry_id:163024) 为何能找到最优解的路径，并且可以直接用于求解某些问题的最优解，如 `problem_id:3438202` 中所示的二次[共识问题](@entry_id:637652)，其最优解可以通过求解这些[最优性条件](@entry_id:634091)组成的[线性系统](@entry_id:147850)得到。