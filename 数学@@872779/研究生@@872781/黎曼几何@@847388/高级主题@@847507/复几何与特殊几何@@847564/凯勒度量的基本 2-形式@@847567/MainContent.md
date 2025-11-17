## 引言
[凯勒几何](@entry_id:160314)是现代数学的璀璨明珠，它优雅地坐落在[黎曼几何](@entry_id:160508)、[复几何](@entry_id:159080)与[辛几何](@entry_id:160783)的[交叉](@entry_id:147634)路口，融合了这三大领域的思想与工具。这一理论的核心与灵魂，便是**[基本2-形式](@entry_id:183276)**（fundamental 2-form），通常记为 $\omega$。这个看似简单的对象，实则蕴含了凯勒流形丰富的几何与拓扑结构，是理解其“刚性”与深刻性质的关键。

然而，从一个一般的[黎曼流形](@entry_id:261160)到一个结构精妙的[凯勒流形](@entry_id:161192)，其间存在着巨大的鸿沟。本文旨在填补这一认知上的差距，系统地探讨：一个几乎埃尔米特[流形](@entry_id:153038)上的度量需要满足何种特殊条件才能成为凯勒度量？这些条件又是如何通过[基本2-形式](@entry_id:183276)来表达的？以及这些条件一旦满足，会带来怎样深远的几何后果？

在接下来的章节中，我们将踏上一段从定义到应用的探索之旅。在“**原理和机制**”一章，我们将严格定义[基本2-形式](@entry_id:183276)，并揭示[凯勒条件](@entry_id:637291)——即该形式的闭合性——如何成为区分[凯勒流形](@entry_id:161192)与其他[流形](@entry_id:153038)的分水岭，同时我们也会探讨其多种等价的几何刻画。随后，在“**应用与跨学科联系**”一章，我们将展示这一形式如何作为一种强大的工具，在计算体积、探测拓扑结构、解决[偏微分方程](@entry_id:141332)以及连接[规范场](@entry_id:159627)论和弦理论等前沿物理领域中发挥核心作用。最后，“**动手实践**”部分将提供一系列具体的计算问题，帮助读者将理论知识转化为实践技能。

## 原理和机制

[凯勒流形](@entry_id:161192)的概念处在[黎曼几何](@entry_id:160508)、[复几何](@entry_id:159080)和[辛几何](@entry_id:160783)的[交叉点](@entry_id:147634)。本节将深入探讨其核心结构——[基本2-形式](@entry_id:183276)——的定义、性质及其在确定[流形](@entry_id:153038)几何中的基础性作用。本章将系统地阐述将一个几乎埃尔米特结构提升为凯勒结构所需的条件，并揭示这些条件所带来的深刻几何后果。

### 几乎埃尔米特[流形](@entry_id:153038)的基本形式

[凯勒几何](@entry_id:160314)的出发点是**几乎埃尔米特[流形](@entry_id:153038)** (almost Hermitian manifold)。一个几乎埃尔米特[流形](@entry_id:153038)是一个三元组 $(M, g, J)$，其中 $M$ 是一个偶数维的光滑实[流形](@entry_id:153038)，其维度为 $2n$，$J$ 是 $M$ 上的一个**几乎[复结构](@entry_id:269128)** (almost complex structure)，$g$ 是 $M$ 上的一个[黎曼度量](@entry_id:754359)。这三个元素必须满足以下条件：

1.  $J$ 是一个 $(1,1)$ 型张量场，在每个切空间 $T_pM$ 上都满足 $J^2 = -I$，其中 $I$ 是[恒等变换](@entry_id:264671)。这赋予了每个[切空间](@entry_id:199137)一个[复向量空间](@entry_id:264355)的结构。
2.  $g$ 是一个[黎曼度量](@entry_id:754359)，即每个[切空间](@entry_id:199137)上的一个光滑变化的对称、正定[内积](@entry_id:158127)。
3.  $g$ 和 $J$ 是**相容的** (compatible)，这意味着对于任意向量场 $X, Y$，都有 $g(JX, JY) = g(X, Y)$。此条件表明 $J$ 是关于度量 $g$ 的一个[等距同构](@entry_id:273188)。

在任何几乎埃尔米特[流形](@entry_id:153038)上，我们可以定义一个核心对象，称为**基本 2-形式** (fundamental 2-form)，通常记为 $\omega$。它通过度量 $g$ 和几乎复结构 $J$ 定义如下：
$$
\omega(X, Y) = g(JX, Y)
$$
对于任意向量场 $X, Y$ [@problem_id:3034906]。

这个对象为何是一个 2-形式？首先，由于 $g$ 的[双线性](@entry_id:146819)和 $J$ 的线性，$\omega$ 在其每个变量中都是线性的。其次，我们需要验证它的反对称性，即 $\omega(X, Y) = -\omega(Y, X)$。利用度量的对称性和 $J$ 的相容性，我们可以推导如下 [@problem_id:1648866]：
$$
\omega(Y, X) = g(JY, X) = g(X, JY)
$$
利用[相容性条件](@entry_id:637057) $g(U,V) = g(JU,JV)$，令 $U=X$ 和 $V=JY$，我们得到：
$$
g(X, JY) = g(JX, J(JY)) = g(JX, J^2Y) = g(JX, -Y) = -g(JX, Y)
$$
结合起来，我们有 $\omega(Y, X) = -g(JX, Y) = -\omega(X, Y)$。因此，$\omega$ 确实是一个[微分](@entry_id:158718) 2-形式。

这个基本 2-形式 $\omega$ 还有一个至关重要的性质：它在 $J$ 的作用下是不变的，即**$J$-不变性** (J-invariance)。这意味着 $\omega(JX, JY) = \omega(X, Y)$。其证明过程如下 [@problem_id:1648866]：
$$
\omega(JX, JY) = g(J(JX), JY) = g(J^2X, JY) = g(-X, JY) = -g(X, JY)
$$
从我们刚才推导反对称性的中间步骤可知，$-g(X, JY) = g(JX, Y) = \omega(X, Y)$。这个[不变性](@entry_id:140168)意味着 $\omega$ 是一个 **(1,1)-形式**，也就是说，在局部复[坐标系](@entry_id:156346)下，它只包含 $dz^\alpha \wedge d\bar{z}^\beta$ 类型的项。

度量 $g$、几乎[复结构](@entry_id:269128) $J$ 和基本形式 $\omega$ 构成了一个紧密联系的“三位一体”结构。我们不仅可以从 $g$ 和 $J$ 定义 $\omega$，还可以反过来从 $\omega$ 和 $J$ 中恢复度量 $g$。其关系式为：
$$
g(X, Y) = \omega(X, JY)
$$
这是一个非常有用的关系，它表明了黎曼结构（由 $g$ 代表）和辛结构（由 $\omega$ 代表）是如何通过[复结构](@entry_id:269128) $J$ 相互关联的。

**示例：从 $\omega$ 和 $J$ 恢复度量**

考虑著名的[庞加莱上半平面](@entry_id:264005) $M = \{(x, y) \in \mathbb{R}^2 \mid y > 0\}$。这是一个[二维流形](@entry_id:188198)，我们可以为其配备一个几乎[复结构](@entry_id:269128) $J$ 和一个 [2-形式](@entry_id:188008) $\omega$。设切空间的基为 $\{\partial_x, \partial_y\}$，定义 $J$ 的作用为 $J(\partial_x) = \partial_y$ 和 $J(\partial_y) = -\partial_x$。给定 [2-形式](@entry_id:188008)为 $\omega = \frac{1}{y^2} dx \wedge dy$。我们的任务是利用关系 $g(X, Y) = \omega(X, JY)$ 找[出度](@entry_id:263181)量张量 $g$ 的分量 $g_{xx}, g_{xy}, g_{yy}$ [@problem_id:1648843]。

首先，我们计算 $\omega$ 在[基向量](@entry_id:199546)对上的值：
$\omega(\partial_x, \partial_y) = \frac{1}{y^2} (dx \wedge dy)(\partial_x, \partial_y) = \frac{1}{y^2}(dx(\partial_x)dy(\partial_y) - dx(\partial_y)dy(\partial_x)) = \frac{1}{y^2}$。
由于[反对称性](@entry_id:261893)，$\omega(\partial_y, \partial_x) = -\frac{1}{y^2}$，且 $\omega(\partial_x, \partial_x) = \omega(\partial_y, \partial_y) = 0$。

现在，我们计算度量分量：
1.  $g_{xx} = g(\partial_x, \partial_x) = \omega(\partial_x, J\partial_x) = \omega(\partial_x, \partial_y) = \frac{1}{y^2}$
2.  $g_{yy} = g(\partial_y, \partial_y) = \omega(\partial_y, J\partial_y) = \omega(\partial_y, -\partial_x) = -\omega(\partial_y, \partial_x) = \frac{1}{y^2}$
3.  $g_{xy} = g(\partial_x, \partial_y) = \omega(\partial_x, J\partial_y) = \omega(\partial_x, -\partial_x) = 0$

因此，度量张量的矩阵形式为 $\begin{pmatrix} 1/y^2  0 \\ 0  1/y^2 \end{pmatrix}$。这正是庞加莱度量。这个例子清晰地展示了 $g, J, \omega$ 之间的相互构造关系。

### [凯勒条件](@entry_id:637291)：从埃尔米特到凯勒

几乎埃尔米特[流形](@entry_id:153038)是一个非常广泛的类别。为了得到更精细和更强大的几何结构，我们需要施加额外的条件。这引导我们进入一个结构层次：
**几乎埃尔米特 $\subset$ 几乎凯勒**
**$\cap$** **$\cap$**
**埃尔米特 $\subset$ 凯勒**

一个**[凯勒流形](@entry_id:161192)** (Kähler manifold) 是一个满足两个关键条件的几乎埃尔米特[流形](@entry_id:153038)：

1.  **$J$ 的可积性 (Integrability of $J$)**: 几乎[复结构](@entry_id:269128) $J$ 必须是“真正的”复结构，即它来自于一个[复流形](@entry_id:159076)结构。根据 Newlander-Nirenberg 定理，这等价于 $J$ 的 **Nijenhuis 张量** $N_J$ 为零。满足此条件的几乎埃尔米特[流形](@entry_id:153038)称为 **埃尔米特[流形](@entry_id:153038)** (Hermitian manifold)。

2.  **$\omega$ 的闭性 (Closure of $\omega$)**: 基本 2-形式 $\omega$ 必须是闭形式，即其外微分 $d\omega = 0$。满足此条件的几乎埃尔米特[流形](@entry_id:153038)称为**几乎凯勒流形** (almost Kähler manifold)。

一个[凯勒流形](@entry_id:161192)就是一个既是埃尔米特[流形](@entry_id:153038)又是几乎[凯勒流形](@entry_id:161192)的几何对象。这两个条件都是非常强的约束，它们共同作用，产生了[凯勒几何](@entry_id:160314)的丰富结构。

仅仅是埃尔米特[流形](@entry_id:153038)并不意味着它是[凯勒流形](@entry_id:161192)。[凯勒条件](@entry_id:637291) $d\omega = 0$ 是一个额外的、严格的约束。为了说明这一点，我们可以构造一个紧致[复流形](@entry_id:159076)（因此是埃尔米特的），它上面可以有非凯勒的[埃尔米特度量](@entry_id:202337)，并且更强的是，它根本不能容纳任何凯勒度量。

**范例：霍普夫[流形](@entry_id:153038)**

一个经典的例子是 **霍普夫[流形](@entry_id:153038)** (Hopf manifold) $H_\lambda$ [@problem_id:3031599]。对于 $n \ge 2$ 和一个复数 $\lambda$ 且 $|\lambda| > 1$，霍普夫[流形](@entry_id:153038)定义为商空间 $H_\lambda = (\mathbb{C}^n \setminus \{0\}) / \Gamma$，其中 $\Gamma$是由映射 $z \mapsto \lambda z$ 生成的离散群。这是一个紧致复流形。

现在，我们在其覆盖空间 $\mathbb{C}^n \setminus \{0\}$ 上考虑一个[埃尔米特度量](@entry_id:202337)，其基本形式为：
$$
\omega = \frac{i}{2|z|^2} \sum_{k=1}^n dz_k \wedge d\bar{z}_k
$$
其中 $|z|^2 = \sum_k |z_k|^2$。在变换 $z \mapsto \lambda z$ 下，$dz_k \mapsto \lambda dz_k$, $d\bar{z}_k \mapsto \bar{\lambda} d\bar{z}_k$，而分母 $|z|^2 \mapsto |\lambda|^2|z|^2$。因此，$\omega$ 的分子和分母都乘以了一个因子 $|\lambda|^2$，使得 $\omega$ 在变换下保持不变。这意味着 $\omega$ 可以完美地下降到[商空间](@entry_id:274314) $H_\lambda$ 上，成为一个良定义的[埃尔米特度量](@entry_id:202337)。

然而，这个度量不是凯勒度量。我们可以计算 $d\omega$。令 $f(z, \bar{z}) = |z|^{-2}$，$\eta = \frac{i}{2} \sum dz_k \wedge d\bar{z}_k$。我们知道 $\eta$ 是 $\mathbb{C}^n$ 上的标准平坦凯勒形式，所以 $d\eta = 0$。因此：
$$
d\omega = d(f \eta) = df \wedge \eta + f d\eta = df \wedge \eta = d(|z|^{-2}) \wedge \eta
$$
由于 $df$ 在 $\mathbb{C}^n \setminus \{0\}$ 上非零，并且 $n \ge 2$，这个 3-形式 $d\omega$ 也非零。所以这个[埃尔米特度量](@entry_id:202337)不是凯勒的。

更重要的是，霍普夫[流形](@entry_id:153038)根本不可能容纳**任何**凯勒度量。这是一个深刻的拓扑事实。霍普夫[流形](@entry_id:153038) $H_\lambda$ 微分同胚于 $S^{2n-1} \times S^1$。它的第一个[贝蒂数](@entry_id:153109) $b_1(H_\lambda) = 1$。然而，根据[霍奇理论](@entry_id:161814)的一个基本结论，任何紧致[凯勒流形](@entry_id:161192)的奇数阶贝蒂数（如 $b_1$）必须是偶数。由于 $b_1(H_\lambda) = 1$ 是奇数，霍普夫[流形](@entry_id:153038)不满足这个拓扑必要条件，因此它不可能是凯勒流形。这也意味着它不可能拥有[凯勒-爱因斯坦度量](@entry_id:270601)或[常标量曲率](@entry_id:186408)凯勒 (cscK) 度量，因为这些都是凯勒度量的特例。

这个例子有力地证明了[凯勒条件](@entry_id:637291) $d\omega=0$ 是一个非常强的全局拓扑约束，而不仅仅是一个局部的度量属性。

### 凯勒流形的等价刻画

凯勒流形的美妙之处在于它的定义可以通过多种看似不同但实则等价的方式来表述。这些等价性是[凯勒几何](@entry_id:160314)中许多“奇迹”的根源。对于一个几乎埃尔米特[流形](@entry_id:153038) $(M, g, J)$，以下陈述是等价的 [@problem_id:3034906] [@problem_id:2996805]：

1.  $(M, g, J)$ 是一个[凯勒流形](@entry_id:161192)（即 $N_J=0$ 且 $d\omega=0$）。
2.  关于度量 $g$ 的[列维-奇维塔联络](@entry_id:161107) $\nabla$ 与 $J$ 相容，即 $\nabla J = 0$。

条件 $\nabla J = 0$ 意味着[复结构](@entry_id:269128) $J$ 在沿[流形](@entry_id:153038)任意曲线进行平行移动时保持不变。这在几何上是一个极强的条件，它将黎曼结构（由 $\nabla$ 代表）和[复结构](@entry_id:269128)（由 $J$ 代表）紧密地锁在一起。如果在一个埃尔米特[流形](@entry_id:153038)上（即已假定 $N_J = 0$），那么条件 $d\omega = 0$ 就等价于 $\nabla J = 0$。

这个平行性条件还与**[和乐群](@entry_id:191471)** (holonomy group) 的概念有关。对于一个 $2n$ 维的黎曼流形，其[列维-奇维塔联络](@entry_id:161107)的和乐群通常是[正交群](@entry_id:152531) $O(2n)$ 的一个[子群](@entry_id:146164)。条件 $\nabla J = 0$ 恰好等价于和乐群被限制在[酉群](@entry_id:138602) $U(n)$ 中。因此，一个埃尔米特[流形](@entry_id:153038)是[凯勒流形](@entry_id:161192)的充要条件是它的[和乐群](@entry_id:191471)是 $U(n)$ 的一个[子群](@entry_id:146164) [@problem_id:2996805]。

另一个至关重要的等价刻画涉及**[凯勒势](@entry_id:154750)** (Kähler potential) 的局部存在性。在任何复流形上，我们可以引入 Dolbeault 算子 $\partial$ 和 $\bar{\partial}$，它们满足 $d = \partial + \bar{\partial}$。在局部全纯坐标 $\{z^\alpha\}$ 下，基本 2-形式可以写为：
$$
\omega = i \sum_{\alpha, \beta} g_{\alpha\bar{\beta}} dz^\alpha \wedge d\bar{z}^\beta
$$
其中 $g_{\alpha\bar{\beta}} = g(\frac{\partial}{\partial z^\alpha}, \frac{\partial}{\partial \bar{z}^\beta})$ 是度量的埃尔米特分量 [@problem_id:2996807]。

现在，假设存在一个**局部**的光滑实值函数 $\phi$，称为 **[凯勒势](@entry_id:154750)**，使得度量分量可以表示为它的二阶[混合偏导数](@entry_id:139334)：
$$
g_{\alpha\bar{\beta}} = \frac{\partial^2 \phi}{\partial z^\alpha \partial\bar{z}^\beta}
$$
在这种情况下，基本形式 $\omega$ 可以简洁地写成：
$$
\omega = i \sum_{\alpha, \beta} \frac{\partial^2 \phi}{\partial z^\alpha \partial\bar{z}^\beta} dz^\alpha \wedge d\bar{z}^\beta = i \partial\bar{\partial}\phi
$$
这个表达形式有一个惊人的推论：$\omega$ 自动是闭的。这是因为外微分 $d$ 作用在其上时，我们有：
$$
d\omega = d(i\partial\bar{\partial}\phi) = i(\partial + \bar{\partial})(\partial\bar{\partial}\phi) = i(\partial^2\bar{\partial}\phi + \bar{\partial}\partial\bar{\partial}\phi)
$$
利用算子恒等式 $\partial^2 = 0$, $\bar{\partial}^2 = 0$ 以及 $\partial\bar{\partial} = -\bar{\partial}\partial$，我们得到：
$$
d\omega = i(\partial^2(\bar{\partial}\phi) - \bar{\partial}^2(\partial\phi)) = i(0 - 0) = 0
$$
因此，只要度量能从一个势函数导出，它就自动是凯勒度量 [@problem_id:2996791] [@problem_id:2996807]。反之，著名的 **$\partial\bar{\partial}$-引理** ($\partial\bar{\partial}$-lemma) 告诉我们，在一个紧致凯勒流形上（更一般地，在满足 $\partial\bar{\partial}$-引理的[流形](@entry_id:153038)上），任何实的、d-闭的 (1,1)-形式（如 $\omega$），如果它也是 d-恰当的，那么它就是 $\partial\bar{\partial}$-恰当的。对于 $\omega$ 本身，$d\omega=0$ 局部上就保证了这种势函数 $\phi$ 的存在。

**示例：Fubini-Study 度量势**

让我们在 $\mathbb{C}^2$ 上考虑一个具体的[凯勒势](@entry_id:154750) $\phi(z,w) = \ln(1 + |z|^2 + |w|^2)$ [@problem_id:2996791]。这是一个在[复射影空间](@entry_id:268402) $\mathbb{CP}^2$ 上的 Fubini-Study 度量的[势函数](@entry_id:176105)在一个坐标卡上的表达。我们来计算其度量分量 $g_{\alpha\bar{\beta}} = \partial_\alpha \bar{\partial}_\beta \phi$：
$$
g_{z\bar{z}} = \frac{\partial^2 \phi}{\partial z \partial\bar{z}} = \frac{1+|w|^2}{(1+|z|^2+|w|^2)^2}
$$
$$
g_{w\bar{w}} = \frac{\partial^2 \phi}{\partial w \partial\bar{w}} = \frac{1+|z|^2}{(1+|z|^2+|w|^2)^2}
$$
$$
g_{z\bar{w}} = \frac{\partial^2 \phi}{\partial z \partial\bar{w}} = \frac{-z\bar{w}}{(1+|z|^2+|w|^2)^2}
$$
可以验证，这个度量矩阵在 $\mathbb{C}^2$ 上是处处正定的。由于它是由一个势函数导出的，我们无需计算即可断定其对应的基本形式 $\omega = i\partial\bar{\partial}\phi$ 是闭的，因此这是一个凯勒度量。

### 几何推论与应用

[凯勒条件](@entry_id:637291)的强大之处在于它所带来的丰富几何后果。

#### 一维情形：黎曼面

[凯勒条件](@entry_id:637291)在复一维（实二维）时是平凡的。任何一维复流形（即黎曼面）上的任意[埃尔米特度量](@entry_id:202337)都自动是凯勒度量。原因很简单：基本形式 $\omega$ 是一个 2-形式。它的外微分 $d\omega$ 是一个 3-形式。在一个实二维的[流形](@entry_id:153038)上，任何 3-形式都必然为零。因此，$d\omega=0$ 的条件总是满足的 [@problem_id:1648822]。这解释了为什么[凯勒几何](@entry_id:160314)的真正魅力和复杂性是在复维度 $n \ge 2$ 时才显现出来。

#### 凯勒[体积形式](@entry_id:203000)

在[黎曼几何](@entry_id:160508)中，体积由度量 $g$ 确定。在[凯勒几何](@entry_id:160314)中，[体积形式](@entry_id:203000)与基本形式 $\omega$ 有着优美的关系。对于一个复维度为 $n$ 的[凯勒流形](@entry_id:161192)，其[黎曼体积形式](@entry_id:275973) $dV_g$ 可以由 $\omega$ 的 $n$ 次[外积](@entry_id:147029)得到：
$$
dV_g = \frac{1}{n!} \omega^n = \frac{1}{n!} \omega \wedge \dots \wedge \omega
$$
（这里的系数可能因 $\omega$ 的定义而异，但比例关系是核心）。这表明，在凯勒流形上，黎曼体积（测量“大小”）可以完全由辛结构（测量“面积”）确定。

例如，在一个复[二维流形](@entry_id:188198)上，我们有 $dV_g = \frac{1}{2} \omega^2$。我们可以通过直接计算来验证这一点 [@problem_id:2996836]。在[局部坐标](@entry_id:181200)中，$\omega = i \sum_{\alpha, \beta=1}^2 g_{\alpha\bar{\beta}} dz^\alpha \wedge d\bar{z}^\beta$。计算其平方 $\omega \wedge \omega$ 会得到：
$$
\omega^2 = -2 \det(g_{\alpha\bar{\beta}}) dz^1 \wedge d\bar{z}^1 \wedge dz^2 \wedge d\bar{z}^2
$$
将 $dz \wedge d\bar{z} = -2i dx \wedge dy$ 代入，可以发现 $\frac{1}{2}\omega^2 = \det(g_{\alpha\bar{\beta}}) dx^1 \wedge dy^1 \wedge dx^2 \wedge dy^2$。系数 $\det(g_{\alpha\bar{\beta}})$ 正是在这些复坐标诱导的实坐标下度量的[行列式](@entry_id:142978)，这证实了该公式。

#### [里奇形式](@entry_id:183612)与拓扑

[凯勒几何](@entry_id:160314)的另一个深刻结果是[曲率与拓扑](@entry_id:264903)之间的联系。对于一个凯勒度量，其 **里奇张量** $R_{\alpha\bar{\beta}}$ 也可以从[凯勒势](@entry_id:154750)中导出，或者更一般地，由度量[行列式](@entry_id:142978)的对数给出：
$$
R_{\alpha\bar{\beta}} = -\frac{\partial^2}{\partial z^\alpha \partial\bar{z}^\beta} \ln(\det(g_{\mu\bar{\nu}}))
$$
与基本形式 $\omega$ 类似，我们可以定义 **[里奇形式](@entry_id:183612)** (Ricci form) $\rho$：
$$
\rho = i \sum_{\alpha, \beta} R_{\alpha\bar{\beta}} dz^\alpha \wedge d\bar{z}^\beta = -i\partial\bar{\partial} \ln(\det(g_{\mu\bar{\nu}}))
$$
从这个表达式可以看出，[里奇形式](@entry_id:183612) $\rho$ 也是由一个[势函数](@entry_id:176105)（即 $-\ln(\det g)$）通过 $i\partial\bar{\partial}$ 算子得到的。因此，与 $\omega$ 完全相同的原因，[里奇形式](@entry_id:183612)也必须是闭的，即 $d\rho = 0$ [@problem_id:906297]。

[里奇形式](@entry_id:183612)的闭性是一个意义深远的结果。它意味着 $\rho$ 在[德拉姆上同调](@entry_id:158673)群中定义了一个[上同调类](@entry_id:263961) $[\rho]$。一个基本定理指出，这个[上同调类](@entry_id:263961)（经过 $2\pi$ 的归一化后）恰好是[流形](@entry_id:153038)的**[第一陈类](@entry_id:201400)** (first Chern class) $c_1(M)$：
$$
\left[\frac{\rho}{2\pi}\right] = c_1(M) \in H^2(M, \mathbb{R})
$$
这个定理将度量的曲率信息（通过[里奇形式](@entry_id:183612)）与[流形](@entry_id:153038)的[复结构](@entry_id:269128)和拓扑结构（通过陈类）联系起来，是现代微分几何的基石之一。它为诸如[卡拉比-丘流形](@entry_id:159253)（其定义要求 $c_1(M)=0$，从而[里奇形式](@entry_id:183612)为恰当形式）和[凯勒-爱因斯坦度量](@entry_id:270601)的存在性等高级课题打开了大门。