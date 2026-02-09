## 引言
在大涡模拟（LES）这一强大的湍流计算工具中，其核心思想在于通过空间滤波将流场划分为可直接求解的大尺度运动和必须建模的小尺度运动。这一划分不可避免地在滤波后的控制方程中引入了一个未知的项——亚格子尺度（SGS）应力张量，它代表了未解析的小尺度涡对已解析的大尺度流场的动量输运效应。如何准确地为这一项建模，是决定LES模拟成败的关键，也是计算流体力学领域持续研究的核心问题。

本文旨在系统性地剖析SGS应力张量及其建模的完整图景。我们将从其诞生的根源出发，探索其复杂的物理内涵，并逐步深入到解决这一封闭问题的各种理论与实践方法中。

读者将通过本文学习到：
- 在 **第一章：原理与机制** 中，我们将追溯SGS应力张量如何从滤波操作中产生，学习其数学分解（如各向同性/偏分解、LCR分解）的物理意义，并掌握作为建模基石的涡粘性假设及其与能量串级的关系。
- 在 **第二章：应用与跨学科交叉** 中，我们将探讨标准模型（如Smagorinsky模型）的局限性，并学习如何通过动态模型、壁模型以及针对特定物理现象（如旋转、压缩、相变）的先进模型来克服这些挑战，将其应用扩展到更广泛的工程与科学问题中。
- 在 **第三章：动手实践** 中，你将有机会通过具体计算练习，将理论知识应用于实践，亲手推导和分析SGS应力的不同分量及动态模型的实现，从而巩固对核心概念的理解。

本系列内容将引领读者从基本原理走向前沿应用，为理解和应用LES中的SGS模型提供坚实的基础。

## 原理与机制

在大涡模拟 (Large Eddy Simulation, LES) 的框架中，对流场变量进行空间滤波是其核心思想。这一操作将湍流运动分解为可直接求解的大尺度（或称解析尺度）运动和必须通过模型来封闭的、包含能量更少的小尺度（或称亚格子尺度）运动。本章旨在深入探讨亚格子尺度 (Subgrid-Scale, SGS) 应力张量的起源、物理内涵、数学分解及其建模的基本原理和机制。

### 亚格子尺度应力的起源：滤波操作

LES 的数学基础是对瞬时的 Navier-Stokes 方程进行低通空间滤波。对于一个任意的流场变量 $f(\boldsymbol{x}, t)$，其滤波后的形式 $\overline{f}(\boldsymbol{x}, t)$ 定义为一个卷积积分：

$$
\overline{f}(\boldsymbol{x}, t) = \int_{\mathcal{D}} G_{\Delta}(\boldsymbol{x} - \boldsymbol{r}) f(\boldsymbol{r}, t) \, \mathrm{d}\boldsymbol{r}
$$

其中 $\mathcal{D}$ 是流动区域，$G_{\Delta}$ 是**滤波核函数 (filter kernel)**，其特征宽度为 $\Delta$。这个宽度 $\Delta$ 决定了尺度分离的界限：大于 $\Delta$ 的流动结构被视为解析尺度，小于 $\Delta$ 的则被归为亚格子尺度。

为了使滤波过程具有物理意义并简化数学处理，滤波核函数通常需要满足以下几个关键性质 [@problem_id:3367528]：

1.  **线性 (Linearity)**：滤波是一个线性操作，即 $\overline{f+g} = \overline{f} + \overline{g}$。卷积积分自然满足此性质。

2.  **常数守恒 (Constant Preservation)**：对一个常数进行滤波应得到其自身，即 $\overline{c} = c$。这要求滤波核函数满足**归一化条件**：$\int_{\mathcal{D}} G_{\Delta}(\boldsymbol{r}) \, \mathrm{d}\boldsymbol{r} = 1$。

3.  **平移不变性 (Translational Invariance)**：滤波核函数仅依赖于空间位置的相对差异，而非绝对位置。这保证了在均匀流中滤波操作不会人为地引入不均匀性。

在均匀或周期性流动中，且当滤波宽度 $\Delta$ 为常数时，滤波操作与空间微分操作可以交换次序，即 $\overline{\partial f / \partial x_i} = \partial \overline{f} / \partial x_i$。这一性质极大地简化了滤波后方程的推导。

当我们将此滤波操作应用于不可压缩流动的 Navier-Stokes 方程时，非线性的对流项 $\partial (u_i u_j) / \partial x_j$ 带来了核心的封闭问题。滤波后的对流项为 $\overline{\partial (u_i u_j) / \partial x_j} = \partial \overline{u_i u_j} / \partial x_j$。由于滤波和乘积运算通常不可交换，我们得到 $\overline{u_i u_j} \neq \overline{u}_i \overline{u}_j$。为了封闭方程，我们定义**亚格子尺度 (SGS) 应力张量** $\tau_{ij}$ 来表示这两者之间的差异：

$$
\tau_{ij} \equiv \overline{u_i u_j} - \overline{u}_i \overline{u}_j
$$

这个张量代表了未解析的亚格子尺度运动通过动量输运对已解析的宏观尺度运动产生的净效应。将此定义代入滤波后的动量方程，我们得到 LES 的主控方程：

$$
\frac{\partial \overline{u}_i}{\partial t} + \frac{\partial (\overline{u}_i \overline{u}_j)}{\partial x_j} = -\frac{1}{\rho}\frac{\partial \overline{p}}{\partial x_i} + \nu \frac{\partial^2 \overline{u}_i}{\partial x_j \partial x_j} - \frac{\partial \tau_{ij}}{\partial x_j}
$$

从方程中可见，SGS 应力张量的散度 $-\partial \tau_{ij} / \partial x_j$ 表现为一个作用在解析尺度流场上的附加“力”。LES 的核心挑战就在于如何建立 $\tau_{ij}$ 与已知的解析尺度场 $\overline{u}_i$ 之间的关系，即所谓的 **SGS 模型**。

值得强调的是，LES 中的 SGS 应力与雷诺平均 Navier-Stokes (RANS) 方法中的雷诺应力在概念上有着本质区别 [@problem_id:3367536]。雷诺应力 $\langle u_i' u_j' \rangle$ 源于对所有湍流脉动进行时间或系综平均，旨在描述所有尺度的湍流波动对平均流的总体影响。而 SGS 应力 $\tau_{ij}$ 则源于空间滤波，仅代表小于滤波尺度 $\Delta$ 的那部分湍流运动对大于 $\Delta$ 的运动的影响。因此，SGS 应力是依赖于 $\Delta$ 的，并且是时空变化的瞬时量，而雷诺应力则是一个统计平均量。

### SGS 应力张量的分解与物理内涵

为了更好地理解 $\tau_{ij}$ 的物理作用并指导其建模，我们通常将其进行分解。

#### 各向同性与偏部分解

任何二阶对称张量都可以唯一地分解为一个**各向同性 (isotropic)**部分和一个**偏 (deviatoric)**部分 [@problem_id:3367470]。对于 SGS 应力张量 $\tau_{ij}$，其分解形式为：

$$
\tau_{ij} = \tau_{ij}^{\text{dev}} + \frac{1}{3}\tau_{kk}\delta_{ij}
$$

其中 $\delta_{ij}$ 是克罗内克符号。各向同性部分 $\frac{1}{3}\tau_{kk}\delta_{ij}$ 在所有方向上施加均等的正应力（或压应力），其大小由 $\tau_{ij}$ 的迹 $\tau_{kk}$ 决定。$\tau_{kk}$ 的物理意义非常重要，它与亚格子尺度的动能 **$k_{\text{sgs}}$** 直接相关：

$$
k_{\text{sgs}} = \frac{1}{2}(\overline{u_k u_k} - \overline{u}_k \overline{u}_k) = \frac{1}{2}\tau_{kk}
$$

因此，各向同性部分可以写成 $\frac{2}{3}k_{\text{sgs}}\delta_{ij}$。在不可压缩流动的动量方程中，该项的散度 $\partial (\frac{2}{3}k_{\text{sgs}}\delta_{ij})/\partial x_j = \partial (\frac{2}{3}k_{\text{sgs}})/\partial x_i$ 是一个标量的梯度，其形式与压力梯度完全相同。因此，它可以被吸收到一个**修正压力 (modified pressure)** $p^*$ 中，$p^* = \overline{p} + \frac{2}{3}\rho k_{\text{sgs}}$。这意味着许多 SGS 模型可以只关注于对偏应力部分 $\tau_{ij}^{\text{dev}}$ 进行建模。

偏应力张量 $\tau_{ij}^{\text{dev}} = \tau_{ij} - \frac{1}{3}\tau_{kk}\delta_{ij}$ 是一个无迹张量，它描述了 SGS 应力的各向异性部分，代表了由亚格子运动引起的剪切应力和不等的正应力。这部分应力是导致解析尺度流体微团发生变形和能量在不同尺度间传递的主要原因。在大多数湍流中，尤其是在存在强剪切或边界的区域，偏应力部分起主导作用。例如：

*   **壁面附近区域**：固体边界的存在破坏了流动的各向同性，湍流结构被拉伸和展平，导致未解析的运动高度各向异性 [@problem_id:3367470]。
*   **强应变区域**：如混合层，强烈的平均应变场会使湍流涡旋沿特定方向拉伸，导致亚格子尺度应力显著的各向异性 [@problem_id:3367470]。
*   **稳定分层流**：浮力效应会抑制垂直方向的运动，形成“扁平”的湍流结构，同样导致强烈的各向异性 [@problem_id:3367470]。

而在理想的均匀各向同性湍流的惯性子区，小尺度运动被假设为统计上各向同性，此时各向同性部分则相对更为重要。

#### Leonard, Cross, and Reynolds 分解

为了更精细地揭示 $\tau_{ij}$ 的构成，可以将其进一步分解为三个部分 [@problem_id:3367532]。通过将瞬时速度分解为解析部分和亚格子部分 $u_i = \overline{u}_i + u_i'$，我们得到：

$$
\tau_{ij} = \underbrace{(\overline{\overline{u}_i \overline{u}_j} - \overline{u}_i \overline{u}_j)}_{\text{Leonard stress, } L_{ij}} + \underbrace{(\overline{\overline{u}_i u_j'} + \overline{u_i' \overline{u}_j})}_{\text{Cross stress, } C_{ij}} + \underbrace{\overline{u_i' u_j'}}_{\text{Reynolds stress, } R_{ij}}
$$

*   **Leonard 应力 ($L_{ij}$)**：代表了不同解析尺度涡之间的相互作用对滤波操作产生的贡献。它不直接涉及亚格子尺度速度，并且不直接耗散能量。
*   **Cross 应力 ($C_{ij}$)**：代表了解析尺度涡与亚格子尺度涡之间的相互作用。这一项既可以从大尺度向小尺度传递能量，也可以反向传递。
*   **Reynolds 应力 ($R_{ij}$)**：代表了亚格子尺度涡之间的相互作用，通常被认为是主要的能量耗散项。

这种分解揭示了 SGS 应力的复杂性，并启发了更先进的建模策略，例如混合模型，它试图分别为这些具有不同物理特性的项进行建模。

### 涡粘性假设与基础模型

最简单且最广泛使用的 SGS 建模方法是**涡粘性假设 (eddy-viscosity hypothesis)**，它类比于分子粘性应力与[应变率](@entry_id:154778)的线性关系 [@problem_id:3367513]。该假设认为，SGS 偏应力张量与解析尺度的应变率张量 $\overline{S}_{ij}$ 成正比：

$$
\tau_{ij}^{\text{dev}} = -2\nu_t \overline{S}_{ij}
$$

其中 $\overline{S}_{ij} = \frac{1}{2}\left(\frac{\partial \overline{u}_i}{\partial x_j} + \frac{\partial \overline{u}_j}{\partial x_i}\right)$ 是解析尺度的应变率张量，$\nu_t$ 是**涡粘性系数 (eddy viscosity)**。这个模型的合理性基于以下几点：

1.  **张量性质**：模型自动满足 $\tau_{ij}^{\text{dev}}$ 是对称且无迹的（在不可压缩流中 $\overline{S}_{kk} = 0$）。
2.  **伽利略不变性**：模型依赖于速度梯度，而非速度本身，因此在不同惯性参考系下形式不变。
3.  **物理图像**：它假设亚格子尺度运动的主要作用类似于增强的分子粘性，即从解析尺度流场中“耗散”能量，并将其传递到更小的尺度。

这个能量传递的过程可以通过**亚格子耗散率** $\Pi = -\tau_{ij}\overline{S}_{ij}$ 来量化。对于涡粘性模型，由于各向同性部分不贡献能量传递，我们有：

$$
\Pi = -\tau_{ij}^{\text{dev}}\overline{S}_{ij} = -(-2\nu_t \overline{S}_{ij})\overline{S}_{ij} = 2\nu_t \overline{S}_{ij}\overline{S}_{ij}
$$

由于 $\overline{S}_{ij}\overline{S}_{ij} \ge 0$，只要 $\nu_t \ge 0$，该模型就保证了 $\Pi \ge 0$。这代表能量总是从解析尺度流向亚格子尺度，这个过程称为**正向散射 (forward scatter)** 或能量顺级串级 [@problem_id:3367477]。这与 Richardson 的能量串级级联的经典图像在平均意义上是一致的：大涡破碎成小涡，能量从大尺度传递到小尺度，最终在分子粘性尺度耗散。

涡粘性系数 $\nu_t$ 的建模是关键。基于 Kolmogorov 的惯性子区理论，可以通过量纲分析来估计其尺度关系 [@problem_id:3367537]。在惯性子区，湍流的性质应只由能量耗散率 $\varepsilon$ 和尺度 $\Delta$ 决定。涡粘性的量纲是 $[L^2/T]$，可以由特征速度 $u_{\Delta}$ 和特征长度 $\Delta$ 构成，即 $\nu_t \sim u_{\Delta} \Delta$。根据 Kolmogorov 理论，$u_{\Delta} \sim (\varepsilon \Delta)^{1/3}$。因此，我们得到：

$$
\nu_t \sim (\varepsilon \Delta)^{1/3} \cdot \Delta = \varepsilon^{1/3} \Delta^{4/3}
$$

经典的 **Smagorinsky 模型**正是这一思想的体现。它假设能量的产生与耗散局部平衡，即 $\varepsilon \approx \Pi$，并利用解析尺度应变率的模量 $|\overline{S}| = (2\overline{S}_{mn}\overline{S}_{mn})^{1/2}$ 来估计能量串级速率，最终得到：

$$
\nu_t = (C_s \Delta)^2 |\overline{S}|
$$

其中 $C_s$ 是 Smagorinsky 常数。这个模型虽然简单且物理基础明确，但也存在过度耗散、无法描述能量反向传递等缺点。

### 先进建模概念与实践考量

#### 能量的正向散射与反向散射

涡粘性模型强制能量单向传递 ($\Pi \ge 0$)，但这只是真实物理过程的平均表现。实际上，湍流中存在局部和瞬时的能量从亚格子尺度向解析尺度回传的现象，称为**反向散射 (backscatter)**，即 $\Pi  0$ [@problem_id:3367477]。

*   **涡粘性模型**（如 Smagorinsky、Vreman 模型等）通过强制 $\nu_t \ge 0$ 的构造，完全排除了反向散射。
*   **尺度相似性模型 (scale-similarity models)** 和**梯度模型 (gradient models)**，它们基于解析尺度场来重构 SGS 应力（例如，梯度模型 $\tau_{ij} \propto \Delta^2 \partial_k \overline{u}_i \partial_k \overline{u}_j$），其与 $\overline{S}_{ij}$ 的缩并并不保证非负，因此能够自然地产生正向和反向散射 [@problem_id:3367477]。然而，这些模型往往耗散性不足，单独使用时可能导致数值不稳定。
*   **动态模型 (dynamic models)** 通过 Germano 恒等式，利用解析尺度流场的信息来动态计算模型系数。这允许涡粘性系数 $\nu_t$ 在局部和瞬时可以取负值，从而能够模拟反向散射。

#### 动态模型与混合模型

为了克服 Smagorinsky 模型常数普适性的问题，并更好地反映流动的局部状态，**动态程序 (dynamic procedure)** 被引入。其核心思想是引入一个比网格滤波 $\Delta$ 更宽的**测试滤波 (test filter)** $\hat{\Delta}$。通过对解析尺度场进行二次滤波，可以得到一个完全由解析尺度信息构成的应力，即 Germano 恒等式。这个恒等式提供了在测试尺度上的 SGS 应力信息，可用于动态地确定模型中的系数（如动态确定 $C_s$）。

**混合模型 (mixed models)** 则试图结合不同模型的优点 [@problem_id:3367532]。一个常见的形式是组合一个尺度相似性模型（用于更好地表示 Leonard 应力并捕捉反向散射）和一个涡粘性模型（用于提供足够的耗散以保证数值稳定）。例如，一个双系数动态混合模型可以写成：

$$
\tau_{ij}^{\text{mod}} = \alpha\,m_2(\Delta;G)\,\partial_k \overline{u}_i\,\partial_k \overline{u}_j - 2\,\beta\,\Delta^2\,|\overline{S}|\,\overline{S}_{ij}
$$

其中第一项是梯度模型形式，第二项是 Smagorinsky 模型形式。系数 $\alpha$ 和 $\beta$ 可以通过动态程序同时确定。$m_2(\Delta;G)$ 是滤波核函数的二阶矩，它使得模型能够反映滤波核函数形状的影响（例如，对于高斯核和高帽核，该项是不同的）。

#### 可实现性约束

一个物理上合理的 SGS 模型必须满足**可实现性 (realizability)** 约束 [@problem_id:3367512]。最基本的约束是，作为一个由速度乘积构成的相关张量 $\tau_{ij} + \overline{u}_i\overline{u}_j = \overline{u_i u_j}$，其模型化的形式必须是半正定的。这意味着其所有特征值都必须非负。这直接导致了以下约束：

1.  对角元非负：$\tau_{ii} \ge 0$（无求和），这保证了各方向的法向应力是拉伸性的。
2.  亚格子动能非负：$k_{\text{sgs}} = \frac{1}{2}\tau_{kk} \ge 0$。
3.  满足 Schwartz 不等式：$|\tau_{ij}|^2 \le \tau_{ii}\tau_{jj}$（无求和）。

在某些模型中，特别是在动态模型中，计算出的 $\tau_{ij}^{\text{mod}}$ 可能违反这些约束。为了强制可实现性，可以设计一个投影算子。该算子首先对模型计算出的 $\tau_{ij}^{\text{mod}}$ 进行特征值分解。然后，将所有负特征值置为零，并可能根据物理约束（如基于局部平衡假设推导出的 $k_{\text{sgs}}$ 上限）对正特征值进行缩放，最后用修正后的特征值和原始的特征向量重构出一个满足可实现性约束的应力张量 [@problem_id:3367512]。

#### 模型一致性与隐式滤波

一个SGS模型必须是**一致的 (consistent)**，这意味着当滤波宽度（或网格尺寸）$\Delta \to 0$ 时，模型所附加的 SGS 应力项必须趋于零，从而使 LES 方程收敛到直接数值模拟 (DNS) 所求解的原始 Navier-Stokes 方程 [@problem_id:3367533]。对于涡粘性模型 $\tau_{ij}^{\text{dev}} = -2 \nu_t \overline{S}_{ij}$，只要 $\nu_t$ 随 $\Delta$ 的正幂次（如 $\Delta^2$）趋于零，模型就是一致的。Smagorinsky 模型、梯度模型和（对于光滑场）动态 Smagorinsky 模型都满足这一要求。

在实际的计算流体力学 (CFD) 应用中，尤其是在有限体积法中，滤波操作通常不是显式施加的。相反，离散化过程本身就起到了滤波的作用，这被称为**隐式滤波 (implicit filtering)** [@problem_id:3367461]。例如，将一个连续场变量表示为其在网格单元上的平均值，这本身就是一个高帽滤波。随后，在计算单元界面上的通量时，对相邻单元的平均值进行插值（如线性插值），这又是一次滤波操作。

我们可以通过傅里叶分析来量化这种隐式滤波的**等效滤波宽度 $\Delta_{\text{eff}}$**。考虑一个一维均匀网格，网格间距为 $\Delta$。将变量表示为单元平均值，其傅里叶传递函数为 $\text{sinc}(k\Delta/2)$。若在单元界面上使用相邻单元平均值的算术平均（二阶中心插值），其传递函数为 $\cos(k\Delta/2)$。这两个操作复合的总传递函数为 $H(k) = \text{sinc}(k\Delta/2)\cos(k\Delta/2) = \text{sinc}(k\Delta)$。通过将其在小波数下的泰勒展开与一个等效高帽滤波的传递函数 $\text{sinc}(k\Delta_{\text{eff}}/2)$ 进行比较，可以发现，要使两者在 $k^2$ 阶上吻合，必须有 $\Delta_{\text{eff}} = 2\Delta$ [@problem_id:3367461]。这揭示了一个重要的事实：数值格式的等效滤波尺度可能显著大于网格间距本身。因此，在实践中，SGS 模型的行为与数值离散格式紧密耦合，这是进行高质量 LES 时必须考虑的关键因素。