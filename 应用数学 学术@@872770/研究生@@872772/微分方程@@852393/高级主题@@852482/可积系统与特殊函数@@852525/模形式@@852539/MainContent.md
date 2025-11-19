## 引言
模形式是现代数学中一颗璀璨的明珠，它们是定义在复上半平面上具有高度对称性的复变函数。这些函数的非凡之处在于，它们看似抽象的分析性质中，却编码了关于整数的极为深刻和精细的算术信息。从[费马大定理](@entry_id:204421)的最终证明到现代物理学的前沿探索，模形式始终扮演着连接不同数学分支的桥梁角色，揭示出数论、几何与分析之间令人惊叹的内在统一性。

然而，模形式理论的抽象性与技术性常常令人望而生畏。本文旨在填补这一知识鸿沟，系统地引导读者从基本原理走向前沿应用。我们将揭示这些美妙函数背后的结构与机制，并展示它们在解决具体问题时的强大威力。

在接下来的章节中，你将学到：
*   **第一章：原理与机制** 将从模形式的严格定义出发，构建起其赖以存在的空间结构，并介绍揭示其算术本质的核心工具——[赫克算子](@entry_id:181282)。
*   **第二章：应用与跨学科联系** 将展示模形式理论的辉煌成就，包括它在解决[费马大定理](@entry_id:204421)中的决定性作用，以及它在代数几何、[弦理论](@entry_id:145688)和“[魔群月光](@entry_id:201697)”等领域的惊人联系。
*   **第三章：动手实践** 将通过一系列精心设计的计算练习，让你亲手操作和感受模形式的性质，从而巩固理论知识。

现在，让我们启程，深入探索模形式理论的核心原理与机制。

## 原理与机制

在介绍性章节之后，我们现在深入探讨模形式理论的核心原理与机制。本章将从基本定义出发，逐步构建起模形式的空间结构，并介绍其深刻的算术性质。我们的目标是建立一个严谨的框架，以便理解模形式在现代数论中的中心地位。

### 模形式的严格定义

模形式是定义在复上半平面上的具有特定变换性质的全纯函数。让我们系统地阐述其定义。

**定义域与[群作用](@entry_id:268812)**

模形式的自然定义域是**复上半平面**（Upper Half-Plane），记为 $\mathfrak{H}$，它由所有虚部为正的复数构成：
$$ \mathfrak{H} = \{z \in \mathbb{C} : \operatorname{Im}(z) > 0 \} $$
作用于此空间的基本群是**[模群](@entry_id:184647)** $\mathrm{SL}_2(\mathbb{Z})$，即由[行列式](@entry_id:142978)为 $1$ 的 $2 \times 2$ 整[系数矩阵](@entry_id:151473)构成的群。$\mathrm{SL}_2(\mathbb{Z})$ 中的一个元素 $\gamma = \begin{pmatrix} a  b \\ c  d \end{pmatrix}$ 通过**[分式线性变换](@entry_id:174812)**（fractional linear transformation）作用于 $z \in \mathfrak{H}$：
$$ \gamma z = \frac{az+b}{cz+d} $$
可以验证，由于 $ad-bc=1$ 且 $a,b,c,d$ 为实数，此变换将 $\mathfrak{H}$ 映到自身。在模形式理论中，我们通常考虑 $\mathrm{SL}_2(\mathbb{Z})$ 的[子群](@entry_id:146164)，特别是所谓的**[同余子群](@entry_id:195720)**。

**权-$k$ 斜杠算子**

为了描述模形式的变换性质，我们引入**权-$k$ 斜杠算子**（weight-$k$ slash operator）。对于一个函数 $f: \mathfrak{H} \to \mathbb{C}$，一个整数 $k$，以及一个矩阵 $\gamma = \begin{pmatrix} a  b \\ c  d \end{pmatrix} \in \mathrm{SL}_2(\mathbb{Z})$，该算子定义为：
$$ (f|_k\gamma)(z) = (cz+d)^{-k} f(\gamma z) $$
这个定义中的因子 $(cz+d)^{-k}$ 称为**自守因子**（automorphy factor）。它的选取恰到好处，使得斜杠算子满足[群作用](@entry_id:268812)的性质，即对于任意 $\gamma_1, \gamma_2 \in \mathrm{SL}_2(\mathbb{Z})$，都有 $(f|_k\gamma_1)|_k\gamma_2 = f|_k(\gamma_1\gamma_2)$。

**尖点与 $q$-展开**

模形式的定义不仅涉及其在 $\mathfrak{H}$ 上的行为，还必须包含其在“边界”上的行为。$\mathrm{SL}_2(\mathbb{Z})$ 的作用自然地延拓到 $\mathfrak{H}$ 的边界，即[实轴](@entry_id:148276) $\mathbb{R}$ 与[无穷远点](@entry_id:172513) $\{\infty\}$。在模形式理论中，我们特别关注有理数点 $\mathbb{Q}$ 和无穷远点 $\{\infty\}$，它们在[同余子群](@entry_id:195720) $\Gamma$ 的作用下形成的[轨道](@entry_id:137151)被称为**[尖点](@entry_id:636792)**（cusps）。

对于一个函数 $f$ 来说，“在尖点处全纯”是什么意思？让我们以最重要的尖点 $\infty$ 为例。若 $f$ 对 $\Gamma$ 中的平移矩阵 $T = \begin{pmatrix} 1  1 \\ 0  1 \end{pmatrix}$ 具有某种周期性，它就可以展开成一个傅里叶级数。具体来说，如果 $f(z+h) = f(z)$ 对某个正整数 $h$ 成立，那么函数 $f$ 可以表示为 $q_h = \exp(2\pi i z/h)$ 的函数。由于当 $\operatorname{Im}(z) \to \infty$ 时，$|q_h| \to 0$，我们可以研究 $f$ 在 $q_h=0$ 附近的性质。

如果 $f$ 在 $q_h=0$ 处的 Laurent [级数展开](@entry_id:142878)不含负幂次项，即具有如下形式的 **$q$-展开**（$q$-expansion）：
$$ f(z) = \sum_{n=0}^{\infty} a_n q_h^n $$
我们就称 $f$ **在尖点 $\infty$ 处全纯**。对于其他任意[尖点](@entry_id:636792) $\mathfrak{a}$，我们可以通过一个矩阵 $\sigma \in \mathrm{SL}_2(\mathbb{Z})$ 将 $\infty$ 映到 $\mathfrak{a}$（即 $\sigma(\infty) = \mathfrak{a}$），然后考察变换后的函数 $f| _k \sigma$ 在 $\infty$ 处的行为。这个变换后的函数具有某个周期 $h_{\mathfrak{a}}$（称为尖点 $\mathfrak{a}$ 的**宽度**），我们要求其关于 $q_{h_{\mathfrak{a}}} = \exp(2\pi i z/h_{\mathfrak{a}})$ 的 $q$-展开不含负幂次项 [@problem_id:3023981]。

**模形式与[尖点形式](@entry_id:189096)的定义**

现在我们可以给出完整的定义 [@problem_id:3023964]。

设 $\Gamma$ 是 $\mathrm{SL}_2(\mathbb{Z})$ 的一个[子群](@entry_id:146164)，$k$ 是一个整数。一个函数 $f: \mathfrak{H} \to \mathbb{C}$ 被称为**权为 $k$ 的关于 $\Gamma$ 的模形式**（modular form of weight $k$ for $\Gamma$），如果它满足以下三个条件：
1.  $f$ 在 $\mathfrak{H}$ 上是全纯的。
2.  对于所有 $\gamma \in \Gamma$，$f$ 满足变换关系 $f|_k\gamma = f$。
3.  $f$ 在 $\Gamma$ 的所有[尖点](@entry_id:636792)处都是全纯的。

我们把权为 $k$ 的关于 $\Gamma$ 的模形式构成的[复向量空间](@entry_id:264355)记为 $M_k(\Gamma)$。

一个重要的[子空间](@entry_id:150286)是**[尖点形式](@entry_id:189096)**（cusp forms）的空间，记为 $S_k(\Gamma)$。一个模形式 $f \in M_k(\Gamma)$ 是一个[尖点形式](@entry_id:189096)，如果它在所有尖点处的 $q$-展开的常数项均为零。这等价于说，$f$ 在所有尖点处都“消失” [@problem_id:3023981]。

与模形式（要求在 $\mathfrak{H}$ 和所有尖点上全纯）相对的是**[模函数](@entry_id:155728)**（modular function）。一个权为 $0$ 的[模函数](@entry_id:155728)允许在 $\mathfrak{H}$ 内部和尖点处存在极点（即 $q$-展开中允许有有限个负幂次项）[@problem_id:3018266]。

### 模形式的空间与结构

模形式“生活”在与特定[同余子群](@entry_id:195720)关联的空间中。理解这些[子群](@entry_id:146164)的结构以及[模形式空间](@entry_id:199790)的具体例子，是深入该理论的关键。

#### 重要的[同余子群](@entry_id:195720)

数论中最重要的三族**[同余子群](@entry_id:195720)**（congruence subgroups）由模 $N$ ($N \ge 1$ 为整数)的[同余](@entry_id:143700)条件定义 [@problem_id:3023962]：
1.  **主[同余子群](@entry_id:195720)**（principal congruence subgroup of level $N$）：
    $$ \Gamma(N) = \left\{ \begin{pmatrix} a  b \\ c  d \end{pmatrix} \in \mathrm{SL}_2(\mathbb{Z}) : \begin{pmatrix} a  b \\ c  d \end{pmatrix} \equiv \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} \pmod{N} \right\} $$
2.  **$\Gamma_1(N)$**：
    $$ \Gamma_1(N) = \left\{ \begin{pmatrix} a  b \\ c  d \end{pmatrix} \in \mathrm{SL}_2(\mathbb{Z}) : \begin{pmatrix} a  b \\ c  d \end{pmatrix} \equiv \begin{pmatrix} 1  * \\ 0  1 \end{pmatrix} \pmod{N} \right\} $$
3.  **$\Gamma_0(N)$**：
    $$ \Gamma_0(N) = \left\{ \begin{pmatrix} a  b \\ c  d \end{pmatrix} \in \mathrm{SL}_2(\mathbb{Z}) : c \equiv 0 \pmod{N} \right\} $$

从定义可直接看出它们之间的包含关系：$\Gamma(N) \subset \Gamma_1(N) \subset \Gamma_0(N)$。这些群在 $\mathrm{SL}_2(\mathbb{Z})$ 中的指数（index）是有限的，其具体值可以通过分析相应的商群 $\mathrm{SL}_2(\mathbb{Z}/N\mathbb{Z})$ 来计算。例如，对于素数 $p$，指数为：
$$ [\mathrm{SL}_2(\mathbb{Z}) : \Gamma_0(p)] = p+1 $$
$$ [\mathrm{SL}_2(\mathbb{Z}) : \Gamma(p)] = p(p^2-1) $$
这些群的几何性质，如尖点的数量和椭圆[不动点](@entry_id:156394)的存在性，也依赖于 $N$。例如，对于 $N \ge 3$，$\Gamma(N)$ 是[无挠的](@entry_id:161664)（torsion-free），意味着它不包含除单位元外任何有限阶元素，其对应的[模曲线](@entry_id:199342)没有[椭圆点](@entry_id:273590) [@problem_id:3023962]。

#### 艾森斯坦级数：第一个范例

最重要的一类非[尖点形式](@entry_id:189096)是**艾森斯坦级数**（Eisenstein series）。对于偶数 $k \ge 4$，权为 $k$ 的关于全[模群](@entry_id:184647) $\mathrm{SL}_2(\mathbb{Z})$ 的非归一化艾森斯坦级数定义为：
$$ G_k(z) = \sum_{(m,n) \in \mathbb{Z}^2 \setminus \{(0,0)\}} (mz+n)^{-k} $$
这个级数在 $\mathfrak{H}$ 上绝对[一致收敛](@entry_id:146084)，可以证明它是一个权为 $k$ 的模形式。通过精巧的分析技巧，可以推导出它的 $q$-展开 [@problem_id:3023936]：
$$ G_k(z) = 2\zeta(k) + \frac{2(2\pi i)^k}{(k-1)!} \sum_{n=1}^{\infty} \sigma_{k-1}(n) q^n $$
其中 $q = \exp(2\pi i z)$，$\zeta(s)$ 是黎曼Zeta函数，$\sigma_{r}(n) = \sum_{d|n} d^r$ 是**[除数函数](@entry_id:194945)**。

这个展开式揭示了深刻的算术信息：模形式的傅里叶系数与[数论函数](@entry_id:200701)（如[除数函数](@entry_id:194945)）紧密相关。$G_k(z)$ 的常数项是 $2\zeta(k)$，它不为零，因此 $G_k(z)$ 不是一个[尖点形式](@entry_id:189096)。

通常，我们会对艾森斯坦级数进行**归一化**，使其常数项为 $1$。利用欧拉关于Zeta函数在偶数处的求值公式 $\zeta(k) = -\frac{(2\pi i)^k B_k}{2 \cdot k!}$，其中 $B_k$ 是**[伯努利数](@entry_id:177442)**，归一化后的艾森斯坦级数 $E_k(z) = G_k(z) / (2\zeta(k))$ 的 $q$-展开为：
$$ E_k(z) = 1 - \frac{2k}{B_k} \sum_{n=1}^{\infty} \sigma_{k-1}(n) q^n $$
例如，$k=4$ 和 $k=6$ 时，我们得到两个基本的归一化艾森斯坦级数：
$$ E_4(z) = 1 + 240 \sum_{n=1}^{\infty} \sigma_3(n) q^n $$
$$ E_6(z) = 1 - 504 \sum_{n=1}^{\infty} \sigma_5(n) q^n $$
我们将看到，$E_4$ 和 $E_6$ 是构建所有 $\mathrm{SL}_2(\mathbb{Z})$ 上模形式的基础。

#### [模形式空间](@entry_id:199790)的结构

对于给定的群 $\Gamma$ 和权 $k$，$M_k(\Gamma)$ 是一个有限维[复向量空间](@entry_id:264355)。它有一个重要的**[直和分解](@entry_id:263004)**：
$$ M_k(\Gamma) = S_k(\Gamma) \oplus \mathcal{E}_k(\Gamma) $$
这里 $S_k(\Gamma)$ 是[尖点形式](@entry_id:189096)空间，$\mathcal{E}_k(\Gamma)$ 是其补空间，称为**艾森斯坦空间**，由艾森斯坦级数张成。这个分解的本质在于，一个模形式是否为[尖点形式](@entry_id:189096)，取决于其在所有尖点处的常数项是否都为零。一个非零的艾森斯坦级数必然在至少一个尖点处有非零常数项 [@problem_id:3023981]。

对于全[模群](@entry_id:184647) $\mathrm{SL}_2(\mathbb{Z})$，模形式[环的结构](@entry_id:150907)异常优美。一个基本定理指出，所有 $\mathrm{SL}_2(\mathbb{Z})$ 上的模形式构成的**分次环** $M_*(\mathrm{SL}_2(\mathbb{Z})) = \bigoplus_k M_k(\mathrm{SL}_2(\mathbb{Z}))$ 同构于一个由 $E_4$ 和 $E_6$ 生成的多项式环 [@problem_id:3018421]：
$$ M_*(\mathrm{SL}_2(\mathbb{Z})) \cong \mathbb{C}[E_4, E_6] $$
这意味着任何权为 $k$ 的关于 $\mathrm{SL}_2(\mathbb{Z})$ 的模形式都可以唯一地写成 $E_4$ 和 $E_6$ 的[齐次多项式](@entry_id:178156)。具体而言，$M_k(\mathrm{SL}_2(\mathbb{Z}))$ 的一组基由所有满足 $4a+6b=k$ 的非负整数对 $(a,b)$ 对应的单项式 $E_4^a E_6^b$ 构成。

由此，我们可以推导出 $M_k(\mathrm{SL}_2(\mathbb{Z}))$ 的**维数公式**。其维数等于方程 $4a+6b=k$ 的非负整数解的个数。可以证明，对于偶数 $k \ge 0$：
$$ \dim M_k(\mathrm{SL}_2(\mathbb{Z})) = \begin{cases} \lfloor k/12 \rfloor  \text{if } k \equiv 2 \pmod{12} \\ \lfloor k/12 \rfloor + 1  \text{if } k \not\equiv 2 \pmod{12} \end{cases} $$
例如，对于权 $k=74$，由于 $74 = 12 \times 6 + 2$，所以 $\dim M_{74}(\mathrm{SL}_2(\mathbb{Z})) = \lfloor 74/12 \rfloor = 6$ [@problem_id:3018421]。

要得到[尖点形式](@entry_id:189096)空间的维数，我们需要**判别式函数** $\Delta$。它是一个权为 $12$ 的[尖点形式](@entry_id:189096)，定义为 $\Delta(\tau) = \eta(\tau)^{24}$，其中 $\eta(\tau)$ 是戴德金eta函数。它的 $q$-展开为：
$$ \Delta(\tau) = q \prod_{n=1}^{\infty}(1-q^n)^{24} = q - 24q^2 + 252q^3 - \dots $$
$\Delta$ 在 $\mathfrak{H}$ 上没有零点，且在无穷远点有一个一阶零点。一个关键事实是，乘以 $\Delta$ 会建立一个从 $M_{k-12}(\mathrm{SL}_2(\mathbb{Z}))$到 $S_k(\mathrm{SL}_2(\mathbb{Z}))$ 的同构，即 $f \mapsto f \cdot \Delta$。因此，我们有：
$$ \dim S_k(\mathrm{SL}_2(\mathbb{Z})) = \dim M_{k-12}(\mathrm{SL}_2(\mathbb{Z})) \quad (\text{for } k \ge 12) $$
对于 $k  12$，$S_k(\mathrm{SL}_2(\mathbb{Z}))$ 是[零空间](@entry_id:171336)。利用此公式，我们可以计算出一系列空间的维数 [@problem_id:3011132]。

这些基本模形式之间还存在代数关系。例如，可以证明 $E_4^3 - E_6^2 = 1728 \Delta$。这表明 $\Delta$ 并非一个独立的生成元。著名的**$j$-[不变量](@entry_id:148850)**（$j$-invariant）定义为 $j(\tau) = E_4(\tau)^3 / \Delta(\tau)$，它是一个权为 $0$ 的[模函数](@entry_id:155728)，其 $q$-展开为 $j(\tau) = q^{-1} + 744 + 196884q + \dots$。我们可以利用这些关系式来计算特定模形式的傅里叶系数 [@problem_id:3018425]。

### 模形式的算术：[赫克算子](@entry_id:181282)与[特征值](@entry_id:154894)

模形式的[傅里叶系数](@entry_id:144886)蕴含着深刻的算术信息。提取这些信息的核心工具是**[赫克算子](@entry_id:181282)**（Hecke operators）。

#### 内特征（Nebentypus）

在引入[赫克算子](@entry_id:181282)之前，我们先介绍一个重要的推广。对于 $\Gamma_0(N)$ 上的模形式，其变换法则可以包含一个**[狄利克雷特征](@entry_id:151586)** $\chi \pmod{N}$，称为**内特征**（Nebentypus）。一个权为 $k$，内特征为 $\chi$ 的关于 $\Gamma_0(N)$ 的模形式 $f$ 满足以下变换律 [@problem_id:3018266]：
$$ f(\gamma z) = \chi(d)(cz+d)^k f(z), \quad \text{for all } \gamma = \begin{pmatrix} a  b \\ c  d \end{pmatrix} \in \Gamma_0(N) $$
这里，由于 $ad-bc=1$ 和 $c \equiv 0 \pmod{N}$，我们有 $ad \equiv 1 \pmod{N}$，因此 $d$ 是模 $N$ 的一个可逆元，$\chi(d)$ 是良定义的。这个推广极大地丰富了模形式理论，并使其能够描述更广泛的算术现象。

#### [赫克算子](@entry_id:181282)的作用

对于每个正整数 $n$，都存在一个[线性算子](@entry_id:149003) $T_n$，称为**第 $n$ 个[赫克算子](@entry_id:181282)**，它作用于[模形式空间](@entry_id:199790) $M_k(\Gamma)$。它将 $M_k(\Gamma)$ 映到自身，并将 $S_k(\Gamma)$ 映到自身。

$T_n$ 的作用可以明确地体现在 $q$-展开上。对于一个 $M_k(\mathrm{SL}_2(\mathbb{Z}))$ 中的模形式 $f(z) = \sum_{m=0}^{\infty} a_m q^m$，其在 $T_n$ 作用下的像 $(T_n f)(z) = \sum_{M=0}^{\infty} b_M q^M$ 的系数由以下公式给出 [@problem_id:3018419]：
$$ b_M = \sum_{d|\gcd(n,M), d0} d^{k-1} a_{Mn/d^2} $$
例如，$(T_2 f)(z)$ 的 $q^M$ 系数是 $a_{2M} + 2^{k-1}a_{M/2}$（如果 $M$是偶数）或 $a_{2M}$（如果 $M$是奇数）。这个公式是通过对所有[行列式](@entry_id:142978)为 $n$ 的整矩阵的特定代表元进行平均得到的。

[赫克算子](@entry_id:181282)家族构成一个可交换的[算子代数](@entry_id:146444)。因此，我们可以寻找 $M_k(\Gamma)$ 的一组基，使得其中每个[基向量](@entry_id:199546)都是所有[赫克算子](@entry_id:181282) $T_n$ 的共同**[特征向量](@entry_id:151813)**，这样的模形式称为**赫克[特征形式](@entry_id:198300)**（Hecke eigenform）。

如果一个赫克[特征形式](@entry_id:198300) $f = \sum a_n q^n$ 被归一化使得 $a_1=1$，那么它具有一个非凡的性质：对于所有素数 $p$，它被 $T_p$ 作用的[特征值](@entry_id:154894)恰好是它的第 $p$ 个[傅里叶系数](@entry_id:144886) $a_p$：
$$ T_p(f) = a_p f $$
这些归一化的、属于[尖点形式](@entry_id:189096)空间中特定“新”[子空间](@entry_id:150286)（newform subspace）的赫克[特征形式](@entry_id:198300)被称为**[新形式](@entry_id:199611)**（newforms）。它们是模形式算术理论的基本构建单元。

### 通往[椭圆曲线](@entry_id:152409)的桥梁：模性定理

模形式理论最惊人的成果之一是它与[椭圆曲线](@entry_id:152409)的深刻联系，这一联系由**模性定理**（Modularity Theorem）所确立。该定理（曾被称为谷山-志村猜想）断言，每一条定义在有理数域 $\mathbb{Q}$ 上的[椭圆曲线](@entry_id:152409)都是“模的”。

具体来说，对于一条 conductor 为 $N$ 的[椭圆曲线](@entry_id:152409) $E/\mathbb{Q}$，该定理保证存在一个权为 $2$、水平为 $N$ 的[新形式](@entry_id:199611) $f \in S_2^{\text{new}}(\Gamma_0(N))$，其[傅里叶系数](@entry_id:144886) $a_p$ (对于不整除 $N$ 的素数 $p$) 精确地编码了 $E$ 在有限域 $\mathbb{F}_p$ 上的点数信息。

这个对应关系是：
$$ a_p = p+1 - \#E(\mathbb{F}_p) $$
其中 $\#E(\mathbb{F}_p)$ 是 $E$ 在[有限域](@entry_id:142106) $\mathbb{F}_p$ 上的[有理点](@entry_id:195164)个数（包括[无穷远点](@entry_id:172513)）。

让我们通过一个具体的例子来感受这一定理的力量 [@problem_id:1124551]。考虑[尖点形式](@entry_id:189096)空间 $S_2(\Gamma_0(11))$。这是一个一维空间，由一个唯一的归一化新形式 $f$ 张成。与 $f$ 对应的椭圆曲线是：
$$ E: y^2 + y = x^3 - x^2 $$
这条曲线的 conductor 正是 $11$。我们的任务是计算[赫克算子](@entry_id:181282) $T_3$ 作用于 $f$ 的[特征值](@entry_id:154894)。根据新形式的理论，这个[特征值](@entry_id:154894)就是 $f$ 的第三个[傅里叶系数](@entry_id:144886) $a_3$。模性定理告诉我们，我们可以通过计算 $\#E(\mathbb{F}_3)$ 来找到 $a_3$。

我们来数一下曲线 $E$ 在 $\mathbb{F}_3 = \{0, 1, 2\}$ 上的点。方程为 $y^2+y = x^3-x^2 \pmod 3$。
-   当 $x=0$ 时，方程为 $y^2+y=0 \implies y(y+1)=0$。解为 $y=0$ 和 $y=-1 \equiv 2 \pmod 3$。得到点 $(0,0)$ 和 $(0,2)$。
-   当 $x=1$ 时，方程为 $y^2+y=1-1=0$。解同样为 $y=0, 2$。得到点 $(1,0)$ 和 $(1,2)$。
-   当 $x=2$ 时，方程为 $y^2+y=2^3-2^2 = 8-4=4 \equiv 1 \pmod 3$。即 $y^2+y-1=0$。此[二次方程](@entry_id:163234)的[判别式](@entry_id:174614)为 $\Delta = 1^2 - 4(1)(-1) = 5 \equiv 2 \pmod 3$。由于 $2$ 在 $\mathbb{F}_3$ 中不是二次剩余，该方程无解。

因此，在 $\mathbb{F}_3$ 上共有 $2+2+0=4$ 个仿射点。加上[无穷远点](@entry_id:172513)，总点数为 $\#E(\mathbb{F}_3) = 4+1=5$。

现在我们可以计算 $a_3$：
$$ a_3 = p+1 - \#E(\mathbb{F}_p) = 3+1 - 5 = -1 $$
所以，[赫克算子](@entry_id:181282) $T_3$ 作用于新形式 $f$ 的[特征值](@entry_id:154894)为 $-1$。这个例子完美地展示了模性定理如何将一个抽象的谱论问题（计算赫克[特征值](@entry_id:154894)）转化为一个具体的、有限的计数问题（计算[椭圆曲线上的点数](@entry_id:634707)）。正是这一深刻的联系，最终为[费马大定理的证明](@entry_id:198073)铺平了道路，也彰显了模形式在数论核心的地位。