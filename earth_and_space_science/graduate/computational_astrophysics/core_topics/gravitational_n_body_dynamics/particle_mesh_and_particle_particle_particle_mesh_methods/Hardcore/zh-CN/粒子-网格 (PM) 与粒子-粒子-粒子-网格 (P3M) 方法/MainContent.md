## 引言
模拟宇宙中数以亿计天体的引力相互作用，以揭示大尺度结构的形成和演化，是现代计算天体物理学的核心挑战之一。直接计算所有粒子对之间的引力是一个计算复杂度为 O(N²) 的问题，对于大规模模拟而言，这在计算上是不可行的。为了弥合理论预测与可观测宇宙之间的鸿沟，科学家们迫切需要一种既高效又精确的数值方法。粒子-网格（PM）及其改进的粒子-粒子 粒子-网格（P³M）方法正是为解决这一难题而诞生的关键技术，它们彻底改变了我们模拟引力动力学的能力。

本文旨在为计算科学领域的研究生提供一份关于PM和P³M方法的全面指南。通过学习本文，您将系统地掌握这一强大的数值模拟范式。在第一章“原理与机制”中，我们将从第一性原理出发，剖析PM方法的核心算法——从质量分配到利用快速傅里叶变换求解泊松方程，并深入分析其固有的数值效应。我们还将探讨P³M方法如何通过混合计算方案来克服PM方法的局限性，从而在小尺度上实现更高的精度。

随后，在第二章“应用与跨学科联系”中，我们将展示这些方法在天体物理学核心问题（如宇宙网结构识别和修正引力模型检验）中的精妙应用，并与其他N体算法进行性能比较。更重要的是，我们将揭示P³M方法背后的抽象思想如何被移植到分子动力学、流行病学和交通流等看似无关的领域，突显其作为一种通用多尺度建模工具的强大生命力。

最后，在第三章“动手实践”中，您将有机会通过一系列精心设计的计算练习，将理论知识转化为实践技能，从实现基本的质量分配方案到分析和修正数值误差，从而巩固您对这些方法的深刻理解。让我们开始这段从基本原理到前沿应用的探索之旅。

## 原理与机制

本章深入探讨了粒子-网格（Particle-Mesh, PM）和粒子-粒子 粒子-网格（Particle-Particle Particle-Mesh, P³M）方法的核心原理与基本机制。这些方法是现代宇宙学 N 体模拟的基石，用于高效计算大尺度结构形成过程中引力的演化。我们将从 PM 方法的基本算法出发，系统地剖析其各个组成部分，分析其数值特性，并在此基础上引出为克服其局限性而设计的 P³M 混合方法。

### 粒子-网格（PM）方法：核心算法

PM 方法的核心思想是通过在规则网格上求解引力势来规避直接计算所有粒子对之间相互作用所需的高昂计算成本。该过程可分解为四个主要步骤：质量分配、求解泊松方程、计算引力场和将力插值回粒子。

#### 从连续场到离散网格

在一个由 $N$ 个粒子组成的自引力系统中，每个粒子的运动都受到所有其他粒子引力的影响。描述这一物理过程的基本方程是引力势 $\Phi(\boldsymbol{x})$ 所满足的泊松方程：

$ \nabla^2 \Phi(\boldsymbol{x}) = 4\pi G \rho(\boldsymbol{x}) $

其中，$G$ 是引力常数，$\rho(\boldsymbol{x})$ 是质量密度分布。对于由质量为 $m_i$、位置为 $\boldsymbol{x}_i$ 的离散粒子组成的系统，其连续密度场可以形式化地表示为一系列狄拉克 $\delta$ 函数之和：$\rho(\boldsymbol{x}) = \sum_i m_i \delta_D(\boldsymbol{x} - \boldsymbol{x}_i)$。

在宇宙学模拟中，通常采用周期性边界条件来模拟一个具有代表性、在统计上均匀的宇宙区域。然而，在周期性边界条件下直接求解上述泊松方程会遇到数学上的困难。对泊松方程在整个周期性立方体（体积为 $V$）上进行积分，利用散度定理，我们得到：

$ \int_V \nabla^2 \Phi \, d^3x = \oint_{\partial V} \nabla\Phi \cdot d\boldsymbol{S} = 0 $

这是因为在周期性边界下，相对面上的通量大小相等、方向相反，总和为零。然而，方程右侧的积分等于 $4\pi G \int_V \rho \, d^3x = 4\pi G M_{\text{tot}}$，其中 $M_{\text{tot}}$ 是盒子内的总质量。这导致了 $0 = 4\pi G M_{\text{tot}}$ 的矛盾，除非总质量为零。

为了解决这个矛盾，我们认识到宇宙学模拟关注的是密度扰动 $\delta\rho(\boldsymbol{x}) = \rho(\boldsymbol{x}) - \bar{\rho}$，其中 $\bar{\rho}$ 是宇宙的平均密度。正是这些扰动驱动了结构的形成。因此，我们求解的是由密度扰动产生的引力势，这等效于引入一个均匀的、起中和作用的背景密度。修正后的泊松方程为：

$ \nabla^2 \Phi(\boldsymbol{x}) = 4\pi G \left[ \rho(\boldsymbol{x}) - \bar{\rho} \right] $

其中 $\bar{\rho} = M_{\text{tot}}/V$。这个方程在周期性边界条件下是自洽的，因为源项的全域积分现在为零。这在物理上意味着我们计算的是相对于均匀膨胀背景的** peculiar potential**（奇特势）[@problem_id:3529286]。

#### 质量分配：将质量分布到网格

为了在网格上求解泊松方程，必须首先将离散粒子的质量分布到网格点上，从而创建一个离散的密度场。这个过程称为**质量分配**（mass assignment）。它将粒子从数学上的点（狄拉克函数）“涂抹”成具有一定空间尺度的“云”。

这个过程可以被理解为粒子分布与一个**分配核函数**（assignment kernel）或**窗口函数**（window function）$W$ 的卷积。给定网格间距为 $h$，分配后的密度场 $\rho_m(\boldsymbol{x})$ 为：

$ \rho_{m}(\boldsymbol{x}) \equiv \sum_{i} m_{i}\, W(\boldsymbol{x}-\boldsymbol{x}_{i}) $

其中 $W(\boldsymbol{x})$ 是一个归一化的（$\int W(\boldsymbol{x}) d^3x = 1$）、具有紧凑支撑的函数 [@problem_id:3529356]。在实践中，我们计算每个网格单元 $j$ 内的平均密度 $\rho_j$。设粒子 $i$ 分配给网格单元 $j$ 的质量分数为 $w_j(\boldsymbol{x}_i)$，且满足质量守恒 $\sum_j w_j(\boldsymbol{x}_i) = 1$，则网格密度为：

$ \rho_j = \frac{1}{\Delta V} \sum_{i=1}^N m_i \cdot w_j(\boldsymbol{x}_i) $

其中 $\Delta V$ 是网格单元的体积 [@problem_id:3529286]。

最常用的分配方案是基于 B-样条函数的分层体系，它们通过重复卷积一个基本的“顶帽”函数（top-hat function）而构成。主要有以下几种 [@problem_id:3529311]：

*   **最近邻网格点（Nearest-Grid-Point, NGP）**：这是零阶方案（$p=0$），将每个粒子的全部质量赋给离它最近的那个网格点。其一维核函数是一个宽度为 $\Delta$（网格间距）的矩形函数：
    $ W_{\mathrm{NGP}}(x) = \begin{cases} 1/\Delta,  |x| \le \Delta/2 \\ 0,  \text{otherwise} \end{cases} $

*   **云中单元（Cloud-In-Cell, CIC）**：这是一阶方案（$p=1$），通过将 NGP 核函数自身卷积一次得到。它将粒子质量线性地分配给相邻的 $2^3=8$ 个（在三维中）网格点。其一维核函数是一个“帐篷”状的三角形函数：
    $ W_{\mathrm{CIC}}(x) = \begin{cases} \frac{1}{\Delta}(1 - \frac{|x|}{\Delta}),  |x| \le \Delta \\ 0,  \text{otherwise} \end{cases} $

*   **三角形状云（Triangular-Shaped Cloud, TSC）**：这是二阶方案（$p=2$），通过将 CIC 核函数与 NGP 核函数卷积得到。它将粒子质量以二次多项式形式分配给相邻的 $3^3=27$ 个网格点。其一维核函数是分段二次函数，具有更平滑的特性。

在三维空间中，这些核函数通常是**可分离的**（separable），即三维核函数是三个一维核函数的乘积：$W(x,y,z) = W(x)W(y)W(z)$。

#### 在傅里叶空间中求解泊松方程

一旦获得了网格上的密度场 $\rho(\boldsymbol{x})$，下一步就是求解泊松方程。直接在实数空间（构型空间）求解微分方程是复杂的。然而，利用**傅里叶变换**，特别是其将微分运算转换成代数乘法的优良性质，可以极大地简化问题。这正是 **卷积定理** 的威力所在。

对修正后的泊松方程 $\nabla^2 \Phi = 4\pi G \delta\rho$（其中 $\delta\rho = \rho - \bar{\rho}$）两边进行傅里叶变换，我们得到：

$ \mathcal{F}\{\nabla^2 \Phi\} = \mathcal{F}\{4\pi G \delta\rho\} $

由于傅里叶变换将 $\nabla^2$ 算子映射为乘以 $-|\boldsymbol{k}|^2$（其中 $\boldsymbol{k}$ 是波数向量），方程变为：

$ -|\boldsymbol{k}|^2 \tilde{\Phi}(\boldsymbol{k}) = 4\pi G \widetilde{\delta\rho}(\boldsymbol{k}) $

其中带波浪线的变量表示其傅里叶变换。这样，我们就得到了一个关于引力势傅里叶模式 $\tilde{\Phi}(\boldsymbol{k})$ 的简单代数方程。对于所有 $\boldsymbol{k} \neq \boldsymbol{0}$ 的模式，解为：

$ \tilde{\Phi}(\boldsymbol{k}) = -\frac{4\pi G}{|\boldsymbol{k}|^2} \widetilde{\delta\rho}(\boldsymbol{k}) $

对于 $\boldsymbol{k} = \boldsymbol{0}$ 模式（对应于直流分量或平均值），由于我们求解的是密度扰动 $\delta\rho$，其平均值为零，因此 $\widetilde{\delta\rho}(\boldsymbol{0}) = 0$。这避免了分母 $|\boldsymbol{k}|^2$ 为零所导致的奇点问题。通常，我们设定 $\tilde{\Phi}(\boldsymbol{0}) = 0$，因为势的常数偏移不影响引力 [@problem_id:3529301]。

在数值实现中，我们使用**快速傅里叶变换（FFT）**来高效地执行离散傅里叶变换。同时，微分算子也必须被离散化。例如，一个二阶精度的有限差分拉普拉斯算子，其在傅里叶空间中的等效表示（或称“符号”）为 [@problem_id:3529301]：

$ \hat{k}^2(\boldsymbol{k}) = \frac{4}{\Delta x^2}\left[ \sin^2\left(\frac{k_x \Delta x}{2}\right) + \sin^2\left(\frac{k_y \Delta x}{2}\right) + \sin^2\left(\frac{k_z \Delta x}{2}\right) \right] $

整个求解流程如下：
1.  **质量分配**：将粒子质量分配到网格上，得到 $\rho(\boldsymbol{x})$，并计算密度扰动 $\delta\rho(\boldsymbol{x}) = \rho(\boldsymbol{x}) - \bar{\rho}$。
2.  **正向 FFT**：计算密度扰动的傅里叶变换 $\widetilde{\delta\rho}(\boldsymbol{k}) = \mathrm{FFT}[\delta\rho(\boldsymbol{x})]$。
3.  **势求解**：在傅里叶空间中，对每个 $\boldsymbol{k} \neq \boldsymbol{0}$ 模式，通过代数乘法计算势的模式 $\tilde{\Phi}(\boldsymbol{k}) = -\frac{4\pi G}{\hat{k}^2(\boldsymbol{k})} \widetilde{\delta\rho}(\boldsymbol{k})$。
4.  **计算引力场**：引力场 $\boldsymbol{g} = -\nabla\Phi$。在傅里叶空间中，梯度算子 $\nabla$ 对应于乘以 $i\boldsymbol{k}$。因此，$\tilde{\boldsymbol{g}}(\boldsymbol{k}) = -i\boldsymbol{k} \tilde{\Phi}(\boldsymbol{k})$。
5.  **逆向 FFT**：对引力场的傅里叶模式进行逆变换，得到网格上的引力场 $\boldsymbol{g}(\boldsymbol{x}) = \mathrm{FFT}^{-1}[\tilde{\boldsymbol{g}}(\boldsymbol{k})]$。

#### 力插值与粒子更新

最后一步是将网格上计算出的引力场插值回每个粒子的实际位置，以获得作用在它们身上的力。这个过程称为**力插值**（force interpolation）。为了保证系统的总动量守恒，一个关键原则是采用与质量分配相同的方案进行力插值。例如，如果使用了 CIC 进行质量分配，那么也应该使用 CIC 将周围 8 个网格点的力值线性插值到粒子位置。

获得每个粒子所受的力 $\boldsymbol{F}_i = m_i \boldsymbol{g}(\boldsymbol{x}_i)$ 后，就可以使用数值积分方法（如蛙跳法，leapfrog integrator）来更新粒子的速度和位置，从而推动模拟向前演化一步。

### 数值效应分析与方法改进

PM 方法虽然高效，但其离散化的本质引入了一系列数值效应，理解并控制这些效应对于确保模拟的准确性至关重要。

#### 混叠与奈奎斯特频率

当一个连续信号在离散点上采样时，高于某个特定频率的频率信息会“伪装”成低于该频率的频率。这种现象称为**混叠**（aliasing）。对于一个间距为 $h$ 的均匀网格，能够被唯一表示的最大波数称为**奈奎斯特波数**（Nyquist wavenumber），定义为 $k_{\mathrm{Ny}} = \pi/h$。

任何高于奈奎斯特波数的连续模式 $k$ 在采样后都会被映射到**第一布里渊区**（first Brillouin zone）$-k_{\mathrm{Ny}}, k_{\mathrm{Ny}})$ 内的一个[混叠波数 $k_a(k)$。这个关系可以通过分析采样过程的傅里叶变换来严格导出。采样过程等效于将连续信号与一个狄拉克梳状函数相乘，这在傅里叶空间中对应于将原始频谱与一个倒易晶格进行卷积。其结果是，原始频谱以 $2k_{\mathrm{Ny}} = 2\pi/h$ 为周期进行复制。因此，混叠波数 $k_a(k)$ 满足 $k_a(k) \equiv k \pmod{2\pi/h}$。一个明确的表达式为 [@problem_id:3529349]：

$ k_{\mathrm{a}}(k) = k - \frac{2\pi}{h} \left\lfloor \frac{kh}{2\pi} + \frac{1}{2} \right\rfloor $

其中 $\lfloor \cdot \rfloor$ 是向下取整函数。混叠效应意味着小尺度（高波数）的物理信息会错误地污染大尺度（低波数）的测量，这是 PM 方法分辨率的一个基本限制。

#### 质量分配核函数的影响

质量分配方案的选择对模拟的精度有深远影响。我们可以从统计学的**核密度估计**（kernel density estimation）角度来分析它。PM 方法中的密度场可被视为对真实密度场的一个估计，其误差可以用**均方积分误差（Mean Integrated Squared Error, MISE）**来度量。MISE 可以分解为**偏差（bias）**的平方和**方差（variance）**两部分 [@problem_id:3529338]。

*   **偏差**：源于分配核函数对真实密度场的平滑作用。对于一个对称的核函数，其导致的偏差在低波数下主要与核函数的二阶矩 $\mu_2(W) = \int x^2 W(\boldsymbol{x}) d^3x$ 成正比。对于 NGP、CIC、TSC，核函数的阶数越高，其支撑范围越广，平滑作用越强，因此偏差也越大。
*   **方差**：主要源于粒子分布的离散性，即所谓的**散粒噪声**（shot noise）。方差与核函数自身的平方积分 $R(W) = \int W(\boldsymbol{x})^2 d^3x$ 成正比。更高阶、更平滑的核函数（如 TSC）具有更小的 $R(W)$，因此能更有效地抑制散粒噪声。

这种偏差-方差权衡也体现在傅里叶空间中。分配过程的卷积操作在傅里叶空间中变为乘法，其乘法因子 $\tilde{W}(\boldsymbol{k})$ 称为**传递函数**（transfer function）。对于 B-样条核函数，可以推导出其传递函数的形式。例如，CIC 和 TSC 的三维传递函数分别为 [@problem_id:3529356]：

$ \tilde{W}_{\mathrm{CIC}}(\boldsymbol{k}) = \mathrm{sinc}^2(\frac{k_x h}{2})\,\mathrm{sinc}^2(\frac{k_y h}{2})\,\mathrm{sinc}^2(\frac{k_z h}{2}) $
$ \tilde{W}_{\mathrm{TSC}}(\boldsymbol{k}) = \mathrm{sinc}^3(\frac{k_x h}{2})\,\mathrm{sinc}^3(\frac{k_y h}{2})\,\mathrm{sinc}^3(\frac{k_z h}{2}) $

其中 $\mathrm{sinc}(z) = \sin(z)/z$。这些函数在 $k=0$ 时为 1，并随着 $k$ 的增大而衰减，这定量地描述了分配方案对高频信号的压制（即平滑偏差）。更高阶的核函数（如 TSC）在相同 $k$ 值下的衰减更慢，这意味着它们对小尺度信号的保真度稍好，但它们也同时引入了更大的偏差。如果尝试通过在傅里叶空间除以 $\tilde{W}(\boldsymbol{k})$ 来进行**反卷积**（deconvolution）以校正这种平滑，那么在接近奈奎斯特频率时，由于 $\tilde{W}(\boldsymbol{k})$ 的值很小，噪声会被急剧放大，对于 TSC 这种高阶方案尤其如此 [@problem_id:3529338]。

在给定粒子数密度 $n$ 的情况下，存在一个**最优网格间距** $\Delta_\star$，它在偏差和方差之间取得平衡，从而最小化总误差 MISE。对于三维情况，这个最优间距的标度关系为 $\Delta_\star \propto n^{-1/7}$，这个标度律不依赖于分配核的阶数，但其具体系数依赖于核函数的 $\mu_2(W)$ 和 $R(W)$ [@problem_id:3529338]。

#### 各向异性与守恒律

PM 方法中使用的笛卡尔网格破坏了物理空间的连续旋转对称性，引入了**各向异性**（anisotropy）误差。这种误差的一个重要表现是力的计算不再精确地指向粒子对的连线方向，从而可能导致角动量不守恒。

一个有趣的特例是**自引力**（self-force）问题。考虑一个孤立粒子，理论上它不应受到自己的引力作用。在使用 NGP 进行质量分配和力插值时，粒子的质量被完全置于最近的网格点上。由于离散傅里叶算子的对称性，一个点质量源在其自身位置产生的力恰好为零。因此，只要粒子不穿越其所在单元的边界，计算出的自引力始终为零 [@problem_id:3529307]。这个结果彰显了保持分配和插值方案一致性的重要性。

然而，对于更一般的情况，如一个粒子绕中心天体运动，网格的各向异性会导致计算出的力有一个微小的、随方位角变化的扰动。这个扰动可以被建模为一个依赖于角度的附加势，例如 $\Phi_1 \propto \cos(4\theta)$，它反映了网格的四重对称性。这种非中心的力会产生一个净扭矩，导致粒子在一个轨道周期内角动量发生振荡，从而引发长期的轨道漂移。分析表明，使用更高阶的分配/插值方案（如 TSC）可以显著减小这种各向异性效应。例如，从 NGP 切换到 TSC，角动量振荡的幅度可以减小一个数量级，其比值为 $(\pi/2)^4 \approx 6.09$ [@problem_id:3529360]。这为选择更平滑的高阶核函数提供了另一个强有力的理由：它们能更好地保持系统的守恒律。

### 粒子-粒子 粒子-网格（P³M）方法

PM 方法的主要缺点在于其空间分辨率受限于网格间距。对于小于网格尺度的结构，引力计算是不准确的。为了解决这个问题，P³M 方法应运而生。

#### 混合方法：结合 PM 与直接求和

P³M 是一种**混合方法**，它将引力巧妙地分解为两部分：
1.  **长程力（Long-range force）**：这部分力变化平滑，可以由 PM 方法在网格上高效计算。
2.  **短程力（Short-range force）**：这部分力在粒子靠近时变化剧烈，通过对邻近粒子对进行**直接求和**（direct summation, 或称 Particle-Particle, PP）来精确计算。

力分解通常通过将 $1/r$ 的引力势乘以一个截断函数来实现。例如，总力 $\boldsymbol{F}$ 可以写成：

$ \boldsymbol{F} = \boldsymbol{F}_{\text{long}} + \boldsymbol{F}_{\text{short}} = \boldsymbol{F} \cdot f(r) + \boldsymbol{F} \cdot (1 - f(r)) $

其中 $f(r)$ 是一个平滑的截断函数（如误差函数 $\mathrm{erf}(r/r_c)$），在小 $r$ 处趋于 0，在大 $r$ 处趋于 1。长程部分由 PM 计算，短程修正部分仅对少数近邻粒子进行直接 PP 计算，从而在保持计算效率的同时，极大地提高了短程力的精度。

#### 短程力与引力软化

在无碰撞的 N 体模拟中（如暗物质晕），我们不希望模拟真实的双体散射，因为这会导致不符合物理的弛豫过程。直接计算牛顿引力 $F \propto 1/r^2$ 会在粒子间距 $r \to 0$ 时导致极大的加速度和发散的力，从而产生剧烈的双体散射。

为了避免这种情况，P³M 的短程力计算中引入了**引力软化**（force softening）。这相当于修改了极近距离下的引力定律，使其保持有限。一个常用的软化方法是**Plummer 软化**，其势能形式为：

$ U(r) = - \frac{G m^2}{\sqrt{r^2 + \epsilon^2}} $

其中 $\epsilon$ 是**软化长度**（softening length）。当 $r \gg \epsilon$ 时，该势能趋近于牛顿引力；而当 $r \ll \epsilon$ 时，力的大小近似为 $F(r) \propto r$，如同一个谐振子，避免了奇点。

我们可以分析软化对双体散射的影响。在小角度散射的**冲量近似**（impulse approximation）下，可以导出最近邻散射角 $\theta_{\mathrm{nn}}$ 与撞击参数 $s$（可视为局部粒子间距）的关系 [@problem_id:3529322]。其散射角为：

$ \theta_{\mathrm{nn}} = \frac{4 G m s}{v_{\infty}^2 (s^2 + \epsilon^2)} $

其中 $v_{\infty}$ 是相对速度。这个表达式揭示了两个重要的渐进行为：
*   当 $s \gg \epsilon$ 时，$\theta_{\mathrm{nn}} \propto s^{-1}$，与无软化的卢瑟福散射行为一致。
*   当 $s \ll \epsilon$ 时，$\theta_{\mathrm{nn}} \propto s$，散射角随撞击参数线性减小，有效抑制了近距离遭遇造成的剧烈偏转。

通过合理选择软化长度 $\epsilon$，P³M 方法能够在精确计算短程力的同时，有效抑制非物理的数值弛豫效应。

### 高等主题与边界条件

#### 孤立边界条件与周期性边界条件

PM 方法的边界条件选择取决于所模拟的物理系统。
*   **周期性边界条件**：适用于模拟宇宙中一个具有代表性、无限延伸的区域，是宇宙学大尺度结构模拟的标准选择。
*   **孤立边界条件（或称自由空间边界条件）**：适用于模拟孤立系统，如单个星系或星系团，其中引力势在无穷远处衰减为零。

这两种情况对应于不同的泊松方程格林函数（Green's function）。周期性情况的解通常在傅里叶空间中进行，如前所述，其谱空间格林函数为 $\tilde{G}(\boldsymbol{k}) = -4\pi G/k^2$（并对 $\boldsymbol{k}=\boldsymbol{0}$ 进行特殊处理）。而孤立系统的解在实空间中是与自由空间格林函数 $g(\boldsymbol{r}) = -G/|\boldsymbol{r}|$ 的卷积 [@problem_id:3529333]：

$ \phi(\boldsymbol{x}) = (g * \rho)(\boldsymbol{x}) = \int -\frac{G}{|\boldsymbol{x}-\boldsymbol{x}'|} \rho(\boldsymbol{x}') d^3x' $

虽然这是实空间积分，但我们仍然可以利用 FFT 的高效性来计算这个卷积。根据卷积定理，$\widehat{g * \rho} = \hat{g} \cdot \hat{\rho}$。因此，我们可以在傅里叶空间中将密度和格林函数的谱相乘，然后通过逆 FFT 得到结果。

然而，一个关键的微妙之处在于，FFT 计算的是**循环卷积**（cyclic convolution），而非物理上需要的**线性卷积**（linear convolution）。直接对同样大小的 $\rho$ 和 $g$ 网格进行 FFT 卷积，会导致由于周期性假设而产生的“环绕”误差，即盒子一侧的质量会错误地影响到另一侧。

为了用 FFT 正确计算线性卷积，必须采用**零填充**（zero-padding）技术。基本思想是将原始数据和卷积核都嵌入到一个更大的、用零填充的数组中。对于一维长度为 $N$ 的数据和长度为 $M$ 的核，其线性卷积结果长度为 $N+M-1$。因此，需要将两个数组都填充到至少这个长度才能避免循环混淆。在三维中，这个规则适用于每个维度。一个安全且常见的做法是将原始的 $N \times N \times N$ 网格数据嵌入到一个 $(2N) \times (2N) \times (2N)$ 的大网格中。计算完成后，结果的中心 $N \times N \times N$ 部分就是正确的线性卷积结果，而周围的区域则可被丢弃。零填充通过在数据周围创建“缓冲区”来确保循环图像不会污染到我们关心的物理区域内，从而使 FFT 能够忠实地模拟出孤立系统的物理行为 [@problem_id:3529333]。