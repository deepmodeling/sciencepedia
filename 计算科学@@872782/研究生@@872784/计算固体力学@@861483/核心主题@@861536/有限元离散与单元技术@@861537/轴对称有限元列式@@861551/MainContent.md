## 引言
轴对称有限元公式是[计算固体力学](@entry_id:169583)中一种极其强大而高效的分析技术。通过利用几何、载荷和边界条件的[旋转不变性](@entry_id:137644)，它能将复杂的三维（3D）问题简化为计算成本更低的二维（2D）模型，广泛应用于[压力容器](@entry_id:191906)、旋转机械、岩土工程等领域的设计与分析。然而，这种简化并非没有代价。轴对称公式引入了独特的理论概念和数值挑战，例如非零的[环向应变](@entry_id:174548)、对称轴上的奇异性处理以及在特定材料下的[锁定现象](@entry_id:751421)。准确理解并掌握这些核心问题，是有效运用该方法的关键。

本文旨在系统性地构建您对[轴对称](@entry_id:173333)有限元公式的深入理解。我们将从第一章“原理与机制”开始，详细推导其运动学、本构关系和[有限元离散化](@entry_id:193156)过程。接着，在第二章“应用与交叉学科联系”中，我们将展示该方法如何在[结构动力学](@entry_id:172684)、[材料科学](@entry_id:152226)和岩[土力学](@entry_id:180264)等多个领域中解决实际工程问题。最后，通过第三章“动手实践”中的具体练习，您将有机会将理论知识应用于解决具体的数值问题。现在，让我们首先深入探讨轴对称有限元公式背后的基本原理与核心机制。

## 原理与机制

本章旨在深入阐述[轴对称](@entry_id:173333)有限元公式的理论基础和核心机制。我们将从运动学定义出发，推导[应变-位移关系](@entry_id:173321)和[本构方程](@entry_id:138559)，然后建立变分原理的[弱形式](@entry_id:142897)，并最终将其离散化为有限元方程。此外，我们还将探讨一些在实际应用中至关重要的特殊问题，如对称轴上的边界条件和[近不可压缩材料](@entry_id:752388)的[体积锁定](@entry_id:172606)现象。

### [轴对称](@entry_id:173333)变形的[运动学](@entry_id:173318)

轴对称问题的核心思想在于利用几何、材料属性、边界条件和载荷相对于某一根轴（通常是 $z$ 轴）的[旋转不变性](@entry_id:137644)，将一个三维（3D）问题简化为二维（2D）问题进行分析。这意味着所有物理场量，包括位移、应变和应力，都与环向坐标 $\theta$ 无关。

在最常见的纯轴对称问题中（即无扭转），物体中的任意一点只会在包含 $z$ 轴的子午平面（meridional plane）内移动。在[柱坐标系](@entry_id:266798) $(r, \theta, z)$ 中，这对应于一个[运动学](@entry_id:173318)约束：环向位移 $u_{\theta}$ 为零，而径向位移 $u_r$ 和轴向位移 $u_z$ 仅是坐标 $r$ 和 $z$ 的函数。

**位移场**可以表示为：
$u_r = u_r(r, z)$, $u_z = u_z(r, z)$, $u_{\theta} = 0$

要推导应变分量，我们从[柱坐标系](@entry_id:266798)下的一般小[应变-位移关系](@entry_id:173321)出发：
$$
\begin{aligned}
\varepsilon_{rr} = \frac{\partial u_r}{\partial r} \\
\varepsilon_{\theta\theta} = \frac{1}{r}\frac{\partial u_{\theta}}{\partial \theta} + \frac{u_r}{r} \\
\varepsilon_{zz} = \frac{\partial u_z}{\partial z} \\
\varepsilon_{rz} = \frac{1}{2} \left( \frac{\partial u_r}{\partial z} + \frac{\partial u_z}{\partial r} \right) \\
\varepsilon_{r\theta} = \frac{1}{2} \left( \frac{1}{r}\frac{\partial u_r}{\partial \theta} + \frac{\partial u_{\theta}}{\partial r} - \frac{u_{\theta}}{r} \right) \\
\varepsilon_{\theta z} = \frac{1}{2} \left( \frac{\partial u_{\theta}}{\partial z} + \frac{1}{r}\frac{\partial u_z}{\partial \theta} \right)
\end{aligned}
$$
将轴对称的[运动学](@entry_id:173318)约束（$u_{\theta} = 0$ 以及所有场量对 $\theta$ 的偏导数为零）代入上述关系，我们可以确定哪些应变分量必然为零，哪些可能不为零。[@problem_id:3545451]

剪切应变分量 $\varepsilon_{r\theta}$ 和 $\varepsilon_{\theta z}$ 的表达式中每一项都包含 $u_{\theta}$ 或对 $\theta$ 的偏导数，因此它们恒为零。
$\varepsilon_{r\theta} = 0$, $\varepsilon_{\theta z} = 0$

剩下的四个应变分量则可能不为零：
- **径向应变**: $\varepsilon_{rr} = \frac{\partial u_r}{\partial r}$
- **[轴向应变](@entry_id:160811)**: $\varepsilon_{zz} = \frac{\partial u_z}{\partial z}$
- **子午面内剪切应变**: $\varepsilon_{rz} = \frac{1}{2} \left( \frac{\partial u_r}{\partial z} + \frac{\partial u_z}{\partial r} \right)$ （工程[剪应变](@entry_id:175241)为 $\gamma_{rz} = 2\varepsilon_{rz}$）
- **环向（或周向）应变 (hoop strain)**: $\varepsilon_{\theta\theta} = \frac{u_r}{r}$

**[环向应变](@entry_id:174548)** $\varepsilon_{\theta\theta}$ 是[轴对称](@entry_id:173333)公式区别于平面应变问题的关键所在。[平面应变假设](@entry_id:186003)在 $r-z$ 平面内分析时，垂直于该平面的应变（即 $\varepsilon_{\theta\theta}$）为零。然而，在轴对称问题中，任何非零的径向位移 $u_r$ 都会导致材料周长的变化。一个初始半径为 $r$ 的材料[圆环](@entry_id:163678)，其[周长](@entry_id:263239)为 $2\pi r$。当发生径向位移 $u_r$ 后，其新半径变为 $r+u_r$，新周长变为 $2\pi (r+u_r)$。根据定义，应变是长度的相对变化量，因此[环向应变](@entry_id:174548)为 $(2\pi (r+u_r) - 2\pi r) / (2\pi r) = u_r/r$。这个非零的[环向应变](@entry_id:174548)会产生相应的[环向应力](@entry_id:190931) $\sigma_{\theta\theta}$，这是维持旋转体（如[压力容器](@entry_id:191906)或旋转飞轮）平衡所必需的。[@problem_id:3545392] [@problem_id:3545397]

在某些特定问题中，如[轴对称](@entry_id:173333)杆的扭转，我们也可以考虑一个非零的环向位移 $u_{\theta}(r, z)$。在这种情况下，虽然[位移场](@entry_id:141476)仍然与 $\theta$ 无关，但会产生非零的剪切应变分量 $\gamma_{r\theta}$ 和 $\gamma_{\theta z}$，从而能够模拟扭转变形。[@problem_id:3545392]

### 轴对称分析的本构关系

由于轴对称问题中存在四个潜在的非零应变分量（$\varepsilon_{rr}, \varepsilon_{zz}, \varepsilon_{\theta\theta}, \varepsilon_{rz}$），我们不能像[平面应力](@entry_id:172193)问题那样预先假设某个应力分量为零来简化[本构关系](@entry_id:186508)。相反，我们必须从完整的三维[本构定律](@entry_id:178936)出发，并将其特殊化以适应[轴对称](@entry_id:173333)的运动学。[@problem_id:3545392]

对于一个均匀、各向同性的线弹性材料，其三维[应力-应变关系](@entry_id:274093)（[胡克定律](@entry_id:149682)）可以用拉梅参数 $\lambda$ 和 $G$（剪切模量）表示为：
$$
\sigma_{ij} = \lambda \operatorname{tr}(\boldsymbol{\varepsilon}) \delta_{ij} + 2G \varepsilon_{ij}
$$
其中 $\operatorname{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{kk} = \varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta}$ 是[应变张量](@entry_id:193332)的迹（[体积应变](@entry_id:267252)），$\delta_{ij}$ 是克罗内克符号。

我们将这个通用形式应用于[轴对称](@entry_id:173333)情况的非零应力分量 [@problem_id:3545449]：
- **[径向应力](@entry_id:197086)**: $\sigma_{rr} = \lambda(\varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta}) + 2G\varepsilon_{rr}$
- **轴向应力**: $\sigma_{zz} = \lambda(\varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta}) + 2G\varepsilon_{zz}$
- **[环向应力](@entry_id:190931)**: $\sigma_{\theta\theta} = \lambda(\varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta}) + 2G\varepsilon_{\theta\theta}$
- **剪切应力**: $\tau_{rz} = \sigma_{rz} = 2G\varepsilon_{rz}$

为了方便有限元实现，我们通常将应力和应变写成向量形式，并建立它们之间的矩阵关系 $\boldsymbol{\sigma} = \mathbf{D}_{\text{axisym}} \boldsymbol{\varepsilon}$。常用的应力-应变向量定义为：
$$
\boldsymbol{\sigma} = \begin{pmatrix} \sigma_{rr} \\ \sigma_{zz} \\ \sigma_{\theta\theta} \\ \tau_{rz} \end{pmatrix}, \quad
\boldsymbol{\varepsilon} = \begin{pmatrix} \varepsilon_{rr} \\ \varepsilon_{zz} \\ \varepsilon_{\theta\theta} \\ \gamma_{rz} \end{pmatrix}
$$
注意，应变向量中通常使用工程[剪应变](@entry_id:175241) $\gamma_{rz} = 2\varepsilon_{rz}$。将上述应力表达式整理成矩阵形式，并将拉梅参数用更工程化的[杨氏模量](@entry_id:140430) $E$ 和[泊松比](@entry_id:158876) $\nu$ 替换（使用关系式 $\lambda = \frac{E\nu}{(1+\nu)(1-2\nu)}$ 和 $G = \frac{E}{2(1+\nu)}$），我们得到 $4 \times 4$ 的[轴对称](@entry_id:173333)[本构矩阵](@entry_id:164908) $\mathbf{D}_{\text{axisym}}$：
$$
\mathbf{D}_{\text{axisym}} = \frac{E}{(1+\nu)(1-2\nu)}
\begin{pmatrix}
1-\nu  & \nu  & \nu  & 0 \\
\nu  & 1-\nu  & \nu  & 0 \\
\nu  & \nu  & 1-\nu  & 0 \\
0  & 0  & 0  & \frac{1-2\nu}{2}
\end{pmatrix}
$$
这个矩阵是后续计算[单元刚度矩阵](@entry_id:139369)的核心组成部分。

### [变分原理](@entry_id:198028)与[弱形式](@entry_id:142897)

有限元法的数学基础是变分原理，通常以[虚功原理](@entry_id:138749)（Principle of Virtual Work, PVW）的[弱形式](@entry_id:142897)表达。对于一个三维连续体，其PVW可以写作：
$$
\int_{V} \boldsymbol{\sigma} : \delta\boldsymbol{\varepsilon} \, \mathrm{d}V = \int_{V} \mathbf{b} \cdot \delta\mathbf{u} \, \mathrm{d}V + \int_{S_t} \mathbf{t} \cdot \delta\mathbf{u} \, \mathrm{d}S
$$
其中，左侧是[内虚功](@entry_id:172278)，右侧是[体力](@entry_id:174230) $\mathbf{b}$ 和面力 $\mathbf{t}$ 所做的外[虚功](@entry_id:176403)。

为了得到轴对称问题的弱形式，我们需要将这些在整个三维体积 $V$ 和边界面 $S_t$ 上的积分，转化为在二维子午平面域 $\Omega$ 及其边界 $\Gamma_t$ 上的积分。[@problem_id:3545457] 关键在于处理[微分](@entry_id:158718)单元。

在[柱坐标系](@entry_id:266798)中，[微分](@entry_id:158718)[体积元](@entry_id:267802)为 $\mathrm{d}V = r \, \mathrm{d}r \, \mathrm{d}\theta \, \mathrm{d}z$。我们可以将其重写为 $\mathrm{d}V = (r \, \mathrm{d}\theta) \, (\mathrm{d}r \, \mathrm{d}z) = (r \, \mathrm{d}\theta) \, \mathrm{d}\Omega$，其中 $\mathrm{d}\Omega$ 是子午平面内的[微分](@entry_id:158718)面积元。对于体积积分中的任意一个被积函数 $f(r,z)$（例如 $\boldsymbol{\sigma}:\delta\boldsymbol{\varepsilon}$），由于[轴对称](@entry_id:173333)性，它不依赖于 $\theta$。因此，积分可以写为：
$$
\int_{V} f(r,z) \, \mathrm{d}V = \int_{\Omega} \left( \int_{0}^{2\pi} f(r,z) \, r \, \mathrm{d}\theta \right) \mathrm{d}\Omega = \int_{\Omega} f(r,z) \, r \left( \int_{0}^{2\pi} \mathrm{d}\theta \right) \mathrm{d}\Omega = \int_{\Omega} 2\pi r \, f(r,z) \, \mathrm{d}\Omega
$$
同样地，对于边界面上的积分，由子午平面边界上的线元 $\mathrm{d}\Gamma$ 绕 $z$ 轴旋转而成的[微分](@entry_id:158718)面积元是 $\mathrm{d}S = r \, \mathrm{d}\theta \, \mathrm{d}\Gamma$。因此，面力积分也遵循相同的转换规则。

最终，轴对称问题的[虚功原理](@entry_id:138749)弱形式为：
$$
\int_{\Omega} (\boldsymbol{\sigma}:\delta\boldsymbol{\varepsilon}) \, 2\pi r \, \mathrm{d}\Omega = \int_{\Omega} (\mathbf{b}\cdot\delta\mathbf{u}) \, 2\pi r \, \mathrm{d}\Omega + \int_{\Gamma_t} (\mathbf{t}\cdot\delta\mathbf{u}) \, 2\pi r \, \mathrm{d}\Gamma
$$
这个表达式是至关重要的。它表明，在从三维问题简化到二维子午平面分析时，所有的积分项都必须乘以一个权重因子 $2\pi r$。这个因子物理上代表了在半径 $r$ 处的一个单位面积（或单位长度）的子午平面元，在三维空间中实际对应的[环状体](@entry_id:263065)积（或环状面积）。[@problem_id:3545457] [@problem_id:3545432]

### [有限元离散化](@entry_id:193156)

在得到弱形式方程后，下一步是使用有限元方法对其进行离散化。我们以一个四节点[双线性](@entry_id:146819)[四边形单元](@entry_id:176937)为例，阐述其 isoparametric（等参）公式。

#### 位移插值

在[等参单元](@entry_id:173863)中，我们使用相同的形函数 $N_i$ 来插值单元的几何坐标和[位移场](@entry_id:141476)。对于一个四[节点单元](@entry_id:752523)，径向和轴向位移可以表示为节点位移的加权和：
$$
u_r(r,z) = \sum_{i=1}^{4} N_i(r,z) u_{ri}, \quad u_z(r,z) = \sum_{i=1}^{4} N_i(r,z) u_{zi}
$$
其中 $u_{ri}$ 和 $u_{zi}$ 是节点 $i$ 的径向和轴向位移自由度。

#### [应变-位移矩阵](@entry_id:163451) (B 矩阵)

[应变-位移矩阵](@entry_id:163451) $\mathbf{B}$ 建立了[单元应变](@entry_id:163000)向量 $\boldsymbol{\varepsilon}$ 与节点位移向量 $\mathbf{u}_e$ 之间的关系，即 $\boldsymbol{\varepsilon} = \mathbf{B} \mathbf{u}_e$。通过将位移插值代入应变定义，我们可以推导出 $\mathbf{B}$ 矩阵的每一行。[@problem_id:3545388]

对于节点 $i$ 的自由度 $(u_{ri}, u_{zi})$，其对四个应变分量的贡献如下：
- $\varepsilon_{rr} = \frac{\partial u_r}{\partial r} \implies$ 贡献来自 $\frac{\partial N_i}{\partial r} u_{ri}$
- $\varepsilon_{zz} = \frac{\partial u_z}{\partial z} \implies$ 贡献来自 $\frac{\partial N_i}{\partial z} u_{zi}$
- $\gamma_{rz} = \frac{\partial u_r}{\partial z} + \frac{\partial u_z}{\partial r} \implies$ 贡献来自 $\frac{\partial N_i}{\partial z} u_{ri} + \frac{\partial N_i}{\partial r} u_{zi}$
- $\varepsilon_{\theta\theta} = \frac{u_r}{r} \implies$ 贡献来自 $\frac{N_i}{r} u_{ri}$

将这些项整理成对应于节点位移向量 $\mathbf{u}_e = [u_{r1}, u_{z1}, u_{r2}, u_{z2}, \dots]^T$ 的形式，我们得到 $4 \times 8$ 的 $\mathbf{B}$ 矩阵：
$$
\mathbf{B} =
\begin{pmatrix}
\frac{\partial N_1}{\partial r}  & 0  & \frac{\partial N_2}{\partial r}  & 0  & \frac{\partial N_3}{\partial r}  & 0  & \frac{\partial N_4}{\partial r}  & 0 \\
0  & \frac{\partial N_1}{\partial z}  & 0  & \frac{\partial N_2}{\partial z}  & 0  & \frac{\partial N_3}{\partial z}  & 0  & \frac{\partial N_4}{\partial z} \\
\frac{\partial N_1}{\partial z}  & \frac{\partial N_1}{\partial r}  & \frac{\partial N_2}{\partial z}  & \frac{\partial N_2}{\partial r}  & \frac{\partial N_3}{\partial z}  & \frac{\partial N_3}{\partial r}  & \frac{\partial N_4}{\partial z}  & \frac{\partial N_4}{\partial r} \\
\frac{N_1}{r}  & 0  & \frac{N_2}{r}  & 0  & \frac{N_3}{r}  & 0  & \frac{N_4}{r}  & 0
\end{pmatrix}
$$
值得注意的是，$\mathbf{B}$ 矩阵的最后一行包含了形函数 $N_i$ 本身以及变量 $r$，这与平面问题中的 $\mathbf{B}$ 矩阵有本质不同。在计算中，分母中的 $r$ 也必须通过形函数进行插值，即 $r = \sum N_j r_j$。[@problem_id:3545458]

作为一个具体的例子，我们可以计算单元[中心点](@entry_id:636820) $(\xi=0, \eta=0)$ 的[环向应变](@entry_id:174548)。在此点，所有双线性形函数 $N_i$ 的值均为 $\frac{1}{4}$。因此，该点的径向位移和半径分别为 $u_r = \frac{1}{4}\sum u_{ri}$ 和 $r = \frac{1}{4}\sum r_i$。代入[环向应变](@entry_id:174548)公式，我们得到一个直观的结果：
$$
\varepsilon_{\theta\theta}(\text{center}) = \frac{u_r}{r} = \frac{\frac{1}{4}(u_{r,1} + u_{r,2} + u_{r,3} + u_{r,4})}{\frac{1}{4}(r_1 + r_2 + r_3 + r_4)} = \frac{\sum u_{r,i}}{\sum r_i}
$$
这表示单元中心的[环向应变](@entry_id:174548)近似为[节点平均](@entry_id:178002)径向位移与[节点平均](@entry_id:178002)半径之比。[@problem_id:3545397]

#### [单元刚度矩阵](@entry_id:139369)

将离散化的应力 $\boldsymbol{\sigma} = \mathbf{D} \mathbf{B} \mathbf{u}_e$ 和虚应变 $\delta\boldsymbol{\varepsilon} = \mathbf{B} \delta\mathbf{u}_e$ 代入[弱形式](@entry_id:142897)的[内虚功](@entry_id:172278)项，即可得到[单元刚度矩阵](@entry_id:139369) $\mathbf{K}_e$ 的表达式：
$$
\mathbf{K}_e = \int_{A_e} \mathbf{B}^T \mathbf{D}_{\text{axisym}} \mathbf{B} \, (2\pi r) \, \mathrm{d}A
$$
为了进行数值积分（如高斯积分），该积分需要被转换到父单元域 $[-1, 1] \times [-1, 1]$ 上。[微分](@entry_id:158718)[面积元](@entry_id:263205)的关系是 $\mathrm{d}A = \mathrm{d}r\,\mathrm{d}z = \det(\mathbf{J}) \, \mathrm{d}\xi \, \mathrm{d}\eta$，其中 $\mathbf{J}$ 是从 $(\xi, \eta)$ 到 $(r, z)$ 的[坐标变换](@entry_id:172727)雅可比矩阵。最终，用于数值计算的刚度矩阵积分表达式为：
$$
\mathbf{K}_e = \int_{-1}^{1} \int_{-1}^{1} \mathbf{B}(\xi, \eta)^T \mathbf{D}_{\text{axisym}} \mathbf{B}(\xi, \eta) \, 2\pi r(\xi, \eta) \, \det(\mathbf{J}(\xi, \eta)) \, \mathrm{d}\xi \, \mathrm{d}\eta
$$
该积分通过在高斯积分点上对被积函数求值并加权求和来近似计算。在每个积分点，都必须计算该点的 $\mathbf{B}$ 矩阵、半径 $r$ 和雅可比行列式 $\det(\mathbf{J})$。[@problem_id:3545458]

### 特殊考虑与高等专题

#### 对称轴上的边界条件

在[轴对称](@entry_id:173333)模型中，$r=0$ 的轴线是一个[坐标奇点](@entry_id:159160)，需要特别处理以保证解的物理合理性和数学正则性。从[环向应变](@entry_id:174548) $\varepsilon_{\theta\theta}=u_r/r$ 的表达式可以看出，如果当 $r \to 0$ 时 $u_r$ 不趋于零，应变将会是奇异的，这是不符合物理实际的。[@problem_id:3545456]

为了确保[位移场](@entry_id:141476)在三维笛卡尔坐标系下是光滑的，必须满足以下**[正则性条件](@entry_id:166962)**：
1.  **径向位移为零**: $u_r(0, z) = 0$。这意味着[对称轴](@entry_id:177299)上的点只能沿着轴线移动。
2.  **轴向位移的径向导数为零**: $\frac{\partial u_z}{\partial r}(0, z) = 0$。这源于[轴对称](@entry_id:173333)性，即 $u_z$ 关于 $r$ 必须是一个偶函数。

这些条件有进一步的推论。使用[洛必达法则](@entry_id:147503)，我们可以确定在轴线上的[环向应变](@entry_id:174548)：
$$
\lim_{r\to 0} \varepsilon_{\theta\theta} = \lim_{r\to 0} \frac{u_r}{r} = \lim_{r\to 0} \frac{\partial u_r}{\partial r} = \varepsilon_{rr}(0,z)
$$
这意味着在[对称轴](@entry_id:177299)上，[环向应变](@entry_id:174548)等于径向应变。对于[各向同性材料](@entry_id:170678)，这也意味着 $\sigma_{\theta\theta}(0,z) = \sigma_{rr}(0,z)$。

在有限元实现中，我们必须强制施加[运动学](@entry_id:173318)条件 $u_r(0, z) = 0$。这通过对所有位于[对称轴](@entry_id:177299)上的节点施加一个固支约束（Dirichlet boundary condition）来实现，即将其径向位移自由度固定为零。轴向位移自由度 $u_z$ 则保持自由，除非有外部约束。值得强调的是，[对称轴](@entry_id:177299)是物体内部的一条线，而不是一个物理边界，因此不应在其上施加任何面力（Neumann）条件。[@problem_id:3545456]

#### [体积锁定](@entry_id:172606)与[混合格式](@entry_id:167436)

在模拟[近不可压缩材料](@entry_id:752388)（即[泊松比](@entry_id:158876) $\nu \to 0.5$，或[体积模量](@entry_id:160069) $K$ 远大于剪切模量 $G$）时，标准的位移基有限元公式会遇到一种称为**[体积锁定](@entry_id:172606) (volumetric locking)** 的数值问题。

其机理如下：对于[近不可压缩材料](@entry_id:752388)，其[应变能](@entry_id:162699)主要由体积变化贡献，并且[体积应变](@entry_id:267252) $\varepsilon_v = \varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta}$ 必须非常接近于零。在位移有限元中，刚度矩阵的体积项 $K \int (2\pi r) \mathbf{B}_v^T \mathbf{B}_v dA$ 充当了一个巨大的惩罚项，试图在所有高斯积分点上强制执行 $\varepsilon_v \approx 0$ 的约束。然而，对于低阶单元（如四节点双线性单元），其[插值函数](@entry_id:262791)提供的运动模式非常有限，不足以在满足变形的同时精确地在多个积分点上实现 $\varepsilon_v = 0$。特别是[轴对称单元](@entry_id:163652)中 $\varepsilon_v$ 表达式里包含的 $u_r/r$ 项，使得约束条件更为复杂。其结果是，单元为了满足这个过强的约束，只能选择几乎不变形，从而表现出远超其实际物理值的“伪刚度”，即为“锁定”。[@problem_id:3545454]

解决[体积锁定](@entry_id:172606)的标准方法是采用**混合位移-压力（u-p）格式**。该方法将[静水压力](@entry_id:275365) $p$ (或[平均应力](@entry_id:751819)) 作为一个独立的插值场引入，而不是从[位移场](@entry_id:141476)导出。弱形式被修改为一个[鞍点问题](@entry_id:174221)，其中压[力场](@entry_id:147325)充当拉格朗日乘子，以积分形式（[弱形式](@entry_id:142897)）来施加不可压缩约束 $\int q \cdot \varepsilon_v \, dV = 0$。这种方法用一个全局的、较弱的约束替代了在每个积分点上的强约束，从而释放了单元的变形能力，避免了锁定。

为了保证[混合格式](@entry_id:167436)的数值稳定性和收敛性，位移和压力的插值空间必须满足一个关键的数学条件，即 **Ladyzhenskaya–Babuška–Brezzi (LBB) [inf-sup 条件](@entry_id:174538)**。不满足此条件的单元对（例如，对位移和压力使用相同的[双线性插值](@entry_id:170280)）会导致[伪压力模式](@entry_id:755261)和不稳定的解。因此，通常需要采用“高阶位移/低阶压力”的策略，例如，用九节点二次单元插值位移，用不连续的线性或常数插值压力。[@problem_id:3545454]