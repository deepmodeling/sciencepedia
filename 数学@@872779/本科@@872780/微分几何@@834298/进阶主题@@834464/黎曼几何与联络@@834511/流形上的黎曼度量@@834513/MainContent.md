## 引言
在探索光滑流形的抽象[世界时](@entry_id:275204)，我们面临一个核心挑战：如何在没有标准欧几里得结构的情况下进行几何测量？为了回答这个问题，微分几何引入了一个强大而基础的工具——**[黎曼度量](@entry_id:754359)（Riemannian metric）**。黎曼度量通过在[流形](@entry_id:153038)的每一点上定义一个[内积](@entry_id:158127)，赋予了这些弯曲空间以丰富的几何结构，使我们能够测量长度、角度、面积和体积。本文旨在全面介绍[黎曼度量](@entry_id:754359)的核心概念及其广泛应用，为读者提供一个从理论基础到实际应用的完整视角。

在“**原理与机制**”一章中，我们将深入[黎曼度量](@entry_id:754359)的定义，学习如何通过其分量矩阵进行计算，并掌握测量[曲线长度](@entry_id:191173)、区域面积以及定义[流形](@entry_id:153038)“直线”——[测地线](@entry_id:269969)的基本方法。接着，在“**应用与跨学科联系**”一章中，我们将见证黎曼度量如何作为一种统一的语言，在物理学（如广义相对论和经典力学）、统计学（[信息几何](@entry_id:141183)）和数据科学等多个领域中发挥关键作用。最后，“**动手实践**”部分将通过一系列精选的练习，帮助您巩固理论知识，将抽象概念应用于解决具体的几何和物理问题。

## 原理与机制

在引入了光滑流形作为我们研究几何的舞台之后，我们现在需要一个工具来在这个抽象的空间中进行测量。正如在[欧几里得空间](@entry_id:138052)中，我们可以测量向量的长度和它们之间的角度，我们希望在弯曲的[流形](@entry_id:153038)上也能进行同样的操作。这个工具就是**黎曼度量（Riemannian metric）**。黎曼度量在[流形](@entry_id:153038)的每一点的[切空间](@entry_id:199137)上都定义了一个[内积](@entry_id:158127)，从而赋予了[流形](@entry_id:153038)以几何结构，使其成为一个**黎曼流形（Riemannian manifold）**。本章将深入探讨黎曼度量的定义、其基本计算方法以及它如何使我们能够测量长度、面积，并定义[流形](@entry_id:153038)上的“直线”——[测地线](@entry_id:269969)。

### [黎曼度量](@entry_id:754359)的定义：几何的引擎

一个**[黎曼度量](@entry_id:754359)** $g$ 是在[光滑流形](@entry_id:160799) $M$ 上的一个光滑的对称 $(0,2)$-张量场，并且在每一点 $p \in M$ 都满足**[正定性](@entry_id:149643)（positive-definite）**。让我们来分解这个定义：

1.  **张量场**：$g$ 为[流形](@entry_id:153038)上的每个点 $p$ 指定了一个[双线性形式](@entry_id:746794) $g_p$，作用于该点的切空间 $T_pM$。这意味着 $g_p$ 是一个函数，它取两个[切向量](@entry_id:265494) $v, w \in T_pM$ 作为输入，并返回一个实数 $g_p(v, w)$。

2.  **[光滑性](@entry_id:634843)**：$g$ 是一个光滑的[张量场](@entry_id:190170)。在任何局部坐标系 $(x^1, \dots, x^n)$ 中，度量的分量 $g_{ij}(p) = g_p(\frac{\partial}{\partial x^i}, \frac{\partial}{\partial x^j})$ 都是关于点 $p$ 坐标的[光滑函数](@entry_id:267124)。

3.  **对称性**：对于任意[切向量](@entry_id:265494) $v, w \in T_pM$，都有 $g_p(v, w) = g_p(w, v)$。在[局部坐标](@entry_id:181200)中，这意味着度量分量矩阵 $(g_{ij})$ 是一个对称矩阵，即 $g_{ij} = g_{ji}$。

4.  **[正定性](@entry_id:149643)**：对于任意非零[切向量](@entry_id:265494) $v \in T_pM$，都有 $g_p(v, v) > 0$。这是最关键的属性，它保证了长度的定义是正的。

在[局部坐标](@entry_id:181200)中，这三个核心属性可以方便地通过度量分量矩阵 $G = (g_{ij})$ 来检验。一个 $(0,2)$-[张量场](@entry_id:190170) $g$ 是一个黎曼度量，当且仅当在[流形](@entry_id:153038)上的每一个点，其分量矩阵 $G$ 都是一个光滑、对称且正定的矩阵。

一个[对称矩阵](@entry_id:143130)是正定的，一个充分必要条件是它的所有主子式（leading principal minors）都为正。对于一个 $n \times n$ 矩阵 $G$，这意味着[行列式](@entry_id:142978) $\det(G_k) > 0$ 对所有 $k=1, \dots, n$ 成立，其中 $G_k$ 是 $G$ 的左上角 $k \times k$ 子矩阵。特别地，对于一个 $2 \times 2$ 矩阵，正定性要求 $g_{11} > 0$ 且 $\det(G) = g_{11}g_{22} - g_{12}^2 > 0$。

让我们通过一个例子来阐明这一点。考虑在 $\mathbb{R}^2$ 上定义的张量场 $g = \sin(x) \, dx \otimes dx + dy \otimes dy$。在标准坐标 $(x,y)$ 下，其分量矩阵为：
$$
[g_{ij}] = \begin{pmatrix} \sin(x)  0 \\ 0  1 \end{pmatrix}
$$
这个矩阵的各分量是光滑的，并且它是对称的。为了使其成为一个黎曼度量，它必须在每一点都是正定的。对于一个对角矩阵，正定性要求所有对角元素都为正。因此，我们需要 $\sin(x) > 0$ 并且 $1 > 0$。第二个条件总是成立，所以 $g$ 构成一个[黎曼度量](@entry_id:754359)的区域是所有满足 $\sin(x) > 0$ 的点 $(x,y)$ 的集合。在 $\sin(x) \le 0$ 的区域，[正定性](@entry_id:149643)条件失效，因此 $g$ 在那里不是一个[黎曼度量](@entry_id:754359) [@problem_id:1660812]。

正定性条件的失败可能更加微妙。考虑在上半平面 $M = \{(x, y) \in \mathbb{R}^2 \mid y > 0\}$ 上定义的[张量场](@entry_id:190170)，其矩阵为：
$$
G = \begin{pmatrix} y^2  -xy \\ -xy  x^2 \end{pmatrix}
$$
各分量 $g_{ij}$ 是光滑的多项式，且矩阵是对称的。我们来检查[正定性](@entry_id:149643)。第一个主子式是 $g_{11} = y^2$。由于我们处于上半平面，$y > 0$，所以 $y^2 > 0$。然而，第二个主子式，即[矩阵的行列式](@entry_id:148198)，是：
$$
\det(G) = (y^2)(x^2) - (-xy)(-xy) = x^2y^2 - x^2y^2 = 0
$$
由于[行列式](@entry_id:142978)在 $M$ 上的每一点都为零，该矩阵不是正定的，而是**半正定（positive semi-definite）**或**退化（degenerate）**的。这意味着存在非[零向量](@entry_id:156189) $v$，使得 $g(v,v)=0$。例如，取向量 $v = x \frac{\partial}{\partial x} + y \frac{\partial}{\partial y}$，我们有：
$$
g(v,v) = y^2(x^2) - 2xy(x)(y) + x^2(y^2) = x^2y^2 - 2x^2y^2 + x^2y^2 = 0
$$
因为存在可以获得零“长度”的非[零向量](@entry_id:156189)，这个张量场 $g$ 在 $M$ 的任何地方都不能定义一个[黎曼度量](@entry_id:754359) [@problem_id:1660801]。

### 度量作为计算工具

一旦我们有了一个黎曼度量，我们就可以开始进行计算。最基本的计算单元是**[线元](@entry_id:196833)（line element）** $ds^2$，它是在物理和工程学中一个历史悠久且直观的概念。线元表示一个[无穷小位移](@entry_id:202209)向量 $d\mathbf{x} = (dx^1, \dots, dx^n)$ 的平方长度：
$$
ds^2 = g_{ij} \, dx^i dx^j
$$
（这里使用了爱因斯坦求和约定，即对重复的上下标求和）。这个表达式非常有用，因为它直接给出了度量张量的分量。例如，在一个[三维流形](@entry_id:193484)上，如果[线元](@entry_id:196833)为：
$$
ds^2 = d\rho^2 + \sin^2(\rho) d\theta^2 + \sin^2(\rho)\sin^2(\theta)d\phi^2
$$
通过比较，我们可以直接读出坐标 $(\rho, \theta, \phi)$ 下的度量矩阵。这是一个对角矩阵：
$$
(g_{ij}) = \begin{pmatrix} 1  0  0 \\ 0  \sin^2(\rho)  0 \\ 0  0  \sin^2(\rho)\sin^2(\theta) \end{pmatrix}
$$
度量张量的一个重要相关对象是它的逆。**逆度量张量（inverse metric tensor）** $(g^{ij})$ 定义为矩阵 $(g_{ij})$ 的逆矩阵，即 $g^{ik}g_{kj} = \delta^i_j$，其中 $\delta^i_j$ 是克罗内克符号。对于对角度量，计算逆矩阵非常简单，只需将对角线上的每个元素取倒数即可。对于上述例子，逆度量矩阵为 [@problem_id:1660805]：
$$
(g^{ij}) = \begin{pmatrix} 1  0  0 \\ 0  \frac{1}{\sin^2(\rho)}  0 \\ 0  0  \frac{1}{\sin^2(\rho)\sin^2(\theta)} \end{pmatrix}
$$
逆度量张量在提升张量指标和定义梯度等操作中起着核心作用。

有了度量分量，我们就可以计算向量的**[内积](@entry_id:158127)（inner product）**。如果 $V = V^i \frac{\partial}{\partial x^i}$ 和 $W = W^j \frac{\partial}{\partial x^j}$ 是两个向量场，它们的[内积](@entry_id:158127)就是：
$$
g(V, W) = g_{ij} V^i W^j
$$
例如，在 $\mathbb{R}^2$ 上有一个度量 $g = 2 \, du \otimes du + \frac{1}{2} \, du \otimes dv + \frac{1}{2} \, dv \otimes du + 3 \, dv \otimes dv$，其分量矩阵为 $[g_{ij}] = \begin{pmatrix} 2  1/2 \\ 1/2  3 \end{pmatrix}$。对于向量场 $V = \frac{\partial}{\partial u} - 2\frac{\partial}{\partial v}$ 和 $W = 3\frac{\partial}{\partial u} + \frac{\partial}{\partial v}$，其分量分别为 $V = (1, -2)$ 和 $W = (3, 1)$。它们的[内积](@entry_id:158127)计算如下 [@problem_id:1660802]：
$$
g(V,W) = \sum_{i,j=1}^2 g_{ij}V^{i}W^{j} = g_{11}V^1W^1 + g_{12}V^1W^2 + g_{21}V^2W^1 + g_{22}V^2W^2
$$
$$
g(V,W) = 2(1)(3) + \frac{1}{2}(1)(1) + \frac{1}{2}(-2)(3) + 3(-2)(1) = 6 + \frac{1}{2} - 3 - 6 = -\frac{5}{2}
$$
一个向量场 $V$ 的**范数（norm）**或**长度（length）**则自然地定义为 $|V|_g = \sqrt{g(V,V)}$。

### [向量与余向量](@entry_id:180712)：[音乐同构](@entry_id:199976)

黎曼度量在切空间 $T_pM$ 和其对偶空间——[余切空间](@entry_id:270516) $T_p^*M$（1-形式的空间）之间建立了一个自然的、典范的同构。这个同构被称为**[音乐同构](@entry_id:199976)（musical isomorphisms）**，因为它们的符号 `♭` (flat) 和 `♯` (sharp) 让人联想到乐谱。

**降号映射 (Flat map)** $V \mapsto V^\flat$ 将一个向量场 $V$ 转换为一个 [1-形式](@entry_id:270392)（或称[余向量](@entry_id:157727)场）$V^\flat$。这个 [1-形式](@entry_id:270392)的定义是：对于任意向量场 $W$，它作用于 $W$ 的结果等于 $V$ 和 $W$ 的[内积](@entry_id:158127)。
$$
V^\flat(W) = g(V, W)
$$
在[局部坐标](@entry_id:181200)中，如果 $V$ 的分量是 $V^j$，那么其对偶的 1-形式 $\omega = V^\flat$ 的分量 $\omega_i$ 就是：
$$
\omega_i = g_{ij}V^j
$$
这个操作有效地用度量张量“降低”了向量的指标。

例如，考虑 $\mathbb{R}^2$ 上的度量 $g = \cosh^2(y) (dx \otimes dx) + (dy \otimes dy)$。度量矩阵是对角的，$g_{xx} = \cosh^2(y)$，$g_{yy} = 1$。让我们找到向量场 $V = \frac{\partial}{\partial x}$ 的对偶 [1-形式](@entry_id:270392) $\omega$。 $V$ 的分量是 $V^x = 1, V^y = 0$。$\omega = \omega_x dx + \omega_y dy$ 的分量计算如下 [@problem_id:1660790]：
$$
\omega_x = g_{xx}V^x + g_{xy}V^y = \cosh^2(y) \cdot 1 + 0 \cdot 0 = \cosh^2(y)
$$
$$
\omega_y = g_{yx}V^x + g_{yy}V^y = 0 \cdot 1 + 1 \cdot 0 = 0
$$
因此，对偶 [1-形式](@entry_id:270392)是 $\omega = \cosh^2(y) dx$。

**升号映射 (Sharp map)** $\omega \mapsto \omega^\sharp$ 是其逆过程，它使用逆度量张量 $g^{ij}$ 将一个 [1-形式](@entry_id:270392) $\omega$ 转换回一个向量场 $\omega^\sharp$：$(\omega^\sharp)^i = g^{ij}\omega_j$。这个操作“提升”了 1-形式的指标。

### 测量几何量

黎曼度量的真正威力在于它能够通[过积分](@entry_id:753033)来定义全局的几何量，例如曲线的长度和区域的面积。

#### 曲线的长度

给定一条[参数化](@entry_id:272587)曲线 $\gamma: [a, b] \to M$，它的**长度（length）** $L(\gamma)$ 是对其速度向量 $\gamma'(t)$ 的范数沿曲线的积分：
$$
L(\gamma) = \int_a^b |\gamma'(t)|_g \, dt = \int_a^b \sqrt{g_{\gamma(t)}(\gamma'(t), \gamma'(t))} \, dt
$$
这个定义推广了欧几里得空间中我们熟悉的概念。

考虑这样一个例子：在[上半平面](@entry_id:199119) $M = \{(x, y) \in \mathbb{R}^2 \mid y > 0\}$ 上，我们不使用标准的[欧几里得度量](@entry_id:147197) $g = dx^2 + dy^2$，而是使用一个**共形相关（conformally related）**的度量 $\tilde{g} = \frac{1}{y^2} g = \frac{dx^2 + dy^2}{y^2}$。这个 $\tilde{g}$ 就是著名的**庞加莱度量（Poincaré metric）**，它定义了双曲几何的模型。让我们计算一条垂直线段 $\gamma(t) = (c, t)$ 从 $t=t_0$到 $t=t_1$ 的长度（其中 $c$ 是常数）。

首先，计算速度向量：$\gamma'(t) = (0, 1)$。然后，在度量 $\tilde{g}$ 下计算其范数的平方：
$$
\tilde{g}_{\gamma(t)}(\gamma'(t), \gamma'(t)) = \frac{1}{y(t)^2} (0^2 + 1^2) = \frac{1}{t^2}
$$
于是，曲线的长度为 [@problem_id:1660808]：
$$
L_{\tilde{g}}(\gamma) = \int_{t_0}^{t_1} \sqrt{\frac{1}{t^2}} \, dt = \int_{t_0}^{t_1} \frac{1}{t} \, dt = [\ln t]_{t_0}^{t_1} = \ln(t_1) - \ln(t_0) = \ln\left(\frac{t_1}{t_0}\right)
$$
这个结果揭示了[双曲几何](@entry_id:158454)的一个反直觉特性：在庞加莱度量下，越靠近 $x$ 轴（即 $y \to 0$），距离被拉伸得越长。

#### 面积与体积

同样，度量也定义了[流形](@entry_id:153038)上的**[面积元](@entry_id:263205)（area element）**或**[体积元](@entry_id:267802)（volume element）**。在 $n$ 维[流形](@entry_id:153038)的[局部坐标](@entry_id:181200) $(x^1, \dots, x^n)$ 中，[体积元](@entry_id:267802)由下式给出：
$$
dV_g = \sqrt{\det(g_{ij})} \, dx^1 \wedge \dots \wedge dx^n
$$
这里的 $\sqrt{\det(g_{ij})}$ 因子可以被理解为从欧几里得坐标体积 $dx^1 \dots dx^n$ 到[流形](@entry_id:153038)上真实几何体积的局部缩放因子。

例如，考虑一个由[参数化](@entry_id:272587) $\mathbf{x}(u, v) = (u \cos v, u \sin v, v)$ 给出的[曲面](@entry_id:267450)（这是一个**螺（helicoid）**）。这个[曲面](@entry_id:267450)上的度量 $g$ 是从 $\mathbb{R}^3$ 的标准[欧几里得度量](@entry_id:147197)中**诱导（induced）**出来的。它的分量可以通过[切向量](@entry_id:265494)的[点积](@entry_id:149019)计算得到：
$$
\mathbf{x}_u = (\cos v, \sin v, 0), \quad \mathbf{x}_v = (-u \sin v, u \cos v, 1)
$$
度量分量为：
$$
g_{uu} = \langle \mathbf{x}_u, \mathbf{x}_u \rangle = 1
$$
$$
g_{uv} = \langle \mathbf{x}_u, \mathbf{x}_v \rangle = 0
$$
$$
g_{vv} = \langle \mathbf{x}_v, \mathbf{x}_v \rangle = u^2\sin^2v + u^2\cos^2v + 1 = u^2 + 1
$$
度量矩阵为 $[g_{ij}] = \begin{pmatrix} 1  0 \\ 0  1+u^2 \end{pmatrix}$。其[行列式](@entry_id:142978)为 $\det(g) = 1+u^2$。因此，面积元中的缩放因子为 $\sqrt{\det(g)} = \sqrt{1+u^2}$，[面积元](@entry_id:263205)本身为 $dA_g = \sqrt{1+u^2} \, du \wedge dv$ [@problem_id:1660818]。

### 运动与结构：[测地线](@entry_id:269969)与完备性

有了测量距离的能力，我们自然会问：[流形](@entry_id:153038)上“最直”的路径是什么？在欧几里得空间中，它们是直线。在[黎曼流形](@entry_id:261160)上，这些路径被称为**[测地线](@entry_id:269969)（geodesics）**。

#### [测地线](@entry_id:269969)

一条[测地线](@entry_id:269969) $\gamma(t)$ 是一条“加速度为零”的路径。更准确地说，它的[切向量](@entry_id:265494)（速度向量）$\gamma'(t)$ 沿着自身的[方向导数](@entry_id:189133)为零，即它是**自平行的（auto-parallel）**。在[局部坐标](@entry_id:181200) $(x^k)$ 中，这个条件可以表示为一组[二阶常微分方程](@entry_id:204212)，即**测地线方程（geodesic equation）**：
$$
\frac{d^2x^k}{dt^2} + \sum_{i,j=1}^n \Gamma^k_{ij} \frac{dx^i}{dt} \frac{dx^j}{dt} = 0 \quad \text{for each } k=1, \dots, n.
$$
这里的 $\Gamma^k_{ij}$ 是**克里斯托费尔符号（Christoffel symbols）**，它们由度量张量 $g_{ij}$ 及其[一阶导数](@entry_id:749425)计算得出。这些符号编码了[坐标系](@entry_id:156346)如何随位置变化的信息，从而反映了[流形](@entry_id:153038)的曲率。

一个特别简单但重要的情况是，如果存在一个[坐标系](@entry_id:156346)，使得度量分量 $g_{ij}$ 都是常数，那么所有的克里斯托费尔符号在该[坐标系](@entry_id:156346)中都为零。此时，测地线方程简化为：
$$
\frac{d^2x^k}{dt^2} = 0
$$
这意味着[测地线](@entry_id:269969)是在这些特殊坐标下参数呈仿射[线性关系](@entry_id:267880)的路径，即 $x^k(t) = a^k t + b^k$。

一个很好的例子是半径为 $R$ 的圆柱面 $M = S^1 \times \mathbb{R}$。使用坐标 $(\theta, z)$，其度量为 $ds^2 = R^2 d\theta^2 + dz^2$。度量分量 $g_{\theta\theta} = R^2$ 和 $g_{zz} = 1$ 都是常数，因此所有 $\Gamma^k_{ij}$ 都为零。测地线方程就是 $\theta''(t)=0$ 和 $z''(t)=0$。其通解为 $\theta(t) = at+b$ 和 $z(t) = ct+d$。这描述了圆柱面上的螺旋线、水平圆周和垂直直线 [@problem_id:1660775]。

#### [测地完备性](@entry_id:160280)

一个自然的问题是：沿着一条[测地线](@entry_id:269969)，我们是否可以永远走下去？如果一个黎曼流形上的任何[测地线](@entry_id:269969)都可以被扩展到定义在整个实数轴 $\mathbb{R}$ 上，那么这个[流形](@entry_id:153038)就被称为**测地完备的（geodesically complete）**。直观地说，这意味着你不能通过沿着一条“直线”行走而在有限的时间内“掉出”[流形](@entry_id:153038)。

[欧几里得空间](@entry_id:138052) $\mathbb{R}^n$ 是测地完备的。然而，即使从 $\mathbb{R}^n$ 中移去一个点，也可能破坏其完备性。考虑[流形](@entry_id:153038) $M = \mathbb{R}^3 \setminus \{\mathbf{0}\}$，即移除了原点的三维[欧几里得空间](@entry_id:138052)，其度量是标准的[欧几里得度量](@entry_id:147197)。在这个[流形](@entry_id:153038)中，[测地线](@entry_id:269969)仍然是直线段。现在，考虑从点 $p_0 = (3, -4, 12)$ 出发，沿着指向原点的方向发射一束粒子。这条路径是一条[测地线](@entry_id:269969)。它的速度为 $v_0$。该粒子到达原点所需的时间 $t_{exit}$ 可以通过计算得到：
$$
t_{exit} = \frac{\|p_0\|}{\|v_0\|}
$$
例如，如果 $\|p_0\| = \sqrt{3^2 + (-4)^2 + 12^2} = 13$米，而[粒子速度](@entry_id:196946)大小为 $\|v_0\| = 26$米/秒，则 $t_{exit} = 13/26 = 0.5$ 秒。由于原点 $\mathbf{0}$ 不在[流形](@entry_id:153038) $M$ 中，这条[测地线](@entry_id:269969)在有限时间 $t_{exit}$ 后就离开了[流形](@entry_id:153038)。因此，$M = \mathbb{R}^3 \setminus \{\mathbf{0}\}$ 不是一个测地完备的[流形](@entry_id:153038) [@problem_id:1660804]。

#### 等距

我们何时认为两个[黎曼流形](@entry_id:261160) $(M_1, g_1)$ 和 $(M_2, g_2)$ 在几何上是“相同的”？这个概念由**等距（isometry）**来描述。

一个**[局部等距](@entry_id:158618)（local isometry）**是一个[光滑映射](@entry_id:203730) $F: M_1 \to M_2$，它保持度量结构。技术上，这意味着 $F$ 的[拉回](@entry_id:160816)（pullback）作用于 $g_2$ 等于 $g_1$，即 $F^*g_2 = g_1$。这等价于说 $F$ 在每一点的[微分](@entry_id:158718) $dF_p: T_pM_1 \to T_{F(p)}M_2$ 都保持[内积](@entry_id:158127)。

一个**[全局等距](@entry_id:184658)（global isometry）**则是一个更强的概念。它是一个保持任意两点之间**[测地距离](@entry_id:159682)**的映射。[测地距离](@entry_id:159682)是连接两点的所有曲线长度的下确界。

一个[全局等距](@entry_id:184658)必然是[局部等距](@entry_id:158618)，但反之不成立。考虑从一个开的长带 $S = \{ (u,v) \in \mathbb{R}^2 \mid -\pi R  u  \pi R \}$（度量为标准[欧几里得度量](@entry_id:147197) $g_S = du^2 + dv^2$）到一个半径为 $R$ 的无限圆柱面 $C$（度量 $g_C$ 为诱导度量）的映射 $F(u,v) = (R \cos(u/R), R \sin(u/R), v)$。这个映射直观上就是将长带“卷起来”形成圆柱。

我们可以通过计算来验证这是否是一个[局部等距](@entry_id:158618)。计算表明 $F^*g_C = du^2 + dv^2 = g_S$，所以 $F$ 确实是一个[局部等距](@entry_id:158618)。然而，它不是[全局等距](@entry_id:184658)。考虑长带中两个快要到边界的点，例如 $p_1 = (\pi R - \epsilon, 0)$ 和 $p_2 = (-\pi R + \epsilon, 0)$。它们在长带中的距离（也是[测地距离](@entry_id:159682)）是 $d_S(p_1, p_2) = 2\pi R - 2\epsilon$。然而，它们在圆柱面上的像点 $F(p_1)$ 和 $F(p_2)$ 非常接近，可以通过“绕到后面”的短[路径连接](@entry_id:149343)。它们在圆柱面上的[测地距离](@entry_id:159682)是 $d_C(F(p_1), F(p_2)) = 2\epsilon$。由于 $2\epsilon \neq 2\pi R - 2\epsilon$，距离没有被保持，因此 $F$ 不是一个[全局等距](@entry_id:184658) [@problem_id:1660822]。这个例子优美地展示了局部几何性质和[全局几何](@entry_id:197506)性质之间的区别。