## 引言
在现代计算固体力学中，精确模拟结构和材料在经历大位移、大转动和大应变时的行为是一个核心挑战。传统的线性分析方法在这种“有限变形”情况下会失效，因此需要更强大的理论框架。更新拉格朗日（Updated Lagrangian, UL）列式法正是为此类高度非线性的问题而生的一种主流数值方法，其核心思想是通过不断更新参考构型，将复杂的变形过程分解为一系列易于处理的增量步。然而，这种增量方法也带来了新的理论和数值挑战，例如如何客观地描述应力率以及如何高效地求解非线性方程组。

本文旨在系统地揭示更新拉格朗日列式法的完整图景。在接下来的章节中，我们将首先深入“原理与机制”部分，详细阐述其运动学基础、应力量度、虚功原理以及为保证客观性而必须采用的率形式本构关系，并介绍其在有限元法中的离散化与求解策略。随后，在“应用与交叉学科联系”一章，我们将展示该方法如何应用于解决弹塑性、结构屈曲、接触力学等前沿工程与科学问题。最后，通过“动手实践”部分提供的具体计算问题，读者将有机会亲手应用所学知识，巩固对核心概念的理解。

## 原理与机制

更新拉格朗日（Updated Lagrangian, UL）列式是求解有限变形问题的一种强大而直观的数值方法。其核心思想是将每个增量步开始时的构型作为计算该增量步的参考构型。这种方法将复杂的、高度非线性的总变形过程分解为一系列连续的、较小的增量变形。本章将系统地阐述更新拉格朗日列式的基本原理与关键机制，内容涵盖运动学描述、应力量度、虚功原理、本构关系以及最终的有限元离散化与求解算法。

### 更新拉格朗日列式的基本运动学

在有限变形理论中，精确描述物体的运动是首要任务。更新拉格朗日列式通过一种巧妙的方式来处理运动学，即不断“更新”参考构型。

我们考虑三个关键构型：
1.  **初始构型 $\Omega_0$**：物体在时间 $t=0$ 时的未变形状态，物质点的坐标用 $\boldsymbol{X}$ 表示。
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

在率形式的本构关系中，我们还需要描述变形的速率。**空间速度梯度** $\boldsymbol{l}$ 被定义为空间速度场 $\boldsymbol{v}$ 对当前空间坐标 $\boldsymbol{x}$ 的梯度，即 $\boldsymbol{l} = \nabla_{\boldsymbol{x}}\boldsymbol{v}$。它与总变形梯度的时间变化率 $\dot{\boldsymbol{F}}$ 之间存在一个基本关系：
$$
\boldsymbol{l} = \dot{\boldsymbol{F}}\boldsymbol{F}^{-1}
$$
在数值实现中，我们需要这个量的离散形式。在一个时间增量 $\Delta t = t_{n+1} - t_n$ 内，使用后向欧拉法对 $\dot{\boldsymbol{F}}_{n+1}$ 进行近似，可以得到 $\boldsymbol{l}_{n+1}$ 在更新拉格朗日框架下的近似表达式：
$$
\boldsymbol{l}_{n+1} \approx \frac{1}{\Delta t}(\boldsymbol{I} - \boldsymbol{f}_{n+1}^{-1})
$$
其中 $\boldsymbol{I}$ 是单位张量。这个表达式将连续介质力学中的速度梯度与数值计算中的增量变形梯度直接联系起来。

### 当前构型中的动力学与应力量度

更新拉格朗日列式的核心是在当前构型上建立平衡方程，因此，最自然的应力测度是定义在当前变形体上的**柯西（Cauchy）应力张量** $\boldsymbol{\sigma}$。柯西应力描述了当前构型中单位面积上所受的真实作用力。

然而，在有限变形理论中，为了建立与变形历史相关的本构关系，常常需要引入其他的应力测度。这些应力测度虽然不是直接出现在最终的平衡方程中，但它们在应力更新的计算过程中扮演着关键角色。常用的应力测度包括：

1.  **基尔霍夫（Kirchhoff）应力张量 $\boldsymbol{\tau}$**：它是柯西应力的体积加权形式，定义为 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$，其中 $J = \det(\boldsymbol{F})$ 是变形梯度的行列式，代表体积变化率。在处理近不可压缩材料时，基尔霍夫应力非常方便。

2.  **第二皮奥拉-基尔霍夫（Second Piola-Kirchhoff, 2nd PK）应力张量 $\boldsymbol{S}$**：这是一个定义在参考构型上的对称应力张量。它与柯西应力之间通过变形梯度进行“拉回”（pull-back）和“推前”（push-forward）操作来转换。

这些应力测度之间的转换关系可以通过力平衡和能量共轭原理导出。在一个从构型 $\Omega_n$ 到 $\Omega_{n+1}$ 的增量步中，描述该增量步的变形梯度为 $\boldsymbol{f}$，体积变化率为 $J_f = \det(\boldsymbol{f})$。在构型 $\Omega_{n+1}$ 中的柯西应力 $\boldsymbol{\sigma}_{n+1}$ 与相对于构型 $\Omega_n$ 定义的第二皮奥拉-基尔霍夫应力 $\boldsymbol{S}_{n+1}$ 之间通过“推前”（push-forward）操作相关联：
$$
\boldsymbol{\sigma}_{n+1} = J_f^{-1} \boldsymbol{f} \boldsymbol{S}_{n+1} \boldsymbol{f}^T
$$
这个关系是将定义在参考构型上的应力（$\boldsymbol{S}_{n+1}$）客观地转换为当前构型上的真实应力（$\boldsymbol{\sigma}_{n+1}$）的基本变换。在应力更新算法中，首先要计算出增量步的应力 $\boldsymbol{S}_{n+1}$，然后通过此公式将其转换为柯西应力，用于构建内力向量。

### 更新拉格朗日列式中的虚功原理

有限元法的基础是积分形式的平衡方程，即虚功原理。在更新拉格朗日列式中，虚功原理建立在**当前构型** $\Omega_t$ 之上。

我们从当前构型下的局部动量平衡方程（即平衡微分方程）出发，在忽略惯性效应的准静态情况下，该方程为：
$$
\nabla_{\boldsymbol{x}} \cdot \boldsymbol{\sigma} + \rho \boldsymbol{b} = \boldsymbol{0}
$$
其中 $\boldsymbol{\sigma}$ 是柯西应力，$\rho$ 是当前密度，$\boldsymbol{b}$ 是单位质量的体力。

通过将上式与一个任意的、满足位移边界条件的虚位移场 $\delta\boldsymbol{u}$ 做点积，并在当前体积 $\Omega_t$ 上积分，再利用高斯散度定理，我们可以得到虚功原理的表达式：
$$
\underbrace{\int_{\Omega_t} \boldsymbol{\sigma} : \nabla_{\boldsymbol{x}}\delta\boldsymbol{u} \, dv}_{\delta W_{int}} = \underbrace{\int_{\Omega_t} \rho \boldsymbol{b} \cdot \delta\boldsymbol{u} \, dv + \int_{\partial\Omega_t^t} \bar{\boldsymbol{t}} \cdot \delta\boldsymbol{u} \, da}_{\delta W_{ext}}
$$
该式表明，对于任意容许的虚位移，内力所做的虚功（$\delta W_{int}$）等于外力（体力 $\boldsymbol{b}$ 和在边界 $\partial\Omega_t^t$ 上的面力 $\bar{\boldsymbol{t}}$）所做的虚功（$\delta W_{ext}$）。

一个至关重要的问题是：内部虚功密度项 $\boldsymbol{\sigma} : \nabla_{\boldsymbol{x}}\delta\boldsymbol{u}$ 中的运动学量度 $\nabla_{\boldsymbol{x}}\delta\boldsymbol{u}$ 是否可以简化？答案是肯定的。根据角动量守恒原理，在没有体力偶的情况下，柯西应力张量 $\boldsymbol{\sigma}$ 必须是对称的。一个二阶张量（如 $\nabla_{\boldsymbol{x}}\delta\boldsymbol{u}$）可以分解为一个对称部分和一个反对称部分。一个对称张量与一个反对称张量的双点积恒为零。因此，只有 $\nabla_{\boldsymbol{x}}\delta\boldsymbol{u}$ 的对称部分才对内力虚功有贡献。这个对称部分被称为**虚变形率张量** $\delta\boldsymbol{d}$：
$$
\delta\boldsymbol{d} = \frac{1}{2}\left( \nabla_{\boldsymbol{x}}\delta\boldsymbol{u} + (\nabla_{\boldsymbol{x}}\delta\boldsymbol{u})^T \right)
$$
于是，内部虚功可以更精确地写为：
$$
\delta W_{int} = \int_{\Omega_t} \boldsymbol{\sigma} : \delta\boldsymbol{d} \, dv
$$
这种选择的物理意义在于，它确保了虚刚体运动（包括虚平移和虚转动）不会产生内部虚功。对于一个虚刚体转动，其位移梯度 $\nabla_{\boldsymbol{x}}\delta\boldsymbol{u}$ 是纯反对称的，因此其对称部分 $\delta\boldsymbol{d}$ 为零，从而 $\delta W_{int}=0$。这符合物理直觉：一个处于平衡状态的物体在经历刚体运动时不应产生或消耗内部能量。因此，柯西应力 $\boldsymbol{\sigma}$ 与虚变形率 $\delta\boldsymbol{d}$ 构成了在当前构型下的**功共轭对**。

### 本构模型：客观性的挑战

在更新拉格朗日列式中，由于参考构型不断更新，本构关系通常以率形式（rate form）给出，即建立应力率和应变率之间的关系。一个核心要求是，本构定律必须满足**物质坐标系无关性原理**，也称**客观性（objectivity）**。这意味着材料的响应不应依赖于观察者（或坐标系）的刚体运动。

如果我们天真地使用柯西应力的材料时间导数 $\dot{\boldsymbol{\sigma}}$ 作为应力率，将会导致严重问题。考虑一个仅经历刚体转动的物体。在这种情况下，物体没有发生任何实际的变形，因此变形率张量 $\boldsymbol{d} = \boldsymbol{0}$。一个简单的率形式本构律（如 $\dot{\boldsymbol{\sigma}} = \mathcal{C}[\boldsymbol{d}]$）会预测 $\dot{\boldsymbol{\sigma}} = \boldsymbol{0}$。这意味着在固定的空间坐标系中，应力张量保持不变。然而，从物理上看，正确的行为是应力张量应该随着物体一起转动。例如，如果初始应力为 $\boldsymbol{\sigma}(0)$，经过旋转 $\boldsymbol{R}(t)$ 后，正确的应力应为 $\boldsymbol{\sigma}_{exact}(t) = \boldsymbol{R}(t)\boldsymbol{\sigma}(0)\boldsymbol{R}^T(t)$。错误的预测 $\boldsymbol{\sigma}_{nonobj}(t) = \boldsymbol{\sigma}(0)$ 与正确值之间的误差会随着转动角度的增加而累积，产生完全不符合物理实际的“伪应力”。

为了解决这个问题，必须使用**客观应力率**。客观应力率测量的是在一个随体旋转的（即余旋的，corotational）坐标系下的应力变化率。一个通用的余旋应力率可以写成：
$$
\overset{\triangledown}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Omega}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Omega}
$$
其中 $\boldsymbol{\Omega}$ 是一个代表余旋坐标系自旋的反对称张量。对 $\boldsymbol{\Omega}$ 的不同选择导致了不同类型的客观应力率。两种最常见的选择是：

1.  **Jaumann 率**：选择连续体的自旋张量 $\boldsymbol{W}$ 作为余旋自旋，即 $\boldsymbol{\Omega} = \boldsymbol{W} = \frac{1}{2}(\boldsymbol{l} - \boldsymbol{l}^T)$。这是最简单、最常用的一种客观率。

2.  **Green-Naghdi 率**：选择与变形梯度极分解 $\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$ 中的旋转张量 $\boldsymbol{R}$ 相关联的自旋，即 $\boldsymbol{\Omega} = \dot{\boldsymbol{R}}\boldsymbol{R}^T$。

这两种率都是客观的，能正确处理刚体转动问题。然而，在包含大剪切变形的问题中，它们的表现有所不同。例如，在使用 Jaumann 率的各向同性弹塑性模型中，简单剪切问题可能会出现非物理的应力振荡现象。而 Green-Naghdi 率由于其自旋直接来自于材料本身的旋转，通常能更好地处理这类问题，提供更平滑、更符合物理直觉的应力响应。这表明，即使在满足客观性的前提下，选择合适的应力率对于获得精确的数值解仍然至关重要。

### 有限元离散与求解过程

将连续的虚功原理转化为可解的代数方程组，需要进行有限元离散。在更新拉格朗日列式中，所有离散化操作和积分都在当前构型上进行。

**等参元插值**

在等参单元中，单元的几何形状和单元内的位移场使用相同的形函数进行插值。这些形函数定义在一个简单的“父单元”上，其坐标为 $\boldsymbol{\xi}$。当前构型中任意一点的坐标 $\boldsymbol{x}$ 可以通过其节点坐标 $\boldsymbol{x}_a$ 和父单元形函数 $\widehat{N}_a(\boldsymbol{\xi})$ 来插值得到：
$$
\boldsymbol{x}(\boldsymbol{\xi}) = \sum_{a} \widehat{N}_a(\boldsymbol{\xi}) \boldsymbol{x}_a
$$
在计算虚功积[分时](@entry_id:274419)，我们需要形函数对空间坐标 $\boldsymbol{x}$ 的梯度 $\nabla_{\boldsymbol{x}}N_a$。这可以通过链式法则，利用从父单元到当前单元的雅可比矩阵 $\boldsymbol{J} = \partial\boldsymbol{x}/\partial\boldsymbol{\xi}$ 来计算：
$$
\nabla_{\boldsymbol{x}}N_a = \boldsymbol{J}^{-T} \nabla_{\boldsymbol{\xi}}\widehat{N}_a
$$
由于几何构型在每个迭代步中都会更新，雅可比矩阵 $\boldsymbol{J}$ 及其逆也需要相应地不断重新计算。

**Newton-Raphson 迭代求解**

将有限元插值代入虚功原理，我们得到一个关于节点位移增量 $\boldsymbol{d}$ 的非线性代数方程组：
$$
\boldsymbol{r}(\boldsymbol{d}) = \boldsymbol{f}_{int}(\boldsymbol{d}) - \boldsymbol{f}_{ext} = \boldsymbol{0}
$$
其中，$\boldsymbol{r}(\boldsymbol{d})$ 是**残差向量**，代表在当前试探构型下的不平衡力。$\boldsymbol{f}_{int}$ 是依赖于位移的内力向量，$\boldsymbol{f}_{ext}$ 是外力向量。

为了求解这个非线性方程组，标准方法是采用 **Newton-Raphson 迭代法**。在第 $k$ 次迭代中，我们对残差方程进行线性化，得到一个关于位移修正量 $\Delta\boldsymbol{d}^{(k)}$ 的线性方程组：
$$
\boldsymbol{K}_T^{(k)} \Delta\boldsymbol{d}^{(k)} = - \boldsymbol{r}^{(k)}
$$
求解后，更新位移和节点坐标：
$$
\boldsymbol{d}^{(k+1)} = \boldsymbol{d}^{(k)} + \Delta\boldsymbol{d}^{(k)} \quad \text{以及} \quad \boldsymbol{x}^{(k+1)} = \boldsymbol{x}^{(k)} + \Delta\boldsymbol{d}^{(k)}
$$
重复此过程直至残差 $\boldsymbol{r}$ 或位移修正量 $\Delta\boldsymbol{d}$ 小于某个预设的容差。

方程中的 $\boldsymbol{K}_T$ 是**一致切线刚度矩阵**，它是残差向量对节点位移的精确导数 $\boldsymbol{K}_T = \partial\boldsymbol{r}/\partial\boldsymbol{d}$。在有限变形问题中，它自然地分为两个部分：
1.  **材料刚度矩阵 $\boldsymbol{K}_{mat}$**：源于应力对应变的本构响应，它包含了材料的切线模量。
2.  **几何刚度矩阵 $\boldsymbol{K}_{geo}$**：也称为初应力矩阵，它源于在现有应力作用下，因几何构型变化而引起的平衡关系改变。它与当前的柯西应力 $\boldsymbol{\sigma}$ 成线性关系。

使用一致切线刚度矩阵至关重要。根据数值分析理论，只有当迭代矩阵是残差的精确导数时，Newton-Raphson 方法才能在解的邻域内实现**二次收敛**。这意味着每次迭代，解的有效数字位数大约会翻倍，从而极大地提高了计算效率。

如果使用一个近似的切线矩阵，例如忽略几何刚度部分，或者使用不更新的切线矩阵（修正 Newton 法），那么收敛速度将退化为线性或超线性。这通常会导致收敛需要更多的迭代次数，并且对载荷步长更加敏感，可能需要更小的载荷步才能保证收敛。对于超弹性材料，其一致切线刚度矩阵具有对称性，这一性质可以被线性方程求解器有效利用。而任意的割线近似（secant approximation）通常不具备这种对称性，可能会牺牲计算效率。因此，尽管计算一致切线刚度矩阵较为复杂，但它为求解非线性有限元问题提供了最快和最稳健的收敛性。