## 引言
[Hartree-Fock理论](@entry_id:160358)为我们从第一性原理理解多电子体系提供了一个基本的平均场图像，但其核心的[微分](@entry_id:158718)-积分方程本身难以直接求解。本文旨在填补从理论概念到实际计算之间的鸿沟，核心问题是：如何将[Hartree-Fock理论](@entry_id:160358)转化为一套在计算机上可行的、稳健的算法？我们将系统性地阐述[Hartree-Fock](@entry_id:142303)-Roothaan方法，这是现代[量子化学](@entry_id:140193)计算程序的基石。

在接下来的内容中，读者将首先在“原理与机制”一章中学习如何通过[原子轨道线性组合](@entry_id:151829)（LCAO）近似，将复杂的算符方程转化为代数[矩阵方程](@entry_id:203695)，并掌握求解该方程的自洽场（SCF）迭代过程。随后，“应用与[交叉](@entry_id:147634)学科联系”一章将探讨这些计算结果的物理意义，如利用[正则轨道](@entry_id:183413)能解释化学现象，分析实际计算中遇到的挑战（如基[组选择](@entry_id:175784)和收敛性），并展示其如何作为更高级理论的出发点。最后，“动手实践”部分将提供具体的计算问题，帮助读者巩固所学知识，将理论应用于实践。

## 原理与机制

在上一章中，我们介绍了[Hartree-Fock理论](@entry_id:160358)作为一种从第一性原理近似求解多电子体系薛定谔方程的基本方法。其核心思想是用一个单[斯莱特行列式](@entry_id:139034)（single Slater determinant）来近似真实的[多电子波函数](@entry_id:156344)。本章将深入探讨将这一理论思想转化为具体计算方法的数学原理与实现机制。我们将首先从[变分原理](@entry_id:198028)出发，推导出描述电子在平均场中运动的[Fock算符](@entry_id:139887)，然后引入[原子轨道线性组合](@entry_id:151829)（LCAO）近似，从而得到著名的[Hartree-Fock-Roothaan方程](@entry_id:171084)。最后，我们将详细阐述求解这些方程的[自洽场](@entry_id:136549)（SCF）迭代过程，并讨论最终得到的[正则轨道](@entry_id:183413)的性质及其物理解释。

### [Hartree-Fock](@entry_id:142303)平均[场算符](@entry_id:140269)

量子力学的[变分原理](@entry_id:198028)是近似方法的基石。它指出，对于一个由[哈密顿算符](@entry_id:144286) $\hat{H}$ 描述的体系，其[基态能量](@entry_id:263704)为 $E_0$，那么对于任意归一化的试探波函数 $\Psi$，其[能量期望值](@entry_id:174035)（即瑞利商，Rayleigh quotient）总是基态能量的一个上界：

$$
R[\Psi] = \langle \Psi | \hat{H} | \Psi \rangle \ge E_0
$$

等号成立的当且仅当试探波函数 $\Psi$ 就是真实的[基态](@entry_id:150928)[波函数](@entry_id:147440) $\Psi_0$ [@problem_id:2895930]。[Hartree-Fock理论](@entry_id:160358)的核心就是运用这一原理，但将搜寻最优[波函数](@entry_id:147440)的范围限制在由N个单电子旋轨函数（spin-orbitals）$\{\psi_i\}$ 构成的单个斯莱特行列式之内。

通过在旋轨函数需满足归一正交约束的条件下，最小化斯莱特行列式的[能量期望值](@entry_id:174035)，我们可以得到一组有效的单[电子薛定谔方程](@entry_id:177999)，即[Hartree-Fock方程](@entry_id:194386)：

$$
\hat{f}(1) \psi_i(1) = \epsilon_i \psi_i(1)
$$

其中，$\hat{f}(1)$ 被称为 **[Fock算符](@entry_id:139887)**，它描述了电子1在所有其他 $N-1$ 个电子所产生的平均场中的运动。$\epsilon_i$ 是与旋轨函数 $\psi_i$ 相关联的 **[轨道](@entry_id:137151)能**。[Fock算符](@entry_id:139887)由三部分构成 [@problem_id:2895862]：

$$
\hat{f}(1) = \hat{h}(1) + \sum_{j=1}^{N} \left( \hat{J}_j(1) - \hat{K}_j(1) \right)
$$

让我们逐一审视这些组成部分：

1.  **核心[哈密顿算符](@entry_id:144286) ($\hat{h}$):** 该算符描述了单个电子自身的动能以及它与[原子核](@entry_id:167902)骨架之间的库仑吸引势。在[原子单位](@entry_id:166762)制下，对于电子1，其形式为：
    $$
    \hat{h}(1) = -\frac{1}{2}\nabla_1^2 - \sum_A \frac{Z_A}{r_{1A}}
    $$
    其中 $-\frac{1}{2}\nabla_1^2$ 是电子1的[动能算符](@entry_id:265633)，$Z_A$ 是[原子核](@entry_id:167902)A的[电荷](@entry_id:275494)数，$r_{1A}$ 是电子1与[原子核](@entry_id:167902)A之间的距离。

2.  **[库仑算符](@entry_id:178946) ($\hat{J}_j$):** 该算符描述了电子1与占据旋轨函数 $\psi_j$ 的电子之间的经典[静电排斥](@entry_id:162128)作用。[轨道](@entry_id:137151) $\psi_j$ 中的电子可以被看作一团电荷密度为 $|\psi_j(2)|^2$ 的“电子云”。这团电子云在电子1所在的位置 $\mathbf{r}_1$ 处产生的[排斥势](@entry_id:185622)，就是[库仑算符](@entry_id:178946)。其对任意试探[轨道](@entry_id:137151) $\psi(1)$ 的作用是：
    $$
    \hat{J}_j(1) \psi(1) = \left( \int d\tau_2 \frac{|\psi_j(2)|^2}{r_{12}} \right) \psi(1)
    $$
    这里，$d\tau_2$ 表示对电子2的所有坐标（空间和自旋）进行积分。括号内的积分项是一个只依赖于电子1坐标 $\mathbf{r}_1$ 的函数，它作为一个局域（local）的乘性[势场](@entry_id:143025)作用在 $\psi(1)$ 上。

3.  **[交换算符](@entry_id:156554) ($\hat{K}_j$):** [交换算符](@entry_id:156554)没有经典对应，它完全源于[多电子波函数](@entry_id:156344)必须满足的[泡利反对称原理](@entry_id:187043)。它描述了同自旋电子之间的一种非经典的相互作用。其对试探[轨道](@entry_id:137151) $\psi(1)$ 的作用定义为：
    $$
    \hat{K}_j(1) \psi(1) = \left( \int d\tau_2 \frac{\psi_j^*(2) \psi(2)}{r_{12}} \right) \psi_j(1)
    $$
    [交换算符](@entry_id:156554)的一个关键特性是它的 **自旋选择性**。将旋轨[函数分解](@entry_id:197881)为空间部分 $\phi(\mathbf{r})$ 和自旋部分 $\sigma(s)$，即 $\psi(\mathbf{x}) = \phi(\mathbf{r})\sigma(s)$，可以看出[交换算符](@entry_id:156554)的积分项中包含了自旋函数的[内积](@entry_id:158127) $\langle \sigma_j | \sigma \rangle$。由于自旋[函数的正交性](@entry_id:160337)（$\langle\alpha|\beta\rangle=0$），交换作用只存在于自旋相同的电子之间 [@problem_id:2895862]。

另一个至关重要的特性是[交换算符](@entry_id:156554)的 **非局域性**（nonlocality）[@problem_id:2895886]。与[库仑算符](@entry_id:178946)不同，$\hat{K}_j$ 的作用不能表示为在 $\mathbf{r}_1$ 点乘以一个势函数。要计算 $(\hat{K}_j\psi)(\mathbf{r}_1)$ 的值，我们需要知道函数 $\psi$ 在所有空间点 $\mathbf{r}_2$ 的值，因为它出现在积分核中。这种积分形式是典型的非局域算符。正是这种特殊的非局域形式，使得[Hartree-Fock理论](@entry_id:160358)能够精确地 **抵消[自相互作用](@entry_id:201333)**（self-interaction）。对于占据[轨道](@entry_id:137151) $\psi_k$ 而言，它与自身的库仑作用 $\hat{J}_k\psi_k$ 被它与自身的交换作用 $\hat{K}_k\psi_k$ 完全抵消，即 $(\hat{J}_k - \hat{K}_k)\psi_k = 0$。这是[Hartree-Fock理论](@entry_id:160358)相较于许多局域密度泛函近似（它们通常受自相互作用误差的困扰）的一个重要优势 [@problem_id:2895886]。

### [Roothaan-Hall方程](@entry_id:146169)：从算符到矩阵

尽管[Hartree-Fock方程](@entry_id:194386)形式优美，但作为[微分](@entry_id:158718)-积分方程，直接求解它们非常困难。Clemens C. J. Roothaan 和 George G. Hall 提出，通过将未知的分子[轨道](@entry_id:137151)（MO）$\psi_i$ 展开在一组已知的[原子轨道](@entry_id:140819)（AO）[基函数](@entry_id:170178) $\{\chi_\mu\}$ 的线性组合中来求解，即[LCAO-MO近似](@entry_id:177363)：

$$
\psi_i(\mathbf{r}) = \sum_{\mu=1}^{M} C_{\mu i} \chi_\mu(\mathbf{r})
$$

这里，$C_{\mu i}$ 是待求的分子[轨道](@entry_id:137151)系数。通过这一近似，[求解微分方程](@entry_id:137471)的问题就转化为了求解[代数方程](@entry_id:272665)（即矩阵方程）的问题。

一个关键的复杂性在于，[原子轨道](@entry_id:140819)[基组](@entry_id:160309) $\{\chi_\mu\}$ 通常是 **非正交** 的。这意味着[基函数](@entry_id:170178)之间的[内积](@entry_id:158127)（重叠积分）不为零。我们定义 **[重叠矩阵](@entry_id:268881)** $\mathbf{S}$，其[矩阵元](@entry_id:186505)为：

$$
S_{\mu\nu} = \langle \chi_\mu | \chi_\nu \rangle = \int \chi_\mu^*(\mathbf{r}) \chi_\nu(\mathbf{r}) d\mathbf{r}
$$

如果[基组](@entry_id:160309)是[线性无关](@entry_id:148207)的，$\mathbf{S}$ 矩阵是 Hermitian 且正定的 [@problem_id:2643532]。分子[轨道](@entry_id:137151) $\psi_i$ 之间必须满足归一正交条件 $\langle \psi_i | \psi_j \rangle = \delta_{ij}$。将LCAO展开式代入此条件，可得对[系数矩阵](@entry_id:151473) $\mathbf{C}$ 的约束：

$$
\mathbf{C}^\dagger \mathbf{S} \mathbf{C} = \mathbf{I}
$$

其中 $\mathbf{I}$ 是[单位矩阵](@entry_id:156724)。如果[基组](@entry_id:160309)是正交的，则 $\mathbf{S}=\mathbf{I}$，约束简化为 $\mathbf{C}^\dagger \mathbf{C} = \mathbf{I}$。

将[Hartree-Fock方程](@entry_id:194386) $\hat{f}\psi_i = \epsilon_i \psi_i$ 在AO[基函数](@entry_id:170178)上投影，我们便将算符方程转化为了[矩阵方程](@entry_id:203695)。[Fock算符](@entry_id:139887)的[矩阵表示](@entry_id:146025)，即 **[Fock矩阵](@entry_id:203184)** $\mathbf{F}$，其矩阵元为 $F_{\mu\nu} = \langle \chi_\mu | \hat{f} | \chi_\nu \rangle$。[Fock矩阵](@entry_id:203184)的具体形式为：

$$
\mathbf{F} = \mathbf{h} + \mathbf{G}
$$

其中 $\mathbf{h}$ 是核心[哈密顿矩阵](@entry_id:136233) ($h_{\mu\nu} = \langle \chi_\mu | \hat{h} | \chi_\nu \rangle$)，而 $\mathbf{G}$ 是包含库仑和[交换相互作用](@entry_id:140006)的电子互斥部分。$\mathbf{G}$ 的矩阵元依赖于 **密度矩阵** $\mathbf{P}$ 和 **[双电子积分](@entry_id:261879)**。对于闭壳层体系，[密度矩阵](@entry_id:139892)定义为 $P_{\lambda\sigma} = 2\sum_{i}^{\text{occ}} C_{\lambda i} C_{\sigma i}^*$。[双电子积分](@entry_id:261879)则定义为：

$$
(\mu\nu|\lambda\sigma) = \iint \chi_\mu^*(1) \chi_\nu(1) \frac{1}{r_{12}} \chi_\lambda^*(2) \chi_\sigma(2) d\mathbf{r}_1 d\mathbf{r}_2
$$

这些积分具有重要的[置换对称性](@entry_id:185825)，例如，对于实函[数基](@entry_id:634389)组，我们有 $(\mu\nu|\lambda\sigma) = (\nu\mu|\lambda\sigma) = (\mu\nu|\sigma\lambda) = (\lambda\sigma|\mu\nu)$ 等共8种对称性，这可以极大减少需要计算和存储的积分数量 [@problem_id:2895893]。

最终，结合所有这些元素，我们得到了 **[Hartree-Fock](@entry_id:142303)-Roothaan** 方程（或称 **Roothaan-Hall** 方程）：

$$
\mathbf{F}\mathbf{C} = \mathbf{S}\mathbf{C}\boldsymbol{\varepsilon}
$$

这里 $\boldsymbol{\varepsilon}$ 是一个[对角矩阵](@entry_id:637782)，其对角元为[轨道](@entry_id:137151)能 $\epsilon_i$。这是一个 **广义本征值问题**，而不是标准的本征值问题 ($\mathbf{A}\mathbf{x} = \lambda\mathbf{x}$)，其根本原因在于原[子基](@entry_id:151637)组的[非正交性](@entry_id:192553)，即 $\mathbf{S} \neq \mathbf{I}$ [@problem_id:2643532]。正是分子[轨道](@entry_id:137151)的正交约束 $\mathbf{C}^\dagger \mathbf{S} \mathbf{C} = \mathbf{I}$ 在变分过程中引入了[重叠矩阵](@entry_id:268881) $\mathbf{S}$ 作为度规张量，导致了这种广义形式。

### 自洽场（SCF）迭代过程

[Roothaan-Hall方程](@entry_id:146169)有一个棘手的特点：[Fock矩阵](@entry_id:203184) $\mathbf{F}$ 本身依赖于[密度矩阵](@entry_id:139892) $\mathbf{P}$，而[密度矩阵](@entry_id:139892)又是由方程的解——[系数矩阵](@entry_id:151473) $\mathbf{C}$——构建的。$\mathbf{F}$ 依赖于 $\mathbf{C}$，而 $\mathbf{C}$ 又由 $\mathbf{F}$ 决定。这种[非线性](@entry_id:637147)特性意味着我们无法一次性直接求解，必须采用迭代的方法，直到输入[Fock矩阵](@entry_id:203184)的[轨道](@entry_id:137151)与输出的[轨道](@entry_id:137151)达到一致。这个过程被称为 **自洽场（Self-Consistent Field, SCF）** 方法。

一个标准的SCF迭代周期如下 [@problem_id:2895860]：

1.  **初始猜测：** 选择一个初始的密度矩阵 $\mathbf{P}^{(0)}$。这可以通过猜测分子[轨道](@entry_id:137151)系数，或使用更简单模型（如扩展休克尔理论）的结果来获得。

2.  **构建[Fock矩阵](@entry_id:203184)：** 在第 $k$ 次迭代中，使用当前的密度矩阵 $\mathbf{P}^{(k)}$ 来计算双电子互斥部分 $\mathbf{G}[\mathbf{P}^{(k)}]$，并组装出[Fock矩阵](@entry_id:203184) $\mathbf{F}^{(k)} = \mathbf{h} + \mathbf{G}[\mathbf{P}^{(k)}]$。

3.  **求解广义[本征值问题](@entry_id:142153)：** 求解当前的[Roothaan-Hall方程](@entry_id:146169) $\mathbf{F}^{(k)}\mathbf{C}^{(k+1)} = \mathbf{S}\mathbf{C}^{(k+1)}\boldsymbol{\varepsilon}^{(k+1)}$，得到一组新的分子[轨道](@entry_id:137151)系数 $\mathbf{C}^{(k+1)}$ 和[轨道](@entry_id:137151)能 $\boldsymbol{\varepsilon}^{(k+1)}$。

4.  **构建新密度矩阵：** 根据[Aufbau原理](@entry_id:141667)，选择能量最低的 $N/2$ 个[轨道](@entry_id:137151)（对于一个N电子闭壳层体系）作为新的占据[轨道](@entry_id:137151) $\mathbf{C}_{\text{occ}}$。利用它们构建新的[密度矩阵](@entry_id:139892) $\mathbf{P}_{\text{new}} = 2\mathbf{C}_{\text{occ}}\mathbf{C}_{\text{occ}}^\dagger$。

5.  **收敛性检查与混合：** 将新的[密度矩阵](@entry_id:139892) $\mathbf{P}_{\text{new}}$ 与旧的密度矩阵 $\mathbf{P}^{(k)}$ 进行比较。如果二者之差（或相应的总能量之差）小于预设的阈值，则认为计算已收敛，迭代结束。否则，将旧密度与新密度进行混合（例如，使用直接求逆[迭代子](@entry_id:200280)空间DIIS等加速收敛技术）得到下一次迭代的输入密度 $\mathbf{P}^{(k+1)}$，然后返回第2步。

6.  **计算能量：** 收敛后，使用最终的[密度矩阵](@entry_id:139892) $\mathbf{P}$ 和[Fock矩阵](@entry_id:203184) $\mathbf{F}$ 计算总电子能量：
    $$
    E_{\text{elec}} = \frac{1}{2} \mathrm{Tr}\left[\mathbf{P}(\mathbf{h} + \mathbf{F})\right]
    $$
    加上[原子核](@entry_id:167902)间的排斥能，即得到体系的总能量。

#### 求解广义本征值问题

在SCF迭代的第3步中，核心任务是求解 $\mathbf{F}\mathbf{C} = \mathbf{S}\mathbf{C}\boldsymbol{\varepsilon}$。直接处理广义[本征值问题](@entry_id:142153)在数值上不便，标准做法是将其转换为标准的[本征值问题](@entry_id:142153)。

首先，我们需要一个变换矩阵 $\mathbf{X}$，它能将非正交的AO[基组](@entry_id:160309)变换为一组正交的[基组](@entry_id:160309)。这样的变换满足 $\mathbf{X}^\dagger \mathbf{S} \mathbf{X} = \mathbf{I}$。一个常用的方法是 **[对称正交化](@entry_id:167626)** [@problem_id:2895888]。因为 $\mathbf{S}$ 是正定对称阵，我们可以计算其唯一的负二分之一方根 $\mathbf{S}^{-1/2}$。通过代换 $\mathbf{C} = \mathbf{S}^{-1/2}\mathbf{C'}$，原方程变为：

$$
\mathbf{F}(\mathbf{S}^{-1/2}\mathbf{C'}) = \mathbf{S}(\mathbf{S}^{-1/2}\mathbf{C'})\boldsymbol{\varepsilon}
$$

两边同时左乘 $(\mathbf{S}^{-1/2})^\dagger = \mathbf{S}^{-1/2}$，并整理得：

$$
(\mathbf{S}^{-1/2}\mathbf{F}\mathbf{S}^{-1/2})\mathbf{C'} = \mathbf{C'}\boldsymbol{\varepsilon}
$$

令 $\mathbf{F'} = \mathbf{S}^{-1/2}\mathbf{F}\mathbf{S}^{-1/2}$，我们就得到了一个[标准形式](@entry_id:153058)的[本征值问题](@entry_id:142153) $\mathbf{F'}\mathbf{C'} = \mathbf{C'}\boldsymbol{\varepsilon}$。我们可以用标准数值库对变换后的[Fock矩阵](@entry_id:203184) $\mathbf{F'}$ 进行对角化，求得其[本征向量](@entry_id:151813) $\mathbf{C'}$ 和[本征值](@entry_id:154894) $\boldsymbol{\varepsilon}$，然后通过反变换 $\mathbf{C} = \mathbf{S}^{-1/2}\mathbf{C'}$ 得到原始AO基下的MO系数。

然而，在实践中，特别是使用大型或弥散[基组](@entry_id:160309)时，AO[基组](@entry_id:160309)可能出现 **近似线性相关**。这表现为[重叠矩阵](@entry_id:268881) $\mathbf{S}$ 的某些[本征值](@entry_id:154894)非常接近于零。直接计算 $\mathbf{S}^{-1/2}$ 会因为除以一个极小的数而导致严重的数值不稳定 [@problem_id:2895861]。

更稳健的方法是 **正则正交化**（canonical orthogonalization）。首先对 $\mathbf{S}$进行对角化：$\mathbf{S} = \mathbf{U}\boldsymbol{\Lambda}\mathbf{U}^\dagger$。然后，舍弃那些[本征值](@entry_id:154894) $\lambda_i$ 小于某个阈值 $\lambda_{\text{cut}}$ 的[本征向量](@entry_id:151813)。例如，给定谱 $\{2.05, 1.98, ..., 7.0\times 10^{-6}, 3.5\times 10^{-8}\}$ 和阈值 $\lambda_{\text{cut}} = 2.05 \times 10^{-5}$，我们会舍弃最后两个[本征值](@entry_id:154894)对应的维度 [@problem_id:2895861]。然后，仅使用保留下来的 $p$ 个[本征向量](@entry_id:151813) $\mathbf{U}_p$ 和[本征值](@entry_id:154894) $\boldsymbol{\Lambda}_p$ 来构建变换矩阵 $\mathbf{X} = \mathbf{U}_p \boldsymbol{\Lambda}_p^{-1/2}$。这样，我们就将问题转化到了一个维度更小但数值稳定的[正交基](@entry_id:264024)上。

### [正则轨道](@entry_id:183413)与[轨道](@entry_id:137151)旋转自由度

通过求解[Roothaan-Hall方程](@entry_id:146169)得到的分子[轨道](@entry_id:137151)，即[Fock矩阵](@entry_id:203184)的[本征向量](@entry_id:151813)，被称为 **[正则分子轨道](@entry_id:197442)**（canonical molecular orbitals）。它们的特殊之处在于，在这些[轨道](@entry_id:137151)的表象下，[Fock矩阵](@entry_id:203184)是对角的，对角元就是[轨道](@entry_id:137151)能 $\epsilon_i$。

然而，需要强调的是，对于一个给定的Hartree-Fock解，其总能量和总电子密度是唯一的，但产生这个解的占据分子[轨道](@entry_id:137151)却不是唯一的。根据[斯莱特行列式](@entry_id:139034)的性质，对占据[轨道](@entry_id:137151)进行任意的[酉变换](@entry_id:152599)（unitary transformation），或者对[虚轨道](@entry_id:188499)进行任意的[酉变换](@entry_id:152599)，并不会改变总的斯莱特行列式[波函数](@entry_id:147440)（最多相差一个相位因子），因此也 **不会改变总能量和电子密度** [@problem_id:2895930] [@problem_id:2895866]。

[Hartree-Fock能量](@entry_id:171145)仅仅是占据[轨道](@entry_id:137151)所张成的空间（由投影算符 $\mathbf{P} = \mathbf{C}_{\text{occ}}\mathbf{C}_{\text{occ}}^\dagger$ 描述）的函数 [@problem_id:2895866]。只要[酉变换](@entry_id:152599)不混合占据[轨道](@entry_id:137151)和[虚轨道](@entry_id:188499)，这个[投影算符](@entry_id:154142)就不变，能量也就不变。

$$
\mathbf{C}'_{\text{occ}} = \mathbf{C}_{\text{occ}}\mathbf{U} \implies \mathbf{P}' = (\mathbf{C}_{\text{occ}}\mathbf{U})(\mathbf{C}_{\text{occ}}\mathbf{U})^\dagger = \mathbf{C}_{\text{occ}}\mathbf{U}\mathbf{U}^\dagger\mathbf{C}_{\text{occ}}^\dagger = \mathbf{C}_{\text{occ}}\mathbf{C}_{\text{occ}}^\dagger = \mathbf{P}
$$

这一[轨道](@entry_id:137151)旋转的自由度非常重要。虽然[正则轨道](@entry_id:183413)在数学上很简洁，但它们通常是离域的，遍布整个分子。通过对正则占据[轨道](@entry_id:137151)进行适当的[酉变换](@entry_id:152599)，我们可以得到化学上更直观的 **定域化分子[轨道](@entry_id:137151)**（localized molecular orbitals），例如对应于化学键或孤对电子的[轨道](@entry_id:137151)，而体系的总能量和密度等性质保持不变。

使[Hartree-Fock能量](@entry_id:171145)达到稳定（极小值）的条件是[布里渊定理](@entry_id:166170)（Brillouin's theorem），它要求[Fock矩阵](@entry_id:203184)在占据[轨道](@entry_id:137151)和[虚轨道](@entry_id:188499)之间的矩阵元为零。这意味着在任何一组满足该条件的[轨道](@entry_id:137151)表象下，[Fock矩阵](@entry_id:203184)都是块对角的。[正则轨道](@entry_id:183413)则是通过进一步在占据块和[虚轨道](@entry_id:188499)块内部进行对角化得到的特殊[轨道](@entry_id:137151)集合 [@problem_id:2895866]。

### RHF 与 UHF

最后，我们根据对自旋轨道的不同限制，区分两种最常见的[Hartree-Fock方法](@entry_id:138063)：限制性（Restricted）和非限制性（Unrestricted）Hartree-Fock [@problem_id:2895890]。

-   **限制性Hartree-Fock (RHF):** 主要用于闭壳层体系（即所有电子都成对）。它强制要求每个空间[轨道](@entry_id:137151) $\phi_i$ 都被两个自旋相反的电子（$\alpha$ 和 $\beta$）占据。这意味着 $\alpha$ 电子的[密度矩阵](@entry_id:139892)与 $\beta$ 电子的密度矩阵相同，即 $D^\alpha = D^\beta = \frac{1}{2}P$。在这种情况下，只有一个统一的[Fock矩阵](@entry_id:203184)需要求解：
    $$
    F_{\text{RHF}} = h + J[P] - \frac{1}{2}K[P]
    $$
    这里的 $J[P]$ 来自于所有电子的[库仑排斥](@entry_id:181876)，$K[P]$ 则包含了任意一个电子与其同自旋电子云（密度为$\frac{1}{2}P$）的交换作用。

-   **非限制性[Hartree-Fock](@entry_id:142303) (UHF):** 用于[开壳层体系](@entry_id:168723)（存在未成对电子）或需要描述键断裂等过程。UHF允许 $\alpha$ 自旋的电子和 $\beta$ 自旋的电子拥有不同的空间[轨道](@entry_id:137151)。因此，存在两套独立的分子[轨道](@entry_id:137151)系数和[密度矩阵](@entry_id:139892)，$D^\alpha$ 和 $D^\beta$。这也导致了两个不同的[Fock矩阵](@entry_id:203184)：
    $$
    \begin{align*}
    F^{\alpha} = h + J[D^{\alpha}+D^{\beta}] - K[D^{\alpha}] \\
    F^{\beta} = h + J[D^{\alpha}+D^{\beta}] - K[D^{\beta}]
    \end{align*}
    $$
    每个[Fock矩阵](@entry_id:203184)都包含来自所有电子的总[库仑排斥](@entry_id:181876) $J[D^\alpha+D^\beta]$，但交换项只来自于同自旋的电子。$F^\alpha$ 中的交换项 $-K[D^\alpha]$ 只考虑了与 $\alpha$ 电子云的交换，而 $F^\beta$ 中的交换项 $-K[D^\beta]$ 只考虑了与 $\beta$ 电子云的交换。这两套方程必须同时求解直至自洽。

综上所述，Hartree-Fock-Roothaan方法通过LCAO近似和SCF迭代过程，为在有限[基组](@entry_id:160309)下求解Hartree-Fock问题提供了一套完整且在计算上可行的方案，构成了现代[量子化学](@entry_id:140193)计算的理论基石。对这一过程的深入理解，对于正确应用和解读[量子化学](@entry_id:140193)计算结果至关重要。