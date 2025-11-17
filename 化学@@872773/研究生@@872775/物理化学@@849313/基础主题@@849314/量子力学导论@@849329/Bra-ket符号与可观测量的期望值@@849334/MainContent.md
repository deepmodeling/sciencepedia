## 引言
[狄拉克符号](@entry_id:154811)（Bra-ket notation）与可观测量[期望值](@entry_id:153208)的计算是现代量子力学的基石，为描述微观世界的物理实在提供了一套严谨而优雅的数学语言。对于[物理化学](@entry_id:145220)及相关领域的研究生而言，掌握这套语言是理解和解决从分子结构到量子动力学等前沿问题的关键。然而，学生们常常面临将抽象的数学形式与具体的物理应用联系起来的挑战。本文旨在填补这一鸿沟，系统性地阐明这一核心理论框架，并展示其在解决实际问题中的强大威力。

本文分为三个核心部分。在“原理与机制”一章中，我们将深入探讨[狄拉克符号](@entry_id:154811)的数学结构，包括希尔伯特空间、态矢、自伴算符以及投影测量等基本概念，为后续讨论奠定坚实的基础。接下来，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些原理如何应用于[分子光谱学](@entry_id:148164)、[量子统计力学](@entry_id:140244)和[量子信息科学](@entry_id:150091)等多个领域，将抽象理论与可观测的实验现象紧密联系。最后，通过“动手实践”部分提供的一系列计算练习，读者将有机会亲手应用所学知识，深化对[高斯波包](@entry_id:151158)、[不确定性原理](@entry_id:141278)等核心概念的理解。通过这一结构化的学习路径，本文将引导读者不仅理解“是什么”，更掌握“如何用”，从而真正将[狄拉克符号](@entry_id:154811)与[期望值](@entry_id:153208)内化为强大的科研工具。

## 原理与机制

在本章中，我们将深入探讨[量子力学形式体系](@entry_id:198016)的数学核心：狄拉克（Dirac）的符号记法，即**[狄拉克符号](@entry_id:154811)**（bra-ket notation），以及如何利用它来描述物理可观测量的测量结果。我们将从基本原理出发，建立一套严谨的框架，用于理解[量子态](@entry_id:146142)、算符以及它们与物理实在之间的联系。这套语言不仅优雅简洁，更是现代[物理化学](@entry_id:145220)，从[分子光谱学](@entry_id:148164)到[量子信息科学](@entry_id:150091)等前沿领域不可或缺的分析工具。

### 希尔伯特空间中的态矢：[右矢](@entry_id:152965)与左矢

在量子力学中，一个孤立系统的状态由[复希尔伯特空间](@entry_id:185216) $\mathcal{H}$ 中的一个矢量来完备地描述。狄拉克引入了一种极其便利的记法，将这些态矢量表示为**[右矢](@entry_id:152965)**（ket），记作 $|\psi\rangle$。例如，一个分子的特定[振动](@entry_id:267781)状态或电子状态都可以用一个特定的[右矢](@entry_id:152965)来表示。

[希尔伯特空间](@entry_id:261193)是一个配备了[内积](@entry_id:158127)的完备[向量空间](@entry_id:151108)。为了处理[内积](@entry_id:158127)，我们需要引入[右矢](@entry_id:152965)的对偶——**左矢**（bra）。每一个[右矢](@entry_id:152965) $|\psi\rangle \in \mathcal{H}$ 都唯一对应一个其对偶空间 $\mathcal{H}^*$ 中的元素，记作 $\langle\psi|$。这个[对偶空间](@entry_id:146945)由作用于 $\mathcal{H}$ 的所有[连续线性泛函](@entry_id:262913)构成。左矢 $\langle\phi|$ 就是一个这样的泛函，它作用于一个[右矢](@entry_id:152965) $|\psi\rangle$ 上，产生一个复数。这个过程被记为**[内积](@entry_id:158127)**（inner product），写作 $\langle\phi|\psi\rangle$。

这种表示法的美妙之处在于它将泛函的作用优雅地写成了一个对称的形式。从定义上讲，由于左矢 $\langle\phi|$ 是一个**线性**泛函，[内积](@entry_id:158127)在其第二个参数（[右矢](@entry_id:152965)）上必须是线性的。这意味着对于任意复数标量 $\alpha_1, \alpha_2$ 和[右矢](@entry_id:152965) $|\psi_1\rangle, |\psi_2\rangle$，我们有：
$$
\langle\phi|(\alpha_1|\psi_1\rangle + \alpha_2|\psi_2\rangle) = \alpha_1\langle\phi|\psi_1\rangle + \alpha_2\langle\phi|\psi_2\rangle
$$
[复希尔伯特空间](@entry_id:185216)[内积](@entry_id:158127)的一个基本公理是**[共轭对称性](@entry_id:144131)**：
$$
\langle\phi|\psi\rangle = \langle\psi|\phi\rangle^*
$$
其中 $*$ 表示复共轭。利用这两个性质，我们可以推导出[内积](@entry_id:158127)在其第一个参数（左矢）上的行为。考虑 $\langle\alpha\phi|\psi\rangle$，其中 $\alpha$ 是一个复数。根据[共轭对称性](@entry_id:144131)，我们有 $\langle\alpha\phi|\psi\rangle = \langle\psi|\alpha\phi\rangle^*$。再利用[右矢](@entry_id:152965)的线性，我们得到 $\langle\psi|\alpha\phi\rangle = \alpha\langle\psi|\phi\rangle$。将其代回，可得：
$$
\langle\alpha\phi|\psi\rangle = (\alpha\langle\psi|\phi\rangle)^* = \alpha^*\langle\psi|\phi\rangle^* = \alpha^*\langle\phi|\psi\rangle
$$
这表明，[内积](@entry_id:158127)在其第一个参数（左矢）上是**[反线性](@entry_id:268590)**的（或称[共轭线性](@entry_id:268590)）。这种在一个参数上线性，在另一个参数上[反线性](@entry_id:268590)的形式在数学上被称为**[半双线性形式](@entry_id:154766)**（sesquilinear form）。

从[右矢](@entry_id:152965)到左矢的对应关系也遵循[反线性](@entry_id:268590)。如果我们有一个[右矢](@entry_id:152965) $\alpha|\psi\rangle$，其对应的左矢记为 $\langle\alpha\psi|$。这个左矢作用于任意[右矢](@entry_id:152965) $|\phi\rangle$ 的结果是 $\langle\alpha\psi|\phi\rangle = \alpha^*\langle\psi|\phi\rangle$。这意味着泛函 $\langle\alpha\psi|$ 等于泛函 $\langle\psi|$ 乘以标量 $\alpha^*$。因此，对应关系是：
$$
\text{若 } |\psi\rangle \longleftrightarrow \langle\psi| \text{，则 } \alpha|\psi\rangle \longleftrightarrow \alpha^*\langle\psi|
$$
这一规则也写作 $\langle\alpha\psi| = \alpha^*\langle\psi|$ [@problem_id:2625866]。

如果我们在一组[标准正交基](@entry_id:147779) $\{|e_j\rangle\}$（即 $\langle e_j|e_k\rangle = \delta_{jk}$）中展开一个[右矢](@entry_id:152965) $|\psi\rangle = \sum_j c_j |e_j\rangle$，那么利用[反线性](@entry_id:268590)规则，其对应的左矢就是：
$$
\langle\psi| = \left( \sum_j c_j |e_j\rangle \right)^\dagger = \sum_j c_j^* \langle e_j|
$$
这里的 $\dagger$ 符号表示**厄米伴随**（Hermitian adjoint），它将[右矢](@entry_id:152965)映射到左矢，并将标量系数取[复共轭](@entry_id:174690)。

### 物理态的表示与概率诠释

量子力学的一个核心假设是，一个物理态并非由[希尔伯特空间](@entry_id:261193)中一个唯一的[右矢](@entry_id:152965)表示，而是由一整条**射线**（ray）所代表。一条射线是指由一个非零[右矢](@entry_id:152965) $|\psi\rangle$ 生成的所有非零复数倍的[右矢](@entry_id:152965)集合 $\{c|\psi\rangle \mid c \in \mathbb{C}, c \neq 0\}$。这意味着，如果两个[右矢](@entry_id:152965) $|\phi\rangle$ 和 $|\psi\rangle$ 仅相差一个非零复数因子，即 $|\phi\rangle = c|\psi\rangle$，那么它们描述的是完全相同的物理状态 [@problem_id:2625879]。

我们可以从物理测量的角度来理解这一点。量子力学中的所有物理预言，如测量结果的概率和[可观测量](@entry_id:267133)的[期望值](@entry_id:153208)，都是通过某种形式的比值来计算的，这使得它们在态矢的整体缩放下保持不变。例如，一个[可观测量](@entry_id:267133) $\hat{A}$ 的[期望值](@entry_id:153208)由下式给出：
$$
\langle \hat{A} \rangle_\psi = \frac{\langle\psi|\hat{A}|\psi\rangle}{\langle\psi|\psi\rangle}
$$
如果我们用 $|\phi\rangle = c|\psi\rangle$ 替换 $|\psi\rangle$，则：
$$
\langle \hat{A} \rangle_\phi = \frac{\langle c\psi|\hat{A}|c\psi\rangle}{\langle c\psi|c\psi\rangle} = \frac{c^*c\langle\psi|\hat{A}|\psi\rangle}{c^*c\langle\psi|\psi\rangle} = \frac{|c|^2\langle\psi|\hat{A}|\psi\rangle}{|c|^2\langle\psi|\psi\rangle} = \frac{\langle\psi|\hat{A}|\psi\rangle}{\langle\psi|\psi\rangle} = \langle \hat{A} \rangle_\psi
$$
可见，所有可观测的物理量都保持不变。描述一个纯态的更严谨的方式是使用**[密度算符](@entry_id:138151)**（density operator），对于[纯态](@entry_id:141688) $|\psi\rangle$，其[密度算符](@entry_id:138151)为 $\hat{\rho}_\psi = \frac{|\psi\rangle\langle\psi|}{\langle\psi|\psi\rangle}$。这个算符对于同一射线上的所有[右矢](@entry_id:152965)都是唯一的 [@problem_id:2625879]。

尽管任何非零[右矢](@entry_id:152965)都可以描述状态，但在实际计算中，我们通常会利用这种标度自由度来简化表达式。标准约定是选择射线上范数为1的那个[右矢](@entry_id:152965)来代表物理状态。这个约定被称为**[归一化条件](@entry_id:156486)**：
$$
\langle\psi|\psi\rangle = 1
$$
这个条件之所以至关重要，是因为它与量子力学的概率解释——**[玻恩定则](@entry_id:154470)**（Born's rule）——紧密相连。考虑一个[可观测量](@entry_id:267133)，其对应的算符拥有一组完备的标准正交本征矢 $\{|a_n\rangle\}$。这意味着这些[基矢](@entry_id:199546)满足**[完备性关系](@entry_id:139077)**（completeness relation），或称恒等算符分解：$\sum_n |a_n\rangle\langle a_n| = \hat{I}$。根据[玻恩定则](@entry_id:154470)，在态 $|\psi\rangle$ 中测量该可观测量得到结果 $a_n$ 的概率 $P(a_n)$ 是 $|\langle a_n|\psi\rangle|^2$。所有可能结果的概率之和必须为1。我们可以通过插入[完备性关系](@entry_id:139077)来验证这一点：
$$
\sum_n P(a_n) = \sum_n |\langle a_n|\psi\rangle|^2 = \sum_n \langle\psi|a_n\rangle\langle a_n|\psi\rangle = \left\langle\psi\left|\left(\sum_n|a_n\rangle\langle a_n|\right)\right|\psi\right\rangle = \langle\psi|\hat{I}|\psi\rangle = \langle\psi|\psi\rangle
$$
因此，为了使 $|\langle a_n|\psi\rangle|^2$ 能被直接解释为概率，我们必须要求总概率为1，即 $\langle\psi|\psi\rangle = 1$。对于连续谱的情况，例如位置表象，[归一化条件](@entry_id:156486)写作 $\int |\psi(x)|^2 dx = 1$，其中 $\psi(x) = \langle x|\psi\rangle$ 是位置[波函数](@entry_id:147440)。这确保了 $|\psi(x)|^2$ 是一个合法的概率密度函数 [@problem_id:2625832]。

### 叠加原理与量子干涉

[量子态](@entry_id:146142)的[线性组合](@entry_id:154743)，即**叠加**（superposition），是量子力学区别于经典物理的核心特征之一。如果 $|\psi\rangle$ 和 $|\phi\rangle$ 是系统可能存在的两个状态，那么它们的任意线性组合 $|\chi\rangle = \alpha|\psi\rangle + \beta|\phi\rangle$ (其中 $\alpha, \beta$ 是复数) 也是一个可能的状态。

叠加的物理意义体现在**量子干涉**（quantum interference）上。考虑一个双路径[干涉仪](@entry_id:261784)的例子，一个分子可以经过路径1（状态 $|\psi\rangle$）或路径2（状态 $|\phi\rangle$）。出射态是这两个路径态的[相干叠加](@entry_id:170209) $|\chi\rangle = \alpha|\psi\rangle + \beta|\phi\rangle$，其中 $|\alpha|^2$ 和 $|\beta|^2$ 分别代表粒子走路径1和路径2的概率。假设 $|\psi\rangle$ 和 $|\phi\rangle$ 是正交的（$\langle\psi|\phi\rangle=0$）且已归一化，则为使 $|\chi\rangle$ 也归一化，需满足 $|\alpha|^2 + |\beta|^2 = 1$。

在探测屏上的某一点 $x_0$ 处探测到这个分子的概率是多少？这个测量由[投影算符](@entry_id:154142) $\hat{\Pi}_{x_0} = |x_0\rangle\langle x_0|$ 描述。根据[玻恩定则](@entry_id:154470)，概率为 $P(x_0) = \langle\chi|\hat{\Pi}_{x_0}|\chi\rangle = |\langle x_0|\chi\rangle|^2$。我们将叠加态代入：
$$
\langle x_0|\chi\rangle = \langle x_0|(\alpha|\psi\rangle + \beta|\phi\rangle) = \alpha\langle x_0|\psi\rangle + \beta\langle x_0|\phi\rangle
$$
因此，探测概率为：
$$
P(x_0) = |\alpha\langle x_0|\psi\rangle + \beta\langle x_0|\phi\rangle|^2 = |\alpha|^2|\langle x_0|\psi\rangle|^2 + |\beta|^2|\langle x_0|\phi\rangle|^2 + 2\mathrm{Re}(\alpha^*\beta\langle\psi|x_0\rangle\langle x_0|\phi\rangle)
$$
这个表达式清楚地展示了量子力学的核心特征 [@problem_id:2625868]。前两项是经典概率的加和：粒子通过路径1到达 $x_0$ 的概率加上通过路径2到达 $x_0$ 的概率。第三项是**干涉项**，它依赖于系数 $\alpha$ 和 $\beta$ 之间的**相对相位**。如果我们令 $\alpha = |\alpha|e^{i\theta_\alpha}$ 和 $\beta = |\beta|e^{i\theta_\beta}$，干涉项就依赖于 $\exp(i(\theta_\beta - \theta_\alpha))$。通过改变这个[相对相位](@entry_id:148120)（例如，通过改变其中一条路径的光程），我们可以连续地调控探测屏上某一点的概率，使其在相长干涉（最大值）和[相消干涉](@entry_id:170966)（最小值）之间变化 [@problem_id:2625868]。这正是[量子叠加](@entry_id:137914)态的可操作性标志，也是[量子计算](@entry_id:142712)等技术的基础。

### 可观测量与自伴算符

物理世界中的[可观测量](@entry_id:267133)，如能量、动量、位置或偶极矩，在量子力学中由[希尔伯特空间](@entry_id:261193)上的**自伴算符**（self-adjoint operators）来表示。一个算符 $\hat{A}$ 被称为自伴的，如果它等于其自身的厄米伴随 $\hat{A}^\dagger$，并且它们的定义域相同，即 $\hat{A} = \hat{A}^\dagger$ 且 $\mathcal{D}(\hat{A}) = \mathcal{D}(\hat{A}^\dagger)$。

要求[可观测量](@entry_id:267133)由自伴算符表示，背后有深刻的物理和数学原因：

1.  **[期望值](@entry_id:153208)为实数**：任何物理量的测量值都是实数，因此其[期望值](@entry_id:153208) $\langle\hat{A}\rangle = \langle\psi|\hat{A}|\psi\rangle$ 对于任意态 $|\psi\rangle$ 都必须是实数。如果[期望值](@entry_id:153208)为实数，则 $\langle\psi|\hat{A}|\psi\rangle = \langle\psi|\hat{A}|\psi\rangle^* = \langle\hat{A}\psi|\psi\rangle$。这个性质定义了所谓的**对称算符**（symmetric operator）。对于定义在整个[希尔伯特空间](@entry_id:261193)上的有界算符（例如在[有限维空间](@entry_id:151571)中），对称性等价于自伴性。然而，在无穷维空间中，许多重要的算符（如动量和位置算符）是无界的，它们的定义域不是整个希尔伯特空间。在这种情况下，自伴性是一个比对称性更强的条件 [@problem_id:2625851]。

2.  **[谱定理](@entry_id:136620)的保证**：**谱定理**（spectral theorem）是量子力学的数学基石，它确保了[可观测量](@entry_id:267133)算符具有我们期望的物理属性。该定理断言，只有自伴算符才保证拥有一套完备的、对应于实数谱（即可能的测量值）的本征态（或更一般的投影值测量）。一个仅仅是对称的算符可能没有这样良好的谱结构 [@problem_id:2625851]。

    谱定理的普适形式是使用**投影值测量**（Projection-Valued Measure, PVM）来表述的。它指出，对于任意自伴算符 $\hat{A}$，存在一个唯一的PVM $\hat{P}$，它将实数轴 $\mathbb{R}$ 上的每个（波莱尔）[子集](@entry_id:261956) $\Delta$ 映射到一个[投影算符](@entry_id:154142) $\hat{P}(\Delta)$，使得：
    $$
    \hat{A} = \int_{\mathbb{R}} a \, d\hat{P}(a)
    $$
    这个PVM $\hat{P}$ 满足 $\hat{P}(\mathbb{R})=\hat{I}$ 和 $\hat{P}(\Delta_1)\hat{P}(\Delta_2) = \hat{P}(\Delta_1 \cap \Delta_2)$ 等性质。在态 $|\psi\rangle$ 中，测量 $\hat{A}$ 的结果落在集合 $\Delta$ 内的概率由[玻恩定则](@entry_id:154470)的推广形式给出：$\mu_\psi(\Delta) = \langle\psi|\hat{P}(\Delta)|\psi\rangle$。而 $\hat{A}$ 的[期望值](@entry_id:153208)就是这个[概率分布](@entry_id:146404)的一阶矩：$\langle\hat{A}\rangle = \int_{\mathbb{R}} a \, d\mu_\psi(a)$ [@problem_id:2625828]。

    对于具有[离散谱](@entry_id:150970)的简单情况，谱分解简化为我们更熟悉的形式：
    $$
    \hat{A} = \sum_n a_n \hat{P}_n = \sum_n a_n |a_n\rangle\langle a_n|
    $$
    其中 $a_n$ 是[本征值](@entry_id:154894)，$\hat{P}_n = |a_n\rangle\langle a_n|$ 是到对应[本征空间](@entry_id:147356)的投影算符（此处为非简并情况）[@problem_id:2625828]。

3.  **时间演化的生成元**：根据**[斯通定理](@entry_id:262301)**（Stone's theorem），一个系统的[幺正时间演化](@entry_id:192535)算符群 $U(t) = \exp(-i\hat{H}t/\hbar)$ 存在且性质良好，当且仅当其生成元——[哈密顿算符](@entry_id:144286) $\hat{H}$——是自伴的。这保证了量子动力学是可逆的且[概率守恒](@entry_id:149166) [@problem_id:2625851]。

### [期望值](@entry_id:153208)的计算与投影测量

一个可观测量 $\hat{A}$ 在归一化态 $|\psi\rangle$ 中的**[期望值](@entry_id:153208)**（expectation value）定义为 $\langle\hat{A}\rangle_\psi = \langle\psi|\hat{A}|\psi\rangle$。利用[基的完备性](@entry_id:196285)关系，我们可以方便地进行计算。在一个离散的标准正交基 $\{|e_j\rangle\}$ 中，我们可以通过在算符两侧插入恒等算符 $\hat{I} = \sum_j |e_j\rangle\langle e_j|$ 来计算：
$$
\langle\hat{A}\rangle_\psi = \langle\psi|\hat{I}\hat{A}\hat{I}|\psi\rangle = \left\langle\psi\left|\left(\sum_j |e_j\rangle\langle e_j|\right)\hat{A}\left(\sum_k |e_k\rangle\langle e_k|\right)\right|\psi\right\rangle
$$
整理后得到：
$$
\langle\hat{A}\rangle_\psi = \sum_{j,k} \langle\psi|e_j\rangle \langle e_j|\hat{A}|e_k\rangle \langle e_k|\psi\rangle
$$
如果我们记态 $|\psi\rangle$ 在该基下的分量为 $c_k = \langle e_k|\psi\rangle$，算符 $\hat{A}$ 的[矩阵元](@entry_id:186505)为 $A_{jk} = \langle e_j|\hat{A}|e_k\rangle$，那么上式就变成了矩阵形式：
$$
\langle\hat{A}\rangle_\psi = \sum_{j,k} c_j^* A_{jk} c_k
$$
这等价于矩阵乘积 $\mathbf{c}^\dagger\mathbf{A}\mathbf{c}$，其中 $\mathbf{c}$ 是由系数 $c_k$ 构成的列向量，$\mathbf{A}$ 是由 $A_{jk}$ 构成的矩阵 [@problem_id:2625856]。

当我们对系统进行一次理想的**投影测量**（projective measurement）时，不仅会得到一个测量结果，系统的状态也会发生不可逆的改变，即**[波函数](@entry_id:147440)塌缩**（wave function collapse）。

假设我们测量可观测量 $\hat{A}$，其[本征值](@entry_id:154894) $a_n$ 可能是简并的，简并度为 $g_n$。对应于[本征值](@entry_id:154894) $a_n$ 的本征[子空间](@entry_id:150286)由一组[标准正交基](@entry_id:147779) $\{|a_n, j\rangle\}_{j=1}^{g_n}$ 张成。到这个[子空间](@entry_id:150286)的投影算符为 $\hat{P}_n = \sum_{j=1}^{g_n} |a_n, j\rangle\langle a_n, j|$。

根据[量子测量假设](@entry_id:150143)：

1.  **概率**：测量得到结果 $a_n$ 的概率为 $\mathcal{P}(a_n) = \langle\psi|\hat{P}_n|\psi\rangle = \|\hat{P}_n|\psi\rangle\|^2$。

2.  **塌缩**：如果测量结果为 $a_n$，系统的状态会瞬间塌缩到其原始态在 $a_n$ 本征[子空间](@entry_id:150286)上的归一化投影：
    $$
    |\psi_{\text{post-measurement}}\rangle = \frac{\hat{P}_n|\psi\rangle}{\sqrt{\langle\psi|\hat{P}_n|\psi\rangle}}
    $$
    这个塌缩过程是量子力学非[幺正演化](@entry_id:145020)的来源。在[密度算符](@entry_id:138151)的语言中，这一过程由吕德斯定则（Lüders' rule）描述，初始态为 $\hat{\rho} = |\psi\rangle\langle\psi|$，测量后的态为 $\hat{\rho}' = \frac{\hat{P}_n\hat{\rho}\hat{P}_n}{\mathrm{Tr}(\hat{\rho}\hat{P}_n)}$ [@problem_id:2625855]。

### [连续谱](@entry_id:155477)与严格的数学框架

许多重要的物理量，如位置和动量，其算符具有[连续谱](@entry_id:155477)。处理这种情况需要对[狄拉克符号](@entry_id:154811)记法进行扩展。以一维空间中的位置算符 $\hat{x}$ 为例，它的“本征矢” $|x\rangle$ 对应于粒子精确位于位置 $x$ 的状态。这些 $|x\rangle$ 并不属于希尔伯特空间 $\mathcal{H} = L^2(\mathbb{R})$，因为它们的“[波函数](@entry_id:147440)”——狄拉克 $\delta$ 函数——不是平方可积的。

尽管如此，我们可以将它们作为一套**广义[基矢](@entry_id:199546)**（generalized basis）来使用，其代数关系需要在[分布](@entry_id:182848)（distribution）的意义上理解 [@problem_id:2625842]：

1.  **广义正交性**：$\langle x|x'\rangle = \delta(x-x')$
2.  **[完备性关系](@entry_id:139077)**：$\int_{\mathbb{R}} |x\rangle\langle x| dx = \hat{I}$

这两条规则是连接抽象的狄拉克 formalism 和具体的[波动力学](@entry_id:166256)的桥梁。例如，任意两个态 $|\phi\rangle$ 和 $|\psi\rangle$ 的[内积](@entry_id:158127)可以通过插入[完备性关系](@entry_id:139077)得到：
$$
\langle\phi|\psi\rangle = \langle\phi|\hat{I}|\psi\rangle = \int \langle\phi|x\rangle\langle x|\psi\rangle dx = \int \phi^*(x)\psi(x) dx
$$
其中我们定义了[波函数](@entry_id:147440) $\psi(x) = \langle x|\psi\rangle$。类似地，任意算符 $\hat{A}$ 的[期望值](@entry_id:153208)可以表示为：
$$
\langle\psi|\hat{A}|\psi\rangle = \iint \langle\psi|x\rangle\langle x|\hat{A}|x'\rangle\langle x'|\psi\rangle dx dx' = \iint \psi^*(x) A(x,x') \psi(x') dx dx'
$$
其中 $A(x,x') = \langle x|\hat{A}|x'\rangle$ 被称为算符 $\hat{A}$ 的积分核 [@problem_id:2625842]。

这种包含广义矢量的 formalism 的严格数学基础是**[装备希尔伯特空间](@entry_id:141353)**（Rigged Hilbert Space, RHS），也称为[盖尔范德三元组](@entry_id:141353)（Gelfand triple）。其思想是构造一个三元组 $\Phi \subset \mathcal{H} \subset \Phi^\times$ [@problem_id:2625843]。

*   $\mathcal{H}$ 是我们熟悉的希尔伯特空间（例如 $L^2(\mathbb{R})$）。
*   $\Phi$ 是 $\mathcal H$ 中的一个[稠密子空间](@entry_id:261392)，由性质非常良好的“测试函数”组成（例如，由无限可微且快速衰减的函数构成的[施瓦茨空间](@entry_id:266248) $\mathcal{S}(\mathbb{R})$）。物理上合理的态矢通常属于这个空间，因为它们能量有限，且在空间中局部化。
*   $\Phi^\times$ 是 $\Phi$ 的[反线性](@entry_id:268590)对偶空间，由作用于 $\Phi$ 的连续反线性泛函构成。

在这个框架中，像 $|x\rangle$ 和 $|p\rangle$ 这样的广义[右矢](@entry_id:152965)被严谨地定义为 $\Phi^\times$ 中的元素。表达式 $\langle x|\psi\rangle = \psi(x)$ 不再仅仅是符号，而是泛函 $|x\rangle$ 对测试函数 $|\psi\rangle \in \Phi$ 的求值操作。选择 $\Phi$ 为[施瓦茨空间](@entry_id:266248) $\mathcal{S}(\mathbb{R})$ 尤其方便，因为位置算符 $\hat{x}$ 和动量算符 $\hat{p}$ 都是 $\mathcal{S}(\mathbb{R})$到自身的[连续映射](@entry_id:153855)，并且[傅里叶变换](@entry_id:142120)也是其上的[自同构](@entry_id:155390)，这使得在位置表象和[动量表象](@entry_id:156131)之间切换变得自然而严谨 [@problem_id:2625843]。这个数学结构不仅为狄拉克的直观记法提供了坚实的基础，也确保了在处理无界算符和连续谱时，物理学家们常用的数学操作（如[分部积分](@entry_id:136350)）是合法且可靠的。