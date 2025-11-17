## 引言
海森堡不确定性原理是量子力学的奠基石之一，它从根本上改变了我们对物理实在的认知。该原理指出，我们无法同时无限精确地获知一个微观粒子的某些成对物理属性，例如位置和动量。这一概念不仅是量子世界反直觉特性的集中体现，更是理解从[原子结构](@entry_id:137190)到宇宙演化等众多现象的出发点。

然而，对不确定性原理的理解常常停留在其最基础的位置-动量形式。其深刻的数学结构、多样的表现形式以及在各个科学前沿的广泛应用，往往未被充分探讨。本文旨在填补这一空白，为读者提供一个从第一性原理到前沿应用的系统性、研究生水平的深度解析。

为此，我们将分三步展开探索。在“原理与机制”一章中，我们将深入其数学核心，从[算符对易子](@entry_id:152475)出发，推导普适的罗伯逊-薛定谔关系，并辨析不同类型[不确定性关系](@entry_id:186128)（如时间-能量）的微妙之处，直至[熵不确定性关系](@entry_id:142360)和[广义不确定性原理](@entry_id:161890)等现代诠释。接着，在“应用与跨学科联系”一章中，我们将展示该原理的强大威力，看它如何解释原子稳定性与[零点能](@entry_id:142176)，如何决定恒星的命运，又如何与凝聚态物理、信号处理乃至量子引力等领域产生深刻的联系。最后，“动手实践”部分将提供一系列计算问题，帮助读者将理论知识转化为解决实际问题的能力。

## 原理与机制

在量子力学中，不[相容可观测量](@entry_id:151766)（由不对易的厄米算符表示）的同时确定性存在一个基本限制，这构成了海森堡不确定性原理的核心。本章旨在从第一性原理出发，系统地阐述这一原理的数学结构、物理内涵及其在不同物理情境下的各种表现形式与推广。

### 从对易子到不确定性：一般关系

[不确定性原理](@entry_id:141278)的数学基础源于希尔伯特空间中算符的[代数结构](@entry_id:137052)。对于任意两个[厄米算符](@entry_id:153410) $\hat{A}$ 和 $\hat{B}$，它们分别对应于[物理可观测量](@entry_id:154692) $A$ 和 $B$。在一个给定的[量子态](@entry_id:146142) $|\psi\rangle$ 中，这些可观测量的统计弥散程度由其[方差](@entry_id:200758)（或[标准差](@entry_id:153618)）来量化。一个[可观测量](@entry_id:267133) $\hat{O}$ 的[方差](@entry_id:200758)定义为：
$$ (\Delta O)^2 = \langle (\hat{O} - \langle \hat{O} \rangle)^2 \rangle $$
其中 $\langle \hat{O} \rangle = \langle \psi | \hat{O} | \psi \rangle$ 是其[期望值](@entry_id:153208)。

为了推导[不确定性关系](@entry_id:186128)，我们考虑两个辅助向量 $|f\rangle = (\hat{A} - \langle \hat{A} \rangle)|\psi\rangle$ 和 $|g\rangle = (\hat{B} - \langle \hat{B} \rangle)|\psi\rangle$。根据柯西-施瓦茨不等式，我们有：
$$ \langle f|f \rangle \langle g|g \rangle \ge |\langle f|g \rangle|^2 $$
注意到 $\langle f|f \rangle = (\Delta A)^2$ 和 $\langle g|g \rangle = (\Delta B)^2$。不等式的右边则涉及两个算符的协[方差](@entry_id:200758)。

关键的一步是将算符的乘积 $\Delta\hat{A} \Delta\hat{B}$（其中 $\Delta\hat{A} = \hat{A} - \langle\hat{A}\rangle$）分解为其厄米和反厄米部分，这等价于将其表示为[反对易子](@entry_id:139754)和对易子的组合：
$$ \Delta\hat{A} \Delta\hat{B} = \frac{1}{2} \{\Delta\hat{A}, \Delta\hat{B}\} + \frac{1}{2} [\Delta\hat{A}, \Delta\hat{B}] $$
由于 $\langle\hat{A}\rangle$ 和 $\langle\hat{B}\rangle$ 是常数，它们与任何算符对易，因此 $[\Delta\hat{A}, \Delta\hat{B}] = [\hat{A}, \hat{B}]$。取[期望值](@entry_id:153208)并利用任何复数 $z$ 的性质 $|z|^2 = (\Re z)^2 + (\Im z)^2$，我们可以得到一个比柯西-施瓦茨不等式更强的关系，即**罗伯逊-薛定谔[不确定性关系](@entry_id:186128)** (Robertson-Schrödinger uncertainty relation) [@problem_id:1150434]：
$$ (\Delta A)^2 (\Delta B)^2 \ge \left| \frac{1}{2i} \langle [\hat{A}, \hat{B}] \rangle \right|^2 + \left| \frac{1}{2} \langle \{\hat{A} - \langle \hat{A} \rangle, \hat{B} - \langle \hat{B} \rangle\} \rangle \right|^2 $$
这个关系式揭示了不确定性乘积的两个来源。第一项是**对易子项**，它量化了两个可观测量内在的量子不相容性。第二项是**协[方差](@entry_id:200758)项**，它量化了在一个特定[量子态](@entry_id:146142)中，两个可观测量的[统计关联](@entry_id:172897)或反关联。例如，对于一个自旋-1/2粒子，其自旋分量 $\hat{\sigma}_x$ 和 $\hat{\sigma}_y$ 的协[方差](@entry_id:200758) $C_{xy} = \frac{1}{2}\langle\{\hat{\sigma}_x, \hat{\sigma}_y\}\rangle - \langle\hat{\sigma}_x\rangle\langle\hat{\sigma}_y\rangle$ 在某些态中可以不为零，从而为不确定性乘积提供一个比仅考虑对易子时更强的下界 [@problem_id:1150422]。

在许多情况下，我们忽略非负的协[方差](@entry_id:200758)项，得到一个更简洁但较弱的不等式，即**[罗伯逊不确定性关系](@entry_id:149837)** (Robertson uncertainty relation)：
$$ \Delta A \Delta B \ge \frac{1}{2} |\langle [\hat{A}, \hat{B}] \rangle| $$
这个关系清晰地表明，只要两个可观测量的对易子的[期望值](@entry_id:153208)不为零，它们的不确定性乘积就有一个非零的下界。如果两个算符对易，即 $[\hat{A}, \hat{B}] = 0$，则下界为零。这对应于物理上的**[相容可观测量](@entry_id:151766)** (compatible observables)，它们可以被同时精确测量，并拥有一组共同的[本征态](@entry_id:149904) [@problem_id:2959695]。

### 典范[对易关系](@entry_id:136780)及其特殊性

量子力学中最著名的一对不[相容可观测量](@entry_id:151766)是位置 $\hat{x}$ 和动量 $\hat{p}$。它们满足**典范[对易关系](@entry_id:136780)** (canonical commutation relation, CCR)：
$$ [\hat{x}, \hat{p}] = i\hbar $$
其中 $\hbar$ 是[约化普朗克常数](@entry_id:275910)。这个对易子的特殊之处在于它是一个**c-数** (c-number)，即一个与所有算符都对易的常[数乘](@entry_id:155971)以单位算符 $\hat{I}$。

将此代入罗伯逊关系，我们得到：
$$ \Delta x \Delta p \ge \frac{1}{2} |\langle i\hbar \rangle| = \frac{\hbar}{2} $$
这个结果就是**海森堡-肯纳德[不确定性关系](@entry_id:186128)** (Heisenberg-Kennard uncertainty relation) [@problem_id:1150376]。其下界 $\hbar/2$ 是一个[普适常数](@entry_id:165600)，不依赖于系统所处的具体[量子态](@entry_id:146142) $|\psi\rangle$。

这种不依赖于状态的下界是典范对易关系的直接后果。一个深刻的问题是：在什么条件下，两个算符 $\hat{A}$ 和 $\hat{B}$ 的对易子 $[\hat{A}, \hat{B}] = i\hat{C}$ 中的 $\hat{C}$ 必须是单位算符的倍数？这在数学上与算符[代数表示](@entry_id:143783)的不可约性有关。根据[舒尔引理](@entry_id:136779) (Schur's Lemma)，如果一个算符（在这里是 $\hat{C}$）与一个代数的所有生成元（$\hat{A}$ 和 $\hat{B}$）都对易，并且该代数的表示是不可约的，那么这个算符必定是单位算符的倍数。对于位置和动量算符，它们所生成的魏尔-[海森堡代数](@entry_id:204103) (Weyl-Heisenberg algebra) 在 $L^2(\mathbb{R})$ 上的薛定谔表示是不可约的。更严格地，斯通-冯·诺依曼定理 (Stone-von Neumann theorem) 指出，任何满足魏尔关系（CCR的指数形式）的[不可约表示](@entry_id:263310)都[酉等价](@entry_id:197898)于标准的薛定谔表示，这保证了其对易子是一个c-数 [@problem_id:2959739]。相比之下，有限维希尔伯特空间中不存在满足 $[\hat{A}, \hat{B}] = i c \hat{I}$（其中 $c \neq 0$）的算符，因为任意有限维矩阵的[对易子的迹](@entry_id:194991)必为零，而 $i c \hat{I}$ 的迹不为零 [@problem_id:2959739]。

#### [最小不确定态](@entry_id:137309)

能够使[不确定性关系](@entry_id:186128)取等号的[量子态](@entry_id:146142)被称为**[最小不确定态](@entry_id:137309)** (minimum-uncertainty states)。对于典范对易关系，这意味着不仅要饱和罗伯逊-薛定谔关系，而且协[方差](@entry_id:200758)项必须为零。

一个典型的例子是一维量子谐振子 (QHO) 的[基态](@entry_id:150928)。其[波函数](@entry_id:147440)是一个高斯函数。通过直接计算可以证明，对于QHO[基态](@entry_id:150928)，$\langle\hat{x}\rangle=0$, $\langle\hat{p}\rangle=0$，并且协[方差](@entry_id:200758)项 $\langle\{\hat{x}, \hat{p}\}\rangle = \langle\hat{x}\hat{p} + \hat{p}\hat{x}\rangle$ 恰好为零。同时，[方差](@entry_id:200758)的乘积 $(\Delta x)^2 (\Delta p)^2 = (\frac{\hbar}{2m\omega})(\frac{m\omega\hbar}{2}) = \frac{\hbar^2}{4}$，正好等于罗伯逊-薛定谔关系下界 $|\frac{1}{2i}\langle[\hat{x}, \hat{p}]\rangle|^2 = (\frac{\hbar}{2})^2$。因此，QHO[基态](@entry_id:150928)是一个理想的[最小不确定态](@entry_id:137309) [@problem_id:1150434]。

更广泛的一类[最小不确定态](@entry_id:137309)是**相干态** (coherent states) $|\alpha\rangle$，它们是湮灭算符 $\hat{a}$ 的本征态。通过将 $\hat{x}$ 和 $\hat{p}$ 用产生和湮灭算符 $\hat{a}^\dagger, \hat{a}$ 表示，可以直接计算出对于任何相干态 $|\alpha\rangle$，其不确定性乘积始终是 $\Delta x \Delta p = \hbar/2$ [@problem_id:348992]。这使得相干态成为描述量子谐振子经典行为的理想选择。

**[压缩态](@entry_id:148885)** (squeezed states) 是另一类重要的[量子态](@entry_id:146142)。它们是罗伯逊-薛定谔关系下的[最小不确定态](@entry_id:137309)（也称“智能态”），但其不确定性的[分布](@entry_id:182848)是各向异性的。一个[压缩真空态](@entry_id:195785)的不确定性乘积为 $(\Delta x)^2 (\Delta p)^2 = \frac{\hbar^2}{4}[1 + \sinh^2(2r)\sin^2\phi]$，其中 $r$ 和 $\phi$ 是压缩参数 [@problem_id:1150474]。当压缩角 $\phi$ 不为0或 $\pi$ 的整数倍时，该乘积大于 $\hbar^2/4$，这是因为此时协[方差](@entry_id:200758)项不为零。然而，不确定性可以在一个正交分量（例如 $X_\theta$）中被“压缩”到小于[标准量子极限](@entry_id:137097)（即 $\Delta X_\theta  \sqrt{\hbar/2}$），代价是其正交伙伴（$X_{\theta+\pi/2}$）的不确定性被“放大” ($\Delta X_{\theta+\pi/2} > \sqrt{\hbar/2}$)。尽管如此，对于这对精心选择的正交分量，其不确定性乘积始终保持在最小值 $\Delta X_\theta \Delta X_{\theta+\pi/2} = \hbar/2$ [@problem_id:2959684]。

### 非 C 数对易子：依赖于状态的界

当两个可观测量的对易子不是c-数，而本身是另一个算符时，[不确定性关系](@entry_id:186128)的下界就变得依赖于状态。

[角动量算符](@entry_id:153013)是这类情况的典型代表。其分量满足对易关系 $[\hat{L}_i, \hat{L}_j] = i\hbar \epsilon_{ijk} \hat{L}_k$。例如，对于 $\hat{L}_x$ 和 $\hat{L}_y$，我们有：
$$ \Delta L_x \Delta L_y \ge \frac{1}{2} |\langle [\hat{L}_x, \hat{L}_y] \rangle| = \frac{1}{2} |\langle i\hbar \hat{L}_z \rangle| = \frac{\hbar}{2} |\langle \hat{L}_z \rangle| $$
这个下界直接取决于系统在所处状态下 $\hat{L}_z$ 的[期望值](@entry_id:153208)。在一个 $\hat{L}_z$ 的[本征态](@entry_id:149904) $|l, m\rangle$ 中，$\langle \hat{L}_z \rangle = \hbar m$。我们可以精确计算出 $\Delta L_x$ 和 $\Delta L_y$，得到不确定性乘积为 $\Delta L_x \Delta L_y = \frac{\hbar^2}{2}[l(l+1)-m^2]$。这个值显然依赖于[量子数](@entry_id:145558) $l$ 和 $m$。当 $l=0$ 时（因此 $m=0$），角动量的所有分量都为零，不确定性乘积的下界和实际值都为零 [@problem_id:1150515]。这与 $(x, p)$ 的情况形成鲜明对比，后者的不确定性乘积永远不能为零。

这个原理同样适用于由典范变量构造的其他算符对。例如，考虑[可观测量](@entry_id:267133) $\hat{A} = \hat{R} + \alpha \hat{P}_{R}$ 和 $\hat{B} = \hat{R} - \alpha \hat{P}_{R}$，其中 $[\hat{R}, \hat{P}_{R}] = i\hbar$。它们的对易子是 $[\hat{A}, \hat{B}] = -2i\alpha\hbar$，这是一个c-数。因此，它们的不确定性乘积有一个不依赖于状态的下界 $\Delta A \Delta B \ge |\alpha|\hbar$。这个下界在经典极限 $\hbar \to 0$ 时消失，反映了量子力学与经典力学之间的对应关系，即[量子对易子](@entry_id:194337)在 $\hbar \to 0$ 的极限下趋向于经典[泊松括号](@entry_id:151133) [@problem_id:2959695]。

### 时间-能量[不确定性关系](@entry_id:186128)

时间-能量[不确定性关系](@entry_id:186128)（TEUR）在形式上类似于位置-动量关系，但其物理内涵更为微妙，因为在标准（非相对论）量子力学中，时间是一个参数，而不是一个[厄米算符](@entry_id:153410)。

根据泡利定理 (Pauli's theorem)，对于一个能量谱有下界（即存在[基态](@entry_id:150928)）的物理系统，不可能存在一个与[哈密顿量](@entry_id:172864) $\hat{H}$ 满足典范对易关系 $[\hat{T}, \hat{H}] = i\hbar$ 的自伴时间算符 $\hat{T}$。如果这样的 $\hat{T}$ 存在，它将生成一个[酉群](@entry_id:138602) $e^{-is\hat{T}/\hbar}$，该[酉群](@entry_id:138602)能够将[能量本征值](@entry_id:144381)连续地平移任意量 $s$，这意味着[哈密顿量](@entry_id:172864)的谱必须是整个实轴 $\mathbb{R}$，这与物理系统的稳定性（能量有下界）相矛盾 [@problem_id:2959714]。

因此，TEUR 必须以其他方式来理解。有两种主流的、严谨的表述：

1.  **曼德尔施塔姆-塔姆关系 (Mandelstam-Tamm relation):** 这种表述将“时间不确定性” $\Delta t$ 定义为一个系统状态发生显著演化所需的[特征时间](@entry_id:173472)。对于一个不依赖于时间的可观测量 $\hat{A}$，其[特征时间](@entry_id:173472) $\Delta t_A$ 定义为它的[期望值](@entry_id:153208) $\langle \hat{A} \rangle$ 改变一个[标准差](@entry_id:153618) $\Delta A$ 所需的时间，即 $\Delta t_A = \frac{\Delta A}{|d\langle \hat{A} \rangle / dt|}$。利用广义的[埃伦费斯特定理](@entry_id:151868) $\frac{d}{dt}\langle \hat{A} \rangle = \frac{1}{i\hbar}\langle[\hat{A}, \hat{H}]\rangle$ 和罗伯逊关系，可以推导出：
    $$ \Delta E \cdot \Delta t_A \ge \frac{\hbar}{2} $$
    其中 $\Delta E$ 是系统的能量不确定性。这个关系表明，系统的能量越不确定，其状态演化得越快 [@problem_id:1150456]。

2.  **寿命-线宽关系 (Lifetime-Linewidth relation):** 对于不稳定的[量子态](@entry_id:146142)（如[激发态](@entry_id:261453)原子或[放射性核](@entry_id:756351)），其能量不是一个确定的值，而是遵循一个具有一定宽度的[分布](@entry_id:182848)，例如[布莱特-维格纳分布](@entry_id:746979) (Breit-Wigner distribution)。这个能量[分布](@entry_id:182848)的宽度 $\Gamma$ (Full Width at Half Maximum) 与该不稳定态的平均寿命 $\tau$ 之间存在一个基本关系 $\tau = \hbar/\Gamma$。如果我们定义能量不确定性为半高全宽 (Half Width at Half Maximum)，即 $\Delta E = \Gamma/2$，那么我们直接得到：
    $$ \Delta E \cdot \tau = \frac{\hbar}{2} $$
    这明确地体现了能量和时间之间的不确定性权衡：一个寿命很短的瞬时态，其能量必然是高度不确定的 [@problem_id:1150517]。这种关系本质上是时间演化函数与其[傅里叶变换](@entry_id:142120)（能量谱）之间宽度关系的体现 [@problem_id:2959714]。

### 拓扑、边界条件与不确定性

[不确定性关系](@entry_id:186128)的具体形式和有效性可能受到系统构型空间的拓扑和算符定义域的深刻影响。一个经典例子是比较直线上的粒子 $(\hat{x}, \hat{p})$ 与圆周上的粒子 $(\hat{\phi}, \hat{L}_z)$。

在无限直线 $\mathbb{R}$ 上，$\hat{x}$ 和 $\hat{p}$ 的谱都是连续的，并且可以严格地定义一个满足 $[\hat{x}, \hat{p}] = i\hbar$ 的自伴算符对，从而得到普适的 $\Delta x \Delta p \ge \hbar/2$ 界。

然而，在圆周 $S^1$ 上，情况变得复杂。[角动量算符](@entry_id:153013) $\hat{L}_z = -i\hbar d/d\phi$ 的本征函数必须是 $2\pi$ 周期的，这导致其谱是分立的（$\hbar m$, $m \in \mathbb{Z}$）。问题在于，我们无法在[周期函数](@entry_id:139337)的[希尔伯特空间](@entry_id:261193)上定义一个与 $\hat{L}_z$ 共轭的、表现良好的自伴角度算符 $\hat{\phi}$。一个简单的乘法算符 $\hat{\phi}$ 会破坏函数的周期性，导致其与 $\hat{L}_z$ 的定义域不匹配。因此，简单的[对易关系](@entry_id:136780) $[\hat{\phi}, \hat{L}_z] = i\hbar$ 在严格意义上是有问题的，并且不存在能够饱和 $\Delta\phi \Delta L_z = \hbar/2$ 的周期性[波函数](@entry_id:147440) [@problem_id:2959682]。

为了解决这个问题，发展了几种替代方案：
- **酉算符方法：** 考虑使用有界的酉算符 $\hat{E} = e^{i\phi}$。它与 $\hat{L}_z$ 满足对易关系 $[\hat{L}_z, \hat{E}] = \hbar \hat{E}$。由此推导出的[不确定性关系](@entry_id:186128)，其下界将依赖于状态的[期望值](@entry_id:153208)，如 $|\langle \hat{E} \rangle|$，后者是角度局域化的一个度量。
- **[分布](@entry_id:182848)对易子：** 将 $\hat{\phi}$ 定义为一个在 $(-\pi, \pi]$ 上的“[锯齿波](@entry_id:159756)”算符。其与 $\hat{L}_z$ 的对易子在[分布](@entry_id:182848)意义下包含一个狄拉克 $\delta$ 函数项，导致一个依赖于状态的罗伯逊界：$\Delta\phi\Delta L_z \ge \frac{\hbar}{2}|1 - 2\pi|\psi(\pi)|^2|$。
- **数-相不确定性：** 类似的问题也出现在[量子谐振子](@entry_id:140678)的**数算符** $\hat{N}$ 和**相算符** $\hat{\Phi}$ 之间。同样，不存在一个表现良好的厄米相算符。Susskind-Glogower 等人提出的方法是引入非酉的指数相算符 $\hat{E}$，从中可以推导出数-相[不确定性关系](@entry_id:186128)，例如 $\Delta N \Delta \Phi \ge 1/2$ [@problem_id:1150495]。

这些例子表明，在处理具有非[平凡拓扑](@entry_id:154009)或边界条件的系统时，必须谨慎地应用[不确定性原理](@entry_id:141278)。

### 现代诠释与推广

近年来，对[不确定性原理](@entry_id:141278)的理解已经超越了其最初的形式，发展出了更普适和深刻的表述。

#### [制备不确定性](@entry_id:203575) vs. 测量-干扰不确定性

海森堡最初的“伽马射线显微镜”思想实验模糊了两种截然不同的不确定性：
1.  **[制备不确定性](@entry_id:203575) (Preparation Uncertainty):** 这是[量子态](@entry_id:146142)的内在属性。罗伯逊-薛定谔关系 $\sigma_A^2 \sigma_B^2 \ge \dots$ 所描述的正是这种不确定性。它指的是，在对一个以同样方式制备的[全集](@entry_id:264200)进行测量时，不同可观测量的测量结果统计分布的弥散程度之间的关系。这个关系与具体的测量过程无关 [@problem_id:2959716]。一个设计拙劣的探测器可能会因为额外的技术噪声而报告比 $\sigma_x$ 大得多的结果[分布](@entry_id:182848)，但这并不违反[制备不确定性](@entry_id:203575)原理 [@problem_id:2959716]。
2.  **测量-干扰不确定性 (Measurement-Disturbance Uncertainty):** 这描述了一个测量过程的两个特性之间的权衡：测量的**误差** $\epsilon(A)$（即测量结果偏离[被测物](@entry_id:199209)理量真实值的程度）和它对另一个物理量 $B$ 造成的**干扰** $\eta(B)$（即测量后该物理量的值相较于测量前的改变程度）。海森堡的直觉是 $\epsilon(A)\eta(B) \ge \frac{1}{2}|\langle[A,B]\rangle|$。然而，现代[量子测量](@entry_id:272490)理论证明这个简单的形式并不普适。Ozawa 等人导出了一个严格普适的误差-干扰关系：
    $$ \epsilon(A)\eta(B) + \epsilon(A)\Delta B + \Delta A \eta(B) \ge \frac{1}{2}|\langle [A,B] \rangle| $$
    这个不等式正确地包含了系统初始态的内禀不确定性 $\Delta A$ 和 $\Delta B$，表明误差和干扰之间的权衡比海森堡最初想象的要复杂 [@problem_id:2959676]。

#### [熵不确定性关系](@entry_id:142360)

另一种现代的推广是从信息论的角度来表述不确定性，使用**香农熵** (Shannon entropy) 来量化不确定性，而不是[方差](@entry_id:200758)。[熵不确定性关系](@entry_id:142360)通常能为某些特殊状态提供比[方差](@entry_id:200758)形式更强的界。

- **[连续变量系统](@entry_id:144293)：** 对于位置和动量，**比亚韦尼茨基-比鲁拉-米切尔斯基 (Białynicki-Birula–Mycielski) 不等式**指出：
  $$ H(X) + H(P) \ge \ln(\pi e \hbar) $$
  其中 $H(X)$ 和 $H(P)$ 分别是位置和动量[概率分布](@entry_id:146404)的[微分熵](@entry_id:264893)。这个界的饱和当且仅当[波函数](@entry_id:147440)是高斯函数时达到 [@problem_id:2959693]。

- **有限维系统：** 对于一个 $d$ 维系统中的两个[可观测量](@entry_id:267133) $A$ 和 $B$，其本征基分别为 $\{|a_j\rangle\}$ 和 $\{|b_k\rangle\}$，**马森-乌芬克 (Maassen-Uffink) [不确定性关系](@entry_id:186128)**给出：
  $$ H(A) + H(B) \ge \ln\left(\frac{1}{c}\right) \quad \text{其中 } c = \max_{j,k} |\langle a_j|b_k\rangle|^2 $$
  这里的 $H(A)$ 和 $H(B)$ 是测量结果的离散香non熵，$c$ 是两个基之间最大交叠的平方。例如，对于一个[三能级系统](@entry_id:147049)，如果两个基是标准基和离散傅里叶变换基，它们是“相互无偏”的，此时 $c=1/3$，[熵不确定性](@entry_id:148835)下界为 $\ln(3)$ [@problem_id:349020]。

- **含[量子存储器](@entry_id:144642)的[熵不确定性](@entry_id:148835)：** 最前沿的进展将[不确定性原理](@entry_id:141278)扩展到包含[量子纠缠](@entry_id:136576)的场景中。如果测量系统 A 的同时，观察者拥有一个与之纠缠的[量子存储器](@entry_id:144642) B，那么对 A 的测量结果的不确定性可以降低。这种情况下，[熵不确定性关系](@entry_id:142360)的下界由系统 A 和存储器 B 之间的条件[冯·诺依曼熵](@entry_id:143216) $S(A|B)$ 和测量的不相容性共同决定 [@problem_id:349022]：
  $$ H(X|B) + H(Z|B) \ge S(A|B) + \ln\left(\frac{1}{c}\right) $$
  这个关系在[量子密码学](@entry_id:144827)等领域有重要应用。

#### [广义不确定性原理](@entry_id:161890)

在量子引力的探索中，一些理论提出，在[普朗克尺度](@entry_id:145654)附近，时空本身可能存在一种“泡沫”结构，导致一个绝对的最小可测量长度。这可以通过修改典范[对易关系](@entry_id:136780)来实现，即所谓的**[广义不确定性原理](@entry_id:161890)** (Generalized Uncertainty Principle, GUP)。例如，考虑一个修正的[对易关系](@entry_id:136780)：
$$ [\hat{X}, \hat{P}] = i\hbar (1 + \beta \hat{P}^2) $$
其中 $\beta$ 是一个正的小参数。应用罗伯逊关系，对于一个 $\langle\hat{P}\rangle=0$ 的状态，我们得到一个修正的[不确定性关系](@entry_id:186128)：
$$ \Delta X \Delta P \ge \frac{\hbar}{2} (1 + \beta (\Delta P)^2) $$
这个关系式可以被改写为 $\Delta X \ge \frac{\hbar}{2\Delta P} + \frac{\hbar\beta}{2}\Delta P$。这个关于 $\Delta X$ 的表达式有一个最小值，当 $(\Delta P)^2 = 1/\beta$ 时达到，最小值为 $\Delta X_{min} = \hbar\sqrt{\beta}$。这表明，与标准量子力学不同，存在一个无法逾越的最小位置不确定性，即最小长度 [@problem_id:1150439]。这为在可观测效应中寻找量子引力现象提供了一个可能的方向。