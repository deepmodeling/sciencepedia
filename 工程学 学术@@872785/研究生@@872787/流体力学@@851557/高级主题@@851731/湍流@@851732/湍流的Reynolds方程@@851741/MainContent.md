## 引言
[湍流](@entry_id:151300)是自然界和工程领域中无处不在的现象，其高度的随机性和多尺度特性给精确预测带来了巨大挑战。[直接数值模拟](@entry_id:149543)（DNS）虽能精确求解[流体运动](@entry_id:182721)的完整方程，但其惊人的计算成本使其难以应用于实际工程问题。[雷诺平均](@entry_id:754341)[Navier-Stokes](@entry_id:276387)（RANS）方法作为一种平衡了计算精度与效率的折衷方案，已成为过去几十年来工业界和学术界分析[湍流](@entry_id:151300)问题的主流工具。它的核心在于将复杂的瞬时流场分解为易于处理的平均流场和需要建模的脉动效应，但这也引出了[湍流建模](@entry_id:151192)的根本性难题——封闭问题。

本文旨在系统性地剖析RANS框架。我们将引导读者深入理解这一强大工具的内在逻辑、优势与局限。
- 在“原理与机制”一章中，我们将从第一性原理出发，推导[雷诺平均](@entry_id:754341)方程，揭示雷诺应力的起源和封闭问题的本质。随后，我们将详细探讨两[类核](@entry_id:178267)心建模策略：应用广泛的涡粘模型（如[k-ε模型](@entry_id:751073)）和更为复杂的[雷诺应力模型](@entry_id:754343)（RSM），分析它们背后的物理假设。
- 在“应用与跨学科联系”一章中，我们将展示RANS思想如何超越传统[流体力学](@entry_id:136788)，成为解决航空航天、传热、地球物理乃至天体物理等领域复杂问题的通用框架。通过具体案例，读者将看到不同层级的模型如何应对不同的物理挑战。
- 最后，在“动手实践”部分，我们将通过一系列引导性问题，帮助读者将理论知识转化为解决实际问题的能力，深化对[湍流](@entry_id:151300)产生机制、模型局限性以及高级理论应用的理解。

通过本章的学习，读者将能够建立起对[湍流](@entry_id:151300)[雷诺平均](@entry_id:754341)方法的全面认识，为后续的研究和工程应用打下坚实的基础。

## 原理与机制

本章旨在系统性地阐述[湍流](@entry_id:151300)[雷诺平均](@entry_id:754341)(Reynolds-Averaged Navier-Stokes, RANS)方法的基本原理与核心机制。我们将从[雷诺平均](@entry_id:754341)方程的推导入手，揭示[湍流建模](@entry_id:151192)的核心挑战——封闭问题，然后深入探讨两类主要的封闭策略：涡粘模型和[雷诺应力模型](@entry_id:754343)。

### [雷诺平均](@entry_id:754341)[Navier-Stokes](@entry_id:276387) (RANS) 方程

[直接数值模拟](@entry_id:149543)(DNS)虽然能够精确求解完整的[Navier-Stokes方程](@entry_id:161487)，但其巨大的计算成本使得它在工程实践中仅限于低雷诺数的简单流动。为了以可行的计算资源来预测高雷诺数[湍流](@entry_id:151300)，我们需要[对流](@entry_id:141806)动的控制方程进行某种形式的简化。RANS方法是其中最成熟和广泛应用的途径。

#### [雷诺分解](@entry_id:267756)与时间平均

RANS方法的核心思想是将瞬时流动变量分解为一个时间平均[部分和](@entry_id:162077)一个脉动部分。以[速度场](@entry_id:271461)为例，[瞬时速度](@entry_id:167797) $u_i$ 可以表示为：
$$
u_i(\mathbf{x}, t) = \overline{u_i}(\mathbf{x}) + u_i'(\mathbf{x}, t)
$$
其中，$\overline{u_i}$ 是[时间平均](@entry_id:267915)速度，定义为在一个足够长的时间周期 $T$ 内的积分：
$$
\overline{u_i}(\mathbf{x}) = \frac{1}{T} \int_{t_0}^{t_0+T} u_i(\mathbf{x}, t) dt
$$
而 $u_i'$ 是围绕平均值的脉动速度。根据定义，脉动分量的时间平均为零，即 $\overline{u_i'} = 0$。压力 $p$ 和其他[标量场](@entry_id:151443)也可以进行类似的分解。

将这种分解代入控制[流体运动](@entry_id:182721)的[Navier-Stokes方程](@entry_id:161487)，并对整个方程进行时间平均，就可以得到描述平均流场演化的方程。对于不可压缩牛顿流体，连续性方程和[动量方程](@entry_id:197225)的平均过程相对直接。平均后的[连续性方程](@entry_id:195013)与瞬时形式相同，只是作用于[平均速度](@entry_id:267649)场：
$$
\frac{\partial \overline{u_i}}{\partial x_i} = 0
$$

#### 雷诺应力与封闭问题

[动量方程](@entry_id:197225)的平均化过程则引入了关键的复杂性。动量方程中的[非线性](@entry_id:637147)[对流](@entry_id:141806)项 $\rho u_j \frac{\partial u_i}{\partial x_j}$ 在平均化之后，会产生一个全新的项。让我们展开该项并取时间平均：
$$
\overline{\rho u_j \frac{\partial u_i}{\partial x_j}} = \overline{\rho (\overline{u_j} + u_j') \frac{\partial (\overline{u_i} + u_i')}{\partial x_j}}
$$
由于平均和脉动量的乘积的平均为零（例如 $\overline{\overline{u_j} u_i'} = 0$），上式展开后得到：
$$
\overline{\rho u_j \frac{\partial u_i}{\partial x_j}} = \rho \overline{u_j} \frac{\partial \overline{u_i}}{\partial x_j} + \rho \overline{u_j' \frac{\partial u_i'}{\partial x_j}}
$$
利用脉动[速度场](@entry_id:271461)的[连续性方程](@entry_id:195013) $\frac{\partial u_j'}{\partial x_j} = 0$，后一项可以写成 $\rho \frac{\partial}{\partial x_j} (\overline{u_i' u_j'})$。因此，经过[时间平均](@entry_id:267915)的动量方程（即[RANS方程](@entry_id:275032)）变为：
$$
\rho \left( \frac{\partial \overline{u_i}}{\partial t} + \overline{u_j} \frac{\partial \overline{u_i}}{\partial x_j} \right) = - \frac{\partial \overline{p}}{\partial x_i} + \frac{\partial}{\partial x_j} \left( \mu \left( \frac{\partial \overline{u_i}}{\partial x_j} + \frac{\partial \overline{u_j}}{\partial x_i} \right) - \rho \overline{u_i' u_j'} \right)
$$
与原始[Navier-Stokes方程](@entry_id:161487)相比，[RANS方程](@entry_id:275032)中出现了一个新的项：$-\rho \overline{u_i' u_j'}$。这个张量被称为**[雷诺应力张量](@entry_id:270803)**（Reynolds stress tensor），记为 $\tau_{ij}' = -\rho \overline{u_i' u_j'}$。它代表了由速度脉动引起的动量在空间中的净输运，其物理效应类似于一个额外的应力作用于平均流场。

雷诺应力的出现是RANS方法的核心，也带来了根本性的挑战。在三维流动中，我们有四个待求解的平均场量：三个[平均速度](@entry_id:267649)分量 $\overline{u_i}$ 和一个平均压力 $\overline{p}$。然而，我们只有四个方程：一个连续性方程和三个动量方程。问题在于，[雷诺应力张量](@entry_id:270803) $\overline{u_i' u_j'}$ 是一个对称张量，它引入了六个新的独立未知数（$\overline{u_1'^2}$, $\overline{u_2'^2}$, $\overline{u_3'^2}$, $\overline{u_1' u_2'}$, $\overline{u_1' u_3'}$, $\overline{u_2' u_3'}$）。这样，我们总共有10个未知数，但只有4个方程。这个“未知数多于方程”的困境被称为[湍流](@entry_id:151300)的**封闭问题**（closure problem）。为了求解[RANS方程](@entry_id:275032)，必须引入额外的方程或关系式来模拟雷诺应力，使其能够通过已知的平均流场量来表达。这项任务便是[湍流模型](@entry_id:190404)的核心目标 [@problem_id:1786561]。

#### [湍流](@entry_id:151300)[标量输运](@entry_id:150360)

封闭问题同样存在于[湍流](@entry_id:151300)中其他物理量的[输运过程](@entry_id:177992)。考虑一个[被动标量](@entry_id:191726)（例如，温度 $T$ 或污染物浓度）的输运，其瞬时[输运方程](@entry_id:756133)为：
$$
\frac{\partial T}{\partial t} + u_j \frac{\partial T}{\partial x_j} = \frac{\partial}{\partial x_j}\left( \alpha \frac{\partial T}{\partial x_j} \right)
$$
其中 $\alpha$ 是[分子扩散系数](@entry_id:752110)。同样应用[雷诺分解](@entry_id:267756) $T = \overline{T} + T'$ 并进行[时间平均](@entry_id:267915)，[对流](@entry_id:141806)项会产生：
$$
\overline{u_j \frac{\partial T}{\partial x_j}} = \overline{u_j} \frac{\partial \overline{T}}{\partial x_j} + \frac{\partial}{\partial x_j}(\overline{u_j' T'})
$$
因此，平均[标量输运](@entry_id:150360)方程为：
$$
\frac{\partial \overline{T}}{\partial t} + \overline{u_j} \frac{\partial \overline{T}}{\partial x_j} = \frac{\partial}{\partial x_j}\left( \alpha \frac{\partial \overline{T}}{\partial x_j} - \overline{u_j' T'} \right)
$$
这里出现了新的未知项 $\overline{u_j' T'}$，被称为**[湍流](@entry_id:151300)标量通量**（turbulent scalar flux），在传热学中特指为**[湍流热通量](@entry_id:151024)**（turbulent heat flux）。它表示由速度脉动和标量脉动的共同作用引起的额外输运。例如，在温度场中，[湍流热通量](@entry_id:151024)向量 $q_j^t = \rho c_p \overline{u_j' T'}$ 代表了湍流涡旋对热量的混合与输运效应。这进一步增加了未知量的数目，使得对这些[湍流](@entry_id:151300)通量项的建模成为求[解耦](@entry_id:637294)合流动与[标量输运](@entry_id:150360)问题的关键 [@problem_id:2535349]。

### [湍流](@entry_id:151300)封闭模型：涡粘模型

涡粘模型（Eddy Viscosity Models, EVM）是迄今为止应用最广泛的一类[湍流模型](@entry_id:190404)。其基本思想是，[湍流](@entry_id:151300)脉动对平均流的[动量输运](@entry_id:139628)效应（即雷诺应力）在形式上可以类比于分子运动对动量的输运（即[粘性应力](@entry_id:261328)）。

#### [Boussinesq假设](@entry_id:272519)

这一类比由 Joseph Boussinesq 在19世纪末首次提出，被称为**[Boussinesq假设](@entry_id:272519)**。该假设将[雷诺应力张量](@entry_id:270803)的各向异性部分与平均流的[应变率张量](@entry_id:266108) $S_{ij}$ 建立线性关系：
$$
-\rho \overline{u_i' u_j'} = \mu_t \left( \frac{\partial \overline{u_i}}{\partial x_j} + \frac{\partial \overline{u_j}}{\partial x_i} \right) - \frac{2}{3} \rho k \delta_{ij}
$$
其中，$\mu_t$ 是新引入的比例系数，被称为**湍流涡粘度**（turbulent or eddy viscosity），它不是流体的物理属性，而是[湍流](@entry_id:151300)状态本身的函数，通常在流场中是变化的。$\delta_{ij}$ 是克罗内克符号。方程右侧的第二项是为了保证在取迹（$i=j$）时等式两边的一致性。根据定义，[雷诺应力张量](@entry_id:270803)的迹为 $-\rho \overline{u_k' u_k'} = -2\rho k$，其中 $k = \frac{1}{2}\overline{u_i' u_i'}$ 是单位质量的**[湍动能](@entry_id:262712)**（Turbulent Kinetic Energy, TKE）。

[Boussinesq假设](@entry_id:272519)的重大意义在于，它将求解六个独立的雷诺应力分量的复杂问题，简化为求解一个[标量场](@entry_id:151443)——[涡粘度](@entry_id:155814) $\mu_t$（或运动[涡粘度](@entry_id:155814) $\nu_t = \mu_t / \rho$）的问题。一旦 $\nu_t$ 和 $k$ 确定，[雷诺应力](@entry_id:263788)即可由[平均速度](@entry_id:267649)梯度计算得出，从而使[RANS方程](@entry_id:275032)组得以封闭。

#### [两方程模型](@entry_id:271436)

接下来的问题是如何确定[涡粘度](@entry_id:155814) $\nu_t$。通过量纲分析可知，粘度具有 $[长度]^2 / [时间]$ 的量纲。在[湍流](@entry_id:151300)中，一个特征速度尺度 $v$ 和一个[特征长度尺度](@entry_id:266383) $l$ 可以组合成一个[涡粘度](@entry_id:155814)：$\nu_t \propto v \cdot l$。[两方程模型](@entry_id:271436)（Two-Equation Models）正是基于这一思想，通过求解两个独立的[输运方程](@entry_id:756133)来确定这两个尺度，进而计算[涡粘度](@entry_id:155814)。

最经典和广泛使用的[两方程模型](@entry_id:271436)是 **$k-\epsilon$ 模型**。
- 第一个方程是关于**湍动能 $k$** 的输运方程。$k$ 的平方根 $\sqrt{k}$ 自然地提供了[湍流](@entry_id:151300)的特征速度尺度。
- 第二个方程是关于**湍[动能[耗](@entry_id:751026)散率](@entry_id:748577) $\epsilon$** 的[输运方程](@entry_id:756133)。$\epsilon$ 代表湍动能通过粘性作用转化为内能的速率，其量纲为 $[长度]^2 / [时间]^3$。
通过量纲组合，$k$ 和 $\epsilon$ 可以构成一个长度尺度 $l \sim k^{3/2}/\epsilon$ 和一个时间尺度 $\tau \sim k/\epsilon$。由此，[涡粘度](@entry_id:155814)可以表示为：
$$
\nu_t = C_\mu \frac{k^2}{\epsilon}
$$
其中 $C_\mu$ 是一个经验常数。通过求解 $k$ 和 $\epsilon$ 的输运方程，我们可以在流场的每一点上动态地计算[涡粘度](@entry_id:155814)，并代入[Boussinesq假设](@entry_id:272519)中，最终封闭[RANS方程](@entry_id:275032)组 [@problem_id:1808166]。

另一个常见的[两方程模型](@entry_id:271436)是 **$k-\omega$ 模型**，它使用**比耗散率 $\omega$**（specific dissipation rate, $\omega \propto \epsilon/k$）作为第二个变量。$\omega$ 的量纲是 $[时间]^{-1}$，代表[湍流](@entry_id:151300)的特征频率。在这种模型中，[涡粘度](@entry_id:155814)的表达式为 $\nu_t = k/\omega$。

#### [湍动能输运方程](@entry_id:269723)建模

$k$ 的精确输运方程可以从[Navier-Stokes方程](@entry_id:161487)严格推导得出。其[守恒形式](@entry_id:747710)为：
$$
\frac{\partial (\rho k)}{\partial t} + \frac{\partial (\rho \overline{u_j} k)}{\partial x_j} = \frac{\partial}{\partial x_j} \left[ \dots \right] + \mathcal{P}_k - \rho \epsilon
$$
方程左边是[对流](@entry_id:141806)项。右边依次是[扩散](@entry_id:141445)项、产生项和耗散项。这些项中同样包含未知的脉动量相关项，需要进行建模。

- **产生项 ($\mathcal{P}_k$)**: 其精确形式为 $\mathcal{P}_k = -\rho \overline{u'_i u'_j} \frac{\partial \overline{u_i}}{\partial x_j}$。该项描述了平均流动通过与[雷诺应力](@entry_id:263788)相互作用，将能量转移给[湍流](@entry_id:151300)脉动的过程。在涡粘模型中，我们可以将[Boussinesq假设](@entry_id:272519)代入此定义中。对于不可压缩流，可以推导出其模型化的表达式 [@problem_id:594028]：
$$
\mathcal{P}_k = 2 \mu_t S_{ij} S_{ij}
$$
其中 $S_{ij} = \frac{1}{2} (\frac{\partial \overline{u_i}}{\partial x_j} + \frac{\partial \overline{u_j}}{\partial x_i})$ 是平均应变率张量。这个表达式明确显示，只有当存在平均速度梯度（即平均应变）时，湍动能才可能从平均流中产生。

- **[扩散](@entry_id:141445)项**: $k$ 的[扩散](@entry_id:141445)由多种机制引起，包括分子粘性[扩散](@entry_id:141445)、[湍流](@entry_id:151300)速度脉动自身的三阶相关输运（$\overline{u'_i u'_i u'_j}$）以及压力脉动与速度脉动的相关输运（$\overline{p' u'_j}$）。后两者是未知的。在标准 $k-\epsilon$ 模型中，通常将这些复杂的[湍流](@entry_id:151300)[扩散](@entry_id:141445)效应统一建模为一个简单的梯度[扩散](@entry_id:141445)形式，即 $\frac{\partial}{\partial x_j} \left( \frac{\mu_t}{\sigma_k} \frac{\partial k}{\partial x_j} \right)$，其中 $\sigma_k$ 是[湍流普朗特数](@entry_id:153739)。更高级的模型，如基于广义梯度[扩散](@entry_id:141445)假设（GGDH）的模型，则可以反映[扩散](@entry_id:141445)的各向异性特性。例如，[扩散](@entry_id:141445)项可以被模型化为 $\frac{\partial}{\partial x_j} \left( D_{jl} \frac{\partial k}{\partial x_l} \right)$，其中[扩散张量](@entry_id:748421) $D_{jl}$ 不仅依赖于分子粘度，还依赖于[雷诺应力](@entry_id:263788)本身 [@problem_id:593960]：
$$
D_{jl} = \nu \delta_{jl} + (C_k+C_p) \frac{k}{\epsilon} \overline{u'_j u'_l}
$$
这表明湍动能的[扩散](@entry_id:141445)在不同方向上可能是不同的，这取决于当地的雷诺应力结构。

- **耗散项 ($\rho \epsilon$)**: [耗散率](@entry_id:748577) $\epsilon = \nu \overline{\frac{\partial u'_i}{\partial x_k} \frac{\partial u'_j}{\partial x_k}}$ 是一个精确的定义，但它本身是一个未知的统计量，必须通过求解其自身的[输运方程](@entry_id:756133)来确定。

#### 耗散率[输运方程](@entry_id:756133)建模

$\epsilon$ 的输运方程比 $k$ 的方程更复杂，其精确形式包含大量难以处理和解释的项。因此，$\epsilon$ 方程的建模更多地依赖于物理推理和量纲分析，而非严格推导。标准 $k-\epsilon$ 模型中的 $\epsilon$ 方程形式如下：
$$
\frac{\partial (\rho \epsilon)}{\partial t} + \frac{\partial (\rho \overline{u_j} \epsilon)}{\partial x_j} = \frac{\partial}{\partial x_j} \left[ \left(\mu + \frac{\mu_t}{\sigma_\epsilon}\right) \frac{\partial \epsilon}{\partial x_j} \right] + C_{\epsilon 1} \frac{\epsilon}{k} \mathcal{P}_k - C_{\epsilon 2} \rho \frac{\epsilon^2}{k}
$$
- **产生项 ($P_\epsilon$)**: $P_\epsilon = C_{\epsilon 1} \frac{\epsilon}{k} \mathcal{P}_k$。这一项的物理根源在于涡拉伸（vortex stretching）过程。平均应变场拉伸湍流涡旋，使其尺度变小，梯度增大，从而增加了耗散。该项的核心建模思想是，耗散的产生应与[湍动能](@entry_id:262712)的产生相关。通过对更基础的涡量相关张量 $\overline{\omega'_i \omega'_j}$ 进行建模，可以为这一看似唯象的表达式提供物理依据。分析表明，模型常数 $C_{\epsilon 1}$ 与描述[涡量](@entry_id:142747)各向异性和速度各向异性之间关系的常数 $C_\omega$ 直接相关，即 $C_{\epsilon 1} = -C_\omega$ [@problem_id:594017]。
- **耗散项 ($Y_\epsilon$)**: $Y_\epsilon = C_{\epsilon 2} \rho \frac{\epsilon^2}{k}$。该项代表 $\epsilon$ 自身的衰减，可理解为耗散过程的“自我毁灭”。当[湍流](@entry_id:151300)衰减时，大尺度涡的能量耗尽，导致小尺度涡的活动减弱，耗散率也随之降低。

#### 模型间的关系

尽管 $k-\epsilon$ 和 $k-\omega$ 模型使用不同的变量，但它们在物理上是密切相关的，因为 $\epsilon$ 和 $\omega$ 描述的是同一[湍流](@entry_id:151300)场的不同方面。通过关系式 $\epsilon = \beta^* k \omega$ (其中 $\beta^*$ 是一个模型常数)，可以在二者之间进行转换。例如，在均匀衰减[湍流](@entry_id:151300)等特定条件下，将 $\epsilon$ 方程变换为 $\omega$ 方程，并与标准的 $\omega$ 方程进行比较，可以发现模型常数之间存在确定的关系，如 $\sigma_\omega = 1/\sigma_\epsilon$ [@problem_id:594019]。这表明不同的[两方程模型](@entry_id:271436)族并非完全独立，而是在描述[湍流](@entry_id:151300)物理的不同侧重点上有所取舍。

### 超越[Boussinesq假设](@entry_id:272519)：[雷诺应力模型](@entry_id:754343)

涡粘模型极大地简化了[湍流](@entry_id:151300)计算，并在许多工程应用中取得了成功。然而，其核心——[Boussinesq假设](@entry_id:272519)——是一个重大的简化，有其固有的局限性。

#### [Boussinesq假设](@entry_id:272519)的局限性

[Boussinesq假设](@entry_id:272519)的本质是一个线性的、各向同性的本构关系。它假定[雷诺应力张量](@entry_id:270803)（的各向异性部分）与平均[应变率张量](@entry_id:266108)之间通过一个标量[涡粘度](@entry_id:155814) $\mu_t$ 线性关联。这一假设的直接数学推论是，[雷诺应力张量](@entry_id:270803)的**[主轴](@entry_id:172691)**必须与平均[应变率张量](@entry_id:266108)的**主轴**对齐。

然而，真实的[湍流](@entry_id:151300)流动往往是高度**各向异性**的。例如，在受强曲率、旋转或系统性压缩/拉伸影响的流动中，雷诺应力与平均[应变率](@entry_id:154778)之间的关系远[非线性](@entry_id:637147)，其主轴也通常不重合。在这些情况下，[Boussinesq假设](@entry_id:272519)会产生错误的预测，例如无法准确捕捉[二次流](@entry_id:754609)、旋转效应或非平衡[湍流](@entry_id:151300)的演化。这正是涡粘模型的根本局限性 [@problem_id:1766472]。

#### [雷诺应力输运方程](@entry_id:754345)

为了克服[Boussinesq假设](@entry_id:272519)的局限性，需要发展更高级的模型。**[二阶矩封闭](@entry_id:754596)模型**（Second-Moment Closure, SMC），更通俗地称为**[雷诺应力模型](@entry_id:754343)**（Reynolds Stress Models, RSM），正是这样一类模型。其核心思想是，不再对[雷诺应力](@entry_id:263788)本身进行建模，而是为其每一个分量 $\overline{u_i' u_j'}$ 求解一个独立的输运方程。

雷诺应力 $\overline{u_i' u_j'}$ 的精确输运方程（RSTE）可以通过对[Navier-Stokes方程](@entry_id:161487)进行更复杂的数学操作得到：
$$
\frac{D \overline{u_i' u_j'}}{Dt} = \mathcal{P}_{ij} + \phi_{ij} - \epsilon_{ij} + \mathcal{D}_{ij}^t + \mathcal{D}_{ij}^v
$$
其中，$\frac{D}{Dt}$ 是随平均流的[物质导数](@entry_id:172646)。右侧的各项分别为：
- **产生项 ($\mathcal{P}_{ij}$)**: $\mathcal{P}_{ij} = -(\overline{u_i' u_k'} \frac{\partial \overline{u_j}}{\partial x_k} + \overline{u_j' u_k'} \frac{\partial \overline{u_i}}{\partial x_k})$。此项是精确的，不需建模。它描述了[平均速度](@entry_id:267649)梯度与现有[雷诺应力](@entry_id:263788)相互作用从而产生新的[雷诺应力](@entry_id:263788)的过程。
- **压力-应变相关项 ($\phi_{ij}$)**: $\phi_{ij} = \overline{p'(\frac{\partial u'_i}{\partial x_j} + \frac{\partial u'_j}{\partial x_i})}$。此项是未知的，必须建模。
- **耗散张量 ($\epsilon_{ij}$)**: $\epsilon_{ij} = 2\nu \overline{\frac{\partial u'_i}{\partial x_k}\frac{\partial u'_j}{\partial x_k}}$。此项也是未知的，需要建模。
- **[湍流](@entry_id:151300)[扩散](@entry_id:141445)项 ($\mathcal{D}_{ij}^t$)** 和 **分子扩散项 ($\mathcal{D}_{ij}^v$)**: 这些项也是未知的，需要建模。

尽管RSTE本身是精确的，但它包含了多个需要建模的未知项。然而，与直接对[雷诺应力](@entry_id:263788)建模相比，对这些更基础的物理过程项（如压力-应变、耗散）进行建模，有望捕捉更丰富的[湍流](@entry_id:151300)物理。

#### 关键未封闭项的物理作用与建模

在RSTE的所有未知项中，**压力-应变相关项 $\phi_{ij}$** (有时也记为 $\Pi_{ij}$) 扮演着至关重要的角色。为了理解其物理作用，我们可以考察它对湍动能 $k = \frac{1}{2}\overline{u_k' u_k'}$ 的贡献。其贡献由它的迹 $\phi_{kk}$ 决定。对于不可压缩流，$\frac{\partial u'_k}{\partial x_k} = 0$，因此：
$$
\phi_{kk} = \overline{p'(2\frac{\partial u'_k}{\partial x_k})} = 0
$$
这表明压力-应变项**既不产生也不耗散总的湍动能**。它的作用是**纯粹的再分配**。具体而言，它将能量在不同的法向[雷诺应力](@entry_id:263788)分量（$\overline{u_1'^2}$, $\overline{u_2'^2}$, $\overline{u_3'^2}$）之间进行重新分配。在一个各向异性的[湍流](@entry_id:151300)场中，比如剪切流中流向速度脉动能量远大于其他方向（$\overline{u_1'^2} \gg \overline{u_2'^2}, \overline{u_3'^2}$），压力-应变项会倾向于将能量从能量最高的脉动分量（流向）转移到能量较低的分量（法向和展向），从而驱动[湍流](@entry_id:151300)趋向于各向同性的状态。这一效应被称为“慢”压力-应变项或“返回各向同性”项。此外，$\phi_{ij}$ 还有一个“快”部分，与平均应变率直接相关，它会即时地响应平均流的变形。对 $\phi_{ij}$ 的精确建模是RSM成功的关键 [@problem_id:1766178]。

#### [各向异性张量](@entry_id:746467)[输运方程](@entry_id:756133)

为了更清晰地描述[湍流](@entry_id:151300)的结构，可以引入**无量纲[各向异性张量](@entry_id:746467)** $a_{ij}$：
$$
a_{ij} = \frac{\overline{u_i' u_j'}}{2k} - \frac{1}{3}\delta_{ij}
$$
该张量描述了[雷诺应力](@entry_id:263788)偏离各向同性状态的程度（各向同性时 $a_{ij}=0$）。从RSTE出发，并引入对耗散张量（通常假设为各向同性 $\epsilon_{ij} = \frac{2}{3}\epsilon \delta_{ij}$）和压力-应变项的先进模型，我们可以推导出关于[各向异性张量](@entry_id:746467) $a_{ij}$ 本身的输运方程。

例如，在均匀[湍流](@entry_id:151300)（[湍流统计](@entry_id:200093)量空间均匀）的简化情况下，可以推导出 $a_{ij}$ 的[演化方程](@entry_id:268137) [@problem_id:593931]：
$$
\frac{D a_{ij}}{Dt} = \frac{1-C_{QI}}{2k}\left(\mathcal{P}_{ij} - \frac{2}{3}\mathcal{P}_k\delta_{ij}\right) - \frac{\mathcal{P}_k}{k}a_{ij} + \left(1 - \frac{C_R}{2}\right)\frac{\varepsilon}{k}a_{ij}
$$
其中 $C_{QI}$ 和 $C_R$ 是压力-应变模型的常数。这个方程优雅地展示了各向异性是如何演化的：第一项代表平均速度梯度如何直接“产生”各向异性；第二项是湍动能产生带来的稀释效应；第三项则是由压力-应变和耗散共同作用，驱动[湍流](@entry_id:151300)返回各向同性的过程。通过直接求解此[类方程](@entry_id:144428)，RSM能够动态地、更真实地捕捉[湍流各向异性](@entry_id:756224)的复杂演化，这是涡粘模型无法企及的。