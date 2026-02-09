## 引言
材料在承受外部载荷时，其内部微观结构会发生不可逆的演化，最终导致性能退化甚至宏观断裂。如何在一个连续介质的框架内，精确描述这一从弥散性微观损伤到最终宏观失效的完整过程，是固体力学领域的核心挑战。连续介质损伤力学（Continuum Damage Mechanics, CDM）应运而生，它通过引入内部状态变量来唯象地表征材料性能的退化，从而在微观缺陷的物理现实与宏观结构的力学响应之间架起了一座坚实的桥梁。

本文旨在系统性地介绍连续介质损伤力学的理论基础、高级应用与实践方法。我们将从最基本的概念出发，逐步深入到理论的前沿与工程实践的核心。
- 在“**原理与机制**”一章中，您将学习CDM的数学框架，从损伤变量的定义出发，构建严格的热力学一致性本构关系，区分损伤与塑性，并探讨解决数值计算中病态问题的非局部理论。
- 随后的“**应用与跨学科交叉**”一章将展示CDM的强大生命力，通过一系列案例，您将看到该理论如何用于表征材料行为、解释疲劳与断裂现象、为复合材料等复杂材料建模，并与多物理场问题和生物力学等领域交叉融合。
- 最后，在“**动手实践**”部分，我们精选了若干典型问题，引导您亲手推导和分析损伤力学中的关键模型与概念，将理论知识转化为解决实际问题的能力。

通过本次学习，您将对连续介质损伤力学形成一个全面而深刻的理解，为您的学术研究和工程应用奠定坚实的基础。

## 原理与机制

在对连续介质损伤力学（Continuum Damage Mechanics, CDM）有了初步了解之后，本章将深入探讨其核心的物理原理与数学框架。我们将从损伤的宏观唯象定义出发，建立一个严格的热力学一致性框架，并由此导出描述材料行为的本构关系。随后，我们将探讨如何区分损伤与其他非弹性现象，并介绍损伤演化的数学表述。最后，我们将讨论更高级的本构模型，以捕捉真实材料中观察到的复杂行为，并解决在数值模拟中出现的关键问题。

### 损伤的宏观表征与状态变量

从工程角度看，材料损伤是指在外部载荷作用下，材料内部产生并逐渐累积微观缺陷（如微裂纹、微孔洞）的过程。这些缺陷虽然在微观尺度上是不连续的，但当其弥散分布于宏观体积单元内时，它们的集体效应表现为材料宏觀力学性能的退化，例如刚度和强度的降低。

CDM的核心思想在于，通过引入一个或多个连续的内部状态变量来描述这种由微观缺陷引起的宏观性能退化，而无需精确追踪每一个微观缺陷的几何形态和演化。最简单的模型是**各向同性标量损伤模型**，它引入一个标量损伤变量 $D$。该变量通常被定义在区间 $[0, 1]$ 内，其中 $D=0$ 代表材料处于无损的原始状态，而 $D=1$ 则代表材料完全丧失承载能力，即宏观尺度上的断裂。

损伤变量 $D$ 的一个直观物理解释是**有效承载面积的损失分数** [@problem_id:2873734]。考虑一个初始横截面积为 $A_0$ 的杆件，在损伤状态下，由于微孔洞和微裂纹的存在，实际能够传递载荷的面积减小为有效面积 $\tilde{A}$。损伤变量 $D$ 定义了这两者之间的关系：
$$
\tilde{A} = (1 - D) A_0
$$
相应地，作用在杆件上的轴向力 $F$ 产生了两种不同的应力度量：其一是基于初始面积的名义应力（或工程应力）$\sigma_n = F/A_0$，其二是作用在实际承载部分（即材料“骨架”）上的有效应力 $\tilde{\sigma} = F/\tilde{A}$。将上述关系联立，我们得到有效应力与名义应力之间的关键联系：
$$
\tilde{\sigma} = \frac{F}{(1-D)A_0} = \frac{\sigma_n}{1-D}
$$
这个关系是构建损伤本构模型的重要基石，它将宏观可测量的名义应力与驱动材料微观变形和破坏的有效应力联系起来。

### 连续介质损伤力学的热力学框架

为了确保损伤模型具有坚实的物理基础并满足能量守恒和耗散定律，我们必须在不可逆过程热力学的框架内构建它。该框架以亥姆霍兹自由能（Helmholtz free energy）为核心，通过热力学第二定律（以Clausius–Duhem不等式形式表达）对本构关系施加约束。

#### 亥姆霍兹自由能与本构关系

在等温、小应变条件下，材料的局部状态由应变张量 $\boldsymbol{\varepsilon}$ 和损伤变量 $D$ 共同确定。我们假设存在一个亥姆霍兹自由能密度函数 $\psi(\boldsymbol{\varepsilon}, D)$，它存储了与弹性变形和材料损伤状态相关的能量。

一个被广泛接受并与有效面积概念相符的假设是**应变等效性原理**（Hypothesis of Strain Equivalence）。该原理指出，受损材料在给定应变下的本构响应形式上与未受损材料在某个有效应力下的响应相同。这引导我们构建如下形式的自由能密度 [@problem_id:2548732]：
$$
\psi(\boldsymbol{\varepsilon}, D) = (1 - D) \psi_0(\boldsymbol{\varepsilon})
$$
其中，$\psi_0(\boldsymbol{\varepsilon})$ 是材料在无损状态（$D=0$）下的弹性应变能密度，对于线性弹性材料，其形式为 $\psi_0(\boldsymbol{\varepsilon}) = \frac{1}{2}\boldsymbol{\varepsilon} : \mathbb{C}_0 : \boldsymbol{\varepsilon}$，$\mathbb{C}_0$ 是初始的、正定的四阶弹性张量。这种形式的自由能直观地表示，损伤的出现使得能够存储弹性应变能的材料体积比例减少了 $D$。

在等温过程中，Clausius–Duhem不等式要求内禀耗散率 $\mathcal{D}$ 必须非负：
$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi}(\boldsymbol{\varepsilon}, D) \ge 0
$$
这里，$\boldsymbol{\sigma}$ 是柯西应力张量，$(\dot{\cdot})$ 代表材料时间导数。利用链式法则展开 $\dot{\psi}$：
$$
\dot{\psi} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} : \dot{\boldsymbol{\varepsilon}} + \frac{\partial \psi}{\partial D} \dot{D}
$$
代入耗散不等式并整理，得到：
$$
\left( \boldsymbol{\sigma} - \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} \right) : \dot{\boldsymbol{\varepsilon}} - \frac{\partial \psi}{\partial D} \dot{D} \ge 0
$$
根据Coleman-Noll方法，为保证不等式对任意可能的加载过程（即任意 $\dot{\boldsymbol{\varepsilon}}$）均成立，必须要求 $\dot{\boldsymbol{\varepsilon}}$ 的系数为零。这给出了应力的状态方程：
$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}
$$
将我们选择的自由能形式 $\psi = (1-D)\psi_0$ 代入，即可得到受损材料的应力-应变关系：
$$
\boldsymbol{\sigma} = \frac{\partial}{\partial \boldsymbol{\varepsilon}} \left[ (1-D) \frac{1}{2}\boldsymbol{\varepsilon} : \mathbb{C}_0 : \boldsymbol{\varepsilon} \right] = (1-D) \mathbb{C}_0 : \boldsymbol{\varepsilon}
$$
此式表明，损伤变量 $D$ 的作用是等效地将材料的弹性刚度张量从 $\mathbb{C}_0$ 降低为有效刚度 $\mathbb{C}(D) = (1-D)\mathbb{C}_0$。

#### 损伤能量释放率

在导出应力本构关系后，耗散不等式简化为：
$$
\mathcal{D} = - \frac{\partial \psi}{\partial D} \dot{D} \ge 0
$$
我们定义一个与损伤变量 $D$ 共轭的热力学力，记为 $Y$，称为**损伤能量释放率**（damage energy release rate）：
$$
Y = - \frac{\partial \psi}{\partial D}
$$
$Y$ 的物理意义是在应变 $\boldsymbol{\varepsilon}$ 保持不变的条件下，自由能密度随损伤增加而减少的速率。这部分被“释放”的能量将用于驱动材料内部微观结构的演化，即损伤的扩展。

对于我们选择的自由能形式，损伤能量释放率 $Y$ 的表达式为 [@problem_id:2548732] [@problem_id:2873713]：
$$
Y = - \frac{\partial}{\partial D} \left[ (1-D) \psi_0(\boldsymbol{\varepsilon}) \right] = \psi_0(\boldsymbol{\varepsilon}) = \frac{1}{2}\boldsymbol{\varepsilon} : \mathbb{C}_0 : \boldsymbol{\varepsilon}
$$
可见，$Y$ 正是无损材料在该应变状态下所存储的弹性应变能密度。由于 $\mathbb{C}_0$ 是正定的，所以 $Y \ge 0$。

现在，耗散不等式可以写成一个简洁的乘积形式：
$$
\mathcal{D} = Y \dot{D} \ge 0
$$
考虑到 $Y \ge 0$，为了保证耗散非负，必须有 $\dot{D} \ge 0$。这从热力学第二定律的高度确立了损伤过程的**不可逆性**：损伤一旦发生，便无法自发“愈合”，只能增加或保持不变。

### 损伤与塑性的区分

材料的非弹性行为不仅包括损伤，还包括塑性。在宏观唯象理论中，这两者都通过内部状态变量来描述，但它们的物理本质和宏观表现截然不同 [@problem_id:2873734]。

- **损伤（Damage, $D$）** 是一种**刚度退化**现象。其核心物理表现是材料弹性模量的降低。在一个加载-卸载-再加载的循环测试中，损伤的累积会使得卸载和再加载路径的斜率（即切线模量）变小。如前所述，有效模量 $E_{eff} = (1-D)E_0$。这一效应也可以通过测量材料中的弹性波速来探测，因为波速 $c$ 与模量和密度 $\rho$ 相关（例如，对于细杆中的纵波，$c = \sqrt{E_{eff}/\rho}$）。因此，随着损伤 $D$ 的增加，波速会显著下降。

- **塑性（Plasticity, $\varepsilon^p$）** 是一种**不可逆变形**现象。它通过引入塑性应变 $\varepsilon^p$ 这一运动学内部变量来描述。在小应变框架下，总应变可以分解为弹性部分和塑性部分，即 $\varepsilon = \varepsilon^e + \varepsilon^p$。塑性的标志性特征是，当外加载荷完全卸除至零时，材料会留下永久的残余应变，其大小即为 $\varepsilon^p$。然而，在纯塑性模型中（即 $D=0$），卸载和再加载的弹性斜率保持不变，始终等于初始的杨氏模量 $E_0$。

总结来说，在一次力学测试中：
- 如果卸载后材料回到原点但卸载路径的斜率降低了，这表明发生了纯损伤。
- 如果卸载后材料未回到原点（有残余应变）但卸载路径的斜率与初始加载时相同，这表明发生了纯塑性。
- 如果卸载路径的斜率降低且存在残余应变，则表明损伤和塑性同时发生。

这两者在热力学框架中的角色也不同。损伤变量 $D$ 主要影响亥姆霍兹自由能中与刚度相关的系数，而塑性应变 $\varepsilon^p$ 则作为一种不可逆的运动学量，从总应变中“扣除”，以确定弹性应变的大小。

### 损伤演化：起始准则与演化律

热力学框架虽然给出了损伤演化的驱动力 $Y$ 和不可逆性约束 $\dot{D} \ge 0$，但并未指明损伤具体在何时开始以及如何随加载而增长。这需要额外的**本构规定**，即定义损伤的**起始准则**和**演化律**。这套规则在形式上与塑性力学中的屈服准则和流动法则高度相似 [@problem_id:2624868] [@problem_id:2548746]。

1.  **损伤起始准则（Damage Initiation Criterion）**：
    我们定义一个损伤加载函数 $f$，它通常是损伤能量释放率 $Y$ 和一个或多个历史变量（如损伤阈值 $\kappa$）的函数。损伤起始准则规定，只要 $f(Y, \kappa)  0$，材料就处于弹性（或非损伤演化）状态。损伤的演化只可能在 $f(Y, \kappa) = 0$ 时发生。一个常见的简单形式是：
    $$
    f(Y, \kappa) = Y - \kappa \le 0
    $$
    其中，历史变量 $\kappa$ 记录了材料经历过的最大损伤驱动力水平。初始时，$\kappa = \kappa_0$，$\kappa_0$ 是材料的初始损伤阈值。

2.  **损伤演化律（Damage Evolution Law）**：
    当损伤准则被满足（$f=0$）且加载持续（$\dot{f}=0$，一致性条件）时，损伤变量 $D$ 便开始增长。对于率无关模型，损伤的增长率 $\dot{D}$ 通常由一个流动法则给出，例如 $\dot{D} = \dot{\lambda}$，其中 $\dot{\lambda}$ 是非负的一致性参数（或损伤乘子）。

这一整套加载-卸载条件可以用Kuhn-Tucker互补条件精炼地表述为：
$$
f(Y, \kappa) \le 0, \quad \dot{\lambda} \ge 0, \quad \dot{\lambda} f(Y, \kappa) = 0
$$
这组条件完美地描述了损伤演化的“开关”机制：
- 当 $f  0$ 时（弹性状态），必须有 $\dot{\lambda}=0$，因此 $\dot{D}=0$，损伤不增长。
- 当 $f = 0$ 时（损伤临界状态），允许 $\dot{\lambda} \ge 0$。如果继续加载使得 $Y$ 有增大的趋势，则 $\dot{\lambda}>0$，导致 $\dot{D}>0$，损伤增长；如果卸载使得 $Y$ 减小，则 $\dot{\lambda}=0$，损伤保持不变。

### 高级损伤本构模型

基础的各向同性标量损伤模型在许多应用中非常有效，但真实材料的行为往往更为复杂。下面介绍几种重要的模型扩展。

#### 各向异性损伤

许多材料（如复合材料、或经受过特定方向拉伸的金属）的损伤是具有方向性的。例如，沿一个方向排列的微裂纹会主要削弱该方向的刚度，而对垂直方向的刚度影响较小。这种情况下，单一的标量损伤变量 $D$ 无法描述刚度退化的方向依赖性 [@problem_id:2873730]。

为了捕捉各向异性损伤，需要引入更高阶的损伤变量。一个最小的扩展是使用一个**二阶对称张量** $\mathbf{D}$。该张量的特征值可以表示沿其对应特征向量（主损伤方向）的损伤程度。例如，对于正交损伤，$\mathbf{D}$ 在其主轴坐标系下可以写为对角矩阵 $\mathrm{diag}(D_1, D_2, D_3)$，其中 $D_i$ 分别是三个主方向上的损伤值。

将张量型损伤变量引入热力学框架有多种方式。一种常见方法是通过一个映射关系，将应变张量 $\boldsymbol{\varepsilon}$ 映射到一个有效应变张量 $\tilde{\boldsymbol{\varepsilon}}$，然后用 $\tilde{\boldsymbol{\varepsilon}}$ 来计算应力。例如，可以定义一个完整性张量 $\mathbf{M} = \mathbf{I} - \mathbf{D}$（其中 $\mathbf{I}$ 是单位张量），并构建有效应变 $\tilde{\boldsymbol{\varepsilon}} = \mathbf{M}^{-1/2} \boldsymbol{\varepsilon} \mathbf{M}^{-1/2}$，再将自由能写为 $\psi = \frac{1}{2}\tilde{\boldsymbol{\varepsilon}} : \mathbb{C}_0 : \tilde{\boldsymbol{\varepsilon}}$。这样的构造能够保证应力张量的对称性以及热力学一致性。

#### 单边效应：拉压异性

对于混凝土、岩石、陶瓷等准脆性材料，损伤行为在拉伸和压缩下表现出显著差异，这种现象被称为**单边效应**（Unilateral Effect）[@problem_id:2624839]。在拉伸载荷下，微裂纹张开，导致材料刚度显著下降。然而，当载荷转为压缩时，之前张开的裂纹会闭合，裂纹面之间可以传递压应力，使得材料的刚度在一定程度上恢复。

为了模拟这种行为，需要对本构模型进行修正，使其能够区分拉伸和压缩状态。一种有效的方法是对**应变张量进行谱分解**。首先计算应变张量 $\boldsymbol{\varepsilon}$ 的主应变 $\varepsilon_i$ 和主方向 $\mathbf{n}_i$。然后，将 $\boldsymbol{\varepsilon}$ 分解为拉伸部分 $\boldsymbol{\varepsilon}^+$ 和压缩部分 $\boldsymbol{\varepsilon}^-$：
$$
\boldsymbol{\varepsilon}^+ = \sum_i \langle \varepsilon_i \rangle_+ \mathbf{n}_i \otimes \mathbf{n}_i \quad ; \quad \boldsymbol{\varepsilon}^- = \sum_i \langle \varepsilon_i \rangle_- \mathbf{n}_i \otimes \mathbf{n}_i
$$
其中 $\langle x \rangle_+ = \max(x, 0)$ 和 $\langle x \rangle_- = \min(x, 0)$ 是Macaulay括号。

随后，在构建自由能时，只让损伤变量 $D$ 作用于与拉伸应变相关的能量项。例如，应力可以定义为：
$$
\boldsymbol{\sigma} = (1-D)(\mathbb{C}_0:\boldsymbol{\varepsilon}^+) + \mathbb{C}_0:\boldsymbol{\varepsilon}^-
$$
这样，只有拉伸部分的应力贡献会因损伤而退化，而压缩部分的响应则不受影响。同时，损伤的演化也应只由拉伸应变驱动，例如，可以将损伤能量释放率 $Y$ 定义为仅与 $\boldsymbol{\varepsilon}^+$ 相关的能量。

#### 应变等效与有效应力：对偶视角

我们之前基于“应变等效性”原理构建了自由能 $\psi(\boldsymbol{\varepsilon}, D) = (1-D)\psi_0(\boldsymbol{\varepsilon})$。在热力学中，还存在一个与之对偶的框架，即使用吉布斯自由能（或互补自由能）$\phi(\boldsymbol{\sigma}, D)$ 作为势函数。基于“有效应力”概念，可以构建另一种形式的损伤模型 [@problem_id:2548735]。

有效应力模型假设，受损材料在名义应力 $\boldsymbol{\sigma}$ 下的应变，等同于无损材料在有效应力 $\tilde{\boldsymbol{\sigma}} = \boldsymbol{\sigma}/(1-D)$ 下的应变。这可以通过构造互补自由能来实现：
$$
\phi(\boldsymbol{\sigma}, D) = \frac{1}{1-D} \phi_0(\boldsymbol{\sigma})
$$
其中 $\phi_0(\boldsymbol{\sigma}) = \frac{1}{2}\boldsymbol{\sigma}:\mathbb{C}_0^{-1}:\boldsymbol{\sigma}$ 是无损材料的互补能。从该势函数出发，可以导出应变 $\boldsymbol{\varepsilon} = \partial\phi/\partial\boldsymbol{\sigma} = \frac{1}{1-D}\mathbb{C}_0^{-1}:\boldsymbol{\sigma}$。整理后可得 $\boldsymbol{\sigma} = (1-D)\mathbb{C}_0:\boldsymbol{\varepsilon}$。

有趣的是，这与从应变等效原理导出的应力-应变关系完全相同。事实上，这两种方法是完全等价的。通过勒让德变换（Legendre Transform）可以证明，上述的亥姆霍兹自由能 $\psi(\boldsymbol{\varepsilon}, D)$ 和互补自由能 $\phi(\boldsymbol{\sigma}, D)$ 互为对偶势，它们描述的是同一个物理模型，只是分别从应变控制和应力控制的视角出发。它们各自导出的损伤能量释放率 $Y = -\partial\psi/\partial D$ 和 $X = \partial\phi/\partial D$ 也是等价的。

### 局部化、病态网格依赖性与正则化

在将CDM模型应用于有限元分析（FEM）等数值方法时，会出现一个严重的问题，尤其是在材料表现出**软化**行为（即应力随应变增加而下降）时。

#### 局部软化模型的网格依赖性问题

考虑一个受拉伸的杆件，其材料本构关系包含一个软化阶段。当杆件某处的应变达到峰值应力点后，损伤开始累积，应力下降。数值计算表明，这种软化变形会自发地**局部化**（localize）到一个极小的区域内，而该区域之外的材料则弹性卸载。对于标准的局部CDM模型，这个局部化区域的宽度会随着有限元网格的加密而无限缩小，最终趋向于一个数学上的面 [@problem_id:2873748]。

这导致了**病态的网格依赖性**：
1.  **能量耗散问题**：断裂一个结构所需的总能量是一个物理量，理应与数值计算的网格无关。然而，在局部软化模型中，总的耗散能被计算为耗散能密度与发生软化的体积的乘积。由于软化体积随着网格尺寸 $h$ 的减小而趋于零（$V \propto h$），导致总耗散能也趋于零。这意味着，只要网格足够密，模拟出的结构断裂几乎不需要任何能量，这显然是错误的。
2.  **结果的非客观性**：模拟得到的力-位移曲线、断裂模式等结果都将严重依赖于所使用的网格尺寸和划分方式，使得预测失去客观性。

#### 非局部损伤模型引论

为了解决局部模型的病态网格依赖性，必须引入一个**内禀长度尺度**（internal length scale），以防止损伤无限地局部化。**非局部损伤模型**正是为此目的而提出的正则化方法 [@problem_id:2624861]。

其核心思想是，一个点 $\mathbf{x}$ 的损伤状态不应仅仅由该点自身的应变决定，而应由其邻域内应变的某种加权平均值来驱动。最常见的非局部模型是积分型模型，它引入一个非局部等效应变 $\bar{\varepsilon}(\mathbf{x})$：
$$
\bar{\varepsilon}(\mathbf{x}) = \int_{\Omega} w(\mathbf{x}, \mathbf{y}) \tilde{\varepsilon}(\mathbf{y}) dV_y
$$
其中，$\tilde{\varepsilon}(\mathbf{y})$ 是点 $\mathbf{y}$ 的局部等效应变（例如von Mises等效应变），$w(\mathbf{x}, \mathbf{y})$ 是一个权重函数（或核函数），它在点 $\mathbf{x}$ 周围的一个有限邻域内取非零值。该邻域的大小由模型的内禀长度尺度决定。损伤演化律中的驱动力 $Y$ 不再是局部应变的函数，而是这个非局部量 $\bar{\varepsilon}(\mathbf{x})$ 的函数。

通过空间平均，非局部模型有效地将应变“涂抹”开，使得损伤演化发生在一个具有有限宽度的带（称为过程区）内，其宽度与内禀长度尺度相关，从而不再受网格尺寸的控制。

在实际应用非局部模型时，需要特别注意边界效应。对于有界域，当点 $\mathbf{x}$ 靠近边界时，其积分邻域会被截断。为了保证即使在边界附近，一个均匀的局部应变场也能产生一个均匀的非局部场（即“常数再现”性质），通常需要对权重函数进行归一化处理：
$$
\bar{\varepsilon}(\mathbf{x}) = \frac{\int_{\Omega} \alpha(\|\mathbf{x}-\mathbf{y}\|) \tilde{\varepsilon}(\mathbf{y}) dV_y}{\int_{\Omega} \alpha(\|\mathbf{x}-\mathbf{y}\|) dV_y}
$$
其中 $\alpha$ 是一个径向对称的核函数。这种归一化确保了模型的响应在边界附近不会出现非物理的“偏软”或“偏硬”现象。对于周期性边界条件，由于积分可以无缝地“环绕”，边界效应自然消失，通常无需显式归一化。

通过引入非局部相互作用，CDM不仅解决了网格依赖性问题，也使其能够更真实地模拟材料内部的协作性破坏过程。