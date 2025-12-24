## 引言
[余伴随轨道](@entry_id:1122577)是现代数学物理中的一个核心概念，它在辛几何、[李群表示](@entry_id:185475)论和几何力学等领域之间架起了一座至关重要的桥梁。对于任何具有[李群对称性](@entry_id:201825)的物理系统，从旋转的陀螺到基本粒子的内部自由度，其[余伴随轨道](@entry_id:1122577)都提供了一个内禀且统一的几何框架来描述其相空间和动力学。然而，这些抽象的数学结构如何与具体的物理现象和数学理论精确对应，是理解其深刻意义的关键所在。

本文旨在系统地揭示[余伴随轨道](@entry_id:1122577)及其内蕴的Kostant-Kirillov-Souriau (KKS) 辛形式的原理、应用与实践。我们将引导读者穿越这一理论的三个核心层面：
- 在“原理与机制”一章中，我们将从[李群](@entry_id:137659)与[李代数](@entry_id:137954)的基本作用出发，严谨地构建[余伴随轨道](@entry_id:1122577)的概念，并详细阐述其上典范的KKS[辛形式](@entry_id:165896)和[李-泊松结构](@entry_id:157559)。
- 随后的“应用与跨学科联系”一章将展示这一理论的强大威力，通过具体实例探讨其如何描述[刚体运动](@entry_id:144691)、流体涡旋动力学、可积系统以及粒子在[规范场](@entry_id:159627)中的行为，并揭示其与Borel-Weil定理及[几何量子化](@entry_id:159174)的深刻联系。
- 最后，“动手实践”部分将提供一系列计算练习，帮助读者将抽象理论应用于具体问题，从而加深对核心概念的理解。

通过这一结构化的学习路径，读者将全面掌握余伴随轨道理论，并理解其作为连接经典与量子、物理与数学的统一语言的独特地位。

## 原理与机制

本章旨在深入阐述余伴随轨道及其内蕴的辛几何结构的原理与机制。在前一章介绍背景之后，我们将从基本定义出发，系统地构建伴随作用与余伴随作用的数学框架，进而引出作为核心研究对象的[余伴随轨道](@entry_id:1122577)。随后，我们将详细定义并分析Kostant-Kirillov-Souriau (KKS) [辛形式](@entry_id:165896)，它是赋予这些轨道深刻几何与物理意义的关键。通过[李-泊松结构](@entry_id:157559)的视角，我们将揭示余伴随轨道作为[辛叶](@entry_id:158259)的本质，并探讨不变量（如[Casimir函数](@entry_id:166674)）如何刻画这些轨道的几何形态。最后，本章将展示这些抽象结构如何与李[群的[表](@entry_id:140711)示论](@entry_id:137998)——这一理论的根本动机——建立深刻联系，特别是在[紧李群](@entry_id:146703)和幂零[李群](@entry_id:137659)的情境下。

### 伴随作用与余伴随作用

李群 $G$ 的结构与其[李代数](@entry_id:137954) $\mathfrak{g}$ 的结构通过**伴随作用（Adjoint action）**紧密相连。对于群中的任意元素 $g \in G$，我们可以定义一个共轭映射 $C_g: G \to G$，其形式为 $C_g(h) = ghg^{-1}$。由于 $C_g(e) = e$（其中 $e$ 是 $G$ 的单位元），这个映射在单位元处的[微分](@entry_id:158422) $d(C_g)_e$ 是一个从切空间 $T_eG$ 到自身的[线性同构](@entry_id:270529)。通过将[李代数](@entry_id:137954) $\mathfrak{g}$ 等同于 $T_eG$，我们便定义了 $g$ 在 $\mathfrak{g}$ 上的伴随作用，记作 $\mathrm{Ad}_g$：
$$
\mathrm{Ad}_g = d(C_g)_e : \mathfrak{g} \to \mathfrak{g}
$$
这给出所谓的**伴随表示（Adjoint representation）**，即一个从李群 $G$ 到其李代数上的[自同构群](@entry_id:139672) $\mathrm{Aut}(\mathfrak{g})$ 的[群同态](@entry_id:140603) $\mathrm{Ad}: G \to \mathrm{Aut}(\mathfrak{g})$。

伴随表示在单位元处的[微分](@entry_id:158422)，则揭示了[李代数](@entry_id:137954)自身的[代数结构](@entry_id:137052)。这个[微分](@entry_id:158422)是一个从 $\mathfrak{g}$ 到其上的线性变换构成的代数 $\mathrm{End}(\mathfrak{g})$ 的[李代数同态](@entry_id:1127204)，记作 $\mathrm{ad}$。对于任意 $X, Y \in \mathfrak{g}$，其作用由[李括号](@entry_id:636461)给出：
$$
\mathrm{ad}_X(Y) = [X, Y]
$$
这表明，[李括号](@entry_id:636461)内蕴地编码了伴随作用的无穷小行为。

现在，我们转向[对偶空间](@entry_id:146945) $\mathfrak{g}^*$。它是 $\mathfrak{g}$ 上的所有[线性泛函](@entry_id:276136)构成的[向量空间](@entry_id:151108)。$\mathfrak{g}^*$ 和 $\mathfrak{g}$ 之间存在一个自然的**对偶配对（dual pairing）**，记作 $\langle \cdot, \cdot \rangle: \mathfrak{g}^* \times \mathfrak{g} \to \mathbb{R}$。基于这个配对，我们可以定义 $G$ 在 $\mathfrak{g}^*$ 上的**余伴随作用（Coadjoint action）** $\mathrm{Ad}^*$。其定义要求该作用与伴随作用在配对下是对偶的。为了使 $\mathrm{Ad}^*$ 成为一个左作用（即满足 $\mathrm{Ad}^*_{gh} = \mathrm{Ad}^*_g \mathrm{Ad}^*_h$），定义中必须包含一个[逆元](@entry_id:140790)素：
$$
\langle \mathrm{Ad}^*_g \mu, X \rangle = \langle \mu, \mathrm{Ad}_{g^{-1}} X \rangle
$$
对于所有的 $g \in G$, $\mu \in \mathfrak{g}^*$, 和 $X \in \mathfrak{g}$。

与伴随作用类似，余伴随作用也有其无穷小版本，记作 $\mathrm{ad}^*$。通过对关于 $g$ 的定义式（沿着[单参数子群](@entry_id:181957) $g(t) = \exp(tX)$）在 $t=0$ 处求导，我们可以得到其定义关系式：
$$
\langle \mathrm{ad}^*_X \mu, Y \rangle = -\langle \mu, [X, Y] \rangle
$$
这个负号的出现至关重要，它源于余伴随作用定义中的[逆元](@entry_id:140790) $g^{-1}$。这些关于伴随和余伴随作用的精确定义是理解后续所有内容的基础 。

### 几何舞台：余伴随轨道

一旦定义了余伴随作用，我们便可以在[对偶空间](@entry_id:146945) $\mathfrak{g}^*$ 中开辟出研究的主要几何对象——**余伴随轨道（Coadjoint orbit）**。对于 $\mathfrak{g}^*$ 中的任意一点 $\mu$，其对应的余伴随轨道 $\mathcal{O}_\mu$ 是 $\mu$ 在整个群 $G$ 的余伴随作用下所形成的轨迹：
$$
\mathcal{O}_\mu = \{ \mathrm{Ad}^*_g \mu \mid g \in G \} \subset \mathfrak{g}^*
$$
整个[对偶空间](@entry_id:146945) $\mathfrak{g}^*$ 因此被分解（或叶状化）为互不相交的[余伴随轨道](@entry_id:1122577)的并集。每个轨道都是一个[光滑流形](@entry_id:160799)。

一个轨道的局部几何形状由其切空间描述。在轨道上一点 $\mu \in \mathcal{O}_\mu$，其[切空间](@entry_id:199137) $T_\mu \mathcal{O}_\mu$ 由所有无穷小余伴随作用在该点产生的[向量张成](@entry_id:152883)：
$$
T_\mu \mathcal{O}_\mu = \{ \mathrm{ad}^*_X \mu \mid X \in \mathfrak{g} \}
$$
这个描述引出了**稳定子代数（stabilizer subalgebra）**的概念，即在无穷小意义下保持 $\mu$ 不变的那些李代数元素：
$$
\mathfrak{g}_\mu = \{ X \in \mathfrak{g} \mid \mathrm{ad}^*_X \mu = 0 \}
$$
从切空间的定义可以看出，从 $\mathfrak{g}$ 到 $T_\mu \mathcal{O}_\mu$ 的映射 $X \mapsto \mathrm{ad}^*_X \mu$ 的核恰好是 $\mathfrak{g}_\mu$。因此，我们有同构关系 $T_\mu \mathcal{O}_\mu \cong \mathfrak{g}/\mathfrak{g}_\mu$。

一个最简单而又具有启发性的例子是当李代数 $\mathfrak{g}$ 是**阿贝尔（Abelian）**的，即其上任意元素的李括号均为零：$[X,Y]=0$ 对所有 $X,Y \in \mathfrak{g}$ 成立。在这种情况下，无穷小伴随作用 $\mathrm{ad}_X$ 和无穷小余伴随作用 $\mathrm{ad}^*_X$ 都是零映射。因此，对于任意 $\mu \in \mathfrak{g}^*$，其轨道的[切空间](@entry_id:199137) $T_\mu \mathcal{O}_\mu = \{0\}$ 是零维的。这意味着每个[余伴随轨道](@entry_id:1122577)都退化为一个单点 $\mathcal{O}_\mu = \{ \mu \}$ 。这个平凡的例子预示了[李括号](@entry_id:636461)的非零性质是产生非平凡轨道几何的根本原因。

### 辛结构：Kostant-Kirillov-Souriau (KKS) 形式

余伴随轨道的非凡之处在于，它们并非仅仅是[光滑流形](@entry_id:160799)，而是天生就带有一个典范的**[辛结构](@entry_id:1132759)（symplectic structure）**。这个结构由一个[2-形式](@entry_id:188008)给出，称为 **Kostant-Kirillov-Souriau (KKS) 形式**，记作 $\omega$ 或 $\omega_\mu$。

在轨道 $\mathcal{O}_\mu$ 上的点 $\nu$ 处，KKS 形式 $\omega_\nu$ 作用于两个[切向量](@entry_id:265494)。如前所述，任意[切向量](@entry_id:265494)可以写成 $\mathrm{ad}^*_X \nu$ 的形式。KKS 形式的定义如下：
$$
\omega_\nu(\mathrm{ad}^*_X \nu, \mathrm{ad}^*_Y \nu) := \langle \nu, [X, Y] \rangle
$$
这个定义表面上依赖于产生[切向量](@entry_id:265494)的李代数元素 $X$ 和 $Y$ 的选取。然而，它是**良定义的（well-defined）**。假设另一个元素 $X'$ 产生了相同的[切向量](@entry_id:265494)，即 $\mathrm{ad}^*_{X'} \nu = \mathrm{ad}^*_X \nu$。这意味着 $\mathrm{ad}^*_{X'-X} \nu = 0$，所以 $X'-X$ 属于稳定子代数 $\mathfrak{g}_\nu$。根据 $\mathrm{ad}^*$ 的定义和 $\mathfrak{g}_\nu$ 的性质，我们有：
$$
\langle \nu, [X'-X, Y] \rangle = -\langle \mathrm{ad}^*_{X'-X} \nu, Y \rangle = -\langle 0, Y \rangle = 0
$$
这表明 $\langle \nu, [X', Y] \rangle = \langle \nu, [X, Y] \rangle$。因此，$\omega_\nu$ 的值仅依赖于[切向量](@entry_id:265494)本身，而与它们的代表元素 $X, Y$ 的选择无关 。

KKS 形式具有以下关键性质：
1.  **[双线性性](@entry_id:146819)**：显然。
2.  **[反对称性](@entry_id:261893)**：源于[李括号](@entry_id:636461)的[反对称性](@entry_id:261893)，$\omega_\nu(v_Y, v_X) = \langle \nu, [Y,X] \rangle = -\langle \nu, [X,Y] \rangle = -\omega_\nu(v_X, v_Y)$。
3.  **闭性**：$d\omega = 0$。这个性质的证明较为复杂，依赖于[李代数](@entry_id:137954)的Jacobi恒等式。
4.  **非退化性**：对于任意非零[切向量](@entry_id:265494) $v \in T_\nu \mathcal{O}_\nu$，都存在另一个切向量 $w$ 使得 $\omega_\nu(v, w) \neq 0$。

一个闭的、非退化的[2-形式](@entry_id:188008)就是一个**辛形式（symplectic form）**。因此，每个余伴随轨道 $(\mathcal{O}_\mu, \omega)$ 都是一个**[辛流形](@entry_id:161608)（symplectic manifold）**。这为我们提供了一个巨大的宝库，可以在其中应用哈密顿力学的工具。

为了更具体地理解KKS形式，我们考虑李代数 $\mathfrak{sl}(2, \mathbb{R})$ 的一个例子。这个代数由矩阵 $H=\begin{pmatrix}10\\0-1\end{pmatrix}$, $E=\begin{pmatrix}01\\00\end{pmatrix}$, $F=\begin{pmatrix}00\\10\end{pmatrix}$ 张成。我们通过非退化的伴随不变配对 $\langle X, Y \rangle = \mathrm{Tr}(XY)$ 将 $\mathfrak{sl}(2, \mathbb{R})$ 与其[对偶空间](@entry_id:146945)等同起来。在这种等同下，[余伴随轨道](@entry_id:1122577)与伴随轨道等同。考虑通过点 $X_t = tH$（其中 $t \in \mathbb{R} \setminus \{0\}$）的轨道。其在 $X_t$ 点的[切空间](@entry_id:199137)由形如 $[Y, X_t]$ 的[向量张成](@entry_id:152883)。我们选取一组基底：$v_E = [E, X_t] = -2tE$ 和 $v_F = [F, X_t] = 2tF$。KKS形式此时可以写作 $\omega_{X_t}([A, X_t], [B, X_t]) = \langle X_t, [A,B] \rangle = \mathrm{Tr}(X_t[A,B])$。
我们来计算 $\omega_{X_t}$ 在基底 $(v_E, v_F)$ 下的矩阵 $\Omega$：
$$
\Omega_{11} = \omega_{X_t}(v_E, v_E) = \mathrm{Tr}(X_t[E,E]) = \mathrm{Tr}(X_t \cdot 0) = 0
$$
$$
\Omega_{12} = \omega_{X_t}(v_E, v_F) = \mathrm{Tr}(X_t[E,F]) = \mathrm{Tr}(tH \cdot H) = t \cdot \mathrm{Tr}(H^2) = t \cdot 2 = 2t
$$
由于[反对称性](@entry_id:261893)，$\Omega_{21} = -2t$ 且 $\Omega_{22}=0$。所以，KKS形式的矩阵为：
$$
\Omega = \begin{pmatrix} 0  2t \\ -2t  0 \end{pmatrix}
$$
这个[矩阵的行列式](@entry_id:148198)是 $\det(\Omega) = 4t^2$。因为 $t \neq 0$，行列式非零，这明确地证明了KKS形式在该点是**非退化的** 。

### 泊松观点：[李-泊松结构](@entry_id:157559)

[余伴随轨道](@entry_id:1122577)和KKS形式的理论可以被优雅地置于一个更广阔的框架——[泊松几何](@entry_id:1129878)（Poisson geometry）——之中。整个[对偶空间](@entry_id:146945) $\mathfrak{g}^*$ 本身构成一个**[泊松流形](@entry_id:1129883)（Poisson manifold）**。

在[函数空间](@entry_id:143478) $C^\infty(\mathfrak{g}^*)$ 上可以定义一个**李-泊松括号（Lie-Poisson bracket）**。对于任意两个光滑函数 $F, H \in C^\infty(\mathfrak{g}^*)$，它们在点 $\mu \in \mathfrak{g}^*$ 的泊松括号定义为：
$$
\{F, H\}(\mu) = \langle \mu, [\nabla F(\mu), \nabla H(\mu)] \rangle
$$
这里的 $\nabla F(\mu)$ 是函数 $F$ 在点 $\mu$ 的**梯度**，它是一个李代数元素，通过关系 $dF_\mu(\nu) = \langle \nu, \nabla F(\mu) \rangle$ 对所有 $\nu \in \mathfrak{g}^*$ 定义。这个括号结构完全由李代数的[李括号](@entry_id:636461)决定。

[泊松流形](@entry_id:1129883)的一个核心特征是它可以被叶状化为一系列**[辛叶](@entry_id:158259)（symplectic leaves）**。对于[李-泊松流形](@entry_id:1127199) $(\mathfrak{g}^*, \{\cdot, \cdot\})$，其[辛叶](@entry_id:158259)恰好就是**[余伴随轨道](@entry_id:1122577)**。每个轨道上的[辛结构](@entry_id:1132759)，正是由泊松括号在该叶上诱导的[辛结构](@entry_id:1132759)，这与我们之前定义的KKS形式是等价的。

在这个框架下，我们可以定义一个函数的**哈密顿向量场（Hamiltonian vector field）** $X_H$，其定义为 $X_H(F) = \{F, H\}$。可以证明 $X_H(\mu) = -\mathrm{ad}^*_{\nabla H(\mu)}\mu$。所有这些哈密顿向量场在一点 $\mu$ 张成的空间恰好就是该点所在轨道的切空间 $T_\mu\mathcal{O}_\mu$。

一类特殊的函数是**Casimir函数**，它们是[泊松括号](@entry_id:151133)的中心元，即与所有函数 $H$ 的[泊松括号](@entry_id:151133)均为零：$\{C, H\} = 0$。这意味着[Casimir函数](@entry_id:166674)的[哈密顿向量场](@entry_id:158846)是[零向量](@entry_id:156189)场。因此，[Casimir函数](@entry_id:166674)在每个辛叶（即每个余伴随轨道）上都取常数值 。

回到阿贝尔代数的例子，由于李括号恒为零，李-泊松括号也恒为零：$\{F,H\}=0$。这意味着 $\mathfrak{g}^*$ 上的所有函数都是Casimir函数，所有哈密顿向量场都为零。[辛叶](@entry_id:158259)（余伴随轨道）的维度为零，即为单点。这再次印证了我们之前的几何观察 。

### 结构、不变量与等同

[余伴随轨道](@entry_id:1122577)与[李代数](@entry_id:137954) $\mathfrak{g}$ 上的**伴随轨道（Adjoint orbits）**（即元素在 $\mathrm{Ad}$ 作用下的轨迹）之间的关系，深刻地依赖于李代数的结构。

一个自然的问题是：我们能否将 $\mathfrak{g}$ 与其对偶 $\mathfrak{g}^*$ 等同起来，从而将余伴随轨道与伴随轨道等同起来？这需要一个从 $\mathfrak{g}$ 到 $\mathfrak{g}^*$ 的[线性同构](@entry_id:270529)。任何一个非退化的[双线性形式](@entry_id:746794) $b: \mathfrak{g} \times \mathfrak{g} \to \mathbb{R}$ 都能提供这样一个同构 $\flat: \mathfrak{g} \to \mathfrak{g}^*$（通过 $\langle \flat(X), Y \rangle = b(X, Y)$）。然而，为了使这个同构在几何上具有意义，我们要求它是 $G$-等变的（$G$-equivariant），即它能保持群作用的结构：$\mathrm{Ad}^*_g \circ \flat = \flat \circ \mathrm{Ad}_g$。通过计算可以证明，这个[等变性](@entry_id:636671)条件等价于[双线性形式](@entry_id:746794) $b$ 是**伴随不变的（Ad-invariant）**：
$$
b(\mathrm{Ad}_g X, \mathrm{Ad}_g Y) = b(X, Y), \quad \forall g \in G, X, Y \in \mathfrak{g}
$$
对于连通李群 $G$，这又等价于无穷小的不变性，即 **ad-[不变性](@entry_id:140168)**：$b([Z,X],Y) + b(X,[Z,Y]) = 0$ 。

对于**[半单李代数](@entry_id:190073)（semisimple Lie algebra）**，其**[基灵型](@entry_id:161046)（Killing form）** $K(X,Y) = \mathrm{Tr}(\mathrm{ad}_X \mathrm{ad}_Y)$ 就是一个非退化且伴随不变的[对称双线性形式](@entry_id:148281)。因此，对于[半单李代数](@entry_id:190073)，存在一个典范的 $G$-等变同构 $\mathfrak{g} \cong \mathfrak{g}^*$。这使得我们可以将余伴随轨道的研究转化为伴随轨道的研究。KKS形式也可以通过这个同构“拉回”到伴随轨道 $\mathcal{O}_x \subset \mathfrak{g}$ 上，其在点 $x$ 的表达式为：
$$
\omega_x([ \xi, x], [\eta, x]) = K(x, [\xi, \eta])
$$

在[半单李代数](@entry_id:190073)的情形下，[Casimir函数](@entry_id:166674)与[不变量理论](@entry_id:145135)紧密相关。**Chevalley定理**指出，对于一个秩为 $r$ 的复[半单李代数](@entry_id:190073)，其上的 $G$-[不变多项式](@entry_id:266937)环 $S(\mathfrak{g})^G$ 是一个由 $r$ 个代数独立的[齐次多项式](@entry_id:178156)自由生成的环。这 $r$ 个生成元，作为 $\mathfrak{g}^*$ 上的函数，恰好构成了基本[Casimir函数](@entry_id:166674)的集合 。这意味着，一个泛型（generic）余伴随轨道的几何形状由这 $r$ 个不变量的值唯一确定。这些Casimir函数的[微分](@entry_id:158422)在泛型点 $\mu$ 张成的空间，正是轨道切空间 $T_\mu\mathcal{O}_\mu$ 的[零化子](@entry_id:155446)，其维度为 $r$。因此，泛型轨道的维度是 $\dim \mathfrak{g} - r$ 。

然而，并非所有李代数都存在这样的典范等同。考虑三维**[海森堡代数](@entry_id:204103)（Heisenberg algebra）** $\mathfrak{h}_3$，其基底为 $\{X,Y,Z\}$，满足 $[X,Y]=Z$。可以证明，该代数上**不存在**任何ad-不变的非退化[对称双线性形式](@entry_id:148281)。任何ad-不变形式都必然是退化的，因为中心元 $Z$ 必定位于其核中。因此，对于[海森堡群](@entry_id:144785)，其伴随轨道和[余伴随轨道](@entry_id:1122577)之间没有典范的等同关系。这凸显了半单（或更一般的，可约）李代数的特殊性 。

### 与[表示论](@entry_id:137998)和量子化的联系

研究[余伴随轨道](@entry_id:1122577)及其辛结构的最终和最深刻的动机之一，来自于[李群](@entry_id:137659)的酉[表示论](@entry_id:137998)。**[几何量子化](@entry_id:159174)（Geometric quantization）**纲领旨在从一个经典物理系统的相空间（一个[辛流形](@entry_id:161608)）出发，构造出对应的量子[希尔伯特空间](@entry_id:261193)。[余伴随轨道](@entry_id:1122577)，作为典范的[辛流形](@entry_id:161608)，是这个纲领的理想试验场。

对于**紧致连通[李群](@entry_id:137659)**，一个余伴随轨道 $(\mathcal{O}_\mu, \omega)$ 是否“可量子化”（即是否存在一个所谓的[预量子化](@entry_id:159954)[线丛](@entry_id:1127303)），取决于一个**整性条件（integrality condition）**。这个条件，也称为Kostant整性条件，要求 $\omega/(2\pi)$ 的[德拉姆上同调](@entry_id:158673)类 $[\omega/(2\pi)]$ 是一个整[上同调类](@entry_id:263961)。这等价于要求 $\omega/(2\pi)$ 在任何2-维球面闭链上的积分都是整数。一个深刻的结果是，这个条件成立当且仅当轨道上的元素 $\mu$（通过与[嘉当子代数](@entry_id:191259)对偶的交集来选取）是一个**整权（integral weight）** 。这奇妙地将轨道的连续几何性质（辛[形式的积分](@entry_id:158607)）与[表示论](@entry_id:137998)的离散结构（[权格](@entry_id:195778)）联系在一起。

对于**幂零[李群](@entry_id:137659)（nilpotent Lie groups）**，这种联系变得更加完美和直接。**Kirillov的[轨道方法](@entry_id:161316)（Orbit Method）**指出，对于一个单连通的幂零李群，其不可约酉表示的[等价类](@entry_id:156032)与 $\mathfrak{g}^*$ 中的余伴随轨道之间存在一个**一一对应**关系。
$$
\widehat{G} \longleftrightarrow \mathfrak{g}^*/G
$$
在这种情况下，余伴随轨道拓扑上[同胚](@entry_id:146933)于某个[欧氏空间](@entry_id:138052) $\mathbb{R}^{2k}$。因此，它们的二阶[上同调群](@entry_id:142450)是平凡的，$H^2(\mathcal{O}_\mu, \mathbb{R}) = 0$。这意味着KKS形式总是**恰当的（exact）**，从而整性条件总是被**平凡地满足**。所以，对于幂零李群，每一个余伴随轨道都对应一个唯一的不可约酉表示。表示本身可以通过从与轨道上一点 $\mu$ 相关的极化子群上的一个特征标进行酉诱导来构造 。

综上所述，[余伴随轨道](@entry_id:1122577)远非抽象的几何构造。它们是自然的[哈密顿系统](@entry_id:143533)相空间，其几何形态由[李代数](@entry_id:137954)的[结构常数](@entry_id:157960)和不变量决定。最重要的是，它们是[李群对称性](@entry_id:201825)的基本载体，通过KKS辛形式与量子力学和[表示论](@entry_id:137998)建立了深刻而富有成果的联系。