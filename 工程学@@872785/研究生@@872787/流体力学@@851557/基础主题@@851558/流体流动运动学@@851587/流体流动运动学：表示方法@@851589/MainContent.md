## 引言
[流体运动学](@entry_id:202835)是[流体力学](@entry_id:136788)的基础分支，它专注于描述流体的运动，而不探究引起运动的力。从湍急的河流到细胞内的原生质流动，理解这些复杂现象的第一步，是建立一个能够精确描述其几何形态与[时间演化](@entry_id:153943)的数学框架。然而，流体由无数连续介质质点构成，其运动模式千变万化，如何系统地、定量地进行描述，构成了本学科的核心挑战。本文旨在为读者构建一个关于[流体运动学](@entry_id:202835)表示方法的完整知识体系。

本文将引导读者逐步深入[流体运动学](@entry_id:202835)的世界。在“原理与机制”一章中，我们将从描述[流体运动](@entry_id:182721)的两种基本视角——拉格朗日和[欧拉观点](@entry_id:198701)——出发，并引入连接二者的关键概念“[物质导数](@entry_id:172646)”。随后，我们将学习如何通过流线、[迹线](@entry_id:261720)等工具将抽象的[速度场](@entry_id:271461)可视化，并定量分析流体微元的局部运动，将其分解为平移、旋转与变形。在“应用与跨学科联系”一章中，我们将看到这些基本原理如何应用于高等[流体力学](@entry_id:136788)、计算科学、海洋学乃至生命科学等前沿领域，揭示运动学在解决真实世界问题中的强大威力。最后，通过“动手实践”部分，您将有机会通过解决具体问题来巩固和深化所学知识，将理论真正内化为自己的技能。

## 原理与机制

[流体运动学](@entry_id:202835)是研究流体运动几何特性而不考虑其背后作用力的学科。本章旨在系统阐述描述和分析流体运动的基本原理与核心机制。我们将从两种基本描述方法——[拉格朗日观点](@entry_id:265471)和[欧拉观点](@entry_id:198701)——出发，建立起连接二者的关键概念“[物质导数](@entry_id:172646)”。随后，我们将探讨用于[流场可视化](@entry_id:269520)的基本工具，如[流线和迹线](@entry_id:182288)，并定量分析它们在[非稳态流](@entry_id:269993)中的区别。最后，我们将深入到流体微元的局部运动学，通过分析[速度梯度张量](@entry_id:270928)来揭示[流体运动](@entry_id:182721)的内在结构，包括变形与旋转，并介绍用于区分不同流动区域拓扑特征的判据。

### 流体运动的描述方法

#### [拉格朗日与欧拉](@entry_id:270774)观点

描述流体运动存在两种根本不同的视角。第一种是**[拉格朗日描述](@entry_id:264498) (Lagrangian description)**，它如同给每个流体质点贴上标签，并追踪这些特定质点随时间的运动轨迹。我们将一个[质点](@entry_id:186768)的初始位置 $\vec{X}_0 = (\xi, \eta, \zeta)$ 作为其永久的“标签”。该[质点](@entry_id:186768)在任意时刻 $t$ 的空间位置 $\vec{x}$ 便是其初始位置和时间的函数，即 $\vec{x} = \vec{x}(\vec{X}_0, t)$。在这种描述下，质点的速度和加速度可以通过对固定质点（即固定 $\vec{X}_0$）的位置矢量求时间导数得到：

$\vec{v}_L(\vec{X}_0, t) = \frac{\partial \vec{x}}{\partial t} \bigg|_{\vec{X}_0}$
$\vec{a}_L(\vec{X}_0, t) = \frac{\partial^2 \vec{x}}{\partial t^2} \bigg|_{\vec{X}_0}$

第二种是**[欧拉描述](@entry_id:264722) (Eulerian description)**，它关注空间中固定的点，并观察流体属性（如速度、压力、密度）在这些点上如何随时间变化。例如，速度场被表示为空间位置 $\vec{x}$ 和时间 $t$ 的函数，即 $\vec{u}(\vec{x}, t)$。这个函数描述的是在 $t$ 时刻，占据空间点 $\vec{x}$ 的那个（可能是不同的）流体质点所具有的速度。

虽然[拉格朗日描述](@entry_id:264498)直观地对应于[牛顿力学](@entry_id:162125)中对质点运动的追踪，但在大多数[流体力学](@entry_id:136788)问题中，[欧拉描述](@entry_id:264722)由于其能够直接处理固定区域内的流动（如流过管道或绕过[翼型](@entry_id:195951)的流体）而更为实用。因此，理解两种描述之间的转换至关重要。

从[拉格朗日描述](@entry_id:264498)到[欧拉描述](@entry_id:264722)的转换，原则上需要两个步骤：首先，计算出拉格朗日速度 $\vec{v}_L(\vec{X}_0, t)$；其次，通过位置关系 $\vec{x} = \vec{x}(\vec{X}_0, t)$ 反解出初始位置与当前位置和时间的关系 $\vec{X}_0 = \vec{X}_0(\vec{x}, t)$，并将其代入拉格朗日速度表达式中，从而得到欧拉速度 $\vec{u}(\vec{x}, t) = \vec{v}_L(\vec{X}_0(\vec{x}, t), t)$。然而，直接进行这种反解通常非常困难。

一个更直接的问题是，给定[拉格朗日描述](@entry_id:264498)，如何求得在特定欧拉时空点 $(\vec{x}, t)$ 的加速度？欧拉[加速度场](@entry_id:266595) $\vec{a}(\vec{x}, t)$ 描述的是在 $t$ 时刻位于 $\vec{x}$ 处的流体[质点](@entry_id:186768)的加速度。这个[质点](@entry_id:186768)的加速度，根据其定义，就是它的拉格朗日加速度。因此，我们只需找到在 $t$ 时刻恰好位于 $\vec{x}$ 处的那个[质点](@entry_id:186768)的初始标签 $\vec{X}_0$，然后计算该[质点](@entry_id:186768)的拉格朗日加速度即可。

例如，考虑一个二维[非稳态流](@entry_id:269993)动，其拉格朗日映射由以下方程给出 [@problem_id:554292]：
$x(\xi, \eta, t) = \xi - \frac{A}{k} \sin(k\eta) \sin(\omega t)$
$y(\xi, \eta, t) = \eta + \frac{B}{k} \sin(k\xi) \cos(\omega t)$

要计算在特定时空点 $(x_p, y_p, t_p) = (\frac{\pi}{2k}, \frac{\pi}{2k}, \frac{\pi}{\omega})$ 的欧拉加速度，我们首先计算任意质点 $(\xi, \eta)$ 的拉格朗日加速度分量：
$a_x(\xi, \eta, t) = \frac{\partial^2 x}{\partial t^2} = \frac{A\omega^2}{k}\sin(k\eta)\sin(\omega t)$
$a_y(\xi, \eta, t) = \frac{\partial^2 y}{\partial t^2} = -\frac{B\omega^2}{k}\sin(k\xi)\cos(\omega t)$

在特定时刻 $t_p = \frac{\pi}{\omega}$，我们有 $\sin(\omega t_p) = \sin(\pi) = 0$ 和 $\cos(\omega t_p) = \cos(\pi) = -1$。此时，[质点](@entry_id:186768)的位置变为：
$x(\xi, \eta, t_p) = \xi$
$y(\xi, \eta, t_p) = \eta - \frac{B}{k} \sin(k\xi)$
我们需要找到在 $t_p$ 时刻位于 $(x_p, y_p)$ 的[质点](@entry_id:186768)的初始位置 $(\xi, \eta)$。通过代入 $x_p = \frac{\pi}{2k}$ 和 $y_p = \frac{\pi}{2k}$，我们得到 $\xi = x_p = \frac{\pi}{2k}$。将 $\xi$ 的值代入 $y$ 的方程，可以解出 $\eta$。然而，注意到在 $t_p$ 时刻，$a_x$ 分量由于 $\sin(\omega t_p) = 0$ 恒为零，而 $a_y$ 分量仅依赖于 $\xi$。因此，我们无需计算 $\eta$ 的具体值，可以直接代入 $\xi$ 和 $t_p$：
$a_x(t_p) = 0$
$a_y(\xi, \eta, t_p) = -\frac{B\omega^2}{k}\sin(k\xi)\cos(\omega t_p) = -\frac{B\omega^2}{k}\sin(k \frac{\pi}{2k})(-1) = \frac{B\omega^2}{k}$

因此，在时空点 $(\frac{\pi}{2k}, \frac{\pi}{2k}, \frac{\pi}{\omega})$ 的加速度向量为 $(0, \frac{B\omega^2}{k})$，其大小为 $\frac{B\omega^2}{k}$。这个过程阐明了欧拉加速度的物理意义：它是跟随流体[质点](@entry_id:186768)定义的加速度在特定时空点的体现。

#### 物质导数：连接两种描述

为了在[欧拉框架](@entry_id:749109)内系统地描述跟随流体[质点](@entry_id:186768)的物理量的变化率，我们引入**物质导数 (material derivative)**，记为 $\frac{D}{Dt}$。考虑一个依赖于欧拉坐标的物理量 $F(\vec{x}, t)$，我们想知道当跟随一个运动轨迹为 $\vec{x}_p(t)$ 的流体[质点](@entry_id:186768)时，$F$ 的变化率是多少。根据[链式法则](@entry_id:190743)：
$\frac{d}{dt} F(\vec{x}_p(t), t) = \frac{\partial F}{\partial t} + \frac{\partial F}{\partial x_i} \frac{dx_{p,i}}{dt}$
由于[质点](@entry_id:186768)速度就是流体的欧拉速度 $\frac{d\vec{x}_p}{dt} = \vec{u}(\vec{x}_p(t), t)$，我们可以将上式写成算子形式：
$\frac{D}{Dt} \equiv \frac{\partial}{\partial t} + \vec{u} \cdot \nabla$

物质导数由两部分组成：**[局部变化率](@entry_id:264961) (local rate of change)** $\frac{\partial}{\partial t}$，表示在空间[固定点](@entry_id:156394)上物理量随时间的变化；以及**[对流](@entry_id:141806)变化率 (convective rate of change)** $\vec{u} \cdot \nabla$，表示由于质点从一个地方移动到另一个物理量值不同的地方而引起的变化。

物质导数的一个直接应用是定义**物质面 (material surface)**。一个由[隐式方程](@entry_id:177636) $f(\vec{x}, t) = C$ 定义的随[时间演化](@entry_id:153943)的[曲面](@entry_id:267450)族，如果总是由相同的流体[质点](@entry_id:186768)构成，则被称为物质面。这意味着，对于任何一个最初位于该[曲面](@entry_id:267450)上的质点，其 $f$ 值将保持不变。换言之，跟随[质点](@entry_id:186768)运动时 $f$ 的变化率为零 [@problem_id:554390]。因此，物质面的充要条件是：
$\frac{Df}{Dt} = \frac{\partial f}{\partial t} + \vec{u} \cdot \nabla f = 0$
这个简洁的方程为[分析物](@entry_id:199209)质线、物质面和物质体积的演化提供了强大的数学工具。

将[物质导数](@entry_id:172646)应用于欧拉[速度场](@entry_id:271461) $\vec{u}$ 本身，我们便得到了欧拉[加速度场](@entry_id:266595)的标准表达式：
$\vec{a}(\vec{x}, t) = \frac{D\vec{u}}{Dt} = \frac{\partial \vec{u}}{\partial t} + (\vec{u} \cdot \nabla)\vec{u}$
这里的[非线性](@entry_id:637147)项 $(\vec{u} \cdot \nabla)\vec{u}$ 被称为**[对流加速度](@entry_id:263153) (convective acceleration)**，是纳维-斯托克斯方程复杂性的主要来源之一。通过一个重要的矢量恒等式，我们可以揭示[对流加速度](@entry_id:263153)的物理内涵 [@problem_id:554386]。该恒等式将[对流加速度](@entry_id:263153)分解为两项：
$(\vec{u} \cdot \nabla)\vec{u} = \nabla\left(\frac{1}{2}|\vec{u}|^2\right) - \vec{u} \times (\nabla \times \vec{u})$
令**[涡量](@entry_id:142747) (vorticity)** 向量为 $\vec{\omega} = \nabla \times \vec{u}$，则上式可写为：
$(\vec{u} \cdot \nabla)\vec{u} = \nabla\left(\frac{1}{2} |\vec{u}|^2\right) + \vec{\omega} \times \vec{u}$
这个分解表明，流体[质点](@entry_id:186768)的[对流加速度](@entry_id:263153)由两部分贡献：一部分是单位质量动能 $\frac{1}{2} |\vec{u}|^2$ 的梯度，驱动流体从高动能区向低动能区加速；另一部分是所谓的**兰姆向量 (Lamb vector)** $\vec{\omega} \times \vec{u}$，它代表了流体的旋转性（[涡量](@entry_id:142747)）与[速度场](@entry_id:271461)的相互作用，且其方向垂直于速度和涡量。在[无旋流动](@entry_id:159258)中 ($\vec{\omega} = \vec{0}$)，[对流加速度](@entry_id:263153)就简化为动能的梯度。

### 流场的可视化

为了直观地理解复杂的流体运动，我们使用几种几何曲线来描绘流场。

#### 流线、[迹线与脉线](@entry_id:272407)

三个最基本的概念是：
*   **[流线](@entry_id:266815) (Streamline)**：在某一固定时刻 $t_0$，流场中一系列与该时刻[速度矢量](@entry_id:269648)处处相切的曲线。流线的方程为 $\frac{d\vec{x}_s}{ds} \propto \vec{u}(\vec{x}_s, t_0)$，其中 $s$ 是沿[流线](@entry_id:266815)的[弧长](@entry_id:191173)参数。流线描绘了该瞬间[流体运动](@entry_id:182721)的“快照”。
*   **[迹线](@entry_id:261720) (Pathline)**：单个流体[质点](@entry_id:186768)在一段时间内实际走过的轨迹。[迹线](@entry_id:261720)由[常微分方程](@entry_id:147024) $\frac{d\vec{x}_p}{dt} = \vec{u}(\vec{x}_p(t), t)$ 的解给出。
*   **[脉线](@entry_id:263857) (Streakline)**：在某一时刻，所有曾经流过空间中某一个[固定点](@entry_id:156394)的流体质点所构成的曲线。可以想象成从一个[固定点](@entry_id:156394)持续释放染料所形成的轨迹。

在**[稳态流](@entry_id:275664) (steady flow)** 中，[速度场](@entry_id:271461)不随时间变化，即 $\frac{\partial \vec{u}}{\partial t} = \vec{0}$。在这种情况下，[流线](@entry_id:266815)的形状固定不变，流体[质点](@entry_id:186768)将沿着固定的[流线](@entry_id:266815)运动，并且从某点释放的染料也会沿着同一条流线[扩散](@entry_id:141445)。因此，在[稳态流](@entry_id:275664)中，流线、[迹线](@entry_id:261720)和[脉线](@entry_id:263857)是重合的。

#### [非稳态流](@entry_id:269993)中的几何关系

然而，在更普遍的**[非稳态流](@entry_id:269993) (unsteady flow)** 中，这三者通常是不同的。流线图在每个瞬间都在变化，而[迹线](@entry_id:261720)则是质点在这一系列变化的流场中穿梭的结果。

它们之间的差异可以用一个优美的几何关系来量化。考虑一个二维[非稳态流](@entry_id:269993)，在任意点 $(x, y)$ 和时刻 $t$，该点的瞬时流线和恰好经过该点的[质点](@entry_id:186768)的[迹线](@entry_id:261720)，通常具有不同的曲率。设 $K_s$ 为流线的曲率，$K_p$ 为[迹线](@entry_id:261720)的曲率，$V = |\vec{v}|$ 为速度大小，$\theta = \arctan(v/u)$ 为速度矢量与x轴的夹角。可以证明，两者曲率之差为 [@problem_id:554309]：
$K_p - K_s = \frac{1}{V} \frac{\partial \theta}{\partial t}$
这个公式直观地说明了[迹线与流线](@entry_id:194917)的分离是由于流场方向的[局部时](@entry_id:194383)间变化所致。如果在一个点附近，流向随时间顺时针转动 ($\frac{\partial \theta}{\partial t}  0$)，那么[质点](@entry_id:186768)的轨迹（[迹线](@entry_id:261720)）将比瞬时流线更“弯曲”（如果$K_s > 0$则$K_p$更小，反之亦然，取决于曲率定义），因为它被“甩”向了[速度矢量](@entry_id:269648)变化的方向。

存在一个特殊的[非稳态流](@entry_id:269993)情况，即[速度场](@entry_id:271461)可以分离变量为 $\vec{u}(\vec{x}, t) = f(t)\vec{v}(\vec{x})$，其中 $f(t)>0$ [@problem_id:554358]。在这种情况下，由于速度场的方向仅由 $\vec{v}(\vec{x})$ 决定，不随时间变化，所以流线的几何形状是固定的。质点会始终保持在同一条流线上运动，因此[迹线与流线](@entry_id:194917)在几何上重合。然而，[质点](@entry_id:186768)沿此路径的运动速度是时变的。设 $s$ 为沿某条[流线](@entry_id:266815)的[弧长](@entry_id:191173)，该流线上[空间速度](@entry_id:190294)分量的大小为 $v_s(s) = |\vec{v}(\vec{x}_s(s))|$。[质点](@entry_id:186768)沿该[流线](@entry_id:266815)的运动由以下[微分方程](@entry_id:264184)描述：
$\frac{ds}{dt} = f(t) v_s(s)$
这表明，尽管轨迹形状不变，但质点在轨迹上的运动速率会根据时间函数 $f(t)$ 和空间位置 $s$ 而调制。

### 流体微元的[运动学](@entry_id:173318)分析

为了理解流体在宏观上如何变形和输运，我们需要考察一个无限小的流体微元在其邻域内的相对运动。所有复杂的局部运动都可以分解为四种[基本模式](@entry_id:165201)：平移、旋转、拉伸/压缩（[正应变](@entry_id:204633)）和剪切（切应变）。

#### [速度梯度张量](@entry_id:270928)

描述流场局部特性的核心数学工具是**[速度梯度张量](@entry_id:270928) (velocity gradient tensor)**，定义为 $\mathbf{A} = \nabla \vec{u}$，其分量为 $A_{ij} = \frac{\partial u_i}{\partial x_j}$。该张量描述了在一个点附近，速度场如何随空间位置变化。考虑一个点 $\vec{x}$ 和一个邻近点 $\vec{x} + d\vec{x}$，它们之间的相对速度 $d\vec{u}$ 可以由一阶[泰勒展开](@entry_id:145057)近似：
$d\vec{u} = \vec{u}(\vec{x} + d\vec{x}) - \vec{u}(\vec{x}) \approx (\nabla \vec{u}) \cdot d\vec{x} = \mathbf{A} \cdot d\vec{x}$

[速度梯度张量](@entry_id:270928)可以唯一地分解为一个对称[部分和](@entry_id:162077)一个反对称部分：$\mathbf{A} = \mathbf{S} + \mathbf{\Omega}$。
*   **[应变率张量](@entry_id:266108) (Rate-of-Strain Tensor)**: $\mathbf{S} = \frac{1}{2}(\nabla \vec{u} + (\nabla \vec{u})^T)$
*   **自旋率张量 (Spin Tensor) 或旋转率张量 (Rate-of-Rotation Tensor)**: $\mathbf{\Omega} = \frac{1}{2}(\nabla \vec{u} - (\nabla \vec{u})^T)$

这个分解具有深刻的物理意义：对称的[应变率张量](@entry_id:266108) $\mathbf{S}$ 描述了流体微元的纯变形（拉伸和剪切），而反对称的自旋率张量 $\mathbf{\Omega}$ 描述了流体微元的刚性旋转。

#### 变形：体积、线性与[剪切应变率](@entry_id:276945)

[应变率张量](@entry_id:266108) $\mathbf{S}$ 完全刻画了流体微元的形状变化速率。

首先，考虑一个初始体积为 $\delta V$ 的物质微元。其体积随时间的变化率与[速度场](@entry_id:271461)的散度密切相关。通过分析一个无限小长方体微元在 $\delta t$ 时间内的形变，可以证明其体积的物质变化率满足 [@problem_id:554320]：
$\frac{1}{\delta V} \frac{D(\delta V)}{Dt} = \frac{\partial u}{\partial x} + \frac{\partial v}{\partial y} + \frac{\partial w}{\partial z} = \nabla \cdot \vec{u}$
这个重要的关系表明，**速度场的散度 (divergence of the velocity field)** 度量了单位体积流体的膨胀或收缩率。对于**[不可压缩流](@entry_id:140301) (incompressible flow)**，我们假设流体密度不变，这意味着任何流体微元的体积也必须保持不变，因此[不可压缩流](@entry_id:140301)的运动学条件就是 $\nabla \cdot \vec{u} = 0$。

其次，考虑一个由单位矢量 $\vec{n}$ 表征方向的物质线元。其长度 $L$ 的变化率，即**线性[应变率](@entry_id:154778) (rate of linear strain)**，由二次型 $\vec{n}^T \mathbf{S} \vec{n}$ 给出。这个量依赖于[线元](@entry_id:196833)的朝向 $\vec{n}$。例如，在[二维流](@entry_id:266853)中，若 $\vec{n} = (\cos\theta, \sin\theta)$，则线性[应变率](@entry_id:154778)为 $\epsilon(\theta) = S_{11}\cos^2\theta + 2S_{12}\cos\theta\sin\theta + S_{22}\sin^2\theta$ [@problem_id:554367]。

一个有趣的问题是，在某一点，所有方向上线性应变率的平均值是多少？在二维情况下，通过对所有方向（$\theta \in [0, \pi]$）进行平均，我们得到平均线性[应变率](@entry_id:154778) $\bar{\epsilon}$：
$\bar{\epsilon} = \frac{1}{\pi} \int_0^\pi \epsilon(\theta) d\theta = \frac{1}{2}(S_{11} + S_{22})$
由于 $S_{11} = \frac{\partial u}{\partial x}$ 和 $S_{22} = \frac{\partial v}{\partial y}$，我们发现 $\bar{\epsilon} = \frac{1}{2}(\frac{\partial u}{\partial x} + \frac{\partial v}{\partial y}) = \frac{1}{2}\nabla \cdot \vec{u}$。这个结果推广到三维也是成立的：平均线性应变率等于散度的三分之一。这再次表明，速度场的散度是衡量流体微元纯体积变化的[平均度](@entry_id:261638)量。

#### 旋转：涡量与自旋率张量

自旋率张量 $\mathbf{\Omega}$ 描述了流体的局部刚性旋转。$\mathbf{\Omega}$ 的分量与之前定义的涡量向量 $\vec{\omega} = \nabla \times \vec{u}$ 直接相关。可以证明，$\mathbf{\Omega}$ 对任意向量 $\vec{c}$ 的作用等价于[涡量](@entry_id:142747)向量叉乘的一半：
$\mathbf{\Omega} \cdot \vec{c} = \frac{1}{2} \vec{\omega} \times \vec{c}$
这表明流体微元以[角速度](@entry_id:192539) $\frac{1}{2}\vec{\omega}$ 进行刚性旋转。因此，涡量 $\vec{\omega}$ 的大小是局部[流体旋转](@entry_id:273789)角速度的两倍。当 $\vec{\omega} = \vec{0}$ 时，流动被称为**无[旋流](@entry_id:153202) (irrotational flow)**。

### 流动拓扑的分类与应用

通过将局部运动分解为应变和旋转，我们可以[对流](@entry_id:141806)场的局部拓扑结构进行分类，并研究一些具有特殊运动学约束的[理想流](@entry_id:261917)动模型。

#### 应变主导与[涡量](@entry_id:142747)主导区域

在任意一点，流体运动是更倾向于拉伸变形还是更倾向于旋转，取决于应变率张量 $\mathbf{S}$ 和自旋率张量 $\mathbf{\Omega}$ 的相对“强度”。这种分类可以通过分析[速度梯度张量](@entry_id:270928) $\mathbf{A}$ 的[特征值](@entry_id:154894)来完成 [@problem_id:554351]。对于[二维不可压缩流](@entry_id:136406)，$\nabla \cdot \vec{u} = 0$ 意味着 $\mathbf{A}$ 的迹为零。其[特征方程](@entry_id:265849)为 $\lambda^2 - (\det \mathbf{A}) = 0$，解为 $\lambda = \pm \sqrt{\det \mathbf{A}}$。
*   如果 $\det \mathbf{A} > 0$，[特征值](@entry_id:154894)为共轭复数，表示局部[流线](@entry_id:266815)呈椭圆形或圆形，这是**涡量主导 (vorticity-dominated)** 的区域。
*   如果 $\det \mathbf{A}  0$，[特征值](@entry_id:154894)为一正一负的实数，表示局部[流线](@entry_id:266815)呈双曲线形，这是**应变主导 (strain-dominated)** 的区域，对应一个[鞍点](@entry_id:142576)。
*   如果 $\det \mathbf{A} = 0$，则为临界情况，如简单剪切流。

为了用物理量表示这个判据，我们计算 $\det \mathbf{A}$。对于[二维不可压缩流](@entry_id:136406)（$\frac{\partial v}{\partial y} = -\frac{\partial u}{\partial x}$），我们定义[正应变](@entry_id:204633)率 $s_n = \frac{\partial u}{\partial x}$，[剪应变率](@entry_id:189459) $s_s = \frac{1}{2}(\frac{\partial u}{\partial y} + \frac{\partial v}{\partial x})$，以及[涡量](@entry_id:142747) $\omega_z = \frac{\partial v}{\partial x} - \frac{\partial u}{\partial y}$。经过计算可得：
$-\det \mathbf{A} = s_n^2 + s_s^2 - \frac{\omega_z^2}{4}$
海洋学和[地球物理流体动力学](@entry_id:150356)中广泛使用的**Okubo-Weiss参数** $Q$ 定义为：
$Q = s_n^2 + s_s^2 - \frac{\omega_z^2}{4}$
这个参数优雅地量化了应变和旋转的竞争：
*   $Q  0$：旋转主导（涡旋结构）。
*   $Q > 0$：应变主导（变形场）。
这使得我们能够从一个速度场数据中自动识别出涡旋和变形区域。

#### [势流理论](@entry_id:267452)：[流函数](@entry_id:266505)与[势函数](@entry_id:176105)

在一些理想化的流动中，[运动学](@entry_id:173318)约束大大简化了问题的分析。**[势流理论](@entry_id:267452) (Potential Flow Theory)** 是研究无粘、无旋、[不可压缩流](@entry_id:140301)动的理论框架。
*   **无旋条件** ($\nabla \times \vec{u} = \vec{0}$) 保证了可以引入一个标量**[速度势](@entry_id:262992)函数 (velocity potential)** $\phi$，使得 $\vec{u} = \nabla \phi$。
*   对于[二维流](@entry_id:266853)动，**不可压缩条件** ($\nabla \cdot \vec{u} = 0$) 保证了可以引入一个标量**[流函数](@entry_id:266505) (stream function)** $\psi$，使得 $u = \frac{\partial \psi}{\partial y}$ 和 $v = - \frac{\partial \psi}{\partial x}$。

流函数的一个重要性质是，沿着一条流线 $\psi$ 的值保持不变，即流线是 $\psi$ 的等值线。类似地，[速度势](@entry_id:262992)的等值线被称为**等势线 (equipotential lines)**。
这两个函数之间存在一个基本的几何关系。[等势线](@entry_id:276883)的[法向量](@entry_id:264185)是 $\nabla \phi$，而[流线](@entry_id:266815)的法向量是 $\nabla \psi$。考虑这两个梯度的[点积](@entry_id:149019) [@problem_id:554361]：
$\nabla \phi \cdot \nabla \psi = \left(\frac{\partial \phi}{\partial x}, \frac{\partial \phi}{\partial y}\right) \cdot \left(\frac{\partial \psi}{\partial x}, \frac{\partial \psi}{\partial y}\right) = (u, v) \cdot (-v, u) = -uv + vu = 0$
由于它们的法向量正交，因此[等势线](@entry_id:276883)和流线本身处处正交。这构成了一个方便的“[流网](@entry_id:265008) (flow net)”，可用于可视化和计算二维[势流](@entry_id:159985)问题。

#### 物质面与[标量输运](@entry_id:150360)

最后，我们将物质面和标量守恒的概念结合在一个综合实例中。考虑一个三维不可压缩[点源](@entry_id:196698)流，其[速度场](@entry_id:271461)为 $\vec{u}(\vec{x}) = \frac{Q}{4\pi r^2}\hat{\mathbf{r}}$。一个[标量场](@entry_id:151443) $\psi(\vec{x}, t)$ 被动地随流体[平流](@entry_id:270026)，这意味着其物质导数为零，$\frac{D\psi}{Dt} = 0$ [@problem_id:554294]。在 $t=0$ 时，$\psi(\vec{x}, 0) = \frac{\beta}{r^3}$，并且我们有一个初始为半径 $R_0$ 的球形物质面 $\mathcal{S}(t)$。

要计算积分 $\int_{\mathcal{S}(t)} \psi^2 dA$ 的时间变化率，我们首先需要追踪物质球面如何演化。球面上任意[质点](@entry_id:186768)的径向位置 $r(t)$ 满足 $\frac{dr}{dt} = u_r = \frac{Q}{4\pi r^2}$，积分可得 $r(t) = \left(R_0^3 + \frac{3Qt}{4\pi}\right)^{1/3}$。
由于 $\psi$ 是物质守恒的，即每个流体质点携带其初始的 $\psi$ 值。对于在 $t=0$ 时刻位于 $r=R_0$ 上的[质点](@entry_id:186768)，其 $\psi$ 值恒为 $\psi_0 = \frac{\beta}{R_0^3}$。因此，在时刻 $t$，在演化后的球面 $\mathcal{S}(t)$ 上，$\psi^2$ 的值处处为常数 $\frac{\beta^2}{R_0^6}$。
球面面积为 $A(t) = 4\pi r(t)^2$。于是积分值为：
$I(t) = \int_{\mathcal{S}(t)} \psi^2 dA = \psi_0^2 A(t) = \frac{\beta^2}{R_0^6} \cdot 4\pi r(t)^2$
对时间求导，并代入 $\frac{dr}{dt}$ 和 $r(t)$ 的表达式，我们最终得到：
$\frac{dI}{dt} = \frac{2Q\beta^2}{R_0^6\left(R_0^3+\frac{3Qt}{4\pi}\right)^{1/3}}$
这个例子完美地展示了如何结合流体质点的[运动学](@entry_id:173318)追踪（拉格朗日思想）、物质[守恒定律](@entry_id:269268)和积分计算，来分析一个在演化域上的物理量的变化。这集中体现了本章介绍的多个核心原理与机制。