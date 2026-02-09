## 引言
调和映射作为黎曼流形间狄利克雷能量泛函的临界点，是几何分析领域的基石概念之一。研究这些由非线性偏微分方程定义的映射的存在性、唯一性、正则性及其几何性质，构成了该领域的核心挑战。为了应对这一挑战，数学家们发展了一套强大的分析工具，其中最具影响力的便是Bochner公式。这一深刻的恒等式揭示了映射的分析性质（如能量密度的变化）与背景流形的几何性质（即曲率）之间令人惊叹的内在联系，为解决上述难题提供了关键钥匙。

本文旨在系统性地阐述调和映射的Bochner公式。我们将首先在“原理与机制”一章中，从能量泛函的变分出发，定义调和映射与张力场，并构建必要的协变微分框架，最终详细推导Bochner公式本身。随后，在“应用与交叉联系”一章中，我们将展示该公式如何被用于证明里程碑式的存在性定理（如Eells-Sampson定理）、建立深刻的刚性定理、分析奇点结构，并启发其在更广阔领域中的应用。最后，通过“动手实践”部分提供的一系列练习，读者将有机会亲手运用这些概念，巩固对理论的理解。通过这三章的学习，您将全面掌握这一强大的几何分析工具。

## 原理与机制

本章旨在深入探讨调和映射理论的核心分析工具——Bochner公式。我们将从调和映射的基本定义出发，该定义源于一个自然的变分原理。随后，我们将构建必要的几何与分析框架，包括拉回丛、拉回联络以及映射的协变导数。在此基础上，我们将详细推导适用于映射微分的 Weitzenböck 恒等式，并最终得到关键的 Bochner 公式。此公式揭示了映射能量密度的拉普拉斯算子如何与定义域和目标流形的曲率以及映射本身的二阶性质相关联。我们还将讨论该公式在不同曲率约定下的形式，并考察其在常截面曲率目标流形这一重要特例下的简化。

### 能量泛函与变分原理

在几何分析中，研究两个黎曼流形 $(M, g)$ 与 $(N, h)$ 之间的光滑映射 $f: M \to N$ 的一个核心策略是考察其**狄利克雷能量 (Dirichlet energy)**。这个泛函量化了映射在“拉伸”源流形方面的总程度。

映射 $f$ 的**能量密度 (energy density)** $e(f)$ 是一个定义在 $M$ 上的函数，它逐点地测量了映射的微分 $df$ 的范数平方。具体而言，
$$
e(f) = \frac{1}{2} |df|^2
$$
这里的因子 $\frac{1}{2}$ 是为了简化后续变分计算而引入的传统约定。为了精确理解 $|df|^2$ 的含义，我们必须考虑在每一点 $p \in M$ 的切空间 $T_pM$ 上的微分 $df_p: T_pM \to T_{f(p)}N$。$|df_p|^2$ 是其作为线性映射的希尔伯特-施密特范数 (Hilbert-Schmidt norm) 的平方，该范数由源度规 $g$ 和目标度规 $h$ 共同诱导。一个实用的计算方式是选取 $T_pM$ 的一组 $g$-单位正交基 $\{e_i\}_{i=1}^m$，其中 $m = \dim(M)$。$|df|^2$ 在点 $p$ 的值即为这些基向量在 $df_p$ 下的像的范数平方和：
$$
|df|^2 = \sum_{i=1}^m h(df(e_i), df(e_i))
$$
这个值不依赖于单位正交基的选取。此外，这个量也可以通过 $f$ 的**拉回度规 (pullback metric)** $f^*h$ 来理解。$f^*h$ 是 $M$ 上的一个 $(0,2)$ 型张量，其定义为 $(f^*h)(X, Y) = h(df(X), df(Y))$。$|df|^2$ 恰好是 $f^*h$ 关于度规 $g$ 的迹，即 $|df|^2 = \operatorname{trace}_g(f^*h)$。[@problem_id:3025931]

通过对能量密度在整个流形 $M$ 上关于其黎曼体积元 $d\mu_g$ 进行积分，我们便得到了映射 $f$ 的总**狄利克雷能量 (Dirichlet energy)**：
$$
E(f) = \int_M e(f) \, d\mu_g = \frac{1}{2} \int_M |df|^2 \, d\mu_g
$$

### 调和映射与张力场

能量泛函 $E(f)$ 的关键点是其临界点。在泛函分析的框架下，这些临界点代表了在某种意义上“最经济”或“最平衡”的映射，我们称之为**调和映射 (harmonic maps)**。

为了找到这些临界点，我们考虑 $f$ 的一个光滑变分。这是一个单参数映射族 $f_t: M \to N$，其中 $t \in (-\epsilon, \epsilon)$，且 $f_0 = f$。该变分在 $t=0$ 处的**变分向量场 (variational vector field)** $V$ 是一个沿着 $f$ 的向量场，定义为 $V(p) = \frac{\partial f_t(p)}{\partial t}\Big|_{t=0}$。$V$ 是拉回丛 $f^*TN$ 的一个截面，即 $V \in \Gamma(f^*TN)$。我们假设 $V$ 在 $M$ 的内部具有紧支集，这意味着它在 $M$ 的边界（如果存在）附近为零。

能量 $E(f_t)$ 对 $t$ 在 $t=0$ 处的导数，即能量泛函的一阶变分，可以通过在积分号下求导并利用分部积分（即流形上的散度定理）来计算。这个计算引出了一个核心概念：映射 $f$ 的**张力场 (tension field)** $\tau(f)$。张力场 $\tau(f)$ 是拉回丛 $f^*TN$ 的一个截面，其定义为映射微分的协变导数 $\nabla df$ 的迹：
$$
\tau(f) := \operatorname{trace}_g(\nabla df)
$$
我们将在下一节详细阐述 $\nabla df$ 的精确定义。一阶变分的最终结果是：
$$
\frac{d}{dt}\Big|_{t=0} E(f_t) = - \int_M \langle \tau(f), V \rangle_h \, d\mu_g
$$
其中 $\langle \cdot, \cdot \rangle_h$ 是由 $h$ 诱导的 $f^*TN$ 纤维上的内积。[@problem_id:3025947]

根据定义，$f$ 是能量泛函 $E$ 的一个临界点，当且仅当对于所有具有紧支集的变分向量场 $V$，上述一阶变分恒为零。根据变分法基本引理，这等价于被积函数的核 $\tau(f)$ 恒为零。因此，我们得到了调和映射的分析定义：
**一个光滑映射 $f$ 被称为调和映射，当且仅当其张力场 $\tau(f)$ 处处为零。**

这个定义将一个变分问题（寻找能量的临界点）转化为了一个偏微分方程问题 $\tau(f) = 0$。这个方程通常是二阶、非线性的。

从泛函分析的角度看，上述变分公式 $\delta E(f)(V) = \langle -\tau(f), V \rangle_{L^2}$ 表明，张力场 $\tau(f)$ 恰好是能量泛函 $E$ 在 $L^2$ 内积下的负梯度，即 $\operatorname{grad}_{L^2}E(f) = -\tau(f)$。因此，调和映射方程 $\tau(f)=0$ 描述的是能量的梯度为零的点，这正是临界点的定义。[@problem_id:3025952]

一个重要的特例是当目标流形是欧几里得空间 $(N, h) = (\mathbb{R}^k, \delta)$ 时，其联络是平凡的。在这种情况下，张力场的表达式大大简化。它变成了作用在映射各个分量函数 $f^\alpha$ 上的 Laplace-Beltrami 算子：
$$
\tau(f)^\alpha = \Delta_g f^\alpha = \operatorname{div}_g(\operatorname{grad}_g f^\alpha)
$$
此时，调和映射方程就是经典的拉普拉斯方程组 $\Delta_g f^\alpha = 0$。[@problem_id:3025952]

### 协变微分框架

要严格地理解张力场 $\tau(f) = \operatorname{trace}_g(\nabla df)$ 的定义，我们必须建立一套在流形间的映射上进行微分计算的框架。这涉及到拉回丛、拉回联络和协变导数等概念。

首先，我们考虑微分 $df$ 的本质。在每一点 $p \in M$，$df_p$ 是一个从 $T_pM$到 $T_{f(p)}N$ 的线性映射。当 $p$ 在 $M$ 上变动时，这些线性映射的集合构成了一个张量丛的[截面](@entry_id:154995)，具体来说，是 $T^*M \otimes f^*TN$ 的一个截面。这里的 $f^*TN$ 是一个关键的构造，称为**拉回丛 (pullback bundle)**。[@problem_id:3025940]

$f^*TN$ 是一个定义在 $M$ 上的向量丛，其在点 $p \in M$ 的纤维 $(f^*TN)_p$ 正是目标流形 $N$ 在点 $f(p)$ 的切空间 $T_{f(p)}N$。直观地说，$f^*TN$ 沿着映射 $f$ 将 $N$ 的切丛“拉回”到了 $M$ 上，使得我们可以在 $M$ 的每一点上谈论 $N$ 的切向量。

接下来，我们需要在 $f^*TN$ 上定义一个协变导数，即一个**联络 (connection)**。幸运的是，$N$ 上的 Levi-Civita 联络 $\nabla^N$ 可以自然地诱导一个**拉回联络 (pullback connection)** $\nabla^{f^*TN}$ 在 $f^*TN$上。对于 $M$ 上的任意向量场 $X$ 和 $f^*TN$ 的任意截面 $W$，协变导数 $\nabla^{f^*TN}_X W$ 被定义为：将 $W$ 延拓为 $f$ 附近 $N$ 上的一个局部向量场 $\widetilde{W}$，然后计算 $(\nabla^N)_{df(X)} \widetilde{W}$。这个定义被证明是与延拓方式无关的。[@problem_id:3025940]

有了源流形 $M$ 上的 Levi-Civita 联络 $\nabla^M$ 和 $f^*TN$ 上的拉回联络 $\nabla^{f^*TN}$，我们就可以在张量积丛 $T^*M \otimes f^*TN$ 上定义一个自然的乘积联络 $\nabla$。$df$ 作为该丛的一个截面，其协变导数 $\nabla df$ 就被定义了。$\nabla df$ 是一个 $(0,2)$ 型、取值于 $f^*TN$ 的张量，有时也被称为映射 $f$ 的**第二基本形式 (second fundamental form)** 或**黑塞张量 (Hessian)**。它由以下法则确定：
$$
(\nabla df)(X,Y) = \nabla^{f^*TN}_X (df(Y)) - df(\nabla^M_X Y)
$$
对于任意 $M$ 上的向量场 $X, Y$。由于 Levi-Civita 联络是无挠的，$\nabla df$ 是一个对称张量，即 $(\nabla df)(X,Y) = (\nabla df)(Y,X)$。[@problem_id:3025940]

至此，张力场的定义 $\tau(f) = \operatorname{trace}_g(\nabla df)$ 变得完全清晰：它是在任意 $g$-单位正交标架场 $\{e_i\}$ 下，对第二基本形式求和 $\sum_i (\nabla df)(e_i, e_i)$ 的结果。

### Bochner-Weitzenböck 公式

Bochner-Weitzenböck 公式（通常简称为 Bochner 公式）是几何分析中的一块基石。它是一个深刻的恒等式，联系了一个几何量的拉普拉斯算子、其协变导数的范数以及背景流形的曲率。对于调和映射理论，我们关注的是作用在能量密度 $e(f) = \frac{1}{2}|df|^2$ 上的拉普拉斯算子 $\Delta_g e(f)$。

推导这一公式的核心步骤是理解协变导数的交换子如何产生曲率。
首先，考虑作用在拉回丛 $f^*TN$ 截面上的拉回联络 $\nabla^{f^*TN}$。其曲率张量 $R^{f^*TN}$ 由协变导数的交换子定义：$R^{f^*TN}(X,Y)W = \nabla_X\nabla_Y W - \nabla_Y\nabla_X W - \nabla_{[X,Y]}W$。一个基础性的计算表明，这个曲率完全由目标流形 $N$ 的曲率 $R^N$ 决定：
$$
R^{f^*TN}(X,Y)W = R^N(df(X), df(Y))W
$$
这个等式被称为**高斯方程 (Gauss equation)** 的一种形式，它表明拉回丛的曲率即为目标流形曲率的“拉回”。[@problem_id:3025944]

完整的 Bochner 公式的推导依赖于一个更为普适的 Weitzenböck 恒等式，该恒等式对任何取值于向量丛的微分形式都成立。它联系了两种不同类型的拉普拉斯算子：**联络拉普拉斯算子 (connection Laplacian)**（或称**粗拉普拉斯算子 (rough Laplacian)**）$\nabla^*\nabla$ 和**霍奇-拉普拉斯算子 (Hodge-Laplacian)** $\Delta_H = d^\nabla d^{\nabla*} + d^{\nabla*} d^\nabla$。对于取值于 $f^*TN$ 的1-形式 $df$，这两个算子之差完全由曲率决定：
$$
(\nabla^*\nabla df - \Delta_H df)(X) = df(\operatorname{Ric}^M(X)) - \sum_{i=1}^m R^N(df(e_i), df(X))df(e_i)
$$
其中 $X$ 是 $M$ 上任意向量场，$\{e_i\}$ 是 $M$ 上的局部单位正交标架。这个恒等式清晰地展示了两种曲率的来源：源流形的里奇曲率 $\operatorname{Ric}^M$ 作用于 $df$ 的 $T^*M$ 部分，而目标流形的黎曼曲率 $R^N$ 作用于其 $f^*TN$ 部分。[@problem_id:3025946]

利用 $\Delta_H df = d^\nabla(\tau(f)) - \delta^\nabla(d^\nabla df)$（这里 $d^\nabla$ 是外微分，$\delta^\nabla$ 是其伴随算子），以及 $\nabla df$ 的对称性（导致 $d^\nabla df=0$），我们可以将 Weitzenböck 恒等式与能量密度的拉普拉斯算子联系起来。经过一系列计算，我们最终得到作用于能量密度 $e(f) = \frac{1}{2}|df|^2$ 的 Bochner 公式。对于一个**一般的**光滑映射 $u: M \to N$，该公式为：
$$
\frac{1}{2}\Delta_g |du|^2 = |\nabla du|^2 + \langle \nabla \tau(u), du \rangle + \langle du \circ \operatorname{Ric}^M, du \rangle - \sum_{i,j=1}^m \langle R^N(du(e_i), du(e_j))du(e_j), du(e_i) \rangle
$$
这里的记号 $\langle du \circ \operatorname{Ric}^M, du \rangle$ 表示 $\sum_{i=1}^m \langle du(\operatorname{Ric}^M(e_i)), du(e_i) \rangle_h$。[@problem_id:3035000] [@problem_id:3033004]

当映射 $u$ 是**调和映射**时，$\tau(u)=0$，因此 $\nabla\tau(u)=0$。公式简化为：
$$
\frac{1}{2}\Delta_g |du|^2 = |\nabla du|^2 + \langle du \circ \operatorname{Ric}^M, du \rangle - \sum_{i,j=1}^m \langle R^N(du(e_i), du(e_j))du(e_j), du(e_i) \rangle
$$
这个公式是调和映射理论的中心。它表明，能量密度的二阶变化（由 $\Delta_g |du|^2$ 衡量）由三部分控制：
1.  $|\nabla du|^2$：映射的第二基本形式的范数平方。这个量总是非负的，反映了映射的“弯曲”程度。
2.  $\langle du \circ \operatorname{Ric}^M, du \rangle$：源流形 $M$ 的里奇曲率的贡献。如果 $\operatorname{Ric}^M \ge 0$，这一项也是非负的。
3.  $-\sum \langle R^N, \dots \rangle$：目标流形 $N$ 的黎曼曲率的贡献。这一项的符号通常更为复杂。

#### 关于曲率符号的注记
在阅读不同文献时，必须注意作者对黎曼曲率张量的符号约定。一个常见的替代约定是 $R^\#(X,Y)Z = -R(X,Y)Z$。如果采用这个 $R^\#$ 约定来定义 $N$ 的曲率，那么 Bochner 公式中的目标曲率项的符号将会翻转。具体来说，如果采用 $R(X,Y)Z = \nabla_X\nabla_Y Z - \nabla_Y\nabla_X Z - \nabla_{[X,Y]}Z$（本文约定），则目标曲率项为负。如果采用相反的约定，则目标曲率项为正。这是一个必须牢记的微妙之处，以避免在应用中出现错误。[@problem_id:3025933]

### 应用：常截面曲率目标流形

Bochner 公式的威力在其应用于具有特殊几何结构的流形时尤为明显。一个重要的例子是当目标流形 $(N,h)$ 具有**常截面曲率 (constant sectional curvature)** $K$ 时。在这种情况下，$N$ 的曲率张量有非常简单的形式：
$$
\langle R^N(U,V)W,Z \rangle_h = K(\langle U,W \rangle_h \langle V,Z \rangle_h - \langle U,Z \rangle_h \langle V,W \rangle_h)
$$
我们将这个表达式代入 Bochner 公式中的目标曲率项 $\mathcal{C}_N = \sum_{i,j=1}^m \langle R^N(df(e_i), df(e_j))df(e_j), df(e_i) \rangle_h$。
令 $U = df(e_i), V = df(e_j), W = df(e_j), Z = df(e_i)$，我们得到：
$$
\mathcal{C}_N = \sum_{i,j=1}^m K \left( \langle df(e_i), df(e_j) \rangle_h \langle df(e_j), df(e_i) \rangle_h - \langle df(e_i), df(e_i) \rangle_h \langle df(e_j), df(e_j) \rangle_h \right)
$$
为了简化这个表达式，我们引入 $df$ 的**格拉姆矩阵 (Gram matrix)** $G$，其元素为 $G_{ij} = \langle df(e_i), df(e_j) \rangle_h$。于是，上述曲率项变为：
$$
\mathcal{C}_N = K \sum_{i,j=1}^m (G_{ij}^2 - G_{ii}G_{jj}) = K \left( \sum_{i,j=1}^m G_{ij}^2 - \left(\sum_i G_{ii}\right) \left(\sum_j G_{jj}\right) \right)
$$
我们认出 $\sum_{i,j} G_{ij}^2$ 是矩阵 $G$ 的希尔伯特-施密特范数的平方 $\|G\|_{HS}^2$，而 $\sum_i G_{ii}$ 是 $G$ 的迹 $\operatorname{tr}(G)$。同时，$\operatorname{tr}(G) = \sum_i \langle df(e_i), df(e_i) \rangle_h = |df|^2$。
因此，$\mathcal{C}_N = K (\|G\|_{HS}^2 - (\operatorname{tr}G)^2)$。

将此结果代入调和映射的 Bochner 公式，我们得到：
$$
\frac{1}{2}\Delta_g |df|^2 = |\nabla df|^2 + \langle df \circ \operatorname{Ric}^M, df \rangle + K ((\operatorname{tr}G)^2 - \|G\|_{HS}^2)
$$
[@problem_id:3025930]

由于 $G$ 是一个格拉姆矩阵，因此它是半正定的。一个关于半正定矩阵的代数不等式确保了 $(\operatorname{tr}G)^2 \ge \|G\|_{HS}^2$。这意味着最后一项 $K ((\operatorname{tr}G)^2 - \|G\|_{HS}^2)$ 的符号与 $K$ 的符号相同。这个公式构成了许多经典结果的基础，例如，当源流形 $M$ 的 Ricci 曲率非负且目标流形 $N$ 的截面曲率非正（$K \le 0$）时，Bochner 公式告诉我们 $\Delta_g |df|^2 \ge 0$。由极大值原理可知，一个定义在紧流形上的调和映射的能量密度 $|df|^2$ 必为常数。这是通向存在性定理（如 Eells-Sampson 定理）和刚性定理的第一步。