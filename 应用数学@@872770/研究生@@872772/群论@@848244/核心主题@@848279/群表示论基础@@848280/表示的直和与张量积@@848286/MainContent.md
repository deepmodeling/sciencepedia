## 引言
在[群表示论](@entry_id:141930)的研究中，仅有单个的不可约表示是不够的。为了描述复杂的物理系统或数学结构，我们必须理解如何从已知的表示出发，系统地构造出新的、更复杂的表示。[表示的直和](@entry_id:138310)与[张量积](@entry_id:140694)正是实现这一目标的核心代数工具，它们分别对应于组合独立子系统和相互作用子系统的数学语言。然而，组合之后往往产生[可约表示](@entry_id:137110)，这就引出了[表示论](@entry_id:137998)中的一个核心问题：如何将一个给定的[表示分解](@entry_id:139061)为其不可约的组成部分？解答这个问题不仅是理论上的挑战，更是在量子力学、粒子物理等领域理解[对称性选择定则](@entry_id:156619)、粒子多重态和相互作用耦合的关键。

本文将系统地引导读者掌握这些强大的工具。在“原理与机制”一章中，我们将深入探讨[直和](@entry_id:156782)与[张量积](@entry_id:140694)的定义、代数性质，并建立强大的[特征标理论](@entry_id:144021)作为计算框架。随后，在“应用与交叉学科联系”一章中，我们将展示这些抽象原理如何在[量子角动量耦合](@entry_id:177285)、粒子物理的[SU(3)](@entry_id:147179)模型以及[大统一理论](@entry_id:150304)的分支规则中发挥关键作用，从而连接理论与实践。最后，通过“动手实践”部分，读者将有机会运用所学知识解决具体的分解问题，从而巩固和深化理解。让我们首先从构建这些表示的基本原理和机制开始。

## 原理与机制

在上一章介绍[群表示论](@entry_id:141930)的基本概念之后，我们现在转向从已有的表示构造新表示的系统性方法。正如在线性代数中，我们可以通过[向量空间](@entry_id:151108)的直和与张量积来构造新的[向量空间](@entry_id:151108)，在表示论中，我们也可以对表示进行类似的操作。这些构造不仅极大地丰富了我们可以研究的表示的种类，而且对于理解物理系统中复合系统的对称性以及群与[子群](@entry_id:146164)之间表示的关联至关重要。本章将深入探讨表示的两种基本组合方式——**直和 (direct sum)** 与**[张量积](@entry_id:140694) (tensor product)**——的原理、性质及其在[表示分解](@entry_id:139061)中的核心作用。

### 表示的组合：[直和](@entry_id:156782)与张量积

假设我们有两个群 $G$ 的表示，$(\rho_V, V)$ 和 $(\rho_W, W)$。我们如何将它们“组合”起来，以生成一个新的、$G$ 的表示？最直接的两种方式是[直和](@entry_id:156782)与[张量积](@entry_id:140694)。

#### 直和：非相互作用系统的叠加

**[直和表示](@entry_id:140467)**的概念是最简单的组合方式。它在物理上对应于将两个独立的、不发生相互作用的系统视为一个整体。表示空间是两个[向量空间](@entry_id:151108)的直和 $V \oplus W$。对于 $V \oplus W$ 中的任意向量 $(v, w)$（其中 $v \in V, w \in W$）以及群元素 $g \in G$，新的表示 $(\rho_{V \oplus W}, V \oplus W)$ 的作用定义为：
$$
\rho_{V \oplus W}(g)(v, w) = (\rho_V(g)v, \rho_W(g)w)
$$
换言之，[群作用](@entry_id:268812)分别独立地作用于 $V$ 和 $W$ 两个[子空间](@entry_id:150286)。如果我们为 $V$ 和 $W$ 选择基，那么 $V \oplus W$ 的基就是这两个基的并集。在此基下，表示矩阵 $\rho_{V \oplus W}(g)$ 具有块[对角形式](@entry_id:264850)：
$$
\rho_{V \oplus W}(g) = \begin{pmatrix} \rho_V(g) & 0 \\ 0 & \rho_W(g) \end{pmatrix}
$$
由于矩阵的迹是对角元素之和，表示的**特征标 (character)** 满足一个简单的加法法则：
$$
\chi_{V \oplus W}(g) = \text{Tr}(\rho_{V \oplus W}(g)) = \text{Tr}(\rho_V(g)) + \text{Tr}(\rho_W(g)) = \chi_V(g) + \chi_W(g)
$$
这个性质是计算[可约表示](@entry_id:137110)特征标的基础。任何[可约表示](@entry_id:137110)都可以分解为不可约表示的直和，因此其特征标就是各不可约分量特征标之和。

#### 张量积：相互作用系统的耦合

**[张量积表示](@entry_id:143629)**是一种更深刻的组合方式。它在物理上常用于描述复合系统，例如，由两个具有自旋的粒子组成的系统，其总的对称性由两个子系统对称性的张量积来刻画。表示空间是[向量空间的张量积](@entry_id:146893) $V \otimes W$。对于 $V \otimes W$ 中的一个简单张量 $v \otimes w$（其中 $v \in V, w \in W$），群元素 $g \in G$ 的作用定义为：
$$
\rho_{V \otimes W}(g)(v \otimes w) = (\rho_V(g)v) \otimes (\rho_W(g)w)
$$
这个定义可以通过线性扩张到整个 $V \otimes W$ 空间。与直和不同，这里的群作用同时“混合”了 $V$ 和 $W$ 的变换。

张量积[表示的特征标](@entry_id:198072)遵循一个同样简洁的[乘法法则](@entry_id:144424)。利用[张量积](@entry_id:140694)的性质 $\text{Tr}(A \otimes B) = \text{Tr}(A)\text{Tr}(B)$，我们得到：
$$
\chi_{V \otimes W}(g) = \text{Tr}(\rho_{V \otimes W}(g)) = \text{Tr}(\rho_V(g) \otimes \rho_W(g)) = \text{Tr}(\rho_V(g)) \cdot \text{Tr}(\rho_W(g)) = \chi_V(g) \chi_W(g)
$$
即，**[张量积的特征标](@entry_id:143383)是特征标的逐点乘积**。这个乘法法则是分解[张量积表示](@entry_id:143629)的关键计算工具。

### 基本性质与[表示环](@entry_id:136421)

[直和](@entry_id:156782)与[张量积](@entry_id:140694)运算满足一些类似于普通算术的代数性质，这些性质将[群的表示](@entry_id:140711)集合构成一个丰富的[代数结构](@entry_id:137052)，即**[表示环](@entry_id:136421) (representation ring)**。

一个关键性质是[张量积](@entry_id:140694)对[直和](@entry_id:156782)的**[分配律](@entry_id:144084)**。对于 $G$ 的三个表示 $V_1, V_2, W$，我们有如下的同构关系：
$$
(V_1 \oplus V_2) \otimes W \simeq (V_1 \otimes W) \oplus (V_2 \otimes W)
$$
这个同构关系在特征标层面表现得尤为清晰：
$$
\chi_{(V_1 \oplus V_2) \otimes W} = (\chi_{V_1} + \chi_{V_2}) \chi_W = \chi_{V_1}\chi_W + \chi_{V_2}\chi_W = \chi_{(V_1 \otimes W) \oplus (V_2 \otimes W)}
$$
我们可以通过一个具体的例子来验证这个性质。考虑[克莱因四元群](@entry_id:138263) $V_4 = \{e, a, b, c\}$，它是一个阿贝尔群，有四个一维[不可约表示](@entry_id:263310) $V_0, V_1, V_2, V_3$。其[特征标表](@entry_id:146676)如下：

| 特征标 | $\chi_i(e)$ | $\chi_i(a)$ | $\chi_i(b)$ | $\chi_i(c)$ |
|:---:|:---:|:---:|:---:|:---:|
| $\chi_0$  | 1         | 1         | 1         | 1         |
| $\chi_1$  | 1         | 1         | -1        | -1        |
| $\chi_2$  | 1         | -1        | 1         | -1        |
| $\chi_3$  | 1         | -1        | -1        | 1         |

让我们来分解表示 $U = (V_1 \oplus V_2) \otimes V_3$ [@problem_id:1644924]。根据[分配律](@entry_id:144084)，其特征标应为 $\chi_U = \chi_{V_1 \otimes V_3} + \chi_{V_2 \otimes V_3} = \chi_1\chi_3 + \chi_2\chi_3$。利用[特征标表](@entry_id:146676)进行逐点乘法：
$$
\chi_1\chi_3 = (1\cdot1, 1\cdot(-1), (-1)\cdot(-1), (-1)\cdot1) = (1, -1, 1, -1) = \chi_2
$$
$$
\chi_2\chi_3 = (1\cdot1, (-1)\cdot(-1), 1\cdot(-1), (-1)\cdot1) = (1, 1, -1, -1) = \chi_1
$$
因此，$\chi_U = \chi_2 + \chi_1 = \chi_{V_2 \oplus V_1}$。这表明表示 $U$ 同构于 $V_1 \oplus V_2$。值得注意的是，对于阿贝尔群，[一维表示](@entry_id:136509)（即[不可约表示](@entry_id:263310)）的张量积仍然是[一维表示](@entry_id:136509)，因此它必然是另一个不可约表示。

另一个重要的构造是**[对偶表示](@entry_id:146263) (dual representation)**，也称为**[共轭表示](@entry_id:139136) (contragredient representation)**。给定表示 $(\rho_V, V)$，其[对偶表示](@entry_id:146263) $(\rho_{V^*}, V^*)$ 在[对偶空间](@entry_id:146945) $V^*$（即从 $V$ 到[复数域](@entry_id:153768) $\mathbb{C}$ 的线性泛函空间）上定义。其特征标与原[表示的特征标](@entry_id:198072)之间有简单的关系：
$$
\chi_{V^*}(g) = \chi_V(g^{-1}) = \overline{\chi_V(g)}
$$
其中上划线表示[复共轭](@entry_id:174690)。最后一个等号对于酉表示总是成立的，而对于有限群的[复表示](@entry_id:144331)，我们总可以将其视为酉表示。

这个性质在研究形如 $V \otimes V^*$ 的[张量积表示](@entry_id:143629)时特别有用。其特征标为：
$$
\chi_{V \otimes V^*}(g) = \chi_V(g) \chi_{V^*}(g) = \chi_V(g) \overline{\chi_V(g)} = |\chi_V(g)|^2
$$
这表明 $\chi_{V \otimes V^*}(g)$ 总是一个非负实数。我们可以利用这一点来计算更复杂组合的特征标。例如，考虑表示 $U = (V \otimes V^*) \oplus (W \otimes W^*)$。其特征标为 $\chi_U(g) = \chi_{V \otimes V^*}(g) + \chi_{W \otimes W^*}(g) = |\chi_V(g)|^2 + |\chi_W(g)|^2$。如果已知 $\chi_V(g) = 2\sqrt{3}i$ 和 $\chi_W(g) = \sqrt{5}i$，则 $\chi_U(g) = |2\sqrt{3}i|^2 + |\sqrt{5}i|^2 = (2\sqrt{3})^2 + (\sqrt{5})^2 = 12 + 5 = 17$ [@problem_id:1604073]。

$V \otimes V^*$ 这个表示具有深刻的意义。它同构于 $V$ 上的线性算子空间 $\text{End}(V)$。这个空间中总存在一个特殊的[子空间](@entry_id:150286)，即**[不变子空间](@entry_id:152829) (invariant subspace)**，记作 $(V \otimes V^*)^G$。其中的向量在所有群元素作用下都保持不变。这个[子空间](@entry_id:150286)的维数等于 $V \otimes V^*$ 分解式中**[平凡表示](@entry_id:141357) (trivial representation)** $V_0$ (其特征标恒为1) 的[重数](@entry_id:136466)。利用[特征标内积](@entry_id:137125)，我们可以计算这个维数：
$$
\dim((V \otimes V^*)^G) = \langle \chi_{V \otimes V^*}, \chi_0 \rangle = \frac{1}{|G|} \sum_{g \in G} \chi_{V \otimes V^*}(g) \overline{\chi_0(g)} = \frac{1}{|G|} \sum_{g \in G} |\chi_V(g)|^2
$$
如果 $V$ 是一个[不可约表示](@entry_id:263310)，根据特征标的[正交关系](@entry_id:145540)，我们有 $\langle \chi_V, \chi_V \rangle = 1$。这意味着：
$$
\frac{1}{|G|} \sum_{g \in G} |\chi_V(g)|^2 = 1
$$
因此，对于任意[不可约表示](@entry_id:263310) $V$，$\dim((V \otimes V^*)^G) = 1$。这个结论是**[舒尔引理](@entry_id:136779) (Schur's Lemma)** 的一个重要推论，它表明不可约表示上的与[群作用](@entry_id:268812)可交换的[线性算子](@entry_id:149003)只能是数乘单位算子。我们可以通过对对称群 $S_4$ 的标准表示来验证这一点 [@problem_id:668496]。$S_4$ 的标准表示 $V$ 是一个3维[不可约表示](@entry_id:263310)。通过计算其特征标在各个[共轭类](@entry_id:143916)上的值的平方和，并考虑到共轭类的大小，可以得到 $\sum_{g \in S_4} |\chi_V(g)|^2 = 24$。由于群的阶 $|S_4|=24$，我们得到 $\dim((V \otimes V^*)^{S_4}) = 24/24 = 1$，与理论预测完全一致。

### [张量积](@entry_id:140694)的分解：Clebsch-Gordan 问题

一个核心问题是：两个不可约[表示的张量积](@entry_id:137150)通常是可约的。那么，它如何分解成不可约表示的直和？即，给定不可约表示 $V_i$ 和 $V_j$，我们希望找到整数系数 $c_{ijk}$，使得：
$$
V_i \otimes V_j \simeq \bigoplus_k c_{ijk} V_k
$$
这个问题在物理学中被称为 **Clebsch-Gordan 问题**。系数 $c_{ijk}$ 称为**[Clebsch-Gordan系数](@entry_id:142551)**或[重数](@entry_id:136466)。在特征标的语言中，这意味着 $\chi_i \chi_j = \sum_k c_{ijk} \chi_k$。利用[特征标的正交性](@entry_id:140971)，我们可以通过[内积](@entry_id:158127)轻易地计算出这些系数：
$$
c_{ijk} = \langle \chi_i \chi_j, \chi_k \rangle = \frac{1}{|G|} \sum_{g \in G} \chi_i(g) \chi_j(g) \overline{\chi_k(g)}
$$
这些系数 $c_{ijk}$ 构成了表示[环的[结](@entry_id:150907)构常数](@entry_id:157960)。

让我们通过一个[非阿贝尔群](@entry_id:141904)的例子来演示这个过程。考虑8阶二面体群 $D_4$（正方形的对称群）。它有一个2维的不可约表示 $\pi_5$，其特征标在5个[共轭类](@entry_id:143916)上的值为 $(2, -2, 0, 0, 0)$。我们来分解张量积 $\pi_5 \otimes \pi_5$ [@problem_id:1653231]。
首先，计算乘积[表示的特征标](@entry_id:198072) $\chi_{5 \otimes 5} = (\chi_5)^2$。其在各个共轭类上的值为 $(2^2, (-2)^2, 0^2, 0^2, 0^2) = (4, 4, 0, 0, 0)$。
接下来，我们将这个特征标与 $D_4$ 的所有不可约特征标 $\chi_l$ ($l=1, \dots, 5$) 做[内积](@entry_id:158127)，以求出重数 $c_{55l} = \langle \chi_5^2, \chi_l \rangle$。例如，对于[平凡表示](@entry_id:141357) $\pi_1$（其特征标为 $(1,1,1,1,1)$），[重数](@entry_id:136466)为：
$$
c_{551} = \frac{1}{8} [1 \cdot 4 \cdot 1 + 1 \cdot 4 \cdot 1 + 2 \cdot 0 \cdot 1 + 2 \cdot 0 \cdot 1 + 2 \cdot 0 \cdot 1] = \frac{8}{8} = 1
$$
（这里我们已将共轭类的大小 $1,1,2,2,2$ 考虑在内）。通过对所有五个不可约表示进行类似的计算，我们发现 $\pi_5 \otimes \pi_5$ 的分解为：
$$
\pi_5 \otimes \pi_5 \simeq \pi_1 \oplus \pi_2 \oplus \pi_3 \oplus \pi_4
$$
这表明，一个2维[不可约表示](@entry_id:263310)的平方可以分解为四个不同的[一维表示](@entry_id:136509)之和。

#### SU(2)的[Clebsch-Gordan级数](@entry_id:137648)

在量子力学中，描述[粒子自旋](@entry_id:142910)的对称性由[特殊酉群](@entry_id:138145) [SU(2)](@entry_id:136274) 或其李代数 $\mathfrak{su}(2)$ 给出。[SU(2)](@entry_id:136274) 的有限维不可约表示由一个非负半整数 $j \in \{0, \frac{1}{2}, 1, \frac{3}{2}, \dots \}$（称为**[自旋量子数](@entry_id:142550)**）标记，记为 $D^{(j)}$。其维数为 $\dim(D^{(j)}) = 2j+1$。

当两个自旋分别为 $j_1$ 和 $j_2$ 的粒子组成一个复合系统时，系统的[状态空间](@entry_id:177074)由[张量积表示](@entry_id:143629) $D^{(j_1)} \otimes D^{(j_2)}$ 描述。这个[张量积表示](@entry_id:143629)的分解规则，即**[Clebsch-Gordan级数](@entry_id:137648)**，是角动量耦合理论的基石：
$$
D^{(j_1)} \otimes D^{(j_2)} = \bigoplus_{J=|j_1-j_2|}^{j_1+j_2} D^{(J)}
$$
其中 $J$ 以整数步长从 $|j_1-j_2|$ 取到 $j_1+j_2$。例如，一个自旋 $j_1 = \frac{5}{2}$ 的粒子和一个自旋 $j_2=2$ 的粒子组成的系统，其总自旋 $J$ 的可能取值为：
$$
J \in \left\{ \left|\frac{5}{2}-2\right|, \dots, \frac{5}{2}+2 \right\} = \left\{ \frac{1}{2}, \frac{3}{2}, \frac{5}{2}, \frac{7}{2}, \frac{9}{2} \right\}
$$
因此，[张量积分解](@entry_id:138873)为 [@problem_id:1638532]：
$$
D^{(\frac{5}{2})} \otimes D^{(2)} = D^{(\frac{1}{2})} \oplus D^{(\frac{3}{2})} \oplus D^{(\frac{5}{2})} \oplus D^{(\frac{7}{2})} \oplus D^{(\frac{9}{2})}
$$
作为一致性检验，我们可以检查维数是否守恒。[张量积](@entry_id:140694)空间的维数是 $\dim(D^{(\frac{5}{2})}) \cdot \dim(D^{(2)}) = (2 \cdot \frac{5}{2} + 1)(2 \cdot 2 + 1) = 6 \cdot 5 = 30$。分解后各分量的维数之和为 $(2\cdot\frac{1}{2}+1) + (2\cdot\frac{3}{2}+1) + \dots + (2\cdot\frac{9}{2}+1) = 2+4+6+8+10=30$，两者相符 [@problem_id:1606866]。

这个分解有着深刻的物理和代数根源。对于 $\mathfrak{su}(2)$ [李代数](@entry_id:137954)，存在一个**[Casimir算子](@entry_id:144193)** $C = \mathbf{J}^2 = J_x^2 + J_y^2 + J_z^2$，它与所有生成元都对易。因此，在任何[不可约表示](@entry_id:263310) $V_j$ 上，它必然是一个[数乘](@entry_id:155971)算子 $C|_{V_j} = j(j+1)I_j$。在[张量积](@entry_id:140694)空间 $V_{j_1} \otimes V_{j_2}$ 上，[总角动量](@entry_id:155748)算子是 $\mathbf{J} = \mathbf{J}_1 \otimes I_2 + I_1 \otimes \mathbf{J}_2$，对应的总[Casimir算子](@entry_id:144193) $C_{\text{tot}}$ 通常不再是一个简单的数乘算子。[Clebsch-Gordan分解](@entry_id:139084)的[实质](@entry_id:149406)，正是将 $V_{j_1} \otimes V_{j_2}$ 分解为 $C_{\text{tot}}$ 的共同本征[子空间](@entry_id:150286)的[直和](@entry_id:156782)。每个[子空间](@entry_id:150286) $V_J$ 对应一个[本征值](@entry_id:154894) $J(J+1)$。

我们可以利用这一点来计算 $C_{\text{tot}}$ 在整个[张量积](@entry_id:140694)空间上的迹 [@problem_id:668600]。考虑 $V_1 \otimes V_2$ 的情况。根据Clebsch-Gordan规则， $V_1 \otimes V_2 = V_1 \oplus V_2 \oplus V_3$。$C_{\text{tot}}$ 在整个空间上的迹等于它在各个不可约[子空间](@entry_id:150286)上迹的和：
$$
\text{Tr}_{V_1 \otimes V_2}(C_{\text{tot}}) = \sum_{J=1}^3 \text{Tr}_{V_J}(C_{\text{tot}}|_{V_J}) = \sum_{J=1}^3 \text{Tr}_{V_J}(J(J+1)I_J)
$$
$$
= \sum_{J=1}^3 \dim(V_J) \cdot J(J+1) = \sum_{J=1}^3 (2J+1)J(J+1)
$$
代入 $J=1, 2, 3$：
$$
\text{Tr}(C_{\text{tot}}) = (3 \cdot 1 \cdot 2) + (5 \cdot 2 \cdot 3) + (7 \cdot 3 \cdot 4) = 6 + 30 + 84 = 120
$$
这展示了[表示分解](@entry_id:139061)如何使复杂算子的分析变得清晰。

### 高阶构造与应用

#### 对称与反对称幂

[张量积](@entry_id:140694) $V \otimes V$ 自身可以被分解。它总能分解为一个**[对称平方](@entry_id:137676) (symmetric square)** $S^2(V)$ 和一个**[外平方](@entry_id:141620) (exterior square)** $\Lambda^2(V)$ 的[直和](@entry_id:156782)：
$$
V \otimes V = S^2(V) \oplus \Lambda^2(V)
$$
$S^2(V)$ 由形如 $v_1 \otimes v_2 + v_2 \otimes v_1$ 的[对称张量](@entry_id:148092)张成，而 $\Lambda^2(V)$ 由形如 $v_1 \otimes v_2 - v_2 \otimes v_1$ 的[反对称张量](@entry_id:199349)张成。在物理学中，这对应于全同粒子的[波函数对称性](@entry_id:141414)（[玻色子](@entry_id:138266)对应[对称张量](@entry_id:148092)，[费米子](@entry_id:146235)对应[反对称张量](@entry_id:199349)）。它们的[特征标公式](@entry_id:142515)为：
$$
\chi_{S^2(V)}(g) = \frac{1}{2} \left[ (\chi_V(g))^2 + \chi_V(g^2) \right]
$$
$$
\chi_{\Lambda^2(V)}(g) = \frac{1}{2} \left[ (\chi_V(g))^2 - \chi_V(g^2) \right]
$$
这些构造可以与[直和](@entry_id:156782)、张量积结合，产生更复杂的表示。例如，我们可以分解 $\Lambda^2(V_{\frac{1}{2}} \oplus V_1)$ [@problem_id:668579]。利用 exterior power 的一般分解公式 $\Lambda^2(U \oplus W) \simeq \Lambda^2(U) \oplus (U \otimes W) \oplus \Lambda^2(W)$，我们有：
$$
\Lambda^2(V_{\frac{1}{2}} \oplus V_1) \simeq \Lambda^2(V_{\frac{1}{2}}) \oplus (V_{\frac{1}{2}} \otimes V_1) \oplus \Lambda^2(V_1)
$$
对于 $\mathfrak{su}(2)$，我们有已知的同构关系 $\Lambda^2(V_{\frac{1}{2}}) = V_0$ （自旋1/2的反对称组合是自旋为0的标量）以及 $\Lambda^2(V_1) = V_1$。而 $V_{\frac{1}{2}} \otimes V_1$ 根据Clebsch-Gordan规则分解为 $V_{\frac{1}{2}} \oplus V_{\frac{3}{2}}$。将这些放在一起，我们得到最终的分解：
$$
\Lambda^2(V_{\frac{1}{2}} \oplus V_1) \simeq V_0 \oplus (V_{\frac{1}{2}} \oplus V_{\frac{3}{2}}) \oplus V_1 = V_0 \oplus V_{\frac{1}{2}} \oplus V_1 \oplus V_{\frac{3}{2}}
$$
这个分解包含了自旋为 $0, 1/2, 1, 3/2$ 的四个不可约分量。

#### [表示的限制](@entry_id:136382)与分支规则

另一个重要的概念是**[表示的限制](@entry_id:136382) (restriction of a representation)**。给定一个群 $G$ 的表示 $(\rho, V)$ 和 $G$ 的一个[子群](@entry_id:146164) $H$，我们可以简单地将映射 $\rho$ 的定义域限制在 $H$ 上。这给我们一个 $H$ 的表示，称为 $V$ 的限制，记作 $\text{Res}_H^G V$。
一个关键现象是，即使 $V$ 作为 $G$ 的表示是不可约的，$\text{Res}_H^G V$ 作为 $H$ 的表示却常常是可约的。将 $\text{Res}_H^G V$ 分解为 $H$ 的[不可约表示](@entry_id:263310)的过程，给出了所谓的**分支规则 (branching rules)**。这在物理学中极为重要，因为它描述了当一个系统的对称性从 $G$ 破缺到其[子群](@entry_id:146164) $H$ 时，原来的能级（$G$ 的不可约表示）如何分裂成新的能级（$H$ 的不可约表示）。

考虑一个例子，将[李代数](@entry_id:137954) $\mathfrak{su}(3)$ 的8维**伴随表示 (adjoint representation)** 限制到其一个极大子代数 $\mathfrak{so}(3)$ [@problem_id:668487]。$\mathfrak{su}(3)$ 的8个生成元可以被看作是伴随表示的基。当我们将伴随作用限制到 $\mathfrak{so}(3)$ 子代数时，这8维[空间分解](@entry_id:755142)成 $\mathfrak{so}(3)$ 的表示。其中，$\mathfrak{so}(3)$ 的3个生成元自身在 $\mathfrak{so}(3)$ 的伴随作用下形成一个不变子空间，这个[子空间](@entry_id:150286)正是 $\mathfrak{so}(3)$ 自身的伴随表示，即自旋为 $j=1$ 的3维[不可约表示](@entry_id:263310)。剩下的5个 $\mathfrak{su}(3)$ 生成元构成了另一个[不变子空间](@entry_id:152829)。由于 $\mathfrak{so}(3)$ 的5维[不可约表示](@entry_id:263310)是唯一的，即自旋为 $j=2$ 的表示，我们便得到了分支规则：
$$
\mathbf{8}_{\mathfrak{su}(3)} \rightarrow \mathbf{3}_{\mathfrak{so}(3)} \oplus \mathbf{5}_{\mathfrak{so}(3)} \quad (\text{或 } j=1 \oplus j=2)
$$

再看一个不同风格的例子：将 $SU(3)$ 的伴随表示限制到其**极大环面 (maximal torus)** $T \cong U(1) \times U(1)$ [@problem_id:668628]。极大环面是 $SU(3)$ 中的[对角矩阵](@entry_id:637782)[子群](@entry_id:146164)。由于 $T$ 是阿贝尔群，其所有不可约表示都是一维的。当任何一个 $SU(3)$ 的表示限制到 $T$ 时，它会分解成一维[表示的直和](@entry_id:138310)。这些一维[表示的特征标](@entry_id:198072)（即权重）对于理解李代数的结构至关重要。对于8维伴随表示，它的分解与 $\mathfrak{su}(3)$ 的**[根系](@entry_id:198970) (root system)** 直接相关。8维[空间分解](@entry_id:755142)为：
- 一个2维的[子空间](@entry_id:150286)，对应**零权重 (zero weight)**。这是[Cartan子代数](@entry_id:191259)本身，它在 $T$ 的伴随作用下不变。因此，它对应2个重数为1的[平凡表示](@entry_id:141357)。所以零权重的重数 $n_0=2$。
- 六个1维的[子空间](@entry_id:150286)，每个对应一个**非零根 (non-zero root)**。每个根空间的[重数](@entry_id:136466)为1，即 $n_\alpha=1$。

因此，伴随表示限制到极大环面后，分解为8个[一维表示](@entry_id:136509)，其中6个是互不相同的，另外2个是[平凡表示](@entry_id:141357)。这些[表示的重数](@entry_id:138441)平方和为 $\sum_\lambda n_\lambda^2 = n_0^2 + \sum_{\alpha \neq 0} n_\alpha^2 = 2^2 + 6 \cdot 1^2 = 10$。这个过程将一个复杂的非[阿贝尔群表示](@entry_id:140513)问题转化为了其可[交换子群](@entry_id:142799)上的分解问题，揭示了表示的精细权重结构。

总结而言，直和与[张量积](@entry_id:140694)不仅是构造新表示的基本工具，更是理解表示结构的核心。通过研究[张量积](@entry_id:140694)的分解（Clebsch-Gordan问题）和[表示的限制](@entry_id:136382)（分支规则），我们得以深入探索群和[李代数](@entry_id:137954)的内在对称性及其在物理世界中的具体体现。[特征标理论](@entry_id:144021)为此提供了强大而优雅的计算框架。