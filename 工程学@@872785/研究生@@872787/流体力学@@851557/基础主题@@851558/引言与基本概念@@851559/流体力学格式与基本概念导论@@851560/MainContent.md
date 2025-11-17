## 引言
[流体力学](@entry_id:136788)是研究流体（液体、气体及等离子体）在静止和运动状态下行为的科学，其原理无处不在，从我们呼吸的空气、流淌的血液，到飞机的升力、天气的变幻，乃至星系的演化。理解这些看似迥异的现象需要一个统一而严谨的理论框架。然而，流体运动的复杂性——尤其是[非线性](@entry_id:637147)效应和多尺度相互作用——构成了理解和预测其行为的主要挑战。本文旨在系统地解决这一问题，为读者构建一个从基本概念到高级应用的完整知识体系。

在接下来的内容中，我们将分三步深入探索[流体力学](@entry_id:136788)的世界。第一章**“原理与机制”**将奠定理论基石，从描述[流体运动](@entry_id:182721)的数学语言入手，推导质量、动量和能量的守恒方程，并介绍涡量、环量和量纲分析等核心概念。第二章**“应用与跨学科联系”**将展示这些基本原理的强大生命力，探讨它们如何应用于航空航天、地球物理、生物系统乃至宇宙学等前沿领域，揭示[流体力学](@entry_id:136788)的普适性。最后，在第三章**“动手实践”**中，我们将通过一系列精心设计的问题，将理论知识转化为解决实际问题的能力，巩固您对关键概念的理解。本篇导论将引导您踏上这段从理论到应用的智力旅程，最终掌握分析[复杂流体](@entry_id:198415)现象的核心工具。

## 原理与机制

在介绍性章节之后，我们现在深入探讨[流体力学](@entry_id:136788)的核心，即支配流体行为的基本原理和机制。本章的目标是系统地构建流体运动的数学框架，从运动学的描述开始，推导质量、动量和[能量守恒](@entry_id:140514)的控制方程，并介绍分析这些方程的关键工具。我们将从最基本的概念出发，逐步建立起一个完整且严谨的理论体系。

### [流体运动](@entry_id:182721)的描述方法

要从数学上描述流体的运动，我们必须首先确定一个参照系。在[流体力学](@entry_id:136788)中，存在两种主要且互补的观点：[拉格朗日描述](@entry_id:264498)和[欧拉描述](@entry_id:264722)。

#### [拉格朗日与欧拉描述](@entry_id:190556)

**[拉格朗日描述](@entry_id:264498) (Lagrangian description)** 遵循着个别流体质点的运动轨迹。在这种观点下，我们将每个流体[质点](@entry_id:186768)标记为其在初始时刻 $t=0$ 的位置 $\mathbf{X}_0$。该[质点](@entry_id:186768)在任意时刻 $t$ 的位置 $\mathbf{x}$ 便是其初始位置和时间的函数，即 $\mathbf{x} = \mathbf{X}(\mathbf{X}_0, t)$。因此，流体[质点](@entry_id:186768)的速度和加速度可以简单地通过对时间求导得到：
$$
\mathbf{v}(\mathbf{X}_0, t) = \frac{\partial \mathbf{X}(\mathbf{X}_0, t)}{\partial t}
$$
$$
\mathbf{a}(\mathbf{X}_0, t) = \frac{\partial^2 \mathbf{X}(\mathbf{X}_0, t)}{\partial t^2}
$$
这种方法直观，类似于经典力学中对[质点](@entry_id:186768)运动的追踪。然而，在大多数流体问题中，追踪天文数字般的流体质点是不现实的。

因此，**[欧拉描述](@entry_id:264722) (Eulerian description)** 更为常用。它关注空间中固定的点，并描述流体属性（如速度、压力、密度）如何随时间在这些点上变化。例如，[速度场](@entry_id:271461)被表示为 $\mathbf{u}(\mathbf{x}, t)$，它给出在空间位置 $\mathbf{x}$ 和时间 $t$ 的[流体速度](@entry_id:267320)。

这两种描述是等价的，并且可以相互转换。一个关键的联系是流体质点的加速度。在[欧拉框架](@entry_id:749109)下，一个流体[质点](@entry_id:186768)经历的加速度（即其拉格朗日加速度）并不仅仅是当地[速度场](@entry_id:271461)的时间偏导数 $\frac{\partial \mathbf{u}}{\partial t}$。这是因为质点在移动，它会进入速度不同的新区域。一个跟随[流体运动](@entry_id:182721)的观察者所测量的任何量 $f(\mathbf{x}, t)$ 的变化率，被称为**物质导数 (material derivative)** 或[随体导数](@entry_id:204621)，记为 $\frac{Df}{Dt}$。根据[链式法则](@entry_id:190743)，我们有：
$$
\frac{Df}{Dt} = \frac{\partial f}{\partial t} + (\mathbf{u} \cdot \nabla)f
$$
右边的第一项 $\frac{\partial f}{\partial t}$ 是**当地变化率 (local rate of change)**，表示在[固定点](@entry_id:156394)上 $f$ 的变化。第二项 $(\mathbf{u} \cdot \nabla)f$ 是**[对流](@entry_id:141806)变化率 (convective rate of change)**，表示由于质点移动到 $f$ 值不同的地方而引起的变化。

因此，在[欧拉框架](@entry_id:749109)下的[加速度场](@entry_id:266595) $\mathbf{a}(\mathbf{x}, t)$ 就是[速度场](@entry_id:271461)的物质导数：
$$
\mathbf{a}(\mathbf{x}, t) = \frac{D\mathbf{u}}{Dt} = \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla)\mathbf{u}
$$
这个[非线性](@entry_id:637147)项 $(\mathbf{u} \cdot \nabla)\mathbf{u}$ 是[流体力学](@entry_id:136788)中许多复杂现象（如[湍流](@entry_id:151300)）的根源。

为了阐明这两种描述之间的转换，考虑一个由拉格朗日映射给出的[二维流](@entry_id:266853) [@problem_id:546539]。假设一个[质点](@entry_id:186768)的初始位置为 $(X_0, Y_0)$，其在时间 $t$ 的位置 $(x, y)$ 为：
$$
x = X_0 e^{\alpha t} + Y_0 (1-e^{-\alpha t})
$$
$$
y = Y_0 e^{-\alpha t}
$$
其中 $\alpha$ 是一个常数。首先，我们计算拉格朗日速度和加速度：
$$
v_x = \frac{dx}{dt} = \alpha X_0 e^{\alpha t} + \alpha Y_0 e^{-\alpha t}, \quad v_y = \frac{dy}{dt} = -\alpha Y_0 e^{-\alpha t}
$$
$$
a_x = \frac{d^2x}{dt^2} = \alpha^2 X_0 e^{\alpha t} - \alpha^2 Y_0 e^{-\alpha t}, \quad a_y = \frac{d^2y}{dt^2} = \alpha^2 Y_0 e^{-\alpha t}
$$
为了得到欧拉[加速度场](@entry_id:266595) $\mathbf{a}(x, y, t)$，我们必须将 $X_0$ 和 $Y_0$ 用欧拉坐标 $(x, y)$ 和时间 $t$ 来表示。通过反解初始的映射关系，我们得到：
$$
Y_0 = y e^{\alpha t}
$$
$$
X_0 = x e^{-\alpha t} - y(1-e^{-\alpha t})
$$
将这两个表达式代入拉格朗日加速度分量中，我们最终得到完全用欧拉变量表示的[加速度场](@entry_id:266595)：
$$
\mathbf{a}(x,y,t) = \begin{pmatrix} \alpha^2 x - \alpha^2 y e^{\alpha t} \\ \alpha^2 y \end{pmatrix}
$$
这个例子清晰地展示了如何从一个基本的[拉格朗日描述](@entry_id:264498)推导出相应的欧拉场量。

#### 流线、[迹线](@entry_id:261720)与流体运动的可视化

为了理解复杂的流场结构，我们使用一些几何概念来对其进行可视化。

*   **[流线](@entry_id:266815) (Streamlines)** 是在某一特定时刻，与流场中各点速度矢量相切的曲线。如果用[弧长](@entry_id:191173) $s$ 来参数化流线 $\mathbf{x}_s(s)$，其定义方程为 $\frac{d\mathbf{x}_s}{ds} = C \mathbf{u}(\mathbf{x}_s, t)$，其中 $t$ 被视为一个固定的参数，C是常数。流线给我们一张流场在某个瞬间的“快照”。

*   **[迹线](@entry_id:261720) (Pathlines)** 是单个流体[质点](@entry_id:186768)随时间流逝所经过的真实轨迹。它是[拉格朗日观点](@entry_id:265471)的直接体现，其方程为 $\frac{d\mathbf{x}_p}{dt} = \mathbf{u}(\mathbf{x}_p, t)$。

*   **[脉线](@entry_id:263857) (Streaklines)** 是在某个[固定点](@entry_id:156394)连续释放的示踪粒子所形成的轨[迹线](@entry_id:261720)。它在实验中通常通过注入染料或烟雾来观察。

在**[定常流](@entry_id:191654) (steady flow)** 中，[速度场](@entry_id:271461)不随时间变化，即 $\frac{\partial \mathbf{u}}{\partial t} = \mathbf{0}$。在这种特殊情况下，流线、[迹线](@entry_id:261720)和[脉线](@entry_id:263857)是完全重合的。然而，在更普遍的**[非定常流](@entry_id:269993) (unsteady flow)** 中，这三者通常是不同的曲线。

一个有趣的问题是：在[非定常流](@entry_id:269993)中，是否存在某种条件能使[流线和迹线](@entry_id:182288)重合？[@problem_id:546447] 答案是肯定的。如果[迹线和流线](@entry_id:184041)在几何上是相同的曲线，那么沿着某条[迹线](@entry_id:261720) $\mathbf{x}_p(t)$，其[切线](@entry_id:268870)方向必须在任何时刻都与该点的[速度矢量](@entry_id:269648)方向相同。这意味着，对于[迹线](@entry_id:261720)上的任意一点 $\mathbf{x}$，其速度矢量 $\mathbf{u}(\mathbf{x}, t)$ 的方向不能随时间改变（其大小可以改变）。如果此条件对所有[迹线](@entry_id:261720)都成立，那么它必须[对流](@entry_id:141806)场中的所有点都成立。

一个矢量 $\mathbf{u}$ 的方向不随时间变化，等价于它和它的时间偏导数 $\frac{\partial \mathbf{u}}{\partial t}$ 始终平行。两个矢量平行的数学条件是它们的矢量积为零。因此，[流线和迹线](@entry_id:182288)重合的充要条件是：
$$
\mathbf{u} \times \frac{\partial \mathbf{u}}{\partial t} = \mathbf{0}
$$
这个条件在整个流场中都必须满足。它为我们提供了一个精确的判据，来判断一个[非定常流](@entry_id:269993)的几何结构是否随时间演化。

### 流场的[运动学](@entry_id:173318)分析

现在我们转向分析一个无限小的流体微团的局部运动。通过在微团中心附近对速度场进行[泰勒展开](@entry_id:145057)，我们可以将最一般的运动分解为平移、旋转和变形。

#### 速度梯度、[应变率](@entry_id:154778)与旋转

考虑一个位于 $\mathbf{x}$ 的流体微团中心，其附近一点 $\mathbf{x} + d\mathbf{r}$ 相对于中心的相对速度 $d\mathbf{u}$ 可以通过[泰勒级数展开](@entry_id:138468)到一阶：
$$
d\mathbf{u} = \mathbf{u}(\mathbf{x} + d\mathbf{r}) - \mathbf{u}(\mathbf{x}) \approx (\nabla \mathbf{u}) d\mathbf{r}
$$
其中 $\nabla \mathbf{u}$ 是**[速度梯度张量](@entry_id:270928) (velocity gradient tensor)**，其分量为 $G_{ij} = \frac{\partial u_i}{\partial x_j}$。这个二阶张量包含了关于流体微团局部运动的全部信息。

任何一个[二阶张量](@entry_id:199780)都可以唯一地分解为一个对称[部分和](@entry_id:162077)一个反对称部分。对于[速度梯度张量](@entry_id:270928)，我们有：
$$
G_{ij} = \frac{1}{2}\left(\frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i}\right) + \frac{1}{2}\left(\frac{\partial u_i}{\partial x_j} - \frac{\partial u_j}{\partial x_i}\right)
$$
我们将这两部分分别定义为**应变率张量 (rate-of-strain tensor)** $E_{ij}$ 和**[自旋张量](@entry_id:187346) (spin tensor)** $\Omega_{ij}$：
$$
E_{ij} = \frac{1}{2}\left(\frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i}\right)
$$
$$
\Omega_{ij} = \frac{1}{2}\left(\frac{\partial u_i}{\partial x_j} - \frac{\partial u_j}{\partial x_i}\right)
$$
应变率张量 $E_{ij}$ 描述了流体微团的形状变化（拉伸和剪切变形）。其对角线元素代表了沿坐标轴方向的线性应变率，而非对角线元素则代表了[剪切应变率](@entry_id:276945)。

[自旋张量](@entry_id:187346) $\Omega_{ij}$ 是一个[反对称张量](@entry_id:199349)，它描述了流体微团的刚性旋转。一个反对称的三维[二阶张量](@entry_id:199780)总可以与一个矢量（称为其[轴矢量](@entry_id:196296)）相关联。这种关联正是连接宏观流场属性与局部旋转的关键。

#### 涡量：[流体旋转](@entry_id:273789)的度量

流体的局部旋转可以通过一个更有物理直观的矢量来描述，即**涡量 (vorticity)**，定义为[速度场的旋度](@entry_id:183606)：
$$
\boldsymbol{\zeta} = \nabla \times \mathbf{u}
$$
[涡量](@entry_id:142747)是一个衡量流体微团旋转强度和方向的场。如果一个流场处处涡量为零 ($\boldsymbol{\zeta} = \mathbf{0}$)，则称之为**无[旋流](@entry_id:153202) (irrotational flow)**。

[涡量](@entry_id:142747)与[自旋张量](@entry_id:187346)之间存在着深刻的联系。流体微团的刚性旋转部分可以表示为角速度矢量 $\boldsymbol{\omega}$ 与相对位置矢量 $d\mathbf{r}$ 的叉积，即 $d\mathbf{u}_{\text{rot}} = \boldsymbol{\omega} \times d\mathbf{r}$。另一方面，这部分运动又是由[自旋张量](@entry_id:187346)决定的：$(d\mathbf{u}_{\text{rot}})_i = \Omega_{ij} dx_j$。通过比较这两种表达方式，我们可以推导出[角速度](@entry_id:192539) $\boldsymbol{\omega}$ 和[涡量](@entry_id:142747) $\boldsymbol{\zeta}$ 之间的关系 [@problem_id:546533]。

在分量形式中，$(\boldsymbol{\omega} \times d\mathbf{r})_i = \epsilon_{ijk} \omega_j dx_k$，其中 $\epsilon_{ijk}$ 是[列维-奇维塔符号](@entry_id:193594)。因此，我们有 $\Omega_{ik} = \epsilon_{ijk} \omega_j$。这个关系可以反转，得到 $\omega_p = \frac{1}{2} \epsilon_{pik} \Omega_{ik}$。同时，我们可以将涡量的分量用[自旋张量](@entry_id:187346)表示出来：
$$
\zeta_p = \epsilon_{pqr} \frac{\partial u_r}{\partial x_q} = \epsilon_{pqr} (E_{qr} + \Omega_{qr}) = \epsilon_{pqr} \Omega_{qr}
$$
（因为 $\epsilon_{pqr}$ 与[对称张量](@entry_id:148092) $E_{qr}$ 的缩并为零）。将 $\Omega_{qr}$ 的表达式代入，经过一些[张量代数](@entry_id:161671)运算，我们最终得到一个极为重要的结果：
$$
\boldsymbol{\omega} = \frac{1}{2} \boldsymbol{\zeta}
$$
这表明，流体微团的局部角速度恰好是其涡量的一半。这为[涡量](@entry_id:142747)这个数学定义提供了坚实的物理诠释。

此外，[自旋张量](@entry_id:187346)的分量也可以直接用局部角速度矢量 $\boldsymbol{\omega}$ 来表示 [@problem_id:546477]。可以证明：
$$
\Omega_{ij} = -\epsilon_{ijk}\omega_k
$$
这两种关系 [@problem_id:546533] [@problem_id:546477] 共同构成了[流体运动学](@entry_id:202835)中关于旋转的核心内容，它们将速度梯度[张量的反对称部分](@entry_id:193562)与[涡量](@entry_id:142747)这个矢量场紧密地联系在一起。

### 基本[守恒定律](@entry_id:269268)

[流体力学](@entry_id:136788)的基石是三大[守恒定律](@entry_id:269268)：[质量守恒](@entry_id:204015)、动量守恒和[能量守恒](@entry_id:140514)。这些定律的数学表达形式——即控制方程——构成了我们分析和预测流体行为的理论基础。为了从物理原理推导出适用于流体连续介质的[微分方程](@entry_id:264184)，我们需要一个强大的数学工具：[雷诺输运定理](@entry_id:191217)。

**[雷诺输运定理](@entry_id:191217) (Reynolds Transport Theorem, RTT)** 是连接[拉格朗日观点](@entry_id:265471)和[欧拉观点](@entry_id:198701)的桥梁。它描述了一个随流体运动的**物质体积 (material volume)** $V_m(t)$ 内某个物理量总和的时间变化率。对于一个单位体积的物理量 $\phi(\mathbf{x}, t)$，其在物质体积内的总和为 $\int_{V_m(t)} \phi \, dV$。RTT 表明：
$$
\frac{d}{dt} \int_{V_m(t)} \phi \, dV = \int_V \frac{\partial \phi}{\partial t} \, dV + \oint_S \phi (\mathbf{u} \cdot \mathbf{n}) \, dS
$$
这里，$V$ 是在某一瞬间与 $V_m(t)$ 重合的**[控制体积](@entry_id:143882) (control volume)**，$S$ 是其边界面，$\mathbf{n}$ 是指向外部的[单位法向量](@entry_id:178851)。该定理的右边两项分别表示控制体积内 $\phi$ 的当地增加率和通过边界净流出的通量。

#### [质量守恒](@entry_id:204015)：[连续性方程](@entry_id:195013)

质量守恒原理指出，一个物质体积（即总是由相同的流体质点构成）的总质量是恒定的。用数学语言表述就是：
$$
\frac{d}{dt} \int_{V_m(t)} \rho \, dV = 0
$$
其中 $\rho(\mathbf{x}, t)$ 是密度场。为了得到一个在流场中每一点都成立的局部[微分方程](@entry_id:264184)，我们将 RTT 应用于密度 $\rho$ (即令 $\phi = \rho$) [@problem_id:546562]。
$$
\frac{d}{dt} \int_{V_m(t)} \rho \, dV = \int_V \frac{\partial \rho}{\partial t} \, dV + \oint_S \rho (\mathbf{u} \cdot \mathbf{n}) \, dS = 0
$$
接下来，我们使用**散度定理 (Divergence Theorem)** 将表[面积分](@entry_id:275394)转换成[体积分](@entry_id:171119)。令矢量场 $\mathbf{F} = \rho\mathbf{u}$，[散度定理](@entry_id:143110)给出：
$$
\oint_S (\rho\mathbf{u} \cdot \mathbf{n}) \, dS = \int_V \nabla \cdot (\rho\mathbf{u}) \, dV
$$
将此结果代回，我们得到一个单一的体积积分：
$$
\int_V \left( \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho\mathbf{u}) \right) dV = 0
$$
由于这个关系对于任意选取的控制体积 $V$ 都必须成立，因此积分内的被积函数必须处处为零。这就得到了**连续性方程 (continuity equation)** 的[微分形式](@entry_id:146747)：
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho\mathbf{u}) = 0
$$
这个方程是对质量守恒定律的局部精确表述。对于**不可压缩流 (incompressible flow)**，流体[质点](@entry_id:186768)的密度不随运动而改变，即 $\frac{D\rho}{Dt} = 0$。在这种情况下，连续性方程简化为 $\nabla \cdot \mathbf{u} = 0$，表明[不可压缩流](@entry_id:140301)的速度场是无散的。

#### [动量守恒](@entry_id:149964)：柯西应力张量与[纳维-斯托克斯方程](@entry_id:142275)

[牛顿第二定律](@entry_id:274217)应用于流体连续介质，构成了[动量守恒](@entry_id:149964)原理。一个物质体积内[总动量](@entry_id:173071)的变化率等于作用在其上的合外力。这些力分为两类：作用于整个体积的**[体力](@entry_id:174230) (body forces)**（如重力），以及作用于其表面的**面力 (surface forces)**（如压力和[摩擦力](@entry_id:171772)）。

对于一个固定的控制体积 $V$，[动量守恒](@entry_id:149964)的积分形式为：
$$
\frac{d}{dt} \int_V \rho \mathbf{u} \, dV + \oint_S \rho \mathbf{u} (\mathbf{u} \cdot \mathbf{n}) \, dS = \int_V \rho \mathbf{g} \, dV + \oint_S \mathbf{T} \, dS
$$
左边是动量的当地变化率和[对流通量](@entry_id:158187)，右边是合外力。其中 $\mathbf{g}$ 是单位质量的[体力](@entry_id:174230)，$\mathbf{T}$ 是作用在表面 $S$ 上的**[面力矢量](@entry_id:189429) (traction vector)**。

[面力矢量](@entry_id:189429) $\mathbf{T}$ 的方向和大小不仅取决于位置，还取决于作用面的方向，该方向由[单位法向量](@entry_id:178851) $\mathbf{n}$ 给出。Augustin-Louis Cauchy 证明了 $\mathbf{T}$ 与 $\mathbf{n}$ 之间存在线性关系，这个关系通过一个[二阶张量](@entry_id:199780)来建立，即**柯西应力张量 (Cauchy stress tensor)** $\boldsymbol{\sigma}$：
$$
\mathbf{T} = \boldsymbol{\sigma} \cdot \mathbf{n} \quad \text{或} \quad T_i = \sigma_{ij} n_j
$$
应力张量 $\sigma_{ij}$ 的物理意义是：作用在以 $j$ 轴为法线的平面上、沿 $i$ 轴方向的单位面积力。

##### 柯西应力[张量的对称性](@entry_id:202126)

一个基本但并非显而易见的事实是，柯西[应力张量](@entry_id:148973)是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$ 或 $\sigma_{ij} = \sigma_{ji}$。这个性质并非来自定义，而是角动量守恒定律的一个深刻推论，前提是假设流体不承受内部的**体力矩 (body couples)** [@problem_id:546534]。

[角动量守恒](@entry_id:156798)的积分形式为：
$$
\frac{d}{dt} \int_V \rho (\mathbf{r} \times \mathbf{u}) \, dV = \int_V \rho (\mathbf{r} \times \mathbf{g}) \, dV + \int_S (\mathbf{r} \times \mathbf{T}) \, dS
$$
通过将 $\mathbf{T}$ 替换为 $\boldsymbol{\sigma} \cdot \mathbf{n}$，并利用[散度定理](@entry_id:143110)和[动量守恒](@entry_id:149964)方程，经过一系列推导，可以证明上述方程蕴含了一个纯粹由[应力张量](@entry_id:148973)构成的体积积分：
$$
\int_V \epsilon_{ijk} \sigma_{kj} \, dV = 0
$$
由于该积分对任意体积 $V$ 都为零，被积函数必须为零，即 $\epsilon_{ijk} \sigma_{kj} = 0$。这个表达式恰恰说明了 $\sigma_{kj} - \sigma_{jk} = 0$，即 $\sigma_{kj} = \sigma_{jk}$。因此，柯西应力张量是对称的。这个结果极大地简化了[流体动力学](@entry_id:136788)的理论，将一个一般[二阶张量](@entry_id:199780)的9个独立分量减少到了6个。

##### 本构关系：[牛顿流体](@entry_id:263796)

到目前为止，[动量方程](@entry_id:197225)中包含了6个未知的应力分量以及速度和压力，[方程组](@entry_id:193238)是不封闭的。为了封闭[方程组](@entry_id:193238)，我们需要一个**[本构关系](@entry_id:186508) (constitutive relation)**，它将[应力张量](@entry_id:148973)与流场的[运动学](@entry_id:173318)特性（即[速度梯度](@entry_id:261686)）联系起来。

对于最常见的一类流体——**[牛顿流体](@entry_id:263796) (Newtonian fluid)**——我们做出如下假设 [@problem_id:546491]：
1.  流体静止时，应力是各向同性的，即 $\boldsymbol{\sigma} = -p_0 \mathbf{I}$，其中 $p_0$ 是[静水压力](@entry_id:275365)。
2.  应力张量 $\boldsymbol{\sigma}$ 是[应变率张量](@entry_id:266108) $\mathbf{E}$ 的线性函数。
3.  流体是各向同性的，这意味着[应力与应变率](@entry_id:263123)之间的关系不依赖于[坐标系](@entry_id:156346)的方向。

基于这些假设，我们可以将总[应力张量](@entry_id:148973)分解为压力部分和由运动引起的**黏性应力张量 (viscous stress tensor)** $\boldsymbol{\tau}$：
$$
\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\tau}
$$
其中 $p$ 是[热力学](@entry_id:141121)压力。根据假设，$\boldsymbol{\tau}$ 必须是[应变率张量](@entry_id:266108) $\mathbf{E}$ 的一个线性[各向同性张量](@entry_id:195105)函数。对于一个对称[二阶张量](@entry_id:199780) $\mathbf{E}$，满足此条件的最一般的线性关系形式为：
$$
\boldsymbol{\tau} = \lambda_v (\text{tr}(\mathbf{E})) \mathbf{I} + 2\mu \mathbf{E}
$$
其中 $\mu$ 是**动力黏度 (dynamic viscosity)**，$\lambda_v$ 是**第二黏度系数 (second coefficient of viscosity)**。$\text{tr}(\mathbf{E}) = \nabla \cdot \mathbf{u}$，它代表了流体体积的膨胀率。对于不可压缩流，$\nabla \cdot \mathbf{u} = 0$，因此该项消失，[本构关系](@entry_id:186508)简化为 $\boldsymbol{\tau} = 2\mu \mathbf{E}$。

##### [纳维-斯托克斯方程](@entry_id:142275)

将本构关系 $\boldsymbol{\sigma} = -p\mathbf{I} + \lambda_v (\nabla \cdot \mathbf{u}) \mathbf{I} + 2\mu \mathbf{E}$ 代入[动量方程](@entry_id:197225)的微分形式 $\rho \frac{D\mathbf{u}}{Dt} = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{g}$，我们就得到了适用于可压缩牛顿流体的**纳维-斯托克斯方程 ([Navier-Stokes](@entry_id:276387) equations)**。对于具有恒定黏度 $\mu$ 和 $\lambda_v$ 的[不可压缩流](@entry_id:140301)，方程简化为更为人熟知的形式：
$$
\rho \left( \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla) \mathbf{u} \right) = -\nabla p + \mu \nabla^2 \mathbf{u} + \rho \mathbf{g}
$$
这个方程与连续性方程 $\nabla \cdot \mathbf{u} = 0$ 共同构成了描述不可压缩[牛顿流体](@entry_id:263796)运动的完整[方程组](@entry_id:193238)。它是现代[流体力学](@entry_id:136788)的基石。

### 关键定理与分析方法

掌握了控制方程之后，我们可以推导出一系列重要的定理，并发展出强大的分析技术来研究流体行为。

#### [环量守恒](@entry_id:189127)：开尔文定理

**环量 (circulation)** $\Gamma$ 定义为速度场沿一条闭合物质回路 $C$ 的线积分：
$$
\Gamma = \oint_C \mathbf{u} \cdot d\mathbf{l}
$$
环量与涡量密切相关，通过[斯托克斯定理](@entry_id:264534)可知，$\Gamma = \int_S (\nabla \times \mathbf{u}) \cdot d\mathbf{S} = \int_S \boldsymbol{\zeta} \cdot d\mathbf{S}$，即环量是穿过该回路的涡通量。

**[开尔文环量定理](@entry_id:139984) (Kelvin's Circulation Theorem)** 描述了环量随时间的演化。该定理指出，对于一个**无黏 (inviscid)**、**正压 (barotropic)**（密度仅是压力的函数，$\rho = \rho(p)$）的流体，在**保守[体力](@entry_id:174230) (conservative body force)**（如 $\mathbf{g} = -\nabla\Phi$）的作用下，随[流体运动](@entry_id:182721)的闭合回路上环量保持不变 [@problem_id:546450]。
$$
\frac{D\Gamma}{Dt} = 0
$$
其推导过程如下：
$$
\frac{D\Gamma}{Dt} = \oint_C \frac{D\mathbf{u}}{Dt} \cdot d\mathbf{l} = \oint_C \left(-\frac{1}{\rho} \nabla p + \mathbf{g}\right) \cdot d\mathbf{l}
$$
由于体力是保守的，$\oint_C \mathbf{g} \cdot d\mathbf{l} = -\oint_C \nabla\Phi \cdot d\mathbf{l} = 0$。对于正压流体，我们可以定义一个压强函数 $P(p) = \int \frac{dp'}{\rho(p')}$，使得 $\nabla P = \frac{1}{\rho}\nabla p$。因此，压力项的积分也为零：$\oint_C \frac{1}{\rho} \nabla p \cdot d\mathbf{l} = \oint_C \nabla P \cdot d\mathbf{l} = 0$。于是得到 $D\Gamma/Dt = 0$。

开尔文定理意味着在理想流体中，涡旋是“冻结”在流体中的，并随流体一起运动。它也解释了为什么在从静止状态开始的[理想流](@entry_id:261917)中，如果初始是无旋的，则将永远保持无旋。

#### 量纲分析与[动力相似](@entry_id:275631)性

[纳维-斯托克斯方程](@entry_id:142275)通常没有解析解，数值求解也代价高昂。**[量纲分析](@entry_id:140259) (dimensional analysis)** 是一种强大的工具，它通过将方程无量纲化来揭示问题中起主导作用的物理机制，并减少问题的参数数量。

考虑不可压缩的[纳维-斯托克斯方程](@entry_id:142275)。我们选取[特征长度](@entry_id:265857) $L$、特征速度 $U$、[特征时间](@entry_id:173472) $T$ 和特征压力 $P$ 来对变量进行无量纲化：
$$
\mathbf{x}^* = \frac{\mathbf{x}}{L}, \quad \mathbf{u}^* = \frac{\mathbf{u}}{U}, \quad t^* = \frac{t}{T}, \quad p^* = \frac{p}{P}
$$
将这些无量纲变量代入方程，并通过选择合适的特征尺度（例如，$T = L/U, P = \rho U^2$），我们可以将方程改写为无量纲形式。例如，对于包含重力 $\mathbf{g}$ 的流动，方程可以写成：
$$
\frac{\partial \mathbf{u}^*}{\partial t^*} + (\mathbf{u}^* \cdot \nabla^*) \mathbf{u}^* = -\nabla^* p^* + \frac{1}{Re} \nabla^{*2} \mathbf{u}^* + \frac{1}{Fr^2} \frac{\mathbf{g}}{g}
$$
这里出现了两个重要的[无量纲数](@entry_id:136814)：
*   **[雷诺数](@entry_id:136372) (Reynolds number)** $Re = \frac{\rho U L}{\mu} = \frac{U L}{\nu}$，表示[惯性力](@entry_id:169104)与黏性力的比值。
*   **弗劳德数 (Froude number)** $Fr = \frac{U}{\sqrt{g L}}$，表示惯性力与重力的比值。

这些无量纲数决定了流动的[动力相似](@entry_id:275631)性。如果两个几何相似的流动的雷诺数和弗劳德数都相同，那么它们的无量纲解也相同，这种流动被称为[动力相似](@entry_id:275631)的。这使得我们可以在模型（如[风洞](@entry_id:184996)中的飞机模型）上进行实验，并将其结果推广到真实尺寸的原型上。

[无量纲化](@entry_id:136704)的具体形式取决于所选择的特征尺度。例如，在一个特殊的瞬态问题中，如果特征时间尺度被选为黏性扩散时间 $T_v = L^2/\nu$ 和[重力波](@entry_id:185196)传播时间 $T_g = \sqrt{L/g}$ 的几何平均值 $T_c = \sqrt{T_v T_g}$，那么无量纲化的纳维-斯托克斯方程中，当地加速度项的系数将呈现出一种特殊的形式 [@problem_id:546498]。经过推导，该系数 $\alpha$ 可以表示为：
$$
\alpha = \frac{L}{U T_c} = \frac{1}{\sqrt{Re \cdot Fr}}
$$
这个例子说明了通过选择不同的特征尺度，可以凸显流动中不同物理过程之间的相互作用。

#### [湍流](@entry_id:151300)简介：[雷诺平均](@entry_id:754341)与雷诺应力

大多数工程和自然界中的流动都是**[湍流](@entry_id:151300) (turbulent)**，其特点是速度和压[力场](@entry_id:147325)在时间和空间上呈现出不规则、混沌的脉动。[直接数值模拟](@entry_id:149543)（DNS）[湍流](@entry_id:151300)需要极大的计算资源，因为它必须解析所有尺度的脉动。

为了使[湍流](@entry_id:151300)问题在工程上易于处理，Osborne Reynolds 提出了一种统计方法，即**[雷诺平均](@entry_id:754341) (Reynolds averaging)**。该方法将瞬时量（如速度 $u_i$）分解为一个时间平均值（或系综平均值）$\overline{u_i}$ 和一个脉动量 $u_i'$：
$$
u_i(\mathbf{x}, t) = \overline{u_i}(\mathbf{x}) + u_i'(\mathbf{x}, t)
$$
根据定义，脉动量的平均值为零，即 $\overline{u_i'} = 0$。

将这种分解代入不[可压缩纳维-斯托克斯](@entry_id:747591)方程，并对整个方程进行时间平均，我们会得到一个描述平均流场演化的方程，即**[雷诺平均纳维-斯托克斯方程](@entry_id:173045) (Reynolds-Averaged Navier-Stokes, RANS)** [@problem_id:546516]。在对[非线性](@entry_id:637147)的[对流](@entry_id:141806)项 $\rho u_j \frac{\partial u_i}{\partial x_j}$ 进行平均时，会出现一个额外的项：
$$
\rho \overline{u_j' \frac{\partial u_i'}{\partial x_j}} = \rho \frac{\partial}{\partial x_j}(\overline{u_i' u_j'})
$$
（利用了脉动量的[连续性方程](@entry_id:195013) $\partial u_j' / \partial x_j = 0$）。将这一项移到方程的右边，RANS 方程可以写成：
$$
\rho \overline{u_j} \frac{\partial \overline{u_i}}{\partial x_j} = -\frac{\partial \overline{p}}{\partial x_i} + \frac{\partial}{\partial x_j} \left( \mu \frac{\partial \overline{u_i}}{\partial x_j} - \rho \overline{u_i' u_j'} \right)
$$
与原始的[纳维-斯托克斯方程](@entry_id:142275)相比，RANS 方程中出现了一个新的项，$\tau'_{ij} = -\rho \overline{u_i' u_j'}$。这个张量被称为**[雷诺应力张量](@entry_id:270803) (Reynolds stress tensor)**。

雷诺应力代表了[湍流](@entry_id:151300)脉动对平均流动输运的动量。它不是一个真正的应力，而是一个数学上的产物，源于对[非线性](@entry_id:637147)[对流](@entry_id:141806)项的平均。然而，从对平均流的影响来看，它的作用类似于一个额外的应力。[雷诺应力](@entry_id:263788)的出现引入了新的未知量（$\overline{u_i' u_j'}$ 的6个独立分量），使得 RANS [方程组](@entry_id:193238)本身不封闭。如何用已知的平均流场量来模化雷诺应力，这就是所谓的**[湍流封闭问题](@entry_id:268973) (turbulence closure problem)**，也是[湍流](@entry_id:151300)研究的核心挑战之一。