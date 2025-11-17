## 引言
[边界元法](@entry_id:141290)（Boundary Element Method, BEM）是[求解偏微分方程](@entry_id:138485)的一种强大而优雅的数值技术，在[计算地球物理学](@entry_id:747618)等众多科学与工程领域中占据着不可或缺的地位。传统上，[有限元法](@entry_id:749389)（FEM）或有限差分法（FDM）等域方法需要对整个问题域进行网格剖分，这在处理无限或[半无限域](@entry_id:175316)问题（如[地震波](@entry_id:164985)向[远场](@entry_id:269288)传播或地壳在无限弹性介质中的变形）时会遇到巨大挑战。[边界元法](@entry_id:141290)通过其独特的数学构造，巧妙地绕开了这一难题，构成了本文旨在填补的知识核心。

本文将带领读者系统地探索[边界元法](@entry_id:141290)的世界。您将首先深入其理论核心，在“原理与机制”一章中理解如何利用[格林公式](@entry_id:173118)将[偏微分方程](@entry_id:141332)[降维](@entry_id:142982)为[边界积分方程](@entry_id:746942)。接着，在“应用与跨学科连接”一章中，您将看到这些理论如何在[地球物理学](@entry_id:147342)的具体问题（如断层反演、波散射和多物理场耦合）中大放异彩。最后，“动手实践”部分将通过一系列精心设计的计算问题，引导您直面并解决实现BEM时遇到的关键数值挑战。通过这一结构化的学习路径，您将全面掌握[边界元法](@entry_id:141290)的理论精髓与应用技巧。

## 原理与机制

本章在前一章介绍性概述的基础上，深入探讨[边界元法 (BEM)](@entry_id:746941) 的核心科学原理与计算机制。我们将从其数学基础——[格林公式](@entry_id:173118)与基本解——出发，构建[边界积分方程](@entry_id:746942) (BIE)，并详细阐明在求解不同类型的地球物理问题时所需的关键概念与技术。本章旨在为读者提供一个严谨而系统的理论框架，为后续章节中更高级的应用和[算法分析](@entry_id:264228)奠定基础。

### 从[偏微分方程](@entry_id:141332)到[边界积分方程](@entry_id:746942)

[边界元法](@entry_id:141290)的核心思想是将一个在域 $\Omega$ 内定义的[偏微分方程](@entry_id:141332) (PDE) 转化为一个仅涉及其边界 $\Gamma$ 的积分方程。这一降维特性是 BEM 最显著的优势，尤其适用于具有高表面积体积比或无限/[半无限域](@entry_id:175316)的地球物理问题。实现这一转化的关键数学工具是**格林第二公式**。

对于定义在域 $\Omega$ 上的两个足够光滑的标量场 $u(\mathbf{y})$ 和 $v(\mathbf{y})$，格林第二公式表述为：
$$
\int_{\Omega} \left( u \nabla^2 v - v \nabla^2 u \right) \, \mathrm{d}\Omega = \int_{\Gamma} \left( u \frac{\partial v}{\partial n} - v \frac{\partial u}{\partial n} \right) \, \mathrm{d}\Gamma
$$
其中 $\nabla^2$ 是拉普拉斯算子，$\partial/\partial n$ 表示沿边界 $\Gamma$ 的外法线方向的导数。

为了利用此公式，我们引入一个特殊的辅助函数 $v$，称为**[基本解](@entry_id:184782)** (fundamental solution) 或[格林函数](@entry_id:147802)。[基本解](@entry_id:184782) $G(\mathbf{x}, \mathbf{y})$ 是控制方程在无限域中对单位[点源](@entry_id:196698)的响应。以地球物理学中广泛应用的拉普拉斯方程 $\nabla^2 u = 0$ 为例，其基本解满足：
$$
\nabla_{\mathbf{y}}^2 G(\mathbf{x}, \mathbf{y}) = -\delta(\mathbf{y}-\mathbf{x})
$$
其中 $\mathbf{x}$ 是“源点”或“观察点”，$\mathbf{y}$ 是“场点”或“积分点”，$\delta(\cdot)$ 是狄拉克δ函数。在三维和二维空间中，拉普拉斯方程的基本解分别为：
- **三维**: $G(\mathbf{x}, \mathbf{y}) = \frac{1}{4\pi |\mathbf{x}-\mathbf{y}|}$ [@problem_id:3616126] [@problem_id:3616104]
- **二维**: $G(\mathbf{x}, \mathbf{y}) = -\frac{1}{2\pi} \ln|\mathbf{x}-\mathbf{y}|$ [@problem_id:3616109]

将 $u$ 视为待求的谐[波函数](@entry_id:147440) ($\nabla^2 u = 0$)，并将 $v$ 替换为[基本解](@entry_id:184782) $G(\mathbf{x}, \mathbf{y})$，代入格林第二公式。利用 $\delta$ 函数的[筛选性质](@entry_id:265662)，域积分变为：
$$
\int_{\Omega} \left( u(\mathbf{y}) [-\delta(\mathbf{y}-\mathbf{x})] - G(\mathbf{x}, \mathbf{y}) [0] \right) \, \mathrm{d}\Omega_{\mathbf{y}} = -u(\mathbf{x})
$$
（假设 $\mathbf{x}$ 在域 $\Omega$ 内部）。于是，我们得到了一个仅包含边界积分的解的表达式，即**边界积分表达式**：
$$
u(\mathbf{x}) = \int_{\Gamma} \left( G(\mathbf{x}, \mathbf{y}) \frac{\partial u(\mathbf{y})}{\partial n_{\mathbf{y}}} - u(\mathbf{y}) \frac{\partial G(\mathbf{x}, \mathbf{y})}{\partial n_{\mathbf{y}}} \right) \, \mathrm{d}\Gamma_{\mathbf{y}}
$$
这个表达式表明，域内任意一点的解 $u(\mathbf{x})$ 完全由其边界上的值 $u(\mathbf{y})$ 和[法向导数](@entry_id:169511) $\partial u / \partial n_{\mathbf{y}}$ 决定。

为了求解一个边值问题，我们需要将观察点 $\mathbf{x}$ 移至边界 $\Gamma$ 上。这个极限过程需要谨慎处理积分核的奇异性，最终得到**[边界积分方程](@entry_id:746942)** (BIE)。对于边界上的点 $\mathbf{x}$，其通用形式为：
$$
c(\mathbf{x})u(\mathbf{x}) + \int_{\Gamma} u(\mathbf{y}) \frac{\partial G(\mathbf{x}, \mathbf{y})}{\partial n_{\mathbf{y}}} \, \mathrm{d}\Gamma_{\mathbf{y}} = \int_{\Gamma} G(\mathbf{x}, \mathbf{y}) \frac{\partial u(\mathbf{y})}{\partial n_{\mathbf{y}}} \, \mathrm{d}\Gamma_{\mathbf{y}}
$$
其中，右侧的积分核 $G$ 及其[法向导数](@entry_id:169511) $\partial G / \partial n$ 分别对应于**单层势** (single-layer potential) 和**双层势** (double-layer potential) 的核函数。系数 $c(\mathbf{x})$ 是一个与边界在 $\mathbf{x}$ 点的局部几何形状相关的常数。BEM 的核心任务就是求解这个关于未知边界量（$u$ 或 $\partial u/\partial n$）的[积分方程](@entry_id:138643)。

### [边界积分方程](@entry_id:746942)的构成要素

#### 自由项系数与几何角点

BIE 中的系数 $c(\mathbf{x})$，通常称为**自由项系数** (free-term coefficient)，它源于双层势积分在源点趋近边界时的极限过程。从物理上看，$c(\mathbf{x})$ 代表了域 $\Omega$ 在 $\mathbf{x}$ 点所占的[立体角](@entry_id:154756)分数。

- 对于位于光滑边界上的点，域占据了整个空间的一半，因此在三维中，[立体角](@entry_id:154756)为 $2\pi$，自由项系数 $c(\mathbf{x}) = 2\pi / (4\pi) = 1/2$；在二维中，内角为 $\pi$，系数 $c(\mathbf{x}) = \pi / (2\pi) = 1/2$。
- 对于位于非光滑边界（例如角点或棱线）上的点，该系数的值取决于局部几何。考虑一个二维[稳态热传导](@entry_id:177666)问题，其边界在一个角点 $\mathbf{x}_0$ 处的域内角为 $\omega$（以[弧度](@entry_id:171693)表示）。通过在 $\mathbf{x}_0$ 周围取一个半径为 $\epsilon$ 的小圆弧并进行[极限分析](@entry_id:188743)，可以精确推导出自由项系数 [@problem_id:3616109]。极限 $\epsilon \to 0$ 时，来自双层势积分的贡献恰好是 $\frac{\omega}{2\pi} u(\mathbf{x}_0)$。因此，在这种情况下：
$$
c(\mathbf{x}_0) = \frac{\omega}{2\pi}
$$
这个系数确保了 BIE 在边界的任何一点（无论是光滑的还是尖锐的）都成立，是正确建立 BEM 离散系统的关键。

#### [奇异积分](@entry_id:167381)：计算核心

当我们将观察点 $\mathbf{x}$ 放置在积分元上时，BIE 中的积分核 $G(\mathbf{x}, \mathbf{y})$ 和 $\partial G(\mathbf{x}, \mathbf{y}) / \partial n_{\mathbf{y}}$ 在 $\mathbf{y} \to \mathbf{x}$ 时会变得奇异。如何正确处理这些[奇异积分](@entry_id:167381)是 BEM 数值实现的核心挑战。

**弱[奇异积分](@entry_id:167381) (Weakly Singular Integrals)**
当积分核的奇异性“足够弱”，使得其与积分微元的乘积仍然可积时，该积分为弱奇异。以三维拉普拉斯问题中的单层势积分为例，其核函数 $G(\mathbf{x}, \mathbf{y})$ 的行为像 $1/r$（其中 $r = |\mathbf{x}-\mathbf{y}|$）。在局部极坐标下，面积微元 $\mathrm{d}\Gamma$ 的行为像 $r \, \mathrm{d}r \, \mathrm{d}\theta$。因此，被积函数的行为像 $(1/r) \cdot r = 1$，是可积的。这种积分在数学上是存在的，但标准的[数值积分方法](@entry_id:141406)（如[高斯求积](@entry_id:146011)）会失效。因此，需要采用特殊的数值技术，如[坐标变换](@entry_id:172727)（例如 Duffy 变换）或[奇点](@entry_id:137764)剔除法来精确计算。[@problem_id:3616104] [@problem_id:3616126]

**强[奇异积分](@entry_id:167381)与[柯西主值](@entry_id:192761) (Strongly Singular Integrals and Cauchy Principal Value)**
当积分核的奇异性“太强”，导致积分在常规意义下发散时，该积分为强奇异。三维拉普拉斯问题中的双层势积分为典型例子。其核函数 $\partial G/\partial n_{\mathbf{y}}$ 的行为像 $1/r^2$。被积函数的行为像 $(1/r^2) \cdot r = 1/r$，其积分会产生对数发散。

这类积分必须在**[柯西主值](@entry_id:192761) (CPV)** 的意义下进行解释。[柯西主值](@entry_id:192761)通过在[奇点](@entry_id:137764)周围挖去一个对称的、半径为 $\epsilon$ 的小区域，计算剩余部分的积分，然后取 $\epsilon \to 0$ 的极限来定义：
$$
\mathrm{p.v.} \int_{E} f(\mathbf{y}) \, \mathrm{d}\Gamma(\mathbf{y}) = \lim_{\epsilon \to 0^+} \int_{E \setminus B_{\epsilon}(\mathbf{x})} f(\mathbf{y}) \, \mathrm{d}\Gamma(\mathbf{y})
$$
对于双层势核，其角度依赖性导致在对称区域上的积分相互抵消，从而使得这个极限存在且有限 [@problem_id:3616104]。在 BEM 中，双层势的贡献被分解为[柯西主值](@entry_id:192761)积分和自由项 $c(\mathbf{x})u(\mathbf{x})$ 两部分。

### 在地球物理问题中的应用

BEM 的原理可以应用于由不同[偏微分方程控制](@entry_id:165441)的多种地球物理现象。

#### 位势问题：拉普拉斯与泊松方程

对于由[拉普拉斯方程](@entry_id:143689) $\nabla^2 u = 0$ 控制的问题，如均匀介质中的区域重[力场](@entry_id:147325)、[磁场](@entry_id:153296)或[稳态热流](@entry_id:264790)/地下水流，BIE 的形式如前所述，不包含域积分项，这使得 BEM 成为一种极其高效的纯边界方法。

然而，许多地球物理问题涉及源项，由**泊松方程** $-\nabla^2 u = f$ 描述，例如考虑了密度异常的[重力模拟](@entry_id:750044)。直接应用[格林公式](@entry_id:173118)会产生一个域积分项：
$$
u(\mathbf{x}) = \int_{\Gamma} \left( G \frac{\partial u}{\partial n} - u \frac{\partial G}{\partial n} \right) \, \mathrm{d}\Gamma_{\mathbf{y}} + \int_{\Omega} G(\mathbf{x}, \mathbf{y}) f(\mathbf{y}) \, \mathrm{d}\Omega_{\mathbf{y}}
$$
这个域积分的存在似乎破坏了 BEM 的纯边界特性。一种标准处理方法是**[特解](@entry_id:149080)法** (particular solution method)。我们将解分解为 $u = u^h + u^p$，其中 $u^h$ 是齐次（拉普拉斯）方程的解，而 $u^p$ 是[泊松方程](@entry_id:143763)的一个[特解](@entry_id:149080)，通常取为域积分本身，$u^p(\mathbf{x}) = \int_{\Omega} G f \, \mathrm{d}\Omega$。这样，我们只需对满足 $\nabla^2 u^h = 0$ 的 $u^h$ 求解一个标准的 BIE，其边界条件根据原始边界条件和 $u^p$ 的边界值进行调整。

尽管如此，在某些重要情况下，我们仍能避免对域进行[网格划分](@entry_id:269463) [@problem_id:3616130]：
1.  **源项为零**：即拉普拉斯问题，域积分为零。
2.  **[源项](@entry_id:269111)为离散点源**：例如，如果 $f$ 是由一系列点质量或点力荷载组成，则域积分退化为这些点源处[基本解](@entry_id:184782)的有限叠加，无需体积网格。
3.  **源项可被[特殊函数](@entry_id:143234)逼近**：诸如**对偶互易法 (DRM)** 或**多重互易法 (MRM)** 等技术，通过将[源项](@entry_id:269111) $f$ 近似为一组已知[特解](@entry_id:149080)的[基函数](@entry_id:170178)展开，从而将域积分等效地转化为一系列边界积分。

#### 波传播问题：[亥姆霍兹方程](@entry_id:149977)与辐射条件

模拟[时谐波](@entry_id:166582)（如[地震波](@entry_id:164985)或[电磁波](@entry_id:269629)）的传播需要求解**亥姆霍兹方程** $(\Delta + k^2)u = 0$，其中 $k$ 是[波数](@entry_id:172452)。其三维基本解（代表一个向外传播的[球面波](@entry_id:200471)）为：
$$
G_k(\mathbf{x}, \mathbf{y}) = \frac{\exp(ik|\mathbf{x}-\mathbf{y}|)}{4\pi|\mathbf{x}-\mathbf{y}|}
$$
[@problem_id:3616080]
在求解亥姆霍兹问题时，**内部问题**（在有界域 $\Omega$ 内）和**外部问题**（在无界域 $\Omega^\mathrm{ext}$ 内）之间存在本质区别 [@problem_id:3616113]。

对于外部问题（如地震散射），为了保证[解的唯一性](@entry_id:143619)并符合物理实际，必须施加一个在无穷远处的边界条件，即**[索末菲辐射条件](@entry_id:168772)** (Sommerfeld radiation condition)。该条件要求波在无穷远处表现为纯粹的向外传播的辐射波，其形式为：
$$
\lim_{R\to\infty} R\left(\frac{\partial u}{\partial R} - i k u\right) = 0
$$
其中 $R = |\mathbf{x}|$。BEM 的一个巨大优势在于，其使用的亥姆霍兹[基本解](@entry_id:184782) $G_k$ 本身就满足辐射条件。因此，任何通过边界势（如单层势 $u(\mathbf{x}) = \int_{\Gamma} G_k \varphi \, \mathrm{d}S$）表示的解，其在[远场](@entry_id:269288)的渐近行为会自动满足[索末菲辐射条件](@entry_id:168772)，从而避免了在有限元等方法中需要设置人工[吸收边界](@entry_id:201489)的麻烦 [@problem_id:3616080]。

然而，BEM 在求解亥姆霍兹方程时也面临一个独特的挑战：**伪频率** (fictitious frequencies)。当波数 $k$ 恰好与相关*内部*问题的某个特征频率（本征频率）重合时，用于求解外部问题的[边界积分方程](@entry_id:746942)会变得奇[异或](@entry_id:172120)病态，导致解不唯一。例如，使用纯双层势求解外部[狄利克雷问题](@entry_id:274408)，会在对应内部[诺伊曼问题](@entry_id:176713)的特征频率处失效 [@problem_id:3616113]。克服此问题需要采用更复杂的[组合场积分方程 (CFIE)](@entry_id:747496) 公式。

#### [弹性静力学](@entry_id:198298)：无限域与[远场](@entry_id:269288)行为

在固体地球物理学中，BEM 在模拟断层错动、岩浆侵入等问题时非常强大，因为这些问题通常被设定在无限或半无限的弹性介质中。对于三维均匀[各向同性线弹性](@entry_id:185899)体，其[平衡方程](@entry_id:172166)的[基本解](@entry_id:184782)是著名的**[开尔文解](@entry_id:187869)** (Kelvin solution) [@problem_id:3616141]。位移[基本解](@entry_id:184782) $U_{ij}(\mathbf{x}, \mathbf{y})$ 表示在 $\mathbf{y}$ 点沿 $j$ 方向施加单位点力而在 $\mathbf{x}$ 点沿 $i$ 方向产生的位移，其表达式为：
$$
U_{ij}(\mathbf{x},\mathbf{y}) = \frac{1}{16 \pi \mu (1 - \nu) r} \left[ (3 - 4 \nu) \delta_{ij} + \frac{r_i r_j}{r^2} \right]
$$
其中 $\mu$ 是剪切模量，$\nu$ 是[泊松比](@entry_id:158876)，$r_i = x_i - y_i$，$r = |\mathbf{r}|$。相应的**面力核** $T_{ij}(\mathbf{x}, \mathbf{y})$ 可由 $U_{ij}$ 通过本构关系和应力-面力定义导出。将这些[核函数](@entry_id:145324)代入弹性力学中的[贝蒂互易定理](@entry_id:200996)，便可得到**[索米里安纳恒等式](@entry_id:755063)** (Somigliana's identity)，即弹性力学问题的[边界积分方程](@entry_id:746942)。

对于外部[弹性静力学](@entry_id:198298)问题，为了确保[解的唯一性](@entry_id:143619)，位移场和应[力场](@entry_id:147325)在无穷远处必须满足特定的[衰减条件](@entry_id:157952)。例如，在三维空间中，位移 $\boldsymbol{u}(\boldsymbol{x})$ 和面力 $\boldsymbol{t}(\boldsymbol{x})$ 必须满足 [@problem_id:3547903]：
$$
\boldsymbol{u}(\boldsymbol{x}) = \mathcal{O}(r^{-1}) \quad \text{and} \quad \boldsymbol{t}(\boldsymbol{x}) = \mathcal{O}(r^{-2}) \quad \text{as } r \to \infty
$$
BEM 的另一个关键优势在此体现。[开尔文解](@entry_id:187869)本身在无穷远处具有与物理[衰减条件](@entry_id:157952)相匹配的衰减行为（$U_{ij} \sim r^{-1}$，$T_{ij} \sim r^{-2}$）。当将[索米里安纳恒等式](@entry_id:755063)应用于一个包含无穷远边界的区域时，由于物理场和[基本解](@entry_id:184782)场的衰减特性，无穷远边界上的积分项在极限过程中自然消失。这表明，BEM 能够自动、精确地施加无穷远边界条件，而无需像有限元法那样进行人工的域截断。

### 数值实现：离散化与系统集成

将[边界积分方程](@entry_id:746942)转化为可解的代数系统，需要对边界进行离散化，并对积分进行数值计算。

#### 等参元用于曲线边界

在实际地球物理模型中，边界通常是弯曲的。为了精确地表示这些几何形状，BEM 采用与[有限元法](@entry_id:749389)类似的思想，引入**[等参单元](@entry_id:173863)** (isoparametric elements)。其核心思想是：使用同一组[插值函数](@entry_id:262791)（即**形函数** $N_i(\xi)$）来描述单元的几何形状和单元上的物理场量 [@problem_id:3616149]。

例如，对于一个具有 $n$ 个节点的边界元，其几何坐标 $\mathbf{r}$ 和场变量 $u$ 可以通过参考坐标 $\xi$（通常在 $[-1, 1]$ 或一个标准三角形内）和节点值进行插值：
$$
\mathbf{r}(\xi) = \sum_{i=1}^{n} N_i(\xi) \mathbf{r}_i, \quad u(\xi) = \sum_{i=1}^{n} N_i(\xi) u_i
$$
其中 $\mathbf{r}_i$ 和 $u_i$ 分别是节点的物理坐标和场变量值。

在计算边界积[分时](@entry_id:274419)，需要将物理单元上的积分 $\int_{\Gamma_e} (\dots) \mathrm{d}s$ 转换到参考[坐标系](@entry_id:156346)上 $\int_{-1}^{1} (\dots) \mathrm{d}\xi$。这需要一个[坐标变换](@entry_id:172727)的伸缩因子，即**雅可比行列式** (Jacobian) $J(\xi)$。对于一维边界元，$J(\xi)$ 是切向量的模：
$$
J(\xi) = \left\| \frac{\mathrm{d}\mathbf{r}}{\mathrm{d}\xi} \right\| = \left\| \sum_{i=1}^{n} \frac{\mathrm{d}N_i(\xi)}{\mathrm{d}\xi} \mathbf{r}_i \right\|
$$
[积分变换](@entry_id:186209)关系为 $\mathrm{d}s = J(\xi) \mathrm{d}\xi$。例如，对于一个由三个节点 $\mathbf{r}_1, \mathbf{r}_2, \mathbf{r}_3$ 定义的二次等参元，其[雅可比行列式](@entry_id:137120)可以通过二次[拉格朗日形函数](@entry_id:635448)及其导数精确求出 [@problem_id:3616149]。

#### 配点法、系统集成与边界条件

最直接的 BEM 数值方法是**配点法** (collocation method)，即将 BIE 在边界离散化后的每个节点上进行配置（即要求方程在每个节点上精确成立）。

将场变量用形函数和节点值近似（例如，$\phi(\mathbf{y}) \approx \sum_{j=1}^{N_n} N_j(\mathbf{y}) \phi_j$），并代入 BIE，在第 $i$ 个节点 $\mathbf{x}_i$ 处进行配点，可得一个[代数方程](@entry_id:272665)。对所有 $N_n$ 个节点重复此过程，即可得到一个 $N_n \times N_n$ 的线性方程组，通常写作 $\mathbf{H}\mathbf{u} = \mathbf{G}\mathbf{q}$。其中，矩阵 $\mathbf{H}$ 和 $\mathbf{G}$ 的元素是通过对双层核和单层核与形函数乘积的积分得到的 [@problem_id:3616126]：
$$
H_{ij} = c_i \delta_{ij} + \int_{\Gamma} \frac{\partial G(\mathbf{x}_i, \mathbf{y})}{\partial n_{\mathbf{y}}} N_j(\mathbf{y}) \, \mathrm{d}\Gamma_{\mathbf{y}}
$$
$$
S_{ij} \text{ (in some literature denoted } G_{ij} \text{)} = \int_{\Gamma} G(\mathbf{x}_i, \mathbf{y}) N_j(\mathbf{y}) \, \mathrm{d}\Gamma_{\mathbf{y}}
$$
其中 $c_i$ 是在节点 $i$ 处的自由项系数。

在实际求解时，边界上的一半变量是已知的（根据给定的边界条件），另一半是待求的。通过重新整理[方程组](@entry_id:193238)，可以将所有未知量移到一边，所有已知量移到另一边，形成一个[标准形式](@entry_id:153058)的线性系统 $\mathbf{A}\mathbf{x} = \mathbf{b}$ 并求解。

值得注意的是，选择不同的积分方程表示法（例如，纯单层势、纯双层势或组合势）来满足边界条件，会导致不同性质的最终代数系统。例如，对于[狄利克雷问题](@entry_id:274408)，若用双层势表示解，则由于其在边界上的**跳跃性质**（产生 $\pm \frac{1}{2}I$ 项），会得到一个**第二类[弗雷德霍姆积分方程](@entry_id:277002)** (Fredholm integral equation of the second kind)。类似地，用单层势求解[诺伊曼问题](@entry_id:176713)也会得到第二[类方程](@entry_id:144428) [@problem_id:3616083]。第二[类方程](@entry_id:144428)通常具有更好的数值性质（如[算子谱](@entry_id:276315)更紧凑），比第一[类方程](@entry_id:144428)更受青睐。正确地选择和构建积分方程，是确保 BEM [算法稳定性](@entry_id:147637)和准确性的关键一步。