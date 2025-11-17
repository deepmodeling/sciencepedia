## 引言
在[固体力学](@entry_id:164042)领域，精确预测材料在复杂载荷下的行为是一项核心挑战。任意一个应力状态都可能同时导致材料体积的改变（压缩或膨胀）和形状的改变（畸变），而将这两种效应分离开来，对于建立准确的材料[本构模型](@entry_id:174726)至关重要。[偏应力](@entry_id:163323)与[静水应力](@entry_id:186327)分解正是解决这一问题的基础理论工具，它提供了一个深刻的框架来独立地分析和量化这两种基本变形模式。

本文旨在全面探讨这一关键概念。在第一章“原理与机制”中，我们将深入其数学基础和物理意义，揭示应力如何分解为驱动体积变化的静水部分和驱动形状变化的偏量部分。接着，在第二章“应用与[交叉](@entry_id:147634)学科联系”中，我们将展示这一分解如何在塑性力学、断裂力学和[地球科学](@entry_id:749876)等多个领域中发挥关键作用，连接起看似无关的材料行为。最后，通过第三章“动手实践”，读者将有机会通过具体计算和编程练习，将理论知识转化为实践技能。通过这一结构化的学习路径，本文将为读者构建一个关于[应力分解](@entry_id:272862)的坚实理论与应用基础。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，理解材料如何响应外部载荷是核心任务。一个通用的应力状态既可能引起材料体积的改变（膨胀或收缩），也可能导致其形状的改变（畸变）。为了系统地分析这两种效应，将柯西[应力张量](@entry_id:148973)分解为其静水（球量）[部分和](@entry_id:162077)偏量部分是一种极其有效且基础深刻的工具。本章将深入探讨这一分解的原理、物理意义、数学基础及其在材料本构理论中的核心作用。

### 应力张量的基本分解

在任意一点，材料的应力状态由二阶对称的柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 描述。根据柯西应力定理，作用在[单位法向量](@entry_id:178851)为 $\boldsymbol{n}$ 的平面上的[面力矢量](@entry_id:189429) $\boldsymbol{t}(\boldsymbol{n})$ 由关系式 $\boldsymbol{t}(\boldsymbol{n})=\boldsymbol{\sigma}\boldsymbol{n}$ 给出。在经典连续介质理论中，若不考虑体力矩，角动量守恒要求 $\boldsymbol{\sigma}$ 必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$。[@problem_id:2630183]

任何二阶张量都可以唯一地分解为一个球形张量（与单位张量 $\boldsymbol{I}$ 成比例）和一个[无迹张量](@entry_id:274053)之和。对于应力张量 $\boldsymbol{\sigma}$，这个分解形式为：
$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}_H + \boldsymbol{s}
$$
其中 $\boldsymbol{\sigma}_H$ 是[静水应力](@entry_id:186327)（或球形应力）部分，$\boldsymbol{s}$ 是[偏应力](@entry_id:163323)部分。

**[静水应力](@entry_id:186327)** $\boldsymbol{\sigma}_H$ 被定义为引起均匀[法向应力](@entry_id:260622)而无[剪切应力](@entry_id:137139)的部分。因此，它必须与二阶单位张量 $\boldsymbol{I}$ 成比例：
$$
\boldsymbol{\sigma}_H = p\boldsymbol{I}
$$
其中标量 $p$ 被称为**平均应力**或**[静水压力](@entry_id:275365)**。为了确定 $p$，我们要求**[偏应力](@entry_id:163323)** $\boldsymbol{s}$ 是无迹的，即其迹 $\operatorname{tr}(\boldsymbol{s}) = 0$。对分解式 $\boldsymbol{\sigma} = p\boldsymbol{I} + \boldsymbol{s}$ 两边取迹，可得：
$$
\operatorname{tr}(\boldsymbol{\sigma}) = \operatorname{tr}(p\boldsymbol{I}) + \operatorname{tr}(\boldsymbol{s}) = p\operatorname{tr}(\boldsymbol{I}) + 0
$$
在三维空间中，$\operatorname{tr}(\boldsymbol{I}) = 3$，因此我们得到 $p$ 的定义：
$$
p = \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})
$$
相应地，[偏应力张量](@entry_id:267642) $\boldsymbol{s}$ 定义为：
$$
\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I} = \boldsymbol{\sigma} - \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})\boldsymbol{I}
$$
通过构造，$\operatorname{tr}(\boldsymbol{s}) = \operatorname{tr}(\boldsymbol{\sigma}) - \operatorname{tr}(\frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})\boldsymbol{I}) = \operatorname{tr}(\boldsymbol{\sigma}) - \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma}) \cdot 3 = 0$，这保证了[偏应力](@entry_id:163323)的无迹特性。

为了获得一个直观的几何理解，我们可以考虑应力张量的主应力 $\sigma_1, \sigma_2, \sigma_3$。它们是 $\boldsymbol{\sigma}$ 的[特征值](@entry_id:154894)。由于迹是张量的[不变量](@entry_id:148850)，它等于其[特征值](@entry_id:154894)之和，即 $\operatorname{tr}(\boldsymbol{\sigma}) = \sigma_1 + \sigma_2 + \sigma_3$。因此，平均应力 $p$ 可以表示为：
$$
p = \frac{\sigma_1 + \sigma_2 + \sigma_3}{3}
$$
这个表达式恰好是三个主应力值的算术平均值。如果我们把 $\sigma_1, \sigma_2, \sigma_3$ 看作是[实数轴](@entry_id:147286)上的三个点，那么 $p$ 的值就是这三个点的**几何[质心](@entry_id:265015)**。[@problem_id:2630169] 这种分解本质上是将应力状态的原点移动到[主应力空间](@entry_id:184388)的[质心](@entry_id:265015)上。

### 物理意义：体积改变与形状畸变

[应力张量](@entry_id:148973)的静水-偏量分解不仅仅是数学上的便利，它深刻地反映了两种截然不同的物理效应。

[静水应力](@entry_id:186327)部分 $p\boldsymbol{I}$ 是一个各向同性的应力状态。它在所有方向上施加的[法向应力](@entry_id:260622)都是相等的，大小为 $p$。作用在任意平面 $\boldsymbol{n}$ 上的面力为 $\boldsymbol{t}_H(\boldsymbol{n}) = (p\boldsymbol{I})\boldsymbol{n} = p\boldsymbol{n}$。这个[面力矢量](@entry_id:189429)与法向量 $\boldsymbol{n}$ 平行，意味着它只产生[法向应力](@entry_id:260622)，而不产生任何[剪切应力](@entry_id:137139)。因此，**[静水应力](@entry_id:186327)与材料的体积改变（膨胀或压缩）相关联**。

相比之下，偏应力部分 $\boldsymbol{s}$ 代表了应力状态的非各向同性部分。由[偏应力](@entry_id:163323)在平面 $\boldsymbol{n}$ 上产生的[法向应力](@entry_id:260622)为 $\boldsymbol{n} \cdot (\boldsymbol{s}\boldsymbol{n})$。可以证明，这个法向应力在所有方向上的平均值为零，因为 $\langle \boldsymbol{n} \cdot (\boldsymbol{s}\boldsymbol{n}) \rangle = \frac{1}{3}\operatorname{tr}(\boldsymbol{s}) = 0$。[偏应力](@entry_id:163323)的主要作用是产生剪切应力，从而导致材料的**形状畸变（[剪切变形](@entry_id:170920)）而保持体积不变**。[@problem_id:2630210]

这种物理效应的解耦在[应力功率](@entry_id:182907)（单位体积的内[功率耗散](@entry_id:264815)率）的表达式中得到了完美的体现。[应力功率](@entry_id:182907)为 $\mathcal{P} = \boldsymbol{\sigma} : \boldsymbol{d}$，其中 $\boldsymbol{d}$ 是变形率张量（[速度梯度](@entry_id:261686)的对称部分）。将应力和变形率张量都进行静水-偏量分解：
$$
\boldsymbol{\sigma} = p\boldsymbol{I} + \boldsymbol{s}
$$
$$
\boldsymbol{d} = \frac{1}{3}\operatorname{tr}(\boldsymbol{d})\boldsymbol{I} + \operatorname{dev}(\boldsymbol{d})
$$
其中 $\operatorname{tr}(\boldsymbol{d})$ 是[体积应变率](@entry_id:272471)，$\operatorname{dev}(\boldsymbol{d})$ 是畸变率张量。[应力功率](@entry_id:182907)可以展开为：
$$
\mathcal{P} = (p\boldsymbol{I} + \boldsymbol{s}) : \left(\frac{1}{3}\operatorname{tr}(\boldsymbol{d})\boldsymbol{I} + \operatorname{dev}(\boldsymbol{d})\right) = p\operatorname{tr}(\boldsymbol{d}) + \boldsymbol{s} : \operatorname{dev}(\boldsymbol{d})
$$
展开式中的交叉项（如 $p\boldsymbol{I} : \operatorname{dev}(\boldsymbol{d})$）为零，因为球形张量与任何[偏张量](@entry_id:185837)在[弗罗贝尼乌斯内积](@entry_id:153693)（Frobenius inner product）下是正交的。这个结果表明，总的[应力功率](@entry_id:182907)可以干净地分解为两部分：**体积改变功率** $p\operatorname{tr}(\boldsymbol{d})$ 和 **形状畸变功率** $\boldsymbol{s} : \operatorname{dev}(\boldsymbol{d})$，两者之间没有[能量耦合](@entry_id:137595)。[@problem_id:2630210]

### 各向同性假设在解耦中的核心作用

体积和畸变响应的解耦在材料[本构关系](@entry_id:186508)中表现得尤为重要，但这依赖于材料的对称性，特别是**各向同性**假设。

对于小应变下的线弹性[各向同性材料](@entry_id:170678)，其本构关系（[胡克定律](@entry_id:149682)）可以表示为：
$$
\boldsymbol{\sigma} = \lambda \operatorname{tr}(\boldsymbol{\varepsilon})\boldsymbol{I} + 2\mu\boldsymbol{\varepsilon}
$$
其中 $\boldsymbol{\varepsilon}$ 是[小应变张量](@entry_id:754968)，$\lambda$ 和 $\mu$ 是拉梅参数。通过对该关系式进行静水-偏量分解，我们可以得到两组独立的[本构方程](@entry_id:138559)：
$$
p = K \operatorname{tr}(\boldsymbol{\varepsilon})
$$
$$
\boldsymbol{s} = 2G \boldsymbol{\varepsilon}'
$$
这里，$p = \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})$ 是[平均应力](@entry_id:751819)，$\operatorname{tr}(\boldsymbol{\varepsilon})$ 是[体应变](@entry_id:267252)；$\boldsymbol{s}$ 和 $\boldsymbol{\varepsilon}'$ 分别是应力和应变的偏量部分。$K = \lambda + \frac{2}{3}\mu$ 是**[体积模量](@entry_id:160069)**，描述材料抵[抗体](@entry_id:146805)积改变的能力；$G$（等同于 $\mu$）是**[剪切模量](@entry_id:167228)**，描述材料抵抗形状改变的能力。[@problem_id:2920817]

这些方程清晰地表明，对于各向同性材料，[静水应力](@entry_id:186327)只与体应变有关，而[偏应力](@entry_id:163323)只与[偏应变](@entry_id:201263)（畸变）有关。因此，一个纯粹的偏应力状态（$p=0$，即 $I_1 = \operatorname{tr}(\boldsymbol{\sigma})=0$）只会产生形状畸变，而不会引起体积变化（$\operatorname{tr}(\boldsymbol{\varepsilon})=0$）。[@problem_id:2920817]

必须强调，这种完美的[解耦](@entry_id:637294)是**各向同性**的直接后果，并非普遍成立。对于**各向异性**材料，其[刚度张量](@entry_id:176588) $\boldsymbol{C}$ 的复杂结构通常会耦合体积响应和剪切响应。例如，在某些晶体中，施加一个纯[静水压力](@entry_id:275365)可能会引起[剪切变形](@entry_id:170920)。因此，体积-畸变响应的解耦是一种本构特性，而非纯粹的运动学或静力学法则。[@problem_id:2920794]

从更高等的数学观点看，这个解耦源于对称[二阶张量](@entry_id:199780)空间 $\mathsf{Sym}$ 在[旋转群](@entry_id:204412) $SO(3)$ 作用下的分解。该空间可以分解为一个一维的球形[子空间](@entry_id:150286)（对应于迹）和一个五维的偏量[子空间](@entry_id:150286)。这两个[子空间](@entry_id:150286)是 $SO(3)$ 的[不可约表示](@entry_id:263310)，并且它们不等价。根据[舒尔引理](@entry_id:136779)（Schur's Lemma），任何与[旋转变换](@entry_id:200017)可交换的线性映射（即各向同性算子，如[各向同性弹性](@entry_id:203237)张量）必须将这些不变子空间映入自身，且不能在它们之间产生[交叉](@entry_id:147634)映射。这从根本上解释了为什么各向同性[本构关系](@entry_id:186508)必须是[块对角化](@entry_id:145518)的，从而实现了体积响应和畸变响应的[解耦](@entry_id:637294)。[@problem_id:2920832]

### 描述应力状态的[不变量](@entry_id:148850)

为了以不依赖于[坐标系](@entry_id:156346)的方式量化应力状态，我们使用[张量不变量](@entry_id:203254)。对于静水-偏量分解，有几组[不变量](@entry_id:148850)特别有用。

#### 静水[应力[不变](@entry_id:170526)量](@entry_id:148850)与符号约定

[静水应力](@entry_id:186327)的大小由[平均应力](@entry_id:751819) $p = \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})$ 直接度量。然而，在不同学科中，$p$ 的符号约定存在差异，这可能导致混淆。

1.  **[固体力学](@entry_id:164042)约定**: 在[固体力学](@entry_id:164042)中，通常规定拉应力为正。在此约定下，$p = \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})$。一个正的 $p$ 值表示静水拉伸状态，负的 $p$ 值表示静水压缩状态。[@problem_id:2630199]

2.  **[热力学](@entry_id:141121)/[流体力学](@entry_id:136788)约定**: 在这些领域，压力通常被定义为在压缩状态下为正。为了与[热力学](@entry_id:141121)压力 $P_{\text{th}}$ 保持一致（流体静止时 $\boldsymbol{\sigma} = -P_{\text{th}}\boldsymbol{I}$），压力 $p$ 定义为 $p = -\frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})$。这样，一个正的 $p$ 值就对应于压缩状态。[@problem_id:2630199]

这两种约定仅仅是符号上的差别，但必须在使用时保持一致。如果采用[热力学](@entry_id:141121)约定，则[应力分解](@entry_id:272862)式应写作 $\boldsymbol{\sigma} = -p\boldsymbol{I} + \boldsymbol{s}$，以确保 $\boldsymbol{s}$ 仍然是无迹的。[@problem_id:2630199]

#### 偏[应力[不变](@entry_id:170526)量](@entry_id:148850)：$J_2$ 和 $J_3$

[偏应力张量](@entry_id:267642) $\boldsymbol{s}$ 也有其自身的[主不变量](@entry_id:193522)，通常记为 $J_1, J_2, J_3$。
- $J_1 = \operatorname{tr}(\boldsymbol{s}) = 0$ (由定义)。
- $J_2 = \frac{1}{2}\operatorname{tr}(\boldsymbol{s}^2) = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s}$。
- $J_3 = \det(\boldsymbol{s})$。

其中，**第二偏[应力[不变](@entry_id:170526)量](@entry_id:148850) $J_2$** 尤为重要。它衡量了[偏应力](@entry_id:163323)的“强度”或“大小”。由于 $\boldsymbol{s}$ 是对称的，$\boldsymbol{s}^2$ 的对角元非负，因此 $J_2 \ge 0$。量纲上，$J_2$ 是应力的平方，所以 $\sqrt{J_2}$ 具有应力的量纲，常被用作偏应力大小的度量。例如，对于一个由应力张量 $\boldsymbol{\sigma}=\begin{pmatrix} 80  20  0\\ 20  50  0\\ 0  0  30 \end{pmatrix}\,\text{MPa}$ 描述的应力状态，可以计算出 $p=\frac{160}{3}\,\text{MPa}$ 和 $J_2=\frac{3100}{3}\,\text{MPa}^2$。[@problem_id:2630194]

**第三偏[应力[不变](@entry_id:170526)量](@entry_id:148850) $J_3$** 描述了偏应力状态的“模式”或“类型”。它与主[偏应力](@entry_id:163323)的相对大小有关。

#### [不变量](@entry_id:148850)的客观性与独立性

$p$ 和 $\sqrt{J_2}$ 是描述应力状态的两个核心标量。它们具有以下重要性质：

- **客观性 (Objectivity)**: 在一个叠加的刚体运动下，柯西应力张量变换为 $\boldsymbol{\sigma}' = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}$，其中 $\boldsymbol{Q}$ 是一个正常交[旋转张量](@entry_id:191990)。可以证明，在这种变换下，$p$ 和 $J_2$ 的值保持不变。这意味着它们是客观的标量，不依赖于观察者的[参考系](@entry_id:169232)，真实地反映了材料内部的应力状态。[@problem_id:2630186]

- **独立性 (Independence)**: $p$ 和 $J_2$ 是两个独立的量。可以构造出具有相同 $p$ 值但不同 $J_2$ 值的应力状态（例如，一个静水拉伸[状态和](@entry_id:193625)一个附加了剪切的静水拉伸状态），也可以构造出具有相同 $J_2$ 值但不同 $p$ 值的应力状态（例如，一个纯剪切[状态和](@entry_id:193625)一个[单轴拉伸](@entry_id:188287)状态）。[@problem_id:2630186] 这种独立性再次印证了体积改变和形状畸变是两种可独立变化的物理过程。一个应力状态不能仅由其中一个标量完全描述。

#### 洛德角 (Lode Angle)

为了更精细地刻画[偏应力](@entry_id:163323)的类型，$J_2$ 和 $J_3$ 可以组合成一个[无量纲参数](@entry_id:169335)，即**洛德角 $\theta$**。一个常见的定义是：
$$
\sin(3\theta) = \frac{3\sqrt{3}}{2}\frac{J_3}{J_2^{3/2}}
$$
这个定义要求 $J_2 > 0$。归一化因子 $\frac{3\sqrt{3}}{2}$ 确保了右边的值总是在 $[-1, 1]$ 区间内，其边界值在[轴对称](@entry_id:173333)偏应力状态（例如[单轴拉伸](@entry_id:188287)或压缩）下达到。[@problem_id:2630212]

洛德角 $\theta$ 的取值范围通常约定在 $[-\pi/6, \pi/6]$。不同的 $\theta$ 值对应于不同的主偏应力[分布](@entry_id:182848)模式，它描述了应力状态在所谓的“$\pi$ 平面”（一个以 $J_2$ 为半径的圆形平面）上的位置：
- $\theta = \pi/6$: 对应于“拉伸型”轴对称[偏应力](@entry_id:163323) ($s_1 > s_2 = s_3$)。
- $\theta = -\pi/6$: 对应于“压缩型”轴对称[偏应力](@entry_id:163323) ($s_1 = s_2 > s_3$)。
- $\theta = 0$: 对应于“纯剪切型”偏应力 ($J_3=0$, 例如 $s_2=0, s_1=-s_3$)。

洛德角只依赖于偏[应力[不变](@entry_id:170526)量](@entry_id:148850)，因此它与[静水压力](@entry_id:275365) $p$ 无关。改变静水压力不会改变洛德角。[@problem_id:2630212]

### 应用与意义

静水-偏量分解在[固体力学](@entry_id:164042)，尤其是非弹性材料行为的建模中，具有至关重要的意义。

在**塑性力学**中，许多金属材料的屈服行为对静水压力不敏感或弱敏感。这意味着材料是否开始塑性变形主要取决于偏应力的大小，而非静水压力。著名的 **von Mises 屈服准则** 就是基于这一思想，它假设当第二偏[应力[不变](@entry_id:170526)量](@entry_id:148850) $J_2$ 达到一个临界值时，材料开始屈服。其[屈服函数](@entry_id:167970)可写作 $f(\boldsymbol{\sigma}) = \sqrt{3J_2} - Y_0 = 0$，其中 $Y_0$ 是[单轴拉伸](@entry_id:188287)屈服应力。根据这个准则，一个纯静水加载路径（$\boldsymbol{s}=\boldsymbol{0}$）永远不会引起[塑性流动](@entry_id:201346)。[@problem_id:2630210] 洛德角 $J_3$ 则在更精细的[屈服准则](@entry_id:193897)（如 Drucker-Prager 或 Tresca 准则）中扮演角色，用于描述拉伸和压缩[屈服应力](@entry_id:274513)的差异。

在**弹性力学**中，这种分解简化了[本构关系](@entry_id:186508)，并将弹性响应与两个独立的物理常数——体积模量 $K$ 和剪切模量 $G$ 联系起来。[弹性应变能](@entry_id:202243)密度 $W = \frac{1}{2}\boldsymbol{\sigma}:\boldsymbol{\varepsilon}$ 也可以被分解为[体积应变](@entry_id:267252)能和畸变应变能两部分。例如，体积[应变能密度](@entry_id:200085)可以表示为 $W_{\text{vol}} = \frac{1}{2} p \operatorname{tr}(\boldsymbol{\varepsilon}) = \frac{1}{18K}I_1^2$。[@problem_id:2920817]

总之，将[应力分解](@entry_id:272862)为驱动体积变化的静水部分和驱动形状变化的偏量部分，是理解和建模[材料力学](@entry_id:201885)行为的一个基本出发点。它不仅简化了数学描述，更重要的是，它揭示了材料响应载荷的两种基本物理机制，为构建严谨而准确的本构理论奠定了基础。