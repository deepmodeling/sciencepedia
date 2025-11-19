## 引言
在[连续介质力学](@entry_id:155125)和[材料科学](@entry_id:152226)中，精确量化和深刻理解材料的变形是分析其力学行为的基石。应变并非一个简单的标量，而是一个二阶张量，能够捕捉变形的方向性和复杂性。然而，如何从这个复杂的张量中提取出最关键的物理信息——例如最大拉伸方向、最大形状扭曲程度以及不随观察角度改变的内在属性——构成了本领域的一个核心知识挑战。本文旨在系统性地解决这一问题，为读者提供一套完整的分析工具。

本文将通过三个章节的递进式学习，引领读者全面掌握应变分析的核心理论与应用。在“原理与机制”一章中，我们将深入探讨应变张量的基本定义，建立[主应变](@entry_id:197797)和[应变不变量](@entry_id:190518)的代数框架，并借助[莫尔圆](@entry_id:168131)这一强大的几何工具将其可视化，同时澄清工程实践中常见的概念误区。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些理论如何在工程测量、[结构分析](@entry_id:153861)、[材料失效理论](@entry_id:185869)以及地球力学等领域中发挥关键作用，揭示其从理论到实践的桥梁。最后，通过“动手实践”部分，读者将有机会运用所学知识解决具体的工程问题，巩固并深化理解。通过本次学习，读者将能够自信地运用[主应变](@entry_id:197797)、[不变量](@entry_id:148850)和[莫尔圆](@entry_id:168131)来分析和解决复杂的[材料变形](@entry_id:169356)问题。

## 原理与机制

在深入研究材料的力学行为时，变形的量化是至关重要的第一步。应变，作为描述材料内部点相对位移的度量，并非一个简单的标量，而是一个二阶张量。这种张量属性能捕捉变形的幅度和方向性，揭示材料在不同方向上所经历的拉伸、压缩和剪切。本章旨在系统阐述描述应变状态的核心工具——[主应变](@entry_id:197797)、[应变不变量](@entry_id:190518)以及[莫尔圆](@entry_id:168131)，并探讨它们在不同变形条件下的应用与局限性。

### [应变张量](@entry_id:193332)的基本概念与[莫尔圆](@entry_id:168131)表示

在小变形假设下，材料内任一点的应变状态可以通过[无穷小应变张量](@entry_id:167211) $\boldsymbol{\epsilon}$ 来描述。其分量 $\epsilon_{ij}$ 由[位移场](@entry_id:141476) $\mathbf{u}$ 的梯度导出：
$$
\epsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})
$$
其中 $u_{i,j}$ 表示位移分量 $u_i$ 对坐标 $x_j$ 的[偏导数](@entry_id:146280)，即 $\partial u_i / \partial x_j$。对角分量 $\epsilon_{xx}, \epsilon_{yy}, \epsilon_{zz}$ 称为 **[正应变](@entry_id:204633) (normal strains)**，描述了材料沿坐标轴方向的伸长或缩短。非对角分量 $\epsilon_{xy}, \epsilon_{yz}, \epsilon_{zx}$ 称为 **张量[剪应变](@entry_id:175241) (tensorial shear strains)**，描述了初始正交线段之间的角度变化。

一个必须澄清的重要区别在于张量[剪应变](@entry_id:175241)与 **工程[剪应变](@entry_id:175241) (engineering shear strain)** $\gamma_{ij}$ 之间的关系。工程[剪应变](@entry_id:175241)直接表示两条初始正交线段夹角的变化量，其定义为 $\gamma_{ij} = 2\epsilon_{ij}$ (对于 $i \neq j$)。例如，在一个由位移场 $u_x = \alpha y$ 和 $u_y = \beta x$ 描述的均匀变形中，我们首先计算[位移梯度](@entry_id:165352)分量：$u_{x,y} = \alpha$ 和 $u_{y,x} = \beta$。由此，[正应变](@entry_id:204633) $\epsilon_{xx}$ 和 $\epsilon_{yy}$ 均为零，而张量[剪应变](@entry_id:175241) $\epsilon_{xy} = \frac{1}{2}(\alpha + \beta)$。相应的工程[剪应变](@entry_id:175241)为 $\gamma_{xy} = \alpha + \beta$。这个因子 2 的差异至关重要，混淆两者将导致严重的计算错误 [@problem_id:2912295]。

为了直观地理解[应变张量](@entry_id:193332)的变换性质，**[莫尔圆](@entry_id:168131) (Mohr's Circle)** 提供了一个强大的几何工具。对于二维[平面应变](@entry_id:167046)状态，[莫尔圆](@entry_id:168131)在一个以[正应变](@entry_id:204633) $\epsilon_n$为横轴、张量[剪应变](@entry_id:175241) $\epsilon_{s}$ 为纵轴的平面上构建。圆的构建基于一个已知[坐标系](@entry_id:156346)（例如 $x-y$）下的应变分量：$(\epsilon_{xx}, \epsilon_{xy})$ 和 $(\epsilon_{yy}, -\epsilon_{xy})$。连接这两点的线段构成了[莫尔圆](@entry_id:168131)的一条直径。

[莫尔圆](@entry_id:168131)的几何特性蕴含了丰富的物理信息：
- **圆心 (Center)**：圆心的横坐标为 $C = \frac{\epsilon_{xx} + \epsilon_{yy}}{2}$，代表了所有方向上[正应变](@entry_id:204633)的平均值。
- **半径 (Radius)**：圆的半径为 $R = \sqrt{\left(\frac{\epsilon_{xx} - \epsilon_{yy}}{2}\right)^2 + \epsilon_{xy}^2}$，代表了最大张量[剪应变](@entry_id:175241)的大小。

[莫尔圆](@entry_id:168131)上的每一个点都对应着特定方向上的[正应变](@entry_id:204633)和[剪应变](@entry_id:175241)。特别地，圆与横轴的两个交点代表了 **[主应变](@entry_id:197797) (principal strains)**，此时[剪应变](@entry_id:175241)为零。圆的最高点和最低点则对应于最大[剪应变](@entry_id:175241)。

在构建[莫尔圆](@entry_id:168131)时，必须严格使用张量[剪应变](@entry_id:175241) $\epsilon_{xy}$ 作为纵坐标。如果误用工程[剪应变](@entry_id:175241) $\gamma_{xy}$，将会导致对变形状态的严重误判。例如，考虑一个应变状态为 $\epsilon_{xx} = 1.2 \times 10^{-3}$, $\epsilon_{yy} = 4.0 \times 10^{-4}$, $\epsilon_{xy} = 3.0 \times 10^{-4}$ 的例子。正确的[莫尔圆](@entry_id:168131)（使用 $\epsilon_{xy}$）会得到一个半径 $R_T = 5.0 \times 10^{-4}$，从而计算出正确的[主应变](@entry_id:197797) $\epsilon_1 = 1.3 \times 10^{-3}$ 和 $\epsilon_2 = 3.0 \times 10^{-4}$。然而，如果一位分析师误将实验报告中的工程[剪应变](@entry_id:175241) $\gamma_{xy} = 6.0 \times 10^{-4}$ 直接作为纵坐标，他构建的圆半径将变为 $R_G \approx 7.21 \times 10^{-4}$。虽然圆心的位置（平均应变）保持不变，但计算出的“[主应变](@entry_id:197797)”将是错误的，并且对[主方向](@entry_id:276187)的预测也会出现偏差。这个例子清楚地表明，虽然工程[剪应变](@entry_id:175241)在实验测量中很常见，但在[张量分析](@entry_id:161423)和[莫尔圆](@entry_id:168131)构建中，必须统一使用张量[剪应变](@entry_id:175241)，以保证结果的正确性 [@problem_id:2912292]。

### [主应变](@entry_id:197797)与[应变不变量](@entry_id:190518)

虽然[莫尔圆](@entry_id:168131)在二维情况下非常直观，但对于三维应变状态，一个更普适、更根本的方法是将其视为一个代数问题。应变张量 $\boldsymbol{\epsilon}$ 是一个实对称[二阶张量](@entry_id:199780)。根据线性代数中的 **[谱定理](@entry_id:136620) (spectral theorem)**，任何此类张量都存在一个由相互正交的[特征向量](@entry_id:151813)构成的基。在这个特殊的基中，应变张量呈现为对角矩阵形式。这些对角元素就是 **[主应变](@entry_id:197797) (principal strains)** $\epsilon_1, \epsilon_2, \epsilon_3$，而对应的[特征向量](@entry_id:151813)就是 **[主方向](@entry_id:276187) (principal directions)**。在物理上，[主方向](@entry_id:276187)代表了材料内部经历纯拉伸或压缩而无[剪切变形](@entry_id:170920)的方向 [@problem_id:2912268]。

[主应变](@entry_id:197797)是应变状态的内在属性，不随[坐标系](@entry_id:156346)的旋转而改变。与此相关，存在三个标量，它们同样在[坐标系](@entry_id:156346)旋转下保持不变，被称为 **[应变不变量](@entry_id:190518) (strain invariants)**。这三个[不变量](@entry_id:148850)是[应变张量](@entry_id:193332)[特征多项式](@entry_id:150909)的系数。[特征方程](@entry_id:265849) $\det(\boldsymbol{\epsilon} - \lambda \mathbf{I}) = 0$ 可以写作：
$$
\lambda^3 - I_1 \lambda^2 + I_2 \lambda - I_3 = 0
$$
其中，$\lambda$ 的三个根就是三个[主应变](@entry_id:197797) $\epsilon_1, \epsilon_2, \epsilon_3$。

三个[主不变量](@entry_id:193522) $I_1, I_2, I_3$ 可以通过应变张量的分量计算，也可以通过[主应变](@entry_id:197797)计算：
- **第一[不变量](@entry_id:148850) $I_1$**：
  $$I_1 = \mathrm{tr}(\boldsymbol{\epsilon}) = \epsilon_{xx} + \epsilon_{yy} + \epsilon_{zz} = \epsilon_1 + \epsilon_2 + \epsilon_3$$
  $I_1$ 代表了[应变张量](@entry_id:193332)的迹，物理上与材料的体积变化直接相关。

- **第二[不变量](@entry_id:148850) $I_2$**：
  $$I_2 = \frac{1}{2} \left[ (\mathrm{tr}\boldsymbol{\epsilon})^2 - \mathrm{tr}(\boldsymbol{\epsilon}^2) \right] = \epsilon_1\epsilon_2 + \epsilon_2\epsilon_3 + \epsilon_3\epsilon_1$$
  
- **第三[不变量](@entry_id:148850) $I_3$**：
  $$I_3 = \det(\boldsymbol{\epsilon}) = \epsilon_1\epsilon_2\epsilon_3$$
  $I_3$ 代表了应变张量的[行列式](@entry_id:142978)。

这些[不变量](@entry_id:148850)之所以不变，是因为张量的坐标变换 $\boldsymbol{\epsilon}' = \mathbf{Q}\boldsymbol{\epsilon}\mathbf{Q}^T$（其中 $\mathbf{Q}$ 是正交矩阵）是一种相似变换，而[相似变换](@entry_id:152935)不改变矩阵的特征多项式，因此其系数（即[不变量](@entry_id:148850)）和根（即[主应变](@entry_id:197797)）都保持不变 [@problem_id:2912297]。

从根本上说，知道了 $I_1, I_2, I_3$，原则上就可以通过求解上述三次特征方程来确定唯一的一组[主应变](@entry_id:197797) $\{\epsilon_1, \epsilon_2, \epsilon_3\}$。一旦[主应变](@entry_id:197797)被求出，就可以构建三维[莫尔圆](@entry_id:168131)（由三对[主应变](@entry_id:197797)确定三个圆），并从中读出材料在任何方向可能经历的最大张量[剪应变](@entry_id:175241) $\epsilon_{\text{shear,max}} = (\epsilon_{\text{max}} - \epsilon_{\text{min}})/2$。这个过程完全不需要知道主方向的具体方位。然而，需要强调的是，仅凭三个[不变量](@entry_id:148850)无法重构完整的应变张量 $\boldsymbol{\epsilon}$，因为它们不包含任何关于主方向（即[特征向量](@entry_id:151813)）的信息 [@problem_id:2912247]。

### 应变的分解：体积应变与[偏应变](@entry_id:201263)

为了更深刻地理解变形的物理效应，任何应变张量 $\boldsymbol{\epsilon}$ 都可以唯一地分解为一个 **球形 (spherical)** 或 **体积 (volumetric)** 部分 $\boldsymbol{\epsilon}_{\text{vol}}$ 和一个 **偏 (deviatoric)** 部分 $\boldsymbol{\epsilon}'$：
$$
\boldsymbol{\epsilon} = \boldsymbol{\epsilon}_{\text{vol}} + \boldsymbol{\epsilon}'
$$
- **[体积应变](@entry_id:267252)张量** $\boldsymbol{\epsilon}_{\text{vol}}$ 定义为：
  $$
  \boldsymbol{\epsilon}_{\text{vol}} = \frac{1}{3} I_1 \mathbf{I} = \begin{bmatrix} \epsilon_m  0  0 \\ 0  \epsilon_m  0 \\ 0  0  \epsilon_m \end{bmatrix}
  $$
  其中 $\epsilon_m = \frac{I_1}{3} = \frac{\epsilon_{xx}+\epsilon_{yy}+\epsilon_{zz}}{3}$ 是平均[正应变](@entry_id:204633)。该张量描述了一种均匀的、各向同性的膨胀或收缩，它完全承担了材料的体积变化。在一阶近似下，相对体积变化 $\Delta V/V \approx I_1$。

- **偏应变张量** $\boldsymbol{\epsilon}'$ 定义为：
  $$
  \boldsymbol{\epsilon}' = \boldsymbol{\epsilon} - \boldsymbol{\epsilon}_{\text{vol}}
  $$
  偏应变[张量的迹](@entry_id:190669)恒为零，即 $\mathrm{tr}(\boldsymbol{\epsilon}') = 0$。这意味着它所描述的变形不引起体积变化，纯粹是形状的畸变（distortion）。

这种分解在[材料科学](@entry_id:152226)中，特别是在塑性力学中，具有核心地位。许多材料（如金属）的屈服行为主要由形状改变（[偏应变](@entry_id:201263)）引起，而对[静水压力](@entry_id:275365)（体积应变）不敏感。

与偏[应变张量](@entry_id:193332)相关的一个关键[不变量](@entry_id:148850)是其 **第二[不变量](@entry_id:148850) $J_2$**：
$$
J_2 = \frac{1}{2} \boldsymbol{\epsilon}' : \boldsymbol{\epsilon}' = \frac{1}{2} \sum_{i,j} (\epsilon'_{ij})^2
$$
$J_2$ 是偏[应变张量](@entry_id:193332)大小的一种度量，与材料内部储存的[畸变能](@entry_id:198925)密切相关，是著名的 von Mises 屈服准则的核心。一个纯体积应变（例如 $\boldsymbol{\epsilon} = \frac{\kappa}{3}\mathbf{I}$）的[偏应变](@entry_id:201263)部分为零，因此 $J_2 = 0$。相反，一个纯[偏应变](@entry_id:201263)（例如，[主应变](@entry_id:197797)为 $\{2a, -a, -a\}$ 的状态）其 $I_1=0$，而 $J_2$ 不为零（在此例中为 $3a^2$），表明其只包含形状改变 [@problem_id:2912245] [@problem_id:2912280]。

### [不变量](@entry_id:148850)、[应变分解](@entry_id:186005)与[莫尔圆](@entry_id:168131)的内在联系

这些抽象的代数概念在[莫尔圆](@entry_id:168131)的几何图像中有着直观的对应。
- 一个纯体积应变状态，其三个[主应变](@entry_id:197797)相等（$\epsilon_1=\epsilon_2=\epsilon_3=\epsilon_m$）。在莫尔[坐标系](@entry_id:156346)中，这三个点重合，三个[莫尔圆](@entry_id:168131)都退化为[正应变](@entry_id:204633)轴上的一个点。这直观地表明，该状态下任何方向的[剪应变](@entry_id:175241)都为零，没有形状改变，与 $J_2=0$ 的结论一致。
- 一个纯[偏应变](@entry_id:201263)状态，其 $I_1 = \epsilon_1+\epsilon_2+\epsilon_3 = 0$。这意味着三个[主应变](@entry_id:197797)在[正应变](@entry_id:204633)轴上的“[质心](@entry_id:265015)”位于原点。
- 对应变状态施加一个[静水应力](@entry_id:186327)（或应变），即 $\epsilon_i \to \epsilon_i + \beta$，这相当于将[体积应变](@entry_id:267252)部分增加了 $\beta \mathbf{I}$。在[莫尔圆](@entry_id:168131)上，这表现为将三个[主应变](@entry_id:197797)点以及由它们构成的三个[莫尔圆](@entry_id:168131)整体沿[正应变](@entry_id:204633)轴平移了 $\beta$ 的距离。圆的半径和相对位置保持不变。

这一[平移不变性](@entry_id:195885)揭示了 $J_2$ 与[莫尔圆](@entry_id:168131)半径之间的深刻联系。可以证明，$J_2$ 与三个[莫尔圆](@entry_id:168131)的半径 $r_{12}, r_{23}, r_{31}$ 之间存在如下关系：
$$
J_2 = \frac{2}{3} (r_{12}^2 + r_{23}^2 + r_{31}^2)
$$
由于[莫尔圆](@entry_id:168131)的面积 $A_{ij} = \pi r_{ij}^2$，我们也可以得到：
$$
J_2 = \frac{2}{3\pi} (A_{12} + A_{23} + A_{31})
$$
这个关系式 [@problem_id:2912272] 表明，$J_2$ 正比于三个[莫尔圆](@entry_id:168131)面积之和。它为 $J_2$ 提供了一个清晰的几何解释：$J_2$ 是衡量总畸变或总剪切程度的综合指标。当施加一个纯体积应变时，[莫尔圆](@entry_id:168131)只是平移，其半径和面积不变，因此 $J_2$ 保持恒定，这与[偏应变](@entry_id:201263)状态不变的物理事实完全吻合。

### 高等专题与应用

#### 平面应变下的三维剪切

在工程实践中，**平面应变 (plane strain)** 是一种常见的理想化模型，其条件为 $\epsilon_{zz} = \epsilon_{xz} = \epsilon_{yz} = 0$。在这种情况下，[应变张量](@entry_id:193332)简化为：
$$
\boldsymbol{\epsilon} = \begin{pmatrix} \epsilon_{xx}  \epsilon_{xy}  0 \\ \epsilon_{xy}  \epsilon_{yy}  0 \\ 0  0  0 \end{pmatrix}
$$
分析通常集中在 $x-y$ 平面内的二维[莫尔圆](@entry_id:168131)上，其半径 $R_{xy} = \sqrt{(\frac{\epsilon_{xx}-\epsilon_{yy}}{2})^2 + \epsilon_{xy}^2}$ 给出了平面内的最大[剪应变](@entry_id:175241)。然而，这并不一定是整个三维物体所经历的 **绝对最大[剪应变](@entry_id:175241)**。

完整的分析必须考虑所有三个[主应变](@entry_id:197797)。对于平面应变，一个[主方向](@entry_id:276187)始终是 $z$ 轴，其[主应变](@entry_id:197797)为 $\epsilon_3=0$（假设我们以此标记）。另外两个面内[主应变](@entry_id:197797) $\epsilon_a, \epsilon_b$ 由二维问题解出。因此，三维[主应变](@entry_id:197797)集合为 $\{\epsilon_a, \epsilon_b, 0\}$。绝对最大[剪应变](@entry_id:175241)由最大和最小[主应变](@entry_id:197797)之差的一半决定，即 $(\epsilon_{\text{max}} - \epsilon_{\text{min}})/2$。

这里会出现两种情况 [@problem_id:2912294]：
1.  如果面内[主应变](@entry_id:197797) $\epsilon_a$ 和 $\epsilon_b$ 符号相反（一个拉伸，一个压缩），那么它们就是三维的最大和最小[主应变](@entry_id:197797)。此时，绝对最大[剪应变](@entry_id:175241)就等于面内最大[剪应变](@entry_id:175241)。
2.  如果面内[主应变](@entry_id:197797) $\epsilon_a$ 和 $\epsilon_b$ 符号相同（均为拉伸或均为压缩），那么零[主应变](@entry_id:197797) $\epsilon_3=0$ 将成为三个[主应变](@entry_id:197797)中的最大值或最小值之一。例如，若 $\epsilon_a > \epsilon_b > 0$，则三维[主应变](@entry_id:197797)为 $\epsilon_1=\epsilon_a, \epsilon_2=\epsilon_b, \epsilon_3=0$。绝对最大[剪应变](@entry_id:175241)将是 $(\epsilon_1 - \epsilon_3)/2 = \epsilon_a/2$，这大于面内最大[剪应变](@entry_id:175241) $(\epsilon_a - \epsilon_b)/2$。在这种情况下，最大的剪切发生在与 $x-y$ 平面成 45 度的平面上。

这一区别对于基于[最大剪应力理论](@entry_id:190279)（[Tresca准则](@entry_id:167002)）的[材料失效分析](@entry_id:160408)至关重要。忽略第三个[主应变](@entry_id:197797)（即使它为零）可能会低估材料所承受的最大剪切效应，从而导致不安全的设计。

#### 有限应变下的思考

[莫尔圆](@entry_id:168131)及其相关概念是建立在[无穷小应变](@entry_id:197162)理论基础上的。当变形很大，即 **有限应变 (finite strain)** 时，直接应用这些工具会遇到根本性的困难。例如，[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E} = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I})$ 是一个 **物质 (material)** 张量，其分量和主方向定义在变形前的 **参考构型 (reference configuration)** 中。而我们通常观察和测量的是变形后的 **当前构型 (current configuration)**。直接对 $\mathbf{E}$ 的分量画[莫尔圆](@entry_id:168131)，得到的所谓“[主方向](@entry_id:276187)”是在参考构型中的方向，这与当前构型中的物理方向是不同的，两者通过变形梯度 $\mathbf{F}$ 相关联。此外，有限应变不具备线性叠加性。

然而，在处理“大变形背景上的小增量变形”问题时，[莫尔圆](@entry_id:168131)仍然可以被严谨地使用。关键在于将其应用于一个在单一固定构型中定义的、描述增量变形的[对称张量](@entry_id:148092)。存在两种逻辑自洽的途径 [@problem_id:2912248]：

1.  **空间描述 (Spatial Description)**：在当前构型中，增量变形由 **变形率张量 (rate-of-deformation tensor)** $\mathbf{D}$ 描述，它是[速度梯度](@entry_id:261686) $\mathbf{L}$ 的对称部分。$\mathbf{D}$ 是一个定义在当前[构型空间](@entry_id:149531)中的对称张量。因此，可以对 $\mathbf{D}$ 的分量应用[莫尔圆](@entry_id:168131)，以求得[主应变率](@entry_id:264248)及其在 *当前构型* 中的方向。这为分析增量变形的瞬时主导方向提供了有效途径。

2.  **物质描述 (Material Description)**：或者，可以将空间中的变形率张量 $\mathbf{D}$ 通过[拉回](@entry_id:160816) (pull-back) 操作映射回参考构型，得到[格林-拉格朗日应变张量](@entry_id:187745)的率 $\dot{\mathbf{E}} = \mathbf{F}^T \mathbf{D} \mathbf{F}$。$\dot{\mathbf{E}}$ 是一个定义在参考构型中的对称张量。同样，可以对 $\dot{\mathbf{E}}$ 的分量应用[莫尔圆](@entry_id:168131)，以求得主拉格朗日[应变率](@entry_id:154778)及其在 *参考构型* 中的方向。

在这两种方法中，[莫尔圆](@entry_id:168131)都是被正确地应用于一个描述微小增量的对称张量上，而不是被错误地应用于描述两个构型之间总变形的有限应变张量上。这种严谨的应用确保了在复杂的有限变形分析中，我们依然能够借助[莫尔圆](@entry_id:168131)的直观性来理解瞬时的变形特性。