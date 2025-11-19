## 引言
自爱因斯坦将其著名地称为“鬼魅般的超距作用”以来，[量子纠缠](@entry_id:136576)已从一个令人费解的悖论演变为现代物理学的基石。它描述了多个量子粒子之间一种深刻而内在的联系，无论它们相隔多远，测量其中一个粒子的状态似乎能瞬间影响到另一个。这种[非局域关联](@entry_id:180194)不仅挑战了我们对物理实在的经典直觉，也为信息处理和物理学探索开辟了前所未有的可能性。

然而，要真正驾驭纠缠的力量，我们必须超越富有诗意的比喻，建立一个严格的数学和物理框架。我们如何确切地判断一个系统是否纠缠？如何量化其纠缠的“多少”？不同类型的纠缠有何区别？这些纠缠又如何在[量子计算](@entry_id:142712)、[材料科学](@entry_id:152226)乃至宇宙学等领域发挥作用？本篇文章旨在系统地回答这些问题，为读者提供一个关于纠缠及其性质的全面而深入的研究生级别图景。

为了实现这一目标，本文将分为三个核心部分。在第一章“原理与机制”中，我们将深入纠缠的数学核心，学习如何使用[施密特分解](@entry_id:145934)、[密度矩阵](@entry_id:139892)和各种判据来精确定义、探测和分类[纠缠态](@entry_id:152310)。我们还将探讨[量化纠缠](@entry_id:144669)的各种度量，如纠缠熵和并发度，并将纠缠置于[量子操作](@entry_id:145906)的框架下，理解其作为一种资源的本质。接下来，在第二章“应用与跨学科连接”中，我们将视野扩展到纠缠的广阔应用领域，见证它如何驱动量子通信、赋能高精度传感，并作为一种强大的理论探针，帮助我们揭示凝聚态[物质的[拓扑](@entry_id:144114)相](@entry_id:141674)、高能物理中的基本相互作用，甚至[黑洞](@entry_id:158571)与时空的几何奥秘。最后，在“动手实践”部分，读者将有机会通过解决具体问题，将前两章学到的理论工具付诸实践，从而巩固和深化对纠缠复杂性的理解。现在，让我们一同踏上这段探索量子世界最深刻奥秘的旅程。

## 原理与机制

量子纠缠是量子力学最深刻、最违反直觉的特征之一，它描述了[复合量子系统](@entry_id:193313)中各部分之间存在的非[经典关联](@entry_id:136367)。与仅在测量时才显现其诡异之处的叠加态不同，纠缠是一种内在的、共享的属性，将多个[量子比特](@entry_id:137928)的命运联系在一起，无论它们在空间上相隔多远。本章将系统地阐述纠缠的核心原理、表征纠缠的数学工具，以及探测和量化这种独特[量子关联](@entry_id:136327)的机制。

### 纠缠的本质：可分离性与[纯态](@entry_id:141688)结构

一个[复合量子系统](@entry_id:193313)的状态可以分为两类：**可分离态 (separable states)** 和 **纠缠态 (entangled states)**。一个可分离的[混合态](@entry_id:141568)可以表示为其子系统状态的[凸组合](@entry_id:635830)，形式为 $\rho = \sum_k p_k \rho_k^A \otimes \rho_k^B$，其中 $p_k$ 是[概率分布](@entry_id:146404)，$p_k \ge 0$ 且 $\sum_k p_k = 1$。这样的状态可以通过[局域操作和经典通信](@entry_id:136398) (LOCC) 来制备。任何不能写成这种形式的状态都被定义为纠缠态。

对于由子系统 A 和 B 组成的[二分纯态](@entry_id:138323) $|\psi\rangle_{AB}$，我们有一个更为强大和简洁的描述工具：**[施密特分解](@entry_id:145934) (Schmidt decomposition)**。任何这样的纯态都可以写成如下形式：

$$
|\psi\rangle = \sum_{k=1}^{d} \lambda_k |u_k\rangle_A |v_k\rangle_B
$$

其中 $d \le \min(\dim\mathcal{H}_A, \dim\mathcal{H}_B)$。系数 $\lambda_k$ 是非负实数，称为**[施密特系数](@entry_id:137823) (Schmidt coefficients)**，它们满足[归一化条件](@entry_id:156486) $\sum_k \lambda_k^2 = 1$。$\{|u_k\rangle_A\}$ 和 $\{|v_k\rangle_B\}$ 分别是子系统 A 和 B 的希尔伯特空间中的一组[正交基](@entry_id:264024)，称为**施密特基 (Schmidt bases)**。

[施密特分解](@entry_id:145934)揭示了纠缠的根本性质。一个纯态是可分离的（即乘积态），当且仅当其[施密特分解](@entry_id:145934)中只有一项。非零[施密特系数](@entry_id:137823)的数量，即**[施密特数](@entry_id:141441) (Schmidt number)** $K$，是纠缠的一个基本指示器。如果 $K=1$，该态是可分离的；如果 $K>1$，该态是纠缠的。

从实践上讲，对于一个给定的纯态 $|\psi\rangle = \sum_{i,j} C_{ij} |i\rangle_A |j\rangle_B$，其[施密特系数](@entry_id:137823)是[系数矩阵](@entry_id:151473) $C$ 的[奇异值](@entry_id:152907)。因此，[施密特数](@entry_id:141441) $K$ 等于矩阵 $C$ 的秩。例如，考虑一个由两个三维量子系统（qutrit）组成的二分态：

$$
|\psi\rangle = \frac{1}{\sqrt{8}}(3|00\rangle + \sqrt{6}|11\rangle + |22\rangle - |01\rangle - |10\rangle)
$$

其系数矩阵 $C$ 为：

$$
C = \frac{1}{\sqrt{8}} \begin{pmatrix} 3  -1  0 \\ -1  \sqrt{6}  0 \\ 0  0  1 \end{pmatrix}
$$

通过计算该矩阵的行列式，$\det(C) \propto (3\sqrt{6} - 1) \neq 0$，我们发现其秩为 3。因此，这个态的[施密特数](@entry_id:141441)为 $K=3$ [@problem_id:74847]，表明它是一个[纠缠态](@entry_id:152310)，并且其纠缠结构涉及每个子系统的全部三个维度。

### 量化[二分纯态](@entry_id:138323)纠缠

对于[纯态](@entry_id:141688) $|\psi\rangle_{AB}$，其纠缠程度可以被唯一地量化。所有关于纠缠的信息都编码在[施密特系数](@entry_id:137823) $\{\lambda_k\}$ 中。描述这种纠缠的标准度量是**纠缠熵 (entropy of entanglement)**，它被定义为任一子系统的**[冯·诺依曼熵](@entry_id:143216) (von Neumann entropy)**。

首先，我们通过对另一个子系统进行求迹（tracing out）来获得[约化密度矩阵](@entry_id:146315)。例如，子系统 A 的[约化密度矩阵](@entry_id:146315)为 $\rho_A = \text{Tr}_B(|\psi\rangle\langle\psi|)$。利用[施密特分解](@entry_id:145934)，我们发现 $\rho_A$ 在其施密特基 $\{|u_k\rangle_A\}$ 中是对角的：

$$
\rho_A = \sum_k \lambda_k^2 |u_k\rangle_A\langle u_k|
$$

$\rho_A$ 的[本征值](@entry_id:154894)恰好是[施密特系数](@entry_id:137823)的平方，$\lambda_k^2$。纠缠熵 $E(|\psi\rangle)$ 随之定义为：

$$
E(|\psi\rangle) = S(\rho_A) = -\text{Tr}(\rho_A \log_2 \rho_A) = -\sum_k \lambda_k^2 \log_2(\lambda_k^2)
$$

这个量在 $0$（对于可分离态）和 $\log_2 d$（对于最大纠缠态）之间取值。值得注意的是，由于 $S(\rho_A) = S(\rho_B)$，纠缠是双方共享的对称属性。

考虑一个由 $N$ 个[量子比特](@entry_id:137928)组成的**Dicke 态 (Dicke state)**，它被定义为所有具有 $k$ 个激发（即 $k$ 个[量子比特](@entry_id:137928)处于 $|1\rangle$ 态）的计算[基态](@entry_id:150928)的等权重叠加。例如，对于 $N=4, k=2$ 的情况，态为 $|D_4^2\rangle = \frac{1}{\sqrt{6}}(|1100\rangle + |1010\rangle + |1001\rangle + |0110\rangle + |0101\rangle + |0011\rangle)$。由于该态的对称性，任何单个[量子比特](@entry_id:137928)的[约化密度矩阵](@entry_id:146315)都是相同的。通过计算，我们发现单个[量子比特](@entry_id:137928)处于 $|0\rangle$ 或 $|1\rangle$ 的概率都是 $1/2$。因此，[约化密度矩阵](@entry_id:146315)为 $\rho_1 = \frac{1}{2}I$，这是一个[最大混合态](@entry_id:137775)。其[冯·诺依曼熵](@entry_id:143216)为 $S(\rho_1) = -(\frac{1}{2}\log_2\frac{1}{2} + \frac{1}{2}\log_2\frac{1}{2}) = 1$ [@problem_id:74849]。这表明，尽管整个四比特系统只处于一个纯态，但其中任意一个[量子比特](@entry_id:137928)与其余部分都是最大纠缠的。

[纠缠熵](@entry_id:140818)也是**相对[纠缠熵](@entry_id:140818) (relative entropy of entanglement)** 在纯态情况下的特例。相对纠缠熵 $E_R(\rho)$ 定义为状态 $\rho$ 与所有可分离态集合的最小[相对熵](@entry_id:263920)距离，对于[纯态](@entry_id:141688) $|\psi\rangle$ 它简化为 $S(\rho_A)$。例如，将一个 CNOT 门作用于初态 $(\sqrt{p}|0\rangle_A + \sqrt{1-p}|1\rangle_A) \otimes |0\rangle_B$ 会产生一个纠缠态 $|\psi_{out}\rangle = \sqrt{p}|00\rangle + \sqrt{1-p}|11\rangle$ [@problem_id:74926]。该态的[约化密度矩阵](@entry_id:146315) $\rho_A$ 的[本征值](@entry_id:154894)为 $p$ 和 $1-p$，因此其[纠缠熵](@entry_id:140818)为[二进制熵函数](@entry_id:269003) $H(p) = -p\log_2 p - (1-p)\log_2(1-p)$。这清晰地展示了[量子门](@entry_id:143510)操作如何将叠加态的“不确定性”转化为子系统间的纠缠。

### 混合态的挑战：探测纠缠

与[纯态](@entry_id:141688)不同，混合态的纠缠性质更为复杂。一个混合态可能是纠缠态的统计混合，但整体上却是可分离的。因此，确定一个给定的混合态 $\rho$ 是否纠缠是一个非平凡的问题。为此，发展出了一系列可操作的判据。

#### [纠缠目击者](@entry_id:137591)

**[纠缠目击者](@entry_id:137591) (Entanglement witness)** 是一个可观测量（厄米算符）$W$，它对于所有可分离态 $\sigma$ 都具有非负的[期望值](@entry_id:153208)，即 $\text{Tr}(W\sigma) \ge 0$。如果对于某个待测态 $\rho$，我们发现其[期望值](@entry_id:153208)为负，即 $\text{Tr}(W\rho)  0$，那么我们就可以断定 $\rho$ 必然是纠缠态。几何上，这相当于在希尔伯特-施密特空间中，用一个超平面将[纠缠态](@entry_id:152310) $\rho$ 与所有可分离态构成的[凸集分离](@entry_id:142000)开。

#### Peres-Horodecki (PPT) 判据

一个更具普适性的判据是 **Peres-Horodecki 判据**，也称为**正[部分转置](@entry_id:136776) (Positive Partial Transpose, PPT)** 判据。它断言：如果一个态 $\rho_{AB}$ 是可分离的，那么它在任一子系统上进行[部分转置](@entry_id:136776)后得到的矩阵 $\rho_{AB}^{T_A}$ 或 $\rho_{AB}^{T_B}$ 必须是半正定的（即所有[本征值](@entry_id:154894)非负）。[部分转置](@entry_id:136776)操作定义为在某个子系统的基底下对[密度矩阵](@entry_id:139892)进行转置。

这个判据的强大之处在于，对于 $2 \otimes 2$ 和 $2 \otimes 3$ 维的系统，它不仅是必要条件，还是**充分条件**。也就是说，在这些[低维系统](@entry_id:145463)中，一个态是可分离的当且仅当它是 PPT 的。

一个典型的例子是 **Werner 态**，它是一个贝尔态与[最大混合态](@entry_id:137775)的混合：$\rho(p) = p|\Psi^-\rangle\langle\Psi^-| + \frac{1-p}{4}I$。通过对其进行[部分转置](@entry_id:136776)并计算[本征值](@entry_id:154894)，可以发现最小的[本征值](@entry_id:154894)为 $\frac{1-3p}{4}$。为使该态是 PPT 的，必须有 $\frac{1-3p}{4} \ge 0$，即 $p \le 1/3$。由于这是个双比特系统，这个条件也保证了可分离性。因此，当 $p  1/3$ 时，该态变为[纠缠态](@entry_id:152310) [@problem_id:74953]。

一个优化的[纠缠目击者](@entry_id:137591)可以由 $\rho^{T_A}$ 的对应于负[本征值](@entry_id:154894)的本征矢 $|\phi_{\text{min}}\rangle$ 构造出来，即 $W = (|\phi_{\text{min}}\rangle\langle\phi_{\text{min}}|)^{T_A}$ [@problem_id:74875]。

#### 重排判据

对于更高维的系统（例如 $3 \otimes 3$），PPT 判据只是可分离性的必要条件而非充分条件。存在一些纠缠态，它们的[部分转置](@entry_id:136776)仍然是半正定的（这类态被称为**束缚[纠缠态](@entry_id:152310)**，后文将详述）。为了探测这些 PPT 纠缠态，需要更强的判据，例如**重排判据 (realignment criterion)** 或称**可计算互范数判据 (computable cross-norm criterion)**。

该判据涉及对密度矩阵 $\rho_{ij,k\ell} = \langle ij | \rho | k\ell \rangle$ 的元素进行重排，构造一个新的矩阵 $R_{ik,j\ell} = \rho_{ij,k\ell}$。判据表明，对于任何可分离态 $\rho_{sep}$，其重排矩阵的迹范数满足 $||\mathcal{R}(\rho_{sep})||_1 \le 1$。因此，如果一个态 $\rho$ 经计算发现 $||\mathcal{R}(\rho)||_1  1$，则它必定是纠缠的。这个判据在某些情况下比 PPT 判据更强，能够探测到 PPT 判据无法识别的纠缠 [@problem_id:74870]。

### 量化二分[混合态纠缠](@entry_id:142680)

量化混合态中的纠缠比[纯态](@entry_id:141688)更为复杂，不存在唯一的度量标准。不同的[纠缠度量](@entry_id:139894)（entanglement measure）通常与不同的操作任务相关联，反映了纠缠资源的不同方面。

#### 并发度与[生成纠缠](@entry_id:139137)

对于[双量子比特系统](@entry_id:203437)，**并发度 (concurrence)** 是一个广为接受的[纠缠度量](@entry_id:139894)。对于一个[密度矩阵](@entry_id:139892) $\rho$，其并发度定义为 $C(\rho) = \max(0, \lambda_1 - \lambda_2 - \lambda_3 - \lambda_4)$，其中 $\lambda_i$ 是矩阵 $\rho \tilde{\rho}$ 的[本征值](@entry_id:154894)的平方根，按降序[排列](@entry_id:136432)。这里的 $\tilde{\rho} = (\sigma_y \otimes \sigma_y) \rho^* (\sigma_y \otimes \sigma_y)$ 是对 $\rho$ 进行“自旋翻转”操作的结果。并发度的取值范围从 0（可分离态）到 1（最大[纠缠态](@entry_id:152310)）。

并发度的一个重要应用是计算**[生成纠缠](@entry_id:139137) (entanglement of formation)**, $E_f(\rho)$。$E_f$ 度量了通过混合[纯态](@entry_id:141688)来制备一系综的混合态 $\rho$ 所需的最小平均纠缠。对于[双量子比特系统](@entry_id:203437)，Wootters 给出了一个优美的解析公式：

$$
E_f(\rho) = h\left(\frac{1+\sqrt{1-C(\rho)^2}}{2}\right)
$$

其中 $h(x) = -x\log_2 x - (1-x)\log_2(1-x)$ 是[二进制熵函数](@entry_id:269003)。这个公式将一个抽象的[优化问题](@entry_id:266749)（寻找最优分解）简化为并发度的计算。例如，对于一个特定的 X 型密度矩阵，我们可以先计算其并发度（比如得到 $C(\rho)=1/4$），然后代入 Wootters 公式即可得到其[生成纠缠](@entry_id:139137)的精确值 [@problem_id:74851]。对于一个由贝尔态 $|\Phi^+\rangle$ 和乘积态 $|01\rangle$ 构成的混合态 $\rho = p |\Phi^+\rangle\langle\Phi^+| + (1-p) |01\rangle\langle 01|$，其并发度可以被精确计算出来，结果为 $C(\rho)=p$ [@problem_id:74872]，直观地反映了纠缠与贝尔态组分的[线性关系](@entry_id:267880)。

#### [对数负性](@entry_id:137607)

**[对数负性](@entry_id:137607) (logarithmic negativity)** $E_N(\rho)$ 是另一个重要且易于计算的[纠缠度量](@entry_id:139894)。它直接量化了 PPT 判据被违背的程度，定义为：

$$
E_N(\rho) = \log_2(||\rho^{T_A}||_1)
$$

其中 $||\cdot||_1$ 是迹范数，即算符[奇异值](@entry_id:152907)之和（对于厄米算符，即其[本征值](@entry_id:154894)[绝对值](@entry_id:147688)之和）。如果一个态是 PPT 的，其[部分转置](@entry_id:136776)的所有[本征值](@entry_id:154894)非负，迹范数等于迹（为 1），因此 $E_N(\rho)=0$。如果[部分转置](@entry_id:136776)有负[本征值](@entry_id:154894)，则迹范数大于 1，[对数负性](@entry_id:137607)为正。[对数负性](@entry_id:137607)是一个**[纠缠单调](@entry_id:136743)量 (entanglement monotone)**，意味着它在 LOCC 操作下不会增加。

例如，对于三比特 W 态 $|W_3\rangle = \frac{1}{\sqrt{3}}(|100\rangle+|010\rangle+|001\rangle)$，如果我们追踪掉一个[量子比特](@entry_id:137928)，剩下的双比特子系统处于一个[混合态](@entry_id:141568)。通过计算其[部分转置](@entry_id:136776)矩阵的[本征值](@entry_id:154894)，我们可以求得其迹范数，并最终得到该[混合态](@entry_id:141568)的[对数负性](@entry_id:137607) [@problem_id:74955] [@problem_id:74832]。

### 纠缠的基本属性与动力学

纠缠不仅仅是一个静态的数学属性，它还支配着量子系统的一系列动力学行为和基本性质。

#### [非局域性](@entry_id:140165)与[贝尔不等式](@entry_id:156237)

纠缠最著名的推论是**非局域性 (non-locality)**。纠缠态中的测量结果关联，其强度超出了任何基于**[局域实在论](@entry_id:144981) (local realism)** 的理论所能解释的范畴。**[贝尔不等式](@entry_id:156237) (Bell's inequality)** 及其推广形式，如 **CHSH 不等式**，为实验检验这一现象提供了框架。

CHSH 实验涉及两方（Alice 和 Bob），他们共享一个[纠缠粒子](@entry_id:153691)对，并各自独立地从两个备选设置中选择一个进行测量。CHSH 算符定义为 $B_{CHSH} = A_1 \otimes B_1 + A_1 \otimes B_2 + A_2 \otimes B_1 - A_2 \otimes B_2$。任何[局域隐变量理论](@entry_id:203716)都预测其[期望值](@entry_id:153208)的[绝对值](@entry_id:147688)不超过 2，即 $|\langle B_{CHSH} \rangle| \le 2$。然而，量子力学预测，对于[纠缠态](@entry_id:152310)，这个界限可以被违背。对于任意双比特纯态 $|\psi(\theta)\rangle = \cos\theta |00\rangle + \sin\theta |11\rangle$，通过优化测量设置，可以达到的最大[期望值](@entry_id:153208)为 $2\sqrt{1+\sin^2(2\theta)}$ [@problem_id:74867]。当 $\theta=\pi/4$ 时（最大纠缠[贝尔态](@entry_id:140749)），该值达到最大 $2\sqrt{2}$，即 **Tsirelson 界**。这表明违背的程度直接与态的纠缠程度相关。

#### 纠缠作为资源：LOCC 变换

在[量子信息](@entry_id:137721)理论中，纠缠被视为一种宝贵的资源，它不能通过[局域操作和经典通信](@entry_id:136398) (LOCC) 从无到有地创造出来。**Nielsen 的定理** 为纯态之间的确定性 LOCC 变换提供了完整的判据。一个[纯态](@entry_id:141688) $|\psi\rangle$ 可以被确定性地（以概率 1）通过 LOCC 变换为另一个纯态 $|\phi\rangle$，当且仅当 $|\psi\rangle$ 的[施密特系数](@entry_id:137823)平方向量 $\vec{\lambda}_\psi$ **主宰 (majorizes)** $|\phi\rangle$ 的[施密特系数](@entry_id:137823)平方向量 $\vec{\lambda}_\phi$，记作 $\vec{\lambda}_\psi \succ \vec{\lambda}_\phi$。

主宰关系意味着初始态的纠缠“更无序”或“更集中”。具体而言，将两个向量的元素按降序[排列](@entry_id:136432)后，$\vec{\lambda}_\psi$ 的前 $k$ 个元素之和必须大于或等于 $\vec{\lambda}_\phi$ 的前 $k$ 个元素之和，对所有 $k$ 成立。利用这个判据，我们可以精确地确定在给定初始态的情况下，哪些目标态是可以通过 LOCC 确定性地达到的 [@problem_id:74846]。

当主宰关系不成立时，确定性变换是不可能的。然而，我们仍可能以小于 1 的概率实现变换。例如，从一个非最大纠缠态 $|\psi\rangle$ 提取（或“浓缩”）出一个最大[纠缠态](@entry_id:152310) $|\Phi^+\rangle$ 的过程，其最大成功概率由初始态和目标态的[施密特系数](@entry_id:137823)共同决定 [@problem_id:74972]。

#### 束缚纠缠与纠缠破坏通道

一个惊人的发现是，并非所有纠缠都是“有用”的。存在一类被称为**束缚纠缠 (bound entanglement)** 的态，它们确实是纠缠的，但却无法通过 LOCC 从中[蒸馏](@entry_id:140660)出任何最大[纠缠态](@entry_id:152310)（如[贝尔态](@entry_id:140749)）。Horodecki 等人证明，任何具有正[部分转置](@entry_id:136776)（PPT）的纠缠态都是束缚纠缠态。这种现象只在维数高于 $2 \otimes 3$ 的系统中出现。例如，在双 qutrit 系统中，存在一个参数区间，使得 isotropic 态是纠缠的，但同时又是 PPT 的，从而构成了束缚纠缠 [@problem_id:74905]。

纠缠的性质也深刻影响着[量子信道](@entry_id:145403)的行为。一个**纠缠破坏信道 (entanglement-breaking channel)** $\mathcal{E}$ 是指，无论输入态 $\rho_{AB}$ 如何纠缠，输出态 $(\mathcal{E} \otimes \mathcal{I})(\rho_{AB})$ 总是可分离的。根据 **Choi-Jamiołkowski 同构**，一个信道是纠缠破坏的，当且仅当其对应的 **Choi 态** $\rho_{\mathcal{E}} = (\mathcal{E} \otimes \mathcal{I}) (|\Phi^+\rangle \langle \Phi^+|)$ 是可分离的。利用这一强大工具，我们可以分析具体信道的性质。例如，对于单比特**退极化信道 (depolarizing channel)** $\mathcal{E}(\rho) = (1-p)\rho + p \frac{I}{2}$，其 Choi 态是一个 Werner 态。通过应用 Werner 态的可分离性判据，我们发现当退极化概率 $p \ge 2/3$ 时，该信道变为纠缠破坏的 [@problem_id:74890]。

### [多体纠缠](@entry_id:142544)

当系统包含三个或更多子系统时，纠缠的结构变得异常丰富和复杂。与二分系统不同，[多体系统](@entry_id:144006)中的纠缠不再有唯一的分类或量化方式。

#### GHZ 态与 W 态

即使在最简单的三比特系统中，也存在两种完全不等价的纠缠类型，分别以 **Greenberger-Horne-Zeilinger (GHZ) 态**和 **W 态**为代表。
$$
|GHZ\rangle = \frac{1}{\sqrt{2}}(|000\rangle + |111\rangle)
$$
$$
|W\rangle = \frac{1}{\sqrt{3}}(|100\rangle + |010\rangle + |001\rangle)
$$
GHZ 态的纠缠是“脆弱”的：测量任何一个[量子比特](@entry_id:137928)都会摧毁整个系统的纠缠。而 W 态的纠缠是“稳健”的：测量一个[量子比特](@entry_id:137928)后，剩下的两个[量子比特](@entry_id:137928)仍然保持纠缠。

#### [纠缠的单配性](@entry_id:141408)

[多体纠缠](@entry_id:142544)的一个基本原则是**[纠缠的单配性](@entry_id:141408) (monogamy of entanglement)**。粗略地说，一个[量子比特](@entry_id:137928) A 与另一个[量子比特](@entry_id:137928) B 纠缠得越厉害，它能与其他[量子比特](@entry_id:137928) C 纠缠的程度就越有限。这种权衡关系可以通过 **Coffman-Kundu-Wootters (CKW) 不等式**来精确表述。使用并发度的平方，即**缠结 (tangle)** $\tau = C^2$，该不等式写作：
$$
\tau_{A|BC} \ge \tau_{AB} + \tau_{AC}
$$
这里 $\tau_{A|BC}$ 是 A 与子系统 (BC) 之间的纠缠，而 $\tau_{AB}$ 和 $\tau_{AC}$ 是 A 分别与 B 和 C 的二体纠缠。

这个不等式引出了**三缠结 (three-tangle)** $\tau_3$ 的概念，它被定义为“剩余”的纠缠：
$$
\tau_3 = \tau_{A|BC} - \tau_{AB} - \tau_{AC}
$$
$\tau_3$ 是一个衡量真正三方纠缠的度量。对于广义 GHZ 态 $|\psi\rangle = \alpha |000\rangle + \sqrt{1-\alpha^2} |111\rangle$，可以计算出其任意两体间的并发度都为零（$\tau_{AB} = \tau_{AC} = 0$），因此其三缠结为 $\tau_3 = \tau_{A|BC} = 4\alpha^2(1-\alpha^2)$ [@problem_id:74877]。这表明 GHZ 态的纠缠是纯粹的三方纠缠。对于更复杂的态，这个“纠缠预算”会在不同的二分划分和三分划分中进行分配 [@problem_id:74895]。

#### 全局纠缠与 SLOCC [不变量](@entry_id:148850)

除了基于划分的[纠缠度量](@entry_id:139894)，还有一些旨在捕捉系统“全局”纠缠程度的度量。**Meyer-Wallach (MW) 度量** $Q$ 就是其中之一，它定义为所有单比特约化态纯度的平均损失：
$$
Q(|\psi\rangle) = \frac{2}{N} \sum_{k=1}^{N} (1 - \text{Tr}(\rho_k^2))
$$
其中 $\rho_k$ 是第 $k$ 个[量子比特](@entry_id:137928)的[约化密度矩阵](@entry_id:146315)。这个度量反映了信息从局域子系统“泄露”到全局关联中的程度。对于一个 N-比特的[图态](@entry_id:142848)（例如[星形图](@entry_id:271558)态），如果每个[量子比特](@entry_id:137928)都至少与一个其他[量子比特](@entry_id:137928)相连，那么它的[约化密度矩阵](@entry_id:146315)就是[最大混合态](@entry_id:137775)，$\rho_k=\frac{1}{2}I$，导致 $\text{Tr}(\rho_k^2) = 1/2$。此时 MW 度量达到其最大值 1，表示高度的全局纠缠 [@problem_id:74824]。

更进一步，为了对[多体纠缠](@entry_id:142544)态进行分类，人们研究在**随机[局域操作和经典通信](@entry_id:136398) (SLOCC)** 下的[不变量](@entry_id:148850)。如果两个态可以通过 SLOCC相互转换，则它们被认为是同一纠缠类型。对于三比特系统，最简单的 SLOCC [不变量](@entry_id:148850)是 **Cayley [超行列式](@entry_id:755853) (hyperdeterminant)**。对于一个态 $|\Psi\rangle = \sum_{i,j,k=0}^1 A_{ijk} |ijk\rangle$，其系数张量 $A_{ijk}$ 的[超行列式](@entry_id:755853) $\text{HDet}(A)$ 若不为零，则表明该态属于 GHZ 类型 [@problem_id:74906]。对于四比特系统，也存在类似的 $2 \times 2 \times 2 \times 2$ [超行列式](@entry_id:755853)。例如，通过计算可以发现，四比特 Dicke 态 $|D_4^2\rangle$ 的[超行列式](@entry_id:755853)为一个非零的负值 [@problem_id:74812]，这揭示了它所具有的独特而复杂的四方纠缠结构，不同于 GHZ 态或 W 态的推广。这些[不变量](@entry_id:148850)为我们绘制复杂的[多体纠缠](@entry_id:142544)世界版图提供了关键的数学工具。