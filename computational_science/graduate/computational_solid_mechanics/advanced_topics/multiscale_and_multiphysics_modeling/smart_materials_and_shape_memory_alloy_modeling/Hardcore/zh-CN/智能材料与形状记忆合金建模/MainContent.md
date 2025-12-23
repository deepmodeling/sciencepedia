## 引言
[智能材料](@entry_id:196298)，特别是形状记忆合金 (SMA)，因其独特的[形状记忆效应](@entry_id:160076)和超弹性，在航空航天、生物医疗和机器人等前沿领域扮演着日益重要的角色。它们能够响应温度或应力等外部刺激，产生巨大的可恢复变形或力，使其成为设计紧凑、高效作动器和智能结构的核心元件。然而，要充分释放其潜力，工程师和科学家必须超越现象学的观察，转而依赖能够精确预测其复杂、高度[非线性](@entry_id:637147)行为的[计算模型](@entry_id:152639)。这正是本篇文章的核心任务：系统性地建立从第一性原理到工程应用的[形状记忆合金](@entry_id:141110)建模知识体系。

本文旨在填补理论基础与实践应用之间的鸿沟。我们将带领读者踏上一段从抽象理论到具体实现的旅程。首先，在“原理与机制”一章中，我们将深入[连续介质力学](@entry_id:155125)和[热力学](@entry_id:141121)的核心，揭示控制 SMA 行为的[本构定律](@entry_id:178936)是如何从物理基本法则中推导出来的。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些模型如何在约束恢复、动态响应分析、[模型预测控制](@entry_id:146965)等多样化的实际问题中发挥威力，彰显其作为连接多学科的桥梁作用。最后，通过一系列“动手实践”的指导，我们将理论知识转化为可操作的计算技能，帮助读者亲手构建和验证自己的 SMA 仿真代码。这趟旅程将为您提供一套完整且强大的工具，用以分析、设计和优化基于[形状记忆合金](@entry_id:141110)的下一代智能系统。

## 原理与机制

本章旨在深入阐述形状记忆合金 (SMA) 本构模型构建的根本原理与核心机制。在前一章介绍其现象学背景之后，我们将系统性地建立一个严格的、基于连续介质力学和不[可逆过程](@entry_id:276625)[热力学](@entry_id:141121)的理论框架。我们将从最基本的热力学定律出发，推导控制材料行为的[本构关系](@entry_id:186508)，进而探讨如何将这些理论转化为可计算的数值算法，并最终讨论一些捕捉 SMA 复杂行为（如热-力耦合与功能疲劳）的高级建模策略。

### [形状记忆合金](@entry_id:141110)模型的[热力学](@entry_id:141121)基础

为了描述材料在经受变形和[相变](@entry_id:147324)时的行为，我们必须确保所建立的模型不违背物理学的基本定律，尤其是[热力学](@entry_id:141121)第一和第二定律。这些定律为所有本构关系提供了最基本的约束。

#### 热力学定律与克劳修斯-杜亥姆不等式

对于一个连续介质体，热力学第一定律（[能量守恒](@entry_id:140514)）和第二定律（[熵增原理](@entry_id:142282)）可以合并，从而得到一个适用于局部物[质点](@entry_id:186768)的强大工具——**克劳修斯-杜亥姆 (Clausius-Duhem, CD) 不等式**。在[等温过程](@entry_id:143096)中，该不等式可以表达为：

$$
\mathcal{D} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0
$$

这里，$\mathcal{D}$ 是单位体积的**[机械耗散](@entry_id:169843)率**，它必须恒为非负值，这体现了[能量耗散](@entry_id:147406)的不可逆性。$\boldsymbol{\sigma}$ 是**柯西应力张量 (Cauchy stress tensor)**，$\dot{\boldsymbol{\varepsilon}}$ 是**总应变率张量**，因此 $\boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}$ 代表单位体积的**[机械功率](@entry_id:163535)**。$\psi$ 是**亥姆霍兹自由能密度 (Helmholtz free energy density)**，$\dot{\psi}$ 则是其随时间的变化率。[亥姆霍兹自由能](@entry_id:136442)是一个[热力学势](@entry_id:140516)函数，它储存了材料在当前状态下的可恢[复能量](@entry_id:263929)。

#### [状态变量](@entry_id:138790)与内变量

为了完整描述 SMA 的状态，我们不仅需要可直接观测的**状态变量 (state variables)**，如总[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 和温度 $T$，还需要引入一组**内变量 (internal variables)**。内变量用于描述材料内部微观结构的非平衡状态，这些状态无法直接通过宏观测量得到，但却深刻影响着材料的宏观响应。对于 SMA 而言，最重要的内变量包括：

1.  **[马氏体](@entry_id:162117)体积分数 (martensite volume fraction)** $\xi$：一个标量，取值范围为 $[0, 1]$。$\xi=0$ 表示材料完全处于奥氏体相，$\xi=1$ 表示完全处于马氏体相。
2.  **[相变](@entry_id:147324)[应变张量](@entry_id:193332) (transformation strain tensor)** $\boldsymbol{\varepsilon}^{tr}$：一个对称二阶张量，代表了由于[相变](@entry_id:147324)引起的非[弹性应变](@entry_id:189634)。

因此，亥姆霍兹自由能通常是这些变量的函数：$\psi = \psi(\boldsymbol{\varepsilon}, \boldsymbol{\varepsilon}^{tr}, \xi, T)$。

#### [科尔曼-诺尔方法](@entry_id:183651)：推导[本构关系](@entry_id:186508)

科尔曼-诺尔 (Coleman-Noll) 方法是一个系统性的流程，它利用克劳修斯-杜亥姆不等式来推导材料的[本构关系](@entry_id:186508)。其核心思想是将[耗散不等式](@entry_id:188634)分解为确定性的、非耗散的[部分和](@entry_id:162077)必须满足非负条件的、耗散的部分。

我们首先对 $\dot{\psi}$ 应用[链式法则](@entry_id:190743)：

$$
\dot{\psi} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}:\dot{\boldsymbol{\varepsilon}} + \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^{tr}}:\dot{\boldsymbol{\varepsilon}}^{tr} + \frac{\partial \psi}{\partial \xi}\dot{\xi}
$$

将此表达式代入克劳修斯-杜亥姆不等式，得到：

$$
\mathcal{D} = \left(\boldsymbol{\sigma} - \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}\right):\dot{\boldsymbol{\varepsilon}} - \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^{tr}}:\dot{\boldsymbol{\varepsilon}}^{tr} - \frac{\partial \psi}{\partial \xi}\dot{\xi} \ge 0
$$

根据科尔曼-诺尔的论证，由于总[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}$ 可以在实验中任意指定，为了保证不等式对所有可能的过程都成立，其系数项必须为零。这就给出了材料的**超弹性应力响应 (hyperelastic stress response)**：

$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}
$$

这条关系表明，应力完全由自由能对当前总应变的导数确定，这部分响应是可逆的、非耗散的。

由此，[耗散不等式](@entry_id:188634)简化为**残余[耗散不等式](@entry_id:188634) (residual dissipation inequality)**：

$$
\mathcal{D} = Y^{tr}:\dot{\boldsymbol{\varepsilon}}^{tr} + Y_{\xi}\dot{\xi} \ge 0
$$

其中，我们定义了驱动内变量演化的**[热力学力](@entry_id:161907) (thermodynamic forces)** 或**共轭力 (conjugate forces)**：

$$
Y^{tr} := -\frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^{tr}}, \quad Y_{\xi} := -\frac{\partial \psi}{\partial \xi}
$$

残余[耗散不等式](@entry_id:188634)是所有 SMA 本构模型的核心，它表明[机械耗散](@entry_id:169843)的来源是[热力学力](@entry_id:161907)与其共轭的内变量[演化速率](@entry_id:202008)的乘积。任何描述内变量如何演化（即[相变](@entry_id:147324)如何进行）的**动力学定律 (kinetic law)** 都必须确保这个不等式恒成立。

作为一个具体的例子 ，考虑一个等温小应变 SMA 模型，其亥姆霍兹自由能密度函数形式如下：
$$
\psi(\boldsymbol{\varepsilon},\boldsymbol{\varepsilon}^{tr},\xi) = \tfrac{1}{2}\big(\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{tr}\big):\mathbf{C}:\big(\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{tr}\big) + \tfrac{1}{2}k\,\|\boldsymbol{\varepsilon}^{tr}\|^2 + H\,\xi + \tfrac{1}{2}h\,\xi^2
$$
其中 $\mathbf{C}$ 是[四阶弹性张量](@entry_id:188318)，$k>0$ 和 $h>0$ 是[硬化](@entry_id:177483)模量，$H$ 是一个常数。

应用[科尔曼-诺尔方法](@entry_id:183651)，我们首先得到应力：
$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} = \mathbf{C}:(\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{tr})
$$
这正是在弹性基体中减去[相变](@entry_id:147324)应变后得到的胡克定律。接着，我们计算共轭于内变量的[热力学力](@entry_id:161907)：
$$
Y^{tr} = -\frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^{tr}} = -(-\mathbf{C}:(\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{tr}) + k\,\boldsymbol{\varepsilon}^{tr}) = \boldsymbol{\sigma} - k\,\boldsymbol{\varepsilon}^{tr}
$$
$$
Y_{\xi} = -\frac{\partial \psi}{\partial \xi} = -(H + h\,\xi)
$$
这些推导出的关系是[热力学一致的](@entry_id:755906)，它们构成了后续建立[相变动力学](@entry_id:197611)模型的基础。

### 自由能势函数的构建

[自由能函数](@entry_id:749582) $\psi$ 是整个模型的“基因”，它编码了材料的能量储存特性。一个合理的 $\psi$ 函数通常由几个物理意义明确的部分叠加而成。

#### 自由能的组成部分

1.  **弹性应变能**：这部分能量储存在因应力而发生弹性变形的[晶格](@entry_id:196752)中。最常见的形式是二次型，例如 $\frac{1}{2}(\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{tr}):\mathbf{C}:(\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{tr})$。这里的物理意义是，总应变 $\boldsymbol{\varepsilon}$ 中扣除掉[相变](@entry_id:147324)引起的非弹性应变 $\boldsymbol{\varepsilon}^{tr}$ 后，剩余的弹性应变 $\boldsymbol{\varepsilon}^e = \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{tr}$ 才贡献于弹性储能。

2.  **化学自由能**：这是[奥氏体](@entry_id:161328)相与马氏体相固有的、与温度密切相关的能量。我们通常表示为 $g_A(T)$ 和 $g_M(T)$。它们的差值 $\Delta g(T) = g_M(T) - g_A(T)$ 是驱动[相变](@entry_id:147324)的一个关键因素 。例如，在考虑马氏体体积分数 $\xi$ 的模型中，这部分能量可以写为 $\xi g_M(T) + (1-\xi) g_A(T) = g_A(T) + \xi \Delta g(T)$。

3.  **硬化[势能](@entry_id:748988)**：这些是与内变量本身相关的能量项，它们通常会惩罚内变量的增长，从而导致材料在[相变过程](@entry_id:147919)中表现出**硬化 (hardening)** 行为。例如，形如 $\frac{1}{2}h\,\xi^2$ 的项意味着随着马氏体体积分数 $\xi$ 的增加，系统的能量也在增加，这使得进一步的[相变](@entry_id:147324)更难发生，宏观上表现为[相变](@entry_id:147324)所需驱动力的提高。类似地，$\frac{1}{2}k\,\|\boldsymbol{\varepsilon}^{tr}\|^2$ 也会导致与[相变](@entry_id:147324)应变相关的[硬化](@entry_id:177483) 。

#### 从自由能到潜热：深入探索

自由能模型不仅能描述力学行为，还能与材料的热学性质建立深刻联系，特别是**[相变](@entry_id:147324)潜热 (latent heat of transformation)**。

根据[热力学基本关系](@entry_id:144320)，比熵 (specific entropy) $s$ 和比内能 (specific internal energy) $u$ 可以从比[亥姆霍兹自由能](@entry_id:136442) $\psi$ 导出：
$$
s = -\frac{\partial \psi}{\partial T}, \quad u = \psi + Ts
$$
在一个可逆的一阶[相变过程](@entry_id:147919)中，例如在无应力下于[相变](@entry_id:147324)温度 $T_t$ 发生的[相变](@entry_id:147324)，两相的吉布斯自由能相等。在零应力下，[吉布斯自由能](@entry_id:146774)等于[亥姆霍兹自由能](@entry_id:136442)，因此平衡条件为 $\psi_A(T_t) = \psi_M(T_t)$，即 $\Delta\psi(T_t) = \psi_M(T_t) - \psi_A(T_t) = 0$。

[相变](@entry_id:147324)[潜热](@entry_id:146032) $L$ 定义为[相变过程](@entry_id:147919)中的[焓变](@entry_id:147639) $\Delta h$。在零压（零应力）下，焓等于内能，因此 $L = \Delta u(T_t)$。结合平衡条件，我们有：
$$
\Delta\psi(T_t) = \Delta u(T_t) - T_t \Delta s(T_t) = 0
$$
这立即导出一个至关重要的关系：
$$
L = \Delta u(T_t) = T_t \Delta s(T_t)
$$
这个公式表明，[相变](@entry_id:147324)[潜热](@entry_id:146032)等于[相变](@entry_id:147324)温度乘以[相变过程中的熵变](@entry_id:138245)。熵是系统无序度的量度，[奥氏体](@entry_id:161328)作为高温相，其原子[排列](@entry_id:136432)通常比[马氏体](@entry_id:162117)更无序，因此熵值更高 ($S_A > S_M$)。这意味着从[奥氏体](@entry_id:161328)到[马氏体](@entry_id:162117)的正向[相变](@entry_id:147324)，熵变 $\Delta s = s_M - s_A  0$，因此潜热 $L  0$，即这是一个[放热过程](@entry_id:147168)。反之，逆[相变](@entry_id:147324)是吸热的。

这个原理使得我们可以通过构建一个精确的[自由能函数](@entry_id:749582)，不仅预测力学行为，还能预测像[差示扫描[量热法](@en](@entry_id:150812)try_id:145378) (DSC) 实验中测得的潜热值，从而为模型的校准和验证提供了一条独立的途径 。

### [相变动力学](@entry_id:197611)建模

确定了[热力学力](@entry_id:161907)和耗散原理后，下一步是规定内变量如何随这些力而演化。这部分内容称为**动力学定律**或**[流动法则](@entry_id:177163) (flow rule)**，它决定了相变过程的速率和路径。

#### 耗散原理与驱动力

残余[耗散不等式](@entry_id:188634) $\mathcal{D} = Y:\dot{\alpha} \ge 0$ 指明了演化的方向。例如，对于正向[相变](@entry_id:147324)（$\dot{\xi}0$），必须要求其共轭的[热力学](@entry_id:141121)驱动力 $Y_\xi$ 为正。模型必须确保这一点。

#### 率无关模型：[相变](@entry_id:147324)屈服面与硬化

对于许多加载速率较慢的应用，可以忽略[相变](@entry_id:147324)的时间效应，采用**率无关 (rate-independent)** 模型。这类模型的核心思想类似于[金属塑性](@entry_id:176585)理论，即引入一个**[相变](@entry_id:147324)[屈服面](@entry_id:175331) (transformation surface)**（或称加载函数），其方程通常写作：
$$
\Phi(\boldsymbol{\sigma}, \text{内变量}) \le 0
$$
-   当 $\Phi  0$ 时，材料处于“弹性”域，内变量不发生变化。
-   当 $\Phi = 0$ 时，材料状态位于[屈服面](@entry_id:175331)上，可能发生[相变](@entry_id:147324)。
-   $\Phi  0$ 的状态是不允许存在的。

[相变](@entry_id:147324)的发生与否由一套**库恩-塔克 (Kuhn-Tucker, KT) 条件**严格定义。例如，对于正向[相变](@entry_id:147324)（$\dot{\xi}\ge 0$）：
$$
\Phi \le 0, \quad \dot{\xi} \ge 0, \quad \Phi \dot{\xi} = 0
$$
这些条件意味着，要么材料处于弹性状态（$\Phi  0, \dot{\xi} = 0$），要么正在发生[相变](@entry_id:147324)（$\Phi = 0, \dot{\xi}  0$）。

多轴应力状态下的[相变](@entry_id:147324)[屈服面](@entry_id:175331)可以基于物理直觉构建。例如，可以认为[相变](@entry_id:147324)既受[静水压力](@entry_id:275365)（体积改变）驱动，也受[剪切应力](@entry_id:137139)（形状改变）驱动。这可以表示为一个[应力不变量](@entry_id:170526)的[线性组合](@entry_id:154743) ：
$$
\Phi = a I_1 + b \sqrt{J_2} - R \le 0
$$
其中 $I_1 = \mathrm{tr}(\boldsymbol{\sigma})$ 是应力第一[不变量](@entry_id:148850)（与静水压力成正比），$J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s}$ 是[偏应力张量](@entry_id:267642) $\boldsymbol{s}$ 的第二[不变量](@entry_id:148850)（与[剪切应力](@entry_id:137139)大小相关），$a$ 和 $b$ 是材料参数，而 $R$ 是[相变](@entry_id:147324)阻力。

随着[相变](@entry_id:147324)的进行，材料的响应通常会发生变化，即**硬化**。
-   **[各向同性硬化](@entry_id:164486) (Isotropic hardening)**：[相变](@entry_id:147324)屈服面均匀扩大，意味着在所有方向上启动[相变](@entry_id:147324)都需要更大的应力。这通常通过使[相变](@entry_id:147324)阻力 $R$ 成为 $\xi$ 的函数来实现，例如 $R(\xi) = R_0 + k\xi$ 。
-   **[随动硬化](@entry_id:172077) (Kinematic hardening)**：[相变](@entry_id:147324)屈服面在应力空间中平移。这通过引入一个**背应力 (backstress)** 张量 $\boldsymbol{\alpha}$ 来实现，[屈服面](@entry_id:175331)方程变为 $\Phi = \|\boldsymbol{s} - \boldsymbol{\alpha}\| - R \le 0$。背应力的演化代表了[相变过程](@entry_id:147919)中形成的内部应力。 

最后，**关联流动法则 (associative flow rule)** 是一个广泛采用的假设，它规定[相变](@entry_id:147324)应变率 $\dot{\boldsymbol{\varepsilon}}^{tr}$ 的方向垂直于[相变](@entry_id:147324)[屈服面](@entry_id:175331)：
$$
\dot{\boldsymbol{\varepsilon}}^{tr} = \dot{\gamma} \frac{\partial \Phi}{\partial \boldsymbol{\sigma}}
$$
其中 $\dot{\gamma}$ 是一个非负的标量乘子，称为[相变](@entry_id:147324)率。这个假设可以从最大耗散原理导出，确保了模型的热力学稳定性。

#### 率相关（粘性）模型

真实材料的[相变](@entry_id:147324)总需要时间。**率相关 (rate-dependent)** 或**粘性 (viscous)** 模型旨在捕捉这种时间依赖性。其核心是引入一个**耗散势 (dissipation potential)** $R(\dot{\alpha})$，它是一个关于内变量速率的凸函数。[热力学力](@entry_id:161907)与速率通过该[势函数](@entry_id:176105)相关联：
$$
Y = \frac{\partial R}{\partial \dot{\alpha}}
$$
例如，一个常见的粘性模型  采用如下的耗散势：
$$
R_\eta(\dot{\xi}) = Y_0 |\dot{\xi}| + \frac{1}{2}\eta \dot{\xi}^2
$$
其中 $Y_0$ 是率无关的[相变](@entry_id:147324)阻力，$\eta$ 是粘性系数。这种模型被称为**[粘塑性](@entry_id:165397) (viscoplastic)** 模型。它导出的动力学关系为 $Y_\xi = Y_0 \mathrm{sgn}(\dot{\xi}) + \eta \dot{\xi}$。这意味着驱动力 $Y_\xi$ 可以超过静态阈值 $Y_0$，这个“超额驱动力”$(|Y_\xi| - Y_0)$ 与[相变](@entry_id:147324)速率 $\dot{\xi}$ 成正比。与率无关模型的“开关”式行为不同，率相关模型描述了一个平滑且依赖于加载速率的[相变过程](@entry_id:147919)。

### 计算实现与高级主题

将连续介质理论转化为可以在计算机上求解的离散算法，是工程应用的关键一步。

#### [预测-校正算法](@entry_id:753695)（[返回映射](@entry_id:754324)）

对于率无关和率相关的非弹性模型，**预测-校正 (predictor-corrector)** 算法（也称**[返回映射](@entry_id:754324) (return-mapping)** 算法）是标准的数值求解方案。在一个离散的时间（或载荷）增量步内，该算法分为两步：

1.  **弹性预测步**：假设该增量步完全是弹性的。基于这个假设，计算出一个“试探”应力状态 $(\boldsymbol{\sigma}^{tr})$。
2.  **[相变](@entry_id:147324)校正步**：检查试探应力状态是否违反了[相变](@entry_id:147324)准则（即 $\Phi(\boldsymbol{\sigma}^{tr})  0$）。如果违反，则说明发生了[相变](@entry_id:147324)。此时，需要通过求解内变量的演化方程，将应力状态“返回”到更新后的、允许存在的[相变](@entry_id:147324)[屈服面](@entry_id:175331)上。这一步的最终状态必须满足**一致性条件 (consistency condition)**，即 $\Phi_{n+1}=0$（对于率无关模型）。

在存在[随动硬化](@entry_id:172077)时，返回路径的具体形式取决于算法选择 。**[径向返回](@entry_id:754007) (radial return)** 是一种简化，它假设返回方向直接指向初始[屈服面](@entry_id:175331)的中心，[计算效率](@entry_id:270255)高但存在一定误差。**非[径向返回](@entry_id:754007) (non-radial return)** 则更精确地考虑了校正过程中[背应力](@entry_id:198105)的演化。此外，算法必须能处理内变量达到其物理边界（如 $\xi=1$）的**饱和 (saturation)** 情况。

#### 热-力耦合：[潜热](@entry_id:146032)与[温度过冲](@entry_id:195464)

在许多实际应用中，尤其是在快速驱动下，SMA 的温度会发生显著变化，不能再作等温假设。这时必须考虑热-力耦合效应。核心是求解一个包含多个热[源项](@entry_id:269111)的**[能量平衡方程](@entry_id:191484)** ：
$$
\rho c \dot{T} = \underbrace{k \nabla^2 T}_{\text{热传导}} + \underbrace{\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}}_{\text{热弹性效应}} \underbrace{- L \dot{\xi}}_{\text{相变潜热}} - \underbrace{\frac{h P}{A} (T - T_\infty)}_{\text{对流换热}}
$$
其中，$\rho$ 是密度，$c$ 是比热容，$k$ 是[热导率](@entry_id:147276)，$L$ 是潜热，$h$ 是[对流换热系数](@entry_id:151029)。

这个耦合系统揭示了一个重要的现象：**[温度过冲](@entry_id:195464) (thermal overshoot)**。当 SMA 经历快速的、放热的正向[相变](@entry_id:147324)时（$\dot{\xi}0, L0$），[潜热](@entry_id:146032)的释放速率可能超过材料通过传导和[对流](@entry_id:141806)散发热量的速率。这会导致材料温度急剧升高。而根据克劳修斯-克拉佩龙关系，温度升高会提高[相变](@entry_id:147324)所需的临界应力，从而反过来抑制[相变](@entry_id:147324)的进一步进行。这种自调节机制在 SMA 的动态响应中至关重要。

#### 功能疲劳建模

SMA在长期[循环加载](@entry_id:181502)下，其[相变](@entry_id:147324)特性（如[相变](@entry_id:147324)温度）会发生漂移，这种现象称为**功能疲劳 (functional fatigue)**。从建模角度看，这意味着材料的某些“常数”实际上是随历史演化的慢变量。

一个有效的**唯象建模 (phenomenological modeling)** 方法是将这些材料参数本身也视为内变量 。例如，我们可以让[马氏体相变](@entry_id:158998)开始温度 $M_s$ 和奥氏体[相变](@entry_id:147324)开始温度 $A_s$ 随累积[相变](@entry_id:147324)量而演化：
$$
\dot{M}_s = -\gamma |\dot{\xi}|, \quad \dot{A}_s = \tilde{\gamma} |\dot{\xi}|
$$
其中，$\gamma$ 和 $\tilde{\gamma}$ 是疲劳参数，而 $|\dot{\xi}|$ 度量了[相变](@entry_id:147324)的“活动强度”。积分 $\int |\dot{\xi}| dt$ 代表了总的累积[相变](@entry_id:147324)程度。这种方法虽然没有深入到微观的损伤机制，但能有效地在宏观层面捕捉到[相变](@entry_id:147324)[滞回环](@entry_id:160173)随循环次数增多而展宽或漂移的现象，对于评估 SMA 器件的长期服役性能至关重要。