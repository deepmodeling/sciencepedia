## 引言
[线性弹性](@entry_id:166983)理论是固体力学的基石，它以简洁的数学形式描述了材料在小变形下的力学响应，是理解和预测从宏伟桥梁到微观[晶格](@entry_id:148274)等各类结构行为的基础。胡克定律作为其核心本构关系，虽然形式简单，却蕴含着深刻的物理内涵，并成为连接理论与工程实践的关键桥梁。然而，要真正掌握这一理论，不仅需要理解其基本方程，更要洞悉其背后的[热力学原理](@entry_id:142232)、[材料对称性](@entry_id:190289)约束、数值实现的挑战及其在广阔的跨学科领域中的应用。

本文旨在为读者提供一个从基本原理到前沿应用的系统性学习路径。文章将首先在“**原理与机制**”一章中，严谨地构建[线性弹性](@entry_id:166983)理论的数学框架。我们将从变形与应变的精确度量出发，引入应力的概念，并基于热力学原理推导出连接二者的[广义胡克定律](@entry_id:203555)，同时深入探讨[材料对称性](@entry_id:190289)与数值计算中的关键问题。随后，在“**应用与跨学科联系**”一章中，我们将展示该理论的强大威力，通过一系列涵盖工程力学、多物理场耦合、[微观力学](@entry_id:195009)乃至生物力学的案例，揭示其在解决真实世界问题中的普适性。最后，通过一系列“**动手实践**”练习，读者将有机会亲手应用所学知识，将抽象的理论转化为具体的计算与分析能力，从而真正巩固对[线性弹性](@entry_id:166983)与胡克定律的深刻理解。

## 原理与机制

本章旨在系统性地阐述[线性弹性力学](@entry_id:166983)的基本原理与核心机制。我们将从变形与应变的精确描述出发，过渡到物体内部作用力的度量——应力，并在此基础上建立联系二者的[本构关系](@entry_id:186508)，即[广义胡克定律](@entry_id:203555)。本章将深入探讨[材料对称性](@entry_id:190289)如何影响[本构关系](@entry_id:186508)，并重点阐述[各向同性材料](@entry_id:170678)的特殊情况。最后，我们将讨论弹性力学边值问题的数学表述，及其在[数值模拟](@entry_id:146043)中面临的挑战与解决方案，为后续[多尺度分析](@entry_id:1128330)奠定坚实的理论基础。

### 变形与应变的度量

描述一个连续体的运动，即是描述其如何从一个**参考构型**（初始构型）映射到**当前构型**（变形后构型）。在参考构型中，物质点的坐标用 $\mathbf{X}$ 表示；在当前构型中，其坐标为 $\mathbf{x}$。运动可以表示为映射 $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X})$。物[质点](@entry_id:186768)的**位移向量**定义为 $\mathbf{u}(\mathbf{X}) = \mathbf{x} - \mathbf{X}$。

描述局部变形的关键物理量是**变形梯度**张量 $\mathbf{F}$，其定义为当前构型坐标相对于参考构型坐标的梯度：
$$
\mathbf{F} = \nabla_{\mathbf{X}} \boldsymbol{\varphi}(\mathbf{X}) = \mathbf{I} + \nabla \mathbf{u}
$$
其中 $\mathbf{I}$ 是二阶单位张量。$\mathbf{F}$ 包含了关于局部拉伸、剪切和旋转的全部信息。

#### 有限应变与微小应变

为了只度量变形（拉伸与剪切）而排除[刚体转动](@entry_id:191086)的影响，我们需要构建一个客观的（即与观察者坐标系无关的）[应变度量](@entry_id:755495)。在有限变形理论中，一个常用的度量是**[格林-拉格朗日应变张量](@entry_id:187745)**（Green-Lagrange strain tensor）$\mathbf{E}$：
$$
\mathbf{E} = \frac{1}{2}(\mathbf{F}^{\top}\mathbf{F} - \mathbf{I})
$$
$\mathbf{E}$ 的一个重要特性是其**标架无关性**（frame-indifference）。对于一个纯[刚体转动](@entry_id:191086)，变形梯度 $\mathbf{F}$ 是一个正交[旋转张量](@entry_id:191990) $\mathbf{R}$（满足 $\mathbf{R}^{\top}\mathbf{R} = \mathbf{I}$）。在这种情况下，$\mathbf{E} = \frac{1}{2}(\mathbf{R}^{\top}\mathbf{R} - \mathbf{I}) = \mathbf{0}$。这表明 $\mathbf{E}$ 能精确地滤除任意大小的[刚体转动](@entry_id:191086)，只反映真实的变形。

在许多工程应用中，变形非常微小。这构成了**小变形假设**（small-deformation assumption）的基础，其数学表述为[位移梯度张量](@entry_id:748571) $\nabla \mathbf{u}$ 的范数远小于1，即 $\lVert \nabla \mathbf{u} \rVert \ll 1$。这个假设意味着物体的拉伸、剪切和转动都非常小。在此假设下，我们可以对[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E}$ 进行线性化。将 $\mathbf{F} = \mathbf{I} + \nabla \mathbf{u}$ 代入 $\mathbf{E}$ 的定义中：
$$
\mathbf{E} = \frac{1}{2}((\mathbf{I} + \nabla \mathbf{u})^{\top}(\mathbf{I} + \nabla \mathbf{u}) - \mathbf{I}) = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^{\top} + (\nabla \mathbf{u})^{\top}\nabla \mathbf{u})
$$
由于 $\lVert \nabla \mathbf{u} \rVert \ll 1$，二次项 $(\nabla \mathbf{u})^{\top}\nabla \mathbf{u}$ 是一个高阶小量，可以忽略。这就引出了**[无穷小应变张量](@entry_id:167211)**（infinitesimal strain tensor）$\boldsymbol{\varepsilon}$ 的定义：
$$
\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^{\top})
$$
[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon}$ 是[位移梯度](@entry_id:165352) $\nabla \mathbf{u}$ 的对称部分。在小变形假设下，我们有 $\mathbf{E} \approx \boldsymbol{\varepsilon}$ 。值得注意的是，$\boldsymbol{\varepsilon}$ 并非严格的标架无关。对于一个微小转动，其应变近似为零，但对于有限转动，它会产生虚假的应变。然而，在[线性弹性](@entry_id:166983)理论的[适用范围](@entry_id:636189)内（即小变形），这种近似客观性是完全可以接受的 。

### 内部作用力的度量：应力

当连续体变形时，其内部产生相互作用力。为了描述这些分布力，我们引入**应力**的概念。在当前构型中，通过一个假想的[截面](@entry_id:154995)将物体切开，[截面](@entry_id:154995)法向为 $\mathbf{n}$。[截面](@entry_id:154995)一侧对另一侧的作用力分布密度（单位当前面积上的力）称为**牵[引力](@entry_id:189550)向量**（traction vector）$\mathbf{t}$。根据**柯西应力定理**（Cauchy's stress theorem），牵[引力](@entry_id:189550)向量与法向向量之间存在线性关系，该关系由**柯西[应力张量](@entry_id:148973)**（Cauchy stress tensor）$\boldsymbol{\sigma}$ 定义：
$$
\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}
$$
柯西应力张量 $\boldsymbol{\sigma}$ 是一个[二阶张量](@entry_id:199780)，描述了物体内部某一点在所有方向上的应力状态。在没有[体力](@entry_id:174230)矩和耦合应力的经典连续[体力](@entry_id:174230)学中，动量矩平衡定律要求柯西[应力张量](@entry_id:148973)必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\top}$。

#### 多种应力度量

柯西应力是定义在当前构型上的“真实”应力。在有限变形理论中，为了方便在固定的参考构型上进行计算，还引入了其他应力度量：
- **[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量**（First Piola-Kirchhoff stress, PK1）：记为 $\mathbf{P}$，它将当前构型中的力与参考构型中的[面积元](@entry_id:263205)联系起来。其与名义牵[引力](@entry_id:189550) $\mathbf{T}$（单位参考面积上的力）的关系是 $\mathbf{T} = \mathbf{P}\mathbf{N}$，其中 $\mathbf{N}$ 是参考构型中的法向。
- **[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量**（Second Piola-Kirchhoff stress, PK2）：记为 $\mathbf{S}$，它是一个在参考构型中定义的[对称张量](@entry_id:148092)，与 $\mathbf{P}$ 的关系是 $\mathbf{P} = \mathbf{F}\mathbf{S}$。

这些不同的应力度量通过变形梯度 $\mathbf{F}$ 相互关联。利用力元不变性（$\mathbf{t}\,da = \mathbf{T}\,dA$）和[面积元](@entry_id:263205)变换的**南松公式**（Nanson's relation, $\mathbf{n}\,da = J\,\mathbf{F}^{-\top}\mathbf{N}\,dA$，其中 $J=\det\mathbf{F}$），可以推导出柯西应力与PK1应力的关系 ：
$$
\mathbf{P} = J\,\boldsymbol{\sigma}\,\mathbf{F}^{-\top}
$$
进而在小应变极限下，当 $\lVert \nabla \mathbf{u} \rVert \ll 1$ 时，$\mathbf{F} \approx \mathbf{I}$ 且 $J \approx 1$。此时，三种应力度量趋于一致：$\boldsymbol{\sigma} \approx \mathbf{P} \approx \mathbf{S}$ 。这为[线性弹性](@entry_id:166983)理论提供了一个重要的简化：尽管理论是在参考构型上建立的，我们仍然可以统一使用柯西应力张量 $\boldsymbol{\sigma}$，而无需区分这些不同的度量。

在多尺度建模中，应力概念同样可以[跨尺度](@entry_id:754544)联系。**希尔-曼德尔宏观均匀性原理**（Hill-Mandel principle of macrohomogeneity）指出，宏观（均质化后）的柯西应力是微观柯西应[力场](@entry_id:147325)在代表性体积元（Representative Volume Element, RVE）上的体积平均 。

### [本构关系](@entry_id:186508)：[广义胡克定律](@entry_id:203555)

本构关系描述了材料的力学响应，即应力与应变之间的关系。对于弹性材料，这种关系是可逆的。

#### [热力学](@entry_id:172368)基础

[线性弹性](@entry_id:166983)[本构关系](@entry_id:186508)可以从连续介质[热力学](@entry_id:172368)的第一和第二定律推导得出。对于一个[等温过程](@entry_id:143096)，**克劳修斯-杜恩不等式**（Clausius-Duhem inequality）要求材料的内禀[耗散率](@entry_id:748577)必须非负。对于一个其状态仅由应变 $\boldsymbol{\varepsilon}$ 决定的弹性体，其[亥姆霍兹自由能](@entry_id:136442)密度为 $\psi = \psi(\boldsymbol{\varepsilon})$。[耗散不等式](@entry_id:188634)可以写作  ：
$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0
$$
将 $\dot{\psi} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} : \dot{\boldsymbol{\varepsilon}}$ 代入，得到：
$$
\left(\boldsymbol{\sigma} - \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}\right) : \dot{\boldsymbol{\varepsilon}} \ge 0
$$
由于此不等式必须对任意[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}$ 成立，括号中的项必须为零。这定义了**[超弹性材料](@entry_id:190241)**（hyperelastic material）：
$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}
$$
这意味着应力可以由一个[标量势](@entry_id:276177)函数（亥姆霍兹自由能）的导数得到，并且这种响应是无耗散的（$\mathcal{D}=0$）。

如果我们假设材料在零应变状态附近的行为是线性的，可以假定自由能密度是应变的二次函数：
$$
\psi(\boldsymbol{\varepsilon}) = \frac{1}{2}\boldsymbol{\varepsilon} : \mathbb{C} : \boldsymbol{\varepsilon}
$$
对其求导便得到了线性的[应力-应变关系](@entry_id:274093)，这便是**[广义胡克定律](@entry_id:203555)**（Generalized Hooke's Law）：
$$
\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}
$$
其中，$\mathbb{C}$ 是一个[四阶张量](@entry_id:181350)，称为**[弹性张量](@entry_id:170728)**或**[刚度张量](@entry_id:176588)**。

#### [弹性张量](@entry_id:170728) $\mathbb{C}$ 的性质

[弹性张量](@entry_id:170728) $\mathbb{C}_{ijkl}$ 的结构蕴含了丰富的物理信息。
- **次对称性**（Minor symmetries）：由于应力张量 $\boldsymbol{\sigma}$ 和[应变张量](@entry_id:1132487) $\boldsymbol{\varepsilon}$ 都是对称的，$\mathbb{C}$ 也具有相应的对称性：$\mathbb{C}_{ijkl} = \mathbb{C}_{jikl}$（源于 $\sigma_{ij}=\sigma_{ji}$）和 $\mathbb{C}_{ijkl} = \mathbb{C}_{ijlk}$（源于 $\varepsilon_{kl}=\varepsilon_{lk}$）。这些对称性是运动学和动量矩平衡的直接结果  。
- **主对称性**（Major symmetry）：如上所述，[超弹性](@entry_id:159356)假设（即存在[应变能势](@entry_id:755493)函数 $\psi$）是胡克定律的[热力学](@entry_id:172368)基础。根据[混合偏导数的对称性](@entry_id:146941)（[克莱罗定理](@entry_id:139814)），我们有 $\mathbb{C}_{ijkl} = \frac{\partial^2 \psi}{\partial\varepsilon_{ij}\partial\varepsilon_{kl}} = \frac{\partial^2 \psi}{\partial\varepsilon_{kl}\partial\varepsilon_{ij}} = \mathbb{C}_{klij}$。这就是主对称性   。
- **独立常数数量**：在三维空间中，一个没有任何对称性的[四阶张量](@entry_id:181350)有 $3^4 = 81$ 个分量。次对称性将独立分量数减少到 $36$ 个。主对称性进一步将此数目减少到 $21$ 个。因此，对于一个一般的各向异性线性[超弹性材料](@entry_id:190241)，其力学行为由 $21$ 个独立的[弹性常数](@entry_id:146207)完全确定  。
- **正定性**：为了保证材料在未变形状态下的稳定性（即任何变形都会增加其能量），[应变能密度函数](@entry_id:755490)必须是严格凸的，其在 $\boldsymbol{\varepsilon}=\mathbf{0}$ 处有最小值。这意味着[弹性张量](@entry_id:170728) $\mathbb{C}$ 必须是**正定的**，即对于任何非零的对称应变张量 $\boldsymbol{\varepsilon}$，二次型 $\boldsymbol{\varepsilon} : \mathbb{C} : \boldsymbol{\varepsilon}$ 恒为正 。

### [材料对称性](@entry_id:190289)与[各向同性弹性](@entry_id:203237)

材料的微观结构（如[晶体结构](@entry_id:140373)、纤维取向）通常具有某种对称性，这会反映在宏观的本构关系上，对[弹性张量](@entry_id:170728) $\mathbb{C}$ 施加额外的约束。[材料对称性](@entry_id:190289)越高，独立的[弹性常数](@entry_id:146207)就越少。例如：
- **[正交各向异性](@entry_id:196967)**（Orthotropic）：具有三个相互正交的对称面，有 $9$ 个独立常数。
- **横观各向同性**（Transversely Isotropic）：在一个平面内是各向同性的，而在垂直于该平面的方向上具有不同性质，有 $5$ 个独立常数。
- **立方对称性**（Cubic）：具有立方[晶系](@entry_id:137271)的对称性，有 $3$ 个独立常数。

最简单且最常见的情况是**各向同性**（Isotropic）材料，其力学性质在所有方向上都相同。对于这类材料，[弹性张量](@entry_id:170728) $\mathbb{C}$ 的一般形式仅由两个独立的材料常数确定  ：
$$
\mathbb{C}_{ijkl} = \lambda \delta_{ij} \delta_{kl} + \mu (\delta_{ik} \delta_{jl} + \delta_{il} \delta_{jk})
$$
这里的 $\lambda$ 和 $\mu$ 便是**拉梅参数**（Lamé parameters）。将此形式代入[广义胡克定律](@entry_id:203555)，得到[各向同性材料](@entry_id:170678)的[应力-应变关系](@entry_id:274093)：
$$
\boldsymbol{\sigma} = \lambda \, \mathrm{tr}(\boldsymbol{\varepsilon}) \, \mathbf{I} + 2\mu \boldsymbol{\varepsilon}
$$
其中，$\mathrm{tr}(\boldsymbol{\varepsilon})$ 是[应变张量](@entry_id:1132487)的迹，代表[体积应变](@entry_id:267252)。$\mu$ 具有明确的物理意义，即**[剪切模量](@entry_id:167228)**（shear modulus），它描述了材料抵抗[剪切变形](@entry_id:170920)的能力。

拉梅参数与工程中更常用的**[杨氏模量](@entry_id:140430)**（Young's modulus）$E$ 和**泊松比**（Poisson's ratio）$\nu$ 可以通过分析一个简单的[单轴拉伸试验](@entry_id:195375)来建立联系。通过对单轴应力状态下的应变进行分析，可以推导出它们之间的换算关系 ：
$$
\mu = \frac{E}{2(1+\nu)}, \quad \lambda = \frac{E\nu}{(1+\nu)(1-2\nu)}
$$
对于[各向同性材料](@entry_id:170678)，[弹性张量](@entry_id:170728)的正定性条件等价于 $\mu > 0$ 和体积模量 $K = \lambda + \frac{2}{3}\mu > 0$（在三维情况下）。

### 实践表述与数值考量

为了将弹性理论应用于实际计算，需要将其转化为适合计算机处理的形式，并注意其中可能出现的数值问题。

#### 沃伊特（Voigt）表示法

在数值计算（尤其是[有限元分析](@entry_id:138109)）中，将[四阶张量](@entry_id:181350) $\mathbb{C}$ 和[二阶张量](@entry_id:199780) $\boldsymbol{\sigma}$、$\boldsymbol{\varepsilon}$ 分别写成 $6 \times 6$ 矩阵和 $6 \times 1$ 向量的形式会极大地方便编程实现。这种表示法称为**沃伊特表示法**。其核心是将对称[二阶张量](@entry_id:199780)的六个独立分量映射到一个向量中，例如：
$$
\{\sigma_{11}, \sigma_{22}, \sigma_{33}, \sigma_{23}, \sigma_{13}, \sigma_{12}\} \quad \text{和} \quad \{\varepsilon_{11}, \varepsilon_{22}, \varepsilon_{33}, 2\varepsilon_{23}, 2\varepsilon_{13}, 2\varepsilon_{12}\}
$$
在沃伊特表示法中，一个关键的细节是如何处理剪切分量中的因子 $2$。这是因为在完整的[张量缩并](@entry_id:193373) $\sigma_{ij} = C_{ijkl}\varepsilon_{kl}$ 中，剪切项（如 $C_{ij12}\varepsilon_{12}$ 和 $C_{ij21}\varepsilon_{21}$）会成对出现。存在两种主流的约定来保持能量和应力计算的一致性 ：
1.  **工程剪切应变约定**：在应变向量中采用工程剪切应变 $\gamma_{ij} = 2\varepsilon_{ij}$ ($i \neq j$)。此时，[刚度矩阵](@entry_id:178659)的分量可以直接从张量分量转换（$C_{\alpha\beta} = C_{ijkl}$），且得到的 $6 \times 6$ 刚度矩阵是对称的。
2.  **张量剪切应变约定**：在应变向量中直接使用张量剪切应变分量 $\varepsilon_{ij}$ ($i \neq j$)。为了补偿缺失的因子 $2$，必须将其引入到刚度矩阵的定义中。这种约定下得到的[刚度矩阵](@entry_id:178659)通常是非对称的。

#### 弹性力学边值问题

一个完整的静态[线性弹性力学](@entry_id:166983)问题由以下几部分构成，这被称为问题的**强形式**（strong form）：
- **平衡方程**：$\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}$ （在求解域 $\Omega$ 内）
- **[几何方程](@entry_id:173321)**：$\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^{\top})$
- **本构方程**：$\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}$
- **边界条件**：
    - **狄利克雷边界**（Dirichlet boundary）：位移已知, $\mathbf{u} = \bar{\mathbf{u}}$ on $\Gamma_u$
    - **诺伊曼边界**（Neumann boundary）：牵[引力](@entry_id:189550)已知, $\boldsymbol{\sigma}\mathbf{n} = \bar{\mathbf{t}}$ on $\Gamma_t$

强形式是偏微分方程组，通常难以求得解析解。有限元法（FEM）等数值方法求解的是问题的**弱形式**（weak form）或称**变分形式**（variational form）。[弱形式](@entry_id:142897)是通过将[平衡方程](@entry_id:172166)与一个任意的**[检验函数](@entry_id:166589)**（test function）$\mathbf{v}$ 做[内积](@entry_id:750660)并在全域积分，然后利用[分部积分](@entry_id:136350)（高斯散度定理）推导出来的。最终的[弱形式](@entry_id:142897)表述为：寻找一个满足[狄利克雷边界条件](@entry_id:173524)的**[试探函数](@entry_id:756165)**（trial function）$\mathbf{u}$，使得对于所有在狄利克雷边界上为零的[检验函数](@entry_id:166589) $\mathbf{v}$，以下[积分方程](@entry_id:138643)成立 ：
$$
\int_{\Omega} \boldsymbol{\sigma}(\mathbf{u}) : \boldsymbol{\varepsilon}(\mathbf{v})\,d\Omega = \int_{\Omega} \mathbf{b} \cdot \mathbf{v}\,d\Omega + \int_{\Gamma_{t}} \bar{\mathbf{t}} \cdot \mathbf{v}\,dS
$$
在这个过程中，狄利克雷边界条件是必须强加的**[本质边界条件](@entry_id:173524)**，而[诺伊曼边界条件](@entry_id:142124)则自然地出现在积分方程中，称为**自然边界条件**。

#### 不可压缩极限与[体积锁定](@entry_id:172606)

对于橡胶等近乎不可压缩的材料，其泊松比 $\nu$ 接近 $0.5$。在此极限下，拉梅参数 $\lambda$ 和体积模量 $K$ 趋于无穷大 。这使得[应变能](@entry_id:162699)中的体积项 $\frac{1}{2}K(\mathrm{tr}(\boldsymbol{\varepsilon}))^2$ 对任何非零的体积变化施加巨大的惩罚。因此，材料的运动在物理上必须近似满足**不可压缩性约束**：
$$
\mathrm{tr}(\boldsymbol{\varepsilon}) = \nabla \cdot \mathbf{u} = 0
$$
在标准的位移有限元法中，特别是使用低阶单元（如线性三角形或四边形）时，离散的位移[函数空间](@entry_id:143478)很难精确满足这个约束。在每个单元或积分点上强加 $\nabla \cdot \mathbf{u}_h = 0$ 会引入过多的约束，导致系统自由度被“锁死”，无法正确模拟弯曲等变形模式。这种现象称为**[体积锁定](@entry_id:172606)**（volumetric locking），其表现为数值解被人为地变得异常刚硬 。

与[体积锁定](@entry_id:172606)相伴的是，当 $\nu \to 0.5$ 时，[有限元刚度矩阵](@entry_id:167652)的条件数会急剧增大（与 $K/\mu$ 同阶），导致数值求解变得非常困难 。

解决[体积锁定](@entry_id:172606)的常用策略包括：
- **混合单元法**（Mixed formulation）：引入压力 $p$ 作为一个独立的未知量场（[拉格朗日乘子](@entry_id:142696)），用于在弱形式意义下施加不可压缩约束。位移和压力的离散函数空间必须满足特定的[兼容性条件](@entry_id:201103)，即**LBB（Ladyzhenskaya-Babuška-Brezzi）条件**或**[inf-sup条件](@entry_id:746626)**，以保证[数值稳定性](@entry_id:175146) 。
- **降阶/选择性积分**（Reduced/selective integration）：对刚度矩阵中的体积能项采用比剪切能项更低阶的[数值积分法则](@entry_id:175061)，从而放松约束。**[B-bar方法](@entry_id:169265)**通过修改[应变-位移矩阵](@entry_id:163451)达到类似的效果 。

值得特别指出的是，[体积锁定](@entry_id:172606)主要影响三维和[平面应变](@entry_id:167046)问题。在**[平面应力](@entry_id:172193)**问题中，由于材料可以在厚度方向上自由变形以补偿平面内的面积变化，不可压缩性约束可以自然满足，因此不会出现[体积锁定](@entry_id:172606)现象 。