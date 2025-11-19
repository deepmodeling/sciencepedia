## 引言
在量子多体物理领域，直接处理由海量粒子（如[阿伏伽德罗常数](@entry_id:141949)级别）组成的系统是一个几乎无法完成的任务。随着粒子数 $N$ 的增加，描述系统的[波函数](@entry_id:147440)维度呈指数级增长，而[全同粒子](@entry_id:142755)所要求的对称性或反对称性更使其结构变得异常复杂。这构成了理论物理学中的一个核心知识鸿沟：我们如何才能有效地描述和计算这些强相互关联系统的行为？

[二次量子化](@entry_id:137766)的语言应运而生，为解决这一根本性挑战提供了一个优雅而强大的框架。它彻底转变了视角，将[焦点](@entry_id:174388)从难以驾驭的[多体波函数](@entry_id:203043)转移到一组在“[福克空间](@entry_id:143624)”中作用的抽象代数算符——[产生与湮灭算符](@entry_id:194608)上。这套语言不仅简化了数学表示，更深刻地揭示了[粒子统计](@entry_id:145640)性质、相互作用以及[集体激发](@entry_id:145026)的物理本质。

本文旨在系统性地引导读者掌握这门核心语言。在“原理与机制”一章中，我们将从零开始，构建[二次量子化](@entry_id:137766)的基本公理，阐明[玻色子与费米子](@entry_id:147957)算符的代数规则，并学习如何表示[量子态](@entry_id:146142)与[物理可观测量](@entry_id:154692)。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这套语言在凝聚态物理、[量子化学](@entry_id:140193)和[量子光学](@entry_id:140582)等前沿领域的具体应用，看它如何被用来构建和理解从Hubbard模型到超导理论的各种物理模型。最后，通过“动手实践”部分，您将有机会亲手运用这些工具来解决具体问题，从而巩固所学知识。

## 原理与机制

在[多体量子系统](@entry_id:161678)的研究中，直接处理包含大量粒子（例如 $N \sim 10^{23}$）的[波函数](@entry_id:147440)是不可行的。不仅因为[波函数](@entry_id:147440)的维度 ($(\mathbb{C}^d)^N$) 随粒子数 $N$ [指数增长](@entry_id:141869)，更重要的是，[全同粒子](@entry_id:142755)的对称性或[反对称性](@entry_id:261893)要求使得[波函数](@entry_id:147440)的结构异常复杂。[二次量子化](@entry_id:137766)语言的出现，正是为了解决这一根本性挑战。它将[焦点](@entry_id:174388)从复杂的N体[波函数](@entry_id:147440)转移到一组遵循特定代数规则的抽象算符上。这些算符在一个名为**[福克空间](@entry_id:143624) (Fock space)** 的扩展[希尔伯特空间](@entry_id:261193)中作用，该空间能够容纳任意粒子数的[量子态](@entry_id:146142)。本章将系统地阐述[二次量子化](@entry_id:137766)的基本原理与核心机制。

### 构建模块：[产生与湮灭算符](@entry_id:194608)

[二次量子化](@entry_id:137766)的核心思想是用代数方法处理粒子的增减。这是通过引入**[产生算符](@entry_id:191512) (creation operator)** 和**[湮灭算符](@entry_id:165390) (annihilation operator)** 实现的。对于给定的单粒子[量子态](@entry_id:146142)（或模式）$k$，我们定义一个[产生算符](@entry_id:191512) $a_k^\dagger$（或 $c_k^\dagger$），它将一个粒子添加到该模式中；同时定义一个[湮灭算符](@entry_id:165390) $a_k$（或 $c_k$），它从该模式中移除一个粒子。

[福克空间](@entry_id:143624)的基础是**真空态 (vacuum state)**，记作 $|0\rangle$ 或 $|\text{vac}\rangle$。这是一个不包含任何粒子的状态，因此任何[湮灭算符](@entry_id:165390)作用于其上都得到[零矢量](@entry_id:155273)：对所有 $k$ 都有 $a_k |0\rangle = 0$。从真空态出发，通过反复应用[产生算符](@entry_id:191512)，我们可以构建出包含任意数量、任意[分布](@entry_id:182848)的粒子的多体态。

粒子的内在统计性质——[玻色-爱因斯坦统计](@entry_id:139965)或[费米-狄拉克统计](@entry_id:140706)——深刻地影响了这些算符的[代数结构](@entry_id:137052)。

#### [玻色子](@entry_id:138266)算符

[玻色子](@entry_id:138266)是遵循[玻色-爱因斯坦统计](@entry_id:139965)的粒子，多个全同[玻色子](@entry_id:138266)可以占据同一个单粒子态。描述它们的产生和湮灭算符（通常用 $a_k^\dagger$ 和 $a_k$ 表示）遵循**[正则对易关系](@entry_id:185041) (Canonical Commutation Relations, CCRs)**：

$$
[a_k, a_l^\dagger] = \delta_{kl}
$$
$$
[a_k, a_l] = 0
$$
$$
[a_k^\dagger, a_l^\dagger] = 0
$$

其中 $[A, B] = AB - BA$ 是对易子，$\delta_{kl}$ 是克罗内克符号。第一条关系式表明，在同一模式中先产生后湮灭与先湮灭后产生的效果相差一个单位，这反映了粒子数的离散性。后两条关系式表明，不同模式的算符之间或者相同类型的算符之间可以任意交换顺序。

这些算符在[粒子数态](@entry_id:155105)（或称[福克态](@entry_id:155105)）$|n_k\rangle$ 上的作用是明确的，其中 $n_k$ 是模式 $k$ 中的粒子数：

$$
a_k |n_k\rangle = \sqrt{n_k} |n_k-1\rangle
$$
$$
a_k^\dagger |n_k\rangle = \sqrt{n_k+1} |n_k+1\rangle
$$

$\sqrt{n_k}$ 和 $\sqrt{n_k+1}$ 这两个因子的出现，保证了态的归一化，并且与[量子谐振子](@entry_id:140678)中的[升降算符](@entry_id:197899)形式一致。

#### [费米子算符](@entry_id:149120)

[费米子](@entry_id:146235)是遵循[费米-狄拉克统计](@entry_id:140706)的粒子，其核心特征是**[泡利不相容原理](@entry_id:141850) (Pauli exclusion principle)**：两个或多个全同[费米子](@entry_id:146235)不能占据同一个[量子态](@entry_id:146142)。这一原理被巧妙地编码在它们的产生和湮灭算符（通常用 $c_k^\dagger$ 和 $c_k$ 表示）的代数关系中，即**[正则反对易关系](@entry_id:146961) (Canonical Anticommutation Relations, CARs)**：

$$
\{c_k, c_l^\dagger\} = \delta_{kl}
$$
$$
\{c_k, c_l\} = 0
$$
$$
\{c_k^\dagger, c_l^\dagger\} = 0
$$

其中 $\{A, B\} = AB + BA$ 是[反对易子](@entry_id:139754)。这些关系式直接体现了[费米子](@entry_id:146235)的独特性质。例如，第二条关系式对任意两个（即使是相同的）[湮灭算符](@entry_id:165390)都成立。特别地，当我们考虑在同一个模式 $k$ 上连续作用两次[产生算符](@entry_id:191512)时，第三条关系式给出了一个深刻的结果：

$$
\{c_k^\dagger, c_k^\dagger\} = c_k^\dagger c_k^\dagger + c_k^\dagger c_k^\dagger = 2(c_k^\dagger)^2 = 0 \implies (c_k^\dagger)^2 = 0
$$

这个简单的代数恒等式 $(c_k^\dagger)^2 = 0$ 意味着不可能在同一个模式 $k$ 中创建两个粒子，这正是[泡利不相容原理](@entry_id:141850)在[二次量子化](@entry_id:137766)语言中的数学表达。因此，对于[费米子](@entry_id:146235)，每个模式的占据数 $n_k$ 只能是 $0$ 或 $1$。

算符在这些占据数态上的作用也因此变得非常简单：
- $c_k |0_k\rangle = 0$
- $c_k |1_k\rangle = |0_k\rangle$
- $c_k^\dagger |0_k\rangle = |1_k\rangle$
- $c_k^\dagger |1_k\rangle = (c_k^\dagger)^2 |0_k\rangle = 0$

通过在占据数基矢上直接计算，我们可以验证 $\{c_k, c_k^\dagger\} = c_k c_k^\dagger + c_k^\dagger c_k = 1$ 确实成立，这为[反对易关系](@entry_id:153815)的[自洽性](@entry_id:160889)提供了具体例证。

值得注意的是，当处理**非正交 (non-orthogonal)** 的单粒子基矢时，例如在某些[紧束缚模型](@entry_id:143446)中，[反对易关系](@entry_id:153815)会推广为 $\{c_i, c_j^\dagger\} = \langle i|j \rangle = S_{ij}$，其中 $S_{ij}$ 是单粒子态 $|i\rangle$ 和 $|j\rangle$ 之间的交叠积分。标准的正交[反对易关系](@entry_id:153815)是此通用形式在 $S_{ij} = \delta_{ij}$ 时的特例。

### 态与物理可观测量之表示

有了产生和[湮灭算符](@entry_id:165390)这些基本构件，我们现在可以构建[多体系统](@entry_id:144006)的[量子态](@entry_id:146142)和表示[物理可观测量](@entry_id:154692)。

#### 多体态的构建

一个包含多个粒子的多体态，可以通过一系列[产生算符](@entry_id:191512)作用于真空态来构建。例如，一个包含三个不同动量 $\vec{k}_1, \vec{k}_2, \vec{k}_3$ 的[费米子](@entry_id:146235)态可以表示为：

$$
|\Psi\rangle = c_{\vec{k}_3}^\dagger c_{\vec{k}_2}^\dagger c_{\vec{k}_1}^\dagger |\text{vac}\rangle
$$

由于[费米子](@entry_id:146235)[产生算符](@entry_id:191512)相互[反对易](@entry_id:186708)（例如 $c_i^\dagger c_j^\dagger = -c_j^\dagger c_i^\dagger$），交换任意两个算符的顺序会给态矢带来一个负号。这自动地将态的[反对称性](@entry_id:261893)（即斯莱特行列式 (Slater determinant) 的性质）编码了进来。对于[玻色子](@entry_id:138266)，由于[产生算符](@entry_id:191512)相互对易，所产生的态是自动对称化的。例如，一个在模式 $k$ 上有 $N$ 个[玻色子](@entry_id:138266)的归一化态是通过 $(a_k^\dagger)^N / \sqrt{N!}$ 作用于真空态得到的。

#### [物理可观测量](@entry_id:154692)

在[二次量子化](@entry_id:137766)中，任何[物理可观测量](@entry_id:154692)（如[哈密顿量](@entry_id:172864)、动量、密度等）都可以用产生和[湮灭算符](@entry_id:165390)的组合来表示。将一个在第一量子化中定义的算符转换成其[二次量子化](@entry_id:137766)形式，是该语言的核心应用之一。

**[单体](@entry_id:136559)算符 (One-Body Operators)**：一个[单体](@entry_id:136559)算符是在所有粒子上求和的形式，$\hat{O}^{(1)} = \sum_{i=1}^N \hat{o}_i$。其[二次量子化](@entry_id:137766)形式为：

$$
\hat{O} = \sum_{k,l} \langle k | \hat{o} | l \rangle c_k^\dagger c_l
$$

其中 $\langle k | \hat{o} | l \rangle$ 是单粒子算符 $\hat{o}$ 在[基矢](@entry_id:199546) $|k\rangle$ 和 $|l\rangle$ 之间的矩阵元。这个表达式的物理图像是：算符 $\hat{O}$ 通过湮灭一个处于 $|l\rangle$ 态的粒子并产生一个处于 $|k\rangle$ 态的粒子，从而实现对系统的作用，其作用强度由[矩阵元](@entry_id:186505) $\langle k | \hat{o} | l \rangle$ 决定。

- **[粒子数算符](@entry_id:153568) (Number Operator)**：最简单的[单体](@entry_id:136559)算符是[粒子数算符](@entry_id:153568) $n_k = c_k^\dagger c_k$（或 $N_k = a_k^\dagger a_k$）。它的矩阵元是 $\langle k | 1 | k \rangle = 1$，其他为零。该算符的[本征值](@entry_id:154894)正是模式 $k$ 中的粒子数。总[粒子数算符](@entry_id:153568)就是所有模式的[粒子数算符](@entry_id:153568)之和，$N = \sum_k n_k$。

- **无[相互作用哈密顿量](@entry_id:181720)**：一个[无相互作用系统](@entry_id:143064)的[哈密顿量](@entry_id:172864)是所有粒子[单粒子能量](@entry_id:160812)之和，其[二次量子化](@entry_id:137766)形式为 $H_0 = \sum_k \epsilon_k c_k^\dagger c_k$，其中 $\epsilon_k$ 是模式 $k$ 的[单粒子能量](@entry_id:160812)。

- **[场算符](@entry_id:140269)与[密度算符](@entry_id:138151)**：为了描述空间相关的物理量，引入**[场算符](@entry_id:140269) (field operators)** 是非常方便的：
  $$
  \hat{\Psi}(\vec{r}) = \sum_k \phi_k(\vec{r}) c_k, \quad \hat{\Psi}^\dagger(\vec{r}) = \sum_k \phi_k^*(\vec{r}) c_k^\dagger
  $$
  其中 $\phi_k(\vec{r})$ 是单粒子[波函数](@entry_id:147440)。$\hat{\Psi}^\dagger(\vec{r})$ 可以被理解为在空间点 $\vec{r}$ 处产生一个粒子。利用[场算符](@entry_id:140269)，粒子[密度算符](@entry_id:138151)可以简洁地写为 $\hat{\rho}(\vec{r}) = \hat{\Psi}^\dagger(\vec{r})\hat{\Psi}(\vec{r})$。这个算符的[期望值](@entry_id:153208) $\langle \hat{\rho}(\vec{r}) \rangle$ 给出系统在 $\vec{r}$ 处的平均粒子密度。

- **键序算符 (Bond Order Operator)**：在凝聚态物理中，描述粒子在不同格点间跃迁强度的“键序”是一个重要物理量。例如，连接格点 $i$ 和 $j$ 的键序算符可以定义为 $B_{ij} = \sum_\sigma (c_{i\sigma}^\dagger c_{j\sigma} + c_{j\sigma}^\dagger c_{i\sigma})$，它包含了从 $j$ 到 $i$ 和从 $i$ 到 $j$ 的跃迁过程。

**二体算符 (Two-Body Operators)**：描述粒子间相互作用的算符，例如库仑相互作用，是二体算符。其一般形式 $\hat{O}^{(2)} = \frac{1}{2} \sum_{i \neq j} \hat{o}(\vec{r}_i, \vec{r}_j)$ 在[二次量子化](@entry_id:137766)中表示为：

$$
\hat{O} = \frac{1}{2} \sum_{p,q,r,s} V_{pqrs} c_p^\dagger c_q^\dagger c_s c_r
$$

其中 $V_{pqrs} = \langle pq | \hat{o} | rs \rangle$ 是二体相互作用[矩阵元](@entry_id:186505)。这个表达式描述了一个散射过程：两个分别处于态 $|r\rangle$ 和 $|s\rangle$ 的粒子被湮灭，同时两个粒子被产生到新的态 $|p\rangle$ 和 $|q\rangle$。注意算符的顺序：[产生算符](@entry_id:191512)在外，[湮灭算符](@entry_id:165390)在内；湮灭算符的指标顺序 ($s, r$) 与[矩阵元](@entry_id:186505)中末态的指标顺序 ($r, s$) 相反，这是[费米子](@entry_id:146235)反对易性的一个惯例。

这个框架可以推广到任意**N体算符**。例如，一个[三体](@entry_id:265960)相互作用 $W(x_1, x_2, x_3)$ 的[二次量子化](@entry_id:137766)形式为：

$$
\hat{W} = \frac{1}{3!} \int dx_1 dx_2 dx_3 \, \hat{\Psi}^\dagger(x_1) \hat{\Psi}^\dagger(x_2) \hat{\Psi}^\dagger(x_3) W(x_1, x_2, x_3) \hat{\Psi}(x_3) \hat{\Psi}(x_2) \hat{\Psi}(x_1)
$$

### 代数工具箱：对易子、守恒律与排序定理

掌握[二次量子化](@entry_id:137766)的语言，意味着能够熟练地运用其代数规则来简化表达式和计算物理量。

#### 对易关系与代数运算

利用基本的(反)[对易关系](@entry_id:136780)，我们可以计算更复杂算符之间的对易子。这是一个基本功。例如，计算[玻色子](@entry_id:138266)数算符 $a^\dagger a$ 与湮灭算符 $a$ 的对易子：

$$
[a^\dagger a, a] = a^\dagger a a - a a^\dagger a
$$

利用 $[a, a^\dagger]=1$ 或 $a a^\dagger = a^\dagger a + 1$，我们得到：

$$
[a^\dagger a, a] = a^\dagger a^2 - (a^\dagger a + 1)a = a^\dagger a^2 - a^\dagger a^2 - a = -a
$$

这个结果表明，[湮灭算符](@entry_id:165390) $a$ 是数算符 $a^\dagger a$ 的本征算符（广义上），[本征值](@entry_id:154894)为 $-1$，这意味着 $a$ 的作用是使系统粒子数减1。

#### 守恒律

在量子力学中，如果一个[可观测量](@entry_id:267133)是守恒的，那么其对应的算符与[哈密顿量](@entry_id:172864)对易。[二次量子化](@entry_id:137766)提供了一个检验守恒律的强大代数框架。

一个核心的守恒律是**总粒子数守恒**。对于一个典型的[哈密顿量](@entry_id:172864) $H = H_0 + V$，其中 $H_0 = \sum_k \epsilon_k c_k^\dagger c_k$ 是[单体](@entry_id:136559)项，而 $V = \frac{1}{2} \sum_{pqrs} V_{pqrs} c_p^\dagger c_q^\dagger c_s c_r$ 是二体[相互作用项](@entry_id:637283)。我们可以证明总[粒子数算符](@entry_id:153568) $N=\sum_k c_k^\dagger c_k$ 与 $H_0$ 和 $V$ 都对易。

- 对于 $H_0$，我们有 $[H_0, N] = [\sum_k \epsilon_k n_k, \sum_q n_q] = \sum_{k,q} \epsilon_k [n_k, n_q]$。由于不同模式的数算符相互对易（即 $[n_k, n_q]=0$ 对 $k \neq q$ 成立，而对 $k=q$ 则显然为零），所以 $[H_0, N]=0$。
- 对于 $V$，计算 $[N, V]$ 会发现，每个二体项 $c_p^\dagger c_q^\dagger c_s c_r$ 中包含两个[产生算符](@entry_id:191512)和两个[湮灭算符](@entry_id:165390)。与总数算符 $N$ 的对易子会精确地得到零，这表明这种形式的相互作用过程，虽然改变了各个模式的粒子数，但保持了系统总粒子数不变。

#### [正规排序](@entry_id:145434)与维克定理

计算真空态对一长串产生和[湮灭算符](@entry_id:165390)的[期望值](@entry_id:153208)是一项常见的任务。**[正规排序](@entry_id:145434) (Normal Ordering)** 和**维克定理 (Wick's Theorem)** 为此提供了系统性的方法。

一个算符乘积的**[正规排序](@entry_id:145434)**，记为 $\mathcal{N}(\dots)$ 或 $:\dots:$，是指通过重新[排列](@entry_id:136432)，将所有的[产生算符](@entry_id:191512)都移动到所有湮灭算符的左边。对于[费米子](@entry_id:146235)，每次[交换算符](@entry_id:156554)位置需要引入一个由[排列](@entry_id:136432)的奇偶性决定的符号。[正规排序](@entry_id:145434)的算符的[真空期望值](@entry_id:146340)恒为零。

**维克定理**指出，一串算符的乘积等于其所有可能的完全“收缩”之和。**收缩 (contraction)** 是指一对算符（通常是一个[湮灭算符](@entry_id:165390)和一个[产生算符](@entry_id:191512)）的[真空期望值](@entry_id:146340)。例如，对于[玻色子](@entry_id:138266)，收缩的定义是 $\contraction{}{A}{}{B} AB = \langle 0 | AB | 0 \rangle$。维克定理将一个复杂的[真空期望值](@entry_id:146340)计算分解为一系列简单的收缩项的乘积。

例如，我们来计算 $\langle 0 | a a a^\dagger a^\dagger | 0 \rangle$。[玻色子](@entry_id:138266)收缩的基本值是 $\contraction{}{a}{}{a^\dagger} a a^\dagger = 1$ 和 $\contraction{}{a}{}{a} aa = \contraction{}{a^\dagger}{}{a^\dagger} a^\dagger a^\dagger = 0$。有以下两种非零的完全收缩方式：
1. 第一个 $a$ 与第一个 $a^\dagger$ 收缩，第二个 $a$ 与第二个 $a^\dagger$ 收缩：贡献为 $1 \times 1 = 1$。
2. 第一个 $a$ 与第二个 $a^\dagger$ 收缩，第二个 $a$ 与第一个 $a^\dagger$ 收缩：贡献为 $1 \times 1 = 1$。

总[期望值](@entry_id:153208)就是所有这些贡献之和：$\langle 0 | a a a^\dagger a^\dagger | 0 \rangle = 1 + 1 = 2$。

#### Baker-Campbell-Hausdorff (BCH) 恒等式

在处理算符的指数函数时，[BCH公式](@entry_id:197600)的一个特例非常有用。如果两个算符 $A$ 和 $B$ 的对易子 $[A, B]$ 是一个与 $A$ 和 $B$ 都对易的 c-数（即一个复数），那么：
$$
e^{A+B} = e^A e^B e^{-\frac{1}{2}[A,B]}
$$
这个公式是在[二次量子化](@entry_id:137766)中进行算符重新排序的利器。一个经典应用是[正规排序](@entry_id:145434)**位移算符 (displacement operator)** $D(\alpha) = \exp(\alpha a^\dagger - \alpha^* a)$，它在[相干态](@entry_id:154533)理论中至关重要。令 $A = \alpha a^\dagger$ 和 $B = -\alpha^* a$，它们的对易子是 $[A, B] = [ \alpha a^\dagger, -\alpha^* a] = -\alpha\alpha^* [a^\dagger, a] = |\alpha|^2$。这是一个 c-数，因此可以使用上述[BCH公式](@entry_id:197600)：
$$
D(\alpha) = \exp(\alpha a^\dagger - \alpha^* a) = \exp(\alpha a^\dagger) \exp(-\alpha^* a) \exp\left(-\frac{1}{2}|\alpha|^2\right)
$$
这个结果给出了位移算符的[正规排序](@entry_id:145434)形式。

### 高级构造与变换

在掌握了基本语言和工具后，我们可以构建更复杂的概念和变换，以解决具体的物理问题。

#### 对称性算符的构造

- **[平移算符](@entry_id:756122) (Translation Operator)**：在[晶格](@entry_id:196752)系统中，平移对称性至关重要。[平移算符](@entry_id:756122) $T$ 使每个格点指标移动一位。它在实空间和[动量空间](@entry_id:148936)算符上的作用定义了它的性质：$T c_j^\dagger T^{-1} = c_{j+1}^\dagger$。由此可以推导出它在[动量空间](@entry_id:148936)算符上的作用：$T c_k^\dagger T^{-1} = e^{-ika} c_k^\dagger$，其中 $a$ 是[晶格常数](@entry_id:158935)。这意味着一个动量为 $k$ 的单粒子态是 $T$ 的本征态，[本征值](@entry_id:154894)为 $e^{-ika}$。对于一个多体态，例如 $|k_1, k_2\rangle = c_{k_1}^\dagger c_{k_2}^\dagger |0\rangle$，它是 $T$ 的[本征态](@entry_id:149904)，[本征值](@entry_id:154894)为所有粒子[本征值](@entry_id:154894)的乘积 $e^{-i(k_1+k_2)a}$。

- **[宇称算符](@entry_id:148434) (Parity Operator)**：宇称（空间反演）是另一个重要的[离散对称性](@entry_id:146994)。在[二次量子化](@entry_id:137766)中，[宇称算符](@entry_id:148434) $\mathcal{P}$ 可以由更基本的算符，如交换两个格点 $i$ 和 $j$ 的[费米子](@entry_id:146235)**[交换算符](@entry_id:156554) (SWAP operator)** $S_{ij}$，组合而成。通过理解其在基本态上的作用，可以计算它在任意叠加态中的[期望值](@entry_id:153208)，从而判断态的宇称性质。

#### [典范变换](@entry_id:178165)

[典范变换](@entry_id:178165)是一种[变量替换](@entry_id:141386)，它寻找一组新的产生和[湮灭算符](@entry_id:165390)（通常称为**[准粒子](@entry_id:136584) (quasiparticle)** 算符），使得[哈密顿量](@entry_id:172864)在新的基底下形式更简单（理想情况下是对角的）。这种变换必须保持基本的(反)[对易关系](@entry_id:136780)不变。

- **Bogoliubov 变换**：这是处理超流和超导理论中[配对相互作用](@entry_id:158014)的基石。对于[玻色子](@entry_id:138266)系统，一种常见的 Bogoliubov 变换形式为：
  $$
  \gamma_k = u_k a_k + v_k a_{-k}^\dagger
  $$
  这里，新的[湮灭算符](@entry_id:165390) $\gamma_k$ 是原有粒子算符的线性组合。为了使新的算符 $\gamma_k$ 仍然满足[玻色子](@entry_id:138266)的[正则对易关系](@entry_id:185041)，即 $[\gamma_k, \gamma_k^\dagger] = 1$，系数 $u_k$ 和 $v_k$ 必须满足约束条件 $|u_k|^2 - |v_k|^2 = 1$。

- **Jordan-Wigner 变换**：这是一个深刻的变换，它在一维系统中建立了自旋-1/2 算符和无自旋[费米子算符](@entry_id:149120)之间的精确映射。例如，$f_j = (\prod_{k=1}^{j-1} \sigma_k^z) \sigma_j^-$。这个变换是非局域的，因为定义在 $j$ 点的费米算符依赖于所有在 $j$ 点左边的自旋状态（通过 $\sigma_k^z$ 连成的“弦”）。这个变换在研究一维[量子磁性](@entry_id:145792)和拓扑物态中极其有用，但它也带来了边界条件的复杂性，例如[周期性边界条件](@entry_id:147809)的[自旋链](@entry_id:139648)可能对应于周期性或反[周期性边界条件](@entry_id:147809)的[费米子](@entry_id:146235)链，这取决于总粒子数的奇偶性。

#### [元激发](@entry_id:140859)

[二次量子化](@entry_id:137766)语言特别适合描述系统从其简单[基态](@entry_id:150928)（如真空态或[费米海](@entry_id:136725)）出发的**[元激发](@entry_id:140859) (elementary excitations)**。

- **[粒子-空穴激发](@entry_id:137289) (Particle-Hole Excitations)**：在[费米子](@entry_id:146235)系统中，[基态](@entry_id:150928)通常是**[费米海](@entry_id:136725) (Fermi sea)**，即所有能量低于[费米能级](@entry_id:143215)的单粒子态都被占据。最低能量的激发是将一个费米面以下的粒子（能量 $E  E_F$）移动到费米面以上的一个空置能级（能量 $E' > E_F$）的过程。