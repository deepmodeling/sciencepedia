## 引言
在工程与科学分析中，理解材料内部的应力状态是预测其行为和确保结构安全的关键。尽管柯西应力张量提供了任一点应力状态的完整描述，但材料的失效和变形往往由特定平面上的特定应力分量主导。剪应力，作为引起材料形状改变（畸变）的根本原因，在这一背景下尤为重要。然而，如何从复杂的三维应力状态中提取一个有代表性的剪[应力量度](@entry_id:198799)，以用于建立简洁而有效的材料模型，是固体力学面临的一个核心问题。本文旨在深入剖析两个最重要且广泛应用的剪[应力量度](@entry_id:198799)——[最大剪应力](@entry_id:181794)与[八面体应力](@entry_id:183012)，澄清它们之间的联系与区别。

本文将分为三个章节，引领读者逐步深入这一主题。在“原理和机制”一章中，我们将从第一性原理出发，推导[最大剪应力](@entry_id:181794)和[八面体应力](@entry_id:183012)的数学表达式，并揭示它们与[主应力](@entry_id:176761)、偏[应力分解](@entry_id:272862)及[应力不变量](@entry_id:170526)的深刻联系。接下来的“应用与跨学科联系”一章将展示这些理论概念如何转化为强大的工程工具，重点分析它们在经典塑性屈服准则（特雷斯卡与冯·米塞斯）中的应用，并探讨它们在岩[土力学](@entry_id:180264)、[损伤力学](@entry_id:178377)和接触力学等领域的延伸与局限。最后，通过“动手实践”部分提供的一系列问题，读者将有机会亲手计算和应用这些概念，从而将理论知识内化为解决实际问题的能力。

## 原理和机制

在对材料点处应力状态进行分析时，一个核心任务是理解在不同方向的[截面](@entry_id:154995)上，应力是如何[分布](@entry_id:182848)的。虽然柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 完整地描述了该点的应力状态，但某些特定的应力分量或在特定平面上的应力值，对于理解材料的变形和失效行为具有更为直接和重要的物理意义。本章将深入探讨两个关键的剪应力衡量标准：[最大剪应力](@entry_id:181794)与[八面体剪应力](@entry_id:200691)，并阐明它们的物理原理、数学推导及其在固体力学中的核心作用。

### 任意平面上的应力

根据柯西应力定理，通过某一点并以[单位法向量](@entry_id:178851) $\mathbf{n}$ 为特征的任意平面上，其[面力矢量](@entry_id:189429) $\mathbf{t}$ 由下式给出：

$$
\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}
$$

这个[面力矢量](@entry_id:189429) $\mathbf{t}$ 通常不与平[面法向量](@entry_id:749211) $\mathbf{n}$ 平行。因此，它可以被分解为一个垂直于平面的**[正应力](@entry_id:260622)**分量和一个平行于平面的**剪应力**分量。正应力分量的大小 $\sigma_n$ 是[面力矢量](@entry_id:189429) $\mathbf{t}$ 在法线方向 $\mathbf{n}$ 上的投影：

$$
\sigma_n = \mathbf{t} \cdot \mathbf{n} = \mathbf{n}^T \boldsymbol{\sigma} \mathbf{n}
$$

[面力矢量](@entry_id:189429)的法向分量为 $\sigma_n \mathbf{n}$。而其切向分量，即剪应力矢量 $\boldsymbol{\tau}_s$，则由总[面力矢量](@entry_id:189429)减去其法向分量得到：$\boldsymbol{\tau}_s = \mathbf{t} - \sigma_n \mathbf{n}$。剪应力的大小 $\tau$ 便是该剪应力矢量的模：

$$
\tau = \|\boldsymbol{\tau}_s\| = \sqrt{\|\mathbf{t}\|^2 - \sigma_n^2}
$$

考虑一个具体例子 [@problem_id:2659324]，假设在某主应力[坐标系](@entry_id:156346)下，[应力张量](@entry_id:148973)为：

$$
\boldsymbol{\sigma} = \begin{bmatrix} 150  0  0 \\ 0  90  0 \\ 0  0  30 \end{bmatrix} \text{ MPa}
$$

对于一个[法向量](@entry_id:264185)为 $\mathbf{n}_{\mathrm{o}} = \frac{1}{\sqrt{3}}[1, 1, 1]^T$ 的平面，其[面力矢量](@entry_id:189429)为：

$$
\mathbf{t}(\mathbf{n}_{\mathrm{o}}) = \boldsymbol{\sigma}\mathbf{n}_{\mathrm{o}} = \frac{1}{\sqrt{3}}\begin{bmatrix} 150 \\ 90 \\ 30 \end{bmatrix} \text{ MPa}
$$

该平面上的[正应力](@entry_id:260622)为：

$$
\sigma_n = \mathbf{t}(\mathbf{n}_{\mathrm{o}}) \cdot \mathbf{n}_{\mathrm{o}} = \frac{1}{3}(150 + 90 + 30) = 90 \text{ MPa}
$$

而剪应力的大小则为：

$$
\tau^2 = \|\mathbf{t}(\mathbf{n}_{\mathrm{o}})\|^2 - \sigma_n^2 = \frac{1}{3}(150^2 + 90^2 + 30^2) - 90^2 = 10500 - 8100 = 2400 \text{ (MPa)}^2
$$

因此，$\tau = \sqrt{2400} \approx 49 \text{ MPa}$。这表明，即使在主应力[坐标系](@entry_id:156346)下，一个任意方向的平面上通常也同时存在正应力和剪应力。

### 主应力与[最大剪应力](@entry_id:181794)

一个自然而然的问题是：是否存在一些特殊的平面，其上的剪应力为零？答案是肯定的。这些平面被称为**[主平面](@entry_id:164488)**，其法线方向被称为**[主方向](@entry_id:276187)**，而作用在[主平面](@entry_id:164488)上的[正应力](@entry_id:260622)则被称为**[主应力](@entry_id:176761)**。在[主平面](@entry_id:164488)上，[面力矢量](@entry_id:189429)与法向量平行，即 $\mathbf{t} = \sigma_p \mathbf{n}$，这正是[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的特征值问题 $\boldsymbol{\sigma}\mathbf{n} = \sigma_p\mathbf{n}$。对于对称的柯西[应力张量](@entry_id:148973)，总能找到三个相互正交的主方向和三个实数主应力，通常记为 $\sigma_1, \sigma_2, \sigma_3$。

另一个关键问题是：哪个方向的平面上承受着最大的剪应力？这对预测材料的塑性屈服至关重要。可以证明，对于给定的应力状态，其**绝对[最大剪应力](@entry_id:181794)** $\tau_{\max}$ 完全由最大和最小主应力决定 [@problem_id:2659326]：

$$
\tau_{\max} = \frac{\sigma_1 - \sigma_3}{2}
$$

这里我们约定主应力的顺序为 $\sigma_1 \ge \sigma_2 \ge \sigma_3$。这个最大值出现在特定的平面上：这些平面的[法线](@entry_id:167651)位于由 $\sigma_1$ 和 $\sigma_3$ 对应的主方向所构成的平面内，并且平分这两个[主方向](@entry_id:276187)之间的夹角 [@problem_id:2906445]。例如，如果 $\mathbf{e}_1$ 和 $\mathbf{e}_3$ 是分别对应于 $\sigma_1$ 和 $\sigma_3$ 的[主方向](@entry_id:276187)，那么[最大剪应力](@entry_id:181794)平面的[法向量](@entry_id:264185)之一就是 $\mathbf{n} = (\mathbf{e}_1 + \mathbf{e}_3)/\sqrt{2}$。

理解为何只有极端的主应力 $\sigma_1$ 和 $\sigma_3$ 决定了[最大剪应力](@entry_id:181794)，一个直观的方式是借助**[莫尔圆](@entry_id:168131)**（Mohr's Circle）。在三维应力状态下，所有可能平面上的应力状态点 $(\sigma_n, \tau)$ 都位于由三个[主应力](@entry_id:176761)对 $(\sigma_1, \sigma_2)$, $(\sigma_2, \sigma_3)$, $(\sigma_1, \sigma_3)$ 所定义的三个[莫尔圆](@entry_id:168131)所包围的区域内。绝对[最大剪应力](@entry_id:181794)即为这三个圆中最大圆的半径，这个最大圆正是由最外侧的两个[主应力](@entry_id:176761) $\sigma_1$ 和 $\sigma_3$ 所确定的圆，其半径为 $(\sigma_1 - \sigma_3)/2$ [@problem_id:2659326]。

### [静水压力与偏应力](@entry_id:750463)分解

为了更深入地理解不同应力分量的物理作用，我们将[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 分解为一个球形部分和一个偏量部分 [@problem_id:2659317]：

$$
\boldsymbol{\sigma} = p\mathbf{I} + \mathbf{s}
$$

其中，$p\mathbf{I}$ 被称为**[静水应力](@entry_id:186327)张量**（或球[应力张量](@entry_id:148973)），$\mathbf{I}$ 是单位张量。标量 $p$ 是平均[正应力](@entry_id:260622)，定义为：

$$
p = \frac{1}{3} \mathrm{tr}(\boldsymbol{\sigma}) = \frac{1}{3}(\sigma_1 + \sigma_2 + \sigma_3)
$$

$\mathbf{s}$ 则被称为**[偏应力张量](@entry_id:267642)**，它代表了总应力状态与纯[静水压力](@entry_id:275365)状态的偏差。其定义为 $\mathbf{s} = \boldsymbol{\sigma} - p\mathbf{I}$。一个关键特性是[偏应力张量](@entry_id:267642)的迹恒为零，$\mathrm{tr}(\mathbf{s}) = 0$。

对于[各向同性线弹性](@entry_id:185899)材料，这种分解具有明确的物理意义：
- **[静水应力](@entry_id:186327)** ($p\mathbf{I}$) 引起材料的**体积变化**（膨胀或收缩），但不引起形状的改变（畸变）。
- **偏应力** ($\mathbf{s}$) 引起材料的**形状变化**（畸变），但不引起体积的变化。

这一分解最重要的推论之一是，剪应力完全由[偏应力张量](@entry_id:267642)决定。如果在任意一个应力状态 $\boldsymbol{\sigma}$ 上叠加一个纯[静水应力](@entry_id:186327) $p_0\mathbf{I}$，得到新的应力状态 $\boldsymbol{\sigma}' = \boldsymbol{\sigma} + p_0\mathbf{I}$，那么对于任意平面 $\mathbf{n}$ [@problem_id:2659357]：
- 新的正应力变为 $\sigma_n' = \sigma_n + p_0$。
- 新的剪应力**保持不变**，即 $\tau' = \tau$。

这是因为剪应力矢量 $\boldsymbol{\tau}_s' = \mathbf{t}' - \sigma_n'\mathbf{n} = (\mathbf{t} + p_0\mathbf{n}) - (\sigma_n + p_0)\mathbf{n} = \mathbf{t} - \sigma_n\mathbf{n} = \boldsymbol{\tau}_s$。这个结论意味着，所有与剪切相关的量，包括[最大剪应力](@entry_id:181794) $\tau_{\max}$ 和我们稍后将讨论的[八面体剪应力](@entry_id:200691) $\tau_{\mathrm{oct}}$，都**不受静水压力的影响**。因此，许多由剪切驱动的材料行为，如金属的塑性屈服，主要由[偏应力](@entry_id:163323) $\mathbf{s}$ 控制，这也是[偏应力](@entry_id:163323)和各种剪应力衡量标准在[材料科学](@entry_id:152226)中如此重要的原因。

### [八面体应力](@entry_id:183012)：一种平均应力度量

除了关注[最大剪应力](@entry_id:181794)，我们还对一种代表“平均”应力状态的量度感兴趣。这引出了**[八面体应力](@entry_id:183012)**的概念。

**八面体平面**被定义为与三个主应力轴夹角均相等的平面。在主应力[坐标系](@entry_id:156346)中，这样的平面有8个（构成4对），其[单位法向量](@entry_id:178851)的分量满足 $|n_1|=|n_2|=|n_3|=1/\sqrt{3}$ [@problem_id:2659327]。这八个平面在空间中围成一个正八面体。

**[八面体正应力](@entry_id:180716) ($\sigma_{\mathrm{oct}}$)**

作用在任意一个八面体平面上的正应力，被称为[八面体正应力](@entry_id:180716)。通过直接计算可得 [@problem_id:2659345]：

$$
\sigma_{\mathrm{oct}} = \mathbf{n}_{\mathrm{oct}}^T \boldsymbol{\sigma} \mathbf{n}_{\mathrm{oct}} = \sigma_1 n_1^2 + \sigma_2 n_2^2 + \sigma_3 n_3^2 = \sigma_1\left(\frac{1}{3}\right) + \sigma_2\left(\frac{1}{3}\right) + \sigma_3\left(\frac{1}{3}\right)
$$

$$
\sigma_{\mathrm{oct}} = \frac{1}{3}(\sigma_1 + \sigma_2 + \sigma_3)
$$

我们发现一个重要的恒等式：[八面体正应力](@entry_id:180716)恰好等于平均正应力 $p$ [@problem_id:2659327, @problem_id:2906445]。由于平均[正应力](@entry_id:260622)与[应力张量](@entry_id:148973)的第一[不变量](@entry_id:148850) $I_1 = \mathrm{tr}(\boldsymbol{\sigma})$ 成正比，因此 $\sigma_{\mathrm{oct}}$ 是一个[应力不变量](@entry_id:170526)，其值不随[坐标系](@entry_id:156346)的旋转而改变。

**[八面体剪应力](@entry_id:200691) ($\tau_{\mathrm{oct}}$)**

作用在八面体平面上的剪应力大小，被称为[八面体剪应力](@entry_id:200691)。从第一性原理出发，我们可以推导出其表达式 [@problem_id:2659305]：

$$
\tau_{\mathrm{oct}}^2 = \|\mathbf{t}_{\mathrm{oct}}\|^2 - \sigma_{\mathrm{oct}}^2 = \frac{1}{3}(\sigma_1^2 + \sigma_2^2 + \sigma_3^2) - \left(\frac{\sigma_1 + \sigma_2 + \sigma_3}{3}\right)^2
$$

通过代数展开和整理，可以得到一个更具物理洞察力的形式：

$$
\tau_{\mathrm{oct}} = \frac{1}{3}\sqrt{(\sigma_1 - \sigma_2)^2 + (\sigma_2 - \sigma_3)^2 + (\sigma_3 - \sigma_1)^2}
$$

这个表达式表明，[八面体剪应力](@entry_id:200691)仅与[主应力](@entry_id:176761)之差有关，因此它不受[静水压力](@entry_id:275365)的影响。更进一步，它可以直接与[偏应力张量](@entry_id:267642)的[不变量](@entry_id:148850)联系起来。[偏应力张量](@entry_id:267642)的第二[不变量](@entry_id:148850) $J_2$ 定义为 $J_2 = \frac{1}{2}\mathrm{tr}(\mathbf{s}^2) = \frac{1}{2}(s_1^2+s_2^2+s_3^2)$，其中 $s_i$ 是主[偏应力](@entry_id:163323)。可以证明 [@problem_id:2659327]：

$$
\tau_{\mathrm{oct}}^2 = \frac{2}{3}J_2
$$

这个关系是[固体力学](@entry_id:164042)，特别是塑性力学中的一个基石。它表明 $\tau_{\mathrm{oct}}$ 本质上是 $J_2$ 的一种度量，而 $J_2$ 正是许多[屈服准则](@entry_id:193897)（如[von Mises屈服准则](@entry_id:174339)）的核心。$\tau_{\mathrm{oct}}$ 作为[应力不变量](@entry_id:170526)，代表了一种平均或有效的剪应力水平，对于描述不依赖于方向的材料行为（如[塑性流动](@entry_id:201346)）非常有用。

### [最大剪应力](@entry_id:181794)与[八面体剪应力](@entry_id:200691)的比较

学生们常常混淆 $\tau_{\max}$ 和 $\tau_{\mathrm{oct}}$。必须明确，它们是两个不同的物理量，作用在不同的平面上，衡量了剪应力状态的不同方面 [@problem_id:2906445]。
- **作用平面不同**：$\tau_{\max}$ 作用于平分最大和最小主应力轴的平面上；而 $\tau_{\mathrm{oct}}$ 作用于与三个主轴等角度倾斜的八面体平面上。
- **数值大小不同**：一般而言，$\tau_{\max}$ 和 $\tau_{\mathrm{oct}}$ 的值不相等。可以严格证明，对于任意应力状态，总有不等式成立 [@problem_id:2659309]：

$$
\tau_{\mathrm{oct}} \le \tau_{\max}
$$

等号仅在一种特殊情况下成立：即[静水应力](@entry_id:186327)状态 ($\sigma_1 = \sigma_2 = \sigma_3$)。在这种状态下，所有平面上的剪应力均为零，因此 $\tau_{\mathrm{oct}} = \tau_{\max} = 0$。

尽管两者不相等，但它们的比值被限制在一个相当窄的范围内。可以证明，对于所有非[静水应力](@entry_id:186327)状态，该比值的上确界为 [@problem_id:2659309]：

$$
\sup \left( \frac{\tau_{\mathrm{oct}}}{\tau_{\max}} \right) = \frac{2\sqrt{2}}{3} \approx 0.943
$$

这个最大值在单轴或纯剪等两个主应力相等的应力状态下达到。同时，其最小值为 $\sqrt{2/3} \approx 0.816$。这个比值总是在 $0.816$ 和 $0.943$ 之间，说明 $\tau_{\mathrm{oct}}$ 总是与 $\tau_{\max}$ 的大小相当。这从数学上解释了为何基于[最大剪应力理论](@entry_id:190279)（[Tresca准则](@entry_id:167002)）和基于[八面体剪应力](@entry_id:200691)理论（[von Mises准则](@entry_id:164472)）的[材料屈服](@entry_id:751736)预测结果总是非常接近。

### 高级主题：偏应力状态的完整描述

我们已经看到，[偏应力张量](@entry_id:267642)的第二[不变量](@entry_id:148850) $J_2$（或等效的 $\tau_{\mathrm{oct}}$）描述了偏应力状态的“大小”或“强度”。然而，要完整地描述一个偏应力状态的“类型”（例如，是更接近[单轴拉伸](@entry_id:188287)还是纯剪），还需要另一个[不变量](@entry_id:148850)，即[偏应力张量](@entry_id:267642)的第三[不变量](@entry_id:148850) $J_3 = \det(\mathbf{s})$。

为了更几何化地理解，可以引入一个称为**[罗德角](@entry_id:191590)**（Lode angle）$\theta$ 的参数，它将 $J_2$ 和 $J_3$ 组合在一起 [@problem_id:2659354]：

$$
\cos(3\theta) = \frac{3\sqrt{3}}{2} \frac{J_3}{J_2^{3/2}}
$$

[罗德角](@entry_id:191590) $\theta$ 描述了应力状态在“$\pi$ 平面”（一个与[静水压力](@entry_id:275365)轴垂直的平面）上的形状特征。例如，在主偏[应力空间](@entry_id:199156)中，不同的 $\theta$ 值对应于从“[偏应力](@entry_id:163323)三轴拉伸”到“偏应力三轴压缩”的不同状态。

通过求解[偏应力张量](@entry_id:267642)的[特征方程](@entry_id:265849)，可以得到主偏应力 $s_1, s_2, s_3$ 完全由 $J_2$ 和 $\theta$ 参数化的优美表达式 [@problem_id:2659354]：

$$
\begin{pmatrix} s_1  s_2  s_3 \end{pmatrix} = \begin{pmatrix} 2\sqrt{\dfrac{J_{2}}{3}}\,\cos\theta  2\sqrt{\dfrac{J_{2}}{3}}\,\cos\!\left(\theta-\dfrac{2\pi}{3}\right)  2\sqrt{\dfrac{J_{2}}{3}}\,\cos\!\left(\theta+\dfrac{2\pi}{3}\right) \end{pmatrix}
$$

这个结果揭示了一个深刻的结构：任何[偏应力](@entry_id:163323)状态（不考虑其空间朝向）都可以由两个标量完全确定：一个代表“半径”或“大小”的量（如 $\sqrt{J_2}$ 或 $\tau_{\mathrm{oct}}$），以及一个代表“角度”或“形状”的量（[罗德角](@entry_id:191590) $\theta$）。这种描述在高级塑性力学和材料本构理论中具有至关重要的作用。