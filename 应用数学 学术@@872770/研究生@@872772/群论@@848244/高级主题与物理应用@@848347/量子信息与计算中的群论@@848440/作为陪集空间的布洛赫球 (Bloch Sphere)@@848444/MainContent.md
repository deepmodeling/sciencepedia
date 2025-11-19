## 引言
布洛赫球是量子信息领域中描述单个[量子比特](@entry_id:137928)状态最直观的工具。然而，在其简洁的几何图像之下，隐藏着深刻的群论结构。本文旨在超越直观描述，揭示布洛赫球作为[陪集空间](@entry_id:180459) SU(2)/U(1) 的严格数学身份，从而为理解[量子态](@entry_id:146142)的几何提供一个坚实的基础。许多学习者将布洛赫球视为一个给定的事实，却不清楚为何单[量子比特](@entry_id:137928)的[纯态](@entry_id:141688)空间必然形成一个二维球面，以及其几何性质为何与[量子操作](@entry_id:145906)如此紧密地联系在一起。本文正是要填补这一知识空白，展示其几何性是如何从量子力学的[基本对称性](@entry_id:161256)原理中自然涌现的。

在接下来的章节中，我们将踏上一段从抽象代数到具体几何的旅程。第一章“原理与机制”将详细阐述 [SU(2)](@entry_id:136274) 群、其[李代数](@entry_id:137954)以及稳定子[子群](@entry_id:146164)的概念，并推导布洛赫球如何作为[陪集空间](@entry_id:180459) $SU(2)/U(1)$ 而产生。第二章“应用与跨学科关联”将展示这一强大框架在[量子计算](@entry_id:142712)、[几何相位](@entry_id:138449)、[对称性破缺](@entry_id:158994)等前沿领域的广泛应用。最后，第三章“动手实践”将通过具体的计算问题，帮助读者巩固所学知识。现在，让我们首先深入其核心，探讨支配[量子比特](@entry_id:137928)世界的数学原理与物理机制。

## 原理与机制

在前一章中，我们介绍了布洛赫球作为描述单[量子比特](@entry_id:137928)[纯态](@entry_id:141688)的直观几何工具。本章将深入探讨其背后的数学原理与物理机制，揭示布洛赫球如何作为一个[陪集空间](@entry_id:180459) $SU(2)/U(1)$ 而自然产生。这一视角不仅为理解[量子态](@entry_id:146142)的几何提供了坚实的群论基础，也为掌握[量子操作](@entry_id:145906)、几何相位以及与广义物理理论的联系开辟了深刻的途径。

### 从[量子态](@entry_id:146142)到几何空间

[量子比特](@entry_id:137928)的状态由二维[复希尔伯特空间](@entry_id:185216) $\mathcal{H} \cong \mathbb{C}^2$ 中的矢量描述。对这些状态的幺正变换由 $2 \times 2$ 的幺[正矩阵](@entry_id:149490) $U$ 给出，且其[行列式](@entry_id:142978)为1。这些矩阵构成了著名的**特殊幺正群 $SU(2)$**。群 $SU(2)$ 的元素可以被视为[量子比特](@entry_id:137928)状态的“旋转”算符。

任何一个[李群](@entry_id:137659)都关联着一个**[李代数](@entry_id:137954) (Lie algebra)**，它描述了群在单位元附近的无穷小变换。$SU(2)$ 的[李代数](@entry_id:137954)，记作 $\mathfrak{su}(2)$，由所有 $2 \times 2$ 的无迹反[厄米矩阵](@entry_id:155147)构成。物理学中，我们通常使用泡利矩阵 $\sigma_k$ 来构造 $\mathfrak{su}(2)$ 的一组基。泡利矩阵本身是厄米的，但乘以虚数单位 $i$ 后就变成了反厄米矩阵：
$$
\sigma_x = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}, \quad \sigma_y = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}, \quad \sigma_z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}
$$
一个物理上常用的 $\mathfrak{su}(2)$ 基是 $T_k = -\frac{i}{2}\sigma_k$（其中 $k \in \{x, y, z\}$）。这些基元被称为群的**生成元**，因为任何 $SU(2)$ 中的元素都可以通过它们的指数映射生成，即 $g = \exp(\sum_k \theta_k T_k)$。

[李代数](@entry_id:137954)的内在结构由其**[李括号](@entry_id:636461) (Lie bracket)** 定义，对于[矩阵李代数](@entry_id:204591)，[李括号](@entry_id:636461)就是矩阵的对易子：$[A, B] = AB - BA$。基元之间的对易关系由**[结构常数](@entry_id:157960) (structure constants)** $f_{jkl}$ 刻画：
$$
[T_j, T_k] = \sum_{l \in \{x,y,z\}} f_{jkl} T_l
$$
这些常数编码了无穷小变换的不可交换性。例如，$[T_x, T_y]$ 描述了围绕 x 轴和 y 轴的[无穷小旋转](@entry_id:166635)以不同顺序作用所产生的净效应。通过直接计算，我们可以揭示 $\mathfrak{su}(2)$ 的基本[代数结构](@entry_id:137052)。利用泡利矩阵的对易关系 $[\sigma_j, \sigma_k] = 2i\sum_l \epsilon_{jkl}\sigma_l$，其中 $\epsilon_{jkl}$ 是[列维-奇维塔符号](@entry_id:193594)，我们得到：
$$
[T_j, T_k] = \left(-\frac{i}{2}\right)^2 [\sigma_j, \sigma_k] = -\frac{1}{4} (2i \epsilon_{jkl} \sigma_l) = \epsilon_{jkl} \left(-\frac{i}{2} \sigma_l\right) = \sum_l \epsilon_{jkl} T_l
$$
因此，$\mathfrak{su}(2)$ 的[结构常数](@entry_id:157960)恰好是[列维-奇维塔符号](@entry_id:193594)，$f_{jkl} = \epsilon_{jkl}$。例如，当我们计算 $f_{xyz}$ 时，我们实际上是在寻找 $[T_x, T_y]$ 展开式中 $T_z$ 的系数。根据上述关系，这个系数是 $\epsilon_{xyz} = 1$ [@problem_id:797551]。这个结果至关重要，因为它表明 $\mathfrak{su}(2)$ 的[代数结构](@entry_id:137052)与三维欧几里得空间中旋转的[代数结构](@entry_id:137052)是相同的。

### $SU(2)$ 与 $SO(3)$ 的深刻联系

上一节的计算结果 $[T_j, T_k] = \sum_l \epsilon_{jkl} T_l$ 表明，李代数 $\mathfrak{su}(2)$ 与三维空间中[旋转生成元](@entry_id:154292)的李代数 $\mathfrak{so}(3)$ 是同构的，即 $\mathfrak{su}(2) \cong \mathfrak{so}(3)$。这个同构是理解布洛赫球几何的核心。

这种联系可以通过**伴随表示 (Adjoint Representation)** 来精确阐述。一个李代数 $\mathfrak{g}$ 的伴随表示是一个映射 $\text{Ad}: \mathfrak{g} \to \text{End}(\mathfrak{g})$，它将代数中的元素 $X$ 映为一个作用于 $\mathfrak{g}$ 自身的线性算符 $\text{Ad}_X$。其作用方式是通过李括号定义的：$\text{Ad}_X(Y) = [X, Y]$。

对于三维的 $\mathfrak{su}(2)$ 代数，我们可以将它看作一个三维[向量空间](@entry_id:151108)，基为 $\{T_x, T_y, T_z\}$。任何元素 $X \in \mathfrak{su}(2)$ 都可以表示为这些基的线性组合。算符 $\text{Ad}_X$ 描述了 $X$ 如何通过对易运算“旋转”代数中的其他元素。由于 $\mathfrak{su}(2)$ 的[结构常数](@entry_id:157960)是 $\epsilon_{jkl}$，这正是在三维空间中[叉积](@entry_id:156672)的[代数表示](@entry_id:143783)。因此，伴随表示提供了一个从 $\mathfrak{su}(2)$ 中的抽象元素到 $\mathbb{R}^3$（布洛赫球所在的[嵌入空间](@entry_id:637157)）中[旋转生成元](@entry_id:154292)的具体映射。

我们可以通过一个具体的计算来体会这一点。考虑 $\mathfrak{su}(2)$ 中的两个任意元素 $A = \alpha T_1 + \beta T_3$ 和 $B = \gamma T_2 + \delta T_1$。它们的对易子 $C = [A, B]$ 也是 $\mathfrak{su}(2)$ 的一个元素。我们可以计算 $C$ 在伴随表示下的作用，例如它作用于 $T_1$ 的结果 $[C, T_1]$。这个结果可以再次按基 $\{T_1, T_2, T_3\}$ 展开。展开式中 $T_3$ 的系数，记作 $(\text{Ad}_C)_{31}$，经过计算可得其值为 $-\beta\delta$ [@problem_id:797558]。这个过程明确显示了 $\mathfrak{su}(2)$ 的代数运算（对易子）如何直接转化为作用在三维[向量空间](@entry_id:151108)上的[线性变换](@entry_id:149133)（由 $3 \times 3$ 矩阵 $\text{Ad}_C$ 表示）。

在群的层面，存在一个从 $SU(2)$到 $SO(3)$ 的**[群同态](@entry_id:140603)**。这个映射是“二对一”的：两个不同的 $SU(2)$ 矩阵，$g$ 和 $-g$，对应于同一个 $SO(3)$ 中的旋转。这揭示了量子力学中自旋的深刻特性，即“旋量”性质。一个在 $SO(3)$ 中旋转 $2\pi$ 的闭合路径（回到起点），当提升到 $SU(2)$ 中时，对应的路径并不是闭合的：它从单位矩阵 $I$ 开始，到 $-I$ 结束。需要旋转 $4\pi$ 才能使 $SU(2)$ 中的路径闭合。这一拓扑特性解释了为什么自旋-1/2粒子的[波函数](@entry_id:147440)在旋转 $2\pi$ 后会获得一个负号（Berry相位的一种体现）。例如，当一个[量子比特](@entry_id:137928)的状态向量在[布洛赫球面](@entry_id:138823)上沿一个闭合回路演化时（例如绕x轴旋转$2\pi$），尽管其布洛赫向量回到了起点，但[量子态](@entry_id:146142)本身却可能获得一个非平庸的相位因子 [@problem_id:797430]。

### 布洛赫球作为[陪集空间](@entry_id:180459) $SU(2)/U(1)$

现在我们来构建核心论点：布洛赫球为何是 $SU(2)/U(1)$ [陪集空间](@entry_id:180459)。

任何一个纯[量子比特](@entry_id:137928)态 $|\psi\rangle$ 都可以通过将一个 $SU(2)$ 变换 $g$ 应用于某个固定的参考态（通常是北极点对应的态 $|0\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$）来获得，即 $|\psi\rangle = g|0\rangle$。然而，这个从群元素到[量子态](@entry_id:146142)的映射是多对一的。其根源在于量子力学的一个基本原理：一个[量子态](@entry_id:146142)乘以一个任意的[全局相位](@entry_id:147947)因子 $e^{i\alpha}$（其中 $\alpha$ 为实数）后，描述的是同一个物理状态。

这意味着，如果两个 $SU(2)$ 矩阵 $g_1$ 和 $g_2$ 所生成的状态仅相差一个相位因子，即 $g_1|0\rangle = e^{i\alpha} g_2|0\rangle$，那么它们代表的是布洛赫球上的同一点。我们可以将此关系改写为 $(g_2^\dagger g_1)|0\rangle = e^{i\alpha}|0\rangle$。

这启发我们定义参考态 $|0\rangle$ 的**[稳定子群](@entry_id:137216) (stabilizer subgroup)** $H$。它由 $SU(2)$ 中所有使 $|0\rangle$ 保持不变（最多相差一个相位）的[元素组成](@entry_id:161166)。对于 $|0\rangle$ 态（布洛赫球的 z 轴正方向），[稳定子群](@entry_id:137216)的元素是所有绕 z 轴的旋转，形式为 $h(\phi) = \exp(-i\frac{\phi}{2}\sigma_z)$。这些元素构成了一个与 $U(1)$ [群同构](@entry_id:147371)的[子群](@entry_id:146164)。

如果 $g_1$ 和 $g_2$ 产生同一个物理态，那么 $h = g_2^\dagger g_1$ 必定是[稳定子群](@entry_id:137216) $H$ 的一个元素。这意味着 $g_1 = g_2 h$。换言之，$g_1$ 和 $g_2$ 属于同一个**[左陪集](@entry_id:143879) (left coset)** $g_2 H$。一个陪集 $gH$ 是将 $H$ 中的每个元素左乘 $g$ 得到的集合。因此，布洛赫球上的每一个点，即每一个物理上可区分的纯态，都与 $SU(2)$ 中 $H$ 的一个唯一[陪集](@entry_id:147145)相对应。所有这些[陪集](@entry_id:147145)的集合被称为**[陪集空间](@entry_id:180459) (coset space)**，记作 $SU(2)/H$，或 $SU(2)/U(1)$。这便是布洛赫球 $S^2$ 的群论身份：$S^2 \cong SU(2)/U(1)$。

这个概念可以通过具体的例子来加深理解。假设有两个 $SU(2)$ 元素 $g_1$ 和 $g_2$，它们通过 $g_2 = g_1 h$ 关联，其中 $h$ 是[稳定子群](@entry_id:137216) $U(1)$ 的一个元素。$h$ 的作用是 $h|0\rangle = e^{-i\Delta\chi}|0\rangle$ 和 $h|1\rangle = e^{i\Delta\chi}|1\rangle$（为了满足 $\det(h)=1$）。我们可以考察 $g_1 g_2^\dagger$ 的迹。利用迹的循环不变性，$\text{Tr}(g_1 g_2^\dagger) = \text{Tr}(g_1 (g_1 h)^\dagger) = \text{Tr}(g_1 h^\dagger g_1^\dagger) = \text{Tr}(h^\dagger)$。计算 $h^\dagger$ 的迹可以得到 $2\cos(\Delta\chi)$ [@problem_id:797405]。这表明，两个代表同一物理态的 $SU(2)$ 元素之间的关系，完全由它们所属的陪集中的 $U(1)$ 相位差决定。

为了使这一抽象概念更加具体，考虑两个看似不同的 $SU(2)$ 变换：
1. $g_1 = \exp(-i\frac{\pi}{4}\sigma_y)$：绕 y 轴旋转 $\pi/2$。
2. $g_2 = \exp(-i\frac{\pi}{2}\frac{\sigma_x+\sigma_z}{\sqrt{2}})$：绕 $(\frac{1}{\sqrt{2}}, 0, \frac{1}{\sqrt{2}})$ 轴旋转 $\pi$。

经过计算可以验证，这两个变换都将北极点 $|0\rangle$ 映射到赤道上同一点 $(\frac{1}{\sqrt{2}}, 0, \frac{1}{\sqrt{2}})$。根据[陪集](@entry_id:147145)理论，必然存在一个[稳定子群](@entry_id:137216)元素 $h \in U(1)$ 使得 $g_1 = g_2 h$。通过求解 $h = g_2^{-1}g_1$，我们可以精确地找到这个连接元素。计算表明 $h = i\sigma_z$ [@problem_id:797481]，它确实是 $U(1)$ [稳定子群](@entry_id:137216)中的一个元素（绕z轴旋转 $\pi$）。这个例子生动地展示了不同的群操作（$g_1, g_2$）如何成为同一物理结果的不同“表示”，它们之间的差异被[稳定子群](@entry_id:137216) $U(1)$ 的一个元素完全吸收。

### [对称空间](@entry_id:181790)与李代数的分解

$S^2 \cong SU(2)/U(1)$ 不仅是一个[陪集空间](@entry_id:180459)，它还是一个特别重要的几何对象——**[黎曼对称空间](@entry_id:193796) (Riemannian symmetric space)**。这一性质蕴含着深刻的代数和几何结构。

对称空间 $G/H$ 的一个关键特征是，群 $G$ 的李代数 $\mathfrak{g}$ 可以分解为两个[子空间](@entry_id:150286)的直和：$\mathfrak{g} = \mathfrak{h} \oplus \mathfrak{m}$。其中 $\mathfrak{h}$ 是[子群](@entry_id:146164) $H$ 的[李代数](@entry_id:137954)，而 $\mathfrak{m}$是 $\mathfrak{h}$ 在一个特定[内积](@entry_id:158127)（通常是[基灵型](@entry_id:161046)）下的正交补。这两个[子空间](@entry_id:150286)满足以下[对易关系](@entry_id:136780)：
$$
[\mathfrak{h}, \mathfrak{h}] \subseteq \mathfrak{h}, \quad [\mathfrak{h}, \mathfrak{m}] \subseteq \mathfrak{m}, \quad [\mathfrak{m}, \mathfrak{m}] \subseteq \mathfrak{h}
$$
对于我们的例子 $SU(2)/U(1)$，在北极点，[李代数](@entry_id:137954) $\mathfrak{su}(2)$ 的分解如下：
- $\mathfrak{h} = \text{span}\{T_z\}$ 是 $U(1)$ [稳定子群](@entry_id:137216)的[李代数](@entry_id:137954)。它生成了保持北极点不变（仅引入相位）的变换。这个方向被称为**垂直[子空间](@entry_id:150286) (vertical subspace)**。
- $\mathfrak{m} = \text{span}\{T_x, T_y\}$ 是 $\mathfrak{h}$ 的[正交补](@entry_id:149922)。它生成的变换会将北极点移开。这个[子空间](@entry_id:150286)可以被等同于球在北极点的**[切空间](@entry_id:199137) (tangent space)**，因此也被称为**水平[子空间](@entry_id:150286) (horizontal subspace)**。

我们可以通过直接计算来验证上述对易关系。
- $[\mathfrak{m}, \mathfrak{m}] \subseteq \mathfrak{h}$：取 $\mathfrak{m}$ 的两个基元 $T_x$ 和 $T_y$。它们的对易子 $[T_x, T_y] = T_z$。由于 $T_z$ 是 $\mathfrak{h}$ 的基元，所以这个关系成立 [@problem_id:797385]。这表明在切空间内的两个[无穷小位移](@entry_id:202209)的交换子是一个垂直方向的变换，即一个纯相位变换。
- $[\mathfrak{h}, \mathfrak{m}] \subseteq \mathfrak{m}$：取 $\mathfrak{h}$ 的基元 $i\sigma_z$ 和 $\mathfrak{m}$ 的基元 $i\sigma_x$。它们的对易子 $[i\sigma_z, i\sigma_x] = (i^2)[\sigma_z, \sigma_x] = - (2i\sigma_y) = -2(i\sigma_y)$ [@problem_id:797435]。由于 $i\sigma_y$ 属于 $\mathfrak{m}$，这个关系也成立。这表明一个垂直方向的变换（相位旋转）作用于一个水平方向的位移，结果仍然是一个水平方向的位移。

这种分解不仅限于北极点。在布洛赫球上的任意一点 $p$（对应布洛赫向量 $\hat{n}$），[李代数](@entry_id:137954) $\mathfrak{su}(2)$ 都可以分解为该点的垂直[子空间](@entry_id:150286) $\mathfrak{h}_p$ 和水平[子空间](@entry_id:150286) $\mathfrak{p}_p$。垂直[子空间](@entry_id:150286) $\mathfrak{h}_p$ 由生成绕 $\hat{n}$ 轴旋转的算符 $i(\hat{n}\cdot\vec{\sigma})$ 张成。水平[子空间](@entry_id:150286) $\mathfrak{p}_p$ 则是 $\mathfrak{h}_p$ 的正交补，对应于在点 $p$ 的所有切向运动。

我们可以将任意一个李代数元素 $X \in \mathfrak{su}(2)$（可视为球面上的一个矢量场）在任意点 $p$分解为它的垂直分量 $X_v$ 和水平分量 $X_h$。$X_v$ 是 $X$ 沿着 $\mathfrak{h}_p$方向的投影，而 $X_h = X - X_v$。例如，考虑一个由向量 $\vec{v}=(1,2,3)$ 定义的[代数元](@entry_id:153893)素 $X = i(\vec{v}\cdot\vec{\sigma})$，以及球面上由 $(\theta, \phi) = (\pi/3, \pi/4)$ 定义的一点 $p$。我们可以计算出 $p$ 点的[单位向量](@entry_id:165907) $\hat{n}$，然后将 $\vec{v}$ 分解为平行于 $\hat{n}$ 的分量 $\vec{v}_v$ 和垂直于 $\hat{n}$ 的分量 $\vec{v}_h$。水平分量 $\vec{v}_h$ 对应的[代数元](@entry_id:153893)素 $X_h = i(\vec{v}_h\cdot\vec{\sigma})$ 就代表了矢量场 $X$ 在 $p$ 点引起的真实物理移动。其范数的平方 $||X_h||^2$ 可以被精确计算出来 [@problem_id:797529]。这种分解是理解平行输运和[几何相位](@entry_id:138449)的关键，因为几何相位正是在沿闭合路径的水平[输运过程](@entry_id:177992)中产生的。

### [代数结构](@entry_id:137052)决定的几何性质

对称空间形式主义的强大之处在于，空间的几何性质，如度规和曲率，完全由其[李代数](@entry_id:137954)的[代数结构](@entry_id:137052)决定。

#### 度规

[李代数](@entry_id:137954) $\mathfrak{su}(2)$ 上自然存在一个[内积](@entry_id:158127)，它与所谓的**[基灵型](@entry_id:161046) (Killing form)**成正比，定义为 $\langle X, Y \rangle = -C \text{Tr}(XY)$，其中 $C$ 是一个正的归一化常数。这个[内积](@entry_id:158127)在群的伴随作用下是不变的。当限制在水平[子空间](@entry_id:150286) $\mathfrak{m}$ 上时，这个[内积](@entry_id:158127)就诱导了[陪集空间](@entry_id:180459) $SU(2)/U(1)$ 上的一个黎曼度规。

我们可以选择合适的常数 $C$，使得这个诱导的度规恰好是单位半径球面 $S^2$ 的标准度规。为此，我们考虑一个无穷小的水平变换 $X \in \mathfrak{m}$。它将北极点的[密度矩阵](@entry_id:139892) $\rho_0 = \frac{1}{2}(I + \sigma_z)$ 变为 $\rho' \approx \rho_0 + [X, \rho_0]$。这个微小变化对应于布洛赫向量的一个位移 $\delta\vec{n}$。标[准球](@entry_id:169696)面度规要求[切向量](@entry_id:265494) $X$ 的代数范数平方 $\langle X, X \rangle$ 等于其对应的几何位移向量 $\delta\vec{n}$ 的欧几里得范数平方 $||\delta\vec{n}||^2$。

通过对任意 $X = \alpha T_1 + \beta T_2 \in \mathfrak{m}$ 进行计算，我们发现 $||\delta\vec{n}||^2 = \alpha^2+\beta^2$。另一方面，$\langle X, X \rangle = -C \text{Tr}(X^2) = \frac{C}{2}(\alpha^2+\beta^2)$。为了使两者相等，我们必须选择 $C=2$ [@problem_id:797442]。这个结果优雅地将[李代数](@entry_id:137954)中的抽象[内积](@entry_id:158127)与我们熟悉的[球面几何](@entry_id:268217)联系了起来。

#### 曲率

对称空间的曲率也可以完全由李代数决定。对于一个由 $\mathfrak{m}$ 中两个[标准正交向量](@entry_id:152061) $X, Y$ 张成的二维切面，其**[截面曲率](@entry_id:159738) (sectional curvature)** $K$ 由以下公式给出：
$$
K(X, Y) = \langle [X, Y], [X, Y] \rangle
$$
由于[对称空间](@entry_id:181790)的性质 $[\mathfrak{m}, \mathfrak{m}] \subseteq \mathfrak{h}$，对易子 $[X, Y]$ 位于垂直[子空间](@entry_id:150286) $\mathfrak{h}$ 中。

让我们使用这个公式计算 $S^2 \cong SU(2)/U(1)$ 的曲率。我们首先需要一个度规，设为 $g(A,B) = -\alpha \text{Tr}(AB)$。在切空间 $\mathfrak{m} = \text{span}\{J_1, J_2\}$ （使用 $J_k = \frac{i}{2}\sigma_k$ 基）中，我们可以构造一组标准正交基 $X, Y$。然后我们计算它们的对易子 $[X, Y]$。这个对易子将正比于 $\mathfrak{h}$ 的基元 $J_3$。最后，我们计算这个对易子在度规 $g$ 下的范数平方。计算结果表明，截面曲率 $K = \frac{2}{\alpha}$ [@problem_id:797589]。

这个结果意义非凡。首先，它表明曲率是一个不依赖于切面选择的常数，这证实了 $S^2$ 是一个[常曲率空间](@entry_id:161841)。其次，它将空间的几何曲率 $K$ 直接与定义代数[内积](@entry_id:158127)的常数 $\alpha$ 联系起来。如果我们选择 $\alpha=2$（这对应于我们之[前推](@entry_id:158718)导出的 $C=2$ 的情况，因为 $T_k = iJ_k$），我们得到 $K=1$，这正是单位半径球面的曲率。这完美地展示了群论方法如何从最基本的代数公理出发，完整地重构出布洛赫球的所有几何特性。

总之，将布洛赫球视为[陪集空间](@entry_id:180459) $SU(2)/U(1)$ 不仅仅是一种数学上的优雅表述。它提供了一个统一的框架，将[量子态](@entry_id:146142)的变换（群 $SU(2)$）、[变换的生成元](@entry_id:172031)（李代数 $\mathfrak{su}(2)$）、物理不可区分性（[稳定子群](@entry_id:137216) $U(1)$）以及最终[状态空间](@entry_id:177074)的几何（度规和曲率）联系在一起。这个强大的视角是现代[量子信息](@entry_id:137721)理论、凝聚态物理和规范场论中许多高级概念的基石。