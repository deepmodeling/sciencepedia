## 引言
[戴德金η函数](@entry_id:200103)（Dedekind eta function）是十九世纪数学的瑰宝，至今仍在数论与理论物理的前沿扮演着核心角色。它以一个简洁的[无穷乘积](@entry_id:176333)形式定义，但其背后却隐藏着深刻的对称性结构。初看之下，η函数的定义与它在[模变换](@entry_id:184910)下的复杂行为之间的联系并不明显，这构成了理解其威力的主要挑战。为何一个简单的乘积会在[坐标变换](@entry_id:172727)下产生与数论对象“[戴德金和](@entry_id:187230)”相关的精确相位？它又是如何成为连接看似无关的数学和物理领域的桥梁？

本文旨在系统地揭开[戴德金η函数](@entry_id:200103)的神秘面纱。在“原理与机制”部分，我们将从其定义出发，详细推导其在模[群作用](@entry_id:268812)下的变换法则，并揭示其与[戴德金和](@entry_id:187230)的精密关系。接下来的“应用与跨学科联系”部分将展示这些抽象原理如何转化为解决数论、[代数几何](@entry_id:156300)和共形场论中具体问题的强大工具。最后，通过“动手实践”部分提供的一系列计算问题，读者将有机会亲手应用所学知识，巩固对这一非凡函数的理解。

## 原理与机制

本章在前一章介绍性背景的基础上，深入探讨[戴德金η函数](@entry_id:200103)的核心数学原理及其在[模变换](@entry_id:184910)下的行为机制。我们将从其定义和级数展开开始，系统地推导其在[模群](@entry_id:184647)基本生成元作用下的变换法则，并最终揭示其与数论中深刻的[戴德金和](@entry_id:187230)之间的联系。

### [戴德金η函数](@entry_id:200103)的定义与[q-展开](@entry_id:186629)

[戴德金η函数](@entry_id:200103)是一个在上半复平面 $\mathbb{H} = \{\tau \in \mathbb{C} \mid \text{Im}(\tau) > 0\}$ 上定义的标准全纯函数。它通常通过其无穷乘积展开式来定义。

对于任意 $\tau \in \mathbb{H}$，我们定义一个变量 $q = \exp(2\pi i \tau)$。由于 $\text{Im}(\tau) > 0$，我们有 $|q|  1$。这个 $q$ 坐标将上半平面映射到单位圆盘内部的去心邻域。以 $q$ 为变量，**[戴德金η函数](@entry_id:200103)** ($\eta$-function) 定义为：
$$ \eta(\tau) = q^{1/24} \prod_{n=1}^{\infty} (1 - q^n) $$
其中 $q^{1/24}$ 这个看似奇特的因子，即 $\exp(\pi i \tau / 12)$，对于确保η函数优美的模性质至关重要，我们将在后续章节中看到这一点。

乘积部分 $\prod_{n=1}^{\infty} (1 - q^n)$ 本身就是一个非常重要的函数，通常被称为**[欧拉函数](@entry_id:634684)**，记作 $\phi(q)$。[欧拉函数](@entry_id:634684)有一个极为优美的[级数展开](@entry_id:142878)式，即**[欧拉五边形数定理](@entry_id:194412)**：
$$ \phi(q) = \prod_{n=1}^{\infty} (1 - q^n) = \sum_{k=-\infty}^{\infty} (-1)^k q^{k(3k-1)/2} $$
指数 $n_k = k(3k-1)/2$ 对于整数 $k$（包括正、负和零）被称为**[广义五边形数](@entry_id:637902)**。例如，对于 $k = 0, \pm 1, \pm 2, \dots$，我们得到序列 $0, 1, 2, 5, 7, 12, 15, \dots$。这一定理揭示了[整数分拆理论](@entry_id:636964)与[模形式](@entry_id:160014)之间深刻的内在联系。

这个[级数展开](@entry_id:142878)式为计算涉及η函数的表达式的 $q$-展开系数提供了一个强大的工具。例如，考虑函数 $F(\tau) = \eta(\tau)^3$，它是一个权为 $3/2$ 的模形式。我们可以通过将[欧拉函数](@entry_id:634684)的[级数展开](@entry_id:142878)自乘来求得其 $q$-展开的系数 [@problem_id:650896]。
$F(\tau) = (q^{1/24}\phi(q))^3 = q^{1/8} \phi(q)^3$。
要计算 $F(\tau)$ 中 $q^{N+1/8}$ 的系数 $a_N$，我们只需计算 $\phi(q)^3$ 中 $q^N$ 的系数。
根据[五边形数定理](@entry_id:635002)，$\phi(q)$ 的前几项是：
$$ \phi(q) = 1 - q - q^2 + q^5 + q^7 - q^{12} - q^{15} + \dots $$
为了计算 $\phi(q)^3$ 中 $q^{10}$ 的系数，我们需求解方程 $i+j+k=10$，其中 $i,j,k$ 是[广义五边形数](@entry_id:637902)，并考虑其系数 $(-1)^{k_i}(-1)^{k_j}(-1)^{k_k}$。
通过直接展开 $(1-q-q^2+q^5+q^7+\dots)^3$，我们寻找 $q^{10}$ 的项。这些项可以由以下组合得到：
1.  来自 $(q^5)(q^5)(1)$ 的组合。由于 $q^5$ 的系数为 $+1$，这一组（包括 $1 \cdot q^5 \cdot q^5$, $q^5 \cdot 1 \cdot q^5$, $q^5 \cdot q^5 \cdot 1$ 三种[排列](@entry_id:136432)）贡献了 $3 \times (1)^2 \times 1 = 3$。
2.  来自 $(q^7)(q^2)(q^1)$ 的组合。$q^7$ 的系数为 $+1$，而 $q^2$ 和 $q$ 的系数均为 $-1$。这三个不同项的[排列](@entry_id:136432)共有 $3! = 6$ 种。每种[排列](@entry_id:136432)的系数贡献为 $(1)(-1)(-1) = 1$。因此总贡献为 $6 \times 1 = 6$。

将这些贡献相加，我们得到 $q^{10}$ 的系数为 $3+6=9$。因此，在 $F(\tau) = \eta(\tau)^3 = q^{1/8} \sum a_n q^n$ 的展开式中，$a_{10}=9$ [@problem_id:650896]。

### [模变换](@entry_id:184910)：生成元S与T

$\eta$[函数的根](@entry_id:169486)本重要性在于其在**[模群](@entry_id:184647)** $SL(2, \mathbb{Z})$ 作用下的变换行为。$SL(2, \mathbb{Z})$ 是所有[行列式](@entry_id:142978)为1的二阶整数矩阵构成的群：
$$ SL(2, \mathbb{Z}) = \left\{ \gamma = \begin{pmatrix} a  b \\ c  d \end{pmatrix} \mid a,b,c,d \in \mathbb{Z}, ad-bc=1 \right\} $$
该群通过**[分式线性变换](@entry_id:174812)** (或称**莫比乌斯变换**) 作用于[上半平面](@entry_id:199119) $\mathbb{H}$：
$$ \tau \mapsto \gamma\tau = \frac{a\tau+b}{c\tau+d} $$
整个[模群](@entry_id:184647)可以由两个基本变换生成：
1.  **平移 (Translation)** $T = \begin{pmatrix} 1  1 \\ 0  1 \end{pmatrix}$，其作用为 $\tau \mapsto \tau+1$。
2.  **反演 (Inversion)** $S = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}$，其作用为 $\tau \mapsto -1/\tau$。

#### T-变换

在 $T$ 变换下，$\eta$函数的行为相对简单。由于 $q = \exp(2\pi i \tau)$，当 $\tau \mapsto \tau+1$ 时，$q \mapsto \exp(2\pi i (\tau+1)) = \exp(2\pi i)\exp(2\pi i \tau) = q$。乘积部分 $\prod(1-q^n)$ 保持不变。然而，$q^{1/24}$ 因子发生了变化：
$$ \exp\left(\frac{2\pi i (\tau+1)}{24}\right) = \exp\left(\frac{2\pi i \tau}{24}\right) \exp\left(\frac{2\pi i}{24}\right) = q^{1/24} e^{\pi i/12} $$
因此，我们得到了第一个基本变换法则：
$$ \eta(\tau+1) = e^{\pi i/12} \eta(\tau) $$
这个 $e^{\pi i/12}$ 的相位因子是一个24次[单位根](@entry_id:143302)，它的出现正是我们选择 $q^{1/24}$ 这个初始因子的原因。

#### S-变换

在 $S$ 变换下的行为则深刻得多。其变换法则为：
$$ \eta(-1/\tau) = \sqrt{-i\tau} \, \eta(\tau) $$
这里的 $\sqrt{-i\tau}$ 因子表明 $\eta$ 函数并非一个严格的模形式，而是所谓的**半整权[模形式](@entry_id:160014)**。对于 $\tau \in \mathbb{H}$，我们约定 $\sqrt{z}$ 取[主分支](@entry_id:164844)，即辐角在 $(-\pi/2, \pi/2]$ 之间。因此 $\sqrt{-i\tau}$ 的辐角是明确的。

这个恒等式的证明并非显而易见。一个经典的证明方法是利用 $\eta$ 函数与**[雅可比θ函数](@entry_id:192522)** (Jacobi theta functions) 之间的关系 [@problem_id:650904]。关键是**雅可比[三重积](@entry_id:162942)恒等式**的一个推论，它将 $\eta(\tau)^3$ 与三个基本的[θ函数](@entry_id:202912)联系起来：
$$ \vartheta_2(\tau) \vartheta_3(\tau) \vartheta_4(\tau) = 2\eta(\tau)^3 $$
（注意：文献中 $\eta^3$ 与theta函数的关系常数有不同版本，这取决于 $\eta$ 和 $\vartheta$ 的具体定义）。
[雅可比θ函数](@entry_id:192522)在 $S$ 变换下有已知的变换法则：
$$ \vartheta_2(-1/\tau) = \sqrt{-i\tau} \, \vartheta_4(\tau) $$
$$ \vartheta_3(-1/\tau) = \sqrt{-i\tau} \, \vartheta_3(\tau) $$
$$ \vartheta_4(-1/\tau) = \sqrt{-i\tau} \, \vartheta_2(\tau) $$
现在，我们在雅可比恒等式中用 $-1/\tau$ 替换 $\tau$：
$$ 2\eta(-1/\tau)^3 = \vartheta_2(-1/\tau) \vartheta_3(-1/\tau) \vartheta_4(-1/\tau) $$
将[θ函数](@entry_id:202912)的变换法则代入右侧：
$$ 2\eta(-1/\tau)^3 = (\sqrt{-i\tau} \, \vartheta_4(\tau)) (\sqrt{-i\tau} \, \vartheta_3(\tau)) (\sqrt{-i\tau} \, \vartheta_2(\tau)) $$
$$ 2\eta(-1/\tau)^3 = (\sqrt{-i\tau})^3 (\vartheta_2(\tau) \vartheta_3(\tau) \vartheta_4(\tau)) $$
再次使用[雅可比恒等式](@entry_id:140480)替换[θ函数](@entry_id:202912)的乘积：
$$ 2\eta(-1/\tau)^3 = (\sqrt{-i\tau})^3 (2\eta(\tau)^3) $$
消去公因子 $2$ 并开三次方根，我们便严格地导出了 $S$ 变换的法则 [@problem_id:650904]：
$$ \eta(-1/\tau) = \sqrt{-i\tau} \, \eta(\tau) $$

### 乘子系统与上循环条件

对于 $SL(2, \mathbb{Z})$ 中的任意一个元素 $\gamma = \begin{pmatrix} a  b \\ c  d \end{pmatrix}$，$\eta$ 函数的变换法则可以统一写成：
$$ \eta(\gamma\tau) = v_\eta(\gamma, \tau) \eta(\tau) $$
其中 $v_\eta(\gamma, \tau)$ 被称为**乘子系统** (multiplier system)。对于 $\eta$ 函数，这个乘子具有特定的形式：
$$ v_\eta(\gamma, \tau) = \varepsilon(\gamma) \sqrt{c\tau+d} $$
这里 $\varepsilon(\gamma)$ 是一个依赖于矩阵 $\gamma$ 的24次[单位根](@entry_id:143302)，而 $\sqrt{c\tau+d}$ 的分支选取使其值为正实部。这种形式的变换表明 $\eta$ 是一个**权为1/2，带有乘子系统 $\varepsilon$ 的模形式**。

乘子系统必须满足一个重要的自洽性条件，称为**上循环条件** (cocycle condition)。对于任意两个[模群](@entry_id:184647)中的元素 $\gamma_1, \gamma_2$，该条件表述为：
$$ v_\eta(\gamma_1\gamma_2, \tau) = v_\eta(\gamma_1, \gamma_2\tau) v_\eta(\gamma_2, \tau) $$
这个条件本质上是说，连续施行两次变换 $(\gamma_1\gamma_2)$ 的效果，等同于先施行 $\gamma_2$ 变换，再在新的变量 $\gamma_2\tau$ 上施行 $\gamma_1$ 变换。

我们可以通过计算复合变换的乘子来验证这一点。例如，考虑变换 $\gamma = (ST)^2$ [@problem_id:651006]。
$$ \eta((ST)^2 \tau) = \eta(ST(ST\tau)) = v_\eta(ST, ST\tau) \eta(ST\tau) = v_\eta(ST, ST\tau) v_\eta(ST, \tau) \eta(\tau) $$
我们首先计算 $v_\eta(ST, \tau)$。$ST\tau = S(\tau+1) = -1/(\tau+1)$。
$$ \eta(ST\tau) = \eta(S(\tau+1)) = v_\eta(S, \tau+1)\eta(\tau+1) = \sqrt{-i(\tau+1)} \cdot e^{\pi i/12}\eta(\tau) $$
所以 $v_\eta(ST, \tau) = e^{\pi i/12}\sqrt{-i(\tau+1)}$。
现在计算 $v_\eta(ST, ST\tau)$，只需将上式中的 $\tau$ 替换为 $ST\tau = -1/(\tau+1)$：
$$ v_\eta(ST, ST\tau) = e^{\pi i/12}\sqrt{-i(ST\tau+1)} = e^{\pi i/12}\sqrt{-i(-\frac{1}{\tau+1}+1)} = e^{\pi i/12}\sqrt{-i\frac{\tau}{\tau+1}} $$
因此，总的乘子是：
$$ v_\eta((ST)^2, \tau) = \left(e^{\pi i/12}\sqrt{-i\frac{\tau}{\tau+1}}\right) \left(e^{\pi i/12}\sqrt{-i(\tau+1)}\right) = e^{\pi i/6} \sqrt{(-i)^2 \tau} = e^{\pi i/6} \sqrt{-\tau} $$
由于 $\tau \in \mathbb{H}$，$\sqrt{-\tau} = \sqrt{(-1)}\sqrt{\tau} = i\sqrt{\tau}$。因此 $v_\eta((ST)^2, \tau) = i e^{\pi i/6} \sqrt{\tau} = e^{i\pi/2} e^{\pi i/6} \sqrt{\tau} = e^{2\pi i/3}\sqrt{\tau}$。
而矩阵 $(ST)^2 = \begin{pmatrix} -1  -1 \\ 1  0 \end{pmatrix}$，其形式为 $\varepsilon((ST)^2)\sqrt{1\cdot\tau+0}$。比较可知 $\varepsilon((ST)^2) = e^{2\pi i/3}$。
*编者注：所引用的问题[@problem_id:651006]中 $\eta(-1/\tau)$ 的定义为 $e^{-i\pi/4}\sqrt{\tau}\eta(\tau)$，这导致结果为 $e^{-i\pi/3}$。不同的文献对 $\sqrt{-i\tau}$ 的定义选择会导致常数相位的差异，但基本结构不变。*

上循环条件的一个深刻体现是在[模群](@entry_id:184647)的关系 $(ST)^3 = -I$ 上（其中 $I$ 是[单位矩阵](@entry_id:156724)）。由于 $-I$ 作用于 $\tau$ 的结果是 $\tau$ 本身（$\frac{-\tau+0}{0\tau-1} = \tau$），因此 $\eta((ST)^3\tau)$ 应当等于 $\eta(\tau)$ 乘以某个常数。通过逐步应用 $S$ 和 $T$ 的变换法则，可以精确计算出这个常数。
$$ \eta((ST)^3\tau) = v_\eta((ST)^2, ST\tau) v_\eta(ST, \tau) \eta(\tau) $$
经过细致的代数运算和对平方根分支的正确处理，可以证明这个总乘子恰好为 $-1$ [@problem_id:886075]。即 $\eta((ST)^3\tau) = -\eta(\tau)$。另一方面，$\eta$ 在 $-I$ 变换下的行为是 $\eta(\frac{-\tau}{-1}) = \varepsilon(-I)\sqrt{-1}\eta(\tau) = (-i)(i)\eta(\tau) = \eta(\tau)$（这里需要更复杂的乘子公式，但结果是 $\eta$ 在 $-I$ 作用下不变）。这一看似矛盾的结果（$-1$ vs $1$）实际上揭示了模形式理论的一个微妙之处：$\eta$ 函数实际上是 $SL(2, \mathbb{Z})$ 的一个**[射影表示](@entry_id:180787)**的向量，它是在一个更复杂的群——$SL(2, \mathbb{Z})$ 的一个[中心扩张](@entry_id:144634)上的真[实表示](@entry_id:146117)。

### [戴德金和](@entry_id:187230)与乘子公式

前面我们确定了乘子 $v_\eta(\gamma, \tau) = \varepsilon(\gamma)\sqrt{c\tau+d}$ 的一般形式。现在的问题是，如何计算任意 $\gamma$ 的24次单位根 $\varepsilon(\gamma)$？答案将我们引向一个纯粹的数论对象：**[戴德金和](@entry_id:187230)** (Dedekind Sum)。

对于[互质](@entry_id:143119)的整数 $c0$ 和 $d$，[戴德金和](@entry_id:187230) $s(d,c)$ 定义为：
$$ s(d,c) = \sum_{k=1}^{c-1} \left(\!\left(\frac{k}{c}\right)\!\right) \left(\!\left(\frac{dk}{c}\right)\!\right) $$
其中函数 $((x))$ 是**锯齿函数** (sawtooth function)：
$$ ((x)) = \begin{cases} x - \lfloor x \rfloor - 1/2  \text{if } x \notin \mathbb{Z} \\ 0  \text{if } x \in \mathbb{Z} \end{cases} $$
$((x))$ 是一个周期为1的奇函数，它度量了 $x$ 与最近整数的带符号距离。

有了[戴德金和](@entry_id:187230)的定义，乘子 $\varepsilon(\gamma)$ 的精确表达式（对于 $c0$）由下式给出：
$$ \varepsilon(\gamma) = \exp\left(\pi i \left( \frac{a+d}{12c} - s(d,c) \right)\right) $$
这个公式将 $\eta$ 函数的解析变换性质（左侧）与离散的算术和（右侧）联系起来，是数学中跨领域联系的一个绝佳范例。

例如，我们来计算矩阵 $\gamma = \begin{pmatrix} 4  3 \\ 5  4 \end{pmatrix}$ 的乘子 $\varepsilon(\gamma)$ [@problem_id:650900]。这里 $a=4, b=3, c=5, d=4$。
首先，计算[戴德金和](@entry_id:187230) $s(4,5)$：
$s(4,5) = \sum_{k=1}^4 ((\frac{k}{5})) ((\frac{4k}{5}))$
$k=1: ((\frac{1}{5}))((\frac{4}{5})) = (\frac{1}{5}-\frac{1}{2})(\frac{4}{5}-\frac{1}{2}) = (-\frac{3}{10})(\frac{3}{10}) = -\frac{9}{100}$
$k=2: ((\frac{2}{5}))((\frac{8}{5})) = (\frac{2}{5}-\frac{1}{2})(\frac{8}{5}-1-\frac{1}{2}) = (-\frac{1}{10})(\frac{1}{10}) = -\frac{1}{100}$
$k=3: ((\frac{3}{5}))((\frac{12}{5})) = (\frac{3}{5}-\frac{1}{2})(\frac{12}{5}-2-\frac{1}{2}) = (\frac{1}{10})(-\frac{1}{10}) = -\frac{1}{100}$
$k=4: ((\frac{4}{5}))((\frac{16}{5})) = (\frac{4}{5}-\frac{1}{2})(\frac{16}{5}-3-\frac{1}{2}) = (\frac{3}{10})(-\frac{3}{10}) = -\frac{9}{100}$
所以 $s(4,5) = -\frac{9+1+1+9}{100} = -\frac{20}{100} = -\frac{1}{5}$。
现在计算指数部分：$\frac{a+d}{12c} - s(d,c) = \frac{4+4}{12 \cdot 5} - (-\frac{1}{5}) = \frac{8}{60} + \frac{1}{5} = \frac{2}{15} + \frac{3}{15} = \frac{5}{15} = \frac{1}{3}$。
因此，$\varepsilon(\gamma) = \exp(\pi i / 3)$。

[戴德金和](@entry_id:187230)自身满足一个深刻的**[互反律](@entry_id:188215)** (Reciprocity Law)。对于任意两个互质的正整数 $h,k$：
$$ s(h,k) + s(k,h) = \frac{h^2 + k^2 + 1}{12hk} - \frac{1}{4} $$
这个定律使得计算[戴德金和](@entry_id:187230)变得更加容易，并且是证明 $\eta$ 函数模性质的关键工具之一。例如，利用该定律，我们可以不经直接求和就计算出 $s(7,11) + s(11,7)$ [@problem_id:651033]：
$$ s(7,11) + s(11,7) = \frac{7^2 + 11^2 + 1}{12 \cdot 7 \cdot 11} - \frac{1}{4} = \frac{49+121+1}{924} - \frac{1}{4} = \frac{171}{924} - \frac{1}{4} = \frac{57}{308} - \frac{77}{308} = -\frac{20}{308} = -\frac{5}{77} $$

对数 $\log\eta(\tau)$ 的变换法则更直接地揭示了[戴德金和](@entry_id:187230)的角色 [@problem_id:650866]。取对数后，[乘法法则](@entry_id:144424)变为加法法则：
$$ \log \eta(\gamma\tau) = \log\eta(\tau) + \frac{1}{2}\log(c\tau+d) + \pi i \left( \frac{a+d}{12c} - s(d,c) \right) + \text{const.} $$
这个形式清楚地表明，[模变换](@entry_id:184910)引起的相位变化由一个代数项 $\frac{a+d}{12c}$ 和一个算术项 $-s(d,c)$ 共同决定。

### 与其他模对象的联系

$\eta$ 函数是构建更复杂模对象的基石。它的性质深刻地影响着整个模形式理论。

#### [模判别式](@entry_id:191288) $\Delta(\tau)$
**[模判别式](@entry_id:191288)** (Modular Discriminant) 定义为 $\Delta(\tau) = (2\pi)^{12} \eta(\tau)^{24}$。
由于 $\eta$ 函数的乘子 $\varepsilon(\gamma)$ 是24次单位根，当取24次方时，这个复杂的相位因子就变成了1。
$$ \eta(\gamma\tau)^{24} = (\varepsilon(\gamma) \sqrt{c\tau+d} \, \eta(\tau))^{24} = \varepsilon(\gamma)^{24} (c\tau+d)^{12} \eta(\tau)^{24} = (c\tau+d)^{12} \eta(\tau)^{24} $$
因此，$\Delta(\tau)$ 的变换法则为：
$$ \Delta(\gamma\tau) = (c\tau+d)^{12} \Delta(\tau) $$
这表明 $\Delta(\tau)$ 是一个对整个[模群](@entry_id:184647) $SL(2, \mathbb{Z})$ 的权为12的**真[模形式](@entry_id:160014)**。它在 $\mathbb{H}$ 上无零点，并在[尖点](@entry_id:636792) $i\infty$ 处有一个一阶零点。

#### 配价公式
模形式的[零点和极点](@entry_id:177073)的[分布](@entry_id:182848)受到严格的拓扑约束，这由**配价公式** (Valence Formula) 给出。对于 $SL(2, \mathbb{Z})$ 上的一个非零的权为 $k$ 的亚纯模形式 $f$，其公式为：
$$ \text{ord}_{i\infty}(f) + \frac{1}{2}\text{ord}_{i}(f) + \frac{1}{3}\text{ord}_{\rho}(f) + \sum_{p \in \mathcal{F}^*} \text{ord}_p(f) = \frac{k}{12} $$
其中 $\rho = e^{i\pi/3}$，$i$ 是椭圆[不动点](@entry_id:156394)，$\text{ord}_p(f)$ 是 $f$ 在点 $p$ 的零点阶数（极点为负）。
这个公式可以用来推断模形式的性质。例如，考虑函数 $F(\tau) = \frac{E_4(\tau) \Delta(\tau)}{E_6(\tau)}$ [@problem_id:650905]，其中 $E_4, E_6$ 是艾森斯坦级数。
$F$ 的权为 $k = 4 + 12 - 6 = 10$。
已知 $E_4$ 在 $\rho$ 处有单零点， $E_6$ 在 $i$ 处有单零点，$\Delta$ 在 $\mathbb{H}$ 中无零点。因此：
$\text{ord}_{\rho}(F) = 1$
$\text{ord}_{i}(F) = -1$
在标准基本区域 $\mathcal{F}$ 的其他地方， $F$ 没有零点或极点。代入配价公式：
$$ \text{ord}_{i\infty}(F) + \frac{1}{2}(-1) + \frac{1}{3}(1) = \frac{10}{12} $$
$$ \text{ord}_{i\infty}(F) - \frac{1}{6} = \frac{5}{6} \implies \text{ord}_{i\infty}(F) = 1 $$
这表明函数 $F(\tau)$ 在[尖点](@entry_id:636792)有一个一阶零点。这个例子展示了如何利用 $\Delta$（即 $\eta^{24}$）的性质以及[模形式](@entry_id:160014)的一般结构理论来推断复杂函数的行为。

#### 拟模艾森斯坦级数 $E_2(\tau)$
权为2的**艾森斯坦级数** $E_2(\tau)$ 与 $\eta$ 函数有非常直接的联系，它可以通过 $\eta$ 的[对数导数](@entry_id:169238)来定义：
$$ E_2(\tau) = \frac{1}{2\pi i} \frac{d}{d\tau} \log \Delta(\tau) = \frac{24}{2\pi i} \frac{d}{d\tau} \log \eta(\tau) = \frac{12}{\pi i} \frac{d}{d\tau} \log \eta(\tau) $$
这个定义立即意味着 $E_2$ 的变换性质继承自 $\eta$ 函数。$E_2$ 并不是一个真正的[模形式](@entry_id:160014)，它的变换法则带有一个“反常”项。我们可以通过对 $\log\eta(\gamma\tau)$ 的变换法则进行[微分](@entry_id:158718)来导出这个反常项 [@problem_id:886095]。
从 $\log\eta(\gamma\tau) = \log\eta(\tau) + \frac{1}{2}\log(c\tau+d) + C(\gamma)$ 开始，对 $\tau$ [微分](@entry_id:158718)：
$$ \frac{d}{d\tau} \log\eta(\gamma\tau) = \frac{d(\gamma\tau)}{d\tau} \cdot \frac{d}{d(\gamma\tau)}\log\eta(\gamma\tau) = \frac{1}{(c\tau+d)^2} \frac{d}{d(\gamma\tau)}\log\eta(\gamma\tau) $$
而右边[微分](@entry_id:158718)得到：
$$ \frac{d}{d\tau}\log\eta(\tau) + \frac{c}{2(c\tau+d)} $$
结合两边并乘以 $\frac{12}{\pi i}(c\tau+d)^2$，我们得到：
$$ \frac{12}{\pi i} \frac{d}{d(\gamma\tau)}\log\eta(\gamma\tau) = (c\tau+d)^2 \left( \frac{12}{\pi i} \frac{d}{d\tau}\log\eta(\tau) \right) + (c\tau+d)^2 \frac{12}{\pi i}\frac{c}{2(c\tau+d)} $$
$$ E_2(\gamma\tau) = (c\tau+d)^2 E_2(\tau) + \frac{6c(c\tau+d)}{\pi i} $$
这个多出来的项 $\frac{6c(c\tau+d)}{\pi i}$ 就是 $E_2$ 的模反常项，它使 $E_2$ 成为一个**拟[模形式](@entry_id:160014)** (quasi-modular form) 而非真[模形式](@entry_id:160014)。这个反常项的根源正是 $\eta$ [函数变换](@entry_id:141095)中的 $\sqrt{c\tau+d}$ 因子。

#### 韦伯[模函数](@entry_id:155728)
最后，除了作为幂和导数的构建块，$\eta$ 函数本身也可以通过比值的形式来构造新的[模函数](@entry_id:155728)。一个重要的例子是**韦伯[模函数](@entry_id:155728)** (Weber modular functions) [@problem_id:651037]。例如：
$$ \mathfrak{f}(\tau) = e^{-\pi i/24} \frac{\eta\left(\frac{\tau+1}{2}\right)}{\eta(\tau)}, \quad \mathfrak{f}_1(\tau) = \frac{\eta\left(\frac{\tau}{2}\right)}{\eta(\tau)} $$
这些函数的模性质可以直接从 $\eta$ 函数的变换法则推导出来。例如，我们可以验证 $\mathfrak{f}(\tau+1)$ 与 $\mathfrak{f}_1(\tau)$ 之间的关系：
$$ \mathfrak{f}(\tau+1) = e^{-\pi i/24} \frac{\eta\left(\frac{(\tau+1)+1}{2}\right)}{\eta(\tau+1)} = e^{-\pi i/24} \frac{\eta\left(\frac{\tau}{2}+1\right)}{\eta(\tau+1)} $$
利用 $\eta(z+1) = e^{\pi i/12}\eta(z)$，我们得到：
$$ \mathfrak{f}(\tau+1) = e^{-\pi i/24} \frac{e^{\pi i/12}\eta(\frac{\tau}{2})}{e^{\pi i/12}\eta(\tau)} = e^{-\pi i/24} \frac{\eta(\frac{\tau}{2})}{\eta(\tau)} = e^{-\pi i/24} \mathfrak{f}_1(\tau) $$
这个简单的计算表明，这些由 $\eta$ 构造的更复杂的对象，其行为完全由 $\eta$ 的基本原理所支配，进一步凸显了[戴德金η函数](@entry_id:200103)在整个理论中的核心地位。