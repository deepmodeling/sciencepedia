## 引言
原子在外部静电场和静[磁场](@entry_id:153296)中表现出的[斯塔克效应](@entry_id:146306)与[塞曼效应](@entry_id:154144)，是量子世界中最基本也最深刻的现象之一。它们不仅是早期量子力学理论的决定性实验证据，至今仍是探索[原子结构](@entry_id:137190)、诊断复杂物理环境以及发展前沿[量子技术](@entry_id:142946)的基石。然而，从对这些效应的初步认识到真正从第一性原理层面深入理解其复杂的量子机制，存在着一条需要严谨理论推导和跨学科视野才能跨越的鸿沟。本文旨在填补这一知识间隙，为读者构建一个关于斯塔克与塞曼效应的完整知识框架。

在接下来的内容中，我们将开启一段从理论核心到实际应用的探索之旅。在“**原理与机制**”一章中，我们将从基本的泡利[哈密顿量](@entry_id:172864)出发，利用微扰论系统地分析外场如何改变原子的能级结构，并揭示不同效应（如[线性斯塔克效应](@entry_id:149905)、[反常塞曼效应](@entry_id:151878)）出现的物理根源。随后，在“**应用与交叉学科联系**”一章，我们将展示这些理论如何在真实世界中大放异彩，从[高分辨率光谱学](@entry_id:163705)、天体物理到分析化学和冷原子物理。最后，“**动手实践**”部分将提供一系列计算练习，帮助读者将抽象的理论转化为具体的计算能力。让我们首先深入其核心，从量子力学的角度剖析这两种效应的原理与机制。

## 原理与机制

本章旨在深入阐述原子在外部[静电场](@entry_id:268546)和静[磁场](@entry_id:153296)中所表现出的斯塔克（Stark）效应和塞曼（Zeeman）效应的物理原理与量子力学机制。我们将从最基本的[哈密顿量](@entry_id:172864)出发，系统地推导出各种相互作用项，并利用微扰论来分析它们对[原子能级](@entry_id:148255)结构的影响。本章内容假定读者已具备量子力学和原子物理的基础知识。

### 基本[相互作用[哈密顿](@entry_id:181720)量](@entry_id:172864)

描述一个非相对论性的、具有自旋的电子在[电磁场](@entry_id:265881)中运动的最基本出发点是泡利[哈密顿量](@entry_id:172864)（Pauli Hamiltonian）。通过[最小耦合](@entry_id:148226)（minimal coupling）原理，将[电磁场](@entry_id:265881)的[四维矢量势](@entry_id:188407) $(A_0, \mathbf{A})$ 引入到自由粒子的薛定谔方程中，我们得到考虑了外场的总[哈密顿量](@entry_id:172864)。对于束缚在[库仑势](@entry_id:154276) $V_C(\mathbf{r})$ 中的单个电子（[电荷](@entry_id:275494) $q=-e$，质量 $m_e$），在静场 $\mathbf{E}$ 和 $\mathbf{B}$ 中，其[哈密顿量](@entry_id:172864)为 [@problem_id:2927335]：

$$
\hat{H}=\frac{1}{2m_e}\left[\hat{\mathbf{p}}-q\mathbf{A}(\mathbf{r})\right]^2+q\phi(\mathbf{r})+V_{C}(\mathbf{r})-\frac{q\hbar}{2m_e}\boldsymbol{\sigma}\cdot \mathbf{B}
$$

这里，$\hat{\mathbf{p}}$ 是动量算符，$\boldsymbol{\sigma}$ 是泡利矩阵矢量。标量势 $\phi(\mathbf{r})$ 和矢量势 $\mathbf{A}(\mathbf{r})$ 分别与电场和磁场相关。对于均匀静场，我们可以选择特定的规范。例如，对于均匀[电场](@entry_id:194326) $\mathbf{E}$，可取 $\phi(\mathbf{r})=-\mathbf{E}\cdot \mathbf{r}$；对于均匀[磁场](@entry_id:153296) $\mathbf{B}$，可取对称规范 $\mathbf{A}(\mathbf{r})=\frac{1}{2}\mathbf{B}\times \mathbf{r}$，此规范满足[库仑规范](@entry_id:273044)条件 $\boldsymbol{\nabla}\cdot \mathbf{A}=0$。

将动能项展开，并利用在[库仑规范](@entry_id:273044)下 $\hat{\mathbf{p}}$ 与 $\mathbf{A}$ 的对易关系（$\hat{\mathbf{p}}\cdot\mathbf{A} = \mathbf{A}\cdot\hat{\mathbf{p}}$），总[哈密顿量](@entry_id:172864)可以分解为[零场](@entry_id:199169)[哈密顿量](@entry_id:172864) $\hat{H}_0 = \frac{\hat{\mathbf{p}}^2}{2m_e} + V_C(\mathbf{r})$ 和一个微扰[哈密顿量](@entry_id:172864) $\hat{H}'$：

$$
\hat{H} = \hat{H}_0 + \hat{H}'
$$

其中，微扰项 $\hat{H}'$ 包含了所有与外场相关的相互作用：

$$
\hat{H}' = q\phi(\mathbf{r}) - \frac{q}{m_e}\mathbf{A}\cdot\hat{\mathbf{p}} + \frac{q^2}{2m_e}\mathbf{A}^2 - \frac{q\hbar}{2m_e}\boldsymbol{\sigma}\cdot\mathbf{B}
$$

将[规范势](@entry_id:188985)的具体形式代入，并利用矢量恒等式和轨道角动量算符的定义 $\hat{\mathbf{L}}=\mathbf{r}\times\hat{\mathbf{p}}$，我们可以识别出各个物理项 [@problem_id:2927335]：

1.  **斯塔克项（Stark Term）**: 这是与电场线性相关的项，源于 $q\phi(\mathbf{r})$。
    $$
    \hat{H}'_{Stark} = -q\mathbf{E}\cdot\mathbf{r} = e\mathbf{E}\cdot\mathbf{r}
    $$
    这代表了原子中电子的[电偶极矩](@entry_id:178520) $\mathbf{d}=-e\mathbf{r}$ 与外[电场](@entry_id:194326)的相互作用能。

2.  **[轨道](@entry_id:137151)塞曼项（Orbital Zeeman Term）**: 这是与[磁场](@entry_id:153296)和[轨道角动量](@entry_id:191303)[线性相关](@entry_id:185830)的项，源于 $-\frac{q}{m_e}\mathbf{A}\cdot\hat{\mathbf{p}}$。
    $$
    \hat{H}'_{B,orb} = -\frac{q}{2m_e}\mathbf{B}\cdot\hat{\mathbf{L}} = \frac{e}{2m_e}\mathbf{B}\cdot\hat{\mathbf{L}} = \frac{\mu_B}{\hbar}\mathbf{B}\cdot\hat{\mathbf{L}}
    $$
    其中 $\mu_B = \frac{e\hbar}{2m_e}$ 是**[玻尔磁子](@entry_id:151037)**。

3.  **自旋塞曼项（Spin Zeeman Term）**: 这是与[磁场](@entry_id:153296)和[自旋角动量](@entry_id:149719)线性相关的项，是泡利[哈密顿量](@entry_id:172864)中明确包含的。
    $$
    \hat{H}'_{B,spin} = -\frac{q g_s}{2m_e}\mathbf{S}\cdot\mathbf{B} = \frac{e g_s}{2m_e}\mathbf{S}\cdot\mathbf{B} = \frac{g_s\mu_B}{\hbar}\mathbf{S}\cdot\mathbf{B}
    $$
    其中 $\mathbf{S}=\frac{\hbar}{2}\boldsymbol{\sigma}$ 是自旋角动量算符，而 $g_s \approx 2.0023$ 是电子的**自旋[g因子](@entry_id:153442)**，通常近似为 $2$。

4.  **抗磁项（Diamagnetic Term）**: 这是与[磁场](@entry_id:153296)二次方相关的项，源于 $\frac{q^2}{2m_e}\mathbf{A}^2$。
    $$
    \hat{H}'_{dia} = \frac{q^2}{8m_e}(\mathbf{B}\times\mathbf{r})^2 = \frac{e^2}{8m_e}(B^2r^2 - (\mathbf{B}\cdot\mathbf{r})^2)
    $$
    该项通常比线性塞曼项小得多，仅在强[磁场](@entry_id:153296)或研究高精度谱时才重要。

将这些微扰项应用于原子的定态，需要使用**微扰论**。微扰论的有效性取决于微扰的[能量尺度](@entry_id:196201)远小于未微扰能级之间的能量间隔。对于主量子数为 $n_0$ 的[类氢原子](@entry_id:164890)，其能级间隔尺度为 $\Delta E \sim E_{\mathrm{h}} \frac{Z^2}{n_0^3}$，而[原子尺寸](@entry_id:151650)尺度为 $r \sim a_0 \frac{n_0^2}{Z}$。通过比较斯塔克和塞曼相互作用的矩阵元与此能级间隔，可以导出微扰论适用的场强范围 [@problem_id:2927364]。分析表明，外场必须远小于原子内部的等效场，例如，对于氢[原子基态](@entry_id:194487)，[电场](@entry_id:194326)需远小于 $E_{\mathrm{au}} \approx 5.1 \times 10^{11}\,\mathrm{V\,m^{-1}}$，[磁场](@entry_id:153296)需远小于 $B_{\mathrm{au}} \approx 4.7 \times 10^{5}\,\mathrm{T}$。在典型的实验室条件下，这些条件通常是满足的。

### [斯塔克效应](@entry_id:146306)：原子与[电场](@entry_id:194326)的相互作用

[斯塔克效应](@entry_id:146306)描述的是[原子能级](@entry_id:148255)在外[电场](@entry_id:194326)中的移动和分裂。其核心是微扰[哈密顿量](@entry_id:172864) $\hat{H}'_{Stark} = eEz$ (假设[电场](@entry_id:194326)沿 $z$ 轴)。

#### 一阶斯塔克效应与宇称

根据非简并微扰论，能级的[一阶修正](@entry_id:155896)为 $\Delta E^{(1)} = \langle \psi | \hat{H}'_{Stark} | \psi \rangle = eE \langle \psi | z | \psi \rangle$，其中 $|\psi\rangle$ 是原子的未微扰本征态。对于束缚态，其[波函数](@entry_id:147440)具有确定的**宇称**（parity）。例如，[原子轨道](@entry_id:140819) $|n,l,m\rangle$ 的宇称是 $(-1)^l$。微扰算符 $z$ 是一个奇[宇称算符](@entry_id:148434)，因为在空间反演操作 $\mathbf{r} \to -\mathbf{r}$ 下，$z \to -z$。对于任何一个具有确定宇称的态 $|\psi\rangle$，其内部一个奇[宇称算符](@entry_id:148434)的[期望值](@entry_id:153208)必定为零。

$$
\langle z \rangle = \langle \psi | z | \psi \rangle = 0
$$

这意味着对于任何非简并的、具有确定宇称的[原子能级](@entry_id:148255)（例如，除氢原子外的多数原子的[基态](@entry_id:150928)），一阶斯塔克效应为零 [@problem_id:2927330] [@problem_id:2927346]。这是一个非常重要的[选择定则](@entry_id:140784)：**没有[永久电偶极矩](@entry_id:178322)的原子（即 $\langle \mathbf{d} \rangle = 0$）不会表现出一阶（线性）斯塔克效应**。作用在电子上的静电力 $\mathbf{F}=-\boldsymbol{\nabla}(eEz) = -eE\hat{\mathbf{z}}$，方向与[电场](@entry_id:194326)相反，但这种力在定态中的平均效应由于对称性而被抵消了 [@problem_id:2927330]。

#### 氢原子的[线性斯塔克效应](@entry_id:149905)与[抛物线坐标](@entry_id:166304)

[线性斯塔克效应](@entry_id:149905)的出现有一个关键前提：[能级简并](@entry_id:140812)，并且简并的子能级之间具有相反的宇称。氢原子（以及[类氢离子](@entry_id:174450)）是这一现象的典型例子。在忽略[精细结构](@entry_id:140861)时，氢原子的能级仅依赖于[主量子数](@entry_id:143678) $n$，而对于给定的 $n>1$，具有不同[轨道角动量量子数](@entry_id:167573) $l$ (例如 $2s$ 和 $2p$) 的态是简并的。由于 $s$ 态 ($l=0$) 是偶宇称，而 $p$ 态 ($l=1$) 是[奇宇称](@entry_id:147965)，斯塔克微扰算符 $z$ 在它们之间具有非零的矩阵元，如 $\langle 2s | z | 2p_z \rangle \neq 0$。

这种情况下，必须使用**简并微扰论**，在简并[子空间](@entry_id:150286)内对微扰[哈密顿量](@entry_id:172864)进行[对角化](@entry_id:147016)。对于氢原子，一个特别有效的处理方法是使用**[抛物线坐标](@entry_id:166304)** $(\xi, \eta, \phi)$。薛定谔方程在这些坐标下对[库仑问题](@entry_id:199261)和 $z$ 方向的斯塔克问题都是可分离的。其[本征态](@entry_id:149904)由一组新的量子数**抛物线量子数** $(n_1, n_2, m)$ 标记，它们与主量子数 $n$ 的关系为 $n = n_1 + n_2 + |m| + 1$ [@problem_id:2927349]。

在[抛物线坐标](@entry_id:166304)基下，斯塔克微扰[哈密顿量](@entry_id:172864) $\hat{H}'_{Stark}$ 是对角的。这背后深刻的对称性原因是，在给定的 $n$ [流形](@entry_id:153038)内，$z$ 算符与**[龙格-楞次矢量](@entry_id:168301)**（Runge-Lenz vector）的 $z$ 分量 $\hat{A}_z$ 成正比。抛物线态正是 $\hat{H}_0$, $\hat{L}_z$ 和 $\hat{A}_z$ 的共同本征态。因此，[一阶能量修正](@entry_id:143593)直接由这些量子数给出：

$$
\Delta E^{(1)} = \frac{3}{2} n (n_1 - n_2) e a_0 E
$$

其中 $k = n_1-n_2$ 是一个整数，称为电[量子数](@entry_id:145558)。这导致了原先简并的[能级分裂](@entry_id:193178)成 $2n-1$ 个等间距的子能级，其能量移动与[电场](@entry_id:194326)强度 $E$ 成正比。

#### 二阶斯塔克效应与[原子极化率](@entry_id:161626)

对于没有宇称简并的能级，例如氢原子的 $1s$ [基态](@entry_id:150928)或碱金属原子的[基态](@entry_id:150928)，主要的[斯塔克效应](@entry_id:146306)是二阶效应。根据二阶微扰论，[能量修正](@entry_id:198270)为 [@problem_id:2927346]：

$$
\Delta E^{(2)} = \sum_{k \neq 0} \frac{|\langle k | \hat{H}'_{Stark} | 0 \rangle|^2}{E_0 - E_k} = -e^2 E^2 \sum_{k \neq 0} \frac{|\langle k | z | 0 \rangle|^2}{E_k - E_0}
$$

其中 $|0\rangle$ 是我们关注的[基态](@entry_id:150928)，求和遍及所有其他（分立与连续的）本征态 $|k\rangle$。对于[基态](@entry_id:150928)，能量 $E_0$ 是最低的，所以分母 $E_k - E_0$ 总是正的。因此，$\Delta E^{(2)}$ 总是负的。这意味着外[电场](@entry_id:194326)总会使[基态能量](@entry_id:263704)降低，从而使原子稳定化。这种能量降低可以理解为[电场](@entry_id:194326)诱导出一个电偶极矩，该[诱导偶极矩](@entry_id:262417)与[电场](@entry_id:194326)相互作用的结果。

这种二次方的能量移动通常用**[原子极化率](@entry_id:161626)**（atomic polarizability）$\alpha$ 来描述：

$$
\Delta E^{(2)} = -\frac{1}{2} \alpha E^2
$$

比较两个表达式，我们得到极化率的量子力学表达式（也称为Kramers-Heisenberg公式）：

$$
\alpha = 2e^2 \sum_{k \neq 0} \frac{|\langle k | z | 0 \rangle|^2}{E_k - E_0}
$$

极化率 $\alpha$ 是一个衡量原子在外[电场](@entry_id:194326)中被极化难易程度的物理量，它是一个恒正的量 [@problem_id:2927346]。

#### 高等专题：标量与[张量极化](@entry_id:197114)率

对于具有[总角动量](@entry_id:155748) $J \ge 1$ 的能级，情况更为复杂。外[电场](@entry_id:194326)不仅会使整个能级的能量移动，还会破坏其旋转对称性，导致原先简并的 $m_J$ 子能级发生分裂。此时，二阶[斯塔克效应](@entry_id:146306)可以用两个参数来描述：**标量极化率** $\alpha_0$ 和**[张量极化](@entry_id:197114)率** $\alpha_2$ [@problem_id:2927353]。

能量移动的表达式为：

$$
\Delta E_{Jm_J} = -\frac{1}{2} E^2 \left[\alpha_0(J) + \alpha_2(J) \frac{3m_J^2 - J(J+1)}{J(2J-1)}\right]
$$

这里，$\alpha_0$ 描述了所有 $m_J$ 子能级的平均能量移动，而 $\alpha_2$ 描述了依赖于 $m_J^2$ 的[能级分裂](@entry_id:193178)。$\alpha_2$ 项只有在 $J \ge 1$ 时才存在，因为它来源于一个[二阶张量](@entry_id:199780)相互作用。这种分解是通过不可约[张量算符](@entry_id:203590)方法得到的，它清晰地分离了相互作用的几何（依赖于 $m_J$）和动力学（包含在 $\alpha_0, \alpha_2$ 的求和表达式中）部分 [@problem_id:2927353]。

### [塞曼效应](@entry_id:154144)：原子与[磁场](@entry_id:153296)的相互作用

塞曼效应描述的是[原子能级](@entry_id:148255)在外[磁场](@entry_id:153296)中的分裂。其核心是[磁偶极矩](@entry_id:158175) $\boldsymbol{\mu}$ 与[磁场](@entry_id:153296) $\mathbf{B}$ 的相互作用 $\hat{H}'_Z = -\boldsymbol{\mu} \cdot \mathbf{B}$。原子的总磁矩由[轨道磁矩](@entry_id:159585)和[自旋磁矩](@entry_id:272337)构成：

$$
\boldsymbol{\mu} = \boldsymbol{\mu}_L + \boldsymbol{\mu}_S = -\frac{\mu_B}{\hbar}(\mathbf{L} + g_s \mathbf{S})
$$

由于电子的自旋[g因子](@entry_id:153442) $g_s \approx 2$ 不等于1，导致 $\boldsymbol{\mu}$ 与总角动量 $\mathbf{J} = \mathbf{L}+\mathbf{S}$ 不共线。这是理解不同塞曼效应机制的关键。

#### 弱场机制：[反常塞曼效应](@entry_id:151878)

当外[磁场](@entry_id:153296)引起的相互作用远小于原子内部的**[自旋-轨道耦合](@entry_id:143520)**（spin-orbit coupling）时，我们称之为弱场机制。在这种情况下，$\mathbf{L}$ 和 $\mathbf{S}$ 首先耦合形成[总角动量](@entry_id:155748) $\mathbf{J}$，$\mathbf{J}$ 是一个近似的[好量子数](@entry_id:262514)。微扰[哈密顿量](@entry_id:172864) $\hat{H}'_Z$ 在 $|L,S,J,m_J\rangle$ [基矢](@entry_id:199546)下计算。

由于 $\hat{L}_z$ 和 $\hat{S}_z$ 与 $\hat{J}^2$ 不对易，我们不能直接取它们的[期望值](@entry_id:153208)。根据**[投影定理](@entry_id:142268)**（[Wigner-Eckart定理](@entry_id:144878)的推论），在一个固定的 $J$ [流形](@entry_id:153038)内，任何矢量算符（如 $\mathbf{L}$ 或 $\mathbf{S}$）的[期望值](@entry_id:153208)都正比于 $\mathbf{J}$ 的[期望值](@entry_id:153208)。这导致了磁矩的有效分量是其沿着 $\mathbf{J}$ 方向的投影。经过推导，[一阶能量修正](@entry_id:143593)为 [@problem_id:2927320] [@problem_id:2927334]：

$$
\Delta E_Z = g_J \mu_B B m_J
$$

其中 $g_J$ 是**[朗德g因子](@entry_id:146126)**（Landé g-factor），其表达式为：

$$
g_J = 1 + \frac{J(J+1) + S(S+1) - L(L+1)}{2J(J+1)} \quad (\text{使用 } g_s = 2)
$$

由于 $g_J$ 的值通常不是整数，一个给定的 $J$ 能级会分裂成 $2J+1$ 个等间距的子能级，其间距由 $g_J$ 决定。不同能级（具有不同的 $L,S,J$）的 $g_J$ 值不同，导致[光谱跃迁](@entry_id:197033)产生复杂的分裂图案，这被称为**[反常塞曼效应](@entry_id:151878)**（Anomalous Zeeman Effect）。其“反常”之处正在于 $g_s \neq 1$ 这一事实。例如，对于一个 $^{2}P$ 项（$L=1, S=1/2$），它分裂成 $J=1/2$ 和 $J=3/2$ 两个精细结构能级。它们的[朗德g因子](@entry_id:146126)分别为 $g_{J=1/2}=2/3$ 和 $g_{J=3/2}=4/3$，导致了截然不同的[磁场](@entry_id:153296)分裂模式 [@problem_id:2927320]。

#### 特例：[正常塞曼效应](@entry_id:153375)

当原子的[总自旋](@entry_id:153335) $S=0$ 时（即处于[单重态](@entry_id:154728)），情况变得简单。此时 $\mathbf{J}=\mathbf{L}$，代入 $S=0$ 到 $g_J$ 的公式中，我们得到 $g_J=1$。[能量修正](@entry_id:198270)简化为：

$$
\Delta E_Z = \mu_B B m_J = \mu_B B m_L
$$

能级分裂只与[轨道](@entry_id:137151)磁量子数 $m_L$ 有关，与能级本身无关。在[电偶极跃迁](@entry_id:149662)[选择定则](@entry_id:140784) $\Delta m_L = 0, \pm 1$ 下，任何[光谱](@entry_id:185632)线都只会分裂成三条等间距的[谱线](@entry_id:193408)（洛伦兹三线态），其能量差为 $\pm \mu_B B$。这种简单的分裂模式被称为**[正常塞曼效应](@entry_id:153375)**（Normal Zeeman Effect），它在历史上先于[反常塞曼效应](@entry_id:151878)被发现和解释 [@problem_id:2927334]。

#### 强场机制：帕申-巴克效应

当外[磁场](@entry_id:153296)非常强，使得塞曼相互作用的能量远大于自旋-轨道耦合能时，$\mathbf{L}$ 和 $\mathbf{S}$ 之间的耦合被“打破”。此时，$\mathbf{L}$ 和 $\mathbf{S}$ 不再耦合形成 $\mathbf{J}$，而是各自独立地围绕外[磁场](@entry_id:153296) $\mathbf{B}$ 进动。在这种**帕申-巴克效应**（Paschen-Back Effect）机制下，好的[量子数](@entry_id:145558)不再是 $J$ 和 $m_J$，而是 $m_L$ 和 $m_S$。

此时，主要的[能量修正](@entry_id:198270)是由塞曼[哈密顿量](@entry_id:172864)对角部分给出：

$$
\Delta E_{PB} \approx \langle m_L, m_S | \hat{H}'_Z | m_L, m_S \rangle = \mu_B B (m_L + g_s m_S)
$$

而[自旋-轨道耦合](@entry_id:143520) $H_{SO} = A \mathbf{L}\cdot\mathbf{S}$ 则成为需要在 $(m_L, m_S)$ 基上处理的小微扰。从弱场到强场的过渡区是复杂的，需要对包含自旋-轨道耦合和塞曼相互作用的总[哈密顿量](@entry_id:172864)进行[对角化](@entry_id:147016)。这个过渡的[临界场](@entry_id:272263)强 $B_c$ 可以通过比较塞曼[能量尺度](@entry_id:196201) $\mu_B B$ 与[精细结构分裂](@entry_id:169442)能标来估计。例如，对于锂原子的 $2p\,{}^{2}P$ 项，其精细结构劈裂约为 $0.335\,\mathrm{cm}^{-1}$，对应的[临界场](@entry_id:272263)强约为 $0.478\,\mathrm{T}$ [@problem_id:2927339]。

### 组合场与复杂情况

当原子同时处于非共线的[电场](@entry_id:194326) $\mathbf{E}$ 和[磁场](@entry_id:153296) $\mathbf{B}$ 中时，情况变得尤为复杂。通常，我们会选择一个方便的量子化轴，例如沿着[磁场](@entry_id:153296)方向。如果[电场](@entry_id:194326)不与该轴平行，它就会引入破坏[轴对称](@entry_id:173333)性的项。

考虑将量子化轴（$z$ 轴）选在 $\mathbf{B}$ 方向。塞曼[哈密顿量](@entry_id:172864) $V_B$ 与 $J_z$ 对易。然而，如果 $\mathbf{E}$ 具有垂直于 $z$ 轴的分量（例如 $E_x \neq 0$），斯塔克[哈密顿量](@entry_id:172864) $V_E = e(E_x x + E_y y + E_z z)$ 将包含 $x$ 和 $y$ 项。这些项在角[动量表象](@entry_id:156131)中对应于[选择定则](@entry_id:140784)为 $\Delta m_J = \pm 1$ 的算符。因此，总的微扰[哈密顿量](@entry_id:172864) $V = V_B + V_E$ 不再与 $J_z$ 对易 [@problem_id:2927327]：

$$
[V, J_z] = [V_E, J_z] \neq 0 \quad (\text{如果 } \mathbf{E} \not\parallel \hat{\mathbf{z}})
$$

这意味着在存在非共线场时，$m_J$ 不再是[好量子数](@entry_id:262514)，不同 $m_J$ 的子能级之间会发生混合。从更根本的层面看，塞曼[哈密顿量](@entry_id:172864) $V_B$ 与斯塔克[哈密顿量](@entry_id:172864) $V_E$ 本身也不对易，其对易子为 $[V_B, V_E] \propto i(\mathbf{B}\times\mathbf{E})\cdot\mathbf{r}$。只要场是非共线的，这对易子就不为零，表明不存在一个共同的本征基可以[同时对角化](@entry_id:196036)这两个相互作用。因此，不存在一个“万能的”量子化轴能够避免所有非对角耦合 [@problem_id:2927327]。这揭示了对称性在决定量子系统行为中的核心作用：外场的对称性直接决定了系统[守恒量](@entry_id:150267)和能谱的结构。