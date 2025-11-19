## 引言
间断Galerkin（DG）方法是一类功能强大且高度灵活的[偏微分方程数值方法](@entry_id:169137)，近年来在科学与工程计算领域获得了广泛关注。与传统的连续Galerkin有限元方法不同，DG方法通过放宽对解在单元边界处连续性的严格要求，获得了在处理复杂几何、[非匹配网格](@entry_id:168552)、变多项式阶次以及强不连续解（如激波）等问题上的独特优势。然而，这种灵活性也带来了理论构造上的复杂性，尤其是在如何保证单元间耦合的稳定性与一致性方面。本文旨在系统性地梳理[DG方法](@entry_id:748369)的理论框架与应用实践，填补从基础数学原理到跨学科工程应用之间的知识鸿沟。

为实现这一目标，本文将分为三个核心部分。首先，在“原理与机制”一章中，我们将深入剖析[DG方法](@entry_id:748369)的数学基石，从定义[破碎函数空间](@entry_id:746988)和界面算子出发，详细推导适用于不同类型[偏微分方程](@entry_id:141332)的[弱形式](@entry_id:142897)，并阐明[数值通量](@entry_id:752791)在确保格式稳定性和精度中的核心作用。接着，在“应用与跨学科联系”一章中，我们将展示DG方法如何在计算流体力学、[固体力学](@entry_id:164042)、电磁学等前沿领域中解决实际问题，将抽象的理论与具体的物理现象相结合。最后，通过一系列精心设计的“动手实践”练习，读者将有机会亲手实现[DG方法](@entry_id:748369)的关键组件，从而将理论知识转化为实际的编程能力。通过这一结构化的学习路径，读者将全面掌握间断Galerkin方法的核心思想与强大功能。

## 原理与机制

本章旨在深入探讨间断Galerkin（DG）方法的数学原理和核心机制。在引言章节的基础上，我们将不再赘述DG方法的背景，而是直接进入其理论构造的核心。我们将从定义[DG方法](@entry_id:748369)所依赖的[破碎函数空间](@entry_id:746988)和界面算子出发，逐步推导得到适用于不同类型[偏微分方程](@entry_id:141332)的[弱形式](@entry_id:142897)。通过引入数值通量的概念，我们将阐明如何针对椭圆、双曲和混合型问题设计稳定且精确的离散格式。本章内容将涵盖[DG方法](@entry_id:748369)从基本构件到高级应用的完整理论框架，为后续章节中更具体的算法实现和分析奠定坚实的基础。

### [DG方法](@entry_id:748369)的基本构件：[破碎函数空间](@entry_id:746988)与界面算子

连续Galerkin有限元方法的基础是定义在整个求解域 $\Omega$ 上的[连续函数空间](@entry_id:150395)，如[Sobolev空间](@entry_id:141995) $H^1(\Omega)$。这些空间要求函数及其[弱导数](@entry_id:189356)在整个域上是平方可积的，并隐含了函数在单元边界上必须是连续的。间断Galerkin方法的核心思想在于**放宽这种跨单元的连续性约束**。

#### [破碎Sobolev空间](@entry_id:746989)

为了形式化地描述这种允许间断的函数，我们引入**[破碎Sobolev空间](@entry_id:746989)**（Broken Sobolev Space）。给定一个由互不重叠的单元 $K$ 组成的区域 $\Omega$ 的网格剖分 $\mathcal{T}_h$，我们将[破碎Sobolev空间](@entry_id:746989) $H^1(\mathcal{T}_h)$ 定义为所有在每个单元 $K \in \mathcal{T}_h$ 上都属于标准Sobolev空间 $H^1(K)$ 的函数的集合。

具体而言，其定义如下 [@problem_id:2552238]：
$$
H^1(\mathcal{T}_h) = \{ v \in L^2(\Omega) \mid v|_K \in H^1(K) \quad \forall K \in \mathcal{T}_h \}
$$
其中 $v|_K$ 表示函数 $v$ 在单元 $K$ 上的限制。这个定义只要求函数在每个单元内部具有Sobolev正则性（即函数本身及其[弱导数](@entry_id:189356)在单元 $K$ 上平方可积），但不对其在单元间界面上的行为施加任何连续性要求。

与之相比，标准的 $H^1(\Omega)$ 空间是 $H^1(\mathcal{T}_h)$ 的一个[真子集](@entry_id:152276)，即 $H^1(\Omega) \subset H^1(\mathcal{T}_h)$。$H^1(\Omega)$ 中的函数在任意内部界面上的迹（trace）是单值的，而 $H^1(\mathcal{T}_h)$ 中的函数在界面两侧可以有不同的迹。正是这种[不连续性](@entry_id:144108)赋予了DG方法高度的灵活性，例如可以方便地处理不匹配的网格（hanging nodes）、在不同单元上使用不同阶次的多项式（$p$-适应性），以及更直接地处理双曲问题。

#### 迹、[跳跃与平均算子](@entry_id:750963)

由于 $H^1(\mathcal{T}_h)$ 中的函数在单元边界上可能是间断的，我们需要一套新的工具来描述和处理界面上的物理量。这些工具就是**迹（trace）**、**跳跃（jump）**和**平均（average）**算子。

考虑一个内部界面 $F$，它是两个相邻单元 $K^+$ 和 $K^-$ 的公共边界，即 $F = \partial K^+ \cap \partial K^-$。我们定义 $\boldsymbol{n}^+$ 和 $\boldsymbol{n}^-$ 分别为 $F$ 相对于 $K^+$ 和 $K^-$ 的单位外法向向量，显然有 $\boldsymbol{n}^+ = -\boldsymbol{n}^-$。

根据[迹定理](@entry_id:203967)，对于任何定义在 $H^1(K)$ 上的函数，其在边界 $\partial K$ 上的迹是良定的。因此，对于一个函数 $u \in H^1(\mathcal{T}_h)$，我们可以从界面 $F$ 的两侧分别取迹，得到两个可能不同的值（或函数）：
-   $u^+ = u|_{K^+}$ 在 $F$ 上的迹。
-   $u^- = u|_{K^-}$ 在 $F$ 上的迹。

基于这两个迹，我们可以定义跳跃和[平均算子](@entry_id:746605)。对于一个标量函数 $u$，其**平均**算子 $\{\!\{u\}\!\}$ 定义为两侧迹的算术平均值 [@problem_id:2552238]：
$$
\{\!\{u\}\!\} := \frac{1}{2}(u^+ + u^-)
$$
而其**法向跳跃**算子 $[\![u]\!]$ 定义为一个向量，它捕捉了函数值的不连续性的大小和方向：
$$
[\![u]\!] := u^+ \boldsymbol{n}^+ + u^- \boldsymbol{n}^-
$$
利用 $\boldsymbol{n}^- = -\boldsymbol{n}^+$，我们也可以将其写作 $[\![u]\!] = (u^+ - u^-) \boldsymbol{n}^+$ 或 $[\![u]\!] = (u^- - u^+) \boldsymbol{n}^-$（取决于法向量的选定方向）。这个定义在通过分部积分推导[DG格式](@entry_id:178043)时尤其有用。类似地，对于一个向量函数 $\boldsymbol{q}$，其平均和跳跃可以定义为：
$$
\{\!\{\boldsymbol{q}\}\!\} := \frac{1}{2}(\boldsymbol{q}^+ + \boldsymbol{q}^-), \quad [\![\boldsymbol{q}]\!] := \boldsymbol{q}^+ \cdot \boldsymbol{n}^+ + \boldsymbol{q}^- \cdot \boldsymbol{n}^-
$$

值得注意的是，如果一个函数 $u$ 恰好在界面 $F$ 上是连续的，即 $u^+=u^-$，那么其平均值就是该连续值，$\{\!\{u\}\!\} = u^+$。而其法向跳跃则为零，$[\![u]\!] = u^+\boldsymbol{n}^+ + u^+\boldsymbol{n}^- = u^+(\boldsymbol{n}^+ + \boldsymbol{n}^-) = \boldsymbol{0}$。这与我们的直觉相符。

为了更具体地理解这些定义，我们来看一个一维的例子 [@problem_id:2552235]。考虑域 $\Omega=[0,1]$ 被划分为两个单元 $K_1=[0, 0.5]$ 和 $K_2=[0.5, 1]$。界面点为 $x=0.5$。设 $K_1$ 为左侧单元（-），$K_2$ 为右侧单元（+）。在1D情况下， $K_1$ 在 $x=0.5$ 处的单位外法向为 $n^- = +1$，$K_2$ 在 $x=0.5$ 处的单位外法向为 $n^+ = -1$。

现在考虑一个[分段函数](@entry_id:160275)：在 $K_1$上 $u(x)=x$ 和在 $K_2$ 上 $u(x)=1-x$。在界面 $x=0.5$ 处，我们计算两侧的迹：
-   从 $K_1$ 逼近：$u^- = \lim_{x \to 0.5^-} x = 0.5$。
-   从 $K_2$ 逼近：$u^+ = \lim_{x \to 0.5^+} (1-x) = 0.5$。

尽管这个函数在界面处是连续的，我们仍然可以应用跳跃和平均的定义：
-   **平均**: $\{\!\{u\}\!\} = \frac{1}{2}(u^- + u^+) = \frac{1}{2}(0.5 + 0.5) = 0.5$。
-   **跳跃**: $[\![u]\!] = u^- \boldsymbol{n}^- + u^+ \boldsymbol{n}^+ = (0.5)(+1) + (0.5)(-1) = 0.5 - 0.5 = \boldsymbol{0}$。
这个例子清楚地表明，对于[连续函数](@entry_id:137361)，法向跳跃为零，而平均值就是函数在该点的值。如果函数不连续，跳跃算子将捕捉到这种不连续性。

### [DG弱形式](@entry_id:748377)与[数值通量](@entry_id:752791)

DG方法的核心思想是在每个单元 $K$ 上独立地写出控制方程的[弱形式](@entry_id:142897)，然后通过在单元边界上引入**[数值通量](@entry_id:752791) (numerical flux)** 来耦合相邻单元。

让我们以一个一般的守恒律方程为例：$\partial_t u + \nabla \cdot \boldsymbol{f}(u) = 0$。我们将其乘以一个[检验函数](@entry_id:166589) $v_h$，并在单元 $K$ 上积分：
$$
\int_K (\partial_t u_h) v_h \,dx + \int_K (\nabla \cdot \boldsymbol{f}(u_h)) v_h \,dx = 0
$$
对第二项使用分部积分（散度定理），我们得到：
$$
\int_K (\partial_t u_h) v_h \,dx - \int_K \boldsymbol{f}(u_h) \cdot \nabla v_h \,dx + \int_{\partial K} (\boldsymbol{f}(u_h) \cdot \boldsymbol{n}_K) v_h \,ds = 0
$$
其中 $\boldsymbol{n}_K$ 是单元 $K$ 的单位外法向向量。边界积分项 $\boldsymbol{f}(u_h) \cdot \boldsymbol{n}_K$ 是物理通量通过单元边界的法向分量。然而，由于 $u_h$ 在边界上是双值的（即有 $u^-$ 和 $u^+$），这个通量项没有唯一定义。

DG方法的关键步骤就是用一个**数值通量** $\widehat{\boldsymbol{f}}(u^-, u^+; \boldsymbol{n})$ 来代替物理通量 $\boldsymbol{f}(u) \cdot \boldsymbol{n}$。这个[数值通量](@entry_id:752791)是一个函数，它依赖于界面两侧的状态 $u^-$ 和 $u^+$ 以及法向量 $\boldsymbol{n}$。于是，[弱形式](@entry_id:142897)变为：
$$
\int_K (\partial_t u_h) v_h \,dx - \int_K \boldsymbol{f}(u_h) \cdot \nabla v_h \,dx + \int_{\partial K} \widehat{\boldsymbol{f}}(u_h^{\text{int}}, u_h^{\text{ext}}; \boldsymbol{n}_K) v_h \,ds = 0
$$
其中 $u_h^{\text{int}}$ 是从单元 $K$ 内部取到的迹，而 $u_h^{\text{ext}}$ 是从相邻单元（或边界）取到的迹。

数值通量的选择是DG方法设计的核心，它决定了离散格式的稳定性、精度和耗散性。一个设计良好的[数值通量](@entry_id:752791)通常需要满足以下几个关键性质 [@problem_id:2552240]：

1.  **相容性 (Consistency)**：如果界面两侧的状态相同，即 $u^- = u^+ = u$，则数值通量必须退化为物理通量。
    $$
    \widehat{\boldsymbol{f}}(u, u; \boldsymbol{n}) = \boldsymbol{f}(u) \cdot \boldsymbol{n}
    $$
    这是保证离散格式在解是光滑的情况下能够收敛到真解的基本要求。例如，Lax-Friedrichs通量 $\widehat{f}_{\mathrm{LF}}(u^-,u^+;\boldsymbol{n}) = \frac{1}{2}(\boldsymbol{f}(u^-)+\boldsymbol{f}(u^+))\cdot \boldsymbol{n} - \frac{1}{2}\alpha(u^+ - u^-)$ 总是相容的，因为当 $u^-=u^+=u$ 时，第二项消失，第一项变为 $\boldsymbol{f}(u)\cdot \boldsymbol{n}$。

2.  **守恒性 (Conservativity)**：在任意一个内部界面 $F$ 上，从一个单元流出的通量必须等于流入相邻单元的通量。设 $\boldsymbol{n}$ 是从 $K^-$ 指向 $K^+$ 的[法向量](@entry_id:264185)。那么从 $K^-$ 流出的[数值通量](@entry_id:752791)是 $\widehat{\boldsymbol{f}}(u^-, u^+; \boldsymbol{n})$，而从 $K^+$ 流出的通量则是 $\widehat{\boldsymbol{f}}(u^+, u^-; -\boldsymbol{n})$。守恒性要求这两个通量相加为零：
    $$
    \widehat{\boldsymbol{f}}(u^-, u^+; \boldsymbol{n}) + \widehat{\boldsymbol{f}}(u^+, u^-; -\boldsymbol{n}) = 0
    $$
    这确保了在整个求解域上，物理量的总和仅因外部边界通量而改变，从而保证了离散格式的全局守恒。

3.  **单调性 (Monotonicity)**（主要针对标量双曲问题）：一个单调的数值通量可以保证最终的数值解不会产生新的极值，从而抑制在间断（如激波）附近出现的非物理[振荡](@entry_id:267781)。对于一个标量[数值通量](@entry_id:752791) $\widehat{f}(u^-, u^+)$，[单调性](@entry_id:143760)要求它关于第一个参数 $u^-$ 是非减的，关于第二个参数 $u^+$ 是非增的。
    $$
    \frac{\partial \widehat{f}}{\partial u^-} \ge 0, \quad \frac{\partial \widehat{f}}{\partial u^+} \le 0
    $$
    [Godunov通量](@entry_id:634733)和满足特定条件的Lax-Friedrichs通量都是单调通量，而[中心通量](@entry_id:747204) $\widehat{f}_{\mathrm{c}}(u^-,u^+;\boldsymbol{n})=\frac{1}{2}(\boldsymbol{f}(u^-)+\boldsymbol{f}(u^+))\cdot \boldsymbol{n}$ 通常不具有[单调性](@entry_id:143760)，因此在双曲问题中可能导致不稳定。

### 应用于[椭圆问题](@entry_id:146817)：内部罚函数法

对于形如 $-\nabla \cdot (\kappa \nabla u) = f$ 的[扩散](@entry_id:141445)或[椭圆问题](@entry_id:146817)，[DG方法](@entry_id:748369)同样适用，但其构造方式与双曲问题有所不同。最流行的一类方法是**内部[罚函数法](@entry_id:636090)（Interior Penalty, IP）**。

为了推导IP格式，我们引入辅助变量 $\boldsymbol{q} = -\kappa \nabla u$，将二阶方程写成一阶[方程组](@entry_id:193238)。然后应用与双曲问题类似的[DG离散化](@entry_id:748366)过程。最终，通过将 $\boldsymbol{q}$ 替换回 $-\kappa \nabla u_h$，可以得到一个只包含 $u_h$ 的[双线性形式](@entry_id:746794) $a(u_h, v_h)$。这个双线性形式族可以由一个参数 $\theta$ 来统一描述 [@problem_id:2552263]：
$$
a_\theta(u_h, v_h) = \sum_{K \in \mathcal{T}_h} \int_K \kappa \nabla_h u_h \cdot \nabla_h v_h \, dx - \sum_{F \in \mathcal{F}_h^{\text{int}}} \left( \langle \{\!\{\kappa \nabla_h u_h\}\!\}, [\![v_h]\!] \rangle_F + \theta \langle \{\!\{\kappa \nabla_h v_h\}\!\}, [\![u_h]\!] \rangle_F \right) + \sum_{F \in \mathcal{F}_h^{\text{int}}} \langle \frac{\sigma_F}{h_F} [\![u_h]\!], [\![v_h]\!] \rangle_F
$$
这里的 $\mathcal{F}_h^{\text{int}}$ 是内部界面的集合，$\langle \cdot, \cdot \rangle_F$ 表示在界面 $F$ 上的 $L^2$ [内积](@entry_id:158127)。此形式包含三个主要部分：
1.  **单元[内部积](@entry_id:158127)分**: $\sum_K \int_K \kappa \nabla_h u_h \cdot \nabla_h v_h \, dx$ 是标准的体积项，与连续[有限元法](@entry_id:749389)类似。
2.  **相容性与对称性项**: $-\sum_F (\dots)$ 部分是核心的耦合项。第一项 $\langle \{\!\{\kappa \nabla_h u_h\}\!\}, [\![v_h]\!] \rangle_F$ 保证了格式的相容性。第二项 $\theta \langle \{\!\{\kappa \nabla_h v_h\}\!\}, [\![u_h]\!] \rangle_F$ 的存在与否及其系数 $\theta$ 决定了格式的对称性。
3.  **罚项**: $\sum_F \langle \frac{\sigma_F}{h_F} [\![u_h]\!], [\![v_h]\!] \rangle_F$ 是罚项，它惩罚了函数在界面上的跳跃。这里的 $\sigma_F$ 是一个无量纲的正常数，称为**罚参数**，而 $h_F$ 是界面的特征尺寸。这个罚项对于保证格式的稳定性和强制[解的唯一性](@entry_id:143619)至关重要。

根据参数 $\theta$ 的取值，我们可以得到几种经典的IP方法：

-   **[对称内部罚](@entry_id:755719)函数法 (SIPG, $\theta=1$)**: 当 $\theta=1$ 时，[双线性形式](@entry_id:746794) $a_1(\cdot, \cdot)$ 是对称的，即 $a_1(u_h, v_h) = a_1(v_h, u_h)$。这是最常用的方法之一，因为它产生对称的正定刚度矩阵。然而，为了保证 coercivity（强制性或椭圆性），罚参数 $\sigma_F$ 必须足够大。理论分析表明，$\sigma_F$ 通常需要与多项式次数的平方成正比，即 $\sigma_F \propto p^2$ [@problem_id:2552236]。

-   **非[对称内部罚](@entry_id:755719)函数法 (NIPG, $\theta=-1$)**: 当 $\theta=-1$ 时，双线性形式 $a_{-1}(\cdot, \cdot)$ 是非对称的。一个有趣的特性是，当 $v_h=u_h$ 时，相容性项 $-(1+\theta)\sum_F \langle \{\!\{\kappa \nabla_h u_h\}\!\}, [\![u_h]\!] \rangle_F$ 完全消失。这使得 coercivity 的证明变得简单，并且对任意正的罚参数 $\sigma_F > 0$ 都成立，无需“足够大”的条件。缺点是它会产生一个非对称的[刚度矩阵](@entry_id:178659)，求解起来通常更昂贵。

-   **不完全内部罚函数法 (IIPG, $\theta=0$)**: 当 $\theta=0$ 时，我们只保留了第一个相容性项。这种方法也是非对称的，并且像SIPG一样，需要足够大的罚参数来保证稳定性。

### 应用于双曲问题：迎风格式与稳定性

对于形如 $u_t + a u_x = 0$ ($a>0$) 的线性[对流](@entry_id:141806)（双曲）问题，[DG方法](@entry_id:748369)的一个自然且强大的选择是**迎风格式（Upwind scheme）**。迎风思想的核心是：信息沿着特征线传播，因此在界面上的[数值通量](@entry_id:752791)应该由信息来源方向（上游，即upwind）的单元状态决定。

对于 $a>0$，信息从左向右传播。在一个界面上，左侧单元的状态是 $u^-$，右侧是 $u^+$。因此，[迎风通量](@entry_id:143931)取上游值，即 $\widehat{f}(u^-, u^+) = a u^-$。

我们可以通过稳定性分析来揭示[迎风格式](@entry_id:756374)的优越性 [@problem_id:2552250]。考虑使用分片常数（$p=0$）[DG方法](@entry_id:748369)求解周期性[对流](@entry_id:141806)问题。[半离散格式](@entry_id:165671)可以写成 $\frac{d u_i}{dt} = (\mathcal{A}_h u)_i$，其中 $u_i$ 是第 $i$ 个单元上的常数值，$\mathcal{A}_h$ 是空间离散算子。通过[离散傅里叶分析](@entry_id:748507)（[von Neumann分析](@entry_id:153661)），我们可以计算出算子 $\mathcal{A}_h$ 的谱（即[特征值](@entry_id:154894)）。

-   **[中心通量](@entry_id:747204)**: 若使用[中心通量](@entry_id:747204) $\widehat{f}^{\text{cen}} = a \frac{u^- + u^+}{2}$，其[特征值](@entry_id:154894)是纯虚数，$\lambda_{\text{cen}}(\theta) = -\frac{\mathrm{i} a}{h} \sin(\theta)$。这意味着能量在离散系统中既不增长也不衰减，任何小的扰动都会以[色散](@entry_id:263750)波的形式持续存在，导致数值解充满[振荡](@entry_id:267781)，格式是不稳定的。其谱半径为 $\rho(\mathcal{A}_{h, \text{cen}}) = \frac{a}{h}$。

-   **[迎风通量](@entry_id:143931)**: 若使用[迎风通量](@entry_id:143931) $\widehat{f}^{\text{up}} = a u^-$，其[特征值](@entry_id:154894)是复数，$\lambda_{\text{up}}(\theta) = -\frac{a}{h} (1 - \exp(-\mathrm{i}\theta))$。这些[特征值](@entry_id:154894)的实部都是非正的，这意味着能量会随时间衰减。这种数值耗散能够抑制[振荡](@entry_id:267781)，从而使格式稳定。其谱半径为 $\rho(\mathcal{A}_{h, \text{up}}) = \frac{2a}{h}$，这个值决定了[显式时间积分](@entry_id:165797)方法（如[龙格-库塔法](@entry_id:140014)）的稳定性[时间步长限制](@entry_id:756010)（CFL条件）。

这个分析清晰地表明，[迎风格式](@entry_id:756374)通过引入必要的[数值耗散](@entry_id:168584)来确保双曲问题的稳定性，这是[中心通量](@entry_id:747204)等无耗散格式所缺乏的。

### 离散系统：组装与实现

将上述原理转化为可执行的计算机代码，需要一个系统化的**组装（assembly）**过程。其核心思想是“先局部，后全局”。我们首先在每个单元上计算局部贡献，然后将它们累加到全局的[刚度矩阵](@entry_id:178659)和[残差向量](@entry_id:165091)中。

让我们以一维线性[对流](@entry_id:141806)方程 $u_t + a u_x = 0$ 在单元 $K_j$ 上使用 $p=1$ 次多项式为例，来说明这个过程 [@problem_id:2552257]。设局部解为 $u_h|_{K_j}(x, t) = \sum_{k=1}^2 U_{j,k}(t) \phi_k(x)$，其中 $\phi_k$ 是[局部基](@entry_id:151573)函数。半离散弱形式可以写成矩阵形式：
$$
M \dot{U}_j = V U_j - F_j
$$
其中 $U_j = (U_{j,1}, U_{j,2})^T$ 是局部自由度向量。

1.  **局部质量矩阵 (Mass Matrix) $M$**: 来自于时间导数项 $\int_{K_j} v u_t \,dx$。其元素为 $M_{ik} = \int_{K_j} \phi_i \phi_k \,dx$。这个矩阵是与时间无关的，描述了[基函数](@entry_id:170178)在 $L^2$ 范数下的关系。

2.  **局部体积刚度/[对流矩阵](@entry_id:747848) (Volume Stiffness/Advection Matrix) $V$**: 来自于单元内部的[对流](@entry_id:141806)项积分 $\int_{K_j} a u_h (\partial_x v) \,dx$（分部积分后）。其元素为 $V_{ik} = \int_{K_j} a \phi_k (\partial_x \phi_i) \,dx$。

3.  **界面通量向量 (Face Flux Vector) $F_j$**: 来自于边界上的[数值通量](@entry_id:752791)项 $\int_{\partial K_j} v \widehat{a u} \,ds$。对于迎风格式（$a>0$），在右边界 $x_{j+1/2}$，通量取自本单元的右端点值 $u_h(x_{j+1/2}^-)$；在左边界 $x_{j-1/2}$，通量取自左邻单元的右端点值 $u_h(x_{j-1/2}^-)|_{K_{j-1}}$。这导致 $F_j$ 不仅依赖于本单元的自由度 $U_j$，还依赖于邻居单元的自由度 $U_{j-1}$。因此，我们可以将其分解为 $F_j = G_R U_j + G_L U_{j-1}$，其中 $G_R$ 和 $G_L$ 是[耦合矩阵](@entry_id:191757)，它们将局部解耦合成一个全局系统。

对于一个更一般的[稳态](@entry_id:182458)[对流](@entry_id:141806)[扩散](@entry_id:141445)问题，其组装过程可以概括为以下算法 [@problem_id:2552236]：
1.  **初始化**全局[残差向量](@entry_id:165091) $R$ 为零。
2.  **遍历所有单元 $K \in \mathcal{T}_h$**：
    a.  计算体积积分项，例如 $\int_K (\kappa \nabla u_h \cdot \nabla v_h - u_h (\boldsymbol{\beta} \cdot \nabla v_h) - f v_h) \,dx$。
    b.  将结果累加到与单元 $K$ 相关的局部[残差向量](@entry_id:165091) $R_K$ 中。
3.  **遍历所有内部界面 $F \in \mathcal{F}_h^{\text{int}}$**：
    a.  计算界面上的数值通量贡献，例如SIPG项和[迎风](@entry_id:756372)项。
    b.  将这些贡献（根据[法向量](@entry_id:264185)方向带相应的正负号）分别累加到与界面 $F$ 相邻的两个单元的局部[残差向量](@entry_id:165091)中。
4.  **遍历所有边界界面 $F \in \mathcal{F}_h^{\text{b}}$**：
    a.  根据边界条件类型（Dirichlet或Neumann），应用相应的数值通量。例如，在Dirichlet边界上，外部状态由给定的边界数据 $g_D$ 代替；在Neumann边界上，法向[扩散通量](@entry_id:748422)由 $g_N$ 代替。
    b.  将贡献累加到与该边界界面相邻的单元的局部残差向量中。
5.  **[全局组装](@entry_id:749916)**：将所有局部[残差向量](@entry_id:165091) $R_K$ 通过索引映射“散射-相加”（scatter-add）到全局[残差向量](@entry_id:165091) $R$ 的对应位置。

最终得到的[代数方程](@entry_id:272665)组 $R(U) = 0$（对于[稳态](@entry_id:182458)问题）或 $M \dot{U} = R(U)$（对于瞬态问题）即可通过线性或[非线性求解器](@entry_id:177708)进行求解。

### [非线性](@entry_id:637147)问题与高级专题

DG方法在处理[非线性](@entry_id:637147)问题和复杂物理现象时展现出巨大潜力，但也带来了一些新的挑战和相应的高级技术。

#### [非线性](@entry_id:637147)通量与混淆误差

当处理形如 $u_t + \partial_x f(u) = 0$ 的[非线性](@entry_id:637147)守恒律时，例如 $f(u)=u^p, p \ge 2$，[DG弱形式](@entry_id:748377)中的体积积分项 $\int_K f(u_h) \partial_x v_h \, dx$ 变得复杂。如果 $u_h$ 是 $N$ 次多项式，那么 $f(u_h)$ 就是 $pN$ 次多项式，整个被积函数是 $pN + (N-1)$ 次多项式。然而，标准的DG实现通常使用仅对 $2N-1$ 次多项式精确的[Gauss-Lobatto求积](@entry_id:749739)。当 $p>1$ 时，$pN+N-1 > 2N-1$，这意味着[数值积分](@entry_id:136578)是不精确的 [@problem_id:2552234]。

这种不精确的积分会导致**混淆误差（aliasing error）**。高阶多项式分量在不精确的积分下被错误地“折叠”或“混淆”成低阶模式，这可能导致非物理的能量增长和数值不稳定性。

有两种主要策略来缓解这个问题：
1.  **[过积分](@entry_id:753033)（Over-integration）**：简单直接地增加求积点的数量 $M$，使得求积法则的精度 $2M-3$ 足够高，能够精确积分 $f(u_h)\partial_x v_h$。例如，选择 $M$ 满足 $2M-3 \ge pN+N-1$。这消除了[积分误差](@entry_id:171351)，但代价是计算成本的增加 [@problem_id:2552234]。
2.  **分裂形式（Split-form）**：将通量导数 $\partial_x f(u)$ 改写为代数上等价但离散性质更优的形式，例如对于[Burgers方程](@entry_id:177995) $f(u)=u^2/2$，可以写成 $\frac{1}{3}(u\partial_x u + \partial_x(u^2/2))$。这些分裂形式在离散化后（特别是与满足[分部求和](@entry_id:185335)性质的算子结合时），能够更好地模拟连续情况下的[能量守恒](@entry_id:140514)或[熵守恒](@entry_id:749018)性质，从而在不完全消除混淆误差的情况下控制其导致的稳定性问题 [@problem_id:2552234]。

#### 激波捕捉与[斜率限制器](@entry_id:638003)

[非线性](@entry_id:637147)双曲问题常常会发展出间断解（激波）。[高阶数值方法](@entry_id:142601)在逼近这些间断时会产生非物理的[吉布斯振荡](@entry_id:749902)。为了获得稳定且物理上相关的解，必须引入[非线性](@entry_id:637147)稳定化机制，最常用的是**[斜率限制器](@entry_id:638003)（slope limiters）**。

限制器的核心思想是：在保持单元平均值（从而保证守恒性）不变的前提下，局部地修改解的[多项式系数](@entry_id:262287)（即斜率、曲率等），以抑制[振荡](@entry_id:267781) [@problem_id:2552230]。
对于 $p=1$ 的[DG方法](@entry_id:748369)，局部解为 $u_h(\xi) = \hat{u}_{i,0} + \hat{u}_{i,1}\xi$，其中 $\hat{u}_{i,0}$ 是单元平均值，$\hat{u}_{i,1}$ 控制斜率。限制器只修改 $\hat{u}_{i,1}$。

一个经典的限制器是**minmod限制器**。它将原始斜率与基于相邻单元平均值构造的前差和后差斜率进行比较，选择其中最小的一个（如果三者同号），否则将斜率设为零。对于一维 $p=1$ DG，修正后的斜率系数 $\hat{u}_{i,1}^{\text{new}}$ 为：
$$
\hat u_{i,1}^{\text{new}} = \operatorname{mm}\! \left( \hat u_{i,1}, \frac{1}{2}(\bar u_{i+1} - \bar u_i), \frac{1}{2}(\bar u_i - \bar u_{i-1}) \right)
$$
其中 $\bar u_j = \hat{u}_{j,0}$ 是第 $j$ 个单元的平均值，$\operatorname{mm}(a,b,c)$ 是minmod函数。$\frac{1}{2}$ 因子的出现是因为 $\hat{u}_{i,1}$ 代表了从单元中心到边界（半个单元宽度）的变化，而 $\bar{u}_{i+1}-\bar{u}_i$ 是跨越一个完整单元宽度的平均值变化，必须进行尺度上的对齐 [@problem_id:2552230]。

#### [hp-自适应](@entry_id:750398)

DG方法的高度局部性使其成为**[hp-自适应](@entry_id:750398)**的理想框架。[hp-自适应](@entry_id:750398)是一种先进的[网格自适应](@entry_id:751899)策略，它根据解的局部光滑性，协同地进行 $h$-细化（减小单元尺寸 $h$）和 $p$-细化（提高多项式次数 $p$）。

基本原理是 [@problem_id:2552252]：
-   在解**光滑**的区域，提高多项式次数 $p$ 可以获得指数级的收敛速度，这远比细化网格 $h$ 高效。
-   在解存在**奇异性**（如角点、间断）的区域，解的正则性很低，提高 $p$ 几乎没有收益。此时必须通过减小单元尺寸 $h$ 来隔离[奇异点](@entry_id:199525)，才能有效降低误差。

为了自动进行 $h$ 或 $p$ 的选择，需要一个**[误差指示子](@entry_id:173250)（error indicator）**来判断解的局部光滑性。在DG中，一个非常有效的方法是分析解在每个单元上模态展开系数的衰减速度。将局部解 $u_h|_K$ 展开为一组[正交基](@entry_id:264024)（如[勒让德多项式](@entry_id:141510)）的[线性组合](@entry_id:154743) $u_h|_K = \sum_n \hat{u}_n^{(K)} \phi_n^{(K)}$。
-   如果解在单元 $K$ 上是解析的（非常光滑），则[模态系数](@entry_id:752057) $|\hat{u}_n^{(K)}|$ 会随模态数 $n$ **指数衰减**。
-   如果解在单元 $K$ 上存在奇异性，则[模态系数](@entry_id:752057)只会**代数衰减**。

通过监测[模态系数](@entry_id:752057)尾部能量的占比，或直接对 $\log|\hat{u}_n^{(K)}|$ 与 $n$ 的关系进行线性拟合，我们就可以估计出衰减率，从而判断是应该进行 $p$-细化（指数衰减）还是 $h$-细化（代数衰减）[@problem_id:2552252]。这种基于物理和数学原理的自适应策略，使得DG方法能够以近乎最优的计算效率求解具有复杂多尺度特征的问题。