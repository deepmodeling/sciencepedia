## 引言
在探索[光滑流形](@entry_id:160799)的几何学时，我们很快就会遇到一个根本性的挑战：如何对定义在[流形上的向量](@entry_id:160178)场进行[微分](@entry_id:158718)？在熟悉的[欧氏空间](@entry_id:138052)中，我们可以简单地对向量的分量求[偏导数](@entry_id:146280)。然而，在一个弯曲的[流形](@entry_id:153038)上，不同点的[切空间](@entry_id:199137)是相互独立的[向量空间](@entry_id:151108)，直接比较和计算相邻点向量之差失去了明确的意义。这种朴素的[微分](@entry_id:158718)方式其结果会依赖于[坐标系](@entry_id:156346)的选择，违背了我们寻求[内蕴几何](@entry_id:158788)性质的初衷。为了解决这一难题，数学家引入了一个强大而优美的概念——**[仿射联络](@entry_id:160152)（Affine Connection）**。它为我们提供了一套一致的规则，用以“连接”相邻的切空间，从而在弯曲空间中明确地定义[方向导数](@entry_id:189133)。[仿射联络](@entry_id:160152)是整个[微分几何](@entry_id:145818)大厦的基石，它使得谈论加速度、平行移动和曲率等概念成为可能。

本文将系统地引导你进入[仿射联络](@entry_id:160152)的世界。在第一章“**原理与机制**”中，我们将从最基本的公理出发，定义作为[仿射联络](@entry_id:160152)核心的[协变导数](@entry_id:152476)，并学习如何在[局部坐标系](@entry_id:751394)下利用[克里斯托费尔符号](@entry_id:159831)进行具体计算。随后，在“**应用与跨学科联系**”一章中，我们将见证[仿射联络](@entry_id:160152)的威力，探索它如何定义了空间中最直的路径（[测地线](@entry_id:269969)），如何成为描述[引力](@entry_id:175476)的语言（广义相对论），以及如何揭示[流形](@entry_id:153038)的整体拓扑性质。最后，在“**动手实践**”部分，你将通过解决具体问题，将理论知识转化为可操作的技能。现在，让我们从建立[仿射联络](@entry_id:160152)的基本原理开始。

## 原理与机制

在引入了[光滑流形](@entry_id:160799)上向量场的概念之后，我们面临一个核心的分析问题：如何对向量场进行[微分](@entry_id:158718)？在[欧氏空间](@entry_id:138052) $\mathbb{R}^n$ 中，我们可以简单地对向量场的每个分量关于坐标求[偏导数](@entry_id:146280)。然而，在一般的弯曲[流形](@entry_id:153038)上，这种朴素的方法是行不通的，因为不同点的[切空间](@entry_id:199137)是不同的，直接比较两个无穷近点上的向量是没有意义的。此外，偏导数的结果依赖于[坐标系](@entry_id:156346)的选择，而我们寻求的是一种内蕴的、与坐标无关的[微分](@entry_id:158718)方式。为了解决这个问题，我们引入了**[仿射联络](@entry_id:160152) (affine connection)** 的概念，它提供了一种在[流形](@entry_id:153038)上一致地“连接”邻近切空间并定义[方向导数](@entry_id:189133)的方法。

### [仿射联络](@entry_id:160152)的定义：[协变导数](@entry_id:152476)

[仿射联络](@entry_id:160152)，通常用符号 $\nabla$ 表示，是一个映射，它取两个向量场 $X$ 和 $Y$，并生成一个新的向量场 $\nabla_X Y$。这个新的向量场直观上代表了向量场 $Y$ 沿着向量场 $X$ 方向的变化率。因此，$\nabla_X Y$ 也被称为 $Y$ 沿 $X$ 的**[协变导数](@entry_id:152476) (covariant derivative)**。

为了使这个导数算子具有良好和一致的性质，它必须满足一组特定的公理。这些公理确保了协变导数以一种合理的方式与向量场的[代数结构](@entry_id:137052)（作为实[向量空间](@entry_id:151108)和光滑函数模）相互作用。一个[仿射联络](@entry_id:160152) $\nabla$ 是一个映射 $\nabla: \Gamma(TM) \times \Gamma(TM) \to \Gamma(TM)$，对于所有向量场 $X, Y, Z \in \Gamma(TM)$、光滑函数 $f \in \mathcal{C}^{\infty}(M)$ 以及实数 $a, b \in \mathbb{R}$，它必须满足以下四个核心属性 [@problem_id:3025051]：

1.  **在第一个变元中的 $\mathcal{C}^{\infty}(M)$-线性性**：
    $$ \nabla_{fX} Y = f \nabla_X Y $$
    这个性质表明，在某一点 $p \in M$ 的[协变导数](@entry_id:152476) $(\nabla_X Y)_p$ 仅依赖于向量 $X_p \in T_p M$ 在该点的值，而与向量场 $X$ 在 $p$ 点邻域内的变化无关。换句话说，它在第一个变元中是“逐点”定义的，这是一个张量性的关键特征。

2.  **在第一个变元中的可加性**：
    $$ \nabla_{X+Z} Y = \nabla_X Y + \nabla_Z Y $$
    结合前一个性质，这意味着 $\nabla$ 在其第一个参数上是 $\mathcal{C}^{\infty}(M)$-线性的，也即对函数乘法和加法都表现出线性。

3.  **在第二个变元中的 $\mathbb{R}$-线性性**：
    $$ \nabla_X (aY+bZ) = a\nabla_X Y + b\nabla_X Z $$
    这表明对于固定的 $X$，算子 $\nabla_X$ 是作用在向量场空间上的一个[线性变换](@entry_id:149133)。

4.  **在第二个变元中的[莱布尼茨法则](@entry_id:157949) (Leibniz Rule)**：
    $$ \nabla_X(fY) = (Xf)Y + f\nabla_X Y $$
    这是[协变导数](@entry_id:152476)最关键的特性之一。它表明对向量场 $fY$ 的求导由两部分组成：一部分来自于函数 $f$ 自身的变化（由 $Xf$ 捕获），另一部分来自于向量场 $Y$ 的变化（由 $f\nabla_X Y$ 捕获）。这个法则精确地刻画了 $\nabla_X$ 作为一个“导数”算子的本质。

总而言之，一个[仿射联络](@entry_id:160152) $\nabla$ 在第一个变元上是 $\mathcal{C}^{\infty}(M)$-线性的，而在第二个变元上是一个满足[莱布尼茨法则](@entry_id:157949)的导数算子。

### [坐标系](@entry_id:156346)中的联络：克氏符号

虽然[仿射联络](@entry_id:160152)的定义是抽象且与坐标无关的，但在实际计算中，我们通常需要在局部坐标系中对其进行操作。在一个[局部坐标系](@entry_id:751394) $\{x^i\}$ 中，切空间由[基向量](@entry_id:199546)场 $\{\partial_i = \frac{\partial}{\partial x^i}\}$ 张成。一个联络的全部信息都蕴含在它如何作用于这些[基向量](@entry_id:199546)场上。

我们将 $\nabla_{\partial_i} \partial_j$ 的结果在同一基底下展开，其分量被称为**克里斯托费尔符号 (Christoffel symbols)** 或**[联络系数](@entry_id:157618) (connection coefficients)**，记为 $\Gamma^k_{ij}$：
$$ \nabla_{\partial_i} \partial_j = \Gamma^k_{ij} \partial_k $$
这里我们采用了爱因斯坦求和约定，即对重复出现的上下指标自动求和。克氏符号 $\Gamma^k_{ij}$ 通常是坐标 $x^i$ 的函数，它们完整地刻画了联络在所选坐标域内的性质。

有了克氏符号，我们就可以计算任意向量场 $Y = Y^j \partial_j$ 沿[基向量](@entry_id:199546)场 $\partial_i$ 的协变导数。利用公理3和4：
$$ \nabla_{\partial_i} Y = \nabla_{\partial_i} (Y^j \partial_j) = (\partial_i Y^j) \partial_j + Y^j (\nabla_{\partial_i} \partial_j) = (\partial_i Y^j) \partial_j + Y^j \Gamma^k_{ij} \partial_k $$
为了使表达式更清晰，我们交换[哑指标](@entry_id:188070) $j$ 和 $k$，得到[协变导数](@entry_id:152476)的分量形式：
$$ \nabla_{\partial_i} Y = (\partial_i Y^k + \Gamma^k_{ij} Y^j) \partial_k $$
这个公式至关重要。它表明[协变导数](@entry_id:152476)由两部分构成：第一部分 $\partial_i Y^k$ 是向量分量的普通偏导数，它描述了向量分量自身的变化；第二部分 $\Gamma^k_{ij} Y^j$ 是一个“修正项”，它解释了由于[基向量](@entry_id:199546) $\partial_j$ 自身在[流形](@entry_id:153038)上的变化所带来的影响。

进一步，对于任意两个向量场 $X = X^i \partial_i$ 和 $Y = Y^j \partial_j$，我们可以利用所有公理计算 $\nabla_X Y$：
$$ \nabla_X Y = \nabla_{X^i \partial_i} (Y^j \partial_j) = X^i \nabla_{\partial_i} (Y^j \partial_j) = X^i ((\partial_i Y^j)\partial_j + Y^j \nabla_{\partial_i} \partial_j) $$
$$ = X^i (\partial_i Y^k) \partial_k + X^i Y^j \Gamma^k_{ij} \partial_k = (X^i \partial_i Y^k + X^i Y^j \Gamma^k_{ij}) \partial_k $$
括号内的项 $(X(Y^k) + X^i Y^j \Gamma^k_{ij})$ 就是向量场 $\nabla_X Y$ 在基底 $\{\partial_k\}$ 下的第 $k$ 个分量。

作为一个具体的计算实例，考虑一个[二维流形](@entry_id:188198)，其非零克氏符号仅为 $\Gamma_{11}^2 = x^1$。设向量场 $X = x^2 \partial_1 + x^1 \partial_2$, $Y = (x^1)^3 \partial_2$ 以及函数 $f = \cos(x^2)$。我们来计算 $\nabla_X(fY)$ [@problem_id:1623087]。根据[莱布尼茨法则](@entry_id:157949)，我们有：
$$ \nabla_X(fY) = (Xf)Y + f \nabla_X Y $$
首先计算 $Xf = (x^2 \partial_1 + x^1 \partial_2)(\cos(x^2)) = -x^1 \sin(x^2)$。
然后计算 $\nabla_X Y = X^1 \nabla_{\partial_1} Y + X^2 \nabla_{\partial_2} Y = x^2 \nabla_{\partial_1} Y + x^1 \nabla_{\partial_2} Y$。
其中 $\nabla_{\partial_1} Y = \nabla_{\partial_1}((x^1)^3 \partial_2) = (\partial_1(x^1)^3)\partial_2 + (x^1)^3 \nabla_{\partial_1}\partial_2 = 3(x^1)^2 \partial_2$ (因为 $\Gamma^k_{12}=0$)。
而 $\nabla_{\partial_2} Y = 0$ (因为 $Y$ 的分量不依赖 $x^2$ 且 $\Gamma^k_{22}=0$)。
所以 $\nabla_X Y = x^2 (3(x^1)^2 \partial_2) = 3(x^1)^2 x^2 \partial_2$。
综合起来，
$$ \nabla_X(fY) = (-x^1 \sin(x^2))((x^1)^3 \partial_2) + \cos(x^2)(3(x^1)^2 x^2 \partial_2) = (-(x^1)^4 \sin(x^2) + 3(x^1)^2 x^2 \cos(x^2)) \partial_2 $$
这个例子展示了如何结合联络的公理和克氏符号进行具体计算。

### 变换性质：联络是张量吗？

一个自然的问题是：克氏符号 $\Gamma^k_{ij}$ 是否构成一个张量的分量？答案是否定的。为了看清这一点，我们考察坐标变换 $x \to x'$ 下[克氏符号的变换法则](@entry_id:180944)。通过复杂的推导可以得出：
$$ \Gamma'^{p}_{mn} = \frac{\partial x'^p}{\partial x^k} \frac{\partial x^i}{\partial x'^m} \frac{\partial x^j}{\partial x'^n} \Gamma^k_{ij} + \frac{\partial x'^p}{\partial x^k} \frac{\partial^2 x^k}{\partial x'^m \partial x'^n} $$
这个变换法则的第一项是标准的 $(1,2)$ 型张量的变换方式，但第二项的存在破坏了张量性。这个“非齐次”或“非张量”项的存在，表明克氏符号的取值不仅依赖于几何结构，还依赖于[坐标系](@entry_id:156346)自身的弯曲。

一个经典的例子可以清晰地说明这一点 [@problem_id:1488875]。考虑二维欧氏平面，在[笛卡尔坐标系](@entry_id:169789) $(x,y)$ 中，度规是常数，$g_{ij} = \delta_{ij}$，对应的 Levi-Civita 联络（一种特殊的[仿射联络](@entry_id:160152)，我们稍后讨论）的所有克氏符号均为零，即 $\Gamma^k_{ij}=0$。如果克氏符号是张量，那么在任何[坐标系](@entry_id:156346)下它的分量都应该为零。然而，在极[坐标系](@entry_id:156346) $(r,\theta)$ 中，通过计算可以得到非零分量，例如 $\Gamma'^r_{\theta\theta} = -r$。这个非零结果明确地证明了克氏符号不遵循[张量变换法则](@entry_id:185176)。

尽管联络本身不是张量，但一个非常重要的性质是：**两个不同联络的差是一个张量**。假设我们有两个联络 $\nabla$ 和 $\tilde{\nabla}$，它们在同一[坐标系](@entry_id:156346)下的克氏符号分别是 $\Gamma^k_{ij}$ 和 $\tilde{\Gamma}^k_{ij}$。它们在另一个[坐标系](@entry_id:156346) $x'$ 下的符号为 $\Gamma'^p_{mn}$ 和 $\tilde{\Gamma}'^p_{mn}$。定义一个量 $A^k_{ij} = \Gamma^k_{ij} - \tilde{\Gamma}^k_{ij}$。当我们计算 $A'^p_{mn} = \Gamma'^p_{mn} - \tilde{\Gamma}'^p_{mn}$ 时，两个变换法则中恼人的非张量项 $\frac{\partial x'^p}{\partial x^k} \frac{\partial^2 x^k}{\partial x'^m \partial x'^n}$ 会完全相同并相互抵消。结果是：
$$ A'^{p}_{mn} = \frac{\partial x'^p}{\partial x^k} \frac{\partial x^i}{\partial x'^m} \frac{\partial x^j}{\partial x'^n} A^k_{ij} $$
这正是 $(1,2)$ 型张量的变换法则 [@problem_id:1488827]。这个事实意味着，[流形](@entry_id:153038)上所有可能的[仿射联络](@entry_id:160152)构成的空间是一个**[仿射空间](@entry_id:152906)**，其底层的[向量空间](@entry_id:151108)是 $(1,2)$ 型[张量场](@entry_id:190170)构成的空间。

### 联络的基本属性

通过组合和比较[协变导数](@entry_id:152476)，我们可以定义出描述联络关键特征的张量，其中最重要的是挠率和曲率。

#### 挠率

联络的**[挠率张量](@entry_id:204137) (torsion tensor)** $T$ 度量了联络在低阶指标上的不对称性。它定义为：
$$ T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y] $$
其中 $[X,Y]$ 是两个[向量场的李括号](@entry_id:193400)。在局部坐标系中，由于基[向量场的李括号](@entry_id:193400)为零（$[\partial_i, \partial_j]=0$），[挠率张量](@entry_id:204137)的分量形式非常简洁：
$$ T^k_{ij} = \Gamma^k_{ij} - \Gamma^k_{ji} $$
从这个定义可以清楚地看到，[挠率张量](@entry_id:204137)是克氏符号反对称部分的两倍。如果一个[联络的挠率](@entry_id:192913)张量处处为零，即 $T=0$，或者等价地，其克氏符号对于下两个指标是对称的（$\Gamma^k_{ij} = \Gamma^k_{ji}$），我们就称这个联络是**[无挠的](@entry_id:161664) (torsion-free)** 或**对称的 (symmetric)**。例如，如果一个联络有非零分量 $\Gamma^1_{12} = \frac{1}{2}(x^1)^2 + 3$ 和 $\Gamma^1_{21} = -\frac{1}{2}(x^1)^2 + 1$，那么其挠率分量 $T^1_{12} = \Gamma^1_{12} - \Gamma^1_{21} = (x^1)^2 + 2$ 是非零的，表明该联络有挠 [@problem_id:1488882]。

#### 度规相容性

如果[流形](@entry_id:153038)上装备了一个[度规张量](@entry_id:160222) $g$（例如黎曼度规或[洛伦兹度规](@entry_id:184391)），我们就可以提出一个关于联络和度规之间关系的问题：这个联络是否“保持”度规结构？具体来说，向量在平行移动时其长度和它们之间的角度是否保持不变？

这个问题的数学表述是联络是否与度规**相容 (compatible)**。一个联络 $\nabla$ 被称为与度规 $g$ 相容，如果[度规张量](@entry_id:160222) $g$ 的[协变导数](@entry_id:152476)为零：
$$ \nabla g = 0 $$
在分量形式下，对一个二阶[协变张量](@entry_id:634493)求导的法则为 $\nabla_k g_{ij} = \partial_k g_{ij} - \Gamma^l_{ki} g_{lj} - \Gamma^l_{kj} g_{il}$。因此，度规[相容性条件](@entry_id:637057)等价于对所有 $i,j,k$ 成立：
$$ \partial_k g_{ij} - \Gamma^l_{ki} g_{lj} - \Gamma^l_{kj} g_{il} = 0 $$
这个条件也被称为**黎卡提方程 (Ricci's lemma)**。

如果一个联络不满足度规相容性，那么 $\nabla g \neq 0$。这会带来直接的物理后果。例如，一个向量 $V$ 沿曲线 $\gamma(t)$ 进行平行输运时，其长度的平方 $L^2 = g_{ij} V^i V^j$ 的变化率可以被计算出来 [@problem_id:1488819]：
$$ \frac{d}{dt} L^2 = \frac{d}{dt} (g_{ij} V^i V^j) = (\nabla_k g_{ij}) \dot{x}^k V^i V^j $$
其中 $\dot{x}^k$ 是曲线切向量的分量。这个公式清楚地表明，当且仅当联络与度规相容（$\nabla g = 0$）时，任何向量在沿任意曲线平行输运时其长度都保持不变。若不相容，则[向量长度](@entry_id:156432)会发生变化，如在一个特定的非相容联络下，一个向量的长度可能会随着移动而收缩或膨胀 [@problem_id:1488883]。

#### Levi-Civita 联络

在[黎曼几何](@entry_id:160508)和广义相对论中，最重要的一类联络是 **Levi-Civita 联络**。对于一个给定的（伪）黎曼度规 $g$，存在一个**唯一**的[仿射联络](@entry_id:160152)，它同时满足**无挠**和**度规相容**这两个条件。这个唯一的联络就是 Levi-Civita 联络。这个基本定理是[黎曼几何](@entry_id:160508)的基石，它保证了每个[黎曼流形](@entry_id:261160)都有一个自然的、内蕴的[微分](@entry_id:158718)结构。

值得注意的是，无挠和度规相容是两个独立的条件。并非所有[无挠的](@entry_id:161664)联络都是某个度规的 Levi-Civita 联络。我们可以构造一个[无挠的](@entry_id:161664)联络，然后证明不存在任何黎曼度规能使其满足度规相容性条件，因为该条件会推导[出度](@entry_id:263181)规矩阵是退化的，这与黎曼度规的定义相矛盾 [@problem_id:1623027]。这揭示了 Levi-Civita 联络在所有[仿射联络](@entry_id:160152)中确实是一个非常特殊的选择。

### 曲率、[测地线](@entry_id:269969)与[平行输运](@entry_id:160671)

有了协变导数，我们就可以定义[流形](@entry_id:153038)上最重要的几个几何概念。

**平行输运 (Parallel Transport)**：给定一条曲线 $\gamma(t)$，我们说一个向量场 $V$ 是沿着 $\gamma$ **平行输运**的，如果它沿着该曲线的[协变导数](@entry_id:152476)为零：
$$ \nabla_{\dot{\gamma}} V = 0 $$
在[局部坐标](@entry_id:181200)中，这写成一个关于 $t$ 的[一阶线性常微分方程](@entry_id:164502)组：
$$ \frac{dV^k}{dt} + \Gamma^k_{ij} \frac{dx^i}{dt} V^j = 0 $$
给定初始向量 $V(0)$，这个方程在曲线上有唯一的解。平行输运的直观意义是，向量 $V$ 在沿着曲线移动时“尽可能保持自身方向不变”。

**[测地线](@entry_id:269969) (Geodesics)**：[测地线](@entry_id:269969)是“最直的”曲线。在欧氏空间中，这是直线。在弯曲[流形](@entry_id:153038)上，[测地线](@entry_id:269969)被定义为**将其自身切向量[平行输运](@entry_id:160671)的曲线**。设曲线由参数 $\lambda$ [参数化](@entry_id:272587)，其切向量为 $T = \frac{d\gamma}{d\lambda}$，则测地线方程为：
$$ \nabla_T T = 0 $$
在[局部坐标](@entry_id:181200)中，这展开为一个二阶[非线性常微分方程](@entry_id:142950)组，即**测地线方程**：
$$ \frac{d^2 x^k}{d\lambda^2} + \Gamma^k_{ij} \frac{dx^i}{d\lambda} \frac{dx^j}{d\lambda} = 0 $$
在物理学中，广义相对论的一个基本假设是，在[引力场](@entry_id:169425)中自由下落的粒子所遵循的路径正是[时空流形](@entry_id:262092)的[测地线](@entry_id:269969)。如果存在其他作用[力场](@entry_id:147325)，粒子的[运动方程](@entry_id:170720)则会偏离测地线方程，例如变为 $\frac{D T^\sigma}{d\lambda} = K^\sigma_\nu T^\nu$ 的形式，其中 $K^\sigma_\nu$ 代表外场的影响 [@problem_id:1535637]。

**曲率 (Curvature)**：曲率是衡量[流形](@entry_id:153038)弯曲程度的最终量度，它也完全由联络决定。曲率的一个直观理解是[协变导数](@entry_id:152476)的不[可交换性](@entry_id:263314)。在平坦空间中，[二阶偏导数](@entry_id:635213)的顺序可以交换（$\partial_i \partial_j f = \partial_j \partial_i f$）。但在弯曲空间中，[协变导数](@entry_id:152476)的顺序一般不可交换。

**黎曼曲率张量 (Riemann Curvature Tensor)** $R$ 精确地量化了这种不[可交换性](@entry_id:263314)。它被定义为一个映射，取三个向量场 $X, Y, Z$，并返回一个新的向量场：
$$ R(X, Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X, Y]} Z $$
如果 $X, Y$ 是[坐标基](@entry_id:270149)向量场 $\partial_i, \partial_j$，则它们的[李括号](@entry_id:636461)为零，公式简化为 $R(\partial_i, \partial_j)\partial_k = \nabla_{\partial_i} \nabla_{\partial_j} \partial_k - \nabla_{\partial_j} \nabla_{\partial_i} \partial_k$。

如果对于所有 $X, Y, Z$，曲率张量 $R(X,Y)Z$ 都为零，则称联络是**平坦的 (flat)**。一个平坦的联络意味着协变导数可以交换，并且向量沿任意闭合回路平行输运后会返回其自身。反之，非零的曲率意味着空间是内蕴弯曲的。即使是在我们熟悉的 $\mathbb{R}^3$ 空间，也可以定义一个具有非零曲率的联络，只要其克氏符号是[非线性](@entry_id:637147)的函数即可 [@problem_id:1623061]。这说明，空间的几何结构不仅仅由其拓扑决定，更关键的是由其上定义的联络所决定。

总之，[仿射联络](@entry_id:160152)是微分几何的核心工具，它统一了导数、[平行输运](@entry_id:160671)、[测地线](@entry_id:269969)和曲率等基本概念，为研究弯曲空间中的分析和几何提供了坚实的框架。