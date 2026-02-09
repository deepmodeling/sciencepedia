## 引言
在流体力学中，描述流体运动（运动学）与作用于其上的力（动力学）之间的关系是核心任务。动量守恒方程本身不足以封闭求解系统，因为它引入了未知的内部应力。为了解决这一问题，我们需要一个“本构关系”来定义特定材料的力学响应。牛顿流体的本构关系，即应力与应变率之间的线性关系，是描述水、空气等众多常见流体行为的最基本也是最重要的模型。然而，这一看似简单的线性关系背后，蕴含着深刻的物理原理和严谨的数学推导。

本文旨在系统性地剖析牛顿流体的本构关系。在“原理与机制”一章中，我们将从连续介质力学的第一性原理出发，详细推导该本构方程，并阐明剪切黏度与体积黏度的物理内涵。接下来的“应用与交叉学科联系”一章将展示该基本定律如何成为连接工程、热力学、生物力学乃至计算科学的桥梁。最后，“动手实践”部分将通过一系列精心设计的练习，帮助读者将理论知识转化为解决实际问题的能力。让我们首先深入其核心，探讨牛顿流体本构关系的根本原理与机制。

## 原理与机制

本章旨在系统阐述牛顿流体本构关系的理论基础。我们将从流体运动的运动学描述出发，引入变形与应力的概念，然后通过一系列物理公理（如客观性原理和材料对称性）推导出牛顿流体的本构方程。最后，我们将探讨该关系在不同流动条件下的具体形式及其物理意义，并讨论相关的热力学约束。

### 运动学基础：变形率张量与涡量张量

为了描述流体微团在运动过程中的变形和旋转，我们首先需要考察其速度场 $\mathbf{v}(\mathbf{x}, t)$ 的局部变化。这种局部变化完全由**速度梯度张量** $\mathbf{L} = \nabla \mathbf{v}$ 来刻画，其分量形式为 $L_{ij} = \partial v_i / \partial x_j$。任何一个二阶张量都可以唯一地分解为一个对称部分和一个反对称部分。速度梯度张量亦不例外：

$ \mathbf{L} = \mathbf{D} + \mathbf{W} $

其中，对称部分 $\mathbf{D}$ 被称为**变形率张量**（rate-of-deformation tensor），反对称部分 $\mathbf{W}$ 被称为**涡量张量**（vorticity tensor）或自旋张量（spin tensor）。它们的定义如下：

$ \mathbf{D} = \frac{1}{2} \left( \nabla \mathbf{v} + (\nabla \mathbf{v})^{\mathsf{T}} \right) $
$ \mathbf{W} = \frac{1}{2} \left( \nabla \mathbf{v} - (\nabla \mathbf{v})^{\mathsf{T}} \right) $

这一分解具有深刻的物理意义。**变形率张量** $\mathbf{D}$ 描述了流体微团的形状改变（剪切变形）和体积改变（膨胀或压缩）的速率。而**涡量张量** $\mathbf{W}$ 则描述了流体微团的刚性旋转速率。[@problem_id:3944758]

我们可以通过几个典型的流场来直观理解这两个张量的作用：
1.  **刚体旋转**：对于一个绕 $z$ 轴以恒定角速度 $\Omega$ 旋转的流场，其速度为 $\mathbf{v} = (-\Omega y, \Omega x, 0)$。计算可得，其变形率张量 $\mathbf{D} = \mathbf{0}$，而涡量张量 $\mathbf{W}$ 非零，其分量恰好编码了角速度 $\Omega$。这表明该运动是纯旋转，不涉及任何变形。
2.  **均匀各向同性膨胀**：对于速度场 $\mathbf{v} = \alpha \mathbf{x}$（其中 $\alpha$ 为常数），我们发现 $\mathbf{W} = \mathbf{0}$，而 $\mathbf{D} = \alpha \mathbf{I}$（其中 $\mathbf{I}$ 是单位张量）。这代表了纯粹的体积膨胀，没有形状改变或旋转。
3.  **二维简单剪切流**：对于速度场 $\mathbf{v} = (\gamma y, 0, 0)$（其中 $\gamma$ 为剪切率），$\mathbf{D}$ 和 $\mathbf{W}$ 均非零。这表明简单剪切流同时包含了剪切变形和局部旋转。[@problem_id:3944758]

变形率张量的一个至关重要的性质是其迹（trace）。张量的迹是一个不依赖于坐标系选择的标量。通过直接计算可知：

$ \operatorname{tr}(\mathbf{D}) = \operatorname{tr} \left( \frac{1}{2} (\nabla \mathbf{v} + (\nabla \mathbf{v})^{\mathsf{T}}) \right) = \frac{1}{2} (\operatorname{tr}(\nabla \mathbf{v}) + \operatorname{tr}((\nabla \mathbf{v})^{\mathsf{T}})) = \operatorname{tr}(\nabla \mathbf{v}) $

而速度梯度张量的迹正是速度场的散度，即 $\operatorname{tr}(\nabla \mathbf{v}) = \nabla \cdot \mathbf{v}$。因此，我们得到了一个基本恒等式：

$ \operatorname{tr}(\mathbf{D}) = \nabla \cdot \mathbf{v} $

根据雷诺输运定理，对于一个随流体运动的物质体积 $\mathcal{V}(t)$，其体积变化率由以下公式给出：

$ \frac{\mathrm{d}}{\mathrm{d}t} \int_{\mathcal{V}(t)} \mathrm{d}V = \int_{\mathcal{V}(t)} (\nabla \cdot \mathbf{v}) \, \mathrm{d}V $

这表明 $\nabla \cdot \mathbf{v}$ 正是局部的**体积膨胀率**。因此，$\operatorname{tr}(\mathbf{D})$ 直接量化了流体微团体积的变化速率。对于**不可压缩流**，其定义就是物质微团的体积保持不变，这意味着 $\nabla \cdot \mathbf{v} = 0$，从而其变形率张量必然是无迹的，即 $\operatorname{tr}(\mathbf{D}) = 0$。[@problem_id:4082494]

### 柯西应力张量与本构关系

流体内部的相互作用力通过**应力**来描述。作用在流体内任意假想面上的接触力（traction）$\mathbf{t}$ 与该面的法向单位矢量 $\mathbf{n}$ 之间存在线性关系，这个关系由**柯西应力张量**（Cauchy stress tensor）$\boldsymbol{\sigma}$ 定义：

$ \mathbf{t} = \boldsymbol{\sigma} \cdot \mathbf{n} $

在没有体力矩或力偶应力的情况下，角动量守恒定律要求柯西应力张量必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$。[@problem_id:4082441] 这一对称性意味着，由表面力在任意物质体积上产生的净力矩为零。

流体静止时，应力是各向同性的，仅表现为静水压力 $p_0$。当流体运动时，黏性效应会产生额外的应力。因此，通常将柯西应力张量分解为一个各向同性的**压力**部分和一个由流动引起的**黏性应力张量**（viscous stress tensor）$\boldsymbol{\tau}$：

$ \boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\tau} $

这里的 $p$ 是热力学压力，$\mathbf{I}$ 是单位张量。由于 $\boldsymbol{\sigma}$ 和 $-p\mathbf{I}$ 都是对称的，$\boldsymbol{\tau}$ 也必须是对称张量。

**本构关系**（constitutive relation）的根本任务就是建立“刺激”与“响应”之间的数学关系。在流体力学中，“刺激”是流体的变形（由变形率张量 $\mathbf{D}$ 描述），“响应”是由此产生的黏性应力 $\boldsymbol{\tau}$。牛顿流体模型正是基于一系列物理公理来确定 $\boldsymbol{\tau}$ 和 $\mathbf{D}$ 之间关系的一种最简单、最普适的模型。

### 牛顿流体本构关系的推导

我们基于以下三个基本公理来推导适用于一大类流体（包括水和空气）的本构方程。

1.  **线性**：黏性应力 $\boldsymbol{\tau}$ 与变形率张量 $\mathbf{D}$ 之间是线性关系。这适用于变形率不太极端的大多数常见情况。

2.  **材料各向同性**（Isotropy）：流体的物理性质不依赖于方向。这意味着本构关系本身在空间旋转下保持不变。

3.  **物质坐标系无关性**（Material Frame-Indifference），或称**客观性**（Objectivity）：物理定律（包括本构关系）不应依赖于观察者的刚体运动。这意味着，如果一个观察者相对于另一个观察者正在进行平移和旋转，他们所观察到的本构关系形式必须完全相同。

客观性原理对本构关系的形式施加了极强的约束。可以证明，在观察者坐标系变换下，变形率张量 $\mathbf{D}$ 是**客观的**，其变换规律为 $\mathbf{D}^* = \mathbf{Q}\mathbf{D}\mathbf{Q}^{\mathsf{T}}$（其中 $\mathbf{Q}(t)$ 是描述坐标系旋转的正交张量）。然而，涡量张量 $\mathbf{W}$ 却**不是客观的**，其变换规律为 $\mathbf{W}^* = \mathbf{Q}\mathbf{W}\mathbf{Q}^{\mathsf{T}} + \dot{\mathbf{Q}}\mathbf{Q}^{\mathsf{T}}$。附加项 $\dot{\mathbf{Q}}\mathbf{Q}^{\mathsf{T}}$ 代表了观察者自身的旋转速率，它是一个任意的反对称张量。由于黏性应力 $\boldsymbol{\tau}$ 作为一个可测量的物理量必须是客观的，它不能依赖于非客观的量 $\mathbf{W}$。因此，**黏性应力只能是变形率张量的函数**：$\boldsymbol{\tau} = \boldsymbol{f}(\mathbf{D})$。[@problem_id:4082469] 这一结论也可以从物理上理解：流体在纯刚体旋转时（$\mathbf{D}=\mathbf{0}, \mathbf{W}\neq\mathbf{0}$），不应产生任何黏性应力，因此 $\boldsymbol{\tau}$ 不能依赖于 $\mathbf{W}$。[@problem_id:4082469]

综合以上三个公理，我们需要寻找一个将对称二阶张量 $\mathbf{D}$ 线性、各向同性地映射到另一个对称二阶张量 $\boldsymbol{\tau}$ 的函数。根据张量表示定理，满足这些条件的最一般的函数形式为：

$ \boldsymbol{\tau} = \lambda \operatorname{tr}(\mathbf{D}) \mathbf{I} + 2\mu \mathbf{D} $

这就是**可压缩牛顿流体的本构关系**。[@problem_id:4082456] 方程中的两个标量系数是材料参数：
*   $\mu$ 是**剪切黏度**（shear viscosity），也称动力黏度（dynamic viscosity），它衡量流体抵抗剪切变形（形状改变）的能力。其国际单位是帕斯卡-秒（$\mathrm{Pa \cdot s}$）。
*   $\lambda$ 是**第二黏度系数**（second coefficient of viscosity），它与流体抵抗体积变形的能力有关。其单位也是 $\mathrm{Pa \cdot s}$。

这个方程以简洁的张量形式，统一描述了流体对各种变形模式的响应。

### 体积黏度与热力学约束

上述本构关系引入了两个独立的黏度系数。为了更好地理解它们的物理意义，特别是 $\lambda$ 的作用，我们引入**体积黏度**（bulk viscosity）的概念。

首先，我们区分**热力学压力** $p$ 和**机械压力** $p_{\text{mech}}$。机械压力定义为法向应力的平均值（带负号），即 $p_{\text{mech}} = -\frac{1}{3} \operatorname{tr}(\boldsymbol{\sigma})$。将本构关系代入柯西应力张量的定义中：

$ \boldsymbol{\sigma} = -p\mathbf{I} + \lambda \operatorname{tr}(\mathbf{D}) \mathbf{I} + 2\mu \mathbf{D} $

对其求迹可得：

$ \operatorname{tr}(\boldsymbol{\sigma}) = -3p + \lambda \operatorname{tr}(\mathbf{D}) \operatorname{tr}(\mathbf{I}) + 2\mu \operatorname{tr}(\mathbf{D}) = -3p + (3\lambda + 2\mu)\operatorname{tr}(\mathbf{D}) $

于是，机械压力与热力学压力之间的关系为：

$ p_{\text{mech}} = -\frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma}) = p - \left(\lambda + \frac{2}{3}\mu\right) \operatorname{tr}(\mathbf{D}) $

我们定义括号中的组合为**体积黏度** $\zeta$：

$ \zeta = \lambda + \frac{2}{3}\mu $

因此，$p_{\text{mech}} = p - \zeta (\nabla \cdot \mathbf{v})$。[@problem_id:4082470] 这表明，只有在流体静止或体积不变（$\nabla \cdot \mathbf{v}=0$）时，机械压力才等于热力学压力。在可压缩流动中，体积黏度 $\zeta$ 导致了这两种压力之间的差异，这种差异正比于体积膨胀（或压缩）的速率。体积黏度 $\zeta$ 量化了流体在经历快速体积变化时由于内部弛豫过程（如分子内能态的重新分布）而产生的耗散。[@problem_id:4082440]

历史上，Stokes曾假设 $\zeta=0$，即**Stokes假设**。这等价于 $\lambda = -\frac{2}{3}\mu$。[@problem_id:4082442] 经典气体动理论表明，对于单原子理想气体，该假设是成立的。然而，对于多原子气体和大多数液体，由于存在分子振动、转动等内部能量模式，其能量平衡弛豫需要时间，导致了不可忽略的体积黏度。因此，Stokes假设并非普遍成立，在许多现代流体动力学问题（如声波衰减、激波结构）中，必须考虑非零的体积黏度。[@problem_id:4082442]

黏度系数并非任意，它们必须满足热力学第二定律。该定律要求，在等温过程中，黏性耗散产生的熵必须为非负。黏性耗散率 $\Phi_v$（单位体积的机械能转化为内能的速率）由 $\Phi_v = \boldsymbol{\tau} : \mathbf{D}$ 给出。将本构关系代入并整理，可以得到：

$ \Phi_v = 2\mu (\mathbf{D}' : \mathbf{D}') + \zeta (\operatorname{tr}(\mathbf{D}))^2 $

其中 $\mathbf{D}' = \mathbf{D} - \frac{1}{3}\operatorname{tr}(\mathbf{D})\mathbf{I}$ 是变形率张量的无迹（剪切）部分。上式是两个平方项之和，要保证 $\Phi_v \ge 0$ 对任何可能的变形（即任意的 $\mathbf{D}'$ 和 $\operatorname{tr}(\mathbf{D})$）都成立，其系数必须为非负。这就得出了对黏度系数的热力学约束：[@problem_id:1744157]

$ \mu \ge 0 \quad \text{and} \quad \zeta \ge 0 $

### 特殊情况与应用

#### 不可压缩流体

许多流体力学问题涉及**不可压缩流体**，其定义为密度沿流线保持不变，对于均匀流体即 $\nabla \cdot \mathbf{v} = 0$。如前所述，这意味着 $\operatorname{tr}(\mathbf{D}) = 0$。在此条件下，可压缩牛顿流体的本构关系显著简化：

$ \boldsymbol{\tau} = 2\mu \mathbf{D} $

在这种情况下，黏性应力张量 $\boldsymbol{\tau}$ 是纯粹的 deviatoric（无迹）张量。第二黏度系数 $\lambda$ 和体积黏度 $\zeta$ 在本构关系中不再出现，对流动没有影响。[@problem_id:4082442] 此时，柯西应力张量为 $\boldsymbol{\sigma} = -p\mathbf{I} + 2\mu\mathbf{D}$。值得注意的是，对于不可压缩流，压力 $p$ 不再是热力学状态量（即不能通过状态方程从密度和温度确定），而变成一个力学量。它的作用是作为拉格朗日乘子，其场分布由动量方程决定，以确保速度场在任何时候都满足 $\nabla \cdot \mathbf{v} = 0$ 这一运动学约束。[@problem_id:4082470]

#### 典型流动分析

不可压缩牛顿流体模型在简单流动中会产生一些标志性的结果。
*   **简单剪切流** $\mathbf{v} = (\dot{\gamma} y, 0, 0)$：
    计算表明，唯一的非零黏性应力分量是剪切应力 $\tau_{xy} = \mu \dot{\gamma}$。所有的法向黏性应力分量（$\tau_{xx}, \tau_{yy}, \tau_{zz}$）均为零。这意味着牛顿流体在剪切中不会产生垂直于剪切方向的额外推力或拉力。因此，其**第一法向应力差** $N_1 = \sigma_{xx} - \sigma_{yy} = 0$ 和**第二法向应力差** $N_2 = \sigma_{yy} - \sigma_{zz} = 0$。这与非牛顿流体（如聚合物溶液）形成鲜明对比，后者通常会表现出非零的法向应力差（Weissenberg效应）。[@problem_id:4082481]

*   **单轴拉伸流** $\mathbf{v} = (\dot{\varepsilon} x, -\frac{1}{2}\dot{\varepsilon} y, -\frac{1}{2}\dot{\varepsilon} z)$：
    这是一种保持体积不变的拉伸流动。计算可得黏性法向应力为 $\tau_{xx} = 2\mu\dot{\varepsilon}$，$\tau_{yy} = \tau_{zz} = -\mu\dot{\varepsilon}$。定义**拉伸黏度** $\eta_E$ 为拉伸方向的法向应力差与拉伸率之比，即 $\eta_E = (\sigma_{xx} - \sigma_{yy})/\dot{\varepsilon}$。对于牛顿流体，我们得到 $\eta_E = (\tau_{xx} - \tau_{yy})/\dot{\varepsilon} = (2\mu\dot{\varepsilon} - (-\mu\dot{\varepsilon}))/\dot{\varepsilon} = 3\mu$。这个比值 $\eta_E/\mu = 3$ 被称为**Trouton比**，是牛顿流体的一个普适常数。[@problem_id:4082481]

#### 声波衰减

体积黏度的物理效应在可压缩流动中最为显著，一个经典例子是声波在流体中的衰减。对可压缩Navier-Stokes方程进行线性化分析可以表明，黏性是声波能量耗散并导致其振幅衰减的原因之一。若忽略热传导效应，平面声波的振幅衰减系数 $\alpha$ 与频率 $\omega$ 的平方成正比，且正比于一个有效黏度：

$ \alpha \propto \omega^2 \left( \zeta + \frac{4}{3}\mu \right) $

这个组合 $\zeta + \frac{4}{3}\mu$ 被称为**纵向黏度**（longitudinal viscosity），它决定了流体对纯压缩波动的总阻力。这个结果清晰地表明，体积黏度 $\zeta$ 和剪切黏度 $\mu$ 共同对声波衰减做出贡献。对于许多体积黏度远大于剪切黏度的流体，$\zeta$ 是声波衰减的主要原因。这也为实验测量体积黏度提供了一种主要途径。[@problem_id:4082440]