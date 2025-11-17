## 引言
在几何学的广阔图景中，我们常常寻求在给定的约束下找到“最佳”或“最典范”的对象——最短的路径是[测地线](@entry_id:269969)，面积最小的[曲面](@entry_id:267450)是极小曲面。调和映射理论将这一思想推广到[流形](@entry_id:153038)之间的映射，提出一个根本性问题：如何在一个给定的[同伦类](@entry_id:149365)中，找到一个能量最小、几何上最优美的代表？调和映射作为能量泛函的[临界点](@entry_id:144653)，为这一问题提供了深刻的答案，成为连接几何、拓扑与分析的核心桥梁。它不仅是[测地线](@entry_id:269969)和调和函数的自然高维推广，其存在性、正则性乃至[奇点](@entry_id:137764)的形成，都与[流形](@entry_id:153038)的内在曲率紧密相连，揭示了空间几何形态如何制约其上的分析对象。

本文旨在系统性地介绍调和映射的核心概念与应用。我们将从第一性原理出发，逐步深入这一迷人领域。
*   在“**原理与机制**”一章中，我们将从[变分原理](@entry_id:198028)出发，严格定义能量泛函与[张力场](@entry_id:188540)，从而引出调和映射的[偏微分方程](@entry_id:141332)。通过分析关键范例，我们将揭示目标[流形](@entry_id:153038)的曲率是如何在根本上决定调和映射的稳定性、存在性与正则性。
*   接下来的“**应用与跨学科联系**”一章将展示调和映射理论的强大威力，探讨其如何作为工具解决拓扑学中的问题，如何与极小曲面理论及[复几何](@entry_id:159080)紧密联系，并如何被推广到更广阔的几何情境中。
*   最后，在“**动手实践**”部分，一系列精心设计的问题将引导读者运用所学知识，解决具体几何问题，从而加深对理论的理解。

通过这三个章节的探索，读者将对调和映射这一现代[几何分析](@entry_id:157700)的基石建立起一个全面而深入的认识。

## 原理与机制

在介绍性章节之后，我们现在深入探讨调和映射理论的核心原理与机制。本章将从[变分原理](@entry_id:198028)出发，严格定义调和映射及其基本属性，然后通过一系列几何实例来建立直观认识。我们将重点剖析目标[流形](@entry_id:153038)的曲率如何在根本上决定调和映射的存在性、唯一性、稳定性与正则性。

### 能量泛函与调和映射的定义

调和映射理论的基石是作用于[黎曼流形](@entry_id:261160)之间[光滑映射](@entry_id:203730)的**[能量泛函](@entry_id:170311)**（energy functional），也称为[狄利克雷能量](@entry_id:276589)。给定一个紧致、有向的黎曼流形 $(M^m, g)$（可能带光滑边界 $\partial M$）和一个黎曼流形 $(N^n, h)$，对于一个[光滑映射](@entry_id:203730) $f: M \to N$，其能量定义为：

$$
E(f) = \frac{1}{2} \int_{M} |df|^2 \, dv_g
$$

这里的核心是能量密度 $|df|^2$。它是 $f$ 的[微分](@entry_id:158718) $df: TM \to f^*TN$ 的范数的平方，该范数由度量 $g$ 和 $h$ 共同诱导。具体而言，在 $M$ 的每一点 $p$，我们取[切空间](@entry_id:199137) $T_pM$ 的一组 $g$-标准正交基 $\{e_i\}_{i=1}^m$，则能量密度为：

$$
|df|^2(p) = \sum_{i=1}^m h_{f(p)}(df_p(e_i), df_p(e_i))
$$

这个定义等价于 $g$-度量下 $f$ [拉回](@entry_id:160816)的度量 $f^*h$ 的迹，即 $|df|^2 = \operatorname{trace}_g(f^*h)$。从物理学的角度看，[能量泛函](@entry_id:170311)衡量了映射的“[弹性形变](@entry_id:161971)”程度。

调和映射被定义为[能量泛函](@entry_id:170311) $E$ 的**[临界点](@entry_id:144653)**（critical point）。为了找到这些[临界点](@entry_id:144653)，我们应用[变分法](@entry_id:163656)。考虑 $f$ 的一个光滑单参数族形变 $f_t: M \to N$，其中 $t \in (-\epsilon, \epsilon)$，$f_0 = f$。这个形变在 $f$ 上的**变分向量场**（variation vector field）定义为 $V = \frac{d}{dt}\big|_{t=0} f_t$，它是沿着 $f$ 的一个 $f^*TN$ 的光滑[截面](@entry_id:154995)。如果我们考虑边界固定的[变分问题](@entry_id:756445)（即当 $\partial M \neq \emptyset$ 时，要求 $f_t|_{\partial M} = f|_{\partial M}$），那么 $V$ 在 $\partial M$ 上为零。

通过在积分号下对 $t$ 求导，并利用黎曼联络与度量的相容性以及[散度定理](@entry_id:143110)（积分的[格林公式](@entry_id:173118)），我们可以计算出能量泛函的**一阶变分公式**（first variation formula）[@problem_id:2978885]：

$$
\frac{d}{dt}\bigg|_{t=0} E(f_t) = - \int_M h(\tau(f), V) \, dv_g
$$

公式中的向量场 $\tau(f)$ 完全由映射 $f$ 及其一阶、[二阶导数](@entry_id:144508)确定，它被称为 $f$ 的**[张力场](@entry_id:188540)**（tension field）。它是 $f$ 的二阶共变导数 $\nabla df$ 关于度量 $g$ 的迹：

$$
\tau(f) = \operatorname{trace}_g(\nabla df) = \sum_{i=1}^m (\nabla df)(e_i, e_i)
$$

其中 $(\nabla df)(X,Y) = \nabla^{f^*TN}_X(df(Y)) - df(\nabla^M_X Y)$ 是对[微分](@entry_id:158718) $df$ 的共变导数，$\nabla^M$ 和 $\nabla^{f^*TN}$ 分别是 $M$ 上的Levi-Civita联络和在[拉回丛](@entry_id:159346) $f^*TN$ 上的[诱导联络](@entry_id:635081)。

根据变分原理，一个映射 $f$ 是[能量泛函](@entry_id:170311) $E$ 的[临界点](@entry_id:144653)，当且仅当其一阶变分对所有允许的变分向量场 $V$ 都为零。由于 $V$ 的任意性，这等价于[张力场](@entry_id:188540)在 $M$ 上恒为零。这就引出了调和映射的核心定义：

**定义：** 一个[光滑映射](@entry_id:203730) $f:(M,g) \to (N,h)$ 被称为**调和映射**（harmonic map），如果它的[张力场](@entry_id:188540)恒为零，即 $\tau(f) \equiv 0$。

调和映射方程 $\tau(f)=0$ 是一个关于 $f$ 的二阶、[非线性](@entry_id:637147)、椭圆型[偏微分方程组](@entry_id:172573)。它的解在几何、拓扑和物理中都有着深刻的应用。

### 基本范例与几何解释

为了更好地理解调和映射的几何意义，我们考察几个关键的基本范例。

**[测地线](@entry_id:269969)：一维区域上的调和映射**
最简单的情形是当定义域 $M$ 是[一维流](@entry_id:269448)形时，例如一个区间 $I$ 配备度量 $g=dt^2$。此时，唯一的[标准正交基](@entry_id:147779)是 $e_1 = \partial_t$。由于 $\nabla^M_{\partial_t}\partial_t = 0$，[张力场](@entry_id:188540)的表达式急剧简化。若 $f: I \to N$ 是一个映射（即一条曲线），其[张力场](@entry_id:188540)为 $\tau(f) = (\nabla df)(\partial_t, \partial_t) = \nabla^{f^*TN}_{\partial_t}(df(\partial_t))$。这正是沿曲线 $f(t)$ 的速度向量 $f'(t)$ 的共变导数，通常记为 $D_t f'(t)$。因此，调和映射方程 $\tau(f)=0$ 变成了测地线方程 $D_t f'(t) = 0$。此外，由 $D_t f'(t) = 0$ 可得 $\frac{d}{dt}h(f'(t), f'(t)) = 2h(D_t f'(t), f'(t)) = 0$，这意味着曲线的速度 $|f'(t)|$ 是常数。综上，**从[一维流](@entry_id:269448)形出发的调和映射恰好是目标[流形](@entry_id:153038)中按弧长（或其仿射重[参数化](@entry_id:272587)）[参数化](@entry_id:272587)的[测地线](@entry_id:269969)** [@problem_id:2978885]。这揭示了调和映射是[测地线](@entry_id:269969)概念在高维的自然推广。

**[极小子流形](@entry_id:204492)：[等距浸入](@entry_id:272242)下的调和映射**
另一个重要的例子是当映射 $f: M^m \to N^n$ 是一个**[等距浸入](@entry_id:272242)**（isometric immersion）时，即 $f^*h = g$。此时，$M$ 可以被视为 $N$ 的一个[子流形](@entry_id:159439)。利用高斯公式，我们可以将[张力场](@entry_id:188540)与[子流形](@entry_id:159439)的外蕴几何联系起来。高斯公式表明，对于 $M$ 上的任意[切向量](@entry_id:265494)场 $X, Y$，有 $\nabla^N_X(df(Y)) = df(\nabla^M_X Y) + \mathrm{II}(X,Y)$，其中 $\mathrm{II}$ 是 $f(M)$ 在 $N$ 中的第二基本形式。
将此代入[张力场](@entry_id:188540)的定义，我们得到：
$$
\tau(f) = \sum_{i=1}^m \left[ \nabla^N_{e_i}(df(e_i)) - df(\nabla^M_{e_i}e_i) \right] = \sum_{i=1}^m \mathrm{II}(e_i, e_i) = m H
$$
这里的 $H = \frac{1}{m}\operatorname{trace}_g(\mathrm{II})$ 是子流形 $f(M)$ 的**[平均曲率向量](@entry_id:199617)**（mean curvature vector）。因此，调和映射方程 $\tau(f)=0$ 等价于 $H=0$。[平均曲率](@entry_id:162147)为零的子流形被称为**[极小子流形](@entry_id:204492)**（minimal submanifold）。于是我们得到结论：**一个[等距浸入](@entry_id:272242)是调和映射当且仅当它的像是目标[流形](@entry_id:153038)中的一个[极小子流形](@entry_id:204492)** [@problem_id:2978885]。这为研究极小曲面提供了强大的变分工具。

**二维区域的[共形不变性](@entry_id:191867)**
[能量泛函](@entry_id:170311)的一个显著特性是它在二维定义域上的**[共形不变性](@entry_id:191867)**（conformal invariance）。假设我们将定义域度量 $g$ 做一个共形变换，变为 $\tilde{g} = e^{2\phi} g$，其中 $\phi$ 是 $M$ 上的光滑函数。在这个新度量下，能量密度变为 $|df|^2_{\tilde{g},h} = e^{-2\phi}|df|^2_{g,h}$，而体积元变为 $dv_{\tilde{g}} = e^{m\phi}dv_g$（其中 $m=\dim M$）。因此，新的能量泛函为：
$$
E_{\tilde{g}}(f) = \frac{1}{2} \int_M e^{-2\phi} |df|^2_{g,h} \cdot e^{m\phi} dv_g = \frac{1}{2} \int_M e^{(m-2)\phi} |df|^2_{g,h} dv_g
$$
从这个表达式可以看出，当且仅当维数 $m=2$ 时，指数因子 $e^{(m-2)\phi}$ 变为 1，使得能量泛函与[共形因子](@entry_id:267682) $\phi$ 无关，即 $E_{\tilde{g}}(f) = E_g(f)$。因此，**在二维情况下，能量泛函是共形不变的** [@problem_id:2978885]。这个性质在理论物理中至关重要，例如，在弦理论中，二维世界面上的[Polyakov作用量](@entry_id:159380)就是一种调和映射能量。它也意味着在研究从[黎曼曲面](@entry_id:178613)出发的调和映射时，我们拥有选择方便的局部[共形坐标](@entry_id:192723)（如[等温坐标](@entry_id:272481)）的自由。

### 调和映射方程：内蕴与外蕴观点

调和映射方程 $\tau(f)=0$ 本质上是一个二阶椭圆型[偏微分方程组](@entry_id:172573)。在[局部坐标](@entry_id:181200) $(x^i)$ 和 $(f^\alpha)$ 下，它可以写作：
$$
\tau(f)^k = g^{ij} \left( \frac{\partial^2 f^k}{\partial x^i \partial x^j} - \Gamma_{ij}^l(x) \frac{\partial f^k}{\partial x^l} + \Gamma_{\alpha\beta}^k(f) \frac{\partial f^\alpha}{\partial x^i} \frac{\partial f^\beta}{\partial x^j} \right) = 0
$$
这里 $\Gamma_{ij}^l$ 是 $(M,g)$ 的[Christoffel符号](@entry_id:159831)，$\Gamma_{\alpha\beta}^k$ 是 $(N,h)$ 的Christoffel符号。第一项是欧氏空间中的[Laplace算子](@entry_id:185214)，第二项是定义域几何的修正，而第三项是一个二次[非线性](@entry_id:637147)项，反映了目标[流形](@entry_id:153038)的几何。正是这个[非线性](@entry_id:637147)项使得调和映射方程的求解变得复杂而有趣。

为了更清晰地理解这个方程的结构，特别是目标[流形](@entry_id:153038)几何的作用，我们常常采用**外蕴观点**（extrinsic viewpoint）。根据[Nash嵌入定理](@entry_id:159937)，任何黎曼流形 $(N,h)$ 都可以等距地嵌入到一个足够高维的欧氏空间 $\mathbb{R}^K$ 中 [@problem_id:2995331] [@problem_id:2978888]。这使我们可以把映射 $u: M \to N$ 看作是一个取值于 $\mathbb{R}^K$ 的[向量值函数](@entry_id:261164)，但其像被约束在子流形 $N$ 上。

在这种观点下，我们可以定义一个作用于 $u$ 的**环境[Laplace-Beltrami算子](@entry_id:267002)** $\Delta_g u$。它与内蕴[张力场](@entry_id:188540) $\tau(u)$ 的关系可以通过高斯公式揭示。该公式将 $\mathbb{R}^K$ 中的平坦联络 $\nabla^{\mathbb{R}^K}$ 分解为 $N$ 上的切向部分（即 $N$ 的[Levi-Civita联络](@entry_id:161107) $\nabla^N$）和法向部分（由第二基本形式 $B$ 描述）。经过推导，我们得到一个至关重要的分解公式 [@problem_id:2978888]：
$$
\Delta_g u = \tau(u) + \operatorname{tr}_g(B_u(du,du))
$$
这里 $\Delta_g u = \operatorname{trace}_g(\nabla^{\mathbb{R}^K} du)$ 是将 $u$ 视为 $\mathbb{R}^K$ 值函数时的[Laplace-Beltrami算子](@entry_id:267002)。$\tau(u)$ 是 $u$ 作为 $M \to N$ 映射的内蕴[张力场](@entry_id:188540)，它完全位于 $N$ 的[切空间](@entry_id:199137)中。而 $\operatorname{tr}_g(B_u(du,du))$ 是 $N$ 在 $\mathbb{R}^K$ 中的[第二基本形式](@entry_id:161454) $B$ 与 $u$ 的[微分](@entry_id:158718) $du$ 复合后的迹，它完全位于 $N$ 的法空间中。

这个公式将环境拉普拉斯算子 $\Delta_g u$ 分解为它在 $N$ 上的切向分量（即内蕴[张力场](@entry_id:188540) $\tau(u)$）和法向分量。它直接导出了几个重要结论：
1.  一个映射 $u: M \to N$ 是调和的（即 $\tau(u)=0$），当且仅当它的环境[拉普拉斯算子](@entry_id:146319) $\Delta_g u$ 处处与 $N$ 的切空间正交，即 $\Delta_g u$ 是一个[法向量场](@entry_id:268853)。
2.  如果目标[流形](@entry_id:153038) $N$ 在 $\mathbb{R}^K$ 中是**[全测地的](@entry_id:183906)**（totally geodesic），例如 $\mathbb{R}^K$ 中的一个[线性子空间](@entry_id:151815)，那么它的[第二基本形式](@entry_id:161454) $B$ 恒为零。此时，$\Delta_g u = \tau(u)$。因此，映射 $u$ 是调和的当且仅当 $\Delta_g u = 0$，即 $u$ 的每个分量都是 $(M,g)$ 上的[调和函数](@entry_id:746864) [@problem_id:2978888]。
3.  一个特别重要的例子是目标[流形](@entry_id:153038)为[单位球](@entry_id:142558)面 $N=S^{K-1} \subset \mathbb{R}^K$。其第二基本形式为 $B_p(V,W) = -h(V,W)p$，其中 $p$ 是球面上的点（也是[单位法向量](@entry_id:178851)）。代入分解公式得到 $\operatorname{tr}_g(B_u(du,du)) = -|du|^2 u$。因此，调和映射方程 $\tau(u)=0$ 等价于 $\Delta_g u = -|du|^2 u$ [@problem_id:2978888]。

我们可以通过一个具体的计算来体会这个外蕴公式的威力 [@problem_id:2978887]。考虑一个从[共形平坦](@entry_id:260902)的二维空间 $(M=\mathbb{R}^2, g=4(dx^2+dy^2))$ 到单位球面 $S^2 \subset \mathbb{R}^3$ 的映射 $f$。由于 $g$ 的分量是常数，其[Christoffel符号](@entry_id:159831)为零，因此环境拉普拉斯算子就是 $\Delta_g f = \frac{1}{4}(\frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2})$。根据上述结论，映射 $f$ 的[张力场](@entry_id:188540)为 $\tau(f) = \Delta_g f - (-|df|_g^2 f) = \Delta_g f + |df|_g^2 f$。这个表达式将内蕴的、复杂的[张力场](@entry_id:188540)计算转化为了在[欧氏空间](@entry_id:138052)中对[向量值函数](@entry_id:261164)进行求导和代数运算，大大简化了分析过程。

### 曲率的角色 I：稳定性与存在性

目标[流形](@entry_id:153038) $N$ 的曲率在调和映射理论中扮演着决定性的角色。曲率的符号（正、负或零）直接影响调和映射的稳定性、存在性和唯一性。

为了研究稳定性，我们考察能量泛函在[临界点](@entry_id:144653)（即调和映射）处的**二阶变分**。对能量 $E(u_t)$ 关于 $t$ 求[二阶导数](@entry_id:144508)，并利用 $u$ 是调和的（$\tau(u)=0$）这一条件，可以得到二阶变分公式 [@problem_id:3033060]：
$$
\left.\frac{d^2}{dt^2}\right|_{t=0} E(u_t) = \int_M h(J_u(V), V) \, dv_g
$$
这里的 $J_u$ 是一个作用于变分场 $V$ 的线性自伴[椭圆算子](@entry_id:181616)，称为**[雅可比算子](@entry_id:195512)**（Jacobi operator）或[稳定性算子](@entry_id:191401)。它的表达式为：
$$
J_u(V) = \nabla^*\nabla V - \sum_{i=1}^m R^N(V, du(e_i))du(e_i)
$$
其中 $\nabla^*\nabla = -\operatorname{trace}_g(\nabla^2)$ 是作用于 $u^*TN$ [截面](@entry_id:154995)上的**糙拉普拉斯算子**（rough Laplacian），$R^N$ 是目标[流形](@entry_id:153038) $(N,h)$ 的黎曼曲率张量。

一个调和映射 $u$ 被称为**稳定的**（stable），如果其二阶变分对所有变分场 $V$ 都是非负的，即 $\int_M h(J_u(V), V) \, dv_g \ge 0$。[雅可比算子](@entry_id:195512)的谱（[特征值](@entry_id:154894)）决定了稳定性。

现在，曲率的作用变得清晰起来。二阶变分公式的被积函数包含两项：一项是 $|\nabla V|^2 = h(\nabla^*\nabla V, V)$，它总是非负的，代表了变分场的“能量”；另一项是曲率项 $-\sum_{i} h(R^N(V, du(e_i))du(e_i), V)$。这一项的符号由 $N$ 的曲率决定。

回忆一下，由 $V$ 和 $X$ 张成的二维平面的[截面曲率](@entry_id:159738) $K_N(V \wedge X)$ 由 $K_N(V \wedge X)|V \wedge X|^2 = h(R^N(V,X)X,V)$ 定义。因此，曲率项可以写成 $\sum_i K_N(V \wedge du(e_i)) |V \wedge du(e_i)|^2$。

如果目标[流形](@entry_id:153038) $(N,h)$ 具有**[非正截面曲率](@entry_id:275356)**（non-positive sectional curvature），即 $K_N \le 0$，那么曲率项 $-\sum_{i} K_N(\dots)|\dots|^2$ 将是**非负的**。此时，二阶变分恒为非负：
$$
\left.\frac{d^2}{dt^2}\right|_{t=0} E(u_t) = \int_M \left( |\nabla V|^2 - \sum_i h(R^N(V, du(e_i))du(e_i), V) \right) dv_g \ge 0
$$
因此，**任何到[非正曲率流形](@entry_id:636489)的调和映射都是稳定的** [@problem_id:2995347]。

这个稳定性有着极其深刻的推论。Eells和Sampson证明，当 $K_N \le 0$ 时，[能量泛函](@entry_id:170311) $E$ 沿着任意两个映射之间的**[测地线](@entry_id:269969)形变**（geodesic homotopy）是凸的 [@problem_id:3029733]。一个凸泛函的[临界点](@entry_id:144653)必然是全局最小值点。这意味着，在这种情况下，**任何调和映射都是其[同伦类](@entry_id:149365)中的[能量泛函](@entry_id:170311)的全局最小值点** [@problem_id:3029733]。这与“任何[临界点](@entry_id:144653)都是最小值”的说法，是调和映射理论中一个里程碑式的结论，它保证了在[非正曲率](@entry_id:203441)目标中，通过[变分法](@entry_id:163656)找到的调和映射具有最佳的能量性质。

相反，如果目标[流形](@entry_id:153038)具有正曲率，情况则大不相同。例如，对于 $m \ge 3$，单位球面 $S^m$ 到自身的[恒等映射](@entry_id:634191) $id: S^m \to S^m$ 是一个调和映射（因为它是一个[等距同构](@entry_id:273188)），但它不是稳定的，也不是其[同伦类](@entry_id:149365)中的能量[最小值点](@entry_id:634980) [@problem_id:3029733]。这表明在正曲率目标中，调和映射可以是能量地形图上的“[鞍点](@entry_id:142576)”，而非“谷底”。

### 曲率的角色 II：正则性与[奇点](@entry_id:137764)

曲率不仅决定稳定性，还深刻影响调和映射的**正则性**（regularity），即解的光滑程度。这一联系可以通过**[Bochner恒等式](@entry_id:193184)**来揭示，它是一个联系映射能量密度、其[拉普拉斯算子](@entry_id:146319)以及[流形曲率](@entry_id:187680)的基本公式。对于一个调和映射 $u: (M,g) \to (N,h)$，其能量密度 $e = \frac{1}{2}|du|^2$ 满足如下的Bochner型恒等式：
$$
\frac{1}{2} \Delta_g |du|^2 = |\nabla du|^2 + \langle \operatorname{Ric}^M(du), du \rangle - \sum_{i,j=1}^m \langle R^N(du(e_i), du(e_j))du(e_j), du(e_i) \rangle
$$
其中 $\operatorname{Ric}^M$ 是定义域 $M$ 的[Ricci曲率](@entry_id:162038)。

我们再次考察曲率项 $\mathcal{R}_N = -\sum_{i,j} \langle R^N(du(e_i), du(e_j))du(e_j), du(e_i) \rangle$。
*   当 $K^N \le 0$ 时，我们已经看到 $\mathcal{R}_N \ge 0$。如果定义域的Ricci曲率也非负（$\operatorname{Ric}^M \ge 0$），那么[Bochner恒等式](@entry_id:193184)给出 $\Delta_g e \ge 2|\nabla du|^2 \ge 0$。这意味着能量密度 $e$ 是一个**[次调和函数](@entry_id:191036)**（subharmonic function）。根据[极值原理](@entry_id:138611)，[次调和函数](@entry_id:191036)不能在区域内部取得最大值（除非是常数）。这个性质可以用来建立能量密度的[先验估计](@entry_id:186098)，从而证明调和映射解的[光滑性](@entry_id:634843)。这正是Eells和Sampson利用调和映射热流方法证明[非正曲率](@entry_id:203441)目标[流形](@entry_id:153038)中存在光滑调和映射的核心分析工具。更精细地，如果 $N$ 的[截面曲率](@entry_id:159738)有负的[上界](@entry_id:274738)，例如 $K^N \le -a^2  0$，[Bochner公式](@entry_id:187951)能给出更强的定量信息，即 $\Delta_g e$ 被一个正的二次项所控制 [@problem_id:3025938]，这反映了能量密度的严格次调和性。

*   当 $K^N > 0$ 时，情况截然相反。此时曲率项 $\mathcal{R}_N$ 为负。它在[Bochner公式](@entry_id:187951)中扮演了一个“吸引”或“聚焦”的角色，与 $|\nabla du|^2$ 的“[扩散](@entry_id:141445)”效应相抗衡。如果这个负的曲率项足够强，它就可能压倒[扩散](@entry_id:141445)项，导致能量密度集中于一点，形成**[奇点](@entry_id:137764)**（singularity）。

一个经典的例子可以完美地诠释这种现象 [@problem_id:3033106]。考虑从三维[单位球](@entry_id:142558) $B_1(0) \subset \mathbb{R}^3$ 到[单位球](@entry_id:142558)面 $S^2$ 的映射 $u(x) = x/|x|$。
1.  这个映射在原点 $x=0$ 未定义，但在 $B_1 \setminus \{0\}$ 上是光滑的。通过直接计算，可以得到其能量密度为 $|du|^2 = 2/|x|^2$。
2.  尽管能量密度在原点发散，但它在 $W^{1,2}$ 意义下是有限能量的，因为在 $m=3$ 维中积分 $\int_{B_1} |x|^{-2} dx$ 是收敛的。具体地，在半径为 $r$ 的球上的能量为 $E(u, B_r) = 8\pi r$。
3.  这个映射在 $B_1 \setminus \{0\}$ 上是调和的，并且它是在其边界值给定的所有映射中的能量最小值点。然而，它在原点有一个不可去除的[奇点](@entry_id:137764)。

为了量化[奇点](@entry_id:137764)的强度，我们引入**单调能量密度**（monotone energy density）的概念：$\Theta(u, x_0) = \lim_{r \to 0} r^{2-m} E(u, B_r(x_0))$。对于 $u(x)=x/|x|$ 在原点，我们有 $m=3$，所以 $\Theta(u, 0) = \lim_{r \to 0} r^{-1} (8\pi r) = 8\pi$。

Schoen和Uhlenbeck的**$\varepsilon$-正则性定理**指出，存在一个普适常数 $\varepsilon_0 > 0$，如果一个能量极小化的调和映射在某一点 $x_0$ 的单调能量密度 $\Theta(u, x_0)$ 小于 $\varepsilon_0$，那么该映射在 $x_0$ 的一个邻域内是光滑的。我们的例子 $u(x)=x/|x|$ 是一个能量极小化映射，但它在原点是奇异的。这必然意味着它的单调能量密度 $\Theta(u,0)=8\pi$ 必须大于或等于正则性阈值 $\varepsilon_0$。这个非零的能量密度“量子”$8\pi$ 精确地衡量了[奇点](@entry_id:137764)所“捕获”的能量，而这个能量的集中正是由目标[流形](@entry_id:153038) $S^2$ 的正曲率所促成的 [@problem_id:3033106]。

### 解析框架：弱调和映射

现代调和映射理论的许多存在性结果，特别是对于一般目标[流形](@entry_id:153038)，都依赖于[偏微分方程](@entry_id:141332)和变分法的弱解理论。这需要我们将调和映射的概念推广到索博列夫空间中。

首先，我们需要在[流形](@entry_id:153038)之间定义**[索博列夫空间](@entry_id:141995)** $W^{1,2}(M,N)$。这同样可以通过Nash嵌入 $i: N \hookrightarrow \mathbb{R}^K$ 来实现。我们将 $W^{1,2}(M,N)$ 定义为所有这样的映射 $u: M \to \mathbb{R}^K$，其像几乎处处落在 $N$ 中，并且其作为 $\mathbb{R}^K$ 值函数，它和它的一阶[弱导数](@entry_id:189356)都是平方可积的 [@problem_id:2995331] [@problem_id:3034979]。一个关键的定理是，这个空间的定义以及映射的能量 $E(u)$ 的值，都不依赖于所选择的具体[等距嵌入](@entry_id:152303) $i$ [@problem_id:2995331]。

有了这个空间，我们可以定义**弱调和映射**（weakly harmonic map）。一个映射 $u \in W^{1,2}(M,N)$ 被称为弱调和映射，如果它在[分布](@entry_id:182848)意义下满足[欧拉-拉格朗日方程](@entry_id:137827)。这等价于对所有具有[紧支集](@entry_id:276214)的、光滑的变分向量场 $\phi \in C_c^\infty(M, u^{-1}TN)$，都有：
$$
\int_M \langle du, \nabla\phi \rangle_{g,h} \, dv_g = 0
$$
这与我们之前通过[分部积分](@entry_id:136350)得到的一阶变分公式是完全对应的，只是现在是在[弱形式](@entry_id:142897)下陈述 [@problem_id:3034979]。

在这个解析框架下，[能量泛函](@entry_id:170311) $E: W^{1,2}(M,N) \to \mathbb{R}$ 具有一个至关重要的性质：**[弱下半连续性](@entry_id:198224)**（weak lower semi-continuity）。这意味着如果一列映射 $u_k$ 在 $W^{1,2}$ 空间中[弱收敛](@entry_id:146650)到 $u$，那么 $E(u) \le \liminf_{k\to\infty} E(u_k)$ [@problem_id:3034979]。这个性质是应用**变分法直接方法**（direct method in the calculus of variations）来证明能量[最小值点](@entry_id:634980)（即弱调和映射）存在性的关键。该方法的大致思路是：在一个给定的[同伦类](@entry_id:149365)中，取一个能量的极小化序列 $u_k$，利用[弱下半连续性](@entry_id:198224)和空间的紧性性质，证明该序列有一个弱收敛的子列，其极限 $u$ 就是能量的[最小值点](@entry_id:634980)，因此是一个弱调和映射。接下来的问题，即这个弱调和映射是否光滑（即正则性问题），则将我们带回到前一节讨论的、由曲率主导的分析中。