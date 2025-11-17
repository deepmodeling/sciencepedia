## 引言
在探索弯曲空间（即[流形](@entry_id:153038)）的几何学时，一个根本性的挑战是如何定义向量场的变化率。在平直的[欧氏空间](@entry_id:138052)中，我们可以简单地对向量的各个分量求偏导数，但在更广义的设定下，这种方法因忽略了[坐标基](@entry_id:270149)矢自身的变化而失效。为了弥补这一知识鸿沟，并建立一个内蕴且一致的[微分](@entry_id:158718)框架，数学家们引入了“联络”这一核心概念，而联络系数（在黎曼几何中常被称为克里斯托费尔符号）正是这一抽象工具在[局部坐标系](@entry_id:751394)下的具体实现。它们是微分几何的基石，深刻地影响了我们对[引力](@entry_id:175476)、宇宙学乃至物质基本相互作用的理解。

本文将系统地引导读者深入联络系数的世界。在“**原理与机制**”一章中，我们将从协变导数的引入出发，揭示联络系数为何是必要的，阐明其非张量的本质，并推导在黎曼几何中如何从[度规张量](@entry_id:160222)唯一确定它们。接下来，在“**应用与跨学科联系**”一章中，我们将跨出纯粹的数学理论，探讨联络系数如何在物理学和工程学中大放异彩，从描述[行星轨道](@entry_id:179004)的[测地线方程](@entry_id:264349)，到解释[宇宙膨胀](@entry_id:161474)的哈勃定律，再到分析壳体结构的应力。最后，通过“**动手实践**”中的精选问题，读者将有机会亲手计算和应用联络系数，将理论知识转化为解决实际问题的能力。通过这一系列的学习，我们将揭示联络系数作为连接抽象几何与具体物理现象的桥梁所扮演的关键角色。

## 原理与机制

在引入了[仿射联络](@entry_id:160152)作为在[流形](@entry_id:153038)上比较邻近点处向量的工具之后，本章将深入探讨其核心原理与具体机制。我们将重点关注作为联络在局部坐标系下具体表示的**联络系数 (connection coefficients)**，也即**[克里斯托费尔符号](@entry_id:159831) (Christoffel symbols)**。我们将从其为何必要开始，揭示其非张量的本质，推导其在黎曼几何中的确定表达式，并最终将其与[流形](@entry_id:153038)的[内蕴曲率](@entry_id:161701)联系起来。

### 协变导数：对偏导数的修正

在平坦的[欧氏空间](@entry_id:138052)中，使用笛卡尔坐标系时，我们可以简单地通过对向量的各个分量求偏导数来描述向量场的变化。例如，向量场 $V = V^i \partial_i$ 的导数可以被认为是 $(\partial_j V^i)$。然而，一旦我们进入弯曲的[流形](@entry_id:153038)，或即便是在平直空间中使用[曲线坐标系](@entry_id:172561)（如极坐标），这种简单的方法便会失效。

其根本原因在于，当我们在[流形](@entry_id:153038)上从一点移动到另一点时，[坐标基](@entry_id:270149)矢 $\partial_i = \frac{\partial}{\partial x^i}$ 本身也在发生变化。简单的偏导数 $\partial_j V^i$ 只捕捉了向量分量 $V^i$ 的变化，却完全忽略了[基矢](@entry_id:199546) $\partial_i$ 的变化。因此，$\partial_j V^i$ 这个量本身并非一个几何上或物理上良好定义的对象。

我们可以通过考察其在坐标变换下的行为来严格地证明这一点。考虑两个交叠的[坐标卡](@entry_id:262338) $(U, x^i)$ 和 $(\tilde{U}, \tilde{x}^\alpha)$。一个向量场 $X$ 的分量在两个[坐标系](@entry_id:156346)下的关系为：
$$
\tilde{X}^\alpha = \frac{\partial \tilde{x}^\alpha}{\partial x^i} X^i
$$
我们来计算新[坐标系](@entry_id:156346)下分量的偏导数 $\tilde{\partial}_\beta \tilde{X}^\alpha = \frac{\partial \tilde{X}^\alpha}{\partial \tilde{x}^\beta}$。利用链式法则和乘积法则：
$$
\begin{align}
\tilde{\partial}_\beta \tilde{X}^\alpha  = \frac{\partial}{\partial \tilde{x}^\beta} \left( \frac{\partial \tilde{x}^\alpha}{\partial x^i} X^i \right) \\
 = \left( \frac{\partial}{\partial \tilde{x}^\beta} \frac{\partial \tilde{x}^\alpha}{\partial x^i} \right) X^i + \frac{\partial \tilde{x}^\alpha}{\partial x^i} \left( \frac{\partial X^i}{\partial \tilde{x}^\beta} \right) \\
 = \frac{\partial x^j}{\partial \tilde{x}^\beta} \frac{\partial^2 \tilde{x}^\alpha}{\partial x^j \partial x^i} X^i + \frac{\partial \tilde{x}^\alpha}{\partial x^i} \frac{\partial x^j}{\partial \tilde{x}^\beta} \frac{\partial X^i}{\partial x^j}
\end{align}
$$
整理后得到：
$$
\tilde{\partial}_\beta \tilde{X}^\alpha = \frac{\partial \tilde{x}^\alpha}{\partial x^i} \frac{\partial x^j}{\partial \tilde{x}^\beta} (\partial_j X^i) + \frac{\partial^2 \tilde{x}^\alpha}{\partial x^i \partial x^j} \frac{\partial x^j}{\partial \tilde{x}^\beta} X^i
$$
一个类型为 $(1,1)$ 的张量，其分量 $T^i_j$ 的变换法则是均匀的（齐次的）：$\tilde{T}^\alpha_\beta = \frac{\partial \tilde{x}^\alpha}{\partial x^i} \frac{\partial x^j}{\partial \tilde{x}^\beta} T^i_j$。显然，$\partial_j X^i$ 的变换法则中多出了一个包含坐标变换[二阶导数](@entry_id:144508)的**非均匀项**。这个非均匀项的存在，证明了偏导数 $\partial_j X^i$ 并非一个张量的分量，其数值依赖于[坐标系](@entry_id:156346)的选择，缺乏内蕴的几何意义。[@problem_id:2972216]

为了修正这一点，我们引入一个几何对象，称为**[协变导数](@entry_id:152476) (covariant derivative)**，记为 $\nabla$。它在分量上定义为：
$$
\nabla_j V^i \equiv (\nabla_{\partial_j} V)^i = \partial_j V^i + \Gamma^i_{jk} V^k
$$
这里，我们引入了一组新的量 $\Gamma^i_{jk}$，它们被称为**联络系数**或**克里斯托费尔符号**。这个定义的精妙之处在于，我们希望通过精心构造 $\Gamma^i_{jk}$ 的变换性质，使其正好能够抵消掉 $\partial_j V^i$ 变换时产生的那个非均匀项，从而使得 $\nabla_j V^i$ 作为一个整体，能够像一个真正的 $(1,1)$ 型张量那样进行变换。

### 联络系数的本质：非张量性与变换定律

为了让 $\nabla_j V^i$ 成为一个张量，我们要求它满足[张量变换法则](@entry_id:185176)。联络系数 $\Gamma^i_{jk}$ 的变换法则正是由这一要求所决定的。通过繁琐但直接的代数推导，可以得到 $\Gamma^k_{ij}$ 在[坐标变换](@entry_id:172727) $x \to \tilde{x}$下的变换定律为：
$$
\tilde{\Gamma}^{m}_{pq} = \frac{\partial \tilde{x}^{m}}{\partial x^{r}} \frac{\partial x^{s}}{\partial \tilde{x}^{p}} \frac{\partial x^{t}}{\partial \tilde{x}^{q}} \Gamma^{r}_{st} + \frac{\partial \tilde{x}^{m}}{\partial x^{r}} \frac{\partial^{2} x^{r}}{\partial \tilde{x}^{p} \partial \tilde{x}^{q}}
$$
这个表达式明确地揭示了联络系数的本质。[@problem_id:2972229] 第一项是类型为 $(1,2)$ 张量所应有的齐次变换部分，但第二项是一个非齐次项，它依赖于坐标变换函数的[二阶导数](@entry_id:144508)。这个非齐次项的存在，是克里斯托费尔符号**不是张量分量**的决定性证据。

这一非张量特性具有深刻的几何意义。它意味着 $\Gamma^k_{ij}$ 的数值并非空间点本身的内蕴属性，而是与我们观察和测量该点所使用的[坐标系](@entry_id:156346)密切相关。一个有力的证明是**[法坐标](@entry_id:143194)系 (normal coordinates)** 的存在。对于[流形](@entry_id:153038)上的任意一点 $p$，我们总可以构造一个特殊的局部坐标系，使得在该点 $p$ 的所有克里斯托费尔符号均为零，即 $\Gamma^k_{ij}(p) = 0$。[@problem_id:2972216] [@problem_id:2972224] 如果 $\Gamma^k_{ij}$ 是一个张量的分量，那么它在一个[坐标系](@entry_id:156346)中为零就意味着在所有[坐标系](@entry_id:156346)中都为零。然而事实并非如此，这恰恰说明了 $\Gamma^k_{ij}$ 的值是坐标依赖的。它们可以被视为衡量所选[坐标系](@entry_id:156346)“弯曲”或“加速度”的量，而[协变导数](@entry_id:152476)中的 $+\Gamma V$ 项正是为了补偿这种坐标效应。

尽管联络本身不是张量，但两个不同联络的**差**却是一个张量。考虑两个不同的[仿射联络](@entry_id:160152) $\nabla$ 和 $\tilde{\nabla}$，其在同一[坐标系](@entry_id:156346)下的系数分别为 $\Gamma^k_{ij}$ 和 $\tilde{\Gamma}^k_{ij}$。它们的差定义为 $A(X, Y) = \nabla_X Y - \tilde{\nabla}_X Y$。在分量上，这对应于 $A^k_{ij} = \Gamma^k_{ij} - \tilde{\Gamma}^k_{ij}$。当进行坐标变换时，由于两个[联络系数的变换法则](@entry_id:190840)中非齐次项完全相同，它们在相减时会精确地抵消掉。因此，差值 $\Delta^k_{ij} = \Gamma^k_{ij} - \tilde{\Gamma}^k_{ij}$ 的变换法则是齐次的，满足一个 $(1,2)$ 型张量的变换规律。[@problem_id:2972229] [@problem_id:1857087]

总结来说，抽象的微分算子 $\nabla$ 是一个内蕴的、与坐标无关的几何对象，而克里斯托费尔符号 $\Gamma^k_{ij}$ 则是这个算子在特定[坐标基](@entry_id:270149)矢 $\{\partial_i\}$ 下的分量表示。[基矢](@entry_id:199546)的选择会影响分量的具体数值，这正是 $\Gamma^k_{ij}$ 坐标依赖性的根源。[@problem_id:2972224]

### Levi-Civita联络：从度规到联络系数

到目前为止，我们讨论的联络是广义的[仿射联络](@entry_id:160152)。在[黎曼几何](@entry_id:160508)中，我们处理的是具有[度规张量](@entry_id:160222) $g$ 的[流形](@entry_id:153038)。度规的存在允许我们从中唯一地确定一个“自然”的联络，即**[Levi-Civita联络](@entry_id:161107)**。这个联络由两个基本公理定义：

1.  **无挠性 (Torsion-free)**: 联络是对称的，即对于任意向量场 $X, Y$，我们有 $\nabla_X Y - \nabla_Y X = [X, Y]$，其中 $[X,Y]$ 是李括号。在[坐标基](@entry_id:270149)中，由于 $[\partial_i, \partial_j] = 0$，这等价于联络系数的下标记是对称的：$\Gamma^k_{ij} = \Gamma^k_{ji}$。
2.  **度规相容性 (Metric compatibility)**: [协变导数](@entry_id:152476)与度规的作用可交换，即 $\nabla g = 0$。这意味着向量在平行移动过程中其长度和它们之间的角度保持不变。对于任意向量场 $X, Y, Z$，此性质表现为：$Z(g(X,Y)) = g(\nabla_Z X, Y) + g(X, \nabla_Z Y)$。

从这两个公理出发，我们可以唯一地确定克里斯托费尔符号与度规张量及其导数之间的关系。这个推导过程被称为科祖尔技巧 (Koszul trick)。其最终结果，即著名的**科祖尔公式 (Koszul formula)**，给出了[克里斯托费尔符号](@entry_id:159831)的表达式：[@problem_id:2972194]
$$
\Gamma^k_{ij} = \frac{1}{2} g^{k\ell} \left( \partial_i g_{j\ell} + \partial_j g_{i\ell} - \partial_\ell g_{ij} \right)
$$
其中 $g^{k\ell}$ 是[逆度规张量](@entry_id:275529) $(g_{k\ell})^{-1}$ 的分量。这个公式是黎曼几何的基石之一。它表明，在一个黎曼流形上，只要度规张量 $g_{ij}$ 在某个[坐标系](@entry_id:156346)下给定，那么该[流形](@entry_id:153038)的几何结构——由[Levi-Civita联络](@entry_id:161107)所描述的平行移动规则——就完全被确定了。

### 计算与应用

有了科祖尔公式，我们就可以在任何给定的[坐标系](@entry_id:156346)中计算联络系数。

#### [平直空间](@entry_id:204618)中的[曲线坐标](@entry_id:178535)

一个极具启发性的例子是在一个我们熟知的平直二维平面上使用极坐标 $(r, \phi)$。虽然空间本身是平的，但极[坐标系](@entry_id:156346)是“弯曲”的。该[坐标系](@entry_id:156346)下的[线元](@entry_id:196833)为 $ds^2 = dr^2 + r^2 d\phi^2$。度规张量的分量为 $g_{rr}=1$, $g_{\phi\phi}=r^2$, $g_{r\phi}=0$。[逆度规](@entry_id:273874)为 $g^{rr}=1$, $g^{\phi\phi}=1/r^2$, $g^{r\phi}=0$。

度规分量 $g_{\phi\phi}$ 明显不是常数，它依赖于坐标 $r$。我们可以预见联络系数不会全部为零。使用科祖尔公式进行计算，我们可以得到几个非零的[克里斯托费尔符号](@entry_id:159831)，例如：[@problem_id:1857086]
$$
\Gamma^r_{\phi\phi} = \frac{1}{2}g^{r\sigma}(\partial_\phi g_{\phi\sigma} + \partial_\phi g_{\phi\sigma} - \partial_\sigma g_{\phi\phi}) = \frac{1}{2}g^{rr}(0+0-\partial_r g_{\phi\phi}) = \frac{1}{2}(1)(-\frac{\partial}{\partial r}(r^2)) = -r
$$
$$
\Gamma^\phi_{r\phi} = \frac{1}{2}g^{\phi\sigma}(\partial_r g_{\phi\sigma} + \partial_\phi g_{r\sigma} - \partial_\sigma g_{r\phi}) = \frac{1}{2}g^{\phi\phi}(\partial_r g_{\phi\phi} + \partial_\phi g_{r\phi} - \partial_\phi g_{r\phi}) = \frac{1}{2}\frac{1}{r^2}(\frac{\partial}{\partial r}(r^2)) = \frac{1}{r}
$$
这些非零的 $\Gamma$ 值代表了什么？它们精确地描述了极[坐标基](@entry_id:270149)矢 $\mathbf{e}_r$ 和 $\mathbf{e}_\phi$ 是如何随位置变化的。例如，$\Gamma^r_{\phi\phi}=-r$ 告诉我们，当沿着 $\phi$ 方向（即绕着原点）移动时，[基矢](@entry_id:199546) $\mathbf{e}_\phi$ 的变化中有一个指向 $-\mathbf{e}_r$ 方向的分量。这正是向心加速度的体现，它并非源于空间的弯曲，而是源于[坐标系](@entry_id:156346)本身的弯曲。这些联络系数恰好提供了描述在[曲线坐标系](@entry_id:172561)下运动（如[测地线方程](@entry_id:264349)）所必需的“伪力”项。[@problem_id:1857074]

#### 一般张量的[协变导数](@entry_id:152476)

[协变导数](@entry_id:152476)的概念可以从向量场自然地推广到任意类型的 $(r,s)$-张量。其法则源于[协变导数](@entry_id:152476)作用于张量积时满足莱布尼茨律。对于一个张量 $T^{i_1\dots i_r}{}_{j_1\dots j_s}$，其沿 $\partial_k$ 方向的协变导数分量为：
$$
\nabla_k T^{i_1\dots i_r}{}_{j_1\dots j_s} = \partial_k T^{i_1\dots i_r}{}_{j_1\dots j_s} + \sum_{a=1}^r \Gamma^{i_a}_{km} T^{i_1\dots m \dots i_r}{}_{j_1\dots j_s} - \sum_{b=1}^s \Gamma^{m}_{kj_b} T^{i_1\dots i_r}{}_{j_1\dots m \dots j_s}
$$
其中，在第一个求和中，$m$ 替换了第 $a$ 个上指标 $i_a$；在第二个求和中，$m$ 替换了第 $b$ 个下指标 $j_b$。规则可以简单记为：对每一个逆变（上）指标，加上一个 $\Gamma T$ 项；对每一个协变（下）指标，减去一个 $\Gamma T$ 项。[@problem_id:2972197] 这是一个在进行[张量分析](@entry_id:161423)计算时必须遵循的普适规则。例如，度规相容性条件 $\nabla_k g_{ij} = 0$ 就可以用这个公式展开，并最终推导出科祖尔公式。

### 联络系数与[内蕴曲率](@entry_id:161701)

我们已经看到，即使在[平直空间](@entry_id:204618)中，只要[坐标系](@entry_id:156346)是曲线的，联络系数也可能不为零。这引出了一个关键问题：我们如何从联络系数中分辨出[坐标系](@entry_id:156346)效应和空间本身的**[内蕴曲率](@entry_id:161701) (intrinsic curvature)**？

答案在于区分联络系数的*局部*可消除性与*全局*可消除性。正如之前提到的，在任何一点 $p$，我们总能找到一个[法坐标](@entry_id:143194)系使得 $\Gamma^k_{ij}(p)=0$。然而，我们能否找到一个覆盖[流形](@entry_id:153038)一个有限区域（甚至整个[流形](@entry_id:153038)）的[坐标系](@entry_id:156346)，使得该区域内所有点的 $\Gamma^k_{ij}$ 都恒等于零？

一个基本定理断言：**一个开集上存在所有[克里斯托费尔符号](@entry_id:159831)都为零的[坐标系](@entry_id:156346)的充要条件是，该开集上的黎曼曲率张量为零。**

黎曼曲率张量 $R^i{}_{jkl}$ 是由联络系数及其[一阶导数](@entry_id:749425)构造而成的张量：
$$
R^i{}_{jkl} = \partial_k \Gamma^i_{jl} - \partial_l \Gamma^i_{jk} + \Gamma^i_{mk}\Gamma^m_{jl} - \Gamma^i_{ml}\Gamma^m_{jk}
$$
由于 $R$ 是一个真正的张量，如果它在一个[坐标系](@entry_id:156346)中为零，那么它在所有[坐标系](@entry_id:156346)中都为零。一个[黎曼曲率张量](@entry_id:160189)处处为零的[流形](@entry_id:153038)被称为**平坦[流形](@entry_id:153038) (flat manifold)**。

以一个半径为 $R$ 的二维球面为例。在标准的球坐标 $(\theta, \phi)$下，我们可以计算出非零的[克里斯托费尔符号](@entry_id:159831)，例如 $\Gamma^\theta_{\phi\phi}=-\sin\theta\cos\theta$。更重要的是，利用这些符号可以算出球面的黎曼曲率张量分量不为零（例如，$R^\theta{}_{\phi\theta\phi} = \sin^2\theta$）。由于[曲率张量](@entry_id:181383)不为零，就从根本上排除了在球面上找到一个（哪怕是局部的）[坐标系](@entry_id:156346)使得所有 $\Gamma$ 符号都消失的可能性。这意味着球面的弯曲是内蕴的，无法通过选择一个“更好”的[坐标系](@entry_id:156346)来“抹平”。[@problem_id:1857047]

因此，克里斯托费尔符号本身是[坐标系](@entry_id:156346)和内蕴几何的混合体。而由它们构造出的黎曼曲率张量，则成功地剥离了[坐标系](@entry_id:156346)的效应，成为了衡量空间内蕴弯曲程度的纯粹几何量。

### [联络1-形式](@entry_id:275839)：[标架场](@entry_id:160577)下的观点

最后，值得一提的是联络系数的一种更抽象但更优雅的表述，即通过**[联络1-形式](@entry_id:275839) (connection 1-forms)**。考虑一个局部的切空间[标架场](@entry_id:160577) $\{e_a\}$（它不必是[坐标基](@entry_id:270149)矢，可以是任意一组[线性无关](@entry_id:148207)的向量场，例如一个正交归一标架）。联络算子 $\nabla$ 作用于标架中每个向量的结果，可以重新用这个标架展开：
$$
\nabla_X e_b = \omega^a{}_b(X) e_a
$$
对于每个固定的指标对 $(a,b)$，$\omega^a{}_b$ 是一个1-形式，它“吃掉”一个向量 $X$，然后给出一个实数（即 $\nabla_X e_b$ 在 $e_a$ 方向上的分量）。

当这个标架恰好是坐标标架 $e_i = \partial_i$ 时，我们可以将上述定义与[克里斯托费尔符号](@entry_id:159831)的定义进行比较。令 $X = \partial_i$：
$$
\nabla_{\partial_i} \partial_j = \omega^k{}_j(\partial_i) \partial_k
$$
而我们已知：
$$
\nabla_{\partial_i} \partial_j = \Gamma^k_{ij} \partial_k
$$
比较系数可知：
$$
\omega^k{}_j(\partial_i) = \Gamma^k_{ij}
$$
一个1-形式 $\omega$ 可以用其在对偶基 $dx^i$ 上的分量展开为 $\omega = \omega(\partial_i) dx^i$。因此，我们可以将[联络1-形式](@entry_id:275839) $\omega^k{}_j$ 写为：
$$
\omega^k{}_j = \Gamma^k_{ij} dx^i
$$
这个关系式建立了基于分量的[克里斯托费尔符号](@entry_id:159831)与基于[标架场](@entry_id:160577)的[联络1-形式](@entry_id:275839)之间的桥梁。后者在处理非坐标标架（在广义相对论中尤其常见）以及在E. Cartan的[移动标架](@entry_id:175562)法中扮演着核心角色。[@problem_id:2972217]