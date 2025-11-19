## 引言
[刚体运动](@entry_id:193355)是描述物体在空间中移动而不产生任何内部变形的理想化模型，它是连续介质力学乃至整个物理学中的一个基石概念。然而，它的重要性远不止于分析刚性物体的动力学。在研究可变形固体时，一个核心的挑战是如何将物体的真实变形从其整体的空间运动中剥离出来。若无法准确界定和处理刚体运动，我们便无法建立独立于观察者的、物理上一致的材料本构关系，也无法开发出在任意大转动下依然稳健可靠的数值计算方法。本文正是为了填补这一认知上的关键环节，为读者构建一个关于刚体运动的完整理论与应用图景。

在接下来的内容中，我们将通过三个章节逐步深入。首先，在“原理与机制”一章中，我们将从第一性原理出发，严格定义刚体运动，推导其速度和[加速度场](@entry_id:266595)，并揭示其背后优美的代数[群结构](@entry_id:146855)（SE(3)）。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章，我们将探讨这些原理如何在连续介质力学、有限元方法、[动力学控制](@entry_id:154879)以及机器人学和计算机图形学等领域中发挥关键作用，展示理论与实践的紧密结合。最后，在“动手实践”部分，我们提供了一系列精心设计的计算问题，引导读者通过编程实践，将抽象的理论转化为解决实际问题的能力。

## 原理与机制

在本章中，我们将深入探讨[刚体运动](@entry_id:193355)的运动学原理与数学机制。刚体运动是连续介质力学中的一个基本概念，它描述了物体在不发生任何内部变形的情况下的空间运动。理解刚体运动不仅是研究更复杂变形问题的基础，而且对于确保[计算模型](@entry_id:152639)在不同观测[参考系](@entry_id:169232)下的一致性（即客观性）至关重要。我们将从刚体运动的基本定义出发，逐步推导出其速度和[加速度场](@entry_id:266595)，揭示其[代数结构](@entry_id:137052)，并探讨其在线性化和本构关系中的深刻意义。

### 刚体运动的定义与[运动学](@entry_id:173318)描述

从物理直觉出发，**[刚体运动](@entry_id:193355)（rigid body motion）**最根本的特征是它保持物体内任意两点间的距离不变。假设一个连续体在参考构型中的物[质点](@entry_id:186768)由位置向量 $\boldsymbol{X}$ 描述，在时刻 $t$ 的当前构型中，其位置为 $\boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{X}, t)$。那么，刚体运动的定义可以精确地表述为：对于物体中任意一对物[质点](@entry_id:186768) $\boldsymbol{X}_1$ 和 $\boldsymbol{X}_2$，在任意时刻 $t$，它们在当前构型中的距离始终等于它们在参考构型中的距离。用数学语言表达即：

$$
\|\boldsymbol{\chi}(\boldsymbol{X}_1, t) - \boldsymbol{\chi}(\boldsymbol{X}_2, t)\| = \|\boldsymbol{X}_1 - \boldsymbol{X}_2\|
$$

为了探究这一几何约束对运动本身的限制，我们考虑两个无限接近的物质点 $\boldsymbol{X}$ 和 $\boldsymbol{X} + d\boldsymbol{X}$。它们之间的向量为 $d\boldsymbol{X}$。在当前构型中，这两个点被映射到 $\boldsymbol{x}$ 和 $\boldsymbol{x} + d\boldsymbol{x}$，其中 $d\boldsymbol{x}$ 是连接它们的向量。根据**变形梯度（deformation gradient）** $\boldsymbol{F} = \frac{\partial \boldsymbol{\chi}}{\partial \boldsymbol{X}}$ 的定义，我们有 $d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$。距离保持不变的条件意味着 $\|d\boldsymbol{x}\|^2 = \|d\boldsymbol{X}\|^2$。将其写为[内积](@entry_id:158127)形式：

$$
(d\boldsymbol{x}) \cdot (d\boldsymbol{x}) = (d\boldsymbol{X}) \cdot (d\boldsymbol{X})
$$

将 $d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$ 代入上式，得到：

$$
(\boldsymbol{F} d\boldsymbol{X}) \cdot (\boldsymbol{F} d\boldsymbol{X}) = d\boldsymbol{X} \cdot (\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} d\boldsymbol{X}) = d\boldsymbol{X} \cdot d\boldsymbol{X}
$$

整理后可得 $d\boldsymbol{X} \cdot [(\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} - \boldsymbol{I})d\boldsymbol{X}] = 0$，其中 $\boldsymbol{I}$ 是二阶单位张量。由于这个关系对任意向量 $d\boldsymbol{X}$ 都必须成立，这意味着方括号中的[对称张量](@entry_id:148092)必须为零张量。因此，我们得到了一个至关重要的结论：

$$
\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = \boldsymbol{I}
$$

这个等式表明，对于[刚体运动](@entry_id:193355)，变形梯度 $\boldsymbol{F}$ 必须是一个**正交张量（orthogonal tensor）**。

在连续介质力学中，**右柯西-格林变形张量（right Cauchy-Green deformation tensor）** $\boldsymbol{C}$ 被定义为 $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$。因此，对于[刚体运动](@entry_id:193355)，我们有 $\boldsymbol{C} = \boldsymbol{I}$。这直接导致**[格林-拉格朗日应变张量](@entry_id:187745)（Green-Lagrange strain tensor）** $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I})$ 恒等于零。这从[运动学](@entry_id:173318)上证实了刚体内部没有任何应变或拉伸 [@problem_id:3596971] [@problem_id:3596973]。

除了保持距离，物理上真实的运动还必须保持物体的朝向，防止发生类似[镜面反射](@entry_id:270785)的反转。这一要求通过规定变形梯度的[行列式](@entry_id:142978)为正来实现，即 $J = \det(\boldsymbol{F}) > 0$。对于一个正交张量 $\boldsymbol{F}$，我们知道 $(\det \boldsymbol{F})^2 = \det(\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}) = \det(\boldsymbol{I}) = 1$，这意味着 $\det(\boldsymbol{F})$ 只能是 $+1$ 或 $-1$。因此，保持朝向的条件迫使我们选择 $\det(\boldsymbol{F}) = +1$。一个同时满足 $\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = \boldsymbol{I}$ 和 $\det(\boldsymbol{F}) = +1$ 的张量被称为**真[旋转张量](@entry_id:191990)（proper orthogonal tensor）**或**[旋转张量](@entry_id:191990)（rotation tensor）**。所有三维旋转张量的集合构成了**[特殊正交群](@entry_id:146418) [SO(3)](@entry_id:138200)** [@problem_id:3597022]。

根据[连续介质运动学](@entry_id:747813)的相容性定理，如果一个连通体的变形梯度在每一点都是正交的，那么该变形梯度在空间上必须是均匀的，即 $\boldsymbol{F}$ 不依赖于物[质点](@entry_id:186768)的位置 $\boldsymbol{X}$。因此，我们可以写出 $\boldsymbol{F}(\boldsymbol{X}, t) = \boldsymbol{R}(t)$，其中 $\boldsymbol{R}(t) \in \mathrm{SO}(3)$ 是一个仅依赖于时间的[旋转张量](@entry_id:191990)。对 $\frac{\partial \boldsymbol{\chi}}{\partial \boldsymbol{X}} = \boldsymbol{R}(t)$ 关于 $\boldsymbol{X}$ 进行积分，我们便得到了[刚体运动](@entry_id:193355)最一般的数学表达式：

$$
\boldsymbol{x}(\boldsymbol{X}, t) = \boldsymbol{R}(t)\boldsymbol{X} + \boldsymbol{c}(t)
$$

其中 $\boldsymbol{R}(t)$ 描述了刚体随时间的旋转，而 $\boldsymbol{c}(t)$ 是一个随时间变化的平移向量，代表了刚体上某一点（此处为参考构型原点）的运动轨迹 [@problem_id:35975] [@problem_id:3596971]。这个表达式清晰地将刚体运动分解为一个旋转和一个平移的叠加。

### [刚体运动](@entry_id:193355)的运动学：速度与加速度

基于刚体运动的表达式 $\boldsymbol{x}(t) = \boldsymbol{R}(t)\boldsymbol{X} + \boldsymbol{c}(t)$，我们可以推导出刚体上任意物质点的速度和加速度。由于物[质点](@entry_id:186768) $\boldsymbol{X}$ 在参考构型中是固定的，其对时间的导数为零。因此，速度 $\boldsymbol{v}$ 是 $\boldsymbol{x}$ 对时间的导数：

$$
\boldsymbol{v}(t) = \dot{\boldsymbol{x}}(t) = \dot{\boldsymbol{R}}(t)\boldsymbol{X} + \dot{\boldsymbol{c}}(t)
$$

这个表达式虽然正确，但它混合了物质坐标 $\boldsymbol{X}$ 和时间导数。在实际应用中，我们通常更关心以当前位置 $\boldsymbol{x}$ 表示的速度场，即[欧拉描述](@entry_id:264722)。为此，我们首先需要引入**[角速度](@entry_id:192539)（angular velocity）**的概念。

[旋转张量](@entry_id:191990) $\boldsymbol{R}(t)$ 满足正交条件 $\boldsymbol{R}(t)\boldsymbol{R}(t)^{\mathsf{T}} = \boldsymbol{I}$。对该式关于时间求导，我们得到：

$$
\dot{\boldsymbol{R}}\boldsymbol{R}^{\mathsf{T}} + \boldsymbol{R}\dot{\boldsymbol{R}}^{\mathsf{T}} = \boldsymbol{0}
$$

令 $\boldsymbol{W} = \dot{\boldsymbol{R}}\boldsymbol{R}^{\mathsf{T}}$，上式可以写为 $\boldsymbol{W} + \boldsymbol{W}^{\mathsf{T}} = \boldsymbol{0}$，即 $\boldsymbol{W}^{\mathsf{T}} = -\boldsymbol{W}$。这表明 $\boldsymbol{W}(t)$ 是一个**[反对称张量](@entry_id:199349)（skew-symmetric tensor）**，它被称为**空间角速度张量**。在三维空间中，任何一个[反对称张量](@entry_id:199349) $\boldsymbol{W}$ 都可以与一个唯一的**轴向量（axial vector）** $\boldsymbol{\omega}$ 相关联，使得对于任意向量 $\boldsymbol{y}$，它们的关系为 $\boldsymbol{W}\boldsymbol{y} = \boldsymbol{\omega} \times \boldsymbol{y}$。向量 $\boldsymbol{\omega}$ 就是我们通常所说的空间[角速度](@entry_id:192539)向量 [@problem_id:3596976]。

现在，我们可以重写速度表达式。从[运动方程](@entry_id:170720) $\boldsymbol{x} = \boldsymbol{R}\boldsymbol{X} + \boldsymbol{c}$ 中解出 $\boldsymbol{X} = \boldsymbol{R}^{\mathsf{T}}(\boldsymbol{x} - \boldsymbol{c})$，并代入速度公式：

$$
\boldsymbol{v}(t) = \dot{\boldsymbol{R}}[\boldsymbol{R}^{\mathsf{T}}(\boldsymbol{x} - \boldsymbol{c})] + \dot{\boldsymbol{c}}(t) = (\dot{\boldsymbol{R}}\boldsymbol{R}^{\mathsf{T}})(\boldsymbol{x} - \boldsymbol{c}) + \dot{\boldsymbol{c}}(t) = \boldsymbol{W}(\boldsymbol{x} - \boldsymbol{c}) + \dot{\boldsymbol{c}}(t)
$$

利用轴向量的[等价关系](@entry_id:138275)，我们得到[速度场](@entry_id:271461)的标准形式：

$$
\boldsymbol{v}(t) = \dot{\boldsymbol{c}}(t) + \boldsymbol{\omega}(t) \times (\boldsymbol{x}(t) - \boldsymbol{c}(t))
$$

这个公式（也称为欧拉速度方程）表明，刚体上任意一点的速度是平移速度 $\dot{\boldsymbol{c}}(t)$ 和绕[瞬时旋转中心](@entry_id:200491)点 $\boldsymbol{c}(t)$ 的旋转速度 $\boldsymbol{\omega} \times (\boldsymbol{x} - \boldsymbol{c})$ 的矢量和 [@problem_id:3597034]。

对速度场再次求导，我们可以得到[加速度场](@entry_id:266595) $\boldsymbol{a}(t) = \dot{\boldsymbol{v}}(t)$。运用链式法则和向量积的[求导法则](@entry_id:145443)，可以得到：

$$
\boldsymbol{a}(t) = \ddot{\boldsymbol{c}}(t) + \dot{\boldsymbol{\omega}}(t) \times (\boldsymbol{x}(t) - \boldsymbol{c}(t)) + \boldsymbol{\omega}(t) \times (\boldsymbol{\omega}(t) \times (\boldsymbol{x}(t) - \boldsymbol{c}(t)))
$$

这个加速度表达式由三部分组成：
1.  **[平动](@entry_id:187700)加速度** $\ddot{\boldsymbol{c}}(t)$：与参考点 $\boldsymbol{c}(t)$ 的加速度相同，对刚体上所有点都一样。
2.  **[切向加速度](@entry_id:173884)** $\dot{\boldsymbol{\omega}}(t) \times (\boldsymbol{x}(t) - \boldsymbol{c}(t))$：由[角速度](@entry_id:192539)的变化（[角加速度](@entry_id:177192) $\dot{\boldsymbol{\omega}}$）引起。
3.  **向心加速度** $\boldsymbol{\omega}(t) \times (\boldsymbol{\omega}(t) \times (\boldsymbol{x}(t) - \boldsymbol{c}(t)))$：由[角速度](@entry_id:192539)本身引起，始终指向瞬时[旋转轴](@entry_id:187094)。

值得注意的是，对于刚体运动，其**变形率张量（rate-of-deformation tensor）** $\boldsymbol{D}$（即[空间速度梯度](@entry_id:187198) $\boldsymbol{L}=\nabla_{\boldsymbol{x}}\boldsymbol{v}$ 的对称部分）恒为零，而**[自旋张量](@entry_id:187346)（spin tensor）** $\boldsymbol{W}$（$\boldsymbol{L}$的反对称部分）则等于角速度张量 $\boldsymbol{W}$，通常不为零。这再次从速率的角度印证了刚体无变形的特性 [@problem_id:3596971]。

### [刚体运动](@entry_id:193355)的[代数结构](@entry_id:137052)：[特殊欧几里得群](@entry_id:139383) SE(3)

单个[刚体运动](@entry_id:193355)可以用一对 $(\boldsymbol{R}, \boldsymbol{c})$ 来表示，其中 $\boldsymbol{R} \in \mathrm{SO}(3)$ 是[旋转矩阵](@entry_id:140302)，$\boldsymbol{c} \in \mathbb{R}^3$ 是平移向量。所有这些运动的集合具有一个优雅的[代数结构](@entry_id:137052)，即**群（group）**的结构。

考虑两个相继的[刚体运动](@entry_id:193355)，$\mathcal{T}_1(\boldsymbol{x}) = \boldsymbol{R}_1\boldsymbol{x} + \boldsymbol{c}_1$ 和 $\mathcal{T}_2(\boldsymbol{x}) = \boldsymbol{R}_2\boldsymbol{x} + \boldsymbol{c}_2$。它们的**复合（composition）** $\mathcal{T}_2 \circ \mathcal{T}_1$ 表示先进行运动1，再进行运动2：

$$
(\mathcal{T}_2 \circ \mathcal{T}_1)(\boldsymbol{x}) = \mathcal{T}_2(\boldsymbol{R}_1\boldsymbol{x} + \boldsymbol{c}_1) = \boldsymbol{R}_2(\boldsymbol{R}_1\boldsymbol{x} + \boldsymbol{c}_1) + \boldsymbol{c}_2 = (\boldsymbol{R}_2\boldsymbol{R}_1)\boldsymbol{x} + (\boldsymbol{R}_2\boldsymbol{c}_1 + \boldsymbol{c}_2)
$$

这个结果表明，两次[刚体运动](@entry_id:193355)的复合仍然是一个[刚体运动](@entry_id:193355)，其等效旋转为 $\boldsymbol{R}_{\text{comp}} = \boldsymbol{R}_2\boldsymbol{R}_1$，等效平移为 $\boldsymbol{c}_{\text{comp}} = \boldsymbol{R}_2\boldsymbol{c}_1 + \boldsymbol{c}_2$。这证明了刚体运动集合在复合运算下是**封闭的** [@problem_id:3596967]。

然而，这个复合运算通常是**非交换的（non-commutative）**。如果我们交换运动的顺序，得到的结果将是：

$$
(\mathcal{T}_1 \circ \mathcal{T}_2)(\boldsymbol{x}) = (\boldsymbol{R}_1\boldsymbol{R}_2)\boldsymbol{x} + (\boldsymbol{R}_1\boldsymbol{c}_2 + \boldsymbol{c}_1)
$$

由于三维空间中的旋转本身是非交换的（即通常 $\boldsymbol{R}_1\boldsymbol{R}_2 \neq \boldsymbol{R}_2\boldsymbol{R}_1$），并且平移向量会受到之前旋转的影响（$\boldsymbol{R}_2\boldsymbol{c}_1 \neq \boldsymbol{R}_1\boldsymbol{c}_2$），因此刚体运动的顺序至关重要。一个经典的例子是，一个物体先绕 x 轴旋转 $90^\circ$ 再绕 z 轴旋转 $90^\circ$，其最终姿态与先绕 z 轴旋转 $90^\circ$ 再绕 x 轴旋转 $90^\circ$ 的最终姿态是不同的 [@problem_id:3596967] [@problem_id:3596968]。

一个[群结构](@entry_id:146855)还要求每个元素都有一个**逆元（inverse）**。对于运动 $\boldsymbol{x}' = \boldsymbol{R}\boldsymbol{x} + \boldsymbol{c}$，其逆运动是将点从 $\boldsymbol{x}'$ 映射回 $\boldsymbol{x}$。通过简单的代数运算可得：

$$
\boldsymbol{x} = \boldsymbol{R}^{-1}(\boldsymbol{x}' - \boldsymbol{c}) = \boldsymbol{R}^{\mathsf{T}}\boldsymbol{x}' - \boldsymbol{R}^{\mathsf{T}}\boldsymbol{c}
$$

因此，逆运动 $(\boldsymbol{R}, \boldsymbol{c})^{-1}$ 对应于 $(\boldsymbol{R}^{\mathsf{T}}, -\boldsymbol{R}^{\mathsf{T}}\boldsymbol{c})$，它本身也是一个[刚体运动](@entry_id:193355) [@problem_id:3597007]。

由于[刚体运动](@entry_id:193355)集合在复合运算下封闭，存在单位元（$\boldsymbol{R}=\boldsymbol{I}, \boldsymbol{c}=\boldsymbol{0}$），且每个元素都有逆元，这个集合构成了一个李群，称为**三维[特殊欧几里得群](@entry_id:139383)（Special Euclidean Group）**，记作 $\mathrm{SE}(3)$。在机器人学和[计算机图形学](@entry_id:148077)中，常使用 $4 \times 4$ 的**齐次[变换矩阵](@entry_id:151616)（homogeneous transformation matrix）** 来表示 $\mathrm{SE}(3)$ 中的元素，这使得复合和求逆运算可以统一表示为矩阵的乘法和求逆。

### 无穷小转动与线性化

虽然有限大小的旋转是不可交换的，但**无穷小转动（infinitesimal rotations）**却具有可交换性。一个围绕轴 $\boldsymbol{n}$ 的无穷小角度 $d\theta$ 的旋转可以线性化为 $\boldsymbol{R} \approx \boldsymbol{I} + d\theta\hat{\boldsymbol{n}}$，其中 $\hat{\boldsymbol{n}}$ 是与轴向量 $\boldsymbol{n}$ 对应的[反对称矩阵](@entry_id:155998)。如果我们复合两个无穷小转动，并忽略二阶无穷小量，可以发现：

$$
( \boldsymbol{I} + d\theta_1\hat{\boldsymbol{n}}_1 ) ( \boldsymbol{I} + d\theta_2\hat{\boldsymbol{n}}_2 ) \approx \boldsymbol{I} + d\theta_1\hat{\boldsymbol{n}}_1 + d\theta_2\hat{\boldsymbol{n}}_2 \approx ( \boldsymbol{I} + d\theta_2\hat{\boldsymbol{n}}_2 ) ( \boldsymbol{I} + d\theta_1\hat{\boldsymbol{n}}_1 )
$$

这表明无穷小转动的次序无关紧要 [@problem_id:3596968]。这一特性使得对涉及小转动的系统进行线性化分析成为可能。

考虑一个由小转动和小平移构成的刚体运动。其位移场 $\boldsymbol{u}(\boldsymbol{X}) = \boldsymbol{x}(\boldsymbol{X}) - \boldsymbol{X} = (\boldsymbol{R}(\boldsymbol{\theta})\boldsymbol{X} + \boldsymbol{c}) - \boldsymbol{X}$，其中 $\boldsymbol{\theta}$ 是一个无穷小转动向量。将旋转矩阵线性化为 $\boldsymbol{R}(\boldsymbol{\theta}) \approx \boldsymbol{I} + \hat{\boldsymbol{\theta}}$，我们得到：

$$
\boldsymbol{u}(\boldsymbol{X}) \approx (\boldsymbol{I} + \hat{\boldsymbol{\theta}})\boldsymbol{X} + \boldsymbol{c} - \boldsymbol{X} = \hat{\boldsymbol{\theta}}\boldsymbol{X} + \boldsymbol{c}
$$

利用轴向量关系 $\hat{\boldsymbol{\theta}}\boldsymbol{X} = \boldsymbol{\theta} \times \boldsymbol{X}$，我们得到了小位移[刚体运动](@entry_id:193355)的线性化[位移场](@entry_id:141476)：

$$
\boldsymbol{u}(\boldsymbol{X}) \approx \boldsymbol{c} + \boldsymbol{\theta} \times \boldsymbol{X}
$$

这个表达式在[结构力学](@entry_id:276699)、[振动分析](@entry_id:146266)和[线性稳定性分析](@entry_id:154985)中极为重要，它表明任何小的刚体位移都可以分解为一个小的平移和一个绕原点的小转动的叠加 [@problem_id:3597015]。

### 刚体运动在[连续介质力学](@entry_id:155125)中的意义

#### 作为零应变状态的[刚体运动](@entry_id:193355)

[刚体运动](@entry_id:193355)在[连续介质力学](@entry_id:155125)中扮演着“零变形”基准的角色。我们已经看到，[刚体运动](@entry_id:193355)的充要条件是[格林-拉格朗日应变张量](@entry_id:187745) $\boldsymbol{E}$ 为零。这提供了一个判别变形是否纯粹是[刚体运动](@entry_id:193355)的清晰判据。在[数值模拟](@entry_id:137087)中，如果一个计算出的变形梯度 $\boldsymbol{F}$ 导致了很小的应变张量（例如，其范数 $\|\boldsymbol{E}\|$ 接近于零），我们就可以认为该单元在该步中近似经历了[刚体运动](@entry_id:193355)。这对于调试和验证有限元代码非常有用 [@problem_id:3596973]。一个更精确的度量是计算 $\boldsymbol{F}$ 与其最近的[旋转矩阵](@entry_id:140302) $\boldsymbol{R}$（通过极分解 $\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$ 得到）之间的距离，即 $\|\boldsymbol{F}-\boldsymbol{R}\|$。如果这个距离和应变范数都很小，那么该运动可以被认为是近似[刚体运动](@entry_id:193355)。

#### 物质[标架无关性原理](@entry_id:200995)（[客观性原理](@entry_id:185412)）

刚体运动在构建材料[本构关系](@entry_id:186508)时起着核心作用，这体现在**物质[标架无关性原理](@entry_id:200995)（principle of material frame indifference）**或**[客观性原理](@entry_id:185412)（principle of objectivity）**上。该原理断言，材料的本构关系（即应力与应变、应变率等之间的关系）必须独立于观察者。换句话说，物理定律不应因观察者自身的[刚体运动](@entry_id:193355)而改变。

考虑两个观察者，他们的[参考系](@entry_id:169232)之间通过一个任意的、随时间变化的[刚体运动](@entry_id:193355)相关联：$\boldsymbol{x}^* (t) = \boldsymbol{R}(t)\boldsymbol{x}(t) + \boldsymbol{c}(t)$。[客观性原理](@entry_id:185412)要求，在带星号（*）[参考系](@entry_id:169232)中测量的物理量所遵循的本构律，形式上必须与在无星号[参考系](@entry_id:169232)中完全相同。

为了满足这一要求，我们需要研究各种物理量在观察者变换下的转换规律。可以证明：
- 变形梯度变换为 $\boldsymbol{F}^* = \boldsymbol{R}\boldsymbol{F}$。
- 柯西应力张量变换为 $\boldsymbol{\sigma}^* = \boldsymbol{R}\boldsymbol{\sigma}\boldsymbol{R}^{\mathsf{T}}$。
- 变形率[张量变换](@entry_id:183453)为 $\boldsymbol{D}^* = \boldsymbol{R}\boldsymbol{D}\boldsymbol{R}^{\mathsf{T}}$。

像 $\boldsymbol{\sigma}$ 和 $\boldsymbol{D}$ 这样变换的张量被称为**客观张量（objective tensors）**。然而，像变形梯度 $\boldsymbol{F}$ 和[自旋张量](@entry_id:187346) $\boldsymbol{W}$（其变换为 $\boldsymbol{W}^* = \boldsymbol{R}\boldsymbol{W}\boldsymbol{R}^{\mathsf{T}} + \dot{\boldsymbol{R}}\boldsymbol{R}^{\mathsf{T}}$）则不是客观的，因为它们的变换规律包含了观察者自身的运动（$\boldsymbol{R}$ 或 $\dot{\boldsymbol{R}}$）。

[客观性原理](@entry_id:185412)对[本构关系](@entry_id:186508)施加了严格的限制。例如，对于一个[超弹性材料](@entry_id:190241)，其[应变能密度函数](@entry_id:755490) $\psi$ 是一个标量，必须是客观的，即 $\psi^* = \psi$。如果 $\psi$ 是变形梯度 $\boldsymbol{F}$ 的函数，即 $\psi = \psi(\boldsymbol{F})$，则客观性要求 $\psi(\boldsymbol{F}) = \psi(\boldsymbol{F}^*) = \psi(\boldsymbol{R}\boldsymbol{F})$ 对所有旋转 $\boldsymbol{R} \in \mathrm{SO}(3)$ 成立。这个条件的一个直接推论是，$\psi$ 只能通过 $\boldsymbol{F}$ 的客观组合来依赖于 $\boldsymbol{F}$，最常见的就是[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$。因为 $(\boldsymbol{R}\boldsymbol{F})^{\mathsf{T}}(\boldsymbol{R}\boldsymbol{F}) = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R}\boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$，所以 $\boldsymbol{C}$ 在叠加的[刚体转动](@entry_id:191086)下是不变的。因此，客观的[应变能函数](@entry_id:178435)必须可以表达为 $\psi = \hat{\psi}(\boldsymbol{C})$ 的形式 [@problem_id:3597041]。

同样，对于依赖于变形率的粘性流体，其[本构关系](@entry_id:186508)必须依赖于客观的张量 $\boldsymbol{D}$，而不是非客观的张量 $\boldsymbol{L}$ 或 $\boldsymbol{W}$。这就是为什么典型的牛顿流体本构关系将应力与变形率张量 $\boldsymbol{D}$ 联系起来的原因。刚体运动，特别是刚体旋转，是检验和构建物理上合理的本构模型的试金石。