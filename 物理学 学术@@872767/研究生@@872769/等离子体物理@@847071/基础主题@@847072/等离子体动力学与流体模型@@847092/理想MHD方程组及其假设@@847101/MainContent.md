## 引言
磁[流体力学](@entry_id:136788)（Magnetohydrodynamics, MHD）为理解等离子体的集体行为提供了不可或缺的理论框架，它不再将等离子体视为海量单个粒子的集合，而是作为一个单一的导电流体来处理。这种宏观方法优雅地绕开了动理学理论的巨大复杂性，但其控制方程是如何推导的？其背后又依赖哪些基本假设？本文旨在通过对理想MHD模型进行全面探讨来填补这一认知空白。在第一章“原理与机制”中，我们将推导完整的理想MHD[方程组](@entry_id:193238)，并深入剖析“磁冻结”定理等核心概念。第二章“应用与跨学科联系”将通过在受控[核聚变](@entry_id:139312)和天体物理学等领域的实际问题，展示该模型的强大解释力。最后，“动手实践”部分将提供练习题以巩固这些原理。现在，让我们从构建这一强大模型的理论基础开始。

## 原理与机制

在[等离子体物理学](@entry_id:139151)中，磁[流体力学](@entry_id:136788)（**Magnetohydrodynamics, MHD**）模型将复杂的、由[带电粒子](@entry_id:160311)构成的等离子体简化为单一的、具有导电性的连续流体。这种宏观描述方法在处理天体物理和受控[核聚变](@entry_id:139312)等领域中大尺度、低频率的等离子体现象时极为有效。本章将深入探讨理想MHD模型的基本原理和核心机制，推导其控制方程，并阐明其成立所依赖的关键假设。

### 单流体模型：从双流体到单流体

等离子体本质上是由电子和一种或多种离子组成的混合物，每种组分都有其自身的密度、温度和速度。原则上，我们需要为每种组分建立一套[流体方程](@entry_id:195729)，这便是所谓的“多流体模型”。然而，在许多情况下，我们可以通过一系列合理的近似，将这个复杂系统简化为一个“单流体”模型。

我们定义几个宏观的单流体变量。首先是**质量密度** $\rho$，它由离子和电子的质量密度加和而成：
$$
\rho = m_i n_i + m_e n_e
$$
其中 $n_s$ 和 $m_s$ 分别是组分 $s$（$i$ 代表离子，$e$ 代表电子）的数密度和[粒子质量](@entry_id:156313)。其次是**流体速度** $\mathbf{v}$，它代表了等离子体的[质心运动](@entry_id:178374)速度：
$$
\rho \mathbf{v} = m_i n_i \mathbf{v}_i + m_e n_e \mathbf{v}_e
$$
由于电子质量远小于离子质量（$m_e \ll m_i$），在大多数情况下，我们可以忽略电子对总质量密度和动量的贡献。同时，等离子体在大尺度上表现出**[准中性](@entry_id:184567)**（**quasineutrality**），即 $n_i \approx n_e = n$。在这些近似下，质量密度和流体速度可以简化为：
$$
\rho \approx m_i n
$$
$$
\mathbf{v} \approx \mathbf{v}_i
$$
即等离子体的质量和动量主要由离子携带。

基于这些单流体变量，我们可以从各组分的粒子数守恒方程出发，推导单流体的[质量守恒定律](@entry_id:147377)，即**连续性方程**。单个组分的连续性方程为：
$$
\frac{\partial n_s}{\partial t} + \nabla \cdot (n_s \mathbf{v}_s) = S_s
$$
其中 $S_s$ 是单位体积内粒子数的净产生率。将离子和电子的方程分别乘以其质量并相加，在 $m_e \ll m_i$ 的近似下，我们得到单流体的质量[连续性方程](@entry_id:195013)：
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) = S_m
$$
其中 $S_m \approx m_i S_i$ 是质量源项。若没有[粒子产生](@entry_id:158755)或湮灭（例如，没有电离或复合），则 $S_m = 0$，方程恢复为标准形式。

一个具体的例子可以帮助我们理解源项的作用。考虑一个通过[电子碰撞电离](@entry_id:164299)中性气体产生、并通过电子-离子复合而损失的[稳态](@entry_id:182458)等离子体。此时，[源项](@entry_id:269111)不为零。在一个一维[稳态模型](@entry_id:157508)中（$\frac{\partial}{\partial t} = 0$），质量[连续性方程](@entry_id:195013)变为 $\nabla \cdot (\rho \mathbf{v}) = S_m$。这意味着从体积内流出的质量通量必须精确等于该体积内净产生的质量。如果我们知道[等离子体密度](@entry_id:202836)[分布](@entry_id:182848)的函数形式（例如，通过实验观测得到），这个[守恒定律](@entry_id:269268)就能对系统参数施加严格的约束。例如，对于一个具有抛物线型密度[分布](@entry_id:182848)的[稳态](@entry_id:182458)放电等离子体，为了保证等离子体在边界处的流速为有限值，其中央密度必须满足一个由电离率和复合率决定的特定关系 [@problem_id:343846]。

### 理想MHD[方程组](@entry_id:193238)

理想MHD模型由一套描述质量、动量、能量和[磁通量守恒](@entry_id:199588)的封闭[方程组](@entry_id:193238)构成。这些方程共同描绘了理想导电流体的动力学行为。

#### 动量方程与[洛伦兹力](@entry_id:145104)

[等离子体流体](@entry_id:187430)元的运动由[动量方程](@entry_id:197225)（其形式类似于[流体力学](@entry_id:136788)中的欧拉方程）描述，但增加了一个关键的力——**[洛伦兹力](@entry_id:145104)**：
$$
\rho \left( \frac{\partial \mathbf{v}}{\partial t} + (\mathbf{v} \cdot \nabla) \mathbf{v} \right) = -\nabla p + \mathbf{J} \times \mathbf{B}
$$
左侧是单位体积流体的惯性项，$\frac{d\mathbf{v}}{dt} = \frac{\partial \mathbf{v}}{\partial t} + (\mathbf{v} \cdot \nabla) \mathbf{v}$ 是流体元的**随动导数**。右侧是作用在流体元上的力：热[压力[梯度](@entry_id:262279)力](@entry_id:166847) $-\nabla p$ 和单位体积的洛伦兹力 $\mathbf{J} \times \mathbf{B}$。

在MHD的低频近似下，[电流密度](@entry_id:190690) $\mathbf{J}$ 主要由[磁场](@entry_id:153296)的卷曲决定，即[安培定律](@entry_id:140092)的简化形式 $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}$（忽略了[位移电流](@entry_id:190231)，我们将在后面讨论其合理性）。将此关系代入洛伦兹力表达式，并利用矢量恒等式，我们可以将洛伦兹力分解为两个具有明确物理意义的部分：
$$
\mathbf{J} \times \mathbf{B} = \frac{1}{\mu_0}(\nabla \times \mathbf{B}) \times \mathbf{B} = -\nabla \left( \frac{B^2}{2\mu_0} \right) + \frac{1}{\mu_0}(\mathbf{B} \cdot \nabla)\mathbf{B}
$$
第一项 $-\nabla \left( \frac{B^2}{2\mu_0} \right)$ 是**[磁压](@entry_id:272413)力**（**magnetic pressure**）[梯度力](@entry_id:166847)。其中 $P_m = \frac{B^2}{2\mu_0}$ 被定义为[磁压](@entry_id:272413)力。这个力与[热压力](@entry_id:202761)类似，总是从[磁场](@entry_id:153296)强的区域指向[磁场](@entry_id:153296)弱的区域，试图将等离子体从强[磁场](@entry_id:153296)区排挤出去。

第二项 $\frac{1}{\mu_0}(\mathbf{B} \cdot \nabla)\mathbf{B}$ 被称为**[磁张力](@entry_id:192593)**（**magnetic tension**）力。这个力类似于张紧的橡皮筋，只有当磁力线发生弯曲时才会出现，其作用是试图拉直弯曲的磁力线。$(\mathbf{B} \cdot \nabla)$ 算[子表示](@entry_id:141094)沿着磁力线方向的[方向导数](@entry_id:189133)。

因此，动量方程可以重写为：
$$
\rho \frac{d\mathbf{v}}{dt} = -\nabla \left( p + \frac{B^2}{2\mu_0} \right) + \frac{1}{\mu_0}(\mathbf{B} \cdot \nabla)\mathbf{B}
$$
这清晰地表明，等离子体的运动受到[总压](@entry_id:265293)力（热压力+[磁压](@entry_id:272413)力）梯度和[磁张力](@entry_id:192593)的共同驱动。在一个纯[环向磁场](@entry_id:756057)构型中，[磁压](@entry_id:272413)力和[磁张力](@entry_id:192593)可以同时存在，并且它们之间的相互作用决定了等离子体的平衡状态 [@problem_id:343688]。

#### [感应方程](@entry_id:750617)与[磁冻结定理](@entry_id:746348)

理想MHD的核心概念之一是**磁冻结效应**（**frozen-in flux**），即磁力线如同被“冻结”在理想导电的[等离子体流体](@entry_id:187430)中，随流体一起运动。这一概念的数学表述是**[感应方程](@entry_id:750617)**。

为了推导[感应方程](@entry_id:750617)，我们首先需要建立[电场](@entry_id:194326) $\mathbf{E}$、[磁场](@entry_id:153296) $\mathbf{B}$ 和[流体速度](@entry_id:267320) $\mathbf{v}$ 之间的关系，这被称为**[广义欧姆定律](@entry_id:180191)**。通过考察电子的[动量方程](@entry_id:197225)，我们可以得到这个关系。在最简化的理想情况下，我们做两个核心假设：
1.  **电子惯性可以忽略** ($m_e \to 0$)。这意味着电子可以瞬时响应电磁力的变化。
2.  **电子[压力梯度](@entry_id:274112)等非理想项可以忽略**。

在这些假设下，电子[动量方程](@entry_id:197225)简化为[电场](@entry_id:194326)力和[洛伦兹力](@entry_id:145104)的平衡，从而得到**[理想欧姆定律](@entry_id:185600)**（**Ideal Ohm's Law**）：
$$
\mathbf{E} + \mathbf{v} \times \mathbf{B} = 0
$$
这个定律的物理解释是：在随等离子体一起运动的[参考系](@entry_id:169232)中，[电场](@entry_id:194326)为零。这是因为在[理想导体](@entry_id:273420)中，任何微小的[电场](@entry_id:194326)都会驱动无穷大的电流，从而立即将[电荷](@entry_id:275494)重新[分布](@entry_id:182848)以完全屏蔽该[电场](@entry_id:194326)。

将[理想欧姆定律](@entry_id:185600)代入法拉第[电磁感应](@entry_id:181154)定律 $\frac{\partial \mathbf{B}}{\partial t} = -\nabla \times \mathbf{E}$，我们便可以消去[电场](@entry_id:194326) $\mathbf{E}$，得到只包含[磁场](@entry_id:153296)和速度的**[感应方程](@entry_id:750617)**（**Induction Equation**）：
$$
\frac{\partial \mathbf{B}}{\partial t} = \nabla \times (\mathbf{v} \times \mathbf{B})
$$
这个方程精确地描述了[磁场](@entry_id:153296)随[流体运动](@entry_id:182721)的[演化过程](@entry_id:175749) [@problem_id:343775]。[磁冻结定理](@entry_id:746348)是该方程的直接物理解释：穿过任何随流体运动的闭合回路的磁通量是守恒的。

为了更深入地理解磁冻结效应，我们可以考察矢量 $\mathbf{C} = \mathbf{B}/\rho$ 的演化。可以证明，在理想MHD中，$\mathbf{C}$ 的随动导数满足：
$$
\frac{d\mathbf{C}}{dt} = (\mathbf{C} \cdot \nabla)\mathbf{v}
$$
这与连接两个相邻流[体元](@entry_id:267802)的无穷小线元 $\delta\mathbf{l}$ 的[演化方程](@entry_id:268137) $\frac{d(\delta\mathbf{l})}{dt} = (\delta\mathbf{l} \cdot \nabla)\mathbf{v}$ 完全相同。这表明，[磁场](@entry_id:153296)矢量 $\mathbf{B}$ 像线元一样被流场拉伸、压缩和扭曲，只是同时其大小还受到密度 $\rho$ 变化的调节。例如，在一个稳定的[剪切流](@entry_id:266817)场 $\mathbf{v} = (Ay, 0, 0)$ 中，一个初始时刻竖直方向的均匀[磁场](@entry_id:153296) $\mathbf{B}(0) = B_0 \hat{\mathbf{y}}$ 会被流场逐渐拉伸，产生一个随时间[线性增长](@entry_id:157553)的水平分量 $B_x(t) = B_0 A t$。这种磁力线的拉伸过程会导致[磁能密度](@entry_id:193006) $U_B = |\mathbf{B}|^2 / (2\mu_0)$ 随时间二次增长，这是将流动动能转化为[磁能](@entry_id:268850)的一个典型例子 [@problem_id:343786]。

#### 状态方程

为了使[方程组](@entry_id:193238)封闭，我们还需要一个联系热压力 $p$ 和密度 $\rho$ 的状态方程。在理想MHD中，我们假设等离子体的[热力学过程](@entry_id:141636)是绝热的，即没有热传导、辐射或外部加热等非[绝热过程](@entry_id:138150)。这由**绝热定律**描述：
$$
\frac{d}{dt} \left( \frac{p}{\rho^\gamma} \right) = 0
$$
其中 $\gamma$ 是绝热指数（对于[单原子气体](@entry_id:140562)，$\gamma = 5/3$）。这意味着对于一个特定的流[体元](@entry_id:267802)，$p/\rho^\gamma$ 这个量在其运动轨迹上保持不变。

这个方程可以从更普适的内能[守恒定律](@entry_id:269268)推导而来。计及外部加热 $H$ 和冷却 $L$（单位体积的功率），内能密度 $\mathcal{E}_{int} = p/(\gamma-1)$ 的[演化方程](@entry_id:268137)为：
$$
\frac{\partial \mathcal{E}_{int}}{\partial t} + \nabla \cdot (\mathcal{E}_{int} \mathbf{v}) = - p (\nabla \cdot \mathbf{v}) + H - L
$$
结合[连续性方程](@entry_id:195013)，可以证明这等价于 $\frac{d}{dt}(p\rho^{-\gamma}) = (\gamma-1)\rho^{1-\gamma}(H-L)$。只有在没有非[绝热过程](@entry_id:138150)（$H=0, L=0$）的理想情况下，我们才得到上述的绝热定律 [@problem_id:343812]。

综上所述，理想MHD[方程组](@entry_id:193238)包括：
1.  **[连续性方程](@entry_id:195013)**: $\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) = 0$
2.  **[动量方程](@entry_id:197225)**: $\rho \frac{d\mathbf{v}}{dt} = -\nabla p + \frac{1}{\mu_0}(\nabla \times \mathbf{B}) \times \mathbf{B}$
3.  **[感应方程](@entry_id:750617)**: $\frac{\partial \mathbf{B}}{\partial t} = \nabla \times (\mathbf{v} \times \mathbf{B})$
4.  **绝热定律**: $\frac{d}{dt} (p \rho^{-\gamma}) = 0$
5.  **无磁单极约束**: $\nabla \cdot \mathbf{B} = 0$

这是一个包含8个标量方程（连续性方程1个，[动量方程](@entry_id:197225)3个，[感应方程](@entry_id:750617)3个，绝热定律1个）的封闭系统，用于求解8个未知标量函数（$\rho$, $p$, $\mathbf{v}$的3个分量, $\mathbf{B}$的3个分量）。无磁单极条件 $\nabla \cdot \mathbf{B} = 0$ 作为一个[初始条件](@entry_id:152863)，如果初始时刻满足，[感应方程](@entry_id:750617)会保证它在后续所有时间都满足。

### 主要性质与推论

理想MHD[方程组](@entry_id:193238)描述了丰富的物理现象，包括各种波动模式和守恒律。

#### MHD波：阿尔芬波

理想MHD[方程组](@entry_id:193238)的线性化分析表明，均匀[磁化等离子体](@entry_id:201225)中存在三种基本的波动模式：**[剪切阿尔芬波](@entry_id:754753)**（**Shear Alfvén wave**）、**[快磁声波](@entry_id:749231)**和**[慢磁声波](@entry_id:754961)**。

[剪切阿尔芬波](@entry_id:754753)是一种特别的模式，其物理性质非常独特。它是一种纯粹的横波，其等离子体流速扰动 $\mathbf{v}_1$ 和[磁场](@entry_id:153296)扰动 $\mathbf{B}_1$ 都严格垂直于背景[磁场](@entry_id:153296) $\mathbf{B}_0$ 和[波矢](@entry_id:178620) $\mathbf{k}$ 构成的平面。一个重要的推论是，[剪切阿尔芬波](@entry_id:754753)是**不可压缩**的。这意味着波的传播不会引起[等离子体密度](@entry_id:202836)的变化（$\rho_1 = 0$）。这可以通过分析线性化的[连续性方程](@entry_id:195013) $\frac{\partial \rho_1}{\partial t} + \rho_0 \nabla \cdot \mathbf{v}_1 = 0$ 直接得出。由于速度扰动是横向的，$\mathbf{k} \cdot \mathbf{v}_1 = 0$，进而导致 $\rho_1=0$ 和 $p_1=0$ [@problem_id:343625]。

[剪切阿尔芬波](@entry_id:754753)的另一个显著特性是**能量均分**。对于一个沿背景[磁场](@entry_id:153296)传播的[剪切阿尔芬波](@entry_id:754753)，其扰动动能密度 $\delta K = \frac{1}{2}\rho_0 |\delta \mathbf{v}|^2$ 和扰动[磁能密度](@entry_id:193006) $\delta U_B = \frac{|\delta \mathbf{B}|^2}{2\mu_0}$ 在时间平均意义下是相等的。即，在一个波周期内，能量在[流体运动](@entry_id:182721)和[磁场](@entry_id:153296)扰动之间来回传递，但两者的[时间平均](@entry_id:267915)值严格相等：$\langle \delta K \rangle = \langle \delta U_B \rangle$ [@problem_id:343694]。这种能量均分是阿尔芬波的基本属性，也是其在[能量输运](@entry_id:183081)和耗散研究中备受关注的原因。

#### 守恒律：[磁螺度](@entry_id:751625)

除了能量、动量和质量等基本[守恒量](@entry_id:150267)外，理想MHD系统还拥有一个重要的拓扑守恒量——**[磁螺度](@entry_id:751625)**（**magnetic helicity**）。[磁螺度](@entry_id:751625)定义为[磁矢势](@entry_id:141246) $\mathbf{A}$ 与[磁场](@entry_id:153296) $\mathbf{B}$ 在整个体积内的积分：
$$
H = \int_V \mathbf{A} \cdot \mathbf{B} \, dV
$$
[磁螺度](@entry_id:751625)衡量了磁力线的缠绕、扭曲和链接程度。例如，两条相互链接的磁通量管具有非零的[磁螺度](@entry_id:751625)。

可以证明，对于一个被[理想导体](@entry_id:273420)边界所包围的等离子体（即边界上[磁场](@entry_id:153296)的法向分量 $\mathbf{B} \cdot \hat{\mathbf{n}} = 0$ 和速度的法向分量 $\mathbf{v} \cdot \hat{\mathbf{n}} = 0$），其总体积内的[磁螺度](@entry_id:751625)是严格守恒的，即 $dH/dt = 0$ [@problem_id:343877]。这意味着在理想MHD[演化过程](@entry_id:175749)中，[磁场](@entry_id:153296)的拓扑结构无法改变。磁力线可以被拉伸和扭曲，但不能被切断和重联。[磁螺度](@entry_id:751625)守恒是理想MHD的一个深刻结果，它对[太阳耀斑](@entry_id:204045)、[日冕物质抛射](@entry_id:200049)以及实验室等离子体中的弛豫现象等过程具有重要的约束作用。

### 理想MHD的适用范围

理想MHD模型的美妙之处在于其简洁性，但这建立在一系列近似之上。理解这些近似的物理含义及其失效的条件，对于正确应用MHD理论至关重要。

#### 有限电阻率与[磁雷诺数](@entry_id:270538)

理想MHD的核心假设是等离子体为[理想导体](@entry_id:273420)（[电阻率](@entry_id:266481)为零）。在真实等离子体中，[电阻率](@entry_id:266481) $\eta$ 是有限的，这会在欧姆定律中引入一个耗散项 $\eta \mathbf{J}$，并最终在[感应方程](@entry_id:750617)中引入一个[扩散](@entry_id:141445)项：
$$
\frac{\partial \mathbf{B}}{\partial t} = \nabla \times (\mathbf{v} \times \mathbf{B}) - \nabla \times (\eta \nabla \times \mathbf{B})
$$
第一项是理想MHD中的[对流](@entry_id:141806)项，代表[磁场](@entry_id:153296)被流体“冻结”输运；第二项是电阻[扩散](@entry_id:141445)项，代表磁力线在等离子体中“滑移”和耗散。

这两个效应的相对重要性可以通过[无量纲化](@entry_id:136704)来衡量。对于一个特征尺度为 $L_0$、[特征速度](@entry_id:165394)为 $V_0$ 的系统，[对流](@entry_id:141806)项的量级为 $V_0 B_0 / L_0$，而[扩散](@entry_id:141445)项的量级为 $\eta B_0 / L_0^2$。两者之比定义了一个关键的无量纲参数——**[磁雷诺数](@entry_id:270538)**（**Magnetic Reynolds Number**）：
$$
R_m = \frac{\text{对流项}}{\text{扩散项}} \sim \frac{V_0 L_0}{\eta}
$$
理想MHD近似成立的条件是 $R_m \gg 1$。这意味着在所考察的尺度和速度下，[磁场](@entry_id:153296)的[对流输运](@entry_id:149512)远远快于其电阻[扩散](@entry_id:141445)，因此磁冻结是一个非常好的近似。反之，如果 $R_m \lesssim 1$，则电阻效应变得重要，必须使用电阻MHD模型。[磁场](@entry_id:153296)重联等拓扑改变的过程正是在电阻效应不可忽略的小尺度区域发生的 [@problem_id:343783]。

#### 位移电流的忽略

MHD理论通常采用安培定律的准静态形式 $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}$，而忽略了完整的[安培-麦克斯韦定律](@entry_id:266368)中的[位移电流](@entry_id:190231)项 $\mu_0 \epsilon_0 \frac{\partial \mathbf{E}}{\partial t}$。这一近似的合理性在于MHD所研究的现象其特征速度远小于光速 $c$。

我们可以通过分析阿尔芬波来定量地验证这一点。对于一个[阿尔芬波](@entry_id:261195)，位移电流的幅值 $| \mathbf{J}_D | = |\epsilon_0 \frac{\partial \mathbf{E}_1}{\partial t}|$ 与传导电流的幅值 $|\mathbf{J}_1|$ 之比可以被计算出来。结果表明，这个比值恰好是[阿尔芬速度](@entry_id:274944) $v_A$ 与光速 $c$ 平方之比：
$$
\frac{|\mathbf{J}_D|}{|\mathbf{J}_1|} = \frac{v_A^2}{c^2}
$$
[@problem_id:343661]。由于在绝大多数天体物理和实验室等离子体中，[阿尔芬速度](@entry_id:274944)远小于光速（例如，太阳日冕中 $v_A \sim 1000 \text{ km/s}$，而 $c \sim 3 \times 10^5 \text{ km/s}$），因此 $v_A^2/c^2$ 是一个极小的数。这雄辩地证明了在非[相对论性等离子体](@entry_id:159751)的低频动力学中，忽略[位移电流](@entry_id:190231)是一个高度精确的近似。

#### 双流体效应：霍尔项

理想MHD将等离子体视为单流体，假设电子和离子紧密耦合，共同运动。当系统尺度非常小，或者[电流密度](@entry_id:190690)非常大时，电子和离子的运动会发生分离，双流体效应变得显著。[广义欧姆定律](@entry_id:180191)中描述这一效应的最主要项是**霍尔项**（**Hall term**）：$\frac{1}{ne}(\mathbf{J} \times \mathbf{B})$。

霍尔项的物理起源在于，电流 $\mathbf{J} = ne(\mathbf{v}_i - \mathbf{v}_e)$ 本身就代表了离子和电子的相对运动。在理想MHD中，我们假设这个[相对运动](@entry_id:169798)可以忽略，但在某些情况下它很重要。霍尔项的引入意味着[磁场](@entry_id:153296)不再冻结于等离子体[质心速度](@entry_id:175479) $\mathbf{v}$，而是冻结于电子流体速度 $\mathbf{v}_e$。

霍尔效应的重要性同样可以通过尺度分析来评估。将[感应方程](@entry_id:750617)中的理想项 $|\nabla \times (\mathbf{v} \times \mathbf{B})| \sim VB/L$ 与霍尔项 $|\nabla \times (\frac{1}{ne} \mathbf{J} \times \mathbf{B})| \sim B^2/(\mu_0 ne L^2)$ 进行比较。两者的比值 $R$ 可以表示为：
$$
R = \frac{d_i}{M_A L}
$$
其中 $d_i = \sqrt{m_i/(\mu_0 n e^2)}$ 是**离子[趋肤深度](@entry_id:270307)**（**ion skin depth**），代表了由于离子惯性而使其运动与[磁场](@entry_id:153296)解耦的特征尺度；$M_A = V/v_A$ 是**阿尔芬[马赫数](@entry_id:274014)**。

霍尔效应可以被忽略的条件是 $R \ll 1$，即 $L/d_i \gg 1/M_A$。这表明，只有当系统的特征尺度 $L$ 远大于离子[趋肤深度](@entry_id:270307) $d_i$（并由 $M_A$ 修正）时，单流体的理想MHD模型才是有效的。当系统尺度接近或小于离子[趋肤深度](@entry_id:270307)时，双流体效应变得不可避免，必须采用霍尔MHD或更完备的[双流体模型](@entry_id:139846)来描述 [@problem_id:343881]。