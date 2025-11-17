## 引言
[压电材料](@entry_id:197563)，作为一类能够实现[机械能](@entry_id:162989)与电能相互转换的[智能材料](@entry_id:196298)，是现代传感器、执行器和高频谐振器的核心。为了精确设计和优化这些功能强大的器件，有限元方法（FEM）已成为不可或缺的分析工具。然而，在理论物理与工程应用之间存在一道鸿沟：如何将描述压电效应的复杂本构关系和多物理场耦合，系统地转化为一个稳定、精确的[计算模型](@entry_id:152639)？这正是工程师和研究人员面临的核心挑战。

本文旨在系统性地解决这一问题，为读者提供一个从理论基础到高级应用的完整视角。我们将首先在 **“原理与机制”** 章节中，从[热力学](@entry_id:141121)第一性原理出发，推导压电耦合的控制方程和有限元离散格式，并探讨建模中的关键数值问题。接着，在 **“应用与[交叉](@entry_id:147634)学科联系”** 章节中，展示这些理论如何应用于执行器、传感器和动态系统的设计，并揭示其与控制、热学及[材料科学](@entry_id:152226)的深刻联系。最后，通过 **“动手实践”** 部分，读者将有机会将理论付诸实践，巩固对压电有限元建模的理解。

## 原理与机制

本章深入探讨了压电耦合单元背后的基本原理和核心机制。我们将从压电现象的物理解释出发，建立其[热力学](@entry_id:141121)和本构框架，然后推导出适用于有限元方法 (FEM) 的[变分形式](@entry_id:166033)和离散方程。此外，我们还将讨论实际建模中遇到的关键问题，如[数值稳定性](@entry_id:146550)、边界条件的施加以及耦合效应的物理解释。本章旨在为读者提供一个从第一性原理到高级计算概念的系统性理解。

### 准静态[电磁场](@entry_id:265881)近似

在对[压电](@entry_id:268187)装置进行[结构动力学](@entry_id:172684)分析时，我们通常处理的是远低于微波范围的频率。一个核心问题是，我们是否需要考虑完整的[麦克斯韦方程组](@entry_id:150940)，包括[磁场](@entry_id:153296)感应和[电磁波传播](@entry_id:272130)效应。答案通常是否定的，这得益于**[准静态近似](@entry_id:264812) (quasi-static approximation)**。

为了理解这一近似的合理性，让我们从[麦克斯韦方程组](@entry_id:150940)出发。在[时谐场](@entry_id:755985)（时间依赖性为 $\exp(i\omega t)$）中，[法拉第感应定律](@entry_id:146175)和[安培-麦克斯韦定律](@entry_id:266368)分别为：
$$ \nabla \times \boldsymbol{E} = -i\omega\boldsymbol{B} $$
$$ \nabla \times \boldsymbol{H} = \boldsymbol{J}_{\text{free}} + i\omega\boldsymbol{D} $$
其中 $\boldsymbol{E}$ 是[电场](@entry_id:194326)，$\boldsymbol{B}$ 是[磁感应强度](@entry_id:144179)，$\boldsymbol{H}$ 是磁场强度，$\boldsymbol{D}$ 是[电位移](@entry_id:269383)，$\boldsymbol{J}_{\text{free}}$ 是[自由电流](@entry_id:191634)密度。

[准静态近似](@entry_id:264812)的核心是假设[电场](@entry_id:194326)是无旋的，即 $\nabla \times \boldsymbol{E} \approx \boldsymbol{0}$，这使得我们可以引入一个标量[电势](@entry_id:267554) $\phi$，定义 $\boldsymbol{E} = -\nabla \phi$。这一假设的有效性取决于感应项 $-i\omega\boldsymbol{B}$ 的大小。通过[量纲分析](@entry_id:140259)，我们可以推导出该近似成立的条件 [@problem_id:2587443]。

考虑一个特征尺寸为 $L$ 的压[电介质](@entry_id:147163)，其[介电常数](@entry_id:146714)为 $\varepsilon$，磁导率为 $\mu$。通过对上述方程进行标度分析，可以证明，当[无量纲数](@entry_id:136814) $\omega L / c_{\text{eff}} \ll 1$ 时，[感应电场](@entry_id:267314)相对于梯度[电场](@entry_id:194326)可以忽略不计。这里，$c_{\text{eff}} = 1/\sqrt{\mu\varepsilon}$ 是材料中的[电磁波](@entry_id:269629)速度。这个条件直观地表示，装置的尺寸 $L$ 必须远小于工作频率下的[电磁波](@entry_id:269629)波长。对于典型的压[电[陶](@entry_id:187650)瓷](@entry_id:148626)（如 PZT）和 MHz 范围内的应用，这个条件通常能够很好地满足。

忽略磁效应的另一个有力证据来自能量的比较。在无损介质中，[磁场能量](@entry_id:267501)密度与[电场能量密度](@entry_id:261497)的比值可以被证明为：
$$ \frac{\langle u_{m} \rangle}{\langle u_{e} \rangle} \sim \left(\frac{\omega L}{c_{\text{eff}}}\right)^{2} $$
这个比值的平方关系意味着，当 $\omega L / c_{\text{eff}}$ 是一个小量时，[磁场能量](@entry_id:267501)在总[电磁能](@entry_id:264720)量中占比极小，可以忽略不计 [@problem_id:2587443]。因此，在构建压电耦合问题的弱形式时，我们通常只考虑[电场能量](@entry_id:193072)，而完全忽略[磁场](@entry_id:153296)项。这极大地简化了问题，将一个复杂的全波电磁问题简化为一个耦合的弹-静电问题。

### [热力学](@entry_id:141121)基础与[本构关系](@entry_id:186508)

压电效应是电学和力学性质的内在耦合，其本构关系必须基于严格的[热力学](@entry_id:141121)框架，以确保[能量守恒](@entry_id:140514)和[材料稳定性](@entry_id:183933)。通过选择不同的热力学势，我们可以得到不同形式的[本构方程](@entry_id:138559)，每种形式在特定应用中都各有优势。

#### [热力学势](@entry_id:140516)与勒让德变换

一个可逆[热力学系统](@entry_id:188734)的状态可以通过一个[势函数](@entry_id:176105)来描述。对于[压电材料](@entry_id:197563)，一个常见的选择是比内能（单位体积内能）$U$，其自然变量是[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$、熵 $S$ 和[电位移](@entry_id:269383) $\boldsymbol{D}$。其微分形式为 [@problem_id:2587465]：
$$ \mathrm{d}U = \boldsymbol{\sigma}:\mathrm{d}\boldsymbol{\varepsilon} + T\mathrm{d}S + \boldsymbol{E}\cdot \mathrm{d}\boldsymbol{D} $$
其中 $\boldsymbol{\sigma}$ 是应力张量，$T$ 是温度。从这个表达式可以看出，应力、温度和[电场](@entry_id:194326)分别是内能对应变、熵和[电位移](@entry_id:269383)的[共轭变量](@entry_id:147843)。

在许多应用中，特别是基于位移和[电势](@entry_id:267554)的有限元公式中，将应变 $\boldsymbol{\varepsilon}$ 和[电场](@entry_id:194326) $\boldsymbol{E}$ 作为自变量更为方便。这可以通过**勒让德变换 (Legendre transform)** 实现。通过对 $U$ 进行关于电学变量的勒让德变换，我们得到电焓 $H$：
$$ H(\boldsymbol{\varepsilon}, S, \boldsymbol{E}) = U - \boldsymbol{E} \cdot \boldsymbol{D} $$
其微分形式为 $\mathrm{d}H = \boldsymbol{\sigma}:\mathrm{d}\boldsymbol{\varepsilon} + T\mathrm{d}S - \boldsymbol{D}\cdot \mathrm{d}\boldsymbol{E}$。

如果过程是等温的（$T$ 是常数），我们可以进一步进行变换，得到[亥姆霍兹自由能](@entry_id:136442)或吉布斯类势函数 $G(\boldsymbol{\varepsilon}, T, \boldsymbol{E})$：
$$ G(\boldsymbol{\varepsilon}, T, \boldsymbol{E}) = H - TS = U - TS - \boldsymbol{E} \cdot \boldsymbol{D} $$
其[微分形式](@entry_id:146747)为 $\mathrm{d}G = \boldsymbol{\sigma}:\mathrm{d}\boldsymbol{\varepsilon} - S\mathrm{d}T - \boldsymbol{D}\cdot \mathrm{d}\boldsymbol{E}$。

这些[势函数](@entry_id:176105)的[二阶导数](@entry_id:144508)（黑塞矩阵）定义了材料的**[切线](@entry_id:268870)模量**。例如，对于[等温过程](@entry_id:143096)，从 $G(\boldsymbol{\varepsilon}, \boldsymbol{E})$ 出发，我们可以得到：
$$ \boldsymbol{c}^E = \frac{\partial^2 G}{\partial\boldsymbol{\varepsilon} \partial\boldsymbol{\varepsilon}}, \quad \boldsymbol{e} = -\frac{\partial^2 G}{\partial\boldsymbol{\varepsilon} \partial\boldsymbol{E}}, \quad \boldsymbol{\epsilon}^S = -\frac{\partial^2 G}{\partial\boldsymbol{E} \partial\boldsymbol{E}} $$
这些分别是恒定[电场](@entry_id:194326)下的弹性刚度、[压电](@entry_id:268187)应力系数和恒定应变下的[介电常数](@entry_id:146714)。[热力学势](@entry_id:140516)的存在保证了[混合偏导数](@entry_id:139334)的相等性，这直接导致了压电[耦合矩阵](@entry_id:191757)的对称性，从而保证了有限元[系统矩阵](@entry_id:172230)的对称性 [@problem_id:2587465]。

#### [本构方程](@entry_id:138559)的不同形式

根据所选的自变量，线弹性[压电](@entry_id:268187)[本构关系](@entry_id:186508)有多种等效形式。最常用的两种是**应变-[电荷](@entry_id:275494) (strain-charge)** 形式和**应力-[电荷](@entry_id:275494) (stress-charge)** 形式。

**应变-[电荷](@entry_id:275494)形式 (e-form):**
这种形式以应变 $\boldsymbol{\varepsilon}$ 和[电场](@entry_id:194326) $\boldsymbol{E}$ 为[自变量](@entry_id:267118)，通常记为 $e$ 形式，直接由电焓 $H$ 或吉布斯势 $G$ 导出。这也是在标准的位移-[电势](@entry_id:267554)有限元公式中最自然的形式 [@problem_id:2587430]：
$$ \boldsymbol{\sigma} = \boldsymbol{c}^{E}:\boldsymbol{\varepsilon} - \boldsymbol{e}^{\mathsf{T}}\boldsymbol{E} $$
$$ \boldsymbol{D} = \boldsymbol{e}:\boldsymbol{\varepsilon} + \boldsymbol{\epsilon}^{S}\boldsymbol{E} $$
这里的上标具有明确的物理意义：
*   $\boldsymbol{c}^{E}$ 是**恒定[电场](@entry_id:194326) (short-circuit)** 条件下测得的[弹性刚度张量](@entry_id:170728)。
*   $\boldsymbol{\epsilon}^{S}$ 是**恒定应变 (clamped)** 条件下测得的[介电常数张量](@entry_id:274052)。
*   $\boldsymbol{e}$ 是[压电](@entry_id:268187)应力系数张量。

**应力-[电荷](@entry_id:275494)形式 (d-form):**
这种形式以应力 $\boldsymbol{\sigma}$ 和[电场](@entry_id:194326) $\boldsymbol{E}$ 为[自变量](@entry_id:267118)，记为 $d$ 形式。它在描述传感器（输入为应力）或从实验数据表征材料时非常有用：
$$ \boldsymbol{\varepsilon} = \boldsymbol{s}^{E}:\boldsymbol{\sigma} + \boldsymbol{d}^{\mathsf{T}}\boldsymbol{E} $$
$$ \boldsymbol{D} = \boldsymbol{d}:\boldsymbol{\sigma} + \boldsymbol{\epsilon}^{T}\boldsymbol{E} $$
这里的材料常数定义为：
*   $\boldsymbol{s}^{E} = (\boldsymbol{c}^{E})^{-1}$ 是恒定[电场](@entry_id:194326)下的**[弹性柔度](@entry_id:189433)**张量。
*   $\boldsymbol{\epsilon}^{T}$ 是**恒定应力 (free)** 条件下测得的[介电常数张量](@entry_id:274052)。
*   $\boldsymbol{d}$ 是[压电](@entry_id:268187)应变系数张量。

这两种形式是完[全等](@entry_id:273198)效的，可以通过代数运算相互转换。例如，从 $d$ 形式的参数推导 $e$ 形式的参数的关系如下 [@problem_id:2587496]：
$$ \boldsymbol{c}^{E} = (\boldsymbol{s}^{E})^{-1} $$
$$ \boldsymbol{e} = \boldsymbol{d} : \boldsymbol{c}^{E} $$
$$ \boldsymbol{\epsilon}^{S} = \boldsymbol{\epsilon}^{T} - \boldsymbol{d} : \boldsymbol{c}^{E} : \boldsymbol{d}^{\mathsf{T}} = \boldsymbol{\epsilon}^{T} - \boldsymbol{e} : \boldsymbol{d}^{\mathsf{T}} $$
这些转换关系在有限元分析中至关重要，因为材料数据手册通常提供 $d$ 形式的参数，而有限元程序内部则需要 $e$ 形式的参数。理解这些不同条件下的材料属性（例如，$\boldsymbol{\epsilon}^{T}$ 在机械自由条件下测量，而 $\boldsymbol{\epsilon}^{S}$ 在机械夹持条件下测量）对于正确建模至关重要 [@problem_id:2587496]。

#### [机电耦合](@entry_id:142536)因子

**[机电耦合](@entry_id:142536)因子 (electromechanical coupling factor)** $k$ 是一个无量纲参数，用于衡量[压电材料](@entry_id:197563)将机械能和电能相互转换的效率。$k^2$ 可以被解释为在一次能量转换过程中，存储在一种形式的能量中可以转换为另一种形式的能量的最大比例。

通过对本构关系进行能量分析，可以推导出 $k^2$ 的表达式。例如，在一维情况下，耦合因子 $k_{33}$ 的平方可以表示为 [@problem_id:2587499]：
$$ k^2 = \frac{e^2}{c^E \varepsilon^S + e^2} $$
这个表达式表明，[耦合强度](@entry_id:275517)取决于压电系数 $e$ 的大小以及材料的纯机械（$c^E$）和纯介电（$\varepsilon^S$）特性的乘积。$k^2$ 的值越高，材料作为执行器或传感器的性能就越好。

### 控制方程与[变分形式](@entry_id:166033)

有限元方法是建立在积分形式的控制方程（即[弱形式](@entry_id:142897)）之上的。对于[压电](@entry_id:268187)问题，我们需要耦合的力学和电学控制方程。

在准静态条件下，力学场的控制方程是**[线性动量平衡](@entry_id:193575)方程**：
$$ \nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0} $$
其中 $\boldsymbol{b}$ 是单位体积的体力。

电学场的控制方程是**高斯静电定律**：
$$ \nabla \cdot \boldsymbol{D} = \rho_f $$
其中 $\rho_f$ 是自由电荷密度。

为了得到[弱形式](@entry_id:142897)，我们将上述两个方程分别乘以一个[虚位移](@entry_id:168781)（测试函数）$\boldsymbol{w}$ 和一个虚[电势](@entry_id:267554)（测试函数）$\eta$，然后在求解域 $\Omega$ 上积分。利用[高斯散度定理](@entry_id:188065)（分部积分），我们可以将[微分算子](@entry_id:140145)从应力 $\boldsymbol{\sigma}$ 和[电位移](@entry_id:269383) $\boldsymbol{D}$ 转移到测试函数 $\boldsymbol{w}$ 和 $\eta$ 上 [@problem_id:2587484]。

经过推导，我们得到耦合的[变分方程](@entry_id:635018)：
$$ \int_{\Omega} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\boldsymbol{w}) \, \mathrm{d}\Omega = \int_{\Omega} \boldsymbol{b} \cdot \boldsymbol{w} \, \mathrm{d}\Omega + \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \boldsymbol{w} \, \mathrm{d}\Gamma $$
$$ -\int_{\Omega} \boldsymbol{D} \cdot \nabla \eta \, \mathrm{d}\Omega = \int_{\Omega} \rho_f \eta \, \mathrm{d}\Omega + \int_{\Gamma_q} \bar{q} \eta \, \mathrm{d}\Gamma $$
这里，$\bar{\boldsymbol{t}}$ 是在边界 $\Gamma_t$ 上施加的面力，$\bar{q}$ 是在边界 $\Gamma_q$ 上施加的表面[自由电荷](@entry_id:264392)密度。

这个推导过程清楚地揭示了两类边界条件 [@problem_id:2587432] [@problem_id:2587484]：
*   **本质边界条件 (Essential Boundary Conditions)**：也称为狄利克雷 (Dirichlet) 条件，直接施加在主变量上。在[压电](@entry_id:268187)问题中，它们是指定的位移 $\boldsymbol{u} = \bar{\boldsymbol{u}}$ 和指定的[电势](@entry_id:267554) $\phi = \bar{\phi}$。这些条件必须在有限元函数空间中被强加。
*   **自然边界条件 (Natural Boundary Conditions)**：也称为诺伊曼 (Neumann) 条件，施加在主变量的导数相关的量上（共轭量）。它们是指定的面力 $\boldsymbol{\sigma}\boldsymbol{n} = \bar{\boldsymbol{t}}$ 和指定的[表面电荷](@entry_id:160539) $\boldsymbol{D}\cdot\boldsymbol{n} = \bar{q}$。这些条件通过[弱形式](@entry_id:142897)中的边界积分项自然地得到满足。

### [有限元离散化](@entry_id:193156)

将连续的[弱形式](@entry_id:142897)转化为[代数方程](@entry_id:272665)组，需要对求解域进行离散化，并对场变量进行插值。

#### 插值与形函数

[变分形式](@entry_id:166033)要求位移场 $\boldsymbol{u}$ 和[电势](@entry_id:267554)场 $\phi$ 的[一阶导数](@entry_id:749425)（应变和[电场](@entry_id:194326)）是平方可积的。这要求解空间是索伯列夫空间 $H^1(\Omega)$。为了满足这一**协调性 (conformity)** 要求，我们需要选择在单元之间至少是 $C^0$ 连续的[插值函数](@entry_id:262791) [@problem_id:2587432]。标准的拉格朗日单元（如线性或二次四边形/[六面体单元](@entry_id:174602)）正好满足此要求。

在一个单元内部，位移和[电势](@entry_id:267554)场可以通过节点值和形函数 $N_i$ 进行插值：
$$ \boldsymbol{u}(\boldsymbol{x}) = \sum_i N_i(\boldsymbol{x}) \boldsymbol{u}_i, \quad \phi(\boldsymbol{x}) = \sum_i N_i(\boldsymbol{x}) \phi_i $$
其中 $\boldsymbol{u}_i$ 和 $\phi_i$ 是节点 $i$ 的位移向量和[电势](@entry_id:267554)值。

应变和[电场](@entry_id:194326)则通过形函数的**导数**与节点自由度联系起来，形成离散的[梯度算子](@entry_id:275922)矩阵 $\boldsymbol{B}_u$ 和 $\boldsymbol{B}_\phi$：
$$ \boldsymbol{\varepsilon} = \boldsymbol{B}_u \boldsymbol{d}_u, \quad \boldsymbol{E} = -\boldsymbol{B}_\phi \boldsymbol{d}_\phi $$
其中 $\boldsymbol{d}_u$ 和 $\boldsymbol{d}_\phi$ 分别是单元的节点位移和[电势](@entry_id:267554)向量。例如，对于三维问题，$\boldsymbol{B}_u$ 的每一列由形函数的空间导数组合而成，而 $\boldsymbol{B}_\phi$ 的每一列就是对应形函数的梯度 [@problem_id:2587432]。

#### 离散系统方程

将插值表达式代入[弱形式](@entry_id:142897)，并利用本构关系，最终可以得到一个耦合的线性代数方程组，其形式为：
$$ \begin{pmatrix} \boldsymbol{K}_{uu}  \boldsymbol{K}_{u\phi} \\ \boldsymbol{K}_{\phi u}  \boldsymbol{K}_{\phi\phi} \end{pmatrix} \begin{pmatrix} \boldsymbol{d}_u \\ \boldsymbol{d}_\phi \end{pmatrix} = \begin{pmatrix} \boldsymbol{f}_u \\ \boldsymbol{f}_\phi \end{pmatrix} $$
其中：
*   $\boldsymbol{K}_{uu} = \int_\Omega \boldsymbol{B}_u^T \boldsymbol{c}^E \boldsymbol{B}_u \, \mathrm{d}\Omega$ 是**弹性[刚度矩阵](@entry_id:178659)**。
*   $\boldsymbol{K}_{\phi\phi} = -\int_\Omega \boldsymbol{B}_\phi^T \boldsymbol{\epsilon}^S \boldsymbol{B}_\phi \, \mathrm{d}\Omega$ 是**介电刚度矩阵**（注意负号约定，通常定义为正定形式）。
*   $\boldsymbol{K}_{u\phi} = \int_\Omega \boldsymbol{B}_u^T \boldsymbol{e}^T \boldsymbol{B}_\phi \, \mathrm{d}\Omega$ 和 $\boldsymbol{K}_{\phi u} = \boldsymbol{K}_{u\phi}^T$ 是**[压电](@entry_id:268187)[耦合矩阵](@entry_id:191757)**。
*   $\boldsymbol{f}_u$ 和 $\boldsymbol{f}_\phi$ 分别是节点力向量和节点电荷向量。

#### 材料属性的矩阵表示

对于各向异性材料，三维[本构关系](@entry_id:186508)中的[四阶张量](@entry_id:181350) $\boldsymbol{c}^E$ 和三阶张量 $\boldsymbol{e}$ 通常使用**Voigt 表示法**简化为 $6 \times 6$ 和 $3 \times 6$ 的矩阵。这些矩阵的结构由材料的[晶体对称性](@entry_id:198772)决定。例如，对于沿 3 轴极化的横观[各向同性材料](@entry_id:170678)（如点群 6mm 的[陶瓷](@entry_id:148626)），其弹性、[压电](@entry_id:268187)和[介电矩阵](@entry_id:144203)具有特定的[稀疏结构](@entry_id:755138) [@problem_id:2587391]。正确构建这些矩阵对于模拟材料的各向异性响应至关重要。

### 高级主题与数值考量

#### 耦合效应：静电软化

[压电](@entry_id:268187)耦合改变了系统的纯力学和纯电学响应。一个重要的现象是**静电软化 (electrostatic softening)**。考虑一种情况，其中[压电](@entry_id:268187)装置的电极短路（$\boldsymbol{f}_\phi = \boldsymbol{0}$），且电学自由度是内部的。我们可以通过**[静态凝聚](@entry_id:176722) (static condensation)** 的方法从耦合方程中消去[电势](@entry_id:267554)自由度 $\boldsymbol{d}_\phi$ [@problem_id:2587464]。

从第二行方程 $\boldsymbol{K}_{\phi u} \boldsymbol{d}_u + \boldsymbol{K}_{\phi\phi} \boldsymbol{d}_\phi = \boldsymbol{0}$ 中解出 $\boldsymbol{d}_\phi = -\boldsymbol{K}_{\phi\phi}^{-1} \boldsymbol{K}_{\phi u} \boldsymbol{d}_u$（这里假设 $\boldsymbol{K}_{\phi\phi}$ 是可逆的），并代入第一行方程，得到一个纯力学形式的方程：
$$ (\boldsymbol{K}_{uu} - \boldsymbol{K}_{u\phi}\boldsymbol{K}_{\phi\phi}^{-1}\boldsymbol{K}_{\phi u}) \boldsymbol{d}_u = \boldsymbol{f}_u $$
系统的**有效机械刚度**为 $\boldsymbol{K}_{\text{eff}} = \boldsymbol{K}_{uu} - \boldsymbol{K}_{u\phi}\boldsymbol{K}_{\phi\phi}^{-1}\boldsymbol{K}_{\phi u}$。由于 $\boldsymbol{K}_{\phi\phi}$ 是正定的，修正项 $\boldsymbol{K}_{u\phi}\boldsymbol{K}_{\phi\phi}^{-1}\boldsymbol{K}_{\phi u}$ 是一个[半正定矩阵](@entry_id:155134)。因此，有效刚度 $\boldsymbol{K}_{\text{eff}}$ 小于或等于纯机械刚度 $\boldsymbol{K}_{uu}$。这种刚度的降低就是静电软化效应。其物理原因是，在短路条件下，材料的变形会产生[电场](@entry_id:194326)和[电荷](@entry_id:275494)的重新[分布](@entry_id:182848)，这种电学上的“自由”反过来使得材料在力学上显得更“软”。

#### 数值稳定性：伪模与锁定

在有限元分析中，**数值积分**的精度会影响结果的准确性和稳定性。对于[压电](@entry_id:268187)单元，不恰当的积分方案可能导致**伪[零能模](@entry_id:172472) (spurious zero-energy modes)**。例如，对一个四节点[四边形单元](@entry_id:176937) (Q4)，如果对介电[刚度矩阵](@entry_id:178659) $\boldsymbol{K}_{\phi\phi}$ 使用单点高斯积分（[减缩积分](@entry_id:167949)），会导致其[秩亏](@entry_id:754065)损，从而引入非物理的、能量为零的[电势](@entry_id:267554)[振荡](@entry_id:267781)模式 [@problem_id:2587420]。这种伪模会污染[电场](@entry_id:194326)解，必须通过使用足阶积分（如 $2 \times 2$ 高斯积分）或其他稳定化技术来避免。

#### 系统奇异性与约束

当模拟一个没有足够本质边界条件（[狄利克雷条件](@entry_id:137096)）的物体时，例如一个在空间中自由漂浮的压电装置，其[全局刚度矩阵](@entry_id:138630)将是**奇异的 (singular)**。这种奇异性源于物理上的不变性：
*   **[刚体运动](@entry_id:193355) (Rigid-body motions)**：整个物体可以在不产生任何应变的情况下平移和旋转。
*   **浮动[电势](@entry_id:267554) (Floating potential)**：整个物体的[电势](@entry_id:267554)可以同时增加一个任意常数，而不会改变[电场](@entry_id:194326)。

为了求解这个[奇异系统](@entry_id:140614)，必须施加足够的约束来消除这些[零能模](@entry_id:172472)。然而，约束的施加方式必须小心，以避免对物理上有意义的解（应变和[电场](@entry_id:194326)）产生偏倚 [@problem_id:2587470]。
*   **错误的方法**：例如，将单个节点固定（$\boldsymbol{u}=\boldsymbol{0}$）可以消除平移，但不能消除绕该点的转动。这种点约束还会引入非物理的应力集中。使用微小的“弹簧”进行正则化（在对角线上加小量）会改变系统的物理性质。
*   **正确的方法**：最理想的方法是施加与[零能模](@entry_id:172472)态正交的**积分约束**。例如，通过[拉格朗日乘子法](@entry_id:176596)施加零平均位移和零平均转动来消除刚体运动，以及施加零平均[电势](@entry_id:267554)来固定[电势](@entry_id:267554)参考点。这些全局约束精确地移除了奇异性，而不影响应变和[电场](@entry_id:194326)，从而得到一个无偏的、物理上正确的解。

#### 电极的建模

在实际设备中，[电势](@entry_id:267554)通常通过**电极 (electrodes)** 施加。电极是近似的[等势面](@entry_id:158674)。在有限元模型中，这需要特殊的处理 [@problem_id:2587484]：
*   **电压驱动电极**：如果电极的[电势](@entry_id:267554)是给定的（例如接地或连接到电压源），则该电极上所有节点的[电势](@entry_id:267554)自由度都被约束为该指定值。这是一种[狄利克雷边界条件](@entry_id:173524)。
*   **浮动电极**：如果电极不连接到外部电源，但由于其导电性仍保持等势，则其[电势](@entry_id:267554)是一个未知的常数。这可以通过引入一个额外的全局自由度（该电极的[电势](@entry_id:267554)值），并将该电极上所有节点的[电势](@entry_id:267554)自由度都约束到这个全局自由度上来实现。相应的测试[函数空间](@entry_id:143478)也必须满足在浮动电极上为常数的约束。

正确处理这些电极条件对于[精确模拟](@entry_id:749142)压电器件的响应至关重要。