## 引言
在探索了范畴、对象和态射这些[范畴论](@entry_id:137315)的基本构件之后，我们自然会问：这些静态的结构如何相互作用？不同的数学“宇宙”之间是否存在着联系的桥梁？这正是[函子](@entry_id:150427)与自然变换所要解答的核心问题。它们是[范畴论](@entry_id:137315)的动态引擎，不仅赋予了这门语言以生命力，更揭示了代数、拓扑和几何等看似无关领域之间深刻而普适的结构性关联。若不理解函子与自然变换，我们对[范畴论](@entry_id:137315)的认识将停留在孤立的定义层面，错失其作为现代数学统一框架的真正威力。

本文旨在系统地引导读者掌握这两个核心概念。在“原则与机理”一章中，我们将深入其形式化定义，理解[函子](@entry_id:150427)如何作为保结构映射在范畴间穿梭，以及自然变换如何成为函子间的“态射”。接着，在“应用与跨学科联系”一章，我们将看到这些抽象概念如何在[行列式](@entry_id:142978)、同调论和[群作用](@entry_id:268812)等具体数学构造中大放异彩。最后，通过“动手实践”部分，读者将有机会亲手验证和应用所学知识，巩固理解。让我们一同开启这段探索数学结构之美的旅程。

## 原则与机理

在前一章中，我们介绍了[范畴论](@entry_id:137315)的基本语言——对象、态射和范畴。现在，我们将深入探讨[范畴论](@entry_id:137315)的核心动力机制：[函子](@entry_id:150427)与自然变换。[函子](@entry_id:150427)是范畴之间的保结构映射，而自然变换则是函子之间的映射。这些概念不仅为现代数学的许多分支提供了统一的语言，而且本身就是强大的工具，能够揭示不同数学结构之间深刻而意想不到的联系。

### 函子：范畴间的保结构映射

如果说范畴是对单个数学宇宙的建模，那么[函子](@entry_id:150427)就是连接这些宇宙的桥梁。函子在范畴间的穿梭，严格地保持着源范畴的内在结构——即态射的复合关系。

#### [函子](@entry_id:150427)的形式化定义

一个（协变）**[函子](@entry_id:150427)** (functor) $F$ 从范畴 $\mathbf{C}$ 到范畴 $\mathbf{D}$，记作 $F: \mathbf{C} \to \mathbf{D}$，是一个映射，它包含两个部分：

1.  **对对象的作用**：它将 $\mathbf{C}$ 中的每一个对象 $X$ 映射到 $\mathbf{D}$ 中的一个对象 $F(X)$。
2.  **对态射的作用**：它将 $\mathbf{C}$ 中的每一个态射 $f: X \to Y$ 映射到 $\mathbf{D}$ 中的一个态射 $F(f): F(X) \to F(Y)$。

这个映射必须满足以下两个公理，以确保其“保持结构”的特性：

*   **保持单位态射**：对于 $\mathbf{C}$ 中的任意对象 $X$，其单位态射为 $id_X: X \to X$。函子 $F$ 必须将其映射为 $F(X)$ 上的单位态射，即 $F(id_X) = id_{F(X)}$。
*   **保持复合**：对于 $\mathbf{C}$ 中任意两个可复合的态射 $f: X \to Y$ 和 $g: Y \to Z$，它们的复合为 $g \circ f: X \to Z$。函子 $F$ 必须将这个复合态射映射为对应映射态射的复合，即 $F(g \circ f) = F(g) \circ F(f)$。

最简单也最基础的[函子](@entry_id:150427)是**恒等[函子](@entry_id:150427)** (identity functor)。对于任何范畴 $\mathbf{C}$，我们可以定义一个从 $\mathbf{C}$ 到其自身的函子 $Id_{\mathbf{C}}: \mathbf{C} \to \mathbf{C}$。这个函子将每个对象和每个态射都映射到其自身。也就是说，$Id_{\mathbf{C}}(X) = X$ 对所有对象 $X$ 成立，且 $Id_{\mathbf{C}}(f) = f$ 对所有态射 $f$ 成立。验证它是否满足[函子](@entry_id:150427)公理是直截了当的：
- 保持单位态射：$Id_{\mathbf{C}}(id_X) = id_X = id_{Id_{\mathbf{C}}(X)}$。
- 保持复合：$Id_{\mathbf{C}}(g \circ f) = g \circ f = Id_{\mathbf{C}}(g) \circ Id_{\mathbf{C}}(f)$。
因此，对于任何范畴，[恒等映射](@entry_id:634191)总是一个函子 [@problem_id:1797666]。

#### 基本[函子](@entry_id:150427)举隅

函子的概念遍及数学的各个角落。以下是一些基本而重要的[函子](@entry_id:150427)类型。

**常[函子](@entry_id:150427) (Constant Functors)**
给定任意两个范畴 $\mathbf{C}$ 和 $\mathbf{D}$，以及 $\mathbf{D}$ 中的一个特定对象 $D_0$，我们可以定义一个**常函子** $C_{D_0}: \mathbf{C} \to \mathbf{D}$。该[函子](@entry_id:150427)将 $\mathbf{C}$ 中的*所有*对象都映射到 $D_0$，并将 $\mathbf{C}$ 中的*所有*态射都映射到 $D_0$ 上的单位态射 $id_{D_0}$。不难验证，这种映射满足函子公理。例如，对于态射 $f: X \to Y$ 和 $g: Y \to Z$，我们有 $C_{D_0}(g \circ f) = id_{D_0}$，而 $C_{D_0}(g) \circ C_{D_0}(f) = id_{D_0} \circ id_{D_0} = id_{D_0}$，因此复合得以保持 [@problem_id:1797644]。

**[遗忘函子](@entry_id:152889) (Forgetful Functors)**
许多函子的作用是“遗忘”其源范畴中的部分或全部[代数结构](@entry_id:137052)。例如，考虑从**群范畴** $\mathbf{Grp}$ 到**集合范畴** $\mathbf{Set}$ 的**[遗忘函子](@entry_id:152889)** $U: \mathbf{Grp} \to \mathbf{Set}$。这个函子将一个群 $(G, *)$ 映射到其底层的集合 $G$，并将一个[群同态](@entry_id:140603) $\phi: G \to H$ 映射到其作为集合间的函数 $\phi$。它“遗忘”了群的运算结构。类似地，存在一个从**拓扑空间范畴** $\mathbf{Top}$ 到 $\mathbf{Set}$ 的[遗忘函子](@entry_id:152889)，它将一个拓扑空间 $(X, \tau)$ 映射到底层集合 $X$，并“遗忘”其拓扑结构 $\tau$ [@problem_id:1797624]。

#### 函子的性质

函子的定义虽然简单，但蕴含了深刻的性质。它们不仅自身可以复合，还能可靠地传递源范畴的结构信息。

**函子的复合 (Composition of Functors)**
[函子](@entry_id:150427)可以像函数一样进行复合。如果 $F: \mathbf{C} \to \mathbf{D}$ 和 $G: \mathbf{D} \to \mathbf{E}$ 是两个[函子](@entry_id:150427)，那么它们的复合 $G \circ F: \mathbf{C} \to \mathbf{E}$ 也是一个函子。其定义是显而易见的：对任意对象 $X \in \mathbf{C}$，$(G \circ F)(X) = G(F(X))$；对任意态射 $f \in \mathbf{C}$，$(G \circ F)(f) = G(F(f))$。复合函子 $G \circ F$ 保持单位态射和复合，这是因为 $F$ 和 $G$ 各自都保持它们。例如，对于 $f: A \to B$ 和 $g: B \to C$：
$$(G \circ F)(g \circ f) = G(F(g \circ f)) = G(F(g) \circ F(f)) = G(F(g)) \circ G(F(f)) = ((G \circ F)(g)) \circ ((G \circ F)(f))$$
这个性质表明，范畴本身（作为对象）和[函子](@entry_id:150427)（作为态射）似乎也构成了一个巨大的“范畴”，即**范畴的范畴** $\mathbf{Cat}$ [@problem_id:1797665]。

**同构的保持 (Preservation of Isomorphisms)**
[函子](@entry_id:150427)的一个关键性质是它们保持同构关系。在范畴 $\mathbf{C}$ 中，一个态射 $f: A \to B$ 是一个**同构** (isomorphism)，如果存在一个态射 $g: B \to A$ 使得 $g \circ f = id_A$ 且 $f \circ g = id_B$。如果 $F: \mathbf{C} \to \mathbf{D}$ 是一个函子，那么它会将 $\mathbf{C}$ 中的同构映射为 $\mathbf{D}$ 中的同构。也就是说，如果 $f$ 是一个同构，那么 $F(f)$ 也必然是一个同构。
证明如下：设 $f$ 的逆为 $g$。将函子 $F$ 应用于等式 $g \circ f = id_A$ 和 $f \circ g = id_B$，我们得到：
$F(g \circ f) = F(g) \circ F(f) = F(id_A) = id_{F(A)}$
$F(f \circ g) = F(f) \circ F(g) = F(id_B) = id_{F(B)}$
这表明 $F(g)$ 正是 $F(f)$ 的逆。因此，$F(f)$ 是一个同构。例如，[遗忘函子](@entry_id:152889) $U: \mathbf{Grp} \to \mathbf{Set}$ 将[群同构](@entry_id:147371)映射为集合间的双射（即 $\mathbf{Set}$ 中的同构）[@problem_id:1797621]。

**忠实性与满性 (Faithfulness and Fullness)**
为了更精细地刻画[函子](@entry_id:150427)如何反映源范畴和目标范畴之间的关系，我们引入**忠实**和**满**这两个概念。对于范畴 $\mathbf{C}$ 中的任意两个对象 $X$ 和 $Y$，它们之间的所有态射构成一个集合，称为 **Hom-集**，记作 $\mathrm{Hom}_{\mathbf{C}}(X, Y)$。一个函子 $F: \mathbf{C} \to \mathbf{D}$ 会为每一对对象 $(X, Y)$ 诱导一个从 Hom-集到 Hom-集的函数：
$$F_{X,Y}: \mathrm{Hom}_{\mathbf{C}}(X, Y) \to \mathrm{Hom}_{\mathbf{D}}(F(X), F(Y))$$
- 如果对于 $\mathbf{C}$ 中所有的 $X, Y$，这个函数 $F_{X,Y}$ 都是**单射** (injective)，那么我们称[函子](@entry_id:150427) $F$ 是**忠实的** (faithful)。忠实的函子不会混淆不同的态射。
- 如果对于 $\mathbf{C}$ 中所有的 $X, Y$，这个函数 $F_{X,Y}$ 都是**满射** (surjective)，那么我们称[函子](@entry_id:150427) $F$ 是**满的** (full)。

让我们通过[遗忘函子](@entry_id:152889)来理解这些概念：
- [遗忘函子](@entry_id:152889) $U: \mathbf{Top} \to \mathbf{Set}$ 是忠实的，但不是满的。它是忠实的，因为如果两个[连续函数](@entry_id:137361) $f, g: (X, \tau_X) \to (Y, \tau_Y)$ 作为集合间的函数是相同的（即 $f(x)=g(x)$ 对所有 $x \in X$ 成立），那么它们作为[连续函数](@entry_id:137361)也必然是相同的。但它不是满的。考虑一个至少有两个点的集合 $S$，并赋予它两种拓扑：非[离散拓扑](@entry_id:152622) $\tau_{\text{ind}} = \{\emptyset, S\}$ 和离散拓扑 $\tau_{\text{disc}} = \mathcal{P}(S)$（$S$的幂集）。在集合范畴中，[恒等函数](@entry_id:152136) $id_S: S \to S$ 是一个态射。然而，这个函数作为从 $(S, \tau_{\text{ind}})$ 到 $(S, \tau_{\text{disc}})$ 的映射通常不是连续的，因为它不满足开集的原像也是开集的要求。因此，$\mathrm{Hom}_{\mathbf{Set}}(S, S)$ 中的 $id_S$ 在 $U$ 的作用下没有[原像](@entry_id:150899)，这表明 $U$ 不是满的 [@problem_id:1797624]。

- 考虑从**阿贝尔群范畴** $\mathbf{Ab}$ 到**群范畴** $\mathbf{Grp}$ 的**包含函子** (inclusion functor) $I: \mathbf{Ab} \to \mathbf{Grp}$。这个函子是满的（同时也是忠实的）。对于任意两个[阿贝尔群](@entry_id:150284) $A$ 和 $B$，$\mathrm{Hom}_{\mathbf{Grp}}(A, B)$ 中的任何一个[群同态](@entry_id:140603) $f: A \to B$，其[定义域和陪域](@entry_id:159300)都是阿贝尔群，因此它自动成为 $\mathrm{Hom}_{\mathbf{Ab}}(A, B)$ 中的一个态射。这意味着 $I_{A,B}$ 是一个[双射](@entry_id:138092)。一个既忠实又满的[函子](@entry_id:150427)被称为**完全忠实** (fully faithful) 的，它表明源范畴可以被看作是目标范畴的一个“全子范畴” [@problem_id:1797653]。

### 自然变换：[函子](@entry_id:150427)间的映射

函子建立了范畴间的联系，而自然变换则描述了这些联系本身的关系。它是“函子之间的态射”。

#### 自然性的概念

假设我们有两个从范畴 $\mathbf{C}$ 映至范畴 $\mathbf{D}$ 的[函子](@entry_id:150427)，$F$ 和 $G$。我们如何比较这两个函子？一种想法是为 $\mathbf{C}$ 中的每个对象 $X$ 提供一个从 $F(X)$ 到 $G(X)$ 的态射 $\eta_X: F(X) \to G(X)$。然而，仅仅一族这样的态射是不够的，我们还需要它们以一种“自然”或“协调”的方式与 $\mathbf{C}$ 中的态射相互作用。

这个协调性的要求被一个称为**自然性方块** (naturality square) 的[交换图](@entry_id:747516)所捕获。一个从 $F$ 到 $G$ 的**自然变换** (natural transformation) $\eta: F \Rightarrow G$ 是 $\mathbf{D}$ 中一族由 $\mathbf{C}$ 的对象索引的态射 $\eta = \{\eta_X: F(X) \to G(X)\}_{X \in \mathrm{Obj}(\mathbf{C})}$，使得对于 $\mathbf{C}$ 中的任意态射 $f: X \to Y$，下面的图是**交换的** (commutes)：
$$
\begin{CD}
F(X) @>{\eta_X}>> G(X) \\
@V{F(f)}VV @VV{G(f)}V \\
F(Y) @>>{\eta_Y}> G(Y)
\end{CD}
$$
图的交换性意味着沿着两条路径从左上角到右下角的复合态射是相等的，即 $G(f) \circ \eta_X = \eta_Y \circ F(f)$。这个等式被称为**自然性条件** (naturality condition)。

#### 验证自然性：关键示例

自然变换的概念初看起来可能相当抽象，但通过具体的例子可以很好地理解其内涵。

**对角映射**
考虑群范畴 $\mathbf{Grp}$。令 $Id: \mathbf{Grp} \to \mathbf{Grp}$ 为恒等函子，$Id(G)=G$。令 $F: \mathbf{Grp} \to \mathbf{Grp}$ 为将一个群 $G$ 映射到其直积 $G \times G$ 的函子，即 $F(G) = G \times G$。对于一个[群同态](@entry_id:140603) $f: G \to H$，$F(f)$ 的定义为 $F(f)(g_1, g_2) = (f(g_1), f(g_2))$。
我们想考察从 $Id$ 到 $F$ 的自然变换。一个候选者是**对角映射** (diagonal map) $\Delta$，其分量为 $\Delta_G: G \to G \times G$，定义为 $\Delta_G(g) = (g, g)$。
要验证 $\Delta$ 是一个自然变换，我们需要检查两个条件 [@problem_id:1797626]：
1.  **分量是态射**：对于每个群 $G$，$\Delta_G$ 必须是一个[群同态](@entry_id:140603)。这是成立的，因为 $\Delta_G(ab) = (ab, ab) = (a,a)(b,b) = \Delta_G(a)\Delta_G(b)$。
2.  **自然性条件**：对于任意[群同态](@entry_id:140603) $f: G \to H$，自然性方块必须交换。我们来验证 $F(f) \circ \Delta_G = \Delta_H \circ f$。对于任意 $g \in G$：
    - 左侧：$(F(f) \circ \Delta_G)(g) = F(f)(g,g) = (f(g), f(g))$。
    - 右侧：$(\Delta_H \circ f)(g) = \Delta_H(f(g)) = (f(g), f(g))$。
    两侧相等，故自然性条件满足。因此，对角映射族确实构成一个自然变换。

有趣的是，并非所有看起来相似的映射族都能构成自然变换。例如，考虑映射族 $\eta_G(g) = (g, g^{-1})$。它在第一步就失败了：对于一个非阿贝尔群 $G$，$\eta_G$ 不是一个[群同态](@entry_id:140603)，因为 $\eta_G(ab)=(ab, (ab)^{-1})=(ab, b^{-1}a^{-1})$，而 $\eta_G(a)\eta_G(b)=(ab, a^{-1}b^{-1})$，通常 $b^{-1}a^{-1} \neq a^{-1}b^{-1}$。

**二重对偶[求值映射](@entry_id:149774)**
在 $R$-模的范畴 $\mathbf{Mod}_R$ 中（$R$ 是一个[交换环](@entry_id:148261)），有一个极为重要的自然变换例子。令 $F$ 为恒等[函子](@entry_id:150427)，$F(M)=M$，而 $G$ 为**二重对偶函子** (double-dual functor)，$G(M) = M^{**} = \mathrm{Hom}_R(\mathrm{Hom}_R(M,R), R)$。
对于每个 $R$-模 $M$，存在一个典范的**[求值映射](@entry_id:149774)** (evaluation map) $\phi_M: M \to M^{**}$，其定义为：对于任意 $m \in M$ 和 $\psi \in M^*$（$M^*$ 是 $M$ 的对偶 $\mathrm{Hom}_R(M,R)$），$(\phi_M(m))(\psi) = \psi(m)$。
这族映射 $\phi = \{\phi_M\}$ 构成了一个从恒等[函子](@entry_id:150427)到二重对偶[函子](@entry_id:150427)的自然变换。为了证明这一点，我们需要验证对于任意 $R$-[模同态](@entry_id:148144) $f: M \to N$，自然性条件 $f^{**} \circ \phi_M = \phi_N \circ f$ 成立。这意味着对于任意 $m \in M$，等式 $f^{**}(\phi_M(m)) = \phi_N(f(m))$ 在 $N^{**}$ 中成立。
为了检验这个等式，我们将两边的元素作用于 $N^*$ 中的任意一个元素 $\chi$：
- 左侧：$(f^{**}(\phi_M(m)))(\chi) = (\phi_M(m) \circ f^*)(\chi) = \phi_M(m)(f^*(\chi)) = \phi_M(m)(\chi \circ f) = (\chi \circ f)(m) = \chi(f(m))$。
- 右侧：$(\phi_N(f(m)))(\chi) = \chi(f(m))$。
由于两边的结果对于任意 $\chi$ 都相等，所以等式成立，证明了 $\phi$ 确实是一个自然变换 [@problem_id:1797634]。

**自然性的缺失**
自然性是一个非常强的约束。一个映射族，即使其每个分量都是合法的态射，也可能因为其构造的“任意性”而无法满足自然性条件。例如，在实[向量空间](@entry_id:151108)范畴 $\mathbf{Vect}_{\mathbb{R}}$ 中，考虑恒等函子 $Id$。我们定义一族映射 $\tau = \{\tau_V: V \to V\}$，其中对于每个维数至少为1的[向量空间](@entry_id:151108) $V$，$\tau_V$ 是一个到 $V$ 的某个*一维[子空间](@entry_id:150286)*的投影。
虽然每个 $\tau_V$ 本身都是一个合法的线性映射（即 $\mathbf{Vect}_{\mathbb{R}}$ 中的态射），但这族映射通常不构成一个自然变换。问题在于每个一维[子空间](@entry_id:150286)是*任意选择*的，缺乏规范性。我们可以构造一个反例来表明自然性方块不交换。
设 $V$ 是一个维数至少为2的[向量空间](@entry_id:151108)，$\tau_V$ 是到一维[子空间](@entry_id:150286) $L_V$ 的投影。设 $W$ 是一个一维[向量空间](@entry_id:151108)，那么到 $W$ 的一维[子空间](@entry_id:150286)的投影只能是[恒等映射](@entry_id:634191) $id_W$，即 $\tau_W=id_W$。现在，选择一个线性映射 $f: V \to W$ 和 $V$ 中的一个向量 $v$，使得 $v$ 在 $\tau_V$ 的核中（即 $\tau_V(v) = 0$）但 $f(v) \neq 0$（这总是可能的）。
我们来检查自然性条件 $f \circ \tau_V = \tau_W \circ f$ 是否对这个 $v$ 成立：
- 左侧：$(f \circ \tau_V)(v) = f(\tau_V(v)) = f(0) = 0$。
- 右侧：$(\tau_W \circ f)(v) = id_W(f(v)) = f(v)$。
因为 $f(v) \neq 0$，所以 $f \circ \tau_V \neq \tau_W \circ f$。这表明，这种依赖于任意选择的投影族不是一个自然变换 [@problem_id:1797661]。

#### 自然变换的代数

自然变换本身也可以被组织起来，形成更高级的结构。

**垂直复合 (Vertical Composition)**
如果 $\alpha: F \Rightarrow G$ 和 $\beta: G \Rightarrow H$ 是两个自然变换（在相同的[函子](@entry_id:150427)之间），我们可以定义它们的**垂直复合** $\gamma = \beta \circ \alpha: F \Rightarrow H$。其定义是逐分量进行的：对于每个对象 $X$，复合变换的分量 $\gamma_X$ 就是原变换分量的复合，即 $\gamma_X = \beta_X \circ \alpha_X$。可以证明，这样定义的 $\gamma$ 仍然是一个自然变换。这个复合操作具有结合律，并且有单位元（即由单位态射构成的自然变换），这使得对于给定的范畴 $\mathbf{C}$ 和 $\mathbf{D}$，从 $\mathbf{C}$ 到 $\mathbf{D}$ 的所有[函子](@entry_id:150427)和它们之间的所有自然变换构成了一个新的范畴，称为**函子范畴** (functor category)，记作 $\mathbf{D}^{\mathbf{C}}$ 或 $[\mathbf{C}, \mathbf{D}]$ [@problem_id:1797642]。

**自然同构 (Natural Isomorphisms)**
如果一个自然变换 $\eta: F \Rightarrow G$ 的每一个分量 $\eta_X: F(X) \to G(X)$ 都是目标范畴 $\mathbf{D}$ 中的一个同构，那么我们称 $\eta$ 是一个**自然同构** (natural isomorphism)。如果存在一个从 $F$ 到 $G$ 的自然同构，我们就说[函子](@entry_id:150427) $F$ 和 $G$ 是**自然同构的**，记作 $F \cong G$。这意味着从[范畴论](@entry_id:137315)的观点看，这两个函子是“本质上相同”的。

自然同构的每个分量 $\eta_X$ 都有一个逆 $(\eta_X)^{-1}$。可以证明，由这些逆态射组成的族 $\{\eta_X^{-1}\}_{X \in \mathrm{Obj}(\mathbf{C})}$ 本身也构成一个从 $G$ 到 $F$ 的自然变换，它是 $\eta$ 的逆。

自然性条件在处理自然同构时显示出其强大的[约束力](@entry_id:170052)。假设 $\eta: F \to G$ 是一个自然同构，其分量在对象 $0$ 和 $1$ 处由[可逆矩阵](@entry_id:171829) $M_0$ 和 $M_1$ 表示。对于一个态射 $f: 0 \to 1$，$F(f)$ 和 $G(f)$ 分别由矩阵 $A_F$ 和 $A_G$ 表示。自然性条件 $G(f) \circ \eta_0 = \eta_1 \circ F(f)$ 在矩阵层面就变成了 $A_G M_0 = M_1 A_F$。这个方程将不同对象上的分量联系在了一起。这表明，自然性条件不仅是一个验证工具，更是一个强大的计算和推理工具 [@problem_id:1797662]。

回到常函子的例子 [@problem_id:1797644]，我们考虑两个常函子 $F, G: \mathbf{C} \to \mathbf{D}$，它们分别将所有对象映为 $S_A$ 和 $S_B$。一个从 $F$ 到 $G$ 的自然变换 $\eta$ 由一族态射 $\eta_X: S_A \to S_B$ 组成。对于 $\mathbf{C}$ 中的任意非恒等态射 $f: O_1 \to O_2$，自然性条件为 $G(f) \circ \eta_{O_1} = \eta_{O_2} \circ F(f)$。由于 $F$ 和 $G$ 是常函子， $G(f)$ 和 $F(f)$ 都是单位态射，因此条件简化为 $id_{S_B} \circ \eta_{O_1} = \eta_{O_2} \circ id_{S_A}$，即 $\eta_{O_1} = \eta_{O_2}$。这意味着整个自然变换完全由一个单一的态射（函数）$\eta: S_A \to S_B$ 决定。这清晰地展示了自然性条件如何将看似独立的各分量“捆绑”在一起，体现了“自然”的真正含义。