## 引言
在物理学的发展历程中，爱因斯坦的狭义相对论彻底改变了我们对时间、空间和物质的基本认知。然而，这一新理论的诞生也带来了一个严峻的挑战：如何使经典电磁理论——由[麦克斯韦方程组](@entry_id:150940)完美描述的宏伟理论体系——与相对论原理相协调？经典表述中的[电场](@entry_id:194326) $\vec{E}$ 和[磁场](@entry_id:153296) $\vec{B}$ 被视为独立的矢量场，它们的变换规律复杂，且[麦克斯韦方程组的形式](@entry_id:189625)在[洛伦兹变换](@entry_id:176827)下并非显而易见地保持不变。这一知识上的鸿沟促使物理学家寻求一种更深刻、更内在的数学语言来描述电磁现象。

本文旨在系统阐述解决这一核心问题的关键概念：电磁场张量 $F^{\mu\nu}$。这一强大的数学工具不仅是技术上的简化，更是概念上的飞跃，它将电场和磁场统一为单一的四维时空实体，从而使整个电[动力学理论](@entry_id:136901)呈现出优美的洛伦兹协变形式。通过学习本文，读者将深入理解[电磁场](@entry_id:265881)的相对论性本质。

在接下来的章节中，我们将分步揭示电磁场张量的奥秘。第一章“原理与机制”将详细介绍[场张量](@entry_id:186486)的定义、其与[四维势](@entry_id:188407)的关系、[规范不变性](@entry_id:137857)，并展示如何用它来重铸[麦克斯韦方程组](@entry_id:150940)。第二章“应用与跨学科联系”将探讨[场张量](@entry_id:186486)在[带电粒子](@entry_id:160311)动力学、[连续介质力学](@entry_id:155125)以及现代[规范场](@entry_id:159627)论等领域的广泛应用。最后，在“动手实践”部分，您将有机会通过解决具体问题来巩固所学知识。让我们首先从构建[电磁场张量](@entry_id:158921)的基本原理开始。

## 原理与机制

在狭义相对论的框架下，我们对电场和磁场的理解发生了根本性的变革。[电场](@entry_id:194326) $\vec{E}$ 和[磁场](@entry_id:153296) $\vec{B}$ 不再是各自独立的实体，而是统一的四维[时空几何](@entry_id:139497)对象——电磁场张量 $F^{\mu\nu}$ 的不同侧面。本章将系统地阐述该张量的定义、性质及其在电动力学中的核心作用。

### 电磁场张量的定义

为了在相对论的四维时空中描述电磁现象，我们需要一个能正确地在不同[惯性参考系](@entry_id:276742)之间进行变换的数学对象。这个对象就是二阶[反对称张量](@entry_id:199349) $F^{\mu\nu}$。在一个给定的惯性系中，其分量由该[参考系](@entry_id:169232)中测得的[电场和磁场](@entry_id:261347)分量决定。

我们使用时空坐标 $x^\mu = (x^0, x^1, x^2, x^3) = (ct, x, y, z)$，其中 $c$ 是[真空中的光速](@entry_id:272753)。[逆变](@entry_id:192290)[电磁场张量](@entry_id:158921) $F^{\mu\nu}$ 的矩阵形式定义如下：

$$
F^{\mu\nu} = \begin{pmatrix}
0  -E_x/c  -E_y/c  -E_z/c \\
E_x/c  0  -B_z  B_y \\
E_y/c  B_z  0  -B_x \\
E_z/c  -B_y  B_x  0
\end{pmatrix}
$$

其中 $(E_x, E_y, E_z)$ 和 $(B_x, B_y, B_z)$ 是三维[电场和磁场](@entry_id:261347)矢量在[笛卡尔坐标系](@entry_id:169789)下的分量。张量的索引 $\mu$ 和 $\nu$ 从 0 到 3，分别对应于 $t, x, y, z$。

从定义可以看出，$F^{\mu\nu}$ 是一个**[反对称张量](@entry_id:199349)** (antisymmetric tensor)，即 $F^{\nu\mu} = -F^{\mu\nu}$。这个性质直接导致其对角线分量 $F^{\mu\mu}$ 均为零。时间-空间分量 ($F^{0i}, i=1,2,3$) 与[电场](@entry_id:194326)成正比，而空间-空间分量 ($F^{ij}, i,j=1,2,3$) 则由[磁场](@entry_id:153296)分量构成。具体来说，空间分量可以紧凑地写作 $F^{ij} = -\sum_{k=1}^{3}\epsilon^{ijk} B_k$，其中 $\epsilon^{ijk}$ 是三维[列维-奇维塔符号](@entry_id:193594)（Levi-Civita symbol），且我们约定 $\epsilon^{123} = +1$。

作为一个具体的例子，考虑一个同时存在[匀强电场](@entry_id:264305) $\vec{E} = E_0 \hat{x}$ 和[匀强磁场](@entry_id:263817) $\vec{B} = B_0 \hat{y}$ 的区域，其中 $E_0$ 和 $B_0$ 是正常数 [@problem_id:1548650]。此时，电场和磁场的分量为 $E_x = E_0, E_y = E_z = 0$ 和 $B_y = B_0, B_x = B_z = 0$。根据上述定义，我们可以构建 $F^{\mu\nu}$ 矩阵：

- 时间-空间分量：$F^{01} = -E_x/c = -E_0/c$，而 $F^{02}$ 和 $F^{03}$ 为零。由反对称性，$F^{10} = E_0/c$。
- 空间-空间分量：$F^{12} = -\epsilon^{123}B_3 = 0$，$F^{13} = -\epsilon^{132}B_2 = -(-1)B_y = B_0$，$F^{23} = -\epsilon^{231}B_1 = 0$。由反对称性，$F^{31}=-B_0$。

将所有分量组合起来，我们得到该特定场配置下的[电磁场张量](@entry_id:158921)：

$$
F^{\mu\nu} = \begin{pmatrix}
0  -E_0/c  0  0 \\
E_0/c  0  0  B_0 \\
0  0  0  0 \\
0  -B_0  0  0
\end{pmatrix}
$$

除了逆变形式 $F^{\mu\nu}$，我们还经常使用[协变](@entry_id:634097)形式 $F_{\mu\nu}$。它通过[闵可夫斯基度规张量](@entry_id:180802) $\eta_{\mu\nu}$ 从 $F^{\mu\nu}$ "降低" 指标得到：$F_{\mu\nu} = \eta_{\mu\alpha} \eta_{\nu\beta} F^{\alpha\beta}$。在 $(+,-,-,-)$ 度规号差下，即 $\eta = \text{diag}(1, -1, -1, -1)$，[协变张量](@entry_id:634493)的分量变为：

$$
F_{\mu\nu} = \begin{pmatrix}
0  E_x/c  E_y/c  E_z/c \\
-E_x/c  0  -B_z  B_y \\
-E_y/c  B_z  0  -B_x \\
-E_z/c  -B_y  B_x  0
\end{pmatrix}
$$

注意到，与 $F^{\mu\nu}$ 相比，$F_{\mu\nu}$ 的时间-空间分量变号了 ($F_{0i} = E_i/c$)，而空间-空间分量保持不变 ($F_{ij} = F^{ij}$)。

### 四维[势与规范](@entry_id:185228)不变性

电磁场张量的一个更深刻的来源是四维[电磁势](@entry_id:266145) $A^\mu$。在[经典电动力学](@entry_id:270496)中，电场和磁场可以由标量势 $\phi$ 和矢量势 $\vec{A}$ 导出：$\vec{E} = -\nabla\phi - \frac{\partial\vec{A}}{\partial t}$ 和 $\vec{B} = \nabla \times \vec{A}$。在相对论框架下，这两者被统一为[四维矢量势](@entry_id:188407) $A^\mu = (\phi/c, \vec{A})$。

电磁场张量 $F_{\mu\nu}$ 可以通过对[四维势](@entry_id:188407)求[微分](@entry_id:158718)得到：

$$
F_{\mu\nu} = \partial_\mu A_\nu - \partial_\nu A_\mu
$$

其中 $\partial_\mu = \frac{\partial}{\partial x^\mu}$ 是四维梯度算符。这个定义简洁地统一了从势到场的两个关系式。例如，使用[协变](@entry_id:634097)[四维势](@entry_id:188407) $A_\mu=(\phi/c, -\vec{A})$，时间-空间分量可以导出为 $F_{0i} = \partial_0 A_i - \partial_i A_0 = -\frac{1}{c}(\partial_i \phi + \partial_t A^i) = E_i/c$。而空间-空间分量 $F_{ij} = \partial_i A_j - \partial_j A_i = \partial_j A^i - \partial_i A^j = -\epsilon_{ijk} (\nabla \times \vec{A})_k = -\epsilon_{ijk}B_k$，这与我们之前的定义相符。

让我们看一个具体的计算例子。考虑一个由[四维势](@entry_id:188407) $A_\mu = (0, \frac{1}{2}B_0 y, -\frac{1}{2}B_0 x, 0)$ 描述的系统，其中 $B_0$ 是一个常数 [@problem_id:1548680]。我们可以计算出对应的[电磁场张量](@entry_id:158921)。由于 $A_0=0$ 且所有分量都不依赖于时间，所有 $F_{0i}$ 分量都为零，这意味着没有[电场](@entry_id:194326)。对于空间分量，唯一不为零的是：

$$
F_{12} = \partial_1 A_2 - \partial_2 A_1 = \frac{\partial}{\partial x}(-\frac{1}{2}B_0 x) - \frac{\partial}{\partial y}(\frac{1}{2}B_0 y) = -\frac{1}{2}B_0 - \frac{1}{2}B_0 = -B_0
$$

根据[反对称性](@entry_id:261893)，$F_{21} = B_0$。所有其他分量均为零。这对应一个沿 $z$ 轴方向的[匀强磁场](@entry_id:263817) $\vec{B} = (0, 0, B_0)$。

这个定义引出了一个至关重要的概念：**规范不变性** (gauge invariance)。我们可以对[四维势](@entry_id:188407) $A_\mu$ 进行一个**[规范变换](@entry_id:176521)** (gauge transformation)，形式为 $A'_\mu = A_\mu + \partial_\mu \chi$，其中 $\chi(x^\alpha)$ 是任意一个[标量场](@entry_id:151443)（称为[规范函数](@entry_id:749731)）。在这样的变换下，电磁场张量保持不变：

$$
F'_{\mu\nu} = \partial_\mu A'_\nu - \partial_\nu A'_\mu = \partial_\mu (A_\nu + \partial_\nu \chi) - \partial_\nu (A_\mu + \partial_\mu \chi) = (\partial_\mu A_\nu - \partial_\nu A_\mu) + (\partial_\mu\partial_\nu\chi - \partial_\nu\partial_\mu\chi)
$$

由于[偏导数](@entry_id:146280)的顺序可以交换（$\partial_\mu\partial_\nu\chi = \partial_\nu\partial_\mu\chi$），上式括号中的第二项恒为零。因此，$F'_{\mu\nu} = F_{\mu\nu}$。

这意味着，对于同一个物理[电磁场](@entry_id:265881)，存在无穷多个不同的[四维势](@entry_id:188407)可以描述它。[四维势](@entry_id:188407)本身不是唯一的[物理可观测量](@entry_id:154692)，只有通过它计算出的场强 $F_{\mu\nu}$ 才是。例如，在问题 [@problem_id:1548662] 中，一个看似更复杂的势 $A'_\mu = (0, B_0(1+k)y, k B_0 x, 0)$ 实际上描述了与 $A_\mu = (0, B_0 y, 0, 0)$ 完全相同的物理场（一个沿 $z$ 轴的[匀强磁场](@entry_id:263817) $B_z = B_0$），因为它们之间仅相差一个[规范变换](@entry_id:176521)（对应的[规范函数](@entry_id:749731)为 $\chi = k B_0 xy$）。由于物理现象仅依赖于 $F_{\mu\nu}$，所有从 $F_{\mu\nu}$ 构造出的物理量（例如[洛伦兹不变量](@entry_id:161821) $F_{\mu\nu}F^{\mu\nu}$）都将是规范不变的。

### [场的洛伦兹变换](@entry_id:267980)

电磁场张量 formalism 的巨大威力在于它清晰地揭示了场在不同[惯性参考系](@entry_id:276742)下的变换规律。根据[张量分析](@entry_id:161423)的法则，[二阶张量](@entry_id:199780) $F^{\mu\nu}$ 在从惯性系 $S$ 变换到以速度 $\vec{v}$ 相对于 $S$ 运动的[惯性系](@entry_id:266190) $S'$ 时，其分量变换如下：

$$
F'^{\mu\nu} = \Lambda^\mu_\alpha \Lambda^\nu_\beta F^{\alpha\beta}
$$

其中 $\Lambda^\mu_\alpha$ 是洛伦兹变换矩阵。这个简单的公式包含了所有关于电场和磁场如何混合和变换的复杂规则。

让我们通过一个经典的例子来理解这一点 [@problem_id:1548632]。假设在[参考系](@entry_id:169232) $S$ 中，只有一个沿 $z$ 轴正方向的[匀强磁场](@entry_id:263817) $\vec{B} = (0, 0, B_0)$，[电场](@entry_id:194326)为零 $\vec{E}=\vec{0}$。另一个[参考系](@entry_id:169232) $S'$ 沿 $x$ 轴正方向以速度 $v$ 运动。

在 $S$ 系中，非零的张量分量只有 $F^{12} = -B_z = -B_0$ 和 $F^{21} = B_0$。
沿 $x$ 轴的洛伦兹 boost 变换矩阵为：

$$
\Lambda^{\mu}_{\ \nu} = \begin{pmatrix}
\gamma  -\beta\gamma  0  0 \\
-\beta\gamma  \gamma  0  0 \\
0  0  1  0 \\
0  0  0  1
\end{pmatrix}
$$

其中 $\beta = v/c$，$\gamma = (1-\beta^2)^{-1/2}$ 是洛伦兹因子。

现在我们来计算 $S'$ 系中的一些张量分量。例如，$F'^{12}$：

$$
F'^{12} = \Lambda^1_\alpha \Lambda^2_\beta F^{\alpha\beta} = \sum_{\alpha, \beta} \Lambda^1_\alpha \Lambda^2_\beta F^{\alpha\beta}
$$

由于 $\Lambda^2_\beta$ 只有在 $\beta=2$ 时才不为零（且 $\Lambda^2_2 = 1$），求和大大简化：

$$
F'^{12} = \Lambda^1_0 \Lambda^2_2 F^{02} + \Lambda^1_1 \Lambda^2_2 F^{12} = (-\beta\gamma)(1)(0) + (\gamma)(1)(-B_0) = -\gamma B_0
$$

在 $S'$ 系中，我们有 $F'^{12} = -B'_z$。因此，我们发现 $S'$ 系中的[磁场](@entry_id:153296) $z$ 分量为 $B'_z = \gamma B_0$。[磁场](@entry_id:153296)被增强了。

更有趣的是，让我们计算 $F'^{02}$：

$$
F'^{02} = \Lambda^0_\alpha \Lambda^2_\beta F^{\alpha\beta} = \Lambda^0_0 \Lambda^2_2 F^{02} + \Lambda^0_1 \Lambda^2_2 F^{12} = (\gamma)(1)(0) + (-\beta\gamma)(1)(-B_0) = \beta\gamma B_0
$$

在 $S'$ 系中，$F'^{02} = -E'_y/c$。因此，我们得到 $E'_y = -c(\beta\gamma B_0) = -v\gamma B_0$。

这个结果意义非凡：在 $S$ 系中明明是纯[磁场](@entry_id:153296)，但在运动的 $S'$ 系看来，却出现了一个[电场](@entry_id:194326)！这正是相对论的核心思想之一：[电场和磁场](@entry_id:261347)是同一事物的不同表现，一个观察者看到的是[电场](@entry_id:194326)还是[磁场](@entry_id:153296)，取决于他的运动状态。

### 相对论形式的[麦克斯韦方程组](@entry_id:150940)

经典电磁理论的核心是麦克斯韦方程组。使用[电磁场张量](@entry_id:158921)，这四组八个方程可以被浓缩为两个异常简洁的张量方程。

#### [齐次方程](@entry_id:163650)

[法拉第感应定律](@entry_id:146175) ($\nabla \times \vec{E} = -\frac{\partial \vec{B}}{\partial t}$) 和[磁场](@entry_id:153296)无散度定律 ($\nabla \cdot \vec{B} = 0$) 可以合并为一个单一的张量方程，称为**齐次麦克斯韦方程**或**比安基恒等式 (Bianchi identity)**：

$$
\partial_\lambda F_{\mu\nu} + \partial_\mu F_{\nu\lambda} + \partial_\nu F_{\lambda\mu} = 0
$$

如果[场张量](@entry_id:186486)由[四维势](@entry_id:188407)导出 ($F_{\mu\nu} = \partial_\mu A_\nu - \partial_\nu A_\mu$)，这个方程就会自动满足，因为它变成了 $\partial_\lambda(\partial_\mu A_\nu - \partial_\nu A_\mu) + \dots = 0$，由于偏导数可交换，所有项都会两两抵消。

为了看清这个方程如何对应于经典形式，我们可以选择特定的索引。例如，令 $(\lambda, \mu, \nu) = (0, 1, 2)$ [@problem_id:1548646]，并设 $c=1$ 以简化表达。方程变为：

$$
\partial_0 F_{12} + \partial_1 F_{20} + \partial_2 F_{01} = 0
$$

从 $F_{\mu\nu}$ 的矩阵形式中代入分量：$F_{12}=-B_z$, $F_{20}=-F_{02}=-E_y$, $F_{01}=E_x$。于是我们得到：

$$
\frac{\partial (-B_z)}{\partial t} + \frac{\partial (-E_y)}{\partial x} + \frac{\partial E_x}{\partial y} = 0 \quad \implies \quad \frac{\partial E_y}{\partial x} - \frac{\partial E_x}{\partial y} = -\frac{\partial B_z}{\partial t}
$$

这正是[法拉第感应定律](@entry_id:146175)的 $z$ 分量 $(\nabla \times \vec{E})_z = -\frac{\partial B_z}{\partial t}$。类似地，选择纯空间索引如 $(\lambda, \mu, \nu) = (1, 2, 3)$ 将会导出 $\nabla \cdot \vec{B} = 0$。

#### 非齐次方程

高斯定律 ($\nabla \cdot \vec{E} = \rho/\epsilon_0$) 和[安培-麦克斯韦定律](@entry_id:266368) ($\nabla \times \vec{B} = \mu_0 \vec{J} + \mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t}$) 描述了[电荷](@entry_id:275494)和电流（源）如何产生场。它们被统一为**非齐次麦克斯韦方程**：

$$
\partial_\mu F^{\mu\nu} = \mu_0 J^\nu
$$

这里，$J^\nu = (c\rho, \vec{J})$ 是[四维电流密度](@entry_id:262568)，其中 $\rho$ 是电荷密度，$\vec{J}$ 是三维电流密度矢量。$\mu_0$ 是[真空磁导率](@entry_id:186031)。

我们来检验这个方程的 $\nu=0$ 分量 [@problem_id:1548615]。此时方程为 $\partial_\mu F^{\mu 0} = \mu_0 J^0$。展开左边的求和：

$$
\partial_0 F^{00} + \partial_1 F^{10} + \partial_2 F^{20} + \partial_3 F^{30} = \mu_0 (c\rho)
$$

根据 $F^{\mu\nu}$ 的定义，$F^{00}=0$，而 $F^{i0} = -F^{0i} = E_i/c$。于是方程变为：

$$
0 + \frac{\partial (E_x/c)}{\partial x} + \frac{\partial (E_y/c)}{\partial y} + \frac{\partial (E_z/c)}{\partial z} = \mu_0 c\rho
$$

$$
\frac{1}{c}(\frac{\partial E_x}{\partial x} + \frac{\partial E_y}{\partial y} + \frac{\partial E_z}{\partial z}) = \mu_0 c\rho \quad \implies \quad \frac{1}{c} (\nabla \cdot \vec{E}) = \mu_0 c\rho
$$

整理后得到 $\nabla \cdot \vec{E} = \mu_0 c^2 \rho$。利用关系式 $c^2 = 1/(\epsilon_0 \mu_0)$，我们最终得到：

$$
\nabla \cdot \vec{E} = \frac{\rho}{\epsilon_0}
$$

这正是[高斯定律](@entry_id:141493)。同样地，该方程的空间分量 ($\nu = 1, 2, 3$) 会导出[安培-麦克斯韦定律](@entry_id:266368)。这种将复杂的矢量[方程组](@entry_id:193238)统一为两个简洁张量方程的能力，是[相对论电动力学](@entry_id:160964)优雅和力量的体现。

### [电磁场](@entry_id:265881)的洛伦兹不变量

在物理学中，[不变量](@entry_id:148850)是那些在某种变换（如此处的[洛伦兹变换](@entry_id:176827)）下保持不变的量。它们揭示了理论的深层结构，因为所有惯性观察者都会对其数值达成一致。[电磁场](@entry_id:265881)有两个基本的[洛伦兹不变量](@entry_id:161821)，它们可以由[场张量](@entry_id:186486) $F^{\mu\nu}$ 构造出来。

#### 第一个[不变量](@entry_id:148850)

第一个[不变量](@entry_id:148850)是[场张量](@entry_id:186486)与其自身的完全收缩：

$$
I_1 = F_{\mu\nu}F^{\mu\nu}
$$

我们可以将其用[电场和磁场](@entry_id:261347)分量表示 [@problem_id:1548669]。展开求和：
$$
I_1 = \sum_{\mu,\nu} F_{\mu\nu}F^{\mu\nu} = \sum_{i=1}^3 (F_{0i}F^{0i} + F_{i0}F^{i0}) + \sum_{i,j=1}^3 F_{ij}F^{ij}
$$

代入分量表达式：
- 时间-空间部分：$F_{0i}F^{0i} = (E_i/c)(-E_i/c) = -E_i^2/c^2$。由于 $F_{i0}=-F_{0i}$ 且 $F^{i0}=-F^{0i}$，所以 $F_{i0}F^{i0} = F_{0i}F^{0i}$。这部分贡献为 $2 \sum_i (-E_i^2/c^2) = -2E^2/c^2$。
- 空间-空间部分：$F_{ij} = F^{ij} = -\epsilon_{ijk}B_k$。所以 $F_{ij}F^{ij} = \sum_{i,j} (-\epsilon_{ijk}B_k)(-\epsilon_{ijm}B_m) = \sum_{k,m} (2\delta_{km}) B_k B_m = 2B^2$。

将两部分相加，我们得到：

$$
I_1 = F_{\mu\nu}F^{\mu\nu} = 2(B^2 - \frac{E^2}{c^2})
$$

这个[不变量](@entry_id:148850)的符号具有物理意义。如果 $I_1 > 0$，则 $B^2 > E^2/c^2$，总可以找到一个[洛伦兹变换](@entry_id:176827)，使得在新[参考系](@entry_id:169232)中[电场](@entry_id:194326)为零，只剩下[磁场](@entry_id:153296)。反之，如果 $I_1  0$，则可以找到一个[参考系](@entry_id:169232)使得[磁场](@entry_id:153296)为零。如果 $I_1 = 0$，则在所有[参考系](@entry_id:169232)中都有 $B^2 = E^2/c^2$（例如平面[电磁波](@entry_id:269629)）。

#### 第二个[不变量](@entry_id:148850)

第二个[不变量](@entry_id:148850)是一个[伪标量](@entry_id:196696)（pseudoscalar），它由[场张量](@entry_id:186486)和四维[列维-奇维塔符号](@entry_id:193594) $\epsilon_{\alpha\beta\gamma\delta}$ 构造而成。

$$
I_2 = \epsilon_{\alpha\beta\gamma\delta}F^{\alpha\beta}F^{\gamma\delta}
$$

要计算这个量 [@problem_id:1548635]，我们需要对所有索引求和。只有当 $\{\alpha, \beta, \gamma, \delta\}$ 是 $\{0,1,2,3\}$ 的一个[排列](@entry_id:136432)时，$\epsilon_{\alpha\beta\gamma\delta}$ 才不为零。这意味着我们只需要考虑 $F^{\alpha\beta}$ 和 $F^{\gamma\delta}$ 的索引完全不重叠的情况。这样的组合有三类，例如 $(\alpha,\beta)=(0,1)$ 与 $(\gamma,\delta)=(2,3)$。考虑到所有[排列](@entry_id:136432)，一个系统性的计算表明：

$$
I_2 = \frac{8}{c} \vec{E} \cdot \vec{B}
$$

这个[不变量](@entry_id:148850)也具有深刻的物理意义。如果 $\vec{E}$ 和 $\vec{B}$ 在某个[参考系](@entry_id:169232)中是正交的，那么 $\vec{E} \cdot \vec{B}=0$，这个[不变量](@entry_id:148850)就为零。由于它是[洛伦兹不变量](@entry_id:161821)，这意味着在所有其他惯性参考系中，变换后的电场和磁场 $\vec{E}'$ 和 $\vec{B}'$ 也将是正交的。如果 $\vec{E} \cdot \vec{B} \neq 0$，则不可能找到一个[参考系](@entry_id:169232)使得[电场](@entry_id:194326)或[磁场](@entry_id:153296)之一消失。

### 高等课题：[拉格朗日表述](@entry_id:188652)与[能量-动量张量](@entry_id:203902)

[电磁场张量](@entry_id:158921)也在更高级的理论表述中扮演核心角色，例如在拉格朗日场论中。

#### [拉格朗日表述](@entry_id:188652)

整个[经典电动力学](@entry_id:270496)的动力学行为可以从一个简单的作用量 $S = \int \mathcal{L} \,d^4x$ 和最小作用量原理中导出。描述[电磁场](@entry_id:265881)与电流相互作用的拉格朗日密度 $\mathcal{L}$ 为：

$$
\mathcal{L} = -\frac{1}{4\mu_0}F_{\mu\nu}F^{\mu\nu} - J^\mu A_\mu
$$

第一项 $-\frac{1}{4\mu_0}F_{\mu\nu}F^{\mu\nu}$ 是[电磁场](@entry_id:265881)自身的动力学项，它正比于我们前面讨论的第一个洛伦兹不变量。第二项 $-J^\mu A_\mu$ 描述了场 ($A_\mu$) 与源 ($J^\mu$) 之间的相互作用。

将场 $A_\rho$ 视为动力学变量，我们可以应用[场的欧拉-拉格朗日方程](@entry_id:173994)：
$$
\partial_\sigma \left( \frac{\partial \mathcal{L}}{\partial (\partial_\sigma A_\rho)} \right) - \frac{\partial \mathcal{L}}{\partial A_\rho} = 0
$$

计算方程中的两项：
1.  对 $A_\rho$ 的导数 $\partial_\sigma A_\rho$ 的[偏导数](@entry_id:146280)。这一项只来自 $\mathcal{L}$ 中的 $F_{\mu\nu}$ 项。一个仔细的计算 [@problem_id:1548679] 表明：
    $$
    \frac{\partial \mathcal{L}}{\partial (\partial_\sigma A_\rho)} = -\frac{1}{\mu_0}F^{\sigma\rho}
    $$
2.  对 $A_\rho$ 本身的[偏导数](@entry_id:146280)。这一项只来自相互作用项：
    $$
    \frac{\partial \mathcal{L}}{\partial A_\rho} = -J^\mu \frac{\partial A_\mu}{\partial A_\rho} = -J^\mu \delta^\rho_\mu = -J^\rho
    $$

将这两项代入[欧拉-拉格朗日方程](@entry_id:137827)，我们得到：
$$
\partial_\sigma \left( -\frac{1}{\mu_0}F^{\sigma\rho} \right) - (-J^\rho) = 0 \quad \implies \quad \partial_\sigma F^{\sigma\rho} = \mu_0 J^\rho
$$
这正是我们之前看到的非齐次麦克斯韦方程！这个优雅的推导展示了[拉格朗日形式主义](@entry_id:158185)的威力，它将整个理论的动力学基础归结为一个单一的标量——拉格朗日密度。

#### 电磁能量-动量张量

根据[诺特定理](@entry_id:145690)，物理系统的每一种[连续对称性](@entry_id:137257)都对应一个守恒量。与时空平移对称性相对应的是守恒的能量-动量张量 $T^{\mu\nu}$。对于真空中的[电磁场](@entry_id:265881)，其能量-动量张量可以完全由[场张量](@entry_id:186486) $F^{\mu\nu}$ 表达：

$$
T^{\mu\nu} = \frac{1}{\mu_0} \left( F^{\mu\rho}{F^\nu}_\rho - \frac{1}{4} \eta^{\mu\nu} F_{\alpha\beta}F^{\alpha\beta} \right)
$$
(这里我们恢复了常数 $1/\mu_0$ 以确保单位正确。)
$T^{00}$ 分量代表场的能量密度， $T^{0i}$ 代表[能流密度](@entry_id:266056)（坡印亭矢量），$T^{ij}$ 代表动量流密度（麦克斯韦胁强张量）。

这个张量有一个非常重要的性质：它的迹 (trace) 为零。我们可以直接验证这一点 [@problem_id:1548642]：
$$
T^\mu_\mu = \eta_{\mu\nu}T^{\mu\nu} = \frac{1}{\mu_0} \left( \eta_{\mu\nu}F^{\mu\rho}{F^\nu}_\rho - \frac{1}{4} \eta_{\mu\nu}\eta^{\mu\nu} F_{\alpha\beta}F^{\alpha\beta} \right)
$$
第一项可以被改写为 $\eta_{\mu\nu}F^{\mu\rho}(\eta_{\rho\sigma}F^{\nu\sigma}) = F_{\nu\sigma}F^{\nu\sigma} = F_{\alpha\beta}F^{\alpha\beta}$。
第二项中，$\eta_{\mu\nu}\eta^{\mu\nu} = \delta^\mu_\mu = 4$（在四维时空中）。所以第二项是 $-\frac{1}{4}(4)F_{\alpha\beta}F^{\alpha\beta} = -F_{\alpha\beta}F^{\alpha\beta}$。
因此，
$$
T^\mu_\mu = \frac{1}{\mu_0} (F_{\alpha\beta}F^{\alpha\beta} - F_{\alpha\beta}F^{\alpha\beta}) = 0
$$
[能量-动量张量](@entry_id:203902)的迹为零是经典电磁理论在四维时空中具有**[共形不变性](@entry_id:191867)** (conformal invariance) 的一个直接后果。这表明该理论不仅在[洛伦兹变换](@entry_id:176827)下形式不变，在更广泛的标度变换下也同样具有[不变性](@entry_id:140168)。这一深刻的几何性质是电磁场张量带来的又一重要洞见。