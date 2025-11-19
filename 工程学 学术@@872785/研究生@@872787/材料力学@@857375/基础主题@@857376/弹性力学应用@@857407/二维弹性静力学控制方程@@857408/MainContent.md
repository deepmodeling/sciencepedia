## 引言
在工程和科学领域，理解固体在外力作用下的内部响应——即应力和应变的[分布](@entry_id:182848)——对于确保结构的安全、可靠和高效至关重要。[二维弹性静力学](@entry_id:200674)为分析这类问题提供了一个基础而强大的数学框架，它将复杂的物理现象抽象为一组严谨的控制方程。本文旨在系统性地构建这一理论体系，弥合抽象原理与实际应用之间的鸿沟，使读者能够掌握从问题建模到求解分析的全过程。

本文将分为三个核心章节，引领您逐步深入[二维弹性静力学](@entry_id:200674)的世界。在“原理与机制”一章中，我们将从第一性原理出发，详细推导构成该理论基石的平衡方程、[运动学方程](@entry_id:173032)和本构关系，并介绍[平面应力与平面应变](@entry_id:172357)这两种关键的二维简化模型，同时还将探讨[艾里应力函数](@entry_id:191331)、[复变函数](@entry_id:175282)以及变分原理等核心求解策略。接下来，“应用与跨学科联系”一章将通过分析应力集中、[裂纹尖端](@entry_id:182807)场等经典问题，展示这些理论在解决工程设计难题中的巨大威力，并揭示其与断裂力学、[材料科学](@entry_id:152226)及[生物力学](@entry_id:153973)等前沿领域的深刻联系。最后，通过“动手实践”部分，您将有机会通过解决具体问题来巩固所学知识。通过这一系列的学习，您将不仅理解了这些方程的数学形式，更能体会到它们在解决真实世界问题中的实际价值。

## 原理与机制

本章深入探讨[二维弹性静力学](@entry_id:200674)的核心控制方程。我们将系统地建立描述弹性体在平面载荷下行为的数学框架。这包括三个基本组成部分：描述力的平衡（动力学）、描述变形的几何关系（运动学），以及连接力和变形的材料本构关系。我们将从基本原理出发，推导出这些方程，并阐明它们之间的相互作用。此外，我们还将介绍求解这些方程的几种关键方法，为后续章节中更具体的应用问题奠定理论基础。

### 应力与[平衡方程](@entry_id:172166)

在连续介质力学中，我们通过**应力**来量化物体内部的内力[分布](@entry_id:182848)。考虑物体内部一个假想的切割面，该面一侧的材料会对另一侧施加一个[分布](@entry_id:182848)力。单位面积上的力定义为**[面力矢量](@entry_id:189429)**或**牵[引力](@entry_id:175476)** $\mathbf{t}$。根据柯西应力定理，对于任意给定的点，其上的[面力矢量](@entry_id:189429) $\mathbf{t}$ 与该面的法向量 $\mathbf{n}$ 之间存在线性关系，该关系由一个二阶张量——**柯西[应力张量](@entry_id:148973)** $\boldsymbol{\sigma}$ 来定义。该关系通常写作：

$$
\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}
$$

在二维[笛卡尔坐标系](@entry_id:169789) $(x,y)$ 中，[应力张量](@entry_id:148973)可以表示为一个矩阵：

$$
\boldsymbol{\sigma} = \begin{pmatrix} \sigma_{xx} & \sigma_{xy} \\ \sigma_{yx} & \sigma_{yy} \end{pmatrix}
$$

其中，$\sigma_{xx}$ 和 $\sigma_{yy}$ 是**[正应力](@entry_id:260622)**，分别作用于垂直于 $x$ 轴和 $y$ 轴的平面上。$\sigma_{xy}$ 和 $\sigma_{yx}$ 是**剪应力**，作用于各自平面的切向方向。

为了使物体保持静止，作用在其上所有力必须平衡。考虑物体内部一个任意的微元体，对其应用牛顿定律（[线性动量守恒](@entry_id:165717)）。在静态且存在[体力](@entry_id:174230)密度 $\mathbf{b} = (b_x, b_y)$（如重力）的情况下，力的平衡要求应[力场](@entry_id:147325)的散度必须抵消[体力](@entry_id:174230)。这导出了**[局部平衡](@entry_id:156295)方程** (local equilibrium equations) [@problem_id:2889739]：

$$
\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} + b_x = 0
$$
$$
\frac{\partial \sigma_{yx}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} + b_y = 0
$$

这些方程也被称为[柯西运动方程](@entry_id:204126)的静态形式。

除了力的平衡，力矩也必须平衡。对微元体应用角动量守恒定律，在没有体力矩的假设下，可以证明柯西应力张量必须是**对称的** [@problem_id:2889739]：

$$
\sigma_{xy} = \sigma_{yx}
$$

这个重要的结论将二维问题中的独立应力分量从四个减少到三个：$\sigma_{xx}$, $\sigma_{yy}$, 和 $\sigma_{xy}$。因此，上面第二条平衡方程通常写作 $\frac{\partial \sigma_{xy}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} + b_y = 0$。

### [运动学](@entry_id:173318)：应变与协调性

当物体受力时，它会发生变形。我们用**位移场** $\mathbf{u}(x,y)$ 来描述物体内各点从初始位置到最终位置的移动。[位移矢量](@entry_id:262782)有两个分量, $\mathbf{u} = (u, v)$。

**应变**是衡量物体局部变形的量，它描述了材料微元的拉伸和形状改变。对于小变形问题，我们可以建立应变与位移之间的[线性关系](@entry_id:267880)。考虑一个点附近的[位移梯度张量](@entry_id:748571) $\nabla \mathbf{u}$，它可以分解为一个对称部分和一个反对称部分。对称部分定义了**[无穷小应变张量](@entry_id:167211)** (infinitesimal strain tensor) $\boldsymbol{\varepsilon}$，而反对称部分描述了[刚体转动](@entry_id:191086)。[应变张量](@entry_id:193332)的分量由以下**[几何方程](@entry_id:173321)**给出 [@problem_id:2889757]：

$$
\varepsilon_{xx} = \frac{\partial u}{\partial x}
$$
$$
\varepsilon_{yy} = \frac{\partial v}{\partial y}
$$
$$
\varepsilon_{xy} = \varepsilon_{yx} = \frac{1}{2}\left(\frac{\partial u}{\partial y} + \frac{\partial v}{\partial x}\right)
$$

这里的 $\varepsilon_{xx}$ 和 $\varepsilon_{yy}$ 是**[正应变](@entry_id:204633)**，代表沿坐标轴方向的伸长率。$\varepsilon_{xy}$ 是**张量[剪应变](@entry_id:175241)**，代表两正交[线元](@entry_id:196833)夹角变化的一半。在工程应用中，更常用的是**工程[剪应变](@entry_id:175241)** $\gamma_{xy} = 2\varepsilon_{xy}$。

这种线性化的[应变-位移关系](@entry_id:173321)仅在**小[位移梯度](@entry_id:165352)**的假设下成立，即 $|\partial u_i / \partial x_j| \ll 1$。这个条件比位移本身很小要严格得多，它要求物体的局部拉伸和转动都必须是微小的 [@problem_id:2889757]。

由于三个应变分量（$\varepsilon_{xx}, \varepsilon_{yy}, \varepsilon_{xy}$）是由两个位移分量（$u, v$）通过[微分](@entry_id:158718)得到的，因此这三个应变分量之间不是[相互独立](@entry_id:273670)的。它们必须满足一定的约束条件，以保证能够从应变场积分得到一个单值的、连续的位移场。这个约束条件称为**协调性条件** (compatibility condition)。通过对[应变-位移关系](@entry_id:173321)式进行二[次微分](@entry_id:175641)并消去位移分量，我们可以得到二维情况下的**圣维南协调性方程** (Saint-Venant's compatibility equation) [@problem_id:2889746]：

$$
\frac{\partial^2 \varepsilon_{xx}}{\partial y^2} + \frac{\partial^2 \varepsilon_{yy}}{\partial x^2} = 2 \frac{\partial^2 \varepsilon_{xy}}{\partial x \partial y}
$$

重要的是，这个方程完全由几何关系导出，不涉及任何材料属性。因此，协调性是一个纯粹的**运动学条件**。任何物理上可能的应变场都必须满足此条件。

### [本构关系](@entry_id:186508)：[胡克定律](@entry_id:149682)

[平衡方程](@entry_id:172166)和[几何方程](@entry_id:173321)描述了所有连续介质的普遍行为。为了完整描述一个特定材料（如钢或橡胶）的行为，我们需要第三组方程，即**[本构方程](@entry_id:138559)** (constitutive equations)，它建立了[应力与应变](@entry_id:137374)之间的关系。

对于线弹性、各向同性材料，这种关系由**[胡克定律](@entry_id:149682)** (Hooke's law) 给出。其最普遍的张量形式使用两个**拉梅参数** (Lamé parameters) $\lambda$ 和 $\mu$ 来表述 [@problem_id:2889796]：

$$
\boldsymbol{\sigma} = \lambda \, \mathrm{tr}(\boldsymbol{\varepsilon}) \mathbf{I} + 2\mu \boldsymbol{\varepsilon}
$$

其中 $\mathrm{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{kk}$ 是应变张量的迹（[体积应变](@entry_id:267252)），$\mathbf{I}$ 是单位张量，而 $\mu$ 也被称为**剪切模量** $G$。

在工程实践中，更常用的是**杨氏模量** $E$ 和**[泊松比](@entry_id:158876)** $\nu$。这两组材料常数可以通过以下关系进行转换 [@problem_id:2889796]：

$$
\mu = \frac{E}{2(1+\nu)}
$$
$$
\lambda = \frac{E\nu}{(1+\nu)(1-2\nu)}
$$

### 二维简化模型：[平面应力与平面应变](@entry_id:172357)

许多工程结构可以近似为二维问题进行分析，这大大简化了求解过程。两种最主要的二维简化是[平面应力](@entry_id:172193)和[平面应变](@entry_id:167046)。

#### 平面应力

**平面应力** (plane stress) 状态假设物体非常薄（如薄板），且载荷作用于其平面内。由于其上下表面（垂直于 $z$ 轴）是自由的，我们假设所有与 $z$ 方向相关的应力分量在整个厚度上都为零 [@problem_id:2889738]：

$$
\sigma_{zz} = \sigma_{xz} = \sigma_{yz} = 0
$$

在这种情况下，物体可以在 $z$ 方向上自由伸缩。根据胡克定律，这会导致非零的平面外[正应变](@entry_id:204633)，即**厚度变化** [@problem_id:2889774]：

$$
\varepsilon_{zz} = -\frac{\nu}{E}(\sigma_{xx} + \sigma_{yy})
$$

通过将 $\sigma_{zz}=0$ 代入三维胡克定律并整理，我们可以得到平面应力状态下的二维[本构关系](@entry_id:186508)。若写成矩阵形式，将应力向量 $\{\sigma_{xx}, \sigma_{yy}, \sigma_{xy}\}^T$ 与包含工程[剪应变](@entry_id:175241)的应变向量 $\{\varepsilon_{xx}, \varepsilon_{yy}, \gamma_{xy}\}^T$ 联系起来，其关系为 [@problem_id:2889781]：

$$
\begin{pmatrix} \sigma_{xx} \\ \sigma_{yy} \\ \sigma_{xy} \end{pmatrix} = \frac{E}{1-\nu^2} \begin{pmatrix} 1 & \nu & 0 \\ \nu & 1 & 0 \\ 0 & 0 & \frac{1-\nu}{2} \end{pmatrix} \begin{pmatrix} \varepsilon_{xx} \\ \varepsilon_{yy} \\ \gamma_{xy} \end{pmatrix}
$$

#### [平面应变](@entry_id:167046)

**[平面应变](@entry_id:167046)** (plane strain) 状态则适用于沿某一方向（如 $z$ 轴）非常长、且[横截面](@entry_id:154995)和载荷沿该方向保持不变的物体（如大坝、隧道或长管道）。在这种情况下，可以合理假设沿 $z$ 轴方向的变形为零 [@problem_id:2889738]：

$$
\varepsilon_{zz} = \varepsilon_{xz} = \varepsilon_{yz} = 0
$$

为了维持 $\varepsilon_{zz}=0$ 的约束，物体内部必须产生一个非零的轴向应力 $\sigma_{zz}$。根据[胡克定律](@entry_id:149682)，这个应力由平面[内应力](@entry_id:193721)决定 [@problem_id:2889774]：

$$
\sigma_{zz} = \nu(\sigma_{xx} + \sigma_{yy})
$$

同样，我们可以推导出平面应变状态下的二维[本构关系](@entry_id:186508)。其矩阵形式与平面应力类似，但其中的材料常数有所不同。一个有效的方法是定义一组**等效二维模量** [@problem_id:2889758]：

$$
E' = \frac{E}{1-\nu^2}, \quad \nu' = \frac{\nu}{1-\nu}
$$

用这些等效模量替换[平面应力](@entry_id:172193)[本构关系](@entry_id:186508)中的 $E$ 和 $\nu$，即可得到平面应变的关系。值得注意的是，剪切项的系数 $G = \frac{E}{2(1+\nu)}$ 在平面应力和平面应变中是**相同**的，因为平面内[剪切变形](@entry_id:170920)与平面外约束无关 [@problem_id:2889774]。

### 求解策略与高级方法

我们已经建立了[二维弹性静力学](@entry_id:200674)的完整[方程组](@entry_id:193238)：平衡方程、[几何方程](@entry_id:173321)和[本构方程](@entry_id:138559)。下一步是求解这些方程以获得特定问题中的应力、应变和[位移场](@entry_id:141476)。

#### [艾里应力函数](@entry_id:191331)

对于没有体力的情况（$b_x=b_y=0$），平衡方程可以被自动满足。这是通过引入一个称为**[艾里应力函数](@entry_id:191331)** (Airy stress function) $\Phi(x,y)$ 的势函数实现的。应力分量由该函数的[二阶偏导数](@entry_id:635213)给出 [@problem_id:2889746]：

$$
\sigma_{xx} = \frac{\partial^2 \Phi}{\partial y^2}, \quad \sigma_{yy} = \frac{\partial^2 \Phi}{\partial x^2}, \quad \sigma_{xy} = -\frac{\partial^2 \Phi}{\partial x \partial y}
$$

将这些应力表达式代入平衡方程，会发现方程恒成立。这样，求解三个应力分量的问题就被简化为求解一个标量函数 $\Phi$。

剩下的任务是确保由 $\Phi$ 产生的应[力场](@entry_id:147325)能够对应一个协调的应变场。我们将应力表达式通过本构关系转换为应变，再代入[应变协调方程](@entry_id:195003)。对于均匀各向同性材料，这个过程最终会得到一个关于[艾里应力函数](@entry_id:191331)的单一控制方程——**[双调和方程](@entry_id:165706)** (biharmonic equation) [@problem_id:2889746]：

$$
\nabla^4 \Phi = \frac{\partial^4 \Phi}{\partial x^4} + 2\frac{\partial^4 \Phi}{\partial x^2 \partial y^2} + \frac{\partial^4 \Phi}{\partial y^4} = 0
$$

有趣的是，对于均匀材料，所有材料常数都在推导过程中被消除了。在极坐标 $(r, \theta)$ 中，[艾里应力函数](@entry_id:191331)和[双调和方程](@entry_id:165706)也有相应的形式，这对于解决圆形孔洞或圆盘等轴对称问题特别有用 [@problem_id:2889741]。

#### [复变函数](@entry_id:175282)方法

求解[双调和方程](@entry_id:165706)的一个强大工具是[复变函数](@entry_id:175282)理论。对于二维问题，任意双调和函数 $\Phi$ 都可以用两个解析函数（**Muskhelishvili[复势](@entry_id:162103)**）$\phi(z)$ 和 $\chi(z)$ 表示，其中 $z=x+iy$ 是[复变量](@entry_id:175312)。这种表示形式，即Goursat表示，为 [@problem_id:2889750]：

$$
\Phi(x,y) = \Re\left[\bar{z}\phi(z) + \chi(z)\right]
$$

其中 $\bar{z}$ 是 $z$ 的共轭。引入另一个[复势](@entry_id:162103) $\psi(z) = \chi'(z)$，应[力场](@entry_id:147325)和位移场可以完全由 $\phi(z)$ 和 $\psi(z)$ 这两个[解析函数](@entry_id:139584)简洁地表达出来。例如，关键的应力组合可以表示为 [@problem_id:2889750]：

$$
\sigma_{xx} + \sigma_{yy} = 4\Re\left[\phi'(z)\right]
$$
$$
\sigma_{yy} - \sigma_{xx} + 2i\sigma_{xy} = 2\left[\bar{z}\phi''(z) + \psi'(z)\right]
$$

这种方法将弹性力学问题转化为在复平面上寻找满足边界条件的解析函数的问题，在处理带有孔洞和裂纹的复杂几何问题时尤其有效。

#### 变分原理与弱形式

解析方法虽然强大，但仅限于相对简单的几何和边界条件。对于复杂的工程问题，数值方法（如[有限元法](@entry_id:749389)）是必不可少的。这些方法的基础是问题的**[变分形式](@entry_id:166033)**或**弱形式** (weak formulation)。

[弱形式](@entry_id:142897)的推导始于[平衡方程](@entry_id:172166)的强形式 $\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}$。我们将其乘以一个任意的、满足特定条件的**[虚位移](@entry_id:168781)**或**[检验函数](@entry_id:166589)** $\mathbf{w}$，然后在整个区域 $\Omega$ 上积分。通过应用[格林公式](@entry_id:173118)（即分部积分），应力上的[微分](@entry_id:158718)可以转移到检验函数上 [@problem_id:2889748]。

这个过程导出了**[虚功原理](@entry_id:138749)**，其最终形式为：寻找一个满足[位移边界条件](@entry_id:203261)的位移场 $\mathbf{u}$，使得对于所有满足齐次[位移边界条件](@entry_id:203261)的检验函数 $\mathbf{w}$，下式成立：

$$
\int_{\Omega} \boldsymbol{\sigma}(\mathbf{u}) : \boldsymbol{\varepsilon}(\mathbf{w}) \, d\Omega = \int_{\Omega} \mathbf{b} \cdot \mathbf{w} \, d\Omega + \int_{\Gamma_{N}} \bar{\mathbf{t}} \cdot \mathbf{w} \, d\Gamma
$$

在这个方程中，左侧代表内力的[虚功](@entry_id:176403)，右侧代表外力（体力和面力）的[虚功](@entry_id:176403)。

在[弱形式](@entry_id:142897)中，边界条件被分为两类 [@problem_id:2889748]：
- **[本质边界条件](@entry_id:173524)** (Essential Boundary Conditions)：指定的[位移边界条件](@entry_id:203261)（[狄利克雷条件](@entry_id:137096)）。它们通过限制解（[试探函数](@entry_id:756165)）和[检验函数](@entry_id:166589)所属的函数空间（通常是索伯列夫空间 $H^1$）来**强加**。
- **自然边界条件** (Natural Boundary Conditions)：指定的[面力边界条件](@entry_id:167112)（[诺伊曼条件](@entry_id:165471)）。它们作为边界积分项**自然地**出现在[变分方程](@entry_id:635018)中，无需对函数空间施加额外约束。

这种提法降低了对解的光滑性要求，并构成了有限元法离散化的理论基础，使其成为现代[固体力学](@entry_id:164042)分析的基石。