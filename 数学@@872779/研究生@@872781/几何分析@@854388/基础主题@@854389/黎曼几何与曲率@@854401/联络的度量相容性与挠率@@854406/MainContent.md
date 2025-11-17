## 引言
在微分几何的宏伟蓝图中，“联络”是描绘弯曲空间中变化的核心工具，它允许我们对向量场和[张量场](@entry_id:190170)进行有意义的[微分](@entry_id:158718)。然而，一个[流形](@entry_id:153038)上可以定义无数个联络，这引出了一个根本问题：在具备度量结构的黎曼流形上，哪个联络才是“自然”或“正确”的？本文旨在解答这一问题，通过系统性地剖析联络的两个基本属性——**[度量兼容性](@entry_id:265910)**与**挠率**——来揭示它们如何成为筛选和定义几何结构的关键准则。

本文将引导读者穿越这一核心概念的三个层次。在“原理与机制”一章中，我们将建立[仿射联络](@entry_id:160152)的严格定义，深入探讨[挠率的几何意义](@entry_id:189091)和[度量兼容性](@entry_id:265910)的物理直觉，并最终见证这两大支柱如何共同构筑起[黎曼几何](@entry_id:160508)的基石——唯一的[Levi-Civita联络](@entry_id:161107)。随后的“应用与跨学科联系”一章将视野拓宽，探索当放宽无挠条件时，挠率如何在理论物理、[材料科学](@entry_id:152226)和[子流形几何](@entry_id:189265)中扮演意想不到的角色，并产生深刻的物理和几何效应。最后，通过“动手实践”环节，读者将有机会将理论付诸实践，通过具体计算来巩固对联络、挠率及其应用的理解。现在，让我们从最基本的原理与机制开始，踏上这段探索几何结构本质的旅程。

## 原理与机制

在上一章中，我们介绍了光滑流形上向量丛的基本概念。现在，我们将注意力转向[微分几何](@entry_id:145818)的核心工具之一：**联络 (connection)**。联络为我们提供了一种在[流形](@entry_id:153038)的弯曲空间中对[张量场](@entry_id:190170)（尤其是向量场）进行[微分](@entry_id:158718)的方法。本章将深入探讨联络的两个基本性质——**[度量兼容性](@entry_id:265910) (metric compatibility)** 和 **挠率 (torsion)**，并阐明它们如何共同确定了黎曼几何中独一无二的核心结构：**[Levi-Civita联络](@entry_id:161107)**。

### [仿射联络](@entry_id:160152)及其性质

一个**[仿射联络](@entry_id:160152) (affine connection)** $\nabla$ 是一个作用于切丛 $TM$ 上的算子，它将一对向量场 $(X, Y)$ 映为另一个向量场 $\nabla_X Y$，即 $X$ 方向上 $Y$ 的**[协变导数](@entry_id:152476) (covariant derivative)**。这个算子需要满足以下三个基本公理 [@problem_id:3032134]：

1.  **对第一个变量的 $C^\infty(M)$-线性**：对任意光滑函数 $f, h \in C^\infty(M)$ 和向量场 $X_1, X_2, Y \in \Gamma(TM)$，有
    $$ \nabla_{fX_1+hX_2} Y = f \nabla_{X_1} Y + h \nabla_{X_2} Y $$

2.  **对第二个变量的 $\mathbb{R}$-线性**：对任意常数 $a, b \in \mathbb{R}$ 和向量场 $X, Y_1, Y_2 \in \Gamma(TM)$，有
    $$ \nabla_X (aY_1 + bY_2) = a \nabla_X Y_1 + b \nabla_X Y_2 $$

3.  **对第二个变量的[Leibniz法则](@entry_id:157949)**：对任意光滑函数 $f \in C^\infty(M)$ 和向量场 $X, Y \in \Gamma(TM)$，有
    $$ \nabla_X (fY) = (Xf)Y + f \nabla_X Y $$
    其中 $Xf$ 表示函数 $f$ 沿向量场 $X$ 的[方向导数](@entry_id:189133)。

一个至关重要的观察是，联络在其第二个变量上不满足 $C^\infty(M)$-线性。若天真地假设它满足，我们将得到 $\nabla_X(fY) = f\nabla_X Y$，但这与[Leibniz法则](@entry_id:157949)相矛盾，除非 $Xf=0$。这一特性——通常被称为“非张量性”——是联络的本质。它意味着联络本身不是一个张量场。我们可以通过结合第一个和第三个公理来更清楚地看到这一点：
$$ \nabla_{fX}(gY) = f \nabla_X(gY) = f((Xg)Y + g\nabla_X Y) = f(Xg)Y + fg\nabla_X Y $$
这个公式 [@problem_id:3032134] 清楚地显示了导数项 $(Xg)$ 的存在，这正是联络与张量的区别所在。

为了在局部进行计算，我们在一个[局部坐标](@entry_id:181200)图 $(U, \{x^i\})$ 中引入联络的系数，即**[克里斯托费尔符号](@entry_id:159831) (Christoffel symbols)** $\Gamma^k_{ij}$，它们由联络作用于[基向量](@entry_id:199546)场 $\partial_i = \frac{\partial}{\partial x^i}$ 的方式定义：
$$ \nabla_{\partial_i} \partial_j = \Gamma^k_{ij} \partial_k $$
（此处及下文均使用爱因斯坦求和约定）。

由于联络不是张量，其分量 $\Gamma^k_{ij}$ 在坐标变换下的行为也非张量性的。考虑从[坐标系](@entry_id:156346) $\{x^i\}$ 到 $\{y^a\}$ 的变换。利用[链式法则](@entry_id:190743)和联络的公理，我们可以推导出克里斯托费尔符号的变换法则 [@problem_id:3032158]：
$$ \tilde{\Gamma}^{c}{}_{ab} = \frac{\partial y^{c}}{\partial x^{k}} \frac{\partial x^{i}}{\partial y^{a}} \frac{\partial x^{j}}{\partial y^{b}} \Gamma^{k}{}_{ij} + \frac{\partial y^{c}}{\partial x^{k}} \frac{\partial^{2} x^{k}}{\partial y^{a} \partial y^{b}} $$
这个变换法则的等式右边包含两项。第一项是标准的 $(1,2)$ 型张量的变换方式。然而，第二项，即所谓的**非齐次项 (inhomogeneous term)**，它依赖于坐标变换函数的[二阶偏导数](@entry_id:635213)。正是这一项的存在，使得 $\Gamma^k_{ij}$ 本身不构成一个[张量场](@entry_id:190170)的分量。

有趣的是，某些由[克里斯托费尔符号](@entry_id:159831)构成的量却是张量。例如，考虑两个不同的联络 $\nabla^{(1)}$ 和 $\nabla^{(2)}$，它们的差 $A(X,Y) = \nabla^{(1)}_X Y - \nabla^{(2)}_X Y$ 是一个张量。这是因为在[坐标变换](@entry_id:172727)下，两个联络的非齐次项是完全相同的，因此它们在相减时会抵消掉。这揭示了一个深刻的道理：尽管单个联络的定义依赖于[坐标系](@entry_id:156346)，但不同联络之间的“差异”是一个内在的、不依赖于坐标的几何对象 [@problem_id:3032158] [@problem_id:3032163]。我们很快会看到，挠率是这种现象的另一个重要例子。

### 挠率：度量联络的非对称性

对于普通欧氏空间中的向量，[二阶偏导数](@entry_id:635213)的求导次序可以交换，例如 $\partial_i \partial_j f = \partial_j \partial_i f$。然而，在弯曲的[流形](@entry_id:153038)上使用协变导数时，交换求导次序会产生额外的项。[挠率张量](@entry_id:204137)正是量化这种不对称性的一部分。

**[挠率张量](@entry_id:204137) (torsion tensor)** $T$ 是一个 $(1,2)$ 型张量，定义为：
$$ T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y] $$
其中 $[X,Y] = XY - YX$ 是向量场 $X$ 和 $Y$ 的**李括号 (Lie bracket)**。[李括号](@entry_id:636461)本身描述了沿着 $X$ 和 $Y$ 的无穷小流动的不可交换性。因此，挠率衡量了协变导数的不[可交换性](@entry_id:263314) $(\nabla_X Y - \nabla_Y X)$ 与向量场本身的几何不[可交换性](@entry_id:263314) $([X,Y])$ 之间的差异。

为了更具体地理解挠率，我们考察它在[局部坐标系](@entry_id:751394)中的表达式。在[坐标基](@entry_id:270149)底下，我们有 $[\partial_i, \partial_j] = 0$。因此，挠率的定义简化为 [@problem_id:3032135]：
$$ T(\partial_i, \partial_j) = \nabla_{\partial_i} \partial_j - \nabla_{\partial_j} \partial_i = \Gamma^k_{ij} \partial_k - \Gamma^k_{ji} \partial_k = (\Gamma^k_{ij} - \Gamma^k_{ji}) \partial_k $$
由此，我们得到[挠率张量](@entry_id:204137)的分量表达式：
$$ T^k_{ij} = \Gamma^k_{ij} - \Gamma^k_{ji} $$
这个简洁的公式表明，挠率恰好是[克里斯托费尔符号](@entry_id:159831)在下指标上的反对称部分。如果一个联络的[克里斯托费尔符号](@entry_id:159831)在任意[坐标系](@entry_id:156346)下都满足 $\Gamma^k_{ij} = \Gamma^k_{ji}$，我们就称这个联络是**[无挠的](@entry_id:161664) (torsion-free)** 或**对称的 (symmetric)** [@problem_id:3032134] [@problem_id:3032137]。

值得注意的是，正如我们之前所暗示的，挠率 $T$ 是一个真正的张量。我们可以通过考察其分量 $T^k_{ij}$ 的变换法则来验证这一点。由于克里斯托费尔符号变换法则中的非齐次项 $\frac{\partial y^{c}}{\partial x^{k}} \frac{\partial^{2} x^{k}}{\partial y^{a} \partial y^{b}}$ 在其下指标 $a,b$ 上是对称的，当我们计算 $T$ 的分量 $\tilde{T}^c_{ab} = \tilde{\Gamma}^c_{ab} - \tilde{\Gamma}^c_{ba}$ 时，这个非齐次项会相互抵消。剩下的部分则严格按照 $(1,2)$ 型张量的方式变换。这再次印证了一个重要原理：通过对[非张量对象](@entry_id:201374)（如 $\Gamma^k_{ij}$）进行适当的组合（如此处的反对称化），可以构造出内在的几何对象（张量） [@problem_id:3032158]。

在更一般的**[活动标架](@entry_id:175562) (moving frame)** $\{e_i\}$（不一定是坐标标架）中，李括号 $[e_i, e_j]$ 通常不为零，而是由所谓的**[结构函数](@entry_id:161908) (structure functions)** $c^k_{ij}$ 描述：$[e_i, e_j] = c^k_{ij} e_k$。在这种情况下，挠率分量的表达式需要包含[李括号](@entry_id:636461)的贡献 [@problem_id:3032137]：
$$ T^k_{ij} = \Gamma^k_{ij} - \Gamma^k_{ji} - c^k_{ij} $$

### [度量兼容性](@entry_id:265910)：保持几何结构

到目前为止，我们的讨论完全是关于[仿射联络](@entry_id:160152)的，它可以在任何[光滑流形](@entry_id:160799)上定义，而无需额外的结构。然而，在黎曼几何中，我们处理的是**[黎曼流形](@entry_id:261160) (Riemannian manifold)** $(M, g)$，它额外配备了一个**[黎曼度量](@entry_id:754359) (Riemannian metric)** $g$。度量 $g$ 为每个[切空间](@entry_id:199137) $T_p M$ 定义了一个[内积](@entry_id:158127)，从而允许我们测量向量的长度和向量间的夹角。

一个自然的问题是：联络与度量之间应该有怎样的关系？一个理想的[协变导数](@entry_id:152476)应该“尊重”[流形](@entry_id:153038)的度量结构。这意味着当我们沿着一个向量场平行移动两个向量时，它们之间的[内积](@entry_id:158127)应该保持不变。这个直观的想法被精确地表述为**[度量兼容性](@entry_id:265910) (metric compatibility)**。

我们说一个联络 $\nabla$ 与度量 $g$ **兼容**，如果度量 $g$ 的[协变导数](@entry_id:152476)为零，即 $\nabla g = 0$。根据[协变导数](@entry_id:152476)作用于 $(0,2)$ 型张量的法则，这等价于对任意向量场 $X, Y, Z$，下式恒成立 [@problem_id:3032134]：
$$ (\nabla_X g)(Y,Z) = X(g(Y,Z)) - g(\nabla_X Y, Z) - g(Y, \nabla_X Z) = 0 $$
移项后，我们得到一个更常用的形式，它类似于微积分中的[乘法法则](@entry_id:144424)：
$$ X(g(Y,Z)) = g(\nabla_X Y, Z) + g(Y, \nabla_X Z) $$
这个方程的含义是，两个向量场[内积](@entry_id:158127)的导数，等于它们各自协变导数与另一向量场内积之和。

必须强调，**挠率**和**[度量兼容性](@entry_id:265910)**是两个完全独立的概念。一个联络可以是度量兼容但有挠的，也可以是无挠但非度量兼容的 [@problem_id:3032137]。这两种性质的结合，将引出[黎曼几何](@entry_id:160508)中最为特殊和重要的联络。

### Riemann几何基本定理：[Levi-Civita联络](@entry_id:161107)

现在我们来到了[黎曼几何](@entry_id:160508)的中心支柱——**Riemann几何基本定理 (The Fundamental Theorem of Riemannian Geometry)**。该定理断言：

> 在任意一个黎曼流形 $(M, g)$ 上，存在**唯一一个**[仿射联络](@entry_id:160152) $\nabla$，它同时满足以下两个条件：
> 1.  **无挠性 (Torsion-free)**: $T \equiv 0$.
> 2.  **[度量兼容性](@entry_id:265910) (Metric-compatible)**: $\nabla g = 0$.

这个独一无二的联络被称为**Levi-Civita联络** (或黎曼联络)。

这个定理的强大之处在于它的**唯一性 (uniqueness)** 和 **存在性 (existence)**。让我们分别探讨其背后的原理。

**唯一性**

为什么满足这两个条件的联络是唯一的？我们可以通过一个优雅的论证来证明 [@problem_id:3032163]。假设 $\nabla$ 和 $\tilde{\nabla}$ 是两个都满足无挠和[度量兼容条件](@entry_id:201846)的联络。定义它们的差为一个 $(1,2)$ 型张量 $A$，即 $A_X Y = \tilde{\nabla}_X Y - \nabla_X Y$。

-   因为两个联络都是**度量兼容**的，我们有：
    $g(A_X Y, Z) + g(Y, A_X Z) = 0$。
    这意味着对任意固定的 $X$，线性映射 $Y \mapsto A_X Y$ 是关于度量 $g$ 的**反对称 (skew-adjoint)** 算子。用分量来说，这意味着张量 $C(X,Y,Z) = g(A_X Y, Z)$ 在后两个变量 $Y, Z$ 上是反对称的。

-   因为两个联络都是**无挠**的，我们有：
    $T^{\tilde{\nabla}}(X,Y) - T^{\nabla}(X,Y) = A_X Y - A_Y X = 0$。
    这意味着张量 $A$ 在其下面两个变量 $X, Y$ 上是**对称的**。因此，$C(X,Y,Z)$ 在前两个变量 $X, Y$ 上也是对称的。

现在我们来综合这两个对称性。一个在 $X, Y$ 上对称，而在 $Y, Z$ 上反对称的张量 $C(X,Y,Z)$ 必然为零。具体来说：
$$ C(X,Y,Z) = C(Y,X,Z) = -C(Y,Z,X) = -C(Z,Y,X) = C(Z,X,Y) = C(X,Z,Y) = -C(X,Y,Z) $$
这导致 $2 C(X,Y,Z) = 0$，因此 $C \equiv 0$。由于度量 $g$ 是非退化的，从 $g(A_X Y, Z) = 0$ 对所有 $Z$ 成立，可以推出 $A_X Y = 0$ 对所有 $X, Y$ 成立。这意味着 $A \equiv 0$，即 $\tilde{\nabla} = \nabla$。唯一性得证。

**存在性与构造**

为了证明存在性并给出一个具体构造，我们利用**[Koszul公式](@entry_id:181356)** [@problem_id:2973008] [@problem_id:3032131]。这个推导过程巧妙地展示了两个条件是如何“恰到好处”地确定联络的。我们从[度量兼容性](@entry_id:265910)条件出发，写下它的三个[循环排列](@entry_id:273014)：
1.  $X(g(Y,Z)) = g(\nabla_X Y, Z) + g(Y, \nabla_X Z)$
2.  $Y(g(Z,X)) = g(\nabla_Y Z, X) + g(Z, \nabla_Y X)$
3.  $Z(g(X,Y)) = g(\nabla_Z X, Y) + g(X, \nabla_Z Y)$

然后，我们计算 $(1) + (2) - (3)$，并利用度量 $g$ 的对称性以及无挠条件 $\nabla_X Y - \nabla_Y X = [X,Y]$ 来重新组合右边的项。经过一番代数运算，最终可以解出 $g(\nabla_X Y, Z)$：
$$ 2g(\nabla_X Y, Z) = X(g(Y,Z)) + Y(g(Z,X)) - Z(g(X,Y)) + g([X,Y], Z) - g([Y,Z], X) + g([Z,X], Y) $$
这就是著名的**[Koszul公式](@entry_id:181356)**。它的右边只涉及度量 $g$、其导数以及[向量场的李括号](@entry_id:193400)，完全不依赖于联络 $\nabla$。这意味着 $g(\nabla_X Y, Z)$ 的值被唯一确定了。又因为 $g$ 是非退化的，一个向量完全由它与所有其他向量的[内积](@entry_id:158127)所确定。因此，$\nabla_X Y$ 这个向量也被唯一确定。

将[Koszul公式](@entry_id:181356)应用到[局部坐标系](@entry_id:751394)中，其中 $[\partial_i, \partial_j] = 0$，我们可以解出[克里斯托费尔符号](@entry_id:159831)的显式表达式 [@problem_id:3032131]：
$$ \Gamma^k_{ij} = \frac{1}{2} g^{kl} \left( \partial_i g_{jl} + \partial_j g_{il} - \partial_l g_{ij} \right) $$
这个公式是[黎曼几何](@entry_id:160508)中进行具体计算的基石。它表明，只要我们知道了度量张量在一个[坐标系](@entry_id:156346)下的分量，我们就可以完全确定[Levi-Civita联络](@entry_id:161107)。由于这个构造过程是基于内在的几何条件（无挠和度量兼容），它所定义的联络是**自然的 (natural)**，即它与[流形](@entry_id:153038)的[微分同胚](@entry_id:147249)是相容的。

### 超越Levi-Civita：联络的广阔天地

尽管[Levi-Civita联络](@entry_id:161107)在[黎曼几何](@entry_id:160508)中占据中心地位，但理解其他类型的联络同样重要。这不仅能加深我们对Levi-Civita联络为何特殊的理解，也因为这些联络在物理学（如广义相对论的某些替代理论）和数学的其他分支中扮演着重要角色。

我们可以通过放宽Levi-Civita联络的两个定义条件之一来探索更广阔的联络世界 [@problem_id:3032163]：

1.  **度量兼容但有挠的联络**：存在无穷多个这样的联络。给定一个[Levi-Civita联络](@entry_id:161107) $\nabla^{LC}$，我们可以通过加上一个特定的张量（称为**挠差张量 (contorsion tensor)**）来构造一个新的、度量兼容但有挠的联络。例如，对任意一个 $(1,2)$ 型张量 $A_X Y$ 使得 $Y \mapsto A_X Y$ 是 $g$-反对称的，联络 $\tilde{\nabla}_X Y = \nabla^{LC}_X Y + A_X Y$ 仍然是度量兼容的，但其挠率通常不为零。

2.  **无挠但非度量兼容的联络**：同样，也存在无穷多个这样的联络。我们可以构造一个对称的张量 $A_X Y = A_Y X$ 使得 $\tilde{\nabla}_X Y = \nabla^{LC}_X Y + A_X Y$ 是[无挠的](@entry_id:161664)，但它通常不再与度量 $g$ 兼容。

**案例研究 1：Weitzenböck联络**

一个极具启发性的例子是**Weitzenböck联络** [@problem_id:3032139]。它是一种**平坦 (flat)**（即曲率为零）且度量兼容，但具有非零挠率的联络。

考虑一个黎曼流形 $(M,g)$，并假设我们能在上面找到一个**全局正交[标架场](@entry_id:160577) (global orthonormal frame field)** $\{e_a\}$。Weitzenböck联络 $\nabla^W$ 被定义为使得这个[标架场](@entry_id:160577)处处平行的联络，即：
$$ \nabla^W_X e_a = 0 \quad \text{对所有 } a \text{ 和任意向量场 } X $$
从这个定义出发，我们可以立即推断出它的几个关键性质：
-   **[度量兼容性](@entry_id:265910)**：因为 $g(e_a, e_b) = \delta_{ab}$ 是常数，且 $\nabla^W e_a = 0$，那么 $X(g(e_a, e_b)) = 0$ 和 $g(\nabla^W_X e_a, e_b) + g(e_a, \nabla^W_X e_b) = 0+0=0$ 总是成立。因此 $\nabla^W$ 是度量兼容的。
-   **平坦性（零曲率）**：[曲率张量](@entry_id:181383) $R(X,Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]} Z$ 在[基向量](@entry_id:199546) $e_a, e_b, e_c$ 上计算时，由于 $\nabla^W e_c = 0$，所有项都将变为零。因此该联络是平坦的。
-   **非零挠率**：它的挠率 $T(X,Y) = \nabla^W_X Y - \nabla^W_Y X - [X,Y] = -[X,Y]$。只要[标架场](@entry_id:160577) $\{e_a\}$ 不是坐标[标架场](@entry_id:160577)（即[李括号](@entry_id:636461) $[e_a, e_b]$ 不全为零），这个联络就具有非零挠率。

例如，在 $\mathbb{R}^3$ 中，我们可以构造一个依赖于位置的旋转[标架场](@entry_id:160577)。通过计算可以发现，其Weitzenböck[联络的挠率](@entry_id:192913)分量不为零，这具体地展示了一个平坦、度量兼容但有挠的联络的存在。这个例子完美地说明了挠率、曲率和[度量兼容性](@entry_id:265910)是三个[相互独立](@entry_id:273670)的概念。

**案例研究 2：一个联络何时是[Levi-Civita联络](@entry_id:161107)？**

反过来，给定一个[仿射联络](@entry_id:160152) $\nabla$，我们如何判断它是否是**某个**黎曼度量 $g$ 的[Levi-Civita联络](@entry_id:161107)？[@problem_id:2999509]

首先，这个联络必须是[无挠的](@entry_id:161664)，否则它不可能是任何度量的Levi-Civita联络。如果 $\nabla$ 是[无挠的](@entry_id:161664)，那么问题就转化为：是否存在一个[黎曼度量](@entry_id:754359) $g$ 使得 $\nabla$ 与 $g$ 兼容？

我们可以利用[Koszul公式](@entry_id:181356)来回答这个问题。如果存在这样的 $g$，那么它的分量 $g_{ij}$ 必须满足由[Koszul公式](@entry_id:181356)导出的一个一阶[线性偏微分方程](@entry_id:172517)组。例如，在[坐标基](@entry_id:270149)底下，[Koszul公式](@entry_id:181356) $2 g(\nabla_{\partial_i} \partial_j, \partial_k) = \partial_i(g_{jk}) + \partial_j(g_{ik}) - \partial_k(g_{ij})$ 必须成立。将给定的联络的[克里斯托费尔符号](@entry_id:159831) $\Gamma^l_{ij}$ 代入左边，我们就得到一个关于未知函数 $g_{ij}$ 的[方程组](@entry_id:193238)。

这个[方程组](@entry_id:193238)可能没有解，或者其解不满足黎曼度量所需的正定性条件。例如，在 $\mathbb{R}^2$ 上考虑由 $\nabla_{\partial_x}\partial_y = \partial_x$ 等定义的[无挠联络](@entry_id:181337)，通过求解这个PDE系统，我们会发现任何可能的解都要求度量分量 $g_{xx}=0$，这与度量必须是正定的相矛盾。因此，这个联络不可能是任何[黎曼度量](@entry_id:754359)的[Levi-Civita联络](@entry_id:161107)。这个例子深刻地揭示了[度量兼容性](@entry_id:265910)是一个非常强的约束条件。

### [活动标架法](@entry_id:175562)：Cartan的视角

最后，我们简要介绍一种处理联络、挠率和曲率的强大而优雅的 formalism，即**[活动标架法](@entry_id:175562) (method of moving frames)**，也称为Cartan方法 [@problem_id:3032140]。这种方法使用[微分形式](@entry_id:146747)来表达几何概念，常常能简化计算并揭示更深刻的结构。

在一个局部正交[标架场](@entry_id:160577) $\{e_i\}$ 及其对偶[余标架场](@entry_id:183575) $\{\theta^i\}$ 中，几何信息被编码在以下对象中：
-   **[联络1-形式](@entry_id:275839) (connection 1-forms)** $\omega^i{}_j$，定义为 $\nabla e_j = \omega^i{}_j \otimes e_i$。
-   **挠率[2-形式](@entry_id:188008) (torsion 2-forms)** $T^i$。
-   **[曲率2-形式](@entry_id:187677) (curvature 2-forms)** $\Omega^i{}_j$。

这些对象由两组基本的**[Cartan结构方程](@entry_id:262185)**联系在一起：
1.  **第一[结构方程](@entry_id:274644)**： $d\theta^i + \omega^i{}_j \wedge \theta^j = T^i$
2.  **第二[结构方程](@entry_id:274644)**： $d\omega^i{}_j + \omega^i{}_k \wedge \omega^k{}_j = \Omega^i{}_j$

在这个 formalism 中，Levi-Civita联络的两个定义条件可以被简洁地翻译成代数约束：
-   **[度量兼容性](@entry_id:265910)** $\iff$ [联络1-形式](@entry_id:275839)矩阵是反对称的：$\omega_{ij} + \omega_{ji} = 0$，其中 $\omega_{ij} = \delta_{ik}\omega^k{}_j$。
-   **无挠性** $\iff$ 挠率[2-形式](@entry_id:188008)为零：$T^i=0$，这使得第一[结构方程](@entry_id:274644)变为 $d\theta^i = -\omega^i{}_j \wedge \theta^j$。

此外，这个 formalism 还优雅地编码了**Bianchi恒等式 (Bianchi identities)**，它们是挠率和曲率必须满足的[微分](@entry_id:158718)约束。例如，第一[Bianchi恒等式](@entry_id:261685)可写作 $dT^i + \omega^i{}_j \wedge T^j = \Omega^i{}_j \wedge \theta^j$。

最后，[活动标架](@entry_id:175562)下的[Koszul公式](@entry_id:181356)给出了Levi-Civita联络的系数 $\Gamma_{ijk}$ (定义自 $\omega_i{}^j = \Gamma_{ik}{}^j \theta^k$) 与[标架场](@entry_id:160577)的[结构函数](@entry_id:161908) $c_{ijk}$ (定义自 $d\theta^i = -\frac{1}{2}c^i{}_{jk}\theta^j \wedge \theta^k$) 之间的直接关系：
$$ \Gamma_{ijk} = \frac{1}{2}(c_{kij} - c_{ijk} - c_{jki}) $$
这为在非坐标标架下进行高效计算提供了强有力的工具。

本章我们详细剖析了[仿射联络](@entry_id:160152)的两个基本属性——挠率和[度量兼容性](@entry_id:265910)。我们看到，这两个看似简单的条件如何结合在一起，以惊人的方式确定了黎曼流形上唯一的、内在的[微分](@entry_id:158718)结构——[Levi-Civita联络](@entry_id:161107)。同时，通过探索不满足这些条件的联络，我们得以一窥更广阔的几何世界，并更深刻地理解了[Levi-Civita联络](@entry_id:161107)的特殊地位。在下一章中，我们将利用Levi-Civita联络来定义和研究曲率——衡量空间弯曲程度的根本概念。