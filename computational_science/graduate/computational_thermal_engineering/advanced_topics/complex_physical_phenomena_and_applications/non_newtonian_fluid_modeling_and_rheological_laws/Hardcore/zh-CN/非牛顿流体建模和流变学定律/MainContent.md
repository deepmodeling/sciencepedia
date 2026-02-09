## 引言
在自然界与工业生产中，从聚合物熔体、食品浆料到血液和泥浆，我们随处可见不遵循经典黏性定律的流体。这些“非牛顿流体”的黏度会随剪切速率、变形历史甚至温度而改变，其复杂的流变行为使得传统的牛顿流体模型在预测和设计中捉襟见肘。为了准确描述并有效利用这些材料，建立能够捕捉其核心特性的数学模型至关重要。本文旨在为读者提供一个关于非牛顿流体建模与流变定律的系统性指南。

我们将通过三个循序渐进的章节展开探讨。首先，在“原理与机制”一章中，我们将奠定理论基石，深入解析流体变形的运动学、所有本构关系必须遵循的客观性原理，以及区分不同流体类型的关键物理机制。接着，在“应用与跨学科联系”一章，我们将跨越学科边界，展示这些理论模型如何在热工、材料加工、生物力学和地球物理等领域中发挥关键作用。最后，通过一系列精心设计的“动手实践”案例，读者将有机会将理论知识应用于解决具体的分析与计算问题。

要驾驭非牛顿流动的复杂性，我们必须从最基本的物理原理出发。现在，让我们从第一章开始，一同探索构建这些强大模型的底层逻辑与机制。

## 原理与机制

在深入探讨非牛顿流体具体的计算模型之前，我们必须首先建立一个坚实的理论基础。本章旨在阐述描述流体运动的基本运动学原理、所有本构模型必须遵守的物理约束，以及表征各类非牛顿行为的核心机制。我们将从流体变形的数学描述入手，逐步构建出广义牛顿流体、黏塑性流体、黏弹性流体和触变性流体等复杂流体模型的理论框架。

### 基本运动学与客观性原理

任何流体本构关系的建立都始于对速度场的分析。流体微团在运动过程中的速度变化，可以分解为纯粹的变形（形状和尺寸的改变）和刚性旋转。这种分解对于理解应力如何产生以及能量如何耗散至关重要。

#### 速度梯度张量的分解

一个连续介质中的速度场 $\mathbf{v}(\mathbf{x}, t)$ 包含了流体运动的全部信息。其空间梯度，即**速度梯度张量** $\mathbf{L} = \nabla \mathbf{v}$，描述了速度随位置的变化。这个二阶张量可以唯一地分解为其对称部分和反对称部分：

$\mathbf{L} = \mathbf{D} + \mathbf{W}$

其中，对称部分 $\mathbf{D}$ 被称为**变形率张量**（rate-of-deformation tensor）或拉伸张量（stretching tensor），定义为：

$\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\top}) = \frac{1}{2}(\nabla\mathbf{v} + (\nabla\mathbf{v})^{\top})$

$\mathbf{D}$ 的对角分量描述了材料沿坐标轴方向的拉伸或压缩速率，而非对角分量则描述了材料线之间夹角的变化速率（剪切速率）。因此，$\mathbf{D}$ 精确地量化了流体微团的变形速率。

反对称部分 $\mathbf{W}$ 被称为**涡量张量**（vorticity tensor）或自旋张量（spin tensor），定义为：

$\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\top}) = \frac{1}{2}(\nabla\mathbf{v} - (\nabla\mathbf{v})^{\top})$

$\mathbf{W}$ 代表了流体微团作为一个刚体的瞬时旋转速率，这个过程不伴随任何形状或体积的改变。涡量矢量 $\boldsymbol{\omega}_{\text{vort}} = \nabla \times \mathbf{v}$ 是 $2\mathbf{W}$ 的轴向矢量。这种运动学分解是构建所有流体本构模型的基础 [@problem_id:3975904]。

对于一个具有对称柯西应力张量 $\boldsymbol{\sigma}$ 的流体（这是在没有体力矩情况下的角动量守恒的必然结果），单位体积的黏性耗散率 $\phi$——即由黏性力所做的功——完全由变形率张量决定。黏性耗散是能量方程中的一个关键源项，它将机械能不可逆地转化为内能。将应力张量分解为压力部分和偏应力张量 $\boldsymbol{\tau}$（$\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\tau}$），耗散率可以写作：

$\phi = \boldsymbol{\tau} : \mathbf{D}$

由于对称张量（$\boldsymbol{\tau}$）和反对称张量（$\mathbf{W}$）的双点积恒为零，即 $\boldsymbol{\tau} : \mathbf{W} = 0$，因此涡量张量（即纯旋转）对黏性耗散没有贡献 [@problem_id:3975904]。

#### 材料坐标系无关性原理

**材料坐标系无关性原理**（principle of material frame indifference），或称**客观性原理**（objectivity），是一个基本物理要求：本构定律（即材料的响应）不应依赖于观察者。换言之，本构方程的形式在所有（刚性运动的）参考系下都应保持不变。

考虑一个相对于实验室参考系进行刚性运动（平移 $\mathbf{c}(t)$ 加旋转 $\mathbf{Q}(t)$）的新参考系。一个在实验室参考系中表示为 $\mathbf{T}$ 的二阶张量，如果其在新参考系中的表示 $\mathbf{T}^{\star}$ 满足以下变换关系，则称该张量是**客观的**：

$\mathbf{T}^{\star}(t) = \boldsymbol{Q}(t) \mathbf{T}(t) \boldsymbol{Q}(t)^{\mathsf{T}}$

这是一个核心定义 [@problem_id:3975907]。根据这个定义，可以证明变形率张量 $\mathbf{D}$ 是一个客观张量，而涡量张量 $\mathbf{W}$ 则不是。$\mathbf{W}$ 的变换包含了观察者自身的旋转速率，因此它是一个依赖于参考系的量 [@problem_id:3975904]。

这一原理对建立时间依赖的本构模型（如黏弹性模型）提出了严峻的挑战。常规的时间导数，例如物质导数 $\dot{\boldsymbol{T}}$，通常不是客观的。我们可以通过一个简单的思想实验来证明这一点：考虑一个材料内部状态不变的物体（例如，其体坐标系下的应力张量 $\boldsymbol{T}^b$ 恒定），仅仅在空间中做纯刚性旋转。从实验室参考系观察，空间应力张量 $\boldsymbol{T}(t) = \boldsymbol{Q}(t) \boldsymbol{T}^b \boldsymbol{Q}(t)^{\mathsf{T}}$ 是随时间变化的。其时间导数 $\dot{\boldsymbol{T}}(t) = \boldsymbol{W}(t)\boldsymbol{T}(t) - \boldsymbol{T}(t)\boldsymbol{W}(t)$ 通常不为零。然而，一个客观的时间导数应该反映材料的内在变化，对于这个例子，它必须为零。由于 $\dot{\boldsymbol{T}}(t)$ 不为零，它显然不是客观的，因为它错误地将刚性旋转解释为材料状态的变化 [@problem_id:3975907]。

为了解决这个问题，需要构建**客观应力率**（objective stress rates）。这些导数通过引入包含涡量张量 $\mathbf{W}$ 的修正项，来抵消由于坐标系旋转引起的非客观性贡献。例如，**余旋（Jaumann）应力率**定义为：

$\overset{\circ}{\boldsymbol{\tau}} = \dot{\boldsymbol{\tau}} - \mathbf{W}\boldsymbol{\tau} + \boldsymbol{\tau}\mathbf{W}$

对于上述纯旋转的例子，可以证明 $\overset{\circ}{\boldsymbol{\tau}}$ 恒等于零，这与物理直觉相符。其他客观率，如上随体导数（upper-convected derivative），也扮演着类似的角色。因此，$\mathbf{W}$ 虽然不直接贡献于耗散，但在确保黏弹性模型的数学和物理一致性方面至关重要 [@problem_id:3975907] [@problem_id:3975904]。

### 广义牛顿流体

最简单的一类非牛顿流体是**广义牛顿流体**（Generalized Newtonian Fluids, GNF）。这类流体的特点是，其偏应力张量 $\boldsymbol{\tau}$ 与当前的变形率张量 $\mathbf{D}$ 之间存在一个瞬时的代数关系，不涉及时间导数或积分，因此它们没有“记忆效应”。其通用本构方程形式为：

$\boldsymbol{\tau} = 2\eta(\dot{\gamma}) \mathbf{D}$

这里的 $\eta$ 是**表观黏度**（apparent viscosity），它不是一个常数，而是变形率大小的函数。为了满足客观性原理，$\eta$ 必须是 $\mathbf{D}$ 的客观标量不变量的函数。最常用的不变量是**等效剪切率**（equivalent shear rate）$\dot{\gamma}$，定义为：

$\dot{\gamma} = \sqrt{2\mathbf{D}:\mathbf{D}}$

这个定义保证了在简单剪切流中，$\dot{\gamma}$ 恰好等于速度梯度的大小 [@problem_id:3975939] [@problem_id:3975934]。

#### 剪切相关黏度模型

许多流体在剪切作用下黏度会发生变化。**剪切致稀**（shear-thinning）指黏度随剪切率增大而降低，而**剪切增稠**（shear-thickening）则相反。多种数学模型被提出来描述这种行为。

- **幂律模型 (Power-Law Model)**：这是最简单的模型之一，其表观黏度为：
  $\eta(\dot{\gamma}) = K\dot{\gamma}^{n-1}$
  其中 $K$ 是**稠度指数**（consistency index），$n$ 是**流动行为指数**（flow behavior index）。当 $n1$ 时为剪切致稀， $n1$ 时为剪切增稠， $n=1$ 时退化为牛顿流体。在对数-对数坐标系中（$\log \eta$ vs $\log \dot{\gamma}$），幂律模型表现为一条斜率为 $n-1$ 的直线。其主要缺点是，对于剪切致稀流体，它预测在 $\dot{\gamma} \to 0$ 时黏度趋于无穷；对于剪切增稠流体，在 $\dot{\gamma} \to 0$ 时黏度趋于零。这通常与实验观察到的在低剪切率下的牛顿平台区（**零剪切黏度** $\eta_0$）不符 [@problem_id:3975919]。

- **具有黏度平台的模型**：为了更真实地描述流体行为，尤其是在极低和极高剪切率下的牛顿平台区，发展出了更复杂的模型。
  - **Carreau-Yasuda 模型** 和 **Cross 模型** 是其中的杰出代表。它们都能描述从零剪切黏度 $\eta_0$ 过渡到**无限剪切黏度** $\eta_\infty$ 的完整流动曲线。
    - **Carreau-Yasuda 模型** 的形式为：
      $\eta(\dot{\gamma}) = \eta_{\infty} + (\eta_0 - \eta_{\infty}) \left[ 1 + (\lambda \dot{\gamma})^a \right]^{\frac{n-1}{a}}$
    - **Cross 模型** 的形式为：
      $\eta(\dot{\gamma}) = \eta_{\infty} + \frac{\eta_0 - \eta_{\infty}}{1 + (\lambda \dot{\gamma})^m}$
  这两个模型都引入了特征时间 $\lambda$ 来定义牛顿平台和幂律区域之间的过渡点。Carreau-Yasuda 模型中的参数 $a$ 和 Cross 模型中的指数 $m$ 提供了额外的自由度，可以调节过渡区域的曲率和宽度，从而能更精确地拟合实验数据。在对数-对数坐标图上，这些模型呈现出具有非零曲率的“S”形曲线，完美地连接了两个水平的牛顿平台区 [@problem_id:3975919]。

#### 黏塑性流体

另一类重要的时间无关非牛顿流体是**黏塑性流体**（viscoplastic fluids），例如泥浆、牙膏和某些食品。它们的特点是存在一个**屈服应力**（yield stress）$\tau_y$。当施加的应力低于屈服应力时，材料表现为固体（或非常高黏度的流体）；只有当应力超过屈服应力时，材料才会像液体一样流动。

- **屈服准则**：为了在复杂流动中判断材料是否屈服，需要一个客观的屈服准则。这通常通过偏应力张量的不变量来定义。常用的**等效剪切应力** $\tau_{\text{eq}}$ 为：
  $\tau_{\text{eq}} = \sqrt{\frac{1}{2}\boldsymbol{\tau}:\boldsymbol{\tau}}$
  屈服条件即为 $\tau_{\text{eq}}  \tau_y$。当 $\tau_{\text{eq}} \le \tau_y$ 时，材料处于未屈服状态，变形率张量为零（$\mathbf{D} = \mathbf{0}$），形成所谓的**刚性栓塞流**（rigid plug）[@problem_id:3975939]。

- **Bingham 模型** 和 **Herschel-Bulkley 模型**：
  - **Bingham 模型** 是最简单的黏塑性模型。在屈服区，其行为类似于牛顿流体，但应力中包含一个屈服项。其张量形式为：
    $\boldsymbol{\tau} = 2\left(\frac{\tau_y}{\dot{\gamma}} + \mu_p \right)\mathbf{D} \quad (\text{当 } \tau_{\text{eq}}  \tau_y)$
    其中 $\mu_p$ 是**塑性黏度**（plastic viscosity）。
  - **Herschel-Bulkley 模型** 是 Bingham 模型的推广，它在屈服区引入了幂律行为，能更广泛地描述黏塑性流体的剪切致稀或增稠特性：
    $\boldsymbol{\tau} = 2\left(\frac{\tau_y}{\dot{\gamma}} + K\dot{\gamma}^{n-1} \right)\mathbf{D} \quad (\text{当 } \tau_{\text{eq}}  \tau_y)$
    显然，当 $n=1$ 且 $K=\mu_p$ 时，Herschel-Bulkley 模型退化为 Bingham 模型 [@problem_id:3975939]。

### 黏弹性流体

许多高分子熔体和溶液表现出**黏弹性**（viscoelasticity），即同时具有黏性流体的耗散特性和弹性固体的储能特性。这种双重行为源于其大分子链的复杂构象和动力学。

#### 黏弹性的宏观现象与量化

- **法向应力差 (Normal Stress Differences)**：黏弹性的一个标志性现象是在简单剪切流中会产生不为零的法向应力分量。**第一法向应力差** $N_1 = \tau_{xx} - \tau_{yy}$ 和**第二法向应力差** $N_2 = \tau_{yy} - \tau_{zz}$ （其中 $x$ 为流动方向，$y$ 为速度梯度方向）的出现是Weissenberg效应的体现，它导致了诸如“爬杆效应”等奇特现象。对于广义牛顿流体，$N_1$ 和 $N_2$ 恒为零。这些量是衡量流体弹性的重要指标，可以通过旋转流变仪测量。例如，在锥板流变仪中，测得的法向力 $F_N$ 是 $N_1$ 和 $N_2$ 的组合函数，这表明仅通过单次锥板测量无法将二者完全解耦 [@problem_id:3975915]。

- **无量纲数**：为了评估弹性效应的重要性，引入了两个关键的无量纲数。
  - **Weissenberg 数 ($Wi$)**：定义为 $Wi = \lambda \dot{\gamma}$，其中 $\lambda$ 是材料的特征弛豫时间。$Wi$ 比较了材料的弛豫时间与流动的特征时间（由剪切率的倒数 $1/\dot{\gamma}$ 定义）。它主要用于衡量**稳态流动**中弹性效应的强度。一个大的 $Wi$ 值意味着在稳态剪切下，弹性（如法向应力）相对于黏性应力非常显著。
  - **Deborah 数 ($De$)**：定义为 $De = \lambda / t_{\text{obs}}$，其中 $t_{\text{obs}}$ 是观察或实验的特征时间。$De$ 比较了材料弛豫时间与外部过程的时间尺度。它主要用于衡量流动的**非稳态性**或**瞬态性**。如果 $De \ll 1$，材料有足够的时间弛豫，流动接近准稳态。如果 $De \gg 1$，过程比材料弛豫快得多，材料表现出强烈的弹性、类似固体的行为。在稳态流动中，$Wi$ 是关键参数；而在启动、停止或振荡流动中，$De$ 则扮演着核心角色 [@problem_id:3975883]。

#### 黏弹性本构模型

黏弹性模型旨在描述应力与整个变形历史之间的关系，主要分为微分模型和积分模型两大类。

- **微分本构模型 (Differential Models)**：这类模型通过应力张量的演化方程来表达记忆效应。
  - **上随体 Maxwell 模型 (Upper-Convected Maxwell, UCM)** 是一个原型：
    $\boldsymbol{\tau} + \lambda \overset{\nabla}{\boldsymbol{\tau}} = 2\eta_p \mathbf{D}$
    其中 $\eta_p$ 是聚合物黏度，$\overset{\nabla}{\boldsymbol{\tau}}$ 是上随体时间导数，它是一种客观应力率。这个模型将流体想象成一个由弹簧（代表弹性）和阻尼器（代表黏性）串联组成的系统。$\lambda$ 是与弹簧和阻尼器特性相关的弛豫时间。这类模型必须使用客观应力率以满足材料坐标系无关性原理 [@problem_id:3975883]。

- **积分本构模型 (Integral Models)**：这类模型直接通过一个时间积分来表达应力对过去所有变形历史的依赖，体现了“衰退记忆”（fading memory）的思想。
  - **Lodge 类橡胶液体模型 (Lodge Rubberlike Liquid Model)** 是一个经典的例子：
    $\boldsymbol{\tau}(t) = \int_{-\infty}^{t} G(t-s) \left[\mathbf{B}(t,s) - \mathbf{I}\right] \mathrm{d}s$
    该模型的应力是过去所有时间步 $s$ 贡献的总和。每个时间步的贡献由两部分决定：一是**记忆函数**或**弛豫模量** $G(t-s)$，它描述了记忆随时间流逝（$\theta = t-s$）的衰减；二是**Finger 应变张量** $\mathbf{B}(t,s)$，它量化了从过去时刻 $s$ 到当前时刻 $t$ 的相对变形。$\mathbf{B}(t,s) - \mathbf{I}$ 的形式确保了在静止状态下（无变形历史）应力为零 [@problem_id:3975933]。
  - 这类积分模型可以从微观理论中得到支持。例如，在**Doi-Edwards 管模型**中，高分子链被限制在由周围链形成的“管子”中运动。模型的记忆函数与管段的“存活概率”直接相关，即一个在过去创建的管段在当前时刻仍然存在的概率。通过将这种微观图像与宏观应变张量相结合，可以推导出剪切应力、法向应力差等流变学函数，从而将宏观行为与分子动力学联系起来 [@problem_id:3975929]。

### 触变性与流凝性流体

除了上述行为，一些流体的黏度还依赖于剪切历史的持续时间。这种时间依赖性源于材料内部微观结构的演化。

- **触变性 (Thixotropy)**：指材料在恒定剪切作用下黏度随时间降低，而在静置后黏度又逐渐恢复的现象。这通常是由于剪切作用破坏了材料内部的絮凝结构或网络。
- **流凝性 (Rheopexy)**：是与触变性相反的现象，指材料在剪切作用下黏度随时间增加，静置后恢复。这通常与剪切诱导的结构形成有关。

为了模拟这种行为，一种常用的方法是引入一个标量的**结构参数** $\lambda_s$（通常取值在 $0$ 到 $1$ 之间），它代表了材料内部结构的完整程度。表观黏度被认为是 $\lambda_s$ 和当前剪切率 $\dot{\gamma}$ 的函数，$\mu = \mu(\lambda_s, \dot{\gamma})$。

结构参数本身则遵循一个演化动力学方程，其一般形式为一阶松弛方程：

$\frac{\mathrm{d}\lambda_s}{\mathrm{d}t} = -\frac{\lambda_s - \lambda_{\mathrm{eq}}(\dot{\gamma})}{\tau(\dot{\gamma})}$

这里，$\lambda_{\mathrm{eq}}(\dot{\gamma})$ 是在给定剪切率 $\dot{\gamma}$ 下，结构最终达到的平衡状态；$\tau$ 是达到该平衡所需的特征时间。

- 对于**触变性**，高剪切率会破坏结构，因此 $\lambda_{\mathrm{eq}}(\dot{\gamma})$ 应是 $\dot{\gamma}$ 的减函数。黏度通常是 $\lambda_s$ 的增函数。
- 对于**流凝性**，高剪切率会促进结构形成，因此 $\lambda_{\mathrm{eq}}(\dot{\gamma})$ 应是 $\dot{\gamma}$ 的增函数。

通过选择合适的 $\lambda_{\mathrm{eq}}(\dot{\gamma})$ 和 $\mu(\lambda_s, \dot{\gamma})$ 的函数形式，就可以定量地描述这些复杂的时间依赖行为 [@problem_id:3975934]。

### 温度的影响

温度是影响流体黏度的最重要参数之一。对于高分子熔体等材料，黏度对温度的依赖性极强，一个微小的温度变化就可能导致黏度几个数量级的改变。

- **Arrhenius 定律**：在远高于玻璃化转变温度 $T_g$ 的区域，许多液体的零剪切黏度 $\eta_0$ 对温度的依赖性遵循 **Arrhenius 定律**：
  $\eta_0(T) = \eta_0^{\ast} \exp\left(\frac{E_a}{R T}\right)$
  该定律源于一个微观图像：流体流动被视为由热激活的局部重排事件驱动。$E_a$ 是流动过程的**活化能**，$R$ 是摩尔气体常数。在 $\ln(\eta_0)$ 对 $1/T$ 的图中，Arrhenius 行为表现为一条直线。

- **Williams–Landel–Ferry (WLF) 方程**：当温度接近玻璃化转变温度 $T_g$ 时，Arrhenius 定律失效。黏度随温度降低的增长速度远比 Arrhenius 预测的要快，这种行为被称为**超 Arrhenius** (super-Arrhenius) 行为。这通常归因于“自由体积”的减少，分子的运动空间受到严重限制。**WLF 方程**是一个被广泛应用的经验模型，用于描述这个区域的黏度行为。其标准形式是：
  $\log_{10}\left(\frac{\eta_0(T)}{\eta_0(T_{\text{ref}})}\right) = \frac{-C_1 (T - T_{\text{ref}})}{C_2 + (T - T_{\text{ref}})}$
  其中 $T_{\text{ref}}$ 是一个参考温度，$C_1$ 和 $C_2$ 是材料常数。WLF 方程能够很好地描述黏度在趋近 $T_g$ 时的“准发散”行为，在 $\ln(\eta_0)$ 对 $1/T$ 的图中表现为一条向上弯曲的曲线 [@problem_id:3975948]。

理解并正确选择描述这些不同物理机制的本构模型，是进行精确的计算热工学仿真和设计的关键。