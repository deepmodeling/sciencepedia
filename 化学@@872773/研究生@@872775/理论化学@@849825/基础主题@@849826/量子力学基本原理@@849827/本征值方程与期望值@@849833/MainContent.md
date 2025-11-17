## 引言
在量子力学的宏伟框架中，[本征值方程](@entry_id:192306)与[期望值](@entry_id:153208)是两个最基本也最强大的概念，它们共同构成了连接抽象数学形式与可观测物理现实的桥梁。深刻理解这两个概念是掌握量子理论、并将其应用于物理、化学、[材料科学](@entry_id:152226)等多个领域的必经之路。然而，初学者常常困惑于它们的抽象定义与复杂的物理诠释之间的鸿沟。本文旨在系统性地弥合这一差距，引领读者从基本原理走向前沿应用。

在接下来的内容中，我们将分三步深入探索这一主题。首先，在“**原理和机制**”一章中，我们将奠定坚实的理论基础，从[本征值方程](@entry_id:192306)和[期望值](@entry_id:153208)的数学定义出发，阐明它们在[量子测量](@entry_id:272490)理论、不确定性原理以及[对称性分析](@entry_id:174795)中的深刻物理内涵，并探讨其严格的数学基础。随后，在“**应用与交叉学科联系**”一章，我们将展示这些原理的强大威力，通过一系列横跨原子分子结构、[光谱学](@entry_id:141940)、[计算化学](@entry_id:143039)和[统计力](@entry_id:194984)学的实例，揭示它们如何成为预测分子性质、解释[化学反应](@entry_id:146973)和理解复杂系统行为的统一语言。最后，在“**动手实践**”部分，我们提供了一系列精心设计的计算问题，旨在将理论知识转化为解决问题的实践技能，帮助读者亲手实现从抽象算符到具体数值的跨越。

## 原理和机制

在[量子化学](@entry_id:140193)的理论框架中，物理可观测量与作用于系统希尔伯特空间上的线性算符相关联。理解这些算符的性质，特别是它们的[本征值方程](@entry_id:192306)和[期望值](@entry_id:153208)，是连接理论形式与实验测量的核心。本章将系统地阐述这些基本原理，从它们的数学定义开始，逐步深入到它们在量子力学测量理论、近似方法和[对称性分析](@entry_id:174795)中的深刻含义。

### 基本定义：[本征值方程](@entry_id:192306)与[期望值](@entry_id:153208)

量子力学中的一个核心假设是，每一个[物理可观测量](@entry_id:154692)（如能量、动量或角动量）都由一个线性算符 $\hat{A}$ 来表示。当一个系统的[量子态](@entry_id:146142) $|\psi\rangle$ 恰好是算符 $\hat{A}$ 的一个**本征态**（eigenstate）时，对该可观测量的测量将确定地得到一个特定的值，该值被称为**[本征值](@entry_id:154894)**（eigenvalue）。这种特殊关系由**[本征值方程](@entry_id:192306)**（eigenvalue equation）描述：

$$
\hat{A}|\psi\rangle = a|\psi\rangle
$$

这里，$|\psi\rangle$ 是非零的本征态，$a$ 是一个标量，即对应的[本征值](@entry_id:154894)。对于代表物理可观测量的算符，一个至关重要的要求是它们必须是**[厄米算符](@entry_id:153410)**（Hermitian operators），这意味着算符等于其自身的[厄米共轭](@entry_id:191215)，即 $\hat{A} = \hat{A}^\dagger$。这一性质保证了所有的[本征值](@entry_id:154894) $a$ 都是实数，这与它们代表可测量的物理量这一事实相符。

然而，一个量子系统并非总处于某个特定算符的本征态。对于一个处于任意归一化态 $|\psi\rangle$（即 $\langle\psi|\psi\rangle = 1$）的系统，可观测量 $A$ 的**[期望值](@entry_id:153208)**（expectation value）被定义为：

$$
\langle \hat{A} \rangle = \langle\psi|\hat{A}|\psi\rangle
$$

这个量代表了在大量相同制备的系统上重复测量 $A$ 所得到的平均值。

这两个概念之间的关系在一个特殊情况下变得尤为简洁。如果态 $|\psi\rangle$ 本身就是一个归一化的本征态，其[本征值](@entry_id:154894)为 $\lambda$，那么根据[本征值方程](@entry_id:192306) $\hat{H}|\psi\rangle = \lambda|\psi\rangle$，我们可以直接计算其[期望值](@entry_id:153208) [@problem_id:16681]：

$$
\langle \hat{H} \rangle = \langle\psi|\hat{H}|\psi\rangle = \langle\psi|(\lambda|\psi\rangle) = \lambda\langle\psi|\psi\rangle = \lambda
$$

这个结果直观地表明，如果系统确定地处于一个本征态，那么对相应可观测量的测量平均值自然就是该[本征值](@entry_id:154894)。然而，在更一般的情况下，态与[期望值](@entry_id:153208)之间的关系则更为微妙。

### 物理诠释：测量、叠加与不确定性

量子力学的测量假设阐明了[本征值](@entry_id:154894)与[期望值](@entry_id:153208)之间的关键区别。对于一个处于一般叠加态 $|\psi\rangle$ 的系统，对[可观测量](@entry_id:267133) $A$ 的单次测量结果**只能是**算符 $\hat{A}$ 的某个[本征值](@entry_id:154894)。[期望值](@entry_id:153208) $\langle \hat{A} \rangle$ 是这些可能结果的统计平均值，它本身不一定是一个可能的单次测量结果。

考虑一个一般的归一化态 $|\psi\rangle$，它可以展开为算符 $\hat{A}$ 的完备正交本征态 $\{|\phi_n\rangle\}$ 的线性叠加：

$$
|\psi\rangle = \sum_n c_n |\phi_n\rangle
$$

其中 $\hat{A}|\phi_n\rangle = a_n |\phi_n\rangle$，且展开系数 $c_n = \langle\phi_n|\psi\rangle$。根据[玻恩定则](@entry_id:154470)（Born rule），在态 $|\psi\rangle$ 中测量 $A$ 得到结果 $a_n$ 的概率为 $P(a_n) = |c_n|^2 = |\langle\phi_n|\psi\rangle|^2$。由于态是归一化的，所有概率之和为1，即 $\sum_n |c_n|^2 = 1$。

此时，[期望值](@entry_id:153208)可以表示为所有可能测量结果与其相应概率的加权和：

$$
\langle \hat{A} \rangle = \langle\psi|\hat{A}|\psi\rangle = \left(\sum_m c_m^* \langle\phi_m|\right) \hat{A} \left(\sum_n c_n |\phi_n\rangle\right) = \sum_{m,n} c_m^* c_n \langle\phi_m|\hat{A}|\phi_n\rangle = \sum_n |c_n|^2 a_n
$$

这个表达式清晰地展示了[期望值](@entry_id:153208)的统计本质。

一个经典的例子可以阐明这一点 [@problem_id:2769850]。假设一个双能级系统，其某个[可观测量](@entry_id:267133)由算符 $\hat{A}$ 表示，它有两个[本征态](@entry_id:149904) $|\phi_+\rangle$ 和 $|\phi_-\rangle$，对应的[本征值](@entry_id:154894)为 $+a_0$ 和 $-a_0$。如果系统被制备在叠加态 $|\psi\rangle=\sqrt{2/3}\,|\phi_{+}\rangle+e^{i\theta}\sqrt{1/3}\,|\phi_{-}\rangle$，那么：

1.  **可能的测量结果**：任何单次测量 $A$ 的结果必然是 $+a_0$ 或 $-a_0$。任何介于两者之间的值，例如 $0$ 或 $a_0/2$，都不可能作为单次测量的输出。
2.  **测量概率**：测量到 $+a_0$ 的概率是 $|\langle\phi_+|\psi\rangle|^2 = (\sqrt{2/3})^2 = 2/3$。测量到 $-a_0$ 的概率是 $|\langle\phi_-|\psi\rangle|^2 = |e^{i\theta}\sqrt{1/3}|^2 = 1/3$。注意，这些概率与相位因子 $\theta$ 无关。
3.  **[期望值](@entry_id:153208)**：该可观测量的[期望值](@entry_id:153208)是 $\langle \hat{A} \rangle = (+a_0)P(+a_0) + (-a_0)P(-a_0) = a_0(2/3) - a_0(1/3) = a_0/3$。这个平均值 $a_0/3$ 本身并不是一个可能的单次测量结果。
4.  **测量与态塌缩**：如果在一次测量中得到结果 $+a_0$，这并不意味着系统在测量前就处于 $|\phi_+\rangle$ 态。它只说明了初始态 $|\psi\rangle$ 在 $|\phi_+\rangle$ 上有非零的投影。根据测量假设，测量行为本身使[波函数](@entry_id:147440)“塌缩”到了与测量结果对应的本征态，即测量后的态变为 $|\phi_+\rangle$。

当两个算符不对易（non-commuting）时，即它们的对易子 $[\hat{A}, \hat{B}] = \hat{A}\hat{B} - \hat{B}\hat{A} \neq 0$ 时，这意味着不存在一个完备的共同本征态基。因此，一个算符的[本征态](@entry_id:149904)通常是另一个算符的叠加态。这直接导致了不确定性原理：一个系统无法同时对两个不对易的[可观测量](@entry_id:267133)拥有确定的值。

一个典型的例子是自旋-$1/2$系统中的泡利算符 [@problem_id:2769990]。在 $\hat{\sigma}_z$ 的本征基 $\{|+\rangle_z, |-\rangle_z\}$ 中，其中 $|+\rangle_z = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ 且 $|-\rangle_z = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$，$\hat{\sigma}_z$ 和 $\hat{\sigma}_x$ 的[矩阵表示](@entry_id:146025)为：
$$
\hat{\sigma}_z = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}, \qquad \hat{\sigma}_x = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}
$$
$\hat{\sigma}_z$ 的[本征值](@entry_id:154894)显然是 $\pm 1$。现在，我们在 $\hat{\sigma}_z$ 的一个[本征态](@entry_id:149904)，例如 $|+\rangle_z$，中计算 $\hat{\sigma}_x$ 的[期望值](@entry_id:153208)：
$$
\langle \hat{\sigma}_x \rangle_+ = \langle +|_z \hat{\sigma}_x |+\rangle_z = \begin{pmatrix} 1  0 \end{pmatrix} \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix} \begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} 1  0 \end{pmatrix} \begin{pmatrix} 0 \\ 1 \end{pmatrix} = 0
$$
同样地，在 $|-\rangle_z$ 态中，$\langle \hat{\sigma}_x \rangle_- = 0$。$\hat{\sigma}_x$ 的[本征值](@entry_id:154894)为 $\pm 1$。计算得到的[期望值](@entry_id:153208)为0，它不是任何一个可能的测量结果，这表明在 $\hat{\sigma}_z$ 的[本征态](@entry_id:149904)中，$\sigma_x$ 的值是完全不确定的（测量得到+1和-1的概率均为1/2）。这正是算符不对易性 $[\hat{\sigma}_z, \hat{\sigma}_x] = 2i\hat{\sigma}_y \neq 0$ 的直接物理后果。

[角动量算符](@entry_id:153013)提供了另一个深刻的例子 [@problem_id:2769865]。其笛卡尔分量满足对易关系 $[L_i, L_j] = i\hbar\epsilon_{ijk}L_k$。由于任意两个不同的分量（如 $L_x, L_y$）都不对易，它们不能被同时确定。然而，总角动量平方算符 $L^2 = L_x^2 + L_y^2 + L_z^2$ 与任何一个分量都对易，例如 $[L^2, L_z] = 0$。这使得我们可以找到 $L^2$ 和 $L_z$ 的共同本征态，记为 $|l, m\rangle$。

在这样一个态中，$L_z$ 的[期望值](@entry_id:153208)是确定的：$\langle L_z \rangle = \langle l, m|L_z|l, m\rangle = \hbar m$。而对于 $L_x$ 和 $L_y$，它们的[期望值](@entry_id:153208)必然为零。这可以通过对称性参数或更严格的代数方法证明。例如，考虑对易子 $[L_y, L_z] = i\hbar L_x$ 的[期望值](@entry_id:153208)：
$$
\langle [L_y, L_z] \rangle = \langle l,m|(L_yL_z - L_zL_y)|l,m\rangle = \langle l,m|L_y(\hbar m)|l,m\rangle - \langle l,m|(\hbar m)L_y|l,m\rangle = 0
$$
另一方面，$\langle [L_y, L_z] \rangle = \langle i\hbar L_x \rangle = i\hbar \langle L_x \rangle$。因此，我们必须有 $\langle L_x \rangle = 0$。同理可得 $\langle L_y \rangle = 0$。

更有趣的是，对于算符的平方，$L_z^2$ 的[期望值](@entry_id:153208)也是确定的：$\langle L_z^2 \rangle = \hbar^2 m^2$。而对于 $\langle L_x^2 \rangle$ 和 $\langle L_y^2 \rangle$，我们可以利用 $L^2$ 的[期望值](@entry_id:153208)来求解：
$$
\langle L^2 \rangle = \langle L_x^2 \rangle + \langle L_y^2 \rangle + \langle L_z^2 \rangle
$$
$$
\hbar^2 l(l+1) = \langle L_x^2 \rangle + \langle L_y^2 \rangle + \hbar^2 m^2
$$
由于态 $|l, m\rangle$ 对于绕 z 轴的旋转具有对称性（仅产生一个相位因子），$x$ 和 $y$ 方向在物理上是等价的。因此，我们预期 $\langle L_x^2 \rangle = \langle L_y^2 \rangle$。结合上式，我们得到：
$$
\langle L_x^2 \rangle = \langle L_y^2 \rangle = \frac{1}{2} \hbar^2 [l(l+1) - m^2]
$$
这些非零的[期望值](@entry_id:153208)（[方差](@entry_id:200758)）反映了在 $|l,m\rangle$ 态中 $L_x$ 和 $L_y$ 的值是不确定的。这些例子展示了[期望值](@entry_id:153208)计算如何揭示由算符代数和系统对称性所支配的基本物理规律。

### 应用与高级原理

#### [变分原理](@entry_id:198028)

[期望值](@entry_id:153208)的一个最重要应用是在**[变分原理](@entry_id:198028)**（variational principle）中，这是[量子化学](@entry_id:140193)中用于近似求解复杂系统基态能量的基石。[变分原理](@entry_id:198028)指出，对于一个由[哈密顿算符](@entry_id:144286) $\hat{H}$ 描述的系统，其[基态能量](@entry_id:263704)为 $E_0$，那么对于任何一个归一化的**试探波函数**（trial wavefunction）$|\psi\rangle$，其[能量期望值](@entry_id:174035) $\langle E \rangle = \langle\psi|\hat{H}|\psi\rangle$ 总是[基态能量](@entry_id:263704)的一个[上界](@entry_id:274738)：

$$
\langle E \rangle \ge E_0
$$

这个强大定理的证明，本质上依赖于[哈密顿算符](@entry_id:144286)本征态的完备性 [@problem_id:2144180] [@problem_id:2769946]。设 $\hat{H}$ 的[精确本征态](@entry_id:138620)为 $\{|n\rangle\}$，对应的[本征值](@entry_id:154894)为 $\{E_n\}$，且 $E_0 \le E_1 \le E_2 \le \dots$。由于 $\{|n\rangle\}$ 构成一个完备集，任何归一化的[试探函数](@entry_id:756165) $|\psi\rangle$ 都可以展开为：

$$
|\psi\rangle = \sum_n c_n |n\rangle, \quad \text{with} \quad \sum_n |c_n|^2 = 1
$$

其[能量期望值](@entry_id:174035)为：
$$
\langle\psi|\hat{H}|\psi\rangle = \sum_n |c_n|^2 E_n
$$
由于对于所有的 $n$ 都有 $E_n \ge E_0$，我们可以得到：
$$
\sum_n |c_n|^2 E_n \ge \sum_n |c_n|^2 E_0 = E_0 \left(\sum_n |c_n|^2\right) = E_0
$$
等号成立的唯一条件是 $|\psi\rangle$ 仅由[基态](@entry_id:150928)本征函数构成，即 $|\psi\rangle$ 本身就是（或属于）[基态](@entry_id:150928)。

在实践中，我们构造一个依赖于一组参数 $\{\alpha\}$ 的[试探波函数](@entry_id:142892) $|\psi(\boldsymbol{\alpha})\rangle$，然后通过最小化[能量期望值](@entry_id:174035) $E(\boldsymbol{\alpha}) = \langle\psi(\boldsymbol{\alpha})|\hat{H}|\psi(\boldsymbol{\alpha})\rangle$ 来寻找最优参数，从而获得对[基态能量](@entry_id:263704)的最佳近似。

值得注意的是，一个能够给出较好变分能量的[试探函数](@entry_id:756165)，不一定能同样好地预测其他物理量的[期望值](@entry_id:153208)。然而，在某些特定条件下，即使[波函数](@entry_id:147440)本身不够精确，某些[可观测量](@entry_id:267133)的[期望值](@entry_id:153208)也可能相当准确 [@problem_id:2769946]。

- 如果一个算符 $\hat{A}$ 与[哈密顿算符](@entry_id:144286) $\hat{H}$ 对易，即 $[\hat{A}, \hat{H}] = 0$，那么它们拥有共同的本征基 $\{|n\rangle\}$。此时 $\langle \hat{A} \rangle_\psi = \sum_n |c_n|^2 a_n$。如果对于那些在 $|\psi\rangle$ 中占主导地位的[激发态](@entry_id:261453) $|n\rangle$（即 $|c_n|^2$ 较大），其对应的[本征值](@entry_id:154894) $a_n$恰好与[基态](@entry_id:150928)[本征值](@entry_id:154894) $a_0$ 非常接近，那么即使 $|\psi\rangle$ 与真实[基态](@entry_id:150928)相差甚远（即 $|c_0|^2 \ll 1$），计算出的 $\langle \hat{A} \rangle_\psi$ 仍然可能非常接近真实值 $a_0$。

- 一个更为普遍且强大的结果是**[Hellmann-Feynman定理](@entry_id:173798)**。如果[哈密顿量](@entry_id:172864)依赖于某个参数 $\lambda$（例如，外[电场](@entry_id:194326)强度或核坐标），$H=H(\lambda)$，并且我们使用变分法优化的[波函数](@entry_id:147440) $|\psi(\boldsymbol{\alpha}^\star(\lambda))\rangle$ 来计算能量 $E_{\mathrm{var}}(\lambda)$，那么能量对参数的一阶导数等于算符 $\partial H/\partial\lambda$ 的[期望值](@entry_id:153208)：
  $$
  \frac{d E_{\mathrm{var}}}{d\lambda} = \left\langle \psi(\boldsymbol{\alpha}^\star(\lambda)) \left| \frac{\partial H}{\partial \lambda} \right| \psi(\boldsymbol{\alpha}^\star(\lambda)) \right\rangle
  $$
  这个结果表明，对于形如 $\partial H/\partial\lambda$ 的可观测量（例如，[电偶极矩](@entry_id:178520)是[电场](@entry_id:194326)参数的导数），其[期望值](@entry_id:153208)的计算是“一阶误差自洽的”。这意味着，如果[波函数](@entry_id:147440)的误差是 $\mathcal{O}(\epsilon)$，那么能量的误差是 $\mathcal{O}(\epsilon^2)$，而这些特定[可观测量](@entry_id:267133)的[期望值](@entry_id:153208)误差也是 $\mathcal{O}(\epsilon^2)$，而非通常的 $\mathcal{O}(\epsilon)$。这使得许多分子性质的计算在变分框架下异常准确。

#### 对称性与选择定则：Wigner-Eckart 定理

[期望值](@entry_id:153208)的计算与系统的对称性密切相关。**[Wigner-Eckart定理](@entry_id:144878)**为我们提供了一个深刻而实用的工具来理解[角动量守恒](@entry_id:156798)如何约束矩阵元素（包括[期望值](@entry_id:153208)） [@problem_id:2769914]。该定理适用于**不可约[张量算符](@entry_id:203590)**（irreducible spherical tensor operators）$T_q^{(k)}$，这是一类在旋转下具有特定变换性质的算符（$k$是阶，$q$是分量）。

[Wigner-Eckart定理](@entry_id:144878)指出，[张量算符](@entry_id:203590)在角动量[本征态](@entry_id:149904) $|l, m\rangle$ 之间的矩阵元素可以分解为两个部分的乘积：
$$
\langle l' m' | T^{(k)}_q | l m \rangle = \frac{1}{\sqrt{2 l' + 1}} \langle l' || T^{(k)} || l \rangle \langle l m; k q | l' m' \rangle
$$
其中：
- $\langle l m; k q | l' m' \rangle$ 是一个**[Clebsch-Gordan系数](@entry_id:142551)**，它完全由旋转对称性（几何）决定，包含了关于 $m, m', q$ 的全部信息。
- $\langle l' || T^{(k)} || l \rangle$ 是**简约[矩阵元](@entry_id:186505)**（reduced matrix element），它与[磁量子数](@entry_id:145584)无关，包含了算符和态的内在物理（动力学）信息。

这个定理的威力在于它所蕴含的**[选择定则](@entry_id:140784)**（selection rules）。[Clebsch-Gordan系数](@entry_id:142551)非零的条件是：
1.  $m' = m + q$
2.  $|l - k| \le l' \le l + k$ (三角不等式)

任何不满足这些条件的[矩阵元](@entry_id:186505)素都必定为零。

当我们考虑一个态 $|l, m\rangle$ 中算符 $T_q^{(k)}$ 的[期望值](@entry_id:153208)时，我们考察的是[对角矩阵](@entry_id:637782)元素，即 $l'=l, m'=m$。应用选择定则：
1.  $m = m + q \implies q=0$
2.  $|l - k| \le l \le l + k \implies k \le 2l$

这意味着，只有一个[张量算符](@entry_id:203590)的 $q=0$ 分量才可能在 $|l, m\rangle$ 态中有非零的[期望值](@entry_id:153208)，并且算符的阶 $k$ 不能超过 $2l$。例如，对于一个 $p$ 电子态 ($l=1$)，只有阶 $k \le 2$ 的[张量算符](@entry_id:203590)（如标量 $k=0$、矢量 $k=1$、[四极矩](@entry_id:157717) $k=2$）才可能有非零[期望值](@entry_id:153208)。这个定理为之前关于 $\langle L_x \rangle = 0$ 的结论提供了更普适和深刻的解释（因为 $L_x$ 是 $k=1, q=\pm 1$ 张量分量的线性组合），并成为[光谱学](@entry_id:141940)和反应动力学中分析跃迁和相互作用的基础。

### 严格的数学基础 (高等主题)

#### 对称算符与自伴算符

在入门级量子力学中，[厄米算符](@entry_id:153410)和自伴算符（self-adjoint operator）通常被混用。然而在严格的[数学物理](@entry_id:265403)中，它们之间存在关键的区别，这对理解[量子理论](@entry_id:145435)的结构至关重要。一个在稠密定义域 $\mathcal{D}(A)$ 上定义的算符 $A$ 被称为**对称的**（symmetric），如果对于所有 $\phi, \psi \in \mathcal{D}(A)$ 都满足 $\langle \phi, A\psi\rangle = \langle A\phi, \psi\rangle$。一个算符被称为**自伴的**，如果它是对称的，并且其定义域与其伴随算符的定义域相同，即 $\mathcal{D}(A) = \mathcal{D}(A^\dagger)$。

**物理可观测量必须由自伴算符表示**。对称性足以保证[本征值](@entry_id:154894)为实数，但只有自伴性才能保证[谱定理](@entry_id:136620)（spectral theorem）的成立，该定理确保存在一个完备的[本征函数](@entry_id:154705)集（或更一般的投影值测量），为[量子测量](@entry_id:272490)理论提供了完整的数学基础。

一个经典的例子是定义在希尔伯特空间 $L^2(\mathbb{R})$ 上的[动量算符](@entry_id:151743) $\hat{p} = -i\hbar d/dx$ [@problem_id:2769976]。如果我们将其定义在一个“过小”的定义域上，例如无限可微且具有[紧支撑](@entry_id:276214)的[函数空间](@entry_id:143478) $C_c^\infty(\mathbb{R})$，那么通过分部积分可以证明该算符是对称的。然而，它并非自伴的，因为它的伴随算符的定义域是更大的Sobolev空间 $H^1(\mathbb{R})$。这个初始的对称算符没有任何属于 $L^2(\mathbb{R})$ 的本征函数（其形式解 $e^{ipx/\hbar}$ 不是平方可积的），这凸显了仅有对称性是不够的。幸运的是，这个算符是“本质自伴的”，它的[闭包](@entry_id:148169)是唯一的自伴算符，即定义在 $H^1(\mathbb{R})$ 上的[动量算符](@entry_id:151743)，它才真正代表了物理动量。

当系统被限制在有限区间 $[0, L]$ 时，情况变得更加复杂 [@problem_id:2769899]。定义在 $\mathcal{D}(\hat{p}_0) = \{\psi \in H^1([0,L]) : \psi(0)=\psi(L)=0\}$ 上的动量算符是对称的，但不是自伴的。它的伴随算符的定义域是整个 $H^1([0,L])$，没有任何边界条件。与在全[实轴](@entry_id:148276)上的情况不同，这个算符有无穷多个[自伴扩张](@entry_id:264525)。每一个扩张对应着一种特定的边界条件，形式为 $\psi(L) = e^{i\theta}\psi(0)$，其中 $\theta \in [0, 2\pi)$ 是一个参数。每一种边界条件都定义了一个合法的、物理上不同的系统（例如，$\theta=0$ 对应周期性边界条件）。这说明边界条件是定义[量子算符](@entry_id:137703)不可或缺的一部分。相比之下，位置算符 $\hat{x}$ 在有限区间 $[0, L]$ 上是一个有界算符，其定义域是整个[希尔伯特空间](@entry_id:261193) $L^2([0,L])$，它自然就是自伴的，不存在这些复杂性。

#### 推广到非厄米系统

尽管量子力学的基本假设要求[哈密顿量](@entry_id:172864)是厄米的，但在许多领域，如[开放量子系统](@entry_id:138632)、光学和反应动力学中，人们会遇到**有效非厄米[哈密顿量](@entry_id:172864)**（effective non-Hermitian Hamiltonians）。这些[哈密顿量](@entry_id:172864)通常用于描述一个更大系统的一部分，其中能量可以流入或流出该子系统。

对于一个非厄米[哈密顿量](@entry_id:172864) $\hat{H} \neq \hat{H}^\dagger$，其左右本征矢通常是不同的。它们分别由以下两个本征方程定义：
$$
\hat{H}\,|\psi_{\mathrm{R}}\rangle = E\,|\psi_{\mathrm{R}}\rangle \qquad (\text{右本征矢})
$$
$$
\langle\psi_{\mathrm{L}}|\,\hat{H} = E\,\langle\psi_{\mathrm{L}}| \qquad (\text{左本征矢})
$$
左本征矢 $\langle\psi_{\mathrm{L}}|$ 是 $\hat{H}^\dagger$ 对应于[本征值](@entry_id:154894) $E^*$ 的右本征矢的[厄米共轭](@entry_id:191215)。对于同一个[本征值](@entry_id:154894) $E$，对应的左右本征矢形成一个**双正交**（biorthogonal）关系：$\langle \psi_{\mathrm{L},i} | \psi_{\mathrm{R},j} \rangle = \delta_{ij}$（经过适当归一化后）。

在这种框架下，可观测量 $\hat{A}$ 的[期望值](@entry_id:153208)需要用双正交定义来计算，以确保物理意义 [@problem_id:2769911]：
$$
\langle \hat{A} \rangle_{\mathrm{b}} = \frac{\langle \psi_{\mathrm{L}} | \hat{A} | \psi_{\mathrm{R}} \rangle}{\langle \psi_{\mathrm{L}} | \psi_{\mathrm{R}} \rangle}
$$
通常我们选择归一化使得分母为1。

考虑一个简单的非厄米[哈密顿量](@entry_id:172864) $\hat{H} = \begin{pmatrix} 0  2 \\ 1/2  0 \end{pmatrix}$。它的[本征值](@entry_id:154894)为 $E=\pm 1$。对于 $E=1$，右本征矢满足 $\begin{pmatrix} 0  2 \\ 1/2  0 \end{pmatrix} \begin{pmatrix} c_1 \\ c_2 \end{pmatrix} = \begin{pmatrix} c_1 \\ c_2 \end{pmatrix}$，解得 $c_1=2c_2$，所以未归一化的右本征矢是 $|\psi_{\mathrm{R}}\rangle \propto \begin{pmatrix} 2 \\ 1 \end{pmatrix}$。左本征矢是 $\hat{H}^\dagger = \begin{pmatrix} 0  1/2 \\ 2  0 \end{pmatrix}$ 的右本征矢的共轭，解得其未归一化的形式为 $\langle\psi_{\mathrm{L}}| \propto \begin{pmatrix} 1  2 \end{pmatrix}$。

双正交[归一化条件](@entry_id:156486) $\langle\psi_{\mathrm{L}}|\psi_{\mathrm{R}}\rangle = 1$ 要求 $N_L N_R (\begin{pmatrix} 1  2 \end{pmatrix}\begin{pmatrix} 2 \\ 1 \end{pmatrix}) = 4N_L N_R = 1$。现在，我们可以计算一个厄米算符，比如 $\hat{A} = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}$ 的[期望值](@entry_id:153208)：
$$
\langle \hat{A} \rangle_{\mathrm{b}} = N_L N_R \begin{pmatrix} 1  2 \end{pmatrix} \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix} \begin{pmatrix} 2 \\ 1 \end{pmatrix} = (N_L N_R) \begin{pmatrix} 1  2 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \end{pmatrix} = (N_L N_R) \cdot 5 = \frac{1}{4} \cdot 5 = \frac{5}{4}
$$
这个例子说明，即使在非厄米系统中，通过引入双正交形式，[期望值](@entry_id:153208)的概念仍然可以被一致地定义和计算，从而为描述更复杂的物理现象提供了数学工具。