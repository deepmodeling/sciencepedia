## 引言
在探索[光滑流形](@entry_id:160799)的几何学时，我们面临一个根本性问题：如何在没有[全局坐标系](@entry_id:171029)的弯曲空间中对向量场进行[微分](@entry_id:158718)？[欧氏空间](@entry_id:138052)中的朴素求导方法不再适用，因为不同点的切空间无法直接比较。为了解决这一难题，[微分几何](@entry_id:145818)引入了“[仿射联络](@entry_id:160152)”这一关键结构，它提供了一种系统性地“连接”相邻[切空间](@entry_id:199137)并定义有效导数（协变导数）的方法。然而，这种新引入的[微分](@entry_id:158718)结构自身也带来了描述空间内在几何的全新工具。

本文旨在深入剖析[仿射联络](@entry_id:160152)及其产生的两个最基本的[几何不变量](@entry_id:178611)：[挠率张量](@entry_id:204137)和[曲率张量](@entry_id:181383)。我们将通过三个循序渐进的章节来构建对这些概念的全面理解。首先，在 **“原理与机制”** 部分，我们将从公理化定义出发，建立协变导数、挠率和曲率的代数框架，并通过[Christoffel符号](@entry_id:159831)给出其坐标表示。接着，在 **“应用与跨学科联系”** 部分，我们将展示这些抽象的理论如何在具体问题中发挥作用，探讨它们如何定义[测地线](@entry_id:269969)、量化[曲面](@entry_id:267450)弯曲，以及它们在广义相对论和李群理论等前沿物理与数学领域中的深刻联系。最后，**“动手实践”** 部分将提供一系列精心设计的问题，让你有机会亲手计算和应用这些概念，将理论知识转化为解决问题的能力。

## 原理与机制

在引入了光滑流形与向量场的基本概念之后，我们现在转向[微分几何](@entry_id:145818)的核心议题：如何在弯曲空间上对向量场进行[微分](@entry_id:158718)。在欧氏空间中，我们可以简单地通过对向量分量求偏导数来定义方向导数，因为我们有一个全局一致的[坐标系](@entry_id:156346)。然而，在一般的[流形](@entry_id:153038)上，不同点的切空间是不同的，直接比较两个不同点上的向量是没有意义的。为了克服这一困难，我们需要引入一个额外的结构，即 **[仿射联络](@entry_id:160152) (affine connection)**，它为我们提供了一种“连接”相邻切空间并定义[协变导数](@entry_id:152476)的方法。本章将系统地阐述[仿射联络](@entry_id:160152)的原理，并深入探讨由它衍生的两个基本[几何不变量](@entry_id:178611)：**挠率 (torsion)** 和 **曲率 (curvature)**。

### [仿射联络](@entry_id:160152)：向量场的[微分](@entry_id:158718)

#### 联络的公理化定义

一个[光滑流形](@entry_id:160799) $M$ 上的 **[仿射联络](@entry_id:160152)** $\nabla$ 是一个映射，它取两个向量场 $X, Y \in \mathfrak{X}(M)$，生成一个新的向量场 $\nabla_X Y$，我们称之为 $Y$ 沿 $X$ 的 **协变导数 (covariant derivative)**。这个映射必须满足以下公理 [@problem_id:3077149]：

1.  **第一变元的 $C^\infty(M)$-线性**：对于任意光滑函数 $f, g \in C^\infty(M)$ 和向量场 $X_1, X_2, Y \in \mathfrak{X}(M)$，有
    $\nabla_{fX_1 + gX_2} Y = f \nabla_{X_1} Y + g \nabla_{X_2} Y$。
    这意味着在某一点 $p \in M$，[协变导数](@entry_id:152476) $\nabla_X Y$ 的值仅依赖于 $X$ 在该点的值 $X_p \in T_p M$。

2.  **第二变元的 $\mathbb{R}$-线性**：对于任意实数 $a, b \in \mathbb{R}$ 和向量场 $X, Y_1, Y_2 \in \mathfrak{X}(M)$，有
    $\nabla_X (aY_1 + bY_2) = a \nabla_X Y_1 + b \nabla_X Y_2$。

3.  **第二变元的 Leibniz 法则 (Leibniz rule)**：对于任意光滑函数 $f \in C^\infty(M)$ 和向量场 $X, Y \in \mathfrak{X}(M)$，有
    $\nabla_X (fY) = (X(f))Y + f \nabla_X Y$。
    其中 $X(f)$ 是函数 $f$ 沿向量场 $X$ 的方向导数。

这些公理共同刻画了[协变导数](@entry_id:152476)作为一个微分算子的本质。第一条公理说明它是一个“局部”操作，依赖于[微分](@entry_id:158718)的方向。第三条 Leibniz 法则至关重要，它表明 $\nabla_X$ 的作用方式类似于一个导数，它正确地处理了向量场与[光滑函数](@entry_id:267124)的乘积。

#### 联络不是张量

一个自然的问题是：联络 $\nabla$ 本身是否是一个张量？一个映射要成为张量，它必须在其所有变元上都是 $C^\infty(M)$-线性的。我们来检验一下 $\nabla$ 在其第二个变元上的表现 [@problem_id:3077149]。根据 Leibniz 法则：
$$ \nabla_X (fY) = (X(f))Y + f \nabla_X Y $$
如果 $\nabla$ 在第二个变元上是 $C^\infty(M)$-线性的，那么我们应该有 $\nabla_X (fY) = f \nabla_X Y$。显然，由于 $(X(f))Y$ 这一项的存在，这个条件通常不成立。这一项不是“乘法性的”，而是一个“[微分](@entry_id:158718)性的”项。正是这个 Leibniz 法则使得联络 $\nabla$ 成为一个[微分算子](@entry_id:140145)，而不是一个 $(1,2)$-张量场。它捕捉了向量场 $Y$ 在 $X$ 方向上的变化率，这需要考虑 $Y$ 的分量函数及其导数，因此其值不仅取决于 $Y$ 在一点的值，还取决于 $Y$ 在该点邻域内的行为。

#### 标量函数的协变导数

我们可以将[协变导数](@entry_id:152476)的概念从向量场推广到任意类型的张量场，包括 $(0,0)$-张量，即[光滑函数](@entry_id:267124)（标量）。那么，对于一个函数 $f \in C^\infty(M)$，其[协变导数](@entry_id:152476) $\nabla_X f$ 应该是什么？

这个问题的答案并非一个约定，而是由联络公理的[自洽性](@entry_id:160889)唯一确定的 [@problem_id:3077161]。我们将协变导数 $\nabla_X$ 视为作用于整个[张量代数](@entry_id:161671)的导子，它对于[张量积](@entry_id:140694)满足 Leibniz 法则。考虑将这个法则应用于一个 $(0,1)$-张量和一个 $(1,0)$-张量（即向量场）的缩并，或者更直接地，我们可以利用向量场的 Leibniz 法则来推导。

我们要求作用于任何张量 $T$ 的标量乘法 $fT$ 满足一般性的 Leibniz 法则：
$$ \nabla_X(fT) = (\nabla_X f)T + f(\nabla_X T) $$
现在，我们将这个一般法则应用于一个向量场 $Y$（即 $T=Y$）：
$$ \nabla_X(fY) = (\nabla_X f)Y + f(\nabla_X Y) $$
将此结果与联络的第三条公理 $\nabla_X(fY) = (X(f))Y + f\nabla_X Y$ 进行比较，我们得到：
$$ (\nabla_X f)Y + f(\nabla_X Y) = (X(f))Y + f\nabla_X Y $$
消去 $f\nabla_X Y$ 项后，我们有：
$$ (\nabla_X f)Y = (X(f))Y $$
由于这个等式对任意向量场 $Y$ 都必须成立，这意味着两个标量系数必须相等：
$$ \nabla_X f = X(f) $$
因此，对于任何[仿射联络](@entry_id:160152)，其在标量函数上的作用必然等同于标准的沿向量场的方向导数。这个结果与[联络的挠率](@entry_id:192913)或曲率无关。

#### 联络的坐标表示：Christoffel 符号

为了进行具体计算，我们需要在局部坐标系中表示联络。设 $(x^1, \dots, x^n)$ 是[流形](@entry_id:153038) $M$ 上的一个局部坐标系，其对应的[坐标基](@entry_id:270149)向量场为 $\partial_i = \frac{\partial}{\partial x^i}$。由于 $\nabla_{\partial_i} \partial_j$ 的结果仍然是一个向量场，它可以表示为[基向量](@entry_id:199546)场的线性组合：
$$ \nabla_{\partial_i} \partial_j = \Gamma^k_{ij} \partial_k $$
这里的系数 $\Gamma^k_{ij}$ 是一组 $n^3$ 个光滑函数，被称为联络的 **Christoffel 符号 (Christoffel symbols)**。它们完全确定了联络在坐标域中的行为。

利用联络的公理，我们可以推导出任意两个向量场 $X = X^i \partial_i$ 和 $Y = Y^j \partial_j$ 的协变导数的一般表达式 [@problem_id:3077190]：
$$
\begin{align*}
\nabla_X Y  = \nabla_{X^i \partial_i} (Y^j \partial_j) \\
 = X^i \nabla_{\partial_i} (Y^j \partial_j)   \text{(第一变元的线性)} \\
 = X^i \left( (\partial_i Y^j) \partial_j + Y^j \nabla_{\partial_i} \partial_j \right)   \text{(Leibniz 法则)} \\
 = X^i (\partial_i Y^j) \partial_j + X^i Y^j (\Gamma^k_{ij} \partial_k)   \text{(代入 Christoffel 符号)}
\end{align*}
$$
为了合并同类项，我们对第二个项中的[哑指标](@entry_id:188070) $k$ 重命名为 $j$，或者对第一个项中的 $j$ 重命名为 $k$。采用后者，我们得到：
$$ \nabla_X Y = X^i (\partial_i Y^k) \partial_k + X^i Y^j \Gamma^k_{ij} \partial_k = \left( X^i \frac{\partial Y^k}{\partial x^i} + X^i Y^j \Gamma^k_{ij} \right) \partial_k $$
这个公式至关重要。它表明，协变导数的分量 $(\nabla_X Y)^k$ 由两部分组成：一部分是欧氏空间中的普通方向导数 $X^i \partial_i Y^k$，另一部分是修正项 $X^i Y^j \Gamma^k_{ij}$，它恰好弥补了[基向量](@entry_id:199546)场 $\partial_j$ 自身在空间中可能发生的变化。

### [挠率张量](@entry_id:204137)：扭曲的度量

#### 挠率的定义与张量性

对于任意两个向量场 $X, Y$，它们的 **[Lie 括号](@entry_id:636461) (Lie bracket)** $[X,Y] = XY - YX$ 衡量了沿着这两个向量场的无穷小流动顺序的不可交换性。一个自然的问题是，协变导数算子 $\nabla_X$ 和 $\nabla_Y$ 的对称性与 [Lie 括号](@entry_id:636461)有何关系？这引出了[挠率张量](@entry_id:204137)的定义：
$$ T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y] $$
**挠率 (torsion)** 衡量了联络的反对称部分与 [Lie 括号](@entry_id:636461)之间的差异。如果一个联络是 **[无挠的](@entry_id:161664) (torsion-free)** 或 **对称的 (symmetric)**，则意味着 $T(X,Y) = 0$，即 $\nabla_X Y - \nabla_Y X = [X,Y]$。

与联络本身不同，挠率是一个真正的张量。我们可以通过检验其对[光滑函数](@entry_id:267124)乘法的行为来证明这一点 [@problem_id:3077149]。例如，对于第一个变元：
$$
\begin{align*}
T(fX, Y)  = \nabla_{fX} Y - \nabla_Y (fX) - [fX, Y] \\
 = f \nabla_X Y - \left( (Yf)X + f \nabla_Y X \right) - \left( f[X,Y] - (Yf)X \right) \\
 = f \nabla_X Y - (Yf)X - f \nabla_Y X - f[X,Y] + (Yf)X \\
 = f (\nabla_X Y - \nabla_Y X - [X,Y]) \\
 = f T(X,Y)
\end{align*}
$$
对第二个变元的 $C^\infty(M)$-线性也可以用类似的方式证明。因此，$T$ 是一个 $(1,2)$-型[张量场](@entry_id:190170)。

在[局部坐标](@entry_id:181200)中，由于[基向量](@entry_id:199546)场的 [Lie 括号](@entry_id:636461)为零 ($[\partial_i, \partial_j] = 0$)，挠率的计算变得非常简单 [@problem_id:3077190]：
$$ T(\partial_i, \partial_j) = \nabla_{\partial_i} \partial_j - \nabla_{\partial_j} \partial_i - 0 = \Gamma^k_{ij}\partial_k - \Gamma^k_{ji}\partial_k = (\Gamma^k_{ij} - \Gamma^k_{ji})\partial_k $$
所以，[挠率张量](@entry_id:204137)的分量就是 Christoffel 符号下两个指标的反对称部分：
$$ T^k_{ij} = \Gamma^k_{ij} - \Gamma^k_{ji} $$
这立即表明，一个联络是[无挠的](@entry_id:161664)，当且仅当其 Christoffel 符号对于下两个指标是对称的，即 $\Gamma^k_{ij} = \Gamma^k_{ji}$。

#### [挠率的几何意义](@entry_id:189091)：无穷小平行四边形的不闭合性

挠率具有深刻的几何意义。它精确地描述了由[测地线](@entry_id:269969)构成的无穷小“平行四边形”无法闭合的程度 [@problem_id:3077150]。考虑如下构造：从点 $p$ 出发，沿初速度为 $X_p$ 的[测地线](@entry_id:269969)走无穷小时间 $\epsilon$ 到达 $p_1$；然后将向量 $Y_p$ 平行移动到 $p_1$ 得到 $\tilde{Y}$，再沿初速度为 $\tilde{Y}$ 的[测地线](@entry_id:269969)走时间 $\eta$ 到达 $q_{12}$。另一条路径是先沿 $Y_p$ 走时间 $\eta$ 到 $p_2$，再将 $X_p$ 平行移动到 $p_2$ 得到 $\tilde{X}$，最后沿 $\tilde{X}$ 走时间 $\epsilon$ 到达 $q_{21}$。

在平坦的[欧氏空间](@entry_id:138052)中，我们期望 $q_{12}$ 和 $q_{21}$ 是同一点。但在有挠率的弯曲空间中，这两点通常会有一个微小的位移。通过在 $p$ 点的局部坐标系中进行[泰勒展开](@entry_id:145057)可以证明，从 $q_{21}$ 指向 $q_{12}$ 的位移向量 $\vec{v}$ 在最低阶上为：
$$ \vec{v} \approx -\frac{1}{2} \epsilon \eta \, T_p(X,Y) $$
(注意：具体的数值因子可能因“平行四边形”的定义而异，但其与 $T_p(X,Y)$ 的正比关系是本质的)。这个结果表明，**挠率是[测地线](@entry_id:269969)网格扭曲的度量**。如果联络无挠，则这种无穷小平行四边形在[一阶近似](@entry_id:147559)下是闭合的。这个“扭曲”或“缠绕”的直观图像，正是“挠率”一词的来源。

#### [自平行曲线](@entry_id:269969)与挠率

与联络密切相关的概念是 **[自平行曲线](@entry_id:269969) (autoparallel curve)**，它是一条其[切向量](@entry_id:265494)场沿自身方向的协变导数为零的曲线 $\gamma(t)$：
$$ \nabla_{\dot{\gamma}} \dot{\gamma} = 0 $$
在[局部坐标](@entry_id:181200)中，设 $\gamma(t)$ 的坐标为 $x^i(t)$，其切向量为 $\dot{\gamma} = \frac{dx^i}{dt}\partial_i$。自平行方程展开为：
$$ \frac{d^2 x^k}{dt^2} + \Gamma^k_{ij} \frac{dx^i}{dt} \frac{dx^j}{dt} = 0 $$
观察这个方程，我们发现 Christoffel 符号 $\Gamma^k_{ij}$ 是与一个对称项 $\dot{x}^i \dot{x}^j$ 相乘的。因此，只有 $\Gamma^k_{ij}$ 的对称部分 $\Gamma^k_{(ij)} = \frac{1}{2}(\Gamma^k_{ij} + \Gamma^k_{ji})$ 对这个方程有贡献。而其反对称部分，即挠率 $T^k_{ij} = \Gamma^k_{ij} - \Gamma^k_{ji}$，则完全不影响[自平行曲线](@entry_id:269969)的形状 [@problem_id:3077183]。

这意味着，两个不同的联络，只要它们的 Christoffel 符号的对称部分相同，它们就会定义完全相同的[自平行曲线](@entry_id:269969)族。因此，给一个联络加上任意的挠率部分，并不会改变其[自平行曲线](@entry_id:269969)。

### [曲率张量](@entry_id:181383)：弯曲的度量

#### 曲率的代数定义：[二阶协变导数](@entry_id:193368)的不[可交换性](@entry_id:263314)

在欧氏空间中，[二阶偏导数](@entry_id:635213)的求导次序可以交换，例如 $\frac{\partial^2 f}{\partial x \partial y} = \frac{\partial^2 f}{\partial y \partial x}$。在[流形](@entry_id:153038)上，我们自然会问：[二阶协变导数](@entry_id:193368)是否也可以交换顺序？即 $\nabla_X \nabla_Y Z$ 是否等于 $\nabla_Y \nabla_X Z$？

答案是否定的，而它们之间的差异正是曲率的核心。直接计算它们的差 $[\nabla_X, \nabla_Y]Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z$ 会发现，这个表达式并不是一个张量。为了得到一个张量，必须引入一个修正项，该修正项恰好与向量场本身的不可交换性有关。这引出了 **Riemann [曲率张量](@entry_id:181383) (Riemann curvature tensor)** $R$ 的标准定义 [@problem_id:3077168]：
$$ R(X,Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]} Z $$
这个定义的美妙之处在于，右侧的非张量项（涉及 $Z$ 的[二阶导数](@entry_id:144508)和 $X,Y$ 的[一阶导数](@entry_id:749425)的项）恰好被消除了。我们可以通过直接计算来验证 $R(X,Y)Z$ 在其所有三个向量变元 $X, Y, Z$ 上都是 $C^\infty(M)$-线性的，因此 $R$ 是一个 $(1,3)$-型张量场 [@problem_id:3077149]。

上述定义可以重写为 **Ricci 恒等式 (Ricci identity)**：
$$ \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z = R(X,Y)Z + \nabla_{[X,Y]} Z $$
这个恒等式清楚地表明，**曲率是在考虑了向量场流动本身的不[可交换性](@entry_id:263314)（由 $\nabla_{[X,Y]}Z$ 项体现）之后，[二阶协变导数](@entry_id:193368)算子不可交换的内在度量**。如果向量场 $X, Y$ 本身是可交换的（即 $[X,Y]=0$，例如[坐标基](@entry_id:270149)向量场），则该恒等式简化为 $\nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z = R(X,Y)Z$ [@problem_id:3077168]。

#### 曲率的几何定义：无穷小和乐

曲率也具有深刻的几何意义，它与向量沿闭合回路的平行移动有关。考虑在 $p$ 点的一个切向量 $W_p \in T_p M$。我们将它沿着一个以 $p$ 为基点的无穷小闭合回路 $\gamma$ 平行移动。当回到 $p$ 点时，这个向量 $W_p$ 会变成一个新的向量 $W'_p$。在平坦空间中，$W'_p = W_p$。但在弯曲空间中，通常 $W'_p \neq W_p$。

这个变换 $W_p \mapsto W'_p$ 是一个[线性变换](@entry_id:149133)，称为沿回路 $\gamma$ 的 **[和乐](@entry_id:137051) (holonomy)**。曲率张量 $R$ 精确地量化了这种无穷小[和乐](@entry_id:137051)效应。对于一个由向量 $X, Y$ 在 $p$ 点张成的无穷小“平行四边形”回路（面积正比于 $\epsilon^2$），平行移动引起的向量变化 $\Delta W_p = W'_p - W_p$ 在最低阶上由曲率给出 [@problem_id:3077140]：
$$ \Delta W_p \approx \epsilon^2 R_p(X,Y)W_p $$
这个结果表明，**曲率是空间内在弯曲的度量，它导致一个向量在沿无穷小闭合回路平行移动后发生“旋转”**。$R(X,Y)$ 这个算子本身可以被看作是生成这种[无穷小旋转](@entry_id:166635)的“李代数”元素。所有沿基点在 $p$ 的可缩回路的[和乐](@entry_id:137051)变换构成一个[李群](@entry_id:137659)，称为 **[限制和乐群](@entry_id:637133) (restricted holonomy group)**，其[李代数](@entry_id:137954)正是由形如 $R(X,Y)$ 的所有[曲率算子](@entry_id:198006)生成的（Ambrose-Singer 定理）。

#### 两种定义的等价性

曲率的代数定义（[协变导数的交换子](@entry_id:198075)）和几何定义（无穷小[和乐](@entry_id:137051)）是等价的 [@problem_id:3077133]。这构成了[微分几何](@entry_id:145818)中最深刻和优美的结果之一。代数定义中的 $\nabla_{[X,Y]}Z$ 修正项，其几何意义正是为了补偿用于构造回路的向量场流本身不闭合所造成的影响，从而分离出纯粹由空间弯曲导致的和乐效应。无论联络是否具有挠率，这种等价性都成立。挠率和曲率是联络的两个独立的基本[不变量](@entry_id:148850)，分别描述了空间的“扭曲”和“弯曲”。

#### 曲率的坐标表示与计算

从曲率的代数定义，我们可以推导出其在[局部坐标](@entry_id:181200)中的分量表达式 [@problem_id:3077190]。设 $X=\partial_m, Y=\partial_n, Z=\partial_k$。由于 $[\partial_m, \partial_n]=0$，我们有 $R(\partial_m, \partial_n)\partial_k = \nabla_{\partial_m}\nabla_{\partial_n}\partial_k - \nabla_{\partial_n}\nabla_{\partial_m}\partial_k$。通过繁琐但直接的计算，可以得到[曲率张量](@entry_id:181383)的分量 $R^\ell{}_{kmn}$（定义为 $R(\partial_m, \partial_n)\partial_k = R^\ell{}_{kmn}\partial_\ell$）：
$$ R^\ell{}_{kmn} = \partial_m \Gamma^\ell_{nk} - \partial_n \Gamma^\ell_{mk} + \Gamma^p_{nk}\Gamma^\ell_{mp} - \Gamma^p_{mk}\Gamma^\ell_{np} $$
这个公式虽然复杂，但是进行具体计算的基础。例如，给定一组 Christoffel 符号，如 [@problem_id:3077190] 中所假设的，我们可以代入此公式，计算出在特定点的曲率分量。这个过程是检验理论理解和计算技巧的经典练习。

### 重要联络与恒等式

#### Levi-Civita 联络：[黎曼几何基本定理](@entry_id:189185)

到目前为止，我们讨论的[仿射联络](@entry_id:160152)是非常一般的。然而，在 **黎曼流形 (Riemannian manifold)** $(M,g)$ 中，即配备了度量张量 $g$ 的[流形](@entry_id:153038)，有一个非常特殊的联络扮演着核心角色。这个联络由两个条件唯一确定：

1.  **无挠性 (Torsion-free)**: $T=0$。
2.  **[度量兼容性](@entry_id:265910) (Metric-compatibility)**: $\nabla g = 0$。

[度量兼容性](@entry_id:265910)意味着[协变导数](@entry_id:152476)与度量张量可以“交换”，即对于任意向量场 $X, Y, Z$，都有 $X(g(Y,Z)) = g(\nabla_X Y, Z) + g(Y, \nabla_X Z)$。这保证了向量在平行移动过程中其长度以及它们之间的角度保持不变。

**[黎曼几何基本定理](@entry_id:189185) (The Fundamental Theorem of Riemannian Geometry)** 断言 [@problem_id:3077141]：
> 在任何一个[黎曼流形](@entry_id:261160) $(M,g)$ 上，存在唯一一个既无挠又与度量兼容的[仿射联络](@entry_id:160152)。

这个唯一的联络被称为 **Levi-Civita 联络 (Levi-Civita connection)**。它的唯一性可以通过一个显式构造公式，即 **Koszul 公式 (Koszul formula)**，来证明。该公式表达了 $g(\nabla_X Y, Z)$ 如何完全由度量张量 $g$ 及其一阶导数（通过 Lie 括号体现）确定。这个定理是黎曼几何的基石，因为它在度量结构和[微分](@entry_id:158718)结构之间建立了一座唯一的桥梁。

#### [自平行曲线](@entry_id:269969)与[测地线](@entry_id:269969)

有了 Levi-Civita 联络，我们现在可以精确地区分两个密切相关的概念：[自平行曲线](@entry_id:269969)和[测地线](@entry_id:269969) [@problem_id:3077183]。

-   **[自平行曲线](@entry_id:269969) (Autoparallel curve)** 是一个与 **联络 $\nabla$** 相关的概念，由方程 $\nabla_{\dot{\gamma}}\dot{\gamma} = 0$ 定义。正如我们所见，它只依赖于联络的对称部分 $\Gamma^k_{(ij)}$。

-   **[测地线](@entry_id:269969) (Geodesic)** 是一个与 **度量 $g$** 相关的概念。它通常被定义为局部连接两点[最短路径](@entry_id:157568)的曲线。通过[变分法](@entry_id:163656)，可以证明[测地线](@entry_id:269969)是[能量泛函](@entry_id:170311) $E(\gamma) = \frac{1}{2}\int g(\dot{\gamma}, \dot{\gamma}) dt$ 的[临界点](@entry_id:144653)。其对应的 Euler-Lagrange 方程恰好是 Levi-Civita 联络的自平行方程。

因此，**Levi-Civita 联络的[自平行曲线](@entry_id:269969)（在[仿射参数](@entry_id:260625)化下）与度量张量的[测地线](@entry_id:269969)是同一回事** [@problem_id:3077183]。对于一个一般的联络 $\nabla$，其[自平行曲线](@entry_id:269969)是否为[测地线](@entry_id:269969)，取决于 $\nabla$ 的对称部分是否与 Levi-Civita 联络一致。即使一个联络是度量兼容的，如果它有挠率，其[自平行曲线](@entry_id:269969)通常也不会是[测地线](@entry_id:269969)。这清晰地揭示了挠率如何使自平行路径偏离长度最短的路径。

#### Bianchi 恒等式

曲率张量并非完全任意，它必须满足一些普适的代数和[微分](@entry_id:158718)恒等式，称为 **Bianchi 恒等式 (Bianchi identities)**。对于一个[无挠联络](@entry_id:181337)，最重要的[微分](@entry_id:158718)恒等式是 **第二 Bianchi 恒等式**。用[抽象指标记法](@entry_id:161431)，它可以简洁地写成：
$$ \nabla_{[i} R^\ell{}_{k|mn|} = 0 $$
这里的符号需要仔细解读 [@problem_id:3077193]。方括号 $[i \dots m \dots n]$ 表示对其中包含的指标 $i, m, n$ 进行反对称化（即对这三个指标的所有[置换](@entry_id:136432)求和，并根据[置换的符号](@entry_id:137178)赋予正负号）。竖线 $|k|$ 表示被排除在反对称化操作之外的指标。由于[曲率张量](@entry_id:181383)本身在最后两个指标上是反对称的（$R^\ell{}_{kmn} = -R^\ell{}_{knm}$），这个恒等式展开后等价于一个循环求和：
$$ \nabla_i R^\ell{}_{kmn} + \nabla_m R^\ell{}_{kni} + \nabla_n R^\ell{}_{kim} = 0 $$
这个恒等式是[曲率张量](@entry_id:181383)的一个基本性质，它在广义相对论等领域有重要的物理应用，例如，它是推导爱因斯坦场方程中[能量-动量守恒](@entry_id:194427)的数学基础。它深刻地约束了空间弯曲的方式，表明曲率的变化不是任意的，而是遵循着严格的[微分](@entry_id:158718)定律。