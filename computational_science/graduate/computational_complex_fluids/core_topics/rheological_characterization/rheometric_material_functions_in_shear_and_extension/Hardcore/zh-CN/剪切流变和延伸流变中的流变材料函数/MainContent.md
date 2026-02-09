## 引言
复杂流体，如聚合物熔体、悬浮液和生物流体，在流动中表现出与简单牛顿流体截然不同的复杂力学行为，例如剪切变稀、弹性效应和拉伸硬化。为了精确量化和预测这些现象，流变学建立了一套标准的材料函数。然而，理解这些函数如何从流动的基本运动学中派生，它们如何揭示材料的微观结构信息，以及它们如何在实际工程和科学问题中得到应用，是掌握计算复杂流体领域的关键挑战。本文旨在系统性地填补这一知识空白，为读者提供一个关于剪切和拉伸流变学的全面框架。

在接下来的内容中，我们将分步构建这一理解。**第一章“原理与机制”**将深入探讨剪切流和拉伸流的运动学基础，严格定义剪切粘度、法向应力差和拉伸粘度等核心材料函数，并展示如何通过Oldroyd-B等本构模型从微观物理层面推导这些宏观响应。**第二章“应用与跨学科联系”**将视野转向实践，探讨这些函数的实验测量技术、潜在的伪影，并通过在材料科学、工程和生物医学领域的实例，展示流变学原理的广泛应用。最后，在**第三章“动手实践”**中，您将通过具体的计算问题，亲手推导和应用关键的流变学关系，从而巩固所学知识。让我们首先从定义流变行为的基础——流动运动学开始。

## 原理与机制

为了量化复杂流体在流动中的力学响应，流变学建立了一套基于两种标准流动类型的材料函数：剪切流和拉伸流。本章将深入探讨这些流动的运动学基础，严格定义相应的流变材料函数，并阐明它们与流体微观结构及本构模型之间的深刻联系。

### 流变流动的运动学基础

所有流体行为的分析都始于对其运动的数学描述。流体运动在空间中的局部变化由**速度梯度张量** $\nabla \mathbf{v}$ 来表征，其分量为 $(\nabla \mathbf{v})_{ij} = \partial v_i / \partial x_j$。根据经典的柯西-斯托克斯分解（Cauchy-Stokes decomposition），任何速度梯度张量都可以唯一地分解为一个对称部分和一个反对称部分：

$\nabla \mathbf{v} = \mathbf{D} + \mathbf{W}$

这里的 $\mathbf{D}$ 是**形变速率张量**（rate-of-deformation tensor），定义为 $\mathbf{D} = \frac{1}{2}(\nabla \mathbf{v} + (\nabla \mathbf{v})^{\top})$。它描述了流体微元的拉伸、压缩和剪切变形速率。$\mathbf{W}$ 是**涡量张量**（vorticity tensor），定义为 $\mathbf{W} = \frac{1}{2}(\nabla \mathbf{v} - (\nabla \mathbf{v})^{\top})$。它描述了流体微元的刚性旋转速率。这种分解至关重要，因为它揭示了任何流动都可被视为变形与旋转的叠加。

#### 简单剪切流

在流变学中，**简单剪切流**（simple shear flow）是最基本和最常见的测试流动。其理想速度场在笛卡尔坐标系中可以表示为 $v_x = \dot{\gamma} y$, $v_y = 0$, $v_z = 0$，其中 $\dot{\gamma}$ 是恒定的剪切速率。

对于这个流动，我们可以直接计算其运动学张量[@problem_id:4102318]：
速度梯度张量 $\nabla \mathbf{v}$ 只有一个非零分量 $(\nabla \mathbf{v})_{xy} = \dot{\gamma}$，因此其矩阵形式为：
$$
\nabla \mathbf{v} = \begin{pmatrix} 0 & \dot{\gamma} & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix}
$$

形变速率张量 $\mathbf{D}$ 和涡量张量 $\mathbf{W}$ 分别为：
$$
\mathbf{D} = \frac{1}{2} \begin{pmatrix} 0 & \dot{\gamma} & 0 \\ \dot{\gamma} & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix}
$$
$$
\mathbf{W} = \frac{1}{2} \begin{pmatrix} 0 & \dot{\gamma} & 0 \\ -\dot{\gamma} & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix}
$$

这一结果明确表明，简单剪切流同时包含变形（由 $\mathbf{D}$ 体现）和旋转（由 $\mathbf{W}$ 体现）。实际上，变形和旋转的幅度是相等的。这种旋转的存在使得剪切流在拉伸聚合物分子等微观结构时效率相对较低，因此常被称为“弱流”（weak flow）。

#### 拉伸流

与剪切流相对的是**拉伸流**（extensional flows），也称为**无旋流**（irrotational flows），因为它们的涡量张量 $\mathbf{W}$ 为零。这意味着流体微元只经历纯粹的变形而没有刚性旋转。由于缺乏旋转，拉伸流能够非常有效地拉伸和取向流体中的微观结构（如聚合物链），因此被称为“强流”（strong flow）。

主要有三种标准的拉伸流模式，它们可以通过形变速率张量 $\mathbf{D}$ 在其主轴坐标系中的对角元（特征值）来定义。对于不可压缩流体，体积守恒要求 $\nabla \cdot \mathbf{v} = \mathrm{tr}(\mathbf{D}) = 0$。设 $\dot{\epsilon} > 0$ 为特征拉伸速率，则三种模式的 $\mathbf{D}$ 张量如下[@problem_id:4102361]：

*   **单轴拉伸 (Uniaxial Extension)**：在一个方向上拉伸，在另外两个垂直方向上对称压缩。
    $$
    \mathbf{D} = \mathrm{diag}(\dot{\epsilon}, -\dot{\epsilon}/2, -\dot{\epsilon}/2)
    $$

*   **平面拉伸 (Planar Extension)**：在一个方向上拉伸，在一个垂直方向上压缩，在第三个方向上保持不变。
    $$
    \mathbf{D} = \mathrm{diag}(\dot{\epsilon}, -\dot{\epsilon}, 0)
    $$

*   **双轴拉伸 (Biaxial Extension)**：在两个垂直方向上等量拉伸，在第三个方向上压缩以保持体积不变。
    $$
    \mathbf{D} = \mathrm{diag}(\dot{\epsilon}, \dot{\epsilon}, -2\dot{\epsilon})
    $$

这些理想化的流动构成了定义核心流变材料函数的基础。

### 剪切流中的材料函数

为了表征流体对剪切变形的响应，我们定义了一系列不依赖于具体仪器和几何形状的材料函数。对于不可压缩流体，其**柯西应力张量**（Cauchy stress tensor）$\boldsymbol{\sigma}$ 可以写成：
$\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\tau}$
其中 $p$ 是一个任意的**各向同性压力**（isotropic pressure），$\mathbf{I}$ 是单位张量，$\boldsymbol{\tau}$ 是**偏应力张量**（deviatoric stress tensor），它完全由流体的本构关系决定。由于 $p$ 的任意性，任何可测量的物理量都必须独立于 $p$。这通过使用应力分量的差值来实现。

在稳态简单剪切流中，定义了三个关键的材料函数[@problem_id:4102373]：

1.  **剪切粘度 (Shear Viscosity)**, $\eta(\dot{\gamma})$：
    $$
    \eta(\dot{\gamma}) = \frac{\sigma_{xy}}{\dot{\gamma}}
    $$
    剪切粘度衡量流体抵抗剪切流动的能力。对于牛顿流体，$\eta$ 是一个常数；而对于非牛顿流体，它通常是剪切速率的函数（例如，剪切变稀或剪切增稠）。

2.  **第一法向应力差 (First Normal Stress Difference)**, $N_1(\dot{\gamma})$：
    $$
    N_1(\dot{\gamma}) = \sigma_{xx} - \sigma_{yy}
    $$
    $N_1$ 是流动方向（$x$）和速度梯度方向（$y$）上的法向应力之差。对于聚合物溶液等弹性流体，$N_1$ 通常为正，这导致了**魏森贝格效应**（Weissenberg effect），即弹性流体在剪切时会产生沿流线方向的张力，使得流体倾向于“爬杆”。

3.  **第二法向应力差 (Second Normal Stress Difference)**, $N_2(\dot{\gamma})$：
    $$
    N_2(\dot{\gamma}) = \sigma_{yy} - \sigma_{zz}
    $$
    $N_2$ 是梯度方向（$y$）和中性或涡量方向（$z$）上的法向应力之差。$N_2$ 通常比 $N_1$ 小得多，其符号和大小也提供了关于材料微观结构的宝贵信息。

这三个函数 $\eta(\dot{\gamma})$, $N_1(\dot{\gamma})$, 和 $N_2(\dot{\gamma})$ 共同构成了对材料在稳态剪切下的完整流变学描述。

### 拉伸流中的材料函数

与剪切流类似，我们也为拉伸流定义材料函数以表征其独特的响应。最重要的函数是**拉伸粘度**（extensional viscosity）。

对于沿 $z$ 轴的单轴拉伸，**单轴拉伸粘度**（uniaxial extensional viscosity）$\eta_E(\dot{\epsilon})$ 的标准定义是拉伸方向上的净张应力与拉伸速率之比。净张应力是拉伸方向的法向应力与横向法向应力的平均值之差。这个定义确保了结果与各向同性压力 $p$ 无关[@problem_id:4102381]：
$$
\eta_E(\dot{\epsilon}) = \frac{\sigma_{zz} - \frac{1}{2}(\sigma_{xx} + \sigma_{yy})}{\dot{\epsilon}}
$$
由于单轴拉伸的轴对称性，横向应力相等，即 $\sigma_{xx} = \sigma_{yy}$，因此定义可以简化为 $\eta_E(\dot{\epsilon}) = (\sigma_{zz} - \sigma_{xx})/\dot{\epsilon}$。

拉伸粘度与剪切粘度的比值被称为**特鲁顿比**（Trouton's ratio），$\mathrm{Tr} = \eta_E / \eta_0$，其中 $\eta_0$ 是零剪切粘度。对于牛顿流体，这个比值是一个常数，其值取决于流动类型[@problem_id:4102361]：
*   单轴拉伸: $\mathrm{Tr} = 3$
*   平面拉伸: $\mathrm{Tr} = 4$
*   双轴拉伸: $\mathrm{Tr} = 6$

对于非牛顿流体，特鲁顿比可以远大于这些牛顿值，并且强烈依赖于拉伸速率，这种现象被称为“拉伸硬化”（strain hardening），是弹性效应的显著标志。

### 时间尺度的作用：粘性与弹性行为

复杂流体区别于简单牛顿流体的核心在于它们具有“记忆”，即当前的应力状态不仅取决于当前的变形速率，还取决于其过去的变形历史。这种记忆的特征时间尺度被称为**弛豫时间**（relaxation time），记为 $\lambda$。非牛顿行为的出现本质上是流体内在的弛豫时间 $\lambda$ 与流动施加的特征时间尺度之间竞争的结果。

为了量化这种竞争，我们引入了两个关键的无量纲数[@problem_id:4102313]：

1.  **魏森贝格数 (Weissenberg Number)**, $\mathrm{Wi}$：
    $\mathrm{Wi}$ 定义为材料弛豫时间与流动特征时间的倒数（即特征变形速率）之比：$\mathrm{Wi} = \lambda \times (\text{characteristic strain rate})$。
    *   在剪切流中：$\mathrm{Wi} = \lambda \dot{\gamma}$
    *   在拉伸流中：$\mathrm{Wi} = \lambda \dot{\epsilon}$
    $\mathrm{Wi}$ 衡量了稳态流动中弹性效应的相对重要性。当 $\mathrm{Wi} \ll 1$ 时，材料有足够的时间在变形之间完全弛豫，其行为接近粘性流体。当 $\mathrm{Wi} \gtrsim 1$ 时，材料来不及完全弛豫，弹性效应（如法向应力差、拉伸硬化）变得显著。

2.  **德博拉数 (Deborah Number)**, $\mathrm{De}$：
    $\mathrm{De}$ 定义为材料弛豫时间与外部观察或过程时间 $T$ 之比：$\mathrm{De} = \lambda / T$。
    $\mathrm{De}$ 用于表征瞬态或非稳态过程。例如，在流动的启动过程中，如果观察时间 $T$ 很短（$\mathrm{De} \gg 1$），材料会表现出类似固体的弹性行为。如果观察时间很长（$\mathrm{De} \ll 1$），材料则表现出类似液体的粘性行为。

在实验中，我们不仅关心稳态响应，也关心从静止状态达到稳态的过程。**瞬态材料函数**（transient material functions），如剪切应力增长粘度 $\eta^+(t, \dot{\gamma})$ 和拉伸应力增长粘度 $\eta_E^+(t, \dot{\epsilon})$，描述了这一过程。根据定义，当时间趋于无穷时，这些瞬态函数将收敛到相应的稳态材料函数[@problem_id:4102354]：
$$
\lim_{t \to \infty} \eta^+(t, \dot{\gamma}) = \eta(\dot{\gamma})
$$
$$
\lim_{t \to \infty} \eta_E^+(t, \dot{\epsilon}) = \eta_E(\dot{\epsilon})
$$

### 从微观结构到宏观函数：本构模型

材料函数是通过实验测量的宏观响应，而**本构参数**（constitutive parameters）是理论模型中代表材料内在属性（如分子量、链刚度等）的固定常数。一个成功的本构模型应该能够利用一套固定的本构参数，预测出材料在所有不同流动条件下的材料函数[@problem_id:4102319]。

#### 案例研究 1：Oldroyd-B 模型

Oldroyd-B 模型是描述聚合物稀溶液的经典模型，它将流体视为牛顿溶剂和弹性（胡克）哑铃（代表聚合物链）的混合物。

*   **在剪切流中**：通过求解该模型的本构方程，可以推导出其在稳态简单剪切下的材料函数[@problem_id:4102305]。结果表明：
    *   剪切粘度 $\eta$ 是一个常数，等于溶剂粘度 $\eta_s$ 和聚合物贡献粘度 $\eta_p$ 之和。
    *   第一法向应力差 $N_1 = 2 \eta_p \lambda \dot{\gamma}^2$，与剪切速率的平方成正比。
    *   第二法向应力差 $N_2 = 0$。
    这个结果意义重大：尽管 Oldroyd-B 模型未能预测剪切变稀行为（这是一个局限），但它成功地捕捉到了非牛顿流体的一个核心特征——由弹性引起的非零法向应力差。

*   **在拉伸流中**：当我们将 Oldroyd-B 模型应用于单轴拉伸流时，会得到一个惊人的结果[@problem_id:4102295]。其拉伸粘度 $\eta_E$ 表达式为：
    $$
    \eta_E(\dot{\epsilon}) = 3\eta_s + \frac{3\eta_p}{(1 - 2\lambda\dot{\epsilon})(1 + \lambda\dot{\epsilon})}
    $$
    这个表达式显示，当拉伸速率达到一个临界值 $\dot{\epsilon}_c = 1/(2\lambda)$ 时，分母变为零，导致拉伸粘度发散至无穷大。这种非物理的发散是胡克哑铃模型（弹簧可以无限伸长）的直接后果，但它正确地预示了物理上真实存在的**线圈-拉伸转变**（coil-stretch transition）。在强拉伸流中，当 $\mathrm{Wi} = \lambda\dot{\epsilon}$ 接近 $1/2$ 时，聚合物链会从无规线团突然转变为高度伸展的状态，导致应力急剧增加。这一结果鲜明地揭示了“弱”剪切流和“强”拉伸流对聚合物构象截然不同的影响。

#### 案例研究 2：有限可伸长性的修正 (FENE-P 模型)

Oldroyd-B 模型的拉伸粘度发散问题可以通过引入更符合物理现实的假设来解决。真实的聚合物链长度是有限的。**FENE-P (Finitely Extensible Nonlinear Elastic–Peterlin)** 模型通过修正胡克定律，使得弹簧力在接近最大伸长时急剧增大，从而引入了**有限可伸长性**。

这个修正在数学上通过一个依赖于聚合物构象张量 $\mathbf{C}$ 的迹（即聚合物链的平均伸长程度）的 Peterlin 因子 $f(\mathbf{C}) = 1 / (1 - \mathrm{tr}\mathbf{C}/b)$ 来实现，其中 $b$ 是最大可伸长性参数[@problem_id:4102322]。

*   **在拉伸流中**：当拉伸速率增大，聚合物链被拉伸，$\mathrm{tr}\mathbf{C}$ 增加。这导致 $f(\mathbf{C})$ 因子也随之增大。在 Oldroyd-B 模型中导致发散的项（在 FENE-P 模型中变为 $f - 2\lambda\dot{\epsilon}$）由于 $f$ 的动态增长而永远不会变为零。因此，有限可伸长性**“正则化”**了拉伸粘度，消除了发散。

取而代之的是，在极高的拉伸速率下，拉伸粘度会趋于一个有限的高原值，该值正比于最大可伸长性参数 $b$：
$$
\eta_E(\dot{\epsilon} \to \infty) \approx 3\eta_s + 2G\lambda b
$$
其中 $G$ 是弹性模量。这个结果表明，可拉伸性越强的聚合物（$b$ 越大），其在高拉伸速率下的粘度也越高。当 $b \to \infty$ 时，FENE-P 模型退化为 Oldroyd-B 模型，高原值也随之消失，恢复了发散行为。

从牛顿流体到 Oldroyd-B 模型，再到 FENE-P 模型，这一系列发展清晰地展示了流变学研究的核心思路：通过实验测量宏观材料函数，启发我们构建能够捕捉这些行为的微观物理图像和数学本构模型，并通过不断修正模型使其更贴近物理现实，从而更准确地预测和理解复杂流体的行为。