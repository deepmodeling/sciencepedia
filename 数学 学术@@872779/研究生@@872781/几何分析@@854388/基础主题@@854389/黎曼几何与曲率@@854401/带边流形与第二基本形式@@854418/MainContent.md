## 引言
在微分几何的研究中，[带边流形](@entry_id:159788)提供了一个既丰富又复杂的舞台。与无边（闭合）[流形](@entry_id:153038)不同，其边界的存在引入了内蕴几何与外蕴几何之间深刻的相互作用，这支配了[流形](@entry_id:153038)上的许多分析和几何现象。理解边界如何嵌入到周围空间中，即其外蕴曲率，是揭示这些现象的关键。然而，如何精确地量化这种“弯曲”？这正是本篇文章旨在解决的核心问题。

本文将系统介绍并深入探讨[带边流形](@entry_id:159788)几何学中的核心工具——第二基本形式。我们将分三个章节展开：在“原理与机制”中，我们将建立第二基本形式的定义，探讨其与形状算子、主曲率的关系，并通过[高斯方程](@entry_id:192573)揭示[内蕴曲率](@entry_id:161701)与外蕴曲率的深刻联系。接着，在“应用与跨学科联系”中，我们将展示[第二基本形式](@entry_id:161454)如何在[几何分析](@entry_id:157700)的前沿领域，如[极小曲面](@entry_id:157732)、[几何流](@entry_id:195216)和[谱几何](@entry_id:186460)中，扮演至关重要的角色。最后，“动手实践”部分将通过具体问题，帮助读者巩固理论知识并应用于实践。

通过本文的学习，读者将全面掌握[第二基本形式](@entry_id:161454)的理论基础，并理解其作为连接局部几何与[全局分析](@entry_id:188294)的桥梁的强大功能。现在，让我们首先深入其基本原理与机制。

## 原理与机制

在研究带边[黎曼流形](@entry_id:261160)时，其几何分析的核心在于理解边界本身作为黎曼流形的内蕴几何，以及边界如何嵌入到周围[流形](@entry_id:153038)中的外蕴几何。这两者之间的相互作用支配了[流形](@entry_id:153038)上的许多分析和几何现象。本章旨在阐述量化边界曲率的核心工具——第二基本形式，并揭示其背后的基本原理和机制。

### 边界的内蕴几何

设 $(M^n, g)$ 是一个光滑的 $n$ 维[黎曼流形](@entry_id:261160)，其边界为 $\partial M$。边界 $\partial M$ 本身是一个光滑的 $(n-1)$ 维[流形](@entry_id:153038)。通过将度量张量 $g$ 限制在边界的[切丛](@entry_id:161294) $T\partial M$ 上，$\partial M$ 自然地继承了一个黎曼度量 $g_{\partial M}$。若 $\iota: \partial M \hookrightarrow M$ 是嵌入映射，则诱导度量由[拉回](@entry_id:160816)（pullback）定义：$g_{\partial M} = \iota^*g$。

为了具体理解诱导度量的计算，我们考虑一个标准例子。令 $M$ 为 $\mathbb{R}^{n+1}$ 中单位 $n$ 维球面 $S^n$ 的上半部分，$M = \{ x \in S^n : x_{n+1} \geq 0 \}$。其边界 $\partial M$ 是赤道，即 $\partial M = \{ x \in S^n : x_{n+1} = 0 \}$，它[等距同构](@entry_id:273188)于标准单位球面 $S^{n-1} \subset \mathbb{R}^n$。我们可以使用标准球坐标来参数化 $S^{n-1}$。给定笛卡尔坐标 $(x_1, \dots, x_n)$ 和球坐标 $(\alpha_1, \dots, \alpha_{n-1})$ 之间的映射 $\Phi$，诱导度量 $g_{\partial M}$ 的分量 $(g_{\partial M})_{jk}$ 可以通过计算[环境空间](@entry_id:184743)（这里是 $\mathbb{R}^n$）的[欧几里得度量](@entry_id:147197)在切向量 $\frac{\partial \Phi}{\partial \alpha_j}$ 和 $\frac{\partial \Phi}{\partial \alpha_k}$ 上的值来得到。通过直接计算，可以证明度量张量是对角的，其分量依赖于角度坐标。最终，我们得到 $S^{n-1}$ 上著名的标[准圆](@entry_id:175119)度量的表达式：
$$
g_{\partial M} = \sum_{j=1}^{n-1} \left( \prod_{k=1}^{j-1} \sin^2(\alpha_k) \right) (d\alpha_j)^2
$$
其中，当 $j=1$ 时，连乘积为空，约定为 $1$。这个计算明确展示了边界如何从环境[流形](@entry_id:153038)继承其作为[黎曼流形](@entry_id:261160)的所有[内蕴几何](@entry_id:158788)结构 [@problem_id:3032031]。

除了度量，定向[流形的边界](@entry_id:196014)还继承了一个自然定向。对于一个可定向的[带边流形](@entry_id:159788) $M$，其边界 $\partial M$ 的[诱导定向](@entry_id:634340)通常通过“外[法向量](@entry_id:264185)在前”的约定来定义。具体而言，如果 $\nu$ 是 $\partial M$ 上的外[单位法向量](@entry_id:178851)场，那么 $\partial M$ 在一点 $p$ 的切空间 $T_p\partial M$ 中的一个有序基 $(v_1, \dots, v_{n-1})$ 被认为是正定向的，当且仅当 $T_pM$ 中的有序基 $(\nu(p), v_1, \dots, v_{n-1})$ 是正定向的。

这个定义可以通过微分形式的语言来精确表述。若 $\Omega$ 是 $M$ 的体积形式，代表其定向，则 $\partial M$ 上的[诱导定向](@entry_id:634340)形式 $\omega$ 可以通过[内积](@entry_id:158127)运算得到：$\omega = i_\nu \Omega$。例如，考虑 $\mathbb{R}^n$ 中的单位球 $B^n = \{x \in \mathbb{R}^n : |x| \leq 1\}$。其边界为 $S^{n-1}$。在 $p \in S^{n-1}$ 处，外[单位法向量](@entry_id:178851)就是位置向量本身，即 $\nu(p) = p$。$\mathbb{R}^n$ 的标准定向由[体积形式](@entry_id:203000) $\Omega = dx^1 \wedge \dots \wedge dx^n$ 给出。诱导到 $S^{n-1}$ 上的定向形式 $\omega$ 就是[内积](@entry_id:158127) $i_\nu \Omega$ 在 $S^{n-1}$ 上的限制。经过计算可得：
$$
\omega = \sum_{j=1}^{n} (-1)^{j-1} x_j dx^1 \wedge \cdots \wedge \widehat{dx^j} \wedge \cdots \wedge dx^n
$$
这里 $\widehat{dx^j}$ 表示省略该项。这个形式在几何分析和拓扑学中极为重要，它是斯托克斯定理（Stokes' Theorem）的一般形式的基础 [@problem_id:3032047]。

### 外蕴曲率：形状算子与[第二基本形式](@entry_id:161454)

边界的内蕴几何描述了在边界“内部”进行的测量，例如[弧长](@entry_id:191173)和角度。然而，这并未捕捉到边界是如何在环境[流形](@entry_id:153038) $M$ 中弯曲的。这个概念被称为**外蕴曲率** (extrinsic curvature)。

量化外蕴曲率的关键在于考察[法向量场](@entry_id:268853) $\nu$ 如何随着沿边界的移动而变化。设 $\nabla$ 是 $M$ 上的列维-奇维塔联络（Levi-Civita connection）。对于一个[切向量](@entry_id:265494) $X \in T_p \partial M$，协变导数 $\nabla_X \nu$ 描述了 $\nu$ 沿 $X$ 方向的变化率。这个向量通常既有切向分量又有法向分量。由于 $\nu$ 是[单位法向量](@entry_id:178851)，即 $g(\nu, \nu) = 1$，我们有：
$$
0 = \nabla_X (g(\nu, \nu)) = 2g(\nabla_X \nu, \nu)
$$
这表明 $\nabla_X \nu$ 总是与 $\nu$ 正交，因此它是一个[切向量](@entry_id:265494)，$\nabla_X \nu \in T_p\partial M$。

这使得我们可以定义一个从 $T_p\partial M$到自身的线性映射，即**[形状算子](@entry_id:264703)**（shape operator），也称为**温加滕映射**（Weingarten map）。一个常见的定义（尤其是在欧氏空间背景下）是：
$$
S(X) = - \nabla_X \nu
$$
形状算子 $S: T_p\partial M \to T_p\partial M$ 捕捉了边界在每个切方向上的弯曲程度。它是一个[自伴算子](@entry_id:152188)，即关于诱导度量 $g_{\partial M}$ 是对称的：$g(S(X), Y) = g(X, S(Y))$。

与形状算子密切相关的是一个[对称双线性形式](@entry_id:148281)，称为**第二基本形式** (second fundamental form)，记为 $II$。它被定义为：
$$
II(X, Y) = g(S(X), Y)
$$
将 $S$ 的定义代入，我们得到 $II(X, Y) = -g(\nabla_X \nu, Y)$。

为了建立直观理解，我们再次考察单位球面 $S^{n-1}$ 作为 $\mathbb{R}^n$ 中单位球的边界。外[单位法向量](@entry_id:178851)为 $\nu(p) = p$。在[欧氏空间](@entry_id:138052)中，$\nabla_X Y$ 就是向量场 $Y$ 沿 $X$ 方向的方向导数。将 $\nu$ 延拓为 $\mathbb{R}^n$ 上的向量场 $\tilde{\nu}(q) = q$，我们计算 $\nabla_X \tilde{\nu}$。其结果就是向量 $X$ 本身。因此，在 $p \in S^{n-1}$ 上，$\nabla_X \nu = X$。根据定义，[形状算子](@entry_id:264703)为 $S(X) = -X$。这意味着形状算子是负[恒等映射](@entry_id:634191)。[第二基本形式](@entry_id:161454)则为：
$$
II(X, Y) = g(-X, Y) = -g(X, Y)
$$
这表明对于单位球面，其外蕴曲率在所有方向上都是均勻的，其大小由度量本身决定 [@problem_id:3032041]。

### 约定与[不变性](@entry_id:140168)

在处理[第二基本形式](@entry_id:161454)时，符号约定是一个微妙且至关重要的问题。文献中存在两种主要的定义：
1.  $II(X, Y) = -g(\nabla_X \nu, Y)$ (有时通过 $S(X) = \nabla_X \nu$ 定义)
2.  $II_{\text{alt}}(X, Y) = g(\nabla_X Y, \nu)$

这两种定义通过对恒等式 $g(Y, \nu) = 0$ 求导可以联系起来。利用度量与联络的相容性（$\nabla g = 0$），我们有：
$$
0 = \nabla_X(g(Y, \nu)) = g(\nabla_X Y, \nu) + g(Y, \nabla_X \nu)
$$
因此，$g(\nabla_X Y, \nu) = -g(Y, \nabla_X \nu) = -g(\nabla_X \nu, Y)$。这揭示了两种常见定义之间的关系。我们采用的定义是 $II(X, Y) = g(S(X), Y) = -g(\nabla_X \nu, Y)$。另一种定义是 $II_{\text{alt}}(X, Y) = g(\nabla_X Y, \nu)$。根据上述恒等式，这两种定义在我们的约定下是等价的（$II = II_{\text{alt}}$）。但如果采用 $II(X, Y) = g(\nabla_X\nu, Y)$ 的约定（即 $S(X)=\nabla_X\nu$），则 $II_{\text{alt}}(X, Y) = -II(X, Y)$。

另一个必须明确的约定是法向量的方向。我们可以选择**外[单位法向量](@entry_id:178851)** $\nu$ 或**内[单位法向量](@entry_id:178851)** $-\nu$。让我们探究这个选择如何影响相关几何量。

设 $\nu' = -\nu$。新的第二基本形式 $II'$ 为：
$$
II'(X, Y) = g(S'(X), Y) \quad \text{with} \quad S'(X) = -\nabla_X \nu' = -\nabla_X(-\nu) = \nabla_X \nu = -S(X)
$$
因此，$S' = -S$ 且 $II' = -II$。这意味着改变[法向量](@entry_id:264185)的方向会使[形状算子](@entry_id:264703)和[第二基本形式](@entry_id:161454)反号。

**主曲率** (principal curvatures) $\kappa_i$ 是形状算子 $S$ 的[特征值](@entry_id:154894)。由于 $S' = -S$，新主曲率 $\kappa'_i = -\kappa_i$。

**平均曲率** (mean curvature) $H$ 定义为形状算子的迹，$H = \text{tr}(S) = \sum_i \kappa_i$。因此，新的平均曲率 $H' = \text{tr}(S') = \text{tr}(-S) = -H$。

然而，**[平均曲率向量](@entry_id:199617)** (mean curvature vector) $\mathbf{H}$ 定义为 $\mathbf{H} = H\nu$。让我们看看它如何变化：
$$
\mathbf{H}' = H'\nu' = (-H)(-\nu) = H\nu = \mathbf{H}
$$
[平均曲率向量](@entry_id:199617)是**不变的**。这是一个重要的几何事实：[平均曲率向量](@entry_id:199617)是一个不依赖于[法向量](@entry_id:264185)方向选择的几何量，它描述了[曲面](@entry_id:267450)“想要”如何移动以减小其面积。相比之下，标量平均曲率 $H$ 的符号则依赖于约定 [@problem_id:3032044]。在阅读文献时，必须时刻注意作者采用的[法向量](@entry_id:264185)和[第二基本形式](@entry_id:161454)的定义。

### [主曲率](@entry_id:270598)与[内蕴曲率](@entry_id:161701)

[形状算子](@entry_id:264703) $S_p: T_p\partial M \to T_p\partial M$ 在每一点都是一个[自伴算子](@entry_id:152188)，因此它有一组实[特征值](@entry_id:154894) $\kappa_1, \dots, \kappa_{n-1}$，称为**主曲率**，以及一组对应的[正交特征向量](@entry_id:155522) $e_1, \dots, e_{n-1}$，称为**主方向**。这些量描述了边界在不同方向上的弯曲程度。[平均曲率](@entry_id:162147) $H = \sum \kappa_i$ 和**高斯-克罗内克曲率** $K_{ext} = \det(S) = \prod \kappa_i$ 是两个特别重要的[不变量](@entry_id:148850)。

对于我们之前研究的[单位球](@entry_id:142558)面 $S^{n-1} \subset \mathbb{R}^n$，我们发现 $S(X)=-X$。这意味着对于任何非零[切向量](@entry_id:265494) $X$，它都是一个[特征向量](@entry_id:151813)，对应的[特征值](@entry_id:154894)为 $-1$。因此，在任意一点，所有的主曲率都等于 $-1$。这样的点被称为**[脐点](@entry_id:260926)** (umbilic point)。球面上每一点都是[脐点](@entry_id:260926) [@problem_id:3032041]。

外蕴曲率（由[主曲率](@entry_id:270598) $\kappa_i$ 描述）与边界的[内蕴曲率](@entry_id:161701)（由黎曼曲率张量 $R^{\partial M}$ 描述）之间存在深刻的联系。这种联系由**[高斯方程](@entry_id:192573)** (Gauss equation) 给出。对于一个嵌入在欧氏空间 $\mathbb{R}^n$ 中的[超曲面](@entry_id:159491) $\partial M$，其环境空间是平坦的（$R^{\mathbb{R}^n}=0$），[高斯方程](@entry_id:192573)简化为：
$$
\langle R^{\partial M}(X,Y)Z, W \rangle = \langle II(X,W), II(Y,Z) \rangle - \langle II(X,Z), II(Y,W) \rangle
$$
这里 $\langle \cdot, \cdot \rangle$ 是诱导度量。使用 $II(X,Y) = \langle S(X),Y \rangle$，上式变为：
$$
\langle R^{\partial M}(X,Y)Z, W \rangle = \langle S(X), W \rangle \langle S(Y), Z \rangle - \langle S(X), Z \rangle \langle S(Y), W \rangle
$$
这个方程也被称为[高斯-科达齐方程](@entry_id:159376)组中的[高斯方程](@entry_id:192573)。它揭示了一个惊人的事实：超曲面的内蕴[黎曼曲率](@entry_id:635343)完全由其[第二基本形式](@entry_id:161454)（即外蕴曲率）决定。这就是高斯著名的*[绝妙定理](@entry_id:159067) (Theorema Egregium)* 的推广。

我们可以用这个方程来计算特定2-维平面（2-plane）的**截面曲率** (sectional curvature)。截面曲率 $K(\sigma)$ 是[内蕴曲率](@entry_id:161701)的一个完整描述。如果一个2-维平面 $\sigma$ 由一对正交单位[主方向](@entry_id:276187) $e_i, e_j$ 张成，那么其[截面曲率](@entry_id:159738)为：
$$
K(e_i, e_j) = \langle R^{\partial M}(e_i, e_j)e_j, e_i \rangle
$$
将 $X=W=e_i$ 和 $Y=Z=e_j$ 代入[高斯方程](@entry_id:192573)，并利用 $S(e_k) = \kappa_k e_k$ 以及 $\langle e_i, e_j \rangle = 0$ (因 $i \neq j$)，我们得到：
$$
K(e_i, e_j) = \langle S(e_i), e_i \rangle \langle S(e_j), e_j \rangle - \langle S(e_i), e_j \rangle^2 = (\kappa_i)(\kappa_j) - 0 = \kappa_i \kappa_j
$$
因此，由两个[主方向](@entry_id:276187)张成的平面的内蕴截面曲率等于相应[主曲率](@entry_id:270598)的乘积。这个简洁而深刻的公式是连接内蕴几何与外蕴几何的桥梁 [@problem_id:3032040]。

### 几何量在[局部坐标](@entry_id:181200)中的表示

为了在具体的分析问题（如[偏微分方程](@entry_id:141332)）中使用这些几何概念，我们需要在[局部坐标](@entry_id:181200)中表达它们。一个特别有用的[坐标系](@entry_id:156346)是**项圈坐标** (collar coordinates) 或**法向坐标** (normal coordinates)。在边界 $\partial M$ 的一个邻域内，我们可以建立一个[坐标系](@entry_id:156346) $(y^1, \dots, y^{n-1}, r)$，其中 $(y^i)$ 是 $\partial M$ 上的[局部坐标](@entry_id:181200)，$r$ 是到边界的有符号距离（例如，内[法线](@entry_id:167651)方向为正）。

在这种[坐标系](@entry_id:156346)下，度量张量 $g$ 具有一种特殊形式。如果 $r$ 是精确的距离函数，则 $\partial_r$ 是[单位法向量](@entry_id:178851)，且与 $\partial_i = \frac{\partial}{\partial y^i}$ 正交。度量可以写成 $g = dr^2 + g_r$，其中 $g_r$ 是一个依赖于 $r$ 的在 $\partial M$ 水平切片上的度量族。

在这种[坐标系](@entry_id:156346)中，环境[流形](@entry_id:153038) $M$ 的列维-奇维塔联络的克里斯托费尔符号（Christoffel symbols）$\Gamma^\alpha_{\beta\gamma}$ 与边界的几何量（如其自身的联络 $\nabla^{\partial}$ 和第二基本形式 $II$）之间存在直接关系。通过使用联络的科zul公式，在边界 $r=0$ 处可以推导出以下重要关系（这里我们采用 $II_{ij} = g(\nabla_{\partial_i} \partial_j, \nu)$ 和内法向量 $\nu = \partial_r$ 的约定）：
- $\Gamma^k_{ij}|_{r=0} = (\Gamma^\partial)^k_{ij}$：切向-切向分量的切向部分是边界内蕴联络的克里斯托费尔符号。
- $\Gamma^r_{ij}|_{r=0} = II_{ij}$：切向-切向分量的法向部分是第二基本形式的分量。
- $\Gamma^k_{ri}|_{r=0} = -g^{\partial kl}II_{li}$：法向-切向分量的切向部分由第二基本形式和边界度量决定。
- 许多其他分量为零，例如 $\Gamma^r_{ri}|_{r=0}=0$ 和 $\Gamma^k_{rr}|_{r=0}=0$。

这些公式是进行涉及边界的张量计算的基石，例如，在推导边界上几何量的演化方程时不可或缺 [@problem_id:3032043]。特别地，关系 $II_{ij} = \Gamma^r_{ij}|_{r=0}$ 可以进一步写为 $II_{ij} = -\frac{1}{2} \partial_r g_{ij}|_{r=0}$。这表明，第二基本形式本质上是边界上的度量张量 $g_{ij}$ 沿法向变化的速率。

### 应用与进阶机制

#### [符号距离函数](@entry_id:754834)

**[符号距离函数](@entry_id:754834)** (signed distance function) $\rho$ 是[几何分析](@entry_id:157700)中一个极其有力的工具。对于一个具有光滑边界 $\partial M$ 的区域 $M \subset \mathbb{R}^n$，$\rho(x)$ 定义为点 $x$ 到边界 $\partial M$ 的距离，并根据 $x$ 在 $M$ 内部还是外部赋予正负号。一个常见的约定是 $\rho  0$ 在 $M$ 内部，$\rho > 0$ 在 $M$ 外部，从而 $\rho=0$ 正是边界 $\partial M$。

在 $\partial M$ 的一个[管状邻域](@entry_id:269959)内，[符号距离函数](@entry_id:754834) $\rho$ 是光滑的，并且满足一个关键的[偏微分方程](@entry_id:141332)，即**程函方程** (Eikonal equation)：$|\nabla \rho| = 1$。这表明 $\nabla \rho$ 是一个[单位向量](@entry_id:165907)场。由于 $\rho$ 的[等值面](@entry_id:196027)就是与 $\partial M$平行的[曲面](@entry_id:267450)，$\nabla \rho$ 在每一点都垂直于该点所在的[等值面](@entry_id:196027)。特别地，在边界 $\partial M$ 上，$\nabla \rho$ 就是外[单位法向量](@entry_id:178851)场 $\nu$。

更进一步，我们可以考察 $\rho$ 的[二阶导数](@entry_id:144508)，即其**黑塞矩阵** (Hessian) $\nabla^2 \rho$。这是一个[对称双线性形式](@entry_id:148281)，定义为 $\nabla^2\rho(X, Y) = \langle \nabla_X (\nabla\rho), Y \rangle$。$\nabla^2 \rho$ 的[特征值](@entry_id:154894)揭示了边界的曲率信息。通过对程函方程 $|\nabla \rho|^2 = 1$ 求导，可以证明在边界上的任意一点 $p \in \partial M$：
- 对于法向量 $\nu$，$\nabla^2\rho(\nu, \cdot) = 0$。这意味着 $\nu$ 是黑塞矩阵的一个[特征向量](@entry_id:151813)，其[特征值](@entry_id:154894)为 $0$。
- 对于[切向量](@entry_id:265494) $X, Y \in T_p \partial M$，我们有 $\nabla^2\rho(X, Y) = \langle \nabla_X \nu, Y \rangle = -\langle S(X), Y \rangle = -II(X,Y)$（这里采用 $S(X) = -\nabla_X \nu$ 的约定）。

这意味着，在由主方向 $e_i$ 和法向量 $\nu$ 构成的标准正交基下，黑塞矩阵 $\nabla^2 \rho$ 是对角的。其[特征值](@entry_id:154894)恰好是 $(-\kappa_1, -\kappa_2, \dots, -\kappa_{n-1}, 0)$。这个优美的结果将一个分析对象（函数的[二阶导数](@entry_id:144508)）与一个纯粹的几何对象（边界的[主曲率](@entry_id:270598)）直接联系起来，在与曲率相关的[偏微分方程](@entry_id:141332)研究中扮演着核心角色 [@problem_id:3032057]。

#### 全测地边界与[流形](@entry_id:153038)加倍

第二基本形式为零的边界具有特殊的几何意义。如果 $II \equiv 0$，则边界被称为**全测地** (totally geodesic)。从 $II_{ij} \propto \partial_r g_{ij}|_{r=0}$ 的关系来看，这意味着度量张量在法向上的变化率在边界处为零。直观上，这样的边界是“平坦地”嵌入到环境[流形](@entry_id:153038)中的。例如，$\mathbb{R}^n$ 中的一个超平面就是[全测地的](@entry_id:183906)。

全测地边界的一个重要性质是，它们允许我们将[流形](@entry_id:153038)“无缝”地反射或加倍。考虑一个[带边流形](@entry_id:159788) $M = [0, \epsilon) \times N$，其度量为翘曲积形式 $g = dr^2 + \phi(r)^2 h$。我们可以通过将 $r$ 的范围扩展到 $(-\epsilon, \epsilon)$ 并通过偶延拓定义度量 $\tilde{g} = dr^2 + \phi(|r|)^2 h$ 来构造一个**加倍[流形](@entry_id:153038)** $\widetilde{M}$。

为了使 $\widetilde{M}$ 成为一个光滑的黎曼流形，度量张量 $\tilde{g}$ 的分量必须在 $r=0$ 处足够光滑。函数 $\phi(|r|)$ 的光滑性依赖于 $\phi$ 在 $r=0$ 处的导数。$\phi(|r|)$ 在 $r=0$ 处是 $C^1$ 的条件是 $\phi'(0) = 0$。我们之前在计算翘曲[积度量](@entry_id:637352)的[第二基本形式](@entry_id:161454)时发现，其表达式为 $II \propto \phi'(0)h$。因此，**加倍[流形](@entry_id:153038) $\widetilde{M}$ 的度量是 $C^1$（从而其联络是连续的，[曲率张量](@entry_id:181383)是定义良好的）的条件，恰好是边界 $\partial M$ 为[全测地的](@entry_id:183906)条件 $II=0$**。

在这种情况下，我们可以计算加倍[流形](@entry_id:153038)在接缝 $r=0$ 处的[截面曲率](@entry_id:159738)。对于由法向 $\partial_r$ 和一个切向单位向量张成的**径向平面**，其截面曲率为 $K_{\text{rad}}(0) = -\frac{\phi''(0)}{\phi(0)}$。对于由两个正交切向[单位向量](@entry_id:165907)张成的**切向平面**，其[截面曲率](@entry_id:159738)为 $K_{\text{tan}}(0) = \frac{\kappa}{\phi(0)^2}$，其中 $\kappa$ 是纤维[流形](@entry_id:153038) $N$ 的（常）[截面曲率](@entry_id:159738)。这个例子深刻地揭示了外蕴曲率（通过[第二基本形式](@entry_id:161454)）如何控制流形的局部和全局构造性质 [@problem_id:3032050]。