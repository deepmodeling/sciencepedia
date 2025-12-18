## 引言
连续介质建模是理解和预测材料在各种载荷与环境条件下行为的基石，它为连接原子尺度的微观世界与工程应用的宏观尺度提供了一套强大而优雅的数学与物理框架。然而，面对材料行为的复杂多样性——从弹性变形到[塑性流动](@entry_id:201346)，从[相变](@entry_id:147324)到断裂，再到[多物理场](@entry_id:164478)的相互耦合——研究人员和工程师迫切需要一个系统性的理论指南来构建准确的预测模型。本文旨在填补这一需求，为读者提供一套关于材料系统连续介质建模的完整知识体系。

在本文中，我们将踏上一段从基础到前沿的旅程。在“原理与机制”一章，我们将首先深入探讨描述变形与力的[运动学](@entry_id:173318)和动力学，并阐明所有[本构关系](@entry_id:186508)必须遵循的普适性物理原理。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章，我们将展示这些基本原理如何应用于解决[材料科学](@entry_id:152226)、地球物理和[生物力学](@entry_id:153973)等领域的复杂[耦合场问题](@entry_id:747960)和微结构-性能关系问题。最后，在“动手实践”部分，我们将通过具体的计算练习，指导您将抽象的理论转化为可执行的计算工具，从而巩固所学知识。

通过本章的学习，您将掌握构建和理解复杂材料模型所需的核心概念和方法论，为后续的学术研究或工程实践打下坚实的基础。

## 原理与机制

本章在前一章介绍的基础上，深入探讨材料系统连续介质建模的核心原理和关键机制。我们将从建立连续介质模型的抽象概念出发，系统地阐述描述材料变形与受力的[运动学](@entry_id:173318)和动力学框架。随后，我们将引入支配所有[本构关系](@entry_id:186508)的普适性物理原理，包括[热力学一致性](@entry_id:138886)和客观性。最后，我们将详细介绍几类重要的本构模型——超弹性、[弹塑性](@entry_id:193198)和广义连续介质模型（如[相场模型](@entry_id:202885)），并讨论将这些理论付诸计算的[变分原理](@entry_id:198028)和均匀化方法。

### 连续介质抽象：尺度与表征

连续介质力学的基石是**连续介质假设**，它假定物质完全填充其所占据的空间，忽略了其微观的原子或分子结构。这一假设的合理性取决于所研究问题的尺度。为了在微观结构（如晶粒、相或夹杂物）和宏观工程部件之间建立桥梁，我们引入了**[代表性](@entry_id:204613)体积单元（Representative Volume Element, RVE）**的概念。

一个RVE是一个足够大的材料体积，它在统计意义上能够代表整个材料的微观结构[特征和](@entry_id:189446)平均物理性质；同时，它又必须远小于宏观物理量（如应力、应变）发生显著变化的特征长度。这一要求可以用尺度分离准则来精确表述。考虑一个微观结构特征尺度为 $\ell_m$（例如，多晶金属的平均晶粒尺寸 $d$）的非均匀材料，其宏观行为由一个[特征长度](@entry_id:265857)为 $\ell_c$ 的外部载荷或几何形状决定。连续介质模型仅在存在一个RVE，其尺寸 $\ell_{rve}$ 满足如下[尺度分离](@entry_id:270204)条件时才有效：

$d \ll \ell_{rve} \ll \ell_c$

这个条件保证了在RVE尺度上进行的体积平均能够收敛到一个稳定的、具有代表性的有效属性。此外，为了能够将应力 $\sigma_{ij}(\mathbf{x})$ 和应变 $\varepsilon_{ij}(\mathbf{x})$ 等宏观场量处理为位置 $\mathbf{x}$ 的光滑（可微）函数，还需要微观属性涨落的[相关长度](@entry_id:143364) $\ell_m$ 远小于宏观[特征长度](@entry_id:265857) $\ell_c$。只有满足这些条件，我们才能用平滑的连续场来替代离散、非均匀的微观现实 。

### [运动学](@entry_id:173318)：描述变形

一旦接受了连续介质假设，我们便需要一套数学语言来精确描述材料的变形。一个物体的运动可以由一个映射 $\boldsymbol{\varphi}$ 描述，它将物体在**参考构型**（或称初始构型）中的每个物[质点](@entry_id:186768) $\mathbf{X}$ 映射到其在**当前构型**（或称变形后构型）中的空间位置 $\mathbf{x}$，即 $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$。

描述局部变形的核心物理量是**变形梯度（deformation gradient）**张量 $\mathbf{F}$，定义为：

$\mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}}$

变形梯度 $\mathbf{F}$ 是一个二阶张量，它将参考构型中的一个无穷小线元 $d\mathbf{X}$ 线性映射到当前构型中的对应[线元](@entry_id:196833) $d\mathbf{x}$，即 $d\mathbf{x} = \mathbf{F} d\mathbf{X}$ 。因此，$\mathbf{F}$ 包含了关于局部拉伸、剪切和旋转的全部信息。

为了将变形中的纯拉伸/压缩与刚体旋转分离开来，**极分解（polar decomposition）**定理至关重要。它表明任何可逆的变形梯度 $\mathbf{F}$ 都可以唯一地分解为一个纯拉伸[部分和](@entry_id:162077)一个旋转部分：

$\mathbf{F} = \mathbf{R}\mathbf{U}$

这里，$\mathbf{R}$ 是一个[旋转张量](@entry_id:191990)（即满足 $\mathbf{R}^T\mathbf{R}=\mathbf{I}$ 且 $\det \mathbf{R}=1$ 的正交张量），而 $\mathbf{U}$ 是一个对称正定的**右[拉伸张量](@entry_id:193200)（right stretch tensor）**。这个分解告诉我们，任何复杂的局部变形都可以看作是首先对物质进行纯拉伸（由 $\mathbf{U}$ 描述），然后再进行一次刚体旋转（由 $\mathbf{R}$ 描述）。

基于变形梯度，我们可以定义客观的（即不随刚体旋转而改变的）[应变度量](@entry_id:755495)。两个最基本的有限应变张量是：

1.  **[格林-拉格朗日应变张量](@entry_id:187745)（Green-Lagrange strain tensor）** $\mathbf{E}$：这是一个定义在参考构型上的度量，它通过**右柯西-格林（right Cauchy-Green）**变形张量 $\mathbf{C} = \mathbf{F}^T\mathbf{F}$ 来定义：
    $\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})$
    由于 $\mathbf{C} = (\mathbf{RU})^T(\mathbf{RU}) = \mathbf{U}^T\mathbf{R}^T\mathbf{R}\mathbf{U} = \mathbf{U}^2$，所以 $\mathbf{E} = \frac{1}{2}(\mathbf{U}^2 - \mathbf{I})$。这清晰地表明，$\mathbf{E}$ 只依赖于[拉伸张量](@entry_id:193200) $\mathbf{U}$，而与旋转 $\mathbf{R}$ 无关。因此，$\mathbf{E}$ 度量的是纯粹的变形。对于[刚体运动](@entry_id:193355)（无变形），$\mathbf{F}=\mathbf{R}$，此时 $\mathbf{U}=\mathbf{I}$，$\mathbf{C}=\mathbf{I}$，因此 $\mathbf{E}=\mathbf{0}$ 。

2.  **[欧拉-阿尔曼西应变张量](@entry_id:194948)（Euler-Almansi strain tensor）** $\mathbf{e}$：这是一个定义在当前构型上的度量，它通过**左柯西-格林（left Cauchy-Green）**变形张量 $\mathbf{B} = \mathbf{F}\mathbf{F}^T$ 的逆来定义：
    $\mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{B}^{-1})$
    与 $\mathbf{E}$ 类似，$\mathbf{e}$ 也是一个客观的[应变度量](@entry_id:755495)，对于刚体运动同样为零。

考虑一个简单的思想实验：均匀简单剪切。其变形梯度为 $\mathbf{F} = \begin{pmatrix} 1  \gamma  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix}$。通过直接计算，我们可以得到[格林-拉格朗日应变张量](@entry_id:187745)为 $\mathbf{E} = \begin{pmatrix} 0  \gamma/2  0 \\ \gamma/2  \gamma^2/2  0 \\ 0  0  0 \end{pmatrix}$。值得注意的是，除了预期的剪切分量 $E_{12}$ 外，还出现了一个正交分量 $E_{22} = \gamma^2/2$。这表明，在有限变形理论中，简单剪切不仅仅是“滑动”，还伴随着沿剪切方向的拉伸。同样，[欧拉-阿尔曼西应变](@entry_id:187104)为 $\mathbf{e} = \begin{pmatrix} 0  \gamma/2  0 \\ \gamma/2  -\gamma^2/2  0 \\ 0  0  0 \end{pmatrix}$，也包含了这种高阶效应 。

### 动力学：描述力与应力

描述了变形之后，我们需要描述物体内部的力。**柯西[应力张量](@entry_id:148973)（Cauchy stress tensor）** $\boldsymbol{\sigma}$ 是描述物体内部应力状态最直观的物理量。它是一个定义在**当前构型**中的对称张量，通过柯西定理与作用在任意[截面](@entry_id:154995)上的**真实面力（traction）** $\mathbf{t}$（单位当前面积上的力）相关联：

$\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$

其中 $\mathbf{n}$ 是当前构型中[截面](@entry_id:154995)的[单位法向量](@entry_id:178851)。

然而，在有限变形问题中，边界条件和本构关系通常在固定的**参考构型**上定义更为方便。这就需要引入与参考构型相关的[应力张量](@entry_id:148973)。

1.  **[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量（First Piola-Kirchhoff stress, PK1）** $\mathbf{P}$：也称为**名义应力（nominal stress）**，它将当前构型中的力与参考构型中的面积联系起来。定义名义面力 $\mathbf{T}$ 为单位参考面积上的力，则有 $\mathbf{T} = \mathbf{P}\mathbf{N}$，其中 $\mathbf{N}$ 是参考构型中的[单位法向量](@entry_id:178851)。$\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 之间的关系可以通过力元 $d\mathbf{f}$ 的等效性推导出来：$d\mathbf{f} = \mathbf{t} da = \mathbf{T} dA$。结合变形梯度对[面积元](@entry_id:263205)的变换关系（[Nanson公式](@entry_id:195566)：$\mathbf{n}da = J\mathbf{F}^{-T}\mathbf{N}dA$，其中 $J = \det \mathbf{F}$），可以得到：
    $\mathbf{P} = J\boldsymbol{\sigma}\mathbf{F}^{-T}$
    $\mathbf{P}$ 是一个非对称的“两点”张量，因为它将参考构型中的一个向量（$\mathbf{N}$）映射到当前构型中的另一个向量（$\mathbf{T}$）。

2.  **[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量（Second Piola-Kirchhoff stress, PK2）** $\mathbf{S}$：这是一个完全在参考构型中定义的[对称张量](@entry_id:148092)。它通过将力元 $d\mathbf{f}$ “[拉回](@entry_id:160816)”到参考构型得到一个[伪力](@entry_id:169104)矢量 $d\mathbf{F}_0 = \mathbf{F}^{-1}d\mathbf{f}$ 来构造。$\mathbf{S}$ 的定义是 $d\mathbf{F}_0 = \mathbf{S}\mathbf{N}dA$。由此可得 $\mathbf{S}$ 与 $\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 的关系：
    $\mathbf{S} = \mathbf{F}^{-1}\mathbf{P}$
    $\mathbf{S} = J\mathbf{F}^{-1}\boldsymbol{\sigma}\mathbf{F}^{-T}$
    $\mathbf{S}$ 与[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$ 在能量上是共轭的（即它们的[点积](@entry_id:149019) $\mathbf{S}:\dot{\mathbf{E}}$ 代表单位参考体积的功率），这使得 $\mathbf{S}$ 在超弹性等理论中极为有用 。

### 本构模型的基本原理

[运动学](@entry_id:173318)和动力学提供了描述变形和应力的语言，但它们本身不足以确定材料的行为。我们需要**本构关系（constitutive relations）**，即[应力与应变](@entry_id:137374)（或其历史）之间的关系，来封闭[方程组](@entry_id:193238)。任何物理上合理的本构模型都必须遵循某些[普适性原理](@entry_id:137218)。

#### [热力学一致性](@entry_id:138886)

材料的响应必须服从[热力学定律](@entry_id:202285)。对于连续介质，这些定律的局部形式为：

*   **第一定律（[能量守恒](@entry_id:140514)）**：单位质量内能 $e$ 的变化率等于[应力功率](@entry_id:182907)、热流散度和外部热源之和。
    $\rho \dot{e} = \boldsymbol{\sigma} : \nabla \mathbf{v} - \nabla \cdot \mathbf{q} + \rho r$
    其中 $\rho$ 是密度，$\mathbf{v}$ 是[速度场](@entry_id:271461)，$\mathbf{q}$ 是热流矢量， $r$ 是单位质量的外部热源。

*   **第二定律（[熵增原理](@entry_id:142282)）**：总熵产必须为非负。其局部形式，即**克劳修斯-杜恩（Clausius-Duhem）不等式**，规定了熵 $s$ 的增长必须大于等于由热流和热源贡献的部分。
    $\rho \dot{s} \ge - \nabla \cdot (\frac{\mathbf{q}}{T}) + \frac{\rho r}{T}$
    其中 $T$ 是绝对温度。

为了更方便地应用于力学问题，通常引入**亥姆霍兹自由能（Helmholtz free energy）** $\psi = e - Ts$。通过一系列推导，可以将上述两个定律合并为一个单一的[耗散不等式](@entry_id:188634) ：

$\rho \dot{\psi} + \rho s \dot{T} \le \boldsymbol{\sigma} : \nabla \mathbf{v} - \frac{1}{T} \mathbf{q} \cdot \nabla T$

这个不等式是构建本构理论的出发点。左边代表自由能的变化率，右边代表外力做功和热传导引起的耗散。它严格约束了材料的响应方式，任何本构模型都必须保证对于所有可能的过程，这个不等式恒成立。

#### [客观性原理](@entry_id:185412)

**[客观性原理](@entry_id:185412)（principle of objectivity）**，或称**物质标架无关性（material frame indifference）**，要求[本构关系](@entry_id:186508)不能依赖于观察者。如果两个观察者以一个[刚体运动](@entry_id:193355)相互关联，即 $\mathbf{x}^*(t) = \mathbf{Q}(t)\mathbf{x}(t) + \mathbf{c}(t)$，其中 $\mathbf{Q}(t)$ 是一个时变的旋转，他们观察到的物理定律和材料响应应该是等效的。

这要求本构关系中的所有物理量都必须是**客观的**。一个客观的标量、矢量或张量在观察者变换下会遵循特定的变换法则：
*   客观标量 $\phi^* = \phi$
*   客观矢量 $\mathbf{v}^* = \mathbf{Q}\mathbf{v}$
*   客观二阶张量 $\mathbf{T}^* = \mathbf{Q}\mathbf{T}\mathbf{Q}^T$

例如，柯西应力 $\boldsymbol{\sigma}$ 和[左柯西-格林张量](@entry_id:186163) $\mathbf{B}$ 都是客观的二阶张量，而变形梯度 $\mathbf{F}$ 却不是（其变换规律为 $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$）。因此，一个[本构关系](@entry_id:186508)如果直接写作 $\boldsymbol{\sigma} = f(\mathbf{F})$ 通常是不允许的。[客观性原理](@entry_id:185412)要求本构函数的形式必须满足特定的[等变性](@entry_id:636671)条件，例如对于一个能量函数 $\psi(\mathbf{F})$，客观性要求 $\psi(\mathbf{F}) = \psi(\mathbf{QF})$ 对所有旋转 $\mathbf{Q}$ 成立。这等价于要求 $\psi$ 只能通过[右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^T\mathbf{F}$ 来依赖于 $\mathbf{F}$。

[客观性原理](@entry_id:185412)是关于*空间*的变换，它适用于所有材料。这必须与**[材料对称性](@entry_id:190289)（material symmetry）**严格区分。[材料对称性](@entry_id:190289)是材料自身的固有属性，它描述了材料在*参考构型*中经过某些变换（如[晶体对称性](@entry_id:198772)操作）后响应不变的特性。其数学表达为 $\psi(\mathbf{F}) = \psi(\mathbf{FS})$，其中 $\mathbf{S}$ 是[材料对称群](@entry_id:185879)中的一个变换。客观性是普适的约束，而[材料对称性](@entry_id:190289)则因材料而异 。

### 机制与模型：具体的本构理论

基于上述原理，我们可以构建描述不同材料行为的具体模型。

#### 超弹性

**超弹性（Hyperelasticity）**材料是一种理想的弹性材料，其应力完全由当前变形状态决定，且[应力-应变关系](@entry_id:274093)可以从一个标量势函数——**[应变能密度函数](@entry_id:755490)（strain-energy density function）** $\psi$ ——导出。这意味着变形过程是可逆的，没有[能量耗散](@entry_id:147406)。

对于[超弹性材料](@entry_id:190241)，我们可以定义[应变能](@entry_id:162699) $\psi$ 是[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$ 或[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 的函数。[第二皮奥拉-基尔霍夫应力](@entry_id:173163)可以直接通过求导得到：

$\mathbf{S} = \frac{\partial \psi}{\partial \mathbf{E}} = 2\frac{\partial \psi}{\partial \mathbf{C}}$

对于许多材料，如橡胶和生物软组织，其变形行为可以近似地分解为体积改变和形状改变两部分。这启发了**体积-等容分解（volumetric-isochoric split）**的思想。[应变能函数](@entry_id:178435)可以写成两部分之和：

$\psi(\mathbf{F}) = \psi_{\text{vol}}(J) + \psi_{\text{iso}}(\bar{\mathbf{B}})$

其中，$\psi_{\text{vol}}$ 只依赖于体积变化比 $J = \det \mathbf{F}$，描述了材料对体积变化的抵抗；而 $\psi_{\text{iso}}$ 描述了等体积（$J=1$）变形下的能量存储。$\psi_{\text{iso}}$ 通常是**修正的[左柯西-格林张量](@entry_id:186163)** $\bar{\mathbf{B}} = J^{-2/3}\mathbf{B}$ 的[不变量](@entry_id:148850)的函数。$\bar{\mathbf{B}}$ 的引入巧妙地移除了体积变化的影响（$\det \bar{\mathbf{B}} = 1$）。这种分解使得[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau} = J\boldsymbol{\sigma}$ 也能够相应地分解为一个球应力部分（来自 $\psi_{\text{vol}}$）和一个[偏应力](@entry_id:163323)部分（来自 $\psi_{\text{iso}}$），后者是无迹的，即 $\operatorname{tr}(\boldsymbol{\tau}_{\text{iso}}) = 0$ 。

#### 有限应变[弹塑性](@entry_id:193198)

与[超弹性材料](@entry_id:190241)不同，金属等材料在加载超过一定限度后会发生不可逆的**塑性变形**，并伴随能量耗散。描述这类行为的模型要复杂得多。一个标准框架是基于**变形梯度的[乘法分解](@entry_id:199514)**：

$\mathbf{F} = \mathbf{F}^e \mathbf{F}^p$

这个分解假设总变形可以被概念性地分解为两步：首先是塑性变形 $\mathbf{F}^p$，它改变材料的微观结构并导致永久变形，将物质点从参考构型映射到一个假想的**[中间构型](@entry_id:193000)**；然后是弹性变形 $\mathbf{F}^e$，它从[中间构型](@entry_id:193000)弹性地加载到最终的当前构型。对于金属，通常假设塑性变形是不可压缩的，即 $\det \mathbf{F}^p = 1$。

在这个框架下，亥姆霍兹自由能 $\psi$ 被认为是弹性变形 $\mathbf{F}^e$ 和描述硬化状态的内变量的函数。热力学第二定律（[耗散不等式](@entry_id:188634)）表明，塑性流动的驱动力（即与塑性变形速率共轭的应力）是**[Mandel应力](@entry_id:191786)** $\boldsymbol{\tau} = \mathbf{C}_e \mathbf{S}_e$，其中 $\mathbf{C}_e$ 和 $\mathbf{S}_e$ 是定义在[中间构型](@entry_id:193000)上的弹性的柯西-格林张量和第二PK应力。

[塑性流动](@entry_id:201346)何时发生由一个**[屈服函数](@entry_id:167970)** $f(\boldsymbol{\tau}, \kappa) \le 0$ 决定，其中 $\kappa$ 是[硬化](@entry_id:177483)变量。对于压强不敏感的金属，[屈服函数](@entry_id:167970)通常只依赖于[Mandel应力](@entry_id:191786)的偏量部分 $\text{dev}\,\boldsymbol{\tau}$。一个典型的例子是[von Mises屈服准则](@entry_id:174339)。塑性流动的方向由**[流动法则](@entry_id:177163)**给出，在关联塑性中，塑性[应变率](@entry_id:154778)的方向垂直于[屈服面](@entry_id:175331)：

$\mathbf{D}_p = \dot{\gamma} \frac{\partial f}{\partial \boldsymbol{\tau}}$

其中 $\mathbf{D}_p$ 是塑性变形速率张量，$\dot{\gamma}$ 是塑性乘子。由于[屈服函数](@entry_id:167970)只依赖于[偏应力](@entry_id:163323)，这个流动法则自然保证了 $\text{tr}(\mathbf{D}_p) = 0$，从而满足了[塑性不可压缩性](@entry_id:183440)条件 。

#### 广义连续介质模型：相场方法

经典连续介质模型在描述具有内部结构（如[相界面](@entry_id:172947)、裂纹、[位错](@entry_id:157482)）的材料时会遇到困难。**广义连续介质模型**通过引入额外的场变量来克服这些限制。**[相场模型](@entry_id:202885)（phase-field models）**是一个突出的例子，它引入一个或多个连续的**内部变量**（或称序参量） $\alpha(\mathbf{x}, t)$ 来描述微观结构的状态，例如，$\alpha=0$ 代表一个相，$\alpha=1$ 代表另一个相，而 $0  \alpha  1$ 的区域则代表两相之间的弥散界面。

为了描述界面本身所存储的能量，[自由能函数](@entry_id:749582)不仅依赖于序参量 $\alpha$，还依赖于它的梯度 $\nabla \alpha$：

$\psi(\alpha, \nabla \alpha) = \psi_0(\alpha) + \frac{\kappa}{2}|\nabla \alpha|^2$

这里的 $\psi_0(\alpha)$ 是局部自由能（通常是一个双阱势，其极小值对应于稳定相），而梯度项 $\frac{\kappa}{2}|\nabla \alpha|^2$ 则惩罚了[序参量](@entry_id:144819)的剧烈空间变化，代表了**[界面能](@entry_id:198323)**。

与序参量的演化相对应，需要引入广义的力。我们公设一个**微[力平衡](@entry_id:267186)（microforce balance）**方程：$\pi - \nabla \cdot \boldsymbol{\xi} = 0$。这里，$\boldsymbol{\xi}$ 是与梯度 $\nabla\alpha$ 共轭的矢量微力（或称微应力），而 $\pi$ 是与 $\alpha$ 变化率 $\dot{\alpha}$ 共轭的标量内力。通过[热力学[一致](@entry_id:138886)性分析](@entry_id:189411)（Coleman-Noll程序），可以确定这些力的保守部分（即能量部分）为：

$\boldsymbol{\xi} = \frac{\partial \psi}{\partial (\nabla \alpha)} = \kappa \nabla \alpha$
$\pi^{\text{cons}} = \frac{\partial \psi}{\partial \alpha} = \frac{d\psi_0}{d\alpha}$

在平衡状态下，[耗散力](@entry_id:166970)为零，微力[平衡方程](@entry_id:172166)就变成一个关于 $\alpha$ 的[偏微分方程](@entry_id:141332)，即**艾伦-凯恩（Allen-Cahn）方程** ：

$\frac{d\psi_0}{d\alpha} - \kappa \Delta \alpha = 0$

这个方程描述了在没有外部驱动力时，系统如何通过演化其内部结构来最小化总自由能。

### 从理论到计算：变分原理与均匀化

#### 虚功原理

上述本构模型最终都表现为一组[偏微分方程](@entry_id:141332)（强形式），例如静态[平衡方程](@entry_id:172166) $\text{Div}\,\mathbf{P} + \rho\mathbf{b} = \mathbf{0}$。直接求解这些方程通常很困难。**虚功原理（principle of virtual work）**为数值求解（如有限元方法, FEM）提供了基础。它将[偏微分方程](@entry_id:141332)重新表述为一个积分形式的**[弱形式](@entry_id:142897)（weak form）**。

其思想是对平衡方程乘以一个任意的、满足[位移边界条件](@entry_id:203261)的**[虚位移](@entry_id:168781)（virtual displacement）** $\delta\mathbf{u}$，然后在整个求解域 $\Omega$ 上积分。通过分部积分（[格林公式](@entry_id:173118)），可以将应力项的导数转移到[虚位移](@entry_id:168781)上，从而降低对解的光滑性要求，并自然地引入力边界条件。对于静态[平衡问题](@entry_id:636409)，[虚功原理](@entry_id:138749)表明，对于任何容许的[虚位移](@entry_id:168781)，[内力](@entry_id:167605)所做的[虚功](@entry_id:176403)等于外力所做的[虚功](@entry_id:176403) ：

$\underbrace{\int_{\Omega} \mathbf{P} : \nabla \delta \mathbf{u} \, d\Omega}_{\delta W_{\text{int}}} = \underbrace{\int_{\Omega} \rho \mathbf{b} \cdot \delta \mathbf{u} \, d\Omega + \int_{\partial \Omega_t} \bar{\mathbf{t}} \cdot \delta \mathbf{u} \, dS}_{\delta W_{\text{ext}}}$

这个[积分方程](@entry_id:138643)是有限元法的出发点，它将一个连续介质力学问题转化为了一个（通常是）[非线性](@entry_id:637147)的[代数方程](@entry_id:272665)组。

#### [计算均匀化](@entry_id:163942)

对于具有复杂微观结构的材料，直接对其宏观部件进行包含所有微观细节的建模在计算上是不可行的。**[计算均匀化](@entry_id:163942)**方法提供了一个多尺度框架来解决此问题。其核心思想是在宏观模型的每个积分点上，求解一个RVE的边界值问题来计算该点的有效（或称均匀化）应力和本构响应。

这个多尺度连接的关键是能量的一致性，由**希尔-曼德尔（Hill-Mandel）条件**保证。该条件要求RVE尺度上微观应力和[应变率](@entry_id:154778)功率的体积平均值等于宏观尺度上宏观应力和[应变率](@entry_id:154778)的功率：

$\langle \boldsymbol{\sigma} : \dot{\boldsymbol{\epsilon}} \rangle = \boldsymbol{\Sigma} : \dot{\mathbf{E}}$

其中 $\langle \cdot \rangle$ 表示在RVE上的体积平均，小写字母代表微观量，大写字母代表宏观量。为了在RVE的计算中满足这个条件，需要施加特定的边界条件。最常见的三种包括 ：

1.  **运动学均匀边界条件（KUBC）**：在RVE边界上施加与宏观应变 $\mathbf{E}$ 一致的线性位移，即 $\mathbf{u} = \mathbf{E}\mathbf{x}$。
2.  **静态均匀边界条件（SUBC）**：在RVE边界上施加与宏观应力 $\boldsymbol{\Sigma}$ 一致的面力，即 $\mathbf{t} = \boldsymbol{\Sigma}\mathbf{n}$。
3.  **[周期性边界条件](@entry_id:147809)（PBC）**：要求[位移场](@entry_id:141476)为宏观线性位移与一个周期性涨落之和，同时面力在RVE相对的面上呈反周期[分布](@entry_id:182848)。

这些边界[条件模拟](@entry_id:747666)了RVE嵌入在一个经受均匀宏观变形的无限大介质中的不同理想情况，从而使得从微观计算得到的有效宏观响应在能量上是自洽的。