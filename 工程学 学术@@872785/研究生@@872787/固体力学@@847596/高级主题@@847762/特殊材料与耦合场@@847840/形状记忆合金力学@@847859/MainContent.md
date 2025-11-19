## 引言
[形状记忆合金](@entry_id:141110)（Shape Memory Alloys, SMAs）是一类非凡的智能材料，以其独特的“记忆”能力和卓越的弹性而闻名于世。这些材料所表现出的[形状记忆效应](@entry_id:160076)和超弹性行为，使其能够在经受巨[大变形](@entry_id:167243)后恢复原始形状，为从微创医疗器械到自适应航空航天结构的众多高科技领域带来了革命性的解决方案。然而，这种非凡行为的背后是复杂的、高度[非线性](@entry_id:637147)的热-力耦合物理过程，这给工程师和科学家的精确预测和设计带来了巨大挑战。

本文旨在系统地揭示[形状记忆合金力学](@entry_id:190042)行为的内在机理，填补基础物理与工程应用之间的知识鸿沟。我们将通过一个逻辑递进的结构，引导读者深入理解这一迷人材料的科学与工程。首先，在“原理与机制”一章中，我们将奠定坚实的理论基础，从[相变](@entry_id:147324)的[热力学](@entry_id:141121)和[晶体学](@entry_id:140656)本质出发，构建一个严谨的[连续介质力学](@entry_id:155125)框架，以数学语言描述其宏观响应。接着，在“应用与交叉学科联系”一章中，我们将展示这些理论如何转化为现实世界中的创新应用，探讨SMA在生物医学、航空航天和机器人等领域的关键作用。最后，通过“动手实践”部分提供的一系列计算问题，读者将有机会亲手应用所学知识，巩固对核心概念的理解。通过本次学习，您将能够掌握分析、建模和应用形状记忆合金的核心技能。

## 原理与机制

本章旨在深入探讨[形状记忆合金](@entry_id:141110)（SMA）独特力学行为背后的基本物理原理和数学框架。我们将从[相变](@entry_id:147324)的[热力学](@entry_id:141121)和[晶体学](@entry_id:140656)基础出发，逐步构建一个能够描述其宏观响应的[连续介质力学](@entry_id:155125)模型。本章的目标是为读者提供一个严谨、系统且自洽的理论基础，用以理解和预测[形状记忆效应](@entry_id:160076)与超弹性等关键现象。

### [热弹性](@entry_id:158447)[马氏体相变](@entry_id:158998)

[形状记忆合金](@entry_id:141110)的核心是一种固态[相变](@entry_id:147324)，即**[热弹性](@entry_id:158447)[马氏体相变](@entry_id:158998) (thermoelastic martensitic transformation)**。这是一种在高温下的母相（称为**[奥氏体](@entry_id:161328) (austenite)**）和低温下的产[物相](@entry_id:196677)（称为**马氏体 (martensite)**）之间的可逆转变。奥氏体相通常具有较高的[晶体对称性](@entry_id:198772)（例如，近等原子比[镍钛合金](@entry_id:161931)中的B2立方结构），并且在较高温度下是[热力学](@entry_id:141121)稳定相。相反，马氏体相具有较低的对称性（例如，[镍钛合金](@entry_id:161931)中的B19'单斜结构），在较低温度下更为稳定。

这种[相变](@entry_id:147324)是**无[扩散](@entry_id:141445) (diffusionless)** 和**位移性 (displacive)** 的，意味着它通过原子在[晶格](@entry_id:196752)内的协同剪切运动完成，而非通过长程[原子扩散](@entry_id:159939)。这一特性使其能够快速发生，并保持原子邻接关系，从而为[相变](@entry_id:147324)的可逆性奠定了基础。

在零应力或近似零应力条件下，[相变过程](@entry_id:147919)由温度主导。当从[奥氏体](@entry_id:161328)相开始冷却时，[马氏体相变](@entry_id:158998)在**[马氏体相变](@entry_id:158998)开始温度 ($M_s$)** 时启动，并在**[马氏体相变](@entry_id:158998)完成温度 ($M_f$)** 时结束。在此温度区间内，材料是奥氏体和马氏体的混合物。反之，当对完全马氏体化的材料进行加热时，逆[相变](@entry_id:147324)在**奥氏体[相变](@entry_id:147324)开始温度 ($A_s$)** 启动，并在**奥氏体[相变](@entry_id:147324)完成温度 ($A_f$)** 结束。这些特征温度是材料的固有属性。

一个显著的特征是**[热滞后](@entry_id:154614) (thermal hysteresis)**，即正向[相变](@entry_id:147324)路径与逆向[相变](@entry_id:147324)路径不重合，通常有 $A_s > M_f$ 且 $A_f > M_s$。例如，一种典型的温度排序是 $M_f  M_s  A_s  A_f$。这个滞后环的存在反映了[相变过程](@entry_id:147919)中的[能量耗散](@entry_id:147406)，例如相界面移动时的[摩擦阻力](@entry_id:270342)或微观结构缺陷的钉扎效应。

从[热力学](@entry_id:141121)角度看，[马氏体相变](@entry_id:158998)是一种**[一级相变](@entry_id:155013) (first-order phase transformation)**。这意味着在[相变过程](@entry_id:147919)中，材料的一阶[热力学](@entry_id:141121)量（如熵和体积）会发生不连续的变化。因此，[相变](@entry_id:147324)伴随着**潜热 (latent heat)** 的释放或吸收。在冷却诱发的奥氏体到[马氏体](@entry_id:162117)的正向[相变](@entry_id:147324)中，系统熵降低（$s_M  s_A$），多余的热量以潜热 $L = T(s_A - s_M)$ 的形式释放到环境中（**[放热过程](@entry_id:147168)**）。在加热诱发的逆[相变](@entry_id:147324)中，系统需要从环境中吸收等量的潜热（**[吸热过程](@entry_id:141358)**）。

“[热弹性](@entry_id:158447)”一词强调了驱动力与恢复力之间的精细平衡。[相变过程](@entry_id:147919)中产生的[应变能](@entry_id:162699)（由于新相与母相之间的[晶格](@entry_id:196752)不匹配）以及[界面能](@entry_id:198323)，与化学自由能差（[相变](@entry_id:147324)的驱动力）相抗衡。在SMA中，[应变能](@entry_id:162699)主要通过可逆的**[晶格](@entry_id:196752)不变剪切 (lattice-invariant shear)**（通常是孪生）来调节，而不是通过不可逆的[位错滑移](@entry_id:275474)。这种可恢复的能量储存与释放机制，是实现[形状记忆效应](@entry_id:160076)和[超弹性](@entry_id:159356)的关键，并使得滞后环相对较小 [@problem_id:2661289]。

### [相变](@entry_id:147324)的晶体学与[运动学](@entry_id:173318)

为了在[连续介质力学](@entry_id:155125)框架下对[相变](@entry_id:147324)进行建模，我们必须首先理解其在晶体尺度上的[运动学](@entry_id:173318)。[相变](@entry_id:147324)将母相奥氏体的[晶格](@entry_id:196752)映射到一个或多个几何上等价但取向不同的[马氏体](@entry_id:162117)[晶格](@entry_id:196752)变体。

**[晶格](@entry_id:196752)对应 (Lattice correspondence)** 描述了奥氏体[晶格](@entry_id:196752)如何变形为[马氏体](@entry_id:162117)[晶格](@entry_id:196752)。在数学上，这可以由一个线性映射（即变形梯度张量）$\boldsymbol{C}$ 来表示。通过极分解 $\boldsymbol{C} = \boldsymbol{R}\boldsymbol{U}$，我们可以将其分解为一个纯拉伸（**Bain拉伸 (Bain stretch)**）张量 $\boldsymbol{U}$ 和一个刚体旋转 $\boldsymbol{R}$。对称、正定的张量 $\boldsymbol{U}$ 捕捉了无旋转的纯[晶格](@entry_id:196752)畸变，是描述[相变](@entry_id:147324)应变的核心 [@problem_id:2661335]。例如，在近等原子比NiTi合金从B2[奥氏体](@entry_id:161328)到B19'马氏体的转变中，Bain拉伸虽然导致了显著的形状改变，但体积变化很小（通常是约 $0.3\%$ 至 $0.5\%$ 的收缩），因此在建模中常被近似为保体积的（即 $\det\boldsymbol{U} \approx 1$）[@problem_id:2661335]。

然而，仅有Bain拉伸通常无法在奥氏体和[马氏体](@entry_id:162117)之间形成一个几何兼容的、无畸变的界面。为了维持界面处的原子键连续性，必须存在一种额外的、不改变[晶格类型](@entry_id:269667)的变形，即**[晶格](@entry_id:196752)不变剪切 (lattice-invariant shear)**。在SMA中，这种剪切通常通过在马氏体内部形成精细的**孪晶 (twins)** 来实现。孪生是一种可逆的变形机制，它允许[马氏体](@entry_id:162117)变体在应力作用下重新取向，这是[形状记忆效应](@entry_id:160076)和[超弹性](@entry_id:159356)的微观基础 [@problem_id:2661289]。

当Bain拉伸与[晶格](@entry_id:196752)不变剪切适当地组合后，可以形成一个宏观上无畸变、无旋转的平面，称为**惯习面 (habit plane)**。惯习面的存在是形成锋锐、共格相界面的运动学条件。根据Wechsler-Lieberman-Read (WLR) 和 Ball-James 等晶体学理论，惯习面存在的充分必要条件是，对于给定的Bain拉伸 $\boldsymbol{U}$，能找到一个旋转 $\boldsymbol{R}$、一个形状改变矢量 $\boldsymbol{a}$ 和一个[单位法向量](@entry_id:178851) $\boldsymbol{n}$（即惯习面法矢），使得下式成立 [@problem_id:2661335]：
$$ \boldsymbol{R}\boldsymbol{U} - \boldsymbol{I} = \boldsymbol{a} \otimes \boldsymbol{n} $$
其中 $\boldsymbol{I}$ 是二阶单位张量。这个方程精确地表达了[相变](@entry_id:147324)前后两个[晶格](@entry_id:196752)在惯习面上必须兼容的运动学约束。

在构建宏观本构模型时，通常将单个[马氏体](@entry_id:162117)变体产生的复杂变形简化为一个等效的**[相变](@entry_id:147324)应变张量 (transformation strain tensor)** $\boldsymbol{\epsilon}^{tr}$。在小应变假设下，对于一个特定的变体，其[相变](@entry_id:147324)应变张量常被模型化为一个具有特定方向和大小的对称张量。例如，可以将其表示为一个沿某一方向 $\boldsymbol{m}$ 的[单轴拉伸](@entry_id:188287)，并保持体积不变（即迹为零）[@problem_id:2661335]。这样的简化张量捕捉了[相变](@entry_id:147324)引起的主要形状变化，并成为连接微观[晶体学](@entry_id:140656)和宏观连续介质模型的桥梁。

### 连续介质[热力学](@entry_id:141121)框架

为了发展一个能够预测[SMA力学](@entry_id:190042)行为的数学模型，我们采用基于**内部变量 (internal variables)** 的连续介质[热力学](@entry_id:141121)框架。该框架通过引入描述材料内部微观结构状态的变量，将复杂的多尺度物理过程纳入到一个宏观的、[热力学一致的](@entry_id:755906)理论中。

对于SMA，最核心的内部变量包括：
1.  **马氏体[体积分数](@entry_id:756566) ($\xi$)**: 一个标量，其取值范围为 $\xi \in [0, 1]$，表示材料中[马氏体](@entry_id:162117)相所占的体积分数。$\xi=0$ 对应纯奥氏体，$\xi=1$ 对应纯[马氏体](@entry_id:162117)。
2.  **[相变](@entry_id:147324)[应变张量](@entry_id:193332) ($\boldsymbol{\epsilon}^{tr}$)**: 一个二阶对称张量，表示由于[马氏体](@entry_id:162117)相的形成及变体的[择优取向](@entry_id:190900)而产生的宏观不可逆（但在加热时可恢复）应变。

在小应变理论中，一个关键的假设是**应变加和分解 (additive decomposition of strain)**。总应变张量 $\boldsymbol{\epsilon}$ 被分解为弹性部分 $\boldsymbol{\epsilon}^e$ 和[相变](@entry_id:147324)部分 $\boldsymbol{\epsilon}^{tr}$ [@problem_id:2661326]：
$$ \boldsymbol{\epsilon} = \boldsymbol{\epsilon}^e + \boldsymbol{\epsilon}^{tr} $$
如果考虑温度变化，还需加入[热应变](@entry_id:187744)项 $\boldsymbol{\epsilon}^{th} = \alpha(T-T_0)\boldsymbol{I}$。[弹性应变](@entry_id:189634) $\boldsymbol{\epsilon}^e$ 是可恢复的，并与应力 $\boldsymbol{\sigma}$ 通过弹性本构关系（如胡克定律）相关联：$\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\epsilon}^e$，其中 $\mathbb{C}$ 是[四阶弹性张量](@entry_id:188318)。

所有[本构关系](@entry_id:186508)都必须满足[热力学第二定律](@entry_id:142732)，通常以**克劳修斯-杜亥姆不等式 (Clausius-Duhem inequality)** 的形式表达。对于单位质量的物质，其局部形式为 [@problem_id:2661336]：
$$ \boldsymbol{\sigma}:\dot{\boldsymbol{\epsilon}} - \rho(\dot{\psi} + s\dot{T}) \ge 0 $$
这里，$\rho$ 是密度，$\psi$ 是单位质量的[亥姆霍兹自由能](@entry_id:136442)，$s$ 是单位质量的熵，上标点表示材料时间导数。不等式的左边代表了单位体积的**内禀耗散 (intrinsic dissipation)**，它必须是非负的。

通过引入[亥姆霍兹自由能](@entry_id:136442)作为状态变量的函数，例如 $\psi = \psi(\boldsymbol{\epsilon}^e, T, \xi, \boldsymbol{\epsilon}^{tr})$，并应用Coleman-Noll程序，我们可以从[耗散不等式](@entry_id:188634)中系统地导出[本构关系](@entry_id:186508)。该程序假定不等式必须对所有可能的[热力学过程](@entry_id:141636)都成立，从而得到两类关系：
1.  **无耗散的[本构关系](@entry_id:186508)**: 应力和熵可以由自由能对相应的状态变量求导得出：
    $$ \boldsymbol{\sigma} = \rho \frac{\partial \psi}{\partial \boldsymbol{\epsilon}^e}, \quad s = -\frac{\partial \psi}{\partial T} $$
2.  **简化的[耗散不等式](@entry_id:188634)**: 剩下的项构成了对内部变量演化的约束。
    $$ \mathcal{D}_{mech} = \boldsymbol{X}_{tr} : \dot{\boldsymbol{\epsilon}}^{tr} + Y_{\xi} \dot{\xi} \ge 0 $$
此不等式揭示了与内部变量[演化速率](@entry_id:202008)（“通量”）$\dot{\boldsymbol{\epsilon}}^{tr}$ 和 $\dot{\xi}$ 共轭的**[热力学力](@entry_id:161907) (thermodynamic forces)**（“驱动力”）$\boldsymbol{X}_{tr}$ 和 $Y_{\xi}$。这些力由应力[状态和](@entry_id:193625)自由能对内部变量的[偏导数](@entry_id:146280)决定。例如，在一个典型的模型中，这些力可以被确定为 [@problem_id:2661336]：
$$ \boldsymbol{X}_{tr} = \boldsymbol{\sigma} - \rho \frac{\partial \psi_{int}}{\partial \boldsymbol{\epsilon}^{tr}}, \quad Y_{\xi} = -\rho \frac{\partial \psi_{int}}{\partial \xi} $$
其中 $\psi_{int}$ 是自由能中与内部变量演化相关的部分。这个框架确保了任何描述[相变](@entry_id:147324)演化的本构律（即内部变量的演化方程）都将是[热力学一致的](@entry_id:755906)。

### [本构模型](@entry_id:174726)：能量与耗散

在[热力学](@entry_id:141121)框架内，具体的材料行为由[亥姆霍兹自由能](@entry_id:136442) $\psi$ 的函数形式和耗散的演化规律共同决定。

#### 自由能的构建

为了构建一个实际可用的模型，通常将单位体积的自由能 $\psi$ 分解为几个物理意义明确的部分 [@problem_id:2661292]：
$$ \psi(\boldsymbol{\epsilon}^e, T, \xi, \boldsymbol{\epsilon}^{tr}) = \psi^e(\boldsymbol{\epsilon}^e, T) + \psi^{ch}(\xi, T) + \psi^{hd}(\xi, \boldsymbol{\epsilon}^{tr}) $$
1.  **弹性[储能](@entry_id:264866) ($\psi^e$)**: 这是与[材料弹性](@entry_id:751729)变形相关的能量，通常采用二次型形式 $\psi^e = \frac{1}{2}\boldsymbol{\epsilon}^e : \mathbb{C}(T) : \boldsymbol{\epsilon}^e$。它还包含与比热相关的纯热学项。
2.  **化学能 ($\psi^{ch}$)**: 这部分能量描述了[奥氏体](@entry_id:161328)和[马氏体](@entry_id:162117)相的[相对稳定性](@entry_id:262615)。它通常是温度 $T$ 的函数，并被构造成在高温下使[奥氏体](@entry_id:161328)相（$\xi=0$）能量更低，而在低温下使马氏体相（$\xi=1$）能量更低。一个简单的形式是 $\psi^{ch} \propto - \ell(T-T_0)\xi$，其中 $\ell$ 是与[相变](@entry_id:147324)熵变相关的常数。
3.  **硬化能 ($\psi^{hd}$)**: 这部分能量描述了[相变过程](@entry_id:147919)中由于内部应力、微观结构交互或[相变](@entry_id:147324)应变的累积而产生的能量储存。它可以引入各向同性或[运动学](@entry_id:173318)硬化，例如通过包含 $\xi^2$ 或 $\boldsymbol{\epsilon}^{tr}:\boldsymbol{\epsilon}^{tr}$ 这样的项，甚至可以是 $\xi$ 和 $\boldsymbol{\epsilon}^{tr}$ 的耦合项 [@problem_id:2661326, @problem_id:2661292]。

为了保证模型的数学**[适定性](@entry_id:148590) (well-posedness)** 和物理稳定性，[自由能函数](@entry_id:749582)必须满足特定的数学条件。首先，在任何固定温度下，$\psi$ 必须是其力学[状态变量](@entry_id:138790)（如 $\boldsymbol{\epsilon}^e, \xi, \boldsymbol{\epsilon}^{tr}$）的**[凸函数](@entry_id:143075) (convex function)**。这确保了在给定的边界条件下，[平衡解](@entry_id:174651)存在且唯一。例如，这意味着[弹性张量](@entry_id:170728) $\mathbb{C}$ 必须是正定的，并且硬化能 $\psi^{hd}$ 相对于其变量的Hessian矩阵必须是半正定的。对于包含耦合项的复杂硬化能，这可能需要通过舒尔补（Schur complement）条件来检验 [@problem_id:2661292]。其次，为了保证热稳定性（即比热为正），$\psi$ 必须是温度 $T$ 的**[凹函数](@entry_id:274100) (concave function)**，即 $\partial^2\psi/\partial T^2 \le 0$ [@problem_id:2661292]。

#### 宏观行为的起源

构建了自由能之后，我们便可以解释SMA的标志性力学行为。

**应力平台**: [超弹性](@entry_id:159356)行为中的应力平台源于系统自由能的**非[凸性](@entry_id:138568) (non-convexity)**。在一个简化的单轴模型中，总能量可以被看作是应变 $\varepsilon$ 的函数，它具有两个“能量阱”：一个对应[奥氏体](@entry_id:161328)相（在 $\varepsilon=0$ 附近），另一个对应马氏体相（在 $\varepsilon=\epsilon_L$ 附近）。当宏观应变处于两个能量阱之间时，均匀变形会导致能量过高，因而是不稳定的。为了最小化总能量，材料会自发形成奥氏体和[马氏体](@entry_id:162117)的**精细混合物 (fine mixture)**。在平衡状态下，两个相的应力必须相等，并且它们的化学势也必须相等。这在能量-应变图上对应于**[公切线构造](@entry_id:187353) (common-tangent construction)**。公[切线的斜率](@entry_id:192479)即为宏观上观察到的恒定应力，即**平台应力 (plateau stress)** 或[麦克斯韦应力](@entry_id:199347)。对于一个具有相同弹性模量 $E$ 的简单双阱模型，平台应力 $\sigma_p$ 直接与两相的化学能差 $\Delta g$ 和[相变](@entry_id:147324)应变 $\epsilon_L$ 相关：$\sigma_p = \Delta g / \epsilon_L$ [@problem_id:2661309]。

**滞后现象**: 实验观察到的应力-应变回线是一个滞后环，加载平台应力高于卸载平台应力。这表明[相变过程](@entry_id:147919)是耗散的。这种**率无关滞后 (rate-independent hysteresis)** 的根源在于相变过程中克服内部阻力所做的功。这些阻力可能源于相界面的移动（类似于干摩擦）、新相的形核能垒或微观缺陷的钉扎效应。

在理论模型中，这种耗散通过为内部变量的演化引入一个**耗散势 (dissipation potential)** 来描述。一个率无关的耗散过程可以通过一个在原点处不可导（非光滑）、正一阶齐次的凸函数来建模。这种数学结构会产生一个演化阈值：只有当[热力学](@entry_id:141121)驱动力达到某个临界值时，[相变](@entry_id:147324)才能发生。这个临界阈值的存在，导致加载和卸载路径不同，从而形成一个即使在加载速率趋于零时也不会消失的滞后环。这与[线性粘弹性](@entry_id:181219)材料的滞后行为有本质区别，后者的滞后环面积与加载频率成正比，在准[静态极限](@entry_id:262480)下会消失 [@problem_id:2661342]。总耗散（即滞后环的面积）等于在一个完整加载-卸载循环中，[热力学力](@entry_id:161907)对内部变量速率所做的总功 $\oint Y \dot{\xi} dt$ [@problem_id:2661342]。

### 连接[热力学](@entry_id:141121)、力学与实验

理论模型不仅要能定性解释现象，还必须与实验测量结果定量地联系起来。

#### 克劳修斯-克拉佩龙关系

应力诱导[相变](@entry_id:147324)的温度依赖性为我们提供了一个连接力学和[热力学](@entry_id:141121)量的强大工具。在应力-温度相图上，奥氏体和[马氏体](@entry_id:162117)的平衡共存线由**克劳修斯-克拉佩龙关系 (Clausius-Clapeyron relation)** 描述。对于单轴应力下的固-固[相变](@entry_id:147324)，该关系为：
$$ \frac{d\sigma}{dT} = \frac{\Delta s}{\Delta\epsilon} $$
其中 $d\sigma/dT$ 是[相变](@entry_id:147324)应力随温度变化的斜率，$\Delta s$ 是单位体积的[相变](@entry_id:147324)[熵变](@entry_id:138294)，$\Delta\epsilon$ 是[相变](@entry_id:147324)应变。由于从[奥氏体](@entry_id:161328)到[马氏体](@entry_id:162117)的正向[相变](@entry_id:147324)是放热的，熵减小（$\Delta s = s_M - s_A  0$）。对于拉伸应力诱导的[相变](@entry_id:147324)，[相变](@entry_id:147324)应变通常为正（$\Delta\epsilon  0$）。然而，在SMA中，实验观察到[相变](@entry_id:147324)应力随温度升高而增加（$d\sigma/dT  0$），这表明上述公式需要仔细定义符号。若定义 $\Delta s_{vol} = s_M - s_A$ 和 $\Delta \epsilon = \epsilon_M - \epsilon_A = \epsilon_L  0$，则关系式应为 $d\sigma/dT = -\Delta s_{vol}/\epsilon_L$。考虑到 $\Delta s_{vol}$ 为负，斜率便为正。此关系式允许我们通过测量力学量（$d\sigma/dT$ 和 $\epsilon_L$）来推断[热力学](@entry_id:141121)量（$\Delta s$），反之亦然。例如，通过力学实验测得的熵变值，可以与通过[差示扫描量热法](@entry_id:151282)（DSC）直接测量的潜热计算出的熵变进行比较，以验证模型的一致性 [@problem_id:2661291]。

#### [相变](@entry_id:147324)准则与不对称性

为了预测在多轴应力状态下[相变](@entry_id:147324)何时发生，我们需要定义一个**[相变](@entry_id:147324)[曲面](@entry_id:267450) (transformation surface)**，这类似于塑性力学中的屈服[曲面](@entry_id:267450)。当应力状态达到该[曲面](@entry_id:267450)时，[相变](@entry_id:147324)启动。

一个简单的方法是基于[相变过程](@entry_id:147919)中的机械功。[相变](@entry_id:147324)驱动力的力学部分为 $\boldsymbol{\sigma}:\Delta\boldsymbol{\epsilon}^{tr}$，其中 $\Delta\boldsymbol{\epsilon}^{tr}$ 是[相变](@entry_id:147324)应变张量。一个类似施密特（Schmid）的准则可以写成 $Y(\boldsymbol{\sigma}) = \boldsymbol{\sigma}:\Delta\boldsymbol{\epsilon}^{tr}/\epsilon_L = Y_c(T)$，其中 $Y_c(T)$ 是临界驱动力。然而，这个准则对于应力反号是对称的，即它预测的拉伸和压缩下的临界应力大小相同。

实验表明，许多SMA表现出显著的**[拉压不对称性](@entry_id:201728) (tension-compression asymmetry)**，即在拉伸和压缩下启动[相变](@entry_id:147324)的临界应力不同。这种现象源于**[非施密特效应](@entry_id:188957) (non-Schmid effects)**，即[相变](@entry_id:147324)的激活不仅取决于沿[相变](@entry_id:147324)剪切方向的分解剪应力，还可能受到其他应力分量的影响，如[静水压力](@entry_id:275365)或惯习面上的[正应力](@entry_id:260622)。

为了在模型中引入这种不对称性，我们需要在[相变](@entry_id:147324)准则中加入对应力张量 $\boldsymbol{\sigma}$ 的奇函数项。这些项必须是标量且满足标架无关性。两种常见的做法是 [@problem_id:2661274]：
1.  **引入[静水压力](@entry_id:275365)项**: 在驱动力中加入与[应力张量](@entry_id:148973)的第一[不变量](@entry_id:148850) $I_1(\boldsymbol{\sigma}) = \mathrm{tr}(\boldsymbol{\sigma})$ 成正比的项。[相变](@entry_id:147324)准则形如：$|Y(\boldsymbol{\sigma})| + \beta I_1(\boldsymbol{\sigma}) = Y_c(T)$。由于 $I_1(-\boldsymbol{\sigma}) = -I_1(\boldsymbol{\sigma})$，该项在拉伸和压缩下符号相反，从而导致不对称性。
2.  **引入其他剪切-[正应力](@entry_id:260622)耦合项**: 加入诸如 $\boldsymbol{\sigma}:\boldsymbol{n}\otimes\boldsymbol{m}$ 形式的项，其中 $\boldsymbol{n}$ 和 $\boldsymbol{m}$ 是与[相变](@entry_id:147324)系统相关的特定方向（如惯习面法向和剪切方向）。这样的项同样对应力反号敏感。

### 从单晶到多晶

以上讨论大多基于单晶或单一[相变](@entry_id:147324)系统。然而，工程中使用的SMA通常是**[多晶体](@entry_id:139228) (polycrystals)**，由大量取向随机或具有织构的晶粒组成。多晶体的宏观力学行为是其内部所有晶粒复杂相互作用的平均结果。从单晶[本构模型](@entry_id:174726)预测多晶行为，是[材料力学](@entry_id:201885)中的一个核心挑战，通常通过**均匀化 (homogenization)** 方法来解决。

一些经典的均匀化方案可以用来估算多晶SMA在某一时刻的**有效[切线](@entry_id:268870)模量 (effective tangent modulus)** [@problem_id:2661325]：
1.  **Voigt模型**: 假设所有晶粒的应变场均匀且等于宏观应变（**[等应变](@entry_id:184570)假设**）。这导致[有效模量](@entry_id:748818)是各相（或各晶粒）模量的[体积分数](@entry_id:756566)加权算术平均。Voigt估计通常是[有效弹性模量](@entry_id:181086)的**上限**。
2.  **Reuss模型**: 假设所有晶粒的应[力场](@entry_id:147325)均匀且等于宏观应力（**[等应力](@entry_id:204402)假设**）。这导致有效柔度是各相柔度的加权算术平均，因此[有效模量](@entry_id:748818)是模量的加权调和平均。Reuss估计通常是[有效弹性模量](@entry_id:181086)的**下限**。
3.  **自洽 (Self-consistent) 模型**: 此模型将每个晶粒视为一个嵌入在未知有效介质中的夹杂物，然后要求夹杂物的响应平均后能自洽地再现这个有效介质的属性。自洽估计值通常介于[Voigt和Reuss界](@entry_id:171021)之间，被认为对于中等[体积分数](@entry_id:756566)的[相混合](@entry_id:199798)物更准确。

在应用这些模型时，至关重要的一点是区分**有效弹性[切线](@entry_id:268870)模量**和**[算法切线模量](@entry_id:199979) (algorithmic tangent modulus)**。前者描述了在微观结构（如相分数 $\xi$）“冻结”的瞬间，材料的纯弹性响应。而后者是宏观应力增量与总应变增量之比，它包含了由于内部变量演化（即[相变](@entry_id:147324)正在发生）所引起的“软化”效应。在超弹性应力平台上，尽管材料的弹性模量（如Voigt或Reuss估计）是有限的正值，但由于[相变](@entry_id:147324)持续进行，宏观应力几乎不增加，导致[算法切线模量](@entry_id:199979)非常小，甚至接近于零。因此，[算法切线模量](@entry_id:199979)通常会远低于Reuss下限 [@problem_id:2661325]。理解这一区别对于开发稳定可靠的数值模拟（如[有限元分析](@entry_id:138109)）至关重要。