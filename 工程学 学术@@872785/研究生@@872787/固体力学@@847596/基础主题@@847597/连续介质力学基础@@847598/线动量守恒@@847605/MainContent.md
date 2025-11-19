## 引言
线[动量平衡原理](@entry_id:196256)是连续介质力学的基石，它将牛顿第二定律从离散[质点](@entry_id:186768)推广到可变形的固体和流体，建立了外部载荷、[内力](@entry_id:167605)[分布](@entry_id:182848)与物体运动之间的基本关系。然而，如何精确描述连续体内部无处不在的[内力](@entry_id:167605)，并将其与宏观运动联系起来，构成了从[质点力学](@entry_id:170420)到[连续介质力学](@entry_id:155125)的关键知识鸿沟。本文旨在系统地跨越这一鸿沟，为读者构建一个关于[线动量](@entry_id:174467)平衡的完整理论与应用图景。

在“原理与机制”一章中，我们将从第一性原理出发，推导[线动量](@entry_id:174467)平衡的积分与微分形式，并引入核心概念——柯西应力张量，同时将其推广至[大变形](@entry_id:167243)框架。随后，“应用与[交叉](@entry_id:147634)学科联系”一章将展示该原理如何在[结构工程](@entry_id:152273)、地球物理学、[材料科学](@entry_id:152226)等多个领域中，被用于解决从静态平衡到动态波传播的各类实际问题。最后，“动手实践”部分将通过一系列精心设计的问题，帮助读者巩固理论知识并提升解决实际问题的能力。

现在，让我们深入探讨[线动量](@entry_id:174467)平衡的基本原理与核心机制。

## 原理与机制

在上一章引言的基础上，本章将深入探讨[线动量](@entry_id:174467)平衡的基本原理与核心机制。我们将从适用于连续介质的牛顿第二定律的积分形式出发，逐步推导出其局部[微分形式](@entry_id:146747)，并在此过程中引入[应力张量](@entry_id:148973)的关键概念。本章旨在为读者建立一个关于连续体力内部力如何传递以及如何与运动和外部载荷相互作用的严谨理论框架。

### 动量与力：[连续介质力学](@entry_id:155125)的基本公设

经典力学的基石是[牛顿第二定律](@entry_id:274217)，它指出一个质点系的动量变化率等于作用在该质点系上的合外力。为了将这一离散质点系统的定律推广到连续介质，我们考虑一个由一组固定物质点构成的**物质体**（material body）。在时刻 $t$，该物质体占据空间中的区域 $B(t)$。

物质体的[总线动量](@entry_id:173071) $\mathbf{P}(t)$ 是其内部所有微元动量的积分。对于一个体积为 $dV$、质量密度为 $\rho(\mathbf{x}, t)$ 的微元，其动量为 $\rho(\mathbf{x}, t)\mathbf{v}(\mathbf{x}, t)dV$，其中 $\mathbf{v}(\mathbf{x}, t)$ 是该微元在空间点 $\mathbf{x}$ 的速度。因此，总线动量为：
$$
\mathbf{P}(t) = \int_{B(t)} \rho(\mathbf{x}, t) \mathbf{v}(\mathbf{x}, t) \,dV
$$

作用在物质体上的外力分为两类：**[体力](@entry_id:174230)**（body forces）和**面力**（surface forces）。[体力](@entry_id:174230)是远程作用力，作用于物质体的整个体积，例如重力或电磁力。我们用 $\mathbf{b}(\mathbf{x}, t)$ 表示单位质量的[体力](@entry_id:174230)。因此，作用在体积微元 $dV$ 上的[体力](@entry_id:174230)为 $\rho\mathbf{b}dV$，总体力为 $\int_{B(t)} \rho\mathbf{b} \,dV$。面力是近程接触力，通过物质体的边界 $\partial B(t)$ 传递。

为了描述面力的局部强度，我们引入**[面力矢量](@entry_id:189429)**（traction vector） $\mathbf{t}$ 的概念。考虑边界 $\partial B(t)$ 上的一点 $\mathbf{x}$，以及包含该点的一个微小面元 $\Delta S$，其面积为 $\Delta A$，单位外法向矢量为 $\mathbf{n}$。设作用在该面元上的合接触力为 $\Delta\mathbf{F}_c$。[面力矢量](@entry_id:189429) $\mathbf{t}$ 在点 $\mathbf{x}$ 处被定义为当面元收缩至该点时，单位面积上的[接触力](@entry_id:165079)极限 [@problem_id:2616721]：
$$
\mathbf{t}(\mathbf{x}, \mathbf{n}, t) = \lim_{\Delta A \to 0^+} \frac{\Delta\mathbf{F}_c}{\Delta A}
$$
此定义强调面力不仅取决于位置 $\mathbf{x}$ 和时间 $t$，还至关重要地取决于表面的**朝向**，由单位法向矢量 $\mathbf{n}$ 描述。总面力即为[面力矢量](@entry_id:189429)在整个边界上的积分 $\int_{\partial B(t)} \mathbf{t} \,dA$。

综合以上定义，牛顿第二定律应用于物质体 $B(t)$，即“[总线动量](@entry_id:173071)的[物质时间导数](@entry_id:190892)等于总外力”，可以写成如下的**[线动量](@entry_id:174467)平衡积分形式**，也称为 Cauchy 第一运动定律 [@problem_id:2616735]：
$$
\frac{d}{dt} \int_{B(t)} \rho\mathbf{v} \,dV = \int_{B(t)} \rho\mathbf{b} \,dV + \int_{\partial B(t)} \mathbf{t} \,dA
$$
这里的导数 $\frac{d}{dt}$ 是**[物质时间导数](@entry_id:190892)**，因为它跟随着一个固定的物质集合。

在许多工程应用中，我们更关心空间中一个固定的或以特定速度移动的区域，即**控制体**（control volume） $V(t)$，而不是跟随物质流动的物质体。物质会流进或流出[控制体](@entry_id:143882)边界。此时，动量[平衡方程](@entry_id:172166)需要一个额外的项来描述随物质流动而穿越边界的动量。利用**[雷诺输运定理](@entry_id:191217)**（Reynolds Transport Theorem），我们可以将[物质导数](@entry_id:172646)与控制体内的变化及跨边界的通量联系起来。对于一个以速度 $\mathbf{w}(\mathbf{x}, t)$ 移动的[控制体](@entry_id:143882) $V(t)$，其[线动量](@entry_id:174467)[平衡方程](@entry_id:172166)为 [@problem_id:2616750]：
$$
\frac{d}{dt} \int_{V(t)} \rho\mathbf{v} \,dV + \int_{\partial V(t)} \rho\mathbf{v} [(\mathbf{v} - \mathbf{w}) \cdot \mathbf{n}] \,dA = \int_{V(t)} \rho\mathbf{b} \,dV + \int_{\partial V(t)} \mathbf{t} \,dA
$$
与物质体方程相比，这里多出的一项是**动量通量**（momentum flux）项。其中 $(\mathbf{v} - \mathbf{w}) \cdot \mathbf{n}$ 表示物质相对于[控制体](@entry_id:143882)边界的法向流出速度。该项物理意义为单位时间内通过[控制体](@entry_id:143882)边界净流出的[线动量](@entry_id:174467)。左边第一项则表示[控制体](@entry_id:143882)内[总线动量](@entry_id:173071)的**累积变化率**。

### 应力的概念：从面力到应力张量

我们已经看到，[面力矢量](@entry_id:189429) $\mathbf{t}$ 依赖于其作用面的法向 $\mathbf{n}$。一个自然而深刻的问题是：它们之间是何种关系？答案蕴含在 Cauchy 的一个巧妙的思维实验中，即**柯西四面体论证**（Cauchy tetrahedron argument）。

考虑连续体内部的任意一点 $\mathbf{x}_0$，我们以此点为顶点构造一个极小的四面体。其三个正交面分别垂直于笛卡尔坐标系的[基矢](@entry_id:199546)量 $\mathbf{e}_1, \mathbf{e}_2, \mathbf{e}_3$，第四个斜面的单位外法向为 $\mathbf{n}$。设该四面体的特征尺寸为 $\ell$。那么，其各个面的面积 $A$ 正比于 $\ell^2$，而其体积 $V$ 则正比于 $\ell^3$。

我们将[线动量](@entry_id:174467)平衡的积分形式应用于这个小四面体。方程中的各项随 $\ell$ 的变化尺度不同 [@problem_id:2616731]：
- **面力项**：作用在每个面上的力是[面力矢量](@entry_id:189429)与面积的乘积，因此总面力与 $A$ 成正比，即 $O(\ell^2)$。
- **体力项和惯性项**：这两项都是对体积的积分，被积函数（如 $\rho\mathbf{b}$ 和 $\rho\mathbf{a}$）在点 $\mathbf{x}_0$ 附近是有界的。因此，这两项都与 $V$ 成正比，即 $O(\ell^3)$。

将整个动量[平衡方程](@entry_id:172166)除以斜面面积 $A_{\mathbf{n}}$，然后取极限 $\ell \to 0$。[体力](@entry_id:174230)项和惯性项的形式为 $\frac{O(\ell^3)}{O(\ell^2)} = O(\ell)$，因此在极限中会消失。最终只剩下纯粹的[表面力](@entry_id:188034)平衡关系。经过推导，我们得到一个只涉及[面力矢量](@entry_id:189429)的核心关系，即**柯西引理**（Cauchy's Lemma）：
$$
\mathbf{t}(\mathbf{n}) = n_1 \mathbf{t}(\mathbf{e}_1) + n_2 \mathbf{t}(\mathbf{e}_2) + n_3 \mathbf{t}(\mathbf{e}_3) = \sum_{i=1}^3 n_i \mathbf{t}(\mathbf{e}_i)
$$
其中 $n_i = \mathbf{n} \cdot \mathbf{e}_i$ 是 $\mathbf{n}$ 在 $\mathbf{e}_i$ 方向的分量（[方向余弦](@entry_id:170591)）。这个惊人的结果表明，任意方向上的[面力矢量](@entry_id:189429)都可以表示为三个[正交坐标](@entry_id:166074)面上[面力矢量](@entry_id:189429)的[线性组合](@entry_id:154743)。

这种线性关系的存在意味着，我们可以定义一个二阶张量，即**柯西应力张量**（Cauchy stress tensor） $\boldsymbol{\sigma}$，它将法向矢量 $\mathbf{n}$ [线性映射](@entry_id:185132)到[面力矢量](@entry_id:189429) $\mathbf{t}$ [@problem_id:2616731]：
$$
\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}
$$
在笛卡尔坐标系中，上述关系可以写为分量形式 $t_i = \sigma_{ij}n_j$（此处及后续均使用爱因斯坦求和约定）。将柯西引理与该定义式对比，我们可以清晰地看到应力张量矩阵的物理意义：矩阵的第 $j$ 列就是作用在法向为 $\mathbf{e}_j$ 的坐标面上的[面力矢量](@entry_id:189429) $\mathbf{t}(\mathbf{e}_j)$ [@problem_id:2616722]。即：
$$
\boldsymbol{\sigma} = \begin{bmatrix} |  |  | \\ \mathbf{t}(\mathbf{e}_1)  \mathbf{t}(\mathbf{e}_2)  \mathbf{t}(\mathbf{e}_3) \\ |  |  | \end{bmatrix}
$$
其中，分量 $\sigma_{ij}$ 代表作用在法向为 $\mathbf{e}_j$ 的平面上、沿 $\mathbf{e}_i$ 方向的力分量。

例如，假设在某点测得作用于三个坐标面上的[面力矢量](@entry_id:189429)（单位为 MPa）分别为 $\mathbf{t}(\mathbf{e}_1) = \begin{pmatrix} 2  -1  4 \end{pmatrix}^T$, $\mathbf{t}(\mathbf{e}_2) = \begin{pmatrix} 0  3  1 \end{pmatrix}^T$, $\mathbf{t}(\mathbf{e}_3) = \begin{pmatrix} -2  5  0 \end{pmatrix}^T$。那么该点的柯西[应力张量](@entry_id:148973)为 [@problem_id:2616722]：
$$
\boldsymbol{\sigma} = \begin{pmatrix} 2  0  -2 \\ -1  3  5 \\ 4  1  0 \end{pmatrix} \, \mathrm{MPa}
$$
一旦知道了[应力张量](@entry_id:148973)，我们就可以计算任何其他方向上的面力。例如，对于法向为 $\mathbf{n} = \frac{1}{\sqrt{14}}\begin{pmatrix} 3  -1  2 \end{pmatrix}^T$ 的平面，其上的[面力矢量](@entry_id:189429)为：
$$
\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma}\mathbf{n} = \frac{1}{\sqrt{14}} \begin{pmatrix} 2  0  -2 \\ -1  3  5 \\ 4  1  0 \end{pmatrix} \begin{pmatrix} 3 \\ -1 \\ 2 \end{pmatrix} = \frac{1}{\sqrt{14}} \begin{pmatrix} 2 \\ 4 \\ 11 \end{pmatrix} \, \mathrm{MPa}
$$

### 动量平衡的局部形式

[线动量](@entry_id:174467)平衡的积分形式描述了有限体积内的宏观行为。为了研究物质内部每一点的力学状态，我们需要一个**局部**（或[微分](@entry_id:158718)）形式的平衡方程。这可以通过将积分形式应用于一个无限小的体积并利用数学定理来实现。

我们从物质体的积分[平衡方程](@entry_id:172166)出发：
$$
\int_{B(t)} \rho\mathbf{a} \,dV = \int_{B(t)} \rho\mathbf{b} \,dV + \int_{\partial B(t)} \mathbf{t} \,dA
$$
这里，我们已经使用[雷诺输运定理](@entry_id:191217)将左侧的动量变化率写成了加速度 $\mathbf{a}$ 的积分。接着，我们将[面力矢量](@entry_id:189429)替换为应力张量的作用，$\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$，得到面力积分为 $\int_{\partial B(t)} \boldsymbol{\sigma}\mathbf{n} \,dA$。

关键的一步是使用**[高斯散度定理](@entry_id:188065)**（Gauss's Divergence Theorem），它将一个矢量场（在这里是张量 $\boldsymbol{\sigma}$ 的每一行）在闭合[曲面](@entry_id:267450)上的积分与其在体积内的散度积分联系起来。应用于应力张量，该定理给出：
$$
\int_{\partial B(t)} \boldsymbol{\sigma}\mathbf{n} \,dA = \int_{B(t)} (\nabla \cdot \boldsymbol{\sigma}) \,dV
$$
其中 $\nabla \cdot \boldsymbol{\sigma}$ 是**应力[张量的散度](@entry_id:191736)**。这是一个矢量，其第 $i$ 个分量为 $(\nabla \cdot \boldsymbol{\sigma})_i = \frac{\partial \sigma_{ij}}{\partial x_j}$。现在，动量[平衡方程](@entry_id:172166)中的所有项都变成了[体积分](@entry_id:171119)：
$$
\int_{B(t)} \rho\mathbf{a} \,dV = \int_{B(t)} \rho\mathbf{b} \,dV + \int_{B(t)} (\nabla \cdot \boldsymbol{\sigma}) \,dV
$$
将所有项移到一边：
$$
\int_{B(t)} ( \nabla \cdot \boldsymbol{\sigma} + \rho\mathbf{b} - \rho\mathbf{a} ) \,dV = \mathbf{0}
$$
由于这个方程必须对**任意**物质体 $B(t)$ 都成立，这意味着被积函数本身必须处处为零（这被称为**局部化论证**）。因此，我们得到了[线动量](@entry_id:174467)平衡的局部微分形式，即 Cauchy 第一运动定律的微分形式：
$$
\nabla \cdot \boldsymbol{\sigma} + \rho\mathbf{b} = \rho\mathbf{a}
$$
这个矢量方程代表了连续介质中每一点的力平衡。它表明，由应力不[均匀性](@entry_id:152612)产生的内部合力密度（$\nabla \cdot \boldsymbol{\sigma}$）与单位体积的体力（$\rho\mathbf{b}$）之和，等于单位体积的[惯性力](@entry_id:169104)（$\rho\mathbf{a}$）[@problem_id:2616742]。

在处理张量运算时，采用**指标符号**（index notation）通常更为便捷。使用逗号表示对空间坐标的[偏导数](@entry_id:146280)，例如 $f_{,j} \equiv \frac{\partial f}{\partial x_j}$，上述平衡方程的第 $i$ 个分量可以写为 [@problem_id:2616702]：
$$
\sigma_{ij,j} + \rho b_i = \rho \dot{v}_i
$$
其中 $\dot{v}_i$ 是速度分量 $v_i$ 的物质导数，即加速度分量 $a_i$。

### 应力[张量的对称性](@entry_id:202126)：[角动量平衡](@entry_id:181848)

除了[线动量](@entry_id:174467)，我们还必须考虑角动量的平衡，这引出了关于柯西[应力张量](@entry_id:148973)的一个至关重要的性质。**角[动量平衡原理](@entry_id:196256)**指出，对于任何物质体，其角动量的[物质时间导数](@entry_id:190892)等于作用在其上的所有外力矩之和（假设不存在[体力](@entry_id:174230)矩或面力偶）。

对于物质体 $B(t)$，绕固定原点的[角动量平衡](@entry_id:181848)[积分方程](@entry_id:138643)为：
$$
\frac{d}{dt} \int_{B(t)} \mathbf{x} \times (\rho\mathbf{v}) \,dV = \int_{B(t)} \mathbf{x} \times (\rho\mathbf{b}) \,dV + \int_{\partial B(t)} \mathbf{x} \times \mathbf{t} \,dA
$$
通过一系列严谨的数学推导，包括使用[散度定理](@entry_id:143110)将[表面力](@entry_id:188034)矩的积分转化为[体积分](@entry_id:171119)，并利用已经建立的[线动量](@entry_id:174467)[平衡方程](@entry_id:172166)来抵消部分项，最终可以证明，上述[角动量平衡](@entry_id:181848)方程要求在每一点上都满足以下局部条件 [@problem_id:2616733]：
$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}^T
$$
或者用指标符号表示为 $\sigma_{ij} = \sigma_{ji}$。这意味着**柯西应力张量必须是对称的**。这个结果也被称为 Cauchy 第二运动定律。物理上，如果应力张量不对称（例如 $\sigma_{12} \neq \sigma_{21}$），那么一个无限小的物质微元将会受到一个净的[内力](@entry_id:167605)矩，导致其产生无限大的角加速度，这是不符合物理现实的。因此，应力[张量的对称性](@entry_id:202126)是角动量守恒在连续介质理论中的直接体现。

### 建立适定的问题

[线动量](@entry_id:174467)平衡的局部方程 $\nabla \cdot \boldsymbol{\sigma} + \rho\mathbf{b} = \rho\mathbf{a}$ 是一个[偏微分方程组](@entry_id:172573)。为了得到一个确定唯一的解，我们必须提供附加的条件。这些条件包括在物体边界上施加的**边界条件**（boundary conditions）和（对于动态问题）在初始时刻的**初始条件**（initial conditions）。

边界 $\partial\Omega$ 上的任何一点，都必须指定一种边界条件。通常，整个边界被划分为两个互不重叠的部分 [@problem_id:2616727]：
1.  **位移边界** $\Gamma_u$：在这部分边界上，物体的位移是被指定的。这称为**[位移边界条件](@entry_id:203261)**或**狄利克雷（Dirichlet）条件**。其数学形式为 $\mathbf{u} = \bar{\mathbf{u}}$，其中 $\bar{\mathbf{u}}$ 是已知的位移函数。
2.  **面力边界** $\Gamma_t$：在这部分边界上，作用于物体表面的力是被指定的。这称为**[面力边界条件](@entry_id:167112)**或**诺伊曼（Neumann）条件**。其数学形式为 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n} = \bar{\mathbf{t}}$，其中 $\bar{\mathbf{t}}$ 是已知的[面力矢量](@entry_id:189429)函数。

一个适定的[边值问题](@entry_id:193901)要求 $\Gamma_u \cup \Gamma_t = \partial\Omega$ 且 $\Gamma_u \cap \Gamma_t = \emptyset$（交集最多为[零测度集](@entry_id:157694)，如边或角）。这意味着在边界的每一点，我们要么指定位移，要么指定面力，但不能同时指定两者（对于同一方向分量），否则问题将是超定的。

在[变分原理](@entry_id:198028)和有限元方法中，这两类边界条件有不同的性质。[位移边界条件](@entry_id:203261)必须在求[解空间](@entry_id:200470)的函数选择上就得到满足，因此被称为**本质边界条件**（essential boundary conditions）。相反，[面力边界条件](@entry_id:167112)是在[变分方程](@entry_id:635018)的推导过程中自然出现的，因此被称为**自然边界条件**（natural boundary conditions）[@problem_id:2616727]。

对于动态问题（$\mathbf{a} \neq \mathbf{0}$），除了边界条件，还必须指定物体的初始状态，通常是初始[位移场](@entry_id:141476) $\mathbf{u}(\mathbf{x}, t=0)$ 和初始速度场 $\mathbf{v}(\mathbf{x}, t=0)$。

### 大变形的应力度量

柯西应力张量 $\boldsymbol{\sigma}$ 是在**当前构型**（current configuration）中定义的，它将当前构型中的法向矢量映射到当前构型中的力矢量。在小变形问题中，当前构型与**参考构型**（reference configuration）几乎没有区别，使用柯西应力非常方便。然而，在**[大变形](@entry_id:167243)**（large deformation）问题中，物体的形状和体积会发生显著变化，求解区域本身是未知的，这使得在当前构型上建立方程变得复杂。

为了解决这个问题，我们引入在固定不变的参考构型上定义的应力度量。这需要将在当前构型中作用的力“[拉回](@entry_id:160816)”到参考构型中。

通过保持微元上的总作用力不变，即 $\mathbf{t} \,ds = \mathbf{T}_0 \,dS_0$（其中 $ds$ 和 $dS_0$ 分别是当前和参考构型的面元面积），并利用 Nanson 公式关联两个构型的面元法向，我们定义了**第一 Piola-Kirchhoff (PK1) [应力张量](@entry_id:148973)** $\mathbf{P}$ [@problem_id:2616703]：
$$
\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-T}
$$
其中 $\mathbf{F}$ 是变形梯度，$J = \det(\mathbf{F})$。$\mathbf{P}$ 是一个“两点张量”，它将参考构型中的法向矢量 $\mathbf{N}$ 映射到当前构型中的力矢量。名义面力（单位参考面积上的力）$\mathbf{T}_0$ 就由 $\mathbf{T}_0 = \mathbf{P}\mathbf{N}$ 给出。使用 $\mathbf{P}$，[线动量](@entry_id:174467)平衡方程可以在参考构型上写为 [@problem_id:2616708]：
$$
\mathrm{Div}(\mathbf{P}) + \rho_0 \mathbf{b} = \rho_0 \mathbf{a}
$$
其中 $\mathrm{Div}$ 是对参考构型坐标的[散度算子](@entry_id:265975)，$\rho_0$ 是参考构型中的密度。尽管 $\mathbf{P}$ 在动量方程中形式简洁，但它通常是**非对称的**。

为了获得一个对称的拉格朗日应力度量，我们进一步定义了**第二 Piola-Kirchhoff (PK2) [应力张量](@entry_id:148973)** $\mathbf{S}$：
$$
\mathbf{S} = \mathbf{F}^{-1}\mathbf{P} = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T}
$$
$\mathbf{S}$ 是一个纯粹定义在参考构型上的张量（它将参考构型中的矢量映射到参考构型中的矢量）。由于柯西应力 $\boldsymbol{\sigma}$ 是对称的，可以证明 $\mathbf{S}$ 也总是**对称的**。这使得 $\mathbf{S}$ 在建立[本构关系](@entry_id:186508)时特别有用，因为它与[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E}$ 是能量共轭的（即单位参考体积的应变功率为 $\mathbf{S}:\dot{\mathbf{E}}$）[@problem_id:2616703]。然而，$\mathbf{S}$ 并不直接以简单的[散度形式](@entry_id:748608)出现在动量[平衡方程](@entry_id:172166)中 [@problem_id:2616708]。

总之，$\boldsymbol{\sigma}$, $\mathbf{P}$, $\mathbf{S}$ 是描述同一物理应力状态的不同数学表示，选择哪种取决于具体问题的数学框架，尤其是在处理[大变形](@entry_id:167243)问题时，$\mathbf{P}$ 和 $\mathbf{S}$ 提供了在固定参考域上求解问题的强大工具。