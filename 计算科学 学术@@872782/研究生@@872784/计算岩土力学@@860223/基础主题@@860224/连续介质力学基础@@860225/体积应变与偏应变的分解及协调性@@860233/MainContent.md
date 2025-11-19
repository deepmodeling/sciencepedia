## 引言
在计算岩[土力学](@entry_id:180264)和连续介质力学领域，精确描述和预测材料在荷载作用下的变形是核心挑战。任何复杂的变形过程，本质上都可以被理解为体积改变与形状改变的组合。将[应变张量分解](@entry_id:184653)为控制体积的“体量”部分和控制形状畸变的“偏量”部分，为我们提供了一个强大而直观的分析框架。然而，仅仅定义一个应变场并不足够，我们还必须确保它是物理上可实现的，即它必须满足“[运动学](@entry_id:173318)相容性”条件，保证能够由一个连续的位移场导出而不会在材料内部产生不合理的裂缝或重叠。本文旨在系统性地阐明[应变分解](@entry_id:186005)与相容性这两大基石性概念，并揭示它们在理论与实践中的深刻联系。

本文将通过三个章节逐步展开。在“原理与机制”一章中，我们将深入探讨无穷小及[有限应变理论](@entry_id:176941)下的体量-偏量分解方法，并详细阐释保证变形物理一致性的圣维南相容性条件。接着，在“应用与跨学科联系”一章中，我们将展示这些原理如何在岩土材料[本构模型](@entry_id:174726)、有限元数值模拟（如[体积锁定](@entry_id:172606)问题）以及[多孔介质力学](@entry_id:171662)等领域发挥关键作用。最后，“动手实践”部分将通过具体的计算练习，帮助读者巩固理论知识，并将其应用于解决实际问题。通过本文的学习，读者将能够深刻理解变形的内在结构，并掌握分析复杂力学问题的关键工具。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，理解材料的变形是核心任务。变形通常可以分解为两个基本部分：体积的改变和形状的改变。这种分解对于[本构模型](@entry_id:174726)的建立、数值模拟的实施以及实验数据的分析都至关重要。此外，任何假设的变形场都必须满足[运动学](@entry_id:173318)上的相容性，以确保其在物理上是可能实现的，即它可以由一个连续的[位移场](@entry_id:141476)产生。本章将深入探讨应变张量的体量-偏量分解原理，并阐释保证物理一致性的相容性条件的核心机制。

### [无穷小应变](@entry_id:197162)理论中的分解

对于大多数工程应用，尤其是在岩土力学中处理加载下的土体和岩体时，[无穷小应变](@entry_id:197162)理论提供了一个足够精确且数学上更易于处理的框架。

#### [小应变张量](@entry_id:754968)及其物理意义

当一个连续体发生变形时，其内部各点的位移可以用一个连续的[位移矢量场](@entry_id:196067) $\boldsymbol{u}(\boldsymbol{x})$ 来描述。在无穷小变形的假设下，[位移梯度](@entry_id:165352) $\nabla \boldsymbol{u}$（其分量为 $u_{i,j} = \partial u_i / \partial x_j$）很小。**[小应变张量](@entry_id:754968)**（或称柯西应变张量）$\boldsymbol{\varepsilon}$ 定义为[位移梯度](@entry_id:165352)的对称部分：

$$
\varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})
$$

这个张量之所以是对称的，因为它描述了材料纤维长度的真实变化。[位移梯度](@entry_id:165352)可以分解为一个对称部分（应变张量 $\boldsymbol{\varepsilon}$）和一个反对称部分（[刚体转动](@entry_id:191086)张量 $\boldsymbol{\omega}$）。通过分析一根无穷小材料纤维长度的平方变化，可以证明，只有对称部分 $\boldsymbol{\varepsilon}$ 对长度的一阶变化有贡献。反对称部分 $\boldsymbol{\omega}$ 代表了无穷小的[刚体转动](@entry_id:191086)，它在[一阶近似](@entry_id:147559)下不改变材料纤维的长度或它们之间的夹角 [@problem_id:3570319]。因此，$\boldsymbol{\varepsilon}$ 精确地捕捉了材料的“变形”或“应变”，而不包含刚体运动。

#### 体积应变：量化体积变化

[应变张量](@entry_id:193332)最直接的物理量之一是它的迹，它量化了材料微元的局部体积变化。**[体积应变](@entry_id:267252)** $\varepsilon_v$ 定义为[应变张量](@entry_id:193332)的迹：

$$
\varepsilon_v = \operatorname{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{kk} = \varepsilon_{11} + \varepsilon_{22} + \varepsilon_{33}
$$

在[无穷小应变](@entry_id:197162)理论中，$\varepsilon_v$ 等于[位移场](@entry_id:141476) $\boldsymbol{u}$ 的散度，即 $\varepsilon_v = \nabla \cdot \boldsymbol{u}$。我们可以通过考虑一个初始体积为 $V_0$ 的无穷小立方体来理解其物理意义。变形后，其体积变为 $V$。体积比 $V/V_0$ 由变形梯度 $\boldsymbol{F} = \boldsymbol{I} + \nabla\boldsymbol{u}$ 的[行列式](@entry_id:142978) $J = \det(\boldsymbol{F})$ 给出。对于小梯度，[行列式](@entry_id:142978)可以线性化为 $J \approx 1 + \operatorname{tr}(\nabla\boldsymbol{u})$。由于 $\operatorname{tr}(\boldsymbol{\varepsilon}) = \operatorname{tr}(\nabla\boldsymbol{u})$，相对体积变化的[一阶近似](@entry_id:147559)为 [@problem_id:3570319]：

$$
\frac{V - V_0}{V_0} = J - 1 \approx \operatorname{tr}(\boldsymbol{\varepsilon}) = \varepsilon_v
$$

正的[体积应变](@entry_id:267252) ($\varepsilon_v > 0$) 表示体积膨胀（剪胀），而负的体积应变 ($\varepsilon_v  0$) 表示体积压缩（固结或压实）。这是岩[土力学](@entry_id:180264)中模拟[地基沉降](@entry_id:755031)、土体固结和剪切过程中[颗粒材料](@entry_id:750005)剪胀等现象的基础。

#### [偏应变](@entry_id:201263)：量化形状变化

一旦我们分离出与体积变化相关的部分，剩下的就是纯粹的形状变化或畸变。这是通过将应变张量 $\boldsymbol{\varepsilon}$ 分解为一个球量[部分和](@entry_id:162077)一个偏量部分来实现的。**偏[应变张量](@entry_id:193332)** $\boldsymbol{\varepsilon}'$（或 $\boldsymbol{e}$）定义为总应变张量减去其球量部分：

$$
\boldsymbol{\varepsilon}' = \boldsymbol{\varepsilon} - \frac{1}{3}\varepsilon_v \boldsymbol{I}
$$

其中 $\boldsymbol{I}$ 是二阶单位张量。球量部分 $\frac{1}{3}\varepsilon_v \boldsymbol{I}$ 代表各向同性的体积变化，因为它在所有方向上都施加了相等的[法向应变](@entry_id:204633)，而没有剪切。偏[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}'$ 的一个关键性质是它的迹为零：

$$
\operatorname{tr}(\boldsymbol{\varepsilon}') = \operatorname{tr}\left(\boldsymbol{\varepsilon} - \frac{1}{3}\varepsilon_v \boldsymbol{I}\right) = \operatorname{tr}(\boldsymbol{\varepsilon}) - \frac{1}{3}\varepsilon_v \operatorname{tr}(\boldsymbol{I}) = \varepsilon_v - \frac{1}{3}\varepsilon_v (3) = 0
$$

迹为零意味着[偏应变](@entry_id:201263)描述的是一种**等体积**（isochoric）变形。它代表了材料微元在保持体积不变的情况下的拉伸、压缩和剪切，从而导致其形状发生改变。在岩[土力学](@entry_id:180264)中，[偏应变](@entry_id:201263)与剪切破坏密切相关。描述不可恢复变形和破坏的塑性模型，通常在偏应力与偏[应变[不变](@entry_id:190518)量](@entry_id:148850)构成的空间中定义其屈服面和流动法则 [@problem_id:3570306]。

#### 分解示例

为了具体说明这种分解，考虑一个均匀材料单元，其应变状态由以下恒定[应变张量](@entry_id:193332)描述 [@problem_id:3570384]：

$$
\boldsymbol{\varepsilon} = \begin{pmatrix} 0.02  0  0 \\ 0  0.01  0 \\ 0  0  -0.01 \end{pmatrix}
$$

首先，我们计算体积应变：

$$
\varepsilon_v = \operatorname{tr}(\boldsymbol{\varepsilon}) = 0.02 + 0.01 + (-0.01) = 0.02
$$

这个正值表示材料发生了 $2\%$ 的体积膨胀。

接下来，我们计算偏应变张量 $\boldsymbol{\varepsilon}' = \boldsymbol{\varepsilon} - \frac{1}{3}\varepsilon_v \boldsymbol{I}$：

$$
\varepsilon'_{11} = 0.02 - \frac{1}{3}(0.02) = \frac{0.04}{3}
$$
$$
\varepsilon'_{22} = 0.01 - \frac{1}{3}(0.02) = \frac{0.01}{3}
$$
$$
\varepsilon'_{33} = -0.01 - \frac{1}{3}(0.02) = -\frac{0.05}{3}
$$

非对角线分量保持为零。因此，偏[应变张量](@entry_id:193332)为：

$$
\boldsymbol{\varepsilon}' = \begin{pmatrix} 0.04/3  0  0 \\ 0  0.01/3  0 \\ 0  0  -0.05/3 \end{pmatrix}
$$

我们可以验证其迹确实为零：$\frac{0.04}{3} + \frac{0.01}{3} - \frac{0.05}{3} = 0$。

这个分解揭示了总变形是由一个 $2\%$ 的均匀[体积膨胀](@entry_id:144241)和一个改变单元形状的畸变叠加而成的。我们可以通过比较两部分的大小来评估哪种效应对总变形的贡献更大。例如，使用[弗罗贝尼乌斯范数](@entry_id:143384)（Frobenius norm）$\|\cdot\|_F$ 作为张量大小的度量，可以定义一个“优势指数”$D = \|\boldsymbol{\varepsilon}'\|_F / |\varepsilon_v|$。对于这个例子，$D \approx 1.080$，表明在此特定变形中，形状改变（[偏应变](@entry_id:201263)）的贡献略大于体积改变的贡献 [@problem_id:3570384]。

### 运动学相容性：确保物理真实性

仅仅指定一个对称的二阶张量场 $\boldsymbol{\varepsilon}(\boldsymbol{x})$ 并不足以保证它是一个物理上可能的应变场。**[运动学](@entry_id:173318)相容性**要求这个应变场能够通过 $\varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})$ 从一个单值、连续的位移场 $\boldsymbol{u}(\boldsymbol{x})$ 中导出。

#### 相容性的概念与圣维南条件

为什么需要相容性？因为位移场 $\boldsymbol{u}$ 只有3个分量，而对称的[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 有6个独立分量。这构成了一个超定[偏微分方程组](@entry_id:172573)。这样的[方程组](@entry_id:193238)只有在其系数（即应变分量）满足特定的可积性条件时才有解。这些条件就是**圣维南相容性条件**。

对称性是必要条件，但远非充分条件。例如，考虑一个二维应变场 $\varepsilon_{11} = c x_2^2$（$c$为非零常数），所有其他分量为零。这个场是光滑且对称的，但它违反了[相容性条件](@entry_id:637057)，因此无法由任何连续位移场产生。试图在连续体中实现这种应变场，将不可避免地导致材料内部出现裂缝或重叠 [@problem_id:3570319]。

对于三维问题，存在六个独立的、非平凡的圣维南相容性方程。这些方程涉及应变分量的[二阶偏导数](@entry_id:635213)，可以用一个紧凑的符号形式表示 [@problem_id:3570319]：

$$
\operatorname{inc}(\boldsymbol{\varepsilon}) \equiv \operatorname{curl}(\operatorname{curl}(\boldsymbol{\varepsilon})) = \boldsymbol{0}
$$

这里的 $\operatorname{inc}(\boldsymbol{\varepsilon})$ 称为**不相容张量**。

#### 区域拓扑与边界条件的角色

圣维南相容性条件的重要性与所考虑的物理域的拓扑性质密切相关。

-   对于**单连通域**（即没有任何“洞”的区域），圣维南条件 $\operatorname{inc}(\boldsymbol{\varepsilon}) = \boldsymbol{0}$ 是应变场相容的**充分必要条件**。如果满足这些条件，那么一定存在一个单值的位移场 $\boldsymbol{u}$（在刚体运动的意义下是唯一的）。通过施加适当的边界条件（例如，在边界的某个部分固定位移），可以完全确定这个唯一的位移场 [@problem_id:3570383]。

-   对于**[多连通域](@entry_id:185277)**（例如，带孔的板或[环形体](@entry_id:263065)），圣维南条件仍然是必要的，但不再是充分的。即使 $\operatorname{inc}(\boldsymbol{\varepsilon}) = \boldsymbol{0}$ 处处成立，在围绕“洞”的闭合路径上积分位移增量也可能得到一个非零结果。这对应于**[位错](@entry_id:157482)**，即位移场是多值的。在这种情况下，需要额外的全局积分条件来保证位移场的[单值性](@entry_id:174849) [@problem_id:3570383]。

#### 相容性的实践检验与分解

除了检验微分形式的圣维南方程，我们还可以通过直接积分来检验相容性并构造[位移场](@entry_id:141476)。给定一个应变场 $\boldsymbol{\varepsilon}(\boldsymbol{x})$，我们可以通[过积分](@entry_id:753033)[法向应变](@entry_id:204633)分量来开始，例如：
$u_x(x,y,z) = \int \varepsilon_{xx} \, dx + f(y,z)$。然后，利用[剪应变](@entry_id:175241)的关系式来逐步确定积分函数 $f(y,z)$ 等。如果这个过程能够无矛盾地完成，就证明了应变场是相容的，并且我们同时找到了对应的位移场。对于一个给定的线性应变场，这个过程可以明确地展示其相容性 [@problem_id:3570306]。

[相容性条件](@entry_id:637057)与应变的体量-偏量分解之间存在着深刻的联系。由于不相容算子 $\operatorname{inc}(\cdot)$ 是线性的，我们可以将其应用于分解后的应变：
$\operatorname{inc}(\boldsymbol{\varepsilon}) = \operatorname{inc}(\boldsymbol{\varepsilon}') + \operatorname{inc}(\frac{1}{3}\varepsilon_v \boldsymbol{I})$。
因此，总应变的相容性取决于其偏量[部分和](@entry_id:162077)球量部分的相容性的总和。

可以证明，一个纯球量应变场 $\phi\boldsymbol{I}$ 是相容的，当且仅当其[势函数](@entry_id:176105) $\phi$ 是一个**[仿射函数](@entry_id:635019)**（即空间坐标的线性函数加一个常数）[@problem_id:3570383]。这意味着，对于一个体量应变 $\varepsilon_v$，只有当它在空间中呈线性[分布](@entry_id:182848)时，对应的球量应变部分才是自身相容的。

这个结论引出了一个强大的叠加原理：如果一个应变场的偏量部分 $\boldsymbol{\varepsilon}'$ 满足[相容性条件](@entry_id:637057)（$\operatorname{inc}(\boldsymbol{\varepsilon}') = \boldsymbol{0}$），并且其体积应变 $\varepsilon_v$ 是一个[仿射函数](@entry_id:635019)，那么整个应变场 $\boldsymbol{\varepsilon}$ 就是相容的 [@problem_id:3570383]。

更一般地，体量应变和偏量应变的空间变化必须协同作用才能满足相容性。在二维[平面应变](@entry_id:167046)问题中，这表现为一个优美的关系式 [@problem_id:3570352] [@problem_id:3570367]：

$$
\Delta \varepsilon_v = - 3 \left( \frac{\partial^2 \varepsilon'_{xx}}{\partial y^2} + \frac{\partial^2 \varepsilon'_{yy}}{\partial x^2} - 2 \frac{\partial^2 \varepsilon'_{xy}}{\partial x \partial y} \right)
$$

其中 $\Delta$ 是拉普拉斯算子。这个方程清楚地表明，[体积应变](@entry_id:267252)的拉普拉斯值（衡量其与调和函数的偏差）必须由[偏应变](@entry_id:201263)分量的特定[二阶导数](@entry_id:144508)组合来精确平衡。例如，如果一个非调和的体积应变场（例如 $\varepsilon_v = \varepsilon_0 \cos(kx)$，其拉普拉斯值为非零）被指定，那么为了保持相容性，材料内部必须同时存在一个与之协调的、特定的[偏应变](@entry_id:201263)场 [@problem_id:3570367]。

### [有限应变理论](@entry_id:176941)中的扩展

当变形不再是无穷小时，需要使用[有限应变理论](@entry_id:176941)。此时，应变的加法分解和线性[相容性条件](@entry_id:637057)变得不再适用，但体量-偏量分解的核心思想得以保留和发展。

#### [乘法分解](@entry_id:199514)

在有限变形中，变形由**变形梯度** $\boldsymbol{F}$ 描述。其[行列式](@entry_id:142978) $J = \det(\boldsymbol{F})$ 仍然代表局部体积比 $dV/dV_0$ [@problem_id:3570308]。一个核心思想是将变形在乘法意义上分解为一个体积改变部分和一个形状改变部分。一种常见的分解是：

$$
\boldsymbol{F} = \boldsymbol{F}_{\text{vol}} \boldsymbol{F}_{\text{dev}} = (J^{1/3}\boldsymbol{I}) \bar{\boldsymbol{F}}
$$

在这里，$\boldsymbol{F}_{\text{vol}} = J^{1/3}\boldsymbol{I}$ 代表一个纯粹的、各向同性的[体积膨胀](@entry_id:144241)或收缩。$\boldsymbol{F}_{\text{dev}} = \bar{\boldsymbol{F}} = J^{-1/3}\boldsymbol{F}$ 被称为**等体积变形梯度**，它描述了保持体积不变的形状改变和旋转，其[行列式](@entry_id:142978)恒为1 [@problem_id:3570308]。

#### [对数应变](@entry_id:751438)的加法分解

尽管变形梯度的分解是乘法形式的，但通过引入**[对数应变](@entry_id:751438)**（或称[Hencky应变](@entry_id:191329)），我们可以在有限应变框架下恢复一个精确的加法分解。[对数应变](@entry_id:751438)定义在右[拉伸张量](@entry_id:193200) $\boldsymbol{U}$（通过极分解 $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$ 得到）上：

$$
\boldsymbol{E} = \ln \boldsymbol{U}
$$

[对数应变](@entry_id:751438)张量 $\boldsymbol{E}$ 的一个杰出特性是，它的迹与体积比的对数直接相关 [@problem_id:3570345]：

$$
\operatorname{tr}(\boldsymbol{E}) = \ln(\det(\boldsymbol{U})) = \ln(J)
$$

这使得[对数应变](@entry_id:751438) $\boldsymbol{E}$ 能够像[小应变张量](@entry_id:754968)一样，被精确地、加法地分解为体量和偏量部分：

$$
\boldsymbol{E} = \boldsymbol{E}_{\text{dev}} + \boldsymbol{E}_{\text{vol}} \quad \text{其中} \quad \boldsymbol{E}_{\text{vol}} = \frac{1}{3}\operatorname{tr}(\boldsymbol{E})\boldsymbol{I} = \frac{1}{3}(\ln J)\boldsymbol{I}
$$

偏量[对数应变](@entry_id:751438) $\boldsymbol{E}_{\text{dev}} = \boldsymbol{E} - \boldsymbol{E}_{\text{vol}}$ 同样是无迹的，并且与总[对数应变](@entry_id:751438) $\boldsymbol{E}$ 以及[拉伸张量](@entry_id:193200) $\boldsymbol{U}$ 共享相同的主方向（它们是同轴的）[@problem_id:3570345]。这种优美的加法分解结构使[对数应变](@entry_id:751438)在建立[弹塑性](@entry_id:193198)[本构模型](@entry_id:174726)时极具吸[引力](@entry_id:175476)。然而，必须强调的是，小应变理论中的圣维南[相容性条件](@entry_id:637057) $\operatorname{curl}(\operatorname{curl}(\boldsymbol{E}))=\boldsymbol{0}$ **不适用于**有限[对数应变](@entry_id:751438) $\boldsymbol{E}$。有限变形的相容性条件要复杂得多，涉及到[黎曼曲率张量](@entry_id:160189)的概念 [@problem_id:3570345]。

### 在计算岩[土力学](@entry_id:180264)中的应用：不可压缩性与[体积锁定](@entry_id:172606)

体量-偏量分解和相容性的概念在有限元等数值方法中具有重要的实际意义，尤其是在处理[近不可压缩材料](@entry_id:752388)时。

#### [近不可压缩](@entry_id:752387)极限与[体积锁定](@entry_id:172606)

许多岩土材料（如饱和粘土）在不排水条件下表现出[近不可压缩](@entry_id:752387)的行为。在[线性弹性](@entry_id:166983)中，这对应于[泊松比](@entry_id:158876) $\nu \to 0.5$。此时，**[体积模量](@entry_id:160069)** $\kappa$ 趋于无穷大 ($\kappa \to \infty$) [@problem_id:3570320]。[应变能密度](@entry_id:200085)可以分解为偏量和体量部分：$\psi = \mu \|\boldsymbol{\varepsilon}'\|^2 + \frac{\kappa}{2} \varepsilon_v^2$。

从变分原理（[最小势能原理](@entry_id:173340)）来看，当 $\kappa \to \infty$ 时，为了保持总能量有限，体积应变 $\varepsilon_v$ 必须处处趋于零。这在连续介质层面施加了一个[运动学](@entry_id:173318)约束：$\nabla \cdot \boldsymbol{u} = 0$。

当使用标准的、基于位移的低阶有限元（如线性三角形或[四面体单元](@entry_id:168311)）来求解时，会遇到一个严重的数值问题，称为**[体积锁定](@entry_id:172606)**（volumetric locking）。其根本原因在于，这些单元的离散位移场无法轻易满足逐点（或逐单元）的零[体积应变](@entry_id:267252)约束。对于这些单元，离散[体积应变](@entry_id:267252) $\varepsilon_{v,h}$ 在每个单元内是常数。施加 $\varepsilon_{v,h} \approx 0$ 的约束会给系统引入过多的限制，其数量往往超过了可用的自由度。结果，系统为了满足这些过度的约束，被迫抑制所有变形，包括物理上应该发生的[偏应变](@entry_id:201263)（剪切）变形，导致计算结果表现出虚假的、过度的刚度 [@problem_id:3570320] [@problem_id:3570368]。

#### 混合公式与[LBB条件](@entry_id:746626)

解决[体积锁定](@entry_id:172606)的标准方法是采用**[混合有限元](@entry_id:178533)公式**。其核心思想是，不再将[不可压缩性](@entry_id:274914)视为一个必须强加于[位移场](@entry_id:141476)的运动学约束，而是将其作为一个通过**[拉格朗日乘子](@entry_id:142696)**来弱施加的约束。这个拉格朗日乘子场在物理上可以被解释为**压力** $p$ [@problem_id:3570368]。

由此产生的 $u-p$ 混合公式将位移 $\boldsymbol{u}$ 和压力 $p$ 作为独立的求解变量。在不可压缩极限下，[应力张量](@entry_id:148973)变为 $\boldsymbol{\sigma} = 2G\boldsymbol{\varepsilon}' - p\boldsymbol{I}$，其中压力 $p$ 不再由[体积应变](@entry_id:267252)决定，而是一个独立的场变量，其作用是维持 $\nabla \cdot \boldsymbol{u} = 0$ 的约束。

然而，混合公式的成功与否取决于位移和压力离散空间（[插值函数](@entry_id:262791)）的明智选择。为了保证数值解的稳定性和收敛性，这两个空间必须满足一个关键的数学条件，即**Ladyzhenskaya-Babuška-Brezzi (LBB)** 条件（或称[inf-sup条件](@entry_id:746626)）。这个条件确保了压力自由度受到位移自由度的充分约束。如果选择的单元类型（例如，对位移和压力使用同阶[线性插值](@entry_id:137092)）违反了[LBB条件](@entry_id:746626)，数值解可能会出现非物理的、棋盘状的压力[振荡](@entry_id:267781)，或者仍然无法摆脱[体积锁定](@entry_id:172606) [@problem_id:3570320] [@problem_id:3570368]。因此，在计算岩土力学中，为不可压缩或[近不可压缩](@entry_id:752387)问题选择满足[LBB条件](@entry_id:746626)的稳定单元至关重要。