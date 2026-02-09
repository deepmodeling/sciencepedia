## 引言
微分形式上的拉普拉斯算子，或称霍奇-拉普拉斯算子，是现代微分几何与几何分析的基石。对于许多熟悉了外微分和黎曼度量的学习者而言，理解如何将分析方法（如求解偏微分方程）与流形的全局拓扑性质（如贝蒂数）联系起来，是一个关键的知识飞跃。本文旨在填补这一空白，系统阐述霍奇-拉普拉斯算子这一强大工具。

本文将引导读者完成一次从理论构建到实际应用的完整旅程。在“原理与机制”一节中，我们将从零开始构建霍奇-拉普拉斯算子，并深入探讨霍奇理论的核心定理。接下来的“应用与跨学科联系”一节将展示该理论如何成为连接拓扑学、复几何乃至理论物理等领域的桥梁。最后，通过“动手实践”部分，读者将有机会通过解决具体问题来巩固所学知识，将抽象理论付诸实践。

## 原理与机制

本章旨在深入探讨微分形式上的拉普拉斯算子，这是黎曼几何与几何分析中的一个核心工具。我们将从定义其基本构成要素——微分形式上的内积、外微分算子和余微分算子——入手，逐步构建霍奇-拉普拉斯算子（Hodge Laplacian）。随后，我们将阐述霍奇理论的核心成果，包括霍奇分解定理和霍奇-德拉姆定理，它们在微分形式空间和流形的拓扑结构之间建立了深刻的联系。最后，我们将讨论一些更为深入的主题，例如该理论在带边流形上的推广以及与曲率相关的魏岑伯克（Weitzenböck）公式，从而揭示几何与拓扑之间的精妙互动。

### 几何工具箱：内积与算子

在微分形式上定义一个合适的拉普拉斯算子之前，我们必须首先建立其代数和分析基础。这包括在微分形式的向量丛上定义一个逐点内积，并回顾与之相互作用的关键微分算子。

#### 微分形式上的内积

设 $(M^n, g)$ 是一个 $n$ 维黎曼流形。黎曼度量 $g$ 在每一点 $x \in M$ 的切空间 $T_xM$ 上定义了一个内积。通过度量诱导的典范同构（音乐同构）$\sharp: T_x^*M \to T_xM$，这个内积可以被唯一地传递到余切空间 $T_x^*M$ 上。对于任意两个余切向量 $\xi, \eta \in T_x^*M$，我们定义它们的**逐点内积**为 $\langle \xi, \eta \rangle_x := g(\xi^\sharp, \eta^\sharp)$。

这个定义可以代数地推广到任意阶的微分形式上。在 $k$-形式的空间 $\Lambda^k T_x^*M$ 上，内积由以下方式确定：对于两个简单 $k$-形式 $\alpha = v^1 \wedge \dots \wedge v^k$ 和 $\beta = w^1 \wedge \dots \wedge w^k$，它们的内积是其分量内积矩阵的行列式：
$$
\langle \alpha, \beta \rangle_x = \det(\langle v^p, w^q \rangle_x)_{p,q=1,\dots,k}
$$
通过线性扩张，这个定义可以扩展到任意 $k$-形式。这个内积的一个重要性质是，它完全由黎曼度量 $g$ 决定，而与流形的定向无关 [@problem_id:3073727]。

这个构造有一个特别简洁的表述。如果在点 $x$ 处选取一个关于度量 $g$ 的标准正交余切标架 $\{e^1, \dots, e^n\}$，即 $\langle e^i, e^j \rangle_x = \delta^{ij}$，那么由这些基 1-形式构成的 $k$-形式集合 $\{e^{i_1} \wedge \dots \wedge e^{i_k} : 1 \le i_1  \dots  i_k \le n\}$ 构成了 $\Lambda^k T_x^*M$ 的一个标准正交基 [@problem_id:3073727]。

在局部坐标系 $\{x^1, \dots, x^n\}$ 中，度量张量为 $g_{ij}$，其逆矩阵为 $g^{ij}$。一个 $k$-形式 $\alpha$ 可以写为 $\alpha = \frac{1}{k!} \alpha_{i_1 \dots i_k} dx^{i_1} \wedge \dots \wedge dx^{i_k}$（使用爱因斯坦求和约定），其中系数 $\alpha_{i_1 \dots i_k}$ 是全反对称的。那么，两个 $k$-形式 $\alpha$ 和 $\beta$ 的逐点内积可以表示为 [@problem_id:3073727]：
$$
\langle \alpha, \beta \rangle = \frac{1}{k!} g^{i_1 j_1} \dots g^{i_k j_k} \alpha_{i_1 \dots i_k} \beta_{j_1 \dots j_k}
$$

有了逐点内积，我们可以在整个流形 $M$ 的光滑 $k$-形式空间 $\Omega^k(M)$ 上定义一个全局的**$L^2$ 内积**。假设 $M$ 是一个定向流形，度量 $g$ 和定向共同决定了一个典范的体积形式 $\mathrm{vol}_g$。两个 $k$-形式 $\alpha, \beta \in \Omega^k(M)$ 的 $L^2$ 内积定义为：
$$
(\alpha, \beta)_{L^2} := \int_M \langle \alpha, \beta \rangle \mathrm{vol}_g
$$
这个积分是对逐点内积这个标量函数在整个流形上进行积分。如果 $M$ 是紧的，或者 $\alpha$ 和 $\beta$ 至少有一个具有紧支集，那么这个积分总是有限的 [@problem_id:3073727]。这个 $L^2$ 内积结构将微分形式的空间变成了一个（预）希尔伯特空间，为后续的分析奠定了基础。

$L^2$ 内积与霍奇星算子 $*$ 之间有一个重要的关系。霍奇星算子是一个从 $\Omega^k(M)$ 到 $\Omega^{n-k}(M)$ 的线性同构，其定义满足对任意 $\alpha, \beta \in \Omega^k(M)$ 都有 $\alpha \wedge *\beta = \langle \alpha, \beta \rangle \mathrm{vol}_g$。因此，$L^2$ 内积也可以写成：
$$
(\alpha, \beta)_{L^2} = \int_M \alpha \wedge *\beta
$$

#### 外微分算子 ($d$)

**外微分算子** $d: \Omega^k(M) \to \Omega^{k+1}(M)$ 是微分几何中最基本的算子之一。它将 $k$-形式映射到 $(k+1)$-形式，并且可以看作是导数概念到高阶微分形式的推广。它具有两个核心性质：

1.  **次分级莱布尼茨法则 (Graded Leibniz Rule)**：对于 $\alpha \in \Omega^k(M)$ 和 $\beta \in \Omega^\ell(M)$，外微分算子满足如下乘积法则 [@problem_id:3073742]：
    $$
    d(\alpha \wedge \beta) = d\alpha \wedge \beta + (-1)^k \alpha \wedge d\beta
    $$
    当 $k=0$ 时（即 $\alpha$ 是一个函数），这退化为熟悉的函数乘积的微分法则。

2.  **链复合物性质 ($d^2=0$)**：连续两次应用外微分算子总是得到零。即对于任意 $k$-形式 $\alpha$，都有 $d(d\alpha) = 0$ [@problem_id:3073742]。这个深刻的性质是德拉姆上同调理论的基石。在局部坐标下，这个性质可以看作是光滑函数二阶混合偏导数相等（克莱罗定理）的直接推论。

在局部坐标系中，一个 1-形式 $\alpha = \sum_{i=1}^n a_i dx^i$ 的外微分由下式给出：
$$
d\alpha = \frac{1}{2} \sum_{i,j=1}^n \left( \frac{\partial a_j}{\partial x^i} - \frac{\partial a_i}{\partial x^j} \right) dx^i \wedge dx^j
$$
这恰好是向量场 $(a_1, \dots, a_n)$ 的旋度的分量。需要注意的是，公式中的符号是减号，而非加号 [@problem_id:3073742]。

#### 余微分算子 ($\delta$)

与升阶的外微分算子 $d$ 相对，**余微分算子** (codifferential) $\delta: \Omega^k(M) \to \Omega^{k-1}(M)$ 是一个降阶算子。在紧致无边定向黎曼流形上，$\delta$ 最自然的定义是作为 $d$ 在 $L^2$ 内积下的**形式伴随算子** (formal adjoint)。这意味着对于任意光滑的 $(k-1)$-形式 $\alpha$ 和 $k$-形式 $\beta$，以下关系成立 [@problem_id:3068879] [@problem_id:3073727]：
$$
(d\alpha, \beta)_{L^2} = (\alpha, \delta\beta)_{L^2} \quad \text{或者} \quad \int_M \langle d\alpha, \beta \rangle \mathrm{vol}_g = \int_M \langle \alpha, \delta\beta \rangle \mathrm{vol}_g
$$
这个定义是霍奇理论的分析核心。从这个定义出发，可以推导出 $\delta$ 的其他重要性质：

1.  **显式公式**：通过斯托克斯定理和伴随定义，可以推导出 $\delta$ 与霍奇星算子 $*$ 的关系。对于一个 $k$-形式 $\omega$，其显式公式为 [@problem_id:3068879] [@problem_id:2998573]：
    $$
    \delta\omega = (-1)^{n(k+1)+1} *d*\omega
    $$
    公式中的符号因子 $(-1)^{n(k+1)+1}$ 确保了伴随属性的成立，其具体形式可能因作者的约定而略有不同，但奇偶性是确定的。

2.  **幂零性质 ($\delta^2=0$)**：与 $d^2=0$ 类似，余微分算子也满足 $\delta^2=0$。这个性质可以直接从 $\delta$ 是 $d$ 的伴随算子这一事实推断出来。因为 $(AB)^* = B^*A^*$，所以 $(d^2)^* = (d \circ d)^* = d^* \circ d^* = \delta \circ \delta = \delta^2$。由于 $d^2$ 是零算子，其伴随算子 $\delta^2$ 也必然是零算子 [@problem_id:3068879] [@problem_id:2998573]。

3.  **与散度的关系**：在欧氏空间 $\mathbb{R}^n$ 中，余微分算子与向量场的散度有着密切的联系。如果一个 1-形式 $\omega$ 通过音乐同构对应于一个向量场 $X$ (即 $\omega = X^\flat$），那么 $\delta\omega$ (这是一个 0-形式，即一个函数) 等于该向量场散度的负值 [@problem_id:3068879]：
    $$
    \delta\omega = -\operatorname{div} X
    $$
    这个关系为我们理解 $\delta$ 算子提供了一个直观的物理图像。

### 霍奇-拉普拉斯算子 ($\Delta$)

有了外微分算子 $d$ 和余微分算子 $\delta$，我们现在可以定义核心的研究对象——霍奇-拉普拉斯算子。

#### 定义与基本性质

**霍奇-拉普拉斯算子**（Hodge Laplacian），有时也称为拉普拉斯-贝尔特拉米算子（Laplace–Beltrami operator），定义为 [@problem_id:3068879]：
$$
\Delta := d\delta + \delta d
$$
我们来分析这个定义的结构。对于一个 $k$-形式 $\omega \in \Omega^k(M)$：
-   $\delta\omega \in \Omega^{k-1}(M)$，然后 $d(\delta\omega) \in \Omega^k(M)$。
-   $d\omega \in \Omega^{k+1}(M)$，然后 $\delta(d\omega) \in \Omega^k(M)$。
因此，$\Delta$ 是一个从 $\Omega^k(M)$ 到自身的线性算子，即 $\Delta: \Omega^k(M) \to \Omega^k(M)$。它是一个二阶椭圆偏微分算子，推广了我们熟悉的函数上的拉普拉斯算子。

这个定义与所谓的**德拉姆算子** $D = d+\delta$ 密切相关。由于 $d^2=0$ 和 $\delta^2=0$，我们可以计算 $D$ 的平方：
$$
D^2 = (d+\delta)(d+\delta) = d^2 + d\delta + \delta d + \delta^2 = d\delta + \delta d = \Delta
$$
所以，霍奇-拉普拉斯算子可以简洁地看作是德拉姆算子的平方 [@problem_id:2998573]。

#### 函数上的拉普拉斯算子

当霍奇-拉普拉斯算子作用于 0-形式（即函数）$f \in \Omega^0(M)$ 时，定义会简化。因为 $\delta$ 是一个降阶算子，$\delta f = 0$。所以 [@problem_id:3070266]：
$$
\Delta f = (d\delta + \delta d)f = \delta(df)
$$
这提供了一个将几何分析中的霍奇-拉普拉斯算子与经典向量微积分中的拉普拉斯算子联系起来的机会。在黎曼流形上，函数的**梯度** $\nabla f$ 是与 1-形式 $df$ 度量对偶的向量场，即 $g(\nabla f, X) = df(X)$。向量场的**散度** $\operatorname{div} X$ 通常被定义为满足 $\mathcal{L}_X \mathrm{vol}_g = (\operatorname{div} X) \mathrm{vol}_g$ 的函数，其中 $\mathcal{L}_X$ 是李导数。通过积分分部，这等价于定义 $\operatorname{div} X$ 为梯度算子的负伴随，即 $\int_M f(\operatorname{div} X) \mathrm{vol}_g = -\int_M g(\nabla f, X) \mathrm{vol}_g$。

结合我们之前得到的 $\delta\omega = -\operatorname{div}(\omega^\sharp)$ 的关系，令 $\omega = df$，则 $\omega^\sharp = \nabla f$。因此，我们得到了一个至关重要的关系 [@problem_id:3073742] [@problem_id:3073729]：
$$
\Delta f = \delta(df) = -\operatorname{div}(\nabla f)
$$
这个负号是几何学家和分析学家之间符号约定的一个著名差异根源。霍奇-拉普拉斯算子 $\Delta$ 通常被定义为一个**非负算子**。我们可以通过计算 $(\Delta f, f)_{L^2}$ 来验证这一点：
$$
(\Delta f, f)_{L^2} = (\delta(df), f)_{L^2} = (df, df)_{L^2} = \|df\|^2_{L^2} \ge 0
$$
这表明 $\Delta$ 的所有特征值都是非负的。相反，算子 $f \mapsto \operatorname{div}(\nabla f)$（有时也记作 $\nabla^2 f$ 或 $\Delta_{\text{LB}} f$）是一个非正算子，因为 $\int_M f \operatorname{div}(\nabla f) dV = -\int_M \|\nabla f\|^2 dV \le 0$。因此，这两个算子互为相反数 [@problem_id:3073729]。

#### 自伴随性与谱性质

在紧致无边流形上，霍奇-拉普拉斯算子 $\Delta$ 是一个**自伴随算子** (self-adjoint)。这意味着对于任意两个合适的 $k$-形式 $\alpha, \beta$，我们有 $(\Delta\alpha, \beta)_{L^2} = (\alpha, \Delta\beta)_{L^2}$。这个性质可以直接从 $\delta$ 是 $d$ 的伴随算子这一事实推出 [@problem_id:2998573]：
$$
(\Delta\alpha, \beta) = (d\delta\alpha, \beta) + (\delta d\alpha, \beta) = (\delta\alpha, \delta\beta) + (d\alpha, d\beta)
$$
这个表达式在 $\alpha$ 和 $\beta$ 之间是对称的，因此 $(\Delta\alpha, \beta) = (\alpha, \Delta\beta)$。

此外，正如我们已经看到的，$\Delta$ 是一个**非负算子** (non-negative operator)。令 $\beta = \alpha$，我们得到一个核心的恒等式：
$$
(\Delta\alpha, \alpha)_{L^2} = \|d\alpha\|_{L^2}^2 + \|\delta\alpha\|_{L^2}^2 \ge 0
$$
这个恒等式是许多深刻几何结论的出发点。

自伴随性在复希尔伯特空间（例如，$L^2$ 空间复化后的空间）的谱理论中有重要推论。仅从自伴随性的定义，就可以证明以下两条谱性质 [@problem_id:3070290]：
1.  **$\Delta$ 的所有特征值都是实数**。
2.  **对应于不同特征值的特征形式（eigenforms）在 $L^2$ 内积下是正交的**。

这些性质是泛函分析的标准结果，它们保证了 $\Delta$ 具有良好定义的谱分解，这对于流形上的分析至关重要。

### 霍奇理论：核心定理

霍奇理论利用拉普拉斯算子 $\Delta$ 来揭示微分形式空间 $\Omega^k(M)$ 的精细结构，并将其与流形 $M$ 的拓扑性质联系起来。其核心成果是霍奇分解定理和霍奇-德拉姆定理。

#### 调和形式与霍奇分解

一个 $k$-形式 $\omega$ 被称为**调和形式** (harmonic form)，如果它位于霍奇-拉普拉斯算子的核空间中，即 $\Delta\omega = 0$。我们之前推导的恒等式 $(\Delta\omega, \omega)_{L^2} = \|d\omega\|_{L^2}^2 + \|\delta\omega\|_{L^2}^2$ 在这里显示了其威力。由于内积的非负性，$\Delta\omega=0$ 当且仅当 $(\Delta\omega, \omega)_{L^2} = 0$，这又当且仅当 $\|d\omega\|_{L^2}^2 = 0$ 且 $\|\delta\omega\|_{L^2}^2 = 0$。因此，我们得到了调和形式的一个等价且极为有用的刻画 [@problem_id:3070272]：
$$
\omega \text{ is harmonic } \iff \Delta\omega = 0 \iff d\omega = 0 \text{ and } \delta\omega = 0
$$
换言之，一个微分形式是调和的，当且仅当它既是**闭形式** (closed form, $d\omega=0$) 又是**余闭形式** (co-closed form, $\delta\omega=0$)。

所有调和 $k$-形式构成的空间记为 $\mathcal{H}^k(M)$。霍奇理论的第一个主要结果是**霍奇分解定理**。它指出，在紧致无边定向黎曼流形上，任何一个光滑 $k$-形式的空间 $\Omega^k(M)$ 都可以唯一地分解为三个相互正交的子空间的直和 [@problem_id:3070272]：
$$
\Omega^k(M) = \mathcal{H}^k(M) \oplus d\Omega^{k-1}(M) \oplus \delta\Omega^{k+1}(M)
$$
这里，$d\Omega^{k-1}(M)$ 是所有**恰当形式** (exact forms, 形如 $d\beta$) 的空间，而 $\delta\Omega^{k+1}(M)$ 是所有**余恰当形式** (co-exact forms, 形如 $\delta\gamma$) 的空间。这三个子空间的**两两正交性**是该定理的关键部分，可以直接由 $d$ 和 $\delta$ 的伴随性质以及 $d^2=0$ 和 $\delta^2=0$ 证明 [@problem_id:3070272]。例如，一个恰当形式 $d\beta$ 和一个余恰当形式 $\delta\gamma$ 的内积是 $(d\beta, \delta\gamma) = (d^2\beta, \gamma) = (0, \gamma) = 0$。

这个定理意味着任何一个光滑 $k$-形式 $\omega$ 都可以被唯一地写成 $\omega = h + d\beta + \delta\gamma$，其中 $h$ 是调和部分，$d\beta$ 是恰当部分，$\delta\gamma$ 是余恰当部分。这三部分是 $\omega$ 到对应子空间上的正交投影。

#### 通往拓扑的桥梁：霍奇-德拉姆定理

霍奇理论最辉煌的成就是它在流形的几何（由度量 $g$ 和拉普拉斯算子 $\Delta$ 体现）与拓扑（由上同调群和贝蒂数体现）之间建立了一座桥梁。

流形的第 $k$ 个**德拉姆上同调群** $H_{dR}^k(M)$ 定义为闭 $k$-形式模去恰当 $k$-形式的商空间，即 $H_{dR}^k(M) = \ker(d_k) / \mathrm{im}(d_{k-1})$。它的维数，即第 $k$ 个**贝蒂数** (Betti number) $b_k(M) = \dim H_{dR}^k(M)$，是一个拓扑不变量，描述了流形中 "$k$ 维洞" 的数量。

**霍奇-德拉姆定理**指出，在紧致无边定向黎曼流形上，第 $k$ 个德拉姆上同调群与第 $k$ 个调和形式空间之间存在一个典范同构 [@problem_id:3070266]：
$$
H_{dR}^k(M) \cong \mathcal{H}^k(M)
$$
这个同构意味着每个上同调类都包含一个且仅一个调和形式作为其代表。这个定理的一个直接推论是，上同调群的维数等于调和形式空间的维数 [@problem_id:3070266]：
$$
b_k(M) = \dim \mathcal{H}^k(M) = \dim(\ker(\Delta|_{\Omega^k(M)}))
$$
这个等式令人惊叹：左边是一个纯拓扑量，不依赖于任何度量结构；而右边是通过一个依赖于度量的微分算子（拉普拉斯算子）的核空间维度来计算的。定理保证了无论我们选择哪种黎曼度量，算子 $\Delta$ 的核空间维度总是不变的，并且恰好等于贝蒂数。

对于 $k=0$ 的情况，我们有 $b_0 = \dim \mathcal{H}^0(M)$。我们已经知道，调和函数 $f$ 满足 $df=0$，这意味着它们在流形的每个连通分支上都是常数。如果 $M$ 有 $r$ 个连通分支，那么调和函数空间的一组基可以由在每个连通分支上取值为 1 而在其他分支上为 0 的函数构成。因此，$\dim \mathcal{H}^0(M) = r$。所以，第零个贝蒂数 $b_0$ 恰好是流形的连通分支数 [@problem_id:3070266]。例如，对于流形 $M=S^1 \sqcup T^2$（一个圆和一个环面的不交并），它有两个连通分支，因此 $b_0=2$ [@problem_id:3070266]。

### 高等主题与应用

霍奇理论的框架可以推广和深化，引出更高级的结果，并揭示几何与分析之间更深层次的相互作用。

#### 带边流形

到目前为止，我们一直假设流形 $M$ 是紧致且无边界的。这个“无边界”的条件至关重要，因为它保证了在使用斯托克斯定理进行积分分部时没有边界项出现。如果 $M$ 有一个光滑的边界 $\partial M$，情况会变得复杂。

让我们考虑在带边流形上推导算子伴随关系。对于 $\alpha \in \Omega^k(M)$ 和 $\beta \in \Omega^{k+1}(M)$，斯托克斯定理的应用会产生一个边界积分，从而得到如下的**格林第一恒等式** [@problem_id:3070269]：
$$
(d\alpha, \beta)_{L^2(M)} = (\alpha, \delta\beta)_{L^2(M)} + \int_{\partial M} \alpha \wedge *\beta
$$
为了使 $d$ 和 $\delta$ 成为伴随算子，我们需要找到合适的函数空间（定义域），使得这个边界项对其中的所有形式都为零。为了分析这个边界项，我们引入微分形式的**切向迹** (tangential trace) $t\omega := i^*\omega$ 和**法向迹** (normal trace) $n\omega := i^*(\iota_\nu \omega)$，其中 $i: \partial M \to M$ 是包含映射，$\nu$ 是沿边界 $\partial M$ 的向外单位法向量场。可以证明，边界项可以重写为 [@problem_id:3073738]：
$$
\int_{\partial M} \alpha \wedge *\beta = \int_{\partial M} \langle t\alpha, n\beta \rangle_{\partial M} \mathrm{dvol}_{\partial M}
$$
基于这个公式，我们可以推导出拉普拉斯算子的**格林第二恒等式** [@problem_id:3073738]：
$$
(\Delta \omega_1, \omega_2)_{L^2} - (\omega_1, \Delta \omega_2)_{L^2} = \int_{\partial M} \left( \langle t(\delta\omega_1), n\omega_2 \rangle - \langle n(d\omega_1), t\omega_2 \rangle - \langle t(\delta\omega_2), n\omega_1 \rangle + \langle n(d\omega_2), t\omega_1 \rangle \right) \mathrm{dvol}_{\partial M}
$$
为了使 $\Delta$ 自伴随，右边的边界积分必须对定义域中的所有 $\omega_1, \omega_2$ 都为零。这可以通过施加特定的边界条件来实现。两种最常见的边界条件是：

1.  **绝对边界条件 (Absolute boundary conditions)**：对所有定义域中的形式 $\omega$，要求 $n\omega = 0$ 和 $n(d\omega) = 0$。
2.  **相对边界条件 (Relative boundary conditions)**：对所有定义域中的形式 $\omega$，要求 $t\omega = 0$ 和 $t(\delta\omega) = 0$。

在这两种边界条件下，$\Delta$ 都成为自伴随算子，并且霍奇理论的相应版本（绝对上同调或相对上同调）得以成立。若不施加任何边界条件，$\Delta$ 通常不是自伴随的，霍奇-德拉姆定理也不再成立 [@problem_id:3070266] [@problem_id:3073738]。

#### 魏岑伯克公式与曲率

霍奇-拉普拉斯算子与流形的曲率之间存在一个深刻的联系，这个联系由**魏岑伯克公式** (Weitzenböck formula) 所揭示。除了霍奇-拉普拉斯算子 $\Delta$ 之外，我们还可以定义另一个作用于微分形式上的二阶算子，即**联络拉普拉斯算子** (connection Laplacian) $\nabla^*\nabla$。它由列维-奇维塔联络 $\nabla$ 诱导，其定义为 $\nabla^*\nabla \omega = -\sum_i \nabla_{e_i}\nabla_{e_i}\omega$（在一个标准正交标架场 $\{e_i\}$ 下）。

魏岑伯克公式指出，这两个拉普拉斯算子之差是一个零阶算子，即一个纯代数算子，它完全由流形的曲率张量决定：
$$
\Delta = \nabla^*\nabla + \mathcal{F}
$$
其中 $\mathcal{F}$ 是一个曲率项。对于一个具有常截面曲率 $\kappa$ 的流形，可以精确地计算出这个曲率项。作用在 $k$-形式上，$\mathcal{F}$ 算子是一个简单的标量乘法 [@problem_id:3073712]：
$$
\mathcal{F}(\omega) = k(n-k)\kappa \cdot \omega
$$
因此，在常截面曲率流形上，魏岑伯克公式为：
$$
\Delta = \nabla^*\nabla + k(n-k)\kappa \cdot \mathrm{Id}
$$
这个公式是**博赫纳技巧** (Bochner technique) 的基础。通过对魏岑伯克公式积分，我们可以得到一个全局的恒等式。对于一个调和 $k$-形式 $\omega$（即 $\Delta\omega=0$），我们有：
$$
0 = (\Delta\omega, \omega)_{L^2} = (\nabla^*\nabla\omega, \omega)_{L^2} + (k(n-k)\kappa \omega, \omega)_{L^2} = \|\nabla\omega\|^2_{L^2} + k(n-k)\kappa \|\omega\|^2_{L^2}
$$
现在，假设流形是紧致的，且截面曲率 $\kappa > 0$。对于 $1 \le k \le n-1$，系数 $k(n-k)\kappa$ 是严格正的。由于 $\|\nabla\omega\|^2$ 和 $\|\omega\|^2$ 都是非负的，上述等式成立的唯一可能是 $\|\nabla\omega\|^2=0$ 和 $\|\omega\|^2=0$。后者意味着 $\omega=0$。

这个惊人的结论是：在一个具有严格正常截面曲率的紧致流形上，不存在非零的调和 $k$-形式（对于 $1 \le k \le n-1$）。结合霍奇-德拉姆定理 $b_k = \dim \mathcal{H}^k(M)$，这意味着这种流形的中间贝蒂数 $b_1, \dots, b_{n-1}$ 全部为零。这是一个通过分析方法（魏岑伯克公式）从几何性质（正曲率）推导出拓扑性质（贝蒂数消失）的经典范例，完美地展示了现代微分几何的威力与美感。