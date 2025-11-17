## 引言
[黎曼几何](@entry_id:160508)为我们提供了在[光滑流形](@entry_id:160799)上测量长度和角度的工具，而复分析则研究[全纯函数](@entry_id:158563)和复结构。一个自然而深刻的问题是：我们如何将这两种思想融合在一起？也就是说，如何在一个[流形](@entry_id:153038)上定义一种既能[度量几何](@entry_id:185748)性质，又与[复数运算](@entry_id:195031)“和谐共处”的度量？标准的[黎曼度量](@entry_id:754359)本身并不能保证这一点，这便引出了本文的核心主题——[埃尔米特度量](@entry_id:202337)。

本文旨在系统地介绍[埃尔米特度量](@entry_id:202337)及其关联的[基本2-形式](@entry_id:183276)，它们是连接[黎曼几何](@entry_id:160508)、[复几何](@entry_id:159080)乃至辛拓扑的关键桥梁。通过学习本文，您将能够：
*   在“原理与机制”一章中，掌握[殆复结构](@entry_id:159849)、[埃尔米特度量](@entry_id:202337)和[基本2-形式](@entry_id:183276)的定义，并理解将[埃尔米特度量](@entry_id:202337)提升为凯勒度量的核心条件。
*   在“应用与跨学科联系”一章中，探索这些结构如何在[复射影空间](@entry_id:268402)等重要范例中得到应用，并了解它们如何与陈类、[卡拉比-丘流形](@entry_id:159253)以及[弦理论](@entry_id:145688)等前沿概念联系起来。
*   在“动手实践”部分，通过具体计算来巩固您对这些抽象概念的理解。

现在，让我们从最基本的构造开始，深入探讨这些强大几何工具的原理与机制。

## 原理与机制

在上一章中，我们介绍了在光滑流形上研究几何所需的基本工具。现在，我们将注意力转向一类具有丰富结构的特殊[流形](@entry_id:153038)，即那些允许我们以一种与度量性质相容的方式定义“[复结构](@entry_id:269128)”的[流形](@entry_id:153038)。本章将系统地阐述[埃尔米特度量](@entry_id:202337)（Hermitian metrics）及其关联的[基本2-形式](@entry_id:183276)（fundamental 2-forms）的原理与机制，它们是[复几何](@entry_id:159080)（complex geometry）与黎曼几何（Riemannian geometry）交汇处的基石。

### 从实到复：[殆复结构](@entry_id:159849)

我们从一个实[光滑流形](@entry_id:160799) $M$ 开始。为了在这样的实[流形](@entry_id:153038)上引入复数的概念，我们需要的不仅仅是在每个点的切空间上定义乘以 $i = \sqrt{-1}$ 的运算。我们需要一个全局光滑的结构。

一个**[殆复结构](@entry_id:159849)（almost complex structure）**是[流形](@entry_id:153038) $M$ 上的一个光滑的 $(1,1)$ 型张量场 $J$，它可以被看作是[切丛](@entry_id:161294) $TM$ 上的一个光滑丛自同态 $J: TM \to TM$，并且在每一点 $p \in M$ 的切空间 $T_pM$ 上，它作为一个线性算子满足：
$$
J_p^2 = -\mathrm{id}_{T_pM}
$$
其中 $\mathrm{id}_{T_pM}$ 是 $T_pM$ 上的[恒等变换](@entry_id:264671)。这个简单的代数条件具有深刻的几何后果。考虑任意一个切空间 $T_pM$，它是一个实[向量空间](@entry_id:151108)。如果其上存在一个[线性算子](@entry_id:149003) $J_p$ 满足 $J_p^2 = -\mathrm{id}$，那么 $J_p$ 的[特征值](@entry_id:154894)必须是 $\pm i$。由于 $J_p$ 是一个实线性算子，非实数的[特征值](@entry_id:154894)必须成共轭对出现。这意味着 $T_pM$ 的维数必须是偶数。因此，一个带有[殆复结构](@entry_id:159849)的[流形](@entry_id:153038) $M$ 的实维数必须是偶数，我们通常记为 $\dim_{\mathbb{R}} M = 2n$ [@problem_id:3049635]。一个装配了[殆复结构](@entry_id:159849) $J$ 的[流形](@entry_id:153038) $(M,J)$ 被称为**殆复流形（almost complex manifold）**。

### 与度量的兼容性：[埃尔米特度量](@entry_id:202337)

[殆复结构](@entry_id:159849)为我们提供了一种代数上的复数操作，但它本身并未与[流形](@entry_id:153038)的度量性质（如长度和角度）联系起来。为了融合这两种结构，我们引入了兼容性的概念。

给定一个殆[复流形](@entry_id:159076) $(M,J)$ 和其上的一个[黎曼度量](@entry_id:754359) $g$（即在每个切空间上定义了一个正定[对称双线性形式](@entry_id:148281)），如果它们满足如下的**[兼容性条件](@entry_id:201103)（compatibility condition）**：
$$
g(JX, JY) = g(X, Y)
$$
对于所有[切向量](@entry_id:265494)场 $X, Y$，我们就称 $g$ 是一个与 $J$ **兼容的（compatible）**[黎曼度量](@entry_id:754359)，或简称为一个**[埃尔米特度量](@entry_id:202337)（Hermitian metric）**。这个条件意味着，从度量的角度看，$J$ 在每个[切空间](@entry_id:199137)上都是一个保距变换（isometry）[@problem_id:3049656] [@problem_id:3049635]。

这个[兼容性条件](@entry_id:201103)引出了一些非常有用的代数性质。首先，$J$ 相对于度量 $g$ 是**斜伴随的（skew-adjoint）**，即：
$$
g(JX, Y) = -g(X, JY)
$$
这个性质可以通过[兼容性条件](@entry_id:201103)直接推导得出：
$$
g(JX, Y) = g(J(JX), J(Y)) = g(J^2X, JY) = g(-X, JY) = -g(X, JY)
$$
这个关系是后续许多计算的关键 [@problem_id:3049656] [@problem_id:3049623]。

此外，[兼容性条件](@entry_id:201103) $g(JX, JY) = g(X, Y)$ 等价于一个看起来更弱的条件：$g(JX, X) = 0$ 对所有切向量场 $X$ 成立。这个等价性的证明是一个很好的练习。从 $g(JX,JY) = g(X,Y)$ 出发，利用斜伴随性质可得 $g(JX,X) = -g(X,JX)$，再利用 $g$ 的对称性 $g(X,JX)=g(JX,X)$，我们得到 $g(JX,X)=-g(JX,X)$，因此 $g(JX,X)=0$。反过来，若 $g(JU,U)=0$ 对所有 $U$ 成立，通过[极化恒等式](@entry_id:271819)（polarization identity），令 $U=X+Y$，即可推导出 $g(JX,Y) = -g(JY,X)$，进而推得 $g(JX,JY) = g(X,Y)$ [@problem_id:3049656]。

一个装备了[殆复结构](@entry_id:159849) $J$ 和与之兼容的[埃尔米特度量](@entry_id:202337) $g$ 的三元组 $(M, J, g)$ 被称为一个**殆埃尔米特[流形](@entry_id:153038)（almost Hermitian manifold）**。

### [基本2-形式](@entry_id:183276)

在殆埃尔米特[流形](@entry_id:153038)上，我们可以利用 $g$ 和 $J$ 构造一个新的几何对象，它编码了这两种结构之间的相互作用。这个对象被称为**[基本2-形式](@entry_id:183276)（fundamental 2-form）**（有时也称作 Kähler 形式），定义为：
$$
\omega(X, Y) = g(JX, Y)
$$
为了证明 $\omega$ 确实是一个[2-形式](@entry_id:188008)，我们需要验证它是反对称的（skew-symmetric）。利用度量 $g$ 的对称性和 $J$ 的斜伴随性质，我们可以进行如下计算 [@problem_id:3049623]：
$$
\omega(Y, X) = g(JY, X) = g(X, JY) = -g(JX, Y) = -\omega(X, Y)
$$
这证实了 $\omega(Y,X) = -\omega(X,Y)$，因此 $\omega$ 是一个反对称的 $(0,2)$ 型张量，即一个[2-形式](@entry_id:188008)。由于 $g$ 是实值度量，$J$ 是实线性算子，$\omega$ 在实向量场上的取值也是实数，所以它是一个**实[2-形式](@entry_id:188008)**。值得强调的是，$\omega$ 的定义及其[2-形式](@entry_id:188008)的性质仅依赖于殆埃尔米特结构，而与 $J$ 是否“可积”（我们将在后面讨论）无关。

### 复数视角：复坐标与类型分解

为了更深入地理解[殆复结构](@entry_id:159849)和基本形式，我们需要引入[复化](@entry_id:260775)的切丛。将每个[切空间](@entry_id:199137) $T_pM$ [复化](@entry_id:260775)，我们得到复[切丛](@entry_id:161294) $T_{\mathbb{C}}M = TM \otimes_{\mathbb{R}} \mathbb{C}$。[殆复结构](@entry_id:159849) $J$ 可以通过复线性扩张作用在 $T_{\mathbb{C}}M$ 上。由于 $J^2 = -\mathrm{id}$，它在[复化](@entry_id:260775)空间上的[特征值](@entry_id:154894)为 $\pm i$。这导致了 $T_{\mathbb{C}}M$ 的一个基本分解 [@problem_id:3049620]：
$$
T_{\mathbb{C}}M = T^{1,0}M \oplus T^{0,1}M
$$
其中 $T^{1,0}M = \{Z \in T_{\mathbb{C}}M \mid JZ = iZ\}$ 是对应于[特征值](@entry_id:154894) $i$ 的**全纯切丛（holomorphic tangent bundle）**，而 $T^{0,1}M = \{Z \in T_{\mathbb{C}}M \mid JZ = -iZ\}$ 是对应于[特征值](@entry_id:154894) $-i$ 的**反全纯切丛（anti-holomorphic tangent bundle）**。

这个分解进一步诱导了复值微分形式的分解。复[余切丛](@entry_id:185138) $T_{\mathbb{C}}^*M$ 也分解为 $T^{*(1,0)}M \oplus T^{*(0,1)}M$。任何一个复 $k$-形式都可以唯一地分解为**类型为 $(p,q)$ 的形式**之和，其中 $p+q=k$。一个 $(p,q)$-形式在作用于 $p$ 个 $(1,0)$-型向量和 $q$ 个 $(0,1)$-型向量时可能非零，而在其他组合下为零。

[基本2-形式](@entry_id:183276) $\omega$ 在这个分解下具有非常特殊的性质：它是一个**类型为 $(1,1)$ 的形式**。这意味着 $\omega$ 在两个同类型的向量（即都属于 $T^{1,0}M$ 或都属于 $T^{0,1}M$）上取值为零。我们可以通过将 $g$ 和 $\omega$ 复双线性地扩张到 $T_{\mathbb{C}}M$ 来证明这一点。对于任意 $Z, W \in T^{1,0}M$，我们有 $JZ=iZ$ 和 $JW=iW$。利用 $g$ 的兼容性：
$$
g(Z, W) = g(JZ, JW) = g(iZ, iW) = i^2 g(Z, W) = -g(Z, W)
$$
这迫使 $g(Z,W) = 0$。因此，$\omega(Z, W) = g(JZ, W) = g(iZ, W) = i g(Z, W) = 0$。类似的论证表明，当 $Z, W \in T^{0,1}M$ 时，$\omega(Z,W)$ 也为零。所以，$\omega$ 只在混合类型的向量对上（一个来自 $T^{1,0}M$，一个来自 $T^{0,1}M$）才可能非零，这正是 $(1,1)$-形式的定义 [@problem_id:3049620] [@problem_id:3049621]。

当[流形](@entry_id:153038)是真正的复流形时（见后文），我们可以引入局部全纯坐标 $\{z^k = x^k + i y^k\}$。在这种坐标下，全纯切向量由 $\{\frac{\partial}{\partial z^k}\}$ 张成。[埃尔米特度量](@entry_id:202337)可以由一个正定[埃尔米特矩阵](@entry_id:155147) $(g_{i\bar{j}})$ 描述。度量张量本身可以写作 $\sum_{i,j} g_{i\bar{j}} dz^i \otimes d\bar{z}^j$ [@problem_id:3049655]。

在这种[局部坐标](@entry_id:181200)下，[基本2-形式](@entry_id:183276)有一个非常简洁的表达式：
$$
\omega = \frac{i}{2} \sum_{i,j=1}^n g_{i\bar{j}} dz^i \wedge d\bar{z}^j
$$
利用 $g_{j\bar{i}} = \overline{g_{i\bar{j}}}$ 和 $dz^i \wedge d\bar{z}^j = - d\bar{z}^j \wedge dz^i$ 的性质，可以验证 $\bar{\omega} = \omega$，说明它确实是一个[实形式](@entry_id:193866) [@problem_id:3049655]。

**范例：$\mathbb{C}^n$ 上的标准[埃尔米特度量](@entry_id:202337)**
为了让这些抽象概念更具体，我们考察复欧几里得空间 $\mathbb{C}^n$。其上的标准[埃尔米特度量](@entry_id:202337)由 $h = \sum_{k=1}^n dz^k \otimes d\bar{z}^k$ 给出。我们将 $z^k = x^k + i y^k$ 代入，得到 $dz^k = dx^k + i dy^k$。于是，
$$
h = \sum_{k=1}^n (dx^k + i dy^k) \otimes (dx^k - i dy^k) = \sum_{k=1}^n \left( (dx^k \otimes dx^k + dy^k \otimes dy^k) + i(dy^k \otimes dx^k - dx^k \otimes dy^k) \right)
$$
相关的黎曼度量 $g = \mathrm{Re}(h)$ 就是 $\mathbb{R}^{2n}$ 上的标准[欧几里得度量](@entry_id:147197) $g = \sum_{k=1}^n (dx^k \otimes dx^k + dy^k \otimes dy^k)$。标准[复结构](@entry_id:269128) $J$ 的作用是 $J(\frac{\partial}{\partial x^k}) = \frac{\partial}{\partial y^k}$ 和 $J(\frac{\partial}{\partial y^k}) = -\frac{\partial}{\partial x^k}$。根据定义 $\omega(u,v) = g(Ju,v)$，我们计算 $\omega$ 在[基向量](@entry_id:199546)上的值，例如：
$$
\omega\left(\frac{\partial}{\partial x^j}, \frac{\partial}{\partial y^k}\right) = g\left(J\frac{\partial}{\partial x^j}, \frac{\partial}{\partial y^k}\right) = g\left(\frac{\partial}{\partial y^j}, \frac{\partial}{\partial y^k}\right) = \delta_{jk}
$$
而 $\omega(\frac{\partial}{\partial x^j}, \frac{\partial}{\partial x^k}) = 0$ 和 $\omega(\frac{\partial}{\partial y^j}, \frac{\partial}{\partial y^k}) = 0$。将这些分量组合起来，我们得到[基本2-形式](@entry_id:183276)的表达式 [@problem_id:3049643]：
$$
\omega = \sum_{k=1}^n dx^k \wedge dy^k
$$
这是一个非常简单而重要的形式，它构成了[辛几何](@entry_id:160783)（symplectic geometry）的基础。

### 连接实与复的世界

我们已经看到，一个殆埃尔米特结构 $(g,J)$ 既可以从实[流形](@entry_id:153038) $TM$ 的角度（一个黎曼度量和一个满足[兼容性条件](@entry_id:201103)的算子）来描述，也可以从[复化](@entry_id:260775)切丛 $T^{1,0}M$ 的角度来描述。事实上，这两种描述是完全等价的。在每个切空间上，这两种结构可以相互确定，这种对应关系是纯代数的，不依赖于 $J$ 的可积性 [@problem_id:3049621]。

1.  **从 $(g,J)$ 到 $h$**：给定一个殆埃尔米特结构 $(g,J)$，我们可以在全纯切丛 $T^{1,0}M$ 上定义一个**[埃尔米特内积](@entry_id:141742)（Hermitian inner product）** $h$。一个[埃尔米特内积](@entry_id:141742) $h$ 是一个正定的[半双线性形式](@entry_id:154766)（sesquilinear form），即它在一个变量上是复线性的，在另一个变量上是[共轭线性](@entry_id:268590)的。标准的构造方式是 [@problem_id:3049637]：
    $$
    h(Z, W) = g(Z, \bar{W}) - i\omega(Z, \bar{W}) \quad \text{对于 } Z, W \in T^{1,0}M
    $$
    其中 $\bar{W}$ 是 $W$ 的[复共轭](@entry_id:174690)。将 $\omega$ 的定义代入并利用 $Z \in T^{1,0}M$ 意味着 $JZ=iZ$ 的事实，上式可以简化为：
    $$
    h(Z,W) = 2g(Z, \bar{W})
    $$
    可以验证，这样定义的 $h$ 满足[埃尔米特内积](@entry_id:141742)的所有性质：它在第一个变量上是线性的，在第二个变量上是[共轭线性](@entry_id:268590)的，并且是正定的。

2.  **从 $h$ 到 $(g,J)$**：反过来，给定 $T^{1,0}M$ 上的一个[埃尔米特内积](@entry_id:141742) $h$，我们可以唯一地恢复出实切丛 $TM$ 上的黎曼度量 $g$ 和[基本2-形式](@entry_id:183276) $\omega$。对于任意实[切向量](@entry_id:265494) $X \in TM$，我们首先将其分解为 $(1,0)$ 部分和 $(0,1)$ 部分，$X = X^{1,0} + X^{0,1}$，其中 $X^{1,0} = \frac{1}{2}(X - iJX)$。则 $g$ 和 $\omega$ 可以通过 $h$ 表示为 [@problem_id:3049621]：
    $$
    g(X, Y) = 2 \cdot \mathrm{Re}\left(h(X^{1,0}, Y^{1,0})\right)
    $$
    $$
    \omega(X, Y) = -2 \cdot \mathrm{Im}\left(h(X^{1,0}, Y^{1,0})\right)
    $$
    这些公式优美地揭示了 $g$ 和 $\omega$ 的本质：它们分别是[埃尔米特内积](@entry_id:141742) $h$ 在实[切丛](@entry_id:161294)上的“实部”和“虚部”的体现。[黎曼度量](@entry_id:754359) $g$ 捕捉了对称的部分，而基本形式 $\omega$ 捕捉了反对称的部分。

### 可积性与[凯勒条件](@entry_id:637291)

到目前为止，我们讨论的[殆复结构](@entry_id:159849) $J$ 在代数上模拟了[复数乘法](@entry_id:167843)，但它不一定来自一个真正的[复结构](@entry_id:269128)。一个[殆复结构](@entry_id:159849)被称为**可积的（integrable）**，如果[流形](@entry_id:153038) $M$ 局部上看起来像 $\mathbb{C}^n$，即存在局部全纯[坐标系](@entry_id:156346)，使得[坐标变换](@entry_id:172727)函数是全纯的。一个深刻的定理（Newlander-Nirenberg 定理）指出，$J$ 是可积的当且仅当其**尼让黑斯张量（Nijenhuis tensor）** $N_J$ 恒为零 [@problem_id:3049635]。一个带有可积[殆复结构](@entry_id:159849)的[流形](@entry_id:153038)就是一个**[复流形](@entry_id:159076)（complex manifold）**。

在复流形上，我们可以问一个更深刻的问题：[埃尔米特度量](@entry_id:202337) $g$ 在何种程度上与复结构“和谐共处”？这种最完美的和谐状态由**[凯勒条件](@entry_id:637291)（Kähler condition）**所描述。

一个复流形上的[埃尔米特度量](@entry_id:202337)被称为**凯勒度量（Kähler metric）**，如果其[基本2-形式](@entry_id:183276) $\omega$ 是**闭的（closed）**，即其[外微分](@entry_id:161900)等于零：
$$
d\omega = 0
$$
这个看似简单的条件 $d\omega = 0$ 具有极其深远的影响，它将[流形](@entry_id:153038)的黎曼几何（通过度量 $g$）、[复几何](@entry_id:159080)（通过结构 $J$）和辛拓扑（通过形式 $\omega$）完美地结合在一起。

[凯勒条件](@entry_id:637291)有一个等价的几何刻画，这正是它如此重要的原因。在任意殆埃尔米特[流形](@entry_id:153038)上，$\omega$ 的[外微分](@entry_id:161900)与 $J$ 的[协变导数](@entry_id:152476)（相对于 $g$ 的 Levi-Civita 联络 $\nabla$）之间存在如下关系：
$$
d\omega(X, Y, Z) = g((\nabla_X J)Y, Z) + g((\nabla_Y J)Z, X) + g((\nabla_Z J)X, Y)
$$
其中 $(\nabla_X J)Y = \nabla_X(JY) - J(\nabla_X Y)$ 度量了 $J$ 在沿 $X$ 方向的平行移动下的变化。从这个公式可以立刻看出，如果 $J$ 是**平行的（parallel）**，即 $\nabla J = 0$，那么 $d\omega$ 必定为零。可以证明，$\nabla J = 0$ 也保证了 $J$ 是可积的（即 $N_J=0$）[@problem_id:3049642]。

[复几何](@entry_id:159080)中的一个核心定理指出，对于一个[复流形](@entry_id:159076)（$N_J=0$）上的[埃尔米特度量](@entry_id:202337)，上述过程可以反过来：如果 $d\omega=0$，那么必定有 $\nabla J = 0$。因此，在[复流形](@entry_id:159076)上，以下三个条件是等价的 [@problem_id:3049642]：
1.  度量是**凯勒度量**（$d\omega = 0$）。
2.  [复结构](@entry_id:269128) $J$ 相对于 Levi-Civita 联络是**平行的**（$\nabla J = 0$）。

需要注意的是，这些等价性在前提不满足时会失效。例如，在一个非可积的殆[复流形](@entry_id:159076)上，$d\omega=0$ 并不足以保证 $\nabla J = 0$（这种[流形](@entry_id:153038)被称为**殆凯勒流形 (almost-Kähler manifold)**）。同样，在一个[复流形](@entry_id:159076)上，并非所有[埃尔米特度量](@entry_id:202337)都是凯勒度量；我们可以构造出 $d\omega \neq 0$ 的[埃尔米特度量](@entry_id:202337) [@problem_id:3049635]。

最后，[凯勒条件](@entry_id:637291)还统一了两种重要的联络。在一般的埃尔米特[流形](@entry_id:153038)上，存在两个自然的联络：**Levi-Civita 联络** $\nabla^{\mathrm{LC}}$，它无挠（torsion-free）且与度量 $g$ 兼容，但通常不保持复结构 $J$；以及**陈联络（Chern connection）** $\nabla^{\mathrm{C}}$，它与 $g$ 和 $J$ 都兼容，但通常有挠率 [@problem_id:3049645]。[凯勒条件](@entry_id:637291) $d\omega=0$（或等价地 $\nabla J = 0$）正是这两个联络重合的充要条件。在凯勒流形上，存在一个唯一的联络，它同时满足无挠、与度量兼容、与复结构兼容这三个理想的性质。这正是[凯勒几何](@entry_id:160314)具有如此优美和刚性结构的原因。