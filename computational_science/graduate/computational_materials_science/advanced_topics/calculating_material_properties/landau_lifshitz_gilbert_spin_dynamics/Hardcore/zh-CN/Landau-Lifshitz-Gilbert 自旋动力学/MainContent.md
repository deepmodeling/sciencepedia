## 引言
在计算材料科学和凝聚态物理领域，理解和预测磁性材料中磁矩的动态行为至关重要。从硬盘中的[数据存储](@entry_id:141659)到下一代自旋电子器件中的信息处理，磁化动力学无处不在。然而，描述这种复杂、[非线性](@entry_id:637147)的时空演化过程，需要一个坚实的理论框架。朗道-栗弗席兹-吉尔伯特（Landau-Lifshitz-Gilbert, LLG）方程正是这一框架的基石，它为我们提供了一套强大的数学工具来模拟磁矩在各种内外部影响下的演变。

本文旨在为研究生和研究人员提供对LLG[自旋动力学](@entry_id:146095)的全面而深入的理解。我们将系统性地解决“如何从物理原理出发，建立一个可计算的磁化动力学模型”这一核心问题。通过本文的学习，读者将不仅掌握[LLG方程](@entry_id:139075)的数学形式，更能深刻理解其背后的物理机制、在现代科技中的关键应用以及将其付诸实践的计算方法。

文章将分为三个核心部分展开：
- **第一章：原理与机制**，我们将从基本物理定律出发，详细推导[LLG方程](@entry_id:139075)，解析其进动项和阻尼项的物理意义，并系统阐述作为驱动力的各类有效场（如交换场、各向异性场、静[磁场](@entry_id:153296)）以及包含自旋转移力矩的现代扩展。
- **第二章：应用与[交叉](@entry_id:147634)学科联系**，我们将展示[LLG方程](@entry_id:139075)如何作为理论工具，用于解读[铁磁共振](@entry_id:193287)等实验现象，指导MRAM、赛道存储器等自旋电子器件的设计，并探讨其与[热力学](@entry_id:141121)、力学等领域的交叉融合。
- **第三章：动手实践**，我们将通过一系列计算练习，引导读者将理论知识转化为实际的[微磁学](@entry_id:751970)模拟代码，包括有效场的离散化计算和高效的[时间积分算法](@entry_id:756002)实现。

现在，让我们从构建这一强大理论的第一块基石开始，深入探索[LLG方程](@entry_id:139075)的原理与机制。

## 原理与机制

在深入探讨计算材料科学中[自旋动力学](@entry_id:146095)的[模拟方法](@entry_id:751987)之前，我们必须首先建立其理论基础。本章将系统地阐述描述铁磁体中磁矩动态演化的核心方程——朗道-栗弗席兹-吉尔伯特（Landau-Lifshitz-Gilbert, LLG）方程。我们将从其基本构成出发，逐步解析驱动磁矩运动的各种物理机制，并最终将其扩展至包含现代[自旋电子学](@entry_id:141468)效应的广义形式。

### [朗道-栗弗席兹-吉尔伯特方程](@entry_id:139075)

在[微磁学](@entry_id:751970)理论的框架下，[铁磁材料](@entry_id:261099)的磁性状态由一个连续的[磁化矢量](@entry_id:180304)场 $\mathbf{M}(\mathbf{r}, t)$ 来描述。在大多数情况下，尤其是在低于居里温度时，[磁化矢量](@entry_id:180304)的大小（即[饱和磁化强度](@entry_id:143313) $M_s$）可以被认为是恒定的，即 $|\mathbf{M}| = M_s$。因此，磁矩的动态演化主要体现在其方向的变化上。为了方便，我们通常使用单位[磁化矢量](@entry_id:180304) $\mathbf{m}(\mathbf{r}, t) = \mathbf{M}(\mathbf{r}, t) / M_s$ 来描述磁矩的方向，其中 $|\mathbf{m}| = 1$。

磁[矩动力学](@entry_id:752137)的核心思想源于角动量与扭矩之间的关系。磁矩 $\mathbf{M}$ 与其承载的电子系统的总角动量 $\mathbf{L}$ 成正比，关系为 $\mathbf{M} = \gamma \mathbf{L}$，其中 $\gamma$ 是[旋磁比](@entry_id:149290)。对于电子而言，其[电荷](@entry_id:275494)为负，导致其磁矩与自旋角动量的方向相反，因此电子的[旋磁比](@entry_id:149290)为一个负值，即 $\gamma  0$。当存在一个[有效磁场](@entry_id:139861) $\mathbf{H}_{\mathrm{eff}}$ 时，磁矩会受到一个扭矩 $\boldsymbol{\tau} = \mu_0 (\mathbf{M} \times \mathbf{H}_{\mathrm{eff}})$，其中 $\mu_0$ 是[真空磁导率](@entry_id:186031)。根据牛顿第二定律的转动形式，角动量的变化率等于所受扭矩，即 $\frac{d\mathbf{L}}{dt} = \boldsymbol{\tau}$。将 $\mathbf{L} = \mathbf{M}/\gamma$ 代入，我们得到：

$$
\frac{d\mathbf{M}}{dt} = \gamma (\mathbf{M} \times \mu_0 \mathbf{H}_{\mathrm{eff}})
$$

这个方程描述了磁矩 $\mathbf{M}$ 围绕有效磁场 $\mathbf{H}_{\mathrm{eff}}$ 的**进动**（precession）。为了理解进动的方向，我们考虑一个简单的例子：设有效磁场沿 $z$ 轴正方向，$\mathbf{H}_{\mathrm{eff}} = H_0 \hat{\mathbf{z}}$ ($H_00$)，初始磁矩沿 $x$ 轴正方向，$\mathbf{M}(0) = M_s \hat{\mathbf{x}}$。在 $t=0$ 时刻，磁矩的变化率为：

$$
\frac{d\mathbf{M}}{dt} \bigg|_{t=0} = \gamma (M_s \hat{\mathbf{x}} \times \mu_0 H_0 \hat{\mathbf{z}}) = \gamma \mu_0 M_s H_0 (\hat{\mathbf{x}} \times \hat{\mathbf{z}}) = - \gamma \mu_0 M_s H_0 \hat{\mathbf{y}}
$$

由于电子的[旋磁比](@entry_id:149290) $\gamma  0$，而 $\mu_0, M_s, H_0$ 均为正值，所以 $- \gamma \mu_0 M_s H_0$ 是一个正数。因此，$\frac{d\mathbf{M}}{dt}$ 的初始方向为 $+\hat{\mathbf{y}}$。这意味着磁矩从 $+\hat{\mathbf{x}}$ 方向开始向 $+\hat{\mathbf{y}}$ 方向运动。从 $+\hat{\mathbf{z}}$ 轴向下看，这是一个逆时针的旋转。这恰好符合围绕角频率矢量 $\boldsymbol{\omega} = -\gamma \mu_0 \mathbf{H}_{\mathrm{eff}}$ 的[右手定则](@entry_id:156766)进动。由于 $\gamma  0$，[角频率](@entry_id:261565)矢量 $\boldsymbol{\omega}$ 与[磁场](@entry_id:153296) $\mathbf{H}_{\mathrm{eff}}$ 的方向相同。这个例子清晰地揭示了[旋磁比](@entry_id:149290)的符号是如何决定磁矩进动方向的 。

然而，纯粹的进动无法描述磁矩弛豫到能量最低状态（通常是与[有效磁场](@entry_id:139861)平行）的物理过程。真实材料中存在[能量耗散](@entry_id:147406)，使得磁矩最终会趋向于与[有效磁场](@entry_id:139861)对齐。为了在现象学上描述这种耗散，Gilbert 引入了一个**阻尼项**。该阻尼项必须满足两个物理约束：(1) 它是一个耗散项，应使能量降低；(2) 它不能改变磁矩的大小，即该项产生的扭矩必须始终与磁矩 $\mathbf{M}$ 垂直。Gilbert 提出的形式正比于 $\mathbf{M} \times \frac{d\mathbf{M}}{dt}$，它天然地满足了第二个条件。

综合进动项和阻尼项，我们得到了描述磁[矩动力学](@entry_id:752137)的**朗道-栗弗席兹-吉尔伯特（LLG）方程**的吉尔伯特形式。在文献中，常将 $\mu_0$ 吸收到[旋磁比](@entry_id:149290)中，定义一个新的[旋磁比](@entry_id:149290)（在此我们仍记作 $\gamma$，其单位为 $\text{s}^{-1}\text{T}^{-1}$）。对于单位[磁化矢量](@entry_id:180304) $\mathbf{m}$，方程可以写作 ：

$$
\frac{d\mathbf{m}}{dt} = - \gamma (\mathbf{m} \times \mathbf{H}_{\mathrm{eff}}) + \alpha \left(\mathbf{m} \times \frac{d\mathbf{m}}{dt}\right)
$$

在这里：
*   **第一项** $-\gamma (\mathbf{m} \times \mathbf{H}_{\mathrm{eff}})$ 是**进动项**，描述了 $\mathbf{m}$ 围绕 $\mathbf{H}_{\mathrm{eff}}$ 的[拉莫尔进动](@entry_id:143131)。$\gamma$ 是[旋磁比](@entry_id:149290)，其[国际单位制](@entry_id:172547)（SI）单位是 $\text{s}^{-1}\cdot\text{T}^{-1}$。
*   **第二项** $\alpha (\mathbf{m} \times \frac{d\mathbf{m}}{dt})$ 是**[吉尔伯特阻尼](@entry_id:749904)项**，描述了磁矩朝向有效磁场方向的弛豫过程。$\alpha$ 是一个无量纲的常数，称为**[吉尔伯特阻尼](@entry_id:749904)系数**，它量化了耗散的强度。
*   $\mathbf{H}_{\mathrm{eff}}$ 是**有效磁场**，单位是特斯拉 (T)，它是系统总自由能对磁矩的泛函导数，是驱动整个动力学过程的[广义力](@entry_id:169699)。
*   $M_s$ 是**[饱和磁化强度](@entry_id:143313)**，单位是安培/米 (A/m)，它定义了宏观磁化强度与单位矢量之间的关系 $\mathbf{M} = M_s \mathbf{m}$。

一个重要的特性是，LLG 方程本身保证了磁矩大小的守恒。对 $|\mathbf{m}|^2 = \mathbf{m} \cdot \mathbf{m} = 1$ 两边对时间求导，得到 $2\mathbf{m} \cdot \frac{d\mathbf{m}}{dt} = 0$，这说明 $\frac{d\mathbf{m}}{dt}$ 总是与 $\mathbf{m}$ 正交。LLG 方程的两个项都是叉乘形式，自然满足这个正交条件，因此动力学演化过程中 $|\mathbf{m}|$ 始终为 1。

### 等价形式与基本性质

LLG 方程的吉尔伯特形式是一个[隐式方程](@entry_id:177636)，因为时间导数 $\frac{d\mathbf{m}}{dt}$ 出现在方程的两边。通过代数运算，可以将其转化为一个显式方程，这便是**朗道-栗弗席兹（LL）形式**。

通过将吉尔伯特方程整理为 $(1+\alpha^2)\frac{d\mathbf{m}}{dt} = - \gamma (\mathbf{m} \times \mathbf{H}_{\mathrm{eff}}) - \alpha\gamma (\mathbf{m} \times (\mathbf{m} \times \mathbf{H}_{\mathrm{eff}}))$，我们可以得到其显式表达 ：
$$
\frac{d\mathbf{m}}{dt} = - \frac{\gamma}{1+\alpha^2} (\mathbf{m} \times \mathbf{H}_{\mathrm{eff}}) - \frac{\alpha\gamma}{1+\alpha^2} \mathbf{m} \times (\mathbf{m} \times \mathbf{H}_{\mathrm{eff}})
$$
这便是 LL 方程。如果我们定义新的系数 $\gamma' = \frac{\gamma}{1+\alpha^2}$ 和 $\lambda = \frac{\alpha\gamma}{1+\alpha^2}$，方程可以写为更紧凑的形式：
$$
\frac{d\mathbf{m}}{dt} = - \gamma' (\mathbf{m} \times \mathbf{H}_{\mathrm{eff}}) - \lambda \mathbf{m} \times (\mathbf{m} \times \mathbf{H}_{\mathrm{eff}})
$$
在这里，$\gamma'$ 是有效[旋磁比](@entry_id:149290)，而 $\lambda$ 是 LL 阻尼参数，其单位为 $\text{s}^{-1}\text{T}^{-1}$。两种形式在物理上是等价的，只是对进动和阻尼的[参数化](@entry_id:272587)方式不同。吉尔伯特形式在物理解释上更直观，而 LL 形式在数值求解时更方便，因为它是一个显式[微分方程](@entry_id:264184)。

接下来，我们探讨 LLG 方程的两个基本性质：[能量耗散](@entry_id:147406)和时间反演对称性 。

**[能量耗散](@entry_id:147406)**：系统的总能量 $E$ 是磁矩构型 $\mathbf{m}$ 的泛函。在没有显式含时外场的情况下，其时间变化率为：
$$
\frac{dE}{dt} = \int \frac{\delta E}{\delta \mathbf{m}} \cdot \frac{d\mathbf{m}}{dt} \, dV
$$
利用[有效磁场](@entry_id:139861)的定义 $\mathbf{H}_{\mathrm{eff}} = - \frac{1}{\mu_0 M_s} \frac{\delta E}{\delta \mathbf{m}}$（为简化记号，这里我们暂时忽略常数系数，即 $\frac{dE}{dt} \propto -\int \mathbf{H}_{\mathrm{eff}} \cdot \frac{d\mathbf{m}}{dt} dV$），并将 LL 形式的 $\frac{d\mathbf{m}}{dt}$ 代入，可以计算出：
$$
\mathbf{H}_{\mathrm{eff}} \cdot \frac{d\mathbf{m}}{dt} = \frac{\alpha\gamma}{1+\alpha^2} |\mathbf{m} \times \mathbf{H}_{\mathrm{eff}}|^2
$$
于是，能量变化率为：
$$
\frac{dE}{dt} \propto - \int \frac{\alpha\gamma}{1+\alpha^2} |\mathbf{m} \times \mathbf{H}_{\mathrm{eff}}|^2 \, dV
$$
由于 $\alpha > 0$ 和 $\gamma > 0$（按惯例，这里的 $\gamma$ 代表[旋磁比](@entry_id:149290)的[绝对值](@entry_id:147688)），上式表明 $\frac{dE}{dt} \le 0$。等号成立的条件是 $\mathbf{m} \times \mathbf{H}_{\mathrm{eff}} = \mathbf{0}$，即磁矩处处与[有效磁场](@entry_id:139861)平行。这证明了[吉尔伯特阻尼](@entry_id:749904)项确实导致了能量的耗散，使得系统向能量极小值状态演化。因此，能量 $E$ 是该动力学系统的一个[李雅普诺夫函数](@entry_id:273986)。

**[时间反演对称性](@entry_id:138094)**：时间反演操作定义为 $t \to -t$。由于磁矩与角动量相关，它是一个轴矢量，在时间反演下反号，即 $\mathbf{m}(t) \to -\mathbf{m}(-t)$。我们可以分析 LLG 方程中各项在时间反演下的变换性质。
*   磁矩的时间导数：$\dot{\mathbf{m}}(t) \to \dot{\mathbf{m}}(-t)$，是**时间反演偶的**。
*   [有效磁场](@entry_id:139861)：若[能量泛函](@entry_id:170311) $E[\mathbf{m}]$ 是 $\mathbf{m}$ 的[偶函数](@entry_id:163605)（如交换能、[各向异性能](@entry_id:200263)等），则 $\mathbf{H}_{\mathrm{eff}}$ 是 $\mathbf{m}$ 的奇函数。因此，$\mathbf{H}_{\mathrm{eff}}(t) \to -\mathbf{H}_{\mathrm{eff}}(-t)$，是**时间反演奇的**。
*   进动项 $-\gamma \mathbf{m} \times \mathbf{H}_{\mathrm{eff}}$：变换为 $(-\mathbf{m}(-t)) \times (-\mathbf{H}_{\mathrm{eff}}(-t)) = \mathbf{m}(-t) \times \mathbf{H}_{\mathrm{eff}}(-t)$。因此，进动项是**[时间反演](@entry_id:182076)偶的**。
*   阻尼项 $\alpha \mathbf{m} \times \dot{\mathbf{m}}$：变换为 $(-\mathbf{m}(-t)) \times (\dot{\mathbf{m}}(-t)) = -(\mathbf{m}(-t) \times \dot{\mathbf{m}}(-t))$。因此，阻尼项是**时间反演奇的**。

LLG 方程的左边是[时间反演](@entry_id:182076)偶的，而右边是时间反演偶的进动项和[时间反演](@entry_id:182076)奇的阻尼项之和。这意味着，只要[阻尼系数](@entry_id:163719) $\alpha > 0$，整个方程在时间反演下是不对称的。只有在无耗散的理想情况（$\alpha = 0$）下，动力学才具有[时间可逆性](@entry_id:274492)。阻尼项破坏了时间反演对称性，反映了磁化动力学中不可逆的[能量耗散](@entry_id:147406)过程。

### [有效磁场](@entry_id:139861)：动力学的驱动力

LLG 方程的核心驱动力是[有效磁场](@entry_id:139861) $\mathbf{H}_{\mathrm{eff}}$。它并非一个真实存在的物理场，而是一个等效场，整合了所有影响磁矩能量的物理因素。在[微磁学](@entry_id:751970)中，总能量 $E$ 是磁化构型 $\mathbf{m}(\mathbf{r})$ 的一个泛函，而有效磁场正是这个能量泛函对磁矩的**泛函变分导数** ：

$$
\mathbf{H}_{\mathrm{eff}} = - \frac{1}{\mu_0 M_s} \frac{\delta E}{\delta \mathbf{m}}
$$

泛函导数 $\frac{\delta E}{\delta \mathbf{m}}$ 定义为这样一个矢量场，它使得能量的无穷小变化 $\delta E$ 可以写成 $\delta E = \int \frac{\delta E}{\delta \mathbf{m}} \cdot \delta \mathbf{m} \, dV$。由于 LLG 方程中的扭矩都涉及与 $\mathbf{m}$ 的叉乘，$\mathbf{H}_{\mathrm{eff}}$ 中任何与 $\mathbf{m}$ 平行的分量都不会对动力学产生影响。这为计算[有效磁场](@entry_id:139861)提供了一定的自由度。

总能量通常是几个不同物理来源的能量之和，因此[有效磁场](@entry_id:139861)也是相应各项贡献的矢量和：$\mathbf{H}_{\mathrm{eff}} = \sum_i \mathbf{H}_{\mathrm{eff}}^{(i)}$。下面我们推导几种最常见的能量项所对应的有效磁场。

#### [交换相互作用](@entry_id:140006)场
交换相互作用是相邻原子磁矩之间的一种强烈的短程量子力学效应，它倾向于使磁矩相互平行（对于铁磁体）。其能量密度可以唯象地表示为与磁化方向梯度的平方成正比。总交换能为：
$$
E_{\mathrm{ex}} = \int_{\Omega} A |\nabla \mathbf{m}|^2 \, dV = \int_{\Omega} A \sum_{i,j} (\partial_i m_j)^2 \, dV
$$
其中 $A$ 是交换劲度系数。通过对该泛函进行变分并使用分部积分法（或[格林公式](@entry_id:173118)），我们可以计算其一阶变分 ：
$$
\delta E_{\mathrm{ex}} = \int_{\Omega} (-2A \nabla^2 \mathbf{m}) \cdot \delta \mathbf{m} \, dV + \oint_{\partial\Omega} (2A \frac{\partial \mathbf{m}}{\partial n}) \cdot \delta \mathbf{m} \, dS
$$
其中 $\nabla^2$ 是矢量拉普拉斯算符，$\frac{\partial \mathbf{m}}{\partial n}$ 是沿边界法向 $n$ 的导数。从[体积分](@entry_id:171119)项，我们识别出对应的有效场，即**交换场**：
$$
\mathbf{H}_{\mathrm{ex}} = \frac{2A}{\mu_0 M_s} \nabla^2 \mathbf{m}
$$
交换场正比于[磁化矢量](@entry_id:180304)场的曲率，它试图使磁化[分布](@entry_id:182848)变得平滑以减小能量。同时，边界积分项给出了**自然边界条件**。对于一个“自由”边界（即边界上没有施加额外的扭矩），为了使 $\delta E_{\mathrm{ex}}$ 对任意 $\delta \mathbf{m}$ 恒为零，边界项必须消失，这要求 $2A \frac{\partial \mathbf{m}}{\partial n} = \mathbf{0}$，即 $\frac{\partial \mathbf{m}}{\partial n} = \mathbf{0}$。这个诺伊曼型边界条件在[微磁学](@entry_id:751970)模拟中被广泛使用。

#### [磁晶各向异性](@entry_id:144488)场
[晶体结构](@entry_id:140373)自身的对称性会使得磁矩在某些特定方向（“[易磁化轴](@entry_id:269657)”）上具有更低的能量。这就是[磁晶各向异性](@entry_id:144488)。以最简单的**单轴各向异性**为例，其能量密度可以写为：
$$
w_K = K_u (1 - (\mathbf{m} \cdot \mathbf{e}_u)^2) \quad \text{或等价地} \quad w_K = -K_u (\mathbf{m} \cdot \mathbf{e}_u)^2 + \text{const.}
$$
其中 $K_u$ 是[各向异性常数](@entry_id:260865)，$\mathbf{e}_u$ 是易轴方向的单位矢量。通过简单的对 $\mathbf{m}$ 求导，可以得到对应的**各向异性场** ：
$$
\mathbf{H}_K = \frac{2K_u}{\mu_0 M_s} (\mathbf{m} \cdot \mathbf{e}_u) \mathbf{e}_u
$$
这个场的作用是施加一个扭矩，试图将磁矩拉向或推离易轴 $\mathbf{e}_u$。$K_u$ 的符号决定了其具体行为：
*   当 $K_u > 0$ 时，能量在 $\mathbf{m} \parallel \mathbf{e}_u$ 时最低。$\mathbf{H}_K$ 总是试图将 $\mathbf{m}$ [拉回](@entry_id:160816)与 $\mathbf{e}_u$ 平行的方向。这种情况称为**易轴各向异性**。
*   当 $K_u  0$ 时，能量在 $\mathbf{m} \perp \mathbf{e}_u$ 时最低。$\mathbf{H}_K$ 总是试图将 $\mathbf{m}$ 推向垂直于 $\mathbf{e}_u$ 的平面。这种情况称为**易面各向异性**。
我们可以通过计算能量对夹角 $\theta = \arccos(\mathbf{m} \cdot \mathbf{e}_u)$ 的[二阶导数](@entry_id:144508)来验证其稳定性：在 $\theta=0$ 处，曲率为 $2K_u$；在 $\theta=\pi/2$ 处，曲率为 $-2K_u$。曲率为正代表稳定[平衡点](@entry_id:272705)。

#### 塞曼场
当材料置于一个外部[磁场](@entry_id:153296) $\mathbf{H}_{\mathrm{ext}}$ 中时，会产生塞曼能量 $E_Z = -\int \mu_0 M_s \mathbf{H}_{\mathrm{ext}} \cdot \mathbf{m} \, dV$。其变分极其简单，对应的**塞曼场**就是外加场本身：
$$
\mathbf{H}_Z = \mathbf{H}_{\mathrm{ext}}
$$

#### 静[磁场](@entry_id:153296)（[退磁场](@entry_id:265717)）
磁化材料本身会成为一个磁源，在空间中产生一个[磁场](@entry_id:153296)。这个场反过来又会作用于材料自身，通常会增加系统的能量。这个由磁化体自身产生的场称为**静[磁场](@entry_id:153296)**或**[退磁场](@entry_id:265717)** $\mathbf{H}_d$。它由无[自由电流](@entry_id:191634)的静态麦克斯韦方程决定：
$$
\nabla \times \mathbf{H}_d = \mathbf{0} \quad \text{和} \quad \nabla \cdot \mathbf{B} = \nabla \cdot (\mu_0(\mathbf{H}_d + \mathbf{M})) = 0
$$
由于 $\mathbf{H}_d$ 是[无旋场](@entry_id:183486)，它可以表示为一个标量势 $\phi$ 的梯度：$\mathbf{H}_d = -\nabla\phi$。代入第二个方程，我们得到一个泊松方程：
$$
\nabla^2 \phi = \nabla \cdot \mathbf{M}
$$
这表明[退磁场](@entry_id:265717)的源是“磁荷”密度 $\rho_m = -\nabla \cdot \mathbf{M}$（体磁荷）和 $\sigma_m = \mathbf{M} \cdot \mathbf{n}$（面磁荷）。退磁能可写作 $E_d = -\frac{\mu_0}{2} \int \mathbf{M} \cdot \mathbf{H}_d \, dV$。通过变分可以证明，其对应的有效场就是[退磁场](@entry_id:265717)本身 ：
$$
\mathbf{H}_d^{\mathrm{eff}} = \mathbf{H}_d
$$
与之前讨论的场不同，[退磁场](@entry_id:265717)是**非局域的**。在某一点 $\mathbf{r}$ 处的 $\mathbf{H}_d$ 取决于整个材料中所有其他点 $\mathbf{r}'$ 的磁化[分布](@entry_id:182848) $\mathbf{M}(\mathbf{r}')$。在实空间中，这种关系通过一个积分核（格林函数）的卷积来表达。在傅里叶空间中，计算变得更简单，它对应于一个代数乘积：
$$
\tilde{\mathbf{H}}_d(\mathbf{k}) = - \frac{\mathbf{k}(\mathbf{k} \cdot \tilde{\mathbf{M}}(\mathbf{k}))}{k^2} = - \left(\frac{\mathbf{k}\mathbf{k}^T}{k^2}\right) \tilde{\mathbf{M}}(\mathbf{k})
$$
其中 $\mathbf{k}$ 是[波矢](@entry_id:178620)，$k=|\mathbf{k}|$。张量 $\frac{\mathbf{k}\mathbf{k}^T}{k^2}$ 是一个沿着 $\mathbf{k}$ 方向的[投影算子](@entry_id:154142)，这表明 $\mathbf{H}_d$ 在傅里叶空间中是一个[纵向场](@entry_id:264833)。静磁相互作用的长程和[非局域性](@entry_id:140165)使其成为[微磁学](@entry_id:751970)模拟中计算最复杂和耗时的部分。

#### Dzyaloshinskii-Moriya 相互作用场
Dzyaloshinskii-Moriya 相互作用（DMI）是一种反对称的交换相互作用，它源于自旋-轨道耦合，并在缺乏空间反演对称性的晶体中出现。与倾向于使磁矩平行的标准交换相互作用不同，DMI 倾向于使相邻磁矩以一定的角度倾斜，从而导致各种手性[磁结构](@entry_id:201216)（如斯格明子和螺旋磁序）的形成。

DMI 能量的数学形式取决于晶体的对称性。例如，对于具有沿 $\hat{z}$ 轴的界面破缺对称性的薄膜，其能量密度可以写为 ：
$$
w_D = D \left[ m_z (\nabla \cdot \mathbf{m}) - (\mathbf{m} \cdot \nabla) m_z \right]
$$
通过对此能量泛函进行变分，可以推导出对应的 DMI 有效场：
$$
\mathbf{H}_D = \frac{2D}{\mu_0 M_s} \left( \nabla m_z - (\nabla \cdot \mathbf{m})\hat{z} \right)
$$
另一种常见的体 DMI 形式，其能量密度为 $D \mathbf{m} \cdot (\nabla \times \mathbf{m})$，对应的有效场则为 $\mathbf{H}_D = - \frac{2D}{\mu_0 M_s} (\nabla \times \mathbf{m})$ 。这些场通常包含磁化的一阶空间导数，它们是形成非共线[磁织构](@entry_id:751636)的关键。

综上所述，总有效磁场是所有这些贡献的总和：$\mathbf{H}_{\mathrm{eff}} = \mathbf{H}_{\mathrm{ex}} + \mathbf{H}_K + \mathbf{H}_Z + \mathbf{H}_d + \mathbf{H}_D + \dots$。正是这个复杂的、通常是[非线性](@entry_id:637147)和非局域的场，驱动着 LLG 方程所描述的丰富多彩的磁化动力学。

### [自旋电子学](@entry_id:141468)扩展：自旋转移力矩

传统的磁化动力学由[磁场](@entry_id:153296)驱动，而现代自旋电子学的发展揭示了一种更有效的操控磁矩的方式——利用[自旋极化](@entry_id:164038)的电流。当自旋极化的传导电子流过一个具有非均匀[磁织构](@entry_id:751636)的区域时，传导电子的[自旋角动量](@entry_id:149719)会与局域磁矩发生交换，从而对[局域磁矩](@entry_id:138106)施加一个力矩。这就是**自旋转移力矩**（Spin-Transfer Torque, STT）。

为了描述 STT 效应，我们需要在 LLG 方程中加入额外的力矩项。这些力矩项通常被分解为**绝热**和**非绝热**两个部分 。

$$
\frac{d\mathbf{m}}{dt} = - \gamma (\mathbf{m} \times \mathbf{H}_{\mathrm{eff}}) + \alpha \left(\mathbf{m} \times \frac{d\mathbf{m}}{dt}\right) + \boldsymbol{\tau}_{\mathrm{STT}}
$$

其中，自旋转移力矩 $\boldsymbol{\tau}_{\mathrm{STT}}$ 可以表示为：
$$
\boldsymbol{\tau}_{\mathrm{STT}} = -(\mathbf{u} \cdot \nabla)\mathbf{m} + \beta \mathbf{m} \times ((\mathbf{u} \cdot \nabla)\mathbf{m})
$$

这里的各项具有明确的物理意义：
*   **绝热自旋转移力矩**：第一项 $-(\mathbf{u} \cdot \nabla)\mathbf{m}$。它描述了在传导电子自旋完美跟随局域磁矩方向（即绝热极限）的情况下，由于电子携带自旋角动量“流过”[磁织构](@entry_id:751636)而传递给[局域磁矩](@entry_id:138106)的力矩。矢量 $\mathbf{u}$ 是一个有效的自旋漂移速度，其方向与电流方向相同，大小为 $u = \frac{P \mu_B J}{e M_s}$，其中 $J$ 是[电流密度](@entry_id:190690)大小，$P$ 是电流的自旋极化率，$e$ 是[基本电荷](@entry_id:272261)。

*   **非绝热自旋转移力矩**：第二项 $\beta \mathbf{m} \times ((\mathbf{u} \cdot \nabla)\mathbf{m})$。在真实材料中，传导电子的自旋并不能完美地跟随快速变化的[磁织构](@entry_id:751636)，存在一定的“失配”。这种失配导致了额外的力矩，其强度由无量纲的**非绝热参数** $\beta$ 决定。

需要特别区分[吉尔伯特阻尼](@entry_id:749904)系数 $\alpha$ 和非绝热参数 $\beta$ 的物理来源：
*   **$\alpha$** 描述的是**局域磁矩系统本身**的固有弛豫。它量化了磁矩系统的角动量通过[自旋-轨道耦合](@entry_id:143520)等机制转移到[晶格](@entry_id:196752)等其他自由度的速率，是一种内在的能量耗散机制。
*   **$\beta$** 描述的是**输运电子（电流）**的[自旋动力学](@entry_id:146095)。它量化了[传导电子](@entry_id:145260)自旋在穿过[磁织构](@entry_id:751636)时，由于自身的自旋弛豫而未能保持与[局域磁矩](@entry_id:138106)共线的程度。

这两个参数共同决定了[电流驱动](@entry_id:186346)的[磁畴壁](@entry_id:137155)运动、磁涡旋[振荡](@entry_id:267781)和斯格明子运动等复杂动力学行为的阈值和速度。包含 STT 的增广 LLG 方程是理解和设计 MRAM、赛道存储器等自旋电子学器件的核心理论工具。