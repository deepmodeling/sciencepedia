## 引言
在量子世界中，预测一个系统如何随时间演化是理解和操控微观现象的核心。这一任务的数学基础是求解[含时薛定谔方程](@entry_id:137898)（Time-Dependent Schrödinger Equation, TDSE）。然而，当系统的[哈密顿量](@entry_id:172864)由动能和势能等互不对易的部分构成时，直接计算[时间演化算符](@entry_id:196774)会变得异常困难。这一计算瓶颈催生了对高效且精确的数值方法的需求。

分裂算符传播方法（Split-operator Propagation Method）正是应对这一挑战的基石性技术。它通过一种巧妙的分解思想，将复杂的演化问题简化为一系列易于处理的步骤，在精度和[计算效率](@entry_id:270255)之间取得了卓越的平衡。

本文将系统地引导读者全面掌握这一强大工具。在“原理与机制”一章中，我们将深入剖析该方法的数学基础和关键的数值实现细节。紧接着，“应用与跨学科联系”一章将展示其如何超越量子力学的范畴，在凝聚态物理、化学、光学等多个领域中发挥关键作用。最后，在“动手实践”一章中，读者将通过具体的编程练习，将理论知识转化为解决实际问题的能力。

## 原理与机制

在[量子动力学](@entry_id:138183)中，我们的核心任务是求解[含时薛定谔方程](@entry_id:137898)（Time-Dependent Schrödinger Equation, TDSE），以预测[量子态](@entry_id:146142)如何随[时间演化](@entry_id:153943)。对于一个由[哈密顿算符](@entry_id:144286) $\hat{H}$ 描述的系统，其形式解为 $|\psi(t+\Delta t)\rangle = \hat{U}(\Delta t)|\psi(t)\rangle$，其中 $\hat{U}(\Delta t) = \exp(-i\hat{H}\Delta t/\hbar)$ 是[时间演化算符](@entry_id:196774)。然而，将这一形式解转化为一个精确且高效的数值算法，尤其是在[哈密顿算符](@entry_id:144286)包含多个互不对易部分时，带来了重大的理论和计算挑战。本章将深入探讨分裂算符传播方法（Split-operator Propagation Method）的根本原理、核心机制及其在数值实现中的关键考量。

### [时间演化算符](@entry_id:196774)与[分裂原理](@entry_id:158035)

在许[多物理场](@entry_id:164478)景中，系统的[哈密顿量](@entry_id:172864)可以分解为[动能算符](@entry_id:265633) $\hat{T}$ 和势能算符 $\hat{V}$ 的和，即 $\hat{H} = \hat{T} + \hat{V}$。一个根本性的困难在于，[动能算符](@entry_id:265633)（在位置表象中是一个[微分](@entry_id:158718)算符）和势能算符（一个依赖于位置的乘法算符）通常是**不对易**的，即它们的对易子 $[\hat{T}, \hat{V}] \neq 0$。根据算符理论，只有当两个算符对易时，它们的和的指数才能分解为各自指数的乘积。因此，一般情况下：
$$
\exp(-i(\hat{T}+\hat{V})\Delta t/\hbar) \neq \exp(-i\hat{T}\Delta t/\hbar) \exp(-i\hat{V}\Delta t/\hbar)
$$
这种不对易性意味着我们无法通过简单地分别演化动能和[势能](@entry_id:748988)部分来精确模拟总的[演化过程](@entry_id:175749)。

分裂算符方法的核心思想是，在足够小的时间步长 $\Delta t$ 内，我们可以构造一个近似的[演化算符](@entry_id:182628)，它将总演化分解为一系列更容易计算的子步骤。最著名和最广泛使用的方案之一是**二阶对称分裂**，也称为**[斯特朗分裂](@entry_id:755497)（Strang Splitting）**。该方案将一个时间步长的演化近似为“半步势能演化-整步动能演化-半步[势能](@entry_id:748988)演化”的对称序列。

为了理解这种对称形式为何如此优越，我们可以推导其近似的阶数[@problem_id:224457]。让我们考虑一个近似[演化算符](@entry_id:182628) $\hat{U}_{\text{approx}}(\Delta t)$ 的一般对称形式：
$$
\hat{U}_{\text{approx}}(\Delta t) = \exp(-ia\hat{V}\frac{\Delta t}{\hbar})\exp(-ib\hat{T}\frac{\Delta t}{\hbar})\exp(-ia\hat{V}\frac{\Delta t}{\hbar})
$$
我们的目标是选择无量纲实系数 $a$ 和 $b$，使得 $\hat{U}_{\text{approx}}(\Delta t)$ 尽可能地逼近精确的[演化算符](@entry_id:182628) $\hat{U}(\Delta t) = \exp(-i(\hat{T}+\hat{V})\Delta t/\hbar)$。为此，我们将两个算符都对 $\Delta t$ 进行泰勒级数展开，并匹配低阶项。

精确算符的展开为：
$$
\hat{U}(\Delta t) = \mathbb{I} - \frac{i\Delta t}{\hbar}(\hat{T}+\hat{V}) - \frac{(\Delta t)^2}{2\hbar^2}(\hat{T}+\hat{V})^2 + \mathcal{O}((\Delta t)^3)
$$
$$
= \mathbb{I} - \frac{i\Delta t}{\hbar}(\hat{T}+\hat{V}) - \frac{(\Delta t)^2}{2\hbar^2}(\hat{T}^2 + \hat{V}^2 + \hat{T}\hat{V} + \hat{V}\hat{T}) + \mathcal{O}((\Delta t)^3)
$$
其中 $\mathbb{I}$ 是单位算符。

近似算符的展开为：
$$
\hat{U}_{\text{approx}}(\Delta t) = \left(\mathbb{I} - \frac{ia\Delta t}{\hbar}\hat{V} - \frac{(a\Delta t)^2}{2\hbar^2}\hat{V}^2\right) \left(\mathbb{I} - \frac{ib\Delta t}{\hbar}\hat{T} - \frac{(b\Delta t)^2}{2\hbar^2}\hat{T}^2\right) \left(\mathbb{I} - \frac{ia\Delta t}{\hbar}\hat{V} - \frac{(a\Delta t)^2}{2\hbar^2}\hat{V}^2\right) + \mathcal{O}((\Delta t)^3)
$$
将上式展开并收集至 $(\Delta t)^2$ 阶，我们得到：
$$
\hat{U}_{\text{approx}}(\Delta t) = \mathbb{I} - \frac{i\Delta t}{\hbar}(b\hat{T} + 2a\hat{V}) - \frac{(\Delta t)^2}{2\hbar^2}(b^2\hat{T}^2 + 2a^2\hat{V}^2 + 2ab(\hat{T}\hat{V} + \hat{V}\hat{T})) + \mathcal{O}((\Delta t)^3)
$$
为了使近似算符与精确算符在尽可能高的阶数上吻合，我们逐阶比较系数。
- **一阶项 ($\Delta t$)**: 比较 $- \frac{i\Delta t}{\hbar}$ 的系数，我们要求 $b\hat{T} + 2a\hat{V} = \hat{T} + \hat{V}$。这立即给出 $b=1$ 和 $2a=1$，即 $a=1/2$。
- **二阶项 ($(\Delta t)^2$)**: 将 $a=1/2$ 和 $b=1$ 代入近似算符的二阶项，得到 $- \frac{(\Delta t)^2}{2\hbar^2}(\hat{T}^2 + \frac{1}{2}\hat{V}^2 + \hat{T}\hat{V} + \hat{V}\hat{T})$。这与精确算符的二阶项 $- \frac{(\Delta t)^2}{2\hbar^2}(\hat{T}^2 + \hat{V}^2 + \hat{T}\hat{V} + \hat{V}\hat{T})$ 并不完全相同。

然而，通过更严谨的**贝克-坎贝尔-豪斯多夫（Baker-Campbell-Hausdorff, BCH）公式**分析，可以证明当 $a=1/2$ 和 $b=1$ 时，一阶和二阶的误差项都能够被精确地消除。其误差（Trotter error）的首个非零项是 $\mathcal{O}((\Delta t)^3)$ 阶的，这使得该方法对于单个时间步长是三阶准确的，而对于整个演化过程（总时间 $T = N \Delta t$）是二阶准确的。因此，我们得到了经典的**二阶对称分裂算符** $\hat{U}_{S2}(\Delta t)$：
$$
\hat{U}_{S2}(\Delta t) = \exp\left(-\frac{i}{2\hbar}\hat{V}\Delta t\right) \exp\left(-\frac{i}{\hbar}\hat{T}\Delta t\right) \exp\left(-\frac{i}{2\hbar}\hat{V}\Delta t\right)
$$
这种对称构造的巧妙之处在于，它通过对称地“三明治”动能演化步骤，有效地抵消了最低阶的对易误差。一个简单的非对称分裂，如 $\exp(-i\hat{T}\Delta t/\hbar) \exp(-i\hat{V}\Delta t/\hbar)$，其误差是 $\mathcal{O}((\Delta t)^2)$ 阶的，因此在精度上远不如对称分裂。

### 动能传播的傅里叶方法

分裂算符方法将复杂的演化问题简化为一系列更简单的子问题。对于位置表象中的[波函数](@entry_id:147440) $\psi(x)$，应用[势能](@entry_id:748988)[演化算符](@entry_id:182628) $e^{-i\hat{V}\Delta t/\hbar}$ 非常直接，因为它是一个**局域算符**，其作用等价于一个逐点相乘：
$$
\psi(x) \rightarrow \exp(-iV(x)\Delta t/\hbar) \psi(x)
$$
这个操作的计算复杂度是 $\mathcal{O}(N)$，其中 $N$ 是空间格点的数量。

然而，[动能算符](@entry_id:265633) $\hat{T} = -\frac{\hbar^2}{2m}\frac{\partial^2}{\partial x^2}$ 是一个**非局域算符**，因为它涉及[微分](@entry_id:158718)。在位置表象中直接计算它的[指数函数](@entry_id:161417)是困难的。这里的关键洞见在于切换到动量（或[波数](@entry_id:172452)）表象。[平面波](@entry_id:189798) $e^{ikx}$ 是动量算符 $\hat{p}$ 的本征函数，因此也是[动能算符](@entry_id:265633) $\hat{T}$ 的本征函数：
$$
\hat{T}e^{ikx} = \left(-\frac{\hbar^2}{2m}\frac{\partial^2}{\partial x^2}\right)e^{ikx} = \frac{\hbar^2 k^2}{2m}e^{ikx}
$$
这意味着[动能算符](@entry_id:265633)在[动量表象](@entry_id:156131)中是**对角的**，其作用仅仅是乘以一个与波数 $k$ 相关的数值（[本征值](@entry_id:154894) $E_k = \frac{\hbar^2 k^2}{2m}$）。因此，动能[演化算符](@entry_id:182628)在[动量表象](@entry_id:156131)中的作用也变得非常简单，即乘以一个依赖于 $k$ 的相位因子：
$$
\exp(-i\hat{T}\Delta t/\hbar)e^{ikx} = \exp(-iE_k\Delta t/\hbar)e^{ikx} = \exp\left(-i\frac{\hbar k^2}{2m}\Delta t\right)e^{ikx}
$$

这一性质为高效的数值实现铺平了道路[@problem_id:2822583]。我们可以采用所谓的**傅里叶方法**或**伪谱方法**来执行动能演化步骤，其算法如下：
1.  **变换到动量空间**：使用**快速傅里叶变换（Fast Fourier Transform, FFT）**将位置表象中的[波函数](@entry_id:147440) $\psi(x)$ 变换为[动量表象](@entry_id:156131)中的[波函数](@entry_id:147440) $\tilde{\psi}(k)$。
2.  **施加相位因子**：在[动量空间](@entry_id:148936)中，将每个分量 $\tilde{\psi}(k)$ 乘以对应的相位因子 $\exp(-i\frac{\hbar k^2}{2m}\Delta t)$。
3.  **变换回位置空间**：使用**逆[快速傅里叶变换](@entry_id:143432)（Inverse FFT）**将演化后的[动量表象](@entry_id:156131)[波函数](@entry_id:147440) $\tilde{\psi}'(k)$ 变换回位置表象。

[FFT算法](@entry_id:146326)的计算复杂度为 $\mathcal{O}(N\log N)$，远低于处理大型矩阵所需的 $\mathcal{O}(N^2)$ 或 $\mathcal{O}(N^3)$。因此，这种“FFT-相乘-IFFT”的三明治结构是在分裂算符框架内处理动能项的标准且高效的方案。

### 关键性质与数值赝象

尽管分裂算符傅里叶方法功能强大，但它是一种近似的数值方法，在离散化的时空网格上运行时会表现出特定的性质和潜在的陷阱。理解这些是进行可靠[量子动力学模拟](@entry_id:177535)的先决条件。

#### [幺正性](@entry_id:138773)与[能量守恒](@entry_id:140514)

分裂算符方法的一个极其重要的优点是它保持了[量子演化](@entry_id:198246)的**幺正性**。由于[势能](@entry_id:748988)算符 $\hat{V}$ 和[动能算符](@entry_id:265633) $\hat{T}$ 都是厄米算符，对应的[演化算符](@entry_id:182628) $e^{-i\hat{V}\tau}$ 和 $e^{-i\hat{T}\tau}$ 都是幺正算符。幺正算符的乘积仍然是幺正的，因此，整个分裂算符 $\hat{U}_{S2}(\Delta t)$ 也是幺正的。这意味着在演化过程中，[波函数](@entry_id:147440)的**范数** $|\psi|^2$ 是精确守恒的（在机器精度内）。这对应于量子力学中总概率守恒的基本要求。

然而，范数守恒并不意味着**[能量守恒](@entry_id:140514)**。对于一个[孤立系统](@entry_id:159201)（[哈密顿量](@entry_id:172864)不显含时间），其总[能量期望值](@entry_id:174035) $E(t)=\langle\psi(t)|\hat{H}|\psi(t)\rangle$ 在精确动力学中是一个守恒量。但在分裂算符模拟中，由于近似[演化算符](@entry_id:182628) $\hat{U}_{S2}$ 与真实[哈密顿量](@entry_id:172864) $\hat{H}$ 并不对易（即 $[\hat{U}_{S2}, \hat{H}] \neq 0$），[能量期望值](@entry_id:174035)通常不守恒。

实践中，使用对称分裂算符方法时，能量并不会无界地增加或减少，而是会在其初始值附近进行有界的、周期的[振荡](@entry_id:267781)[@problem_id:2441313]。这种行为可以理解为，数值方法实际上精确地演化了一个与真实[哈密顿量](@entry_id:172864) $\hat{H}$ 非常接近的“影子[哈密顿量](@entry_id:172864)” $\hat{H}_{\text{shadow}}$。由于 $\hat{H}_{\text{shadow}}$ 是守恒的，能量的数值误差表现为有界[振荡](@entry_id:267781)。这些[振荡](@entry_id:267781)的幅度与[分裂误差](@entry_id:755244)直接相关，并随时间步长 $\Delta t$ 的减小而减小。例如，对于一个[自由粒子](@entry_id:148748)（$V(x)=0$），$\hat{T}$ 和 $\hat{V}$ 对易，分裂是精确的，[能量守恒](@entry_id:140514)。对于[谐振子势](@entry_id:750179)（$V(x) \propto x^2$），对易子 $[\hat{T}, \hat{V}]$ 相对简单，能量[振荡](@entry_id:267781)通常很小。而对于[非谐振子](@entry_id:142760)势（例如，包含 $x^4$ 项），对易子更复杂，能量的数值不守恒性会更加明显。

#### 精度与[误差控制](@entry_id:169753)

分裂算符方法的精度由时间步长 $\Delta t$ 控制。如前所述，对称分裂的**局域误差**（单个时间步长引入的误差）是 $\mathcal{O}((\Delta t)^3)$。在总时间 $T$ 的演化中，累积的**[全局误差](@entry_id:147874)**为 $\mathcal{O}((\Delta t)^2)$。

误差的大小不仅取决于 $\Delta t$，还取决于误差项的系数，这些系数由 $\hat{T}$ 和 $\hat{V}$ 的嵌套对易子给出，例如 $[\hat{T},[\hat{T},\hat{V}]]$ 和 $[[\hat{T},\hat{V}],\hat{V}]$ [@problem_id:2441318]。这些对易子物理上与势的梯度和曲率有关。一个变化剧烈的势（大曲率）或一个具有高动能分量的[波函数](@entry_id:147440)（高动量）会导致更大的[分裂误差](@entry_id:755244)。

因此，选择一个合适的 $\Delta t$ 是一个关键的实践问题。一个基本的准则是，$\Delta t$ 必须足够小，以解析系统中所有相关的**最快时间尺度**。这些时间尺度与系统中的[能量尺度](@entry_id:196201)成反比，$\tau \sim \hbar/E$。因此，$\Delta t$ 必须远小于由以下最大能量尺度决定的时间：
$$
\Delta t \ll \frac{\hbar}{\max\{E_{k,\max}, V_{\max}, \hbar\omega_{\text{curv}}\}}
$$
其中 $E_{k,\max}$ 是[波函数](@entry_id:147440)在网格上具有的最高动能， $V_{\max}$ 是势能的最大值，而 $\hbar\omega_{\text{curv}}$ 是与势的曲率相关的特征能量。违反此条件不会导致模拟不稳定（因为方法是幺正的），但会导致精度严重下降，模拟结果将与真实物理过程大相径庭。

#### [空间离散化](@entry_id:172158)与混叠

将[波函数](@entry_id:147440)表示在有限的空间网格上会引入另一类关键的数值赝象，称为**混叠（Aliasing）**。根据**奈奎斯特-香农采样定理**，一个空间格点间距为 $\Delta x$ 的网格，只能无歧义地表示[波数](@entry_id:172452)（[空间频率](@entry_id:270500)）在 $[-k_{\text{Ny}}, k_{\text{Ny}})$ 范围内的分量，其中**奈奎斯特波数** $k_{\text{Ny}} = \pi/\Delta x$ [@problem_id:2822583]。

如果真实的[连续波函数](@entry_id:269248)包含的波数分量 $|k|$ 超出了这个范围（$|k| > k_{\text{Ny}}$），那么在离散采样时，这些高频分量将被错误地“折叠”或“[混叠](@entry_id:146322)”到可表示的频率范围内。例如，一个波数为 $k_0 > k_{\text{Ny}}$ 的分量可能会被表示为一个[波数](@entry_id:172452)为 $k_{\text{alias}} = k_0 - 2k_{\text{Ny}}$ 的分量。

这种效应在[量子动力学模拟](@entry_id:177535)中有直接的物理后果。考虑一个初始具有较高中心动量 $\hbar k_0$ 的[高斯波包](@entry_id:151158)[@problem_id:2441358]。在精确的[自由粒子](@entry_id:148748)动力学中，其群速度为 $v_g = \hbar k_0/m$。但是，如果 $k_0 > k_{\text{Ny}}$，[数值模拟](@entry_id:137087)将把[波包](@entry_id:154698)的中心[波数](@entry_id:172452)误解为 $k_{\text{alias}}$。因此，模拟出的[波包](@entry_id:154698)将以错误的[群速度](@entry_id:147686) $v_g' = \hbar k_{\text{alias}}/m$ 运动，导致其位置随时间的演化完全错误。

混叠不仅可能在初始状态设置时发生，也可能在动力学[演化过程](@entry_id:175749)中动态出现[@problem_id:2441310]。例如，一个粒子在恒定[力场](@entry_id:147325)（[线性势](@entry_id:160860) $V(x) = -Fx$）中运动。根据[埃伦费斯特定理](@entry_id:151868)，其动量[期望值](@entry_id:153208)将随时间线性增加：$\langle p(t) \rangle = \langle p(0) \rangle + Ft$。即使初始动量远低于奈奎斯特极限，随着时间的推移，粒子被加速，其动量谱向高动量移动。一旦动量谱的显著部分超过了 $k_{\text{Ny}}$，它就会从动量空间的一端（例如 $+k_{\text{Ny}}$）“绕回”到另一端（$-k_{\text{Ny}}$）。这在动量[期望值](@entry_id:153208)的演化曲线上表现为一次突然的、非物理性的“反射”，表明模拟已经因为[混叠](@entry_id:146322)而失效。

#### 边界条件与对称性

傅里叶方法的一个固有特性是它隐含了**周期性边界条件**。这意味着任何到达模拟区域一端的[波函数](@entry_id:147440)部分，都会立即从另一端重新进入。这种“绕回”（wrap-around）效应本身不是混叠，但同样是一种需要警惕的数值赝象[@problem_id:2822583]。如果模拟的是一个在无界空间中运动的波包，必须确保模拟盒子足够大，以至于在整个模拟时间内，[波函数](@entry_id:147440)的显著部分不会到达边界。否则，绕回的[波函数](@entry_id:147440)会干扰主体，污染[物理可观测量](@entry_id:154692)。处理这个问题的方法包括使用更大的模拟盒子或在边界附近引入**复吸收势（Complex Absorbing Potentials, CAPs）**来吸收外传的[波函数](@entry_id:147440)。

此外，数值方案是否能保持物理系统的对称性，是衡量其好坏的重要标准。考虑一个在偶[对称势](@entry_id:148561) $V(x)=V(-x)$ 中运动的粒子。如果初始状态是反对称的（$\psi(x,0) = -\psi(-x,0)$），那么在精确的[量子动力学](@entry_id:138183)下，由于[哈密顿量](@entry_id:172864)与[宇称算符](@entry_id:148434) $\hat{P}$ 对易，[波函数](@entry_id:147440)将在所有时间保持[反对称性](@entry_id:261893)。然而，这种对称性在[数值模拟](@entry_id:137087)中能否保持，取决于离散化方案是否也尊重这种对称性[@problem_id:2441292]。如果空间网格关于 $x=0$ 对称（例如，$x_j = (j - N/2)\Delta x$），那么[傅里叶变换](@entry_id:142120)本身会保持函数的宇称性（将反[对称函数](@entry_id:177113)映射为反[对称函数](@entry_id:177113)）。由于动能和[势能](@entry_id:748988)演化步骤在这种情况下也都保持宇称性，整个分裂算符步骤将保持[波函数](@entry_id:147440)的[反对称性](@entry_id:261893)（在机器精度内）。反之，如果使用一个非对称的网格（例如，$x_j = j\Delta x$ for $j=0, \dots, N-1$），离散傅里叶变换的[基函数](@entry_id:170178)本身不具有确定的宇称性，这会导致动能演化步骤破坏[波函数](@entry_id:147440)的对称性。这揭示了一个深刻的原则：数值算法的设计必须与待解决问题的物理对称性相兼容。

### 扩展到更复杂的系统

分裂算符方法的优雅和强大之处在于其模块化的结构，这使其能够灵活地扩展以处理更复杂的物理情况。

#### 显[含时哈密顿量](@entry_id:136684)

当[势能](@entry_id:748988)明确依赖于时间，即 $\hat{H}(t) = \hat{T} + \hat{V}(x,t)$ 时，系统的能量不再守恒。其变化率由[埃伦费斯特定理](@entry_id:151868)的一个推广给出：$d\langle \hat{H} \rangle/dt = \langle \partial \hat{H}/\partial t \rangle$ [@problem_id:2441348]。为了在数值上处理这种情况，我们需要对分裂算符方案进行微调。一个保持二阶精度的标准做法是在每个时间步长的**中点**评估[势能](@entry_id:748988)。一个常用的形式是
$$
\hat{U}(t, \Delta t) \approx \exp\left(-\frac{i}{2\hbar}\hat{V}(x, t+\frac{\Delta t}{2})\Delta t\right) \exp\left(-\frac{i}{\hbar}\hat{T}\Delta t\right) \exp\left(-\frac{i}{2\hbar}\hat{V}(x, t+\frac{\Delta t}{2})\Delta t\right)
$$
一个可靠的[数值模拟](@entry_id:137087)应该能够准确地追踪这种物理上的能量变化，同时其固有的数值误差（即能量[振荡](@entry_id:267781)）叠加在这种物理趋势之上。

#### 非厄米[哈密顿量](@entry_id:172864)与[开放系统](@entry_id:147845)

在许多物理问题中，如描述粒子吸收、衰变或与环境相互作用的[开放量子系统](@entry_id:138632)，[哈密顿量](@entry_id:172864)不再是厄米的。一个常见的模型是引入一个**[复势](@entry_id:162103)**，例如 $V(x) = V_R(x) - iV_I(x)$，其中 $V_I(x) > 0$ 表示吸收。对于一个非厄米[哈密顿量](@entry_id:172864) $\hat{H} \neq \hat{H}^\dagger$，波[函数的范数](@entry_id:275551)不再守恒。其变化率由下式给出：
$$
\frac{dN(t)}{dt} = \frac{i}{\hbar}\langle\psi|(\hat{H}^\dagger - \hat{H})|\psi\rangle = \frac{2}{\hbar}\langle\psi|\text{Im}(\hat{H})|\psi\rangle
$$
对于一个空间均匀的[复势](@entry_id:162103) $V(x) = V_0 - i\Gamma$（其中 $\Gamma$ 是正常数），范数将随时间指数衰减：$N(t) = N(0)e^{-2\Gamma t/\hbar}$ [@problem_id:2441355]。

分裂算符方法可以毫无障碍地应用于非厄米系统。势能[演化算符](@entry_id:182628) $e^{-i(V_0-i\Gamma)\Delta t/\hbar}$ 现在包含一个实部 $e^{-\Gamma\Delta t/\hbar}$，它会直接改变[波函数](@entry_id:147440)的模长。动能演化步骤仍然是幺正的。整个分裂算符步骤不再是幺正的，但它能准确地模拟由非厄米[哈密顿量](@entry_id:172864)引起的物理范数变化。一个好的模拟将显示出与解析预测相符的范数衰减，其间的微小差异仅由[分裂误差](@entry_id:755244)引起。

#### 非局域势

标准的分裂算符傅里叶方法依赖于[势能](@entry_id:748988)算符在位置表象中是对角的这一事实。然而，在某些理论中，例如 Hartree-Fock 理论，会出现**非局域势**。其作用由一个积分核 $W(x,x')$ 定义：
$$
(\hat{V}\psi)(x) = \int W(x,x')\psi(x')dx'
$$
在离散化的网格上，该算符对应于一个通常是稠密的矩阵 $\mathbf{V}$，而不再是[对角矩阵](@entry_id:637782)。因此，计算势能[演化算符](@entry_id:182628) $e^{-i\mathbf{V}\Delta t/\hbar}$ 及其对[波函数](@entry_id:147440)向量的作用成为一个计算瓶颈。直接计算[稠密矩阵](@entry_id:174457)的[指数函数](@entry_id:161417)是不可行的。

一个先进且高效的解决方案是，在保持分裂算符结构的同时，使用**[克雷洛夫子空间](@entry_id:751067)（Krylov subspace）**方法来近似计算矩阵指数乘以向量的作用，即 $e^{\mathbf{A}}\vec{v}$ [@problem_id:2441312]。像**Lanczos**或**Arnoldi**这样的算法，通过构建一个由 $\{\vec{v}, \mathbf{A}\vec{v}, \mathbf{A}^2\vec{v}, \dots\}$ 张成的低维[子空间](@entry_id:150286)，能够以远低于直接计算矩阵指数的成本，高精度地计算出结果。这种方法将动能步的FFT效率与处理复杂非局域相互作用的强大[数值线性代数](@entry_id:144418)技术相结合，极大地扩展了分裂算符方法的应用范围。