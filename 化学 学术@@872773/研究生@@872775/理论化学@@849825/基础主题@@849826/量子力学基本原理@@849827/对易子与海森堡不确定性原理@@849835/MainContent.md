## 引言
对易子与海森堡不确定性原理是量子力学的基石，深刻地塑造了我们对微观世界的理解，尤其是在[理论化学](@entry_id:199050)领域。这些概念超越了简单的数学公式，它们揭示了[物理可观测量](@entry_id:154692)之间内在的、不可避免的相互制约关系。然而，从基础的对易关系 $[\hat{x}, \hat{p}] = i\hbar$ 到其在复杂分子系统和前沿[材料科学](@entry_id:152226)中的深远应用，存在一个需要通过严谨理论和广泛实例来填补的认知鸿沟。

本文旨在系统地构建这一知识体系。我们将从第一章**“原理与机制”**出发，深入探讨[量子算符](@entry_id:137703)的数学基础，严格推导不对易性如何直接导致[不确定性原理](@entry_id:141278)。接着，在第二章**“应用与[交叉](@entry_id:147634)学科联系”**中，我们将展示这些抽象原理如何转化为解释[量子动力学](@entry_id:138183)、[分子结构](@entry_id:140109)、[光谱选择定则](@entry_id:139860)和凝聚态现象的强大工具。最后，通过**“动手实践”**部分提供的一系列练习，读者将有机会将理论知识付诸实践，加深对核心概念的掌握。通过这一结构化的学习路径，本文将带领读者领略对易子与[不确定性原理](@entry_id:141278)的理论深度与实践广度。

## 原理与机制

在[量子化学](@entry_id:140193)的理论框架中，[物理可观测量](@entry_id:154692)由作用于系统[希尔伯特空间](@entry_id:261193)上的算符表示。这些算符之间的代数关系，特别是它们的[对易关系](@entry_id:136780)，不仅深刻地揭示了不同物理量之间的内在联系，还直接导出了量子力学中最具标志性的结论之一——[海森堡不确定性原理](@entry_id:171099)。本章旨在深入探讨算符对易性的数学基础及其物理后果，从严谨的算符理论出发，系统地建立起对易子与[不确定性原理](@entry_id:141278)之间的桥梁，并讨论在[理论化学](@entry_id:199050)中遇到的一些重要且微妙的情形。

### [量子算符](@entry_id:137703)的数学基础

为了精确地讨论量子力学，我们必须首先建立一个严格的数学框架。系统的状态由[复希尔伯特空间](@entry_id:185216) $\mathcal{H}$ 中的矢量（[波函数](@entry_id:147440)）描述。在多电子分子体系中，这个空间通常是 $L^2(\mathbb{R}^{3N}, \mathbb{C})$，即 $N$ 电子坐标上的平方可积复函数空间。

#### 线性算符及其定义域

一个**线性算符** $\hat{A}$ 是一个映射，它将其定义域 $\mathcal{D}(\hat{A}) \subset \mathcal{H}$ 中的矢量线性地变换到 $\mathcal{H}$ 中的另一个矢量。即对于任意 $|\psi\rangle, |\phi\rangle \in \mathcal{D}(\hat{A})$ 和复数 $\alpha, \beta$，满足 $\hat{A}(\alpha |\psi\rangle + \beta |\phi\rangle) = \alpha \hat{A}|\psi\rangle + \beta \hat{A}|\phi\rangle$。

在量子力学中，**定义域** $\mathcal{D}(\hat{A})$ 的概念至关重要，尤其是在处理[微分](@entry_id:158718)算符时。例如，动量算符 $\hat{p}_x = -i\hbar \frac{\partial}{\partial x}$ 不能作用于任意一个[平方可积函数](@entry_id:200316)上，因为其导数可能不再是平方可积的。因此，我们必须将其定义域限制在一个合适的函数[子空间](@entry_id:150286)上，例如[施瓦茨空间](@entry_id:266248) $\mathcal{S}(\mathbb{R})$（无穷可微且快速衰减的[函数空间](@entry_id:143478)），这是一个在 $\mathcal{H}$ 中稠密的[子空间](@entry_id:150286)。

#### 有界与无界算符

根据算符对其作用的矢量范数的影响，算符可以分为**有界算符**和**无界算符**。一个线性算符 $\hat{A}$ 是有界的，如果存在一个有限的常数 $M$，使得对于其定义域中所有的 $|\psi\rangle$，不等式 $\|\hat{A}|\psi\rangle\| \le M \, \||\psi\rangle\|$ 恒成立。否则，该算符是无界的。

在[量子化学](@entry_id:140193)中，许多核心算符都是无界的。例如，位置算符 $\hat{x}$ 和[动量算符](@entry_id:151743) $\hat{p}$ 都是无界算符。我们可以通过一个具体的例子来理解动量算符的无界性 [@problem_id:2765389]。考虑一维空间中的归一化[高斯波包](@entry_id:151158) $g_\lambda(x) = (\lambda/\pi)^{1/4} \exp(-\lambda x^2/2)$。它的范数 $\|g_\lambda\| = 1$。[动量算符](@entry_id:151743)作用于其上，得到的结果的范数平方为 $\|\hat{p} g_\lambda\|^2 = \langle \hat{p} g_\lambda | \hat{p} g_\lambda \rangle = \langle g_\lambda | \hat{p}^2 | g_\lambda \rangle = \hbar^2 \lambda/2$。因此，$\|\hat{p} g_\lambda\| = \hbar \sqrt{\lambda/2}$。通过增大参数 $\lambda$（即使[波包](@entry_id:154698)在空间上更局域化），我们可以使 $\|\hat{p} g_\lambda\|$ 的值任意大。这意味着不存在一个统一的常数 $M$ 来约束 $\|\hat{p}|\psi\rangle\|$ 与 $\||\psi\rangle\|$ 的比值，因此 $\hat{p}$ 是无界的。相反，在[量子化学](@entry_id:140193)计算中常用的、投影到有限[高斯基组](@entry_id:198430)[子空间](@entry_id:150286)上的**正交投影算符** $\hat{P}_\mathcal{B}$ 是有界的，其算符范数为1，因为投影操作不会增加矢量的长度。

#### 伴随算符与自伴算符

对于一个在[稠密子空间](@entry_id:261392) $\mathcal{D}(\hat{A})$ 上定义的算符 $\hat{A}$，我们可以定义其**伴随算符**（或称[埃尔米特共轭](@entry_id:191215)算符）$\hat{A}^\dagger$。$\hat{A}^\dagger$ 的定义域 $\mathcal{D}(\hat{A}^\dagger)$ 包含所有满足如下条件的矢量 $|\phi\rangle \in \mathcal{H}$：存在一个矢量 $|\chi\rangle \in \mathcal{H}$，使得对于所有 $|\psi\rangle \in \mathcal{D}(\hat{A})$，都有 $\langle \phi | \hat{A} \psi \rangle = \langle \chi | \psi \rangle$。此时，我们定义 $\hat{A}^\dagger |\phi\rangle = |\chi\rangle$。这个定义等价于在[狄拉克符号](@entry_id:154811)中更为人熟知的形式 [@problem_id:2765389]：
$$
\langle \phi | \hat{A} \psi \rangle = \langle \hat{A}^\dagger \phi | \psi \rangle
$$
或者对于[矩阵元](@entry_id:186505)：
$$
(\langle \phi | \hat{A} | \psi \rangle)^* = \langle \psi | \hat{A}^\dagger | \phi \rangle
$$

如果一个算符 $\hat{A}$ 满足 $\langle \phi | \hat{A} \psi \rangle = \langle \hat{A} \phi | \psi \rangle$ 对其定义域中所有元素都成立，则称其为**对称算符**。如果一个对称算符的定义域与其伴随算符的定义域相同，即 $\mathcal{D}(\hat{A}) = \mathcal{D}(\hat{A}^\dagger)$，则该算符称为**自伴算符**（或[埃尔米特算符](@entry_id:153410)）。物理可观测量必须由自伴算符表示，这保证了其[本征值](@entry_id:154894)（即测量结果）是实数，并且它能够作为[幺正时间演化](@entry_id:192535)[群的生成元](@entry_id:137215)。

对于定义在某个[稠密子空间](@entry_id:261392)（称为一个**核**）上的对称算符，如果它只有一个[自伴扩张](@entry_id:264525)，则称其为**本质自伴的**。这时，其闭包就是一个自伴算符。例如，动量算符 $\hat{p} = - i \hbar \frac{d}{dx}$ 在 $C_0^\infty(\mathbb{R})$（[紧支撑](@entry_id:276214)的无穷可微函数）上是本质自伴的，其[亏指数](@entry_id:266905)为 $(0,0)$。它的唯一[自伴扩张](@entry_id:264525)是在索伯列夫空间 $H^1(\mathbb{R})$ 上定义的算符。根据[斯通定理](@entry_id:262301)，这个自伴的动量算符是空间平移幺正群 $U(a) = \exp(-ia\overline{\hat{p}}/\hbar)$ 的生成元 [@problem_id:2765436]。然而，若将空间限制在半直线 $(0, \infty)$ 上，同样的[微分](@entry_id:158718)算符就不再是本质自伴的（其[亏指数](@entry_id:266905)为 $(1,0)$），这揭示了边界条件在确定算符性质中的关键作用。

### 对易子及其直接推论

两个算符 $\hat{A}$ 和 $\hat{B}$ 之间的作用次序可能会影响最终结果。为了量化这种差异，我们定义**对易子**为：
$$
[\hat{A}, \hat{B}] = \hat{A}\hat{B} - \hat{B}\hat{A}
$$
如果 $[\hat{A}, \hat{B}] = 0$，我们称这两个算符是**对易的**；否则，它们是**不对易的**。

#### 对易性与共同[本征态](@entry_id:149904)

对易性有一个至关重要的物理意义：**两个自伴算符拥有一组完备的共同[本征函数](@entry_id:154705)，当且仅当它们相互对易**。这意味着，只有当两个可观测量对应的算符对易时，我们才可能制备出一个系统，使其同时具有这两个物理量的确定值。

反之，如果两个算符不对易，它们就不可能拥有一组完备的共同本征态。我们可以通过一个简单的[反证法](@entry_id:276604)来证明这一点 [@problem_id:1378507]。假设存在一个非零的共同本征函数 $|\psi\rangle$，使得 $\hat{A}|\psi\rangle = a|\psi\rangle$ 和 $\hat{B}|\psi\rangle = b|\psi\rangle$。现在我们将对易子作用于这个态上：
$$
[\hat{A}, \hat{B}]|\psi\rangle = (\hat{A}\hat{B} - \hat{B}\hat{A})|\psi\rangle = \hat{A}(b|\psi\rangle) - \hat{B}(a|\psi\rangle) = ab|\psi\rangle - ba|\psi\rangle = 0
$$
然而，如果给定的对易关系是 $[\hat{A}, \hat{B}] = i\hbar \hat{I}$（其中 $\hat{I}$ 是恒等算符），那么我们得到：
$$
[\hat{A}, \hat{B}]|\psi\rangle = i\hbar \hat{I} |\psi\rangle = i\hbar |\psi\rangle
$$
联立两个结果，我们得到 $i\hbar|\psi\rangle = 0$。由于 $\hbar$ 是一个非零常数，这必然要求 $|\psi\rangle$ 是[零矢量](@entry_id:155273)，这与我们假设 $|\psi\rangle$ 是一个非零本征函数相矛盾。因此，对于满足 $[\hat{A}, \hat{B}] = i\hbar$ 的算符，不存在任何共同的[本征函数](@entry_id:154705)。这直接预示了我们无法同时精确测量它们所对应的物理量。

#### [正则对易关系](@entry_id:185041)

在量子力学中，最核心的[对易关系](@entry_id:136780)是位置算符和动量算符之间的**[正则对易关系](@entry_id:185041) (Canonical Commutation Relations, CCRs)**。对于三维空间中的粒子，这些关系是 [@problem_id:2765424] [@problem_id:2765440]：
$$
[\hat{x}_i, \hat{p}_j] = i\hbar \delta_{ij}
$$
$$
[\hat{x}_i, \hat{x}_j] = 0
$$
$$
[\hat{p}_i, \hat{p}_j] = 0
$$
其中 $i, j \in \{1, 2, 3\}$，$\delta_{ij}$ 是克罗内克符号。

我们可以通过将对易子作用于一个任意的测试函数 $\psi(\mathbf{r})$ 上来验证第一个关系。例如，对于 $[\hat{x}_i, \hat{p}_j]$：
$$
[\hat{x}_i, \hat{p}_j]\psi = x_i(-i\hbar \frac{\partial}{\partial r_j}\psi) - (-i\hbar \frac{\partial}{\partial r_j}(r_i \psi))
$$
利用[微分](@entry_id:158718)的[乘法法则](@entry_id:144424) $\frac{\partial}{\partial r_j}(r_i \psi) = (\frac{\partial r_i}{\partial r_j})\psi + r_i(\frac{\partial \psi}{\partial r_j}) = \delta_{ij}\psi + r_i\frac{\partial \psi}{\partial r_j}$，我们得到：
$$
[\hat{x}_i, \hat{p}_j]\psi = -i\hbar r_i \frac{\partial \psi}{\partial r_j} + i\hbar (\delta_{ij}\psi + r_i \frac{\partial \psi}{\partial r_j}) = i\hbar \delta_{ij} \psi
$$
由于这对任意合适的 $\psi$ 都成立，我们便得到了算符关系 $[\hat{x}_i, \hat{p}_j] = i\hbar \delta_{ij}$。位置分量之间的对易性以及动量分量之间的对易性为零，则分别源于坐标乘法的交换律和[混合偏导数](@entry_id:139334)的[克莱罗定理](@entry_id:139814)。

这些关系是物理定律的基础，并且它们在[坐标系](@entry_id:156346)旋转下保持形式不变，即具有**旋转协变性**。这意味着量子力学的基本[代数结构](@entry_id:137052)不依赖于观察者[坐标系](@entry_id:156346)的选择，这是物理学[基本对称性](@entry_id:161256)的体现 [@problem_id:2765424]。

### [海森堡不确定性原理](@entry_id:171099)

不对易性最著名的物理后果就是海森堡不确定性原理，它为我们能同时知道的共轭物理量的精度设定了一个基本限制。

#### 普遍[不确定性关系](@entry_id:186128)的推导

这个原理可以从算符代数和希尔伯特空间的几何性质中严格推导出来。对于任意两个自伴算符 $\hat{A}$ 和 $\hat{B}$，以及一个给定的归一化[量子态](@entry_id:146142) $|\psi\rangle$，我们定义涨落算符 $\hat{A}' = \hat{A} - \langle\hat{A}\rangle$ 和 $\hat{B}' = \hat{B} - \langle\hat{B}\rangle$，其中 $\langle\hat{O}\rangle = \langle\psi|\hat{O}|\psi\rangle$ 是[期望值](@entry_id:153208)。标准差（或不确定度）定义为 $\Delta A = \sqrt{\langle(\hat{A}')^2\rangle}$。

推导始于对矢量 $\hat{A}'|\psi\rangle$ 和 $\hat{B}'|\psi\rangle$ 应用柯西-[施瓦茨不等式](@entry_id:202153)：
$$
(\Delta A)^2 (\Delta B)^2 = \|\hat{A}'\psi\|^2 \|\hat{B}'\psi\|^2 \ge |\langle \hat{A}'\psi | \hat{B}'\psi \rangle|^2 = |\langle\psi|\hat{A}'\hat{B}'|\psi\rangle|^2
$$
接下来，我们将算符乘积 $\hat{A}'\hat{B}'$ 分解为对称和反对称部分，这对应于**[反对易子](@entry_id:139754)**和对易子：
$$
\hat{A}'\hat{B}' = \frac{1}{2}\{\hat{A}', \hat{B}'\} + \frac{1}{2}[\hat{A}', \hat{B}']
$$
其中[反对易子](@entry_id:139754)定义为 $\{\hat{X}, \hat{Y}\} = \hat{X}\hat{Y} + \hat{Y}\hat{X}$ [@problem_id:2765386]。由于 $\hat{A}'$ 和 $\hat{B}'$ 是自伴的，它们的对易子是反自伴的（[期望值](@entry_id:153208)为纯虚数），而[反对易子](@entry_id:139754)是自伴的（[期望值](@entry_id:153208)为实数）。因此，$\langle\hat{A}'\hat{B}'\rangle$ 的[期望值](@entry_id:153208)是一个复数，其实部和虚部分别是 [@problem_id:2765378] [@problem_id:2765386]：
$$
\langle\hat{A}'\hat{B}'\rangle = \frac{1}{2}\langle\{\hat{A}', \hat{B}'\}\rangle + \frac{1}{2}\langle[\hat{A}, \hat{B}]\rangle
$$
注意，由于[期望值](@entry_id:153208)是常数，$[\hat{A}', \hat{B}'] = [\hat{A}, \hat{B}]$。一个[复数的模](@entry_id:634598)平方等于其实部平方与虚部平方之和。因此：
$$
|\langle\hat{A}'\hat{B}'\rangle|^2 = \left|\frac{1}{2}\langle\{\hat{A}', \hat{B}'\}\rangle\right|^2 + \left|\frac{1}{2}\langle[\hat{A}, \hat{B}]\rangle\right|^2
$$
将此代入柯西-施瓦茨不等式，我们得到**罗伯逊-薛定谔[不确定性关系](@entry_id:186128)**：
$$
(\Delta A)^2 (\Delta B)^2 \ge \frac{1}{4} |\langle[\hat{A}, \hat{B}]\rangle|^2 + \frac{1}{4} \langle\{\hat{A}', \hat{B}'\}\rangle^2
$$
这个关系式比标准的海森堡形式更为普适和强大。第二项 $\frac{1}{4}\langle\{\hat{A}', \hat{B}'\}\rangle^2$ 是**协[方差](@entry_id:200758)**的平方，它量化了两个[可观测量](@entry_id:267133)涨落之间的[统计相关性](@entry_id:267552)。协[方差](@entry_id:200758)项的存在意味着，即使两个算符对易（$[\hat{A}, \hat{B}]=0$），如果它们的涨落在特定状态下是相关的，其不确定度的乘积也可能有一个非零的下限。反之，这个相关性项只会让不确定性乘积的下限变得更大 [@problem_id:2765378]。例如，对于正则算符 $\hat{x}$ 和 $\hat{p}$，如果体系的[波函数](@entry_id:147440) $\psi(x)$ 是实函数，可以证明协[方差](@entry_id:200758)项为零 [@problem_id:2765378]。

如果我们忽略协[方差](@entry_id:200758)项（因为它总是非负的），我们就得到了更常见的**海森堡-罗伯逊[不确定性原理](@entry_id:141278)**：
$$
\Delta A \Delta B \ge \frac{1}{2} |\langle[\hat{A}, \hat{B}]\rangle|
$$

#### 位置与动量的不确定性

将此原理应用于位置和[动量算符](@entry_id:151743)，利用 $[\hat{x}, \hat{p}] = i\hbar$，我们得到：
$$
\Delta x \Delta p \ge \frac{1}{2} |\langle i\hbar \rangle| = \frac{1}{2} |i\hbar| = \frac{\hbar}{2}
$$
这个著名的不等式定量地表达了位置和动量不能被同时任意精确地确定。一个在位置上高度局域化的波包（$\Delta x$ 小）必然会在动量上表现出巨大的扩展（$\Delta p$ 大），反之亦然。能够使该不等式取等号的[量子态](@entry_id:146142)，即**最小不确定度态**，是[高斯波包](@entry_id:151158) [@problem_id:2765440] [@problem_id:2765370]。这个不等式的推导过程从根本上依赖于非零的[对易关系](@entry_id:136780)，它是量子世界非经典性的直接数学体现 [@problem_id:2765370] [@problem_id:2765436]。

### 概念辨析与高等专题

尽管位置-动量[不确定性原理](@entry_id:141278)形式简洁，但在更广泛的背景下，对易性和不确定性的概念需要更细致的审视。

#### [制备不确定性](@entry_id:203575)与测量扰动

海森堡不确定性原理 $(\Delta X \Delta P \ge \hbar/2)$ 是关于**态制备**的内在统计性质的陈述。它描述的是，如果我们对一个按同样方式制备出的大量（系综）系统分别测量其位置和动量，所得到结果的统计分布的标准差所必须满足的限制。它与任何单个测量过程无关 [@problem_id:2765394]。

这必须与**测量扰动**关系区分开。后者描述的是一个测量行为本身如何影响系统的后续状态。例如，一个精确测量粒子位置 ($\varepsilon(X) \to 0$) 的过程，必然会不可避免地扰动其动量，导致动量的不确定性 $\eta(P)$ 增大。这种测量误差与扰动之间的权衡关系，由更现代的[不确定性关系](@entry_id:186128)（如小泽不等式）所描述，它们既依赖于系统的初始状态，也依赖于测量仪器的具体构造。这两类不确定性在概念上是截然不同的 [@problem_id:2765394]。

#### [对易关系](@entry_id:136780)的微妙之处：特殊共轭对

虽然位置和动量算符是[正则对易关系](@entry_id:185041)的典范，但在其他物理系统中，定义[共轭变量](@entry_id:147843)对可能遇到深刻的数学难题，这通常与系统的拓扑结构和算符的定义域问题有关。

**1. 角度与角动量**

考虑一个在平面上转动的[刚性转子](@entry_id:156317)，如分子中的一个内部旋转自由度。其[位形空间](@entry_id:149531)是圆周 $S^1$，由角度坐标 $\phi \in [0, 2\pi)$ 描述。[角动量算符](@entry_id:153013)为 $\hat{L}_z = -i\hbar\frac{\partial}{\partial\phi}$。一个看似自然的角度算符是乘以 $\phi$ 的算符 $\hat{\Phi}$。然而，这个“朴素”的 $\hat{\Phi}$ 算符是有问题的 [@problem_id:2765374]。$\hat{L}_z$ 的自伴性要求其定义域中的函数必须是周期性的，即 $\psi(0) = \psi(2\pi)$。但 $\hat{\Phi}$ 算符（由于 $\phi$ 本身的[非周期性](@entry_id:275873)）会破坏这种周期性，例如，对于一个非零的周期函数 $\psi$，$(\hat{\Phi}\psi)(2\pi) = 2\pi\psi(2\pi)$ 而 $(\hat{\Phi}\psi)(0) = 0$，两者通常不相等。这导致 $\hat{\Phi}$ 不能将 $\hat{L}_z$ 的定义域映射到自身，使得对易子 $[\hat{L}_z, \hat{\Phi}]$ 无法在公共不变稠密定义域上良好定义。因此，简单的对易关系 $[\hat{\Phi}, \hat{L}_z] = i\hbar$ 在数学上是不成立的。

解决这个问题的一种方法是使用周期性函数来表示角度，例如使用**幺正算符** $\hat{U} = e^{i\hat{\Phi}}$。这个算符是良定义的有界算符，并且它与 $\hat{L}_z$ 满足一个精确的对易关系 $[\hat{L}_z, \hat{U}] = \hbar \hat{U}$ [@problem_id:2765374]。基于这个关系以及使用 $\cos\hat{\Phi}$ 和 $\sin\hat{\Phi}$ 算符，可以推导出适用于角度-角动量的、形式更复杂但数学上严格的[不确定性关系](@entry_id:186128)，它避免了直接使用有问题的 $\hat{\Phi}$ 算符 [@problem_id:2765374]。

**2. 能量与时间**

另一个更为深刻的例子是[能量-时间不确定性](@entry_id:138934)关系。人们可能期望存在一个时间算符 $\hat{T}$，与[哈密顿量](@entry_id:172864) $\hat{H}$ 满足对易关系 $[\hat{H}, \hat{T}] = i\hbar$。然而，**泡利定理**指出，对于任何具有**半有界谱**（即能量有下界，存在[基态](@entry_id:150928)）的物理系统，不存在这样的自伴时间算符 $\hat{T}$ [@problem_id:2765433]。其证明思路是：如果存在这样的 $\hat{T}$，那么幺正算符 $e^{i\alpha \hat{T}/\hbar}$ 将会平移能量谱，使得 $\hat{H} \to \hat{H} + \alpha \hat{I}$。这意味着能量谱必须是整个实直线 $\mathbb{R}$，这与能量有下界的前提相矛盾 [@problem_id:2765433]。

由于物理系统的[哈密顿量](@entry_id:172864)总是半有界的，这意味着[能量-时间不确定性](@entry_id:138934)关系不能像位置-动量关系那样从一个简单的对易子中推导出来。现代[量子理论](@entry_id:145435)通过引入**[正算符取值测量](@entry_id:138349) (Positive Operator-Valued Measure, [POVM](@entry_id:138770))** 的概念来处理时间[可观测量](@entry_id:267133)，如粒子穿过某个界面的“到达时间”。[POVM](@entry_id:138770) 是对自伴算符（对应于投影取值测量 PVM）的推广，它允许描述更一般的测量过程。即使不存在自伴的时间算符，我们仍然可以构建一个数学上一致的、满足[协变](@entry_id:634097)性要求的“时间”[POVM](@entry_id:138770) [@problem_id:2765433]。通过[奈马克扩张定理](@entry_id:153668)可知，任何这样的[POVM](@entry_id:138770)都可以被看作是在一个更大的、[哈密顿量](@entry_id:172864)非半有界的[辅助系统](@entry_id:142219)上进行标准投影测量的结果 [@problem_id:2765433]。这优雅地解释了为何我们可以在具有[基态](@entry_id:150928)的系统中谈论时间测量，其本质是系统与一个无能量下界的“时钟”或测量装置的相互作用。因此，[能量-时间不确定性](@entry_id:138934)关系有着多种不同的形式和诠释（如[Mandelstam-Tamm关系](@entry_id:156423)），其根基比[正则对易关系](@entry_id:185041)更为微妙。