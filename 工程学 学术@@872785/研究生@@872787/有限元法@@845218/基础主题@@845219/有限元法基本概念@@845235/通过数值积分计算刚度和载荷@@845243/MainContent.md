## 引言
在有限元分析（FEA）的广阔领域中，[单元刚度矩阵](@entry_id:139369)和[载荷向量](@entry_id:635284)的精确计算是构建和求解任何问题的基石。这些关键组件源于控制方程的积分形式，代表了单元内部的物理行为和外部载荷的贡献。然而，一个根本性的挑战在于，工程结构中的单元几何形状往往是任意且复杂的，直接在这些物理域上进行解析积分几乎是不可能的。这一知识鸿沟催生了对一种既通用又高效的积分策略的迫切需求。

本文旨在系统性地解决这一核心问题，全面阐述通过[数值积分](@entry_id:136578)来评估刚度和载荷的完整方法。读者将通过本文的学习，掌握从理论到实践的整个流程。在“原理与机制”一章中，我们将奠定理论基础，深入探讨如何通过[等参映射](@entry_id:173239)将复杂的物理单元转换为简单的[参考单元](@entry_id:168425)，并介绍[高斯求积](@entry_id:146011)这一强大的数值工具来高效近似积分。随后的“应用与跨学科联系”一章将理论付诸实践，展示数值积分在处理空间变化的材料属性、结构稳定性分析、[剪切自锁](@entry_id:164115)现象以及复杂的[弹塑性](@entry_id:193198)[非线性](@entry_id:637147)问题等前沿应用中的关键作用。最后，在“动手实践”部分，我们提供了一系列精心设计的编程练习，帮助读者将理论知识转化为解决实际问题的能力，从而真正精通这一有限元分析的核心技术。

## 原理与机制

在[有限元分析](@entry_id:138109)中，[单元刚度矩阵](@entry_id:139369)和[载荷向量](@entry_id:635284)的计算是核心步骤，它们源于控制方程的弱形式或变分原理，最终表现为在每个单元域上进行的积分。然而，物理单元的几何形状通常是任意的，直接在这些域上进行解析积分几乎是不可能的。为了克服这一挑战，有限元方法采用了一种强大而系统的策略：将积分计算从复杂的物理域转换到一个简单的、[标准化](@entry_id:637219)的“父”单元或“参考”单元域上，然后在此标准域上使用数值方法近似计算积分。本章将深入探讨这一过程的原理与机制，从坐标变换的基础到高斯[数值积分的应用](@entry_id:633943)，再到刚度和载荷评估中的实际考量。

### 从物理单元到参考单元的映射

有限元方法的核心思想之一是 **[等参映射](@entry_id:173239) (isoparametric mapping)**。在这种方法中，单元的几何形状和单元内的场变量（如位移）使用相同的形函数进行插值。考虑一个位于物理[坐标系](@entry_id:156346) $\boldsymbol{x}$ 中的单元 $\Omega_e$。我们可以定义一个简单的[参考单元](@entry_id:168425) $\hat{\Omega}$，其位于参数[坐标系](@entry_id:156346) $\hat{\boldsymbol{\xi}}$ 中。例如，对于二维[四边形单元](@entry_id:176937)，参考单元通常是边长为2的正方形，其坐标 $\hat{\boldsymbol{\xi}} = (\xi, \eta)$ 满足 $-1 \le \xi \le 1$ 和 $-1 \le \eta \le 1$。

[等参映射](@entry_id:173239)建立了物理坐标 $\boldsymbol{x}$ 和参考坐标 $\hat{\boldsymbol{\xi}}$ 之间的关系：
$$
\boldsymbol{x}(\hat{\boldsymbol{\xi}}) = \sum_{a=1}^{n_{\text{en}}} N_a(\hat{\boldsymbol{\xi}}) \boldsymbol{x}_a
$$
其中，$n_{\text{en}}$ 是单元的节点数，$N_a(\hat{\boldsymbol{\xi}})$ 是在参考[坐标系](@entry_id:156346)中定义的节点 $a$ 的形函数，$\boldsymbol{x}_a$ 是节点 $a$ 在物理空间中的[坐标向量](@entry_id:153319)。

在进行[积分变换](@entry_id:186209)时，一个关键量是 **[雅可比矩阵](@entry_id:264467) (Jacobian matrix)** $\boldsymbol{J}$，它描述了从参考坐标到物理坐标的[局部线性](@entry_id:266981)变换：
$$
\boldsymbol{J}(\hat{\boldsymbol{\xi}}) = \frac{\partial \boldsymbol{x}}{\partial \hat{\boldsymbol{\xi}}}
$$
对于二维情况，$\boldsymbol{J}$ 是一个 $2 \times 2$ 矩阵：
$$
\boldsymbol{J} = \begin{pmatrix} \frac{\partial x}{\partial \xi} & \frac{\partial x}{\partial \eta} \\ \frac{\partial y}{\partial \xi} & \frac{\partial y}{\partial \eta} \end{pmatrix}
$$
根据多元微[积分中的变量替换](@entry_id:140343)法则，物理域中的[微分](@entry_id:158718)[面积元](@entry_id:263205) $\mathrm{d}\Omega$ 与参考域中的[微分](@entry_id:158718)面积元 $\mathrm{d}\hat{\Omega}$ 之间的关系由雅可比矩阵的[行列式](@entry_id:142978) $\det \boldsymbol{J}$ 给出：
$$
\mathrm{d}\Omega = \det(\boldsymbol{J}(\hat{\boldsymbol{\xi}})) \mathrm{d}\hat{\Omega}
$$
因此，任何在物理单元 $\Omega_e$ 上的积分都可以转换为在[参考单元](@entry_id:168425) $\hat{\Omega}$ 上的积分：
$$
\int_{\Omega_e} f(\boldsymbol{x}) \mathrm{d}\Omega = \int_{\hat{\Omega}} f(\boldsymbol{x}(\hat{\boldsymbol{\xi}})) \det(\boldsymbol{J}(\hat{\boldsymbol{\xi}})) \mathrm{d}\hat{\Omega}
$$
这一变换是后续所有计算的基石 [@problem_id:2599423]。

### 高斯[数值积分](@entry_id:136578)

即使在转换到[参考单元](@entry_id:168425)后，被积函数通常仍然非常复杂（通常是多项式或有理函数），难以解析求解。因此，我们采用 **[数值积分](@entry_id:136578) (numerical quadrature)**，特别是 **[高斯积分](@entry_id:187139) (Gaussian quadrature)** 来近似这些积分。

高斯-勒让德 (Gauss-Legendre) 法则是定义在区间 $[-1, 1]$ 上的一种高效数值积分格式。一个 $n$ 点的高斯-勒让德积分法则用以下求和形式来近似积分：
$$
\int_{-1}^{1} g(\xi) \mathrm{d}\xi \approx \sum_{i=1}^{n} w_i g(\xi_i)
$$
其中，$\xi_i$ 是 **积分点 (integration points)** 或 **[高斯点](@entry_id:170251) (Gauss points)**，$w_i$ 是相应的 **权重 (weights)**。高斯积分的卓越之处在于其积分点和权重的选择方式。对于 $n$ 点法则，积分点 $\xi_i$ 被选为 $n$ 阶[勒让德多项式](@entry_id:141510) $P_n(\xi)$ 的 $n$ 个根。这些根都位于开区间 $(-1, 1)$ 内。通过这样的选择，并相应地计算出 **恒为正的权重** $w_i$，该 $n$ [点积](@entry_id:149019)分法则能够精确地积分所有次数最高为 $2n-1$ 的多项式。这是具有 $n$ 个积分点的求积公式所能达到的最高精度 [@problem_id:2599413]。

一个重要的性质是，所有[高斯点](@entry_id:170251)的权重之和等于积分区间的长度。对于 $[-1, 1]$ 区间，我们可以通过对[常数函数](@entry_id:152060) $g(\xi)=1$ (一个0次多项式) 应用该法则来验证：
$$
\int_{-1}^{1} 1 \mathrm{d}\xi = 2
$$
由于任何 $n \ge 1$ 的高斯法则都能精确积分0次多项式，我们必须有：
$$
\sum_{i=1}^{n} w_i \cdot 1 = \sum_{i=1}^{n} w_i = 2
$$
这个性质在代码实现中可作为一个简单的校验 [@problem_id:2599413]。对于二维或三维的[参考单元](@entry_id:168425)（如正方形或立方体），通常使用一维高斯法则的 **张量积 (tensor product)** 来构造[高维积分](@entry_id:143557)法则。

### [单元刚度矩阵](@entry_id:139369)的计算

[单元刚度矩阵](@entry_id:139369) $\boldsymbol{K}_e$ 的各项通常包含形函数梯度的乘积。例如，在线性弹性问题中，其一般形式为：
$$
\boldsymbol{K}_e = \int_{\Omega_e} \boldsymbol{B}(\boldsymbol{x})^{\mathsf{T}} \boldsymbol{D}(\boldsymbol{x}) \boldsymbol{B}(\boldsymbol{x}) \mathrm{d}\Omega
$$
其中 $\boldsymbol{B}$ 是[应变-位移矩阵](@entry_id:163451)，$\boldsymbol{D}$ 是[本构矩阵](@entry_id:164908)。$\boldsymbol{B}$ 矩阵的项包含形函数对物理坐标的导数，如 $\partial N_a / \partial x$。这些导数必须通过链式法则和[雅可比矩阵](@entry_id:264467)的逆来计算：
$$
\begin{Bmatrix} \frac{\partial N_a}{\partial x} \\ \frac{\partial N_a}{\partial y} \end{Bmatrix} = \boldsymbol{J}^{-\mathsf{T}} \begin{Bmatrix} \frac{\partial N_a}{\partial \xi} \\ \frac{\partial N_a}{\partial \eta} \end{Bmatrix}
$$
注意，这里的梯度变换关系是 $\nabla_{\boldsymbol{x}} = \boldsymbol{J}^{-\mathsf{T}} \nabla_{\hat{\boldsymbol{\xi}}}$，其中 $\boldsymbol{J}^{-\mathsf{T}} = (\boldsymbol{J}^{-1})^{\mathsf{T}} = (\boldsymbol{J}^{\mathsf{T}})^{-1}$ [@problem_id:2599442]。

将所有项都变换到参考[坐标系](@entry_id:156346)下，[刚度矩阵](@entry_id:178659)的积分变为：
$$
\boldsymbol{K}_e = \int_{\hat{\Omega}} \boldsymbol{B}(\hat{\boldsymbol{\xi}})^{\mathsf{T}} \boldsymbol{D}(\boldsymbol{x}(\hat{\boldsymbol{\xi}})) \boldsymbol{B}(\hat{\boldsymbol{\xi}}) \det(\boldsymbol{J}(\hat{\boldsymbol{\xi}})) \mathrm{d}\hat{\Omega}
$$
然后应用[高斯积分](@entry_id:187139)进行数值计算：
$$
\boldsymbol{K}_e \approx \sum_{i=1}^{n_q} w_i \boldsymbol{B}(\hat{\boldsymbol{\xi}}_i)^{\mathsf{T}} \boldsymbol{D}(\boldsymbol{x}(\hat{\boldsymbol{\xi}}_i)) \boldsymbol{B}(\hat{\boldsymbol{\xi}}_i) \det(\boldsymbol{J}(\hat{\boldsymbol{\xi}}_i))
$$
这里 $n_q$ 是[高斯点](@entry_id:170251)的总数。值得注意的是，如果材料属性 $\boldsymbol{D}$ 在空间上变化，必须在每个[高斯点](@entry_id:170251)对应的 **物理位置** $\boldsymbol{x}(\hat{\boldsymbol{\xi}}_i)$ 上进行取值，而不是直接使用参考坐标 $\hat{\boldsymbol{\xi}}_i$ [@problem_id:2599423]。

#### 积分精度的确定

选择所需的最少[高斯点](@entry_id:170251)数 $n$ (即确定 **积分阶次**)，取决于被积函数在参考[坐标系](@entry_id:156346)下的多项式次数。我们的目标是选择最小的 $n$ 使得 $2n-1$ 大于或等于被积函数的最高次数。

- **一维线性杆单元示例**：考虑一个两节点的线性杆单元。形函数 $N_a(\xi)$ 是 $\xi$ 的一次多项式。其导数 $dN_a/d\xi$ 是常数。对于一个直杆，[几何映射](@entry_id:749852)是线性的，因此雅可比行列式 $J$ 也是常数。刚度积分中的被积函数 $\left(\frac{dN}{dx}\right)^2 J = \left(\frac{1}{J}\frac{dN}{d\xi}\right)^2 J$ 是一个常数，即0次多项式。为了精确积分0次多项式，我们需要 $2n-1 \ge 0$，这意味着 $n \ge 1/2$。因此，最少需要 $n=1$ 个[高斯点](@entry_id:170251) [@problem_id:2599472]。

- **二维[四边形单元](@entry_id:176937)示例**：对于一个四节点双线性[四边形单元](@entry_id:176937)，形函数 $N_a(\xi, \eta)$ 是 $\xi$ 和 $\eta$ 的[双线性](@entry_id:146819)函数（例如，包含 $1, \xi, \eta, \xi\eta$ 项）。其导数，如 $\partial N_a/\partial \xi$，是 $\eta$ 的一次多项式。
    - **[仿射映射](@entry_id:746332) (Affine Mapping)**：如果单元是一个平行四边形（包括矩形），则[几何映射](@entry_id:749852)是仿射的，[雅可比矩阵](@entry_id:264467) $\boldsymbol{J}$ 及其[行列式](@entry_id:142978) $\det \boldsymbol{J}$ 都是常数。$\boldsymbol{B}$ 矩阵的项是 $\xi$ 和 $\eta$ 的一次多项式。那么，刚度积分的被积函数 $\boldsymbol{B}^{\mathsf{T}}\boldsymbol{D}\boldsymbol{B}$ 的各项将是 $\xi$ 和 $\eta$ 的二次多项式。为了精确积分一个二次多项式，我们需要 $2n-1 \ge 2$，即 $n \ge 1.5$。因此，在每个方向上最少需要 $n=2$ 个[高斯点](@entry_id:170251)，即一个 $2 \times 2$ 的积分方案 [@problem_id:2599482] [@problem_id:2599442]。
    - **非[仿射映射](@entry_id:746332) (Non-affine Mapping)**：如果单元是任意扭曲的四边形，$\boldsymbol{J}$ 不再是常数，而是 $\xi, \eta$ 的函数。$\det \boldsymbol{J}$ 通常是线性的。更重要的是，$\boldsymbol{B}$ 矩阵中包含 $\boldsymbol{J}^{-1}$，这使得刚度积分的被积函数变成了 **有理函数**（分子和分母都是多项式），而不是多项式。高斯积分无法精确积分有理函数。因此，对于扭曲的等参元，数值积分本身就会引入近似误差，无论使用多少积分点都无法“精确”积分 [@problem_id:2599442] [@problem_id:2599485]。

### 一致性[载荷向量](@entry_id:635284)的计算

与外力（如[体力](@entry_id:174230)、面力）等效的节点力向量，即 **一致性[载荷向量](@entry_id:635284) (consistent load vector)**，也通过在弱形式中对[虚功](@entry_id:176403)项进行积分来获得。

#### [体力](@entry_id:174230)载荷

对于体力 $\boldsymbol{b}$，其[虚功](@entry_id:176403)项为 $\int_{\Omega_e} \delta \boldsymbol{u}^{\mathsf{T}} \boldsymbol{b} \mathrm{d}\Omega$。这导出了一致性节点力向量 $\boldsymbol{f}_e$：
$$
\boldsymbol{f}_e = \int_{\Omega_e} \boldsymbol{N}^{\mathsf{T}} \boldsymbol{b} \mathrm{d}\Omega = \int_{\hat{\Omega}} \boldsymbol{N}(\hat{\boldsymbol{\xi}})^{\mathsf{T}} \boldsymbol{b}(\boldsymbol{x}(\hat{\boldsymbol{\xi}})) \det(\boldsymbol{J}(\hat{\boldsymbol{\xi}})) \mathrm{d}\hat{\Omega}
$$
其中 $\boldsymbol{N}$ 是形函数矩阵。

- **线性[三角形单元](@entry_id:167871)示例**：对于一个三节点线性[三角形单元](@entry_id:167871)，形函数 $N_a$ 是线性的。如果体力 $\boldsymbol{b}$ 是常数，则被积函数 $N_a \det(\boldsymbol{J})$ 是线性的（因为 $\det(\boldsymbol{J})$ 对常应变三角形是常数）。已知对于三角形区域，位于其形心的一个单[点积](@entry_id:149019)分法则可以精确积分线性函数。因此，对于常数体力，使用[形心](@entry_id:265015)处的1[点积](@entry_id:149019)分法就能精确计算出一致性[载荷向量](@entry_id:635284) [@problem_id:2599448]。
- **双线性[四边形单元](@entry_id:176937)示例**：对于双线性[四边形单元](@entry_id:176937)和常数体力 $\boldsymbol{b}$，被积函数是 $\boldsymbol{N}(\xi, \eta) \det(\boldsymbol{J}(\xi, \eta))$。形函数 $\boldsymbol{N}$ 是[双线性](@entry_id:146819)的，对于一般映射 $\det(\boldsymbol{J})$ 是线性的。它们的乘积是 $\xi$ 和 $\eta$ 的二次多项式。因此，需要一个 $2 \times 2$ 的高斯积分方案才能精确计算 [@problem_id:2599442]。

#### [表面牵引力](@entry_id:169207)载荷

对于作用在单元边界 $\Gamma_e$ 上的[表面牵引力](@entry_id:169207) $\boldsymbol{t}$，一致性[载荷向量](@entry_id:635284)为：
$$
\boldsymbol{f}_e = \int_{\Gamma_e} \boldsymbol{N}^{\mathsf{T}} \boldsymbol{t} \mathrm{d}\Gamma
$$
计算这个边界积分也需要映射到[参考单元](@entry_id:168425)的边界上。例如，考虑作用在[四边形单元](@entry_id:176937)边2-3（对应参考单元的 $\xi=1, \eta \in [-1, 1]$ 边）上的均布压力 $p$。

1.  **映射边界**：物理边上的积分 $\int_{\Gamma_{23}} (\cdot) \mathrm{d}\Gamma$ 需转换为参考边上的积分 $\int_{-1}^{1} (\cdot) \mathrm{d}\eta$。
2.  **变换[微分](@entry_id:158718)[弧长](@entry_id:191173)**：[微分](@entry_id:158718)[弧长](@entry_id:191173) $\mathrm{d}\Gamma$ 通过一维[雅可比行列式](@entry_id:137120) $J_{1D}$ 与 $\mathrm{d}\eta$ 联系：$\mathrm{d}\Gamma = J_{1D} \mathrm{d}\eta = ||\partial \boldsymbol{x}/\partial \eta|| \mathrm{d}\eta$。对于直边，这是边长的一半。
3.  **变换[法向量](@entry_id:264185)**：物理边上的外法向量 $\boldsymbol{n}$ 也必须用节点坐标表示出来。
4.  **积分**：将形函数（在 $\xi=1$ 上取值）、变换后的[法向量](@entry_id:264185)和[弧长](@entry_id:191173)代入积分表达式，并在 $[-1, 1]$ 上用一维[高斯积分](@entry_id:187139)求解。对于线性边（即由两个节点定义的边），形函数在切向坐标 $\eta$ 上是线性的，因此2点[高斯积分](@entry_id:187139)足以精确计算均布压力产生的载荷 [@problem_id:2599415]。

### 实际应用中的高级主题

#### 几何有效性与[雅可比行列式](@entry_id:137120)

[雅可比行列式](@entry_id:137120) $\det \boldsymbol{J}$ 不仅是面积（或体积）的缩放因子，它还具有深刻的几何意义。$\det \boldsymbol{J} > 0$ 表示映射是保向的、非奇异的，即[参考单元](@entry_id:168425)中的一个小区域被映射为物理空间中一个“未翻转”的区域。

在数值积分中，我们仅在离散的[高斯点](@entry_id:170251)上计算 $\det \boldsymbol{J}$。
- 如果在所有[高斯点](@entry_id:170251)上都有 $\det \boldsymbol{J} > 0$，这保证了在这些点的局部邻域内映射是有效的。这是得到物理上有意义的[刚度矩阵](@entry_id:178659)的必要条件。然而，这并不能保证整个单元没有发生扭曲或翻转（可能在积分点之间发生）[@problem_id:2599485]。
- 如果在任何一个[高斯点](@entry_id:170251)上出现 $\det \boldsymbol{J} \le 0$，则[数值积分](@entry_id:136578)失效。$\det \boldsymbol{J} = 0$ 意味着映射在该点是奇异的（例如，一个区域被压成一条线），导致 $\boldsymbol{J}^{-1}$ 不存在。$\det \boldsymbol{J}  0$ 意味着局部发生了“翻转”，一个[右手坐标系](@entry_id:166669)变成了左手[坐标系](@entry_id:156346)，这会导致积分项贡献负的“面积”，从而可能产生非正定的[刚度矩阵](@entry_id:178659)，这在物理上是荒谬的。因此，任何有限元程序都必须在每个积分点检查 $\det \boldsymbol{J}  0$ [@problem_id:2599485]。

#### [减缩积分](@entry_id:167949)、[剪切自锁](@entry_id:164115)与[沙漏模式](@entry_id:174855)

对于某些问题，特别是涉及薄结构（如梁、板、壳）时，使用精确积分所有项的“完全积分”方案，反而会导致称为 **[剪切自锁](@entry_id:164115) (shear locking)** 的病态现象。

- **[剪切自锁](@entry_id:164115)**：以[Timoshenko梁](@entry_id:756014)单元为例，当梁的厚度 $t \to 0$ 时，其抗剪刚度相对于[抗弯刚度](@entry_id:180453)的比例会变得非常大，约为 $O(1/t^2)$。一个完全积分方案会试图在单元的多个点上强制[剪应变](@entry_id:175241)为零。对于低阶单元，这种过多的约束会导致其无法正确地弯曲，表现出远超实际的刚度，即“自锁” [@problem_id:2599469]。

- **[减缩积分](@entry_id:167949) (Reduced Integration)**：解决自锁的一种常用方法是 **[减缩积分](@entry_id:167949)** 或 **[选择性减缩积分](@entry_id:168281) (selective reduced integration)**。即对易于引起自锁的项（如剪切能项）使用比完全积分更低阶的积分法则（更少的[高斯点](@entry_id:170251)），而对其他项（如弯曲能项）仍使用完全积分。例如，对四节点[四边形单元](@entry_id:176937)的剪切项使用1[点积](@entry_id:149019)分。这相当于放宽了约束，从而显著改善单元在薄[结构分析](@entry_id:153861)中的表现 [@problem_id:2599469]。

- **[沙漏模式](@entry_id:174855) (Hourglass Modes)**：[减缩积分](@entry_id:167949)的代价是可能引入 **[伪零能模式](@entry_id:755267) (spurious zero-energy modes)**，通常称为 **[沙漏模式](@entry_id:174855) (hourglass modes)**。这些是单元的非[刚体运动](@entry_id:193355)变形模式，但在减缩的积分点上产生的应变为零，因此单元无法“感知”到这种变形，其贡献的能量为零。例如，对一个四节点[四边形单元](@entry_id:176937)的刚度矩阵使用1[点积](@entry_id:149019)分，其[刚度矩阵](@entry_id:178659)的秩会从5（完全积分时的秩，对应8个自由度减去3个[刚体模态](@entry_id:754366)）降低到3。这导致了 $8 - 3 - 3 = 2$ 个额外的[零能模式](@entry_id:172472)，即[沙漏模式](@entry_id:174855)。这些模式具有棋盘状的节点位移形式，若不加以控制，会导致整个结构计算失稳。因此，使用[减缩积分](@entry_id:167949)的单元通常需要配合 **[沙漏控制](@entry_id:163812) (hourglass control)** 技术来抑制这些[伪模式](@entry_id:163321) [@problem_id:2599460]。像 $\bar{B}$ 方法或混合公式等其他技术，也能达到缓解自锁的效果，其本质也与[减缩积分](@entry_id:167949)相似，都是为了减少运动学约束 [@problem_id:2599469]。

总之，刚度与载荷的数值积分是有限元方法中理论与实践紧密结合的领域。它不仅涉及[坐标变换](@entry_id:172727)和数值方法的数学基础，还包含了对单元行为、计算精度和稳定性的深刻理解。为特定问题选择合适的单元类型和积分方案，是在准确性、计算成本和稳定性之间进行权衡的艺术。