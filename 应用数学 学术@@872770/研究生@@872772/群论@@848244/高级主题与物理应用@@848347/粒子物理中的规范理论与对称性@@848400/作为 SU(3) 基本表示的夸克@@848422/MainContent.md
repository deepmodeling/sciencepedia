## 引言
夸克是构成物质的基本粒子，它们通过强相互作用结合在一起，形成质子和中子等我们熟知的强子。这种强大的力由一种被称为“颜色”的量子荷所支配，其背后的对称性原理可以用特殊的[酉群](@entry_id:138602) $SU(N)$ 来精确描述。然而，一个核心的谜题是：为什么我们从未在自然界中观测到单个的自由夸克，它们又是如何通过这种“颜色”相互作用，精确地组合成特定的[复合粒子](@entry_id:150176)？本文旨在揭开这个谜题，系统性地阐述夸克如何作为 $SU(N)$ 群的[基本表示](@entry_id:157678)，从而建立起从抽象群论到可观测粒子物理现象的桥梁。

在接下来的内容中，我们将分三个章节深入探讨这一主题。在“原理与机制”一章中，我们将首先建立 $SU(N)$ [李代数](@entry_id:137954)的数学框架，介绍生成元、卡西米尔算符等核心工具，并推导它们如何决定夸克间的相互作用力。随后，在“应用与跨学科联系”一章中，我们将展示这一理论框架如何应用于解释[强子谱学](@entry_id:155019)、计算散射过程中的颜[色因子](@entry_id:159844)，并探讨其与[大统一理论](@entry_id:150304)、宇宙学等前沿领域的深刻联系。最后，“动手实践”部分将通过具体问题，帮助读者巩固和应用所学知识。

让我们首先深入研究这一理论的基石——描述夸克及其相互作用的 $SU(N)$ 群的原理与机制。

## 原理与机制

继前一章对夸克和颜色对称性进行了初步介绍之后，本章将深入探讨将夸克描述为[特殊酉群](@entry_id:138145) $SU(N)$ 的[基本表示](@entry_id:157678)的数学原理和物理机制。我们将建立描述[夸克相互作用](@entry_id:204726)的群论框架，并利用此框架来解释[强子](@entry_id:158325)（如[介子和重子](@entry_id:158328)）的内部结构和性质。本章内容将从 $SU(N)$ [李代数](@entry_id:137954)的基本属性出发，逐步推导描述复合粒子内部颜色相互作用的关键量，并最终将这些抽象的对称性原理与可观测的物理量（如[粒子自旋](@entry_id:142910)）联系起来。

### SU(N) 李代数的[基本表示](@entry_id:157678)

在[量子色动力学](@entry_id:143869) (QCD) 及其推广理论中，夸克被描述为在 $N$ 维[复向量空间](@entry_id:264355) $\mathbb{C}^N$ 上变换的场。这个空间承载了 $SU(N)$ 群的一个[不可约表示](@entry_id:263310)，即**[基本表示](@entry_id:157678)** (fundamental representation)，通常记为 $\mathbf{N}$。描述理论动力学的关键在于其李代数 $\mathfrak{su}(N)$。

#### 生成元与归一化

$SU(N)$ 的李代数 $\mathfrak{su}(N)$ 由一组 $N^2-1$ 个**生成元** (generators) $T^a$（其中 $a=1, 2, \dots, N^2-1$）张成。在[基本表示](@entry_id:157678)中，这些生成元由 $N \times N$ 的厄米 (Hermitian) 且无迹 (traceless) 的[矩阵表示](@entry_id:146025)：

$$
(T^a)^\dagger = T^a, \quad \mathrm{Tr}(T^a) = 0
$$

这些生成元在物理学中的一个核心性质是它们的迹正交归一化关系。这个关系定义了生成元之间的“[内积](@entry_id:158127)”，并为理论的计算设定了约定。其[标准形式](@entry_id:153058)为：

$$
\mathrm{Tr}(T^a T^b) = T_F \delta^{ab}
$$

其中 $\delta^{ab}$ 是克罗内克 (Kronecker) delta 符号，$T_F$ 是一个称为**迹[归一化常数](@entry_id:752675)** (trace normalization constant) 的正实数。这个常数的选择本质上是一种约定，但在高能物理的标准模型中，通常采用一个特定的值。

#### 二次卡西米尔算符与菲尔兹恒等式

李代数中一个极其重要的算符是**二次卡西米尔算符** (quadratic Casimir operator)，它被定义为所有生成元平方和：

$$
C_2(F) = \sum_{a=1}^{N^2-1} T^a T^a
$$

根据**[舒尔引理](@entry_id:136779)** (Schur's Lemma)，在任何一个不可约表示中，卡西米尔算符必然正比于[单位矩阵](@entry_id:156724)。对于[基本表示](@entry_id:157678) $\mathbf{N}$，我们可以写作：

$$
\sum_{a=1}^{N^2-1} T^a T^a = C_2(F) \mathbb{I}_N
$$

这里的标量 $C_2(F)$ 是该表示下卡西米尔算符的[本征值](@entry_id:154894)，它唯一地标记了这个[不可约表示](@entry_id:263310)。

迹[归一化常数](@entry_id:752675) $T_F$ 和卡西米尔[本征值](@entry_id:154894) $C_2(F)$ 并非相互独立。我们可以通过一个简单的推导建立它们之间的关系。对卡西米尔算符的定义式两边取迹，可得：

$$
\mathrm{Tr} \left( \sum_{a=1}^{N^2-1} T^a T^a \right) = \mathrm{Tr} (C_2(F) \mathbb{I}_N)
$$

利用[迹的线性](@entry_id:199170)性质，左边变为 $\sum_{a=1}^{N^2-1} \mathrm{Tr}(T^a T^a)$。根据迹的归一化关系，当 $b=a$ 时，$\mathrm{Tr}(T^a T^a) = T_F \delta^{aa} = T_F$。由于求和遍及所有 $N^2-1$ 个生成元，左边的结果是 $(N^2-1)T_F$。右边则是 $C_2(F) \mathrm{Tr}(\mathbb{I}_N) = C_2(F) \cdot N$。因此，我们得到：

$$
(N^2-1)T_F = N C_2(F)
$$

这个关系式表明，一旦我们为 $T_F$ 或 $C_2(F)$ 中的任何一个设定了约定值，另一个的值也就随之确定。在粒子物理学的标准文献中，通常约定[基本表示](@entry_id:157678)的迹[归一化常数](@entry_id:752675)为 $T_F = 1/2$ [@problem_id:749319]。

有了这个约定，我们就可以确定卡西米尔算符的[本征值](@entry_id:154894)。一个强有力的推导方法是利用**菲尔兹恒等式** (Fierz completeness identity)，它给出了[基本表示](@entry_id:157678)生成元[矩阵元](@entry_id:186505)乘积的求和表达式 [@problem_id:749420]：

$$
\sum_{a=1}^{N^2-1} (T^a)_{ij} (T^a)_{kl} = T_F \left( \delta_{il}\delta_{jk} - \frac{1}{N}\delta_{ij}\delta_{kl} \right)
$$

这里 $(T^a)_{ij}$ 是矩阵 $T^a$ 的第 $i$ 行、第 $j$ 列的元素。这个恒等式反映了 $\mathfrak{su}(N)$ 生成元与[单位矩阵](@entry_id:156724)一起构成了 $N \times N$ 矩阵空间的[完备基](@entry_id:143908)。为了求出 $C_2(F)$，我们考察卡西米尔算符的矩阵元：

$$
(C_2(F))_{ik} = \left( \sum_{a=1}^{N^2-1} T^a T^a \right)_{ik} = \sum_{a=1}^{N^2-1} \sum_{j=1}^{N} (T^a)_{ij} (T^a)_{jk}
$$

这个表达式与菲尔兹恒等式的左边非常相似。通过在菲尔兹恒等式中令 $l=j$ 并对 $j$ 求和，我们可以将两者联系起来：

$$
\sum_{a=1}^{N^2-1} \sum_{j=1}^{N} (T^a)_{ij} (T^a)_{jk} = T_F \sum_{j=1}^{N} \left( \delta_{ik}\delta_{jj} - \frac{1}{N}\delta_{ij}\delta_{jk} \right)
$$

在右边，$\sum_{j=1}^{N} \delta_{jj} = \mathrm{Tr}(\mathbb{I}_N) = N$，而 $\sum_{j=1}^{N} \delta_{ij}\delta_{jk} = \delta_{ik}$。代入这些结果，我们得到：

$$
(C_2(F))_{ik} = T_F \left( N\delta_{ik} - \frac{1}{N}\delta_{ik} \right) = T_F \left( N - \frac{1}{N} \right) \delta_{ik} = \frac{T_F(N^2-1)}{N} \delta_{ik}
$$

由于 $(C_2(F))_{ik} = C_2(F) \delta_{ik}$，通过比较系数，我们得到卡西米尔算符的[本征值](@entry_id:154894)：

$$
C_2(F) = \frac{T_F(N^2-1)}{N}
$$

在 $T_F = 1/2$ 的标准约定下，我们得到了[粒子物理学](@entry_id:145253)中一个极其重要的结果：

$$
C_2(F) = \frac{N^2-1}{2N}
$$

#### 代数关系：[反对易子](@entry_id:139754)

除了[对易关系](@entry_id:136780) $[T^a, T^b] = i f^{abc} T^c$ 定义了[李代数](@entry_id:137954)的[结构常数](@entry_id:157960) $f^{abc}$ 外，生成元的**[反对易子](@entry_id:139754)** (anticommutator) $\{T^a, T^b\} = T^a T^b + T^b T^a$ 也具有重要的物理意义。由于任何 $N \times N$ 矩阵都可以由单位矩阵 $\mathbb{I}_N$ 和生成元 $T^c$ [线性表示](@entry_id:139970)，[反对易子](@entry_id:139754)也可以在这个基上展开：

$$
\{T^a, T^b\} = c_{ab} \mathbb{I}_N + \sum_{c=1}^{N^2-1} d_{abc} T^c
$$

其中 $c_{ab}$ 是系数，而 $d_{abc}$ 是完全对称的[结构常数](@entry_id:157960)。我们可以通过取迹的方法来确定系数 $c_{ab}$ [@problem_id:749459]。对上式两边取迹，并利用 $\mathrm{Tr}(\mathbb{I}_N)=N$ 和 $\mathrm{Tr}(T^c)=0$：

$$
\mathrm{Tr}(\{T^a, T^b\}) = c_{ab} \mathrm{Tr}(\mathbb{I}_N) + \sum_{c} d_{abc} \mathrm{Tr}(T^c) = N c_{ab}
$$

另一方面，利用迹的循环不变性 $\mathrm{Tr}(AB)=\mathrm{Tr}(BA)$，我们有：

$$
\mathrm{Tr}(\{T^a, T^b\}) = \mathrm{Tr}(T^a T^b + T^b T^a) = 2\mathrm{Tr}(T^a T^b)
$$

根据归一化关系 $\mathrm{Tr}(T^a T^b) = T_F \delta^{ab} = \frac{1}{2}\delta^{ab}$，上式等于 $\delta^{ab}$。联立两个结果，我们得到 $N c_{ab} = \delta^{ab}$，即：

$$
c_{ab} = \frac{1}{N} \delta^{ab}
$$

这导出了一个非常实用的恒等式：

$$
\{T^a, T^b\} = \frac{1}{N} \delta^{ab} \mathbb{I}_N + \sum_{c=1}^{N^2-1} d_{abc} T^c
$$

这个关系在计算[费曼图](@entry_id:144373)中的颜[色因子](@entry_id:159844)时非常有用。

### 复合态中的颜色相互作用

自然界中观测不到自由的夸克，它们总是以颜色中性的束缚态——**强子** (hadrons) 的形式存在。这些[复合粒子](@entry_id:150176)的性质由其组分夸克的颜色相互作用决定。

#### [张量积](@entry_id:140694)与[强子](@entry_id:158325)态

一个由多个夸克组成的系统，其颜色态空间由单个夸克颜色态空间的**张量积** (tensor product) 描述。例如，一个由夸克 ($q$) 和反夸克 ($\bar{q}$) 组成的介子，其颜色态空间是 $V_{\mathbf{N}} \otimes V_{\mathbf{\bar{N}}}$，其中 $\mathbf{N}$ 是夸克所属的[基本表示](@entry_id:157678)，$\mathbf{\bar{N}}$ 是反夸克所属的共轭[基本表示](@entry_id:157678)。

这个[张量积](@entry_id:140694)空间通常是可约的，它可以分解为多个不可约表示（irreps）的直和。对于 $q\bar{q}$ 系统，这个分解是：

$$
\mathbf{N} \otimes \mathbf{\bar{N}} = \mathbf{1} \oplus \mathbf{adj}
$$

这里 $\mathbf{1}$ 代表一维的**平庸表示** (trivial representation)，即**颜[色单态](@entry_id:159293)** (color singlet)，它在 $SU(N)$ 变换下保持不变。$\mathbf{adj}$ 代表维度为 $N^2-1$ 的**伴随表示** (adjoint representation)，例如在 $SU(3)$ 中，这就是所谓的**颜色八重态** (color octet)。物理上稳定的[介子](@entry_id:184535)被认为是颜[色单态](@entry_id:159293)。

#### [介子](@entry_id:184535) ($q\bar{q}$ 态)：颜[色单态](@entry_id:159293)与伴随态

夸克间的相互作用（例如通过单胶子交换）的强度与一个称为**颜[色因子](@entry_id:159844)** (color factor) 的群论量有关。对于 $q\bar{q}$ 系统，这个因子是 $\langle \mathbf{T}_q \cdot \mathbf{T}_{\bar{q}} \rangle$，其中 $\mathbf{T}_q \cdot \mathbf{T}_{\bar{q}} = \sum_{a=1}^{N^2-1} T_q^a T_{\bar{q}}^a$。$T_q^a$ 是作用在夸克色空间上的生成元算符，而 $T_{\bar{q}}^a$ 作用在反夸克的色空间上。这个算符的[期望值](@entry_id:153208)决定了相互作用[势能](@entry_id:748988)是吸引的还是排斥的。

我们可以利用卡西米尔算符来计算这个[期望值](@entry_id:153208)。定义作用于整个系统的总颜色算符为 $\mathbf{T}_{\text{tot}} = \mathbf{T}_q + \mathbf{T}_{\bar{q}}$。它的平方是：

$$
\mathbf{T}_{\text{tot}}^2 = (\mathbf{T}_q + \mathbf{T}_{\bar{q}})^2 = \mathbf{T}_q^2 + \mathbf{T}_{\bar{q}}^2 + 2 \mathbf{T}_q \cdot \mathbf{T}_{\bar{q}}
$$

左边是总系统的二次卡西米尔算符，其[本征值](@entry_id:154894)是 $C_2(R_{\text{tot}})$，其中 $R_{\text{tot}}$ 是 $q\bar{q}$ 组合成的[不可约表示](@entry_id:263310)。$\mathbf{T}_q^2$ 和 $\mathbf{T}_{\bar{q}}^2$ 分别是夸克和反夸克的卡西米尔算符，其[本征值](@entry_id:154894)分别为 $C_2(\mathbf{N})$ 和 $C_2(\mathbf{\bar{N}})$。对于[共轭表示](@entry_id:139136)，其[卡西米尔不变量](@entry_id:181340)的值与原表示相同，即 $C_2(\mathbf{\bar{N}}) = C_2(\mathbf{N}) = \frac{N^2-1}{2N}$。因此，我们可以得到一个普适的关系式：

$$
\langle \mathbf{T}_q \cdot \mathbf{T}_{\bar{q}} \rangle = \frac{1}{2} \left[ C_2(R_{\text{tot}}) - C_2(\mathbf{N}) - C_2(\mathbf{\bar{N}}) \right] = \frac{1}{2} \left[ C_2(R_{\text{tot}}) - 2C_2(\mathbf{N}) \right]
$$

现在我们可以分析不同的颜色组态：

1.  **颜[色单态](@entry_id:159293) ($\mathbf{1}$)**: 颜[色单态](@entry_id:159293)的定义是它在所有 $SU(N)$ 变换下不变，这意味着总颜色算符作用于其上为零：$\mathbf{T}_{\text{tot}} |\text{singlet}\rangle = 0$ [@problem_id:749511]。因此，总系统的卡西米尔算符[本征值](@entry_id:154894)为 $C_2(\mathbf{1})=0$。代入上式得到：
    $$
    \langle \mathbf{T}_q \cdot \mathbf{T}_{\bar{q}} \rangle_{\text{singlet}} = \frac{1}{2} [0 - 2C_2(\mathbf{N})] = -C_2(\mathbf{N}) = -\frac{N^2-1}{2N}
    $$
    这个负号至关重要，它意味着在颜[色单态](@entry_id:159293)下，$q\bar{q}$ 之间的相互作用是**吸引**的，从而可以形成稳定的束缚态——[介子](@entry_id:184535)。

2.  **伴随态 ($\mathbf{adj}$)**: 对于伴随表示，其卡西米尔算符的[本征值](@entry_id:154894)为 $C_2(\text{adj}) = N$。将 $R_{\text{tot}}=\text{adj}$ 代入 [@problem_id:749353] [@problem_id:749512]：
    $$
    \langle \mathbf{T}_q \cdot \mathbf{T}_{\bar{q}} \rangle_{\text{adj}} = \frac{1}{2} [C_2(\text{adj}) - 2C_2(\mathbf{N})] = \frac{1}{2} \left[ N - 2 \left( \frac{N^2-1}{2N} \right) \right] = \frac{1}{2} \left[ \frac{N^2 - (N^2-1)}{N} \right] = \frac{1}{2N}
    $$
    这个结果是正的，意味着在伴随态（如色八重态）下，$q\bar{q}$ 之间的相互作用是**排斥**的。这从动力学上解释了为什么我们观测不到有色的[强子](@entry_id:158325)，这一现象被称为**颜[色禁闭](@entry_id:143757)** (color confinement)。

#### 重子中的颜[色因子](@entry_id:159844)

与[介子](@entry_id:184535)类似，重子是 $SU(N)$ 理论中由 $N$ 个夸克组成的颜[色单态](@entry_id:159293)束缚态。其颜色[波函数](@entry_id:147440)在任意两个夸克的交换下是完全反对称的。我们可以用同样的方法计算重子内部任意两个夸克（比如夸克1和夸克2）之间的颜[色因子](@entry_id:159844) $\langle \mathbf{T}_1 \cdot \mathbf{T}_2 \rangle$ [@problem_id:749387]。

总颜色算符为 $\mathbf{T}_{\text{tot}} = \sum_{k=1}^{N} \mathbf{T}_k$。由于重子是颜[色单态](@entry_id:159293)，我们有 $\mathbf{T}_{\text{tot}} |B\rangle = 0$，其平方的[期望值](@entry_id:153208)也为零：

$$
\langle B | \mathbf{T}_{\text{tot}}^2 | B \rangle = \left\langle B \left| \left(\sum_{k=1}^{N} \mathbf{T}_k\right)^2 \right| B \right\rangle = 0
$$

展开平方项：

$$
\mathbf{T}_{\text{tot}}^2 = \sum_{k=1}^{N} \mathbf{T}_k^2 + \sum_{k \neq l} \mathbf{T}_k \cdot \mathbf{T}_l
$$

取[期望值](@entry_id:153208)后，第一项为 $\sum_{k=1}^{N} \langle \mathbf{T}_k^2 \rangle = N C_2(\mathbf{N})$。由于重子[波函数](@entry_id:147440)的对称性，任意一对不同夸克之间的颜[色因子](@entry_id:159844)[期望值](@entry_id:153208)都相同，我们记为 $C = \langle \mathbf{T}_1 \cdot \mathbf{T}_2 \rangle$。共有 $N(N-1)$ 对这样的组合。于是方程变为：

$$
N C_2(\mathbf{N}) + N(N-1) C = 0
$$

解出 $C$：

$$
C = -\frac{N C_2(\mathbf{N})}{N(N-1)} = -\frac{C_2(\mathbf{N})}{N-1} = -\frac{(N^2-1)/2N}{N-1} = -\frac{(N-1)(N+1)}{2N(N-1)} = -\frac{N+1}{2N}
$$

结果再次为负，表明重子内部夸克之间的相互作用也是吸引的，从而形成了稳定的束缚态。对于物理上的 $SU(3)$ 重子，这个因子是 $-\frac{3+1}{2 \cdot 3} = -\frac{2}{3}$。

### 颜色对称性的物理推论

群论的抽象结构最终必须与物理世界的具体现象联系起来。颜色对称性最深刻的体现之一是它如何与[量子统计力学](@entry_id:140244)相结合，从而决定了强子的基本属性。

#### 一个具体例子：SU(2) 双夸克系统

为了更具体地理解这些概念，我们可以考察一个简化的 $SU(2)$ 颜色理论 [@problem_id:749461]。$SU(2)$ 的[基本表示](@entry_id:157678)是二维的，其生成元可以由[泡利矩阵](@entry_id:139493) (Pauli matrices) 给出：$T^a = \frac{1}{2}\sigma^a$。

一个双夸克系统的颜色空间是 $V_{\mathbf{2}} \otimes V_{\mathbf{2}}$。这个[张量积](@entry_id:140694)可以分解为：

$$
\mathbf{2} \otimes \mathbf{2} = \mathbf{1} \oplus \mathbf{3}
$$

其中 $\mathbf{1}$ 是反对称的单态，$\mathbf{3}$ 是对称的[三重态](@entry_id:156705)（即伴随表示）。反对称的单态[波函数](@entry_id:147440)为 $|\Psi_A\rangle = \frac{1}{\sqrt{2}}(|r\rangle|g\rangle - |g\rangle|r\rangle)$，其中 $|r\rangle, |g\rangle$ 是颜色基。我们可以直接验证这个态确实是单态，即证明作用于其上的总卡西米尔算符 $C_2 = \sum_a (T^a_{\text{total}})^2$ 的[本征值](@entry_id:154894)为零。通过计算，可以证明 $C_2 |\Psi_A\rangle = 0 \cdot |\Psi_A\rangle$，从而确认了这一点。这为更普适的 $N$ 夸克单态是全反对称的结论提供了一个具体的例证。

#### 泡利原理与重子自旋

夸克是自旋为 $1/2$ 的[费米子](@entry_id:146235)，因此由多个夸克组成的系统必须遵循**[泡利不相容原理](@entry_id:141850)**，即系统的总[波函数](@entry_id:147440) $\Psi_{\text{total}}$ 在交换任意两个全同夸克时必须是反对称的。总[波函数](@entry_id:147440)可以分解为颜色、自旋和空间三部分的乘积：

$$
\Psi_{\text{total}} = \psi_{\text{color}} \otimes \psi_{\text{spin}} \otimes \psi_{\text{spatial}}
$$

现在考虑一个由 $N$ 个同味夸克组成的[基态](@entry_id:150928)重子 [@problem_id:749322]。
- **空间[波函数](@entry_id:147440) $\psi_{\text{spatial}}$**：在[基态](@entry_id:150928)下，所有夸克都处于最低的能量[轨道](@entry_id:137151)（s-波），这意味着它们共享相同的空间[波函数](@entry_id:147440)。因此，$\psi_{\text{spatial}}$ 在任意夸克交换下是**完全对称**的。
- **颜色[波函数](@entry_id:147440) $\psi_{\text{color}}$**：如前所述，为了构成颜[色单态](@entry_id:159293)，重子的 $\psi_{\text{color}}$ 必须是**完全反对称**的。

为了使总[波函数](@entry_id:147440) $\Psi_{\text{total}}$ 保持反对称性，[自旋波函数](@entry_id:190161) $\psi_{\text{spin}}$ 的对称性必须满足：
$$
(\text{反对称}) = (\text{反对称}) \otimes (\psi_{\text{spin}}) \otimes (\text{对称})
$$
这迫使 $\psi_{\text{spin}}$ 必须是**完全对称**的。

一个由 $N$ 个自旋 $1/2$ 粒子组成的完全对称的自旋态，是所有[粒子自旋](@entry_id:142910)方向一致“朝上”的态，即[总自旋](@entry_id:153335)取最大值的态。这个最大[总自旋](@entry_id:153335)值 $J$ 等于所有单个[自旋投影](@entry_id:184359)之和：

$$
J = M_{J, \text{max}} = \sum_{i=1}^{N} m_{s,i} = \sum_{i=1}^{N} \frac{1}{2} = \frac{N}{2}
$$

这是一个惊人的预测：一个由 $N$ 个同味夸克组成的[基态](@entry_id:150928)重子，其[总自旋](@entry_id:153335)必然是 $J=N/2$。对于 QCD ($N=3$)，这预测了[基态](@entry_id:150928)重子如 $\Delta^{++}$ (uuu) 或 $\Omega^-$ (sss) 的自旋为 $J=3/2$，这与实验观测完全吻合。这个成功是颜色量子数存在的第一个也是最有力的证据之一。

### [子群](@entry_id:146164)与[表示分解](@entry_id:139061)

在物理学中，特别是在[大统一理论 (GUTs)](@entry_id:158642) 中，一个大的对称群常常会破缺到其[子群](@entry_id:146164)。因此，研究表示在[子群](@entry_id:146164)下的分解（即**分支规则**, branching rules）具有重要意义。

一个典型的例子是 $SU(N)$ 破缺到其一个[极大子群](@entry_id:137142) $SU(N-1) \times U(1)$ [@problem_id:749395]。在这种情况下，$SU(N)$ 的[基本表示](@entry_id:157678) $\mathbf{N}$ 会如何分解成 $SU(N-1)$ 和 $U(1)$ 的表示呢？

$SU(N)$ 的 $N$ 维[基本表示](@entry_id:157678)向量可以写作 $(v_1, \dots, v_{N-1}, v_N)^T$。$SU(N-1)$ [子群](@entry_id:146164)可以被看作是作用于前 $N-1$ 个分量，而保持最后一个分量不变的 $SU(N)$ 变换的[子集](@entry_id:261956)。因此，这个 $N$ 维[向量空间](@entry_id:151108)自然地分解为一个 $N-1$ 维的 $SU(N-1)$ 空间和一个一维空间。也就是说，在 $SU(N-1)$ [子群](@entry_id:146164)下，$\mathbf{N}$ 分解为：

$$
\mathbf{N} \rightarrow (\mathbf{N-1}) + \mathbf{1}
$$

这意味着原来 $SU(N)$ 的 $N$ 维[表示分解](@entry_id:139061)成了一个 $SU(N-1)$ 的 $N-1$ 维[基本表示](@entry_id:157678)和一个 $SU(N-1)$ 的单态。

同时，我们需要考虑 $U(1)$ 因子。这个 $U(1)$ 生成元 $T_Y$ 必须与所有 $SU(N-1)$ 生成元对易。在[基本表示](@entry_id:157678)中，满足这个条件的唯一无迹厄米矩阵（不计标度因子）是对角矩阵，其前 $N-1$ 个对角元相等，最后一个对角元不同：

$$
T_Y = \mathrm{diag}(a, a, \dots, a, b)
$$

无迹条件 $\mathrm{Tr}(T_Y)=0$ 给出 $(N-1)a + b = 0$。物理学中的标准[归一化条件](@entry_id:156486)是 $\mathrm{Tr}(T_Y^2) = 1/2$，这给出 $(N-1)a^2 + b^2 = 1/2$。联立求解这两个方程，可以得到两个不同的 $U(1)$ 荷 $a$ 和 $b$ 的值。例如，可以解出这两个非零荷的乘积为 $-\frac{1}{2N}$。这个过程展示了如何从一个高阶[对称群](@entry_id:146083)系统地导出其在低能量下子群的表示内容和量子数，这是超越标准模型物理学研究中的一项基本技能。