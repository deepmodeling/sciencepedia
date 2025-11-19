## 引言
在工程与科学计算中，准确描述外部作用力是预测结构行为的关键。然而，现实世界中的大多数载荷，如重力、流体压力或[表面摩擦力](@entry_id:152983)，并非作用于单点的集中力，而是连续分布在物体的体积、表面或边线上。将这些连续的物理作用精确地转化为离散有限元模型能够“理解”的语言，是所有[有限元分析](@entry_id:138109)面临的根本挑战之一。这不仅是一个[数值近似](@entry_id:161970)问题，更关系到计算结果是否在能量和静力学上与物理现实保持一致。

本文旨在系统性地解决这一问题，为研究生及高级工程师提供一份关于在有限元方法中建模[分布](@entry_id:182848)式载荷与[体力](@entry_id:174230)的全面指南。我们将从第一性原理出发，逐步揭示从连续载荷到等效节点力的完整推导路径，并展示其在复杂工程与[交叉](@entry_id:147634)学科问题中的强大应用。

*   在**“原理与机制”**一章中，我们将回归到[有限元法](@entry_id:749389)的基石——[虚功原理](@entry_id:138749)，阐明体力、面力和线载荷如何通过虚[功积分](@entry_id:181218)被统一表达。随后，我们将深入探讨离散化过程的核心，即如何通过形函数将连续载荷一致地分配到单元节点上，形成“等效节点力”。我们还将讨论[数值积分](@entry_id:136578)的精度要求以及在[非线性](@entry_id:637147)分析中处理构型相关载荷等高级主题。
*   在**“应用与交叉学科联系”**一章中，我们将展示这些基本原理的广泛适用性。通过一系列从经典固体力学到流固耦合、[压电效应](@entry_id:138222)、接触力学乃至生物力学的案例，您将看到统一的载荷建模框架如何跨越学科边界，解决多样化的实际问题。
*   最后，在**“动手实践”**部分，我们设计了三个逐步深入的编程练习，旨在帮助您将理论知识转化为实践技能，学会如何实现、验证和应用[分布](@entry_id:182848)式载荷的建模技术。

通过学习本课程，您将掌握有限元分析中载荷建模的精髓，为您解决复杂的真实世界工程问题奠定坚实的理论与实践基础。让我们首先进入第一章，深入探索其背后的核心原理与机制。

## 原理与机制

在[有限元分析](@entry_id:138109)的框架内，外部作用力通过外力[虚功](@entry_id:176403)项被引入到系统的控制方程中。这些作用力可以是集中力，也可以是[分布](@entry_id:182848)在构件体积、表面或边线上的载荷。本章旨在系统性地阐述在有限元方法中对[分布](@entry_id:182848)式载荷和[体力](@entry_id:174230)进行建[模的基](@entry_id:156416)本原理与核心机制。我们将从[虚功原理](@entry_id:138749)出发，建立各类[分布](@entry_id:182848)式载荷的数学表述，随后深入探讨其在离散化过程中的处理方法，即如何将连续的载荷[分布](@entry_id:182848)转化为等效的节点力。最后，我们将讨论一些高级主题，包括惯性力、[非线性](@entry_id:637147)分析中的追随力以及确保计算精度的[数值积分](@entry_id:136578)问题。

### [分布](@entry_id:182848)式载荷与虚功原理

[有限元法](@entry_id:749389)的理论基础——[虚功原理](@entry_id:138749)，为处理各类外力提供了统一的框架。对于一个处于准静态平衡的连续体，其外力[虚功](@entry_id:176403) $\delta W_{\text{ext}}$ 等于内力[虚功](@entry_id:176403) $\delta W_{\text{int}}$。外力[虚功](@entry_id:176403)是所有外部作用力在任意容许的[虚位移](@entry_id:168781) $\delta\boldsymbol{u}$ 上所做的功。根据载荷作用的几何维度，我们可以将其分为三类 [@problem_id:2580294]：

1.  **体力 (Body Forces)**：作用于整个构件体积 $\Omega$ 的力，如重力、[惯性力](@entry_id:169104)或电磁力。体力通常用单位体积的力密度 $\boldsymbol{b}(\boldsymbol{x})$ 来描述，其单位为 $\text{N/m}^3$。它对[虚功](@entry_id:176403)的贡献是一个[体积分](@entry_id:171119)：
    $$
    \delta W_{\text{body}} = \int_{\Omega} \boldsymbol{b} \cdot \delta\boldsymbol{u} \, dV
    $$

2.  **面力 (Surface Tractions)**：作用于构件一部分表面 $\Gamma_t$ 的力，如压力、[摩擦力](@entry_id:171772)或[接触力](@entry_id:165079)。面力通常用单位面积的力密度 $\boldsymbol{t}(\boldsymbol{x})$ 来描述，即**牵[引力](@entry_id:175476) (traction)**，其单位为 $\text{N/m}^2$ (或 Pa)。它对[虚功](@entry_id:176403)的贡献是一个面积分：
    $$
    \delta W_{\text{surface}} = \int_{\Gamma_t} \boldsymbol{t} \cdot \delta\boldsymbol{u} \, dA
    $$

3.  **线载荷 (Line Loads)**：作用于构件边界上一条曲线 $\Lambda$ 上的力，常见于壳或板的边缘。线载荷用单位长度的力密度 $\boldsymbol{l}(\boldsymbol{x})$ 描述，其单位为 $\text{N/m}$。它对[虚功](@entry_id:176403)的贡献是一个线积分：
    $$
    \delta W_{\text{line}} = \int_{\Lambda} \boldsymbol{l} \cdot \delta\boldsymbol{u} \, dL
    $$

因此，总的外力[虚功](@entry_id:176403)是上述各项之和：
$$
\delta W_{\text{ext}} = \int_{\Omega} \boldsymbol{b} \cdot \delta\boldsymbol{u} \, dV + \int_{\Gamma_t} \boldsymbol{t} \cdot \delta\boldsymbol{u} \, dA + \int_{\Lambda} \boldsymbol{l} \cdot \delta\boldsymbol{u} \, dL
$$

从[量纲分析](@entry_id:140259)的角度看，每个积分项都必须具有能量的单位（力乘以位移，即 $\text{N} \cdot \text{m}$ 或焦耳 J）。以[体力](@entry_id:174230)项为例，其被积函数的单位是 $(\text{N/m}^3) \cdot \text{m} = \text{N/m}^2$，再乘以体积微元 $dV$ 的单位 $\text{m}^3$，最终得到能量单位 $\text{N} \cdot \text{m}$。同样地，面力项的量纲为 $(\text{N/m}^2) \cdot \text{m} \cdot \text{m}^2 = \text{N} \cdot \text{m}$，线载荷项的量纲为 $(\text{N/m}) \cdot \text{m} \cdot \text{m} = \text{N} \cdot \text{m}$，这保证了整个[虚功](@entry_id:176403)表达式在物理上的一致性 [@problem_id:2580329]。

值得注意的是，[体力](@entry_id:174230)的定义存在两种通用约定 [@problem_id:2580294]。第一种是**单位体积力**，如上所述。第二种是**单位质量力**（或称比体力），单位为 $\text{N/kg}$ 或 $\text{m/s}^2$。重力就是一个典型的例子，其[体力](@entry_id:174230)场通常由重力加速度矢量 $\boldsymbol{g}$ 描述。在这种情况下，单位体积的体力需要乘以材料的质量密度 $\rho(\boldsymbol{x})$，[虚功](@entry_id:176403)项写作：
$$
\delta W_{\text{gravity}} = \int_{\Omega} (\rho \boldsymbol{g}) \cdot \delta\boldsymbol{u} \, dV
$$
在实际应用中，必须明确所使用的[体力](@entry_id:174230)定义约定，以确保模型的正确性。

### 牵[引力](@entry_id:175476)边界条件与数学框架

面力，即牵[引力](@entry_id:175476)，是[有限元分析](@entry_id:138109)中最常见的边界条件类型之一。根据**柯西应力定理 (Cauchy's Stress Theorem)**，作用在任意一个[法向量](@entry_id:264185)为 $\boldsymbol{n}$ 的微小表面上的牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}$，与该点内部的应力状态 $\boldsymbol{\sigma}$ 之间存在线性关系：
$$
\boldsymbol{t} = \boldsymbol{\sigma} \boldsymbol{n}
$$
这个关系是连接内部应[力场](@entry_id:147325)与外部边界载荷的桥梁。在边界的特定部分 $\Gamma_t$ 上，我们可以施加指定的牵[引力](@entry_id:175476) $\bar{\boldsymbol{t}}$ 作为**自然边界条件 (Neumann boundary condition)**，即 $\boldsymbol{\sigma}\boldsymbol{n} = \bar{\boldsymbol{t}}$。

在许多工程问题中，一个常见的简化是将表面载荷建模为纯法向压力，例如[流体静压](@entry_id:141627)。若一个标量压[力场](@entry_id:147325) $p(\boldsymbol{x})$ 作用于表面，我们通常可以将其表示为一个矢量牵[引力](@entry_id:175476) $\bar{\boldsymbol{t}} = p\boldsymbol{n}$。然而，必须谨慎处理其符号约定 [@problem_id:2580290]。通常，压力被定义为压缩性（compressive）的，即它将物体推向其内部。如果 $\boldsymbol{n}$ 是指向域外的[单位法向量](@entry_id:178851)，那么一个大小为 $p$（$p > 0$）的压缩压力所对应的牵[引力](@entry_id:175476)矢量应为 $\bar{\boldsymbol{t}} = -p\boldsymbol{n}$。因此，$\bar{\boldsymbol{t}} = p\boldsymbol{n}$ 的表达式仅在 $p$ 被定义为拉伸性（tensile）载荷（即正值表示向外拉）时才成立。这种纯法向载荷的建模选择，无论[曲面](@entry_id:267450)是平坦还是弯曲，都是有效的，它定义了一种跟随当前法向的**追随力 (follower force)**。

从更严格的数学角度来看，为了保证[弱形式](@entry_id:142897)的良定性（well-posedness），我们需要对求[解空间](@entry_id:200470)和载荷数据施加一定的正则性要求 [@problem_id:2580322]。在小应变弹性理论中，位移场 $\boldsymbol{u}$ 通常被假定属于**索博列夫空间 (Sobolev space)** $H^1(\Omega)$，这意味着位移本身及其一阶导数都是平方可积的。根据**[迹定理](@entry_id:203967) (Trace Theorem)**，对于具有**利普希茨 (Lipschitz)** 连续边界的区域，定义在 $\Omega$ 上的 $H^1$ 函数在边界 $\partial\Omega$ 上的“迹”（即边界值）属于一个分数阶索博列夫空间 $H^{1/2}(\partial\Omega)$。

为了使外力[虚功](@entry_id:176403)泛函 $\ell(\boldsymbol{v}) = \int_{\Gamma_t} \boldsymbol{t} \cdot \boldsymbol{v} \, dA$ 对于所有[检验函数](@entry_id:166589) $\boldsymbol{v} \in H^1(\Omega)$ 都是一个[连续线性泛函](@entry_id:262913)，被积函数 $\boldsymbol{t}$ 必须属于[迹空间](@entry_id:756085) $H^{1/2}(\Gamma_t)$ 的**对偶空间 (dual space)**，即 $H^{-1/2}(\Gamma_t)$。这意味着，从数学上讲，牵[引力](@entry_id:175476) $\boldsymbol{t}$ 可以是比[平方可积函数](@entry_id:200316)更广义的[分布](@entry_id:182848)。此时，边界积分应被理解为对偶[内积](@entry_id:158127)：
$$
\int_{\Gamma_t} \boldsymbol{t} \cdot \boldsymbol{v} \, dA \equiv \langle \boldsymbol{t}, \gamma\boldsymbol{v} \rangle_{H^{-1/2}(\Gamma_t), H^{1/2}(\Gamma_t)}
$$
其中 $\gamma$ 是[迹算子](@entry_id:183665)。这一理论框架为处理包括集中力在内的奇异载荷提供了坚实的基础。

在处理[大变形](@entry_id:167243)问题时，区分**参考构型 (reference configuration)** 和**当前构型 (current configuration)** 上的载荷定义至关重要。如果一个压力 $p$ 是按单位参考面积定义的，那么在计算其对当前构型上的柯西牵[引力](@entry_id:175476)时，必须考虑[面积元](@entry_id:263205)的变化。这种转换通常通过**[南森公式](@entry_id:195566) (Nanson's formula)** 实现，它关联了参考构型和当前构型的法向量与[面积元](@entry_id:263205) [@problem_id:2580290]。

### 离散化与等效节点力

将连续的[分布](@entry_id:182848)式载荷应用于离散的有限元模型的关键机制，是计算**等效节点力 (consistent nodal forces)**。这个过程通过将连续的[虚功](@entry_id:176403)表达式离散化来实现。

在一个单元内部，位移场 $\boldsymbol{u}$ 和[虚位移](@entry_id:168781)场 $\delta\boldsymbol{u}$ 都通过形函数 $\mathbf{N}$ 从节点位移 $\mathbf{d}$ 和节点[虚位移](@entry_id:168781) $\delta\mathbf{d}$ 插值得到：
$$
\boldsymbol{u}(\boldsymbol{x}) = \mathbf{N}(\boldsymbol{x})\mathbf{d} \quad \text{and} \quad \delta\boldsymbol{u}(\boldsymbol{x}) = \mathbf{N}(\boldsymbol{x})\delta\mathbf{d}
$$
将此离散表达式代入外力[虚功](@entry_id:176403)的积分形式中，例如体力项：
$$
\delta W_{\text{body}}^{(e)} = \int_{\Omega_e} \delta\boldsymbol{u}^T \boldsymbol{b} \, dV = \int_{\Omega_e} (\mathbf{N}\delta\mathbf{d})^T \boldsymbol{b} \, dV = \delta\mathbf{d}^T \int_{\Omega_e} \mathbf{N}^T \boldsymbol{b} \, dV
$$
同时，[虚功](@entry_id:176403)也可以直接表示为节点力与节点[虚位移](@entry_id:168781)的[点积](@entry_id:149019) $\delta W_{\text{body}}^{(e)} = \delta\mathbf{d}^T \mathbf{f}_e$。由于 $\delta\mathbf{d}$ 的任意性，我们得到单元等效节点[体力](@entry_id:174230)向量的定义：
$$
\mathbf{f}_e = \int_{\Omega_e} \mathbf{N}^T(\boldsymbol{x}) \boldsymbol{b}(\boldsymbol{x}) \, dV
$$
这个向量 $\mathbf{f}_e$ 将连续的[体力](@entry_id:174230)[分布](@entry_id:182848)等效地分配到单元的各个节点上，保证了在能量（功）的意义上与原始[分布](@entry_id:182848)等价。

为了在计算机上实现这一积分，我们通常需要将积分从物理单元域 $\Omega_e$ 变换到规则的**父单元域 (parent element)** $\hat{\Omega}$（例如，对于四边形是 $[-1, 1]^2$）上。这一变换基于**等参元 (isoparametric element)** 的思想，即几何坐标 $\boldsymbol{x}$ 也由相同的形函数插值得到：
$$
\boldsymbol{x}(\boldsymbol{\xi}) = \sum_a N_a(\boldsymbol{\xi})\boldsymbol{x}_a
$$
其中 $\boldsymbol{\xi}$ 是父单元的[局部坐标](@entry_id:181200)。根据多变量微[积分的[变量替](@entry_id:178219)换](@entry_id:141386)法则，体积微元 $dV$ 可以通过**[雅可比行列式](@entry_id:137120) (Jacobian determinant)** $J(\boldsymbol{\xi}) = \det(\frac{\partial\boldsymbol{x}}{\partial\boldsymbol{\xi}})$ 进行变换：$dV = J(\boldsymbol{\xi}) d\hat{V}$。

因此，等效节点体力的计算公式变换为在父单元上的积分 [@problem_id:2580327]：
$$
\mathbf{f}_e = \int_{\hat{\Omega}} \mathbf{N}^T(\boldsymbol{\xi}) \boldsymbol{b}(\boldsymbol{x}(\boldsymbol{\xi})) J(\boldsymbol{\xi}) \, d\hat{V}
$$
对于作用在单元表面 $\Gamma_e$ 上的牵[引力](@entry_id:175476) $\boldsymbol{t}$，推导过程完全类似 [@problem_id:2580323]。等效[节点面](@entry_id:752526)力向量为：
$$
\mathbf{f}_e = \int_{\Gamma_e} \mathbf{N}^T(\boldsymbol{x}) \boldsymbol{t}(\boldsymbol{x}) \, dA
$$
通过[参数化](@entry_id:272587) $\boldsymbol{x}(\xi_1, \xi_2)$ 将物理表面 $\Gamma_e$ 映射到父表面 $\hat{\Gamma}$，面积微元变换为 $dA = \|\frac{\partial\boldsymbol{x}}{\partial\xi_1} \times \frac{\partial\boldsymbol{x}}{\partial\xi_2}\| d\hat{A}$，其中 $\|\frac{\partial\boldsymbol{x}}{\partial\xi_1} \times \frac{\partial\boldsymbol{x}}{\partial\xi_2}\|$ 是表面雅可比行列式。最终的计算公式为：
$$
\mathbf{f}_e = \int_{\hat{\Gamma}} \mathbf{N}^T(\boldsymbol{\xi}) \boldsymbol{t}(\boldsymbol{x}(\boldsymbol{\xi})) \left\|\frac{\partial\boldsymbol{x}}{\partial\xi_1} \times \frac{\partial\boldsymbol{x}}{\partial\xi_2}\right\| \, d\hat{A}
$$
在三维问题中，参数化 $\boldsymbol{\xi} = (\xi, \eta)$ 的顺序（例如，在叉乘中是 $\partial\boldsymbol{x}/\partial\xi \times \partial\boldsymbol{x}/\partial\eta$ 还是 $\partial\boldsymbol{x}/\partial\eta \times \partial\boldsymbol{x}/\partial\xi$）决定了计算出的[法向量](@entry_id:264185)的方向。根据右手法则，这两种顺序会得到方向相反的法向量。为了正确施加载荷，必须确保所使用的法向量指向正确的方向（通常是域外），否则将导致节点力的符号错误。

### 高级加载概念

#### 集中力作为极限情况

在工程实践中，我们经常使用**集中力 (concentrated force)** 或点载荷的概念。在数学上，一个严格的集中力会导致[应力奇异性](@entry_id:166362)。在有限元框架下，施加在节点上的力可以被严谨地理解为一个[分布](@entry_id:182848)式载荷序列的**弱极限 (weak limit)** [@problem_id:2580331]。

考虑一个作用在边界小块区域 $\Gamma_\varepsilon$ 上的牵[引力](@entry_id:175476) $\boldsymbol{t}_\varepsilon$，其支撑集 $\Gamma_\varepsilon$ 的直径随 $\varepsilon \to 0$ 而趋于零，并收缩至一点 $\boldsymbol{x}_0$。同时，该载荷的总[合力](@entry_id:163825)（resultant）保持为一个固定的非零向量 $\boldsymbol{P}$，即 $\int_{\Gamma} \boldsymbol{t}_\varepsilon \, dA = \boldsymbol{P}$。这样的一个载荷序列在测度意义上[弱*收敛](@entry_id:196227)于一个以 $\boldsymbol{P}$ 为权重的**狄拉克 delta [分布](@entry_id:182848) (Dirac delta distribution)**，记为 $\boldsymbol{P}\delta_{\boldsymbol{x}_0}$。它对任意连续的[检验函数](@entry_id:166589)（[虚位移](@entry_id:168781)）$\boldsymbol{\varphi}$ 的作用定义为：
$$
\lim_{\varepsilon \to 0^+} \int_{\Gamma} \boldsymbol{t}_\varepsilon \cdot \boldsymbol{\varphi} \, dA = \boldsymbol{P} \cdot \boldsymbol{\varphi}(\boldsymbol{x}_0)
$$
这个极限恰恰是大小为 $\boldsymbol{P}$ 的集中力作用在点 $\boldsymbol{x}_0$ 上所做的[虚功](@entry_id:176403)。

将这一概念应用于有限元等效节点力的计算，节点 $i$ 上的等效力为 $\boldsymbol{f}_i^{(\varepsilon)} = \int_{\Gamma} N_i \boldsymbol{t}_\varepsilon \, dA$。取极限后，我们得到：
$$
\lim_{\varepsilon \to 0^+} \boldsymbol{f}_i^{(\varepsilon)} = \boldsymbol{P} N_i(\boldsymbol{x}_0)
$$
这个重要的结果揭示了集中力如何分配到节点上：
-   如果集中力作用点 $\boldsymbol{x}_0$ 恰好是节点 $j$ 的位置，由于[拉格朗日形函数](@entry_id:635448)具有 $N_i(\boldsymbol{x}_j) = \delta_{ij}$ 的性质，我们得到 $\lim \boldsymbol{f}_j^{(\varepsilon)} = \boldsymbol{P}$，而所有其他节点上的力均为零。这与直观的节点力施加方式完全一致。
-   如果 $\boldsymbol{x}_0$ 位于单元 $e$ 的内部，那么只有属于该单元的节点的形函数值 $N_i(\boldsymbol{x}_0)$ 非零。因此，该集中力将根据形函数在 $\boldsymbol{x}_0$ 处的值[按比例分配](@entry_id:634725)到单元的各个节点上。由于形函数具有[单位分解](@entry_id:150115)性（$\sum_i N_i(\boldsymbol{x}_0) = 1$），总的作用力得到保持。

#### [惯性力](@entry_id:169104)与等效质量矩阵

在动力学分析中，根据**[达朗贝尔原理](@entry_id:166612) (d'Alembert's principle)**，我们可以将惯性项 $-\rho\ddot{\boldsymbol{u}}$ 视为一种作用于构件上的[体力](@entry_id:174230)。这种“惯性[体力](@entry_id:174230)”对[虚功](@entry_id:176403)的贡献为 [@problem_id:2580272]：
$$
\delta W_{\text{inertial}} = \int_{\Omega} \delta\boldsymbol{u}^T (-\rho \ddot{\boldsymbol{u}}) \, dV
$$
采用与处理静力[体力](@entry_id:174230)完全相同的离散化和[等参变换](@entry_id:750863)方法，将 $\delta\boldsymbol{u} = \mathbf{N}\delta\mathbf{d}$ 和 $\ddot{\boldsymbol{u}} = \mathbf{N}\ddot{\mathbf{d}}$ 代入上式，我们得到：
$$
\delta W_{\text{inertial}}^{(e)} = \delta\mathbf{d}^T \left( -\int_{\Omega_e} \rho \mathbf{N}^T \mathbf{N} \, dV \right) \ddot{\mathbf{d}}
$$
括号中的矩阵项被称为**等效[质量矩阵](@entry_id:177093) (consistent mass matrix)**：
$$
\mathbf{M}^e = \int_{\Omega_e} \rho \mathbf{N}^T \mathbf{N} \, dV
$$
这个矩阵将[连续分布](@entry_id:264735)的质量以能量一致的方式分配到单元节点上。与对角化的**[集中质量矩阵](@entry_id:173011) (lumped mass matrix)** 不同，等效[质量矩阵](@entry_id:177093)通常是满秩的，它耦合了单元内所有节点的加速度，能够更精确地反映结构的动力学特性，尤其是在高频[振动分析](@entry_id:146266)中。最终，系统的[半离散运动方程](@entry_id:754679)形如 $\mathbf{M}\ddot{\mathbf{d}} + \mathbf{K}\mathbf{d} = \mathbf{F}_{\text{ext}}$。

#### [非线性](@entry_id:637147)分析中的构型相关载荷

在[几何非线性](@entry_id:169896)分析中，必须区分载荷是否依赖于物体的构型 [@problem_id:2580342]。

-   **保守载荷 (Dead Loads)**：这类载荷的方向和大小在变形过程中保持不变，它们被定义在未变形的参考构型上。例如，一个固定方向和大小的重[力场](@entry_id:147325)。其外力[势能](@entry_id:748988) $W_{\text{ext}}(\boldsymbol{u}) = \int_{\Omega_0} \boldsymbol{B}_0 \cdot \boldsymbol{u} \, dV_0$ 是位移 $\boldsymbol{u}$ 的线性函数。在[求解非线性方程](@entry_id:177343)的[牛顿-拉弗森](@entry_id:177436)迭代过程中，这类载荷对**[切线刚度矩阵](@entry_id:170852) (tangent stiffness matrix)** 没有贡献，即它们不产生**[几何刚度](@entry_id:172820) (geometric stiffness)**。

-   **追随载荷 (Follower Loads)**：这类载荷的大小或方向会随着构型的变化而改变。一个典型的例子是作用在变形表面上的压力，其方向始终垂直于当前的表面。这种载荷的外力[势能](@entry_id:748988)（如果存在）是位移 $\boldsymbol{u}$ 的[非线性](@entry_id:637147)函数。例如，对于施加在封闭体积上的均匀压力 $p$，其外力[势能](@entry_id:748988)可以表示为 $W_{\text{ext}}(\boldsymbol{u}) = pV(\boldsymbol{u})$，其中 $V(\boldsymbol{u})$ 是当前构型的体积，它是位移的[非线性](@entry_id:637147)函数。当对弱形式进行线性化以得到[切线刚度矩阵](@entry_id:170852)时，这种[非线性](@entry_id:637147)[势能](@entry_id:748988)会产生一个附加的刚度项，称为**载荷[刚度矩阵](@entry_id:178659) (load stiffness matrix)**，它是[几何刚度矩阵](@entry_id:162967)的一部分。对于可从[势能](@entry_id:748988)导出的保守追随载荷（如上述压力），载荷刚度矩阵是对称的。然而，对于非保守的追随载荷（如切向追随力），其贡献可能导致总的[切线刚度矩阵](@entry_id:170852)变为非对称，这对求解器的选择有重要影响。

### [数值积分](@entry_id:136578)与精度

在实践中，变换到父单元上的等效节点力积分通常无法获得解析解，必须通过**[数值积分](@entry_id:136578) (numerical quadrature)**（最常用的是**[高斯-勒让德求积](@entry_id:138201) (Gauss-Legendre quadrature)**）来计算。选择正确的积分阶次对于保证[载荷向量](@entry_id:635284)的准确性至关重要。

一条 $n$ 点[高斯求积法](@entry_id:146011)则在一维上可以精确积分最高 $2n-1$ 次的多项式。对于在父单元上的积分 $f_i = \int_{-1}^1\int_{-1}^1 I(\xi, \eta) \, d\xi d\eta$，为了保证精确积分，我们需要确定被积函数 $I(\xi, \eta) = N_i(\xi,\eta)\, b(x(\xi,\eta),y(\xi,\eta))\, J(\xi,\eta)$ 在每个[局部坐标](@entry_id:181200)方向上的最高多项式次数，并选择足够高的积分点数 $n$ [@problem_id:2580316]。

以一个 $Q_2$（双二次）单元为例，其形函数 $N_i$ 是 $\xi$ 和 $\eta$ 的二次多项式。[几何映射](@entry_id:749852) $\boldsymbol{x}(\boldsymbol{\xi})$ 也是二次的。因此，雅可比行列式 $J$ 的次数为二次。如果体力 $b(x,y)$ 是物理坐标的 $k$ 次多项式，那么[复合函数](@entry_id:147347) $b(\boldsymbol{x}(\boldsymbol{\xi}))$ 的次数为 $2k$。因此，被积函数 $I(\xi, \eta)$ 的总次数为 $2 + 2k + 2 = 2k+4$。为了精确积分，需要满足 $2n-1 \ge 2k+4$，解得 $n \ge k+2.5$。因此，所需的最小积分点数为 $n=k+3$。

**积分不足 (under-integration)**，即使用过低的积分阶次，会导致[载荷向量](@entry_id:635284)计算不准确。这不仅会引入误差，还可能破坏基本的物理守恒律。例如，积分不足可能导致计算出的等效节点力总和不等于原始[分布载荷](@entry_id:162746)的总合力 [@problem_id:2580318]。考虑一个二次曲边杆单元，其几何由二次形函数描述，承受线性变化的牵[引力](@entry_id:175476) $p(x) = p_0 + p_1x$。如果使用单点高斯积分（对于线性单元是精确的，但对于[曲边单元](@entry_id:748117)则不足），计算出的总[合力](@entry_id:163825) $R^{(1)}$ 与精确[合力](@entry_id:163825) $R$ 之间的误差 $\Delta R = R^{(1)} - R$ 可以被精确地计算出来。分析表明，该误差正比于载荷的梯度 $p_1$ 和单元的曲率（由中间节点偏离弦中点的程度度量）。只有当载荷为常数（$p_1=0$）或单元为直线（无曲率）时，单[点积](@entry_id:149019)分才是精确的。这个例子生动地说明了，为了准确地表示载荷，[数值积分](@entry_id:136578)方案必须有足够的能力来精确积分（至少）低阶多项式载荷场与几何雅可比的乘积。这与保证[单元刚度矩阵](@entry_id:139369)精度的要求是并行且同等重要的。