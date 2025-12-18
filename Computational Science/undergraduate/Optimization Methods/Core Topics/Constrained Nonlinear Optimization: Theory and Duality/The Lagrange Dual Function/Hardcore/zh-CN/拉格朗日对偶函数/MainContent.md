## 引言
在[约束优化](@entry_id:635027)领域，拉格朗日函数是我们将问题从有约束转化为无约束形式的初步工具。然而，这一转变引入了新的变量——[拉格朗日乘子](@entry_id:142696)，其真正的力量和深刻含义需要通过一个更强大的概念来揭示：[拉格朗日对偶函数](@entry_id:637331)。理解对[偶函数](@entry_id:163605)是开启[优化理论](@entry_id:144639)中深刻对偶世界大门的关键，它不仅为求解复杂问题提供了新途径，也为我们理解问题结构本身提供了独特的视角。

本文旨在全面解析[拉格朗日对偶函数](@entry_id:637331)。我们将解决一个核心问题：如何通过构造对[偶函数](@entry_id:163605)来发现原问题最优值的下界，并利用这一性质来简化或分解问题。通过学习，您将掌握从理论到实践的全过程。

在“原理与机制”一章中，我们将深入其数学核心，从定义和计算实例出发，详细阐述其关键性质——[弱对偶](@entry_id:163073)性和[凹性](@entry_id:139843)。接着，在“应用与跨学科联系”一章中，我们将探索[对偶理论](@entry_id:143133)的现实意义，揭示[对偶变量](@entry_id:143282)如何化身为经济学中的“影子价格”，如何驱动[分布](@entry_id:182848)式[算法设计](@entry_id:634229)，以及如何成为[支持向量机](@entry_id:172128)等[机器学习模型](@entry_id:262335)背后的理论支柱。最后，通过“动手实践”环节，您将通过具体计算练习，巩固对偶函数的构建与分析能力。让我们一同踏上这段旅程，发掘[拉格朗日对偶](@entry_id:638042)理论的精髓与魅力。

## 原理与机制

在上一章中，我们引入了[拉格朗日函数](@entry_id:174593)，它是将一个带约束的[优化问题](@entry_id:266749)转化为一个无约束函数的工具。然而，[拉格朗日函数](@entry_id:174593)本身引入了新的变量——拉格朗日乘子。本章中，我们将深入探讨这些乘子的作用，并通过构造一个被称为**[拉格朗日对偶函数](@entry_id:637331) (Lagrange dual function)** 的新函数，来揭示原始问题（或称**原问题**, primal problem）背后深刻的对偶结构。

### [拉格朗日对偶函数](@entry_id:637331)的定义

考虑一个一般的[优化问题](@entry_id:266749)：
$$
\begin{array}{lll}
\text{最小化} & f_0(x) \\
\text{满足} & f_i(x) \le 0, & i = 1, \dots, m \\
& h_j(x) = 0, & j = 1, \dots, p
\end{array}
$$
其中 $x \in \mathbb{R}^n$ 是优化变量。其[拉格朗日函数](@entry_id:174593)为：
$$
L(x, \lambda, \nu) = f_0(x) + \sum_{i=1}^{m} \lambda_i f_i(x) + \sum_{j=1}^{p} \nu_j h_j(x)
$$
其中 $\lambda = (\lambda_1, \dots, \lambda_m)$ 和 $\nu = (\nu_1, \dots, \nu_p)$ 是[拉格朗日乘子](@entry_id:142696)向量。

**[拉格朗日对偶函数](@entry_id:637331)** $g: \mathbb{R}^m \times \mathbb{R}^p \to \mathbb{R}$ 被定义为拉格朗日函数 $L(x, \lambda, \nu)$ 关于原问题变量 $x$ 的**[下确界](@entry_id:140118) (infimum)**：
$$
g(\lambda, \nu) = \inf_{x \in \mathcal{D}} L(x, \lambda, \nu) = \inf_{x \in \mathcal{D}} \left( f_0(x) + \sum_{i=1}^{m} \lambda_i f_i(x) + \sum_{j=1}^{p} \nu_j h_j(x) \right)
$$
其中 $\mathcal{D}$ 是原问题[函数的定义域](@entry_id:162002)。这个定义是[拉格朗日对偶](@entry_id:638042)理论的基石。请注意，当 $L(x, \lambda, \nu)$ 作为 $x$ 的函数在定义域上无下界时，对[偶函数](@entry_id:163605)的值为 $-\infty$。

对偶函数的定义引出了一个重要的概念：**有效域 (effective domain)**。对偶函数的[有效域](@entry_id:636189)是指所有使得 $g(\lambda, \nu)$ 取有限值的 $(\lambda, \nu)$ 的集合。对于某些 $(\lambda, \nu)$，求 $L(x, \lambda, \nu)$ 关于 $x$ 的下确界时可能会发现函数是无下界的，此时 $g(\lambda, \nu) = -\infty$。

我们来看一个极简的线性例子 。考虑一个最小化 $f(x)=x$ 且满足 $-x \le 0$ 的问题。[拉格朗日函数](@entry_id:174593)为 $L(x, \lambda) = x + \lambda(-x) = (1-\lambda)x$，其中 $\lambda \ge 0$。对偶函数 $g(\lambda)$ 是 $L(x, \lambda)$ 关于 $x \in \mathbb{R}$ 的[下确界](@entry_id:140118)。
$$
g(\lambda) = \inf_{x \in \mathbb{R}} (1-\lambda)x
$$
这个[下确界](@entry_id:140118)的值取决于 $x$ 的系数 $(1-\lambda)$：
*   如果 $1-\lambda > 0$ (即 $0 \le \lambda < 1$)，这是一个斜率为正的线性函数，当 $x \to -\infty$ 时，函数值趋于 $-\infty$。
*   如果 $1-\lambda < 0$ (即 $\lambda > 1$)，这是一个斜率为负的线性函数，当 $x \to +\infty$ 时，函数值趋于 $-\infty$。
*   只有当 $1-\lambda = 0$ (即 $\lambda = 1$) 时，函数为 $L(x, 1) = 0 \cdot x = 0$，其[下确界](@entry_id:140118)为 $0$。

因此，该问题的对偶函数为：
$$
g(\lambda) = \begin{cases} 0 & \text{若 } \lambda = 1 \\ -\infty & \text{若 } \lambda \ge 0 \text{ 且 } \lambda \neq 1 \end{cases}
$$
这个例子清晰地表明，对偶函数的有效域可能非常有限，在此例中仅为单点集合 $\{1\}$。

### 对[偶函数](@entry_id:163605)的计算实例

从定义出发计算对偶函数是理解其性质的关键。下面我们通过几个典型的例子来展示计算过程。

#### [等式约束](@entry_id:175290)二次规划

考虑一个凸二次规划 (QP) 问题，其目标函数是二次的，约束是线性的。例如，最小化 $f(\mathbf{x}) = \frac{1}{2}\mathbf{x}^T Q \mathbf{x} + q^T \mathbf{x}$，满足 $A\mathbf{x} = \mathbf{b}$，其中 $Q$ 是[对称正定矩阵](@entry_id:136714) 。

拉格朗日函数为：
$$
L(\mathbf{x}, \nu) = \frac{1}{2}\mathbf{x}^T Q \mathbf{x} + q^T \mathbf{x} + \nu^T(A\mathbf{x} - \mathbf{b})
$$
为了求 $g(\nu) = \inf_{\mathbf{x}} L(\mathbf{x}, \nu)$，我们注意到对于固定的 $\nu$， $L(\mathbf{x}, \nu)$ 是一个关于 $\mathbf{x}$ 的严格凸二次函数（因为 $Q \succ 0$）。因此，其[下确界](@entry_id:140118)在梯度为零的点达到。我们对 $\mathbf{x}$ 求导并令其为零：
$$
\nabla_{\mathbf{x}} L(\mathbf{x}, \nu) = Q\mathbf{x} + q + A^T\nu = 0
$$
解出使拉格朗日函数最小化的 $\mathbf{x}$，我们称之为 $\mathbf{x}^*(\nu)$：
$$
\mathbf{x}^*(\nu) = -Q^{-1}(A^T\nu + q)
$$
将这个 $\mathbf{x}^*(\nu)$ 代回拉格朗日函数表达式，便得到对偶函数 $g(\nu)$ 的封闭形式：
$$
g(\nu) = L(\mathbf{x}^*(\nu), \nu) = -\frac{1}{2}(A^T\nu + q)^T Q^{-1} (A^T\nu + q) - \mathbf{b}^T\nu
$$
这表明，对于一个凸二次规划问题，其对偶函数是关于对偶变量 $\nu$ 的另一个（凹）二次函数。

例如，考虑最小化 $f(x_1, x_2) = x_1^2 + 2x_2^2$ 满足 $x_1 + x_2 = 3$ 。该问题可写成矩阵形式，其中 $Q = \begin{pmatrix} 2 & 0 \\ 0 & 4 \end{pmatrix}$，$q = \mathbf{0}$，$A = \begin{pmatrix} 1 & 1 \end{pmatrix}$，$\mathbf{b} = 3$。利用上述通用公式，我们可以计算出对偶函数为 $g(\lambda) = -\frac{3}{8}\lambda^2 - 3\lambda$。

#### 含[不等式约束](@entry_id:176084)的问题

当问题包含[不等式约束](@entry_id:176084)时，计算方法类似，但对偶变量需要满足非负条件。考虑一个[二阶锥规划 (SOCP)](@entry_id:637013) 问题：最小化 $c^T x$ 满足 $\|x\|_2 \le r$ 。

该问题的[不等式约束](@entry_id:176084)为 $f_1(x) = \|x\|_2 - r \le 0$。[拉格朗日函数](@entry_id:174593)为 $L(x, \lambda) = c^T x + \lambda(\|x\|_2 - r)$，其中 $\lambda \ge 0$。对[偶函数](@entry_id:163605)为：
$$
g(\lambda) = \inf_x L(x, \lambda) = \inf_x (c^T x + \lambda\|x\|_2 - \lambda r) = -\lambda r + \inf_x (c^T x + \lambda\|x\|_2)
$$
求解 $\inf_x (c^T x + \lambda\|x\|_2)$ 需要一些[凸分析](@entry_id:273238)的知识。这个表达式的[下确界](@entry_id:140118)可以通过分析其关于 $x$ 的[次梯度](@entry_id:142710)得到。我们发现：
*   如果 $\|c\|_2 \le \lambda$，那么下确界在 $x=0$ 处取得，值为 $0$。
*   如果 $\|c\|_2 > \lambda$，函数是无下界的，其值为 $-\infty$。

因此，对偶函数为：
$$
g(\lambda) = \begin{cases} -\lambda r & \text{若 } \lambda \ge \|c\|_2 \\ -\infty & \text{若 } 0 \le \lambda < \|c\|_2 \end{cases}
$$
这个例子展示了如何处理非多项式形式的函数，并再次突出了[有效域](@entry_id:636189)的概念。

### 对偶函数的基本性质

[拉格朗日对偶函数](@entry_id:637331)具有两个至关重要的性质，无论原问题是否为凸问题，这两个性质都成立。

#### 作为下界：[弱对偶](@entry_id:163073)性

对偶函数的第一个关键性质是，对于任意满足 $\lambda \ge 0$ 的 $(\lambda, \nu)$，函数值 $g(\lambda, \nu)$ 总是原问题最优值 $p^*$ 的一个下界。这就是**[弱对偶](@entry_id:163073)性 (weak duality)** 定理 。

**定理 ([弱对偶](@entry_id:163073)性)**：令 $p^*$ 为原问题的最优值，则对于任意 $\lambda \ge 0$ 和任意 $\nu$，我们有 $g(\lambda, \nu) \le p^*$。

*证明*：令 $\tilde{x}$ 为原问题的任意一个可行点，即 $f_i(\tilde{x}) \le 0$ 且 $h_j(\tilde{x}) = 0$。再令 $(\lambda, \nu)$ 为任意一个对偶可行点，即 $\lambda_i \ge 0$ 对所有 $i$ 成立。我们可以评估在 $(\tilde{x}, \lambda, \nu)$ 处的[拉格朗日函数](@entry_id:174593)值：
$$
L(\tilde{x}, \lambda, \nu) = f_0(\tilde{x}) + \sum_{i=1}^{m} \lambda_i f_i(\tilde{x}) + \sum_{j=1}^{p} \nu_j h_j(\tilde{x})
$$
由于 $\tilde{x}$ 是原问题可行的，而 $(\lambda, \nu)$ 是对偶可行的，我们有：
*   $\lambda_i \ge 0$ 且 $f_i(\tilde{x}) \le 0 \implies \lambda_i f_i(\tilde{x}) \le 0$。
*   $h_j(\tilde{x}) = 0 \implies \nu_j h_j(\tilde{x}) = 0$。

因此，拉格朗日函数中的两个和项都是非正的，我们得到：
$$
L(\tilde{x}, \lambda, \nu) \le f_0(\tilde{x})
$$
根据对偶函数的定义，$g(\lambda, \nu)$ 是 $L(x, \lambda, \nu)$ 对所有 $x \in \mathcal{D}$ 的[下确界](@entry_id:140118)，所以它必然小于或等于在特定可行点 $\tilde{x}$ 处的值：
$$
g(\lambda, \nu) = \inf_{x \in \mathcal{D}} L(x, \lambda, \nu) \le L(\tilde{x}, \lambda, \nu)
$$
结合上面两个不等式，我们得到 $g(\lambda, \nu) \le f_0(\tilde{x})$。这个结论对所有原问题可行点 $\tilde{x}$ 都成立，因此它也必须对最优值 $p^* = \inf \{f_0(x) \mid x \text{ is feasible}\}$ 成立。故 $g(\lambda, \nu) \le p^*$。

[弱对偶](@entry_id:163073)性是一个非常强大的结论，因为它不需要任何关于问题[凸性](@entry_id:138568)的假设。它为我们提供了一种系统性寻找原问题最优值下界的方法。

#### [凹性](@entry_id:139843)

对偶函数的第二个关键性质是它**总是[凹函数](@entry_id:274100) (concave function)**，这同样与原问题是否凸无关。

一个函数 $g$ 是[凹函数](@entry_id:274100)，当且仅当它的定义域是凸集，并且对于其定义域中的任意两点 $\theta_1, \theta_2$ 和任意 $\alpha \in [0,1]$，满足 $g(\alpha \theta_1 + (1-\alpha)\theta_2) \ge \alpha g(\theta_1) + (1-\alpha)g(\theta_2)$。

*证明*：对[偶函数](@entry_id:163605) $g(\lambda, \nu)$ 是关于 $(\lambda, \nu)$ 的一系列[仿射函数](@entry_id:635019)（affine functions）的逐点[下确界](@entry_id:140118)：
$$
L(x, \lambda, \nu) = f_0(x) + \lambda^T f(x) + \nu^T h(x)
$$
对于每个固定的 $x$，这个函数是 $(\lambda, \nu)$ 的[仿射函数](@entry_id:635019)。由于一系列[仿射函数](@entry_id:635019)的逐点下确界是[凹函数](@entry_id:274100)，所以 $g(\lambda, \nu)$ 是[凹函数](@entry_id:274100)。

这个性质至关重要，因为无论原问题多么复杂、是否为凸，我们接下来要定义的“[对偶问题](@entry_id:177454)”（即最大化对[偶函数](@entry_id:163605)）总是一个凸[优化问题](@entry_id:266749)（因为最大化一个[凹函数](@entry_id:274100)等价于最小化一个[凸函数](@entry_id:143075) $-g$）。

为了更深刻地体会这一点，让我们看一个原问题非凸的例子 。考虑在[单位圆](@entry_id:267290) $x^2 + y^2 = 1$上最小化非[凸函数](@entry_id:143075) $f(x, y) = x^2 - 2y^2$。拉格朗日函数为：
$$
L(x, y, \lambda) = x^2 - 2y^2 + \lambda(x^2 + y^2 - 1) = (1+\lambda)x^2 + (\lambda-2)y^2 - \lambda
$$
对偶函数 $g(\lambda) = \inf_{x,y} L(x,y,\lambda)$。要使这个下确界不为 $-\infty$，二次项的系数必须为非负，即 $1+\lambda \ge 0$ 和 $\lambda-2 \ge 0$，这要求 $\lambda \ge 2$。当此条件满足时，[下确界](@entry_id:140118)在 $x=0, y=0$ 处取得，值为 $g(\lambda) = -\lambda$。因此，
$$
g(\lambda) = \begin{cases} -\lambda & \text{若 } \lambda \ge 2 \\ -\infty & \text{若 } \lambda < 2 \end{cases}
$$
这个对[偶函数](@entry_id:163605) $g(\lambda) = -\lambda$ (在其有效域 $\lambda \ge 2$上) 显然是一个[凹函数](@entry_id:274100)（实际上是线性的），尽管原问题的[目标函数](@entry_id:267263)是非凸的。

#### 不可微性与次梯度

尽管对[偶函数](@entry_id:163605)总是凹的，但它并不总是可微的。对偶函数的不[可微性](@entry_id:140863)通常发生在拉格朗日函数的最小点不唯一时。

考虑一个精巧的例子 ：最小化 $f(x)=0$ 满足 $x \in [-1,1]$ 和 $x=0$。我们可以将域约束 $x \in [-1,1]$ 视为目标函数的一部分，即最小化 $\mathbb{I}_{[-1,1]}(x)$（指示函数），约束为 $x=0$。拉格朗日函数为 $L(x, \lambda) = \mathbb{I}_{[-1,1]}(x) + \lambda x$。对[偶函数](@entry_id:163605)为：
$$
g(\lambda) = \inf_{x \in [-1,1]} (\lambda x) = -|\lambda|
$$
这个对[偶函数](@entry_id:163605) $g(\lambda) = -|\lambda|$ 在 $\lambda=0$ 处有一个[尖点](@entry_id:636792)，是不可微的。这个不可微点恰好是其[最大值点](@entry_id:634610)。

在 $\lambda=0$ 处，$L(x,0) = \mathbb{I}_{[-1,1]}(x)$。对于所有 $x \in [-1,1]$， $L(x,0)$ 都等于其[下确界](@entry_id:140118) $0$。这意味着在 $\lambda=0$ 时，最小化拉格朗日函数的 $x^*$ 不是唯一的，而是整个区间 $[-1,1]$。

一般地，我们有以下重要结论：
*   如果在某点 $\lambda$，最小化 $L(x, \lambda)$ 的 $x^*$ 是唯一的，那么 $g$ 在该点 $\lambda$ 可微，并且其梯度为 $\nabla g(\lambda) = (f_1(x^*), \dots, f_m(x^*))$（以只有[不等式约束](@entry_id:176084)为例）。
*   如果在某点 $\lambda$，最小化 $L(x, \lambda)$ 的 $x^*$ 不唯一，那么 $g$ 在该点 $\lambda$ 通常是不可微的。此时，我们使用**次梯度 (subgradient)** 的概念来描述其局部行为。$g$ 在 $\lambda$ 的[次微分](@entry_id:175641) $\partial g(\lambda)$ 是一个集合，包含了所有满足 $g(z) \le g(\lambda) + s^T(z-\lambda)$ 的向量 $s$。可以证明，在 $L(x,\lambda)$ 的所有最小点 $x^*$ 集合中，对应的约束函数值向量 $(f_1(x^*), \dots, f_m(x^*))$ 的[凸包](@entry_id:262864)构成了 $\partial g(\lambda)$。

### 对偶问题与[对偶间隙](@entry_id:173383)

#### [拉格朗日对偶问题](@entry_id:637210)

既然对[偶函数](@entry_id:163605) $g(\lambda, \nu)$ 为原问题最优值 $p^*$ 提供了一个下界，一个自然的想法是去寻找这个下界的“最佳”值，即下界的最大值。这个问题被称为**[拉格朗日对偶问题](@entry_id:637210) (Lagrange dual problem)**：
$$
\begin{array}{ll}
\text{最大化} & g(\lambda, \nu) \\
\text{满足} & \lambda \ge 0
\end{array}
$$
这是一个凸[优化问题](@entry_id:266749)，因为目标函数 $g$ 是凹的，且约束 $\lambda \ge 0$ 是[凸集](@entry_id:155617)。我们将对偶问题的最优值记为 $d^*$。

由[弱对偶](@entry_id:163073)性可知，$g(\lambda, \nu) \le p^*$ 对所有对偶可行的 $(\lambda, \nu)$ 都成立，因此：
$$
d^* = \sup_{\lambda \ge 0, \nu} g(\lambda, \nu) \le p^*
$$
这个关系总是成立的。

#### 强对偶性与[对偶间隙](@entry_id:173383)

$p^* - d^*$ 这个差值被称为**[对偶间隙](@entry_id:173383) (duality gap)**。
*   如果[对偶间隙](@entry_id:173383)为正，即 $p^* > d^*$，我们称之为**[弱对偶](@entry_id:163073) (weak duality)**。
*   如果[对偶间隙](@entry_id:173383)为零，即 $p^* = d^*$，我们称之为**强对偶 (strong duality)**。

强对偶性是一个非常理想的性质，但它并不总是成立。通常，要保证强对偶性，原问题需要是凸问题，并且满足某些额外的**[约束规范](@entry_id:635836) (constraint qualification)** 条件。

一个著名的[约束规范](@entry_id:635836)是 **Slater 条件 (Slater's condition)**。对于一个凸[优化问题](@entry_id:266749)，如果存在一个点 $x$ 使得所有[不等式约束](@entry_id:176084)都严格成立（即 $f_i(x) < 0$）并且所有仿射[等式约束](@entry_id:175290)成立，那么 Slater 条件成立，进而强对偶性成立。例如，在前面的 SOCP 问题中 ，如果 $r>0$，那么点 $x=0$ 就是一个严格可行点（因为 $\|0\|_2 = 0 < r$），因此 Slater 条件成立，强对偶性保证 $p^* = d^*$。

当强对偶性不成立时，就会出现非零的[对偶间隙](@entry_id:173383)。这通常发生在非凸问题中，或者即使问题是凸的但[约束规范](@entry_id:635836)不满足时。一个非凸问题的例子 ：最小化一个非[凸函数](@entry_id:143075) $f(x)$（在 $x=0$ 处为 $1$，否则为 $0$），约束为 $x^2 \le 0$。
*   原问题的可行集只有 $x=0$，因此 $p^*=f(0)=1$。
*   可以计算出其对[偶函数](@entry_id:163605)恒为 $g(\lambda)=0$，因此 $d^*=0$。
*   [对偶间隙](@entry_id:173383)为 $p^* - d^* = 1 - 0 = 1$。这里存在一个非零的[对偶间隙](@entry_id:173383)。

### [对偶变量](@entry_id:143282)的解释及进阶主题

#### 灵敏度分析

除了提供下界，[对偶变量](@entry_id:143282)还有一个深刻的物理解释：它们代表了原问题最优值对约束变化的**灵敏度 (sensitivity)**。

考虑一个被[参数化](@entry_id:272587)的原问题，其约束的右侧是变量 $b$：最小化 $f_0(x)$ subject to $f_i(x) \le b_i$。其最优值是 $b$ 的函数，我们称之为值函数 $p^*(b)$。假设强对偶性成立，并且对偶最优解 $\lambda^*$ 是唯一的。那么，我们有：
$$
\lambda_i^* = -\frac{\partial p^*}{\partial b_i}(b)
$$
这个结论意味着，[对偶变量](@entry_id:143282) $\lambda_i^*$ 度量了当第 $i$ 个约束的边界 $b_i$ 发生微小变化时，原问题的最优值 $p^*$ 会如何变化。如果 $\lambda_i^*$ 很大，说明第 $i$ 个约束是一个“瓶颈”，稍微“放松”这个约束（即增加 $b_i$）可以显著地降低（即改善）最优目标值。这个性质在经济学和工程设计中有广泛应用，$\lambda^*$ 常被称为资源的“影子价格” 。

#### 与 Fenchel 对偶的联系

对于更熟悉[凸分析](@entry_id:273238)的学生，[拉格朗日对偶](@entry_id:638042)理论可以被看作是更广泛的 Fenchel [对偶理论](@entry_id:143133)的一个特例。考虑一个[复合优化](@entry_id:165215)问题 ：
$$
\text{最小化} \quad f(x) + g(Ax)
$$
其中 $f$ 和 $g$ 是[凸函数](@entry_id:143075)。我们可以通过引入新变量 $u=Ax$ 将其转化为一个[等式约束](@entry_id:175290)问题：
$$
\text{最小化} \quad f(x) + g(u) \quad \text{满足} \quad Ax-u=0
$$
对此问题构造[拉格朗日对偶函数](@entry_id:637331)，经过推导可以发现，其对[偶函数](@entry_id:163605)可以用**Fenchel 共轭 (Fenchel conjugate)** 来表示：
$$
g_{\text{Lag}}(\lambda) = -f^*(-A^T\lambda) - g^*(\lambda)
$$
其中 $f^*$ 和 $g^*$ 分别是 $f$ 和 $g$ 的 Fenchel 共轭。最大化 $g_{\text{Lag}}(\lambda)$ 的对偶问题正是 Fenchel [对偶理论](@entry_id:143133)给出的[对偶问题](@entry_id:177454)。此外，在这种框架下，[最优性条件](@entry_id:634091)可以被优雅地表达为[次梯度](@entry_id:142710)的关系：如果强对偶性成立，那么存在原最优解 $x^*$ 和对偶最优解 $\lambda^*$ 满足：
$$
-A^T\lambda^* \in \partial f(x^*) \quad \text{并且} \quad \lambda^* \in \partial g(Ax^*)
$$
这些条件是 KKT 条件在非光滑情况下的自然推广，构成了现代凸[优化算法](@entry_id:147840)设计的理论基础。

本章介绍了[拉格朗日对偶函数](@entry_id:637331)，从其定义、计算方法到其深刻的理论性质（[弱对偶](@entry_id:163073)性、[凹性](@entry_id:139843)）和实际应用（[灵敏度分析](@entry_id:147555)）。理解对[偶函数](@entry_id:163605)是掌握[拉格朗日对偶](@entry_id:638042)理论，乃至整个[优化理论](@entry_id:144639)的关键一步。在下一章，我们将利用对偶函数来阐述 KKT [最优性条件](@entry_id:634091)，这是[约束优化理论](@entry_id:635923)的顶峰。