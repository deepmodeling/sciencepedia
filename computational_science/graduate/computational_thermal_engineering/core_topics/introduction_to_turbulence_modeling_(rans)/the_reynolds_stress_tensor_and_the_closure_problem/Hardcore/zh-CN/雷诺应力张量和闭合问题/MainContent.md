## 引言
在众多科学与工程领域，准确预测[湍流](@entry_id:151300)现象是设计与研究的基石。然而，由于[湍流](@entry_id:151300)固有的多尺度和[非线性](@entry_id:637147)特性，直接从第一性原理求解瞬时流场在计算上往往是不可行的。雷诺平均Navier-Stokes (RANS) 方法提供了一个高效的替代方案，它通过对流动方程进行时间平均，专注于求解工程上更关心的平均流动特性。然而，这一平均过程也引入了一个核心的理论难题：未知的[雷诺应力张量](@entry_id:270803)及其带来的[湍流封闭问题](@entry_id:268973)。

本文旨在系统性地阐述雷诺应力张量的起源、物理意义以及解决相关封闭问题的关键建模策略。文章将填补从基础理论到高级应用之间的知识鸿沟，为读者构建一个连贯的理解框架。通过学习本文，您将深入了解[湍流建模](@entry_id:151192)的核心思想，并掌握其在不同物理场景下的应用与演化。

文章将分为三个核心章节展开。在“原理与机制”部分，我们将从[雷诺分解](@entry_id:267756)出发，推导[RANS方程](@entry_id:275032)，揭示雷诺应力张量的诞生和封闭问题的本质。您将学习到最经典的涡粘模型（如[k-ε模型](@entry_id:751073)）及其背后的[Boussinesq假设](@entry_id:272519)，并理解其固有的局限性，进而转向更高级的[雷诺应力模型](@entry_id:198103)（RSM）。随后的“应用与跨学科联系”章节将展示这些理论在实际工程问题（如壁面流、热交换）和前沿科学领域（如地球物理、天体物理）中的广泛应用，探讨[浮力](@entry_id:154088)、[可压缩性](@entry_id:144559)等复杂效应对湍流模型提出的新挑战。最后，“动手实践”部分将提供具体的计算练习，帮助您将抽象的理论概念转化为可操作的物理量计算，加深对[湍动能](@entry_id:262712)产生、[湍流各向异性](@entry_id:756224)以及模型可实现性等关键概念的理解。

## 原理与机制

在对[湍流](@entry_id:151300)进行[数值模拟](@entry_id:146043)时，我们面临一个根本性的挑战：[湍流](@entry_id:151300)包含的尺度范围极广，从宏观的流动结构到微观的耗散涡，直接求解所有尺度的瞬时运动（即[直接数值模拟](@entry_id:149543)，DNS）在计算上是极其昂贵的，对于工程应用而言往往是不可行的。因此，我们需要发展一种系统性的方法，仅求解平均流动特性，同时将所有[湍流](@entry_id:151300)脉动的影响以某种方式模型化。[雷诺平均](@entry_id:754341)[Navier-Stokes](@entry_id:276387) (RANS) 方法正是这样一种框架，而理解其核心——雷诺应力张量及其封闭问题——是湍流建模的基石。

### [雷诺平均](@entry_id:754341)与[雷诺应力张量](@entry_id:270803)的起源

我们从描述不可压缩[牛顿流体](@entry_id:263796)运动的瞬时Navier-Stokes方程和连续性方程出发：
$$
\frac{\partial u_i}{\partial t} + u_j \frac{\partial u_i}{\partial x_j} = -\frac{1}{\rho} \frac{\partial p}{\partial x_i} + \nu \frac{\partial^2 u_i}{\partial x_j^2}
$$
$$
\frac{\partial u_i}{\partial x_i} = 0
$$
其中 $u_i$ 是[瞬时速度](@entry_id:167797)分量，$p$ 是瞬时压力，$\rho$ 是常数密度，$\nu$ 是[运动粘度](@entry_id:275614)。

为了分离出平均运动和脉动运动，我们引入**[雷诺分解](@entry_id:267756)** (Reynolds decomposition)。任何瞬时量 $\phi$ 都可以分解为其[时间平均](@entry_id:267915)值（或系综平均值）$\overline{\phi}$ 和脉动值 $\phi'$ 的和：
$$
u_i = U_i + u'_i \quad \text{以及} \quad p = P + p'
$$
这里，我们用 $U_i$ 和 $P$ 分别表示[平均速度](@entry_id:267649)和平均压力，即 $U_i = \overline{u_i}$ 和 $P = \overline{p}$。雷诺平均算子 $\overline{(\cdot)}$ 是一个[线性算子](@entry_id:149003)，它遵循一系列基本规则。根据其定义，脉动量的平均值为零 ：
$$
\overline{u'_i} = \overline{u_i - U_i} = \overline{u_i} - \overline{U_i} = U_i - U_i = 0
$$
同样地，$\overline{p'} = 0$。此外，[平均算子](@entry_id:746605)还满足其他重要性质，如与时空导数的可交换性（对于足够光滑的场）以及平均一个已平均量或常数不改变其值。一个关键的法则是，一个平均量与一个脉动量的乘积的平均值为零 ：
$$
\overline{U_i u'_j} = U_i \overline{u'_j} = 0
$$

将[雷诺分解](@entry_id:267756)代入瞬时[Navier-Stokes](@entry_id:276387)方程并对整个方程进行平均，我们得到**雷诺平均[Navier-Stokes](@entry_id:276387) (RANS) 方程**。在这个过程中，大部分项的平均都相对直接。例如，压力梯度项变为 $\overline{-\frac{1}{\rho} \frac{\partial p}{\partial x_i}} = -\frac{1}{\rho} \frac{\partial P}{\partial x_i}$。然而，[非线性](@entry_id:637147)的对流项 $\overline{u_j \frac{\partial u_i}{\partial x_j}}$ (或其等价的[保守形式](@entry_id:747710) $\overline{\frac{\partial (u_i u_j)}{\partial x_j}}$) 的处理则引出了一个核心的新项。让我们来展开它：
$$
\overline{u_i u_j} = \overline{(U_i + u'_i)(U_j + u'_j)} = \overline{U_i U_j + U_i u'_j + u'_i U_j + u'_i u'_j}
$$
利用[平均法](@entry_id:264400)则，上式简化为：
$$
\overline{u_i u_j} = U_i U_j + \overline{u'_i u'_j}
$$
因此，平均后的对流项变为 $\frac{\partial (U_i U_j)}{\partial x_j} + \frac{\partial \overline{u'_i u'_j}}{\partial x_j}$。将此结果代入，[RANS方程](@entry_id:275032)可写为：
$$
\frac{\partial U_i}{\partial t} + U_j \frac{\partial U_i}{\partial x_j} = -\frac{1}{\rho} \frac{\partial P}{\partial x_i} + \nu \frac{\partial^2 U_i}{\partial x_j^2} - \frac{\partial \overline{u'_i u'_j}}{\partial x_j}
$$
与原始的瞬时方程相比，[RANS方程](@entry_id:275032)的形式非常相似，但出现了一个新的项：$-\frac{\partial \overline{u'_i u'_j}}{\partial x_j}$。这个[二阶张量](@entry_id:199780) $\overline{u'_i u'_j}$ 被称为**运动学[雷诺应力张量](@entry_id:270803)**。将其乘以密度 $\rho$ 并移到方程右边，可以定义**[雷诺应力张量](@entry_id:270803)** $\tau^R_{ij} = -\rho \overline{u'_i u'_j}$。它在方程中扮演着与分子[粘性应力](@entry_id:261328) $\sigma_{ij}$ 类似的角色，代表了由速度脉动引起的动量输运 。值得注意的是，$\tau^R_{ij}$ 并非流体内部的真实应力，而是由于我们选择对[Navier-Stokes](@entry_id:276387)方程进行平均而产生的数学产物，它量化了[湍流](@entry_id:151300)[涡对](@entry_id:199153)平均流动的宏观影响。

这个新出现的雷诺应力张量是**封闭问题** (closure problem) 的核心。在三维空间中，[RANS方程](@entry_id:275032)组包含4个方程（3个[动量方程](@entry_id:197225)和1个[连续性方程](@entry_id:195013)），用以求解4个平均场变量（$U_1, U_2, U_3, P$）。然而，由于[雷诺应力张量](@entry_id:270803) $\overline{u'_i u'_j}$ 是对称的，它引入了6个新的独立未知分量（$\overline{u'_1 u'_1}, \overline{u'_2 u'_2}, \overline{u'_3 u'_3}, \overline{u'_1 u'_2}, \overline{u'_1 u'_3}, \overline{u'_2 u'_3}$）。这导致方程组中的未知量多于方程数，系统在数学上是不封闭的。为了求解[RANS方程](@entry_id:275032)，我们必须引入额外的关系式或模型，将未知的[雷诺应力](@entry_id:263788)与已知的平均流动量联系起来。这就是湍流模型的主要任务。

在寻找模型之前，我们必须认识到雷诺应力张量本身所具有的严格数学性质。首先，它显然是**对称的**：$\overline{u'_i u'_j} = \overline{u'_j u'_i}$。其次，它是一个**半[正定张量](@entry_id:204409)**。这意味着对于任意非[零向量](@entry_id:156189) $a_i$，二次型 $a_i a_j \overline{u'_i u'_j}$ 必须是非负的。这可以通过以下方式证明  ：
$$
a_i a_j \overline{u'_i u'_j} = \overline{(a_i u'_i)(a_j u'_j)} = \overline{(a_k u'_k)^2} \ge 0
$$
这个性质源于一个标量平方的平均值必然是非负的。[半正定性](@entry_id:147720)意味着[雷诺应力张量](@entry_id:270803)的所有特征值都必须是非负的。特别是，它的对角线元素 $\overline{u'_i u'_i}$（法向应力）代表了速度脉动的方差，必须是非负的。任何一个有效的[湍流模型](@entry_id:190404)都必须尊重这些基本的数学约束，即所谓的**[可实现性](@entry_id:193701)** (realizability) 约束。

### 涡粘模型与[Boussinesq假设](@entry_id:272519)

面对封闭问题的挑战，最直接和广泛使用的建模策略是**[Boussinesq假设](@entry_id:272519)**，由Joseph Boussinesq于1877年提出。该假设的核心思想是，[湍流](@entry_id:151300)对平均流动的动量输运效应，可以类比于分子粘性对动量的输运。正如分子粘性[应力与[应变](@entry_id:263123)率张量](@entry_id:266108)成线性关系一样，我们可以假设[雷诺应力张量](@entry_id:270803)的非各向同性部分也与平均[应变率张量](@entry_id:266108) $S_{ij}$ 成线性关系 。

平均应变率张量定义为：
$$
S_{ij} = \frac{1}{2} \left( \frac{\partial U_i}{\partial x_j} + \frac{\partial U_j}{\partial x_i} \right)
$$
首先，我们将[雷诺应力张量](@entry_id:270803)分解为其各向同性[部分和](@entry_id:162077)偏（非各向同性）部分。一个[二阶张量](@entry_id:199780)的各向同性部分与其迹 (trace) 成正比。雷诺应力张量 $\overline{u'_i u'_j}$ 的迹是：
$$
\overline{u'_k u'_k} = \overline{u'_1 u'_1 + u'_2 u'_2 + u'_3 u'_3} = 2k
$$
其中，$k \equiv \frac{1}{2}\overline{u'_i u'_i}$ 是单位质量的**[湍动能](@entry_id:262712)** (Turbulent Kinetic Energy, TKE)。因此，各向同性部分为 $\frac{1}{3}(2k)\delta_{ij}$。

[Boussinesq假设](@entry_id:272519)正是对[偏应力](@entry_id:163323)部分进行建模，令其与平均应变率张量成正比：
$$
\overline{u'_i u'_j} - \frac{2}{3}k\delta_{ij} = -2\nu_t S_{ij}
$$
其中，$\nu_t$ 是一个标量，称为**[湍流](@entry_id:151300)涡粘度** (turbulent eddy viscosity)，它不是流体的物理属性，而是[湍流](@entry_id:151300)本身的特性。负号和因子2是约定俗成的，以确保当涡粘度 $\nu_t$ 为正时，[湍流](@entry_id:151300)能够从平均流中提取能量（即湍动能的产生项为正）。整理上式，我们得到[Boussinesq假设](@entry_id:272519)的完整形式：
$$
\overline{u'_i u'_j} = -2\nu_t S_{ij} + \frac{2}{3}k\delta_{ij}
$$
或者用[雷诺应力](@entry_id:263788) $\tau^R_{ij} = -\rho \overline{u'_i u'_j}$ 表示：
$$
\tau^R_{ij} = 2\mu_t S_{ij} - \frac{2}{3}\rho k\delta_{ij}
$$
其中 $\mu_t = \rho \nu_t$ 是动力涡粘度。

这个模型成功地将6个未知的雷诺应力分量与平均速度梯度关联起来，但代价是引入了新的未知量：涡粘度 $\nu_t$（或 TKE $k$ 和其他尺度量）。为了确定 $\nu_t$，我们需要所谓的**[两方程模型](@entry_id:271436)**，其中最著名的就是**标准 $k-\epsilon$ 模型** 。

$k-\epsilon$ 模型通过求解两个独立的[输运方程](@entry_id:174281)来确定[湍动能](@entry_id:262712) $k$ 和其[耗散率](@entry_id:748577) $\epsilon$。$\epsilon$ 定义为 $\epsilon \equiv \nu \overline{\frac{\partial u'_i}{\partial x_j}\frac{\partial u'_i}{\partial x_j}}$，它代表了湍动能通过粘性作用转化为内能的速率。通过量纲分析，[湍流](@entry_id:151300)速度尺度可近似为 $k^{1/2}$，长度尺度可近似为 $k^{3/2}/\epsilon$。涡粘度具有（密度 $\times$ 速度 $\times$ 长度）的量纲，因此可以建模为：
$$
\mu_t = \rho C_\mu \frac{k^2}{\epsilon}
$$
其中 $C_\mu$ 是一个经验常数。

$k$ 和 $\epsilon$ 的[输运方程](@entry_id:174281)在形式上是相似的，都包含了瞬变、对流、扩散、产生和耗散（或毁灭）项：
$$
\frac{\partial (\rho k)}{\partial t} + \frac{\partial (\rho U_j k)}{\partial x_j} = \frac{\partial}{\partial x_j}\left[\left(\mu + \frac{\mu_t}{\sigma_k}\right)\frac{\partial k}{\partial x_j}\right] + P_k - \rho\epsilon
$$
$$
\frac{\partial (\rho \epsilon)}{\partial t} + \frac{\partial (\rho U_j \epsilon)}{\partial x_j} = \frac{\partial}{\partial x_j}\left[\left(\mu + \frac{\mu_t}{\sigma_\epsilon}\right)\frac{\partial \epsilon}{\partial x_j}\right] + C_{\epsilon 1}\frac{\epsilon}{k}P_k - C_{\epsilon 2}\rho\frac{\epsilon^2}{k}
$$
在这些方程中：
-   $P_k = -\rho\overline{u'_i u'_j} \frac{\partial U_i}{\partial x_j} \approx 2\mu_t S_{ij}S_{ij}$ 是湍动能的**产生项**，表示平均流通过应变作用对[湍流](@entry_id:151300)做的功。
-   $\rho\epsilon$ 是 $k$ 的**耗散项**。
-   $C_{\epsilon 1}\frac{\epsilon}{k}P_k$ 和 $-C_{\epsilon 2}\rho\frac{\epsilon^2}{k}$ 分别是 $\epsilon$ 方程中的**产生项**和**毁灭项**。
-   $\sigma_k$ 和 $\sigma_\epsilon$ 是**[湍流普朗特数](@entry_id:153739)**，用于对 $k$ 和 $\epsilon$ 的[湍流扩散](@entry_id:1133505)进行建模。
-   $C_\mu, C_{\epsilon 1}, C_{\epsilon 2}, \sigma_k, \sigma_\epsilon$ 是一组通过匹配[简单剪切流](@entry_id:1131665)和格栅[湍流](@entry_id:151300)衰减等典型流动实验数据而校准的**模型常数** 。

通过求解这两个额外的[输运方程](@entry_id:174281)，我们得到 $k$ 和 $\epsilon$ 的场，从而计算出涡粘度 $\nu_t$，最终封闭[RANS方程](@entry_id:275032)。

### 涡粘模型的局限性

尽管[Boussinesq假设](@entry_id:272519)和基于它的 $k-\epsilon$ 模型在许多工程应用中取得了巨大成功，但它们建立在一个根本性的简化之上，这个简化在某些[复杂流动](@entry_id:747569)中会导致严重的预测偏差。这个核心假设是：偏[雷诺应力张量](@entry_id:270803)与平均[应变率张量](@entry_id:266108)是**共轴**的 (co-axial)，即它们的主轴方向完全对齐 。

在许多流动中，这种共轴性假设并不成立。例如：
-   **旋转和[曲率流](@entry_id:921438)动**：在强旋转或流线弯曲的流动中，科里奥利力或离心力会显著改变[湍流](@entry_id:151300)结构，导致雷诺应力张量的主轴方向与平均应变率张量的主轴方向发生偏离。一个极端的例子是固定的固壁旋转流，其平均应变率为零 ($S_{ij}=0$)，但[湍流](@entry_id:151300)应力由于旋转效应而呈现非各向同性。Boussinesq模型在这种情况下会错误地预测出各向同性的应力状态，从而无法捕捉到旋转对[湍流](@entry_id:151300)输运的影响 。
-   **[二次流](@entry_id:754609)**：在非圆形管道（如方形管道）的[充分发展湍流](@entry_id:182734)中，实验观察到垂直于主流方向的微弱二次流动。这种[二次流](@entry_id:754609)是由雷诺[法向应力](@entry_id:260622)的非各向同性（例如 $\overline{u'_y u'_y} \neq \overline{u'_z u'_z}$）驱动的。然而，Boussinesq模型只能在存在平均应变率的情况下产生非各向同性应力。在一个纯轴向流动中，横向的[应变率](@entry_id:154778)为零，因此模型无法预测驱动二次流的法向应力差，从而完全错失了这种重要的物理现象 。

除了物理图像上的局限，[线性涡粘模型](@entry_id:751307)还可能违反前面提到的**[可实现性](@entry_id:193701)** (realizability) 约束。[可实现性](@entry_id:193701)要求模型预测的雷诺应力必须是物理上可能的，例如，法向应力 $\overline{u'_i u'_i}$ (i无求和) 必须非负。在一个简单的平面剪切流中（$\overline{U} = \Gamma y$），Boussinesq模型预测的[雷诺应力张量](@entry_id:270803)的特征值之一为 $\lambda = \frac{2}{3}k - \nu_t \Gamma$。当剪切率 $\Gamma$ 足够大时，这个特征值可能变为负值，这意味着模型预测出了一个负的[法向应力](@entry_id:260622)，这在物理上是荒谬的 。这表明，即便 $\nu_t \ge 0$，线性模型在强应变下也可能失效。

### 高级模型：[雷诺应力模型](@entry_id:198103)

为了克服涡粘模型的根本局限性，我们需要更先进的建模方法。一个自然的想法是，不再对雷诺应力本身进行建模，而是为其推导并求解精确的[输运方程](@entry_id:174281)。这种方法被称为**[二阶矩封闭](@entry_id:754596)** (Second-Moment Closure) 或**[雷诺应力模型](@entry_id:198103)** (Reynolds Stress Model, RSM)。

通过对[Navier-Stokes](@entry_id:276387)方程进行一系列繁复的数学操作，可以推导出雷诺应力分量 $\overline{u'_i u'_j}$ 的精确[输运方程](@entry_id:174281) ：
$$
\frac{D \overline{u'_i u'_j}}{D t} = \frac{\partial \overline{u'_i u'_j}}{\partial t} + U_k \frac{\partial \overline{u'_i u'_j}}{\partial x_k} = P_{ij} + \Pi_{ij} + D_{T,ij} - \epsilon_{ij}
$$
其中，方程右边的各项具有明确的物理意义：
-   **产生项** $P_{ij} = -\left(\overline{u'_i u'_k}\frac{\partial U_j}{\partial x_k} + \overline{u'_j u'_k}\frac{\partial U_i}{\partial x_k}\right)$：表示平均速度梯度通过与[雷诺应力](@entry_id:263788)相互作用，将能量从平均流转移到[湍流](@entry_id:151300)脉动中。这一项是精确的，不需要建模。
-   **耗散项** $\epsilon_{ij} = 2\nu \overline{\frac{\partial u'_i}{\partial x_k}\frac{\partial u'_j}{\partial x_k}}$：表示[粘性力](@entry_id:263294)将雷诺应力的脉动[能量耗散](@entry_id:147406)掉的速率。
-   **[湍流](@entry_id:151300)输运项** $D_{T,ij} = -\frac{\partial}{\partial x_k}\left(\overline{u'_i u'_j u'_k} + \frac{1}{\rho}(\overline{p'u'_i}\delta_{jk} + \overline{p'u'_j}\delta_{ik})\right)$：表示由速度和压力脉动引起的空间输运。
-   **压力-应变相关项** $\Pi_{ij} = \overline{\frac{p'}{\rho}\left(\frac{\partial u'_i}{\partial x_j} + \frac{\partial u'_j}{\partial x_i}\right)}$：这是最关键和最复杂的项之一。

与[RANS方程](@entry_id:275032)一样，这个精确的[输运方程](@entry_id:174281)同样是不封闭的。耗散张量 $\epsilon_{ij}$、[湍流](@entry_id:151300)输运项 $D_{T,ij}$ 以及压力-应变项 $\Pi_{ij}$ 都包含了未知的脉动量高阶相关，需要被模型化。

压力-应变项 $\Pi_{ij}$ 尤为重要。它的迹为零（$\Pi_{ii}=0$），意味着它本身不产生或毁灭总的湍动能，而是将能量在不同的法向应力分量之间进行**重新分配**，从而趋向于使[湍流](@entry_id:151300)变得更**各向同性**。对 $\Pi_{ij}$ 的建模是RSM成功的关键。一个经典的模型是将其分解为“慢”部分（仅依赖于[湍流](@entry_id:151300)自身状态）和“快”部分（对平均[应变率](@entry_id:154778)的快速响应）。

对于慢部分，**Rotta模型**提出了一个简单而物理意义明确的假设：压力-应变项的作用是使[湍流](@entry_id:151300)以与当前非各向同性程度成正比的速率“返回”到各向同性状态 。定义一个无量纲的非[各向同性张量](@entry_id:195105) $a_{ij} = \frac{\overline{u'_i u'_j}}{2k} - \frac{1}{3}\delta_{ij}$，它在各向同性时为零。Rotta模型为：
$$
\Pi^{(s)}_{ij} = -C_1 \epsilon a_{ij}
$$
其中 $C_1$ 是一个正常数。这个模型形式简单，满足对称、迹为零、量纲一致等所有基本约束，并正确地描述了[湍流](@entry_id:151300)内在的趋向各向同性的趋势。

RSM通过直接求解雷诺应力的[输运方程](@entry_id:174281)，原则上能够精确地捕捉到流线弯曲、旋转和[二次流](@entry_id:754609)等复杂流动现象，因为[应力张量](@entry_id:148973)不再被强制与[应变率张量](@entry_id:266108)对齐。然而，其代价是需要求解6个额外的[输运方程](@entry_id:174281)，且模型本身（特别是 $\Pi_{ij}$ 和 $\epsilon_{ij}$ 的模型）非常复杂，使得计算成本和[数值稳定性](@entry_id:175146)方面的挑战远大于涡粘模型。

### [湍流](@entry_id:151300)输运的推广

[雷诺平均](@entry_id:754341)和封闭问题的概念不仅适用于[动量输运](@entry_id:139628)，也同样适用于其他物理量的输运，如热量和物质浓度。

考虑温度场 $T$ 的输运。瞬时能量方程可以写为：
$$
\frac{\partial T}{\partial t} + u_j \frac{\partial T}{\partial x_j} = \frac{\partial}{\partial x_j}\left(\alpha_m \frac{\partial T}{\partial x_j}\right)
$$
其中 $\alpha_m = k_{th}/(\rho c_p)$ 是分子热扩散系数。对该方程进行[雷诺平均](@entry_id:754341)，同样会在对流项中产生一个新的未知相关项 ：
$$
\overline{u_j T} = U_j \overline{T} + \overline{u'_j T'}
$$
这个新项 $\overline{u'_j T'}$ 被称为**湍流热通量**。它代表了由[湍流](@entry_id:151300)涡的宏观运动所携带的额外热量输运。为了封闭平均能量方程，我们需要对 $\overline{u'_j T'}$ 进行建模。最简单的方法是再次使用梯度扩散假设，类比于傅里叶热传导定律：
$$
\overline{u'_j T'} = -\alpha_t \frac{\partial \overline{T}}{\partial x_j}
$$
这里，$\alpha_t$ 是**[湍流](@entry_id:151300)[热扩散](@entry_id:148740)系数**。为了将其与[动量输运](@entry_id:139628)模型联系起来，我们定义一个**[湍流普朗特数](@entry_id:153739)** $\mathrm{Pr}_t$：
$$
\mathrm{Pr}_t = \frac{\nu_t}{\alpha_t}
$$
$\mathrm{Pr}_t$ 通常是一个接近1的常数（例如，对于空气约为0.85）。一旦我们通过 $k-\epsilon$ 模型等方法得到了涡粘度 $\nu_t$，就可以通过 $\mathrm{Pr}_t$ 计算出 $\alpha_t$，从而封闭能量方程。在大多数[高雷诺数流](@entry_id:1126089)动中，[湍流](@entry_id:151300)输运（由 $\alpha_t$ 主导）远大于[分子输运](@entry_id:195239)（由 $\alpha_m$ 主导），即 $\alpha_t / \alpha_m \gg 1$ 。

最后，当处理**可压缩[湍流](@entry_id:151300)**时，由于密度 $\rho$ 也会脉动，传统的[雷诺平均](@entry_id:754341)会引入大量难以处理的密度-速度-压力相关项。为了简化方程，**[Favre平均](@entry_id:198824)** (或密度加权平均) 被引入 。对于任意量 $\phi$，其[Favre平均](@entry_id:198824) $\tilde{\phi}$ 定义为：
$$
\tilde{\phi} = \frac{\overline{\rho \phi}}{\overline{\rho}}
$$
相应的Favre脉动为 $\phi'' = \phi - \tilde{\phi}$。[Favre平均](@entry_id:198824)的一个关键性质是 $\overline{\rho \phi''} = 0$。

使用[Favre平均](@entry_id:198824)，可压缩[RANS方程](@entry_id:275032)在形式上变得与不可压缩方程非常相似。例如，[Favre平均](@entry_id:198824)后的连续性方程和[动量方程](@entry_id:197225)为：
$$
\frac{\partial \overline{\rho}}{\partial t} + \frac{\partial (\overline{\rho}\tilde{u}_j)}{\partial x_j} = 0
$$
$$
\frac{\partial (\overline{\rho}\tilde{u}_i)}{\partial t} + \frac{\partial (\overline{\rho}\tilde{u}_i \tilde{u}_j)}{\partial x_j} = -\frac{\partial \overline{p}}{\partial x_i} + \frac{\partial \overline{\tau}_{ij}}{\partial x_j} - \frac{\partial \overline{\rho u''_i u''_j}}{\partial x_j} + \overline{\rho} f_i
$$
对流项的平均只产生了一个新的未知项，即**[Favre平均](@entry_id:198824)雷诺应力张量** $\overline{\rho u''_i u''_j}$。封闭问题现在转移到了对这个张量的建模上，其方法和思路与不可压缩情况下的建模是平行的。[Favre平均](@entry_id:198824)通过将密度脉动的影响“吸收”到平均量的定义中，极大地简化了可压缩[湍流](@entry_id:151300)的建模框架。