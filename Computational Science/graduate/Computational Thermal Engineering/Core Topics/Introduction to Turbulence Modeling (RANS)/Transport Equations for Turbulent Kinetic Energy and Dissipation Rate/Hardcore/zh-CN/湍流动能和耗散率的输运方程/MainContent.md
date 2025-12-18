## 引言
在[计算流体动力学](@entry_id:142614)领域，精确预测[湍流](@entry_id:151300)行为是工程设计与科学研究的核心挑战。直接解析所有尺度的[湍流](@entry_id:151300)脉动计算成本过高，因此[雷诺平均纳维-斯托克斯 (RANS)](@entry_id:185095) 方法成为主流。然而，RANS方法引入了未知的雷诺应力项，导致了著名的“[湍流](@entry_id:151300)闭合问题”。本文聚焦于解决该问题的最流行方法之一——$k$-$\varepsilon$[两方程模型](@entry_id:271436)，旨在为读者提供一个关于[湍动能](@entry_id:262712)和耗散率[输运方程](@entry_id:174281)的全面理解。

本文将分为三个部分，系统地引导读者掌握这一关键的[湍流模型](@entry_id:190404)。在“原理与机制”一章中，我们将深入探讨模型背后的物理基础，从[雷诺分解](@entry_id:267756)出发，定义[湍动能](@entry_id:262712) (k) 与耗散率 (ε)，并推导它们的[输运方程](@entry_id:174281)，阐明其中的Boussinesq假说等核心建模思想。接下来，在“应用与跨学科联系”一章中，我们将展示该模型如何[超越理论](@entry_id:203777)，应用于从航空航天到地球物理等多个领域的复杂流动问题，并讨论其改进形式。最后，通过“动手实践”部分，读者将有机会通过具体问题来巩固和应用所学知识，将理论与计算实践紧密结合。

## 原理与机制

在[湍流](@entry_id:151300)的计算建模中，我们的目标是预测平均流动特性，而无需解析所有时空尺度上的混沌运动。[雷诺平均纳维-斯托克斯 (RANS)](@entry_id:185095) 方法是实现这一目标的核心。本章深入探讨了最广泛使用的 RANS 闭合方法之一——$k$-$\varepsilon$ 模型——背后的基本原理和机制。我们将从定义[湍流](@entry_id:151300)的关键量开始，构建它们的[输运方程](@entry_id:174281)，阐明建模假设，并最终探讨这些模型的固有局限性。

### [湍流](@entry_id:151300)的基本量化

为了分析[湍流](@entry_id:151300)，我们首先需要一种方法来[分离流](@entry_id:754694)动的平均行为和随机波动。**[雷诺分解](@entry_id:267756) (Reynolds decomposition)** 提供了这种方法，它将[瞬时速度](@entry_id:167797)场 $u_i$ 分解为[时间平均](@entry_id:267915)（或系综平均）部分 $\bar{u}_i$ 和波动部分 $u'_i$：

$u_i = \bar{u}_i + u'_i$

根据[平均算子](@entry_id:746605) $\overline{(\cdot)}$ 的定义，波动部分的平均值必须为零，即 $\overline{u'_i} = 0$。这一简单的分解是整个 RANS 框架的基石。基于此，我们可以定义两个核心的[湍流](@entry_id:151300)标度量，它们是大多数现代湍流模型的核心。

#### [湍动能](@entry_id:262712)

第一个，也是最直观的量是**[湍动能](@entry_id:262712) (turbulent kinetic energy)**，符号为 $k$。它被定义为单位质量流体由于速度波动而具有的平均动能。数学上，它是：

$k = \frac{1}{2} \overline{u'_i u'_i} = \frac{1}{2} (\overline{u'_1 u'_1} + \overline{u'_2 u'_2} + \overline{u'_3 u'_3})$

其中，我们使用了爱因斯坦求和约定。湍动能 $k$ 的量纲是 $L^2 T^{-2}$（能量/质量），它直接衡量了[湍流](@entry_id:151300)脉动的强度。$k$ 值高的区域表示强烈的[湍流](@entry_id:151300)，而 $k$ 值低的区域表示弱[湍流](@entry_id:151300)或层流。

#### [湍流耗散率](@entry_id:756234)

第二个关键量是**[湍流耗散率](@entry_id:756234) (turbulent dissipation rate)**，符号为 $\varepsilon$。它描述了[湍动能](@entry_id:262712)由于粘性效应被不可逆地转化为内能（热）的速率。能量从最大的涡（尺度与主流相当）通过一系列越来越小的涡传递下来，这个过程被称为**能量级串 (energy cascade)**。最终，在最小的尺度（即**柯尔莫哥洛夫微尺度 (Kolmogorov microscales)**）上，粘性力变得足够强，能够将[动能耗散](@entry_id:751026)掉。

为了精确定义 $\varepsilon$，我们引入**脉动[应变率张量](@entry_id:266108) (fluctuating rate-of-strain tensor)**, $S'_{ij}$，其定义为脉动速度梯度[张量的对称部分](@entry_id:182434)：

$S'_{ij} = \frac{1}{2} \left( \frac{\partial u'_i}{\partial x_j} + \frac{\partial u'_j}{\partial x_i} \right)$

对于不可压缩流，脉动速度场也是无散的（即 $\partial u'_i / \partial x_i = 0$），这意味着脉动[应变率张量](@entry_id:266108)的迹为零 ($S'_{ii} = 0$)。[耗散率](@entry_id:748577) $\varepsilon$ 是由脉动[应变率张量](@entry_id:266108)通过[粘性力](@entry_id:263294)做功所产生的，其精确定义为：

$\varepsilon = 2\nu \overline{S'_{ij}S'_{ij}}$

其中 $\nu$ 是流体的[运动粘度](@entry_id:275614)。由于该表达式包含平方项的平均值，$\varepsilon$ 本质上是一个非负量。它的量纲是 $L^2 T^{-3}$，即单位质量的能量耗散速率。因此，$\varepsilon$ 不仅决定了能量级串的终点，还与[湍流](@entry_id:151300)中最小涡的尺度和时间尺度直接相关。

### [雷诺应力](@entry_id:263788)与闭合问题

将[雷诺分解](@entry_id:267756)代入[纳维-斯托克斯方程](@entry_id:142275)并进行平均，我们得到[雷诺平均纳维-斯托克斯 (RANS)](@entry_id:185095) 方程。对于不可压缩的牛顿流体，其平均[动量方程](@entry_id:197225)为：

$\rho\left(\frac{\partial \bar{u}_i}{\partial t} + \bar{u}_j \frac{\partial \bar{u}_i}{\partial x_j}\right) = -\frac{\partial \bar{p}}{\partial x_i} + \frac{\partial}{\partial x_j} \left( \mu \frac{\partial \bar{u}_i}{\partial x_j} - \rho\overline{u'_i u'_j} \right)$

这个方程看起来很像原始的[纳维-斯托克斯方程](@entry_id:142275)，但有一个关键的新增项：$-\rho\overline{u'_i u'_j}$。这个张量被称为**[雷诺应力张量](@entry_id:270803) (Reynolds stress tensor)**。它源于[非线性](@entry_id:637147)的对流项，代表了[湍流](@entry_id:151300)脉动对平均动量输运的贡献。它在方程中起着与[粘性应力](@entry_id:261328)类似的作用，但它不是流体的属性，而是流动的属性。

这个新项引入了新的未知数 ($\overline{u'_i u'_j}$ 的六个独立分量)，使得方程组不封闭。为了求解 RANS 方程，我们必须建立一个模型，将[雷诺应力](@entry_id:263788)与已知的平均流场量（如平均速度梯度）联系起来。这就是所谓的**[湍流](@entry_id:151300)闭合问题 (turbulence closure problem)**。

### Boussinesq 假说与涡粘模型

解决闭合问题最流行的方法之一是 **Boussinesq 假说 (Boussinesq hypothesis)**。这个假说类比了[牛顿流体](@entry_id:263796)中粘性[应力与[应变](@entry_id:263123)率](@entry_id:154778)之间的线性关系，假设雷诺应力张量的各向异性部分与平均应变率张量 $S_{ij}$ 成正比：

$S_{ij} = \frac{1}{2}\left(\frac{\partial \bar{u}_i}{\partial x_j} + \frac{\partial \bar{u}_j}{\partial x_i}\right)$

具体来说，模型将雷诺应力张量 $\overline{u'_i u'_j}$ 分解为其各向同性部分和偏量（各向异性）部分。其迹为 $\overline{u'_k u'_k} = 2k$。因此，各向同性部分为 $\frac{2}{3}k\delta_{ij}$，其中 $\delta_{ij}$ 是克罗内克符号。Boussinesq 假说正是对偏量部分的建模：

$-\rho \overline{u'_i u'_j} = \mu_t \left(\frac{\partial \bar{u}_i}{\partial x_j} + \frac{\partial \bar{u}_j}{\partial x_i}\right) - \frac{2}{3}\rho k \delta_{ij} = 2\mu_t S_{ij} - \frac{2}{3}\rho k \delta_{ij}$

这里的 $\mu_t$ 是一个比例常数，被称为**[湍流](@entry_id:151300)涡粘度 (turbulent eddy viscosity)**，它是一个标量，与分子粘度 $\mu$ 具有相同的量纲。与 $\mu$ 是流体固有属性不同，$\mu_t$ 是流动的局部属性，反映了[湍流混合](@entry_id:202591)的强度。对于不可压缩流，各向同性项的散度 $-\frac{\partial}{\partial x_j}(\frac{2}{3}\rho k \delta_{ij}) = -\frac{\partial}{\partial x_i}(\frac{2}{3}\rho k)$ 是一个[标量场的梯度](@entry_id:270765)，因此可以与平均压力梯度项合并，定义一个修正压力或“[湍流](@entry_id:151300)压力” $P^\star = \bar{p} + \frac{2}{3}\rho k$。

这个模型的一个重要物理内涵是关于湍动能的产生。湍动能的**产生项 (production term)**, $P_k$，精确地定义为[雷诺应力](@entry_id:263788)对平均[应变率](@entry_id:154778)做的功：$P_k = -\overline{u'_i u'_j} \frac{\partial \bar{u}_i}{\partial x_j}$。由于[雷诺应力张量](@entry_id:270803)是对称的，而[平均速度](@entry_id:267649)梯度可以分解为对称的[应变率张量](@entry_id:266108) $S_{ij}$ 和反对称的旋转率张量 $\Omega_{ij}$，我们发现产生项仅取决于应变：

$P_k = -\overline{u'_i u'_j} (S_{ij} + \Omega_{ij}) = -\overline{u'_i u'_j} S_{ij}$

因为[对称张量与反对称张量](@entry_id:194720)的缩并恒为零。这意味着平均流的刚性旋转不直接产生[湍动能](@entry_id:262712)。将 Boussinesq 假说代入这个表达式，并利用不可压缩性条件（$S_{ii} = 0$），我们得到了产生项的模型表达式：

$P_k = \left(2\nu_t S_{ij} - \frac{2}{3}k\delta_{ij}\right) S_{ij} = 2\nu_t S_{ij}S_{ij} - \frac{2}{3}k S_{ii} = 2\nu_t S_{ij}S_{ij}$

其中 $\nu_t = \mu_t / \rho$ 是[湍流](@entry_id:151300)运动粘度。由于 $\nu_t$ 必须为正以确保能量从平均流向[湍流](@entry_id:151300)传递（物理现实性要求 $P_k \ge 0$），且 $S_{ij}S_{ij}$ 是一个非负的平方和，该模型保证了 $P_k \ge 0$。

### 为何需要[输运方程](@entry_id:174281)：超越代数模型

Boussinesq 假说将闭合问题简化为确定标量涡粘度 $\nu_t$ 的问题。最简单的方法是使用**代数模型 (algebraic models)**，例如普朗特的混合长度模型，它假设 $\nu_t$ 只与当地的平均速度梯度和到壁面的距离有关。然而，这类模型基于一个强假设：**[局部平衡](@entry_id:156295) (local equilibrium)**，即湍动能的产生与耗散在每一点都近似相等 ($P_k \approx \varepsilon$)。

在许多工程应用中，如流经曲面的边界层、存在突变（如压力梯度变化或热通量阶跃）的流动中，这个假设是不成立的。在这些**非平衡流 (non-equilibrium flows)** 中，[湍流](@entry_id:151300)的“历史”效应变得至关重要。一个流体微团所携带的[湍流](@entry_id:151300)特性（如 $k$ 和 $\varepsilon$）取决于其上游的经历。[湍流](@entry_id:151300)的对流和[扩散输运](@entry_id:150792)项在 $k$ 的总收支中变得不可忽略。代数模型无法捕捉这种输运和历史效应，因为它们是纯局部的。

为了克服这一缺陷，我们需要一种能够动态描述[湍流](@entry_id:151300)尺度演化的方法。这就是**[两方程模型](@entry_id:271436) (two-equation models)** 的切入点。通过求解 $k$ 和另一个尺度决定量（如 $\varepsilon$）的[输运方程](@entry_id:174281)，模型可以计及[湍流](@entry_id:151300)的对流、扩散、产生和耗散，从而允许 $P_k \neq \varepsilon$，并捕捉非平衡和[非局部效应](@entry_id:198046)。

通过[量纲分析](@entry_id:140259)，我们可以将涡粘度 $\nu_t$ 与 $k$ 和 $\varepsilon$ 联系起来。$k$ 的量纲是 $L^2 T^{-2}$，$\varepsilon$ 的量纲是 $L^2 T^{-3}$。为了得到 $\nu_t$ 的量纲 $L^2 T^{-1}$，唯一不含其它常数的组合是：

$\nu_t \propto \frac{k^2}{\varepsilon}$

因此，标准的 $k$-$\varepsilon$ 模型采用以下形式：

$\nu_t = C_\mu \frac{k^2}{\varepsilon}$

其中 $C_\mu$ 是一个通过实验校准的无量纲常数。这个关系式将涡粘度的计算与两个待解的[湍流](@entry_id:151300)输运变量 $k$ 和 $\varepsilon$ 联系起来，从而使整个模型系统得以封闭。

### 建模的[输运方程](@entry_id:174281)

现在我们来构建 $k$ 和 $\varepsilon$ 的模型化[输运方程](@entry_id:174281)。一个通用标量 $\phi$ 的[输运方程](@entry_id:174281)可以写作：

$\frac{D\phi}{Dt} = \text{扩散} + \text{源} - \text{汇}$

其中 $\frac{D\phi}{Dt} = \frac{\partial\phi}{\partial t} + \bar{u}_j \frac{\partial\phi}{\partial x_j}$ 是物质导数，代表了随平均流运动的 $\phi$ 的变化率，这确保了模型的**伽利略[不变性](@entry_id:140168) (Galilean invariance)**。

#### 湍动能 ($k$) 方程

$k$ 的精确[输运方程](@entry_id:174281)可以从[纳维-斯托克斯方程](@entry_id:142275)直接导出。它包含以下物理过程：
- **产生 ($P_k$)**: 如前所述，通过[雷诺应力](@entry_id:263788)与平均[应变率](@entry_id:154778)的相互作用，从平均流中提取能量。
- **耗散 ($-\varepsilon$)**: 通过粘性作用将湍动能转化为内能，这是一个汇项。
- **[湍流](@entry_id:151300)输运**: 由速度和压力脉动的更高阶相关项（如 $\overline{u'_j p'}$ 和 $\overline{u'_i u'_i u'_j}$）引起的空间重新分布。这是一个散度项，在全域积分时为零，仅重新分配能量。
- **分子扩散**: 由分子粘性引起的 $k$ 的扩散。

在标准的 $k$-$\varepsilon$ 模型中，输运项采用**[梯度扩散假说](@entry_id:1125716) (gradient-diffusion hypothesis)** 进行建模，假设[湍流](@entry_id:151300)的输运通量与 $k$ 的梯度成正比。这与分子扩散项合并，得到最终的模型化 $k$ 方程：

$ \frac{D k}{D t} = \frac{\partial}{\partial x_j} \left[ \left( \nu + \frac{\nu_t}{\sigma_k} \right) \frac{\partial k}{\partial x_j} \right] + P_k - \varepsilon $

其中 $P_k = 2\nu_t S_{ij}S_{ij}$ 是已建模的产生项，而 $\sigma_k$ 是 $k$ 的**[湍流普朗特数](@entry_id:153739) (turbulent Prandtl number)**，是一个无量纲常数，用于调节[湍流扩散](@entry_id:1133505)的相对强度。

#### [耗散率](@entry_id:748577) ($\varepsilon$) 方程

$\varepsilon$ 的精确[输运方程](@entry_id:174281)极其复杂，包含许多难以建模的高阶相关项。因此，$\varepsilon$ 的模型方程更多地是基于物理直觉、[量纲分析](@entry_id:140259)和与 $k$ 方程的类比构建的。其源项和汇项的形式可以通过[标度分析](@entry_id:153681)来论证：

- **源项 (产生)**: $\varepsilon$ 的产生与 $k$ 的产生密切相关，因为是相同的平均应变过程在拉伸涡旋。然而，量纲分析表明，仅用 $P_k$ (量纲 $L^2 T^{-3}$) 作为源项是不够的，因为它与 $\frac{D\varepsilon}{Dt}$ (量纲 $L^2 T^{-4}$) 的量纲不匹配。为了匹配量纲，我们需要乘以一个具有频率量纲 ($T^{-1}$) 的量。[湍流](@entry_id:151300)大涡的特征频率是 $\varepsilon/k$。因此，源项被建模为与 $\frac{\varepsilon}{k}P_k$ 成正比。
- **汇项 (耗散)**: $\varepsilon$ 本身的耗散被认为发生在[湍流](@entry_id:151300)[特征时间尺度](@entry_id:276738) $\tau \sim k/\varepsilon$上。因此，其耗散率应与 $\varepsilon/\tau$ 成正比，即 $\varepsilon / (k/\varepsilon) = \varepsilon^2/k$。这个组合的量纲也恰好是 $L^2 T^{-4}$。

结合[梯度扩散假说](@entry_id:1125716)用于输运项，标准的 $\varepsilon$ 模型方程为：

$ \frac{D \varepsilon}{D t} = \frac{\partial}{\partial x_j} \left[ \left( \nu + \frac{\nu_t}{\sigma_\varepsilon} \right) \frac{\partial \varepsilon}{\partial x_j} \right] + C_{\varepsilon 1} \frac{\varepsilon}{k} P_k - C_{\varepsilon 2} \frac{\varepsilon^2}{k} $

其中 $C_{\varepsilon 1}$ 和 $C_{\varepsilon 2}$ 是两个主要的模型常数，$\sigma_\varepsilon$ 是 $\varepsilon$ 的湍流普朗特数。

### 模型常数的校准与模型的局限性

#### 模型常数的来源

$k$-$\varepsilon$ 模型中的五个标准常数——$C_\mu, C_{\varepsilon 1}, C_{\varepsilon 2}, \sigma_k, \sigma_\varepsilon$——并非从第一性原理推导得出，而是通过与一系列规范的、简单的[湍流](@entry_id:151300)实验数据进行对比来校准的。这种方法确保了模型在这些基础流动中具有合理的预测能力。

- **$C_\mu \approx 0.09$**: 这个常数主要通过考察[壁面束缚流](@entry_id:153603)（如[管道流](@entry_id:189531)、[平板边界层](@entry_id:749449)）的[对数律区](@entry_id:264342)来确定。在该区域，假定产生与耗散平衡 ($P_k \approx \varepsilon$)，可以推导出 $C_\mu$ 与[雷诺切应力](@entry_id:148861)和湍动能之间的关系，实验数据表明 $C_\mu \approx 0.09$。
- **$C_{\varepsilon 2} \approx 1.92$**: 这个常数主要通过匹配均匀[各向同性湍流](@entry_id:199323)的衰减率来校准。在没有平均剪切的情况下（$P_k=0$），$k$ 和 $\varepsilon$ 的方程可以求解，其衰减指数与 $C_{\varepsilon 2}$ 直接相关。实验（如风洞中的格栅[湍流](@entry_id:151300)）数据约束了其取值。
- **$C_{\varepsilon 1} \approx 1.44$**: 在 $C_{\varepsilon 2}$ 确定后，$C_{\varepsilon 1}$ 通过匹配均匀[剪切流](@entry_id:266817)的实验数据来确定，确保模型能正确预测湍动能在此类流动中的增长。
- **$\sigma_k \approx 1.0$ 和 $\sigma_\varepsilon \approx 1.3$**: 这两个扩散相关的常数主要通[过拟合](@entry_id:139093)[自由剪切流](@entry_id:271682)（如射流、尾流、[混合层](@entry_id:926526)）的扩展率和中心线衰减率来调整。它们控制着[湍流](@entry_id:151300)能量和耗散在空间上的输运速率。

#### Boussinesq 假说的根本局限性

尽管 $k$-$\varepsilon$ 模型非常成功，但其核心——Boussinesq 假说——存在根本性的局限性。该假说假设[雷诺应力张量](@entry_id:270803)与平均[应变率张量](@entry_id:266108)的**主轴是对齐的**。然而，在许多复杂的流动中，这个假设是错误的。

在存在**强[流线](@entry_id:266815)曲率**、**系统旋转**或**流动分离**的区域，[湍流](@entry_id:151300)涡的输运历史和各向异性效应变得非常显著。例如，在弯曲的剪切流中，[离心力](@entry_id:173726)会抑制或增强[湍流](@entry_id:151300)，导致雷诺应力张量与平均[应变率张量](@entry_id:266108)之间出现显著的“错位”。Boussinesq 假说无法捕捉这种物理效应，因为它将应力张量与[应变率张量](@entry_id:266108)强制对齐，并通过一个标量涡粘度进行缩放。

这种错位直接导致了对**湍动能产生项 $P_k$ 的错误预测**。真实的产生项 $P_k = -\overline{u'_i u'_j} S_{ij}$ 依赖于[应力与应变](@entry_id:137374)张量的真实相对方向，而模型化的产生项 $P_k = 2\nu_t S_{ij}S_{ij}$ 仅依赖于应变率的大小。在旋转或弯曲流动中，这可能导致对 $P_k$ 的严重高估或低估，从而影响整个[湍流](@entry_id:151300)场的预测。例如，模型无法区分稳定（凸面）和不稳定（凹面）曲率对[湍流](@entry_id:151300)的不同影响。

因此，尽管[两方程模型](@entry_id:271436)在捕捉[湍流](@entry_id:151300)的非平衡输运方面比代数模型有了巨大进步，但它们仍然受到涡粘模型自身的各向同性假设的限制。要克服这些限制，就需要更高级的模型，例如直接求解[雷诺应力张量](@entry_id:270803)[输运方程](@entry_id:174281)的[雷诺应力模型](@entry_id:198103) (Reynolds Stress Models, RSM)。