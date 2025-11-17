## 引言
凯勒流形是现代[微分几何](@entry_id:145818)的基石，它在[复几何](@entry_id:159080)、[黎曼几何](@entry_id:160508)与[辛几何](@entry_id:160783)的交汇处构建了一座优雅的桥梁。通过引入一个看似简单的约束条件，[凯勒几何](@entry_id:160314)不仅统一了这些重要的几何结构，还在纯数学的多个分支和[理论物理学](@entry_id:154070)中引发了深刻的革命。然而，对于初学者而言，这些结构之间错综复杂的关系以及其深远影响往往难以把握。本文旨在系统地揭开凯勒流形的神秘面纱，为读者提供一条从基本原理到前沿应用的清晰路径。

在接下来的内容中，我们将首先在“原理与机制”一章中，从[殆复结构](@entry_id:159849)和[厄米度量](@entry_id:202337)出发，详细阐释[凯勒条件](@entry_id:637291)如何将各个部分融合成一个和谐的整体。随后，在“应用与跨学科联系”一章中，我们将探索凯勒流形在[极小曲面](@entry_id:157732)理论、[霍奇理论](@entry_id:161814)、代数几何以及弦理论中的具体应用，展现其强大的理论威力。最后，通过一系列“动手实践”的练习，读者将有机会亲手计算和验证[凯勒几何](@entry_id:160314)中的核心概念，从而巩固所学知识。

## 原理与机制

在深入探讨[凯勒流形](@entry_id:161192)的丰富几何学之前，我们必须首先系统地建立构成其基础的各个结构，并理解它们之间深刻的相互作用。本章将详细阐述[凯勒流形](@entry_id:161192)的核心原理与机制，从复结构和[黎曼度量](@entry_id:754359)的兼容性出发，引出关键的凯勒形式，并最终揭示[凯勒条件](@entry_id:637291)如何将这些元素统一为一个和谐的整体。

### 构成结构：从[复流形](@entry_id:159076)到厄米[流形](@entry_id:153038)

[凯勒几何](@entry_id:160314)的舞台是同时具有[复结构](@entry_id:269128)和[黎曼度量](@entry_id:754359)的[流形](@entry_id:153038)。这两种结构的融合并非简单的叠加，而是通过一个关键的[兼容性条件](@entry_id:201103)实现的，这个条件将[流形](@entry_id:153038)提升为厄米[流形](@entry_id:153038)（Hermitian manifold）。

#### [殆复结构](@entry_id:159849)

几何学中的“复”结构，其本质是在实[切空间](@entry_id:199137)上定义一个线性变换，其行为类似于复数中的乘法因子 $i$。更形式地说，一个光滑流形 $M$ 上的**[殆复结构](@entry_id:159849)** (almost complex structure) 是一个 $(1,1)$ 型[张量场](@entry_id:190170) $J$，即在每一点 $p \in M$ 的切空间 $T_pM$ 上都定义了一个[线性映射](@entry_id:185132) $J_p: T_pM \to T_pM$，并且满足 $J^2 = -\mathrm{Id}$，其中 $\mathrm{Id}$ 是[恒等变换](@entry_id:264671)。

这个条件的直接后果是，[殆复结构](@entry_id:159849) $J$ 在偶数维的实[向量空间](@entry_id:151108)上才可能存在。如果 $M$ 的实维数是 $2n$，那么 $J$ 就将每个切空间 $T_pM$ 变成了一个 $n$ 维的[复向量空间](@entry_id:264355)。

最典型的例子是复平面 $\mathbb{C}$，我们可以将其视为实[二维流形](@entry_id:188198) $\mathbb{R}^2$。在任意一点，切空间由实[坐标基](@entry_id:270149)矢 $\{\frac{\partial}{\partial x}, \frac{\partial}{\partial y}\}$ 张成。一个切向量 $v = a\frac{\partial}{\partial x} + b\frac{\partial}{\partial y}$ 可以与复数 $a+ib$ 等同。[殆复结构](@entry_id:159849) $J$ 的作用被定义为乘以虚数单位 $i$。因此，$J(v)$ 对应于复数 $i(a+ib) = -b+ia$。这在实[基矢](@entry_id:199546)上的作用是：
$J(\frac{\partial}{\partial x}) = \frac{\partial}{\partial y}$
$J(\frac{\partial}{\partial y}) = -\frac{\partial}{\partial x}$
我们可以将 $J$ 表示为一个矩阵：
$$ [J] = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix} $$
直接计算矩阵的平方可以验证 $[J]^2 = \begin{pmatrix} -1  0 \\ 0  -1 \end{pmatrix} = -I$，这与 $i^2 = -1$ 的事实相符。这个简单的计算具体地展示了 $J^2 = -\mathrm{Id}$ 的代数本质。[@problem_id:1648891]

一个[殆复结构](@entry_id:159849)被称为**可积的** (integrable)，如果它是由[流形](@entry_id:153038)上局部全纯坐标图卡产生的。在这种情况下，$J$ 被称为一个**复结构** (complex structure)，而[流形](@entry_id:153038) $(M, J)$ 则是一个**复流形** (complex manifold)。对于[二维流形](@entry_id:188198)（即黎曼面），任何[殆复结构](@entry_id:159849)都是可积的。但在更高维度，可积性是一个需要额外满足的非平凡条件（由[Newlander-Nirenberg定理](@entry_id:158862)刻画）。在后续的讨论中，我们默认处理的都是具有真正复结构的[复流形](@entry_id:159076)。

#### [厄米度量](@entry_id:202337)

在拥有[复结构](@entry_id:269128)的[流形](@entry_id:153038)上，我们希望引入一个黎曼度量 $g$ 来测量长度和角度，并且这个度量需要“尊重”[复结构](@entry_id:269128)。这种尊重体现在所谓的**[兼容性条件](@entry_id:201103)** (compatibility condition) 上：
$$ g(JX, JY) = g(X, Y) $$
对于任意[切向量](@entry_id:265494) $X, Y$ 成立。这个条件意味着 $J$ 是一个关于度量 $g$ 的[等距变换](@entry_id:150881)，即它保持向量的长度和它们之间的角度。一个同时装备了[复结构](@entry_id:269128) $J$ 和与之兼容的黎曼度量 $g$ 的[复流形](@entry_id:159076) $(M, J, g)$ 被称为**厄米[流形](@entry_id:153038)** (Hermitian manifold)。

例如，在 $\mathbb{C}^n \cong \mathbb{R}^{2n}$ 上，我们有标准复结构 $J(\frac{\partial}{\partial x^j}) = \frac{\partial}{\partial y^j}$ 和 $J(\frac{\partial}{\partial y^j}) = -\frac{\partial}{\partial x^j}$，以及标准欧氏度量 $g = \sum_{j=1}^n (dx^j \otimes dx^j + dy^j \otimes dy^j)$。我们可以直接验证其兼容性。例如，对于[基向量](@entry_id:199546) $X = \frac{\partial}{\partial x^j}$ 和 $Y = \frac{\partial}{\partial x^k}$，我们有 $g(X, Y) = \delta_{jk}$。而 $JX = \frac{\partial}{\partial y^j}$，$JY = \frac{\partial}{\partial y^k}$，因此 $g(JX, JY) = g(\frac{\partial}{\partial y^j}, \frac{\partial}{\partial y^k}) = \delta_{jk}$。同样地，可以验证所有其他[基向量](@entry_id:199546)组合。因此，配备了标准欧氏度量的 $\mathbb{C}^n$ 是一个厄米[流形](@entry_id:153038)。[@problem_id:1648848]

### 统一结构：[基本2-形式](@entry_id:183276)

在厄米[流形](@entry_id:153038)上，度量 $g$ 和[复结构](@entry_id:269128) $J$ 并非孤立存在，它们通过一个称为**[基本2-形式](@entry_id:183276)** (fundamental 2-form) 或**凯勒形式** (Kähler form) 的对象 $\omega$ 紧密地联系在一起。这个2-形式是[凯勒几何](@entry_id:160314)的核心。

#### 定义与相互关系

[基本2-形式](@entry_id:183276) $\omega$ 定义为：
$$ \omega(X, Y) = g(JX, Y) $$
对于任意[切向量](@entry_id:265494) $X, Y$。首先，我们需要验证 $\omega$ 确实是一个[微分2-形式](@entry_id:186910)，这意味着它是双线性的且反对称的。双线性直接继承自 $g$ 和 $J$ 的线性性。反对称性则是一个精妙的推论：
$$ \omega(Y, X) = g(JY, X) $$
利用度量的对称性和兼容性 $g(U, V) = g(JU, JV)$，我们可以写出：
$$ g(JY, X) = g(J(JY), JX) = g(-Y, JX) = -g(Y, JX) = -g(JX, Y) = -\omega(X, Y) $$
因此，$\omega(Y, X) = -\omega(X, Y)$，$\omega$ 是一个反对称的[2-形式](@entry_id:188008)。[@problem_id:1648866]

这三个结构 $(g, J, \omega)$ 构成了一个几何“三位一体”，其中任意两者都可以确定第三者。我们已经看到了如何从 $g$ 和 $J$ 定义 $\omega$。反过来，如果我们已知 $\omega$ 和 $J$，也可以恢复度量 $g$。利用 $J^2 = -\mathrm{Id}$，关系式可以改写为：
$$ g(X, Y) = \omega(X, JY) $$
为了看到这一点，我们只需将定义代入：$\omega(X, JY) = g(JX, JY)$。根据[兼容性条件](@entry_id:201103)，这正好等于 $g(X, Y)$。

这个关系在实际计算中非常强大。例如，考虑[庞加莱上半平面](@entry_id:264005) $M = \{(x, y) \in \mathbb{R}^2 \mid y > 0\}$，它拥有一个非欧几里得的几何结构。设其复结构为标准结构 $J(\partial_x) = \partial_y, J(\partial_y) = -\partial_x$，并给定一个2-形式 $\omega = \frac{1}{y^2} dx \wedge dy$。我们可以用上述关系来确定对应的黎曼度量 $g$ 的分量。
- $g_{xx} = g(\partial_x, \partial_x) = \omega(\partial_x, J\partial_x) = \omega(\partial_x, \partial_y) = \frac{1}{y^2}(dx \wedge dy)(\partial_x, \partial_y) = \frac{1}{y^2}$
- $g_{yy} = g(\partial_y, \partial_y) = \omega(\partial_y, J\partial_y) = \omega(\partial_y, -\partial_x) = -\omega(\partial_y, \partial_x) = \omega(\partial_x, \partial_y) = \frac{1}{y^2}$
- $g_{xy} = g(\partial_x, \partial_y) = \omega(\partial_x, J\partial_y) = \omega(\partial_x, -\partial_x) = 0$
因此，度量张量为 $g = \frac{1}{y^2}(dx \otimes dx + dy \otimes dy)$，这正是庞加莱度量的表达式。[@problem_id:1648843]

#### 基本性质

$\omega$ 最重要的性质之一是它与复结构 $J$ 的关系，即它是 **$J$-不变的** ($J$-invariant)。这意味着：
$$ \omega(JX, JY) = \omega(X, Y) $$
这个性质的证明非常直接，再次利用了定义和[兼容性条件](@entry_id:201103)：
$$ \omega(JX, JY) = g(J(JX), JY) = g(J^2X, JY) = g(-X, JY) $$
利用我们之[前推](@entry_id:158718)导的恒等式 $g(X, JY) = -g(JX, Y)$，上式变为：
$$ -g(X, JY) = -(-g(JX, Y)) = g(JX, Y) = \omega(X, Y) $$
这个性质表明 $\omega$ 是一个 **(1,1)-形式**，意味着它在全纯和反全纯分解中没有 $dz \wedge dw$ 或 $d\bar{z} \wedge d\bar{w}$ 类型的分量。[@problem_id:1648866]

### [凯勒条件](@entry_id:637291)：从厄米到凯勒

厄米[流形](@entry_id:153038)为[复几何](@entry_id:159080)和黎曼几何的结合提供了一个框架，但其结构还相对灵活。通过施加一个额外的[微分](@entry_id:158718)条件，我们便得到了凯勒流形，其几何性质变得异常丰富和刚性。

#### 闭合条件

一个厄米[流形](@entry_id:153038) $(M, g, J)$ 若其[基本2-形式](@entry_id:183276) $\omega$ 是**闭合的** (closed)，即其[外微分](@entry_id:161900) $d\omega = 0$，则称该[流形](@entry_id:153038)为**凯勒流形** (Kähler manifold)。度量 $g$ 此时被称为**凯勒度量** (Kähler metric)。

$d\omega=0$ 这个看似简单的方程，实际上是对度量 $g$ 的分量施加了一组复杂的[偏微分方程](@entry_id:141332)约束。它将[流形](@entry_id:153038)的局部几何与整体拓扑紧密联系起来，并引出了[代数几何](@entry_id:156300)、[微分几何](@entry_id:145818)和数学物理中许多深刻的结果。

#### 规范例子

研究[凯勒流形](@entry_id:161192)最好的起点是其最基本的例子：复[欧氏空间](@entry_id:138052) $\mathbb{C}^n$。如前所述，它配备了标准欧氏度量 $g$ 和标准复结构 $J$。我们来计算其[基本2-形式](@entry_id:183276) $\omega$。利用 $\omega(X,Y) = g(JX,Y)$ 和基[向量的正交性](@entry_id:274719)，我们可以得到：
$$ \omega(\frac{\partial}{\partial x^j}, \frac{\partial}{\partial y^k}) = g(J\frac{\partial}{\partial x^j}, \frac{\partial}{\partial y^k}) = g(\frac{\partial}{\partial y^j}, \frac{\partial}{\partial y^k}) = \delta_{jk} $$
$$ \omega(\frac{\partial}{\partial x^j}, \frac{\partial}{\partial x^k}) = 0, \quad \omega(\frac{\partial}{\partial y^j}, \frac{\partial}{\partial y^k}) = 0 $$
因此，$\omega$ 在[坐标基](@entry_id:270149)底下的表达式为：
$$ \omega = \sum_{j=1}^n dx^j \wedge dy^j $$
这是一个系数为常数的2-形式。对其求[外微分](@entry_id:161900)，由于 $d(dx^j)=0$ 和 $d(dy^j)=0$，我们立即得到：
$$ d\omega = d\left(\sum_{j=1}^n dx^j \wedge dy^j\right) = \sum_{j=1}^n (d(dx^j) \wedge dy^j - dx^j \wedge d(dy^j)) = 0 $$
这证明了 $\omega$ 是闭合的，因此，具有标准欧氏度量的 $\mathbb{C}^n$ 是一个[凯勒流形](@entry_id:161192)。它是最简单（平坦）的凯勒流形。[@problem_id:1648842]

一个有趣且重要的事实是，在任何一维[复流形](@entry_id:159076)（即黎曼面）上，任何[厄米度量](@entry_id:202337)都自动成为凯勒度量。这是因为[流形](@entry_id:153038)的实维数是2，而 $d\omega$ 是一个3-形式。在[二维流形](@entry_id:188198)上，任何3-形式都必然为零。因此，[凯勒条件](@entry_id:637291) $d\omega=0$ 在这种情况下是自动满足的。[@problem_id:1648822]

### [凯勒势](@entry_id:154750)：一个简化的原理

[凯勒条件](@entry_id:637291) $d\omega=0$ 的一个强大推论是**[凯勒势](@entry_id:154750)** (Kähler potential) 的存在性。根据[庞加莱引理](@entry_id:160150)，一个[闭形式](@entry_id:272960)在局部总是恰当的，即 $d\omega=0$ 意味着在任何一[点的邻域](@entry_id:144055)内，存在一个1-形式 $\alpha$ 使得 $\omega = d\alpha$。在[凯勒几何](@entry_id:160314)的框架下，这个结果可以被进一步加强。

#### 凯勒形式的局部生成

在复流形上，可以证明，如果 $\omega$ 是一个闭合的实 $(1,1)$-形式，那么在局部总存在一个实值光滑函数 $K$，称为**[凯勒势](@entry_id:154750)**，使得：
$$ \omega = \frac{i}{2} \partial \bar{\partial} K $$
这里的 $\partial$ 和 $\bar{\partial}$ 是Dolbeault算子。在局部复坐标 $(z^1, \dots, z^n)$ 下，这个表达式等价于：
$$ \omega = \frac{i}{2} \sum_{j,k=1}^n \frac{\partial^2 K}{\partial z^j \partial \bar{z}^k} dz^j \wedge d\bar{z}^k $$
这个公式的意义在于，一个看似复杂的凯勒度量的所有信息，在局部上都编码在一个单一的实值函数 $K$ 之中。这为构造和研究凯勒度量提供了极其有效的工具。

#### 从[凯勒势](@entry_id:154750)到度量

结合 $\omega$ 的定义，我们可以直接从[凯勒势](@entry_id:154750) $K$ 得到凯勒度量 $g$ 的分量。在复坐标下，度量张量的非零分量是 $g_{j\bar{k}}$ 和 $g_{\bar{k}j}$。它们与[凯勒势](@entry_id:154750)的关系是：
$$ g_{j\bar{k}} = \frac{\partial^2 K}{\partial z^j \partial \bar{z}^k} $$
在进行这个计算时，我们使用Wirtinger calculus，将 $z^j$ 和其[复共轭](@entry_id:174690) $\bar{z}^k$ 视为独立的变量。

让我们看几个例子。对于复平面 $\mathbb{C}$，考虑一个简单的[凯勒势](@entry_id:154750) $K(z, \bar{z}) = \frac{5}{2}|z|^2 = \frac{5}{2}z\bar{z}$。度量分量 $g_{z\bar{z}}$ 的计算如下：
$$ \frac{\partial K}{\partial \bar{z}} = \frac{\partial}{\partial \bar{z}} \left( \frac{5}{2}z\bar{z} \right) = \frac{5}{2}z $$
$$ g_{z\bar{z}} = \frac{\partial^2 K}{\partial z \partial \bar{z}} = \frac{\partial}{\partial z} \left( \frac{5}{2}z \right) = \frac{5}{2} $$
这给出了一个常数度量，对应于一个平坦的[凯勒几何](@entry_id:160314)。[@problem_id:1648847]

如果我们选择一个更复杂的势，例如 $K(z, \bar{z}) = \alpha|z|^2 + \beta|z|^4 = \alpha z\bar{z} + \beta(z\bar{z})^2$，其中 $\alpha, \beta$ 是正常数，我们会得到一个非平坦的度量：
$$ \frac{\partial K}{\partial \bar{z}} = \alpha z + 2\beta z^2\bar{z} $$
$$ g_{z\bar{z}} = \frac{\partial^2 K}{\partial z \partial \bar{z}} = \frac{\partial}{\partial z} \left( \alpha z + 2\beta z^2\bar{z} \right) = \alpha + 4\beta z\bar{z} = \alpha + 4\beta |z|^2 $$
这个度量不再是常数，它依赖于点在复平面上的位置，因此描述了一个弯曲的几何空间。[@problem_id:1648879]

### 更深层的几何刻画与推论

[凯勒条件](@entry_id:637291) $d\omega=0$ 远不止是定义上的一个约束，它深刻地影响着[流形](@entry_id:153038)的几何结构，并与其他几何领域（如[辛几何](@entry_id:160783)和和乐群理论）建立了桥梁。

#### [凯勒几何](@entry_id:160314)作为[辛几何](@entry_id:160783)

一个**[辛流形](@entry_id:161608)** (symplectic manifold) 是一个配备了闭合 ($d\omega=0$) 且非退化 (non-degenerate) 的2-形式 $\omega$ 的[流形](@entry_id:153038)。在凯勒流形中，[基本2-形式](@entry_id:183276) $\omega$ 正好满足这两个条件。闭合性是凯勒的定义。非退化性则源于度量 $g$ 的[正定性](@entry_id:149643)：如果对于某个非[零向量](@entry_id:156189) $X$，有 $\omega(X, Y) = 0$ 对所有 $Y$ 成立，那么 $g(JX, Y) = 0$ 对所有 $Y$ 成立。由于 $g$ 非退化，这要求 $JX=0$，但 $J$ 是可逆的，所以 $X=0$，产生矛盾。因此，$\omega$ 是非退化的。

这意味着**任何凯勒流形都是一个[辛流形](@entry_id:161608)**。这一事实使得[辛几何](@entry_id:160783)中强大的工具，如[哈密顿力学](@entry_id:146202)和[哈密顿向量场](@entry_id:270696)，可以直接应用于[凯勒几何](@entry_id:160314)。给定一个函数（[哈密顿量](@entry_id:172864)）$H: M \to \mathbb{R}$，其关联的**[哈密顿向量场](@entry_id:270696)** $X_H$ 由关系式 $i_{X_H}\omega = -dH$ 唯一确定。在凯勒流形上，这个关系可以被翻译成一个连接三种几何结构的美妙公式。对于任意向量场 $Y$：
$$ \omega(X_H, Y) = g(JX_H, Y) \quad \text{和} \quad -dH(Y) = -g(\nabla H, Y) $$
其中 $\nabla H$ 是 $H$ 关于黎曼度量 $g$ 的梯度。由于这对所有 $Y$ 都成立，我们得到：
$$ JX_H = -\nabla H \quad \implies \quad X_H = J\nabla H $$
这个公式优美地展示了凯勒流形上辛结构（$X_H$）、[复结构](@entry_id:269128)（$J$）和黎曼结构（$\nabla H$）的完美融合。例如，在 $\mathbb{R}^4$ 上考虑[哈密顿量](@entry_id:172864) $H = x_1 y_2 - x_2 y_1$，其梯度为 $\nabla H = y_2 \partial_{x_1} - x_2 \partial_{y_1} - y_1 \partial_{x_2} + x_1 \partial_{y_2}$。对应的[哈密顿向量场](@entry_id:270696)就是 $X_H = J\nabla H = x_2 \partial_{x_1} + y_2 \partial_{y_1} - x_1 \partial_{x_2} - y_1 \partial_{y_2}$。其长度平方 $|X_H|^2 = g(X_H, X_H) = x_1^2 + y_1^2 + x_2^2 + y_2^2$。[@problem_id:1648888]

#### 列维-奇维塔联络与和乐群

[黎曼几何](@entry_id:160508)的核心工具是**列维-奇维塔联络** (Levi-Civita connection) $\nabla$，它定义了向量场的协变导数和平行输运。在[凯勒流形](@entry_id:161192)上，这个联络具有一个至关重要的性质：它与复结构 $J$ 相容，即 $\nabla J = 0$。这意味着[复结构](@entry_id:269128) $J$ 在平行输运下是不变的。这个性质是[凯勒条件](@entry_id:637291)的另一个等价表述。也就是说，一个厄米[流形](@entry_id:153038)是凯勒流形，当且仅当其[列维-奇维塔联络](@entry_id:161107)保持复结构不变。

值得注意的是，$\nabla J = 0$ 并不意味着[联络系数](@entry_id:157618)（克氏符号 $\Gamma^k_{ij}$）在任何[坐标系](@entry_id:156346)下都为零。例如，即使是在平坦的 $\mathbb{C} \cong \mathbb{R}^2$ 上，如果我们使用极坐标 $(r, \theta)$，其度量为 $ds^2 = dr^2 + r^2 d\theta^2$，克氏符号如 $\Gamma^r_{\theta\theta} = -r$ 和 $\Gamma^\theta_{r\theta} = \frac{1}{r}$ 都是非零的。这说明了[联络系数](@entry_id:157618)是坐标依赖的，而 $\nabla J=0$ 是一个内在的、不依赖于坐标的几何事实。[@problem_id:1648878]

$\nabla J = 0$ 这个条件[对流](@entry_id:141806)形的**[和乐群](@entry_id:191471)** (holonomy group) $\mathrm{Hol}(g)$ 有着深刻的影响。和乐群是在某点由沿所有闭环路进行[平行输运](@entry_id:160671)所产生的变换构成的群。对于一个一般的 $2n$ 维黎曼流形，[和乐群](@entry_id:191471)是[正交群](@entry_id:152531) $O(2n)$ 的一个[子群](@entry_id:146164)。而对于凯勒流形，由于[平行输运](@entry_id:160671)必须保持复结构 $J$ 不变，和乐群的元素必须与 $J$ 交换。这将其限制在一个更小的群——[酉群](@entry_id:138602) $U(n)$ 中。

事实上，这是一个等价的刻画：一个 $2n$ 维可定向、单连通的黎曼流形 $(M,g)$ 是凯勒流形，当且仅当其约化[和乐群](@entry_id:191471) $\mathrm{Hol}^0(g)$ 是[酉群](@entry_id:138602) $U(n)$ 的一个[子群](@entry_id:146164)。

这个标准为我们提供了一个判断黎曼流形是否可能成为凯勒流形的有力工具。例如，一个四维（$n=2$）单连通黎曼流形，如果其和乐群被确定为 $SO(4)$，那么它不可能是[凯勒流形](@entry_id:161192)，因为 $SO(4)$ 并不包含于 $U(2)$。然而，如果另一个[四维流形](@entry_id:274951)的[和乐群](@entry_id:191471)是 $SU(2)$，由于 $SU(2) \subset U(2)$，这个[流形](@entry_id:153038)则是一个[凯勒流形](@entry_id:161192)（实际上，它甚至是一个更特殊的[超凯勒流形](@entry_id:159760)或Calabi-Yau流形）。[@problem_id:1648865]

综上所述，凯勒流形通过 $d\omega=0$ 这一核心条件，将[复结构](@entry_id:269128)、[黎曼度量](@entry_id:754359)和辛结构完美地融合在一起。这种融合不仅产生了丰富的局部几何，如[凯勒势](@entry_id:154750)的存在，也导致了深刻的全局性质，如和乐群的约化，使其成为现代几何和物理学中一个极其重要的研究对象。