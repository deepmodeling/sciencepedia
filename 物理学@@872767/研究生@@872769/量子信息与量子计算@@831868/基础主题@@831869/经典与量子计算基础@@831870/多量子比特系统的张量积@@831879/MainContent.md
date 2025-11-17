## 引言
从单个[量子比特](@entry_id:137928)到[多量子比特系统](@entry_id:142942)的跨越，是量子信息与计算领域实现指数级能力增长的关键。然而，描述这些由多个部分构成的[复合量子系统](@entry_id:193313)需要一个严谨而强大的数学框架，这便是[张量积](@entry_id:140694)的核心作用。[张量积](@entry_id:140694)不仅为我们提供了描述多体[量子态](@entry_id:146142)和它们之间相互作用的语言，更重要的是，它揭示了量子世界最深刻、最反直觉的特性——量子纠缠。理解这一框架是掌握现代[量子技术](@entry_id:142946)和探索前沿量子物理的基石。

本文旨在系统性地解析[多量子比特系统](@entry_id:142942)中的张量积及其推论。在“原理与机制”一章中，我们将建立复合系统的[基本表示](@entry_id:157678)法，深入探讨量子纠缠的描述与量化，并介绍对称性原理和[张量网络](@entry_id:142149)等高级工具。随后的“应用与跨学科联系”一章将展示这些理论在[量子计算](@entry_id:142712)、[量子通信](@entry_id:138989)、量子纠错以及凝聚态物理等领域的具体应用，揭示其作为连接不同学科的桥梁作用。最后，通过“动手实践”部分提供的一系列精选问题，您将有机会亲手应用所学知识，加深对这一核心概念的理解。

## 原理与机制

在[量子信息](@entry_id:137721)与[量子计算](@entry_id:142712)领域，单个[量子比特](@entry_id:137928)是基本的构建单元，但真正的计算能力和丰富的物理现象源于多个[量子比特](@entry_id:137928)的组合。本章将深入探讨描述[多量子比特系统](@entry_id:142942)的核心数学框架——张量积，并以此为基础，系统地阐述[复合量子系统](@entry_id:193313)的基本原理和关键机制。我们将从[状态和](@entry_id:193625)算符的表示出发，逐步深入到[量子纠缠](@entry_id:136576)的量化、对称性原理的应用，直至介绍用于高效描述多体[量子态](@entry_id:146142)的现代工具。

### [复合量子系统](@entry_id:193313)的表示

描述一个由 $N$ 个[量子比特](@entry_id:137928)组成的复合系统，其[希尔伯特空间](@entry_id:261193) $\mathcal{H}$ 是单个[量子比特](@entry_id:137928)希尔伯特空间 $\mathcal{H}_i \cong \mathbb{C}^2$ 的[张量积](@entry_id:140694)：
$$ \mathcal{H} = \mathcal{H}_1 \otimes \mathcal{H}_2 \otimes \dots \otimes \mathcal{H}_N \cong (\mathbb{C}^2)^{\otimes N} $$
该空间的维度为 $2^N$。如果单比特的计算[基矢](@entry_id:199546)为 $\{|0\rangle, |1\rangle\}$，那么 $N$ 比特系统的计算[基矢](@entry_id:199546)就是这些单比特[基矢](@entry_id:199546)的[张量积](@entry_id:140694)，记为 $|i_1 i_2 \dots i_N\rangle \equiv |i_1\rangle \otimes |i_2\rangle \otimes \dots \otimes |i_N\rangle$，其中 $i_k \in \{0, 1\}$。

一个[多量子比特系统](@entry_id:142942)的普遍[纯态](@entry_id:141688)是这些[基矢](@entry_id:199546)的线性叠加：
$$ |\psi\rangle = \sum_{i_1, \dots, i_N = 0}^{1} c_{i_1 \dots i_N} |i_1 i_2 \dots i_N\rangle $$
其中 $c_{i_1 \dots i_N}$ 是复数振幅，满足[归一化条件](@entry_id:156486) $\sum |c_{i_1 \dots i_N}|^2 = 1$。

作用于复合系统上的算符同样通过[张量积](@entry_id:140694)来构建。一个作用于第 $k$ 个[量子比特](@entry_id:137928)的单比特算符 $O_k$，在整个 $N$ 比特系统上的表示是 $I_1 \otimes \dots \otimes I_{k-1} \otimes O_k \otimes I_{k+1} \otimes \dots \otimes I_N$。为简洁起见，通常会省略恒等算符 $I$，例如 $X_1$ 表示 $X \otimes I \otimes \dots \otimes I$。一个更普适的多体算符是[单体](@entry_id:136559)算符[张量积](@entry_id:140694)的线性组合。例如，一个作用于两比特系统的算符 $A \otimes B$，其作用在[基矢](@entry_id:199546) $|ij\rangle$ 上定义为 $(A \otimes B) |ij\rangle = (A|i\rangle) \otimes (B|j\rangle)$。

这些张量积算符的代数性质直接源于其构成部分。例如，两个张量积算符的乘积遵循规则 $(A \otimes B)(C \otimes D) = (AC) \otimes (BD)$。这使得我们可以方便地计算多体算符的代数关系，如对易子。考虑一个两比特系统上的算符 $M = [H \otimes X, Z \otimes Y]$，其中 $H = \frac{1}{\sqrt{2}}(X+Z)$ 是哈达玛门，而 $X, Y, Z$ 是[泡利算符](@entry_id:144061)。我们可以利用[张量积](@entry_id:140694)的[乘法规则](@entry_id:197368)以及泡利代数（如 $XZ = -iY$, $XY=iZ$ 等）来简化这个表达式 [@problem_id:142033]。
$$ M = (H \otimes X)(Z \otimes Y) - (Z \otimes Y)(H \otimes X) = (HZ) \otimes (XY) - (ZH) \otimes (YX) $$
代入泡利代数关系 $XY = iZ$ 和 $YX = -iZ$，我们得到：
$$ M = i(HZ + ZH) \otimes Z $$
进一步计算 $HZ+ZH = \frac{1}{\sqrt{2}}([X,Z]_+ + 2Z^2) = \frac{1}{\sqrt{2}}(0 + 2I) = \sqrt{2}I$，其中 $[A,B]_+ = AB+BA$ 是[反对易子](@entry_id:139754)。最终得到一个简洁的形式 $M = i\sqrt{2}(I \otimes Z)$。这个例子展示了，看似复杂的多体算符可以通过其局部的[代数结构](@entry_id:137052)得以简化。

### 量子纠缠：描述与量化

张量积结构允许存在一类特殊的态，称为**纠缠态 (entangled states)**，它们无法被写成单个子系统态的乘积，即**可分离态 (separable states)**。对于一个两比特[纯态](@entry_id:141688) $|\psi\rangle$，如果它不能表示为 $|\psi\rangle = |\phi\rangle_A \otimes |\chi\rangle_B$ 的形式，则称其为[纠缠态](@entry_id:152310)。纠缠是量子力学最深刻的特征之一，也是[量子计算](@entry_id:142712)和通信的宝贵资源。

#### [施密特分解](@entry_id:145934)

对于任何两体系统（例如，两个[量子比特](@entry_id:137928) A 和 B）的[纯态](@entry_id:141688) $|\psi\rangle_{AB}$，都存在一种规范的表示方法，称为**[施密特分解](@entry_id:145934) (Schmidt decomposition)**：
$$ |\psi\rangle_{AB} = \sum_{i=1}^{k} \lambda_i |u_i\rangle_A |v_i\rangle_B $$
其中 $\{|u_i\rangle_A\}$ 和 $\{|v_i\rangle_B\}$ 分别是子系统 A 和 B 的一组标准正交基，$\lambda_i$ 是非负实数，称为**[施密特系数](@entry_id:137823) (Schmidt coefficients)**，并满足[归一化条件](@entry_id:156486) $\sum_i \lambda_i^2 = 1$。非零[施密特系数](@entry_id:137823)的个数 $k$ 被称为**[施密特秩](@entry_id:154893) (Schmidt rank)**。一个[纯态](@entry_id:141688)是可分离的，当且仅当其[施密特秩](@entry_id:154893)为 1。[施密特秩](@entry_id:154893)越大，通常意味着纠缠越强。

要找到一个态的[施密特分解](@entry_id:145934)，我们可以将其系数写成一个矩阵。例如，一个两体系统（子系统维度分别为 $d_A, d_B$）的态 $|\psi\rangle = \sum_{ij} C_{ij} |i\rangle_A |j\rangle_B$，其[施密特系数](@entry_id:137823)的平方 $\{\lambda_i^2\}$ 就是系数矩阵 $C$ 的[奇异值分解](@entry_id:138057)（SVD）中[奇异值](@entry_id:152907)的平方，即矩阵 $C C^\dagger$（或 $C^\dagger C$）的非零[本征值](@entry_id:154894)。

例如，考虑一个由两个三维量子系统（qutrits）组成的态 [@problem_id:142037]：
$$ |\psi\rangle = N \left( |00\rangle + |01\rangle + |11\rangle + |12\rangle + |20\rangle + |22\rangle \right) $$
其系数矩阵为 $M = \begin{pmatrix} 1  1  0\\ 0  1  1\\ 1  0  1 \end{pmatrix}$。[施密特系数](@entry_id:137823)的平方由 $N^2 M M^T$ 的[本征值](@entry_id:154894)给出。由于 $\mathrm{Tr}(MM^T) = 6$，[归一化常数](@entry_id:752675) $N = 1/\sqrt{6}$。矩阵 $MM^T = \begin{pmatrix} 2  1  1\\ 1  2  1\\ 1  1  2 \end{pmatrix}$ 的[本征值](@entry_id:154894)为 $\{4, 1, 1\}$。因此，[施密特系数](@entry_id:137823)的平方为 $\{\frac{4}{6}, \frac{1}{6}, \frac{1}{6}\}$，最大的[施密特系数](@entry_id:137823)为 $\lambda_{\max} = \sqrt{4/6} = \sqrt{2/3}$。由于[施密特秩](@entry_id:154893)为 3，该态是纠缠的。

#### [约化密度矩阵](@entry_id:146315)与纯度

当量子系统是某个更大纠缠系统的一部[分时](@entry_id:274419)，我们无法用一个态矢量来描述它。相反，我们使用**[密度矩阵](@entry_id:139892) (density matrix)** $\rho$。对于一个处于[纯态](@entry_id:141688) $|\psi\rangle$ 的复合系统，其[密度矩阵](@entry_id:139892)为 $\rho = |\psi\rangle\langle\psi|$。要描述子系统 A 的状态，我们需要通过**部分迹 (partial trace)**运算将子系统 B 的自由度“追踪掉”，得到子系统 A 的**[约化密度矩阵](@entry_id:146315) (reduced density matrix)** $\rho_A = \text{Tr}_B(\rho)$。

部分迹的定义为 $\rho_A = \sum_k \langle k_B | \rho | k_B \rangle$，其中 $\{|k_B\rangle\}$ 是子系统 B 的任意一组标准正交基。一个关键事实是：如果复合系统 $|\psi\rangle_{AB}$ 是纠缠的，那么其子系统的[约化密度矩阵](@entry_id:146315) $\rho_A$ 和 $\rho_B$ 描述的都是**混合态 (mixed state)**，即无法表示为单个[纯态](@entry_id:141688)的投影，而是多个[纯态](@entry_id:141688)的统计混合。

例如，考虑一个四比特线性簇态 [@problem_id:142041]：
$$ |\Psi\rangle = \frac{1}{2}(|0000\rangle + |0011\rangle + |1100\rangle - |1111\rangle) $$
为了得到中间两个[量子比特](@entry_id:137928)（2和3）的[约化密度矩阵](@entry_id:146315) $\rho_{23}$，我们需要追踪掉[量子比特](@entry_id:137928)1和4。通过计算 $\rho_{23} = \sum_{i,j \in \{0,1\}} \langle ij|_{14} (|\Psi\rangle\langle\Psi|) |ij\rangle_{14}$，我们发现结果是 $\rho_{23} = \frac{1}{2}(|00\rangle\langle 00| + |11\rangle\langle 11|)$。这是一个由两个正交[纯态](@entry_id:141688)等权重构成的混合态，但并非[最大混合态](@entry_id:137775)。这是纠缠的一个深刻体现：尽管整个四比特系统处于一个[纯态](@entry_id:141688)，但其子系统却处于一个混合态，关于子系统的部分信息丢失在与系统其余部分的关联中。

一个态的混合程度可以通过其**纯度 (purity)** $\gamma = \text{Tr}(\rho^2)$ 来量化。对于纯态，$\gamma=1$；对于混合态，$\gamma  1$。对于一个两体[纯态](@entry_id:141688) $|\psi\rangle_{AB}$，其子系统 A 的纯度与[施密特系数](@entry_id:137823)直接相关：$\gamma_A = \text{Tr}(\rho_A^2) = \sum_i \lambda_i^4$。这表明，子系统的混合程度（即纯度偏离1的程度）直接反映了原始[纯态](@entry_id:141688)的纠缠程度。对于一个两 qutrit 系统处于态 $|\psi\rangle = \frac{\cos\theta}{\sqrt{2}}(|01\rangle - |10\rangle) + \frac{\sin\theta}{\sqrt{2}}(|12\rangle - |21\rangle)$ [@problem_id:142141]，尽管其表达形式依赖于 $\theta$，但其子系统 A 的纯度 $\gamma_A$ 经过计算，惊人地是一个与 $\theta$ 无关的常数 $1/2$。这揭示了该纠缠结构的一种内在稳定性。

### [多体纠缠](@entry_id:142544)

当系统包含三个或更多[量子比特](@entry_id:137928)时，纠缠的结构变得异常丰富和复杂。不同于两体系统，[多体纠缠](@entry_id:142544)不再只有一种“风味”。

#### 重要的[多体纠缠](@entry_id:142544)态家族

在[多体纠缠](@entry_id:142544)的研究中，几类特殊的态扮演了基石的角色：
- **GHZ 态 (Greenberger-Horne-Zeilinger states):** $|GHZ_N\rangle = \frac{1}{\sqrt{2}}(|0\dots0\rangle + |1\dots1\rangle)$。这种态表现出“全或无”的纠缠特性。测量任何一个比特的状态会瞬间确定所有其他比特的状态。
- **W 态:** $|W_N\rangle = \frac{1}{\sqrt{N}}\sum_{k=1}^N |0\dots1_k\dots0\rangle$。与 GHZ 态不同，W 态的纠缠是“[分布](@entry_id:182848)式”的。即使丢失一个[量子比特](@entry_id:137928)，剩下的 $N-1$ 个[量子比特](@entry_id:137928)系统仍然是纠缠的。
- **Dicke 态:** $|D_k^N\rangle$ 是 W 态的推广，定义为所有具有[汉明权重](@entry_id:265886)（即 $|1\rangle$ 的个数）为 $k$ 的计算[基矢](@entry_id:199546)的等权叠加。例如，问题 [@problem_id:141992] 中提到的 $|D_2^4\rangle$ 就是一个四比特系统中有两个激发（两个 $|1\rangle$）的 Dicke 态。
- **簇态 (Cluster states):** 如问题 [@problem_id:142041] 中的例子，这类态在[基于测量的量子计算](@entry_id:138733)中至关重要。

我们经常需要计算某个可观测量在特定多体态下的[期望值](@entry_id:153208)。例如，考虑一个由 GHZ 态和 W 态叠加而成的三比特态 $|\psi(\alpha)\rangle = N ( |\text{GHZ}\rangle + \alpha |\text{W}\rangle )$ [@problem_id:142062]。计算可观测量 $O = Z \otimes Z \otimes I$ 的[期望值](@entry_id:153208) $\langle O \rangle$ 需要先对态进行归一化，然后分别计算 $O$ 在 $|GHZ\rangle$ 和 $|W\rangle$ 分量上的作用，最终得到依赖于参数 $\alpha$ 的结果 $\langle O \rangle = \frac{1-\alpha^2/3}{1+\alpha^2}$。

#### 量化[多体纠缠](@entry_id:142544)

由于[多体纠缠](@entry_id:142544)的复杂性，单一的[纠缠度量](@entry_id:139894)无法捕捉其所有方面。
- **几何纠缠度 ($E_g$):** 这个度量从几何角度定义纠缠，即一个给定的纯态 $|\psi\rangle$ 与所有可分离积态集合的“距离”。具体来说，它通过找到与 $|\psi\rangle$ 有最大保真度（或重叠）的积态 $|\phi_{\text{prod}}\rangle$ 来定义：
$$ \Lambda_{\max}(|\psi\rangle) = \max_{|\phi_{\text{prod}}\rangle} |\langle \phi_{\text{prod}} | \psi \rangle| $$
几何纠缠度则为 $E_g(|\psi\rangle) = -\log_2 (\Lambda_{\max}(|\psi\rangle)^2)$。计算 $E_g$ 的关键是执行这个最大化过程。对于具有高度对称性的态，如 W 态 [@problem_id:142032] 或 Dicke 态 [@problem_id:141992]，寻找最优积态的过程可以大大简化，通常对称的积态形式 $|\phi\rangle^{\otimes N}$ 就是最优解。例如，对于 $N$ 比特 W 态，可以证明其几何纠缠度为 $E_g(|W_N\rangle) = (N-1)\log_2\left(\frac{N}{N-1}\right)$。

- **[纠缠的单配性](@entry_id:141408)与三-纠缠度:** 一个称为**[纠缠单配性](@entry_id:137181) (monogamy of entanglement)** 的基本原则指出，一个[量子比特](@entry_id:137928)不能同时与两个或多个其他[量子比特](@entry_id:137928)形成最大纠缠。Coffman-Kundu-Wootters (CKW) 不等式为三比特系统量化了这一思想：$\tau_{A(BC)} \ge \tau_{AB} + \tau_{AC}$。这里的 $\tau$ 是**纠缠缠结 (tangle)**，定义为**并发度 (concurrence)** $C$ 的平方。$\tau_{A(BC)}$ 度量了比特 A 与子系统 BC 之间的总纠缠，而 $\tau_{AB}$ 和 $\tau_{AC}$ 是两两之间的纠缠。这个不等式意味着，A 分配给 B 和 C 的纠缠之和不能超过它与 BC 整体的纠缠。
**三-纠缠度 (three-tangle)** $\tau_3 = \tau_{A(BC)} - \tau_{AB} - \tau_{AC}$ 被定义为这个不等式中的剩余部分，它量化了真正意义上的、不能归结为两两纠缠的三体纠缠。对于一个广义 GHZ 态 $|\psi(\theta)\rangle = \cos\theta|000\rangle + \sin\theta|111\rangle$ [@problem_id:142139]，可以计算出其两两纠缠 $C_{AB}$ 和 $C_{AC}$ 均为零，而三-纠缠度为 $\tau_3 = \sin^2(2\theta)$。这完美地捕捉了 GHZ 态的特性：其所有纠缠都是纯粹的三体形式。这一概念可以推广到更多[量子比特](@entry_id:137928)，通过定义**单配性得分 (monogamy score)** [@problem_id:141994] 来检验纠缠是如何在多体系统中分配的。

- **SLOCC 分类与[超行列式](@entry_id:755853):** 除了[量化纠缠](@entry_id:144669)，对纠缠进行分类也至关重要。如果两个态可以通过**随机[局域操作和经典通信](@entry_id:136398) (SLOCC)**相互转换，则它们被认为是同一纠缠类型。对于三比特系统，存在两个不等价的真[三体](@entry_id:265960)纠缠类：GHZ 类和 W 类。一个强大的数学工具——**[凯莱超行列式](@entry_id:201076) (Cayley's hyperdeterminant)**，可以作为区分这两类的判据。它是一个关于态系数 $A_{ijk}$ 的四次多项式[不变量](@entry_id:148850)。对于一个态，如果其[超行列式](@entry_id:755853)不为零，它就属于 GHZ 类。我们可以通过寻找使[超行列式](@entry_id:755853)为零的参数，来探索不同纠缠类别之间的边界 [@problem_id:142051]。

### [多体系统](@entry_id:144006)中的对称性

当复合系统由全同粒子（如[量子比特](@entry_id:137928)）组成时，**[置换对称性](@entry_id:185825) (permutation symmetry)** 扮演了核心角色。描述两个相同粒子状态的希尔伯特空间可以分解为**对称[子空间](@entry_id:150286)** $\mathcal{H}_S$ 和**反对称[子空间](@entry_id:150286)** $\mathcal{H}_A$ 的直和。

#### 对称与反对称[子空间](@entry_id:150286)

**[交换算符](@entry_id:156554) (SWAP operator)** $S$ 的定义是交换两个粒子的状态：$S|ij\rangle = |ji\rangle$。它的[本征值](@entry_id:154894)是 $+1$ 和 $-1$，分别对应对称和反对称的本征态。我们可以定义投影到这两个[子空间](@entry_id:150286)的[投影算符](@entry_id:154142)：
$$ P_S = \frac{I+S}{2}, \quad P_A = \frac{I-S}{2} $$
这两个投影算符是正交的 ($P_S P_A = 0$) 且完备的 ($P_S + P_A = I$)。对于由两个 $d$ 维系统（qutrits, $d=3$）组成的系统，对称[子空间](@entry_id:150286)的维度是 $\dim(\mathcal{H}_S) = d(d+1)/2 = 6$，反对称[子空间](@entry_id:150286)的维度是 $\dim(\mathcal{H}_A) = d(d-1)/2 = 3$ [@problem_id:142000]。

对于 $N>2$ 的系统，我们可以定义一个**全对称[子空间](@entry_id:150286)** $\text{Sym}^N(\mathbb{C}^d)$，它包含了所有在任意粒子[置换](@entry_id:136432)下保持不变的态。投影到该[子空间](@entry_id:150286)的算符由**对称化算符**给出：$P_{\text{sym}} = \frac{1}{N!} \sum_{\sigma \in S_N} U_\sigma$，其中 $U_\sigma$ 是实现[置换](@entry_id:136432) $\sigma$ 的酉算符。我们可以计算任意态，如 $|+\rangle|0\rangle|1\rangle$，在这个[子空间](@entry_id:150286)上的投影分量的模方，这在研究[玻色子](@entry_id:138266)系统时非常重要 [@problem_id:142018]。

#### [对称性与守恒](@entry_id:154858)量

对称性原理在物理学中无处不在，它与[守恒量](@entry_id:150267)紧密相连。在多体系统中，我们可以研究不同对称性之间的相互作用。例如，我们可以同时考虑粒子[交换对称性](@entry_id:151892)和由总自旋 $z$ 分量算符 $S_z^{\text{tot}} = \sum_i S_z^{(i)}$ 产生的对称性。一个有趣的问题是确定同时满足多个对称性约束的[子空间](@entry_id:150286)的维度。例如，在双 qutrit 系统（可视为自旋-1粒子）中，我们可以寻找同时满足交换对称（[本征值](@entry_id:154894)为+1）且总自旋 $z$ 分量为零（$m_1+m_2=0$）的态所张成的[子空间](@entry_id:150286)。通过列举满足条件的[基矢](@entry_id:199546)并构造其对称组合，可以发现该[子空间](@entry_id:150286)的维度为 2 [@problem_id:142070]。

从一个更抽象的代数角度看，一个算符集合的**[中心化子](@entry_id:146604) (centralizer)** 或**对易子 (commutant)** 是指与该集合中所有算符都对易的算符所构成的[向量空间](@entry_id:151108)。根据[舒尔引理](@entry_id:136779)，一个算符如果与某个群的所有表示矩阵对易，那么它必然是一个标量矩阵乘以单位阵。推广而言，与一组定义了系统对称性的算符（如[哈密顿量](@entry_id:172864)及其守恒量）对易的算符，在其共同本征基下必然是块对角的。每个块对应一个简并的共同本征[子空间](@entry_id:150286)。因此，[中心化子](@entry_id:146604)的维度等于所有这些块的维度平方和：$\dim C(\mathcal{A}) = \sum_j d_j^2$，其中 $d_j$ 是第 $j$ 个[不可约表示](@entry_id:263310)（或共同本征[子空间](@entry_id:150286)）的维度。

例如，对于两比特系统，各项同性海森堡相互作用 $H_{iso} = X \otimes X + Y \otimes Y + Z \otimes Z$ 和总磁化强度 $M_z = Z \otimes I + I \otimes Z$ 都是与总[自旋算符](@entry_id:155419)对易的。它们的共同[本征态](@entry_id:149904)将希尔伯特空间分解为四个一维[子空间](@entry_id:150286)（自旋三重态的三个分量和[自旋单重态](@entry_id:153133)）。因此，它们的对易子的维度为 $1^2+1^2+1^2+1^2=4$ [@problem_id:142086]。这个原理在[量子纠错](@entry_id:139596)中也至关重要，[稳定子码](@entry_id:143150)的[中心化子](@entry_id:146604)包含了所有逻辑算符，其维度直接关系到编码信息的容量 [@problem_id:142094]。

### 高级表示方法：[张量网络](@entry_id:142149)

随着[量子比特](@entry_id:137928)数的增加，描述一个一般[量子态](@entry_id:146142)所需的系数数量 $2^N$ 呈[指数增长](@entry_id:141869)，这被称为“维数灾难”。**[张量网络](@entry_id:142149) (Tensor Networks)** 是一类强大的数学工具，旨在通过利用物理系统（尤其是[基态](@entry_id:150928)）中纠缠的特定结构来有效表示多体[量子态](@entry_id:146142)。

#### [矩阵乘积态 (MPS)](@entry_id:140190)

对于一维量子链，**[矩阵乘积态](@entry_id:143296) (Matrix Product State, MPS)** 提供了一种极其高效的表示方法。一个 $N$ 比特[量子态](@entry_id:146142)的 MPS 表示将其 $N$ 阶系数张量 $c_{i_1 \dots i_N}$ 分解为一系列矩阵的乘积：
$$ c_{i_1 \dots i_N} = \text{Tr}(A_1^{[i_1]} A_2^{[i_2]} \cdots A_N^{[i_N]}) $$
其中，每个 $A_k^{[i_k]}$ 是一个与物理指标 $i_k$ 相关联的矩阵。这些矩阵的最大维度 $\chi = \max_k \dim(A_k)$ 被称为**键维 (bond dimension)**。如果一个态可以用一个小的、与系统尺寸 $N$ 无关的键维精确表示，那么关于它的许多计算（如[能量期望值](@entry_id:174035)）都可以高效完成。

MPS 的物理意义与[施密特分解](@entry_id:145934)密切相关。要精确表示一个态 $|\Psi\rangle$，在任意两个相邻比特 $k$ 和 $k+1$ 之间所需的最小键维 $\chi_k$，恰好等于将系统划分为 $(1, \dots, k)$ 和 $(k+1, \dots, N)$ 两部分时，态 $|\Psi\rangle$ 的[施密特秩](@entry_id:154893)。因此，表示整个态所需的最小键维是所有可能划分中最大的[施密特秩](@entry_id:154893)：$\chi = \max_k \chi_k$。

我们可以通过计算不同划分下的[施密特秩](@entry_id:154893)来确定一个态的最小键维。例如，对于四比特 Dicke 态 $|D_2^4\rangle$ [@problem_id:142007]，在 $1|234$ 和 $3|4$ 划分下[施密特秩](@entry_id:154893)为 2，但在 $12|34$ 划分下[施密特秩](@entry_id:154893)为 3。因此，精确表示该态所需的最小键维为 $\chi=3$。同样的方法可以应用于分析量子算法产生的态的纠缠结构，如问题 [@problem_id:142082] 中的例子，其最小键维也被证明是 3。

#### [投影纠缠对态](@entry_id:137616) (PEPS)

MPS 的概念可以自然地推广到二维及更高维度，其中一种常见的形式是**[投影纠缠对态](@entry_id:137616) (Projected Entangled Pair State, PEPS)**。在 PEPS 中，每个格点上的物理量子比特都与一个张量相关联，该张量通过虚拟的“键”与其他张量连接。同样，精确表示一个二维格点上的态所需的键维 $D$ 也受到该态纠缠结构的限制。例如，对于一个横向或纵向的划分，态的[施密特秩](@entry_id:154893) $\chi$ 为键维提供了一个下界，例如 $D \ge \sqrt{\chi}$ [@problem_id:142011]。

[张量网络](@entry_id:142149)不仅为多体[量子态](@entry_id:146142)提供了一个紧凑的表示框架，也为理解和分类[多体纠缠](@entry_id:142544)的复杂结构（如对称保护[拓扑序](@entry_id:147345)）开辟了新的道路，并构成了现代[数值模拟](@entry_id:137087)方法的核心。