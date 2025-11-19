## 引言
[狄拉克符号](@entry_id:154811)与[希尔伯特空间](@entry_id:261193)共同构成了现代量子力学的数学基石与表述语言，是任何希望深入研究理论化学与物理的学者的必备工具。然而，从量子概念的直观理解跨越到能够进行严谨推导和精确计算的数学形式体系，往往是学习过程中的一道门槛。本文旨在系统性地扫清这一障碍，为读者搭建一座连接抽象理论与实际应用的坚实桥梁。

在接下来的内容中，我们将分三个章节展开探讨。**第一章：原理与机制**将深入量子理论的数学核心，建立[希尔伯特空间](@entry_id:261193)的舞台，并介绍[狄拉克符号](@entry_id:154811)这套优雅的语言，用以描述[量子态](@entry_id:146142)、算符和测量过程。**第二章：应用与跨学科联系**将展示这一抽象框架在分子[光谱](@entry_id:185632)、[量子化学](@entry_id:140193)、凝聚态物理乃至量子信息等前沿领域的强大威力，阐明其如何解决具体的科学问题。最后，**第三章：动手实践**将通过一系列精心设计的问题，帮助读者将理论知识转化为实际的计算和推导能力。

通过这一结构化的学习路径，读者将不仅掌握[狄拉克符号](@entry_id:154811)与[希尔伯特空间](@entry_id:261193)的定义和性质，更能深刻领会它们如何成为贯穿整个现代量子科学的统一[范式](@entry_id:161181)。让我们首先进入第一章，探索量子世界的原理与机制。

## 原理与机制

本章在前一章介绍性背景的基础上，深入探讨量子力学数学形式体系的核心原理与机制。我们将首先建立[量子态](@entry_id:146142)所在的数学舞台——希尔伯特空间，然后介绍描述和操作这些[量子态](@entry_id:146142)的优雅语言——[狄拉克符号](@entry_id:154811)。最后，我们会将这些工具应用于描述[物理可观测量](@entry_id:154692)、复合系统以及[量子测量](@entry_id:272490)的过程。

### 希尔伯特空间：[量子态](@entry_id:146142)的舞台

在量子力学中，一个系统的纯态由一个[复向量空间](@entry_id:264355)中的[向量表示](@entry_id:166424)。为了赋予这个空间足够的结构以支持物理诠释和计算，我们要求它是一个**[希尔伯特空间](@entry_id:261193) (Hilbert space)**。这需要引入一个[内积](@entry_id:158127)，并满足完备性条件。

#### [内积](@entry_id:158127)及其性质

一个[复向量空间](@entry_id:264355) $V$ 上的**[内积](@entry_id:158127) (inner product)** 是一个映射 $\langle \cdot | \cdot \rangle: V \times V \to \mathbb{C}$，它将一对向量 $| \phi \rangle$ 和 $| \psi \rangle$ 映为一个复数 $\langle \phi | \psi \rangle$，并满足以下公理 [@problem_id:2768447]：

1.  **[共轭对称性](@entry_id:144131) (Conjugate symmetry)**：$\langle \phi | \psi \rangle = \overline{\langle \psi | \phi \rangle}$。这里上划线表示[复共轭](@entry_id:174690)。

2.  **[半双线性](@entry_id:188042) (Sesquilinearity)**：[内积](@entry_id:158127)在一个参数中是线性的，在另一个参数中是[共轭线性](@entry_id:268590)的。物理学界普遍采用狄拉克约定，即[内积](@entry_id:158127)在第二个参数（右侧的 ket）上是线性的，而在第一个参数（左侧的 bra）上是[共轭线性](@entry_id:268590)的。对于任意复数 $a, b \in \mathbb{C}$ 和向量 $| \phi_1 \rangle, | \phi_2 \rangle, | \psi \rangle \in V$：
    $$ \langle \psi | a \phi_1 + b \phi_2 \rangle = a \langle \psi | \phi_1 \rangle + b \langle \psi | \phi_2 \rangle \quad (\text{线性})$$
    $$ \langle a \phi_1 + b \phi_2 | \psi \rangle = \bar{a} \langle \phi_1 | \psi \rangle + \bar{b} \langle \phi_2 | \psi \rangle \quad (\text{共轭线性})$$
    我们将在下一节中看到，这个约定是[狄拉克符号](@entry_id:154811)内在逻辑的自然结果。

3.  **正定性 (Positive-definiteness)**：任意向量与自身的[内积](@entry_id:158127)是非负实数：$\langle \psi | \psi \rangle \ge 0$。并且，$\langle \psi | \psi \rangle = 0$ 当且仅当 $| \psi \rangle$ 是零向量。

[内积](@entry_id:158127)自然地在[向量空间](@entry_id:151108)上引入了**范数 (norm)** 的概念，定义为 $||\psi|| = \sqrt{\langle \psi | \psi \rangle}$。范数可以理解为向量的“长度”。对于一个归一化的[量子态](@entry_id:146142) $| \psi \rangle$，我们有 $||\psi|| = 1$。

#### 完备性及其物理意义

一个配备了[内积](@entry_id:158127)的[向量空间](@entry_id:151108)被称为**[内积空间](@entry_id:271570) (inner product space)** 或前[希尔伯特空间](@entry_id:261193)。要成为一个真正的希尔伯特空间，它还必须满足**完备性 (completeness)** 公理。完备性要求空间中任何**柯西序列 (Cauchy sequence)** 都收敛于空间内的某个向量。一个向量序列 $\{|\psi_n\rangle\}$ 是柯西序列，如果当 $m, n \to \infty$ 时，它们之间的“距离” $||\psi_m - \psi_n|| \to 0$。完备性保证了这个[序列的极限](@entry_id:159239) $|\psi\rangle = \lim_{n\to\infty} |\psi_n\rangle$ 确实存在于该空间之内。

完备性并非一个无足轻重的数学细节，它对[量子理论](@entry_id:145435)的结构至关重要 [@problem_id:2768447]：
-   在[理论化学](@entry_id:199050)的[变分法](@entry_id:163656)和[基组展开](@entry_id:204251)等近似计算中，我们构造一系列近似[波函数](@entry_id:147440) $\{|\psi_n\rangle\}$，期望它们能收敛到真实的解。这些序列通常是柯西序列。完备性保证了它们的极限是一个合法的[量子态](@entry_id:146142)，存在于我们定义的态空间中，从而确保了近似方法与精确理论之间的桥梁是稳固的。
-   描述物理可观测量（如[哈密顿量](@entry_id:172864)）的自伴算符的**谱理论 (spectral theorem)**，以及描述系统[幺正时间演化](@entry_id:192535)的**[斯通定理](@entry_id:262301) (Stone's theorem)**，都是在希尔伯特空间中表述和证明的。这些定理是量子理论的支柱，它们依赖于空间的完备性。

一个典型的例子是描述三维空间中单个电子的希尔伯特空间 $L^2(\mathbb{R}^3)$，即所有在 $\mathbb{R}^3$ 上平方可积的[复值函数](@entry_id:196054)构成的空间。其[内积](@entry_id:158127)定义为 $\langle \phi | \psi \rangle = \int_{\mathbb{R}^3} \overline{\phi(\mathbf{r})} \psi(\mathbf{r}) d^3\mathbf{r}$。根据量子力学的[玻恩诠释](@entry_id:261984)，对于一个束缚态，在全空间找到该电子的总概率必须为1，即 $\int_{\mathbb{R}^3} |\psi(\mathbf{r})|^2 d^3\mathbf{r} = 1$。这个[归一化条件](@entry_id:156486)直接意味着[波函数](@entry_id:147440) $\psi(\mathbf{r})$ 的 $L^2$ 范数是有限的（等于1），因此它必须属于 $L^2(\mathbb{R}^3)$ 空间 [@problem_id:2768439]。

人们可能会担心，在[原子核](@entry_id:167902)位置，库仑势是奇异的，这是否会破坏[波函数](@entry_id:147440)的平方可积性？事实上，[库仑势](@entry_id:154276)的[奇点](@entry_id:137764)确实导致了[波函数](@entry_id:147440)在[原子核](@entry_id:167902)位置出现**尖点 (cusp)**，即其一阶导数不连续。然而，[波函数](@entry_id:147440)本身在[原子核](@entry_id:167902)处仍然是有限且连续的。例如，对于一个[电荷](@entry_id:275494)为 $Z$ 的[原子核](@entry_id:167902)和一个 $s$ 态电子，精确的[波函数](@entry_id:147440)满足 Kato [尖点条件](@entry_id:190416) $(\partial \psi / \partial r)|_{r=0} = -Z \psi(0)$。一个在某点有限的函数，其在该点附近的平方可积性不会受到导数不连续的影响。此外，对于能量为 $E  0$ 的束缚态，在远离[原子核](@entry_id:167902)的区域（$r \to \infty$），[波函数](@entry_id:147440)会呈指数衰减，其渐近行为近似于 $\psi(\mathbf{r}) \sim \exp(-\sqrt{-2E}r)$。这种快速衰减的行为确保了[波函数](@entry_id:147440)在全空间是平方可积的 [@problem_id:2768439]。

### [狄拉克符号](@entry_id:154811)：量子力学的语言

狄拉克引入的**bra-ket**或**[狄拉克符号](@entry_id:154811) (Dirac notation)** 不仅是一种方便的记法，它还深刻地反映了希尔伯特空间的内在数学结构。

#### Bra、Ket 与对偶空间

-   **[右矢](@entry_id:152965) (Ket)**：一个 ket 向量 $| \psi \rangle$ 是希尔伯特空间 $\mathcal{H}$ 中的一个元素。它代表一个系统的物理状态。

-   **左矢 (Bra)**：一个 bra 向量 $\langle \phi |$ 被定义为 $\mathcal{H}$ 上的一个**[连续线性泛函](@entry_id:262913) (continuous linear functional)**。[线性泛函](@entry_id:276136)是一个从 $\mathcal{H}$ 到复数域 $\mathbb{C}$ 的线性映射。也就是说，$\langle \phi |$ “吃”一个 ket $| \psi \rangle$，然后“吐出”一个复数，这个过程我们记作 $\langle \phi | \psi \rangle$。
    根据其定义，这个映射必须对它的输入参数——ket——是线性的：
    $$ \langle \phi | (a|\psi_1\rangle + b|\psi_2\rangle) = a \langle \phi | \psi_1 \rangle + b \langle \phi | \psi_2 \rangle $$

-   **对偶空间 (Dual space)**：所有 $\mathcal{H}$ 上的[连续线性泛函](@entry_id:262913)构成的空间称为 $\mathcal{H}$ 的[对偶空间](@entry_id:146945)，记作 $\mathcal{H}^*$。因此，bra 向量是[对偶空间](@entry_id:146945)的元素。

#### [内积](@entry_id:158127)、Riesz [表示定理](@entry_id:637872)与物理学家的约定

我们将 bra-ket $\langle \phi | \psi \rangle$ 与希尔伯特空间中的[内积](@entry_id:158127)等同起来。这个看似简单的举动，结合 bra 作为[线性泛函](@entry_id:276136)的定义，立即产生了深刻的后果。我们已经知道，$\langle \phi | \psi \rangle$ 必须在第二个参数 $| \psi \rangle$ 上是线性的。现在，利用[内积](@entry_id:158127)的[共轭对称性](@entry_id:144131)公理，我们可以推断出它在第一个参数上的性质 [@problem_id:2768452]：
$$ \langle a \phi | \psi \rangle = \overline{\langle \psi | a \phi \rangle} = \overline{a \langle \psi | \phi \rangle} = \bar{a} \overline{\langle \psi | \phi \rangle} = \bar{a} \langle \phi | \psi \rangle $$
这证明了[内积](@entry_id:158127)在第一个参数（bra）上必须是[共轭线性](@entry_id:268590)的。因此，物理学中[内积](@entry_id:158127)的[半双线性](@entry_id:188042)约定（在 ket 上线性，在 bra 上[共轭线性](@entry_id:268590)）是[狄拉克符号](@entry_id:154811)内部逻辑自洽性的直接要求。

那么，每个 ket $| \phi \rangle \in \mathcal{H}$ 是否都唯一对应一个 bra $\langle \phi | \in \mathcal{H}^*$ 呢？**Riesz [表示定理](@entry_id:637872) (Riesz representation theorem)** 给出了肯定的回答。该定理指出，对于[复希尔伯特空间](@entry_id:185216) $\mathcal{H}$ 中的任意一个[连续线性泛函](@entry_id:262913) $f \in \mathcal{H}^*$，都存在一个唯一的向量 $| \phi_f \rangle \in \mathcal{H}$，使得对于所有 $| \psi \rangle \in \mathcal{H}$，有 $f(|\psi\rangle) = \langle \phi_f | \psi \rangle$。

这一定理为 bra 和 ket 之间通过[内积](@entry_id:158127)建立的对应关系提供了严格的数学基础。它保证了我们可以将[对偶空间](@entry_id:146945) $\mathcal{H}^*$ 中的每个 bra 与原始空间 $\mathcal{H}$ 中的一个 ket 唯一地联系起来。然而，这个对应关系 $J: \mathcal{H} \to \mathcal{H}^*$（即 $J(|\phi\rangle) = \langle\phi|$）并[非线性映射](@entry_id:272931)，而是**[反线性](@entry_id:268590) (anti-linear)** 或[共轭线性](@entry_id:268590)的 [@problem_id:2768452]。这是因为：
$$ J(a|\phi\rangle) = \langle a\phi | $$
而 $\langle a\phi |$ 这个泛函作用在任意 ket $|\psi\rangle$ 上得到 $\langle a\phi | \psi \rangle = \bar{a} \langle \phi | \psi \rangle$。这正是泛函 $\bar{a}\langle\phi|$ 的作用。因此，$J(a|\phi\rangle) = \bar{a} J(|\phi\rangle)$，这表明 $J$ 是一个反[线性同构](@entry_id:270529)。

### 算符、可观测量及其表示

物理可观测量，如能量、动量和位置，在量子力学中由[希尔伯特空间](@entry_id:261193)上的**线性算符 (linear operators)** 来表示。

#### 线性算符、有界性与无界性

一个线性算符 $\hat{A}$ 是一个从其**定义域 (domain)** $\mathcal{D}(\hat{A}) \subseteq \mathcal{H}$ 到 $\mathcal{H}$ 的映射，满足线性条件：
$$ \hat{A}(\alpha|\psi\rangle + \beta|\phi\rangle) = \alpha \hat{A}|\psi\rangle + \beta \hat{A}|\phi\rangle $$
对于所有 $|\psi\rangle, |\phi\rangle \in \mathcal{D}(\hat{A})$ 和 $\alpha, \beta \in \mathbb{C}$。对于许多重要的物理算符，定义域并非整个希尔伯特空间 $\mathcal{H}$，而只是其中的一个[稠密子空间](@entry_id:261392)。

算符可以根据其行为分为**有界 (bounded)** 和**无界 (unbounded)** 两类 [@problem_id:2765389]。
-   一个算符 $\hat{A}$ 是**有界的**，如果存在一个常数 $M  \infty$，使得对于其定义域中的所有 $|\psi\rangle$，都有 $||\hat{A}|\psi\rangle|| \le M |||\psi\rangle||$。有界算符不会将范数有限的向量映射到范数无限的向量。例如，在[量子化学](@entry_id:140193)计算中，将一个态投影到由有限个高斯[基函数](@entry_id:170178)张成的[子空间](@entry_id:150286)上的[投影算符](@entry_id:154142) $\hat{P}$ 就是有界的，其算符范数为1。
-   一个算符是**无界的**，如果不存在这样的有限常数 $M$。量子力学中大多[数基](@entry_id:634389)本的[可观测量](@entry_id:267133)，如位置算符 $\hat{\mathbf{r}}$、动量算符 $\hat{\mathbf{p}} = -i\hbar\nabla$ 和[动能算符](@entry_id:265633) $\hat{T} = -\frac{\hbar^2}{2m}\nabla^2$，都是无界算符。我们可以通过构造一系列[波函数](@entry_id:147440)（例如，越来越窄的[高斯波包](@entry_id:151158)）来表明，即使其范数保持为1，作用在其上的[动量算符](@entry_id:151743)所产生的新态的范数可以任意大。

#### 伴随算符与自伴算符

对于一个在[稠密子空间](@entry_id:261392)上定义的算符 $\hat{A}$，我们可以定义其**伴随算符 (adjoint operator)** $\hat{A}^\dagger$。它由以下关系唯一确定，对于所有 $|\psi\rangle \in \mathcal{D}(\hat{A})$ 和 $|\phi\rangle \in \mathcal{D}(\hat{A}^\dagger)$：
$$ \langle \phi | \hat{A} \psi \rangle = \langle \hat{A}^\dagger \phi | \psi \rangle $$
这个定义等价于矩阵元的表示形式 [@problem_id:2765389]：
$$ (\langle \phi | \hat{A} | \psi \rangle)^* = \langle \psi | \hat{A}^\dagger | \phi \rangle $$
注意，取伴随不仅涉及到算符本身，还涉及到 bra 和 ket 的交换以及对整个矩阵元取[复共轭](@entry_id:174690)。

代表物理可观测量（如能量、动量）的算符必须是**自伴的 (self-adjoint)**，这意味着 $\hat{A} = \hat{A}^\dagger$ 并且它们的定义域相同 $\mathcal{D}(\hat{A}) = \mathcal{D}(\hat{A}^\dagger)$。自伴算符的一个关键性质是它们的[本征值](@entry_id:154894)是实数，这与物理测量的结果是实数相符。

#### [外积](@entry_id:147029)

[狄拉克符号](@entry_id:154811)还允许我们方便地构造一类重要的算符。由一个 bra $\langle\psi|$ 和一个 ket $|\phi\rangle$ 构成的**[外积](@entry_id:147029) (outer product)** $|\phi\rangle\langle\psi|$ 是一个线性算符。它作用于任意一个 ket $|\chi\rangle$ 的方式如下 [@problem_id:2768452]：
$$ (|\phi\rangle\langle\psi|) |\chi\rangle = |\phi\rangle (\langle\psi|\chi\rangle) $$
由于 $\langle\psi|\chi\rangle$ 是一个复数（标量），所以这个算符的作用是将任意向量 $|\chi\rangle$ 变成一个与 $|\phi\rangle$ 成比例的新向量。特别地，如果 $|\phi\rangle$ 是一个归一化的向量，那么 $\hat{P} = |\phi\rangle\langle\phi|$ 就是一个**[投影算符](@entry_id:154142)**，它将任意[向量投影](@entry_id:147046)到由 $|\phi\rangle$ 张成的一维[子空间](@entry_id:150286)上。

### 谱理论与[恒等分解](@entry_id:197722)

自伴算符的**谱 (spectrum)**（即其[本征值](@entry_id:154894)的集合）包含了关于物理系统可测量值的全部信息。[谱理论](@entry_id:275351)为我们提供了系统地分析和使用这些信息的方法。

#### [离散谱](@entry_id:150970)与[恒等分解](@entry_id:197722)

我们首先考虑最简单的情况：一个自伴算符 $\hat{H}$（例如一个体系的[哈密顿量](@entry_id:172864)）拥有一个离散、非简并的[本征值](@entry_id:154894)谱 $\{E_n\}$ 和一套对应的标准正交本征矢 $\{|n\rangle\}$ [@problem_id:2625846]。

**完备性 (Completeness)** 意味着这套本征矢 $\{|n\rangle\}$ 构成了一个希尔伯特空间的**基底 (basis)**。任何一个态向量 $|\psi\rangle$ 都可以唯一地展开为它们的线性组合：$|\psi\rangle = \sum_n c_n |n\rangle$，其中展开系数 $c_n = \langle n | \psi \rangle$。将 $c_n$ 的表达式代回，我们得到：
$$ |\psi\rangle = \sum_n (\langle n | \psi \rangle) |n\rangle = \sum_n |n\rangle \langle n | \psi \rangle = \left( \sum_n |n\rangle \langle n | \right) |\psi\rangle $$
由于上式对任意 $|\psi\rangle$ 都成立，括号中的算符必定是**恒等算符 (identity operator)** $\hat{I}$。这就是**[恒等分解](@entry_id:197722) (resolution of the identity)**：
$$ \hat{I} = \sum_n |n\rangle \langle n | $$

这个关系极为强大。它可以用来导出算符的**谱分解 (spectral decomposition)**。例如，将 $\hat{H}$ 作用于上式右侧的任意一项 $|n\rangle\langle n|$：
$$ \hat{H} = \hat{H} \hat{I} = \hat{H} \sum_n |n\rangle \langle n | = \sum_n (\hat{H}|n\rangle) \langle n | = \sum_n E_n |n\rangle \langle n | $$
这个思想可以推广到任何关于 $\hat{H}$ 的（解析）函数 $f(\hat{H})$：
$$ f(\hat{H}) = \sum_n f(E_n) |n\rangle \langle n | $$
利用这个谱分解，计算一个任意态 $|\psi\rangle = \sum_n c_n|n\rangle$ 中 $f(\hat{H})$ 的[期望值](@entry_id:153208)就变得非常直接 [@problem_id:2625846]：
$$ \langle \psi | f(\hat{H}) | \psi \rangle = \sum_{m,n} \overline{c_m} c_n \langle m | f(\hat{H}) | n \rangle = \sum_{m,n} \overline{c_m} c_n f(E_n) \langle m | n \rangle = \sum_n |c_n|^2 f(E_n) $$
例如，对于算符函数 $f(\hat{H}) = \exp(-\beta\hat{H}) + \alpha\hat{H}^2$，其[期望值](@entry_id:153208)为 $\sum_n |c_n|^2 (\exp(-\beta E_n) + \alpha E_n^2)$。

#### 连续谱与严格基础

许多重要的算符，如位置和[动量算符](@entry_id:151743)，具有[连续谱](@entry_id:155477)。它们的“本征矢”并不能像[离散谱](@entry_id:150970)那样被归一化，也不属于原始的希尔伯特空间 $\mathcal{H}$。例如，位置算符 $\hat{x}$ 的本征矢 $|x\rangle$ 在位置表象中是狄拉克 $\delta$ 函数 $\delta(x'-x)$，它不是一个[平方可积函数](@entry_id:200316)。

为了给这些对象提供一个严格的数学地位，我们引入**[装备希尔伯特空间](@entry_id:141353) (rigged Hilbert space)** 或 **Gelfand 三元组 (Gelfand triple)** 的概念 [@problem_id:2768422]。这是一个由三个空间构成的嵌套结构：$\Phi \subset \mathcal{H} \subset \Phi^\times$。
-   $\mathcal{H}$ 是我们熟悉的[希尔伯特空间](@entry_id:261193) (例如 $L^2(\mathbb{R})$)。
-   $\Phi$ 是一个比 $\mathcal{H}$ “更小”的、由性质非常良好的“测试函数”（例如 Schwartz 空间 $\mathcal{S}(\mathbb{R})$）构成的[稠密子空间](@entry_id:261392)。
-   $\Phi^\times$ 是 $\Phi$ 的[反线性](@entry_id:268590)对偶空间，其元素是“[广义函数](@entry_id:182848)”或“缓增[分布](@entry_id:182848)”。

在这个框架中，像 $|x\rangle$ 这样的“本征矢”被严谨地定义为 $\Phi^\times$ 中的元素。它们对 $\Phi$ 中函数的作用被定义为函数值的评估，即 $\langle x | \varphi \rangle = \varphi(x)$。这样，离散情况下的求和就被积分所取代，[恒等分解](@entry_id:197722)和正交归一关系可以被严格地表述为：
$$ \hat{I} = \int dx \, |x\rangle\langle x| \quad (\text{在 } \Phi \text{ 上弱算符意义下成立}) $$
$$ \langle x | x' \rangle = \delta(x-x') \quad (\text{在分布意义下成立}) $$

更普遍地，**无界自伴算符的[谱定理](@entry_id:136620)** 将离散和[连续谱](@entry_id:155477)统一在一个框架下。该定理指出，对任意自伴算符 $\hat{A}$，存在一个唯一的**投影值测量 (Projection-Valued Measure, PVM)** $E$ [@problem_id:2768464] [@problem_id:2768459]。PVM 将实数轴 $\mathbb{R}$ 上的每个（波莱尔）[子集](@entry_id:261956) $\Delta$ 映射到一个[希尔伯特空间](@entry_id:261193)上的正交投影算符 $E(\Delta)$。这个算符 $E(\Delta)$ 投影到与测量结果落在 $\Delta$ 内相对应的态的[子空间](@entry_id:150286)上。

利用 PVM，算符 $\hat{A}$ 及其函数可以表示为积分形式：
$$ \hat{A} = \int_{\mathbb{R}} \lambda \, dE(\lambda), \quad f(\hat{A}) = \int_{\mathbb{R}} f(\lambda) \, dE(\lambda) $$
这个框架完美地统一了[离散谱](@entry_id:150970)和连续谱：
-   对于离散[本征值](@entry_id:154894) $\alpha$，对应的投影算符就是 $E(\{\alpha\})$，如果是非简并的，则 $E(\{\alpha\}) = |\alpha\rangle\langle\alpha|$。
-   对于[连续谱](@entry_id:155477)部分 $\sigma_c(\hat{A})$，对于任意单点集 $\{\lambda\}$，都有 $E(\{\lambda\}) = 0$。

因此，完整的[恒等分解](@entry_id:197722)可以写作 $\hat{I} = \sum_{\alpha \in \sigma_p(\hat{A})} E(\{\alpha\}) + E(\sigma_c(\hat{A}))$ [@problem_id:2768464]。

### 复合系统与[量子态](@entry_id:146142)的结构

#### 张量积

当一个系统由多个子系统组成时（例如，一个包含两个电子的分子），其总的[量子态空间](@entry_id:197873)是如何构建的？答案是**[张量积](@entry_id:140694) (tensor product)**。如果子系统 A 和 B 的希尔伯特空间分别是 $\mathcal{H}_A$ 和 $\mathcal{H}_B$，那么复合系统的[希尔伯特空间](@entry_id:261193)就是 $\mathcal{H} = \mathcal{H}_A \otimes \mathcal{H}_B$。

张量积空间的严格构造过程如下 [@problem_id:2896440]：
1.  首先构建**代数[张量积](@entry_id:140694)** $\mathcal{H}_A \otimes_{\text{alg}} \mathcal{H}_B$，它由形如 $|a\rangle \otimes |b\rangle$（其中 $|a\rangle \in \mathcal{H}_A, |b\rangle \in \mathcal{H}_B$）的**简单张量**的有限[线性组合](@entry_id:154743)构成。
2.  在这个代数张量积空间上定义[内积](@entry_id:158127)。对于简单张量，[内积](@entry_id:158127)定义为各子系统[内积](@entry_id:158127)的乘积：
    $$ \langle a_1 \otimes b_1 | a_2 \otimes b_2 \rangle := \langle a_1 | a_2 \rangle_A \langle b_1 | b_2 \rangle_B $$
    然后通过[半双线性](@entry_id:188042)将此定义扩展到所有有限[线性组合](@entry_id:154743)上。
3.  一般情况下，如果 $\mathcal{H}_A$ 和 $\mathcal{H}_B$ 都是无限维的，那么代数[张量积](@entry_id:140694)空间是不完备的。因此，最后一步是对这个前希尔伯特空间进行**完备化 (completion)**，得到的才是最终的[希尔伯特张量](@entry_id:750343)积空间 $\mathcal{H}_A \otimes \mathcal{H}_B$。

#### 纯态与[混合态](@entry_id:141568)

到目前为止，我们主要讨论了由单个 ket 向量描述的**纯态 (pure states)**。然而，更一般的情况是，我们可能对系统的知识不完整，或者[系统与环境](@entry_id:142270)发生了纠缠。这种状态被称为**[混合态](@entry_id:141568) (mixed states)**，需要用**[密度算符](@entry_id:138151) (density operator)** $\rho$ 来描述。

一个算符 $\rho$ 若要成为一个合法的[密度算符](@entry_id:138151)，必须满足以下三个条件 [@problem_id:2768476]：
1.  **自伴性**：$\rho = \rho^\dagger$。
2.  **[半正定性](@entry_id:147720)**：对于任意态 $|\phi\rangle$，$\langle \phi | \rho | \phi \rangle \ge 0$。这意味着 $\rho$ 的[本征值](@entry_id:154894)都是非负的。
3.  **单位迹**：$\mathrm{Tr}(\rho) = 1$。迹 $(\mathrm{Tr})$ 是算符对角元之和。

-   如果一个态是纯态，可以由归一化的 ket $|\psi\rangle$ 描述，那么其[密度算符](@entry_id:138151)就是投影算符 $\rho = |\psi\rangle\langle\psi|$。
-   如果一个态是混合态，它不能表示为单个 ket 的[外积](@entry_id:147029)，而是多个[纯态](@entry_id:141688)的统计混合，例如 $\rho = \sum_i p_i |\psi_i\rangle\langle\psi_i|$，其中 $p_i$ 是处于[纯态](@entry_id:141688) $|\psi_i\rangle$ 的概率（$p_i > 0, \sum_i p_i = 1$）。

我们可以用 $\rho$ 的**纯度 (purity)** $\mathrm{Tr}(\rho^2)$ 来区分纯态和[混合态](@entry_id:141568)。
-   对于[纯态](@entry_id:141688) $\rho = |\psi\rangle\langle\psi|$，我们有 $\rho^2 = (|\psi\rangle\langle\psi|)(|\psi\rangle\langle\psi|) = |\psi\rangle\langle\psi|\psi\rangle\langle\psi| = |\psi\rangle\langle\psi| = \rho$。因此 $\mathrm{Tr}(\rho^2) = \mathrm{Tr}(\rho) = 1$。
-   对于混合态，可以证明 $\mathrm{Tr}(\rho^2)  1$。例如，对于一个完全混合的[二能级系统](@entry_id:138452)态 $\rho_B = \frac{1}{2}|\alpha\rangle\langle\alpha| + \frac{1}{2}|\beta\rangle\langle\beta| = \frac{1}{2}\hat{I}$，其纯度为 $\mathrm{Tr}(\rho_B^2) = \mathrm{Tr}(\frac{1}{4}\hat{I}) = \frac{1}{4}\mathrm{Tr}(\hat{I}) = \frac{1}{4} \times 2 = \frac{1}{2}$ [@problem_id:2768476]。

所有[密度算符](@entry_id:138151)构成的集合 $\mathcal{S}$ 具有**凸性 (convex)** 结构。这意味着，任意两个[密度算符](@entry_id:138151) $\sigma$ 和 $\tau$ 的[凸组合](@entry_id:635830) $\rho = p\sigma + (1-p)\tau$（其中 $0 \le p \le 1$）仍然是一个[密度算符](@entry_id:138151)。在这个凸集中，**极点 (extreme points)** 正是所有的纯态。任何[混合态](@entry_id:141568)都可以表示为纯态的凸组合，但纯态不能表示为两个不同状态的[凸组合](@entry_id:635830) [@problem_id:2768476]。

### 再论测量假设

现在，我们可以用 PVM 的语言来更普适和严谨地重述[量子测量](@entry_id:272490)的基本假设。

对于一个由态 $|\psi\rangle$ 描述的系统，测量一个由自伴算符 $\hat{A}$ 代表的物理量：

1.  **[广义玻恩](@entry_id:182759)规则 (Generalized Born's Rule)**：测量结果落在一个实数集合 $\Delta$ 内的概率为 [@problem_id:2768459]：
    $$ P(\Delta) = \langle \psi | E(\Delta) | \psi \rangle = ||E(\Delta)|\psi\rangle||^2 $$
    其中 $E(\Delta)$ 是与 $\hat{A}$ 和集合 $\Delta$ 相关联的[投影算符](@entry_id:154142)。

2.  **投影假设 (Projection Postulate)**：如果测量结果确实落在 $\Delta$ 内（且概率不为零），那么测量后系统的状态会“坍缩”到新的归一化状态 [@problem_id:2768459]：
    $$ |\psi_{\text{post}}\rangle = \frac{E(\Delta)|\psi\rangle}{||E(\Delta)|\psi\rangle||} $$
    这通常被称为 **von Neumann-Lüders 规则**。

这个普适的规则包含了我们熟悉的所有特例。例如，如果 $\hat{A}$ 具有[离散谱](@entry_id:150970) $\{a_i\}$，那么测量结果为特定值 $a_i$ 的概率就是 $P(\{a_i\}) = \langle\psi|E(\{a_i\})|\psi\rangle = \langle\psi|P_i|\psi\rangle = |\langle a_i|\psi\rangle|^2$，其中 $P_i = |a_i\rangle\langle a_i|$ 是对应非简并本征矢的投影。

特别需要注意的是在**简并 (degeneracy)** 情况下的测量。假设一个[本征值](@entry_id:154894) $a$ 对应一个多维的本征[子空间](@entry_id:150286) $\mathcal{E}$，其[投影算符](@entry_id:154142)为 $P_{\mathcal{E}}$。如果测量结果被确定为 $a$，那么根据 Lüders 规则，末态是 $|\psi_{\text{post}}\rangle = P_{\mathcal{E}}|\psi\rangle / ||P_{\mathcal{E}}|\psi\rangle||$。这表示初始态 $|\psi\rangle$ 被投影到它在[子空间](@entry_id:150286) $\mathcal{E}$ 中的分量上。这个过程并不会随机选择 $\mathcal{E}$ 中的一个本征矢，也不会破坏 $|\psi\rangle$ 在 $\mathcal{E}$ 内部的[相干叠加](@entry_id:170209)。例如，如果 $P_{\mathcal{E}}|\psi\rangle = c_1|\phi_1\rangle + c_2|\phi_2\rangle$（其中 $|\phi_1\rangle, |\phi_2\rangle$ 是 $\mathcal{E}$ 的一组基），那么末态就是这个叠加态的归一化，保留了 $c_1$ 和 $c_2$ 之间的[相对相位](@entry_id:148120)和振幅关系 [@problem_id:2768459]。