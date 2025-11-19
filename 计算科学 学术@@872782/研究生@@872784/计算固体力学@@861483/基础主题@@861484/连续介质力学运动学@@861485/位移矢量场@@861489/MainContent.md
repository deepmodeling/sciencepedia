## 引言
[位移矢量](@entry_id:262782)场是描述固体如何响应外力而移动和变形的基础物理量，是整个[计算固体力学](@entry_id:169583)大厦的基石。然而，从其抽象的数学定义到在复杂的、前沿的工程和科学问题中的具体应用，存在着一条充满挑战的概念鸿沟。许多学习者在掌握了基本定义后，仍然难以理解其在[有限元法](@entry_id:749389)、[非线性](@entry_id:637147)分析以及跨学科研究中的深层意义和实际操作。本文旨在系统地弥合这一鸿沟。

为此，本文将引导读者踏上一段从理论到实践的完整旅程。在第一章“原理与机制”中，我们将深入剖析[位移矢量](@entry_id:262782)场的数学本质，从[运动学](@entry_id:173318)描述到应变与转动的分解，再到求解弹性问题的严谨数学框架。接下来的第二章“应用与[交叉](@entry_id:147634)学科联系”将视野扩展到实际应用，展示位移场如何在断裂力学、接触问题、多物理场耦合以及医学成像等前沿领域扮演核心角色。最后，第三章“动手实践”将理论付诸于行，通过一系列精心设计的计算练习，让读者亲手解决从变形梯度计算到有限元[方法验证](@entry_id:153496)的经典问题，从而巩固和深化理解。

通过这三章的学习，读者不仅能建立对[位移矢量](@entry_id:262782)场的坚实理论基础，更能掌握其在现代计算模拟和科学研究中的强大应用能力，为解决更复杂的力学问题做好准备。

## 原理与机制

本章深入探讨[位移矢量](@entry_id:262782)场的核心原理与机制。作为描述连续体变形的关键物理量，[位移矢量](@entry_id:262782)场不仅是[运动学](@entry_id:173318)的基石，也是连接材料本构关系与外部载荷、最终形成可解力学问题的桥梁。我们将从位移的基本定义出发，剖析其在不同[坐标系](@entry_id:156346)下的描述方法，进而研究其梯度所蕴含的局部变形信息，包括应变与转动。随后，我们将建立求解弹性问题的数学框架，阐明其解的存在性、唯一性以及对[函数空间](@entry_id:143478)的要求。最后，我们将讨论在高级计算模拟中出现的具体挑战，如大转动和不可压缩性问题，并介绍相应的解决方案。

### 描述运动：物质视角与空间视角

在[连续介质力学](@entry_id:155125)中，一个物体的运动是通过一个参考构型 $\mathcal{B}_{0}$ 到当前构型 $\mathcal{B}_{t}$ 的映射来描述的。参考构型是物体在初始时刻（通常为 $t=0$）占据的空间区域，而当前构型是物体在时刻 $t$ 占据的区域。

为了精确地描述变形，我们引入两种[坐标系](@entry_id:156346)。**物质坐标**（或称**拉格朗日坐标**），用大写字母 $\mathbf{X}$ 表示，它如同一个永久的“标签”，唯一地标识了物体中的一个物质点。无论物体如何运动和变形，一个物质点的 $\mathbf{X}$ 保持不变。该物[质点](@entry_id:186768)在参考构型中的位置就是 $\mathbf{X}$。在时刻 $t$，该物[质点](@entry_id:186768)运动到了空间中的新位置，我们用**空间坐标**（或称**欧拉坐标**）$\mathbf{x}$ 来表示。

运动本身可以被描述为一个映射 $\boldsymbol{\varphi}$，它告诉我们每个物[质点](@entry_id:186768) $\mathbf{X}$ 在时刻 $t$ 的空间位置：
$$
\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)
$$
基于此，**[位移矢量](@entry_id:262782)**被定义为连接一个物质点在参考构型和当前构型中位置的矢量。对于由 $\mathbf{X}$ 标识的物[质点](@entry_id:186768)，其[位移矢量](@entry_id:262782)为 $\mathbf{x} - \mathbf{X}$。

描述位移场的方式取决于我们选择的自变量。这导致了两种等价但形式不同的观点：

1.  **物质描述（[拉格朗日描述](@entry_id:264498)）**：在此描述中，我们关注的是“每一个物质点发生了什么”。物理量被表示为物质坐标 $\mathbf{X}$ 和时间 $t$ 的函数。因此，[位移矢量](@entry_id:262782)场是一个映射 $\mathbf{u}: \mathcal{B}_{0} \times [0, T] \to \mathbb{R}^{d}$，其定义为：
    $$
    \mathbf{u}(\mathbf{X}, t) = \boldsymbol{\varphi}(\mathbf{X}, t) - \mathbf{X}
    $$
    这里，$\mathbf{u}(\mathbf{X}, t)$ 明确地给出了物质点 $\mathbf{X}$ 在时刻 $t$ 的位移。[@problem_id:3559237]

2.  **空间描述（[欧拉描述](@entry_id:264722)）**：在此描述中，我们关注的是“空间中每一个位置正在发生什么”。物理量被表示为空间坐标 $\mathbf{x}$ 和时间 $t$ 的函数。为了得到在特定空间位置 $\mathbf{x}$ 的位移，我们首先需要知道是哪个物[质点](@entry_id:186768)在时刻 $t$ 占据了该位置。这需要运动映射 $\boldsymbol{\varphi}$ 是可逆的，即存在一个逆映射 $\boldsymbol{\chi} = \boldsymbol{\varphi}^{-1}$，使得 $\mathbf{X} = \boldsymbol{\chi}(\mathbf{x}, t)$。这个逆映射告诉我们当前位于 $\mathbf{x}$ 的物质点其最初的参考坐标是什么。因此，该物质点的位移是其当前位置 $\mathbf{x}$ 减去其[参考位](@entry_id:754187)置 $\boldsymbol{\chi}(\mathbf{x}, t)$。空间位移场（有时用不同符号如 $\hat{\mathbf{u}}$ 或 $\mathbf{w}$ 表示以作区分）是一个定义在当前构型 $\mathcal{B}_{t}$ 上的映射：
    $$
    \hat{\mathbf{u}}(\mathbf{x}, t) = \mathbf{x} - \boldsymbol{\chi}(\mathbf{x}, t)
    $$
    [@problem_id:3559237] [@problem_id:3559242]

这两种描述是相通的，它们通过运动映射相关联：$\mathbf{u}(\mathbf{X}, t) = \hat{\mathbf{u}}(\boldsymbol{\varphi}(\mathbf{X}, t), t)$。在函数表达式中，严格区分[自变量](@entry_id:267118)是至关重要的；将 $\mathbf{x}$ 和 $\mathbf{X}$ 视为可互换的变量是一个常见的概念性错误。[@problem_id:3559237]

### [位移梯度](@entry_id:165352)：局部变形的度量

位移场本身描述了物体的整体移动，但其**梯度**则揭示了关于材料局部变形（即拉伸、剪切和转动）的丰富信息。

#### 变形梯度与[位移梯度](@entry_id:165352)的关系

**变形梯度张量** $\mathbf{F}$ 定义为运动映射 $\boldsymbol{\varphi}$ 对物质坐标 $\mathbf{X}$ 的梯度，它描述了一个无穷小的物质[线元](@entry_id:196833) $d\mathbf{X}$ 如何映射到当前构型中的线元 $d\mathbf{x}$：
$$
d\mathbf{x} = \mathbf{F} \, d\mathbf{X} \quad \text{其中} \quad \mathbf{F}(\mathbf{X}, t) = \frac{\partial \boldsymbol{\varphi}(\mathbf{X}, t)}{\partial \mathbf{X}} = \nabla_{\mathbf{X}} \boldsymbol{\varphi}
$$
由于 $\boldsymbol{\varphi}(\mathbf{X}, t) = \mathbf{X} + \mathbf{u}(\mathbf{X}, t)$，我们可以立即得到变形梯度与**[位移梯度](@entry_id:165352)** $\nabla_{\mathbf{X}} \mathbf{u}$ 之间的关系：
$$
\mathbf{F} = \frac{\partial (\mathbf{X} + \mathbf{u})}{\partial \mathbf{X}} = \frac{\partial \mathbf{X}}{\partial \mathbf{X}} + \frac{\partial \mathbf{u}}{\partial \mathbf{X}} = \mathbf{I} + \nabla_{\mathbf{X}} \mathbf{u}
$$
其中 $\mathbf{I}$ 是二阶单位张量。这个关系是有限变形理论的基础。一个常见的误解是认为 $\mathbf{F}$ 和 $\nabla_{\mathbf{X}} \mathbf{u}$ 相等，这是不正确的，因为 $\mathbf{X}$ 本身是自变量，其对自身的梯度为 $\mathbf{I}$，而非零。[@problem_id:3559237]

#### [小变形理论](@entry_id:174991)：应变与转动的分解

在许多工程应用中，变形很小，即[位移梯度](@entry_id:165352) $\mathbf{H} = \nabla_{\mathbf{X}} \mathbf{u}$ 的范数远小于1（$\|\mathbf{H}\| \ll 1$）。在这种**小变形**或**小应变**假设下，我们可以对[运动学](@entry_id:173318)进行线性化，从而极大地简化问题。

任何[二阶张量](@entry_id:199780) $\mathbf{H}$ 都可以唯一地分解为其**对称部分**和**反对称部分**：
$$
\mathbf{H} = \boldsymbol{\varepsilon} + \boldsymbol{\Omega}
$$
其中：
-   **[无穷小应变张量](@entry_id:167211)**（对称部分）：$\boldsymbol{\varepsilon} = \frac{1}{2}(\mathbf{H} + \mathbf{H}^{\top}) = \frac{1}{2}(\nabla_{\mathbf{X}}\mathbf{u} + (\nabla_{\mathbf{X}}\mathbf{u})^{\top})$
-   **无穷小转动张量**（反对称部分）：$\boldsymbol{\Omega} = \frac{1}{2}(\mathbf{H} - \mathbf{H}^{\top}) = \frac{1}{2}(\nabla_{\mathbf{X}}\mathbf{u} - (\nabla_{\mathbf{X}}\mathbf{u})^{\top})$

这种分解具有深刻的物理意义。[@problem_id:3559244]

**[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$** 描述了材料的纯变形，即形状和尺寸的变化。一个物质线元 $d\mathbf{X}$ 的长度平方变化 $\delta(\|d\mathbf{x}\|^2)$ 在[一阶近似](@entry_id:147559)下完全由应变张量决定：
$$
\delta(\|d\mathbf{x}\|^2) = \|d\mathbf{x}\|^2 - \|d\mathbf{X}\|^2 \approx 2 \, d\mathbf{X}^{\top} \boldsymbol{\varepsilon} \, d\mathbf{X}
$$
这表明，反对称的转动部分 $\boldsymbol{\Omega}$ 在[一阶近似](@entry_id:147559)下对长度变化没有贡献。同样，局部体积的相对变化在[一阶近似](@entry_id:147559)下由[应变张量](@entry_id:193332)的迹（trace）给出：
$$
J - 1 = \det(\mathbf{F}) - 1 = \det(\mathbf{I} + \mathbf{H}) - 1 \approx \mathrm{tr}(\mathbf{H}) = \mathrm{tr}(\boldsymbol{\varepsilon})
$$
因为任何[反对称张量](@entry_id:199349)的迹都为零。[@problem_id:3559244]

**转动张量 $\boldsymbol{\Omega}$** 描述了材料的局部[刚体转动](@entry_id:191086)。在[小变形理论](@entry_id:174991)中，这种转动是无穷小的。任何三维[反对称张量](@entry_id:199349) $\boldsymbol{\Omega}$ 都与一个唯一的**[轴矢量](@entry_id:196296)** $\boldsymbol{\omega}$ 相关联，使得对于任意矢量 $\mathbf{v}$，都有 $\boldsymbol{\Omega}\mathbf{v} = \boldsymbol{\omega} \times \mathbf{v}$。这个轴矢量 $\boldsymbol{\omega}$ 代表了无穷小转动的[转轴](@entry_id:187094)和角度，它与[位移场](@entry_id:141476)的关系为：
$$
\boldsymbol{\omega} = \frac{1}{2} \nabla_{\mathbf{X}} \times \mathbf{u}
$$
即无穷小转动矢量是[位移场](@entry_id:141476)旋度的一半。[@problem_id:3559244] 这一关系在分析材料的局部[涡旋运动](@entry_id:198769)时非常有用。例如，给定一个位移场，如 $\mathbf{u} = (0.002YZ + 0.001X, -0.003XZ + 0.002Y^2, 0.004XY)^{\top}$，我们可以通过计算其偏导数并代入上述旋度公式，来求得空间中任意一点的无穷小转动矢量的大小和方向。[@problem_id:3559252]

需要强调的是，即使是纯[刚体转动](@entry_id:191086)，只要它不是无穷小，其位移场的梯度也会产生一个非零的对称部分，即线性化的应变张量 $\boldsymbol{\varepsilon}$ 不为零。这是因为线性应变张量无法精确描述有限转动，它错误地将转动的一部分解释为应变。只有在小转动假设下，$\boldsymbol{\varepsilon}$ 才能被视为纯应变的可靠度量。[@problem_id:3559244]

### 弹性问题的数学框架

从[位移场](@entry_id:141476)和应变场的定义，我们现在转向如何构建和求解一个完整的弹性力学问题。这需要引入[本构关系](@entry_id:186508)（如[胡克定律](@entry_id:149682) $\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon}$）和[平衡方程](@entry_id:172166)（$\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}$），并为这些[偏微分方程](@entry_id:141332)建立一个稳健的数学框架。

#### [弱形式](@entry_id:142897)与函数空间

直接求解强形式的[偏微分方程组](@entry_id:172573)通常很困难，尤其对于复杂的几何形状和边界条件。有限元方法（Finite Element Method, FEM）等数值技术依赖于问题的**[弱形式](@entry_id:142897)**或**[变分形式](@entry_id:166033)**。通过将[平衡方程](@entry_id:172166)乘以一个任意的、满足一定条件的**[虚位移](@entry_id:168781)场**（或称**[检验函数](@entry_id:166589)**）$\mathbf{v}$，并在整个求解域 $\Omega$ 上积分，然后利用[分部积分](@entry_id:136350)（[格林公式](@entry_id:173118)），我们可以将求解强形式的问题转化为求解一个等价的积分形式问题。

这个过程揭示了[位移场](@entry_id:141476) $\mathbf{u}$ 必须满足的内在数学要求。在弱[形式的积分](@entry_id:158607)中，会出现形如 $\int_{\Omega} \boldsymbol{\sigma}(\mathbf{u}) : \boldsymbol{\varepsilon}(\mathbf{v}) \, dV$ 的项，这一项代表了[内力](@entry_id:167605)所做的[虚功](@entry_id:176403)。系统的总[应变能](@entry_id:162699)与 $\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{u}) : \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{u}) \, dV$ 成正比。为了保证这个[能量积分](@entry_id:166228)为有限值，$\boldsymbol{\varepsilon}(\mathbf{u})$ 的分量必须是平方可积的。由于 $\boldsymbol{\varepsilon}(\mathbf{u})$ 包含 $\mathbf{u}$ 的[一阶导数](@entry_id:749425)，这意味着 $\mathbf{u}$ 本身及其（弱）一阶导数都必须是平方可积的。

满足这一条件的函数所构成的空间被称为**[索博列夫空间](@entry_id:141995) (Sobolev space)** $H^1(\Omega)$。对于矢量场 $\mathbf{u}$，其自然归属的[函数空间](@entry_id:143478)是 $[H^1(\Omega)]^d$。这个空间是线性弹性问题的“天然能量空间”。[@problem_id:3559300]

对于基于分片多项式的[协调有限元](@entry_id:170866)方法，为了保证近似解 $\mathbf{u}^h$ 属于全局的 $[H^1(\Omega)]^d$ 空间，它必须在单元边界上至少是连续的（即 $C^0$ 连续）。如果单元之间存在跳跃，其导数将在边界上产生狄拉克 $\delta$ 函数，导致[能量积分](@entry_id:166228)发散。因此，$C^0$ 连续性是协调位移有限元法的基本要求。[@problem_id:3559300]

#### 边界条件：本质与自然

在推导弱形式的分部积分过程中，边界积分项 $\oint_{\partial\Omega} (\boldsymbol{\sigma}\mathbf{n}) \cdot \mathbf{v} \, dS$ 会自然出现。如何处理这一项，揭示了两类边界条件的根本区别。[@problem_id:3559298]

-   **[本质边界条件](@entry_id:173524) (Essential Boundary Conditions)**：这类条件直接施加在解（即位移 $\mathbf{u}$）本身上，例如在边界的某一部分 $\Gamma_D$ 上规定 $\mathbf{u} = \mathbf{u}_D$。在[弱形式](@entry_id:142897)中，这类条件是通过限制**[试探函数](@entry_id:756165)空间**（解 $\mathbf{u}$ 所在的函数空间）和**检验函数空间**（[虚位移](@entry_id:168781) $\mathbf{v}$ 所在的函数空间）来“强加”的。具体来说，[试探函数](@entry_id:756165) $\mathbf{u}$ 必须在 $\Gamma_D$ 上满足给定的位移值，而检验函数 $\mathbf{v}$ 必须在 $\Gamma_D$ 上为零（因为在已知位移的地方不允许有[虚位移](@entry_id:168781)）。由于 $\mathbf{v}|_{\Gamma_D} = \mathbf{0}$，边界积分中相应于 $\Gamma_D$ 的部分自动消失。

-   **自然边界条件 (Natural Boundary Conditions)**：这类条件施加在解的导数相关的量上，在[线性弹性](@entry_id:166983)中即为面力 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$。例如，在边界的另一部分 $\Gamma_N$ 上规定 $\boldsymbol{\sigma}\mathbf{n} = \mathbf{t}$。这类条件是在推导弱形式后“自然”出现的。它们并不直接约束函数空间，而是通过将已知的面力 $\mathbf{t}$ 代入到[弱形式](@entry_id:142897)右端的边界积分项中来满足，即 $\int_{\Gamma_N} \mathbf{t} \cdot \mathbf{v} \, dS$。因此，它们是以积分的“弱”形式被满足的。[@problem_id:3559298] [@problem_id:3559312]

#### 解的[存在性与唯一性](@entry_id:263101)：Korn 不等式与相容性条件

一个数学模型是否适定（well-posed），取决于其解是否存在、是否唯一以及是否稳定。对于弹性力学问题，有两个关键的数学概念保证了其[适定性](@entry_id:148590)。

首先是 **Korn 不等式 (Korn's inequality)**。该不等式建立了位移的全梯度 $\nabla\mathbf{u}$ 和其对称部分 $\boldsymbol{\varepsilon}(\mathbf{u})$ 之间的深刻联系。其一个基本形式为：
$$
\|\nabla \mathbf{u}\|_{L^{2}(\Omega)} \leq C\big(\|\boldsymbol{\varepsilon}(\mathbf{u})\|_{L^{2}(\Omega)} + \|\mathbf{u}\|_{L^{2}(\Omega)}\big)
$$
其中 $C$ 是一个仅与区域 $\Omega$ 有关的常数。[@problem_id:3559259] 这个不等式的关键作用在于，它保证了只要应变为零，位移的全梯度也就（在某种意义上）为零。我们知道，产生零应变的位移场正是**刚体位移**（[平动](@entry_id:187700)和转动）。Korn 不等式意味着，一旦我们通过某些方式（例如，施加足够的本质边界条件，或在数学上排除刚体位移）控制了刚体位移，那么仅通过[应变能](@entry_id:162699)（依赖于 $\boldsymbol{\varepsilon}(\mathbf{u})$）就可以控制整个[位移梯度](@entry_id:165352)。这在线性弹性[弱形式](@entry_id:142897)的**[矫顽性](@entry_id:159399) (coercivity)** 证明中至关重要，从而保证了当刚体位移被约束后，弹性问题的解是唯一的。对于纯面力（纯 Neumann）问题，解在相差一个刚体位移的意义下是唯一的。[@problem_id:3559259]

其次是**[应变相容性](@entry_id:199659)条件 (Strain Compatibility Conditions)**。这涉及到另一个问题：任意给定一个二阶对称张量场 $\boldsymbol{\varepsilon}(\mathbf{x})$，它是否总能对应一个单值的位移场 $\mathbf{u}(\mathbf{x})$？答案是否定的。为了保证存在一个（在相差一个刚体位移的意义下）唯一的、单值的位移场，应变场必须满足一定的[微分](@entry_id:158718)约束，即**圣维南[相容性条件](@entry_id:637057) (Saint-Venant's compatibility conditions)**。在[指标记法](@entry_id:191923)中，这些条件可以写为：
$$
\varepsilon_{ij,kl} + \varepsilon_{kl,ij} - \varepsilon_{ik,jl} - \varepsilon_{jl,ik} = 0
$$
对于所有 $i,j,k,l \in \{1,2,3\}$。在**单连通 (simply connected)** 区域内，这些条件是应变场可积为单值位移场的充分必要条件。如果区域不是单连通的（例如，带孔的板），满足[相容性条件](@entry_id:637057)的应变场仍可能导致多值位移（这在[位错理论](@entry_id:160051)中非常重要）。[@problem_id:3559243]

### 高级[计算力学](@entry_id:174464)中的挑战与对策

在将上述理论应用于实际的[非线性](@entry_id:637147)或复杂材料的计算模拟时，位移场的处理会面临新的挑战。

#### 大转动问题与协同转动法

在**有限变形**理论中，特别是当物体经历大的[刚体转动](@entry_id:191086)时，采用简单的位移[增量更新](@entry_id:750602)会产生严重问题。考虑一个在总拉格朗日（Total Lagrangian, TL）框架下的有限元求解过程，其中位移是逐步累加的，$ \mathbf{u}_{k+1} = \mathbf{u}_{k} + \Delta\mathbf{u} $。即使每一步的增量都对应于一个纯[刚体转动](@entry_id:191086)，将这些增量线性相加所得到的总位移，在通过[非线性](@entry_id:637147)的[格林-拉格朗日应变](@entry_id:170427)公式 $ \mathbf{E} = \frac{1}{2}(\mathbf{F}^{\top}\mathbf{F} - \mathbf{I}) $ 计算时，会产生虚假的、非零的应变。[@problem_id:3559310]

这是因为有限转动是乘性的（[矩阵乘法](@entry_id:156035)），而非加性的。简单的位移累加等同于将变形梯度增量进行加法叠加，这破坏了[刚体转动](@entry_id:191086)对应的变形梯度必须是正交矩阵这一基本性质。这种虚假应变会导致系统产生错误的内力，使得模拟结果严重失真，甚至无法收敛。

一个有效的解决方案是**协同转动法 (corotational formulation)**。其核心思想是，在每一步计算中，通过对变形梯度 $\mathbf{F}$ 进行**极分解 (polar decomposition)**，$\mathbf{F} = \mathbf{R}\mathbf{U}$，将局部运动显式地分解为一个纯转动部分（旋转矩阵 $\mathbf{R}$）和一个纯拉伸部分（右[拉伸张量](@entry_id:193200) $\mathbf{U}$）。应变和应力在跟随物体转动的“协同转动[坐标系](@entry_id:156346)”中进行计算和更新，而局部坐标系的转动则通过[旋转矩阵](@entry_id:140302)的乘法进行累积更新（$ \mathbf{R}_{k+1} = \Delta\mathbf{R} \, \mathbf{R}_{k} $）。通过这种方式，大的[刚体转动](@entry_id:191086)被精确地处理，不会产生虚假应变，从而保证了[非线性](@entry_id:637147)求解的鲁棒性和准确性。[@problem_id:3559310]

#### [不可压缩性](@entry_id:274914)与[体积锁定](@entry_id:172606)

另一个经典的计算挑战出现在模拟**[近不可压缩材料](@entry_id:752388)**（如橡胶）或在[塑性流动](@entry_id:201346)中（[体积守恒](@entry_id:276587)）。这类材料的[体积模量](@entry_id:160069) $K$ 远大于剪切模量 $\mu$（$K \gg \mu$）。在纯位移格式的有限元中，[应变能](@entry_id:162699)中的体积项 $\frac{1}{2} K (\nabla \cdot \mathbf{u})^2$ 起到了一个巨大的惩罚作用。

当使用低阶有限元（如线性三角形或四面体）时，近似位移场 $\mathbf{u}^h$ 的散度 $\nabla \cdot \mathbf{u}^h$ 在每个单元内是常数。为了使巨大的惩罚项保持有限，数值解会试图在每个单元上强制满足 $\nabla \cdot \mathbf{u}^h \approx 0$。然而，对于低阶单元，满足这个约束所需的自由度非常有限，导致整个单元网格的变形能力被严重限制，几乎无法产生任何变形。这种现象称为**[体积锁定](@entry_id:172606) (volumetric locking)**，它会导致计算出的位移和应力远小于实际值，使得结果毫无意义。[@problem_id:3559312]

为了解决锁定问题，需要引入一种不直接依赖于位移的、独立的场来处理压力。这就是**[混合格式](@entry_id:167436) (mixed formulation)**。我们引入一个独立的压[力场](@entry_id:147325) $p$，它作为拉格朗日乘子来施加体积约束。通过建立一个包含位移 $\mathbf{u}$ 和压力 $p$ 的[混合变分原理](@entry_id:165106)，我们可以推导出如下的混合弱形式：寻找 $(\mathbf{u}, p)$ 对，使其对所有检验函数 $(\mathbf{v}, q)$ 满足：
$$
\int_{\Omega} 2\mu \, \mathrm{dev}(\boldsymbol{\varepsilon}(\mathbf{u})) : \mathrm{dev}(\boldsymbol{\varepsilon}(\mathbf{v})) \, dV - \int_{\Omega} p (\nabla \cdot \mathbf{v}) \, dV - \int_{\Omega} q (\nabla \cdot \mathbf{u}) \, dV - \int_{\Omega} \frac{1}{K} p q \, dV = L(\mathbf{v}, q)
$$
在这个 **u-p [混合格式](@entry_id:167436)**中，位移和压力采用独立的有限元插值。通过为 $\mathbf{u}$ 和 $p$ 选择满足特定数学相容性条件（即 LBB 或 [inf-sup 条件](@entry_id:174538)）的[插值函数](@entry_id:262791)空间，可以有效避免[体积锁定](@entry_id:172606)，从而获得对[近不可压缩材料](@entry_id:752388)行为的准确模拟。[@problem_id:3559312]