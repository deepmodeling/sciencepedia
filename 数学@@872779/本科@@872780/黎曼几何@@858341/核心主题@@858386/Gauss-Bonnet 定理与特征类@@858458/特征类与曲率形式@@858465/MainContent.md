## 引言
一个空间的局部弯曲程度如何决定其整体的拓扑形态？这是现代几何学最核心的问题之一。在[微分几何](@entry_id:145818)中，我们使用“曲率”来精确度量一个[流形](@entry_id:153038)在每一点的局部弯曲情况；而在代数拓扑中，我们使用“[示性类](@entry_id:160596)”等[不变量](@entry_id:148850)来刻画其无法通过连续变形改变的全局结构。这两种看似截然不同的概念之间，存在着一条深刻而优美的数学桥梁，而本文的目的正是系统地阐释这一联系。

本文将引导读者踏上一段从局部几何到全局拓扑的旅程，内容分为三个核心部分。首先，在“原理与机制”一章中，我们将深入探讨数学基础，从[联络与曲率](@entry_id:158520)的定义出发，揭示陈-韦伊同态如何将局部的[曲率形式](@entry_id:199387)转化为全局的示性类。接着，在“应用与跨学科联系”一章中，我们将通过陈-[高斯-博内定理](@entry_id:160424)、霍普夫丛等经典案例，展示这一理论在微分几何、代数几何乃至理论物理中的强大应用。最后，为了将理论付诸实践，“动手实践”部分提供了一系列计算练习，帮助读者巩固对联络、曲率和示性数计算的掌握。通过这三个章节的学习，读者将对[示性类](@entry_id:160596)与[曲率形式](@entry_id:199387)之间的内在联系建立起一个清晰而完整的认识。

## 原理与机制

本章在前一章介绍性概述的基础上，深入探讨了[示性类](@entry_id:160596)理论的数学核心。我们将从联络和曲率的基本概念出发，它们是微分几何中用于描述弯曲空间的语言。随后，我们将展示这些局部几何量如何通过一个被称为陈-韦伊同态（Chern–Weil homomorphism）的精妙机制，生成独立于局部细节的全局拓扑不变量——[示性类](@entry_id:160596)。本章的目标是系统性地揭示从几何到拓扑的完整路径，并阐明陈类（Chern classes）、[庞特里亚金类](@entry_id:161084)（Pontryagin classes）和[欧拉类](@entry_id:161259)（Euler class）等主要示性类的[构造原理](@entry_id:141667)。

### 联络与协变导数：平行的语言

在[欧几里得空间](@entry_id:138052) $\mathbb{R}^n$ 中，我们可以轻易地比较不同点的向量，因为存在一个全局的、自然的平行移动方式。然而，在一个一般的弯曲[流形](@entry_id:153038) $M$ 上，[切空间](@entry_id:199137) $T_pM$ 在不同点 $p$ 是相互独立的。为了[微分](@entry_id:158718)[流形上的向量](@entry_id:160178)场（即[向量丛的截面](@entry_id:270734)），我们需要一个能够“连接”相邻纤维的工具，这就是**联络（connection）**的概念。

联络最直观的体现是**[协变导数](@entry_id:152476)（covariant derivative）**。对于一个秩为 $r$ 的光滑向量丛 $E \to M$，其上的一个协变导数 $\nabla$ 是一个算子，它取一个向量场 $X \in \Gamma(TM)$ 和一个 $E$ 的[截面](@entry_id:154995) $s \in \Gamma(E)$，生成一个新的[截面](@entry_id:154995) $\nabla_X s \in \Gamma(E)$。这个算子推广了函数沿向量场方向求导的概念，并满足以下两个核心性质 [@problem_id:3038949]：

1.  **$C^\infty(M)$-线性于向量场（张量性）**：对于任意[光滑函数](@entry_id:267124) $f \in C^\infty(M)$，
    $$
    \nabla_{fX} s = f \nabla_X s
    $$
    此性质表明，$\nabla_X s$ 在点 $p$ 的值仅依赖于向量 $X_p \in T_pM$，而与 $X$ 在 $p$ 点邻域内的形态无关。这使得[协变导数](@entry_id:152476)成为一个逐点的、几何的操作。

2.  **[莱布尼茨法则](@entry_id:157949)（Leibniz rule）**：对于任意光滑函数 $f \in C^\infty(M)$，
    $$
    \nabla_X (f s) = (Xf)s + f(\nabla_X s)
    $$
    其中 $Xf$ 是函数 $f$ 沿 $X$ 的方向导数。这个法则是协变导数的关键特征，它描述了导数如何与[截面](@entry_id:154995)乘函数的[代数结构](@entry_id:137052)相互作用。注意，$\nabla_X$ 关于[截面](@entry_id:154995) $s$ 并不是 $C^\infty(M)$-线性的，这正是它与张量的根本区别。

[协变导数](@entry_id:152476)也可以等价地看作一个算子 $\nabla: \Gamma(E) \to \Gamma(T^*M \otimes E)$，它将一个[截面](@entry_id:154995) $s$ 映为一个 $E$ 值的1-形式 $\nabla s$。这两个观点通过关系 $\nabla_X s := \langle \nabla s, X \rangle$ 联系起来。在这种观点下，[莱布尼茨法则](@entry_id:157949)表现为：
$$
\nabla(fs) = df \otimes s + f \nabla s
$$
其中 $df$ 是函数 $f$ 的外微分。这个表达式清晰地分离了对函数 $f$ 的[微分](@entry_id:158718)和对[截面](@entry_id:154995) $s$ 的[协变微分](@entry_id:263981)。

[协变导数](@entry_id:152476)的核心功能是定义了**平行输运（parallel transport）**。给定一条曲线 $\gamma: [0,1] \to M$，一个沿 $\gamma$ 的[截面](@entry_id:154995) $s(t) \in E_{\gamma(t)}$ 被称为是平行的，如果它的[协变导数](@entry_id:152476)为零，即 $\nabla_{\dot{\gamma}(t)}s(t) = 0$。这个方程的解为我们提供了从起点 $E_{\gamma(0)}$ 到终点 $E_{\gamma(1)}$ 的[线性同构](@entry_id:270529) $P_\gamma: E_{\gamma(0)} \to E_{\gamma(1)}$。这个同构就是沿曲线 $\gamma$ 的平行输运。

### 曲率：不[可积性](@entry_id:142415)之度量

平行输运的一个至关重要的特性是它依赖于路径。在一个弯曲的空间中，沿两条不同路径将一个向量从一点输运到另一点，结果通常是不同的。更引人注目的是，将一个向量沿一条闭合回路进行平行输运，当它返回起点时，通常不会变回原来的向量。**曲率（curvature）**正是对这种[路径依赖性](@entry_id:186326)的局部度量。

代数上，**曲率张量**或**[曲率算子](@entry_id:198006)**被定义为协变导数[交换子](@entry_id:158878)的[非对易](@entry_id:136599)部分：
$$
R(X,Y)s = \nabla_X \nabla_Y s - \nabla_Y \nabla_X s - \nabla_{[X,Y]}s
$$
其中 $X, Y$ 是向量场，$s$ 是[截面](@entry_id:154995)。如果曲率为零（即联络是平坦的），则[二阶协变导数](@entry_id:193368)的顺序无关紧要（除去李括号项的影响），且平行输运与路径无关。

曲率的几何意义可以通过**和乐（holonomy）**来精确阐述。考虑在点 $p$ 附近由两个[切向量](@entry_id:265494) $v, w \in T_pM$ 张成的一个无穷小平行四边形回路 $\gamma_\varepsilon$。将纤维 $E_p$ 中的一个向量沿此回路[平行输运](@entry_id:160671)，得到的变换 $U_\varepsilon: E_p \to E_p$ 会非常接近于[恒等变换](@entry_id:264671) $I$。[曲率张量](@entry_id:181383)描述了这个变换的一阶偏离：
$$
U_\varepsilon \approx I + \varepsilon^2 R_p(v,w) + O(\varepsilon^3)
$$
这个关系表明，曲率是无穷小和乐的生成元。一个更精确的表述是，[和乐](@entry_id:137051)变换的[行列式](@entry_id:142978)与[曲率形式](@entry_id:199387)的迹（trace）相关。对于一个酉联络，有如下关系 [@problem_id:3038926]：
$$
\lim_{\varepsilon \to 0}\frac{1}{\varepsilon^2}\,\ln \det(U_\varepsilon) = \operatorname{tr}\big(\Omega_p(v,w)\big)
$$
其中 $\Omega$ 是曲率的2-形式表示（将在下一节介绍）。

这个思想被**[Ambrose-Singer定理](@entry_id:198517)**推广到全局层面 [@problem_id:303908]。它断言，在点 $p$ 的**[和乐群](@entry_id:191471)** $\mathrm{Hol}_p(\nabla)$（由所有以 $p$ 为基点的闭回路的[平行输运](@entry_id:160671)变换构成的群）的李代数 $\mathfrak{hol}_p(\nabla)$，恰好是由[流形](@entry_id:153038)上所有点的[曲率算子](@entry_id:198006)通过[平行输运](@entry_id:160671)“[拉回](@entry_id:160816)”到点 $p$ 的所有算子所生成的。具体来说，$\mathfrak{hol}_p(\nabla)$ 是由形如 $P_\gamma^{-1} \circ R_q(X,Y) \circ P_\gamma$ 的所有算子生成的最小李代数，其中 $q$ 是[流形](@entry_id:153038)上任意一点，$\gamma$ 是从 $p$ 到 $q$ 的任意路径。这个深刻的定理建立了局部曲率与全局[和乐](@entry_id:137051)之间的直接桥梁。

### [标架场](@entry_id:160577)中的[联络与曲率](@entry_id:158520)：嘉当形式

为了进行具体的计算，我们常常将抽象的算子转化为在[局部标架](@entry_id:635789)场（local frame）下的矩阵形式。这种方法由[Élie Cartan](@entry_id:263871)发展，被称为[移动标架](@entry_id:175562)法。

考虑一个[主丛](@entry_id:160029)，例如[黎曼流形](@entry_id:261160) $(M,g)$ 上的定向正交[标架丛](@entry_id:187852) $SO(M)$。其结构群为[特殊正交群](@entry_id:146418) $SO(n)$。一个与度规相容的[协变导数](@entry_id:152476) $\nabla$ 可以等价地由该[主丛](@entry_id:160029)上的一个**[联络1-形式](@entry_id:275839)（connection 1-form）** $\omega$ 描述 [@problem_id:3038916]。这是一个在[主丛](@entry_id:160029) $SO(M)$ 上定义的、取值于李代数 $\mathfrak{so}(n)$ 的[1-形式](@entry_id:270392)。

在一个[局部定向](@entry_id:264384)正交[标架场](@entry_id:160577) $\{e_i\}$（它是 $SO(M)$ 的一个局部[截面](@entry_id:154995) $s: U \to SO(M)$）下，这个全局的[联络形式](@entry_id:263247) $\omega$ 被[拉回](@entry_id:160816)到基[流形](@entry_id:153038) $M$ 的开集 $U$ 上，成为一个 $\mathfrak{so}(n)$-值的[1-形式](@entry_id:270392)矩阵，其分量 $(\omega_i{}^j) = s^*\omega$ 由协变导数的定义决定：
$$
\nabla e_i = \sum_j \omega_i{}^j \otimes e_j
$$
由于联络与度规相容，矩阵 $(\omega_i{}^j)$ 必须是反对称的，即 $\omega_i{}^j + \omega_j{}^i = 0$。

相应地，[曲率算子](@entry_id:198006) $R$ 也有一个[矩阵表示](@entry_id:146025)，即**[曲率2-形式](@entry_id:187677)（curvature 2-form）** $\Omega$。它是一个 $\mathfrak{so}(n)$-值的[2-形式](@entry_id:188008)，由**[嘉当第二结构方程](@entry_id:196278)（Cartan's second structural equation）**给出：
$$
\Omega = d\omega + \frac{1}{2}[\omega, \omega]
$$
在分量形式下，即 $\Omega_i{}^j = d\omega_i{}^j + \sum_k \omega_i{}^k \wedge \omega_k{}^j$。这个方程优雅地将曲率的[代数结构](@entry_id:137052)（[李括号](@entry_id:636461)）和[微分](@entry_id:158718)结构（[外微分](@entry_id:161900)）结合在一起。

为了更好地理解这些形式化的定义，让我们看一个具体的例子。考虑一个3维定向[黎曼流形](@entry_id:261160)，其上存在一个全局正交[余标架场](@entry_id:183575) $\{\theta^1, \theta^2, \theta^3\}$ 满足 $d\theta^i = -c \varepsilon_{ijk} \theta^j \wedge \theta^k$，其中 $c>0$ 为常数。这是一个[常曲率空间](@entry_id:161841)的例子 [@problem_id:3038945]。通过无挠条件 $d\theta^i + \omega^i{}_j \wedge \theta^j = 0$ 和度规相容条件 $\omega^i{}_j + \omega^j{}_i = 0$，我们可以唯一确定[联络1-形式](@entry_id:275839)为：
$$
\omega^i{}_j = -c \varepsilon_{ijk} \theta^k
$$
然后，利用[嘉当第二结构方程](@entry_id:196278)，我们可以计算出[曲率2-形式](@entry_id:187677)：
$$
\Omega^i{}_j = d\omega^i{}_j + \omega^i{}_k \wedge \omega^k{}_j = c^2 \theta^i \wedge \theta^j
$$
这个结果表明，该[流形](@entry_id:153038)具有[常截面曲率](@entry_id:272200) $c^2$。

[曲率形式](@entry_id:199387)还满足一个至关重要的恒等式，即**[第二比安基恒等式](@entry_id:199705)（second Bianchi identity）**。利用**外[协变导数](@entry_id:152476)** $D$（定义为 $D\alpha^i_j = d\alpha^i_j + \omega^i_k \wedge \alpha^k_j - \alpha^i_k \wedge \omega^k_j$），该恒等式可以简洁地写成：
$$
D\Omega = 0
$$
这个恒等式是曲率[张量对称性](@entry_id:191651)的体现，也是下一节中陈-韦伊理论的基石。在上面的例子中，我们可以显式计算 $D\Omega^i_j = d\Omega^i_j + \omega^i_k \wedge \Omega^k_j - \Omega^i_k \wedge \omega^k_j$，并验证结果确实为零 [@problem_id:3038945]。

### 陈-韦伊同态：从几何到拓扑

我们已经看到，曲率是一个描述局部几何的量。然而，通过一个名为**陈-韦伊同态（Chern–Weil homomorphism）**的强大工具，我们可以从曲率中构造出完全不依赖于局部几何细节（如所选的联络）的全局拓扑不变量。

这个构造过程的关键代数成分是[李代数](@entry_id:137954) $\mathfrak{g}$ 上的**[不变多项式](@entry_id:266937)（invariant polynomial）** [@problem_id:3038948]。一个多项式 $P: \mathfrak{g} \to \mathbb{R}$（或 $\mathbb{C}$）如果对于[李群](@entry_id:137659) $G$ 的伴随作用是不变的，即对于所有 $g \in G$ 和 $X \in \mathfrak{g}$，都满足 $P(\mathrm{Ad}_g(X)) = P(gXg^{-1}) = P(X)$，则称其为[不变多项式](@entry_id:266937)。
对于[矩阵李代数](@entry_id:204591) $\mathfrak{gl}(n, \mathbb{C})$，最基本的[不变多项式](@entry_id:266937)是由[矩阵的迹和行列式](@entry_id:182536)给出的。更一般地，对于任意矩阵 $X \in \mathfrak{gl}(n, \mathbb{C})$，其特征多项式 $\det(tI - X)$ 的系数都是关于 $X$ 的[不变多项式](@entry_id:266937)。这些系数等价于 $X$ 的[特征值](@entry_id:154894)的[基本对称多项式](@entry_id:152224)。事实上，整个[不变多项式](@entry_id:266937)代数是由这些系数，或者等价地，由[幂和多项式](@entry_id:153700) $P_k(X) = \operatorname{tr}(X^k)$ ($k=1, \dots, n$) 生成的。

陈-韦伊构造如下：给定一个 $G$-[主丛上的联络](@entry_id:159386)，其[曲率2-形式](@entry_id:187677) $\Omega$ 是一个 $\mathfrak{g}$-值的2-形式。如果我们取一个 $k$ 次齐次[不变多项式](@entry_id:266937) $P$，我们可以将其应用于 $\Omega$，得到一个标量值的 $2k$-形式 $P(\Omega)$。例如，如果 $P(X) = \operatorname{tr}(X^2)$，则 $P(\Omega) = \operatorname{tr}(\Omega \wedge \Omega)$。

这个微分形式 $P(\Omega)$ 具有两个非凡的性质：

1.  **它是闭形式**：$d(P(\Omega)) = 0$。这个性质是[不变多项式](@entry_id:266937)的“不变性”和曲率的[第二比安基恒等式](@entry_id:199705) $D\Omega = 0$ 的直接推论。因此，$P(\Omega)$ 在[德拉姆上同调](@entry_id:158673)（de Rham cohomology）中定义了一个[上同调类](@entry_id:263961) $[P(\Omega)] \in H^{2k}_{\mathrm{dR}}(M)$。

2.  **其上同调类独立于联络的选择**：这是陈-韦伊理论最深刻的结果 [@problem_id:3038934]。如果我们选取丛上的两个不同联络 $\omega_0$ 和 $\omega_1$，它们对应的[曲率形式](@entry_id:199387)为 $\Omega_0$ 和 $\Omega_1$。尽管[微分形式](@entry_id:146747) $P(\Omega_0)$ 和 $P(\Omega_1)$ 本身可能不同，但它们的差是一个恰当形式。具体来说，可以证明存在一个 $(2k-1)$-形式 $\alpha$（称为**超越形式**或**陈-西蒙斯形式**），使得：
    $$
    P(\Omega_1) - P(\Omega_0) = d\alpha
    $$
    这意味着 $P(\Omega_0)$ 和 $P(\Omega_1)$ 定义了同一个[上同调类](@entry_id:263961)。

综上所述，陈-韦伊同态为我们提供了一个从李代数 $\mathfrak{g}$ 上的[不变多项式](@entry_id:266937)环到[流形](@entry_id:153038) $M$ 的[上同调环](@entry_id:160158)的映射。这个映射将几何对象（曲率）转化为了拓扑不变量（**[示性类](@entry_id:160596)**），这些[不变量](@entry_id:148850)只依赖于向量丛本身的拓扑结构。

### 构造示性类

现在，我们应用陈-韦伊理论来具体构造一些最重要的[示性类](@entry_id:160596)。

#### 陈类 (Chern Classes)

对于一个秩为 $r$ 的[复向量丛](@entry_id:276223) $E \to M$，我们可以为其配备一个酉联络，其[曲率2-形式](@entry_id:187677) $\Omega$ 是一个 $\mathfrak{u}(r)$-值的形式（即反对称厄米矩阵）。为了构造陈类，我们考虑在 $\mathfrak{gl}(r, \mathbb{C})$ 上的[不变多项式](@entry_id:266937) $\det(I + A)$。通过一个特定的代换，我们定义**总陈形式（total Chern form）**为 [@problem_id:303901]：
$$
c(\Omega) = \det\left(I + \frac{i}{2\pi}\Omega\right)
$$
这个表达式的定义非常精妙：
-   因子 $i$ 的作用是至关重要的。由于 $\Omega$ 是反对称[厄米矩阵](@entry_id:155147)值的，$\frac{i}{2\pi}\Omega$ 变成了一个厄米矩阵值的[2-形式](@entry_id:188008)。[厄米矩阵的特征值](@entry_id:202187)为实数，其特征多项式的系数也为实数。这保证了 $c(\Omega)$ 展开后的各项都是实值的微分形式。
-   因子 $\frac{1}{2\pi}$ 是一个[归一化常数](@entry_id:752675)。它确保了当陈类与拓扑学中通过胞腔分解等方式定义的整上同调类相比对时，它们的周期是整数。

将上述[行列式](@entry_id:142978)展开，我们得到一个形式和：
$$
c(\Omega) = 1 + c_1(\Omega) + c_2(\Omega) + \dots + c_r(\Omega)
$$
其中 $c_k(\Omega)$ 是一个 $2k$-形式，被称为第 $k$ 个**陈形式**。它们的上同调类 $[c_k(\Omega)]$ 就是第 $k$ 个**陈类** $c_k(E) \in H^{2k}_{\mathrm{dR}}(M)$。

#### [庞特里亚金类](@entry_id:161084) (Pontryagin Classes)

对于一个实向量丛 $E \to M$，我们不能直接使用上述构造。一个标准的方法是先将其**[复化](@entry_id:260775)（complexification）**，得到[复向量丛](@entry_id:276223) $E \otimes \mathbb{C}$。然后，我们借用复丛的陈类来定义实丛的**[庞特里亚金类](@entry_id:161084)（Pontryagin classes）** [@problem_id:303919]：
$$
p_k(E) := (-1)^k c_{2k}(E \otimes \mathbb{C}) \in H^{4k}_{\mathrm{dR}}(M)
$$
可以证明，$E \otimes \mathbb{C}$ 的奇数陈类总是为零，所以[庞特里亚金类](@entry_id:161084)只出现在 $4k$ 次的[上同调群](@entry_id:142450)中。与陈类一样，[庞特里亚金类](@entry_id:161084)是独立于联络选择的拓扑不变量。如果一个丛容许平坦联络（即曲率处处为零），那么它的所有[庞特里亚金类](@entry_id:161084)都为零。第一个庞特里亚金形式 $p_1(\Omega)$ 可以通过计算 $c_2(E \otimes \mathbb{C})$ 得到，其表达式为：
$$
p_1(\Omega) = -\frac{1}{8\pi^2} \operatorname{tr}(\Omega \wedge \Omega)
$$

#### [欧拉类](@entry_id:161259) (Euler Class)

对于一个**定向的**、偶数秩 $2m$ 的实向量丛 $E \to M$，我们可以定义另一个重要的[示性类](@entry_id:160596)——**[欧拉类](@entry_id:161259)（Euler class）**。此时，一个与度规相容的[联络的曲率](@entry_id:159154)形式 $\Omega$ 是一个 $\mathfrak{so}(2m)$-值的2-形式，即一个[反对称矩阵](@entry_id:155998)。对于反对称矩阵，有一个特殊的[不变多项式](@entry_id:266937)叫做**普法菲安（Pfaffian）**，记为 $\mathrm{Pf}$。它的平方等于[矩阵的行列式](@entry_id:148198)：$(\mathrm{Pf}(A))^2 = \det(A)$。

**[欧拉形式](@entry_id:637896)（Euler form）**通过普法菲安定义为 [@problem_id:303903]：
$$
e(\Omega) = \mathrm{Pf}\left(\frac{\Omega}{2\pi}\right)
$$
其上同调类 $[e(\Omega)]$ 就是**[欧拉类](@entry_id:161259)** $e(E) \in H^{2m}_{\mathrm{dR}}(M)$。[欧拉类](@entry_id:161259)具有以下关键性质：
-   它是一个拓扑不变量，其定义不依赖于联络的选择。
-   它依赖于丛的定向。如果反转定向，[欧拉类](@entry_id:161259)会变号：$e(E_{\text{rev}}) = -e(E)$。
-   **陈-[高斯-博内定理](@entry_id:160424)（Chern-Gauss-Bonnet Theorem）**：对于一个紧致定向的 $2m$ 维黎曼流形 $M$，其切丛 $TM$ 的[欧拉类](@entry_id:161259)在整个[流形上的积分](@entry_id:156150)等于该[流形的拓扑](@entry_id:267834)[欧拉示性数](@entry_id:152513) $\chi(M)$：
    $$
    \int_M e(TM) = \chi(M)
    $$
    这个定理是现代几何中最深刻和优美的结果之一，它将[流形](@entry_id:153038)的局部几何（由曲率编码）与纯粹的拓扑不变量（[欧拉示性数](@entry_id:152513)）联系起来。
-   [欧拉类](@entry_id:161259)是向量丛是否存在一个**处处非零[截面](@entry_id:154995)**的主要**障碍（obstruction）**。如果向量丛 $E$ 拥有一个处处非零的光滑[截面](@entry_id:154995)，那么它的[欧拉类](@entry_id:161259)必定为零：$e(E) = 0$。反之不一定成立，但这个性质使得[欧拉类](@entry_id:161259)在许多拓扑问题中扮演着核心角色。

总而言之，本章我们从联络的定义出发，通过曲率的概念，最终利用陈-韦伊同态这一桥梁，系统地构造了[微分几何](@entry_id:145818)中最重要的几种[示性类](@entry_id:160596)。这些[不变量](@entry_id:148850)是衡量向量丛“扭曲”程度的拓扑尺度，深刻地揭示了[局部几何与全局拓扑](@entry_id:636645)之间的内在联系。