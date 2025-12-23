## 引言
在计算燃烧学领域，对火焰、爆轰等[复杂反应](@entry_id:166407)流现象进行高保真模拟是推动科学认知与工程设计的关键。然而，这些流动现象内蕴的物理过程极其复杂，往往包含激波等不连续结构、跨越数个数量级的时间与空间尺度，以及强[非线性](@entry_id:637147)的化学反应，为[数值模拟](@entry_id:146043)带来了巨大挑战。传统的数值方法在同时保证[高阶精度](@entry_id:750325)、几何灵活性和数值稳定性方面常常捉襟见肘。间断Galerkin (DG) 方法和格子Boltzmann (LBM) 方法作为两类强大的先进数值工具，正是在应对这些挑战中脱颖而出，为反应流的精细化模拟提供了可能。

本文旨在系统性地介绍如何应用DG和LBM来求解反应流问题。我们首先要解决的核心知识鸿沟在于，如何将这两种截然不同的离散方法（分别为基于有限元的DG和基于动力学理论的LBM）应用于统一的反应流控制方程，并处理其中固有的数值难题，特别是[化学刚性](@entry_id:1122356)问题。

通过本文的学习，读者将全面掌握这两种方法的原理与实践。在“原理与机制”一章中，我们将建立[反应流](@entry_id:190741)的控制方程，并深入剖析DG和LBM如何离散对流、扩散和[化学源项](@entry_id:747323)。接着，在“应用与交叉学科联系”一章，我们将展示这些方法在模拟层流火焰、[爆轰波](@entry_id:1123609)等典型燃烧现象中的具体应用，并探讨其与高性能计算等领域的交叉。最后，“动手实践”部分将提供精选的编程练习，帮助读者将理论知识转化为实际的计算能力，从而真正驾驭这两种强大的计算工具。

## 原理与机制

本章旨在阐述用于模拟反应流的间断Galerkin（DG）方法和[格子Boltzmann方法](@entry_id:142209)（LBM）的核心科学原理与数值机制。我们将首先建立描述多组分反应流的控制方程，然后分别深入探讨DG和LBM如何离散这些方程，最后讨论处理化学反应所带来的[数值刚性](@entry_id:752836)这一共通挑战。

### [反应流](@entry_id:190741)的数学模型

任何[计算模拟](@entry_id:146373)的第一步都是建立一个能够准确描述相关物理现象的数学模型。对于反应流，该模型由一组[偏微分](@entry_id:194612)方程（PDEs）构成，即[反应流](@entry_id:190741)[Navier-Stokes](@entry_id:276387)方程。

#### 控制方程的[守恒形式](@entry_id:1122899)

为了确保在数值离散中物理量的守恒性（如质量、动量和能量），我们将控制方程写成严格的[守恒形式](@entry_id:1122899)。对于一个包含 $N_s$ 个组分的可压缩[反应气体](@entry_id:754126)混合物，其状态可以用一个状态向量 $\boldsymbol{U}$ 来描述。方程的一般形式为：
$$
\partial_t \boldsymbol{U} + \nabla \cdot \boldsymbol{F}^c(\boldsymbol{U}) = \nabla \cdot \boldsymbol{F}^v(\boldsymbol{U}, \nabla \boldsymbol{U}) + \boldsymbol{S}(\boldsymbol{U}, T)
$$
其中，$\partial_t$ 表示对时间的[偏导数](@entry_id:146280)，$\nabla \cdot$ 表示[散度算子](@entry_id:265975)。$\boldsymbol{F}^c$ 是对流通量，$\boldsymbol{F}^v$ 是黏性/[扩散通量](@entry_id:748422)，$\boldsymbol{S}$ 是源项。

对于三维流动，这些向量和张量的具体形式如下：

**状态向量** $\boldsymbol{U}$ 包含了所有守恒变量的密度：
$$
\boldsymbol{U} = \begin{bmatrix} \rho \\ \rho \mathbf{u} \\ \rho E \\ \rho Y_1 \\ \vdots \\ \rho Y_{N_s} \end{bmatrix}
$$
这里，$\rho$ 是混合物的总密度，$\mathbf{u}$ 是[质量平均速度](@entry_id:149575)向量，$\rho \mathbf{u}$ 是[动量密度](@entry_id:271360)，$\rho E$ 是总能量密度，$Y_k$ 是组分 $k$ 的质量分数，$\rho Y_k$ 是组分 $k$ 的质量密度。总能量 $E = e + \frac{1}{2} |\mathbf{u}|^2$，由内能 $e$ 和动能组成。

**对流通量** $\boldsymbol{F}^c(\boldsymbol{U})$ 描述了由流体宏观运动引起的[守恒量](@entry_id:161475)输运：
$$
\boldsymbol{F}^c(\boldsymbol{U}) = \begin{bmatrix}
\rho \mathbf{u} \\
\rho \mathbf{u} \otimes \mathbf{u} + p \mathbf{I} \\
(\rho E + p) \mathbf{u} \\
\rho Y_1 \mathbf{u} \\
\vdots \\
\rho Y_{N_s} \mathbf{u}
\end{bmatrix}
$$
其中，$p$ 是压力，$\mathbf{I}$ 是单位张量，$\otimes$ 表示[张量积](@entry_id:140694)。压力 $p$ 通过[理想气体混合物](@entry_id:149212)[状态方程](@entry_id:274378) $p = \rho R_{\text{mix}} T$ 与其他状态变量关联，其中 $R_{\text{mix}} = \sum_{k=1}^{N_s} Y_k R_k$ 是混合气体常数。

**黏性通量** $\boldsymbol{F}^v(\boldsymbol{U}, \nabla \boldsymbol{U})$ 代表了由[分子扩散](@entry_id:154595)引起的动量、能量和质量的输运。与对流项不同，这些通量依赖于状态变量的梯度：
$$
\boldsymbol{F}^v(\boldsymbol{U}, \nabla \boldsymbol{U}) = \begin{bmatrix}
\mathbf{0} \\
\boldsymbol{\tau} \\
\boldsymbol{\tau} \cdot \mathbf{u} - \mathbf{q} - \sum_{k=1}^{N_s} h_k \mathbf{J}_k \\
-\mathbf{J}_1 \\
\vdots \\
-\mathbf{J}_{N_s}
\end{bmatrix}
$$
这里的负号源于将扩散项移至方程右侧并保持散度算子形式的约定。各项定义如下：
- $\boldsymbol{\tau}$ 是黏性应力张量，对于牛顿流体，它与[速度梯度](@entry_id:261686) $\nabla \mathbf{u}$ 成正比。
- $\mathbf{q}$ 是热通量向量，通常由傅里叶定律 $\mathbf{q} = -k \nabla T$ 描述，其中 $k$ 是热导率。
- $\mathbf{J}_k$ 是组分 $k$ 的扩散质量通量，它描述了由于浓度梯度引起的组分相对运动。
- $\sum_{k=1}^{N_s} h_k \mathbf{J}_k$ 是一项关键的能量输运项，代表了由于组分扩散所携带的焓（$h_k$ 是组分 $k$ 的比焓）的输运。在多组分[反应流](@entry_id:190741)中忽略此项会导致严重的能量不守恒。

**源项** $\boldsymbol{S}(\boldsymbol{U}, T)$ 包含了体积力（如重力）和化学反应的贡献：
$$
\boldsymbol{S}(\boldsymbol{U}, T) = \begin{bmatrix}
0 \\
\rho \mathbf{f} \\
\rho \mathbf{u} \cdot \mathbf{f} \\
\dot{\omega}_1 \\
\vdots \\
\dot{\omega}_{N_s}
\end{bmatrix}
$$
其中 $\mathbf{f}$ 是单位质量的体积力，$\dot{\omega}_k$ 是组分 $k$ 的单位体积[质量生成](@entry_id:161427)率，它直接来源于化学反应。

#### 对流系统的双曲性

控制方程中的对流部分（即无黏、无扩散的[欧拉方程](@entry_id:177914)）决定了信息在流场中的传播方式。为了理解这一点，我们考虑一维无黏反应欧拉子系统。其通量[雅可比矩阵](@entry_id:178326) $\boldsymbol{A}(\boldsymbol{U}) = \partial \boldsymbol{F}^c / \partial \boldsymbol{U}$ 的特征值决定了系统的[特征速度](@entry_id:165394)。对于包含一个示踪组分（如[反应进度](@entry_id:140591)变量）的系统，其状态向量为 $\boldsymbol{U} = [\rho, \rho u, E, \rho Y]^{\top}$，通量[雅可比矩阵的特征值](@entry_id:264008)为：
$$
\lambda \in \{u-c, u, u, u+c\}
$$
这些特征值都是实数，前提是声速 $c$ 是实数。声速由 $c^2 = \gamma p / \rho$ 给出，其中 $\gamma$ 是比热比。在物理上合理的条件下（$\rho > 0, p \ge 0, \gamma > 1$），$c^2 \ge 0$ 成立，因此特征值均为实数。这证明了[欧拉方程组](@entry_id:143098)是**双曲型**的。

双曲性意味着解以有限速度（[特征速度](@entry_id:165394)）传播的波的形式存在。具体来说，$u \pm c$ 对应于声波，而两个[重根](@entry_id:151486) $u$ 对应于随流体移动的接触间断（携带熵和组分信息）。这一特性是发展如DG等迎风[类数](@entry_id:156164)值格式的理论基础，这些格式通过求解界面上的黎曼问题来捕捉波的传播。

#### 化学源项

化学反应是反应流的核心。源项 $\dot{\omega}_k$ 描述了化学反应如何改变各组分的质量分数。对于一组元反应 $\sum_j \nu_{j,r}' X_j \rightleftharpoons \sum_j \nu_{j,r}'' X_j$，其中 $X_j$ 是组分，$ \nu_{j,r}'$ 和 $\nu_{j,r}''$ 分别是反应物和产物的化学计量系数，其[质量生成](@entry_id:161427)率可以根据[质量作用定律](@entry_id:916274)推导得出。

组分 $k$ 的单位体积摩尔生成率 $\dot{c}_k$ 是所有反应 $r$ 对其贡献的总和：
$$
\dot{c}_k = \sum_{r} \nu_{k,r} q_r = \sum_{r} (\nu_{k,r}'' - \nu_{k,r}') \left(k_{f,r} \prod_{j} C_{j}^{\nu_{j,r}'} - k_{b,r} \prod_{j} C_{j}^{\nu_{j,r}''}\right)
$$
其中，$\nu_{k,r} = \nu_{k,r}'' - \nu_{k,r}'$ 是净化学计量系数，$q_r$ 是反应 $r$ 的净摩尔[反应速率](@entry_id:185114)，$k_{f,r}$ 和 $k_{b,r}$ 分别是正向和逆向反应速率常数，$C_j$ 是组分 $j$ 的[摩尔浓度](@entry_id:1128100)。

要得到[质量生成](@entry_id:161427)率 $\dot{\omega}_k$（单位：$\mathrm{kg}\cdot\mathrm{m}^{-3}\cdot\mathrm{s}^{-1}$），我们只需将摩尔生成率乘以组分 $k$ 的[摩尔质量](@entry_id:146110) $W_k$：
$$
\dot{\omega}_k = W_k \dot{c}_k = W_k \sum_{r} \nu_{k,r} \left(k_{f,r} \prod_{j} C_{j}^{\nu_{j,r}'} - k_{b,r} \prod_{j} C_{j}^{\nu_{j,r}''}\right)
$$
这个表达式是连接宏观流体动力学和微观[化学动力学](@entry_id:144961)的桥梁，是反应流模拟中至关重要的一环。

### 基于[间断Galerkin方法](@entry_id:748369)的离散

间断Galerkin（DG）方法是一类高阶有限元方法，特别适用于求解双曲型守恒律。其核心思想是在不连续的[多项式空间](@entry_id:144410)中寻找数值解。

#### 核心原理：弱形式与单元离散

[DG方法](@entry_id:748369)首先将计算域 $\Omega$ 剖分为互不重叠的单元 $\mathcal{T}_h$。在每个单元 $K$ 内部，解 $u_h$ 和检验函数 $\varphi_h$ 都被表示为多项式。与连续有限元不同，DG允许解在单元边界上是不连续的。

对于一个[标量守恒律](@entry_id:754532) $\partial_t u + \nabla \cdot \boldsymbol{f}(u) = s(u)$，我们将其乘以一个[检验函数](@entry_id:166589) $\varphi_h$，并在单元 $K$ 上积分，得到其弱形式。对通量项使用分部积分（[格林公式](@entry_id:173118)），我们得到：
$$
\int_K (\partial_t u_h) \varphi_h \, \mathrm{d}V - \int_K \boldsymbol{f}(u_h) \cdot \nabla \varphi_h \, \mathrm{d}V + \int_{\partial K} (\boldsymbol{f}(u_h) \cdot \boldsymbol{n}_K) \varphi_h \, \mathrm{d}S = \int_K s(u_h) \varphi_h \, \mathrm{d}V
$$
其中 $\boldsymbol{n}_K$ 是单元 $K$ 的外法向向量。

#### 处理[对流通量](@entry_id:158187)：界面上的数值通量

由于解在单元界面 $F$ 上是双值的（从单元 $K^-$ 逼近得到 $u^-$，从 $K^+$ 逼近得到 $u^+$），边界积分项中的物理通量 $\boldsymbol{f}(u_h) \cdot \boldsymbol{n}_K$ 没有唯一定义。[DG方法](@entry_id:748369)通过引入一个单值的**[数值通量](@entry_id:145174)** $\widehat{\boldsymbol{f}}(u_h^-, u_h^+)$ 来解决这个问题。

为了方便地表示界面上的量，我们定义**平均**和**跳跃**算子。对于一个在界面 $F$ 上具有左右值 $v^-$ 和 $v^+$ 的标量 $v$，其平均值为 $\{v\} = (v^- + v^+)/2$，跳跃值为 $\llbracket v \rrbracket = v^- - v^+$（注意：跳跃的定义有多种约定）。

一个简单而有效的数值通量是**Lax-Friedrichs通量**，它通过添加一个正比于解的跳跃的[数值耗散](@entry_id:168584)项来稳定格式：
$$
\widehat{\boldsymbol{f}}(u^-, u^+) \cdot \boldsymbol{n} = \{\boldsymbol{f}(u)\} \cdot \boldsymbol{n} - \frac{\lambda_F}{2}(u^+ - u^-) = \{\boldsymbol{f}(u)\} \cdot \boldsymbol{n} + \frac{\lambda_F}{2}\llbracket u \rrbracket
$$
其中 $\lambda_F$ 是一个稳定化参数，通常取为界面两侧法向特征速度绝对值的最大值。

对于[欧拉方程组](@entry_id:143098)这样更复杂的系统，需要更精细的[数值通量](@entry_id:145174)，即[近似黎曼求解器](@entry_id:267136)。
- **[Roe通量](@entry_id:754409)**：通过求解一个线性化的[黎曼问题](@entry_id:171440)来构造，该线性化在特殊构造的**[Roe平均](@entry_id:754407)**状态下进行。它能够精确解析线性间断，但可能需要[熵修正](@entry_id:749021)。对于多组分气体，[Roe平均](@entry_id:754407)速度、焓和质量分数通常使用 $\sqrt{\rho}$ 进行加权。
- **[HLL通量](@entry_id:750354)**（Harten-Lax-van Leer）：这是一个更稳健但更耗散的两波模型，它只考虑最左和最右的声波，将中间的所有波（包括接触间断）压缩到一个区域。因此，它会数值地模糊[接触间断](@entry_id:194702)，这对于需要精确追踪[组分输运](@entry_id:1132066)的[反应流](@entry_id:190741)来说是一个缺点。
- **[HLLC通量](@entry_id:750350)**（Harten-Lax-van Leer-Contact）：这是HLL格式的改进，它在HLL的两波模型中重新引入了接触波。这使得HLLC能够精确地（无耗散地）捕捉接触间断和线性平流的组分场，因此在模拟多组分反应流中通常是比HLL更好的选择。

#### 处理黏性通量：Bassi–Rebay 2 (BR2) 格式

黏性项涉及解的二阶导数，这给[DG方法](@entry_id:748369)带来了挑战。直接应用两次分部积分会引入梯度的跳跃，导致格式不稳定或不对称。Bassi和Rebay提出了几种格式来解决这个问题，其中BR2格式因其对称性和紧凑性而广受欢迎。

BR2格式的核心思想是引入一个**[提升算子](@entry_id:751273)** $\mathbf{r}_e$。这个算子将界面 $e$ 上的标量函数（如解的跳跃 $[u_h]$）“提升”为一个定义在相邻单元上的向量场。该算子通过变分形式定义。

BR2格式的黏性[双线性形式](@entry_id:746794) $a_{\mathrm{BR2}}(u_h, v_h)$ 由三部分组成：
1.  标准的体积积分项：$\sum_{K} \int_K \kappa \, \nabla u_h \cdot \nabla v_h \, \mathrm{d}x$
2.  对称的[界面耦合](@entry_id:750728)项：$- \sum_{e} \int_e \kappa (\{\nabla u_h\} \cdot \mathbf{n}_e [v_h] + \{\nabla v_h\} \cdot \mathbf{n}_e [u_h]) \, \mathrm{d}s$
3.  基于[提升算子](@entry_id:751273)的[罚函数](@entry_id:638029)项：$\sum_{e} \eta_e \sum_{K \in \mathcal{N}(e)} \int_K \kappa \, \mathbf{r}_e([u_h]) \cdot \mathbf{r}_e([v_h]) \, \mathrm{d}x$

[罚函数](@entry_id:638029)项是一个体积积分，它惩罚了界面上解的跳跃。由于它是通过[提升算子](@entry_id:751273)得到的向量场的[内积](@entry_id:750660)形式，因此这个[罚函数](@entry_id:638029)项天然是对称的，从而保证了整个[双线性形式](@entry_id:746794)的对称性。通过适当地选择罚参数 $\eta_e$，可以保证格式的稳定性和收敛性。

#### 处理源项：求积与混淆误差

在[DG弱形式](@entry_id:748377)中，源项以体积积分 $\int_K s(u_h) \varphi_h \, \mathrm{d}V$ 的形式出现。在实际计算中，这个积分通常采用高斯数值求积来近似。然而，当源项 $s(u)$ 是[非线性](@entry_id:637147)时（例如，[化学反应速率](@entry_id:147315)常常是温度和浓度的[非线性](@entry_id:637147)函数），这会引入**混淆误差**（aliasing error）。

考虑一个 $p$ 次多项式解 $c_h \in \mathbb{P}_p$ 和一个源项 $\omega(c)=c^m$。弱形式中的被积函数 $\omega(c_h)\varphi_h = (c_h)^m \varphi_h$ 的次数为 $(m+1)p$。标准的[高斯求积](@entry_id:146011)（$N_q = p+1$ 个点）只能精确积分到 $2p+1$ 次的多项式。当 $(m+1)p > 2p+1$ 时，求积就会不精确，产生的误差会污染所有模式，可能导致数值不稳定。例如，对于 $p=2, \omega(c)=c^2$，被积函数次数为 $6$，而 $N_q=3$ 的求积只能精确到 $5$ 次，从而产生一个大小为 $-27/175$ 的误差。

有两种主要策略来控制混淆误差：
1.  **过积分**（Over-integration）：使用比标准更多的求积点，即选择 $N_q$ 使得 $2N_q - 1 \ge (m+1)p$。这种方法简单直接，但计算成本更高。
2.  **分裂形式/投影策略**：在计算弱形式积分之前，先将[非线性](@entry_id:637147)的源项 $\omega(c_h)$ 在 $L^2$ 意义下**投影**回[多项式空间](@entry_id:144410) $\mathbb{P}_p$。记投影为 $\mathcal{I}_p(\omega(c_h))$。然后计算积分 $\int_K \mathcal{I}_p(\omega(c_h)) \varphi_h \, \mathrm{d}V$。此时，被积函数的次数最高为 $2p$，因此使用标准的 $N_q = p+1$ 个求积点就足以精确计算，从而消除了混淆误差。

### 基于[格子Boltzmann方法](@entry_id:142209)的离散

[格子Boltzmann方法](@entry_id:142209)（LBM）是一种介于宏观流体动力学和微观分子动力学之间的介观方法。它不直接求解Navier-Stokes方程，而是求解一个简化的[Boltzmann方程](@entry_id:138866)——格子Boltzmann方程。

#### 核心原理：从动力学理论到流体力学

LBM的核心是粒子**分布函数** $f_i(\mathbf{x}, t)$，它表示在位置 $\mathbf{x}$、时间 $t$ 沿离散速度方向 $\mathbf{c}_i$ 运动的粒子密度。LBM的演化过程包括两个步骤：
1.  **碰撞**（Collision）：在每个格点上，[分布函数](@entry_id:145626)向局部平衡态 $f_i^{\mathrm{eq}}$ 松弛。
2.  **迁移**（Streaming）：粒子沿其各自的速度方向移动到相邻的格点。

宏观流[体力](@entry_id:174230)学量，如密度 $\rho$ 和动量 $\rho \mathbf{u}$，可以通过计算[分布函数的矩](@entry_id:1128117)来恢复：
$$
\rho = \sum_i f_i, \quad \rho \mathbf{u} = \sum_i \mathbf{c}_i f_i
$$
通过[Chapman-Enskog展开](@entry_id:136379)可以证明，在低马赫数极限下，LBM能够恢复Navier-Stokes方程。

#### 等温LBM框架

一个标准的LBM模型是**[D2Q9模型](@entry_id:1123349)**，用于二维（D2）模拟，包含九个（Q9）离散速度。其离散速度集 $\mathbf{c}_i$ 包括静止粒子、沿坐标轴和沿对角线方向运动的粒子。每个速度都关联一个特定的**权重** $w_i$。对于[D2Q9模型](@entry_id:1123349)，标准权重为 $w_0=4/9$（静止），$w_{1-4}=1/9$（轴向），$w_{5-8}=1/36$（对角）。

碰撞过程通常采用Bhatnagar-Gross-Krook (BGK) 近似，它假设分布函数以单一的松弛时间 $\tau$ 向**[平衡分布](@entry_id:263943)函数** $f_i^{\mathrm{eq}}$ 松弛。对于等温流动，[二阶精度](@entry_id:137876)的[平衡分布](@entry_id:263943)函数为：
$$
f_i^{\mathrm{eq}} = w_i \rho \left[ 1 + \frac{\mathbf{c}_i \cdot \mathbf{u}}{c_s^2} + \frac{(\mathbf{c}_i \cdot \mathbf{u})^2}{2c_s^4} - \frac{\mathbf{u} \cdot \mathbf{u}}{2c_s^2} \right]
$$
其中 $c_s$ 是格子声速，对于标准的[D2Q9模型](@entry_id:1123349)，它与格子速度 $c=\Delta x/\Delta t$ 的关系为 $c_s^2=c^2/3$。这个关系是确保从LBM恢复的宏观方程具有正确各向同性的关键。

#### 在LBM中引入反应源项

为了模拟[反应流](@entry_id:190741)，需要将化学反应的源项（如热量释放或组分生成）引入LBM框架。这通常通过在LBM演化方程中添加一个**力项**或**源项** $\Phi_i$ 来实现。
$$
g_i(\mathbf{x}+\mathbf{c}_i \Delta t, t+\Delta t) - g_i(\mathbf{x},t) = -\frac{1}{\tau_g}\left[g_i(\mathbf{x},t)-g_i^{\mathrm{eq}}(\mathbf{x},t)\right] + \Delta t \Phi_i(\mathbf{x},t)
$$
（这里我们用 $g_i$ 代表[热LBM](@entry_id:755891)的分布函数）

为了使LBM在宏观上正确地再现源项（例如，能量方程中的热释放率 $\dot{Q}$），动力学源项 $\Phi_i$ 的矩必须满足特定条件。最简单的要求是其零阶矩等于宏观源项：$\sum_i \Phi_i = \dot{Q}$。然而，这种简单的处理方式在时间上只有[一阶精度](@entry_id:749410)。

为了达到二阶时间精度，需要采用更精细的格式，如**Guo力格式**。该格式通过引入一个修正因子来补偿碰撞和源项在一个时间步内的相互作用。施加的动力学源项 $S_i$ 变为 $S_i = (1 - \frac{1}{2\tau_g})\Phi_i$，其中 $\Phi_i$ 满足[矩条件](@entry_id:136365) $\sum_i \Phi_i = \dot{Q}$ 和 $\sum_i \mathbf{c}_i \Phi_i = \mathbf{0}$（假设源项在动力学层面是各向同性的）。这样可以确保恢复的宏观方程中的源项是 $\dot{Q}$，且误差为 $O(\Delta t^2)$。

### [化学刚性](@entry_id:1122356)带来的挑战

在许多燃烧问题中，化学反应的时间尺度远小于流体输运的时间尺度。这种多尺度特性导致了所谓的**[数值刚性](@entry_id:752836)**，这是[反应流](@entry_id:190741)模拟中的一个核心挑战。

#### 刚性的来源与量化

[化学反应速率](@entry_id:147315)通常由**[Arrhenius定律](@entry_id:261434)**描述：$k_f = A T^n \exp(-E_a/(RT))$。由于活化能 $E_a$ 通常很大，反应速率常数 $k_f$ 对温度表现出极强的指数敏感性。这意味着温度的微小变化可能导致[反应速率](@entry_id:185114)和化学时间尺度 $\tau_{\mathrm{chem}} \approx 1/k_f$ 的数量级变化。

例如，对于一个典型的反应，温度从 $1000\,\mathrm{K}$ 升高到 $1050\,\mathrm{K}$（仅 $5\%$ 的增幅），化学时间尺度 $\tau_{\mathrm{chem}}$ 可能会减半，从 $6.86 \times 10^{-6}\,\mathrm{s}$ 降至 $3.21 \times 10^{-6}\,\mathrm{s}$。

这种时间尺度的悬殊差异可以用无量纲的**[Damköhler数](@entry_id:151890)** ($Da$) 来量化，它定义为流动时间尺度与化学时间尺度之比：$Da = \tau_{\mathrm{flow}} / \tau_{\mathrm{chem}}$。当 $Da \gg 1$ 时，化学反应非常快，系统就呈现出刚性。

#### 针对[刚性系统](@entry_id:146021)的[算子分裂](@entry_id:634210)

对于[刚性系统](@entry_id:146021)，如果使用标准的显式时间积分格式，其[稳定时间步长](@entry_id:755325)将受到最快的化学时间尺度的限制，即 $\Delta t \lesssim \tau_{\mathrm{chem}}$。这对于模拟宏观流动现象来说是不可接受的，因为流动时间尺度要大得多。

解决这个问题的标准方法是**算子分裂**。其思想是将控制方程的演化[算子分解](@entry_id:154443)为输运部分 $\mathcal{L}_{\text{transport}}$ 和反应部分 $\mathcal{R}_{\text{reaction}}$，然后在每个时间步内分别求解。
$$
\frac{d\boldsymbol{U}}{dt} = (\mathcal{L}_{\text{transport}} + \mathcal{R}_{\text{reaction}})\boldsymbol{U}
$$
一个常用的分裂格式是**[Strang分裂](@entry_id:755497)**，它具有二阶精度：
1.  输运半步：使用DG或LBM方法推进解，时间步长为 $\Delta t/2$。
2.  反应全步：在每个空间点上，[求解常微分方程组](@entry_id:173311) $d\boldsymbol{U}/dt = \boldsymbol{S}(\boldsymbol{U})$，时间步长为 $\Delta t$。由于此步是刚性的，必须使用**[刚性ODE求解器](@entry_id:203847)**（如隐式欧拉或更高阶的[隐式方法](@entry_id:138537)）。
3.  输运半步：再次使用DG或LBM方法推进解，时间步长为 $\Delta t/2$。

通过这种方式，输运部分（通常是非刚性的）可以采用显式或半显式方法，而刚性的化学反应部分则由专门的稳定求解器处理。这使得整个模拟的时间步长可以由流动本身的精度要求（如CFL条件）来决定，而不是被极快的化学反应所束缚，从而极大地提高了计算效率。这一策略对于DG和LBM等方法在应用于刚性[反应流](@entry_id:190741)模拟时都是必不可少的。