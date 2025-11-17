## 引言
泡利矩阵是量子力学，特别是自旋理论的数学基石。这组看似简单的 $2 \times 2$ 矩阵，却深刻地描述了电子等基本粒子的[内禀角动量](@entry_id:189727)——这一纯粹的量子现象。然而，对于初学者而言，这些矩阵从何而来，其独特的代数规则背后隐藏着怎样的物理意义，以及它们为何能超越自旋理论，在[量子化学](@entry_id:140193)、凝聚态物理乃至粒子物理中扮演关键角色，这些问题往往构成了一个知识上的缺口。本文旨在填补这一缺口，带领读者系统地掌握泡利矩阵。在接下来的章节中，我们将首先深入“原理与机制”，从基本公理出发推导泡利矩阵，并揭示其核心[代数结构](@entry_id:137052)；随后，在“应用与跨学科联系”一章中，我们将展示这些矩阵如何应用于解决从[自旋进动](@entry_id:149995)到[量子纠缠](@entry_id:136576)等实际物理问题，并探索其在不同学科中的重要作用；最后，通过“动手实践”环节，您将有机会通过解决具体问题来巩固所学知识。

## 原理与机制

继前一章对泡利矩阵在量子力学，特别是自旋理论中核心地位的介绍之后，本章将深入剖析这些矩阵的内在原理与作用机制。我们将从它们的数学定义出发，揭示其深刻的[代数结构](@entry_id:137052)，并最终阐明这些结构如何在[量子动力学](@entry_id:138183)中扮演关键角色。本章旨在为您提供一个系统而严谨的框架，用于理解和应用泡利矩阵来描述和预测双能级量子系统的行为。

### 泡利矩阵的定义与基本性质

为了精确地描述[电子自旋](@entry_id:137016)等双能级系统，我们需要一套具有特定属性的数学工具。泡利矩阵正是为此而生。它们并非任意选取的，而是由一组严格的物理和数学公理唯一确定（在特定[基矢](@entry_id:199546)下）。

#### 从基本公理出发

我们可以从一套最基本的公理出发，推导出泡利矩阵的具体形式。这套公理封装了[自旋算符](@entry_id:155419)所必须满足的物理要求。考虑一组三个 $2 \times 2$ 矩阵，记作 $\sigma_x, \sigma_y, \sigma_z$（或 $\sigma_1, \sigma_2, \sigma_3$），它们必须满足以下条件 [@problem_id:2926174]：

1.  **[厄米性](@entry_id:141899) (Hermiticity)**: 每个矩阵都是厄米矩阵，即 $\sigma_k^\dagger = \sigma_k$。这一条保证了它们所代表的物理可观测量（如自旋分量）的测量结果是实数。

2.  **无迹性 (Tracelessness)**: 每个[矩阵的迹](@entry_id:139694)（对角元素之和）为零，即 $\text{Tr}(\sigma_k) = 0$。

3.  **对合性 (Involutory Property)**: 每个矩阵的平方是 $2 \times 2$ 的[单位矩阵](@entry_id:156724) $\mathbb{I}_2$，即 $\sigma_k^2 = \mathbb{I}_2$。这个性质直接导致它们的[本征值](@entry_id:154894)只能是 $+1$ 或 $-1$。

4.  **[对易关系](@entry_id:136780) (Commutation Relations)**: 它们满足特定的[对易关系](@entry_id:136780) $[\sigma_i, \sigma_j] \equiv \sigma_i\sigma_j - \sigma_j\sigma_i = 2i\varepsilon_{ijk}\sigma_k$。其中 $i$ 是虚数单位，$\varepsilon_{ijk}$ 是[列维-奇维塔符号](@entry_id:193594)。这个关系是[角动量代数](@entry_id:178952)的核心，它表明不同自旋分量是互不相容的[可观测量](@entry_id:267133)。

在量子力学中，我们通常选择一个特定的[基矢](@entry_id:199546)，即沿着某个固定方向（通常定义为 $z$ 轴）的自旋[本征态](@entry_id:149904)构成的[基矢](@entry_id:199546)。这两个[基矢](@entry_id:199546)态分别被称为“自旋向上”($|\uparrow\rangle$) 和“自旋向下”($|\downarrow\rangle$)，它们的矩阵表示为：
$$
|\uparrow\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad |\downarrow\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}
$$
在这个[基矢](@entry_id:199546)下，$\sigma_z$ 算符的作用被定义为 $\sigma_z|\uparrow\rangle = +1 \cdot |\uparrow\rangle$ 和 $\sigma_z|\downarrow\rangle = -1 \cdot |\downarrow\rangle$。这意味着 $|\uparrow\rangle$ 和 $|\downarrow\rangle$ 分别是 $\sigma_z$ 的[本征值](@entry_id:154894)为 $+1$ 和 $-1$ 的本征态。根据这个定义，我们可以立即确定 $\sigma_z$ 的矩阵形式：
$$
\sigma_z = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}
$$
有了 $\sigma_z$ 的显式形式，我们可以利用对易关系和其他公理来确定 $\sigma_x$ 和 $\sigma_y$。例如，考虑对易子 $[\sigma_z, \sigma_x] = 2i\sigma_y$。同时，$\sigma_x$ 和 $\sigma_y$ 必须是厄米且无迹的，这意味着它们的一般形式为 $\begin{pmatrix} a  b \\ b^*  -a \end{pmatrix}$，其中 $a$ 是实数，$b$ 是复数。通过一系列代数推导，可以证明满足所有公理的唯一（除了一个整体的相位因子）解是：
$$
\sigma_x = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}, \quad \sigma_y = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}, \quad \sigma_z = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}
$$
这组矩阵被称为泡利矩阵的**标准表示**，它构成了我们后续讨论的基础 [@problem_id:2926174]。

#### 关键矩阵属性

除了上述定义性公理，泡利矩阵还拥有一系列重要的数学属性。

*   **[厄米性](@entry_id:141899)与[幺正性](@entry_id:138773) (Hermiticity and Unitarity)**: 我们已经要求泡利矩阵是厄米矩阵。一个有趣且重要的推论是，它们同时也是**幺[正矩阵](@entry_id:149490)**。一个矩阵 $U$ 是幺正的，如果 $U^\dagger U = \mathbb{I}$。对于泡利矩阵，$\sigma_k^\dagger = \sigma_k$，所以 $\sigma_k^\dagger \sigma_k = \sigma_k \sigma_k = \sigma_k^2 = \mathbb{I}$。因此，泡利矩阵既是厄米矩阵又是幺[正矩阵](@entry_id:149490)。这是一个非常特殊的性质，在物理学中并不常见（例如，动量和位置算符是厄米的但不是幺正的）。

*   **无迹性 (Tracelessness)**: 通过直接观察，我们确认 $\text{Tr}(\sigma_x) = 0+0=0$, $\text{Tr}(\sigma_y) = 0+0=0$, $\text{Tr}(\sigma_z) = 1-1=0$。无迹性是一个深刻的性质。事实上，单位矩阵 $\mathbb{I}$ 和三个泡利矩阵 $\sigma_x, \sigma_y, \sigma_z$ 构成了一个完备的基，任何 $2 \times 2$ 的厄米矩阵都可以表示为它们的实系数[线性组合](@entry_id:154743)。一个任意的 $2 \times 2$ 厄米矩阵 $M$ 都可以写成 $M = c_0 \mathbb{I} + c_x\sigma_x + c_y\sigma_y + c_z\sigma_z$。如果 $M$ 是无迹的，则 $c_0=0$ [@problem_id:1385864]。

*   **[行列式](@entry_id:142978) (Determinant)**: 我们可以直接计算每个泡利[矩阵的行列式](@entry_id:148198)：
    $$
    \det(\sigma_x) = (0)(0) - (1)(1) = -1
    $$
    $$
    \det(\sigma_y) = (0)(0) - (-i)(i) = -i^2 = -1
    $$
    $$
    \det(\sigma_z) = (1)(-1) - (0)(0) = -1
    $$
    所有三个泡利[矩阵的行列式](@entry_id:148198)都是 $-1$。这与它们的[本征值](@entry_id:154894)为 $\pm 1$ 是一致的，因为矩阵的行列式等于其[本征值](@entry_id:154894)的乘积。对于一个由泡利矩阵[线性组合](@entry_id:154743)构成的更一般的无迹厄米矩阵 $M = a\sigma_x + b\sigma_y + c\sigma_z$（其中 $a,b,c$ 为实数），其矩阵形式为 $M = \begin{pmatrix} c  a-ib \\ a+ib  -c \end{pmatrix}$。它的[行列式](@entry_id:142978)可以计算为 $\det(M) = -c^2 - (a-ib)(a+ib) = -(a^2+b^2+c^2)$ [@problem_id:1385887]。

*   **[本征值与本征向量](@entry_id:748836) (Eigenvalues and Eigenvectors)**: 由于 $\sigma_k^2 = \mathbb{I}$，若 $\sigma_k |v\rangle = \lambda|v\rangle$，则 $\sigma_k^2 |v\rangle = \lambda^2 |v\rangle = \mathbb{I}|v\rangle = |v\rangle$，这意味着 $\lambda^2=1$，所以[本征值](@entry_id:154894)必然是 $\lambda = \pm 1$。
    
    对于每个泡利矩阵，我们都可以找到一组对应的归一化[本征向量](@entry_id:151813)，它们代表了沿着相应坐标轴的自旋确定态：
    *   **z-方向**: 如定义所示，$\sigma_z$ 的[本征态](@entry_id:149904)是标准[基矢](@entry_id:199546)：
        $|z+\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ ([本征值](@entry_id:154894) $+1$) 和 $|z-\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$ ([本征值](@entry_id:154894) $-1$)。
    *   **x-方向**: 求解 $\sigma_x|v\rangle = \lambda|v\rangle$ [@problem_id:1385876]，我们得到[本征态](@entry_id:149904)：
        $|x+\rangle = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix}$ ([本征值](@entry_id:154894) $+1$) 和 $|x-\rangle = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ -1 \end{pmatrix}$ ([本征值](@entry_id:154894) $-1$)。
    *   **y-方向**: 类似地，$\sigma_y$ 的本征态是：
        $|y+\rangle = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ i \end{pmatrix}$ ([本征值](@entry_id:154894) $+1$) 和 $|y-\rangle = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ -i \end{pmatrix}$ ([本征值](@entry_id:154894) $-1$)。
    
    这些本征态在物理上至关重要，因为它们代表了在对相应自旋分量进行测量后，系统可能“塌缩”到的状态。
    
    如果我们考虑一个更一般的算符，例如 $A = c_1 \mathbb{I} + c_2 \sigma_y$，其中 $c_1, c_2$ 是实常数，那么它的[本征值](@entry_id:154894)也很容易找到。因为 $\mathbb{I}$ 和 $\sigma_y$ 是对易的，它们拥有共同的[本征向量](@entry_id:151813)。对于 $\sigma_y$ 的任意[本征向量](@entry_id:151813) $|v\rangle$ ([本征值](@entry_id:154894)为 $\lambda = \pm 1$)，我们有 $A|v\rangle = (c_1 \mathbb{I} + c_2 \sigma_y)|v\rangle = c_1|v\rangle + c_2\lambda|v\rangle = (c_1+c_2\lambda)|v\rangle$。因此，$A$ 的[本征值](@entry_id:154894)为 $c_1+c_2$ 和 $c_1-c_2$ [@problem_id:1385847]。

### 核心代数关系

泡利矩阵的真正威力体现在它们独特的[代数结构](@entry_id:137052)中，这套结构由[对易关系](@entry_id:136780)和[反对易关系](@entry_id:153815)共同定义。

#### 对易与[反对易关系](@entry_id:153815)

如前所述，**对易关系**为：
$$
[\sigma_i, \sigma_j] = 2i\varepsilon_{ijk}\sigma_k
$$
具体展开为：
$$
[\sigma_x, \sigma_y] = 2i\sigma_z, \quad [\sigma_y, \sigma_z] = 2i\sigma_x, \quad [\sigma_z, \sigma_x] = 2i\sigma_y
$$
在量子力学中，两个算符的对易子不为零，意味着它们所对应的物理量不能被同时精确测量。这就是[海森堡不确定性原理](@entry_id:171099)的体现。因此，上述关系式从根本上说明了我们无法同时知道一个电子在x、y、z三个方向上的自旋分量。例如，如果我们测量并确定了电子的z分量自旋（使其处于 $|z+\rangle$ 或 $|z-\rangle$ 态），那么它在x和y方向的自旋就处于不确定状态。这是自旋量子行为的一个核心特征 [@problem_id:1385857]。

与[对易关系](@entry_id:136780)互补的是**[反对易关系](@entry_id:153815)**，定义为 $\{\sigma_i, \sigma_j\} \equiv \sigma_i\sigma_j + \sigma_j\sigma_i$：
$$
\{\sigma_i, \sigma_j\} = 2\delta_{ij}\mathbb{I}
$$
其中 $\delta_{ij}$ 是克罗内克符号。当 $i=j$ 时，这退化为我们已知的 $\sigma_i^2 = \mathbb{I}$。当 $i \neq j$ 时，我们得到 $\{\sigma_i, \sigma_j\} = 0$，即 $\sigma_i\sigma_j = -\sigma_j\sigma_i$。这个性质在计算中非常有用。例如，考虑一个[哈密顿量](@entry_id:172864) $H = c_x\sigma_x + c_y\sigma_y$，计算它的平方 $H^2$ [@problem_id:1385888]：
$$
H^2 = (c_x\sigma_x + c_y\sigma_y)^2 = c_x^2\sigma_x^2 + c_y^2\sigma_y^2 + c_x c_y (\sigma_x\sigma_y + \sigma_y\sigma_x)
$$
利用[反对易关系](@entry_id:153815) $\{\sigma_x, \sigma_y\}=0$ 和 $\sigma_k^2=\mathbb{I}$，上式简化为：
$$
H^2 = c_x^2\mathbb{I} + c_y^2\mathbb{I} + c_x c_y (0) = (c_x^2 + c_y^2)\mathbb{I}
$$
这个结果表明，某些特定形式的[哈密顿量](@entry_id:172864)的平方是一个与空间无关的常数乘以[单位矩阵](@entry_id:156724)，这在求解量子动力学问题时极大地简化了计算 [@problem_id:1385864]。

#### 泡利矢量与[点积](@entry_id:149019)恒等式

我们可以将三个泡利矩阵组合成一个**泡利矢量** $\vec{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$。这个形式上的矢量使得我们可以将上述所有代数关系统一到一个极其优美和强大的恒等式中。对于任意两个与 $\vec{\sigma}$ 对易的普通矢量 $\vec{A}$ 和 $\vec{B}$（即它们的分量是常数或不作用于自旋空间的算符），我们有：
$$
(\vec{\sigma} \cdot \vec{A})(\vec{\sigma} \cdot \vec{B}) = (\vec{A} \cdot \vec{B})\mathbb{I} + i\vec{\sigma} \cdot (\vec{A} \times \vec{B})
$$
这个恒等式 [@problem_id:1181308] 包含了关于泡利矩阵的所有代数信息。我们可以通过选择特定的 $\vec{A}$ 和 $\vec{B}$ 来验证这一点。例如，令 $\vec{A} = \hat{e}_i$ 和 $\vec{B} = \hat{e}_j$，其中 $\hat{e}_i$ 是第 $i$ 个笛卡尔单位矢量。那么 $\vec{\sigma} \cdot \hat{e}_i = \sigma_i$。恒等式左边变为 $\sigma_i \sigma_j$。右边变为：
$$
(\hat{e}_i \cdot \hat{e}_j)\mathbb{I} + i\vec{\sigma} \cdot (\hat{e}_i \times \hat{e}_j) = \delta_{ij}\mathbb{I} + i\vec{\sigma} \cdot (\varepsilon_{ijk}\hat{e}_k) = \delta_{ij}\mathbb{I} + i\varepsilon_{ijk}\sigma_k
$$
于是我们得到了关系式 $\sigma_i \sigma_j = \delta_{ij}\mathbb{I} + i\varepsilon_{ijk}\sigma_k$。由此可以轻松推导出[对易关系](@entry_id:136780)和[反对易关系](@entry_id:153815)：
*   **对易子**: $[\sigma_i, \sigma_j] = \sigma_i\sigma_j - \sigma_j\sigma_i = (\delta_{ij}\mathbb{I} + i\varepsilon_{ijk}\sigma_k) - (\delta_{ji}\mathbb{I} + i\varepsilon_{jik}\sigma_k) = i(\varepsilon_{ijk} - \varepsilon_{jik})\sigma_k = 2i\varepsilon_{ijk}\sigma_k$。
*   **[反对易子](@entry_id:139754)**: $\{\sigma_i, \sigma_j\} = \sigma_i\sigma_j + \sigma_j\sigma_i = (\delta_{ij}\mathbb{I} + i\varepsilon_{ijk}\sigma_k) + (\delta_{ji}\mathbb{I} + i\varepsilon_{jik}\sigma_k) = 2\delta_{ij}\mathbb{I}$。

这个[点积](@entry_id:149019)恒等式是处理涉及泡利矩阵的复杂表达式的有力工具。

### 在量子动力学中的应用

泡利矩阵不仅仅是静态的数学对象，它们是描述自旋[系统动力学](@entry_id:136288)的核心。

#### 自旋[算符与可观测量](@entry_id:262342)

在物理学中，电子的自旋角动量算符 $\vec{S}$ 与泡利矢量 $\vec{\sigma}$ 成正比：
$$
\hat{S}_k = \frac{\hbar}{2}\sigma_k, \quad \text{for } k=x,y,z
$$
其中 $\hbar$ 是[约化普朗克常数](@entry_id:275910)。[总自旋](@entry_id:153335)的平方算符 $\hat{S}^2$ 定义为 $\hat{S}^2 = \hat{S}_x^2 + \hat{S}_y^2 + \hat{S}_z^2$。利用泡利矩阵的性质，我们可以计算出它：
$$
\hat{S}^2 = \left(\frac{\hbar}{2}\right)^2 (\sigma_x^2 + \sigma_y^2 + \sigma_z^2) = \frac{\hbar^2}{4}(\mathbb{I} + \mathbb{I} + \mathbb{I}) = \frac{3}{4}\hbar^2\mathbb{I}
$$
这个结果意义非凡。它表明对于任何自旋1/2的粒子，其总自旋的平方是一个确定值 $\frac{3}{4}\hbar^2$（即[量子数](@entry_id:145558) $s=1/2$ 时的 $s(s+1)\hbar^2$），并且该算符只是[单位矩阵](@entry_id:156724)的一个倍数。由于[单位矩阵](@entry_id:156724)与任何算符都对易，我们有 $[\hat{S}^2, \hat{S}_k] = 0$ 对任何 $k$ 都成立。

这让我们能够精确回答哪些自旋观测量可以被同时测量 [@problem_id:1385857]。由于 $[\hat{S}^2, \hat{S}_z] = 0$，[总自旋](@entry_id:153335)平方 $\hat{S}^2$ 和z分量自旋 $\hat{S}_z$ 是相容的[可观测量](@entry_id:267133)，可以同时确定。然而，由于 $[\hat{S}_x, \hat{S}_y] = i\hbar\hat{S}_z \neq 0$，x和y分量自旋则不能同时确定。因此，诸如 $\{\hat{S}^2, \hat{S}_z\}$ 这样的集合代表了可以同时测量的物理量，而 $\{\hat{S}_x, \hat{S}_y, \hat{S}_z\}$ 则不行。

#### 矩阵指数与时间演化

量子系统的状态随时间的演化由薛定谔方程决定，其形式解由[时间演化算符](@entry_id:196774) $\hat{U}(t) = \exp(-i\hat{H}t/\hbar)$ 给出，其中 $\hat{H}$ 是系统的[哈密顿量](@entry_id:172864)。当[哈密顿量](@entry_id:172864)涉及自旋时，通常会包含泡利矩阵，这时我们就需要计算泡利矩阵的指数。

考虑一个常见的[哈密顿量](@entry_id:172864)形式 $\hat{H} \propto \vec{n} \cdot \vec{\sigma}$，其中 $\vec{n}$ 是一个实单位矢量。设 $\hat{H} = \alpha (\vec{n} \cdot \vec{\sigma})$。利用[点积](@entry_id:149019)恒等式，我们知道 $(\vec{n} \cdot \vec{\sigma})^2 = (\vec{n} \cdot \vec{n})\mathbb{I} = \mathbb{I}$。这个性质使得矩阵指数的计算大大简化。我们可以利用[泰勒级数展开](@entry_id:138468) $\exp(X) = \sum_{k=0}^\infty X^k/k!$：
$$
\exp(-i\theta(\vec{n} \cdot \vec{\sigma})) = \sum_{k=0}^{\infty} \frac{(-i\theta)^k}{k!} (\vec{n} \cdot \vec{\sigma})^k
$$
将级数分为偶数项和奇数项，并利用 $(\vec{n} \cdot \vec{\sigma})^{2m} = \mathbb{I}$ 和 $(\vec{n} \cdot \vec{\sigma})^{2m+1} = \vec{n} \cdot \vec{\sigma}$，我们得到：
$$
\exp(-i\theta(\vec{n} \cdot \vec{\sigma})) = \left( \sum_{m=0}^{\infty} \frac{(-1)^m \theta^{2m}}{(2m)!} \right)\mathbb{I} - i\left( \sum_{m=0}^{\infty} \frac{(-1)^m \theta^{2m+1}}{(2m+1)!} \right)(\vec{n} \cdot \vec{\sigma})
$$
括号中的级数正是 $\cos(\theta)$ 和 $\sin(\theta)$ 的[泰勒展开](@entry_id:145057)。于是我们得到了一个极其重要的公式，类似于欧拉公式：
$$
\exp(-i\theta(\vec{n} \cdot \vec{\sigma})) = \cos(\theta)\mathbb{I} - i\sin(\theta)(\vec{n} \cdot \vec{\sigma})
$$
这个公式是处理双能级系统[时间演化](@entry_id:153943)的关键 [@problem_id:1385890] [@problem_id:1181308]。

**应用实例：[拉莫尔进动](@entry_id:143131)**
考虑一个处于沿z轴方向的均匀[磁场](@entry_id:153296) $B_0$ 中的电子，其[哈密顿量](@entry_id:172864)为 $\hat{H} = \omega_0 \hat{S}_z = \frac{\hbar\omega_0}{2}\sigma_z$，其中 $\omega_0$ 是[拉莫尔频率](@entry_id:149912)。假设在 $t=0$ 时刻，系统被制备在x方向自旋向上的状态 $|\psi(0)\rangle = |x+\rangle = \frac{1}{\sqrt{2}}(|z+\rangle + |z-\rangle)$ [@problem_id:1385831]。

[时间演化算符](@entry_id:196774)为 $\hat{U}(t) = \exp(-i\hat{H}t/\hbar) = \exp(-i\frac{\omega_0 t}{2}\sigma_z)$。利用上述[指数公式](@entry_id:270327)（这里 $\vec{n}=\hat{e}_z, \theta=\omega_0 t/2$），我们有：
$$
\hat{U}(t) = \cos(\frac{\omega_0 t}{2})\mathbb{I} - i\sin(\frac{\omega_0 t}{2})\sigma_z = \begin{pmatrix} \exp(-i\omega_0t/2)  0 \\ 0  \exp(i\omega_0t/2) \end{pmatrix}
$$
演化后的状态为：
$$
|\psi(t)\rangle = \hat{U}(t)|\psi(0)\rangle = \frac{1}{\sqrt{2}} \begin{pmatrix} \exp(-i\omega_0t/2) \\ \exp(i\omega_0t/2) \end{pmatrix}
$$
现在我们可以计算任意时刻y方向自旋分量的[期望值](@entry_id:153208) $\langle \hat{S}_y(t) \rangle$：
$$
\langle \hat{S}_y(t) \rangle = \langle\psi(t)|\frac{\hbar}{2}\sigma_y|\psi(t)\rangle = \frac{\hbar}{2} \cdot \frac{1}{2} \begin{pmatrix} \exp(i\omega_0t/2)  \exp(-i\omega_0t/2) \end{pmatrix} \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix} \begin{pmatrix} \exp(-i\omega_0t/2) \\ \exp(i\omega_0t/2) \end{pmatrix}
$$
计算矩阵乘法得到：
$$
\langle \hat{S}_y(t) \rangle = \frac{\hbar}{4} [i\exp(-i\omega_0t) - i\exp(i\omega_0t)] = \frac{\hbar}{2} \frac{\exp(i\omega_0t) - \exp(-i\omega_0t)}{2i} = \frac{\hbar}{2}\sin(\omega_0t)
$$
类似地，可以算出 $\langle \hat{S}_x(t) \rangle = \frac{\hbar}{2}\cos(\omega_0t)$ 和 $\langle \hat{S}_z(t) \rangle = 0$。这组结果清晰地描绘了一幅物理图像：初始指向x轴的自旋矢量，在z-y平面上绕着z轴（[磁场](@entry_id:153296)方向）以角频率 $\omega_0$ 进行圆周运动（进动）。这正是[泡利矩阵代数](@entry_id:265878)在描述真实物理现象中的威力体现。