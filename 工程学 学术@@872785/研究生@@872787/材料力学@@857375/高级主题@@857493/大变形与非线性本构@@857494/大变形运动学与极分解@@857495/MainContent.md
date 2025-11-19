## 引言
在现代[固体力学](@entry_id:164042)和[材料科学](@entry_id:152226)中，精确描述物体在经历大位移和显著转动时的行为至关重要。当变形不再微小时，经典小应变理论的线性假设便宣告失效。此时，我们需要一个更严谨的数学框架——有限变形[运动学](@entry_id:173318)。这一理论是理解和模拟从橡胶拉伸、金属成型到生物组织生长等众多工程与自然现象的基础。其核心挑战在于如何将物体真实的形状改变（应变）从其整体的[刚体运动](@entry_id:193355)（平移和旋转）中精确地分离出来。

本文旨在系统地阐述有限变形[运动学](@entry_id:173318)的核心原理与应用。我们将从最基本的概念出发，层层深入，为读者构建一个清晰而完整的知识体系。
*   在**“原理与机制”**一章中，我们将详细介绍变形梯度，这是描述局部变形的基石。随后，我们将聚焦于其关键的数学工具——极分解，揭示它如何巧妙地将变形分解为[拉伸与旋转](@entry_id:150197)，并由此引出各种有限应变和应变率的度量。
*   进入**“应用与[交叉](@entry_id:147634)学科联系”**一章，我们将展示这些运动学原理的强大生命力。您将看到它们如何成为构建超弹性和塑性[本构模型](@entry_id:174726)、指导先进[计算力学](@entry_id:174464)方法以及连接[材料科学](@entry_id:152226)前沿（如[相变](@entry_id:147324)和[微极理论](@entry_id:202574)）的理论支柱。
*   最后，在**“动手实践”**部分，通过精选的计算练习，您将有机会亲手应用所学知识，加深对关键概念（如简单剪切中的内蕴旋转）的理解。

通过本文的学习，您将掌握描述材料大变形行为的通用语言，为深入研究[非线性](@entry_id:637147)[连续介质力学](@entry_id:155125)、本构理论和[计算固体力学](@entry_id:169583)奠定坚实的运动学基础。

## 原理与机制

在连续介质力学中，对物体变形的运动学描述是后续[应力分析](@entry_id:168804)和本构关系建[模的基](@entry_id:156416)础。本章旨在系统地阐述有限变形运动学的核心概念，从变形梯度的基本定义出发，深入探讨其关键的数学分解——极分解，并由此引出各种应变和[应变率](@entry_id:154778)的度量。我们将揭示这些数学工具如何精确地将复杂的变形过程分解为更易于物理理解的[拉伸与旋转](@entry_id:150197)分量。

### 变形梯度

描述连续体运动的核心是 **运动** (motion) 函数 $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$，它将物体在 **参考构型**（或称为[材料构型](@entry_id:183091)）$\mathcal{B}_0$ 中的任一物质点 $\mathbf{X}$ 映射到其在 $t$ 时刻 **当前构型**（或称为空间构型）$\mathcal{B}_t$ 中的空间位置 $\mathbf{x}$。参考构型是[固有时](@entry_id:192124)（通常是 $t=0$）的构型，而当前构型则随[时间演化](@entry_id:153943)。

为了量化局部的变形，我们考察参考构型中一个点 $\mathbf{X}$ 及其无限接近的邻点 $\mathbf{X} + \mathrm{d}\mathbf{X}$。经过运动后，它们分别变为当前构型中的点 $\mathbf{x}$ 和 $\mathbf{x} + \mathrm{d}\mathbf{x}$。根据[多元函数](@entry_id:145643)[微分](@entry_id:158718)的定义，这两个无穷小线元矢量之间的关系可以通过对运动函数 $\boldsymbol{\varphi}$ 进行一阶泰勒展开得到：
$$
\mathrm{d}\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X} + \mathrm{d}\mathbf{X}, t) - \boldsymbol{\varphi}(\mathbf{X}, t) \approx \frac{\partial \boldsymbol{\varphi}(\mathbf{X}, t)}{\partial \mathbf{X}} \mathrm{d}\mathbf{X}
$$
这个关系中的[线性映射](@entry_id:185132)算子，即运动函数 $\boldsymbol{\varphi}$ 对材料坐标 $\mathbf{X}$ 的梯度，被称为 **变形梯度** (deformation gradient)，记为 $\mathbf{F}$。
$$
\mathbf{F}(\mathbf{X}, t) = \nabla_{\mathbf{X}} \boldsymbol{\varphi} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}}
$$
因此，变形梯度 $\mathbf{F}$ 是一个[二阶张量](@entry_id:199780)，它将参考构型中的一个无穷小[线元](@entry_id:196833) $\mathrm{d}\mathbf{X}$ 线性地映射到当前构型中对应的[线元](@entry_id:196833) $\mathrm{d}\mathbf{x}$ [@problem_id:2922110]。

$$
\mathrm{d}\mathbf{x} = \mathbf{F} \mathrm{d}\mathbf{X}
$$

对于一种特殊的 **均匀变形** (homogeneous deformation)，其运动函数形式为 $\mathbf{x} = \mathbf{A}\mathbf{X} + \mathbf{b}$，其中 $\mathbf{A}$ 和 $\mathbf{b}$ 是不依赖于 $\mathbf{X}$ 的张量和矢量。在这种情况下，变形梯度在整个物体内是均匀的，恒等于 $\mathbf{F} = \mathbf{A}$ [@problem_id:2886421]。这个简单的例子清晰地揭示了 $\mathbf{F}$ 作为局部变形线性近似的本质。

变形梯度不仅描述了线元的变换，它还包含了关于体积和面积变化的全部信息。$\mathbf{F}$ 的[行列式](@entry_id:142978)，即雅可比行列式 $J = \det \mathbf{F}$，给出了局部体积变化的比例。一个在参考构型中体积为 $\mathrm{d}V$ 的无穷小元，在当前构型中的体积 $\mathrm{d}v$ 为：
$$
\mathrm{d}v = J \mathrm{d}V
$$
为了保证物质的不可穿透性（即两个不同的物[质点](@entry_id:186768)不能占据同一空间位置）并保持物质微元的原始方位（例如，[右手坐标系](@entry_id:166669)始终映射为[右手坐标系](@entry_id:166669)），物理上允许的变形必须满足 $J > 0$ 的条件。这个条件意味着变形是局部可逆的，且保持了朝向。任何导致 $J \le 0$ 的变形在物理上都是不可接受的，例如 $J  0$ 意味着物质发生了“里外翻转”，而 $J=0$ 则意味着一个三维体被压缩成了平面或线 [@problem_id:2886421] [@problem_id:2886418]。

[面积元](@entry_id:263205)的变化则由著名的 **[南森公式](@entry_id:195566)** (Nanson's formula) 描述。若参考构型中一个[有向面积](@entry_id:169588)元为 $\mathbf{N}\mathrm{d}A$（其中 $\mathbf{N}$ 为[单位法向量](@entry_id:178851)，$\mathrm{d}A$ 为面积大小），其在当前构型中对应的[有向面积](@entry_id:169588)元为 $\mathbf{n}\mathrm{d}a$，则它们之间的关系是：
$$
\mathbf{n}\mathrm{d}a = J \mathbf{F}^{-T} \mathbf{N}\mathrm{d}A
$$
其中 $\mathbf{F}^{-T}$ 是 $\mathbf{F}$ 的逆之转置。这个公式在处理涉及[曲面](@entry_id:267450)力（如压力）的[积分变换](@entry_id:186209)时至关重要 [@problem_id:2922110]。

### 极分解：分离[拉伸与旋转](@entry_id:150197)

变形梯度 $\mathbf{F}$ 作为一个[线性算子](@entry_id:149003)，同时包含了物体的拉伸和旋转信息。为了更深入地理解变形的物理本质，我们需要将这两种效应分离开来。**极分解定理** (polar decomposition theorem) 为此提供了强大的数学工具。该定理指出，任何可逆的二阶张量 $\mathbf{F}$（即 $\det \mathbf{F} \neq 0$）都可以唯一地分解为两种形式：

1.  **右极分解** (right polar decomposition): $\mathbf{F} = \mathbf{R}\mathbf{U}$
2.  **左极分解** (left polar decomposition): $\mathbf{F} = \mathbf{V}\mathbf{R}$

在这里：
*   $\mathbf{R}$ 是一个 **正常正交张量** (proper orthogonal tensor)，代表了刚体 **旋转** (rotation)。它满足 $\mathbf{R}^T\mathbf{R} = \mathbf{I}$ 和 $\det \mathbf{R} = +1$。物理可容许性条件 $\det \mathbf{F}  0$ 确保了 $\mathbf{R}$ 必须是纯旋转，排除了反射等非物理变换 [@problem_id:2886418]。
*   $\mathbf{U}$ 是 **右[拉伸张量](@entry_id:193200)** (right stretch tensor)，它是一个[对称正定](@entry_id:145886)张量 ($\mathbf{U}^T = \mathbf{U}$，且所有[特征值](@entry_id:154894)均为正)。
*   $\mathbf{V}$ 是 **左[拉伸张量](@entry_id:193200)** (left stretch tensor)，它也是一个对称正定张量 ($\mathbf{V}^T = \mathbf{V}$，且所有[特征值](@entry_id:154894)均为正)。

右极分解 $\mathbf{F} = \mathbf{R}\mathbf{U}$ 的物理图像非常直观：一个物质[线元](@entry_id:196833) $\mathrm{d}\mathbf{X}$ 首先经历一次由 $\mathbf{U}$ 描述的纯拉伸，变为中间状态的 $\mathrm{d}\mathbf{X}' = \mathbf{U}\mathrm{d}\mathbf{X}$；然后，这个被拉伸后的[线元](@entry_id:196833)再经历一次由 $\mathbf{R}$ 描述的刚体旋转，得到其在当前构型中的最终形态 $\mathrm{d}\mathbf{x} = \mathbf{R}(\mathrm{d}\mathbf{X}')$ [@problem_id:2922110]。重要的是，右[拉伸张量](@entry_id:193200) $\mathbf{U}$ 的作用空间是参考构型，而左[拉伸张量](@entry_id:193200) $\mathbf{V}$ 的作用空间是当前构型。这两个[拉伸张量](@entry_id:193200)通过[旋转张量](@entry_id:191990) $\mathbf{R}$ 联系在一起：$\mathbf{V} = \mathbf{R}\mathbf{U}\mathbf{R}^T$。

为了具体说明，考虑一个沿 $\mathbf{e}_1$ 方向的[单轴拉伸](@entry_id:188287)，其变形梯度为 $\mathbf{F} = \mathrm{diag}(\lambda, 1, 1)$，其中 $\lambda  0$ 是拉伸比 [@problem_id:2886394]。由于 $\mathbf{F}$ 本身就是[对称正定](@entry_id:145886)的，它不包含任何旋转。通过计算可以验证，其右[拉伸张量](@entry_id:193200) $\mathbf{U} = \mathbf{F}$，而[旋转张量](@entry_id:191990) $\mathbf{R} = \mathbf{I}$（单位张量）。这清晰地表明，纯拉伸变形的旋转部分为零。

### 应变张量与主变形

[拉伸张量](@entry_id:193200) $\mathbf{U}$ 和 $\mathbf{V}$ 是纯粹的变形量度，它们完全决定了物体的应变状态。为了方便工程应用，我们定义了多种[应变张量](@entry_id:193332)。

首先是与[拉伸张量](@entry_id:193200)直接相关的 **柯西-格林[应变张量](@entry_id:193332)** (Cauchy-Green strain tensors)：
*   **[右柯西-格林张量](@entry_id:174156)** (right Cauchy-Green tensor): $\mathbf{C} = \mathbf{F}^T\mathbf{F} = (\mathbf{R}\mathbf{U})^T(\mathbf{R}\mathbf{U}) = \mathbf{U}^T\mathbf{R}^T\mathbf{R}\mathbf{U} = \mathbf{U}^2$。它在参考构型中定义。
*   **[左柯西-格林张量](@entry_id:186163)** (left Cauchy-Green or Finger tensor): $\mathbf{B} = \mathbf{F}\mathbf{F}^T = (\mathbf{V}\mathbf{R})(\mathbf{V}\mathbf{R})^T = \mathbf{V}\mathbf{R}\mathbf{R}^T\mathbf{V}^T = \mathbf{V}^2$。它在当前构型中定义。

$\mathbf{C}$ 和 $\mathbf{B}$ 都是[对称正定](@entry_id:145886)张量，它们只与拉伸有关，与刚体旋转 $\mathbf{R}$ 无关。

根据[谱定理](@entry_id:136620)，对称张量 $\mathbf{U}$ 和 $\mathbf{V}$ 存在一组正交的[特征向量](@entry_id:151813)，它们定义了 **主方向** (principal directions)，其对应的[特征值](@entry_id:154894)则是 **主拉伸比** (principal stretches) $\lambda_i$ [@problem_id:2918196]。
*   $\mathbf{U}$ 的[特征向量](@entry_id:151813) $\mathbf{E}_i$ 是参考构型中的[主方向](@entry_id:276187)。
*   $\mathbf{V}$ 的[特征向量](@entry_id:151813) $\mathbf{e}_i$ 是当前构型中的[主方向](@entry_id:276187)。
*   $\mathbf{U}$ 和 $\mathbf{V}$ 具有相同的主拉伸比 $\lambda_i$。
*   [主方向](@entry_id:276187)之间通过旋转 $\mathbf{R}$ 相互关联：$\mathbf{e}_i = \mathbf{R}\mathbf{E}_i$。

物理上，[主方向](@entry_id:276187)是指那些在变形过程中只经历长度变化而没有[剪切变形](@entry_id:170920)的方向。一个沿参考[主方向](@entry_id:276187) $\mathbf{E}_i$ 的[线元](@entry_id:196833)，变形后将变为一个沿当前主方向 $\mathbf{e}_i$ 的[线元](@entry_id:196833)，其长度被拉伸了 $\lambda_i$ 倍 [@problem_id:2918196]。

$\mathbf{C}$ 和 $\mathbf{B}$ 的[特征值](@entry_id:154894)是主拉伸比的平方，即 $\lambda_i^2$。因此，它们的 **[主不变量](@entry_id:193522)** (principal invariants) $I_1 = \mathrm{tr}(\mathbf{C})$, $I_2 = \frac{1}{2}[(\mathrm{tr}(\mathbf{C}))^2 - \mathrm{tr}(\mathbf{C}^2)]$, $I_3 = \det(\mathbf{C})$ 只依赖于变形的量值，而与旋转无关。例如，对于一个简单剪切变形 $\mathbf{F} = \mathbf{I} + \gamma \mathbf{e}_1 \otimes \mathbf{e}_2$，我们可以计算出 $I_1(\mathbf{C}) = 3+\gamma^2$, $I_2(\mathbf{C}) = 3+\gamma^2$, $I_3(\mathbf{C}) = 1$。这些[不变量](@entry_id:148850)都依赖于 $\gamma^2$，因此它们能反映剪切的幅度，但无法区分剪切的方向（即 $\gamma$ 的符号），因为方向信息包含在[旋转张量](@entry_id:191990) $\mathbf{R}$ 中 [@problem_id:2886401]。

从柯西-格林张量出发，可以定义两个常用的[应变张量](@entry_id:193332)：
*   **[格林-拉格朗日应变张量](@entry_id:187745)** (Green-Lagrange strain tensor): $\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})$。它是一个材料量，描述了相对于参考构型的应变。
*   **阿勒曼西[应变张量](@entry_id:193332)** (Almansi strain tensor): $\mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{B}^{-1})$。它是一个空间量，描述了相对于当前构型的应变。

这两个张量虽然描述的是同一个物理变形状态，但由于其参考基准不同，它们的数值分量通常是不同的。例如，在[单轴拉伸](@entry_id:188287) $\lambda$ 的情况下，拉伸方向上的应变分量分别为 $E_{11} = \frac{1}{2}(\lambda^2 - 1)$ 和 $e_{11} = \frac{1}{2}(1 - \lambda^{-2})$。$E_{11}$ 将长度平方的变化归一化到初始长度，而 $e_{11}$ 则将其归一化到最终长度 [@problem_id:2886403]。

### 变形率的运动学

为了研究变形随时间的变化，我们需要引入速率的概念。物质点 $\mathbf{X}$ 的[速度场](@entry_id:271461)在空间描述下为 $\mathbf{v}(\mathbf{x}, t)$。**[速度梯度](@entry_id:261686)** (velocity gradient) $\mathbf{L}$ 定义为速度场对空间坐标的梯度：
$$
\mathbf{L} = \nabla_{\mathbf{x}} \mathbf{v}
$$
它与变形梯度的时间导数 $\dot{\mathbf{F}}$ 之间存在重要关系：$\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}$。

与变形梯度类似，速度梯度也可以分解。任何[二阶张量](@entry_id:199780)都可以唯一地分解为其对称部分和反对称部分之和。因此，$\mathbf{L}$ 可以分解为：
$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$
其中：
*   $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T)$ 是 **应变率张量** (rate of deformation tensor)，它是对称的。
*   $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T)$ 是 **[自旋张量](@entry_id:187346)** (spin tensor)，它是反对称的。

这个分解具有深刻的物理意义。[应变率张量](@entry_id:266108) $\mathbf{D}$ 描述了材料微元的纯粹变形速率（拉伸和剪切率）。一个方向为 $\mathbf{n}$ 的材料纤维的长度 $\mathrm{d}\ell$ 的变化率完全由 $\mathbf{D}$ 决定：$\frac{\mathrm{d}}{\mathrm{d}t}(\mathrm{d}\ell) = (\mathbf{n} \cdot \mathbf{D}\mathbf{n}) \mathrm{d}\ell$。[自旋张量](@entry_id:187346) $\mathbf{W}$ 则描述了材料微元的刚体旋转[角速度](@entry_id:192539)，它不引起任何长度或形状的变化。对于纯刚体运动，$\mathbf{D}=\mathbf{0}$，而 $\mathbf{W}$ 恰好等于该[刚体运动](@entry_id:193355)的[角速度](@entry_id:192539)张量 [@problem_id:2886428]。

将极分解代入 $\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}$ 的关系式，可以得到 $\mathbf{D}$ 和 $\mathbf{W}$ 与 $\mathbf{R}, \mathbf{U}$ 及其时间导数之间的复杂关系 [@problem_id:2886428]：
$$
\mathbf{L} = \dot{\mathbf{R}}\mathbf{R}^T + \mathbf{R}(\dot{\mathbf{U}}\mathbf{U}^{-1})\mathbf{R}^T
$$
由此可得 $\mathbf{D}$ 和 $\mathbf{W}$ 的表达式：
$$
\mathbf{D} = \mathrm{sym}(\mathbf{R}(\dot{\mathbf{U}}\mathbf{U}^{-1})\mathbf{R}^T)
$$
$$
\mathbf{W} = \dot{\mathbf{R}}\mathbf{R}^T + \mathrm{skew}(\mathbf{R}(\dot{\mathbf{U}}\mathbf{U}^{-1})\mathbf{R}^T)
$$
值得注意的是，[自旋张量](@entry_id:187346) $\mathbf{W}$ 一般不等于材料的旋转速率 $\dot{\mathbf{R}}\mathbf{R}^T$，除非在某些特殊情况下（例如，[主应变](@entry_id:197797)方向与材料[坐标系](@entry_id:156346)固连）。

### 高级主题与应用

#### 客观性与材料本构

在建立本构关系时，一个基本原则是 **[材料客观性原理](@entry_id:177427)** (principle of material frame-indifference)，即本构律不应依赖于观察者的刚体运动。这意味着[本构关系](@entry_id:186508)中使用的物理量在叠加一个任意的刚体运动后应具有特定的[协变](@entry_id:634097)性。在数学上，如果一个张量 $\mathbf{T}$ 在叠加旋转 $\mathbf{Q}(t)$ 后变换为 $\mathbf{T}^* = \mathbf{Q}\mathbf{T}\mathbf{Q}^T$，则称其为 **客观的** (objective)。

通过分析可知，应变率张量 $\mathbf{D}$ 是客观的，而速度梯度 $\mathbf{L}$ 和[自旋张量](@entry_id:187346) $\mathbf{W}$ 则不是 [@problem_id:2886428]。这一性质对本构理论有深远影响。例如，一个直接使用柯西应力 $\boldsymbol{\sigma}$ 的材料时间导数 $\dot{\boldsymbol{\sigma}}$ 的本构模型，如 $\dot{\boldsymbol{\sigma}} = f(\mathbf{D})$，是 **非客观的**。这是因为 $\dot{\boldsymbol{\sigma}}$ 本身不是一个[客观率](@entry_id:198692)。在一个纯刚体旋转下，$\mathbf{D}=\mathbf{0}$，该模型会错误地预测应力不发生变化。然而，物理上正确的应力张量必须随材料一起旋转，即 $\boldsymbol{\sigma}_{\text{phys}}(t) = \mathbf{R}(t)\boldsymbol{\sigma}(0)\mathbf{R}^T(t)$。这种不匹配揭示了使用非[客观应力率](@entry_id:199282)的根本缺陷，并催生了对各种[客观应力率](@entry_id:199282)（如 [Jaumann 率](@entry_id:185572)、Truesdell 率等）的研究 [@problem_id:2886400]。

#### 变形场的相容性

到目前为止，我们都假设存在一个光滑的单值运动函数 $\boldsymbol{\varphi}(\mathbf{X})$，并从中推导变形梯度 $\mathbf{F} = \nabla \boldsymbol{\varphi}$。然而，反过来的问题是：任意给定的一个张量场 $\mathbf{F}(\mathbf{X})$ 是否都能成为某个实际运动的变形梯度？答案是否定的。

要使 $\mathbf{F}$ 成为一个梯度假定是有效的，它必须满足一定的可积性条件，即 **相容性条件** (compatibility condition)。源于二次偏导数的[可交换性](@entry_id:263314)（$\frac{\partial^2 \boldsymbol{\varphi}}{\partial X_i \partial X_j} = \frac{\partial^2 \boldsymbol{\varphi}}{\partial X_j \partial X_i}$），可以证明，一个变形梯度场必须是无旋的：
$$
\mathrm{Curl}(\mathbf{F}) = \mathbf{0}
$$
其中 $\mathrm{Curl}$ 是对[二阶张量](@entry_id:199780)场逐行求旋度的算子。如果一个给定的 $\mathbf{F}(\mathbf{X})$ 场处处满足 $\det\mathbf{F}  0$，但其旋度不为零，那么就不可能在全域内找到一个连续的、单值的位移场与之对应。这样的变形场被称为 **不相容的** (incompatible)。例如，场 $\mathbf{F}(\mathbf{X}) = \mathbf{R}(\gamma X_3)$ 描述了一个随高度 $X_3$ 线性增加的扭转。尽管它处处无应变（$\mathbf{U}=\mathbf{I}$）且保持体积（$\det\mathbf{F}=1$），但可以计算出其旋度非零。这意味着没有任何连续体可以通过一个光滑的整体运动达到这种状态。不相容的变形场在[晶体塑性理论](@entry_id:180579)中与[位错](@entry_id:157482)等缺陷的连续统描述密切相关 [@problem_id:2886397]。