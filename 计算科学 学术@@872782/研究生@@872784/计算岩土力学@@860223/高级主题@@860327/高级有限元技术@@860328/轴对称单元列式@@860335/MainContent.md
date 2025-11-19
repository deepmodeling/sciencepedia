## 引言
在计算力学领域，[轴对称单元](@entry_id:163652)公式是分析具有旋转对称性三维问题的基石。对于诸如圆形地基、隧道、[压力容器](@entry_id:191906)或土坝等工程结构，完整的全三维[有限元分析](@entry_id:138109)往往计算成本高昂且非必要。轴对称公式通过利用几何、荷载和材料属性的对称性，将问题巧妙地[降维](@entry_id:142982)至二维平面进行求解，极大地提升了分析效率，使其成为工程师和研究人员不可或缺的工具。然而，这种简化并非简单的二维平面问题，其背后蕴含着独特的运动学假设和力学内涵，若理解不当，极易导致错误的结果。本文旨在系统性地解决这一知识鸿沟，为读者提供一个从理论到实践的完整指南。

本文将分为三个核心章节。第一章，**“原理与机制”**，将深入探讨[轴对称单元](@entry_id:163652)的理论基础，从运动学假设出发，推导其独特的应变场，构建[有限元弱形式](@entry_id:756663)，并详细讨论数值实现中的关键技术细节，如对称轴处理和[体积锁定](@entry_id:172606)等问题。第二章，**“应用与交叉学科联系”**，将展示该公式在岩土与结构工程中的广泛应用，并进一步拓展至热-力-流-化等多物理场耦合问题以及接触、断裂等高度[非线性力学](@entry_id:178303)行为的分析。最后，在第三章，**“动手实践”**中，我们将通过一系列精心设计的编程练习，引导读者亲手实现并验证[轴对称单元](@entry_id:163652)的关键特性，从而将理论知识转化为解决实际问题的能力。通过学习本文，读者将能够全面掌握[轴对称单元](@entry_id:163652)的精髓，并将其自信地应用于复杂的工程与科研挑战中。

## 原理与机制

本章旨在深入阐述[轴对称单元](@entry_id:163652)公式的理论基础和核心机制。我们将从其运动学假设出发，推导[应变-位移关系](@entry_id:173321)，并将其与经典的二维平面问题进行对比。随后，我们将系统地构建基于虚功原理的[有限元弱形式](@entry_id:756663)，并详细探讨数值积分、[应变-位移矩阵](@entry_id:163451)的构造、[对称轴](@entry_id:177299)处的特殊处理、边界条件的施加以及在[近不可压缩材料](@entry_id:752388)分析中可能出现的[体积锁定](@entry_id:172606)等高级问题。

### 轴对称[运动学](@entry_id:173318)假设

[轴对称](@entry_id:173333)分析的核心思想在于利用几何、荷载、边界条件及材料属性在周向（$\theta$）上的[不变性](@entry_id:140168)，将一个三维实体问题简化为二维问题。在[圆柱坐标系](@entry_id:266798) $(r, \theta, z)$ 中，[位移矢量](@entry_id:262782)为 $\boldsymbol{u}=(u_r, u_\theta, u_z)$。轴对称假设意味着所有物理量均不依赖于周向角 $\theta$，即对于任意物理量 $\phi$，我们有 $\frac{\partial \phi}{\partial \theta} = 0$。

在大多数工程应用中，例如竖向荷载作用下的地基或[内压](@entry_id:153696)作用下的圆柱形压力容器，问题不涉及扭转。因此，标准的[轴对称](@entry_id:173333)运动学模型进一步假设周向位移为零，即 $u_\theta = 0$。

综合这些假设，位移场被完全简化：
$$
u_r = u_r(r, z)
$$
$$
u_\theta = 0
$$
$$
u_z = u_z(r, z)
$$

这一简化具有深远的意义。它意味着三维空间中任意一点的运动被限制在其所在的子午平面（一个固定的 $\theta$ 角所定义的 $r-z$ 半平面）内。整个三维体的变形可以通过分析这个二维的 $r-z$ 平面来完全描述。因此，在[有限元离散化](@entry_id:193156)中，我们只需在 $r-z$ 平面上划分网格。该平面内每个节点仅需存储描述其平面内运动的位移分量：径向位移 $u_r$ 和轴向位移 $u_z$。于是，每个节点具有 **两个位移自由度 (DOF)**。[@problem_id:3502216]

### 轴对称[应变-位移关系](@entry_id:173321)

在确定了[运动学](@entry_id:173318)框架后，我们接下来考察在此框架下的应变状态。在小应变假设下，[圆柱坐标系](@entry_id:266798)中的一般[应变-位移关系](@entry_id:173321)为：
$$
\varepsilon_{rr} = \frac{\partial u_r}{\partial r}
$$
$$
\varepsilon_{\theta\theta} = \frac{1}{r}\frac{\partial u_\theta}{\partial \theta} + \frac{u_r}{r}
$$
$$
\varepsilon_{zz} = \frac{\partial u_z}{\partial z}
$$
$$
\gamma_{r\theta} = 2\varepsilon_{r\theta} = \frac{1}{r}\frac{\partial u_r}{\partial \theta} + \frac{\partial u_\theta}{\partial r} - \frac{u_\theta}{r}
$$
$$
\gamma_{\theta z} = 2\varepsilon_{\theta z} = \frac{\partial u_\theta}{\partial z} + \frac{1}{r}\frac{\partial u_z}{\partial \theta}
$$
$$
\gamma_{rz} = 2\varepsilon_{rz} = \frac{\partial u_z}{\partial r} + \frac{\partial u_r}{\partial z}
$$
其中 $\gamma_{ij}$ 表示工程[剪应变](@entry_id:175241)。

将[轴对称](@entry_id:173333)运动学假设（$u_\theta = 0$ 和 $\frac{\partial}{\partial \theta} = 0$）代入上述关系，我们可以确定哪些应变分量为零，哪些依然存在：
- **径向[正应变](@entry_id:204633)**: $\varepsilon_{rr} = \frac{\partial u_r}{\partial r}$ (通常非零)
- **轴向[正应变](@entry_id:204633)**: $\varepsilon_{zz} = \frac{\partial u_z}{\partial z}$ (通常非零)
- **周向（环向）[正应变](@entry_id:204633)**: $\varepsilon_{\theta\theta} = \frac{1}{r}\frac{\partial (0)}{\partial \theta} + \frac{u_r}{r} = \frac{u_r}{r}$ (通常非零)
- **子午面内[剪应变](@entry_id:175241)**: $\gamma_{rz} = \frac{\partial u_z}{\partial r} + \frac{\partial u_r}{\partial z}$ (通常非零)
- **面外[剪应变](@entry_id:175241)**: $\gamma_{r\theta} = 0$ 和 $\gamma_{\theta z} = 0$

因此，在标准的[轴对称](@entry_id:173333)问题中，存在四个非零的应变分量。通常将它们组合成一个应变矢量 $\boldsymbol{\varepsilon}$，其标准形式为：
$$
\boldsymbol{\varepsilon} = \begin{pmatrix} \varepsilon_{rr}  \varepsilon_{zz}  \varepsilon_{\theta\theta}  \gamma_{rz} \end{pmatrix}^T
$$
[@problem_id:3502233]

其中，**[环向应变](@entry_id:174548)** $\varepsilon_{\theta\theta} = u_r/r$ 是一个关键且独特的组成部分。它表明，即使没有周向位移，仅径向位移 $u_r$ 就会引起周向纤维的拉伸或压缩，从而产生应变。想象一个圆环，当其半径从 $r$ 变为 $r+u_r$ 时，其[周长](@entry_id:263239)从 $2\pi r$ 变为 $2\pi(r+u_r)$。[环向应变](@entry_id:174548)的定义即为周长的相对变化：$(\text{新周长} - \text{原周长}) / \text{原周长} = \frac{2\pi(r+u_r) - 2\pi r}{2\pi r} = \frac{u_r}{r}$。

### 与二维平面公式的比较

轴对称公式虽然是在一个二维平面上求解，但其物理内涵与经典的[平面应变](@entry_id:167046)和[平面应力](@entry_id:172193)问题有本质区别。

**与平面应变的区别**：[平面应变假设](@entry_id:186003)在一个方向上（例如 $z$ 方向）没有应变，即 $\varepsilon_{zz} = \gamma_{xz} = \gamma_{yz} = 0$。如果我们将此概念应用于轴对称问题的 $r-z$ 平面，那么“面外”方向就是 $\theta$ 方向。[平面应变](@entry_id:167046)条件将要求 $\varepsilon_{\theta\theta}=0$。然而，在轴对称分析中，$\varepsilon_{\theta\theta} = u_r/r$。要使其恒等于零，则必须有 $u_r=0$（在 $r \neq 0$ 的区域）。这将过度[约束系统](@entry_id:164587)，使其无法发生径向变形，这与大多数实际的[轴对称](@entry_id:173333)问题不符。因此，[轴对称](@entry_id:173333)问题**不是**一种特殊形式的[平面应变](@entry_id:167046)问题。[@problem_id:3502233]

**刚度内涵**：[环向应变](@entry_id:174548)的存在对系统的力学行为有显著影响。在[各向同性线弹性](@entry_id:185899)材料中，应力分量通过[本构关系](@entry_id:186508)与所有[正应变](@entry_id:204633)分量耦合。例如，[径向应力](@entry_id:197086) $\sigma_{rr}$ 不仅依赖于 $\varepsilon_{rr}$，还依赖于体积应变 $\varepsilon_v = \varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta}$。[环向应变](@entry_id:174548) $\varepsilon_{\theta\theta}$ 作为[体积应变](@entry_id:267252)的一部分，会通过泊松效应影响到 $\sigma_{rr}$ 和 $\sigma_{zz}$。这种耦合效应意味着，要产生相同的径向位移 $u_r$，[轴对称](@entry_id:173333)体需要抵抗额外的环向拉伸，这使其表现出比相应[平面应变](@entry_id:167046)体更高的“表观刚度”。环向纤维就像一组约束径向变形的弹簧，提供了额外的约束。[@problem_id:3502252]

### [弱形式](@entry_id:142897)与[数值积分](@entry_id:136578)

有限元法的数学基础是其积分形式（或称弱形式），通常由虚功原理导出。[内虚功](@entry_id:172278)（IVW）表示为应力与虚应变在整个体积上的积分：
$$
\text{IVW} = \int_V \delta\boldsymbol{\varepsilon}^T \boldsymbol{\sigma} \, dV
$$
为了在轴对称框架下计算此积分，我们必须使用[圆柱坐标系](@entry_id:266798)下的体积微元 $dV = r \, dr \, d\theta \, dz$。这一表达式中的因子 $r$ 源于从[笛卡尔坐标](@entry_id:167698)到圆柱坐标的坐标变换的[雅可比行列式](@entry_id:137120)。[@problem_id:3502216]

由于被积函数（应力、应变等）在[轴对称](@entry_id:173333)假设下不依赖于 $\theta$，我们可以先对 $\theta$ 进行积分：
$$
\text{IVW} = \int_{A} \left( \int_0^{2\pi} d\theta \right) (\delta\boldsymbol{\varepsilon}^T \boldsymbol{\sigma}) \, r \, dr \, dz = \int_{A} (\delta\boldsymbol{\varepsilon}^T \boldsymbol{\sigma}) \, (2\pi r) \, dA
$$
其中 $A$ 是 $r-z$ 平面上的二维积分域，$dA = dr \, dz$。此结果表明，三维体积积分被精确地转化为在子午平面上的二维面积分，但被积函数多了一个权重因子 $2\pi r$。

在等参元公式中，单元内的积分需要变换到标准母单元[坐标系](@entry_id:156346) $(\xi, \eta)$ 中进行。面积微元变换为 $dA = \det(\boldsymbol{J}) \, d\xi \, d\eta$，其中 $\boldsymbol{J}$ 是从 $(\xi, \eta)$ 到 $(r, z)$ 的坐标变换的雅可比矩阵。因此，单元内的任意积分项最终形式为：
$$
\int_{A_e} f(r, z) \, (2\pi r) \, dA = \int_{-1}^1 \int_{-1}^1 f(\xi, \eta) \, 2\pi \, r(\xi, \eta) \, \det(\boldsymbol{J}(\xi, \eta)) \, d\xi \, d\eta
$$
该积分通常采用[高斯求积法](@entry_id:146011)进行数值计算。在每个[高斯点](@entry_id:170251) $(\xi_g, \eta_g)$，其对应的积分权重为：
$$
W_g = w_g \cdot \det(\boldsymbol{J}_g) \cdot 2\pi r_g
$$
其中 $w_g$ 是标准的高斯权重，$\det(\boldsymbol{J}_g)$ 是在该点计算的[雅可比行列式](@entry_id:137120)，而 $r_g = r(\xi_g, \eta_g)$ 是通过形函数从节点坐标插值得到的该[高斯点](@entry_id:170251)的[径向坐标](@entry_id:165186)。[@problem_id:3502250]

值得注意的是，在小应变或总拉格朗日 (Total Lagrangian) 有限变形分析中，$r_g$ 是由初始节点坐标计算的。而在更新拉格朗日 (Updated Lagrangian) 有限变形分析中，由于积分在当前构型上进行，$r_g$ 必须由当前时刻的节点坐标在每个迭代步中重新计算。[@problem_id:3502250]

### [应变-位移矩阵](@entry_id:163451) (B 矩阵)

在有限元中，单元内的位移场由节点位移通过形函数 $N_i$ 插值得到：
$$
u_r(r, z) = \sum_{i=1}^{n} N_i(r, z) u_{ri}, \quad u_z(r, z) = \sum_{i=1}^{n} N_i(r, z) u_{zi}
$$
其中 $n$ 是单元的节点数，$(u_{ri}, u_{zi})$ 是节点 $i$ 的自由度。

应变矢量 $\boldsymbol{\varepsilon}$ 与单元的节点[位移矢量](@entry_id:262782) $\boldsymbol{d}_e = \begin{pmatrix} u_{r1}  u_{z1}  \dots  u_{rn}  u_{zn} \end{pmatrix}^T$ 通过[应变-位移矩阵](@entry_id:163451) $\boldsymbol{B}$ 建立联系：$\boldsymbol{\varepsilon} = \boldsymbol{B} \boldsymbol{d}_e$。$\boldsymbol{B}$ 矩阵的每一列对应一个节点自由度，每一行对应一个应变分量。

将插值位移代入应变定义，可推导出 $\boldsymbol{B}$ 矩阵的各项。对于节点 $i$ 的自由度 $(u_{ri}, u_{zi})$，其对应的 $4 \times 2$ 子矩阵 $\boldsymbol{B}_i$ 为：
$$
\boldsymbol{B}_i = \begin{pmatrix}
\frac{\partial N_i}{\partial r}  0 \\
0  \frac{\partial N_i}{\partial z} \\
\frac{N_i}{r}  0 \\
\frac{\partial N_i}{\partial z}  \frac{\partial N_i}{\partial r}
\end{pmatrix}
$$
完整的 $\boldsymbol{B}$ 矩阵由所有节点的子矩阵 $\boldsymbol{B}_i$ 横向拼接而成：$\boldsymbol{B} = \begin{pmatrix} \boldsymbol{B}_1  \boldsymbol{B}_2  \dots  \boldsymbol{B}_n \end{pmatrix}$。[@problem_id:3502229]

在等参元中，形函数 $N_i$ 是母单元坐标 $(\xi, \eta)$ 的函数。其对物理坐标 $(r, z)$ 的导数需要通过链式法则和[雅可比矩阵](@entry_id:264467)的逆来计算：
$$
\begin{pmatrix} \frac{\partial N_i}{\partial r} \\ \frac{\partial N_i}{\partial z} \end{pmatrix} = \boldsymbol{J}^{-1} \begin{pmatrix} \frac{\partial N_i}{\partial \xi} \\ \frac{\partial N_i}{\partial \eta} \end{pmatrix}
$$
将此关系代入，我们便得到了在任意[高斯点](@entry_id:170251) $(\xi_g, \eta_g)$ 处计算 $\boldsymbol{B}$ 矩阵的完整表达式，这对于计算[单元刚度矩阵](@entry_id:139369)至关重要。[@problem_id:3502268]

### 对称轴 $r=0$ 处的特殊处理

当单元的一条边或一个节点位于[对称轴](@entry_id:177299) $r=0$ 上时，必须进行特殊处理，以避免数值上的奇异性。问题的核心在于[环向应变](@entry_id:174548) $\varepsilon_{\theta\theta} = u_r/r$ 以及 $\boldsymbol{B}$ 矩阵中出现的 $N_i/r$ 项。

从物理角度看，[对称轴](@entry_id:177299)上的点只能沿轴向移动，任何径向位移都是不符合物理连续性的。因此，一个必要的**物理[正则性条件](@entry_id:166962)**是在轴线上必须有 $u_r = 0$。为了保证应变场有界，特别是 $\varepsilon_{\theta\theta}$ 在 $r \to 0$ 时为有限值，径向位移场 $u_r$ 在 $r=0$ 附近必须是 $r$ 的高阶小量，即 $u_r(r,z) = \mathcal{O}(r)$。

在有限元实现中，这一要求通过以下两条措施来满足：
1.  **几何约束**：将位于[对称轴](@entry_id:177299)上的所有节点的[径向坐标](@entry_id:165186) $r_i$ 严格设为 0。
2.  **运动学约束**：对位于对称轴上的所有节点，将其径向位移自由度 $u_{ri}$ 约束为 0，这通常作为[本质边界条件](@entry_id:173524)施加。[@problem_id:3502283]

这些措施确保了 $u_r = \sum N_i u_{ri}$ 在 $r \to 0$ 时与 $r$ 具有相同的趋近于零的速率，从而使得比值 $u_r/r$ 保持有限。同时，它也解决了[刚度矩阵](@entry_id:178659)积分的奇异性问题。[单元刚度矩阵](@entry_id:139369)的被积函数包含 $\boldsymbol{B}^T \boldsymbol{D} \boldsymbol{B} (2\pi r)$ 这样的项。$\boldsymbol{B}$ 矩阵中包含 $1/r$ 项，会导致 $\boldsymbol{B}^T \boldsymbol{D} \boldsymbol{B}$ 中出现 $(1/r)^2$ 项。若不加处理，与积分权重中的 $r$ 相乘后，被积函数仍含有 $1/r$ 项，导致积分发散。通过施加 $u_{ri}=0$ 的约束，与奇异的 $N_i/r$ (对于轴上节点 $i$) 相乘的自由度为零，从而消除了发散项，保证了[积分的收敛](@entry_id:187300)性。

在[数值积分](@entry_id:136578)策略上，标准的高斯-勒让德 (Gauss-Legendre) 求积方案的积分点总是位于积分区间的内部，即对于 $[0, r_b]$ 的积分，所有[高斯点](@entry_id:170251)都满足 $r_g  0$。这天然地避免了在 $r=0$ 处对奇异项进行求值，是一种稳健的做法。[@problem_id:3502278]

### 边界条件的施加

与其它有限元分析类似，[轴对称](@entry_id:173333)问题中的边界条件分为[本质边界条件](@entry_id:173524)（位移）和自然边界条件（力）。

[本质边界条件](@entry_id:173524)，如固定位移或前述的对称轴约束 $u_r=0$，通过直接对节点自由度向量 $\boldsymbol{d}$ 中的相应分量进行约束来实现。

自然边界条件，即作用在物体边界上的[分布](@entry_id:182848)力（面力），通过计算其等效的节点力矢量来施加。考虑作用在边界 $\Gamma_t$ 上的[面力矢量](@entry_id:189429) $\boldsymbol{t} = \begin{pmatrix} t_r  t_z \end{pmatrix}^T$。其贡献的[虚功](@entry_id:176403)为 $\int_{S_t} \delta\boldsymbol{u}^T \boldsymbol{t} \, dS$，其中 $S_t$ 是三维旋转[曲面](@entry_id:267450)。三维[曲面](@entry_id:267450)微元 $dS$ 与 $r-z$ 平面内的线微元 $d\Gamma$ 的关系是 $dS = 2\pi r \, d\Gamma$。因此，等效节点力矢量 $\boldsymbol{f}^t$ 的计算公式为：
$$
\boldsymbol{f}^t = \int_{\Gamma_t} \boldsymbol{N}^T \boldsymbol{t} \, (2\pi r) \, d\Gamma
$$
其中 $\boldsymbol{N}$ 是边界上的形函数矩阵。该积分沿 $r-z$ 平面内的边界线进行，同样需要通过高斯求积进行数值计算。[@problem_id:3502234]

### 高级主题：[体积锁定](@entry_id:172606)

在分析[近不可压缩材料](@entry_id:752388)时，例如模拟饱和土在不排水条件下的快速加载，[轴对称单元](@entry_id:163652)可能会遇到**[体积锁定](@entry_id:172606) (volumetric locking)** 的问题。在这种情况下，材料的有效泊松比 $\nu_u$ 趋近于 $0.5$，体积几乎不可压缩，即[体积应变](@entry_id:267252) $\varepsilon_v = \varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta} \approx 0$。

对于低阶的、纯位移格式的有限元单元（如四节点双线性单元），如果采用完全积分（例如 $2 \times 2$ 高斯积分），在每个积分点上施加的 $\varepsilon_v = 0$ 约束过多。单元的位移模式（运动自由度）不足以在满足所有这些约束的同时还能自由变形。这导致单元表现出虚假的、过高的体积刚度，即“锁定”。其后果是：计算出的应力远高于实际值，而位移则远小于实际值。[@problem_id:3502251]

解决[体积锁定](@entry_id:172606)的一种有效方法是采用**混合位移-压力 ($u-p$) 公式**。该方法将[孔隙水压力](@entry_id:753587) $p$ 作为独立的未知场引入，与[位移场](@entry_id:141476) $u$ 同时求解。这有效地将体积约束从强制的逐点满足转变为在积分意义下的弱满足。然而，混合公式的位移和压力[插值函数](@entry_id:262791)空间必须满足特定的[兼容性条件](@entry_id:201103)，即 **LBB (Ladyzhenskaya–Babuška–Brezzi) 稳定条件**，否则会导致压力的虚假振荡（棋盘格现象）。

例如，采用[双线性](@entry_id:146819)位移和双线性压力插值（等阶插值）的单元是不满足[LBB条件](@entry_id:746626)的，会产生不稳定的压力解。而采用双线性位移和分片常数压力，并辅以适当的稳定化技术，或者采用对[位移场](@entry_id:141476)进行特定增强（如[气泡函数](@entry_id:176111)）的单元，则可以构建出稳定且能有效避免[体积锁定](@entry_id:172606)的[轴对称单元](@entry_id:163652)。这些稳定的混合单元对于准确模拟饱和岩土材料的不排水行为至关重要。[@problem_id:3502251]