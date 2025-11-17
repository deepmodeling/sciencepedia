## 引言
在[半单李代数](@entry_id:190073)的宏伟结构中，[根系](@entry_id:198970)如同一副精密的骨架，支撑着整个代数的构造。然而，要真正理解这副骨架的动态运作机制，我们必须深入到其最基本的组成单元——[根串](@entry_id:180284)。[根串](@entry_id:180284)不仅揭示了根与根之间隐藏的几何与代数关系，更是连接[根系](@entry_id:198970)几何与[李代数表示论](@entry_id:190569)的桥梁。本文旨在系统地阐明[根串](@entry_id:180284)的核心理论，解决如何通过[根系](@entry_id:198970)内在属性来确定[代数结构](@entry_id:137052)和表示性质这一基本问题。

本文将引导您完成一次从理论到应用的深度探索。在“原理与机制”一章中，我们将建立[根串](@entry_id:180284)的数学框架，阐明其长度、对称性背后的决定性公式，并揭示其与 $\mathfrak{sl}_2$ 子[代数表示](@entry_id:143783)的深刻[等价关系](@entry_id:138275)。接下来，在“应用与[交叉](@entry_id:147634)学科联系”中，我们将展示[根串](@entry_id:180284)如何在计算[结构常数](@entry_id:157960)、分析[表示分解](@entry_id:139061)、理解代数对称性乃至探索无限维[卡茨-穆迪代数](@entry_id:154948)等前沿领域中发挥关键作用。最后，通过“动手实践”部分的一系列问题，您将有机会亲手应用所学知识，将抽象的理论转化为具体的计算能力。

## 原理与机制

在前一章中，我们介绍了[半单李代数](@entry_id:190073)及其[根系](@entry_id:198970)的基本概念。现在，我们将深入探讨[根系](@entry_id:198970)的一个核心结构特征——**[根串](@entry_id:180284) (root strings)**。[根串](@entry_id:180284)不仅揭示了根之间深刻的几何关系，更重要的是，它们构成了理解整个[李代数表示](@entry_id:196776)理论的基石。本章将系统地阐述[根串](@entry_id:180284)的定义、其长度和对称性的决定性原理，并揭示其与 $\mathfrak{sl}_2(\mathbb{C})$ 子[代数表示](@entry_id:143783)之间的根本联系。

### [根串](@entry_id:180284)的结构

对于一个给定的[根系](@entry_id:198970) $\Phi$，如果我们任意选取两个根 $\alpha$ 和 $\beta$（不必是不同的），一个自然的问题是：从 $\beta$ 开始，沿着 $\alpha$ 的方向，我们还能在[根系](@entry_id:198970) $\Phi$ 中找到哪些其他的根？更形式地说，我们考虑所有形如 $\beta + k\alpha$（其中 $k$ 为整数）的向量集合，并探究其中哪些向量仍然属于 $\Phi$。这个集合被称为**通过 $\beta$ 的 $\alpha$-[根串](@entry_id:180284)**。

[李代数](@entry_id:137954)理论的一个基本定理指出，任何[根串](@entry_id:180284)中的根所对应的整数 $k$ 的集合，总是一个**不间断的整数序列**。也就是说，存在两个非负整数 $p$ 和 $q$，使得通过 $\beta$ 的 $\alpha$-[根串](@entry_id:180284)可以写作：
$$
S_{\beta, \alpha} = \{ \beta + k\alpha \in \Phi \mid k \in \mathbb{Z}, -q \le k \le p \}
$$
这个[根串](@entry_id:180284)的长度，即其中根的个数，为 $p+q+1$。

那么，是什么决定了这两个整数 $p$ 和 $q$ 的值呢？答案蕴含在根系的几何结构之中，具体由一个优美的公式给出：
$$
q - p = \langle \beta, \alpha^\vee \rangle = \frac{2(\beta, \alpha)}{(\alpha, \alpha)}
$$
这里的 $(\cdot, \cdot)$ 是[欧几里得空间](@entry_id:138052)上的[内积](@entry_id:158127)，而 $\alpha^\vee = \frac{2\alpha}{(\alpha, \alpha)}$ 是根 $\alpha$ 对应的**[余根](@entry_id:193338) (coroot)**。表达式 $\langle \beta, \alpha^\vee \rangle$ 是一个整数，称为**嘉当整数 (Cartan integer)**。这个公式是计算[根串](@entry_id:180284)性质的核心工具，它将[根串](@entry_id:180284)的非对称性（由 $q-p$ 度量）与两个根的[内积](@entry_id:158127)联系起来。

值得注意的是，该公式只给出了 $p$ 和 $q$ 的差值。为了唯一确定 $p$ 和 $q$，我们还需要通过检验来确定[根串](@entry_id:180284)的端点。具体来说，我们需要检查形如 $\beta + \alpha, \beta + 2\alpha, \dots$ 的向量，直到找到第一个不属于[根系](@entry_id:198970)的向量，从而确定 $p$ 的值。类似地，通过检查 $\beta - \alpha, \beta - 2\alpha, \dots$ 来确定 $q$ 的值。

让我们通过一个具体的例子来理解这个过程。考虑 $C_3$ 型[李代数的根](@entry_id:190590)系，其根可以表示在三维[欧几里得空间](@entry_id:138052) $\mathbb{R}^3$ 中，基为 $\{e_1, e_2, e_3\}$。我们研究通过根 $\beta = e_1 + e_2$ 的 $\alpha = e_2 - e_3$ [根串](@entry_id:180284) [@problem_id:762700]。

首先，我们计算[内积](@entry_id:158127)：
$$
(\beta, \alpha) = (e_1 + e_2, e_2 - e_3) = (e_2, e_2) = 1
$$
$$
(\alpha, \alpha) = (e_2 - e_3, e_2 - e_3) = (e_2, e_2) + (-e_3, -e_3) = 1+1=2
$$
利用核心公式，我们得到：
$$
q - p = \frac{2(\beta, \alpha)}{(\alpha, \alpha)} = \frac{2 \cdot 1}{2} = 1
$$
这告诉我们 $q = p+1$。现在我们来寻找 $p$ 和 $q$ 的具体值。我们从 $k=1$ 开始检验 $\beta+k\alpha$：
$$
\beta + \alpha = (e_1 + e_2) + (e_2 - e_3) = e_1 + 2e_2 - e_3
$$
在 $C_3$ 的根系中，根的形式为 $\pm 2e_i$ 或 $\pm e_i \pm e_j$。显然，$e_1 + 2e_2 - e_3$ 不属于这些形式，因此它不是一个根。这意味着[根串](@entry_id:180284)在正方向上不能延伸，所以 $p=0$。根据 $q = p+1$，我们得到 $q=1$。
为了验证，我们检查 $k=-1$ 的情况：
$$
\beta - \alpha = (e_1 + e_2) - (e_2 - e_3) = e_1 + e_3
$$
这确实是 $C_3$ 的一个短根。我们再检查 $k=-2$：
$$
\beta - 2\alpha = (e_1+e_2) - 2(e_2-e_3) = e_1 - e_2 + 2e_3
$$
这也不是一个根。因此，$q$ 的最大值确实是 $1$。
综上所述，[根串](@entry_id:180284)为 $\{\beta-\alpha, \beta\}$，包含 $p+q+1 = 0+1+1=2$ 个根。

当根的长度不同时，[余根](@entry_id:193338) $\alpha^\vee$ 在公式中的作用就显得尤为重要。考虑 $G_2$ 根系，它由一个短单根 $\alpha_1$ 和一个长单根 $\alpha_2$ 生成，满足 $(\alpha_2, \alpha_2) = 3(\alpha_1, \alpha_1)$。让我们确定通过长根 $\alpha_2$ 的短根 $\alpha_1$-串 [@problem_id:747341]。我们需要计算 $\langle \alpha_2, \alpha_1^\vee \rangle$。
$$
\langle \alpha_2, \alpha_1^\vee \rangle = \frac{2(\alpha_2, \alpha_1)}{(\alpha_1, \alpha_1)}
$$
两个单根之间的夹角为 $\frac{5\pi}{6}$。设 $(\alpha_1, \alpha_1)=s$，则 $(\alpha_2, \alpha_2)=3s$，且 $(\alpha_2, \alpha_1) = \sqrt{s} \sqrt{3s} \cos(5\pi/6) = \sqrt{3}s (-\frac{\sqrt{3}}{2}) = -\frac{3}{2}s$。代入得：
$$
q - p = \frac{2(-\frac{3}{2}s)}{s} = -3
$$
由于 $\alpha_1, \alpha_2$ 都是单根，它们的差 $\alpha_2 - \alpha_1$ 不可能是根，这意味着[根串](@entry_id:180284)在负方向不能延伸，即 $q=0$。因此 $0-p=-3$，得到 $p=3$。该[根串](@entry_id:180284)为 $\{\alpha_2, \alpha_2+\alpha_1, \alpha_2+2\alpha_1, \alpha_2+3\alpha_1\}$，共 $p+q+1=4$ 个根。

### [根串](@entry_id:180284)作为 $\mathfrak{sl}_2(\mathbb{C})$ 的表示

[根串](@entry_id:180284)的真正威力在于它们与[李代数表示论](@entry_id:190569)的深刻联系。对于根系 $\Phi$ 中的任意一个根 $\alpha$，其对应的根向量 $E_\alpha$, $F_\alpha$（分别对应根 $\alpha$ 和 $-\alpha$）以及[嘉当子代数](@entry_id:191259)中的元素 $H_\alpha = [E_\alpha, F_\alpha]$，构成了一个与 $\mathfrak{sl}_2(\mathbb{C})$ 同构的子代数，我们记为 $\mathfrak{sl}_2(\alpha)$。

整个李代数 $\mathfrak{g}$ 可以被看作是这个 $\mathfrak{sl}_2(\alpha)$ 子代数的一个表示。这个表示通常是可约的，它可以分解为一系列不可约的 $\mathfrak{sl}_2(\alpha)$ 子[模的[直](@entry_id:156308)和](@entry_id:156782)。令人惊奇的是，每一个[根串](@entry_id:180284)都精确地对应着这样一个不可约子模。具体来说，由一个 $\alpha$-[根串](@entry_id:180284) $\{ \beta+k\alpha \mid -q \le k \le p \}$ 中所有根对应的根空间 $\mathfrak{g}_{\beta+k\alpha}$ 的直和，构成了一个不可约的 $\mathfrak{sl}_2(\alpha)$-模 $M_{\beta, \alpha}$。
$$
M_{\beta, \alpha} = \bigoplus_{k=-q}^{p} \mathfrak{g}_{\beta+k\alpha}
$$
在这个模中，$H_\alpha$ 的作用是[对角化](@entry_id:147016)的，其在一个根空间 $\mathfrak{g}_{\gamma}$ 上的[本征值](@entry_id:154894)为 $\langle \gamma, \alpha^\vee \rangle$。对于我们的[根串](@entry_id:180284)模 $M_{\beta, \alpha}$，其权重（$H_\alpha$ 的[本征值](@entry_id:154894)）集合为：
$$
\{ \langle \beta+k\alpha, \alpha^\vee \rangle = \langle \beta, \alpha^\vee \rangle + 2k \mid -q \le k \le p \}
$$
这是一个由整数构成的[等差数列](@entry_id:265070)，公差为 2，这正是有限维 $\mathfrak{sl}_2(\mathbb{C})$ 表示的标志性特征。一个不可约的 $\mathfrak{sl}_2(\mathbb{C})$ 表示由其**[最高权](@entry_id:202808)重 (highest weight)** $\lambda$（一个非负整数）完全确定，其权重集为 $\{\lambda, \lambda-2, \dots, -\lambda\}$。

对于[根串](@entry_id:180284)模 $M_{\beta, \alpha}$，其最高权重 $\lambda$ 是什么呢？模中的[最高权](@entry_id:202808)重向量对应于[根串](@entry_id:180284)的正向端点，即 $\mathfrak{g}_{\beta+p\alpha}$ 中的向量。其权重为：
$$
\lambda = \langle \beta+p\alpha, \alpha^\vee \rangle = \langle \beta, \alpha^\vee \rangle + 2p
$$
将我们之前得到的公式 $q-p = \langle \beta, \alpha^\vee \rangle$ 代入，可得：
$$
\lambda = (q-p) + 2p = p+q
$$
这是一个非常优美的结果：构成 $\mathfrak{sl}_2(\alpha)$-不可约表示的[根串](@entry_id:180284)，其[最高权](@entry_id:202808)重恰好是描述[根串](@entry_id:180284)两端延伸长度的整数 $p$ 和 $q$ 的和。

这个联系为计算提供了捷径。例如，在 $A_3$ 根系中，我们想知道由通过 $\beta = \alpha_2+\alpha_3$ 的 $\alpha_1$-[根串](@entry_id:180284)构成的 $\mathfrak{sl}_2(\alpha_1)$-模的[最高权](@entry_id:202808)重 [@problem_id:762579]。我们只需找到 $p$ 和 $q$。
$\beta+\alpha_1 = \alpha_1+\alpha_2+\alpha_3$ 是 $A_3$ 的[最高根](@entry_id:183719)，因此它是一个根。
$\beta+2\alpha_1 = 2\alpha_1+\alpha_2+\alpha_3$ 不再是根（在 $A_3$ 中，[正根](@entry_id:199264)的单[根系](@entry_id:198970)数均不大于1）。所以 $p=1$。
$\beta-\alpha_1 = -\alpha_1+\alpha_2+\alpha_3$ 不是一个根（既不是[正根](@entry_id:199264)也不是负根）。所以 $q=0$。
因此，该模的最高权重为 $\lambda = p+q = 1+0=1$。这对应于 $\mathfrak{sl}_2$ 的 2 维标准表示。

在某些情况下，我们可以利用根的特殊性质来简化计算。例如，考虑 $G_2$ [根系](@entry_id:198970)中通过[最高根](@entry_id:183719) $\theta=3\alpha_1+2\alpha_2$ 的 $\alpha_1$-[根串](@entry_id:180284) [@problem_id:762595]。[最高根](@entry_id:183719)的一个基本性质是，对于任何单根 $\alpha_i$，$\theta+\alpha_i$ 都不是根。这立即告诉我们 $p=0$。然后我们计算 $q-p = \langle \theta, \alpha_1^\vee \rangle$。根据[嘉当矩阵](@entry_id:185184) $A_{ij} = \langle\alpha_j, \alpha_i^\vee\rangle$ 的惯例：
$$
\langle 3\alpha_1+2\alpha_2, \alpha_1^\vee \rangle = 3\langle \alpha_1, \alpha_1^\vee \rangle + 2\langle \alpha_2, \alpha_1^\vee \rangle = 3A_{11} + 2A_{12} = 3(2) + 2(-1) = 4
$$
其中 $A_{ij}$ 是 $G_2$ 的[嘉当矩阵](@entry_id:185184)元素。因此 $q-0 = 4 \Rightarrow q=4$。对应的 $\mathfrak{sl}_2(\alpha_1)$-模的最高权重为 $\lambda = p+q=0+4=4$。

这一表示理论的观点还允许我们计算更复杂的物理量，例如 **Casimir 算子**的[本征值](@entry_id:154894)。对于 $\mathfrak{sl}_2(\alpha_1)$ 子代数，其二次 Casimir 算子 $C_1$ 在一个[最高权](@entry_id:202808)重为 $\lambda$ 的[不可约表示](@entry_id:263310)上是一个标量算子，其[本征值](@entry_id:154894)为 $\lambda(\lambda+2)$（在某个标准规范化下）。考虑 $A_2$ [根系](@entry_id:198970)中由通过 $\alpha_2$ 的 $\alpha_1$-[根串](@entry_id:180284)构成的模 $M$ [@problem_id:762594]。该[根串](@entry_id:180284)包含根 $\alpha_2$ 和 $\alpha_1+\alpha_2$。我们需要找到此 $\mathfrak{sl}_2(\alpha_1)$-模的[最高权](@entry_id:202808)重。模中的权重由 $H_1$ 的[本征值](@entry_id:154894)给出：
$$
\langle \alpha_2, \alpha_1^\vee \rangle = A_{12} = -1
$$
$$
\langle \alpha_1+\alpha_2, \alpha_1^\vee \rangle = \langle \alpha_1, \alpha_1^\vee \rangle + \langle \alpha_2, \alpha_1^\vee \rangle = A_{11} + A_{12} = 2 + (-1) = 1
$$
权重的集合是 $\{-1, 1\}$。这是一个最高权重为 $\lambda=1$ 的[不可约表示](@entry_id:263310)。因此，Casimir 算子 $C_1$ 在该模上的[本征值](@entry_id:154894)为 $\lambda(\lambda+2) = 1(1+2) = 3$。

### 几何与对称性质

[根串](@entry_id:180284)的向量性质使其具有有趣的几何属性。一个[根串](@entry_id:180284)中的所有根向量 $\{v_1, \dots, v_N\}$，可以看作欧几里得空间中的点集。这些点的**[质心](@entry_id:265015) (centroid)** 是它们的算术平均值 $C = \frac{1}{N} \sum v_i$。对于一个[根串](@entry_id:180284) $\{\beta+k\alpha \mid k=-q, \dots, p\}$，其质心为：
$$
C = \frac{1}{p+q+1} \sum_{k=-q}^{p} (\beta+k\alpha) = \beta + \frac{\alpha}{p+q+1} \sum_{k=-q}^{p} k
$$
利用[等差数列](@entry_id:265070)求和公式 $\sum_{k=-q}^{p} k = \frac{(p-q)(p+q+1)}{2}$，我们得到一个简洁的表达式：
$$
C = \beta + \frac{p-q}{2}\alpha = \beta - \frac{\langle\beta,\alpha^\vee\rangle}{2}\alpha
$$
这个公式表明，[根串](@entry_id:180284)的质心位于穿过 $\beta$ 且平行于 $\alpha$ 的直线上，其精确位置由嘉当整数 $\langle\beta,\alpha^\vee\rangle$ 决定。

例如，在 $A_3$ [根系](@entry_id:198970)中，通过 $\alpha_2$ 的 $\alpha_1$-[根串](@entry_id:180284)为 $S = \{\alpha_2, \alpha_1+\alpha_2\}$ [@problem_id:762761]。这里 $p=1, q=0$。质心为 $C = \frac{1}{2}(\alpha_2 + \alpha_1+\alpha_2) = \frac{1}{2}\alpha_1+\alpha_2$。如果我们采用 $A_3$ 的一个标准实现，如 $\alpha_1=e_1-e_2, \alpha_2=e_2-e_3$，那么 $C = \frac{1}{2}(e_1-e_2)+(e_2-e_3) = \frac{1}{2}e_1+\frac{1}{2}e_2-e_3$。其[欧几里得范数](@entry_id:172687)的平方为 $\|C\|^2 = (\frac{1}{2})^2+(\frac{1}{2})^2+(-1)^2 = \frac{3}{2}$。

[根串](@entry_id:180284)的性质与根系的对称性，即**魏尔群 (Weyl group)**，密切相关。魏尔群是由对根的反射 $s_\gamma(\beta) = \beta - \langle\beta, \gamma^\vee\rangle\gamma$ 生成的。这些反射是等距变换，它们保持向量间的[内积](@entry_id:158127)和长度。因此，一个魏尔群元素作用于一个[根串](@entry_id:180284)，会得到另一个根的集合，这个新集合依然保持着原根串的几何结构（长度、相对位置等）。

考虑前一个例子中的 $A_3$ [根串](@entry_id:180284) $S=\{\alpha_2, \alpha_1+\alpha_2\}$。如果我们对其应用魏尔反射 $s_{\alpha_3}$ [@problem_id:762752]，我们会得到一个新的根集合 $S' = \{s_{\alpha_3}(\alpha_2), s_{\alpha_3}(\alpha_1+\alpha_2)\}$。
$$
s_{\alpha_3}(\alpha_2) = \alpha_2 - \langle\alpha_2, \alpha_3^\vee\rangle\alpha_3 = \alpha_2 - (-1)\alpha_3 = \alpha_2+\alpha_3
$$
$$
s_{\alpha_3}(\alpha_1+\alpha_2) = \alpha_1+\alpha_2 - \langle\alpha_1+\alpha_2, \alpha_3^\vee\rangle\alpha_3 = \alpha_1+\alpha_2 - (-1)\alpha_3 = \alpha_1+\alpha_2+\alpha_3
$$
新集合为 $S' = \{\alpha_2+\alpha_3, \alpha_1+\alpha_2+\alpha_3\}$。新[质心](@entry_id:265015) $C'$ 就是原[质心](@entry_id:265015) $C$ 在反射下的像，$C' = s_{\alpha_3}(C)$。由于反射是[等距变换](@entry_id:150881)，[质心](@entry_id:265015)的范数平方保持不变：$\|C'\|^2 = \|C\|^2 = \frac{3}{2}$。

这个组合操作在更复杂的[根系](@entry_id:198970)中也同样适用。例如，在 $D_4$ [根系](@entry_id:198970)中，我们可以确定通过 $\alpha_2$ 的 $\alpha_1$-[根串](@entry_id:180284)，然后对其应用反射 $s_{\alpha_3}$，并分析结果集中根的性质，比如**高度 (height)**（根表示为单根[线性组合](@entry_id:154743)时系数之和） [@problem_id:762734]。通过 $\alpha_2$ 的 $\alpha_1$-[根串](@entry_id:180284)是 $\{\alpha_2, \alpha_1+\alpha_2\}$。经 $s_{\alpha_3}$ 反射后得到 $\{\alpha_2+\alpha_3, \alpha_1+\alpha_2+\alpha_3\}$。这两个根的高度分别为 $1+1=2$ 和 $1+1+1=3$。因此，变换后集合中高度最大的根是 $\alpha_1+\alpha_2+\alpha_3$，其高度为 $3$。

### 对偶性与[余根](@entry_id:193338)串

根系 $\Phi$ 具有一个与之对偶的结构，即由所有[余根](@entry_id:193338) $\alpha^\vee$ 构成的**对偶根系 (dual root system)** $\Phi^\vee$。与[根串](@entry_id:180284)类似，我们也可以定义**[余根](@entry_id:193338)串 (coroot string)**。通过 $\beta^\vee$ 的 $\alpha^\vee$-[余根](@entry_id:193338)串是集合 $\{\beta^\vee+k\alpha^\vee \in \Phi^\vee\}$。

决定[余根](@entry_id:193338)串端点的公式与[根串](@entry_id:180284)的公式非常相似，只是根与[余根](@entry_id:193338)的角色发生了互换。若[余根](@entry_id:193338)串的整数范围是 $-q$ 到 $p$，则：
$$
q - p = \langle \beta^\vee, \alpha \rangle = \frac{2(\beta^\vee, \alpha)}{(\alpha, \alpha)}
$$
注意，这里[内积](@entry_id:158127)是与普通的根 $\alpha$ 进行计算的。

$B_2$ [根系](@entry_id:198970)提供了一个很好的例子来展示这种对偶性 [@problem_id:762707]。令 $\alpha_1$ 为长单根，$\alpha_2$ 为短单根。我们来构造两个向量和：$V$ 是通过 $\alpha_1$ 的 $\alpha_2$-[根串](@entry_id:180284)中所有根的和；$W$ 是通过 $\alpha_1^\vee$ 的 $\alpha_2^\vee$-[余根](@entry_id:193338)串中所有[余根](@entry_id:193338)的和。
1.  **[根串](@entry_id:180284)**: 设 $A_{ij} = \langle\alpha_i, \alpha_j^\vee\rangle$。对于 $B_2$ [根系](@entry_id:198970)，若 $\alpha_1$ 长、$\alpha_2$ 短，则 $A_{12}=-1, A_{21}=-2$。我们求 $\alpha_2$-串穿过 $\alpha_1$。因此，我们计算 $q-p = \langle \alpha_1, \alpha_2^\vee \rangle = A_{21} = -2$。由于 $\alpha_1-\alpha_2$ 不是根（单根之差），所以 $q=0$。从而得到 $p=2$。该[根串](@entry_id:180284)为 $\{\alpha_1, \alpha_1+\alpha_2, \alpha_1+2\alpha_2\}$。它们的和是 $V=3\alpha_1+3\alpha_2$。
2.  **[余根](@entry_id:193338)串**: 我们求 $\alpha_2^\vee$-串穿过 $\alpha_1^\vee$。计算 $q-p = \langle \alpha_1^\vee, \alpha_2 \rangle = \langle \alpha_2, \alpha_1^\vee \rangle = A_{12} = -1$。由于 $\alpha_1^\vee-\alpha_2^\vee$ 不是[余根](@entry_id:193338)，所以 $q=0$。从而得到 $p=1$。该[余根](@entry_id:193338)串为 $\{\alpha_1^\vee, \alpha_1^\vee+\alpha_2^\vee\}$。它们的和是 $W=2\alpha_1^\vee+\alpha_2^\vee$。
利用 $B_2$ 的[内积](@entry_id:158127)关系 $(\alpha_1,\alpha_1)=2, (\alpha_2,\alpha_2)=1, (\alpha_1,\alpha_2)=-1$ 以及[余根](@entry_id:193338)定义，我们可以计算[内积](@entry_id:158127) $(V, W)$，最终得到一个整数值，这具体地展示了根系与其对偶根系之间相互关联的对称性。

总之，[根串](@entry_id:180284)是理解李[代数结构](@entry_id:137052)的关键。它们不仅是根系中的几何对象，更是 $\mathfrak{sl}_2$ 子[代数表示](@entry_id:143783)的物理体现。通过掌握[根串](@entry_id:180284)的计算公式、其与[表示论](@entry_id:137998)的联系以及在魏尔[群作用](@entry_id:268812)下的变换规律，我们能够对[李代数](@entry_id:137954)的内部工作机制获得更深刻的洞察。