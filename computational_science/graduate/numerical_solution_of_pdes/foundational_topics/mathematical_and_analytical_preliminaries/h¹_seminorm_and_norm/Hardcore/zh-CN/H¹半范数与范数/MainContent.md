## 引言
在[偏微分方程](@entry_id:141332) (PDE) 的现代分析与数值求解中，[H¹半范数](@entry_id:750495)与[H¹范数](@entry_id:750494)是索博列夫空间理论中两个不可或缺的核心工具。它们为量化函数及其导数的行为提供了精确的数学语言，是理解[PDE解](@entry_id:166250)的正则性、稳定性和设计可靠数值算法的基石。然而，对于初学者而言，这两个度量之间的细微差别、深刻联系及其在物理和计算中的实际意义往往构成了一个知识缺口。为何有时仅用[半范数](@entry_id:264573)就足够，而在其他情况下则必须使用完整的范数？这种选择背后又蕴含着怎样的物理和数学原理？

本文旨在系统地回答这些问题，为读者构建一个关于[H¹半范数](@entry_id:750495)与范数的完整知识框架。我们将通过三个章节的递进式学习，带领读者从基本原理走向前沿应用：

*   在**第一章：原理与机制**中，我们将从基本定义出发，揭示[H¹半范数](@entry_id:750495)的物理本质——它如何与系统的能量直接关联。随后，我们将深入探讨其核心数学性质，阐明为何它只是一个“半”范数，并通过[庞加莱不等式](@entry_id:142086)揭示它在特定约束下如何与完整的[H¹范数](@entry_id:750494)等价，以及这种等价性对保证PDE问题良定性的关键作用。

*   在**第二章：应用与跨学科联系**中，我们将展示这些理论在实践中的强大威力。读者将看到[H¹范数](@entry_id:750494)如何成为[有限元误差分析](@entry_id:749282)的自然尺度，指导从[自适应网格](@entry_id:164379)到[迭代求解器](@entry_id:136910)的[算法设计](@entry_id:634229)，并作为一种统一的语言，连接固体力学、[流体动力学](@entry_id:136788)、优化理论乃至[科学机器学习](@entry_id:145555)等多个学科领域。

*   在**第三章：动手实践**中，我们将理论付诸实践，通过一系列精心设计的计算练习，帮助读者手动计算范数、理解其在坐标变换下的行为，并编写代码进行[数值验证](@entry_id:156090)，从而将抽象知识转化为具体的计算技能。

通过本次学习，您不仅将掌握[H¹半范数](@entry_id:750495)与范数的定义与理论，更将深刻理解它们如何成为连接物理世界、数学理论与高效计算的桥梁。

## 原理与机制

在[偏微分方程](@entry_id:141332) (PDE) 的现代理论和数值分析中，[索博列夫空间](@entry_id:141995) (Sobolev space) 提供了一个基础框架，用于分析解的存在性、唯一性和性质。其中，一阶[索博列夫空间](@entry_id:141995) $H^1(\Omega)$ 尤为重要，它自然地出现在许多物理问题的[变分形式](@entry_id:166033)中。本章旨在深入探讨 $H^1$ [半范数](@entry_id:264573)和 $H^1$ 范数的原理与机制，它们是理解和量化 $H^1(\Omega)$ 空间中函数行为的核心工具。我们将从基本定义出发，揭示它们的物理意义，探讨它们在何种条件下等价，并阐明这种等价性如何保证[偏微分方程数值解](@entry_id:753287)的稳定性和收敛性。

### 基本定义与关系

我们考虑一个位于 $\mathbb{R}^d$ ($d \ge 1$) 中的有界开集 $\Omega$，其边界 $\partial\Omega$ 至少是利普希茨 (Lipschitz) 连续的。函数空间 $L^2(\Omega)$ 包含所有在 $\Omega$ 上平方可积的函数，其范数为：
$$
\|u\|_{L^2(\Omega)} = \left( \int_{\Omega} |u(x)|^2 \, \mathrm{d}x \right)^{1/2}
$$

**一阶索博列夫空间** $H^1(\Omega)$ 由 $L^2(\Omega)$ 中所有其[弱导数](@entry_id:189356) (weak derivatives) 也属于 $L^2(\Omega)$ 的函数构成。换言之，对于一个函数 $u \in L^2(\Omega)$，如果存在一个向量场 $g \in (L^2(\Omega))^d$ 满足如下积分等式（[分部积分](@entry_id:136350)的推广）：
$$
\int_{\Omega} u (\nabla \cdot \phi) \, \mathrm{d}x = - \int_{\Omega} g \cdot \phi \, \mathrm{d}x
$$
对于所有具有[紧支集](@entry_id:276214)的无限[可微函数](@entry_id:144590) $\phi \in C_c^\infty(\Omega)$ 均成立，那么我们就称 $g$ 为 $u$ 的[弱梯度](@entry_id:756667)，记作 $\nabla u$。$H^1(\Omega)$ 空间的定义可以形式化地写为：
$$
H^1(\Omega) = \{ u \in L^2(\Omega) : \nabla u \in (L^2(\Omega))^d \}
$$

基于此，我们可以定义两个关键的度量：**$H^1$ [半范数](@entry_id:264573) (seminorm)** 和 **$H^1$ 范数 (norm)**。

**$H^1$ [半范数](@entry_id:264573)**，记作 $|u|_{H^1(\Omega)}$，只度量函数梯度的“大小”，其定义为梯度的 $L^2$ 范数：
$$
|u|_{H^1(\Omega)} := \|\nabla u\|_{L^2(\Omega)} = \left( \int_{\Omega} |\nabla u(x)|^2 \, \mathrm{d}x \right)^{1/2}
$$

**$H^1$ 范数**，记作 $\|u\|_{H^1(\Omega)}$，则同时度量函数自身及其梯度的大小，通常定义为两者 $L^2$ 范数的平方和的平方根，这赋予了 $H^1(\Omega)$ 一个希尔伯特空间 (Hilbert space) 结构：
$$
\|u\|_{H^1(\Omega)} := \left( \|u\|_{L^2(\Omega)}^2 + |u|_{H^1(\Omega)}^2 \right)^{1/2}
$$
这个定义在数学上等价于其他形式，例如 $\|u\|_{L^2(\Omega)} + |u|_{H^1(\Omega)}$，因为在[向量空间](@entry_id:151108)上，所有这些范数都是等价的 。在实际应用中，采用平方和的形式更为普遍。值得注意的是，在文献中，$H^1(\Omega)$ 空间有时也记作 $W^{1,2}(\Omega)$，根据 Meyers-Serrin 定理，这两个基于不同构造方式（$W^{1,2}$ 基于[弱导数](@entry_id:189356)定义，$H^1$ 基于[光滑函数](@entry_id:267124)完备化定义）的空间在具有[利普希茨边界](@entry_id:184843)的区域上是等同的 。

通过这些定义，我们立刻可以观察到[半范数](@entry_id:264573)和范数之间的基本关系：$|u|_{H^1(\Omega)} \le \|u\|_{H^1(\Omega)}$。然而，反向的不等式并不普遍成立，这正是 $H^1$ [半范数](@entry_id:264573)与范数理论的核心所在 。

### [半范数](@entry_id:264573)的物理意义：能量与形变

$H^1$ [半范数](@entry_id:264573)并非纯粹的数学抽象，它在物理学和工程学中有着深刻的根源，通常与系统的 **[应变能](@entry_id:162699) (strain energy)** 或 **能量耗散 (energy dissipation)** 直接相关。一个典型的例子是线弹性力学 。

考虑一个二维弹性体 $\Omega \subset \mathbb{R}^2$ 的 **平面外 (antiplane) 剪切形变**。此时，[位移场](@entry_id:141476)具有特殊形式 $w(x_1, x_2, x_3) = (0, 0, u(x_1, x_2))$，其中 $u$ 是仅依赖于 $x_1, x_2$ 的平面外位移。在这种情况下，[应变张量](@entry_id:193332) $\varepsilon$ 的非零分量仅为：
$$
\varepsilon_{13} = \frac{1}{2} \frac{\partial u}{\partial x_1}, \quad \varepsilon_{23} = \frac{1}{2} \frac{\partial u}{\partial x_2}
$$
对于一个具有[剪切模量](@entry_id:167228) $\mu$ 的均匀[各向同性材料](@entry_id:170678)，其[应力张量](@entry_id:148973) $\sigma$ 与应变张量成正比，即 $\sigma = 2\mu\varepsilon$（因为该形变是保体积的，即 $\mathrm{tr}(\varepsilon)=0$）。系统的总弹性应变能 $E(u)$ 是[应变能密度](@entry_id:200085)在整个区域上的积分，可以计算得出：
$$
E(u) = \int_{\Omega} \frac{1}{2} \sigma : \varepsilon \, \mathrm{d}x = \int_{\Omega} \mu \varepsilon : \varepsilon \, \mathrm{d}x = \int_{\Omega} \mu (2 \varepsilon_{13}^2 + 2 \varepsilon_{23}^2) \, \mathrm{d}x = \frac{1}{2}\mu \int_{\Omega} \left( \left(\frac{\partial u}{\partial x_1}\right)^2 + \left(\frac{\partial u}{\partial x_2}\right)^2 \right) \, \mathrm{d}x
$$
最终我们得到一个简洁而深刻的表达式：
$$
E(u) = \frac{1}{2}\mu \int_{\Omega} |\nabla u|^2 \, \mathrm{d}x = \frac{1}{2}\mu |u|_{H^1(\Omega)}^2
$$
这个结果表明，系统的[弹性应变能](@entry_id:202243)正比于位移场 $u$ 的 $H^1$ [半范数](@entry_id:264573)的平方。因此，$|u|_{H^1(\Omega)}$ 直接量化了物体的形变程度。

### [半范数](@entry_id:264573)的核：刚体位移

一个关键问题是：$H^1$ [半范数](@entry_id:264573)是否是一个真正的范数？一个范数必须满足正定性，即 $\|v\|=0$ 当且仅当 $v=0$。然而，$|u|_{H^1(\Omega)}=0$ 意味着 $\int_{\Omega} |\nabla u|^2 \, \mathrm{d}x = 0$，这等价于 $\nabla u = 0$ 在 $\Omega$ 上[几乎处处](@entry_id:146631)成立。

对于一个连通区域，梯度为零的函数必然是[常数函数](@entry_id:152060)，即 $u(x) = C$。对于一个由多个不相交的连通子区域 $\Omega_i$ 组成的非连通区域，梯度为零的函数是在每个子区域上取不同常数值的函数 。
$$
u(x) = \sum_{i} C_i \chi_{\Omega_i}(x)
$$
其中 $\chi_{\Omega_i}$ 是子区域 $\Omega_i$ 的特征函数。

这些使得[半范数](@entry_id:264573)为零的非零函数构成了 **[半范数](@entry_id:264573)的核 (kernel)**。在物理上，一个常数位移 $u=C$ 对应于整个物体的 **刚体平移 (rigid body translation)**，它不产生任何内部形变，因此不储存任何[应变能](@entry_id:162699) 。由于存在这些非零的“零能量”状态，所以 $|u|_{H^1(\Omega)}$ 在整个 $H^1(\Omega)$ 空间上只是一个[半范数](@entry_id:264573)，而不是一个范数。

### 从[半范数](@entry_id:264573)到范数：约束的重要性

尽管 $H^1$ [半范数](@entry_id:264573)在整个 $H^1(\Omega)$ 空间上不是一个范数，但在许多重要的[子空间](@entry_id:150286)上，它却能成为一个真正的、且与完整 $H^1$ [范数等价](@entry_id:137561)的范数。这种转变的关键在于施加适当的约束来“消除”[半范数](@entry_id:264573)核中的非零函数。

#### 1. 齐次[狄利克雷边界条件](@entry_id:173524) (Homogeneous Dirichlet Conditions)

考虑[子空间](@entry_id:150286) $H_0^1(\Omega)$，它是 $H^1(\Omega)$ 中在边界 $\partial\Omega$ 上迹为零的函数的[闭包](@entry_id:148169)。这个空间通常用于模拟那些在边界上被固定的系统（例如，边缘固定的膜的[振动](@entry_id:267781)）。如果一个函数 $u \in H_0^1(\Omega)$ 并且 $|u|_{H^1(\Omega)}=0$，我们知道 $u$ 必须是一个常数 $C$。但由于 $u$ 在边界上的值为零，所以这个常数必须是 $C=0$。因此，在 $H_0^1(\Omega)$ 空间中，$|u|_{H^1(\Omega)}=0$ 意味着 $u=0$，这表明 $H^1$ [半范数](@entry_id:264573)在该[子空间](@entry_id:150286)上是一个真正的范数 。

#### 2. 零均值约束 (Zero-Mean Constraint)

在处理纯诺伊曼 (Neumann) 边界问题的场景中（例如，热流问题中边界绝热），解空间通常是整个 $H^1(\Omega)$，其解的任意常数叠加仍然是解。为了确保唯一性，通常会施加一个额外的约束，例如要求解的平均值为零。考虑[子空间](@entry_id:150286) $V = \{ u \in H^1(\Omega) : \int_{\Omega} u \, \mathrm{d}x = 0 \}$。如果一个函数 $u \in V$ 且 $|u|_{H^1(\Omega)}=0$，那么 $u$ 必须是一个常数 $C$。将其代入零均值约束中，我们得到：
$$
\int_{\Omega} C \, \mathrm{d}x = C \cdot \text{meas}(\Omega) = 0
$$
因为区域 $\Omega$ 的测度 $\text{meas}(\Omega)$ 是正的，所以必须有 $C=0$。同样，[半范数](@entry_id:264573)在这个[子空间](@entry_id:150286)上也是一个范数 。

#### 3. [罗宾边界条件](@entry_id:163914) (Robin Boundary Conditions)

另一种“固定”函数的方法是通过在边界的一部分上施加惩罚。考虑一个范数，它结合了内部的[半范数](@entry_id:264573)和边界上的一个项，例如在边界的某一部分 $\Gamma$ 上定义一个范数 ：
$$
\|u\|_{R} := \left( |u|_{H^1(\Omega)}^2 + \alpha \int_{\Gamma} |u|^2 \, \mathrm{d}s \right)^{1/2}
$$
其中 $\alpha > 0$ 且 $\Gamma$ 具有正测度。如果 $\|u\|_R=0$，那么 $\nabla u=0$ 并且 $u$ 在 $\Gamma$ 上的积分为零。前者意味着 $u$ 是常数 $C$，后者则迫使 $C=0$。因此，这个包含了边界积分的量也是 $H^1(\Omega)$ 上的一个范数。

### [范数等价](@entry_id:137561)性与[庞加莱不等式](@entry_id:142086)

我们已经看到，在特定[子空间](@entry_id:150286)上，$H^1$ [半范数](@entry_id:264573)可以成为一个范数。一个更深刻的问题是：这个由[半范数](@entry_id:264573)定义的范数是否与原始的 $H^1$ [范数等价](@entry_id:137561)？两个范数 $\| \cdot \|_a$ 和 $\| \cdot \|_b$ 等价，是指存在正常数 $c_1, c_2$ 使得对所有函数 $u$，都有 $c_1 \|u\|_a \le \|u\|_b \le c_2 \|u\|_a$。[范数等价](@entry_id:137561)性是一个至关重要的性质，因为它保证了空间的拓扑结构不依赖于我们选择哪个范数。

[范数等价](@entry_id:137561)性的关键在于 **[庞加莱不等式](@entry_id:142086) (Poincaré inequality)**。

**庞加莱-弗里德里希不等式 (Poincaré-Friedrichs inequality)** 指出，对于一个有界区域 $\Omega$，存在一个仅依赖于 $\Omega$ 的常数 $C_P > 0$，使得对于所有 $u \in H_0^1(\Omega)$，都有：
$$
\|u\|_{L^2(\Omega)} \le C_P |u|_{H^1(\Omega)}
$$
这个不等式表明，只要一个函数在边界上为零，我们就可以通过其梯度的大小（形变）来控制其自身的整体大小。利用这个不等式，我们可以证明 $|u|_{H^1(\Omega)}$ 和 $\|u\|_{H^1(\Omega)}$ 在 $H_0^1(\Omega)$ 上的等价性 [@problem_id:3402640, @problem_id:3402650]：
$$
\|u\|_{H^1(\Omega)}^2 = \|u\|_{L^2(\Omega)}^2 + |u|_{H^1(\Omega)}^2 \le (C_P^2 + 1) |u|_{H^1(\Omega)}^2
$$
结合另一方向的显然不等式 $|u|_{H^1(\Omega)}^2 \le \|u\|_{H^1(\Omega)}^2$，我们便确立了[范数等价](@entry_id:137561)性。

类似地，对于零[均值函数](@entry_id:264860)空间，**庞加莱-维廷格不等式 (Poincaré-Wirtinger inequality)** 也提供了类似 $\|u-\bar{u}\|_{L^2(\Omega)} \le C_{PW} |u|_{H^1(\Omega)}$ 的估计，其中 $\bar{u}$ 是 $u$ 的平均值。对于属于零均值[子空间](@entry_id:150286)的函数，这直接导致了[范数等价](@entry_id:137561)性 。

**重要警示：有界区域的必要性**
[庞加莱不等式](@entry_id:142086)及其推论严重依赖于区域 $\Omega$ 的 **有界性**。在无界区域（例如整个 $\mathbb{R}^n$）上，这个不等式不成立。我们可以构造一个[函数序列](@entry_id:145607)，其 $L^2$ 范数保持不变，而 $H^1$ [半范数](@entry_id:264573)可以任意小。例如，考虑函数族 $u_R(x) = \exp(-|x|^2 / (2R^2))$ 。随着 $R \to \infty$，函数图像变得越来越“平坦”和“宽广”，其梯度趋于零，但其 $L^2$ 范数却在增长。具体计算表明，比值 $\|u_R\|_{L^2} / |u_R|_{H^1}$ 与 $R$ 成正比，当 $R \to \infty$ 时趋于无穷大。这表明在 $\mathbb{R}^n$ 上不存在一个统一的常数 $C$ 使得 $\|u\|_{L^2} \le C |u|_{H^1}$ 对所有 $u \in H^1(\mathbb{R}^n)$ 成立。

### 应用：[变分形式](@entry_id:166033)的[矫顽性](@entry_id:159399)

[范数等价](@entry_id:137561)性的核心重要性体现在[偏微分方程](@entry_id:141332)的变分理论中，特别是与 **矫顽性 (coercivity)** 的概念相关。考虑一个典型的椭圆型方程，如泊松方程 $-\Delta u = f$，其[弱形式](@entry_id:142897)通常涉及一个双线性形式 $a(u,v)$。对于[拉普拉斯算子](@entry_id:146319)，这个双线性形式恰好是：
$$
a(u,v) = \int_{\Omega} \nabla u \cdot \nabla v \, \mathrm{d}x
$$
显然，$a(u,u) = |u|_{H^1(\Omega)}^2$。

根据 Lax-Milgram 定理，一个[变分问题](@entry_id:756445)是良定义的（即存在唯一解），一个关键条件是[双线性形式](@entry_id:746794) $a(u,v)$ 在相应的函数空间上是矫顽的。对于空间 $V$ 上的 $H^1$ 范数，矫顽性意味着存在一个常数 $\alpha > 0$，使得：
$$
a(u,u) \ge \alpha \|u\|_{H^1(V)}^2 \quad \forall u \in V
$$
将 $a(u,u) = |u|_{H^1(\Omega)}^2$ 代入，我们发现[矫顽性](@entry_id:159399)条件就是 $|u|_{H^1(\Omega)}^2 \ge \alpha \|u\|_{H^1(\Omega)}^2$。这正是我们之前讨论的[范数等价](@entry_id:137561)性不等式！

因此，我们可以得出以下结论 ：
- 在 $H_0^1(\Omega)$ 上，由于[庞加莱不等式](@entry_id:142086)保证了[范数等价](@entry_id:137561)性，双线性形式 $a(u,v) = \int \nabla u \cdot \nabla v \, \mathrm{d}x$ 是矫顽的。这保证了齐次[狄利克雷问题](@entry_id:274408)的良定性。
- 在整个 $H^1(\Omega)$ 上，$a(u,v)$ 不是矫顽的，因为常数函数的存在破坏了[范数等价](@entry_id:137561)性。
- 在零均值[子空间](@entry_id:150286)上，庞加莱-维廷格不等式同样保证了[矫顽性](@entry_id:159399)，这对于纯[诺伊曼问题](@entry_id:176713)的分析至关重要。
- 如果我们修改[双线性形式](@entry_id:746794)，加入一个“质量项”，例如 $a_{\beta}(u,v) = \int \nabla u \cdot \nabla v \, \mathrm{d}x + \beta \int u v \, \mathrm{d}x$（其中 $\beta > 0$），那么这个新的形式在整个 $H^1(\Omega)$ 空间上都是矫顽的，因为 $a_{\beta}(u,u) = |u|_{H^1(\Omega)}^2 + \beta \|u\|_{L^2(\Omega)}^2 \ge \min(1, \beta) \|u\|_{H^1(\Omega)}^2$。

### 在有限元方法中的离散表示

当使用有限元方法 (FEM) 求解偏微分方程时，连续的函数空间 $V$ 被离散的有限维[子空间](@entry_id:150286) $V_h \subset V$ 所取代。设 $\{\phi_i\}_{i=1}^N$ 是 $V_h$ 的一组[基函数](@entry_id:170178)（例如，[节点基](@entry_id:752522)函数），那么 $V_h$ 中的任意函数 $u_h$ 都可以表示为系数向量 $\mathbf{u}$ 与[基函数](@entry_id:170178)的线性组合：$u_h = \sum_{i=1}^N \mathbf{u}_i \phi_i$。

在这种离散设定下，$H^1$ [半范数](@entry_id:264573)和 $L^2$ 范数可以方便地用矩阵和向量的二次型来表示 [@problem_id:3402649, @problem_id:3402644]。

$u_h$ 的 $L^2$ 范数平方为：
$$
\|u_h\|_{L^2(\Omega)}^2 = \int_{\Omega} \left(\sum_i \mathbf{u}_i \phi_i\right) \left(\sum_j \mathbf{u}_j \phi_j\right) \, \mathrm{d}x = \sum_{i,j} \mathbf{u}_i \mathbf{u}_j \int_{\Omega} \phi_i \phi_j \, \mathrm{d}x = \mathbf{u}^\top M \mathbf{u}
$$
其中 $M$ 是 **质量矩阵 (mass matrix)**，其元素为 $M_{ij} = \int_{\Omega} \phi_i \phi_j \, \mathrm{d}x$。

$u_h$ 的 $H^1$ [半范数](@entry_id:264573)平方为：
$$
|u_h|_{H^1(\Omega)}^2 = \int_{\Omega} |\nabla u_h|^2 \, \mathrm{d}x = \int_{\Omega} \left(\sum_i \mathbf{u}_i \nabla \phi_i\right) \cdot \left(\sum_j \mathbf{u}_j \nabla \phi_j\right) \, \mathrm{d}x = \sum_{i,j} \mathbf{u}_i \mathbf{u}_j \int_{\Omega} \nabla \phi_i \cdot \nabla \phi_j \, \mathrm{d}x = \mathbf{u}^\top K \mathbf{u}
$$
其中 $K$ 是 **刚度矩阵 (stiffness matrix)**，其元素为 $K_{ij} = \int_{\Omega} \nabla \phi_i \cdot \nabla \phi_j \, \mathrm{d}x$。

因此，$u_h$ 的 $H^1$ 范数平方就是这两个二次型的和：
$$
\|u_h\|_{H^1(\Omega)}^2 = \|u_h\|_{L^2(\Omega)}^2 + |u_h|_{H^1(\Omega)}^2 = \mathbf{u}^\top M \mathbf{u} + \mathbf{u}^\top K \mathbf{u} = \mathbf{u}^\top (M+K) \mathbf{u}
$$
这种[代数表示](@entry_id:143783)是有限元方法的核心，它将无穷维的[泛函分析](@entry_id:146220)问题转化为了有限维的线性代数问题。例如，离散的[庞加莱不等式](@entry_id:142086)和[稳定性估计](@entry_id:755306)都与[刚度矩阵](@entry_id:178659) $K$ 和质量矩阵 $M$ 的谱性质（特别是[特征值](@entry_id:154894)）密切相关 。

### 扩展概念

#### [索博列夫嵌入定理](@entry_id:192380) (Sobolev Embedding Theorems)

$H^1$ 范数的重要性不仅在于它与能量和[矫顽性](@entry_id:159399)的联系，还在于它能[控制函数](@entry_id:183140)在其他范数下的行为。[索博列夫嵌入定理](@entry_id:192380)精确地描述了这一点。例如，在有界利普希茨区域 $\Omega$ 上 ：
- 在一维 ($d=1$)， $H^1(\Omega)$ 中的函数可以被嵌入到[连续函数空间](@entry_id:150395) $C^0(\bar{\Omega})$ 中，这意味着 $H^1$ 函数（在修正后）是连续的。
- 在二维 ($d=2$)， $H^1(\Omega)$ 可以嵌入到任意的 $L^p(\Omega)$ 空间（对于所有 $1 \le p  \infty$）。
- 在三维 ($d=3$)， $H^1(\Omega)$ 可以嵌入到 $L^6(\Omega)$ 空间。这意味着存在一个常数 $C$ 使得 $\|u\|_{L^6(\Omega)} \le C \|u\|_{H^1(\Omega)}$。

这些[嵌入定理](@entry_id:150872)非常强大，它们表明一个具有有限 $H^1$ 范数的函数，其“奇异性”是受限的。

#### [迹定理](@entry_id:203967)与边界值 (Trace Theorem and Boundary Values)

对于 $H^1(\Omega)$ 中的函数，其在边界 $\partial\Omega$ 上的值（称为 **迹 (trace)**）是良定义的。**[迹定理](@entry_id:203967) (Trace Theorem)** 保证了[迹算子](@entry_id:183665) $T: H^1(\Omega) \to L^2(\partial\Omega)$ 是一个有界（连续）线性算子。这意味着我们可以控制边界上的函数大小：$\|u\|_{L^2(\partial\Omega)} \le C_T \|u\|_{H^1(\Omega)}$。这个定理是处理[非齐次边界条件](@entry_id:750645)和边界积分的基础，它确保了诸如 $\int_{\Gamma} u \, v \, ds$ 这样的项在[变分形式](@entry_id:166033)中是良定义的和连续的 。

#### 破碎[索博列夫空间](@entry_id:141995) (Broken Sobolev Spaces)

在[非协调有限元方法](@entry_id:752621)（如不[连续伽辽金方法](@entry_id:747805)，DG）中，函数在单元之间可以是不连续的。在这种情况下，我们使用 **破碎 $H^1$ 空间** $H^1(\mathcal{T}_h) = \prod_{K \in \mathcal{T}_h} H^1(K)$，其中 $\mathcal{T}_h$ 是区域的剖分。**破碎 $H^1$ [半范数](@entry_id:264573)** 被定义为单元上[半范数](@entry_id:264573)的平方和 ：
$$
|v|_{H^1(\mathcal{T}_h)}^2 = \sum_{K \in \mathcal{T}_h} \| \nabla v \|_{L^2(K)}^2
$$
这个[半范数](@entry_id:264573)的核是所有在每个单元上为常数的函数（即分片[常数函数](@entry_id:152060)）。由于它对单元间的跳跃不敏感，为了构造一个有用的范数，DG 方法必须额外引入惩罚项来约束这些跳跃。这与[协调有限元](@entry_id:170866)方法形成了鲜明对比，在协调方法中，函数属于 $H^1(\Omega)$ 的连续性要求已经内在地处理了单元间的耦合。