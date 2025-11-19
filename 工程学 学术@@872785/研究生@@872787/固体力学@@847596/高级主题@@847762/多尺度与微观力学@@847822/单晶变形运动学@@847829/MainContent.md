## 引言
在先进材料的设计与应用中，准确预测其在复杂载荷下的力学响应至关重要。对于单晶体材料而言，其行为深刻地根植于其底层的[晶体结构](@entry_id:140373)。传统的[唯象模型](@entry_id:273816)往往无法捕捉这种由晶体学各向异性主导的复杂行为，因此，我们需要一个能够在晶体尺度上精确描述变形物理机制的理论框架。本文旨在填补这一知识空白，系统性地建立单晶体变形的**[运动学](@entry_id:173318)**基础。

本文将引导读者深入理解[单晶塑性](@entry_id:754915)的核心[运动学](@entry_id:173318)原理。在“**原理和机制**”一章中，我们将详细阐述变形梯度的[乘法分解](@entry_id:199514)，揭示弹性变形与[塑性流动](@entry_id:201346)的分离，并建立描述滑移和[晶格](@entry_id:196752)旋转的数学语言。随后，在“**应用与跨学科联系**”一章中，我们将展示这些理论如何应用于计算力学、[材料科学](@entry_id:152226)和实验表征，连接理论与实际工程问题。最后，“**动手实践**”部分提供了一系列计算练习，帮助读者将抽象的理论转化为具体的分析技能。通过这一结构化的学习路径，读者将掌握分析和模拟单晶[材料力学](@entry_id:201885)行为所必需的基本工具。

## 原理和机制

在理解单晶体材料的力学行为时，精确描述其变形运动学是至关重要的第一步。与各向同性[多晶材料](@entry_id:158956)的[唯象模型](@entry_id:273816)不同，[单晶塑性](@entry_id:754915)理论必须在晶体学层面考虑变形的物理机制。本章将系统地阐述描述单晶变形的运动学原理，重点关注变形的分解、塑性流动的基本机制，以及这些机制在[连续介质力学](@entry_id:155125)框架下的数学表达。

### 变形的[运动学分解](@entry_id:751020)

变形在最基本的层面上由变形梯度张量 $\mathbf{F}$ 来描述，它将参考构型中的一个无穷小材料线元 $d\mathbf{X}$ 映射到当前构型中的对应线元 $d\mathbf{x}$，即 $d\mathbf{x} = \mathbf{F} d\mathbf{X}$。为了深入理解变形的物理内涵，我们需要将 $\mathbf{F}$ 分解为更能体现物理过程的组成部分。

#### 极分解：分离拉伸与转动

任何非奇异的变形梯度 $\mathbf{F}$（即 $\det\mathbf{F} > 0$）都可以唯一地分解为一个纯拉伸和一个[刚体转动](@entry_id:191086)。这种分解有两种形式，即右极分解和左极分解 [@problem_id:2653215]：
$$ \mathbf{F} = \mathbf{R}\mathbf{U} = \mathbf{V}\mathbf{R} $$
其中，$\mathbf{R}$ 是一个正常正交张量（$\mathbf{R}^{\mathsf{T}}\mathbf{R}=\mathbf{I}$ 且 $\det\mathbf{R}=+1$），代表了材料点的**局部[刚体转动](@entry_id:191086)**。在单晶体的背景下，这对应于[晶格](@entry_id:196752)的[刚体转动](@entry_id:191086)。$\mathbf{U}$ 和 $\mathbf{V}$ 分别是**右[拉伸张量](@entry_id:193200)**和**左[拉伸张量](@entry_id:193200)**，它们都是[对称正定](@entry_id:145886)张量，描述了材料的纯变形，即不包含[刚体转动](@entry_id:191086)的拉伸与剪切。

$\mathbf{U}$ 和 $\mathbf{V}$ 与柯西-格林（Cauchy-Green）变形张量直接相关。**[右柯西-格林张量](@entry_id:174156)** $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$ 定义在参考构型上，而**[左柯西-格林张量](@entry_id:186163)** $\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}}$ 定义在当前构型上。通过极分解可以发现，$\mathbf{C} = \mathbf{U}^2$ 且 $\mathbf{B} = \mathbf{V}^2$。因此，$\mathbf{U}$ 和 $\mathbf{V}$ 分别是 $\mathbf{C}$ 和 $\mathbf{B}$ 的唯一正定平方根。

这两个[拉伸张量](@entry_id:193200)描述的是相同的变形状态，但作用于不同的构型。$\mathbf{U}$ 作用于参考构型，而 $\mathbf{V}$ 作用于一个被转动了的构型。它们通过转动张量 $\mathbf{R}$ 相互关联：$\mathbf{V} = \mathbf{R}\mathbf{U}\mathbf{R}^{\mathsf{T}}$。这种关系是一种[相似变换](@entry_id:152935)，意味着它们拥有相同的[特征值](@entry_id:154894)，即**主拉伸**（principal stretches）。然而，它们的[特征向量](@entry_id:151813)（主拉伸方向）不同：$\mathbf{U}$ 的[特征向量](@entry_id:151813)是参考构型中的[主方向](@entry_id:276187)，而 $\mathbf{V}$ 的[特征向量](@entry_id:151813)是当前构型中的[主方向](@entry_id:276187) [@problem_id:2653215]。一个常见的误解是认为纯[拉伸张量](@entry_id:193200)不会改变材料线的方向。实际上，只有当一个向量是[拉伸张量](@entry_id:193200)的[特征向量](@entry_id:151813)时，其方向才保持不变。对于任意方向的材料线，纯拉伸通常会同时改变其长度和方向。

#### [乘法分解](@entry_id:199514)：分离弹性和塑性

极分解虽然在几何上很直观，但未能区分变形的可恢复（弹性）和不可恢复（塑性）部分。在[晶体塑性理论](@entry_id:180579)中，一个更核心的分解是**[乘法分解](@entry_id:199514)**（multiplicative decomposition），它将总变形梯度 $\mathbf{F}$ 分解为弹性和塑性两部分 [@problem_id:2653214]：
$$ \mathbf{F} = \mathbf{F}^e \mathbf{F}^p $$
这个分解引入了一个概念性的**[中间构型](@entry_id:193000)**（intermediate configuration）。这个构型通常被认为是“卸载”或“松弛”的构型。整个变形过程可以被概念性地分为两步：

1.  **塑性变形 $\mathbf{F}^p$**：首先，材料点从参考构型通过[塑性流动](@entry_id:201346)（主要是[晶格](@entry_id:196752)滑移和孪生）到达[中间构型](@entry_id:193000)。在这个过程中，原子在[晶格](@entry_id:196752)中重新[排列](@entry_id:136432)，但[晶格](@entry_id:196752)本身（即原子间的键长和键角）被认为没有发生畸变。因此，[中间构型](@entry_id:193000)是局部无应力的。

2.  **弹性变形 $\mathbf{F}^e$**：接着，[晶格](@entry_id:196752)本身作为一个整体，从无应力的[中间构型](@entry_id:193000)经历弹性拉伸和[刚体转动](@entry_id:191086)，最终到达当前构型。这一步导致了[晶格](@entry_id:196752)畸变，从而产生了宏观应力。

因此，$\mathbf{F}^p$ 描述了材料的永久变形，而 $\mathbf{F}^e$ 则包含了[晶格](@entry_id:196752)的弹性畸变和整体转动。这一分解是现代[有限应变塑性](@entry_id:185352)理论的基石。

### 塑性变形的物理机制

在原子尺度上，晶体的塑性变形主要通过[位错运动](@entry_id:143448)（滑移）和形变孪生这两种机制实现。

#### 晶体滑移

晶体滑移是指晶体的一部分相对于另一部分沿着特定的**滑移面**（slip plane）和**滑移方向**（slip direction）发生剪切运动。一个[滑移面](@entry_id:158709)及其上的一个滑移方向共同构成一个**[滑移系](@entry_id:136401)**（slip system）。在连续介质力学层面，一个[滑移系](@entry_id:136401) $\alpha$ 可以由其单位滑移[面[法向](@entry_id:749211)量](@entry_id:264185) $\mathbf{m}^\alpha$ 和单位滑移方向向量 $\mathbf{s}^\alpha$ 来定义，且两者相互垂直，即 $\mathbf{s}^\alpha \cdot \mathbf{m}^\alpha = 0$。描述滑移产生的[剪切变形](@entry_id:170920)的基本张量是**施密特张量**（Schmid tensor）$\mathbf{S}^\alpha = \mathbf{s}^\alpha \otimes \mathbf{m}^\alpha$ [@problem_id:2653163]。

#### 形变孪生

形变孪生是另一种重要的塑性变形机制，它通过[晶格](@entry_id:196752)的局部重取向形成一个与母体[晶格](@entry_id:196752)呈镜像对称的区域（孪晶）。在运动学上，理想的孪生过程可以被描述为一个**简单剪切**（simple shear）变形 [@problem_id:2653176]。一个由孪生面法向 $\mathbf{m}_t$、剪切方向 $\mathbf{s}_t$（满足 $\mathbf{s}_t \cdot \mathbf{m}_t = 0$）和孪生剪切量 $s_t$ 所定义的孪生变形，其变形梯度可以表示为：
$$ \mathbf{F}^t = \mathbf{I} + s_t \mathbf{s}_t \otimes \mathbf{m}_t $$
其中 $\mathbf{I}$ 是单位张量。这种变形的一个重要特性是它是保体积的。利用[行列式](@entry_id:142978)性质 $\det(\mathbf{I} + \mathbf{a} \otimes \mathbf{b}) = 1 + \mathbf{a} \cdot \mathbf{b}$，我们可以立即得到：
$$ \det(\mathbf{F}^t) = 1 + s_t (\mathbf{s}_t \cdot \mathbf{m}_t) = 1 $$
这表明理想孪生过程不引起体积变化。此外，孪生面本身是变形过程中的一个**[不变平面](@entry_id:163758)**（invariant plane），即位于该平面内的任何向量 $\mathbf{a}$（满足 $\mathbf{a} \cdot \mathbf{m}_t = 0$）在变形后保持不变：$\mathbf{F}^t \mathbf{a} = \mathbf{a}$。

### 变形率运动学

为了建立本构关系，我们需要描述变形的速率。这需要引入速度梯度及其分解。

#### [空间速度梯度](@entry_id:187198)及其分解

**[空间速度梯度](@entry_id:187198)** $\mathbf{L}$ 定义为[空间速度](@entry_id:190294)场 $\mathbf{v}$ 对当前位置 $\mathbf{x}$ 的梯度，$\mathbf{L} = \nabla_{\mathbf{x}}\mathbf{v}$。它与变形梯度的时间导数之间存在一个基本关系：$\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}$ [@problem_id:2653185]。

将[乘法分解](@entry_id:199514) $\mathbf{F} = \mathbf{F}^e\mathbf{F}^p$ 对时间求导，可以得到 $\mathbf{L}$ 的一个加法分解：
$$ \mathbf{L} = \dot{\mathbf{F}}^e(\mathbf{F}^e)^{-1} + \mathbf{F}^e \big( \dot{\mathbf{F}}^p(\mathbf{F}^p)^{-1} \big) (\mathbf{F}^e)^{-1} $$
我们定义**弹性[速度梯度](@entry_id:261686)** $\mathbf{L}^e = \dot{\mathbf{F}}^e(\mathbf{F}^e)^{-1}$ 和在[中间构型](@entry_id:193000)中定义的**塑性[速度梯度](@entry_id:261686)** $\mathbf{L}^p = \dot{\mathbf{F}}^p(\mathbf{F}^p)^{-1}$。于是，[空间速度梯度](@entry_id:187198)可以分解为：
$$ \mathbf{L} = \mathbf{L}^e + \mathbf{L}_p \quad \text{其中} \quad \mathbf{L}_p = \mathbf{F}^e \mathbf{L}^p (\mathbf{F}^e)^{-1} $$
这里的 $\mathbf{L}_p$ 是塑性速度梯度在当前构型中的“推前”（push-forward）形式。

#### 变形率与自旋

[空间速度梯度](@entry_id:187198) $\mathbf{L}$ 可进一步分解为其对称部分**变形率张量** $\mathbf{D}$ 和反对称部分**[自旋张量](@entry_id:187346)** $\mathbf{W}$：
$$ \mathbf{D} = \mathrm{sym}(\mathbf{L}) = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\mathsf{T}}) $$
$$ \mathbf{W} = \mathrm{skw}(\mathbf{L}) = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\mathsf{T}}) $$
$\mathbf{D}$ 描述了材料[线元](@entry_id:196833)长度和角度的[瞬时变化率](@entry_id:141382)，而 $\mathbf{W}$ 描述了材料点的局部[刚体转动](@entry_id:191086)速率 [@problem_id:2653185]。

同样地，$\mathbf{D}$ 和 $\mathbf{W}$ 也可以进行[弹塑性](@entry_id:193198)分解：
$$ \mathbf{D} = \mathbf{D}^e + \mathbf{D}^p \quad \text{其中} \quad \mathbf{D}^e = \mathrm{sym}(\mathbf{L}^e), \quad \mathbf{D}^p = \mathrm{sym}(\mathbf{L}_p) $$
$$ \mathbf{W} = \mathbf{W}^e + \mathbf{W}^p \quad \text{其中} \quad \mathbf{W}^e = \mathrm{skw}(\mathbf{L}^e), \quad \mathbf{W}^p = \mathrm{skw}(\mathbf{L}_p) $$
这里的 $\mathbf{D}^p$ 和 $\mathbf{W}^p$ 分别是**塑性变形率**和**塑性自旋**。$\mathbf{W}^e$ 通常被称为**[晶格自旋](@entry_id:198780)**，因为它描述了[晶格](@entry_id:196752)的转动速率。

### 关键原理及其推论

基于上述[运动学](@entry_id:173318)框架，我们可以导出几个关于[单晶塑性](@entry_id:754915)的核心原理。

#### [塑性不可压缩性](@entry_id:183440)

[晶体塑性理论](@entry_id:180579)的一个基本假设是，由[位错滑移](@entry_id:275474)主导的塑性变形是保体积的。这一假设源于滑移的剪切本质。我们可以从运动学上严格证明这一点。塑性[速度梯度](@entry_id:261686) $\mathbf{L}^p$ 可表示为所有激活滑移系贡献的总和：
$$ \mathbf{L}^p = \sum_{\alpha} \dot{\gamma}^\alpha \mathbf{S}^\alpha = \sum_{\alpha} \dot{\gamma}^\alpha \mathbf{s}^\alpha \otimes \mathbf{m}^\alpha $$
其中 $\dot{\gamma}^\alpha$ 是第 $\alpha$ 个[滑移系](@entry_id:136401)上的滑移率。$\mathbf{L}^p$ 的迹（trace）代表了塑性变形引起的体积变化率。利用迹的性质 $\mathrm{tr}(\mathbf{a} \otimes \mathbf{b}) = \mathbf{a} \cdot \mathbf{b}$，我们得到 [@problem_id:2653179]：
$$ \mathrm{tr}(\mathbf{L}^p) = \sum_{\alpha} \dot{\gamma}^\alpha (\mathbf{s}^\alpha \cdot \mathbf{m}^\alpha) = 0 $$
因为对于任何滑移系，$\mathbf{s}^\alpha \cdot \mathbf{m}^\alpha = 0$。又因为任何[反对称张量](@entry_id:199349)的迹都为零（即 $\mathrm{tr}(\mathbf{W}^p)=0$），所以我们有 $\mathrm{tr}(\mathbf{D}^p) = \mathrm{tr}(\mathbf{L}^p) = 0$。这即是**塑性流动不可压缩**的速率形式。

这个速率形式的条件与有限变形张量 $\mathbf{F}^p$ 的体积约束直接相关。利用[雅可比公式](@entry_id:142453)（Jacobi's formula），$\frac{d}{dt}\det(\mathbf{F}^p) = \det(\mathbf{F}^p) \mathrm{tr}(\mathbf{L}^p)$，既然 $\mathrm{tr}(\mathbf{L}^p)=0$，则 $\det(\mathbf{F}^p)$ 是一个常数。假设初始状态没有塑性变形，即 $\mathbf{F}^p(0)=\mathbf{I}$，那么 $\det(\mathbf{F}^p(0))=1$，因此在整个变形过程中 $\det(\mathbf{F}^p)=1$。

需要强调的是，塑性不可压缩（$\det\mathbf{F}^p=1$）不代表总变形不可压缩。总的体积变化 $J = \det\mathbf{F} = \det(\mathbf{F}^e)\det(\mathbf{F}^p) = \det(\mathbf{F}^e)$，完全由弹性变形引起。

#### [晶格](@entry_id:196752)转动及其运动学描述

[晶格](@entry_id:196752)的取向演化是[单晶塑性](@entry_id:754915)的一个核心特征，直接导致了织构（texture）的形成。[晶格](@entry_id:196752)的转动速率由**[晶格自旋](@entry_id:198780)** $\mathbf{W}^e$ 描述。从自旋的加法分解 $\mathbf{W} = \mathbf{W}^e + \mathbf{W}^p$ 中，我们得到一个至关重要的关系：
$$ \mathbf{W}^e = \mathbf{W} - \mathbf{W}^p $$
这表明，[晶格](@entry_id:196752)的转动速率（$\mathbf{W}^e$）等于材料的总自旋速率（$\mathbf{W}$）减去由塑性剪切引起的自旋（$\mathbf{W}^p$）[@problem_id:2653185]。塑性自旋 $\mathbf{W}^p = \mathrm{skw}(\mathbf{F}^e \mathbf{L}^p (\mathbf{F}^e)^{-1})$ 本身依赖于[塑性流动](@entry_id:201346) $\mathbf{L}^p$ 和当前的弹性变形状态 $\mathbf{F}^e$ [@problem_id:2653173]。这个关系是理解和预测晶体在塑性变形过程中取向如何演变的关键。

#### 塑性变形的[路径依赖性](@entry_id:186326)

与弹性变形不同，有限塑性变形是**路径依赖**的。最终的塑性状态 $\mathbf{F}^p$ 不仅取决于总的变形量，还取决于变形所经历的路径。这源于控制 $\mathbf{F}^p$ 演化的[微分方程](@entry_id:264184) $\dot{\mathbf{F}}^p = \mathbf{L}^p \mathbf{F}^p$。

我们可以通过一个简单的例子来说明。考虑一个晶体先后在两个不同的[滑移系](@entry_id:136401)上发生剪切 [@problem_id:2653191]。在时间段 $[0, t_1]$，只有滑移系1激活，其塑性[速度梯度](@entry_id:261686)为常数 $\mathbf{L}_1^p$。在时间段 $[t_1, t_f]$，只有滑移系2激活，其塑性[速度梯度](@entry_id:261686)为常数 $\mathbf{L}_2^p$。从初始状态 $\mathbf{F}^p(0)=\mathbf{I}$ 开始积分，在 $t_1$ 时刻，$\mathbf{F}^p(t_1) = \exp(t_1 \mathbf{L}_1^p) \mathbf{F}^p(0)$。接着从 $t_1$ 积分到 $t_f$，最终的塑性变形梯度为：
$$ \mathbf{F}^p(t_f) = \exp((t_f - t_1) \mathbf{L}_2^p) \mathbf{F}^p(t_1) = \exp((t_f - t_1) \mathbf{L}_2^p) \exp(t_1 \mathbf{L}_1^p) \mathbf{F}^p(0) $$
由于[矩阵指数](@entry_id:139347)通常是不可交换的，即 $\exp(\mathbf{A})\exp(\mathbf{B}) \neq \exp(\mathbf{B})\exp(\mathbf{A})$，因此如果我们颠倒滑移激活的顺序，最终的 $\mathbf{F}^p(t_f)$ 将会不同。这个结果（一个时间有序的指数）清晰地表明了塑性变形的累积历史效应。

### 运动学与力学的联系

运动学为建立材料本构关系提供了框架。本构关系必须遵循某些基本物理原理，其中最重要的是材料[坐标系](@entry_id:156346)无关性。

#### 材料[坐标系](@entry_id:156346)无关性（客观性）

**材料[坐标系](@entry_id:156346)无关性原理**（principle of material frame indifference），或称**[客观性原理](@entry_id:185412)**（principle of objectivity），要求[本构关系](@entry_id:186508)不能因观察者的改变而改变。一个[刚体运动](@entry_id:193355)的叠加（$\mathbf{x}^\star = \mathbf{c}(t) + \mathbf{Q}(t)\mathbf{x}$）仅仅是改变了观察者，不应影响材料的内在响应。在这种变换下，变形梯度变为 $\mathbf{F}^\star = \mathbf{QF}$ [@problem_id:2653167]。

为了满足客观性，任何依赖于变形的标量物理量（如自由能 $\psi$）必须通过客观的张量来表达。例如，$\psi$ 不能直接是 $\mathbf{F}$ 的函数，而必须是[右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$ 的函数，因为 $\mathbf{C}^\star = (\mathbf{F}^\star)^{\mathsf{T}}\mathbf{F}^\star = (\mathbf{QF})^{\mathsf{T}}(\mathbf{QF}) = \mathbf{F}^{\mathsf{T}}\mathbf{Q}^{\mathsf{T}}\mathbf{Q}\mathbf{F} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \mathbf{C}$，即 $\mathbf{C}$ 在这种变换下是不变的。

对于[晶体塑性](@entry_id:141273)，一个关键的量是**分切剪应力**（resolved shear stress）$\tau^\alpha$，它是作用在滑移面上、沿滑移方向的剪应力分量。它由柯西应力 $\boldsymbol{\sigma}$ 计算得出：$\tau^\alpha = \boldsymbol{\sigma} : (\mathbf{s}^\alpha \otimes \mathbf{m}^\alpha) = \mathbf{s}^\alpha \cdot \boldsymbol{\sigma} \mathbf{m}^\alpha$。可以证明，当[滑移系](@entry_id:136401)向量随[晶格](@entry_id:196752)一起转动时，$\tau^\alpha$ 是一个客观的标量。这使得它成为驱动[滑移流](@entry_id:154133)动的理想物理量。例如，在 [@problem_id:2653163] 中，为了计算分切剪应力，必须首先将不同[坐标系](@entry_id:156346)下的应力张量和[滑移系](@entry_id:136401)向量转换到同一个[坐标系](@entry_id:156346)下，然后才能应用公式 $\tau = s_i \sigma_{ij} m_j$。

#### [应变测量](@entry_id:193240)与[功共轭](@entry_id:194957)

在有限塑性应变但小弹性应变的情况下（这在金属中很常见），选择一个合适的弹性应变测量至关重要。一个常用的选择是**弹性[格林-拉格朗日应变张量](@entry_id:187745)**（elastic Green-Lagrange strain tensor）[@problem_id:2653166]：
$$ \mathbf{E}^e = \frac{1}{2}(\mathbf{C}^e - \mathbf{I}) = \frac{1}{2}((\mathbf{F}^e)^{\mathsf{T}}\mathbf{F}^e - \mathbf{I}) $$
选择 $\mathbf{E}^e$ 的理由是多方面的：首先，它只依赖于弹性变形的拉伸部分 $\mathbf{U}^e$（因为 $\mathbf{C}^e = (\mathbf{U}^e)^2$），因此它天生对[晶格](@entry_id:196752)的弹性转动 $\mathbf{R}^e$ 不敏感，满足了客观性要求。其次，在小[弹性应变](@entry_id:189634)下，它近似等于线[弹性应变](@entry_id:189634)张量 $\boldsymbol{\varepsilon}^e$。最重要的是，在一个[超弹性](@entry_id:159356)框架中，如果弹性自由能 $\psi$ 是 $\mathbf{E}^e$ 的函数，那么与 $\mathbf{E}^e$ **[功共轭](@entry_id:194957)**（work-conjugate）的应力是定义在[中间构型](@entry_id:193000)上的**[第二皮奥拉-基尔霍夫应力](@entry_id:173163)**（second Piola-Kirchhoff stress）$\mathbf{S}^e = \partial\psi/\partial\mathbf{E}^e$。这为建立[热力学一致的](@entry_id:755906)本构模型提供了坚实的基础。

#### [客观率](@entry_id:198692)与协同转动框架的选择

在率形式的[本构关系](@entry_id:186508)中（例如 $\dot{\boldsymbol{\sigma}} \sim \mathbf{D}$），为了保证客观性，必须使用**[客观应力率](@entry_id:199282)**。一个常见的选择是**Jaumann率**，它使用材料自旋 $\mathbf{W}$ 来修正柯西应力的时间导数：$\overset{\triangle}{\boldsymbol{\sigma}}=\dot{\boldsymbol{\sigma}}+\boldsymbol{\sigma}\mathbf{W}-\mathbf{W}\boldsymbol{\sigma}$。

然而，研究表明，对于大剪切变形，使用基于材料自旋 $\mathbf{W}$ 的Jaumann率会导致非物理的应力[振荡](@entry_id:267781) [@problem_id:2653178]。其根本原因在于，材料应力源于弹性[晶格](@entry_id:196752)的畸变，因此其本构关系的更新应该在一个随[晶格](@entry_id:196752)转动的[参考系](@entry_id:169232)中进行。物理上更合理的选择是使用一个基于**[晶格自旋](@entry_id:198780)** $\mathbf{W}^e$ 的协同转动率。由于 $\mathbf{W} = \mathbf{W}^e + \mathbf{W}^p$，使用材料自旋 $\mathbf{W}$ 会错误地引入一个由塑性自旋 $\mathbf{W}^p$ 引起的额外转动来更新弹性应力。因此，在现代[晶体塑性](@entry_id:141273)模型中，通常采用基于[晶格自旋](@entry_id:198780) $\mathbf{W}^e$ 的[客观率](@entry_id:198692)，这能显著改善模型在[大变形](@entry_id:167243)下的预测能力，并避免非物理的[振荡](@entry_id:267781)行为。