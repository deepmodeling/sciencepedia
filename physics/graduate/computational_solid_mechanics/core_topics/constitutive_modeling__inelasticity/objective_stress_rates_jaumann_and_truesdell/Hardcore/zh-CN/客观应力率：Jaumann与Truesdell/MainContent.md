## 引言
在处理大变形问题时，例如金属成型、橡胶部件的拉伸或地质材料的流动，我们必须在当前变形构形下描述材料的力学行为。这要求本构关系能够联系应力的变化率和材料的变形率。然而，一个根本性的挑战随之而来：直接使用柯西应力张量的材料时间导数会与连续介质力学的基石——客观性原理（或称材料无差异原理）——相冲突。这意味着，由不同（相对旋转的）观察者测量的应力率会包含非物理性的旋转效应，导致本构定律依赖于观察者，这是物理上不可接受的。

本文旨在系统性地解决这一知识空白，深入探讨“客观应力率”这一核心概念。我们将带领读者穿越有限变形理论的复杂性，揭示为何需要客观率，以及它们是如何被构建出来的。

- 在“**原理与机制**”章节中，我们将从第一性原理出发，阐明柯西应力率的非客观性，并详细推导两种最经典的客观应力率：基于共旋思想的**Jaumann率**和基于拖曳变换的**Truesdell率**。本章将揭示它们背后的物理与运动学图像，并辨析次弹性与超弹性之间的关键区别。
- 接下来，在“**应用与交叉学科联系**”章节中，我们将展示选择不同客观率所带来的截然不同的物理预测，例如在简单剪切流中的病态振荡行为。我们将探讨这些选择如何影响数值算法的稳定性和效率，并将其应用扩展到岩土力学、流变学和塑性力学等交叉学科领域。
- 最后，通过“**动手实践**”部分，读者将有机会通过具体的计算练习，亲手验证Jaumann率和Truesdell率在不同运动条件下的行为，从而将抽象的理论转化为深刻的物理直觉。

通过本文的学习，您将不仅掌握Jaumann率和Truesdell率的数学定义，更能深刻理解它们在现代计算固体力学中的理论地位、应用场景及内在局限性，为您的研究和工程实践提供坚实的理论基础。

## 原理与机制

在有限变形分析中，本构关系必须在欧拉描述（空间描述）下建立，以联系应力率和变形率。然而，正如我们在引言中所述，简单地使用柯西（Cauchy）应力张量的材料时间导数会引发与观察者无关性（或称客观性）原理的冲突。本章旨在深入探讨这一挑战的根源，并系统地介绍为解决此问题而发展的关键概念——客观应力率。我们将重点阐述两种最经典的客观应力率：Jaumann率和Truesdell率，分析它们的物理和运动学基础，并揭示它们在计算固体力学本构模型中的应用与局限性。

### 客观性原理与材料时间导数的非客观性

连续介质力学的基本公理之一是**材料无差异原理（Principle of Material Frame Indifference）**，或称**客观性原理（Principle of Objectivity）**。该原理指出，材料的本构响应（即应力与变形之间的关系）必须独立于观察者。不同的观察者可以通过一个叠加的刚体运动联系起来。在任意时刻 $t$，一个观察者（我们称之为主观察者）测量的空间点 $\boldsymbol{x}$ 与另一个（星号）观察者测量的点 $\boldsymbol{x}^*$ 之间的关系可以表示为：
$$
\boldsymbol{x}^*(t) = \boldsymbol{c}(t) + \boldsymbol{Q}(t)\boldsymbol{x}(t)
$$
其中，$\boldsymbol{c}(t)$ 是一个时变平移向量，$\boldsymbol{Q}(t)$ 是一个时变真三维正交张量（$\boldsymbol{Q}^T\boldsymbol{Q} = \boldsymbol{I}$, $\det\boldsymbol{Q} = +1$），代表一个刚体旋转。

根据这一定理，一个物理量如果是客观的，其在不同观察者坐标系下的分量必须遵循特定的张量变换法则。例如，二阶柯西应力张量 $\boldsymbol{\sigma}$ 是一个客观张量，其变换规律为：
$$
\boldsymbol{\sigma}^* = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T
$$
然而，在本构关系中，我们通常需要应力的“率”。最直接的率是**材料时间导数（material time derivative）**，它表示跟随一个物质点（质点）测量的物理量的变化率。对于一个任意的空间张量场 $\boldsymbol{A}(\boldsymbol{x},t)$，其材料时间导数 $\dot{\boldsymbol{A}}$ 定义为：
$$
\dot{\boldsymbol{A}} = \frac{\partial \boldsymbol{A}}{\partial t} + (\nabla \boldsymbol{A})\boldsymbol{v}
$$
其中 $\frac{\partial \boldsymbol{A}}{\partial t}$ 是局部导数（固定空间点的变化率），$(\nabla \boldsymbol{A})\boldsymbol{v}$ 是对流项，$\boldsymbol{v}$ 是速度场。

问题在于，柯西应力张量的材料时间导数 $\dot{\boldsymbol{\sigma}}$ 并不是一个客观张量。我们可以通过考察其在叠加刚体运动下的变换规律来证明这一点。对 $\boldsymbol{\sigma}^* = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T$ 两边求材料时间导数，并应用乘法法则，得到：
$$
\dot{\boldsymbol{\sigma}}^* = \dot{\boldsymbol{Q}}\boldsymbol{\sigma}\boldsymbol{Q}^T + \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^T + \boldsymbol{Q}\boldsymbol{\sigma}\dot{\boldsymbol{Q}}^T
$$
如果 $\dot{\boldsymbol{\sigma}}$ 是客观的，其变换规律应为 $\dot{\boldsymbol{\sigma}}^* = \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^T$。然而，上式中多出了 $\dot{\boldsymbol{Q}}\boldsymbol{\sigma}\boldsymbol{Q}^T$ 和 $\boldsymbol{Q}\boldsymbol{\sigma}\dot{\boldsymbol{Q}}^T$ 这两项。只要叠加的运动包含旋转（即 $\dot{\boldsymbol{Q}} \neq \boldsymbol{0}$），这两项就不为零。这表明，柯西应力张量的材料时间导数 $\dot{\boldsymbol{\sigma}}$ 包含了由于观察者自身的旋转而产生的非物理性部分，因此它不是一个客观的物理量 [@problem_id:3597665]。

因此，我们的核心任务是构建一个新的应力率，我们称之为**客观应力率**，并用 $\mathring{\boldsymbol{\sigma}}$ 表示。根据定义，这个新的率必须是一个客观的二阶张量，即它必须在任何叠加刚体运动下都满足变换关系 [@problem_id:2666106]：
$$
\mathring{\boldsymbol{\sigma}}^* = \boldsymbol{Q}\mathring{\boldsymbol{\sigma}}\boldsymbol{Q}^T
$$
这确保了基于该率建立的本构方程能够满足材料无差异原理。

### 运动学的分解：变形率与自旋

为了构建客观应力率，我们必须首先精确地分解材料的局部运动。所有信息都包含在**速度梯度张量（velocity gradient tensor）** $\boldsymbol{L}$ 中，它定义为速度场 $\boldsymbol{v}$ 的空间梯度：
$$
\boldsymbol{L} = \nabla \boldsymbol{v} \quad (L_{ij} = \frac{\partial v_i}{\partial x_j})
$$
速度梯度张量 $\boldsymbol{L}$ 可以唯一地分解为其对称和反对称部分之和：
$$
\boldsymbol{L} = \boldsymbol{D} + \boldsymbol{W}
$$
其中：
- **变形率张量（rate-of-deformation tensor）** $\boldsymbol{D}$ 是 $\boldsymbol{L}$ 的对称部分：
  $$
  \boldsymbol{D} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^T)
  $$
  $\boldsymbol{D}$ 描述了材料微元的拉伸、压缩和剪切变形速率。

- **自旋张量（spin tensor）** 或涡量张量（vorticity tensor） $\boldsymbol{W}$ 是 $\boldsymbol{L}$ 的反对称部分：
  $$
  \boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^T)
  $$
  $\boldsymbol{W}$ 描述了材料微元的平均刚体转动角速度。

为了直观理解这一分解，考虑一个纯刚体转动的情形。其速度场可以表示为 $\boldsymbol{v}(\boldsymbol{x},t) = \dot{\boldsymbol{Q}}(t)\boldsymbol{Q}(t)^T\boldsymbol{x}$，其中 $\boldsymbol{Q}(t)$ 是旋转张量。在这种情况下，速度梯度 $\boldsymbol{L} = \dot{\boldsymbol{Q}}\boldsymbol{Q}^T$。由于 $\boldsymbol{Q}$ 是正交的，可以证明 $\dot{\boldsymbol{Q}}\boldsymbol{Q}^T$ 是一个反对称张量。因此，对于纯刚体转动，我们有 $\boldsymbol{D}=\boldsymbol{0}$ 且 $\boldsymbol{W}=\boldsymbol{L}$。这清晰地表明，此时的运动完全由自旋描述，没有任何变形发生 [@problem_id:3585724]。

### 主要的客观应力率类别

构造客观应力率的本质，是从非客观的材料时间导数 $\dot{\boldsymbol{\sigma}}$ 中减去由刚体转动引起的非物理性部分。实现这一目标的途径不止一种，从而产生了不同类别的客观应力率。这些类别反映了对“如何追踪和移除转动”的不同几何与物理诠释 [@problem_id:3585764]。

#### 同转率：Jaumann率

同转（corotational）方法的基本思想是，在一个与材料微元一同旋转的（非惯性）坐标系中去测量应力的变化率。这个“同转”坐标系的转动角速度被认为是材料的**自旋（spin）**，由自旋张量 $\boldsymbol{W}$ 描述。从旋转坐标系理论可知，在一个以角速度张量 $\boldsymbol{W}$ 旋转的坐标系中观察到的张量 $\boldsymbol{\sigma}$ 的变化率，与固定坐标系中的材料导数 $\dot{\boldsymbol{\sigma}}$ 之间，通过李氏括号（Lie bracket）或交换子（commutator）相关联。这便引出了**Jaumann率**（也称Jaumann-Zaremba率）的定义：
$$
\boldsymbol{\sigma}^{\nabla J} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}
$$
这里的修正项 $\boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}$ 精确地抵消了由于观察者自身的旋转而导致的 $\dot{\boldsymbol{\sigma}}$ 的非客观部分，从而使得 $\boldsymbol{\sigma}^{\nabla J}$ 成为一个客观张量 [@problem_id:3581301]。

Jaumann率的一个重要特性是，对于一个只经历刚体转动而无变形（即 $\boldsymbol{D}=\boldsymbol{0}$）的应力场，它为零。在这种情况下，应力张量只是随着物体一起转动，其在本构意义上并未发生“变化”。数学上，当 $\boldsymbol{D}=\boldsymbol{0}$ 时，应力张量满足 $\boldsymbol{\sigma}(t) = \boldsymbol{Q}(t)\boldsymbol{\sigma}_0\boldsymbol{Q}(t)^T$，其材料导数为 $\dot{\boldsymbol{\sigma}} = \boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}$。代入Jaumann率的定义，我们得到 $\boldsymbol{\sigma}^{\nabla J} = \boldsymbol{0}$ [@problem_id:2905914] [@problem_id:3585755]。这证实了Jaumann率在纯转动下表现出期望的物理行为。

#### 拖曳率：Truesdell率

拖曳（convected）方法则源于一种不同的几何图像。它不引入一个显式的旋转坐标系，而是基于张量随材料流动的“拖曳”变换。其基本思想是：
1.  将当前构形下的柯西应力张量 $\boldsymbol{\sigma}$ 通过变形梯度 $\boldsymbol{F}$ **拉回（pull-back）** 到初始参考构形，得到一个参考构形下的张量（例如第二Piola-Kirchhoff应力张量 $\boldsymbol{S}$）。
2.  在不旋转、不形变的参考构形中，张量的材料时间导数（如 $\dot{\boldsymbol{S}}$）是天然客观的。
3.  再将这个客观的率**推前（push-forward）** 回到当前构形，从而定义一个当前构形下的客观应力率。

遵循这一流程，可以定义**Truesdell率**。对于柯西应力张量 $\boldsymbol{\sigma}$，其Truesdell率 $\boldsymbol{\sigma}^{\nabla T}$ 的表达式为 [@problem_id:3581301]：
$$
\boldsymbol{\sigma}^{\nabla T} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{L}^T + (\text{tr}\boldsymbol{D})\boldsymbol{\sigma}
$$
与Jaumann率不同，Truesdell率的定义中包含了完整的速度梯度张量 $\boldsymbol{L}$，而非仅仅其反对称部分 $\boldsymbol{W}$。这是因为“拖曳”操作不仅涉及转动，还涉及材料微元的变形，这两者都包含在 $\boldsymbol{L}$ 中。

值得注意的是，Truesdell率与基尔霍夫（Kirchhoff）应力张量 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$（其中 $J=\det\boldsymbol{F}$ 是体积变化率）的Oldroyd率密切相关。可以证明，$\boldsymbol{\sigma}^{\nabla T} = J^{-1} (\dot{\boldsymbol{\tau}} - \boldsymbol{L}\boldsymbol{\tau} - \boldsymbol{\tau}\boldsymbol{L}^T)$ [@problem_id:2709106]。这个关系在讨论超弹性理论时至关重要。

在纯刚体转动（$\boldsymbol{D}=\boldsymbol{0}$, $\boldsymbol{L}=\boldsymbol{W}$）的特殊情况下，$\text{tr}\boldsymbol{D}=0$，$\boldsymbol{L}^T = -\boldsymbol{L}$，Truesdell率的表达式简化为 $\boldsymbol{\sigma}^{\nabla T} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{L}$，这与Jaumann率的形式完全相同。因此，在这种简单情况下，两种率是一致的 [@problem_id:2905914]。但在一般变形情况下，两者存在差异，其差值为：
$$
\boldsymbol{\sigma}^{\nabla T} - \boldsymbol{\sigma}^{\nabla J} = - (\boldsymbol{D}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{D}) + (\text{tr}\boldsymbol{D})\boldsymbol{\sigma}
$$
这个差值显式地依赖于变形率张量 $\boldsymbol{D}$ [@problem_id:2709106]。

### 本构模型与计算应用

客观应力率是构建有限变形下率形式本构关系的基础。这类模型通常被称为**亚弹性（hypoelastic）**模型，其一般形式为：
$$
\mathring{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}
$$
其中 $\mathring{\boldsymbol{\sigma}}$ 是某个选择的客观应力率，$\mathbb{C}$ 是一个四阶弹性模量张量。

#### 亚弹性与超弹性

在这里，必须强调一个至关重要的区别：**客观性**与**能量守恒**是两个独立的物理要求。客观性是运动学上的要求，保证本构律的表达形式与观察者无关。而能量守恒，对于纯弹性材料而言，要求应力功必须是某个储能函数 $\psi$ 的全微分，即 $\boldsymbol{\sigma}:\boldsymbol{D} = \dot{\psi}$。满足后一条件的材料称为**超弹性（hyperelastic）**材料，其应力可以从一个势函数（储能函数）中导出。

一个亚弹性模型，即便其形式是客观的（例如，当 $\mathbb{C}$ 为各向同性时），通常却不满足可积性条件，即无法从一个储能函数中导出。这意味着，对于一个封闭的变形路径（变形终态与初态相同），亚弹性模型预测的净功 $\oint \boldsymbol{\sigma}:\boldsymbol{D} dt$ 可能不为零。这代表了虚假的能量产生或耗散，与纯弹性材料的物理本质相悖 [@problem_id:3552803]。

#### Jaumann率的病态行为

尽管Jaumann率在概念上很直观，但将其用于亚弹性模型时，会在某些变形模式下导致非物理的“病态”行为。最著名的例子是**单剪切（simple shear）**流动。考虑一个速度场为 $v_1 = \dot{\gamma}x_2$ 的平面单剪切流动，其中剪切率 $\dot{\gamma}$ 为常数。在这种情况下，变形率张量 $\boldsymbol{D}$ 和自旋张量 $\boldsymbol{W}$ 都是常数。

如果我们采用基于Jaumann率的线性各向同性亚弹性模型 $\boldsymbol{\sigma}^{\nabla J} = 2\mu\boldsymbol{D}$，并从零应力状态开始积分，可以精确求解出应力随时间的演化。求解结果表明，剪切应力 $\sigma_{12}$ 和法向应力 $\sigma_{11}, \sigma_{22}$ 都会随剪切应变 $\gamma = \dot{\gamma}t$ 的增加而呈现周期性振荡 [@problem_id:3585737]。例如，剪切应力为：
$$
\sigma_{12}(t) = \mu \sin(\dot{\gamma}t)
$$
这个结果是完全非物理的：在持续的剪切作用下，材料的抵抗力（剪切应力）并不会单调增加，而是在一个范围内振荡。这种病态行为的根源在于，单剪切运动中恒定的自旋 $\boldsymbol{W}$ 使得Jaumann率所依赖的“同转”坐标系不断旋转，导致应力张量相对于变形的物质微元发生了不真实的“翻滚” [@problem_id:2709106]。

#### Truesdell率与超弹性的联系

尽管亚弹性模型存在理论缺陷，但率形式的本构方程在计算力学中（尤其是在增量求解的更新拉格朗日（Updated Lagrangian）框架中）是不可或缺的。关键的洞察在于，如果我们从一个热力学上一致的超弹性模型（即从一个储能函数 $W$ 出发）开始，可以推导出其**唯一**且**一致**的率形式本构关系。

这个一致的率形式恰好与Truesdell率（或等价地，基尔霍夫应力的Oldroyd率）相关。也就是说，对于一个超弹性材料，其客观应力率与变形率之间的关系 $\mathring{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$ 天然地采取了以Truesdell率为基础的形式，并且其中的模量张量 $\mathbb{C}$ 不再是常数，而是可以从储能函数 $W$ 推导出的当前状态的函数。

因此，在计算固体力学中，当需要在率形式下实现一个超弹性模型时，采用Truesdell率是理论上最可靠的选择。它保证了数值积分算法所逼近的是一个真实存在的、路径无关的、能量守恒的响应（在时间步长趋于零的极限下）[@problem_id:2709106]。这使得Truesdell率相较于Jaumann率，在描述弹性材料时具有更深刻的物理基础，而不仅仅是一个运动学上的构造。