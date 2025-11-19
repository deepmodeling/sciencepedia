## 引言
在计算流体动力学（CFD）领域，准确模拟[湍流](@entry_id:151300)是核心挑战之一。直接求解包含所有尺度涡旋的[Navier-Stokes方程](@entry_id:161487)（DNS）在计算上极为昂贵，因此工程实践普遍依赖于[雷诺平均](@entry_id:754341)[Navier-Stokes](@entry_id:276387)（RANS）方法。然而，RANS方法引入了未知的[雷诺应力](@entry_id:263788)项，带来了所谓的“[湍流封闭问题](@entry_id:268973)”。$k-\varepsilon$模型作为一种经典的双方程[湍流模型](@entry_id:190404)，通过引入两个独立的输运方程来描述[湍流](@entry_id:151300)的特征尺度，为这一问题提供了计算高效且相对准确的解决方案。

本文旨在深入剖析[湍动能](@entry_id:262712)（$k$）与其耗散率（$\varepsilon$）输运方程的理论、应用与实践。读者将系统地学习到：
在 **“原理与机制”** 一章中，我们将从[RANS方程](@entry_id:275032)和[Boussinesq假设](@entry_id:272519)出发，详细推导并解释$k$和$\varepsilon$[输运方程](@entry_id:756133)中各项的物理意义与模型化过程，并探讨模型常数的校准原理及其内在局限性。
在 **“应用与跨学科联系”** 一章中，我们将展示$k-\varepsilon$模型如何应用于分析经典[湍流](@entry_id:151300)现象和解决复杂的工程问题，并探讨其如何通过修正与扩展，与传热、地球物理、[高速空气动力学](@entry_id:272086)等领域[交叉](@entry_id:147634)融合。
最后，在 **“动手实践”** 部分，您将通过一系列精心设计的问题，将理论知识应用于实际分析，加深对模型平衡关系、数值实现和适用边界的理解。

## 原理与机制

在对[湍流](@entry_id:151300)进行[雷诺平均](@entry_id:754341)[Navier-Stokes](@entry_id:276387) (RANS) 方程模拟时，核心挑战在于如何对未知的雷诺应力项进行建模。双方程模型，特别是$k-\varepsilon$模型，通过引入两个额外的[输运方程](@entry_id:756133)来封闭[RANS方程](@entry_id:275032)，从而提供了一种在计算成本和物理保真度之间取得平衡的有效方法。本章将深入探讨湍动能$k$和其耗散率$\varepsilon$的[输运方程](@entry_id:756133)背后的基本原理和力学机制，从它们的物理定义到模型方程的构建，再到常数的校准和模型的内在局限性。

### [雷诺平均](@entry_id:754341)[Navier-Stokes方程](@entry_id:161487)与[湍流封闭问题](@entry_id:268973)

对不可压缩牛顿流体的瞬时[Navier-Stokes方程](@entry_id:161487)进行[雷诺平均](@entry_id:754341)后，我们得到[RANS方程](@entry_id:275032)。对于[平均速度](@entry_id:267649)场$\bar{u}_i$，动量方程呈现出以下形式：
$$
\frac{\partial \bar{u}_i}{\partial t} + \bar{u}_j \frac{\partial \bar{u}_i}{\partial x_j} = -\frac{1}{\rho} \frac{\partial \bar{p}}{\partial x_i} + \nu \frac{\partial^2 \bar{u}_i}{\partial x_j \partial x_j} - \frac{\partial \overline{u'_i u'_j}}{\partial x_j}
$$
与原始的[Navier-Stokes方程](@entry_id:161487)相比，此方程中出现了一个新的项：[雷诺应力张量](@entry_id:270803)$-\rho\overline{u'_i u'_j}$的散度。此项源于对[非线性](@entry_id:637147)的[对流](@entry_id:141806)项$u_j \frac{\partial u_i}{\partial x_j}$进行平均时产生的速度脉动相关项。从物理上看，雷诺应力代表了由湍流涡旋引起的[动量输运](@entry_id:139628)。从数学上看，它引入了新的未知量，使得平均动量方程与平均[连续性方程](@entry_id:195013)构成的[方程组](@entry_id:193238)不封闭。为了求解平均流动，我们必须建立一个模型，将雷诺应力与已知的平均流场量（如平均速度梯度）联系起来。这个问题被称为**[湍流封闭问题](@entry_id:268973)**。[@problem_id:3384777]

一个基础且广泛应用的封闭策略是 **Boussinesq涡粘性假设**。该假设类比分子粘性引起的粘性[应力与[应变](@entry_id:263123)率](@entry_id:154778)之间的[线性关系](@entry_id:267880)，提出[雷诺应力](@entry_id:263788)的非各向同性部分与平均应变率张量$\bar{S}_{ij} = \frac{1}{2}\left( \frac{\partial \bar{u}_i}{\partial x_j} + \frac{\partial \bar{u}_j}{\partial x_i} \right)$成正比。对于不可压缩流体，该关系可以写为：
$$
-\overline{u'_i u'_j} = 2 \nu_t \bar{S}_{ij} - \frac{2}{3} k \delta_{ij}
$$
这里，$\nu_t$是**[湍流涡](@entry_id:266898)粘性系数**（turbulent or eddy viscosity），它是一个标量，代表了[湍流](@entry_id:151300)对[动量输运](@entry_id:139628)的增强效应，通常远大于分子粘性系数$\nu$。$k$是湍动能，$\delta_{ij}$是克罗内克符号。这一假设的优点在于其简洁性，并将复杂的张量封闭问题简化为确定标量场$\nu_t$的问题。为了确定$\nu_t$，我们需要了解[湍流](@entry_id:151300)的特征尺度，这自然引出了[湍动能](@entry_id:262712)$k$和耗散率$\varepsilon$的概念。[@problem_id:3384777]

### [湍流](@entry_id:151300)尺度：湍动能与耗散率

为了构建一个适用于广泛流动的涡粘性模型，我们需要基于流动的局部状态来确定$\nu_t$的值。这需要引入描述[湍流](@entry_id:151300)强度和尺度的关键物理量。

**[湍动能](@entry_id:262712) (Turbulent Kinetic Energy, $k$)**

[湍动能](@entry_id:262712)$k$定义为单位质量流体所具有的脉动动能，即：
$$
k = \frac{1}{2} \overline{u'_i u'_i} = \frac{1}{2} \left( \overline{u'_1 u'_1} + \overline{u'_2 u'_2} + \overline{u'_3 u'_3} \right)
$$
由于$k$是速度脉动分量平方和的平均值，而平方项总是非负的，因此$k$本身是一个**非负标量**（$k \ge 0$）。这一物理约束对模型的数值实现至关重要。从量纲上看，速度的量纲是$L T^{-1}$，因此$k$的量纲是$(L T^{-1})^2 = L^2 T^{-2}$，代表单位质量的能量。物理上，$k$度量了[湍流](@entry_id:151300)脉动的强度。$k$越大，意味着流体质点在平均运动轨迹周围的随机运动越剧烈。[@problem_id:3384749] [@problem_id:3384766]

**耗散率 (Dissipation Rate, $\varepsilon$)**

[湍流](@entry_id:151300)是一种[耗散结构](@entry_id:181361)，若没有能量的持续输入，[湍流](@entry_id:151300)最终会因粘性作用而衰减。**[湍流耗散率](@entry_id:756234)**$\varepsilon$定义为单位质量流体中，[湍动能](@entry_id:262712)通过分子粘性转化为内能（热能）的速率。根据热力学第二定律，这个过程是不可逆的，因此$\varepsilon$也是一个**非负标量**（$\varepsilon \ge 0$）。其精确定义为：
$$
\varepsilon = \nu \overline{\frac{\partial u'_i}{\partial x_j} \frac{\partial u'_i}{\partial x_j}} = 2 \nu \overline{s'_{ij} s'_{ij}}
$$
其中$s'_{ij}$是脉动[应变率张量](@entry_id:266108)。这个表达式表明，$\varepsilon$是一个由脉动[速度梯度](@entry_id:261686)的平方构成并由粘性系数加权的量，因此其值必然为非负。量纲分析表明，[运动粘度](@entry_id:275614)$\nu$的量纲为$L^2 T^{-1}$，速度梯度$\partial u'_i / \partial x_j$的量纲为$T^{-1}$，因此$\varepsilon$的量纲为$(L^2 T^{-1}) \cdot (T^{-1})^2 = L^2 T^{-3}$。这与单位质量的功率（能量/时间）的量纲相符。[@problem_id:3384749] [@problem_id:3384766]

在 Kolmogorov 的[湍流理论](@entry_id:264896)中，$\varepsilon$扮演着核心角色。在高[雷诺数](@entry_id:136372)[湍流](@entry_id:151300)中，存在一个能量级串过程：大尺度涡从平均流中获取能量，通过[非线性](@entry_id:637147)相互作用将[能量传递](@entry_id:174809)给中等尺度的涡，再依次传递给更小尺度的涡，最终在最小的尺度上由[粘性耗散](@entry_id:143708)。$\varepsilon$不仅是最终的耗散率，也被认为是能量在[惯性子区](@entry_id:273327)（即中间尺度范围）中从大尺度向小尺度传递的通量率。Kolmogorov 假设，在[湍流](@entry_id:151300)充分发展的情况下，最小的、受粘性主导的尺度（称为Kolmogorov微尺度）仅由$\nu$和$\varepsilon$决定。通过量纲分析，我们可以得到[Kolmogorov长度尺度](@entry_id:262467)$\eta$、速度尺度$u_\eta$和时间尺度$\tau_\eta$：
$$
\eta = \left( \frac{\nu^3}{\varepsilon} \right)^{1/4}, \quad u_\eta = (\nu \varepsilon)^{1/4}, \quad \tau_\eta = \left( \frac{\nu}{\varepsilon} \right)^{1/2}
$$
在这些最小尺度上，[雷诺数](@entry_id:136372)$Re_\eta = u_\eta \eta / \nu$的量级为1，这标志着[惯性力](@entry_id:169104)与[粘性力](@entry_id:263294)[达到平衡](@entry_id:170346)，能量级串终止。[@problem_id:3384709]

### [涡粘度](@entry_id:155814)模型的构建

有了描述[湍流](@entry_id:151300)特征速度和时间的尺度，$k$和$\varepsilon$，我们便可以构建涡粘性系数$\nu_t$的模型。回顾Prandtl的[混合长度理论](@entry_id:752030)，涡粘性系数可以被看作是流体密度、一个特征速度和一个特征长度的乘积。在双方程模型的框架下，我们可以从$k$和$\varepsilon$中提取这些尺度。

- 一个自然的**[特征速度](@entry_id:165394)尺度**$v_t$可以从湍动能$k$得到，即$v_t \sim \sqrt{k}$，其量纲为$L T^{-1}$。
- 一个**[特征时间尺度](@entry_id:276738)**$t_t$可以被认为是[能量尺度](@entry_id:196201)涡的翻转时间，即湍动能与其耗散率之比：$t_t \sim k/\varepsilon$。其量纲为$(L^2 T^{-2}) / (L^2 T^{-3}) = T$。

通过这两个尺度，我们可以构造出一个**[特征长度尺度](@entry_id:266383)**$\ell_t = v_t t_t \sim \sqrt{k} (k/\varepsilon) = k^{3/2}/\varepsilon$。现在，我们可以仿照[分子运动论](@entry_id:145023)中的[扩散](@entry_id:141445)系数，将涡粘性系数$\nu_t$表示为[特征速度](@entry_id:165394)和特征长度的乘积：
$$
\nu_t \propto v_t \ell_t \sim \sqrt{k} \cdot \frac{k^{3/2}}{\varepsilon} = \frac{k^2}{\varepsilon}
$$
引入一个无量纲的模型常数$C_\mu$，我们便得到了标准$k-\varepsilon$模型中的涡粘性公式：
$$
\nu_t = C_\mu \frac{k^2}{\varepsilon}
$$
这个公式是$k-\varepsilon$模型的基石，它将待求的涡粘性系数与两个通过输运方程求解的[湍流](@entry_id:151300)量$k$和$\varepsilon$联系了起来。常数$C_\mu$是一个通过实验数据校准得到的经验参数，其标准值约为$0.09$。[@problem_id:3384728]

### [湍动能](@entry_id:262712) $k$ 的输运方程

为了求解$k$和$\varepsilon$的空间和时间[分布](@entry_id:182848)，我们需要为它们建立各自的输运方程。这些方程可以从瞬时的[Navier-Stokes方程](@entry_id:161487)严格推导，但推导过程中会产生更多未知的更高阶相关项。因此，在工程应用中，我们使用的是经过模型化封闭的输运方程。

模型化的$k$方程具有普适的[输运方程](@entry_id:756133)形式，包含了[对流](@entry_id:141806)、[扩散](@entry_id:141445)、生成和耗散等项：
$$
\frac{\partial k}{\partial t} + \bar{u}_j \frac{\partial k}{\partial x_j} = \frac{\partial}{\partial x_j} \left[ \left(\nu + \frac{\nu_t}{\sigma_k}\right) \frac{\partial k}{\partial x_j} \right] + P_k - \varepsilon
$$

- **[对流](@entry_id:141806)项 (Convection):** $\frac{\partial k}{\partial t} + \bar{u}_j \frac{\partial k}{\partial x_j}$ 描述了$k$随平均流动的输运。

- **生成项 $P_k$ (Production):** $P_k$代表了通过[雷诺应力](@entry_id:263788)做功，平均流动的动能转化为[湍动能](@entry_id:262712)的速率。其精确形式为$P_k = -\overline{u'_i u'_j} \frac{\partial \bar{u}_i}{\partial x_j}$。将[Boussinesq假设](@entry_id:272519)代入并考虑不可压缩流体 ($\partial \bar{u}_i/\partial x_i = 0$)，生成项可以表示为：
$$
P_k = 2 \nu_t \bar{S}_{ij} \bar{S}_{ij}
$$
这一项表明，只有当流动中存在平均应变率（即速度梯度）时，湍动能才能从平均流中产生。例如，考虑一个在某点处平均[速度梯度张量](@entry_id:270928)为 $\frac{\partial U_i}{\partial x_j} = \begin{pmatrix} 0  40  0 \\ -10  0  30 \\ 0  -20  0 \end{pmatrix} \, \mathrm{s^{-1}}$ 的流动。我们可以计算出对称的平均[应变率张量](@entry_id:266108) $\mathbf{S} = \begin{pmatrix} 0  15  0 \\ 15  0  5 \\ 0  5  0 \end{pmatrix} \, \mathrm{s^{-1}}$。该张量的二阶[不变量](@entry_id:148850)为 $S_{ij}S_{ij} = \sum_{i,j} S_{ij}^2 = 500 \, \mathrm{s^{-2}}$。若该点处的$k=0.60 \, \mathrm{m^2 s^{-2}}$ 且 $\varepsilon=0.30 \, \mathrm{m^2 s^{-3}}$，并使用$C_\mu = 0.09$，我们可以计算出涡粘性$\nu_t = 0.09 \frac{(0.60)^2}{0.30} = 0.108 \, \mathrm{m^2 s^{-1}}$。进而，湍动能生成率为$P_k = 2 \times 0.108 \times 500 = 108.0 \, \mathrm{m^2 s^{-3}}$。这清晰地展示了平均流变形如何驱动[湍流](@entry_id:151300)的产生。[@problem_id:3384784]

- **耗散项 $\varepsilon$ (Dissipation):** 如前所述，$\varepsilon$ 作为 $k$ 方程中的汇项，精确地代表了[湍动能](@entry_id:262712)因粘性作用转化为内能的速率。在许多达到平衡的[湍流](@entry_id:151300)中（如[边界层](@entry_id:139416)[对数律区](@entry_id:264342)），生成项 $P_k$ 与耗散项 $\varepsilon$ 近似相等。

- **[扩散](@entry_id:141445)项 (Diffusion):** $\frac{\partial}{\partial x_j} \left[ \left(\nu + \frac{\nu_t}{\sigma_k}\right) \frac{\partial k}{\partial x_j} \right]$ 描述了$k$在空间中的输运。它包含两部分：分子扩散（由$\nu$引起）和[湍流](@entry_id:151300)[扩散](@entry_id:141445)（由$\nu_t$引起）。[湍流](@entry_id:151300)[扩散](@entry_id:141445)项源于对精确$k$方程中湍动能通量三阶相关项$\overline{u'_j k'}$的建模。类似于动量和热量的[湍流输运](@entry_id:150198)，我们采用**梯度[扩散](@entry_id:141445)假设**，认为[湍流](@entry_id:151300)会倾向于将[湍动能](@entry_id:262712)从高浓度区域输运到低浓度区域：
$$
\overline{u'_j k'} \approx -D_k \frac{\partial k}{\partial x_j}
$$
其中$D_k$是$k$的[湍流扩散系数](@entry_id:196515)。基于[混合长度理论](@entry_id:752030)的[尺度分析](@entry_id:153681)表明，$D_k$和$\nu_t$具有相同的量纲和[尺度依赖性](@entry_id:197044)（均与[特征速度](@entry_id:165394)和长度的乘积成正比），因此可以合理地假设它们成正比：$D_k = \nu_t / \sigma_k$。这里的$\sigma_k$是一个无量纲常数，称为**[湍流普朗特数](@entry_id:153739)**（或[施密特数](@entry_id:141441)），它量化了动量[湍流](@entry_id:151300)[扩散](@entry_id:141445)与[湍动能](@entry_id:262712)[湍流](@entry_id:151300)[扩散](@entry_id:141445)的[相对效率](@entry_id:165851)。$\sigma_k$的标准值通常取为$1.0$。[@problem_id:3384705]

### 耗散率 $\varepsilon$ 的[输运方程](@entry_id:756133)

为封闭整个模型，我们还需要一个关于$\varepsilon$的输运方程。

**精确方程的复杂性**

与$k$方程类似，$\varepsilon$的精确[输运方程](@entry_id:756133)也可以从[Navier-Stokes方程](@entry_id:161487)推导出来。然而，其结果极其复杂，包含了大量更难以处理的、物理意义不明确的高阶相关项。例如，方程中会出现涉及脉动[压力梯度](@entry_id:274112)、速度梯度、[涡量](@entry_id:142747)拉伸（vortex stretching）以及四阶速度相关等极其复杂的项。这些项的直接建模被认为是几乎不可能完成的任务，因为我们对这些小尺度[湍流](@entry_id:151300)动力学过程的理解非常有限。[@problem_id:3384708]

**模型化方程**

因此，$\varepsilon$的输运方程在很大程度上是基于物理直觉和[量纲分析](@entry_id:140259)构建的现象学模型，而非对精确方程各项的逐一近似。其[标准形式](@entry_id:153058)为：
$$
\frac{\partial \varepsilon}{\partial t} + \bar{u}_j \frac{\partial \varepsilon}{\partial x_j} = \frac{\partial}{\partial x_j} \left[ \left(\nu + \frac{\nu_t}{\sigma_\varepsilon}\right) \frac{\partial \varepsilon}{\partial x_j} \right] + C_{\varepsilon1} \frac{\varepsilon}{k} P_k - C_{\varepsilon2} \frac{\varepsilon^2}{k}
$$
- **[对流](@entry_id:141806)和[扩散](@entry_id:141445):** $\varepsilon$的[对流](@entry_id:141806)项与$k$类似。[扩散](@entry_id:141445)项也采用梯度[扩散](@entry_id:141445)假设，引入了另一个模型常数$\sigma_\varepsilon$。

- **源项和汇项:** 这是$\varepsilon$方程建模的核心。
    - **生成项 $C_{\varepsilon1} \frac{\varepsilon}{k} P_k$:** 该项模拟耗散的产生。其物理逻辑是：平均流的剪切首先产生大尺度涡（由$P_k$体现），这些大尺度涡随后破碎成小尺度涡，最终导致耗散。因此，$\varepsilon$的产生率应与$k$的产生率$P_k$相关。因子$\varepsilon/k$(量纲为$T^{-1}$)被引入以确保量纲正确，它代表了[湍流](@entry_id:151300)的特征频率。
    - **耗散项 $C_{\varepsilon2} \frac{\varepsilon^2}{k}$:** 该项模拟耗散自身的衰减。这个过程被认为是[湍流](@entry_id:151300)内在的[非线性](@entry_id:637147)过程，与平均流的剪切无关。其形式可以通过对无平均剪切的均匀各向同性衰减[湍流](@entry_id:151300)的分析得到，其中$\varepsilon$的衰减率被发现与$\varepsilon^2/k$成正比。

$C_{\varepsilon1}$和$C_{\varepsilon2}$是两个关键的经验常数，它们将极其复杂的耗散动力学（如涡拉伸和压力-应变相关）压缩进了这两个看似简单的项中。[@problem_id:3384708]

### 模型常数的校准与物理约束

$k-\varepsilon$模型包含一组 "标准" 的经验常数：
$C_\mu = 0.09, \quad C_{\varepsilon1} = 1.44, \quad C_{\varepsilon2} = 1.92, \quad \sigma_k = 1.0, \quad \sigma_\varepsilon = 1.3$
这些数值并非随意选取，而是通过对一系列经典[湍流](@entry_id:151300)（如均匀各向同性衰减[湍流](@entry_id:151300)、均匀[剪切流](@entry_id:266817)以及壁[湍流](@entry_id:151300)）的理论分析和实验[数据拟合](@entry_id:149007)得到的。

**对数律层的一致性**

其中最重要的校准依据之一是要求模型能够正确再现高[雷诺数](@entry_id:136372)下壁[湍流](@entry_id:151300)中的**[对数律区](@entry_id:264342) (logarithmic layer)**。在该区域内，实验和理论表明：
1.  [湍动能](@entry_id:262712)生成与耗散达到[局部平衡](@entry_id:156295)，即$P_k \approx \varepsilon$。
2.  [平均速度](@entry_id:267649)剖面满足对数律$\frac{\bar{u}}{u_\tau} = \frac{1}{\kappa} \ln\left(\frac{y u_\tau}{\nu}\right) + B$，其中$u_\tau$是壁面[摩擦速度](@entry_id:267882)，$\kappa \approx 0.41$是[冯·卡门常数](@entry_id:261117)。
3.  [湍流](@entry_id:151300)量具有特定的[标度律](@entry_id:139947)，如$k \approx u_\tau^2 / \sqrt{C_\mu}$（即$k$近似为常数），且$\varepsilon \approx u_\tau^3 / (\kappa y)$。

通过将这些条件代入模型化的$k$和$\varepsilon$[输运方程](@entry_id:756133)，可以推导出一系列关于模型常数的约束关系。例如，$C_\mu$的值直接由[对数律区](@entry_id:264342)测得的$k/u_\tau^2$的平台值确定。更进一步，对$\varepsilon$方程进行分析，可以得到一个连接$\kappa, C_\mu, C_{\varepsilon1}, C_{\varepsilon2}, \sigma_\varepsilon$的代数关系：
$$
\sigma_\varepsilon = \frac{\kappa^2}{(C_{\varepsilon2} - C_{\varepsilon1})\sqrt{C_\mu}}
$$
这个关系确保了当其他常数确定后，模型能够自洽地维持$\varepsilon \propto 1/y$的剖面。这也解释了为何$\sigma_\varepsilon$(约1.3)通常取值大于$\sigma_k$(约1.0)。因为在[对数律区](@entry_id:264342)，$k$的剖面相对平坦，而$\varepsilon$的剖面较陡峭。为了维持这个更陡峭的梯度，模型需要一个相对较弱的[扩散机制](@entry_id:158710)，即较大的[湍流普朗特数](@entry_id:153739)$\sigma_\varepsilon$（因为[扩散](@entry_id:141445)系数与$1/\sigma_\varepsilon$成正比）。[@problem_id:3384697] [@problem_id:3384710]

**物理[可实现性](@entry_id:193701) (Physical Realizability)**

正如前面强调的，$k$和$\varepsilon$分别代表能量和能量耗散率，它们必须始终为非负。然而，在数值计算中，由于离散误差，特别是在[对流](@entry_id:141806)项的处理上，可能会导致$k$或$\varepsilon$的计算值出现负值。这种违反**物理[可实现性](@entry_id:193701)**的情况会带来灾难性的后果。
-   如果$k0$，这本身就是物理上的荒谬。
-   如果$\varepsilon0$，根据涡粘性公式$\nu_t = C_\mu k^2/\varepsilon$，将导致$\nu_t  0$。负的涡粘性系数意味着[动量扩散](@entry_id:157895)变成了**反[扩散](@entry_id:141445)**，即模型会放大而非抹平速度梯度，这会使得[RANS方程](@entry_id:275032)在数学上变得不适定 (ill-posed)，并迅速导致数值解的发散（blow-up）。

因此，在CFD代码中必须采取特殊措施来保证$k$和$\varepsilon$的非负性。常用的方法包括在离散格式上使用具有[正定性](@entry_id:149643)的[迎风格式](@entry_id:756374)、对源项进行隐式线性化处理、或者求解变换后的变量（如求解$\ln(k)$和$\ln(\varepsilon)$的方程）来从根本上保证其正值。[@problem_id:3384766]

### 标准 $k-\varepsilon$ 模型的局限性

尽管$k-\varepsilon$模型在许多工程应用中取得了巨大成功，但它的一个根本性缺陷源于其核心——各向同性的Boussinesq涡粘性假设。

**各向同性假设**

该假设认为[雷诺应力张量](@entry_id:270803)的主轴方向与平均应变率张量的[主轴](@entry_id:172691)方向是重合的。这意味着，[湍流](@entry_id:151300)应力只响应于平均流的变形（拉伸或剪切），而不能独立地存在或发展出各向异性。具体来说，当不存在平均[应变率](@entry_id:154778)时，[Boussinesq假设](@entry_id:272519)预测[雷诺应力张量](@entry_id:270803)是各向同性的，即$-\overline{u'_i u'_j} = -\frac{2}{3}k\delta_{ij}$，这意味着所有方向的正应力都相等($\overline{u'^2} = \overline{v'^2} = \overline{w'^2}$)，且剪应力为零。

**无法预测各向异性驱动的流动**

这一局限性使得标准$k-\varepsilon$模型无法预测那些由[雷诺应力](@entry_id:263788)各向异性驱动的流动现象。一个典型的例子是**非圆形[直管](@entry_id:151308)道中的[二次流](@entry_id:754609)**。例如，在流经直的正方形[截面](@entry_id:154995)管道的[充分发展湍流](@entry_id:182734)中，实验观察到在[横截面](@entry_id:154995)上存在着从角部流向中心、再沿壁面中分线流回角部的四个对称的二次涡胞。这种[二次流](@entry_id:754609)的驱动力来自于[横截面](@entry_id:154995)内法向[雷诺应力](@entry_id:263788)的差异（即$\overline{v'^2} \neq \overline{w'^2}$）。

然而，对于这种流动，平均流在[横截面](@entry_id:154995)内是没有速度的（$V=W=0$），因此也没有[横截面](@entry_id:154995)内的平均[应变率](@entry_id:154778)。根据[Boussinesq假设](@entry_id:272519)，模型预测$\overline{v'^2} = \overline{w'^2}$且$\overline{v'w'}=0$，因此无法产生驱动[二次流](@entry_id:754609)的力。这是模型结构性的缺陷，无论网格多么精细都无法克服。

为了捕捉这类现象，需要更高级的[湍流模型](@entry_id:190404)，如**[代数应力模型](@entry_id:746353)(ASM)** 或 **[雷诺应力模型](@entry_id:754343)(RSM)**。这些模型放弃了涡粘性假设，转而直接为每一个雷诺应力分量$\overline{u'_i u'_j}$求解一个[输运方程](@entry_id:756133)（或其代数简化形式）。通过包含对压力-应变相关项的复杂建模，这些模型能够正确地描述由平均剪切产生的[雷诺应力](@entry_id:263788)各向异性，并能再现由这种各向异性驱动的[二次流](@entry_id:754609)等[复杂流动](@entry_id:747569)现象。[@problem_id:3384755]