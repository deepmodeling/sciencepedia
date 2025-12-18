## 引言
[粘性流体动力学](@entry_id:756535)是理解从日常现象到宇宙奥秘中物质运动的关键，它研究的是内摩擦力（即粘性）如何支配流体的行为。然而，要将这一宏观效应与流体微元的运动和受力精确联系起来，需要一个严谨的物理和数学框架。本文旨在系统性地填补这一认知鸿沟，为读者构建一个从第一性原理到前沿应用的完整知识体系。

在接下来的内容中，我们将分三步展开：首先，在**“原理与机制”**一章中，我们将从连续介质假设出发，深入剖析[应力与应变率](@entry_id:263123)的关系，并最终推导出[流体动力](@entry_id:750449)学的基石——[纳维-斯托克斯方程](@entry_id:142275)。随后，在**“应用与跨学科联系”**一章中，我们将展示这些核心原理如何跨越尺度，应用于从工程润滑、生物力学到天体物理等看似迥异的领域，揭示其惊人的普适性。最后，通过**“动手实践”**部分，您将有机会运用所学知识解决具体的分析问题，将理论内化为实践能力。让我们一同开启这段探索粘性流动的旅程。

## 原理与机制

本章旨在深入探讨[粘性流体动力学](@entry_id:756535)的核心原理与内在机制。在前一章介绍流体动力学宏观背景的基础上，我们将从第一性原理出发，系统地构建描述粘性流体运动的数学与物理框架。我们将首先确立流体作为连续介质的适用范围，然后剖析流体微元的运动学特性，即变形与旋转。接着，我们将引入[应力张量](@entry_id:148973)的概念来描述流体内部的力，并建立[应力与应变率](@entry_id:263123)之间的[本构关系](@entry_id:186508)，这是区分不同类型流体的关键。最终，我们将这些要素整合，推导出流体运动的基本控制方程——[纳维-斯托克斯方程](@entry_id:142275)，并探讨其在不同流动状态下的简化与应用。本章还将通过[无量纲分析](@entry_id:188181)揭示主导流动的关键参数，并展示如何将基本原理类比应用于[湍流](@entry_id:151300)等更复杂的现象中。

### 连续介质假设：连接微观与宏观的桥梁

流体本质上是由大量遵循[牛顿定律](@entry_id:163541)的离散分子组成的系统。然而，在宏观尺度上追踪每一个分子的运动既无可能也无必要。流体动力学通过引入**连续介质假设 (continuum hypothesis)**，成功地将这一离散系统替换为连续的场，如密度场 $\rho(\boldsymbol{x},t)$、速度场 $\boldsymbol{u}(\boldsymbol{x},t)$ 和温度场 $T(\boldsymbol{x},t)$。

这一假设的核心是**尺度分离 (scale separation)** 的概念。为了使宏观场量有明确的物理意义，我们必须能够定义一个**代表性基本体积 (Representative Elementary Volume, REV)**。这个REV的线性尺度 $\ell$ 必须远大于分子的平均自由程 $\lambda$（即分子两次连续碰撞之间平均走过的距离），以确保其内部包含足够多的分子，使得统计平均值（如密度、速度）具有稳定性且涨落可以忽略。同时，$\ell$ 又必须远小于流体宏观性质发生显著变化的特征长度 $L$（例如，管道的直径或[翼型](@entry_id:195951)的弦长），这样我们才能将REV内的平均值视为空间点 $\boldsymbol{x}$ 处的场量值，并保证这些场是光滑可微的。这个尺度分离的条件可以表示为不等式链：$\lambda \ll \ell \ll L$。

该不等式链成立的前提是微观尺度与宏观尺度之间存在巨大的鸿沟，即 $\lambda \ll L$。这一基本要求可以通过一个[无量纲参数](@entry_id:169335)——**努森数 (Knudsen number)** 来量化：

$$ \mathrm{Kn} = \frac{\lambda}{L} $$

因此，连续介质假设的有效性，等价于要求 **努森数远小于1**，即 $\mathrm{Kn} \ll 1$。

当 $\mathrm{Kn} \ll 1$ 时，宏观场量在单个分子自由程尺度上的梯度变化极小。这一条件与系统处于**局部热力学平衡 (Local Thermodynamic Equilibrium, LTE)** 状态是内在一致的。LTE意味着在任何一个REV内，分子的碰撞足够频繁，使得其速度分布能够迅速弛豫到与局部宏观温度和速度相对应的麦克斯韦-玻尔兹曼分布附近。定量地，对于任何一个宏观场 $\phi$（如密度或温度），LTE要求 $|\nabla \phi| \lambda / |\phi| \ll 1$，这正是 $\mathrm{Kn} \ll 1$ 的另一种表述 。

努森数不仅定义了连续介质模型的[适用范围](@entry_id:636189)，还决定了边界条件的具体形式。对于气体流动：
- 当 $\mathrm{Kn} \lesssim 0.01$ 时，流体可以被精确地描述为连续介质，并且在固体壁面处满足经典的**[无滑移边界条件](@entry_id:186229) (no-slip boundary conditions)**。
- 当 $0.01 \lesssim \mathrm{Kn} \lesssim 0.1$ 时，流体主体部分依然可以用连续介质方程描述，但壁面附近分子与壁面的相互作用变得不可忽略，需要引入**[滑移流](@entry_id:154133) (slip-flow)** 修正。
- 当 $\mathrm{Kn} \approx 1$ 或更大时，连续介质假设完全失效，必须采用基于玻尔兹曼方程或分子动力学的方法，如[直接模拟蒙特卡洛 (DSMC)](@entry_id:748474) 方法。

此外，努森数也揭示了时间和空间尺度的关联。将分子平均自由程写为 $\lambda \approx c \tau_c$，其中 $c$ 是分子热运动特征速率，$\tau_c$ 是分子平均[碰撞时间](@entry_id:261390)。宏观过程的时间尺度可估计为 $T_{macro} \sim L/c_s$，其中 $c_s$ 是声速。由于 $c$ 和 $c_s$ 量级相同，我们得到 $\tau_c / T_{macro} \sim \lambda / L = \mathrm{Kn}$。因此，$\mathrm{Kn} \ll 1$ 同时意味着微观[碰撞时间](@entry_id:261390)远小于宏观流动时间 ($\tau_c \ll T_{macro}$)。这种时间尺度分离是输运系数（如粘性系数）可以被视为局部[热力学状态](@entry_id:755916)的函数（而非依赖于流动历史）的根本原因 。

### 流体运动的运动学：变形与旋转

在连续介质框架下，流体的局部运动可以通过其速度场 $\boldsymbol{u}(\boldsymbol{x},t)$ 的梯度来描述。考虑流体中两个相距一个无穷小矢量 $\delta\boldsymbol{x}$ 的邻近质点，它们的[相对速度](@entry_id:178060) $\delta\dot{\boldsymbol{x}}$ 由[速度梯度张量](@entry_id:270928) $\nabla\boldsymbol{u}$ 决定：$\delta\dot{\boldsymbol{x}} = (\nabla\boldsymbol{u})\delta\boldsymbol{x}$。

[速度梯度张量](@entry_id:270928) $\nabla\boldsymbol{u}$ 是一个[二阶张量](@entry_id:199780)，它可以被唯一地分解为一个对称部分和一个反对称部分：

$$ \nabla\boldsymbol{u} = \boldsymbol{E} + \boldsymbol{W} $$

其中，$\boldsymbol{E}$ 是对称的**[应变率张量](@entry_id:266108) (rate-of-strain tensor)**，$\boldsymbol{W}$ 是反对称的**[自旋张量](@entry_id:187346) (spin tensor)** 或**[涡量张量](@entry_id:189621) (vorticity tensor)**。

$$ \boldsymbol{E} = \frac{1}{2}\left(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^{\top}\right) $$
$$ \boldsymbol{W} = \frac{1}{2}\left(\nabla\boldsymbol{u} - (\nabla\boldsymbol{u})^{\top}\right) $$

这个分解在[流体运动学](@entry_id:202835)中至关重要，因为它将一个复杂的局部运动清晰地分离为纯变形和纯刚性旋转两种[基本模式](@entry_id:165201)。

#### 对称部分：应变率张量

应变率张量 $\boldsymbol{E}$ 描述了流体微元的形状和体积如何随时间变化。我们可以通过考察连接两个质点的物质[线元](@entry_id:196833) $\boldsymbol{r}(t)$ 的长度平方的变化率来理解其物理意义 ：

$$ \frac{\mathrm{d}}{\mathrm{d}t}(\boldsymbol{r}\cdot\boldsymbol{r}) = 2\boldsymbol{r}\cdot\frac{\mathrm{d}\boldsymbol{r}}{\mathrm{d}t} = 2\boldsymbol{r}\cdot((\nabla\boldsymbol{u})\boldsymbol{r}) = 2\boldsymbol{r}\cdot(\boldsymbol{E}\boldsymbol{r}) + 2\boldsymbol{r}\cdot(\boldsymbol{W}\boldsymbol{r}) $$

由于 $\boldsymbol{W}$ 是反对称的，二次型 $\boldsymbol{r}\cdot(\boldsymbol{W}\boldsymbol{r})$ 恒等于零。因此，

$$ \frac{\mathrm{d}}{\mathrm{d}t}(\boldsymbol{r}\cdot\boldsymbol{r}) = 2\boldsymbol{r}\cdot(\boldsymbol{E}\boldsymbol{r}) $$

这个结果表明，物质[线元](@entry_id:196833)长度的变化率（即拉伸或压缩）完全由对称的应变率张量 $\boldsymbol{E}$ 决定。类似地，可以证明两个物质[线元](@entry_id:196833)之间夹角的变化率也仅由 $\boldsymbol{E}$ 决定。因此，$\boldsymbol{E}$ 是流体微元变形的唯一度量。

$\boldsymbol{E}$ 的对角分量 $E_{ii}$ 表示沿坐标轴方向的线[应变率](@entry_id:154778)，而非对角分量 $E_{ij}$ ($i \neq j$) 表示相应平面内夹角的[剪切应变率](@entry_id:276945)。$\boldsymbol{E}$ 的迹表示流体微元的体积膨胀率：

$$ \mathrm{tr}(\boldsymbol{E}) = \frac{1}{2}\mathrm{tr}(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^{\top}) = \mathrm{tr}(\nabla\boldsymbol{u}) = \nabla\cdot\boldsymbol{u} $$

对于**[不可压缩流](@entry_id:140301) (incompressible flow)**，其定义就是体积不变，即 $\nabla\cdot\boldsymbol{u} = 0$，这意味着[应变率张量](@entry_id:266108)的迹为零。例如，一个二维纯拉伸流 $\boldsymbol{u}=(\alpha x, -\alpha y, 0)$，其应变率张量非零但迹为零，符合不可压缩的特性 。

#### 反对称部分：[自旋张量](@entry_id:187346)

[自旋张量](@entry_id:187346) $\boldsymbol{W}$ 描述了流体微元的纯刚性转动，它不引起任何形状或体积的改变。$\boldsymbol{W}$ 与另一个重要的运动学向量——**涡量 (vorticity)** 密切相关。[涡量](@entry_id:142747)定义为[速度场的旋度](@entry_id:183606)：

$$ \boldsymbol{\omega} = \nabla \times \boldsymbol{u} $$

可以证明，[自旋张量](@entry_id:187346) $\boldsymbol{W}$ 对邻近[质点](@entry_id:186768)相对速度的贡献 $\boldsymbol{W}\boldsymbol{r}$，等效于一个[角速度](@entry_id:192539)为 $\frac{1}{2}\boldsymbol{\omega}$ 的刚性旋转所产生的速度场 ：

$$ \boldsymbol{W}\boldsymbol{r} = \frac{1}{2}\boldsymbol{\omega} \times \boldsymbol{r} $$

因此，[涡量](@entry_id:142747) $\boldsymbol{\omega}$ 的大小是流体微元刚性转动角速度的两倍。在流体中，涡量非零的区域即为有旋区。一个简单的例子是[刚体](@entry_id:1131033)[旋转流](@entry_id:276737) $\boldsymbol{u} = \boldsymbol{\Omega} \times \boldsymbol{x}$，其中 $\boldsymbol{\Omega}$ 是一个恒定的角速度向量。对于这种流动，可以计算出[应变率张量](@entry_id:266108) $\boldsymbol{E} = \boldsymbol{0}$（没有变形），而涡量 $\boldsymbol{\omega} = 2\boldsymbol{\Omega}$ 。这清晰地说明了变形和旋转的独立性。

### 流体中的力：应力与压力

根据[牛顿第二定律](@entry_id:274217)，流体微元的动量变化是由作用在其上的力引起的。这些力分为两类：作用于整个体积的**[体力](@entry_id:174230) (body forces)**（如重力），以及作用于其表面的**面力 (surface forces)**。

在连续介质中，面力通过**接触应力 (contact stress)** 来描述。在流体微元表面的任意一点，作用在单位面积上的面力被称为**[面力矢量](@entry_id:189429) (traction vector)**，记为 $\boldsymbol{t}$。根据**柯西公设 (Cauchy's postulate)**，[面力矢量](@entry_id:189429)不仅依赖于空间位置和时间，还依赖于该点处表面的朝向，这个朝向由表面的单位外法向量 $\boldsymbol{n}$ 描述。

通过对一个无限小的四面体微元进行力平衡分析（柯西四面体论证），可以证明[面力矢量](@entry_id:189429) $\boldsymbol{t}$ 与[法向量](@entry_id:264185) $\boldsymbol{n}$ 之间存在一个[线性映射](@entry_id:185132)关系。这个关系定义了**柯西[应力张量](@entry_id:148973) (Cauchy stress tensor)** $\boldsymbol{\sigma}$，它是一个[二阶张量](@entry_id:199780)，完全描述了某一点的应力状态：

$$ \boldsymbol{t}(\boldsymbol{n}) = \boldsymbol{\sigma}\boldsymbol{n} $$

柯西应力张量 $\boldsymbol{\sigma}_{ij}$ 的物理意义是：作用在以 $j$ 轴为[法线](@entry_id:167651)的微小平面上、指向 $i$ 方向的单位面积力。$\boldsymbol{\sigma}$ 的对角分量 $\sigma_{ii}$ 称为**[正应力](@entry_id:260622) (normal stresses)**，非对角分量 $\sigma_{ij}$ ($i \neq j$) 称为**剪应力 (shear stresses)**。作用在法向为 $\boldsymbol{n}$ 的表面上的正应力为 $\sigma_n = \boldsymbol{n} \cdot \boldsymbol{t}(\boldsymbol{n}) = \boldsymbol{n} \cdot \boldsymbol{\sigma}\boldsymbol{n}$。

对于流体，通常将[应力张量](@entry_id:148973)分解为一个各向同性的部分和一个偏量部分 ：

$$ \boldsymbol{\sigma} = -p\boldsymbol{I} + \boldsymbol{\tau} $$

这里，$\boldsymbol{I}$ 是单位张量。标量 $p$ 是**[热力学压力](@entry_id:1133073) (thermodynamic pressure)**，它代表了流体在静止平衡时产生的各向同性的压缩应力。在流体中，压力习惯上取为正值，表示压缩，因此前面有一个负号。张量 $\boldsymbol{\tau}$ 被称为**[偏应力张量](@entry_id:267642) (deviatoric stress tensor)** 或**粘性应力张量 (viscous stress tensor)**，它代表了由流体运动（变形）引起的附加应力，并在流体静止时为零。这个分解明确了流体内部力的两个来源：一个是[静压](@entry_id:275419)，另一个是由运动产生的粘性力。

### [本构关系](@entry_id:186508)：连接运动学与应力

本构关系（constitutive relation）是描述特定材料应力如何响应变形的数学方程，它体现了材料的物理属性。对于[粘性流](@entry_id:136330)体，[本构关系](@entry_id:186508)将粘性应力 $\boldsymbol{\tau}$ 与应变率 $\boldsymbol{E}$ 联系起来。

#### 牛顿流体模型

最简单也是最常见的流体模型是**[牛顿流体](@entry_id:263796) (Newtonian fluid)**。其[本构关系](@entry_id:186508)基于以下假设：
1.  流体是**各向同性 (isotropic)** 的，其力学行为不依赖于方向。
2.  粘性应力 $\boldsymbol{\tau}$ 与[应变率](@entry_id:154778) $\boldsymbol{E}$ 之间是**线性**关系。
3.  关系满足**物质标架无关性 (material frame-indifference)** 或称**客观性 (objectivity)**，即本构关系在任何[旋转坐标系](@entry_id:170324)下形式不变。

[客观性原理](@entry_id:185412)要求[本构关系](@entry_id:186508)不能依赖于刚性转动，因此 $\boldsymbol{\tau}$ 只能是应变率张量 $\boldsymbol{E}$ 的函数，而不能是[自旋张量](@entry_id:187346) $\boldsymbol{W}$ 的函数。对于各向同性的线性关系，$\boldsymbol{\tau}$ 必须由 $\boldsymbol{E}$ 和单位张量 $\boldsymbol{I}$ [线性组合](@entry_id:154743)而成。最一般的形式为 ：

$$ \boldsymbol{\tau} = 2\mu\boldsymbol{E} + \lambda_b(\nabla\cdot\boldsymbol{u})\boldsymbol{I} $$

其中 $\mu$ 是**[剪切粘度](@entry_id:141046) (shear viscosity)** 或称**[动力粘度](@entry_id:268228) (dynamic viscosity)**，它度量了流体对[剪切变形](@entry_id:170920)的抵抗能力。$\lambda_b$ 是**[第二粘度](@entry_id:189253)系数 (second coefficient of viscosity)**，它与流体体积变化时的粘性效应有关。回顾到 $\nabla\cdot\boldsymbol{u} = \mathrm{tr}(\boldsymbol{E})$，这个关系清晰地表明[粘性应力](@entry_id:261328)来源于流体的变形。

#### [斯托克斯假设](@entry_id:195909)

在上述本构关系中，压力的定义出现了一个微妙之处。**力学压力 (mechanical pressure)** $p_m$ 定义为[正应力](@entry_id:260622)的平均值的[相反数](@entry_id:151709)：$p_m = -\frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})$。将[本构关系](@entry_id:186508)代入，我们发现力学压力和[热力学压力](@entry_id:1133073) $p_{th}$ 并不总是一致：

$$ p_m = -\frac{1}{3}\mathrm{tr}(-p_{th}\boldsymbol{I} + \boldsymbol{\tau}) = p_{th} - \frac{1}{3}\mathrm{tr}(\boldsymbol{\tau}) = p_{th} - \left(\lambda_b + \frac{2}{3}\mu\right)(\nabla\cdot\boldsymbol{u}) $$

括号中的组合 $\kappa = \lambda_b + \frac{2}{3}\mu$ 被称为**[体积粘度](@entry_id:187773) (bulk viscosity)**，它度量了流体在均匀压缩或膨胀时由于粘性产生的熵增。

**[斯托克斯假设](@entry_id:195909) (Stokes hypothesis)** 是一个广泛应用的简化，它假定[体积粘度](@entry_id:187773)为零，即 $\kappa = 0$。这等价于设定：

$$ \lambda_b = -\frac{2}{3}\mu $$

在该假设下，力学压力与[热力学压力](@entry_id:1133073)在任何流动中都相等，除非流体正在经历体积变化。[斯托克斯假设](@entry_id:195909)的物理基础是假定流体在经历体积变化时能够瞬间达到热力学平衡，这对于能量仅以[平动动能](@entry_id:174977)形式存在的[单原子气体](@entry_id:140562)是很好的近似。然而，对于多原子气体或液体，能量需要在[平动](@entry_id:187700)、转动和振动模式之间重新分配，这个过程需要有限的时间。如果流动的特征时间与这个[弛豫时间](@entry_id:191572)相当，[体积粘度](@entry_id:187773)就不可忽略 。

#### [广义牛顿流体](@entry_id:1125558)

许多真实流体，如[聚合物熔体](@entry_id:192068)、悬浮液和血液，表现出非牛顿行为，即其粘度不是常数，而是依赖于剪切的快慢。**[广义牛顿流体](@entry_id:1125558) (Generalized Newtonian Fluid, GNF)** 模型通过让剪切粘度 $\mu$ 成为[应变率张量](@entry_id:266108)不变量的函数，来描述这种现象。最常用的不变量是剪切率的量级，定义为 $\dot{\gamma} = \sqrt{2\boldsymbol{E}:\boldsymbol{E}}$。其本构关系为 ：

$$ \boldsymbol{\tau} = 2\mu(\dot{\gamma})\boldsymbol{E} $$

这种形式保持了粘性应力 $\boldsymbol{\tau}$ 和[应变率](@entry_id:154778) $\boldsymbol{E}$ 的[共线性](@entry_id:270224)，因此满足客观性和各向同性。[热力学](@entry_id:172368)第二定律要求[粘性耗散](@entry_id:143708)率 $\boldsymbol{\tau}:\boldsymbol{E} = \mu(\dot{\gamma})\dot{\gamma}^2 \ge 0$，这意味着 $\mu(\dot{\gamma})$ 必须始终为非负。

常见的GNF模型包括：
- **[幂律模型](@entry_id:272028) (Power-Law model)**：$\mu(\dot{\gamma}) = K\dot{\gamma}^{n-1}$。其中 $K$ 是稠度指数，$n$ 是幂律指数。当 $n  1$ 时，粘度随剪切率增加而减小，称为**剪切致稀 (shear-thinning)**。当 $n > 1$ 时，粘度随剪切率增加而增加，称为**[剪切增稠](@entry_id:260777) (shear-thickening)**。当 $n=1$ 时，恢复为牛顿流体，$\mu=K$。
- **卡罗模型 (Carreau model)**：$\mu(\dot{\gamma}) = \mu_{\infty} + (\mu_{0} - \mu_{\infty})[1 + (\lambda\dot{\gamma})^2]^{\frac{n-1}{2}}$。该模型能更好地描述许多流体在极低和极高剪切率下的行为，它包含一个零剪切粘度平台 $\mu_0$ 和一个无限剪切粘度平台 $\mu_\infty$，并通过一个特征时间 $\lambda$ 实现两者之间的过渡。

值得注意的是，所有GNF模型由于其 $\boldsymbol{\tau}$ 与 $\boldsymbol{E}$ 的[共线性](@entry_id:270224)，都无法预测在[简单剪切流](@entry_id:1131665)中观察到的非零法向应力差，这是更复杂的粘弹性流体模型的领域。

### [粘性流](@entry_id:136330)动的控制方程

将[质量守恒](@entry_id:204015)、[动量守恒](@entry_id:149964)（牛顿第二定律）和[本构关系](@entry_id:186508)相结合，我们便能得到描述粘性流体运动的完整控制方程组。

#### [不可压缩纳维-斯托克斯](@entry_id:750595)方程

对于密度 $\rho$ 和粘度 $\mu$ 均为常数的不可压缩[牛顿流体](@entry_id:263796)，控制方程的推导过程如下：
1.  **[质量守恒](@entry_id:204015)**：对于不可压缩流，$\nabla\cdot\boldsymbol{u}=0$。
2.  **动量守恒**：[柯西动量方程](@entry_id:187010)为 $\rho \frac{D\boldsymbol{u}}{Dt} = \nabla\cdot\boldsymbol{\sigma} + \rho\boldsymbol{f}$，其中 $\frac{D\boldsymbol{u}}{Dt} = \frac{\partial\boldsymbol{u}}{\partial t} + (\boldsymbol{u}\cdot\nabla)\boldsymbol{u}$ 是[物质导数](@entry_id:262900)，$\boldsymbol{f}$ 是单位质量的体力。
3.  **代入[本构关系](@entry_id:186508)**：将[应力张量](@entry_id:148973) $\boldsymbol{\sigma} = -p\boldsymbol{I} + \boldsymbol{\tau}$ 和不可压缩[牛顿流体的本构关系](@entry_id:1122933) $\boldsymbol{\tau}=2\mu\boldsymbol{E}$ 代入动量方程中的应力散度项：
    $$ \nabla\cdot\boldsymbol{\sigma} = \nabla\cdot(-p\boldsymbol{I} + 2\mu\boldsymbol{E}) = -\nabla p + 2\mu\nabla\cdot\boldsymbol{E} $$
4.  **简化粘性项**：利用 $\boldsymbol{E} = \frac{1}{2}(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^{\top})$ 和矢量恒等式 $\nabla\cdot((\nabla\boldsymbol{u})^{\top}) = \nabla(\nabla\cdot\boldsymbol{u})$，我们得到：
    $$ \nabla\cdot(2\boldsymbol{E}) = \nabla\cdot(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^{\top}) = \nabla^2\boldsymbol{u} + \nabla(\nabla\cdot\boldsymbol{u}) $$
    其中 $\nabla^2\boldsymbol{u}$ 是作用于速度向量的拉普拉斯算子。由于流体不可压缩，$\nabla\cdot\boldsymbol{u}=0$，因此[粘性力](@entry_id:263294)项最终简化为 $\mu\nabla^2\boldsymbol{u}$ 。

这个 $\mu\nabla^2\boldsymbol{u}$ 项代表了动量的粘性扩散。如同[热传导](@entry_id:143509)中温度梯度引起热量流动，[速度梯度](@entry_id:261686)在此引起动量从高速区向低速区传递，其扩散系数正是粘度 $\mu$。该项前面的正号保证了粘性作用总是耗散动能，符合[热力学](@entry_id:172368)第二定律。

最终，我们得到描述密度和粘度恒定的不可压缩[牛顿流体](@entry_id:263796)运动的**[纳维-斯托克斯方程](@entry_id:142275) ([Navier-Stokes](@entry_id:276387) equations)**：

$$ \nabla\cdot\boldsymbol{u} = 0 \quad (\text{质量守恒}) $$
$$ \rho\left(\frac{\partial\boldsymbol{u}}{\partial t} + (\boldsymbol{u}\cdot\nabla)\boldsymbol{u}\right) = -\nabla p + \mu\nabla^2\boldsymbol{u} + \rho\boldsymbol{f} \quad (\text{动量守恒}) $$

通常将[动量方程](@entry_id:197225)除以密度 $\rho$，并引入**[运动粘度](@entry_id:275614) (kinematic viscosity)** $\nu = \mu/\rho$，得到其[标准形式](@entry_id:153058)。

#### [不可压缩流](@entry_id:140301)中压力的特殊角色

在[不可压缩纳维-斯托克斯](@entry_id:750595)方程组中，速度 $\boldsymbol{u}$ 有三个分量，压力 $p$ 有一个分量，总共四个未知数，但方程只有四个（一个连续性方程和三个[动量方程](@entry_id:197225)）。然而，这里没有像[可压缩流](@entry_id:747589)中那样的[状态方程](@entry_id:274378)（如理想气体定律）来直接关联压力和密度或温度。

在不可压缩流动中，压力 $p$ 的角色非常特殊：它不再是一个独立的[热力学变量](@entry_id:160587)，而是一个**约束变量 (constraint variable)** 。它的值会在流场中瞬时调整，以确保速度场在任何时刻都严格满足不可压缩约束 $\nabla\cdot\boldsymbol{u}=0$。可以把压力看作一个拉格朗日乘子。

我们可以通过对[动量方程](@entry_id:197225)两边取散度来导出一个关于压力的方程。由于 $\nabla\cdot(\nabla\cdot\boldsymbol{u})=0$，我们得到一个**[压力泊松方程](@entry_id:1129887) (Pressure Poisson Equation)**：

$$ \nabla^2 p = \nabla\cdot(\rho\boldsymbol{f}) - \rho\nabla\cdot((\boldsymbol{u}\cdot\nabla)\boldsymbol{u}) $$

这个椭圆型[偏微分](@entry_id:194612)方程表明，在任意时刻，只要速度场 $\boldsymbol{u}$ 和体力 $\boldsymbol{f}$ 已知，压[力场](@entry_id:147325) $p$ 就被完全确定（相差一个任意常数）。压力的梯度 $\nabla p$ 作为一个力，确保了流体在运动过程中不会被压缩。这种处理方式的物理基础是，[不可压缩流](@entry_id:140301)可以视为声速无穷大（或[马赫数](@entry_id:274014)趋于零）的极限情况。在这种极限下，任何局部的压力扰动都会以无穷大的速度传播至整个流场，以维持处处不可压缩的约束 。

### [无量纲分析](@entry_id:188181)与流动状态

[纳维-斯托克斯方程](@entry_id:142275)包含了[惯性力](@entry_id:169104)、压力[梯度力](@entry_id:166847)、粘性力和[体力](@entry_id:174230)等多种物理效应。为了评估这些效应的相对重要性，我们可以对方程进行无量纲化。

考虑一个特征速度为 $U$、特征长度为 $L$ 的流动。我们引入无量纲变量：$\hat{\boldsymbol{x}}=\boldsymbol{x}/L$, $\hat{t}=t/(L/U)$, $\hat{\boldsymbol{u}}=\boldsymbol{u}/U$, 以及 $\hat{p}=p/(\rho U^2)$。将这些变量代入[不可压缩纳维-斯托克斯](@entry_id:750595)方程（忽略体力），经过整理可以得到 ：

$$ \frac{\partial\hat{\boldsymbol{u}}}{\partial\hat{t}} + (\hat{\boldsymbol{u}}\cdot\hat{\nabla})\hat{\boldsymbol{u}} = -\hat{\nabla}\hat{p} + \frac{\mu}{\rho U L}\hat{\nabla}^2\hat{\boldsymbol{u}} $$

方程右侧粘性项的系数是一个[无量纲数](@entry_id:260863)，其倒数被定义为**雷诺数 (Reynolds number)**, $Re$：

$$ \mathrm{Re} = \frac{\rho U L}{\mu} = \frac{U L}{\nu} $$

雷诺数代表了流动中**惯性力与粘性力的比值**。
- 当 $Re \ll 1$ 时，粘性力占主导地位，流动平缓且有序，称为斯托克斯流或[蠕动流](@entry_id:263844)。
- 当 $Re \gg 1$ 时，惯性力占主导地位，流动可能变得不稳定，并最终[转捩](@entry_id:150036)为[湍流](@entry_id:151300)。

雷诺数是流体动力学中最重要的[无量纲参数](@entry_id:169335)之一，是判断流动状态（层流或[湍流](@entry_id:151300)）和决定[流动相似性](@entry_id:1125109)的关键。

### 原理的延伸：[湍流](@entry_id:151300)粘性模型

粘性[本构关系](@entry_id:186508)的基本思想，即[应力与应变率](@entry_id:263123)相关，也可以被类比地应用于更复杂的现象，例如[湍流](@entry_id:151300)。在**雷诺平均纳维-斯托克斯 (Reynolds-Averaged [Navier-Stokes](@entry_id:276387), RANS)** 方法中，我们将[瞬时速度](@entry_id:167797)分解为平均速度 $\boldsymbol{U}$ 和脉动速度 $\boldsymbol{u}'$。对动量方程取平均后，会出现一个新的项，即**[雷诺应力张量](@entry_id:270803)** $-\rho\overline{u_i'u_j'}$，它代表了[湍流](@entry_id:151300)脉动对平均动量的输运效应。

为了封闭方程组，需要对雷诺应力进行建模。**Boussinesq[涡粘性假设](@entry_id:1124144) (Boussinesq eddy viscosity hypothesis)** 正是借鉴了[牛顿流体的本构关系](@entry_id:1122933)，它假设[雷诺应力](@entry_id:263788)的偏量部分与平均应变率张量 $\boldsymbol{S}_{ij} = \frac{1}{2}(\frac{\partial U_i}{\partial x_j} + \frac{\partial U_j}{\partial x_i})$ 成正比 ：

$$ -\overline{u_i'u_j'} = 2\nu_t S_{ij} - \frac{2}{3}k\delta_{ij} $$

这里，$\nu_t$ 是**涡粘性系数 (eddy viscosity)**，它不是流体的物理属性，而是与流动状态（如湍流强度和尺度）相关的量。$k = \frac{1}{2}\overline{u_k'u_k'}$ 是湍动能。

这个模型将复杂的[湍流](@entry_id:151300)脉动效应简化为一种增强的、各向同性的“扩散”过程，极大地简化了计算。然而，这个类比有其根本局限性。真实的[湍流](@entry_id:151300)输运是高度**各向异性**、**非局部**且具有**历史效应**的。[Boussinesq假设](@entry_id:272519)强制雷诺应力张量的[主轴](@entry_id:172691)与平均应变率张量的[主轴](@entry_id:172691)对齐，这与实验中在旋转流、曲壁流、分离流等复杂流动中观察到的现象严重不符。尽管有这些缺陷，[涡粘性模型](@entry_id:1124145)因其简单和鲁棒性，在工程应用中仍被广泛使用，但理解其基本假设和局限性对于正确解释其预测结果至关重要。