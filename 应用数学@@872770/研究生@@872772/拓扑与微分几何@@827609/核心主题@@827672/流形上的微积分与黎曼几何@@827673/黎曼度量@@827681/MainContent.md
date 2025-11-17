## 引言
在数学和物理学的广阔天地中，空间的概念无处不在。我们对平直的[欧几里得空间](@entry_id:138052)及其几何规律了如指掌，但在现实世界和现代科学理论中，我们遇到的空间往往是弯曲的——从地球的表面到爱因斯坦理论中由物质和能量塑造的时空。那么，我们如何在这些弯曲的空间中测量距离、角度和体积呢？这个根本性问题引出了[微分几何](@entry_id:145818)中最核心的概念之一：黎曼度量。它是一种强大的数学工具，为我们提供了在任意光滑流形上进行几何测量的“尺子”。本文旨在系统性地揭开黎曼度量的面纱，解决在非欧几里得空间中如何建立几何学这一知识缺口。

在接下来的内容中，我们将通过三个层次递进的章节来探索黎曼度量的世界。首先，在“原理与机制”一章中，我们将深入其数学核心，从形式化定义出发，理解度量如何催生出联络、[测地线](@entry_id:269969)和曲率等关键几何结构。接着，在“应用与交叉学科联系”部分，我们将走出纯粹数学的范畴，展示黎曼度量如何在广义相对论、[信息几何](@entry_id:141183)乃至计算科学等多个前沿领域中发挥其不可或缺的作用。最后，“动手实践”部分将提供具体的计算问题，帮助您将理论知识转化为解决实际问题的能力。通过这一旅程，您将不仅理解黎曼度量的定义，更能体会到它作为一种统一性语言，在描绘和理解宇宙的几何形态时所展现的深刻力量。

## 原理与机制

在介绍性章节之后，我们现在深入探讨黎曼度量的核心原理与机制。本章将从其严格的数学定义出发，阐明它如何成为测量弯曲空间中几何量的基本工具，并最终揭示度量如何内在地决定了[流形](@entry_id:153038)上的联络、[测地线](@entry_id:269969)和曲率等关键几何结构。

### 黎曼度量的定义与存在性

#### 形式化定义：切空间上的[内积](@entry_id:158127)族

一个[光滑流形](@entry_id:160799) $M$ 在每一点 $p$ 都拥有一个切空间 $T_pM$，这是一个[向量空间](@entry_id:151108)。黎曼度量的本质是在整个[流形](@entry_id:153038)上为每一个切[空间平滑](@entry_id:202768)地指定一个[内积](@entry_id:158127)。

更精确地说，一个**黎曼度量（Riemannian metric）** $g$ 是[流形](@entry_id:153038) $M$ 上的一个光滑的、对称的 $(0,2)$-[张量场](@entry_id:190170)，它在每一点 $p \in M$ 都诱导了一个正定的双线性形式 $g_p: T_pM \times T_pM \to \mathbb{R}$。让我们剖析这个定义 [@problem_id:3033278]：

1.  **双线性形式（Bilinear Form）**: 在每一点 $p$，对于切向量 $v, w, u \in T_pM$ 和标量 $a, b \in \mathbb{R}$，$g_p$ 满足[线性关系](@entry_id:267880) $g_p(av+bw, u) = a g_p(v, u) + b g_p(w, u)$ 和 $g_p(u, av+bw) = a g_p(u, v) + b g_p(u, w)$。
2.  **对称性（Symmetry）**: 对所有 $v, w \in T_pM$，都有 $g_p(v, w) = g_p(w, v)$。
3.  **光滑性（Smoothness）**: 当点 $p$ 在[流形](@entry_id:153038)上变化时，$g_p$ 的变化是光滑的。这意味着，对于任意两个光滑向量场 $X, Y$，函数 $p \mapsto g_p(X_p, Y_p)$ 是一个[光滑函数](@entry_id:267124)。
4.  **[正定性](@entry_id:149643)（Positive-Definiteness）**: 对于任意非零[切向量](@entry_id:265494) $v \in T_pM \setminus \{0\}$，都有 $g_p(v, v) > 0$。

**[正定性](@entry_id:149643)**是黎曼几何的基石。它保证了我们可以定义向量的长度（范数）为一个正实数 $\|v\|_p = \sqrt{g_p(v,v)}$，并且只有零向量的长度才为零。如果我们将此条件放宽为非退定（non-degenerate），即 $g_p(v, w) = 0$ 对所有 $w \in T_pM$ 成立的唯一条件是 $v=0$，我们就进入了**[伪黎曼度量](@entry_id:185204)（pseudo-Riemannian metric）**的领域。[伪黎曼度量](@entry_id:185204)在每个切空间上都有一个固定的符号 $(p,q)$。洛伦兹度量，作为广义相对论的数学基础，就是一个重要的[伪黎曼度量](@entry_id:185204)例子，其符号为 $(n-1, 1)$ 或 $(1, n-1)$。

#### [局部坐标](@entry_id:181200)表示与[正定性](@entry_id:149643)检验

在[局部坐标](@entry_id:181200)图 $(U, x^1, \dots, x^n)$ 中，[切空间](@entry_id:199137) $T_pM$ 有一组基底 $\{\partial_1, \dots, \partial_n\}$，其中 $\partial_i = \frac{\partial}{\partial x^i}$。度量张量 $g$ 可以由其在这些基底上的分量矩阵 $G$ 来表示，其元素为 $g_{ij}(p) = g_p(\partial_i, \partial_j)$。在这些坐标下，两个向量 $v = v^i \partial_i$ 和 $w = w^j \partial_j$ 的[内积](@entry_id:158127)为 $g(v,w) = g_{ij}v^i w^j$（这里使用了爱因斯坦求和约定）。度量本身则可以写作 $ds^2 = g_{ij} dx^i \otimes dx^j$。

判断一个给定的张量场 $g$ 是否构成黎曼度量，需要检验上述所有性质。光滑性和对称性通常能从其分量 $g_{ij}$ 的表达式中直接看出。关键且更微妙的检验在于正定性。对于一个 $n \times n$ 的[对称矩阵](@entry_id:143130) $G = (g_{ij})$，其为正定的充分必要条件是它的所有主子式（leading principal minors）都为正。即：
$$ \Delta_1 = g_{11} > 0, \quad \Delta_2 = \det \begin{pmatrix} g_{11} & g_{12} \\ g_{21} & g_{22} \end{pmatrix} > 0, \quad \dots, \quad \Delta_n = \det(G) > 0 $$

考虑一个位于上半平面 $M = \{(x, y) \in \mathbb{R}^2 \mid y > 0\}$ 上的[张量场](@entry_id:190170)，其分量矩阵为 [@problem_id:1660801]：
$$ G = \begin{pmatrix} y^2 & -xy \\ -xy & x^2 \end{pmatrix} $$
该张量的分量都是[光滑函数](@entry_id:267124)，且矩阵是对称的。然而，它的[行列式](@entry_id:142978) $\det(G) = (y^2)(x^2) - (-xy)^2 = x^2y^2 - x^2y^2 = 0$。由于[行列式](@entry_id:142978)为零，该矩阵不是正定的，而是奇异的（或称退化的）。因此，这个张量场 $g$ 不是一个黎曼度量。我们可以找到一个非[零向量](@entry_id:156189) $v = x \partial_x + y \partial_y$，使得 $g(v,v) = (y \cdot x - x \cdot y)^2 = 0$，这直接违反了[正定性](@entry_id:149643)条件。

#### [黎曼度量的存在性](@entry_id:190637)

一个自然而深刻的问题是：是否所有[光滑流形](@entry_id:160799)都容许一个黎曼度量？答案是肯定的，这保证了[黎曼几何](@entry_id:160508)具有广泛的适用性。这一结论的基石是**[单位分解](@entry_id:150115)（partition of unity）**的存在性。

一个[光滑流形](@entry_id:160799)若具备**[仿紧性](@entry_id:152096)（paracompactness）**，则对于其任意开覆盖，都存在一个从属于该覆盖的光滑单位分解。幸运的是，[微分几何](@entry_id:145818)中通常研究的[流形](@entry_id:153038)（豪斯多夫且[第二可数](@entry_id:151735)）都是仿紧的。

[单位分解](@entry_id:150115)的存在性允许我们将局部构造“粘合”成一个全局对象。构造一个黎曼度量的过程大致如下 [@problem_id:2975232]：
1.  [对流](@entry_id:141806)形 $M$，取一个开覆盖 $\{U_\alpha\}$，其中每个 $U_\alpha$ 都是一个[坐标邻域](@entry_id:276525)，[同胚](@entry_id:146933)于 $\mathbb{R}^n$ 中的一个开集。
2.  在每个 $U_\alpha$ 上，我们可以定义一个局部的黎曼度量 $g_\alpha$。最简单的方法是将在 $\mathbb{R}^n$ 中的标准[欧几里得度量](@entry_id:147197)通过[坐标映射](@entry_id:747874)[拉回](@entry_id:160816)到 $U_\alpha$ 上。
3.  取一个从属于开覆盖 $\{U_\alpha\}$ 的光滑[单位分解](@entry_id:150115) $\{\varphi_i\}$。这意味着每个 $\varphi_i$ 都是一个光滑函数 $\varphi_i: M \to [0,1]$，其支集 $\text{supp}(\varphi_i)$ 包含在某个 $U_{\alpha(i)}$ 中，且对所有 $p \in M$，$\sum_i \varphi_i(p) = 1$。
4.  全局的黎曼度量 $g$ 可以通过这些局部度量和单位分解的加权和来定义：
    $$ g = \sum_i \varphi_i g_{\alpha(i)} $$
由于[单位分解](@entry_id:150115)是局部有限的，在任何一[点的邻域](@entry_id:144055)内，这个和都只是有限项之和，因此 $g$ 是光滑的。易于验证，$g$ 是对称的，并且由于所有 $g_{\alpha(i)}$ 是正定的且 $\varphi_i \ge 0$（且在每一点至少有一个 $\varphi_i > 0$），$g$ 也是正定的。

这个强大的[构造性证明](@entry_id:157587)意味着，我们几乎总可以假设我们的[光滑流形](@entry_id:160799)已经配备了一个黎曼度量，从而可以利用它来探索[流形](@entry_id:153038)的几何性质。

### 度量的作用：测量几何

黎曼度量的首要作用是为[切空间](@entry_id:199137)提供了[内积](@entry_id:158127)，从而将欧几里得空间中的长度、角度和体积等基本概念推广到了一般的弯曲[流形](@entry_id:153038)上。

#### [曲线长度](@entry_id:191173)

一旦定义了切向量的长度，我们就可以通[过积分](@entry_id:753033)来定义一条可微曲线 $\gamma: [a, b] \to M$ 的长度 $L(\gamma)$。其思想是将曲线分割成无穷小的片段，每个片段的长度近似于其切向量的长度乘以一个无穷小的时间间隔 $dt$。这引出了弧长积分公式：
$$ L(\gamma) = \int_a^b \|\gamma'(t)\| dt = \int_a^b \sqrt{g_{\gamma(t)}(\gamma'(t), \gamma'(t))} \, dt $$
在[局部坐标](@entry_id:181200)中，如果 $\gamma(t) = (x^1(t), \dots, x^n(t))$，那么 $\gamma'(t) = \frac{dx^i}{dt}\partial_i$，公式变为：
$$ L(\gamma) = \int_a^b \sqrt{g_{ij}(\gamma(t)) \frac{dx^i}{dt} \frac{dx^j}{dt}} \, dt $$

让我们看一个具体的计算。考虑著名的**[庞加莱上半平面](@entry_id:264005)（Poincaré upper half-plane）** $\mathbb{H}^2 = \{ (x,y) \in \mathbb{R}^2 \mid y > 0 \}$，其度量为 $ds^2 = \frac{dx^2 + dy^2}{y^2}$。我们来计算连接点 $P_1 = (2, 2)$ 和 $P_2 = (2, 8)$ 的竖直直线段的长度 [@problem_id:1660826]。
我们可以将这条[曲线参数化](@entry_id:635915)为 $\gamma(t) = (2, t)$，其中 $t \in [2, 8]$。其[切向量](@entry_id:265494)为 $\gamma'(t) = (0, 1)$，即 $x'(t)=0, y'(t)=1$。代入弧长公式：
$$ L(\gamma) = \int_2^8 \frac{\sqrt{(x'(t))^2 + (y'(t))^2}}{y(t)} dt = \int_2^8 \frac{\sqrt{0^2 + 1^2}}{t} dt = \int_2^8 \frac{1}{t} dt $$
计算该积分得到：
$$ L(\gamma) = [\ln|t|]_2^8 = \ln(8) - \ln(2) = \ln\left(\frac{8}{2}\right) = \ln(4) $$
有趣的是，尽管在欧几里得平面上，从 $y=2$ 到 $y=8$ 的距离是 $6$，但在[双曲几何](@entry_id:158454)的庞加莱模型中，这段“看起来”等长的路径，其“真实”的几何长度却是 $\ln(4) \approx 1.386$。这生动地展示了度量如何重新定义了我们对距离的感知。

#### 面积与诱导度量

度量不仅定义了长度，还定义了面积和体积。在一个 $n$ 维[流形](@entry_id:153038)上，由度量 $g$ 诱导的**[体积元](@entry_id:267802)（volume form）**在[局部坐标](@entry_id:181200)中由下式给出：
$$ dV = \sqrt{\det(g_{ij})} \, dx^1 \wedge \dots \wedge dx^n $$
一个区域的体积就是在这个区域上对[体积元](@entry_id:267802)进行积分。

当一个[流形嵌入](@entry_id:159781)或[浸入](@entry_id:161534)到另一个更大的黎曼流形中时，它会自然地“继承”一个度量，这称为**诱导度量（induced metric）**。一个更普适的概念是**[拉回度量](@entry_id:161465)（pullback metric）**。若 $\Phi: N \to M$ 是一个[光滑映射](@entry_id:203730)，且 $(M, g)$ 是一个黎曼流形，则在 $N$ 上的[拉回度量](@entry_id:161465) $\Phi^*g$ 定义为：
$$ (\Phi^*g)_p(u, v) = g_{\Phi(p)}(d\Phi_p(u), d\Phi_p(v)) $$
其中 $p \in N$，$u, v \in T_p N$，而 $d\Phi_p: T_p N \to T_{\Phi(p)} M$ 是 $\Phi$ 在 $p$ 点的[微分](@entry_id:158718)（或称[推前映射](@entry_id:160933)）。

一个经典且极具启发性的例子是球极投影（stereographic projection）[@problem_id:1018350]。考虑从单位球面 $S^2 \subset \mathbb{R}^3$ 的北极 $N=(0,0,1)$ 到赤道平面 $Z=0$（等同于复平面 $\mathbb{C}$）的投影。这个投影的逆映射 $\Phi: \mathbb{C} \to S^2 \setminus \{N\}$ 将平面上的点 $(x,y)$ 映射到球面上的点 $(X,Y,Z)$。标准单位球面上的度量 $g_{S^2}$ 是从 $\mathbb{R}^3$ 的[欧几里得度量](@entry_id:147197) $dX^2+dY^2+dZ^2$ 诱导的。通过 $\Phi$ 将 $g_{S^2}$ [拉回](@entry_id:160816)到 $\mathbb{C}$ 上，经过计算可得诱导度量 $g_{\mathbb{C}} = \Phi^*g_{S^2}$ 为：
$$ ds^2 = \frac{4}{(1+x^2+y^2)^2}(dx^2+dy^2) $$
令 $r^2 = x^2+y^2$，度量矩阵为 $G = \frac{4}{(1+r^2)^2} \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$。其[行列式](@entry_id:142978)为 $\det(G) = \frac{16}{(1+r^2)^4}$。因此，平面上的[面积元](@entry_id:263205)为 $dA = \sqrt{\det(G)} \, dx dy = \frac{4}{(1+r^2)^2} \, dx dy$。
我们可以计算整个平面的总面积：
$$ \text{Area} = \int_{\mathbb{R}^2} \frac{4}{(1+x^2+y^2)^2} \, dx dy $$
切换到极坐标 $x=r\cos\theta, y=r\sin\theta, dx dy=rdrd\theta$，积分变为：
$$ \text{Area} = \int_0^{2\pi} \int_0^\infty \frac{4}{(1+r^2)^2} r \, dr d\theta = 2\pi \int_0^\infty \frac{4r}{(1+r^2)^2} dr = 8\pi \left[ -\frac{1}{2(1+r^2)} \right]_0^\infty = 4\pi $$
这个结果恰好是[单位球](@entry_id:142558)面的总面积！这表明球极投影是一个保角的映射，它以一种扭曲的方式将整个球面（除去一点）映射到了整个平面上，但总面积得以保持。

#### 等距：局部与全局

一个保持度量的映射称为**等距（isometry）**。更细致地区分，一个[光滑映射](@entry_id:203730) $F: (M_1, g_1) \to (M_2, g_2)$ 如果满足 $F^*g_2 = g_1$，则称其为**[局部等距](@entry_id:158618)（local isometry）**。这意味着它在无穷小的尺度上保持长度和角度。而**[全局等距](@entry_id:184658)（global isometry）**则是一个更强的概念，它要求保持任意两点之间的**[测地距离](@entry_id:159682)**（即连接两点的最短曲线的长度）。

一个[局部等距](@entry_id:158618)不一定是[全局等距](@entry_id:184658)。一个经典的例子是将一个无限长的欧几里得平面带 $S = \{ (u,v) \in \mathbb{R}^2 \mid -\pi R  u  \pi R \}$ 卷成一个半径为 $R$ 的无限长圆柱 $C \subset \mathbb{R}^3$ [@problem_id:1660822]。映射 $F(u,v) = (R \cos(u/R), R \sin(u/R), v)$ 将带子 $S$ 映射到圆柱 $C$ 上。可以计算出，这个映射的[拉回度量](@entry_id:161465)恰好是带子上的[欧几里得度量](@entry_id:147197) $du^2+dv^2$，因此 $F$ 是一个[局部等距](@entry_id:158618)。然而，它不是[全局等距](@entry_id:184658)。
考虑带子上的两个点 $p_1 = (\pi R - \epsilon, 0)$ 和 $p_2 = (-\pi R + \epsilon, 0)$，其中 $\epsilon$ 是一个小的正数。它们在带子中的欧几里得距离（也是[测地距离](@entry_id:159682)）是 $d_S(p_1, p_2) = 2\pi R - 2\epsilon$。然而，它们在圆柱上的像 $F(p_1)$ 和 $F(p_2)$ 非常接近，可以通过绕圆柱的“短路”到达。它们在圆柱上的[测地距离](@entry_id:159682)是 $d_C(F(p_1), F(p_2)) = 2\epsilon$。由于 $2\epsilon  2\pi R - 2\epsilon$，距离没有被保持。这个例子揭示了拓扑结构（如圆柱的“环绕”特性）如何影响全局距离，即使局部几何完全相同。

### 度量催生的几何结构

黎曼度量的意义远不止于测量。它是一切内在几何结构的“母亲”，唯一地决定了[流形](@entry_id:153038)上的导数（联络）、直线（[测地线](@entry_id:269969)）和弯曲程度（曲率）。

#### Levi-Civita 联络

在欧几里得空间中，我们可以直接对向量场进行[微分](@entry_id:158718)。但在弯曲[流形](@entry_id:153038)上，不同点的切空间是不同的，直接求导没有意义。我们需要一个**[仿射联络](@entry_id:160152)（affine connection）** $\nabla$ 来定义向量场沿另一个向量场方向的[协变导数](@entry_id:152476) $\nabla_X Y$。

**[黎曼几何基本定理](@entry_id:189185)（Fundamental Theorem of Riemannian Geometry）**指出：在任意一个[黎曼流形](@entry_id:261160) $(M, g)$ 上，存在唯一一个[仿射联络](@entry_id:160152) $\nabla$，它同时满足以下两个条件：
1.  **无挠性（Torsion-Free）**: 对任意向量场 $X, Y$，有 $\nabla_X Y - \nabla_Y X = [X,Y]$，其中 $[X,Y]$ 是李括号。
2.  **[度量兼容性](@entry_id:265910)（Metric-Compatible）**: 对任意向量场 $X, Y, Z$，有 $X(g(Y,Z)) = g(\nabla_X Y, Z) + g(Y, \nabla_X Z)$。这个性质也写作 $\nabla g = 0$，意味着度量张量在[协变导数](@entry_id:152476)下为零，即平行移动保持[内积](@entry_id:158127)。

这个唯一的联络被称为**Levi-Civita联络**或黎曼联络。它是黎曼流形上进行微积分运算的规范工具。

#### Christoffel 符号

在[局部坐标](@entry_id:181200)中，联络 $\nabla$ 的信息被编码在一组称为**[Christoffel符号](@entry_id:159831)（Christoffel symbols）**（第二类）的系数 $\Gamma^k_{ij}$ 中，它们定义了基[向量的[协变导](@entry_id:191566)数](@entry_id:152476)：$\nabla_{\partial_i} \partial_j = \Gamma^k_{ij} \partial_k$。

利用无挠性（$\Gamma^k_{ij} = \Gamma^k_{ji}$）和[度量兼容性](@entry_id:265910)，可以通过一个被称为“Koszul 技巧”的代数运算，导出 Christoffel 符号完全由度量张量及其[一阶导数](@entry_id:749425)决定的著名公式 [@problem_id:3033296]：
$$ \Gamma^k_{ij} = \frac{1}{2}g^{kl} \left( \frac{\partial g_{jl}}{\partial x^i} + \frac{\partial g_{il}}{\partial x^j} - \frac{\partial g_{ij}}{\partial x^l} \right) $$
其中 $g^{kl}$ 是度量矩阵 $(g_{ij})$ 的[逆矩阵](@entry_id:140380) $(g^{ij})$ 的分量。这个公式明确地展示了度量如何“生成”了联络。

例如，对于欧几里得平面 $\mathbb{R}^2$ 中的极坐标 $(r, \theta)$，度量为 $ds^2 = dr^2 + r^2 d\theta^2$。其度量矩阵为 $g_{ij} = \begin{pmatrix} 1  0 \\ 0  r^2 \end{pmatrix}$，[逆矩阵](@entry_id:140380)为 $g^{ij} = \begin{pmatrix} 1  0 \\ 0  1/r^2 \end{pmatrix}$。唯一的非零导数是 $\partial_r g_{\theta\theta} = 2r$。
利用上述公式，我们可以计算出非零的 Christoffel 符号 [@problem_id:3033296]：
$$ \Gamma^r_{\theta\theta} = \frac{1}{2}g^{rr}(\partial_\theta g_{\theta r} + \partial_\theta g_{r\theta} - \partial_r g_{\theta\theta}) = \frac{1}{2}(1)(0+0-2r) = -r $$
$$ \Gamma^\theta_{r\theta} = \Gamma^\theta_{\theta r} = \frac{1}{2}g^{\theta\theta}(\partial_r g_{\theta\theta} + \partial_\theta g_{r\theta} - \partial_\theta g_{r\theta}) = \frac{1}{2}\left(\frac{1}{r^2}\right)(2r) = \frac{1}{r} $$
这些符号的非零性反映了极[坐标系](@entry_id:156346)本身是“弯曲”的，即使它描述的是一个平直的空间。

#### [测地线](@entry_id:269969)

在[黎曼流形](@entry_id:261160)上，**[测地线](@entry_id:269969)（geodesic）**是[欧几里得空间](@entry_id:138052)中“直线”概念的推广。一条[测地线](@entry_id:269969)是其自身切向量被平行移动的曲线。用 Levi-Civita 联络来表达，即曲线 $\gamma(t)$ 满足方程 $\nabla_{\gamma'(t)} \gamma'(t) = 0$。

在[局部坐标](@entry_id:181200)中，这个定义展开为**测地线方程**，这是一组[二阶常微分方程](@entry_id:204212)：
$$ \frac{d^2x^k}{dt^2} + \Gamma^k_{ij} \frac{dx^i}{dt} \frac{dx^j}{dt} = 0 $$
[测地线](@entry_id:269969)是局部最短的路径。给定一点和该点的一个切向量，存在唯一一条以此为初始位置和初始速度的[测地线](@entry_id:269969)。

考虑一个一般的[旋转曲面](@entry_id:261378)，其度量为 $ds^2 = du^2 + f(u)^2 dv^2$，其中 $f(u)$ 是一个光滑正函数 [@problem_id:1018418]。由于度量不依赖于坐标 $v$，这体现了旋转对称性。根据诺特定理的思想，这种对称性导致了一个[守恒量](@entry_id:150267)。对于[测地线](@entry_id:269969) $\gamma(t) = (u(t), v(t))$，这个[守恒量](@entry_id:150267)是 Clairaut 常数 $C = f(u)^2 \frac{dv}{dt}$。利用这个[守恒量](@entry_id:150267)，我们可以将关于 $u(t)$ 的测地线方程解耦，得到：
$$ \frac{d^2u}{dt^2} = f(u)f'(u) \left(\frac{dv}{dt}\right)^2 = f(u)f'(u) \frac{C^2}{f(u)^4} = \frac{C^2 f'(u)}{f(u)^3} $$
这个方程描述了[测地线](@entry_id:269969)在“纬度”方向 $u$ 上的运动，完全由度量的函数 $f(u)$ 和运动的守恒量 $C$ 决定。

#### 曲率

曲率是衡量[流形](@entry_id:153038)弯曲程度的核心概念。它量化了平行移动对路径的依赖程度。**[黎曼曲率张量](@entry_id:160189)（Riemann curvature tensor）** $R(X,Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]} Z$ 捕捉了这种不[可交换性](@entry_id:263314)。

在二维情况下，曲率的所有信息都包含在一个标量函数——**[高斯曲率](@entry_id:149725)（Gaussian curvature）** $K$ 中。一个特别有用的[坐标系](@entry_id:156346)是**[等温坐标](@entry_id:272481)（isothermal coordinates）**，在这种[坐标系](@entry_id:156346)下，度量形式为 $ds^2 = \lambda(u,v)(du^2+dv^2)$。若令 $\lambda(u,v) = e^{2\sigma(u,v)}$，则[高斯曲率](@entry_id:149725)有一个简洁的表达式：
$$ K = -e^{-2\sigma} \left( \frac{\partial^2\sigma}{\partial u^2} + \frac{\partial^2\sigma}{\partial v^2} \right) = -e^{-2\sigma} \Delta \sigma $$
其中 $\Delta$ 是标准的欧几里得拉普拉斯算子。这个公式（Brioschi 公式的一种形式）将曲率与度量函数 $\sigma$ 的[二阶导数](@entry_id:144508)联系起来。

例如，若一个度量由 $\sigma(u,v) = \beta(u^4+v^4)$ 给出 [@problem_id:1018226]，我们可以计算其[高斯曲率](@entry_id:149725)。首先计算 $\sigma$ 的拉普拉斯量：
$$ \frac{\partial^2\sigma}{\partial u^2} = 12\beta u^2, \quad \frac{\partial^2\sigma}{\partial v^2} = 12\beta v^2 \quad \implies \quad \Delta\sigma = 12\beta(u^2+v^2) $$
代入[高斯曲率](@entry_id:149725)公式：
$$ K(u,v) = -e^{-2\beta(u^4+v^4)} \cdot 12\beta(u^2+v^2) = -12\beta(u^2+v^2) \exp\left(-2\beta(u^4+v^4)\right) $$
这表明曲率通常是[流形](@entry_id:153038)上一个变化的量，其值在不同点可能不同。

#### 何种联络是黎曼联络？

最后，我们回到一个更抽象的问题：给定一个[仿射联络](@entry_id:160152) $\nabla$，它在何种条件下会是某个黎曼度量的 Levi-Civita 联络？ [@problem_id:2996997]

根据[黎曼几何基本定理](@entry_id:189185)，$\nabla$ 必须是[无挠的](@entry_id:161664)。此外，必须存在一个黎曼度量 $g$ 使得 $\nabla g = 0$。这个[度量兼容条件](@entry_id:201846)是关键。它意味着沿任何闭环的平行移动必须保持度量 $g$ 在该点的[内积](@entry_id:158127)结构。这等价于说，联络 $\nabla$ 在任意一点 $p$ 的**[和乐群](@entry_id:191471)（holonomy group）** $\text{Hol}_p(\nabla)$ 必须是某个正定[内积](@entry_id:158127)的[等距群](@entry_id:161661)。换言之，$\text{Hol}_p(\nabla)$ 必须是 $GL(T_pM)$ 中某个紧[子群](@entry_id:146164)的[子群](@entry_id:146164)，可以共轭于[正交群](@entry_id:152531) $O(n)$ 的一个[子群](@entry_id:146164)。

这个观点为我们提供了判断的准则和障碍：
- **充分条件**：一个[无挠联络](@entry_id:181337) $\nabla$ 是黎曼联络，当且仅当它的[和乐群](@entry_id:191471)保持一个正定[内积](@entry_id:158127)。例如，如果[流形](@entry_id:153038)是单连通的且联络是平坦的（曲率为零），那么其[和乐群](@entry_id:191471)是[平凡群](@entry_id:151996) $\{\text{Id}\}$。平凡群显然保持任何[内积](@entry_id:158127)，因此这种联络总是某个（平坦的）黎曼度量的 Levi-Civita 联络。
- **障碍**：如果一个联络的[和乐群](@entry_id:191471)是非紧的，例如，它包含了[剪切变换](@entry_id:151272)，那么它就不可能保持任何[内积](@entry_id:158127)，从而不可能是任何黎曼度量的 Levi-Civita 联络。一个联络保持一个体积形式（意味着其和乐群在 $SL(n,\mathbb{R})$ 中）并不足以保证它是黎曼的，因为 $SL(n,\mathbb{R})$ 包含许多非紧[子群](@entry_id:146164)。

这一深刻的联系，将[代数结构](@entry_id:137052)（和乐群）与几何结构（度量）紧密地联系在一起，完美地体现了黎曼几何的内在和谐与强大。