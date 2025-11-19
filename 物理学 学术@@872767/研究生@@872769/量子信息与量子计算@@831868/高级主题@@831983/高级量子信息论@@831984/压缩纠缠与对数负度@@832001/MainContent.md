## 引言
量化量子纠缠是[量子信息科学](@entry_id:150091)的核心任务之一，尤其是对于普遍存在的混合态系统。与[纯态](@entry_id:141688)不同，混合态的关联包含了经典不确定性和量子相干性的复杂混合，使得简单的纠缠熵不再适用。这构成了一个知识鸿沟：我们需要更强大的、在[局域操作和经典通信](@entry_id:136398)（LOCC）下不会增加的[纠缠度量](@entry_id:139894)，即“纠缠幺正单调”。本文旨在深入剖析两种互补且至关重要的[混合态纠缠](@entry_id:142680)度量：对数负度（Logarithmic Negativity）和压缩纠缠（Squashed Entanglement）。前者以其[可计算性](@entry_id:276011)而闻名，是实验和理论计算的有力工具；后者则以其完美的理论性质而著称，为理解纠缠的根本属性提供了坚实的框架。通过本文，读者将系统学习这两种度量的核心思想、性质及其在物理学前沿的应用。

## 原理与机制

在对[混合态](@entry_id:141568)量子系统中的纠缠进行量化时，我们需要比分析[纯态](@entry_id:141688)时更为精细的工具。虽然纯态的纠缠熵提供了一个清晰的度量，但对于[混合态](@entry_id:141568)，情况要复杂得多。[混合态](@entry_id:141568)可以看作是[纯态](@entry_id:141688)的[统计系综](@entry_id:149738)，其纠缠不仅源于其组成成分的量子相干性，还受到经典不确定性的影响。因此，一个有效的[混合态纠缠](@entry_id:142680)度量（称为纠缠幺正单调（entanglement monotone））必须满足一系列严格的公理，以确保其在[局域操作和经典通信](@entry_id:136398)（LOCC）下不会增加。本章将深入探讨两种重要且互补的[纠缠度量](@entry_id:139894)：对数负度（Logarithmic Negativity）和压缩纠缠（Squashed Entanglement）。前者因其可计算性而广受欢迎，而后者则因其优越的理论性质而备受推崇。

### 对数负度：一个可计算的[纠缠见证](@entry_id:137591)

[量化纠缠](@entry_id:144669)最直接的方法之一是基于一个强大的[可分性](@entry_id:143854)判据：**[Peres-Horodecki判据](@entry_id:146053)**，或称为**正[部分转置](@entry_id:136776) (positive partial transpose, PPT)** 判据。

#### [部分转置](@entry_id:136776)与[PPT判据](@entry_id:137549)

考虑一个作用于[希尔伯特空间](@entry_id:261193) $\mathcal{H}_{AB} = \mathcal{H}_A \otimes \mathcal{H}_B$ 上的二体态[密度矩阵](@entry_id:139892) $\rho_{AB}$。对于子系统B的**[部分转置](@entry_id:136776) (partial transpose)** 操作 $\rho_{AB}^{T_B}$ 定义为在某个给定的乘积基 $|i_A\rangle \otimes |j_B\rangle$ 下，仅对子系统B的矩阵指标进行[转置](@entry_id:142115)：
$$
\langle i_A, j_B | \rho_{AB}^{T_B} | k_A, l_B \rangle = \langle i_A, l_B | \rho_{AB} | k_A, j_B \rangle
$$
[Peres-Horodecki判据](@entry_id:146053)指出，如果一个态 $\rho_{AB}$ 是可分的（即可以写成乘积态的[凸组合](@entry_id:635830)），那么其[部分转置](@entry_id:136776) $\rho_{AB}^{T_B}$ 必然是半正定的（即所有[本征值](@entry_id:154894)均非负）。因此，如果一个态的[部分转置](@entry_id:136776)矩阵至少有一个负[本征值](@entry_id:154894)，那么该态必定是纠缠的。这样的态被称为**非正[部分转置](@entry_id:136776) (negative partial transpose, NPT)** 态。

对于[低维系统](@entry_id:145463)，如 $2 \otimes 2$ 和 $2 \otimes 3$ 维系统，[PPT判据](@entry_id:137549)既是[可分性](@entry_id:143854)的必要条件也是充分条件。但在更高维度中，存在一些被称为**束缚纠缠 (bound entangled)** 的特殊态，它们是纠缠的，但却满足PPT条件。

#### 对数负度的定义与计算

基于[PPT判据](@entry_id:137549)，我们可以定义一个定量的[纠缠度量](@entry_id:139894)，称为**对数负度 (logarithmic negativity)**，记为 $E_N(\rho)$：
$$
E_N(\rho) = \log_2 (\| \rho^{T_B} \|_1)
$$
其中，$\|X\|_1 = \mathrm{Tr}\sqrt{X^\dagger X}$ 是**迹范数 (trace norm)**，它等于算符 $X$ 的所有[奇异值](@entry_id:152907)之和。由于 $\rho^{T_B}$ 是厄米矩阵，其迹范数简化为所有[本征值](@entry_id:154894)的[绝对值](@entry_id:147688)之和，即 $\| \rho^{T_B} \|_1 = \sum_i |\lambda_i|$。根据定义，一个态是PPT态当且仅当其迹范数为1（因为 $\mathrm{Tr}(\rho^{T_B}) = \mathrm{Tr}(\rho) = 1$），此时对数负度为零。任何NPT态的对数负度都大于零。

**示例：计算一个二[量子比特](@entry_id:137928)X-态的对数负度** [@problem_id:135042]

考虑一个二[量子比特](@entry_id:137928)X-态，其密度矩阵在计算基 $\lbrace|00\rangle, |01\rangle, |10\rangle, |11\rangle\rbrace$ 下为：
$$
\rho = \frac{1}{12} \begin{pmatrix}
5 & 0 & 0 & 3\sqrt{2} \\
0 & 1 & 0 & 0 \\
0 & 0 & 2 & 0 \\
3\sqrt{2} & 0 & 0 & 4
\end{pmatrix}
$$
对子系统B进行[部分转置](@entry_id:136776)。当密度矩阵以子系统A的基为索引的[分块矩阵](@entry_id:148435)形式书写时，[部分转置](@entry_id:136776)操作相当于转置每一个子块。操作后的矩阵为：
$$
\rho^{T_B} = \frac{1}{12} \begin{pmatrix}
5 & 0 & 0 & 0 \\
0 & 1 & 3\sqrt{2} & 0 \\
0 & 3\sqrt{2} & 2 & 0 \\
0 & 0 & 0 & 4
\end{pmatrix}
$$
该矩阵是块对角的。其[本征值](@entry_id:154894)由对角块的[本征值](@entry_id:154894)给出。第一个和第四个块是 $1 \times 1$ 的，给出[本征值](@entry_id:154894) $\frac{5}{12}$ 和 $\frac{4}{12}$。中间 $2 \times 2$ 块 $\frac{1}{12} \begin{pmatrix} 1 & 3\sqrt{2} \\ 3\sqrt{2} & 2 \end{pmatrix}$ 的[本征值](@entry_id:154894)为 $\frac{3 \pm \sqrt{73}}{24}$。其中一个[本征值](@entry_id:154894) $\frac{3 - \sqrt{73}}{24}$ 是负的，证实了该态是纠缠的。

迹范数是这些[本征值](@entry_id:154894)[绝对值](@entry_id:147688)的和：
$$
\|\rho^{T_B}\|_1 = \frac{5}{12} + \frac{4}{12} + \left|\frac{3 + \sqrt{73}}{24}\right| + \left|\frac{3 - \sqrt{73}}{24}\right| = \frac{10}{24} + \frac{8}{24} + \frac{3+\sqrt{73}}{24} + \frac{\sqrt{73}-3}{24} = \frac{18 + 2\sqrt{73}}{24} = \frac{9 + \sqrt{73}}{12}
$$
因此，对数负度为 $E_N(\rho) = \log_2 \left( \frac{9 + \sqrt{73}}{12} \right)$。

这个例子阐明了从一个给定的[密度矩阵](@entry_id:139892)计算对数负度的标准流程：执行[部分转置](@entry_id:136776)，计算新矩阵的本征谱，求和它们的[绝对值](@entry_id:147688)，最后取对数。这一过程对于任何有限维系统都是明确的。

**示例：纠缠的[激活阈值](@entry_id:635336)** [@problem_id:135029]

对数负度可以用来确定一个态何时从可分变为纠缠。考虑一个混合态 $\rho(p) = p |\Psi^+\rangle\langle\Psi^+| + (1-p) \sigma$，其中 $|\Psi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$ 是一个贝尔态，而 $\sigma = \frac{1}{2}(|01\rangle\langle01| + |10\rangle\langle10|)$ 是一个[可分态](@entry_id:142281)。[部分转置](@entry_id:136776)是线性操作，因此 $\rho(p)^{T_B} = p (|\Psi^+\rangle\langle\Psi^+|)^{T_B} + (1-p) \sigma^{T_B}$。计算表明，$\rho(p)^{T_B}$ 的最小[本征值](@entry_id:154894)为 $\frac{1-2p}{2}$。该态变为NPT的[临界点](@entry_id:144653)是当这个最小[本征值](@entry_id:154894)变为负数时，即 $1-2p  0$，解得 $p > \frac{1}{2}$。因此，[临界概率](@entry_id:182169)为 $p_c = \frac{1}{2}$。当混合概率超过这个阈值时，[贝尔态](@entry_id:140749)的纠缠特性才“战胜”[可分态](@entry_id:142281)的噪声并表现出来。

**示例：[连续变量系统](@entry_id:144293)** [@problem_id:135145]

对数负度的概念也适用于[连续变量系统](@entry_id:144293)。一个重要的例子是**[双模压缩真空态](@entry_id:147759) (two-mode squeezed vacuum, TMSV)**，其在 Fock 基 $|n, m\rangle$ 下表示为：
$$
|\psi(r)\rangle_{AB} = \frac{1}{\cosh r} \sum_{n=0}^\infty (\tanh r)^n |n, n\rangle
$$
其中 $r>0$ 是压缩参数。通过计算其[部分转置](@entry_id:136776)矩阵的[本征值](@entry_id:154894)谱并求和，可以得到其迹范数为 $\|\rho_{AB}^{T_B}\|_1 = e^{2r}$。因此，TMSV态的对数负度是一个与压缩参数成正比的简单表达式：
$$
E_N(\rho_{AB}) = \log_2(e^{2r}) = \frac{2r}{\ln 2}
$$
这表明随着压缩参数 $r$ 的增加，纠缠也单调增加。

### 对数负度的性质与局限性

尽管对数负度是一个非常有用的工具，但它并非一个完美的[纠缠度量](@entry_id:139894)。它具有一些理论上的“缺陷”，这促使我们去寻找更符合物理直觉的度量。

#### 非凸性

一个理想的[纠缠度量](@entry_id:139894)应该是**凸 (convex)** 的，即混合两个态所产生的纠缠不应超过这两个态纠缠的加权平均值：$E(p\rho_1 + (1-p)\rho_2) \le p E(\rho_1) + (1-p) E(\rho_2)$。这个性质意味着仅仅通过经典混合无法凭空创造纠缠。然而，对数负度不满足这个性质。

**示例：对数负度的非[凸性](@entry_id:138568)** [@problem_id:135163]

考虑两个正交[贝尔态](@entry_id:140749)的混合：$\rho(p) = p|\phi^+\rangle\langle\phi^+| + (1-p)|\psi^+\rangle\langle\psi^+|$，其中 $|\phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$ 和 $|\psi^+\rangle = \frac{1}{\sqrt{2}}(|01\rangle + |10\rangle)$。
$|\phi^+\rangle$ 和 $|\psi^+\rangle$ 都是最大纠缠态，它们的对数负度都是 $E_N = \log_2(2) = 1$。根据凸性，我们期望 $E_N(\rho(p)) \le p \cdot 1 + (1-p) \cdot 1 = 1$。
然而，直接计算表明 $E_N(\rho(p)) = \log_2(1 + |2p - 1|)$。在 $p=\frac{1}{2}$ 时，$\rho(\frac{1}{2})$ 的对数负度为 $E_N = \log_2(1)=0$。这与[凸性](@entry_id:138568)不等式 $0 \le 1$ 并不矛盾。
但是，我们可以定义一个“[凸性](@entry_id:138568)违反”函数 $\Delta(p) = [p E_N(\rho_1) + (1-p) E_N(\rho_0)] - E_N(\rho(p))$。对于这个例子，$\Delta(p) = 1 - \log_2(1+|2p-1|)$。在 $p = 1/2$ 时，这个违反达到了最大值 $\Delta(1/2) = 1$。这表明混合操作显著地“破坏”了纠缠，其结果远比预期的要小，这正是非[凸性](@entry_id:138568)的体现。

#### 非单配性

**[纠缠单配性](@entry_id:137181) (Monogamy of entanglement)** 是[量子纠缠](@entry_id:136576)的一个标志性特征，它指出纠缠是一种不可分享的资源。如果系统A与系统B高度纠缠，那么A与任何第三方系统C的纠缠就会受到严格限制。对于一个三体[纯态](@entry_id:141688) $|\psi\rangle_{ABC}$，一个单配的[纠缠度量](@entry_id:139894) $E$ 应满足 $E(A:BC) \ge E(A:B) + E(A:C)$。对数负度同样违反了这个性质。

**示例：W-态的[纠缠单配性](@entry_id:137181)** [@problem_id:135096] [@problem_id:135071]

考虑[三量子比特](@entry_id:146257)的 **W-态**：$|\text{W}\rangle_{ABC} = \frac{1}{\sqrt{3}}(|100\rangle + |010\rangle + |001\rangle)$。
我们可以计算系统A与BC之间的纠缠，以及A与B、A与C之间的纠缠。
1. 对于A:BC划分，W-态为纯态，其[施密特分解](@entry_id:145934)为 $|\text{W}\rangle = \sqrt{\frac{2}{3}} |0\rangle_A \otimes \frac{1}{\sqrt{2}}(|10\rangle+|01\rangle)_{BC} + \sqrt{\frac{1}{3}}|1\rangle_A \otimes |00\rangle_{BC}$。[施密特系数](@entry_id:137823)为 $\lambda_1=\sqrt{2/3}$ 和 $\lambda_2=\sqrt{1/3}$。其对数负度为 $E_N(A:BC) = \log_2 \left( (\lambda_1+\lambda_2)^2 \right) = \log_2 \left( (\sqrt{2/3}+\sqrt{1/3})^2 \right) = \log_2(\frac{3+2\sqrt{2}}{3}) \approx 0.95$。
2. 对于A:B划分，我们需要先得到[约化密度矩阵](@entry_id:146315) $\rho_{AB} = \mathrm{Tr}_C(\rho_{ABC}) = \frac{1}{3}(|00\rangle\langle00| + |01\rangle\langle01| + |10\rangle\langle10| + |01\rangle\langle10| + |10\rangle\langle01|)$。对该态进行[部分转置](@entry_id:136776)，可以发现其所有[本征值](@entry_id:154894)均为非负。因此，对数负度为 $E_N(A:B)=0$。由于对称性，$E_N(A:C) = E_N(A:B) = 0$。

单配性关系为 $E_N(A:BC) \ge E_N(A:B) + E_N(A:C)$。对于[W态](@entry_id:180654)，我们得到 $\log_2(\frac{3+2\sqrt{2}}{3}) \ge 0 + 0$，该不等式成立。所以对于[W态](@entry_id:180654)，对数负度是单配的。然而，单配性要求这个不等式对所有态都成立，而存在其他态（如此处未展示的某些[GHZ态](@entry_id:182114)和噪声的[混合态](@entry_id:141568)）使得该不等式被违反。因此，对数负度不是一个普适的单配[纠缠度量](@entry_id:139894)。

#### 操作性意义：与[量子隐形传态](@entry_id:144485)保真度的联系

尽管有理论上的局限性，对数负度在一个重要的操作任务中扮演了角色：**[量子隐形传态](@entry_id:144485) (quantum teleportation)**。使用一个二体态 $\rho$ 作为资源来传输一个任意的[量子比特](@entry_id:137928)，其平均传输保真度 $F_{avg}$ 与该资源态的**单态分数 (singlet fraction)** $F_s = \langle \Psi^- | \rho | \Psi^- \rangle$ （或任何贝尔态）直接相关：$F_{avg} = \frac{2 F_s + 1}{3}$。当保真度超过[经典极限](@entry_id:148587) $2/3$ 时，隐形传态被认为是成功的。

**示例：纠缠与隐形传态保真度** [@problem_id:135143]

考虑一个[混合态](@entry_id:141568)资源 $\rho(p) = p |\Phi^+\rangle\langle\Phi^+| + (1-p) |00\rangle\langle 00|$。
它的单态分数为 $F_s = \langle \Phi^+ | \rho | \Phi^+ \rangle = p + \frac{1-p}{2} = \frac{1+p}{2}$。
平均保真度为 $F_{avg} = \frac{2(\frac{1+p}{2})+1}{3} = \frac{2+p}{3}$。
另一方面，该态的对数负度可以计算为 $E_N(\rho(p)) = \log_2(1+p)$。
通过联立这两个方程，消去参数 $p$，我们可以得到对数负度与平均保真度之间的一个直接关系：
$$
E_N(\rho) = \log_2(3F_{avg} - 1)
$$
这个优美的公式表明，对于这类态，对数负度直接量化了其作为隐形传态资源的有效性。只有当 $F_{avg} > 2/3$ 时（即 $p > 0$），对数负度才大于零，这恰好对应于[量子隐形传态](@entry_id:144485)超越经典能力的范围。

### 压缩纠缠：一种信息论方法

对数负度的理论缺陷促使研究者们寻求更完美的[纠缠度量](@entry_id:139894)。**压缩纠缠 (Squashed Entanglement)**, $E_{sq}$, 就是其中之一，它基于深刻的信息论思想，并满足所有理想[纠缠度量](@entry_id:139894)应具备的性质。

#### 定义

压缩纠缠的思想是，两个系统A和B之间的纠缠，是它们所共享的、任何潜在窃听者E都无法获取的关联信息的量。为了形式化这个思想，我们考虑一个二体态 $\rho_{AB}$ 的任意**扩展 (extension)**，即一个[三体](@entry_id:265960)态 $\rho_{ABE}$，使得 $\mathrm{Tr}_E(\rho_{ABE}) = \rho_{AB}$。这个扩展可以被看作是包含了窃听者E所能掌握的关于A和B的所有信息的系统。

在此基础上，我们定义**量子[条件互信息](@entry_id:139456) (quantum conditional mutual information)**：
$$
I(A:B|E) = S(\rho_{AE}) + S(\rho_{BE}) - S(\rho_{ABE}) - S(\rho_{E})
$$
其中 $S(\sigma) = -\mathrm{Tr}(\sigma \log_2 \sigma)$ 是[冯·诺依曼熵](@entry_id:143216)。$I(A:B|E)$ 量化了在给定E的知识后，A和B之间仍然存在的总关联（包括经典和量子）。

**压缩纠缠**被定义为在所有可能的扩展中，量子[条件互信息](@entry_id:139456)的最小值（[下确界](@entry_id:140118)）：
$$
E_{sq}(\rho_{AB}) = \frac{1}{2} \inf_{\rho_{ABE}} I(A:B|E)
$$
因子 $1/2$ 是为了使得对于一个最大纠缠的二[量子比特](@entry_id:137928)态，其值为1。取下确界的过程，直观上对应于寻找一个“最坏情况”下的窃听者E，即她对A和B之间纠缠的干扰最大化。A和B之间能够“抵抗”住这种窃听而幸存下来的关联，就是它们的内在纠缠。

#### 基本性质

压缩纠缠具有许多理想的性质，包括：
- **忠实性 (Faithfulness):** $E_{sq}(\rho) = 0$ 当且仅当 $\rho$ 是可分的。
- **凸性 (Convexity):** 满足 $E_{sq}(p\rho_1 + (1-p)\rho_2) \le p E_{sq}(\rho_1) + (1-p) E_{sq}(\rho_2)$。
- **单配性 (Monogamy):** 对于任意[三体](@entry_id:265960)态，满足 $E_{sq}(A:BC) \ge E_{sq}(A:B) + E_{sq}(A:C)$。
- **可加性 (Additivity):** $E_{sq}(\rho \otimes \sigma) = E_{sq}(\rho) + E_{sq}(\sigma)$。

**证明：[可分态](@entry_id:142281)的压缩纠缠为零** [@problem_id:135097]

我们可以证明[可分态](@entry_id:142281)的压缩纠缠为零。任何一个[可分态](@entry_id:142281)都可以写成 $\rho_{AB} = \sum_k q_k \rho_A^{(k)} \otimes \rho_B^{(k)}$。我们可以构造一个特殊的“经典扩展”：
$$
\rho_{ABE} = \sum_{k} q_k \rho_A^{(k)} \otimes \rho_B^{(k)} \otimes |k\rangle_E\langle k|
$$
这里，[辅助系统](@entry_id:142219)E是一个经典寄存器，它记录了混合系综中的索引 $k$。对于这个态，我们可以计算其所有部分的[冯·诺依曼熵](@entry_id:143216)。由于态在E的基下是块对角的，熵的计算可以简化。例如，$S(\rho_{ABE}) = H(\{q_k\}) + \sum_k q_k S(\rho_A^{(k)} \otimes \rho_B^{(k)})$，其中 $H(\{q_k\})$ 是经典[香农熵](@entry_id:144587)。经过一番代数运算，可以精确地证明 $I(A:B|E) = 0$。
由于压缩纠缠是所有扩展中 $I(A:B|E)$ 的下确界，而我们找到了一个使它为零的扩展，且 $I(A:B|E)$ 总是非负的，因此对于任何[可分态](@entry_id:142281)，其压缩纠缠必定为零。

#### 计算的挑战与操作性意义

压缩纠缠的定义涉及对所有可能扩展的优化，这使得它在绝大多数情况下都极难计算。然而，它的定义本身就蕴含了深刻的操作性意义。压缩纠缠等于通过LOCC和一个从B到A的单向经典信道，从EPR对中制备态 $\rho_{AB}$ 所需的最小速率。

**示例：与纠缠破缺信道的联系** [@problem_id:135068]

一个信道被称为**纠缠破缺 (entanglement-breaking)** 的，如果它作用在一个纠缠态的任何一个子系统上后，总会输出一个[可分态](@entry_id:142281)。这类信道的 Choi-Jamiołkowski 表示，即其对应的 Choi 态，总是一个[可分态](@entry_id:142281)。利用上面为[可分态](@entry_id:142281)构造的经典扩展，可以证明任何纠缠破缺信道的 Choi 态的压缩纠缠都为零。这为我们理解信道性质和态的纠缠之间建立了深刻的联系。

**示例：与[量子密钥分发](@entry_id:138070)的联系** [@problem_id:135087]

压缩纠缠也与**[量子密钥分发](@entry_id:138070) (Quantum Key Distribution, QKD)** 密切相关。在A、B、E三方场景下，一个重要的量是**条件[相干信息](@entry_id:147583) (conditional coherent information)**, $I(A\rangle B|E) = S(\rho_{BE}) - S(\rho_{ABE})$，它为A和B之间可以提取的安全密钥速率提供了一个下界。考虑一个三方态 $\rho_{ABE} = (1-p)|\phi^+\rangle_{AB}\langle\phi^+| \otimes |0\rangle_E\langle 0| + p |01\rangle_{AB}\langle 01| \otimes |1\rangle_E\langle 1|$。在这个模型中，系统有 $1-p$ 的概率处于完美纠缠且不被窃听的状态，有 $p$ 的概率处于一个被窃听者完全知晓的乘积态。通过计算可以得到 $I(A\rangle B|E) = 1-p$。这直观地反映了A和B能够获得的密钥速率等于系统未被干扰的概率。这个量与压缩纠缠密切相关，为后者在[量子密码学](@entry_id:144827)中的应用提供了基础。

### 计算与界定压缩纠缠

尽管直接计算压缩纠缠很困难，但我们可以通过为特定的扩展计算 $I(A:B|E)$ 来获得其**[上界](@entry_id:274738)**。

**示例：利用特定纯化计算上界** [@problem_id:135051] [@problem_id:135086]

1.  考虑一个由两个正交贝尔态组成的[混合态](@entry_id:141568) $\rho_{AB}(p) = p |\phi^+\rangle\langle\phi^+| + (1-p)|\phi^-\rangle\langle\phi^-|$ [@problem_id:135051]。我们可以为其构造一个纯化 $|\Psi\rangle_{ABE} = \sqrt{p} |\phi^+\rangle_{AB} |0\rangle_E + \sqrt{1-p} |\phi^-\rangle_{AB} |1\rangle_E$。对于这个[纯态](@entry_id:141688)扩展，由于 $S(\rho_{ABE})=0$，计算 $I(A:B|E) = S(\rho_{AE}) + S(\rho_{BE}) - S(\rho_E)$ 变得相对容易。计算表明，$S(\rho_{AE}) = S(\rho_{BE}) = 1$，$S(\rho_E)$ 是二元熵 $H(p)$。因此，$I(A:B|E) = 2 - H(p)$。这为 $E_{sq}(\rho_{AB})$ 提供了一个[上界](@entry_id:274738)：$E_{sq}(\rho_{AB}) \le 1 - \frac{1}{2}H(p)$。

2.  考虑一个[贝尔态](@entry_id:140749) $|\Phi^+\rangle$ 的一个[量子比特](@entry_id:137928)通过**[相位阻尼](@entry_id:147888)信道 (phase-damping channel)** 后得到的态 [@problem_id:135086]。最终态是 $\rho_{AB}=(1-p)|\Phi^+\rangle\langle\Phi^+| + p|\Phi^-\rangle\langle\Phi^-|$，这与上一个例子中的态形式相同。因此，利用其典范纯化 (canonical purification) 得到的压缩纠缠[上界](@entry_id:274738)同样是 $1-\frac{1}{2}H(p)$。

### 两种度量的比较

对数负度和压缩纠缠为我们提供了两种不同的视角来审视纠缠。它们之间的关系并非简单的等价。

#### 度量间的层级关系

一个重要的理论结果是，对于任何二体态 $\rho$，压缩纠缠总是大于或等于对数负度：
$$
E_{sq}(\rho) \ge E_N(\rho)
$$
这表明压缩纠缠捕捉到了所有对数负度能探测到的纠缠，并且可能更多（例如，对于PPT束缚[纠缠态](@entry_id:152310)，$E_{sq}$ 可能为正，而 $E_N$ 始终为零）。

#### 渐近行为的差异

即使对于两种度量都不为零的态，它们的行为也可能截然不同。

**示例：[Werner态](@entry_id:141722)** [@problem_id:135165]

对于二[量子比特](@entry_id:137928)的[Werner态](@entry_id:141722) $\rho_W(p) = p |\psi^-\rangle\langle\psi^-| + (1-p) \frac{I}{4}$，它在 $p > 1/3$ 时是纠缠的。在此区域，两种[纠缠度量](@entry_id:139894)都为正。然而，当我们考察它们在纠缠边界 $p \to 1/3^+$ 附近的比值时，会发现一个有趣的现象：
$$
\lim_{p \to 1/3^+} \frac{E_{\text{sq}}(\rho_W(p))}{E_N(\rho_W(p))} = 3
$$
这个结果表明，即使在纠缠刚刚出现的区域，这两个度量也存在显著差异，它们并非简单的[线性依赖](@entry_id:185830)关系。

**示例：接近[纯态](@entry_id:141688)的极限** [@problem_id:135120]

考虑态 $\rho(p) = p |\Phi^+\rangle\langle\Phi^+| + (1-p) |00\rangle\langle 00|$。当 $p \to 1^-$ 时，该态趋于一个最大纠缠[纯态](@entry_id:141688)，此时 $E_{sq}$ 和 $E_N$ 都趋于1。然而，它们趋近于1的速率是不同的。通过[泰勒展开](@entry_id:145057)可以发现：
$$
\lim_{p \to 1^-} \frac{1 - E_{sq}(\rho(p))}{1 - E_N(\rho(p))} = 2
$$
这意味着在接近最大纠缠时，对数负度比压缩纠缠更快地“饱和”到最大值。这再次凸显了两种度量捕捉纠缠动力学方式的不同。

#### 特殊情况下的等价性

尽管存在差异，但在某些高度对称的态族中，压缩纠缠可以被精确计算，并与其他更容易计算的量（如[形成纠缠](@entry_id:139137) (entanglement of formation)）等价。例如，对于贝尔对[角态](@entry_id:145477)（在贝尔基下是对角的态），其压缩纠缠等于其[形成纠缠](@entry_id:139137)。对于问题 [@problem_id:135101] 中探讨的态 $\rho(p) = p |\Phi^+\rangle\langle\Phi^+| + (1-p) |\Psi^-\rangle\langle\Psi^-|$，其压缩纠缠可以被精确地计算出来，结果为 $E_{sq}(\rho(p)) = h\left( \frac{1}{2} + \sqrt{p(1-p)} \right)$，其中 $h(x)$ 是二元熵函数。

### 总结

本章介绍了两种核心的[混合态纠缠](@entry_id:142680)度量：对数负度和压缩纠缠。

- **对数负度**基于[PPT判据](@entry_id:137549)，易于计算，并与[量子隐形传态](@entry_id:144485)等操作任务有直接联系。然而，它在理论上存在缺陷，如非凸性和非单配性，且无法检测所有纠缠（如PPT束缚纠缠）。

- **压缩纠缠**基于信息论，定义优雅，并满足所有作为理想[纠缠度量](@entry_id:139894)的公理（忠实性、[凸性](@entry_id:138568)、单配性等）。它具有深刻的操作性意义，与量子信道和[量子密码学](@entry_id:144827)密切相关。但其计算极为困难，通常只能求得其上界。

这两种度量并非相互排斥，而是互为补充。对数负度是实验和理论计算中的实用工具，而压缩纠缠则为我们理解纠缠的根本性质提供了坚实的理论框架。在探索[量子信息科学](@entry_id:150091)的广阔领域时，根据具体问题的需求选择合适的[纠缠度量](@entry_id:139894)，是进行有效研究的关键一步。