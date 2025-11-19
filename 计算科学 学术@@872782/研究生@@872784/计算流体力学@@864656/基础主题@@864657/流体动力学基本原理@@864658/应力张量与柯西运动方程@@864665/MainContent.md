## 引言
在连续介质力学中，精确描述物质内部相互作用力并将其与运动和变形联系起来，是理解和预测流体与固体行为的核心挑战。柯西应力张量与[柯西运动方程](@entry_id:204126)构成了解决这一挑战的理论基石，为从微观的流体剪切到宏观的[行星大气](@entry_id:148668)环流等广泛现象提供了统一的数学语言。然而，仅有[运动方程](@entry_id:170720)本身是不够的，它引入了未知的应力项，形成了一个不封闭的系统。这引出了一个关键问题：我们如何建立应力与物质变形速率之间的关系，从而使问题可解？

本文旨在系统性地解答这一问题。在“原理与机制”一章中，我们将从最基本的[接触力](@entry_id:165079)概念出发，推导出应力张量，并结合动量守恒建立[柯西运动方程](@entry_id:204126)，最终通过引入[本构关系](@entry_id:186508)（如牛顿流体模型）形成完整的理论框架。随后的“应用与[交叉](@entry_id:147634)学科联系”一章将展示这一理论框架在[计算流体力学](@entry_id:747620)、[地球物理学](@entry_id:147342)、天体物理学等前沿领域的强大应用能力。最后，在“动手实践”一章中，读者将通过具体问题加深对核心概念的理解。

现在，让我们从最基本的原理出发，深入探索连续介质内部力的世界。

## 原理与机制

在对连续介质（如流体和固体）的力学行为进行数学描述时，核心在于如何量化物质内部的相互作用力，并将这些力与物质的运动或变形联系起来。本章旨在系统性地阐述[应力张量](@entry_id:148973)的基本原理、其在[柯西运动方程](@entry_id:204126)中的核心作用，以及描述[应力与应变率](@entry_id:263123)之间关系的[本构模型](@entry_id:174726)。我们将从最基本的物理概念出发，逐步构建起一套完整而严谨的理论框架。

### 从接触力到[应力张量](@entry_id:148973)

想象一块连续的流体。如果我们用一个假想的平面将其一分为二，那么平面两侧的流体分子必然会相互作用。这些跨越假想平面的微观作用力，在宏观上表现为一种接触力。柯西应力理论为我们提供了一种精确描述这种[内力](@entry_id:167605)的方法。

#### 柯西应力原理与曳引矢量

考虑连续介质内部的任意一点 $\mathbf{x}$。我们可以想象一个通过此点的无限小[面积元](@entry_id:263205) $\Delta A$，其方向由[单位法向量](@entry_id:178851) $\mathbf{n}$ 定义。平面一侧的物质对另一侧施加的接触力为 $\Delta \mathbf{F}^{c}$。**曳引矢量**（traction vector）$\mathbf{t}(\mathbf{n}, \mathbf{x})$ 被定义为在该点处作用于法向为 $\mathbf{n}$ 的平面上的单位面积接触力。数学上，它是一个极限过程：

$$
\mathbf{t}(\mathbf{n}, \mathbf{x}) = \lim_{\Delta A \to 0} \frac{\Delta \mathbf{F}^{c}}{\Delta A}
$$

这个定义的成立依赖于几个关键的物理假设 [@problem_id:3382766]。首先是**连续介质假设**，它允许我们定义点函数（如密度、速度）并进行极限运算。其次是**[接触力](@entry_id:165079)的局部性原理**，即作用于 $\Delta A$ 上的力仅取决于其紧邻区域的物质，并且我们假设不存在集中作用于[面积元](@entry_id:263205)边界的“线力”或作用于面上的“力偶”。在这些假设下，总接触力 $\Delta \mathbf{F}^{c}$ 与面积 $\Delta A$ 成正比，从而保证上述极限存在，且极限值与面积元 $\Delta A$ 趋近于点 $\mathbf{x}$ 时的具体形状无关。因此，曳引矢量 $\mathbf{t}$ 仅仅是位置 $\mathbf{x}$ 和该处平面方向 $\mathbf{n}$ 的函数。

#### 柯西应力张量

曳引矢量 $\mathbf{t}$ 与[法向量](@entry_id:264185) $\mathbf{n}$ 之间存在着深刻的联系。法国数学家 Augustin-Louis Cauchy 证明了一个基本定理（**柯西定理**）：曳引矢量是[法向量](@entry_id:264185)的线性函数。这意味着存在一个[二阶张量](@entry_id:199780)，即**柯西应力张量** $\boldsymbol{\sigma}(\mathbf{x})$，使得对于任意方向 $\mathbf{n}$，都有：

$$
\mathbf{t}(\mathbf{n}, \mathbf{x}) = \boldsymbol{\sigma}(\mathbf{x}) \cdot \mathbf{n} \quad \text{或分量形式} \quad t_i = \sigma_{ji} n_j
$$

此处的分量形式采用了常见的物理学和工程学约定，其中 $\sigma_{ji}$ 是作用在 $j$ 坐标面上的力的第 $i$ 个分量。柯西应力张量 $\boldsymbol{\sigma}$ 完整地描述了连续介质内某一点的应力状态。一旦知道了 $\boldsymbol{\sigma}$，我们就可以计算出作用于通过该点的任何方向平面的曳[引力](@entry_id:175476)。张量的九个分量 $\sigma_{ij}$ 中，对角线分量 $\sigma_{ii}$（无求和）代表**[正应力](@entry_id:260622)**（normal stresses），而非对角线分量 $\sigma_{ij}$ ($i \neq j$) 代表**切应力**（shear stresses）。

#### 应力[张量的对称性](@entry_id:202126)

对于绝大多数在[计算流体力学](@entry_id:747620)（CFD）中遇到的流体，柯西[应力张量](@entry_id:148973)是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\top}$ 或 $\sigma_{ij} = \sigma_{ji}$。这个性质并非凭空假设，而是[角动量守恒](@entry_id:156798)定律的直接推论。对于一个没有内部力偶源（即非极性介质）的微元体，对其施加的力矩必须平衡，这直接导致了应力[张量的对称性](@entry_id:202126)。

然而，在一些更复杂的流体模型中，如**极性流体**（或称 Cosserat/micropolar 流体），物质微团除了平动外，还具有独立的[转动自由度](@entry_id:141502)（自旋角动量）。在这种情况下，[角动量守恒](@entry_id:156798)方程会包含一个额外的项——**[力偶应力](@entry_id:747952)张量** $\mathbf{m}$ 的散度。此时的[角动量守恒](@entry_id:156798)方程变为：

$$
\rho \frac{D h_i}{D t} = \varepsilon_{ijk} \sigma_{jk} + \partial_j m_{ij} + c_i
$$

其中 $h_i$ 是单位质量的自旋角动量，$\varepsilon_{ijk}$ 是 Levi-Civita 符号，$c_i$ 是[体力](@entry_id:174230)偶。在一个静态、无外力偶和体力偶的例子中，该方程简化为 $\varepsilon_{ijk} \sigma_{jk} + \partial_j m_{ij} = 0$。如果存在一个非零的[力偶应力](@entry_id:747952)场，其散度可以平衡由[非对称应力张量](@entry_id:184161)产生的力矩。例如，考虑一个非对称的应[力场](@entry_id:147325)，其唯一非零分量为 $\sigma_{12} = \tau$（常数），同时存在一个[力偶应力](@entry_id:747952)场，其唯一非零分量为 $m_{33} = -\tau x_3$。在这种情况下，[角动量守恒](@entry_id:156798)的第三个分量为 $\varepsilon_{3jk}\sigma_{jk} + \partial_j m_{3j} = (\sigma_{12} - \sigma_{21}) + \partial_3 m_{33} = (\tau - 0) - \tau = 0$。这个例子清晰地表明，只有当[力偶应力](@entry_id:747952)可以被忽略时（即在经典[连续介质力学](@entry_id:155125)中），我们才能理所当然地认为柯西应力张量是对称的 [@problem_id:3382724]。

### [柯西运动方程](@entry_id:204126)

将[应力张量](@entry_id:148973)的概念与牛顿第二定律相结合，我们便能推导出描述连续介质运动的基本方程。

#### 积分形式与[微分形式](@entry_id:146747)

考虑一个随流体运动的任意物质体积 $V$，其边界为 $S$。[牛顿第二定律](@entry_id:274217)指出，该物质体积内[总动量](@entry_id:173071)的物质导数等于作用在其上的所有外力之和。这些外力包括作用于整个体积的**[体力](@entry_id:174230)**（body forces，如重力），以及作用于其表面的**面力**（surface forces）。用积分形式表达为：

$$
\frac{D}{Dt} \int_V \rho \mathbf{v} \, dV = \oint_S \mathbf{t} \, dS + \int_V \rho \mathbf{b} \, dV
$$

其中 $\rho$ 是密度，$\mathbf{v}$ 是[速度场](@entry_id:271461)，$\mathbf{b}$ 是单位质量的体力。

利用柯西定理 $\mathbf{t} = \boldsymbol{\sigma} \cdot \mathbf{n}$，我们可以将面力积分写为 $\oint_S \boldsymbol{\sigma} \cdot \mathbf{n} \, dS$。接下来，一个关键的数学工具——**[高斯散度定理](@entry_id:188065)**的张量形式——允许我们将面积分转化为[体积分](@entry_id:171119) [@problem_id:2643427]。该定理指出，对于任意[二阶张量](@entry_id:199780)场 $\boldsymbol{T}$，有：

$$
\oint_S \boldsymbol{T} \cdot \mathbf{n} \, dS = \int_V (\nabla \cdot \boldsymbol{T}) \, dV
$$

此处的 $\nabla \cdot \boldsymbol{T}$ 是张量 $\boldsymbol{T}$ 的**散度**，其结果是一个矢量。物理上，如果 $\boldsymbol{T}$ 代表某个矢量值通量的密度，那么 $\boldsymbol{T} \cdot \mathbf{n}$ 就是通过法向为 $\mathbf{n}$ 的单位面积的[通量矢量](@entry_id:273577)。对于[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$，$\boldsymbol{\sigma} \cdot \mathbf{n}$ 正是曳引矢量 $\mathbf{t}$。

将散度定理应用于动量方程中的面力项，我们得到：

$$
\int_V \rho \frac{D\mathbf{v}}{Dt} \, dV = \int_V (\nabla \cdot \boldsymbol{\sigma}) \, dV + \int_V \rho \mathbf{b} \, dV
$$

由于这个积分关系对任意选取的物质体积 $V$ 都必须成立，因此被积函数在每一点上都必须相等。这便得到了**[柯西运动方程](@entry_id:204126)**的微分形式：

$$
\rho \frac{D\mathbf{v}}{Dt} = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b}
$$

这个方程是[流体力学](@entry_id:136788)和固体力学中最基本的方程之一，它将一个流体[质点](@entry_id:186768)的加速度（左侧）与作用在该[质点](@entry_id:186768)上的[内力](@entry_id:167605)（应力梯度的形式）和外力（[体力](@entry_id:174230)）联系起来。

#### 应用：从应[力场](@entry_id:147325)计算加速度

[柯西运动方程](@entry_id:204126)提供了一个直接的计算框架。如果我们知道某一点的应力张量场和[体力](@entry_id:174230)场，就可以确定该点的流体加速度 [@problem_id:1794869]。加速度 $\mathbf{a}$ (即[物质导数](@entry_id:172646) $D\mathbf{v}/Dt$) 可以表示为：

$$
\mathbf{a} = \frac{1}{\rho}(\nabla \cdot \boldsymbol{\sigma}) + \mathbf{b}
$$

在[笛卡尔坐标系](@entry_id:169789)中，应力张量散度的第 $i$ 个分量 $(\nabla \cdot \boldsymbol{\sigma})_i$ 计算为张量第 $i$ 列对各个坐标的[偏导数](@entry_id:146280)之和：

$$
(\nabla \cdot \boldsymbol{\sigma})_i = \frac{\partial \sigma_{xi}}{\partial x} + \frac{\partial \sigma_{yi}}{\partial y} + \frac{\partial \sigma_{zi}}{\partial z}
$$

例如，给定一个假设的应[力场](@entry_id:147325) $\sigma_{ij}(\mathbf{x})$ 和[体力](@entry_id:174230)场 $\mathbf{b}(\mathbf{x})$，通过计算各个应力分量对相应坐标的偏导数，我们就可以求出 $\nabla \cdot \boldsymbol{\sigma}$ 矢量的三个分量。然后，将其代入加速度表达式，即可在任意给定点算出流体的加[速度矢量](@entry_id:269648) $(a_x, a_y, a_z)$。这个过程是CFD数值求解器在每个时间步内所执行的核心计算之一。

### [本构关系](@entry_id:186508)：应力与变形的联系

[柯西运动方程](@entry_id:204126)本身并不封闭，因为它引入了未知的[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$。为了求解流体的运动，我们还需要一个额外的方程，即**[本构关系](@entry_id:186508)**（constitutive relation），它描述了材料的应力如何响应其运动或变形。

#### 本构关系的基本原则

对于流体，我们通常关心应力与速度梯度的关系。一个合理的本构关系必须遵循几个基本物理原则。

**物质标架无关性（客观性）**：[本构定律](@entry_id:178936)不应依赖于观察者的运动状态。一个正在做刚性转动的流体，其内部不应产生[粘性应力](@entry_id:261328)，因为流体微团之间没有相对变形。任何预测在刚性转动中会产生额外应力的本构模型都是非客观的，物理上是错误的 [@problem_id:3382763]。例如，一个[本构关系](@entry_id:186508)如果直接依赖于[速度矢量](@entry_id:269648) $\mathbf{v}$ 或[自旋张量](@entry_id:187346) $\mathbf{W} = \frac{1}{2}(\nabla\mathbf{v} - (\nabla\mathbf{v})^{\top})$，它就是非客观的。因为对于一个以[角速度](@entry_id:192539) $\boldsymbol{\Omega}$ 旋转的观察者而言，[流体速度](@entry_id:267320)和自旋都会改变，但这不应改变材料的内在应力状态。客观的本构关系必须由客观的张量（如应变率张量 $\mathbf{S}$）来构建。

**局部作用原理**：某一点的应力只取决于该点及其无限小邻域的[运动学](@entry_id:173318)状态，而与远处无关。

**各向同性**：流体的力学性质在所有方向上都是相同的。这意味着[本构关系](@entry_id:186508)中不应包含任何特定的方向矢量。

#### 可压缩牛顿流体

对于最常见的流体类型——**牛顿流体**，我们假设[应力与应变率](@entry_id:263123)之间存在线性关系。首先，我们将柯西[应力张量](@entry_id:148973)分解为两部分：

$$
\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\tau}
$$

这里，$-p\mathbf{I}$ 是各向同性的**[静水压力](@entry_id:275365)**部分，其中 $p$ 是[热力学](@entry_id:141121)压力，$\mathbf{I}$ 是单位张量。$\boldsymbol{\tau}$ 是**[粘性应力](@entry_id:261328)张量**，它代表了由流体内部速度梯度引起的附加应力，是流体“粘性”的宏观体现。

根据上述的客观性、各向同性和线性假设，可以证明，对于一个可压缩的牛顿流体，其[粘性应力](@entry_id:261328)张量 $\boldsymbol{\tau}$ 必须具有以下唯一形式 [@problem_id:3382753]：

$$
\boldsymbol{\tau} = 2\mu\mathbf{S} + \lambda(\nabla \cdot \mathbf{v})\mathbf{I}
$$

其中，$\mu$ 是**[剪切粘度](@entry_id:141046)**（或称[动力粘度](@entry_id:268228)），$\lambda$ 是**[第二粘度](@entry_id:189253)系数**。$\mathbf{S}$ 是**[应变率张量](@entry_id:266108)**，定义为[速度梯度](@entry_id:261686)的对称部分：

$$
\mathbf{S} = \frac{1}{2}\left(\nabla\mathbf{v} + (\nabla\mathbf{v})^{\top}\right)
$$

应变率张量 $\mathbf{S}$ 描述了流体微团的变形速率（拉伸和剪切），而速度的散度 $\nabla \cdot \mathbf{v}$ 则描述了微团体积的膨胀或收缩速率。这个本构关系完美地将应力与[流体运动学](@entry_id:202835)联系起来，构成了著名的**[Navier-Stokes方程组](@entry_id:142275)**的基础。

#### 不可压缩牛顿流体

在许多工程应用中，流体可以被视为**不可压缩的**，这意味着流体微团的体积在运动过程中保持不变。其数学表达为[速度场散度](@entry_id:178755)为零：

$$
\nabla \cdot \mathbf{v} = 0
$$

对于[不可压缩流](@entry_id:140301)，上述牛顿流体的本构关系得到极大简化。由于 $\nabla \cdot \mathbf{v} = 0$，包含[第二粘度](@entry_id:189253)系数 $\lambda$ 的项直接消失，[粘性应力](@entry_id:261328)张量变为 [@problem_id:3382745]：

$$
\boldsymbol{\tau} = 2\mu\mathbf{S}
$$

此时，完整的[应力张量](@entry_id:148973)为 $\boldsymbol{\sigma} = -p\mathbf{I} + 2\mu\mathbf{S}$。这里的压力 $p$ 的角色发生了微妙而深刻的变化。在不可压缩流中，密度 $\rho$ 是常数，压力 $p$ 不再能通过状态方程（如[理想气体定律](@entry_id:146757)）与密度和温度关联。它变成了一个纯粹的力学量，其作用是确保[流体运动](@entry_id:182721)始终满足 $\nabla \cdot \mathbf{v} = 0$ 这一运动学约束。从数学上看，$p$ 扮演了**拉格朗日乘子**的角色。在CFD[数值算法](@entry_id:752770)（如[投影法](@entry_id:144836)）中，通常通过求解一个**[压力泊松方程](@entry_id:137996)**（由[动量方程](@entry_id:197225)取散度得到）来确定压[力场](@entry_id:147325)，从而保证速度场的无散性。

### 能量、耗散与[热力学约束](@entry_id:755911)

[应力张量](@entry_id:148973)不仅在动量守恒中起作用，它还与[能量守恒](@entry_id:140514)紧密相关，特别是能量的耗散过程。

#### 动能方程与[应力功率](@entry_id:182907)

我们可以通过将[柯西运动方程](@entry_id:204126)与[速度矢量](@entry_id:269648) $\mathbf{v}$ 做[点积](@entry_id:149019)并对控制体积分，来推导**动能方程**的弱形式 [@problem_id:3382744]。经过一系列推导，可以得到总动能的变化率等于体力做的功率和应力做的功率之和。其中，应力做的总功率项 $\int_V \mathbf{v} \cdot (\nabla \cdot \boldsymbol{\sigma}) \, dV$ 可以通过散度定理和分部积分转化为：

$$
\mathcal{P}_{\sigma} = \oint_S (\boldsymbol{\sigma} \cdot \mathbf{n}) \cdot \mathbf{v} \, dS - \int_V \boldsymbol{\sigma} : \nabla\mathbf{v} \, dV
$$

第一项是边界上的曳[引力](@entry_id:175476)对速度做的功，即**曳引功率**。第二项是体积内的**[应力功率](@entry_id:182907)密度** $\boldsymbol{\sigma} : \nabla\mathbf{v}$ 的积分（注意负号）。将[应力分解](@entry_id:272862) $\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\tau}$ 代入，体积项可以进一步分解为：

$$
- \int_V (-p\mathbf{I} + \boldsymbol{\tau}) : \nabla\mathbf{v} \, dV = \int_V p(\nabla \cdot \mathbf{v}) \, dV - \int_V \boldsymbol{\tau} : \nabla\mathbf{v} \, dV
$$

第一部分 $\int_V p(\nabla \cdot \mathbf{v}) \, dV$ 代[表压力](@entry_id:147760)在流体膨胀或收缩时做的可逆功。第二部分 $- \int_V \boldsymbol{\tau} : \nabla\mathbf{v} \, dV$ 代表由[粘性应力](@entry_id:261328)引起的不可逆的能量转化。对于不可压缩流，$\nabla \cdot \mathbf{v} = 0$，压力功项消失，只剩下粘性项，它总是将宏观的动能转化为微观的内能（热），这个过程称为**[粘性耗散](@entry_id:143708)**。

#### 粘性耗散函数与第二定律

**[粘性耗散](@entry_id:143708)函数** $\Phi$ 定义为单位体积的粘性耗散率，即 $\Phi = \boldsymbol{\tau} : \nabla\mathbf{v}$。由于[粘性应力](@entry_id:261328)张量 $\boldsymbol{\tau}$ 是对称的，而速度梯度 $\nabla\mathbf{v}$ 的反对称部分（[自旋张量](@entry_id:187346)）与对称张量的缩并为零，因此 $\Phi = \boldsymbol{\tau} : \mathbf{S}$。

将可压缩牛顿流体的[本构关系](@entry_id:186508)代入，并引入[应变率张量](@entry_id:266108)的无迹部分 $\mathbf{S}' = \mathbf{S} - \frac{1}{3}(\nabla \cdot \mathbf{v})\mathbf{I}$，可以推导出耗散函数的一个非常富有洞察力的形式 [@problem_id:3382775]：

$$
\Phi = 2\mu(\mathbf{S}' : \mathbf{S}') + \kappa(\nabla \cdot \mathbf{v})^2
$$

其中 $\kappa = \lambda + \frac{2}{3}\mu$ 被称为**[体积粘度](@entry_id:187773)**（bulk viscosity）。第一项 $2\mu(\mathbf{S}' : \mathbf{S}')$ 代表由剪切和无体积变化的拉伸变形引起的耗散。第二项 $\kappa(\nabla \cdot \mathbf{v})^2$ 代表由[体积膨胀](@entry_id:144241)或收缩引起的耗散。

根据[热力学第二定律](@entry_id:142732)，任何自发的不[可逆过程](@entry_id:276625)都必须导致[熵增](@entry_id:138799)，对于流体流动，这意味着粘性耗散率必须是非负的，即 $\Phi \ge 0$。由于 $(\mathbf{S}' : \mathbf{S}')$ 和 $(\nabla \cdot \mathbf{v})^2$ 都是非负的，为了保证 $\Phi$ 对所有可能的流动都非负，材料系数必须满足：

$$
\mu \ge 0 \quad \text{和} \quad \kappa \ge 0
$$

这意味着[剪切粘度](@entry_id:141046)和[体积粘度](@entry_id:187773)都不能为负。在许多情况下，特别是对于单原子[理想气体](@entry_id:200096)，可以从[动力学理论](@entry_id:136901)推断 $\kappa = 0$，这被称为**[斯托克斯假设](@entry_id:195909)**。在此假设下，耗散函数简化为 $\Phi = 2\mu(\mathbf{S}' : \mathbf{S}')$，意味着纯粹的体积变化（如均匀膨胀）不产生[粘性耗散](@entry_id:143708)。

### [广义坐标](@entry_id:156576)系中的表述

在CFD中，为了处理复杂的几何形状，我们经常使用非笛卡尔的正交或非[正交曲线坐标](@entry_id:190233)系（如[柱坐标](@entry_id:271645)、[球坐标](@entry_id:146054)或任意[贴体坐标](@entry_id:746934)）。在这些[坐标系](@entry_id:156346)中，[基矢](@entry_id:199546)量本身是空间位置的函数，这给[微分](@entry_id:158718)运算带来了新的挑战。

#### [协变导数](@entry_id:152476)的必要性

在[曲线坐标系](@entry_id:172561)中，计算[张量的散度](@entry_id:191736) $\nabla \cdot \boldsymbol{\sigma}$ 时，我们不能再简单地对张量的分量求[偏导数](@entry_id:146280)。因为这样做忽略了[基矢](@entry_id:199546)量随空间位置变化所带来的影响。直接对分量求偏导数得到的量在[坐标变换](@entry_id:172727)下不具有矢量或张量的变换性质，因此它不是一个有物理意义的量 [@problem_id:3382759]。

为了在任意[坐标系](@entry_id:156346)下都能得到一个坐标无关的物理方程，我们必须使用**协变导数**（covariant derivative），记为 $\nabla_j$。[协变导数](@entry_id:152476)在普通偏导数的基础上，增加了额外的项（即**[克里斯托费尔符号](@entry_id:159831)** $\Gamma^i_{jk}$），这些项精确地计入了[基矢](@entry_id:199546)量的变化。

#### 应力张量散度的分量形式

使用协变导数，[应力张量](@entry_id:148973)散度的第 $i$ 个（逆变）分量可以正确地表示为：

$$
(\nabla \cdot \boldsymbol{\sigma})^i = \nabla_j \sigma^{ij} = \partial_j \sigma^{ij} + \Gamma^i_{kj} \sigma^{kj} + \Gamma^j_{kj} \sigma^{ik}
$$

这个表达式确保了 $\nabla \cdot \boldsymbol{\sigma}$ 的分量在不同[坐标系](@entry_id:156346)之间能够作为矢量的分量正确地变换，从而保证了[柯西运动方程](@entry_id:204126)的物理意义和[形式不变性](@entry_id:275482)。对于CFD实践而言，这意味着无论网格是笛卡尔的还是弯曲的，底层的物理方程都是一致的，只是其离散形式会因克里斯托费尔符号（或等价的几何项）的出现而变得更加复杂。