## 引言
在探索[微分](@entry_id:158718)[流形](@entry_id:153038)世界的旅程中，我们已经将微分形式确立为描述局部几何与物理量的强大语言。然而，一个关键问题随之而来：我们如何在不同的[流形](@entry_id:153038)之间，或是在一个[流形](@entry_id:153038)与其[子流形](@entry_id:159439)之间，建立起这些几何结构的联系？这正是“**[1-形式的拉回](@entry_id:263669) (Pullback of a One-form)**”这一核心概念所要解决的问题。它远不止是[多变量微积分](@entry_id:147547)中简单的变量替换，而是微分几何中一座连接代数、几何与拓扑的桥梁。

本文将系统地引导您掌握[拉回](@entry_id:160816)这一基本工具。在第一章**“原理与机制”**中，我们将从[拉回](@entry_id:160816)的严格定义和几何直观入手，学习其在坐标下的两种计算方法，并剖析其关键的代数性质。随后，在第二章**“应用与跨学科联系”**中，我们将视野拓宽，探索[拉回](@entry_id:160816)如何作为一种通用语言，在验证物理定律的[不变性](@entry_id:140168)、在[子流形](@entry_id:159439)上诱导场、以及揭示[流形的拓扑](@entry_id:267834)[不变量](@entry_id:148850)（如[德拉姆上同调](@entry_id:158673)）中发挥至关重要的作用。最后，**“动手实践”**部分将提供一系列精心设计的问题，帮助您将理论知识转化为扎实的计算与应用能力。

让我们首先进入**“原理与机制”**，揭开[拉回](@entry_id:160816)的神秘面纱，理解它如何精确地将一个[流形](@entry_id:153038)上的几何信息“[拉回](@entry_id:160816)”到另一个[流形](@entry_id:153038)之上。

## 原理与机制

在上一章中，我们介绍了[微分形式](@entry_id:146747)作为[多变量微积分](@entry_id:147547)中被积对象的一般化概念。现在，我们将探讨一个核心工具，它使我们能够在不同[流形](@entry_id:153038)之间传递这些几何结构，这个工具就是**[拉回](@entry_id:160816) (pullback)**。[拉回](@entry_id:160816)是微分几何中的“变量替换”法则，但其作用远不止于此，它构成了[流形理论](@entry_id:263722)中许多深刻结果的基石。

### [拉回](@entry_id:160816)的定义与几何直观

想象我们有两个光滑流形 $M$ 和 $N$，以及一个[光滑映射](@entry_id:203730) $F: M \to N$。如果在目标[流形](@entry_id:153038) $N$ 上存在一个 1-形式 $\omega$，我们如何利用映射 $F$ 在源[流形](@entry_id:153038) $M$ 上定义一个相应的 1-形式呢？这个新的 [1-形式](@entry_id:270392)被称为 $\omega$ 在 $F$ 作用下的**[拉回](@entry_id:160816)**，记作 $F^*\omega$。

要定义在 $M$ 上的 1-形式 $F^*\omega$，我们需要说明它如何作用于 $M$ 上任意一点 $p$ 的任意一个切向量 $w \in T_pM$。其核心思想是，利用映射 $F$ 将问题“推送”到[流形](@entry_id:153038) $N$ 上，在 $N$ 上利用已知的 [1-形式](@entry_id:270392) $\omega$ 进行计算，然后将结果“[拉回](@entry_id:160816)”到 $M$。

这个过程分为三步：
1.  **点的映射**：我们将源[流形](@entry_id:153038)中的点 $p \in M$ 通过映射 $F$ 映到目标[流形](@entry_id:153038)中的点 $F(p) \in N$。
2.  **向量的推送**：我们将点 $p$ 处的[切向量](@entry_id:265494) $w \in T_pM$ 通过 $F$ 的[微分](@entry_id:158718)（或称**[前推](@entry_id:158718) (pushforward)**）$dF_p$ 映为点 $F(p)$ 处的一个切向量 $dF_p(w) \in T_{F(p)}N$。
3.  **形式的求值**：现在，我们在目标[流形](@entry_id:153038) $N$ 上有了一个点 $F(p)$ 和一个在该点处的[切向量](@entry_id:265494) $dF_p(w)$。这正是 1-形式 $\omega$ 所需的输入。我们将 $\omega$ 在点 $F(p)$ 处作用于向量 $dF_p(w)$，得到一个实数 $\omega_{F(p)}(dF_p(w))$。

这个最终得到的实数，我们定义为[拉回](@entry_id:160816)形式 $(F^*\omega)$ 在点 $p$ 处作用于向量 $w$ 的值。

**定义：[1-形式的拉回](@entry_id:263669)**
设 $F: M \to N$ 是一个[光滑映射](@entry_id:203730)，$\omega$ 是 $N$ 上的一个 [1-形式](@entry_id:270392)。$\omega$ 的[拉回](@entry_id:160816) $F^*\omega$ 是 $M$ 上的一个 [1-形式](@entry_id:270392)，其在任意点 $p \in M$ 和任意[切向量](@entry_id:265494) $w \in T_pM$ 上的定义为：
$$
(F^*\omega)_p(w) = \omega_{F(p)}(dF_p(w))
$$

这个定义虽然抽象，但它完美地体现了“通过映射关联计算”的几何思想。让我们通过一个具体的例子来剖析这个过程。

**示例：验证[拉回](@entry_id:160816)的定义** [@problem_id:1681842]

假设有两个[二维流形](@entry_id:188198) $M$（坐标为 $(u,v)$）和 $N$（坐标为 $(x,y)$）。映射 $F: M \to N$ 定义为 $x(u,v) = u^2 - v^2$ 和 $y(u,v) = 2uv$。在 $N$ 上有一个 1-形式 $\omega = \frac{-y}{x^2+y^2} dx + \frac{x}{x^2+y^2} dy$。我们希望计算 $(F^*\omega)_p(w)$，其中 $p=(2,1) \in M$，$w = 3 \frac{\partial}{\partial u}\big|_p - 4 \frac{\partial}{\partial v}\big|_p$ 是 $p$ 点的一个[切向量](@entry_id:265494)。

根据定义，我们按部就班地计算：
1.  **计算 $F(p)$**：
    $F(p) = (x(2,1), y(2,1)) = (2^2 - 1^2, 2 \cdot 2 \cdot 1) = (3,4)$。这是 $N$ 上的一个点。

2.  **计算 $dF_p(w)$**：
    $dF_p(w)$ 是 $N$ 中 $F(p)=(3,4)$ 点的一个切向量。它的分量可以通过 $w$ 作用于坐标函数 $x$ 和 $y$ 来得到：
    $dF_p(w) = w(x) \frac{\partial}{\partial x}\big|_{F(p)} + w(y) \frac{\partial}{\partial y}\big|_{F(p)}$。
    其中，$w(x) = (3 \frac{\partial}{\partial u} - 4 \frac{\partial}{\partial v})(x) = 3 \frac{\partial x}{\partial u}\big|_p - 4 \frac{\partial x}{\partial v}\big|_p$。
    在 $p=(2,1)$ 处，[偏导数](@entry_id:146280)为：$\frac{\partial x}{\partial u} = 2u = 4$，$\frac{\partial x}{\partial v} = -2v = -2$。
    所以，$w(x) = 3(4) - 4(-2) = 20$。
    同理，$w(y) = 3 \frac{\partial y}{\partial u}\big|_p - 4 \frac{\partial y}{\partial v}\big|_p$。
    在 $p=(2,1)$ 处，[偏导数](@entry_id:146280)为：$\frac{\partial y}{\partial u} = 2v = 2$，$\frac{\partial y}{\partial v} = 2u = 4$。
    所以，$w(y) = 3(2) - 4(4) = -10$。
    因此，[前推](@entry_id:158718)的向量是 $dF_p(w) = 20 \frac{\partial}{\partial x}\big|_{(3,4)} - 10 \frac{\partial}{\partial y}\big|_{(3,4)}$。

3.  **计算 $\omega_{F(p)}(dF_p(w))$**：
    我们将 $\omega$ 在点 $F(p)=(3,4)$ 处作用于向量 $dF_p(w)$。
    $\omega$ 在 $(x,y)=(3,4)$ 处的系数为：
    $\frac{-y}{x^2+y^2} = \frac{-4}{3^2+4^2} = -\frac{4}{25}$
    $\frac{x}{x^2+y^2} = \frac{3}{3^2+4^2} = \frac{3}{25}$
    所以，$\omega_{(3,4)} = -\frac{4}{25} dx + \frac{3}{25} dy$。
    将其作用于 $dF_p(w)$：
    $\omega_{F(p)}(dF_p(w)) = \left(-\frac{4}{25} dx + \frac{3}{25} dy\right) \left(20 \frac{\partial}{\partial x} - 10 \frac{\partial}{\partial y}\right)$
    $= -\frac{4}{25} \cdot 20 + \frac{3}{25} \cdot (-10) = -\frac{80}{25} - \frac{30}{25} = -\frac{110}{25} = -\frac{22}{5}$。

最终，我们得到 $(F^*\omega)_p(w) = -\frac{22}{5}$。这个例子展示了定义的每一步是如何在具体计算中实现的。

### 坐标下的计算方法

虽然上述定义在概念上至关重要，但在实际计算中，我们通常采用一种更直接的代数方法，即在[局部坐标](@entry_id:181200)下进行计算。这种方法基于[拉回](@entry_id:160816)作用于函数（0-形式）和基底 [1-形式](@entry_id:270392)的规则。

1.  **对函数（0-形式）的[拉回](@entry_id:160816)**：对于 $N$ 上的一个函数 $g$，$F^*g$ 是 $M$ 上的一个函数，定义为复合函数 $g \circ F$。即 $(F^*g)(p) = g(F(p))$。

2.  **对基底[微分](@entry_id:158718)的[拉回](@entry_id:160816)**：如果 $y^j$ 是 $N$ 上的一个坐标函数，那么 $F^*(dy^j)$ 是 $M$ 上的一个 [1-形式](@entry_id:270392)。根据一个核心性质（我们将在下一节探讨），[拉回](@entry_id:160816)与外微分算子 $d$ 是可交换的，即 $F^*(dg) = d(F^*g)$。将此应用于坐标函数 $y^j$，我们得到 $F^*(dy^j) = d(F^*y^j) = d(y^j \circ F)$。
    如果 $F$ 在坐标中由 $y^j = y^j(x^1, \dots, x^m)$ 给出，那么根据全[微分法则](@entry_id:169252)：
    $$
    F^*(dy^j) = d(y^j(x^1, \dots, x^m)) = \sum_{i=1}^m \frac{\partial y^j}{\partial x^i} dx^i
    $$

结合这两条规则，我们可以计算任何 [1-形式](@entry_id:270392) $\omega = \sum_j g_j(y) dy^j$ 的[拉回](@entry_id:160816)：
$$
F^*\omega = F^*\left(\sum_j g_j dy^j\right) = \sum_j (F^*g_j) (F^*dy^j) = \sum_j (g_j \circ F) \left(\sum_i \frac{\partial y^j}{\partial x^i} dx^i\right)
$$

这提供了一个简单明了的计算流程：
**将目标坐标的表达式和它们的[微分](@entry_id:158718)，全部用源坐标的表达式和它们的[微分](@entry_id:158718)代入，然后化简。**

**示例：[坐标变换](@entry_id:172727)下的[拉回](@entry_id:160816)**

让我们通过几个经典例子来掌握这种计算方法。

1.  **[复变函数](@entry_id:175282)平方映射** [@problem_id:1681792]
    考虑映射 $F: \mathbb{R}^2 \to \mathbb{R}^2$，其中 $(u,v) \mapsto (x,y)$ 由 $x = u^2 - v^2$ 和 $y = 2uv$ 给出（这对应于复数平面上的 $z \mapsto z^2$，其中 $z=u+iv$）。我们来计算 [1-形式](@entry_id:270392) $\omega = x dy - y dx$ 的[拉回](@entry_id:160816) $F^*\omega$。
    首先，计算 $dx$ 和 $dy$ 的[拉回](@entry_id:160816)：
    $F^*(dx) = d(u^2 - v^2) = 2u du - 2v dv$
    $F^*(dy) = d(2uv) = 2v du + 2u dv$
    然后，将 $x, y, dx, dy$ 全部替换：
    $F^*\omega = (u^2 - v^2)(2v du + 2u dv) - (2uv)(2u du - 2v dv)$
    展开并按 $du$ 和 $dv$ 合并同类项：
    $du$ 的系数是：$(u^2 - v^2)(2v) - (2uv)(2u) = 2u^2v - 2v^3 - 4u^2v = -2u^2v - 2v^3 = -2v(u^2+v^2)$
    $dv$ 的系数是：$(u^2 - v^2)(2u) - (2uv)(-2v) = 2u^3 - 2uv^2 + 4uv^2 = 2u^3 + 2uv^2 = 2u(u^2+v^2)$
    所以，$F^*\omega = -2v(u^2+v^2) du + 2u(u^2+v^2) dv = 2(u^2+v^2)(-v du + u dv)$。

2.  **极[坐标变换](@entry_id:172727)** [@problem_id:1681853]
    [笛卡尔坐标](@entry_id:167698) $(x,y)$ 和极坐标 $(r,\theta)$ 之间的关系由映射 $F: (r,\theta) \mapsto (x,y)$ 给出，$x = r\cos\theta, y = r\sin\theta$。让我们计算 [1-形式](@entry_id:270392) $\omega = y dx - x dy$ 在这个变换下的[拉回](@entry_id:160816)（注意这里我们把笛卡尔坐标看作目标，极坐标看作源）。
    $F^*(dx) = d(r\cos\theta) = \cos\theta dr - r\sin\theta d\theta$
    $F^*(dy) = d(r\sin\theta) = \sin\theta dr + r\cos\theta d\theta$
    替换到 $\omega$ 中：
    $F^*\omega = (r\sin\theta)(\cos\theta dr - r\sin\theta d\theta) - (r\cos\theta)(\sin\theta dr + r\cos\theta d\theta)$
    展开：
    $F^*\omega = (r\sin\theta\cos\theta) dr - r^2\sin^2\theta d\theta - (r\cos\theta\sin\theta) dr - r^2\cos^2\theta d\theta$
    $dr$ 项相互抵消，合并 $d\theta$ 项：
    $F^*\omega = -r^2(\sin^2\theta + \cos^2\theta) d\theta = -r^2 d\theta$
    这个结果非常简洁和优美。原来在[笛卡尔坐标](@entry_id:167698)下形式复杂的 $\omega$（它与二维的“转动”或角动量有关），在极坐标下变成了简单的 $-r^2 d\theta$。这揭示了 $\omega$ 的内在几何意义，并展示了[拉回](@entry_id:160816)作为“翻译工具”的威力。通过[拉回](@entry_id:160816)，我们可以选择最适合问题的[坐标系](@entry_id:156346)来进行分析。

    更进一步，我们还可以计算“角度形式” $\omega_{\text{angle}} = \frac{-y dx + x dy}{x^2+y^2}$ 的[拉回](@entry_id:160816) [@problem_id:1681821]。读者可以自行验证，在使用复平方映射 $F(u,v)=(u^2-v^2, 2uv)$ 时，其[拉回](@entry_id:160816) $F^*\omega_{\text{angle}}$ 会得到 $\frac{2(-v du + u dv)}{u^2+v^2}$。这个结果可以被解释为角度的加倍，与复数平方的几何意义相符。

### [拉回](@entry_id:160816)的基本性质

[拉回运算](@entry_id:753859)满足一系列重要的代数性质，这些性质使其成为一个强大而可靠的工具。设 $F: M \to N$ 和 $G: N \to P$ 是[光滑映射](@entry_id:203730)，$\omega, \eta$ 是 $N$ 上的 [1-形式](@entry_id:270392)，$g$ 是 $N$ 上的函数（0-形式），$c$ 是常数。

1.  **线性性**: $F^*(c\omega + g\eta) = c(F^*\omega) + (F^*g)(F^*\eta)$。
    特别地，如果 $c_1, c_2$ 是常数，$F^*(c_1\omega + c_2\eta) = c_1(F^*\omega) + c_2(F^*\eta)$。

2.  **与[楔积](@entry_id:147029)的相容性**: [拉回运算](@entry_id:753859)保持[楔积](@entry_id:147029)结构：$F^*(\omega \wedge \eta) = (F^*\omega) \wedge (F^*\eta)$。

3.  **[函子性](@entry_id:150069)（复合映射）**: [拉回运算](@entry_id:753859)与映射的复合“反向”兼容：
    $$
    (G \circ F)^* = F^* \circ G^*
    $$
    这意味着，先复合映射再[拉回](@entry_id:160816)，等价于先从 $P$ [拉回](@entry_id:160816)到 $N$，再从 $N$ [拉回](@entry_id:160816)到 $M$。这个性质非常有用，它允许我们将复杂的映射分解为简单的步骤来处理 [@problem_id:1681834] [@problem_id:1681795]。

    例如，要计算 $(G \circ F)^*\omega$，我们可以先计算 [1-形式](@entry_id:270392) $\eta = G^*\omega$（这是一个在 $N$ 上的形式），然后计算 $F^*\eta$（这是一个在 $M$ 上的形式），最终结果就是所求的 $(G \circ F)^*\omega$。这种分步计算有时比直接计算复合映射的[拉回](@entry_id:160816)要简单 [@problem_id:1681795]。

4.  **与[外微分](@entry_id:161900)的[可交换性](@entry_id:263314)**: 这是[拉回](@entry_id:160816)最深刻的性质之一。[拉回运算](@entry_id:753859)与外[微分算子](@entry_id:140145) $d$ 可交换：
    $$
    F^*(d\omega) = d(F^*\omega)
    $$
    对于任何 $k$-形式 $\omega$ 都成立。当 $\omega$ 是一个 0-形式（即一个函数 $g$）时，这个性质变为 $F^*(dg) = d(F^*g)$ [@problem_id:1681837]。
    这个等式两边的含义是：
    -   左边 $F^*(dg)$：先在 $N$ 上求 $g$ 的[微分](@entry_id:158718)得到 1-形式 $dg$，然后再将其[拉回](@entry_id:160816)到 $M$。
    -   右边 $d(F^*g)$：先将函数 $g$ [拉回](@entry_id:160816)到 $M$ 得到函数 $F^*g = g \circ F$，然后再在 $M$ 上求这个新[函数的微分](@entry_id:274991)。
    这个性质表明，这两种顺序不同的操作会得到完全相同的结果。

### 特殊情况与进阶讨论

#### 常数映射
一个简单但重要的特例是当 $F: M \to N$ 是一个**常数映射**时，即对所有 $p \in M$，$F(p) = c$（$N$ 中的一个[固定点](@entry_id:156394)）。此时，对于 $N$ 上的任何 1-形式 $\omega$，其[拉回](@entry_id:160816) $F^*\omega$ 都是 $M$ 上的零形式 [@problem_id:1681847]。

这是因为在坐标计算中，$F^*(dy^j) = d(y^j \circ F)$。由于 $y^j \circ F$ 是一个[常数函数](@entry_id:152060)，其[微分](@entry_id:158718)为零。因此，$F^*\omega$ 的所有分量都将为零。从几何上看，常数映射将整个[流形](@entry_id:153038) $M$ 压缩到 $N$ 上的一个点，所有关于方向和变化的信息都丢失了，所以[拉回](@entry_id:160816)的形式自然为零。

#### [拉回](@entry_id:160816)映射的[单射性](@entry_id:147722)
我们可以将[拉回](@entry_id:160816) $F^*$ 视为一个作用于微分形式空间的线性映射，$F^*: \Omega^1(N) \to \Omega^1(M)$。一个自然的问题是：这个[线性映射](@entry_id:185132)何时是[单射](@entry_id:183792)的？[单射](@entry_id:183792)意味着，如果 $F^*\omega = 0$，那么一定有 $\omega=0$。换句话说，没有非零的 1-形式在[拉回](@entry_id:160816)后“消失”。

这个问题的答案与映射 $F$ 本身的几何性质紧密相关 [@problem_id:1681838]。

-   一个直接的结论是：如果映射 $F: M \to N$ **不是满射 (surjective)**，那么 $F^*$ **不是[单射](@entry_id:183792)的**。
    直观的解释是，如果 $F$ 的像 $F(M)$ 没有覆盖整个 $N$，我们就可以在 $N$ 的“空白”区域 $N \setminus F(M)$ 中构造一个非零的 [1-形式](@entry_id:270392) $\omega$（例如，一个支集完全在该区域内的形式）。当我们将 $\omega$ [拉回](@entry_id:160816)到 $M$ 时，由于 $\omega$ 在 $F(M)$ 上恒为零，我们有 $(\omega \circ F) \equiv 0$，因此 $F^*\omega = 0$。但 $\omega$ 本身并非零形式，所以 $F^*$ 不是单射的。例如，从 $\mathbb{R}^2$ 到 $\mathbb{R}^3$ 的嵌入映射，其像是一个[曲面](@entry_id:267450)，不是满射，所以其[拉回](@entry_id:160816)不是单射的。

-   反之，一个充分条件是：如果 $F$ 是一个**淹没 (submersion)**（即其[微分](@entry_id:158718) $dF_p$ 在每一点 $p$ 都是满射），那么 $F^*$ 是单射的。

#### 对[上同调](@entry_id:160558)的启示
[拉回](@entry_id:160816)与外微分的可交换性 $F^*d=dF^*$ 是一个极其深刻的性质。它表明，[拉回](@entry_id:160816)将[闭形式](@entry_id:272960)（$d\omega=0$）映为闭形式（$d(F^*\omega)=F^*(d\omega)=F^*(0)=0$），并将恰当形式（$\omega=d\alpha$）映为恰当形式（$F^*\omega=F^*(d\alpha)=d(F^*\alpha)$）。

这意味着[拉回](@entry_id:160816)诱导了一个在**[德拉姆上同调](@entry_id:158673)群 (de Rham cohomology groups)** 之间的[良定义映射](@entry_id:136264)：
$$
F^*: H^k_{dR}(N) \to H^k_{dR}(M)
$$
[上同调群](@entry_id:142450)是[流形的拓扑](@entry_id:267834)[不变量](@entry_id:148850)，它捕捉了[流形](@entry_id:153038)的“洞”的信息。[拉回](@entry_id:160816)提供了一个通过[光滑映射](@entry_id:203730)来研究不同[流形](@entry_id:153038)拓扑结构之间关系的代数工具。例如，可以证明，如果两个[流形](@entry_id:153038)是同伦等价的，那么它们具有同构的上同调群。

一个优美的例子是切丛的[投影映射](@entry_id:153398) $\pi: TM \to M$，它将每个切向量映回其基点。由于[流形](@entry_id:153038) $M$ 可以看作是其[切丛](@entry_id:161294) $TM$ 的一个[形变收缩](@entry_id:148036)核，$\pi$ 诱导的上同调映射 $\pi^*: H^k_{dR}(M) \to H^k_{dR}(TM)$ 实际上是一个同构 [@problem_id:1681800]。这一事实表明，尽管[切丛](@entry_id:161294)的维数更高，但其拓扑复杂性（由[上同调](@entry_id:160558)衡量）与基[流形](@entry_id:153038)完全相同。这展示了[拉回](@entry_id:160816)在连接几何与拓扑方面的强大力量。

总之，[拉回](@entry_id:160816)不仅是进行[坐标变换](@entry_id:172727)计算的实用工具，更是联系不同[流形](@entry_id:153038)上微积分、几何和拓扑的理论桥梁。掌握其定义、计算方法和基本性质，是深入学习现代微分几何不可或缺的一步。