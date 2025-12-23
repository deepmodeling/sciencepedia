## 引言
在[计算等离子体物理](@entry_id:198820)领域，粒子-网格（Particle-In-Cell, PIC）模拟是研究从实验室聚变到天体物理现象等各种复杂动力学过程的基石。然而，这些系统普遍存在一个核心挑战：多尺度性。物理过程往往发生在跨越数个数量级的时间尺度上，从飞秒级的电子振荡到秒级的宏观输运。这种“[数值刚性](@entry_id:752836)”问题对时间积分方法的选择提出了严苛的要求，直接决定了模拟的可行性与计算成本。本文旨在系统性地剖析解决这一挑战的两种主要策略：显式与[隐式时间积分](@entry_id:171761)。

本文将带领读者深入理解这两种方法的内在机制、优势与局限。在“原理与机制”一章中，我们将从[Vlasov-Maxwell方程组](@entry_id:756541)出发，详细阐述显式蛙跳格式的构造及其稳定性约束，并进一步揭示[隐式方法](@entry_id:138537)如何通过自洽求解绕开这些限制，以及实现它所需的高级数值技术，如牛顿-克雷洛夫方法。随后的“应用与交叉学科联系”一章将理论付诸实践，展示这些方法在聚变科学、地球科学等领域的具体应用，并探讨如何通过子循环、IMEX等混合策略应对复杂的多尺度问题。最后，在“动手实践”部分，读者将通过一系列精心设计的练习，亲手实现和分析这些算法的核心环节，从而将理论知识转化为真正的计算能力。

## 原理与机制

本章旨在深入探讨粒子-网格（PIC）模拟中两种核心的[时间积分方法](@entry_id:136323)：显式积分和[隐式积分](@entry_id:1126415)。我们将从控制等离子体动力学的基本方程出发，系统地阐述每种方法的数学构造、物理机制、稳定性约束以及在多尺度等离子体现象建模中的应用。本章的组织结构将引导读者从显式方法的直观性与局限性，过渡到[隐式方法](@entry_id:138537)的复杂性与强大功能，最终揭示现代大规模等离子体仿真实践中的前沿数值技术。

### 基础模型：Vlasov–Maxwell 方程组与 PIC 方法

无碰撞、磁化等离子体的动力学行为可由 Vlasov–Maxwell 方程组进行精确描述。该方程组自洽地耦合了描述带电粒子在相空间中演化的动力学方程与描述电磁场演化的 Maxwell 方程。

对于等离子体中的每个组分 $s$（例如电子、离子），其[相空间分布](@entry_id:151304)函数 $f_s(t, \mathbf{x}, \mathbf{v})$ 的演化遵循 Vlasov 方程，也即无碰撞的 Boltzmann 方程：
$$
\frac{\partial f_s}{\partial t} + \mathbf{v} \cdot \nabla_{\mathbf{x}} f_s + \frac{q_s}{m_s} \left( \mathbf{E} + \mathbf{v} \times \mathbf{B} \right) \cdot \nabla_{\mathbf{v}} f_s = 0
$$
其中 $q_s$ 和 $m_s$ 分别是组分 $s$ 的电荷和质量，$\mathbf{E}(t, \mathbf{x})$ 和 $\mathbf{B}(t, \mathbf{x})$ 分别是[电场和磁场](@entry_id:261347)。此方程的物理意义是，[分布函数](@entry_id:145626) $f_s$ 沿着由 Lorentz 力决定的粒子运动轨迹保持不变。

这些电磁场自身则由 Maxwell 方程组决定，其源项——电荷密度 $\rho(t, \mathbf{x})$ 和电流密度 $\mathbf{J}(t, \mathbf{x})$——由所有粒子组分的[分布函数](@entry_id:145626)积分（即取矩）得到：
$$
\rho = \sum_s q_s \int f_s \, \mathrm{d}\mathbf{v}
$$
$$
\mathbf{J} = \sum_s q_s \int \mathbf{v} f_s \, \mathrm{d}\mathbf{v}
$$
完整的 Maxwell 方程组包括：
$$
\nabla \cdot \mathbf{E} = \rho / \varepsilon_0 \quad (\text{Gauss 定理})
$$
$$
\nabla \cdot \mathbf{B} = 0 \quad (\text{磁场无散})
$$
$$
\nabla \times \mathbf{E} = - \frac{\partial \mathbf{B}}{\partial t} \quad (\text{Faraday 定律})
$$
$$
\nabla \times \mathbf{B} = \mu_0 \mathbf{J} + \mu_0 \varepsilon_0 \frac{\partial \mathbf{E}}{\partial t} \quad (\text{Ampère-Maxwell 定律})
$$

由于 Vlasov–Maxwell 方程组是定义在六维相空间上的[非线性偏微分方程](@entry_id:169481)组，直接求解极其困难。**粒子-网格（Particle-In-Cell, PIC）**方法是一种高效的[数值近似](@entry_id:161970)技术，它将连续的[分布函数](@entry_id:145626) $f_s$ 离散为大量计算“宏粒子”（macroparticles）的集合。每个宏粒子代表了相空间中一片区域的真实粒子。其分布函数可近似表示为：
$$
f_s(t,\mathbf{x},\mathbf{v}) \approx \sum_{p \in s} w_{p} S\left(\mathbf{x}-\mathbf{x}_{p}(t)\right) \delta\left(\mathbf{v}-\mathbf{v}_{p}(t)\right)
$$
其中，$p$ 索引所有属于组分 $s$ 的宏粒子，每个宏粒子具有权重 $w_p$、位置 $\mathbf{x}_p(t)$ 和速度 $\mathbf{v}_p(t)$。$\delta$ 是 Dirac delta 函数，表示宏粒子在速度空间是离散的；而 $S(\mathbf{x})$ 是一个有限宽度的**形函数**（shape function），用于在空间上将离散粒子的物理量（如电荷）平滑地分配到周围的网格节点上 。

PIC 模拟的核心是一个[循环过程](@entry_id:146195)，通常称为 **PIC 循环**：
1.  **收集（Gather）**：将定义在空间网格上的电磁场 $\mathbf{E}$ 和 $\mathbf{B}$，通过形函数 $S$ 插值到每个宏粒子的位置 $\mathbf{x}_p$ 上，以计算作用在该粒子上的 Lorentz 力。
2.  **推进（Push）**：根据 Newton-Lorentz [运动方程](@entry_id:264286)，更新每个粒子的速度和位置。这是一个[常微分方程的数值积分](@entry_id:274798)过程：
    $$
    m_p \frac{\mathrm{d}\mathbf{v}_p}{\mathrm{d}t} = q_p\left(\mathbf{E}(\mathbf{x}_p,t) + \mathbf{v}_p \times \mathbf{B}(\mathbf{x}_p,t)\right), \quad \frac{\mathrm{d}\mathbf{x}_p}{\mathrm{d}t} = \mathbf{v}_p
    $$
3.  **散播（Scatter）**：将更新后的粒子信息贡献回网格，通过形函数 $S$ 计算网格节点上的电荷密度 $\rho$ 和电流密度 $\mathbf{J}$。
4.  **场求解（Field Solve）**：以计算得到的 $\rho$ 和 $\mathbf{J}$ 为源项，在网格上求解 Maxwell 方程组，得到新的电磁场分布。

这个循环的[时间积分](@entry_id:267413)方式，即如何从时间步 $t^n$ 推进到 $t^{n+1}$，构成了[显式与隐式方法](@entry_id:168763)的主要区别。

### 显式时间积分：蛙跳法

显式时间积分方法直接利用过去时刻（如 $t^n$ 和 $t^{n-1/2}$）的已知量来计算未来时刻（$t^{n+1}$）的未知量。这种方法的优点是算法简单、计算量小，但其稳定性是有条件的。

#### 场求解器：Yee 氏 FDTD 格式

在电磁 PIC 模拟中，最广泛使用的显式场求解器是 **Yee 氏[有限差分](@entry_id:167874)时域（Finite-Difference Time-Domain, FDTD）** 格式 。其精妙之处在于将电场 $\mathbf{E}$ 和磁场 $\mathbf{B}$ 的不同分量在空间和时间上交[错排](@entry_id:264832)列。

在一个三维[笛卡尔](@entry_id:925811)网格单元中，$\mathbf{E}$ 的分量定义在棱心（edge-centered），而 $\mathbf{B}$ 的分量定义在面心（face-centered）。例如，$E_x$ 分量位于 $(i+1/2, j, k)$，而 $B_x$ 分量位于 $(i, j+1/2, k+1/2)$。这种空间交错布局使得 Faraday 定律和 Ampère-Maxwell 定律中的[旋度算子](@entry_id:184984)可以采用中心差分格式，从而达到二阶空间精度，并且能够精确满足离散的 $\nabla \cdot (\nabla \times \cdot) = 0$ 恒等式。

在时间上，Yee 氏格式采用**蛙跳（leapfrog）**积分：$\mathbf{E}$ 场定义在整数时间步（$t^n = n\Delta t$），而 $\mathbf{B}$ 场定义在半整数时间步（$t^{n \pm 1/2} = (n \pm 1/2)\Delta t$）。这样，Faraday 定律和 Ampère-Maxwell 定律的时间导数也可以采用中心差分，实现了二阶时间精度。

#### 粒子推进器：蛙跳/Boris 算法

为了与场的[蛙跳格式](@entry_id:163462)保持一致，粒子推进器也采用类似的时间交错。粒子位置 $\mathbf{x}_p^n$ 在整数时间步上定义，而速度 $\mathbf{v}_p^{n \pm 1/2}$ 在半整数时间步上定义。一个标准的推进步骤如下：
1.  利用 $t^n$ 时刻的 $\mathbf{E}^n$ 和 $t^{n-1/2}$ 时刻的 $\mathbf{B}^{n-1/2}$ （或通过平均得到的 $t^n$ 时刻的[有效磁场](@entry_id:139861)）计算 Lorentz 力。
2.  将速度从 $\mathbf{v}_p^{n-1/2}$ 推进半步到 $\mathbf{v}_p^{n+1/2}$。**Boris 算法**是实现这一步的常用方法，它能精确地处理磁场引起的旋转运动。
3.  利用新得到的速度 $\mathbf{v}_p^{n+1/2}$，将位置从 $\mathbf{x}_p^n$ 推进整步到 $\mathbf{x}_p^{n+1}$：$\mathbf{x}_p^{n+1} = \mathbf{x}_p^n + \mathbf{v}_p^{n+1/2} \Delta t$。

#### 耦合与电荷守恒

一个完整的显式 PIC 循环将上述步骤结合起来。为了保证模拟的[长期稳定性](@entry_id:146123)和物理真实性，电流密度的散播步骤必须采用**[电荷守恒](@entry_id:264158)**的算法。这意味着离散的[电荷密度](@entry_id:144672) $\rho^n$ 和电流密度 $\mathbf{J}^{n+1/2}$ 必须精确满足离散的[电荷连续性](@entry_id:747292)方程：
$$
\frac{\rho^{n+1} - \rho^n}{\Delta t} + \nabla_h \cdot \mathbf{J}^{n+1/2} = 0
$$
其中 $\nabla_h \cdot$ 是离散[散度算子](@entry_id:265975)。如果这个条件得到满足，那么只要初始时刻的场满足离散的 Gauss 定理（$\nabla_h \cdot \mathbf{E}^n = \rho^n / \varepsilon_0$），该定理在后续所有时间步都将自动保持（在[舍入误差](@entry_id:162651)范围内），从而避免了非物理电荷的累积和由此引发的[数值不稳定性](@entry_id:137058) 。

### 显式方法的稳定性约束

显式方法最大的缺点是其**[条件稳定性](@entry_id:276568)**，即时间步长 $\Delta t$ 必须足够小，以满足若干严格的稳定性判据。

#### [等离子体振荡](@entry_id:268974)约束

[显式积分器](@entry_id:1124772)必须能够解析系统中最高频率的物理振荡。在无磁化或[弱磁](@entry_id:1124938)化的等离子体中，最快的特征时间尺度通常由[电子等离子体振荡](@entry_id:272994)决定，其频率为 $\omega_{pe} = \sqrt{n_e e^2 / (\varepsilon_0 m_e)}$。对[蛙跳法](@entry_id:163462)应用于线性[谐振子](@entry_id:155622)（如 Langmuir 振荡）的稳定性分析表明 ，时间步长必须满足：
$$
\omega_{pe} \Delta t \lesssim 2
$$
这个条件意味着，为了维持数值稳定，时间步长必须远小于[电子等离子体振荡](@entry_id:272994)的周期。对于[高密度等离子体](@entry_id:187441)（如聚变装置的芯部），$\omega_{pe}$ 非常高，这使得 $\Delta t$ 变得极小，导致模拟长时标物理现象的计算成本过高 。

#### Courant–Friedrichs–Lewy (CFL) 条件

对于显式电磁场求解器（如 Yee 氏格式），还存在一个由电磁波在离散网格上传播引起的稳定性约束，即 **Courant–Friedrichs–Lewy (CFL) 条件**。该条件要求在一个时间步内，信息（在此即光波）的传播距离不能超过一个网格单元。对于一个三维立方网格，其最严格的形式为：
$$
\Delta t \le \frac{1}{c\sqrt{\frac{1}{(\Delta x)^2} + \frac{1}{(\Delta y)^2} + \frac{1}{(\Delta z)^2}}}
$$
如果网格间距相等，即 $\Delta x = \Delta y = \Delta z$，则简化为 $\Delta t \le \frac{\Delta x}{c\sqrt{3}}$ 。需要强调的是，静电 PIC 模拟由于不求解波动性的 Maxwell 方程，因此不受此 CFL 条件的限制。

#### 综合约束

一个显式**电磁** PIC 模拟必须**同时**满足上述两个条件。因此，最大允许的时间步长由两者中更严格的一个决定：
$$
\Delta t_{\text{max}} = \min\left( \frac{2}{\omega_{pe}}, \frac{1}{c\sqrt{\frac{1}{(\Delta x)^2} + \frac{1}{(\Delta y)^2} + \frac{1}{(\Delta z)^2}}} \right)
$$
例如，在一个典型的聚变边缘等离子体场景中，若电子密度 $n_e = 7.5 \times 10^{19} \text{ m}^{-3}$，网格尺寸 $\Delta x = 2.5 \text{ mm}$，那么[等离子体振荡](@entry_id:268974)约束给出的 $\Delta t$ 上限约为 $4.09 \times 10^{-12} \text{ s}$，而三维 CFL 条件给出的上限约为 $4.81 \times 10^{-12} \text{ s}$。在这个具体案例中，$\omega_{pe}$ 约束更为严格 。

### [隐式时间积分](@entry_id:171761)：超越稳定性限制

当研究的物理现象时间尺度远大于电子等离子体周期时（例如离子声波、MHD 模），使用显式方法会因为必须满足 $\omega_{pe}$ 约束而浪费大量计算资源。**[隐式时间积分](@entry_id:171761)**方法通过改变算法结构，消除了这些由高频振荡带来的稳定性限制，从而允许使用远大于显式方法所允许的时间步长。

#### 隐式格式的构造

[隐式方法](@entry_id:138537)的核心思想是，在计算 $t^{n+1}$ 时刻的系统状态时，所依赖的力或场源项也取自 $t^{n+1}$ 时刻（或 $t^{n+1/2}$ 时刻）。这导致了一个耦合的、[非线性](@entry_id:637147)的代数方程组，必须在每个时间步迭代求解。

一个典型的二阶时间精度的[隐式格式](@entry_id:166484)是**时间中心隐式格式**（或称 Crank-Nicolson 类型格式）。应用于 PIC 系统，其形式如下 ：
- **[场方程](@entry_id:1124935)**：
$$
\frac{\mathbf{E}^{n+1} - \mathbf{E}^{n}}{\Delta t} = c^2 \nabla \times \mathbf{B}^{n+1/2} - \frac{1}{\varepsilon_0} \mathbf{J}^{n+1/2}
$$
$$
\frac{\mathbf{B}^{n+1} - \mathbf{B}^{n}}{\Delta t} = - \nabla \times \mathbf{E}^{n+1/2}
$$
- **粒子[运动方程](@entry_id:264286)**：
$$
m_p \frac{\mathbf{V}_p^{n+1} - \mathbf{V}_p^{n}}{\Delta t} = q_p \left( \mathbf{E}^{n+1/2}(\mathbf{X}_p^{n+1/2}) + \mathbf{V}_p^{n+1/2} \times \mathbf{B}^{n+1/2}(\mathbf{X}_p^{n+1/2}) \right)
$$
$$
\frac{\mathbf{X}_p^{n+1} - \mathbf{X}_p^{n}}{\Delta t} = \mathbf{V}_p^{n+1/2}
$$
其中，所有位于半时间步 $t^{n+1/2}$ 的量都是 $t^n$ 和 $t^{n+1}$ 时刻对应量的平均值，例如 $\mathbf{E}^{n+1/2} = \frac{1}{2}(\mathbf{E}^{n}+\mathbf{E}^{n+1})$。关键在于，场方程的源项——电流密度 $\mathbf{J}^{n+1/2}$——是由中心化的粒子速度 $\mathbf{V}_p^{n+1/2}$ 和位置 $\mathbf{X}_p^{n+1/2}$ 计算得出的。而这些[粒子动力学](@entry_id:1129385)量又反过来依赖于中心的场 $\mathbf{E}^{n+1/2}$ 和 $\mathbf{B}^{n+1/2}$。因此，所有未知量 $\{\mathbf{E}^{n+1}, \mathbf{B}^{n+1}, \mathbf{X}^{n+1}, \mathbf{V}^{n+1}\}$ 都被耦合在一起，形成一个巨大的非线性方程组。

#### 物理机制：轨道平均与[介电响应](@entry_id:140146)

[隐式方法](@entry_id:138537)为何能绕开 $\omega_{pe}$ 稳定性限制？其物理机制在于，它并不试图解析电子在 $\Delta t$ 时间段内的每一次快速振荡，而是通过自洽求解，捕捉到了粒子对时间平均场的**轨道平均响应**。

当 $\Delta t \gg 1/\omega_{pe}$ 时，电子实际上会在一个时间步内完成多次[等离子体振荡](@entry_id:268974)。隐式算法中的耦合求解过程，在数学上等价于计算了一个离散的、频率和时间步长相关的等离子体极化率或[介电函数](@entry_id:136859) $\tilde{\varepsilon}(\omega, \Delta t)$。这个离散的[介电函数](@entry_id:136859)能够稳定地描述等离子体在高频扰动下的整体[屏蔽效应](@entry_id:136974)，而不是去追踪每一次微观振荡。因此，高频的 Langmuir 振荡被有效地“[时间平均](@entry_id:267915)”或“过滤”掉了，从而解除了必须解析其周期的稳定性束缚 。

### [隐式方法](@entry_id:138537)的特性与挑战

#### [无条件稳定性](@entry_id:145631)

对于线性振荡问题，诸如 Crank-Nicolson 或向后 Euler（Backward Euler）这样的隐式格式通常是**无条件稳定**的。这意味着无论时间步长 $\Delta t$ 取多大，数值解都不会发散。例如，对于真空电磁波，Crank-Nicolson 格式的单步放大因子模为 1，而向后 Euler 格式的模小于 1。这表明前者保持能量，而后者引入[数值耗散](@entry_id:168584)。因此，一个完全隐式的电磁 PIC 格式既不受 $\omega_{pe}$ 约束，也不受 CFL 条件的限制  。

#### 精度与稳定性的权衡

[无条件稳定](@entry_id:146281)不等于无条件精确。这是一个至关重要的区别。虽然[隐式方法](@entry_id:138537)允许使用大的 $\Delta t$ 而不失稳定，但 $\Delta t$ 的选择仍然受到**精度**的制约。
1.  **慢现象解析度**：为了精确模拟一个[特征频率](@entry_id:911376)为 $\omega_s$ 的慢物理过程，时间步长必须远小于其周期，即 $\omega_s \Delta t \ll 1$。
2.  **轨道平均有效性**：轨道平均的物理图像要求粒子在一个时间步[内感受](@entry_id:903863)到的场变化是缓慢的。对于[特征速度](@entry_id:165394)为 $v_s$、空间尺度为 $L_s$ 的慢现象，必须满足粒子位移远小于其波长，即 $|v_s|\Delta t \ll L_s$ 。
3.  **物理过程解析度**：对于具体的物理过程，如电子在磁场中的[回旋运动](@entry_id:204632)，也需要足够的[时间分辨率](@entry_id:194281)来避免过大的相位误差。例如，要将 Boris 算法或 Crank-Nicolson 格式对电子[回旋运动](@entry_id:204632)的[相位误差](@entry_id:162993)控制在 5% 以内，需要满足 $\Omega_e \Delta t \lesssim 0.8$，其中 $\Omega_e = eB/m_e$ 是[电子回旋频率](@entry_id:203398)。在 $B_0=5 \text{ T}$ 的强磁场中，这意味着 $\Delta t$ 需在皮秒（$10^{-12}$ s）量级 。

#### [数值阻尼](@entry_id:166654)与[数值加热](@entry_id:1128967)

不同的隐式格式具有不同的耗散特性。如前所述，Crank-Nicolson 格式是无耗散的，而向后 Euler 格式则会引入随 $\omega \Delta t$ 增大的[数值阻尼](@entry_id:166654)。这种阻尼有时是有益的，可以抑制由离散化和有限粒子数引起的、非物理的高频[数值噪声](@entry_id:1128984)。

[数值加热](@entry_id:1128967)是 PIC 模拟中的一个重要问题，它源于粒子与离散网格上非物理的场涨落（即网格噪声）的相互作用。在显式方法中，这些高频噪声未被抑制，可能导致粒子动能的持续、非物理性增长。而[隐式方法](@entry_id:138537)，特别是那些具有[数值阻尼](@entry_id:166654)的格式，可以通过在大时间步下衰减高频场分量，来显著降低[数值加热](@entry_id:1128967)率 。

### 求解隐式系统：Newton-Krylov 方法

[隐式方法](@entry_id:138537)最大的挑战在于求解每个时间步中出现的庞大、耦合的非线性方程组 $\mathbf{R}(\mathbf{U}) = \mathbf{0}$，其中 $\mathbf{U}$ 代表所有场和粒子的未知自由度。

对于这类问题，**Newton-Krylov (NK)** 方法是当前最先进的求解策略。这是一个两层迭代过程：
- **外层（Newton 迭代）**：使用牛顿法[求解非线性方程](@entry_id:177343)。在第 $k$ 次迭代，通过求解一个线性方程组来计算更新量 $\delta \mathbf{U}$：
$$
\mathbf{J}(\mathbf{U}_k) \delta \mathbf{U} = -\mathbf{R}(\mathbf{U}_k)
$$
其中 $\mathbf{J} = \partial \mathbf{R} / \partial \mathbf{U}$ 是系统的 **Jacobian 矩阵**。
- **内层（Krylov 迭代）**：由于 Jacobian 矩阵极其巨大，且在 PIC 中是稠密的（因为每个粒子都与所有场自由度耦合），直接构造或求逆是不现实的。**[Krylov 子空间方法](@entry_id:144111)**（如 GMRES）被用来迭代求解这个线性系统。Krylov 方法的优点是它不需要 Jacobian 矩阵本身，只需要计算该矩阵与一个任意向量 $\mathbf{v}$ 的乘积，即**矩阵-[向量积](@entry_id:156672)** $\mathbf{Jv}$。

这引出了 **无 Jacobian 的 [Newton-Krylov](@entry_id:752475) (Jacobian-Free Newton-Krylov, JFNK)** 方法。其核心思想是，利用有限差分来[近似计算](@entry_id:1121073)所需的矩阵-向量积 ：
$$
\mathbf{J}(\mathbf{U}_k) \mathbf{v} \approx \frac{\mathbf{R}(\mathbf{U}_k + \epsilon \mathbf{v}) - \mathbf{R}(\mathbf{U}_k)}{\epsilon}
$$
其中 $\epsilon$ 是一个需要仔细选择的小参数。

在隐式 PIC 的背景下，JFNK 方法的计算代价体现在**残差函数 $\mathbf{R}(\cdot)$ 的求值**上。为了计算 JFNK 中的近似矩阵-向量积，每当 Krylov 迭代器需要一个新的 $\mathbf{Jv}$ 时，程序就必须：
1.  给定一个微扰后的场 $\mathbf{U}_k + \epsilon \mathbf{v}$。
2.  在此微扰场的作用下，重新计算**所有粒子**从 $t^n$到 $t^{n+1}$ 的完整运动轨迹。
3.  根据新的[粒子轨迹](@entry_id:204827)，重新将电荷和电流散播到网格上。
4.  用这些新的源项，计算并返回残差 $\mathbf{R}(\mathbf{U}_k + \epsilon \mathbf{v})$。

这个过程的计算成本非常高，但它精确地包含了粒子响应对场的依赖关系（即 $\partial \mathbf{J} / \partial \mathbf{E}$ 等项），这是牛顿法能够实现快速收敛（理想情况下为二次收敛）的保证。正是这种复杂的算法结构，使得隐式 PIC 能够在单个时间步内稳定地跨越显式方法无法企及的时间尺度。