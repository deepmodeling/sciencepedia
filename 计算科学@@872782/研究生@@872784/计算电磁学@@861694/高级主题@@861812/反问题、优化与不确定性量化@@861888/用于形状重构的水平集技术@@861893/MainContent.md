## 引言
在计算科学与工程领域，从外部测量数据中重构或设计物体几何形状是一个基础而又充满挑战的[逆问题](@entry_id:143129)。无论是医学成像、[无损检测](@entry_id:273209)还是[超材料设计](@entry_id:184616)，精确控制和识别复杂形状的能力都至关重要。水平集（level-set）方法为此类问题提供了一个强大而灵活的计算框架，尤其擅长处理演化过程中可能发生的复杂[拓扑变化](@entry_id:136654)。传统方法在处理形状的合并、分裂或产生新孔洞时常遇到困难，而[基于梯度的优化](@entry_id:169228)方法如何高效地计算形状对[目标函数](@entry_id:267263)（如[数据失配](@entry_id:748209)）的敏感度，是实现稳健反演的关键瓶颈。

本文旨在系统性地介绍用于形状重构的[水平集](@entry_id:751248)技术。读者将首先在“原理与机制”一章中，深入学习该方法的核心：如何用[水平集](@entry_id:751248)函数表示形状，如何将[优化问题](@entry_id:266749)构建为梯度流，以及如何利用伴随状态法高效计算形状梯度。接着，在“应用与跨学科交叉”一章中，我们将展示该框架如何应用于电磁[逆散射](@entry_id:182338)、[周期结构](@entry_id:753351)重构、[超材料设计](@entry_id:184616)，乃至与机器学习前沿相结合，凸显其广泛的适用性。最后，“动手实践”部分将通过一系列具体的编程练习，引导读者将理论知识转化为实际的计算能力，巩固对核心概念的理解。这套结构化的学习路径将带领读者从理论基础出发，逐步拓展到前沿应用，最终通过实践掌握这一强大的[形状优化](@entry_id:170695)工具。

## 原理与机制

本章深入探讨了用于电磁学中形状重构的水平集（level-set）技术的基本原理和核心机制。在上一章“引言”的基础上，我们将不再赘述背景，而是直接进入该方法的技术核心。我们将从形状的数学表示出发，阐述如何将形状反演问题转化为一个[梯度流](@entry_id:635964)[优化问题](@entry_id:266749)，并详细推导计算该梯度最关键的工具——伴随状态法（adjoint-state method）。此外，本章还将讨论数值实现中的关键方面、数据完备性的重要性以及提高[计算效率](@entry_id:270255)的高级策略。

### 形状的[水平集](@entry_id:751248)表示

在[形状优化](@entry_id:170695)和反演问题中，首要的挑战是如何在计算上灵活地表示和演化一个几何体的边界。[水平集方法](@entry_id:165633)通过一个更高维度的辅助函数——**[水平集](@entry_id:751248)函数** $\phi(\mathbf{x})$ ——来隐式地表示一个形状，从而优雅地解决了这个问题。

#### 基本定义

给定一个定义在某个计算域 $\mathcal{D} \subset \mathbb{R}^d$ 上的标量函数 $\phi: \mathcal{D} \to \mathbb{R}$，我们可以定义一个区域 $\Omega$ 及其边界 $\partial\Omega$ 如下：
$$
\begin{align*}
\Omega = \{\mathbf{x} \in \mathcal{D} : \phi(\mathbf{x})  0\} \\
\partial\Omega = \{\mathbf{x} \in \mathcal{D} : \phi(\mathbf{x}) = 0\} \\
\mathcal{D} \setminus \bar{\Omega} = \{\mathbf{x} \in \mathcal{D} : \phi(\mathbf{x}) > 0\}
\end{align*}
$$
按照惯例，$\phi$ 的负值区域代表形状的内部，正值区域代表外部，而**零[水平集](@entry_id:751248)**则精确地描绘了形状的边界。这种表示方法的一大优势在于其拓扑灵活性：即使 $\Omega$ 在演化过程中经历合并或分裂，$\phi$ 函数本身仍然保持为一个定义在整个网格上的单值函数，从而极大地简化了数值处理。

为了在物理模型（如 Maxwell [方程组](@entry_id:193238)）中描述不同区域的材料属性，我们可以使用 **Heaviside 函数** $H(s)$。例如，一个具有内部[介电常数](@entry_id:146714) $\varepsilon_{\mathrm{in}}$ 和外部[介电常数](@entry_id:146714) $\varepsilon_{\mathrm{out}}$ 的物体可以被描述为：
$$
\varepsilon(\mathbf{x}) = \varepsilon_{\mathrm{in}} (1 - H(\phi(\mathbf{x}))) + \varepsilon_{\mathrm{out}} H(\phi(\mathbf{x}))
$$
或者等价地：
$$
\varepsilon(\phi(\mathbf{x})) = \varepsilon_{\mathrm{in}} + (\varepsilon_{\mathrm{out}} - \varepsilon_{\mathrm{in}}) H(\phi(\mathbf{x}))
$$
然而，标准的 Heaviside 函数在原点处不连续，这给[基于梯度的优化](@entry_id:169228)带来了困难。因此，在实践中，我们通常使用一个**平滑的 Heaviside 函数** $H_\beta(s)$，它在一个宽度为 $2\beta$ 的窄带内从 $0$ 平滑过渡到 $1$。其导数是一个**平滑的 Dirac delta 函数** $\delta_\beta(s)$，它在过渡带之外为零 [@problem_id:3323749]。这种平滑处理使得[介电常数](@entry_id:146714) $\varepsilon$ 对水平集函数 $\phi$ 可微，这是应用伴随法的先决条件。

#### 多材料表示

[水平集方法](@entry_id:165633)可以自然地推广到表示多个材料区域。使用一个**向量[水平集](@entry_id:751248)函数** $(\phi_1, \phi_2, \dots, \phi_{N-1})$，我们可以区分 $N$ 种不同的材料。例如，对于包含三种材料（[介电常数](@entry_id:146714)分别为 $\varepsilon_1, \varepsilon_2, \varepsilon_3$）的场景，我们可以使用两个[水平集](@entry_id:751248)函数 $(\phi_1, \phi_2)$ [@problem_id:3323758]。关键在于构造一组**[单位分解](@entry_id:150115)**（partition of unity）权重函数 $\{\chi_i(\phi_1, \phi_2)\}_{i=1}^3$，它们满足：
$$
\chi_i \ge 0 \quad \forall i, \quad \text{and} \quad \sum_{i=1}^3 \chi_i(\phi_1, \phi_2) = 1
$$
一种有效构造方式是采用分层逻辑：$\phi_1$ 用于区分背景材料（例如相3）和两种前景材料（相1和相2），而 $\phi_2$ 则在前景区域内区分相1和相2。使用平滑 Heaviside 函数 $H_1 = H_\beta(\phi_1)$ 和 $H_2 = H_\beta(\phi_2)$，权重可以定义为：
$$
\begin{aligned}
\chi_1(\phi_1, \phi_2) = H_1 (1 - H_2) \\
\chi_2(\phi_1, \phi_2) = H_1 H_2 \\
\chi_3(\phi_1, \phi_2) = 1 - H_1
\end{aligned}
$$
于是，[介电常数](@entry_id:146714)[分布](@entry_id:182848)就成为这些权重的[线性组合](@entry_id:154743)：
$$
\varepsilon(\phi_1, \phi_2) = \varepsilon_1 \chi_1 + \varepsilon_2 \chi_2 + \varepsilon_3 \chi_3 = \varepsilon_3 + (\varepsilon_1 - \varepsilon_3)H_1 + (\varepsilon_2 - \varepsilon_1)H_1 H_2
$$
这种表示法允许我们使用与单材料问题类似的梯度优化框架来处理更复杂的多材料反演问题。

### [形状优化](@entry_id:170695)作为[梯度流](@entry_id:635964)

形状重构的目标是找到一个能最佳解释观测数据的形状。这可以被形式化为一个[优化问题](@entry_id:266749)：寻找能最小化某个**[代价泛函](@entry_id:268062)** (cost functional) $J$ 的水平集函数 $\phi$。[代价泛函](@entry_id:268062)通常定义为模拟数据与测量数据之间的失配度，例如 $L^2$ 范数的平方：
$$
J(\phi) = \frac{1}{2} \sum_{m=1}^M |u(x_m; \phi) - d_m|^2
$$
其中 $u(x_m; \phi)$ 是在 $m$ 个接收器位置 $x_m$ 处、由与 $\phi$ 对应的形状产生的模拟场，而 $d_m$ 是相应的测量数据 [@problem_id:3323747]。

为了最小化 $J(\phi)$，我们采用梯度下降的思想。我们将水平集函数 $\phi$ 视为一个随“时间” $t$ 演化的函数，并寻求一种演化方式，使得 $J$ 随时间下降最快。这种演化由一个 **Hamilton-Jacobi 方程** 描述：
$$
\frac{\partial \phi}{\partial t} + V_n |\nabla \phi| = 0
$$
这里，$V_n$ 是边界 $\partial\Omega$ 在其[法线](@entry_id:167651)方向上的演化速度。我们的核心任务是找到一个[速度场](@entry_id:271461) $V_n$，使得它指向 $J$ 的最速下降方向。这种将形状演化视为最小化泛函的[梯度流](@entry_id:635964)的方法，是水平集[形状优化](@entry_id:170695)框架的基石。

### 用于形状敏感度分析的伴随状态法

直接计算[代价泛函](@entry_id:268062) $J$ 对水平集函数 $\phi$ 的梯度是极其困难的，因为 $\phi$ 的微小变化会通过求解一个[偏微分方程](@entry_id:141332)（如 Helmholtz 方程）传递给场 $u$，进而影响 $J$。**伴随状态法**（Adjoint-State Method）是一种强大的技术，它能够以极高的效率计算这个梯度，而无需显式地计算场对 $\phi$ 的导数。

伴随法的核心思想是引入一个**伴随场** (adjoint field) $p$，它满足一个与原物理问题（我们称之为**正向问题**）密切相关的**伴随方程**。通过巧妙地运用 Lagrangian 泛函和格林第二定理，我们可以将 $J$ 对 $\phi$ 的导数表示为正向场 $u$ 和伴随场 $p$ 的某种乘积的积分。

#### 连续公式：边界敏感度

考虑一个 TE 极化的二维散射问题，[电场](@entry_id:194326) $u$ 满足 Helmholtz 方程。我们可以推导出[代价泛函](@entry_id:268062) $J$ 对形状边界法向微小扰动的敏感度 [@problem_id:3323747]。首先，我们定义一个伴随场 $p$，它满足与 $u$ 相同的 Helmholtz 算子，但其[源项](@entry_id:269111)由数据残差（即模拟数据与测量数据之差）在接收器位置处的 Dirac delta 函数构成：
$$
\nabla \cdot \left(\frac{1}{\mu_0}\nabla p(x)\right) + \omega^2 \varepsilon(x) p(x) = \sum_{m=1}^M \left(u(x_m;\phi) - d_m\right) \delta(x - x_m)
$$
注意，伴随源项的具体形式（例如是否取共轭）取决于[代价泛函](@entry_id:268062)和所使用的[内积](@entry_id:158127)的定义，但其物理意义始终是“将误差反向传播回计算域”。

通过一系列推导，可以证明 $J$ 对时间的变化率 $\frac{dJ}{dt}$ 可以表示为一个边界积分：
$$
\frac{dJ}{dt} = \int_{\partial\Omega} V_n(\mathbf{s}) G(u, p, \mathbf{s}) \, d\mathbf{s}
$$
其中 $G(u, p, \mathbf{s})$ 是一个依赖于正向场 $u$ 和伴随场 $p$ 在边界 $\partial\Omega$ 上的值的**敏感度核**。为了实现最速下降，我们应选择 $V_n$与敏感度核 $G$ 符号相反，即 $V_n \propto -G$。对于上述[电磁散射](@entry_id:182193)问题，可以证明最速下降的法向速度为 [@problem_id:3323747]：
$$
V_n(\mathbf{x}) = -C \cdot \operatorname{Re}\! \left( u(\mathbf{x};\phi)\,\overline{p(\mathbf{x};\phi)} \right) \quad \text{for } \mathbf{x} \in \partial\Omega
$$
其中 $C$ 是一个包含物理参数（如频率 $\omega$ 和[介电常数](@entry_id:146714)跳变 $\varepsilon_{\mathrm{e}} - \varepsilon_{\mathrm{i}}$）的正常数。这个优美的公式是形状反演的核心：**边界的移动速度由该处正向场和伴随场的乘积的实部决定**。这个结果也被称为 **Hadamard 边界积分表示** [@problem_id:3323745]。

#### 离散公式：体积敏感度

另一种视角是使用平滑的 Heaviside 函数 $H_\beta(\phi)$。此时，[介电常数](@entry_id:146714) $\varepsilon(\phi)$ 在整个计算域内都是可微的。我们可以直接计算 $J$ 对离散网格上每个点的 $\phi$ 值的导数。这个梯度是一个体积量，但由于 $\frac{\partial\varepsilon}{\partial\phi} \propto \delta_\beta(\phi)$，它只在零水平集周围的窄带内非零 [@problem_id:3323749]。

使用离散化的[拉格朗日乘子法](@entry_id:176596)，我们可以推导出 $J$ 对每个网格点 $j$ 处的[介电常数](@entry_id:146714) $\varepsilon_{r,j}$ 的梯度：
$$
\frac{\partial J}{\partial \varepsilon_{r,j}} = \operatorname{Re}\left( k_0^2 \, h^2 \, \overline{p_j} \, u_j \right)
$$
其中 $u_j$ 和 $p_j$ 分别是该点的正向场和伴随场值，$k_0$ 是自由空间波数，$h$ 是网格间距。

然后，利用链式法则，我们得到 $J$ 对 $\phi_j$ 的梯度：
$$
\mathcal{G}_j = \frac{\partial J}{\partial \phi_j} = \frac{\partial J}{\partial \varepsilon_{r,j}} \frac{\partial \varepsilon_{r,j}}{\partial \phi_j} = \frac{\partial J}{\partial \varepsilon_{r,j}} \cdot (\varepsilon_{\mathrm{in}} - \varepsilon_{\mathrm{out}}) \delta_\beta(\phi_j)
$$
这个梯度 $\mathcal{G}_j$可以直接用于更新[水平集](@entry_id:751248)函数，例如通过简单的[梯度下降](@entry_id:145942)步骤：$\phi^{k+1} = \phi^k - \alpha \mathcal{G}$，其中 $\alpha$ 是步长。

### 数值实现与实际考量

将上述理论转化为可靠的算法需要关注几个关键的数值问题。

#### 求解水平集演化方程

Hamilton-Jacobi 方程 $\frac{\partial \phi}{\partial t} + V_n |\nabla \phi| = 0$ 是一种[对流](@entry_id:141806)方程，数值求解时容易产生不稳定性和[振荡](@entry_id:267781)。简单的[中心差分格式](@entry_id:747203)通常不适用。为了保证解的稳定性和物理正确性，必须使用**迎风格式** (upwind schemes)，如 Godunov 格式或 Engquist-Osher 格式 [@problem_id:3323768]。这类格式会根据速度场 $V_n$ 的符号（即信息传播的方向）来选择单侧差分，从而正确地捕捉解的传播特性。

此外，为了使演化过程更平滑，避免产生尖角或不规则形状，常常在演化方程中加入一个**曲率正则化项**：
$$
\frac{\partial \phi}{\partial t} + V_n |\nabla \phi| = \mu \kappa(\phi) |\nabla \phi|
$$
其中 $\kappa(\phi) = \nabla \cdot (\frac{\nabla\phi}{|\nabla\phi|})$ 是[水平集](@entry_id:751248)的[平均曲率](@entry_id:162147)，$\mu$ 是正则化参数。该项的作用类似于表面张力，会使边界趋于平滑 [@problem_id:3323768]。

在长[时间演化](@entry_id:153943)后，水平集函数 $\phi$ 可能会偏离其作为**[符号距离函数](@entry_id:754834)** (signed distance function, SDF) 的性质（即 $|\nabla\phi|=1$）。这会导致数值误差累积。因此，需要周期性地对 $\phi$进行**重新初始化** (reinitialization)，将其重置为一个保持零水平集不变的[符号距离函数](@entry_id:754834)。高效的重新初始化算法包括**[快速行进法](@entry_id:749232)** (Fast Marching Method, FMM) [@problem_id:3323789]。

#### 数据完备性与唯一性

反演问题的解的质量和唯一性严重依赖于测量数据的“丰富性”。一个关键问题是：我们需要什么样的实验配置才能唯一地重构一个形状？[@problem_id:3323753]

从理论上看，这取决于线性化的正向散射算子（将形状的微小扰动映射到散射数据的变化）是否是单射的（即没有非平凡的零空间）。如果存在某些形状扰动不会产生任何散射信号，那么这些扰动就是“不可见的”，反演问题就没有唯一解。

对于[电磁散射](@entry_id:182193)问题，分析表明，为了唯一重构一个三维物体，通常需要 [@problem_id:3323753]：
1.  **多方向入射**：从多个不同方向照射物体，以“照亮”其所有側面。单一方向的入射波只能提供物体在傅里葉空间中某个球面上的信息，这不足以确定其完整形状。
2.  **多极化**：对于矢量[电磁波](@entry_id:269629)，每个入射方向需要使用两个正交的极化方式。这可以消除由于特定极化方向与散射方向对齐而导致的信息丢失。
3.  **全孔径测量**：在物体周围尽可能大的角度范围内测量散射场。

我们可以使用 **[Fisher 信息](@entry_id:144784)** 和 **Cramér-Rao 界** (CRB) 来量化地评估数据对特定形状参数（例如半径）的敏感度 [@problem_id:3323775]。Fisher 信息衡量了数据中包含的关于未知参数的[信息量](@entry_id:272315)。更多的入射波或更优的实验配置会增加 [Fisher 信息](@entry_id:144784)，从而降低[参数估计](@entry_id:139349)[方差](@entry_id:200758)的理论下限（CRB），意味着可以实现更精确的重构。

### 计算效率策略

大规模三维形状反演的计算量是巨大的。每次迭代都需要求解多次大型[偏微分方程](@entry_id:141332)（正向和伴随问题）。因此，开发高效的计算策略至关重要。

#### 利用互易性加速伴随求解

在标准的伴随法中，如果有 $P$ 个独立的入射源，我们就需要进行 $P$ 次正向求解（每个源一次）和 $P$ 次伴随求解（每个源的误差[反向传播](@entry_id:199535)一次）。当源的数量非常多时，这会成为计算瓶頸。

然而，如果物理系统满足**互易性**（reciprocity），即格林函数是对称的，我们可以极大地减少计算量 [@problem_id:3323776]。我们可以不为每个源求解一个伴随问题，而是为每个接收器 $m$（共 $M$ 个）求解一个“接收器场” $w_m$。这个 $w_m$ 满足一个正向类型的方程，其源项是第 $m$ 个传感器的空间响应函数。

通过推导可以证明，每个源 $p$ 对应的伴随场 $\lambda_p$ 可以表示为所有接收器场 $w_m$ 的[线性组合](@entry_id:154743)，其系数为数据残差 $r_{p,m}$：
$$
\lambda_p = \sum_{m=1}^M r_{p,m} w_m
$$
这样，计算梯度所需的总求解次数从 $P$ 次正向 + $P$ 次伴随，变成了 $P$ 次正向 + $M$ 次接收器场求解。在许多应用中（如[地震成像](@entry_id:273056)或全息成像），源的数量 $P$ 远大于接收器数量 $M$，因此这种方法可以带来[数量级](@entry_id:264888)的加速 [@problem_id:3323776]。

#### 算法复杂性与加速技术

除了利用物理特性，我们还可以从算法层面进行优化 [@problem_id:3323789]。
*   **场求解器**：对于自由空间或均匀背景下的散射问题，基于[积分方程](@entry_id:138643)的方法非常有效。正向和伴随求解本质上是卷积运算。朴素的[离散卷积](@entry_id:160939)在 $N$ 个网格点的系统上复杂度为 $\mathcal{O}(N^2)$，而使用**快速傅里叶变换** (FFT) 可以将其降至 $\mathcal{O}(N \log N)$。
*   **窄带法**：[水平集](@entry_id:751248)梯度和更新计算在理论上只需要在零水平集附近进行。**窄带法** (Narrow-band methods) 将计算限制在一个围绕零水平集、宽度有限的窄带内，从而将梯度计算和重新初始化的复杂度从与总体积 $N$ 相关降低到与边界长度（二维）或面积（三维）相关，例如 $\mathcal{O}(\sqrt{N})$ 或 $\mathcal{O}(N^{2/3})$。
*   **[快速行进法 (FMM)](@entry_id:749233)**：如前所述，FMM 是一种高效的重新初始化算法，其复杂度为 $\mathcal{O}(N \log N)$，远优于简单的迭代求解方法。

综合运用 FFT 卷积、窄带技术和 FMM 等方法，可以将水平集形状反演的每次迭代成本从不可接受的 $\mathcal{O}(S N^2)$ 降低到更易于管理的 $\mathcal{O}(S N \log N + \dots)$，使得处理大规模实际问题成为可能 [@problem_id:3323789]。