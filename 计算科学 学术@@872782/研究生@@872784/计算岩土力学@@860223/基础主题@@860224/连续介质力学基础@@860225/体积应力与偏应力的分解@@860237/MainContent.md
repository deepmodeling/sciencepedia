## 引言
在现代计算岩土力学和[连续介质力学](@entry_id:155125)领域，体积与偏[应力分解](@entry_id:272862)（Volumetric and Deviatoric Stress Decomposition）是一个基石性的概念。它提出，任何复杂的应力状态都可以被精确地分解为两个物理意义明确且相互正交的分量：一个引起体积变化的**体积应力**和一个引起形状畸变的**[偏应力](@entry_id:163323)**。这种分解远不止是数学上的简化，它深刻揭示了材料在受力时变形的两种基本物理机制，解决了如何从统一的视角理解和量化材料对压缩和剪切两种不同加载模式响应的难题。掌握这一工具，是深入理解材料本构关系、破坏机理以及高级[数值模拟](@entry_id:137087)方法的关键。

本文将系统性地引导您全面掌握体积与偏[应力分解](@entry_id:272862)的理论与实践。在“**原理与机制**”一章中，我们将深入探讨该分解的数学基础、物理诠释，以及它如何与应变能、[应力不变量](@entry_id:170526)和[波的传播](@entry_id:144063)等基本概念紧密相连。随后，在“**应用与跨学科联系**”一章中，我们将视野扩展到广阔的工程与科学领域，展示这一分解在岩土材料破坏、黏弹性建模、[损伤力学](@entry_id:178377)、流固耦合乃至机器学习本构模型等前沿问题中的强大威力。最后，“**动手实践**”部分将提供一系列精心设计的计算练习，帮助您将理论知识转化为解决实际问题的能力。让我们从这一分解的基本原理开始，开启对[材料力学](@entry_id:201885)行为更深层次的探索。

## 原理与机制

在连续介质力学中，理解材料在一般荷载下的力学响应是一项核心任务。任意一个三维应力状态，无论多么复杂，都可以被唯一地分解为两个基本分量：一个引起体积变化的**体积应力**（volumetric stress）分量，和一个引起形状变化的**偏应力**（deviatoric stress）分量。这种分解不仅是一个数学上的便利操作，更深刻地反映了材料变形的内在物理机制。本章将详细阐述该分解的原理，探讨其物理意义，并介绍其在弹性、塑性和[波动力学](@entry_id:166256)中的关键应用。

### 应力的基本分解

考虑一个连续体内的任意一点，其应力状态由柯西应力张量 $\boldsymbol{\sigma}$ 描述。这个二阶对称张量可以被加法分解为一个球形张量（spherical tensor）和一个[偏张量](@entry_id:185837)（deviatoric tensor）。

#### 体积（球形）分量

体积应力分量代表了在所有方向上均等的[法向应力](@entry_id:260622)，即一种静水压力或张力状态。在几何上，唯一在所有[坐标旋转](@entry_id:164444)下都保持不变的二阶张量是单位张量 $\mathbf{I}$。因此，任何各向同性的应力状态都必须与单位张量成正比。我们将体积应力分量记为 $\boldsymbol{\sigma}_{\text{vol}}$，其形式为：

$ \boldsymbol{\sigma}_{\text{vol}} = p\mathbf{I} $

这里的标量 $p$ 是该[静水应力](@entry_id:186327)的大小。为了确定 $p$，我们寻求一个能够客观衡量应力状态“平均”[法向应力](@entry_id:260622)大小的标量。[张量的迹](@entry_id:190669) $\text{tr}(\boldsymbol{\sigma})$ 是一个基本的[标量不变量](@entry_id:193787)，它等于张量对角元素之和，在物理上对应于三个正交方向上法向应力之和。因此，**[平均应力](@entry_id:751819)**（mean stress）被自然地定义为这些[法向应力](@entry_id:260622)的平均值 [@problem_id:3570611]：

$ p = \frac{1}{3} \text{tr}(\boldsymbol{\sigma}) = \frac{1}{3} (\sigma_{xx} + \sigma_{yy} + \sigma_{zz}) $

在岩土力学中，通常采用压应力为正的符号约定。因此，一个正的 $p$ 值表示该点处于平均受压状态。这个标量 $p$ 是驱动材料体积变化的主要因素。

#### [偏应力](@entry_id:163323)分量

偏应力分量 $\mathbf{s}$ 被定义为从总[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 中减去[体积分](@entry_id:171119)量后剩余的部分：

$ \mathbf{s} = \boldsymbol{\sigma} - \boldsymbol{\sigma}_{\text{vol}} = \boldsymbol{\sigma} - p\mathbf{I} $

将 $p$ 的定义代入，我们得到：

$ \mathbf{s} = \boldsymbol{\sigma} - \left(\frac{1}{3}\text{tr}(\boldsymbol{\sigma})\right)\mathbf{I} $

[偏应力张量](@entry_id:267642)的一个决定性特征是其迹为零。我们可以利用[迹算子](@entry_id:183665)的线性和 $\text{tr}(\mathbf{I})=3$ 这一事实来验证这一点 [@problem_id:2612528]：

$ \text{tr}(\mathbf{s}) = \text{tr}(\boldsymbol{\sigma} - p\mathbf{I}) = \text{tr}(\boldsymbol{\sigma}) - \text{tr}(p\mathbf{I}) = \text{tr}(\boldsymbol{\sigma}) - p \cdot \text{tr}(\mathbf{I}) $

$ \text{tr}(\mathbf{s}) = \text{tr}(\boldsymbol{\sigma}) - \left(\frac{1}{3}\text{tr}(\boldsymbol{\sigma})\right)(3) = \text{tr}(\boldsymbol{\sigma}) - \text{tr}(\boldsymbol{\sigma}) = 0 $

由于 $\text{tr}(\mathbf{s})=0$，偏应力代表了一种纯剪切状态，它不贡献于平均[法向应力](@entry_id:260622)。它包含了所有的剪应力分量以及[法向应力](@entry_id:260622)分量相对于平均应力的偏差。

#### 分量形式的计算

为了在实际计算中应用这一分解，我们可以写出[偏应力张量](@entry_id:267642)各个分量的表达式。给定一个对称的柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ [@problem_id:3570617]：

$$ \boldsymbol{\sigma} = \begin{pmatrix} \sigma_{xx}  \sigma_{xy}  \sigma_{xz} \\ \sigma_{yx}  \sigma_{yy}  \sigma_{yz} \\ \sigma_{zx}  \sigma_{zy}  \sigma_{zz} \end{pmatrix} $$

[偏应力张量](@entry_id:267642) $\mathbf{s}$ 的对角分量为：

$ s_{xx} = \sigma_{xx} - p = \sigma_{xx} - \frac{1}{3}(\sigma_{xx} + \sigma_{yy} + \sigma_{zz}) = \frac{2}{3}\sigma_{xx} - \frac{1}{3}\sigma_{yy} - \frac{1}{3}\sigma_{zz} $

$ s_{yy} = \sigma_{yy} - p = \sigma_{yy} - \frac{1}{3}(\sigma_{xx} + \sigma_{yy} + \sigma_{zz}) = -\frac{1}{3}\sigma_{xx} + \frac{2}{3}\sigma_{yy} - \frac{1}{3}\sigma_{zz} $

$ s_{zz} = \sigma_{zz} - p = \sigma_{zz} - \frac{1}{3}(\sigma_{xx} + \sigma_{yy} + \sigma_{zz}) = -\frac{1}{3}\sigma_{xx} - \frac{1}{3}\sigma_{yy} + \frac{2}{3}\sigma_{zz} $

而非对角分量（剪应力分量）则保持不变，因为单位张量 $\mathbf{I}$ 的非对角分量为零：

$ s_{xy} = \sigma_{xy}, \quad s_{xz} = \sigma_{xz}, \quad s_{yz} = \sigma_{yz} $

这一分解是纯数学操作，对于任何二阶张量都是唯一的，不依赖于材料的本构性质（例如，各向同性或各向异性）。

### 物理诠释与弹性响应

[应力分解](@entry_id:272862)的巨大威力在于，对于[各向同性线弹性](@entry_id:185899)材料，其应变响应也相应地解耦。

#### 弹性响应的[解耦](@entry_id:637294)

与[应力分解](@entry_id:272862)类似，[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 也可以分解为[体积应变](@entry_id:267252) $\epsilon_v$ 和[偏应变](@entry_id:201263) $\mathbf{e}$：

$ \epsilon_v = \text{tr}(\boldsymbol{\varepsilon}) $

$ \mathbf{e} = \boldsymbol{\varepsilon} - \frac{1}{3}\epsilon_v \mathbf{I} $

对于[各向同性线弹性](@entry_id:185899)材料，其本构关系可以用两个[弹性模量](@entry_id:198862)——**体积模量** $K$ 和**[剪切模量](@entry_id:167228)** $G$——来简洁地表达，这两个模量分别独立地关联着应力和应变的体积部分与[偏应力](@entry_id:163323)部分 [@problem_id:3570637]：

$ p = K \epsilon_v $

$ \mathbf{s} = 2G \mathbf{e} $

这个解耦的[本构关系](@entry_id:186508)表明，体积应力仅引起体积应变（体积变化），而偏应力仅引起[偏应变](@entry_id:201263)（形状变化）。$K$ 衡量材料抵[抗体](@entry_id:146805)积变化的能力，而 $G$ 衡量材料抵抗形状变化（[剪切变形](@entry_id:170920)）的能力。

#### [应变能](@entry_id:162699)的分解

这种[解耦](@entry_id:637294)特性同样体现在[应变能密度](@entry_id:200085) $W$ 上。对于线弹性材料，$W = \frac{1}{2}\boldsymbol{\sigma}:\boldsymbol{\varepsilon}$。将应力和应变都进行分解：

$ W = \frac{1}{2}(p\mathbf{I} + \mathbf{s}) : (\frac{1}{3}\epsilon_v \mathbf{I} + \mathbf{e}) $

展开后，交叉项 $(p\mathbf{I}):\mathbf{e}$ 和 $\mathbf{s}:(\frac{1}{3}\epsilon_v \mathbf{I})$ 均为零，因为球形张量和[偏张量](@entry_id:185837)的[双点积](@entry_id:748648)为零。因此，[应变能密度](@entry_id:200085)也干净地分解为体积应变能和[偏应变](@entry_id:201263)能两部分 [@problem_id:3570637] [@problem_id:3570662]：

$ W = W_v + W_d = \frac{1}{2} p \epsilon_v + \frac{1}{2} \mathbf{s}:\mathbf{e} $

利用[解耦](@entry_id:637294)的[本构关系](@entry_id:186508)，可以将其表达为纯应力或纯应变的形式：

$ W = \frac{1}{2K} p^2 + \frac{1}{4G} \mathbf{s}:\mathbf{s} = \frac{1}{2} K \epsilon_v^2 + G \mathbf{e}:\mathbf{e} $

这个能量的加法分解是体积-偏[应力分解](@entry_id:272862)物理意义的深刻体现。例如，在纯[静水压力](@entry_id:275365)加载下 ($\mathbf{s}=\mathbf{0}$)，所有[应变能](@entry_id:162699)都存储为[体积应变](@entry_id:267252)能 $W_v$。在纯剪切加载下 ($p=0$)，所有[应变能](@entry_id:162699)都存储为[偏应变](@entry_id:201263)能（或称[畸变能](@entry_id:198925)）$W_d$。

#### 实例分析：单轴应力状态

为了更深入地理解 $K$ 和 $G$ 的物理意义，我们考虑一个简单的[单轴拉伸](@entry_id:188287)（或压缩）状态，[应力张量](@entry_id:148973)为 $\boldsymbol{\sigma} = \sigma \mathbf{e}_1 \otimes \mathbf{e}_1$ [@problem_id:2680061]。

首先分解应力：
平均应力 $p = \frac{1}{3}\text{tr}(\boldsymbol{\sigma}) = \frac{\sigma}{3}$。
[偏应力张量](@entry_id:267642) $\mathbf{s} = \boldsymbol{\sigma} - p\mathbf{I} = \text{diag}(\frac{2\sigma}{3}, -\frac{\sigma}{3}, -\frac{\sigma}{3})$。

然后，利用[解耦](@entry_id:637294)的本构关系求解应变。
体积应变 $\epsilon_v = p/K = \sigma/(3K)$。
[偏应变](@entry_id:201263) $\mathbf{e} = \mathbf{s}/(2G) = \frac{1}{2G}\text{diag}(\frac{2\sigma}{3}, -\frac{\sigma}{3}, -\frac{\sigma}{3})$。

最后，通过 $\boldsymbol{\varepsilon} = \mathbf{e} + \frac{1}{3}\epsilon_v\mathbf{I}$ 合成总应变，得到[轴向应变](@entry_id:160811) $\varepsilon_{11}$ 和[横向应变](@entry_id:157965) $\varepsilon_{22}$：

$ \varepsilon_{11} = e_{11} + \frac{1}{3}\epsilon_v = \frac{2\sigma}{3 \cdot 2G} + \frac{1}{3}\frac{\sigma}{3K} = \sigma \left( \frac{1}{3G} + \frac{1}{9K} \right) $

$ \varepsilon_{22} = e_{22} + \frac{1}{3}\epsilon_v = -\frac{\sigma}{3 \cdot 2G} + \frac{1}{3}\frac{\sigma}{3K} = \sigma \left( \frac{1}{9K} - \frac{1}{6G} \right) $

这个结果完全用 $K$ 和 $G$ 表达了材料在单轴应力下的行为。我们可以考察其极限情况：
- **不可压缩极限** ($K \to \infty$): [体积应变](@entry_id:267252)为 $\epsilon_v = \sigma/(3K) \to 0$，材料体积不变。此时，$\varepsilon_{11} \to \sigma/(3G)$，$\varepsilon_{22} \to -\sigma/(6G)$。[横向应变](@entry_id:157965)与[轴向应变](@entry_id:160811)之比（[泊松比](@entry_id:158876) $\nu$）为 $-\varepsilon_{22}/\varepsilon_{11} = 0.5$，这正是[不可压缩材料](@entry_id:159741)的理论值。
- **流体极限** ($G \to 0$): 材料失去抗剪切能力。由于单轴应力包含非零的[偏应力](@entry_id:163323)分量，当 $G \to 0$ 时，[偏应变](@entry_id:201263) $\mathbf{e}$ 将趋于无穷大，导致总应变发散。这表明，没有剪切刚度的材料（如理想流体）无法在静止状态下承受任何偏应力。

### [不变量](@entry_id:148850)与坐标无关的应力度量

应力张量的分量依赖于[坐标系](@entry_id:156346)的选择。为了建立普适的材料模型（如[屈服准则](@entry_id:193897)），我们需要不随[坐标系](@entry_id:156346)旋转而改变的标量，即**[不变量](@entry_id:148850)**。体积-偏[应力分解](@entry_id:272862)为定义这些[不变量](@entry_id:148850)提供了一个自然框架。

#### [应力不变量](@entry_id:170526) $I_1, J_2, J_3$

通常使用三个[主不变量](@entry_id:193522)来完全描述一个应力状态的大小，而不涉及其方向。一种常用的[不变量](@entry_id:148850)组合是：
- **第一[应力不变量](@entry_id:170526) ($I_1$)**: 这是总[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的迹，直接关联到[平均应力](@entry_id:751819) $p$。
  $ I_1 = \text{tr}(\boldsymbol{\sigma}) = \sigma_1 + \sigma_2 + \sigma_3 $
  其中 $\sigma_1, \sigma_2, \sigma_3$ 是主应力。$p = I_1/3$。

- **第二偏[应力[不变](@entry_id:170526)量](@entry_id:148850) ($J_2$)**: 这是[偏应力张量](@entry_id:267642) $\mathbf{s}$ 的第二[不变量](@entry_id:148850)，定义为 [@problem_id:3570657]：
  $ J_2 = \frac{1}{2} \mathbf{s}:\mathbf{s} = \frac{1}{2} \sum_{i,j} s_{ij}^2 $
  $J_2$ 与[畸变能](@entry_id:198925)密度直接相关 ($W_d = J_2/G$)，因此它是一个衡量偏应力大小或剪切效应强度的关键指标。它也可以用[主应力](@entry_id:176761)表示：
  $ J_2 = \frac{1}{6} [(\sigma_1 - \sigma_2)^2 + (\sigma_2 - \sigma_3)^2 + (\sigma_3 - \sigma_1)^2] $

- **第三偏[应力[不变](@entry_id:170526)量](@entry_id:148850) ($J_3$)**: 这是[偏应力张量](@entry_id:267642) $\mathbf{s}$ 的[行列式](@entry_id:142978)：
  $ J_3 = \det(\mathbf{s}) = s_1 s_2 s_3 $
  其中 $s_1, s_2, s_3$ 是主偏应力。$J_3$ 描述了应力状态在偏平面（deviatoric plane）上的模式，例如，它能区分三轴压缩和三轴拉伸状态。

这组[不变量](@entry_id:148850) $(I_1, J_2, J_3)$ 或等价的 $(p, J_2, J_3)$ 能够唯一地确定三个主应力的大小，但丢弃了[主应力方向](@entry_id:753737)的信息。

#### [等效应力](@entry_id:749064) $q$

在[金属塑性](@entry_id:176585)以及岩土力学的许多模型中，一个特别重要的标量是 **von Mises [等效应力](@entry_id:749064)**，通常记为 $q$。它直接由 $J_2$ 定义，作为[偏应力](@entry_id:163323)大小的度量 [@problem_id:3570621]：

$ q = \sqrt{3J_2} = \sqrt{\frac{1}{2} [(\sigma_1 - \sigma_2)^2 + (\sigma_2 - \sigma_3)^2 + (\sigma_3 - \sigma_1)^2]} $

由于 $q$ 仅依赖于 $J_2$，而 $J_2$ 完全由[偏应力](@entry_id:163323) $\mathbf{s}$ 定义，所以 $q$ 是一个纯粹的偏应力度量，与[静水压力](@entry_id:275365) $p$ 无关。许多材料的屈服行为主要由 $q$ 控制，而受 $p$ 的影响较小（或以不同的方式影响）。

**计算示例**: 考虑一个主应力状态为 $(\sigma_1, \sigma_2, \sigma_3) = (140, 80, 50)$ MPa [@problem_id:3570621]。
- $I_1 = 140 + 80 + 50 = 270$ MPa
- $p = I_1/3 = 90$ MPa
- 主偏应力为 $(s_1, s_2, s_3) = (140-90, 80-90, 50-90) = (50, -10, -40)$ MPa
- $J_2 = \frac{1}{2}(50^2 + (-10)^2 + (-40)^2) = \frac{1}{2}(2500+100+1600) = 2100$ MPa$^2$
- $J_3 = (50)(-10)(-40) = 20000$ MPa$^3$
- $q = \sqrt{3 \times 2100} = \sqrt{6300} = 30\sqrt{7}$ MPa

### 高级原理与应用

体积-偏[应力分解](@entry_id:272862)的框架在理论和计算力学的许多高级领域中都至关重要。

#### 正交性与功的分解

从更形式化的几何角度看，[体积分](@entry_id:171119)量 $p\mathbf{I}$ 和偏应力分量 $\mathbf{s}$ 在[张量内积](@entry_id:190619)空间中是**正交**的。这个[内积](@entry_id:158127)由[双点积](@entry_id:748648)定义，正交性意味着 [@problem_id:2612528]：

$ \boldsymbol{\sigma}_{\text{vol}} : \mathbf{s} = (p\mathbf{I}) : \mathbf{s} = p(\mathbf{I}:\mathbf{s}) = p \cdot \text{tr}(\mathbf{s}) = 0 $

这种正交性的一个直接且重要的推论是内功率率（单位体积的功率）的分解。内功率率 $\dot{W} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}$，其中 $\dot{\boldsymbol{\varepsilon}}$ 是[应变率张量](@entry_id:266108)。将应力和[应变率](@entry_id:154778)都进行分解，由于交叉项为零，我们得到：

$ \dot{W} = (p\mathbf{I} + \mathbf{s}) : (\frac{1}{3}\dot{\epsilon}_v \mathbf{I} + \dot{\mathbf{e}}) = p\dot{\epsilon}_v + \mathbf{s}:\dot{\mathbf{e}} $

内功率率完美地分解为体积变化功率 $p\dot{\epsilon}_v$ 和形状变化功率 $\mathbf{s}:\dot{\mathbf{e}}$。这在塑性理论中尤其重要，因为它将与体积变化（如[压实](@entry_id:161543)）相关的功和与剪切滑移（塑性流动）相关的功分离开来。

#### [偏应力](@entry_id:163323)投影算子

分解过程可以被抽象为一个线性算子。我们可以定义一个四阶**[偏应力](@entry_id:163323)[投影算子](@entry_id:154142)** $\mathbb{P}_{\text{dev}}$，它将任何二阶张量投影到其偏应力部分 [@problem_id:3570673]。这个算子由四阶单位张量 $\mathbb{I}$ 和二阶单位张量 $\mathbf{I}$ 的张量积构成：

$ \mathbb{P}_{\text{dev}} = \mathbb{I} - \frac{1}{3} \mathbf{I} \otimes \mathbf{I} $

将此算子作用于任意[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$，即可得到其[偏应力](@entry_id:163323)部分：

$ \mathbf{s} = \mathbb{P}_{\text{dev}} : \boldsymbol{\sigma} $

这个算子是**幂等**的 ($\mathbb{P}_{\text{dev}} : \mathbb{P}_{\text{dev}} = \mathbb{P}_{\text{dev}}$)，意味着对一个已经是[偏张量](@entry_id:185837)的张量进行投影不会改变它。这种算子形式的表述在有限元方法的现代本构模型实现中是标准语言。

#### 在[弹性动力学](@entry_id:175818)中的应用：波的传播

体积-偏[应力分解](@entry_id:272862)的物理真实性在[弹性波传播](@entry_id:201422)中得到了最鲜明的体现。[各向同性弹性](@entry_id:203237)体中的运动方程（[Navier-Cauchy方程](@entry_id:189211)）可以通过对其取[散度和旋度](@entry_id:270881)进行分解 [@problem_id:3570662]。
- 对运动方程取**散度**，可以得到一个关于位移场散度（即[体积应变](@entry_id:267252) $\epsilon_v$）的标量[波动方程](@entry_id:139839)。[波的传播](@entry_id:144063)速度仅由[体积模量](@entry_id:160069) $K$、[剪切模量](@entry_id:167228) $G$ 和密度 $\rho$ 决定。这就是**纵波（[P波](@entry_id:178440)）**，其速度为：
  $ c_P = \sqrt{\frac{K + \frac{4}{3}G}{\rho}} $
- 对[运动方程](@entry_id:170720)取**旋度**，可以得到一个关于位移场旋度的矢量波动方程。[波的传播](@entry_id:144063)速度仅由剪切模量 $G$ 和密度 $\rho$ 决定。这就是**横波（[S波](@entry_id:174890)）**，其速度为：
  $ c_S = \sqrt{\frac{G}{\rho}} $

[P波](@entry_id:178440)本质上是体积变化的传播（[压缩波](@entry_id:747596)），其速度依赖于材料的体积刚度 $K$ 和剪切刚度 $G$。而[S波](@entry_id:174890)是形状变化的传播（剪切波），其速度仅依赖于材料的剪切刚度 $G$。理想流体中 $G=0$，因此S波无法在其中传播。这一现象有力地证明了体积变形和[剪切变形](@entry_id:170920)是两种独立的物理机制。

#### 有限元计算中的考量

尽管体积-偏[应力分解](@entry_id:272862)在理论上是点态唯一的，但在有限元等数值计算的实践中，处理方式的差异可能导致结果不同。特别是在计算单元平均量时，运算的顺序很重要 [@problem_id:3570655]。

考虑计算单元平均的第二偏[应力[不变](@entry_id:170526)量](@entry_id:148850) $J_2$。有两种路径：
1.  **先平均后分解 (Project-after-average)**：先计算单元内应力张量的平均值 $\overline{\boldsymbol{\sigma}}$，然后分解 $\overline{\boldsymbol{\sigma}}$ 得到平均[偏应力](@entry_id:163323) $\overline{\mathbf{s}}$，最后计算 $J_{2,P} = \frac{1}{2}\overline{\mathbf{s}}:\overline{\mathbf{s}}$。
2.  **先分解后平均 (Average-after-project)**：在每个积分点上计算[偏应力](@entry_id:163323) $\mathbf{s}$ 和 $J_2$，然后计算 $J_2$ 在单元内的平均值 $\overline{J_2}$，记为 $J_{2,I}$。

由于 $J_2$ 是 $\mathbf{s}$ 的二次（[非线性](@entry_id:637147)）函数，根据延森不等式，$\overline{f(x)} \ge f(\overline{x})$，我们有 $J_{2,I} \ge J_{2,P}$。等号仅在偏应力场 $\mathbf{s}$ 在单元内为常数时成立。对于非均匀应[力场](@entry_id:147325)（例如，由高阶位移场引起或在扭曲的单元上），这两种计算路径会给出不同的结果。理解这种差异对于准确解释和后处理[非线性有限元分析](@entry_id:167596)的结果至关重要。