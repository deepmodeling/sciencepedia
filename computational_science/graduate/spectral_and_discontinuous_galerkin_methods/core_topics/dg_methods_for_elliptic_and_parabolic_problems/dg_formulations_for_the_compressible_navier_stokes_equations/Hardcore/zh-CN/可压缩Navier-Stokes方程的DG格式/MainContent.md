## 引言
在计算流体力学（CFD）领域，对飞行器绕流、发动机燃烧、天气预报等复杂流动现象进行高保真仿真是推动科学发现和工程创新的关键。可压缩Navier-Stokes方程是描述这些现象的数学模型，但其非线性、多尺度特性给数值求解带来了巨大挑战。传统低阶方法难以准确捕捉湍流、激波等精细结构，而间断Galerkin（DG）方法作为一种高阶数值方法，凭借其卓越的几何灵活性、对间断的清晰捕捉能力以及天然的并行性，成为解决此类问题的前沿工具。然而，构建一个稳定、高效且准确的DG格式，需要深入理解其内在的数学原理与复杂的实现细节，这正是本文旨在解决的知识鸿沟。

本文将系统性地引导读者深入可压缩Navier-Stokes方程的DG世界。在**“原理与机制”**一章中，我们将从守恒律方程出发，详细剖析DG离散化的核心构件，包括对流项的数值通量和粘性项的专门处理方法。接着，**“应用与跨学科联系”**一章将展示DG方法如何通过IMEX时间积分、壁模型LES、hp-自适应等先进技术，从理论走向实践，解决航空航天、地球物理等领域的实际问题。最后，**“动手实践”**部分提供了一系列精心设计的练习，帮助读者将理论知识转化为解决实际计算问题的能力。通过这一结构化的学习路径，读者将全面掌握DG方法的核心思想与前沿应用。

## 原理与机制

本章深入探讨了可压缩Navier-Stokes方程的间断Galerkin (DG) 离散格式的原理和机制。我们将从守恒形式的控制方程出发，系统地阐述求解过程中各个环节的核心概念，包括变量集的选取、对流项与粘性项的数值通量构造，以及高阶方法在实际计算中的关键技术问题。

### 可压缩Navier-Stokes方程的守恒形式

可压缩流动的控制方程源于质量、动量和总能量的守恒定律。对于DG方法而言，将这些方程写成统一的守恒形式至关重要。一个一般性的守恒形式如下：
$$
\partial_{t} U + \nabla \cdot F^{c}(U) \;=\; \nabla \cdot F^{v}(U,\nabla U) \;+\; S
$$
此形式将状态随时间的变化率与空间通量的散度以及源项联系起来。下面我们详细定义每个组成部分 [@problem_id:3376463]。

**守恒变量向量 (State Vector of Conserved Variables)** $U$ 包含了单位体积内的守恒量。在三维空间中，它通常是一个包含五个分量的向量：
$$
U \;=\; \begin{pmatrix} \rho \\ \rho u_1 \\ \rho u_2 \\ \rho u_3 \\ \rho E \end{pmatrix}
$$
其中，$\rho$ 是流体密度，$\boldsymbol{u} = (u_1, u_2, u_3)^T$ 是速度向量，$\rho \boldsymbol{u}$ 是动量密度。$E$ 是单位质量的总能量，定义为内能 $e$ 和动能之和，即 $E = e + \frac{1}{2}|\boldsymbol{u}|^2$。因此，$\rho E$ 是单位体积的总能量。

**对流通量 (Convective Flux)** $F^c(U)$ 描述了守恒量随流体自身运动（即平流）而产生的输运。它是一个张量，其各列是沿相应坐标轴方向的通量向量。在 $j$ 方向上的对流通量向量为：
$$
F^c_j(U) \;=\; \begin{pmatrix} \rho u_j \\ \rho u_1 u_j + p \delta_{1j} \\ \rho u_2 u_j + p \delta_{2j} \\ \rho u_3 u_j + p \delta_{3j} \\ (\rho E + p) u_j \end{pmatrix}
$$
这里，$p$ 是压力，$\delta_{ij}$ 是克罗内克符号。通量的物理意义非常直观：第一项 $\rho u_j$ 是质量通量；动量方程中的 $\rho u_i u_j$ 表示动量的对流输运，而 $p \delta_{ij}$ 是作用在控制体表面上的压力；能量方程中的 $(\rho E + p) u_j$ 代表总能量的输运，其中包含了总焓 $(\rho E + p)$ 的平流。

**粘性通量 (Viscous Flux)** $F^v(U, \nabla U)$ 代表由粘性应力和热传导引起的扩散输运。质量守恒方程没有粘性项。在 $j$ 方向上的粘性通量向量为：
$$
F^v_j(U, \nabla U) \;=\; \begin{pmatrix} 0 \\ \tau_{1j} \\ \tau_{2j} \\ \tau_{3j} \\ \sum_{k=1}^3 \tau_{kj} u_k - q_j \end{pmatrix}
$$
其中，$\boldsymbol{\tau}$ 是 **粘性应力张量 (viscous stress tensor)**，$\boldsymbol{q}$ 是 **热通量向量 (heat flux vector)**。能量方程中的 $\sum_k \tau_{kj} u_k$ 代表粘性力所做的功，而 $-q_j$ 是通过热传导进入控制体的能量。

**源项 (Source Term)** $S$ 包含了体积力（如重力）和体积热源。
$$
S \;=\; \begin{pmatrix} 0 \\ \rho f_1 \\ \rho f_2 \\ \rho f_3 \\ \rho \boldsymbol{f} \cdot \boldsymbol{u} + s_Q \end{pmatrix}
$$
其中，$\boldsymbol{f}$ 是单位质量的体积力， $s_Q$ 是单位体积的热量增加率。

### 变量集与热力学关系

在求解Navier-Stokes方程时，我们通常在两套变量之间切换：**守恒变量 (conservative variables)** $U$ 和 **原始变量 (primitive variables)** $W$。守恒变量是守恒定律的直接对象，而原始变量，如密度、速度和压力 $(\rho, \boldsymbol{u}, p)$ 或温度 $(\rho, \boldsymbol{u}, T)$，具有更直观的物理意义，并且粘性通量和热力学关系通常以它们为函数更易于表达 [@problem_id:3376445]。

对于量热完全理想气体（calorically perfect ideal gas），这些变量通过一系列热力学关系联系在一起。例如，状态方程为 $p=\rho R T$，其中 $R$ 是气体常数。单位质量内能 $e$ 仅是温度的函数，$e=c_v T$，其中 $c_v$ 是定容比热。总能量 $E$ 随之确定为 $E = c_v T + \frac{1}{2}|\boldsymbol{u}|^2$。

选择一组独立的原始变量，例如 $W = (\rho, \boldsymbol{u}, T)$，我们可以在物理允许的范围内（$\rho > 0, T > 0$）建立 $W$ 与 $U$ 之间的一一对应、光滑且可逆的映射关系。这种映射的存在性与非奇异性是至关重要的，尤其是在隐式DG方法中。隐式方法需要求解线性系统，其中涉及到通量对守恒变量的雅可比矩阵 $\frac{\partial F}{\partial U}$。由于通量 $F$ 通常更容易表示为原始变量 $W$ 的函数，我们可以利用链式法则来计算这个雅可比矩阵：
$$
\frac{\partial F}{\partial U} = \frac{\partial F}{\partial W} \frac{\partial W}{\partial U}
$$
其中，$\frac{\partial W}{\partial U}$ 是映射 $U \mapsto W$ 的雅可比矩阵，它等于 $\left(\frac{\partial U}{\partial W}\right)^{-1}$。对于物理上有效的状态，这个雅可比矩阵是存在的且非奇异的 [@problem_id:3376445]。

### 对流项的离散化：数值通量

DG方法的核心思想是在每个单元上使用分片多项式来逼近解，并允许解在单元边界上存在间断。将守恒律方程乘以一个测试函数 $\phi_h$，在单元 $K$ 上分部积分，可以得到DG的半离散格式：
$$
\int_K \frac{\partial U_h}{\partial t} \phi_h \, dV = \int_K F^c(U_h) : \nabla \phi_h \, dV - \int_{\partial K} \hat{F}^c_n \phi_h \, dS + \dots
$$
（此处省略了粘性项和源项）。上式中的边界积分项出现了一个新的量 $\hat{F}^c_n$，即 **数值通量 (numerical flux)**。由于单元边界上的解 $U_h$ 是双值的（来自相邻两个单元），物理通量 $F^c(U_h)\cdot\boldsymbol{n}$ 也是不确定的。数值通量的作用就是提供一个在界面上单值的、物理上合理的通量，以耦合相邻的单元。

一个有效的数值通量必须满足两个基本属性 [@problem_id:3376501]：
1.  **相容性 (Consistency)**：当界面两侧的状态相同时 ($U_L = U_R = U$)，数值通量必须退化为物理通量，即 $\hat{F}^c_n(U, U) = F^c(U)\cdot\boldsymbol{n}$。
2.  **守恒性 (Conservation)**：对于共享同一界面的两个相邻单元，从一个单元流出的通量必须等于流入另一个单元的通量。

数值通量的选择直接影响到格式的稳定性和精度。常见选择包括：

*   **Lax-Friedrichs (或 Rusanov) 通量**：这是一种构造简单且非常鲁棒的通量。其形式为界面两侧物理通量的平均值，再减去一个与解的跳变 $[U] = U_R - U_L$ 成正比的数值耗散项 [@problem_id:3376449]。
    $$
    \hat{F}^c_n = \frac{1}{2} \left( F^c_n(U_L) + F^c_n(U_R) \right) - \frac{1}{2} \alpha_{\max} (U_R - U_L)
    $$
    其中，耗散系数 $\alpha_{\max}$ 取为界面两侧法向最大特征波速。这种通量虽然稳定，但耗散较大，可能会过度抹平接触间断等精细结构。

*   **Roe 通量**：这是一种基于近似黎曼问题求解器的通量，它通过对界面处的雅可比矩阵进行局部线性化来构造。Roe通量引入的数值耗散更具物理性，只在真正需要的地方（如激波）添加耗散。其一个显著优点是能够精确地解析孤立的、与网格对齐的间断，包括静止的接触间断。然而，它需要一个所谓的“熵修正”来处理声速点附近的非物理现象 [@problem_id:3376501]。

*   **HLLC 通量**：HLLC（Harten-Lax-van Leer-Contact）通量是对HLL通量的改进，它在黎曼扇形结构中显式地重构了中间的接触波。这使得HLLC通量在保持鲁棒性的同时，能够精确地解析接触间断和剪切波，这对于许多空气动力学问题至关重要 [@problem_id:3376501]。

与之相对，无耗散的中心通量（即简单地取两侧通量的平均值）会导致格式不稳定，因为它无法抑制非线性计算中产生的高频振荡。

### 粘性项的离散化：挑战与对策

粘性项 $\nabla \cdot F^v(U, \nabla U)$ 的离散化比对流项更为复杂，因为它涉及解的梯度，是一个二阶导数项。在DG框架下，由于解$U_h$在单元间是间断的，其梯度 $\nabla U_h$ 在界面上没有良好定义，这使得粘性通量 $F^v$ 的值变得模糊不清 [@problem_id:3376502]。处理这一挑战主要有两种策略。

#### 粘性应力张量与Stokes假设

在深入探讨离散化方法之前，我们首先需要明确粘性应力张量 $\boldsymbol{\tau}$ 的具体形式。对于牛顿流体，粘性应力与应变率张量 $D_{ij} = \frac{1}{2}(\partial_i u_j + \partial_j u_i)$ 呈线性关系。最一般的各向同性关系包含两个粘性系数：剪切粘性系数 $\mu$ 和第二粘性系数 $\lambda$。
$$
\tau_{ij} = \mu \left( \partial_i u_j + \partial_j u_i \right) + \lambda (\nabla \cdot \boldsymbol{u}) \delta_{ij}
$$
通常，我们引入 **体积粘性系数 (bulk viscosity)** $\zeta = \lambda + \frac{2}{3}\mu$。**Stokes 假设** 是一个广泛应用的简化，它假定 $\zeta = 0$，即 $\lambda = -\frac{2}{3}\mu$。在该假设下，粘性应力张量的迹 $\tau_{kk}$ 恒为零。这一假设会影响流体对压缩和膨胀的阻尼效应。对速度场进行平面波分析可以发现，剪切（横向）模式的耗散系数为 $\mu$，而膨胀（纵向）模式的耗散系数为 $\zeta + \frac{4}{3}\mu$。因此，Stokes假设将纵向模式的耗散从 $\zeta + \frac{4}{3}\mu$ 减小到 $\frac{4}{3}\mu$ [@problem_id:3376443]。这在设计罚参数时需要予以考虑。

#### 策略一：混合格式 (Mixed Formulations)

混合格式的核心思想是将原始的二阶问题转化为一个等价的、更大的 **一阶系统**。这是通过引入一个辅助变量（通常记为 $\boldsymbol{Q}$）来代表主变量的梯度，例如 $\boldsymbol{Q} \approx \nabla U$。原来的二阶方程被替换为两个一阶方程组：
$$
\boldsymbol{Q} - \nabla U = \mathbf{0}
$$
$$
\partial_t U + \nabla \cdot F^c(U) - \nabla \cdot F^v(U, \boldsymbol{Q}) = \mathbf{0}
$$
现在，粘性通量 $F^v$ 仅依赖于 $U$ 和新的辅助变量 $\boldsymbol{Q}$，而不再直接依赖于 $\nabla U$。对这个一阶系统应用DG方法，我们可以在单元界面上为 $U$ 和 $\boldsymbol{Q}$ 分别定义单值的数值通量。这种做法的精妙之处在于，它通过引入辅助变量，使得整个粘性项的离散化过程恢复了守恒性，即在全域网格上求和时，内部界面的通量贡献能够精确抵消。著名的 **局部间断Galerkin (LDG)** 方法和 **Bassi-Rebay 2 (BR2)** 格式都是这种思想的体现 [@problem_id:3376502]。

#### 策略二：内部罚方法 (Interior Penalty Methods)

内部罚方法是另一种不引入辅助变量的直接方法。其基本思想是在标准的Galerkin离散（分部积分一次）的基础上，通过在单元界面上添加额外的项来保证稳定性和对称性。以 **对称内部罚Galerkin (SIPG)** 方法为例，其双线性形式包含三个部分 [@problem_id:3376476]：
1.  **标准Galerkin项**：来自单元内积分和界面上通量平均值的项。
2.  **对称项**：为了使最终的离散算子对称，添加一个与标准Galerkin边界项“共轭”的项。
3.  **罚项 (Penalty Term)**：一个与解在界面上的跳变（jump）的平方成正比的项，写作 $\sigma [U][\phi]$。这个罚项的作用是惩罚解的间断，从而将相邻单元“拉”在一起，保证离散算子的正定性（或强制性），进而保证格式的稳定性。

对于粘性项，SIPG的双线性形式可以概括为：
$$
a(\boldsymbol{u},\boldsymbol{v}) = \sum_{K} \int_K \boldsymbol{\tau}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\boldsymbol{v}) dV - \sum_{F} \int_F \left( \{\boldsymbol{\tau}(\boldsymbol{u})\boldsymbol{n}\} \cdot [\boldsymbol{v}] + \{\boldsymbol{\tau}(\boldsymbol{v})\boldsymbol{n}\} \cdot [\boldsymbol{u}] \right) dS + \sum_{F} \int_F \sigma_u [\boldsymbol{u}] \cdot [\boldsymbol{v}] dS
$$
其中 $\{ \cdot \}$ 和 $[ \cdot ]$ 分别代表界面上的平均和跳变算子。**罚参数 (penalty parameter)** $\sigma_u$ 的选择至关重要。理论分析表明，为保证稳定性，$\sigma_u$ 必须足够大，其大小需要与多项式次数 $p$ 的平方成正比，与单元尺寸 $h$ 成反比，即 $\sigma_u \sim O(p^2/h)$ [@problem_id:3376476] [@problem_id:3376446]。

### 实现细节与实践考量

#### 节点型DG与参考单元

现代DG方法，特别是高阶方法，通常在 **参考单元 (reference element)** （如一维的 $[-1,1]$ 或二维的 $[-1,1]^2$）上进行构建。物理单元通过一个可逆的映射 $\boldsymbol{x}(\boldsymbol{\xi})$ 与参考单元相关联。在节点型DG方法中，解在参考单元上由其在一组预先定义的节点（如Gauss-Lobatto节点）上的值来表示和存储。

计算梯度是粘性项离散化的关键步骤。在节点型DG中，这可以通过 **微分矩阵 (differentiation matrix)** 高效完成。对于一维参考单元上的节点，可以构造一个微分矩阵 $D$，使得向量化的节点值乘以 $D$ 便能得到导数在这些节点上的值。对于二维或三维的张量积单元，可以通过对每个维度依次应用一维微分矩阵来计算偏导数 [@problem_id:3376458]。

得到参考坐标系下的梯度 $\nabla_{\boldsymbol{\xi}} U$ 后，需要通过链式法则和映射的雅可比矩阵 $J = \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{\xi}}$ 将其转换到物理坐标系下的梯度：
$$
\nabla_{\boldsymbol{x}} U = (J^{-1})^T \nabla_{\boldsymbol{\xi}} U
$$

#### 数值积分与非线性不稳定性

DG弱形式中的积分，特别是涉及非线性通量项的积分，通常无法解析计算，必须采用 **数值积分 (numerical quadrature)** （如Gauss积分）。积分的精度对DG格式的稳定性和精度有深远影响。

考虑对流通量项的体积积分 $\int_K \boldsymbol{F}^c(U_h) : \nabla \phi_h \, dV$。如果解 $U_h$ 和测试函数 $\phi_h$ 都是 $p$ 次多项式，那么 $\nabla \phi_h$ 是 $p-1$ 次多项式。对于Euler方程，$\boldsymbol{F}^c(U_h)$ 是 $U_h$ 的二次函数，因此被积函数是 $2p + (p-1) = 3p-1$ 次多项式。为了精确计算此积分，Gauss积分规则需要至少 $\lceil (3p-1+1)/2 \rceil = \lceil 3p/2 \rceil$ 个积分点 [@problem_id:3376487]。

如果使用的积分点数不足（例如，仅使用 $p+1$ 个点，这在节点DG中很常见），就会发生 **欠积分 (under-integration)**。欠积分会导致 **混淆误差 (aliasing error)**，高频的非线性乘积模式被错误地表示为低频模式。对于非线性双曲问题，这种误差会破坏离散格式的内在守恒性质（如动能或熵的守恒），从而引发 **非线性不稳定性**。这种不稳定性通常表现为计算过程中能量的无界增长，最终导致模拟失败。

需要强调的是，即使在界面上使用了具有耗散性的数值通量（如Rusanov或Roe通量），也往往不足以抑制由体积积分欠积分引起的非线性不稳定性。因此，为了保证高阶DG格式在求解非线性问题时的鲁棒性，必须采用以下策略之一：
1.  **过积分 (Over-integration)** 或 **去混淆 (De-aliasing)**：使用足够多的积分点来精确计算非线性项的积分。
2.  采用 **分裂形式 (Split-form)** 或 **保熵 (Entropy-stable)** 的DG格式：这些特殊构造的格式在离散层面也能保持某些守恒性质，即使在欠积分的情况下也能保持稳定。

### 收敛性分析

最后，我们关心DG方法的精度。对于具有足够光滑真解 $U$ 的问题，一个设计良好的DG格式（即相容、稳定且使用了恰当的数值通量和罚参数）可以达到最优的收敛阶。对于使用 $p$ 次多项式的DG方法，其在 $L^2$ 范数下的误差期望为：
$$
\| U(\cdot, T) - U_h(\cdot, T) \|_{L^2(\Omega)} \le C h^{p+1}
$$
其中 $h$ 是网格的特征尺寸。这表示当网格加密时，误差会以 $h$ 的 $p+1$ 次幂迅速减小 [@problem_id:3376446]。

误差常数 $C$ 依赖于真解的光滑度、网格的质量、粘性系数等，同时也受到数值格式具体参数的影响。例如，对流通量中的数值耗散大小、内部罚方法中的罚参数大小，都会影响稳定性证明中的常数，从而改变 $C$ 的值。然而，只要这些参数的选择保证了格式的相容性和稳定性，它们通常只影响误差的大小（常数 $C$），而不会改变误差随网格尺寸减小的渐近收敛阶（$p+1$）。