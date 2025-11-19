## 引言
[狄拉克算子](@entry_id:161631)是现代[微分几何](@entry_id:145818)与数学物理中的核心概念，它深刻地统一了分析、代数与拓扑学。这一理论最初源于物理学中对相对论性电子的描述，但其数学上的普适性与强大威力，使其成为研究黎曼流形内在几何与全局拓扑的利器。然而，[狄拉克算子](@entry_id:161631)与[流形曲率](@entry_id:187680)之间的精确联系，即它如何“感知”空间的弯曲，构成了一个核心的知识缺口。填补这一缺口的关键，正是本文将要深入探讨的Lichnerowicz公式。

本文旨在系统地介绍[狄拉克算子](@entry_id:161631)理论及其应用。读者将从其代数基础出发，逐步掌握其在[几何流](@entry_id:195216)形上的构造与性质，并最终领略其在解决深刻几何与物理问题中的力量。
- 在“**原理与机制**”一章中，我们将从[Clifford代数](@entry_id:137625)和[旋量表示](@entry_id:141362)开始，构建[旋量丛](@entry_id:181093)的几何框架，并在此基础上定义[狄拉克算子](@entry_id:161631)。本章的重点是推导Lichnerowicz公式，并展示其如何直接推导出关于调和[旋量](@entry_id:158054)与标量曲率的基本定理。
- 接着，“**应用与[交叉](@entry_id:147634)学科联系**”一章将展示这一理论的广泛影响，包括它在[Atiyah-Singer指标定理](@entry_id:144128)中的核心作用，如何提供[正标量曲率](@entry_id:203664)度量存在的拓扑障碍，以及它在广义相对论的[正质量定理](@entry_id:158774)和前沿的高等[指标理论](@entry_id:270237)中的应用。
- 最后，“**动手实践**”部分提供了一系列练习，引导读者从具体计算中加深对旋量构造、[狄拉克算子](@entry_id:161631)形式以及[自旋结构](@entry_id:161662)拓扑障碍的理解。

通过这一结构化的学习路径，读者将全面理解[狄拉克算子](@entry_id:161631)为何是连接几何、拓扑与分析的关键桥梁。

## 原理与机制

本章旨在深入探讨[狄拉克算子](@entry_id:161631)（Dirac operator）的构造、基本性质及其在现代几何学中的核心作用。我们将从其代数基础出发，逐步构建[旋量丛](@entry_id:181093)（spinor bundle）的几何框架，并在此基础上定义[狄拉克算子](@entry_id:161631)。本章的中心是Lichnerowicz公式，这是一个深刻的恒等式，它将[狄拉克算子](@entry_id:161631)与[黎曼流形](@entry_id:261160)的曲率联系起来，从而成为连接分析、拓扑与几何的桥梁。我们将通过此公式揭示[流形](@entry_id:153038)上存在特定[旋量](@entry_id:158054)场（spinor field）的丰富几何蕴涵。

### 基础：从代数到几何

[狄拉克算子](@entry_id:161631)的构造深深植根于[Clifford代数](@entry_id:137625)的表示论。在我们将算子定义在[黎曼流形](@entry_id:261160)上之前，必须首先建立其代数和几何基础，包括[Clifford代数](@entry_id:137625)、旋量群（Spin group）、[旋量表示](@entry_id:141362)以及最终的[旋量丛](@entry_id:181093)。

#### [Clifford代数](@entry_id:137625)：一个代数序曲

我们从一个有限维实[内积空间](@entry_id:271570) $(V, g)$ 开始。该空间的**[Clifford代数](@entry_id:137625)** $\mathrm{Cl}(V, g)$ 是一个结合代数，其构造旨在“线性化”[内积](@entry_id:158127) $g$。形式上，它是[张量代数](@entry_id:161671) $T(V)$ 对[双边理想](@entry_id:272452) $I$ 的商代数，该理想由所有形如 $v \otimes v + g(v, v) \cdot 1$ 的元素生成，其中 $v \in V$。这个定义的核心关系在商代数中可以简洁地写为：
$v^2 = -g(v, v) \cdot 1 = -|v|^2 \cdot 1$

其中 $|v|^2 = g(v, v)$ 是由[内积](@entry_id:158127) $g$ 诱导的范数平方。这个关系是[Clifford代数](@entry_id:137625)的基石。特别地，对于任意两个向量 $v, w \in V$，我们可以通过[极化恒等式](@entry_id:271819)得到它们的[反交换关系](@entry_id:153815)：
$(v+w)^2 = -(v+w, v+w) = -(|v|^2 + |w|^2 + 2g(v,w))$
另一方面，在代数中展开 $(v+w)^2 = v^2 + vw + wv + w^2 = -|v|^2 -|w|^2 + vw + wv$。
比较两式可得：
$vw + wv = -2g(v, w)$

在旋量几何中，我们通常处理的是[Clifford代数](@entry_id:137625)在[复向量空间](@entry_id:264355)上的表示。一个关键的惯例选择是表示 $c: \mathrm{Cl}(V, g) \to \mathrm{End}(\Sigma)$ 满足关系 $c(v)^2 = -|v|^2 \mathrm{Id}$。这与上述代数定义完全一致 [@problem_id:2995185]。

[Clifford代数](@entry_id:137625)的结构取决于其维数 $n = \dim V$。特别是对于复[Clifford代数](@entry_id:137625) $C\ell_n(\mathbb{C}) = \mathrm{Cl}(\mathbb{R}^n) \otimes_{\mathbb{R}} \mathbb{C}$，其结构有如下分类 [@problem_id:2995173]：
- 如果 $n=2k$ 是偶数，则 $C\ell_n(\mathbb{C}) \cong M_{2^k}(\mathbb{C})$，即一个 $2^k \times 2^k$ 复矩阵代数。
- 如果 $n=2k+1$ 是奇数，则 $C\ell_n(\mathbb{C}) \cong M_{2^k}(\mathbb{C}) \oplus M_{2^k}(\mathbb{C})$，即两个[矩阵代数](@entry_id:153824)的[直和](@entry_id:156782)。

#### 旋量群与[旋量表示](@entry_id:141362)

**旋量群** $\mathrm{Spin}(n)$ 是[Clifford代数](@entry_id:137625) $C\ell_n$ 中可[逆元](@entry_id:140790)的一个[子群](@entry_id:146164)，它可以被看作是[特殊正交群](@entry_id:146418) $\mathrm{SO}(n)$ 的一个双重覆盖（double cover）。具体来说，存在一个 $2$-to-$1$ 的[群同态](@entry_id:140603) $\lambda: \mathrm{Spin}(n) \to \mathrm{SO}(n)$。这个性质使得旋量群成为处理与定向相关的几何问题时的基本工具。

**旋量空间** (space of spinors) $\Sigma_n$ 被定义为复[Clifford代数](@entry_id:137625) $C\ell_n(\mathbb{C})$ 的一个不可约模。根据上述 $C\ell_n(\mathbb{C})$ 的结构理论，我们可以推断出 $\Sigma_n$ 的维数 [@problem_id:2995173]：
- 当 $n=2k$ 或 $n=2k+1$ 时，一个不可约复模的维数总是 $\dim_{\mathbb{C}}(\Sigma_n) = 2^{\lfloor n/2 \rfloor}$。

这个维数远小于[Clifford代数](@entry_id:137625)本身的维数 $2^n$。将 $\mathrm{Spin}(n)$ 群在 $\Sigma_n$ 上的作用称为**[旋量表示](@entry_id:141362)**（spin representation）。它是一个无法分解为 $\mathrm{SO}(n)$ 表示的“真正”的[旋量表示](@entry_id:141362)。

当维数 $n=2k$ 为偶数时，[旋量](@entry_id:158054)空间有更精细的结构。此时，[Clifford代数](@entry_id:137625)中的**复体积元**（complex volume element），定义为 $\omega_{\mathbb{C}} = i^k e_1 e_2 \cdots e_n$ (对于一个标准正交基 $\{e_i\}$)，它与所有向量 $v \in V$ 反交换，并且其平方为 $\omega_{\mathbb{C}}^2 = \mathrm{Id}$。因此，$\omega_{\mathbb{C}}$ 在 $\Sigma_n$ 上的作用将 $\Sigma_n$ 分解为两个[特征值](@entry_id:154894)为 $+1$ 和 $-1$ 的特征[子空间](@entry_id:150286)：
$\Sigma_n = \Sigma_n^+ \oplus \Sigma_n^-$

这两个[子空间](@entry_id:150286)分别称为**正手性（positive chirality）**和**负手性（negative chirality）**[旋量](@entry_id:158054)空间，或**半[旋量](@entry_id:158054)空间**（half-spinor spaces）。它们的维数相等，均为 $2^{k-1}$ [@problem_id:2995173]。这个分解对于偶数维[流形](@entry_id:153038)上的[指标理论](@entry_id:270237)至关重要。

#### [旋量](@entry_id:158054)结构与[旋量丛](@entry_id:181093)

现在我们将这些代数概念应用到黎曼流形 $(M, g)$ 上。首先，我们需要能够在[流形](@entry_id:153038)上一致地定义[旋量](@entry_id:158054)。这要求[流形](@entry_id:153038)具有一个**[旋量](@entry_id:158054)结构**（spin structure）[@problem_id:2995187]。

一个定向黎曼 $n$-[流形](@entry_id:153038) $(M,g)$ 具有一个与之关联的**定向[标准正交标架](@entry_id:189702)丛** $P_{\mathrm{SO}}(M)$，这是一个以 $\mathrm{SO}(n)$ 为结构群的[主丛](@entry_id:160029)。一个[旋量](@entry_id:158054)结构被定义为该[主丛](@entry_id:160029)到 $\mathrm{Spin}(n)$-[主丛](@entry_id:160029)的一个提升（lift）。也就是说，一个旋量结构是一个 $\mathrm{Spin}(n)$-[主丛](@entry_id:160029) $P_{\mathrm{Spin}}(M)$，伴随着一个丛映射 $\pi: P_{\mathrm{Spin}}(M) \to P_{\mathrm{SO}}(M)$，该映射在纤维上限制为群的覆盖同态 $\lambda: \mathrm{Spin}(n) \to \mathrm{SO}(n)$。

这样一个提升存在的拓扑障碍由[流形](@entry_id:153038)的第二个**Stiefel-Whitney类** $w_2(TM) \in H^2(M; \mathbb{Z}_2)$ 给出。一个[旋量](@entry_id:158054)结构存在当且仅当 $w_2(TM) = 0$。当这个条件满足时，不同的旋量结构由 $H^1(M; \mathbb{Z}_2)$ 中的元素进行分类 [@problem_id:2995187]。

一旦[流形](@entry_id:153038)具备旋量结构 $P_{\mathrm{Spin}}(M)$，我们就可以通过**伴随丛**（associated bundle）构造**复[旋量丛](@entry_id:181093)** $\mathbb{S}$：
$\mathbb{S} := P_{\mathrm{Spin}}(M) \times_{\rho} \Sigma_n$

这里的 $\rho$ 是 $\mathrm{Spin}(n)$ 在[旋量](@entry_id:158054)空间 $\Sigma_n$ 上的[旋量表示](@entry_id:141362)。$\mathbb{S}$ 是一个[复向量丛](@entry_id:276223)，其秩（纤维维数）为 $2^{\lfloor n/2 \rfloor}$。它的每个纤维 $\mathbb{S}_x$ 在 $x \in M$ 点都是一个旋量空间，并且[切空间](@entry_id:199137) $T_xM$ 的[Clifford代数](@entry_id:137625) $C\ell(T_xM)$ 自然地作用于其上，使得 $\mathbb{S}$ 成为一个Clifford模丛 [@problem_id:2995173]。

对于许多[流形](@entry_id:153038)（例如，所有[复流形](@entry_id:159076)），即使 $w_2(TM) \neq 0$，我们仍然可以定义一个推广的旋量概念，即**spin$^c$结构**。这对应于将 $\mathrm{SO}(n)$ 提升到 $\mathrm{Spin}^c(n) = (\mathrm{Spin}(n) \times U(1))/\mathbb{Z}_2$ 群。一个spin$^c$结构存在当且仅当 $w_2(TM)$ 是某个整上同调类 $c_1(L) \in H^2(M; \mathbb{Z})$ 的模2约化。这里的 $L$ 是一个复线丛，称为spin$^c$结构的**[行列式线丛](@entry_id:201038)**（determinant line bundle）[@problem_id:2995175]。

### [狄拉克算子](@entry_id:161631)及其基本性质

在[旋量丛](@entry_id:181093)的几何框架之上，我们可以引入[微分](@entry_id:158718)结构，即联络和[狄拉克算子](@entry_id:161631)。

#### 旋量联络

黎曼度量 $g$ 唯一确定了一个[无挠的](@entry_id:161664)度量联络——**[Levi-Civita联络](@entry_id:161107)** $\nabla^{LC}$。这个联络可以被看作是[主丛](@entry_id:160029) $P_{\mathrm{SO}}(M)$ 上的一个[联络1-形式](@entry_id:275839) $\omega$。由于 $P_{\mathrm{Spin}}(M)$ 是 $P_{\mathrm{SO}}(M)$ 的覆盖，这个[联络形式](@entry_id:263247)可以唯一地提升到 $P_{\mathrm{Spin}}(M)$ 上的一个[联络形式](@entry_id:263247)。

这个提升的联络继而在伴随的[旋量丛](@entry_id:181093) $\mathbb{S}$ 上诱导了一个协变导数，我们称之为**[旋量](@entry_id:158054)联络**（spin connection），记为 $\nabla$ (或 $\nabla^{\mathbb{S}}$)。这个联络与[Levi-Civita联络](@entry_id:161107)以及Clifford乘法是相容的，体现在性质 $\nabla_X(c(Y)\psi) = c(\nabla^{LC}_X Y)\psi + c(Y)\nabla_X \psi$ 上。

在局部[标准正交标架](@entry_id:189702) $\{e_i\}$ 下，旋量联络可以具体地表示出来。设[Levi-Civita联络](@entry_id:161107)由[联络1-形式](@entry_id:275839) $\omega_{ij}$ 定义，即 $\nabla^{LC} e_i = \sum_j \omega_{ij} \otimes e_j$。那么，旋量联络作用在一个局部[旋量](@entry_id:158054)场 $\psi$ 上的表达式为 [@problem_id:2995205]：
$\nabla_X \psi = X(\psi) + \frac{1}{4} \sum_{i,j=1}^n \omega_{ij}(X) c(e_i)c(e_j) \psi$

这里的 $X(\psi)$ 是在[局部平凡化](@entry_id:267993)下对 $\psi$ 的分量求导，而第二项则是由[流形](@entry_id:153038)的几何（通过 $\omega_{ij}$）和[Clifford代数](@entry_id:137625)结构（通过 $c(e_i)c(e_j)$）决定的修正项。

#### [狄拉克算子](@entry_id:161631)的定义与性质

**[狄拉克算子](@entry_id:161631)** $D$ 是通过复合Clifford乘法与[旋量](@entry_id:158054)联络定义的。它是一个从旋量场到[旋量](@entry_id:158054)场的微分算子。其定义在坐标无关的形式下是 $D = c \circ \nabla$，在局部[标准正交标架](@entry_id:189702) $\{e_i\}$ 下的表达式为 [@problem_id:2995171]：
$D = \sum_{i=1}^n c(e_i) \nabla_{e_i}$

从定义可以看出，$D$ 是一个一阶微分算子。它是[椭圆算子](@entry_id:181616)，这是其具有良好[解析性](@entry_id:140716)质（如Fredholm性质）的根源。

一个至关重要的性质是，[狄拉克算子](@entry_id:161631)是**形式自伴**（formally self-adjoint）的。这意味着对于任何[紧支撑](@entry_id:276214)的旋量场 $\psi, \phi$，我们有 $\int_M \langle D\psi, \phi \rangle dV_g = \int_M \langle \psi, D\phi \rangle dV_g$。这个性质的证明依赖于两个关键要素：(1) [旋量](@entry_id:158054)联络 $\nabla$ 是度量联络，即它保持[旋量](@entry_id:158054)[内积](@entry_id:158127)；(2) Clifford乘法 $c(v)$ 对于实[切向量](@entry_id:265494) $v$ 是斜伴的（skew-adjoint） [@problem_id:2995185]。

在偶数维 $n=2k$ 的情况下，[旋量丛](@entry_id:181093)分裂为 $\mathbb{S} = \mathbb{S}^+ \oplus \mathbb{S}^-$。由于Clifford乘法将正负手性旋量相互转换 ($c(v): \mathbb{S}^\pm \to \mathbb{S}^\mp$)，[狄拉克算子](@entry_id:161631)也具有相同的性质，即 $D: \Gamma(\mathbb{S}^\pm) \to \Gamma(\mathbb{S}^\mp)$。因此，$D$ 可以被看作由两个算子组成：
$D^+: \Gamma(\mathbb{S}^+) \to \Gamma(\mathbb{S}^-)$ 和 $D^-: \Gamma(\mathbb{S}^-) \to \Gamma(\mathbb{S}^+)$

这两个算子互为形式伴随。

### Lichnerowicz公式：通向几何的桥梁

[狄拉克算子](@entry_id:161631)的威力很大程度上源于其平方 $D^2$ 与[流形曲率](@entry_id:187680)之间的一个驚人关系，即**Lichnerowicz公式**。

#### 公式及其推导

Lichnerowicz公式断言，[狄拉克算子](@entry_id:161631)的平方等于**[联络拉普拉斯算子](@entry_id:197120)**（connection Laplacian）$\nabla^*\nabla$ 加上一个与[标量曲率](@entry_id:157547)成正比的零阶项 [@problem_id:2995185]：
$D^2 = \nabla^*\nabla + \frac{1}{4}\mathrm{Scal}$

这里的 $\mathrm{Scal}$ 是[流形](@entry_id:153038)的标量曲率，而 $\nabla^*\nabla = - \sum_i (\nabla_{e_i}\nabla_{e_i} - \nabla_{\nabla_{e_i}e_i})$ 是作用在[旋量丛](@entry_id:181093)上的 Laplace-type 算子。

这个公式的推导过程本身就很有启发性。计算 $D^2 = (\sum_j c(e_j)\nabla_{e_j})(\sum_i c(e_i)\nabla_{e_i})$ 时，我们会得到二阶、一阶和零阶[微分](@entry_id:158718)项。
- 二阶项来自对角线部分 $i=j$，给出 $-\sum_i \nabla_{e_i}^2$，这构成了 $\nabla^*\nabla$ 的[主部](@entry_id:168896)。
- 零阶项主要来自非对角线部分 $i \neq j$，利用[协变导数的交换子](@entry_id:198075) $[ \nabla_{e_i}, \nabla_{e_j} ]$ 与曲率的关系，经过复杂的[Clifford代数](@entry_id:137625)运算后，最终化简为 $\frac{1}{4}\mathrm{Scal}$。
- 一阶[微分](@entry_id:158718)项的消失是推导中的关键一步。这些项的出现是因为[联络系数](@entry_id:157618) $\nabla_{e_i}e_j$ 不为零。然而，通过旋量联络与Clifford乘法的相容性以及[Clifford代数](@entry_id:137625)的[反交换关系](@entry_id:153815)，这些一阶项恰好重组为 $\nabla^*\nabla$ 中的低阶项，从而在 $D^2 - \nabla^*\nabla$ 的差中被完全抵消。这个抵消是一个逐点成立的代数奇迹，而非某种积分效应 [@problem_id:2995213]。

#### 应用一：从[Killing旋量](@entry_id:190525)到曲率

Lichnerowicz公式的第一个直接应用是揭示特殊[旋量](@entry_id:158054)场与[流形](@entry_id:153038)几何之间的刚性关系。一个**[Killing旋量](@entry_id:190525)** $\psi$ 是满足方程 $\nabla_X \psi = \mu c(X) \psi$ 的[旋量](@entry_id:158054)场，其中 $\mu$ 是一个实常数。

我们可以用两种方法计算 $D^2\psi$ [@problem_id:2995171]：
1.  **直接计算**: $D\psi = \sum_i c(e_i) \nabla_{e_i}\psi = \sum_i c(e_i) (\mu c(e_i) \psi) = \mu \sum_i c(e_i)^2 \psi = -n\mu\psi$。因此，$D^2\psi = D(-n\mu\psi) = -n\mu(D\psi) = (-n\mu)(-n\mu\psi) = n^2\mu^2\psi$。
2.  **使用Lichnerowicz公式**: 我们需要计算 $\nabla^*\nabla\psi$。在一个测地标架下，$\nabla^*\nabla\psi = -\sum_i \nabla_{e_i}\nabla_{e_i}\psi$。利用[Killing旋量](@entry_id:190525)方程和联络的相容性，可以算出 $\nabla^*\nabla\psi = n\mu^2\psi$。代入Lichnerowicz公式得到 $D^2\psi = (n\mu^2 + \frac{1}{4}\mathrm{Scal})\psi$。

比较这两个结果，我们得到 $n^2\mu^2 = n\mu^2 + \frac{1}{4}\mathrm{Scal}$。解出[标量曲率](@entry_id:157547)，我们发现它必须是一个常数：
$\mathrm{Scal} = 4n(n-1)\mu^2$

这个结果表明，任何存在非平凡实[Killing旋量](@entry_id:190525)的[黎曼流形](@entry_id:261160)必定是爱因斯坦[流形](@entry_id:153038)，其标量曲率由维数 $n$ 和Killing常数 $\mu$ 完全确定。

#### 应用二：消失定理与特殊[和乐](@entry_id:137051)

Lichnerowicz公式最著名的应用之一是通过所谓的**[Bochner技巧](@entry_id:196927)**来证明消失定理。考虑一个紧致旋量[流形](@entry_id:153038) $M$，并设 $\psi$ 是一个**和谐旋量**（harmonic spinor），即 $D\psi=0$。这意味着 $D^2\psi=0$。将Lichnerowicz公式两边与 $\psi$ 作[内积](@entry_id:158127)，然后在整个[流形](@entry_id:153038)上积分：
$\int_M \langle D^2\psi, \psi \rangle dV_g = \int_M \left( \langle \nabla^*\nabla\psi, \psi \rangle + \frac{1}{4}\mathrm{Scal}|\psi|^2 \right) dV_g = 0$

利用分部积分，$\int_M \langle \nabla^*\nabla\psi, \psi \rangle dV_g = \int_M |\nabla\psi|^2 dV_g$。于是我们得到一个积分恒等式：
$\int_M \left( |\nabla\psi|^2 + \frac{1}{4}\mathrm{Scal}|\psi|^2 \right) dV_g = 0$

这个简单的恒等式有着深刻的几何后果：
- **Lichnerowicz消失定理**: 如果[流形](@entry_id:153038)的标量曲率处处严格为正（$\mathrm{Scal} > 0$），那么上述积分中的两个被积项都是非负的。积分为零意味着被积函数必须恒为零。特别地，$\mathrm{Scal}|\psi|^2=0$，因为 $\mathrm{Scal}>0$，这强制要求 $|\psi|^2=0$，即 $\psi=0$。结论是：一个标量曲率为正的紧致旋量[流形](@entry_id:153038)上不存在非平凡的和谐旋量 [@problem_id:2995197]。

- **[平行旋量](@entry_id:189679)与特殊和乐**: 如果标量曲率是非负的（$\mathrm{Scal} \ge 0$），并且存在一个非平凡的和谐[旋量](@entry_id:158054) $\psi$，那么为了使积分为零，被积函数必须恒为零。这意味着 $|\nabla\psi|^2 = 0$ 并且 $\mathrm{Scal}|\psi|^2 = 0$。前者说明 $\psi$ 必须是**[平行旋量](@entry_id:189679)**（parallel spinor），即 $\nabla\psi=0$。后者则说明[流形](@entry_id:153038)的[标量曲率](@entry_id:157547)必须恒为零（$\mathrm{Scal} \equiv 0$）[@problem_id:2995188]。

一个[流形](@entry_id:153038)上存在非平凡[平行旋量](@entry_id:189679)是一个极强的条件。它意味着[流形](@entry_id:153038)的黎曼**[和乐群](@entry_id:191471)**（holonomy group）$\mathrm{Hol}(g)$ 在[旋量表示](@entry_id:141362)下有一个不动向量，因此 $\mathrm{Hol}(g)$ 必须是 $\mathrm{SO}(n)$ 的一个[真子群](@entry_id:141915)。根据Berger对不可约黎曼流形[和乐群](@entry_id:191471)的分类，满足此条件的仅有几类特殊的几何结构，它们都对应于[Ricci平坦流形](@entry_id:636329)（因此 $\mathrm{Scal}=0$ 也被满足）：
- $n=2m$: $\mathrm{Hol}(g) \subseteq \mathrm{SU}(m)$ (Calabi-Yau流形)
- $n=4m$: $\mathrm{Hol}(g) \subseteq \mathrm{Sp}(m)$ ([超凯勒流形](@entry_id:159760))
- $n=7$: $\mathrm{Hol}(g) \subseteq G_2$
- $n=8$: $\mathrm{Hol}(g) \subseteq \mathrm{Spin}(7)$

因此，一个[标量曲率](@entry_id:157547)非负的紧致不可约[旋量](@entry_id:158054)[流形](@entry_id:153038)，如果存在和谐旋量，那么它必定是[Ricci平坦](@entry_id:159097)的，并且具有上述一种[特殊几何](@entry_id:194564)结构 [@problem_id:2995188]。

### 全局后果：[狄拉克算子](@entry_id:161631)的指标

除了产生局部几何约束外，[狄拉克算子](@entry_id:161631)在[流形](@entry_id:153038)的全局拓扑中也扮演着核心角色，这集中体现在[Atiyah-Singer指标定理](@entry_id:144128)中。

#### 解析指标

在一个紧致、偶数维 $n=2k$ 的[旋量](@entry_id:158054)[流形](@entry_id:153038)上，我们有手性分解 $\mathbb{S} = \mathbb{S}^+ \oplus \mathbb{S}^-$，以及相应的算子 $D^+: \Gamma(\mathbb{S}^+) \to \Gamma(\mathbb{S}^-)$。[狄拉克算子](@entry_id:161631)的**解析指标**（analytic index）定义为：
$\mathrm{ind}(D) = \dim \ker D^+ - \dim \ker D^-$

这里 $\ker D^+$ 是由正手性和谐旋量构成的空间，而 $\ker D^-$ 是由负手性和谐旋量构成的空间。由于 $(D^+)^* = D^-$，这个定义恰好是算子 $D^+$ 的Fredholm指标。这个指标可以等价地看作是整个和谐旋量空间 $\ker D = \ker D^+ \oplus \ker D^-$ 的**超维数**（superdimension）[@problem_id:2995197]。

#### [Atiyah-Singer指标定理](@entry_id:144128)

**[Atiyah-Singer指标定理](@entry_id:144128)**是20世纪数学的里程碑之一。对于[旋量](@entry_id:158054)[狄拉克算子](@entry_id:161631)，它断言解析指标等于一个纯粹由[流形](@entry_id:153038)拓扑和几何定义的量，称为**拓扑指标**（topological index）。具体来说，它等于[流形](@entry_id:153038)的**Â-genus**：
$\mathrm{ind}(D) = \int_M \hat{A}(TM)$

这里的 $\hat{A}(TM)$ 是一个由[流形曲率](@entry_id:187680)张量构造的[特征形式](@entry_id:198300)，称为Â-form。这个定理的惊人之处在于，它将一个由[微分方程](@entry_id:264184)解的个数（一个分析量）决定的整数，与一个由[流形曲率](@entry_id:187680)积分（一个拓扑量）得到的数联系起来 [@problem_id:2995189]。

该定理的一个优雅证明是基于**热[核方法](@entry_id:276706)**（heat kernel method）。其关键步骤如下：
1.  **McKean-Singer公式**: 解析指标可以表示为热算子 $e^{-tD^2}$ 的[超迹](@entry_id:183947)数（supertrace），对任意 $t>0$ 成立：$\mathrm{ind}(D) = \mathrm{Str}(e^{-tD^2}) = \mathrm{Tr}(e^{-tD^2}|_{\mathbb{S}^+}) - \mathrm{Tr}(e^{-tD^2}|_{\mathbb{S}^-})$。
2.  **独立性**: 指标是一个与形变无关的整数，因此 $\mathrm{Str}(e^{-tD^2})$ 实际上与 $t$ 无关。
3.  **小时间[渐近展开](@entry_id:173196)**: 我们可以通过取极限 $t \to 0^+$ 来计算这个指标。当 $t \to 0^+$ 时，热核有一个局部[渐近展开](@entry_id:173196)。
4.  **奇迹般的抵消**: Lichnerowicz公式和[Clifford代数](@entry_id:137625)的[代数结构](@entry_id:137052)导致在计算[超迹](@entry_id:183947)数的局部展开时发生大规模的抵消。最终，当 $t \to 0^+$ 时，热核的[超迹](@entry_id:183947)[数密度](@entry_id:268986)逐点收敛于Â-form。

积分后即得到[指标定理](@entry_id:637636)。

#### 指标与曲率

[指标定理](@entry_id:637636)为Lichnerowicz消失定理提供了拓扑层面的诠释。我们已经知道，如果紧致[旋量](@entry_id:158054)[流形](@entry_id:153038) $M$ 的标量曲率 $\mathrm{Scal}>0$，那么 $\ker D = \{0\}$，这意味着 $\ker D^+=\{0\}$ 和 $\ker D^-=\{0\}$。因此，解析指标必须为零：$\mathrm{ind}(D) = 0 - 0 = 0$ [@problem_id:2995197]。

根据[Atiyah-Singer指标定理](@entry_id:144128)，这也意味着拓扑指标必须为零：
$\int_M \hat{A}(TM) = 0$

如果一个[流形](@entry_id:153038)（例如，[复射影空间](@entry_id:268402) $\mathbb{CP}^{2k}$）的Â-genus已知不为零，那么[指标定理](@entry_id:637636)就构成了一个强大的拓扑障碍：这样的[流形](@entry_id:153038)不可能容纳任何具有处处为[正标量曲率](@entry_id:203664)的[黎曼度量](@entry_id:754359)。这是[黎曼几何](@entry_id:160508)中利用[旋量](@entry_id:158054)和[狄拉克算子](@entry_id:161631)解决核心问题的典范。