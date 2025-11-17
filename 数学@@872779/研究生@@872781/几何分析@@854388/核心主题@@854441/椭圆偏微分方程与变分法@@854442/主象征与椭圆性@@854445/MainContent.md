## 引言
在现代数学和物理学中，微分算子是描述各种现象的核心工具。然而，要从复杂的算子表达式中提炼出其本质行为，尤其是在处理高频[振荡](@entry_id:267781)或奇异性时，是一项巨大的挑战。主象征与椭圆性的理论正是在此背景下应运而生，它通过将算子的分析性质与[余切丛](@entry_id:185138)上的代数和几何结构相联系，为这一挑战提供了强有力的解决方案。这一理论不仅是[偏微分方程分析](@entry_id:753283)的基石，更是连接几何、拓扑与物理学的关键纽带。本文旨在系统性地介绍这一深刻而优美的理论。在第一章“原理与机制”中，我们将严格定义主象征，并引入椭圆性的概念，探讨其如何保证解的[光滑性](@entry_id:634843)。随后，在第二章“应用与跨学科联系”中，我们将展示椭圆性理论如何在[连续介质力学](@entry_id:155125)、几何分析、[指标理论](@entry_id:270237)和[规范理论](@entry_id:142992)等多个领域中发挥关键作用。最后，通过第三章“动手实践”中的具体练习，读者将有机会亲手计算和应用这些核心概念。通过这三章的学习，您将掌握一个从代数视角理解微分算子的强大框架，并领会其在现代科学中的广泛影响。

## 原理与机制

在引言之后，我们现在深入探讨主象征与椭圆性的核心原理和机制。本章的目标是建立一个严格的数学框架，将微分算子的分析性质与其在[余切丛](@entry_id:185138)上的代数和几何对应物联系起来。我们将从主象征的定义出发，揭示其作为算子高频行为的几何化身，然后引入椭圆性的概念，并展示其在[正则性理论](@entry_id:194071)、混合阶系统、边值问题乃至全局[指标理论](@entry_id:270237)中的深远影响。

### 主象征的定义与性质

微分算子本质上是局域的，它通过取函数及其导数的线性组合来运作。为了理解算子的深层结构，特别是其在处理高频[振荡](@entry_id:267781)函数时的行为，我们需要一种方法来分离其最重要的部分。主象征正是实现这一目标的关键工具。

#### 从[微分算子](@entry_id:140145)到象征

考虑一个[光滑流形](@entry_id:160799) $M$ 上的两个光滑[复向量丛](@entry_id:276223) $E \to M$ 和 $F \to M$，其秩分别为 $r_E$ 和 $r_F$。一个从 $E$ 的[截面](@entry_id:154995)空间 $\Gamma(E)$ 到 $F$ 的[截面](@entry_id:154995)空间 $\Gamma(F)$ 的 $m$ 阶[线性微分算子](@entry_id:174781) $P$，在任意[局部坐标](@entry_id:181200)卡 $(U; x^1, \dots, x^n)$ 以及 $E$ 和 $F$ 的[局部平凡化](@entry_id:267993)中，可以表示为：
$$
P s = \sum_{|\alpha| \le m} A_{\alpha}(x)\,\partial^{\alpha}s
$$
其中 $\alpha = (\alpha_1, \dots, \alpha_n)$ 是一个多重指标，$|\alpha| = \alpha_1 + \cdots + \alpha_n$，$\partial^{\alpha} = \partial_{x^1}^{\alpha_1} \cdots \partial_{x^n}^{\alpha_n}$。系数 $A_{\alpha}(x)$ 是作用在 $s$ 的局部向量分量上的光滑 $r_F \times r_E$ [矩阵值函数](@entry_id:199897)。算子的阶数为 $m$ 意味着这是表达式中出现的导数的最高阶，并且至少有一个 $|\alpha|=m$ 对应的系数矩阵 $A_{\alpha}(x)$ 不恒为零。[@problem_id:3032869]

这个表达式混合了所有阶数的导数，从 $0$ 阶（乘法算子）到 $m$ 阶。我们的目标是分离出决定算子主要分析性质的“[主部](@entry_id:168896)”。直观上，当作用于高频函数（例如 $s(x) = v e^{i \langle x, \xi \rangle}$，其中“频率” $\xi$ 很大）时，最高阶的导数项将占主导地位，因为每次求导都会引入一个因子 $\xi$。这启发我们将[微分](@entry_id:158718)运算 $\partial_{x^j}$ 替换为一个代数变量 $\xi_j$。

#### 主象征的构造

**主象征 (principal symbol)**，记作 $\sigma_m(P)$，正是通过上述思想精确定义的。它是一个定义在[余切丛](@entry_id:185138) $T^*M$ 上的函数，其在点 $(x, \xi) \in T^*M$（其中 $x \in M, \xi \in T_x^*M$）的值是一个从纤维 $E_x$ 到 $F_x$ 的[线性映射](@entry_id:185132)。在[局部坐标](@entry_id:181200)中，其构造规则如下：

1.  仅保留算子表达式中最高阶（即 $|\alpha|=m$）的项。
2.  用相应的余[切向量](@entry_id:265494)分量 $\xi_j$ 替换[偏导数](@entry_id:146280)算子 $\partial_{x^j}$。更正式地，我们将微分算子 $D_{x_j} = -i\partial_{x_j}$ 替换为 $\xi_j$，从而 $\partial^\alpha$ 被 $(-i\xi)^\alpha$ 替换。为了简化表示，我们常常直接将 $\partial^\alpha$ 替换为 $\xi^\alpha$，这在符号约定上略有不同，但本质相同。我们将遵循后一种约定。

由此，主象征的局部表达式为：
$$
\sigma_m(P)(x, \xi) = \sum_{|\alpha|=m} A_{\alpha}(x) \xi^{\alpha} \in \operatorname{Hom}(E_x, F_x)
$$
其中 $\xi^{\alpha} = \xi_1^{\alpha_1} \cdots \xi_n^{\alpha_n}$。对于给定的 $(x, \xi)$，这是一个 $r_F \times r_E$ 矩阵。由于求和遍及所有 $|\alpha|=m$ 的项，这个矩阵的每个元素都是关于 $\xi = (\xi_1, \dots, \xi_n)$ 的 $m$ 次[齐次多项式](@entry_id:178156)。[@problem_id:3032869]

值得注意的是，主象征只依赖于算子的最高阶部分。任何低阶项（$|\alpha| \lt m$）的修改都不会影响主象征。同样，主象征的定义与联络的选择无关。如果在局部表达式中使用协变导数 $\nabla$ 代替普通偏导数 $\partial$，由于 $\nabla_j - \partial_j$ 是一个零阶算子（即一个矩阵乘法），$\nabla^\alpha$ 与 $\partial^\alpha$ 的差是一个阶数严格小于 $|\alpha|$ 的[微分算子](@entry_id:140145)。因此，这种替换只会改变 $P$ 的低阶项，而 $m$ 阶项的系数 $A_\alpha(|\alpha|=m)$ 保持不变，从而主象征也保持不变。[@problem_id:3032869]

#### 主象征的几何意义

主象征的定义看似依赖于[局部坐标](@entry_id:181200)和丛的平凡化，但实际上它是一个内在的、几何的对象。在[坐标变换](@entry_id:172727)下，算子的系数 $A_\alpha(x)$ 会以一种复杂的方式变化，但其最高阶部分的变化方式恰好能保证 $\sigma_m(P)$ 在[余切丛](@entry_id:185138) $T^*M$（除去零[截面](@entry_id:154995)）上是一个良定义的映射。具体来说，$\sigma_m(P)$ 是从[拉回丛](@entry_id:159346) $\pi^*E$到 $\pi^*F$ 的一个丛同态，其中 $\pi: T^*M \to M$ 是丛投影。这意味着，主象征在某一点 $(x,\xi)$ 的取值是独立于我们如何用坐标来描述这个点和这个余切向量的。[@problem_id:3032864]

主象征的真正威力在于它揭示了算子在高频极限下的行为。考虑在[余切丛](@entry_id:185138)的纤维方向进行尺度变换：$(x, \xi) \mapsto (x, \lambda\xi)$，其中 $\lambda > 0$。这是一个在 $T^*M$ 上有内在几何意义的操作，即纤维内的[标量乘法](@entry_id:155971)。由于主象征 $\sigma_m(P)(x, \xi)$ 是 $\xi$ 的 $m$ 次齐次函数，我们有：
$$
\sigma_m(P)(x, \lambda\xi) = \lambda^m \sigma_m(P)(x, \xi)
$$
算子的全象征（包含所有阶数项）$p(x, \xi) = \sum_{|\alpha| \le m} A_{\alpha}(x) \xi^{\alpha}$ 在此变换下表现为：
$$
p(x, \lambda\xi) = \sum_{|\alpha| \le m} A_{\alpha}(x) (\lambda\xi)^{\alpha} = \sum_{k=0}^m \lambda^k \left( \sum_{|\alpha|=k} A_{\alpha}(x) \xi^{\alpha} \right)
$$
$$
p(x, \lambda\xi) = \lambda^m \sigma_m(P)(x, \xi) + \lambda^{m-1} (\text{m-1 阶项}) + \dots
$$
当 $\lambda \to \infty$ 时，$\lambda^m$ 项的增长速度远超所有其他低阶项。因此，算子的行为由其主象征主导。这个主导性质以及尺度变换本身都是坐标无关的，这凸显了主象征作为算子高频渐进行为的[几何不变量](@entry_id:178611)的核心地位。[@problem_id:3032864]

#### [伪微分算子](@entry_id:192996)的象征

[微分算子](@entry_id:140145)的概念可以推广到**[伪微分算子](@entry_id:192996) (Pseudodifferential Operator, ΨDO)**。一个经典的 $m$ 阶[伪微分算子](@entry_id:192996) $A \in \Psi_{\mathrm{cl}}^m(M)$ 在局部可以表示为一个[振荡积分](@entry_id:137059)，其核由一个称为**全象征 (complete symbol)** 的函数 $a(x, \xi)$ 确定。与微分[算子的多项式](@entry_id:261608)象征不同，[伪微分算子](@entry_id:192996)的全象征是一个更一般的函数，它在 $|\xi|$ 很大时有一个渐进展开：
$$
a(x, \xi) \sim \sum_{j=0}^{\infty} a_{m-j}(x, \xi)
$$
其中每一项 $a_{m-j}(x, \xi)$ 都是关于 $\xi$ 的 $m-j$ 次齐次函数。

在这种更广阔的框架下，**主象征** $\sigma_m(A)$ 被定义为这个渐进展开中的主项，即 $a_m(x, \xi)$。这个主项本身是在 $T^*M \setminus \{0\}$ 上良定义的 $m$ 次齐次函数，其定义方式与[微分算子](@entry_id:140145)的情况完全一致，并且同样具有坐标[不变性](@entry_id:140168)。算子 $A$ 和 $B$ 若有相同的主象征，则它们的差 $A-B$ 是一个阶数至多为 $m-1$ 的算子。因此，主象征可以被看作是商空间 $S^m/S^{m-1}$ 中的一个元素，其中 $S^k$ 代表 $k$ 阶象征类。[@problem_id:3032791]

### 椭圆性：从定义到正则性

有了主象征的工具，我们现在可以定义一类性质极其优良的[微分算子](@entry_id:140145)——[椭圆算子](@entry_id:181616)。

#### 椭圆性的核心概念

一个 $m$ 阶[微分](@entry_id:158718)（或伪[微分](@entry_id:158718)）算子 $P: \Gamma(E) \to \Gamma(F)$ 被称为**[椭圆算子](@entry_id:181616) (elliptic operator)**，如果其主象征 $\sigma_m(P)(x, \xi): E_x \to F_x$ 对于所有 $x \in M$ 和所有**非零**余[切向量](@entry_id:265494) $\xi \in T_x^*M \setminus \{0\}$ 都是一个[线性同构](@entry_id:270529)。[@problem_id:3032869]

这个条件意味着主象征在任何点、任何非零“方向”上都是可逆的。这是一种非常强的均匀性条件。从代数上看，这意味着对于每个 $(x, \xi \neq 0)$，矩阵 $\sigma_m(P)(x, \xi)$ 都是可逆的。

#### 标量算子与算子系统

椭圆性的具体含义取决于算子作用的对象：

*   **标量算子 (Scalar Operators):** 当 $E$ 和 $F$ 都是平凡复线丛时（即算子作用于[复值函数](@entry_id:196054)），$E_x \cong \mathbb{C}$，$F_x \cong \mathbb{C}$。此时，主象征 $\sigma_m(P)(x, \xi)$ 是一个复数。线性映射 $z \mapsto c \cdot z$ 是同构当且仅当 $c \neq 0$。因此，对于标量算子，椭圆性等价于其主象征在 $T^*M \setminus \{0\}$ 上处处非零。[@problem_id:3032879]

*   **算子系统 (Systems of Operators):** 当 $E$ 和 $F$ 是更高秩的向量丛时，$P$ 是一个算子系统。椭圆性要求 $\sigma_m(P)(x, \xi)$ 是一个[线性同构](@entry_id:270529)。根据线性代数的基本定理，两个[有限维向量空间](@entry_id:265491)之间存在同构的必要条件是它们的维数相等。因此，一个算子系统要是椭圆的，其源丛和目标丛的秩必须相等，即 $r_E = r_F$。[@problem_id:3032879]

一个重要的例子是闭黎曼流形 $(M,g)$ 上的**霍奇-德拉姆算子 (Hodge-de Rham operator)** $D = d+d^*$, 它作用在[微分形式](@entry_id:146747)丛 $\Lambda^\bullet T^*M$ 上。这是一个一阶[椭圆算子](@entry_id:181616)。其主象征 $\sigma_1(D)(x, \xi)$ 满足一个关键的代数关系：
$$
\sigma_1(D)(x, \xi)^2 = -|\xi|_g^2 \, \mathrm{Id}
$$
其中 $|\xi|_g$ 是由黎曼度量 $g$ 诱导的 $\xi$ 的范数。当 $\xi \neq 0$ 时，$-|\xi|_g^2$ 是一个非零的负实数，因此 $\sigma_1(D)(x, \xi)$ 显然是可逆的，其逆为 $-\frac{1}{|\xi|_g^2} \sigma_1(D)(x, \xi)$。这证明了 $D$ 的椭圆性。[@problem_id:3032879]

然而，并非所有重要的算子都是椭圆的。例如，在一个复维数 $n \gt 1$ 的[复流形](@entry_id:159076)上，作用于函数上的 $\bar{\partial}$ 算子 $\bar{\partial}: C^\infty(M) \to C^\infty(M, T^{0,1}M^*)$，其源丛是秩为 1 的平凡丛，而目标丛是秩为 $n$ 的 $(0,1)$-形式丛。由于秩不相等，它不可能是椭圆的。[@problem_id:3032879]

#### 强椭圆性

对于偶数阶 $2m$ 的标量算子，我们还可以定义一个更强的概念——**强椭圆性 (strong ellipticity)**。如果存在一个常数 $c>0$，使得对于所有 $(x, \xi \neq 0)$，主象征的实部满足一个一致的强制性条件：
$$
\operatorname{Re}(\sigma_{2m}(P)(x, \xi)) \ge c |\xi|^{2m}
$$
强椭圆性意味着主象征的实部不仅为正，而且以与 $|\xi|^{2m}$ 相同的速度增长。这个条件直接蕴含了椭圆性，因为如果 $\operatorname{Re}(z) \ge c|\xi|^{2m} > 0$，那么 $|z| \ge |\operatorname{Re}(z)| > 0$，所以 $z \neq 0$。[@problem_id:3032862]

然而，反过来不成立。椭圆性并不意味着强椭圆性。例如，考虑一个主象征为 $\sigma_{2m}(P)(x, \xi) = i|\xi|^{2m}$ 的算子。这个象征对于所有 $\xi \neq 0$ 都是非零的，因此算子是椭圆的。但是，它的实部恒为零，不满足任何正的下界条件。因此，存在椭圆但非强椭圆的算子。[@problem_id:3032862]

#### 微局域椭圆性与[波前集](@entry_id:197277)

椭圆性是一个全局概念（要求在所有非零方向上可逆），但我们也可以将其局域化到[余切丛](@entry_id:185138)的某一点上。

算子 $P$ 的**特征集 (characteristic set)** 定义为 $\operatorname{Char}(P) = \{(x, \xi) \in T^*M \setminus \{0\} \mid \sigma_m(P)(x, \xi) \text{ 不可逆}\}$。这是主象征不可逆的点集，也就是算子“退化”的方向。

我们称 $P$ 在点 $(x_0, \xi_0) \in T^*M \setminus \{0\}$ 是**微局域椭圆的 (microlocally elliptic)**，如果 $(x_0, \xi_0)$ 不在特征集内，即 $\sigma_m(P)(x_0, \xi_0)$ 是可逆的。根据连续性，这等价于存在 $(x_0, \xi_0)$ 的一个锥形邻域（在纤维方向上对正[数乘](@entry_id:155971)法封闭）和常数 $c>0$，使得在该邻域内有 $| \det(\sigma_m(P)(x, \xi)) | \ge c |\xi|^{m \cdot r_E}$。[@problem_id:3032782]

微局域椭圆性与[分布](@entry_id:182848)的[正则性理论](@entry_id:194071)紧密相连。一个[分布](@entry_id:182848) $u \in \mathcal{D}'(M)$ 的**[波前集](@entry_id:197277) (wavefront set)** $\operatorname{WF}(u) \subset T^*M \setminus \{0\}$，粗略地说是 $u$ “非光滑”的所有位置和方向的集合。如果 $(x_0, \xi_0) \notin \operatorname{WF}(u)$，我们称 $u$ 在 $(x_0, \xi_0)$ 处是微局域光滑的。

**微局域[椭圆正则性](@entry_id:177548)定理 (Microlocal Elliptic Regularity Theorem)** 阐述了[椭圆算子](@entry_id:181616)与正则性之间的基本关系：对于任意[分布](@entry_id:182848) $u$，我们有如下包含关系：
$$
\operatorname{WF}(u) \subset \operatorname{WF}(Pu) \cup \operatorname{Char}(P)
$$
这个定理的含义是：一个[分布](@entry_id:182848) $u$ 的奇异性，要么已经被算子作用后的结果 $Pu$ 所包含，要么就存在于算子的特征集中。换言之，在算子是微局域椭圆的地方（即非特征点），奇异性不会“凭空产生”。如果 $Pu$ 在某个[椭圆点](@entry_id:273590) $(x_0, \xi_0)$ 处是微局域光滑的（即 $(x_0, \xi_0) \notin \operatorname{WF}(Pu)$），那么 $u$ 在该点也必定是微局域光滑的（即 $(x_0, \xi_0) \notin \operatorname{WF}(u)$）。[@problem_id:3032782] 这个性质是[椭圆算子](@entry_id:181616)理论的基石，它保证了[椭圆方程](@entry_id:169190)解的光滑性。

### 椭圆性的推广与应用

椭圆性的概念可以被推广以适应更复杂的分析情境，并引出深刻的几何与拓扑结果。

#### 混合阶系统的椭圆性

对于由不同阶[微分算子](@entry_id:140145)组成的矩阵 $L=(L_{ij})$，简单的椭圆性定义（要求 $\sigma_m(L)$ 可逆，其中 $m$ 是所有 $L_{ij}$ 阶数的最大值）通常过于粗糙，无法描述系统的真实性质。**Agmon-Douglis-Nirenberg (ADN) 理论**提供了一个更精细的框架。[@problem_id:3032861]

ADN 椭圆性的核心思想是为系统的每个方程（第 $i$ 行）和每个未知函数（第 $j$ 列）引入整数权重 $s_i$ 和 $t_j$。这些权重需要满足阶数条件 $m_{ij} = \operatorname{ord}(L_{ij}) \le s_i + t_j$。然后，我们定义一个**加权主象征矩阵 (weighted principal symbol matrix)** $\sigma_{s,t}(L)(x, \xi)$，其 $(i,j)$ 元素由算子 $L_{ij}$ 中阶数恰好为 $s_i+t_j$ 的项给出：
$$
(\sigma_{s,t}(L)(x, \xi))_{ij} = \sum_{|\alpha| = s_i + t_j} a_{ij, \alpha}(x) \xi^\alpha
$$
如果存在这样一组权重 $s_i, t_j$，使得对于所有 $x \in \Omega$ 和所有非零 $\xi \in \mathbb{R}^n \setminus \{0\}$，加权主象征矩阵 $\sigma_{s,t}(L)(x, \xi)$ 都是可逆的（即其[行列式](@entry_id:142978)非零），那么该系统就被称为 **ADN [椭圆系统](@entry_id:165255)**。这个定义成功地捕捉了混合阶系统中不同算子之间的相互作用。[@problem_id:3032861]

#### 边值问题的椭圆性

当[流形](@entry_id:153038) $M$ 带有边界 $\partial M$ 时，仅有算子 $P$ 的（内部）椭圆性不足以保证方程解的[适定性](@entry_id:148590)，通常还需要施加边界条件。一个边值问题 $(P, B)$ 的椭圆性，其中 $B$ 是一组[边界算子](@entry_id:160216)，依赖于 $P$ 和 $B$ 在边界上的相互作用。

这一相互作用通过**主边界象征 (principal boundary symbol)** 来刻画。考虑边界点 $(x', 0)$ 和一个切向余向量 $\eta$。我们将法向变量 $x_n$ 视为半直线 $[0, \infty)$ 上的变量 $t$，并将法向[微分算子](@entry_id:140145) $D_t = -i\partial_t$ 与法向余向量分量 $\tau$ 对应。主边界象征 $\sigma_b(P)(x', \eta)$ 是一个关于 $t$ 的[常系数](@entry_id:269842)常[微分算子](@entry_id:140145)，通过在内部主象征 $p_m(x', 0, \eta, \tau)$ 中将 $\tau$ 替换为 $D_t$ 得到：
$$
\sigma_b(P)(x', \eta) = p_m(x', 0, \eta, D_t)
$$
这个算子作用在半直线 $[0, \infty)$ 上的[函数空间](@entry_id:143478)上。[@problem_id:3032842]

一个边值问题的椭圆性由 **Lopatinskii-Shapiro 补充条件** 给出。该条件考察模型问题 $p_m(x_0, \xi'+\tau\nu)=0$ 的根 $\tau_j$。其中，虚部 $\operatorname{Im}(\tau_j) > 0$ 的根对应的解 $e^{i\tau_j t}$ 在 $t \to \infty$ 时衰减。这些衰减解张成的[线性空间](@entry_id:151108)记为 $E^+(x_0, \xi')$。Lopatinskii-Shapiro 条件要求，对于每个[边界点](@entry_id:176493) $x_0$ 和每个非零切向余向量 $\xi'$，由[边界算子](@entry_id:160216) $B$ 诱导的边界象征映射
$$
b_m(x_0, \xi', \partial_t): E^+(x_0, \xi') \to \mathbb{C}^k
$$
是一个同构。其中 $k$ 是边界条件的个数。[@problem_id:3032794]

这个条件保证了在每个切向频率下，边界条件能够唯一地确定衰减解，从而确保了边值问题的[适定性](@entry_id:148590)。一个直接的推论是，边界条件的个数 $k$ 必须等于衰减解空间的维数 $\dim E^+(x_0, \xi')$（对于二阶强[椭圆算子](@entry_id:181616)，这个维数通常是 $m/2=1$）。例如，对于[拉普拉斯算子](@entry_id:146319) $\Delta$，$E^+$ 是一维的，所以我们需要一个边界条件。Dirichlet 条件 ($u|_{\partial M} = f$) 和 Neumann 条件 ($\partial_\nu u|_{\partial M} = g$) 都满足 Lopatinskii-Shapiro 条件，因此它们都定义了椭圆边值问题。[@problem_id:3032794]

#### 椭圆性与[指标理论](@entry_id:270237)

[椭圆算子](@entry_id:181616)理论的顶峰是 **Atiyah-Singer [指标定理](@entry_id:637636)**，它在分析、几何和拓扑之间建立了深刻的联系。

对于一个闭[流形](@entry_id:153038) $M$ 上的[椭圆算子](@entry_id:181616) $P: \Gamma(E) \to \Gamma(F)$，其解空间 $\ker P$（核）和 $\operatorname{coker} P$（余核）都是有限维的。其**分析指标 (analytical index)** 定义为：
$$
\operatorname{ind}_{\mathrm{an}}(P) = \dim \ker P - \dim \operatorname{coker} P
$$
这是一个整数，衡量了算子解的“稳定性”。

另一方面，算子的主象征 $\sigma_m(P)$ 定义了一个纯拓扑的对象。由于 $\sigma_m(P)(x, \xi)$ 在 $T^*M \setminus \{0\}$ 上是同构，它定义了从 $\pi^*E$到 $\pi^*F$ 的一个丛同构。利用这个同构，可以通过所谓的“粘合构造”在拓扑 K-理论中定义一个具有[紧支撑](@entry_id:276214)的 K-理论类，记为 $[\sigma_m(P)] \in K^0_c(T^*M)$。[@problem_id:3032799]

Atiyah-Singer [指标定理](@entry_id:637636)的惊人之处在于它断言，分析指标完全由这个拓扑量决定。**拓扑指标 (topological index)** $\operatorname{ind}_{\mathrm{top}}(P)$ 是通过对 K-理论类 $[\sigma_m(P)]$ 进行一系列拓扑操作计算得到的整数。其计算流程如下：
$$
K^{0}_{c}(T^{*}M) \xrightarrow{\pi_{!}} K^{0}(M) \xrightarrow{\operatorname{ch}} H^{\mathrm{even}}(M;\mathbb{Q}) \xrightarrow{\langle \cdot \cup \operatorname{Td}(T_{\mathbb{C}}M), [M]\rangle} \mathbb{Z}
$$
这个过程包括 K-理论中的 Thom 同构（或下推）$\pi_!$，陈特征标 $\operatorname{ch}$，以及与[流形](@entry_id:153038) $M$ 的[复化](@entry_id:260775)[切丛](@entry_id:161294)的 Todd 类相乘并积分。[@problem_id:3032799]

**Atiyah-Singer [指标定理](@entry_id:637636)**：
$$
\operatorname{ind}_{\mathrm{an}}(P) = \operatorname{ind}_{\mathrm{top}}([\sigma_m(P)])
$$
这个定理意味着，一个算子的解的数量（一个分析量）可以通过其象征的[拓扑性质](@entry_id:141605)（一个拓扑量）来计算。由于拓扑量在连续变形下保持不变，定理的一个直接推论是分析指标的[同伦不变性](@entry_id:150428)：如果两个[椭圆算子](@entry_id:181616) $P_0$ 和 $P_1$ 的主象征是同伦的，那么它们的分析指标必然相等。[@problem_id:3032799] 这揭示了[椭圆算子](@entry_id:181616)理论深处的刚性，并将局部分析与全局拓扑完美地结合在一起。