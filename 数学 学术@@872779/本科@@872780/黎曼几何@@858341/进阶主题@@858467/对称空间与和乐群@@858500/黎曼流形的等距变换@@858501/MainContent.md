## 引言
在探索几何世界时，一个基本问题油然而生：我们如何判断两个空间在几何上是“相同”的？对于[黎曼流形](@entry_id:261160)，其丰富的结构由度量所赋予，这个问题的答案便是“[等距同构](@entry_id:273188)”——一种不仅保持拓扑结构，更严格保持所有几何量（如长度、角度和曲率）的映射。本文旨在系统地阐述黎曼流形上的[等距同构](@entry_id:273188)理论，弥合几何直觉与严格数学定义之间的鸿沟。

本文将引导读者深入理解这一核心概念。在第一章 **原理和机制** 中，我们将从基本定义出发，探讨[等距同构](@entry_id:273188)的等价刻画、[局部坐标](@entry_id:181200)表示，并引入其[代数结构](@entry_id:137052)——[等距同构](@entry_id:273188)群，以及其无穷小对应物——[Killing向量场](@entry_id:161770)。随后，在第二章 **应用与跨学科联系** 中，我们将展示这些理论如何应用于物理学中以揭示守恒律，如何帮助我们分类和理解高度对称的齐性与对称空间，并作为构造新[流形](@entry_id:153038)的强大工具。最后，通过第三章的 **动手实践**，读者将有机会通过解决具体问题，将理论知识转化为解决实际几何问题的能力。通过这一系列的学习，我们将揭示[等距同构](@entry_id:273188)是如何成为连接几何、代数、拓扑与物理学的关键桥梁。

## 原理和机制

在研究[黎曼流形](@entry_id:261160)的几何结构时，一个核心问题是：我们何时可以认为两个黎曼流形是“相同”的？“相同”的严格数学概念便是 **[等距同构](@entry_id:273188) (isometry)**。一个[等距同构](@entry_id:273188)不仅在拓扑上是等价的（即一个[微分同胚](@entry_id:147249)），而且还必须保持黎曼度量所赋予的整个几何结构。本章将深入探讨[等距同构](@entry_id:273188)的定义、其对几何性质的影响、由[等距同构](@entry_id:273188)构成的群的结构，以及其无穷小对应物——[Killing向量场](@entry_id:161770)。

### [等距同构](@entry_id:273188)的定义与几何内涵

从最根本的层面看，几何学研究的是长度、角度和曲率等概念。一个[黎曼度量](@entry_id:754359) $g$ 在[流形](@entry_id:153038) $M$ 的每一点 $p$ 的[切空间](@entry_id:199137) $T_pM$ 上都定义了一个[内积](@entry_id:158127)，正是这个[内积](@entry_id:158127)让我们能够在无穷小的尺度上测量这些量。因此，两个黎曼流形之间的保度量映射，自然应该是在每一点上都保持这种[内积](@entry_id:158127)结构的映射。

**定义 ([等距同构](@entry_id:273188))** 令 $(M, g)$ 和 $(N, h)$ 为两个黎曼流形。一个微分同胚 $f: M \to N$ 如果满足 $f^*h = g$，则称之为一个 **[等距同构](@entry_id:273188)**。

这里的关键条件是[拉回度量](@entry_id:161465) $f^*h$ 等于 $g$。[拉回](@entry_id:160816)张量 $f^*h$ 是一个在 $M$ 上的 $(0,2)$-张量场，其定义方式恰恰体现了保持[内积](@entry_id:158127)的思想。对于 $M$ 上的任意一点 $p$ 和任意[切向量](@entry_id:265494) $u, v \in T_pM$，[拉回度量](@entry_id:161465)的定义为：
$$
(f^*h)_p(u, v) := h_{f(p)}(df_p(u), df_p(v))
$$
其中 $df_p: T_pM \to T_{f(p)}N$ 是 $f$ 在点 $p$ 的[微分](@entry_id:158718)（或称切映射）。因此，$f^*h = g$ 的条件逐点展开就是：
$$
g_p(u, v) = h_{f(p)}(df_p(u), df_p(v)) \quad \text{对于所有 } p \in M \text{ 和 } u, v \in T_pM
$$
这个等式是[等距同构](@entry_id:273188)的基石，它告诉我们，在点 $p$ 处用度量 $g$ 测量的两个[切向量](@entry_id:265494) $u$ 和 $v$ 的[内积](@entry_id:158127)，等于它们在 $f$ 的[微分](@entry_id:158718)作用下得到的像 $df_p(u)$ 和 $df_p(v)$ 在点 $f(p)$ 处用度量 $h$ 测量的[内积](@entry_id:158127)。换言之，$f$ 的[微分](@entry_id:158718) $df_p$ 是一个从[内积空间](@entry_id:271570) $(T_pM, g_p)$ 到 $(T_{f(p)}N, h_{f(p)})$ 的线性等距映射 [@problem_id:3054262]。

这一基本定义直接导致了几个等价的几何刻画：

1.  **保持切向量的长度和角度**：向量的长度和向量间的夹角都是由[内积](@entry_id:158127)定义的。向量 $u \in T_pM$ 的长度 $\|u\|_g$ 定义为 $\sqrt{g_p(u, u)}$。两个非[零向量](@entry_id:156189) $u, v$ 之间的夹角 $\angle_g(u, v)$ 由 $\cos(\angle_g(u, v)) = \frac{g_p(u, v)}{\|u\|_g \|v\|_g}$ 决定。从[等距同构](@entry_id:273188)的基本条件出发，取 $u=v$，我们立刻得到 $g_p(u, u) = h_{f(p)}(df_p(u), df_p(u))$，即 $\|u\|_g^2 = \|df_p(u)\|_h^2$，所以长度被保持。进而，对于任意非零向量 $u,v$，由于[内积](@entry_id:158127)和长度都被保持，它们之间的夹角也必然被保持 [@problem_id:3054264]。

    反过来，如果一个[微分同胚](@entry_id:147249)保持了所有[切向量](@entry_id:265494)的长度和夹角，那么它也必然保持[内积](@entry_id:158127)（因为 $g_p(u,v)=\|u\|_{g}\\|v\|_{g}\cos(\angle_{g}(u,v))$），从而构成一个[等距同构](@entry_id:273188)。更有力的是，我们甚至不需要同时假设长度和角度都被保持。**[极化恒等式](@entry_id:271819) (polarization identity)**，例如 $g_p(u,v) = \frac{1}{2}(\|u+v\|_g^2 - \|u\|_g^2 - \|v\|_g^2)$，表明[内积](@entry_id:158127)完全由长度（范数）决定。因此，一个微分同胚是[等距同构](@entry_id:273188)，当且仅当它保持所有切向量的长度。即，对于所有 $p \in M$ 和 $u \in T_pM$，都有 $\|u\|_g = \|df_p(u)\|_h$ [@problem_id:3054264]。

2.  **保持曲线的长度**：曲线的长度是通过对曲线上每一点的切向量长度进行积分得到的。设 $\gamma: [a,b] \to M$是一条光滑曲线，其在 $(M,g)$ 中的长度为 $L_g(\gamma) = \int_a^b \|\gamma'(t)\|_g dt$。在[等距同构](@entry_id:273188) $f$ 的作用下，它变为一条新曲线 $f \circ \gamma$ in $N$。根据链式法则，新曲线的[切向量](@entry_id:265494)为 $(f \circ \gamma)'(t) = df_{\gamma(t)}(\gamma'(t))$。由于[等距同构](@entry_id:273188)保持[切向量](@entry_id:265494)的长度，我们有 $\|\gamma'(t)\|_g = \|df_{\gamma(t)}(\gamma'(t))\|_h$。因此，积分值也必然相等：
    $$
    L_g(\gamma) = \int_a^b \|\gamma'(t)\|_g dt = \int_a^b \|(f \circ \gamma)'(t)\|_h dt = L_h(f \circ \gamma)
    $$
    所以，[等距同构](@entry_id:273188)保持所有曲线的长度。事实上，这也是一个等价定义：任何保持由度量诱导的距离函数（即连接两点的所有曲线长度的[下确界](@entry_id:140118)）的映射都是[等距同构](@entry_id:273188)（这是[Myers-Steenrod定理](@entry_id:158086)的一部分）[@problem_id:3054262]。

3.  **[等距同构](@entry_id:273188)的逆**：如果 $f: (M,g) \to (N,h)$ 是一个[等距同构](@entry_id:273188)，那么它的逆映射 $f^{-1}: (N,h) \to (M,g)$ 也是一个[等距同构](@entry_id:273188)。这可以从 $f^*h = g$ 出发，通过在等式两边应用 $(f^{-1})^*$ 来证明，利用[拉回](@entry_id:160816)算子的[函子性](@entry_id:150069) $(f^{-1})^* \circ f^* = (f \circ f^{-1})^* = \text{id}^*$，可以得到 $(f^{-1})^*g=h$ [@problem_id:3054262]。

### [等距同构](@entry_id:273188)的[局部坐标](@entry_id:181200)表示

为了更具体地理解[等距同构](@entry_id:273188)的条件，我们可以在[局部坐标](@entry_id:181200)中表达它。设 $(x^1, \dots, x^n)$ 是 $M$ 上的[局部坐标](@entry_id:181200)，$(y^1, \dots, y^n)$ 是 $N$ 上的[局部坐标](@entry_id:181200)。映射 $f$ 在这些坐标下表示为 $y^\alpha = f^\alpha(x^1, \dots, x^n)$。度量张量 $g$ 和 $h$ 的分量分别为 $g_{ij}$ 和 $h_{\alpha\beta}$。

[拉回度量](@entry_id:161465) $(f^*h)$ 的分量 $(f^*h)_{ij}$ 可以通过计算它在[基向量](@entry_id:199546)场 $\frac{\partial}{\partial x^i}$ 和 $\frac{\partial}{\partial x^j}$ 上的作用得到：
$$
(f^*h)_{ij} = h\left(df\left(\frac{\partial}{\partial x^i}\right), df\left(\frac{\partial}{\partial x^j}\right)\right) = h\left(\sum_\alpha \frac{\partial f^\alpha}{\partial x^i} \frac{\partial}{\partial y^\alpha}, \sum_\beta \frac{\partial f^\beta}{\partial x^j} \frac{\partial}{\partial y^\beta}\right)
$$
利用度量的[双线性](@entry_id:146819)和 $h(\frac{\partial}{\partial y^\alpha}, \frac{\partial}{\partial y^\beta}) = h_{\alpha\beta}$，我们得到：
$$
(f^*h)_{ij}(x) = \sum_{\alpha, \beta} h_{\alpha\beta}(f(x)) \frac{\partial f^\alpha}{\partial x^i}(x) \frac{\partial f^\beta}{\partial x^j}(x)
$$
因此，[等距同构](@entry_id:273188)的条件 $g = f^*h$ 在[局部坐标](@entry_id:181200)中写为：
$$
g_{ij}(x) = \sum_{\alpha, \beta} h_{\alpha\beta}(f(x)) \frac{\partial f^\alpha}{\partial x^i}(x) \frac{\partial f^\beta}{\partial x^j}(x)
$$
这个方程描述了度量分量如何通过 $f$ 的雅可比矩阵 $J^\alpha_i = \frac{\partial f^\alpha}{\partial x^i}$ 联系起来。我们可以将此写成矩阵形式：$G(x) = J(x)^T H(f(x)) J(x)$，其中 $G$ 和 $H$ 分别是 $g$ 和 $h$ 的度量矩阵。

这个表达式在特殊[坐标系](@entry_id:156346)下会变得特别简洁。例如，如果我们选择在 $p_0 \in M$ 点的 **[测地法坐标](@entry_id:162016)系 (geodesic normal coordinates)**，那么在该点有 $g_{ij}(p_0) = \delta_{ij}$（克罗内克符号）。同样，在 $f(p_0)$ 点选择[测地法坐标](@entry_id:162016)系，有 $h_{\alpha\beta}(f(p_0)) = \delta_{\alpha\beta}$。在 $p_0$ 点，[等距同构](@entry_id:273188)条件简化为：
$$
\delta_{ij} = \sum_{\alpha} \frac{\partial f^\alpha}{\partial x^i}(p_0) \frac{\partial f^\alpha}{\partial x^j}(p_0)
$$
这正是[雅可比矩阵](@entry_id:264467) $J(p_0)$ 的转置乘以其自身等于单位矩阵的条件：$J(p_0)^T J(p_0) = I$。这意味着雅可比矩阵 $J(p_0)$ 必须是一个 **[正交矩阵](@entry_id:169220) (orthogonal matrix)** [@problem_id:3054242]。

[正交矩阵的行列式](@entry_id:137174)值为 $+1$ 或 $-1$。这一事实对于定向[流形](@entry_id:153038)具有重要意义。在连通的[黎曼流形](@entry_id:261160) $M$ 上，对于一个[等距同构](@entry_id:273188) $f: M \to M$，函数 $p \mapsto \det(df_p)$ 是一个从 $M$ 到[离散集](@entry_id:146023)合 $\{+1, -1\}$ 的[连续函数](@entry_id:137361)。由于[连通空间](@entry_id:156017)在[连续映射](@entry_id:153855)下的像是连通的，所以这个函数必须是常数。这意味着一个[等距同构](@entry_id:273188)要么在每一点都保持定向（此时 $\det(df_p)=+1$），要么在每一点都反转定向（此时 $\det(df_p)=-1$）。它不可能在某些点保持定向而在另一些点反转定向 [@problem_id:3054261]。

### 内蕴性质与外蕴性质

[等距同构](@entry_id:273188)的核心意义在于它保持了[流形](@entry_id:153038)的所有 **内蕴 (intrinsic)** 几何性质，即那些仅由[黎曼度量](@entry_id:754359)本身决定的性质。如果一个量可以在不知道[流形](@entry_id:153038)如何嵌入到更高维空间的情况下，仅通过在[流形](@entry_id:153038)上进行测量（即使用度量 $g$）来计算，那么它就是内蕴的。

以下是一些重要的内蕴性质，它们都在[等距同构](@entry_id:273188)下保持不变 [@problem_id:3054251]：
- **[曲线长度](@entry_id:191173)、向量夹角、区域面积**：这些是度量的直接后果。
- **[Levi-Civita联络](@entry_id:161107)**：由度量唯一确定的无挠率、保度量的联络。[等距同构](@entry_id:273188) $f$ 保持联络，意味着 $df(\nabla_X Y) = \nabla_{df(X)} df(Y)$。
- **[测地线](@entry_id:269969) (Geodesics)**：作为满足 $\nabla_{\dot{\gamma}}\dot{\gamma}=0$ 的曲线，其定义依赖于联络，因此是内蕴的。[等距同构](@entry_id:273188)将[测地线](@entry_id:269969)映射到[测地线](@entry_id:269969)。
- **[黎曼曲率张量](@entry_id:160189)**：由联络的交换子定义，完全是内蕴的。
- **[截面曲率](@entry_id:159738) (Sectional Curvature)**：对于给定的二维切平面，[截面曲率](@entry_id:159738)由[黎曼曲率张量](@entry_id:160189)和度量决定。[等距同构](@entry_id:273188) $f$ 满足 $K_M(p, \sigma) = K_N(f(p), df_p(\sigma))$，其中 $\sigma$ 是 $T_pM$ 中的一个二维平面。这是高斯“[绝妙定理](@entry_id:159067) (Theorema Egregium)”的推广 [@problem_id:3054293]。
- **Ricci曲率和数量曲率 (Scalar Curvature)**：它们是黎曼曲率张量的迹，因此也是内蕴的。

如果两个黎曼流形的[截面曲率](@entry_id:159738)函数不同，那么它们就不可能是[等距同构](@entry_id:273188)的。这为我们提供了一个强有力的工具来区分不同的黎曼流形。

与内蕴性质相对的是 **外蕴 (extrinsic)** 性质，它们依赖于[流形](@entry_id:153038)如何被嵌入到某个周围空间中（例如，嵌入到[欧几里得空间](@entry_id:138052) $\mathbb{R}^3$ 中）。一个经典的例子是[曲面](@entry_id:267450)的 **[主曲率](@entry_id:270598) (principal curvatures)**，它们是形算子 (shape operator) 的[特征值](@entry_id:154894)，而形算子描述了[法向量](@entry_id:264185)如何随着[切向量](@entry_id:265494)方向的变化而变化。

一个绝佳的例子是平面与圆柱面之间的关系。我们可以将平面上的一个矩形 $S_1 = \{ (x,y,0) \in \mathbb{R}^3 \}$ 卷成一个圆柱面 $S_2 = \{ (\cos x, \sin x, y) \in \mathbb{R}^3 \}$。这个映射 $F(x,y,0) = (\cos x, \sin x, y)$ 是一个 **[局部等距](@entry_id:158618)同构 (local isometry)**，因为它保持了[第一基本形式](@entry_id:274022)（诱导度量）。平面和圆柱面都是“平坦的”，因为它们的 **高斯曲率** (Gaussian curvature) 处处为零，这是一个内蕴性质。然而，圆柱面的主曲率是一个为 $1/R$（其中$R$是半径），另一个为 $0$；而平面的两个主曲率都为 $0$。由于主曲率不同，这两个[曲面](@entry_id:267450)作为 $\mathbb{R}^3$中的[子流形](@entry_id:159439)是不同的，但从其内蕴几何的角度看，它们是局部相同的 [@problem_id:3054251]。

这个例子也提醒我们，并非所有保持某些几何特征的映射都是[等距同构](@entry_id:273188)。例如，一个 **伸缩变换 (homothety)** $g' = c^2 g$（$c$ 为常数）会保持 Levi-Civita 联络不变，因此它将[测地线](@entry_id:269969)映射到[测地线](@entry_id:269969)（作为点集）。但如果 $c \neq 1$，它会改变所有曲线的长度，因此不是[等距同构](@entry_id:273188) [@problem_id:3054277]。

### [等距同构](@entry_id:273188)群及其结构

给定一个[黎曼流形](@entry_id:261160) $(M, g)$，所有从 $M$ 到其自身的[等距同构](@entry_id:273188)形成一个群，称为 $(M,g)$ 的 **[等距同构](@entry_id:273188)群 (isometry group)**，记作 $\mathrm{Isom}(M,g)$。群运算是映射的复合。单位元是恒等映射，每个元素的逆是其逆映射。这个群捕获了[流形](@entry_id:153038)的对称性。

关于[等距同构](@entry_id:273188)群的一个里程碑式的结果是 **Myers-Steenrod 定理**。该定理指出，对于任意连通黎曼流形 $(M,g)$，其[等距同构](@entry_id:273188)群 $\mathrm{Isom}(M,g)$（被赋予[紧致开拓扑](@entry_id:153876)）是一个有限维的 **[李群](@entry_id:137659) (Lie group)**，并且其在 $M$ 上的作用 $(f, p) \mapsto f(p)$ 是光滑的 [@problem_id:3054278]。这个定理意义非凡，它将一个纯粹的几何对称性问题（保度量映射）与一个丰富的代数和拓扑对象（李群）联系起来。

对于[流形](@entry_id:153038)上的某一点 $p \in M$，我们可以考虑所有保持该点不变的[等距同构](@entry_id:273188)，它们构成 $\mathrm{Isom}(M,g)$ 的一个[子群](@entry_id:146164)，称为 $p$ 点的 **[稳定子群](@entry_id:137216) (stabilizer subgroup)** 或 **[迷向子群](@entry_id:200360) (isotropy subgroup)**，记作 $\mathrm{Stab}(p)$。
$$
\mathrm{Stab}(p) = \{ f \in \mathrm{Isom}(M,g) \mid f(p) = p \}
$$
对于任意 $f \in \mathrm{Stab}(p)$，其[微分](@entry_id:158718) $df_p$ 是一个从 $T_pM$到自身的线性等距映射，即 $df_p \in O(T_pM, g_p)$，其中 $O(T_pM, g_p)$ 是切空间上[内积](@entry_id:158127) $g_p$ 的[正交群](@entry_id:152531)。这定义了一个 **[迷向表示](@entry_id:184529) (isotropy representation)**：
$$
\rho: \mathrm{Stab}(p) \to O(T_pM, g_p), \quad \rho(f) = df_p
$$
这个表示是一个[群同态](@entry_id:140603)，并且是 **[单射](@entry_id:183792) (injective)** 的。[单射性](@entry_id:147722)的证明非常巧妙：如果一个[等距同构](@entry_id:273188) $f$ 满足 $f(p)=p$ 和 $df_p = \mathrm{id}_{T_pM}$（即 $f$ 在核中），那么它必须是整个[流形](@entry_id:153038)上的恒等映射。这是因为 $f$ 保持[测地线](@entry_id:269969)和它们的初始速度，所以它在 $p$ 的一个法[坐标邻域](@entry_id:276525)内是[恒等映射](@entry_id:634191)。由于 $f$ 的[不动点](@entry_id:156394)集既是开集也是[闭集](@entry_id:136446)，而在连通[流形](@entry_id:153038)中，唯一非空的开[闭子集](@entry_id:155133)是[流形](@entry_id:153038)本身，所以 $f$ 在整个 $M$ 上都是[恒等映射](@entry_id:634191) [@problem_id:3054280]。这个结论意味着一个[等距同构](@entry_id:273188)完全由它在一个点上的作用以及在该点切空间上的作用所决定。

### [无穷小等距](@entry_id:634668)同构：Killing 向量场

[李群](@entry_id:137659)的研究通常与其李代数（其无穷小生成元的空间）密切相关。[等距同构](@entry_id:273188)群 $\mathrm{Isom}(M,g)$ 也不例外。$\mathrm{Isom}(M,g)$ 中的[单参数子群](@entry_id:181957)对应于[流形](@entry_id:153038)上的连续对称性。这些[连续对称性](@entry_id:137257)的无穷小生成元是一种特殊的向量场，称为 **Killing 向量场 (Killing vector field)**。

一个向量场 $X$ 是 Killing 向量场，如果它的局部流 $\Phi_t$（对于所有 $t$）由[等距同构](@entry_id:273188)组成。这等价于说，沿着向量场 $X$ 的方向拖动度量 $g$ 时，度量保持不变。这个概念被精确地表述为度量 $g$ 沿 $X$ 的 **李导数 (Lie derivative)** 为零：
$$
\mathcal{L}_X g = 0
$$
利用 Levi-Civita 联络 $\nabla$，这个条件可以被改写为一个更实用的形式。对于任意向量场 $Y, Z$，我们有：
$$
(\mathcal{L}_X g)(Y,Z) = g(\nabla_Y X, Z) + g(Y, \nabla_Z X) = 0
$$
在[局部坐标](@entry_id:181200)中，设 $X$ 的分量为 $X^i$，其对应的协变分量为 $X_j = g_{ji}X^i$。上述方程变成了著名的 **Killing 方程**：
$$
\nabla_i X_j + \nabla_j X_i = 0
$$
其中 $\nabla_i X_j$ 是协变导数 [@problem_id:3054291]。Killing 向量场的集合构成了[等距同构](@entry_id:273188)群 $\mathrm{Isom}(M,g)$ 对应的[李代数](@entry_id:137954)。

例如，在欧几里得平面 $(\mathbb{R}^2, dx^2 + dy^2)$ 中，Levi-Civita联络的系数（Christoffel 符号）全为零，[协变导数](@entry_id:152476)就是普通偏导数。
- 向量场 $X = -y\frac{\partial}{\partial x} + x\frac{\partial}{\partial y}$ 生成绕原点的旋转。它的协变分量是 $X_1 = -y, X_2 = x$。我们有 $\partial_1 X_1 + \partial_1 X_1 = 0$，$\partial_2 X_2 + \partial_2 X_2 = 0$，以及 $\partial_1 X_2 + \partial_2 X_1 = \frac{\partial x}{\partial x} + \frac{\partial (-y)}{\partial y} = 1 - 1 = 0$。Killing 方程成立，所以它是一个 Killing 向量场。
- 向量场 $X = x\frac{\partial}{\partial x} + y\frac{\partial}{\partial y}$ 生成沿径向的伸缩变换。其协变分量为 $X_1 = x, X_2 = y$。我们有 $\partial_1 X_1 + \partial_1 X_1 = 2\frac{\partial x}{\partial x} = 2 \neq 0$。它不是 Killing 向量场，这与伸缩变换不是[等距同构](@entry_id:273188)的事实相符 [@problem_id:3054291]。

### [等距同构](@entry_id:273188)与覆盖空间

[等距同构](@entry_id:273188)的概念与拓扑学中的覆盖空间理论也有深刻的联系。一个 **黎曼覆盖 (Riemannian covering)** 是一个[覆盖映射](@entry_id:169347) $p: (\tilde{M}, \tilde{g}) \to (M,g)$，同时它也是一个[局部等距](@entry_id:158618)同构。这意味着 $\tilde{M}$ 的度量 $\tilde{g}$ 是 $M$ 的度量 $g$ 通过 $p$ [拉回](@entry_id:160816)到 $\tilde{M}$ 上的结果，即 $\tilde{g} = p^*g$。

一个基本定理指出，如果 $p: \tilde{M} \to M$ 是一个连通[完备黎曼流形](@entry_id:182954)之间的满射[局部等距](@entry_id:158618)同构，那么 $p$ 实际上就是一个黎曼[覆盖映射](@entry_id:169347) [@problem_id:3054247]。

对于一个黎曼覆盖 $p: \tilde{M} \to M$，其 **[Deck变换群](@entry_id:153627)** $\mathrm{Deck}(p)$（即满足 $p \circ f = p$ 的所有[自同构](@entry_id:155390) $f: \tilde{M} \to \tilde{M}$）中的每一个元素都是 $(\tilde{M}, \tilde{g})$ 的一个[等距同构](@entry_id:273188)。换句话说，$\mathrm{Deck}(p)$ 是 $\mathrm{Isom}(\tilde{M})$ 的一个[子群](@entry_id:146164)。更准确地说，$\mathrm{Deck}(p)$ 恰好是 $\mathrm{Isom}(\tilde{M})$ 中所有保持 $p$ 的纤维不变的[等距同构](@entry_id:273188)构成的[子群](@entry_id:146164) [@problem_id:3054247]。

这个关系在研究具有对称性的[流形](@entry_id:153038)时尤其重要。许多[流形](@entry_id:153038)可以通过取一个更简单、对称性更高的[流形](@entry_id:153038)（如球面、欧氏空间、双曲空间）作商来构造。如果 $\tilde{M}$ 是 $M$ 的[万有覆盖空间](@entry_id:154691)，并且 $p: \tilde{M} \to M$ 是黎曼覆盖，那么 $M$ 就[等距同构](@entry_id:273188)于[商空间](@entry_id:274314) $\tilde{M}/\mathrm{Deck}(p)$ [@problem_id:3054247]。这使得我们可以通过研究 $\tilde{M}$ 的几何及其离散[等距同构](@entry_id:273188)[子群](@entry_id:146164) $\mathrm{Deck}(p)$ 来理解 $M$ 的几何。