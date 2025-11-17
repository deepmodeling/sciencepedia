## 引言
在描述固体变形时，连续介质力学使用两种视角：物体变形前的初始状态（**参考构型**）和变形后的当前状态（**空间构型**）。然而，一个核心的挑战随之而来：如何将在一个构型中定义的物理量（如密度、应力和应变率）与另一个构型中的对应量建立严谨且一致的联系？简单地在不同[坐标系](@entry_id:156346)下使用相同的数值是错误的，因为它忽略了变形本身对物理量的影响。

本文旨在填补这一认知空白，系统介绍解决此问题的基本数学框架——**[前推](@entry_id:158718) (push-forward)** 与 **后拉 (pull-back)** 张量运算。这些操作并非抽象的数学游戏，而是确保物理定律（如质量守恒、[动量守恒](@entry_id:149964)）在拉格朗日和[欧拉描述](@entry_id:264722)之间转换时保持其形式不变的根本保证。通过学习本文，读者将能够理解和应用这些变换法则，从而精确地建模大变形问题。

文章将分为三个核心部分。在“**原则与机理**”一章中，我们将深入探讨[前推](@entry_id:158718)与后拉的数学定义，以及它们如何应用于变形梯度、[应变张量](@entry_id:193332)和不同类型的[应力张量](@entry_id:148973)。随后，“**应用与交叉学科联系**”一章将展示这些理论在先进本构模型、计算力学、[多物理场耦合](@entry_id:171389)乃至医学成像等前沿领域的实际应用。最后，“**动手实践**”部分提供了一系列计算练习，帮助读者将理论知识转化为实践能力。

让我们首先从这些变换操作的基本原则和运动学机理开始。

## 原则与机理

在[连续介质力学](@entry_id:155125)中，固体的变形行为通过连接其初始（或**参考**）构型与当前（或**空间**）构型的数学映射来描述。这些构型中的物理量，如密度、应力和应变，必须以一种一致的方式相互关联。**[前推](@entry_id:158718) (push-forward)** 和 **后拉 (pull-back)** 操作正是实现这种关联的严谨数学工具。本章将深入探讨这些操作的基本原则、推导过程及其在描述运动学、动力学和本构关系中的核心作用。

### 基本的运动学映射

我们考虑一个连续体，其在参考构型 $\mathcal{B}_0$ 中占据空间区域，物质点的坐标用 $\boldsymbol{X}$ 表示。经过变形后，连续体在当前构型 $\mathcal{B}$ 中占据空间区域，相应空间点的坐标用 $\boldsymbol{x}$ 表示。描述这一过程的**变形映射 (deformation mapping)** 为 $\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X})$，我们假设此映射是光滑且可逆的。

#### 变形梯度

变形的核心局部特征由**变形梯度张量 (deformation gradient tensor)** $\boldsymbol{F}$ 捕捉。它被定义为空间坐标 $\boldsymbol{x}$ 对参考坐标 $\boldsymbol{X}$ 的梯度：

$F_{iJ} = \frac{\partial x_i}{\partial X_J}$

从几何上看，$\boldsymbol{F}$ 是变形映射 $\boldsymbol{\varphi}$ 在某一点的线性化，它描述了一个无穷小的物质元如何变形。具体来说，一个在参考构型中由矢量 $d\boldsymbol{X}$ 表示的无穷小线元，在变形后会映射为当前构型中的[线元](@entry_id:196833) $d\boldsymbol{x}$，两者之间的关系为：

$d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$

这个关系是有限变形理论的基石，它表明变形梯度 $\boldsymbol{F}$ 将参考构型中的切空间向量“[前推](@entry_id:158718)”至当前构型中的[切空间](@entry_id:199137)。[@problem_id:3591928]

#### 雅可比行列式

变形梯度张量的[行列式](@entry_id:142978)，即**[雅可比行列式](@entry_id:137120) (Jacobian determinant)** $J = \det(\boldsymbol{F})$，具有明确的物理意义。它表示了局部的体积变化率。一个在参考构型中具有体积 $dV$ 的无穷小[体积元](@entry_id:267802)，在变形后其体积 $dv$ 为：

$dv = J dV$

对于物理上真实的变形，物质不应发生相互穿透，这意味着一个具有正体积的物质元在变形后体积仍然为正。这要求 $J > 0$。这个条件确保了变形在局部是保持方向的（例如，右手表系仍然映射为右手表系）。需要注意的是，$J > 0$ 仅表示方向保持，而不等同于不可压缩性。[不可压缩材料](@entry_id:159741)的运动学约束是体积不变，即 $J=1$。[@problem_id:3591928]

### 场的变换：[前推](@entry_id:158718)与后拉

物理量可以被定义在参考构型上（[拉格朗日描述](@entry_id:264498)）或当前构型上（[欧拉描述](@entry_id:264722)）。[前推](@entry_id:158718)与后拉操作是在这两种描述之间进行转换的数学语言。

#### 标量场

我们以质量密度为例来说明[标量场](@entry_id:151443)的变换。假设参考构型中的密度场为 $\rho_0(\boldsymbol{X})$，当前构型中的密度场为 $\rho(\boldsymbol{x})$。根据质量守恒原理，一个物质[体积元](@entry_id:267802)的质量在变形过程中保持不变：

$\rho_0 dV = \rho dv$

结合体积变化关系 $dv = J dV$，我们得到：

$\rho_0(\boldsymbol{X}) = J(\boldsymbol{X}) \rho(\boldsymbol{\varphi}(\boldsymbol{X}))$

这个关系被称为空间密度场 $\rho$ 到参考构型的**后拉**。反之，我们可以将参考密度场 $\rho_0$ **[前推](@entry_id:158718)**到当前构型，得到空间密度场：

$\rho(\boldsymbol{x}) = J^{-1}(\boldsymbol{\varphi}^{-1}(\boldsymbol{x})) \rho_0(\boldsymbol{\varphi}^{-1}(\boldsymbol{x}))$

举一个具体的例子 [@problem_id:3591885]，考虑一个具有非均匀参考密度 $\rho_0(\boldsymbol{X}) = \rho_\star (1 + \frac{1}{3} X_1^{2} - X_2 X_3)$ 的物体，它经历了由 $\boldsymbol{F}(\boldsymbol{X})$ 描述的变形。为了求出某物[质点](@entry_id:186768) $\boldsymbol{X}^\star$ 在变形后对应空间点 $\boldsymbol{x}^\star = \boldsymbol{\varphi}(\boldsymbol{X}^\star)$ 处的空间密度 $\rho(\boldsymbol{x}^\star)$，我们首先计算该点的变形梯度 $\boldsymbol{F}(\boldsymbol{X}^\star)$，然后求其[行列式](@entry_id:142978) $J(\boldsymbol{X}^\star)$。最后，利用关系式 $\rho(\boldsymbol{x}^\star) = \rho_0(\boldsymbol{X}^\star) / J(\boldsymbol{X}^\star)$ 即可得到所需结果。这个过程清晰地展示了如何利用雅可比行列式在不同构型之间转换[标量密度](@entry_id:161438)。

#### 矢量和[余矢量](@entry_id:157727)

矢量和余矢量（或称[1-形式](@entry_id:270392)，如梯度的对偶）的变换规则有所不同，这些规则是为了在变换过程中保持其固有的几何或物理意义。

一个定义在参考构型中的**物质矢量场 (material vector field)** $\boldsymbol{V}(\boldsymbol{X})$，例如代表材料纤维方向的矢量，其**[前推](@entry_id:158718)**到当前构型后得到空间矢量场 $\boldsymbol{v}(\boldsymbol{x})$，其变换法则为：

$\boldsymbol{v}(\boldsymbol{\varphi}(\boldsymbol{X})) = \boldsymbol{F}(\boldsymbol{X}) \boldsymbol{V}(\boldsymbol{X})$

这与[线元](@entry_id:196833)的变换规则一致，反映了[切空间](@entry_id:199137)向量的映射。

相对地，一个定义在当前构型中的**空间[余矢量场](@entry_id:186855) (spatial covector field)** $\boldsymbol{a}(\boldsymbol{x})$，例如某个标量场的空间梯度，其**后拉**到参考构型后得到物质[余矢量场](@entry_id:186855) $\boldsymbol{A}(\boldsymbol{X})$，其变换法则是：

$\boldsymbol{A}(\boldsymbol{X}) = \boldsymbol{F}^T(\boldsymbol{X}) \boldsymbol{a}(\boldsymbol{\varphi}(\boldsymbol{X}))$

这个变换法则的选择并非随意，其目的是为了保持[矢量与余矢量](@entry_id:635686)的[内积](@entry_id:158127)（对偶关系）在变换前后不变，即 $A \cdot V = a \cdot v$。这确保了与标量相关的物理量（如功率）在不同构型描述下的一致性。[@problem_id:3591928]

类似地，也存在空间矢量的后拉（$\boldsymbol{W} = \boldsymbol{F}^{-1}\boldsymbol{w}$）和物质余矢量的[前推](@entry_id:158718)（$\boldsymbol{b} = \boldsymbol{F}^{-T}\boldsymbol{B}$），它们在不同的物理情境中同样扮演着重要角色。

### 张量与运动学量度的变换

二阶及更[高阶张量](@entry_id:200122)的变换规则遵循着相似的逻辑，即保持其内在的物理和几何结构。

#### [面积元](@entry_id:263205)：南松公式

无穷小面积元的变换比线元更复杂。一个在参考构型中由法向 $\boldsymbol{N}$ 和面积 $dA$ 定义的矢量面元 $d\boldsymbol{A} = \boldsymbol{N}dA$，在变形后变为当前构型中的矢量面元 $d\boldsymbol{a} = \boldsymbol{n}da$。它们之间的关系由著名的**南松公式 (Nanson's formula)** 给出：

$\boldsymbol{n} da = J \boldsymbol{F}^{-T} \boldsymbol{N} dA$

这个公式可以通过考虑两个[切向量](@entry_id:265494)的[叉积](@entry_id:156672)如何在[线性映射](@entry_id:185132) $\boldsymbol{F}$ 下变换来推导。[@problem_id:3591941] 值得注意的是，当前法向 $\boldsymbol{n}$ 并非简单地由 $\boldsymbol{F}\boldsymbol{N}$ 得到，其变换涉及逆和[转置](@entry_id:142115)，这反映了[面积元](@entry_id:263205)变换的复杂几何性质。南松公式在推导[应力张量](@entry_id:148973)的变换关系时至关重要。

#### 度量张量与应变

度量张量定义了空间中的长度和角度。在标准的笛卡尔坐标系下，参考构型中的度量张量是单位张量 $\boldsymbol{I}$。

**左柯西-格林变形张量 (left Cauchy-Green deformation tensor)** $\boldsymbol{B}$ 可以被理解为参考构型度量张量 $\boldsymbol{I}$ 的[前推](@entry_id:158718)。[@problem_id:3591898] 具体来说，若将 $\boldsymbol{I}$ 写为[标准正交基](@entry_id:147779)的并矢和 $\boldsymbol{I} = \sum_{i=1}^{3} \boldsymbol{E}_i \otimes \boldsymbol{E}_i$，并应用[二阶张量](@entry_id:199780)的[前推](@entry_id:158718)法则 $\varphi_*(\boldsymbol{U} \otimes \boldsymbol{V}) = (\boldsymbol{F}\boldsymbol{U}) \otimes (\boldsymbol{F}\boldsymbol{V})$，我们得到：

$\varphi_*(\boldsymbol{I}) = \sum_{i=1}^{3} (\boldsymbol{F}\boldsymbol{E}_i) \otimes (\boldsymbol{F}\boldsymbol{E}_i) = \boldsymbol{F} \boldsymbol{I} \boldsymbol{F}^T = \boldsymbol{F}\boldsymbol{F}^T = \boldsymbol{B}$

因此，$\boldsymbol{B}$ 正是当前构型中的度量张量，它度量了变形后的长度和角度。

相对地，**右柯西-格林变形张量 (right Cauchy-Green deformation tensor)** $\boldsymbol{C} = \boldsymbol{F}^T\boldsymbol{F}$ 是空间度量张量的后拉，它将度量能力[拉回](@entry_id:160816)到参考构型中。一个物质线元 $d\boldsymbol{X}$ 的变形后长度平方 $ds^2$ 可以用 $\boldsymbol{C}$ 计算：$ds^2 = d\boldsymbol{x} \cdot d\boldsymbol{x} = (\boldsymbol{F}d\boldsymbol{X})\cdot(\boldsymbol{F}d\boldsymbol{X}) = d\boldsymbol{X} \cdot (\boldsymbol{F}^T\boldsymbol{F}d\boldsymbol{X}) = d\boldsymbol{X} \cdot (\boldsymbol{C}d\boldsymbol{X})$。

这些变形张量与[应变度量](@entry_id:755495)直接相关。**[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)** $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C}-\boldsymbol{I})$ 是一个物质度量，它完全在参考构型中定义。而**[欧拉-阿尔曼西应变张量](@entry_id:194948) (Euler-Almansi strain tensor)** $\boldsymbol{e} = \frac{1}{2}(\boldsymbol{I}-\boldsymbol{B}^{-1})$ 是一个空间度量。

这两种[应变度量](@entry_id:755495)通过[前推](@entry_id:158718)/后拉操作紧密相连。例如，沿当前构型中单位方向 $\widehat{\boldsymbol{n}}$ 的方向应变，可以通过一个纯粹的拉格朗日量——物质纤维的伸长率 $\lambda_{\boldsymbol{N}}$——来计算 [@problem_id:3581886]。这里的 $\boldsymbol{N}$ 是 $\widehat{\boldsymbol{n}}$ 在参考构型中的对应方向。其间的优美关系为：

$\widehat{\boldsymbol{n}} \cdot \boldsymbol{e} \cdot \widehat{\boldsymbol{n}} = \frac{1}{2} (1 - \lambda_{\boldsymbol{N}}^{-2})$

这个关系式体现了[前推](@entry_id:158718)/后拉思想的精髓：看似复杂的空间量（欧拉应变）可以通过转换到参考构型，用更直观的物理量（伸长率）来表达。

### 应力张量与力的变换

在有限变形理论中，存在多种应力张量，它们之间的转换是[前推](@entry_id:158718)与后拉操作的核心应用。

- **柯西应力张量 (Cauchy stress tensor)** $\boldsymbol{\sigma}$：也称为真实应力，是定义在当前构型上的[空间张量](@entry_id:185799)。它将当前构型的法向矢量 $\boldsymbol{n}$ 映射为作用在该面上的真实力（牵[引力](@entry_id:175476)）$\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$。
- **[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量 (First Piola-Kirchhoff stress tensor, PK1)** $\boldsymbol{P}$：也称为名义应力，是一个两点张量。它将参考构型的法向 $\boldsymbol{N}$ 映射到作用在变形后面积上的真实力，即名义牵[引力](@entry_id:175476) $\boldsymbol{T} = \boldsymbol{P}\boldsymbol{N}$。
- **[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量 (Second Piola-Kirchhoff stress tensor, PK2)** $\boldsymbol{S}$：是一个纯粹的物质张量，它在能量和本构关系中具有重要意义。

这些应力张量之间的关系源于作用在同一物质面元上的力在任何描述下都必须是相同的这一基本物理原理。即 $d\boldsymbol{f} = \boldsymbol{t} da = \boldsymbol{T} dA$。结合柯西应力定义和南松公式，我们可以推导出 $\boldsymbol{P}$ 和 $\boldsymbol{\sigma}$ 之间的**[皮奥拉变换](@entry_id:163790) (Piola transformation)** [@problem_id:3591895]：

$\boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-T}$

这个关系表明，第一PK应力 $\boldsymbol{P}$ 是通过对柯西应力 $\boldsymbol{\sigma}$ 进行缩放和后拉操作得到的。反过来，柯西应力可以通过[前推](@entry_id:158718)操作获得：$\boldsymbol{\sigma} = \frac{1}{J} \boldsymbol{P} \boldsymbol{F}^T$。

而第二PK应力 $\boldsymbol{S}$ 与 $\boldsymbol{P}$ 的关系通常被定义为：

$\boldsymbol{P} = \boldsymbol{F}\boldsymbol{S}$

这个关系可以看作是将物质[应力张量](@entry_id:148973) $\boldsymbol{S}$ “[前推](@entry_id:158718)”到两点张量 $\boldsymbol{P}$。结合以上关系，我们可以得到 $\boldsymbol{S}$ 与 $\boldsymbol{\sigma}$ 之间的联系，即 $\boldsymbol{S} = J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-T}$。这可以被解释为将**[基尔霍夫应力](@entry_id:751039) (Kirchhoff stress)** $\boldsymbol{\tau} = J\boldsymbol{\sigma}$ 从当前构型完全后拉到参考构型。

这些变换关系在实际计算中至关重要。例如，计算作用在某个变形后面元上的**名义牵[引力](@entry_id:175476)矢量 (nominal traction vector)** $\boldsymbol{T}$，需要执行一系列变换 [@problem_id:3591941]。首先，给定当前构型的法向 $\boldsymbol{n}$，需要通过后拉操作（利用南松公式）找到对应的参考法向 $\boldsymbol{N} \propto \boldsymbol{F}^T \boldsymbol{n}$。然后，利用[皮奥拉变换](@entry_id:163790)计算出 $\boldsymbol{P}$。最后，通过 $\boldsymbol{T} = \boldsymbol{P}\boldsymbol{N}$ 得到最终的力矢量。

### [客观性原理](@entry_id:185412)与张量性质

为什么我们需要定义如此多的应力张量？答案在于**[物质客观性原理](@entry_id:191727) (principle of material objectivity)**，也称框架无关性。该原理断言，材料的本构响应不应依赖于观察者的刚体运动。这意味着，如果在现有变形之上叠加一个刚体旋转（由[旋转张量](@entry_id:191990) $\boldsymbol{Q}$ 描述），材料的内在响应应保持不变。

在这样的叠加旋转下，各个运动学和动力学量的变换规律如下 [@problem_id:3591933]：
- 变形梯度：$\boldsymbol{F}^* = \boldsymbol{Q}\boldsymbol{F}$
- [左柯西-格林张量](@entry_id:186163)：$\boldsymbol{B}^* = \boldsymbol{F}^*(\boldsymbol{F}^*)^T = \boldsymbol{Q}\boldsymbol{B}\boldsymbol{Q}^T$
- 柯西应力：$\boldsymbol{\sigma}^* = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T$

这些量（$\boldsymbol{B}$ 和 $\boldsymbol{\sigma}$）都随观察者旋转，因此被称为**非客观的 (non-objective)** 或[空间张量](@entry_id:185799)。然而，当我们考察[皮奥拉-基尔霍夫应力](@entry_id:173629)时，会发现：
- 第一PK应力：$\boldsymbol{P}^* = \boldsymbol{F}^*\boldsymbol{S}^* = (\boldsymbol{Q}\boldsymbol{F})\boldsymbol{S}^*$
- 第二PK应力：$\boldsymbol{S}^* = (\boldsymbol{F}^*)^{-1}\boldsymbol{P}^* = (\boldsymbol{Q}\boldsymbol{F})^{-1}(\boldsymbol{Q}\boldsymbol{P}) = \boldsymbol{F}^{-1}\boldsymbol{Q}^{-1}\boldsymbol{Q}\boldsymbol{P} = \boldsymbol{F}^{-1}\boldsymbol{P} = \boldsymbol{S}$

这一推导揭示了一个深刻的结果：第二PK[应力张量](@entry_id:148973) $\boldsymbol{S}$ 在叠加刚体旋转下保持不变，即 $\boldsymbol{S}^* = \boldsymbol{S}$。因此，$\boldsymbol{S}$ 是一个**客观的 (objective)** 张量。这正是它在建立不依赖于观察者的[本构方程](@entry_id:138559)（例如[超弹性材料](@entry_id:190241)的[应变能函数](@entry_id:178435)）中占据核心地位的原因。

此外，这些变换关系也决定了应力[张量的对称性](@entry_id:202126) [@problem_id:3591914]。在没有[体力](@entry_id:174230)矩的经典连续介质中，角动量守恒要求柯西[应力张量](@entry_id:148973)必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$。通过后拉关系 $\boldsymbol{S} = J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-T}$，可以证明第二PK应力张量 $\boldsymbol{S}$ 也必须是对称的。然而，第一PK应力张量 $\boldsymbol{P} = \boldsymbol{F}\boldsymbol{S}$ 通常是**非对称的**，因为变形梯度 $\boldsymbol{F}$ 本身通常包含旋转和剪切，不是对称的，且矩阵乘法不满足交换律。

### [本构关系](@entry_id:186508)的[前推](@entry_id:158718)（进阶主题）

[前推](@entry_id:158718)与后拉操作的威力最终体现在它们能够变换整个[本构关系](@entry_id:186508)。一个在参考构型中形式简单的本构律，在被“[前推](@entry_id:158718)”到当前构型后，其形式可能会变得非常复杂。

考虑描述[材料弹性](@entry_id:751729)的四阶**[弹性张量](@entry_id:170728) (elasticity tensor)**。假设在参考构型中，材料是各向同性的，其[弹性张量](@entry_id:170728) $\mathbb{C}$ 具有标准形式。其到当前构型的**[前推](@entry_id:158718)**由以下法则定义：

$c_{ijkl} = J^{-1} F_{iI} F_{jJ} F_{kK} F_{lL} C_{IJKL}$

其中 $\boldsymbol{c}$ 是空间[弹性张量](@entry_id:170728)。这个变换保证了在两种构型下计算的[应力功率](@entry_id:182907)密度是等价的。

这个操作的一个重要启示是，一个初始为各向同性的材料，在经历非均匀变形后，其在当前构型中的力学行为通常表现为**各向异性**。例如，对于一个简单的[剪切变形](@entry_id:170920) [@problem_id:3591923]，其中变形梯度为 $F = \begin{pmatrix} 1 & \gamma & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix}$，我们可以计算出空间[弹性张量](@entry_id:170728)的某个分量，如 $c_{1212} = \mu + (\lambda + 2\mu)\gamma^2$。这里 $\lambda$ 和 $\mu$ 是材料的拉梅常数。这个结果表明，变形后材料的有效剪切刚度依赖于已经历的剪切变形量 $\gamma$，这正是变形诱导的各向异性的体现。这一概念对于理解材料在塑性成形、[大变形](@entry_id:167243)等过程中的行为至关重要。