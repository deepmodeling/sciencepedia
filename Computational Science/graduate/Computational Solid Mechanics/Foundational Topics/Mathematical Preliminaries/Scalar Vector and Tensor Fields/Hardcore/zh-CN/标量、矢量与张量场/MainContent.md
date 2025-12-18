## 引言
标量、向量与[张量场](@entry_id:190170)是描述物理世界，特别是连续介质力学现象不可或缺的数学语言。从材料内部的温度[分布](@entry_id:182848)到复杂的应力状态，这些场将物理量与空间中的每一点精确地联系起来，为[分析物](@entry_id:199209)体的运动、变形与受力提供了统一的框架。然而，从掌握这些场的基本定义到能够自如地将其应用于解决高级力学问题，特别是涉及[大变形](@entry_id:167243)和[计算模拟](@entry_id:146373)的场景，存在着一条需要系统性学习的路径。

本文旨在为读者铺设这条路径，引领读者全面掌握场论在现代[计算固体力学](@entry_id:169583)中的核心地位。文章分为三个主要部分。在第一章“原理与机制”中，我们将建立坚实的数学基础，系统阐述场的基本代数与微积分运算，探索它们在变形[运动学](@entry_id:173318)中的关键作用，并讨论客观性等基本物理原理。随后的“应用与跨学科联系”一章将展示这些抽象概念的强大威力，通过实例探讨它们在高等力学公式、先进材料本构以及与其他科学领域的交叉应用。最后，通过“动手实践”部分，读者将有机会将所学理论应用于具体问题，加深理解。现在，让我们从最基本的原理与机制开始，正式进入[张量场](@entry_id:190170)的世界。

## 原理与机制

在深入探讨[连续介质力学](@entry_id:155125)的计算方法之前，我们必须首先掌握描述其物理现象的数学语言：[标量场](@entry_id:151443)、向量场和[张量场](@entry_id:190170)。这些场将物理量（如温度、位移、应力）与空间中的每一点联系起来，为我们提供了描述和分析变形体行为的框架。本章将系统地阐述这些场的基本代数和微积分运算、它们在变形运动学中的作用、如何构建客观的物理度量，以及它们在现代[本构模型](@entry_id:174726)和计算方法中的应用。

### 场的基本运算：代数与微积分

连续介质力学的核心在于场量之间的相互作用。这些相互作用可以通过明确的代数和微积分运算来描述。

#### 场的代数构造

从已知的向量场出发，我们可以通过代数运算构造出新的、具有不同物理意义和数学阶次的场。考虑定义在三维[欧几里得空间](@entry_id:138052) $\Omega \subset \mathbb{R}^3$ 上的两个光滑向量场 $\boldsymbol{a}(\boldsymbol{x})$ 和 $\boldsymbol{b}(\boldsymbol{x})$。为具体起见，假设这两个场都代表位移，因此其物理单位为长度 $L$。我们可以通过三种基本的双线性运算生成新的场：

1.  **[内积](@entry_id:158127)（[点积](@entry_id:149019)）**：两个向量场的[内积](@entry_id:158127)产生一个 **[标量场](@entry_id:151443)**（零阶[张量场](@entry_id:190170)）。
    $s(\boldsymbol{x}) = \boldsymbol{a}(\boldsymbol{x}) \cdot \boldsymbol{b}(\boldsymbol{x})$
    在[标准正交基](@entry_id:147779) $\{ \boldsymbol{e}_i \}$ 中，其分量形式为 $s = a_i b_i$（此处及后文均采用爱因斯坦求和约定）。由于每个分量 $a_i$ 和 $b_i$ 的单位都是 $L$，所以标量场 $s(\boldsymbol{x})$ 的单位是 $L^2$。例如，如果 $\boldsymbol{a}$ 和 $\boldsymbol{b}$ 分别代表力和位移，它们的[点积](@entry_id:149019)就代表了功，一个标量。

2.  **外积（叉积）**：在三维空间中，两个向量场的[外积](@entry_id:147029)产生一个 **向量场**（一阶[张量场](@entry_id:190170)），准确地说是轴矢量或伪矢量。
    $\boldsymbol{v}(\boldsymbol{x}) = \boldsymbol{a}(\boldsymbol{x}) \times \boldsymbol{b}(\boldsymbol{x})$
    其第 $i$ 个分量由[列维-奇维塔符号](@entry_id:193594) $\varepsilon_{ijk}$ 定义：$v_i = \varepsilon_{ijk} a_j b_k$。由于 $\varepsilon_{ijk}$ 是无量纲的，外积得到的向量场 $\boldsymbol{v}(\boldsymbol{x})$ 的每个分量的单位都是 $L \times L = L^2$。例如，在[流体力学](@entry_id:136788)中，位置向量和流体速度向量的[叉积](@entry_id:156672)与角[动量密度](@entry_id:271360)有关。

3.  **[并矢积](@entry_id:748716)（张量积）**：两个向量场的[并矢积](@entry_id:748716)产生一个 **二阶张量场**。
    $\boldsymbol{T}(\boldsymbol{x}) = \boldsymbol{a}(\boldsymbol{x}) \otimes \boldsymbol{b}(\boldsymbol{x})$
    其分量形式为 $T_{ij} = a_i b_j$。此运算的单位也是 $L^2$。重要的是，[并矢积](@entry_id:748716)是不可交换的，即 $\boldsymbol{a} \otimes \boldsymbol{b} \neq \boldsymbol{b} \otimes \boldsymbol{a}$（除非 $\boldsymbol{a}$ 和 $\boldsymbol{b}$ 共线）。因此，从[有序对](@entry_id:269702) $(\boldsymbol{a}, \boldsymbol{b})$ 出发，我们可以得到两个不同的[二阶张量](@entry_id:199780)场，$\boldsymbol{a} \otimes \boldsymbol{b}$ 和 $\boldsymbol{b} \otimes \boldsymbol{a}$。在[连续介质力学](@entry_id:155125)中，[位移梯度张量](@entry_id:748571)就可以看作是[梯度算子](@entry_id:275922)与位移向量场的组合结果，这是一种更复杂的张量积形式。

这些基本运算构成了[张量代数](@entry_id:161671)的基础，使我们能够从基本物理量构建更复杂的模型。

#### 场的[微分](@entry_id:158718)运算

除了代数运算，描述场在空间中如何变化的[微分算子](@entry_id:140145)也至关重要。最核心的三个算子是梯度、[散度和旋度](@entry_id:270881)。

-   **向量场的梯度 (Gradient)**：一个向量场 $\boldsymbol{v}$ 的梯度 $\nabla\boldsymbol{v}$ 是一个二阶张量，它描述了向量场在空间中各方向的变化率。其分量定义为：
    $(\nabla \boldsymbol{v})_{ij} = \frac{\partial v_i}{\partial x_j} = \partial_j v_i$
    从几何上看，$\nabla\boldsymbol{v}$ 是一个[线性映射](@entry_id:185132)，它将一个无穷小的位移向量 $d\boldsymbol{x}$ 映射到向量场 $\boldsymbol{v}$ 的相应变化 $d\boldsymbol{v}$，即 $d v_i \approx (\nabla \boldsymbol{v})_{ij} dx_j$。这个张量就是 $\boldsymbol{v}$ 的 **[雅可比矩阵](@entry_id:264467)**。

-   **[二阶张量](@entry_id:199780)场的散度 (Divergence)**：一个二阶张量场 $\boldsymbol{T}$ 的散度 $\nabla \cdot \boldsymbol{T}$ 是一个向量场。其第 $i$ 个分量等于张量 $\boldsymbol{T}$ 的第 $i$ 个行向量的散度。其分量形式为：
    $(\nabla \cdot \boldsymbol{T})_i = \partial_j T_{ij}$
    这个定义的物理意义源于[高斯散度定理](@entry_id:188065)。$(\nabla \cdot \boldsymbol{T})_i$ 表示围绕一个点单位体积内，第 $i$ 个行向量场的净流出通量密度。在[固体力学](@entry_id:164042)中，柯西应力张量 $\boldsymbol{\sigma}$ 的散度 $\nabla \cdot \boldsymbol{\sigma}$ 代表了单位体积上的净[表面力](@entry_id:188034)，直接出现在[动量平衡](@entry_id:193575)方程中。

-   **向量场的旋度 (Curl)**：一个向量场 $\boldsymbol{v}$ 的旋度 $\nabla \times \boldsymbol{v}$ 是另一个向量场，它描述了场在无穷小尺度上的旋转趋势。其分量形式为：
    $(\nabla \times \boldsymbol{v})_i = \varepsilon_{ijk} \partial_j v_k$
    根据[斯托克斯定理](@entry_id:264534)，旋度向量的方向是局部旋转轴的方向（由右手定则确定），其大小则代表了单位面积的环量或“旋转密度”。例如，在小应变理论中，位移场旋度的一半代表了物[质点](@entry_id:186768)的[刚体转动](@entry_id:191086)。

#### 张量的本质：[坐标无关性](@entry_id:159715)

深刻理解张量的关键在于认识到它是一个**几何对象**，其物理意义独立于任何特定的[坐标系](@entry_id:156346)。我们用一组分量来表示张量，但这组分量会随着[坐标系](@entry_id:156346)的改变而改变。一个“真正的”[张量场](@entry_id:190170)，其在不同[坐标系](@entry_id:156346)下的分量必须遵循特定的变换法则。

考虑一个被动[坐标变换](@entry_id:172727) $\tilde{\boldsymbol{x}}=\boldsymbol{Q}\boldsymbol{x}+\boldsymbol{c}$，其中 $\boldsymbol{Q} \in \mathrm{SO}(3)$ 是一个正交[旋转矩阵](@entry_id:140302)。一个真正的[二阶张量](@entry_id:199780)场 $\boldsymbol{T}$ 的分量变换规律是：
$\tilde{T}_{ij}(\tilde{\boldsymbol{x}}) = Q_{ip} Q_{jq} T_{pq}(\boldsymbol{x})$

任何一组不遵循此变换法则的 $3 \times 3$ 数组都不能被称为张量。一个典型的反例是向量场分量的普通偏导数。在笛卡尔坐标系下，梯度 $(\nabla\boldsymbol{v})_{ij} = \partial_j v_i$ 确实是一个张量。然而，在[曲线坐标系](@entry_id:172561)（如[柱坐标](@entry_id:271645)或球坐标）中，由于[基向量](@entry_id:199546)本身随位置变化，普通[偏导数](@entry_id:146280)构成的数组 $\partial v_i / \partial q^j$ 不再是张量。要得到一个真正的张量，必须使用**协变导数**，它包含了修正项（克里斯托费尔符号）来计及[基向量](@entry_id:199546)的变化。

例如，考虑二维空间中一个均匀的水平[速度场](@entry_id:271461) $\boldsymbol{v} = v_0 \boldsymbol{e}_x$。在[笛卡尔坐标系](@entry_id:169789)中，其分量为 $(v_x, v_y) = (v_0, 0)$，梯度矩阵的所有分量 $\partial v_i / \partial x_j$ 均为零。然而，在极[坐标系](@entry_id:156346) $(r, \theta)$ 中，该向量场的分量为 $(v_r, v_\theta) = (v_0 \cos\theta, -v_0 \sin\theta)$。如果我们天真地计算这些分量的[偏导数](@entry_id:146280)，会得到如 $\partial v_r / \partial \theta = -v_0 \sin\theta$ 等非零项。由于同一个物理场（均匀速度场）在一个[坐标系](@entry_id:156346)下的“梯度”为零，而在另一个[坐标系](@entry_id:156346)下非零，这说明由普通[偏导数](@entry_id:146280)构成的数组并不是一个张量。正确的张量——[协变导数](@entry_id:152476)——对于这个均匀场在任何[坐标系](@entry_id:156346)下都将为零。

### 变形运动学：场的映射

连续介质力学的核心是描述物质如何从一个**参考构型**（初始状态） $\Omega_0$ 运动到一个**当前构型**（变形后状态） $\Omega$。这一过程由 **变形映射** $\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t)$ 描述，它将参考构型中的每个物[质点](@entry_id:186768) $\boldsymbol{X}$ 映射到其在时刻 $t$ 的空间位置 $\boldsymbol{x}$。

#### 变形梯度

描述局部变形的关键物理量是 **变形梯度张量** $\boldsymbol{F}$，它被定义为变形映射 $\boldsymbol{\varphi}$ 对参考坐标 $\boldsymbol{X}$ 的梯度：
$\boldsymbol{F} = \frac{\partial \boldsymbol{\varphi}}{\partial \boldsymbol{X}} = \nabla_{\boldsymbol{X}} \boldsymbol{\varphi}$
$\boldsymbol{F}$ 是一个二阶张量，它将参考构型中的一个无穷小物质[线元](@entry_id:196833) $d\boldsymbol{X}$ 线性地映射到当前构型中对应的[线元](@entry_id:196833) $d\boldsymbol{x}$：
$d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$
因此，$\boldsymbol{F}$ 包含了关于局部拉伸和旋转的全部信息。

#### 面积和[体积元](@entry_id:267802)素的映射

变形梯度张量 $\boldsymbol{F}$ 的两个重要导出量决定了面积和体积元素如何变换：

-   **雅可比行列式 (Jacobian)**：$J = \det \boldsymbol{F}$。它描述了局部体积的变化率。一个参考构型中的体积元 $dV$ 在变形后变为 $dv = J dV$。对于物理上可能的变形，物质不能相互穿透，且局部朝向必须保持，因此要求 $J > 0$。根据[质量守恒定律](@entry_id:147377)（$dm = \rho_0 dV = \rho dv$），[雅可比行列式](@entry_id:137120)还将参考密度 $\rho_0$ 和当前密度 $\rho$ 联系起来：$\rho_0(\boldsymbol{X}) = J(\boldsymbol{X}) \rho(\boldsymbol{x})$。

-   **[余子式](@entry_id:137503)张量 (Cofactor)**：$\operatorname{cof} \boldsymbol{F} = J \boldsymbol{F}^{-T}$。这个张量用于映射[有向面积](@entry_id:169588)元。一个在参考构型中由法向 $\boldsymbol{N}$ 和面积 $dA$ 定义的[有向面积](@entry_id:169588)元 $d\boldsymbol{A} = \boldsymbol{N} dA$，在当前构型中变为 $d\boldsymbol{a} = \boldsymbol{n} da$。它们之间的关系由著名的 **[南森公式](@entry_id:195566) (Nanson's formula)** 给出：
    $\boldsymbol{n} da = (\operatorname{cof} \boldsymbol{F}) \boldsymbol{N} dA = J \boldsymbol{F}^{-T} \boldsymbol{N} dA$
    这个关系在推导不同构型下的[力平衡](@entry_id:267186)和通量守恒时至关重要。

#### 推前与[拉回运算](@entry_id:753859)

为了在参考构型（[拉格朗日描述](@entry_id:264498)）和当前构型（[欧拉描述](@entry_id:264722)）之间系统地转换物理量，我们定义了**推前 (push-forward)** 和 **[拉回](@entry_id:160816) (pull-back)** 运算。

-   **向量场**：
    -   推前：将一个定义在参考构型上的向量场 $\boldsymbol{V}_0(\boldsymbol{X})$ 转换为当前构型上的空间向量场 $\boldsymbol{v}(\boldsymbol{x})$，其变换法则正是变形梯度所定义的：$\boldsymbol{v} = \boldsymbol{F} \boldsymbol{V}_0$。
    -   [拉回](@entry_id:160816)：逆运算为 $\boldsymbol{V}_0 = \boldsymbol{F}^{-1} \boldsymbol{v}$。

-   **[二阶张量](@entry_id:199780)场**：
    考虑一个在参考构型中作为线性映射的张量 $\boldsymbol{A}_0$。其推前后的张量 $\boldsymbol{a}$ 必须保持映射关系。这意味着如果 $\boldsymbol{W}_0 = \boldsymbol{A}_0 \boldsymbol{U}_0$，那么它们的推前向量 $\boldsymbol{w} = \boldsymbol{F}\boldsymbol{W}_0$ 和 $\boldsymbol{u} = \boldsymbol{F}\boldsymbol{U}_0$ 必须满足 $\boldsymbol{w} = \boldsymbol{a}\boldsymbol{u}$。由此可以推导出变换法则：
    -   推前：$\boldsymbol{a} = \boldsymbol{F} \boldsymbol{A}_0 \boldsymbol{F}^{-1}$
    -   [拉回](@entry_id:160816)：$\boldsymbol{A}_0 = \boldsymbol{F}^{-1} \boldsymbol{a} \boldsymbol{F}$
    这些变换法则保证了张量作为几何对象的内在属性在不同构型描述下得以保持。

### 应变与变形率的度量

从变形梯度 $\boldsymbol{F}$ 出发，我们可以定义一系列张量场来客观地量化变形的程度和速率。

#### 有限应变张量

为了消除变形中的[刚体转动](@entry_id:191086)效应，我们构造如下的[应变度量](@entry_id:755495)：

-   **右柯西-格林变形张量 (Right Cauchy-Green Tensor)**：$\boldsymbol{C} = \boldsymbol{F}^T \boldsymbol{F}$。它定义在参考构型上，度量了物质线元长度的平方变化。
-   **[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange Strain Tensor)**：$\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I})$。它也定义在参考构型上，度量了相对于初始状态的应变。当 $\boldsymbol{F}=\boldsymbol{I}$（无变形）时，$\boldsymbol{E}=0$。
-   **左柯西-格林变形张量 (Left Cauchy-Green Tensor)**：$\boldsymbol{B} = \boldsymbol{F} \boldsymbol{F}^T$。它定义在当前构型上，与空间变形状态相关。
-   **[欧拉-阿尔曼西应变张量](@entry_id:194948) (Euler-Almansi Strain Tensor)**：$\boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{B}^{-1})$。它定义在当前构型上，度量了相对于最终状态的应变。

#### 变形率与自旋

在[欧拉描述](@entry_id:264722)下，我们关注物[质点](@entry_id:186768)速度场的空间变化，这由**[速度梯度张量](@entry_id:270928)** $\boldsymbol{L} = \nabla\boldsymbol{v}$ 描述，其分量为 $L_{ij} = \partial v_i / \partial x_j$。[速度梯度](@entry_id:261686)可以分解为对称和反对称两部分：

-   **变形率张量 (Rate-of-Deformation Tensor)**：$\boldsymbol{D} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^T)$。它是 $\boldsymbol{L}$ 的对称部分，描述了物质线元长度和夹角的变化率，即变形的速率。
-   **[自旋张量](@entry_id:187346) (Spin Tensor)**：$\boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^T)$。它是 $\boldsymbol{L}$ 的反对称部分，描述了物质的瞬时[刚体转动](@entry_id:191086)[角速度](@entry_id:192539)。

#### [客观性原理](@entry_id:185412)

一个基本的物理要求是，本构关系（材料定律）不能依赖于观察者。这一**[客观性原理](@entry_id:185412) (Principle of Objectivity)** 或称**物质标架无关性 (Material Frame-Indifference)**，要求在叠加一个任意的[刚体运动](@entry_id:193355) $x^* = \boldsymbol{c}(t) + \boldsymbol{Q}(t)\boldsymbol{x}$（其中 $\boldsymbol{Q}(t)$ 是[旋转张量](@entry_id:191990)）后，[本构方程](@entry_id:138559)的形式保持不变。

我们可以检验上述[应变度量](@entry_id:755495)的客观性。在观察者变换下，变形梯度变为 $\boldsymbol{F}^* = \boldsymbol{Q}\boldsymbol{F}$。
-   对于[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}$：
    $\boldsymbol{C}^* = (\boldsymbol{F}^*)^T \boldsymbol{F}^* = (\boldsymbol{Q}\boldsymbol{F})^T (\boldsymbol{Q}\boldsymbol{F}) = \boldsymbol{F}^T \boldsymbol{Q}^T \boldsymbol{Q} \boldsymbol{F} = \boldsymbol{F}^T \boldsymbol{I} \boldsymbol{F} = \boldsymbol{C}$
    由于 $\boldsymbol{C}^* = \boldsymbol{C}$，$\boldsymbol{C}$ 是客观的（对于参考构型上的张量，客观性表现为不变性）。同理，$\boldsymbol{E}$ 也是客观的。
-   对于[左柯西-格林张量](@entry_id:186163) $\boldsymbol{B}$：
    $\boldsymbol{B}^* = \boldsymbol{F}^* (\boldsymbol{F}^*)^T = (\boldsymbol{Q}\boldsymbol{F}) (\boldsymbol{Q}\boldsymbol{F})^T = \boldsymbol{Q} \boldsymbol{F} \boldsymbol{F}^T \boldsymbol{Q}^T = \boldsymbol{Q} \boldsymbol{B} \boldsymbol{Q}^T$
    $\boldsymbol{B}$ 的变换规律符合欧拉型（空间）张量的客观性要求，因此 $\boldsymbol{B}$ 是客观的。同理，$\boldsymbol{e}$ 也是客观的。

然而，并非所有物理上重要的量的时间导数都是客观的。一个突出的例子是柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的**[物质时间导数](@entry_id:190892)** $\dot{\boldsymbol{\sigma}}$。[物质时间导数](@entry_id:190892)是跟随物[质点](@entry_id:186768)运动所观察到的变化率，其定义为 $\dot{\boldsymbol{\sigma}} = \frac{\partial \boldsymbol{\sigma}}{\partial t} + \boldsymbol{v} \cdot \nabla \boldsymbol{\sigma}$。柯西应力本身是客观的，即 $\boldsymbol{\sigma}^* = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T$。但对其物质时间求导会得到：
$\dot{\boldsymbol{\sigma}}^* = \frac{d}{dt}(\boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T) = \dot{\boldsymbol{Q}}\boldsymbol{\sigma}\boldsymbol{Q}^T + \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^T + \boldsymbol{Q}\boldsymbol{\sigma}\dot{\boldsymbol{Q}}^T$
这个结果并不等于 $ \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^T $（除非 $\dot{\boldsymbol{Q}}=0$）。因此，$\dot{\boldsymbol{\sigma}}$ 不是一个客观张量。这促使了多种**[客观应力率](@entry_id:199282)**的定义（如Jaumann率、[Truesdell率](@entry_id:181014)），它们通过引入与[自旋张量](@entry_id:187346)相关的修正项来消除非客观性，从而能够在率形式的[本构方程](@entry_id:138559)中正确使用。

### [本构模型](@entry_id:174726)：场的相互关系

本构模型或材料定律是描述特定材料[应力与应变](@entry_id:137374)之间关系的数学方程。这些关系本质上是[张量场](@entry_id:190170)之间的函数关系。

#### [弹性张量](@entry_id:170728)与对称性

对于[线性弹性](@entry_id:166983)材料，应力张量 $\boldsymbol{\sigma}$ 和[小应变张量](@entry_id:754968) $\boldsymbol{\varepsilon}$ 之间存在[线性关系](@entry_id:267880)，由四阶**[弹性张量](@entry_id:170728)** $\mathbb{C}$ 描述：
$\sigma_{ij} = C_{ijkl} \varepsilon_{kl}$

[弹性张量](@entry_id:170728) $C_{ijkl}$ 具有重要的对称性，这些对称性源于基本的物理原理：
-   **次对称性 (Minor Symmetries)**：
    1.  $C_{ijkl} = C_{ijlk}$：源于应变[张量的对称性](@entry_id:202126) $\varepsilon_{kl} = \varepsilon_{lk}$。
    2.  $C_{ijkl} = C_{jikl}$：源于（在无体力矩时）由[角动量守恒](@entry_id:156798)保证的应力[张量的对称性](@entry_id:202126) $\sigma_{ij} = \sigma_{ji}$。
    在考虑了这些次对称性后，一个[四阶张量](@entry_id:181350)的独立分量数从 $3^4 = 81$ 个减少到 $36$ 个。如果在广义连续体理论（如[Cosserat理论](@entry_id:186875)）中应力张量不对称，则第二条次对称性可能不成立。

-   **主对称性 (Major Symmetry)**：
    $C_{ijkl} = C_{klij}$：这个对称性源于一个更强的假设——材料是**超弹性的 (hyperelastic)**。这意味着存在一个标量**[应变能密度函数](@entry_id:755490)** $\psi(\boldsymbol{\varepsilon})$，使得应力可以通过对应变求导得到：$\boldsymbol{\sigma} = \partial\psi / \partial\boldsymbol{\varepsilon}$。对于线性材料，$\psi = \frac{1}{2} C_{ijkl} \varepsilon_{ij} \varepsilon_{kl}$。主对称性是二阶[混合偏导数次序无关性](@entry_id:146941) ($\partial^2\psi / \partial\varepsilon_{ij}\partial\varepsilon_{kl} = \partial^2\psi / \partial\varepsilon_{kl}\partial\varepsilon_{ij}$) 的直接结果。这一性质也与[Maxwell-Betti互易定理](@entry_id:186682)等价，它将[独立弹性常数](@entry_id:203649)的数量从 $36$ 个进一步减少到 $21$ 个。

#### 各向同性[超弹性](@entry_id:159356)

对于有限变形的[超弹性材料](@entry_id:190241)，[应变能](@entry_id:162699) $\psi$ 是变形梯度 $\boldsymbol{F}$ 的函数。[客观性原理](@entry_id:185412)要求 $\psi$ 仅依赖于拉伸部分，即 $\psi(\boldsymbol{F}) = \hat{\psi}(\boldsymbol{C})$。如果材料还是**各向同性的 (isotropic)**，意味着其力学性质与方向无关，那么 $\psi$ 必须是一个关于其张量参数的[各向同性函数](@entry_id:750877)。根据张量函数[表示定理](@entry_id:637872)，任何一个对称二阶张量（如 $\boldsymbol{C}$ 或 $\boldsymbol{B}$）的各向同性标量函数，都可以表示为其三个**[主不变量](@entry_id:193522)**的函数：
$I_1(\boldsymbol{C}) = \operatorname{tr}(\boldsymbol{C})$
$I_2(\boldsymbol{C}) = \frac{1}{2}[(\operatorname{tr}\boldsymbol{C})^2 - \operatorname{tr}(\boldsymbol{C}^2)]$
$I_3(\boldsymbol{C}) = \det(\boldsymbol{C})$
因此，各向同性[超弹性材料](@entry_id:190241)的[应变能密度函数](@entry_id:755490)可以写成：
$\psi = \phi(I_1(\boldsymbol{C}), I_2(\boldsymbol{C}), I_3(\boldsymbol{C}))$
由于 $\boldsymbol{B}$ 和 $\boldsymbol{C}$ 具有相同的[不变量](@entry_id:148850)，$\psi$ 也可以等价地表示为 $\boldsymbol{B}$ 的[不变量](@entry_id:148850)的函数。此外，由于[不变量](@entry_id:148850)是[特征值](@entry_id:154894)的[对称多项式](@entry_id:153581)，$\psi$ 也可以表示为三个[主伸长](@entry_id:194664)率 $\lambda_1, \lambda_2, \lambda_3$（即右[拉伸张量](@entry_id:193200) $\boldsymbol{U}=\sqrt{\boldsymbol{C}}$ 的[特征值](@entry_id:154894)）的[对称函数](@entry_id:177113) $g(\lambda_1, \lambda_2, \lambda_3)$。对于[不可压缩材料](@entry_id:159741) ($J=\sqrt{I_3}=1$)，应变能仅依赖于前两个（修正的）[不变量](@entry_id:148850)。

#### [皮奥拉变换](@entry_id:163790)与应[力场](@entry_id:147325)

在不同构型中，力的度量方式不同。当前构型中的柯西应力 $\boldsymbol{\sigma}$ 度量了单位当前面积上的力。为了在参考构型上进行计算，我们引入了**[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量 (First Piola-Kirchhoff Stress Tensor)** $\boldsymbol{P}$。它通过保持总力元不变 ($d\boldsymbol{f} = \boldsymbol{t}da = \boldsymbol{T}_0 dA$) 而定义，其中 $\boldsymbol{t}=\boldsymbol{\sigma}\boldsymbol{n}$ 是柯西牵[引力](@entry_id:175476)，$\boldsymbol{T}_0=\boldsymbol{P}\boldsymbol{N}$ 是名义牵[引力](@entry_id:175476)。利用[南森公式](@entry_id:195566)，可以导出 $\boldsymbol{\sigma}$ 和 $\boldsymbol{P}$ 之间的关系：
$\boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-T}$
这种将欧拉场（如 $\boldsymbol{\sigma}$）变换为拉格朗日场（如 $\boldsymbol{P}$）的操作称为**[皮奥拉变换](@entry_id:163790)**。类似地，一个在当前构型中定义的通量向量 $\boldsymbol{j}$（单位当前面积的通量）可以通过[皮奥拉变换](@entry_id:163790)得到其在参考构型中的对应量 $\boldsymbol{J}_0$（单位参考面积的通量），以保证总通量守恒：
$\boldsymbol{J}_0 = J \boldsymbol{F}^{-1} \boldsymbol{j}$
这些变换是连接不同力学描述的桥梁。

### [计算力学](@entry_id:174464)中的场：离散化与[函数空间](@entry_id:143478)

将[连续介质力学](@entry_id:155125)理论转化为可计算的算法（如有限元法 FEM）时，场的概念面临着新的挑战和要求。

#### [等参映射](@entry_id:173239)与单元有效性

在有限元法中，复杂的物理域被划分为简单的单元（如四边形或六面体）。每个物理单元通过一个**[等参映射](@entry_id:173239)**从一个标准的**参考单元**（如 $[-1, 1]^2$）变换而来。这个映射由单元节点的坐标和形函数定义。
$\boldsymbol{x}(\xi, \eta) = \sum_{i} N_i(\xi, \eta) \boldsymbol{x}_i$
该映射的[雅可比矩阵](@entry_id:264467) $\boldsymbol{J}$ 及其[行列式](@entry_id:142978) $\det \boldsymbol{J}$ 至关重要。根据积分[变量替换定理](@entry_id:160749)，$d\Omega = \det \boldsymbol{J} d\hat{\Omega}$。为了保证映射是物理上可接受的（一对一且保持定向），必须在整个单元内满足 $\det \boldsymbol{J} > 0$。
-   如果 $\det \boldsymbol{J} = 0$，映射是奇异的，物理单元的面积（或体积）在某点被压缩为零。
-   如果 $\det \boldsymbol{J}  0$，映射发生了**反转 (inversion)**，参考单元的局部朝向被翻转。这在物理上对应于物质的自我穿透，在数学上会导致梯度计算和积分的符号错误，从而使计算结果毫无意义。

一个简单的例子可以说明单元反转。对于一个[双线性](@entry_id:146819)[四边形单元](@entry_id:176937)，如果节点[排列](@entry_id:136432)不当，例如形成一个凹四边形甚至自相交的“蝴蝶结”形，就可能导致 $\det \boldsymbol{J}$ 在单元内部变为负值。例如，若四节点坐标为 $(0,0), (2,0), (0.2, -0.5), (-0.2, 1.2)$，可以计算出在[参考单元](@entry_id:168425)中心 $(\xi, \eta)=(0,0)$ 处 $\det \boldsymbol{J}  0$，表明单元发生了反转。因此，在[有限元网格](@entry_id:174862)生成和[大变形分析](@entry_id:163435)中，检查并保证所有单元的 $\det \boldsymbol{J}  0$ 是保证计算有效性的基本前提。

#### 变分公式的函数空间

有限元法的基础是求解控制方程的**[弱形式](@entry_id:142897)**或**[变分形式](@entry_id:166033)**。为了严谨地建立这些公式，我们需要将未知场（如位移、应力）置于合适的**[函数空间](@entry_id:143478)**中。这些空间，即索伯列夫空间 (Sobolev spaces)，对函数本身及其（弱）导数的[可积性](@entry_id:142415)提出了要求。

-   **$L^2(\Omega)$**：[平方可积函数](@entry_id:200316)的空间。对于向量或[张量场](@entry_id:190170)，要求其每个分量都是平方可积的。其范数由积分 $\int_\Omega |\boldsymbol{u}|^2 d\Omega$ 定义。$L^2$ 空间中的函数不一定连续，也**不具有**良定义的边界值（迹）。

-   **$H^1(\Omega)$**：函数本身及其一阶[弱导数](@entry_id:189356)都属于 $L^2$ 的空间。其范数包含函数本身和其梯度的 $L^2$ 范数。根据[迹定理](@entry_id:203967)，对于足够光滑的边界，定义在 $H^1(\Omega)$ 上的函数**具有**良定义的边界值，属于 $H^{1/2}(\partial\Omega)$ 空间。在位移法有限元中，[位移场](@entry_id:141476)通常要求属于 $H^1$ 空间，以确保应变能（依赖于[位移梯度](@entry_id:165352)）是有限的。

-   **$H(\operatorname{div}, \Omega)$**：函数本身及其散度都属于 $L^2$ 的空间。对于张量场 $\boldsymbol{\tau}$，要求 $\boldsymbol{\tau} \in L^2$ 且 $\nabla \cdot \boldsymbol{\tau} \in L^2$。根据一个广义的[迹定理](@entry_id:203967)，属于 $H(\operatorname{div}, \Omega)$ 的[张量场](@entry_id:190170)**具有**良定义的法向分量（或法向通量）迹 $\boldsymbol{\tau}\boldsymbol{n}$，它属于 $H^{-1/2}(\partial\Omega)$ 空间。

这些[函数空间](@entry_id:143478)的选择对于[变分问题](@entry_id:756445)的[适定性](@entry_id:148590)（解的存在性、唯一性和稳定性）至关重要。例如，在Hellinger-Reissner等**[混合变分原理](@entry_id:165106)**中，位移和应力被当作独立的未知场。为了使弱形式中的各项积分有意义，需要为它们选择合适的[函数空间](@entry_id:143478)。典型的选择是：
-   **应[力场](@entry_id:147325)** $\boldsymbol{\sigma} \in H(\operatorname{div}, \Omega; \mathbb{S})$
-   **位移场** $\boldsymbol{u} \in L^2(\Omega; \mathbb{R}^d)$

这种选择的合理性在于，[动量平衡](@entry_id:193575)方程的弱形式包含 $\int_\Omega (\nabla\cdot\boldsymbol{\sigma})\cdot\boldsymbol{v} \, d\Omega$ 项，这就要求应[力场](@entry_id:147325)的散度是平方可积的。而[应力-应变关系](@entry_id:274093)的弱形式包含 $\int_\Omega (\nabla\cdot\boldsymbol{\tau})\cdot\boldsymbol{u} \, d\Omega$ 项，将[位移场](@entry_id:141476) $\boldsymbol{u}$ 置于 $L^2$ 空间是满足此项要求的最低[正则性条件](@entry_id:166962)。这种方法放宽了对位移场连续性的要求，在某些问题（如处理[不可压缩材料](@entry_id:159741)）中具有独特的优势。