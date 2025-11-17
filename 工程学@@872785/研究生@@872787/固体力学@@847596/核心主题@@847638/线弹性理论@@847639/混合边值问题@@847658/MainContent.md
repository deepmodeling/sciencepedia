## 引言
在模拟真实世界的工程结构时，我们很少遇到边界条件完全统一的理想情况。更常见的是，结构的某些部分被固定或强制位移，而其他部分则承受着已知的外部载荷。这种在边界上施加了不同类型约束的力学模型，构成了[固体力学](@entry_id:164042)中一类至关重要且普遍存在的问题——混合[边值问题](@entry_id:193901)。理解和求解这类问题，对于精确预测结构响应、确保其安全性和可靠性至关重要。

然而，[混合边界条件](@entry_id:176456)的引入也带来了理论上的挑战。它打破了纯位移或纯力边界问题的简洁性，要求我们建立一个更为通用和稳健的数学框架来统一处理不同类型的约束。本文旨在填补这一认知上的间隙，为读者提供一个关于混合[边值问题](@entry_id:193901)的全面视角。

在接下来的内容中，我们将分三步深入探索这一主题。首先，在“原理与机制”一章，我们将建立问题的数学基础，从经典的强形式提法过渡到功能强大的[变分弱形式](@entry_id:756448)，并探讨其[解的存在唯一性](@entry_id:177406)。接着，在“应用与交叉学科联系”一章，我们将展示这些理论如何在结构力学、接触力学、断裂力学乃至[多物理场](@entry_id:164478)和[反问题](@entry_id:143129)等前沿领域中发挥关键作用。最后，通过“动手实践”部分提供的具体计算和分析练习，您将有机会亲手应用所学知识，将抽象的理论转化为解决实际问题的能力。

## 原理与机制

在对弹性体进行力学分析时，其行为不仅取决于控制体积内部的物理定律，同样也深刻地依赖于其边界与外部环境的相互作用。混合边值问题（Mixed Boundary Value Problems）是[固体力学](@entry_id:164042)中一类至关重要且普遍存在的问题，其特点是在物体边界的不同部分分别施加了不同类型的约束。一部分边界的位移被直接指定，而另一部分的受力情况（即牵[引力](@entry_id:175476)）被给定。本章旨在系统阐述混合边值问题的基本原理、数学表述及其求解机制，为后续更复杂的应用奠定坚实的理论基础。

### 强形式提法：控制方程与边界条件

一个[线性弹性](@entry_id:166983)体的静态行为可以通过一组[偏微分方程](@entry_id:141332)和相应的边界条件来完整描述，这被称为问题的**强形式**（strong form）。该提法要求解在定义域内的每一点都精确满足控制方程，并在边界的每一点都精确满足边界条件。

#### 平衡方程与[本构关系](@entry_id:186508)

在静态和忽略[体力](@entry_id:174230)矩的假设下，物体内部任意一点的应力状态必须满足**[线性动量平衡](@entry_id:193575)方程**（balance of linear momentum），也称为柯西第一运动定律的静态形式。若以 $\boldsymbol{\sigma}$ 表示柯西[应力张量](@entry_id:148973)，$\boldsymbol{f}$ 表示单位体积的体力（如重力），则[平衡方程](@entry_id:172166)为：
$$
-\nabla \cdot \boldsymbol{\sigma} = \boldsymbol{f}
$$
其中 $\nabla \cdot$ 是[散度算子](@entry_id:265975)。这个方程的含义是，作用于一个无限小体积单元上的应力变化率必须与体力[相平衡](@entry_id:136822)。

应力 $\boldsymbol{\sigma}$ 与物体的变形状态之间通过**本构关系**（constitutive law）联系起来。在[线性弹性](@entry_id:166983)范围内，[应力与应变](@entry_id:137374)成[线性关系](@entry_id:267880)。对于一个各向同性、均匀的材料，其本构关系（胡克定律）通常用两个拉梅参数（Lamé parameters）$\lambda$ 和 $\mu$（剪切模量）来描述：
$$
\boldsymbol{\sigma}(\boldsymbol{u}) = \lambda (\nabla \cdot \boldsymbol{u})\boldsymbol{I} + 2\mu \boldsymbol{\varepsilon}(\boldsymbol{u})
$$
式中，$\boldsymbol{u}$ 是[位移场](@entry_id:141476)，$\boldsymbol{I}$ 是二阶单位张量，而 $\boldsymbol{\varepsilon}(\boldsymbol{u})$ 是**[无穷小应变张量](@entry_id:167211)**（infinitesimal strain tensor），定义为[位移梯度](@entry_id:165352)的对称部分：
$$
\boldsymbol{\varepsilon}(\boldsymbol{u}) = \frac{1}{2} \left( \nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^{\top} \right)
$$
这个定义确保了[应变张量](@entry_id:193332)是纯变形的度量，不包含[刚体转动](@entry_id:191086) [@problem_id:2662855]。

#### 边界条件的分类与物理意义

一个定义在有界域 $\Omega \subset \mathbb{R}^d$ 上的[边值问题](@entry_id:193901)，其[解的唯一性](@entry_id:143619)与边界 $\partial\Omega$ 上的约束条件密切相关。在混合[边值问题](@entry_id:193901)中，边界被划分为互不相交的两个部分 $\Gamma_u$ 和 $\Gamma_t$，使得 $\partial\Omega = \overline{\Gamma_u} \cup \overline{\Gamma_t}$。

1.  **[位移边界条件](@entry_id:203261) (Dirichlet 条件)**：在边界部分 $\Gamma_u$ 上，[位移场](@entry_id:141476)被直接指定为一个已知函数 $\bar{\boldsymbol{u}}$：
    $$
    \boldsymbol{u} = \bar{\boldsymbol{u}} \quad \text{在 } \Gamma_u \text{ 上}
    $$
    这类条件也被称为**本质边界条件**（essential boundary condition），因为它们必须在求解过程中被精确满足，并且通常直接施加在解[函数空间](@entry_id:143478)的定义上。物理上，这对应于将物体的某一部分固定或使其按预定轨迹运动。

2.  **牵[引力](@entry_id:175476)边界条件 (Neumann 条件)**：在边界部分 $\Gamma_t$ 上，作用在物体表面上的力被指定。这个力通过**牵[引力](@entry_id:175476)矢量**（traction vector）$\bar{\boldsymbol{t}}$ 来描述，它代表单位面积上的接触力。根据**柯西应力定理**，内部[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 通过边界外法向单位矢量 $\boldsymbol{n}$ 与牵[引力](@entry_id:175476)相联系：
    $$
    \boldsymbol{\sigma}\boldsymbol{n} = \bar{\boldsymbol{t}} \quad \text{在 } \Gamma_t \text{ 上}
    $$
    这类条件被称为**自然边界条件**（natural boundary condition），我们将在后续的变分推导中看到其命名的缘由。

牵[引力](@entry_id:175476)边界条件的物理意义源于边界处局部作用力的平衡。我们可以想象在边界 $\Gamma_t$ 处取一个极薄的“药盒”形控制体，其一个表面与物体外部环境接触，另一个表面位于物体内部。当我们将该控制体的高度趋近于零时，其体积相关的项（如体力和惯性力）将比面积相关的项更快地趋于零。因此，在边界表面上，外部环境施加的面力 $\bar{\boldsymbol{t}}$ 必须与物体内部应力在边界上产生的反作用力 $\boldsymbol{\sigma}\boldsymbol{n}$ 精确平衡 [@problem_id:2662899]。这清楚地表明，牵[引力](@entry_id:175476)边界条件是边界上局部力平衡的直接体现，它仅与该点的应力[状态和](@entry_id:193625)法向有关，在一个经典的柯西连续介质模型中，与边界的曲率无关（除非引入表面张力等非经典效应）[@problem_id:2662899]。值得注意的是，在位移边界 $\Gamma_u$ 上，牵[引力](@entry_id:175476) $\boldsymbol{\sigma}\boldsymbol{n}$ 通常是未知的，它代表了为维持指定位移所必须施加的[反作用](@entry_id:203910)力。

### 变分框架与[弱形式](@entry_id:142897)提法

强形式提法要求解具有高度的光滑性（例如，位移场至少二次可微），这在许多实际问题中（如存在尖角或载荷突变）难以满足。**变分原理**（variational principles）提供了一种更灵活且数学上更稳健的框架，即**弱形式**（weak form）。

#### 从[虚功原理](@entry_id:138749)到弱形式

[弱形式](@entry_id:142897)可以通过**虚功原理**（Principle of Virtual Work）导出。我们将[平衡方程](@entry_id:172166) $-(\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{f}) = \boldsymbol{0}$ 的两边点乘一个任意的、满足运动学约束的[虚位移](@entry_id:168781)场 $\boldsymbol{v}$（称为**检验函数**或**试函数**），并在整个定义域 $\Omega$ 上积分：
$$
\int_{\Omega} (-\nabla \cdot \boldsymbol{\sigma}) \cdot \boldsymbol{v} \, d\Omega = \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, d\Omega
$$
利用张量形式的[格林公式](@entry_id:173118)（即分部积分），左侧的积分可以转化为：
$$
\int_{\Omega} \boldsymbol{\sigma} : \nabla\boldsymbol{v} \, d\Omega - \int_{\partial\Omega} (\boldsymbol{\sigma}\boldsymbol{n}) \cdot \boldsymbol{v} \, dS = \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, d\Omega
$$
考虑到[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的对称性，我们有 $\boldsymbol{\sigma} : \nabla\boldsymbol{v} = \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\boldsymbol{v})$。边界积分则在 $\Gamma_u$ 和 $\Gamma_t$ 上分别处理。关键的一步是，我们选择的检验函数 $\boldsymbol{v}$ 必须是**运动学容许**的，并且满足齐次的本质边界条件，即 $\boldsymbol{v} = \boldsymbol{0}$ 在 $\Gamma_u$ 上。这样，边界积分中在 $\Gamma_u$ 上的部分就自动消失了。在 $\Gamma_t$ 上，我们代入牵[引力](@entry_id:175476)边界条件 $\boldsymbol{\sigma}\boldsymbol{n} = \bar{\boldsymbol{t}}$。

经过整理，我们得到[弱形式](@entry_id:142897)：寻找位移场 $\boldsymbol{u}$，满足[本质边界条件](@entry_id:173524) $\boldsymbol{u} = \bar{\boldsymbol{u}}$ 在 $\Gamma_u$ 上，并且对于所有满足 $\boldsymbol{v} = \boldsymbol{0}$ 在 $\Gamma_u$ 上的[检验函数](@entry_id:166589) $\boldsymbol{v}$，下式均成立：
$$
\int_{\Omega} \boldsymbol{\sigma}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\boldsymbol{v}) \, d\Omega = \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, d\Omega + \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \boldsymbol{v} \, dS
$$
对于各向同性材料，左侧可以写成 [@problem_id:2662855]：
$$
\int_{\Omega} \left[ \lambda (\nabla \cdot \boldsymbol{u})(\nabla \cdot \boldsymbol{v}) + 2\mu \boldsymbol{\varepsilon}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\boldsymbol{v}) \right] d\Omega
$$
弱形式的优势在于它降低了对解的[光滑性](@entry_id:634843)要求（仅要求位移场一阶可积），并且将边界条件以不同的方式纳入体系：[本质边界条件](@entry_id:173524)（位移）是对求解函数空间本身的约束，而自然边界条件（牵[引力](@entry_id:175476)）则体现在[变分方程](@entry_id:635018)的积分项中，这也是其“自然”之名的由来。

#### 从[势能](@entry_id:748988)原理到自然边界条件

[变分原理](@entry_id:198028)的另一个深刻体现是**[最小势能原理](@entry_id:173340)**。对于一个弹性系统，其总[势能](@entry_id:748988) $\Pi(\boldsymbol{u})$ 由内部应变能和外力势能组成。对于一个在 $\Gamma_t$ 上受牵[引力](@entry_id:175476) $\boldsymbol{t}$ 作用的物体，其总[势能](@entry_id:748988)泛函为：
$$
\Pi(\boldsymbol{u}) = \int_{\Omega} W(\boldsymbol{\varepsilon}(\boldsymbol{u})) \, dV - \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{u} \, dV - \int_{\Gamma_t} \boldsymbol{t} \cdot \boldsymbol{u} \, dS
$$
其中 $W(\boldsymbol{\varepsilon}) = \frac{1}{2}\boldsymbol{\varepsilon} : \mathbb{C} : \boldsymbol{\varepsilon}$ 是[应变能密度](@entry_id:200085)。平衡状态对应于总势能的[稳定点](@entry_id:136617)，即其一阶变分 $\delta\Pi$ 为零。通过对 $\Pi(\boldsymbol{u})$ 进行变分计算，并再次利用分部积分，可以发现 [@problem_id:2662866]：
$$
\delta\Pi = - \int_{\Omega} (\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{f}) \cdot \delta\boldsymbol{u} \, dV + \int_{\Gamma_t} (\boldsymbol{\sigma}\boldsymbol{n} - \boldsymbol{t}) \cdot \delta\boldsymbol{u} \, dS = 0
$$
由于[虚位移](@entry_id:168781) $\delta\boldsymbol{u}$ 在定义域内部和 $\Gamma_t$ 边界上是任意的，这要求两个积分内的被积函数必须恒为零。这不仅重新得到了体积内的[平衡方程](@entry_id:172166) $\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{f} = \boldsymbol{0}$，而且直接导出了在 $\Gamma_t$ 上的自然边界条件 $\boldsymbol{\sigma}\boldsymbol{n} = \boldsymbol{t}$。这个推导优美地揭示了自然边界条件是系统能量泛函取[极值](@entry_id:145933)时的必然结果。

### 数学基础：函数空间与良定性

为了严格地分析[弱形式](@entry_id:142897)解的存在性和唯一性（即**良定性**），必须引入适当的数学工具，主要是 Sobolev 空间理论。

对于[弱形式](@entry_id:142897)，[位移场](@entry_id:141476) $\boldsymbol{u}$ 和[检验函数](@entry_id:166589) $\boldsymbol{v}$ 的函数空间需要包含其自身和其[一阶导数](@entry_id:749425)的平方可积的函数。这正是**Sobolev 空间** $[H^1(\Omega)]^d$ 的定义。然而，对于 $H^1$ 空间中的函数，其在边界上的取值并不是逐点明确定义的。

**[迹定理](@entry_id:203967)**（Trace Theorem）是解决这一问题的关键。它指出，对于一个具有 Lipschitz 连续边界的域 $\Omega$，存在一个唯一的、连续的[线性算子](@entry_id:149003) $\gamma$（称为**[迹算子](@entry_id:183665)**），可以将 $H^1(\Omega)$ 中的函数映射到边界上的[函数空间](@entry_id:143478) $H^{1/2}(\partial\Omega)$ 中。这里的 $H^{1/2}$ 是一个分数阶 Sobolev 空间，其光滑性介于 $L^2$ (平方可积) 和 $H^1$ 之间。该算子是满射的，意味着任何 $H^{1/2}$ 空间中的边界函数都可以作为某个 $H^1$ 域内函数的“迹” [@problem_id:2662863]。

基于[迹定理](@entry_id:203967)，我们可以精确定义[弱形式](@entry_id:142897)所涉及的函数空间：
- **容许位移空间 (Trial Space)**：$V = \{ \boldsymbol{v} \in [H^1(\Omega)]^d : \gamma_{\Gamma_u}(\boldsymbol{v}) = \bar{\boldsymbol{u}} \}$。为了使这个空间非空，我们必须要求给定的边界位移 $\bar{\boldsymbol{u}}$ 属于[迹空间](@entry_id:756085)，即 $\bar{\boldsymbol{u}} \in [H^{1/2}(\Gamma_u)]^d$。
- **检验函数空间 (Test Space)**：$V_0 = \{ \boldsymbol{v} \in [H^1(\Omega)]^d : \gamma_{\Gamma_u}(\boldsymbol{v}) = \boldsymbol{0} \}$。这是一个闭合的[线性子空间](@entry_id:151815)。

对于载荷项，为了确保[弱形式](@entry_id:142897)右端的[线性泛函](@entry_id:276136) $\ell(\boldsymbol{v})$ 在 $V_0$ 上是连续的，载荷数据也需要满足一定的**正则性**（regularity）要求。最弱的（即最一般的）假设是载荷项属于检验函数空间的[对偶空间](@entry_id:146945)。这意味着[体力](@entry_id:174230) $\boldsymbol{f}$ 应属于 $[H^{-1}(\Omega)]^d$，而牵[引力](@entry_id:175476) $\bar{\boldsymbol{t}}$ 应属于 $[H^{-1/2}(\Gamma_t)]^d$ [@problem_id:2662859]。这些负指数空间包含了比[平方可积函数](@entry_id:200316)更广义的[分布](@entry_id:182848)，例如点载荷。

### 刚体位移的角色：强制性与唯一性

弱形式 $a(\boldsymbol{u}, \boldsymbol{v}) = \ell(\boldsymbol{v})$ 的[解的存在唯一性](@entry_id:177406)通常由 **Lax-Milgram 定理**保证。该定理的一个核心条件是双线性形式 $a(\cdot, \cdot)$ 在[检验函数](@entry_id:166589)空间 $V_0$ 上是**强制的**（coercive），即存在常数 $\alpha > 0$ 使得对于所有 $\boldsymbol{v} \in V_0$ 都有 $a(\boldsymbol{v}, \boldsymbol{v}) \ge \alpha \|\boldsymbol{v}\|_{[H^1(\Omega)]^d}^2$。

弹性[双线性形式](@entry_id:746794) $a(\boldsymbol{v}, \boldsymbol{v}) = \int_{\Omega} \boldsymbol{\varepsilon}(\boldsymbol{v}) : \mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{v}) d\Omega$ 度量了物体的[应变能](@entry_id:162699)。由于材料是正定的，我们有 $a(\boldsymbol{v}, \boldsymbol{v}) \ge c_0 \|\boldsymbol{\varepsilon}(\boldsymbol{v})\|_{[L^2(\Omega)]^{d \times d}}^2$。强制性是否成立，关键在于应变范数 $\|\boldsymbol{\varepsilon}(\boldsymbol{v})\|_{L^2}$ 是否能控制整个 $H^1$ 范数 $\|\boldsymbol{v}\|_{H^1}$。

这个问题的答案与**刚体位移**（rigid-body motion）密切相关。刚体位移 $\boldsymbol{r}(\boldsymbol{x})$（平移和无穷小转动）的特征是其应变张量为零，$\boldsymbol{\varepsilon}(\boldsymbol{r}) = \boldsymbol{0}$。因此，对于任何非零的刚体位移，其[应变能](@entry_id:162699) $a(\boldsymbol{r}, \boldsymbol{r})$ 为零，但其 $H^1$ 范数不为零。这就破坏了强制性。

不同类型的边界值问题在此表现出根本差异 [@problem_id:2662907] [@problem_id:2662880]：

1.  **纯 Neumann 问题** ($\Gamma_u = \emptyset$)：检验函数空间为整个 $[H^1(\Omega)]^d$，它包含了所有刚体位移。因此，[双线性形式](@entry_id:746794) $a(\cdot, \cdot)$ 不是强制的。这意味着：
    -   **唯一性丧失**：如果 $\boldsymbol{u}$ 是一个解，那么 $\boldsymbol{u} + \boldsymbol{r}$（其中 $\boldsymbol{r}$ 是任意刚体位移）也是一个解。解在相差一个刚体位移的意义下是唯一的。
    -   **存在性条件**：为了保证解的存在，外载荷必须与刚体位移动[解耦](@entry_id:637294)，即外力的合力和[合力矩](@entry_id:166772)必须为零。

2.  **纯 [Dirichlet 问题](@entry_id:274408)** ($\Gamma_u = \partial\Omega$)：检验函数空间为 $[H_0^1(\Omega)]^d$，其中的函数在整个边界上为零。这个空间不包含任何非零的刚体位移。**Korn 第一不等式**保证了在此空间上强制性成立，因此解存在且唯一。

3.  **[混合问题](@entry_id:634383)** (meas$(\Gamma_u) > 0$)：只要位移边界 $\Gamma_u$ 的测度（长度或面积）为正，任何在 $\Gamma_u$ 上为零的非平凡刚体位移都不存在。因此，[检验函数](@entry_id:166589)空间 $V_0$ 中不包含刚体位移模式。**Korn 第二不等式**的推广形式确保了在这样的空间上强制性成立。因此，混合[边值问题](@entry_id:193901)的解是存在且唯一的，无需附加任何对载荷的约束条件。值得注意的是，仅仅在一个点或一条线上（在三维中）施加位移约束不足以消除所有刚体位移（例如，绕该点或线的转动仍然可能）[@problem_id:2662907]。

### 高级与替代公式

除了标准的 Dirichlet-Neumann 问题，还存在其他重要的边界条件和求解框架。

#### Robin 边界条件

**Robin 边界条件**是一种混合了 Dirichlet 和 Neumann 条件特征的边界类型。在力学中，它通常用于模拟[弹性地基](@entry_id:186539)或柔性支撑。一个典型的例子是 **Winkler 地基**，它被理想化为在边界 $\Gamma_r$ 上附着的一系列独立的线性弹簧。若弹簧的单位面积刚度为 $\kappa > 0$，其另一端固定，则地基提供的[反作用](@entry_id:203910)力与边界位移 $\boldsymbol{u}$ 成正比，方向相反，即 $-\kappa \boldsymbol{u}$。总的牵引力平衡条件为 [@problem_id:2662867]：
$$
\boldsymbol{\sigma}\boldsymbol{n} + \kappa\boldsymbol{u} = \bar{\boldsymbol{g}}
$$
其中 $\bar{\boldsymbol{g}}$ 是可能存在的外部施加面力。$\kappa$ 的物理单位是力/体积（例如 $\mathrm{N/m^3}$）。在[弱形式](@entry_id:142897)中，这个边界条件会在双线性形式中增加一个边界积分项 $\int_{\Gamma_r} \kappa \boldsymbol{u} \cdot \boldsymbol{v} \, d\Gamma$。这个项的意义非凡：即使没有位移边界（$\Gamma_u = \emptyset$），只要 Robin 边界 $\Gamma_r$ 的测度为正，这一项就能有效地“惩罚”刚体位移，因为它使得任何非零刚体位移的“能量”$a(\boldsymbol{r}, \boldsymbol{r})$ 为正。因此，Robin 边界条件同样能确保双线性形式的强制性，从而保证[解的唯一性](@entry_id:143619) [@problem_id:2662867]。

#### Airy 应力函数 (二维)

对于二维平面问题（平面应力或平面应变），在没有[体力](@entry_id:174230)的情况下，可以引入一个标量函数 $\Phi(x, y)$——**Airy 应力函数**——来自动满足平衡方程。应力分量可以表示为 $\Phi$ 的[二阶偏导数](@entry_id:635213)：
$$
\sigma_{xx} = \frac{\partial^2 \Phi}{\partial y^2}, \quad \sigma_{yy} = \frac{\partial^2 \Phi}{\partial x^2}, \quad \sigma_{xy} = - \frac{\partial^2 \Phi}{\partial x \partial y}
$$
此时，[应力协调方程](@entry_id:184960)（[应变相容性](@entry_id:199659)条件）转化为一个单一的[四阶偏微分方程](@entry_id:176247)，即**双和谐方程**（biharmonic equation）：
$$
\Delta\Delta\Phi = 0
$$
边界条件也需要相应地转化为关于 $\Phi$ 及其导数的条件。例如，在牵[引力](@entry_id:175476)边界 $\Gamma_t$ 上，法向和切向牵[引力](@entry_id:175476) $t_n^*$ 和 $t_s^*$ 可以表示为 $\Phi$ 沿边界的切向 $s$ 和法向 $n$ 的导数。在位移边界 $\Gamma_u$ 上，给定的位移导数则通过[本构关系](@entry_id:186508)与 $\Phi$ 的[二阶导数](@entry_id:144508)联系起来 [@problem_id:2662830]。这种方法将一个矢量问题（求解位移 $\boldsymbol{u}$）转化为一个标量问题（求解 $\Phi$），为解析和半解析求解提供了另一条途径。

#### 混合边界角点的[应力奇异性](@entry_id:166362)

混合边值问题的一个显著特征是，在不同类型边界条件的交界处（例如，Dirichlet 边界与 Neumann 边界的交点），应[力场](@entry_id:147325)往往会表现出**奇异性**（singularity），即应力在理论上趋于无穷大。

以一个二维扇形域为例，其两边分别为 $\theta=0$ 和 $\theta=\alpha$。假设在 $\theta=0$ 边上施加位移约束（如 $w=0$），在 $\theta=\alpha$ 边上施加牵[引力](@entry_id:175476)约束（如 $\tau_{\theta z}=0$），这构成了一个典型的混合边界角点问题。采用 Williams 的[渐近分析](@entry_id:160416)方法，假设角点附近的解具有形式 $w(r, \theta) = r^{\lambda} f(\theta)$，代入控制方程（对于反平面剪切问题是拉普拉斯方程 $\Delta w = 0$）并施加边界条件，可以得到一个关于指数 $\lambda$ 的特征值问题。对于上述 Dirichlet-Neumann 混合边界，解出的[特征值](@entry_id:154894)为 [@problem_id:2662849]：
$$
\lambda = \frac{(2n+1)\pi}{2\alpha}, \quad n=0, 1, 2, \dots
$$
应力分量与位移的梯度成正比，因此与 $r^{\lambda-1}$ 成比例。为了保证有限[应变能](@entry_id:162699)（要求 $\lambda>0$），最小的正[特征值](@entry_id:154894)是当 $n=0$ 时取得的 $\lambda_{min} = \frac{\pi}{2\alpha}$。如果 $\lambda_{min}  1$（即角点角度 $\alpha  \pi/2$），则应力将以 $r^{\lambda_{min}-1}$ 的形式趋于无穷，其中指数为负。这种奇异性是材料的[线性弹性](@entry_id:166983)模型在几何不连续和边界条件突变处的数学产物，对理解结构的断裂和疲劳行为至关重要。