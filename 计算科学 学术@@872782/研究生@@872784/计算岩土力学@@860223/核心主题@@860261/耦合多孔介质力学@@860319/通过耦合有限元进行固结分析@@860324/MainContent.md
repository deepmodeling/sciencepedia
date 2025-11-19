## 引言
固结是岩土工程中的一个核心现象，它控制着[地基沉降](@entry_id:755031)、边坡稳定以及土工结构物的长期性能。虽然经典的解析理论为理解一维固结提供了基础，但在面对复杂的几何形状、[非均质材料](@entry_id:196262)以及力学-水力[双向耦合](@entry_id:178809)的真实世界问题时，这些理论便显得力不从心。因此，建立一个能够[精确模拟](@entry_id:749142)固结过程的强大数值方法，对于现代岩土工程分析与设计至关重要。

本文旨在系统性地介绍基于[Biot理论](@entry_id:186785)的[耦合有限元](@entry_id:747964)[固结分析](@entry_id:747735)方法，引领读者从基本原理走向高级应用。在“原理与机制”一章中，我们将深入剖析控制固结过程的物理定律和数学方程，并详细阐述如何将其转化为稳健的有限元离散格式，同时讨论数值实施中的关键挑战。接下来，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示如何将该理论应用于解决实际工程问题，例如地基处理、土壤-大气相互作用和[水力压裂](@entry_id:750442)，并探讨其与多个学科的[交叉](@entry_id:147634)融合。最后，“动手实践”部分将提供一系列精心设计的练习，帮助您巩固所学知识，并将理论付诸实践。

## 原理与机制

本章深入探讨了饱和多孔介质[固结分析](@entry_id:747735)的物理原理和数学机制。我们将从多孔弹性力学的基本本构关系出发，建立控制固结过程的[耦合偏微分方程组](@entry_id:198181)。随后，我们将详细阐述如何将这些连续介质方程转化为适用于计算分析的有限元离散格式。最后，本章将讨论在数值实施过程中出现的关键挑战，如保证数值解的稳定性和选择高效的求解策略，为读者提供一个从理论到实践的完整知识框架。

### 多孔弹性力学的控制原理

[多孔介质力学](@entry_id:171662)，特别是[Biot理论](@entry_id:186785)，为描述流体饱和的变形固体提供了一个严谨的框架。其核心在于认识到总应力由固体骨架和孔隙流体共同承担，并且固体变形与孔隙流体压力之间存在[双向耦合](@entry_id:178809)。

#### [有效应力原理](@entry_id:755871)

[土力学](@entry_id:180264)中的一个基石是Terzaghi提出的[有效应力原理](@entry_id:755871)，Biot将其推广，以更普适的方式描述了总应力、有效应力和孔隙压力之间的关系。在[多孔介质](@entry_id:154591)中，宏观上的总柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 是由固体骨架承载的有效应力张量 $\boldsymbol{\sigma}'$ 和孔隙[流体压力](@entry_id:142203) $p$ 共同构成的。Biot的[有效应力原理](@entry_id:755871)（采用力学中拉为正、岩土中压为正的惯例有所不同，此处我们以拉应力为正，孔压为[压实](@entry_id:161543)性压力）可以表示为：

$ \boldsymbol{\sigma} = \boldsymbol{\sigma}' + \alpha p \boldsymbol{I} $

其中，$\boldsymbol{I}$ 是二阶单位张量，而 $\alpha$ 是无量纲的 **[Biot系数](@entry_id:183813)**。该系数反映了[孔隙压力](@entry_id:188528)对总应力的贡献程度。它并非一个经验参数，而是由材料的微观结构决定的物理量。具体而言，$\alpha$ 与多孔介质的骨架在排水条件下的[体积模量](@entry_id:160069) $K_d$ 和构[成骨](@entry_id:194658)架的固体颗粒本身的[体积模量](@entry_id:160069) $K_s$ 有关 [@problem_id:3509130]：

$ \alpha = 1 - \frac{K_d}{K_s} $

由于多孔骨架的压缩性总是大于或等于其组成固体颗粒的压缩性（即 $K_d \le K_s$），[Biot系数](@entry_id:183813)的取值范围为 $0 \le \alpha \le 1$。对于由不可压缩固体颗粒构成的材料（$K_s \to \infty$），$\alpha \to 1$，此时Biot的表达式退化为Terzaghi的形式。对于孔隙度趋于零的致密材料（$K_d \to K_s$），$\alpha \to 0$，[孔隙压力](@entry_id:188528)的影响将变得微不足道。

在此，必须将[Biot系数](@entry_id:183813) $\alpha$ 与另一个重要的岩土参数——**Skempton孔压系数 $B$** 明确区分开来。$\alpha$ 是一个基本的本构参数，直接出现在[应力分解](@entry_id:272862)的定义中。而 $B$ 是一个响应参数，定义为在不排水条件下，各向同性总应力增量 $\Delta \sigma_m$ 引起的孔隙压力增量 $\Delta p$ 的比值，即 $B = \Delta p / \Delta \sigma_m$。$B$ 的值不仅依赖于 $\alpha$ 和骨架的压缩性，还依赖于流体的压缩性，因此它描述的是整个[多孔介质](@entry_id:154591)系统在特定加载路径下的响应特性，而非一个独立的本构常数 [@problem_id:3509130]。

#### [本构关系](@entry_id:186508)

为了完整地描述固结过程，我们需要为固体骨架和孔隙流体分别建立本构关系。

对于固体骨架，我们假设其在排水条件下（即孔隙压力恒定）的行为是线弹性的。这意味着[有效应力](@entry_id:198048) $\boldsymbol{\sigma}'$ 与应变张量 $\boldsymbol{\varepsilon}$ 之间存在线性关系 [@problem_id:3509112]：

$ \boldsymbol{\sigma}' = \mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{u}) $

其中，$\boldsymbol{u}$ 是位移场，$\boldsymbol{\varepsilon}(\boldsymbol{u}) = \frac{1}{2}(\nabla \boldsymbol{u} + \nabla \boldsymbol{u}^\top)$ 是[小应变张量](@entry_id:754968)，$\mathbb{C}$ 是四阶的排水[弹性张量](@entry_id:170728)。

对于孔隙流体，其行为由质量守恒定律控制。单位体积内流体含量的变化率 $\dot{\zeta}$ 由两个因素引起：固体骨架的[体积应变率](@entry_id:272471)和孔隙压力的变化率。这一关系可以表示为 [@problem_id:3509112]：

$ \dot{\zeta} = \alpha \nabla \cdot \dot{\boldsymbol{u}} + S \dot{p} $

这里，$\nabla \cdot \dot{\boldsymbol{u}}$ 是[体积应变率](@entry_id:272471)，$\dot{p}$ 是[孔隙压力](@entry_id:188528)变化率。系数 $S$ 是**比储水系数**，表示在[体积应变](@entry_id:267252)不变时，单位[孔隙压力](@entry_id:188528)变化所引起的单位体积[多孔介质](@entry_id:154591)中流体含量的变化。它与流体压缩性、固体颗粒压缩性以及孔隙度有关。流体在[多孔介质](@entry_id:154591)中的流动则遵循**[达西定律](@entry_id:153223)**，即流体通量 $\boldsymbol{q}$ 与孔隙压力梯度成正比 [@problem_id:3509158]：

$ \boldsymbol{q} = -\boldsymbol{K} \nabla p $

其中 $\boldsymbol{K}$ 是[水力传导系数](@entry_id:149185)张量（在更基本的层面，$\boldsymbol{K} = \boldsymbol{k}/\mu_f$，其中 $\boldsymbol{k}$ 是渗透率张量，$\mu_f$ 是[流体粘度](@entry_id:267219)）。负号表示流体从高压区流向低压区。

#### 耦合控制方程：强形式

将上述物理原理——[有效应力](@entry_id:198048)、固体本构、流体储存和流动定律——与动量守恒和质量守恒相结合，我们便能得到描述准静态固结过程的[耦合偏微分方程组](@entry_id:198181)（强形式） [@problem_id:3509158]。

1.  **动量守恒方程**：在准静态（忽略[惯性力](@entry_id:169104)）条件下，总[应力的散度](@entry_id:185633)必须与体积力[相平衡](@entry_id:136822)。
    $ \nabla \cdot \boldsymbol{\sigma} + \rho \boldsymbol{b} = \boldsymbol{0} $
    将[有效应力原理](@entry_id:755871)和固体本构代入，得到以位移 $\boldsymbol{u}$ 和压力 $p$ 为未知量的力学[平衡方程](@entry_id:172166)：
    $ \nabla \cdot (\mathbb{C}:\boldsymbol{\varepsilon}(\boldsymbol{u}) - \alpha p \boldsymbol{I}) + \rho \boldsymbol{b} = \boldsymbol{0} $

2.  **流体质量守恒方程**：单位体积内流体质量的变化率等于流入的净通量加上源汇项。
    $ \frac{\partial \zeta}{\partial t} + \nabla \cdot \boldsymbol{q} = s $
    将流体储存和达西定律代入，得到以 $\boldsymbol{u}$ 和 $p$ 为未知量的[渗流](@entry_id:158786)[连续性方程](@entry_id:195013)：
    $ S \dot{p} + \alpha \nabla \cdot \dot{\boldsymbol{u}} - \nabla \cdot (\boldsymbol{K} \nabla p) = s $

这两个方程构成了Biot[固结理论](@entry_id:747736)的核心，清晰地展示了[位移场](@entry_id:141476)和压[力场](@entry_id:147325)之间的[双向耦合](@entry_id:178809)：压力 $p$ 作为一种体积荷载出现在力学方程中，而固体体积变化率 $\nabla \cdot \dot{\boldsymbol{u}}$ 则作为一种[源项](@entry_id:269111)出现在渗流方程中。

#### 极限情况：排水与[不排水响应](@entry_id:756307)

耦合系统的行为在两个时间极限下表现出显著不同的特征。

**瞬时响应（不排水条件）**：当荷载突然施加（$t \to 0$）时，孔隙中的流体来不及流出，此时系统处于不排水状态。这意味着流体含量变化为零，$\Delta \zeta = 0$。在这种约束下，[多孔介质](@entry_id:154591)表现出更高的刚度，其不排水体积模量 $K_u$ 高于排水体积模量 $K_d$。两者之间的关系为 [@problem_id:3509120]：

$ K_u = K_d + \frac{\alpha^2}{S} $

这个关系表明，流体的存在（通过 $\alpha$ 和 $S$ 体现）增强了材料抵[抗体](@entry_id:146805)积变形的能力。

**长期响应（排水条件）**：随着时间的推移（$t \to \infty$），超静孔隙压力逐渐消散，最终达到新的平衡状态，此时系统处于完全排水状态。孔隙压力不再随时间变化，[渗流](@entry_id:158786)方程中的时间导数项消失。

**与经典[固结理论](@entry_id:747736)的联系**：在某些简化假设下，Biot的耦合理论可以退化为更经典的Terzaghi[一维固结理论](@entry_id:752912)。例如，考虑一个一维问题，并假设总应力在加载后保持恒定，且材料参数均匀。在这些条件下，力学方程和[渗流](@entry_id:158786)方程可以被[解耦](@entry_id:637294)，最终得到一个仅关于[孔隙压力](@entry_id:188528) $p$ 的标准[热传导](@entry_id:147831)（或[扩散](@entry_id:141445)）方程 [@problem_id:3509088]：

$ \frac{\partial p}{\partial t} = c_v \frac{\partial^2 p}{\partial x^2} $

其中 $c_v$ 是**[固结系数](@entry_id:185948)**，它是一个综合了[材料力学](@entry_id:201885)性质（模量 $M$）、耦合性质（[Biot系数](@entry_id:183813) $\alpha$）和水力性质（渗透率 $k$、粘度 $\mu$）的常数：$c_v = \frac{k/\mu}{S + \alpha^2/M}$。这个简化过程揭示了[Biot理论](@entry_id:186785)作为更一般框架的地位。

### 有限元格式

为了对复杂的几何形状和边界条件下的固结问题进行数值求解，有限元方法（FEM）是一种强大而灵活的工具。其出发点是将控制方程的强形式转化为等价的积分形式，即[弱形式](@entry_id:142897)。

#### [弱形式](@entry_id:142897)（[变分形式](@entry_id:166033)）与边界条件

我们通过将强形式方程乘以相应的[检验函数](@entry_id:166589)（位移的检验函数 $\boldsymbol{w}$ 和压力的[检验函数](@entry_id:166589) $\eta$），然后在求解域 $\Omega$ 上积分，并利用分部积分（[格林公式](@entry_id:173118)）来推导弱形式。这个过程不仅降低了对解的[光滑性](@entry_id:634843)要求，而且自然地将边界条件引入了方程。

对于力学平衡方程，其[弱形式](@entry_id:142897)为 [@problem_id:3509158]：
$ \int_{\Omega} \boldsymbol{\varepsilon}(\boldsymbol{w}) : \mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{u}) \, \mathrm{d}\Omega - \int_{\Omega} \alpha (\nabla \cdot \boldsymbol{w}) p \, \mathrm{d}\Omega = \int_{\Omega} \boldsymbol{w} \cdot \rho \boldsymbol{b} \, \mathrm{d}\Omega + \int_{\Gamma_t} \boldsymbol{w} \cdot \bar{\boldsymbol{t}} \, \mathrm{d}\Gamma $

对于渗流[连续性方程](@entry_id:195013)，其[弱形式](@entry_id:142897)为 [@problem_id:3509158]：
$ \int_{\Omega} S \eta \, \dot{p} \, \mathrm{d}\Omega + \int_{\Omega} \alpha \eta \, \nabla \cdot \dot{\boldsymbol{u}} \, \mathrm{d}\Omega + \int_{\Omega} \nabla \eta \cdot \boldsymbol{K} \nabla p \, \mathrm{d}\Omega = \int_{\Omega} \eta s \, \mathrm{d}\Omega + \int_{\Gamma_q} \eta \bar{q} \, \mathrm{d}\Gamma $

在推导[弱形式](@entry_id:142897)的过程中，边界条件被明确区分为两类 [@problem_id:3509092]：
- **本质边界条件（[Dirichlet条件](@entry_id:137096)）**：这类条件直接施加在未知场变量上，例如在边界 $\Gamma_u$ 上指定位移 $\boldsymbol{u} = \bar{\boldsymbol{u}}$，或在边界 $\Gamma_p$ 上指定压力 $p = \bar{p}$。在有限元中，这些条件通过直接约束解空间的[基函数](@entry_id:170178)来实现。
- **自然边界条件（[Neumann条件](@entry_id:165471)）**：这类条件通过[分部积分](@entry_id:136350)自然地出现在弱形式的边界积分项中。例如，在边界 $\Gamma_t$ 上施加的总法向应力（面力）$\bar{\boldsymbol{t}} = \boldsymbol{\sigma} \boldsymbol{n}$，以及在边界 $\Gamma_q$ 上施加的法向流体通量 $\bar{q} = -\boldsymbol{K} \nabla p \cdot \boldsymbol{n}$。

对于纯[Neumann问题](@entry_id:176713)（即整个边界都施加自然边界条件），为了保证解的存在性和唯一性，必须满足一定的**全局相容性约束**。例如，对于力学问题，所有外力（包括[体力](@entry_id:174230)与面力）的主矢和主矩必须为零，以保证[静力平衡](@entry_id:163498)。对于[稳态](@entry_id:182458)[渗流](@entry_id:158786)问题，流入域内的总流量必须等于流出的总流量，以保证质量守恒 [@problem_id:3509092]。

#### 空间与[时间离散化](@entry_id:169380)

在得到[弱形式](@entry_id:142897)后，我们采用伽辽金方法进行[空间离散化](@entry_id:172158)。将未知位移场 $\boldsymbol{u}$ 和压[力场](@entry_id:147325) $p$ 分别用其所在有限元空间中的一组[基函数](@entry_id:170178)（形函数）$\boldsymbol{N}_u$ 和 $\boldsymbol{N}_p$ 的[线性组合](@entry_id:154743)来近似：
$ \boldsymbol{u}(\boldsymbol{x}, t) \approx \boldsymbol{u}_h(\boldsymbol{x}, t) = \boldsymbol{N}_u(\boldsymbol{x}) \boldsymbol{U}(t) $
$ p(\boldsymbol{x}, t) \approx p_h(\boldsymbol{x}, t) = \boldsymbol{N}_p(\boldsymbol{x}) \boldsymbol{P}(t) $
其中 $\boldsymbol{U}(t)$ 和 $\boldsymbol{P}(t)$ 是待求的节点未知向量。将这些近似代入弱形式，即可得到一个关于时间 $t$ 的[常微分方程组](@entry_id:266774)（[半离散系统](@entry_id:754680)） [@problem_id:3509158]：

$ \begin{pmatrix} \boldsymbol{0} & \boldsymbol{0} \\ \boldsymbol{Q}^\top & \boldsymbol{S}_p \end{pmatrix} \begin{pmatrix} \dot{\boldsymbol{U}} \\ \dot{\boldsymbol{P}} \end{pmatrix} + \begin{pmatrix} \boldsymbol{K}_{uu} & -\boldsymbol{Q} \\ \boldsymbol{0} & \boldsymbol{K}_{pp} \end{pmatrix} \begin{pmatrix} \boldsymbol{U} \\ \boldsymbol{P} \end{pmatrix} = \begin{pmatrix} \boldsymbol{F}_u \\ \boldsymbol{F}_p \end{pmatrix} $

这里的矩阵分别代表：
- $\boldsymbol{K}_{uu}$: 骨架刚度矩阵
- $\boldsymbol{S}_p$: 压缩储水矩阵
- $\boldsymbol{K}_{pp}$: 渗透矩阵
- $\boldsymbol{Q}$: [耦合矩阵](@entry_id:191757)
- $\boldsymbol{F}_u$, $\boldsymbol{F}_p$: 外荷载与源汇项向量

接下来，我们对时间进行离散化。一个常用且稳健的方法是**向后欧拉法**（完全[隐式格式](@entry_id:166484)）。在该方法中，时间导数用差分近似，例如 $\dot{\boldsymbol{P}}^{n+1} \approx (\boldsymbol{P}^{n+1} - \boldsymbol{P}^n) / \Delta t$，并且所有项都在新的时间步 $t^{n+1}$ 处取值。这样处理后，我们得到一个在每个时间步都需要求解的大型线性代数方程组，即**整体（monolithic）系统** [@problem_id:3509144]：

$ \begin{pmatrix} \boldsymbol{K}_{uu} & -\boldsymbol{Q} \\ \frac{1}{\Delta t} \boldsymbol{Q}^\top & \frac{1}{\Delta t} \boldsymbol{S}_p + \boldsymbol{K}_{pp} \end{pmatrix} \begin{pmatrix} \boldsymbol{U}^{n+1} \\ \boldsymbol{P}^{n+1} \end{pmatrix} = \begin{pmatrix} \boldsymbol{F}_u^{n+1} \\ \boldsymbol{F}_p^{n+1} + \frac{1}{\Delta t} (\boldsymbol{Q}^\top \boldsymbol{U}^n + \boldsymbol{S}_p \boldsymbol{P}^n) \end{pmatrix} $

求解这个[方程组](@entry_id:193238)即可得到下一时刻的位移和[孔隙压力](@entry_id:188528)。

### 高等数值专题与挑战

尽管上述有限元格式在理论上是完善的，但在实际计算中会遇到一些深刻的挑战，主要涉及数值稳定性和求解效率。

#### [混合格式](@entry_id:167436)的稳定性：LBB 条件

Biot固结问题的 $(\boldsymbol{u}, p)$ [混合有限元](@entry_id:178533)格式在数学上属于一个“[鞍点问题](@entry_id:174221)”。这类问题的数值稳定性，特别是在某些物理极限情况下，需要满足一个关键的数学条件，即**Ladyzhenskaya–Babuška–Brezzi (LBB) 条件**（或称[inf-sup条件](@entry_id:746626)）。

这个条件要求位移和压力的有限元插值空间必须“兼容”。直观地说，位移空间必须足够“丰富”，能够表示出对任何非零[压力模](@entry_id:159654)式的响应。当材料趋于不可压缩（骨架或流体不可压缩）或[渗透性](@entry_id:154559)极低时，固结方程中的约束性增强，此时如果[LBB条件](@entry_id:746626)不被满足，数值解中就会出现非物理的、棋盘状的**伪压力[振荡](@entry_id:267781)** [@problem_id:3509164]。

一个典型的例子是，如果对位移和压力采用相同阶次的连续[插值函数](@entry_id:262791)（例如，线性的P1/P1单元或双线性的Q1/Q1单元），[LBB条件](@entry_id:746626)通常是不满足的。我们可以通过一个简单的一维例子来说明：对于一个由P1单元构成的压[力场](@entry_id:147325)，如果其节点值在$+1$和$-1$之间交替，那么在每个单元内部，该压[力场](@entry_id:147325)的积分为零。这意味着这种[压力模](@entry_id:159654)式对于由P1单元构成的位移场（其散度在单元上是常数）是“不可见的”，从而导致其在离散系统中无法被唯一确定，引发[振荡](@entry_id:267781) [@problem_id:3509154]。

这种数值不稳定性在以下物理情境下尤为突出：低[渗透性](@entry_id:154559)($k \to 0$)、低压缩性($S \to 0$)、小时间步长($\Delta t \to 0$) [@problem_id:3509164]。在这种情况下，渗流方程退化为一个对位移散度的纯约束，[LBB条件](@entry_id:746626)的满足与否成为决定性的。

解决LBB不稳定性问题主要有两种途径：
1.  **选择稳定的单元组合**：采用满足[LBB条件](@entry_id:746626)的单元，例如对位移使用比压力更高阶的插值，如[Taylor-Hood单元](@entry_id:165658)（$P_2/P_1$单元，即二次位移、线性压力）[@problem_id:3509154]。
2.  **使用稳定化方法**：对不满足[LBB条件](@entry_id:746626)的单元组合（如等阶元）的离散方程进行修正，添加一个“稳定项”。这个稳定项能惩罚[伪压力模式](@entry_id:755261)，但它必须是**一致的**，即对于精确解它为零，从而不改变原始问题的解。例如，基于残差的压力稳定化[Petrov-Galerkin](@entry_id:174072) (PSPG) 方法或伽辽金最小二乘 (GLS) 方法就是这类技术的代表 [@problem_id:3509164]。

值得注意的是，当流体或骨架具有显著的[可压缩性](@entry_id:144559)时，渗流方程中的储水项 $\boldsymbol{S}_p$ 会在离散系统的对角线上提供一个足够大的正定项，使得系统不再是纯粹的[鞍点问题](@entry_id:174221)，此时即使使用[等阶单元](@entry_id:174194)，压力[振荡](@entry_id:267781)也可能被抑制 [@problem_id:3509164]。

#### 求解策略：整体求解与交错求解

求解每个时间步的完全耦合的整体[线性系统](@entry_id:147850)，虽然稳健，但计算成本高昂，因为它涉及一个大规模、非对称的矩阵。为了提高[计算效率](@entry_id:270255)，研究者们发展了多种**交错（staggered）求解算法**，也称为[算子分裂法](@entry_id:752962)。

一个常见的交错格式是“[固定应力分裂](@entry_id:749440)”（fixed-stress split）。在一个时间步内，它将耦合[问题分解](@entry_id:272624)为两个子问题顺序求解 [@problem_id:3509138]：
1.  **力学步**：假设[孔隙压力](@entry_id:188528)为上一时刻的值 $p^n$，求解一个标准的弹性力学问题，得到当前时刻的位移 $\boldsymbol{U}^{n+1}$。
    $ \boldsymbol{K}_{uu} \boldsymbol{U}^{n+1} = \boldsymbol{F}_u^{n+1} + \boldsymbol{Q} \boldsymbol{P}^n $
2.  **渗流步**：利用上一步计算出的位移 $\boldsymbol{U}^{n+1}$，求解一个渗流问题，得到当前时刻的压力 $\boldsymbol{P}^{n+1}$。
    $ (\frac{1}{\Delta t} \boldsymbol{S}_p + \boldsymbol{K}_{pp}) \boldsymbol{P}^{n+1} = \boldsymbol{F}_p^{n+1} + \frac{1}{\Delta t} (\boldsymbol{S}_p \boldsymbol{P}^n - \boldsymbol{Q}^\top (\boldsymbol{U}^{n+1} - \boldsymbol{U}^n)) $

这种交错格式的优点在于，每一步求解的都是规模更小、且通常是更为良态（如对称正定）的线性系统，计算上更为高效。然而，它也引入了所谓的“[分裂误差](@entry_id:755244)”。对于上述格式，它在数学上等价于对整体系统进行一次块[高斯-赛德尔迭代](@entry_id:136271) [@problem_id:3509138]。

关于这种交错格式的性质，有以下几点结论 [@problem_id:3509138]：
- **稳定性**：对于线性多孔弹性问题，当每个子问题都采用无条件稳定的向后欧拉法求解时，这种交错格式本身也是**[无条件稳定](@entry_id:146281)**的。
- **精度**：由于分裂操作，该格式的精度通常低于同阶的整体格式。对于基于一阶向后欧拉法的分裂，其全局时间精度仍为一阶，即 $\mathcal{O}(\Delta t)$。
- **收敛性**：[分裂误差](@entry_id:755244)的大小与时间步长 $\Delta t$ 相关。随着 $\Delta t \to 0$，交错解会收敛到整体解。此外，如果在每个时间步内对这两个子问题进行迭代，直至位移和压力收敛（即执行多次块[高斯-赛德尔迭代](@entry_id:136271)），那么最终得到的解将与整体求解的解完全相同 [@problem_id:3509138]。

因此，在整体求解和交错求解之间存在一个权衡：整体法更为稳健和精确，而交错法在计算上更具吸[引力](@entry_id:175476)，但可能需要更小的时间步长或内部迭代来保证精度。