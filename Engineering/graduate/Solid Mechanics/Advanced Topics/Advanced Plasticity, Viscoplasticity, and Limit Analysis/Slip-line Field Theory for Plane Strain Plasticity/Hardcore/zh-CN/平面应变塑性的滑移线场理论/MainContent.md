## 引言
在[固体力学](@entry_id:164042)领域，理解材料在超过[弹性极限](@entry_id:186242)后的行为至关重要。[平面应变塑性](@entry_id:201004)[滑移线场理论](@entry_id:181917)是分析这类大塑性变形问题的一种经典而深刻的解析方法。它为工程师和科学家提供了一套强大的工具，用以揭示材料内部的应力[分布](@entry_id:182848)和流动模式，尤其在金属加工和岩土工程等领域具有不可替代的价值。尽管现代[计算力学](@entry_id:174464)（如有限元法）能够处理复杂的塑性问题，但[滑移线场理论](@entry_id:181917)以其简洁的数学形式和清晰的物理图像，解决了在特定理想化条件下寻求解析解或半解析解的需求，从而为理解塑性变形的内在机制提供了独特的视角。本文旨在全面介绍[滑移线场理论](@entry_id:181917)。我们将从其核心的数学物理基础出发，逐步深入其实际应用。在“原理与机制”一章中，我们将建立理论的基石，推导 Hencky 方程和 Geiringer 方程。接着，在“应用与跨学科联系”一章中，我们将展示该理论如何解决从[压头](@entry_id:141368)接触到挤压成形等一系列经典工程问题，并探讨其与[极限分析](@entry_id:188743)及其他学科的联系。最后，通过“动手实践”中的一系列练习，你将有机会将理论知识转化为解决实际问题的能力。

## 原理与机制

本章旨在系统阐述[平面应变塑性](@entry_id:201004)[滑移线场理论](@entry_id:181917)的核心原理与基本机制。在前一章介绍其背景和应用领域的基础上，我们将深入探讨该理论的[数学物理](@entry_id:265403)基础。我们将从刚塑性材料[本构模型](@entry_id:174726)的关键假设出发，推导控制应[力场](@entry_id:147325)的 governing equations，揭示其双曲特性，并最终建立沿特征线（即滑移线）的[不变量](@entry_id:148850)关系——Hencky 方程。此外，我们还将讨论与之相关的运动学关系（Geiringer 方程）以及[解的唯一性](@entry_id:143619)问题，为后续章节中具体问题的求解奠定坚实的理论基础。

### [平面应变塑性](@entry_id:201004)中的应力状态

[滑移线场理论](@entry_id:181917)建立在一个理想化的模型之上：**刚-[理想塑性](@entry_id:753335)材料 (rigid-perfectly plastic material)**。该模型忽略了弹性变形，认为材料在达到屈服极限之前是完全刚性的；一旦达到屈服，材料便在应力水平保持不变的情况下发生[塑性流动](@entry_id:201346)，即不存在[加工硬化](@entry_id:160669)。我们将在此框架下考虑**平面应变 (plane strain)** 条件。

从[运动学](@entry_id:173318)上定义，[平面应变](@entry_id:167046)意味着物体在面外（设为 $z$ 方向）的应变分量为零，即 $\epsilon_{zz} = \epsilon_{xz} = \epsilon_{yz} = 0$。在刚塑性模型中，由于弹性应变为零，总[应变率](@entry_id:154778)即为塑性应变率 $\dot{\boldsymbol{\epsilon}}^p$。因此，平面应变条件转化为对塑性[应变率](@entry_id:154778)的约束：$\dot{\epsilon}_{zz}^p = 0$, $\dot{\epsilon}_{xz}^p = 0$, $\dot{\epsilon}_{yz}^p = 0$。

这些运动学约束通过**关联[流动法则](@entry_id:177163) (associated flow rule)** 对塑性区的应力状态施加了严格的限制。关联[流动法则](@entry_id:177163)指出，塑性应变率张量 $\dot{\boldsymbol{\epsilon}}^p$ 的方向与[屈服函数](@entry_id:167970) $f(\boldsymbol{\sigma})$ 关于[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的梯度方向一致：
$$ \dot{\boldsymbol{\epsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}} $$
其中 $\dot{\lambda} > 0$ 是一个非负的塑性乘子，在[塑性流动](@entry_id:201346)期间为正。对于与静水压力无关的[屈服准则](@entry_id:193897)（如 von Mises 和 Tresca 准则），$\frac{\partial f}{\partial \boldsymbol{\sigma}}$ 是[偏应力张量](@entry_id:267642) $\mathbf{s}$ 的函数。例如，对于 von Mises 准则，$f = J_2 - k^2$，其中 $J_2 = \frac{1}{2} s_{ij}s_{ij}$ 是偏应力第二[不变量](@entry_id:148850)，我们有 $\frac{\partial f}{\partial \boldsymbol{\sigma}} = \mathbf{s}$。因此，流动法则简化为 $\dot{\epsilon}_{ij}^p = \dot{\lambda} s_{ij}$。

将[平面应变](@entry_id:167046)运动学约束应用于此[流动法则](@entry_id:177163)，我们可以得到关于应力状态的重要结论 ：
1.  由 $\dot{\epsilon}_{zz}^p = 0$ 可得 $\dot{\lambda} s_{zz} = 0$，因为[塑性流动](@entry_id:201346)时 $\dot{\lambda}>0$，所以必然有 $s_{zz} = 0$。
2.  由 $\dot{\epsilon}_{xz}^p = 0$ 和 $\dot{\epsilon}_{yz}^p = 0$ 可得 $s_{xz} = 0$ 和 $s_{yz} = 0$。由于剪应力分量的偏应力部分就是其自身（即 $s_{ij} = \sigma_{ij}$ 当 $i \neq j$），这直接意味着 $\sigma_{xz} = 0$ 和 $\sigma_{yz} = 0$。

$s_{zz}=0$ 的结论尤为重要。根据[偏应力](@entry_id:163323)定义 $s_{zz} = \sigma_{zz} - \frac{1}{3}(\sigma_{xx} + \sigma_{yy} + \sigma_{zz})$，该条件导出：
$$ 2\sigma_{zz} = \sigma_{xx} + \sigma_{yy} \quad \implies \quad \sigma_{zz} = \frac{\sigma_{xx} + \sigma_{yy}}{2} $$
这表明，在 von Mises 材料的[平面应变塑性](@entry_id:201004)流动中，面外[正应力](@entry_id:260622)等于两个面内[正应力](@entry_id:260622)的平均值。这与通常定义为 $\sigma_{zz}=0$ 的**平面应力 (plane stress)** 状态有本质区别。

### 平面应变屈服准则

尽管 von Mises 和 Tresca 准则在三维[应力空间](@entry_id:199156)中形式不同，但在平面应变条件下，它们都可以简化为一种相似的、适用于二维分析的形式。

对于 **von Mises 准则**，其通用形式为 $J_2 = k^2$。在平面应变条件下，利用已推导的 $s_{zz}=0$ 和[塑性不可压缩性](@entry_id:183440)所引出的 $s_{xx} = -s_{yy}$，该准则简化为 ：
$$ J_2 = s_{xx}^2 + s_{xy}^2 = k^2 $$
将偏应力用总应力表示，即 $s_{xx} = \frac{1}{2}(\sigma_{xx} - \sigma_{yy})$ 和 $s_{xy} = \sigma_{xy}$，我们得到平面应变 von Mises [屈服准则](@entry_id:193897)：
$$ \left(\frac{\sigma_{xx} - \sigma_{yy}}{2}\right)^2 + \sigma_{xy}^2 = k^2 $$
或者写作 $(\sigma_{xx}-\sigma_{yy})^{2}+4\sigma_{xy}^{2}=4k^{2}$。

对于 **Tresca 准则**，其核心是[最大剪应力](@entry_id:181794)达到临界值 $k$。在[主应力空间](@entry_id:184388)中，$\max(|\sigma_1-\sigma_2|, |\sigma_2-\sigma_3|, |\sigma_3-\sigma_1|) = 2k$。为了使塑性流动局限于 $1-2$ 平面，通常假设面外[主应力](@entry_id:176761) $\sigma_3$ 是中间主应力，即 $\sigma_1 \ge \sigma_3 \ge \sigma_2$ (或 $\sigma_2 \ge \sigma_3 \ge \sigma_1$)。在此条件下，[最大剪应力](@entry_id:181794)发生在面内，Tresca 准则简化为：
$$ |\sigma_1 - \sigma_2| = 2k $$
这与上述 von Mises 准则用主应力表达的形式 $(\sigma_1-\sigma_2)^2 = 4k^2$ 是等价的。因此，在[平面应变](@entry_id:167046)[滑移线场理论](@entry_id:181917)的框架下，两种准则都导致了相同的面内屈服条件：**面内主应力差的[绝对值](@entry_id:147688)为一个常数 $2k$**。

两种理论的主要区别在于参数 $k$（纯剪切屈服应力）与[单轴拉伸](@entry_id:188287)屈服应力 $\sigma_Y$ 的关系不同 ：
- 对于 **von Mises 准则**，$k = \frac{\sigma_Y}{\sqrt{3}}$。
- 对于 **Tresca 准则**，$k = \frac{\sigma_Y}{2}$。

在后续推导中，我们仅需使用关系式 $|\sigma_1 - \sigma_2| = 2k$，这使得理论具有相当的普适性，只需在最后代入特定材料准则对应的 $k$ 值即可。

### 应[力场](@entry_id:147325)方程及其双曲特性

在塑性区内，我们有两个[静力平衡](@entry_id:163498)方程（不计体力）和上述的一个屈服方程，共有三个方程来求解三个未知的面[内应力](@entry_id:193721)分量 ($\sigma_x, \sigma_y, \tau_{xy}$)。这是一个封闭的（静定的）应力问题。

为了求解这个[方程组](@entry_id:193238)，一个关键步骤是**应力[参数化](@entry_id:272587)**。我们不再直接求解 $\sigma_x, \sigma_y, \tau_{xy}$，而是引入两个新的场变量：**[平均应力](@entry_id:751819) (mean stress)** $p$ 和**[主应力方向](@entry_id:753737)角 (stress angle)** $\theta$。其中，$p$ 通常定义为静水压力的相反数，$\theta$ 为最大[主应力](@entry_id:176761) $\sigma_1$ 方向与 $x$ 轴的夹角。
$$ p = -\frac{\sigma_1 + \sigma_2}{2} $$
结合屈服条件 $\sigma_1 - \sigma_2 = 2k$ (假设 $\sigma_1 \ge \sigma_2$)，我们可以将主应力表示为：
$$ \sigma_1 = -p + k $$
$$ \sigma_2 = -p - k $$

利用 Mohr 圆的几何关系或标准应力变换公式，可以将[笛卡尔坐标系](@entry_id:169789)下的应力分量用 $p$ 和 $\theta$ 表示 ：
$$ \sigma_x = \frac{\sigma_1 + \sigma_2}{2} + \frac{\sigma_1 - \sigma_2}{2}\cos(2\theta) = -p + k\cos(2\theta) $$
$$ \sigma_y = \frac{\sigma_1 + \sigma_2}{2} - \frac{\sigma_1 - \sigma_2}{2}\cos(2\theta) = -p - k\cos(2\theta) $$
$$ \tau_{xy} = \frac{\sigma_1 - \sigma_2}{2}\sin(2\theta) = k\sin(2\theta) $$
(注意：这里的符号约定与某些文献可能不同，例如将 $p$ 定义为 $p = (\sigma_x+\sigma_y)/2$，但这只会影响推导过程中的符号，最终的物理结论和方程结构不变。)

现在，我们将这组[参数化](@entry_id:272587)的应力表达式代入二维[静力平衡](@entry_id:163498)方程 ：
$$ \frac{\partial \sigma_x}{\partial x} + \frac{\partial \tau_{xy}}{\partial y} = 0 \quad \implies \quad -\frac{\partial p}{\partial x} - 2k\sin(2\theta)\frac{\partial \theta}{\partial x} + 2k\cos(2\theta)\frac{\partial \theta}{\partial y} = 0 $$
$$ \frac{\partial \tau_{xy}}{\partial x} + \frac{\partial \sigma_y}{\partial y} = 0 \quad \implies \quad 2k\cos(2\theta)\frac{\partial \theta}{\partial x} - \frac{\partial p}{\partial y} + 2k\sin(2\theta)\frac{\partial \theta}{\partial y} = 0 $$
我们得到了一个关于两个未知场变量 $p(x,y)$ 和 $\theta(x,y)$ 的一阶[拟线性偏微分方程](@entry_id:164345)组。对此[方程组](@entry_id:193238)进行特征分析可以发现，它属于**双曲型 (hyperbolic)**。这与弹性问题中的椭圆型方程有着根本性的区别，也是[滑移线场理论](@entry_id:181917)众多独特现象（如不连续解、非唯一解）的数学根源。

### 特征线与 Hencky 方程

[双曲型方程组](@entry_id:260647)的显著特征是其解的信息沿着特定的曲线——**特征线 (characteristics)** ——传播。对于上述应力[方程组](@entry_id:193238)，可以证明存在两个实特征方向。这些特征线的斜率 $\frac{dy}{dx}$ 满足 ：
$$ \frac{dy}{dx} = \tan(\theta \pm \frac{\pi}{4}) $$
这揭示了一个深刻的物理意义：应[力场](@entry_id:147325)方程的特征线，在物理平面上恰好是材料中**[最大剪应力](@entry_id:181794)方向**的轨迹。这两族相互正交的曲线，就是我们所说的**滑移线 (slip-lines)**。我们通常将它们标记为 $\alpha$-线和 $\beta$-线。例如，约定[切线](@entry_id:268870)方向与 $x$ 轴夹角为 $\theta - \pi/4$ 的是 $\alpha$-线，夹角为 $\theta + \pi/4$ 的是 $\beta$-线。

从物理上讲，滑移线代表了材料最容易发生剪切滑动的方向。由于最大[主应力](@entry_id:176761) $\sigma_1$ 和最小主应力 $\sigma_2$ 作用的平面上剪应力为零，而[最大剪应力](@entry_id:181794)作用的平面与[主应力](@entry_id:176761)平面成 $\pm 45^\circ$ 角，因此滑移[线与](@entry_id:177118)[主应力方向](@entry_id:753737)成 $\pm \pi/4$ 的角度。由于这两个方向相差 $90^\circ$，因此 $\alpha$ 和 $\beta$ 两族滑移线在任何点都是**相互正交**的 。

[双曲系统](@entry_id:260647)的另一个优点是，沿着特征线，复杂的[偏微分方程](@entry_id:141332)可以简化为[常微分方程](@entry_id:147024)。通过对[方程组](@entry_id:193238)进行适当的线性组合，可以推导出沿滑移线的关系式 ：
- 沿 $\alpha$-线: $dp + 2k d\theta = 0$
- 沿 $\beta$-线: $dp - 2k d\theta = 0$

对上述关系式积分，我们便得到了[滑移线场理论](@entry_id:181917)中用于求解应[力场](@entry_id:147325)的两个核心关系式——**Hencky 方程 (Hencky's equations)**，也称为特征[不变量](@entry_id:148850)：
- **沿任意一条 $\alpha$-线，$p + 2k\theta$ 为常数。**
- **沿任意一条 $\beta$-线，$p - 2k\theta$ 为常数。**

Hencky 方程的物理意义是：当沿着一条滑移线移动时，平均应力 $p$ 的变化量与[主应力方向](@entry_id:753737)的偏转角 $\theta$ 的变化量成正比。这一简洁而深刻的关系是构建和分析滑移线场的基础，使得我们能够通过几何方法或[数值积分](@entry_id:136578)来确定整个塑性区的应力[分布](@entry_id:182848)。

### [塑性流动](@entry_id:201346)的[运动学](@entry_id:173318)：Geiringer 方程与[速度图](@entry_id:195718)

除了应[力场](@entry_id:147325)，完整的解还需要确定速度场 $(u, v)$。运动学由两个条件控制：
1.  **[不可压缩性](@entry_id:274914)**: $\dot{\epsilon}_{xx} + \dot{\epsilon}_{yy} = \frac{\partial u}{\partial x} + \frac{\partial v}{\partial y} = 0$。
2.  **[流动法则](@entry_id:177163)**: 它要求应变率[主方向](@entry_id:276187)与应力主方向重合，这进一步导出一个条件：沿着滑移线方向的[线元](@entry_id:196833)伸长率为零。

这两个条件可以导出关于速度分量沿滑移线变化的方程，即 **Geiringer 方程**。它构成了速度场的[双曲型方程组](@entry_id:260647)，其特征线与应[力场](@entry_id:147325)的特征线完全相同，都是滑移线。

在求解某些问题时，直接处理速度场可能非常复杂。**[速度图](@entry_id:195718)法 (hodograph method)** 提供了一种巧妙的替代方案 。该方法将速度分量 $(u, v)$ 视作自变量，而将空间坐标 $(x, y)$ 视作因变量，即求解 $x(u,v)$ 和 $y(u,v)$。经过这种变换，描述[运动学](@entry_id:173318)的[方程组](@entry_id:193238)在[速度图](@entry_id:195718)平面 $(u,v)$ 上变为一个线性的双曲型系统。一个非凡的结果是，这个新系统的特征线——即物理滑移线在[速度图](@entry_id:195718)上的映射——同样是**相互正交**的。这个特性使得[速度图](@entry_id:195718)成为分析[复杂流动](@entry_id:747569)问题（特别是当速度边界条件比应力边界条件更简单时）的一个强有力的几何工具。

### 关于[适定性](@entry_id:148590)与唯一性

刚-[理想塑性](@entry_id:753335)模型的简单性是以付出一定代价为代价的。由于模型中完全没有弹性（即[弹性模量](@entry_id:198862) $E \to \infty$）和任何形式的[硬化](@entry_id:177483)，导致应[力场](@entry_id:147325)控制方程是双曲型的 。这与包含弹性的、通常是椭圆型的问题有着本质区别，并直接引发了解的**唯一性 (uniqueness)** 问题。

对于[双曲型方程](@entry_id:145657)的边值问题，其[解的唯一性](@entry_id:143619)不总能得到保证。特别地，当边界的一部分本身就是一条特征线（即一条滑移线）时，问题可能会变得不适定 。在这种情况下，仅在边界上给定牵[引力](@entry_id:175476)（应力）条件可能不足以唯一确定邻域内的解。这是因为信息是沿着特征线传播的，给定在一条特征线上的数据，无法完全约束从该线出发的共轭特征线族的形态。因此，可能存在多个不同的、均满足平衡、屈服和边界条件的滑移线场。这并非纯粹的数学瑕疵，在有限元数值计算中，它可能表现为解对网格的极端依赖性，是理想模型“病态”的一种体现 。

理解这种非唯一性的一个重要视角是将其视为一种**正则化 (regularization)** 的极限。在更符合物理现实的模型中，例如引入微小的线弹性、应变硬化或[应变率敏感性](@entry_id:188216)（[粘塑性](@entry_id:165397)），都会改变控制方程的数学类型（通常变为椭圆型或抛物型），从而恢复[解的唯一性](@entry_id:143619)。理想刚塑性模型的多个可能解，可以被看作是这个唯一的“正则化”解在[弹性模量](@entry_id:198862)趋于无穷、硬化模量或粘性系数趋于零时的不同极限情况 。这种观点不仅有助于我们理解理想模型的局限性，也为在多种可能的滑移线场解中进行选择提供了物理依据。