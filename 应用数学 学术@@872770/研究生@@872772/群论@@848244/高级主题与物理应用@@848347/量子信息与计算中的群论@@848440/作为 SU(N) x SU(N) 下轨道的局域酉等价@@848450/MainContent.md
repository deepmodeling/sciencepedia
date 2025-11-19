## 引言
量子纠缠是现代物理学的核心概念之一，但对其进行分类和量化仍是一项根本性的挑战。传统方法往往依赖于复杂的代数运算，而本文将引入一个更为直观且深刻的视角：几何。我们将把[量子态](@entry_id:146142)的集合视为一个巨大的几何空间，而所有物理上等价的[纠缠态](@entry_id:152310)则在其中形成优美的“[轨道](@entry_id:137151)”。这种方法不仅揭示了纠缠的内在结构，也构建了[量子信息](@entry_id:137721)与数学及物理学其他前沿领域的桥梁。

本文旨在系统地阐述这一几何框架。在第一章“原理与机制”中，我们将建立群作用、[轨道](@entry_id:137151)、稳定子和[不变量](@entry_id:148850)等核心数学概念。随后，在“应用与跨学科联系”一章中，我们将展示如何运用这些工具来[量化纠缠](@entry_id:144669)，并探讨其与凝聚态物理及规范场论的深刻联系。最后，“动手实践”部分将通过具体问题加深您的理解。让我们首先深入探讨将[局域酉等价](@entry_id:198966)类视为几何[轨道](@entry_id:137151)的具体原理与机制。

## 原理与机制

本章旨在深入探讨[量子态](@entry_id:146142)在局域[酉变换](@entry_id:152599)下的几何结构。我们将揭示物理上等效的[量子态](@entry_id:146142)如何构成一个几何[轨道](@entry_id:137151)，并阐述这些[轨道](@entry_id:137151)的性质（如维度和曲率）如何量化了[量子态](@entry_id:146142)的纠缠特性。我们将从[群作用](@entry_id:268812)的基本概念出发，逐步建立起[轨道](@entry_id:137151)、[切空间](@entry_id:199137)、稳定子和[不变量](@entry_id:148850)等核心概念，并通过具体的计算实例来阐明这些抽象理论的物理意义。

### 局部[酉变换](@entry_id:152599)群的作用

在[复合量子系统](@entry_id:193313)中，例如一个由子系统A和B组成的二体系统，其[希尔伯特空间](@entry_id:261193)为 $\mathcal{H} = \mathcal{H}_A \otimes \mathcal{H}_B$。对单个子系统进行的、不影响其他子系统的操作被称为**局域操作**。当我们考虑那些保持[量子态](@entry_id:146142)范数不变的可逆操作时，我们自然地引入了**局域[酉变换](@entry_id:152599) (Local Unitary, LU) 变换**。对于一个希尔伯特空间维度为 $\mathbb{C}^{d_A} \otimes \mathbb{C}^{d_B}$ 的系统，这些变换构成的群是 $G = U(d_A) \times U(d_B)$。由于[全局相位](@entry_id:147947)在物理上是不可观测的，我们通常关注那些[行列式](@entry_id:142978)为1的特殊酉矩阵，它们构成了**特殊局域[酉变换](@entry_id:152599)群** $G = SU(d_A) \times SU(d_B)$。

一个变换 $g = U_A \otimes U_B \in G$ 作用在一个纯态 $|\psi\rangle \in \mathcal{H}$ 上，会产生一个新的[量子态](@entry_id:146142) $|\psi'\rangle = g|\psi\rangle$。从物理角度看，由于纠缠是一种内蕴的、非局域的关联性质，它不应被局域操作所改变。因此，$|\psi\rangle$ 和 $|\psi'\rangle$ 拥有完全相同的纠缠特性，被认为是**[局域酉等价](@entry_id:198966)**的。

从一个给定的初始态 $|\psi\rangle$ 出发，通过所有可能的局域[酉变换](@entry_id:152599)，我们可以得到一个态的集合。这个集合在几何上被称为态 $|\psi\rangle$ 在群 $G$ 作用下的**[轨道](@entry_id:137151) (orbit)**，记为 $\mathcal{O}_{|\psi\rangle}$。
$$
\mathcal{O}_{|\psi\rangle} = \{ (U_A \otimes U_B)|\psi\rangle \mid U_A \in SU(d_A), U_B \in SU(d_B) \}
$$
同一个[轨道](@entry_id:137151)上的所有[量子态](@entry_id:146142)构成了同一个**纠缠等价类**。因此，研究量子纠缠的[分类问题](@entry_id:637153)，在很大程度上可以转化为研究这些由局域酉群作用产生的[轨道](@entry_id:137151)的几何与拓扑性质。

### [轨道](@entry_id:137151)的几何结构

将[量子态空间](@entry_id:197873)视为一个几何空间，[轨道](@entry_id:137151)就是嵌入其中的子流形。[流形](@entry_id:153038)的几何性质，如距离和曲率，为我们理解局域操作对[量子态](@entry_id:146142)的影响提供了有力的数学工具。

当一个微小的局域[酉变换](@entry_id:152599)作用在态上时，态矢量会在[希尔伯特空间](@entry_id:261193)中移动一小段距离。我们可以用标准的**[欧几里得距离](@entry_id:143990)**来衡量这种变化。对于两个已归一化的态 $|\psi_1\rangle$ 和 $|\psi_2\rangle$，它们之间的[欧几里得距离](@entry_id:143990) $D$ 定义为：
$$
D(|\psi_1\rangle, |\psi_2\rangle) = \sqrt{\langle \psi_1 - \psi_2 | \psi_1 - \psi_2 \rangle} = \sqrt{2 - 2\Re\langle\psi_1|\psi_2\rangle}
$$
其中 $\Re$ 表示取实部。这个距离直观地反映了两个态矢量在[复向量空间](@entry_id:264355)中的分离程度。

为了具体理解这一点，我们可以考察一个沿[轨道](@entry_id:137151)移动的实例。考虑一个由参数 $p$ 控制的两[量子比特](@entry_id:137928)部分纠缠态：
$$
|\psi_p\rangle = \sqrt{p}|00\rangle + \sqrt{1-p}|11\rangle
$$
我们对其施加一个局域旋转操作 $U = U_A \otimes U_B$，其中 $U_A = \exp(i\alpha\sigma_x)$ 和 $U_B = \exp(i\beta\sigma_x)$ 是分别绕x轴的旋转。这里 $\sigma_x$ 是泡利X矩阵。变换后的态为 $|\psi'_p\rangle = U|\psi_p\rangle$。我们感兴趣的是初末态之间的距离。[内积](@entry_id:158127) $\langle\psi_p|U|\psi_p\rangle$ 可以被计算出来：
$$
\langle\psi_p|U|\psi_p\rangle = \cos(\alpha)\cos(\beta) - 2\sqrt{p(1-p)}\sin(\alpha)\sin(\beta)
$$
于是，距离的平方为 $D^2 = 2(1 - \Re\langle\psi_p|U|\psi_p\rangle)$。例如，当代入特定参数 $p = \frac{1}{3}$，$\alpha = \frac{\pi}{4}$ 以及 $\beta = \frac{\pi}{2}$ 时，我们得到 $\cos(\alpha)\cos(\beta) = 0$ 和 $\sin(\alpha)\sin(\beta) = \frac{\sqrt{2}}{2}$。此外，$2\sqrt{p(1-p)} = \frac{2\sqrt{2}}{3}$。将这些值代入，可得 $\langle\psi_p|U|\psi_p\rangle = -\frac{2}{3}$。因此，距离的平方为 $D^2 = 2(1 - (-\frac{2}{3})) = \frac{10}{3}$，即 $D = \sqrt{\frac{10}{3}}$。这个计算清晰地展示了[局域酉操作](@entry_id:198146)如何使[量子态](@entry_id:146142)在其[轨道](@entry_id:137151)上移动，并产生一个可度量的位移 [@problem_id:720188]。

### 切空间与李代数作用

为了深入研究[轨道](@entry_id:137151)的局域几何性质，我们转向分析无穷小的变换。任何一个[酉算子](@entry_id:151194) $U$ 都可以表示为 $U = \exp(iH)$，其中 $H$ 是一个厄米算子。对于 $SU(d)$ 群中的元素，厄米算子 $H$ 还需要满足迹为零的条件。这些厄米算子构成了群的**李代数**，记为 $\mathfrak{su}(d)$。一个无穷小的局域[酉变换](@entry_id:152599)可以写成 $U \approx I + i(\epsilon_A H_A \otimes I + I \otimes \epsilon_B H_B)$，其中 $H_A \in \mathfrak{su}(d_A)$，$H_B \in \mathfrak{su}(d_B)$ 是李代数的生成元，$\epsilon_{A,B}$ 是无穷小参数。

当一个无穷小变换作用在态 $|\psi\rangle$ 上时，它产生的变化方向由向量 $i(H_A \otimes I + I \otimes H_B)|\psi\rangle$ 决定。所有由李代数 $\mathfrak{g} = \mathfrak{su}(d_A) \oplus \mathfrak{su}(d_B)$ 的元素作用在 $|\psi\rangle$ 上生成的向量，张成了一个[线性空间](@entry_id:151108)，称为在 $|\psi\rangle$ 点的**切空间 (tangent space)**。这些向量 $|v_H\rangle = i(H_A \otimes I + I \otimes H_B)|\psi\rangle$ 都是[轨道](@entry_id:137151)在该点的**[切向量](@entry_id:265494) (tangent vectors)**。

考虑一个由[施密特分解](@entry_id:145934)形式给出的两比特[纠缠态](@entry_id:152310) $|\psi(\theta)\rangle = \cos\theta |00\rangle + \sin\theta |11\rangle$。我们考察一个由局域操作 $L_z^A = -i\sigma_z^A \otimes I^B$ 生成的切向量，其中 $\sigma_z$ 是泡利[Z矩阵](@entry_id:178741)。这个算子等价于 $H_A = \sigma_z, H_B = 0$。作用在 $|\psi(\theta)\rangle$ 上，我们得到切向量 $|v\rangle = i(\sigma_z \otimes I)|\psi(\theta)\rangle = i\cos\theta|00\rangle - i\sin\theta|11\rangle$。这个切向量与原初态 $|\psi(\theta)\rangle$ 的[内积](@entry_id:158127)为 $\langle\psi(\theta)|v\rangle = i\cos^2\theta - i\sin^2\theta = i\cos(2\theta)$。其模长的平方是 $|\langle\psi(\theta)|v\rangle|^2 = \cos^2(2\theta)$。对于 $\theta=\frac{\pi}{6}$ 的情况，这个值是 $\cos^2(\frac{\pi}{3}) = \frac{1}{4}$ [@problem_id:720183]。这个投影不为零，说明[切向量](@entry_id:265494)有沿着原态矢量方向的分量，这对应于一个纯粹的相位变化。在考虑物理状态所在的[射影希尔伯特空间](@entry_id:188975)时，只有与原态正交的[切向量](@entry_id:265494)分量才对应于[轨道](@entry_id:137151)上的真实移动。

[切空间](@entry_id:199137)本身也具有丰富的几何结构，例如，我们可以定义切向量之间的[内积](@entry_id:158127)，这个[内积](@entry_id:158127)由背景希尔伯特空间自然诱导。考察两个不同的[切向量](@entry_id:265494)，它们的[内积](@entry_id:158127)可以揭示[轨道](@entry_id:137151)几何的更多信息。例如，在两量子三态（qutrit）系统 $\mathbb{C}^3 \otimes \mathbb{C}^3$ 中，考虑最大[纠缠态](@entry_id:152310) $|\Psi\rangle = \frac{1}{\sqrt{3}} \sum_{k=0}^{2} |k k\rangle$。我们由两个不同的李代数生成元——[盖尔曼矩阵](@entry_id:159244) $\lambda_1$ 和 $\lambda_2$ ——在不同子系统上作用，生成两个[切向量](@entry_id:265494)：
$$
|v_1\rangle = i(\lambda_1 \otimes I)|\Psi\rangle, \quad |v_2\rangle = i(I \otimes \lambda_2)|\Psi\rangle
$$
它们的[内积](@entry_id:158127)为 $\langle v_1 | v_2 \rangle = \langle\Psi| (\lambda_1 \otimes I)^\dagger (I \otimes \lambda_2) |\Psi\rangle = \langle\Psi| \lambda_1 \otimes \lambda_2 |\Psi\rangle$。通过计算，可以发现 $\langle v_1 | v_2 \rangle = \frac{1}{3}\sum_{k,l=0}^{2} \langle k|\lambda_1|l\rangle \langle k|\lambda_2|l\rangle = \frac{1}{3}\sum_{k,l=0}^{2} (\lambda_1)_{kl} (\lambda_2)_{kl} = \frac{1}{3}[1 \cdot (-i) + 1 \cdot i] = 0$。这意味着由局域算子 $\lambda_1$ 在子系统A上产生的运动方向，与由局域算子 $\lambda_2$ 在子系统B上产生的运动方向是正交的。这反映了切空间的一种分解属性 [@problem_id:720208]。

### [稳定子群](@entry_id:137216)与[轨道](@entry_id:137151)维度

对于给定的态 $|\psi\rangle$，并非所有[局域酉操作](@entry_id:198146)都会改变它。那些保持态不变（或只产生一个[全局相位](@entry_id:147947)）的变换 $g = U_A \otimes U_B$ 的集合，构成 $G$ 的一个[子群](@entry_id:146164)，称为 $|\psi\rangle$ 的**[稳定子群](@entry_id:137216) (stabilizer subgroup)**，记为 $S_{|\psi\rangle}$。
$$
S_{|\psi\rangle} = \{ (U_A, U_B) \in G \mid (U_A \otimes U_B)|\psi\rangle = e^{i\phi}|\psi\rangle \text{ for some } \phi \in \mathbb{R} \}
$$
[稳定子群](@entry_id:137216)的大小和结构反映了[量子态](@entry_id:146142)的对称性。对称性越高的态（如最大纠缠态），其[稳定子群](@entry_id:137216)越大；而一个“随机”或“泛型”的态，其对称性很低，[稳定子群](@entry_id:137216)通常很小。

我们可以通过一个具体的例子来理解稳定子的概念。考虑一个在 $\mathbb{C}^3 \otimes \mathbb{C}^3$ 空间中的纠缠态 $|\Psi\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$。假设我们对第一个三态量子系统施加了一个对角酉操作 $U_A = \text{diag}(e^{i\alpha}, e^{i\beta}, e^{-i(\alpha+\beta)})$。为了使总的态 $|\Psi\rangle$ 保持不变，我们必须找到一个补偿操作 $V_B \in SU(3)$，使得 $(U_A \otimes V_B)|\Psi\rangle = |\Psi\rangle$。将此作用在 $|\Psi\rangle$ 上，我们得到：
$$
\frac{1}{\sqrt{2}} (U_A|0\rangle \otimes V_B|0\rangle + U_A|1\rangle \otimes V_B|1\rangle) = \frac{1}{\sqrt{2}} (e^{i\alpha}|0\rangle \otimes V_B|0\rangle + e^{i\beta}|1\rangle \otimes V_B|1\rangle)
$$
为了使其等于原态 $\frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$，必须有 $e^{i\alpha}V_B|0\rangle = |0\rangle$ 和 $e^{i\beta}V_B|1\rangle = |1\rangle$。这意味着 $V_B$ 必须是一个对角矩阵，其对角元满足 $v_0 = e^{-i\alpha}$ 和 $v_1 = e^{-i\beta}$。由于 $V_B \in SU(3)$，其[行列式](@entry_id:142978)必须为1，即 $v_0 v_1 v_2 = 1$，这确定了第三个对角元 $v_2 = e^{i(\alpha+\beta)}$。因此，对于给定的 $U_A$，存在一个唯一的 $V_B$ 使 $(U_A, V_B)$ 成为稳定子对。例如，当 $\alpha = \frac{\pi}{3}, \beta = \frac{\pi}{6}$ 时，我们可以计算出 $V_B$ 的迹为 $\mathrm{Tr}(V_B) = e^{-i\pi/3} + e^{-i\pi/6} + e^{i\pi/2} = \frac{1+\sqrt{3}}{2} + i\frac{1-\sqrt{3}}{2}$ [@problem_id:720179]。

[轨道](@entry_id:137151)的维度与[稳定子群](@entry_id:137216)的维度之间存在一个深刻的联系，这由**[轨道](@entry_id:137151)-稳定子定理**给出：
$$
\dim(\mathcal{O}_{|\psi\rangle}) = \dim(G) - \dim(S_{|\psi\rangle})
$$
其中 $\dim$ 表示[李群](@entry_id:137659)作为[流形](@entry_id:153038)的维度。对于 $SU(d)$，其维度是 $d^2-1$。因此，对于二体系统，$\dim(G) = (d_A^2-1) + (d_B^2-1)$。此定理表明，[轨道](@entry_id:137151)的维度（即态的自由度）等于总的变换自由度减去保持态不变的那些变换的自由度。

要应用此定理，我们首先需要计算[稳定子群](@entry_id:137216)的维度。考虑一个两比特态 $|\psi\rangle = |00\rangle + i|11\rangle$，它与贝尔态 $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$ 是[局域酉等价](@entry_id:198966)的，因此它们有相同维度的稳定子。对于 $|\Phi^+\rangle$，其稳定子的李代数 $\mathfrak{s}_{|\Phi^+\rangle}$ 由满足 $(h_A \otimes I + I \otimes h_B)|\Phi^+\rangle \propto |\Phi^+\rangle$ 的李代数元素对 $(h_A, h_B) \in \mathfrak{su}(2) \oplus \mathfrak{su}(2)$ 构成。这个条件等价于 $h_A + h_B^T = cI$，其中 $c$ 是一个常数。由于 $h_A$ 和 $h_B$ 都是无迹的，对等式两边取迹可得 $c=0$。因此，稳定子代数的元素满足 $h_A = -h_B^T$。这意味着对于任意一个 $h_A \in \mathfrak{su}(2)$，相应的 $h_B$ 是唯一确定的。所以，稳定子代数的维度等于 $\mathfrak{su}(2)$ 的维度，即 $\dim(\mathfrak{s}_{|\Phi^+\rangle}) = \dim(\mathfrak{su}(2)) = 2^2-1 = 3$。因此，[贝尔态](@entry_id:140749)的[稳定子群](@entry_id:137216)维度为3 [@problem_id:720218]。

现在我们可以计算[轨道](@entry_id:137151)的维度。对于一个由两个三态量子系统（qutrit）构成的系统，变换群为 $G = SU(3) \times SU(3)$，其维度为 $\dim(G) = (3^2-1) + (3^2-1) = 16$。考虑该系统中的最大纠缠态 $|\Psi_{ME}\rangle = \frac{1}{\sqrt{3}}\sum_{i=0}^2 |ii\rangle$。其[稳定子群](@entry_id:137216)被证明与 $SU(3)$ 同构（在忽略离散部[分时](@entry_id:274419)），因此 $\dim(S_{|\Psi_{ME}\rangle}) = \dim(SU(3)) = 8$。根据[轨道](@entry_id:137151)-稳定子定理，该态的[轨道](@entry_id:137151)维度为 $\dim(\mathcal{O}_{|\Psi_{ME}\rangle}) = 16 - 8 = 8$ [@problem_id:720195]。

这个方法也可以推广到[多体系统](@entry_id:144006)。例如，对于一个[三量子比特](@entry_id:146257)系统，局域[酉群](@entry_id:138602)为 $G = SU(2) \times SU(2) \times SU(2)$，其维度为 $\dim(G) = 3 \times (2^2-1) = 9$。著名的[W态](@entry_id:180654) $|W\rangle = \frac{1}{\sqrt{3}}(|100\rangle+|010\rangle+|001\rangle)$ 是一个重要的纠缠类型。通过分析其稳定子的李代数，可以发现其维度为1。因此，[W态](@entry_id:180654)的[轨道](@entry_id:137151)维度为 $\dim(\mathcal{O}_{|W\rangle}) = 9 - 1 = 8$ [@problem_id:720241]。这个结果与三比特[GHZ态](@entry_id:182114)的[轨道](@entry_id:137151)维度（为6）不同，从几何上证实了[W态](@entry_id:180654)和[GHZ态](@entry_id:182114)属于完全不同的纠缠类别。

### 局部酉[不变量](@entry_id:148850)与[纠缠分类](@entry_id:198383)

[轨道](@entry_id:137151)-稳定子定理提供了一种从顶层到底层的方法来表征[轨道](@entry_id:137151)，但如果我们想判断两个给定的态 $|\psi_1\rangle$ 和 $|\psi_2\rangle$ 是否在同一个[轨道](@entry_id:137151)上，逐一尝试所有局域[酉变换](@entry_id:152599)是不现实的。我们需要一种更直接的方法，即计算一些在局域[酉变换](@entry_id:152599)下保持不变的量，即**局域酉[不变量](@entry_id:148850) (LU invariants)**。如果任何一个[不变量](@entry_id:148850)在两个态上取值不同，那么它们必然属于不同的[轨道](@entry_id:137151)。

对于二体[纯态](@entry_id:141688)，一个完备的局域酉[不变量](@entry_id:148850)集合由**[施密特系数](@entry_id:137823)**给出。任何二体[纯态](@entry_id:141688) $|\psi\rangle = \sum_{i,j} C_{ij}|i\rangle_A \otimes |j\rangle_B$ 都可以通过局域[酉变换](@entry_id:152599)写成其[标准形式](@entry_id:153058)，即**[施密特分解](@entry_id:145934)**：
$$
|\psi\rangle = \sum_{k} s_k |u_k\rangle_A \otimes |v_k\rangle_B
$$
其中 $\{|u_k\rangle_A\}$ 和 $\{|v_k\rangle_B\}$ 是各自子系统中的标准正交基，而非负实数 $s_k$ 被称为**[施密特系数](@entry_id:137823)**。从线性代数的角度看，[施密特系数](@entry_id:137823) $s_k$ 正是态的[系数矩阵](@entry_id:151473) $C$ 的**奇异值**。[奇异值](@entry_id:152907)是矩阵 $C^\dagger C$ 的[特征值](@entry_id:154894)的平方根。[施密特系数](@entry_id:137823)的集合（谱）在局域[酉变换](@entry_id:152599)下是唯一的（不计排序）。

因此，要计算一个态的[施密特系数](@entry_id:137823)，我们只需计算其系数矩阵 $C$ 的[奇异值](@entry_id:152907)。例如，考虑一个由非归一化[系数矩阵](@entry_id:151473) $C = \begin{pmatrix} 1  1 \\ 0  1 \end{pmatrix}$ 表示的两比特态。我们计算 $C^\dagger C = \begin{pmatrix} 1  1 \\ 1  2 \end{pmatrix}$。其[特征值](@entry_id:154894)由[特征方程](@entry_id:265849) $\lambda^2 - 3\lambda + 1 = 0$ 给出，解为 $\lambda_{\pm} = \frac{3 \pm \sqrt{5}}{2}$。因此，非归一化的[施密特系数](@entry_id:137823)为 $s_{\pm} = \sqrt{\frac{3 \pm \sqrt{5}}{2}}$。这些系数本身不是[不变量](@entry_id:148850)（因为它们依赖于态的归一化），但它们的比率是。最小与最大[施密特系数](@entry_id:137823)之比为 $\frac{s_-}{s_+} = \sqrt{\frac{3-\sqrt{5}}{3+\sqrt{5}}}$。这个比值是一个局域酉[不变量](@entry_id:148850)，可以用来区分不同的纠缠类型 [@problem_id:720329]。

任何只依赖于[施密特系数](@entry_id:137823)的函数也都是局域酉[不变量](@entry_id:148850)，这些函数通常被用作**[纠缠度量](@entry_id:139894)**。一个常见的例子是**线性熵** $S_L$。对于一个归一化二体纯态，其子系统A的[约化密度矩阵](@entry_id:146315)为 $\rho_A = \mathrm{Tr}_B(|\psi\rangle\langle\psi|)$。线性熵定义为 $S_L(\rho_A) = 1 - \mathrm{Tr}(\rho_A^2)$。可以证明，$\mathrm{Tr}(\rho_A^2) = \sum_k s_k^4$，其中 $s_k$ 是归一化后的[施密特系数](@entry_id:137823)（满足 $\sum_k s_k^2 = 1$）。因此，$S_L = 1 - \sum_k s_k^4$。

例如，考虑一个由非归一化[系数矩阵](@entry_id:151473) $C_{un} = I + i\sigma_y = \begin{pmatrix} 1  1 \\ -1  1 \end{pmatrix}$ 定义的两比特态。首先我们计算归一化因子：$\mathrm{Tr}(C_{un}^\dagger C_{un}) = 4$。所以归一化后的系数矩阵为 $C = \frac{1}{2}C_{un}$。接着我们计算 $C C^\dagger = \frac{1}{4}C_{un}C_{un}^\dagger = \frac{1}{2}I$。它的[特征值](@entry_id:154894)为 $\frac{1}{2}, \frac{1}{2}$。这些就是归一化的[施密特系数](@entry_id:137823)的平方，即 $s_0^2=s_1^2=\frac{1}{2}$。这意味着该态是一个最大纠缠态。其线性熵为 $S_L = 1 - (s_0^4 + s_1^4) = 1 - ((\frac{1}{2})^2 + (\frac{1}{2})^2) = 1 - \frac{1}{2} = \frac{1}{2}$。这个值是两比特系统线性熵的最大可[能值](@entry_id:187992)，确认了该态的最大纠缠性质 [@problem_id:720202]。

### [轨道](@entry_id:137151)间的距离

既然不同的[轨道](@entry_id:137151)代表了不同的纠缠类型，一个自然的问题是：这些纠缠类型在几何上相距多远？为此，我们需要一个在整个[射影希尔伯特空间](@entry_id:188975)上定义的[距离度量](@entry_id:636073)。最自然的度量是**Fubini-Study距离**，它度量了两个[量子态](@entry_id:146142)（作为希尔伯特空间中的“射线”）之间的夹角。对于两个归一化纯态 $|\psi\rangle$ 和 $|\phi\rangle$，Fubini-Study距离定义为：
$$
d_{FS}(|\psi\rangle, |\phi\rangle) = \arccos(|\langle\psi|\phi\rangle|)
$$
这个距离在 $0$ (当态相同时) 和 $\frac{\pi}{2}$ (当态正交时) 之间取值。

两个[轨道](@entry_id:137151) $\mathcal{O}_{|\Psi_1\rangle}$ 和 $\mathcal{O}_{|\Psi_2\rangle}$ 之间的最小距离定义为从两个[轨道](@entry_id:137151)中各取一个态所能达到的最小Fubini-Study距离。这等价于寻找最大化保真度（[内积](@entry_id:158127)的模）的操作：
$$
D(\mathcal{O}_{|\Psi_1\rangle}, \mathcal{O}_{|\Psi_2\rangle}) = \min_{U,V} d_{FS}(U|\Psi_1\rangle, V|\Psi_2\rangle) = \arccos\left(\max_{U_A, U_B} |\langle\Psi_1| U_A \otimes U_B |\Psi_2\rangle|\right)
$$
一个深刻的结论是，这个最大保真度可以直接通过两个态的[施密特系数](@entry_id:137823)谱计算得出。如果 $|\Psi_1\rangle$ 和 $|\Psi_2\rangle$ 的归一化[施密特系数](@entry_id:137823)分别为 $\{s_{1,k}\}$ 和 $\{s_{2,k}\}$，那么最大保真度为：
$$
\max_{U_A, U_B} |\langle\Psi_1| U_A \otimes U_B |\Psi_2\rangle| = \sum_k s_{1,k} s_{2,k}
$$
这个公式的直观解释是，最大化交叠是通过局域[酉变换](@entry_id:152599)将两个态的施密特基对齐。

我们用一个例子来说明这个强大的工具。考虑在 $\mathbb{C}^3 \otimes \mathbb{C}^3$ 空间中的两个态：一个[施密特秩](@entry_id:154893)为2的贝尔型态 $|\Psi_A\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$，和一个[施密特秩](@entry_id:154893)为3的最大纠缠态 $|\Psi_B\rangle = \frac{1}{\sqrt{3}}(|00\rangle + |11\rangle + |22\rangle)$。它们的归一化[施密特系数](@entry_id:137823)分别为 $\{s_{A,k}\} = \{\frac{1}{\sqrt{2}}, \frac{1}{\sqrt{2}}, 0\}$ 和 $\{s_{B,k}\} = \{\frac{1}{\sqrt{3}}, \frac{1}{\sqrt{3}}, \frac{1}{\sqrt{3}}\}$。它们[轨道](@entry_id:137151)间的最大保真度为：
$$
F_{\max} = \sum_k s_{A,k} s_{B,k} = \frac{1}{\sqrt{2}}\frac{1}{\sqrt{3}} + \frac{1}{\sqrt{2}}\frac{1}{\sqrt{3}} + 0 \cdot \frac{1}{\sqrt{3}} = \frac{2}{\sqrt{6}} = \sqrt{\frac{2}{3}}
$$
因此，这两个纠缠[等价类](@entry_id:156032)之间的最小Fubini-Study距离为 $D(\mathcal{O}_{|\Psi_A\rangle}, \mathcal{O}_{|\Psi_B\rangle}) = \arccos\left(\sqrt{\frac{2}{3}}\right)$ [@problem_id:720147]。这个结果将抽象的[轨道](@entry_id:137151)间距离与具体的、可计算的施密特谱联系起来，完美地体现了纠缠的几何图像。