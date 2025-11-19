## 引言
在现代工程与科学领域，精确描述材料在极端载荷下的行为至关重要，这通常涉及到“[大变形](@entry_id:167243)”问题。在这些情况下，物体的形状和尺寸会发生显著改变，使得传统的基于初始构形的线性力学理论不再适用。我们所熟知的柯西应力张量虽然描述了变形后物体的“真实”应力，但它定义在不断变化的当前构形上，这为建立和求解控制方程带来了巨大的复杂性。为了克服这一挑战，[连续介质力学](@entry_id:155125)引入了一系列在固定不变的参考构形上定义的应力测度，其中最核心的便是第一和第二类[Piola-Kirchhoff应力](@entry_id:173629)张量。

本文旨在系统地揭开这两种关键应力张量的面纱，为读者构建一个从基本概念到前沿应用的完整知识框架。我们将首先在“原理与机制”一章中，深入探讨第一和第二类[Piola-Kirchhoff应力](@entry_id:173629)张量的定义、物理内涵以及它们之间和与柯西应力的数学关系，并分析其对称性与客观性等关键性质。接着，在“应用与跨学科联系”一章中，我们将展示这些理论工具如何在超弹性理论、[软组织生物力学](@entry_id:191910)和计算力学等领域发挥实际作用，将抽象的张量与具体的工程问题联系起来。最后，通过“动手实践”部分提供的一系列计算问题，读者将有机会亲手应用所学知识，巩固对这些重要概念的理解。

## 原理与机制

在处理固体力学中的[大变形](@entry_id:167243)问题时，将物体的当前构形（current configuration）与其初始的、未变形的参考构形（reference configuration）进行比较是一种至关重要的分析方法。我们熟悉的柯西应力张量（Cauchy stress tensor）是在当前构形中定义的，它描述了变形后物体内部的“真实”应力。然而，为了在固定的参考构形上建立控制方程，我们需要引入新的[应力张量](@entry_id:148973)，这些张量能够将力与参考构形中的几何元素联系起来。本章将系统地介绍第一和第二类[Piola-Kirchhoff应力](@entry_id:173629)张量，阐明它们的定义、物理意义、相互关系以及在连续介质力学基本定律中的核心作用。

### 第一类[Piola-Kirchhoff应力](@entry_id:173629)张量：连接过去与现在的桥梁

在分析变形体时，我们关心的力是作用在当前构形上的真实物理力。然而，变形后物体的几何形状可能是复杂且随时间变化的，这给求解带来了困难。一个有效的策略是将问题[拉回](@entry_id:160816)到固定不变的参考构形中进行分析。为此，我们需要一个能够将当前构形中的力与参考构形中面积元联系起来的物理量。

我们定义**第一类Piola-Kirchhoff (PK1)应力张量 (First Piola-Kirchhoff stress tensor)**，记为 $\boldsymbol{P}$，它精确地扮演了这个角色。考虑作用在当前构形中一个面积元 $da$ 上的力矢量 $d\boldsymbol{f}$。这个[面积元](@entry_id:263205)的[单位法向量](@entry_id:178851)为 $\boldsymbol{n}$。根据柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的定义，我们有 $d\boldsymbol{f} = \boldsymbol{\sigma}\boldsymbol{n} \, da$。现在，我们将这个力 $d\boldsymbol{f}$ 与其在参考构形中对应的面积元 $dA$ （[单位法向量](@entry_id:178851)为 $\boldsymbol{N}$）关联起来。PK1[应力张量](@entry_id:148973) $\boldsymbol{P}$ 被定义为这样一个张量，它通过参考构形的法向量 $\boldsymbol{N}$ 直接给出作用在每单位参考面积上的力，这个力被称为**名义牵[引力](@entry_id:175476) (nominal traction)** $\boldsymbol{T}$。

$$
\boldsymbol{T} = \boldsymbol{P}\boldsymbol{N}
$$

总的作用力 $d\boldsymbol{f}$ 因此也可以表示为 $d\boldsymbol{f} = \boldsymbol{T} \, dA = \boldsymbol{P}\boldsymbol{N} \, dA$。通过力的等效性，我们得到：

$$
\boldsymbol{P}\boldsymbol{N} \, dA = \boldsymbol{\sigma}\boldsymbol{n} \, da
$$

为了建立 $\boldsymbol{P}$ 和 $\boldsymbol{\sigma}$ 之间的关系，我们需要联系两个构形中的[面积元](@entry_id:263205)。这一联系由著名的**[南森公式](@entry_id:195566) (Nanson's formula)** 给出，它源于变形的[运动学](@entry_id:173318)：$\boldsymbol{n} \, da = J \boldsymbol{F}^{-T} \boldsymbol{N} \, dA$。其中，$\boldsymbol{F}$ 是**变形梯度 (deformation gradient)**，定义为 $\boldsymbol{F} = \nabla_{\boldsymbol{X}} \boldsymbol{x}$，它将参考构形中的线元映射到当前构形；$J = \det(\boldsymbol{F})$ 是变形的[雅可比行列式](@entry_id:137120)，代表了体积的变化率；$\boldsymbol{F}^{-T}$ 表示 $\boldsymbol{F}$ 的逆的转置。将[南森公式](@entry_id:195566)代入力的[平衡方程](@entry_id:172166)中，我们得到：

$$
\boldsymbol{P}\boldsymbol{N} \, dA = \boldsymbol{\sigma} (J \boldsymbol{F}^{-T} \boldsymbol{N}) \, dA
$$

由于该关系对任意参考[面积元](@entry_id:263205) $\boldsymbol{N} \, dA$ 均成立，我们便得到了第一类[Piola-Kirchhoff应力](@entry_id:173629)张量与柯西应力张量之间的基本关系 [@problem_id:2641039]：

$$
\boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-T}
$$

从这个定义可以看出，$\boldsymbol{P}$ 将参考构形中的一个矢量（法向量 $\boldsymbol{N}$）映射到当前构形中的一个矢量（名义牵[引力](@entry_id:175476) $\boldsymbol{T}$）。因此，$\boldsymbol{P}$ 是一个**两点张量 (two-point tensor)**，它的分量混合了两个构形的信息。

反过来，我们也可以从 $\boldsymbol{P}$ 和 $\boldsymbol{F}$ 计算出柯西应力 $\boldsymbol{\sigma}$：

$$
\boldsymbol{\sigma} = \frac{1}{J} \boldsymbol{P} \boldsymbol{F}^{T}
$$

例如，在一个二维问题中，若变形梯度 $\boldsymbol{F} = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}$ 且第一类PK应力 $\boldsymbol{P} = \begin{pmatrix} 0 & \tau \\ \tau & 0 \end{pmatrix}$，我们可以计算出雅可比 $J = 2 \cdot 2 - 1 \cdot 1 = 3$。由于 $\boldsymbol{F}$ 是对称的，$\boldsymbol{F}^T = \boldsymbol{F}$。因此，对应的柯西应力为 [@problem_id:1549745]：

$$
\boldsymbol{\sigma} = \frac{1}{3} \begin{pmatrix} 0 & \tau \\ \tau & 0 \end{pmatrix} \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix} = \frac{1}{3} \begin{pmatrix} \tau & 2\tau \\ 2\tau & \tau \end{pmatrix}
$$

### 第二类[Piola-Kirchhoff应力](@entry_id:173629)张量：完全的物质描述

尽管 $\boldsymbol{P}$ 张量在将平衡方程转换到参考构形时非常有用 [@problem_id:1549756]，但它作为两点张量，并且通常是非对称的（下文将详细讨论），这在建立本构关系时带来了不便。理想的[本构关系](@entry_id:186508)应该将材料的内在响应（应力）与纯粹的材料变形（应变）联系起来，这两者都应该是在参考构形中描述的、与观察者无关的量。

为此，我们引入**第二类Piola-Kirchhoff (PK2)[应力张量](@entry_id:148973) (Second Piola-Kirchhoff stress tensor)**，记为 $\boldsymbol{S}$。其物理思想是将作用在当前构形中的力矢量 $d\boldsymbol{f}$ 也通过变形梯度“[拉回](@entry_id:160816)” (pull-back) 到参考构形中，得到一个虚构的力矢量 $\boldsymbol{F}^{-1} d\boldsymbol{f}$。$\boldsymbol{S}$ 张量被定义为将参考构形中的法向量 $\boldsymbol{N}$ 映射到这个“[拉回](@entry_id:160816)力”的张量 [@problem_id:2641038]。

$$
\boldsymbol{F}^{-1} d\boldsymbol{f} = \boldsymbol{S}\boldsymbol{N} \, dA
$$

结合 $d\boldsymbol{f} = \boldsymbol{P}\boldsymbol{N} \, dA$，我们得到 $\boldsymbol{F}^{-1}(\boldsymbol{P}\boldsymbol{N} \, dA) = \boldsymbol{S}\boldsymbol{N} \, dA$，这揭示了 $\boldsymbol{S}$ 和 $\boldsymbol{P}$ 之间的简单关系：

$$
\boldsymbol{S} = \boldsymbol{F}^{-1} \boldsymbol{P} \quad \text{或等价地} \quad \boldsymbol{P} = \boldsymbol{F} \boldsymbol{S}
$$

将 $\boldsymbol{P} = J\boldsymbol{\sigma}\boldsymbol{F}^{-T}$ 代入，我们得到 $\boldsymbol{S}$ 与柯西应力 $\boldsymbol{\sigma}$ 的直接关系：

$$
\boldsymbol{S} = J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-T}
$$

这个关系式被称为**[皮奥拉变换](@entry_id:163790) (Piola transform)**，它将一个定义在当前构形中的张量（此处为 $J\boldsymbol{\sigma}$，即[Kirchhoff应力](@entry_id:751039)）[拉回](@entry_id:160816)到参考构形中。$\boldsymbol{S}$ 的所有部分都与参考构形相关，因此它是一个纯粹的**拉格朗日张量 (Lagrangian tensor)** 或**物质张量 (material tensor)**。

我们可以通过一个简单的例子来直观理解 $\boldsymbol{P}$ 和 $\boldsymbol{S}$ 的区别。考虑一个物体承受均匀的静水压力 $\boldsymbol{\sigma} = -p\boldsymbol{I}$，并发生均匀的体积膨胀，其变形梯度为 $\boldsymbol{F} = \lambda\boldsymbol{I}$，其中 $\lambda$ 是伸长比 [@problem_id:1549789]。通过计算可得：

$$
\boldsymbol{P} = -p\lambda^{2}\boldsymbol{I} \quad \text{以及} \quad \boldsymbol{S} = -p\lambda\boldsymbol{I}
$$

这个结果清晰地表明 $\boldsymbol{P} = \lambda\boldsymbol{S} = \boldsymbol{F}\boldsymbol{S}$。$\boldsymbol{S}$ 的量值与 $\lambda$ 成正比，反映了力被[拉回](@entry_id:160816)到参考长度尺度上的效果；而 $\boldsymbol{P}$ 的量值与 $\lambda^2$ 成正比，因为它直接关联的是参考“面积”。

### [Piola-Kirchhoff应力](@entry_id:173629)张量的关键性质

#### 对称性

对称性是应力张量的一个核心性质，它与角动量守恒定律紧密相关。在没有[体力](@entry_id:174230)矩和耦合应力的前提下，空间构形中的角动量守恒要求柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$。这是我们分析[Piola-Kirchhoff应力](@entry_id:173629)[张量对称性](@entry_id:191651)的出发点 [@problem_id:2640989]。

首先考察 $\boldsymbol{S}$ 张量。对其定义式取[转置](@entry_id:142115)：

$$
\boldsymbol{S}^T = (J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-T})^T = J (\boldsymbol{F}^{-T})^T \boldsymbol{\sigma}^T (\boldsymbol{F}^{-1})^T = J \boldsymbol{F}^{-1} \boldsymbol{\sigma}^T \boldsymbol{F}^{-T}
$$

由于 $\boldsymbol{\sigma}$ 是对称的（$\boldsymbol{\sigma}^T = \boldsymbol{\sigma}$），我们立即得到 $\boldsymbol{S}^T = \boldsymbol{S}$。这意味着，**如果柯西应力是对称的，那么第二类[Piola-Kirchhoff应力](@entry_id:173629)张量也总是对称的** [@problem_id:2641038] [@problem_id:1549770]。

然而，第一类[Piola-Kirchhoff应力](@entry_id:173629)张量 $\boldsymbol{P}$ 通常是**非对称**的。对其定义式取转置：

$$
\boldsymbol{P}^T = (J \boldsymbol{\sigma} \boldsymbol{F}^{-T})^T = J (\boldsymbol{F}^{-T})^T \boldsymbol{\sigma}^T = J \boldsymbol{F}^{-1} \boldsymbol{\sigma}^T = J \boldsymbol{F}^{-1} \boldsymbol{\sigma}
$$

将此结果与 $\boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-T}$ 比较，可以发现除非在非常特殊的情况下（例如，变形是纯体积膨胀），否则 $\boldsymbol{P} \neq \boldsymbol{P}^T$ [@problem_id:2641039]。

$\boldsymbol{P}$ 的非对称性是否意味着角动量不守恒？答案是否定的。[角动量守恒](@entry_id:156798)在物质描述下的正确表达形式并非要求 $\boldsymbol{P}$ 对称，而是要求张量 $\boldsymbol{P}\boldsymbol{F}^T$ 是对称的。我们可以验证这一点：

$$
\boldsymbol{P}\boldsymbol{F}^T = (J \boldsymbol{\sigma} \boldsymbol{F}^{-T}) \boldsymbol{F}^T = J \boldsymbol{\sigma} (\boldsymbol{F}^{-T}\boldsymbol{F}^T) = J\boldsymbol{\sigma}
$$

张量 $J\boldsymbol{\sigma}$ 被称为**[基尔霍夫应力](@entry_id:751039)张量 (Kirchhoff stress tensor)**。由于 $J$ 是标量且 $\boldsymbol{\sigma}$ 是对称的，所以 $J\boldsymbol{\sigma}$ 必然是对称的。因此，$\boldsymbol{P}\boldsymbol{F}^T$ 的对称性自然得到保证，角动量守恒定律得以满足 [@problem_id:2640989]。$\boldsymbol{P}$ 的非对称性恰好与变形 $\boldsymbol{F}$ 的几何效应[相平衡](@entry_id:136822)，从而确保了物理上的[力矩平衡](@entry_id:752138)。

#### 客观性与[坐标系](@entry_id:156346)不变性

一个重要的物理原则是，材料的本构响应不应依赖于观察者（即[坐标系](@entry_id:156346)）的刚体运动。这个性质被称为**客观性 (objectivity)** 或**[坐标系](@entry_id:156346)[不变性](@entry_id:140168) (frame-invariance)**。考虑在当前构形上叠加一个刚体旋转，由正交张量 $\boldsymbol{Q}$ 描述，新的空间位置为 $\boldsymbol{x}^* = \boldsymbol{Q}\boldsymbol{x}$。

在此变换下，变形梯度变为 $\boldsymbol{F}^* = \boldsymbol{Q}\boldsymbol{F}$。柯西应力作为一个客观的[空间张量](@entry_id:185799)，其变换规律为 $\boldsymbol{\sigma}^* = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T$。我们来考察PK[应力张量](@entry_id:148973)的变换行为。对于第一类PK应力 $\boldsymbol{P}$ [@problem_id:2641039]：

$$
\boldsymbol{P}^* = J^* \boldsymbol{\sigma}^* (\boldsymbol{F}^*)^{-T} = J (\boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T) (\boldsymbol{Q}\boldsymbol{F})^{-T} = J (\boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T) (\boldsymbol{Q}\boldsymbol{F}^{-T}) = \boldsymbol{Q}(J\boldsymbol{\sigma}\boldsymbol{F}^{-T}) = \boldsymbol{Q}\boldsymbol{P}
$$

由于 $\boldsymbol{P}^* = \boldsymbol{Q}\boldsymbol{P} \neq \boldsymbol{P}$，所以 $\boldsymbol{P}$ 不是一个客观张量。它的值会随着观察者[坐标系](@entry_id:156346)的旋转而改变。

现在考察第二类PK应力 $\boldsymbol{S}$ [@problem_id:1549814]：

$$
\boldsymbol{S}^* = (\boldsymbol{F}^*)^{-1} \boldsymbol{P}^* = (\boldsymbol{Q}\boldsymbol{F})^{-1} (\boldsymbol{Q}\boldsymbol{P}) = (\boldsymbol{F}^{-1}\boldsymbol{Q}^{-1})(\boldsymbol{Q}\boldsymbol{P}) = \boldsymbol{F}^{-1}(\boldsymbol{Q}^T\boldsymbol{Q})\boldsymbol{P} = \boldsymbol{F}^{-1}\boldsymbol{P} = \boldsymbol{S}
$$

我们发现 $\boldsymbol{S}^* = \boldsymbol{S}$。这意味着**第二类[Piola-Kirchhoff应力](@entry_id:173629)张量在当前构形的刚体旋转下保持不变**。这一优良特性使得 $\boldsymbol{S}$ 成为建立[本构方程](@entry_id:138559)的理想选择，因为它所衡量的应力状态是材料的内在属性，与外部观察者的旋转无关。

### 在物理定律中的应用

#### [应力功率](@entry_id:182907)与[功共轭](@entry_id:194957)关系

**[应力功率](@entry_id:182907) (stress power)** 是指应力在[材料变形](@entry_id:169356)过程中做功的速率。单位参考体积内的[应力功率](@entry_id:182907) $\dot{W}$ 可以表示为第一类PK应力 $\boldsymbol{P}$ 与变形梯度率 $\dot{\boldsymbol{F}}$ 的[双点积](@entry_id:748648)：

$$
\dot{W} = \boldsymbol{P} : \dot{\boldsymbol{F}}
$$

这个表达式有一个等价形式，它揭示了 $\boldsymbol{S}$ 张量在能量上的重要意义。我们将 $\boldsymbol{P}=\boldsymbol{F}\boldsymbol{S}$ 代入上式：

$$
\dot{W} = (\boldsymbol{F}\boldsymbol{S}) : \dot{\boldsymbol{F}} = \boldsymbol{S} : (\boldsymbol{F}^T \dot{\boldsymbol{F}})
$$

我们引入**[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)** $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{F}^T\boldsymbol{F} - \boldsymbol{I})$，它是一个纯粹的物质[应变度量](@entry_id:755495)。其时间变化率为 $\dot{\boldsymbol{E}} = \frac{1}{2}(\dot{\boldsymbol{F}}^T\boldsymbol{F} + \boldsymbol{F}^T\dot{\boldsymbol{F}})$。由于 $\boldsymbol{S}$ 是对称的，可以证明 $\boldsymbol{S}:(\dot{\boldsymbol{F}}^T\boldsymbol{F}) = \boldsymbol{S}:(\boldsymbol{F}^T\dot{\boldsymbol{F}})$。因此：

$$
\boldsymbol{S} : \dot{\boldsymbol{E}} = \boldsymbol{S} : \frac{1}{2}(\dot{\boldsymbol{F}}^T\boldsymbol{F} + \boldsymbol{F}^T\dot{\boldsymbol{F}}) = \boldsymbol{S} : (\boldsymbol{F}^T \dot{\boldsymbol{F}})
$$

比较可知，我们得到了一个至关重要的恒等式 [@problem_id:2641039] [@problem_id:2641038] [@problem_id:1549750]：

$$
\boldsymbol{P} : \dot{\boldsymbol{F}} = \boldsymbol{S} : \dot{\boldsymbol{E}}
$$

这个关系表明，应力-应变对 $(\boldsymbol{P}, \boldsymbol{F})$ 和 $(\boldsymbol{S}, \boldsymbol{E})$ 在能量上是**[功共轭](@entry_id:194957) (work-conjugate)**的。这意味着，如果一个材料的[应变能密度函数](@entry_id:755490)是基于 $\boldsymbol{E}$ 表达的，那么通过对[应变能函数](@entry_id:178435)求导，我们就能得到与之共轭的应力 $\boldsymbol{S}$。这是超[弹性理论](@entry_id:184142)的基石。

#### [平衡方程](@entry_id:172166)

在静态平衡条件下，物体[内力](@entry_id:167605)的合力与[体力](@entry_id:174230)之和为零。这个原理可以用不同的构形来表述。在当前（空间）构形中，平衡方程是大家所熟知的：

$$
\text{div}(\boldsymbol{\sigma}) + \boldsymbol{b} = 0
$$

其中 $\text{div}(\cdot)$ 是关于空间坐标 $\boldsymbol{x}$ 的[散度算子](@entry_id:265975)，$\boldsymbol{b}$ 是单位当前体积的体力密度。

通过[Piola-Kirchhoff应力](@entry_id:173629)，我们可以将平衡方程转化到参考（物质）构形中。使用第一类PK应力 $\boldsymbol{P}$，物质形式的平衡方程写作：

$$
\text{Div}(\boldsymbol{P}) + \boldsymbol{b}_0 = 0
$$

其中 $\text{Div}(\cdot)$ 是关于物质坐标 $\boldsymbol{X}$ 的[散度算子](@entry_id:265975)，$\boldsymbol{b}_0$ 是单位参考体积的体力密度。这两个方程描述的是同一个物理状态。它们之间的联系可以通过**皮奥拉恒等式 (Piola identity)** 建立，该恒等式对任何光滑的[空间张量](@entry_id:185799)场 $\boldsymbol{\tau}$ 成立：$\text{Div}(J\boldsymbol{\tau}\boldsymbol{F}^{-T}) = J\,\text{div}(\boldsymbol{\tau})$。

令 $\boldsymbol{\tau} = \boldsymbol{\sigma}$，我们有 $\text{Div}(\boldsymbol{P}) = \text{Div}(J\boldsymbol{\sigma}\boldsymbol{F}^{-T}) = J\,\text{div}(\boldsymbol{\sigma})$。代入物质[平衡方程](@entry_id:172166)，得到 $J\,\text{div}(\boldsymbol{\sigma}) + \boldsymbol{b}_0 = 0$。与空间平衡方程 $J\,\text{div}(\boldsymbol{\sigma}) + J\boldsymbol{b} = 0$ 比较，我们便得到了两种[体力](@entry_id:174230)密度之间的关系 [@problem_id:1549756]：

$$
\boldsymbol{b}_0 = J\boldsymbol{b}
$$

这一转换表明，通过引入 $\boldsymbol{P}$ 张量，我们可以将在随时间变化的复杂区域上的[偏微分方程](@entry_id:141332)，转化为在固定不变的参考区域上的方程，这极大地简化了问题的求解，尤其是在数值计算中。