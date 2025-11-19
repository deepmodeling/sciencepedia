## 引言
在李群与李代数的研究中，伴随与余伴随表示是两个基石性的概念，它们是理解[李理论](@entry_id:148240)内在对称性及其与外部世界联系的钥匙。这些表示不仅是纯粹的代数构造，更是连接[抽象代数](@entry_id:145216)、[微分几何](@entry_id:145818)与理论物理的宏伟桥梁。它们的重要性体现在能够将一个群或代数的复杂结构，转化为其[向量空间](@entry_id:151108)上更易于处理的[线性变换](@entry_id:149133)。然而，这些表示的深刻意义远不止于此，它们为描述从经典力学中的刚体旋转到[量子场论](@entry_id:138177)中的[粒子分类](@entry_id:189151)等广泛现象提供了统一的数学语言。

本文旨在系统地揭示伴随与余伴随表示的理论框架及其广泛应用。我们将从基本定义出发，解决如何精确描述李群与李代数的自作用这一核心问题，并展示这两种表示之间深刻的对偶关系。通过阅读本文，您将学习到：

在“原理和机制”一章中，我们将详细定义[李群](@entry_id:137659)和李代数的伴随与余伴随表示，并通过指数映射揭示它们之间的紧密联系。接着，在“应用与跨学科联系”一章中，我们将探索这些结构在[哈密顿力学](@entry_id:146202)、[几何量子化](@entry_id:159174)、粒子物理及现代几何学等领域的强大威力，展示它们如何将抽象理论转化为解决实际问题的工具。最后，“动手实践”部分将通过一系列具体的计算问题，巩固您对这些核心概念的理解。本文将引导您穿越这片迷人而深刻的数学领域，领略其内在的和谐与力量。

## 原理和机制

在介绍[李群](@entry_id:137659)和李代数的基本概念之后，我们现在转向研究它们表示论中的两个核心结构：伴随表示和余伴随表示。这些表示不仅在[李理论](@entry_id:148240)的内部结构中扮演着中心角色，而且为现代[数学物理](@entry_id:265403)，特别是[几何力学](@entry_id:169959)和量子化理论，提供了基本的框架。本章将系统地阐述这些表示的定义、性质及其深刻的相互关系。

### 伴随表示

伴随表示提供了两种标准方式，使得一个李群或[李代数](@entry_id:137954)可以作用于其自身的李代数上。这种自作用揭示了[李代数](@entry_id:137954)固有的代数和[几何对称性](@entry_id:189059)。

#### 李群的伴随表示 (Ad)

对于一个[李群](@entry_id:137659) $G$，其在自身李代数 $\mathfrak{g}$ 上的**伴随表示 (Adjoint Representation)** 是一个[群同态](@entry_id:140603) $\text{Ad}: G \to \text{GL}(\mathfrak{g})$，定义为：
$$
\text{Ad}_g(Y) = gYg^{-1}, \quad \text{对于 } g \in G, Y \in \mathfrak{g}
$$
这里，$gYg^{-1}$ 被理解为矩阵乘法（如果 $G$ 是一个矩阵群）或者更广义地，通过[共轭作用](@entry_id:143328)。对于每一个固定的 $g \in G$，映射 $\text{Ad}_g: \mathfrak{g} \to \mathfrak{g}$ 是一个[李代数的自同构](@entry_id:193710)，这意味着它保持了李括号结构：$\text{Ad}_g([Y_1, Y_2]) = [\text{Ad}_g(Y_1), \text{Ad}_g(Y_2)]$。

$\text{Ad}$ 表示的几何意义非常直观。由于李代数 $\mathfrak{g}$ 是 $G$ 在[单位元处的切空间](@entry_id:266468) $T_eG$，$\text{Ad}_g$ 描述了群元 $g$ 的[共轭作用](@entry_id:143328)在切空间上诱导的线性变换。

一个极具启发性的例子是[李群](@entry_id:137659) $SU(2)$。$SU(2)$ 的[李代数](@entry_id:137954) $\mathfrak{su}(2)$ 是所有迹为零的 $2 \times 2$ [反埃尔米特矩阵](@entry_id:153530)构成的三维实[向量空间](@entry_id:151108)。一个标准基底可以由泡利矩阵 $\sigma_k$ 导出：$T_k = -\frac{i}{2}\sigma_k$。存在一个著名的[群同态](@entry_id:140603)，将 $SU(2)$ 映射到 $SO(3)$（[三维旋转](@entry_id:148533)群），这个同态实际上就是 $SU(2)$ 的伴随表示。也就是说，对于任意 $g \in SU(2)$，[线性算子](@entry_id:149003) $\text{Ad}_g$ 在 $\mathfrak{su}(2)$ 上引起的变换，等同于三维[欧氏空间](@entry_id:138052) $\mathbb{R}^3$ 中的一个旋转。例如，我们可以通过计算一个[单参数子群](@entry_id:181957) $g(t) = \exp(tX)$ 在[基向量](@entry_id:199546)上的作用来显式地看到这一点 [@problem_id:1033252]。如果 $g(t)$ 对应于绕轴 $\mathbf{n}$ 旋转角度 $\phi(t)$ 的操作，那么 $\text{Ad}_{g(t)}$ 的[矩阵表示](@entry_id:146025)就是相应的 $SO(3)$ [旋转矩阵](@entry_id:140302) $R(\mathbf{n}, \phi)$。

#### 李代数的伴随表示 (ad)

与[李群](@entry_id:137659)的伴随表示相应，[李代数](@entry_id:137954) $\mathfrak{g}$ 也有一种在自身上的表示，称为**李代数的伴随表示 (adjoint representation)**，记作 $\text{ad}$。这是一个[李代数](@entry_id:137954)同态 $\text{ad}: \mathfrak{g} \to \mathfrak{gl}(\mathfrak{g})$，定义为：
$$
\text{ad}_X(Y) = [X, Y], \quad \text{对于 } X, Y \in \mathfrak{g}
$$
其中 $[X, Y]$ 是 $\mathfrak{g}$ 上的李括号，$\mathfrak{gl}(\mathfrak{g})$ 是 $\mathfrak{g}$ 上所有[线性算子](@entry_id:149003)构成的[李代数](@entry_id:137954)（其[李括号](@entry_id:636461)是[算子的交换子](@entry_id:261812)）。[雅可比恒等式](@entry_id:140480) $[X, [Y, Z]] + [Y, [Z, X]] + [Z, [X, Y]] = 0$ 保证了 $\text{ad}$ 确实是一个李代数同态，即 $\text{ad}_{[X,Y]} = [\text{ad}_X, \text{ad}_Y]$。

由于 $\text{ad}_X$ 是一个线性算子，一旦我们为 $\mathfrak{g}$ 选定一个基底 $\{T_1, \dots, T_n\}$，就可以将其表示为一个矩阵。设[李代数](@entry_id:137954)的[结构常数](@entry_id:157960)为 $f_{ij}^k$，定义为 $[T_i, T_j] = \sum_k f_{ij}^k T_k$。那么 $\text{ad}_{T_i}$ 的矩阵表示 $(M_i)$ 的元素为 $(M_i)_{kj} = f_{ik}^j$。

**示例 1：$\mathfrak{su}(2)$ 的伴随表示**
考虑李代数 $\mathfrak{su}(2)$，其基底 $\{T_1, T_2, T_3\}$ 满足 $[T_j, T_k] = \sum_{l=1}^3 \epsilon_{jkl} T_l$，其中 $\epsilon_{jkl}$ 是[列维-奇维塔符号](@entry_id:193594)。对于一个任意元素 $X = \sum_{j=1}^3 x_j T_j \in \mathfrak{su}(2)$，我们来计算 $\text{ad}_X$ 的[矩阵表示](@entry_id:146025) [@problem_id:1033219]。矩阵的第 $k$ 列是 $\text{ad}_X(T_k)$ 在基 $\{T_j\}$ 下的坐标。
$$
\text{ad}_X(T_k) = [X, T_k] = \sum_{j=1}^3 x_j [T_j, T_k] = \sum_{j,l=1}^3 x_j \epsilon_{jkl} T_l
$$
例如，对于 $T_1$：
$$
\text{ad}_X(T_1) = x_2[T_2, T_1] + x_3[T_3, T_1] = x_2(-\epsilon_{123}T_3) + x_3(\epsilon_{312}T_2) = -x_2 T_3 + x_3 T_2
$$
其[坐标向量](@entry_id:153319)为 $(0, x_3, -x_2)^T$。对所有[基向量](@entry_id:199546)进行计算，我们得到 $\text{ad}_X$ 的矩阵表示为：
$$
[\text{ad}_X] = \begin{pmatrix} 0  -x_3  x_2 \\ x_3  0  -x_1 \\ -x_2  x_1  0 \end{pmatrix}
$$
这恰好是三维向量叉乘的矩阵形式：如果我们将 $X$ 对应于向量 $\mathbf{x} = (x_1, x_2, x_3)$，Y 对应于向量 $\mathbf{y} = (y_1, y_2, y_3)$，那么 $[X, Y]$ 对应于叉乘 $\mathbf{x} \times \mathbf{y}$。这个矩阵是一个实反对称矩阵。

**示例 2：$\mathfrak{se}(2)$ 的伴随表示**
作为对比，我们考察[二维欧几里得群](@entry_id:196732) $SE(2)$ 的[李代数](@entry_id:137954) $\mathfrak{se}(2)$，它由[旋转生成元](@entry_id:154292) $J$ 和平移生成元 $P_x, P_y$ 张成。非零的对易关系为 $[J, P_x] = P_y$ 和 $[J, P_y] = -P_x$。对于一个一般元素 $X = \omega J + v_x P_x + v_y P_y$，我们计算其在基 $\{J, P_x, P_y\}$ 下的伴随表示矩阵 [@problem_id:1033117]。
$$
\text{ad}_X(J) = [v_x P_x + v_y P_y, J] = v_x [P_x, J] + v_y [P_y, J] = -v_x (-P_y) + v_y P_x = v_y P_x - v_x P_y \\
\text{ad}_X(P_x) = [\omega J, P_x] = \omega P_y \\
\text{ad}_X(P_y) = [\omega J, P_y] = -\omega P_x
$$
将这些结果表示为列向量，我们得到 $\text{ad}_X$ 的矩阵：
$$
[\text{ad}_X] = \begin{pmatrix} 0  0  0 \\ v_y  0  -\omega \\ -v_x  \omega  0 \end{pmatrix}
$$
这个矩阵不再是反对称的，反映了 $\mathfrak{se}(2)$ 作为一个非[半单李代数](@entry_id:190073)的不同结构。

#### Ad 和 ad 之间的关系

[李群](@entry_id:137659)和[李代数](@entry_id:137954)的伴随表示通过[指数映射](@entry_id:137184)紧密地联系在一起。它们之间的基本关系式是：
$$
\text{Ad}_{\exp(X)} = \exp(\text{ad}_X)
$$
这里的 $\exp(\text{ad}_X)$ 是算子 $\text{ad}_X$ 的[矩阵指数](@entry_id:139347)，定义为 $\exp(A) = \sum_{k=0}^\infty \frac{A^k}{k!}$。这个公式表明，李代数的伴随表示是李群伴随表示在单位元处的“[微分](@entry_id:158718)”。

这个关系式非常强大，它允许我们通过计算李代数层面的量来理解[李群](@entry_id:137659)层面的性质。例如，要计算 $\text{Ad}_{\exp(tX)}$ 的某个性质，我们可以转而研究 $\text{ad}_X$ 的性质 [@problem_id:1033186]。考虑[李代数](@entry_id:137954) $\mathfrak{sl}(2, \mathbb{R})$ 和元素 $X = E+F = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}$。要计算算子 $\text{Ad}_{\exp(tX)}$ 的迹，我们可以利用上述公式，计算 $\text{Tr}(\exp(t \cdot \text{ad}_X))$。根据[矩阵指数](@entry_id:139347)的性质，这个迹等于 $e^{\lambda_i t}$ 的和，其中 $\lambda_i$ 是 $\text{ad}_X$ 的[特征值](@entry_id:154894)。通过计算 $\text{ad}_X$ 在基 $\{H, E, F\}$ 上的作用矩阵，我们发现其[特征值](@entry_id:154894)为 $\{0, 2, -2\}$。因此，
$$
\text{Tr}(\text{Ad}_{\exp(tX)}) = e^{0 \cdot t} + e^{2t} + e^{-2t} = 1 + 2\cosh(2t)
$$
这个例子优美地展示了如何利用[李代数](@entry_id:137954)的谱信息来推断[李群表示](@entry_id:185475)的性质。

### 余伴随表示

与伴随表示对偶的概念是余伴随表示，它描述了[李群](@entry_id:137659)和李代数在其[对偶空间](@entry_id:146945) $\mathfrak{g}^*$ 上的作用。这个概念在哈密顿力学和[几何量子化](@entry_id:159174)中至关重要。

#### 定义与对偶性

令 $\mathfrak{g}^*$ 为 $\mathfrak{g}$ 的对偶空间，即从 $\mathfrak{g}$ 到 $\mathbb{R}$ 的[线性泛函](@entry_id:276136)构成的空间。$\mathfrak{g}$ 和 $\mathfrak{g}^*$ 之间的自然配对记为 $\langle \alpha, Y \rangle$，其中 $\alpha \in \mathfrak{g}^*$，$Y \in \mathfrak{g}$。

**李代数的余伴随表示 (Coadjoint Representation of a Lie algebra)**，记作 $\text{ad}^*$，是映射 $\text{ad}^*: \mathfrak{g} \to \mathfrak{gl}(\mathfrak{g}^*)$，定义为：
$$
(\text{ad}^*_X \alpha)(Y) = -\langle \alpha, [X, Y] \rangle = -\langle \alpha, \text{ad}_X(Y) \rangle, \quad \text{对于 } X, Y \in \mathfrak{g}, \alpha \in \mathfrak{g}^*
$$
定义中的负号是一个惯例，它确保了后续定义的[李-泊松括号](@entry_id:159190)满足雅可比恒等式。从定义可以看出，$\text{ad}^*_X$ 是 $\text{ad}_X$ 的对偶算子（带一个负号）。如果在一个基底下，$\text{ad}_X$ 的矩阵是 $M$，那么在对应的对偶基底下，$\text{ad}^*_X$ 的矩阵就是 $-M^T$。

**示例：$\mathfrak{sl}(2, \mathbb{R})$ 的余伴随表示**
考虑李代数 $\mathfrak{sl}(2, \mathbb{R})$，基底为 $\{H, E, F\}$。对于一个一般元素 $X = xH + yE + zF$，我们来确定 $\text{ad}^*_X$ 在对偶基 $\{H^*, E^*, F^*\}$ 下的矩阵 [@problem_id:1033190]。我们需要计算 $\text{ad}^*_X$ 对每个对偶[基向量](@entry_id:199546)的作用。例如，对于 $H^*$：
$$
(\text{ad}^*_X H^*)(Y) = -H^*([X, Y])
$$
通过在 $Y$ 上分别取 $H, E, F$，我们得到 $\text{ad}^*_X H^*$ 在对偶基下的坐标。
- $Y=H$: $-H^*([X,H]) = -H^*(-2yE+2zF) = 0$
- $Y=E$: $-H^*([X,E]) = -H^*(2xE-zH) = z$
- $Y=F$: $-H^*([X,F]) = -H^*(-2xF+yH) = -y$
所以，$\text{ad}^*_X H^* = zE^* - yF^*$。类似地计算对 $E^*$ 和 $F^*$ 的作用，我们得到 $\text{ad}^*_X$ 的矩阵表示：
$$
[\text{ad}^*_X] = \begin{pmatrix} 0  2y  -2z \\ z  -2x  0 \\ -y  0  2x \end{pmatrix}
$$
通过比较，我们不难验证，该矩阵确实是 $\text{ad}_X$ 矩阵的负转置。

**[李群](@entry_id:137659)的余伴随表示 (Coadjoint Representation of a Lie group)**，记作 $\text{Ad}^*$，是映射 $\text{Ad}^*: G \to \text{GL}(\mathfrak{g}^*)$，定义为：
$$
(\text{Ad}^*_g \alpha)(Y) = \langle \alpha, \text{Ad}_{g^{-1}} Y \rangle, \quad \text{对于 } g \in G, Y \in \mathfrak{g}, \alpha \in \mathfrak{g}^*
$$
与伴随表示一样，$\text{Ad}^*$ 和 $\text{ad}^*$ 通过[指数映射](@entry_id:137184)相连：$\text{Ad}^*_{\exp(X)} = \exp(\text{ad}^*_X)$。

这个公式在处理具体计算时非常有用。例如，在[海森堡代数](@entry_id:204103) $\mathfrak{h}_3$ 中，其对易关系为 $[e_1, e_2] = e_3$，其余为零。对于任何 $A \in \mathfrak{h}_3$，算子 $\text{ad}_A$ 具有[幂零性](@entry_id:147926)，即 $(\text{ad}_A)^2=0$。因此，$(\text{ad}^*_A)^2=0$ 也成立。这意味着[指数映射](@entry_id:137184)被极大地简化了 [@problem_id:1033130]：
$$
\text{Ad}^*_{\exp(A)} = \exp(\text{ad}^*_A) = I + \text{ad}^*_A
$$
这使得在[海森堡群](@entry_id:144785)上计算余伴随作用变得异常简单。

#### [李代数](@entry_id:137954)与其[对偶空间](@entry_id:146945)的同构

当[李代数](@entry_id:137954) $\mathfrak{g}$ 上存在一个**非退化、对称且伴随不变的**双线性形式 $B: \mathfrak{g} \times \mathfrak{g} \to \mathbb{R}$ 时，$\mathfrak{g}$ 和其[对偶空间](@entry_id:146945) $\mathfrak{g}^*$ 之间可以建立一个自然的同构。伴随[不变性](@entry_id:140168)意味着 $B([X, Y], Z) + B(Y, [X, Z]) = 0$ 对于所有 $X, Y, Z \in \mathfrak{g}$ 成立。

该同构 $\phi_B: \mathfrak{g} \to \mathfrak{g}^*$ 定义为：
$$
\langle \phi_B(X), Y \rangle = B(X, Y)
$$
对于所有[半单李代数](@entry_id:190073)，**[基灵型](@entry_id:161046) (Killing form)** $K(X, Y) = \text{Tr}(\text{ad}_X \circ \text{ad}_Y)$ 就是这样一个非退化的双线性形式，它提供了一个典范的同构。

这个同构在 $\text{ad}$ 和 $\text{ad}^*$ 表示之间建立了联系。对于紧致[半单李代数](@entry_id:190073)（如 $\mathfrak{su}(2)$），[基灵型](@entry_id:161046)是负定的。通常使用 $-K$ 作为[内积](@entry_id:158127)，这诱导了 $\mathfrak{g}$ 和 $\mathfrak{g}^*$ 之间的[等距同构](@entry_id:273188)。在这种认同下，$\text{Ad}$ 和 $\text{Ad}^*$ 作用的[矩阵表示](@entry_id:146025)是相同的。这就是为什么在 $SU(2)$ 的例子中，$\text{Ad}^*_g$ 的作用矩阵与 $SO(3)$ [旋转矩阵](@entry_id:140302) $R(g)$ 相同的原因 [@problem_id:1033120]。

在更一般的情况下，不同的[不变双线性形式](@entry_id:137662)会给出不同的同构。例如，在 $\mathfrak{su}(2)$ 上，除了[基灵型](@entry_id:161046) $K(X,Y)$，我们还可以定义一个与之成比例的迹形式 $B(X,Y) = -4 \text{Tr}(XY)$ [@problem_id:1033178]。计算表明，对于我们选择的基底，$K(T_a, T_b) = -2\delta_{ab}$ 而 $B(T_a, T_b) = 2\delta_{ab}$。因此，$K = -B$。这两种形式给出的同构 $\phi_K$ 和 $\phi_B$ 之间只相差一个负号，即 $\phi_K = -\phi_B$。这揭示了对于一个给定的李代数，其几何结构可以有多种等价的描述方式，它们通过简单的变换联系在一起。

### 应用与几何结构：李-泊松[流形](@entry_id:153038)

余伴随表示最重要的应用之一是在[哈密顿力学](@entry_id:146202)中。它为[李代数](@entry_id:137954)的对偶空间 $\mathfrak{g}^*$ 赋予了一个称为**[李-泊松结构](@entry_id:157559) (Lie-Poisson structure)** 的几何结构，使其成为一个相空间。

在 $\mathfrak{g}^*$ 上，两个[光滑函数](@entry_id:267124) $F, H \in C^\infty(\mathfrak{g}^*)$ 的**[李-泊松括号](@entry_id:159190) (Lie-Poisson bracket)** 定义为：
$$
\{F, H\}(\mu) = \langle \mu, [dF_\mu, dH_\mu] \rangle, \quad \text{对于 } \mu \in \mathfrak{g}^*
$$
这里的 $dF_\mu$ 是函数 $F$ 在点 $\mu$ 的[微分](@entry_id:158718)，它被自然地看作是 $\mathfrak{g}$ 中的一个元素（因为 $(\mathfrak{g}^*)^* \cong \mathfrak{g}$）。具体来说，在[坐标系](@entry_id:156346)下，$dF_\mu = \sum_i \frac{\partial F}{\partial \mu_i} T_i$。

用[结构常数](@entry_id:157960) $f_{ij}^k$ 表示，[李-泊松括号](@entry_id:159190)可以写成：
$$
\{F, H\}(\mu) = \sum_{i,j,k} f_{ij}^k \mu_k \frac{\partial F}{\partial \mu_i} \frac{\partial H}{\partial \mu_j}
$$
其中 $\mu_k = \langle \mu, T_k \rangle$ 是坐标函数。这个括号满足[反对称性](@entry_id:261893)和[雅可比恒等式](@entry_id:140480)，因此将 $(\mathfrak{g}^*, \{\cdot, \cdot\})$ 构成一个泊松[流形](@entry_id:153038)。

**示例：$\mathfrak{so}(3)$ 上的[李-泊松括号](@entry_id:159190)**
考虑 $\mathfrak{so}(3)$，其对易关系为 $[L_i, L_j] = \sum_k \epsilon_{ijk} L_k$。其[对偶空间](@entry_id:146945) $\mathfrak{g}^* \cong \mathbb{R}^3$ 上的坐标函数 $\alpha_i = \langle \alpha, L_i \rangle$ 之间的基本括号关系为：
$$
\{\alpha_i, \alpha_j\} = \langle \alpha, [L_i, L_j] \rangle = \langle \alpha, \sum_k \epsilon_{ijk} L_k \rangle = \sum_k \epsilon_{ijk} \alpha_k
$$
这正是三维空间中角动量分量的经典泊松括号。我们可以用这个定义来计算更复杂的括号，例如，对于函数 $f = \frac{1}{2}(\alpha_1^2 + \alpha_2^2)$, $g = \alpha_3$, $h = \alpha_1$，我们可以验证雅可比恒等式的一个实例 $\{f, \{g, h\}\} + \{g, \{h, f\}\} + \{h, \{f, g\}\} = 0$ [@problem_id:1033099]。

#### [哈密顿动力学](@entry_id:156273)

一旦 $\mathfrak{g}^*$ 被赋予了[李-泊松结构](@entry_id:157559)，它就成为了一个哈密顿系统的相空间。系统由一个[哈密顿函数](@entry_id:172864) $H \in C^\infty(\mathfrak{g}^*)$ 描述。任何[可观测量](@entry_id:267133)（即 $\mathfrak{g}^*$ 上的一个函数）$F$ 的时间演化由[哈密顿方程](@entry_id:156213)给出：
$$
\frac{dF}{dt} = \{F, H\}
$$
特别地，坐标函数 $\mu_i$ 的[演化方程](@entry_id:268137)为 $\frac{d\mu_i}{dt} = \{\mu_i, H\}$。

**示例：$\mathfrak{aff}(1, \mathbb{R})$ 上的动力学**
考虑二维[仿射李代数](@entry_id:186784) $\mathfrak{aff}(1, \mathbb{R})$，由伸缩元 $D$ 和平移元 $T$ 张成，满足 $[D, T] = T$。其[对偶空间](@entry_id:146945) $\mathfrak{g}^*$ 上的坐标为 $\mu_D, \mu_T$。基本[李-泊松括号](@entry_id:159190)为：
$$
\{\mu_D, \mu_T\} = \langle \mu, [D, T] \rangle = \langle \mu, T \rangle = \mu_T
$$
假设一个动力学系统由[哈密顿量](@entry_id:172864) $H = \alpha \mu_D \mu_T$ 描述 [@problem_id:1033276]。坐标的[演化方程](@entry_id:268137)为：
$$
\frac{d\mu_D}{dt} = \{\mu_D, H\} = \{\mu_D, \alpha \mu_D \mu_T\} = \alpha \mu_D \{\mu_D, \mu_T\} = \alpha \mu_D \mu_T
$$
$$
\frac{d\mu_T}{dt} = \{\mu_T, H\} = \{\mu_T, \alpha \mu_D \mu_T\} = \alpha \mu_T \{\mu_T, \mu_D\} = -\alpha \mu_T^2
$$
这是一组可以求解的[常微分方程](@entry_id:147024)。对于初始条件 $\mu_D(0)=x_0, \mu_T(0)=p_0$，解为：
$$
\mu_T(t) = \frac{p_0}{1+\alpha p_0 t}, \quad \mu_D(t) = x_0 (1 + \alpha p_0 t)
$$
这个例子完美地展示了从一个抽象的李[代数结构](@entry_id:137052)出发，如何通过余伴随表示和[李-泊松括号](@entry_id:159190)，最终得到一个具体物理系统的可解[动力学方程](@entry_id:751029)。

一个重要的概念是**[卡西米尔函数](@entry_id:166674) (Casimir function)**，它是一个与所有函数[泊松括号](@entry_id:151133)为零的函数 $C$，即 $\{C, F\} = 0$ 对所有 $F$ 成立。[卡西米尔函数](@entry_id:166674)是任何[哈密顿系统](@entry_id:143533)在 $\mathfrak{g}^*$ 上的守恒量，因为 $\frac{dC}{dt} = \{C, H\} = 0$。这些守恒量定义了余伴随[轨道](@entry_id:137151)，它们是 $\mathfrak{g}^*$ 上的[辛叶](@entry_id:158259)，构成了相空间的基本不可约单元。

总之，伴随与余伴随表示是探索李群和[李代数](@entry_id:137954)内在对称性的基本工具。它们不仅连接了群与代数的结构，还通过李-泊松几何为[哈密顿力学](@entry_id:146202)提供了统一而深刻的代数框架。