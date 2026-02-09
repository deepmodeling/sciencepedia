## 引言
连续介质建模是理解和预测材料在各种载荷与环境条件下行为的基石，它为连接原子尺度的微观世界与工程应用的宏观尺度提供了一套强大而优雅的数学与物理框架。然而，面对材料行为的复杂多样性——从弹性变形到塑性流动，从相变到断裂，再到多物理场的相互耦合——研究人员和工程师迫切需要一个系统性的理论指南来构建准确的预测模型。本文旨在填补这一需求，为读者提供一套关于材料系统连续介质建模的完整知识体系。

在本文中，我们将踏上一段从基础到前沿的旅程。在“原理与机制”一章，我们将首先深入探讨描述变形与力的运动学和动力学，并阐明所有本构关系必须遵循的普适性物理原理。接着，在“应用与交叉学科联系”一章，我们将展示这些基本原理如何应用于解决材料科学、地球物理和生物力学等领域的复杂耦合场问题和微结构-性能关系问题。最后，在“动手实践”部分，我们将通过具体的计算练习，指导您将抽象的理论转化为可执行的计算工具，从而巩固所学知识。

通过本章的学习，您将掌握构建和理解复杂材料模型所需的核心概念和方法论，为后续的学术研究或工程实践打下坚实的基础。

## 原理与机制

本章在前一章介绍的基础上，深入探讨材料系统连续介质建模的核心原理和关键机制。我们将从建立连续介质模型的抽象概念出发，系统地阐述描述材料变形与受力的运动学和动力学框架。随后，我们将引入支配所有本构关系的普适性物理原理，包括热力学一致性和客观性。最后，我们将详细介绍几类重要的本构模型——超弹性、弹塑性和广义连续介质模型（如相场模型），并讨论将这些理论付诸计算的变分原理和均匀化方法。

### 连续介质抽象：尺度与表征

连续介质力学的基石是**连续介质假设**，它假定物质完全填充其所占据的空间，忽略了其微观的原子或分子结构。这一假设的合理性取决于所研究问题的尺度。为了在微观结构（如晶粒、相或夹杂物）和宏观工程部件之间建立桥梁，我们引入了**代表性体积单元（Representative Volume Element, RVE）**的概念。

一个RVE是一个足够大的材料体积，它在统计意义上能够代表整个材料的微观结构特征和平均物理性质；同时，它又必须远小于宏观物理量（如应力、应变）发生显著变化的特征长度。这一要求可以用尺度分离准则来精确表述。考虑一个微观结构特征尺度为 $\ell_m$（例如，多晶金属的平均晶粒尺寸 $d$）的非均匀材料，其宏观行为由一个特征长度为 $\ell_c$ 的外部载荷或几何形状决定。连续介质模型仅在存在一个RVE，其尺寸 $\ell_{rve}$ 满足如下尺度分离条件时才有效：

$d \ll \ell_{rve} \ll \ell_c$

这个条件保证了在RVE尺度上进行的体积平均能够收敛到一个稳定的、具有代表性的有效属性。此外，为了能够将应力 $\sigma_{ij}(\mathbf{x})$ 和应变 $\varepsilon_{ij}(\mathbf{x})$ 等宏观场量处理为位置 $\mathbf{x}$ 的光滑（可微）函数，还需要微观属性涨落的相关长度 $\ell_m$ 远小于宏观特征长度 $\ell_c$。只有满足这些条件，我们才能用平滑的连续场来替代离散、非均匀的微观现实 [@problem_id:3440406]。

### 运动学：描述变形

一旦接受了连续介质假设，我们便需要一套数学语言来精确描述材料的变形。一个物体的运动可以由一个映射 $\boldsymbol{\varphi}$ 描述，它将物体在**参考构型**（或称初始构型）中的每个物质点 $\mathbf{X}$ 映射到其在**当前构型**（或称变形后构型）中的空间位置 $\mathbf{x}$，即 $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$。

描述局部变形的核心物理量是**变形梯度（deformation gradient）**张量 $\mathbf{F}$，定义为：

$\mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}}$

变形梯度 $\mathbf{F}$ 是一个二阶张量，它将参考构型中的一个无穷小线元 $d\mathbf{X}$ 线性映射到当前构型中的对应线元 $d\mathbf{x}$，即 $d\mathbf{x} = \mathbf{F} d\mathbf{X}$ [@problem_id:3440431]。因此，$\mathbf{F}$ 包含了关于局部拉伸、剪切和旋转的全部信息。

为了将变形中的纯拉伸/压缩与刚体旋转分离开来，**极分解（polar decomposition）**定理至关重要。它表明任何可逆的变形梯度 $\mathbf{F}$ 都可以唯一地分解为一个纯拉伸部分和一个旋转部分：

$\mathbf{F} = \mathbf{R}\mathbf{U}$

这里，$\mathbf{R}$ 是一个旋转张量（即满足 $\mathbf{R}^T\mathbf{R}=\mathbf{I}$ 且 $\det \mathbf{R}=1$ 的正交张量），而 $\mathbf{U}$ 是一个对称正定的**右拉伸张量（right stretch tensor）**。这个分解告诉我们，任何复杂的局部变形都可以看作是首先对物质进行纯拉伸（由 $\mathbf{U}$ 描述），然后再进行一次刚体旋转（由 $\mathbf{R}$ 描述）。

基于变形梯度，我们可以定义客观的（即不随刚体旋转而改变的）应变度量。两个最基本的有限应变张量是：

1.  **格林-拉格朗日应变张量（Green-Lagrange strain tensor）** $\mathbf{E}$：这是一个定义在参考构型上的度量，它通过**右柯西-格林（right Cauchy-Green）**变形张量 $\mathbf{C} = \mathbf{F}^T\mathbf{F}$ 来定义：
    $\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})$
    由于 $\mathbf{C} = (\mathbf{RU})^T(\mathbf{RU}) = \mathbf{U}^T\mathbf{R}^T\mathbf{R}\mathbf{U} = \mathbf{U}^2$，所以 $\mathbf{E} = \frac{1}{2}(\mathbf{U}^2 - \mathbf{I})$。这清晰地表明，$\mathbf{E}$ 只依赖于拉伸张量 $\mathbf{U}$，而与旋转 $\mathbf{R}$ 无关。因此，$\mathbf{E}$ 度量的是纯粹的变形。对于刚体运动（无变形），$\mathbf{F}=\mathbf{R}$，此时 $\mathbf{U}=\mathbf{I}$，$\mathbf{C}=\mathbf{I}$，因此 $\mathbf{E}=\mathbf{0}$ [@problem_id:3440431]。

2.  **欧拉-阿尔曼西应变张量（Euler-Almansi strain tensor）** $\mathbf{e}$：这是一个定义在当前构型上的度量，它通过**左柯西-格林（left Cauchy-Green）**变形张量 $\mathbf{B} = \mathbf{F}\mathbf{F}^T$ 的逆来定义：
    $\mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{B}^{-1})$
    与 $\mathbf{E}$ 类似，$\mathbf{e}$ 也是一个客观的应变度量，对于刚体运动同样为零。

考虑一个简单的思想实验：均匀简单剪切。其变形梯度为 $\mathbf{F} = \begin{pmatrix} 1  \gamma  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix}$。通过直接计算，我们可以得到格林-拉格朗日应变张量为 $\mathbf{E} = \begin{pmatrix} 0  \gamma/2  0 \\ \gamma/2  \gamma^2/2  0 \\ 0  0  0 \end{pmatrix}$。值得注意的是，除了预期的剪切分量 $E_{12}$ 外，还出现了一个正交分量 $E_{22} = \gamma^2/2$。这表明，在有限变形理论中，简单剪切不仅仅是“滑动”，还伴随着沿剪切方向的拉伸。同样，欧拉-阿尔曼西应变为 $\mathbf{e} = \begin{pmatrix} 0  \gamma/2  0 \\ \gamma/2  -\gamma^2/2  0 \\ 0  0  0 \end{pmatrix}$，也包含了这种高阶效应 [@problem_id:3440431]。

### 动力学：描述力与应力

描述了变形之后，我们需要描述物体内部的力。**柯西应力张量（Cauchy stress tensor）** $\boldsymbol{\sigma}$ 是描述物体内部应力状态最直观的物理量。它是一个定义在**当前构型**中的对称张量，通过柯西定理与作用在任意截面上的**真实面力（traction）** $\mathbf{t}$（单位当前面积上的力）相关联：

$\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$

其中 $\mathbf{n}$ 是当前构型中截面的单位法向量。

然而，在有限变形问题中，边界条件和本构关系通常在固定的**参考构型**上定义更为方便。这就需要引入与参考构型相关的应力张量。

1.  **第一皮奥拉-基尔霍夫应力张量（First Piola-Kirchhoff stress, PK1）** $\mathbf{P}$：也称为**名义应力（nominal stress）**，它将当前构型中的力与参考构型中的面积联系起来。定义名义面力 $\mathbf{T}$ 为单位参考面积上的力，则有 $\mathbf{T} = \mathbf{P}\mathbf{N}$，其中 $\mathbf{N}$ 是参考构型中的单位法向量。$\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 之间的关系可以通过力元 $d\mathbf{f}$ 的等效性推导出来：$d\mathbf{f} = \mathbf{t} da = \mathbf{T} dA$。结合变形梯度对面积元的变换关系（Nanson公式：$\mathbf{n}da = J\mathbf{F}^{-T}\mathbf{N}dA$，其中 $J = \det \mathbf{F}$），可以得到：
    $\mathbf{P} = J\boldsymbol{\sigma}\mathbf{F}^{-T}$
    $\mathbf{P}$ 是一个非对称的“两点”张量，因为它将参考构型中的一个向量（$\mathbf{N}$）映射到当前构型中的另一个向量（$\mathbf{T}$）。

2.  **第二皮奥拉-基尔霍夫应力张量（Second Piola-Kirchhoff stress, PK2）** $\mathbf{S}$：这是一个完全在参考构型中定义的对称张量。它通过将力元 $d\mathbf{f}$ “拉回”到参考构型得到一个伪力矢量 $d\mathbf{F}_0 = \mathbf{F}^{-1}d\mathbf{f}$ 来构造。$\mathbf{S}$ 的定义是 $d\mathbf{F}_0 = \mathbf{S}\mathbf{N}dA$。由此可得 $\mathbf{S}$ 与 $\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 的关系：
    $\mathbf{S} = \mathbf{F}^{-1}\mathbf{P}$
    $\mathbf{S} = J\mathbf{F}^{-1}\boldsymbol{\sigma}\mathbf{F}^{-T}$
    $\mathbf{S}$ 与格林-拉格朗日应变 $\mathbf{E}$ 在能量上是共轭的（即它们的点积 $\mathbf{S}:\dot{\mathbf{E}}$ 代表单位参考体积的功率），这使得 $\mathbf{S}$ 在超弹性等理论中极为有用 [@problem_id:3440411]。

### 本构模型的基本原理

运动学和动力学提供了描述变形和应力的语言，但它们本身不足以确定材料的行为。我们需要**本构关系（constitutive relations）**，即应力与应变（或其历史）之间的关系，来封闭方程组。任何物理上合理的本构模型都必须遵循某些普适性原理。

#### 热力学一致性

材料的响应必须服从热力学定律。对于连续介质，这些定律的局部形式为：

*   **第一定律（能量守恒）**：单位质量内能 $e$ 的变化率等于应力功率、热流散度和外部热源之和。
    $\rho \dot{e} = \boldsymbol{\sigma} : \nabla \mathbf{v} - \nabla \cdot \mathbf{q} + \rho r$
    其中 $\rho$ 是密度，$\mathbf{v}$ 是速度场，$\mathbf{q}$ 是热流矢量， $r$ 是单位质量的外部热源。

*   **第二定律（熵增原理）**：总熵产必须为非负。其局部形式，即**克劳修斯-杜恩（Clausius-Duhem）不等式**，规定了熵 $s$ 的增长必须大于等于由热流和热源贡献的部分。
    $\rho \dot{s} \ge - \nabla \cdot (\frac{\mathbf{q}}{T}) + \frac{\rho r}{T}$
    其中 $T$ 是绝对温度。

为了更方便地应用于力学问题，通常引入**亥姆霍兹自由能（Helmholtz free energy）** $\psi = e - Ts$。通过一系列推导，可以将上述两个定律合并为一个单一的耗散不等式 [@problem_id:3440469]：

$\rho \dot{\psi} + \rho s \dot{T} \le \boldsymbol{\sigma} : \nabla \mathbf{v} - \frac{1}{T} \mathbf{q} \cdot \nabla T$

这个不等式是构建本构理论的出发点。左边代表自由能的变化率，右边代表外力做功和热传导引起的耗散。它严格约束了材料的响应方式，任何本构模型都必须保证对于所有可能的过程，这个不等式恒成立。

#### 客观性原理

**客观性原理（principle of objectivity）**，或称**物质标架无关性（material frame indifference）**，要求本构关系不能依赖于观察者。如果两个观察者以一个刚体运动相互关联，即 $\mathbf{x}^*(t) = \mathbf{Q}(t)\mathbf{x}(t) + \mathbf{c}(t)$，其中 $\mathbf{Q}(t)$ 是一个时变的旋转，他们观察到的物理定律和材料响应应该是等效的。

这要求本构关系中的所有物理量都必须是**客观的**。一个客观的标量、矢量或张量在观察者变换下会遵循特定的变换法则：
*   客观标量 $\phi^* = \phi$
*   客观矢量 $\mathbf{v}^* = \mathbf{Q}\mathbf{v}$
*   客观二阶张量 $\mathbf{T}^* = \mathbf{Q}\mathbf{T}\mathbf{Q}^T$

例如，柯西应力 $\boldsymbol{\sigma}$ 和左柯西-格林张量 $\mathbf{B}$ 都是客观的二阶张量，而变形梯度 $\mathbf{F}$ 却不是（其变换规律为 $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$）。因此，一个本构关系如果直接写作 $\boldsymbol{\sigma} = f(\mathbf{F})$ 通常是不允许的。客观性原理要求本构函数的形式必须满足特定的等变性条件，例如对于一个能量函数 $\psi(\mathbf{F})$，客观性要求 $\psi(\mathbf{F}) = \psi(\mathbf{QF})$ 对所有旋转 $\mathbf{Q}$ 成立。这等价于要求 $\psi$ 只能通过右柯西-格林张量 $\mathbf{C} = \mathbf{F}^T\mathbf{F}$ 来依赖于 $\mathbf{F}$。

客观性原理是关于*空间*的变换，它适用于所有材料。这必须与**材料对称性（material symmetry）**严格区分。材料对称性是材料自身的固有属性，它描述了材料在*参考构型*中经过某些变换（如晶体对称性操作）后响应不变的特性。其数学表达为 $\psi(\mathbf{F}) = \psi(\mathbf{FS})$，其中 $\mathbf{S}$ 是材料对称群中的一个变换。客观性是普适的约束，而材料对称性则因材料而异 [@problem_id:3440475]。

### 机制与模型：具体的本构理论

基于上述原理，我们可以构建描述不同材料行为的具体模型。

#### 超弹性

**超弹性（Hyperelasticity）**材料是一种理想的弹性材料，其应力完全由当前变形状态决定，且应力-应变关系可以从一个标量势函数——**应变能密度函数（strain-energy density function）** $\psi$ ——导出。这意味着变形过程是可逆的，没有能量耗散。

对于超弹性材料，我们可以定义应变能 $\psi$ 是格林-拉格朗日应变 $\mathbf{E}$ 或右柯西-格林张量 $\mathbf{C}$ 的函数。第二皮奥拉-基尔霍夫应力可以直接通过求导得到：

$\mathbf{S} = \frac{\partial \psi}{\partial \mathbf{E}} = 2\frac{\partial \psi}{\partial \mathbf{C}}$

对于许多材料，如橡胶和生物软组织，其变形行为可以近似地分解为体积改变和形状改变两部分。这启发了**体积-等容分解（volumetric-isochoric split）**的思想。应变能函数可以写成两部分之和：

$\psi(\mathbf{F}) = \psi_{\text{vol}}(J) + \psi_{\text{iso}}(\bar{\mathbf{B}})$

其中，$\psi_{\text{vol}}$ 只依赖于体积变化比 $J = \det \mathbf{F}$，描述了材料对体积变化的抵抗；而 $\psi_{\text{iso}}$ 描述了等体积（$J=1$）变形下的能量存储。$\psi_{\text{iso}}$ 通常是**修正的左柯西-格林张量** $\bar{\mathbf{B}} = J^{-2/3}\mathbf{B}$ 的不变量的函数。$\bar{\mathbf{B}}$ 的引入巧妙地移除了体积变化的影响（$\det \bar{\mathbf{B}} = 1$）。这种分解使得基尔霍夫应力 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$ 也能够相应地分解为一个球应力部分（来自 $\psi_{\text{vol}}$）和一个偏应力部分（来自 $\psi_{\text{iso}}$），后者是无迹的，即 $\operatorname{tr}(\boldsymbol{\tau}_{\text{iso}}) = 0$ [@problem_id:3440452]。

#### 有限应变弹塑性

与超弹性材料不同，金属等材料在加载超过一定限度后会发生不可逆的**塑性变形**，并伴随能量耗散。描述这类行为的模型要复杂得多。一个标准框架是基于**变形梯度的乘法分解**：

$\mathbf{F} = \mathbf{F}^e \mathbf{F}^p$

这个分解假设总变形可以被概念性地分解为两步：首先是塑性变形 $\mathbf{F}^p$，它改变材料的微观结构并导致永久变形，将物质点从参考构型映射到一个假想的**中间构型**；然后是弹性变形 $\mathbf{F}^e$，它从中间构型弹性地加载到最终的当前构型。对于金属，通常假设塑性变形是不可压缩的，即 $\det \mathbf{F}^p = 1$。

在这个框架下，亥姆霍兹自由能 $\psi$ 被认为是弹性变形 $\mathbf{F}^e$ 和描述硬化状态的内变量的函数。热力学第二定律（耗散不等式）表明，塑性流动的驱动力（即与塑性变形速率共轭的应力）是**Mandel应力** $\boldsymbol{\tau} = \mathbf{C}_e \mathbf{S}_e$，其中 $\mathbf{C}_e$ 和 $\mathbf{S}_e$ 是定义在中间构型上的弹性的柯西-格林张量和第二PK应力。

塑性流动何时发生由一个**屈服函数** $f(\boldsymbol{\tau}, \kappa) \le 0$ 决定，其中 $\kappa$ 是硬化变量。对于压强不敏感的金属，屈服函数通常只依赖于Mandel应力的偏量部分 $\text{dev}\,\boldsymbol{\tau}$。一个典型的例子是von Mises屈服准则。塑性流动的方向由**流动法则**给出，在关联塑性中，塑性应变率的方向垂直于屈服面：

$\mathbf{D}_p = \dot{\gamma} \frac{\partial f}{\partial \boldsymbol{\tau}}$

其中 $\mathbf{D}_p$ 是塑性变形速率张量，$\dot{\gamma}$ 是塑性乘子。由于屈服函数只依赖于偏应力，这个流动法则自然保证了 $\text{tr}(\mathbf{D}_p) = 0$，从而满足了塑性不可压缩性条件 [@problem_id:3440455]。

#### 广义连续介质模型：相场方法

经典连续介质模型在描述具有内部结构（如相界面、裂纹、位错）的材料时会遇到困难。**广义连续介质模型**通过引入额外的场变量来克服这些限制。**相场模型（phase-field models）**是一个突出的例子，它引入一个或多个连续的**内部变量**（或称序参量） $\alpha(\mathbf{x}, t)$ 来描述微观结构的状态，例如，$\alpha=0$ 代表一个相，$\alpha=1$ 代表另一个相，而 $0  \alpha  1$ 的区域则代表两相之间的弥散界面。

为了描述界面本身所存储的能量，自由能函数不仅依赖于序参量 $\alpha$，还依赖于它的梯度 $\nabla \alpha$：

$\psi(\alpha, \nabla \alpha) = \psi_0(\alpha) + \frac{\kappa}{2}|\nabla \alpha|^2$

这里的 $\psi_0(\alpha)$ 是局部自由能（通常是一个双阱势，其极小值对应于稳定相），而梯度项 $\frac{\kappa}{2}|\nabla \alpha|^2$ 则惩罚了序参量的剧烈空间变化，代表了**界面能**。

与序参量的演化相对应，需要引入广义的力。我们公设一个**微力平衡（microforce balance）**方程：$\pi - \nabla \cdot \boldsymbol{\xi} = 0$。这里，$\boldsymbol{\xi}$ 是与梯度 $\nabla\alpha$ 共轭的矢量微力（或称微应力），而 $\pi$ 是与 $\alpha$ 变化率 $\dot{\alpha}$ 共轭的标量内力。通过热力学[一致性分析](@entry_id:189411)（Coleman-Noll程序），可以确定这些力的保守部分（即能量部分）为：

$\boldsymbol{\xi} = \frac{\partial \psi}{\partial (\nabla \alpha)} = \kappa \nabla \alpha$
$\pi^{\text{cons}} = \frac{\partial \psi}{\partial \alpha} = \frac{d\psi_0}{d\alpha}$

在平衡状态下，耗散力为零，微力平衡方程就变成一个关于 $\alpha$ 的偏微分方程，即**艾伦-凯恩（Allen-Cahn）方程** [@problem_id:3440441]：

$\frac{d\psi_0}{d\alpha} - \kappa \Delta \alpha = 0$

这个方程描述了在没有外部驱动力时，系统如何通过演化其内部结构来最小化总自由能。

### 从理论到计算：变分原理与均匀化

#### 虚功原理

上述本构模型最终都表现为一组偏微分方程（强形式），例如静态平衡方程 $\text{Div}\,\mathbf{P} + \rho\mathbf{b} = \mathbf{0}$。直接求解这些方程通常很困难。**虚功原理（principle of virtual work）**为数值求解（如有限元方法, FEM）提供了基础。它将偏微分方程重新表述为一个积分形式的**弱形式（weak form）**。

其思想是对平衡方程乘以一个任意的、满足位移边界条件的**虚位移（virtual displacement）** $\delta\mathbf{u}$，然后在整个求解域 $\Omega$ 上积分。通过分部积分（格林公式），可以将应力项的导数转移到虚位移上，从而降低对解的光滑性要求，并自然地引入力边界条件。对于静态平衡问题，虚功原理表明，对于任何容许的虚位移，内力所做的虚功等于外力所做的虚功 [@problem_id:3440432]：

$\underbrace{\int_{\Omega} \mathbf{P} : \nabla \delta \mathbf{u} \, d\Omega}_{\delta W_{\text{int}}} = \underbrace{\int_{\Omega} \rho \mathbf{b} \cdot \delta \mathbf{u} \, d\Omega + \int_{\partial \Omega_t} \bar{\mathbf{t}} \cdot \delta \mathbf{u} \, dS}_{\delta W_{\text{ext}}}$

这个积分方程是有限元法的出发点，它将一个连续介质力学问题转化为了一个（通常是）非线性的代数方程组。

#### 计算均匀化

对于具有复杂微观结构的材料，直接对其宏观部件进行包含所有微观细节的建模在计算上是不可行的。**计算均匀化**方法提供了一个多尺度框架来解决此问题。其核心思想是在宏观模型的每个积分点上，求解一个RVE的边界值问题来计算该点的有效（或称均匀化）应力和本构响应。

这个多尺度连接的关键是能量的一致性，由**希尔-曼德尔（Hill-Mandel）条件**保证。该条件要求RVE尺度上微观应力和应变率功率的体积平均值等于宏观尺度上宏观应力和应变率的功率：

$\langle \boldsymbol{\sigma} : \dot{\boldsymbol{\epsilon}} \rangle = \boldsymbol{\Sigma} : \dot{\mathbf{E}}$

其中 $\langle \cdot \rangle$ 表示在RVE上的体积平均，小写字母代表微观量，大写字母代表宏观量。为了在RVE的计算中满足这个条件，需要施加特定的边界条件。最常见的三种包括 [@problem_id:3440466]：

1.  **运动学均匀边界条件（KUBC）**：在RVE边界上施加与宏观应变 $\mathbf{E}$ 一致的线性位移，即 $\mathbf{u} = \mathbf{E}\mathbf{x}$。
2.  **静态均匀边界条件（SUBC）**：在RVE边界上施加与宏观应力 $\boldsymbol{\Sigma}$ 一致的面力，即 $\mathbf{t} = \boldsymbol{\Sigma}\mathbf{n}$。
3.  **周期性边界条件（PBC）**：要求位移场为宏观线性位移与一个周期性涨落之和，同时面力在RVE相对的面上呈反周期分布。

这些边界条件模拟了RVE嵌入在一个经受均匀宏观变形的无限大介质中的不同理想情况，从而使得从微观计算得到的有效宏观响应在能量上是自洽的。