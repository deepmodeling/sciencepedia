## 引言
在连续介质力学中，描述材料内部某一点受力情况的物理量是[应力张量](@entry_id:148973)。然而，[应力张量](@entry_id:148973)的分量值并非绝对，而是依赖于我们观察和测量时所选定的[坐标系](@entry_id:156346)。这一事实引出了一个根本性问题：我们如何将在一个[坐标系](@entry_id:156346)下描述的应力状态，准确地转换到另一个任意旋转的[坐标系](@entry_id:156346)中？这一过程，即应力变换，是理解应力状态内在物理特性的关键。它允许我们超越[坐标系](@entry_id:156346)的束缚，去探寻那些不随观察角度而改变的量，例如材料所能承受的最大拉应力或[最大剪应力](@entry_id:181794)，这些量直接关系到材料的强度、屈服与断裂。本文旨在系统地阐述应力变换的理论及其在工程与科学中的应用。

在接下来的内容中，我们将分三个章节展开探讨。第一章**“原理与机制”**将深入力学核心，从[张量变换](@entry_id:183453)的数学法则出发，揭示[主应力与主方向](@entry_id:193792)作为本征值问题的本质，并详细介绍强大的可视化工具——[莫尔圆](@entry_id:168131)。第二章**“应用与跨学科联系”**将理论与实践相结合，展示这些原理如何在实验力学、[材料失效分析](@entry_id:160408)（涵盖金属、岩土等）、以及[各向异性材料](@entry_id:184874)力学等领域发挥关键作用。最后，在第三章**“动手实践”**中，我们将通过一系列精心设计的问题，帮助您巩固和深化对这些核心概念的理解与应用能力。通过本次学习，您将构建起一个从抽象理论到具体应用的完整知识体系。

## 原理与机制

在对一个点处的应力状态进行表征时，我们所用的[应力张量](@entry_id:148973)分量取决于我们选择的[坐标系](@entry_id:156346)。这是一个根本性的观察，它引出了连续介质力学中的一个核心问题：如果我们知道了在一个[坐标系](@entry_id:156346)下的应力分量，我们如何确定在任意一个旋转后的新[坐标系](@entry_id:156346)下的应力分量？这个过程被称为**应力变换**。理解应力变换不仅对于在不同[坐标系](@entry_id:156346)下表达应力至关重要，它还能揭示应力状态的内在、不依赖于[坐标系](@entry_id:156346)的物理特性。

### 应力[张量变换法则](@entry_id:185176)

为了推导变换法则，我们可以考虑两种等效的观点：一种是**被动变换**，即物理状态保持不变，我们仅仅是旋转了描述它的[坐标基](@entry_id:270149)；另一种是**主动变换**，即[坐标基](@entry_id:270149)保持不变，而材料单元连同其应力状态一起发生刚性旋转 [@problem_id:2921249]。

让我们考虑一个被动的基变换。设原始[坐标基](@entry_id:270149)为 $\{\mathbf{e}_1, \mathbf{e}_2, \mathbf{e}_3\}$，新[坐标基](@entry_id:270149)为 $\{\mathbf{e}'_1, \mathbf{e}'_2, \mathbf{e}'_3\}$。这两个基通过一个正交[旋转张量](@entry_id:191990) $\mathbf{Q}$ 联系，使得 $\mathbf{e}'_i = \mathbf{Q} \mathbf{e}_i$。根据矢量变换法则，任何矢量（如法向量 $\mathbf{n}$ 和牵[引力](@entry_id:175476)矢量 $\mathbf{t}$）在新旧[坐标系](@entry_id:156346)下的分量表示是相关的，关系为 $\mathbf{n}' = \mathbf{Q}^\top \mathbf{n}$ 和 $\mathbf{t}' = \mathbf{Q}^\top \mathbf{t}$。

Cauchy 应力关系 $\mathbf{t} = \boldsymbol{\sigma} \mathbf{n}$ 是一个物理定律，它必须在所有[坐标系](@entry_id:156346)下都成立。在新的[坐标系](@entry_id:156346)中，它写作 $\mathbf{t}' = \boldsymbol{\sigma}' \mathbf{n}'$，其中 $\boldsymbol{\sigma}'$ 是应力张量在新基下的分量矩阵。将矢量变换关系代入，我们得到：

$\mathbf{Q}^\top \mathbf{t} = \boldsymbol{\sigma}' (\mathbf{Q}^\top \mathbf{n})$

将原始的 Cauchy 关系 $\mathbf{t} = \boldsymbol{\sigma} \mathbf{n}$ 代入上式左侧：

$\mathbf{Q}^\top (\boldsymbol{\sigma} \mathbf{n}) = \boldsymbol{\sigma}' \mathbf{Q}^\top \mathbf{n}$

由于这个方程对任意[法向量](@entry_id:264185) $\mathbf{n}$ 都必须成立，我们可以得到算子之间的关系：$\mathbf{Q}^\top \boldsymbol{\sigma} = \boldsymbol{\sigma}' \mathbf{Q}^\top$。用 $\mathbf{Q}$ 右乘方程两边，并利用其正交性 ($\mathbf{Q}^\top \mathbf{Q} = \mathbf{I}$)，我们得到应力张量的被动变换法则：

$$
\boldsymbol{\sigma}' = \mathbf{Q}^\top \boldsymbol{\sigma} \mathbf{Q}
$$

这个公式是所有二阶张量在基变换下的统一定义。它表明，新[坐标系](@entry_id:156346)下的应力分量是旧分量通过与旋转矩阵的预乘和后乘而获得的。值得注意的是，主动旋转（即应[力场](@entry_id:147325)本身旋转 $\mathbf{Q}$）会得到一个相关的变换法则 $\boldsymbol{\sigma}^{\text{rot}} = \mathbf{Q} \boldsymbol{\sigma} \mathbf{Q}^\top$ [@problem_id:2921249]。尽管这两个矩阵 $\boldsymbol{\sigma}'$ 和 $\boldsymbol{\sigma}^{\text{rot}}$ 通常是不同的，但它们都代表了相同的内在物理状态，只是从不同视角观察而已。

### [主应力与主方向](@entry_id:193792)：一个[本征值问题](@entry_id:142153)

尽管应力分量随[坐标系](@entry_id:156346)而变，但应力状态的某些内在特征是恒定的。这引出了一个关键问题：是否存在某些特殊的平面，其上的应力作用最为简单？具体来说，是否存在一些平面，其上的牵[引力](@entry_id:175476)矢量 $\mathbf{t}$ 完全垂直于该平面？

在这样的平面上，剪切应力分量为零。这些平面被称为**[主平面](@entry_id:164488)**，其法线方向被称为**[主方向](@entry_id:276187)**。作用在[主平面](@entry_id:164488)上的[正应力](@entry_id:260622)被称为**主应力**。这个物理定义可以直接翻译成一个深刻的数学陈述 [@problem_id:2690989]。如果牵[引力](@entry_id:175476) $\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n}$ 与法向量 $\mathbf{n}$ 共线，那么必然存在一个标量 $\lambda$ 使得：

$$
\boldsymbol{\sigma} \mathbf{n} = \lambda \mathbf{n}
$$

这正是线性代数中的**本征值问题**。因此，主应力就是应力张量 $\boldsymbol{\sigma}$ 的**[本征值](@entry_id:154894)**，而主方向就是对应的**本征矢量**。

由于角动量守恒（在无[体力](@entry_id:174230)矩的情况下），Cauchy 应力张量 $\boldsymbol{\sigma}$ 是对称的。这个对称性具有至关重要的后果，这由**[谱定理](@entry_id:136620)**所保证：

1.  一个实[对称张量](@entry_id:148092)的所有[本征值](@entry_id:154894)（[主应力](@entry_id:176761)）都是实数。
2.  总能找到一组三个相互正交的本征矢量（主方向），它们构成一个完整的[标准正交基](@entry_id:147779)。

这意味着在任何一点，无论应力状态多么复杂，我们总能找到一个由[主方向](@entry_id:276187)构成的[坐标系](@entry_id:156346)。在这个**主[坐标系](@entry_id:156346)**中，应力张量的矩阵表示是[对角化](@entry_id:147016)的，其对角[线元](@entry_id:196833)素就是三个[主应力](@entry_id:176761) $\sigma_1, \sigma_2, \sigma_3$。

$$
\boldsymbol{\sigma}' = \begin{pmatrix} \sigma_1 & 0 & 0 \\ 0 & \sigma_2 & 0 \\ 0 & 0 & \sigma_3 \end{pmatrix}
$$

这是该应力状态的最简表示，完全由三个正应力描述，所有剪应力分量都为零。

### [主应力](@entry_id:176761)的求解与诠释

#### 特征方程与[应力不变量](@entry_id:170526)

求解本征值问题的标准方法是求解[特征方程](@entry_id:265849)。方程 $(\boldsymbol{\sigma} - \lambda \mathbf{I})\mathbf{n} = \mathbf{0}$ 要有非零解 $\mathbf{n}$，其系数矩阵的[行列式](@entry_id:142978)必须为零：

$$
\det(\boldsymbol{\sigma} - \lambda \mathbf{I}) = 0
$$

将这个[行列式](@entry_id:142978)展开会得到一个关于 $\lambda$ 的三次多项式 [@problem_id:2690989]：

$$
-\lambda^3 + I_1 \lambda^2 - I_2 \lambda + I_3 = 0
$$

这个方程的三个根就是三个[主应力](@entry_id:176761) $\sigma_1, \sigma_2, \sigma_3$。方程的系数 $I_1, I_2, I_3$ 被称为**主[应力[不变](@entry_id:170526)量](@entry_id:148850)**，因为它们的值不随[坐标系](@entry_id:156346)的旋转而改变。它们是应力状态的内在属性。这些[不变量](@entry_id:148850)可以用任意[坐标系](@entry_id:156346)下的应力分量计算：

$I_1 = \mathrm{tr}(\boldsymbol{\sigma}) = \sigma_{xx} + \sigma_{yy} + \sigma_{zz}$

$I_2 = \frac{1}{2}[(\mathrm{tr}(\boldsymbol{\sigma}))^2 - \mathrm{tr}(\boldsymbol{\sigma}^2)] = \sigma_{xx}\sigma_{yy} + \sigma_{yy}\sigma_{zz} + \sigma_{zz}\sigma_{xx} - \tau_{xy}^2 - \tau_{yz}^2 - \tau_{zx}^2$

$I_3 = \det(\boldsymbol{\sigma})$

一旦求得主应力，[不变量](@entry_id:148850)也可以用更简单的形式表示：

$I_1 = \sigma_1 + \sigma_2 + \sigma_3$

$I_2 = \sigma_1\sigma_2 + \sigma_2\sigma_3 + \sigma_3\sigma_1$

$I_3 = \sigma_1\sigma_2\sigma_3$

#### 变分原理：正应力的极值

主应力有一个非常直观的物理意义：它们是作用在材料点所有可能平面上的[正应力](@entry_id:260622)的极值（最大值、最小值和[鞍点](@entry_id:142576)值）[@problem_id:2690989]。我们可以通过求解一个约束[极值](@entry_id:145933)问题来证明这一点：在所有[单位法向量](@entry_id:178851) $\mathbf{n}$（满足约束 $\mathbf{n} \cdot \mathbf{n} = 1$）中，找到使[正应力](@entry_id:260622) $\sigma_n(\mathbf{n}) = \mathbf{n}^\top \boldsymbol{\sigma} \mathbf{n}$ 取[极值](@entry_id:145933)的方向。

使用拉格朗日乘子法，我们发现[极值](@entry_id:145933)条件恰好就是[本征值方程](@entry_id:192306) $\boldsymbol{\sigma}\mathbf{n} = \lambda\mathbf{n}$ [@problem_id:2921224]。这证实了使[正应力](@entry_id:260622)达到极值的方向就是[主方向](@entry_id:276187)，而这些[极值](@entry_id:145933)本身就是[主应力](@entry_id:176761)。

更进一步，我们可以证明，在这些正应力取极值的平面上，剪应力必然为零。对于二维平面应力状态，我们可以显式地推导[正应力](@entry_id:260622) $\sigma_n$ 和剪应力 $\tau_n$ 随平面[方位角](@entry_id:164011) $\theta$ 的变化关系。对 $\sigma_n(\theta)$ 求导可以得到一个优美的关系 [@problem_id:2921224]：

$$
\frac{d\sigma_n}{d\theta} = 2\tau_n(\theta)
$$

这个方程清楚地表明，当[正应力](@entry_id:260622) $\sigma_n$ 达到极值时（即 $\frac{d\sigma_n}{d\theta} = 0$），该平面上的剪应力 $\tau_n$ 必须为零。这两种定义主应力的方法——零剪应力平面和正应力极值平面——是完全等价的。

### [静水应力](@entry_id:186327)与偏[应力分解](@entry_id:272862)

为了更好地理解应力状态的不同物理效应，将应力张量分解为其**静水**部分和**偏**部分是极其有用的。

$$
\boldsymbol{\sigma} = \mathbf{s} + p\mathbf{I}
$$

这里，$p = \frac{1}{3}I_1 = \frac{1}{3}(\sigma_{xx}+\sigma_{yy}+\sigma_{zz})$ 是**平均[正应力](@entry_id:260622)**或**[静水应力](@entry_id:186327)**。[静水应力](@entry_id:186327)部分 $p\mathbf{I}$ 引起材料的体积变化（膨胀或压缩），但不改变其形状。

剩下的部分 $\mathbf{s} = \boldsymbol{\sigma} - p\mathbf{I}$ 被称为**[偏应力张量](@entry_id:267642)**。它完全负责材料的形状改变（畸变或剪切变形）。[偏应力张量](@entry_id:267642)也有它自己的一组[不变量](@entry_id:148850)，通常记为 $J_1, J_2, J_3$。根据其定义，第一个[不变量](@entry_id:148850) $J_1 = \mathrm{tr}(\mathbf{s})$ 恒等于零。

第二个[不变量](@entry_id:148850) $J_2$ 和第三个[不变量](@entry_id:148850) $J_3$ 在[材料科学](@entry_id:152226)和工程中尤为重要 [@problem_id:2921230] [@problem_id:2921246]。

**$J_2$：** 第二偏[应力[不变](@entry_id:170526)量](@entry_id:148850)定义为 $J_2 = \frac{1}{2}\mathbf{s}:\mathbf{s} = \frac{1}{2}s_{ij}s_{ji}$。它代表了[剪切变形](@entry_id:170920)强度的一个度量，并与储存在材料中的[畸变能](@entry_id:198925)直接相关。许多金属的塑性屈服行为主要由[偏应力](@entry_id:163323)引起，而几乎不受[静水压力](@entry_id:275365)的影响。例如，著名的 **von Mises [屈服准则](@entry_id:193897)**就指出，当 $J_2$ 达到一个临界值时，材料开始屈服。该准则可以写作 $\sqrt{3J_2} = \sigma_y$，其中 $\sigma_y$ 是材料在[单轴拉伸](@entry_id:188287)下的[屈服强度](@entry_id:162154) [@problem_id:2921246]。

**$J_3$：** 第三偏[应力[不变](@entry_id:170526)量](@entry_id:148850)定义为 $J_3 = \det(\mathbf{s})$。它描述了应力状态的“模式”或特性，有时通过所谓的**[Lode角](@entry_id:191590)**来表征。它区分了具有相同 $J_2$ 值（即相同[畸变能](@entry_id:198925)）但[剪切应力分布](@entry_id:197453)不同的状态，例如广义拉伸、广义剪切或广义压缩。

考虑一个由以下张量描述的应力状态 [@problem_id:2921230]：
$$
\boldsymbol{\sigma} = \begin{pmatrix} 150 & 30 & -20 \\ 30 & 120 & 10 \\ -20 & 10 & 90 \end{pmatrix} \, \mathrm{MPa}
$$
首先，我们计算第一[不变量](@entry_id:148850) $I_1 = 150 + 120 + 90 = 360 \, \mathrm{MPa}$，这给出了平均[正应力](@entry_id:260622) $p = 360/3 = 120 \, \mathrm{MPa}$。然后，我们计算[偏应力张量](@entry_id:267642)：
$$
\mathbf{s} = \boldsymbol{\sigma} - 120\mathbf{I} = \begin{pmatrix} 30 & 30 & -20 \\ 30 & 0 & 10 \\ -20 & 10 & -30 \end{pmatrix} \, \mathrm{MPa}
$$
利用 $J_2 = \frac{1}{2}(s_{11}^2 + s_{22}^2 + s_{33}^2) + s_{12}^2 + s_{23}^2 + s_{31}^2$ 和 $J_3 = \det(\mathbf{s})$，我们可以计算出该状态的偏[应力[不变](@entry_id:170526)量](@entry_id:148850)为 $J_2 = 2300 \, \mathrm{MPa}^2$ 和 $J_3 = 12000 \, \mathrm{MPa}^3$。这些数值量化了该点的体积改变效应（通过 $I_1$）、畸变强度（通过 $J_2$）和应力状态模式（通过 $J_3$）。

### [莫尔圆](@entry_id:168131)：应力变换的可视化

虽然上述代数方法是完备的，但德国工程师 Otto Mohr 在19世纪末提出了一种巧妙的图形方法来可视化应力变换，即**[莫尔圆](@entry_id:168131)**。

#### 二维[平面应力](@entry_id:172193)[莫尔圆](@entry_id:168131)

对于[平面应力](@entry_id:172193)状态，作用在任意平面上的正应力 $\sigma_n$ 和剪应力 $\tau_n$ 的变换方程为：

$$
\sigma_n = \frac{\sigma_x + \sigma_y}{2} + \frac{\sigma_x - \sigma_y}{2}\cos(2\theta) + \tau_{xy}\sin(2\theta)
$$
$$
\tau_n = -\frac{\sigma_x - \sigma_y}{2}\sin(2\theta) + \tau_{xy}\cos(2\theta)
$$

将这两式进行[平方和相加](@entry_id:188300)，可以消去 $\theta$，得到一个[圆的方程](@entry_id:169149)：

$$
\left(\sigma_n - \frac{\sigma_x + \sigma_y}{2}\right)^2 + \tau_n^2 = \left(\frac{\sigma_x - \sigma_y}{2}\right)^2 + \tau_{xy}^2
$$

这是一个在 $(\sigma_n, \tau_n)$ 平面上的圆，其圆心位于 $C = \frac{\sigma_x + \sigma_y}{2}$，半径为 $R = \sqrt{(\frac{\sigma_x - \sigma_y}{2})^2 + \tau_{xy}^2}$。

[莫尔圆](@entry_id:168131)上的每个点都对应于一个特定方向平面上的应力状态。主应力 $\sigma_1$ 和 $\sigma_2$ 是圆与水平轴的两个交点，因为在这些点上剪应力 $\tau_n=0$ [@problem_id:2921224]。这两个值分别为 $\sigma_{1,2} = C \pm R$。圆的最高点和最低点则对应于[最大剪应力](@entry_id:181794)平面。

**符号约定与角度关系：** [莫尔圆](@entry_id:168131)的构建对符号约定非常敏感 [@problem_id:2921210]。一个常见的约定是：正应力 $\sigma$ 轴向右为正，剪应力 $\tau$ 轴向上为正。在这种约定下，一个重要的规则是：**物理空间中逆时针（CCW）的转角 $\theta$，对应于[莫尔圆](@entry_id:168131)上顺时针（CW）的转角 $2\theta$**。

让我们通过一个例子来说明 [@problem_id:1557601] [@problem_id:2921210]。考虑一个应力状态：$\sigma_{xx} = 80 \, \mathrm{MPa}$, $\sigma_{yy} = -20 \, \mathrm{MPa}$, $\tau_{xy} = 40 \, \mathrm{MPa}$。
- 圆心：$C = (80 - 20)/2 = 30 \, \mathrm{MPa}$
- 半径：$R = \sqrt{((80 - (-20))/2)^2 + 40^2} = \sqrt{50^2 + 40^2} \approx 64.0 \, \mathrm{MPa}$
- [主应力](@entry_id:176761)：$\sigma_1 = 30 + 64.0 = 94.0 \, \mathrm{MPa}$，$\sigma_2 = 30 - 64.0 = -34.0 \, \mathrm{MPa}$。
- [主方向](@entry_id:276187)角 $\theta_p$ 由 $\tan(2\theta_p) = \frac{2\tau_{xy}}{\sigma_{xx}-\sigma_{yy}} = \frac{2(40)}{100} = 0.8$ 确定，因此 $2\theta_p \approx 38.7^\circ$，$\theta_p \approx 19.3^\circ$。
如果一个分析师错误地记为 $\tau_{xy} = -40 \, \mathrm{MPa}$，圆心和半径不变，但主方向角会变为 $\tan(2\theta_p) = -0.8$，导致 $\theta_p \approx -19.3^\circ$。这凸显了正确处理剪应力符号的重要性。

#### 三维应力[莫尔圆](@entry_id:168131)

对于三维应力状态，情况更为复杂，但[莫尔圆](@entry_id:168131)的概念仍然适用。给定三个主应力 $\sigma_1 \ge \sigma_2 \ge \sigma_3$，我们可以构建三个主[莫尔圆](@entry_id:168131)，分别对应于 $(\sigma_1, \sigma_2)$、$(\sigma_2, \sigma_3)$ 和 $(\sigma_1, \sigma_3)$ 这三对[主应力](@entry_id:176761) [@problem_id:2690981]。

- 第一个圆的圆心为 $(\sigma_1+\sigma_2)/2$，半径为 $(\sigma_1-\sigma_2)/2$。
- 第二个圆的圆心为 $(\sigma_2+\sigma_3)/2$，半径为 $(\sigma_2-\sigma_3)/2$。
- 第三个圆的圆心为 $(\sigma_1+\sigma_3)/2$，半径为 $(\sigma_1-\sigma_3)/2$。

一个基本结论是，材料点内任何可能平面上的应力状态 $(\sigma_n, \tau_n)$ 都必须位于这三个[莫尔圆](@entry_id:168131)所围成的阴影区域内。由此可以立即得出一个极为重要的工程结论：作用在某一点上的**[最大剪应力](@entry_id:181794)**等于最大[莫尔圆](@entry_id:168131)的半径，即：

$$
\tau_{\max} = \frac{\sigma_1 - \sigma_3}{2}
$$

这解释了为什么在进行强度校核时，仅仅考虑平面应力可能是不够的，因为即使面外正应力为零（如 $\sigma_3=0$），它仍然参与决定最大的三维剪应力。

三维[莫尔圆](@entry_id:168131)的几何形状与[应力不变量](@entry_id:170526)也有着密切联系。例如，第二偏[应力[不变](@entry_id:170526)量](@entry_id:148850) $J_2$ 可以表示为三个[莫尔圆](@entry_id:168131)半径平方的加权和 [@problem_id:2690981] [@problem_id:2921246]：

$$
J_2 = \frac{2}{3}(R_{12}^2 + R_{23}^2 + R_{13}^2)
$$

此外，[静水应力](@entry_id:186327) $p$ 的作用是将整个三维[莫尔圆](@entry_id:168131)图沿 $\sigma$ 轴进行平移，而不改变任何一个圆的半径。这再次从图形上证实了 $J_2$ 和 $\tau_{\max}$ 都不受静水压力的影响 [@problem_id:2690981]。

#### 特殊情况与局限性

**退化[主应力](@entry_id:176761)：** 当两个或三个[主应力](@entry_id:176761)相等时，应力状态具有对称性，[莫尔圆](@entry_id:168131)的形状也相应简化 [@problem_id:2921227]。
- 如果 $\sigma_1 = \sigma_2 \neq \sigma_3$（[轴对称](@entry_id:173333)应力状态），则 $(\sigma_1, \sigma_2)$ [莫尔圆](@entry_id:168131)退化为一个点，另外两个圆重合。物理上，这意味着在垂直于 $\sigma_3$ [主方向](@entry_id:276187)的平面内，所有方向都是[主方向](@entry_id:276187)，这些平面上的剪应力为零。
- 如果 $\sigma_1 = \sigma_2 = \sigma_3$（[静水应力](@entry_id:186327)状态），三个[莫尔圆](@entry_id:168131)都退化为同一个点。这意味着所有平面都是[主平面](@entry_id:164488)，所有平面上的剪应力都为零。

**[莫尔圆](@entry_id:168131)的局限性：** 尽管[莫尔圆](@entry_id:168131)是一个强大的工具，但它也有其固有的局限性 [@problem_id:2921222]。
1.  **剪应力方向信息的丢失**：[莫尔圆](@entry_id:168131)的纵坐标是剪应力的大小 $\tau$，它是一个标量。然而，在一个三维空间中的平面上，剪切牵[引力](@entry_id:175476)本身是一个矢量 $\mathbf{t}_s$，它有自己的方向。[莫尔圆](@entry_id:168131)完全舍弃了关于剪切矢量在平面内指向何处的信息。
2.  **空间方位信息的丢失**：三个[莫尔圆](@entry_id:168131)仅由三个主应力值确定。它们本身并不包含关于[主方向](@entry_id:276187)（即本征矢量）在空间中如何定向的信息。两个具有相同[主应力](@entry_id:176761)值但在空间中方位不同的应力状态，将具有完全相同的[莫尔圆](@entry_id:168131)图。

因此，[莫尔圆](@entry_id:168131)是对称二阶[应力张量](@entry_id:148973)（需要6个独立分量来完全定义）的一种[降维](@entry_id:142982)、不完整的可视化，它牺牲了部分信息以换取对正应力和剪应力大小关系的直观理解。