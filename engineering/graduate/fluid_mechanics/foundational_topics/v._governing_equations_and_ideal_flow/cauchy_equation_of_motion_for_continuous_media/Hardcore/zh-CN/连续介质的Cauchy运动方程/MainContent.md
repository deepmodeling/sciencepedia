## 引言
柯西运动方程是牛顿第二定律在可变形连续介质世界中的宏伟体现，是现代流体力学、固体力学乃至更广阔物理科学领域的基石。它以一个优雅的微分方程，捕捉了物质运动变化的本质——惯性、内力与外力的平衡。这个方程的深刻意义在于，它为描述从空气、水等简单流体到聚合物、土壤、甚至星系气体等复杂系统的动力学行为，提供了一个统一的数学框架。本文旨在系统性地剖析这一核心理论，弥合抽象原理与实际应用之间的鸿沟。

为实现这一目标，我们将分三个章节展开探讨。在第一章“原理与机制”中，我们将追溯柯西运动方程的推导过程，阐明应力张量、物质导数等核心概念，并探索其多种重要等价形式以及与能量守恒的内在联系。接着，在第二章“应用与跨学科联系”中，我们将跨越学科界限，展示该方程如何被应用于解释声波与重力波的传播、涡旋的产生、地球物理流动、材料的弹塑性与损伤行为，乃至宇宙大尺度结构的形成。最后，在第三章“动手实践”中，您将有机会通过解决具体问题，将理论知识转化为解决实际力学问题的能力。通过这一结构化的学习路径，读者将对柯西运动方程的理论深度和应用广度建立起全面而深刻的理解。

## 原理与机制

本章旨在深入探讨连续介质运动的根本动力学定律——柯西运动方程。我们将从基本物理原理出发，系统地推导出该方程，并探讨其多种等价形式，每一种形式都揭示了流体或固体运动的不同侧面。此外，我们还将考察该方程在不同参照系下的变换特性，并阐明其与能量守恒定律的深刻联系。

### 局部动量平衡：柯西运动方程

物质运动的改变是由作用在其上的力引起的，这是牛顿第二定律的核心思想。对于一个连续体，这一定律可以表述为：一个物质体积的总动量对时间的变化率，等于作用在该体积上的所有力的总和。这些力分为两类：作用于整个体积的**体力**（如重力）和作用于其表面的**面力**（或称接触力）。

#### 从全局平衡到局部定律

考虑一个占据空间区域 $\Omega$、边界为 $\partial\Omega$ 的任意物质体积。其动量平衡的积分形式可以写作：
$$
\frac{d}{dt} \int_{\Omega} \rho \mathbf{u} \, dV = \oint_{\partial\Omega} \mathbf{t} \, dS + \int_{\Omega} \rho \mathbf{b} \, dV
$$
其中，$\rho$ 是密度，$\mathbf{u}$ 是速度场，$\mathbf{b}$ 是单位质量的体力，而 $\mathbf{t}$ 是**牵引力矢量**，代表了在边界 $\partial\Omega$ 上，外部物质对内部物质施加的单位面积上的接触力。

要从这个适用于有限体积的“全局”定律得到一个适用于空间中每一点的“局部”微分方程，我们必须将所有项都表示为对同一体积 $\Omega$ 的积分。这一过程的核心挑战在于如何处理表面积分项 $\oint_{\partial\Omega} \mathbf{t} \, dS$。

#### 连续介质假设与牵引力矢量

为了在数学上处理接触力，我们首先需要引入**连续介质假设**。该假设认为，物质是无限可分的，并完全填充其所占据的空间区域，从而允许我们将物理量（如密度、速度）定义为位置和时间的连续场。从物理上看，这一假设的合理性建立在宏观尺度 $L$ 远大于微观结构特征尺度 $\ell_{\text{mic}}$（例如分子间距）的基础上 ($L \gg \ell_{\text{mic}}$)。[@problem_id:2922818]

在此假设下，牵引力矢量 $\mathbf{t}$ 可以在一个点 $\mathbf{x}$ 处，通过一个以该点为中心、具有确定法向 $\mathbf{n}$ 的无限小面积元 $\Delta S$ 上的力 $\Delta \mathbf{F}$ 取极限来明确定义：$\mathbf{t}(\mathbf{x}, \mathbf{n}) = \lim_{\Delta S \to 0} \frac{\Delta \mathbf{F}}{\Delta S}$。**柯西的局部作用公设**（Cauchy's Postulate of Local Action）进一步断言，牵引力矢量 $\mathbf{t}$ 仅依赖于作用点 $\mathbf{x}$ 和该点处表面的法向 $\mathbf{n}$，而与该表面局部区域的曲率或形状无关。这个公设是经典连续介质理论的基石。[@problem_id:2619656]

这一经典观点与更先进的理论形成了对比。例如，在**非局部理论**（如Eringen的非局部弹性理论或近场动力学）中，一点的受力取决于其周围一个有限邻域内所有点的状态，从而摒弃了纯粹的表面接触力概念。在**高阶梯度理论**（如应变梯度理论或Cosserat理论）中，接触力可能还依赖于表面的曲率，这引入了内禀长度尺度，用以描述微观结构的影响。[@problem_id:2619656]

#### 柯西应力张量

柯西的下一个关键贡献是证明了牵引力矢量 $\mathbf{t}$ 与法向矢量 $\mathbf{n}$ 之间存在线性关系。这个结论，即**柯西应力定理**，可以通过对一个无限小的四面体应用动量平衡定律来证明。[@problem_id:2621555] 考虑一个顶点在 $\mathbf{x}_0$ 的四面体，其三个面与坐标平面平行，第四个斜面的法向为 $\mathbf{n}$。当四面体的特征尺寸 $h$ 趋于零时，体积力（如重力）和惯性力的贡献（与 $h^3$ 成正比）将远小于表面力的贡献（与 $h^2$ 成正比），因此可以忽略。

最终的力平衡关系揭示了，在 $\mathbf{x}_0$ 点，作用于任意法向为 $\mathbf{n}$ 的平面上的牵引力 $\mathbf{t}(\mathbf{x}_0, \mathbf{n})$ 可以通过一个二阶张量——**柯西应力张量** $\boldsymbol{\sigma}(\mathbf{x}_0)$——与 $\mathbf{n}$ 的线性映射来表示：
$$
\mathbf{t}(\mathbf{x}_0, \mathbf{n}) = \boldsymbol{\sigma}(\mathbf{x}_0) \mathbf{n}
$$
这个定理的成立依赖于应力场在 $\mathbf{x}_0$ 点的**连续性**。如果应力场在该点无界（例如，在理论上的集中力作用点），则此推导失效。值得注意的是，推导仅要求应力场是连续的，而不需要更强的可微性条件。[@problem_id:2621555] 同样，如果体力场包含奇异性，如一个集中力（用狄拉克 $\delta$ 函数表示），则体积力在极限过程中将不可忽略，四面体法的论证也会失败。[@problem_id:2621555]

#### 柯西运动方程的推导

有了应力张量的概念，动量平衡方程中的表面积分项可以重写为 $\oint_{\partial\Omega} \boldsymbol{\sigma} \mathbf{n} \, dS$。此时，我们可以应用**高斯散度定理**，将其转化为一个体积分：
$$
\oint_{\partial\Omega} \boldsymbol{\sigma} \mathbf{n} \, dS = \int_{\Omega} (\nabla \cdot \boldsymbol{\sigma}) \, dV
$$
这里，$\nabla \cdot \boldsymbol{\sigma}$ 是应力张量的散度。经典散度定理的应用要求应力场 $\boldsymbol{\sigma}$ 是一次连续可微的（$C^1$），且边界 $\partial\Omega$ 是分片光滑的。在更现代、更严谨的数学框架中，这些条件可以放宽：只要 $\boldsymbol{\sigma}$ 属于特定的索博列夫空间（即 $\boldsymbol{\sigma} \in H(\text{div};\Omega)$），并且边界是利普希茨连续的，散度定理在弱形式下仍然成立。这恰恰反映了连续介质场作为微观量在代表性体积元上平均的物理本质。[@problem_id:2922818]

同时，动量平衡方程的左侧，即总动量的时间变化率，可以使用**雷诺输运定理**转化为：
$$
\frac{d}{dt} \int_{\Omega} \rho \mathbf{u} \, dV = \int_{\Omega} \rho \frac{D\mathbf{u}}{Dt} \, dV
$$
其中 $\frac{D}{Dt} = \frac{\partial}{\partial t} + \mathbf{u} \cdot \nabla$ 是**物质导数**，表示跟随一个物质点（流体质点）测量的速度变化率。

将所有项都表示为在任意物质体积 $\Omega$ 上的积分后，我们得到：
$$
\int_{\Omega} \rho \frac{D\mathbf{u}}{Dt} \, dV = \int_{\Omega} (\nabla \cdot \boldsymbol{\sigma}) \, dV + \int_{\Omega} \rho \mathbf{b} \, dV
$$
由于这个等式对任意选择的体积 $\Omega$ 都必须成立，且假设被积函数是连续的，那么被积函数本身必须相等。这就得到了动量平衡的局部形式，即**柯西第一运动定律**或**柯西运动方程**：
$$
\rho \frac{D\mathbf{u}}{Dt} = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b}
$$
这个方程是连续介质力学的基石。它表明，单位体积内物质的惯性力（左侧）由内部应力产生的力（$\nabla \cdot \boldsymbol{\sigma}$）和作用于其上的体力（$\rho \mathbf{b}$）所平衡。

### 角动量平衡与应力张量的对称性

除了动量守恒，角动量守恒也是一条基本物理定律。对于连续介质，在没有外部体力矩或面力矩作用的经典（非极性）情况下，角动量平衡定律对柯西应力张量施加了一个非常重要的约束。[@problem_id:2904980]

从角动量平衡的积分形式出发，经过与推导柯西方程类似但更为复杂的步骤，可以证明该定律的局部形式最终归结为一个极其简洁的代数关系：
$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}^T
$$
这意味着柯西应力张量是一个**对称张量**。例如，$\sigma_{xy}$，即作用在 $x$ 法向平面上沿 $y$ 方向的剪应力，必须等于 $\sigma_{yx}$，即作用在 $y$ 法向平面上沿 $x$ 方向的剪应力。

这一对称性并非一个本构假设（即与材料性质相关的假设），而是角动量守恒在经典连续介质框架下的直接推论。它极大地简化了应力分析，将一个二阶张量中独立的未知分量从9个减少到6个。需要强调的是，在考虑具有内部微观结构的材料（如Cosserat介质）时，可能会存在所谓的“力偶应力”，此时角动量平衡将导致一个非对称的应力张量。[@problem_id:2619656] [@problem_id:2621555]

### 动量方程的等价形式

柯西运动方程可以通过各种数学变换，改写成不同的等价形式。这些形式在特定应用中非常有用，因为它们能够凸显出流场中不同的物理机制。

#### 守恒形式

物理学中的许多基本定律都可以表示为守恒律的形式：$\frac{\partial \mathcal{Q}}{\partial t} + \nabla \cdot \mathbf{J}_{\mathcal{Q}} = S_{\mathcal{Q}}$，其中 $\mathcal{Q}$ 是某个守恒量的密度，$\mathbf{J}_{\mathcal{Q}}$ 是其通量，而 $S_{\mathcal{Q}}$ 是源/汇项。

通过结合连续性方程 $\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) = 0$，柯西运动方程可以被严格地改写为动量守恒形式。[@problem_id:460854] 首先展开物质导数：
$$
\rho \left( \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla)\mathbf{u} \right) = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b}
$$
利用连续性方程和向量恒等式，上式可以整理为：
$$
\frac{\partial (\rho \mathbf{u})}{\partial t} + \nabla \cdot (\rho \mathbf{u} \otimes \mathbf{u} - \boldsymbol{\sigma}) = \rho \mathbf{b}
$$
这里，$\mathbf{u} \otimes \mathbf{u}$ 是速度矢量的并矢（在笛卡尔坐标下，其分量为 $u_i u_j$）。这个方程清晰地展示了动量守恒的结构：
-   **动量密度**: $\rho \mathbf{u}$，即单位体积的动量。
-   **总动量通量张量**: $\boldsymbol{\Pi} = \rho \mathbf{u} \otimes \mathbf{u} - \boldsymbol{\sigma}$。这个张量描述了动量如何通过空间进行输运。它包含两个部分：
    -   $\rho \mathbf{u} \otimes \mathbf{u}$：**对流输运项**，表示由于流体自身流动而携带的动量。
    -   $-\boldsymbol{\sigma}$：**应力输运项**，表示由于分子间的相互作用（压力和粘性力）而传递的动量。
-   **动量源**: $\rho \mathbf{b}$，即体力引起的动量产生。

守恒形式在计算流体动力学中尤为重要，因为基于此形式的数值格式能更好地保证物理量的守恒性。

#### 兰姆-格罗梅卡形式与涡量

对于无粘流体（$\boldsymbol{\sigma} = -p\mathbf{I}$，其中 $p$ 是压力），柯西方程简化为**欧拉方程**。通过引入一个重要的向量恒等式，可以将欧拉方程中的对流加速度项 $(\mathbf{u} \cdot \nabla)\mathbf{u}$ 与流体的旋转特性联系起来。该恒等式为：
$$
(\mathbf{u} \cdot \nabla)\mathbf{u} = \nabla\left(\frac{1}{2}|\mathbf{u}|^2\right) - \mathbf{u} \times (\nabla \times \mathbf{u})
$$
其中，$\boldsymbol{\omega} = \nabla \times \mathbf{u}$ 是**涡量矢量**，它描述了流体微团的局部旋转角速度的两倍。

将此恒等式代入欧拉方程，并假设体力是保守的（$\mathbf{b} = -\nabla\Phi$）且流体是正压的（即压力仅是密度的函数，这允许定义一个比焓 $h$ 使得 $\nabla h = \frac{1}{\rho}\nabla p$），我们可以得到**兰姆-格罗梅卡方程**（Lamb-Gromeka form）[@problem_id:460798]：
$$
\frac{\partial \mathbf{u}}{\partial t} + \nabla H = \mathbf{u} \times \boldsymbol{\omega}
$$
其中，$H = \frac{1}{2}|\mathbf{u}|^2 + h + \Phi$ 是**总焓**或**伯努利函数**。该方程形式优美地揭示了流体加速度、能量梯度和涡量之间的关系。右侧的 $\mathbf{u} \times \boldsymbol{\omega}$ 项通常被称为兰姆矢量。

#### 克罗科-瓦松尼形式与热力学

在定常流动（$\frac{\partial}{\partial t} = 0$）的情况下，兰姆-格罗梅卡方程进一步简化。此时，我们可以利用热力学关系，将流动的动力学特性与热力学状态直接联系起来。吉布斯关系给出了比焓 $h$、温度 $T$、比熵 $s$ 和压力 $p$ 之间的微分关系：$dh = T ds + \frac{dp}{\rho}$。其梯度形式为 $\nabla h = T \nabla s + \frac{1}{\rho}\nabla p$。

将此关系代入定常欧拉方程，可推导出**克罗科-瓦松尼方程**（Crocco-Vazsonyi equation）[@problem_id:460832]：
$$
\mathbf{u} \times \boldsymbol{\omega} = T \nabla s - \nabla h_0
$$
其中 $h_0 = h + \frac{1}{2}|\mathbf{u}|^2$ 是总比焓（对于定常绝热流动，若无外功和热交换，此量守恒）。这个方程意义非凡，它直接表明，在定常无粘流动中，涡量（通过兰姆矢量 $\mathbf{u} \times \boldsymbol{\omega}$ 体现）的存在与熵的梯度紧密相连。对于一个熵处处均匀的流动（等熵流），$\nabla s = 0$，如果总焓也均匀，那么必然有 $\mathbf{u} \times \boldsymbol{\omega} = 0$，这意味着速度矢量和涡量矢量处处平行，这种流动被称为“螺旋流”。该方程的一个有趣推论是，对两边取旋度可得 $\nabla \times (\mathbf{u} \times \boldsymbol{\omega}) = \nabla T \times \nabla s$，直接将流场运动学与热力学量的空间分布联系起来。[@problem_id:460832]

### 参照系依赖性与变换

柯西运动方程的形式取决于观察者所在的参照系。

#### 非惯性参照系

在惯性系中表述的柯西方程，可以通过坐标变换转换到非惯性系（例如，一个相对于惯性系在做旋转和平动的参照系，如地球）中。变换的结果是，在方程的右侧会额外出现一些“虚拟”的体力项，这些项被称为**惯性力**或**视在力**。[@problem_id:460816]

在以角速度 $\mathbf{\Omega}'$ 旋转的非惯性系中，完整的柯西方程（以非惯性系中的量表示）写作：
$$
\rho \frac{D\mathbf{u}'}{Dt} = \nabla' \cdot \boldsymbol{\sigma}' + \rho \mathbf{g}' - \rho \mathbf{a}'_0 - 2\rho(\mathbf{\Omega}' \times \mathbf{u}') - \rho[\mathbf{\Omega}' \times (\mathbf{\Omega}' \times \mathbf{x}')] - \rho(\dot{\mathbf{\Omega}}' \times \mathbf{x}')
$$
新增的视在力项分别为：
-   **平动惯性力**: $-\rho \mathbf{a}'_0$，与参照系原点的平动加速度有关。
-   **科里奥利力**: $-2\rho(\mathbf{\Omega}' \times \mathbf{u}')$，作用于运动的物体。
-   **离心力**: $-\rho[\mathbf{\Omega}' \times (\mathbf{\Omega}' \times \mathbf{x}')]$，指向旋转轴的外部。
-   **欧拉力**: $-\rho(\dot{\mathbf{\Omega}}' \times \mathbf{x}')$，仅在角速度变化时出现。

这些视在力的散度并非总是为零，它们可以影响流体的可压缩性效应。例如，可以证明，视在力场的总散度为 $\nabla' \cdot \mathbf{f}_{\text{app}} = 2\mathbf{\Omega}' \cdot \boldsymbol{\omega}' + 2|\mathbf{\Omega}'|^2$，其中 $\boldsymbol{\omega}' = \nabla' \times \mathbf{u}'$ 是非惯性系中的相对涡量。[@problem_id:460816]

#### 任意拉格朗日-欧拉（ALE）参照系

在计算力学中，特别是在处理移动边界或大变形问题时，纯粹的欧拉描述（固定网格）或拉格朗日描述（网格随物质运动）都有其局限性。**任意拉格朗日-欧拉（ALE）**方法提供了一种混合框架，其计算网格以一个独立指定的网格速度 $\mathbf{w}$ 运动。

在这种框架下，物理量 $f$ 的时间导数关系变为 $\left. \frac{\partial f}{\partial t} \right|_{\mathbf{x}} = \left. \frac{\partial f}{\partial t} \right|_{\boldsymbol{\xi}} - (\mathbf{w} \cdot \nabla) f$，其中 $\boldsymbol{\xi}$ 是ALE参照坐标。将此关系代入柯西方程，物质导数中的对流项变为由物质速度与网格速度的相对速度 $\mathbf{u} - \mathbf{w}$ 驱动。整理后可得，柯西方程在ALE框架下的形式为 [@problem_id:460746]：
$$
\rho \left. \frac{\partial \mathbf{u}}{\partial t} \right|_{\boldsymbol{\xi}} + \rho ((\mathbf{u} - \mathbf{w}) \cdot \nabla)\mathbf{u} = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b}
$$
这种形式允许网格运动与物质运动解耦，从而在模拟流固耦合等问题时提供了极大的灵活性。

### 能量平衡与耗散

动量方程与能量守恒定律密切相关。通过将柯西运动方程与速度矢量 $\mathbf{u}$ 做点积，可以推导出单位质量动能 $k = \frac{1}{2}\mathbf{u} \cdot \mathbf{u}$ 的平衡方程。[@problem_id:460770]

在这一过程中，应力项 $\mathbf{u} \cdot (\nabla \cdot \boldsymbol{\sigma})$ 代表了应力力所做的功率密度。利用向量恒等式和应力张量的对称性，该项可以分解为：
$$
\mathbf{u} \cdot (\nabla \cdot \boldsymbol{\sigma}) = \nabla \cdot (\boldsymbol{\sigma} \cdot \mathbf{u}) - \boldsymbol{\sigma} : \nabla \mathbf{u}
$$
-   **能量通量**: $\nabla \cdot (\boldsymbol{\sigma} \cdot \mathbf{u})$ 这一项可以被移到方程的另一侧，解释为通过应力传递的机械能通量。
-   **应力耗散**: $\mathcal{P}_{diss} = \boldsymbol{\sigma} : \nabla \mathbf{u}$ 这一项则是一个源/汇项。它代表了单位体积内，机械能由于材料变形而不可逆地转化为内能（通常是热能）的速率。对于粘性流体，这一项总是非负的，代表了粘性耗散。

我们可以通过一个具体的例子来理解应力耗散。考虑一个幂律流体在定常简单剪切流 $\mathbf{u} = (Ky, 0, 0)$ 中的行为。其粘性应力张量为 $\boldsymbol{\tau} = 2 \eta \mathbf{D}$，其中 $\mathbf{D}$ 是应变率张量，表观粘度 $\eta = m (\dot{\gamma}_{eq})^{n-1}$，而等效剪切率 $\dot{\gamma}_{eq} = \sqrt{2 (\mathbf{D}:\mathbf{D})}$。对于此流动，可以计算出 $\dot{\gamma}_{eq} = K$。应力耗散功率密度为 $\mathcal{P}_{diss} = \boldsymbol{\tau} : \nabla \mathbf{u}$。经过计算，我们得到一个简洁的结果 [@problem_id:460770]：
$$
\mathcal{P}_{diss} = m K^{n+1}
$$
这个结果清晰地展示了耗散率如何依赖于材料的流变特性（$m$ 和 $n$）以及流动的运动学特性（剪切率 $K$）。