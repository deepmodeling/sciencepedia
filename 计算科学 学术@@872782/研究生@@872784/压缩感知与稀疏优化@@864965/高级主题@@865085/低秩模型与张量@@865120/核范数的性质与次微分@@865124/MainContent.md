## 引言
在现代数据科学、机器学习和信号处理领域，处理[高维数据](@entry_id:138874)中固有的低秩结构是一个核心挑战。[核范数](@entry_id:195543)作为[矩阵秩](@entry_id:153017)的有效凸代理，已成为解决此类问题的基石，尤其在[矩阵补全](@entry_id:172040)、[稳健主成分分析](@entry_id:754394)和[系统辨识](@entry_id:201290)等任务中发挥着不可或替代的作用。然而，尽管其应用广泛，但其成功的深层数学原理，特别是其复杂的[次微分](@entry_id:175641)结构，往往未被充分理解。本文旨在填补这一知识鸿沟，为读者提供一个关于核范数性质及其在优化中作用的系统性视角。

本文将分为三个核心部分，引导读者从理论走向实践。首先，在“原理与机制”一章中，我们将深入探讨核范数的[凸分析](@entry_id:273238)性质、与[谱范数](@entry_id:143091)的对偶关系，并精确刻画其[次微分](@entry_id:175641)的几何结构，揭示其与矩阵[奇异值](@entry_id:152907)谱的深刻联系。接着，在“应用与跨学科联系”一章中，我们将展示这些抽象原理如何转化为解决现实问题的强大工具，例如在矩阵恢复中构建对偶证书，在稳健PCA中实现信号[解耦](@entry_id:637294)，并连接到量子信息、网络科学等多个前沿领域。最后，“动手实践”部分将提供一系列精心设计的问题，帮助读者将理论知识应用于具体计算和分析中，从而巩固对[核范数](@entry_id:195543)[次微分](@entry_id:175641)的掌握。

## 原理与机制

本章旨在深入探讨核范数的关键数学原理与机制。我们将从其基本[凸分析](@entry_id:273238)性质出发，详细阐述核范数与[谱范数](@entry_id:143091)的对偶关系，并由此揭示其[单位球](@entry_id:142558)的几何结构。核心内容将聚焦于核范数[次微分](@entry_id:175641)的精确刻画，分析其[次微分](@entry_id:175641)结构如何依赖于矩阵的奇异值分解（SVD），并阐释这一结构如何决定了[矩阵秩](@entry_id:153017)的变化对[次微分](@entry_id:175641)集“大小”的影响。最后，我们将这些理论原理与实际应用联系起来，展示[次微分](@entry_id:175641)在求解[核范数最小化](@entry_id:634994)问题中的核心作用，特别是在[近端梯度算法](@entry_id:193462)（如[奇异值](@entry_id:152907)阈值算法）和低秩矩阵恢复的理论保证（如对偶证书）中的应用。

### [核范数](@entry_id:195543)的[凸分析](@entry_id:273238)性质

#### 定义与对偶性

我们首先定义矩阵空间中的**[核范数](@entry_id:195543) (nuclear norm)**。对于任意实矩阵 $X \in \mathbb{R}^{m \times n}$，其[核范数](@entry_id:195543) $\Vert X \Vert_*$ 定义为其所有奇异值 $\sigma_i(X)$ 的和：
$$
\Vert X \Vert_* = \sum_{i=1}^{\min(m,n)} \sigma_i(X)
$$
[核范数](@entry_id:195543)是矩阵奇异值向量的 $\ell_1$ 范数，因此有时也被称为迹范数 (trace norm)。与此密切相关的是**[谱范数](@entry_id:143091) (spectral norm)**，记为 $\Vert X \Vert_2$，它定义为 $X$ 的最大[奇异值](@entry_id:152907)，即 $\Vert X \Vert_2 = \sigma_{\max}(X)$。[谱范数](@entry_id:143091)是矩阵奇异值向量的 $\ell_\infty$ 范数。

这两个范数之间存在着深刻的**对偶关系 (duality)**。在配备了[弗罗贝尼乌斯内积](@entry_id:153693)（Frobenius inner product）$\langle A, B \rangle = \operatorname{tr}(A^\top B)$ 的矩阵空间中，[核范数](@entry_id:195543)与[谱范数](@entry_id:143091)互为[对偶范数](@entry_id:200340)。这意味着：
$$
\Vert X \Vert_* = \sup_{\Vert Z \Vert_2 \le 1} \langle Z, X \rangle \quad \text{且} \quad \Vert X \Vert_2 = \sup_{\Vert Z \Vert_* \le 1} \langle Z, X \rangle
$$
我们可以通过[冯·诺依曼迹不等式](@entry_id:188204) (von Neumann's trace inequality) 来验证第一部分。该不等式指出，对于任意两个矩阵 $Z, X \in \mathbb{R}^{m \times n}$，有 $\operatorname{tr}(Z^\top X) \le \sum_i \sigma_i(Z) \sigma_i(X)$。因此，对于任意满足 $\Vert Z \Vert_2 \le 1$ 的矩阵 $Z$，我们有：
$$
\langle Z, X \rangle \le \sum_i \sigma_i(Z) \sigma_i(X) \le \sigma_{\max}(Z) \sum_i \sigma_i(X) = \Vert Z \Vert_2 \Vert X \Vert_* \le \Vert X \Vert_*
$$
为了证明这个[上界](@entry_id:274738)是可以达到的，我们只需构造一个特定的 $Z$。假设 $X$ 的[奇异值分解](@entry_id:138057)为 $X = U \Sigma V^\top$。令 $Z_0 = U V^\top$（这里我们假设 $X$ 是方阵，或者通过[零填充](@entry_id:637925)使其成为方阵的极因子）。$Z_0$ 是一个[部分等距](@entry_id:268371)矩阵，其奇异值均为 $1$，因此 $\Vert Z_0 \Vert_2 = 1$。计算[内积](@entry_id:158127)可得：
$$
\langle Z_0, X \rangle = \operatorname{tr}((U V^\top)^\top U \Sigma V^\top) = \operatorname{tr}(V U^\top U \Sigma V^\top) = \operatorname{tr}(V \Sigma V^\top) = \operatorname{tr}(\Sigma) = \sum_i \sigma_i(X) = \Vert X \Vert_*
$$
这证明了核范数与[谱范数](@entry_id:143091)之间的对偶关系 [@problem_id:3469338]。

#### [核范数](@entry_id:195543)单位球的几何结构

范数的几何性质可以通过其[单位球](@entry_id:142558)来直观理解。核范数[单位球](@entry_id:142558)定义为 $B_* = \{ X \in \mathbb{R}^{m \times n} : \Vert X \Vert_* \le 1 \}$，[谱范数](@entry_id:143091)单位球定义为 $B_2 = \{ Y \in \mathbb{R}^{m \times n} : \Vert Y \Vert_2 \le 1 \}$。

一个直接的性质是 **中心对称性 (central symmetry)**。由于矩阵 $X$ 和 $-X$ 的奇异值相同（因为 $(-X)^\top(-X) = X^\top X$），它们的核范数也必然相等，即 $\Vert X \Vert_* = \Vert -X \Vert_*$。因此，如果 $X \in B_*$，那么 $-X$ 也必定在 $B_*$ 中，这意味着 $B_*$ 是[中心对称](@entry_id:144242)的 [@problem_id:3469338]。

对偶关系在几何上体现为**[极集](@entry_id:193237) (polar set)** 的概念。一个包含原点的闭[凸集](@entry_id:155617) $K$ 的[极集](@entry_id:193237)定义为 $K^\circ = \{ Y : \sup_{X \in K} \langle Y, X \rangle \le 1 \}$。根据[对偶范数](@entry_id:200340)的定义，一个范数单位球的[极集](@entry_id:193237)正是其[对偶范数](@entry_id:200340)的[单位球](@entry_id:142558)。因此，我们立即得到 $B_*^\circ = B_2$ 以及 $B_2^\circ = B_*$。更进一步地，根据**双极定理 (Bipolar Theorem)**，对于任何包含原点的闭凸集 $K$，我们有 $(K^\circ)^\circ = K$。由于 $B_*$ 本身就是一个包含原点的闭[凸集](@entry_id:155617)，所以 $(B_*^\circ)^\circ = B_*$ 成立 [@problem_id:3469338]。

单位球的**极点 (extreme points)** 揭示了范数鼓励的结构类型。一个[凸集](@entry_id:155617)的极点是不能被该集合中任何两个不同点的非平凡凸组合表示的点。对于核范数[单位球](@entry_id:142558) $B_*$ 而言，其极点恰好是所有秩为1且[谱范数](@entry_id:143091)为1（等价于[核范数](@entry_id:195543)为1）的矩阵 [@problem_id:3469338]。任何秩大于等于2的矩阵 $X$（即使 $\Vert X \Vert_* = 1$），总可以被分解为两个或多个秩1矩阵的加权和，这意味着它可以表示为球内其他点的[凸组合](@entry_id:635830)，因此不是极点。例如，若 $X = \sum_{i=1}^r \sigma_i u_i v_i^\top$ 且 $\Vert X \Vert_* = \sum \sigma_i = 1$，只要 $r \ge 2$，我们就可以将其写成 $X = \sigma_1 (u_1 v_1^\top) + (1-\sigma_1) (\frac{\sum_{i=2}^r \sigma_i u_i v_i^\top}{1-\sigma_1})$，这是两个单位球内不同点的凸组合。这个性质从几何上解释了为什么[核范数最小化](@entry_id:634994)能够有效地促进解的低秩性：它倾向于将解“推向”[单位球](@entry_id:142558)的极点，即秩1矩阵。

### 凸性与[次微分](@entry_id:175641)

#### 凸性而非[严格凸性](@entry_id:193965)

作为一种范数，核范数是[凸函数](@entry_id:143075)。然而，一个至关重要的性质是，它**不是严格凸 (strictly convex)** 的。[严格凸性](@entry_id:193965)要求对于任意两个不同的点 $X, Y$ 和任意 $t \in (0,1)$，不等式 $\Vert tX + (1-t)Y \Vert_*  t \Vert X \Vert_* + (1-t) \Vert Y \Vert_*$ 严格成立。

核范数不满足此性质，我们可以构造出反例。一个关键的构造思路是利用核范数的[酉不变性](@entry_id:198984)。考虑两个不同的正定(PSD)矩阵 $X$ 和 $Y$，它们具有相同的[奇异值](@entry_id:152907)（即[特征值](@entry_id:154894)）。例如，在 $\mathbb{R}^{3 \times 3}$ 中，令 $X = \operatorname{diag}(4, 2, 1)$。它的奇异值是 $\{4, 2, 1\}$，核范数为 $7$。对于PSD矩阵，[核范数](@entry_id:195543)等于其迹，$\Vert X \Vert_* = \operatorname{trace}(X) = 7$。现在，选取一个非单位阵的[旋转矩阵](@entry_id:140302) $R$，例如一个在 $(e_1, e_2)$ 平面旋转的矩阵，并定义 $Y = RXR^\top$。由于 $X$ 的奇异值不全相等，所以 $Y \neq X$。根据[酉不变性](@entry_id:198984)， $Y$ 的[奇异值](@entry_id:152907)与 $X$ 相同，因此 $\Vert Y \Vert_* = 7$。同时，$\operatorname{trace}(Y) = \operatorname{trace}(RXR^\top) = \operatorname{trace}(X) = 7$。现在考虑它们的中点 $M = \frac{X+Y}{2}$。由于 $X$ 和 $Y$ 都是PSD的，它们的和及中点也是PSD的。因此，我们可以再次使用迹来计算其[核范数](@entry_id:195543)：
$$
\Big\Vert\frac{X+Y}{2}\Big\Vert_* = \operatorname{trace}\Big(\frac{X+Y}{2}\Big) = \frac{\operatorname{trace}(X) + \operatorname{trace}(Y)}{2} = \frac{7+7}{2} = 7
$$
我们找到了两个不同的点 $X, Y$ 使得 $\Vert \frac{X+Y}{2} \Vert_* = \frac{1}{2}\Vert X \Vert_* + \frac{1}{2}\Vert Y \Vert_*$，这证明了核范数不是严格凸的 [@problem_id:3469335]。这个现象的几何意义是，核范数[单位球](@entry_id:142558)的边界上存在“平面区域” (flat faces)。连接 $X$ 和 $Y$ 的线段（经过适当缩放后）就位于这样的平面区域上。

#### [次微分](@entry_id:175641)的精确刻画

函数在某点不是严格凸或不可微，这使得我们需要使用**[次微分](@entry_id:175641) (subdifferential)** 的概念来分析其性质。一个凸函数 $f$ 在点 $X$ 的[次微分](@entry_id:175641) $\partial f(X)$ 是所有**次梯度 (subgradient)** $G$ 的集合，其中每个次梯度都满足以下不等式：
$$
f(Z) \ge f(X) + \langle G, Z - X \rangle \quad \text{for all } Z
$$
对于范数函数，其[次微分](@entry_id:175641)与其[对偶范数](@entry_id:200340)紧密相关。利用我们之前建立的对偶关系，可以证明核范数在非零点 $X$ 的[次微分](@entry_id:175641)由以下集合给出 [@problem_id:3469338]：
$$
\partial \Vert X \Vert_* = \{ G \in \mathbb{R}^{m \times n} : \Vert G \Vert_2 \le 1, \langle G, X \rangle = \Vert X \Vert_* \}
$$
值得注意的是，这个集合对于 $X \neq 0$ 并不是[中心对称](@entry_id:144242)的。如果 $G \in \partial \Vert X \Vert_*$，那么 $\langle G, X \rangle = \Vert X \Vert_* > 0$。而对于 $-G$，我们有 $\langle -G, X \rangle = -\Vert X \Vert_* \neq \Vert X \Vert_*$，因此 $-G$ 不在 $\partial \Vert X \Vert_*$ 中 [@problem_id:3469338]。

为了得到一个更具体、更具操作性的表达式，我们可以利用 $X$ 的[奇异值分解](@entry_id:138057)。令 $X$ 的秩为 $r$，其紧[奇异值分解](@entry_id:138057)为 $X = U_r \Sigma_r V_r^\top$，其中 $U_r \in \mathbb{R}^{m \times r}$ 和 $V_r \in \mathbb{R}^{n \times r}$ 分别是包含前 $r$ 个左、[右奇异向量](@entry_id:754365)的矩阵。通过细致的推导，可以证明[次微分](@entry_id:175641)具有如下精确形式 [@problem_id:3469347]：
$$
\partial \Vert X \Vert_* = \{ U_r V_r^\top + W \mid U_r^\top W = 0, W V_r = 0, \Vert W \Vert_2 \le 1 \}
$$
这个表达式揭示了[次梯度](@entry_id:142710)的深刻结构。任何一个次梯度 $G$ 都可以分解为两个正交的部分：
1.  **极因子部分** $U_r V_r^\top$：这个部分由 $X$ 的奇异[向量[子空](@entry_id:151815)间](@entry_id:150286)唯一确定，它是一个[部分等距](@entry_id:268371)算子，将 $X$ 的行空间 $\operatorname{span}(V_r)$ 等距地映射到 $X$ 的[列空间](@entry_id:156444) $\operatorname{span}(U_r)$。
2.  **法向部分** $W$：这个矩阵 $W$ 必须满足两个正交性约束 $U_r^\top W = 0$ 和 $W V_r = 0$。这两个约束意味着 $W$ 的[列空间](@entry_id:156444)必须与 $U_r$ 的[列空间](@entry_id:156444)正交，且 $W$ 的行空间必须与 $V_r$ 的行空间正交。此外，这个法向部分的[谱范数](@entry_id:143091)必须不大于1。

当 $X$ 的所有[奇异值](@entry_id:152907)都非零（即矩阵满秩）时，[核范数](@entry_id:195543)是可微的，此时[次微分](@entry_id:175641)集合是单点集，其中 $W$ 必须为零。而当 $X$ 是[秩亏](@entry_id:754065)的（即存在零[奇异值](@entry_id:152907)）或存在重复的非零[奇异值](@entry_id:152907)时，[次微分](@entry_id:175641)将包含不止一个元素，函数在该点不可微 [@problem_id:3469338]。

#### [次微分](@entry_id:175641)与[奇异值](@entry_id:152907)谱的关系

从[次微分](@entry_id:175641)的表达式中，我们可以观察到一个关键事实：它**仅依赖于 $X$ 的奇异[子空间](@entry_id:150286)（由 $U_r, V_r$ 张成）和秩 $r$，而与具体的非零[奇异值](@entry_id:152907)的大小无关** [@problem_id:3469362]。这意味着，如果我们有两个矩阵 $X_1$ 和 $X_2$，它们拥有相同的秩和相同的奇异[子空间](@entry_id:150286)，即使它们的[奇异值](@entry_id:152907)谱不同（例如，一个谱是 $\{5,3\}$，另一个是 $\{4,4\}$），它们的[次微分](@entry_id:175641)集合 $\partial\Vert X_1\Vert_*$ 和 $\partial\Vert X_2\Vert_*$ 是完全相同的。

这个性质引出了一个有趣的推论：**[次微分](@entry_id:175641)的大小与矩阵的秩成反比关系**。这里的“大小”可以用其仿射维度来衡量。法向部分 $W$ 所在的空间由约束 $U_r^\top W = 0$ 和 $W V_r = 0$ 定义，这是一个维度为 $(m-r)(n-r)$ 的[线性空间](@entry_id:151108)。[次微分](@entry_id:175641)集合 $\partial \Vert X \Vert_*$ 的仿射维度即为这个值 [@problem_id:3469343]。

当一个矩阵的秩 $r$ 降低时，例如从 $r$ 降到 $s  r$，张成奇异[子空间的基](@entry_id:160685) $U_s, V_s$ 的列数减少，施加在 $W$ 上的正交约束也随之减弱。这使得满足条件的 $W$ 的集合变得更大。因此，**[矩阵的秩](@entry_id:155507)越低，其[核范数的次微分](@entry_id:755596)集合就越大**，函数在该点的“不可微程度”就越高。例如，秩从 $r$ 降到 $s$ 后，[次微分](@entry_id:175641)集合的仿射维度从 $(m-r)(n-r)$ 增加到 $(m-s)(n-s)$ [@problem_id:3469362]。

### [次微分](@entry_id:175641)在优化与恢复中的应用

[次微分](@entry_id:175641)不仅是一个理论概念，它在与核范数相关的优化算法和恢复理论中扮演着核心角色。

#### [近端算子](@entry_id:635396)：[奇异值](@entry_id:152907)阈值算法

许多现代[优化算法](@entry_id:147840)，特别是用于求解非光滑凸[优化问题](@entry_id:266749)的算法，都依赖于**[近端算子](@entry_id:635396) (proximal operator)**。对于核范数，其[近端算子](@entry_id:635396)定义为以下[优化问题](@entry_id:266749)的解：
$$
\operatorname{prox}_{\lambda \Vert\cdot\Vert_*}(X) \coloneqq \arg\min_{Y \in \mathbb{R}^{m \times n}} \left\{ \lambda \Vert Y \Vert_* + \frac{1}{2} \Vert Y - X \Vert_F^2 \right\}
$$
这个问题有一个优美的解析解，可以通过[次微分](@entry_id:175641)的[一阶最优性条件](@entry_id:634945) $0 \in \partial (\lambda \Vert Y \Vert_* + \frac{1}{2} \Vert Y - X \Vert_F^2)$ 来导出。令 $Y^*$ 为最优解，则[最优性条件](@entry_id:634091)为：
$$
0 \in \lambda \partial \Vert Y^* \Vert_* + (Y^* - X) \quad \implies \quad X - Y^* \in \lambda \partial \Vert Y^* \Vert_*
$$
通过利用范数的[酉不变性](@entry_id:198984)，可以证明最优解 $Y^*$ 必须与输入矩阵 $X$ 共享相同的[奇异向量](@entry_id:143538)。如果 $X = U \Sigma V^\top$，那么 $Y^* = U \Sigma' V^\top$，其中 $\Sigma'$ 是[对角矩阵](@entry_id:637782)。问题随之分解为对[奇异值](@entry_id:152907)的一系列独立的标量[优化问题](@entry_id:266749)。对每个奇异值 $\sigma_i(X)$，我们求解 $\min_{y_i \ge 0} \{ \lambda y_i + \frac{1}{2}(y_i - \sigma_i(X))^2 \}$，其解是**[软阈值](@entry_id:635249) (soft-thresholding)** 操作：$y_i^* = \max(0, \sigma_i(X) - \lambda)$。

因此，核范数的[近端算子](@entry_id:635396)就是著名的**奇异值阈值 (Singular Value Thresholding, SVT)** 算子 [@problem_id:3469325]：
$$
\operatorname{prox}_{\lambda \Vert\cdot\Vert_*}(X) = U \cdot \operatorname{diag}\big((\sigma_i(X) - \lambda)_+\big) \cdot V^\top
$$
这个算子通过对输入矩阵的奇异值进行[软阈值](@entry_id:635249)处理来实现，它是[迭代软阈值算法](@entry_id:750899)（ISTA）及其加速版本（FISTA）等求解[核范数最小化](@entry_id:634994)问题的基石。

#### 对偶证书与[恢复保证](@entry_id:754159)

在低秩矩阵恢复问题（如[矩阵填充](@entry_id:751752)）中，我们希望从不完整的线性测量 $b = \mathcal{A}(X^\star)$ 中恢复出低秩矩阵 $X^\star$。一个标准的[凸松弛](@entry_id:636024)方法是求解以下问题：
$$
\min_{X} \Vert X \Vert_* \quad \text{subject to} \quad \mathcal{A}(X) = b
$$
[次微分](@entry_id:175641)理论为判断 $X^\star$ 是否是上述问题的唯一解提供了判据。根据[凸优化](@entry_id:137441)的[KKT条件](@entry_id:185881)，$X^\star$ 是一个解，当且仅当存在一个**[对偶向量](@entry_id:161217) (dual vector)** $y$，使得 $\mathcal{A}^*(y) \in \partial \Vert X^\star \Vert_*$，其中 $\mathcal{A}^*$ 是测量算子 $\mathcal{A}$ 的[伴随算子](@entry_id:140236)。

要保证 $X^\star$ 是**唯一解**，需要一个更强的条件，这通常被称为**对偶证书 (dual certificate)** 的存在性。一个有效的对偶证书 $Y = \mathcal{A}^*(y)$ 必须满足：
1.  $Y$ 在 $X^\star$ 的奇异[子空间](@entry_id:150286)（[切空间](@entry_id:199137)）上的投影，等于 $X^\star$ 的极因子：$P_T(Y) = U_r V_r^\top$。
2.  $Y$ 在法空间上的投影，其[谱范数](@entry_id:143091)严格小于1：$\Vert P_{T^\perp}(Y) \Vert_2  1$。

这里的切空间 $T$ 和法空间 $T^\perp$ 正是我们在刻画[次微分](@entry_id:175641)时遇到的[子空间](@entry_id:150286)。具体来说，$P_{T^\perp}(Y)$ 就对应于次梯度表达式中的 $W$ 部分。这个严格小于1的条件确保了[次梯度](@entry_id:142710)在法向上的分量没有“饱和”，从而保证了在该方向上的“曲率”，排除了其他可能解的存在。这个条件的鲁棒性，即 $\Vert P_{T^\perp}(Y) \Vert_2$ 离1有多远，决定了恢复算法对噪声的稳健性。如果这个范数越小，恢复就越稳健 [@problem_id:3469337]。

#### [相干性](@entry_id:268953)在[矩阵填充](@entry_id:751752)中的作用

对偶证书的存在性与测量算子 $\mathcal{A}$ 和待恢[复矩阵](@entry_id:190650) $X^\star$ 的奇异[子空间](@entry_id:150286)之间的相互作用密切相关。在[矩阵填充](@entry_id:751752)问题中，$\mathcal{A}$ 是一个 entry-wise 的采样算子，其性质可以用**相干性 (coherence)** 来度量。

[相干性](@entry_id:268953)衡量的是 $X^\star$ 的奇异[子空间](@entry_id:150286)（由 $U_r, V_r$ 张成）与标准[坐标基](@entry_id:270149)（即采样基）的对齐程度。**低[相干性](@entry_id:268953)（或称非相干性）**意味着奇异[子空间](@entry_id:150286)的能量均匀地[分布](@entry_id:182848)在所有坐标轴上，而不是集中在少数几个上。

低相干性是成功恢复的关键。从几何上看，低[相干性](@entry_id:268953)保证了[切空间](@entry_id:199137) $T$ 与采样所依赖的坐标[子空间](@entry_id:150286)之间的“角度”足够大。这使得采样算子 $P_\Omega$ 作用在[切空间](@entry_id:199137)上时能够近似地保持等距性，从而保证了可以从采样数据中构造出一个满足条件的对偶证书 $Y$。换言之，低[相干性](@entry_id:268953)使得我们有足够的自由度去寻找一个位于法空间 $T^\perp$ 中的分量 $W = P_{T^\perp}(Y)$，使其[谱范数](@entry_id:143091)严格小于1，从而保证唯一且稳健的恢复 [@problem_id:3469367]。反之，高相干性意味着 $T$ 与某些坐标轴高度对齐，如果采样的条目恰好错过了这些关键位置，信息将无法恢复，对偶证书也将无从构建。

#### 加权[核范数](@entry_id:195543)

最后，值得一提的是，可以通过对奇异值进行加权来推广[核范数](@entry_id:195543)，例如定义 $f_w(X) = \sum_i w_i \sigma_i(X)$。如果权重 $w_i$ 是正的且递减的，这仍然是一个[凸函数](@entry_id:143075)。当[奇异值](@entry_id:152907)互不相同时，其[次微分](@entry_id:175641)（此时为梯度）的形式变为 $U \operatorname{diag}(w) V^\top$ [@problem_id:3469350]。通过设计不同的权重方案，例如给较大的奇异值分配较大的权重，可以实现更精细的正则化效果，例如在惩罚秩的同时，对信号的主要成分保留更多信息。