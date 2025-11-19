## 引言
[柯西运动方程](@entry_id:204126)是牛顿第二定律在可变形连续介质世界中的宏伟体现，是现代[流体力学](@entry_id:136788)、[固体力学](@entry_id:164042)乃至更广阔物理科学领域的基石。它以一个优雅的[微分方程](@entry_id:264184)，捕捉了物质运动变化的本质——惯性、[内力与外力](@entry_id:170589)的平衡。这个方程的深刻意义在于，它为描述从空气、水等简单流体到聚合物、土壤、甚至星系气体等复杂系统的动力学行为，提供了一个统一的数学框架。本文旨在系统性地剖析这一核心理论，弥合抽象原理与实际应用之间的鸿沟。

为实现这一目标，我们将分三个章节展开探讨。在第一章“原理与机制”中，我们将追溯[柯西运动方程](@entry_id:204126)的推导过程，阐明应力张量、物质导数等核心概念，并探索其多种重要等价形式以及与[能量守恒](@entry_id:140514)的内在联系。接着，在第二章“应用与跨学科联系”中，我们将跨越学科界限，展示该方程如何被应用于解释声波与重力[波的传播](@entry_id:144063)、涡旋的产生、地球物理流动、材料的[弹塑性](@entry_id:193198)与损伤行为，乃至宇宙大尺度结构的形成。最后，在第三章“动手实践”中，您将有机会通过解决具体问题，将理论知识转化为解决实际力学问题的能力。通过这一结构化的学习路径，读者将对[柯西运动方程](@entry_id:204126)的理论深度和应用广度建立起全面而深刻的理解。

## 原理与机制

本章旨在深入探讨连续介质运动的根本动力学定律——[柯西运动方程](@entry_id:204126)。我们将从基本物理原理出发，系统地推导出该方程，并探讨其多种等价形式，每一种形式都揭示了流体或固体运动的不同侧面。此外，我们还将考察该方程在不同参照系下的变换特性，并阐明其与[能量守恒](@entry_id:140514)定律的深刻联系。

### 局部[动量平衡](@entry_id:193575)：[柯西运动方程](@entry_id:204126)

物质运动的改变是由作用在其上的力引起的，这是[牛顿第二定律](@entry_id:274217)的核心思想。对于一个连续体，这一定律可以表述为：一个物质体积的总动量对时间的变化率，等于作用在该体积上的所有力的总和。这些力分为两类：作用于整个体积的**[体力](@entry_id:174230)**（如重力）和作用于其表面的**面力**（或称[接触力](@entry_id:165079)）。

#### 从全局平衡到局部定律

考虑一个占据空间区域 $\Omega$、边界为 $\partial\Omega$ 的任意物质体积。其[动量平衡](@entry_id:193575)的积分形式可以写作：
$$
\frac{d}{dt} \int_{\Omega} \rho \mathbf{u} \, dV = \oint_{\partial\Omega} \mathbf{t} \, dS + \int_{\Omega} \rho \mathbf{b} \, dV
$$
其中，$\rho$ 是密度，$\mathbf{u}$ 是[速度场](@entry_id:271461)，$\mathbf{b}$ 是单位质量的[体力](@entry_id:174230)，而 $\mathbf{t}$ 是**牵[引力](@entry_id:175476)矢量**，代表了在边界 $\partial\Omega$ 上，外部物质对内部物质施加的单位面积上的[接触力](@entry_id:165079)。

要从这个适用于有限体积的“全局”定律得到一个适用于空间中每一点的“局部”[微分方程](@entry_id:264184)，我们必须将所有项都表示为对同一体积 $\Omega$ 的积分。这一过程的核心挑战在于如何处理表[面积分](@entry_id:275394)项 $\oint_{\partial\Omega} \mathbf{t} \, dS$。

#### 连续介质假设与牵[引力](@entry_id:175476)矢量

为了在数学上处理[接触力](@entry_id:165079)，我们首先需要引入**连续介质假设**。该假设认为，物质是无限可分的，并完全填充其所占据的空间区域，从而允许我们将物理量（如密度、速度）定义为位置和时间的连续场。从物理上看，这一假设的合理性建立在宏观尺度 $L$ 远大于微观结构特征尺度 $\ell_{\text{mic}}$（例如分子间距）的基础上 ($L \gg \ell_{\text{mic}}$)。[@problem_id:2922818]

在此假设下，牵[引力](@entry_id:175476)矢量 $\mathbf{t}$ 可以在一个点 $\mathbf{x}$ 处，通过一个以该点为中心、具有确定法向 $\mathbf{n}$ 的无限小[面积元](@entry_id:263205) $\Delta S$ 上的力 $\Delta \mathbf{F}$ 取极限来明确定义：$\mathbf{t}(\mathbf{x}, \mathbf{n}) = \lim_{\Delta S \to 0} \frac{\Delta \mathbf{F}}{\Delta S}$。**柯西的局部作用公设**（Cauchy's Postulate of Local Action）进一步断言，牵[引力](@entry_id:175476)矢量 $\mathbf{t}$ 仅依赖于作用点 $\mathbf{x}$ 和该点处表面的法向 $\mathbf{n}$，而与该表面局部区域的曲率或形状无关。这个公设是经典连续介质理论的基石。[@problem_id:2619656]

这一经典观点与更先进的理论形成了对比。例如，在**[非局部理论](@entry_id:752667)**（如Eringen的[非局部弹性](@entry_id:193991)理论或[近场动力学](@entry_id:191791)）中，一点的受力取决于其周围一个有限邻域内所有点的状态，从而摒弃了纯粹的表面接触力概念。在**高阶梯[度理论](@entry_id:636058)**（如[应变梯度理论](@entry_id:180517)或[Cosserat理论](@entry_id:186875)）中，[接触力](@entry_id:165079)可能还依赖于表面的曲率，这引入了[内禀长度尺度](@entry_id:750789)，用以描述微观结构的影响。[@problem_id:2619656]

#### 柯西应力张量

柯西的下一个关键贡献是证明了牵[引力](@entry_id:175476)矢量 $\mathbf{t}$ 与法向矢量 $\mathbf{n}$ 之间存在[线性关系](@entry_id:267880)。这个结论，即**柯西应力定理**，可以通过对一个无限小的四面体应用[动量平衡](@entry_id:193575)定律来证明。[@problem_id:2621555] 考虑一个顶点在 $\mathbf{x}_0$ 的四面体，其三个面与坐标平面平行，第四个斜面的法向为 $\mathbf{n}$。当四面体的特征尺寸 $h$ 趋于零时，体积力（如重力）和惯性力的贡献（与 $h^3$ 成正比）将远小于[表面力](@entry_id:188034)的贡献（与 $h^2$ 成正比），因此可以忽略。

最终的力平衡关系揭示了，在 $\mathbf{x}_0$ 点，作用于任意法向为 $\mathbf{n}$ 的平面上的牵[引力](@entry_id:175476) $\mathbf{t}(\mathbf{x}_0, \mathbf{n})$ 可以通过一个[二阶张量](@entry_id:199780)——**柯西应力张量** $\boldsymbol{\sigma}(\mathbf{x}_0)$——与 $\mathbf{n}$ 的[线性映射](@entry_id:185132)来表示：
$$
\mathbf{t}(\mathbf{x}_0, \mathbf{n}) = \boldsymbol{\sigma}(\mathbf{x}_0) \mathbf{n}
$$
这个定理的成立依赖于应[力场](@entry_id:147325)在 $\mathbf{x}_0$ 点的**连续性**。如果应[力场](@entry_id:147325)在该点无界（例如，在理论上的集中力作用点），则此推导失效。值得注意的是，推导仅要求应[力场](@entry_id:147325)是连续的，而不需要更强的[可微性](@entry_id:140863)条件。[@problem_id:2621555] 同样，如果体力场包含奇异性，如一个集中力（用狄拉克 $\delta$ 函数表示），则体积力在极限过程中将不可忽略，四面体法的论证也会失败。[@problem_id:2621555]

#### [柯西运动方程](@entry_id:204126)的推导

有了[应力张量](@entry_id:148973)的概念，[动量平衡](@entry_id:193575)方程中的表[面积分](@entry_id:275394)项可以重写为 $\oint_{\partial\Omega} \boldsymbol{\sigma} \mathbf{n} \, dS$。此时，我们可以应用**[高斯散度定理](@entry_id:188065)**，将其转化为一个[体积分](@entry_id:171119)：
$$
\oint_{\partial\Omega} \boldsymbol{\sigma} \mathbf{n} \, dS = \int_{\Omega} (\nabla \cdot \boldsymbol{\sigma}) \, dV
$$
这里，$\nabla \cdot \boldsymbol{\sigma}$ 是应力[张量的散度](@entry_id:191736)。经典[散度定理](@entry_id:143110)的应用要求应[力场](@entry_id:147325) $\boldsymbol{\sigma}$ 是一次连续可微的（$C^1$），且边界 $\partial\Omega$ 是分片光滑的。在更现代、更严谨的数学框架中，这些条件可以放宽：只要 $\boldsymbol{\sigma}$ 属于特定的索博列夫空间（即 $\boldsymbol{\sigma} \in H(\text{div};\Omega)$），并且边界是[利普希茨连续的](@entry_id:267396)，[散度定理](@entry_id:143110)在弱形式下仍然成立。这恰恰反映了连续介质场作为微观量在[代表性体积元](@entry_id:164290)上平均的物理本质。[@problem_id:2922818]

同时，[动量平衡](@entry_id:193575)方程的左侧，即[总动量](@entry_id:173071)的时间变化率，可以使用**[雷诺输运定理](@entry_id:191217)**转化为：
$$
\frac{d}{dt} \int_{\Omega} \rho \mathbf{u} \, dV = \int_{\Omega} \rho \frac{D\mathbf{u}}{Dt} \, dV
$$
其中 $\frac{D}{Dt} = \frac{\partial}{\partial t} + \mathbf{u} \cdot \nabla$ 是**[物质导数](@entry_id:172646)**，表示跟随一个物质点（流体[质点](@entry_id:186768)）测量的速度变化率。

将所有项都表示为在任意物质体积 $\Omega$ 上的积分后，我们得到：
$$
\int_{\Omega} \rho \frac{D\mathbf{u}}{Dt} \, dV = \int_{\Omega} (\nabla \cdot \boldsymbol{\sigma}) \, dV + \int_{\Omega} \rho \mathbf{b} \, dV
$$
由于这个等式对任意选择的体积 $\Omega$ 都必须成立，且假设被积函数是连续的，那么被积函数本身必须相等。这就得到了[动量平衡](@entry_id:193575)的局部形式，即**柯西第一运动定律**或**[柯西运动方程](@entry_id:204126)**：
$$
\rho \frac{D\mathbf{u}}{Dt} = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b}
$$
这个方程是连续介质力学的基石。它表明，单位体积内物质的[惯性力](@entry_id:169104)（左侧）由内部应力产生的力（$\nabla \cdot \boldsymbol{\sigma}$）和作用于其上的[体力](@entry_id:174230)（$\rho \mathbf{b}$）所平衡。

### [角动量平衡](@entry_id:181848)与应力[张量的对称性](@entry_id:202126)

除了动量守恒，[角动量守恒](@entry_id:156798)也是一条基本物理定律。对于连续介质，在没有外部[体力](@entry_id:174230)矩或面力矩作用的经典（非极性）情况下，[角动量平衡](@entry_id:181848)定律对柯西[应力张量](@entry_id:148973)施加了一个非常重要的约束。[@problem_id:2904980]

从[角动量平衡](@entry_id:181848)的积分形式出发，经过与推导[柯西方程](@entry_id:164868)类似但更为复杂的步骤，可以证明该定律的局部形式最终归结为一个极其简洁的代数关系：
$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}^T
$$
这意味着柯西[应力张量](@entry_id:148973)是一个**对称张量**。例如，$\sigma_{xy}$，即作用在 $x$ 法向平面上沿 $y$ 方向的剪应力，必须等于 $\sigma_{yx}$，即作用在 $y$ 法向平面上沿 $x$ 方向的剪应力。

这一对称性并非一个本构假设（即与[材料性质](@entry_id:146723)相关的假设），而是[角动量守恒](@entry_id:156798)在经典连续介质框架下的直接推论。它极大地简化了[应力分析](@entry_id:168804)，将一个二阶张量中独立的未知分量从9个减少到6个。需要强调的是，在考虑具有内部微观结构的材料（如[Cosserat介质](@entry_id:747932)）时，可能会存在所谓的“[力偶应力](@entry_id:747952)”，此时[角动量平衡](@entry_id:181848)将导致一个非对称的应力张量。[@problem_id:2619656] [@problem_id:2621555]

### 动量方程的等价形式

[柯西运动方程](@entry_id:204126)可以通过各种数学变换，改写成不同的等价形式。这些形式在特定应用中非常有用，因为它们能够凸显出流场中不同的物理机制。

#### [守恒形式](@entry_id:747710)

物理学中的许多基本定律都可以表示为守恒律的形式：$\frac{\partial \mathcal{Q}}{\partial t} + \nabla \cdot \mathbf{J}_{\mathcal{Q}} = S_{\mathcal{Q}}$，其中 $\mathcal{Q}$ 是某个守恒量的密度，$\mathbf{J}_{\mathcal{Q}}$ 是其通量，而 $S_{\mathcal{Q}}$ 是源/汇项。

通过结合连续性方程 $\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) = 0$，[柯西运动方程](@entry_id:204126)可以被严格地改写为[动量守恒](@entry_id:149964)形式。[@problem_id:460854] 首先展开物质导数：
$$
\rho \left( \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla)\mathbf{u} \right) = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b}
$$
利用连续性方程和向量恒等式，上式可以整理为：
$$
\frac{\partial (\rho \mathbf{u})}{\partial t} + \nabla \cdot (\rho \mathbf{u} \otimes \mathbf{u} - \boldsymbol{\sigma}) = \rho \mathbf{b}
$$
这里，$\mathbf{u} \otimes \mathbf{u}$ 是[速度矢量](@entry_id:269648)的并矢（在[笛卡尔坐标](@entry_id:167698)下，其分量为 $u_i u_j$）。这个方程清晰地展示了[动量守恒](@entry_id:149964)的结构：
-   **动量密度**: $\rho \mathbf{u}$，即单位体积的动量。
-   **总动量通量张量**: $\boldsymbol{\Pi} = \rho \mathbf{u} \otimes \mathbf{u} - \boldsymbol{\sigma}$。这个张量描述了动量如何通过空间进行输运。它包含两个部分：
    -   $\rho \mathbf{u} \otimes \mathbf{u}$：**[对流输运](@entry_id:149512)项**，表示由于流体自身流动而携带的动量。
    -   $-\boldsymbol{\sigma}$：**应力输运项**，表示由于分子间的相互作用（压力和[粘性力](@entry_id:263294)）而传递的动量。
-   **动量源**: $\rho \mathbf{b}$，即体力引起的动量产生。

[守恒形式](@entry_id:747710)在计算流体动力学中尤为重要，因为基于此形式的[数值格式](@entry_id:752822)能更好地保证物理量的守恒性。

#### 兰姆-格罗梅卡形式与涡量

对于[无粘流](@entry_id:273124)体（$\boldsymbol{\sigma} = -p\mathbf{I}$，其中 $p$ 是压力），[柯西方程](@entry_id:164868)简化为**[欧拉方程](@entry_id:177914)**。通过引入一个重要的向量恒等式，可以将欧拉方程中的[对流加速度](@entry_id:263153)项 $(\mathbf{u} \cdot \nabla)\mathbf{u}$ 与流体的旋转特性联系起来。该恒等式为：
$$
(\mathbf{u} \cdot \nabla)\mathbf{u} = \nabla\left(\frac{1}{2}|\mathbf{u}|^2\right) - \mathbf{u} \times (\nabla \times \mathbf{u})
$$
其中，$\boldsymbol{\omega} = \nabla \times \mathbf{u}$ 是**[涡量矢量](@entry_id:187667)**，它描述了流体微团的局部旋转角速度的两倍。

将此恒等式代入[欧拉方程](@entry_id:177914)，并假设[体力](@entry_id:174230)是保守的（$\mathbf{b} = -\nabla\Phi$）且流体是正压的（即压力仅是密度的函数，这允许定义一个比焓 $h$ 使得 $\nabla h = \frac{1}{\rho}\nabla p$），我们可以得到**兰姆-格罗梅卡方程**（Lamb-Gromeka form）[@problem_id:460798]：
$$
\frac{\partial \mathbf{u}}{\partial t} + \nabla H = \mathbf{u} \times \boldsymbol{\omega}
$$
其中，$H = \frac{1}{2}|\mathbf{u}|^2 + h + \Phi$ 是**[总焓](@entry_id:197863)**或**伯努利函数**。该方程形式优美地揭示了流体加速度、能量梯度和涡量之间的关系。右侧的 $\mathbf{u} \times \boldsymbol{\omega}$ 项通常被称为[兰姆矢量](@entry_id:183436)。

#### 克罗科-瓦松尼形式与[热力学](@entry_id:141121)

在[定常流](@entry_id:191654)动（$\frac{\partial}{\partial t} = 0$）的情况下，兰姆-格罗梅卡方程进一步简化。此时，我们可以利用[热力学](@entry_id:141121)关系，将流动的动力学特性与[热力学状态](@entry_id:755916)直接联系起来。吉布斯关系给出了比焓 $h$、温度 $T$、比熵 $s$ 和压力 $p$ 之间的[微分](@entry_id:158718)关系：$dh = T ds + \frac{dp}{\rho}$。其梯度形式为 $\nabla h = T \nabla s + \frac{1}{\rho}\nabla p$。

将此关系代入定常欧拉方程，可推导出**克罗科-瓦松尼方程**（Crocco-Vazsonyi equation）[@problem_id:460832]：
$$
\mathbf{u} \times \boldsymbol{\omega} = T \nabla s - \nabla h_0
$$
其中 $h_0 = h + \frac{1}{2}|\mathbf{u}|^2$ 是总比焓（对于定常[绝热流](@entry_id:262576)动，若无外功和热交换，此量守恒）。这个方程意义非凡，它直接表明，在定常[无粘流](@entry_id:273124)动中，[涡量](@entry_id:142747)（通过[兰姆矢量](@entry_id:183436) $\mathbf{u} \times \boldsymbol{\omega}$ 体现）的存在与熵的梯度紧密相连。对于一个熵处处均匀的流动（[等熵流](@entry_id:267193)），$\nabla s = 0$，如果[总焓](@entry_id:197863)也均匀，那么必然有 $\mathbf{u} \times \boldsymbol{\omega} = 0$，这意味着速度矢量和[涡量矢量](@entry_id:187667)处处平行，这种流动被称为“螺[旋流](@entry_id:153202)”。该方程的一个有趣推论是，对两边取旋度可得 $\nabla \times (\mathbf{u} \times \boldsymbol{\omega}) = \nabla T \times \nabla s$，直接将流场运动学与[热力学](@entry_id:141121)量的空间分布联系起来。[@problem_id:460832]

### 参照系依赖性与变换

[柯西运动方程](@entry_id:204126)的形式取决于观察者所在的参照系。

#### 非惯性参照系

在[惯性系](@entry_id:266190)中表述的[柯西方程](@entry_id:164868)，可以通过坐标变换转换到[非惯性系](@entry_id:168746)（例如，一个相对于[惯性系](@entry_id:266190)在做旋转和平动的参照系，如地球）中。变换的结果是，在方程的右侧会额外出现一些“虚拟”的体力项，这些项被称为**惯性力**或**视在力**。[@problem_id:460816]

在以角速度 $\mathbf{\Omega}'$ 旋转的[非惯性系](@entry_id:168746)中，完整的[柯西方程](@entry_id:164868)（以[非惯性系](@entry_id:168746)中的量表示）写作：
$$
\rho \frac{D\mathbf{u}'}{Dt} = \nabla' \cdot \boldsymbol{\sigma}' + \rho \mathbf{g}' - \rho \mathbf{a}'_0 - 2\rho(\mathbf{\Omega}' \times \mathbf{u}') - \rho[\mathbf{\Omega}' \times (\mathbf{\Omega}' \times \mathbf{x}')] - \rho(\dot{\mathbf{\Omega}}' \times \mathbf{x}')
$$
新增的视在力项分别为：
-   **平动[惯性力](@entry_id:169104)**: $-\rho \mathbf{a}'_0$，与参照系原点的[平动](@entry_id:187700)加速度有关。
-   **[科里奥利力](@entry_id:160096)**: $-2\rho(\mathbf{\Omega}' \times \mathbf{u}')$，作用于运动的物体。
-   **[离心力](@entry_id:173726)**: $-\rho[\mathbf{\Omega}' \times (\mathbf{\Omega}' \times \mathbf{x}')]$，指向[旋转轴](@entry_id:187094)的外部。
-   **[欧拉力](@entry_id:173795)**: $-\rho(\dot{\mathbf{\Omega}}' \times \mathbf{x}')$，仅在角速度变化时出现。

这些视在力的散度并非总是为零，它们可以影响流体的[可压缩性](@entry_id:144559)效应。例如，可以证明，视在[力场](@entry_id:147325)的总散度为 $\nabla' \cdot \mathbf{f}_{\text{app}} = 2\mathbf{\Omega}' \cdot \boldsymbol{\omega}' + 2|\mathbf{\Omega}'|^2$，其中 $\boldsymbol{\omega}' = \nabla' \times \mathbf{u}'$ 是[非惯性系](@entry_id:168746)中的相对[涡量](@entry_id:142747)。[@problem_id:460816]

#### 任意拉格朗日-欧拉（ALE）参照系

在计算力学中，特别是在处理移动边界或大变形问题时，纯粹的[欧拉描述](@entry_id:264722)（固定网格）或[拉格朗日描述](@entry_id:264498)（网格随物质运动）都有其局限性。**任意拉格朗日-欧拉（ALE）**方法提供了一种混合框架，其计算网格以一个独立指定的网格速度 $\mathbf{w}$ 运动。

在这种框架下，物理量 $f$ 的时间导数关系变为 $\left. \frac{\partial f}{\partial t} \right|_{\mathbf{x}} = \left. \frac{\partial f}{\partial t} \right|_{\boldsymbol{\xi}} - (\mathbf{w} \cdot \nabla) f$，其中 $\boldsymbol{\xi}$ 是ALE参照坐标。将此关系代入[柯西方程](@entry_id:164868)，[物质导数](@entry_id:172646)中的[对流](@entry_id:141806)项变为由物质速度与网格速度的相对速度 $\mathbf{u} - \mathbf{w}$ 驱动。整理后可得，[柯西方程](@entry_id:164868)在ALE框架下的形式为 [@problem_id:460746]：
$$
\rho \left. \frac{\partial \mathbf{u}}{\partial t} \right|_{\boldsymbol{\xi}} + \rho ((\mathbf{u} - \mathbf{w}) \cdot \nabla)\mathbf{u} = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b}
$$
这种形式允许[网格运动](@entry_id:163293)与物质运动[解耦](@entry_id:637294)，从而在模拟[流固耦合](@entry_id:171183)等问题时提供了极大的灵活性。

### 能量平衡与耗散

[动量方程](@entry_id:197225)与[能量守恒](@entry_id:140514)定律密切相关。通过将[柯西运动方程](@entry_id:204126)与速度矢量 $\mathbf{u}$ 做[点积](@entry_id:149019)，可以推[导出单位](@entry_id:141082)质量动能 $k = \frac{1}{2}\mathbf{u} \cdot \mathbf{u}$ 的平衡方程。[@problem_id:460770]

在这一过程中，应力项 $\mathbf{u} \cdot (\nabla \cdot \boldsymbol{\sigma})$ 代表了应力力所做的[功率密度](@entry_id:194407)。利用向量恒等式和应力[张量的对称性](@entry_id:202126)，该项可以分解为：
$$
\mathbf{u} \cdot (\nabla \cdot \boldsymbol{\sigma}) = \nabla \cdot (\boldsymbol{\sigma} \cdot \mathbf{u}) - \boldsymbol{\sigma} : \nabla \mathbf{u}
$$
-   **能量通量**: $\nabla \cdot (\boldsymbol{\sigma} \cdot \mathbf{u})$ 这一项可以被移到方程的另一侧，解释为通过[应力传递](@entry_id:182468)的机械能通量。
-   **应力耗散**: $\mathcal{P}_{diss} = \boldsymbol{\sigma} : \nabla \mathbf{u}$ 这一项则是一个源/汇项。它代表了单位体积内，机械能由于材料变形而不可逆地转化为内能（通常是热能）的速率。对于粘性流体，这一项总是非负的，代表了[粘性耗散](@entry_id:143708)。

我们可以通过一个具体的例子来理解应力耗散。考虑一个[幂律流体](@entry_id:151453)在定常简单[剪切流](@entry_id:266817) $\mathbf{u} = (Ky, 0, 0)$ 中的行为。其[粘性应力](@entry_id:261328)张量为 $\boldsymbol{\tau} = 2 \eta \mathbf{D}$，其中 $\mathbf{D}$ 是[应变率张量](@entry_id:266108)，[表观粘度](@entry_id:260802) $\eta = m (\dot{\gamma}_{eq})^{n-1}$，而等效剪切率 $\dot{\gamma}_{eq} = \sqrt{2 (\mathbf{D}:\mathbf{D})}$。对于此流动，可以计算出 $\dot{\gamma}_{eq} = K$。应力[耗散功率](@entry_id:177328)密度为 $\mathcal{P}_{diss} = \boldsymbol{\tau} : \nabla \mathbf{u}$。经过计算，我们得到一个简洁的结果 [@problem_id:460770]：
$$
\mathcal{P}_{diss} = m K^{n+1}
$$
这个结果清晰地展示了耗散率如何依赖于材料的流变特性（$m$ 和 $n$）以及流动的[运动学](@entry_id:173318)特性（剪切率 $K$）。