## 引言
强制[对流](@entry_id:141806)，即通过外部手段（如风扇、泵）强制流体运动来传递热量的过程，是工程技术与自然界中最为普遍的热传递机制之一。从计算机芯片的散热到发电厂的能量转换，再到[动物的体温调节](@entry_id:204197)，精确预测和控制强制[对流](@entry_id:141806)对于系统性能、效率和安全至关重要。然而，[对流传热](@entry_id:151349)的复杂性在于它融合了流体[动力学与[热力](@entry_id:138039)学](@entry_id:141121)，其行为由一系列相互耦合的物理过程决定。为了系统地掌握这一关键课题，我们需要一个从基本原理到实际应用的完整知识框架。

本文旨在提供这样一个全面的视角。在第一章“原理与机制”中，我们将回归本源，从质量、动量和[能量守恒](@entry_id:140514)定律出发，通过引入强大的[边界层理论](@entry_id:202929)，揭示控制强制[对流](@entry_id:141806)的核心[无量纲参数](@entry_id:169335)（如雷诺数和普朗特数）的物理意义，并探讨[层流](@entry_id:149458)、[混合对流](@entry_id:154925)乃至[湍流](@entry_id:151300)的基本概念。随后的“应用与跨学科[交叉](@entry_id:147634)”一章将展示这些理论的巨大威力，通过深入剖析其在[换热器设计](@entry_id:136266)、电子设备[热管理](@entry_id:146042)、[化学反应工程](@entry_id:151477)、生物物理等多个领域的具体应用，连接基础理论与真实世界问题。最后，在“动手实践”部分，您将有机会通过解决一系列精心设计的问题，将理论知识转化为实践技能，从推导关键参数到分析复杂的系统行为，从而巩固并深化您的理解。

## 原理与机制

本章旨在深入探讨强制[对流](@entry_id:141806)的基本原理和核心机制。我们将从控制[流体运动](@entry_id:182721)和热量传递的[守恒定律](@entry_id:269268)出发，通过引入[边界层理论](@entry_id:202929)这一强大的简化工具，揭示强制[对流](@entry_id:141806)问题的内在结构。在此基础上，我们将分析几个典型的流动构型，阐释关键无量纲参数（如[雷诺数](@entry_id:136372)、[普朗特数](@entry_id:143303)）的物理意义，并最终将讨论拓展至更复杂的[混合对流](@entry_id:154925)与[湍流](@entry_id:151300)现象。

### [无量纲参数](@entry_id:169335)与控制方程

强制[对流](@entry_id:141806)的分析始于质量、动量和能量的[守恒定律](@entry_id:269268)。对于不可压缩的牛顿流体，在[稳态](@entry_id:182458)条件下，这些定律的数学表达式为：

- **质量守恒（[连续性方程](@entry_id:195013)）**:
$$ \nabla \cdot \mathbf{u} = 0 $$

- **动量守恒（[Navier-Stokes](@entry_id:276387) 方程）**:
$$ \rho (\mathbf{u} \cdot \nabla \mathbf{u}) = -\nabla p + \mu \nabla^2 \mathbf{u} + \mathbf{f} $$

- **[能量守恒](@entry_id:140514)**:
$$ \rho c_p (\mathbf{u} \cdot \nabla T) = k \nabla^2 T + \Phi_v $$

在此，$\rho$ 是流体密度，$\mathbf{u}$ 是[速度场](@entry_id:271461)，$p$ 是压力，$\mu$ 是[动力粘度](@entry_id:268228)，$\mathbf{f}$ 是单位体积的[体力](@entry_id:174230)（如重力），$c_p$ 是定[压比](@entry_id:137698)[热容](@entry_id:137594)，$T$ 是温度场，$k$ 是热导率。$\Phi_v$ 是[粘性耗散](@entry_id:143708)函数，表示由流体内摩擦产生的热量，其量级可近似为 $\mu (U/L)^2$，其中 $U$ 和 $L$ 分别是问题的特征速度和[特征长度](@entry_id:265857)。

为了揭示这些方程中各项的相对重要性，并使分析具有普适性，我们对其进行[无量纲化](@entry_id:136704)。通过引入特征尺度 $L$、$U$、$\Delta T$（特征温差）和 $T_0$（参考温度），我们可以定义无量纲变量：$\mathbf{x}^* = \mathbf{x}/L$，$\mathbf{u}^* = \mathbf{u}/U$，$\theta = (T - T_0)/\Delta T$。将这些变量代入能量方程，可以得到两个重要的[无量纲数](@entry_id:136814) [@problem_id:546558]。

将能量方程 $\rho c_p (\mathbf{u} \cdot \nabla T) = k \nabla^2 T + \Phi_v$ 的各项除以[热传导](@entry_id:147831)项的尺度 $k \Delta T / L^2$，我们得到：
$$ \frac{\rho c_p U L}{k} (\mathbf{u}^* \cdot \nabla^* \theta) = \nabla^{*2} \theta + \frac{\mu U^2}{k \Delta T} $$

其中，[对流](@entry_id:141806)项的系数定义为**[佩克莱数](@entry_id:141791) (Peclet number)**, $Pe$：
$$ Pe = \frac{\rho c_p U L}{k} = \frac{UL}{\alpha} $$
这里 $\alpha = k/(\rho c_p)$ 是[热扩散率](@entry_id:144337)。佩克莱数代表了[对流传热](@entry_id:151349)速率与热传导速率之比。

[粘性耗散](@entry_id:143708)项的系数可以重新整理为**埃克特数 (Eckert number)**, $Ec$：
$$ \frac{\mu U^2}{k \Delta T} = \frac{\mu c_p}{k} \frac{U^2}{c_p \Delta T} = \frac{\nu}{\alpha} \frac{U^2}{c_p \Delta T} = Pr \cdot Ec $$
其中 $Pr = \nu/\alpha$ 是[普朗特数](@entry_id:143303)，而埃克特数的标准定义为：
$$ Ec = \frac{U^2}{c_p \Delta T} $$
埃克特数代表了流动的特征动能与[特征比](@entry_id:190624)焓差之比。在大多数工程应用中，除非流速极高（如[高超声速飞行](@entry_id:272087)）或粘度极大，否则 $Ec$ 的值通常远小于1，这意味着[粘性耗散](@entry_id:143708)产生的热量相对于[对流](@entry_id:141806)和传导传递的热量可以忽略不计。因此，在后续的许多分析中，我们将忽略 $\Phi_v$ 项。

### [边界层近似](@entry_id:153725)

对于高雷诺数 ($Re \gg 1$) 的外部绕流问题，粘性效应和热效应主要集中在紧贴物体表面的一个薄层内，这个薄层被称为**[边界层](@entry_id:139416) (boundary layer)**。[边界层理论](@entry_id:202929)是 [Ludwig Prandtl](@entry_id:268561) 在20世纪初提出的一个里程碑式的概念，它极大地简化了[流体动力学](@entry_id:136788)和传热学的分析。

考虑一个[特征长度](@entry_id:265857)为 $L$ 的物体，沉浸在速度为 $U_\infty$ 的来流中。在高[雷诺数](@entry_id:136372)下，[边界层](@entry_id:139416)的厚度 $\delta$ 远小于 $L$ ($\delta \ll L$)。我们可以利用这一几何特征进行量级分析，从而简化控制方程 [@problem_id:2477122]。

我们引入如下的无量纲变量，其中纵向坐标 $y$ 用[边界层厚度](@entry_id:269100) $\delta$ 进行缩放，而横向坐标 $x$ 用物体[特征长度](@entry_id:265857) $L$ 进行缩放：
$$ x = L x^*, \quad y = \delta y^*, \quad u = U_\infty u^*, \quad v = \varepsilon U_\infty v^*, \quad p = p_\infty + \rho U_\infty^2 p^*, \quad \theta = \frac{T - T_\infty}{\Delta T} $$
其中 $\varepsilon = \delta/L \ll 1$ 是[边界层](@entry_id:139416)的细长比。

将这些变量代入二维[稳态](@entry_id:182458)的[动量方程](@entry_id:197225)，特别是流向[动量方程](@entry_id:197225)：
$$ \rho \left( u \frac{\partial u}{\partial x} + v \frac{\partial u}{\partial y} \right) = - \frac{\partial p}{\partial x} + \mu \left( \frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} \right) $$
[无量纲化](@entry_id:136704)后得到：
$$ u^* \frac{\partial u^*}{\partial x^*} + v^* \frac{\partial u^*}{\partial y^*} = - \frac{\partial p^*}{\partial x^*} + \frac{1}{Re_L} \frac{\partial^2 u^*}{\partial x^{*2}} + \frac{1}{\varepsilon^2 Re_L} \frac{\partial^2 u^*}{\partial y^{*2}} $$
这里 $Re_L = U_\infty L / \nu$。方程左侧的惯性项量级为 $O(1)$。为了使粘性项在方程中保持重要性（否则就变成了[无粘流](@entry_id:273124)动），最大的粘性项必须也是 $O(1)$ 量级。由于 $Re_L \gg 1$，$\partial^2 u^*/\partial x^{*2}$ 前的系数 $1/Re_L$ 很小，因此流向的粘性[扩散](@entry_id:141445)项可以忽略。为了使法向粘性[扩散](@entry_id:141445)项得以保留，必须满足：
$$ \frac{1}{\varepsilon^2 Re_L} \sim O(1) \implies \varepsilon^2 \sim \frac{1}{Re_L} \implies \varepsilon = \frac{\delta}{L} \sim Re_L^{-1/2} $$
这是[层流边界层](@entry_id:153016)厚度 scaling 的基本关系。它表明，雷诺数越高，[边界层](@entry_id:139416)相对越薄。

通过类似的量级分析，我们可以得到简化后的**[边界层方程](@entry_id:202817)组**:
- **[连续性方程](@entry_id:195013)**: $\dfrac{\partial u^*}{\partial x^*} + \dfrac{\partial v^*}{\partial y^*} = 0$
- **流向[动量方程](@entry_id:197225)**: $u^* \dfrac{\partial u^*}{\partial x^*} + v^* \dfrac{\partial u^*}{\partial y^*} = - \dfrac{dp^*}{dx^*} + \dfrac{\partial^2 u^*}{\partial y^{*2}}$
- **法向[动量方程](@entry_id:197225)**: $\dfrac{\partial p^*}{\partial y^*} = 0$
- **能量方程** (假设 $Pr = O(1)$): $u^* \dfrac{\partial \theta}{\partial x^*} + v^* \dfrac{\partial \theta}{\partial y^*} = \dfrac{1}{Pr} \dfrac{\partial^2 \theta}{\partial y^{*2}}$

这些方程的重要特征包括：(1) 流向的[扩散](@entry_id:141445)项（粘性[扩散](@entry_id:141445)和[热传导](@entry_id:147831)）被忽略；(2) 法向动量方程简化为压力在[边界层](@entry_id:139416)法向方向上不变，即 $p(x,y) = p_e(x)$，[边界层](@entry_id:139416)内的压力由外部[无粘流](@entry_id:273124)决定；(3) [方程组](@entry_id:193238)从椭圆型[偏微分方程](@entry_id:141332)简化为抛物线型，这使得可以采用高效的 marching 算法沿流向进行数值求解。

### 相似性解：平板上的强制[对流](@entry_id:141806)

[边界层方程](@entry_id:202817)虽然是简化形式，但仍是[偏微分方程组](@entry_id:172573) (PDEs)。在某些特定条件下，可以通过**相似性变换 (similarity transformation)** 将其转化为[常微分方程组](@entry_id:266774) (ODEs)，从而得到解析或半解析解。最经典的例子是零[压力梯度](@entry_id:274112)的平板绕流问题，即 **Blasius 解**。

考虑流速为 $U_\infty$ 的均匀来流流过一个半无限长的等温平板。在这种情况下，$dp^*/dx^*=0$。Blasius 发现，[速度场](@entry_id:271461)可以用一个相似性变量 $\eta$ 和一个无量纲流函数 $f(\eta)$ 来描述 [@problem_id:2477084]：
$$ \eta = y \sqrt{\frac{U_\infty}{\nu x}}, \quad \psi(x,y) = \sqrt{\nu U_\infty x} f(\eta) $$
其中流函数 $\psi$ 自动满足连续性方程，其定义为 $u = \partial\psi/\partial y$ 和 $v = -\partial\psi/\partial x$。通过这个变换，动量[边界层方程](@entry_id:202817)简化为著名的 **Blasius 方程**：
$$ 2 f'''(\eta) + f(\eta) f''(\eta) = 0 $$
其边界条件为 $f(0)=0, f'(0)=0, f'(\infty)=1$。值得注意的是，这个方程及其解 $f(\eta)$ 完全由[流体动力学](@entry_id:136788)决定，与温度场无关。

对于[热传导](@entry_id:147831)问题，我们可以假设温度场也具有相似性，即无量纲温度 $\theta = (T - T_\infty)/(T_w - T_\infty)$ 仅是 $\eta$ 的函数，$\theta=\theta(\eta)$。将此形式代入能量[边界层方程](@entry_id:202817)，得到：
$$ \theta''(\eta) + \frac{Pr}{2} f(\eta) \theta'(\eta) = 0 $$
其边界条件为 $\theta(0)=1, \theta(\infty)=0$。这个方程的解（有时称为 **Pohlhausen 解**）依赖于两个因素：普朗特数 $Pr$ 和已经从 Blasius 方程中解出的速度场函数 $f(\eta)$。

这个求解过程揭示了一个至关重要的概念：**[单向耦合](@entry_id:752919) (one-way coupling)**。在流体物性（密度、粘度等）恒定且忽略[浮力](@entry_id:144145)效应的假设下，[动量方程](@entry_id:197225)是[解耦](@entry_id:637294)的，可以独立求解速度场。然后，这个已知的[速度场](@entry_id:271461)作为能量方程的输入，用于求解温度场。温度场虽然受[速度场](@entry_id:271461)输运，但它本身不会反过来影响[速度场](@entry_id:271461)。这种情况下的热量传递被称为**[被动标量](@entry_id:191726)输运 (passive scalar transport)**。如果物性随温度变化，或者存在[浮力](@entry_id:144145)效应（见[混合对流](@entry_id:154925)部分），这种[单向耦合](@entry_id:752919)就会被打破，动量和能量方程必须联立求解。

### 普朗特数与雷诺比拟的角色

**普朗特数 (Prandtl number)**, $Pr = \nu/\alpha$，是动量扩散率（[运动粘度](@entry_id:275614) $\nu$）与[热扩散率](@entry_id:144337)（$\alpha$）之比，它在强制[对流](@entry_id:141806)中扮演着核心角色。它直接决定了速度[边界层厚度](@entry_id:269100) $\delta$ 与热[边界层厚度](@entry_id:269100) $\delta_t$ 的相对大小 [@problem_id:2488747]。通过对动量和能量[边界层方程](@entry_id:202817)进行量级分析，可以推导出它们厚度的近似关系：
$$ \frac{\delta_t}{\delta} \sim Pr^{-n} $$
其中指数 $n$ 通常在 $1/3$ 到 $1/2$ 之间。这个关系具有深刻的物理含义：
- **$Pr > 1$ (例如水、油)**: [动量扩散](@entry_id:157895)比热扩散快。这意味着速度[边界层](@entry_id:139416)比热边界层更厚 ($\delta > \delta_t$)。流体微团在减速之前，其热量已经有效地传递给了邻近流体。
- **$Pr < 1$ (例如液态金属)**: [热扩散](@entry_id:148740)比[动量扩散](@entry_id:157895)快。[热边界层](@entry_id:147903)比速度[边界层](@entry_id:139416)更厚 ($\delta_t > \delta$)。热量能够迅速[扩散](@entry_id:141445)到速度尚未受到壁面影响的区域。
- **$Pr \approx 1$ (例如空气和大多数气体)**: 动量和热量的[扩散](@entry_id:141445)速率相近，因此两个[边界层](@entry_id:139416)的厚度也大致相同 ($\delta_t \approx \delta$)。

由于局部努塞尔数 $Nu_L$ 反比于热[边界层厚度](@entry_id:269100)（$Nu_L \sim L/\delta_t$），因此在固定的[雷诺数](@entry_id:136372)下，$Nu_L$ 会随着普朗特数的增加而增加。这是因为更高的 $Pr$ 值（在 $\nu$ 不变时意味着更小的 $\alpha$）导致热边界层更薄，从而在壁面产生更陡峭的温度梯度，增大了壁面热流密度。

$Pr=1$ 的特殊情况引出了一个重要的概念——**雷诺比拟 (Reynolds analogy)**。当 $Pr=1$ 且压力梯度为零时，无量纲的动量和能量相似性方程在形式上变得完全相同。可以证明，此时 $\theta(\eta) = 1 - f'(\eta)$ [@problem_id:2477113] [@problem_id:2477084]。这意味着无量纲温度[分布](@entry_id:182848)与无量纲[速度亏损](@entry_id:269642) (velocity defect) 的[分布](@entry_id:182848)完全一致。这一数学上的等价性直接导致了壁面摩擦与换热之间的简单关系：
$$ St = \frac{C_f}{2} $$
其中 $St$ 是**[斯坦顿数](@entry_id:151149) (Stanton number)** ($St=Nu/(Re \cdot Pr)$)，$C_f$ 是**壁面摩擦系数 (skin-friction coefficient)**。这个比拟在工程上非常有用，因为它允许通过更容易测量的壁面摩擦来估算传热速率。

然而，雷诺比拟的有效性严格限于 $Pr \approx 1$ 的情况。在 $Pr \to \infty$ 的极限下，[热边界层](@entry_id:147903)极薄，完全位于速度[边界层](@entry_id:139416)的线性近壁区内。[渐近分析](@entry_id:160416)表明，此时 $St/(C_f/2) \sim Pr^{-2/3}$，远小于1 [@problem_id:2477113]。而在 $Pr \to 0$ 的极限下，[热边界层](@entry_id:147903)极厚，远超速度[边界层](@entry_id:139416)。[渐近分析](@entry_id:160416)表明，$St/(C_f/2) \sim Pr^{-1/2}$，远大于1。这些结果清晰地表明，当动量和热量的[扩散机制](@entry_id:158710)存在显著差异时，雷诺比拟会失效。

### 外部绕流：圆柱体的横向流

从理想的[平板流](@entry_id:151812)动转向更现实的[曲面](@entry_id:267450)绕流，例如圆柱体横向流，会引入[压力梯度](@entry_id:274112)的重要影响。

首先，正确定义描述流动的无量纲参数至关重要。对于圆柱体横向流，**雷诺数**通常定义为 $Re_D = U_\infty D / \nu$，其中 $D$ 是圆柱体的直径。这一选择具有坚实的理论基础 [@problem_id:2488694]。$D$ 是该几何体唯一的外部[特征长度](@entry_id:265857)，用它对 Navier-Stokes 方程进行[无量纲化](@entry_id:136704)，可以自然地导出 $Re_D$ 作为表征惯性力与粘性力之比的关键相似性参数。而来流速度 $U_\infty$ 和来流物性（如 $\nu_\infty$）是问题的外部给定条件，使用它们可以清晰地将流动的主要动力学特性与壁面热效应（如因温度变化引起的物性变化）分离开来。

圆柱体绕流的物理图像比平板复杂得多 [@problem_id:2488699]。从前[驻点](@entry_id:136617) ($\theta=0$) 开始，流体沿表面加速，此区域存在**[顺压梯度](@entry_id:271110) (favorable pressure gradient)** ($dp/dx < 0$)。随后，流体经过圆柱顶部（对于无粘[势流](@entry_id:159985)，在 $\theta=\pi/2$ 处速度最大），进入**逆压梯度 (adverse pressure gradient)** 区 ($dp/dx > 0$)。这个压[力场](@entry_id:147325)的变化深刻地影响了[边界层](@entry_id:139416)的行为：
- **壁面[剪切应力](@entry_id:137139) $\tau_w(\theta)$**: 在前[驻点](@entry_id:136617) $\theta=0$ 处，由于对称性，切向速度为零，因此 $\tau_w=0$。在[顺压梯度](@entry_id:271110)区，流体加速，[边界层](@entry_id:139416)变薄，$\tau_w$ 随 $\theta$ 增加而增加。进入逆压梯度区后，流体减速，[边界层](@entry_id:139416)增厚，$\tau_w$ 开始下降。最终，在[分离点](@entry_id:265082) $\theta_s$ 处，壁面速度梯度变为零，$\tau_w$ 再次为零，[边界层](@entry_id:139416)从壁面脱离。因此，$\tau_w$ 的[分布](@entry_id:182848)是从0开始，达到一个峰值，然后下降到0。
- **壁面热流密度 $q''_w(\theta)$**: [传热效率](@entry_id:153787)与热[边界层厚度](@entry_id:269100)密切相关。在前驻点 $\theta=0$ 处，[边界层](@entry_id:139416)刚刚开始发展，厚度最薄，因此[温度梯度](@entry_id:136845)最大，导致[传热系数](@entry_id:155200)和[热流密度](@entry_id:138471)达到**最大值**。随着流体沿表面向下游流动，[边界层](@entry_id:139416)逐渐增厚，[传热效率](@entry_id:153787)下降，因此 $q''_w(\theta)$ 从[驻点](@entry_id:136617)开始递减。在分离点附近，由于流动缓慢和[边界层](@entry_id:139416)很厚，[传热效率](@entry_id:153787)达到局部最小值。

在工程应用中，我们通常更关心整个表面的平均传热效果。这需要正确地将局部量积分得到平均量 [@problem_id:2488751]。对于等温圆柱体，平均传热系数 $\overline{h}$ 定义为总热流量 $q'$ 与总表面积 $A$ 和温差 $\Delta T$ 的比值，即 $q' = \overline{h} A \Delta T$。通过对局部[热流密度](@entry_id:138471) $q''_w(\theta) = h(\theta)\Delta T$ 在整个表面进行积分，可以证明，平均[传热系数](@entry_id:155200) $\overline{h}$ 正是局部传热系数 $h(\theta)$ 的面积平均值。因此，平均努塞尔数 $\overline{Nu} = \overline{h}D/k$ 也就是局部努塞尔数 $Nu_\theta = h(\theta)D/k$ 的面积平均值：
$$ \overline{Nu} = \frac{1}{2\pi} \int_{0}^{2\pi} Nu_\theta \,d\theta $$
这些关系为从局部传热测量或计算结果推断总体性能提供了数学基础。

### [混合对流](@entry_id:154925)：[强制对流与自然对流](@entry_id:151028)的相互作用

到目前为止，我们一直假设浮力可以忽略不计。然而，当存在显著的温度差异和重[力场](@entry_id:147325)时，由温度引起的密度变化会产生浮力，从而驱动或阻碍流动。当这种[自然对流](@entry_id:197869)效应与外部强制流动的惯性[效应量](@entry_id:177181)级相当时，就进入了**[混合对流](@entry_id:154925) (mixed convection)** 的范畴 [@problem_id:2506691]。

考虑一个竖直放置的平板，环境流体可以向上或向下流动。在 Boussinesq 近似下，[浮力](@entry_id:144145)项 $g\beta(T-T_\infty)$ 出现在流向[动量方程](@entry_id:197225)中，其中 $g$ 是[重力加速度](@entry_id:173411)，$\beta$ 是热膨胀系数。[混合对流](@entry_id:154925)的本质是惯性项（如 $u \partial u / \partial x$）与浮力项的竞争。

为了量化这种竞争关系，我们定义**[理查森数](@entry_id:151448) (Richardson number)**, $Ri$，作为浮力项与惯性项的量级之比：
$$ Ri = \frac{g\beta(T_s - T_\infty)L}{U_\infty^2} = \frac{Gr}{Re^2} $$
其中，$Gr = g\beta|T_s - T_\infty|L^3/\nu^2$ 是**[格拉晓夫数](@entry_id:150661) (Grashof number)**，代表浮力与[粘性力](@entry_id:263294)的比值。$Ri$ 的大小决定了流动的性质：
- **$|Ri| \ll 1$**: [惯性力](@entry_id:169104)占主导，流动为强制[对流](@entry_id:141806)。
- **$|Ri| \gg 1$**: 浮力占主导，流动为自然对流。
- **$|Ri| \sim O(1)$**: 两种效应都重要，流动为[混合对流](@entry_id:154925)。

浮力可以增强或削弱强制流动，这取决于[浮力](@entry_id:144145)的方向与主流方向的关系。对于竖直平板（$x$ 轴向上）：
- **助流 (Aiding/Augmenting flow)**: [浮力](@entry_id:144145)与主流同向。
    - 向上主流 ($U_\infty > 0$) + 热壁 ($T_s > T_\infty$，浮力向上)。
    - 向下主流 ($U_\infty < 0$) + 冷壁 ($T_s < T_\infty$，浮力向下)。
- **反向流 (Opposing flow)**: [浮力](@entry_id:144145)与主流反向。
    - 向上主流 ($U_\infty > 0$) + 冷壁 ($T_s < T_\infty$，浮力向下)。
    - 向下主流 ($U_\infty < 0$) + 热壁 ($T_s > T_\infty$，[浮力](@entry_id:144145)向上)。

助流通常会使[边界层](@entry_id:139416)变薄，从而增强壁面摩擦和传热。反向流则会使[边界层](@entry_id:139416)增厚，甚至可能导致[流动分离](@entry_id:143331)，使流动结构和传热特性变得异常复杂。

### 对[湍流模型](@entry_id:190404)的展望

本章的讨论主要集中在层流。然而，大多数工程实际中的强制[对流](@entry_id:141806)问题都涉及[湍流](@entry_id:151300)。在[湍流](@entry_id:151300)中，动量和热量的输运被随机的[涡旋运动](@entry_id:198769)（即“[湍流](@entry_id:151300)脉动”）大大增强。直接模拟这些脉动（DNS）计算量极大，因此工程上依赖于**[湍流模型](@entry_id:190404) (turbulence models)**。

这些模型的核心思想是，[湍流](@entry_id:151300)脉动对平均流动的影响可以类比于分子运动，从而引入**[湍流](@entry_id:151300)粘度 (turbulent viscosity)** $\nu_t$ 和**[湍流](@entry_id:151300)[热扩散率](@entry_id:144337) (turbulent thermal diffusivity)** $\alpha_t$。例如，雷诺应力 $-\overline{u'_1 u'_2}$ 和[湍流热通量](@entry_id:151024) $-\overline{u'_2 \theta'}$ 可以分别模化为：
$$ -\overline{u'_1 u'_2} = \nu_t \frac{\partial U_1}{\partial x_2}, \quad -\overline{u'_2 \theta'} = \alpha_t \frac{\partial \Theta}{\partial x_2} $$
这里 $U_1, \Theta$ 是平均速度和平均温度，而 $u', \theta'$ 是脉动量。

类似于[分子输运](@entry_id:195239)，我们可以定义**[湍流普朗特数](@entry_id:153739) (turbulent Prandtl number)**：
$$ Pr_t = \frac{\nu_t}{\alpha_t} $$
$Pr_t$ 表征了[湍流输运](@entry_id:150198)动量与[输运热](@entry_id:136679)量的[相对效率](@entry_id:165851)。在许多简单模型中，$Pr_t$ 被假设为一个常数（通常在 0.85 到 0.9 之间）。然而，更高级的湍流模型，如**代数[雷诺应力模型](@entry_id:754343) (ARSM)** 和**代数热通量模型 (AHFM)**，可以从更基本的物理原理出发，推导出 $Pr_t$ 的表达式。

例如，在[局部平衡](@entry_id:156295)的均匀[剪切流](@entry_id:266817)中，通过求解简化的雷诺应力和热通量输运方程，可以得到 $Pr_t$ 与模型常数之间的关系 [@problem_id:520478]。一个典型的结果是：
$$ Pr_t = \frac{C_{1\theta}(1-C_2)}{C_1(1-C_{2\theta})} $$
其中 $C_1, C_2, C_{1\theta}, C_{2\theta}$ 等是描述[湍流](@entry_id:151300)中压力-应变和压力-[温度梯度](@entry_id:136845)相互作用的经验常数。这个结果虽然依赖于模型，但它揭示了 $Pr_t$ 并非一个普适常数，而是由[湍流](@entry_id:151300)场中动量和热量输运的复杂物理过程共同决定的。这为我们从层流的基本原理向更复杂的[湍流](@entry_id:151300)世界迈进提供了一个概念性的桥梁。