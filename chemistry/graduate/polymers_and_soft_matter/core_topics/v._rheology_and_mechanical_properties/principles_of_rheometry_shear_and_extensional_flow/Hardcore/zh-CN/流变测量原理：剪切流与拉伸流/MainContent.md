## 引言
从工业生产线上的高分子熔体到我们血管中流动的血液，我们周围的世界充满了行为复杂的流体。与水或蜂蜜等简单流体不同，这些“复杂流体”在流动时会表现出拉伸、弹性甚至爬杆等奇特现象。流变测量学（Rheometry）正是量化和理解这些复杂行为的科学，它为我们预测和控制这些材料在加工和应用中的表现提供了关键工具。然而，仅仅用一个“粘度”值远不足以描述这些材料的丰富行为。一个核心的挑战在于理解和区分材料在不同类型流动——主要是剪切流和拉伸流——中的响应差异，并将这些宏观行为与它们的微观结构（如高分子链的构象）联系起来。

本文旨在系统地构建理解这一挑战的知识框架。我们将通过三个章节，带领读者从基础走向应用。在“原则与机理”一章中，我们将建立描述流体变形的普适运动学框架，并详细定义在剪切流和拉伸流中表征材料响应的关键函数，同时探究其背后的物理机理。接着，在“应用与跨学科交叉”一章中，我们将展示这些基本原理如何应用于仪器设计、高分子加工、生物流变学等实际问题中，彰显流变学的跨学科价值。最后，“动手实践”部分将提供一系列练习，帮助读者巩固和应用所学知识。

## 原则与机理

在本章中，我们将深入探讨流变测量学的核心原则与机理。我们将从描述流体变形的普适运动学框架出发，系统地定义和解释在两种典型的理想流动——剪切流和拉伸流——中表征材料响应的关键材料函数。此外，我们将探讨这些宏观流变行为背后的微观物理机理，并介绍用于量化材料时间尺度与流动时间尺度之间相互作用的重要无量纲数。

### 流动的运动学描述

为了精确描述材料在流动过程中的变形，我们首先需要一个数学框架。任何流动的局部行为都可以由速度梯度张量 $\nabla \mathbf{v}$ 来完全描述，其分量为 $[\nabla \mathbf{v}]_{ij} = \partial v_i / \partial x_j$。这个二阶张量捕捉了流场中相邻点之间速度的差异。

根据柯西-斯托克斯分解定理 (Cauchy-Stokes decomposition theorem)，任何速度梯度张量都可以唯一地分解为一个对称部分和一个反对称部分：

$\nabla \mathbf{v} = \mathbf{D} + \mathbf{W}$

其中，**形变速率张量 (rate-of-deformation tensor)** $\mathbf{D}$ 是对称部分，定义为：

$\mathbf{D} = \frac{1}{2} \left( \nabla \mathbf{v} + (\nabla \mathbf{v})^{\mathsf{T}} \right)$

而 **涡量张量 (vorticity tensor)** $\mathbf{W}$ 是反对称部分，定义为：

$\mathbf{W} = \frac{1}{2} \left( \nabla \mathbf{v} - (\nabla \mathbf{v})^{\mathsf{T}} \right)$

形变速率张量 $\mathbf{D}$ 描述了流体微元的纯拉伸和压缩变形，即其形状的改变。对于不可压缩流体，其体积在变形过程中保持不变，这在数学上表现为 $\mathrm{tr}(\mathbf{D}) = \nabla \cdot \mathbf{v} = 0$。涡量张量 $\mathbf{W}$ 则描述了流体微元的刚性旋转。如果一个流动中 $\mathbf{W} = \mathbf{0}$，则该流动被称为**无旋流 (irrotational flow)**。

#### 简单剪切流

**简单剪切流 (simple shear flow)** 是流变学中最基本和最常研究的流动类型。在笛卡尔坐标系 $(x, y, z)$ 中，其理想速度场可以表示为 $\mathbf{v} = (\dot{\gamma} y, 0, 0)$，其中 $\dot{\gamma}$ 是恒定的剪切速率，$x$ 是流动方向，$y$ 是速度梯度方向。

对于这个流动，速度梯度张量 $\nabla \mathbf{v}$ 非常简单 [@problem_id:2925800]：

$$ \nabla \mathbf{v} = \begin{pmatrix} 0  \dot{\gamma}  0 \\ 0  0  0 \\ 0  0  0 \end{pmatrix} $$

由此，我们可以计算出其对称和反对称部分：

$$ \mathbf{D} = \frac{1}{2} \begin{pmatrix} 0  \dot{\gamma}  0 \\ \dot{\gamma}  0  0 \\ 0  0  0 \end{pmatrix}, \quad \mathbf{W} = \frac{1}{2} \begin{pmatrix} 0  \dot{\gamma}  0 \\ -\dot{\gamma}  0  0 \\ 0  0  0 \end{pmatrix} $$

这个结果清晰地表明，简单剪切流既包含纯粹的变形（由非零的 $\mathbf{D}$ 体现），也包含纯粹的旋转（由非零的 $\mathbf{W}$ 体现）。因此，简单剪切流是一种**有旋流 (rotational flow)**。

$\mathbf{D}$ 的本征值被称为**主应变率 (principal strain rates)**，它们表示在某些特定方向（主轴）上流体微元所经历的拉伸或压缩速率。通过求解 $\mathbf{D}$ 的特征方程 $\det(\mathbf{D} - \lambda \mathbf{I}) = 0$，我们得到三个主应变率：$\lambda_1 = \dot{\gamma}/2$（拉伸），$\lambda_2 = -\dot{\gamma}/2$（压缩），以及 $\lambda_3 = 0$ [@problem_id:2925800]。这揭示了在看似简单的剪切背后，实际上存在着沿与流动方向成 $45^\circ$ 角的拉伸和压缩。

#### 拉伸流

与剪切流形成对比的是**拉伸流 (extensional flow)**，这是一类以拉伸变形为主导的无旋流。其中两种重要的类型是单轴拉伸和平面拉伸 [@problem_id:2925851]。

- **单轴拉伸流 (uniaxial extensional flow)**：在一个方向上拉伸，在另外两个垂直方向上对称压缩以保持体积不变。其速度场为 $\mathbf{v} = (\dot{\varepsilon}x, -\frac{\dot{\varepsilon}}{2}y, -\frac{\dot{\varepsilon}}{2}z)$，其中 $\dot{\varepsilon}$ 是拉伸速率。其速度梯度张量和形变速率张量为：
  $$ \nabla \mathbf{v} = \mathbf{D} = \begin{pmatrix} \dot{\varepsilon}  0  0 \\ 0  -\dot{\varepsilon}/2  0 \\ 0  0  -\dot{\varepsilon}/2 \end{pmatrix}, \quad \mathbf{W} = \mathbf{0} $$
  其主应变率即为对角线元素 $\{\dot{\varepsilon}, -\dot{\varepsilon}/2, -\dot{\varepsilon}/2\}$。

- **平面拉伸流 (planar extensional flow)**：在一个方向上拉伸，在另一个垂直方向上以相同速率压缩，而在第三个方向上无变形。其速度场为 $\mathbf{v} = (\dot{\varepsilon}x, -\dot{\varepsilon}y, 0)$。
  $$ \nabla \mathbf{v} = \mathbf{D} = \begin{pmatrix} \dot{\varepsilon}  0  0 \\ 0  -\dot{\varepsilon}  0 \\ 0  0  0 \end{pmatrix}, \quad \mathbf{W} = \mathbf{0} $$
  其主应变率为 $\{\dot{\varepsilon}, -\dot{\varepsilon}, 0\}$。

通过比较这三种流动，我们可以发现深刻的差异 [@problem_id:2925851]。拉伸流是无旋的，而简单剪切流是有旋的。有趣的是，如果我们选择 $\dot{\gamma} = 2\dot{\varepsilon}$，那么简单剪切流的 $\mathbf{D}$ 的本征值将变为 $\{\dot{\varepsilon}, -\dot{\varepsilon}, 0\}$，这与平面拉伸流的本征值完全相同。这意味着仅通过形变速率张量 $\mathbf{D}$ 的不变量（例如迹、行列式等）是无法区分这两种流动的。必须借助涡量张量 $\mathbf{W}$ 来进行区分，这凸显了全面运动学描述的重要性。

为了在不同流动类型之间进行比较，通常会定义一个标量来衡量变形的“强度”，即**广义剪切速率 (generalized shear rate)**，通常定义为 $\dot{\Gamma} \equiv \sqrt{2\mathbf{D}:\mathbf{D}} = \sqrt{2\sum_{i,j}D_{ij}^2}$。对于我们讨论的三种流动，可以计算出 [@problem_id:2925805] [@problem_id:2925851]：
- 简单剪切流：$\dot{\Gamma} = \dot{\gamma}$
- 单轴拉伸流：$\dot{\Gamma} = \sqrt{3}\dot{\varepsilon}$
- 平面拉伸流：$\dot{\Gamma} = 2\dot{\varepsilon}$
这个量为建立不同流动中材料响应的联系提供了基础。

### 剪切流中的材料函数

#### 稳态剪切流

在稳态简单剪切流中，材料的响应通过一系列材料函数来表征。最基本的是**剪切粘度 (shear viscosity)**，$\eta(\dot{\gamma}) = \sigma_{xy}/\dot{\gamma}$，它描述了材料对剪切流动的阻力。对于简单的牛顿流体，其本构关系为 $\boldsymbol{\tau} = 2\eta_0\mathbf{D}$（其中 $\boldsymbol{\tau}$ 是偏应力张量，$\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\tau}$），这预言了粘度是一个常数 $\eta_0$，与剪切速率无关。

然而，对于高分子熔体和浓溶液等复杂流体，情况远非如此。一个显著的特征是**正应力差 (normal stress differences)** 的出现 [@problem_id:2925775]。它们被定义为：
- **第一正应力差 (First Normal Stress Difference)**: $N_1 = \sigma_{xx} - \sigma_{yy}$
- **第二正应力差 (Second Normal Stress Difference)**: $N_2 = \sigma_{yy} - \sigma_{zz}$

对于牛顿流体，由于其偏应力张量 $\boldsymbol{\tau}$ 的对角线元素在简单剪切中均为零，因此 $N_1=0$ 且 $N_2=0$。但对于高分子流体，实验普遍观察到 $N_1  0$ 且 $N_2$ 通常为负，且其绝对值远小于 $N_1$（例如，$-N_2/N_1 \approx 0.1 - 0.3$）。

这些非零正应力差的物理起源在于流动对高分子链的微观作用。在剪切流场中，柔性长链高分子倾向于被拉伸和取向，其长轴平均方向会沿着流动方向 ($x$ 方向)。这种分子尺度的拉伸在宏观上表现为沿流动方向的张力，使得 $\sigma_{xx}$ 显著大于其他方向的正应力，从而导致了正的 $N_1$ [@problem_id:2925775]。

$N_1  0$ 产生了许多独特的非牛顿现象，其中最著名的是 **魏森贝格效应 (Weissenberg effect)** 或爬杆效应。当一根旋转杆插入高分子流体中时，流体不会像牛顿流体那样因离心力而被甩开，反而会沿杆向上爬升。这是因为在旋转剪切流中，$N_1$ 表现为沿流线方向的环向张力（hoop stress）。这种张力产生了一个向内的径向力，必须由一个朝向旋转中心增大的压力梯度来平衡。这个压力梯度支撑流体柱抵抗重力，从而形成爬杆现象 [@problem_id:2925775]。

除了正应力差，高分子流体通常还表现出**剪切变稀 (shear thinning)** 的行为，即剪切粘度 $\eta(\dot{\gamma})$ 随着剪切速率 $\dot{\gamma}$ 的增大而减小。这种现象的微观机理可以通过 **Doi-Edwards 管模型 (Doi-Edwards tube model)** 来理解。该模型认为，在缠结高分子熔体中，一条高分子链（“测试链”）的运动被周围其他链形成的类似“管道”的拓扑约束所限制。在低速流动下，应力松弛主要通过测试链在管道中的“爬行”(reptation) 来实现，其特征时间为爬行时间 $\tau_d$，它与分子量 $M$ 存在强烈的依赖关系，通常为 $\tau_d \sim M^3$。在稳态下，零剪切粘度 $\eta_0$ 与 $\tau_d$ 成正比。

当剪切速率增大时，流动本身会加速周围约束的更新，这种效应被称为**对流约束释放 (convective constraint release, CCR)**。这为应力松弛提供了一个额外的、更快的途径。我们可以将总的松弛速率近似为静态爬行速率和 CCR 速率之和，即 $1/\tau_{\text{eff}} = 1/\tau_d + c\dot{\gamma}$，其中 $c$ 是一个系数。由于稳态粘度与有效松弛时间成正比，即 $\eta(\dot{\gamma}) \propto \tau_{\text{eff}}$，我们可以推导出粘度随剪切速率变化的表达式 [@problem_id:2925853]：

$\eta(\dot{\gamma}) = \frac{G_N^0 \tau_d}{1 + c\dot{\gamma}\tau_d} = \frac{\eta_0}{1 + c\dot{\gamma}\tau_d}$

其中 $G_N^0$ 是平台模量。这个简单的模型成功地捕捉了剪切变稀的本质。剪切变稀的起始点通常定义在 $c\dot{\gamma}\tau_d \approx 1$ 处，即剪切速率的倒数与材料的特征松弛时间相当。这表明剪切变稀的起始剪切速率 $\dot{\gamma}_*$ 与 $\tau_d^{-1}$ 成正比，因此与分子量的关系为 $\dot{\gamma}_* \sim M^{-3}$ [@problem_id:2925853]。

#### 瞬态剪切流与线性粘弹性

除了稳态行为，瞬态响应也包含了关于材料结构和动力学的重要信息。一个典型的瞬态实验是**稳态剪切流的启动 (startup of steady shear)**。对于一个简单的 **Maxwell 模型 (Maxwell model)**，其本构方程为 $\boldsymbol{\tau} + \lambda \frac{d\boldsymbol{\tau}}{dt} = 2\eta\mathbf{D}$，其中 $\lambda$ 是材料的**松弛时间 (relaxation time)**。当在 $t=0$ 时刻突然施加一个恒定的剪切速率 $\dot{\gamma}$，可以解出剪切应力随时间的演化 [@problem_id:2925806]：

$\sigma_{xy}(t) = \eta\dot{\gamma}\left(1 - \exp(-t/\lambda)\right)$

这个结果表明，应力以指数形式增长，并以特征时间 $\lambda$ 趋近其稳态值 $\eta\dot{\gamma}$。这清晰地揭示了松弛时间 $\lambda$ 作为材料响应时间尺度的物理意义。

对于更一般的情况，只要变形足够小，材料的响应可以被**线性粘弹性 (linear viscoelasticity, LVE)** 理论所描述。其核心是**玻尔兹曼叠加原理 (Boltzmann superposition principle)**，它将任意时刻的应力表示为过去所有应变速率历史的加权积分 [@problem_id:2925820]：

$\sigma(t) = \int_{-\infty}^{t} G(t-t') \dot{\gamma}(t') dt'$

其中 $G(t)$ 是材料的**松弛模量 (relaxation modulus)**，它描述了施加一个单位阶跃应变后应力的松弛过程。

**小振幅振荡剪切 (Small-Amplitude Oscillatory Shear, SAOS)** 是研究线性粘弹性的最强大技术。在该实验中，施加一个正弦应变 $\gamma(t) = \gamma_0 \sin(\omega t)$。根据叠加原理，对于线性粘弹性材料，稳态应力响应也必须是同频率的正弦函数，但可能存在一个相位差 $\delta$：$\sigma(t) = \sigma_0 \sin(\omega t + \delta)$。这个响应可以分解为与应变同相和异相（相差 $\pi/2$）的两个部分：

$\sigma(t) = \gamma_0 \left[ G'(\omega)\sin(\omega t) + G''(\omega)\cos(\omega t) \right]$

这里的系数 $G'(\omega)$ 和 $G''(\omega)$ 被称为**储能模量 (storage modulus)** 和**损耗模量 (loss modulus)**。$G'$ 衡量了材料在一个振荡周期内储存并能恢复的弹性能量，代表材料的弹性部分。$G''$ 衡量了以热的形式耗散掉的能量，代表材料的粘性部分。通过对叠加原理中的卷积积分进行傅里叶变换，可以证明这两个模量与松弛模量 $G(t)$ 之间存在如下的积分关系 [@problem_id:2925820]：

$G'(\omega) = \omega \int_0^{\infty} G(s) \sin(\omega s) ds$

$G''(\omega) = \omega \int_0^{\infty} G(s) \cos(\omega s) ds$

为了方便，这些量通常被组合成一个**复数模量 (complex modulus)** $G^*(\omega) = G'(\omega) + iG''(\omega)$。其他相关的量包括：

- **损耗角正切 (loss tangent)**: $\tan\delta = G''/G'$，它表示耗散能量与储存能量的比值。
- **复数粘度 (complex viscosity)**: $\eta^*(\omega) = G^*(\omega)/(i\omega)$。其大小 $|\eta^*(\omega)| = \sqrt{(G'/\omega)^2 + (G''/\omega)^2}$。根据 Cox-Merz 经验法则，对于许多高分子流体，在数值上 $|\eta^*(\omega)|$ 与稳态剪切粘度 $\eta(\dot{\gamma})$ 在 $\omega = \dot{\gamma}$ 时非常接近。

#### 非线性粘弹性：大振幅振荡剪切 (LAOS)

当振荡应变的振幅 $\gamma_0$ 足够大时，材料的响应进入非线性区域，应力响应虽然仍是周期性的，但不再是纯粹的正弦波。这种技术被称为**大振幅振荡剪切 (Large Amplitude Oscillatory Shear, LAOS)** [@problem_id:2925772]。

非线性的出现意味着应力响应中包含了基频 $\omega$ 的**高次谐波 (higher harmonics)**。因此，应力信号可以被表示为一个傅里叶级数：

$\sigma(t) = \sum_{n=1}^{\infty} \sigma_n \sin(n\omega t + \phi_n)$

其中 $\sigma_n$ 和 $\phi_n$ 分别是第 $n$ 次谐波的振幅和相位。这些谐波分量的存在和大小是材料非线性行为的“指纹”。为了从测量的应力-时间数据中提取这些参数，需要进行傅里叶分析。利用三角函数的正交性，我们可以计算出傅里叶系数 $a_n$ 和 $b_n$ [@problem_id:2925772]：

$a_n = \frac{2}{T} \int_0^T \sigma(t) \cos(n\omega t) dt, \quad b_n = \frac{2}{T} \int_0^T \sigma(t) \sin(n\omega t) dt$

然后通过关系式 $\sigma_n = \sqrt{a_n^2 + b_n^2}$ 和 $\phi_n = \mathrm{atan2}(a_n, b_n)$ 来确定谐波振幅和相位。一个有趣的事实是，如果材料具有反转对称性（即 $\sigma(-\gamma, -\dot{\gamma}) = -\sigma(\gamma, \dot{\gamma})$），那么应力响应将具有半波奇对称性 $\sigma(t+T/2) = -\sigma(t)$，这导致所有偶次谐波（$n=2, 4, ...$）的振幅都为零 [@problem_id:2925772]。

### 拉伸流中的材料函数与现象

拉伸流揭示了复杂流体，特别是高分子溶液和熔体的独特且常常是戏剧性的行为。

#### 拉伸粘度与特鲁顿比

在稳态单轴拉伸流中，关键的材料函数是**单轴拉伸粘度 (uniaxial extensional viscosity)**，定义为正应力差与拉伸速率之比 [@problem_id:2925805]：

$\eta_E(\dot{\varepsilon}) = \frac{\sigma_{zz} - \sigma_{rr}}{\dot{\varepsilon}}$

其中 $z$ 是拉伸方向，$r$ 是任意一个横向压缩方向。

**特鲁顿比 (Trouton ratio)**, $Tr = \eta_E/\eta$，是衡量材料在拉伸和剪切中响应差异的指标。对于牛顿流体，可以严格证明 $Tr = 3$。这个结果源于牛顿流体本构关系的线性特性。

然而，对于非牛顿流体，情况要复杂得多。使用**广义牛顿流体 (Generalized Newtonian Fluid, GNF)** 模型（$\boldsymbol{\tau} = 2\eta(\dot{\Gamma})\mathbf{D}$），可以推导出剪切粘度与拉伸粘度之间的普适关系 [@problem_id:2925805]：

$\eta_E(\dot{\varepsilon}) = 3\eta(\sqrt{3}\dot{\varepsilon})$

这个关系非常重要。它表明拉伸粘度不仅是剪切粘度的三倍，而且还取决于在不同（更高）有效速率下的剪切粘度值。对于剪切变稀流体，这意味着 $\eta(\sqrt{3}\dot{\varepsilon})  \eta(\dot{\varepsilon})$。

如果特鲁顿比是按照问题 [@problem_id:2925805] 中的定义 $Tr(\dot{\varepsilon}) \equiv \eta_E(\dot{\varepsilon})/\eta(\dot{\varepsilon})$ 来计算，那么对于 GNF 模型，我们得到 $Tr(\dot{\varepsilon}) = 3\eta(\sqrt{3}\dot{\varepsilon})/\eta(\dot{\varepsilon})$。对于一个幂律流体 $\eta(\dot{\gamma}) = K\dot{\gamma}^{n-1}$，这个比值变为一个常数：$Tr = 3^{(n+1)/2}$。这意味着对于剪切变稀流体 ($n1$)，$Tr  3$；对于剪切增稠流体 ($n1$)，$Tr  3$。这提醒我们，虽然高分子流体通常表现出所谓的“拉伸增稠”（$\eta_E$ 随 $\dot{\varepsilon}$ 增加而增加），但 GNF 模型本身由于其纯粘性的性质，无法捕捉到由弹性引起的这种行为，其预测的特鲁顿比完全由剪切粘度函数的形式决定。

#### 线圈-拉伸转变

高分子溶液在拉伸流中最引人注目的现象是**线圈-拉伸转变 (coil-stretch transition)**。在静止或低速流动中，柔性高分子链以无规线圈的构象存在，以最大化其构象熵。然而，当拉伸流足够强时，它可以克服使链卷曲的熵致回缩力，将高分子链急剧地拉伸成近乎完全伸展的状态。

这个现象可以通过一个简单的**胡克哑铃模型 (Hookean dumbbell model)** 来理论上描述。该模型将高分子链简化为由一个胡克弹簧连接的两个珠子。其构象可以用连接矢量 $\mathbf{Q}$ 的二阶矩张量 $\mathbf{A} \equiv \langle\mathbf{Q}\mathbf{Q}\rangle$ 来表征。在稳态单轴拉伸流中，$\mathbf{A}$ 的演化方程可以求解，得到沿拉伸方向的分量 $A_{11}$ [@problem_id:2925852]：

$A_{11} = \frac{A_0}{1 - 2\lambda\dot{\varepsilon}}$

其中 $A_0$ 是平衡态下的值，$k_B T/H$，$H$ 是弹簧常数，$\lambda$ 是哑铃的松弛时间。从这个解可以看出，当分母趋近于零时，$A_{11}$ 将发散至无穷大。这个临界点发生在：

$\dot{\varepsilon}\lambda = \frac{1}{2}$

这个无量纲乘积，即拉伸速率与松弛时间的乘积，是一个衡量流动强度的**魏森贝格数 (Weissenberg number)**。当它超过临界值 $1/2$ 时，胡克弹簧会被无限拉伸，标志着线圈-拉伸转变的发生。这一转变导致了拉伸粘度的急剧增加，即“拉伸增稠”，这是 GNF 模型无法描述的。

### 流变学中的无量纲数

时间和速率尺度在流变学中至关重要。两个核心的无量纲数——魏森贝格数和德博拉数——帮助我们理解材料响应与外部条件之间的关系 [@problem_id:2925834]。

**魏森贝格数 (Weissenberg number, Wi)** 比较的是材料的特征时间（如松弛时间 $\lambda$）与流动的特征时间（即特征变形速率的倒数）。

$Wi = \lambda \times (\text{特征变形速率})$

例如，在稳态剪切中 $Wi = \lambda\dot{\gamma}$，在单轴拉伸中 $Wi = \lambda\dot{\varepsilon}$。$Wi$ 量化了流动引起的弹性效应的重要性。
- 当 $Wi \ll 1$ 时，流动非常缓慢，材料有足够的时间松弛，其行为接近于粘性流体。
- 当 $Wi \gg 1$ 时，流动非常快，材料来不及松弛，弹性效应占主导，通常会导致显著的非线性行为，如剪切变稀和正应力差。

**德博拉数 (Deborah number, De)** 比较的是材料的特征时间与**实验或观察**的特征时间 $t_{\text{obs}}$。

$De = \frac{\lambda}{t_{\text{obs}}}$

$De$ 判断材料在特定的观察时间尺度下更像固体还是更像液体。
- 当 $De \ll 1$ 时（观察时间远大于松弛时间），材料有足够的时间“流动”，表现出流体特性。
- 当 $De \gg 1$ 时（观察时间远小于松弛时间），材料来不及响应，表现出固体般的弹性。在振荡实验中，$t_{\text{obs}}$ 通常取为振荡周期的倒数，即 $1/\omega$，因此 $De = \lambda\omega$。$De=1$ 标志着从粘性主导到弹性主导行为的转变。

这两个数描述了不同的物理方面。在一个实验中，它们可能同时起作用。例如，在一个持续时间为 $t_{\text{obs}}$ 的剪切启动实验中，$Wi=\lambda\dot{\gamma}$ 描述了最终稳态的性质（是否是高弹性的），而 $De=\lambda/t_{\text{obs}}$ 则描述了瞬态过程的重要性（系统是否能在观察时间内达到稳态）。完全可能存在一个实验，其中 $Wi \gg 1$ （流速很快）同时 $De \ll 1$ （观察时间很长），这意味着我们正在观察一个高度弹性流动在长时间演化后达到的稳态 [@problem_id:2925834]。正确区分和使用这两个无量纲数是理解和预测复杂流体行为的关键。