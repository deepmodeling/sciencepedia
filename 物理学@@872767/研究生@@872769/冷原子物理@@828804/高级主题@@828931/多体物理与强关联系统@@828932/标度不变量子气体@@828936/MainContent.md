## 引言
[标度不变性](@entry_id:180291)是物理学中一个深刻而优美的对称性原理，它描述了物理规律在尺度缩放下的[不变性](@entry_id:140168)。在强关联[量子多体系统](@entry_id:141221)中，当传统的微扰理论失效时，利用对称性原理往往成为理解其复杂行为的关键。标度不变量子气体，特别是处于幺正极限的费米气体，正是这样一个理想的研究平台。由于系统中缺乏内禀的相互作用长度标度，其性质呈现出高度的普适性，为检验和发展我们对多体物理的基本理解提供了前所未有的机遇。本文旨在系统性地阐述标度不变量子气体的核心概念及其广泛应用。

在接下来的内容中，我们将分三步深入这一迷人的领域。首先，在“原理与机制”一章中，我们将奠定理论基础，从[标度不变性](@entry_id:180291)的严格定义出发，探讨其对[热力学](@entry_id:141121)和动力学的深刻影响，并介绍[幺正费米气体](@entry_id:160541)、Tan接触度、动力学对称性等关键概念。随后，“应用与跨学科[交叉](@entry_id:147634)”一章将展示这些抽象原理的强大威力，探索它们如何解释超流输运现象，并如何作为桥梁，连接凝聚态物理、[量子临界性](@entry_id:143927)、类比[引力](@entry_id:175476)乃至弦论等看似无关的领域。最后，通过“动手实践”环节，读者将有机会通过解决具体问题来巩固和深化对这些核心物理思想的理解。

## 原理与机制

在上一章引言的基础上，本章将深入探讨标度不变量子气体的核心物理原理与基本机制。我们将从[标度不变性](@entry_id:180291)的严格定义出发，推导其普适的[热力学与动力学](@entry_id:146887)推论，并借助[幺正费米气体](@entry_id:160541)这一典型范例，阐释这些原理如何在具体的物理系统中得以体现。我们将重点介绍Tan接触度、动力学对称性以及[量子反常](@entry_id:146580)等关键概念，它们共同构成了理解此类强关联[量子多体系统](@entry_id:141221)的理论基石。

### 标度不变性的定义与推论

[标度不变性](@entry_id:180291)是物理学中的一个基本对称性概念。一个物理系统如果具有[标度不变性](@entry_id:180291)，意味着其物理规律在空间尺度（或等效地，能量尺度）的缩放下保持形式不变。对于一个由质量为 $m$ 的粒子构成的非相对论量子系统，其[哈密顿量](@entry_id:172864)通常可以写成动能 $T$、外势 $V_{\text{ext}}$ 和相互作用势 $V_{\text{int}}$ 之和：$H = T + V_{\text{ext}} + V_{\text{int}}$。

考虑一个均匀的坐标标度变换 $\mathbf{r}_i \to \lambda \mathbf{r}_i$，其中 $\lambda$ 是一个无量纲的标度因子。在此变换下，[动能算符](@entry_id:265633)中的梯度变换为 $\nabla_i \to \lambda^{-1} \nabla_i$，因此动能的[期望值](@entry_id:153208)变换为 $\langle T \rangle \to \lambda^{-2} \langle T \rangle$。如果相互作用势 $V_{\text{int}}$ 是坐标的 $-2$ 次齐次函数，即 $V_{\text{int}}(\lambda \mathbf{r}_1, \dots, \lambda \mathbf{r}_N) = \lambda^{-2} V_{\text{int}}(\mathbf{r}_1, \dots, \mathbf{r}_N)$，那么相互作用能也同样变换：$\langle V_{\text{int}} \rangle \to \lambda^{-2} \langle V_{\text{int}} \rangle$。满足此条件的相互作用包括三维空间中的 $1/r^2$ 势，以及一个至关重要的例子——在幺正极限（unitary limit）下的零程[接触相互作用](@entry_id:150822)。当一个系统的动能和相互作用能都以 $\lambda^{-2}$ 形式标度时，我们就称该系统（在没有外场时）具有 **标度不变性**。

这一对称性最直接、最强大的推论之一是 **[维里定理](@entry_id:146441) (Virial Theorem)**。对于任何束缚[定态](@entry_id:137260)，系统总能量的[期望值](@entry_id:153208) $E = \langle H \rangle$ 在任意[标度变换](@entry_id:166413)下都应保持[极值](@entry_id:145933)，即 $\frac{dE(\lambda)}{d\lambda}|_{\lambda=1} = 0$。考虑一个被囚禁在谐振子势 $V_{\text{ext}} = \frac{1}{2} m \omega^2 \sum_{i=1}^N |\mathbf{r}_i|^2$ 中的标度不变气体。外势能的[期望值](@entry_id:153208)标度为 $\langle V_{\text{ext}} \rangle \to \lambda^2 \langle V_{\text{ext}} \rangle$。因此，总能量的标度行为是：
$$ E(\lambda) = \lambda^{-2} \langle T + V_{\text{int}} \rangle + \lambda^{2} \langle V_{\text{ext}} \rangle $$
对其求导并令 $\lambda=1$，我们得到：
$$ \frac{dE(\lambda)}{d\lambda}\Big|_{\lambda=1} = -2 \langle T + V_{\text{int}} \rangle + 2 \langle V_{\text{ext}} \rangle = 0 $$
由此我们立即获得一个深刻的关系：$2 \langle V_{\text{ext}} \rangle = 2 \langle T + V_{\text{int}} \rangle$。这意味着系统的外势能等于动能与相互作用能之和。进而，我们可以计算总能量：
$$ E = \langle T + V_{\text{int}} \rangle + \langle V_{\text{ext}} \rangle = \langle V_{\text{ext}} \rangle + \langle V_{\text{ext}} \rangle = 2 \langle V_{\text{ext}} \rangle $$
对于谐振子势，$\langle V_{\text{ext}} \rangle = \frac{1}{2} m \omega^2 \sum_{i=1}^N \langle |\mathbf{r}_i|^2 \rangle = \frac{1}{2} m \omega^2 \langle R^2 \rangle$，其中 $\langle R^2 \rangle$ 是粒子云的总[均方半径](@entry_id:146552)。代入上式，我们得到一个不依赖于[粒子统计](@entry_id:145640)、温度或相互作用细节的普适关系：
$$ E = m \omega^2 \langle R^2 \rangle $$
这个结果极为优美，它将系统的总能量这一[热力学](@entry_id:141121)量与粒子云的尺寸这一结构量直接联系起来，是[标度不变性](@entry_id:180291)的一个标志性体现。这个关系对于系统的任何[定态](@entry_id:137260)（包括热平衡态）都成立。[@problem_id:1265850]

### [幺正费米气体](@entry_id:160541)：[标度不变性](@entry_id:180291)的范例

三维空间中自旋-1/2[费米子](@entry_id:146235)之间的零程相互作用，当其s波[散射长度](@entry_id:142881) $a_s$ 通过Feshbach共振等技术被调节至无穷大时（$a_s \to \infty$），系统进入所谓的 **幺正极限**。在此极限下，相互作用没有内禀的长度标度（[散射长度](@entry_id:142881)发散）和能量标度，系统展现出完美的[标度不变性](@entry_id:180291)。这种 **[幺正费米气体](@entry_id:160541)** 是研究标度[不变量](@entry_id:148850)子多体物理最理想的实验平台。

#### 普适方程和[集体激发](@entry_id:145026)

在幺正极限下，均匀费米气体的所有[热力学性质](@entry_id:146047)都具有普适性。在零温下，系统的总能量 $E$ 只能与系统中唯一相关的能量标度——无[相互作用费米气体](@entry_id:160307)的能量 $E_{FG}$——成正比。其比例系数是一个普适的无量纲常数，称为 **[Bertsch参数](@entry_id:159019)** $\xi$：
$$ E = \xi E_{FG} $$
对于一个密度为 $n$ 的自旋平衡（$n_\uparrow = n_\downarrow = n/2$）的均匀[费米气体](@entry_id:145305)，其能量密度 $\mathcal{E}(n) = E/V$ 与[费米能](@entry_id:143977)量 $\epsilon_F = \frac{\hbar^2}{2m}(3\pi^2 n)^{2/3}$ 的关系为：
$$ \mathcal{E}(n) = \xi \mathcal{E}_{FG}(n) = \xi \left( \frac{3}{5} n \epsilon_F \right) = \xi \frac{3\hbar^2}{10m} (3\pi^2)^{2/3} n^{5/3} $$
这个普适的 **[状态方程](@entry_id:274378) (equation of state)** 是[幺正费米气体](@entry_id:160541)理论的基石。实验上测得 $\xi \approx 0.37$。

利用标准[热力学](@entry_id:141121)关系，我们可以从能量密度导出其他[热力学](@entry_id:141121)量。例如，零温下的压强 $P$ 为：
$$ P = n \frac{\partial \mathcal{E}}{\partial n} - \mathcal{E} = n \left( \frac{5}{3} \mathcal{E}/n \right) - \mathcal{E} = \frac{2}{3} \mathcal{E} $$
这个 $P = \frac{2}{3}\mathcal{E}$ 的关系是任何标度不变非相对论气体在三维空间中的普适结果。

我们还可以计算系统的[集体激发](@entry_id:145026)谱，例如声速 $c_s$。声速由压强对密度的响应决定，$c_s^2 = \frac{1}{m} \frac{\partial P}{\partial n}$。利用上述压强和能量密度的关系，我们得到：
$$ c_s^2 = \frac{1}{m} \frac{\partial}{\partial n} \left( \frac{2}{3} \mathcal{E} \right) = \frac{1}{m} \frac{\partial}{\partial n} \left( \xi \frac{\hbar^2}{5m} (3\pi^2)^{2/3} n^{5/3} \right) = \frac{\xi}{3} \frac{\hbar^2}{m^2} (3\pi^2 n)^{2/3} = \frac{\xi}{3} v_F^2 $$
其中 $v_F = \frac{\hbar k_F}{m} = \frac{\hbar}{m}(3\pi^2 n)^{1/3}$ 是费米速度。因此，声速为：
$$ c_s = v_F \sqrt{\frac{\xi}{3}} = \frac{\hbar}{m}(3\pi^2 n)^{1/3}\sqrt{\frac{\xi}{3}} $$
这个结果将宏观的声速与微观的[Bertsch参数](@entry_id:159019) $\xi$ 直接联系起来，为实验测量 $\xi$ 提供了重要途径。[@problem_id:1265946]

#### [局域密度近似](@entry_id:138982)

实验中的[冷原子气体](@entry_id:136262)通常被囚禁在谐振子势中，密度[分布](@entry_id:182848)是不均匀的。为了将均匀气体的理论成果应用于囚禁系统，我们采用 **局域密度近似 (Local Density Approximation, LDA)**。LDA的核心思想是，如果[势场](@entry_id:143025)变化足够缓慢，那么在空间中每一点 $\mathbf{r}$ 的局域物理性质可以看作是密度为 $n(\mathbf{r})$ 的均匀气体的性质。在热力学平衡中，全局化学势 $\mu_0$ 是一个常数。在位置 $\mathbf{r}$，粒子感受到的有效化学势是 $\mu(\mathbf{r}) = \mu_0 - V_{\text{ext}}(\mathbf{r})$。LDA假设这个局域有效化学势就等于密度为 $n(\mathbf{r})$ 的均匀气体的化学势 $\mu_{\text{unif}}(n(\mathbf{r}))$。

对于零温[幺正费米气体](@entry_id:160541)，$\mu_{\text{unif}}(n) = \frac{\partial \mathcal{E}}{\partial n} = \xi \epsilon_F(n)$。因此，在[谐振子势](@entry_id:750179) $V_{\text{ext}}(r) = \frac{1}{2}m\omega^2 r^2$ 中，我们有：
$$ \mu_0 - \frac{1}{2}m\omega^2 r^2 = \xi \frac{\hbar^2}{2m}(3\pi^2 n(r))^{2/3} $$
从这个方程可以解出密度[分布](@entry_id:182848) $n(r)$。将 $n(r)$ 在全空间积分 $\int n(r) d^3r$ 并使其等于总粒子数 $N$，我们就可以反解出trap中心的化学势 $\mu_0$。经过计算可得：
$$ \mu_0 = \hbar\omega\,\xi^{1/2}(3N)^{1/3} $$
这个结果巧妙地结合了[原子数](@entry_id:746561) $N$、囚禁频率 $\omega$ 和普适的[Bertsch参数](@entry_id:159019) $\xi$，展示了如何从第一性原理出发，预测囚禁系统中可测量的宏观量。[@problem_id:1265834]

### 短程物理与[算符乘积展开](@entry_id:141941)：Tan接触

尽管幺正极限下的相互作用是零程的，但其物理效应却并非无足轻重。其奥秘在于，[多体波函数](@entry_id:203043)在两个不同自旋的[费米子](@entry_id:146235)彼此靠近时（$\mathbf{r}_{ij} = \mathbf{r}_i - \mathbf{r}_j \to 0$）表现出一种普适的奇异行为。这种行为可以用[算符乘积展开](@entry_id:141941)（Operator Product Expansion, OPE）的思想来理解，其核心是[多体波函数](@entry_id:203043)在短距离下的渐近形式：
$$ \Psi(\dots, \mathbf{r}_i, \dots, \mathbf{r}_j, \dots) \xrightarrow{r_{ij}\to 0} \frac{A_{ij}(\mathbf{R}_{ij}, \{\text{other}\})}{r_{ij}} + \text{regular terms} $$
其中 $\mathbf{R}_{ij}$ 是这对粒子的[质心](@entry_id:265015)坐标，$\{\text{other}\}$ 代表其他所有粒子的坐标。函数 $A_{ij}$ 在 $r_{ij} \to 0$ 时是正则的。这个 $1/r_{ij}$ 的[奇点](@entry_id:137764)结构正是强相互作用的体现。

Shina Tan发现，一个名为 **接触度密度 (Contact Density)** 的单一量 $C$ 捕捉了所有这些短程奇异行为的强度，并支配了一系列普适关系。接触度密度是一个局域[热力学](@entry_id:141121)量，它量化了单位体积内“紧密接触”的不同自旋粒子对的数量。

Tan接触度的重要性在于它将不可见的[短程关联](@entry_id:158693)与一系列可测量的宏观量联系起来：

**动量分布的高动量尾：** [波函数](@entry_id:147440)在实空间的[奇点](@entry_id:137764)通过[傅里叶变换](@entry_id:142120)，会转化为[动量空间](@entry_id:148936)中的[幂律](@entry_id:143404)行为。上述 $1/r$ 的[奇点](@entry_id:137764)直接导致了单粒子动量分布 $n(k)$ 在大动量 $k \to \infty$ 时呈现一个普适的 $k^{-4}$ 尾巴。对于自旋平衡体系，其精确形式为：
$$ n(k) \approx \frac{C}{k^4} $$
这意味着通过测量粒子动量分布的高能翼，可以直接测得接触度密度 $C$。这个[幂律](@entry_id:143404)尾是强相互作用的直接证据。[@problem_id:1265876]

**[静态结构因子](@entry_id:141682)：** 接触度也决定了对关联函数 $g_{\uparrow\downarrow}(r)$ 在短距离 $r \to 0$ 处的行为。具体而言，$g_{\uparrow\downarrow}(r) \propto C/r^2$。通过[傅里叶变换](@entry_id:142120)，这一行为反映在[静态结构因子](@entry_id:141682) $S(q)$ 的大波矢 $q \to \infty$ 行为上。$S(q)$ 描述了系统对密度探针的响应。对于一个自旋平衡的气体，当 $q \to \infty$ 时，$S(q)$ 趋近于1，其渐近形式为：
$$ S(q) = 1 + \frac{C}{nq} + o(q^{-1}) $$
其中 $n$ 是总粒子[数密度](@entry_id:268986)。这个 $1/q$ 的尾巴也是一个可以直接测量并用于确定接触度的普适关系。[@problem_id:1265899]

**绝热关系：** Tan接触度不仅是一个结构参数，还是一个关键的[热力学](@entry_id:141121)参数。它与散射长度 $a_s$ 的倒数 $1/a_s$ 形成一个[共轭变量](@entry_id:147843)对。Tan导出了一个精确的[绝热定理](@entry_id:142116)，描述了当缓慢改变散射长度时系统能量密度的变化率：
$$ \frac{d\mathcal{E}}{d(1/a_s)} = -\frac{\hbar^2 C}{4\pi m} $$
这个关系式意义非凡。它表明，接触度密度 $C$ 衡量了系统能量对偏离幺正极限（即打破标度不变性）的敏感度。我们可以利用此定理计算当系统从幺正极限（$1/a_s=0$）微扰到一个小的 $1/a_s$ 值时能量密度的变化 $\Delta \mathcal{E}$。如果接触度在 $1/a_s$ 附近有展开式 $C(1/a_s) = C_0 + C_1 (1/a_s) + \dots$，其中 $C_0$ 是幺正极限下的接触度密度，积分上式可得：
$$ \Delta \mathcal{E} = -\frac{\hbar^2}{4\pi m} \int_0^{1/a_s} C(\lambda) d\lambda = -\frac{\hbar^2 C_0}{4\pi m a_s} - \frac{\hbar^2 C_1}{8\pi m a_s^2} + \dots $$
这为通过能量测量来研究接触度提供了理论基础。[@problem_id:1265849]

### 动力学与[离散标度对称性](@entry_id:159453)

[标度不变性](@entry_id:180291)不仅决定了系统的静态[热力学性质](@entry_id:146047)，还蕴含着深刻的动力学对称性。

#### SO(2,1) 动力学对称性与呼吸模

对于囚禁在[谐振子势](@entry_id:750179)中的标度不变气体，系统的对称性实际上从简单的标度不变性提升为一个更强大的 **SO(2,1) 动力学对称性**。这个对称性代数由三个多体算符生成：
1.  相对[哈密顿量](@entry_id:172864)：$\mathcal{H}_0 = T + V_{\text{int}}$
2.  惯性矩算符：$\mathcal{C} = \frac{m}{2} \sum_i |\mathbf{r}_i|^2$
3.  标度变换生成元（膨胀算符）：$\mathcal{D} = \frac{1}{2} \sum_i (\mathbf{r}_i \cdot \mathbf{p}_i + \mathbf{p}_i \cdot \mathbf{r}_i)$

这三个算符的对易关系构成了一个封闭的so(2,1)李代数。囚禁系统的总[哈密顿量](@entry_id:172864)为 $H = \mathcal{H}_0 + \omega^2 \mathcal{C}$。利用[海森堡运动方程](@entry_id:140445)，我们可以推导出这些算符[期望值的时间演化](@entry_id:153265)[方程组](@entry_id:193238)。对 $\langle \mathcal{C}(t) \rangle$ 求二阶时间导数，并利用总能量 $E = \langle H \rangle$ 守恒，可以得到一个关于粒子云尺寸平方 $\langle \mathcal{C}(t) \rangle$ 的[二阶常微分方程](@entry_id:204212)：
$$ \frac{d^2}{dt^2}\langle \mathcal{C} \rangle + (2\omega)^2 \langle \mathcal{C} \rangle = \frac{2E}{m} $$
这是一个[受驱振子](@entry_id:163906)的方程。其齐次解描述了系统尺寸的[集体振荡](@entry_id:158973)，即 **呼吸模 (breathing mode)**。从方程中可以立刻读出，这个[振荡](@entry_id:267781)模式的频率精确为 $\omega_B = 2\omega$。这是一个非常强的非微扰结果，它不依赖于相互作用的强度（只要是标度不变的）、温度或[粒子统计](@entry_id:145640)。这个模式频率是标度不变性的精确动力学指纹，已在冷原子实验中被精确验证。[@problem_id:1265878]

#### [离散标度不变性](@entry_id:180622)与[Efimov效应](@entry_id:159916)

除了连续标度不变性，还存在一种更奇特的 **[离散标度不变性](@entry_id:180622)**。其最著名的例子是 **[Efimov效应](@entry_id:159916)**。考虑一个[三体系统](@entry_id:186069)（例如三个相同的[玻色子](@entry_id:138266)，或两重一轻的粒子组合），当任意两体间的相互作用都处于共振状态（$|a_s| \to \infty$）时，即使没有稳定的[二体束缚态](@entry_id:189696)，也可能出现无穷多个三体束缚态（Efimov三聚体）。

这些三体束缚态的能谱 $E_n$ 并非[连续分布](@entry_id:264735)，而是遵循一个[几何级数](@entry_id:158490)：
$$ E_{n+1} / E_n = \exp(-2\pi/s_0) $$
其中 $s_0$ 是一个普适的无量纲数，只依赖于粒子的[质量比](@entry_id:167674)和统计性质。这种[几何级数](@entry_id:158490)的出现，正是一种[离散标度不变性](@entry_id:180622)的体现：系统在特定的标度因子 $\exp(\pi/s_0)$ 变换下看起来是相同的。

这种行为的根源在于，在超[径向坐标](@entry_id:165186) $R$（衡量[三体系统](@entry_id:186069)整体尺寸）下，有效的相互作用势在长程呈现 $V_{\text{eff}}(R) = -\frac{\hbar^2(s_0^2+1/4)}{2mR^2}$ 的形式。这是一个标度不变的 $1/R^2$ 吸引势。对于这类势能，维里定理同样适用。对于一个能量为 $E = -E_B  0$ 的深束缚[Efimov态](@entry_id:158901)，可以证明其超径向动能 $\langle T_R \rangle = \langle -\frac{\hbar^2}{2m} \frac{d^2}{dR^2} \rangle$ 和束缚能 $E_B$ 之间存在一个简单的关系：
$$ \langle T_R \rangle = E_B $$
即动能恰好等于束缚能的大小。[@problem_id:1265822]

[Efimov效应](@entry_id:159916)的出现与否对质量比非常敏感。例如，在两重（质量$m$）一轻（质量$M$）的系统中，只有当[质量比](@entry_id:167674) $M/m$ 大于某个临界值时，[Efimov效应](@entry_id:159916)才会出现。这个[临界点](@entry_id:144653)可以通过求解一个决定标度因子 $s$ 的[超越方程](@entry_id:276279)在 $s \to 0$ 时的行为来确定。对于一个特定的模型方程 $\sqrt{M/m} \sin(\pi s/2) = \sinh(A s/2)$，在$s\to0$时展开两边可得临界质量比为 $(M/m)_{crit} = A^2/\pi^2$。[@problem_id:1265959]

### [标度不变性](@entry_id:180291)的破缺：[量子反常](@entry_id:146580)

最后，值得注意的是，一个在经典层面具有[标度不变性](@entry_id:180291)的理论，在量子化之后其对称性可能会被破坏。这种现象称为 **[量子反常](@entry_id:146580) (Quantum Anomaly)**。

一个经典的例子是二维[玻色气体](@entry_id:155364)中的[接触相互作用](@entry_id:150822)。在经典力学中，一个二维零程势是标度不变的，根据维里定理，我们期望系统的压强 $P$ 和能量密度 $\mathcal{E}$ 满足 $P=\mathcal{E}$。然而，在量子力学中，为了定义零程相互作用，必须进行正规化（regularization）和[重整化](@entry_id:143501)（renormalization）的过程。这个过程不可避免地会引入一个长度尺度，即二维散射长度 $a_{2D}$。这个内在尺度的出现破坏了系统的连续标度不变性。这个过程也被称为 **维度嬗变 (dimensional transmutation)**，即一个无量纲的[耦合常数](@entry_id:747980)被一个有量纲的尺度（$a_{2D}$）所取代。

对称性的破缺直接反映在状态方程上。对于一个[弱相互作用](@entry_id:157579)的二维[玻色气体](@entry_id:155364)，其零温能量密度为：
$$ \mathcal{E}(n) = \frac{2\pi\hbar^2 n^2}{m \ln(1/(na_{2D}^2))} $$
其中 $n$ 是[面密度](@entry_id:161889)。我们可以通过[热力学](@entry_id:141121)关系 $P = n\mu - \mathcal{E}$ (其中 $\mu = \partial\mathcal{E}/\partial n$) 来计算压强。经过计算，我们发现压强与能量密度的比值为：
$$ \frac{P}{\mathcal{E}} = 1 + \frac{1}{\ln(1/(na_{2D}^2))} $$
这个结果清楚地表明，$P \neq \mathcal{E}$。偏离经典关系 $P=\mathcal{E}$ 的修正项 $\frac{1}{\ln(1/(na_{2D}^2))}$ 正是[量子反常](@entry_id:146580)的直接后果。只有在密度趋于零的极限下 $n \to 0$，这个修正项才消失，系统恢复经典行为。这为在实验中观测和量化[量子反常](@entry_id:146580)提供了坚实的理论基础。[@problem_id:1265852]