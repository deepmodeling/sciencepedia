## 引言
在现代科学与工程领域，从[无线通信](@entry_id:266253)到医学成像，再到[隐身技术](@entry_id:264201)，对[电磁波传播](@entry_id:272130)的精确预测至关重要。麦克斯韦方程组是描述这些现象的基石，而间断伽辽金（Discontinuous Galerkin, DG）方法已成为求解该[方程组](@entry_id:193238)的一种极其强大和灵活的数值工具。与传统方法相比，DG方法在处理复杂几何、非均匀材料以及实现[高阶精度](@entry_id:750325)和并行计算方面展现出独特优势，但其背后的原理和应用广度也为学习者带来了挑战。本文旨在系统性地揭示DG方法的内在机制及其在计算电磁学中的前沿应用。

本文将分为三个核心部分。在“原理与机制”一章中，我们将深入其数学心脏，从弱形式的构建到数值通量的选择，再到[能量守恒](@entry_id:140514)性的证明，为您奠定坚实的理论基础。接着，在“应用与跨学科连接”中，我们将视野扩展到真实世界，探讨DG方法如何模拟超材料、处理[非协调网格](@entry_id:752550)、实现[多物理场耦合](@entry_id:171389)，并与[高性能计算](@entry_id:169980)[范式](@entry_id:161181)深度融合。最后，“动手实践”部分将提供精选的编程练习，引导您将理论知识转化为解决实际问题的能力。通过这一结构化的学习路径，读者将全面掌握DG方法，并获得将其应用于前沿研究与工程挑战的信心和技能。

## 原理与机制

本章深入探讨了求解麦克斯韦方程组的间断 Galerkin (DG) 方法的数学原理和核心机制。我们将从其基本弱形式出发，系统地阐述该方法的构建、[能量守恒](@entry_id:140514)特性、实际实现的关键方面、精度行为，并讨论一些高级主题，如散度[误差控制](@entry_id:169753)和与相关[离散化方法](@entry_id:272547)的联系。

### 麦克斯韦方程的半离散[DG格式](@entry_id:178043)

麦克斯韦方程组在无源、线性、各向同性的介质中，可写为以下[一阶偏微分方程](@entry_id:178306)组形式：
$$
\varepsilon \frac{\partial \boldsymbol{E}}{\partial t} - \nabla \times \boldsymbol{H} = \boldsymbol{0}
$$
$$
\mu \frac{\partial \boldsymbol{H}}{\partial t} + \nabla \times \boldsymbol{E} = \boldsymbol{0}
$$
其中 $\boldsymbol{E}$ 和 $\boldsymbol{H}$ 分别是电场和磁场强度，$\varepsilon$ 和 $\mu$ 分别是介质的[介电常数](@entry_id:146714)和磁导率。

DG 方法的第一步是将计算域 $\Omega$ 剖分为一个不重叠的单元集合 $\mathcal{T}_h$，其中每个单元记为 $K$。与要求解在单元间连续的传统有限元方法不同，DG 方法在所谓的**间断[多项式空间](@entry_id:144410)**中寻找近似解。这意味着近似解 $\boldsymbol{E}_h$ 和 $\boldsymbol{H}_h$ 在每个单元 $K$ 内部是多项式，但在单元边界上不要求连续。

选择[间断函数](@entry_id:143848)空间是基于深刻的物理和数学考量。首先，[麦克斯韦方程组](@entry_id:150940)本质上是一个**[双曲系统](@entry_id:260647)**，其解（[电磁波](@entry_id:269629)）本身就允许存在间断，例如[波前](@entry_id:197956)。当波穿过不同材料的交界面时，场量也可能发生跳跃。在一个不要求跨单元连续性的函数空间中，可以自然地表示这些物理现象，而强加连续性则会过度约束问题，尤其是在[非均匀介质](@entry_id:750241)中。

为了构建 DG 格式，我们在每个单元 $K$ 上将控制方程乘以一个矢量**测试函数** $\boldsymbol{v}$（取自与解函数相同的多项式空间），然后进行积分。以法拉第定律为例：
$$
\int_K \left( \mu \frac{\partial \boldsymbol{H}_h}{\partial t} \right) \cdot \boldsymbol{v} \, \mathrm{d}x + \int_K (\nabla \times \boldsymbol{E}_h) \cdot \boldsymbol{v} \, \mathrm{d}x = 0
$$
DG 方法的关键一步是对包含[旋度算子](@entry_id:184984)的项使用**[分部积分](@entry_id:136350)**。利用矢量恒等式 $\int_K (\nabla \times \boldsymbol{A}) \cdot \boldsymbol{B} \, \mathrm{d}x = \int_K \boldsymbol{A} \cdot (\nabla \times \boldsymbol{B}) \, \mathrm{d}x + \int_{\partial K} (\boldsymbol{n}_K \times \boldsymbol{A}) \cdot \boldsymbol{B} \, \mathrm{d}s$，其中 $\boldsymbol{n}_K$ 是单元 $K$ 的外法向单位矢量，我们将空间导数从待求的解 $\boldsymbol{E}_h$ 转移到测试函数 $\boldsymbol{v}$ 上：
$$
\int_K \mu \frac{\partial \boldsymbol{H}_h}{\partial t} \cdot \boldsymbol{v} \, \mathrm{d}x + \int_K \boldsymbol{E}_h \cdot (\nabla \times \boldsymbol{v}) \, \mathrm{d}x - \int_{\partial K} (\boldsymbol{n}_K \times \boldsymbol{E}_h) \cdot \boldsymbol{v} \, \mathrm{d}s = 0
$$
这个过程在单元边界 $\partial K$ 上引入了一个[面积分](@entry_id:275394)项。由于解 $\boldsymbol{E}_h$ 在单元边界上是间断的，其[迹线](@entry_id:261720)（即从单元内部趋近边界时的值）是双值的。为了定义一个唯一的边界值并建立相邻单元间的耦合，我们引入了**[数值通量](@entry_id:752791)**（numerical flux）的概念，记为 $\widehat{\boldsymbol{n}_K \times \boldsymbol{E}}$。[数值通量](@entry_id:752791)是根据单元内部和相邻单元的场值构造的，它近似了边界上的[切向电场](@entry_id:267195)。其作用是[弱形式](@entry_id:142897)地（而非强加地）实现物理上要求的切向场连续性条件。

将[数值通量](@entry_id:752791)代入，我们得到 DG 方法的最终半离散[弱形式](@entry_id:142897)：寻找 $\boldsymbol{E}_h, \boldsymbol{H}_h \in \boldsymbol{V}_h^p$（$p$ 为多项式次数），使得对于所有测试函数 $\boldsymbol{v}_E, \boldsymbol{v}_H \in \boldsymbol{V}_h^p$ 和所有单元 $K \in \mathcal{T}_h$ 成立：
$$
\int_K \varepsilon \frac{\partial \boldsymbol{E}_h}{\partial t} \cdot \boldsymbol{v}_E \, \mathrm{d}x - \int_K \boldsymbol{H}_h \cdot (\nabla \times \boldsymbol{v}_E) \, \mathrm{d}x + \int_{\partial K} (\boldsymbol{n}_K \times \boldsymbol{v}_E) \cdot \widehat{\boldsymbol{n}_K \times \boldsymbol{H}} \, \mathrm{d}s = 0
$$
$$
\int_K \mu \frac{\partial \boldsymbol{H}_h}{\partial t} \cdot \boldsymbol{v}_H \, \mathrm{d}x + \int_K \boldsymbol{E}_h \cdot (\nabla \times \boldsymbol{v}_H) \, \mathrm{d}x - \int_{\partial K} (\boldsymbol{n}_K \times \boldsymbol{v}_H) \cdot \widehat{\boldsymbol{n}_K \times \boldsymbol{E}} \, \mathrm{d}s = 0
$$
在这个系统中，单元间的耦合完全通过包含[数值通量](@entry_id:752791)的[面积分](@entry_id:275394)项实现。这导致了高度局部化的[代数结构](@entry_id:137052)，是 DG 方法并行计算效率高的关键原因之一。

### 能量原理：守恒与稳定性

[数值格式](@entry_id:752822)的稳定性是其可靠性的基本要求。对于模拟物理波动的麦克斯韦方程，我们尤其关心离散系统是否能正确地反映物理能量的演化。一个关键的分析工具是**离散 Poynting 定理**，它描述了离散[电磁能](@entry_id:264720)量的时间变化率。

我们定义半离散[电磁能](@entry_id:264720)量为所有单元内能量之和：
$$
\mathcal{E}_h(t) := \frac{1}{2} \sum_{K \in \mathcal{T}_h} \int_{K} \left( \varepsilon |\boldsymbol{E}_h|^2 + \mu |\boldsymbol{H}_h|^2 \right) \, \mathrm{d}x
$$
通过在 DG [弱形式](@entry_id:142897)中选取测试函数等于解本身（即 $\boldsymbol{v}_E = \boldsymbol{E}_h$ 和 $\boldsymbol{v}_H = \boldsymbol{H}_h$），然后将两个方程相加并对所有单元求和，我们可以推导出能量的时间导数。经过一系列矢量[恒等变换](@entry_id:264671)，可以证明，能量的变化率完全由穿过单元边界的数值通量决定。这体现了**局部[能量守恒](@entry_id:140514)**原理：每个单元内能量的变化等于通过其边界的数值[能量通量](@entry_id:266056)净额。

能量的全局行为（守恒或耗散）直接取决于数值通量的具体选择。考虑一个由单元 $K^-$ 和 $K^+$ 共享的内部界面 $F$，其[法向量](@entry_id:264185) $\boldsymbol{n}$ 从 $K^-$ 指向 $K^+$。我们定义场 $\boldsymbol{v}$ 的平均和跳跃算子：
$$
\{\!\{\boldsymbol{v}\}\!\} := \frac{\boldsymbol{v}^{-} + \boldsymbol{v}^{+}}{2}, \qquad [\![ \boldsymbol{v} ]\!] := \boldsymbol{n} \times (\boldsymbol{v}^{+} - \boldsymbol{v}^{-})
$$

一个常见的通量族是**阻抗加权通量**，它由一个参数 $\eta \in [0,1]$ 控制：
$$
\boldsymbol{n}\times \widehat{\mathbf{E}}_{h} = \boldsymbol{n}\times \{\!\{\mathbf{E}_{h}\}\!\} + \frac{\eta}{2}\, Z \,[\![ \mathbf{H}_{h}]\!]
$$
$$
\boldsymbol{n}\times \widehat{\mathbf{H}}_{h} = \boldsymbol{n}\times \{\!\{\mathbf{H}_{h}\}\!\} - \frac{\eta}{2}\, Y \,[\![ \mathbf{E}_{h}]\!]
$$
其中 $Z = \sqrt{\mu/\varepsilon}$ 和 $Y = \sqrt{\varepsilon/\mu}$ 分别是介质的[波阻抗](@entry_id:276571)和[波导](@entry_id:198471)纳。

*   **[中心通量](@entry_id:747204)** ($\eta=0$)：当 $\eta = 0$ 时，[数值通量](@entry_id:752791)就是场的简单平均。对于这类通量，可以证明在周期性或[理想电导体](@entry_id:753331)（PEC）边界条件下，总的离散能量是精确守恒的，即 $\frac{\mathrm{d}\mathcal{E}_h}{\mathrm{d}t} = 0$。这表明[中心通量](@entry_id:747204)格式是无耗散的。

*   **上风通量** ($\eta > 0$)：当 $\eta > 0$ 时，例如取 $\eta=1$ 的纯上风格式，[能量导数](@entry_id:170468)变为一个非正项：
    $$
    \frac{\mathrm{d}\mathcal{E}_h}{\mathrm{d}t} = - \sum_{F \in \mathcal{F}_h^{\mathrm{int}}} \int_F \frac{\eta}{2} \left( Y |[\![\mathbf{E}_h]\!]|^2 + Z |[\![\mathbf{H}_h]\!]|^2 \right) \mathrm{d}s \le 0
    $$
    这意味着总能量随时间单调不增。能量的耗散量与界面上场切向分量的跳跃（即不连续性）的平方成正比。这种**数值耗散**有助于抑制由离散化引起的非物理[振荡](@entry_id:267781)，从而增强格式的稳定性。

通过选择不同的[数值通量](@entry_id:752791)，DG 方法提供了在[能量守恒](@entry_id:140514)和数值稳定性之间进行权衡的灵活性，这是其强大的特征之一。

### 实现细节：[基函数](@entry_id:170178)与[几何映射](@entry_id:749852)

将 DG 弱形式转化为可计算的代数系统，需要处理两个关键的实现方面：单元内多项式[基函数](@entry_id:170178)的选择和从规则的参考单元到物理空间中可能弯曲的单元的[几何映射](@entry_id:749852)。

#### [基函数](@entry_id:170178)与质量矩阵

在 DG 格式的[时间演化](@entry_id:153943)项中，会出现形如 $\int_K \varepsilon \boldsymbol{E}_h \cdot \boldsymbol{v}_E \, \mathrm{d}x$ 的积分。当用一组[基函数](@entry_id:170178) $\phi_i$ 展开解和测试函数时，这会产生所谓的**[质量矩阵](@entry_id:177093)** $M_{ij} = \int_K \varepsilon \phi_i \phi_j \, \mathrm{d}V$。[质量矩阵](@entry_id:177093)的结构对[计算效率](@entry_id:270255)，特别是对[显式时间积分](@entry_id:165797)方法的效率，有至关重要的影响。

*   **[模态基](@entry_id:752055)函数 (Modal Basis)**：这类[基函数](@entry_id:170178)通常由在一维参考单元 $[-1,1]$ 上相互正交的多项式（如 Legendre 多项式）通过张量积构造而成。由于其 $L^2$ 正交性，即 $\int_{\hat{K}} \hat{\phi}_i \hat{\phi}_j \, d\hat{V} = \delta_{ij}$，在[仿射映射](@entry_id:746332)（即 Jacobian 为常数）的单元上进行精确积[分时](@entry_id:274419)，质量矩阵是**对角的**。[对角质量矩阵](@entry_id:173002)的求逆是平凡的，这使得[显式时间步进](@entry_id:168157)极为高效。

*   **[节点基](@entry_id:752522)函数 (Nodal Basis)**：这类[基函数](@entry_id:170178)由 Lagrange 多项式构成，其在单元内的一组特定节点上取值为 1，在其他节点上为 0。
    *   如果对[节点基](@entry_id:752522)函数使用**精确积分**，由于 Lagrange 多项式通常不是 $L^2$ 正交的，得到的[质量矩阵](@entry_id:177093)（称为**[一致质量矩阵](@entry_id:174630)**）是**非对角的**（即稠密的），其求逆运算代价高昂。
    *   然而，一个非常流行且高效的策略是将[节点基](@entry_id:752522)函数的节点与**[数值求积](@entry_id:136578)**的求积点配置在一起。例如，使用基于 [Gauss-Lobatto-Legendre](@entry_id:749736) (GLL) 节点的 Lagrange [基函数](@entry_id:170178)，并采用 GLL 求积公式来近似计算质量矩阵积分。由于 Lagrange [基函数](@entry_id:170178)在节点上的 Kronecker delta 性质 ($\phi_i(\boldsymbol{x}_j) = \delta_{ij}$)，求积公式的求和会立即对角化，得到一个对角矩阵（称为**[集总质量矩阵](@entry_id:173011)**）。虽然这是一种近似，但它极大地简化了计算，并且对于许多应用而言精度足够。
    *   一个特殊的例子是，如果[节点基](@entry_id:752522)函数构建在 Gauss-Legendre 求积点上，这些[基函数](@entry_id:170178)恰好是 $L^2$ 正交的。因此，即使使用精确积分，它们也能产生对角的质量矩阵。

#### 处理复杂几何：曲线元

为了模拟具有弯曲边界的复杂物体，我们需要使用能够贴合这些边界的曲线单元。这通过一个从简单参考单元（如单位立方体 $\widehat{K} = [-1,1]^3$）到物理空间中曲线单元 $K$ 的[光滑映射](@entry_id:203730) $\boldsymbol{x} = \boldsymbol{x}(\boldsymbol{\xi})$ 来实现。

这个映射引入了度量项，必须在[弱形式](@entry_id:142897)中加以考虑。关键的变换关系涉及到 **Jacobian 矩阵** $\boldsymbol{A} = \partial \boldsymbol{x}/\partial \boldsymbol{\xi}$，其[行列式](@entry_id:142978) $J = \det(\boldsymbol{A})$，以及**余因子矩阵** $\boldsymbol{C} = J \boldsymbol{A}^{-T}$。利用 **Piola 变换**，可以将物理空间中的[旋度算子](@entry_id:184984)与参考空间中[旋度算子](@entry_id:184984)通过几何度量项联系起来。这个变换是至关重要的，因为它允许我们将所有计算都在固定的参考单元 $\widehat{K}$ 上执行。DG 弱形式中的体积积分项，例如 $\int_K \boldsymbol{H}_h \cdot (\nabla \times \boldsymbol{v}_E) \, \mathrm{d}x$，被变换为在参考单元上的积分，其被积函数中包含了这些依赖于[几何映射](@entry_id:749852)的度量项。

需要注意的是，对于曲线单元，Jacobian [行列式](@entry_id:142978) $J(\boldsymbol{\xi})$ 通常不再是常数，而是坐标的函数。这意味着即使使用模态正交基，[质量矩阵](@entry_id:177093) $\int_{\hat{K}} \varepsilon \hat{\phi}_i \hat{\phi}_j J(\boldsymbol{\xi}) \, d\hat{V}$ 也通常不再是对角的。这是处理复杂几何时必须付出的计算代价。

### 精度与长时间行为

DG 方法的精度不仅取决于多项式次数和网格尺寸，还与被求解波的频率（或波数）密切相关。

#### [色散](@entry_id:263750)与耗散误差

任何空间离散格式都会引入与物理波传播特性的偏差。这些偏差主要表现为两种形式：

*   **[色散误差](@entry_id:748555) (Dispersion Error)**：数值波的相速度依赖于频率，即使在物理上非[色散](@entry_id:263750)的介质中也是如此。这导致不同频率的波以不同的速度传播，从而使[波包](@entry_id:154698)变形。这表现为**相位误差**。
*   **耗散误差 (Dissipation Error)**：数值波的振幅随时间衰减，即使在物理上无损的介质中也是如此。这表现为**振幅误差**。

我们可以通过对一个简单的模型问题进行**[色散](@entry_id:263750)分析**来量化这些误差。考虑一维麦克斯韦方程，并采用 $p=0$（分段常数）的 DG 格式和上风通量。通过代入[平面波解](@entry_id:195230)的离散形式 $U_j(t) = \hat{U} \exp(i(k x_j - \omega_{num} t))$，可以推导出数值角频率 $\omega_{num}$ 与物理[波数](@entry_id:172452) $k$ 之间的关系，即**[数值色散关系](@entry_id:752786)**。

对于上述例子，我们得到一个复数值的 $\omega_{num} = \omega_R + i\omega_I$。其实部 $\omega_R = \frac{c}{h}\sin(kh)$ 决定了数值相速度 $v_p = \omega_R/k$，而其虚部 $\omega_I = -\frac{c}{h}(1-\cos(kh))$ 决定了[数值耗散](@entry_id:168584)。与精确的[色散关系](@entry_id:140395) $\omega = ck$ 相比，我们可以计算出[相位误差](@entry_id:162993)、振幅误差以及群速度 $v_g = d\omega_R/dk$ 的误差。这些分析为我们提供了关于格式在不同分辨率（由无量纲参数 $kh$ 或每波长点数衡量）下表现的定量认识。

#### 污染效应与 hp 自适应

对于波传播问题，一个特别具有挑战性的现象是**污染效应**（pollution effect）。[色散](@entry_id:263750)分析表明，对于固定的网格尺寸 $h$ 和多项式次数 $p$，相对相位误差通常随着波数 $k$ 的增加而增长。例如，对于一维 $p=0$ 的情况，相对相位误差 $(k_{num}-k)/k$ 的[主导项](@entry_id:167418)为 $-\frac{k^2h^2}{6}$。

这意味着，当模拟高频波（大 $k$）或进行长距离传播时，即使每波长的网格点数保持不变，累积的相位误差也会显著增长，最终“污染”整个数值解。为了在给定误差容限 $\varepsilon$ 内控制污染效应，我们需要更精细的分辨率。上述分析表明，无量纲乘积 $kh$ 必须满足一个界限，例如 $kh \le \sqrt{6\varepsilon}$。这启发了 **[hp-自适应](@entry_id:750398)**策略，即根据局部波的特性，动态地调整网格尺寸 $h$ 和/或多项式次数 $p$，以经济高效地达到期望的精度。

### [DG格式](@entry_id:178043)的高级主题

除了上述基本原理，DG 方法的研究还涵盖了许多高级和专门的主题，以解决特定挑战并提升性能。

#### 散度问题与散度清除策略

麦克斯韦方程组除了包含两个旋度演化方程外，还隐含了两个散度约束，即高斯定律：$\nabla \cdot (\varepsilon \boldsymbol{E}) = \rho$ 和 $\nabla \cdot (\mu \boldsymbol{H}) = 0$。在连续理论中，如果这两个定律在初始时刻成立，那么旋度方程会自动保证它们在所有后续时间都成立。

然而，在标准的 DG 离散化中，这个性质通常会丢失。离散的[旋度算子](@entry_id:184984)和[散度算子](@entry_id:265975)之间的代数关系不再能保证散度守恒。其结果是，即使初始场是无散的，[数值误差](@entry_id:635587)也会在[时间演化](@entry_id:153943)中不断累积，产生非物理的**散度误差**。这种误差可能导致严重的伪振荡甚至计算崩溃。

为了解决这个问题，研究者们提出了多种**散度清除**（divergence cleaning）策略：

*   **[广义拉格朗日乘子 (GLM)](@entry_id:749786) 方法**：该方法引入一个辅助标量场，并修改麦克斯韦方程组。修改后的系统将散度误差转化为一个以特定速度传播并可被阻尼的波。这样，散度误差就不会在原地累积，而是被主动地传输出计算域或被耗散掉。

*   **惩罚通量**：另一种策略是修改[数值通量](@entry_id:752791)，加入一个惩罚项，该惩罚项与界面上场法向分量的跳跃成正比。由于离散散度与法向跳跃直接相关，这种惩罚机制可以有效地抑制散度误差的增长。

#### 与协调方法和[伪模式](@entry_id:163321)的联系

在求解电磁谐振腔的本征值问题时，散度问题变得尤为突出。亥姆霍兹方程 $\nabla \times (\mu^{-1} \nabla \times \boldsymbol{E}) = \omega^2 \varepsilon \boldsymbol{E}$ 的旋-旋算子有一个巨大的零空间，由所有无旋度场（即梯度场 $\nabla\phi$）构成。物理上，只有无散的[无旋场](@entry_id:183486)（即满足 $\nabla \cdot (\varepsilon \nabla \phi) = 0$ 的场）才是有效的直流解。如果数值格式不能正确地实施[无散约束](@entry_id:755035)，它会计算出大量非物理的、对应于[梯度场](@entry_id:264143)的**[伪模式](@entry_id:163321)**（spurious modes），从而严重污染本征谱。

与 DG 形成对比的是**[协调有限元](@entry_id:170866)方法**，特别是使用 **Nédélec（边）单元**的方法。这类单元天生满足切向连续性，属于 $H(\text{curl})$ 协调空间。更重要的是，Nédélec 单元的构造遵循了离散 de Rham 复形的深刻数学结构，该结构精确地模拟了连续空间中梯度、[旋度和散度](@entry_id:269913)算子之间的关系。因此，基于 Nédélec 单元的格式能够自然地将无旋[梯度场](@entry_id:264143)与物理[模式分离](@entry_id:199607)开，从而避免[伪模式](@entry_id:163321)的产生。

标准的 DG 格式不具备这种内在结构，因此容易受到[伪模式](@entry_id:163321)的困扰。这再次凸显了为 DG 格式配备有效的散度控制机制的重要性。同时，也有研究致力于构建能够再现离散精确序列性质的 DG 格式，以从根本上解决此问题。

#### 可杂交间断Galerkin (HDG) 方法

HDG 方法是 DG 的一个重要变体，它旨在结合 DG 的灵活性和传统有限元方法[计算效率](@entry_id:270255)的某些优点。HDG 的核心思想是在网格的所有界面（骨架）上引入一个新的全局未知量，称为**混合变量**（hybrid variable），例如，用 $\widehat{\boldsymbol{E}}_{t,h}$ 来近似[电场](@entry_id:194326)的切向迹。

然后，原始的[偏微分方程](@entry_id:141332)被分解为两部分：
1.  一组**局部问题**：在每个单元上，场变量 $(\boldsymbol{E}_h, \boldsymbol{H}_h)$ 可以完全用该单元边界上的混合变量 $\widehat{\boldsymbol{E}}_{t,h}$ 来表示和求解。这一步可以在所有单元上并行完成。
2.  一个**全局问题**：通过要求数值通量的连续性，导出一个只涉及混合变量 $\widehat{\boldsymbol{E}}_{t,h}$ 的、耦合了所有界面的全局线性系统。

这种方法的优势在于，最终需要求解的全局系统只定义在网格的界面上，其自由度数量通常远少于标准 DG 方法中所有体积自由度的总和。

与标准 DG 类似，HDG 的稳定性和能量特性也由其[数值通量](@entry_id:752791)决定。在一个典型的 HDG 格式中，会引入一个稳定化参数 $\tau$。能量分析表明，系统的能量变化率与这个参数直接相关。例如，要实现精确的[能量守恒](@entry_id:140514)，必须取 $\tau=0$。然而，为了保证格式的稳定性，通常需要选择一个非零的 $\tau$ 值来引入适量的数值耗散。