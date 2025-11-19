## 引言
应变与应力是固体力学乃至整个[材料科学](@entry_id:152226)领域的基石。它们是描述物质如何响应外力、温度变化或其他刺激而发生变形和产生[内力](@entry_id:167605)的基本语言。从摩天大楼的结构安全到[半导体](@entry_id:141536)芯片中的微观应力，再到生物组织的力学行为，对这些概念的深刻理解是现代科学与工程实践的核心。然而，从抽象的张量数学到解决具体物理问题的应用之间，往往存在一条知识鸿沟。本文旨在系统性地跨越这条鸿沟，为读者构建一个关于[弹性应变](@entry_id:189634)与[应力分析](@entry_id:168804)的坚实而全面的知识体系。

本文将引导读者踏上一段从理论到应用的旅程。在第一章“原理和机制”中，我们将奠定坚实的理论基础，系统阐述应变和应力的定义、它们所遵循的物理定律（如协调性与[平衡方程](@entry_id:172166)），以及连接二者的核心——[本构关系](@entry_id:186508)。随后的第二章“应用与跨学科交叉”，我们将展示这些理论的强大威力，探讨其如何在工程力学、[材料科学](@entry_id:152226)、地球物理学等不同领域解决实际问题，从宏观的结构失效预测到微观的缺陷相互作用。最后，在“动手实践”部分，通过精选的计算练习，读者将有机会亲手应用所学知识，巩固对关键概念的理解。通过这一结构化的学习路径，读者将能够不仅掌握[应力应变](@entry_id:204183)分析的数学形式，更能领会其在科学探索和技术创新中的深刻内涵。

## 原理和机制

本章旨在系统性地阐述描述固体[材料力学](@entry_id:201885)行为的核心概念——应变和应力，并探讨它们之间的本构关系。我们将从变形的几何描述出发，逐步建立[应变张量](@entry_id:193332)的概念，区分微小变形和有限变形。随后，我们将引入应力的概念，并讨论其在平衡状态下的性质。最后，我们将重点讨论连接应力和应变的[本构关系](@entry_id:186508)，涵盖从简单的线弹性[各向同性材料](@entry_id:170678)到复杂的[各向异性晶体](@entry_id:193334)，并进一步拓展到[热弹性耦合](@entry_id:183445)和有限变形理论的范畴。

### 变形的几何描述：应变

当一个物体受到外力或[发生温度](@entry_id:197328)变化时，其内部各点的相对位置会发生改变，这种几何形状和尺寸的变化我们称之为**变形 (deformation)**。为了定量地描述变形，我们引入应变的概念。

#### 微小应变

在多数工程和物理应用场景中，材料的变形非常微小。在这种情况下，我们可以使用**微[小应变张量](@entry_id:754968) (infinitesimal strain tensor)**，也称为柯西[应变张量](@entry_id:193332)，来描述变形。考虑物体中一个点在变形前的参考构型中的位置矢量为 $\mathbf{X}$，变形后在当前构型中的位置矢量为 $\mathbf{x}$。[位移矢量场](@entry_id:196067) $\mathbf{u}$ 定义为 $\mathbf{u}(\mathbf{X}) = \mathbf{x} - \mathbf{X}$。当[位移梯度](@entry_id:165352)很小时，微[小应变张量](@entry_id:754968) $\boldsymbol{\epsilon}$ 的分量 $\epsilon_{ij}$ 定义为[位移梯度张量](@entry_id:748571) $\nabla \mathbf{u}$ 的对称部分：
$$
\epsilon_{ij} = \frac{1}{2}\left(\frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i}\right)
$$
其中，$u_i$ 是[位移矢量](@entry_id:262782) $\mathbf{u}$ 的分量，$x_i$ 是坐标分量。

对角分量 $\epsilon_{ii}$（无求和）被称为**[正应变](@entry_id:204633) (normal strains)**，它们描述了沿坐标轴方向的线段的相对伸长或缩短。非对角分量 $\epsilon_{ij}$ ($i \neq j$) 被称为**[剪应变](@entry_id:175241) (shear strains)**，它们描述了最初相互垂直的两个线元之间角度的变化。例如，工程[剪应变](@entry_id:175241) $\gamma_{xy} = 2\epsilon_{xy}$ 表示 $xy$ 平面内直角的改变量。

#### [应变协调性](@entry_id:199659)

值得注意的是，一个任意给定的应变张量场不一定对应一个物理上可能的变形。为了确保应变场可以由一个连续、单值的[位移场](@entry_id:141476)导出，它必须满足一组[偏微分方程](@entry_id:141332)，即**[圣维南协调条件](@entry_id:173493) (Saint-Venant compatibility conditions)**。这些条件保证了变形后物质的连续性，即不会出现不合理的孔洞或重叠。

例如，在一个二维平面问题中（平面应力或平面应变），存在一个单一的协调方程。假设一个应变场由以下分量描述 [@problem_id:33529]：
$$
\epsilon_{xx} = 6 x^2 y^2 + y^4
$$
$$
\epsilon_{yy} = C x^2 y^2
$$
$$
\gamma_{xy} = 4 x^3 y + F x y^3
$$
其中 $C$ 和 $F$ 是待定常数。二维协调条件要求：
$$
\frac{\partial^2 \epsilon_{xx}}{\partial y^2} + \frac{\partial^2 \epsilon_{yy}}{\partial x^2} = \frac{\partial^2 \gamma_{xy}}{\partial x \partial y}
$$
通过计算各个[偏导数](@entry_id:146280)并代入，我们可以发现，为了使该方程对所有 $x$ 和 $y$ 均成立，常数 $C$ 和 $F$ 必须满足特定的关系，即 $12 + 2C = 3F$。这个例子清晰地表明，一个物理上有效的应变场，其各个分量不是相互独立的，而是必须满足严格的数学约束。

#### 有限应变：格林-拉格朗日张量

当物体的变形很大，特别是包含大转动时，微[小应变张量](@entry_id:754968)不再适用。此时，我们需要使用**[有限应变理论](@entry_id:176941) (finite strain theory)**。一个常用的[有限应变度量](@entry_id:185716)是**[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)** $\mathbf{E}$。它在参考构型上定义，其分量形式为：
$$
E_{IJ} = \frac{1}{2} \left( \frac{\partial u_I}{\partial X_J} + \frac{\partial u_J}{\partial X_I} + \sum_{K=1}^3 \frac{\partial u_K}{\partial X_I} \frac{\partial u_K}{\partial X_J} \right)
$$
其中，$u_I$ 是位移分量，$X_I$ 是参考构型中的坐标。这个定义包含了一个[非线性](@entry_id:637147)的二次项 $\frac{\partial u_K}{\partial X_I} \frac{\partial u_K}{\partial X_J}$，它能够正确处理大位移和大转动。

考虑一个同时经历均匀膨胀和有限简单剪切的物体，其[位移场](@entry_id:141476)为 $u_1 = \epsilon X_1 + \gamma X_2$, $u_2 = \epsilon X_2$, $u_3 = \epsilon X_3$ [@problem_id:33510]。通过计算位移[偏导数](@entry_id:146280)并代入上式，我们可以得到 $E_{22}$ 分量为 $\epsilon + \frac{1}{2} (\gamma^2 + \epsilon^2)$。这里的 $\frac{1}{2}\gamma^2$ 项正是由[非线性](@entry_id:637147)项贡献的，它表明在有限剪切下，即使在垂直于剪切位移的方向上也会产生[正应变](@entry_id:204633)效应。

#### 有限变形的运动学：变形梯度与极分解

有限变形的运动学可以通过**变形梯度张量 (deformation gradient tensor)** $\mathbf{F}$ 进行更深入的描述，其分量定义为 $F_{iJ} = \partial x_i / \partial X_J$。$\mathbf{F}$ 描述了参考构型中的一个微小线元 $d\mathbf{X}$ 如何映射到当前构型中的 $d\mathbf{x}$，即 $d\mathbf{x} = \mathbf{F} d\mathbf{X}$。

根据**极分解定理 (polar decomposition theorem)**，任何可逆的变形梯度 $\mathbf{F}$ 都可以唯一地分解为一个[旋转张量](@entry_id:191990) $\mathbf{R}$ 和一个对称正定的**右[拉伸张量](@entry_id:193200) (right stretch tensor)** $\mathbf{U}$ 的乘积，即 $\mathbf{F} = \mathbf{R}\mathbf{U}$。$\mathbf{U}$ 描述了材料纤维的纯拉伸和剪切，而 $\mathbf{R}$ 描述了随后的刚体旋转。右[拉伸张量](@entry_id:193200) $\mathbf{U}$ 与**右柯西-格林变形张量 (right Cauchy-Green deformation tensor)** $\mathbf{C} = \mathbf{F}^T \mathbf{F}$ 之间存在关系 $\mathbf{U} = \sqrt{\mathbf{C}}$。通过分析一个给定的变形梯度场，可以计算出相应的[拉伸张量](@entry_id:193200)，从而量化局部的纯变形 [@problem_id:33500]。

### 力的概念与力学平衡

为了维持材料的变形状态，必须有力的作用。在连续介质力学中，我们使用应力来描述物体内部相互作用力的[分布](@entry_id:182848)。

#### 柯西应力张量

**柯西[应力张量](@entry_id:148973) (Cauchy stress tensor)** $\boldsymbol{\sigma}$ 是描述变形后物体（当前构型）内部应力状态的基本工具。其分量 $\sigma_{ij}$ 表示在 $x_i$ 方向上作用于单位面积法向为 $x_j$ 的微小面上的力。与应变张量类似，对角分量 $\sigma_{ii}$ 是**正应力 (normal stresses)**，非对角分量 $\sigma_{ij}$ ($i \neq j$) 是**剪应力 (shear stresses)**。

应力是一个张量，这意味着它的分量会随着[坐标系](@entry_id:156346)的旋转而变换。考虑一个二维[平面应力](@entry_id:172193)状态，在一个 $(x, y)$ [坐标系](@entry_id:156346)下，应力张量为已知。当我们[旋转坐标系](@entry_id:170324)一个角度 $\theta$ 得到新的 $(x', y')$ [坐标系](@entry_id:156346)时，新[坐标系](@entry_id:156346)下的正应力 $\sigma_{x'x'}$ 和剪应力 $\tau_{x'y'}$ 可以通过坐标变换公式计算得出 [@problem_id:33535]：
$$
\sigma_{x'x'}=\frac{\sigma_{xx}+\sigma_{yy}}{2}+\frac{\sigma_{xx}-\sigma_{yy}}{2}\cos(2\theta)+\sigma_{xy}\sin(2\theta)
$$
$$
\tau_{x'y'}=-\frac{\sigma_{xx}-\sigma_{yy}}{2}\sin(2\theta)+\sigma_{xy}\cos(2\theta)
$$
这些变换公式是[材料力学](@entry_id:201885)中的核心，它们允许我们找到主应力（剪应力为零的面上的[正应力](@entry_id:260622)）和[最大剪应力](@entry_id:181794)，这对于预测材料的屈服和断裂至关重要。

#### 静力学平衡

在一个处于静止状态的物体中，任何一部分都必须处于力学平衡状态。这要求应[力场](@entry_id:147325)必须满足**柯西静力学[平衡方程](@entry_id:172166) (Cauchy's equation of motion for statics)**：
$$
\nabla \cdot \boldsymbol{\sigma} + \mathbf{f} = 0
$$
或者写成分量形式 $\sum_j \frac{\partial \sigma_{ij}}{\partial x_j} + f_i = 0$。这里，$\mathbf{f}$ 是作用在物体上的**[体力](@entry_id:174230) (body force)**，例如重力或[电磁力](@entry_id:196024)，单位是力/单位体积。这个方程表明，应力在空间上的变化率必须由[体力](@entry_id:174230)来平衡。

给定一个位移场，我们可以依次计算出应变场和应[力场](@entry_id:147325)（需要本构关系，见下一节），然后通过[平衡方程](@entry_id:172166)确定为维持该变形状态所必需的体力场[分布](@entry_id:182848) [@problem_id:33549]。这是一个典型的“[逆问题](@entry_id:143129)”，在地球物理学和[材料设计](@entry_id:160450)等领域有重要应用。

#### [静水压力与偏应力](@entry_id:750463)

将应力张量分解为两部分通常很有用：一部分引起体积变化，另一部分引起形状变化。**[静水压力](@entry_id:275365) (hydrostatic stress)** 或球[应力张量](@entry_id:148973)定义为 $\frac{1}{3} \mathrm{Tr}(\boldsymbol{\sigma}) \boldsymbol{\delta}$，其中 $\mathrm{Tr}(\boldsymbol{\sigma}) = \sigma_{kk}$ 是应力张量的迹，$\boldsymbol{\delta}$ 是单位张量。这部分应力倾向于均匀地压缩或拉伸物体，而不改变其形状。

从总应力中减去静水压力部分，我们得到**[偏应力张量](@entry_id:267642) (deviatoric stress tensor)** $\mathbf{s}$：
$$
s_{ij} = \sigma_{ij} - \frac{1}{3} \mathrm{Tr}(\boldsymbol{\sigma}) \delta_{ij}
$$
[偏应力张量](@entry_id:267642)描述了引起材料畸变或剪切变形的应力状态。许多材料的塑性屈服行为，如金属，主要由[偏应力](@entry_id:163323)的大小决定。[偏应力张量](@entry_id:267642)的第二[不变量](@entry_id:148850) $J_2 = \frac{1}{2} s_{ij}s_{ji}$ 是一个重要的标量，它正比于材料的**弹性[畸变能](@entry_id:198925)密度 (elastic distortion energy density)**，并构成了著名的冯·米塞斯屈服准则 (von Mises yield criterion) 的基础 [@problem_id:33604]。

### [本构关系](@entry_id:186508)：连接应力与应变

本构关系（或[本构方程](@entry_id:138559)）是描述特定材料[应力与应变](@entry_id:137374)之间关系的数学模型。它们是材料的内在属性，反映了其微观结构和原子间相互作用。

#### 线弹性与[胡克定律](@entry_id:149682)

对于许多材料在小变形范围内，[应力与应变](@entry_id:137374)成线性关系，这被称为**线弹性 (linear elasticity)**。这种关系由**[广义胡克定律](@entry_id:203555) (generalized Hooke's law)** 描述：
$$
\sigma_{ij} = C_{ijkl} \epsilon_{kl}
$$
其中 $C_{ijkl}$ 是四阶的**[弹性刚度张量](@entry_id:170728) (elastic stiffness tensor)**，其分量是材料的[弹性常数](@entry_id:146207)。反之，我们也可以写出 $\epsilon_{ij} = S_{ijkl} \sigma_{kl}$，其中 $S_{ijkl}$ 是**[弹性柔度](@entry_id:189433)张量 (elastic compliance tensor)**。

#### [各向同性材料](@entry_id:170678)

最简单的情况是**各向同性 (isotropic)** 材料，其力学性质在所有方向上都相同。在这种情况下，其弹性行为可以由两个独立的弹性常数完全描述。常用的有拉梅常数 (Lamé parameters) $\lambda$ 和 $\mu$（$\mu$ 也被称为[剪切模量](@entry_id:167228) $G$）。其本构关系为 [@problem_id:33549]：
$$
\sigma_{ij} = \lambda \delta_{ij} \epsilon_{kk} + 2\mu \epsilon_{ij}
$$
其中 $\epsilon_{kk}$ 是应变张量的迹，代表体积应变。

#### [各向异性材料](@entry_id:184874)：晶体

晶体材料由于其规则的原子[排列](@entry_id:136432)而表现出**各向异性 (anisotropy)**，即其弹性性质依赖于方向。晶体的对称性会减少[独立弹性常数](@entry_id:203649)的数量。例如，**[立方晶体](@entry_id:198932) (cubic crystal)** 具有3个独立的[弹性常数](@entry_id:146207)：$C_{11}$、$C_{12}$ 和 $C_{44}$（使用Voigt简写标记）。其[应力-应变关系](@entry_id:274093)更为复杂 [@problem_id:33604]：
$$
\begin{aligned}
\sigma_{11} = C_{11}\epsilon_{11} + C_{12}(\epsilon_{22} + \epsilon_{33}) \\
\sigma_{23} = 2C_{44}\epsilon_{23} \quad (\text{及其他分量的循环置换})
\end{aligned}
$$
由于各向异性，像杨氏模量 $E$ 这样的弹性模量也依赖于晶体取向。例如，对于立方晶体，沿 $[110]$ 方向的[杨氏模量](@entry_id:140430) $E_{[110]}$ 可以表示为 $C_{11}$、$C_{12}$ 和 $C_{44}$ 的一个特定组合 [@problem_id:33505]，这与沿[主轴](@entry_id:172691) $[100]$ 方向的[杨氏模量](@entry_id:140430) $E_{[100]}$ 不同。

#### [弹性稳定性](@entry_id:182825)

物理上，一个材料必须是稳定的。在力学上，这意味着任何施加的应变都必须增加系统的**[应变能密度](@entry_id:200085) (strain energy density)** $U$。对于线弹性材料，$U$ 是应变分量的二次型：
$$
U = \frac{1}{2} C_{ijkl} \epsilon_{ij} \epsilon_{kl}
$$
稳定性要求这个二次型是正定的，即对于任何非零应变，$U > 0$。这个要求对弹性常数施加了一系列[不等式约束](@entry_id:176084)，即**伯恩[稳定性判据](@entry_id:755304) (Born stability criteria)**。例如，对于一个六方晶体，通过考虑特定的应变模式并要求应变能为正，可以推导出其[弹性常数](@entry_id:146207)必须满足如 $(C_{11} + C_{12})C_{33} > 2C_{13}^2$ 这样的不等式关系 [@problem_id:33483]。

#### 高级[本构模型](@entry_id:174726)

**1. [热弹性耦合](@entry_id:183445)**

材料的力学行为通常与温度相关。在**[热弹性](@entry_id:158447) (thermoelasticity)** 框架下，我们可以定义一个依赖于应变和温度 $T$ 的**亥姆霍兹自由能密度 (Helmholtz free energy density)** $F(\boldsymbol{\epsilon}, T)$。[应力张量](@entry_id:148973)可以通过[热力学](@entry_id:141121)关系导出：
$$
\sigma_{ij} = \left( \frac{\partial F}{\partial \epsilon_{ij}} \right)_T
$$
通过构建一个合适的[自由能函数](@entry_id:749582)，可以模型化复杂的耦合效应，例如热膨胀（应力依赖于温度变化）和弹性常数对温度的依赖性。例如，从一个包含应变、温度以及它们耦合项的自由能表达式出发，我们可以推导出一个完整的应力-应变-温度本构关系 [@problem_id:33582]，该关系可以描述材料在非等温条件下的力学响应。

**2. 有限变形中的应力测量**

在有限变形理论中，由于参考构型和当前构型不再相同，可以定义多种应力张量。除了作用在当前构型上的柯西应力 $\boldsymbol{\sigma}$ 外，还有与参考构型相关的应力张量，如**第一和[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量 (1st and 2nd Piola-Kirchhoff stress tensors)**。[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量 $\mathbf{S}$ 在能量上与[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E}$ 共轭。它与柯西应力 $\boldsymbol{\sigma}$ 的关系通过变形梯度 $\mathbf{F}$ 建立：
$$
\boldsymbol{\sigma} = \frac{1}{J} \mathbf{F} \mathbf{S} \mathbf{F}^T
$$
其中 $J = \det(\mathbf{F})$。这个关系是有限变形力学中的一个核心变换。在处理复杂几何和[坐标系](@entry_id:156346)时，我们可能需要先从一个简单的应力状态（如在参考构型中定义的 $\mathbf{S}$）出发，通过此变换计算出当前构型中的柯西应力，然后再将其变换到特定的[曲线坐标系](@entry_id:172561)下，例如计算其[逆变分量](@entry_id:185440) [@problem_id:33471]。这一过程整合了[运动学](@entry_id:173318)、应力定义和[张量分析](@entry_id:161423)，是解决高级[固体力学](@entry_id:164042)问题的基础。