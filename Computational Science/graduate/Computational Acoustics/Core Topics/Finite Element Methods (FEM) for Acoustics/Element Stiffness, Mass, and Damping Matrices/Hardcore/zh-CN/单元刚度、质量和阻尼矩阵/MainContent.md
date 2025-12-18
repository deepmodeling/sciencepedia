## 引言
在计算声学领域，有限元法（FEM）是一种强大而通用的数值工具，能够[精确模拟](@entry_id:749142)复杂几何形状和材料中的声波传播与相互作用。这种方法的核心在于将连续的物理问题（如波动方程）离散化为[代数方程](@entry_id:272665)组，而构成这个系统的基本构件正是单元刚度、质量和阻尼矩阵。这些矩阵不仅是数学上的抽象符号，更是物理[系统弹性](@entry_id:1132834)、惯性和能量耗散特性的直接体现。

然而，许多学习者和工程师往往在理解这些矩阵的物理起源、数学构建及其对最终仿真结果的深远影响之间存在鸿沟。例如，它们是如何从一个[偏微分](@entry_id:194612)方程中产生的？为什么需要复杂的[数值积分](@entry_id:136578)？集总质量和一致质量有何区别？沙漏模态又是如何出现的？解答这些问题对于有效运用有限元软件、诊断数值问题以及开发新的[计算模型](@entry_id:637456)至关重要。

本文旨在系统性地填补这一空白，为读者提供一份关于单元刚度、质量和阻尼矩阵的全面指南。在**“原理与机制”**一章中，我们将从[波动方程](@entry_id:139839)的[弱形式](@entry_id:142897)出发，详细推导这些矩阵的定义，并深入探讨[等参映射](@entry_id:173239)、[数值求积](@entry_id:136578)、矩阵集总以及沙漏模态等关键计算细节。接下来，在**“应用与交叉学科联系”**一章中，我们将展示这些基本构件如何在[声学模态分析](@entry_id:1127997)、阻尼建模、流固耦合以及完美匹配层（PML）等实际应用中发挥作用，揭示其与[结构动力学](@entry_id:172684)、材料科学等领域的深刻联系。最后，通过**“动手实践”**环节，你将有机会将理论付诸实践，通过编程练习来构建、组装和应用这些矩阵，从而真正巩固所学知识。

## 原理与机制

在计算声学中，[有限元法](@entry_id:749389) (Finite Element Method, FEM) 通过将连续的控制方程（如波动方程）转化为一个离散的[代数方程](@entry_id:272665)组，从而实现数值求解。这一转化的核心在于将求解域离散为一系列单元，并在每个单元上构建局部近似。本章将深入探讨构成这一离散系统的基本构件：**[单元刚度矩阵](@entry_id:139369)**、**质量矩阵**和**阻尼矩阵**。我们将从其物理和数学起源出发，详细阐述其计算方法、关键性质，以及它们如何共同决定整个数值模型的精度、稳定性和计算效率。

### 从弱形式到单元矩阵

有限元系统的矩阵形式源于控制[偏微分](@entry_id:194612)方程的**[弱形式](@entry_id:142897)** (weak form)。以一个非均匀、[无粘性流体](@entry_id:198262)中的[线性声学](@entry_id:1127264)问题为例，其压[力场](@entry_id:147325) $p(\boldsymbol{x},t)$ 满足如下变系数[波动方程](@entry_id:139839)：

$$
\nabla \cdot \left(\frac{1}{\rho(\boldsymbol{x})}\nabla p(\boldsymbol{x},t)\right) - \frac{1}{K(\boldsymbol{x})}\,\frac{\partial^2 p(\boldsymbol{x},t)}{\partial t^2} = 0
$$

其中 $\rho(\boldsymbol{x})$ 是介质密度，$K(\boldsymbol{x})$ 是体积模量。

通过伽辽金法 (Galerkin method)，我们将该方程乘以一个**测试函数** (test function) $w(\boldsymbol{x})$ 并在求解域 $\Omega$ 上积分。利用[分部积分](@entry_id:136350)（[格林第一恒等式](@entry_id:170345)）并将边界条件（例如，刚性壁边界 $\boldsymbol{n}\cdot(\frac{1}{\rho}\nabla p)=0$）代入后，可得到如下的弱形式方程：

$$
\int_{\Omega} \frac{1}{K}\,w\,\frac{\partial^2 p}{\partial t^2} \,dV + \int_{\Omega} \frac{1}{\rho} \nabla w \cdot \nabla p \,dV = 0
$$

在[有限元法](@entry_id:749389)中，我们将待求的压[力场](@entry_id:147325) $p$ 和测试函数 $w$ 在每个单元 $\Omega_e$ 内用一组**形函数** (shape functions) $\{N_a(\boldsymbol{x})\}$ 进行近似展开，$p(\boldsymbol{x},t) \approx \sum_b N_b(\boldsymbol{x})\hat{p}_b(t)$，其中 $\hat{p}_b(t)$ 是节点上的压力值。将此近似代入弱形式，并令测试函数 $w$ 依次等于每个形函数 $N_a$，我们便可得到一个关于节点未知数的[半离散化](@entry_id:163562)[常微分方程组](@entry_id:907499)：

$$
\mathbf{M}\,\ddot{\hat{\boldsymbol{p}}}(t) + \mathbf{K}\,\hat{\boldsymbol{p}}(t) = \boldsymbol{0}
$$

全局的**质量矩阵** $\mathbf{M}$ 和**刚度矩阵** $\mathbf{K}$ 是由各个单元矩阵 $\mathbf{M}_e$ 和 $\mathbf{K}_e$ **组装** (assemble) 而成。这些单元矩阵的各项定义来自于[弱形式](@entry_id:142897)中的积分项  ：

- **[单元质量矩阵](@entry_id:748930)** ($\mathbf{M}_e$):
$$
(M_e)_{ab} = \int_{\Omega_e} \frac{1}{K(\boldsymbol{x})} N_a N_b \,dV
$$
该矩阵与时间的二阶导数项（加速度项）相关，物理上代表了系统的惯性或压缩性储能。

- **[单元刚度矩阵](@entry_id:139369)** ($\mathbf{K}_e$):
$$
(K_e)_{ab} = \int_{\Omega_e} \frac{1}{\rho(\boldsymbol{x})} \nabla N_a \cdot \nabla N_b \,dV
$$
该矩阵与场的空间梯度项相关，物理上代表了系统的弹性或位能。

当系统中存在能量耗散时，还会出现**单元阻尼矩阵** ($\mathbf{C}_e$)，它与时间的[一阶导数](@entry_id:749425)项（速度项）相关。

### [等参映射](@entry_id:173239)与矩阵计算

直接在形状任意的物理单元 $\Omega_e$ 上计算上述积分是十分困难的。因此，有限元法引入了**[等参映射](@entry_id:173239)** (isoparametric mapping) 的概念，将所有计算都转换到一个规则的、统一的**[参考单元](@entry_id:168425)** (reference element) $\hat{\Omega}$ 上进行，例如一个边长为2的立方体或正方形。

这种映射通过形函数本身来定义物理坐标 $\boldsymbol{x}$ 与参考坐标 $\boldsymbol{\xi}$ 之间的关系：$\boldsymbol{x}(\boldsymbol{\xi}) = \sum_a \boldsymbol{x}_a N_a(\boldsymbol{\xi})$。这一转换的关键在于**[雅可比矩阵](@entry_id:178326)** (Jacobian matrix) $\mathbf{J}$，它联系了两个坐标系下的[微分](@entry_id:158422)关系：

$$
\mathbf{J} = \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{\xi}}
$$

雅可比[矩阵的行列式](@entry_id:148198) $J = \det(\mathbf{J})$ 用于转换积分的[体积元](@entry_id:267802)：$dV = J\,d\hat{V}$。更重要的是，它也用于转换[梯度算子](@entry_id:1125719)。根据[链式法则](@entry_id:190743)，物理坐标下的梯度 $\nabla_{\boldsymbol{x}}$ 可以通过[雅可比矩阵](@entry_id:178326)的逆[转置](@entry_id:142115) $\mathbf{J}^{-T}$ 从参考坐标下的梯度 $\nabla_{\boldsymbol{\xi}}$ 得到 ：

$$
\nabla_{\boldsymbol{x}} N_a = \mathbf{J}^{-T} \nabla_{\boldsymbol{\xi}} \hat{N}_a
$$

于是，[单元刚度矩阵](@entry_id:139369)的计算便可在[参考单元](@entry_id:168425)上进行：

$$
(K_e)_{ab} = \int_{\hat{\Omega}} \frac{1}{\rho} (\mathbf{J}^{-T} \nabla_{\boldsymbol{\xi}} \hat{N}_a) \cdot (\mathbf{J}^{-T} \nabla_{\boldsymbol{\xi}} \hat{N}_b) J \,d\hat{\Omega}
$$

**示例：二维[双线性](@entry_id:146819)[四边形单元](@entry_id:176937)的刚度矩阵计算**

考虑一个将参考正方形 $\hat{\Omega}=[-1,1]\times[-1,1]$ 映射到边长为 $L$ 和 $H$ 的物理矩形单元 $\Omega_e$ 的情况。此映射为[仿射变换](@entry_id:144885)：$x=\frac{L}{2}(1+\xi)$，$y=\frac{H}{2}(1+\eta)$。其[雅可比矩阵](@entry_id:178326)为常数对角阵：

$$
\mathbf{J} = \begin{pmatrix} L/2 & 0 \\ 0 & H/2 \end{pmatrix}, \quad J = \det(\mathbf{J}) = \frac{LH}{4}
$$

我们来计算与节点1（对应参考点 $(-1,-1)$）相关的对角项 $(K_e)_{11}$。该节点的形函数为 $\hat{N}_1(\xi,\eta) = \frac{1}{4}(1-\xi)(1-\eta)$。首先计算其在参考坐标下的梯度：

$$
\nabla_{\boldsymbol{\xi}} \hat{N}_1 = \begin{pmatrix} -\frac{1}{4}(1-\eta) \\ -\frac{1}{4}(1-\xi) \end{pmatrix}
$$

然后通过 $\mathbf{J}^{-T}$ 转换为物理梯度。由于 $\mathbf{J}$ 是对角阵，$\mathbf{J}^{-T} = \mathbf{J}^{-1} = \text{diag}(2/L, 2/H)$。

$$
\nabla_{\mathbf{x}} N_1 = \begin{pmatrix} 2/L & 0 \\ 0 & 2/H \end{pmatrix} \begin{pmatrix} -\frac{1}{4}(1-\eta) \\ -\frac{1}{4}(1-\xi) \end{pmatrix} = \begin{pmatrix} -\frac{1}{2L}(1-\eta) \\ -\frac{1}{2H}(1-\xi) \end{pmatrix}
$$

最后，我们将此结果代入积分表达式，并在[参考单元](@entry_id:168425)上进行积分 ：

$$
(K_e)_{11} = \int_{-1}^{1}\int_{-1}^{1} \frac{1}{\rho} |\nabla_{\mathbf{x}} N_1|^2 J \,d\xi d\eta = \frac{1}{\rho} \left(\frac{LH}{4}\right) \int_{-1}^{1}\int_{-1}^{1} \left( \frac{(1-\eta)^2}{4L^2} + \frac{(1-\xi)^2}{4H^2} \right) \,d\xi d\eta = \frac{1}{3\rho}\left(\frac{L}{H} + \frac{H}{L}\right)
$$

这个例子清晰地展示了从形函数到最终矩阵项的具体计算流程。

### 矩阵积分的[数值求积](@entry_id:136578)

除了少数简单情况（如[常系数](@entry_id:269842)、[仿射映射](@entry_id:746332)），单元矩阵的积分通常无法解析求解，必须依赖**[数值求积](@entry_id:136578)** (numerical quadrature)，例如[高斯求积法](@entry_id:146011) (Gauss quadrature)。选择合适的求积方案至关重要，它直接影响计算的准确性和效率。

一个[求积法则](@entry_id:753909)的**精确度等级** (degree of exactness) 是指它能够精确积分的多项式的最高次数。要精确计算单元矩阵，[求积法则](@entry_id:753909)的[精确度](@entry_id:143382)等级必须不低于被积函数的最高多项式次数。

我们来分析被积函数的次数。以质量矩阵为例，其被积函数为 $\frac{1}{K}\,\hat{N}_a \hat{N}_b\,J$。

- **线性单纯元（三角形/四面体）**: 形函数 $\hat{N}$ 是线性的（1次）。其乘积 $\hat{N}_a \hat{N}_b$ 是2次多项式。对于[仿射映射](@entry_id:746332)，雅可比行列式 $J$ 和材料参数都是常数（0次）。因此，被积函数是2次多项式，需要一个[精确度](@entry_id:143382)等级至少为2的[求积法则](@entry_id:753909) 。例如，对于三角形，一个对称的3点[求积法则](@entry_id:753909)即可满足要求；对于四面体，则可用一个4点法则。

- **[高阶谱](@entry_id:191458)元/等参元**: 当使用高阶形函数或弯曲的单元（非[仿射映射](@entry_id:746332)）时，情况变得复杂 。假设我们使用 $p$ 次拉格朗日谱元：
    1.  形函数 $\hat{N}_a, \hat{N}_b$ 在每个坐标方向上是 $p$ 次多项式，其乘积是 $2p$ 次。
    2.  如果映射也是 $p$ 次的（等参），[雅可比矩阵](@entry_id:178326)的项是 $\partial \hat{N}/\partial \xi_i$ 的[线性组合](@entry_id:154743)，次数为 $p-1$。其行列式 $J$ 的次数最高可达 $3(p-1)$（在3D情况下）。
    3.  如果材料参数 $1/K$ 也用 $p$ 次多项式近似，则被积函数的总次数最高可达 $2p + 3(p-1) + p = 6p-3$。

    因此，为了精确积分这样一个[高阶单元](@entry_id:750328)的[质量矩阵](@entry_id:177093)，需要一个[精确度](@entry_id:143382)等级非常高的[求积法则](@entry_id:753909)。例如，对于 $d_{max}=6p-3$ 的被积函数，高斯-勒让德 (Gauss-Legendre) 求积至少需要 $n$ 个点，其中 $2n-1 \ge 6p-3$，即 $n \ge 3p-1$。这表明，单元的几何形状和材料的复杂性会极大地增加精确积分的计算成本。

### 单元矩阵的性质与病态

#### [一致质量矩阵](@entry_id:174630)与[集总质量矩阵](@entry_id:173011)

通过精确积分得到的质量矩阵 $\mathbf{M}_e$ 被称为**[一致质量矩阵](@entry_id:174630)** (consistent mass matrix)。它通常是全矩阵（非对角），耦合了单元上所有节点的运动。例如，对于面积为 $A$ 的线性[三角形单元](@entry_id:167871)，其[一致质量矩阵](@entry_id:174630)为 ：

$$
\mathbf{M}_{e}^{\text{cons}} = \frac{A}{12} \begin{pmatrix} 2 & 1 & 1 \\ 1 & 2 & 1 \\ 1 & 1 & 2 \end{pmatrix}
$$

然而，在许多应用中，特别是**[显式时间积分](@entry_id:165797)** (explicit time integration) 算法中，需要频繁求解形如 $\mathbf{M}^{-1}\mathbf{r}$ 的运算。如果 $\mathbf{M}$ 是一个全矩阵，求逆的计算代价将非常高昂，从而破坏了显式算法的效率优势。

为了解决这个问题，人们引入了**[集总质量矩阵](@entry_id:173011)** (lumped mass matrix) $\mathbf{M}_{e}^{\text{lump}}$，它是一个对角矩阵。构造[集总质量矩阵](@entry_id:173011)的常用方法是**[行和集总](@entry_id:754439)** (row-sum lumping)，即将[一致质量矩阵](@entry_id:174630)每行的元素加到该行的对角元上，并将所有非对角元置零。对于上述线性三角形，其[集总质量矩阵](@entry_id:173011)的对角元均为 $A/3$。另一种方法是使用低阶的**节点求积** (nodal quadrature)，即只在单元节点处求值。对于线性单元，这两种方法得到的结果是相同的 。[集总质量矩阵](@entry_id:173011)的求逆操作仅需对对角元取倒数，计算效率极高。

#### 伪[零能模](@entry_id:172472)态（沙漏模态）

理想情况下，一个未受约束的单元的[刚度矩阵](@entry_id:178659) $\mathbf{K}_e$ 应该只包含对应于刚体运动（在声学中标量场中为常数[压力模](@entry_id:159654)式）的[零能模](@entry_id:172472)态。然而，如果[刚度矩阵](@entry_id:178659)的[数值积分](@entry_id:136578)不充分，即**[减缩积分](@entry_id:167949)** (reduced integration)，就可能引入非物理的、能量为零的变形模式，称为**伪[零能模](@entry_id:172472)态** (spurious zero-energy modes) 或**沙漏模态** (hourglass modes)。

以一个四节点的[双线性](@entry_id:146819)[四边形单元](@entry_id:176937)为例 ，其刚度矩阵的被积函数包含梯度项。如果我们仅使用一个积分点（例如单元中心的 $1 \times 1$ [高斯点](@entry_id:170251)）来[计算刚度](@entry_id:1122809)矩阵，那么任何在该积分点梯度为零的变形模式都将不产生应变能，从而成为一个[零能模](@entry_id:172472)态。

对于[双线性](@entry_id:146819)四边形，除了物理的常数[压力模](@entry_id:159654)态（梯度处处为零）外，还存在一个“沙漏”形状的[压力分布](@entry_id:275409)（例如，节点压力为 $(1, -1, 1, -1)$），其梯度恰好在单元中心为零。因此，采用单点积分的刚度矩阵将具有两个[零能模](@entry_id:172472)态，其秩比完全积分的矩阵低1。这种[秩亏](@entry_id:754065)损会导致数值解的污染和不稳定。

需要强调的是，沙漏模态是刚度矩阵 $\mathbf{K}_e$ 的一种病态，由其积分不当引起。即使质量矩阵 $\mathbf{M}_e$ 被完全、精确地积分，也无法消除沙漏模态本身的存在 。

### 组装与全局系统性质

计算完所有单元的矩阵 $\mathbf{K}_e$ 和 $\mathbf{M}_e$ 后，需要将它们**组装** (assemble) 成全局矩阵 $\mathbf{K}$ 和 $\mathbf{M}$，以形成描述整个系统行为的方程组。

组装过程本质上是一个“对号入座”并累加的过程。对于每个单元 $e$，其局部节点 $a$ 和 $b$ 对应于全局节点 $I$ 和 $J$。单元矩阵的项 $(K_e)_{ab}$ 就会被加到全局矩阵的 $(K)_{IJ}$ 位置上。这个过程可以用**连接矩阵** (connectivity matrix) $\mathbf{L}_e$ 进行优雅的数学描述 ：

$$
\mathbf{K} = \sum_{e=1}^{n_{\text{el}}} \mathbf{L}_e^T \mathbf{K}_e \mathbf{L}_e \quad \text{and} \quad \mathbf{M} = \sum_{e=1}^{n_{\text{el}}} \mathbf{L}_e^T \mathbf{M}_e \mathbf{L}_e
$$

组装过程一个极其重要的结果是全局矩阵的**[稀疏性](@entry_id:136793)** (sparsity)。由于形函数 $N_I$ 的**局部支撑** (local support)特性（即它只在包含节点 $I$ 的单元上非零），全局矩阵项 $K_{IJ}$ 或 $M_{IJ}$ 只有在节点 $I$ 和 $J$ 至少共享一个单元时才可能非零。这意味着在一个大规模的三维网格中，矩阵的每一行只有少数几个非零项，这些项对应于该节点的直接邻居。每行的非零元数量由局部网格的拓扑结构决定，而与整个网格的规模 $N$ 无关。正是这种[稀疏性](@entry_id:136793)使得[有限元法](@entry_id:749389)能够高效地求解拥有数百万甚至数十亿自由度的大型工程问题 。对于标准的伽辽金法，$\mathbf{K}$ 和 $\mathbf{M}$ 的稀疏模式是相同的。

### 与[系统动力学](@entry_id:136288)及精度的关联

单元矩阵的特性深刻地影响着最终数值解的动态行为和准确性。

#### 数值频散

[有限元离散化](@entry_id:193156)会引入**数值频散** (numerical dispersion)，即数值[波速](@entry_id:186208) $c_{num}$ 依赖于波的频率和网格尺寸，与物理[波速](@entry_id:186208) $c$ 产生偏差。这种偏差是衡量数值方案精度的重要指标。

以[一维波动方程](@entry_id:164824)为例，若采用线性元和**[一致质量矩阵](@entry_id:174630)**，可以推导出离散系统的频散关系 。设无量纲频率为 $p = \omega h / c$，其中 $h$ 是单元尺寸，$\omega$ 是角频率。数值相速度 $c_{p,num}$ 与物理相速度 $c$ 的[相对误差](@entry_id:147538)为：

$$
E(p) = \frac{c_{p,num}}{c} - 1 = \frac{p}{\arccos\left(\frac{6 - 2p^2}{6 + p^2}\right)} - 1
$$

这个表达式表明，即使是对于“精确”的[一致质量矩阵](@entry_id:174630)，数值波在网格上传播时也会出现[相速度误差](@entry_id:1129602)，尤其是在高频（或每波长单元数较少）的情况下。

#### [时间积分](@entry_id:267413)的稳定性

当使用[显式时间积分](@entry_id:165797)方案（如[中心差分法](@entry_id:163679)）时，时间步长 $\Delta t$ 受到一个**稳定性条件**的限制，即著名的 Courant-Friedrichs-Lewy (CFL) 条件。这个条件与系统的最高本征频率 $\omega_{max}$ 相关，而 $\omega_{max}$ 又由[质量矩阵](@entry_id:177093)和刚度矩阵共同决定。

继续以[一维波动方程](@entry_id:164824)为例，这次我们采用**[集总质量矩阵](@entry_id:173011)**。通过对离散系统的[模态分析](@entry_id:163921)，可以推导出系统的最高频率 $\omega_{\max} = \frac{2}{h} \sqrt{\frac{K}{\rho}}$。[中心差分法](@entry_id:163679)的稳定性要求 $\Delta t \le 2/\omega_{max}$，因此最大稳定时间步长为 ：

$$
\Delta t_{\max} = h \sqrt{\frac{\rho}{K}} = \frac{h}{c}
$$

这个结果清晰地表明，时间步长的上限直接由单元尺寸 $h$ 和材料物理属性（波速 $c$）决定。它也揭示了显式方法的一个[基本权](@entry_id:200855)衡：为了提高[空间分辨率](@entry_id:904633)而加密网格（减小 $h$），将不可避免地导致必须使用更小的时间步长，从而增加总的计算时间。

### 阻尼建模

在许多实际声学问题中，[能量耗散](@entry_id:147406)或阻尼是不可忽略的。阻尼效应在有限元方程中通过引入阻尼矩阵 $\mathbf{C}$ 来体现。

#### 基于物理的阻尼

一种方法是通过复数材料参数来引入[本构关系](@entry_id:186508)层面的损耗。例如，声学介质中的粘滞损耗可以等效为使用复数体积模量或复数密度 。

1.  **复数[体积模量](@entry_id:160069)**: $K \to K(1+i\eta)$。其中 $\eta$ 是一个小的、频率无关的损耗因子。这种模型在[频域分析](@entry_id:1125318)中会导致一个与[质量矩阵](@entry_id:177093)结构相同的有效阻尼矩阵，近似为 $\mathbf{C} \approx \omega\eta\mathbf{M}$。这是一种**[质量比例阻尼](@entry_id:165902)** (mass-proportional damping)。

2.  **复数密度**: $\rho \to \rho(1+i\eta)$。这种模型则会导致一个与刚度矩阵结构相同的有效阻尼矩阵，近似为 $\mathbf{C} \approx (1/\omega)\eta\mathbf{K}$。这是一种**[刚度比例阻尼](@entry_id:165011)** (stiffness-proportional damping)，也称为滞后阻尼 (hysteretic damping)。

这表明，不同的物理耗散机制在[有限元模型](@entry_id:1124986)中会体现为不同结构的阻尼矩阵。

#### 唯象[阻尼模型](@entry_id:748160)：[瑞利阻尼](@entry_id:172362)

在工程实践中，一种更通用且方便的[唯象模型](@entry_id:1129607)是**[瑞利阻尼](@entry_id:172362)** (Rayleigh damping)。它假设阻尼矩阵是[质量矩阵](@entry_id:177093)和刚度矩阵的[线性组合](@entry_id:154743) ：

$$
\mathbf{C} = \alpha \mathbf{M} + \beta \mathbf{K}
$$

其中 $\alpha$ 和 $\beta$ 是待定系数。对于系统的第 $j$ 个振动模态，其[模态阻尼比](@entry_id:162799) $\zeta_j$ 与自身的[固有频率](@entry_id:174472) $\omega_j$ 相关：

$$
\zeta_j = \frac{\alpha}{2\omega_j} + \frac{\beta\omega_j}{2}
$$

这种模型的灵活性在于，我们可以通过选择合适的 $\alpha$ 和 $\beta$ 来控制特定频率范围内的阻尼水平。例如，如果我们希望在频率区间 $[\omega_a, \omega_b]$ 内获得一个接近常数的目标[阻尼比](@entry_id:262264) $\zeta_0$，我们可以令区间端点的[阻尼比](@entry_id:262264)都等于 $\zeta_0$，即 $\zeta(\omega_a) = \zeta(\omega_b) = \zeta_0$。解此[线性方程组](@entry_id:148943)可得：

$$
\alpha = \frac{2\zeta_0 \omega_a \omega_b}{\omega_a + \omega_b}, \quad \beta = \frac{2\zeta_0}{\omega_a + \omega_b}
$$

通过这种方式，我们可以在没有精确物理模型的情况下，有效地为[数值模拟](@entry_id:146043)引入符合工程要求的耗散特性 。