## 引言
[量子傅里叶变换](@entry_id:139146)（Quantum Fourier Transform, QFT）是[量子计算](@entry_id:142712)领域中最强大、最核心的工具之一，是Shor的因子分解算法和许多其他[量子算法](@entry_id:147346)成功的基石。然而，要真正驾驭QFT的力量，仅仅将其视为一个黑箱算符是远远不够的。其深刻的威力根植于抽象代数，特别是[有限循环群](@entry_id:147298)的[表示论](@entry_id:137998)之中。本文旨在揭开QFT的数学面纱，系统地展示其从[群表示论](@entry_id:141930)到实际物理和计算应用的完整图景。

本文将带领读者踏上一段从抽象理论到具体应用的探索之旅，分为三个核心部分：

在第一章 **“原理与机制”** 中，我们将从[循环群](@entry_id:138668) $\mathbb{Z}_N$ 的[表示论](@entry_id:137998)出发，建立QFT的理论基础。您将学习到QFT如何作为一种[基变换](@entry_id:189626)，[对角化](@entry_id:147016)与系统对称性相关的算符，并探索其谱性质、与[宇称算符](@entry_id:148434)的关系，以及它如何通过中国剩余定理与数论结构紧密相连。

随后的第二章 **“应用与[交叉](@entry_id:147634)学科联系”** 将展示这些基础原理的强大威力。我们将探讨QFT如何在[量子相位估计](@entry_id:136538)、隐藏[子群](@entry_id:146164)问题等关键算法中发挥作用，并将其应用扩展到物理学中的量子行走动力学，以及与数论中[高斯和](@entry_id:196588)等概念的深刻联系。

最后，在 **“动手实践”** 部分，我们提供了一系列精心设计的练习，旨在通过具体计算来巩固您对QFT算符性质及其在不同场景下应用的理解，将抽象的理论转化为可操作的技能。

通过这趟旅程，读者将不仅理解QFT“是什么”，更将领会它“为什么”如此强大，从而为在[量子信息科学](@entry_id:150091)及相关领域进行更深入的研究与创新打下坚实的基础。

## 原理与机制

本章将深入探讨[量子傅里叶变换](@entry_id:139146) (Quantum Fourier Transform, QFT) 的核心数学原理与物理机制。我们将从循环群的[表示论](@entry_id:137998)出发，揭示QFT作为一种基变换的本质，探索其深刻的代数与谱性质，并最终阐明其与子群结构和数论概念（如中国剩余定理）的内在联系。这些原理不仅是理解QFT的关键，也是掌握如Shor算法等[量子算法](@entry_id:147346)的基石。

### 循环群 $\mathbb{Z}_N$ 的表示

循环群 $\mathbb{Z}_N = \{0, 1, \dots, N-1\}$（在模$N$加法下构成群）是[离散对称性](@entry_id:146994)中最简单而又最重要的例子。它在物理和工程中的应用，如[晶格](@entry_id:196752)系统和数字信号处理，使其表示论成为一个基础而强大的工具。

群的**表示 (representation)** 是群到一组[可逆线性变换](@entry_id:149915)（矩阵）的同态映射，它保留了群的乘法结构。对于像 $\mathbb{Z}_N$ 这样的阿贝尔群（[交换群](@entry_id:145145)），其所有的**[不可约表示](@entry_id:263310) (irreducible representations, irreps)** 都是一维的。这意味着每个群元素 $j \in \mathbb{Z}_N$ 被映射到一个复数。$\mathbb{Z}_N$ 共有 $N$ 个不同的[不可约表示](@entry_id:263310)，我们用索引 $k \in \{0, 1, \dots, N-1\}$ 来标记它们。第 $k$ 个[不可约表示](@entry_id:263310) $\rho_k$ 将群元素 $j$ 映射为：

$$
\rho_k(j) = \exp\left(\frac{2\pi i j k}{N}\right)
$$

这个复数值本身就是[一维表示](@entry_id:136509)矩阵的迹，因此它也是该表示的**特征标 (character)**，记为 $\chi_k(j)$。这些特征标构成了所谓的特征标群 $\widehat{\mathbb{Z}_N}$，它本身也同构于 $\mathbb{Z}_N$。

任何有限维的 $\mathbb{Z}_N$ 表示 $\Gamma$ 都可以被完全分解为这些不可约表示的直和：

$$
\Gamma \cong \bigoplus_{j=0}^{N-1} a_j \rho_j
$$

其中，非负整数 $a_j$ 被称为不可约表示 $\rho_j$ 在分解中的**重数 (multiplicity)**。一个[表示的特征标](@entry_id:198072)是其构成的不可约表示特征标的加权和，即 $\chi_\Gamma = \sum_j a_j \chi_j$。由于特征标系构成一组[正交函数](@entry_id:160936)，我们可以通过[特征标的内积](@entry_id:137615)来提取这些重数：

$$
a_j = \langle \chi_j, \chi_\Gamma \rangle = \frac{1}{N} \sum_{k=0}^{N-1} \chi_j(g^k)^* \chi_\Gamma(g^k)
$$

其中 $g$是$\mathbb{Z}_N$的生成元（例如，元素$1$），$g^k$代表群中的元素$k$，而 $*$ 表示[复共轭](@entry_id:174690)。

为了具体理解这一分解过程，我们考虑一个假设的例子。设想一个4维系统，其对称性由群 $\mathbb{Z}_6$ 描述。该表示 $\Gamma$ 由其生成元 $g$ 的作用矩阵 $\Gamma(g) = M$ 定义，其中 $M$ 是一个 $4 \times 4$ 的矩阵。任意元素 $g^k$ 的表示即为 $\Gamma(g^k) = M^k$。此[表示的特征标](@entry_id:198072) $\chi_\Gamma(g^k)$ 就是矩阵 $M^k$ 的迹 $\text{Tr}(M^k)$。如果我们知道 $\chi_\Gamma(g^k)$ 的具体形式，例如对于某个特定的$M$可以计算出 $\chi_\Gamma(g^k) = 2\cos(k\pi/3) + 1 + (-1)^k$，我们就可以利用[内积](@entry_id:158127)公式计算每个不可约表示 $\chi_j(g^k) = \exp(2\pi i j k / 6)$ 的重数 $a_j$。通过计算 $j=0, 1, \dots, 5$ 的所有 $a_j$ 值，我们就能完全确定该4维表示是如何由 $\mathbb{Z}_6$ 的基本[一维表示](@entry_id:136509)构成的。这个过程揭示了复杂系统如何在其基本对称单元的基础上构建 [@problem_id:821832]。

### 作为基变换的[量子傅里叶变换](@entry_id:139146)

[量子傅里叶变换](@entry_id:139146)是在一个 $N$ 维希尔伯特空间 $\mathcal{H}_N = \mathbb{C}^N$ 上的一个关键酉算符。这个空间通常由一组称为**计算基 (computational basis)** 的[标准正交基](@entry_id:147779)矢 $\{|j\rangle : j=0, 1, \dots, N-1\}$ 张成，其中每个[基矢](@entry_id:199546) $|j\rangle$ 对应于[循环群](@entry_id:138668) $\mathbb{Z}_N$ 的一个元素。

QFT算符 $F_N$ 在计算基下的矩阵元定义为：

$$
(F_N)_{kj} = \frac{1}{\sqrt{N}} \omega_N^{jk}
$$

其中 $\omega_N = \exp(2\pi i/N)$ 是 $N$ 次单位[主根](@entry_id:164411)。算符 $F_N$ 作用在计算[基矢](@entry_id:199546) $|j\rangle$ 上的结果是：

$$
F_N |j\rangle = \frac{1}{\sqrt{N}} \sum_{k=0}^{N-1} \omega_N^{jk} |k\rangle
$$

这个操作的核心意义在于执行了一次[基变换](@entry_id:189626)。QFT将计算基 $\{|j\rangle\}$ 变换到一组新的[正交基](@entry_id:264024)，即**[傅里叶基](@entry_id:201167) (Fourier basis)** $\{|\tilde{k}\rangle\}$。[傅里叶基](@entry_id:201167)矢的定义为：

$$
|\tilde{k}\rangle = F_N |k\rangle = \frac{1}{\sqrt{N}} \sum_{j=0}^{N-1} \omega_N^{kj} |j\rangle
$$

[傅里叶基](@entry_id:201167)之所以重要，是因为它们是所有**[平移算符](@entry_id:756122) (translation operators)** $U_a$ 的共同本征矢。[平移算符](@entry_id:756122) $U_a$ 定义为 $U_a |j\rangle = |(j+a) \pmod N\rangle$。容易验证，[傅里叶基](@entry_id:201167)矢满足如下本征方程：

$$
U_a |\tilde{k}\rangle = \omega_N^{-ak} |\tilde{k}\rangle
$$

这意味着，在计算基中表现为[置换](@entry_id:136432)的[平移算符](@entry_id:756122)，在[傅里叶基](@entry_id:201167)中则变成了简单的对角矩阵，其对角元为复相位 $\omega_N^{-ak}$。QFT 正是实现这种[对角化](@entry_id:147016)的变换。

理解了 QFT 作为基变换的角色，我们就可以分析任意算符在两个基下的关系。例如，给定一个由计算[基矢](@entry_id:199546)构成的秩一算符 $A = |a\rangle\langle b|$，我们可以计算它在[傅里叶基](@entry_id:201167)下的矩阵元 $\langle \tilde{p} | A | \tilde{q} \rangle$。这等价于将算符 $A$ 的分量从一个[坐标系转换](@entry_id:263003)到另一个[坐标系](@entry_id:156346)。计算过程如下：

$$
\langle \tilde{p} | A | \tilde{q} \rangle = \langle \tilde{p} | a \rangle \langle b | \tilde{q} \rangle
$$

其中 $\langle \tilde{p} | a \rangle$ 是[基矢](@entry_id:199546) $|a\rangle$ 在[傅里叶基](@entry_id:201167)矢 $|\tilde{p}\rangle$ 上的投影。根据[傅里叶基](@entry_id:201167)的定义，$\langle a | \tilde{p} \rangle = \frac{1}{\sqrt{N}} \omega_N^{ap}$，因此 $\langle \tilde{p} | a \rangle = (\langle a | \tilde{p} \rangle)^* = \frac{1}{\sqrt{N}} \omega_N^{-ap}$。代入后可得：

$$
\langle \tilde{p} | A | \tilde{q} \rangle = \left(\frac{1}{\sqrt{N}} \omega_N^{-ap}\right) \left(\frac{1}{\sqrt{N}} \omega_N^{bq}\right) = \frac{1}{N} \omega_N^{bq-ap}
$$

这种计算练习强化了我们对 QFT 如何联系这两个重要基底的理解 [@problem_id:821787]。

### [量子傅里叶变换](@entry_id:139146)算符的基本性质

#### 与[循环矩阵](@entry_id:143620)的关系

[傅里叶基](@entry_id:201167)能够[对角化](@entry_id:147016)[平移算符](@entry_id:756122)这一性质，具有深远的意义。一个 $N \times N$ 矩阵 $C$ 如果它的每一行都是上一行向右循环平移一位得到的结果，则称之为**[循环矩阵](@entry_id:143620) (circulant matrix)**。所有 $N \times N$ [循环矩阵](@entry_id:143620)构成的集合形成一个代数，它与[群代数](@entry_id:145139) $\mathbb{C}[\mathbb{Z}_N]$ 同构。

任何一个首行为 $(c_0, c_1, \dots, c_{N-1})$ 的[循环矩阵](@entry_id:143620) $C$ 都可以表示为基本[平移算符](@entry_id:756122) $U_1$ (即将 $|j\rangle$ 变为 $|j+1\rangle$) 的多项式： $C = \sum_{j=0}^{N-1} c_j U_{-j} = \sum_{j=0}^{N-1} c_j (U_1^\dagger)^j$。由于[傅里叶基](@entry_id:201167) $\{|\tilde{k}\rangle\}$ 是 $U_1$ (以及 $U_1^\dagger$) 的本征基，它也必然是所有[循环矩阵](@entry_id:143620)的共同本征基。$C$ 在[傅里叶基](@entry_id:201167)下的[本征值](@entry_id:154894) $\lambda_k$ 可以通过将其作用于本征矢 $|\tilde{k}\rangle$ 来找到：

$$
C |\tilde{k}\rangle = \left(\sum_{j=0}^{N-1} c_j U_{-j}\right) |\tilde{k}\rangle = \left(\sum_{j=0}^{N-1} c_j \omega_N^{-(-j)k}\right) |\tilde{k}\rangle = \left(\sum_{j=0}^{N-1} c_j \omega_N^{jk}\right) |\tilde{k}\rangle
$$
注意，这里的[本征值](@entry_id:154894)公式可能因 $U_a$ 的[本征值](@entry_id:154894)符号约定（$\omega_N^{\pm ak}$）而异。若约定 $U_a$ 的[本征值](@entry_id:154894)为 $\omega_N^{-ak}$，则 $C$ 的[本征值](@entry_id:154894)为 $\sum c_j (\omega_N^{-k})^j$。若约定为 $\omega_N^{ak}$，则 $C$ 的[本征值](@entry_id:154894)为 $\sum c_j (\omega_N^k)^j$。无论如何，[本征值](@entry_id:154894)总是首行向量的离散傅里叶变换。

由于一个矩阵的行列式是其所有[本征值](@entry_id:154894)的乘积，我们可以利用这一性质来高效计算循环[矩阵的[行列](@entry_id:148198)式](@entry_id:142978)。例如，对于一个 $5 \times 5$ 的[循环矩阵](@entry_id:143620)，其首行为 $(2, 1, 0, 0, 1)$，我们可以计算出它的5个[本征值](@entry_id:154894) $\lambda_k = 2 + \omega_5^{-k} + \omega_5^{-4k} = 2 + 2\cos(2\pi k/5)$ for $k=0, \dots, 4$。然后将这5个[本征值](@entry_id:154894)相乘，即可得到该矩阵的行列式 [@problem_id:821898]。

#### 算符的平方与宇称

QFT算符的幂次具有简洁而优美的性质。我们来考察 $F_N^2$ 的作用。通过连续两次应用QFT变换，可以推导出：

$$
F_N^2 |j\rangle = |(-j) \pmod N\rangle
$$

这个推导依赖于关于[单位根](@entry_id:143302)求和的一个重要恒等式: $\sum_{k=0}^{N-1} \omega_N^{k(m)} = N \delta_{m \pmod N, 0}$。因此，$F_N^2$ 算符等价于一个**[宇称算符](@entry_id:148434) (Parity Operator)** $P$，它将每个计算[基矢](@entry_id:199546)映射到其在群 $\mathbb{Z}_N$ 中的加法逆元对应的[基矢](@entry_id:199546)上 [@problem_id:821784]。

这一优雅的关系立即带来一些重要的推论。首先，$P^2 = I$（两次反转等于恒等操作），这意味着 $F_N^4 = (F_N^2)^2 = P^2 = I$。这表明 QFT 算符的四次方是单位算符，这是一个深刻的代数性质。

其次，我们可以计算 $F_N^2$ 的迹。[算符的迹](@entry_id:185149)等于其对角元之和，$\text{Tr}(F_N^2) = \sum_j \langle j | F_N^2 | j \rangle = \sum_j \langle j | (-j) \pmod N \rangle$。由于计算基是正交的，$\langle j | k \rangle = \delta_{j,k}$，所以 $\text{Tr}(F_N^2)$ 就等于满足 $j \equiv -j \pmod N$（即 $2j \equiv 0 \pmod N$）的解 $j$ 的个数。
*   如果 $N$ 是奇数（例如 $N=23$），由于 $2$ 和 $N$ [互素](@entry_id:143119)，$2j \equiv 0 \pmod N$ 的唯一解是 $j=0$。因此 $\text{Tr}(F_{23}^2) = 1$ [@problem_id:821784]。
*   如果 $N$ 是偶数（例如 $N=30$），$2j \equiv 0 \pmod N$有两个解：$j=0$ 和 $j=N/2$。因此 $\text{Tr}(F_{30}^2) = 2$ [@problem_id:821903]。

这个性质也揭示了 QFT 与[宇称算符](@entry_id:148434)的紧密联系。例如，利用[迹的循环性质](@entry_id:153103) $\text{Tr}(ABC) = \text{Tr}(CAB)$，可以轻易证明 $\text{Tr}(F_N P F_N^\dagger) = \text{Tr}(P F_N^\dagger F_N) = \text{Tr}(P I) = \text{Tr}(P) = \text{Tr}(F_N^2)$ [@problem_id:821903]。

### 更深层的结构与谱性质

#### QFT的本征谱

$F_N^4 = I$ 这一事实意味着 $F_N$ 的[本征值](@entry_id:154894) $\lambda$ 必须满足 $\lambda^4=1$，所以 $F_N$ 的本征谱落在集合 $\{1, -1, i, -i\}$ 中。一个自然且深刻的问题是：对于给定的 $N$，这四个[本征值](@entry_id:154894)各自的重数（即对应[本征空间](@entry_id:147356)的维度）是多少？

我们可以通过求解一个线性方程组来确定这些重数，记为 $n_1, n_{-1}, n_i, n_{-i}$。这个[方程组](@entry_id:193238)由 $F_N$ 的各次幂的迹构成：
1.  $n_1 + n_{-1} + n_i + n_{-i} = \text{Tr}(F_N^0) = \text{Tr}(I) = N$
2.  $1 \cdot n_1 + (-1) \cdot n_{-1} + i \cdot n_i + (-i) \cdot n_{-i} = \text{Tr}(F_N)$
3.  $1^2 \cdot n_1 + (-1)^2 \cdot n_{-1} + i^2 \cdot n_i + (-i)^2 \cdot n_{-i} = n_1 + n_{-1} - n_i - n_{-i} = \text{Tr}(F_N^2)$
4.  $1^3 \cdot n_1 + (-1)^3 \cdot n_{-1} + i^3 \cdot n_i + (-i)^3 \cdot n_{-i} = n_1 - n_{-1} - i n_i + i n_{-i} = \text{Tr}(F_N^3)$

我们已经知道如何计算 $\text{Tr}(F_N^2)$。$\text{Tr}(F_N^3) = \text{Tr}(F_N^\dagger) = \overline{\text{Tr}(F_N)}$。因此，关键在于计算 $\text{Tr}(F_N)$。$\text{Tr}(F_N) = \sum_j \langle j | F_N | j \rangle = \frac{1}{\sqrt{N}} \sum_j \omega_N^{j^2}$。这个求和被称为**二次[高斯和](@entry_id:196588) (Quadratic Gauss Sum)** $G(N) = \sum_{j=0}^{N-1} \exp(2\pi i j^2/N)$。[高斯和](@entry_id:196588)的值取决于 $N$ 的数论性质，其计算在数论中是一个经典问题。例如，对于 $N=10$，可以证明 $G(10)=0$，而对于素数 $p \equiv 1 \pmod 4$ (如 $p=17$)，$G(p)=\sqrt{p}$。

掌握了这些迹的值后，我们就可以解出[重数](@entry_id:136466)。例如，对于 $N=10$，我们有 $\text{Tr}(F_{10}^2)=2$ 和（根据上述）$\text{Tr}(F_{10})=0$。联立上述[方程组](@entry_id:193238)，可以解得这四个[本征空间](@entry_id:147356)的维度分别为 $n_1=3, n_{-1}=3, n_i=2, n_{-i}=2$ [@problem_id:821948]。

#### 对称性与[子空间](@entry_id:150286)

[宇称算符](@entry_id:148434) $P=F_N^2$ 与 $F_N$ 是可交换的（因为 $P F_N = F_N^3$ 且 $F_N P = F_N F_N^2 = F_N^3$），这意味着它们可以被[同时对角化](@entry_id:196036)。因此，$F_N$ 在 $P$ 的[本征空间](@entry_id:147356)中是块对角的。$P$ 的[本征值](@entry_id:154894)为 $\pm 1$，对应的[本征空间](@entry_id:147356)分别是**对称[子空间](@entry_id:150286)** $\mathcal{H}_+$（$P|\psi\rangle = |\psi\rangle$）和**反对称[子空间](@entry_id:150286)** $\mathcal{H}_-$（$P|\psi\rangle = -|\psi\rangle$）。

我们可以研究 QFT 算符在这些不变子空间上的行为。例如，要计算 $F_N$ 限制在对称[子空间](@entry_id:150286) $\mathcal{H}_+$ 上的迹 $\text{Tr}_{\mathcal{H}_+}(F_N)$，我们可以使用[投影算符](@entry_id:154142)。投影到 $\mathcal{H}_+$ 的算符是 $\Pi_+ = \frac{1}{2}(I+P)$。因此，

$$
\text{Tr}_{\mathcal{H}_+}(F_N) = \text{Tr}(F_N \Pi_+) = \frac{1}{2} \text{Tr}(F_N(I+P)) = \frac{1}{2}(\text{Tr}(F_N) + \text{Tr}(F_N P))
$$

$\text{Tr}(F_N P)$ 可以通过计算 $\text{Tr}(F_N^3)$ 得到，而 $\text{Tr}(F_N)$ 依赖于[高斯和](@entry_id:196588)。以 $N=17$（一个素数且 $17 \equiv 1 \pmod 4$）为例，我们知道 $G(17)=\sqrt{17}$。所以 $\text{Tr}(F_{17}) = \frac{1}{\sqrt{17}}G(17)=1$。同时，$\text{Tr}(F_{17}^3) = \overline{\text{Tr}(F_{17})} = 1$。因此，$\text{Tr}_{\mathcal{H}_+}(F_{17}) = \frac{1}{2}(1+1)=1$。这揭示了 QFT 在具有特定对称性的态构成的[子空间](@entry_id:150286)上的平均行为 [@problem_id:821753]。

### QFT与子[群结构](@entry_id:146855)

#### [零化子](@entry_id:155446)群

QFT 与 $\mathbb{Z}_N$ 的子群结构之间存在深刻的对偶关系，这通过**[零化子](@entry_id:155446) (annihilator)** 的概念来阐明。对于 $\mathbb{Z}_N$ 的任何一个[子群](@entry_id:146164) $H \le \mathbb{Z}_N$，其[零化子](@entry_id:155446) $H^\perp$ 是特征标群 $\widehat{\mathbb{Z}_N}$ 中的一个[子群](@entry_id:146164)，它由所有在 $H$ 上取值为1的特征标构成：

$$
H^\perp = \{ \chi_k \in \widehat{\mathbb{Z}_N} \mid \chi_k(h) = 1 \text{ for all } h \in H \}
$$

由于 $\widehat{\mathbb{Z}_N}$ 同构于 $\mathbb{Z}_N$（通过映射 $\chi_k \leftrightarrow k$），$H^\perp$ 也对应于 $\mathbb{Z}_N$ 中的一个[子群](@entry_id:146164)。$\chi_k$ 是 $H$ 的[零化子](@entry_id:155446)的条件是 $\exp(2\pi i h k / N) = 1$ 对所有 $h \in H$ 成立，这等价于 $hk/N$ 对所有 $h \in H$ 都是整数。如果 $H$ 是由元素 $g$ 生成的[循环子群](@entry_id:138079) $H=\langle g \rangle$，那么这个条件简化为 $gk/N$ 是一个整数。

例如，考虑群 $G = \mathbb{Z}_{24}$ 和其[子群](@entry_id:146164) $H = \langle 6 \rangle = \{0, 6, 12, 18\}$。要找到其[零化子](@entry_id:155446) $H^\perp$ 对应的 $\mathbb{Z}_{24}$中的[子群](@entry_id:146164)，我们需求解 $6k/24 \in \mathbb{Z}$，即 $k/4 \in \mathbb{Z}$。这意味着 $k$ 必须是 $4$ 的倍数。因此，$H^\perp$ 对应的[子群](@entry_id:146164)是 $\{0, 4, 8, 12, 16, 20\} = \langle 4 \rangle$。这个[子群](@entry_id:146164)的最小正生成元是 $4$ [@problem_id:821783]。

这个概念也解释了[傅里叶基](@entry_id:201167)矢的“稳定性”问题。一个[傅里叶基](@entry_id:201167)矢 $|\tilde{k}\rangle$ 如果被[子群](@entry_id:146164) $H$ “稳定”，意味着对于所有 $h \in H$，$U_h |\tilde{k}\rangle = |\tilde{k}\rangle$。根据 $U_h$ 的[本征值方程](@entry_id:192306)，这要求 $\omega_N^{-hk} = 1$（或 $\omega_N^{hk}=1$，符号不影响结果），这恰好是 $k$ 属于 $H^\perp$ 对应[指标集](@entry_id:268489)的条件。因此，被 $H$ 稳定的[傅里叶基](@entry_id:201167)矢的数目就是零化[子群的阶](@entry_id:143341) $|H^\perp|$。根据拉格朗日定理的对偶形式，我们有 $|H| \cdot |H^\perp| = N$。这提供了一个计算稳[定态](@entry_id:137260)数目的优雅方法 [@problem_id:821905]。

#### 中国剩余定理与QFT的分解

当 $N$ 是两个[互素整数](@entry_id:152973) $N_1, N_2$ 的乘积（$N=N_1 N_2$）时，**[中国剩余定理](@entry_id:144030) (Chinese Remainder Theorem, CRT)** 指出，群 $\mathbb{Z}_N$ 同构于[直积](@entry_id:143046)群 $\mathbb{Z}_{N_1} \times \mathbb{Z}_{N_2}$。该同构由映射 $\phi(j) = (j \pmod{N_1}, j \pmod{N_2})$ 给出。

这个[群同构](@entry_id:147371)诱导了其特征标群之间的一个同构：$\widehat{\mathbb{Z}_N} \cong \widehat{\mathbb{Z}_{N_1}} \times \widehat{\mathbb{Z}_{N_2}}$。这意味着 $\mathbb{Z}_N$ 上的每一个特征标 $\chi_k$ 都唯一对应于一对特征标 $(\chi'_a, \chi''_b)$，其中 $\chi'_a \in \widehat{\mathbb{Z}_{N_1}}$ and $\chi''_b \in \widehat{\mathbb{Z}_{N_2}}$。它们之间的关系通过以下等式建立：

$$
\chi_k(j) = \chi'_a(j \pmod{N_1}) \cdot \chi''_b(j \pmod{N_2})
$$

将特征标的定义代入，我们得到：

$$
\exp\left(\frac{2\pi i j k}{N_1 N_2}\right) = \exp\left(\frac{2\pi i a (j \pmod{N_1})}{N_1}\right) \cdot \exp\left(\frac{2\pi i b (j \pmod{N_2})}{N_2}\right)
$$

这个等式对所有 $j$ 成立，它隐含了索引 $k$ 与索引对 $(a, b)$ 之间的深刻数论联系。我们可以通过选取特殊的 $j$ 值来解出 $a$ 和 $b$ 与 $k$ 的关系。例如，考虑 $\mathbb{Z}_{35} \cong \mathbb{Z}_5 \times \mathbb{Z}_7$。对于 $\mathbb{Z}_{35}$ 上的特征标 $\chi_1$ (即 $k=1$)，我们可以通过令 $j$ 为 $7$ 的倍数来求解 $a$，再令 $j$ 为 $5$ 的倍数来求解 $b$，从而找到与之对应的 $a \in \mathbb{Z}_5$ 和 $b \in \mathbb{Z}_7$ [@problem_id:821786]。

这个数学上的分解是[量子傅里叶变换](@entry_id:139146)能够被高效实现为[量子线路](@entry_id:151866)的理论基础。$F_N$ 算符可以分解为作用在更小[子空间](@entry_id:150286)上的 $F_{N_1}$ 和 $F_{N_2}$ 算符的张量积（以及一些受控[旋转操作](@entry_id:140575)）。通过递归地应用这个分解，可以将一个大维度的QFT分解为一系列单[量子比特](@entry_id:137928)和双[量子比特](@entry_id:137928)门，这是 Shor 算法等依赖 QFT 的[量子算法](@entry_id:147346)能够具备指数级加速能力的关键所在。