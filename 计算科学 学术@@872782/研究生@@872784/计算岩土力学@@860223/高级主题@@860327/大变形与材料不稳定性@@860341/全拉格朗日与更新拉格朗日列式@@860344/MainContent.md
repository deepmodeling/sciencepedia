## 引言
在计算岩[土力学](@entry_id:180264)领域，精确模拟如土体滑坡、地基大沉降及隧道开挖等现象，是工程师和研究者面临的核心挑战。这些过程的共同特征是材料会经历显著的几何形状变化和[应力重分布](@entry_id:190225)，即“[大变形](@entry_id:167243)”或“有限应变”效应。在这种情况下，传统的基于小应变假设的线性理论将不再适用，因为它无法捕捉大转动和应力强化等关键的[几何非线性](@entry_id:169896)行为，从而导致分析结果出现严重偏差。为了克服这一知识鸿沟，[连续介质力学](@entry_id:155125)提供了更为普适的运动学框架。

本文聚焦于解决有限变形问题的两种基石性数值方法：**全拉格朗-日（Total Lagrangian, TL）**和**更新拉格朗日（Updated Lagrangian, UL）**列式。这两种方法从不同视角描述物体的运动和变形，但最终殊途同归，为复杂的[非线性](@entry_id:637147)问题提供了严谨的求[解路径](@entry_id:755046)。通过学习本文，您将系统地掌握这两种方法的核心思想和数学构造。

在接下来的章节中，我们将首先在“**原理与机制**”中，从最基本的运动学出发，建立变形梯度、有限[应变张量](@entry_id:193332)以及柯西应力与[皮奥拉-基尔霍夫应力](@entry_id:173629)等关键物理量，并揭示它们如何通过虚功原理统一在TL和UL两种不同的[有限元列式](@entry_id:164720)中。随后，“**应用与[交叉](@entry_id:147634)学科联系**”一章将通过岩土工程中的具体实例，如边坡失稳、有限应变固结和高等本构模型的实现，深入剖析两种方法的适用场景、优势与挑战。最后，“**动手实践**”部分将提供一系列精心设计的计算和编程练习，帮助您将理论知识转化为解决实际问题的能力，从而真正内化这两种强大的分析工具。

## 原理与机制

在处理诸如土体滑坡、[地基沉降](@entry_id:755031)或隧道开挖等岩[土力学](@entry_id:180264)问题时，材料往往会经历[大变形](@entry_id:167243)，其几何形状和内部应力状态发生显著改变。为了在[数值模拟](@entry_id:137087)中精确地捕捉这些效应，我们需要采用能够处理有限变形的[运动学](@entry_id:173318)框架。在本章中，我们将深入探讨两种在[计算力学](@entry_id:174464)中占有核心地位的列式方法：**全拉格朗日 (Total Lagrangian, TL)** 和 **更新拉格朗日 (Updated Lagrangian, UL)** 列式。我们将从最基本的运动学和动力学原理出发，系统地建立这两种方法所需的应变和应力度量，阐明它们之间的内在联系，并最终揭示它们在有限元法中实现的具体机制。

### 变形与运动：运动学基础

描述一个连续体的运动，首先需要定义它的构型。我们通常将物体在初始时刻 $t=0$ 所占据的、通常是无应力的状态，称为**参考构型 (reference configuration)**，记为 $B_0$。物体中的任意一个物[质点](@entry_id:186768)在参考构型中的位置由**物质坐标 (material coordinates)** $\mathbf{X}$ 描述。随着时间的推移，物体运动并变形，在任意时刻 $t$ 占据的空间区域称为**当前构型 (current configuration)**，记为 $B_t$。该物质点在当前构型中的位置由**空间坐标 (spatial coordinates)** $\mathbf{x}$ 描述。

连接这两个构型的桥梁是**运动映射 (motion map)** $\boldsymbol{\varphi}$，它描述了每个物质点随时间变化的轨迹：
$$
\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)
$$
为了量化物质点邻域内的局部变形，我们引入一个至关重要的物理量：**变形梯度 (deformation gradient)** $\mathbf{F}$。它被定义为当前位置对[参考位](@entry_id:754187)置的梯度：
$$
\mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}} = \nabla_X \mathbf{x}
$$
变形梯度 $\mathbf{F}$ 是有限变形理论的基石，它包含了关于局部拉伸、剪切和旋转的全部信息。它作为一个线性变换算子，建立了参考构型和当前构型中微分几何元素之间的联系 [@problem_id:3568051]。

- **[线元](@entry_id:196833)映射**: 参考构型中的一个无限小物质[线元](@entry_id:196833) $d\mathbf{X}$，在变形后会映射为当前构型中的线元 $d\mathbf{x}$，它们之间的关系由 $\mathbf{F}$ 直接给出：
  $$
  d\mathbf{x} = \mathbf{F} d\mathbf{X}
  $$

- **体积元映射**: 参考构型中的一个无限小[体积元](@entry_id:267802) $dV$，在变形后会映射为当前构型中的体积元 $dv$。它们之间的体积变化比率由 $\mathbf{F}$ 的[行列式](@entry_id:142978)，即 **雅可比行列式 (Jacobian determinant)** $J = \det(\mathbf{F})$ 决定：
  $$
  dv = J dV
  $$
  为了保证物理上的合理性（即物质不会相互穿透或凭空消失），我们要求 $J \gt 0$。

- **[面积元](@entry_id:263205)映射**: 两个构型中面积元之间的关系更为复杂，由著名的 **[南森公式](@entry_id:195566) (Nanson's formula)** 描述。设 $d\mathbf{A} = \mathbf{N} dA$ 是参考构型中的一个[有向面积](@entry_id:169588)元（其中 $\mathbf{N}$ 为[单位法向量](@entry_id:178851)， $dA$ 为面积），其在当前构型中的对应量为 $d\mathbf{a} = \mathbf{n} da$。它们之间的关系为：
  $$
  \mathbf{n} da = J \mathbf{F}^{-T} \mathbf{N} dA
  $$
  其中 $\mathbf{F}^{-T}$ 表示 $\mathbf{F}$ 的逆之[转置](@entry_id:142115)。这个公式在推导不同应力度量之间的关系时至关重要。

为了更深入地理解变形的物理本质，我们可以使用**极分解 (polar decomposition)** 定理将变形梯度分解为一个纯拉伸和一个纯旋转的相继作用 [@problem_id:3568009]。对于任何满足 $J \gt 0$ 的 $\mathbf{F}$，存在唯一的[对称正定](@entry_id:145886)张量 $\mathbf{U}$ (右[拉伸张量](@entry_id:193200)) 和唯一的正交张量 $\mathbf{R}$ ([旋转张量](@entry_id:191990))，使得：
$$
\mathbf{F} = \mathbf{R} \mathbf{U}
$$
这个分解清晰地表明，任何复杂的局部变形都可以看作是首先对物质进行拉伸和剪切（由 $\mathbf{U}$ 描述），然后再进行一次刚体旋转（由 $\mathbf{R}$ 描述）。这一思想是建立[客观应变度量](@entry_id:752864)的关键。

### 有限变形中的[应变度量](@entry_id:755495)

当变形很小时，我们通常使用线性化的[应变张量](@entry_id:193332)。但在岩土材料的[大变形分析](@entry_id:163435)中，线性应变不再适用，因为它无法正确处理大转动。我们需要能够精确衡量有限变形的[应变度量](@entry_id:755495)。

#### 拉格朗日[应变度量](@entry_id:755495)

[拉格朗日描述](@entry_id:264498)的特点是始终从参考构型的角度来观察和度量变形。为了构建一个这样的[应变度量](@entry_id:755495)，我们比较一个物质线元在变形前后的长度平方。在参考构型中，线元 $d\mathbf{X}$ 的长度平方为 $dS^2 = d\mathbf{X} \cdot d\mathbf{X}$。在当前构型中，其像 $d\mathbf{x} = \mathbf{F} d\mathbf{X}$ 的长度平方为：
$$
ds^2 = d\mathbf{x} \cdot d\mathbf{x} = (\mathbf{F} d\mathbf{X}) \cdot (\mathbf{F} d\mathbf{X}) = d\mathbf{X}^T \mathbf{F}^T \mathbf{F} d\mathbf{X}
$$
我们定义**右柯西-格林变形张量 (right Cauchy-Green deformation tensor)** $\mathbf{C} = \mathbf{F}^T \mathbf{F}$，于是 $ds^2 = d\mathbf{X}^T \mathbf{C} d\mathbf{X}$。$\mathbf{C}$ 完全描述了物[质点](@entry_id:186768)邻域的纯拉伸状态。

长度平方的改变量为 $ds^2 - dS^2 = d\mathbf{X}^T (\mathbf{C} - \mathbf{I}) d\mathbf{X}$，其中 $\mathbf{I}$ 是单位张量。为了得到一个在[刚体运动](@entry_id:193355)（此时 $ds^2 = dS^2$）时为零的[应变度量](@entry_id:755495)，我们定义**[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)** $\mathbf{E}$ [@problem_id:3568032]：
$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^T \mathbf{F} - \mathbf{I})
$$
$\mathbf{E}$ 是一个**物质张量 (material tensor)**，因为它完全由物质坐标及其梯度定义，与观察者的空间位置无关。至关重要的是，$\mathbf{E}$ 是**客观的 (objective)**，即在叠加任意刚体运动后其值不变。这可以通过极分解清晰地看出。将 $\mathbf{F}=\mathbf{R}\mathbf{U}$ 代入，我们发现 $\mathbf{C} = \mathbf{U}^T \mathbf{R}^T \mathbf{R} \mathbf{U} = \mathbf{U}^2$。因此：
$$
\mathbf{E} = \frac{1}{2}(\mathbf{U}^2 - \mathbf{I})
$$
这个表达式表明，$\mathbf{E}$ 只依赖于描述纯拉伸的张量 $\mathbf{U}$，而与刚体旋转 $\mathbf{R}$ 无关。这正是它成为有限变形理论中一个理想的[应变度量](@entry_id:755495)的原因 [@problem_id:3568009]。

#### 欧拉[应变度量](@entry_id:755495)

与[拉格朗日描述](@entry_id:264498)相对的是[欧拉描述](@entry_id:264722)，它从当前构型的角度进行度量。我们可以用类似的方法，但将长度变化表示为当前构型[线元](@entry_id:196833) $d\mathbf{x}$ 的函数。利用 $d\mathbf{X} = \mathbf{F}^{-1} d\mathbf{x}$，长度平方的变化量为：
$$
ds^2 - dS^2 = d\mathbf{x}^T (\mathbf{I} - \mathbf{F}^{-T} \mathbf{F}^{-1}) d\mathbf{x}
$$
我们定义**左柯西-格林变形张量 (left Cauchy-Green deformation tensor)** $\mathbf{B} = \mathbf{F} \mathbf{F}^T$，其逆为 $\mathbf{B}^{-1} = \mathbf{F}^{-T}\mathbf{F}^{-1}$。由此，我们定义**[欧拉-阿尔曼西应变张量](@entry_id:194948) (Euler-Almansi strain tensor)** $\mathbf{e}$ [@problem_id:3568001]：
$$
\mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{B}^{-1})
$$
$\mathbf{e}$ 是一个**[空间张量](@entry_id:185799) (spatial tensor)**，因为它与当前构型的几何相关。它在更新拉格朗日列式中扮演着重要角色。$\mathbf{E}$ 和 $\mathbf{e}$ 描述的是同一个物理变形，只是从不同的构型视角来看。它们之间可以通过变形梯度进行转换，例如，$\mathbf{e}$ 是 $\mathbf{E}$ 的“推前 (push-forward)”操作结果：$\mathbf{e} = \mathbf{F}^{-T} \mathbf{E} \mathbf{F}^{-1}$ [@problem_id:3568001]。

### 应力度量：从真实到名义

正如应变有多种度量方式，应力也一样。选择哪种应力度量取决于我们采用哪种运动学框架。

最符合物理直觉的是**柯西应力 (Cauchy stress)** $\boldsymbol{\sigma}$，也称为真实应力 [@problem_id:3568013]。它定义为作用在**当前构型**中单位面积上的力。根据柯西应力定理，作用在[法向量](@entry_id:264185)为 $\mathbf{n}$ 的[截面](@entry_id:154995)上的牵[引力](@entry_id:175476)（单位面积力）$\mathbf{t}$ 由下式给出：
$$
\mathbf{t} = \boldsymbol{\sigma} \mathbf{n}
$$
$\boldsymbol{\sigma}$ 是一个[空间张量](@entry_id:185799)，定义在当前构型 $B_t$ 上，因此它是更新拉格朗日列式的自然选择。

然而，在全拉格朗日列式中，所有计算都在固定的参考构型 $B_0$ 上进行。我们需要一种应力度量，它能将参考构型中的[面积元](@entry_id:263205)直接映射到作用在当前构型上的力。这就引出了**[第一皮奥拉-基尔霍夫应力](@entry_id:163971) (First Piola-Kirchhoff stress, PK1)** $\mathbf{P}$ [@problem_id:3568050]。它被定义为“名义应力”，即作用在当前构型上的力，但按**参考构型**的单位面积计算。名义牵[引力](@entry_id:175476) $\mathbf{T}_N$ 与 $\mathbf{P}$ 的关系为 $\mathbf{T}_N = \mathbf{P}\mathbf{N}$。

$\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 之间的关系可以通过力矢量的[不变性](@entry_id:140168)推导出来。作用在同一物质面元上的总力是唯一的，即 $\mathbf{t} da = \mathbf{T}_N dA$。结合[南森公式](@entry_id:195566)，我们可以得到它们之间的转换关系：
$$
\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-T}
$$
$\mathbf{P}$ 是一个“两点张量”，因为它将参考构型中的一个矢量 ($\mathbf{N}$) 映射到当前构型中的一个矢量 ($\mathbf{T}_N$)。一个重要的特点是，即使 $\boldsymbol{\sigma}$ 是对称的，$\mathbf{P}$ 通常也是**非对称**的。

为了与对称的[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$ 形成优美的对偶关系，我们引入了**[第二皮奥拉-基尔霍夫应力](@entry_id:173163) (Second Piola-Kirchhoff stress, PK2)** $\mathbf{S}$ [@problem_id:3568050]。$\mathbf{S}$ 与 $\mathbf{P}$ 的关系定义为：
$$
\mathbf{P} = \mathbf{F} \mathbf{S}
$$
通过这个定义，我们可以推导出 $\mathbf{S}$ 与柯西应力 $\boldsymbol{\sigma}$ 的关系：
$$
\mathbf{S} = \mathbf{F}^{-1} \mathbf{P} = \mathbf{F}^{-1} (J \boldsymbol{\sigma} \mathbf{F}^{-T}) = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T}
$$
$\mathbf{S}$ 是一个物质张量，它完全生活在参考构型中。如果 $\boldsymbol{\sigma}$ 是对称的，那么 $\mathbf{S}$ 也是对称的。更重要的是，$\mathbf{S}$ 是客观的，这使得它非常适合于在参考构型中构建不依赖于观察者[刚体运动](@entry_id:193355)的[本构关系](@entry_id:186508)。

### [虚功原理](@entry_id:138749)与运动学列式

虚功原理是连接[运动学](@entry_id:173318)（应变）和动力学（应力）的桥梁，也是[有限元列式](@entry_id:164720)的出发点。其基本形式通常在当前构型中给出，即[内力](@entry_id:167605)所做的[虚功](@entry_id:176403)等于外力所做的[虚功](@entry_id:176403)：
$$
\delta W_{\text{int}} = \int_{B_t} \boldsymbol{\sigma} : \delta\mathbf{d} \, dv = \delta W_{\text{ext}}
$$
其中 $\delta\mathbf{d}$ 是虚变形率张量（虚[位移梯度](@entry_id:165352)的对称部分）。不同的列式方法本质上就是对这个积分表达式采用不同的处理方式。

#### 全拉格朗日 (TL) 列式

TL 列式的核心思想是将所有积分和变量都“[拉回](@entry_id:160816) (pull-back)”到固定不变的参考构型 $B_0$ 上进行计算 [@problem_id:3567995]。通过前面建立的应变和应力度量之间的转换关系，我们可以对内力虚[功积分](@entry_id:181218)进行变换：
$$
\int_{B_t} \boldsymbol{\sigma} : \delta\mathbf{d} \, dv = \int_{B_0} J(\boldsymbol{\sigma} : \delta\mathbf{d}) \, dV = \int_{B_0} \mathbf{P} : \delta\mathbf{F} \, dV = \int_{B_0} \mathbf{S} : \delta\mathbf{E} \, dV
$$
这个变换过程完美地展示了不同应力-应变率（或其变分）对之间的**[功共轭](@entry_id:194957) (work-conjugate)** 关系。最终，TL 列式的[虚功](@entry_id:176403)方程写作：
$$
\int_{B_0} \mathbf{S} : \delta\mathbf{E} \, dV = \delta W_{\text{ext}}
$$
其中外力[虚功](@entry_id:176403)也必须相应地转换到参考构型上。TL 列式的优点在于积分域 $\Omega_0$ 是固定的，这简化了数值积分过程。它使用物质度量，如 $(\mathbf{S}, \mathbf{E})$，这些度量是客观的，便于建立复杂的本构模型 [@problem_id:3568004]。

#### 更新拉格朗日 (UL) 列式

UL 列式的核心思想则不同。它采用一种增量步进的方式，在每个增量步的开始，将当前已知的构型 $B_t$ 作为下一个增量步的“临时”参考构型 [@problem_id:3568000]。因此，其控制方程始终保持在[空间形式](@entry_id:186145)：
$$
\int_{B_t} \boldsymbol{\sigma} : \delta\mathbf{d} \, dv = \delta W_{\text{ext}}
$$
在 UL 列式中，我们直接使用柯西应力 $\boldsymbol{\sigma}$ 和空间变形率 $\mathbf{d}$。这种方法的优点在于它总是与物理上可直接观察和测量的量（真实应力和当[前几何](@entry_id:191573)）打交道。然而，它的代价是积分域 $B_t$ 在每个增量步都在变化，这给数值实现带来了挑战。

#### 能量一致性：统一原理

所有这些看似复杂的应力度量和变换关系，实际上都统一在一个深刻的物理原则之下：**功率不变性 (power invariance)** [@problem_id:3568021]。单位参考体积的[功率密度](@entry_id:194407) $p_V$ 必须是唯一的，无论我们用哪一套共轭的应力-[应变率](@entry_id:154778)对来计算。引入**[基尔霍夫应力](@entry_id:751039) (Kirchhoff stress)** $\boldsymbol{\tau} = J\boldsymbol{\sigma}$，我们可以得到一个优美的恒等式：
$$
p_V = \boldsymbol{\tau}:\mathbf{d} = \mathbf{P}:\dot{\mathbf{F}} = \mathbf{S}:\dot{\mathbf{E}}
$$
这个恒等式不仅是所有应力度量转换关系的最终检验标准，也为在数值程序中验证代码实现的正确性提供了强有力的工具。例如，一个编写正确的有限元程序，在给定一组运动学量 $(F, \dot{F})$ 和一个应力状态 (如 $\tau$) 后，计算出的四种[功率密度](@entry_id:194407) $J(\boldsymbol{\sigma}:\mathbf{d})$, $\boldsymbol{\tau}:\mathbf{d}$, $\mathbf{P}:\dot{\mathbf{F}}$ 和 $\mathbf{S}:\dot{\mathbf{E}}$ 应该在[数值精度](@entry_id:173145)范围内完全相等。

### 在[有限元法](@entry_id:749389)中的实现

将这些理论转化为可工作的计算程序，需要我们理解它们如何影响有限元离散后的方程。

#### TL列式中的[几何非线性](@entry_id:169896)

在 TL 列式中，虽然积分域是固定的，但[非线性](@entry_id:637147)却深深地嵌入在[运动学](@entry_id:173318)关系中。这种[非线性](@entry_id:637147)被称为**[几何非线性](@entry_id:169896) (geometric nonlinearity)** [@problem_id:3568010]。其根源在于[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$ 与[位移梯度](@entry_id:165352) $\nabla_0 \mathbf{u}$ 之间的非[线性关系](@entry_id:267880)：
$$
\mathbf{E} = \frac{1}{2}(\nabla_0 \mathbf{u} + (\nabla_0 \mathbf{u})^T + (\nabla_0 \mathbf{u})^T \nabla_0 \mathbf{u})
$$
即使对于最简单的线性材料（例如，$S$ 与 $E$ 成正比），由于应变 $E$ 本身是位移的二次函数，导致[内力](@entry_id:167605)矢量 $F_{\text{int}}$ 成为节点位移的高度[非线性](@entry_id:637147)函数。在组装有限元方程的残差向量时，必须在每个积分点计算完整的、[非线性](@entry_id:637147)的 $E$，然后通过[本构模型](@entry_id:174726)计算 $S$。同样，在推导[求解非线性方程](@entry_id:177343)组所需的[切线刚度矩阵](@entry_id:170852)时，也必须考虑这种复杂的[运动学](@entry_id:173318)关系，这使得[应变-位移矩阵](@entry_id:163451) ($B$ 矩阵) 本身也依赖于当前的位移状态。

#### UL列式中移动域的挑战

UL 列式的实现则面临着不同的挑战，即如何处理不断变化的积分域 [@problem_id:3568012]。在每个载荷步或迭代步中，由于构型 $\Omega_t$ 发生了改变，所有与几何相关的量都必须被重新计算。这包括：

1.  **单元雅可比矩阵 $\mathbf{J}_{\text{elem}}$**: 连接父单元坐标与当前空间坐标的映射，它依赖于当前节点的坐标。
2.  **形函数空间梯度 $\nabla_x N_I$**: 这是计算应变的基础，它通过 $\mathbf{J}_{\text{elem}}^{-1}$ 与单元几何直接相关。
3.  **边界法向量 $\mathbf{n}$**: 对于施加[表面力](@entry_id:188034)或处理接触问题至关重要，它随着边界的变形而改变。

这种不断的更新意味着在每个迭代步中，计算成本相对较高。此外，UL 列式的[切线刚度矩阵](@entry_id:170852)也包含两个部分：反映材料本构响应的**材料刚度 (material stiffness)** 和反映应力状态对几何变化影响的**[几何刚度](@entry_id:172820) (geometric stiffness)**（或称初应力刚度）。后者直接依赖于当前的柯西应力 $\boldsymbol{\sigma}$，这再次凸显了 UL 列式中几何与应力状态的紧密耦合。

总之，TL 和 UL 列式为求解大变形问题提供了两条不同的路径。TL 将所有的复杂性封装在[非线性](@entry_id:637147)的[应变度量](@entry_id:755495)中，但受益于固定的积分域。UL 则保持了[运动学](@entry_id:173318)和应力度量的简洁性，但代价是必须在不断更新的、移动的积分域上进行计算。在实践中，选择哪种方法取决于问题的具体特点、所用[本构模型](@entry_id:174726)的形式以及对[计算效率](@entry_id:270255)的考量。