## 引言
在[流体力学](@entry_id:136788)的宏伟画卷中，[速度场](@entry_id:271461)是描绘流体运动形态的基石。它如同一个无所不在的观察者，为我们提供了空间中每一点流体在任意时刻的[瞬时速度](@entry_id:167797)，从而构成了对[流体运动](@entry_id:182721)最完整的[运动学](@entry_id:173318)描述。掌握[速度场](@entry_id:271461)不仅是理解和预测流体行为的第一步，更是连接[流体运动学](@entry_id:202835)（如何运动）与动力学（为何如此运动）的关键桥梁。然而，这一看似基础的概念背后，蕴含着丰富的物理机制和深刻的数学结构，从流动分类到质点加速度的计算，再到微元变形与旋转的分析，每一个环节都至关重要。本文旨在系统性地剖析[速度场](@entry_id:271461)，解决从抽象数学表述到具体物理图像的认知鸿沟。

为实现这一目标，本文将分为三个核心部分。在 **“原理与机制”** 一章中，我们将奠定理论基础，深入探讨描述[速度场](@entry_id:271461)的欧拉方法、流动的基本分类、用于可视化的[流线](@entry_id:266815)与[迹线](@entry_id:261720)，以及至关重要的加速度、变形和旋转等运动学概念。随后，在 **“应用与跨学科联系”** 一章中，我们将视野从理论转向实践，展示速度场如何在工程设计、[地球物理模拟](@entry_id:749873)、天体物理乃至计算生物学等多元领域中发挥其强大的分析和建模能力。最后，在 **“动手实践”** 部分，我们将通过一系列精心设计的练习，引导读者将所学知识应用于具体问题的求解，从而巩固和深化理解。通过这一结构化的学习路径，读者将能够建立起对速度场全面而深入的认识。

## 原理与机制

在对[流体运动](@entry_id:182721)的分析中，速度场是描述[流体动力学](@entry_id:136788)状态最核心的物理量。它为我们提供了一个瞬时快照，展示了空间中每一点的[流体速度](@entry_id:267320)。本章旨在深入探讨速度场的内在原理与关键机制，从其数学描述到其物理意义，建立一个系统性的理解框架。

### 速度场的[欧拉描述](@entry_id:264722)

描述[流体运动](@entry_id:182721)有两种基本方法：[拉格朗日方法](@entry_id:142825)和欧拉方法。[拉格朗日方法](@entry_id:142825)通过追踪每个单独的流体质点的运动轨迹来描述流动，就像在地图上标记一艘艘船的航行路线。然而，在大多数工程和物理问题中，我们更关心的是固定空间点上的[流体性质](@entry_id:200256)（如速度、压力），而不是追踪亿万个流体[质点](@entry_id:186768)的轨迹。

因此，[流体力学](@entry_id:136788)主要采用 **[欧拉描述](@entry_id:264722) (Eulerian description)**。在这种描述下，我们将速度视为一个依赖于空间坐标和时间的向量函数，即 **[速度场](@entry_id:271461) (velocity field)** $\vec{V}(x, y, z, t)$。这个向量场在任意给定时刻 $t$，为空间中的每一点 $(x, y, z)$ 指定了一个速度向量。这意味着 $\vec{V}(x, y, z, t)$ 代表的是在时刻 $t$ **流经** 空间点 $(x, y, z)$ 的那个流体质点的速度，而不是某个固定[质点](@entry_id:186768)在不同时刻的速度。这种将注意力从流体质点转移到空间点上的视角，是[流体动力学分析](@entry_id:268621)的基石。

### 流动的分类：[稳态](@entry_id:182458)与非[稳态](@entry_id:182458)，均匀与非均匀

为了系统地研究和简化问题，我们常常根据[速度场](@entry_id:271461)在时间和空间上的变化特性[对流](@entry_id:141806)动进行分类。

**[稳态流](@entry_id:275664) (steady flow)** 与 **[非稳态流](@entry_id:269993) (unsteady flow)** 的区别在于流动是否随时间变化。如果在一个流动中，任意空间点的[速度矢量](@entry_id:269648)都不随时间改变，那么这个流动就是[稳态](@entry_id:182458)的。用数学语言表达，即[速度场](@entry_id:271461)对时间的[偏导数](@entry_id:146280)为零：
$$
\frac{\partial \vec{V}}{\partial t} = \vec{0}
$$
反之，如果[速度场](@entry_id:271461)随时间变化，即 $\frac{\partial \vec{V}}{\partial t} \neq \vec{0}$，则流动是 **非[稳态](@entry_id:182458)** 的。在[稳态流](@entry_id:275664)中，流场的形态是恒定的，就像一条稳定流淌的河流。而在[非稳态流](@entry_id:269993)中，流场在不断演变，例如启动或关闭阀门时管道中的水流。

**均匀流 (uniform flow)** 与 **[非均匀流](@entry_id:262867) (non-uniform flow)** 的区别在于流动是否随空间位置变化。如果在任一时刻，流场中所有点的[速度矢量](@entry_id:269648)都相同，那么这个流动就是均匀的。这意味着速度场对所有空间坐标的梯度都为零。反之，如果速度矢量随空间位置变化，则流动是 **非均匀** 的。例如，在一条等[截面](@entry_id:154995)直管中远离入口和出口的流动可以近似为均匀流，而水流过弯道或障碍物时，由于不同位置的速度大小和方向都不同，因此是典型的[非均匀流](@entry_id:262867)。

为了更清晰地理解这些概念，我们来看一个具体的例子。假设一个微通道中流体的速度场模型为 $\vec{V} = ( A x^{2} + B \cos(\omega t) ) \hat{i}$，其中 $A, B, \omega$ 均为非零常数 [@problem_id:1805696]。
为了判断其是否为[稳态流](@entry_id:275664)，我们计算速度场对时间的偏导数：
$$
\frac{\partial \vec{V}}{\partial t} = \frac{\partial}{\partial t} \left( A x^{2} + B \cos(\omega t) \right) \hat{i} = (-B \omega \sin(\omega t)) \hat{i}
$$
由于 $B$ 和 $\omega$ 非零，该导数通常不为零，因此该流动是 **非[稳态](@entry_id:182458)** 的。
为了判断其是否为[均匀流](@entry_id:272775)，我们计算速度场对空间坐标的[偏导数](@entry_id:146280)（这里只有 $x$ 方向）：
$$
\frac{\partial \vec{V}}{\partial x} = \frac{\partial}{\partial x} \left( A x^{2} + B \cos(\omega t) \right) \hat{i} = (2 A x) \hat{i}
$$
由于 $A$ 非零，该导数通常不为零，说明速度随位置 $x$ 变化，因此该流动是 **非均匀** 的。综上所述，这个模型描述的是一个非[稳态](@entry_id:182458)、非均匀的流动。

### [流场可视化](@entry_id:269520)：[流线](@entry_id:266815)、[迹线与脉线](@entry_id:272407)

为了直观地理解复杂的流场结构，我们引入了三种几何曲线：流线、[迹线](@entry_id:261720)和[脉线](@entry_id:263857)。

**流线 (Streamline)** 是在某一瞬时，一系列与速度场处处相切的曲线。[流线](@entry_id:266815)图能够即时地展示出流动的方向和模式。流线上任意一点的[切线](@entry_id:268870)方向都代表该点在该时刻的速度方向。对于[二维流](@entry_id:266853)动 $\vec{V} = u(x,y,t)\hat{i} + v(x,y,t)\hat{j}$，流线的斜率 $dy/dx$ 必须等于[速度矢量](@entry_id:269648)的斜率 $v/u$。因此，在给定时刻 $t_0$，[流线方程](@entry_id:203027)由以下[微分方程](@entry_id:264184)定义：
$$
\frac{dy}{dx} = \frac{v(x, y, t_0)}{u(x, y, t_0)}
$$
通过求解这个方程，我们就能得到流场的几何形态 [@problem_id:1805633]。

**[迹线](@entry_id:261720) (Pathline)** 是单个流体质点在一段时间内走过的实际路径。这就像长时间曝光拍摄夜空中星星的移动轨迹。[迹线](@entry_id:261720)是通过对[质点](@entry_id:186768)的速度进行时间积分得到的。对于从 $(x_0, y_0)$ 出发的[质点](@entry_id:186768)，其[迹线](@entry_id:261720)坐标 $(x_p(t), y_p(t))$ 由下式确定：
$$
x_p(t) = x_0 + \int_{0}^{t} u(x_p(\tau), y_p(\tau), \tau) d\tau
$$
$$
y_p(t) = y_0 + \int_{0}^{t} v(x_p(\tau), y_p(\tau), \tau) d\tau
$$

**[脉线](@entry_id:263857) (Streakline)** 是在某一时刻，所有曾经流过空间某[固定点](@entry_id:156394)的流体质点所构成的连线。这就像从一个[固定点](@entry_id:156394)持续释放染料，染料在某一时刻形成的彩色条带。

在 **[稳态流](@entry_id:275664)** 中，由于流场不随时间变化，[流线](@entry_id:266815)、[迹线](@entry_id:261720)和[脉线](@entry_id:263857)是完全重合的。一个[质点](@entry_id:186768)的运动轨迹将恰好沿着一条固定的[流线](@entry_id:266815)。然而，在 **[非稳态流](@entry_id:269993)** 中，这三者通常是不同的。流线图在每个时刻都在变化，而[质点](@entry_id:186768)在从一个旧的[流线](@entry_id:266815)图移动到下一个新的流线图时，其轨迹（[迹线](@entry_id:261720)）不必与任何一个瞬时的[流线](@entry_id:266815)重合。

一个经典的例子可以阐明这一区别 [@problem_id:1805637]。考虑一个速度场 $\vec{V}(t) = U_0 \hat{i} + (kt) \hat{j}$，其中 $U_0$ 和 $k$ 是常数。这是一个空间均匀但时间非[稳态](@entry_id:182458)的流动。
- **[迹线](@entry_id:261720)**：一个从原点 $(0,0)$ 在 $t=0$ 时释放的质点，其速度为 $dx/dt = U_0$ 和 $dy/dt = kt$。积分后得到 $x(t) = U_0 t$ 和 $y(t) = \frac{1}{2}kt^2$。消去时间 $t$，得到[迹线](@entry_id:261720)方程为 $y_p(x) = \frac{k}{2 U_0^2}x^2$，这是一条抛物线。
- **流线**：我们考察 $t=0$ 时刻的流线。此时[速度场](@entry_id:271461)为 $\vec{V}(0) = U_0 \hat{i}$。流线的斜率为 $dy/dx = v/u = 0/U_0 = 0$。因此，通过原点的[流线](@entry_id:266815)是一条水平线 $y_s(x)=0$。

显然，[质点](@entry_id:186768)的实际运动轨迹（抛物线）与它出发瞬间的[流线](@entry_id:266815)（水平线）完全不同。这生动地说明了在[非稳态流](@entry_id:269993)中，[流线](@entry_id:266815)仅仅是流场的一个“瞬时快照”，而[迹线](@entry_id:261720)则记录了质点经历的完整历史。

### 流体微元的[运动学](@entry_id:173318)：加速度

根据牛顿第二定律，力与加速度成正比。因此，要研究[流体运动](@entry_id:182721)的动力学，我们必须首先能正确计算流体质点的加速度。在[欧拉框架](@entry_id:749109)下，流体质点的加速度并不仅仅是[速度场](@entry_id:271461)对时间的偏导数。

一个流体质点的速度之所以会变化，有两个原因：第一，它所在位置的速度场本身可能随时间变化（**[局部加速度](@entry_id:272847)**）；第二，它从一个位置移动到另一个速度不同的位置（**[对流加速度](@entry_id:263153)**）。这两种效应的总和，即跟随流体[质点](@entry_id:186768)测量的速度变化率，被称为 **[物质导数](@entry_id:172646) (material derivative)** 或随动导数，记为 $D/Dt$。

对于速度场 $\vec{V}(x, y, z, t)$，其[物质导数](@entry_id:172646)定义为：
$$
\vec{a} = \frac{D\vec{V}}{Dt} = \frac{\partial \vec{V}}{\partial t} + (\vec{V} \cdot \nabla)\vec{V}
$$
其中：
- $\frac{\partial \vec{V}}{\partial t}$ 是 **[局部加速度](@entry_id:272847) (local acceleration)**，它只在[非稳态流](@entry_id:269993)中存在，代表固定空间点上速度随时间的变化。
- $(\vec{V} \cdot \nabla)\vec{V}$ 是 **[对流加速度](@entry_id:263153) (convective acceleration)**，它源于[质点](@entry_id:186768)在空间中的运动。只要流场是非均匀的，即使是[稳态流](@entry_id:275664)，这个[非线性](@entry_id:637147)项也可能不为零。

一个常见的误解是[稳态流](@entry_id:275664)中质点没有加速度。事实并非如此。在[稳态流](@entry_id:275664)中，$\partial \vec{V}/\partial t = 0$，但只要流场非均匀，[对流加速度](@entry_id:263153)依然存在。例如，考虑一个[稳态](@entry_id:182458)收缩管道中的流动，流体从宽[截面](@entry_id:154995)流向窄[截面](@entry_id:154995)时必然会加速，尽管管道内每一点的速度都恒定不变。

让我们通过一个二维[稳态流](@entry_id:275664)动的例子来计算加速度 [@problem_id:1805667]。设[速度场](@entry_id:271461)为 $\vec{V} = (U_0 + kx^2) \hat{i} - (2kxy) \hat{j}$。这是一个[稳态流](@entry_id:275664)，因此[局部加速度](@entry_id:272847)为零。加速度完全由[对流](@entry_id:141806)项贡献：$\vec{a} = (\vec{V} \cdot \nabla)\vec{V}$。
其 $x$ 和 $y$ 分量分别为：
$$
a_x = u\frac{\partial u}{\partial x} + v\frac{\partial u}{\partial y} = (U_0 + kx^2)(2kx) + (-2kxy)(0) = 2kx(U_0 + kx^2)
$$
$$
a_y = u\frac{\partial v}{\partial x} + v\frac{\partial v}{\partial y} = (U_0 + kx^2)(-2ky) + (-2kxy)(-2kx) = -2ky U_0 - 2k^2x^2y + 4k^2x^2y = 2ky(kx^2 - U_0)
$$
可见，即使在[稳态流](@entry_id:275664)中，由于速度在空间上的变化，流体质点仍然可以经历显著的加速度。

[物质导数](@entry_id:172646)的概念巧妙地连接了拉格朗日和欧拉两种描述。一个[质点](@entry_id:186768)的拉格朗日加速度（即其轨迹的二阶时间导数）在数值上精确等于在[欧拉框架](@entry_id:749109)下，在该[质点](@entry_id:186768)所处位置和时刻计算的[物质导数](@entry_id:172646) [@problem_id:1805651]。

### 局部运动分析：变形与旋转

除了整体的平移运动，一个微小的流体团（或称流体微元）还会经历旋转和变形。这些局部运动的特性完全包含在 **[速度梯度张量](@entry_id:270928) (velocity gradient tensor)** $\nabla\vec{V}$ 中。这个二阶张量可以分解为一个对称[部分和](@entry_id:162077)一个反对称部分，它们分别描述了流体微元的变形和旋转。

$$
\nabla\vec{V} = E + \Omega
$$

其中，$E = \frac{1}{2}[\nabla\vec{V} + (\nabla\vec{V})^T]$ 是 **应变率张量 (rate-of-strain tensor)**，它描述了流体微元的形状如何变化（线性拉伸和[剪切变形](@entry_id:170920)）。
$\Omega = \frac{1}{2}[\nabla\vec{V} - (\nabla\vec{V})^T]$ 是 **[自旋张量](@entry_id:187346) (spin tensor)**，它描述了流体微元的刚性旋转。

一个经典的例子是两[平行板](@entry_id:269827)之间的简单剪切流（平面 Couette 流），其[速度场](@entry_id:271461)为 $\vec{V} = \frac{Uy}{h}\hat{i}$ [@problem_id:1805629]。[速度梯度张量](@entry_id:270928)为：
$$
\nabla\vec{V} = \begin{pmatrix} \frac{\partial u}{\partial x} & \frac{\partial u}{\partial y} \\ \frac{\partial v}{\partial x} & \frac{\partial v}{\partial y} \end{pmatrix} = \begin{pmatrix} 0 & \frac{U}{h} \\ 0 & 0 \end{pmatrix}
$$
其应变率张量和[自旋张量](@entry_id:187346)分别为：
$$
E = \frac{1}{2} \left[ \begin{pmatrix} 0 & \frac{U}{h} \\ 0 & 0 \end{pmatrix} + \begin{pmatrix} 0 & 0 \\ \frac{U}{h} & 0 \end{pmatrix} \right] = \begin{pmatrix} 0 & \frac{U}{2h} \\ \frac{U}{2h} & 0 \end{pmatrix}
$$
$$
\Omega = \frac{1}{2} \left[ \begin{pmatrix} 0 & \frac{U}{h} \\ 0 & 0 \end{pmatrix} - \begin{pmatrix} 0 & 0 \\ \frac{U}{h} & 0 \end{pmatrix} \right] = \begin{pmatrix} 0 & \frac{U}{2h} \\ -\frac{U}{2h} & 0 \end{pmatrix}
$$
这个结果揭示了一个深刻的物理图像：简单的[剪切流](@entry_id:266817)可以被看作是纯应变（使方形微元变成菱形）和纯旋转（使微元旋转）的叠加。

#### [体积应变率](@entry_id:272471)与不可压缩性

[应变率张量](@entry_id:266108)的对角[线元](@entry_id:196833)素之和，即[张量的迹](@entry_id:190669)，具有特殊的物理意义。它代表了流体微元体积的变化率，被称为 **[体积应变率](@entry_id:272471) (volumetric strain rate)**。这个量等于[速度场](@entry_id:271461)的 **散度 (divergence)**。
$$
\text{体积应变率} = \text{tr}(E) = \nabla \cdot \vec{V} = \frac{\partial u}{\partial x} + \frac{\partial v}{\partial y} + \frac{\partial w}{\partial z}
$$
如果一个流动的[体积应变率](@entry_id:272471)为零，即 $\nabla \cdot \vec{V} = 0$，则意味着流体微元在运动过程中[体积保持](@entry_id:141001)不变。这样的流动被称为 **[不可压缩流](@entry_id:140301) (incompressible flow)**。这对于液体和低速气体流动是一个非常好的近似。例如，对于一个速度场为 $\vec{V} = (\alpha x) \hat{i} + (\beta y) \hat{j} + (\gamma z) \hat{k}$ 的流动，其[体积应变率](@entry_id:272471)为 $\nabla \cdot \vec{V} = \alpha + \beta + \gamma$ [@problem_id:1805673]。该流动为[不可压缩流](@entry_id:140301)的条件是 $\alpha + \beta + \gamma = 0$。

#### 涡量与[无旋流动](@entry_id:159258)

[自旋张量](@entry_id:187346)描述了流体的局部旋转。与它密切相关的一个更常用的物理量是 **涡量 (vorticity)** 矢量 $\vec{\omega}$，它定义为[速度场](@entry_id:271461)的 **旋度 (curl)**：
$$
\vec{\omega} = \nabla \times \vec{V}
$$
[涡量矢量](@entry_id:187667)的大小等于流体微元刚性旋转角速度的两倍，其方向为[旋转轴](@entry_id:187094)的方向。如果一个流场中处处涡量为零（$\vec{\omega} = \vec{0}$），则该流动被称为 **[无旋流动](@entry_id:159258) (irrotational flow)**。在[无旋流动](@entry_id:159258)中，流体微元只有平移和变形，没有净的旋转。

值得注意的是，一个具有弯曲[流线](@entry_id:266815)的流动不一定是[旋转流](@entry_id:276737)，而一个具有直线[流线](@entry_id:266815)的流动（如[剪切流](@entry_id:266817)）却可以是[旋转流](@entry_id:276737)。例如，对于[平行剪切流](@entry_id:275289) $\vec{V} = (\alpha y^3 - \beta y) \hat{i}$，尽管流线都是直线，但其涡量为 [@problem_id:1805652]：
$$
\vec{\omega} = \nabla \times \vec{V} = \left(\frac{\partial v}{\partial x} - \frac{\partial u}{\partial y}\right)\hat{k} = -\frac{d}{dy}(\alpha y^3 - \beta y)\hat{k} = -(3\alpha y^2 - \beta)\hat{k}
$$
该流动通常是旋转的。只有在满足 $3\alpha y^2 - \beta = 0$ 的特定位置 $y = \pm\sqrt{\beta/(3\alpha)}$，流动才是局部无旋的。

### 积分分析：流量

除了上述基于[微分](@entry_id:158718)的局部分析，我们还可以通过对速度场进行积分来获得关于流动整体性质的信息。其中一个最重要的积分量是 **[体积流量](@entry_id:265771) (volumetric flow rate)** $Q$，它表示单位时间内流过某一[截面](@entry_id:154995)的流体体积。

[体积流量](@entry_id:265771)是通过对速度矢量在指定[截面](@entry_id:154995) $S$ 上的法向分量进行面积分得到的：
$$
Q = \iint_S (\vec{V} \cdot \hat{n}) \, dA
$$
其中 $\hat{n}$ 是[截面](@entry_id:154995)的[单位法向量](@entry_id:178851)。$\vec{V} \cdot \hat{n}$ 表示速度在垂直于[截面](@entry_id:154995)方向上的分量，只有这个分量[对流](@entry_id:141806)过[截面](@entry_id:154995)的流量有贡献。

例如，考虑一个速度为 $V_0$ 的均匀流，其方向与负 x 轴成 $\theta$ 角向下。其速度矢量为 $\vec{V} = V_0(-\cos\theta \hat{i} - \sin\theta \hat{j})$。我们想要计算流过一个位于 $xz$ 平面、由 $0 \le x \le W, 0 \le z \le H$ 定义的矩形传感器门的流量，并规定沿正 $y$ 方向的流量为正 [@problem_id:1805666]。此处的[法向量](@entry_id:264185)为 $\hat{n} = \hat{j}$。因此，流量为：
$$
Q = \iint_S \vec{V} \cdot \hat{j} \, dA = \iint_S v_y \, dA
$$
由于流动是均匀的，$v_y = -V_0 \sin\theta$ 是一个常数。积分区域的面积是 $WH$。所以：
$$
Q = (-V_0 \sin\theta) (WH) = -V_0 WH \sin\theta
$$
这个简单的例子展示了如何从一个抽象的[速度场](@entry_id:271461)矢量得到一个可测量的宏观物理量。

### [湍流](@entry_id:151300)中的[速度场](@entry_id:271461)：[雷诺分解](@entry_id:267756)

在许多实际应用中，[流体运动](@entry_id:182721)并非平滑有序，而是呈现出混乱和无序的 **[湍流](@entry_id:151300) (turbulent flow)** 状态。直接描述[湍流](@entry_id:151300)中瞬时速度场的复杂变化是极其困难的。因此，我们通常采用一种统计方法，即 **[雷诺分解](@entry_id:267756) (Reynolds decomposition)**。

该方法将瞬时速度 $\vec{v}$ 分解为一个时间平均的 **[平均速度](@entry_id:267649) (mean velocity)** $\vec{V}$ 和一个脉动的 **脉动速度 (fluctuating velocity)** $\vec{v'}$：
$$
\vec{v}(\vec{x}, t) = \vec{V}(\vec{x}) + \vec{v'}(\vec{x}, t)
$$
其中，平均速度 $\vec{V} = \overline{\vec{v}}$，而脉动速度的平均值为零，$\overline{\vec{v'}} = 0$。

当我们将这个分解代入描述加速度的[非线性](@entry_id:637147)[对流](@entry_id:141806)项 $(\vec{v} \cdot \nabla)\vec{v}$ 并进行时间平均时，会出现一个深刻的结果。平均后的[对流加速度](@entry_id:263153)为：
$$
\overline{(\vec{v} \cdot \nabla)\vec{v}} = (\vec{V} \cdot \nabla)\vec{V} + \overline{(\vec{v'} \cdot \nabla)\vec{v'}}
$$
第一项是平均速度场的[对流加速度](@entry_id:263153)。第二项 $\overline{(\vec{v'} \cdot \nabla)\vec{v'}}$ 是一个新增的项，它代表了由速度脉动引起的平均[动量输运](@entry_id:139628)。这个项通常被移到方程的另一边，并被解释为一种附加的应力，称为 **[雷诺应力](@entry_id:263788) (Reynolds stress)**。它不是由分子黏性产生的真实应力，而是[湍流](@entry_id:151300)脉动对平均流动宏观效应的数学体现。

考虑一个简化的[二维湍流](@entry_id:198015)模型，其脉动速度分量为 $v'_x = a \cos(ky) \sin(\omega t)$ 和 $v'_y = b \sin(ky) \sin(\omega t + \phi)$ [@problem_id:1805640]。我们可以计算[雷诺应力](@entry_id:263788)项对[平均加速度](@entry_id:163219)的贡献。例如，其 $x$ 分量为：
$$
(\vec{a}_{\text{turb}})_x = \overline{v'_x \frac{\partial v'_x}{\partial x} + v'_y \frac{\partial v'_x}{\partial y}} = \overline{v'_y \frac{\partial v'_x}{\partial y}}
$$
经过计算和[时间平均](@entry_id:267915)，可以发现即使每个脉动分量的平均值为零，它们的乘积的平均值却可以不为零。最终结果显示，脉动间的相关性（由相位差 $\phi$ 体现）能够对平均流动产生持续的、非零的加速效应。这揭示了[湍流](@entry_id:151300)的核心机制之一：脉动运动可以通过[非线性](@entry_id:637147)效应系统地改变平均流动的行为。