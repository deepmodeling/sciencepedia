## 引言
在[连续介质力学](@entry_id:155125)领域，对物体运动与变形的精确描述是所有后续分析的基石。无论是预测桥梁在载荷下的挠度，模拟飞机的空气动力学行为，还是理解生物组织的生长，我们都需要一个严谨的数学框架来量化物质如何随时间改变其形状和位置。这个框架的核心挑战在于，如何清晰地区分物质本身（物质点）与它所占据的空间，并建立两者之间的联系。

本文旨在系统性地构建这一[运动学](@entry_id:173318)理论。我们将从最基本的概念出发，揭示看似抽象的数学工具如何与真实的物理现象紧密相连。在学习过程中，读者将掌握从宏观运动到局部变形的完整描述方法，并理解其背后的物理约束和数学原理。

文章将分为三个核心部分。在“原理与机制”一章中，我们将建立运动学的基本语言，介绍构形、运动映射、变形梯度等核心概念。接下来，“应用与交叉学科联系”一章将展示这些原理如何在[固体力学](@entry_id:164042)、[材料科学](@entry_id:152226)、[计算力学](@entry_id:174464)等多个领域中发挥关键作用。最后，“动手实践”部分将通过具体问题，帮助读者将理论知识转化为解决实际问题的能力。

让我们从第一步开始，深入探索描述连续体运动的基本原理与机制。

## 原理与机制

在连续介质力学中，精确描述一个物体的运动和变形是所有后续分析的基础。这需要一个严谨的数学框架，用以区分物质本身和它所占据的空间，并量化其形状随时间的变化。本章将系统地阐述描述连续体[运动学](@entry_id:173318)的核心原理与机制，从最基本的构形与映射概念出发，逐步深入到变形、速度、加速度的度量，并最终探讨协调性与客观性等高等[运动学](@entry_id:173318)原理。

### 运动的运动学描述

为了建立一个精确的理论，我们必须首先区分三个基本概念：物体、空间和构形。

一个**物体**（body），记为 $\mathcal{B}$，被理想化为一个由无数**物质点**（material points）或粒子（particles）组成的集合。这些物质点是物体的基本组成单元，它们在时间流逝中保持其自身的同一性。重要的是要理解，物[质点](@entry_id:186768)是一个抽象的标签，而不是空间中的一个位置。

我们所处的物理**空间**（space）被建模为一个三维欧几里得空间 $\mathbb{R}^3$。空间中的点被称为**空间点**（spatial points），用[坐标向量](@entry_id:153319) $\boldsymbol{x} \in \mathbb{R}^3$ 表示。

一个**构形**（configuration）是物体在某一时刻的几何形状和空间位置，它通过一个称为**安置**（placement）的映射 $\kappa$ 来定义。该映射将每一个抽象的物质点 $P \in \mathcal{B}$ 赋予一个唯一的空间位置 $\boldsymbol{x} = \kappa(P)$。因此，构形是物体 $\mathcal{B}$ 在空间 $\mathbb{R}^3$ 中的一个“快照”。

为了进行计算，直接处理抽象的物质点集合 $\mathcal{B}$ 是不方便的。因此，我们引入**参考构形**（reference configuration）的概念。我们选取物体在某个特定时刻（通常是 $t=0$）的一个构形作为基准，记为 $\mathcal{B}_0$。这个参考构形是物体在 $\mathbb{R}^3$ 中占据的一个确定区域。一旦选定，我们就用一个物[质点](@entry_id:186768)在参考构形中的位置向量 $\boldsymbol{X} \in \mathcal{B}_0$ 来作为这个物[质点](@entry_id:186768)的永久标签。这个向量 $\boldsymbol{X}$ 被称为**物质坐标**（material coordinate）或**拉格朗日坐标**（Lagrangian coordinate）。对于一个给定的物质点，其物质坐标 $\boldsymbol{X}$ 是不随时间变化的。[@problem_id:2658138]

与之相对，物体在任意时刻 $t$ 所占据的空间区域被称为**当前构形**（current configuration），记为 $\mathcal{B}_t$。当前构形中的点用**空间坐标**（spatial coordinate）或**欧拉坐标**（Eulerian coordinate）$\boldsymbol{x}$ 表示。显然，同一个物[质点](@entry_id:186768)在不同时刻会占据不同的空间位置。

物体的**运动**（motion）被描述为一系列随时间连续变化的构形。数学上，这通过一个**运动映射**（motion map） $\boldsymbol{\chi}$ 来实现。这个映射建立了[物质坐标与空间坐标](@entry_id:751726)之间的关系：
$$ \boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{X}, t) $$
该方程表明，在参考构形中被标记为 $\boldsymbol{X}$ 的物质点，在时刻 $t$ 会运动到空间位置 $\boldsymbol{x}$。因此，运动映射 $\boldsymbol{\chi}$ 的定义域是参考构形与时间区间的笛卡尔积 $\mathcal{B}_0 \times I$，而其值域则是空间 $\mathbb{R}^3$。[@problem_id:2658076] [@problem_id:2658005] 对于一个固定的物质点 $\boldsymbol{X}$，函数 $t \mapsto \boldsymbol{\chi}(\boldsymbol{X}, t)$ 描绘了该点在空间中随时间变化的轨迹。

### 运动的基本公理与性质

物理上的合理性对运动映射 $\boldsymbol{\chi}$ 施加了若干基本限制，这些限制构成了运动学的基本公理。

首先是**物质不可入性**（impenetrability of matter）公理。该公理指出，在同一时刻，两个不同的物质点不能占据同一个空间位置。这对应于数学上的要求：对于任意固定的时刻 $t$，运动映射 $\boldsymbol{\chi}(\cdot, t)$ 必须是**[单射](@entry_id:183792)**（injective）的。即，若 $\boldsymbol{X}_1 \neq \boldsymbol{X}_2$，则必须有 $\boldsymbol{\chi}(\boldsymbol{X}_1, t) \neq \boldsymbol{\chi}(\boldsymbol{X}_2, t)$。如果违反了这一条，意味着物质发生了自我穿透，这在经典单组分连续体理论中是不允许的。不满足[单射性](@entry_id:147722)会导致在重叠点处的速度、应力等物理场出现多值，从而使理论失效。[@problem_id:2658138] [@problem_id:2658098]

其次，为了保证速度、加速度以及变形度量的存在性和连续性，我们通常要求运动映射 $\boldsymbol{\chi}(\boldsymbol{X}, t)$ 具有足够的**正则性**（regularity），即光滑性。一个标准假设是，$\boldsymbol{\chi}$ 关于其两个变量 $\boldsymbol{X}$ 和 $t$ 至少是连续可微的（$C^1$ 类）。对 $\boldsymbol{X}$ 的可微性保证了我们可以定义变形的局部度量，而对 $t$ 的[可微性](@entry_id:140863)则保证了速度场是良定义的。[@problem_id:2658076]

虽然[单射性](@entry_id:147722)是全局要求，但在数学上，确保一个映射在整个定义域上是单射的可能非常复杂。一个重要的局部条件是 $\det(\nabla_{\boldsymbol{X}} \boldsymbol{\chi}) > 0$，但这本身并不足以保证全局单射。在非线性弹性力学的现代研究中，数学家们发展了更复杂的条件来保证全局[单射性](@entry_id:147722)，例如，在特定假设下，满足 Ciarlet-Nečas 条件的映射可以被证明是全局[单射](@entry_id:183792)的，从而为理论的数学严谨性提供了坚实基础。[@problem_id:2658098]

### 变形的局部度量

运动映射 $\boldsymbol{\chi}$ 完整地描述了物体的全局运动。然而，在力学中，我们更关心的是材料的局部变形，即物体内部的拉伸、剪切和旋转。这些信息包含在运动映射的空间导数中。

**变形梯度**（deformation gradient）张量 $\boldsymbol{F}$ 定义为运动映射 $\boldsymbol{\chi}$ 对物质坐标 $\boldsymbol{X}$ 的梯度：
$$ \boldsymbol{F}(\boldsymbol{X}, t) = \frac{\partial \boldsymbol{\chi}(\boldsymbol{X}, t)}{\partial \boldsymbol{X}} \quad \text{或} \quad F_{iJ} = \frac{\partial \chi_i}{\partial X_J} $$
变形梯度 $\boldsymbol{F}$ 是一个[二阶张量](@entry_id:199780)，它包含了关于材料在点 $\boldsymbol{X}$ 邻域内变形的全部信息。其核心几何意义是：它将参考构形中的一个无限小物质线元 $d\boldsymbol{X}$ 线性地映射到当前构形中对应的空间[线元](@entry_id:196833) $d\boldsymbol{x}$。
$$ d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X} $$
这意味着 $\boldsymbol{F}$ 描述了材料纤维的局部拉伸和旋转。[@problem_id:2658002]

变形梯度的[行列式](@entry_id:142978)被称为**雅可比行列式**（Jacobian determinant），记为 $J$：
$$ J(\boldsymbol{X}, t) = \det \boldsymbol{F}(\boldsymbol{X}, t) $$
$J$ 的几何意义是局部体积变化的比例。一个在参考构形中体积为 $dV$ 的无限小单元，在当前构形中其体积 $dv$ 将变为：
$$ dv = J dV $$
为了保证物质不会被压缩成零体积或“由内向外”翻转，我们要求运动保持**方向**（orientation-preserving），这在数学上体现为 $J > 0$。这个条件也保证了变形梯度 $\boldsymbol{F}$ 是局部可逆的。[@problem_id:2658002]

与变形梯度相关的还有其他重要的变形度量。例如，**[右柯西-格林张量](@entry_id:174156)**（right Cauchy-Green tensor）定义为 $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$。它是一个[对称正定](@entry_id:145886)张量，完全由材料的局部拉伸确定，与刚性转动无关。它的[行列式](@entry_id:142978)与[雅可比行列式](@entry_id:137120)之间存在关系 $\det \boldsymbol{C} = (\det \boldsymbol{F})^2 = J^2$。此外，无限小面积元的变换由著名的**[南森公式](@entry_id:195566)**（Nanson's formula）给出：$d\boldsymbol{a} = J \boldsymbol{F}^{-\mathsf{T}} d\boldsymbol{A}$，其中 $d\boldsymbol{A}$ 和 $d\boldsymbol{a}$ 分别是参考构形和当前构形中[有向面积](@entry_id:169588)元。[@problem_id:2658002]

### 速度与加速度

运动学不仅要描述物体在某一时刻的构形，还要描述其变化率。

**物质速度**（material velocity）$\boldsymbol{V}$ 定义为固定物[质点](@entry_id:186768) $\boldsymbol{X}$ 的位置随时间的变化率：
$$ \boldsymbol{V}(\boldsymbol{X}, t) = \frac{\partial \boldsymbol{\chi}(\boldsymbol{X}, t)}{\partial t} $$
它描述的是“跟随一个特定物[质粒](@entry_id:263777)子运动”时观察到的速度。类似地，**[物质加速度](@entry_id:270992)**（material acceleration）$\boldsymbol{A}$ 是物质速度对时间的变化率：
$$ \boldsymbol{A}(\boldsymbol{X}, t) = \frac{\partial \boldsymbol{V}(\boldsymbol{X}, t)}{\partial t} = \frac{\partial^2 \boldsymbol{\chi}(\boldsymbol{X}, t)}{\partial t^2} $$
物质描述中的求导相对简单，因为[自变量](@entry_id:267118) $\boldsymbol{X}$ 是固定的。[@problem_id:2658107]

然而，在许多情况下（尤其是在[流体力学](@entry_id:136788)中），我们更关心在固定的**空间点** $\boldsymbol{x}$ 处速度是多少。这引出了**[空间速度](@entry_id:190294)**（spatial velocity）场 $\boldsymbol{v}(\boldsymbol{x}, t)$ 的概念。它与物质速度的关系通过以下方式建立：在时刻 $t$ 占据空间点 $\boldsymbol{x}$ 的那个物质点，其速度就是 $\boldsymbol{v}(\boldsymbol{x}, t)$。数学上：
$$ \boldsymbol{v}(\boldsymbol{\chi}(\boldsymbol{X}, t), t) = \boldsymbol{V}(\boldsymbol{X}, t) $$
同理，**空间加速度**（spatial acceleration）$\boldsymbol{a}(\boldsymbol{x}, t)$ 也通过类似的方式定义：$\boldsymbol{a}(\boldsymbol{\chi}(\boldsymbol{X}, t), t) = \boldsymbol{A}(\boldsymbol{X}, t)$。[@problem_id:2658005] [@problem_id:2658107]

一个核心的问题是，如何从[空间速度](@entry_id:190294)场 $\boldsymbol{v}(\boldsymbol{x}, t)$ 计算出空间[加速度场](@entry_id:266595) $\boldsymbol{a}(\boldsymbol{x}, t)$？简单地对 $\boldsymbol{v}$ 求时间[偏导数](@entry_id:146280)是不够的，因为它没有考虑物[质点](@entry_id:186768)正在流过空间点 $\boldsymbol{x}$ 这一事实。正确的表达式通过链式法则得到，这个过程定义了**物质导数**（material derivative） $D/Dt$：
$$ \boldsymbol{a}(\boldsymbol{x}, t) = \frac{D\boldsymbol{v}}{Dt} (\boldsymbol{x}, t) = \frac{\partial \boldsymbol{v}(\boldsymbol{x}, t)}{\partial t} + (\nabla_{\boldsymbol{x}}\boldsymbol{v}(\boldsymbol{x}, t)) \boldsymbol{v}(\boldsymbol{x}, t) $$
上式是[连续介质运动学](@entry_id:747813)中最基本的恒等式之一。它表明，一个物质点的加速度（左侧）由两部分组成：在固定空间点观察到的速度变化率（$\partial \boldsymbol{v}/\partial t$，称为**[局部加速度](@entry_id:272847)**）和由于粒子运动到速度不同的新位置而产生的加速度（$(\nabla_{\boldsymbol{x}}\boldsymbol{v})\boldsymbol{v}$，称为**[对流加速度](@entry_id:263153)**）。其中 $\nabla_{\boldsymbol{x}}\boldsymbol{v}$ 是[空间速度梯度](@entry_id:187198)。

例如，考虑一个均匀变形的运动 $\boldsymbol{\chi}(\boldsymbol{X}, t) = \boldsymbol{F}(t)\boldsymbol{X} + \boldsymbol{c}(t)$。通过直接计算可以验证，其[空间速度](@entry_id:190294)场为 $\boldsymbol{v}(\boldsymbol{x}, t) = \dot{\boldsymbol{F}}(t)\boldsymbol{F}^{-1}(t)(\boldsymbol{x} - \boldsymbol{c}(t)) + \dot{\boldsymbol{c}}(t)$，[空间速度梯度](@entry_id:187198)为 $\nabla_{\boldsymbol{x}} \boldsymbol{v} = \dot{\boldsymbol{F}}(t)\boldsymbol{F}^{-1}(t)$，而空间[加速度场](@entry_id:266595) $\boldsymbol{a}(\boldsymbol{x}, t)$ 确实满足上述物质导数公式。[@problem_id:2658107]

### 基本原理与高等概念

在掌握了[运动学](@entry_id:173318)描述的基础之上，我们可以进一步探讨一些更深层次的原理，它们构成了现代连续介质力学理论的支柱。

#### [拉格朗日与欧拉描述](@entry_id:190556)

到目前为止，我们已经接触到了两种描述物理场的观点。

**[拉格朗日描述](@entry_id:264498)**（Lagrangian description），或称物质描述，将所有物理量（如速度、应力）视为物质坐标 $\boldsymbol{X}$ 和时间 $t$ 的函数，例如 $\boldsymbol{V}(\boldsymbol{X}, t)$。这种描述方式的优点是它天然地追踪每个物[质粒](@entry_id:263777)子的历史，因为 $\boldsymbol{X}$ 是粒子的固定标签。这对于[固体力学](@entry_id:164042)至关重要，因为固体的本构关系（材料响应）通常依赖于其经历的整个变形历史。此外，在固体力学问题中，边界条件通常施加在物体的特定物质边界上，在[拉格朗日描述](@entry_id:264498)中，这些边界是固定的，从而简化了问题的提法。

**[欧拉描述](@entry_id:264722)**（Eulerian description），或称空间描述，将物理量视为空间坐标 $\boldsymbol{x}$ 和时间 $t$ 的函数，例如 $\boldsymbol{v}(\boldsymbol{x}, t)$。这种描述方式在[流体力学](@entry_id:136788)中占据主导地位，因为它关注的是空间中固定区域的流动情况，而不是追踪单个流体粒子。

对于涉及大变形和复杂材料（如[弹塑性](@entry_id:193198)、[粘弹性](@entry_id:148045)）的[非线性固体力学](@entry_id:171757)，[拉格朗日描述](@entry_id:264498)通常是首选。这是因为它能够直接、清晰地构建与材料相关的变形度量（如 $\boldsymbol{F}$ 和 $\boldsymbol{C}$）和本构模型，而纯粹的[欧拉描述](@entry_id:264722)若要包含有限变形和路径依赖效应，就必须额外追踪[粒子轨迹](@entry_id:204827)，这会使得问题变得异常复杂和繁琐。[@problem_id:2658004]

#### 运动学协调性

一个自然的问题是：任意一个给定的二阶张量场 $\boldsymbol{F}(\boldsymbol{X})$ 是否都能成为某个实际变形的变形梯度？答案是否定的。为了使一个张量场 $\boldsymbol{F}$ 能够成为某个[位移场](@entry_id:141476) $\boldsymbol{\chi}$ 的梯度（即 $\boldsymbol{F} = \nabla_{\boldsymbol{X}}\boldsymbol{\chi}$），它必须满足一定的**协调性条件**（compatibility condition）。

这个条件源于一个基本的数学事实：[梯度的旋度](@entry_id:274168)恒为零。由于 $\boldsymbol{F}$ 的每一行都可以看作是位移分量 $\chi_i$ 的梯度，因此，为了保证[位移场](@entry_id:141476) $\boldsymbol{\chi}$ 的存在（并且是单值的），$\boldsymbol{F}$ 的每一行的旋度都必须为零。在单连通区域内，这是一个充分必要条件。用张量形式写出，这个条件是：
$$ \operatorname{Curl} \boldsymbol{F} = \boldsymbol{0} $$
其中 $(\operatorname{Curl} \boldsymbol{F})_{iJ} = \varepsilon_{JKL} \frac{\partial F_{iL}}{\partial X_K}$，$\varepsilon_{JKL}$ 是[列维-奇维塔符号](@entry_id:193594)。这个[方程组](@entry_id:193238)确保了从变形梯度场积分得到的[位移场](@entry_id:141476)是唯一的（相差一个刚体平移），并且不会因为积分路径的不同而产生矛盾，从而保证了变形后的物体不会出现“裂缝”或“重叠”。[@problem_id:2658009]

#### [客观性原理](@entry_id:185412)

[客观性原理](@entry_id:185412)（principle of objectivity），或称物质标架无关性（material frame-indifference），是本构理论的一个基本要求。它指出，材料的本构关系（即应力如何响应变形）不应依赖于观察者。这一原理有两个关键方面。

第一方面是**参考构形的任意性**。我们选择哪个构形作为参考构形是任意的，物理定律的预测不应依赖于这种选择。这并不意味着所有量都在改变参考构形时保持不变。实际上，物理上可直接测量的量（如柯西应力 $\boldsymbol{\sigma}$、[空间速度](@entry_id:190294) $\boldsymbol{v}$、空间密度 $\rho$）是**不变的**。而那些依赖于参考构形的量，如变形梯度 $\boldsymbol{F}$、[第一皮奥拉-基尔霍夫应力](@entry_id:163971) $\boldsymbol{P}$ 和参考密度 $\rho_0$，则会根据明确的规则进行变换。例如，若两个参考构形通过映射 $\boldsymbol{X} = \boldsymbol{\kappa}(\tilde{\boldsymbol{X}})$ 相关联，其梯度为 $\boldsymbol{K} = \nabla_{\tilde{\boldsymbol{X}}}\boldsymbol{\kappa}$，则变形梯度和参考密度的变换关系为：
$$ \tilde{\boldsymbol{F}} = \boldsymbol{F} \boldsymbol{K}, \quad \tilde{\rho}_0 = \rho_0 \det \boldsymbol{K} $$
而[第一皮奥拉-基尔霍夫应力](@entry_id:163971)的变换规则为 $\tilde{\boldsymbol{P}} = \boldsymbol{P} \operatorname{cof}(\boldsymbol{K})$。这些变换规则确保了从不同参考构形出发计算得到的物理结果是一致的。[@problem_id:2658093]

第二方面，也是更常被讨论的，是**观察者的无关性**。一个观察者的改变可以通过在一个已有的运动上叠加一个刚体运动来表示。即，如果一个运动是 $\boldsymbol{\chi}(\boldsymbol{X}, t)$，另一个以[旋转和平移](@entry_id:175994)方式相对于前者运动的观察者将观察到运动 $\tilde{\boldsymbol{\chi}}(\boldsymbol{X}, t) = \boldsymbol{c}(t) + \boldsymbol{Q}(t)\boldsymbol{\chi}(\boldsymbol{X}, t)$，其中 $\boldsymbol{c}(t)$ 是一个时变平移向量，$\boldsymbol{Q}(t)$ 是一个时变[旋转张量](@entry_id:191990)（$\boldsymbol{Q} \in SO(3)$）。

一个物理量如果在这种变换下遵循特定的[张量变换](@entry_id:183453)规则，则被称为**客观的**（objective）。
- **客观的物质张量**（如[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}$）必须是不变的：$\tilde{\boldsymbol{C}} = \boldsymbol{C}$。
- **客观的空间向量**（如两点间的距离向量）必须只受旋转影响：$\tilde{\boldsymbol{v}} = \boldsymbol{Q}\boldsymbol{v}$。
- **客观的空间[二阶张量](@entry_id:199780)**（如柯西应力 $\boldsymbol{\sigma}$ 和变形率张量 $\boldsymbol{d}$）的变换规则是：$\tilde{\boldsymbol{T}} = \boldsymbol{Q}\boldsymbol{T}\boldsymbol{Q}^{\mathsf{T}}$。

通过直接推导可以验证，以下重要运动学量的客观性 [@problem_id:2658054]：
- **变形梯度** $\boldsymbol{F}$ **不是**客观的，因为它变换为 $\tilde{\boldsymbol{F}} = \boldsymbol{Q}\boldsymbol{F}$。
- **[右柯西-格林张量](@entry_id:174156)** $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$ 和**[格林-拉格朗日应变张量](@entry_id:187745)** $\boldsymbol{E} = (\boldsymbol{C}-\boldsymbol{I})/2$ 是**客观的**物质张量，因为 $\tilde{\boldsymbol{C}} = \boldsymbol{C}$。
- **[空间速度梯度](@entry_id:187198)** $\boldsymbol{l} = \nabla_{\boldsymbol{x}}\boldsymbol{v}$ **不是**客观的，因为它变换为 $\tilde{\boldsymbol{l}} = \boldsymbol{Q}\boldsymbol{l}\boldsymbol{Q}^{\mathsf{T}} + \dot{\boldsymbol{Q}}\boldsymbol{Q}^{\mathsf{T}}$。
- **变形率张量** $\boldsymbol{d}$ ([空间速度梯度](@entry_id:187198)的对称部分) 是**客观的**[空间张量](@entry_id:185799)。
- **[自旋张量](@entry_id:187346)** $\boldsymbol{w}$ ([空间速度梯度](@entry_id:187198)的反对称部分) **不是**客观的。

[客观性原理](@entry_id:185412)是建立合理[本构方程](@entry_id:138559)的指导原则：任何[本构方程](@entry_id:138559)都必须由客观的量构成，以确保材料属性独立于观察者。