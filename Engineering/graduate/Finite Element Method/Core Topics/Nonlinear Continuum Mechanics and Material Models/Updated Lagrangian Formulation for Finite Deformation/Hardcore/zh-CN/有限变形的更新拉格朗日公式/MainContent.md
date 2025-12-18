## 引言
在现代[计算固体力学](@entry_id:169583)中，[精确模拟](@entry_id:749142)结构和材料在经历大位移、大转动和[大应变](@entry_id:751152)时的行为是一个核心挑战。传统的线性分析方法在这种“有限变形”情况下会失效，因此需要更强大的理论框架。更新拉格朗日（Updated Lagrangian, UL）列式法正是为此类高度[非线性](@entry_id:637147)的问题而生的一种主流数值方法，其核心思想是通过不断更新参考构型，将复杂的变形过程分解为一系列易于处理的增量步。然而，这种增量方法也带来了新的理论和数值挑战，例如如何客观地描述应力率以及如何高效地[求解非线性方程](@entry_id:177343)组。

本文旨在系统地揭示更新拉格朗日列式法的完整图景。在接下来的章节中，我们将首先深入“原理与机制”部分，详细阐述其[运动学](@entry_id:173318)基础、[应力量度](@entry_id:198799)、[虚功原理](@entry_id:138749)以及为保证客观性而必须采用的率形式本构关系，并介绍其在有限元法中的离散化与求解策略。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章，我们将展示该方法如何应用于解决[弹塑性](@entry_id:193198)、[结构屈曲](@entry_id:171177)、接触力学等前沿工程与科学问题。最后，通过“动手实践”部分提供的具体计算问题，读者将有机会亲手应用所学知识，巩固对核心概念的理解。

## 原理与机制

更新拉格朗日（Updated Lagrangian, UL）列式是求解有限变形问题的一种强大而直观的数值方法。其核心思想是将每个增量步开始时的构型作为计算该增量步的参考构型。这种方法将复杂的、高度[非线性](@entry_id:637147)的总变形过程分解为一系列连续的、较小的增量变形。本章将系统地阐述更新拉格朗日列式的基本原理与关键机制，内容涵盖运动学描述、[应力量度](@entry_id:198799)、虚功原理、本构关系以及最终的[有限元离散化](@entry_id:193156)与求解算法。

### 更新拉格朗日列式的基本运动学

在有限变形理论中，精确描述物体的运动是首要任务。更新拉格朗日列式通过一种巧妙的方式来处理[运动学](@entry_id:173318)，即不断“更新”参考构型。

我们考虑三个关键构型：
1.  **初始构型 $\Omega_0$**：物体在时间 $t=0$ 时的未变形状态，物[质点](@entry_id:186768)的坐标用 $\boldsymbol{X}$ 表示。
2.  **前一构型 $\Omega_n$**：在离散的时间点 $t_n$，物体所处的已知构型。在更新拉格朗日列式中，此构型被选为计算下一步增量的**参考构型**。构型中的点用 $\boldsymbol{x}_n$ 表示。
3.  **当前构型 $\Omega_{n+1}$**：在时间点 $t_{n+1}$，物体所处的待求未知构型，其中的点用 $\boldsymbol{x}_{n+1}$ 表示。

总运动是一个将物质点从初始构型映射到当前构型的映射 $\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t)$。在离散的时间步中，到达构型 $\Omega_{n+1}$ 的运动可以看作是先运动到 $\Omega_n$，再从 $\Omega_n$ 运动到 $\Omega_{n+1}$ 的复合。这引出了**增量运动**的概念，即一个将点从前一构型 $\Omega_n$ 映射到当前构型 $\Omega_{n+1}$ 的映射：$\boldsymbol{x}_{n+1} = \boldsymbol{\varphi}_{n+1}(\boldsymbol{x}_n)$。

与这些运动相对应的是变形梯度。**总变形梯度** $\boldsymbol{F}$ 描述了从初始构型到当前构型的局部变形：
$$
\boldsymbol{F} = \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{X}}
$$
而在更新拉格朗日列式中，我们更关心**增量变形梯度** $\boldsymbol{f}$，它描述了从前一构型 $\Omega_n$到当前构型 $\Omega_{n+1}$ 的局部变形：
$$
\boldsymbol{f}_{n+1} = \frac{\partial \boldsymbol{x}_{n+1}}{\partial \boldsymbol{x}_n}
$$
根据链式法则，总变形梯度可以通过增量变形梯度进行乘法更新。从 $t=0$ 到 $t_{n+1}$ 的总变形梯度 $\boldsymbol{F}_{n+1}$ 是从 $t=0$ 到 $t_n$ 的总变形梯度 $\boldsymbol{F}_n$ 与从 $t_n$ 到 $t_{n+1}$ 的增量变形梯度 $\boldsymbol{f}_{n+1}$ 的乘积：
$$
\boldsymbol{F}_{n+1} = \frac{\partial \boldsymbol{x}_{n+1}}{\partial \boldsymbol{X}} = \frac{\partial \boldsymbol{x}_{n+1}}{\partial \boldsymbol{x}_n} \frac{\partial \boldsymbol{x}_n}{\partial \boldsymbol{X}} = \boldsymbol{f}_{n+1} \boldsymbol{F}_n
$$
这种乘法更新关系是更新拉格朗日列式运动学框架的基石。

在率形式的本构关系中，我们还需要描述变形的速率。**[空间速度梯度](@entry_id:187198)** $\boldsymbol{l}$ 被定义为[空间速度](@entry_id:190294)场 $\boldsymbol{v}$ 对当前空间坐标 $\boldsymbol{x}$ 的梯度，即 $\boldsymbol{l} = \nabla_{\boldsymbol{x}}\boldsymbol{v}$。它与总变形梯度的时间变化率 $\dot{\boldsymbol{F}}$ 之间存在一个基本关系：
$$
\boldsymbol{l} = \dot{\boldsymbol{F}}\boldsymbol{F}^{-1}
$$
在数值实现中，我们需要这个量的离散形式。在一个时间增量 $\Delta t = t_{n+1} - t_n$ 内，使用[后向欧拉法](@entry_id:139674)对 $\dot{\boldsymbol{F}}_{n+1}$ 进行近似，可以得到 $\boldsymbol{l}_{n+1}$ 在更新[拉格朗日框架](@entry_id:751113)下的近似表达式：
$$
\boldsymbol{l}_{n+1} \approx \frac{1}{\Delta t}(\boldsymbol{I} - \boldsymbol{f}_{n+1}^{-1})
$$
其中 $\boldsymbol{I}$ 是单位张量。这个表达式将[连续介质力学](@entry_id:155125)中的速度梯度与数值计算中的增量变形梯度直接联系起来。

### 当前构型中的动力学与[应力量度](@entry_id:198799)

更新拉格朗日列式的核心是在当前构型上建立[平衡方程](@entry_id:172166)，因此，最自然的应力测度是定义在当前变形体上的**柯西（Cauchy）[应力张量](@entry_id:148973)** $\boldsymbol{\sigma}$。柯西应力描述了当前构型中单位面积上所受的真实作用力。

然而，在有限变形理论中，为了建立与变形历史相关的本构关系，常常需要引入其他的应力测度。这些应力测度虽然不是直接出现在最终的[平衡方程](@entry_id:172166)中，但它们在应力更新的计算过程中扮演着关键角色。常用的应力测度包括：

1.  **基尔霍夫（Kirchhoff）应力张量 $\boldsymbol{\tau}$**：它是柯西应力的体积加权形式，定义为 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$，其中 $J = \det(\boldsymbol{F})$ 是变形梯度的[行列式](@entry_id:142978)，代表体积变化率。在处理[近不可压缩材料](@entry_id:752388)时，[基尔霍夫应力](@entry_id:751039)非常方便。

2.  **第二皮奥拉-基尔霍夫（Second Piola-Kirchhoff, 2nd PK）应力张量 $\boldsymbol{S}$**：这是一个定义在参考构型上的对称[应力张量](@entry_id:148973)。它与柯西应力之间通过变形梯度进行“[拉回](@entry_id:160816)”（pull-back）和“推前”（push-forward）操作来转换。

这些应力测度之间的转换关系可以通过力平衡和能量共轭原理导出。在一个从构型 $\Omega_n$ 到 $\Omega_{n+1}$ 的增量步中，描述该增量步的变形梯度为 $\boldsymbol{f}$，体积变化率为 $J_f = \det(\boldsymbol{f})$。在构型 $\Omega_{n+1}$ 中的柯西应力 $\boldsymbol{\sigma}_{n+1}$ 与相对于构型 $\Omega_n$ 定义的[第二皮奥拉-基尔霍夫应力](@entry_id:173163) $\boldsymbol{S}_{n+1}$ 之间通过“推前”（push-forward）操作相关联：
$$
\boldsymbol{\sigma}_{n+1} = J_f^{-1} \boldsymbol{f} \boldsymbol{S}_{n+1} \boldsymbol{f}^T
$$
这个关系是将定义在参考构型上的应力（$\boldsymbol{S}_{n+1}$）客观地转换为当前构型上的真实应力（$\boldsymbol{\sigma}_{n+1}$）的基本变换。在[应力更新算法](@entry_id:181937)中，首先要计算出增量步的应力 $\boldsymbol{S}_{n+1}$，然后通过此公式将其转换为柯西应力，用于构建[内力向量](@entry_id:750751)。

### 更新拉格朗日列式中的[虚功原理](@entry_id:138749)

有限元法的基础是积分形式的[平衡方程](@entry_id:172166)，即虚功原理。在更新拉格朗日列式中，虚功原理建立在**当前构型** $\Omega_t$ 之上。

我们从当前构型下的局部[动量平衡](@entry_id:193575)方程（即平衡[微分方程](@entry_id:264184)）出发，在忽略惯性效应的准静态情况下，该方程为：
$$
\nabla_{\boldsymbol{x}} \cdot \boldsymbol{\sigma} + \rho \boldsymbol{b} = \boldsymbol{0}
$$
其中 $\boldsymbol{\sigma}$ 是柯西应力，$\rho$ 是当前密度，$\boldsymbol{b}$ 是单位质量的[体力](@entry_id:174230)。

通过将上式与一个任意的、满足[位移边界条件](@entry_id:203261)的[虚位移](@entry_id:168781)场 $\delta\boldsymbol{u}$ 做[点积](@entry_id:149019)，并在当前体积 $\Omega_t$ 上积分，再利用[高斯散度定理](@entry_id:188065)，我们可以得到[虚功原理](@entry_id:138749)的表达式：
$$
\underbrace{\int_{\Omega_t} \boldsymbol{\sigma} : \nabla_{\boldsymbol{x}}\delta\boldsymbol{u} \, dv}_{\delta W_{int}} = \underbrace{\int_{\Omega_t} \rho \boldsymbol{b} \cdot \delta\boldsymbol{u} \, dv + \int_{\partial\Omega_t^t} \bar{\boldsymbol{t}} \cdot \delta\boldsymbol{u} \, da}_{\delta W_{ext}}
$$
该式表明，对于任意容许的[虚位移](@entry_id:168781)，内力所做的[虚功](@entry_id:176403)（$\delta W_{int}$）等于外力（体力 $\boldsymbol{b}$ 和在边界 $\partial\Omega_t^t$ 上的面力 $\bar{\boldsymbol{t}}$）所做的[虚功](@entry_id:176403)（$\delta W_{ext}$）。

一个至关重要的问题是：内部[虚功](@entry_id:176403)密度项 $\boldsymbol{\sigma} : \nabla_{\boldsymbol{x}}\delta\boldsymbol{u}$ 中的运动学量度 $\nabla_{\boldsymbol{x}}\delta\boldsymbol{u}$ 是否可以简化？答案是肯定的。根据[角动量守恒](@entry_id:156798)原理，在没有[体力](@entry_id:174230)偶的情况下，柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 必须是对称的。一个二阶张量（如 $\nabla_{\boldsymbol{x}}\delta\boldsymbol{u}$）可以分解为一个对称部分和一个反对称部分。一个[对称张量](@entry_id:148092)与一个[反对称张量](@entry_id:199349)的[双点积](@entry_id:748648)恒为零。因此，只有 $\nabla_{\boldsymbol{x}}\delta\boldsymbol{u}$ 的对称部分才对[内力](@entry_id:167605)[虚功](@entry_id:176403)有贡献。这个对称部分被称为**虚变形率张量** $\delta\boldsymbol{d}$：
$$
\delta\boldsymbol{d} = \frac{1}{2}\left( \nabla_{\boldsymbol{x}}\delta\boldsymbol{u} + (\nabla_{\boldsymbol{x}}\delta\boldsymbol{u})^T \right)
$$
于是，内部[虚功](@entry_id:176403)可以更精确地写为：
$$
\delta W_{int} = \int_{\Omega_t} \boldsymbol{\sigma} : \delta\boldsymbol{d} \, dv
$$
这种选择的物理意义在于，它确保了虚[刚体运动](@entry_id:193355)（包括虚平移和虚转动）不会产生内部[虚功](@entry_id:176403)。对于一个虚[刚体转动](@entry_id:191086)，其[位移梯度](@entry_id:165352) $\nabla_{\boldsymbol{x}}\delta\boldsymbol{u}$ 是纯反对称的，因此其对称部分 $\delta\boldsymbol{d}$ 为零，从而 $\delta W_{int}=0$。这符合物理直觉：一个处于平衡状态的物体在经历刚体运动时不应产生或消耗内部能量。因此，柯西应力 $\boldsymbol{\sigma}$ 与虚变形率 $\delta\boldsymbol{d}$ 构成了在当前构型下的**[功共轭](@entry_id:194957)对**。

### 本构模型：客观性的挑战

在更新拉格朗日列式中，由于参考构型不断更新，[本构关系](@entry_id:186508)通常以率形式（rate form）给出，即建立应力率和应变率之间的关系。一个核心要求是，[本构定律](@entry_id:178936)必须满足**物质[坐标系](@entry_id:156346)无关性原理**，也称**客观性（objectivity）**。这意味着材料的响应不应依赖于观察者（或[坐标系](@entry_id:156346)）的刚体运动。

如果我们天真地使用柯西应力的材料时间导数 $\dot{\boldsymbol{\sigma}}$ 作为应力率，将会导致严重问题。考虑一个仅经历[刚体转动](@entry_id:191086)的物体。在这种情况下，物体没有发生任何实际的变形，因此变形率张量 $\boldsymbol{d} = \boldsymbol{0}$。一个简单的率形式本构律（如 $\dot{\boldsymbol{\sigma}} = \mathcal{C}[\boldsymbol{d}]$）会预测 $\dot{\boldsymbol{\sigma}} = \boldsymbol{0}$。这意味着在固定的空间[坐标系](@entry_id:156346)中，应力张量保持不变。然而，从物理上看，正确的行为是应力张量应该随着物体一起转动。例如，如果[初始应力](@entry_id:750652)为 $\boldsymbol{\sigma}(0)$，经过旋转 $\boldsymbol{R}(t)$ 后，正确的应力应为 $\boldsymbol{\sigma}_{exact}(t) = \boldsymbol{R}(t)\boldsymbol{\sigma}(0)\boldsymbol{R}^T(t)$。错误的预测 $\boldsymbol{\sigma}_{nonobj}(t) = \boldsymbol{\sigma}(0)$ 与正确值之间的误差会随着转动角度的增加而累积，产生完全不符合物理实际的“伪应力”。

为了解决这个问题，必须使用**[客观应力率](@entry_id:199282)**。[客观应力率](@entry_id:199282)测量的是在一个随体旋转的（即余旋的，corotational）[坐标系](@entry_id:156346)下的应力变化率。一个通用的余旋应力率可以写成：
$$
\overset{\triangledown}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Omega}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Omega}
$$
其中 $\boldsymbol{\Omega}$ 是一个代表余旋[坐标系](@entry_id:156346)自旋的[反对称张量](@entry_id:199349)。对 $\boldsymbol{\Omega}$ 的不同选择导致了不同类型的[客观应力率](@entry_id:199282)。两种最常见的选择是：

1.  **[Jaumann 率](@entry_id:185572)**：选择连续体的[自旋张量](@entry_id:187346) $\boldsymbol{W}$ 作为余旋自旋，即 $\boldsymbol{\Omega} = \boldsymbol{W} = \frac{1}{2}(\boldsymbol{l} - \boldsymbol{l}^T)$。这是最简单、最常用的一种[客观率](@entry_id:198692)。

2.  **Green-Naghdi 率**：选择与变形梯度极分解 $\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$ 中的[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 相关联的自旋，即 $\boldsymbol{\Omega} = \dot{\boldsymbol{R}}\boldsymbol{R}^T$。

这两种率都是客观的，能正确处理[刚体转动](@entry_id:191086)问题。然而，在包含大[剪切变形](@entry_id:170920)的问题中，它们的表现有所不同。例如，在使用 [Jaumann 率](@entry_id:185572)的各向同性[弹塑性](@entry_id:193198)模型中，简单剪切问题可能会出现非物理的应力[振荡](@entry_id:267781)现象。而 Green-Naghdi 率由于其自旋直接来自于材料本身的旋转，通常能更好地处理这类问题，提供更平滑、更符合物理直觉的应力响应。这表明，即使在满足客观性的前提下，选择合适的应力率对于获得精确的数值解仍然至关重要。

### 有限元离散与求解过程

将连续的虚功原理转化为可解的[代数方程](@entry_id:272665)组，需要进行有限元离散。在更新拉格朗日列式中，所有离散化操作和积分都在当前构型上进行。

**等参元插值**

在[等参单元](@entry_id:173863)中，单元的几何形状和单元内的[位移场](@entry_id:141476)使用相同的形函数进行插值。这些形函数定义在一个简单的“父单元”上，其坐标为 $\boldsymbol{\xi}$。当前构型中任意一点的坐标 $\boldsymbol{x}$ 可以通过其节点坐标 $\boldsymbol{x}_a$ 和父[单元形函数](@entry_id:198891) $\widehat{N}_a(\boldsymbol{\xi})$ 来插值得到：
$$
\boldsymbol{x}(\boldsymbol{\xi}) = \sum_{a} \widehat{N}_a(\boldsymbol{\xi}) \boldsymbol{x}_a
$$
在计算虚[功积[](@entry_id:181218)分时](@entry_id:274419)，我们需要形函数对空间坐标 $\boldsymbol{x}$ 的梯度 $\nabla_{\boldsymbol{x}}N_a$。这可以通过链式法则，利用从父单元到当前单元的[雅可比矩阵](@entry_id:264467) $\boldsymbol{J} = \partial\boldsymbol{x}/\partial\boldsymbol{\xi}$ 来计算：
$$
\nabla_{\boldsymbol{x}}N_a = \boldsymbol{J}^{-T} \nabla_{\boldsymbol{\xi}}\widehat{N}_a
$$
由于几何构型在每个迭代步中都会更新，[雅可比矩阵](@entry_id:264467) $\boldsymbol{J}$ 及其逆也需要相应地不断重新计算。

**[Newton-Raphson](@entry_id:177436) 迭代求解**

将有限元插值代入[虚功原理](@entry_id:138749)，我们得到一个关于节点位移增量 $\boldsymbol{d}$ 的[非线性](@entry_id:637147)[代数方程](@entry_id:272665)组：
$$
\boldsymbol{r}(\boldsymbol{d}) = \boldsymbol{f}_{int}(\boldsymbol{d}) - \boldsymbol{f}_{ext} = \boldsymbol{0}
$$
其中，$\boldsymbol{r}(\boldsymbol{d})$ 是**[残差向量](@entry_id:165091)**，代表在当前试探构型下的[不平衡力](@entry_id:753019)。$\boldsymbol{f}_{int}$ 是依赖于位移的[内力向量](@entry_id:750751)，$\boldsymbol{f}_{ext}$ 是外力向量。

为了求解这个非线性方程组，标准方法是采用 **[Newton-Raphson](@entry_id:177436) [迭代法](@entry_id:194857)**。在第 $k$ 次迭代中，我们对残差方程进行线性化，得到一个关于位移修正量 $\Delta\boldsymbol{d}^{(k)}$ 的[线性方程组](@entry_id:148943)：
$$
\boldsymbol{K}_T^{(k)} \Delta\boldsymbol{d}^{(k)} = - \boldsymbol{r}^{(k)}
$$
求解后，更新位移和节点坐标：
$$
\boldsymbol{d}^{(k+1)} = \boldsymbol{d}^{(k)} + \Delta\boldsymbol{d}^{(k)} \quad \text{以及} \quad \boldsymbol{x}^{(k+1)} = \boldsymbol{x}^{(k)} + \Delta\boldsymbol{d}^{(k)}
$$
重复此过程直至残差 $\boldsymbol{r}$ 或位移修正量 $\Delta\boldsymbol{d}$ 小于某个预设的容差。

方程中的 $\boldsymbol{K}_T$ 是**[一致切线刚度矩阵](@entry_id:747734)**，它是[残差向量](@entry_id:165091)对节点位移的精确导数 $\boldsymbol{K}_T = \partial\boldsymbol{r}/\partial\boldsymbol{d}$。在有限变形问题中，它自然地分为两个部分：
1.  **材料刚度矩阵 $\boldsymbol{K}_{mat}$**：源于应力对应变的本构响应，它包含了材料的[切线](@entry_id:268870)模量。
2.  **[几何刚度矩阵](@entry_id:162967) $\boldsymbol{K}_{geo}$**：也称为初应力矩阵，它源于在现有应力作用下，因几何构型变化而引起的平衡关系改变。它与当前的柯西应力 $\boldsymbol{\sigma}$ 成线性关系。

使用[一致切线刚度矩阵](@entry_id:747734)至关重要。根据数值分析理论，只有当[迭代矩阵](@entry_id:637346)是残差的精确导数时，[Newton-Raphson](@entry_id:177436) 方法才能在解的邻域内实现**二次收敛**。这意味着每次迭代，解的[有效数字](@entry_id:144089)位数大约会翻倍，从而极大地提高了[计算效率](@entry_id:270255)。

如果使用一个近似的[切线](@entry_id:268870)矩阵，例如忽略[几何刚度](@entry_id:172820)部分，或者使用不更新的[切线](@entry_id:268870)矩阵（修正 Newton 法），那么收敛速度将退化为线性或超线性。这通常会导致收敛需要更多的迭代次数，并且对载荷步长更加敏感，可能需要更小的载荷步才能保证收敛。对于[超弹性材料](@entry_id:190241)，其[一致切线刚度矩阵](@entry_id:747734)具有对称性，这一性质可以被[线性方程](@entry_id:151487)求解器有效利用。而任意的[割线](@entry_id:178768)近似（secant approximation）通常不具备这种对称性，可能会牺牲[计算效率](@entry_id:270255)。因此，尽管计算[一致切线刚度矩阵](@entry_id:747734)较为复杂，但它为求解[非线性有限元](@entry_id:173184)问题提供了最快和最稳健的收敛性。