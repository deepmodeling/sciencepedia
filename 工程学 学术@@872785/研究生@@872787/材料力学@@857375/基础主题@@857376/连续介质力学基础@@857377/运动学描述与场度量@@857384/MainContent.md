## 引言
在现代工程科学与物理学中，从预测结构失效到模拟细胞迁移，准确描述物质的运动与变形是所有力学分析的出发点。[连续介质力学](@entry_id:155125)提供了一个强大而统一的框架来应对这一挑战，其基石便是运动学——一门纯粹研究运动几何学而不考虑其背后成因（力）的学科。然而，从直观的位移概念过渡到能够处理任意[大变形](@entry_id:167243)和复杂旋转的严谨数学描述，存在着一个关键的知识体系。本文旨在系统地构建这一体系，为读者理解和应用高级材料模型和计算方法奠定坚实的运动学基础。

本文将分为三个核心部分，引导读者逐步掌握运动学描述的精髓。首先，在“原理与机制”部分，我们将从运动的基本定义出发，引入核心概念如变形梯度张量，并探讨如何通过极分解将其分解为纯粹的拉伸和转动。接着，我们将建立不同的[有限应变度量](@entry_id:185716)，并讨论在处理变形速率时至关重要的[客观性原理](@entry_id:185412)和[应变相容性](@entry_id:199659)条件。随后，在“应用与交叉学科联系”部分，我们将展示这些抽象的[运动学](@entry_id:173318)工具如何在[材料建模](@entry_id:751724)（如[弹塑性](@entry_id:193198)、[各向异性材料](@entry_id:184874)）、计算力学（如有限元方法）以及生物力学等前沿领域中发挥关键作用。最后，通过一系列“动手实践”的练习，读者将有机会将所学理论应用于具体问题，从而加深对这些核心概念的理解。

## 原理与机制

在连续介质力学中，对物体运动和变形的精确描述是构建任何力学理论的基石。本章旨在建立描述这些现象的数学框架，从运动的基本定义出发，系统地介绍变形、应变、运动速率以及在不同参考标架下描述这些量的客观性要求。我们将探讨从有限变形到其速率测度的各种描述方法，为后续章节中本构关系和[平衡方程](@entry_id:172166)的建立奠定[运动学](@entry_id:173318)基础。

### 运动与变形梯度

连续体的**运动 (motion)** 是一个映射 $\boldsymbol{\chi}$，它将物体在某一参考时刻（通常是 $t=0$）的构型 $\mathcal{B}_{0}$ 中的每一个物[质点](@entry_id:186768) $\mathbf{X}$，映射到当前时刻 $t$ 在空间中的位置 $\mathbf{x}$。数学上，这表示为：

$$
\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)
$$

其中，$\mathbf{X}$ 称为**物质坐标 (material coordinate)** 或**拉格朗日坐标 (Lagrangian coordinate)**，它如同一个标签，唯一地标识了一个物质点。$\mathbf{x}$ 称为**空间坐标 (spatial coordinate)** 或**欧拉坐标 (Eulerian coordinate)**，它描述了物质点在当前时刻的几何位置。

一个物理上可接受的运动必须满足两个基本条件。首先，物质是不可穿透的，这意味着两个不同的物质点 $\mathbf{X}_a$ 和 $\mathbf{X}_b$ 在同一时刻不能占据相同的空间位置。这要求映射 $\boldsymbol{\chi}(\cdot, t)$ 在其定义域上是**[单射](@entry_id:183792)的 (injective)**。其次，一个物质微元在变形后必须保持其原始的朝向，不能发生“内外翻转”。这个条件通过要求变形的[雅可比行列式](@entry_id:137120)为正来保证。

为了量化局部的变形，我们引入**变形梯度 (deformation gradient)** 张量 $\mathbf{F}$。它被定义为空间坐标 $\mathbf{x}$ 对物质坐标 $\mathbf{X}$ 的梯度：

$$
\mathbf{F}(\mathbf{X}, t) = \frac{\partial \boldsymbol{\chi}(\mathbf{X}, t)}{\partial \mathbf{X}} = \nabla_{\mathbf{X}} \mathbf{x}
$$

变形梯度 $\mathbf{F}$ 是一个二阶张量，它包含了关于局部变形的全部信息。它的一个基本几何意义是，它将参考构型中的一个无穷小物质[线元](@entry_id:196833) $d\mathbf{X}$ 映射到当前构型中对应的空间线元 $d\mathbf{x}$：

$$
d\mathbf{x} = \mathbf{F} \, d\mathbf{X}
$$

因此，$\mathbf{F}$ 是一个**两点张量 (two-point tensor)**，它的一个标引与物质构型相关，另一个与空间构型相关。

物理上可接受的第二个条件，即**方向保持 (orientation preservation)**，现在可以精确地表述为变形梯度的[行列式](@entry_id:142978)，即雅可比行列式 $J$，必须为正：

$$
J = \det(\mathbf{F}) > 0
$$

$J$ 的值为零或负值分别对应着体积被压缩至零或物质微元发生翻转，这在物理上通常是不允许的。

考虑一个立方体 $[0,1]^3$ 的变形，我们可以通过检验候选的运动映射是否满足[单射性](@entry_id:147722)和 $J>0$ 来判断其物理上的可容许性。例如，运动 $\boldsymbol{\chi}(\mathbf{X}) = (X_1, X_2, -X_3)$ 是单射的，但其变形梯度为 $\mathbf{F} = \text{diag}(1, 1, -1)$，导致 $J = -1$。这代表了一个反射，它翻转了物质的局部朝向，因此是物理上不可接受的。另一个例子，$\boldsymbol{\chi}(\mathbf{X}) = (X_1, X_2, |2X_3-1|)$，代表了物体沿 $X_3=0.5$ 平面的折叠，这显然破坏了[单射性](@entry_id:147722) [@problem_id:2896781]。相反，一个如 $\boldsymbol{\chi}(\mathbf{X})=(X_{1}, X_{2}, X_{3}^{3})$ 的运动，可以验证其在 $[0,1]^3$ 上是单射的，并且其[雅可比行列式](@entry_id:137120) $J = 3X_3^2$ 几乎处处为正（仅在 $X_3=0$ 的面上为零），因此它是一个物理上可接受的变形 [@problem_id:2896781]。

### 变形的几何解释

变形梯度 $\mathbf{F}$ 及其[行列式](@entry_id:142978) $J$ 不仅描述了[线元](@entry_id:196833)的变形，还描述了面元和体元的变形。

**[体元](@entry_id:267802)变换**: 雅可比行列式 $J$ 描述了局部的体积变化。一个在参考构型中体积为 $dV$ 的无穷小体元，在变形后其体积 $dv$ 变为：

$$
dv = J \, dV
$$

这表明 $J$ 是当前体积与参考体积之比 [@problem_id:2896792]。如果 $J=1$，则变形是**等容的 (isochoric)** 或不可压缩的。如果质量守恒，即 $dm = \rho_0 dV = \rho dv$，其中 $\rho_0$ 和 $\rho$ 分别是参考构型和当前构型中的密度，那么我们可以得到密度之间的关系：

$$
\rho = \frac{\rho_0}{J}
$$

这表明，[体积膨胀](@entry_id:144241)（$J>1$）导致密度降低，而体积收缩（$J<1$）导致密度增加 [@problem_id:2896792]。

**面元变换**: 参考构型中由法向量 $\mathbf{N}$ 和面积 $dA$ 定义的有向面元 $\mathbf{N}dA$，在变形后变为由法向量 $\mathbf{n}$ 和面积 $da$ 定义的空间有向面元 $\mathbf{n}da$。它们之间的关系由著名的**[南森公式](@entry_id:195566) (Nanson's relation)** 给出：

$$
\mathbf{n} \, da = J \, \mathbf{F}^{-T} \, \mathbf{N} \, dA
$$

其中 $\mathbf{F}^{-T}$ 表示 $\mathbf{F}$ 的逆的[转置](@entry_id:142115)。这个关系在推导[流体力学](@entry_id:136788)中的[输运定理](@entry_id:176504)和固体力学中的边界条件时至关重要 [@problem_id:2896807]。

### 变形的分解：拉伸与转动

任何一个局部变形，无论多么复杂，都可以被分解为纯粹的拉伸（或压缩）和纯粹的[刚体转动](@entry_id:191086)。这就是**极分解定理 (polar decomposition theorem)** 的核心思想。对于任何具有正[行列式](@entry_id:142978)的变形梯度 $\mathbf{F}$，存在唯一的分解方式：

$$
\mathbf{F} = \mathbf{R}\mathbf{U} = \mathbf{V}\mathbf{R}
$$

其中：
- $\mathbf{R}$ 是一个**纯转动张量 (rotation tensor)**，属于[特殊正交群](@entry_id:146418) $SO(3)$，即 $\mathbf{R}^T\mathbf{R} = \mathbf{I}$ 且 $\det(\mathbf{R})=1$。
- $\mathbf{U}$ 是**右[拉伸张量](@entry_id:193200) (right stretch tensor)**，它是一个[对称正定](@entry_id:145886)张量 ($\mathbf{U}^T=\mathbf{U}$，且其[特征值](@entry_id:154894)全为正)。
- $\mathbf{V}$ 是**左[拉伸张量](@entry_id:193200) (left stretch tensor)**，它也是一个对称正定张量。

这种分解是唯一的 [@problem_id:2896796]。$\mathbf{F}=\mathbf{R}\mathbf{U}$ 这一形式（称为右极分解）可以被解释为：一个物质微元首先经历由 $\mathbf{U}$ 描述的纯拉伸，然后作为一个刚体经历由 $\mathbf{R}$ 描述的转动。类似地，$\mathbf{F}=\mathbf{V}\mathbf{R}$（左极分解）则可解释为先转动后拉伸。

右[拉伸张量](@entry_id:193200) $\mathbf{U}$ 和左[拉伸张量](@entry_id:193200) $\mathbf{V}$ 可以通过变形梯度方便地计算。为此，我们定义两个重要的张量：

- **右柯西-格林变形张量 (Right Cauchy-Green deformation tensor)**: $\mathbf{C} = \mathbf{F}^T\mathbf{F}$
- **左柯西-格林变形张量 (Left Cauchy-Green deformation tensor)**: $\mathbf{B} = \mathbf{F}\mathbf{F}^T$

这两个张量都是[对称正定](@entry_id:145886)的。可以证明，[拉伸张量](@entry_id:193200) $\mathbf{U}$ 和 $\mathbf{V}$ 分别是 $\mathbf{C}$ 和 $\mathbf{B}$ 的唯一正定平方根：

$$
\mathbf{U} = \sqrt{\mathbf{C}} = (\mathbf{F}^T\mathbf{F})^{1/2}
$$
$$
\mathbf{V} = \sqrt{\mathbf{B}} = (\mathbf{F}\mathbf{F}^T)^{1/2}
$$

$\mathbf{U}$ 的[特征值](@entry_id:154894)称为**主拉伸率 (principal stretches)**，它们量化了在三个相互垂直的方向上（即 $\mathbf{U}$ 的[特征向量](@entry_id:151813)方向）的伸长或缩短。可以证明，$\mathbf{U}$ 和 $\mathbf{V}$ 具有相同的[特征值](@entry_id:154894)，即主拉伸率。这些主拉伸率也等于变形梯度 $\mathbf{F}$ 的奇异值 [@problem_id:2896796]。

### [有限应变度量](@entry_id:185716)

变形梯度 $\mathbf{F}$ 包含了[刚体转动](@entry_id:191086)，而应变（Strain）的目的是只量化形状和尺寸的变化。柯西-格林张量 $\mathbf{C}$ 和 $\mathbf{B}$ 正是为此而生。

考虑一个物质线元 $d\mathbf{X}$，其变形后的长度平方为 $ds^2 = d\mathbf{x} \cdot d\mathbf{x}$。利用 $d\mathbf{x} = \mathbf{F}d\mathbf{X}$，我们有：

$$
ds^2 = (\mathbf{F}d\mathbf{X}) \cdot (\mathbf{F}d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{F}^T\mathbf{F}d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{C}d\mathbf{X})
$$

这个关系表明，$\mathbf{C}$ 扮演了参考构型中的一个度量张量的角色，它被用来计算变形后的长度。因此，$\mathbf{C}$ 被称为空间欧几里得度规在参考构型上的**[拉回](@entry_id:160816) (pull-back)** [@problem_id:2896806]。由于 $\mathbf{C}$ 是在物质[坐标系](@entry_id:156346)下定义的，它是一个**[拉格朗日量](@entry_id:174593) (Lagrangian quantity)**。

类似地，我们可以将参考长度平方 $ds_0^2 = d\mathbf{X} \cdot d\mathbf{X}$用空间坐标表示：

$$
ds_0^2 = (\mathbf{F}^{-1}d\mathbf{x}) \cdot (\mathbf{F}^{-1}d\mathbf{x}) = d\mathbf{x} \cdot ((\mathbf{F}^{-1})^T\mathbf{F}^{-1}d\mathbf{x}) = d\mathbf{x} \cdot (\mathbf{B}^{-1}d\mathbf{x})
$$

这表明张量 $\mathbf{B}^{-1}$ 扮演了当前构型中的一个度量张量的角色，它被用来计算变形前的长度。因此，$\mathbf{B}^{-1}$ 被称为参考欧几里得度规在当前构型上的**推前 (push-forward)** [@problem_id:2896806]。$\mathbf{B}$ 和 $\mathbf{B}^{-1}$ 是在空间[坐标系](@entry_id:156346)下定义的，是**欧拉量 (Eulerian quantities)**。

基于 $\mathbf{C}$ 和 $\mathbf{B}$，我们可以定义两个最常用的有限[应变张量](@entry_id:193332)：

1.  **[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor) $\mathbf{E}$**:
    $$
    \mathbf{E} = \frac{1}{2} (\mathbf{C} - \mathbf{I})
    $$
    其中 $\mathbf{I}$ 是单位张量。$\mathbf{E}$ 是一个物质张量（[拉格朗日描述](@entry_id:264498)），它直接量化了物质[线元](@entry_id:196833)长度平方的变化：
    $$
    ds^2 - ds_0^2 = 2 d\mathbf{X} \cdot (\mathbf{E} d\mathbf{X})
    $$
    如果不存在变形（即只有[刚体运动](@entry_id:193355)），则 $\mathbf{F}$ 是一个转动张量，$\mathbf{C}=\mathbf{I}$，因此 $\mathbf{E}=\mathbf{0}$。

2.  **[欧拉-阿尔曼西应变张量](@entry_id:194948) (Euler-Almansi strain tensor) $\mathbf{e}$**:
    $$
    \mathbf{e} = \frac{1}{2} (\mathbf{I} - \mathbf{B}^{-1})
    $$
    $\mathbf{e}$ 是一个[空间张量](@entry_id:185799)（[欧拉描述](@entry_id:264722)），它也量化了长度平方的变化，但以空间线元为参考：
    $$
    ds^2 - ds_0^2 = 2 d\mathbf{x} \cdot (\mathbf{e} d\mathbf{x})
    $$
    同样，对于刚体运动，$\mathbf{B}=\mathbf{I}$，因此 $\mathbf{e}=\mathbf{0}$ [@problem_id:2896798]。

这两个[应变张量](@entry_id:193332)通过变形梯度相互关联，$\mathbf{E}$ 是 $\mathbf{e}$ 的[拉回](@entry_id:160816)，$\mathbf{e}$ 是 $\mathbf{E}$ 的推前：

$$
\mathbf{E} = \mathbf{F}^T \mathbf{e} \mathbf{F}, \quad \mathbf{e} = \mathbf{F}^{-T} \mathbf{E} \mathbf{F}^{-1}
$$

在**小应变 (small-strain)** 假设下，[位移梯度](@entry_id:165352) $\nabla\mathbf{u}$ 很小，变形梯度 $\mathbf{F} = \mathbf{I} + \nabla\mathbf{u}$。此时，$\mathbf{E}$ 和 $\mathbf{e}$ 都可以近似为线化[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$：

$$
\mathbf{E} \approx \mathbf{e} \approx \boldsymbol{\varepsilon} = \frac{1}{2} (\nabla\mathbf{u} + (\nabla\mathbf{u})^T)
$$

这个结果连接了有限变形理论和[小变形理论](@entry_id:174991) [@problem_id:2896798]。

### 运动学量的率

在许多问题中，特别是涉及流体或黏弹性/塑性材料时，变形的[速率比](@entry_id:164491)变形本身更重要。

首先需要区分两种速度描述。**物质速度 (material velocity)** $V(\mathbf{X},t)$ 是固定物质点 $\mathbf{X}$ 的位置随时间的变化率。**[空间速度](@entry_id:190294) (spatial velocity)** $\mathbf{v}(\mathbf{x},t)$ 是在时刻 $t$ 占据空间点 $\mathbf{x}$ 的那个物质点的速度。它们的关系是：

$$
\mathbf{V}(\mathbf{X}, t) = \frac{\partial \boldsymbol{\chi}(\mathbf{X}, t)}{\partial t}, \quad \mathbf{v}(\boldsymbol{\chi}(\mathbf{X}, t), t) = \mathbf{V}(\mathbf{X}, t)
$$

为了描述一个随[流体运动](@entry_id:182721)的粒子所经历的某个物理量（如温度或压力）$\phi(\mathbf{x}, t)$ 的变化率，我们引入**[物质导数](@entry_id:172646) (material derivative)** $D\phi/Dt$。它由[链式法则](@entry_id:190743)给出：

$$
\frac{D\phi}{Dt} = \frac{\partial \phi}{\partial t} + (\nabla_{\mathbf{x}}\phi) \cdot \mathbf{v}
$$

第一项 $\partial \phi / \partial t$ 是在固定空间点上的**[局部变化率](@entry_id:264961)**，第二项 $(\nabla_{\mathbf{x}}\phi) \cdot \mathbf{v}$ 是由于粒子运动到物理场值不同的新位置而产生的**[对流](@entry_id:141806)变化率** [@problem_id:2896812]。

描述变形速率的核心量是**[速度梯度张量](@entry_id:270928) (velocity gradient tensor)** $\mathbf{L}$，它被定义为[空间速度](@entry_id:190294)场 $\mathbf{v}$ 对空间坐标 $\mathbf{x}$ 的梯度：

$$
\mathbf{L} = \nabla_{\mathbf{x}} \mathbf{v}
$$

[速度梯度](@entry_id:261686)可以分解为一个对称[部分和](@entry_id:162077)一个反对称部分：

$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$

其中：
- $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T)$ 是**变形率张量 (rate of deformation tensor)**，它描述了物质微元的拉伸和[剪切变形](@entry_id:170920)的速率。其迹 $\text{tr}(\mathbf{D}) = \nabla \cdot \mathbf{v}$ 代表了体积的膨胀率。如果一个运动是等容的，则 $\text{tr}(\mathbf{D})=0$ [@problem_id:2896770]。
- $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T)$ 是**[自旋张量](@entry_id:187346) (spin tensor)** 或**[涡量张量](@entry_id:189621) (vorticity tensor)**，它描述了物质微元作为刚体的平均转动速率。

[自旋张量](@entry_id:187346) $\mathbf{W}$ 密切相关于**[涡量矢量](@entry_id:187667) (vorticity vector)** $\boldsymbol{\omega} = \nabla \times \mathbf{v}$。它们之间的关系是 $\boldsymbol{\omega}$ 是 $\mathbf{W}$ 的轴矢量（axial vector）的两倍，即对任意矢量 $\mathbf{u}$，有 $(\nabla \times \mathbf{v}) \times \mathbf{u} = 2\mathbf{W}\mathbf{u}$ [@problem_id:2896770]。

### 客观性与标架无关性

物理定律不应依赖于观察者。这意味着[本构关系](@entry_id:186508)（连接应力和应变的方程）必须在所有惯性或非惯性参考标架下保持形式不变。这个原理被称为**物质[标架无关性原理](@entry_id:200995) (principle of material frame-indifference)** 或**[客观性原理](@entry_id:185412) (principle of objectivity)**。

一个从当前参考标架到另一个作刚体运动的标架的变换可以表示为 $\mathbf{x}^* = \mathbf{Q}(t)\mathbf{x} + \mathbf{c}(t)$，其中 $\mathbf{Q}(t)$ 是一个时间相关的转动张量，$\mathbf{c}(t)$ 是一个平移向量。在这个变换下，一个客观的矢量 $\mathbf{v}$ 和一个客观的二阶张量 $\mathbf{T}$ 必须满足如下变换法则：

$$
\mathbf{v}^* = \mathbf{Q}\mathbf{v}, \quad \mathbf{T}^* = \mathbf{Q}\mathbf{T}\mathbf{Q}^T
$$

通过分析，可以发现：
- 变形梯度 $\mathbf{F}$ 不是客观的（$\mathbf{F}^*=\mathbf{Q}\mathbf{F}$）。
- [右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 是客观的（因为它是一个物质张量，不受空间标架变换影响，$\mathbf{C}^*=\mathbf{C}$）。
- [左柯西-格林张量](@entry_id:186163) $\mathbf{B}$ 是客观的（$\mathbf{B}^*=\mathbf{Q}\mathbf{B}\mathbf{Q}^T$）。
- 变形率张量 $\mathbf{D}$ 是客观的，但[自旋张量](@entry_id:187346) $\mathbf{W}$ 不是客观的 [@problem_id:2896806] [@problem_id:2896770]。

然而，一个关键的问题是，柯西应力张量 $\boldsymbol{\sigma}$ 的物质导数 $\dot{\boldsymbol{\sigma}}$ 并不是客观的。这意味着一个简单的本构率形式，如 $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\mathbf{D}$（其中 $\mathbb{C}$ 是[弹性张量](@entry_id:170728)），会违反[客观性原理](@entry_id:185412)，因为它会在纯[刚体转动](@entry_id:191086)下预测出虚假的应力变化。

为了解决这个问题，必须使用**[客观应力率](@entry_id:199282) (objective stress rate)**，它被构造为在参考标架变换下是客观的。大多数[客观率](@entry_id:198692)都具有**余旋 (corotational)** 形式，即从[物质导数](@entry_id:172646)中减去由某种自旋 $\mathbf{\Omega}$ 引起的[刚体转动](@entry_id:191086)部分：

$$
\boldsymbol{\sigma}^{\nabla} = \dot{\boldsymbol{\sigma}} - \mathbf{\Omega}\boldsymbol{\sigma} + \boldsymbol{\sigma}\mathbf{\Omega}^T
$$

不同的[客观率](@entry_id:198692)定义对应于对自旋 $\mathbf{\Omega}$ 的不同选择：
- **[Jaumann 率](@entry_id:185572)**: 采用连续体的[涡量张量](@entry_id:189621)作为自旋，$\mathbf{\Omega} = \mathbf{W}$。
- **Green-Naghdi 率**: 采用极分解中转动张量 $\mathbf{R}$ 的变化率作为自旋，$\mathbf{\Omega} = \dot{\mathbf{R}}\mathbf{R}^T$。
- **Truesdell 率**: 形式更复杂，它与 Kirchhoff 应力的李导数相关。

在纯[刚体转动](@entry_id:191086)下（$\mathbf{D}=\mathbf{0}$），任何形式为 "[客观应力率](@entry_id:199282) = $\mathbb{C}:\mathbf{D}$" 的本构律都会预测应力率为零，这符合物理直觉 [@problem_id:2896809]。然而，不同的[客观率](@entry_id:198692)在复杂的变形历史（如大剪切）下会给出不同的应力响应。例如，基于 [Jaumann 率](@entry_id:185572)的简单[弹塑性](@entry_id:193198)模型在单剪下会预测出非物理的应力[振荡](@entry_id:267781)，这表明客观性本身并不足以保证一个率形式本构律在物理上的完全合理性 [@problem_id:2896809]。

### 应变场的相容性

到目前为止，我们都从一个给定的[位移场](@entry_id:141476) $\mathbf{u}$ 或运动 $\boldsymbol{\chi}$ 出发来计算应变。现在我们反过来问：给定一个对称的二阶张量场 $\boldsymbol{\varepsilon}(\mathbf{x})$，它是否能成为某个连续、单值的[位移场](@entry_id:141476) $\mathbf{u}(\mathbf{x})$ 的应变场？

答案是否定的。一个任意的[对称张量](@entry_id:148092)场通常不能由一个[位移场](@entry_id:141476)导出。为了保证一个位移场的存在，应变场的分量之间必须满足一定的[微分](@entry_id:158718)约束，这就是**[相容性条件](@entry_id:637057) (compatibility conditions)**。

对于[小应变张量](@entry_id:754968) $\boldsymbol{\varepsilon}$，其[相容性条件](@entry_id:637057)是著名的**圣维南相容性方程 (Saint-Venant's compatibility equations)**。这组[偏微分方程](@entry_id:141332)可以被紧凑地写成一个张量方程：

$$
\text{curl} \, (\text{curl} \, \boldsymbol{\varepsilon})^T = \mathbf{0}
$$

或者对于[对称张量](@entry_id:148092)，更常见的形式是：

$$
\text{inc} \, \boldsymbol{\varepsilon} := \text{curl} \, (\text{curl} \, \boldsymbol{\varepsilon}) = \mathbf{0}
$$

这个条件是**必要的**。如果一个应变场是由一个[位移场](@entry_id:141476)导出的，那么它必须自动满足这个方程。在一个**单连通 (simply connected)** 的区域（即没有“洞”的区域）内，这个条件也是**充分的**。也就是说，只要一个[对称张量](@entry_id:148092)场 $\boldsymbol{\varepsilon}$ 满足圣维南相容性方程，就一定存在一个[位移场](@entry_id:141476) $\mathbf{u}$（唯一性以刚体位移为模），使得 $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T)$ [@problem_id:2896773]。

然而，在**多连通 (multiply connected)** 的区域（例如，一个有孔的圆环或一个中空的圆柱体），情况变得复杂。圣维南相容性方程仍然是必要的，但不再是充分的。即使局部相容性得到满足，沿着围绕“洞”的闭合[路径积分](@entry_id:156701)位移增量，也可能得到一个非零的结果，这会导致[位移场](@entry_id:141476)是多值的。这种情况与晶体中的**[位错](@entry_id:157482) (dislocations)** 概念密切相关。为了在多连通体中保证单值位移场的存在，除了局部的[微分](@entry_id:158718)相容性条件外，还需要满足额外的全局积分条件 [@problem_id:2896773]。