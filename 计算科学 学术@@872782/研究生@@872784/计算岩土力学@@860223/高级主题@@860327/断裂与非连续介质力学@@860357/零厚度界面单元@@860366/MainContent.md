## 引言
在计算力学，特别是计算岩[土力学](@entry_id:180264)领域，精确模拟材料和结构界面处的复杂行为——如滑移、开裂与接触——是理解系统整体响应的关键。传统的[连续介质力学](@entry_id:155125)模型在处理这些位移不连续现象时存在固有的局限性，难以捕捉应力集中和局部化失效的真实物理过程。[零厚度界面单元](@entry_id:756820)正是在这一背景下应运而生，它提供了一种强大而灵活的数值工具，专门用于在有限元模型中引入和描述这种[不连续性](@entry_id:144108)。

本文旨在系统性地介绍[零厚度界面单元](@entry_id:756820)的理论、应用与实现。通过学习，读者将能够深刻理解这一方法的核心思想，并掌握其在解决实际工程问题中的应用技巧。我们将首先在“原理与机制”一章中，从第一性原理出发，建立界面单元的运动学和本构关系，并探讨其数值实现的关键技术。随后，在“应用与跨学科联系”一章中，我们将展示该方法在土-结构相互作用、材料断裂及多物理场耦合等前沿领域的广泛应用。最后，“动手实践”部分将通过具体的编程练习，引导读者将理论知识转化为实践能力。

让我们从深入剖析[零厚度界面单元](@entry_id:756820)的理论基础和力学机制开始，为后续的探索奠定坚实的基础。

## 原理与机制

本章深入探讨[零厚度界面单元](@entry_id:756820)的理论基础、[运动学](@entry_id:173318)描述、本构关系及其在有限元框架下的数值实现。我们将从[连续介质力学](@entry_id:155125)的基本原理出发，逐步建立起这些单元的数学和物理模型，并讨论在实际计算中遇到的关键问题，如数值积分、刚度矩阵的推导和系统条件的改善。

### 界面不连续性的基本概念

在计算岩土力学和[固体力学](@entry_id:164042)中，许多关键现象——如岩体节理的张开与滑移、[复合材料](@entry_id:139856)层间的剥离、以及材料的断裂过程——都与一个核心的物理概念相关：**位移[不连续性](@entry_id:144108)**。为了精确地模拟这些现象，我们必须在数学上描述一个连续体内部存在的、[位移场](@entry_id:141476)不再连续的表面。

设想一个物体被一个假想的表面 $\Gamma$ 分割为两个[子域](@entry_id:155812) $\Omega^{+}$ 和 $\Omega^{-}$。当物体变形时，原先在表面 $\Gamma$ 上重合的物[质点](@entry_id:186768)可能会发生分离或相对滑动。我们将 $\Gamma$ 上的位移[不连续性](@entry_id:144108)，即**位移跳跃 (displacement jump)**，定义为两个子域在该表面上位移的差值：
$$ \llbracket \boldsymbol{u} \rrbracket = \boldsymbol{u}^{+} - \boldsymbol{u}^{-} $$
其中 $\boldsymbol{u}^{+}$ 和 $\boldsymbol{u}^{-}$ 分别是子域 $\Omega^{+}$ 和 $\Omega^{-}$ 在界面 $\Gamma$ 上的[位移矢量](@entry_id:262782)。这个位移跳跃向量 $\llbracket \boldsymbol{u} \rrbracket$ 捕捉了界面的所有相对运动模式，包括法向的张开或闭合，以及切向的滑移。

与位移跳跃这个[运动学](@entry_id:173318)量相对应的是动力学量——**界面牵[引力](@entry_id:175476) (interface traction)** $\boldsymbol{t}$。根据牛顿第三定律，在忽略界面本身惯性效应的准静态条件下，作用在界面两侧的牵[引力](@entry_id:175476)必须大小相等、方向相反。这构成了**牵引力平衡 (traction equilibrium)** 条件。若定义 $\boldsymbol{n}$ 为从 $\Omega^{-}$ 指向 $\Omega^{+}$ 的[单位法向量](@entry_id:178851)，则该条件可表示为：
$$ \boldsymbol{t} = \boldsymbol{\sigma}^{+}\boldsymbol{n} = -\boldsymbol{\sigma}^{-}\boldsymbol{n} $$
其中 $\boldsymbol{\sigma}^{+}$ 和 $\boldsymbol{\sigma}^{-}$ 分别是两个子域在界面上的柯西[应力张量](@entry_id:148973)。

### [虚功原理](@entry_id:138749)与[零厚度界面单元](@entry_id:756820)的引入

为了将界面[不连续性](@entry_id:144108)的概念融入有限元方法，我们求助于**[虚功原理](@entry_id:138749) (Principle of Virtual Work)**。对于一个标准的连续体，[内力](@entry_id:167605)所做的[虚功](@entry_id:176403)等于[体力](@entry_id:174230)和面力所做的[虚功](@entry_id:176403)。然而，当体内存在位移不连续表面 $\Gamma$ 时，[内虚功](@entry_id:172278)的表达式必须做出修正。

总[内虚功](@entry_id:172278) $\delta W_{int}$ 不仅包含连续体块体部分 $\Omega^+ \cup \Omega^-$ 的应力-应变功，还必须包含一个额外的项，用以描述界面牵[引力](@entry_id:175476) $\boldsymbol{t}$ 在[虚位移](@entry_id:168781)跳跃 $\delta \llbracket \boldsymbol{u} \rrbracket$ 上所做的功。因此，虚功原理的完整形式变为：
$$ \int_{\Omega^+ \cup \Omega^-} \boldsymbol{\sigma} : \delta\boldsymbol{\varepsilon} \, \mathrm{d}V + \int_{\Gamma} \boldsymbol{t} \cdot \delta \llbracket \boldsymbol{u} \rrbracket \, \mathrm{d}\Gamma = \delta W_{ext} $$
其中 $\delta W_{ext}$ 是外力（如[体力](@entry_id:174230)、外边界上的面力）所做的[虚功](@entry_id:176403)。

这个公式中的第二项，即界面上的积分项 $\int_{\Gamma} \boldsymbol{t} \cdot \delta \llbracket \boldsymbol{u} \rrbracket \, \mathrm{d}\Gamma$，是整个问题的核心。**[零厚度界面单元](@entry_id:756820) (zero-thickness interface elements)** 正是这一项在有限元法中的离散化体现。这些单元在几何上没有厚度，被嵌入到相邻体单元之间，其唯一的目的就是建立界面牵[引力](@entry_id:175476) $\boldsymbol{t}$ 和位移跳跃 $\llbracket \boldsymbol{u} \rrbracket$ 之间的[本构关系](@entry_id:186508)，从而在不引入额外体积柔度的前提下，精确地模拟界面的开启、滑移、接触和软化等局部化行为 [@problem_id:3571918]。

### [零厚度界面单元](@entry_id:756820)的[运动学](@entry_id:173318)

在有限元模型中，我们通过在潜在不连续路径上创建重合的节点来定义零厚度界面。例如，一个二维线性界面单元通常由四对节点组成，其中两对属于“+”面，另外两对属于“-”面，初始时刻它们的坐标完全相同。

单元的[运动学](@entry_id:173318)描述旨在建立节点位移与界面上任意点处位移跳跃之间的关系。

#### 位移跳跃的插值

设单元的节点位移向量为 $\mathbf{u}_e^+$ 和 $\mathbf{u}_e^-$，分别对应“+”面和“-”面的节点。利用标准的有限元形函数 $N_i(\xi)$（其中 $\xi$ 是单元的自然坐标），我们可以插值得到界面上任意点的位移：
$$ \boldsymbol{u}^{+}(\xi) = \mathbf{N}^{+}(\xi) \mathbf{u}_e^{+} \quad \text{和} \quad \boldsymbol{u}^{-}(\xi) = \mathbf{N}^{-}(\xi) \mathbf{u}_e^{-} $$
这里的 $\mathbf{N}(\xi)$ 是由标量形函数 $N_i(\xi)$ 组成的插值矩阵。因此，位移跳跃向量 $\boldsymbol{\delta}(\xi)$（即 $\llbracket \boldsymbol{u} \rrbracket$ 的离散形式）可以表示为：
$$ \boldsymbol{\delta}(\xi) = \boldsymbol{u}^{+}(\xi) - \boldsymbol{u}^{-}(\xi) = \mathbf{N}^{+}(\xi) \mathbf{u}_e^{+} - \mathbf{N}^{-}(\xi) \mathbf{u}_e^{-} $$
这个向量 $\boldsymbol{\delta}(\xi)$ 是在[全局坐标系](@entry_id:171029)下定义的。

#### [局部坐标系](@entry_id:751394)及其投影

为了描述物理上更有意义的界面行为，如法向张开和切向滑移，我们通常需要在界面的每个积分点（例如，[高斯点](@entry_id:170251)）上定义一个**局部[正交坐标](@entry_id:166074)系** $\{\mathbf{n}, \mathbf{t}\}$。其中，$\mathbf{n}$ 是界面的[单位法向量](@entry_id:178851)，$\mathbf{t}$ 是[单位切向量](@entry_id:262985)。

全局位移跳跃向量 $\boldsymbol{\delta}$ 可以通过投影分解到这个局部坐标系中，得到法向分离量 $\delta_n$ 和切向分离量 $\delta_t$。如果我们将[局部基](@entry_id:151573)底向量组合成一个旋转矩阵 $\mathbf{Q} = [\mathbf{n} \; \mathbf{t}]$，这个投影过程可以通过矩阵运算完成 [@problem_id:3549015]：
$$ \begin{pmatrix} \delta_n \\ \delta_t \end{pmatrix} = \mathbf{Q}^\top \boldsymbol{\delta} = \begin{pmatrix} \mathbf{n}^\top \boldsymbol{\delta} \\ \mathbf{t}^\top \boldsymbol{\delta} \end{pmatrix} $$
这里的符号约定至关重要。通常，我们定义 $\mathbf{n}$ 从“-”面指向“+”面，这样当“+”面相对于“-”面沿 $\mathbf{n}$ 方向移动时，$\delta_n$ 为正值，代表界面张开。$\delta_t$ 则是一个有符号的量，表示沿 $\mathbf{t}$ 方向的相对滑移。这个运动学计算是后续所有本构模型评估的基础，它本身完全独立于本构律。

为了具体说明这一过程，我们考虑一个二维线性界面单元的数值算例 [@problem_id:3571962]。假设单元的节点1和节点2的初始坐标分别为 $(0,0)$ 和 $(2,1)$（单位 mm）。给定两对节点的位移后，我们首先可以在[高斯点](@entry_id:170251) $\xi=0$ 处利用形函数（$N_1(0)=N_2(0)=0.5$）插值计算出“+”面和“-”面的位移，进而求得全局位移跳跃向量 $\Delta\mathbf{u}(0)$。接着，根据变形后的[节点平均](@entry_id:178002)位置确定单元的[切线](@entry_id:268870)方向，并旋转 $90^{\circ}$ 得到[法线](@entry_id:167651)方向，从而建立局部坐标系。最后，将全局位移跳跃向量 $\Delta\mathbf{u}(0)$ 投影到[单位法向量](@entry_id:178851) $\mathbf{n}$上，即可求得该点的法向间隙 $g_n = \Delta\mathbf{u}(0) \cdot \mathbf{n}$。这个计算流程将抽象的公式与具体的数值联系起来，是理解界面单元运动学的关键。

### [本构模型](@entry_id:174726)：牵[引力](@entry_id:175476)-分离律 (TSL)

界面单元的“机制”由其[本构关系](@entry_id:186508)，即**牵[引力](@entry_id:175476)-分离律 (Traction-Separation Law, TSL)** 所决定。TSL 定义了界面牵[引力](@entry_id:175476) $\boldsymbol{t}$ 如何随局部相对位移（分离）$\boldsymbol{\delta}$ 而变化，即 $\boldsymbol{t} = \boldsymbol{t}(\boldsymbol{\delta})$。TSL 的选择直接决定了界面模拟的行为。

#### [线性弹性](@entry_id:166983)关系与[罚函数法](@entry_id:636090)

最简单的 TSL 是线性关系，即 $\boldsymbol{t} = \mathbf{K} \boldsymbol{\delta}$，其中 $\mathbf{K}$ 是界面[刚度矩阵](@entry_id:178659)。这种关系可以用来模拟一个弹性连接。然而，在计算实践中，它更常被用于以**[罚函数法](@entry_id:636090) (penalty method)** 的形式近似地施加连续性或[接触约束](@entry_id:171598)。

考虑一个一维杆件，其中间由一个[罚刚度](@entry_id:753321)为 $k_p$ 的界面单元连接 [@problem_id:3571944]。当杆件受力 $P$ 时，界面处的牵[引力](@entry_id:175476) $t = P/A$（$A$为[横截面](@entry_id:154995)积）。根据界面本构关系 $t = k_p [[u]]$，产生的位移跳跃为 $[[u]] = P/(A k_p)$。这个跳跃代表了罚方法引入的“人为柔度”。总的杆端位移 $u_{\text{penalty}}$ 是杆件自身弹性变形 $u_{\text{exact}} = PL/(AE)$ 与这个人为跳跃之和。为了使误差（即相对位移增加量 $(u_{\text{penalty}} - u_{\text{exact}})/u_{\text{exact}} = E/(k_p L)$）控制在可接受的范围内，罚参数 $k_p$ 必须足够大。例如，要将[误差控制](@entry_id:169753)在 $1\%$ 以内，则 $k_p$ 必须至少为 $E/(0.01 L)$。这揭示了罚参数、材料属性和几何尺寸之间的权衡关系。

#### 用于[断裂模拟](@entry_id:199069)的内聚力模型 (CZM)

当目标是模拟断裂过程时，TSL 必须能够描述材料的损伤、软化和能量耗散。这类 TSL 通常被称为**内聚力模型 (Cohesive Zone Models, CZM)**。一个典型的 CZM 曲线包括：
1.  **初始弹性阶段**：牵[引力](@entry_id:175476)随分离量线性增加，达到一个峰值牵[引力](@entry_id:175476) $\sigma_{\max}$，也称为材料的[内聚强度](@entry_id:194858)。
2.  **软化阶段**：达到峰值后，牵[引力](@entry_id:175476)随分离量的进一步增加而下降，模拟材料损伤的[累积和](@entry_id:748124)承载能力的丧失。
3.  **完全失效**：当分离量达到某个临界值 $\delta_f$ 时，牵[引力](@entry_id:175476)降为零，表示界面完全断开。

CZM 的一个核心物理参数是**[断裂能](@entry_id:174458) (fracture energy)** $G_c$，定义为将单位面积的界面完全分离所需的功，等于 TSL 曲线下的总面积：$G_c = \int_{0}^{\delta_f} T(\delta) \, \mathrm{d}\delta$。$G_c$ 是一个材料常数，使用基于能量的断裂模型可以有效地消除[网格依赖性](@entry_id:198563)。

软化阶段的函数形式可以有多种选择，例如线性软化或指数软化 [@problem_id:3571925]。不同形状的 TSL 会影响断裂过程的细节，但它们可以被校准以具有相同的总[断裂能](@entry_id:174458) $G_c$。例如，一个具有线性软化、最终失效位移为 $\delta_f$ 的 TSL，其[断裂能](@entry_id:174458)为 $G_{c,A} = \frac{1}{2} \sigma_{\max} \delta_f$。而一个具有指数软化形式 $T(\delta) = \sigma_{\max} \exp(-(\delta - \delta_p)/\delta_0)$ 的 TSL，其断裂能为 $G_{c,B} = \frac{1}{2}\sigma_{\max}\delta_p + \sigma_{\max}\delta_0$。通过令 $G_{c,A} = G_{c,B}$，我们就可以建立两种模型参数之间的关系，从而实现能量等效的校准。

#### 基于[热力学](@entry_id:141121)框架的损伤模型

为了更严谨地构建 TSL，我们可以采用基于[连续介质损伤力学](@entry_id:177438)的[热力学](@entry_id:141121)框架。在这种方法中，我们首先定义一个表征界面状态的**[亥姆霍兹自由能](@entry_id:136442) (Helmholtz free energy)** $\psi$，它通常是分离量 $\boldsymbol{s}$ 和一个或多个内部状态变量（如[损伤变量](@entry_id:197066) $d$）的函数。

例如，一个简单的损伤模型可以定义为 [@problem_id:3571960]：
$$ \psi(\boldsymbol{s}, d) = \frac{1}{2}(1 - d)\boldsymbol{s}^{\mathsf{T}}\mathbf{K}\boldsymbol{s} $$
其中 $\mathbf{K}$ 是界面的初始（无损）[刚度矩阵](@entry_id:178659)，$d \in [0,1]$ 是[标量损伤变量](@entry_id:196275)。

根据[热力学](@entry_id:141121)共轭关系，牵[引力](@entry_id:175476) $\boldsymbol{t}$ 和损伤驱动力 $Y$ 可以通过对自由能求导得到：
$$ \boldsymbol{t} = \frac{\partial \psi}{\partial \boldsymbol{s}} = (1-d)\mathbf{K}\boldsymbol{s} $$
$$ Y = -\frac{\partial \psi}{\partial d} = \frac{1}{2}\boldsymbol{s}^{\mathsf{T}}\mathbf{K}\boldsymbol{s} $$
损伤驱动力 $Y$ 代表了无损状态下的弹性应变能密度。然后，我们需要一个**[损伤演化](@entry_id:184965)律 (damage evolution law)**，它规定了[损伤变量](@entry_id:197066) $d$ 如何随加载历史（通常由 $Y$ 的最大历史值 $Y^{\max}$ 决定）而增长。例如，一个线性软化演化律可以定义为当 $Y$ 超过[损伤起始](@entry_id:748159)阈值 $Y_0$ 后，$d$ 开始线性增长，直到 $Y$ 达到失效阈值 $Y_f$ 时 $d$ 增长到 1。通过这种方式，我们可以为给定的分离状态 $\boldsymbol{s}$，首先计算出 $Y$，然后根据演化律确定 $d$，最后计算出相应的牵[引力](@entry_id:175476) $\boldsymbol{t}$。这个框架为构建复杂的、物理意义明确的 TSL 提供了坚实的理论基础。

### 数值实现与注意事项

将[零厚度界面单元](@entry_id:756820)应用于[非线性有限元分析](@entry_id:167596)中，需要解决几个关键的数值问题。

#### [有限元列式](@entry_id:164720)与一致性[切线刚度](@entry_id:166213)

在有限元框架中，我们需要计算单元的**[内力向量](@entry_id:750751) (internal force vector)** $\mathbf{F}_{\text{int}}$ 和**[切线刚度矩阵](@entry_id:170852) (tangent stiffness matrix)** $\mathbf{K}_e$。根据[虚功原理](@entry_id:138749)，[内力向量](@entry_id:750751)由下式给出：
$$ \mathbf{F}_{\text{int}} = \int_{\Gamma_e} \mathbf{B}(\xi)^\top \mathbf{t}(\xi) \, \mathrm{d}\Gamma $$
其中 $\mathbf{B}(\xi)$ 是连接节点位移与界面分离的运动学矩阵（或称几何矩阵）。

在基于牛顿-拉夫逊法的[隐式求解器](@entry_id:140315)中，为了保证二次[收敛率](@entry_id:146534)，必须使用**一致性[切线刚度矩阵](@entry_id:170852) (consistent tangent stiffness matrix)**，它被定义为[内力向量](@entry_id:750751)对节点位移的导数：
$$ \mathbf{K}_e = \frac{\partial \mathbf{F}_{\text{int}}}{\partial \mathbf{d}} = \int_{\Gamma_e} \mathbf{B}^\top \frac{\partial \mathbf{t}}{\partial \boldsymbol{\delta}} \frac{\partial \boldsymbol{\delta}}{\partial \mathbf{d}} \, \mathrm{d}\Gamma = \int_{\Gamma_e} \mathbf{B}^\top \mathbf{D} \mathbf{B} \, \mathrm{d}\Gamma $$
这里的关键是**局部[算法切线](@entry_id:165770)矩阵 (local algorithmic tangent matrix)** $\mathbf{D} = \partial \boldsymbol{t} / \partial \boldsymbol{\delta}$。对于复杂的 TSL，例如前面提到的损伤模型 $\boldsymbol{t} = (1-d(\lambda(\boldsymbol{\delta})))\mathbf{K}\boldsymbol{\delta}$，计算 $\mathbf{D}$ 需要应用链式法则 [@problem_id:3571955] [@problem_id:2871438]：
$$ \mathbf{D} = \frac{\partial \boldsymbol{t}}{\partial \boldsymbol{\delta}} = (1-d)\mathbf{K} - (\mathbf{K}\boldsymbol{\delta}) \otimes \left( \frac{\mathrm{d}d}{\mathrm{d}\lambda} \frac{\partial \lambda}{\partial \boldsymbol{\delta}} \right) $$
其中 $\otimes$ 表示[并矢积](@entry_id:748716)。值得注意的是，由于损伤准则 $\lambda$ 的混合[模式耦合](@entry_id:752088)（即同时依赖于 $\delta_n$ 和 $\delta_t$），上式中的第二项通常会导致 $\mathbf{D}$ 矩阵**非对称**。使用非对称的 $\mathbf{D}$ 对于保证算法的收敛性至关重要，而使用简化的对称或割线刚度则会破坏二次收敛性。

#### [数值积分](@entry_id:136578)

单元的[内力向量](@entry_id:750751)和[刚度矩阵](@entry_id:178659)的计算涉及到沿单元长度的积分，这通常通过**[高斯-勒让德求积](@entry_id:138201) (Gauss-Legendre Quadrature)** 等[数值积分方法](@entry_id:141406)完成。积分方案的选择需要平衡计算成本、精度和稳定性。

对于一个使用线性形函数插值位移跳跃的界面单元，其[刚度矩阵](@entry_id:178659)的被积函数 $\mathbf{B}^\top \mathbf{D} \mathbf{B}$（假设 $\mathbf{D}$ 是常数）是一个关于自然坐标 $\xi$ 的二次多项式。为了精确地积分一个 $k$ 次多项式，高斯求积至少需要 $(k+1)/2$ 个积分点。因此，要精确积分一个二次多项式，至少需要 $p \ge (2+1)/2 = 1.5$，即最少需要 **2 个[高斯点](@entry_id:170251)**。这被称为**完全积分 (full integration)**。

使用少于所需点数的积分方案，如 **1 [点积](@entry_id:149019)分**（**[减缩积分](@entry_id:167949)**），虽然可以降低计算成本，但可能无法“感知”某些变形模式，从而导致**[伪零能模式](@entry_id:755267) (spurious zero-energy modes)** 或称“[沙漏模式](@entry_id:174855)”，使得[刚度矩阵](@entry_id:178659)奇[异或](@entry_id:172120)接近奇异，最终导致数值解的剧烈[振荡](@entry_id:267781)和失稳 [@problem_id:3572002]。因此，对于线性界面单元，采用 2 点[高斯积分](@entry_id:187139)是兼顾精度、稳定性和效率的标准做法。

#### [数值条件](@entry_id:136760)与稳定性

当界面单元被用于施加接触或连续性等硬约束时（即界面刚度非常大时），可能会引发严重的**[数值病态](@entry_id:169044) (ill-conditioning)** 问题。系统的**谱[条件数](@entry_id:145150) (spectral condition number)** $\kappa = \lambda_{max} / \lambda_{min}$（最大[特征值](@entry_id:154894)与最小特征值之比）会变得非常大，导致线性方程组求解器精度下降甚至失效。

考虑一个简单的[罚函数法](@entry_id:636090)模型 [@problem_id:3572013]，系统的条件数 $\kappa$ 近似为 $1 + 2k_p/k_b$，其中 $k_p$ 是[罚刚度](@entry_id:753321)，$k_b$ 是相邻体单元的刚度。在有限元中，体单元刚度 $k_b$ 通常与网格尺寸 $h$ 成反比，即 $k_b \sim EA/h$。如果选择一个与网格无关的、非常大的常数作为 $k_p$，那么随着网格加密（$h \to 0$），$k_b$ 会减小，导致[条件数](@entry_id:145150) $\kappa$ 剧增，从而引发病态问题。

为了解决这个问题，标准做法是让罚参数与体单元刚度**成比例**，即 $k_p \sim EA/h$。通过这种方式，比值 $k_p/k_b$ 保持为一个与网格无关的常数，从而使得系统的条件数增长得到控制，避免了随着[网格加密](@entry_id:168565)而出现的严重病态。

除了罚方法，还有更先进的约束施加技术：
*   **Nitsche 方法**：通过在[虚功](@entry_id:176403)方程中添加对称且一致的项来施加约束。它同样需要一个稳定参数 $\gamma$，该参数也需要与 $EA/h$ 成比例以保证稳定性和良好的[条件数](@entry_id:145150)。Nitsche 方法的优点在于它是一个一致的方法，并且不引入额外的自由度 [@problem_id:3572013]。
*   **拉格朗日乘子法**：通过引入一个代表界面牵[引力](@entry_id:175476)的拉格朗日乘子场 $\lambda$ 来精确施加约束。这种[混合格式](@entry_id:167436)虽然可以精确满足约束，但会形成一个[鞍点问题](@entry_id:174221)的系统矩阵，且要求位移和乘子场的[插值函数](@entry_id:262791)满足**LBB (Ladyzhenskaya-Babuška-Brezzi) 稳定条件**，否则会导致伪压力[振荡](@entry_id:267781)。例如，对位移和乘子采用同阶插值（如 P1-P1）通常是不稳定的 [@problem_id:3572013]。

综上所述，[零厚度界面单元](@entry_id:756820)是一种功能强大且灵活的工具，但其成功的应用依赖于对运动学、本构关系以及数值实现细节的深刻理解。