## 引言
当电流穿过真空时，它产生的[磁场](@entry_id:153296)可以通过[安培定律](@entry_id:140092)精确描述。然而，现实世界中的大多数电磁设备都包含各种材料，从电线周围的绝缘体到变压器和电机中的铁芯。这些材料自身并非被动的，它们会在外部[磁场](@entry_id:153296)的作用下被磁化，从而成为新的[磁场源](@entry_id:267241)，使得问题变得异常复杂。如何修正安培定律以系统性地处理这种由材料磁化带来的额外贡献，是[静磁学](@entry_id:140120)中的一个核心知识缺口。

本文旨在填补这一缺口，为读者提供一套完整的理论工具来分析磁化物质中的静[磁场](@entry_id:153296)。通过学习本文，你将：

在“原理与机制”一章中，深入理解磁化强度和束缚电流的物理图像，并掌握关键的辅助场 $\vec{H}$ 的定义，它能巧妙地将我们关心的[自由电流](@entry_id:191634)从复杂的材料响应中分离出来。

在“应用与跨学科联系”一章中，看到这些原理如何应用于电机工程和[材料科学](@entry_id:152226)的实际问题中，例如增强[螺线管磁场](@entry_id:264987)、设计[磁路](@entry_id:268480)与气隙，以及实现[磁屏蔽](@entry_id:192877)。

最后，在“动手实践”部分，通过解决具体问题来巩固所学知识，将理论转化为解决实际计算的能力。

让我们首先进入第一章，揭示在磁介质内部，安培定律是如何以一种更强大、更通用的形式呈现的。

## 原理与机制

在上一章中，我们探讨了真空中的[磁场](@entry_id:153296)是如何由电流产生的。然而，当我们引入物质时，情况会变得更加复杂。材料本身会对外部[磁场](@entry_id:153296)做出响应，产生自身的磁化现象，而这种磁化又会成为[磁场](@entry_id:153296)的一个新来源。本章旨在系统地阐述如何处理存在磁介质时的[静磁学](@entry_id:140120)问题。我们将引入束缚电流的概念来描述材料的磁响应，并定义一个[辅助场](@entry_id:155519) $\vec{H}$ 来简化安培环路定律，最终掌握在各种实际场景中计算[磁场](@entry_id:153296)的方法。

### 磁化与束缚电流

当材料被置于[磁场](@entry_id:153296)中时，其内部的原子或分子会响应。这种响应可以表现为原有分子磁矩的取向[排列](@entry_id:136432)（[顺磁性](@entry_id:139883)），或是感生出方向相反的磁矩（[抗磁性](@entry_id:148741)）。在宏观尺度上，我们将这种集体效应描述为材料被**磁化**了。我们定义**磁化强度 (Magnetization)** $\vec{M}$ 为单位体积内的净[磁偶极矩](@entry_id:158175)。这是一个矢量场，描述了在材料中每一点的磁化程度和方向。在[国际单位制](@entry_id:172547)（SI）中，磁偶极矩的单位是安培·米²（$\mathrm{A \cdot m^2}$），因此磁化强度 $\vec{M}$ 的单位是安培/米（$\mathrm{A/m}$）[@problem_id:2504872]。

磁化的核心物理图像是，它等效于在材料内部和表面产生了宏观的电流[分布](@entry_id:182848)。这些电流并非由[自由电荷](@entry_id:264392)的传导产生，而是源于原子尺度的磁矩在空间上的变化，因此被称为**束缚电流 (bound currents)**。

我们可以将束缚电流分为两类：

1.  **[束缚体电流](@entry_id:266207)密度 (Bound Volume Current Density)** $\vec{J}_b$：当磁化强度在材料内部不均匀时，相邻微元体之间的原子环流无法完全抵消，从而在宏观上形成净电流。可以证明，[束缚体电流](@entry_id:266207)密度与[磁化强度的旋度](@entry_id:276904)成正比：

    $$ \vec{J}_b = \nabla \times \vec{M} $$

    这个关系意味着，只有当磁化强度在空间中发生“卷曲”或变化时，才会产生[束缚体电流](@entry_id:266207)。一个直接的推论是，如果一种材料内的磁化强度场是无旋的，即 $\nabla \times \vec{M} = 0$，那么其内部将不存在[束缚体电流](@entry_id:266207)。均匀磁化（$\vec{M}$ 为常矢量）是这种情况的一个特例，但并非唯一情况 [@problem_id:1568135]。

    为了更具体地理解这一点，考虑一个磁化强度由 $\vec{M}(x, y, z) = k y^2 \hat{x} - k x^2 \hat{y}$ 描述的材料。通过计算其旋度，我们可以得到[束缚体电流](@entry_id:266207)密度 [@problem_id:1565042]：
    $$ \vec{J}_b = \nabla \times \vec{M} = \left( \frac{\partial M_z}{\partial y} - \frac{\partial M_y}{\partial z} \right)\hat{x} + \left( \frac{\partial M_x}{\partial z} - \frac{\partial M_z}{\partial x} \right)\hat{y} + \left( \frac{\partial M_y}{\partial x} - \frac{\partial M_x}{\partial y} \right)\hat{z} $$
    $$ \vec{J}_b = \left( \frac{\partial (-kx^2)}{\partial x} - \frac{\partial (ky^2)}{\partial y} \right)\hat{z} = (-2kx - 2ky)\hat{z} = -2k(x+y)\hat{z} $$
    在这个例子中，非均匀的[磁化场](@entry_id:197918)导致了空间依赖的束缚电流。

    另一个有趣的例子是[磁化场](@entry_id:197918)呈现旋转模式，例如 $\vec{M} = k(y\hat{x} - x\hat{y})$。尽管磁化强度的大小 $| \vec{M} | = k\sqrt{y^2+x^2}$ 随半径变化，但其旋度却是一个常数 [@problem_id:1565066]：
    $$ \vec{J}_b = \nabla \times \vec{M} = \left( \frac{\partial (-kx)}{\partial x} - \frac{\partial (ky)}{\partial y} \right)\hat{z} = (-k - k)\hat{z} = -2k\hat{z} $$
    这表明一个类似涡旋的磁化[分布](@entry_id:182848)可以在材料内部产生均匀的束缚电流。

2.  **束缚面[电流密度](@entry_id:190690) (Bound Surface Current Density)** $\vec{K}_b$：在磁化材料的表面，原子环流不再有邻近的环流来抵消，因此在宏观上表现为在表面流动的电流。束缚面电流密度由磁化强度在边界处的切向分量决定：

    $$ \vec{K}_b = \vec{M} \times \hat{n} $$

    其中 $\hat{n}$ 是指向材料外部的[单位法向量](@entry_id:178851)。例如，一个沿着轴向均匀磁化的圆柱体，其侧面就会有环形的束缚面电流，就像一个[螺线管](@entry_id:261182)。

### [辅助场](@entry_id:155519) $\vec{H}$ 与介质中的[安培环路定律](@entry_id:140092)

在[静磁学](@entry_id:140120)中，总的[磁感应强度](@entry_id:144179) $\vec{B}$ 由所有电流产生，包括我们能直接控制的**[自由电流](@entry_id:191634) (free currents)** $\vec{J}_f$（例如导线中的电流）和材料响应产生的束缚电流 $\vec{J}_b$。因此，安培环路定律的微分形式应写作：
$$ \nabla \times \vec{B} = \mu_0 (\vec{J}_f + \vec{J}_b) $$

这个方程虽然精确，但在实际应用中却不方便，因为束缚电流 $\vec{J}_b$ 通常是未知的，它本身是场作用于材料的结果。为了解决这个难题，我们引入一个辅助的矢量场，其源仅为我们通常已知的[自由电流](@entry_id:191634)。

将 $\vec{J}_b = \nabla \times \vec{M}$ 代入上式：
$$ \nabla \times \vec{B} = \mu_0 (\vec{J}_f + \nabla \times \vec{M}) $$

移项并除以 $\mu_0$：
$$ \nabla \times \left( \frac{\vec{B}}{\mu_0} - \vec{M} \right) = \vec{J}_f $$

这启发我们定义一个新的矢量场，即**[磁场强度](@entry_id:197932) (Magnetic Field Strength)** $\vec{H}$：
$$ \vec{H} \equiv \frac{\vec{B}}{\mu_0} - \vec{M} $$

这个定义是处理磁介质问题的关键一步。$\vec{B}$ 和 $\vec{H}$ 都描述[磁场](@entry_id:153296)，但它们的物理意义和单位不同。$\vec{B}$ 称为**[磁感应强度](@entry_id:144179) (Magnetic Flux Density)**，单位是特斯拉（$\mathrm{T}$），它是在[洛伦兹力](@entry_id:145104)公式中出现的那个基本场。$\vec{H}$ 的单位与 $\vec{M}$ 相同，是安培/米（$\mathrm{A/m}$）[@problem_id:2504872]。

通过定义 $\vec{H}$ 场，安培环路定律被改写成一个更简洁、更实用的形式，即**介质中的[安培环路定律](@entry_id:140092)**：
$$ \nabla \times \vec{H} = \vec{J}_f $$

其积分形式为：
$$ \oint \vec{H} \cdot d\vec{l} = I_{f, \text{enc}} $$

这个定律的巨大优势在于，$\vec{H}$ 场的[环路积分](@entry_id:164828)只与闭合路径所包围的**[自由电流](@entry_id:191634)** $I_{f, \text{enc}}$ 有关。材料复杂的磁化响应（即束缚电流）被巧妙地包含在了 $\vec{H}$ 场的定义之中。因此，只要系统的几何结构具有足够的对称性，即使存在磁介质，我们也可以像在真空中一样使用[安培环路定律](@entry_id:140092)来求解 $\vec{H}$ 场，只要我们知道[自由电流](@entry_id:191634)的[分布](@entry_id:182848)。

### 线性介质与[本构关系](@entry_id:186508)

虽然 $\vec{H}$ 场的引入简化了[安培定律](@entry_id:140092)，但我们还需要一个联系 $\vec{B}$，$\vec{H}$ 和 $\vec{M}$ 的方程才能最终确定[磁场](@entry_id:153296)。我们已经有了定义式 $\vec{B} = \mu_0(\vec{H} + \vec{M})$。现在还需要一个描述材料如何响应[磁场](@entry_id:153296)的**本构关系 (constitutive relation)**。

对于许多材料，在不是特别强的[磁场](@entry_id:153296)下，其磁化强度 $\vec{M}$ 与磁场强度 $\vec{H}$ 成正比。这类材料被称为**[线性磁介质](@entry_id:274072) (linear magnetic media)**。对于线性、各向同性、均匀（LIH）的介质，[本构关系](@entry_id:186508)可以写成：
$$ \vec{M} = \chi_m \vec{H} $$

这里的比例常数 $\chi_m$ 被称为**磁化率 (Magnetic Susceptibility)**，它是一个无量纲的纯数，衡量了材料被磁化的难易程度 [@problem_id:2504872]。
*   如果 $\chi_m > 0$，材料是**[顺磁性](@entry_id:139883) (paramagnetic)** 的。其内部磁矩倾向于与外场同向[排列](@entry_id:136432)，从而增强总[磁场](@entry_id:153296)。
*   如果 $\chi_m < 0$，材料是**抗磁性 (diamagnetic)** 的。其感生磁矩与外场反向，从而削弱总[磁场](@entry_id:153296)。大多数物质都具有[抗磁性](@entry_id:148741)，但效应通常很弱。

将此本构关系代入 $\vec{B}$ 和 $\vec{H}$ 的定义式，我们得到：
$$ \vec{B} = \mu_0(\vec{H} + \vec{M}) = \mu_0(\vec{H} + \chi_m \vec{H}) = \mu_0(1 + \chi_m)\vec{H} $$

我们通常将上式写成更简洁的形式：
$$ \vec{B} = \mu \vec{H} $$

其中 $\mu = \mu_0(1 + \chi_m)$ 被称为材料的**磁导率 (permeability)**。我们还常定义**[相对磁导率](@entry_id:272081) (relative permeability)** $\mu_r = 1 + \chi_m$，于是 $\mu = \mu_r \mu_0$。对于真空，$\chi_m=0$，$\mu_r=1$，$\mu=\mu_0$。

### 应用与实例

掌握了 $\vec{H}$ 场、安培定律和线性介质的本构关系后，我们就有了一套强大的工具来解决涉及磁介质的[静磁学](@entry_id:140120)问题。其基本策略是：
1.  利用对称性和安培定律 $\oint \vec{H} \cdot d\vec{l} = I_{f, \text{enc}}$ 求出由[自由电流](@entry_id:191634)决定的 $\vec{H}$ 场。
2.  利用[本构关系](@entry_id:186508) $\vec{B} = \mu \vec{H}$ 和 $\vec{M} = \chi_m \vec{H}$ 求出 $\vec{B}$ 场和磁化强度 $\vec{M}$。

#### 长[螺线管](@entry_id:261182)

考虑一个单位长度匝数为 $n$ 的无限长螺线管，通有[自由电流](@entry_id:191634) $I_f$。
1.  **求解 $\vec{H}$**：在[螺线管](@entry_id:261182)内部取一个长为 $L$ 的矩形[安培环路](@entry_id:275261)，根据 $\oint \vec{H} \cdot d\vec{l} = I_{f, \text{enc}}$，我们得到 $H \cdot L = nL \cdot I_f$，因此在[螺线管](@entry_id:261182)内部（远离端点处），$\vec{H}$ 场的大小为：
    $$ H = n I_f $$
    这是一个非常重要的结论：只要[自由电流](@entry_id:191634) $I_f$ 不变，无论螺线管内部填充的是真空还是任何[线性磁介质](@entry_id:274072)，$\vec{H}$ 场都保持不变 [@problem_id:1784418]。$\vec{H}$ 场只“感受”[自由电流](@entry_id:191634)。

2.  **求解 $\vec{B}$ 和 $\vec{M}$**：当螺线管内部填充[磁化率](@entry_id:138219)为 $\chi_m$ 的线性介质时，[磁感应强度](@entry_id:144179) $\vec{B}$ 和磁化强度 $\vec{M}$ 分别为：
    $$ B = \mu H = \mu_0(1+\chi_m)H = \mu_0(1+\chi_m)nI_f $$
    $$ M = \chi_m H = \chi_m nI_f $$
    可见，插入顺[磁性材料](@entry_id:137953)（$\chi_m > 0$）会使得总的[磁感应强度](@entry_id:144179) $\vec{B}$ 增大 $(1+\chi_m)$ 倍。

3.  **场的分解与物理诠释**：总场 $\vec{B}$ 可以看作是[自由电流](@entry_id:191634)产生的场 $\vec{B}_{free}$ 和束缚电流产生的场 $\vec{B}_{bound}$ 的叠加。从 $\vec{B} = \mu_0(\vec{H} + \vec{M})$ 的结构中，我们可以自然地做出如下对应：
    $$ \vec{B}_{free} = \mu_0 \vec{H} $$
    $$ \vec{B}_{bound} = \mu_0 \vec{M} $$
    因此，束缚电流贡献的场与[自由电流](@entry_id:191634)贡献的场的大小之比为：
    $$ \frac{|\vec{B}_{bound}|}{|\vec{B}_{free}|} = \frac{\mu_0 M}{\mu_0 H} = \frac{M}{H} = \chi_m $$
    这个结果为[磁化率](@entry_id:138219) $\chi_m$ 提供了一个清晰的物理图像：它直接衡量了材料的磁响应（由束缚电流体现）与外部驱动（由[自由电流](@entry_id:191634)体现）的相对强度。例如，铝的磁化率约为 $\chi_m = 2.2 \times 10^{-5}$，这意味着在铝芯螺线管中，由材料磁化贡献的磁场强度大约是[自由电流](@entry_id:191634)贡献的[磁场强度](@entry_id:197932)的 $2.2 \times 10^{-5}$ 倍 [@problem_id:1565085]。同时，总[磁场](@entry_id:153296)与磁化强度的比值为 $\frac{B}{M} = \frac{\mu_0(1+\chi_m)H}{\chi_m H} = \frac{\mu_0(1+\chi_m)}{\chi_m}$ [@problem_id:1784418]。

#### 环形[螺线管](@entry_id:261182)

对于一个总匝数为 $N$、通有电流 $I$ 的环形[螺线管](@entry_id:261182)（或称环形[电感](@entry_id:276031)），其芯材为磁化率为 $\chi_m$ 的线性介质。
1.  **求解 $\vec{H}$**：取一条沿环芯中心线、半径为 $s$ 的圆形[安培环路](@entry_id:275261)。该环路包围的总[自由电流](@entry_id:191634)为 $I_{f, enc} = NI$。根据安培定律，我们有 $H \cdot (2\pi s) = NI$，因此：
    $$ H = \frac{NI}{2\pi s} $$

2.  **计算束缚电流**：我们现在可以反过来验证束缚电流的概念。总的[磁感应强度](@entry_id:144179) $B = \mu_0(1+\chi_m)H = \mu_0(1+\chi_m)\frac{NI}{2\pi s}$。根据包含所有电流的原始[安培定律](@entry_id:140092) $\oint \vec{B} \cdot d\vec{l} = \mu_0(I_{f, enc} + I_{b, enc})$，我们计算左侧的[环路积分](@entry_id:164828)：
    $$ \oint \vec{B} \cdot d\vec{l} = B \cdot (2\pi s) = \mu_0(1+\chi_m)NI $$
    与右侧比较，$\mu_0(1+\chi_m)NI = \mu_0(NI + I_{b, enc})$，可以解得总的等效束缚电流为：
    $$ I_{b, enc} = \chi_m NI = \chi_m I_{f, enc} $$
    这个结果 [@problem_id:1805598] 优美地展示了整个理论框架的[自洽性](@entry_id:160889)：由材料磁化产生的束缚电流，其总大小等于[自由电流](@entry_id:191634)乘以[磁化率](@entry_id:138219)。

#### 具有“冻结”磁化的圆柱体

考虑一个半径为 $R$ 的无限长圆柱体，其内部具有固定的、非均匀的“冻结”磁化 $\vec{M} = \alpha r^2 \hat{z}$（$r \le R$），其中 $\alpha$ 是常数，且无任何[自由电流](@entry_id:191634)。求解圆柱体内部的[磁场](@entry_id:153296) $\vec{B}$。这个问题可以通过两种截然不同的方法解决，从而凸显 $\vec{H}$ 场的威力 [@problem_id:1565103]。

*   **方法一：直接计算束缚电流**
    首先计算束缚电流。[体电流密度](@entry_id:268648)为 $\vec{J}_b = \nabla \times \vec{M} = -\frac{\partial M_z}{\partial r} \hat{\phi} = -2\alpha r \hat{\phi}$。[表面电流密度](@entry_id:274967)为 $\vec{K}_b = \vec{M}|_{r=R} \times \hat{r} = \alpha R^2 \hat{z} \times \hat{r} = \alpha R^2 \hat{\phi}$。然后利用[安培定律](@entry_id:140092) $\nabla \times \vec{B} = \mu_0 \vec{J}_b$ 来求解 $\vec{B}$。这是一个更繁琐的过程，需要积分并利用边界条件来确定积分常数。

*   **方法二：利用 $\vec{H}$ 场**
    注意到系统中没有[自由电流](@entry_id:191634)，即 $I_f = 0$。因此，根据介质中的安培定律，$\oint \vec{H} \cdot d\vec{l} = 0$ 对任意闭合路径都成立。这在微分形式上意味着 $\nabla \times \vec{H} = 0$。对于这个具有高度对称性的系统，可以推断 $\vec{H}$ 场在所有地方都为零（因为在无穷远处 $\vec{H}$ 必须为零）。既然 $\vec{H} = 0$，我们可以直接使用定义式来求 $\vec{B}$：
    $$ \vec{B} = \mu_0(\vec{H} + \vec{M}) = \mu_0(0 + \vec{M}) = \mu_0 \alpha r^2 \hat{z} $$
    这种方法极其简洁，充分展示了当[自由电流](@entry_id:191634)为零或[分布](@entry_id:182848)简单时，首先求解 $\vec{H}$ 场是多么明智的策略。

### [磁场](@entry_id:153296)的边值关系

当[磁场](@entry_id:153296)从一种介质进入另一种介质时，场线会发生变化。这些变化由一组边界条件决定，它们可以从麦克斯韦方程的积分形式导出。

1.  从[高斯磁定律](@entry_id:182942) $\nabla \cdot \vec{B} = 0$ 可推导出，穿过任意闭合[曲面](@entry_id:267450)的磁通量为零。在两种介质的交界面上取一个小的“药盒”形[高斯面](@entry_id:272964)，可以得到：
    $$ B_{1\perp} = B_{2\perp} $$
    即[磁感应强度](@entry_id:144179) $\vec{B}$ 的法向分量在界面上是连续的。

2.  从介质中的安培定律 $\nabla \times \vec{H} = \vec{J}_f$ 可推导出 $\vec{H}$ 场的[环路积分](@entry_id:164828)。在界面上取一个窄长的矩形[安培环路](@entry_id:275261)，可以得到：
    $$ \vec{H}_{2\parallel} - \vec{H}_{1\parallel} = \vec{K}_f \times \hat{n} $$
    其中 $\vec{K}_f$ 是界面上的自由面[电流密度](@entry_id:190690)。这表明，磁场强度 $\vec{H}$ 的切向分量的改变量取决于垂直于它的自由面电流。

在一个常见且重要的情况下，界面上没有自由面电流（$\vec{K}_f = 0$）。此时，边界条件简化为：
$$ B_{1\perp} = B_{2\perp} \quad \text{和} \quad H_{1\parallel} = H_{2\parallel} $$

考虑一个位于[磁导率](@entry_id:154559)为 $\mu_1 = \mu_r \mu_0$ 的介质和真空（$\mu_2 = \mu_0$）之间的平直界面。假设场线在介质中与法线的夹角为 $\theta_1$，在真空中为 $\theta_2$。
根据边界条件：
$$ B_1 \cos\theta_1 = B_2 \cos\theta_2 $$
$$ H_1 \sin\theta_1 = H_2 \sin\theta_2 $$

利用本构关系 $B_1 = \mu_1 H_1$ 和 $B_2 = \mu_2 H_2$，第二个方程可以改写为：
$$ \frac{B_1}{\mu_1} \sin\theta_1 = \frac{B_2}{\mu_2} \sin\theta_2 $$

将此式与第一个边界条件相除，可以消去 $B_1$ 和 $B_2$，得到[磁场](@entry_id:153296)线的“[折射定律](@entry_id:165991)”：
$$ \frac{\tan\theta_1}{\mu_1} = \frac{\tan\theta_2}{\mu_2} \implies \tan\theta_2 = \frac{\mu_2}{\mu_1} \tan\theta_1 $$

对于从介质到真空的情况，$\mu_1 = \mu_r \mu_0$ 且 $\mu_2 = \mu_0$，因此：
$$ \tan\theta_2 = \frac{1}{\mu_r} \tan\theta_1 $$
解出 $\theta_2$ 得到 $\theta_2 = \arctan\left(\frac{1}{\mu_r}\tan\theta_1\right)$ [@problem_id:1565102]。由于对于顺磁和[铁磁材料](@entry_id:261099) $\mu_r > 1$，这意味着[磁场](@entry_id:153296)线从磁介质进入真空时，会以更大的角度“[折射](@entry_id:163428)”出去，即更偏离法线方向。