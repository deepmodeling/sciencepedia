## 引言
在[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的宏伟蓝图中，传统的电路模型通过一系列精确控制的量子门来操纵[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，但这并非唯一的途径。簇态与[单向量子计算](@keyword=one_way_quantum_computing|lang=zh-CN|style=Feynman)（或称[基于测量的量子计算](@keyword=measurement_based_quantum_computing|lang=zh-CN|style=Feynman)）提出了一种革命性的替代[范式](@keyword=normal_form|lang=zh-CN|style=Feynman)：计算并非通过动态施加门操作，而是通过消耗一个静态的、高度纠缠的资源态来驱动。这种方法的核心问题在于，一个静态的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)如何能够蕴含[通用计算](@keyword=universal_computation|lang=zh-CN|style=Feynman)的能力？以及我们如何通过简单的局域测量来“编程”并执行复杂的[量子算法](@keyword=quantum_algorithms|lang=zh-CN|style=Feynman)？

本文将系统性地解答这些问题。我们将从第一章“原理与机制”开始，深入剖析簇态的数学结构和物理性质，揭示其作为计算资源的奥秘。接着，在第二章“应用与[交叉](@keyword=chiasmata|lang=zh-CN|style=Feynman)学科联系”中，我们将探索该模型从实现量子算法、构建[容错计算](@keyword=fault_tolerant_computing|lang=zh-CN|style=Feynman)机到启发[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学乃至[时空几何](@keyword=spacetime_geometry|lang=zh-CN|style=Feynman)理论的广泛影响。最后，第三章“动手实践”将通过具体的思想实验，巩固读者对核心概念的理解。通过这三个篇章的学习，读者将建立一个关于簇态和[单向量子计算](@keyword=one_way_quantum_computing|lang=zh-CN|style=Feynman)的坚实理论基础，为理解其在前沿研究中的应用做好准备。

## 原理与机制

在介绍性章节之后，我们现在深入探讨簇态和[单向量子计算](@keyword=one_way_quantum_computing|lang=zh-CN|style=Feynman)的核心原理与机制。本章将系统地阐述簇态的数学描述、其内在的纠缠特性，以及如何利用这些特性通过一系列局域测量来驱动[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)。

### 簇态的定义：图、电路与稳定子

理解簇态的关键在于掌握其三种互补的描述方式：[图论](@keyword=graph_theory|lang=zh-CN|style=Feynman)表示、量子电路构造以及[稳定子形式体系](@keyword=stabilizer_formalism|lang=zh-CN|style=Feynman)。这三种方式共同描绘了这些高度纠缠的多[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)态的完整图像。

#### 操作性定义与[图论](@keyword=graph_theory|lang=zh-CN|style=Feynman)表示

从操作层面看，一个 **簇态 (cluster state)** 是通过一个确定性的、两步的量子电路过程制备的。首先，我们初始化 $N$ 个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，使它们均处于 $|+\rangle$ 态，其中 $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$。此初始态是一个简单的乘积态：$|+\rangle^{\otimes N}$。其次，我们根据一个预先定义的数学图 $G=(V, E)$ 来施加纠缠操作。在此图中，顶点集合 $V$ 中的每个顶点 $v \in V$ 对应一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，而[边集](@keyword=edge_set|lang=zh-CN|style=Feynman)合 $E$ 中的每条边 $(i, j) \in E$ 指示需要在[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) $i$ 和 $j$ 之间施加一个 **受控-Z 门 (Controlled-Z or CZ gate)**。

$CZ_{ij}$ 门的作用是在计算基下对目标[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)施加一个相位翻转，但仅当控制[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)处于 $|1\rangle$ 态时：$CZ_{ij}|kl\rangle = (-1)^{k \cdot l}|kl\rangle$，其中 $k, l \in \{0, 1\}$。由于任意两个 $CZ$ 门都是对易的 ($[CZ_{ij}, CZ_{kl}]=0$)，因此施加这些门的顺序无关紧要。最终得到的簇态 $|G\rangle$ 可以写作：

$$
|G\rangle = \left( \prod_{(i,j) \in E} CZ_{ij} \right) |+\rangle^{\otimes N}
$$

这种[图论](@keyword=graph_theory|lang=zh-CN|style=Feynman)的视角极为强大，它将一个复杂的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)简化为一个直观的图形结构，其中连接性直接反映了纠缠的模式。

#### [稳定子形式体系](@keyword=stabilizer_formalism|lang=zh-CN|style=Feynman)：代数描述

尽管电路定义很直观，但对于分析簇态的性质和在测量中的演化而言，**[稳定子形式体系](@keyword=stabilizer_formalism|lang=zh-CN|style=Feynman) (stabilizer formalism)** 提供了一种更为强大和高效的代数工具。一个算符 $S$ 被称为态 $|\psi\rangle$ 的**稳定子 (stabilizer)**，如果它作用于该态上不改变该态，即 $S|\psi\rangle = |\psi\rangle$。对于一个给定的图 $G$，其对应的簇态 $|G\rangle$ 是一个由 $N$ 个相互对易的独立算符（称为**稳定子生成元**）共同构成的[稳定子群](@keyword=stabilizer_subgroup|lang=zh-CN|style=Feynman)的唯一（在[全局相位](@keyword=global_phase|lang=zh-CN|style=Feynman)意义下）公共[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)为 $+1$ 的本征态。

对于一个图 $G=(V,E)$，其簇态的稳定子生成元集合 $\{K_v\}_{v \in V}$ 具有非常简洁和规范的形式：

$$
K_v = X_v \bigotimes_{u \in N(v)} Z_u
$$

其中，$X_v$ 是作用在[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) $v$ 上的泡利-X 算符，$Z_u$ 是作用在[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) $u$ 上的泡利-Z 算符，$N(v)$ 是图中与顶点 $v$ 相邻的顶点集合（即 $v$ 的邻域）。

我们可以通过追踪初始态 $|+\rangle^{\otimes N}$ 的稳定子在 $CZ$ 门电路下的演化来推导出这个规则。初始态 $|+\rangle^{\otimes N}$ 的稳定子生成元是 $\{X_1, X_2, \dots, X_N\}$。当施加整个纠缠酉算符 $U_G = \prod_{(i,j) \in E} CZ_{ij}$ 后，新的稳定子生成元 $K_v$ 通过共轭变换得到：$K_v = U_G X_v U_G^\dagger$。

$CZ_{ab}$ 门对[泡利算符](@keyword=pauli_operators|lang=zh-CN|style=Feynman)的共轭变换规则如下：
- $CZ_{ab} X_a CZ_{ab}^\dagger = X_a Z_b$
- $CZ_{ab} X_b CZ_{ab}^\dagger = Z_a X_b$
- 对于 $c \neq a, b$，$CZ_{ab}$ 不改变作用在[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) $c$ 上的泡利算符。
- $CZ_{ab}$ 与任何泡利-Z 算符对易。

根据这个规则，当计算 $K_v = U_G X_v U_G^\dagger$ 时，每一个连接到 $v$ 的边 $(v, u) \in E$ 所对应的 $CZ_{vu}$ 门都会给 $X_v$ 附加一个 $Z_u$ 因子。而其他不涉及 $v$ 的 $CZ$ 门则与 $X_v$ 对易。因此，最终的结果恰好是 $X_v$ 乘以其所有邻居上的 $Z$ 算符的乘积，这精确地验证了 $K_v = X_v \prod_{u \in N(v)} Z_u$ 的形式 [@problem_id:652759]。

例如，考虑一个 4 [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)系统，其纠缠操作为 $U_{ent} = CZ_{34} \cdot CZ_{23} \cdot CZ_{13} \cdot CZ_{12}$。为了确定其对应的图结构，我们可以计算每个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的稳定子生成元。以 $S_1$ 为例：
$S_1 = U_{ent} X_1 U_{ent}^\dagger$
- $CZ_{12}$ 作用：$X_1 \to X_1 Z_2$
- $CZ_{13}$ 作用：$X_1 Z_2 \to (X_1 Z_3) Z_2 = X_1 Z_2 Z_3$
- $CZ_{23}$ 和 $CZ_{34}$ 不影响 $X_1$ 及其邻近的 $Z$ 算符。
所以 $S_1 = X_1 Z_2 Z_3$。这表明[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 1 的邻居是 $\{2, 3\}$。通过对所有四个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)重复此过程，我们可以确定图的所有连接，并构建其[邻接矩阵](@keyword=adjacency_matrix|lang=zh-CN|style=Feynman) $\Gamma$，其中 $\Gamma_{ij}=1$ 若 $(i,j)$ 是一条边 [@problem_id:652776]。这个过程清晰地展示了如何从一个给定的量子电路[反向工程](@keyword=reverse_engineering|lang=zh-CN|style=Feynman)出其底层的图结构，从而统一了操作定义和代数描述。

### 簇态的基本性质

簇态之所以成为[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的宝贵资源，源于其独特的纠缠结构。

#### 信息的非局域性与最大纠缠

簇态的一个显著特征是信息的完全**非局域存储 (non-local storage)**。如果我们观察簇态中的任何一个单独的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，我们得不到任何信息。更令人惊讶的是，即使我们观察一对通过边直接相连的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，我们同样无法获得确定性的信息。

具体来说，可以证明对于一个任意簇态，任何一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的**[约化密度矩阵](@keyword=reduced_density_matrix|lang=zh-CN|style=Feynman) (reduced density matrix)** $\rho_i = \operatorname{Tr}_{V\setminus\{i\}} |G\rangle\langle G|$ 都是一个**[最大混合态](@keyword=maximally_mixed_state|lang=zh-CN|style=Feynman) (maximally mixed state)**，即 $\rho_i = \frac{1}{2}I$。这意味着测量单个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)时，得到 $|0\rangle$ 或 $|1\rangle$ 的概率完全相等，无论选择何种测量基。

这个性质可以推广到更大的[子集](@keyword=subset|lang=zh-CN|style=Feynman)。例如，在一个由四个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)组成的环形簇态中，如果我们计算任意两个相邻[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)（如 1 和 2）的[约化密度矩阵](@keyword=reduced_density_matrix|lang=zh-CN|style=Feynman) $\rho_{12}$，我们会发现它也是一个[最大混合态](@keyword=maximally_mixed_state|lang=zh-CN|style=Feynman)：$\rho_{12} = \frac{1}{4}I_4$ [@problem_id:652778]。这表明，尽管整个系统处于一个[纯态](@keyword=pure_states|lang=zh-CN|style=Feynman)，但其所有局部子系统都表现出最大程度的无序。信息并非存储在单个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)或小的子系统中，而是编码在整个网络的多体关联之中。

#### 跨越划分的[纠缠量化](@keyword=entanglement_quantification|lang=zh-CN|style=Feynman)

为了更定量地理解簇态的纠缠，我们可以考虑将图的顶点集 $V$ 划分为两个不相交的[子集](@keyword=subset|lang=zh-CN|style=Feynman) $A$ 和 $B$ ($V = A \cup B$)。这两个子系统之间的纠缠强度可以通过**[施密特秩](@keyword=schmidt_rank|lang=zh-CN|style=Feynman) (Schmidt rank)** $R_{AB}$ 来量化。[施密特秩](@keyword=schmidt_rank|lang=zh-CN|style=Feynman)告诉我们需要多少个乘积态的[线性组合](@keyword=linear_combinations|lang=zh-CN|style=Feynman)才能表示这个纯态的[施密特分解](@keyword=schmidt_decomposition|lang=zh-CN|style=Feynman)。

对于[图态](@keyword=graph_states|lang=zh-CN|style=Feynman)，[施密特秩](@keyword=schmidt_rank|lang=zh-CN|style=Feynman)与图的连接性之间有一个优美的关系。它由[连接子](@keyword=connexons|lang=zh-CN|style=Feynman)图 $A$ 和 $B$ 的邻接矩阵的“跨区”子矩阵 $\Gamma_{AB}$ 的秩决定。这个子矩阵的行由 $A$ 中的顶点索引，列由 $B$ 中的顶点索引。其计算在[二元域](@keyword=gf(2)|lang=zh-CN|style=Feynman) $\mathbb{F}_2=\{0, 1\}$（即模2算术）上进行：

$$
R_{AB} = 2^{\text{rank}_{\mathbb{F}_2}(\Gamma_{AB})}
$$

这个公式揭示了一个深刻的联系：连接两个[子图](@keyword=subgraph|lang=zh-CN|style=Feynman)的每条“独立”的边（以 $\mathbb{F}_2$ 上的[线性独立](@keyword=linear_independence|lang=zh-CN|style=Feynman)性衡量）都贡献一个 $e$ 比特 (ebit) 的纠缠，使[施密特秩](@keyword=schmidt_rank|lang=zh-CN|style=Feynman)加倍。例如，考虑一个 6 [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的[图态](@keyword=graph_states|lang=zh-CN|style=Feynman)，将其划分为 $A=\{1,2,3\}$ 和 $B=\{4,5,6\}$。通过写出连接 $A$ 和 $B$ 的边的邻接子矩阵 $\Gamma_{AB}$，并计算其在 $\mathbb{F}_2$ 上的秩（例如，通过[高斯消元法](@keyword=row_reduction|lang=zh-CN|style=Feynman)），我们可以直接得到两个子系统间的纠缠大小。如果 $\text{rank}_{\mathbb{F}_2}(\Gamma_{AB})=3$，那么[施密特秩](@keyword=schmidt_rank|lang=zh-CN|style=Feynman)就是 $2^3=8$，表明这两个子系统之间存在 3 $e$ 比特的纠缠 [@problem_id:652718]。

### [单向量子计算机](@keyword=one_way_quantum_computer|lang=zh-CN|style=Feynman)：通过测量实现计算

簇态的核心应用是作为**[单向量子计算](@keyword=one_way_quantum_computing|lang=zh-CN|style=Feynman) (one-way quantum computing)** 或**[基于测量的量子计算](@keyword=measurement_based_quantum_computing|lang=zh-CN|style=Feynman) (Measurement-Based Quantum Computing, MBQC)** 的通用资源。其基本思想是，计算不是通过施加一系列[酉门](@keyword=unitary_gates|lang=zh-CN|style=Feynman)来实现，而是通过对大型、静态的簇态资源进行一系列自适应的局域单比特测量来驱动。测量过程会消耗纠缠资源，因此被称为“单向的”。

#### [量子线](@keyword=quantum_wires|lang=zh-CN|style=Feynman)：传输[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)

MBQC 中最基本的计算原语是**[量子线](@keyword=quantum_wires|lang=zh-CN|style=Feynman) (quantum wire)**，它能将一个[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)从图的一个位置传输到另一个位置。一个线性的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)链，如 1-2-3，就可以实现这个功能。

假设一个任意的输入态 $|\psi_{in}\rangle$ 被编码在链的第一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)上（通过一个适当的纠缠操作）。为了将这个态传输到链的末端，我们沿着链依次对[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)进行测量。例如，在一个 1-2-3 的线性簇态上，如果我们对中间的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 2 在泡利-X 基（即 $\{|+\rangle, |-\rangle\}$ 基）下进行测量，会发生什么？计算表明，无论测量结果是 $+1$ ($m_2=0$) 还是 $-1$ ($m_2=1$)，剩下的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 1 和 3 都会被投影到一个最大纠缠的[贝尔态](@keyword=bell_states|lang=zh-CN|style=Feynman)上 [@problem_id:652600]。测量结果仅仅决定了是哪个具体的贝尔态。

这个过程可以被看作是“消耗”了[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 2，从而在[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 1 和 3 之间建立了一条纠缠通道。通过这种方式，量子信息可以沿着一条[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)链“跳跃”前进，实现了态的传输。

#### 实现单比特旋转与前馈机制

真正的计算需要实现任意的[量子门](@keyword=quantum_gates|lang=zh-CN|style=Feynman)。在 MBQC 中，单比特旋转是通过在 $XY$ 平面上选择不同的测量基来实现的。一个通用的测量基可以写为 $\{|+\alpha\rangle, |-\alpha\rangle\}$，其中 $| \pm \alpha \rangle = \frac{1}{\sqrt{2}}(|0\rangle \pm e^{i\alpha}|1\rangle)$。测量角度 $\alpha$ 就是我们“编程”到计算中的参数。

当我们在一个线性簇态的某个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)上以角度 $\alpha$ 进行测量时，这个测量不仅会传播信息，还会在传播的信息上施加一个旋转操作。例如，在一个[三量子比特](@keyword=qutrit|lang=zh-CN|style=Feynman)的线性簇态上，对第一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)进行角度为 $\alpha$ 的测量，会使剩下的两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)处于一个纠缠态，其纠缠度（如**并发度 (concurrence)**）依赖于 $\sin(\alpha)$ [@problem_id:652738]。这说明测量角度 $\alpha$ 被有效地转化为了作用在量子信息上的一个操作。

然而，[量子测量](@keyword=quantum_mechanics_measurement|lang=zh-CN|style=Feynman)本质上是概率性的。测量结果（通常记为 $m \in \{0,1\}$）是随机的，这会导致在最终的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)上产生不希望的、依赖于测量结果的[泡利算符](@keyword=pauli_operators|lang=zh-CN|style=Feynman)（$X$ 或 $Z$），称为**副产物算符 (byproduct operators)**。为了得到确定性的计算结果，必须消除这些副产物算符。

这就是**前馈 (feed-forward)** 机制的用武之地。后续测量的基选择可以依赖于先前测量的结果。例如，一个在[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) $j$ 上的测量角度 $\alpha_j$ 可以根据前面某个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) $k$ 的测量结果 $m_k$ 进行调整，如 $\alpha_j \to \alpha_j + m_k \pi$。这种自适应的测量方案可以系统地校正副产物算符。

考虑一个旨在作为[量子线](@keyword=quantum_wires|lang=zh-CN|style=Feynman)的四[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)链，正常的测量角度应全部为零。如果第二次测量因误差而以角度 $\theta$ 进行，这会引入一个不必要的 $R_z$ 旋转。为了补偿这个错误，我们可以调整第三次测量的角度。通过分析总的[酉变换](@keyword=unitary_transformation|lang=zh-CN|style=Feynman)，可以发现，只要将第三个测量角度设为 $-\theta$（假设第一次测量结果为 0），就可以精确地抵消掉由误差引起的旋转，从而恢复[量子线](@keyword=quantum_wires|lang=zh-CN|style=Feynman)的功能 [@problem_id:652741]。这完美地展示了前馈机制在维持计算确定性中的关键作用。

### 高级机制与态操控

随着计算复杂度的增加，我们需要更精细的工具来理解和操控簇态资源。

#### 因果流与测量调度

一个 MBQC 算法的结构并非简单的[线性序](@keyword=total_order|lang=zh-CN|style=Feynman)列。由于前馈的存在，测量之间形成了一种**偏[序关系](@keyword=order_relations|lang=zh-CN|style=Feynman) (partial order)**。一个测量 $M_j$ 是否可以进行，可能依赖于一个或多个先前测量 $M_i$ 的结果。这种依赖关系定义了算法的**因果流 (causal flow)**，可以用一个[有向无环图 (DAG)](@keyword=directed_acyclic_graphs_(dags)|lang=zh-CN|style=Feynman) 来表示，其中一条从 $i$ 到 $j$ 的有向边意味着测量 $i$ 必须在测量 $j$ 之前完成。

任何与这个偏[序关系](@keyword=order_relations|lang=zh-CN|style=Feynman)一致的线性测量序列都是一个有效的**测量调度 (measurement schedule)**。例如，实现一个 CNOT 门需要一个 6 [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的簇态，其测量依赖关系相当复杂：测量 3 依赖于 1 和 2，测量 6 依赖于 4 和 5 等等。虽然存在这些依赖约束，但仍有多种可能的顺序来执行这些测量（例如，测量 1 和 2 可以按任意顺序进行）。计算所有可能的有效调度总数（即对该偏[序关系](@keyword=order_relations|lang=zh-CN|style=Feynman)进行[拓扑排序](@keyword=topological_sorting|lang=zh-CN|style=Feynman)的数量），可以帮助我们理解算法的并行性和时间结构 [@problem_id:652792]。

#### 构建与变换资源态

大规模[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)需要大型簇态资源。这些资源可以通过将较小的纠缠态“缝合”在一起来构建。一种强大的技术是在两个分别属于不同簇态的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)之间执行一个**[贝尔测量](@keyword=bell_measurement|lang=zh-CN|style=Feynman) (Bell-state measurement)**。例如，将两个初始时独立的、各自由两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)组成的[纠缠对](@keyword=entangled_pairs|lang=zh-CN|style=Feynman)（例如，[图态](@keyword=graph_states|lang=zh-CN|style=Feynman) $|G_A\rangle$ 和 $|G_B\rangle$）连接起来。通过在[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 2（来自 A）和 3（来自 B）上执行[贝尔测量](@keyword=bell_measurement|lang=zh-CN|style=Feynman)，我们可以将它们纠缠起来。使用[稳定子形式体系](@keyword=stabilizer_formalism|lang=zh-CN|style=Feynman)可以精确地追踪这个过程：初始的稳定子生成元在[贝尔测量](@keyword=bell_measurement|lang=zh-CN|style=Feynman)的[等效电路](@keyword=equivalent_circuits|lang=zh-CN|style=Feynman)（一个 CNOT 门和一个哈德玛门）下发生变换，测量结果固定了某些算符的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)，从而为剩下的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)（1 和 4）导出一个新的[稳定子群](@keyword=stabilizer_subgroup|lang=zh-CN|style=Feynman)，描述了它们之间新形成的纠缠关系 [@problem_id:652831]。

最后，一个深刻的概念是，许多在图论上看起来截然不同的簇态，在物理上却是等价的。它们之间的关系可以通过**局域克利福德 (Local Clifford, LC) 操作**来建立。如果两个[图态](@keyword=graph_states|lang=zh-CN|style=Feynman)可以通过只在单个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)上施加[克利福德群](@keyword=clifford_group|lang=zh-CN|style=Feynman)中的酉算符而相互转化，则称它们是 **LC 等价的**。

在图的层面，一个关键的 LC 等价变换是**局域补图 (local complementation)**。对图 $G$ 在顶点 $v$ 处执行局域补图操作 $\tau_v$，会产生一个新图 $G'$。变换规则是：保持 $v$ 及其所有边不变，但将其邻域 $N(v)$ 所诱导的子图 $G_{N(v)}$ 替换为其补图 $\overline{G_{N(v)}}$（即在 $N(v)$ 内部，有边的变没边，没边的变有边）。通过一系列这样的操作，可以探索整个 LC [等价类](@keyword=equivalence_classes|lang=zh-CN|style=Feynman)。例如，一个 5 [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的线性链图，可以通过在顶点 4 和 2 上相继进行局域[补图](@keyword=graph_complement|lang=zh-CN|style=Feynman)操作，变换成一个具有不同拓扑结构的新图 [@problem_id:652656]。这一发现表明，资源态的选择具有很大的灵活性，为优化 MBQC 的物理实现提供了广阔空间。