## 引言
在[固体力学](@entry_id:164042)领域，能量方法提供了一种超越传统力平衡分析的深刻且强大的视角。[弹性应变能](@entry_id:202243)与余能作为这一方法的核心，不仅是衡量[材料变形](@entry_id:169356)[储能](@entry_id:264866)的物理量，更是连接[热力学](@entry_id:141121)、[结构分析](@entry_id:153861)与[计算力学](@entry_id:174464)的理论基石。然而，许多学习者在掌握这些概念时，常常难以理解其深刻的[热力学](@entry_id:141121)渊源、两者之间的对偶关系，以及它们在解决复杂工程问题时的真正威力。本文旨在填补这一认知鸿沟，系统地构建从基本原理到前沿应用的完整知识体系。

在接下来的章节中，我们将踏上一段从理论到实践的探索之旅。在“原理与机制”一章，我们将追溯到[热力学](@entry_id:141121)第一和第二定律，揭示[应变能](@entry_id:162699)与[余能](@entry_id:192009)的物理本质和数学形式，并探讨其成立的严格条件。随后，在“应用与交叉学科联系”一章，我们将展示这些能量原理如何作为强大工具，被用于求解结构位移、分析[超静定](@entry_id:178116)系统、预测失稳与断裂，并连接[材料科学](@entry_id:152226)与[非线性力学](@entry_id:178303)等多个领域。最后，通过“动手实践”部分，您将有机会将理论付诸实践，解决具体的工程问题。现在，让我们从最根本的原理开始，深入探索弹性应变能与余能的奥秘。

## 原理与机制

本章旨在深入阐述[弹性应变能](@entry_id:202243)和余能的核心原理与机制。我们将从[热力学](@entry_id:141121)基础出发，建立这些能量度量的物理意义，然后推导它们的数学形式，并探讨其在变分原理（variational principles）和[结构分析](@entry_id:153861)中的应用。我们还将明确这些理论成立所需的条件，并通过具体实例，包括其在[非线性](@entry_id:637147)和有限变形理论中的局限性，来提供一个全面的视角。

### [弹性势能](@entry_id:168893)的[热力学](@entry_id:141121)基础

在[连续介质力学](@entry_id:155125)中，能量概念植根于[热力学](@entry_id:141121)。对于一个经历可逆过程的弹性体，其内部能量、机械功和热量交换之间的关系由热力学第一定律和第二定律共同支配。

首先，单位体积的**内能** $U_{\text{int}}$ 是系统内部所有微观粒子动能和势能的总和。其[微分形式](@entry_id:146747)由吉布斯关系式给出：
$$
dU_{\text{int}} = \sigma_{ij} d\epsilon_{ij} + T dS
$$
其中，$\sigma_{ij}$ 是柯西应力张量，$\epsilon_{ij}$ 是[无穷小应变张量](@entry_id:167211)，$T$ 是绝对温度，$S$ 是单位体积的熵。该式表明，内能的变化来自两部分：系统所做的机械功增量 $\delta W = \sigma_{ij} d\epsilon_{ij}$ 和吸收的热量增量 $\delta Q = T dS$。

然而，在许多工程问题中，我们更关心的是在恒定温度下系统与外界交换的功。为此，我们引入一个重要的热力学势——**亥姆霍兹自由能** $\Psi$。它通过勒让德变换（Legendre transformation）由内能定义：
$$
\Psi = U_{\text{int}} - TS
$$
[亥姆霍兹自由能](@entry_id:136442)的微分形式为：
$$
d\Psi = dU_{\text{int}} - T dS - S dT = (\sigma_{ij} d\epsilon_{ij} + T dS) - T dS - S dT = \sigma_{ij} d\epsilon_{ij} - S dT
$$
这个关系式揭示了[亥姆霍兹自由能](@entry_id:136442)的“自然”变量是应变 $\epsilon$ 和温度 $T$。对于**[等温过程](@entry_id:143096)**（isothermal process），温度保持不变（$dT=0$），此时[亥姆霍兹自由能](@entry_id:136442)的变化恰好等于对系统所做的机械功增量：
$$
d\Psi = \sigma_{ij} d\epsilon_{ij}
$$

另一方面，**弹性应变能** $U$ 被定义为在可逆加载路径中储存在材料内部、可以完全恢复的机械功。因此，其微分形式为：
$$
dU = \sigma_{ij} d\epsilon_{ij}
$$
通过比较[等温过程](@entry_id:143096)中 $d\Psi$ 和 $dU$ 的表达式，我们得出一个至关重要的结论：在可逆的[等温过程](@entry_id:143096)中，[弹性应变能](@entry_id:202243)与[亥姆霍兹自由能](@entry_id:136442)的变化是相同的。如果我们选择在未变形状态下（$\epsilon = 0$）两种能量均为零作为参考态，那么在整个等温加载过程中，它们的值是相等的，即 $U = \Psi$ [@problem_id:2881852]。

与之相对，在**[绝热过程](@entry_id:138150)**（adiabatic process）中，系统与外界没有热量交换（$\delta Q = 0$）。对于一个可逆的绝热过程，熵保持不变（$dS=0$），这被称为[等熵过程](@entry_id:137496)。在这种情况下，吉布斯关系式简化为：
$$
dU_{\text{int}} = \sigma_{ij} d\epsilon_{ij} = dU
$$
这意味着在可逆绝热过程中，[弹性应变能](@entry_id:202243)等于内能（同样，在选择共同的零点参考态后）。区分这两种情况至关重要：在[等温过程](@entry_id:143096)中，$U = \Psi$；在[等熵过程](@entry_id:137496)中，$U = U_{\text{int}}$。混淆这两种情况会导致错误，例如，在温度变化的绝热过程中，由于 $d\Psi = dU - S dT$，通常 $U \neq \Psi$ [@problem_id:2881852]。这些定义共同构成了弹性行为能量描述的[热力学](@entry_id:141121)基石 [@problem_id:2881852]。

### [应变能密度](@entry_id:200085)与[余能](@entry_id:192009)密度

在纯力学框架下，我们通常关注[应力-应变关系](@entry_id:274093)，并由此定义两种核心的能量密度函数：[应变能密度](@entry_id:200085)和余能密度。

**[应变能密度](@entry_id:200085)**（strain energy density），记为 $\psi(\varepsilon)$，定义为从零应变状态加载到当前应变状态 $\varepsilon$ 时，单位体积内储存的弹性应变能。其数学表达式为应力对应变的积分：
$$
\psi(\varepsilon) = \int_0^\varepsilon \sigma : d\varepsilon'
$$
这里使用[张量缩并](@entry_id:193373)符号 $\sigma : d\varepsilon'$ 表示 $\sigma_{ij} d\epsilon'_{ij}$。从定义可知，应力张量是[应变能密度](@entry_id:200085)对应变张量的梯度：
$$
\sigma = \frac{\partial \psi}{\partial \varepsilon}
$$

**[余能](@entry_id:192009)密度**（complementary energy density），记为 $\psi^*(\sigma)$，是通过对[应变能密度](@entry_id:200085) $\psi(\varepsilon)$ 进行[勒让德变换](@entry_id:146727)得到的，其自变量是应力 $\sigma$。变换定义如下：
$$
\psi^*(\sigma) = \sigma : \varepsilon - \psi(\varepsilon)
$$
式中，$\varepsilon$ 需要通过[本构关系](@entry_id:186508)表示为 $\sigma$ 的函数。这一变换的优美之处在于它保留了共轭关系，即应变是[余能](@entry_id:192009)密度对应力的梯度：
$$
\varepsilon = \frac{\partial \psi^*}{\partial \sigma}
$$
从几何上看，在 $\sigma-\varepsilon$ [坐标系](@entry_id:156346)中，$\psi$ 代表了应力-应变曲线下方的面积，而 $\psi^*$ 则代表了曲线与应力轴之间的面积。它们的和 $\psi + \psi^* = \sigma:\varepsilon$ 恰好是[应力与应变](@entry_id:137374)所围成的矩形面积。

为了更具体地理解这一对偶关系，考虑一个一维[非线性弹性](@entry_id:185743)材料，其[本构关系](@entry_id:186508)为[幂律](@entry_id:143404)形式 $\sigma = K \epsilon^n$，其中 $K > 0$ 和 $n > 0$ 是材料常数 [@problem_id:1264798]。
其[应变能密度](@entry_id:200085)为：
$$
\psi(\epsilon) = \int_0^\epsilon K (\epsilon')^n d\epsilon' = \frac{K}{n+1} \epsilon^{n+1}
$$
根据勒让德变换，[余能](@entry_id:192009)密度为：
$$
\psi^*(\sigma) = \sigma \epsilon - \psi(\epsilon) = (K \epsilon^n) \epsilon - \frac{K}{n+1} \epsilon^{n+1} = \frac{n}{n+1} K \epsilon^{n+1}
$$
因此，对于这类材料，余能密度与[应变能密度](@entry_id:200085)的比值为一个常数：
$$
\frac{\psi^*}{\psi} = n
$$
这个简单的例子清晰地展示了两种能量密度的关系。特别地，对于**[线性弹性](@entry_id:166983)材料**，其本构关系为 $\sigma = \mathbb{C} : \varepsilon$，其中 $\mathbb{C}$ 是四阶[刚度张量](@entry_id:176588)。此时 $n=1$。[应变能密度](@entry_id:200085)为二次型：
$$
\psi(\varepsilon) = \int_0^\varepsilon (\mathbb{C}:\varepsilon') : d\varepsilon' = \frac{1}{2} \varepsilon : \mathbb{C} : \varepsilon = \frac{1}{2} \sigma : \varepsilon
$$
代入勒让德变换，我们得到[余能](@entry_id:192009)密度：
$$
\psi^*(\sigma) = \sigma : \varepsilon - \psi(\varepsilon) = \sigma : \varepsilon - \frac{1}{2} \sigma : \varepsilon = \frac{1}{2} \sigma : \varepsilon
$$
因此，对于[线性弹性](@entry_id:166983)材料，[应变能密度](@entry_id:200085)与余能密度数值上是相等的，即 $\psi = \psi^*$ [@problem_id:2881852] [@problem_id:2687964]。这是线性理论中一个非常重要且方便的特性。

### 能量函数的存在性与[凸性](@entry_id:138568)条件

为了使[应变能](@entry_id:162699)和[余能](@entry_id:192009)理论在数学上是完善且在物理上是有意义的，描述材料行为的[刚度张量](@entry_id:176588) $\mathbb{C}$ 必须满足特定的对称性和[正定性](@entry_id:149643)条件 [@problem_id:2675427]。

1.  **对称性 (Symmetry)**：
    - **主对称性 (Major Symmetry)**: $\mathbb{C}_{ijkl} = \mathbb{C}_{klij}$。这个条件是保证应力可以由一个[势函数](@entry_id:176105)（即[应变能密度](@entry_id:200085)）求导得出的充要条件。满足该条件的材料被称为**[超弹性材料](@entry_id:190241)**（hyperelastic material）。没有主对称性，[能量守恒](@entry_id:140514)的变分框架便无法建立。
    - **次对称性 (Minor Symmetries)**: $\mathbb{C}_{ijkl} = \mathbb{C}_{jikl} = \mathbb{C}_{ijlk}$。这些对称性源于[应力张量和应变张量](@entry_id:755512)自身的对称性（$\sigma_{ij}=\sigma_{ji}, \varepsilon_{kl}=\varepsilon_{lk}$），确保对称的应变产生对称的应力。

2.  **正定性 (Positive-Definiteness)**：
    为了保证材料的稳定性，即任何非零应变状态都储存正的应变能，[刚度张量](@entry_id:176588) $\mathbb{C}$ 必须是**正定的**。这意味着对于任何非零的对称[应变张量](@entry_id:193332) $\varepsilon$，下式恒成立：
    $$
    \psi(\varepsilon) = \frac{1}{2} \varepsilon : \mathbb{C} : \varepsilon > 0
    $$
    正定性保证了[应变能密度函数](@entry_id:755490) $\psi(\varepsilon)$ 是一个**严格[凸函数](@entry_id:143075)**（strictly convex function）。这在物理上意味着应力-应变曲线的斜率总是正的，从而保证了在荷载控制下[解的唯一性](@entry_id:143619)和稳定性。

当[刚度张量](@entry_id:176588) $\mathbb{C}$ 是正定的，其[逆矩阵](@entry_id:140380)——柔度张量 $\mathbb{S} = \mathbb{C}^{-1}$——也必然是正定的。因此，[余能](@entry_id:192009)密度函数 $\psi^*(\sigma) = \frac{1}{2} \sigma : \mathbb{S} : \sigma$ 也是一个严格[凸函数](@entry_id:143075)。这些[凸性](@entry_id:138568)条件是[最小势能原理](@entry_id:173340)和[最小余能原理](@entry_id:200382)成立的数学基础 [@problem_id:2675427]。

### [结构力学](@entry_id:276699)中的能量原理

抽象的能量密度概念通过在整个结构体积上积分，转化为描述结构整体行为的宏观能量。

**总[应变能](@entry_id:162699)** $U_{total}$ 和 **总[余能](@entry_id:192009)** $U^*_{total}$ 分别定义为：
$$
U_{total} = \int_V \psi(\varepsilon) \, dV \quad \text{and} \quad U^*_{total} = \int_V \psi^*(\sigma) \, dV
$$
对于杆、梁、轴等一维结构，我们可以通过在[横截面](@entry_id:154995)积分，将三维理论简化。从[应力功率](@entry_id:182907) $\dot{W}_i = \sigma : \dot{\varepsilon}$ 出发，我们可以在[横截面](@entry_id:154995)上积分，识别出[广义力](@entry_id:169699)与其共轭的广义变形率 [@problem_id:2881854]。例如：
-   **轴向拉伸**：轴力 $N$ 与轴线[应变率](@entry_id:154778) $\dot{\varepsilon}_0$ 共轭。
-   **梁的弯曲**：弯矩 $M$ 与曲率变化率 $\dot{\kappa}$ 共轭。
-   **轴的扭转**：扭矩 $T$ 与单位长度扭转角变化率 $\dot{\phi}'$ 共轭。

对于[线性弹性](@entry_id:166983)结构，我们可以方便地用[广义力](@entry_id:169699)来表示单位长度的余能密度。例如，对于弯曲，余能密度为 $\frac{M^2}{2EI}$；对于扭转，为 $\frac{T^2}{2GJ}$。通过沿构件长度积分，可以计算整个结构的总[余能](@entry_id:192009)。例如，对于一个长度为 $L_b$，承受恒定弯矩 $M_0$ 的梁，其总余能为 [@problem_id:2881854]：
$$
U_b^* = \int_0^{L_b} \frac{M_0^2}{2EI} \, dx = \frac{M_0^2 L_b}{2EI}
$$

对于线性弹性系统，总应变能与外力所做的功之间存在一个简单而深刻的关系，即**克拉伯龙定理**（Clapeyron's Theorem）。该定理指出，对于一个承受荷载向量 $\mathbf{P}$ 并产生相应位移向量 $\boldsymbol{\delta}$ 的[线性弹性](@entry_id:166983)体，其储存的总应变能 $U$ 等于外力所做功的一半：
$$
2U = \mathbf{P}^{T} \boldsymbol{\delta}
$$
这个定理非常有用。例如，在一个桁架结构中，如果我们知道外荷载 $\mathbf{P}$，并通过实验测量出加载点的位移 $\boldsymbol{\delta}$，我们就可以直接计算出整个结构储存的总应变能，而无需知道每个杆件的内力或材料属性 [@problem_id:2881873]。

然而，克拉伯龙定理严格依赖于**[线性弹性](@entry_id:166983)**和**[保守系统](@entry_id:167760)**的假设。如果材料行为是[非线性](@entry_id:637147)的或存在[能量耗散](@entry_id:147406)（如塑性变形），这个关系就不再成立。考虑一个[弹塑性](@entry_id:193198)杆，在加载过程中经历了屈服。其加载路径是不可逆的，一部分机械功会转化为热能耗散掉。在这种情况下，外力所做的总功 $W_{\text{actual}}$ 将大于储存在系统中的弹性应变能。与假想的、加载到同样终点的线性弹性系统所做的功 $W_{\text{lin}} = \frac{1}{2}\mathbf{P}^{T}\boldsymbol{\delta}$ 相比，$W_{\text{actual}}$ 会显著更大。这个差值 $\Delta W = W_{\text{actual}} - W_{\text{lin}}$ 正是由于非保守的塑性变形路径所导致的 [@problem_id:2881838]。

### 变分原理与能量定理

能量函数的重要性不仅在于其本身，更在于它们构成了固体力学中强大的变分原理的基础。这些原理将求解复杂的[微分方程](@entry_id:264184)问题转化为求解泛函的极值问题。

#### [最小势能原理](@entry_id:173340)
**总势能** $\Pi(u)$ 定义为总[应变能](@entry_id:162699)与外力[势能](@entry_id:748988)之和。外力[势能](@entry_id:748988)是外力所做功的负值。对于一个承受体力 $b$ 和面力 $t$ 的物体，其总势能泛函为 [@problem_id:2687964]：
$$
\Pi(u) = \int_V \psi(\varepsilon(u)) \,dV - \int_V b \cdot u \,dV - \int_{\partial_t V} t \cdot u \,dS
$$
**[最小势能原理](@entry_id:173340)**（Principle of Minimum Potential Energy）指出：在所有满足[位移边界条件](@entry_id:203261)（即**[运动学](@entry_id:173318)容许的**）的位移场中，真实的[位移场](@entry_id:141476)使得总势能 $\Pi(u)$ 取最小值。求解 $\delta\Pi = 0$ 会自然地导出平衡方程和力边界条件 [@problem_id:2881859]。

#### [最小余能原理](@entry_id:200382)
与[势能](@entry_id:748988)原理对偶的是[余能原理](@entry_id:168263)。**总余能** $\mathcal{C}(\sigma)$ 泛函定义为：
$$
\mathcal{C}(\sigma) = \int_V \psi^*(\sigma) \, dV
$$
**[最小余能原理](@entry_id:200382)**（Principle of Minimum Complementary Energy）指出：在所有满足平衡方程和力边界条件（即**静力学容许的**）的应[力场](@entry_id:147325)中，真实的应[力场](@entry_id:147325)（也满足协调条件）使得总余能 $\mathcal{C}(\sigma)$ 取最小值 [@problem_id:2675427] [@problem_id:2881859]。

#### [卡氏定理](@entry_id:191013)与克罗蒂-恩格瑟定理
这些变分思想也催生了用于计算位移的强大定理 [@problem_id:2628235]。

-   **克罗蒂-恩格瑟定理 (Crotti-Engesser Theorem)**：对于一个保守的**[非线性弹性](@entry_id:185743)**系统，在力 $P_i$ 作用点沿其方向的位移 $q_i$，等于总余能 $U^*$ 对该力的偏导数：
    $$
    q_i = \frac{\partial U^*}{\partial P_i}
    $$
    这是一个普适的定理，只要材料是弹性的且[应力-应变关系](@entry_id:274093)是单值的。

-   **[卡氏第二定理](@entry_id:176952) (Castigliano's Second Theorem)**：这是一个更著名但[适用范围](@entry_id:636189)更窄的定理。它指出，对于**线性弹性**系统，位移 $q_i$ 等于总应变能 $U$ 对相应力 $P_i$ 的偏导数：
    $$
    q_i = \frac{\partial U}{\partial P_i}
    $$
    [卡氏第二定理](@entry_id:176952)实际上是克罗蒂-恩格瑟定理在[线性弹性](@entry_id:166983)情况下的一个特例。在[线性弹性](@entry_id:166983)系统中，$U=U^*$，因此两个定理的形式变得一致。但在[非线性弹性](@entry_id:185743)情况下，必须使用[余能](@entry_id:192009) $U^*$，因为应变能 $U$ 是位移的函数，不能直接[对力](@entry_id:159909)求导。

### 有限弹性理论中的局限性

虽然[应变能](@entry_id:162699)和余能在线性[小变形理论](@entry_id:174991)中极为成功，但将这些概念，特别是余能，推广到有限变形理论时会遇到根本性的困难 [@problem_id:2881841]。

主要障碍源于**[物质客观性原理](@entry_id:191727)**（principle of material objectivity），也称为标架无关性。该原理要求[应变能密度函数](@entry_id:755490) $\psi$ 对于任意的[刚体转动](@entry_id:191086) $\mathbf{R}$ 必须保持不变，即 $\psi(\mathbf{F}) = \psi(\mathbf{R}\mathbf{F})$，其中 $\mathbf{F}$ 是变形梯度。这一要求使得 $\psi$ 作为 $\mathbf{F}$ 的函数必然是**非凸的**。一个函数如果在某些方向上是常数（如此处绕 $\mathrm{SO}(3)$ 群的作用），它就不可能是严格凸的。例如，对于经典的 Saint Venant-Kirchhoff 模型，虽然在某些变形路径（如简单剪切）上能量函数可能是凸的，但在其他路径（如单轴压缩）上则会显示出非凸性，当[压缩比](@entry_id:136279) $\lambda  1/\sqrt{3}$ 时，能量函数的[二阶导数](@entry_id:144508)会变为负值 [@problem_id:2881841]。

$\psi(\mathbf{F})$ 的非[凸性](@entry_id:138568)意味着从变形到应力的映射（例如 $\mathbf{P} = \partial\psi/\partial\mathbf{F}$）通常不是全局单射的。这意味着可能存在多个不同的变形状态对应同一个应力状态，这使得定义一个全局的、单值的、仅以应力为变量的余能函数成为不可能。

第二个障碍在于**[功共轭](@entry_id:194957)对**（work-conjugate pairs）的选择。在超弹性理论中，[应力功率](@entry_id:182907)（单位参考体积）为 $\dot{W} = \mathbf{P} : \dot{\mathbf{F}}$，表明第一类[皮奥拉-基尔霍夫应力](@entry_id:173629) $\mathbf{P}$ 与变形梯度 $\mathbf{F}$ 是天然的[功共轭](@entry_id:194957)对。然而，柯西应力 $\boldsymbol{\sigma}$ 并非 $\mathbf{F}$ 的[功共轭](@entry_id:194957)。尝试对 $\psi(\mathbf{F})$ 关于一个非共轭的变量（如 $\boldsymbol{\sigma}$）进行勒让德变换，在概念上是不成立的。

综上所述，虽然在线性弹性理论中，[余能](@entry_id:192009)是一个与[应变能](@entry_id:162699)对偶且同样强大的工具，但在有限弹性理论的通用框架下，由于物质客观性导致的非[凸性](@entry_id:138568)和[功共轭](@entry_id:194957)对的不匹配，我们无法像在线性理论中那样，轻易地定义一个以柯西应力为变量的全局[余能](@entry_id:192009)函数。这促使研究者们发展了更复杂的理论，如基于其他应力-应变对（如第二类 P-K 应力 $\mathbf{S}$ 与[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$）的能量函数，或引入更弱的凸性概念如[多凸性](@entry_id:185154)（polyconvexity）。