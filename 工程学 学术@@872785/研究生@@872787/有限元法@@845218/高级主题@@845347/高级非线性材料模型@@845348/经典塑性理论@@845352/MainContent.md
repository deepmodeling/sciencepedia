## 引言
经典塑性理论是[固体力学](@entry_id:164042)的重要基石，它为我们理解和预测材料在超过其[弹性极限](@entry_id:186242)后的力学行为提供了数学框架。当工程结构与部件承受极端载荷时，单纯的[弹性理论](@entry_id:184142)已不足以描述其永久变形和最终失效的过程，这正是塑性理论所要解决的核心知识缺口。它不仅对于确保结构在极限载荷下的安全性至关重要，也是现代材料加工、制造工艺模拟和结构耐久性评估等领域的理论基础。

本文将引导读者深入探索这一领域。在“原理与机制”一章中，我们将从最基本的变形分解和[应力不变量](@entry_id:170526)出发，逐步构建起一个完整塑性本构模型的各个核心要素：定义弹性边界的屈服准则，描述屈服面演化的硬化定律，以及决定塑性变形方向的[流动法则](@entry_id:177163)，并最终将其整合到有限元计算的算法框架中。随后，在“应用与跨学科连接”一章，我们将展示这些理论在结构工程、[材料科学](@entry_id:152226)乃至[地球科学](@entry_id:749876)中的实际应用，揭示其强大的问题解决能力和广泛的学科[交叉](@entry_id:147634)价值。最后，“动手实践”部分将通过一系列精心设计的计算问题，帮助读者巩固并深化对理论知识的理解，将抽象的公式转化为解决实际问题的能力。

## 原理与机制

本章旨在系统性地阐述控制材料[弹塑性](@entry_id:193198)响应的基本原理与内在机制。我们将从变形的基本分量分解和构成客观本构律基础的[应力不变量](@entry_id:170526)入手。随后，我们将构建起一个塑性模型的核心要素：定义塑性流动起点的屈服准则、描述其演化的硬化定律，以及决定塑性变形方向的[流动法则](@entry_id:177163)。整个理论框架将根植于热力学原理，特别是[塑性耗散](@entry_id:201273)的概念。最后，我们将介绍在[有限元法](@entry_id:749389)（FEM）等数值方法中实现这些模型所必需的算法概念，从而连接起连续介质理论与计算实践。

### 变形的分解：弹性与塑性

材料在外力作用下会发生变形。这种变形可以分为两个部分：一部分是可恢复的**弹性变形**，当外力移除后，这部分变形会完全消失；另一部分是不可恢复的**塑性变形**，它代表了材料内部微观结构发生永久性改变而导致的永久变形。在小应变理论的框架下，描述这一物理现象的核心[运动学](@entry_id:173318)假设是**应变张量的加法分解**。总应变张量 $\boldsymbol{\varepsilon}$ 可以被线性地分解为弹性部分 $\boldsymbol{\varepsilon}^{e}$ 和塑性部分 $\boldsymbol{\varepsilon}^{p}$ 的和：

$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^{e} + \boldsymbol{\varepsilon}^{p}
$$

这个假设是经典塑性理论的出发点之一 [@problem_id:2543954]。

为了更深入地理解变形的物理本质，我们可以进一步将[应变张量分解](@entry_id:184653)为两个部分：引起体积变化的**[体积应变](@entry_id:267252)**（或称球形应变）和引起形状变化的**[偏应变](@entry_id:201263)**（或称等容应变）。对于任意一个[小应变张量](@entry_id:754968) $\boldsymbol{\varepsilon}$，其体积应变张量 $\boldsymbol{\varepsilon}_{\text{vol}}$ 定义为：

$$
\boldsymbol{\varepsilon}_{\text{vol}} = \frac{1}{3} \mathrm{tr}(\boldsymbol{\varepsilon}) \mathbf{I}
$$

其中 $\mathrm{tr}(\boldsymbol{\varepsilon})$ 是应变张量的迹，代表了单位体积的变化（即体积应变），而 $\mathbf{I}$ 是二阶单位张量。偏[应变张量](@entry_id:193332) $\mathbf{e}$ (或 $\boldsymbol{\varepsilon}_{\text{dev}}$) 则是总应变张量减去其体积部分：

$$
\mathbf{e} = \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}_{\text{vol}}
$$

根据定义，偏应变[张量的迹](@entry_id:190669)恒为零，即 $\mathrm{tr}(\mathbf{e}) = 0$，这意味着它只描述了形状的改变（扭曲），而不涉及体积的变化 [@problem_id:2544078]。

这种分解在塑性理论中至关重要。对于大多数金属材料，实验观察表明[塑性流动](@entry_id:201346)在很大程度上是**等容的**（isochoric），即塑性变形几乎不引起材料体积的改变。这等价于说塑性应变张量的迹为零，$\mathrm{tr}(\boldsymbol{\varepsilon}^{p}) = 0$。因此，材料的体积变化几乎完全由[弹性应变](@entry_id:189634)承担，而塑性屈服和流动则主要由引起形状扭曲的偏应力分量驱动。这使得[偏应变](@entry_id:201263)成为描述塑性变形的核心物理量。

### 应力状态与[不变量](@entry_id:148850)

与[应变分解](@entry_id:186005)相对应，柯西应力张量 $\boldsymbol{\sigma}$ 也可以被分解为引起体积变化的**静水压力**部分和引起形状变化的**偏应力**部分。[偏应力张量](@entry_id:267642) $\mathbf{s}$ 定义为：

$$
\mathbf{s} = \boldsymbol{\sigma} - \frac{1}{3} \mathrm{tr}(\boldsymbol{\sigma}) \mathbf{I} = \boldsymbol{\sigma} - \sigma_m \mathbf{I}
$$

其中 $\sigma_m = \frac{1}{3} \mathrm{tr}(\boldsymbol{\sigma})$ 是平均应力或[静水应力](@entry_id:186327)。

对于一个**各向同性**材料，其本构关系（即[应力与应变](@entry_id:137374)之间的关系）必须与[坐标系](@entry_id:156346)的选择无关。这一**客观性**原理要求本构函数必须通过应力（或应变）张量的[不变量](@entry_id:148850)来表达。对于[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$，其三个[主不变量](@entry_id:193522)在理论上可以完备地描述应力状态，但在塑性力学中，使用以下一组[不变量](@entry_id:148850)更为方便 [@problem_id:2544050]：

1.  **应力张量的第一[不变量](@entry_id:148850) $I_1(\boldsymbol{\sigma})$**:
    $$
    I_1(\boldsymbol{\sigma}) = \mathrm{tr}(\boldsymbol{\sigma}) = \sigma_{11} + \sigma_{22} + \sigma_{33}
    $$
    该[不变量](@entry_id:148850)正比于[静水应力](@entry_id:186327)，主要与材料的体积弹性响应相关。

2.  **[偏应力张量](@entry_id:267642)的第二[不变量](@entry_id:148850) $J_2(\mathbf{s})$**:
    $$
    J_2(\mathbf{s}) = \frac{1}{2} \mathbf{s}:\mathbf{s} = \frac{1}{2} s_{ij} s_{ij}
    $$
    $J_2$ 是[偏应力](@entry_id:163323)大小的度量，与材料的弹性[畸变能](@entry_id:198925)相关。由于金属的塑性屈服主要是由剪切变形驱动的，因此 $J_2$ 是描述屈服发生的最关键的量。

3.  **[偏应力张量](@entry_id:267642)的第三[不变量](@entry_id:148850) $J_3(\mathbf{s})$**:
    $$
    J_3(\mathbf{s}) = \det(\mathbf{s})
    $$
    $J_3$ 描述了偏应力状态的“类型”或“模式”，它与**洛德角 (Lode angle)** 参数相关，可以区分例如[单轴拉伸](@entry_id:188287)、纯剪切和单轴压缩等不同的偏应力状态。

例如，给定一个应力张量 $\boldsymbol{\sigma} = \begin{pmatrix} 120 & 30 & -10 \\ 30 & 80 & 20 \\ -10 & 20 & 60 \end{pmatrix} \text{MPa}$，我们可以计算出其[不变量](@entry_id:148850)来量化其应力状态。其第一[不变量](@entry_id:148850)为 $I_1(\boldsymbol{\sigma}) = 120 + 80 + 60 = 260 \, \text{MPa}$。通过计算[偏应力张量](@entry_id:267642) $\mathbf{s}$，可以进一步得到 $J_2(\mathbf{s}) = \frac{7000}{3} \, \text{MPa}^2$ 和 $J_3(\mathbf{s}) = \frac{142000}{27} \, \text{MPa}^3$ [@problem_id:2544050]。这些[不变量](@entry_id:148850)构成了建立[屈服准则](@entry_id:193897)的数学基础。

### [屈服准则](@entry_id:193897)：弹性行为的边界

**[屈服准则](@entry_id:193897)**定义了材料从弹性行为过渡到塑性行为的临界应力状态。在应力空间中，这个临界状态的集合构成一个[曲面](@entry_id:267450)，称为**[屈服面](@entry_id:175331)**。屈服面内部的应力状态对应弹性行为，而应力状态达到[屈服面](@entry_id:175331)时则开始发生塑性变形。

数学上，屈服准则通过一个**[屈服函数](@entry_id:167970)** $f(\boldsymbol{\sigma}, \boldsymbol{\kappa})$ 来表达，其中 $\boldsymbol{\kappa}$ 代表了一组描述材料内部状态（例如[硬化](@entry_id:177483)程度）的**内变量**。弹性域 $\mathcal{E}$ 被定义为所有满足 $f(\boldsymbol{\sigma}, \boldsymbol{\kappa}) \le 0$ 的应力状态的集合 [@problem_id:2544007]。

对于延性金属，构建屈服准则需要遵循几个关键的物理原理 [@problem_id:2544007] [@problem_id:2544065]：
- **客观性与各向同性**: [屈服函数](@entry_id:167970)必须是[应力不变量](@entry_id:170526)的函数。
- **压力无关性**: 大量实验表明，[延性](@entry_id:160108)金属的屈服行为几乎不受静水压力的影响。这意味着[屈服函数](@entry_id:167970)不应依赖于 $I_1(\boldsymbol{\sigma})$，而只能是偏[应力[不变](@entry_id:170526)量](@entry_id:148850) $J_2$ 和 $J_3$ 的函数。

最著名且应用最广泛的屈服准则是 **von Mises [屈服准则](@entry_id:193897)**。该准则在压力无关性的基础上，进一步假设材料的屈服行为与洛德角无关，即不依赖于 $J_3$。因此，[屈服函数](@entry_id:167970)只与 $J_2$ 和内变量 $\kappa$ (代表累积塑性应变)有关。其标准形式为：

$$
f(\boldsymbol{\sigma}, \kappa) = \sigma_{\text{eq}}(\boldsymbol{\sigma}) - \sigma_y(\kappa) \le 0
$$

这里的 $\sigma_{\text{eq}}$ 是 **von Mises [等效应力](@entry_id:749064)**，定义为 $\sigma_{\text{eq}} = \sqrt{3 J_2(\mathbf{s})}$。常数 $\sqrt{3}$ 的引入是为了使得在[单轴拉伸](@entry_id:188287)情况下，[等效应力](@entry_id:749064)恰好等于拉伸应力值 [@problem_id:2544065]。$\sigma_y(\kappa)$ 是材料当前的[屈服强度](@entry_id:162154)，它是累积塑性应变的函数。

与[等效应力](@entry_id:749064)相对应，我们也可以定义一个标量的**等效塑性应变** $\bar{\varepsilon}^p$ (也常用 $\varepsilon_{\text{eq}}$ 表示)，它与[等效应力](@entry_id:749064)在塑性功的意义上是共轭的。其速率，即**等效塑性应变率** $\dot{\bar{\varepsilon}}^p$，标准定义为 [@problem_id:2544078]：
$$
\dot{\bar{\varepsilon}}^p = \sqrt{\frac{2}{3} \dot{\boldsymbol{\varepsilon}}^p : \dot{\boldsymbol{\varepsilon}}^p}
$$
累积的等效塑性应变 $\bar{\varepsilon}^p$ 是其在加载历史上的积分。这个定义确保了在单轴情况下，等效塑性应变的大小等于轴向塑性应变的大小。

### [硬化](@entry_id:177483)定律：屈服面的演化

当材料发生塑性变形后，其[屈服强度](@entry_id:162154)通常会发生变化，这种现象称为**[硬化](@entry_id:177483)** (或在某些情况下称为软化)。[硬化](@entry_id:177483)定律描述了屈服面如何随着塑性变形的累积而演化。描述硬化程度的内变量通常是**等效塑性应变** $\kappa$ (也常用 $\bar{\varepsilon}^p$ 表示)，它是一个单调不减的标量，量化了塑性变形的[累积量](@entry_id:152982)。

主要有两种理想化的硬化模型：

1.  **[各向同性硬化](@entry_id:164486) (Isotropic Hardening)**: 这种模型假设[屈服面](@entry_id:175331)在所有方向上均匀膨胀，其形状和在[应力空间](@entry_id:199156)中的中心位置保持不变。当前的[屈服强度](@entry_id:162154) $\sigma_y$ 是等效塑性应变 $\kappa$ 的函数。对于线性[各向同性硬化](@entry_id:164486)，该关系为：
    $$
    \sigma_y(\kappa) = \sigma_{y0} + H_{\text{iso}} \kappa
    $$
    其中 $\sigma_{y0}$ 是初始[屈服强度](@entry_id:162154)，$H_{\text{iso}}$ 是[各向同性硬化](@entry_id:164486)模量。

2.  **[随动硬化](@entry_id:172077) (Kinematic Hardening)**: 这种模型假设[屈服面](@entry_id:175331)的大小和形状保持不变，但在[应力空间](@entry_id:199156)中发生平移。这种平移由一个称为**[背应力](@entry_id:198105)** (backstress) 的张量 $\boldsymbol{\alpha}$ 来描述。[屈服函数](@entry_id:167970)变为 $f = \sigma_{\text{eq}}(\boldsymbol{\sigma} - \boldsymbol{\alpha}) - \sigma_{y0} \le 0$。[随动硬化](@entry_id:172077)对于描述材料在[循环加载](@entry_id:181502)下的**[包辛格效应](@entry_id:173790)** (Bauschinger effect) 至关重要。对于线性[随动硬化](@entry_id:172077)，[背应力](@entry_id:198105)的演化率与塑性应变率成正比，例如 $d\boldsymbol{\alpha} = H_{\text{kin}} d\boldsymbol{\varepsilon}^p$ (在1D情况下) [@problem_id:2544016]。

更复杂的模型，如**混合硬化 (Mixed Hardening)**，则结合了上述两种效应，即[屈服面](@entry_id:175331)既膨胀又平移。

### 流动法则与[塑性耗散](@entry_id:201273)

当应力状态达到屈服面并继续加载时，材料开始产生塑性应变。**[流动法则](@entry_id:177163)** (Flow Rule) 规定了塑性应变增量 (或率) 的方向。

这一法则的理论基础源于[热力学](@entry_id:141121)。根据适用于[等温过程](@entry_id:143096)的 **Clausius-Duhem 不等式**，材料内部的耗散率 $\mathcal{D}$ 必须是非负的：
$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0
$$
其中 $\psi$ 是单位体积的[亥姆霍兹自由能](@entry_id:136442)。对于[弹塑性](@entry_id:193198)材料，自由能通常是[弹性应变](@entry_id:189634) $\boldsymbol{\varepsilon}^e$ 和硬化内变量 $\kappa$ 的函数，例如 $\psi(\boldsymbol{\varepsilon}^e, \kappa) = \frac{1}{2}\boldsymbol{\varepsilon}^e : \mathbb{C} : \boldsymbol{\varepsilon}^e + \frac{1}{2}H\kappa^2$ [@problem_id:2544036]。通过标准的[热力学](@entry_id:141121)推导 (Coleman-Noll procedure)，可以得到应力 $\boldsymbol{\sigma} = \partial\psi / \partial\boldsymbol{\varepsilon}^e$，并且[塑性耗散](@entry_id:201273)可以表示为：
$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p - K \dot{\kappa} \ge 0
$$
其中 $K = \partial\psi / \partial\kappa$ 是与硬化内变量共轭的[热力学力](@entry_id:161907)。

基于**[最大塑性耗散](@entry_id:184825)原理** (Drucker's postulate)，可以推导出塑性应变率 $\dot{\boldsymbol{\varepsilon}}^p$ 的方向垂直于屈服面。这被称为**关联[流动法则](@entry_id:177163)** (Associative Flow Rule) 或**正交[流动法则](@entry_id:177163)** (Normality Rule)：

$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$

其中 $\dot{\lambda} \ge 0$ 是一个非负的标量，称为**塑性乘子**。它的大小决定了[塑性流动](@entry_id:201346)的速率，而其方向由[屈服函数](@entry_id:167970)对应力的梯度决定。当[屈服函数](@entry_id:167970)与流动势函数相同时，[流动法则](@entry_id:177163)是关联的。对于 von Mises 准则，$f = \sqrt{3J_2} - \sigma_y(\kappa)$，其梯度为 $\partial f / \partial \boldsymbol{\sigma} = \frac{3}{2\sigma_{\text{eq}}}\mathbf{s}$。代入流动法则得到 $\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{3}{2\sigma_{\text{eq}}}\mathbf{s}$，由于 $\mathrm{tr}(\mathbf{s})=0$，这自然地导出了塑性流动是等容的结论 [@problem_id:2543954]。

将关联[流动法则](@entry_id:177163)代入耗散表达式，并在[屈服面](@entry_id:175331)上 ($f=0$) 进行计算，可以得到一个简洁的结果。对于前面提到的 von Mises 模型和自由能形式，可以证明[塑性耗散](@entry_id:201273)率恰好为 $\mathcal{D} = \sigma_{y0} \dot{\lambda}$ [@problem_id:2544036]。这表明，对于线性[各向同性硬化](@entry_id:164486)，只有与初始屈服强度相关的部分是真正耗散掉的能量，而[硬化](@entry_id:177483)所增加的能量则以某种形式存储在材料微结构中。

### 塑性本构模型的完整框架

综合以上要素，一个完整的小应变、率无关[弹塑性](@entry_id:193198)本构模型（以带线性[各向同性硬化](@entry_id:164486)的 von Mises 模型为例）由以下一组方程构成 [@problem_id:2543954]：

1.  **[运动学分解](@entry_id:751020)**: $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p$
2.  **弹性本构**: $\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}^e$
3.  **[屈服函数](@entry_id:167970)**: $f(\boldsymbol{\sigma}, \kappa) = \sigma_{\text{eq}} - (\sigma_{y0} + H\kappa) \le 0$
4.  **流动法则**: $\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}$
5.  **[硬化](@entry_id:177483)定律**: $\dot{\kappa} = \dot{\lambda}$

为了完备这个模型，还需要一组描述加载和卸载过程的条件，即 **[Karush-Kuhn-Tucker (KKT) 条件](@entry_id:176491)**：

$$
\dot{\lambda} \ge 0, \quad f(\boldsymbol{\sigma}, \kappa) \le 0, \quad \dot{\lambda} f(\boldsymbol{\sigma}, \kappa) = 0
$$

这组[互补条件](@entry_id:747558)优雅地概括了材料的三种可能状态：
- **弹性状态**: $f < 0$，此时必须有 $\dot{\lambda}=0$，无[塑性流动](@entry_id:201346)。
- **塑性加载**: $f = 0$ 且 $\dot{\lambda} > 0$，材料发生塑性变形。
- **[弹性卸载](@entry_id:748863)或中性加载**: $f = 0$ 但 $\dot{\lambda} = 0$。

在塑性加载过程中，应力点必须始终停留在演化中的屈服面上，这要求[屈服函数](@entry_id:167970)的时间变化率必须为零，即 $\dot{f}=0$。这个条件被称为**一致性条件 (Consistency Condition)**，它被用来确定在给定的总[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}$ 下塑性乘子 $\dot{\lambda}$ 的具体数值。

### [计算塑性力学](@entry_id:171377)：算法实现

将上述连续介质力学理论应用于有限元等数值方法时，需要将其离散化为在每个时间增量步内执行的算法。

首先要深刻理解塑性变形的**[路径依赖性](@entry_id:186326)**。与弹性不同，塑性变形是不可逆的耗散过程。最终的应力状态不仅取决于最终的总应变，还取决于达到该应变的整个加载历史。例如，对于相同的最终总应变，先施加剪切再施加拉伸，与先施加拉伸再施加剪切，所导致的最终应力[状态和](@entry_id:193625)累积塑性应变是不同的 [@problem_id:2543912]。

在有限元计算的每个[高斯积分](@entry_id:187139)点上，应力更新通常采用**[弹性预测-塑性修正](@entry_id:748860)**算法，最常用的是**[返回映射算法](@entry_id:168456) (Return-Mapping Algorithm)**。该算法分为两步 [@problem_id:2543912] [@problem_id:2543913]：

1.  **弹性预测**: 假设在整个时间步内材料行为完全是弹性的。根据弹性定律计算出一个“试探应力” $\boldsymbol{\sigma}^{\text{trial}}$。
2.  **塑性修正**: 将试探应力代入[屈服函数](@entry_id:167970)进行判断。
    - 如果 $f(\boldsymbol{\sigma}^{\text{trial}}, \kappa_n) \le 0$，说明试探应力在弹性域内或恰好在屈服面上，弹性假设成立。该步为弹性步，最终应力就是试探应力。
    - 如果 $f(\boldsymbol{\sigma}^{\text{trial}}, \kappa_n) > 0$，说明试探应力超出了屈服面，这是物理上不允许的。弹性假设错误，该步内发生了塑性变形。此时需要进行塑性修正，即通过一个算法将试探应力“返回”到更新后的屈服面上。

这个返回过程需要求解一个由离散化后的一致性条件构成的方程，以确定增量步内的塑性乘子增量 $\Delta\gamma$ (或 $\Delta\lambda$)。对于带线性硬化的 von Mises 模型，这个方程恰好是线性的，可以求得解析解 [@problem_id:2543913]：

$$
\Delta\gamma = \frac{q^{\text{trial}} - \sigma_y(\kappa_n)}{3G+H}
$$

其中 $G$ 是剪切模量，$q^{\text{trial}}$ 是试探[等效应力](@entry_id:749064)。

在有限元分析中，求解全局非线性方程组通常采用 [Newton-Raphson](@entry_id:177436) 迭代法，这需要一个**一致性[切线](@entry_id:268870)模量** $C_{\text{alg}} = d\sigma / d\varepsilon$。这个模量是增量步末端的应力对该步末端应变的导数，它与连续介质力学中的[弹塑性切线模量](@entry_id:189492)不同。它可以通过对[返回映射算法](@entry_id:168456)进行精确的线性化来导出。例如，在一维情况下，对于混合[硬化](@entry_id:177483)模型，可以从一致性条件 $df=0$ 出发，推导出一致性[切线](@entry_id:268870)模量为 [@problem_id:2544016]：

$$
C_{\text{alg}} = \frac{E (H_{\text{iso}} + H_{\text{kin}})}{E + H_{\text{iso}} + H_{\text{kin}}}
$$

使用一致性[切线](@entry_id:268870)模量可以确保 [Newton-Raphson](@entry_id:177436) 算法的二次[收敛率](@entry_id:146534)，这对于大型[非线性](@entry_id:637147)计算的效率至关重要。

### 有限变形塑性理论简介

以上讨论均局限于小应变框架。当材料经历大转动和大变形时，小应变理论不再适用，必须采用**有限变形 (Finite Deformation)** 理论。其核心变化在于运动学描述。总变形梯度 $F$ 被**[乘法分解](@entry_id:199514)**为一个弹性部分 $F^e$ 和一个塑性部分 $F^p$ [@problem_id:2543944]：

$$
F = F^e F^p
$$

这个分解引入了一个虚拟的、无应力的**[中间构型](@entry_id:193000)**。$F^p$ 描述了从初始参考构型到[中间构型](@entry_id:193000)的映射，包含了所有不可恢复的塑性变形。$F^e$ 则描述了从[中间构型](@entry_id:193000)到当前真实构型的可恢复弹性变形。

在这种框架下，本构关系通常建立在[中间构型](@entry_id:193000)上，并通过弹性变形映射到当前构型。为了保证客观性，本构关系通常基于**弹性[左柯西-格林张量](@entry_id:186163)** $b^e = F^e (F^e)^T$ 的[不变量](@entry_id:148850)来构建。对于[各向同性材料](@entry_id:170678)，$b^e$ 包含了计算应力所需的全部信息（即弹性[主伸长](@entry_id:194664)）。然而，值得注意的是，$b^e$ 本身不包含弹性转动的信息，因此对于需要追踪材料方向的[各向异性材料](@entry_id:184874)，仅存储 $b^e$ 是不够的 [@problem_id:2543944]。同样，对于金属，[塑性不可压缩性](@entry_id:183440)假设 ($\det(F^p)=1$) 仍然是一个很好的近似，这意味着所有体积变化都由弹性变形 $F^e$ 承担，即 $J = \det(F) = \det(F^e)$ [@problem_id:2543944]。有限变形塑性理论的完整推导和算法实现比小应变理论要复杂得多，是[计算固体力学](@entry_id:169583)中的一个高级课题。