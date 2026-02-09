## 引言
在宇宙学中，功率谱和双谱是描述宇宙大尺度结构统计特性的基石。它们如同宇宙的“指纹”，将关于早期宇宙、引力演化和宇宙组分的关键信息编码在物质密度场的空间关联之中。理论模型能够精确预测这些统计量，但要将理论与真实宇宙进行比较，我们必须面对一个根本性挑战：理论处理的是理想化的连续、无限场，而我们的数据——无论是来自大规模数值模拟还是星系巡天观测——本质上都是离散、有限且受系统误差污染的。

本文旨在系统性地解决这一知识鸿沟，为读者提供一套从离散场中精确估计功率谱和双谱的完整框架。我们将深入探讨如何从充满复杂性的实际数据中，可靠地提取出蕴含深刻物理意义的统计信号。

在接下来的章节中，我们将踏上一段从理论到实践的旅程：
*   **第一章：原理与机制** 将奠定理论基础，阐明如何将连续空间的傅里叶分析转译到周期性、离散的网格上。我们将详细推导功率谱和双谱的估计量，并揭示质量分配、傅里叶变换归一化等关键步骤背后的物理原理，同时深入剖析如散粒噪声、混叠效应等不可避免的系统误差。
*   **第二章：应用与跨学科关联** 将展示这些估计技术在解决前沿科学问题中的强大威力。我们将探讨如何利用它们测量红移空间畸变以检验引力理论，如何通过双谱约束基础物理模型，并揭示该领域与统计信号处理、计算机科学等学科的深刻交叉。
*   **第三章：动手实践** 将通过一系列精心设计的计算练习，将理论知识转化为实践技能。读者将亲手实现对傅里叶模式的计数、理解宇宙方差的来源，并处理带权重的示踪体所产生的散粒噪声。

通过学习本章内容，您将不仅掌握功率谱和双谱估计的核心技术，还将深刻理解连接理论预测与实际数据分析的完整逻辑链条。

## 原理与机制

在宇宙学研究中，理论模型预测了宇宙物质密度场的统计特性，而这些特性蕴含在多点相关函数及其傅里叶对偶——功率谱和更高阶的多体谱（如双谱）之中。然而，观测和数值模拟所提供的数据是离散的、有限体积的，并且受到各种系统效应的影响。本章旨在系统地阐述从离散密度场中估计功率谱和双谱的基本原理与关键机制，为连接理论预测与实际数据分析搭建桥梁。我们将从傅里叶空间的基本定义出发，逐步引入估计量的构建方法，并深入探讨在实际操作中必须面对和校正的主要系统效应。

### 从连续场到离散傅里叶模式

理论上，我们通常处理一个定义在连续三维空间中的无量纲物质密度涨落场 $\delta(\boldsymbol{x}) = \rho(\boldsymbol{x})/\bar{\rho} - 1$，其中 $\rho(\boldsymbol{x})$ 是位置 $\boldsymbol{x}$ 处的物质密度，$\bar{\rho}$ 是宇宙的平均物质密度。在无限大的宇宙中，这个场的傅里叶分析通过傅里叶变换来完成：
$$
\delta(\boldsymbol{k}) = \int_{\mathbb{R}^3} d^3x \, \delta(\boldsymbol{x}) e^{-i\boldsymbol{k}\cdot\boldsymbol{x}}, \quad \delta(\boldsymbol{x}) = \int \frac{d^3k}{(2\pi)^3} \delta(\boldsymbol{k}) e^{i\boldsymbol{k}\cdot\boldsymbol{x}}
$$
其中，波数向量 $\boldsymbol{k}$ 是一个连续变量。

然而，在数值模拟中，我们处理的是一个边长为 $L$ 的周期性立方体盒子，其体积为 $V=L^3$。周期性边界条件意味着所有物理量在盒子的相对两面是相同的，这极大地改变了傅里叶分析的性质。在这种情况下，场不再由傅里叶积分表示，而是由傅里叶级数表示。只有那些与盒子边界相容的波矢才能存在，它们构成分立的**傅里叶模式**，其波数向量为：
$$
\boldsymbol{k}_{\boldsymbol{m}} = \frac{2\pi}{L}\boldsymbol{m}, \quad \text{其中 } \boldsymbol{m} \in \mathbb{Z}^3 \text{ 是整数向量}
$$
这些离散的波数构成了傅里叶空间中的一个晶格，其基本间距（即**基频**）为 $k_f = 2\pi/L$。

对于这样一个周期性盒子中的离散场，我们需要一个与之相适应的傅里叶变换约定。当我们将场离散到一个包含 $N^3$ 个格点的均匀网格上时，格点间距为 $a=L/N$，格点坐标为 $\boldsymbol{x}_{\boldsymbol{j}} = a\boldsymbol{j}$。此时，傅里叶变换中的积分就变成了求和。一个物理上自洽且在宇宙学中广泛使用的约定是 [@problem_id:3481951]：
$$
\tilde{\delta}_{\boldsymbol{m}} = a^3 \sum_{\boldsymbol{j}} \delta_{\boldsymbol{j}} e^{-i \boldsymbol{k}_{\boldsymbol{m}} \cdot \boldsymbol{x}_{\boldsymbol{j}}}
$$
$$
\delta_{\boldsymbol{j}} = \frac{1}{V} \sum_{\boldsymbol{m}} \tilde{\delta}_{\boldsymbol{m}} e^{i \boldsymbol{k}_{\boldsymbol{m}} \cdot \boldsymbol{x}_{\boldsymbol{j}}}
$$
这里的 $\delta_{\boldsymbol{j}}$ 是在格点 $\boldsymbol{j}$ 上的密度涨落。前向变换中的 $a^3$ 因子是黎曼和中的体积元，确保了当格点数 $N \to \infty$ 时，该求和能够收敛到连续积分。反向变换中的 $1/V$ 因子则保证了变换对的归一化。这个约定与无限体积约定中的 $(2\pi)^{-3}$ 因子扮演着类似的角色，但明确地反映了有限体积的离散谱特性。在此约定下，傅里叶系数 $\tilde{\delta}_{\boldsymbol{m}}$ 的量纲是体积（$L^3$），而 $\delta_{\boldsymbol{j}}$ 是无量纲的。

这种离散傅里叶模式的正交性由**克罗内克-δ函数**（Kronecker delta）$\delta_{\boldsymbol{m}\boldsymbol{n}}$ 描述，而非连续情况下的狄拉克-δ函数（Dirac delta）。具体来说：
$$
\sum_{\boldsymbol{j}} e^{i (\boldsymbol{k}_{\boldsymbol{m}} - \boldsymbol{k}_{\boldsymbol{n}}) \cdot \boldsymbol{x}_{\boldsymbol{j}}} = N^3 \delta_{\boldsymbol{m}\boldsymbol{n}}
$$

### 傅里叶空间中的二点与三点统计量

密度场的统计特性主要体现在其傅里叶模式的关联之中。**统计均匀性**（statistical homogeneity）和**统计各向同性**（statistical isotropy）这两个基本假设极大地简化了这些关联的结构。

#### 功率谱

**功率谱** $P(k)$ 是密度场二点相关函数 $\xi(r) = \langle \delta(\boldsymbol{x}) \delta(\boldsymbol{x}+\boldsymbol{r}) \rangle$ 的傅里叶变换，它描述了不同尺度上密度涨落的强度。在傅里叶空间中，统计均匀性有一个至关重要的推论：不同的傅里叶模式是互不相关的 [@problem_id:3481982]。这意味着它们的协方差是对角的：
$$
\langle \tilde{\delta}(\boldsymbol{k}) \tilde{\delta}^{*}(\boldsymbol{k}') \rangle \propto \delta^K_{\boldsymbol{k},\boldsymbol{k}'}
$$
其中尖括号 $\langle \dots \rangle$ 表示系综平均（ensemble average），即在所有可能的宇宙实现上取平均。

通过严谨的推导，可以得到在周期性盒子中傅里叶模式协方差与功率谱之间的基本关系 [@problem_id:3481940]：
$$
\langle \tilde{\delta}(\boldsymbol{k}) \tilde{\delta}^{*}(\boldsymbol{k}') \rangle = V P(\boldsymbol{k}) \delta^K_{\boldsymbol{k},\boldsymbol{k}'}
$$
这个关系式是功率谱估计的核心。它表明，对于给定的模式 $\boldsymbol{k}$，其涨落的期望功率 $\langle |\tilde{\delta}(\boldsymbol{k})|^2 \rangle$ 直接正比于该模式的功率谱 $P(\boldsymbol{k})$ 和体积 $V$。

进一步，统计各向同性的假设意味着统计特性不依赖于方向。这使得功率谱 $P(\boldsymbol{k})$ 仅依赖于波数向量的模长 $k=|\boldsymbol{k}|$，即 $P(\boldsymbol{k}) = P(k)$ [@problem_id:3481982]。因此，所有位于同一半径的球面壳层内的傅里叶模式都具有相同的期望功率。

这个框架可以自然地推广到**互功率谱** $P_{ab}(k)$，它描述了两个不同密度场 $\delta_a$ 和 $\delta_b$（例如，不同类型的星系或星系与物质场）之间的关联。其定义关系为 [@problem_id:3481952]：
$$
\langle \tilde{\delta}_a(\boldsymbol{k}) \tilde{\delta}_b^{*}(\boldsymbol{k}') \rangle = V P_{ab}(\boldsymbol{k}) \delta^K_{\boldsymbol{k},\boldsymbol{k}'}
$$
互功率谱通常是复数，并满足 $P_{ba}(\boldsymbol{k}) = P_{ab}^*(\boldsymbol{k})$。只有当场的统计特性满足空间反演不变性（宇称守恒）时，$P_{ab}(k)$ 才为实数。

#### 双谱

**双谱** $B(\boldsymbol{k}_1, \boldsymbol{k}_2, \boldsymbol{k}_3)$ 是三点相关函数的傅里叶变换，它测量了由非线性引力演化引起的不同傅里叶模式之间的相位耦合，从而揭示了非高斯信息。与功率谱类似，统计均匀性要求三个傅里叶模式的关联只有在它们的波矢构成一个闭合三角形时才不为零，即满足**闭合条件** $\boldsymbol{k}_1 + \boldsymbol{k}_2 + \boldsymbol{k}_3 = \boldsymbol{0}$。

在周期性盒子中，双谱与三点模式关联的基本关系为 [@problem_id:3481933]：
$$
\langle \tilde{\delta}(\boldsymbol{k}_1) \tilde{\delta}(\boldsymbol{k}_2) \tilde{\delta}(\boldsymbol{k}_3) \rangle = V B(\boldsymbol{k}_1, \boldsymbol{k}_2, \boldsymbol{k}_3) \delta^K_{\boldsymbol{k}_1+\boldsymbol{k}_2+\boldsymbol{k}_3, \boldsymbol{0}}
$$
这个关系式表明，我们可以通过测量傅里叶空间中满足闭合条件的三个模式的乘积的系综平均来估计双谱。

### 从离散数据进行实际估计

理论上的定义是基于系综平均的，但在实践中我们只有一个宇宙的实现（或一次模拟）。根据**遍历性假设**（ergodic hypothesis），我们可以用空间平均（即对傅里叶空间中大量模式的平均）来代替系综平均。对于功率谱，这意味着我们可以通过平均一个薄的球面壳层内所有模式的功率来估计 $P(k)$：
$$
\hat{P}(k) = \frac{1}{V N_k} \sum_{\boldsymbol{k} \in \text{shell}(k)} |\tilde{\delta}(\boldsymbol{k})|^2
$$
其中 $N_k$ 是壳层内的模式数量。然而，从原始数据到这个估计量，有几个关键的实践步骤。

#### 质量分配方案

数值模拟的输出通常是大量离散粒子的位置和速度，而不是一个网格化的密度场。为了使用快速傅里叶变换（FFT），我们必须首先将这些粒子的质量分配到规则的网格上，生成一个离散的密度场。这个过程称为**质量分配**（mass assignment）。

常用的分配方案包括最近邻点格法（Nearest Grid Point, NGP）、云中单元格法（Cloud-In-Cell, CIC）和三角形状云法（Triangular Shaped Cloud, TSC）。这些方案在数学上等价于将每个粒子的点状分布（一个狄拉克-δ函数）与一个特定的分配核函数进行卷积。根据卷积定理，这个操作在傅里叶空间中对应于将真实的傅里叶模式乘以一个**窗口函数** $W(\boldsymbol{k})$ [@problem_id:3481985]。

这些分配核是可分离的，因此三维窗口函数可以分解为三个一维窗口函数的乘积：$W(\boldsymbol{k}) = W(k_x)W(k_y)W(k_z)$。对于 NGP (p=0)、CIC (p=1) 和 TSC (p=2)，一维窗口函数的形式为 [@problem_id:3481985]：
$$
W_p(k) = \left[ \operatorname{sinc}\left(\frac{k\Delta}{2}\right) \right]^{p+1}
$$
其中 $\Delta$ 是网格间距，$\operatorname{sinc}(x) \equiv \sin(x)/x$。由于这个窗口函数的存在，我们测得的功率谱实际上是 $|W(\boldsymbol{k})|^2 P_{\text{true}}(k)$。因此，为了得到真实的功率谱，我们必须对估计出的谱进行**解卷积**，即除以 $|W(\boldsymbol{k})|^2$。

#### 快速傅里叶变换（FFT）的归一化

标准的FFT算法库通常返回一个未归一化的傅里叶系数。例如，一个没有前置因子的FFT实现，其输出与我们物理上定义的傅里叶模式 $\tilde{\delta}(\boldsymbol{k})$ 之间存在一个与网格单元体积 $\Delta V = a^3$ 相关的比例因子。将离散傅里叶变换的定义与黎曼和进行比较可以发现 [@problem_id:3481931]：
$$
\tilde{\delta}(\boldsymbol{k}_{\boldsymbol{n}}) \approx \Delta V \cdot \text{FFT}[\delta](\boldsymbol{n})
$$
其中 $\text{FFT}[\delta](\boldsymbol{n})$ 是FFT算法对格点场 $\delta_{\boldsymbol{j}}$ 返回的复数数组。

综合考虑，一个完整的功率谱估计流程如下 [@problem_id:3481931]：
1.  **质量分配**：将粒子质量分配到网格上，得到 $\delta_{\boldsymbol{j}}$。
2.  **FFT**：计算 $\text{FFT}[\delta](\boldsymbol{n})$。
3.  **归一化**：将FFT输出乘以 $\Delta V$ 得到 $\tilde{\delta}(\boldsymbol{k}_{\boldsymbol{n}})$。
4.  **计算功率**：计算每个模式的功率 $|\tilde{\delta}(\boldsymbol{k}_{\boldsymbol{n}})|^2$。
5.  **球壳平均**：在 $k$ 空间的不同球壳内对模式功率进行平均，并除以体积 $V$。
6.  **窗口函数解卷积**：将结果除以相应 $k$ 处的 $|W(\boldsymbol{k})|^2$。

### 系统效应与校正

在估计过程中，多种物理和数值效应会引入系统性的偏差，必须加以理解和校正。

#### 散粒噪声

当密度场由离散的示踪物（如星系或模拟粒子）表示时，即使这些示踪物完全随机分布（即不包含任何物理成团性），它们的离散性本身也会产生一个非零的功率谱，这被称为**散粒噪声**（shot noise）。

对于一个平均数密度为 $\bar{n}$ 的泊松采样点过程，可以从第一性原理推导出，测得的功率谱是真实信号功率谱与一个常数项的和 [@problem_id:3481964]：
$$
\langle \hat{P}_{\text{measured}}(k) \rangle = P_{\text{signal}}(k) + \frac{1}{\bar{n}}
$$
这个加性常数 $1/\bar{n}$ 就是散粒噪声项。它源于对粒子自身位置的关联计算（即二点相关中“同一点对”的贡献）。因此，为了得到无偏的信号功率[谱估计](@entry_id:262779)，必须从测得的功率谱中减去这个理论预测的散粒噪声项 [@problem_id:3481940]。对于一个完整的功率谱估计器，正确的做法是在完成所有步骤（包括窗口解卷积）后，再减去 $1/\bar{n}$ [@problem_id:3481931]。

#### 混叠效应

**混叠**（Aliasing）是一种由于在离散网格上采样连续场而产生的效应。在实空间中，以间距 $\Delta$ 进行采样，等效于将连续场乘以一个由狄拉克-δ函数组成的梳状函数。根据卷积定理，这在傅里叶空间中对应于将真实的傅里叶谱与另一个梳状函数进行卷积，其周期为 $k_s = 2\pi/\Delta$ [@problem_id:3481980]。

这个卷积过程导致真实的频谱以 $k_s$ 为周期在傅里叶空间中无限复制。离散傅里叶变换（DFT）只能测量一个基本区间（第一布里渊区）内的模式，通常是 $|k_\alpha|  k_{\text{Ny}}$，其中 $k_{\text{Ny}} = \pi/\Delta = k_s/2$ 是**奈奎斯特频率**。因此，在某个波数 $\boldsymbol{k}$ 处测得的功率，实际上是真实谱在 $\boldsymbol{k}$、$\boldsymbol{k} \pm \boldsymbol{k}_s$、$\boldsymbol{k} \pm 2\boldsymbol{k}_s$ 等所有位置的功率之和。来自高频（$|k| > k_{\text{Ny}}$）的功率被“折叠”到了低频区域，从而污染了测量结果。混叠效应的大小由网格间距 $\Delta$ 和超出奈奎斯特频率的真实功率大小决定，与模拟盒子的尺寸 $L$ 无关。

#### 有限体积效应与积分约束

**有限体积效应**源于我们只能在有限的体积 $V$ 内观测宇宙。这等效于将真实的宇宙密度场乘以一个窗函数（在周期性盒子中是整个盒子的窗）。这会在傅里叶空间中导致谱的卷积模糊，并使得可测量的傅里叶模式离散化，基频为 $k_f = 2\pi/L$。这意味着波长大于盒子尺寸 $L$ 的涨落模式无法被直接测量，这是宇宙方差（cosmic variance）的一个来源 [@problem_id:3481980]。

一个更微妙的有限体积效应是**积分约束**（integral constraint）[@problem_id:3481960]。由于我们无法得知宇宙的真实平均密度，我们只能测量相对于我们观测体积内样本平均密度的涨落。这意味着我们实际分析的场 $\delta_{\text{ic}}(\boldsymbol{x})$ 被强制要求在观测体积内的均值为零，即 $\int_V \delta_{\text{ic}}(\boldsymbol{x}) d^3x = 0$。

这个操作在傅里叶空间中等效于强制设定中心模式 $\tilde{\delta}(\boldsymbol{k}=\boldsymbol{0})$ 为零。然而，真实的密度场在 $k=0$ 附近（即对应于大于等于巡天尺度的波长）是存在功率的。减去样本均值的操作，实际上移除了这部分大尺度模式的贡献。由于窗函数的存在导致的模式耦合，这种在 $\boldsymbol{k}=0$ 处的功率压制会“泄漏”到其附近的波数模式上。结果是，估计出的功率谱 $\hat{P}(k)$ 在小 $k$（大尺度）处会系统性地低于真实的功率谱，产生一种负向偏差。这种偏差的精确形式依赖于巡天的几何形状（即窗函数），是分析大尺度巡天数据时必须考虑和建模的重要系统效应 [@problem_id:3481960]。