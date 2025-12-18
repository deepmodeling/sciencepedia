## 引言
[滑移线场理论](@entry_id:181917)是塑性力学中一个强大而经典的分析工具，专门用于解决材料在[平面应变](@entry_id:167046)条件下的塑性流动问题。当材料的应力超过其[弹性极限](@entry_id:186242)，进入塑性变形阶段时，传统的弹性力学方法便不再适用。[滑移线理论](@entry_id:184792)精准地填补了这一空白，它通过一套严谨的数学框架，为分析和预测[金属成形](@entry_id:188560)、岩[土力学](@entry_id:180264)和[接触力学](@entry_id:177379)中的复杂变形行为提供了深刻的物理洞察和定量的解析解或半解析解。其重要性在于，它能将复杂的[非线性偏微分方程](@entry_id:169481)组简化为沿着特定曲线（即滑移线）的常[微分](@entry_id:158718)关系，从而揭示应[力场](@entry_id:147325)和[速度场](@entry_id:271461)的内在结构。

本文旨在系统地阐述亨基-盖林格滑移线方程的理论与实践。我们将引导读者穿越这一经典理论的完整图景，从其基本原理到前沿应用。
- 在“原理与机制”一章中，我们将从刚-[理想塑性](@entry_id:753335)材料模型和[平面应变假设](@entry_id:186003)出发，严格推导[滑移线理论](@entry_id:184792)的核心——Hencky应力方程和Geiringer速度方程，并深入探讨其物理与几何意义。
- 接着，在“应用与跨学科联系”一章中，我们将展示该理论在解决实际工程问题中的威力，通过分析普朗特压痕、块体压缩等经典案例，演示如何施加边界条件并构建完整的滑移线场，同时将其与[极限分析](@entry_id:188743)等更广泛的力学原理相联系。
- 最后，在“动手实践”部分，我们提供了一系列精心设计的练习，旨在将理论知识转化为解决问题的实践能力。

通过本次学习，读者将能够深刻理解[滑移线理论](@entry_id:184792)的精髓，并掌握其在分析复杂塑性变形问题中的应用。

## 原理与机制

本章在前一章介绍的基础上，深入探讨[滑移线场理论](@entry_id:181917)的数学与物理原理。我们将从刚塑性材料模型的基本假设出发，系统地推导[平面应变塑性](@entry_id:201004)问题中应[力场](@entry_id:147325)和[速度场](@entry_id:271461)的核心控制方程——即[Hencky方程](@entry_id:200234)和[Geiringer方程](@entry_id:195065)。本章的目标是不仅呈现这些方程的形式，更要揭示其内在的物理意义、几何解释以及它们在解决实际问题中的应用。我们将通过分析一系列典型问题，逐步构建起对该理论的深刻理解。

### 刚塑性模型的基本假设

[滑移线场理论](@entry_id:181917)建立在一系列理想化假设之上，旨在简化复杂[弹塑性](@entry_id:193198)行为的分析，从而得到工程问题的解析解或半解析解。这些假设构成了我们后续所有推导的基石 。

首先，我们采用**刚-[理想塑性](@entry_id:753335)（rigid-perfectly plastic）**材料模型。该模型包含两个核心思想：
1.  **刚性（Rigid）**：材料在达到屈服极限之前，被认为是完全刚性的，即不发生任何变形。这意味着[弹性应变](@entry_id:189634)被忽略不计（$\boldsymbol{\varepsilon}^e = \mathbf{0}$）。因此，材料的弹性常数，如杨氏模量 $E$ 和泊松比 $\nu$，不会出现在问题的控制方程中。只有当应力状态达到某一[临界条件](@entry_id:201918)时，材料才开始流动。
2.  **[理想塑性](@entry_id:753335)（Perfectly Plastic）**：材料一旦开始[塑性流动](@entry_id:201346)，其[屈服应力](@entry_id:274513)保持不变，即不存在加工硬化现象。这简化了本构关系，使得屈服条件成为应力状态的一个固定边界。

其次，我们考虑**平面应变（plane strain）**变形。在这种条件下，垂直于变形平面（通常是 $xy$ 平面）方向的应变分量恒为零（$\varepsilon_z = 0$）。这一假设适用于许多工程场景，例如宽板的拉伸、[厚壁圆筒](@entry_id:189222)的膨胀以及某些[金属成形](@entry_id:188560)过程（如轧制和拉拔）。

最后，我们假设[塑性流动](@entry_id:201346)是**不可压缩的（incompressible）**。这意味着在塑性变形过程中，材料的[体积保持](@entry_id:141001)不变。用[应变率张量](@entry_id:266108) $\dot{\boldsymbol{\varepsilon}}^p$ 表示，该条件写作其迹为零，即 $\mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p) = 0$。对于只依赖于[偏应力张量](@entry_id:267642)的[屈服准则](@entry_id:193897)（如Tresca和[von Mises准则](@entry_id:164472)），若采用**关联流动法则（associated flow rule）**，[塑性不可压缩性](@entry_id:183440)是自然满足的  。

在这些假设下，塑性区域内的应[力场](@entry_id:147325)完全由以下三个条件决定：
1.  **[静力平衡](@entry_id:163498)方程（Static Equilibrium）**：在没有[体力](@entry_id:174230)的情况下，应力张量 $\boldsymbol{\sigma}$ 必须满足 $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$。
2.  **屈服条件（Yield Criterion）**：应力状态必须位于[屈服面](@entry_id:175331)上，例如对于[Tresca准则](@entry_id:167002)，在[平面应变](@entry_id:167046)条件下为 $|\sigma_1 - \sigma_2| = 2k$。
3.  **流动法则（Flow Rule）**：通常采用关联流动法则，它将应变率的方向与屈服面的法线方向联系起来。

### [平面应变塑性](@entry_id:201004)中的应力状态

为了描述[平面应变塑性](@entry_id:201004)问题中的应力状态，我们需要一个合适的[参数化](@entry_id:272587)方法。

#### 应力[参数化](@entry_id:272587)

在[平面应变](@entry_id:167046)条件下，[主应力](@entry_id:176761) $\sigma_1$ 和 $\sigma_2$ 位于变形平面内，而第三[主应力](@entry_id:176761) $\sigma_3$ 垂直于该平面。对于关联流动，可以证明 $\sigma_3$ 是中间[主应力](@entry_id:176761)，即 $\sigma_3 = \frac{1}{2}(\sigma_1 + \sigma_2)$。因此，[Tresca屈服准则](@entry_id:190718) $\max(|\sigma_1-\sigma_2|, |\sigma_2-\sigma_3|, |\sigma_3-\sigma_1|) = 2k$ 简化为：
$$
|\sigma_1 - \sigma_2| = 2k
$$
其中 $k$ 是材料的纯剪切[屈服强度](@entry_id:162154)。

此时，应力状态可以由两个[标量场](@entry_id:151443)完全描述：[静水压力](@entry_id:275365)（或[平均应力](@entry_id:751819)）和[主应力方向](@entry_id:753737)。我们定义**静水压力** $p$ 为（注意：此处定义压力在压缩时为正）：
$$
p = -\frac{\sigma_1 + \sigma_2}{2}
$$
结合屈服条件，我们可以将主应力表示为：
$$
\sigma_1 = -p + k \quad , \quad \sigma_2 = -p - k
$$
另一个关键变量是最大主应力 $\sigma_1$ 的方向，我们用它与 $x$ 轴的夹角 $\theta$ 来表示。通过[Mohr圆](@entry_id:168131)变换，可以得到笛卡尔坐标系下的应力分量  ：
$$
\sigma_{xx} = -p - k\cos(2\theta)
$$
$$
\sigma_{yy} = -p + k\cos(2\theta)
$$
$$
\sigma_{xy} = k\sin(2\theta)
$$
因此，整个应[力场](@entry_id:147325)被归结为求解两个标量场：$p(x, y)$ 和 $\theta(x, y)$。

#### Tresca 与 von Mises 准则的等价性

值得注意的是，尽管[滑移线理论](@entry_id:184792)最初主要基于[Tresca准则](@entry_id:167002)，但在[平面应变](@entry_id:167046)条件下，它同样适用于[von Mises准则](@entry_id:164472)。[von Mises准则](@entry_id:164472)通常写作 $J_2 = k_v^2$，其中 $J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s}$ 是[偏应力](@entry_id:163323)第二[不变量](@entry_id:148850)。在平面应变和关联流动下，$\sigma_3 = (\sigma_1+\sigma_2)/2$，代入 $J_2$ 的表达式可以推导出：
$$
|\sigma_1 - \sigma_2| = \frac{2}{\sqrt{3}}\sigma_y
$$
其中 $\sigma_y$ 是[单轴拉伸](@entry_id:188287)屈服应力。这表明，[von Mises准则](@entry_id:164472)在[平面应变](@entry_id:167046)下也简化为[最大剪应力](@entry_id:181794)恒定的形式。因此，Hencky-[Geiringer方程](@entry_id:195065)的形式对于两种准则是相同的，唯一的区别在于剪切[屈服强度](@entry_id:162154) $k$ 与单轴屈服应力 $\sigma_y$ 的关系 ：
*   **对于[Tresca准则](@entry_id:167002)**： $k = \frac{\sigma_y}{2}$
*   **对于[von Mises准则](@entry_id:164472)**： $k = \frac{\sigma_y}{\sqrt{3}}$

由于von Mises材料对应的 $k$ 值比Tresca材料大，其承载能力预测值约高出 $15.5\%$。然而，滑移线场的几何形状对于给定的边界值问题是相同的。

#### 压力的拉格朗日乘子角色

在不可压缩塑性流动中，[静水压力](@entry_id:275365) $p$ 扮演着一个特殊的角色。[塑性耗散](@entry_id:201273)[功率密度](@entry_id:194407)为 $\dot{W}^p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p$。将[应力张量](@entry_id:148973)分解为静水部分 $-p\mathbf{I}$ 和偏应力部分 $\boldsymbol{s}$，我们有：
$$
\dot{W}^p = (\boldsymbol{s} - p\mathbf{I}) : \dot{\boldsymbol{\varepsilon}}^p = \boldsymbol{s} : \dot{\boldsymbol{\varepsilon}}^p - p (\mathbf{I} : \dot{\boldsymbol{\varepsilon}}^p) = \boldsymbol{s} : \dot{\boldsymbol{\varepsilon}}^p - p \, \mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p)
$$
由于[塑性流动](@entry_id:201346)是不可压缩的，$\mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p)=0$，因此静水压力部分不做任何塑性功，即 $\dot{W}^p = \boldsymbol{s} : \dot{\boldsymbol{\varepsilon}}^p$。这意味着，流动法则（如关联流动）只规定了偏应力 $\boldsymbol{s}$ 和塑性应变率 $\dot{\boldsymbol{\varepsilon}}^p$ 之间的关系。静水压力 $p$ 不由本构关系确定，它更像一个**拉格朗日乘子**，其值由[静力平衡](@entry_id:163498)方程和应力边界条件在全局上确定，以满足不可压缩性的运动学约束 。

### 应力特征线：[Hencky方程](@entry_id:200234)

将应力分量关于 $p$ 和 $\theta$ 的表达式代入二维[静力平衡](@entry_id:163498)方程，我们得到一个关于 $p(x, y)$ 和 $\theta(x, y)$ 的一阶[拟线性偏微分方程](@entry_id:164345)组 ：
$$
\frac{\partial p}{\partial x} = 2k(-\sin(2\theta)\frac{\partial\theta}{\partial x} + \cos(2\theta)\frac{\partial\theta}{\partial y})
$$
$$
\frac{\partial p}{\partial y} = 2k(\cos(2\theta)\frac{\partial\theta}{\partial x} + \sin(2\theta)\frac{\partial\theta}{\partial y})
$$
这是一个**双曲型（hyperbolic）**[方程组](@entry_id:193238)。[双曲型方程](@entry_id:145657)的解具有沿特定曲线（称为**特征线**）传播信息的特性。在塑性力学中，这些应力特征线就是**滑移线（slip-lines）**。

滑移线定义为材料中[最大剪应力](@entry_id:181794)方向处处相切的曲线。对于各向同性材料，[最大剪应力](@entry_id:181794)方向与[主应力方向](@entry_id:753737)成 $\pm \pi/4$ 角 。因此，存在两个相互正交的滑移线族，分别称为 $\alpha$ 线和 $\beta$ 线。它们的[切线](@entry_id:268870)[方向角](@entry_id:167868) $\phi$ 与最大[主应力方向](@entry_id:753737)角 $\theta$ 的关系为：
$$
\phi = \theta \pm \frac{\pi}{4}
$$
通常约定，从 $\sigma_1$ 方向逆时针旋转 $\pi/4$ 得到 $\alpha$ 线方向，顺时针旋转 $\pi/4$ 得到 $\beta$ 线方向。即：
$$
\phi_\alpha = \theta + \frac{\pi}{4} \quad , \quad \phi_\beta = \theta - \frac{\pi}{4}
$$
通过特征线分析，可以证明上述[偏微分方程组](@entry_id:172573)沿着滑移线方向退化为更简单的常[微分](@entry_id:158718)关系式，这便是著名的**Hencky应力方程**：
$$
\begin{cases}
p + 2k\theta = \text{常数}  \quad \text{沿 } \alpha \text{ 线} \\
p - 2k\theta = \text{常数}  \quad \text{沿 } \beta \text{ 线}
\end{cases}
$$
积分后可得：
$$
\begin{cases}
p + 2k\theta = C_1  (\text{常数}) \quad \text{沿 } \alpha \text{ 线} \\
p - 2k\theta = C_2  (\text{常数}) \quad \text{沿 } \beta \text{ 线}
\end{cases}
$$
这两个关系式被称为**Hencky[不变量](@entry_id:148850)**。它们表明，沿着一条给定的 $\alpha$ 滑移线，[静水压力](@entry_id:275365) $p$ 的增加量与[主应力方向](@entry_id:753737)角 $\theta$ 的增加量成反比；而沿着一条 $\beta$ 滑移线，$p$ 的增加量与 $\theta$ 的增加量成正比。这为求解复杂应[力场](@entry_id:147325)提供了强大的工具。

### 几何解释与曲率关系

[Hencky方程](@entry_id:200234)不仅是数学关系，还具有深刻的几何与物理意义。我们可以将其与滑移线的几何形状联系起来。

#### 曲率与压力梯度

一条[平面曲线](@entry_id:271353)的**曲率** $\kappa$ 定义为其[切线](@entry_id:268870)[方向角](@entry_id:167868)随弧长 $s$ 的变化率，即 $\kappa = d\phi/ds$。曲率的倒数是[曲率半径](@entry_id:274690) $R=1/\kappa$。

对于 $\alpha$ 线，其[切线](@entry_id:268870)角为 $\phi_\alpha = \theta + \pi/4$。因此其曲率 $\kappa_\alpha$ 为：
$$
\kappa_\alpha = \frac{d\phi_\alpha}{ds_\alpha} = \frac{d}{ds_\alpha}(\theta + \pi/4) = \frac{d\theta}{ds_\alpha}
$$
同样，对于 $\beta$ 线，其[切线](@entry_id:268870)角为 $\phi_\beta = \theta - \pi/4$，曲率 $\kappa_\beta$ 为：
$$
\kappa_\beta = \frac{d\phi_\beta}{ds_\beta} = \frac{d}{ds_\beta}(\theta - \pi/4) = \frac{d\theta}{ds_\beta}
$$
将这两个几何关系代入微分形式的[Hencky方程](@entry_id:200234)（$dp+2kd\theta=0$ 沿 $\alpha$ 线, $dp-2kd\theta=0$ 沿 $\beta$ 线），我们得到压力梯度与滑移线曲率之间的直接联系   ：
$$
\frac{dp}{ds_\alpha} = -2k \frac{d\theta}{ds_\alpha} = -2k \kappa_\alpha = -\frac{2k}{R_\alpha}
$$
$$
\frac{dp}{ds_\beta} = 2k \frac{d\theta}{ds_\beta} = 2k \kappa_\beta = \frac{2k}{R_\beta}
$$
这里的 $R_\alpha$ 和 $R_\beta$ 是带符号的[曲率半径](@entry_id:274690)。通常约定，当沿弧长方向前进，曲线向其左法线方向弯曲时，曲率为正。根据这个约定：
*   **沿 $\alpha$ 线**：$\frac{dp}{ds_\alpha}$ 与 $\kappa_\alpha$ 符号相反。这意味着，如果[静水压力](@entry_id:275365) $p$ 沿 $\alpha$ 线增加（$\frac{dp}{ds_\alpha} > 0$），则该线必定具有负曲率（$\kappa_\alpha  0$），即向右弯曲。
*   **沿 $\beta$ 线**：$\frac{dp}{ds_\beta}$ 与 $\kappa_\beta$ 符号相同。这意味着，如果静水压力 $p$ 沿 $\beta$ 线增加（$\frac{dp}{ds_\beta} > 0$），则该线必定具有正曲率（$\kappa_\beta > 0$），即向左弯曲 。

这个关系为我们提供了强大的直观理解：**滑移线因静水压力的变化而弯曲**。如果沿某条滑移线的压力梯度为常数 $g$，则该线的曲率也为常数，这意味着这条滑移线是一段圆弧。其曲率半径可以直接计算得出。例如，若沿 $\beta$ 线有 $\frac{dp}{ds_\beta} = g_\beta$，则其曲率半径为 $R_\beta = \frac{2k}{g_\beta}$ 。

**例题分析** : 
在一个塑性区中的P点，测量得到沿滑移线方向的[压力梯度](@entry_id:274112)为 $\frac{\partial p}{\partial s_{\alpha}} = -60 \text{ MPa}\cdot \text{m}^{-1}$ 和 $\frac{\partial p}{\partial s_{\beta}} = 75 \text{ MPa}\cdot \text{m}^{-1}$。材料的剪切屈服强度为 $k = 150 \text{ MPa}$。求P点处两族滑移线的[曲率半径](@entry_id:274690)。
根据我们推导的关系：
$$
R_\alpha = -\frac{2k}{\partial p/\partial s_\alpha} = -\frac{2 \times 150 \text{ MPa}}{-60 \text{ MPa}\cdot \text{m}^{-1}} = 5 \text{ m}
$$
$$
R_\beta = \frac{2k}{\partial p/\partial s_\beta} = \frac{2 \times 150 \text{ MPa}}{75 \text{ MPa}\cdot \text{m}^{-1}} = 4 \text{ m}
$$
因此，在P点，$\alpha$ 线和 $\beta$ 线分别是半径为5米和4米的圆弧的一部分。

### 高等主题与数学结构

#### [特征坐标](@entry_id:166542)系与 Geiringer 方程

为了便于求解，特别是数值求解，通常引入**[特征坐标](@entry_id:166542)系** $(\alpha, \beta)$，使得坐标线与滑移线重合。按惯例，$\beta=\text{const}$ 的曲线是 $\alpha$ 线，$\alpha=\text{const}$ 的曲线是 $\beta$ 线。[Hencky方程](@entry_id:200234)在这些坐标下可以写成简单的偏[微分形式](@entry_id:146747)。例如，对于 $p+2k\theta=\text{const}$ 沿 $\alpha$ 线，这意味着 $p$ 和 $\theta$ 沿 $\alpha$ 线的变化（即对 $\alpha$ 求偏导，此处有误，应是对$\beta$）是相关的。经过推导，[Hencky方程](@entry_id:200234)变为：
$$
\frac{\partial p}{\partial \beta} + 2k\frac{\partial \theta}{\partial \beta} = 0 \quad , \quad \frac{\partial p}{\partial \alpha} - 2k\frac{\partial \theta}{\partial \alpha} = 0
$$
（注意：方程的具体符号取决于 $\alpha,\beta$ 线与 $\pm \pi/4$ 的对应关系以及 $p$ 的定义）。

除了应力方程，滑移线网格自身的几何形状也必须满足[相容性条件](@entry_id:637057)。如果引入 Lamé 系数 $H_\alpha, H_\beta$ 来描述[弧长](@entry_id:191173)元 $ds_\alpha = H_\alpha d\alpha, ds_\beta = H_\beta d\beta$，则[坐标系](@entry_id:156346)的相容性（即 $\frac{\partial^2 \mathbf{r}}{\partial\alpha\partial\beta} = \frac{\partial^2 \mathbf{r}}{\partial\beta\partial\alpha}$）会导出一组关于 $H_\alpha, H_\beta$ 和 $\theta$ 的几何关系，这便是**Geiringer速度（或几何）方程**。在某些特殊坐标选择下（如令 $H_\alpha = H_\beta = \lambda$），这些方程可以简化为类似柯西-黎曼方程的形式 ：
$$
\frac{\partial\theta}{\partial\alpha} = -\frac{\partial(\ln\lambda)}{\partial\beta} \quad , \quad \frac{\partial\theta}{\partial\beta} = \frac{\partial(\ln\lambda)}{\partial\alpha}
$$
这套完整的[方程组](@entry_id:193238)（Hencky应力方程和Geiringer[几何方程](@entry_id:173321)）构成了求解[平面应变塑性](@entry_id:201004)问题的理论基础。

如果[主应力方向](@entry_id:753737)场 $\theta(x,y)$ 已知，追踪滑移线就简化为一个求解[常微分方程(ODE)](@entry_id:162988)的初值问题 。例如，$\beta$ 线的方程为 $dy/dx = \tan(\theta(x,y) - \pi/4)$。给定一个起始点 $(x_0, y_0)$，就可以使用数值方法（如[自适应步长](@entry_id:636271)的[Runge-Kutta](@entry_id:140452)法）来积分这条曲线。在实际计算中，需要特别处理[切线](@entry_id:268870)接近垂直（$dy/dx \to \infty$）的情况，通常可以通过切换积分变量（即求解 $dx/dy$）或采用[弧长参数化](@entry_id:634139)来保证数值稳定性。

#### 关联与[非关联流动](@entry_id:199220)

我们之前的推导都基于**关联流动法则**，即塑性[应变率](@entry_id:154778)的方向垂直于[屈服面](@entry_id:175331)。在这种情况下，应力特征线（滑移线）与速度特征线（零伸长率线）是重合的。

然而，对于某些材料（如土壤、岩石、聚合物），实验观察表明其流动规律可能不遵循关联法则，这时需要引入一个不同于[屈服函数](@entry_id:167970) $f$ 的**塑性势函数** $g$ 来定义流动方向，即 $\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}}$，这称为**[非关联流动](@entry_id:199220)（non-associated flow）**。

在这种情况下：
*   **应力特征线**（滑移线）的性质不变，因为它们仅由[静力平衡](@entry_id:163498)方程和屈服条件 $f$ 决定。它们仍然是[最大剪应力](@entry_id:181794)方向。
*   **速度特征线**（零伸长率线）的方向则由塑性[势函数](@entry_id:176105) $g$ 决定，其方向为与 $\partial g/\partial\boldsymbol{\sigma}$ 的主方向成 $\pm \pi/4$ 角。

由于 $f \neq g$，$\boldsymbol{\sigma}$ 的主方向与 $\partial g/\partial\boldsymbol{\sigma}$ 的[主方向](@entry_id:276187)通常不一致。因此，在[非关联流动](@entry_id:199220)中，应力特征线和速度特征线**不再重合** 。这使得问题的求解变得异常复杂，经典的滑移[线图](@entry_id:264599)解法失效，需要更复杂的数学工具来处理两个不同方向的特征线族。

#### [粘塑性](@entry_id:165397)正则化

刚-[理想塑性](@entry_id:753335)模型在数学上会导致解的奇异性（如速度间断）。一种更符合物理实际并能改善数学性质的方法是引入**率相关性（rate-sensitivity）**，即**[粘塑性](@entry_id:165397)（viscoplasticity）**模型。在这种模型中，应力不仅取决于应变，还取决于应变率，例如 $\boldsymbol{s} = \mathbf{F}(\dot{\boldsymbol{\varepsilon}}^p, \varepsilon)$，其中 $\varepsilon$ 是一个小的率敏感性参数。

引入[粘塑性](@entry_id:165397)会对控制方程的数学类型产生根本性改变 。通过[应变率](@entry_id:154778)相容性方程消去[速度场](@entry_id:271461)后，原先的一阶双曲型应力[方程组](@entry_id:193238)会转变为一个包含二阶空间导数的高阶[方程组](@entry_id:193238)。这个新系统通常是**混合双曲-抛物型（hyperbolic-parabolic）**的。二阶项（通常与 $\varepsilon$ 成正比）起到了类似粘性耗散或[扩散](@entry_id:141445)的作用，平滑了刚塑性解中的[不连续性](@entry_id:144108)。

当率敏感性参数 $\varepsilon \to 0$ 时，这个过程构成了对原[双曲系统](@entry_id:260647)的**[奇异摄动](@entry_id:170303)（singular perturbation）**。理论和计算表明，[粘塑性](@entry_id:165397)解在绝大部分区域会收敛到刚塑性解。这意味着Hencky[不变量](@entry_id:148850)在极限情况下“几乎处处”成立。然而，在刚塑性解存在速度间断的区域，[粘塑性](@entry_id:165397)解会形成厚度随 $\varepsilon$ 趋于零的窄**内部层（internal layers）**，在这些层内应力梯度和[应变率](@entry_id:154778)梯度极大，但场量保持光滑。这种[正则化方法](@entry_id:150559)为理解和计算[塑性流动](@entry_id:201346)中的剪切带等局部化现象提供了重要途径。