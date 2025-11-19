## 引言
量子力学是描述微观物质世界的基石理论，其预测的现象，如[量子隧穿](@entry_id:142867)和纠缠，从根本上挑战了我们的经典直觉。然而，要超越对这些奇特现象的定性描述，我们需要一个严谨的数学框架来精确定义量子世界的规则。本文旨在系统性地建立这一框架，即量子力学的基本公设，并深入探讨其中最具革命性的概念——[叠加原理](@entry_id:144649)。尽管早期量子论成功解释了部分实验，但一个自洽且普适的理论体系直至公理化方法的建立才得以完善。本文正是要填补从实验现象到抽象数学形式主义之间的认知鸿沟。

读者将通过本文的学习，获得对[量子力学形式体系](@entry_id:198016)的全面理解。第一章“原理与机制”将逐一介绍量子力学的核心公设，从态矢量、[可观测量](@entry_id:267133)到测量和动力学演化，并重点剖析叠加原理的内涵。第二章“应用与交叉学科联系”将展示这些抽象原理如何在化学、物理和信息科学等领域中转化为强大的解释和预测工具。最后，第三章“动手实践”将通过具体的计算问题，帮助读者将理论知识内化为解决实际问题的能力。通过这一结构化的学习路径，我们将揭示[量子力学公设](@entry_id:155183)不仅是数学构造，更是理解和操控微观世界的蓝图。

## 原理与机制

继前一章对量子力学历史背景和基本现象的介绍之后，本章将深入探讨其数学形式主义的核心——一系列定义了量子世界规则的基本原理或公设。这些公设不仅为我们在原子和分子尺度上遇到的奇特现象提供了严谨的数学描述，而且构成了整个[量子化学](@entry_id:140193)和物理学的理论基石。我们将系统地阐述这些原理，并揭示它们之间深刻的内在联系与机制。

### 量子力学的公理化框架

从经验事实出发，例如双路径[散射实验](@entry_id:173304)中的干涉现象、可重复的制备-测量统计规律、以及复合系统中的[非局域关联](@entry_id:180194)，物理学家构建了一套数学框架来描述非[相对论量子力学](@entry_id:148643)。这个框架通过四个核心要素——**状态（states）**、**[可观测量](@entry_id:267133)（observables）**、**测量（measurements）**和**动力学（dynamics）**——将物理现实映射到精确的数学对象上。一个完备且自洽的量子力学表述必须正确地定义这些要素及其相互关系。我们将遵循这一逻辑结构，逐一展开量子力学的基本公设 [@problem_id:2661207]。

### 量子系统的状态

量子力学的第一个基本问题是：如何描述一个物理系统的状态？[经典物理学](@entry_id:150394)中，一个粒子的状态由其确定的位置和动量所定义。然而，量子世界要求一种全新的、基于概率的描述方式。

#### 态矢量与[希尔伯特空间](@entry_id:261193)

**第一公设（状态空间）：**一个孤立量子系统的状态由一个复可分**[希尔伯特空间](@entry_id:261193)（complex separable Hilbert space）** $\mathcal{H}$ 中的一个矢量来完全描述，这个矢量被称为**态矢量（state vector）**或**酮矢量（ket vector）**，记作 $|\psi\rangle$。

希尔伯特空间是一个配备了**[内积](@entry_id:158127)（inner product）**的完备[复向量空间](@entry_id:264355)。[内积](@entry_id:158127)将任意一对矢量 $|\phi\rangle$ 和 $|\psi\rangle$ 映射为一个复数，记作 $\langle\phi|\psi\rangle$。在物理学中，根据狄拉克（Dirac）的**[狄拉克符号](@entry_id:154811)（bra-ket notation）**，[内积](@entry_id:158127)具有以下关键性质 [@problem_id:2661161]：

1.  **[共轭对称性](@entry_id:144131)（Conjugate symmetry）：** $\langle\phi|\psi\rangle = \langle\psi|\phi\rangle^*$，其中 $*$ 表示复共轭。

2.  **对第二个参数的线性（Linearity in the ket）：** 对于任意复数 $a, b \in \mathbb{C}$，有 $\langle\phi | (a|\psi_1\rangle + b|\psi_2\rangle) \rangle = a\langle\phi|\psi_1\rangle + b\langle\phi|\psi_2\rangle$。结合[共轭对称性](@entry_id:144131)，这意味着[内积](@entry_id:158127)对第一个参数（** bra 矢量** $\langle\phi|$）是**[共轭线性](@entry_id:268590)（conjugate linear）**的：$\langle (a|\phi_1\rangle + b|\phi_2\rangle) | \psi \rangle = a^*\langle\phi_1|\psi\rangle + b^*\langle\phi_2|\psi\rangle$。这种综合性质被称为**[半双线性](@entry_id:188042)（sesquilinearity）**。

3.  **正定性（Positive-definiteness）：** 对于任意非[零矢量](@entry_id:155273) $|\psi\rangle \neq \mathbf{0}$，其与自身的[内积](@entry_id:158127)是严格正实数，即 $\langle\psi|\psi\rangle > 0$。且 $\langle\psi|\psi\rangle=0$ 当且仅当 $|\psi\rangle$ 是[零矢量](@entry_id:155273)。

这个[正定性](@entry_id:149643)允许我们定义态矢量的**范数（norm）**：$\|\psi\| = \sqrt{\langle\psi|\psi\rangle}$。在量子力学中，态矢量通常被归一化至单位范数，即 $\langle\psi|\psi\rangle = 1$。正如我们将看到的，这与[概率的解释](@entry_id:200448)密切相关。

#### 作为射[线束](@entry_id:167936)的状态：[全局相位](@entry_id:147947)的不可观测性

尽管我们用一个归一化的矢量 $|\psi\rangle$ 来代表一个[量子态](@entry_id:146142)，但更精确的说法是，一个纯[量子态](@entry_id:146142)对应于[希尔伯特空间](@entry_id:261193)中的一个**射[线束](@entry_id:167936)（ray）**。一个射[线束](@entry_id:167936)是由一个非[零矢量](@entry_id:155273) $|\psi\rangle$ 张成的一维[子空间](@entry_id:150286)，即集合 $\{\lambda |\psi\rangle : \lambda \in \mathbb{C}, \lambda \neq 0\}$。这意味着，对于任意非零复数 $c$，矢量 $|\psi\rangle$ 和 $c|\psi\rangle$ 代表同一个物理状态。当我们处理归一化矢量时，这等价于说 $|\psi\rangle$ 和 $e^{i\phi}|\psi\rangle$（其中 $\phi$ 是任意实数，称为**[全局相位](@entry_id:147947)（global phase）**）代表完全相同的物理状态。

为什么[全局相位](@entry_id:147947)是不可观测的？这个结论可以从量子力学的其他公设中得到坚实的论证 [@problem_id:2661194]：

1.  **从测量公设看：** 所有可观测的物理量最终都归结为测量概率。根据**[玻恩定则](@entry_id:154470)（Born's rule）**，当系统处于状态 $|\psi\rangle$ 时，测量某个可观测量得到结果 $a_k$ 的概率为 $p(a_k) = |\langle a_k|\psi\rangle|^2$，其中 $|a_k\rangle$ 是与结果 $a_k$ 对应的[本征态](@entry_id:149904)。如果我们将态矢量乘以一个[全局相位](@entry_id:147947) $e^{i\phi}$，新的概率为 $p'(a_k) = |\langle a_k|e^{i\phi}|\psi\rangle|^2 = |e^{i\phi}\langle a_k|\psi\rangle|^2 = |e^{i\phi}|^2 |\langle a_k|\psi\rangle|^2 = 1 \cdot p(a_k) = p(a_k)$。由于所有测量结果的概率都保持不变，这两个态矢量在操作上是无法区分的。

2.  **从[密度算符](@entry_id:138151)看：** 一个纯态 $|\psi\rangle$ 也可以用一个**[密度算符](@entry_id:138151)（density operator）** $\rho = |\psi\rangle\langle\psi|$ 来描述。这个算符包含了关于该状态的所有统计信息。对于态矢量 $e^{i\phi}|\psi\rangle$，其对应的[密度算符](@entry_id:138151)为 $\rho' = (e^{i\phi}|\psi\rangle)(\langle\psi|e^{-i\phi}) = |\psi\rangle\langle\psi| = \rho$。由于两个态矢量定义了完全相同的[密度算符](@entry_id:138151)，它们必定代表同一个物理状态。

3.  **从动力学演化看：** 一个孤立系统的演化由薛定谔方程 $i\hbar\frac{d}{dt}|\psi(t)\rangle = \hat{H}|\psi(t)\rangle$ 描述。由于该方程是线性的，如果 $|\psi(t)\rangle$ 是一个解，那么 $e^{i\phi}|\psi(t)\rangle$（对于一个不依赖于时间的 $\phi$）也必然是一个解。这意味着，如果两个态矢量在初始时刻处于同一射[线束](@entry_id:167936)上，它们在随后的任何时刻都将始终处于同一射[线束](@entry_id:167936)上，从而在所有时刻都给出相同的测量统计结果。

因此，将物理状态等同于希尔伯特空间中的射[线束](@entry_id:167936)，是量子力学数学结构中一个深刻且自洽的组成部分。

### [叠加原理](@entry_id:144649)

希尔伯特空间是一个[向量空间](@entry_id:151108)，这一事实直接引出了量子力学中最具特色和革命性的概念之一：**[叠加原理](@entry_id:144649)（superposition principle）**。

#### [量子力学的线性](@entry_id:146991)结构

**第二公设（叠加原理）：** 如果 $|\psi_1\rangle$ 和 $|\psi_2\rangle$ 是一个量子系统可能的状态，那么它们的任意线性组合 $|\Psi\rangle = c_1|\psi_1\rangle + c_2|\psi_2\rangle$（其中 $c_1, c_2 \in \mathbb{C}$ 且不全为零）也代表了该系统的一个可能物理状态。

这个原理从根本上区别于经典物理。一个经典物体不可能同时处于两个不同的位置，但一个量子粒子，如电子，却可以处于多个位置的**[相干叠加](@entry_id:170209)态（coherent superposition）**。这种线性叠加的能力是解释所有波动和干涉现象的数学基础。

事实上，正是实验上观测到的非经典干涉现象，迫使我们必须采用一个线性的、复数的[向量空间](@entry_id:151108)来描述[量子态](@entry_id:146142) [@problem_id:2661242]。在一个双缝干涉实验中，当粒子可以走路径1（状态 $|\psi_1\rangle$）或路径2（状态 $|\psi_2\rangle$）时，最终在探测屏上某点观测到粒子的概率 $P_{12}$ 并不等于只开放路径1的概率 $P_1$ 和只开放路径2的概率 $P_2$ 之和，即 $P_{12} \neq P_1 + P_2$。为了解释这一点，我们必须假设存在一种比概率更基本的量——**[概率幅](@entry_id:150609)（probability amplitude）**，也就是态矢量。当两个路径都开放时，总的概率幅是两个路径概率幅的**和**：$|\psi_{12}\rangle = |\psi_1\rangle + |\psi_2\rangle$。而概率由[概率幅](@entry_id:150609)的模平方给出：$P_{12} = |\langle x|\psi_{12}\rangle|^2 = |\langle x|\psi_1\rangle + \langle x|\psi_2\rangle|^2 = P_1 + P_2 + 2\text{Re}(\langle x|\psi_1\rangle^*\langle x|\psi_2\rangle)$。正是这个**干涉项（interference term）**导致了与经典概率论的偏离。能够对态矢量进行加法运算，是[向量空间](@entry_id:151108)（即线性结构）的定义性特征。而干涉项中相位的存在，则要求这些矢量是在[复数域](@entry_id:153768) $\mathbb{C}$ 上定义的。

#### 相干叠加与统计混合

理解[叠加原理](@entry_id:144649)的关键在于区分**[相干叠加](@entry_id:170209)（coherent superposition）**和**统计混合（statistical mixture）**。这是一个微妙但至关重要的区别 [@problem_id:2661174]。

假设一个系统可以处于两个正交归一的本征态 $|\phi\rangle$ 和 $|\psi\rangle$。

-   一个**[相干叠加](@entry_id:170209)态**可以写作 $|\Phi\rangle = \alpha|\phi\rangle + \beta|\psi\rangle$，其中 $|\alpha|^2 + |\beta|^2 = 1$。这是一个**纯态（pure state）**，系统“同时”处于 $|\phi\rangle$ 和 $|\psi\rangle$ 的一种确定组合中。其[密度算符](@entry_id:138151)为 $\rho_{\Phi} = |\Phi\rangle\langle\Phi| = |\alpha|^2|\phi\rangle\langle\phi| + |\beta|^2|\psi\rangle\langle\psi| + \alpha\beta^*|\phi\rangle\langle\psi| + \alpha^*\beta|\psi\rangle\langle\phi|$。注意其中的**非对角项（off-diagonal terms）**或**相干项（coherences）**，如 $\alpha\beta^*|\phi\rangle\langle\psi|$。

-   一个**统计[混合态](@entry_id:141568)**描述的是一个系综（ensemble），其中一部分系统处于状态 $|\phi\rangle$（概率为 $|\alpha|^2$），另一部分处于状态 $|\psi\rangle$（概率为 $|\beta|^2$）。这是一个**[混合态](@entry_id:141568)（mixed state）**，代表了我们对系统真实状态的经典无知。其[密度算符](@entry_id:138151)为 $\rho_{\text{mix}} = |\alpha|^2|\phi\rangle\langle\phi| + |\beta|^2|\psi\rangle\langle\psi|$。这个[密度算符](@entry_id:138151)是**对角的（diagonal）**，没有非对角项。

这两种状态在物理上是截然不同的。虽然对于任何在基 $\{|\phi\rangle, |\psi\rangle\}$ 下对角的 observable $\hat{A}$，它们的测量[期望值](@entry_id:153208) $\langle\hat{A}\rangle = \text{Tr}(\rho \hat{A})$ 是相同的（都等于 $|\alpha|^2 A_{\phi\phi} + |\beta|^2 A_{\psi\psi}$），但对于非对角的 observable，结果就会不同。例如，测量投影到 $|+\rangle = \frac{1}{\sqrt{2}}(|\phi\rangle+|\psi\rangle)$ 上的概率，对于相干叠加态是 $P(+)_\Phi = |\langle+|\Phi\rangle|^2 = \frac{1}{2}|\alpha+\beta|^2$，而对于统计混合态则是 $P(+)_\text{mix} = \text{Tr}(\rho_\text{mix}|+\rangle\langle+|) = \frac{1}{2}(|\alpha|^2+|\beta|^2) = \frac{1}{2}$。这两个结果通常是不同的。

此外，在动力学演化下，两者的区别更加明显。如果 $|\phi\rangle$ 和 $|\psi\rangle$ 是[哈密顿量](@entry_id:172864) $\hat{H}$ 的能量本征态且能量不同 ($E_\phi \neq E_\psi$)，那么[混合态](@entry_id:141568)的[密度算符](@entry_id:138151) $\rho_{\text{mix}}$ 是不随[时间演化](@entry_id:153943)的。而[相干叠加](@entry_id:170209)态 $|\Phi(t)\rangle = \alpha e^{-iE_\phi t/\hbar}|\phi\rangle + \beta e^{-iE_\psi t/\hbar}|\psi\rangle$ 中的[相对相位](@entry_id:148120)会随时间演化，导致非对角 observable 的[期望值](@entry_id:153208)会随时间[振荡](@entry_id:267781)，这种现象被称为**[量子拍](@entry_id:155286)（quantum beats）**。相干项的存在是所有[量子干涉](@entry_id:139127)、纠缠和[量子计算](@entry_id:142712)的根源。

### [可观测量](@entry_id:267133)与测量

**第三公设（可观测量）：** 每一个[物理可观测量](@entry_id:154692)（如能量、动量、位置、自旋）都由一个作用在希尔伯特空间 $\mathcal{H}$ 上的**自伴算符（self-adjoint operator）**（在物理学文献中通常称为**厄米算符（Hermitian operator）**）来表示。

#### [可观测量](@entry_id:267133)作为自伴算符

为什么[可观测量](@entry_id:267133)必须由自伴算符表示？这背后有深刻的物理和数学原因 [@problem_id:2661203]。一个算符 $\hat{A}$ 被称为自伴的，如果它等于其自身的[厄米共轭](@entry_id:191215) $\hat{A}^\dagger$，即 $\hat{A} = \hat{A}^\dagger$（并满足一定的定义域条件）。这导致了两个关键的物理后果：

1.  **实数测量值：** 自伴算符的[本征值](@entry_id:154894)必然是实数。由于测量的结果就是算符的[本征值](@entry_id:154894)之一，这保证了我们的测量读数（如能量、位置）总是实数，与实验观测相符。

2.  **完备的本征基：** **谱定理（Spectral Theorem）**保证了任何自伴算符都存在一个对应的**投影值测量（Projection-Valued Measure, PVM）**。对于有[离散谱](@entry_id:150970)的算符，这意味着其本征矢量构成一个完备的正交基。这使得任何态矢量都可以展开为该 observable 的本征态的[线性组合](@entry_id:154743)，为概率解释提供了基础。对于具有连续谱的算符（如位置和动量），谱定理提供了更广义的框架，确保了与[实轴](@entry_id:148276)上的[概率分布](@entry_id:146404)的严格联系。

3.  **[幺正演化](@entry_id:145020)的生成元：** 根据**[斯通定理](@entry_id:262301)（Stone's Theorem）**，任何一个连续的单参数幺正群 $U(t)$（代表一种[连续对称性](@entry_id:137257)变换，如[时间演化](@entry_id:153943)或空间平移）都可以写成 $U(t) = \exp(-i t \hat{A})$ 的形式，其中 $\hat{A}$ 是一个自伴算符，被称为该幺正群的**生成元（generator）**。例如，[哈密顿量](@entry_id:172864) $\hat{H}$ 是时间演化的生成元，[动量算符](@entry_id:151743) $\hat{p}$ 是空间平移的生成元。因此，要求 observable 是自伴的，也保证了它们可以作为物理[变换的生成元](@entry_id:172031)，这与量子力学的动力学和对称性结构保持了一致。

仅仅要求算符是**对称的（symmetric）**（即对于其定义域中的所有矢量，$\langle\phi|\hat{A}\psi\rangle = \langle\hat{A}\phi|\psi\rangle$）是不够的。对称算符不一定有唯一的[谱分解](@entry_id:173707)，从而无法唯一地定义一个物理可观测量。自伴是一个更强的条件，它保证了物理诠释的唯一性和完备性。

#### 测量过程与状态坍缩

**第四公设（测量与概率）：** 当对处于归一化状态 $|\psi\rangle$ 的系统测量[可观测量](@entry_id:267133) $\hat{A}$ 时：
(a) 测量的结果必然是 $\hat{A}$ 的一个[本征值](@entry_id:154894) $a_n$。
(b) 测量得到特定非简并[本征值](@entry_id:154894) $a_n$ 的概率由**[玻恩定则](@entry_id:154470)**给出：$P(a_n) = |\langle a_n|\psi\rangle|^2$，其中 $|a_n\rangle$ 是对应于 $a_n$ 的归一化本征态。$\langle a_n|\psi\rangle$ 被称为**跃迁振幅（transition amplitude）**。
(c) 如果测量结果是 $a_n$，那么在测量之后瞬间，系统的状态将**坍缩（collapse）**到对应的[本征态](@entry_id:149904) $|a_n\rangle$。这个过程也被称为**投影（projection）**。

让我们通过一个例子来阐明这个过程 [@problem_id:2467272]。假设一个系统的初始状态是[能量本征态](@entry_id:152154) $|\phi_1\rangle$ 和 $|\phi_2\rangle$ 的一个叠加态：$|\Psi\rangle = c_1|\phi_1\rangle + c_2|\phi_2\rangle$，且 $|c_1|^2+|c_2|^2=1$。我们测量系统的能量（对应的算符是[哈密顿量](@entry_id:172864) $\hat{H}$），并得到了结果 $E_1$。

1.  **概率：** 得到结果 $E_1$ 的概率是 $P(E_1) = |\langle\phi_1|\Psi\rangle|^2 = |\langle\phi_1|(c_1|\phi_1\rangle + c_2|\phi_2\rangle)|^2 = |c_1|^2$。

2.  **状态坍缩：** 根据[投影公设](@entry_id:145685)，[测量后状态](@entry_id:148034)坍缩到与 $E_1$ 对应的[本征态](@entry_id:149904)。形式上，我们将[投影算符](@entry_id:154142) $\hat{P}_1 = |\phi_1\rangle\langle\phi_1|$ 作用于初始状态，得到未归一化的末态：
    $|\Psi'\rangle_{\text{un}} = \hat{P}_1|\Psi\rangle = |\phi_1\rangle\langle\phi_1|(c_1|\phi_1\rangle + c_2|\phi_2\rangle) = c_1|\phi_1\rangle$。

3.  **归一化：** 最后，我们将这个末态归一化。其范数为 $\||\Psi'\rangle_{\text{un}}\| = \sqrt{\langle c_1\phi_1|c_1\phi_1\rangle} = \sqrt{|c_1|^2} = |c_1|$。因此，归一化后的后测量状态为：
    $|\Psi'\rangle = \frac{c_1|\phi_1\rangle}{|c_1|}$。

这个最终状态保留了原始叠加系数 $c_1$ 的相位信息，这在需要考虑后续演化或测量的序列实验中至关重要。

**第五公设（动力学演化）：** 一个孤立量子系统的状态随时间的演化由**薛定谔方程（Schrödinger equation）**描述：
$i\hbar\frac{d}{dt}|\psi(t)\rangle = \hat{H}|\psi(t)\rangle$
其中 $\hat{H}$ 是系统的[哈密顿量](@entry_id:172864)算符。对于不依赖时间的[哈密顿量](@entry_id:172864)，其形式解为 $|\psi(t)\rangle = U(t)|\psi(0)\rangle$，其中 $U(t) = \exp(-i\hat{H}t/\hbar)$ 是一个**幺正算符（unitary operator）**。[幺正演化](@entry_id:145020)保持了态矢量的范数，从而保证了总[概率守恒](@entry_id:149166)。

### [非对易性](@entry_id:153545)的后果

#### 不[相容可观测量](@entry_id:151766)与不确定性原理

在经典物理中，所有[可观测量](@entry_id:267133)都可以被同时精确地测量。但在量子力学中，情况并非如此。两个可观测量 $\hat{A}$ 和 $\hat{B}$ 是否可以同时具有确定的值，取决于它们的算符是否**对易（commute）**。两个算符的**对易子（commutator）**定义为 $[\hat{A}, \hat{B}] = \hat{A}\hat{B} - \hat{B}\hat{A}$。

-   如果 $[\hat{A}, \hat{B}] = 0$，则 $\hat{A}$ 和 $\hat{B}$ 是**相容的（compatible）**。存在一个共同的本征基，使得系统可以同时处于 $\hat{A}$ 和 $\hat{B}$ 的本征态上，即它们的值可以被同时精确确定。
-   如果 $[\hat{A}, \hat{B}] \neq 0$，则 $\hat{A}$ 和 $\hat{B}$ 是**不相容的（incompatible）**。不可能制备一个系统，使其同时是 $\hat{A}$ 和 $\hat{B}$ 的[本征态](@entry_id:149904)。

这种不相容性被**海森堡不确定性原理（Heisenberg uncertainty principle）**定量地表达。其更普适的形式，即**罗伯逊-薛定谔[不确定性关系](@entry_id:186128)（Robertson-Schrödinger uncertainty relation）**，给出了在任意状态 $|\psi\rangle$ 下，两个[可观测量](@entry_id:267133)标准差 $(\Delta\hat{A})$ 和 $(\Delta\hat{B})$ 乘积的下限：
$(\Delta\hat{A})^2 (\Delta\hat{B})^2 \ge \left(\frac{1}{2i}\langle[\hat{A},\hat{B}]\rangle\right)^2 + \left(\frac{1}{2}\langle\{\hat{A},\hat{B}\}\rangle - \langle\hat{A}\rangle\langle\hat{B}\rangle\right)^2
一个更简单常用的形式是：
$\Delta\hat{A}\,\Delta\hat{B} \ge \frac{1}{2} |\langle[\hat{A},\hat{B}]\rangle|$

以自旋-1/2系统为例，沿x, y, z方向的自旋分量由泡利矩阵 $\sigma_x, \sigma_y, \sigma_z$ 表示。通过直接计算矩阵乘法，可以得到它们的对易关系，例如 [@problem_id:2661166]：
$$[\sigma_x, \sigma_y] = \sigma_x\sigma_y - \sigma_y\sigma_x = \begin{pmatrix} i  0 \\ 0  -i \end{pmatrix} - \begin{pmatrix} -i  0 \\ 0  i \end{pmatrix} = \begin{pmatrix} 2i  0 \\ 0  -2i \end{pmatrix} = 2i\sigma_z$$
由于 $[\sigma_x, \sigma_y] \neq 0$，$\sigma_x$ 和 $\sigma_y$ 是不相容的。如果我们把系统制备在 $\sigma_z$ 的 $+1$ 本征态 $|+z\rangle$ 上，那么不确定性乘积的下限为：
$\Delta\sigma_x\,\Delta\sigma_y \ge \frac{1}{2} |\langle+z|[\sigma_x,\sigma_y]|+z\rangle| = \frac{1}{2} |\langle+z|2i\sigma_z|+z\rangle| = \frac{1}{2} |2i \langle+z|\sigma_z|+z\rangle| = \frac{1}{2} |2i \cdot 1| = 1$
这意味着，即使我们对 z 方向的自旋有完全确定的知识 ($\Delta\sigma_z=0$)，对 x 和 y 方向自旋的知识也存在一个不可逾越的内在限制。任何减小 $\Delta\sigma_x$ 的尝试都必然以增大 $\Delta\sigma_y$ 为代价，反之亦然。

### 关于叠加原理的高阶主题

叠加原理虽然普适，但在某些情况下会受到限制，或者其后果会因与环境的相互作用而变得隐蔽。

#### 超选择定则：对叠加的限制

尽管叠加原理是量子力学的核心，但我们从未在宏观世界中观察到像“一个带 $+e$ 电荷的质子和一个不带电的中子的叠加态”这样的状态。**超选择定则（superselection rule）**正是为了解释这种现象而引入的概念 [@problem_id:2661162]。

当一个量子系统中存在一个所有物理可观测量都与之对易的守恒量（如电荷、重子数、或粒子数 $N$）时，就会出现超选择定则。如果所有可观测量 $\hat{O}$ 和所有幺正演化 $\hat{U}$ 都满足 $[\hat{O}, N]=0$ 和 $[\hat{U}, N]=0$，那么该守恒量 $N$ 就定义了一个超选择规则。

其核心后果是，任何处于不同 $N$ 本征值（例如，$n_1$ 和 $n_2$）的本征态 $|\phi_1\rangle$ 和 $|\phi_2\rangle$ 之间的相干叠加，例如 $|\Psi\rangle = \alpha|\phi_1\rangle + \beta|\phi_2\rangle$，在所有允许的物理测量下，都表现得和一个统计混合态 $\rho_{\text{mix}} = |\alpha|^2|\phi_1\rangle\langle\phi_1| + |\beta|^2|\phi_2\rangle\langle\phi_2|$ 完全一样。这是因为任何允许的 observable $\hat{O}$ 的矩阵元 $\langle\phi_1|\hat{O}|\phi_2\rangle$ 都必然为零。因此，叠加态中的相对相位是不可观测的，相干性无法被探测到。

重要的是，超选择定则**不禁止**在同一个守恒量扇区内部的叠加。例如，在单粒子数扇区 $\mathcal{H}_1$ 内，形成两个不同单粒子态的叠加是完全允许的，并且其相干效应是可以被观测到的。超选择定则仅仅隔离了不同的守恒量扇区，使得它们之间的相干性变得不可见。

#### 退相干：经典性的涌现

超选择定则解释了为何某些基本守恒量之间没有相干性，但它没有完全解释我们日常经验中的经典世界——为何一个宏观物体（如薛定谔的猫）不会处于“死”和“活”的叠加态？现代量子理论对这个问题的主流解释是**环境诱导退相干（environment-induced decoherence）** [@problem_id:2661167]。

这个理论的核心思想是，任何宏观系统都不可避免地与周围庞大的环境（如空气分子、光子等）发生相互作用。一个初始处于相干叠加态的系统 $S$，如 $|\Psi_S\rangle = a|0\rangle + b|1\rangle$，会通过幺正演化与环境 $E$ 纠缠在一起。例如，一个初始的乘积态 $(a|0\rangle+b|1\rangle)\otimes|E_0\rangle$ 会演化为一个纠缠态：
$|\Psi_{SE}\rangle = a|0\rangle\otimes|E_0^0\rangle + b|1\rangle\otimes|E_0^1\rangle$
这里，系统的状态 $|0\rangle$ 和 $|1\rangle$ 分别与环境的不同状态 $|E_0^0\rangle$ 和 $|E_0^1\rangle$ 关联起来。

对于一个只能对系统 $S$ 进行测量的观察者来说，他所能描述的系统状态是 $S$ 的**约化密度矩阵（reduced density matrix）**，通过对总系统的密度矩阵 $\rho_{SE} = |\Psi_{SE}\rangle\langle\Psi_{SE}|$ 求关于环境自由度的**偏迹（partial trace）**得到：
$\rho_S = \text{Tr}_E(\rho_{SE}) = |a|^2|0\rangle\langle 0| + |b|^2|1\rangle\langle 1| + ab^*\langle E_0^1|E_0^0\rangle|0\rangle\langle 1| + a^*b\langle E_0^0|E_0^1\rangle|1\rangle\langle 0|$

关键在于环境态的内积 $\gamma = \langle E_0^1|E_0^0\rangle$。由于环境自由度极多，即使微小的相互作用也会导致 $|E_0^0\rangle$ 和 $|E_0^1\rangle$ 迅速变得近似正交，即 $|\gamma| \to 0$。当这种情况发生时，$\rho_S$ 中的非对角相干项迅速衰减至零，使得 $\rho_S$ 变得与一个经典统计混合态 $\rho_{\text{mix}} = |a|^2|0\rangle\langle 0| + |b|^2|1\rangle\langle 1|$ 在操作上无法区分。

重要的是，这个过程完全是幺正的，没有发生任何真正的“坍缩”。整个“系统+环境”的总态仍然是一个纯的纠缠态。[相干性](@entry_id:268953)信息并没有消失，而是被“泄漏”到了[系统与环境](@entry_id:142270)之间复杂的关联之中，对于只看系统的局域观察者而言变得无法获取。退相干解释了为何宏观叠加态如此脆弱，以及为何由环境相互作用所决定的某些“[指针态](@entry_id:150099)”（pointer states，如宏观物体的位置）构成了我们经验中的经典现实。