## 引言
在[流体力学](@entry_id:136788)领域，[湍流](@entry_id:151300)是一种普遍存在却又极其复杂的现象。直接从控制流体运动的[Navier-Stokes方程](@entry_id:161487)出发进行[数值模拟](@entry_id:137087)（DNS）来解析所有时空尺度的[湍流](@entry_id:151300)结构，对于大多数工程问题而言，其计算成本高到无法承受。因此，迫切需要一种能够高效预测[湍流](@entry_id:151300)平均效应，而非其瞬时细节的建模框架。[雷诺平均](@entry_id:754341)[Navier-Stokes](@entry_id:276387)（RANS）方程正是为解决这一挑战而生，它构成了过去几十年来计算流体力学（CFD）在工程应用中的基石。

本文旨在系统性地剖析RANS方法的核心理论与实践。在第一章“原理与机制”中，我们将从[雷诺分解](@entry_id:267756)这一基本概念出发，详细推导[RANS方程](@entry_id:275032)，并阐明由此产生的[湍流封闭问题](@entry_id:268973)，同时介绍解决该问题的关键思路，如[Boussinesq假设](@entry_id:272519)和[雷诺应力模型](@entry_id:754343)。第二章“应用与跨学科连接”将展示RANS框架如何在[空气动力学](@entry_id:193011)、[地球物理学](@entry_id:147342)和燃烧学等多个领域中得到应用，并探讨其在处理[复杂流动](@entry_id:747569)时的能力与局限性。最后，在第三章“动手实践”中，你将通过一系列精心设计的计算练习，从理论走向实践，亲手验证和评估不同湍流模型的性能。通过这三章的学习，读者将建立起对RANS方法的深刻理解，掌握其理论精髓，洞悉其应用边界，并具备初步的实践分析能力。

## Principles and Mechanisms

### [雷诺分解](@entry_id:267756)与平均方法

[湍流](@entry_id:151300)的内在特征是其在时间和空间上的无序、混沌和多尺度性。直接求解描述[流体运动](@entry_id:182721)的[Navier-Stokes方程](@entry_id:161487)（即[直接数值模拟](@entry_id:149543)，DNS）需要极高的计算资源，因为它必须解析从最大的能量尺度到最小的耗散尺度的所有涡结构。对于工程应用中常见的[高雷诺数流](@entry_id:199822)动，这在可预见的未来仍然是不可行的。因此，我们需要一种系统性的方法来处理[湍流](@entry_id:151300)的统计特性，而不是其瞬时细节。这种方法的核心是**[雷诺分解](@entry_id:267756)**（Reynolds decomposition）。

[雷诺分解](@entry_id:267756)将任意一个瞬时流场变量 $\phi(\boldsymbol{x}, t)$ 分解为其**平均值** $\overline{\phi}$ 和**脉动值** $\phi'$ 的和：

$$
\phi(\boldsymbol{x}, t) = \overline{\phi} + \phi'(\boldsymbol{x}, t)
$$

根据定义，脉动值的平均为零，即 $\overline{\phi'} = 0$。这里的[平均算子](@entry_id:746605) $\overline{(\cdot)}$ 必须满足一组被称为**雷诺公理**（Reynolds axioms）的性质：它对于求和是线性的（$\overline{f+g} = \overline{f} + \overline{g}$），与常数相乘可交换（$\overline{cf} = c\overline{f}$），并且与时空导数可交换（例如 $\overline{\partial f / \partial t} = \partial \overline{f} / \partial t$）。后一个性质并非无条件成立，例如，对于有限窗口的时间平均，它要求平均窗口的长度不随空间变化 [@problem_id:3357806]。

在实践中，有几种定义[平均算子](@entry_id:746605)的方式，它们的等价性取决于流动的统计特性 [@problem_id:3357789]：

1.  **系综平均（Ensemble Average）**：理论上最严谨的平均方式，定义为对大量相同宏观条件下生成的[湍流](@entry_id:151300)实现（realizations）进行平均，记作 $\langle \phi \rangle$。它是[随机场](@entry_id:177952)理论中的[期望值](@entry_id:153208)。

2.  **时间平均（Time Average）**：对于一个固定的空间点 $\boldsymbol{x}$，对一个足够长的时间周期 $T$ 进行积分平均：
    $$
    \overline{\phi}(\boldsymbol{x}) = \lim_{T \to \infty} \frac{1}{T} \int_{0}^{T} \phi(\boldsymbol{x}, t) \, dt
    $$
    对于**统计定常**（statistically stationary）的[湍流](@entry_id:151300)，其任意阶[统计矩](@entry_id:268545)都不随时间变化。如果流动同时满足**时间遍历性**（ergodicity in time），即单个实现的时间样本足以代表整个系综的统计特性，那么[时间平均](@entry_id:267915)等价于系综平均。

3.  **[空间平均](@entry_id:203499)（Spatial Average）**：对于在某个方向（例如 $x_1$）上**统计均匀**（statistically homogeneous）的流动，其统计特性在该方向上不随空间位置变化。如果流动在该方向上还满足**空间遍历性**（ergodicity in space），那么沿着该方向进行的长距离[空间平均](@entry_id:203499)也等价于系综平均。

在许多工程和理论分析中，我们假设流动满足这些遍历性条件，从而允许使用更易于在实验或模拟中获取的时间或[空间平均](@entry_id:203499)来代替系综平均。例如，在分析一个[稳态流场](@entry_id:191654)时，[时间平均](@entry_id:267915)是自然的选择。

### [雷诺平均](@entry_id:754341)[Navier-Stokes方程](@entry_id:161487)与[湍流封闭问题](@entry_id:268973)

将[雷诺分解](@entry_id:267756)应用于不可压缩、常密度的[Navier-Stokes方程](@entry_id:161487)，我们就可以推导出控制平均流场的方程，即**[雷诺平均](@entry_id:754341)[Navier-Stokes](@entry_id:276387)（RANS）方程**。

考虑不可压缩动量方程：
$$
\frac{\partial u_i}{\partial t} + \frac{\partial (u_i u_j)}{\partial x_j} = -\frac{1}{\rho}\frac{\partial p}{\partial x_i} + \nu \frac{\partial^2 u_i}{\partial x_j^2}
$$
其中 $u_i$ 是瞬时速度分量，$p$ 是瞬时压力，$\rho$ 是常[数密度](@entry_id:268986)，$\nu$ 是运动粘度。我们将分解式 $u_i = \overline{u_i} + u_i'$ 和 $p = \overline{p} + p'$ 代入，并对整个方程进行平均。

由于[平均算子](@entry_id:746605)的线性以及与时空导数的[可交换性](@entry_id:263314)，大部分项的处理都非常直接：
$$
\overline{\frac{\partial u_i}{\partial t}} = \frac{\partial \overline{u_i}}{\partial t} \quad , \quad \overline{\frac{\partial p}{\partial x_i}} = \frac{\partial \overline{p}}{\partial x_i} \quad , \quad \overline{\nu \frac{\partial^2 u_i}{\partial x_j^2}} = \nu \frac{\partial^2 \overline{u_i}}{\partial x_j^2}
$$
然而，[非线性](@entry_id:637147)的[对流](@entry_id:141806)项 $\frac{\partial (u_i u_j)}{\partial x_j}$ 在平均后会产生一个额外的项。让我们详细展开它 [@problem_id:3357825]：
$$
\overline{u_i u_j} = \overline{(\overline{u_i} + u_i')(\overline{u_j} + u_j')} = \overline{\overline{u_i}\overline{u_j} + \overline{u_i}u_j' + u_i'\overline{u_j} + u_i'u_j'}
$$
根据雷诺公理，$\overline{\overline{u_i}\overline{u_j}} = \overline{u_i}\overline{u_j}$，以及 $\overline{\overline{u_i}u_j'} = \overline{u_i}\overline{u_j'} = 0$。因此，我们得到：
$$
\overline{u_i u_j} = \overline{u_i}\overline{u_j} + \overline{u_i'u_j'}
$$
这个结果是[湍流建模](@entry_id:151192)的核心。它表明，瞬时速度乘积的平均值，不等于平均速度的乘积，而是多出了一个速度脉动量乘积的平均值 $\overline{u_i'u_j'}$。这个新项在一般[湍流](@entry_id:151300)中不为零。

将此结果代回[动量方程](@entry_id:197225)的平均形式，我们得到[RANS方程](@entry_id:275032)：
$$
\frac{\partial \overline{u_i}}{\partial t} + \frac{\partial (\overline{u_i}\overline{u_j})}{\partial x_j} = -\frac{1}{\rho}\frac{\partial \overline{p}}{\partial x_i} + \nu \frac{\partial^2 \overline{u_i}}{\partial x_j^2} - \frac{\partial (\overline{u_i'u_j'})}{\partial x_j}
$$
为了更清晰地看出物理意义，我们常将新项移到右边，并与粘性项类比：
$$
\rho\left(\frac{\partial \overline{u_i}}{\partial t} + \overline{u_j}\frac{\partial \overline{u_i}}{\partial x_j}\right) = -\frac{\partial \overline{p}}{\partial x_i} + \frac{\partial}{\partial x_j}\left( \mu\frac{\partial \overline{u_i}}{\partial x_j} - \rho\overline{u_i'u_j'} \right)
$$
这里的张量 $\tau_{ij}^{\text{R}} = -\rho\overline{u_i'u_j'}$ 被称为**[雷诺应力张量](@entry_id:270803)**。它代表了由速度脉动引起的[动量输运](@entry_id:139628)，其效果类似于一个额外的应力作用于平均流场。

这就引出了著名的**[湍流封闭问题](@entry_id:268973)**（turbulence closure problem）。[RANS方程](@entry_id:275032)组（3个[动量方程](@entry_id:197225)和1个平均[连续性方程](@entry_id:195013) $\partial \overline{u_i}/\partial x_i = 0$）的目标是求解4个平均场变量（$\overline{u_1}, \overline{u_2}, \overline{u_3}, \overline{p}$）。然而，方程中出现了新的未知量——对称的[雷诺应力张量](@entry_id:270803) $\overline{u_i'u_j'}$ 的6个独立分量。未知量的数量超过了方程的数量，使得[方程组](@entry_id:193238)在数学上不封闭。为了求解[RANS方程](@entry_id:275032)，必须引入额外的模型关系，将雷诺应力与已知的平均流场量（如平均速度梯度）联系起来。这个过程就是**[湍流建模](@entry_id:151192)** [@problem_id:3382031]。

### 雷诺应力的物理诠释

雷诺应力不仅是数学上的产物，它具有深刻的物理意义。它量化了[湍流](@entry_id:151300)脉动如何输运平均动量。对角线分量，如 $\overline{u'^2}$、$\overline{v'^2}$ 和 $\overline{w'^2}$（通常用 $R_{11}, R_{22}, R_{33}$ 表示），代表了在各个方向上速度脉动的强度，它们的和与湍动能成正比。非对角线分量，如 $\overline{u'v'}$（$R_{12}$），代表了不同方向速度脉动之间的相关性，它们构成了**[湍流](@entry_id:151300)剪切应力**。

我们可以通过一个经典的例子——充分发展的平面槽道流——来具体理解[雷诺应力](@entry_id:263788)的行为 [@problem_id:3357820]。考虑在两块无限大[平行板](@entry_id:269827)之间的流动，主流方向为 $x$，壁面法向为 $y$。

-   **[湍流](@entry_id:151300)剪切应力 $(-\overline{u'v'})$**：在这样的剪切流中，平均速度 $U(y)$ 随 $y$ 的增加而增加。一个流体微团若因[湍流](@entry_id:151300)而向壁面运动（$v'0$），它通常来自速度较高的区域，因此携带正的流向速度脉动（$u'>0$）。反之，若微团向通道中心运动（$v'>0$），它来自低速区，携带负的流向速度脉动（$u'0$）。在这两种典型情况下，乘积 $u'v'$ 大多为负。因此，相关项 $\overline{u'v'}$ 在整个通道内（除中心线和壁面）是负的。这意味着[湍流](@entry_id:151300)[剪切应力](@entry_id:137139) $-\overline{u'v'}$ 是正值。这个正的应力起到了将动量从高速区向低速区传递的作用，其效果与粘性剪切应力类似，但机理完全不同。在壁面处，由于无滑移条件，所有脉动为零，故 $\overline{u'v'}=0$。在通道中心线，由于对称性，$\overline{u'v'}$ 也为零。因此，[湍流](@entry_id:151300)[剪切应力](@entry_id:137139)从壁面处的零值开始，在近壁区迅速增长，达到一个峰值，然后向中心线逐渐减小至零。在远离壁面的[对数律区](@entry_id:264342)和核心区，总[剪切应力](@entry_id:137139)几乎完全由[湍流](@entry_id:151300)剪切应力承担。

-   **法向应力 $(\overline{u_i'^2})$**：[法向应力](@entry_id:260622)分量描述了不同方向脉动的剧烈程度。在壁面附近，流动是高度**各向异性**的。由于壁面的阻碍作用，法向脉动 $v'$ 受到强烈抑制，因此 $\overline{v'^2}$ 是最小的法向应力分量。同时，巨大的平均速度梯度在近壁区通过 $-\overline{u'v'} \partial U/\partial y$ 项产生大量[湍动能](@entry_id:262712)，这些能量主要注入到流向脉动中。因此，在近壁区，我们有明确的强度排序：$\overline{u'^2}  \overline{w'^2}  \overline{v'^2}$。流向脉动强度 $\overline{u'^2}$ 的峰值通常出现在[缓冲层](@entry_id:160164)内（例如，无量纲壁面距离 $y^+ \approx 15-30$）。随着向通道中心移动，壁面效应和平均剪切都减弱，[湍流](@entry_id:151300)通过压力-应变作用趋向于**各向同性**，即三个法向应力分量的值趋于相等。

### [Boussinesq假设](@entry_id:272519)与涡粘模型

解决封闭问题的最直接和广泛使用的方法是引入**[Boussinesq假设](@entry_id:272519)** [@problem_id:3382031]。该假设类比了层流中粘性[应力与[应变](@entry_id:263123)率](@entry_id:154778)的[线性关系](@entry_id:267880)，提出[雷诺应力张量](@entry_id:270803)的**各向异性部分**（或称偏应力部分）与平均应变率张量成正比：
$$
-\rho\overline{u_i'u_j'} + \frac{1}{3}\delta_{ij}(-\rho\overline{u_k'u_k'}) = 2\mu_t S_{ij}
$$
其中 $S_{ij} = \frac{1}{2}\left(\frac{\partial \overline{u_i}}{\partial x_j} + \frac{\partial \overline{u_j}}{\partial x_i}\right)$ 是**平均应变率张量**，$\delta_{ij}$ 是克罗内克符号。左边第一项是[雷诺应力](@entry_id:263788)，第二项通过引入**湍动能** $k = \frac{1}{2}\overline{u_k'u_k'}$，使得整个左边成为一个迹为零的张量（对于不可压缩流）。新引入的比例系数 $\mu_t$ 被称为**[湍流](@entry_id:151300)粘度**或**[涡粘度](@entry_id:155814)**（eddy viscosity）。它不是流体的物理属性，而是[湍流](@entry_id:151300)本身的特性，反映了[湍流涡](@entry_id:266898)对动量的混合与输运能力。

重新整理上式，我们得到涡粘模型的标准形式：
$$
-\rho\overline{u_i'u_j'} = 2\mu_t S_{ij} - \frac{2}{3}\rho k \delta_{ij}
$$

从[张量分析](@entry_id:161423)的角度看，[Boussinesq假设](@entry_id:272519)是连接两个对称二阶张量（[雷诺应力](@entry_id:263788)与平均应变率）的最简单、线性的**各向同性**关系 [@problem_id:3357801]。
- **各向同性与标量粘度**：该关系之所以是各向同性的，是因为它不依赖于[坐标系](@entry_id:156346)的选择。[涡粘度](@entry_id:155814) $\mu_t$ 必须是一个标量，但它可以是空间和时间的函数，依赖于当地[湍流](@entry_id:151300)的标量属性（如 $k$ 和它的耗散率 $\epsilon$），而不会破坏模型的各向同性。
- **标架无关性（Frame Indifference）**：一个合理的本构关系不应依赖于观察者的刚体运动。平均速度梯度 $\partial \overline{u_i}/\partial x_j$ 本身并非标架无关，但其对称部分（[应变率](@entry_id:154778) $S_{ij}$）是。[Boussinesq假设](@entry_id:272519)只依赖于 $S_{ij}$，而排除了非标架无关的反对称部分（旋转率 $\Omega_{ij}$）。这确保了模型在物理上的客观性。例如，对于纯刚体[旋转流](@entry_id:276737)场，$S_{ij}=0$，该模型正确地预测出雷诺[偏应力](@entry_id:163323)为零，因为没有变形，就不应产生应力。

[Boussinesq假设](@entry_id:272519)的引入，将封闭问题从求解6个[雷诺应力](@entry_id:263788)分量，简化为求解一个[标量场](@entry_id:151443)——[涡粘度](@entry_id:155814) $\mu_t$。然而，这只是将问题转化了。下一步是建立模型来确定 $\mu_t$。诸如 $k-\epsilon$ 或 $k-\omega$ 这样的**[两方程模型](@entry_id:271436)**，就是通过求解湍动能 $k$ 和其耗散率 $\epsilon$（或比[耗散率](@entry_id:748577) $\omega$）的[输运方程](@entry_id:756133)，然后通过代数关系（如 $\mu_t = C_\mu \rho k^2/\epsilon$）来计算 $\mu_t$，从而最终封闭[RANS方程](@entry_id:275032)组。

### [湍动能](@entry_id:262712)及其输运

湍动能 $k$ 是[湍流建模](@entry_id:151192)中的核心物理量，它代表了单位[质量流](@entry_id:143424)体中[湍流](@entry_id:151300)脉动的[平均动能](@entry_id:146353)。其精确定义为：
$$
k = \frac{1}{2}\overline{u_i'u_i'} = \frac{1}{2}(\overline{u'^2} + \overline{v'^2} + \overline{w'^2})
$$
通过对脉动速度的[动量方程](@entry_id:197225)进行数学推导，可以得到一个精确的**[湍动能输运方程](@entry_id:269723)**，它描述了 $k$ 的生消、输运和转化过程。在最简单的均匀[湍流](@entry_id:151300)中（所有统计量在空间上均匀），该方程简化为 [@problem_id:3357779]：
$$
\frac{d k}{d t} = P_k - \epsilon
$$
这里，$P_k = -\overline{u_i'u_j'}\frac{\partial \overline{u_i}}{\partial x_j}$ 是**产生项**，表示通过雷诺应力与平均速度梯度相互作用，从平均流动动能向湍动能的转化率。该项是[湍流](@entry_id:151300)得以维持的能量来源。

$\epsilon$ 是**[耗散率](@entry_id:748577)**项，其精确定义为：
$$
\epsilon = \nu \overline{\frac{\partial u_i'}{\partial x_j} \frac{\partial u_i'}{\partial x_j}}
$$
- **物理意义**：$\epsilon$ 代表单位质量流体的湍动能通过粘性作用转化为内能（热）的速率。由于 $\nu  0$ 且被平均的项是一个平方和，所以 $\epsilon$ 始终是**非负的**。它在湍动能预算中永远是汇项，即能量的耗散。在著名的[湍流能量级串](@entry_id:194234)理论中，能量从大尺度涡注入，通过[惯性子区](@entry_id:273327)的非粘性过程逐级传递到小尺度涡，最终在最小的[Kolmogorov尺度](@entry_id:270763)上由粘性耗散掉，其速率正是 $\epsilon$ [@problem_id:3357779]。
- **数学角色**：在上述简化的均匀[湍流](@entry_id:151300)方程中，如果不存在平均剪切（$P_k = 0$），则方程变为 $dk/dt = -\epsilon$，描述了[湍流](@entry_id:151300)在没有能量输入的情况下如何因粘性耗散而自然衰减。

### 超越[Boussinesq假设](@entry_id:272519)：[二阶矩封闭](@entry_id:754596)模型

涡粘模型虽然广泛应用，但其核心的[Boussinesq假设](@entry_id:272519)是一个巨大的简化。它假设[湍流](@entry_id:151300)粘性是各向同性的，即 $\mu_t$ 是一个标量，这意味着[雷诺应力张量](@entry_id:270803)的[主轴](@entry_id:172691)方向必须与平均[应变率张量](@entry_id:266108)的[主轴](@entry_id:172691)方向对齐。这在许多[复杂流动](@entry_id:747569)中（如强旋转、曲壁流动、[二次流](@entry_id:754609)）是不成立的。

为了克服这些限制，发展了更高级的**[二阶矩封闭](@entry_id:754596)（Second-Moment Closure, SMC）模型**，也称为**[雷诺应力模型](@entry_id:754343)（Reynolds Stress Model, RSM）**。这类模型不再使用涡粘假设，而是直接为[雷诺应力张量](@entry_id:270803) $R_{ij} = \overline{u_i'u_j'}$ 的每一个分量求解一个独立的输运方程 [@problem_id:3357788]。

[雷诺应力输运方程](@entry_id:754345)（RSTE）的示意形式为：
$$
\frac{D R_{ij}}{D t} = P_{ij} + \phi_{ij} + D_{ij} - \epsilon_{ij}
$$
其中，$\frac{D}{Dt}$ 是随平均流的[物质导数](@entry_id:172646)。各项的物理意义如下：
- **产生项 ($P_{ij}$)**：$P_{ij} = -(\overline{u_i'u_k'}\frac{\partial \overline{u_j}}{\partial x_k} + \overline{u_j'u_k'}\frac{\partial \overline{u_i}}{\partial x_k})$。这是雷诺应力与[平均速度](@entry_id:267649)梯度相互作用产生的项。它是精确的，不需要建模。
- **耗散项 ($\epsilon_{ij}$)**：$\epsilon_{ij} = 2\nu\overline{\frac{\partial u_i'}{\partial x_k}\frac{\partial u_j'}{\partial x_k}}$。它描述了粘性作用对雷诺应力的耗散。在近壁区它是各向异性的，需要建模。
- **[扩散](@entry_id:141445)项 ($D_{ij}$)**：它包含了由速度三重相关、压力-速度相关引起的[湍流输运](@entry_id:150198)，以及粘性[扩散](@entry_id:141445)。这一项需要建模。
- **压力-应变相关项 ($\phi_{ij}$)**：$\phi_{ij} = \overline{p'\left(\frac{\partial u_i'}{\partial x_j} + \frac{\partial u_j'}{\partial x_i}\right)} / \rho$。这是RSTE中最复杂、最关键的项。

**压力-应变项 $\phi_{ij}$** 的作用至关重要 [@problem_id:3357785]：
1.  **能量重新分配**：对于[不可压缩流](@entry_id:140301)，该项的迹为零，即 $\phi_{ii} = 0$。这意味着它不产生也不耗散总的湍动能 $k$。它的作用是在不同的[法向应力](@entry_id:260622)分量（$\overline{u'^2}, \overline{v'^2}, \overline{w'^2}$）之间重新分配能量，从而影响[湍流](@entry_id:151300)的各向异性程度。它通常倾向于将能量从脉动最强的分量转移到较弱的分量，起到“削峰填谷”的作用，使[湍流](@entry_id:151300)趋向各向同性。
2.  **非局部性**：脉动压力 $p'$ 由一个泊松方程决定，其[源项](@entry_id:269111)遍布整个流场。这意味着任何一点的 $p'$ 都受到全流场流动[状态和](@entry_id:193625)边界几何的影响。因此，$\phi_{ij}$ 是一个**非局部**（non-local）项。正是这种非局部性使得RSM能够自然地响应流场的曲率、旋转和系统变形，而这些是涡粘模型难以捕捉的 [@problem_id:3357788]。

RSM通过直接求解雷诺应力的动力学行为，提供了比涡粘模型高得多的物理保真度，但代价是求解更多的输运方程，且模型本身更加复杂和不稳定。

### [可变密度流](@entry_id:756427)动的推广：[Favre平均](@entry_id:198824)

当流体密度不再是常数时（例如在高速[可压缩流](@entry_id:747589)或燃烧问题中），标准的[雷诺分解](@entry_id:267756)和平均会带来巨大的复杂性。[对流](@entry_id:141806)项 $\overline{\rho u_i u_j}$ 在平均后会产生一系列复杂的未知相关项，如 $\overline{\rho'u_i'}$、$\overline{\rho'u_j'}$ 和 $\overline{\rho'u_i'u_j'}$ 等。

为了简化方程，引入了**[Favre平均](@entry_id:198824)**或**质量加权平均** [@problem_id:3357787]。对于任意变量 $\phi$，其[Favre平均](@entry_id:198824)定义为：
$$
\widetilde{\phi} = \frac{\overline{\rho \phi}}{\overline{\rho}}
$$
相应的，Favre分解将瞬时速度写为 $u_i = \widetilde{u_i} + u_i''$。注意，Favre脉动 $u_i''$ 的性质与雷诺脉动不同，其简单的[雷诺平均](@entry_id:754341) $\overline{u_i''}$ 不为零，但其质量加权平均为零：$\widetilde{u_i''} = 0$，或等价地 $\overline{\rho u_i''} = 0$。

使用[Favre平均](@entry_id:198824)的巨大优势在于，平均后的[对流](@entry_id:141806)项形式得以简化。平均动量方程中的总动量通量变为：
$$
\overline{\rho u_i u_j} = \overline{\rho} \widetilde{u_i} \widetilde{u_j} + \overline{\rho u_i'' u_j''}
$$
新的未封闭项是 $\overline{\rho u_i'' u_j''}$，通常记为 $\overline{\rho}\widetilde{u_i''u_j''}$。这被称为**Favre应力张量**。与标准[雷诺平均](@entry_id:754341)相比，方程形式更加简洁，与常密度[RANS方程](@entry_id:275032)非常相似，便于应用类似的封闭模型。

需要强调的是，Favre应力与[雷诺应力](@entry_id:263788)是不同的物理量。它们之间的关系可以通过推导得出，包含了密度与速度的复杂相关项。只有在密度恒定的极限下（$\rho' \to 0$），[Favre平均](@entry_id:198824)才退化为[雷诺平均](@entry_id:754341)，此时 $\widetilde{u_i} \to \overline{u_i}$， $u_i'' \to u_i'$，并且 $\widetilde{u_i''u_j''} \to \overline{u_i'u_j'}$，两种方法得到的方程和应力张量才完全一致 [@problem_id:3357787]。