## 引言
塑性功与[能量耗散](@entry_id:147406)是理解材料在超过其[弹性极限](@entry_id:186242)后行为的核心概念。当结构构件发生永久变形时，外力所做的功究竟去了哪里？一部分转化为热量，另一部分改变了材料的内部状态，但如何精确地量化这一过程，并将其与材料的[硬化](@entry_id:177483)、损伤及最终失效联系起来，是固体力学研究中的一个根本问题。本文旨在填补这一认知空白，通过建立一个从基本物理定律出发的严谨分析框架，系统地揭示机械功在塑性变形过程中的转化路径与分配机制。

在接下来的内容中，我们将分三个章节展开探讨。首先，在“原理与机制”一章中，我们将从连续介质力学和[热力学](@entry_id:141121)的基本公理出发，推导能量耗散的核心方程，并阐明关联流动、[硬化](@entry_id:177483)模型等在[能量分配](@entry_id:748987)中的作用。随后，在“应用与交叉学科联系”一章，我们将展示这些原理如何在结构[失效分析](@entry_id:266723)、断裂力学、疲劳预测和材料加工等多个工程与科学领域中发挥关键作用。最后，“动手实践”部分将通过具体的计算问题，帮助读者将理论知识转化为解决实际问题的能力。让我们首先深入第一章，探索塑性功与耗散的内在原理与机制。

## 原理与机制

本章旨在深入探讨塑性变形过程中的核心[热力学](@entry_id:141121)概念：塑性功与能量耗散。我们将从[连续介质力学](@entry_id:155125)的基本公理出发，建立一个严格的理论框架，用以描述机械功如何转化为材料内部的存储能和热量。通过这一过程，我们将揭示关联塑性、硬化模型以及[非关联流动](@entry_id:199220)等关键机制在能量转化过程中的作用。

### 连续介质中的功率与功

在研究能量耗散之前，我们必须首先精确定义力学功率。在连续介质力学中，单位体积的[内力](@entry_id:167605)所做的功率，即**[应力功率](@entry_id:182907)密度**（stress power density），是理解材料变形过程中能量转化的起点。在当前构型（或[欧拉描述](@entry_id:264722)）下，[应力功率](@entry_id:182907)密度 $w_i$ 由柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 和变形率张量 $\mathbf{D}$ 的[双点积](@entry_id:748648)给出：

$w_i = \boldsymbol{\sigma} : \mathbf{D}$

其中，$\mathbf{D}$ 是[速度梯度](@entry_id:261686) $\mathbf{L} = \nabla \mathbf{v}$ 的对称部分，即 $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\mathsf{T}})$。这个表达式代表了应力在材料点上瞬时变形所做的功的速率。

一个基本原理是，总内功率的计算与观察者的[坐标系](@entry_id:156346)无关，即它在参考构型（[拉格朗日描述](@entry_id:264498)）和当前构型下的积分结果应当是相同的。这引出了**[功共轭](@entry_id:194957)**（work-conjugate）的概念，即不同构型下的[应力张量](@entry_id:148973)和[应变率张量](@entry_id:266108)配对，以保持功率表达式的[不变性](@entry_id:140168) 。通过体积微元的关系 $dv = J dV_0$（其中 $J = \det \mathbf{F}$ 是变形梯度 $\mathbf{F}$ 的[雅可比行列式](@entry_id:137120)），我们可以推[导出单位](@entry_id:141082)参考体积的[应力功率](@entry_id:182907)密度 $w_{i,0}$ 的几种等价形式：

$w_{i,0} = J(\boldsymbol{\sigma} : \mathbf{D}) = \boldsymbol{\tau} : \mathbf{D} = \mathbf{P} : \dot{\mathbf{F}} = \mathbf{S} : \dot{\mathbf{E}}$

这里，$\boldsymbol{\tau} = J\boldsymbol{\sigma}$ 是基尔霍夫（Kirchhoff）应力张量，$\mathbf{P}$ 是第一皮奥拉-基尔霍夫（Piola-Kirchhoff）应力张量，$\mathbf{S}$ 是第二皮奥拉-基尔霍夫（Piola-Kirchhoff）[应力张量](@entry_id:148973)，而 $\dot{\mathbf{E}}$ 是格林-拉格朗日（Green-Lagrange）[应变张量](@entry_id:193332) $\mathbf{E}$ 的[物质时间导数](@entry_id:190892)。这些关系式构成了有限变形理论中功与功率计算的基石。

对于本章主要关注的**小应变理论**，情况得以简化。当变形足够小时，$\mathbf{F} \approx \mathbf{I}$，$J \approx 1$，且变形率张量 $\mathbf{D}$ 近似等于[小应变张量](@entry_id:754968) $\boldsymbol{\varepsilon}$ 的[物质时间导数](@entry_id:190892) $\dot{\boldsymbol{\varepsilon}}$。因此，单位体积的[应力功率](@entry_id:182907)密度可以直接写为：

$w_i \approx \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}$

这个简化的表达式是小应变塑性理论中分析塑性功的基础 。

### 耗散的[热力学](@entry_id:141121)根源

机械功的最终去向由[热力学定律](@entry_id:202285)决定。塑性变形的不[可逆性](@entry_id:143146)本质上是一个[热力学过程](@entry_id:141636)，其中一部分机械功被耗散为热量。为了精确描述这一过程，我们引入局部形式的[热力学](@entry_id:141121)第一和第二定律。

**热力学第一定律**（[能量守恒](@entry_id:140514)）的局部形式为：
$\rho \dot{e} = \boldsymbol{\sigma}:\mathbf{D} - \nabla \cdot \mathbf{q} + \rho r$

**热力学第二定律**（[熵增原理](@entry_id:142282)）的局部形式，即克劳修斯（Clausius）不等式，要求熵的产生率非负：
$\rho \dot{s} \ge - \nabla \cdot (\frac{\mathbf{q}}{T}) + \frac{\rho r}{T}$

其中，$\rho$ 是质量密度，$e$ 是单位质量的内能，$s$ 是单位质量的熵，$\mathbf{q}$ 是热流矢量，$r$ 是单位质量的体积热源，$T$ 是绝对温度。

为了将力学变量与[热力学状态](@entry_id:755916)联系起来，我们引入单位质量的**[亥姆霍兹自由能](@entry_id:136442)**（Helmholtz free energy）$\psi \equiv e - Ts$。对其求[物质时间导数](@entry_id:190892)，并结合第一定律，我们可以推导出著名的**克劳修斯-杜亥姆（Clausius-Duhem）不等式** ：

$\mathcal{D} = \boldsymbol{\sigma}:\mathbf{D} - \rho(\dot{\psi} + s\dot{T}) - \frac{1}{T}\mathbf{q} \cdot \nabla T \ge 0$

这个不等式是连续介质[热力学](@entry_id:141121)的核心。左侧的量 $\mathcal{D}$ 定义为**局部耗散密度**（local dissipation density），它代表了在材料点上由不可逆过程（如塑性变形和热传导）所导致的能量耗散率，并且根据热力学第二定律，它必须是非负的。这个总耗散 $\mathcal{D}$ 可以分为两部分：

1.  **力学耗散** $\mathcal{D}_{\mathrm{mech}} = \boldsymbol{\sigma}:\mathbf{D} - \rho(\dot{\psi} + s\dot{T})$，与材料的内部结构变化和变形有关。
2.  **热耗散** $\mathcal{D}_{\mathrm{th}} = - \frac{1}{T}\mathbf{q} \cdot \nabla T$，与温差引起的[热传导](@entry_id:147831)有关。

总的熵产生率密度 $\xi$ 与总耗散 $\mathcal{D}$ 之间存在直接关系 $\xi = \mathcal{D}/T$ 。这清楚地表明，机械功的耗散过程是熵产生的直接来源，其物理表现即为热量的生成。

### 等温[弹塑性](@entry_id:193198)过程中的功与耗散

现在，我们将上述[一般性](@entry_id:161765)框架应用于等温（$\dot{T}=0, \nabla T = \mathbf{0}$）、小应变[弹塑性](@entry_id:193198)材料。这是大多数工程金属在准静态加载下行为的良好近似。在此条件下，热耗散项为零，克劳修斯-杜亥姆不等式简化为纯力学形式：

$\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\Psi} \ge 0$

其中 $\Psi$ 是单位体积的亥姆霍兹自由能。

为了区分弹性和塑性行为，我们引入**应变加法分解**的基本假设，即总应变张量 $\boldsymbol{\varepsilon}$ 可以分解为弹性部分 $\boldsymbol{\varepsilon}^e$ 和塑性部分 $\boldsymbol{\varepsilon}^p$ 之和 ：

$\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p$

我们进一步假设自由能是[弹性应变](@entry_id:189634)和一组代表[材料微观结构](@entry_id:198422)状态（如位错密度、晶粒硬化等）的**内变量** $\boldsymbol{\alpha}$ 的函数，即 $\Psi = \Psi(\boldsymbol{\varepsilon}^e, \boldsymbol{\alpha})$。

将 $\dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^e + \dot{\boldsymbol{\varepsilon}}^p$ 和 $\dot{\Psi} = \frac{\partial \Psi}{\partial \boldsymbol{\varepsilon}^e}:\dot{\boldsymbol{\varepsilon}}^e + \frac{\partial \Psi}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}}$ 代入[耗散不等式](@entry_id:188634)，并应用经典的 Coleman-Noll 论证方法，我们可以得到两个关键结果  ：

1.  **超弹性应力关系**: 应力由自由能对弹性应变的[偏导数](@entry_id:146280)给出。
    $\boldsymbol{\sigma} = \frac{\partial \Psi}{\partial \boldsymbol{\varepsilon}^e}$

2.  **简化[耗散不等式](@entry_id:188634)**:
    $\mathcal{D}_{int} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p - \frac{\partial \Psi}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}} \ge 0$

这个不等式揭示了塑性功的最终分配。我们定义：

- **塑性[功率密度](@entry_id:194407)**（Plastic Power Density），$\dot{W}_p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p$。这是应力在塑性应变率上所做的总功率。

- **存储能变化率**（Stored Energy Rate），$\dot{W}_{\mathrm{stored}} = \frac{\partial \Psi}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}}$。这部分塑性功被用来改变材料的微观结构，例如增加[位错密度](@entry_id:161592)，从而导致[加工硬化](@entry_id:160669)。这部分能量以自由能的形式“储存”在材料中。

- **塑性产热率**（Heat Generation Rate due to Plasticity），$\dot{Q}_{\mathrm{plastic}} = \mathcal{D}_{int} = \dot{W}_p - \dot{W}_{\mathrm{stored}}$。这部分塑性功是不可逆地耗散掉的，并根据热力学第一定律转化为热能，导致材料温度升高。

因此，塑性功率被分配为两部分：一部分用于硬化材料（存[储能](@entry_id:264866)），另一部分则以热的形式耗散掉。

$\dot{W}_p = \dot{W}_{\mathrm{stored}} + \dot{Q}_{\mathrm{plastic}}$

为了量化这种分配，[G. I. Taylor](@entry_id:266667) 和 H. Quinney 引入了一个[无量纲参数](@entry_id:169335)，即**[泰勒-奎尼因子](@entry_id:194704)**（Taylor-Quinney factor）$\beta$：

$\beta = \frac{\dot{Q}_{\mathrm{plastic}}}{\dot{W}_p} = 1 - \frac{\dot{W}_{\mathrm{stored}}}{\dot{W}_p}$

$\beta$ 代表了塑性功中转化为热量的比例。对于发生[加工硬化](@entry_id:160669)的材料，$\dot{W}_{\mathrm{stored}} > 0$，因此 $\beta  1$。对于不发生[硬化](@entry_id:177483)的[理想塑性](@entry_id:753335)材料，$\dot{W}_{\mathrm{stored}} = 0$，所有塑性功都转化为热量，即 $\beta = 1$。实验测量表明，对于大多数金属，$\beta$ 的值通常在 $0.9$到$1.0$之间，这意味着绝大部分塑性功都以热的形式耗散掉了 。

### [塑性流动](@entry_id:201346)的机制与计算

上述[热力学](@entry_id:141121)框架为我们理解塑性功的分配提供了原理，但要进行具体计算，我们还需要描述塑性流动如何发生的力学模型。

#### [屈服面](@entry_id:175331)与流动法则

率无关塑性理论的核心是**[屈服函数](@entry_id:167970)** $f(\boldsymbol{\sigma}, \kappa)$，它定义了一个[应力空间](@entry_id:199156)中的弹性区域 $\mathcal{E}(\kappa) = \{\boldsymbol{\sigma} | f(\boldsymbol{\sigma}, \kappa) \le 0\}$。其中 $\kappa$ 是代表[硬化](@entry_id:177483)状态的标量或张量内变量。塑性流动只有在应力状态位于屈服面上（$f=0$）时才可能发生。这一系列的加载/卸载条件可以用**库恩-塔克（Kuhn-Tucker）条件**优雅地表述 ：

$\lambda \ge 0, \quad f(\boldsymbol{\sigma}, \kappa) \le 0, \quad \lambda f(\boldsymbol{\sigma}, \kappa) = 0$

这里，$\lambda$ 是一个非负的**塑性乘子**（或称为一致性参数）。$\lambda f = 0$ 的[互补条件](@entry_id:747558)确保了当应力在弹性域内（$f0$）时，$\lambda=0$，无塑性流动；而当发生[塑性流动](@entry_id:201346)（$\lambda>0$）时，应力状态必须保持在屈服面上（$f=0$）。为了在塑性加载过程中始终满足 $f=0$，还必须满足**[一致性条件](@entry_id:637057)** $\lambda \dot{f} = 0$。

#### 关联流动与 J2 塑性

对于大多数金属，一个被广泛接受的假设是**关联[流动法则](@entry_id:177163)**（associated flow rule），即塑性应变率的方向与[屈服函数](@entry_id:167970)对应力的梯度方向一致：

$\dot{\boldsymbol{\varepsilon}}^p = \lambda \frac{\partial f}{\partial \boldsymbol{\sigma}}$

这在几何上意味着塑性[应变率](@entry_id:154778)矢量 $\dot{\boldsymbol{\varepsilon}}^p$ 垂直于[屈服面](@entry_id:175331)，这也被称为**法向法则**（normality rule）。

一个重要的特例是金属材料常用的**von Mises（或 J2）塑性理论**。其[屈服函数](@entry_id:167970)仅依赖于[偏应力张量](@entry_id:267642) $\boldsymbol{s} = \boldsymbol{\sigma} - \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})\mathbf{I}$：

$f(\boldsymbol{\sigma}, \kappa) = \sigma_{\mathrm{eq}} - \sigma_y(\kappa) = \sqrt{\frac{3}{2}\boldsymbol{s}:\boldsymbol{s}} - \sigma_y(\kappa)$

其中 $\sigma_{\mathrm{eq}}$ 是 von Mises [等效应力](@entry_id:749064)，$\sigma_y$ 是当前的[屈服应力](@entry_id:274513)。关联[流动法则](@entry_id:177163)给出的塑性[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}^p = \lambda \frac{3}{2} \frac{\boldsymbol{s}}{\sigma_{\mathrm{eq}}}$ 是一个纯偏量张量，即 $\operatorname{tr}(\dot{\boldsymbol{\varepsilon}}^p)=0$。这表明 J2 塑性流动是**体积不可压缩**的。

这一特性对塑性功有直接影响。由于[静水压力](@entry_id:275365)部分 $\frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})\mathbf{I}$ 与纯偏量张量 $\dot{\boldsymbol{\varepsilon}}^p$ 的[双点积](@entry_id:748648)为零，因此[静水压力](@entry_id:275365)不做塑性功。塑性功率完全由偏应力贡献 ：

$\dot{W}_p = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p = (\boldsymbol{s} + \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})\mathbf{I}):\dot{\boldsymbol{\varepsilon}}^p = \boldsymbol{s}:\dot{\boldsymbol{\varepsilon}}^p$

通过进一步推导，可以得到一个极为有用的塑性功率计算公式 ：

$\dot{W}_p = \sigma_{\mathrm{eq}} \dot{\bar{\varepsilon}}^p$

其中 $\dot{\bar{\varepsilon}}^p = \sqrt{\frac{2}{3}\dot{\boldsymbol{\varepsilon}}^p:\dot{\boldsymbol{\varepsilon}}^p}$ 是等效塑性应变率。这个公式将宏观的功率与材料的[等效应力](@entry_id:749064)-应变行为直接联系起来。例如，考虑一个处于屈服状态的材料点，其 von Mises [等效应力](@entry_id:749064)为 $\sigma_{\mathrm{eq}} = \sigma_y = 290 \text{ MPa}$，若塑性乘子为 $\lambda = 4.37 \text{ s}^{-1}$，则塑性[功率密度](@entry_id:194407)为 $\mathcal{D} = \lambda \sigma_y = 4.37 \times 290 \approx 1267 \text{ MW/m}^3$ 。同样，如果已知一个材料点的应力状态（例如 $\sigma_{\mathrm{eq}} = \sqrt{13500} \text{ MPa}$）和等效塑性应变率（例如 $\dot{\bar{\varepsilon}}^p = 7.20 \times 10^{-4} \text{ s}^{-1}$），我们可以直接计算[塑性耗散](@entry_id:201273)功率为 $\mathcal{D}_p = \sigma_{\mathrm{eq}}\dot{\bar{\varepsilon}}^p \approx 0.08366 \text{ MW/m}^3$ 。

对于一个具有线性[各向同性硬化](@entry_id:164486)的材料，其自由能中的[硬化](@entry_id:177483)部分可写为 $\Psi_{\mathrm{hard}}(\alpha) = \frac{1}{2}H\alpha^2$，其中 $\alpha$ 是累积塑性应变，H是硬化模量。[屈服应力](@entry_id:274513)为 $\sigma_{\mathrm{eq}} = \sigma_{y0} + H\alpha$。在这种情况下，存储能的变化率为 $\dot{W}_{\mathrm{stored}} = H\alpha\dot{\alpha}$，而塑性功为 $\dot{W}_p = (\sigma_{y0} + H\alpha)\dot{\alpha}$。因此，[泰勒-奎尼因子](@entry_id:194704)可以表示为当前应力状态的函数 ：

$\beta = 1 - \frac{H\alpha}{\sigma_{y0} + H\alpha}$

### 高级主题：[非关联流动](@entry_id:199220)与[材料稳定性](@entry_id:183933)

关联流动法则（$g=f$）不仅是一个方便的数学假设，它还具有深刻的物理意义。对于[凸屈服面](@entry_id:203690)，关联流动自动保证了[塑性耗散](@entry_id:201273)的非负性，即 $\dot{W}_p = \lambda \boldsymbol{\sigma} : \frac{\partial f}{\partial \boldsymbol{\sigma}} \ge 0$，这是[Drucker稳定性公设](@entry_id:200080)的一个推论。

然而，对于某些材料，如土壤、岩石和混凝土，实验观察到的塑性流动方向与[屈服面](@entry_id:175331)的法线方向并不一致。这类行为需要通过**[非关联流动法则](@entry_id:752544)**（non-associated flow rule）来描述，即引入一个不同于[屈服函数](@entry_id:167970)的**塑性[势函数](@entry_id:176105)** $g(\boldsymbol{\sigma}, \kappa)$：

$\dot{\boldsymbol{\varepsilon}}^p = \lambda \frac{\partial g}{\partial \boldsymbol{\sigma}}$

在这种情况下，塑性功率为 $\mathcal{D}_p = \lambda (\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}})$。热力学第二定律的非负耗散要求 $\mathcal{D}_p \ge 0$ 不再被自动满足，它成为了对塑性[势函数](@entry_id:176105) $g$ 的一个严格约束 ：

$\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}} \ge 0$

这个条件必须在所有可能的[屈服应力](@entry_id:274513)状态下都成立。一个足以保证该条件的做法是，选择一个在[屈服面](@entry_id:175331)上取值非负且对应力是一次正齐次的函数 $g$。根据[欧拉齐次函数定理](@entry_id:186434)，$\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}} = g(\boldsymbol{\sigma}) \ge 0$，从而保证了耗散的非负性 。

若此条件被违反，例如对于一个受高围压的压力敏感材料，其塑性[势函数](@entry_id:176105)可能导致 $\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}}  0$。这将意味着 $\mathcal{D}_p  0$，即材料在塑性变形时会从外界“吸能”，这对应于材料的失稳，如[应变软化](@entry_id:755491)或[剪切带](@entry_id:183352)的形成。因此，[非关联流动](@entry_id:199220)模型虽然能更准确地描述某些材料的[运动学](@entry_id:173318)行为，但必须谨慎使用，以确保其在所应用的应力范围内满足[热力学一致性](@entry_id:138886) 。