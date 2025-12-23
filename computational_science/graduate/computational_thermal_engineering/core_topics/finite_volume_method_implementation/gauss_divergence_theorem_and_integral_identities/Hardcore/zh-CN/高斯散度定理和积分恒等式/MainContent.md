## 引言
[高斯散度定理](@entry_id:188065)是矢量分析中的一块基石，它以深刻的数学优雅性，连接了物理守恒定律的局部[微分](@entry_id:158422)描述与全局积分陈述。然而，对于许多工程和物理科学的研究生而言，从其抽象的数学形式到其在复杂的[计算模型](@entry_id:637456)（如[计算热工学](@entry_id:1122812)）中的具体应用，存在一条概念上的鸿沟。本篇文章旨在填补这一鸿沟，系统性地揭示高斯散度定理如何成为理解和量化物理世界的强大工具。

为此，本文将分为三个核心章节。在“原理与机制”中，我们将深入探讨定理的数学基础及其在传热学中的物理诠释，阐明其作为能量守恒基本原理的角色。接着，在“应用与跨学科联系”中，我们将拓宽视野，展示该定理如何统一地应用于电磁学、[连续介质力学](@entry_id:155125)等多个领域，并作为[有限体积法](@entry_id:141374)等计算方法的理论支柱。最后，通过“动手实践”部分，您将有机会将理论知识应用于具体的工程问题，巩固所学。

## 原理与机制

本章深入探讨高斯散度定理的数学原理及其在[计算热工学](@entry_id:1122812)中的物理机制。我们将从定理的精确表述出发，逐步揭示其在建立能量守恒方程、处理复杂几何构型以及应对移动边界等高级问题中的核心作用。

### 高斯散度定理：一项基本的[守恒原理](@entry_id:1122907)

高斯散度定理，亦称奥氏-高斯公式，是矢量分析中的一个基石，它在物理守恒定律的积分形式和微分形式之间建立了桥梁。该定理的本质是将一个体积内所有微观源（或汇）的累积效应，与通过该体积边界的净通量联系起来。

从数学上讲，该定理可以精确地表述如下：考虑三维[欧几里得空间](@entry_id:138052) $\mathbb{R}^3$ 中的一个有界Lipschitz区域 $\Omega$，其边界为 $\partial\Omega$。设 $\mathbf{F}$ 是一个在 $\overline{\Omega}$（$\Omega$ 的[闭包](@entry_id:148169)）上连续可微的矢量场，即 $\mathbf{F} \in C^1(\overline{\Omega})$。令 $\mathbf{n}$ 为在边界 $\partial\Omega$ 上[几乎处处](@entry_id:146631)定义的单位外法向矢量。高斯散度定理指出，矢量场 $\mathbf{F}$ 的散度 $\nabla \cdot \mathbf{F}$ 在体积 $\Omega$ 上的积分，等于该矢量场通过边界 $\partial\Omega$ 的法向分量的面积分：

$$
\int_{\Omega} \nabla \cdot \mathbf{F} \, dV = \int_{\partial\Omega} \mathbf{F} \cdot \mathbf{n} \, dS
$$

其中，$dV$ 是三维勒贝格体积元，$dS$ 是在边界 $\partial\Omega$ 上的[面积元](@entry_id:263205) 。

这里的几个条件至关重要。**Lipschitz区域**的要求保证了边界足够“良好”，没有过于病态的几何特征（如无限长的[尖点](@entry_id:636792)或分形结构），从而确保单位法向矢量 $\mathbf{n}$ 和边界积分能够被良好地定义。矢量场 $\mathbf{F}$ 至少为 $C^1$ 类的要求则保证了其散度 $\nabla \cdot \mathbf{F}$ 是一个[连续函数](@entry_id:137361)，因此在体积 $\Omega$ 上是可积的。正如我们稍后将看到的，在更现代的计算框架中，这些正则性要求可以被放宽。

此定理的直观含义是：体积 $\Omega$ 内部所有点的“源强度”（由散度 $\nabla \cdot \mathbf{F}$ 度量）的总和，精确地等于流出该体积边界的总“流量”（由通量 $\mathbf{F} \cdot \mathbf{n}$ 的[面积分](@entry_id:275394)度量）。如果 $\nabla \cdot \mathbf{F}$ 在某点为正，意味着该点是一个源，有净流出；如果为负，则该点是一个汇，有净流入。[高斯散度定理](@entry_id:188065)表明，内部所有源和汇的净效应，必然完全体现在边界的净流出或流入上。

### 在传热学中的物理诠释

为了将抽象的数学定理应用于实际的工程问题，我们需要赋予其物理意义。在传热学中，最核心的矢量场便是**热流密度矢量** $\mathbf{q}$。对于各向同性介质，它由**[傅里叶定律](@entry_id:136311) (Fourier's Law)** 给出：

$$
\mathbf{q}(\mathbf{x}, t) = -k(\mathbf{x}) \nabla T(\mathbf{x}, t)
$$

其中，$k$ 是材料的[热导](@entry_id:189019)率，$T$ 是温度场，$\nabla T$ 是温度梯度。负号表明热量总是从高温区域流向低温区域，即与温度梯度方向相反。

在此背景下，高斯散度定理中的各项具有了明确的物理含义 ：

*   **热流密度矢量 $\mathbf{q}$**：代表在某一点单位时间内垂直于某方向的单位面积上传输的热量，其单位为瓦特每平方米 ($\mathrm{W} \cdot \mathrm{m}^{-2}$)。

*   **法向热流密度 $\mathbf{q} \cdot \mathbf{n}$**：代表热流密度矢量在边界法线方向上的分量。由于 $\mathbf{n}$ 是单位**外**法向矢量，当 $\mathbf{q} \cdot \mathbf{n} > 0$ 时，表示热量正流出控制体；当 $\mathbf{q} \cdot \mathbf{n}  0$ 时，表示热量正流入控制体。

*   **总边界热通量 $\int_{\partial\Omega} \mathbf{q} \cdot \mathbf{n} \, dS$**：代表单位时间内通过整个边界 $\partial\Omega$ 的净热量。其单位为瓦特 ($\mathrm{W}$)。正值表示从控制体中有净热量流出。

*   **热流密度的散度 $\nabla \cdot \mathbf{q}$**：代表在某一点周围单位体积的净热量流出率。如果在一个无穷小的控制体积中心，$\nabla \cdot \mathbf{q}  0$，意味着从该点流出的热量比流入的多，该点表现为一个“热源”。反之，如果 $\nabla \cdot \mathbf{q}  0$，则该点表现为一个“热汇” 。

将高斯散度定理应用于热流密度矢量 $\mathbf{q}$，我们得到：

$$
\int_{\Omega} \nabla \cdot \mathbf{q} \, dV = \int_{\partial\Omega} \mathbf{q} \cdot \mathbf{n} \, dS
$$

这个恒等式说明，体积内所有微元净热量流出率的总和，等于通过该体积边界的总净热量流出率。这正是能量守恒的体现。

我们可以通过[热传导方程](@entry_id:194763)的[微分形式](@entry_id:146747)来加深对 $\nabla \cdot \mathbf{q}$ 物理意义的理解。对于一个固定的控制体，其[能量守恒方程](@entry_id:748978)的积分形式为：

$$
\frac{d}{dt} \int_{\Omega} \rho c T \, dV = -\int_{\partial\Omega} \mathbf{q} \cdot \mathbf{n} \, dS + \int_{\Omega} s \, dV
$$

其中，$\rho$ 是密度，$c$ 是比热容，$s$ 是单位体积的内热源生成率。左边是控制体内能的变化率，右边第一项是流入的净热量（注意负号），第二项是内部生成的热量。

利用[高斯散度定理](@entry_id:188065)改写边界积分项，可得：

$$
\int_{\Omega} \rho c \frac{\partial T}{\partial t} \, dV = -\int_{\Omega} \nabla \cdot \mathbf{q} \, dV + \int_{\Omega} s \, dV
$$

由于该等式对任意控制体 $\Omega$ 都成立，因此被积函数必须处处相等，我们便得到了[热传导方程](@entry_id:194763)的[微分形式](@entry_id:146747)：

$$
\rho c \frac{\partial T}{\partial t} = - \nabla \cdot \mathbf{q} + s
$$

这个方程清晰地揭示了 $\nabla \cdot \mathbf{q}$ 的作用。考虑几种情况 ：

1.  **[稳态](@entry_id:139253)情况** ($\partial T / \partial t = 0$)：方程简化为 $\nabla \cdot \mathbf{q} = s$。此时，热流的散度直接等于内热源的生成率。若某点 $\nabla \cdot \mathbf{q}  0$，必然意味着该点存在一个正的内热源 ($s0$) 来补充净流出的热量。

2.  **无内热源的瞬态情况** ($s=0$)：方程变为 $\rho c (\partial T / \partial t) = - \nabla \cdot \mathbf{q}$。若某点 $\nabla \cdot \mathbf{q}  0$，由于 $\rho c  0$，必然导致 $\partial T / \partial t  0$。这意味着该点的净热量流出是以消耗自身内能为代价的，从而导致局部温度下降。

3.  **对于具有常数热导率 $k$ 的各向同性介质**：$\nabla \cdot \mathbf{q} = \nabla \cdot (-k \nabla T) = -k \nabla^2 T$。因此，$\nabla \cdot \mathbf{q}  0$ 等价于拉普拉斯算子作用于温度场为负，即 $\nabla^2 T  0$。这与[最大值原理](@entry_id:138611)一致，即在没有热源的区域，温度的[极值](@entry_id:145933)只能出现在边界上。

### 全局能量平衡与积分恒等式

上一节导出的[微分形式守恒律](@entry_id:166470)在计算中极为重要，但其积分形式同样具有深刻的物理意义和实用价值。特别是在[稳态](@entry_id:139253)条件下，能量守恒要求系统内部产生的总热量必须等于通过边界散失的总热量。

我们从[稳态热传导](@entry_id:1132353)方程 $\nabla \cdot \mathbf{q} = s$ 出发 。将此方程在整个求解域 $\Omega$ 上进行体积积分：

$$
\int_{\Omega} \nabla \cdot \mathbf{q} \, dV = \int_{\Omega} s \, dV
$$

对左侧的体积积分应用[高斯散度定理](@entry_id:188065)，我们得到：

$$
\int_{\partial\Omega} \mathbf{q} \cdot \mathbf{n} \, dS = \int_{\Omega} s \, dV
$$

这个优美的**全局能量平衡恒等式**表明：在[稳态](@entry_id:139253)下，通过区域边界 $\partial\Omega$ 的总净热流出量 $Q_{out} = \int_{\partial\Omega} \mathbf{q} \cdot \mathbf{n} \, dS$，精确地等于区域 $\Omega$ 内部所有热源产生的总热量 $\int_{\Omega} s \, dV$。这一关系是[检验数](@entry_id:173345)值解是否满足全局能量守恒的重要标准。

**示例：球体[内部热生成](@entry_id:1126624)**

为了将理论付诸实践，让我们考虑一个具体的计算案例 。一个半径为 $R$ 的均匀球体，其热导率为常数 $k$。球内存在一个与半径相关的[体积热源](@entry_id:1133894) $\dot{q}(r) = q_0 r^2$。球体表面维持在恒定温度 $T(R) = T_b$。我们需要验证上述全局能量平衡恒等式。

**第一步：求解温度场和边界热流**

由于问题具有[球对称性](@entry_id:272852)，[稳态热传导](@entry_id:1132353)方程 $\nabla \cdot (-k \nabla T) = \dot{q}(r)$ 在[球坐标系](@entry_id:167517)下简化为：

$$
-k \frac{1}{r^2} \frac{d}{dr} \left( r^2 \frac{dT}{dr} \right) = q_0 r^2
$$

通过两次积分并利用边界条件（$r=0$ 处梯度有限和 $T(R)=T_b$），我们可以解得温度分布为：

$$
T(r) = T_b + \frac{q_0}{20k}(R^4 - r^4)
$$

径向热流密度为 $q_r(r) = -k \frac{dT}{dr} = \frac{q_0 r^3}{5}$。因此，在球体表面 $r=R$ 处，向外的热流密度为 $q_r(R) = \frac{q_0 R^3}{5}$。

**第二步：计算总边界流出热量**

通过边界的总净热流出量 $Q_{out}$ 是将边界热流密度在整个球面上积分得到的。由于 $q_r(R)$ 在球面上是常数，积分简化为热流密度乘以球表面积 $4\pi R^2$：

$$
Q_{out} = \int_{\partial\Omega} \mathbf{q} \cdot \mathbf{n} \, dS = q_r(R) \times (4\pi R^2) = \left( \frac{q_0 R^3}{5} \right) (4\pi R^2) = \frac{4\pi q_0 R^5}{5}
$$

**第三步：计算总体积生热量**

独立地，我们计算球体内热源生成的总热量，即对 $\dot{q}(r)$ 进行体积积分。在[球坐标系](@entry_id:167517)中，体积微元 $dV = 4\pi r^2 dr$：

$$
\int_{\Omega} \dot{q} \, dV = \int_0^R (q_0 r^2) (4\pi r^2) \, dr = 4\pi q_0 \int_0^R r^4 \, dr = 4\pi q_0 \left[ \frac{r^5}{5} \right]_0^R = \frac{4\pi q_0 R^5}{5}
$$

**结论**：通过两种完全独立的路径计算出的结果完全相同，有力地验证了全局能量平衡恒等式 $\int_{\partial\Omega} \mathbf{q} \cdot \mathbf{n} \, dS = \int_{\Omega} \dot{q} \, dV$。对于给定的参数 $q_0 = 1.0 \times 10^8 \, \text{W} \cdot \text{m}^{-5}$ 和 $R = 0.15 \, \text{m}$，计算出的总热量约为 $1.909 \times 10^4 \, \text{W}$。

### 在计算公式中的应用

[高斯散度定理](@entry_id:188065)不仅是物理学的基础，也是现代计算方法（如[有限元法](@entry_id:749389) FEM 和[有限体积法](@entry_id:141374) FVM）的数学支柱。它使得我们能够将描述物理问题的[偏微分](@entry_id:194612)方程（强形式）转化为更适[合数](@entry_id:263553)值离散的积分方程（弱形式或守恒形式）。

#### [格林恒等式](@entry_id:176369)与弱形式

考虑一个具有[各向异性热导率](@entry_id:1121030)张量 $\mathbf{K}(\mathbf{x})$ 的[稳态热传导](@entry_id:1132353)问题，其控制方程为：

$$
-\nabla \cdot (\mathbf{K} \nabla T) = q
$$

为了推导其弱形式，我们将该方程乘以一个任意的**测试函数** $\varphi$，并在整个区域 $\Omega$ 上积分：

$$
-\int_{\Omega} \varphi \, \nabla \cdot (\mathbf{K} \nabla T) \, dV = \int_{\Omega} q \varphi \, dV
$$

这里的关键一步是使用基于高斯散度定理的**[格林第一恒等式](@entry_id:170345)**（或称[分部积分公式](@entry_id:145262)）来处理左侧的项。对于矢量场 $\varphi (\mathbf{K} \nabla T)$ 应用散度定理，并结合[乘积法则](@entry_id:158393)，我们得到：

$$
\int_{\Omega} \nabla \varphi \cdot (\mathbf{K} \nabla T) \, dV = \int_{\partial\Omega} \varphi (\mathbf{n} \cdot \mathbf{K} \nabla T) \, dS - \int_{\Omega} \varphi \nabla \cdot (\mathbf{K} \nabla T) \, dV
$$

将此恒等式代入原[积分方程](@entry_id:138643)，我们得到[弱形式](@entry_id:142897)：

$$
\int_{\Omega} \nabla \varphi \cdot \mathbf{K} \nabla T \, dV = \int_{\partial\Omega} \varphi (\mathbf{n} \cdot \mathbf{K} \nabla T) \, dS + \int_{\Omega} q \varphi \, dV
$$

这个形式将求解一个[二阶微分方程](@entry_id:269365)的问题，转化为了求解一个只涉及函数及其[一阶导数](@entry_id:749425)积分的方程，从而降低了对解的[光滑性](@entry_id:634843)要求。

在[弱形式](@entry_id:142897)中，左侧的[双线性形式](@entry_id:746794) $a(T, \varphi) = \int_{\Omega} \nabla \varphi \cdot \mathbf{K} \nabla T \, dV$ 至关重要。当我们取测试函数等于解本身 ($\varphi=T$) 时，我们得到所谓的**[能量积分](@entry_id:166228)** $\int_{\Omega} \nabla T \cdot \mathbf{K} \nabla T \, dV$ 。由于热导率张量 $\mathbf{K}$ 是[对称正定](@entry_id:145886)的，这个积分总是非负的，并代表了系统由于[热传导](@entry_id:143509)而产生的内部[能量耗散](@entry_id:147406)率。

该积分的**[矫顽性](@entry_id:159399) (coercivity)**，即是否存在常数 $\alpha  0$ 使得 $a(v,v) \ge \alpha \|v\|^2$（在适当的[函数空间](@entry_id:143478)范数下），直接决定了弱形式解的存在性和唯一性。边界条件在此起着决定性作用 ：

*   **齐次[Dirichlet边界条件](@entry_id:142800)** ($T=0$ on $\Gamma_D$)：在这种情况下，[解空间](@entry_id:200470)为 $H_0^1(\Omega)$。利用[Poincaré不等式](@entry_id:142086)，可以证明[能量积分](@entry_id:166228)在该空间上是矫顽的，从而保证了弱[解的唯一性](@entry_id:143619)。
*   **纯[Neumann边界条件](@entry_id:142124)** ($\mathbf{n} \cdot \mathbf{K} \nabla T = g$ on $\partial\Omega$)：此时，任何[常数函数](@entry_id:152060) $T=C$ 都会使[能量积分](@entry_id:166228)为零，因此[双线性形式](@entry_id:746794)在 $H^1(\Omega)$ 空间上不是矫顽的。解至多在一个任意常数下是唯一的。
*   **[Robin边界条件](@entry_id:163914)** ($\mathbf{n} \cdot \mathbf{K} \nabla T + hT = g$ on $\Gamma_R$)：这种边界条件在[弱形式](@entry_id:142897)中引入了一个额外的边界积分项 $\int_{\Gamma_R} h T \varphi \, dS$。当 $\varphi=T$ 且 $h0$ 时，这个项 $\int_{\Gamma_R} h T^2 \, dS$ 是正的，它有助于增强[双线性形式](@entry_id:746794)的[矫顽性](@entry_id:159399)，即使在没有[Dirichlet边界条件](@entry_id:142800)的情况下也能确保[解的唯一性](@entry_id:143619)。

#### [曲线坐标系](@entry_id:172561)与映射单元

在处理复杂几何形状时，直接在物理域上构建网格和求解方程是困难的。FEM和FVM等方法通常采用一种更灵活的策略：将物理空间中形状不规则的单元 $\Omega$ 通过一个光滑的、可逆的映射 $\mathbf{x} = \mathbf{x}(\boldsymbol{\xi})$，与一个计算空间中形状规则的[参考单元](@entry_id:168425)（如立方体 $\hat{\Omega}=[-1,1]^3$）关联起来。

在这种情况下，所有的计算都在[参考单元](@entry_id:168425)上进行。然而，[像散](@entry_id:174378)度这样的[微分算子](@entry_id:140145)和积分本身必须被正确地转换，以反映物理空间的几何形变。这正是[张量分析](@entry_id:161423)和高斯散度定理发挥作用的地方。

关键的几何量是**[雅可比矩阵](@entry_id:178326)** $[\partial\mathbf{x}/\partial\boldsymbol{\xi}]$ 及其行列式 $J = \det[\partial\mathbf{x}/\partial\boldsymbol{\xi}]$。$J$ 度量了从参考空间到物理空间的体积微元的缩放因子，即 $dV = J \, d\hat{V}$。

在[曲线坐标系](@entry_id:172561) $\boldsymbol{\xi} = (\xi^1, \xi^2, \xi^3)$ 中，一个矢量场 $\mathbf{q}$ 的散度表达式变为 ：

$$
\nabla \cdot \mathbf{q} = \frac{1}{J} \frac{\partial}{\partial \xi^i} (J q^i)
$$

这里，$q^i = \mathbf{q} \cdot \mathbf{a}^i$ 是 $\mathbf{q}$ 的**[逆变分量](@entry_id:185440)**，$\mathbf{a}^i$ 是与[协变基](@entry_id:198968)矢量 $\mathbf{a}_j = \partial\mathbf{x}/\partial\xi^j$ 对偶的[逆变基](@entry_id:197906)矢量。这个公式说明，在[曲线坐标系](@entry_id:172561)中计算散度时，必须考虑雅可比行列式 $J$ 的空间变化。

同样，通过边界的[通量积分](@entry_id:138365)也需要转换。考虑[参考单元](@entry_id:168425)上一个由 $\xi^1 = \text{constant}$ 定义的面 $\hat{\Gamma}$，其在物理空间中对应的面为 $\Gamma$。通过 $\Gamma$ 的通量可以被转换为在 $\hat{\Gamma}$ 上的积分 ：

$$
\int_{\Gamma} \mathbf{q} \cdot \mathbf{n} \, dS = \int_{\hat{\Gamma}} J q^1 \, d\hat{S}
$$

其中 $d\hat{S}$ 是参考面上的面积微元。这个关系的核心是面积微元的变换：$d\mathbf{S} = \mathbf{n} dS = J \mathbf{a}^1 d\hat{S}$。这表明，物理空间中的法向通量可以通过计算参考空间中相应的[逆变分量](@entry_id:185440) $q^1$ 与雅可比行列式 $J$ 的乘积并积分得到。这些变换公式是所有基于映射单元的计算方法正确实施能量守恒的基础。

### 高级主题与推广

高斯散度定理的强大之处在于其普适性，它能够被推广以处理更复杂的物理和几何情境。

#### 多连通区域

许多工程结构具有内部空腔或孔洞，形成所谓的**多连通区域**。例如，一个带冷却通道的涡轮叶片。在这种情况下，物理域 $\Omega$ 的边界 $\partial\Omega$ 不再是单一的封闭曲面，而是由一个外部边界 $\Gamma_{\text{ext}}$ 和一个或多个内部边界 $\Gamma_i$ 组成 。

[高斯散度定理](@entry_id:188065)依然成立，但边界积分必须包含所有边界部分：

$$
\int_{\Omega} \nabla \cdot \mathbf{q} \, dV = \int_{\Gamma_{\text{ext}}} \mathbf{q} \cdot \mathbf{n} \, dS + \sum_{i=1}^{m} \int_{\Gamma_i} \mathbf{q} \cdot \mathbf{n} \, dS
$$

这里的关键在于对**单位外法向矢量** $\mathbf{n}$ 的正确理解。对于区域 $\Omega$ 而言，“外”指的是离开该区域的方向。因此，在外部边界 $\Gamma_{\text{ext}}$ 上，$\mathbf{n}$ 指向区域的外部；而在每个内部空腔的边界 $\Gamma_i$ 上，$\mathbf{n}$ 指向空腔内部。遵循这一约定，全局[能量平衡方程](@entry_id:191484) $\int_{\Omega} s \, dV = \int_{\partial\Omega} \mathbf{q} \cdot \mathbf{n} \, dS$ 自然地包含了流向所有内部和外部边界的总热量。

#### 非光滑边界

经典的[高斯散度定理](@entry_id:188065)证明依赖于边界的良好性质，如 $C^1$ 光滑或至少是Lipschitz连续。然而，实际工程几何体中充满了尖角、棱线，甚至可能存在更奇异的**[尖点](@entry_id:636792) (cusp)**。在这些点上，边界不是[Lipschitz连续的](@entry_id:267396)，经典的法向定义和证明方法失效 。

现代数学（特别是[几何测度论](@entry_id:187987)）为处理这类问题提供了强大的工具。对于一类比Lipschitz区域更广泛的“[有限周长集](@entry_id:202067)”，可以定义一个所谓的**既约边界** $\partial^*\Omega$ 和一个**[测度论](@entry_id:139744)意义上的法向**。对于定义在这些区域上且属于特定[索伯列夫空间](@entry_id:141995) $H(\text{div}, \Omega)$ 的矢量场（即场本身及其散度都是平方可积的），一个推广的[散度定理](@entry_id:143110)仍然成立 。

这个理论的意义在于，它为在具有几何[奇异点](@entry_id:199525)的区域上应用基于[守恒律的数值方法](@entry_id:752804)（如FVM）提供了严格的数学基础。它确保了即使在网格不断细化以逼近尖点时，离散的[通量平衡](@entry_id:637776)也能收敛到物理上正确的、在整个广义边界上都守恒的极限，从而保证了数值解的能量守恒性。

#### 时变区域

在许多问题中，如相变过程、热膨胀或[流固耦合](@entry_id:1125339)，计算区域 $\Omega(t)$ 本身会随时间变化。在这种情况下，对一个在时变区域上积分的量求时间导数，不能简单地将导数移入积分号内。此时，必须借助**雷诺输运定理 (Reynolds Transport Theorem, RTT)**。

雷诺输运定理给出了一个在移动和变形的控制体 $\Omega(t)$ 上积分的物理量 $\phi$ 的总变化率 ：

$$
\frac{d}{dt} \int_{\Omega(t)} \phi \, dV = \int_{\Omega(t)} \frac{\partial \phi}{\partial t} \, dV + \int_{\partial\Omega(t)} \phi (\mathbf{w} \cdot \mathbf{n}) \, dS
$$

其中 $\mathbf{w}(\mathbf{x}, t)$ 是控制体边界自身的运动速度（在任意拉格朗日-欧拉，即[ALE方法](@entry_id:174313)中，这被称为网格速度）。第一项是由于场 $\phi$ 自身随时间变化引起的，第二项是由于控制体边界运动“扫过”场 $\phi$ 引起的。

在建立能量守恒方程时，我们需要结合物理定律、雷诺输运定理和高斯散度定理。能量守恒定律指出，控制体内能的总变化率等于通过边界的净能量通量与内部源项之和。这里的关键是，通过运动边界的[对流通量](@entry_id:158187)取决于[流体速度](@entry_id:267320) $\mathbf{v}$ 相对于边界速度 $\mathbf{w}$ 的**相对速度** $(\mathbf{v}-\mathbf{w})$。因此，正确的积分[能量平衡方程](@entry_id:191484)为 ：

$$
\frac{d}{dt}\int_{\Omega(t)} \phi\,dV = - \int_{\partial \Omega(t)} \left( \mathbf{q} + \phi\,(\mathbf{v}-\mathbf{w}) \right) \cdot \mathbf{n} \, dS + \int_{\Omega(t)} s\,dV
$$

其中 $\phi=\rho c T$ 是热能密度。现在，将[雷诺输运定理](@entry_id:191217)用于左侧，并将[高斯散度定理](@entry_id:188065)用于右侧的边界积分，经过化简，一个奇妙的结果出现了：包含任意网格速度 $\mathbf{w}$ 的项会完全抵消。最终，我们得到了与网格运动无关的、在物理上普适的局部[能量守恒方程](@entry_id:748978)：

$$
\frac{\partial \phi}{\partial t} + \nabla \cdot (\phi \mathbf{v} + \mathbf{q}) = s
$$

这个推导过程清楚地表明，[雷诺输运定理](@entry_id:191217)对于正确处理存储项的时间导数是必不可少的，而[高斯散度定理](@entry_id:188065)则用于处理通量项。两者的结合是建立移动和变形域上守恒型方程的严谨途径，也是ALE等高级计算方法的核心理论基础。