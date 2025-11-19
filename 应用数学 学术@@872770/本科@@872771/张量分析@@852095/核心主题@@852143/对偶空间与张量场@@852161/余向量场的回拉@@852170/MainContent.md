## 引言
在探索[流形](@entry_id:153038)上的几何与物理世界时，一个核心问题是：当一个空间通过映射与另一个空间联系起来时，定义其上的物理量（如[力场](@entry_id:147325)或[电磁场](@entry_id:265881)）或几何结构会如何变换？与将切向量从源空间“推向”目标空间的推前运算不同，[协变矢量](@entry_id:263917)场（或称[1-形式](@entry_id:270392)）表现出一种自然的“逆向”变换行为，即从目标空间“[拉回](@entry_id:160816)”到源空间。这一被称为**[拉回](@entry_id:160816)（Pullback）**的运算，是微分几何中连接不同空间或不同[坐标系](@entry_id:156346)下物理量的基石，其重要性贯穿了从经典力学到广义相对论的诸多领域。

本文旨在系统地阐述[协变矢量](@entry_id:263917)场[拉回](@entry_id:160816)的完整图景。我们将从其根本定义出发，逐步深入，为读者构建一个清晰、坚实的理解框架。
- 在**“原理与机制”**一章中，我们将详细介绍[拉回](@entry_id:160816)的抽象定义与坐标计算方法，并通过具体例子阐明其代数性质，特别是其与外微分算子的深刻关系。
- 接着，在**“应用与跨学科联系”**一章中，我们将展示[拉回](@entry_id:160816)如何作为核心工具，在坐标变换、[场论](@entry_id:155241)限制、哈密顿力学和相对论等多个领域中发挥关键作用，揭示其在解决实际问题中的强大威力。
- 最后，**“动手实践”**部分提供了一系列精心设计的问题，帮助读者将理论知识转化为解决问题的实践能力。

通过这一结构化的学习路径，读者将不仅掌握[拉回](@entry_id:160816)的计算技巧，更能深刻理解其作为一种基本语言，在现代数学和物理学中所扮演的不可或缺的角色。

## 原理与机制

在研究一个空间（或[流形](@entry_id:153038)）上的物理量或几何结构时，我们常常需要理解当这个空间被映射到另一个空间时，这些量会如何变化。例如，一个在三维空间中定义的[力场](@entry_id:147325)，在一个嵌入于此空间内的二维[曲面](@entry_id:267450)上会呈现出怎样的形态？为了回答这类问题，微分几何学发展出了一套强大的工具，其中**[拉回](@entry_id:160816) (pullback)** 运算是核心概念之一。

与将切向量从源[流形](@entry_id:153038)“推向”目标[流形](@entry_id:153038)的**推前 (pushforward)** 映射相反，[协变矢量](@entry_id:263917)场（也称余切矢量场或1-形式）具有一种自然的“逆向”变换行为。给定一个[光滑映射](@entry_id:203730) $\phi: M \to N$，它将[流形](@entry_id:153038) $M$ 上的点映射到[流形](@entry_id:153038) $N$ 上，[拉回运算](@entry_id:753859) $\phi^*$ 则将 $N$ 上的[协变矢量](@entry_id:263917)场“[拉回](@entry_id:160816)”到 $M$ 上，成为 $M$ 上的一个[协变矢量](@entry_id:263917)场。这种看似“逆行”的特性，源于[协变矢量](@entry_id:263917)作为线性函数的内在属性。

本章将系统地阐述[协变矢量](@entry_id:263917)场[拉回](@entry_id:160816)的定义、基本性质及其与微积分中其它核心运算（如[外微分](@entry_id:161900)）的深刻联系。

### [拉回](@entry_id:160816)的定义：概念与计算

从概念上讲，[拉回](@entry_id:160816)的定义建立在[协变矢量](@entry_id:263917)与[切向量](@entry_id:265494)的配对（即[协变矢量](@entry_id:263917)作用于切向量）之上。设 $\phi: M \to N$ 是一个[光滑映射](@entry_id:203730)，$p \in M$ 是源[流形](@entry_id:153038)上的一个点，其在目标[流形](@entry_id:153038)上的像为 $\phi(p) \in N$。令 $\omega$ 是 $N$ 上的一个[协变矢量](@entry_id:263917)场，那么在点 $\phi(p)$ 处，它是一个线性函数 $\omega_{\phi(p)}: T_{\phi(p)}N \to \mathbb{R}$，作用于该点的切向量。

[拉回](@entry_id:160816) $\phi^*\omega$ 是 $M$ 上的一个[协变矢量](@entry_id:263917)场。在 $M$ 的任意一点 $p$ 处，$(\phi^*\omega)_p$ 的定义由它如何作用于 $p$ 点的任意切向量 $v \in T_pM$ 给出：

$$
(\phi^*\omega)_p(v) = \omega_{\phi(p)}(\phi_* v)
$$

其中 $\phi_*: T_pM \to T_{\phi(p)}N$ 是 $\phi$ 在点 $p$ 的**[推前映射](@entry_id:160933)**（或称[微分](@entry_id:158718)），它将 $M$ 上的切向量 $v$ 变换为 $N$ 上的切向量 $\phi_*v$。这个定义精妙地揭示了[拉回](@entry_id:160816)的本质：在 $M$ 上用[拉回](@entry_id:160816)后的[协变矢量](@entry_id:263917) $(\phi^*\omega)_p$ 测量一个向量 $v$，等价于先将向量 $v$ “推前”到 $N$ 中，再用 $N$ 上原始的[协变矢量](@entry_id:263917) $\omega_{\phi(p)}$ 进行测量。

尽管这个抽象定义具有根本性，但在实际计算中，我们通常采用一种更直接的坐标方法。假设 $M$ 上的[局部坐标](@entry_id:181200)为 $(x^1, \dots, x^m)$，$N$ 上的[局部坐标](@entry_id:181200)为 $(y^1, \dots, y^n)$。[光滑映射](@entry_id:203730) $\phi$ 可以用一组坐标函数表示：$y^i = y^i(x^1, \dots, x^m)$。$N$ 上的任意一个[协变矢量](@entry_id:263917)场 $\omega$ 可以写成 $\omega = \sum_{i=1}^n f_i(y) dy^i$，其中 $f_i$ 是[光滑函数](@entry_id:267124)。

计算其[拉回](@entry_id:160816) $\phi^*\omega$ 的步骤如下：
1.  **替换系数函数**：将 $\omega$ 的系数函数 $f_i(y)$ 中的变量 $y$ 替换为它们关于 $x$ 坐标的表达式，得到[复合函数](@entry_id:147347) $f_i \circ \phi$。
2.  **替换[微分](@entry_id:158718)基**：将[微分](@entry_id:158718)基 $dy^i$ 替换为其在 $x$ 坐标下的[全微分](@entry_id:171747)表达式。根据[复合函数](@entry_id:147347)[求导法则](@entry_id:145443)（链式法则），我们有：
    $$
    d(y^i \circ \phi) = \sum_{j=1}^m \frac{\partial y^i}{\partial x^j} dx^j
    $$
    因此，[拉回](@entry_id:160816)作用于[微分](@entry_id:158718)基的规则是 $\phi^*(dy^i) = d(y^i \circ \phi)$。

结合这两步，我们得到[拉回](@entry_id:160816)的坐标计算公式：

$$
\phi^*\omega = \sum_{i=1}^n (f_i \circ \phi) \, d(y^i \circ \phi) = \sum_{i=1}^n \sum_{j=1}^m f_i(y(x)) \frac{\partial y^i}{\partial x^j} dx^j
$$

让我们通过几个例子来深入理解这个过程。

**例 1：常数映射**
思考一个最简单的情形：一个从 $\mathbb{R}^2$（坐标 $(u,v)$）到 $\mathbb{R}^2$（坐标 $(x,y)$）的常数映射 $\phi(u,v) = (c_1, c_2)$，其中 $c_1, c_2$ 是常数 [@problem_id:1533194]。目标空间上任意一个 [1-形式](@entry_id:270392)为 $\omega = f(x,y)dx + g(x,y)dy$。根据[拉回](@entry_id:160816)的定义，我们有：
$$
\phi^*(x) = x \circ \phi = c_1 \quad \text{和} \quad \phi^*(y) = y \circ \phi = c_2
$$
因此，$\phi^*(dx) = d(x \circ \phi) = d(c_1) = 0$，同理 $\phi^*(dy) = 0$。于是，
$$
\phi^*\omega = (f \circ \phi) \phi^*(dx) + (g \circ \phi) \phi^*(dy) = f(c_1, c_2) \cdot 0 + g(c_1, c_2) \cdot 0 = 0
$$
这表明，任何[协变矢量](@entry_id:263917)场在常数映射下的[拉回](@entry_id:160816)都是零形式。这符合直觉：如果一个映射不产生任何“变化”，那么在源空间中就无法“感知”到目标空间中的任何梯度或流。

**例 2：退化映射**
考虑一个从 $\mathbb{R}^2$（坐标 $(u,v)$）到 $\mathbb{R}^2$（坐标 $(x,y)$）的退化映射 $\phi(u,v) = (u, c)$，其中 $c$ 为常数 [@problem_id:1533210]。这个映射将整个 $(u,v)$ 平面压缩到目标平面中的一条水平线 $y=c$ 上。我们来计算 $\omega = y dx + dy$ 的[拉回](@entry_id:160816)。
$$
\phi^*(x) = u, \quad \phi^*(y) = c
$$
$$
\phi^*(dx) = d(u) = du, \quad \phi^*(dy) = d(c) = 0
$$
因此，
$$
\phi^*\omega = (\phi^*y) (\phi^*dx) + \phi^*(dy) = c \cdot du + 0 = c \, du
$$
结果 $c \, du$ 是一个在 $(u,v)$ 平面上的 1-形式。注意，原始形式 $\omega$ 中的 $dy$ 部分在[拉回](@entry_id:160816)后消失了，这是因为映射 $\phi$ 在 $y$ 方向上是恒定的，所有关于 $y$ 的变化信息都在[拉回](@entry_id:160816)过程中丢失了。

**例 3：[坐标变换](@entry_id:172727)**
[拉回](@entry_id:160816)在[坐标变换](@entry_id:172727)中扮演着至关重要的角色。考虑从极坐标 $(r, \theta)$ 到[笛卡尔坐标](@entry_id:167698) $(x,y)$ 的标准变换 $\phi: (r, \theta) \mapsto (x,y)$，其中 $x = r\cos\theta$，$y = r\sin\theta$。让我们[拉回](@entry_id:160816)一个在 $(x,y)$ 平面上非常重要的 1-形式 $\omega = -y dx + x dy$ [@problem_id:1533207]。
首先，计算 $dx$ 和 $dy$ 的[拉回](@entry_id:160816)：
$$
\phi^*(dx) = d(r\cos\theta) = \cos\theta dr - r\sin\theta d\theta
$$
$$
\phi^*(dy) = d(r\sin\theta) = \sin\theta dr + r\cos\theta d\theta
$$
然后，将 $x$, $y$, $dx$, $dy$ 的表达式代入 $\omega$：
$$
\phi^*\omega = -(r\sin\theta)(\cos\theta dr - r\sin\theta d\theta) + (r\cos\theta)(\sin\theta dr + r\cos\theta d\theta)
$$
展开[并合](@entry_id:147963)并同类项：
$$
\phi^*\omega = (-r\sin\theta\cos\theta + r\cos\theta\sin\theta)dr + (r^2\sin^2\theta + r^2\cos^2\theta)d\theta
$$
$dr$ 的系数恰好抵消，而 $d\theta$ 的系数利用[三角恒等式](@entry_id:165065) $\sin^2\theta + \cos^2\theta = 1$ 化简为 $r^2$。最终得到：
$$
\phi^*\omega = r^2 d\theta
$$
这个结果非常优美。原始的 1-形式 $\omega = -y dx + x dy$ 在几何上与绕原点的旋转有关（它在[单位圆](@entry_id:267290)上的积分是 $2\pi$）。通过[拉回](@entry_id:160816)到极[坐标系](@entry_id:156346)，它的几何意义被清晰地揭示出来：它正比于角[微分](@entry_id:158718) $d\theta$，并且其强度随半径的平方 $r^2$ 增加，这与角动量的概念密切相关。

### [拉回](@entry_id:160816)的基本代数性质

[拉回运算](@entry_id:753859)遵循一系列优雅的代数规则，这些规则使其成为一个结构保持的映射。

1.  **线性性**: [拉回](@entry_id:160816)是线性的。对于 $N$ 上的任意两个 1-形式 $\omega_1, \omega_2$ 和任意常数 $c \in \mathbb{R}$，我们有：
    $$
    \phi^*(\omega_1 + \omega_2) = \phi^*\omega_1 + \phi^*\omega_2
    $$
    $$
    \phi^*(c\omega_1) = c(\phi^*\omega_1)
    $$
    这个性质可以通过坐标定义直接验证。例如，考虑一个映射 $\phi(t) = (t^3, 2t^2)$ 和两个 1-形式 $\omega_1 = y dx$ 及 $\omega_2 = 2x dy$ [@problem_id:1533190]。它们的和是 $\omega_3 = y dx + 2x dy$。
    我们有 $x(t) = t^3, y(t) = 2t^2$，所以 $dx = 3t^2 dt, dy = 4t dt$。
    直接计算 $\phi^*\omega_3$：
    $$
    \phi^*\omega_3 = (2t^2)(3t^2 dt) + 2(t^3)(4t dt) = 6t^4 dt + 8t^4 dt = 14t^4 dt
    $$
    分别计算 $\phi^*\omega_1$ 和 $\phi^*\omega_2$：
    $$
    \phi^*\omega_1 = (2t^2)(3t^2 dt) = 6t^4 dt
    $$
    $$
    \phi^*\omega_2 = 2(t^3)(4t dt) = 8t^4 dt
    $$
    显然，$\phi^*\omega_3 = \phi^*\omega_1 + \phi^*\omega_2$，验证了其可加性。

2.  **函[数乘](@entry_id:155971)积的性质**: 当一个 1-形式乘以一个函数时，[拉回运算](@entry_id:753859)表现出如下性质。对于 $N$ 上的函数 $f$ 和 1-形式 $\omega$：
    $$
    \phi^*(f\omega) = (\phi^*f)(\phi^*\omega) = (f \circ \phi)(\phi^*\omega)
    $$
    也就是说，函数的[拉回](@entry_id:160816)（即复合）可以从 [1-形式的拉回](@entry_id:263669)中“提出”。让我们通过一个例子来验证 [@problem_id:1533214]。设 $\phi(u,v) = (u^2, v)$，函数 $f(x,y)=y$，以及 1-形式 $\omega = dx$。我们计算 $\phi^*(f\omega) = \phi^*(y dx)$。
    首先，$\phi^*f = f \circ \phi = y(u,v) = v$。其次，$\phi^*\omega = \phi^*(dx) = d(u^2) = 2u du$。
    根据性质，我们预期结果是 $(\phi^*f)(\phi^*\omega) = v \cdot (2u du) = 2uv du$。
    现在直接计算 $\phi^*(y dx)$：
    $$
    \phi^*(y dx) = (y \circ \phi) d(x \circ \phi) = v \cdot d(u^2) = v \cdot (2u du) = 2uv du
    $$
    两者结果一致，验证了该性质。

3.  **对映射复合的[函子性](@entry_id:150069)**: [拉回](@entry_id:160816)最重要的结构性质之一是它如何处理映射的复合。如果有两个[光滑映射](@entry_id:203730) $\phi: M \to N$ 和 $\psi: N \to P$，我们可以先从 $M$ 映射到 $P$，即复合映射 $\psi \circ \phi$。这三个映射各自诱导了[拉回](@entry_id:160816)。它们之间的关系是：
    $$
    (\psi \circ \phi)^* = \phi^* \circ \psi^*
    $$
    注意右侧算子的顺序是反转的。这个性质被称为[拉回](@entry_id:160816)的**[逆变函子](@entry_id:155027)性** (contravariant functoriality)，它表明[拉回](@entry_id:160816)将映射的复合“反向”地转化为[拉回](@entry_id:160816)算子的复合。
    我们可以通过一个具体的例子来感受这一点 [@problem_id:1533187]。设 $\phi: \mathbb{R}^2_{(u,v)} \to \mathbb{R}^2_{(x,y)}$ 由 $x=uv, y=u+v$ 定义；$\psi: \mathbb{R}^2_{(x,y)} \to \mathbb{R}^2_{(z_1,z_2)}$ 由 $z_1=x+y, z_2=x-y$ 定义。我们要计算 $(\psi \circ \phi)^*(dz_1)$。
    
    方法一：先复合映射，再[拉回](@entry_id:160816)。
    $z_1 \circ \psi \circ \phi = (x+y) \circ \phi = (uv) + (u+v) = uv+u+v$。
    $(\psi \circ \phi)^*(dz_1) = d(z_1 \circ \psi \circ \phi) = d(uv+u+v) = (v du + u dv) + du + dv = (v+1)du + (u+1)dv$。

    方法二：先分别[拉回](@entry_id:160816)，再复合算子。
    首先，$\psi^*(dz_1) = d(z_1 \circ \psi) = d(x+y) = dx+dy$。
    然后，应用 $\phi^*$ 到结果 $dx+dy$ 上：
    $\phi^*(dx+dy) = \phi^*(dx) + \phi^*(dy) = d(x \circ \phi) + d(y \circ \phi) = d(uv) + d(u+v) = (vdu+udv) + (du+dv) = (v+1)du + (u+1)dv$。
    两种方法得到的结果完全相同，这正是[逆变函子](@entry_id:155027)性的体现。

### [拉回](@entry_id:160816)与外微分

[拉回](@entry_id:160816)与外微分算子 $d$ 之间存在一种深刻且极其重要的关系，这使得它们成为[微分几何](@entry_id:145818)和理论物理中不可或缺的组合。

首先，对于任何光滑函数 $g: N \to \mathbb{R}$，它的外微分 $dg$ 是 $N$ 上的一个 1-形式。同时，复合函数 $g \circ \phi$ 是 $M$ 上的一个函数，其外微分 $d(g \circ \phi)$ 是 $M$ 上的一个 1-形式。根据链式法则，我们有：
$$
d(g \circ \phi) = \phi^*(dg)
$$
这个恒等式 [@problem_id:1546227] 是如此基础，以至于有时它被用作定义函数[微分](@entry_id:158718)（即精确1-形式）[拉回](@entry_id:160816)的出发点。它将微积分中最核心的[链式法则](@entry_id:190743)用[微分形式](@entry_id:146747)的语言重新表述了出来。

更一般地，这个关系扩展到任意阶的[微分形式](@entry_id:146747)。对于[协变矢量](@entry_id:263917)场（[1-形式](@entry_id:270392)），这个关键性质是**[拉回](@entry_id:160816)与外[微分算子](@entry_id:140145)可交换**：
$$
d(\phi^*\omega) = \phi^*(d\omega)
$$
这意味着，我们可以先将一个 1-形式 $\omega$ 从 $N$ [拉回](@entry_id:160816)到 $M$ 上得到 $\phi^*\omega$，然后计算其[外微分](@entry_id:161900)；或者，先在 $N$ 上计算 $\omega$ 的[外微分](@entry_id:161900) $d\omega$（得到一个 [2-形式](@entry_id:188008)），然后再将其[拉回](@entry_id:160816)到 $M$ 上。两种途径得到的结果是相同的。

这个性质的意义是巨大的。它构成了[广义斯托克斯定理](@entry_id:159620)在[子流形](@entry_id:159439)上应用的基础，并且在电磁学和[规范场](@entry_id:159627)论中，它保证了物理定律在坐标变换下的[协变](@entry_id:634097)性。

让我们通过一个实例来验证这一性质 [@problem_id:1533229]。考虑 $\mathbb{R}^3$（坐标 $(x,y,z)$）中的 1-形式 $\omega = z dx - x dz$。以及一个从 $(u,v)$ 平面到 $\mathbb{R}^3$ 的[螺旋面](@entry_id:264087)参数化映射 $\phi(u,v) = (u\cos v, u\sin v, v)$。

路径一：先计算 $d\omega$，再[拉回](@entry_id:160816)。
在 $\mathbb{R}^3$ 中，$d\omega = d(z dx) - d(x dz) = (dz \wedge dx + z d(dx)) - (dx \wedge dz + x d(dz))$。由于 $d(dx)=0, d(dz)=0$ 且 $dz \wedge dx = -dx \wedge dz$，我们得到：
$d\omega = dz \wedge dx - dx \wedge dz = -2 dx \wedge dz$。
现在[拉回](@entry_id:160816)这个 2-形式。我们需要 $\phi^*(dx)$ 和 $\phi^*(dz)$：
$\phi^*(dx) = d(u\cos v) = \cos v du - u\sin v dv$
$\phi^*(dz) = d(v) = dv$
于是，
$\phi^*(d\omega) = \phi^*(-2 dx \wedge dz) = -2 \phi^*(dx) \wedge \phi^*(dz) = -2 (\cos v du - u\sin v dv) \wedge dv$。
利用[楔积](@entry_id:147029)的性质 ($dv \wedge dv = 0$)，上式简化为：
$\phi^*(d\omega) = -2 (\cos v du \wedge dv) = -2\cos v \, du \wedge dv$。

路径二：先[拉回](@entry_id:160816) $\omega$，再计算[外微分](@entry_id:161900)。
$\phi^*\omega = \phi^*(z dx - x dz) = (\phi^*z)(\phi^*dx) - (\phi^*x)(\phi^*dz)$
$= v (\cos v du - u\sin v dv) - (u\cos v)(dv)$
$= v\cos v du - (uv\sin v + u\cos v) dv$。
现在对这个在 $(u,v)$ 平面上的 1-形式计算[外微分](@entry_id:161900)：
$d(\phi^*\omega) = d(v\cos v \cdot du) - d((uv\sin v + u\cos v) \cdot dv)$
$= d(v\cos v) \wedge du - d(uv\sin v + u\cos v) \wedge dv$
$= (\cos v - v\sin v)dv \wedge du - ((v\sin v + \cos v)du + (uv\cos v)dv) \wedge dv$
$= -(\cos v - v\sin v)du \wedge dv - (v\sin v + \cos v)du \wedge dv$
$= (-\cos v + v\sin v - v\sin v - \cos v)du \wedge dv$
$= -2\cos v \, du \wedge dv$。
完美！两种路径得到的结果完全相同，这有力地证明了 $d\phi^* = \phi^*d$ 的普适性。

### 高等主题与应用

#### [微分同胚](@entry_id:147249)下的“推前”

[协变矢量](@entry_id:263917)天然地被“[拉回](@entry_id:160816)”，而切矢量天然地被“推前”。一般情况下，不存在[协变矢量](@entry_id:263917)的“推前”运算。然而，当映射 $\phi: M \to N$ 是一个**[微分同胚](@entry_id:147249)**时，情况就有所不同。[微分同胚](@entry_id:147249)意味着 $\phi$ 是一个光滑的双射，并且其逆映射 $\phi^{-1}: N \to M$ 也是光滑的。

在这种特殊情况下，我们可以利用逆映射 $\phi^{-1}$ 的[拉回](@entry_id:160816)，来定义一个从 $M$ 到 $N$ 的[协变矢量](@entry_id:263917)“推前”运算，记为 $\phi_\#$。对于 $M$ 上的一个[协变矢量](@entry_id:263917)场 $\omega$，其推前定义为：
$$
\phi_\#(\omega) = (\phi^{-1})^*(\omega)
$$
这个定义实际上是将 $M$ 上的 $\omega$ 通过 $\phi^{-1}$ [拉回](@entry_id:160816)到 $N$ 上，从而实现了从 $M$ 到 $N$ 的变换 [@problem_id:1546172]。这强调了一个关键点：[协变矢量](@entry_id:263917)的“推前”并非一个基本运算，而是依赖于逆映射存在这一苛刻条件下的派生概念。

#### [拉回](@entry_id:160816)映射的[单射性](@entry_id:147722)

我们可以将[拉回](@entry_id:160816) $\phi^*$ 视为一个作用于整个[协变矢量](@entry_id:263917)场空间的[线性映射](@entry_id:185132)，$\phi^*: \Omega^1(N) \to \Omega^1(M)$。一个自然的问题是：这个映射何时是单射的？[单射](@entry_id:183792)意味着，如果 $\phi^*\omega = 0$，则必然有 $\omega = 0$。换言之，没有非零的[协变矢量](@entry_id:263917)场在[拉回](@entry_id:160816)后会“消失”。

[拉回](@entry_id:160816)映射的[单射性](@entry_id:147722)与原映射 $\phi$ 的几何性质密切相关。一个关键的结论是：如果 $\phi: M \to N$ 不是一个**满射 (surjective map)**，那么其[拉回](@entry_id:160816) $\phi^*: \Omega^1(N) \to \Omega^1(M)$ 一定不是[单射](@entry_id:183792)的 [@problem_id:1681838]。

原因很简单：如果 $\phi$ 不是满射，那么在目标[流形](@entry_id:153038) $N$ 中存在一个区域 $U$ 是 $\phi(M)$ 的像集所无法触及的。我们可以在这个区域 $U$ 内构造一个非零的[协变矢量](@entry_id:263917)场 $\omega$，并使其在 $U$ 之外为零。当计算 $\phi^*\omega = (\omega \circ \phi) d(\dots)$ 时，由于 $\phi(p)$ 对于 $M$ 中任何一点 $p$ 都不在 $U$ 中，所以 $\omega \circ \phi$ 恒为零。因此，$\phi^*\omega = 0$，但我们构造的 $\omega$ 本身并非零形式。

例如，考虑映射 $F: \mathbb{R}^2 \to \mathbb{R}^3$ 定义为 $F(x,y) = (x, y, x^2-y^2)$ [@problem_id:1681838, B]。它的像集是 $\mathbb{R}^3$ 中的一个抛物面。这个映射显然不是满射。因此，我们可以找到一个非零的 1-形式 $\omega$ 在 $\mathbb{R}^3$ 上，其[拉回](@entry_id:160816) $F^*\omega$ 为零。

另一个例子是 $F: \mathbb{R}^2 \to \mathbb{R}$ 定义为 $F(x,y) = \sin(x)+2$ [@problem_id:1681838, E]。它的像集是区间 $[1,3]$，这并非整个 $\mathbb{R}$。因此，我们可以选取一个在 $(-\infty, 1)$ 上有支撑的非零 1-形式 $\omega = f(u)du$。由于 $F(x,y)$ 的值域与 $f(u)$ 的支撑域不相交，$(f \circ F)$ 恒为零，导致 $F^*\omega = 0$。

反之，如果一个映射是**淹没 (submersion)**（一个比满射更强的局部条件，粗略地说，其[微分](@entry_id:158718)在每一点都是满射），那么其[拉回](@entry_id:160816)映射是[单射](@entry_id:183792)的。理解这些性质，有助于我们从映射的几何行为来预判其对微分形式所诱导的变换的代数特性。