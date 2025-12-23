## 引言
在固体力学领域，准确描述材料在外力作用下如何从可恢复的弹性变形过渡到永久的塑性变形，是理解结构行为、预测[材料失效](@entry_id:160997)和优化工程设计的核心。[弹塑性](@entry_id:193198)[应变分解](@entry_id:186005)是为解决这一挑战而提出的基石性概念。它提供了一个强大而优雅的理论框架，用以在数学上清晰地分离材料响应中的可逆与不可逆部分，从而为建立复杂的材料本构模型奠定了基础。本文旨在系统性地剖析[弹塑性](@entry_id:193198)[应变分解](@entry_id:186005)的理论内涵、应用广度与实践方法。

本文将引导读者循序渐进地掌握这一关键理论。在第一章**“原理与机制”**中，我们将从最基本的[运动学](@entry_id:173318)假设出发，构建基于[热力学原理](@entry_id:142232)的自洽[本构方程](@entry_id:138559)，并详细介绍[屈服准则](@entry_id:193897)、[流动法则](@entry_id:177163)、硬化规律以及数值实现中的[返回映射算法](@entry_id:168456)等核心要素。随后，在第二章**“应用与跨学科联系”**中，我们将展示这一理论框架如何应用于解决从岩土工程的压力敏感性、制造业的各向异性成形，到结构[疲劳寿命预测](@entry_id:197711)和微观织构演化等多样化的实际问题。最后，在第三章**“动手实践”**中，通过一系列精心设计的计算练习，读者将有机会亲手应用所学知识，将抽象的理论转化为具体的分析能力。通过这三个层次的深入学习，您将对[弹塑性](@entry_id:193198)[应变分解](@entry_id:186005)建立起一个全面而深刻的理解。

## 原理与机制

### 基本运动学假设：应变增量分解

在固体力学的研究中，描述材料从弹性变形到塑性变形的转变是一个核心挑战。在[小变形理论](@entry_id:174991)框架下，一个关键的出发点是**加法[应变分解](@entry_id:186005)**（additive strain decomposition）的[运动学](@entry_id:173318)假设。该假设提出，一个质点的总[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon}$ 可以分解为一个可恢复的**[弹性应变](@entry_id:189634)** $\boldsymbol{\varepsilon}^e$ 和一个不可恢复的**塑性应变** $\boldsymbol{\varepsilon}^p$ 之和：

$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p
$$

这一假设构成了经典小应变塑性理论的基石 。从物理上看，$\boldsymbol{\varepsilon}^e$ 描述了当外力移除后能够完全恢复的变形部分，它与材料[晶格](@entry_id:196752)的弹性拉伸或压缩相关。而 $\boldsymbol{\varepsilon}^p$ 则代表了永久变形，如[金属中的位错](@entry_id:188503)滑移等微观机制导致，即使在卸载后这部分应变依然存在。

值得强调的是，加法分解是小应变、小转动（即[位移梯度](@entry_id:165352) $\nabla \boldsymbol{u}$ 的范数 $\lVert \nabla \boldsymbol{u} \rVert \ll 1$）情况下的一个[运动学](@entry_id:173318)近似。在更普适的有限变形理论中，基本的[运动学分解](@entry_id:751020)是针对**变形梯度** $\mathbf{F}$ 的**[乘法分解](@entry_id:199514)** ：

$$
\mathbf{F} = \mathbf{F}^e \mathbf{F}^p
$$

这里，$\mathbf{F}^p$ 将材料从初始参考构型映射到一个假想的、无应力的**[中间构型](@entry_id:193000)**，而 $\mathbf{F}^e$ 则将此[中间构型](@entry_id:193000)映射到最终的、承受应力的当前构型。只有当所有变形梯度都接近单位张量时，[乘法分解](@entry_id:199514)才能线性化为应变的加法分解 。在有限变形中，一般不存在能够使得[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E}$ 满足 $\mathbf{E} = \mathbf{E}^e + \mathbf{E}^p$ 的简单加法关系，因为分解中会出现涉及 $\mathbf{F}^e$ 和 $\mathbf{F}^p$ 的复杂[交叉](@entry_id:147634)项 。

此外，一个深刻的见解是，通常情况下，分解出的弹性应变 $\boldsymbol{\varepsilon}^e$ 和塑性应变 $\boldsymbol{\varepsilon}^p$ 各自都不是一个**相容应变场**。只有一个它们的和，即总应变 $\boldsymbol{\varepsilon}$，能够从一个单值的连续位移场 $\boldsymbol{u}$ 中导出。这意味着，如果我们将材料卸载至零应力状态，剩下的塑性应变场 $\boldsymbol{\varepsilon}^p$ 通常无法对应一个连续的“塑性[位移场](@entry_id:141476)”。这在数学上表现为 $\boldsymbol{\varepsilon}^p$ 的不相容性（$\text{inc}(\boldsymbol{\varepsilon}^p) \neq \mathbf{0}$）。因此，将 $\boldsymbol{\varepsilon}^p$ 视为一个描述材料内部状态（例如，[位错密度](@entry_id:161592)和[分布](@entry_id:182848)）的**内变量**，而不是一个简单的运动学量，是更为恰当和深刻的理解 。同样地，塑性应变的累积是一个依赖于加载历史的过程，因此 $\boldsymbol{\varepsilon}^p$ 是一个**路径依赖**的量，而不是一个[状态函数](@entry_id:137683) 。

### [热力学](@entry_id:141121)框架与本构关系

为了建立一个自洽的本构理论，我们必须将[运动学](@entry_id:173318)假设与[热力学原理](@entry_id:142232)相结合。在[等温过程](@entry_id:143096)中，热力学第二定律简化为 Clausius-Duhem 不等式，即材料内部的[功率耗散](@entry_id:264815)必须非负：

$$
\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0
$$

其中 $\boldsymbol{\sigma}$ 是柯西[应力张量](@entry_id:148973)，$\dot{\boldsymbol{\varepsilon}}$ 是总[应变率](@entry_id:154778)，$\psi$ 是单位体积的亥姆霍兹自由能（或称[应变能密度](@entry_id:200085)）。

根据内变量理论，自由能 $\psi$ 是当前状态的函数，其状态变量应包括可恢复的变形量和描述内部结构的内变量。在[弹塑性](@entry_id:193198)理论中，我们选择[弹性应变](@entry_id:189634) $\boldsymbol{\varepsilon}^e$ 和一组代表[硬化](@entry_id:177483)状态的内变量 $\boldsymbol{\alpha}$ 作为状态变量，即 $\psi = \hat{\psi}(\boldsymbol{\varepsilon}^e, \boldsymbol{\alpha})$。将其时间导数 $\dot{\psi} = \frac{\partial \hat{\psi}}{\partial \boldsymbol{\varepsilon}^e} : \dot{\boldsymbol{\varepsilon}}^e + \frac{\partial \hat{\psi}}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}}$ 和应变率分解 $\dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^e + \dot{\boldsymbol{\varepsilon}}^p$ 代入[耗散不等式](@entry_id:188634)，我们得到：

$$
\left( \boldsymbol{\sigma} - \frac{\partial \hat{\psi}}{\partial \boldsymbol{\varepsilon}^e} \right) : \dot{\boldsymbol{\varepsilon}}^e + \left( \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p - \frac{\partial \hat{\psi}}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}} \right) \ge 0
$$

根据 Coleman-Noll 程序，由于弹性过程是可逆的，我们可以任意控制 $\dot{\boldsymbol{\varepsilon}}^e$ 的大小和方向。为了确保不等式对任何过程都成立，$\dot{\boldsymbol{\varepsilon}}^e$ 的系数必须为零。这给出了应力的本构关系：

$$
\boldsymbol{\sigma} = \frac{\partial \hat{\psi}}{\partial \boldsymbol{\varepsilon}^e}
$$

这个关系式是一个核心结论：**应力完全由弹性应变决定** 。塑性应变 $\boldsymbol{\varepsilon}^p$ 通过改变给定的总应变 $\boldsymbol{\varepsilon}$ 中[弹性应变](@entry_id:189634) $\boldsymbol{\varepsilon}^e = \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^p$ 的部分，从而间接影响应力。这也明确地说明了为何一个简单的**应力加法分解**（例如，$\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon}^e + \mathbb{C}:\boldsymbol{\varepsilon}^p$）是**不正确**的，因为它将导致 $\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon}$，这描述的是一个纯弹性材料，完全忽略了塑性的本质 。

在应力本构关系确定后，[耗散不等式](@entry_id:188634)简化为[塑性耗散](@entry_id:201273)率 $\mathcal{D}_p$ 必须非负：

$$
\mathcal{D}_p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p - \frac{\partial \hat{\psi}}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}} \ge 0
$$

这个不等式将成为我们建立[塑性流动](@entry_id:201346)和硬化演化规律的基石。对于线弹性材料，$\psi = \frac{1}{2} \boldsymbol{\varepsilon}^e : \mathbb{C} : \boldsymbol{\varepsilon}^e$，其中 $\mathbb{C}$ 是[四阶弹性张量](@entry_id:188318)。此时应力关系简化为我们熟悉的胡克定律 $\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}^e$。应力率与应变率的关系则为 $\dot{\boldsymbol{\sigma}} = \mathbb{C} : \dot{\boldsymbol{\varepsilon}}^e = \mathbb{C} : (\dot{\boldsymbol{\varepsilon}} - \dot{\boldsymbol{\varepsilon}}^p)$，这构成了率形式本构模型的出发点。

### 塑性的起始与演化

一个完整的塑性模型需要回答三个基本问题：何时发生塑性变形（[屈服准则](@entry_id:193897)），塑性应变如何演化（[流动法则](@entry_id:177163)），以及屈服条件本身如何随塑性变形而改变（[硬化](@entry_id:177483)规律）。

#### 屈服准则：定义弹性域

材料的弹性行为范围由一个在[应力空间](@entry_id:199156)中定义的**[屈服面](@entry_id:175331)**界定。我们定义一个**[屈服函数](@entry_id:167970)** $f(\boldsymbol{\sigma}, \boldsymbol{q})$，其中 $\boldsymbol{q}$ 是一组描述硬化状态的内变量。弹性域由不等式 $f(\boldsymbol{\sigma}, \boldsymbol{q}) \le 0$ 定义。当应力状态满足 $f  0$ 时，材料处于弹性状态；当 $f=0$ 时，材料达到屈服极限，可能发生[塑性流动](@entry_id:201346)；而 $f > 0$ 的状态是不可允许的。

对于金属等延性材料，一个广泛使用的屈服准则是 **von Mises 准则**。该准则假设[塑性流动](@entry_id:201346)是由**偏应力**（deviatoric stress）$\mathbf{s} = \boldsymbol{\sigma} - \frac{1}{3}\text{tr}(\boldsymbol{\sigma})\mathbf{I}$ 引起的，而与静水压力无关。其[屈服函数](@entry_id:167970)可以写成[偏应力](@entry_id:163323)第二[不变量](@entry_id:148850) $J_2 = \frac{1}{2} \mathbf{s}:\mathbf{s}$ 的形式：

$$
f(\boldsymbol{\sigma}, \kappa) = \sqrt{3 J_2} - \sigma_y(\kappa) \le 0
$$

其中，$\sigma_y(\kappa)$ 是材料当前的单轴屈服强度，$\kappa$ 是一个标量[硬化](@entry_id:177483)变量。量 $\sigma_{\text{eq}} = \sqrt{3 J_2}$ 被称为 von Mises [等效应力](@entry_id:749064)。用主应力 $\sigma_1, \sigma_2, \sigma_3$ 表示，该准则等价于 ：

$$
\sigma_{\text{eq}} = \sqrt{\frac{1}{2}[(\sigma_1-\sigma_2)^2 + (\sigma_2-\sigma_3)^2 + (\sigma_3-\sigma_1)^2]} = \sigma_y(\kappa)
$$

另一个重要的准则是 **Tresca 准则**，它假设当[最大剪应力](@entry_id:181794)达到临界值时材料开始屈服。用[主应力](@entry_id:176761)表示为：

$$
\frac{1}{2} \max(|\sigma_1-\sigma_2|, |\sigma_2-\sigma_3|, |\sigma_3-\sigma_1|) = \frac{\sigma_y(\kappa)}{2}
$$

在以主应力为坐标的偏应力平面（$\pi$ 平面）上，von Mises 屈服面是一个圆形，表明其屈服行为不依赖于应力状态的“模式”（由 Lode 角 $\theta$ 度量）。而 Tresca 屈服面是一个正六边形，其屈服行为在不同区域依赖于不同的[主应力](@entry_id:176761)差，表现出对 Lode 角的依赖性 。

#### 流动法则：塑性应变的方向

当应力状态达到[屈服面](@entry_id:175331)时，塑性应变开始演化。**[流动法则](@entry_id:177163)**（flow rule）规定了塑性[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}^p$ 的方向。在**关联塑性**（associative plasticity）理论中，我们假设塑性应变率的方向与[屈服面](@entry_id:175331)在当前应力点的外[法线](@entry_id:167651)方向相同。这被称为**法向[流动法则](@entry_id:177163)**（normality rule）：

$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$

其中 $\dot{\lambda} \ge 0$ 是一个待定的非负标量，称为**塑性乘子率**（plastic multiplier rate）。它的值在弹性变形时为零，在塑性加载时为正。

应用关联[流动法则](@entry_id:177163)于 von Mises 准则，由于其[屈服函数](@entry_id:167970) $f = \sqrt{3J_2} - \sigma_y(\kappa)$ 只依赖于偏应力 $\mathbf{s}$，其对应力 $\boldsymbol{\sigma}$ 的梯度 $\frac{\partial f}{\partial \boldsymbol{\sigma}}$ 也是一个[偏张量](@entry_id:185837)。这意味着塑性应变率的迹为零：

$$
\text{tr}(\dot{\boldsymbol{\varepsilon}}^p) = \text{tr}\left(\dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}\right) = \dot{\lambda} \, \frac{\partial f}{\partial \sigma_{kk}} = 0
$$

这表明，基于 von Mises 准则的关联塑性流动是体积不可压缩的，即**[塑性流动](@entry_id:201346)保持体积不变** 。这与[金属塑性](@entry_id:176585)变形主要由[位错滑移](@entry_id:275474)主导的物理事实高度吻合。然而，需要注意的是，塑性体积[不可压缩性](@entry_id:274914)是该特定[本构模型](@entry_id:174726)（von Mises + 关联流动）的一个推论，而不是加法[应变分解](@entry_id:186005)这一[运动学](@entry_id:173318)假设的先决条件。对于土壤、岩石等材料，其塑性变形可能伴随着显著的体积变化（剪胀或[压实](@entry_id:161543)），它们的模型就需要采用能描述体积塑性应变的[屈服函数](@entry_id:167970)（如 Drucker-Prager 或 Cam-Clay 模型）。

#### [硬化](@entry_id:177483)：[屈服面](@entry_id:175331)的演化

大多数金属材料在经历塑性变形后，其屈服强度会提高，这种现象称为**[加工硬化](@entry_id:160669)**（work hardening）。在理论模型中，这通过[屈服面](@entry_id:175331)随塑性变形的演化来描述。最简单的[硬化](@entry_id:177483)模型是**[各向同性硬化](@entry_id:164486)**，即[屈服面](@entry_id:175331)在应力空间中均匀扩大，而不改变其形状和中心位置。这通过让屈服强度 $\sigma_y$ 成为某个累积塑性度量 $\kappa$ 的函数来实现。一个常用的线性[各向同性硬化](@entry_id:164486)法则是 ：

$$
\sigma_y(\kappa) = \sigma_{y0} + H\kappa
$$

其中 $\sigma_{y0}$ 是初始屈服强度，$H$ 是硬化模量。累积塑性应变 $\kappa$ 通常与塑性功或等效塑性应变率相关，例如，定义 $\dot{\kappa} = \sqrt{\frac{2}{3}\dot{\boldsymbol{\varepsilon}}^p : \dot{\boldsymbol{\varepsilon}}^p}$。

### 完整的率无关塑性理论体系

将屈服准则、[流动法则](@entry_id:177163)和[硬化](@entry_id:177483)规律结合在一起，就形成了一个完整的[弹塑性](@entry_id:193198)本构模型。其运行逻辑由一组被称为加载/卸载条件的代数关系控制。

#### 加载/卸载条件（[Kuhn-Tucker 条件](@entry_id:185881)）

对于率无关塑性，塑性乘子率 $\dot{\lambda}$ 和[屈服函数](@entry_id:167970) $f$ 之间的关系必须满足以下三个条件，这组条件在数学上被称为 [Karush-Kuhn-Tucker](@entry_id:634966) (KKT) [最优性条件](@entry_id:634091) ：

1.  **屈服条件**: 应力状态必须始终位于弹性域内或其边界上：$f(\boldsymbol{\sigma}, \boldsymbol{q}) \le 0$。
2.  **非负[塑性耗散](@entry_id:201273)**: 塑性流动不可逆，要求塑性乘子率为非负：$\dot{\lambda} \ge 0$。
3.  **[互补条件](@entry_id:747558)**: 塑性流动（$\dot{\lambda}>0$）只可能在应力状态位于[屈服面](@entry_id:175331)上时（$f=0$）发生。如果应力在弹性域内部（$f0$），则必无[塑性流动](@entry_id:201346)（$\dot{\lambda}=0$）。这两个论断可以简洁地写作：$\dot{\lambda} f = 0$。

这三个条件构成了[弹塑性](@entry_id:193198)模型的“逻辑开关”。此外，当塑性加载持续进行时（即 $\dot{\lambda} > 0$），应力点必须停留在不断演化的[屈服面](@entry_id:175331)上。这意味着[屈服函数](@entry_id:167970)的时间导数必须为零，这被称为**[一致性条件](@entry_id:637057)**（consistency condition）：

$$
\dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \dot{\boldsymbol{\sigma}} + \frac{\partial f}{\partial \boldsymbol{q}} \cdot \dot{\boldsymbol{q}} = 0 \quad (\text{当 } f=0 \text{ 且 } \dot{\lambda}>0)
$$

[一致性条件](@entry_id:637057)是求解塑性乘子率 $\dot{\lambda}$ 的关键方程 。

#### 连续[弹塑性切线模量](@entry_id:189492)

在塑性加载过程中，材料的刚度会发生变化。描述应力率 $\dot{\boldsymbol{\sigma}}$ 与总应变率 $\dot{\boldsymbol{\varepsilon}}$ 之间关系的[四阶张量](@entry_id:181350) $\mathbb{C}^{\text{ep}}$ 被称为**连续[弹塑性切线模量](@entry_id:189492)**。我们可以通过联立应力率方程 $\dot{\boldsymbol{\sigma}} = \mathbb{C} : (\dot{\boldsymbol{\varepsilon}} - \dot{\boldsymbol{\varepsilon}}^p)$、[流动法则](@entry_id:177163) $\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}$ 以及[一致性条件](@entry_id:637057) $\dot{f}=0$ 来推导它。

通过一致性条件，我们可以将 $\dot{\lambda}$ 表示为 $\dot{\boldsymbol{\varepsilon}}$ 的线性函数，然后将其代回应力率方程，最终得到 $\dot{\boldsymbol{\sigma}} = \mathbb{C}^{\text{ep}} : \dot{\boldsymbol{\varepsilon}}$。对于关联塑性，其一般形式为 ：

$$
\mathbb{C}^{\text{ep}} = \mathbb{C} - \frac{(\mathbb{C} : \frac{\partial f}{\partial \boldsymbol{\sigma}}) \otimes (\frac{\partial f}{\partial \boldsymbol{\sigma}} : \mathbb{C})}{\frac{\partial f}{\partial \boldsymbol{\sigma}} : \mathbb{C} : \frac{\partial f}{\partial \boldsymbol{\sigma}} - \frac{\partial f}{\partial \boldsymbol{q}} \cdot \frac{\partial \boldsymbol{q}}{\partial \dot{\lambda}}}
$$

这个表达式明确显示了在[塑性流动](@entry_id:201346)期间，材料的有效刚度 $\mathbb{C}^{\text{ep}}$ 是在弹性刚度 $\mathbb{C}$ 的基础上减去一个由塑性流动引起的“软化”项。

#### 一个说明性示例：[单轴拉伸](@entry_id:188287)

为了更具体地理解上述理论，我们考虑一个受[单轴拉伸](@entry_id:188287)的杆件，其材料服从带有线性[各向同性硬化](@entry_id:164486)（硬化模量为 $H$）的 von Mises 准则。杨氏模量为 $E$，初始屈服应力为 $\sigma_{y0}$ 。

1.  **弹性阶段** ($\sigma \le \sigma_{y0}$): 行为是纯弹性的，$\sigma = E\varepsilon$。塑性应变为零，$\varepsilon^p = 0$。

2.  **塑性阶段** ($\sigma > \sigma_{y0}$):
    *   在[单轴拉伸](@entry_id:188287)下，von Mises [等效应力](@entry_id:749064) $\sigma_{\text{eq}}$ 等于轴向应力 $\sigma$。
    *   屈服条件变为 $\sigma = \sigma_y(\kappa) = \sigma_{y0} + H\kappa$。
    *   关联[流动法则](@entry_id:177163)和硬化法则表明，累积塑性应变 $\kappa$ 等于轴向塑性应变 $\varepsilon^p$。因此，$\sigma = \sigma_{y0} + H\varepsilon^p$。
    *   总[应变分解](@entry_id:186005)为 $\varepsilon = \varepsilon^e + \varepsilon^p = \frac{\sigma}{E} + \varepsilon^p$。
    *   联立以上方程，我们可以得到应力-总应变关系：
        $$
        \sigma(\varepsilon) = \frac{EH}{E+H}\varepsilon + \frac{E\sigma_{y0}}{E+H}
        $$
    *   此时的[切线](@entry_id:268870)模量，即[弹塑性](@entry_id:193198)模量 $E_{\text{ep}}$，为 $\frac{d\sigma}{d\varepsilon} = \frac{EH}{E+H}$。这正是前述[四阶张量](@entry_id:181350) $\mathbb{C}^{\text{ep}}$ 在一维情况下的具体体现。

例如，对于一个材料，其 $E = 210$ GPa, $\sigma_{y0} = 300$ MPa, $H = 4.0$ GPa，当施加的应力达到 $\sigma^*=410$ MPa 时，由于 $\sigma^* > \sigma_{y0}$，材料已进入塑性状态。我们可以从[硬化](@entry_id:177483)法则直接计算出此时的塑性应变 ：

$$
\varepsilon^p = \frac{\sigma^* - \sigma_{y0}}{H} = \frac{410 \, \text{MPa} - 300 \, \text{MPa}}{4000 \, \text{MPa}} = 0.02750
$$

### 计算实现：[返回映射算法](@entry_id:168456)

在[有限元分析](@entry_id:138109)等[数值模拟](@entry_id:137087)中，我们需要在离散的时间（或荷载）步[内积](@entry_id:158127)分上述[本构方程](@entry_id:138559)。最常用和最稳健的方法是基于**[返回映射算法](@entry_id:168456)**（return mapping algorithm）的隐式积分格式。

#### [弹性预测-塑性修正](@entry_id:748860)格式

[返回映射算法](@entry_id:168456)通常包含两个步骤 ：

1.  **弹性预测**: 在一个时间步开始时，我们已知上一步结束时的状态（$\boldsymbol{\sigma}_n, \boldsymbol{\varepsilon}^p_n, \boldsymbol{q}_n$）。对于给定的总应变增量 $\Delta\boldsymbol{\varepsilon}$，我们首先假设整个增量步是纯弹性的。这样计算出的应力被称为**试探应力**（trial stress）：
    $$
    \boldsymbol{\sigma}_{\text{tr}} = \boldsymbol{\sigma}_n + \mathbb{C} : \Delta\boldsymbol{\varepsilon} = \mathbb{C} : (\boldsymbol{\varepsilon}_n^e + \Delta\boldsymbol{\varepsilon})
    $$

2.  **塑性修正**: 接下来，我们用试探应力来检查屈服条件 $f(\boldsymbol{\sigma}_{\text{tr}}, \boldsymbol{q}_n) \le 0$。
    *   如果满足条件，说明弹性假设成立，该步确实是弹性的。最终状态就是试探状态：$\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}_{\text{tr}}$，内变量不变。
    *   如果 $f(\boldsymbol{\sigma}_{\text{tr}}, \boldsymbol{q}_n) > 0$，说明试探应力“穿透”了屈服面，这是不被允许的。弹性假设错误，该步内发生了塑性变形。我们需要进行**塑性修正**，将应力状态“[拉回](@entry_id:160816)”到更新后的[屈服面](@entry_id:175331)上。

对于 J2 塑性，这个修正过程有一个优雅的几何解释，称为**[径向返回](@entry_id:754007)**（radial return）。修正后的偏应力 $s_{n+1}$ 与试探[偏应力](@entry_id:163323) $s_{\text{tr}}$ 方向相同，只是其大小被缩减以满足屈服条件。通过求解离散化的流动和硬化方程，可以得到塑性乘子增量 $\Delta\gamma$ 的封闭解 ：

$$
\Delta\gamma = \frac{f_{\text{tr}}}{3G + H}
$$

其中 $f_{\text{tr}}$ 是在试探应力处计算的[屈服函数](@entry_id:167970)值，$G$ 是剪切模量。一旦求得 $\Delta\gamma$，就可以更新塑性应变和硬化变量，并最终确定步末的真实应力 $\boldsymbol{\sigma}_{n+1}$。值得注意的是，对于 J2 塑性，只有[偏应力](@entry_id:163323)部分被修正，[静水压力](@entry_id:275365)部分保持与试探状态相同。

#### 一致性[切线](@entry_id:268870)模量与收敛性

在[非线性有限元分析](@entry_id:167596)中，求解[全局平衡方程](@entry_id:272290)通常采用牛顿-拉夫逊（[Newton-Raphson](@entry_id:177436)）[迭代法](@entry_id:194857)，该方法需要计算系统刚度矩阵，而刚度矩阵的构建则依赖于[本构关系](@entry_id:186508)在当前状态的[切线](@entry_id:268870)模量。

为了在牛顿法中保持二次收敛的优良特性，必须使用与离散[积分算法](@entry_id:192581)完全一致的[切线](@entry_id:268870)模量。这个模量被称为**[算法切线模量](@entry_id:199979)**或**一致性[切线](@entry_id:268870)模量**（consistent tangent modulus），记为 $\mathbb{A}$ 或 $\mathbb{C}_{\text{alg}}$。它被严格定义为步末应力 $\boldsymbol{\sigma}_{n+1}$ 对步末总应变 $\boldsymbol{\varepsilon}_{n+1}$ 的精确导数 ：

$$
\mathbb{A} := \frac{\partial \boldsymbol{\sigma}_{n+1}}{\partial \boldsymbol{\varepsilon}_{n+1}}
$$

这个导数是通过对整个[返回映射算法](@entry_id:168456)（包括屈服条件的判断和塑性修正的[非线性方程](@entry_id:145852)）进行线性化得到的。一般而言，对于有限大小的时间步 $\Delta t$，一致性[切线](@entry_id:268870)模量 $\mathbb{A}$ **不等于**在步末状态评估的连续[弹塑性](@entry_id:193198)模量 $\mathbb{C}^{\text{ep}}$。这种差异来源于离散化带来的误差。只有在时间步长趋于零的极限情况下，或者在某些特殊情况（如在 J2 塑性中沿固定方向的[比例加载](@entry_id:191744)）下，两者才会相等 。

使用不正确的[切线](@entry_id:268870)模量会导致牛顿迭代的收敛速度下降。一个典型的例子是，如果在塑性加载步中使用弹性刚度 $\mathbb{C}$ 来代替 $\mathbb{A}$，牛顿法的收敛速度将从二次退化为线性 。对于前述的[单轴拉伸](@entry_id:188287)问题，使用弹性模量 $E$ 代替一致性[切线](@entry_id:268870)模量 $C_{\text{alg}} = \frac{EH}{E+H}$ 时，每次迭代的误差缩减率（[线性收敛](@entry_id:163614)因子）将是 $q = 1 - C_{\text{alg}}/E = E/(E+H)$。只要 $H>0$，这个因子就大于零，从而导致[线性收敛](@entry_id:163614) 。这凸显了在[计算塑性力学](@entry_id:171377)中使用正确的一致性[切线](@entry_id:268870)模量的极端重要性。

### 高级主题与推广

小应变理论为理解[弹塑性](@entry_id:193198)行为提供了坚实的基础。然而，当变形或转动变得显著时，必须考虑更复杂的理论。

#### 率形式理论与客观性

当处理[大变形](@entry_id:167243)问题时，我们通常在当前构型下建立本构关系的率形式。一个关键的挑战是，柯西应力张量的时间导数 $\dot{\boldsymbol{\sigma}}$ 并不是一个**客观**的张量率，即它的值会随观察者[参考系](@entry_id:169232)的旋转而改变。一个物理上合理的[本构定律](@entry_id:178936)必须是客观的，即独立于观察者的运动。

为了确保客观性，必须使用一个**[客观应力率](@entry_id:199282)**，它能够消除由材料[刚体转动](@entry_id:191086)引起的应力变化。常见的[客观率](@entry_id:198692)包括**[Jaumann 率](@entry_id:185572)**和 **Green-Naghdi 率**。它们的一般形式为 $\overset{\nabla}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Omega}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Omega}$，其中 $\boldsymbol{\Omega}$ 是一个反对称的[自旋张量](@entry_id:187346)。[Jaumann 率](@entry_id:185572)使用变形的[自旋张量](@entry_id:187346) $W$（速度梯度的反对称部分），而 Green-Naghdi 率使用与极分解中转动张量 $R$ 相关联的自旋 $\boldsymbol{\Omega}^R = \dot{R}R^T$。

在非平凡的变形历史中，不同的[客观率](@entry_id:198692)会导致不同的应力预测。例如，在有限简单[剪切变形](@entry_id:170920)下，材料点的连续转动会导致 $W$ 和 $\boldsymbol{\Omega}^R$ 之间产生显著差异。$W$ 的大小保持恒定，而 $\boldsymbol{\Omega}^R$ 的大小随剪切应变的增加而减小。因此，使用 [Jaumann 率](@entry_id:185572)或 Green-Naghdi 率的[弹塑性](@entry_id:193198)模型会预测出截然不同的[法向应力](@entry_id:260622)演化（即 Poynting 效应）。这说明在有限变形塑性理论中，对[运动学](@entry_id:173318)和本构率形式的选择至关重要。

#### [中间构型](@entry_id:193000)及其模糊性

回到有限变形的[乘法分解](@entry_id:199514) $\mathbf{F} = \mathbf{F}^e \mathbf{F}^p$，[中间构型](@entry_id:193000)的概念虽然在物理上直观（一个卸载后无宏观应力的状态），但在数学上存在一定的模糊性。对于一个各向同性的材料，其[储能函数](@entry_id:197811)只依赖于弹性变形，而不依赖于材料在[中间构型](@entry_id:193000)中的绝对取向。这意味着，我们可以对[中间构型](@entry_id:193000)施加任意一个[刚体转动](@entry_id:191086) $\mathbf{Q} \in \mathrm{SO}(3)$，同时对弹性变形施加一个反向转动，而不会改变最终的应力[状态和](@entry_id:193625)总变形 ：

$$
\mathbf{F}_p \to \mathbf{Q}^{-1}\mathbf{F}_p, \quad \mathbf{F}_e \to \mathbf{F}_e\mathbf{Q}
$$

这种定义上的不唯一性被称为**[规范自由度](@entry_id:160491)**（gauge freedom）。为了使理论完备，必须引入额外的结构或约定来“固定规范”。

在**[晶体塑性](@entry_id:141273)**理论中，这种模糊性被自然地消除了。[中间构型](@entry_id:193000)被赋予了真实的物理结构——[晶格](@entry_id:196752)。此时，任何对[中间构型](@entry_id:193000)的转动 $\mathbf{Q}$ 必须保持[晶格](@entry_id:196752)自身的对称性。因此，连续的[规范自由度](@entry_id:160491) $\mathrm{SO}(3)$ 被缩减为[晶体点群](@entry_id:183880)的离散[子群](@entry_id:146164)。对于对称性最低的三斜晶系，其转动对称群只包含单位元，这意味着[中间构型](@entry_id:193000)的分解是完全唯一的 。

对于宏观各向同性模型，不存在晶格结构，必须通过一个**本构约定**来消除模糊性。一个常见的选择是要求塑性速度梯度 $\mathbf{L}_p = \dot{\mathbf{F}}_p \mathbf{F}_p^{-1}$ 的反对称部分，即**塑性自旋** $\mathbf{W}_p$，恒为零。这个条件为 $\mathbf{F}_p$ 的演化提供了唯一的路径，从而解决了[规范自由度](@entry_id:160491)问题 。