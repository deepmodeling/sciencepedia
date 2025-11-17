## 引言
在自然界与工程技术中，从搏动的心脏到[振动](@entry_id:267781)的机翼，流体与固体结构的相互作用无处不在。准确预测和分析这些[流固耦合](@entry_id:171183)（FSI）现象，对于科学发现和工程创新至关重要。所有FSI问题的核心，都归结于一个共同的挑战：如何精确描述流体与固体在共享交界面上的物理“对话”规则。

尽管FSI仿真技术已日益成熟，但对界面上[运动学](@entry_id:173318)与动力学条件的深刻理解仍是许多研究者和工程师面临的知识壁垒。这些看似简单的条件，其背后蕴含着深刻的物理[守恒定律](@entry_id:269268)，并在不同的计算策略和物理情境下呈现出复杂的形态。

本文旨在系统性地剖析这些核心[界面条件](@entry_id:750725)。在第一章“原理与机制”中，我们将深入探讨速度连续性与力平衡的基本数学表述及其物理内涵。随后的第二章“应用与跨学科联系”将展示这些原理如何作为通用语言，连接生物医学、航空航天、地球物理等多个学科领域。最后，在第三章“动手实践”中，我们将通过具体的计算练习，揭示[数值算法](@entry_id:752770)如何影响这些条件的实现及其稳定性。通过这一由理论到应用再到实践的完整学习路径，读者将能够牢固掌握FSI建[模的基](@entry_id:156416)石，为解决复杂的[多物理场耦合](@entry_id:171389)问题奠定坚实的基础。

## 原理与机制

在[流固耦合](@entry_id:171183)（Fluid-Structure Interaction, FSI）系统中，流体与固体在它们共享的交界面上相互作用。要准确地模拟这种相互作用，必须施加一组数学条件来描述交界面上的物理行为。这些条件源于基本的物理[守恒定律](@entry_id:269268)，主要分为两大类：**[运动学](@entry_id:173318)条件**，它规定了运动的连续性；以及**动力学条件**，它规定了力的平衡。本章将系统地阐述这些核心原理，并探讨它们在不同物理和计算情境下的具体机制。

### 基本[界面条件](@entry_id:750725)

FSI 问题的核心在于两种不同介质在移动边界上的耦合。这些耦合条件确保了模型在物理上的一致性。

#### 运动学相容性：无滑移与不可穿透条件

运动学条件描述了流体和固体在交界面上的运动关系。其核心思想是，对于一个不产生空隙或重叠的连续界面，流体和固体必须以一种相容的方式运动。

我们考虑一个流体域 $\Omega_f(t)$ 和一个固体域 $\Omega_s(t)$，它们共享一个随[时间演化](@entry_id:153943)的交界面 $\Gamma_{fs}(t)$。固体的运动通常在[拉格朗日框架](@entry_id:751113)中描述，其中固体材料点 $\mathbf{X}$ 在参考构型 $\Omega_{s,0}$ 中的位置通过映射 $\mathbf{x}=\boldsymbol{\varphi}_s(\mathbf{X},t)=\mathbf{X}+\mathbf{u}_s(\mathbf{X},t)$ 变为当前构型中的位置 $\mathbf{x}$。这里，$\mathbf{u}_s$ 是固体[位移场](@entry_id:141476)。因此，固体材料点的速度是其位移的[物质时间导数](@entry_id:190892)，记为 $\mathbf{v}_s = \dot{\mathbf{u}}_s(\mathbf{X},t)$。[流体运动](@entry_id:182721)通常在[欧拉框架](@entry_id:749109)中描述，其在空间点 $\mathbf{x}$ 的速度为 $\mathbf{v}_f(\mathbf{x},t)$。

在 FSI 中最常用的运动学条件是**[无滑移条件](@entry_id:275670) (no-slip condition)**。该条件假设流体粒子会“粘附”在固体表面上，并随之一起运动。这意味着在交界面上的任意一点，流体速度必须完[全等](@entry_id:273198)于固体速度 [@problem_id:3512125]：
$$
\mathbf{v}_f(\mathbf{x},t) = \mathbf{v}_s(\mathbf{x},t) = \dot{\mathbf{u}}_s(\mathbf{X},t), \quad \text{其中 } \mathbf{x} = \boldsymbol{\varphi}_s(\mathbf{X},t) \in \Gamma_{fs}(t)
$$
这个单一的矢量方程保证了流体和固体在界面法向和切向的速度分量都完全匹配。它适用于所有粘性流体，是大多数 FSI 应用的标准假设。

在某些特定情况下，例如模拟理想（无粘）流体时，无滑移条件可能过于严格。这时可以采用一个较弱的条件，即**不可穿透条件 (impermeability condition)**。该条件源于质量守恒，仅要求流体不能穿过固体边界。这通过规定流体相对于固体的速度在界面法向上的分量为零来实现。令 $\mathbf{n}(\mathbf{x},t)$ 为交界面上指向流体域的[单位法向量](@entry_id:178851)，则该条件可写为 [@problem_id:3512125]：
$$
(\mathbf{v}_f(\mathbf{x},t) - \mathbf{v}_s(\mathbf{x},t)) \cdot \mathbf{n}(\mathbf{x},t) = 0
$$
这个条件等价于要求法向速度连续，即 $\mathbf{v}_f \cdot \mathbf{n} = \mathbf{v}_s \cdot \mathbf{n}$。它允许流体在切向上相对于固体表面滑动，即 $(\mathbf{v}_f - \mathbf{v}_s)$ 的切向分量可以不为零。

#### [动力学平衡](@entry_id:187220)：[牵引力连续性](@entry_id:756091)

动力学条件描述了作用在交界面上的力的平衡。根据牛顿第三定律（作用力与[反作用](@entry_id:203910)力定律），如果交界面本身没有质量（即不考虑其惯性），那么流体作用在固体上的力必须等于并反向于固体作用在流体上的力。这些力通过**牵[引力](@entry_id:175476)矢量 (traction vector)** $\mathbf{t}$ 来量化，它表示单位面积上的力。

牵[引力](@entry_id:175476)矢量由柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 和作用面的[单位法向量](@entry_id:178851) $\mathbf{n}$ 决定，关系为 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$。为了精确表述力的平衡，我们需要仔细定义[法向量](@entry_id:264185)的指向。设 $\mathbf{n}_f$ 为流体域 $\Omega_f$ 在交界面 $\Gamma_{fs}$ 上的外[法线](@entry_id:167651)（指向固体），$\mathbf{n}_s$ 为固体域 $\Omega_s$ 在交界面上的外法线（指向流体）。显然，$\mathbf{n}_f = -\mathbf{n}_s$。

流体作用在固体上的牵[引力](@entry_id:175476)是 $\mathbf{t}_{f \to s}$，它作用在固体边界上，因此[法向量](@entry_id:264185)是 $\mathbf{n}_s$，应[力场](@entry_id:147325)是固体的 $\boldsymbol{\sigma}_s$。但是，根据柯西应力原理，这个牵[引力](@entry_id:175476)是由流体的应力状态决定的。更清晰的推导是考虑一个跨越界面的无限薄的“药盒”形控制体。根据动量守恒，当[控制体](@entry_id:143882)厚度趋于零时，作用在控制体两面的牵[引力](@entry_id:175476)之和必须为零（假设没有奇异的[界面力](@entry_id:184024)源）[@problem_id:3512148]。作用在流体侧表面（法向量为 $\mathbf{n}_f$）上的牵[引力](@entry_id:175476)为 $\boldsymbol{\sigma}_f \mathbf{n}_f$；作用在固体侧表面（法向量为 $\mathbf{n}_s$）上的牵[引力](@entry_id:175476)为 $\boldsymbol{\sigma}_s \mathbf{n}_s$。因此，力的平衡要求：
$$
\boldsymbol{\sigma}_f \mathbf{n}_f + \boldsymbol{\sigma}_s \mathbf{n}_s = \mathbf{0}
$$
考虑到 $\mathbf{n}_f = -\mathbf{n}_s$，上式可以写成更常见的形式，即**牵[引力](@entry_id:175476)连续条件 (continuity of traction)**：
$$
\boldsymbol{\sigma}_f \mathbf{n}_s = \boldsymbol{\sigma}_s \mathbf{n}_s
$$
如果我们定义一个统一的界[面法向量](@entry_id:749211) $\mathbf{n}$（例如，总是指向流体侧，即 $\mathbf{n} = \mathbf{n}_s$），那么条件简化为：
$$
\boldsymbol{\sigma}_f \mathbf{n} = \boldsymbol{\sigma}_s \mathbf{n}
$$
这个矢量方程确保了界面上法向和切向应力的平衡。它是连接流体压力、[粘性力](@entry_id:263294)和固体弹性力、[内应力](@entry_id:193721)的核心纽带。

### [界面条件](@entry_id:750725)的应用与诠释

抽象的原理需要通过具体的应用来深化理解。本节将通过一个实例计算，并深入探讨[不可压缩流](@entry_id:140301)中压力的特殊作用，来阐明这些条件的物理意义。

#### 一个示例：平面[剪切流](@entry_id:266817)

让我们考虑一个具体的例子来演示动力学条件的用法 [@problem_id:3512169]。假设一个不可压缩的[牛顿流体](@entry_id:263796)（位于 $y>0$）与一个线弹性固体（位于 $y0$）在 $y=0$ 平面接触。从固体指向流体的[单位法向量](@entry_id:178851)为 $\mathbf{n} = \mathbf{e}_y$。

流体的柯西[应力张量](@entry_id:148973)为 $\boldsymbol{\sigma}_f = -p\mathbf{I} + 2\mu\mathbf{D}_f$，其中 $p$ 是[流体静压](@entry_id:141627)，$\mu$ 是[动力粘度](@entry_id:268228)，$\mathbf{D}_f$ 是应变率张量。假设流体处于一个稳定的 Couette 型剪切流场中，速度为 $\mathbf{v}_f = \gamma y \mathbf{e}_x$，其中 $\gamma$ 是常数剪切率。通过计算可得，[流体应力](@entry_id:269919)张量为：
$$
\boldsymbol{\sigma}_f = \begin{pmatrix} -p  \mu\gamma  0 \\ \mu\gamma  -p  0 \\ 0  0  -p \end{pmatrix}
$$
固体的柯西应力张量为 $\boldsymbol{\sigma}_s = \lambda\,\mathrm{tr}(\boldsymbol{\varepsilon})\,\mathbf{I} + 2G\,\boldsymbol{\varepsilon}$，其中 $\lambda$ 和 $G$ 是拉梅参数，$\boldsymbol{\varepsilon}$ 是[小应变张量](@entry_id:754968)。

现在我们施加[动力学平衡](@entry_id:187220)条件 $\boldsymbol{\sigma}_f \mathbf{n} = \boldsymbol{\sigma}_s \mathbf{n}$。在 $y=0$ 界面处，$\mathbf{n} = (0, 1, 0)^{\mathsf{T}}$。
流体侧的牵[引力](@entry_id:175476)为：
$$
\mathbf{t}_f = \boldsymbol{\sigma}_f \mathbf{n} = \begin{pmatrix} -p  \mu\gamma  0 \\ \mu\gamma  -p  0 \\ 0  0  -p \end{pmatrix} \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix} = \begin{pmatrix} \mu\gamma \\ -p \\ 0 \end{pmatrix}
$$
固体侧的牵[引力](@entry_id:175476)为：
$$
\mathbf{t}_s = \boldsymbol{\sigma}_s \mathbf{n} = \begin{pmatrix} \sigma_{s,xx}  \sigma_{s,xy}  \sigma_{s,xz} \\ \sigma_{s,yx}  \sigma_{s,yy}  \sigma_{s,yz} \\ \sigma_{s,zx}  \sigma_{s,zy}  \sigma_{s,zz} \end{pmatrix} \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix} = \begin{pmatrix} \sigma_{s,xy} \\ \sigma_{s,yy} \\ \sigma_{s,zy} \end{pmatrix} = \begin{pmatrix} 2G\varepsilon_{xy} \\ \lambda \mathrm{tr}(\boldsymbol{\varepsilon}) + 2G\varepsilon_{yy} \\ 2G\varepsilon_{zy} \end{pmatrix}
$$
令 $\mathbf{t}_f = \mathbf{t}_s$，我们得到三个标量方程：
1.  $x$ 方向（切向）：$\mu\gamma = 2G\varepsilon_{xy}$
2.  $y$ 方向（法向）：$-p = \lambda \mathrm{tr}(\boldsymbol{\varepsilon}) + 2G\varepsilon_{yy}$
3.  $z$ 方向（切向）：$0 = 2G\varepsilon_{zy}$

从第二个方程，我们可以求解出界面上的流体压力 $p$ [@problem_id:3512169]：
$$
p = -(\lambda \mathrm{tr}(\boldsymbol{\varepsilon}) + 2G\varepsilon_{yy})
$$
这个结果清晰地表明，界面上的流体压力直接与固体的法向应力分量 ($\sigma_{s,yy}$) [相平衡](@entry_id:136822)。同时，第一个方程表明流体的粘性[剪切应力](@entry_id:137139) ($\mu\gamma$) 由固体的弹性剪切应变 ($\varepsilon_{xy}$) 来平衡。这个例子生动地展示了动力学条件如何将两个物理场的变量耦合在一起。

#### 不可压缩 FSI 中压力的作用

在不可压缩流体的 FSI 问题中，压力 $p$ 扮演着一个微妙而关键的双重角色 [@problem_id:3512156]。

首先，在流体域 $\Omega_f(t)$ 内部，压力是一个**[拉格朗日乘子](@entry_id:142696)**。对于[不可压缩流](@entry_id:140301)，质量守恒方程简化为运动学约束 $\nabla \cdot \mathbf{v}_f = 0$。在流体动量方程（[欧拉方程](@entry_id:177914)或[纳维-斯托克斯方程](@entry_id:142275)）中，[压力梯度](@entry_id:274112) $-\nabla p$ 作为一个力出现。这个压[力场](@entry_id:147325)没有自己的独立[演化方程](@entry_id:268137)；相反，在每个时刻，它会瞬时地调整自身，以产生一个恰到好处的梯度场，从而确保最终求解得到的速度场 $\mathbf{v}_f$ 精确满足 $\nabla \cdot \mathbf{v}_f = 0$ 的约束。

其次，在流固交界面 $\Gamma_{fs}(t)$ 上，压力的**值**（而不仅仅是它的梯度）变得至关重要。对于[无粘流](@entry_id:273124)体，应力张量为 $\boldsymbol{\sigma}_f = -p\mathbf{I}$。[动力学平衡](@entry_id:187220)条件 $\boldsymbol{\sigma}_f \mathbf{n} = \boldsymbol{\sigma}_s \mathbf{n}$ 变为 $-p\mathbf{n} = \boldsymbol{\sigma}_s \mathbf{n}$。这表明流体只能通过压力 $p$ 对固体施加[法向力](@entry_id:174233)。因此，压力的边界值直接由固体的牵[引力](@entry_id:175476)决定。

综上所述，压力 $p$ 是一个全局场，它既要满足流体域内的不可压缩约束，又要在边界上满足力的平衡。结构运动（通过[运动学](@entry_id:173318)条件 $\mathbf{v}_f = \dot{\mathbf{u}}_s$）为[流体速度](@entry_id:267320)场提供了狄利克雷边界条件。[流体压力](@entry_id:142203) $p$ 随之调整以维持流场无散度。这个压[力场](@entry_id:147325)在界面上的值产生一个作用力，该力反过来又影响结构的运动，从而形成一个完整的耦合回路 [@problem_id:3512156]。

### 高级与计算 formulations

将连续介质力学原理应用于计算机模拟时，会遇到一系列新的挑战，尤其是在处理移动边界和离散化不匹配等问题时。

#### 任意拉格朗日-欧拉（ALE）框架下的条件

在 FSI 模拟中，固体部分天然适合[拉格朗日描述](@entry_id:264498)，而流体部分则适合[欧拉描述](@entry_id:264722)。然而，当边界移动时，纯欧拉网格会变得扭曲或与边界不符。**任意拉格朗日-欧拉 (Arbitrary Lagrangian-Eulerian, ALE)** 方法通过引入一个可独立移动的计算网格来解决这个问题。网格本身以速度 $\mathbf{w}(\mathbf{x},t)$ 运动，这个速度既不等于材料速度 $\mathbf{v}_f$（拉格朗日），也不等于零（欧拉）。

在 ALE 框架下，物理定律必须保持不变。[运动学](@entry_id:173318)条件 $\mathbf{v}_f = \dot{\mathbf{u}}_s$ 是一个关于物理速度的陈述，它必须独立于我们选择的[计算网格](@entry_id:168560)速度 $\mathbf{w}$ [@problem_id:3512143]。我们可以通过一种看似迂回的方式来表达这个条件，以阐明其与 $\mathbf{w}$ 的关系：
$$
\mathbf{v}_f - \mathbf{w} = \dot{\mathbf{u}}_s - \mathbf{w}
$$
这里，$(\mathbf{v}_f - \mathbf{w})$ 是流体相对于[移动网格](@entry_id:752196)的速度。显然，两侧的 $\mathbf{w}$ 可以直接消去，还原为 $\mathbf{v}_f = \dot{\mathbf{u}}_s$。这个表述的意义在于强调，无论网格如何运动，物理上的耦合条件是不变的。在实际的计算中，为了使流体网格与固体边界保持贴合（即所谓的**[贴体网格](@entry_id:746935)**），我们必须在交界面上强制要求网格速度等于固体速度，即 $\mathbf{w} = \dot{\mathbf{u}}_s$。然后，流体求解器将这个网格速度作为流体速度的[狄利克雷边界条件](@entry_id:173524)，即 $\mathbf{v}_f = \mathbf{w}$。这两个计算步骤结合起来，便能正确地施加物理条件 $\mathbf{v}_f = \dot{\mathbf{u}}_s$ [@problem_id:3512143]。

#### [非匹配网格](@entry_id:168552)的耦合

在复杂的 FSI 问题中，为流体和固体域生成相互匹配（节点对齐）的界面网格可能非常困难或不切实际。因此，需要在[非匹配网格](@entry_id:168552)之间传递信息。这要求构建**传输算子 (transfer operators)**，将一个网格上的物理量（如速度）映射到另一个网格上，同时还要传递反作用力（如牵[引力](@entry_id:175476)）。

一个关键的要求是，这个传输过程必须是**[能量守恒](@entry_id:140514)**的（或更准确地说，是功率守恒的）。这意味着流体在界面上对固体所做的功的速率，必须等于固体从流体接收的功的速率。任何由于[插值误差](@entry_id:139425)导致的虚假能量产生或耗散都可能导致[数值不稳定性](@entry_id:137058)。

考虑流体和固体的离散界面速度分别为 $u_f$ 和 $u_s$（系数向量），离散牵[引力](@entry_id:175476)为 $t_f$ 和 $t_s$。功率守恒要求 $t_f^{\top} M_f u_f = t_s^{\top} M_s u_s$，其中 $M_f$ 和 $M_s$ 是界面[质量矩阵](@entry_id:177093) [@problem_id:3512127]。如果我们定义速度传输算子 $T_u$ 和牵[引力](@entry_id:175476)传输算子 $T_t$ 使得 $u_f = T_u u_s$ 和 $t_s = T_t t_f$，那么为了保证功率守恒，这两个算子必须满足**对偶性条件 (duality condition)**：$M_f T_u = T_t^{\top} M_s$。

一种常见的守恒方法是，将速度的传递定义为从一个空间到另一个空间的 $L^2$ 投影。例如，将固体速度投影到[流体速度](@entry_id:267320)空间。这给出了速度传输算子 $T_u = M_f^{-1} C$，其中 $C$ 是由两种网格[基函数](@entry_id:170178)乘积的积分构成的[耦合矩阵](@entry_id:191757)。然后，通过对偶性条件，可以唯一确定牵[引力](@entry_id:175476)传输算子为 $T_t = M_s^{-1} C^{\top}$ [@problem_id:3512127]。这对 $(T_u, T_t)$ 确保了力和位移在[非匹配网格](@entry_id:168552)间的传递是功率守恒的。

此外，仅仅守恒总作用力（线性动量）是不够的。如果力的[分布](@entry_id:182848)在插值后发生改变，可能会产生虚假的力矩（角动量），导致结构发生非物理的旋转。为了确保**[角动量守恒](@entry_id:156798)**，需要更高阶的守恒性质。例如，在使用**[砂浆法](@entry_id:752184) (mortar methods)** 进行耦合时，不仅要保证牵[引力](@entry_id:175476)误差与常数测试函数正交（保证力守恒），还需保证其与线性测试函数（如 $\boldsymbol{\mu} = \mathbf{a} \times \mathbf{r}$）正交。这等价于显式地施加一个约束，要求界面上的[合力矩](@entry_id:166772)为零 [@problem_id:3512137]。

#### 分区（交错）格式的稳定性

FSI 问题通常采用分区或交错格式求解，即交替求解流体和固体子问题。例如，在一个**狄利克雷-诺伊曼 (Dirichlet-Neumann)** 格式中：
1.  将固体的速度作为狄利克雷边界条件施加给流体。
2.  求解[流体方程](@entry_id:195729)，计算出作用在界面上的牵[引力](@entry_id:175476)。
3.  将此牵[引力](@entry_id:175476)作为[诺伊曼边界条件](@entry_id:142124)施加给固体。
4.  求解固体方程，更新其位置和速度。

这种交错执行在[运动学](@entry_id:173318)条件和动力学条件的满足上引入了时间延迟。这种延迟可能导致严重的数值不稳定性，特别是当固体相对于流体很轻时。这种现象被称为**[附加质量不稳定性](@entry_id:174360) (added-mass instability)** [@problem_id:3512155]。

我们可以通过一个简化的 1D 模型来理解这一点。考虑一个质量为 $m_s$ 的薄板与声速为 $c_f$、密度为 $\rho_f$ 的流体相互作用。当固体以速度 $v_s^n$ 运动时，它在流体中产生一个压力响应 $p^{n+1/2} = \rho_f c_f v_s^n$。在交错格式中，这个压力被用来更新下一个时间步的固体速度：$m_s (v_s^{n+1} - v_s^n) = -p^{n+1/2} \Delta t$。将两者结合，我们得到速度的[递推关系](@entry_id:189264)：
$$
v_s^{n+1} = \left( 1 - \frac{\rho_f c_f \Delta t}{m_s} \right) v_s^n
$$
为了使解保持有界（稳定），放大因子的大小必须不大于 1，即 $|1 - \frac{\rho_f c_f \Delta t}{m_s}| \le 1$。这导出了一个类似于 CFL 条件的[时间步长限制](@entry_id:756010)：
$$
\Delta t \le \frac{2 m_s}{\rho_f c_f} = \frac{2 \rho_s h_s}{\rho_f c_f}
$$
其中 $m_s = \rho_s h_s$。这个不等式表明，当固体密度 $\rho_s$ 或厚度 $h_s$ 相对于流体密度 $\rho_f$ 很小时，允许的最大时间步长 $\Delta t$ 会变得非常小，使得显式交错格式的计算成本过高 [@problem_id:3512155]。

### 复杂界面的扩展

基本原理可以扩展以模拟更复杂的[界面现象](@entry_id:167796)。

#### 可渗透界面

对于多孔介质或[生物膜](@entry_id:167298)等可渗透界面，流体可以穿过固体。此时，[运动学](@entry_id:173318)和动力学条件都需要修正 [@problem_id:3512174]。

运动学条件不再是不可穿透的。相反，流体相对于固体的法向速度等于穿过界面的**体积通量** $J_v$（单位面积的[体积流率](@entry_id:265771)）。如果 $q_m$ 是质量通量（单位面积的[质量流率](@entry_id:264194)），则 $J_v = q_m / \rho_f$。因此，[运动学](@entry_id:173318)条件变为：
$$
(\mathbf{v}_f - \dot{\mathbf{u}}_s) \cdot \mathbf{n} = \frac{q_m}{\rho_f}
$$

动力学上，流体流过[多孔介质](@entry_id:154591)时会受到阻力，这导致了跨界面的压力降 $\Delta p(q_m)$。这个压力降表现为一个作用在固体基质上的拖曳力。根据[牛顿第三定律](@entry_id:166652)，这个力必须包含在[界面力](@entry_id:184024)平衡中。修正后的动力学条件为：
$$
\boldsymbol{\sigma}_f \mathbf{n} = \boldsymbol{\sigma}_s \mathbf{n} - \Delta p(q_m) \mathbf{n}
$$
这里的负号表示，为了驱动一个正向流动（$q_m  0$），上游（流体侧）的压力必须高于下游（固体侧）的压力，这个压力差作为一种反作用力作用在固体上 [@problem_id:3512174]。

#### 与壳体模型的耦合

当固体结构非常薄时，通常使用[降维](@entry_id:142982)模型（如梁、板或壳）来提高计算效率。例如，一个**基尔霍夫-洛夫 (Kirchhoff-Love) 壳**模型用其中间[曲面](@entry_id:267450)的运动来描述整个结构。此时，[界面条件](@entry_id:750725)必须将三维流体物理场与二维结构模型联系起来 [@problem_id:3512144]。

[运动学](@entry_id:173318)上，壳体表面上一点的速度由两部分组成：中面的平移速度 $\mathbf{v}_s$ 和由于法线（或称导向矢量）$\mathbf{n}$ 旋转引起的附加速度。如果中面法线的角速度为 $\boldsymbol{\omega}$，壳厚为 $t$，那么外表面（在 $\zeta=+t/2$ 处）上一点的速度为：
$$
\mathbf{v}(\zeta=+t/2) = \mathbf{v}_s + \frac{t}{2} (\boldsymbol{\omega} \times \mathbf{n})
$$
因此，[流体速度](@entry_id:267320) $\mathbf{v}_f$ 必须与这个合成速度相等。

动力学上，作用在壳体三维表面上的流体牵[引力](@entry_id:175476) $\mathbf{t}_f$ 必须被等效地转换为作用在二维中面上的**合力** $\mathbf{f}$ 和**[合力矩](@entry_id:166772)** $\mathbf{m}$。这种转换必须在功的意义上是等效的（即遵循虚功原理）。对于一个[曲面](@entry_id:267450)壳，这种映射涉及到复杂的几何变换，包括考虑由于曲率引起的面积变化因子 $J$ 和一个称为“[移位](@entry_id:145848)器” $\mathbf{P}$ 的张量，以确保[能量守恒](@entry_id:140514)。最终，[合力](@entry_id:163825) $\mathbf{f}$ 和[合力矩](@entry_id:166772) $\mathbf{m}$ 是流体牵[引力](@entry_id:175476) $\mathbf{t}_f$ 在中面上的积分和一阶矩的结果 [@problem_id:3512144]。

这些例子表明，FSI 界面的基本原理虽然简单，但它们的应用需要根据具体的物理模型和计算策略进行精心的调整和扩展。