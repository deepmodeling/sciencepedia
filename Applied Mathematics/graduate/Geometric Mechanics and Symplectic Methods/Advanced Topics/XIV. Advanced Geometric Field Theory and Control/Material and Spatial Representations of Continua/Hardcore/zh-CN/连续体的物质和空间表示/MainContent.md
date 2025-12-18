## 引言
在连续介质力学的广阔领域中，准确描述物体的运动、变形与[内力](@entry_id:167605)是其核心任务。为了实现这一目标，物理学家和工程师发展出两种基本但截然不同的观察视角：追踪每个物质粒子运动轨迹的物质（拉格朗日）描述，以及在固定的空间点上观察物理量变化的空间（欧拉）描述。然而，如何在这两种视角之间建立严谨的数学联系，并利用这种联系来构建能够处理[大变形](@entry_id:167243)和复杂材料行为的物理模型，便构成了一个核心的知识挑战。

本文旨在系统地阐述这两种表示法的理论基础及其应用。我们将从**第一章：原理与机制**出发，借助[微分几何](@entry_id:145818)的语言，引入作为[几何变换](@entry_id:150649)核心的运动映射，并详细介绍“拉回”与“推前”运算如何作为系统性的工具，在不同描述框架下转换应变与应力等关键物理量。随后，在**第二章：应用与交叉学科联系**中，我们将展示这些理论工具在流体动力学、材料科学、生物物理学等前沿领域的具体应用，揭示它们如何帮助我们理解和建模[各向异性材料](@entry_id:184874)、[移动界面](@entry_id:141467)和复杂流动等现象。最后，通过**第三章：动手实践**中的一系列计算练习，读者将有机会亲手应用所学知识，将抽象的理论转化为具体的分析能力。

通过这一结构化的学习路径，本文将为读者构建一个从基本原理到前沿应用的完整知识体系，为深入研究[连续介质力学](@entry_id:155125)中的高级课题奠定坚实的几何与物理基础。

## 原理与机制

在对[连续介质运动学](@entry_id:747813)有了初步了解之后，本章将深入探讨其核心的数学原理与物理机制。我们将采用[微分几何](@entry_id:145818)的语言，系统地阐述物质（拉格朗日）描述与空间（欧拉）描述这两种基本视角。我们将看到，这两种描述方式并非孤立，而是通过一个称为运动映射的[几何变换](@entry_id:150649)紧密联系在一起。理解这种联系的关键在于掌握“拉回”与“推前”这两种对[张量场](@entry_id:190170)进行坐标变换的基本运算。基于此，我们将能够定义各种运动学和动力学量，如应变张量和[应力张量](@entry_id:148973)，并在不同描述框架下建立它们之间的转换关系。最后，我们将探讨这些工具在建立客观[本构关系](@entry_id:186508)和表述动力学[变分原理](@entry_id:198028)中的应用，从而为连续介质力学提供一个严谨而优美的几何框架。

### 运动映射：几何基础

[连续介质力学](@entry_id:155125)的核心在于描述物[质点](@entry_id:186768)如何随时间在空间中运动。我们将连续体在某一初始时刻（通常为 $t=0$）的构型称为**参考构型**或**物质构型**，并将其抽象为一个光滑、紧致、有向的 $n$ 维流形 $\mathcal{B}$（在典型应用中，$n=3$）。流形 $\mathcal{B}$ 上的点用**物质坐标** $\boldsymbol{X}$ 表示。连续体运动所处的物理空间则被模型化为另一个光滑的 $n$ 维流形 $\mathcal{S}$（通常为[欧几里得空间](@entry_id:138052) $\mathbb{R}^3$），其上的点用**空间坐标** $\boldsymbol{x}$ 表示。

连续体的运动由一个单参数映射族 $\boldsymbol{\varphi}: I \times \mathcal{B} \to \mathcal{S}$ 描述，其中 $I \subset \mathbb{R}$ 是一个时间区间。对于任意固定的时刻 $t \in I$，我们得到一个**运动映射** $\boldsymbol{\varphi}_t: \mathcal{B} \to \mathcal{S}$，它将每个物[质点](@entry_id:186768) $\boldsymbol{X} \in \mathcal{B}$ 映射到其在时刻 $t$ 的空间位置 $\boldsymbol{x} = \boldsymbol{\varphi}_t(\boldsymbol{X})$。

一个物理上可接受的运动必须满足两个基本条件：物质的不可穿透性和方向的保持。数学上，这要求运动映射 $\boldsymbol{\varphi}_t$ 对于每个时刻 $t$ 都是一个从 $\mathcal{B}$ 到其像 $\boldsymbol{\varphi}_t(\mathcal{B})$ 的**微分同胚**。微分同胚是一个光滑、可逆且其逆也光滑的映射。为保证这一点，需要满足以下条件 ：
1.  **正则性**：映射 $\boldsymbol{\varphi}_t$ 至少是 $\mathcal{C}^1$ 的，即连续可微。
2.  **[局部可逆性](@entry_id:143266)**：$\boldsymbol{\varphi}_t$ 的[微分](@entry_id:158422)（或切映射）在每一点都是可逆的。
3.  **全局[单射性](@entry_id:147722)**：$\boldsymbol{\varphi}_t$ 必须是[单射](@entry_id:183792)的，即不同的物[质点](@entry_id:186768) $\boldsymbol{X}_1 \neq \boldsymbol{X}_2$ 不能被映射到同一空间位置 $\boldsymbol{\varphi}_t(\boldsymbol{X}_1) \neq \boldsymbol{\varphi}_t(\boldsymbol{X}_2)$。

运动映射 $\boldsymbol{\varphi}_t$ 在物质点 $\boldsymbol{X}$ 的[微分](@entry_id:158422)，被称为**变形梯度**（deformation gradient），记为 $\boldsymbol{F}(\boldsymbol{X},t)$：
$$
\boldsymbol{F}(\boldsymbol{X},t) = \mathrm{D}\boldsymbol{\varphi}_t(\boldsymbol{X}) : T_{\boldsymbol{X}}\mathcal{B} \to T_{\boldsymbol{\varphi}_t(\boldsymbol{X})}\mathcal{S}
$$
这里，$T_{\boldsymbol{X}}\mathcal{B}$ 和 $T_{\boldsymbol{\varphi}_t(\boldsymbol{X})}\mathcal{S}$ 分别是流形 $\mathcal{B}$ 在点 $\boldsymbol{X}$ 和流形 $\mathcal{S}$ 在点 $\boldsymbol{x}=\boldsymbol{\varphi}_t(\boldsymbol{X})$ 的切空间。在坐标表示下，$\boldsymbol{F}$ 是一个矩阵，其分量为 $F^i{}_A = \partial \varphi_t^i / \partial X^A$。变形梯度 $\boldsymbol{F}$ 是运动学的核心，它描述了物质微元在变形过程中的局部拉伸和旋转。一个物质切向量（代表一个无限小的物质线元）$\boldsymbol{U} \in T_{\boldsymbol{X}}\mathcal{B}$ 通过变形被映射为一个空间[切向量](@entry_id:265494) $\boldsymbol{u} \in T_{\boldsymbol{x}}\mathcal{S}$，其关系为 $\boldsymbol{u} = \boldsymbol{F} \boldsymbol{U}$ 。

[局部可逆性](@entry_id:143266)条件等价于变形梯度的行列式，即**[雅可比行列式](@entry_id:137120)**（Jacobian）$J(\boldsymbol{X},t) = \det \boldsymbol{F}(\boldsymbol{X},t)$，在任何地方都不能为零。根据[反函数定理](@entry_id:275014)，若 $J \neq 0$，则 $\boldsymbol{\varphi}_t$ 在该点的一个邻域内是微分同胚。物理上，我们要求更强的条件 $J > 0$，这保证了变形不仅是局部可逆的，而且保持了物质微元的定向（例如，[右手坐标系](@entry_id:166669)不会被翻转成左手坐标系）。[雅可比行列式](@entry_id:137120) $J$ 的几何意义是局部体积变化的比例：一个无限小的物质体积元 $dV$ 在变形后，其对应的空间[体积元](@entry_id:267802) $dv$ 满足关系 $dv = J \, dV$ 。当 $J=1$ 时，运动是**不可压缩的**，即局部[体积保持](@entry_id:141001)不变。

全局[单射性](@entry_id:147722)结合[局部可逆性](@entry_id:143266)，并在 $\mathcal{B}$ 是[紧流形](@entry_id:158804)的条件下，可以借助（Hadamard）全局[反函数定理](@entry_id:275014)，保证 $\boldsymbol{\varphi}_t$ 是一个从 $\mathcal{B}$ 到其像 $\boldsymbol{\varphi}_t(\mathcal{B})$ 的全局微分同胚 。

### 物质与空间描述：两种视角

在连续介质力学中，描述一个物理量（如温度、密度、应力等）有两种基本的方式：

1.  **物质描述 (Material Description)** 或 **拉格朗日描述 (Lagrangian Description)**：这种方法跟踪每一个物[质点](@entry_id:186768) $\boldsymbol{X} \in \mathcal{B}$，并描述该物理量如何随时间 $t$ 变化。因此，一个拉格朗日场是一个定义在物质流形与时间上的函数，例如一个标量场 $f_L: \mathcal{B} \times \mathbb{R} \to \mathbb{R}$。

2.  **空间描述 (Spatial Description)** 或 **[欧拉描述](@entry_id:264722) (Eulerian Description)**：这种方法关注空间中的固定点 $\boldsymbol{x} \in \mathcal{S}$，并描述在该点处的物理量如何随时间 $t$ 变化（无论哪个物[质点](@entry_id:186768)恰好在该时刻经过此点）。因此，一个欧拉场是一个定义在空间流形与时间上的函数，例如一个标量场 $f_E: \mathcal{S} \times \mathbb{R} \to \mathbb{R}$。

这两种描述必须在物理上是一致的。在时刻 $t$，占据空间位置 $\boldsymbol{x} = \boldsymbol{\varphi}_t(\boldsymbol{X})$ 的物质点是 $\boldsymbol{X}$。因此，在 $\boldsymbol{X}$ 点的拉格朗日场的值必须等于在 $\boldsymbol{x}$ 点的欧拉场的值。这个基本关系可以表示为 ：
$$
f_L(\boldsymbol{X}, t) = f_E(\boldsymbol{\varphi}_t(\boldsymbol{X}), t)
$$
这个等式是连接两种描述的桥梁。利用运动映射的可逆性，我们也可以反过来表达欧拉场：
$$
f_E(\boldsymbol{x}, t) = f_L(\boldsymbol{\varphi}_t^{-1}(\boldsymbol{x}), t)
$$
这里 $\boldsymbol{\varphi}_t^{-1}: \boldsymbol{\varphi}_t(\mathcal{B}) \to \mathcal{B}$ 是运动映射的逆，它告诉我们占据空间位置 $\boldsymbol{x}$ 的物[质点](@entry_id:186768)是哪一个。

在微分几何的语言中，上述关系可以用**拉回**（pullback）运算来简洁地表述。对于一个固定的时刻 $t$，拉格朗日[标量场](@entry_id:151443) $f_L(\cdot, t)$ 是欧拉标量场 $f_E(\cdot, t)$ 被运动映射 $\boldsymbol{\varphi}_t$ **拉回**的结果，记为 $f_L(\cdot, t) = \boldsymbol{\varphi}_t^* f_E(\cdot, t)$。反之，欧拉场是拉格朗日场被逆映射 $\boldsymbol{\varphi}_t^{-1}$ **拉回**的结果，即 $f_E(\cdot, t) = (\boldsymbol{\varphi}_t^{-1})^* f_L(\cdot, t)$ 。

### 张量的输运：拉回与推前

拉回和推前的概念可以推广到任意类型的[张量场](@entry_id:190170)，为在物质构型和空间构型之间转换物理量提供了系统的工具 。

- **标量场 (Scalars)**：如前所述，标量场的拉回是与映射的复合：$(\boldsymbol{\varphi}_t^* f)(\boldsymbol{X}) = f(\boldsymbol{\varphi}_t(\boldsymbol{X}))$。标量场的**推前**（pushforward）则是与逆映射的复合：$(\boldsymbol{\varphi}_{t*} g)(\boldsymbol{x}) = g(\boldsymbol{\varphi}_t^{-1}(\boldsymbol{x}))$。

- **矢量场 (Vectors)**：矢量是切空间中的元素，它们的变换由切映射（即变形梯度 $\boldsymbol{F}$）决定。
    - **推前**：一个物质矢量场 $\boldsymbol{V}(\boldsymbol{X})$ 被**推前**为[空间矢量](@entry_id:1132014)场 $(\boldsymbol{\varphi}_{t*}\boldsymbol{V})(\boldsymbol{x})$，其变换规则为：
      $$
      (\boldsymbol{\varphi}_{t*}\boldsymbol{V})(\boldsymbol{x}) = \boldsymbol{F}(\boldsymbol{X}) \boldsymbol{V}(\boldsymbol{X}), \quad \text{其中 } \boldsymbol{X} = \boldsymbol{\varphi}_t^{-1}(\boldsymbol{x})
      $$
    - **拉回**：一个[空间矢量](@entry_id:1132014)场 $\boldsymbol{v}(\boldsymbol{x})$ 被**拉回**为物质矢量场 $(\boldsymbol{\varphi}_t^*\boldsymbol{v})(\boldsymbol{X})$，其变换规则由逆映射的切映射（即 $\boldsymbol{F}^{-1}$）给出：
      $$
      (\boldsymbol{\varphi}_t^*\boldsymbol{v})(\boldsymbol{X}) = \boldsymbol{F}(\boldsymbol{X})^{-1} \boldsymbol{v}(\boldsymbol{\varphi}_t(\boldsymbol{X}))
      $$

- **[余矢量场](@entry_id:186855) (Covectors / 1-forms)**：[余矢量](@entry_id:157727)（或[1-形式](@entry_id:270392)）是作用于矢量的线性函数，它们的变换规则由对偶性确定，以保持与矢量的[内积](@entry_id:750660)不变。
    - **拉回**：一个空间[余矢量场](@entry_id:186855) $\boldsymbol{a}(\boldsymbol{x})$ 被**拉回**为物质[余矢量场](@entry_id:186855) $(\boldsymbol{\varphi}_t^*\boldsymbol{a})(\boldsymbol{X})$，其变换规则为：
      $$
      (\boldsymbol{\varphi}_t^*\boldsymbol{a})(\boldsymbol{X}) = \boldsymbol{F}(\boldsymbol{X})^{\mathsf{T}} \boldsymbol{a}(\boldsymbol{\varphi}_t(\boldsymbol{X}))
      $$
      其中 $\boldsymbol{F}^{\mathsf{T}}$ 是 $\boldsymbol{F}$ 的转置。
    - **推前**：一个物质[余矢量场](@entry_id:186855) $\boldsymbol{A}(\boldsymbol{X})$ 被**推前**为空间[余矢量场](@entry_id:186855) $(\boldsymbol{\varphi}_{t*}\boldsymbol{A})(\boldsymbol{x})$，变换规则为：
      $$
      (\boldsymbol{\varphi}_{t*}\boldsymbol{A})(\boldsymbol{x}) = \boldsymbol{F}(\boldsymbol{X})^{-\mathsf{T}} \boldsymbol{A}(\boldsymbol{X}), \quad \text{其中 } \boldsymbol{X} = \boldsymbol{\varphi}_t^{-1}(\boldsymbol{x})
      $$
      其中 $\boldsymbol{F}^{-\mathsf{T}} = (\boldsymbol{F}^{-1})^{\mathsf{T}}$。

- **[高阶张量](@entry_id:200122)场 (Higher-Order Tensors)**：对于一个一般的 $(r,s)$ 型张量（有 $r$ 个逆变指标和 $s$ 个[协变](@entry_id:634097)指标），其拉回和推前运算遵循对每个指标应用相应变换规则的原则。例如，一个物质张量 $\boldsymbol{T}$ 的推前 $(\boldsymbol{\varphi}_{t*}\boldsymbol{T})$，其每个逆变（上）指标都像矢量一样用 $\boldsymbol{F}$ 变换，而每个[协变](@entry_id:634097)（下）指标则像[余矢量](@entry_id:157727)一样用 $\boldsymbol{F}^{-\mathsf{T}}$ (或分量形式的 $\boldsymbol{F}^{-1}$) 变换。

利用这些工具，我们可以理解一些重要的几何量和运动学量是如何在两种描述之间转换的。

**[面积元](@entry_id:263205)与[Nanson公式](@entry_id:195566)**：一个物质面元，由其法向量 $\boldsymbol{N}$ 和面积 $dA$ 描述，其在空间构型中的对应物（法向量 $\boldsymbol{n}$ 和面积 $da$）由著名的**[Nanson公式](@entry_id:195566)**给出 ：
$$
\boldsymbol{n} \, da = J \, \boldsymbol{F}^{-\mathsf{T}} \boldsymbol{N} \, dA
$$
这个公式在推导[应力张量](@entry_id:148973)的关系时至关重要。

**度量张量与应变张量**：应变是衡量变形中局部长度和角度变化的量。在几何观点下，应变可以理解为度量张量的变化。
- **右柯西-格林变形张量 (Right Cauchy-Green Tensor)**：$\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$。它可以被看作是空间中的标准[欧几里得度量](@entry_id:147197)（单位张量 $\boldsymbol{I}$）被运动映射 $\boldsymbol{\varphi}_t$ **拉回**到物质构型的结果。$\boldsymbol{C}$ 完全在物质构型上定义，它衡量了物质[线元](@entry_id:196833)在变形后长度的平方变化。
- **左柯西-格林变形张量 (Left Cauchy-Green Tensor)**：$\boldsymbol{b} = \boldsymbol{F}\boldsymbol{F}^{\mathsf{T}}$。它可以被看作是物质构型中的标准度量被**推前**到空间构型的结果。

基于这两个张量，我们可以定义两个核心的[应变度量](@entry_id:755495) ：
- **[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange Strain Tensor)**：
  $$
  \boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I})
  $$
  $\boldsymbol{E}$ 是一个纯粹的**物质应变张量**，它将变形后的度量 $\boldsymbol{C}$与原始度量 $\boldsymbol{I}$进行比较。如果 $\boldsymbol{E}=\boldsymbol{0}$，则没有发生应变（仅有[刚体转动](@entry_id:191086)）。
- **[阿尔曼西应变](@entry_id:191140)张量 (Almansi Strain Tensor)**：
  $$
  \boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{b}^{-1})
  $$
  $\boldsymbol{e}$ 是一个纯粹的**空间应变张量**，它将参考度量（通过 $\boldsymbol{b}^{-1}$ 体现）与当前空间度量 $\boldsymbol{I}$进行比较。

举一个具体的例子，考虑一个二维变形 $x_1 = X_1 + a X_1 X_2, x_2 = (1+b X_1)X_2$。通过计算变形梯度 $\boldsymbol{F}$，我们可以显式地计算出 $\boldsymbol{E}$ 和 $\boldsymbol{e}$ 。我们会发现 $\boldsymbol{E}$ 是物质坐标 $(X_1, X_2)$ 的函数，而 $\boldsymbol{e}$（在通过逆映射表达后）也是物质坐标的函数，但它们的函数形式完全不同。这凸显了两种[应变度量](@entry_id:755495)虽然都描述了变形，但它们是基于不同的参考框架。在小变形情况下，它们都近似等于[位移梯度](@entry_id:165352)的对称部分，但在[大变形](@entry_id:167243)下则有显著差异。

### 变化率：物质与空间时间导数

描述物理量如何随时间演化是动力学的核心。同样，我们有两种不同的时间导数。

对于一个[标量场](@entry_id:151443)，我们已经看到拉格朗日场 $f_L(\boldsymbol{X},t)$ 和欧拉场 $f_E(\boldsymbol{x},t)$ 的关系。对一个固定的物质点 $\boldsymbol{X}$，其物理量的变化率是**[物质时间导数](@entry_id:190892)**（material time derivative），记为 $D/Dt$ 或 $\dot{f}_L$。通过对关系式 $f_L(\boldsymbol{X},t) = f_E(\boldsymbol{\varphi}_t(\boldsymbol{X}), t)$ 关于时间 $t$ 求导，并利用[链式法则](@entry_id:190743)，我们得到 ：
$$
\frac{D f_E}{D t} := \frac{d}{dt} f_L(\boldsymbol{X},t) = \frac{\partial f_E}{\partial t} + (\nabla_{\boldsymbol{x}} f_E) \cdot \frac{\partial \boldsymbol{\varphi}_t(\boldsymbol{X})}{\partial t}
$$
其中 $\partial f_E / \partial t$ 是欧拉场在固定空间点的**[局部时](@entry_id:194383)间导数**，$\nabla_{\boldsymbol{x}} f_E$ 是欧拉场的空间梯度，而 $\boldsymbol{v}(\boldsymbol{x},t) = \partial \boldsymbol{\varphi}_t(\boldsymbol{X}) / \partial t$ 是物[质点](@entry_id:186768) $\boldsymbol{X}$ 在其当前位置 $\boldsymbol{x}$ 的**[空间速度](@entry_id:190294)**。因此，[物质导数](@entry_id:262900)与局部导数的关系是：
$$
\frac{D f_E}{D t} = \frac{\partial f_E}{\partial t} + \boldsymbol{v} \cdot \nabla_{\boldsymbol{x}} f_E
$$
第二项 $\boldsymbol{v} \cdot \nabla_{\boldsymbol{x}} f_E$ 被称为**对流项**，它描述了由于物质点移动到梯度非零的区域而引起的变化。

对于一般的[张量场](@entry_id:190170)，简单的时间求导在几何上是无定义的，因为不同时刻的张量位于不同点的[切空间](@entry_id:199137)中，无法直接相减。我们需要一个在[欧拉描述](@entry_id:264722)下客观地衡量变化率的工具，这就是**[李导数](@entry_id:171745)**（Lie derivative）。一个[张量场](@entry_id:190170) $\boldsymbol{T}$ 沿[空间速度](@entry_id:190294)场 $\boldsymbol{v}$ 的[李导数](@entry_id:171745) $\mathcal{L}_{\boldsymbol{v}} \boldsymbol{T}$ 描述了当 $\boldsymbol{T}$ 被 $\boldsymbol{v}$ 的流拖拽时，其在空间框架下的变化率。其严格定义为 ：
$$
\mathcal{L}_{\boldsymbol{v}} \boldsymbol{T} = \left.\frac{d}{dt}\right|_{t=0} \Phi_t^* \boldsymbol{T}
$$
其中 $\Phi_t$ 是由速度场 $\boldsymbol{v}$ 生成的局部流映射。[李导数](@entry_id:171745)的一个重要特性是它不依赖于任何特定的联络或度量，是一个纯粹的几何概念。

[李导数](@entry_id:171745)对于不同类型的张量有具体的计算公式 ：
- 对于矢量场 $\boldsymbol{w}$，[李导数](@entry_id:171745)等于两个矢量场的**李括号**：$(\mathcal{L}_{\boldsymbol{v}} \boldsymbol{w})^i = [\boldsymbol{v}, \boldsymbol{w}]^i = v^j \partial_j w^i - w^j \partial_j v^i$。
- 对于[微分形式](@entry_id:146747) $\omega$（例如[余矢量](@entry_id:157727)），[李导数](@entry_id:171745)由优美的**[嘉当公式](@entry_id:157961)**给出：$\mathcal{L}_{\boldsymbol{v}} \omega = d(\iota_{\boldsymbol{v}} \omega) + \iota_{\boldsymbol{v}}(d\omega)$，其中 $d$ 是外微分，$\iota_{\boldsymbol{v}}$ 是[内积](@entry_id:750660)。对于[1-形式](@entry_id:270392) $\alpha$，其分量形式为 $(\mathcal{L}_{\boldsymbol{v}} \alpha)_i = v^j \partial_j \alpha_i + \alpha_j \partial_i v^j$。

如果一个欧拉场 $a(t)$ 满足[输运方程](@entry_id:174281) $\partial_t a + \mathcal{L}_{\boldsymbol{v}} a = 0$，我们称之为一个**被动输运场**（advected field）。这等价于说该场在物质描述下是恒定的，即 $\frac{d}{dt}(\boldsymbol{\varphi}_t^* a(t)) = 0$ 。这意味着该物理量“冻结”在物质中并随之运动。一个重要的例子是质量守恒。如果我们将质量密度视为一个密度形式 $\mu = \rho \, dV_g$，那么其被动输运条件 $\partial_t \mu + \mathcal{L}_{\boldsymbol{v}} \mu = 0$ 等价于我们所熟知的**[连续性方程](@entry_id:195013)** $\partial_t \rho + \nabla \cdot (\rho \boldsymbol{v}) = 0$ 。

### 在本构模型和动力学中的应用

物质与空间描述的框架为建立本构关系和动力学方程提供了基础。

#### [应力张量](@entry_id:148973)

应力描述了物体内部的相互作用力。与应变一样，应力也可以在物质或空间框架中定义，从而产生几种不同的应力张量 。

- **柯西[应力张量](@entry_id:148973) (Cauchy Stress Tensor)** $\boldsymbol{\sigma}$：这是一个**[空间张量](@entry_id:185799)**，定义在当前构型上。它将空间面元[法向量](@entry_id:264185) $\boldsymbol{n}$ 映射为该面元上的力矢量（面力）$\boldsymbol{t}$：$\boldsymbol{t} = \boldsymbol{\sigma} \boldsymbol{n}$。在没有体力矩的情况下，动量矩守恒要求 $\boldsymbol{\sigma}$ 是对称的。

- **[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量 (First Piola-Kirchhoff Stress Tensor)** $\boldsymbol{P}$：这是一个**两点张量**，它将参考构型中的[法向量](@entry_id:264185) $\boldsymbol{N}$ 映射为空间构型中的力矢量。它通过[力平衡](@entry_id:267186)关系 $\boldsymbol{t} \, da = \boldsymbol{T}_R \, dA$ 与柯西应力联系起来，其中 $\boldsymbol{T}_R = \boldsymbol{P} \boldsymbol{N}$ 是参考面力。利用[Nanson公式](@entry_id:195566)，可以推导出 $\boldsymbol{P}$ 和 $\boldsymbol{\sigma}$ 之间的关系：
  $$
  \boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-\mathsf{T}}
  $$
  $\boldsymbol{P}$ 通常是不对称的。它的物理意义是：第一列是作用在变形后 $X_1$ 方向单位面积上的力。

- **[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量 (Second Piola-Kirchhoff Stress Tensor)** $\boldsymbol{S}$：这是一个**物质张量**，完全定义在参考构型上。它通过将 $\boldsymbol{P}$ 张量拉回到参考构型来定义：
  $$
  \boldsymbol{S} = \boldsymbol{F}^{-1} \boldsymbol{P} = J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-\mathsf{T}}
  $$
  如果柯西应力 $\boldsymbol{\sigma}$ 是对称的，那么 $\boldsymbol{S}$ 也必然是对称的。$\boldsymbol{S}$ 的一个重要特性是它与[格林-拉格朗日应变](@entry_id:170427) $\boldsymbol{E}$ 在能量上是共轭的，即[应力功率](@entry_id:182907)可以表示为 $\boldsymbol{S}:\dot{\boldsymbol{E}}$。

#### [标架无关性原理](@entry_id:200995)

本构关系描述了材料的力学响应（如应力）如何依赖于变形（如应变）。一个基本的物理要求是**[标架无关性原理](@entry_id:200995)**（principle of frame indifference），也称为**[客观性原理](@entry_id:185412)**（principle of objectivity）。该原理指出，本构关系不能依赖于观察者的[刚体运动](@entry_id:144691) 。

一个叠加在当前运动上的[刚体运动](@entry_id:144691)（旋转 $\boldsymbol{Q}(t)$ 和平移 $\boldsymbol{c}(t)$）会使变形梯度变换为 $\boldsymbol{F}^* = \boldsymbol{Q} \boldsymbol{F}$。标架无关性要求材料的[储能函数](@entry_id:197811) $W$ 在这种变换下不变，即 $W(\boldsymbol{F}) = W(\boldsymbol{F}^*) = W(\boldsymbol{Q}\boldsymbol{F})$。
要满足这个条件，一个充分的方式是要求 $W$ 仅通过[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$ 依赖于变形。这是因为 $\boldsymbol{C}$ 在这种变换下是不变的：
$$
\boldsymbol{C}^* = (\boldsymbol{F}^*)^{\mathsf{T}}\boldsymbol{F}^* = (\boldsymbol{Q}\boldsymbol{F})^{\mathsf{T}}(\boldsymbol{Q}\boldsymbol{F}) = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}\boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{I}\boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = \boldsymbol{C}
$$
因此，任何形式为 $W(\boldsymbol{F}) = \hat{W}(\boldsymbol{C})$ 的[储能函数](@entry_id:197811)都自动满足标架无关性。这为建立客观的[超弹性本构模型](@entry_id:191665)提供了标准方法。例如，[第二皮奥拉-基尔霍夫应力](@entry_id:173163)可以客观地定义为 $\boldsymbol{S} = 2 \frac{\partial \hat{W}}{\partial \boldsymbol{C}}$。

需要注意的是，标架无关性是一个普适的物理公理，而**[材料对称性](@entry_id:190289)**（如各向同性）是材料自身的属性。各向同性要求 $W(\boldsymbol{F}) = W(\boldsymbol{F}\boldsymbol{R})$ 对于所有旋转 $\boldsymbol{R}$ 都成立，这会进一步将 $\hat{W}(\boldsymbol{C})$ 限制为仅依赖于 $\boldsymbol{C}$ 的[主不变量](@entry_id:193522)的函数 。

#### 变分原理与相容性

物质描述框架在表述力学原理时特别有效，因为它提供了一个固定的、不随时间变化的积分域。一个强大的例子是用于[弹性动力学](@entry_id:175818)的**[哈密顿原理](@entry_id:175601)**（Hamilton's Principle）。

对于一个[超弹性](@entry_id:159356)体，其[作用量泛函](@entry_id:169216) $S[\boldsymbol{\varphi}]$ 可以定义为动能和势能之差对时间的积分：
$$
S[\boldsymbol{\varphi}]=\int_{t_0}^{t_1}\int_{\mathcal{B}} \left( \frac{1}{2}\rho_0 \|\dot{\boldsymbol{\varphi}}(\boldsymbol{X},t)\|^2 - W(\boldsymbol{F}(\boldsymbol{X},t)) \right) dX\,dt
$$
其中，$\rho_0$ 是参考密度，$\dot{\boldsymbol{\varphi}}$ 是物质速度，$W(\boldsymbol{F})$ 是单位参考体积的储能密度。所有量都在参考构型 $\mathcal{B}$ 上定义。[哈密顿原理](@entry_id:175601)指出，真实的运动路径使得作用量 $S[\boldsymbol{\varphi}]$ 的变分为零，即 $\delta S = 0$。

通过对该泛函进行变分计算，我们可以同时得到系统的[运动方程](@entry_id:264286)和自然边界条件。其结果是物质描述下的动量守恒方程 ：
$$
\rho_0 \ddot{\boldsymbol{\varphi}} = \operatorname{Div} \boldsymbol{P}
$$
其中 $\operatorname{Div}$ 是物质散度算子，而 $\boldsymbol{P} = \frac{\partial W}{\partial \boldsymbol{F}}$ 是[第一皮奥拉-基尔霍夫应力](@entry_id:163971)。这个方程优雅地将牛顿第二定律（左侧的惯性项）与内力（右侧的应力散度）联系起来。

最后，值得一提的是**[相容性条件](@entry_id:637057)**（compatibility condition）。并非任意一个[二阶张量](@entry_id:199780)场 $\boldsymbol{F}(\boldsymbol{X})$ 都能成为某个位移场 $\boldsymbol{\varphi}(\boldsymbol{X})$ 的梯度。正如一个矢量场若想成为一个标量[势的梯度](@entry_id:268447)，其旋度必须为零一样，一个[张量场](@entry_id:190170) $\boldsymbol{F}$ 若想成为一个变形梯度，它也必须满足一定的[微分](@entry_id:158422)约束。在单连通区域 $\Omega$ 中，这个条件是 $\boldsymbol{F}$ 的物质旋度（对每一行分别求旋度）为零 ：
$$
\operatorname{Curl}_{\boldsymbol{X}} \boldsymbol{F} = \boldsymbol{0}
$$
这个条件保证了从 $\boldsymbol{F}$ 积分得到的位移场 $\boldsymbol{\varphi}$ 是单值的，从而确保了变形的连续性和完整性。

本章通过几何的视角，系统地建立了[连续介质力学](@entry_id:155125)的运动学和动力学框架。掌握物质与空间描述及其转换关系，是深入理解和研究固体与流体力学中各种复杂现象的基石。