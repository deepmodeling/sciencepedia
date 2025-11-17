## 引言
在黎曼几何的抽象框架中，度量被定义为切丛上一个光滑变化的[内积](@entry_id:158127)结构。然而，为了进行具体的几何计算——从测量曲线长度到求解爱因斯坦场方程——我们必须将这个抽象概念转化为一种可操作的、基于坐标的语言。这正是[黎曼度量](@entry_id:754359)的[局部坐标](@entry_id:181200)[表示的核](@entry_id:202190)心意义所在：它是在理论与实践之间架起的一座至关重要的桥梁。

本文将系统地引导读者掌握这一关键工具。在第一章“原则与机制”中，我们将深入探讨度量张量如何分解为坐标分量矩阵 $g_{ij}$，并阐明其必须满足的代数性质（对称性、[正定性](@entry_id:149643)）和在[坐标变换](@entry_id:172727)下保持[几何不变性](@entry_id:637068)的[协变](@entry_id:634097)原理。我们还将揭示度量如何唯一地确定[流形上的微积分](@entry_id:270207)法则，即[列维-奇维塔联络](@entry_id:161107)。随后的第二章“应用与跨学科联系”将展示这一表示法的强大威力，通过[欧氏空间](@entry_id:138052)、球面、[双曲空间](@entry_id:268092)等经典案例，演示如何使用 $g_{ij}$ 计算[测地线](@entry_id:269969)、曲率，并重新定义梯度和散度等[微分算子](@entry_id:140145)。我们还将探索其在广义相对论和[复几何](@entry_id:159080)等前沿领域的延伸。最后，在“动手实践”部分，读者将通过解决具体问题，将理论知识转化为实际的计算技能。

通过这三部分的学习，读者将不仅理解什么是度量的坐标表示，更将学会如何运用它来分析和解决[黎曼几何](@entry_id:160508)及其相关学科中的问题。让我们首先从其基本原则与机制开始。

## 原则与机制

在前一章中，我们介绍了[黎曼度量](@entry_id:754359)的抽象概念，即在光滑流形的每个切空间上平滑变化地指定一个[内积](@entry_id:158127)。为了在[黎曼几何](@entry_id:160508)中进行具体的计算和深入的理论分析，我们必须掌握如何在[局部坐标](@entry_id:181200)中表达度量张量及其相关概念。本章将系统地阐述黎曼度量在[局部坐标](@entry_id:181200)下表示的基本原则和关键机制。我们将看到，这些坐标表示虽然依赖于[坐标系](@entry_id:156346)的选择，但它们遵循着严格的变换法则，从而保证了从它们计算出的几何量（如长度、角度和曲率）是内蕴且不依赖于坐标的。

### 度量张量的[局部坐标](@entry_id:181200)表示

在[光滑流形](@entry_id:160799) $M$ 上给定一个黎曼度量 $g$。考虑 $M$ 上的一个[局部坐标](@entry_id:181200)卡 $(U, x)$，其坐标为 $(x^1, \dots, x^n)$。在 $U$ 中的每一点 $p$，该[坐标卡](@entry_id:262338)都提供了一个[切空间](@entry_id:199137) $T_p M$ 的自然基底，即[坐标基](@entry_id:270149)矢场 $\{\partial_i = \partial/\partial x^i\}$ 在点 $p$ 的取值 $\{\partial_i|_p\}$。

度量张量 $g$ 在这个[坐标卡](@entry_id:262338)中的**分量 (components)** 被定义为[基矢](@entry_id:199546)量的[内积](@entry_id:158127)，即一组函数 $g_{ij}: U \to \mathbb{R}$，其在点 $p$ 的取值为：
$$
g_{ij}(p) = g_p(\partial_i|_p, \partial_j|_p)
$$
有了这些分量，我们就可以表示任意两个切向量的[内积](@entry_id:158127)。若向量 $v, w \in T_p M$ 在此基底下的分量分别为 $(v^1, \dots, v^n)$ 和 $(w^1, \dots, w^n)$，即 $v = v^i \partial_i|_p$ 且 $w = w^j \partial_j|_p$（这里我们采用了爱因斯坦求和约定），则它们的[内积](@entry_id:158127)由度量的双线性性质决定：
$$
g_p(v, w) = g_p(v^i \partial_i|_p, w^j \partial_j|_p) = v^i w^j g_p(\partial_i|_p, \partial_j|_p) = g_{ij}(p) v^i w^j
$$
特别地，向量 $v$ 的长度平方为 $|v|_g^2 = g_p(v,v) = g_{ij}(p) v^i v^j$ [@problem_id:2983166]。这个二次型表达式是[黎曼几何](@entry_id:160508)中最基本的计算公式之一。

度量张量 $g$ 作为[切丛](@entry_id:161294)上一个光滑、对称、正定的 $(0,2)$ 型张量场的定义，直接转化为对其[局部坐标](@entry_id:181200)分量 $g_{ij}$ 的一系列要求 [@problem_id:2983141]。

#### [光滑性](@entry_id:634843)

黎曼度量被定义为一个**光滑**张量场，这意味着在任何光滑[坐标卡](@entry_id:262338)中，其分量函数 $g_{ij}(x)$ 都必须是关于坐标 $x=(x^1, \dots, x^n)$ 的光滑函数，即 $g_{ij} \in C^\infty(U)$。

#### 对称性

[内积](@entry_id:158127)的对称性，$g_p(v, w) = g_p(w, v)$，直接蕴含了其分量的对称性。将[基向量](@entry_id:199546)代入可得：
$$
g_{ij}(p) = g_p(\partial_i|_p, \partial_j|_p) = g_p(\partial_j|_p, \partial_i|_p) = g_{ji}(p)
$$
因此，在任何[坐标系](@entry_id:156346)中，由分量 $g_{ij}$ 构成的矩阵 $G(x) = [g_{ij}(x)]$ 都是一个[对称矩阵](@entry_id:143130)。在[无穷小位移](@entry_id:202209) $dx = dx^i \partial_i$ 的长度平方（即[线元](@entry_id:196833)）的表达式 $ds^2 = g_{ij} dx^i dx^j$ 中，对称性确保了交叉项 $g_{ij}dx^i dx^j$ 和 $g_{ji}dx^j dx^i$ (其中 $i \neq j$) 可以被合并为 $2g_{ij}dx^i dx^j$ [@problem_id:2983176]。

#### [正定性](@entry_id:149643)

[内积](@entry_id:158127)的正定性要求，对于任意非零向量 $v \in T_p M$，必须有 $g_p(v,v) > 0$。用坐标表示，即对于任意非零的分量向量 $(v^1, \dots, v^n) \in \mathbb{R}^n$，二次型 $g_{ij}(p) v^i v^j$ 必须为正。这正是矩阵 $G(p) = [g_{ij}(p)]$ 为[正定矩阵](@entry_id:155546)的定义。

从线性代数的角度看，一个[实对称矩阵](@entry_id:192806)是正定的，当且仅当它的所有[特征值](@entry_id:154894)都为严格正数。因此，在每一点 $p$，矩阵 $[g_{ij}(p)]$ 的所有[特征值](@entry_id:154894)必须大于零。这一条件强于仅仅要求[行列式](@entry_id:142978) $\det(G) > 0$，后者只保证了度量的非退化性（即[伪黎曼度量](@entry_id:185204)的情形），但不能排除负[特征值](@entry_id:154894)的存在 [@problem_id:2983168]。根据 **Sylvester 准则 (Sylvester's criterion)**，正定性的一个等价条件是矩阵的所有主子式（leading principal minors）都为正。

### [协变](@entry_id:634097)性与[不变性原理](@entry_id:199405)

[黎曼几何](@entry_id:160508)的一个核心思想是区分内蕴的、不依赖于坐标的几何对象与它们在特定[坐标系](@entry_id:156346)下的表示。度量张量 $g$ 本身是一个几何对象，它为每个点的[切空间](@entry_id:199137)赋予了[内积](@entry_id:158127)结构，这个事实不依赖于我们如何标记这些点。然而，它的分量 $g_{ij}$ 是通过将 $g$ 作用于特定的[坐标基](@entry_id:270149)向量 $\partial_i$ 和 $\partial_j$ 而得到的数值，因此这些数值显然依赖于[坐标系](@entry_id:156346)的选择 [@problem_id:2983138]。

当我们在两个重叠的[坐标卡](@entry_id:262338) $(U,x)$ 和 $(V,y)$ 之间切换时，[切空间](@entry_id:199137)的[基向量](@entry_id:199546)会根据[链式法则](@entry_id:190743)进行变换。设 $y=y(x)$ 是[坐标变换](@entry_id:172727)函数，则：
$$
\frac{\partial}{\partial y^\alpha} = \frac{\partial x^i}{\partial y^\alpha} \frac{\partial}{\partial x^i}
$$
度量在 $y$ [坐标系](@entry_id:156346)下的新分量 $\tilde{g}_{\alpha\beta}$ 被定义为 $\tilde{g}_{\alpha\beta}(p) = g_p(\partial/\partial y^\alpha|_p, \partial/\partial y^\beta|_p)$。利用 $g_p$ 的双线性性质和[基向量](@entry_id:199546)的变换法则，我们可以推导出分量的变换法则：
$$
\tilde{g}_{\alpha\beta} = g_p\left(\frac{\partial x^i}{\partial y^\alpha} \frac{\partial}{\partial x^i}, \frac{\partial x^j}{\partial y^\beta} \frac{\partial}{\partial x^j}\right) = \frac{\partial x^i}{\partial y^\alpha} \frac{\partial x^j}{\partial y^\beta} g_p\left(\frac{\partial}{\partial x^i}, \frac{\partial}{\partial x^j}\right) = \frac{\partial x^i}{\partial y^\alpha} \frac{\partial x^j}{\partial y^\beta} g_{ij}
$$
这正是**协变二阶张量 (covariant rank-2 tensor)** 的变换法则 [@problem_id:2983157]。它精确地描述了度量分量是如何“随[坐标系](@entry_id:156346)的改变而改变”的。

这个变换法则确保了[几何不变量](@entry_id:178611)的计算结果与[坐标系](@entry_id:156346)无关。例如，向量 $v$ 的长度平方是一个标量，其值必须是唯一的。设 $v$ 在 $x$ 坐标和 $y$ 坐标下的分量分别为 $v^i$ 和 $\tilde{v}^\alpha$。我们知道向量（[逆变张量](@entry_id:636697)）分量的变换法则是 $\tilde{v}^\alpha = \frac{\partial y^\alpha}{\partial x^i} v^i$。我们可以验证：
$$
\tilde{g}_{\alpha\beta} \tilde{v}^\alpha \tilde{v}^\beta = \left(\frac{\partial x^i}{\partial y^\alpha} \frac{\partial x^j}{\partial y^\beta} g_{ij}\right) \left(\frac{\partial y^\alpha}{\partial x^k} v^k\right) \left(\frac{\partial y^\beta}{\partial x^l} v^l\right) = \left(\frac{\partial x^i}{\partial y^\alpha}\frac{\partial y^\alpha}{\partial x^k}\right) \left(\frac{\partial x^j}{\partial y^\beta}\frac{\partial y^\beta}{\partial x^l}\right) g_{ij} v^k v^l
$$
根据链式法则，括号内的项等于克罗内克符号 $\delta^i_k$ 和 $\delta^j_l$，因此上式化为 $g_{ij} \delta^i_k \delta^j_l v^k v^l = g_{kl} v^k v^l$。这表明，尽管分量 $g_{ij}$ 和 $v^i$ 都随[坐标系](@entry_id:156346)而变，但它们的特定组合 $g_{ij}v^i v^j$ 却是**[不变量](@entry_id:148850)** [@problem_id:2983138]。

如果用矩阵来表示，令 $G = [g_{ij}]$，$G' = [\tilde{g}_{\alpha\beta}]$，以及[雅可比矩阵](@entry_id:264467) $J = [\frac{\partial y^\alpha}{\partial x^i}]$，则向量分量变换为 $v' = Jv$，而度量矩阵的变换法则可以从不变性 $v^\top G v = (v')^\top G' (v')$ 推导出来：
$$
v^\top G v = (Jv)^\top G' (Jv) = v^\top (J^\top G' J) v
$$
由于这对所有向量 $v$ 都成立，我们必须有 $G = J^\top G' J$。这等价于 $G' = (J^{-1})^\top G (J^{-1})$ [@problem_id:2983155]。这个[矩阵合同](@entry_id:189805)变换关系是协变二阶[张量变换法则](@entry_id:185176)的矩阵形式。它也清楚地显示，如果矩阵 $G$ 是对称正定的，那么 $G'$ 也是[对称正定](@entry_id:145886)的，这保证了黎曼度量的基本属性在坐标变换下得以保持 [@problem_id:2983168]。

这种[不变性](@entry_id:140168)的深刻体现是，我们可以从依赖于坐标的度量分量及其导数中构造出完全不依赖于坐标的几何量，例如**曲率 (curvature)**。一个经典的例子是[二维球面](@entry_id:269890) $S^2_R$ 的[高斯曲率](@entry_id:149725)。无论我们使用球面坐标 $(\theta, \phi)$ 还是通过球极投影得到的[平面极坐标](@entry_id:171478) $(\rho, \phi)$，尽管度量分量的表达式截然不同，通过标准程序计算出的[高斯曲率](@entry_id:149725)总是一个常数 $1/R^2$ [@problem_id:2983137]。这正是高斯“[绝妙定理](@entry_id:159067)”(Theorema Egregium) 的体现，它揭示了曲率是一个内蕴于度量的几何属性。

### 度量张量的微积分：联络与[协变微分](@entry_id:263981)

[黎曼度量](@entry_id:754359)最重要的作用之一是它唯一地确定了一个与度量结构相容的[微分](@entry_id:158718)方式——**列维-奇维塔联络 (Levi-Civita connection)**，记为 $\nabla$。这个联络是进行黎曼流形上[张量分析](@entry_id:161423)的基础。

[列维-奇维塔联络](@entry_id:161107)由两个基本属性定义：它是[无挠的](@entry_id:161664) (torsion-free)，并且与度量相容 (metric-compatible)。**度量相容性**意味着度量张量在[协变微分](@entry_id:263981)下为零，即 $\nabla g = 0$。这在物理上可以理解为，当一个向量沿着某条曲线平行移动时，它的长度和任意两个平行移动的向量之间的夹角都保持不变。

在[局部坐标](@entry_id:181200)中，度量[相容性条件](@entry_id:637057)表现为一个关于度量分量 $g_{ij}$ 和[联络系数](@entry_id:157618)（即**[克里斯托费尔符号](@entry_id:159831) (Christoffel symbols)** $\Gamma^k_{ij}$）的方程：
$$
\nabla_k g_{ij} = \partial_k g_{ij} - \Gamma^l_{ki} g_{lj} - \Gamma^l_{kj} g_{il} = 0
$$
其中 $\partial_k g_{ij}$ 是分量的普通偏导数，而包含 $\Gamma$ 的项是修正项，它们弥补了[坐标基](@entry_id:270149)向量 $\partial_i$ 自身在空间中的变化。事实上，如果我们从无挠和度量相容这两个条件出发，就可以唯一地解出[克里斯托费尔符号](@entry_id:159831)完全由度量分量及其一阶导数决定：
$$
\Gamma^k_{ij} = \frac{1}{2} g^{kl}(\partial_i g_{jl} + \partial_j g_{il} - \partial_l g_{ij})
$$
将这个表达式代入 $\nabla_k g_{ij}$ 的公式中，经过直接计算可以验证结果确实恒为零 [@problem_id:2983148]。这个结果是黎曼几何的基石之一，它意味着我们可以像在欧氏空间中处理常数[内积](@entry_id:158127)一样，在[协变微分](@entry_id:263981)的意义下“自由地移动”度量张量进出导数。

#### 特殊[坐标系](@entry_id:156346)与标架

虽然上述公式在任何[坐标系](@entry_id:156346)下都成立，但选择合适的[坐标系](@entry_id:156346)或基底（即**标架 (frame)**）可以极大地简化计算。

**坐标标架与[标准正交标架](@entry_id:189702)：** [坐标基](@entry_id:270149)向量 $\{\partial_i\}$ 构成一个**坐标标架 (coordinate frame)** 或称**完整标架 (holonomic frame)**，其特点是[基向量](@entry_id:199546)的[李括号](@entry_id:636461)为零：$[\partial_i, \partial_j]=0$。然而，在这个标架下，度量分量 $g_{ij}$ 通常是一个复杂的函数矩阵。作为替代，我们可以选择一个**[标准正交标架](@entry_id:189702) (orthonormal frame)** $\{e_a\}$，它由一组光滑的向量场构成，在每一点都满足 $g(e_a, e_b) = \delta_{ab}$。在这个标架下，度量分量是常数矩阵 $\delta_{ab}$，这大大简化了[内积](@entry_id:158127)计算。但是，代价是这个标架通常是**非完整 (anholonomic)** 的，即[基向量](@entry_id:199546)的李括号不为零：$[e_a, e_b] \neq 0$。与这两种标架相关的[联络系数](@entry_id:157618)也不同：坐标标架对应[克里斯托费尔符号](@entry_id:159831) $\Gamma^k_{ij}$，而[标准正交标架](@entry_id:189702)对应所谓的**[联络1-形式](@entry_id:275839) (connection 1-forms)** $\omega^a{}_b$。度量相容性在[标准正交标架](@entry_id:189702)下表现为一个简洁的[反对称关系](@entry_id:261979)：$\omega_{ab} + \omega_{ba} = 0$，其中 $\omega_{ab} = \delta_{ac}\omega^c{}_b$ [@problem_id:2983134]。

**[法坐标](@entry_id:143194)系 (Normal Coordinates)：** 在许多理论证明和局部近似计算中，**[法坐标](@entry_id:143194)系**是一个极其有用的工具。在任意一点 $p$ 的邻域，我们总可以构造一个以 $p$ 为中心点的[法坐标](@entry_id:143194)系。这个[坐标系](@entry_id:156346)的显著优点是，在[中心点](@entry_id:636820) $p$，它同时具备了坐标标架和[标准正交标架](@entry_id:189702)的部分优点：
1.  度量分量等于欧氏度量：$g_{ij}(p) = \delta_{ij}$。
2.  度量分量的一阶偏导数为零：$\partial_k g_{ij}(p) = 0$。

由克里斯托费尔符号的公式可知，第二个性质直接导致了在点 $p$ 处所有的[克里斯托费尔符号](@entry_id:159831)都为零：$\Gamma^k_{ij}(p) = 0$。

这个性质使得在点 $p$ 的所有[协变微分](@entry_id:263981)运算都退化为普通的[偏微分](@entry_id:194612)。例如，对于任意一个[张量场](@entry_id:190170) $T$，其协变导数的分量在点 $p$ 等于其普通[偏导数](@entry_id:146280)：$(\nabla_k T)(p) = (\partial_k T)(p)$。具体来说：
-   一个函数 $f$ 的梯度 $(\nabla f)^i(p) = g^{ij}(p) \partial_j f(p) = \delta^{ij} \partial_j f(p) = \partial_i f(p)$。
-   一个向量场 $X$ 的散度 $\text{div}X(p) = \partial_i X^i(p) + \Gamma^i_{ki}(p) X^k(p) = \partial_i X^i(p)$。
-   [拉普拉斯-贝尔特拉米算子](@entry_id:267002) $\Delta f(p) = g^{ij}(p)(\partial_i\partial_j f(p) - \Gamma^k_{ij}(p)\partial_k f(p)) = \sum_i \partial_i^2 f(p)$。

因此，在[法坐标](@entry_id:143194)系的中心点，所有基本微分算子都恢复了它们在[欧氏空间](@entry_id:138052)中的简单形式 [@problem_id:2983124]。值得注意的是，这种简化仅仅发生在[中心点](@entry_id:636820) $p$。度量的[二阶导数](@entry_id:144508)通常不为零，它们包含了该点曲率的全部信息。

总而言之，[黎曼度量](@entry_id:754359)的[局部坐标](@entry_id:181200)表示是连接抽象几何概念与具体分析计算的桥梁。理解其分量的性质、变换法则以及在微积分运算中的作用，是掌握黎曼几何这门学科的关键。