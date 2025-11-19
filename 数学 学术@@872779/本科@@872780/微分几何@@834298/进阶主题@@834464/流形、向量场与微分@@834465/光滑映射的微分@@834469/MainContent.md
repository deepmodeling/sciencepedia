## 引言
在微分几何的探索中，光滑流形构成了我们研究的基本空间，而[光滑映射](@entry_id:203730)则是连接这些空间的桥梁。然而，这些映射本质上的[非线性](@entry_id:637147)特性为直接分析带来了巨大挑战。如何才能有效地研究一个[流形](@entry_id:153038)到另一个[流形](@entry_id:153038)的复杂变换？本文旨在解决这一核心问题，引入了一个强大的工具——[光滑映射的微分](@entry_id:268823)。[微分](@entry_id:158718)的本质思想是将复杂的[非线性映射](@entry_id:272931)在每一点局部地简化为一个线性的、易于处理的切映射，这构成了现代[微分几何](@entry_id:145818)的基石。

在接下来的内容中，您将踏上一段系统性的学习之旅。在“原理与机制”一章，我们将建立[微分](@entry_id:158718)的严格定义，探讨其与雅可比矩阵的联系，并掌握其核心性质如[链式法则](@entry_id:190743)。随后，在“应用与跨学科联系”一章，我们将视野拓宽，见证[微分](@entry_id:158718)如何被用于刻画浸入、淹没等几何现象，并成为连接物理学、复分析和[李理论](@entry_id:148240)等领域的关键纽带。最后，通过“动手实践”部分，您将有机会巩固所学知识，解决具体问题。让我们首先深入其核心，从[微分](@entry_id:158718)的原理与机制开始。

## 原理与机制

在上一章中，我们熟悉了[光滑流形](@entry_id:160799)作为[微分几何](@entry_id:145818)基本研究对象的概念。现在，我们转向研究这些[流形](@entry_id:153038)之间的关系，即[光滑映射](@entry_id:203730)。正如线性代数研究[向量空间](@entry_id:151108)之间的[线性变换](@entry_id:149133)一样，[微分几何](@entry_id:145818)的核心是研究光滑流形之间的[光滑映射](@entry_id:203730)。然而，直接处理[非线性](@entry_id:637147)的[光滑映射](@entry_id:203730)是困难的。关键的突破在于，在每一点的局部，我们可以用一个[线性映射](@entry_id:185132)来逼近一个[光滑映射](@entry_id:203730)。这个[线性逼近](@entry_id:142309)就是本章的主角——**[微分](@entry_id:158718)**（differential），也被称为**切映射**（tangent map）或**[前推](@entry_id:158718)**（pushforward）。

### [微分](@entry_id:158718)：光滑[映射的线性化](@entry_id:276268)

想象一下，你有一个光滑的函数 $f: \mathbb{R} \to \mathbb{R}$。在任意一点 $p$，这条曲线都可以用它的[切线](@entry_id:268870)来近似。这条[切线的斜率](@entry_id:192479) $f'(p)$ 描述了当输入发生微小变化时，输出如何线性地变化。[光滑映射的微分](@entry_id:268823)正是这个概念在任意维度[光滑流形](@entry_id:160799)上的推广。

给定一个[光滑映射](@entry_id:203730) $F: M \to N$，其中 $M$ 和 $N$ 是[光滑流形](@entry_id:160799)，对于 $M$ 中的每一点 $p$，这个映射都诱导了一个介于对应[切空间](@entry_id:199137)之间的[线性映射](@entry_id:185132)，称为 $F$ 在点 $p$ 的**[微分](@entry_id:158718)**，记作 $dF_p$ 或 $F_{*,p}$。
$$
dF_p: T_pM \to T_{F(p)}N
$$
这个[线性映射](@entry_id:185132) $dF_p$ 捕捉了映射 $F$ 在点 $p$ 附近的局部行为。它告诉我们，当我们沿着 $p$ 点的一个切向量 $v_p \in T_pM$ "移动"时，$F$ 的像会相应地沿着 $F(p)$ 点的哪个切向量 $dF_p(v_p) \in T_{F(p)}N$ "移动"。

从形式上讲，切向量可以被看作是作用于光滑函数上的导子。基于这个观点，[微分](@entry_id:158718) $dF_p$ 的作用可以精确定义如下：对于任意切向量 $v_p \in T_pM$ 和任意定义在 $N$ 上 $F(p)$ 点邻域内的[光滑函数](@entry_id:267124) $g: N \to \mathbb{R}$，像向量 $dF_p(v_p)$ 作用于 $g$ 的结果是：
$$
(dF_p(v_p))(g) = v_p(g \circ F)
$$
这个定义是优雅且抽象的。它表明，要了解向量 $v_p$ 在经过 $F$ 的变换后如何影响 $N$ 上的函数 $g$，我们只需通过复合函数 $g \circ F$ 将 $g$ "[拉回](@entry_id:160816)"到 $M$ 上，然后让原始向量 $v_p$ 直接作用于这个[复合函数](@entry_id:147347)。

### 雅可比矩阵：[坐标系](@entry_id:156346)下的[微分](@entry_id:158718)

虽然[微分](@entry_id:158718)的抽象定义很强大，但在实际计算中，我们通常在局部坐标系下工作。在[坐标系](@entry_id:156346)中，[切向量](@entry_id:265494)可以表示为分量的元组，而[线性映射](@entry_id:185132)则可以表示为矩阵。[微分](@entry_id:158718) $dF_p$ 的矩阵表示被称为**[雅可比矩阵](@entry_id:264467)**（Jacobian matrix）。

假设 $M$ 是一个 $m$ 维[流形](@entry_id:153038)，在点 $p$ 附近有[局部坐标系](@entry_id:751394) $(x^1, \dots, x^m)$。$N$ 是一个 $n$ 维[流形](@entry_id:153038)，在点 $F(p)$ 附近有局部坐标系 $(y^1, \dots, y^n)$。那么，[光滑映射](@entry_id:203730) $F$ 在这些[坐标系](@entry_id:156346)下可以表示为一组函数：
$$
y^i = F^i(x^1, \dots, x^m), \quad i = 1, \dots, n
$$
[切空间](@entry_id:199137) $T_pM$ 的一组自然基底是 $\{\frac{\partial}{\partial x^1}|_p, \dots, \frac{\partial}{\partial x^m}|_p\}$，而 $T_{F(p)}N$ 的自然基底是 $\{\frac{\partial}{\partial y^1}|_{F(p)}, \dots, \frac{\partial}{\partial y^n}|_{F(p)}\}$。[微分](@entry_id:158718) $dF_p$ 在这两组基底下的[矩阵表示](@entry_id:146025)，即[雅可比矩阵](@entry_id:264467) $J_F(p)$，是一个 $n \times m$ 矩阵，其第 $i$ 行第 $j$ 列的元素为：
$$
(J_F(p))_{ij} = \frac{\partial F^i}{\partial x^j}(p)
$$
这个矩阵完全描述了线性映射 $dF_p$。如果一个切向量 $v_p \in T_pM$ 在[坐标系](@entry_id:156346)下的分量是 $v = (v^1, \dots, v^m)^T$，那么它的像 $dF_p(v_p)$ 在[坐标系](@entry_id:156346)下的分量 $w = (w^1, \dots, w^n)^T$ 就是通过矩阵乘法得到的：
$$
w = J_F(p) \cdot v
$$

一个非常经典且重要的例子是从极坐标到[笛卡尔坐标](@entry_id:167698)的转换。这可以看作是一个从 $\mathbb{R}^2$ 的一个开[子集](@entry_id:261956) $U = \{(r, \theta) \mid r > 0\}$ 到 $\mathbb{R}^2$ 的[光滑映射](@entry_id:203730) $F$。该映射由方程 $x = r\cos(\theta)$ 和 $y = r\sin(\theta)$ 定义。要计算其[微分](@entry_id:158718)的[矩阵表示](@entry_id:146025)，我们需求解其[雅可比矩阵](@entry_id:264467)[@problem_id:1671525]。
$$
J_F(r, \theta) = \begin{pmatrix} \frac{\partial x}{\partial r}  \frac{\partial x}{\partial \theta} \\ \frac{\partial y}{\partial r}  \frac{\partial y}{\partial \theta} \end{pmatrix} = \begin{pmatrix} \cos(\theta)  -r\sin(\theta) \\ \sin(\theta)  r\cos(\theta) \end{pmatrix}
$$
这个矩阵告诉我们，极[坐标系](@entry_id:156346)中的[基向量](@entry_id:199546) $\frac{\partial}{\partial r}$ 和 $\frac{\partial}{\partial \theta}$ 在笛卡尔坐标系中是如何表示的。例如，$dF_p(\frac{\partial}{\partial r}|_p)$ 对应的向量是 $(\cos(\theta), \sin(\theta))^T$，这正是在该点处径向单位向量。

雅可比矩阵的维度取决于[定义域和陪域](@entry_id:159300)[流形](@entry_id:153038)的维度。例如，对于一个从 $\mathbb{R}^2$ 到 $\mathbb{R}^3$ 的[光滑映射](@entry_id:203730) $F(x, y) = (x^3, y^3, xy)$，其[微分](@entry_id:158718)在点 $p=(x_0, y_0)$ 的[矩阵表示](@entry_id:146025)是一个 $3 \times 2$ 的矩阵[@problem_id:1671489]：
$$
J_F(x_0, y_0) = \begin{pmatrix} 3x_0^2  0 \\ 0  3y_0^2 \\ y_0  x_0 \end{pmatrix}
$$

### [微分](@entry_id:158718)的基本性质

作为一种基本的构造，[微分](@entry_id:158718)具有一些必须掌握的核心性质。

#### 线性

从定义可知，$dF_p$ 是一个**线性映射**。这意味着它保持向量的加法和[标量乘法](@entry_id:155971)：
$$
dF_p(a v_p + b w_p) = a\, dF_p(v_p) + b\, dF_p(w_p)
$$
其中 $v_p, w_p \in T_pM$，$a, b \in \mathbb{R}$。这个性质也可以通过雅可比矩阵来验证。例如，对于映射 $F(x, y) = (x^2y, x - y^2)$ 和点 $p = (1, 2)$，我们可以计算其雅可比矩阵[@problem_id:1671517]：
$$
J_F(1, 2) = \begin{pmatrix} 4  1 \\ 1  -4 \end{pmatrix}
$$
如果我们有两个向量 $v_p$ 和 $w_p$，其坐标分量分别为 $v = (3, -1)^T$ 和 $w = (1, 4)^T$，以及标量 $a=2, b=-1$，那么线性组合向量 $u_p = a v_p + b w_p$ 的坐标为 $u = (5, -6)^T$。其像[向量的坐标](@entry_id:198852)为：
$$
J_F(p) \cdot u = \begin{pmatrix} 4  1 \\ 1  -4 \end{pmatrix} \begin{pmatrix} 5 \\ -6 \end{pmatrix} = \begin{pmatrix} 14 \\ 29 \end{pmatrix}
$$
这与分别计算 $a J_F(p)v + b J_F(p)w$ 的结果是相同的，验证了其线性。

#### 恒同[映射的微分](@entry_id:269524)

如果 $F$ 是[流形](@entry_id:153038) $M$ 上的**恒同映射**（identity map），即 $\text{id}_M: M \to M$，$q \mapsto q$，那么它在任意点 $p$ 的[微分](@entry_id:158718) $d(\text{id}_M)_p$ 就是切空间 $T_pM$ 上的恒同变换[@problem_id:1671532]。这符合我们的直觉：如果我们根本没有移动，那么切向量也应该保持不变。在任何[坐标系](@entry_id:156346)下，恒同映射的雅可比矩阵都是[单位矩阵](@entry_id:156724)。

#### 链式法则

[微分](@entry_id:158718)最重要的性质之一是**[链式法则](@entry_id:190743)**（Chain Rule）。如果我们有两个[光滑映射](@entry_id:203730) $F: M \to N$ 和 $G: N \to P$，我们可以构造它们的复合映射 $H = G \circ F: M \to P$。[链式法则](@entry_id:190743)表明，复合[映射的微分](@entry_id:269524)等于各个映射[微分](@entry_id:158718)的复合：
$$
d(G \circ F)_p = dG_{F(p)} \circ dF_p
$$
在[坐标系](@entry_id:156346)下，这个法则体现为[雅可比矩阵](@entry_id:264467)的乘法：
$$
J_{G \circ F}(p) = J_G(F(p)) \cdot J_F(p)
$$
这正是多元微积分中我们熟悉的链式法则的几何形式。例如，考虑映射 $F: \mathbb{R} \to \mathbb{R}^2$，$F(t) = (t^2, e^{-t})$ 和 $G: \mathbb{R}^2 \to \mathbb{R}$，$G(x,y) = x^2 y$。复合映射 $H(t) = G(F(t)) = (t^2)^2 e^{-t} = t^4 e^{-t}$。根据单变量微积分，在点 $p=\ln(2)$ 处的导数（即[微分](@entry_id:158718)）为 $H'(\ln(2)) = 2(\ln 2)^3 - \frac{1}{2}(\ln 2)^4$。另一方面，我们可以用链式法则计算。$F$ 和 $G$ 在对应点的雅可比矩阵分别为[@problem_id:1671487]：
$$
J_F(t) = \begin{pmatrix} 2t \\ -e^{-t} \end{pmatrix}, \quad J_G(x,y) = \begin{pmatrix} 2xy  x^2 \end{pmatrix}
$$
在 $p=\ln(2)$，我们有 $F(p) = ((\ln 2)^2, 1/2)$。因此，
$$
J_H(\ln 2) = J_G(F(\ln 2)) \cdot J_F(\ln 2) = \begin{pmatrix} 2(\ln 2)^2 \cdot \frac{1}{2}  ((\ln 2)^2)^2 \end{pmatrix} \begin{pmatrix} 2\ln 2 \\ -e^{-\ln 2} \end{pmatrix}
$$
$$
= \begin{pmatrix} (\ln 2)^2  (\ln 2)^4 \end{pmatrix} \begin{pmatrix} 2\ln 2 \\ -1/2 \end{pmatrix} = 2(\ln 2)^3 - \frac{1}{2}(\ln 2)^4
$$
结果与直接求导完全一致。

### [微分](@entry_id:158718)的几何解释

[微分](@entry_id:158718)的威力不仅在于计算，更在于其深刻的几何意义。[微分](@entry_id:158718)的代数性质（如秩、核、像）直接对应于[光滑映射](@entry_id:203730)的几何性质。

#### [标量场](@entry_id:151443)的[微分](@entry_id:158718)：梯度与[等值面](@entry_id:196027)

当映射的目标空间是 $\mathbb{R}$ 时，即我们有一个光滑函数 $f: M \to \mathbb{R}$，情况变得特别。其[微分](@entry_id:158718) $df_p$ 是一个从 $T_pM$ 到 $T_{f(p)}\mathbb{R} \cong \mathbb{R}$ 的[线性映射](@entry_id:185132)。换言之，$df_p$ 是一个作用于切向量并返回一个实数的[线性泛函](@entry_id:276136)，这正是**余[切向量](@entry_id:265494)**（covector）或 **1-形式**（1-form）的定义。

在[欧氏空间](@entry_id:138052) $\mathbb{R}^n$ 中，这个 [1-形式](@entry_id:270392) $df_p$ 与我们熟悉的**梯度**（gradient） $\nabla f(p)$ 密切相关。对于任意切向量 $v_p \in T_p\mathbb{R}^n$（我们可以将其等同于向量 $v \in \mathbb{R}^n$），[微分](@entry_id:158718)的作用由[点积](@entry_id:149019)给出[@problem_id:1671472]：
$$
df_p(v_p) = \nabla f(p) \cdot v
$$
这正是函数 $f$ 在 $p$ 点沿 $v$ 方向的**方向导数**。

[微分](@entry_id:158718)的**核**（kernel），$\ker(df_p) = \{v_p \in T_pM \mid df_p(v_p) = 0\}$，具有清晰的几何意义。在欧氏空间中，$\ker(df_p)$ 是所有与[梯度向量](@entry_id:141180) $\nabla f(p)$ 正交的向量组成的集合。这个[向量空间](@entry_id:151108)正是穿过 $p$ 点的 $f$ 的**[等值面](@entry_id:196027)**（level set）$S = \{q \in M \mid f(q) = f(p)\}$ 在 $p$ 点的[切空间](@entry_id:199137) $T_pS$[@problem_id:1671495]。例如，对于函数 $f(x, y, z) = x^2 y - y \sin(z)$ 和点 $p = (2, 1, \pi/2)$，我们计算梯度为 $\nabla f(p) = (4, 3, 0)$。$df_p$ 的核由所有满足 $4v_1 + 3v_2 = 0$ 的向量 $(v_1, v_2, v_3)$ 组成。这个平面由向量 $(3, -4, 0)$ 和 $(0, 0, 1)$ 张成，它就是 $f$ 在 $p$ 点的[等值面](@entry_id:196027)的[切平面](@entry_id:136914)。

#### 秩、[核与像](@entry_id:151957)

对于一般的映射 $F: M \to N$，[微分](@entry_id:158718) $dF_p$ 的**秩**（rank）是指其像空间 $\text{Im}(dF_p)$ 的维度。这个秩在几何上至关重要。

- **[浸入](@entry_id:161534) (Immersion)**：如果 $dF_p$ 在每一点 $p$ 都是[单射](@entry_id:183792)（injective），即 $\ker(dF_p) = \{0\}$，那么 $F$ 是一个[浸入](@entry_id:161534)。这意味着 $F$ 局部地不会 "折叠" 或 "压扁" [流形](@entry_id:153038)。
- **淹没 (Submersion)**：如果 $dF_p$ 在每一点 $p$ 都是满射（surjective），即 $\text{Im}(dF_p) = T_{F(p)}N$，那么 $F$ 是一个淹没。这意味着 $F$ 局部地覆盖了目标[流形](@entry_id:153038)的所有方向。上面讨论的标量函数 $f: \mathbb{R}^3 \to \mathbb{R}$ 在其梯度非零的点就是淹没。
- **[局部微分同胚](@entry_id:203529) (Local Diffeomorphism)**：如果 $dF_p$ 是一个同构（isomorphism），即它既是单射也是满射，那么 $F$ 在 $p$ 点附近是一个[局部微分同胚](@entry_id:203529)。这要求 $M$ 和 $N$ 具有相同的维度，并且 $dF_p$ 的[雅可比矩阵](@entry_id:264467)是可逆的（[行列式](@entry_id:142978)非零）。如果雅可比[矩阵的[行列](@entry_id:148198)式](@entry_id:142978)为零，那么 $dF_p$ 就不是同构，推向前的[基向量](@entry_id:199546)将不再是目标[切空间](@entry_id:199137)的基底，映射在该点是**奇异的**（singular）[@problem_id:1671526]。

[微分](@entry_id:158718)的**像**（image）$\text{Im}(dF_p)$ 描述了源[流形](@entry_id:153038)的切空间在映射下的"投影"。它张成了像集 $F(M)$ 的切空间（在 $F(M)$ 也是一个[子流形](@entry_id:159439)的良好情况下）。例如，考虑从[抛物面](@entry_id:264713) $M: z = x^2 + 2y^2$ 到 $\mathbb{R}^4$ 的映射 $F(x,y,z) = (x, y, x+y, z)$。在点 $p=(2,1,6)$，我们可以找到 $T_pM$ 的一组基，然后通过 $dF_p$ 将它们推向前，得到 $T_{F(p)}\mathbb{R}^4$ 中像空间 $\text{Im}(dF_p)$ 的一组基。计算表明，这个像空间由向量 $\{(1, 0, 1, 4), (0, 1, 1, 4)\}$ 张成[@problem_id:1671513]。

### 对偶性：[前推与拉回](@entry_id:181877)

最后，我们探讨一个展示微分几何优雅对偶性的深刻联系。我们已经看到，[微分](@entry_id:158718) $dF_p$ 将[切向量](@entry_id:265494)从 $T_pM$ **[前推](@entry_id:158718)**到 $T_{F(p)}N$。另一方面，一个[光滑映射](@entry_id:203730) $F: M \to N$ 也可以将 $N$ 上的几何对象 "[拉回](@entry_id:160816)" 到 $M$ 上。对于 1-形式（或余切向量）尤其如此。

给定 $N$ 上的一个 1-形式 $\omega$，它在每一点 $q \in N$ 都是一个作用于 $T_qN$ 中向量的线性泛函 $\omega_q$。我们可以定义 $M$ 上的一个**[拉回](@entry_id:160816) 1-形式**（pullback 1-form）$F^*\omega$，它在每一点 $p \in M$ 作用于 $T_pM$ 中的向量。其定义方式完美地利用了[前推](@entry_id:158718)：
$$
(F^*\omega)_p(v_p) = \omega_{F(p)}(dF_p(v_p))
$$
其中 $v_p \in T_pM$。这个公式的含义是：要在 $M$ 上计算[拉回](@entry_id:160816)形式 $F^*\omega$ 对向量 $v_p$ 的值，我们首先将 $v_p$ **[前推](@entry_id:158718)**到 $N$ 的[切空间](@entry_id:199137)中得到 $dF_p(v_p)$，然后用原始的 [1-形式](@entry_id:270392) $\omega$ 在像点 $F(p)$ 处对这个[前推](@entry_id:158718)的向量求值[@problem_id:1671477]。

这个关系是[微分几何](@entry_id:145818)中许多计算和理论的基石。它将向量的[协变](@entry_id:634097)行为（[前推](@entry_id:158718)）与形式的[逆变](@entry_id:192290)行为（[拉回](@entry_id:160816)）联系在一起，形成了一个和谐的整体。

总而言之，[光滑映射的微分](@entry_id:268823)是理解[流形](@entry_id:153038)之间关系的核心工具。它将复杂的[非线性](@entry_id:637147)问题局部地转化为可处理的线性代数问题。通过研究[微分](@entry_id:158718)的雅可比矩阵、基本性质以及其核、像和秩的几何意义，我们得以深入探索[浸入](@entry_id:161534)、淹没、[等值面](@entry_id:196027)以及更高级的几何结构。