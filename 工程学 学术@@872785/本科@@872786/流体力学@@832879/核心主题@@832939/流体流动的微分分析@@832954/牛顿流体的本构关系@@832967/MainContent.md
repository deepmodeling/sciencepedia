## 引言
流体如何响应外力？当流体流动时，其内部的力是如何[分布](@entry_id:182848)的？这些是[流体动力学](@entry_id:136788)的核心问题。要回答这些问题，我们必须理解流体[内应力](@entry_id:193721)与[流体变形](@entry_id:271538)速率之间的关系，即**[本构关系](@entry_id:186508)** (constitutive relation)。这一关系是连接抽象的力学概念与可观测的流体运动的桥梁，对于构建和求解控制[流体运动](@entry_id:182721)的数学方程至关重要。然而，对于初学者而言，从直观的“黏稠”感到严谨的数学张量表述，往往存在一条认知上的鸿沟。本文旨在填补这一鸿沟，系统性地阐述最常见的一类流体——[牛顿流体](@entry_id:263796)的本构关系。

在接下来的内容中，我们将分三步深入探索这一主题。在“**原理与机制**”一章中，我们将从流体与固体的对比出发，建立应变率的概念，并从简单的一维[剪切流](@entry_id:266817)逐步推广到普适的三维张量形式，最终展示它如何引出著名的[Navier-Stokes方程](@entry_id:161487)。随后，在“**应用与跨学科连接**”一章中，我们将通过[机械工程](@entry_id:165985)、地球物理、生物医学等多个领域的实例，展示这一基本原理在解决真实世界问题中的强大威力。最后，“**动手实践**”部分提供了一系列计算练习，帮助读者将理论知识转化为解决具体问题的能力。让我们首先进入第一章，探究本构关系的基本原理。

## 原理与机制

在上一章中，我们介绍了[流体力学](@entry_id:136788)的基本概念。现在，我们将深入探讨流体运动的核心动力学原理之一：[应力与应变率](@entry_id:263123)之间的关系。这种关系被称为**本构关系** (constitutive relation)，它定义了特定类型流体的力学行为。本章的重点是**牛顿流体** (Newtonian fluids)，这是一类在工程和自然界中极为常见且重要的流体。理解其本构关系是构建和求解流体运动控制方程（即[Navier-Stokes方程](@entry_id:161487)）的关键一步。

### 从固体到流体：[应变率](@entry_id:154778)的概念

要理解流体的独特性质，最有效的方法之一是将其与我们更熟悉的弹性固体进行对比。想象一个简单的思想实验：将一层薄薄的材料置于两块大的平行平板之间，下板固定，上板可自由移动。

首先，假设该材料是一种理想的**胡克弹性固体** (Hookean elastic solid)。根据胡克定律，[剪切应力](@entry_id:137139) $\tau$ (单位面积上的剪切力) 与产生的剪切应变 $\gamma$ (材料的角变形) 成正比，即 $\tau = G\gamma$，其中 $G$ 是[剪切模量](@entry_id:167228)。当我们对上板施加一个恒定的[剪切应力](@entry_id:137139) $\tau_0$ 时，板会发生位移，材料随之变形。随着应变 $\gamma$ 的增加，材料内部的[反作用](@entry_id:203910)力也随之增大，直到与外加应力相平衡。此时，上板将静止在一个新的平衡位置，其位移是固定的。只要外加应力不变，位移就不再改变。

现在，我们将材料换成一种流体，例如水或油。当我们对上板施加同样的恒定[剪切应力](@entry_id:137139) $\tau_0$ 时，我们会观察到截然不同的现象：上板不会停留在某个固定位移处，而是会以一个恒定的速度持续运动。只要[剪切应力](@entry_id:137139)存在，流体层就会持续变形。

这个对比揭示了流体与固体的根本区别。对于固体，应力与**应变**（变形量）相关联。而对于流体，应力与**[应变率](@entry_id:154778)**（变形的速率）相关联 [@problem_id:1795077]。换言之，流体抵抗的是变形的速率，而非变形本身。当流体静止时，其内部不存在剪切应力（静水压力除外）。只有当流体层之间发生[相对运动](@entry_id:169798)，即流体发生[剪切变形](@entry_id:170920)时，剪切应力才会出现。这种持续变形的运动，我们称之为**流动** (flow)。

### [牛顿黏性定律](@entry_id:144378)：最简情形

[艾萨克·牛顿](@entry_id:175889) ([Isaac Newton](@entry_id:175889)) 最早[对流](@entry_id:141806)体的这种行为进行了量化。他研究了最简单的流动情形之一，即两[平行板](@entry_id:269827)间的**简单[剪切流](@entry_id:266817)** (simple shear flow)，也称为**[库埃特流](@entry_id:260750)** (Couette flow)。

在这种流动中，流体被限制在间距为 $h$ 的两块[平行板](@entry_id:269827)之间。下板静止，上板以恒定速度 $U$ 运动。实验表明，在许多常见流体（如水、空气、油）中，若流动是层流状态，流体的[速度剖面](@entry_id:266404)会呈现线性[分布](@entry_id:182848)，即从下板的零速度线性增加到上板的速度 $U$。

在这种情况下，流体的**[剪切应变率](@entry_id:276945)** (shear strain rate)，通常用 $\dot{\gamma}$ 表示，即流体速度在垂直于流动方向上的梯度。对于线性[速度剖面](@entry_id:266404)，$u(y) = (U/h)y$，该梯度在整个流体层中为常数：
$$
\dot{\gamma} = \frac{du}{dy} = \frac{U}{h}
$$
牛顿发现，维持上板运动所需的[剪切应力](@entry_id:137139) $\tau$ 与这个[剪切应变率](@entry_id:276945)成正比。这个线性关系被称为**[牛顿黏性定律](@entry_id:144378)** (Newton's law of viscosity)：
$$
\tau = \mu \frac{du}{dy} = \mu \dot{\gamma}
$$
这里的比例常数 $\mu$ 被称为**动力黏度** (dynamic viscosity) 或简称**黏度** (viscosity)。黏度是流体的一种内在属性，它量化了流体对剪切变形的抵抗能力。$\mu$ 值越大的流体（如蜂蜜）比 $\mu$ 值较小的流体（如水）更难发生流动，因此感觉上“更黏稠”。

黏度的国际标准单位是帕斯卡-秒 (Pa·s) 或千克每米秒 (kg·m⁻¹·s⁻¹)。通过一个具体的实验设置，我们可以测量流体的黏度。例如，假设两块面积为 $A = 0.750 \text{ m}^2$ 的[平行板](@entry_id:269827)间填充了厚度为 $h = 1.50 \text{ mm}$ 的流体。若施加 $F = 2.25 \text{ N}$ 的水平力使上板以 $v = 0.500 \text{ m/s}$ 的恒定速度运动，我们便可以计算其黏度。首先，剪切应力为 $\tau = F/A = 2.25 / 0.750 = 3.00 \text{ Pa}$。其次，速度梯度为 $du/dy = v/h = 0.500 / (1.50 \times 10^{-3}) \approx 333.3 \text{ s}^{-1}$。根据[牛顿黏性定律](@entry_id:144378)，黏度为 [@problem_id:1775537]：
$$
\mu = \frac{\tau}{du/dy} = \frac{3.00 \text{ Pa}}{333.3 \text{ s}^{-1}} = 0.00900 \text{ Pa}\cdot\text{s}
$$
满足 $\tau \propto \dot{\gamma}$ 关系的流体被称为**牛顿流体**。不满足此[线性关系](@entry_id:267880)的流体则称为**非牛顿流体** (non-Newtonian fluids)，例如牙膏、油漆和血液，它们的行为更为复杂。

### 推广至三维：[应力与应变率](@entry_id:263123)张量

简单的剪切流模型虽然直观，但真实世界的流动通常是复杂的三维运动。为了描述普适的流体运动，我们需要将应力和应变率的概念从标量推广到张量。

**[应力张量](@entry_id:148973) (Stress Tensor)**
在流体内部取一个微小的立方[体元](@entry_id:267802)，作用在其每个面上的力可以分解为垂直于该面的**正向应力** (normal stress) 和平行于该面的**[剪切应力](@entry_id:137139)** (shear stress)。为了完整描述任意方向平面上的应力状态，我们需要一个二阶张量，即**柯西[应力张量](@entry_id:148973)** (Cauchy stress tensor)，记为 $\boldsymbol{\sigma}$。其分量 $\sigma_{ij}$ 表示作用在法向为 $i$ 轴方向的平面上，沿 $j$ 轴方向的应力分量。
*   **对角线分量** ($\sigma_{xx}, \sigma_{yy}, \sigma_{zz}$) 是正向应力。
*   **非对角线分量** ($\sigma_{xy}, \sigma_{yx}, \dots$) 是剪切应力。可以证明，为了满足[力矩平衡](@entry_id:752138)，[应力张量](@entry_id:148973)是对称的，即 $\sigma_{ij} = \sigma_{ji}$。

**应变率张量 (Rate-of-Strain Tensor)**
同样，流体微元的变形速率也需要用一个张量来描述。这个张量被称为**[应变率张量](@entry_id:266108)**或**[形变率张量](@entry_id:184787)** (rate-of-strain tensor)，记为 $\boldsymbol{\varepsilon}$ (在一些文献中也记为 $\mathbf{S}$ 或 $\mathbf{D}$)。其分量定义为：
$$
\varepsilon_{ij} = \frac{1}{2} \left( \frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i} \right)
$$
其中 $u_i$ 是速度矢量 $\mathbf{u}$ 在 $x_i$ 方向的分量。
*   **对角线分量** ($\varepsilon_{xx} = \partial u/\partial x, \dots$) 代表流体元沿坐标轴方向的**拉伸或压缩速率**。
*   **非对角线分量** ($\varepsilon_{xy} = \frac{1}{2}(\partial u/\partial y + \partial v/\partial x), \dots$) 代表流[体元](@entry_id:267802)在相应平面内的**剪切变形速率**（角变形速率的一半）。

**[牛顿流体](@entry_id:263796)的三维[本构关系](@entry_id:186508)**
对于一个**各向同性** (isotropic) 的[牛顿流体](@entry_id:263796)，其[应力张量](@entry_id:148973)和应变率张量之间存在[线性关系](@entry_id:267880)。对于**不可压缩流体** (incompressible fluid)，其密度在流动中保持不变，这意味着流体元的体积变化率为零，即 $\nabla \cdot \mathbf{u} = \varepsilon_{xx} + \varepsilon_{yy} + \varepsilon_{zz} = 0$。在这种条件下，本构关系可以表示为：
$$
\sigma_{ij} = -p\delta_{ij} + 2\mu\varepsilon_{ij}
$$
其中：
*   $p$ 是**静水压力** (hydrostatic pressure)，它是一个[标量场](@entry_id:151443)。$-p\delta_{ij}$ 项代表了即使在流体静止时也存在的[各向同性压力](@entry_id:269937)。$\delta_{ij}$ 是**克罗内克符号** (Kronecker delta)，当 $i=j$ 时为1，否则为0。
*   $\tau_{ij} = 2\mu\varepsilon_{ij}$ 是由[流体运动](@entry_id:182721)产生的**黏性[应力张量](@entry_id:148973)** (viscous stress tensor)。它正比于应变率张量，比例系数为 $2\mu$。

这个张量方程是[牛顿黏性定律](@entry_id:144378)的普适形式。我们可以验证，它包含了之前讨论的简单剪切流情况。对于[库埃特流](@entry_id:260750) $\mathbf{u} = (U y/h, 0, 0)$，唯一非零的[速度梯度](@entry_id:261686)是 $\partial u/\partial y = U/h$。我们来计算[应变率张量](@entry_id:266108)和应力张量的非对角分量 $\varepsilon_{xy}$ 和 $\sigma_{xy}$ [@problem_id:1795116]：
$$
\varepsilon_{xy} = \frac{1}{2} \left( \frac{\partial u}{\partial y} + \frac{\partial v}{\partial x} \right) = \frac{1}{2} \left( \frac{U}{h} + 0 \right) = \frac{U}{2h}
$$
根据[本构关系](@entry_id:186508)（当 $i \neq j$ 时，$\delta_{ij}=0$）：
$$
\sigma_{xy} = -p\delta_{xy} + 2\mu\varepsilon_{xy} = 0 + 2\mu \left( \frac{U}{2h} \right) = \mu \frac{U}{h}
$$
这与我们最初从一维视角得到的 $\tau = \mu(du/dy)$ 完全一致。因此，三维[本构关系](@entry_id:186508)是一个更强大、更通用的框架。

### 黏性应力的类型：[剪切应力](@entry_id:137139)与正向应力

一个常见的误解是认为黏性只产生剪切应力。然而，通用的本构关系 $\tau_{ij} = 2\mu\varepsilon_{ij}$ 告诉我们，只要[应变率张量](@entry_id:266108)的分量不为零，就会有相应的黏性应力分量。这包括正向应力。

**剪切黏性应力**
当流速在某个方向上存在垂直于该方向的梯度时，就会产生剪切黏性应力。[库埃特流](@entry_id:260750)中的 $\sigma_{xy}$ 就是最典型的例子。这种应力源于流体层之间的“摩擦”，并导致能量耗散。例如，为了维持[库埃特流](@entry_id:260750)中上板的恒定速度，外界必须持续做功来克服流体施加的黏性拖曳力。这个功率等于拖曳力与速度的乘积，最终被转化为流体的内能（热量）[@problem_id:1803032]。其表达式为：
$$
P = F \cdot U = (\tau_{yx} A) U = \left(\mu \frac{U}{h}\right) (LW) U = \mu \frac{LW}{h} U^2
$$
其中 $L$ 和 $W$ 是平板的长度和宽度。

**正向黏性应力**
当流[体元](@entry_id:267802)在某个方向上被拉伸或压缩时，即[应变率张量](@entry_id:266108)的对角分量 $\varepsilon_{ii}$ 不为零时，黏性会产生**正向黏性应力**。考虑一个二维**[驻点](@entry_id:136617)流** (stagnation-point flow)，其速度场为 $\mathbf{v} = (kx, -ky, 0)$，其中 $k$ 是一个正常数。这个流场描述了流体流向一个平面并向两侧散开的情形。
流体元在 $x$ 方向被拉伸，其拉伸率为 $\varepsilon_{xx} = \partial u/\partial x = k$。根据本构关系，这会产生一个 $x$ 方向的正向黏性应力 [@problem_id:1794848]：
$$
\tau_{xx} = 2\mu\varepsilon_{xx} = 2\mu k
$$
同理，在 $y$ 方向，流体被压缩，$\varepsilon_{yy} = \partial v/\partial y = -k$，产生的正向黏性应力为 $\tau_{yy} = 2\mu\varepsilon_{yy} = -2\mu k$。

需要强调的是，总的正向应力 $\sigma_{xx}$ 是静水压力和正向黏性应力的总和：$\sigma_{xx} = -p + \tau_{xx}$。在一个更复杂的**纯[拉伸流](@entry_id:198535)** (pure extensional flow) $\mathbf{v} = (\epsilon_0 x, -\epsilon_0 y, 0)$ 中，压力 $p$ 并非[均匀分布](@entry_id:194597)，它会随着位置而变化以平衡流体的惯性力。通过求解动量方程可以得到压[力场](@entry_id:147325)，进而得到总正向应力 [@problem_id:1744156]。这表明，流场中的总应力状态是由压力和黏性效应共同决定的。

### 本构关系在[动量方程](@entry_id:197225)中的作用

本构关系之所以至关重要，是因为它将抽象的应力张量与可测量的速度场联系起来，从而使[流体动力学](@entry_id:136788)的控制方程——[动量守恒](@entry_id:149964)方程——变得“封闭”和可解。

流体运动的**[柯西动量方程](@entry_id:187010)** (Cauchy's momentum equation) 写为：
$$
\rho \frac{D\mathbf{u}}{Dt} = \nabla \cdot \boldsymbol{\sigma} + \rho\mathbf{g}
$$
其中 $\rho$ 是密度, $D/Dt$ 是物质导数, $\mathbf{g}$ 是重力加速度, $\nabla \cdot \boldsymbol{\sigma}$ 是应力[张量的散度](@entry_id:191736)，代表作用在流[体元](@entry_id:267802)上的净[表面力](@entry_id:188034)。在不知道 $\boldsymbol{\sigma}$ 与[速度场](@entry_id:271461) $\mathbf{u}$ 的关系时，这个方程是无法求解的。

现在，我们将不可压缩[牛顿流体](@entry_id:263796)的本构关系 $\sigma_{ij} = -p\delta_{ij} + 2\mu\varepsilon_{ij}$ 代入。应力[张量的散度](@entry_id:191736)项变为：
$$
(\nabla \cdot \boldsymbol{\sigma})_i = \frac{\partial \sigma_{ij}}{\partial x_j} = \frac{\partial}{\partial x_j} (-p\delta_{ij} + 2\mu\varepsilon_{ij}) = -\frac{\partial p}{\partial x_i} + 2\mu \frac{\partial \varepsilon_{ij}}{\partial x_j}
$$
最后一项是黏性力项。将其展开：
$$
2\mu \frac{\partial \varepsilon_{ij}}{\partial x_j} = 2\mu \frac{\partial}{\partial x_j} \left[ \frac{1}{2} \left( \frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i} \right) \right] = \mu \left( \frac{\partial^2 u_i}{\partial x_j \partial x_j} + \frac{\partial}{\partial x_i} \left( \frac{\partial u_j}{\partial x_j} \right) \right)
$$
在矢量形式下，这可以写成 $\mu (\nabla^2 \mathbf{u} + \nabla(\nabla \cdot \mathbf{u}))$。对于不可压缩流体，$\nabla \cdot \mathbf{u} = 0$，因此黏性力项简化为 $\mu \nabla^2 \mathbf{u}$ [@problem_id:1746673]。

将这个结果代回动量方程，我们便得到了著名的**不可压缩牛顿流体的[Navier-Stokes方程](@entry_id:161487)**:
$$
\rho \frac{D\mathbf{u}}{Dt} = -\nabla p + \mu \nabla^2 \mathbf{u} + \rho\mathbf{g}
$$
这个[方程组](@entry_id:193238)（连同连续性方程 $\nabla \cdot \mathbf{u} = 0$）构成了描述水、空气以及许多其他常见[流体运动](@entry_id:182721)的数学基础。[本构关系](@entry_id:186508)是连接基本物理原理（[动量守恒](@entry_id:149964)）和特定材料行为（牛顿黏性）的桥梁。

### [牛顿流体](@entry_id:263796)模型的推广

虽然不可压缩牛顿流体模型应用广泛，但在某些情况下需要考虑更复杂的效应，例如可压缩性和[热力学约束](@entry_id:755911)。

#### [可压缩流体](@entry_id:164617)与体积黏性

当流体密度发生显著变化时（例如在[高速空气动力学](@entry_id:272086)或声学中），不可压缩的假设不再成立。对于**可压缩的各向同性牛顿流体**，其本构关系需要增加一个额外的项来描述与体积变化相关的应力 [@problem_id:1526392]：
$$
\sigma_{ij} = -p\delta_{ij} + \lambda (\nabla \cdot \mathbf{u}) \delta_{ij} + 2\mu \varepsilon_{ij}
$$
或者用张量形式写作：
$$
\boldsymbol{\sigma} = -p\mathbf{I} + \lambda (\nabla \cdot \mathbf{u})\mathbf{I} + 2\mu \boldsymbol{\varepsilon}
$$
与不可压缩情况相比，这里多了一个 $\lambda (\nabla \cdot \mathbf{u}) \delta_{ij}$ 项。其中：
*   $\nabla \cdot \mathbf{u} = \varepsilon_{kk}$ 是流体元的[体积膨胀](@entry_id:144241)率，也称为**散度率** (dilatation rate)。
*   $\lambda$ 是**第二黏度系数** (second coefficient of viscosity)，通常与一个叫做**体积黏度** (bulk viscosity) $K$ (或 $\kappa$) 的量有关，其关系为 $K = \lambda + \frac{2}{3}\mu$。

物理上，动力黏度 $\mu$ 描述了流体对**[等容变形](@entry_id:196451)**（形状改变）的抵抗，而体积黏度 $K$ 描述了流体对**体积变化速率**的抵抗。例如，当声波通过流体时，会引起局部的快速压缩和膨胀，此时体积黏性就会变得很重要，并导致声[波能](@entry_id:164626)量的衰减。对于许多[单原子气体](@entry_id:140562)，可以理论上证明 $K \approx 0$，这引出了所谓的**[斯托克斯假设](@entry_id:195909)** (Stokes' hypothesis) $K=0$ 或 $\lambda = -2/3 \mu$。然而，对于多原子气体和液体，这个假设并不普遍成立，$K$ 是一个独立的、需要通过实验测定的正值。

#### [热力学约束](@entry_id:755911)与黏性耗散

黏度系数 $\mu$ 和 $K$ 是否可以是任意值？答案是否定的。它们受到热力学第二定律的严格约束。

黏性应力在[流体变形](@entry_id:271538)时做功，这个功会不可逆地转化为流体的内能（热量）。这个能量转化的速率，即单位体积的**黏性耗散率** (viscous dissipation rate)，用 $\Phi_v$ 表示，其值为黏性应力张量与[应变率张量](@entry_id:266108)的缩并：$\Phi_v = \tau_{ij}\varepsilon_{ij}$。

[热力学第二定律](@entry_id:142732)要求，在一个孤立系统中，熵永不减少。对于流体流动，这意味着动能向内能的转化过程必须是耗散性的，即 $\Phi_v \ge 0$。这个条件必须对任何可能的流动（即任何可能的[应变率张量](@entry_id:266108) $\boldsymbol{\varepsilon}$）都成立。

将可压缩牛顿流体的本构关系代入[耗散率](@entry_id:748577)表达式，经过一系列张量运算，可以得到一个非常简洁的结果 [@problem_id:1744157]：
$$
\Phi_v = 2\mu \varepsilon'_{ij}\varepsilon'_{ij} + K (\varepsilon_{kk})^2
$$
其中 $\varepsilon'_{ij}$ 是[应变率张量](@entry_id:266108)的偏量部分（描述形状改变），$\varepsilon_{kk}$ 是[应变率张量](@entry_id:266108)的迹（描述体积改变）。这个表达式是两个平方项之和。$\varepsilon'_{ij}\varepsilon'_{ij}$ 和 $(\varepsilon_{kk})^2$ 总是非负的。为了保证 $\Phi_v$ 对所有可能的变形（剪切变形或体积变形）都非负，其系数必须满足：
$$
\mu \ge 0 \quad \text{和} \quad K \ge 0
$$
这个结果从根本上解释了为什么黏度是一种“摩擦”或“阻尼”效应。流体内部的黏性总是消耗[机械能](@entry_id:162989)，而绝不会凭空创造它。这为我们之前建立的数学模型提供了坚实的物理基础。