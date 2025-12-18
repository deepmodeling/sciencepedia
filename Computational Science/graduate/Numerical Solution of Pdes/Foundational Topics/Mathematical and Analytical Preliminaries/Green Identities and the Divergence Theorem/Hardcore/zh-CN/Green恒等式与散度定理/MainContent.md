## 引言
[格林恒等式](@entry_id:176369)与散度定理是多元微积分的基石，但在现代[偏微分方程(PDE)](@entry_id:166689)的理论与计算研究中，它们的意义远超于此。它们不仅是连接PDE强形式与[弱形式](@entry_id:142897)的桥梁，更是有限元法、[有限体积法](@entry_id:749372)等强大数值方法的理论支柱。然而，经典的定理形式依赖于函数的[光滑性](@entry_id:634843)和区域边界的正则性，这在处理现代[PDE理论](@entry_id:189232)中的[弱解](@entry_id:161732)以及工程应用中常见的复杂几何时，显得力不从心。本文旨在填补这一认知空白，从一个更广阔、更严谨的视角重新审视这些经典定理。

本文将分为三个核心部分，系统地引导读者掌握[格林恒等式](@entry_id:176369)与散度定理的现代内涵及其应用。在第一章“原理与机制”中，我们将深入探讨在[索博列夫空间](@entry_id:141995)框架下的[广义散度定理](@entry_id:181016)和[格林恒等式](@entry_id:176369)，引入[迹算子](@entry_id:183665)等关键概念，为处理弱正则性问题建立坚实的数学基础。随后，在第二章“应用与[交叉](@entry_id:147634)学科联系”中，我们将展示这些理论如何在有限元、有限体积和边界元等数值方法中发挥核心作用，并揭示其与物理学、[连续介质力学](@entry_id:155125)及前沿[科学计算](@entry_id:143987)领域的深刻联系。最后，在第三章“动手实践”中，您将通过一系列精心设计的计算问题，亲手验证理论并构建数值求解器，将抽象的数学原理转化为解决实际问题的能力。

## 原理与机制

本章旨在深入探讨[格林恒等式](@entry_id:176369) (Green's identities) 与散度定理 (divergence theorem) 的基本原理及其在[偏微分方程](@entry_id:141332) (PDE) [数值分析](@entry_id:142637)中的核心作用。我们将从现代泛函分析的视角出发，建立一个适用于[弱解](@entry_id:161732)理论的严谨框架。这一框架不仅是[有限元法 (FEM)](@entry_id:176633) 等高级数值方法的理论基石，也为理解解的性质和边界条件的处理方式提供了深刻的洞见。

### [广义散度定理](@entry_id:181016)

[散度定理](@entry_id:143110)，又称高斯-[格林定理](@entry_id:140478) (Gauss-Green theorem)，是多元微积分中的一个基本结果。在其经典形式中，该定理指出，对于一个具有光滑边界 $\partial\Omega$ 的有界区域 $\Omega \subset \mathbb{R}^n$ 和一个在 $\overline{\Omega}$ 上连续可微的向量场 $\mathbf{F} \in C^1(\overline{\Omega}; \mathbb{R}^n)$，向量场在区域 $\Omega$ 内的散度（源或汇的密度）的[体积分](@entry_id:171119)，等于向量场穿过区域边界 $\partial\Omega$ 的法向分量的通量（净流出量）的[面积分](@entry_id:275394)。数学上表示为：
$$
\int_{\Omega} \operatorname{div} \mathbf{F} \, dx = \int_{\partial \Omega} (\mathbf{F} \cdot \mathbf{n}) \, dS
$$
其中，$\mathbf{n}$ 是 $\partial\Omega$ 上的单位外[法向量](@entry_id:264185)，$dx$ 和 $dS$ 分别是 $\Omega$ 上的 $n$ 维勒贝格测度和 $\partial\Omega$ 上的 $(n-1)$ 维[曲面](@entry_id:267450)测度。

然而，在[偏微分方程](@entry_id:141332)的现代研究中，我们常常处理不具备经典[可微性](@entry_id:140863)的“弱解”，这些解所属的函数空间（如[索博列夫空间](@entry_id:141995)）中的函数可能在任何地方都不可微。此外，计算区域的边界也可能不光滑，例如带有尖点或拐角的多边形区域。因此，我们必须将散度定理推广到更弱的正则性假设下。

#### [迹算子](@entry_id:183665)：为边界值赋予意义

推广散度定理的关键挑战在于如何定义[索博列夫空间](@entry_id:141995)中函数在边界上的值。一个典型的[索博列夫空间](@entry_id:141995)，如 **$H^1(\Omega)$**，由其弱[一阶导数](@entry_id:749425)平方可积的 $L^2(\Omega)$ 函数构成。由于 $n$ 维空间中 $(n-1)$ 维边界的[勒贝格测度](@entry_id:139781)为零，从 $L^2$ 的角度看，函数在边界上的值是没有定义的。

为了克服这一困难，我们引入了**[迹算子](@entry_id:183665) (trace operator)** 的概念。对于具有有界 **Lipschitz 边界**（一个足够正则，允许存在拐角但不允许出现分形或尖刺等更复杂奇异性的边界）的区域 $\Omega$，可以证明存在一个唯一的线性[连续算子](@entry_id:143297) $T: H^1(\Omega) \to H^{1/2}(\partial\Omega)$。其中 $H^{1/2}(\partial\Omega)$ 是一个分数阶索博列夫空间，其元素可以被视为在边界 $\partial\Omega$ 上“半阶可微”的函数。该算子具有以下关键性质 ：
1.  **连续性**: 存在常数 $C$，使得 $\lVert T u\rVert_{H^{1/2}(\partial \Omega)} \le C \lVert u\rVert_{H^1(\Omega)}$ 对所有 $u \in H^1(\Omega)$ 成立。这意味着内部函数的微小变化（在 $H^1$ 范数下）会导致边界迹的微小变化。
2.  **稠密性**: 如果一个函数 $u$ 属于[光滑函数](@entry_id:267124)空间 $C(\overline{\Omega})$，那么它的迹 $Tu$ 就是它在边界上的标准限制 $u|_{\partial\Omega}$。
3.  **满射性与[右逆](@entry_id:161498)**: [迹算子](@entry_id:183665)是满射的，即任何边界函数 $g \in H^{1/2}(\partial\Omega)$ 都是某个内部函数 $u \in H^1(\Omega)$ 的迹。更重要的是，存在一个有界的**[延拓算子](@entry_id:749192) (extension operator)** $E: H^{1/2}(\partial \Omega) \to H^1(\Omega)$，它是 $T$ 的[右逆](@entry_id:161498)，满足 $T \circ E = \mathrm{Id}$。

[迹算子](@entry_id:183665)为我们提供了一个严谨的工具来讨论 $H^1$ 函数的边界值，这对于在弱形式中施加边界条件和解释边界积分至关重要。

#### 弱正则性下的[散度定理](@entry_id:143110)

有了[迹算子](@entry_id:183665)的概念，我们可以陈述适用于[索博列夫空间](@entry_id:141995)的[广义散度定理](@entry_id:181016)。对于一个有界 Lipschitz 区域 $\Omega \subset \mathbb{R}^n$ 和一个向量场 $\mathbf{F} \in W^{1,1}(\Omega; \mathbb{R}^n)$（即 $\mathbf{F}$ 及其弱一阶导数均在 $L^1(\Omega)$ 中），散度定理成立 ：
$$
\int_{\Omega} \operatorname{div} \mathbf{F} \, dx = \int_{\partial \Omega} \gamma(\mathbf{F}) \cdot \mathbf{n} \, dS
$$
在此公式中，各项的精确含义如下：
-   $\operatorname{div} \mathbf{F} = \sum_{i=1}^n \partial_{x_i} F_i$ 是在[分布](@entry_id:182848)意义下定义的**弱散度 (weak divergence)**，它属于 $L^1(\Omega)$。
-   $\gamma(\mathbf{F})$ 是 $\mathbf{F}$ 在边界 $\partial\Omega$ 上的**索博列夫迹 (Sobolev trace)**，它属于 $L^1(\partial\Omega; \mathbb{R}^n)$。
-   $\mathbf{n}$ 是在 $\partial\Omega$ 上 $dS$-[几乎处处](@entry_id:146631)定义的单位外法向量。
-   $dx$ 是 $\Omega$ 上的 $n$ 维勒贝格测度，$dS$ 是 $\partial\Omega$ 上的 $(n-1)$ 维豪斯多夫[曲面](@entry_id:267450)测度。

这个广义形式是现代[偏微分方程理论](@entry_id:189232)的基石，它允许我们在极弱的正则性假设下进行分部积分。

#### 外法向约定及其影响

在应用散度定理及其推论时，对单位外法向量 $\mathbf{n}$ 的**方向约定 (orientation convention)** 必须保持一致。所谓“外法向”，指的是在边界的每一点都指向区域 $\Omega$ 外部的方向。

对于一个简单的连通区域，这个概念很直观。但对于有“洞”的区域，如一个环形域 $\Omega = \{ x \in \mathbb{R}^2 : r_1 \lt |x| \lt r_2 \}$，其边界由外圆周 $|x|=r_2$ 和内圆周 $|x|=r_1$ 组成。此时，“外法向”约定意味着 ：
-   在外边界 $|x|=r_2$ 上，$\mathbf{n}$ 指向径向外侧。
-   在内边界 $|x|=r_1$ 上，$\Omega$ 区域位于该圆周之外，因此“外法向”$\mathbf{n}$ 指向径向内侧，即指向中心的“洞”。

这一约定直接影响边界积分的符号。例如，环域上的总通量是外边界的通量与内边界的通量之和。根据散度定理，$\int_{\Omega} \nabla \cdot \mathbf{F} \, dx = \int_{|x|=r_2} \mathbf{F} \cdot \mathbf{n}_{\text{out}} \, ds + \int_{|x|=r_1} \mathbf{F} \cdot \mathbf{n}_{\text{in}} \, ds$。若用径向单位向量 $\hat{\mathbf{r}}$ 表示，外边界法向为 $\hat{\mathbf{r}}$，内边界法向为 $-\hat{\mathbf{r}}$。于是，[体积分](@entry_id:171119)等于外圆周通量（以 $\hat{\mathbf{r}}$ 为法向）减去内圆周通量（同样以 $\hat{\mathbf{r}}$ 为法向）。这个符号的改变在[守恒定律](@entry_id:269268)的数值计算（如[有限体积法](@entry_id:749372)）中至关重要。

#### 定理的局限性与BV理论

尽管推广到 Lipschitz 域已经极大地扩展了[散度定理](@entry_id:143110)的应用范围，但仍存在一些几何上更奇异的区域，其边界甚至不是 Lipschitz 的。一个典型的例子是 **von Koch 雪花**，其边界是分形的，处处不可微，且具有无限的一维[豪斯多夫测度](@entry_id:200740)（长度）。对于这样的区域，经典的边界积分 $\int_{\partial\Omega} \mathbf{F} \cdot \mathbf{n} \, dS$ 变得没有意义 。

为了处理这类更复杂的情形，[几何测度论](@entry_id:187987)提供了更为强大的工具，即**[有界变差函数](@entry_id:198128) (functions of bounded variation, BV)** 和**[有限周长集](@entry_id:202067) (sets of finite perimeter)** 理论。一个区域 $\Omega$ 被称为[有限周长集](@entry_id:202067)，如果其特征函数 $\chi_\Omega$ 的[分布导数](@entry_id:181138)是一个有界 Radon 测度。对于任何[有限周长集](@entry_id:202067)，可以定义一个[测度论](@entry_id:139744)意义下的“[约化边界](@entry_id:191712)” $\partial^*\Omega$ 和其上的外法向量 $\boldsymbol{\nu}_\Omega$，并证明一个极广义的高斯-[格林公式](@entry_id:173118)成立。这一理论为在具有高度不规则边界的区域上进行通量计算提供了坚实的数学基础，尽管它已超出了大多数标准有限元课程的范畴。

### [格林恒等式](@entry_id:176369)

[格林恒等式](@entry_id:176369)是散度定理的重要推论，通过在[散度定理](@entry_id:143110)中巧妙地选择向量场 $\mathbf{F}$ 得到。这些恒等式是推导[偏微分方程](@entry_id:141332)[弱形式](@entry_id:142897)、研究算子性质以及发展[边界积分方法](@entry_id:746943)的关键。

#### [格林第一恒等式](@entry_id:170345)

**[格林第一恒等式](@entry_id:170345) (Green's first identity)** 源于对向量场 $\mathbf{F} = v A \nabla u$ 应用散度定理，其中 $u$ 和 $v$ 是标量函数，$A$ 是一个[矩阵值函数](@entry_id:199897)（例如，代表材料的电导率或[扩散](@entry_id:141445)系数）。

首先，利用向量微积分的[乘积法则](@entry_id:158393)：
$$
\nabla \cdot (v A \nabla u) = \nabla v \cdot (A \nabla u) + v (\nabla \cdot (A \nabla u))
$$
将上式在区域 $\Omega$ 上积分，并对左侧项应用[广义散度定理](@entry_id:181016)，我们得到：
$$
\int_{\partial\Omega} v (A \nabla u) \cdot \mathbf{n} \, dS = \int_{\Omega} (A \nabla u) \cdot \nabla v \, dx + \int_{\Omega} v (\nabla \cdot (A \nabla u)) \, dx
$$
整理后即得[格林第一恒等式](@entry_id:170345)的广义形式 ：
$$
\int_{\Omega} (A \nabla u) \cdot \nabla v \, dx = \int_{\partial \Omega} v \, (A \nabla u) \cdot \mathbf{n} \, dS - \int_{\Omega} v \, \nabla \cdot (A \nabla u) \, dx
$$
这个恒等式成立，而**无需假设矩阵 $A$ 是对称的**。

在最常见的特例中，$A$ 是单位矩阵 $I$，算子 $\nabla \cdot (A \nabla u)$ 简化为拉普拉斯算子 $\Delta u$。此时，恒等式变为：
$$
\int_{\Omega} \nabla u \cdot \nabla v \, dx = \int_{\partial \Omega} v \frac{\partial u}{\partial n} \, dS - \int_{\Omega} v \Delta u \, dx
$$
其中 $\frac{\partial u}{\partial n} = \nabla u \cdot \mathbf{n}$ 是 $u$ 的[法向导数](@entry_id:169511)。

这个公式的严谨性依赖于函数和区域的正则性。在现代泛函分析的框架下，此恒等式的**最小正则性假设**为 ：
-   区域 $\Omega$ 是有界的 Lipschitz 域。
-   函数 $u \in H^1(\Omega)$ 且其拉普拉斯 $\Delta u \in L^2(\Omega)$。
-   函数 $v \in H^1(\Omega)$。

在这些假设下，边界项必须被理解为**对偶作用 (duality pairing)**。具体来说，$v$ 的迹 $\gamma(v)$ 属于 $H^{1/2}(\partial\Omega)$，而 $u$ 的（共轭）[法向导数](@entry_id:169511) $\frac{\partial u}{\partial n}$ 作为一个线性泛函属于其对偶空间 $H^{-1/2}(\partial\Omega)$。因此，边界积分被严谨地写为：
$$
\int_{\partial \Omega} v \frac{\partial u}{\partial n} \, dS \equiv \left\langle \frac{\partial u}{\partial n}, \gamma(v) \right\rangle_{H^{-1/2}(\partial\Omega), H^{1/2}(\partial\Omega)}
$$

#### [格林第二恒等式](@entry_id:169499)及其与自伴随性的联系

**[格林第二恒等式](@entry_id:169499) (Green's second identity)** 是通过交换 $u$ 和 $v$ 在第一恒等式中的角色并相减得到的。它揭示了拉普拉斯算子（或更一般的二阶[椭圆算子](@entry_id:181616)）在 $L^2$ [内积](@entry_id:158127)下的对称性。其形式为：
$$
\int_{\Omega} (u \Delta v - v \Delta u) \, dx = \int_{\partial \Omega} \left( u \frac{\partial v}{\partial n} - v \frac{\partial u}{\partial n} \right) \, dS
$$
用 $L^2(\Omega)$ [内积](@entry_id:158127) $(f,g)_{L^2} = \int_\Omega f g \, dx$ 来表示，上式可以写成：
$$
(u, \Delta v)_{L^2} - (\Delta u, v)_{L^2} = \int_{\partial \Omega} \left( u \frac{\partial v}{\partial n} - v \frac{\partial u}{\partial n} \right) \, dS
$$
一个算子 $L$ 被称为**对称的 (symmetric)** 或**形式自伴的 (formally self-adjoint)**，如果对于其定义域 $\mathcal{D}(L)$ 中的所有函数 $u, v$，都有 $(Lu, v) = (u, Lv)$。对于算子 $L = -\Delta$，其对称性条件为 $(-\Delta u, v)_{L^2} = (u, -\Delta v)_{L^2}$，这等价于[格林第二恒等式](@entry_id:169499)中的边界积分项为零 ：
$$
\int_{\partial \Omega} \left( u \frac{\partial v}{\partial n} - v \frac{\partial u}{\partial n} \right) \, dS = 0
$$
这个条件是否满足，完全取决于[算子定义域](@entry_id:275586) $\mathcal{D}(-\Delta)$ 所包含的**边界条件**。
-   **齐次狄利克雷 (Dirichlet) 边界条件**: $u=0, v=0$ on $\partial\Omega$。此时边界项显然为零。定义在 $\mathcal{D}(-\Delta) = \{u \in H^2(\Omega) \cap H^1_0(\Omega)\}$ 上的 $-\Delta$ 算子是自伴的。
-   **齐次诺伊曼 (Neumann) 边界条件**: $\frac{\partial u}{\partial n}=0, \frac{\partial v}{\partial n}=0$ on $\partial\Omega$。此时边界项也为零。定义在 $\mathcal{D}(-\Delta) = \{u \in H^2(\Omega) : \frac{\partial u}{\partial n}=0\}$ 上的 $-\Delta$ 算子也是自伴的。
-   **齐次罗宾 (Robin) 边界条件**: $\frac{\partial u}{\partial n} + \beta u = 0, \frac{\partial v}{\partial n} + \beta v = 0$ on $\partial\Omega$（其中 $\beta \ge 0$）。代入边界项得到 $\int_{\partial\Omega} (u(-\beta v) - v(-\beta u)) dS = 0$。因此，相应的 $-\Delta$ 算子也是自伴的。

因此，自伴随性并非算子本身的固有属性，而是**算子与其定义域（即边界条件）共同决定的**。这个性质对解的存在性、唯一性以及特征值问题（频谱理论）的研究具有深远的影响。

### 在[偏微分方程理论](@entry_id:189232)与数值计算中的应用

[格林恒等式](@entry_id:176369)不仅是理论分析的工具，更是连接强形式PDE和其[数值近似](@entry_id:161970)（如[有限元法](@entry_id:749389)）的桥梁。

#### 弱形式的推导：[本质边界条件与自然边界条件](@entry_id:146051)

考虑一个一般的二阶椭圆[边值问题](@entry_id:193901)：
$$
-\nabla \cdot (a \nabla u) = f \quad \text{in } \Omega
$$
边界 $\partial\Omega$ 被划分为 $\Gamma_D$ 和 $\Gamma_N$，分别施加狄利克雷和[诺伊曼条件](@entry_id:165471)：
$$
u = g \quad \text{on } \Gamma_D, \qquad a \frac{\partial u}{\partial n} = h \quad \text{on } \Gamma_N
$$
推导其**[弱形式](@entry_id:142897) (weak formulation)** 的标准流程是：将原PDE乘以一个合适的**[检验函数](@entry_id:166589) (test function)** $v$，然后在 $\Omega$ 上积分，并利用[格林第一恒等式](@entry_id:170345)进行分部积分。
$$
\int_{\Omega} a \nabla u \cdot \nabla v \, dx - \int_{\partial \Omega} v (a \nabla u \cdot n) \, dS = \int_{\Omega} f v \, dx
$$
此时，边界条件的处理方式揭示了两种边界条件的根本区别 ：

1.  **本质边界条件 (Essential Boundary Conditions)**: [狄利克雷条件](@entry_id:137096) $u=g$ on $\Gamma_D$ 被称为本质条件。它直接对解函数本身提出要求。在[弱形式](@entry_id:142897)中，它通过限制**[试探空间](@entry_id:756166) (trial space)** 来“强行”施加。我们寻找的解 $u$ 必须属于一个[仿射空间](@entry_id:152906) $V_g = \{ w \in H^1(\Omega) \mid \gamma(w) = g \text{ on } \Gamma_D \}$。为了消除边界积分中未知的[法向导数](@entry_id:169511)项 $\int_{\Gamma_D} v (a \nabla u \cdot n) \, dS$，我们选择的**检验空间 (test space)** $V_0$ 中的函数必须在 $\Gamma_D$ 上为零，即 $V_0 = \{ v \in H^1(\Omega) \mid \gamma(v) = 0 \text{ on } \Gamma_D \}$。这样，该边界积分项就自动消失了。

2.  **自然边界条件 (Natural Boundary Conditions)**: [诺伊曼条件](@entry_id:165471) $a \frac{\partial u}{\partial n} = h$ on $\Gamma_N$ 被称为自然条件。它对解的导数（通量）提出要求。在弱形式中，它并不限制[函数空间](@entry_id:143478)，而是“自然地”融入到积分方程中。我们将已知的 $h$ 代入边界积分项，得到 $\int_{\Gamma_N} v h \, dS$。

经过上述处理，最终的弱形式为：求 $u \in V_g$，使得对于所有 $v \in V_0$，
$$
\int_{\Omega} a \nabla u \cdot \nabla v \, dx = \int_{\Omega} f v \, dx + \int_{\Gamma_N} h v \, dS
$$
这个方程可以抽象地写成 $B(u,v) = L(v)$，其中 $B(u,v) = \int_{\Omega} a \nabla u \cdot \nabla v \, dx$ 是**双线性形式 (bilinear form)**，而 $L(v) = \int_{\Omega} f v \, dx + \int_{\Gamma_N} h v \, dS$ 是**[线性泛函](@entry_id:276136) (linear functional)**。诺伊曼数据 $h$ 改变了线性泛函，而狄利克雷数据 $g$ 改变了[试探空间](@entry_id:756166)。

**示例：[泊松方程](@entry_id:143763)的[弱形式](@entry_id:142897)**
考虑一个典型的模型问题：[泊松方程](@entry_id:143763) $-\Delta u = f$ 加上齐次狄利克雷边界条件 $u=0$ on $\partial\Omega$ 。
-   **[试探空间](@entry_id:756166)**: 由于 $u=0$ on $\partial\Omega$，我们寻找的解 $u$ 属于 $H_0^1(\Omega)$（迹为零的 $H^1$ [函数空间](@entry_id:143478)）。
-   **检验空间**: 在伽辽金 (Galerkin) 方法中，检验空间与[试探空间](@entry_id:756166)相同，即 $v \in H_0^1(\Omega)$。
-   **推导**: 应用[格林第一恒等式](@entry_id:170345)，边界项 $\int_{\partial\Omega} v \frac{\partial u}{\partial n} dS$ 因为 $v$ 的迹为零而消失。
于是，弱形式为：求 $u \in H_0^1(\Omega)$，使得对于所有 $v \in H_0^1(\Omega)$，
$$
\int_{\Omega} \nabla u \cdot \nabla v \, dx = \int_{\Omega} f v \, dx
$$
这里的[双线性形式](@entry_id:746794) $a(u,v) = \int_{\Omega} \nabla u \cdot \nabla v \, dx$ 是对称且正定的（在 $H_0^1(\Omega)$ 上），这保证了通过[Lax-Milgram定理](@entry_id:137966)可以得到唯一解，并导致[有限元离散化](@entry_id:193156)后产生对称正定的刚度矩阵。

#### 积分表示公式

[格林恒等式](@entry_id:176369)的另一个强大应用是推导解的积分表示，这构成了**[边界元法](@entry_id:141290) (Boundary Element Method, BEM)** 的理论基础。其核心思想是利用算子的**基本解 (fundamental solution)**。

拉普拉斯算子的基本解 $\Phi(x,y)$ 是满足 $-\Delta_y \Phi(x,y) = \delta_x(y)$ 的[分布](@entry_id:182848)，其中 $\delta_x$ 是位于点 $x$ 的[狄拉克测度](@entry_id:197577)。在物理上，它代表了在点 $x$ 处放置一个单位点源所产生的势。

现在，对于区域 $\Omega$ 内的一个**调和函数** (harmonic function) $u$（即 $\Delta u = 0$），我们在[格林第二恒等式](@entry_id:169499)中令 $v(y) = \Phi(x,y)$，其中 $x$ 是 $\Omega$ 内的一个[固定点](@entry_id:156394)。利用 $\Delta u = 0$ 和 $\Delta_y \Phi(x,y) = -\delta_x(y)$，恒等式的左边变为 ：
$$
\int_{\Omega} \big(u(y) \Delta_y \Phi(x,y) - \Phi(x,y) \Delta_y u(y) \big) \, dy = \int_{\Omega} u(y) (-\delta_x(y)) \, dy = -u(x)
$$
于是，我们得到：
$$
-u(x) = \int_{\partial \Omega} \left( u(y) \frac{\partial \Phi(x,y)}{\partial n_y} - \Phi(x,y) \frac{\partial u(y)}{\partial n_y} \right) \, dS_y
$$
整理后得到**格林表示公式 (Green's representation formula)**：
$$
u(x) = \int_{\partial \Omega} \left( \Phi(x,y) \frac{\partial u(y)}{\partial n_y} - u(y) \frac{\partial \Phi(x,y)}{\partial n_y} \right) \, dS_y
$$
这个惊人的公式表明，区域内部任意一点的调和函数值 $u(x)$ 完全由其在边界上的值（狄利克雷数据 $u|_{\partial\Omega}$）和[法向导数](@entry_id:169511)值（诺伊曼数据 $\frac{\partial u}{\partial n}|_{\partial\Omega}$）所决定。这揭示了问题的维度可以降低一维：求解一个 $n$ 维的体问题可以转化为求解一个 $(n-1)$ 维的[边界积分方程](@entry_id:746942)。