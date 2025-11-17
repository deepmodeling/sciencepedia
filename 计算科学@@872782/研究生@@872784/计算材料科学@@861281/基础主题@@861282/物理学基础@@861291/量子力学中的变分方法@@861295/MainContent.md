## 引言
在量子力学的宏伟殿堂中，薛定谔方程是描述微观世界行为的中心法则。然而，除了少数高度理想化的模型外，对绝大多数真实物理系统（如多电子原子、分子和固体材料）而言，精确求解该方程几乎是不可能的。这一挑战催生了量子力学中一些最强大、最富有创造性的近似方法，其中，[变分法](@entry_id:163656)（Variational Method）以其深刻的物理洞察、严谨的数学基础和无与伦比的普适性而占据核心地位。它不仅是一种计算工具，更是一种系统性地将物理直觉转化为定量模型的强大思想框架。

本文旨在为读者提供一个关于[量子力学变分法](@entry_id:154442)的全面而深入的视角。我们将不再局限于教科书式的介绍，而是系统地揭示其理论精髓与实践力量。在“原理与机制”一章中，我们将从[变分原理](@entry_id:198028)的严格数学证明出发，阐明其如何保证我们得到的近似能量是真实基态能量的可靠上限，并详细介绍如何通过[参数化](@entry_id:272587)的[试探波函数](@entry_id:142892)和强大的里利-里兹方法系统地逼近解。接着，在“应用与跨学科连接”一章中，我们将穿越学科的边界，探索[变分法](@entry_id:163656)如何在[量子化学](@entry_id:140193)、凝聚态物理、[材料科学](@entry_id:152226)乃至[量子计算](@entry_id:142712)等前沿领域中大放异彩，从解释[化学键](@entry_id:138216)的本质到设计新型[拓扑材料](@entry_id:142123)和[量子算法](@entry_id:147346)。最后，通过一系列精心设计的“动手实践”练习，您将有机会亲手应用这些方法，将抽象的理论转化为具体的计算技能，从而真正内化对[变分法](@entry_id:163656)的理解。

## 原理与机制

继前一章对量子力学中变分思想的介绍之后，本章将深入探讨其核心的数学原理和具体的应用机制。我们将从[变分原理](@entry_id:198028)的严格证明出发，系统地阐述如何通过[参数化](@entry_id:272587)的[试探波函数](@entry_id:142892)和线性组合的里利-里兹方法来近似求解量子体系的[基态](@entry_id:150928)和[激发态](@entry_id:261453)。最后，我们将讨论该原理在更广阔的理论框架（如[密度泛函理论](@entry_id:139027)）中的应用，并审视其在无穷维[希尔伯特空间](@entry_id:261193)中所面临的数学严谨性问题与内在局限性。

### 里利-里兹商与变分原理

量子力学中[变分方法](@entry_id:163656)的核心是**里利-里兹商 (Rayleigh Quotient)**，对于一个给定的[哈密顿算符](@entry_id:144286) $\hat{H}$ 和任意一个非零的[试探波函数](@entry_id:142892) $|\psi\rangle$，里利-里兹商定义为[哈密顿量](@entry_id:172864)的[期望值](@entry_id:153208)：

$R_H(\psi) = \frac{\langle \psi | \hat{H} | \psi \rangle}{\langle \psi | \psi \rangle}$

对于归一化的[波函数](@entry_id:147440)（即 $\langle \psi | \psi \rangle = 1$），里利-里兹商简化为[能量期望值](@entry_id:174035) $\langle E \rangle = \langle \psi | \hat{H} | \psi \rangle$。变分方法最重要的基石是**变分原理 (Variational Principle)**，它断言：对于任何一个行为良好的[试探波函数](@entry_id:142892) $|\psi\rangle$，其对应的[能量期望值](@entry_id:174035) $\langle E \rangle$ 永远不会低于体系真实的基态能量 $E_0$。这可以写成一个简洁而深刻的不等式：

$\langle E \rangle = \langle \psi | \hat{H} | \psi \rangle \geq E_0$

这个原理的证明是量子力学基础理论的直接推论，其关键在于[哈密顿算符](@entry_id:144286)的本征态构成了一个完备的正交归一[基组](@entry_id:160309) [@problem_id:2144180]。让我们来详细推导这个不等式。

假设体系的[哈密顿算符](@entry_id:144286) $\hat{H}$ 具有一组离散或连续的本征态 $\{|n\rangle\}$，对应的本征能量为 $\{E_n\}$，且满足本征方程 $\hat{H}|n\rangle = E_n|n\rangle$。我们将这些能量值排序，使得 $E_0 \le E_1 \le E_2 \le \dots$。由于这组[本征态](@entry_id:149904) $\{|n\rangle\}$ 是完备的，任何一个归一化的[试探波函数](@entry_id:142892) $|\psi\rangle$ 都可以被唯一地展开为这些[本征态](@entry_id:149904)的线性叠加：

$|\psi\rangle = \sum_n c_n |n\rangle$

其中，$c_n = \langle n | \psi \rangle$ 是展开系数。由于 $|\psi\rangle$ 是归一化的，这些系数必须满足[归一化条件](@entry_id:156486)：$\sum_n |c_n|^2 = 1$。现在，我们计算 $|\psi\rangle$ 的[能量期望值](@entry_id:174035)：

$\langle E \rangle = \langle \psi | \hat{H} | \psi \rangle = \left( \sum_m c_m^* \langle m | \right) \hat{H} \left( \sum_n c_n |n\rangle \right)$
$= \sum_{m,n} c_m^* c_n \langle m | \hat{H} | n \rangle$

利用本征方程 $\hat{H}|n\rangle = E_n|n\rangle$ 和[本征态](@entry_id:149904)的正交性 $\langle m|n\rangle = \delta_{mn}$，上式可以简化为：

$\langle E \rangle = \sum_{m,n} c_m^* c_n E_n \delta_{mn} = \sum_n |c_n|^2 E_n$

这个表达式的物理意义非常清晰：对于一个非[本征态](@entry_id:149904)，其[能量期望值](@entry_id:174035)是各个本征能量 $E_n$ 的加权平均，权重为该态布居在相应[本征态](@entry_id:149904)上的概率 $|c_n|^2$。

由于 $E_0$ 是所有[能量本征值](@entry_id:144381)中的最小值，即对于所有的 $n$ 都有 $E_n \ge E_0$，我们可以得到：

$\langle E \rangle = \sum_n |c_n|^2 E_n \ge \sum_n |c_n|^2 E_0 = E_0 \left( \sum_n |c_n|^2 \right)$

结合[归一化条件](@entry_id:156486) $\sum_n |c_n|^2 = 1$，我们最终证明了[变分原理](@entry_id:198028)：

$\langle E \rangle \ge E_0$

这个不等式中的等号成立的充要条件是，试探波函数 $|\psi\rangle$ 只包含[基态](@entry_id:150928)成分，即除了 $c_0$ 之外所有的 $c_n$ 都为零。换句话说，当且仅当试探波函数 $|\psi\rangle$ 就是真实的[基态](@entry_id:150928)[波函数](@entry_id:147440) $|0\rangle$ 时，计算出的[能量期望值](@entry_id:174035)才精确等于基态能量 $E_0$。

[变分原理](@entry_id:198028)的这个“上限”特性是一个非常强大的工具。例如，在早期对[氦原子基态](@entry_id:182645)能量的计算中，实验测定的基态能量约为 $-79.0 \, \text{eV}$。一个忽略电子间相互作用的简单模型给出的能量是 $-108.8 \, \text{eV}$，远低于实验值。而一个考虑了电子间排斥的变分计算得到的结果是 $-77.5 \, \text{eV}$。这个结果虽然没有达到实验的精确度，但它正确地位于实验值的上方（$-77.5 > -79.0$），这完美地印证了变分原理的预测，即任何近似计算得到的能量都是真实[基态能量](@entry_id:263704)的一个上限 [@problem_id:2042044]。

### 实践中的变分方法：求解近似解

[变分原理](@entry_id:198028)不仅提供了一个理论上的界限，更重要的是，它指明了一条寻找近似解的途径：通过构造一个依赖于某些参数的**[试探波函数](@entry_id:142892) (trial wavefunction)** $|\psi(\alpha_1, \alpha_2, \dots)\rangle$，然后调整这些参数，使得[能量期望值](@entry_id:174035) $E(\alpha_1, \alpha_2, \dots) = \langle \psi | \hat{H} | \psi \rangle$ 达到最小值。这个最小化的能量 $E_{\min}$ 就是在该[试探函数](@entry_id:756165)形式下对[基态能量](@entry_id:263704) $E_0$ 的最佳近似。

#### 解析最小化

在某些简单的情形下，我们可以选择一个具有解析形式的试探波函数，并通过微积分的方法直接找到能量的最小值。这种方法清晰地展示了变分法的核心操作流程。

我们以一个二维体系中的粒子为例 [@problem_id:404202]。假设一个质量为 $m$ 的粒子在极坐标 $(r, \theta)$ 下受到一个对数形式的中心对称势 $V(r) = C \ln(r/a)$ 的作用，其中 $C$ 和 $a$ 是正常数。该体系的[哈密顿算符](@entry_id:144286)为：

$\hat{H} = -\frac{\hbar^2}{2m} \left( \frac{\partial^2}{\partial r^2} + \frac{1}{r} \frac{\partial}{\partial r} + \frac{1}{r^2} \frac{\partial^2}{\partial \theta^2} \right) + C \ln(r/a)$

为了估算其基态能量，我们可以选择一个归一化的、不依赖于角度 $\theta$ 的高斯型试探波函数，它包含一个可变参数 $\alpha > 0$：

$\psi(r; \alpha) = \sqrt{\frac{2\alpha}{\pi}} e^{-\alpha r^2}$

应用[变分法](@entry_id:163656)的步骤如下：
1.  **计算动能[期望值](@entry_id:153208) $\langle T \rangle(\alpha)$**：通过计算 $\langle \psi | (-\frac{\hbar^2}{2m} \nabla^2) | \psi \rangle$ 得到 $\langle T \rangle(\alpha) = \frac{\hbar^2 \alpha}{m}$。
2.  **计算[势能](@entry_id:748988)[期望值](@entry_id:153208) $\langle V \rangle(\alpha)$**：通过计算 $\langle \psi | V(r) | \psi \rangle$ 得到 $\langle V \rangle(\alpha) = -\frac{C}{2}(\gamma+\ln(2\alpha))-C\ln a$，其中 $\gamma$ 是[欧拉-马歇罗尼常数](@entry_id:146205)。
3.  **构建总[能量泛函](@entry_id:170311) $E(\alpha)$**：将动能和[势能](@entry_id:748988)相加，得到依赖于参数 $\alpha$ 的总能量 $E(\alpha) = \frac{\hbar^2\alpha}{m}-\frac{C}{2}(\gamma+\ln(2\alpha))-C\ln a$。
4.  **最小化能量**：为了找到最佳的 $\alpha$ 值，我们对 $E(\alpha)$ 求导并令其为零：
    $\frac{dE}{d\alpha} = \frac{\hbar^2}{m} - \frac{C}{2\alpha} = 0$
    解得最优参数为 $\alpha_{opt} = \frac{mC}{2\hbar^2}$。
5.  **得到最佳能量估计**：将 $\alpha_{opt}$ 代回能量表达式 $E(\alpha)$，得到在该[试探函数](@entry_id:756165)族下的最低能量，即[基态能量](@entry_id:263704)的最佳上限：
    $E_{\min} = \frac{C}{2}\left(1-\gamma-\ln\frac{mC a^2}{\hbar^2}\right)$

这个过程完整地演示了如何通过引入一个灵活的参数并最小化[能量期望值](@entry_id:174035)，来系统地逼近真实的[基态能量](@entry_id:263704)。

#### 里利-里兹方法（[线性变分法](@entry_id:150058)）

对于更复杂的系统，直接找到一个具有良好[解析性](@entry_id:140716)质的[试探函数](@entry_id:756165)并进行最小化是困难的。一个更强大和系统化的方法是**里利-里兹方法 (Rayleigh-Ritz method)**，也称为[线性变分法](@entry_id:150058)。其核心思想是将未知的试探波函数 $|\psi\rangle$ 展开为一组已知的、[线性无关](@entry_id:148207)的**[基函数](@entry_id:170178) (basis functions)** $\{|\phi_i\rangle\}$ 的线性组合：

$|\psi\rangle = \sum_{i=1}^{N} c_i |\phi_i\rangle$

在这个框架下，变分参数不再是函数形式中的[非线性](@entry_id:637147)参数（如上例中的 $\alpha$），而是展开式中的线性系数 $\{c_i\}$。将这个展开式代入里利-里兹商，[能量期望值](@entry_id:174035)就变成了系数 $\{c_i\}$ 的函数。最小化这个[能量期望值](@entry_id:174035)，通过对每个系数 $c_i$ 求偏导并令其为零，最终可以导出一个矩阵形式的**广义本征值问题 (generalized eigenvalue problem)**：

$\mathbf{H}\mathbf{c} = E\mathbf{S}\mathbf{c}$

其中：
-   $\mathbf{c}$ 是由系数 $c_i$ 构成的列向量。
-   $\mathbf{H}$ 是哈密顿矩阵，其[矩阵元](@entry_id:186505)为 $H_{ij} = \langle \phi_i | \hat{H} | \phi_j \rangle$。
-   $\mathbf{S}$ 是交叠矩阵 (overlap matrix)，其矩阵元为 $S_{ij} = \langle \phi_i | \phi_j \rangle$。

如果所选的[基函数](@entry_id:170178) $\{|\phi_i\rangle\}$ 是正交归一的（即 $S_{ij} = \delta_{ij}$），那么交叠矩阵 $\mathbf{S}$ 就是单位矩阵 $\mathbf{I}$，问题简化为标准的**矩阵本征值问题** $\mathbf{H}\mathbf{c} = E\mathbf{c}$。

这个矩阵方程的解会给出一系列[本征值](@entry_id:154894) $E_k$ 和对应的[本征向量](@entry_id:151813) $\mathbf{c}_k$。根据变分原理，其中最低的[本征值](@entry_id:154894) $E_0^{(N)}$ 就是在由这 $N$ 个[基函数](@entry_id:170178)张成的[子空间](@entry_id:150286)中对体系基态能量的最佳近似。同时，其他较高的[本征值](@entry_id:154894) $E_1^{(N)}, E_2^{(N)}, \dots$ 则可以被看作是体系[激发态](@entry_id:261453)能量的近似。

这种方法在计算物理和计算化学中得到了广泛应用。例如，在模拟晶体材料的电子结构时，常采用平面波作为[基函数](@entry_id:170178)。对于一个一维周期性势场 $V(x) = V_0 \cos(2\pi x/a)$ 中的电子，我们可以用一组[平面波基](@entry_id:140187)函数 $\{\phi_n(x) = \frac{1}{\sqrt{a}} e^{ik_nx}\}$ 来展开电子[波函数](@entry_id:147440)。通过计算[哈密顿矩阵元](@entry_id:201928)并[对角化](@entry_id:147016)，就可以得到能带结构。该[哈密顿矩阵](@entry_id:136233)的最低[本征值](@entry_id:154894)即为价带顶（或[导带](@entry_id:159736)底）的能量近似值 [@problem_id:3498139]。

里利-里兹方法的另一个重要应用体现在[量子化学](@entry_id:140193)的[组态相互作用](@entry_id:195713) (Configuration Interaction, CI) 方法中。在给定的单粒子[基函数](@entry_id:170178)（原子轨道）基础上，可以构建多电子的[斯莱特行列式](@entry_id:139034) (Slater determinants)。
-   **[Hartree-Fock](@entry_id:142303) (HF) 方法**可以被视为一种特殊的[变分法](@entry_id:163656)，它将变分空间限制在单个[斯莱特行列式](@entry_id:139034)所构成的[流形](@entry_id:153038)上。
-   **CISD 方法**（包含单重和双重激发）则在一个更大的变分空间中求解，该空间由 HF 参考态以及所有相对于它进行了单、双[电子激发](@entry_id:190531)所产生的[行列式](@entry_id:142978)构成。
-   **[全组态相互作用](@entry_id:172539) (Full CI) 方法**则在由给定单粒子[基函数](@entry_id:170178)所能构建的*所有*可能的[斯莱特行列式](@entry_id:139034)构成的完备空间中求解。

这三个方法所对应的变分空间是逐级嵌套的：$\mathcal{S}_{\text{HF}} \subset \mathcal{S}_{\text{CISD}} \subset \mathcal{S}_{\text{FCI}}$。根据里利-里兹方法的一个重要推论——在更大的[子空间](@entry_id:150286)中进行[能量最小化](@entry_id:147698)，得到的结果必然等于或低于在较小[子空间](@entry_id:150286)中的结果——我们可以立即断定它们计算得到的[基态能量](@entry_id:263704)满足如下排序 [@problem_id:1978296]：

$E_{\text{HF}} \ge E_{\text{CISD}} \ge E_{\text{FCI}}$

这清晰地展示了通过系统性地扩大变分空间，可以逐步地、单调地逼近在给定[基组](@entry_id:160309)下的精确基态能量。

### 高等主题与数学基础

变分原理不仅是求解近似解的实用工具，其本身也蕴含着深刻的物理和数学内容。

#### 驻点与本征态

[变分原理](@entry_id:198028)可以被推广：里利-里兹商 $R_H(\psi)$ 的**驻点 (stationary points)**（即泛函导数为零的点）不仅仅对应[基态](@entry_id:150928)，而是对应[哈密顿算符](@entry_id:144286) $\hat{H}$ 的所有**[本征态](@entry_id:149904)**。[基态](@entry_id:150928)对应于[全局最小值](@entry_id:165977)，而其他[驻点](@entry_id:136617)（如极小值、极大值和[鞍点](@entry_id:142576)）则对应于[激发态](@entry_id:261453)。

一个优美的例子是任意一个[二能级系统](@entry_id:138452)。其[哈密顿量](@entry_id:172864)总可以写成 $H = \epsilon_0 I + \mathbf{b} \cdot \boldsymbol{\sigma}$ 的形式，其中 $\boldsymbol{\sigma}$ 是[泡利矩阵](@entry_id:139493)向量。任意一个归一化态可以用[布洛赫球面](@entry_id:138823)上的点 $(\theta, \phi)$ 来[参数化](@entry_id:272587)。[能量期望值](@entry_id:174035)为 $E(\theta, \phi) = \epsilon_0 + \mathbf{b} \cdot \mathbf{n}(\theta, \phi)$，其中 $\mathbf{n}$ 是[布洛赫球面](@entry_id:138823)上的单位向量。通过寻找这个能量函数的[极值](@entry_id:145933)，可以发现其最大值和最小值分别出现在向量 $\mathbf{n}$ 与 $\mathbf{b}$ 平行和反平行时，得到的结果恰好是[哈密顿量](@entry_id:172864)的两个本征能量 $E_{\pm} = \epsilon_0 \pm |\mathbf{b}|$ [@problem_id:217531]。这表明，变分搜索不仅能找到[基态](@entry_id:150928)，原则上也能找到[激发态](@entry_id:261453)。

#### 能量泛函的[凹性](@entry_id:139843)

[变分原理](@entry_id:198028)的一个精妙应用体现在密度泛函理论 (DFT) 的基础中。DFT 表明，系统的[基态能量](@entry_id:263704)可以被看作是外部势场 $v(\mathbf{r})$ 的一个泛函，记为 $E[v]$。利用变分原理可以证明，这个能量泛函 $E[v]$ 是关于势场 $v(\mathbf{r})$ 的一个**凹泛函 (concave functional)** [@problem_id:209530]。

具体来说，考虑两个不同的外部[势场](@entry_id:143025) $v_1$ 和 $v_2$，以及它们的[线性组合](@entry_id:154743) $v_{\lambda} = \lambda v_1 + (1-\lambda) v_2$，其中 $0  \lambda  1$。对应的[基态能量](@entry_id:263704)分别为 $E_1=E[v_1]$, $E_2=E[v_2]$ 和 $E_\lambda=E[v_\lambda]$。根据[变分原理](@entry_id:198028)，对于任意的归一化[波函数](@entry_id:147440) $|\Psi\rangle$，我们有 $E[v] \le \langle \Psi | H[v] | \Psi \rangle$。让 $|\Psi_\lambda\rangle$ 作为 $v_\lambda$ 对应的真实[基态](@entry_id:150928)[波函数](@entry_id:147440)，那么：

$E_\lambda = \langle \Psi_\lambda | H[v_\lambda] | \Psi_\lambda \rangle = \langle \Psi_\lambda | \lambda H[v_1] + (1-\lambda) H[v_2] | \Psi_\lambda \rangle$
$= \lambda \langle \Psi_\lambda | H[v_1] | \Psi_\lambda \rangle + (1-\lambda) \langle \Psi_\lambda | H[v_2] | \Psi_\lambda \rangle$

由于 $|\Psi_\lambda\rangle$ 对于 $H[v_1]$ 和 $H[v_2]$ 来说只是一个试探波函数，根据[变分原理](@entry_id:198028)，$\langle \Psi_\lambda | H[v_1] | \Psi_\lambda \rangle \ge E_1$ 且 $\langle \Psi_\lambda | H[v_2] | \Psi_\lambda \rangle \ge E_2$。因此，

$E_\lambda \ge \lambda E_1 + (1-\lambda) E_2$

这个不等式正是[凹函数](@entry_id:274100)（或凹泛函）的定义。这一性质对DFT的理论构建至关重要，它保证了能量泛函的良好数学行为。

#### 无穷维空间中的数学严谨性与局限性

虽然变分原理非常强大，但它的应用并非毫无限制。在处理真实的、定义在无穷维希尔伯特空间上的量子系统时，必须仔细考虑其数学基础和潜在的“失效”场景 [@problem_id:2932261]。

1.  **[哈密顿量](@entry_id:172864)的有界性**：变分原理的标准形式是为**有下界 (bounded from below)** 的[哈密顿量](@entry_id:172864)建立的。如果一个[哈密顿量](@entry_id:172864)没有下界，其[能谱](@entry_id:181780)的下确界为 $-\infty$。此时，任何有限的[能量期望值](@entry_id:174035)都 trivially 满足 $\langle E \rangle \ge -\infty$，这使得变分原理失去了提供有意义的能量上限的能力 [@problem_id:1218543]。

2.  **算符定义域**：对于无界算符（如[动能算符](@entry_id:265633)），[哈密顿量](@entry_id:172864) $\hat{H}$ 并非定义在整个[希尔伯特空间](@entry_id:261193) $\mathcal{H}$ 上，而是定义在一个称为其**定义域 (domain)** $D(H)$ 的[稠密子空间](@entry_id:261392)上。因此，里利-里兹商严格来说只对 $D(H)$ 中的非零函数有意义。忽略算符定义域会引发严重的数学问题 [@problem_id:2932261, statement B]。

3.  **[下确界](@entry_id:140118)的获得问题 (Attainment of the Infimum)**：在有限维的里利-里兹方法中，由于单位球面是紧集，能量函数（连续）总能在这个集合上取到其最小值。但在无穷维[希尔伯特空间](@entry_id:261193)中，[单位球](@entry_id:142558)面不再是紧集。这意味着，即使能量的下确界存在，也可能没有任何一个函数能够使其达到这个最小值。
    -   一个典型的例子是**[自由粒子](@entry_id:148748)** ($H = -\Delta$ on $L^2(\mathbb{R}^3)$)。其[能量期望值](@entry_id:174035) $\langle \psi | H | \psi \rangle / \langle \psi | \psi \rangle = \int |\nabla\psi|^2 d^3x / \int |\psi|^2 d^3x \ge 0$。我们可以构造一列能量趋近于 0 的[波函数](@entry_id:147440)（例如，越来越宽的[高斯波包](@entry_id:151158)），所以能量的[下确界](@entry_id:140118)是 0。然而，不存在任何一个非零的、平方可积的函数 $\psi$ 能使能量精确为 0（这要求 $\psi$ 是常数，但在 $\mathbb{R}^3$ 上不可积）。因此，这个[下确界](@entry_id:140118)是无法“达到”的 [@problem_id:2932261, statement E]。
    -   另一个例子是纯[排斥势](@entry_id:185622) $V(x)=C/x$ ($C0$) 中的粒子。该体系的能谱是 $[0, \infty)$ 的[连续谱](@entry_id:155477)，不存在能量小于 0 的束缚态。变分法会找到能谱的[下确界](@entry_id:140118)为 0，但这对应于连续谱的边缘，而非一个可归一化的[基态](@entry_id:150928)[本征函数](@entry_id:154705) [@problem_id:2144193]。

4.  **紧致[预解式](@entry_id:199555)算符**：幸运的是，对于许多物理系统（如原子、分子中的电子，或处于束缚[势阱](@entry_id:151413)中的粒子），其[哈密顿量](@entry_id:172864)具有一个重要的性质，即拥有**紧致[预解式](@entry_id:199555) (compact resolvent)**。对于这类算符，其[能谱](@entry_id:181780)是纯离散的，且任何一个[能量最小化](@entry_id:147698)序列都包含一个强收敛的[子序列](@entry_id:147702)，其极限就是真正的[基态](@entry_id:150928)[波函数](@entry_id:147440)。这从数学上保证了变分法对于寻找这类系统的[基态](@entry_id:150928)是可靠和成功的 [@problem_id:2932261, statement C]。

综上所述，变分原理是量子力学中一个集深刻、优美与实用于一体的强大工具。理解其背后的数学机制和适用边界，对于在理论和计算层面精准地应用它来探索量子世界至关重要。