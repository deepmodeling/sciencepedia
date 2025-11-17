## 引言
[线性三原子分子](@entry_id:174604)，如二氧化碳（$\text{CO}_2$）或硫化羰（OCS），是自然界中最基本的[分子结构](@entry_id:140109)之一。理解其内部运动，特别是原子间的[振动](@entry_id:267781)，对于从[化学反应动力学](@entry_id:274455)到[材料科学](@entry_id:152226)的诸多领域都至关重要。然而，即使是这样一个看似简单的系统，其内部动力学也隐藏着复杂性：三个原子通过[化学键](@entry_id:138216)“弹簧”相互连接，形成一个耦合[振动](@entry_id:267781)系统。单个原子的运动会不可避免地影响其他原子，这使得直接求解它们的运动变得异常困难。我们如何才能解耦这种复杂的相互作用，并以一种清晰、系统的方式来描述分子的整体[振动](@entry_id:267781)行为呢？

本文旨在通过[分析力学](@entry_id:166738)中的强大工具——[简正模分析](@entry_id:176817)，来深入剖析这一问题。我们将把这个多体问题转化为一组独立的、易于理解的简谐[振动](@entry_id:267781)模式，从而揭示系统内在的动力学结构。通过本文的学习，您将不仅掌握一种重要的物理分析方法，还能体会到基础理论模型在解释真实世界现象中的巨大威力。

文章将分为三个核心部分。在“**原理与机制**”一章中，我们将从[牛顿定律](@entry_id:163541)出发，建立系统的[运动方程](@entry_id:170720)，并引入矩阵形式和广义本征值问题，系统地推导出[简正频率](@entry_id:276390)和[振动](@entry_id:267781)模式的求解方法。接着，在“**应用与跨学科联系**”一章，我们将把这一理论模型应用于[分子光谱学](@entry_id:148164)、凝聚态物理等实际场景，探讨[同位素效应](@entry_id:164159)、共振现象以及外部扰动对系统行为的影响，展示其广泛的解释力。最后，“**动手实践**”部分提供了一系列精心设计的问题，引导您亲手应用所学知识，将理论转化为解决具体物理问题的能力。让我们从建立这个系统的力学模型开始，踏上探索分子振动奥秘的旅程。

## 原理与机制

在本章中，我们将深入探讨[线性三原子分子](@entry_id:174604)[纵向振动](@entry_id:176640)的核心物理原理和数学处理机制。我们将从建立系统的[运动方程](@entry_id:170720)入手，发展到[简正模分析](@entry_id:176817)这一强大的工具，并最终应用这些概念来解决具体的物理情境。

### 运动方程的建立

研究任何力学系统的第一步是准确描述其运动。我们考虑一个由三个[质点](@entry_id:186768)构成的通用[线性分子](@entry_id:166760)模型，三个质点的质量分别为 $m_1$、$m_2$ 和 $m_3$，沿一条直线[排列](@entry_id:136432)。它们之间通过两个理想化的无质量弹簧连接，弹簧系数分别为 $k_1$（连接 $m_1$ 和 $m_2$）和 $k_2$（连接 $m_2$ 和 $m_3$）。系统被限制在一维空间内运动。

我们用 $x_1(t)$、$x_2(t)$、$x_3(t)$ 分别表示三个质点偏离其平衡位置的位移。根据[胡克定律](@entry_id:149682)和牛顿第二定律，我们可以写出每个质点的[运动方程](@entry_id:170720)：

对于质量为 $m_1$ 的[质点](@entry_id:186768)，它只受到弹簧 $k_1$ 的作用力：
$$m_1 \ddot{x}_1 = -k_1(x_1 - x_2)$$

对于质量为 $m_2$ 的[质点](@entry_id:186768)，它同时受到两个弹簧的作用力：
$$m_2 \ddot{x}_2 = -k_1(x_2 - x_1) - k_2(x_2 - x_3)$$

对于质量为 $m_3$ 的质点，它只受到弹簧 $k_2$ 的作用力：
$$m_3 \ddot{x}_3 = -k_2(x_3 - x_2)$$

这些方程构成了一个[线性常微分方程组](@entry_id:163837)，清晰地展示了三个[质点](@entry_id:186768)运动的耦合特性——一个[质点](@entry_id:186768)的运动会通过弹簧影响其他质点。为了更系统地分析这类耦合[振动](@entry_id:267781)系统，我们通常采用矩阵形式。将上述[方程组](@entry_id:193238)整理后，可以写成如下的二阶矩阵[微分方程](@entry_id:264184)：

$$\mathbf{M}\ddot{\mathbf{x}} + \mathbf{K}\mathbf{x} = \mathbf{0}$$

其中，$\mathbf{x} = \begin{pmatrix} x_1 \\ x_2 \\ x_3 \end{pmatrix}$ 是位移列向量。$\mathbf{M}$ 是[质量矩阵](@entry_id:177093)，它是一个对角矩阵，对角线元素为各个[质点](@entry_id:186768)的质量：

$$\mathbf{M} = \begin{pmatrix} m_1 & 0 & 0 \\ 0 & m_2 & 0 \\ 0 & 0 & m_3 \end{pmatrix}$$

$\mathbf{K}$ 是刚度矩阵（或称劲度矩阵），它描述了系统内部的恢复力特性。通过整理[运动方程](@entry_id:170720)中与位移 $x_1, x_2, x_3$ 相关的项，我们可以得到刚度矩阵 [@problem_id:2033717]：

$$\mathbf{K} = \begin{pmatrix} k_1 & -k_1 & 0 \\ -k_1 & k_1+k_2 & -k_2 \\ 0 & -k_2 & k_2 \end{pmatrix}$$

这个矩阵是对称的 ($K_{ij} = K_{ji}$)，这是[保守力](@entry_id:170586)系统的普遍特征，源于系统的势能可以表示为位移的二次型 $U = \frac{1}{2}\mathbf{x}^T \mathbf{K} \mathbf{x}$。

### [简正模分析](@entry_id:176817)方法

求解耦合的[运动方程](@entry_id:170720) $\mathbf{M}\ddot{\mathbf{x}} + \mathbf{K}\mathbf{x} = \mathbf{0}$ 的关键在于寻找系统的**[简正模](@entry_id:139640)**（normal modes）。一个简正模是系统的一种特殊的[集体运动](@entry_id:747472)模式，其中所有粒子都以相同的频率和固定的相位关系作简谐[振动](@entry_id:267781)。

我们假设系统存在简谐[振动](@entry_id:267781)解，其形式为：
$$\mathbf{x}(t) = \mathbf{a} e^{i\omega t}$$

其中，$\mathbf{a} = \begin{pmatrix} a_1 \\ a_2 \\ a_3 \end{pmatrix}$ 是一个与时间无关的振幅向量，它定义了简正模的“形状”，即各个质点[振动](@entry_id:267781)的相对振幅和相位。$\omega$ 是[简正模](@entry_id:139640)的[角频率](@entry_id:261565)。将该假设解代入运动方程，我们得到 $\ddot{\mathbf{x}}(t) = -\omega^2 \mathbf{a} e^{i\omega t} = -\omega^2 \mathbf{x}(t)$。于是，矩阵[微分方程](@entry_id:264184)转化为一个[代数方程](@entry_id:272665)：

$$-\omega^2 \mathbf{M} \mathbf{a} + \mathbf{K} \mathbf{a} = 0$$
即
$$(\mathbf{K} - \omega^2 \mathbf{M})\mathbf{a} = 0$$

这是一个广义本征值问题。对于非零的振幅向量 $\mathbf{a}$（即系统在运动），上述方程有解的充要条件是其系数[矩阵的[行列](@entry_id:148198)式](@entry_id:142978)为零：

$$\det(\mathbf{K} - \omega^2 \mathbf{M}) = 0$$

这个方程被称为**[特征方程](@entry_id:265849)**。它是一个关于 $\lambda = \omega^2$ 的多项式方程。对于一个有 $N$ 个自由度的系统，这个方程将是 $\lambda$ 的 $N$ 次方程，其根 $\lambda_i = \omega_i^2$ 给出了系统所有可能的[简正模频率](@entry_id:169246)的平方。对于每个[本征值](@entry_id:154894) $\omega_i^2$，我们都可以解出相应的[本征向量](@entry_id:151813) $\mathbf{a}_i$，它描述了该频率对应的[简正模](@entry_id:139640)的运动形态。

### [简正频率](@entry_id:276390)的普适性质

在直接求解[特征方程](@entry_id:265849)之前，我们可以通过分析其结构来揭示一些关于[简正频率](@entry_id:276390)的普适性质。

#### [零频模式](@entry_id:166697)：刚性平动

对于一个孤立的、不受外力作用的分子系统，[总动量](@entry_id:173071)是守恒的。这意味着整个分子可以作为一个刚体在空间中平移，而系统内部的弹簧不会产生恢复力。这种运动模式对应于一个频率为零的[简正模](@entry_id:139640)。

从数学上看，我们可以检验当所有质点发生相同的位移时，即 $\mathbf{a} = \begin{pmatrix} 1 & 1 & 1 \end{pmatrix}^T$ 时，恢复力 $\mathbf{K}\mathbf{a}$ 是多少。由于刚度矩阵 $\mathbf{K}$ 的每一行元素之和均为零（例如，第一行 $k_1 - k_1 + 0 = 0$），我们总是有 $\mathbf{K} \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix} = \mathbf{0}$。将此代入[本征值方程](@entry_id:192306) $(\mathbf{K} - \omega^2 \mathbf{M})\mathbf{a} = 0$，得到：

$$\mathbf{0} - \omega^2 \mathbf{M} \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix} = \mathbf{0}$$

由于质量矩阵 $\mathbf{M}$ 和向量 $\mathbf{a}$ 都不是零，唯一的解就是 $\omega^2 = 0$。因此，任何自由的线性[多原子分子](@entry_id:268323)都必然存在一个零频[简正模](@entry_id:139640)，它物理上对应于整个系统的刚性平动 [@problem_id:2033751]。

#### [振动](@entry_id:267781)模式频率的关系

对于我们的[三原子分子](@entry_id:155569)系统（$N=3$），特征方程是关于 $\lambda=\omega^2$ 的三次方程。由于我们已经知道 $\lambda_0 = 0$ 是一个根，我们可以将[特征多项式](@entry_id:150909)写作 $P(\lambda) = C \lambda (\lambda - \lambda_1)(\lambda - \lambda_2)$，其中 $\lambda_1 = \omega_1^2$ 和 $\lambda_2 = \omega_2^2$ 是两个非零[振动](@entry_id:267781)模式的频率平方。

利用[韦达定理](@entry_id:150627)（Vieta's formulas），[多项式的根](@entry_id:154615)与系数之间存在确定关系。特征多项式为 $P(\lambda) = \det(\mathbf{K} - \lambda \mathbf{M})$。展开这个[行列式](@entry_id:142978)会非常繁琐，但我们可以只关注其低次项。$\lambda$ 的一次项系数由多项式 $P(\lambda)$ 在 $\lambda=0$ 处的[一阶导数](@entry_id:749425)决定，也等于 $-C(\lambda_1 + \lambda_2) + C\lambda_1\lambda_2$ 中的常数项 $C\lambda_1\lambda_2$。通过仔细计算[行列式](@entry_id:142978)展开后 $\lambda$ 的系数，可以得到一个优美的结果 [@problem_id:2033734]：

$$(\omega_1 \omega_2)^2 = \lambda_1 \lambda_2 = \frac{k_1 k_2 (m_1 + m_2 + m_3)}{m_1 m_2 m_3}$$

这个公式揭示了两个[振动频率](@entry_id:199185)的乘积如何依赖于系统的所有质量和弹簧常数，而无需单独求解每个频率。它体现了系统作为一个整体的内在属性。

### 对称[三原子分子](@entry_id:155569)：对称性的应用

现在，我们转向一个重要的特例：对称的[线性三原子分子](@entry_id:174604)，例如二氧化碳（$\text{CO}_2$）的模型。在这种情况下，两个外侧原子的质量相等，即 $m_1 = m_3 = m$，中心原子的质量为 $M$。两个弹簧也相同，即 $k_1 = k_2 = k$。

系统的对称性极大地简化了简正模的求解。根据群论，对于具有对称性的系统，其[简正模](@entry_id:139640)必须遵从该对称性，表现为对称或反对称的运动模式。

#### 反[对称伸缩](@entry_id:165187)[振动](@entry_id:267781)

反对称模式是指分子围绕其中心（即质量为 $M$ 的原子）表现出反对称的运动。这意味着两个外侧原子 $m$ 做等幅反相运动，而中心原子 $M$ 保持静止。即：
$$x_1(t) = -x_3(t) \quad \text{且} \quad x_2(t) = 0$$

将这个运动 ansatz 代入第一个质点的[运动方程](@entry_id:170720) $m\ddot{x}_1 = -k(x_1 - x_2)$：
$$m\ddot{x}_1 = -k(x_1 - 0) = -kx_1$$

这是一个标准的简谐[振动](@entry_id:267781)方程 $\ddot{x}_1 + (k/m)x_1 = 0$。因此，反[对称伸缩](@entry_id:165187)[振动](@entry_id:267781)模式的频率平方为：
$$\omega_A^2 = \frac{k}{m}$$

我们可以验证这个解的[自洽性](@entry_id:160889)：中心原子 $M$ 的运动方程为 $M\ddot{x}_2 = -k(2x_2 - x_1 - x_3)$。代入 $x_2=0$ 和 $x_1=-x_3$，右侧变为 $-k(0 - x_1 - (-x_1)) = 0$，这与左侧 $M\ddot{x}_2=0$ [完美匹配](@entry_id:273916)。这个模式通常被称为**反对称伸缩[振动](@entry_id:267781)**（antisymmetric stretch）。

#### 对称伸缩[振动](@entry_id:267781)

对称模式是指分子围绕其中心表现出对称的运动。这意味着两个外侧原子 $m$ 做等幅同相运动，即 $x_1(t) = x_3(t)$。由于没有外力，系统的质心必须保持静止（或匀速直线运动）。对于[振动](@entry_id:267781)而言，我们要求[质心](@entry_id:265015)在[平衡位置](@entry_id:272392)不动。质心的位移 $X_{CM}$ 为：
$$X_{CM} = \frac{mx_1 + Mx_2 + mx_3}{m+M+m} = \frac{m x_1 + M x_2 + m x_1}{2m+M} = \frac{2mx_1 + Mx_2}{2m+M}$$

令 $X_{CM} = 0$，我们得到中心原子和外侧原子的振幅关系：
$$2mx_1 + Mx_2 = 0 \implies x_2 = -\frac{2m}{M}x_1$$

这表明中心原子与外侧原子做反相[振动](@entry_id:267781)，振幅比为 $2m/M$。现在，我们将这个关系代入第一个[质点](@entry_id:186768)的运动方程：
$$m\ddot{x}_1 = -k(x_1 - x_2) = -k\left(x_1 - \left(-\frac{2m}{M}x_1\right)\right) = -k\left(1 + \frac{2m}{M}\right)x_1$$

这同样是一个简谐[振动](@entry_id:267781)方程，其频率平方为：
$$\omega_S^2 = \frac{k}{m}\left(1 + \frac{2m}{M}\right) = \frac{k(M+2m)}{mM}$$

这个模式被称为**[对称伸缩](@entry_id:165187)[振动](@entry_id:267781)**（symmetric stretch）。

#### [频率比](@entry_id:202730)

我们已经找到了两个非零的[振动频率](@entry_id:199185)。通常情况下，$1 + 2m/M > 1$，因此对称伸缩[振动](@entry_id:267781)的频率 $\omega_S$ 高于反对称伸缩[振动](@entry_id:267781)的频率 $\omega_A$。这两个频率的比值是一个只依赖于质量比的无量纲常数 [@problem_id:2033769] [@problem_id:2033767] [@problem_id:2033770]：

$$\frac{\omega_S}{\omega_A} = \sqrt{\frac{\omega_S^2}{\omega_A^2}} = \sqrt{\frac{\frac{k(M+2m)}{mM}}{\frac{k}{m}}} = \sqrt{\frac{M+2m}{M}} = \sqrt{1+\frac{2m}{M}}$$

这个结果在[光谱学](@entry_id:141940)中非常重要，因为它直接关联到[分子结构](@entry_id:140109)（原子质量）和其可测量的[振动光谱](@entry_id:176233)。

### 叠加原理与[初值问题](@entry_id:144620)

[简正模](@entry_id:139640)之所以强大，是因为它们构成了系统所有可能运动的一组[完备基](@entry_id:143908)。根据**叠加原理**，系统任何复杂的纵向运动都可以表示为这三个简正模（一个平动模，两个[振动](@entry_id:267781)模）的线性叠加：
$$\mathbf{x}(t) = C_0 \mathbf{a}_0 (v_0 t + d_0) + C_A \mathbf{a}_A \cos(\omega_A t + \phi_A) + C_S \mathbf{a}_S \cos(\omega_S t + \phi_S)$$

其中 $C_i$ 和 $\phi_i$ 是由[初始条件](@entry_id:152863)（初始位移和初始速度）决定的振幅和相位。

#### 实例一：初始位移

考虑这样一个初值问题：在 $t=0$ 时，左侧原子被拉开位移 $-A$，而其他两个原子处于[平衡位置](@entry_id:272392)，整个系统从静止释放 [@problem_id:2033712]。
[初始条件](@entry_id:152863)为: $\mathbf{x}(0) = \begin{pmatrix} -A \\ 0 \\ 0 \end{pmatrix}$，$\dot{\mathbf{x}}(0) = \mathbf{0}$。

由于系统从静止释放，所有[简正模](@entry_id:139640)的初速度都为零，因此相位 $\phi_i$ 均为零（或 $\pi$），解可以写成余弦和的形式。我们需要将初始位移向量 $\mathbf{x}(0)$ 分解到三个[简正模](@entry_id:139640)的[本征向量](@entry_id:151813)上：
$$\mathbf{x}(0) = c_0 \mathbf{a}_0 + c_A \mathbf{a}_A + c_S \mathbf{a}_S$$

[简正模](@entry_id:139640)的（未归一化）[本征向量](@entry_id:151813)为：
$$\mathbf{a}_0 = \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix} \text{ (平动)}$$
$$\mathbf{a}_A = \begin{pmatrix} 1 \\ 0 \\ -1 \end{pmatrix} \text{ (反对称)}$$
$$\mathbf{a}_S = \begin{pmatrix} 1 \\ -2m/M \\ 1 \end{pmatrix} \text{ (对称)}$$

代入[初始条件](@entry_id:152863)向量：
$$\begin{pmatrix} -A \\ 0 \\ 0 \end{pmatrix} = c_0 \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix} + c_A \begin{pmatrix} 1 \\ 0 \\ -1 \end{pmatrix} + c_S \begin{pmatrix} 1 \\ -2m/M \\ 1 \end{pmatrix}$$

这是一个三元线性方程组。求解可得系数：
$$c_0 = -\frac{Am}{M+2m}, \quad c_A = -\frac{A}{2}, \quad c_S = -\frac{AM}{2(M+2m)}$$

中心原子的位移 $x_2(t)$ 只与包含 $x_2$ 分量的[简正模](@entry_id:139640)有关，即[平动](@entry_id:187700)模和对称模。注意[平动](@entry_id:187700)模对应一个恒定的位移偏移，因为初速度为零：
$$x_2(t) = c_0 \cdot 1 + c_S \cdot \left(-\frac{2m}{M}\right) \cos(\omega_S t)$$
$$x_2(t) = -\frac{Am}{M+2m} + \left(-\frac{AM}{2(M+2m)}\right) \left(-\frac{2m}{M}\right) \cos(\omega_S t)$$
$$x_2(t) = -\frac{Am}{M+2m} + \frac{Am}{M+2m} \cos(\omega_S t)$$
$$x_2(t) = \frac{Am}{M+2m} \left( \cos(\omega_S t) - 1 \right)$$

这个结果表明，中心原子将围绕一个新的[平衡位置](@entry_id:272392) $-\frac{Am}{M+2m}$ 进行频率为 $\omega_S$ 的[振动](@entry_id:267781)。这个新的[平衡位置](@entry_id:272392)的偏移，正是由于初始位移导致整个系统[质心](@entry_id:265015)发生了移动。

#### 实例二：初始冲量

现在考虑一个不同的[初始条件](@entry_id:152863)：系统初始静止于[平衡位置](@entry_id:272392)，在 $t=0$ 时刻，中心原子 $M$ 受到一个沿轴向的冲量 $P$ [@problem_id:2033780]。
[初始条件](@entry_id:152863)为: $\mathbf{x}(0) = \mathbf{0}$，$\dot{x}_1(0)=0, \dot{x}_2(0)=P/M, \dot{x}_3(0)=0$。

系统的总动量为 $P$，因此质心将以速度 $V_{CM} = P/(2m+M)$ 运动。为了研究内部[振动](@entry_id:267781)，我们转换到[质心参考系](@entry_id:158134)。在[质心系](@entry_id:168444)中，初始速度为：
$$\dot{x}'_1(0) = 0 - V_{CM} = -\frac{P}{2m+M}$$
$$\dot{x}'_2(0) = \frac{P}{M} - V_{CM} = \frac{2mP}{M(2m+M)}$$
$$\dot{x}'_3(0) = 0 - V_{CM} = -\frac{P}{2m+M}$$

由于 $\mathbf{x}'(0)=0$，系统的[振动](@entry_id:267781)解将是正弦函数的形式 $\mathbf{x}'(t) = \sum_i \mathbf{a}_i d_i \sin(\omega_i t)$。初始速度为 $\dot{\mathbf{x}}'(0) = \sum_i \mathbf{a}_i d_i \omega_i$。为了求解振幅 $d_i$，我们需要将初始速度向量 $\dot{\mathbf{x}}'(0)$ 投影到各个[简正模](@entry_id:139640)上。一个关键的性质是简正模的**[M-正交性](@entry_id:178008)**（我们将在下一节讨论），它允许我们独立地计算每个模式的贡献。

我们可以直接观察 $\dot{\mathbf{x}}'(0)$ 的对称性。注意到 $\dot{x}'_1(0) = \dot{x}'_3(0)$，这是一个对称的初始速度[分布](@entry_id:182848)。因此，它不能激发任何反对称的运动模式。反对称模式要求 $x_1 = -x_3$，从而 $\dot{x}_1 = -\dot{x}_3$，这与我们的初始条件不符。因此，只有对称伸缩[振动](@entry_id:267781)模式被激发。

这意味着内部运动完全由对称模式描述。外侧原子的运动振幅可以通过求解对称模式的振幅来确定。通过更正式的投影计算，可以得到外侧原子在[质心系](@entry_id:168444)中的振幅为：
$$A_m = P\left(\frac{mM}{k(2m+M)^{3}}\right)^{\frac{1}{2}}$$

这个例子突显了[简正模分析](@entry_id:176817)的一个重要应用：它可以预测在特定的外部激励下，哪些[振动](@entry_id:267781)模式会被激发，以及激发的程度。

### 简正模的形式理论

最后，我们简要介绍一些支撑[简正模分析](@entry_id:176817)的形式化概念。

#### 广义质量与[M-正交性](@entry_id:178008)

对于一个给定的[简正模](@entry_id:139640)，其振幅向量为 $\mathbf{a}_i$，我们可以定义其**广义质量** $\mu_i$：
$$\mu_i = \mathbf{a}_i^T \mathbf{M} \mathbf{a}_i$$

这个量可以被看作是该[简正模](@entry_id:139640)运动时的“有效惯性”。例如，对于[对称伸缩](@entry_id:165187)[振动](@entry_id:267781)模式，其[本征向量](@entry_id:151813)可取为 $\mathbf{a}_S = \begin{pmatrix} 1 & -2m/M & 1 \end{pmatrix}^T$。其广义质量为 [@problem_id:2033771]：

$$\mu_S = \begin{pmatrix} 1 & -2m/M & 1 \end{pmatrix} \begin{pmatrix} m & 0 & 0 \\ 0 & M & 0 \\ 0 & 0 & m \end{pmatrix} \begin{pmatrix} 1 \\ -2m/M \\ 1 \end{pmatrix}$$
$$\mu_S = \begin{pmatrix} 1 & -2m/M & 1 \end{pmatrix} \begin{pmatrix} m \\ -2m \\ m \end{pmatrix} = m + \left(-\frac{2m}{M}\right)(-2m) + m = 2m + \frac{4m^2}{M}$$

广义[本征值问题](@entry_id:142153)的一个基本定理是，对应于不同本征频率的[本征向量](@entry_id:151813)关于[质量矩阵](@entry_id:177093) $\mathbf{M}$ 是正交的，这被称为 **[M-正交性](@entry_id:178008)**:

$$\mathbf{a}_i^T \mathbf{M} \mathbf{a}_j = 0 \quad (\text{if } \omega_i^2 \neq \omega_j^2)$$

同时，它们也关于[刚度矩阵](@entry_id:178659) $\mathbf{K}$ 正交：

$$\mathbf{a}_i^T \mathbf{K} \mathbf{a}_j = 0 \quad (\text{if } \omega_i^2 \neq \omega_j^2)$$

我们可以验证对称与反对称模式之间的[M-正交性](@entry_id:178008)。$\mathbf{a}_A = \begin{pmatrix} 1 & 0 & -1 \end{pmatrix}^T$：

$$\mathbf{a}_A^T \mathbf{M} \mathbf{a}_S = \begin{pmatrix} 1 & 0 & -1 \end{pmatrix} \begin{pmatrix} m & 0 & 0 \\ 0 & M & 0 \\ 0 & 0 & m \end{pmatrix} \begin{pmatrix} 1 \\ -2m/M \\ 1 \end{pmatrix}$$
$$= \begin{pmatrix} m & 0 & -m \end{pmatrix} \begin{pmatrix} 1 \\ -2m/M \\ 1 \end{pmatrix} = m \cdot 1 + 0 \cdot (-2m/M) + (-m) \cdot 1 = m - m = 0$$

正交性是[简正模分析](@entry_id:176817)的核心，它保证了我们可以将复杂的运动唯一地分解为一系列独立的简谐[振动](@entry_id:267781)之和，极大地简化了多自由度系统的动力学分析。