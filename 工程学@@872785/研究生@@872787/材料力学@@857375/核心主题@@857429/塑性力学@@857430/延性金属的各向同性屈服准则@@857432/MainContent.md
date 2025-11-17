## 引言
在工程设计与[材料分析](@entry_id:161282)中，准确预测[延性](@entry_id:160108)金属何时从弹性变形过渡到永久的塑性变形至关重要。[各向同性屈服准则](@entry_id:204294)正是解决这一核心问题的理论基石，它为复杂应力状态下的材料行为提供了数学描述。然而，如何将简单的[单轴拉伸](@entry_id:188287)实验结果推广到普遍的三维应力状态，并建立一个既有坚实物理基础又便于工程应用的数学框架，是[固体力学](@entry_id:164042)面临的一个基本挑战。

本文旨在系统性地阐述延性金属的各向同性屈服理论。在“原理与机制”一章中，我们将从[连续介质力学](@entry_id:155125)的基本公理出发，推导出经典的von Mises和[Tresca屈服准则](@entry_id:190718)，并探讨它们的物理内涵与几何表示。接下来，在“应用与跨学科关联”一章中，我们将展示这些准则在解决从[压力容器设计](@entry_id:184353)到结构安全评估等实际工程问题中的应用，并揭示其与[断裂力学](@entry_id:141480)、[损伤力学](@entry_id:178377)及[材料科学](@entry_id:152226)等领域的深刻联系。最后，通过“动手实践”部分，读者将有机会通过具体问题加深对核心概念的理解和应用能力。

## 原理与机制

本章旨在深入探讨延性金属的[各向同性屈服准则](@entry_id:204294)。我们将从连续介质力学的基本原理出发，建立描述[材料屈服](@entry_id:751736)行为的数学框架。随后，我们将详细阐述两个核心的屈服准则——von Mises 准则和 Tresca 准则，分析它们的物理基础、几何表示和应用。最后，我们将讨论这些模型的扩展，如[硬化](@entry_id:177483)规律，并对它们的理论和计算方面进行比较。

### [屈服函数](@entry_id:167970)的公理化基础

在塑性力学中，**[屈服函数](@entry_id:167970)** $f(\boldsymbol{\sigma})$ 是一个标量函数，它定义了材料从弹性变形过渡到塑性变形的应力边界。当 $f(\boldsymbol{\sigma})  0$ 时，材料处于弹性状态；当 $f(\boldsymbol{\sigma}) = 0$ 时，材料达到屈服极限，开始发生塑性流动；而 $f(\boldsymbol{\sigma}) > 0$ 则代表在率无关塑性模型中不可及的应力状态。为了建立一个适用于各向同性材料的普适性[屈服函数](@entry_id:167970)，我们必须遵循两条基本物理原理：**[材料客观性](@entry_id:177919)**（或称**物质[坐标无关性](@entry_id:159715)**）和**材料各向同性**。

**客观性**原理要求[本构关系](@entry_id:186508)在任意叠加的刚体运动（即观察者变换）下保持不变。对于仅依赖于当前柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的[屈服函数](@entry_id:167970)，这意味着在任意旋转下，函数值应保持不变。若一个旋转由一个正交张量 $\mathbf{Q}$ ($\mathbf{Q}^{\top}\mathbf{Q}=\boldsymbol{I}, \det\mathbf{Q}=+1$) 表示，则[应力张量](@entry_id:148973)变换为 $\mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^{\top}$。因此，客观性要求：

$f(\mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^{\top}) = f(\boldsymbol{\sigma})$

[@problem_id:2896249]

**各向同性**原理指出，材料本身没有优选方向。对于一个各向同性的标量函数，其数学表达形式与客观性要求一致。根据张量函数的[表示定理](@entry_id:637872)，任何满足此[不变性](@entry_id:140168)要求的、以对称二阶张量为变量的标量函数，必然可以表示为其[主不变量](@entry_id:193522)的函数。

柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 是一个对称二阶张量，它有三个实数[特征值](@entry_id:154894)，称为**主应力**，记为 $\sigma_1, \sigma_2, \sigma_3$。这些[主应力](@entry_id:176761)是与[坐标系](@entry_id:156346)选择无关的内在量。因此，任何各向同性[屈服函数](@entry_id:167970)都可以表示为这三个[主应力](@entry_id:176761)的[对称函数](@entry_id:177113) $f(\boldsymbol{\sigma}) = G(\sigma_1, \sigma_2, \sigma_3)$ [@problem_id:2896249]。根据[对称多项式基本定理](@entry_id:152306)，这等价于将[屈服函数](@entry_id:167970)表示为应力张量[主不变量](@entry_id:193522)的函数：

$f(\boldsymbol{\sigma}) = \hat{F}(I_1, I_2, I_3)$

其中，三个**主[应力[不变](@entry_id:170526)量](@entry_id:148850)**定义为：
- 第一[不变量](@entry_id:148850)：$I_1 = \operatorname{tr}(\boldsymbol{\sigma}) = \sigma_1 + \sigma_2 + \sigma_3$
- 第二[不变量](@entry_id:148850)：$I_2 = \frac{1}{2}[(\operatorname{tr}\boldsymbol{\sigma})^2 - \operatorname{tr}(\boldsymbol{\sigma}^2)] = \sigma_1\sigma_2 + \sigma_2\sigma_3 + \sigma_3\sigma_1$
- 第三[不变量](@entry_id:148850)：$I_3 = \det(\boldsymbol{\sigma}) = \sigma_1\sigma_2\sigma_3$

这些[不变量](@entry_id:148850)的集合构成了描述应力状态的一个[完备基](@entry_id:143908)。

### 静水压力无关性与应力偏量

大量实验证据表明，[延性](@entry_id:160108)金属的屈服行为在很大程度上不受**[静水压力](@entry_id:275365)**（hydrostatic pressure）的影响。例如，在纯剪切实验中叠加一个巨大的[静水压力](@entry_id:275365)，测得的初始屈服剪应力几乎不变 [@problem_id:2896219]。这一现象有其深刻的物理根源。

从微观机制上看，[延性](@entry_id:160108)金属的塑性变形主要由[位错](@entry_id:157482)在晶体[滑移面](@entry_id:158709)上的滑移驱动。位错运动的驱动力是滑移面上的**分解剪应力**。一个纯[静水压力](@entry_id:275365)状态，其[应力张量](@entry_id:148973)为 $\boldsymbol{\sigma} = -p\boldsymbol{I}$（其中 $p$ 为压力），在任何平面上产生的牵[引力](@entry_id:175476)都垂直于该平面，不产生任何剪切分量。因此，[静水压力](@entry_id:275365)本身无法驱动[位错滑移](@entry_id:275474)，也无法单独引起塑性屈服 [@problem_id:2711750]。

从[热力学](@entry_id:141121)角度看，金属的塑性变形过程近似为体积不可压缩的，即塑性应变率张量 $\dot{\boldsymbol{\varepsilon}}^p$ 的迹为零，$\mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p) \approx 0$。单位体积的塑性功率耗散为 $\dot{D}^p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p$。将应力张量分解为球量[部分和](@entry_id:162077)偏量部分，这一概念将在下文详述，我们发现[静水压力](@entry_id:275365)部分所做的功为 $p\boldsymbol{I} : \dot{\boldsymbol{\varepsilon}}^p = p \, \mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p) \approx 0$。这意味着[塑性耗散](@entry_id:201273)几乎完全由非[静水压力](@entry_id:275365)部分贡献，因此屈服条件理应与静水压力无关 [@problem_id:2896219] [@problem_id:2711750]。

为了在数学上精确描述这种压力无关性，我们引入[应力张量](@entry_id:148973)的**[静水-偏应力分解](@entry_id:196441)**。任何一个对称[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 都可以唯一地分解为一个球形张量（[静水应力](@entry_id:186327)部分）和一个迹为零的张量（**[偏应力张量](@entry_id:267642)** $\boldsymbol{s}$）之和 [@problem_id:2896244]：

$\boldsymbol{\sigma} = \boldsymbol{s} + p\boldsymbol{I}$

其中，**[平均应力](@entry_id:751819)**或**[静水应力](@entry_id:186327)** $p$ 定义为 $p = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma}) = \frac{1}{3}I_1$。[偏应力张量](@entry_id:267642) $\boldsymbol{s}$ 则为 $\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}$。通过取迹运算可以验证 $\mathrm{tr}(\boldsymbol{s}) = \mathrm{tr}(\boldsymbol{\sigma}) - \mathrm{tr}(p\boldsymbol{I}) = I_1 - 3p = 0$，证明 $\boldsymbol{s}$ 确实是迹为零的。

这个分解的意义在于，球量部分 $p\boldsymbol{I}$ 引起体积变化，而偏量部分 $\boldsymbol{s}$ 引起形状变化（畸变）。压力无关性的假设，意味着屈服仅由引起形状变化的[偏应力张量](@entry_id:267642) $\boldsymbol{s}$ 决定。对一个应力张量叠加任意大小的[静水压力](@entry_id:275365) $\sigma_H \boldsymbol{I}$，新的[应力张量](@entry_id:148973)为 $\boldsymbol{\sigma}' = \boldsymbol{\sigma} + \sigma_H \boldsymbol{I}$。其平均应力变为 $p' = p + \sigma_H$，但其[偏应力张量](@entry_id:267642)保持不变：$\boldsymbol{s}' = \boldsymbol{\sigma}' - p'\boldsymbol{I} = (\boldsymbol{\sigma} + \sigma_H \boldsymbol{I}) - (p+\sigma_H)\boldsymbol{I} = \boldsymbol{\sigma} - p\boldsymbol{I} = \boldsymbol{s}$ [@problem_id:2896271]。

因此，一个压力无关的各向同性[屈服函数](@entry_id:167970)，其变量不能包含 $I_1$，而只能是[偏应力张量](@entry_id:267642) $\boldsymbol{s}$ 的[不变量](@entry_id:148850)。$\boldsymbol{s}$ 的[主不变量](@entry_id:193522)通常记为 $J_1, J_2, J_3$。其中 $J_1 = \mathrm{tr}(\boldsymbol{s}) = 0$。最重要的两个是：
- **[偏应力](@entry_id:163323)第二[不变量](@entry_id:148850)**：$J_2 = \frac{1}{2}\mathrm{tr}(\boldsymbol{s}^2) = \frac{1}{2}s_{ij}s_{ij}$
- **偏应力第三[不变量](@entry_id:148850)**：$J_3 = \det(\boldsymbol{s})$

故，任何压力无关的各向同性[屈服函数](@entry_id:167970)的通用形式可以写为 $\Phi(J_2, J_3) = 0$ [@problem_id:2896282]。

### von Mises (J2) [屈服准则](@entry_id:193897)

von Mises 屈服准则，也称为最大[畸变能](@entry_id:198925)密度准则或 $J_2$ 流动理论，是描述[延性](@entry_id:160108)[金属屈服](@entry_id:195134)行为最常用和最成功的模型之一。

#### 定义与物理诠释

von Mises 准则假定，当材料内某点的弹性[畸变能](@entry_id:198925)密度达到一个临界值时，材料就开始屈服。对于线弹性各向同性材料，单位体积的弹性[畸变能](@entry_id:198925)密度 $U_d$ 可以表示为：

$U_d = \frac{1}{2G} J_2$

其中 $G$ 是剪切模量。由于 $G$ 是材料常数，这个能量准则等价于假定当 $J_2$ 达到一个临界值时发生屈服 [@problem_id:2711750] [@problem_id:2896264]。该准则的[屈服函数](@entry_id:167970)可以写为：

$f(\boldsymbol{\sigma}) = \sigma_{\text{eq}} - \sigma_Y = 0$

这里，$\sigma_Y$ 是通过[单轴拉伸](@entry_id:188287)实验测定的[材料屈服](@entry_id:751736)强度，而 $\sigma_{\text{eq}}$ 是**von Mises [等效应力](@entry_id:749064)**，定义为：

$\sigma_{\text{eq}} = \sqrt{3J_2}$

通过这个定义，一个复杂三维应力状态的屈服条件被等效为一个简单的[单轴拉伸](@entry_id:188287)问题。通过将 $J_2$ 用主应力表示，我们得到[等效应力](@entry_id:749064)的另一种常用形式：

$\sigma_{\text{eq}} = \sqrt{\frac{1}{2}[(\sigma_1-\sigma_2)^2 + (\sigma_2-\sigma_3)^2 + (\sigma_3-\sigma_1)^2]}$

这个表达式明确显示[等效应力](@entry_id:749064)仅取决于主应力之差，因此天然地满足了压力无关性。其中的 $\sqrt{3}$ 因子是为了保证在[单轴拉伸](@entry_id:188287)状态（主应力为 $\sigma_Y, 0, 0$）下，$\sigma_{\text{eq}}$ 恰好等于 $\sigma_Y$。

#### 几何表示

在以三个主应力 $(\sigma_1, \sigma_2, \sigma_3)$ 为坐标轴的[主应力空间](@entry_id:184388)中，von Mises 屈服面方程 $\sigma_{\text{eq}} = \sigma_Y$ 描述了一个以静水压力轴（即 $\sigma_1=\sigma_2=\sigma_3$ 的直线）为中心轴的**无限长圆柱面**。其“无限长”体现了压力无关性，而“圆柱面”[截面](@entry_id:154995)为圆形，则是因为屈服条件仅依赖于 $J_2$，而与 $J_3$ 无关。$J_3$ 的值（或等价地，**Lode 参数**）决定了屈服面在偏平面（垂直于[静水压力](@entry_id:275365)轴的平面）内的形状是否为圆形。von Mises 准则的圆形[截面](@entry_id:154995)意味着，对于所有具有相同 $J_2$ 值的应力状态，其屈服行为是相同的，与主应力的具体[排列](@entry_id:136432)方式无关 [@problem_id:2896264] [@problem_id:2896282]。

#### 应用

von Mises 准则的一个重要预测是纯剪切状态下的屈服应力。对于纯剪切，主应力状态为 $(\tau, 0, -\tau)$。代入[等效应力](@entry_id:749064)公式，我们得到 $\sigma_{\text{eq}} = \sqrt{\frac{1}{2}[(\tau-0)^2 + (0-(-\tau))^2 + (-\tau-\tau)^2]} = \sqrt{3\tau^2} = \sqrt{3}\tau$。令其等于 $\sigma_Y$，可解得纯剪切[屈服应力](@entry_id:274513)为：

$\tau_Y = \frac{\sigma_Y}{\sqrt{3}} \approx 0.577 \sigma_Y$

[@problem_id:2896264]

### Tresca ([最大剪应力](@entry_id:181794)) 屈服准则

Tresca 屈服准则提出了一个更早也更直观的物理图像：材料的屈服由其内部经受的[最大剪应力](@entry_id:181794)所控制。

#### 定义与校准

该准则断言，当材料内某点的[最大剪应力](@entry_id:181794) $\tau_{\text{max}}$ 达到一个临界值 $k$ 时，[塑性流动](@entry_id:201346)开始。[最大剪应力](@entry_id:181794)等于最大主应力与最小主应力之差的一半：

$\tau_{\text{max}} = \frac{\sigma_{\text{max}} - \sigma_{\text{min}}}{2}$

若主应力按大小排序为 $\sigma_1 \ge \sigma_2 \ge \sigma_3$，则 $\tau_{\text{max}} = (\sigma_1 - \sigma_3)/2$。同样，该定义仅依赖于[主应力](@entry_id:176761)之差，因此也是压力无关的 [@problem_id:2896271]。

为了确定临界剪应力 $k$ 的值，我们使用[单轴拉伸](@entry_id:188287)实验进行校准。在[屈服点](@entry_id:188474)，主应力为 $(\sigma_Y, 0, 0)$。此时的[最大剪应力](@entry_id:181794)为 $\tau_{\text{max}} = (\sigma_Y - 0)/2 = \sigma_Y/2$。因此，临界剪应力 $k = \sigma_Y/2$ [@problem_id:2896225]。

Tresca 屈服准则可以表示为：

$\tau_{\text{max}} = \frac{\sigma_Y}{2} \quad \text{或等价地} \quad \sigma_1 - \sigma_3 = \sigma_Y$

在不排序的情况下，[屈服函数](@entry_id:167970)可以写为 $f(\boldsymbol{\sigma}) = \max\{|\sigma_1-\sigma_2|, |\sigma_2-\sigma_3|, |\sigma_3-\sigma_1|\} - \sigma_Y = 0$ [@problem_id:2896225]。

#### 几何表示

在[主应力空间](@entry_id:184388)中，Tresca [屈服面](@entry_id:175331)由六个[平面方程](@entry_id:152977) $\sigma_i - \sigma_j = \pm \sigma_Y$ ($i \neq j$) 所围成。这个几何体是一个以[静水压力](@entry_id:275365)轴为中心轴的**无限长正六角形棱柱**。其“无限长”同样源于压力无关性，而其在偏平面上的[截面](@entry_id:154995)是一个**正六边形** [@problem_id:2896225]。这个六边形形状表明，Tresca 准则的屈服行为依赖于 Lode 参数，即依赖于 $J_3$ [@problem_id:2896282]。

#### 应用

对于纯剪切状态 $(\tau, 0, -\tau)$，排序后的主应力为 $\sigma_1=\tau, \sigma_2=0, \sigma_3=-\tau$ (假设 $\tau>0$）。[最大剪应力](@entry_id:181794)为 $\tau_{\text{max}} = (\tau - (-\tau))/2 = \tau$。根据 Tresca 准则，屈服时有 $\tau = k = \sigma_Y/2$。因此，纯剪切[屈服应力](@entry_id:274513)为：

$\tau_Y = \frac{\sigma_Y}{2} = 0.5 \sigma_Y$

[@problem_id:2896225]

### 比较与高级主题

#### 几何与保守性比较

将 Tresca 和 von Mises 准则的屈服面在偏平面上进行比较，Tresca 的正六边形内切于 von Mises 的圆形。这意味着，除了在六边形的六个顶点处（对应纯剪切及类似状态），Tresca 准则预测的[屈服应力](@entry_id:274513)总是低于 von Mises 准则。因此，Tresca 准则通常被认为是更**保守**的设计准则。例如，对于一个给定的复杂应力状态，若要达到屈服，Tresca 准则所需的载荷比例因子 $\alpha_T$ 通常小于 von Mises 准则所需的 $\alpha_{vM}$ [@problem_id:2896242]。两者的预测差异最大约为 $15.5\%$。

#### 光滑性与[塑性流动法则](@entry_id:189597)

von Mises [屈服面](@entry_id:175331)是光滑、处处可微的。根据**[相关联流动法则](@entry_id:163391)**，塑性应变率的方向垂直于屈服面。对于 von Mises 面，这意味着在任何应力点，塑性流动的方向都是唯一确定的，方向为 $\dot{\boldsymbol{\varepsilon}}^p \propto \boldsymbol{s}$ [@problem_id:2896251]。

相比之下，Tresca 的六角形屈服面在棱和角点处是**不可微**的。在这些非光滑点，法向不唯一。根据推广的[流动法则](@entry_id:177163)（Koiter 法则），塑性应变率的方向必须位于一个由相邻光滑面法向张成的**法向锥**内。这意味着在角点处，[塑性流动](@entry_id:201346)的方向不是唯一的，而是取决于加载路径。这在理论和计算上都引入了额外的复杂性 [@problem_id:2896228]。

#### 硬化模型

实际材料在发生塑性变形后，其[屈服强度](@entry_id:162154)通常会发生变化，这一现象称为**硬化**。[屈服准则](@entry_id:193897)可以通过引入内部状态变量来描述硬化。
- **[各向同性硬化](@entry_id:164486) (Isotropic Hardening)**：假设屈服面在[应力空间](@entry_id:199156)中均匀膨胀，而不改变形状或中心位置。这通过让[屈服强度](@entry_id:162154) $\sigma_Y$ 成为等效塑性应变等标量硬化变量的函数来实现。几何上，von Mises 圆柱或 Tresca 六角棱柱的“半径”增大了 [@problem_id:2896251]。
- **[随动硬化](@entry_id:172077) (Kinematic Hardening)**：假设屈服面在[应力空间](@entry_id:199156)中平移，而不改变其大小或形状。这通过引入一个**背应力张量** $\boldsymbol{\alpha}$ 来实现，它代表了屈服面的中心位置。[屈服函数](@entry_id:167970)变为关于**相对[偏应力](@entry_id:163323)** $\boldsymbol{\eta} = \boldsymbol{s} - \boldsymbol{\alpha}$ 的函数。例如，[随动硬化](@entry_id:172077)的 von Mises 准则为 $\sqrt{3J_2(\boldsymbol{\eta})} - \sigma_Y = 0$。这种硬化模型能够描述[包辛格效应](@entry_id:173790)（Bauschinger effect），即材料在反向加载时[屈服强度](@entry_id:162154)降低的现象 [@problem_id:2896251]。

这些硬化模型是现代[计算塑性力学](@entry_id:171377)中数值积分算法（如**[径向返回算法](@entry_id:169742)**）的基础，它们为模拟材料在复杂加载历史下的行为提供了框架。