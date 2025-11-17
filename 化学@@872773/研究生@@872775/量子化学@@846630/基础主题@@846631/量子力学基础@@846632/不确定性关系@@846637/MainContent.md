## 引言
不确定性关系是量子力学的奠基性原则之一，其意义远超于对测量行为的简单限制。它深刻地揭示了微观世界固有的概率性和非经典特征，是理解[物质结构](@entry_id:269505)、稳定性与动力学行为的关键。然而，其常常被简化或误解为仅仅是观测过程带来的干扰效应，而其作为一种强大预测工具的建设性作用则未被充分认识。本文旨在填补这一认知空白，系统地展现不确定性关系如何从抽象的数学公理，转变为解释和预测化学及相关物理现象的有力工具。

为实现这一目标，本文将分为三个核心部分。在“原理和机制”一章中，我们将从量子力学的基本公设出发，推导不确定性关系的普适形式，并辨析其在不同物理场景下的具体内涵。随后的“应用与跨学科连接”一章将通过一系列实例，展示这些原理如何解释[分子稳定性](@entry_id:137744)、[谱线](@entry_id:193408)展宽、[量子限制效应](@entry_id:184087)等关键现象。最后，在“动手实践”部分，读者将有机会通过具体的计算问题，亲手验证和应用这些理论概念。

通过这一系列的探讨，我们将逐步揭示不确定性原理的深层力量。现在，让我们从其最根本的数学与物理基础——原理和机制——开始我们的探索之旅。

## 原理和机制

在量子力学中，不确定性原理并非仅仅是测量过程中的干扰效应，而是系统内在属性的基[本体](@entry_id:264049)现。本章将从量子力学的基本公设出发，系统地阐述不确定性关系的数学原理，并探讨其在[量子化学](@entry_id:140193)各领域的不同表现形式和深刻内涵。

### 不确定性关系的一般形式

不确定性关系的数学基础源于希尔伯特空间（Hilbert Space）的内在几何结构。对于任何一个归一化的[量子态](@entry_id:146142) $|\psi\rangle$ 和两个厄米算符（Hermitian operators） $\hat{A}$ 和 $\hat{B}$（代表可观测的物理量），我们可以定义其[期望值](@entry_id:153208) $\langle \hat{A} \rangle = \langle \psi | \hat{A} | \psi \rangle$ 和标准差 $\Delta A = \sqrt{\langle (\hat{A} - \langle \hat{A} \rangle)^2 \rangle}$。[标准差](@entry_id:153618) $\Delta A$ 量化了在态 $|\psi\rangle$ 上对物理量 $A$ 进行多次测量所得结果的统计离散程度，即物理量 $A$ 的**不确定度**。

所有不确定性关系都可以从一个普适的数学不等式——**柯西-[施瓦茨不等式](@entry_id:202153)**（Cauchy–Schwarz inequality）中推导出来。考虑两个向量 $|f\rangle = (\hat{A} - \langle \hat{A} \rangle) |\psi\rangle$ 和 $|g\rangle = (\hat{B} - \langle \hat{B} \rangle) |\psi\rangle$。根据柯西-[施瓦茨不等式](@entry_id:202153)，我们有：
$$
\langle f | f \rangle \langle g | g \rangle \ge |\langle f | g \rangle|^2
$$
左侧的两项正是[方差](@entry_id:200758)的定义：
$$
\langle f | f \rangle = \langle \psi | (\hat{A} - \langle \hat{A} \rangle)^\dagger (\hat{A} - \langle \hat{A} \rangle) | \psi \rangle = \langle (\hat{A} - \langle \hat{A} \rangle)^2 \rangle = (\Delta A)^2
$$
$$
\langle g | g \rangle = \langle (\hat{B} - \langle \hat{B} \rangle)^2 \rangle = (\Delta B)^2
$$
右侧的[内积](@entry_id:158127)可以展开为一个算符[乘积的期望值](@entry_id:201037)：
$$
\langle f | g \rangle = \langle (\hat{A} - \langle \hat{A} \rangle)(\hat{B} - \langle \hat{B} \rangle) \rangle
$$
任意算符乘积 $\hat{C}\hat{D}$ 都可以分解为厄米和反厄米部分之和：
$$
\hat{C}\hat{D} = \frac{1}{2}(\hat{C}\hat{D} + \hat{D}\hat{C}) + \frac{1}{2}(\hat{C}\hat{D} - \hat{D}\hat{C}) = \frac{1}{2}\{\hat{C}, \hat{D}\} + \frac{1}{2}[\hat{C}, \hat{D}]
$$
其中 $\{\hat{C}, \hat{D}\}$ 是**[反对易子](@entry_id:139754)**（anticommutator），$[\hat{C}, \hat{D}]$ 是**对易子**（commutator）。当 $\hat{C}$ 和 $\hat{D}$ 为[厄米算符](@entry_id:153410)时，其[反对易子](@entry_id:139754)是厄米的，[期望值](@entry_id:153208)为实数；其对易子是反厄米的，[期望值](@entry_id:153208)为纯虚数。应用这个分解，我们得到：
$$
\langle f | g \rangle = \frac{1}{2} \langle \{ \hat{A} - \langle \hat{A} \rangle, \hat{B} - \langle \hat{B} \rangle \} \rangle + \frac{1}{2} \langle [\hat{A} - \langle \hat{A} \rangle, \hat{B} - \langle \hat{B} \rangle] \rangle
$$
由于标量与任何算符都对易，因此 $[\hat{A} - \langle \hat{A} \rangle, \hat{B} - \langle \hat{B} \rangle] = [\hat{A}, \hat{B}]$。第一项的实部定义了物理量 $A$ 和 $B$ 在态 $|\psi\rangle$ 中的**协[方差](@entry_id:200758)**（covariance），记为 $\mathrm{cov}(A,B)$。因此，$\langle f | g \rangle$ 的模平方为：
$$
|\langle f | g \rangle|^2 = \left( \frac{1}{2} \langle \{ \hat{A} - \langle \hat{A} \rangle, \hat{B} - \langle \hat{B} \rangle \} \rangle \right)^2 + \left| \frac{1}{2} \langle [\hat{A}, \hat{B}] \rangle \right|^2
$$
将所有部分组合在一起，我们便得到了最强形式的**罗伯逊-薛定谔不确定性关系**（Robertson–Schrödinger uncertainty relation）：
$$
(\Delta A)^2 (\Delta B)^2 \ge \left( \mathrm{cov}(A,B) \right)^2 + \left| \frac{1}{2i} \langle [\hat{A}, \hat{B}] \rangle \right|^2
$$
这个关系揭示了不确定性的两个独立来源：算符的**[非对易性](@entry_id:153545)**（由对易子项表征）和态的**[统计相关性](@entry_id:267552)**（由协[方差](@entry_id:200758)项表征）。忽略非负的协[方差](@entry_id:200758)项，我们得到一个更常见但较弱的形式，即**[罗伯逊不确定性关系](@entry_id:149837)**：
$$
\Delta A \Delta B \ge \frac{1}{2} |\langle [\hat{A}, \hat{B}] \rangle|
$$

### [正则对易关系](@entry_id:185041)与[海森堡不确定性原理](@entry_id:171099)

量子力学中最著名和最基本的不确定性关系是位置和动量之间的关系。一维空间中，位置算符 $\hat{x}$ 和动量算符 $\hat{p}$ 满足**[正则对易关系](@entry_id:185041)**（Canonical Commutation Relation, CCR）：
$$
[\hat{x}, \hat{p}] = i\hbar
$$
这个[对易关系](@entry_id:136780)是一个算符恒等式，它的结果是一个常数（$i\hbar$）乘以单位算符。这意味着对于任何归一化的[量子态](@entry_id:146142) $|\psi\rangle$，其[期望值](@entry_id:153208)都是一个与态无关的常数：
$$
\langle [\hat{x}, \hat{p}] \rangle = \langle \psi | i\hbar I | \psi \rangle = i\hbar \langle \psi | \psi \rangle = i\hbar
$$
将这个结果代入罗伯逊关系，我们立刻得到**海森堡不确定性原理**（Heisenberg Uncertainty Principle, HUP）：
$$
\Delta x \Delta p \ge \frac{\hbar}{2}
$$
这个下限 $\hbar/2$ 是一个普适常数，它不依赖于具体的[量子态](@entry_id:146142)，也不依赖于系统所处的势场 $V(x)$。[势场](@entry_id:143025) $V(x)$ 通过[哈密顿量](@entry_id:172864) $H = \frac{\hat{p}^2}{2m} + V(x)$ 决定了系统的能级和[本征态](@entry_id:149904)，从而影响了特[定态](@entry_id:137260)的 $\Delta x$ 和 $\Delta p$ 的具体数值，但它绝不会改变这个由[运动学](@entry_id:173318)结构（即CCR）决定的基本下限 [@problem_id:2934739]。

能够使上述不等式取等号的态被称为**最小不确定度态**。对于位置和动量，这些态的[波函数](@entry_id:147440)是[高斯波包](@entry_id:151158)（Gaussian wave packets）。值得注意的是，虽然[高斯波包](@entry_id:151158)作为一种有效的[量子态](@entry_id:146142)普遍存在于希尔伯特空间中，但它们仅在[势能](@entry_id:748988) $V(x)$ 为二次或常数（即[量子谐振子](@entry_id:140678)或自由粒子）的情况下才是[哈密顿量](@entry_id:172864)的[定态](@entry_id:137260)（能量本征态）[@problem_id:2934739]。对于更复杂的[分子振动](@entry_id:140827)（[非谐振子](@entry_id:142760)），其[振动](@entry_id:267781)[基态](@entry_id:150928)并非高斯函数，因此其不确定度乘积 $\Delta x \Delta p$ 将严格大于 $\hbar/2$。

### 态依赖与协[方差](@entry_id:200758)引起的不确定性

当两个算符的对易子不是常数算符时，罗伯逊关系给出的下限就依赖于[量子态](@entry_id:146142)。一个很好的例子是算符对 $(\hat{x}, \hat{p}^2)$。利用对易子恒等式，我们发现 $[\hat{x}, \hat{p}^2] = [\hat{x}, \hat{p}]\hat{p} + \hat{p}[\hat{x}, \hat{p}] = 2i\hbar\hat{p}$。此时，不确定性关系变为：
$$
\Delta x \Delta(p^2) \ge \frac{1}{2} |\langle 2i\hbar\hat{p} \rangle| = \hbar |\langle \hat{p} \rangle|
$$
这个下限直接正比于动量的平均值。对于一个被束缚在[对称势](@entry_id:148561)场（如谐振子或[无限深势阱](@entry_id:140940)中心）中的粒子，其任何[能量本征态](@entry_id:152154)的平均动量 $\langle \hat{p} \rangle$ 都为零。在这种情况下，罗伯逊关系给出的下限是 $\Delta x \Delta(p^2) \ge 0$，这是一个毫无信息的平凡界。然而，这并不意味着 $\Delta x$ 或 $\Delta(p^2)$ 为零；它们通常都有非零的涨落。这说明罗伯逊关系有时会因为其下限依赖于态的特定对称性而变得不够有效 [@problem_id:2631079]。

更有趣的是，即使两个算符完全对易（$ [\hat{A}, \hat{B}]=0 $），它们的不确定度乘积也未必为零。在这种情况下，罗伯逊-薛定谔关系简化为：
$$
\Delta A \Delta B \ge |\mathrm{cov}(A,B)|
$$
其中协[方差](@entry_id:200758) $\mathrm{cov}(A,B) = \frac{1}{2}\langle\{\hat{A}-\langle A \rangle, \hat{B}-\langle B \rangle\}\rangle = \langle \hat{A}\hat{B} \rangle - \langle \hat{A} \rangle\langle \hat{B} \rangle$。这个关系表明，对于可对易的观测量，不确定性来源于它们在特定[量子态](@entry_id:146142)中的**[统计相关性](@entry_id:267552)**。如果一个态不是 $\hat{A}$ 或 $\hat{B}$ 的共同本征态，那么对它们的测量结果可能是[统计相关](@entry_id:200201)的，导致协[方差](@entry_id:200758)不为零。

一个具体的例子是在[量子化学](@entry_id:140193)中，考虑两个不同的单电子自旋[轨道](@entry_id:137151) $p$ 和 $q$，以及它们对应的[粒子数算符](@entry_id:153568) $\hat{n}_p$ 和 $\hat{n}_q$。这两个算符显然是对易的。现在考虑一个单电子叠加态 $|\psi\rangle = \cos\theta |1_p, 0_q\rangle + \sin\theta |0_p, 1_q\rangle$。在这个态中，我们发现电子要么在[轨道](@entry_id:137151) $p$ 中，要么在[轨道](@entry_id:137151) $q$ 中，但绝不会同时在两者中。这种互斥性导致了强烈的反相关。计算表明，$\langle \hat{n}_p \hat{n}_q \rangle = 0$，而 $\langle \hat{n}_p \rangle = \cos^2\theta$ 且 $\langle \hat{n}_q \rangle = \sin^2\theta$。因此，协[方差](@entry_id:200758)为 $\mathrm{cov}(n_p, n_q) = 0 - \cos^2\theta \sin^2\theta = -\cos^2\theta \sin^2\theta$。不确定性关系给出 $\Delta n_p \Delta n_q \ge \cos^2\theta \sin^2\theta$。除非 $\theta=0$ 或 $\theta=\pi/2$（即系统处于其中一个[基态](@entry_id:150928)），否则这个下限是非零的。这清晰地展示了即使没有[非对易性](@entry_id:153545)，[统计相关性](@entry_id:267552)本身也是[量子不确定性](@entry_id:156130)的一个独立来源 [@problem_id:2934694]。

### [能量-时间不确定性](@entry_id:138934)与量子速率极限

[能量-时间不确定性](@entry_id:138934)关系具有特殊的地位，因为在非[相对论量子力学](@entry_id:148643)中，时间 $t$ 是一个参数，而不是一个[厄米算符](@entry_id:153410)。因此，形式如 $\Delta E \Delta t \ge \hbar/2$ 的简单类比是不严谨的。更严格的表述联系了系统的能量不确定度 $\Delta E$ 与某个可观测量 $\hat{A}$ 的[期望值](@entry_id:153208)随[时间演化](@entry_id:153943)的速率。这一关系，即**曼德尔施塔姆-塔姆关系**（Mandelstam-Tamm relation），可以从薛定谔方程和罗伯逊关系推导得出：
$$
\Delta E \Delta A \ge \frac{\hbar}{2} \left| \frac{d\langle \hat{A} \rangle}{dt} \right|
$$
这个关系表明，系统的能量不确定度越大，其内部 observable 的[期望值](@entry_id:153208)就可能演化得越快。

这个原理的一个重要推论是所谓的**量子速率极限**（quantum speed limit），它限制了一个量子系统从一个状态演化到另一个状态所需的最短时间。特别地，我们可以计算一个系统从初始态 $|\psi(0)\rangle$ 演化到与其正交的态 $|\psi(T_\perp)\rangle$（即 $\langle \psi(0) | \psi(T_\perp) \rangle = 0$）所需的最短时间，称为**正交化时间**。基于曼德尔施塔姆-塔姆关系，可以推导出 $T_\perp$ 的一个下限：
$$
T_\perp \ge \frac{\pi\hbar}{2\Delta E}
$$
这个界限意味着，能量越确定的系统（$\Delta E$ 越小），其演化到正交状态所需的时间就越长。例如，对于一个处在叠加态 $|\psi(0)\rangle = \cos(\theta/2)|0\rangle + \sin(\theta/2)|1\rangle$ 的[量子比特](@entry_id:137928)（qubit），其能量不确定度为 $\Delta E = \frac{\hbar\omega}{2}|\sin\theta|$，因此其正交化时间满足 $T_\perp \ge \frac{\pi}{\omega |\sin\theta|}$ [@problem_id:2131879]。

除了依赖于[能量方差](@entry_id:156656)的曼德尔施塔姆-塔姆界，还存在另一个独立的量子速率极限，即**马戈勒斯-列[维京定理](@entry_id:264111)**（Margolus-Levitin theorem）。它给出的[正交化](@entry_id:149208)时间下限依赖于系统相对于[基态](@entry_id:150928)的平均能量 $E - E_0$：
$$
\tau \ge \frac{\pi\hbar}{2(E - E_0)}
$$
这两个界限共同构成了[量子演化](@entry_id:198246)速率的约束：$\tau \ge \max\left(\frac{\pi\hbar}{2\Delta E}, \frac{\pi\hbar}{2(E - E_0)}\right)$。在某些情况下，一个界限可能比另一个更严格。例如，对于一个处于相干态的[分子振动](@entry_id:140827)模式，其[振动](@entry_id:267781)量子数服从[泊松分布](@entry_id:147769)，平均值为 $\bar{n}$，[方差](@entry_id:200758)也为 $\bar{n}$。在这种情况下，$\Delta E \propto \sqrt{\bar{n}}$ 而 $E - E_0 \propto \bar{n}$。当 $\bar{n} > 1$ 时，$\sqrt{\bar{n}}  \bar{n}$，因此曼德尔施塔姆-塔姆界（依赖于 $\Delta E$）会比马戈勒斯-列维京界（依赖于 $E - E_0$）更严格，即给出更长的最小演化时间 [@problem_id:2934757]。

### 不确定性关系的现代诠释

#### 测量噪声与扰动

海森堡最初构想的不确定性原理，是通过一个思想实验——伽利略显微镜——来阐述的，其中测量一个粒子的位置（噪声 $\epsilon(A)$）不可避免地会扰动其动量（扰动 $\eta(B)$）。然而，罗伯逊关系 $\Delta x \Delta p \ge \hbar/2$ 描述的是在相同制备的系统系综上，分别测量 $A$ 和 $B$ 的固有统计**涨落**，即所谓的**[制备不确定性](@entry_id:203575)**，它与任何具体的测量过程无关。

混淆这两者曾导致一个错误的观念，即认为测量的噪声和扰动也遵循类似的简单乘积关系 $\epsilon(A)\eta(B) \ge \hbar/2$。现代[量子测量](@entry_id:272490)理论已经证明这个“海森堡噪声-扰动关系”并非普适成立。由 Ozawa Masanao 等人发展的严谨理论，为间接测量模型下的噪声和扰动提供了一个**普适有效的不等式**：
$$
\epsilon(A)\eta(B) + \epsilon(A)\Delta B + \Delta A \eta(B) \ge \frac{1}{2} |\langle [\hat{A}, \hat{B}] \rangle|
$$
这里，$\epsilon(A)$ 是测量 $A$ 的**噪声**（测量结果与真实值之间的[均方根](@entry_id:263605)差），$\eta(B)$ 是该测量对物理量 $B$ 造成的**扰动**（测量前后 $B$ 值的[均方根](@entry_id:263605)差），而 $\Delta A$ 和 $\Delta B$ 是系统初始态的内在不确定度。这个关系式更加复杂，它表明噪声-扰动的权衡还与系统本身的量子涨落有关。在 $\Delta A \to 0$ 或 $\Delta B \to 0$ 的极限下，这个关系并不会失效，而是揭示了更深刻的联系 [@problem_id:2631057]。

#### [熵不确定性关系](@entry_id:142360)

另一种现代且更强大的表述方式是**[熵不确定性关系](@entry_id:142360)**（entropic uncertainty relation）。它使用[香农熵](@entry_id:144587)（Shannon entropy）来量化不确定性，而不是[标准差](@entry_id:153618)。对于连续的[概率分布](@entry_id:146404) $\rho(x)$，其[微分熵](@entry_id:264893)定义为 $h_x = -\int \rho(x) \ln \rho(x) dx$。对于位置和动量，其[微分熵](@entry_id:264893)之和有一个普适下限：
$$
h_x + h_p \ge \ln(\pi e \hbar)
$$
这个关系比基于[方差](@entry_id:200758)的海森堡原理更强，因为它约束了整个[概率分布](@entry_id:146404)的形态，而不仅仅是其二阶矩。例如，一个具有多个峰值的[分布](@entry_id:182848)可能有很小的[方差](@entry_id:200758)，但熵会很大。

更有用的是，这个连续熵关系可以与离散测量联系起来。如果我们用宽度为 $\delta x$ 和 $\delta p$ 的探测器阵列来测量位置和动量，得到离散的[概率分布](@entry_id:146404)，其对应的[香农熵](@entry_id:144587) $H_X$ 和 $H_P$ 满足：
$$
H_X + H_P \ge \ln\left(\frac{\pi e \hbar}{\delta x \delta p}\right)
$$
这个关系直接量化了在有限分辨率测量下我们对位置和动量信息的总获取能力的极限。而且，可以证明，在精细化极限下（$\delta x, \delta p \to 0$），结合高斯分布是定[方差](@entry_id:200758)下熵最大的[分布](@entry_id:182848)这一事实，这个[熵不确定性关系](@entry_id:142360)可以恢复出标准的海森堡关系 $\Delta x \Delta p \ge \hbar/2$ [@problem_id:2934747]。

#### [量子计量学](@entry_id:138980)中的不确定性

不确定性原理也为**[量子计量学](@entry_id:138980)**（quantum metrology）提供了根本限制，即我们能达到的最高[测量精度](@entry_id:271560)。考虑一个通过幺正过程 $U_\theta = \exp(-i\theta G)$ 将参数 $\theta$ （例如外场强度）编码到[量子态](@entry_id:146142) $|\psi_\theta\rangle = U_\theta |\psi_0\rangle$ 的情景。这里的厄米算符 $G$ 是该过程的**生成元**。

**[量子克拉默-拉奥界](@entry_id:144137)**（Quantum Cramér-Rao Bound, QCRB）指出，任何对 $\theta$ 的[无偏估计](@entry_id:756289)，其[标准差](@entry_id:153618) $\Delta\theta$ 都受到一个由**量子费雪信息**（Quantum Fisher Information, QFI）$F_Q$ 决定的下限约束：
$$
\Delta\theta \ge \frac{1}{\sqrt{F_Q}}
$$
对于上述幺正编码过程，可以证明量子费雪信息恰好是生成元 $G$ 在初态 $|\psi_0\rangle$ 上[方差](@entry_id:200758)的四倍：
$$
F_Q = 4(\Delta G)^2
$$
结合 QCRB，我们得到了一个深刻的参数估计不确定性关系：
$$
\Delta\theta \ge \frac{1}{2\Delta G} \quad \text{或} \quad \Delta\theta \Delta G \ge \frac{1}{2}
$$
这个关系形式上与海森堡原理非常相似。它表明，要想精确地估计参数 $\theta$，我们需要选择一个初始态 $|\psi_0\rangle$ 和一个生成元 $G$，使得生成元在该初始态上具有巨大的不确定度（涨落）$\Delta G$。这在[分子光谱学](@entry_id:148164)和[量子传感](@entry_id:138398)等领域具有重要的指导意义 [@problem_id:2934707]。

### 特定物理系统中的微妙之处

尽管[正则对易关系](@entry_id:185041) $[\hat{x}, \hat{p}]=i\hbar$ 及其不确定性原理是量子力学的基石，但在某些[坐标系](@entry_id:156346)或受限空间中，简单地套用这种形式会遇到深刻的数学困难。这些困难通常与算符的定义域和自伴性（self-adjointness）有关。

#### 角度与角动量

对于一个在圆周上运动的粒子，其[角位置](@entry_id:174053) $\phi$ 和 z-轴角动量 $L_z = -i\hbar \partial_\phi$ 似乎是共轭的。然而，试图建立一个满足 $[\hat{\phi}, L_z] = i\hbar$ 的自伴算符 $\hat{\phi}$ 会失败。根本原因在于 $L_z$ 在圆周（[周期性边界条件](@entry_id:147809)）上的谱是离散的（$\hbar m, m \in \mathbb{Z}$）。根据**泡利定理**（Pauli's theorem），如果两个自伴算符满足[正则对易关系](@entry_id:185041)，那么它们的谱必须是连续的并且覆盖整个实轴。由于 $L_z$ 的谱是离散的，不存在一个全局定义的、自伴的角度算符 $\hat{\phi}$ 与之共轭 [@problem_id:2934738]。

这个问题的一个严格处理方法是**Pegg-Barnett形式**，它在有限维的角动[量子数](@entry_id:145558)[子空间](@entry_id:150286)中定义一个厄米相位算符，然后通过取极限来计算物理量的[期望值](@entry_id:153208)。另一个方法是避免使用 $\hat{\phi}$，转而使用定义良好的周期性算符，如 $\cos\phi$ 和 $\sin\phi$，并为它们建立不确定性关系，例如 $\Delta L_z \Delta(\cos\phi) \ge \frac{\hbar}{2}|\langle\sin\phi\rangle|$ [@problem_id:2934738]。

#### 径向位置与径向动量

在三维[中心势](@entry_id:148563)场问题中，[径向坐标](@entry_id:165186) $r \in [0, \infty)$ 和径向动量 $p_r$ 之间也存在类似的复杂性。通常定义的径向[动量算符](@entry_id:151743) $p_r = -i\hbar(\partial_r + 1/r)$ 在希尔伯特空间 $L^2(\mathbb{R}^+, r^2 dr)$ 上只是一个**对称算符**（symmetric operator），但**不是自伴算符**。通过与一维动量算符 $P = -i\hbar d/dr$ 在半直线 $L^2(\mathbb{R}^+, dr)$ 上进行幺正变换对比，可以发现其亏损指数为 $(1,0)$，这意味着它没有任何[自伴扩张](@entry_id:264525)。

尽管如此，形式上的[对易关系](@entry_id:136780) $[r, p_r] = i\hbar$ 依然成立。因此，罗伯逊不等式 $\Delta r \Delta p_r \ge \hbar/2$ 在 $r$ 和 $p_r$ 的公共稠密定义域上是数学上有效的。然而，一个关键的物理区别在于，这个下限**永远无法被达到**。能够使不等式取等的最小不确定度态是[高斯函数](@entry_id:261394)，但任何[高斯函数](@entry_id:261394)在 $r=0$ 处的值都不为零。而 $p_r$ 作为对称算符的定义域要求其上的函数在原点处必须为零（或者更准确地说，其幺正变换后的函数 $u(r)=r\psi(r)$ 在原点为零）。因此，没有任何一个物理上允许的态（即在 $p_r$ 定义域内的态）可以是[高斯函数](@entry_id:261394)，所以 $\Delta r \Delta p_r$ 的值总是严格大于 $\hbar/2$ [@problem_id:2934692]。

这些例子强调了一个核心要点：在量子力学中，对算符性质（特别是定义域和自伴性）的严格[数学分析](@entry_id:139664)对于正确理解物理原理至关重要。