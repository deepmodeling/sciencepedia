## 引言
在数学、物理和工程领域，我们经常需要处理那些不具备经典意义上“[光滑性](@entry_id:634843)”的函数，例如描述激波或[点电荷](@entry_id:263616)的函数。对于这些在某些点或线上存在[尖点](@entry_id:636792)、跳跃甚至更复杂奇性的函数，经典微积分中基于极限的求导方法束手无策。然而，这些函数描述了至关重要的物理现实，我们迫切需要一种方法来“[微分](@entry_id:158718)”它们，以构建和分析相应的数学模型。

本文旨在填补这一知识鸿沟，系统介绍现代分析中处理[非光滑函数](@entry_id:175189)的两大核心工具：[弱导数](@entry_id:189356)与[分布理论](@entry_id:186499)。这些概念通过一种巧妙的“责任转移”思想，绕开了对函数本身逐点光滑性的苛刻要求，为[微分](@entry_id:158718)运算提供了一个更广阔、更强大的舞台。

读者将通过本文踏上一段从基础到应用的探索之旅。在“原理与机制”一章，我们将从[分部积分](@entry_id:136350)出发，建立[弱导数](@entry_id:189356)和[分布](@entry_id:182848)的严谨定义，揭示其内在逻辑。随后，在“应用与交叉学科联系”一章，我们将见证这一理论如何成为现代[偏微分方程](@entry_id:141332)、物理建模、工程分析乃至计算科学的基石。最后，“动手实践”部分将提供一系列精心设计的问题，帮助您将理论知识转化为解决实际问题的能力。

## 原理与机制

在经典微积分的框架中，函数的可微性是一个核心但具有限制性的概念。一个函数必须足够“光滑”或“良好”，才能定义其导数。然而，在物理学、工程学和现代[偏微分方程理论](@entry_id:189232)中，我们经常遇到一些在某些点、线甚至更复杂的集合上表现出不规则行为的函数，例如在[点电荷](@entry_id:263616)处的[电势](@entry_id:267554)或激[波阵面](@entry_id:197956)上的压力。这些函数可能不具有经典意义上的导数，但它们描述了重要的物理现象，我们仍希望能够以一种有意义的方式对其进行“[微分](@entry_id:158718)”。这一需求催生了[广义函数](@entry_id:182848)（或[分布](@entry_id:182848)）和[弱导数](@entry_id:189356)的概念，它们是现代分析中用于处理[非光滑函数](@entry_id:175189)的强大工具。

### 从经典导数到[弱导数](@entry_id:189356)

我们思考一个基本问题：如何理解一个并非处处可微的函数的“导数”？让我们考虑一个经典的一维例子：$u(x) = |x|$，定义在[开区间](@entry_id:157577) $\Omega=(-1,1)$ 上 [@problem_id:3037166]。这个函数在除了 $x=0$ 之外的所有点上都是可微的，但在原点处有一个[尖点](@entry_id:636792)，因此其经典导数在 $x=0$ 处不存在。然而，从图像上看，它的“斜率”在 $x  0$ 时是 $-1$，在 $x > 0$ 时是 $+1$。我们能否将这种直观认识转化为一个严谨的数学定义？

答案在于一种“转移责任”的思想，也就是通过**[分部积分](@entry_id:136350)** (integration by parts) 将[微分](@entry_id:158718)操作从可能不光滑的函数 $u$ 转移到一个任意“良好”的函数 $\varphi$ 上。这些“良好”的函数被称为**[检验函数](@entry_id:166589)** (test functions)。它们是定义在 $\Omega$ 上、具有[紧支集](@entry_id:276214)且无限次可微的函数，其全体记为 $C_c^\infty(\Omega)$。[紧支集](@entry_id:276214)属性意味着每个[检验函数](@entry_id:166589)及其所有阶导数在一个包含于 $\Omega$ 的紧集之外恒为零，这使得在[分部积分](@entry_id:136350)时边界项自动消失。

对于一个光滑函数 $u \in C^1(\Omega)$ 和一个[检验函数](@entry_id:166589) $\varphi \in C_c^\infty(\Omega)$，标准的[分部积分公式](@entry_id:145262)给出：
$$
\int_{\Omega} u'(x) \varphi(x) \,dx = [u(x)\varphi(x)]_{\partial\Omega} - \int_{\Omega} u(x) \varphi'(x) \,dx
$$
由于 $\varphi$ 在 $\Omega$ 的边界附近为零，边界项 $[u(x)\varphi(x)]_{\partial\Omega}$ 消失，我们得到：
$$
\int_{\Omega} u'(x) \varphi(x) \,dx = - \int_{\Omega} u(x) \varphi'(x) \,dx
$$
这个恒等式启发了[弱导数](@entry_id:189356)的定义。我们不再要求 $u$ 是可微的，而是寻找一个函数 $v$，使得对于**所有**检验函数 $\varphi \in C_c^\infty(\Omega)$，上述关系式仍然成立。

**定义 ([弱导数](@entry_id:189356))**：设 $u$ 是 $\Omega \subset \mathbb{R}^n$ 上的一个**[局部可积函数](@entry_id:175678)** (locally integrable function)，即 $u \in L_{\mathrm{loc}}^1(\Omega)$。如果存在另一个[局部可积函数](@entry_id:175678) $v \in L_{\mathrm{loc}}^1(\Omega)$，使得对于任意多重指标 $\alpha$ 和任意检验函数 $\varphi \in C_c^\infty(\Omega)$，以下积分恒等式成立：
$$
\int_\Omega v(x) \varphi(x) \, dx = (-1)^{|\alpha|} \int_\Omega u(x) \partial^\alpha \varphi(x) \, dx
$$
则称 $v$ 是 $u$ 的 $\alpha$ **阶[弱导数](@entry_id:189356)** (weak derivative)，记作 $v = \partial^\alpha u$。[@problem_id:2560417] [@problem_id:3033586]

这里，$\alpha = (\alpha_1, \dots, \alpha_n)$ 是一个多重指标， $|\alpha| = \sum \alpha_i$ 是其阶数，$\partial^\alpha = \partial_1^{\alpha_1} \cdots \partial_n^{\alpha_n}$ 是经典偏导数算子。因子 $(-1)^{|\alpha|}$ 是 $n$ 维空间中 $|\alpha|$ 次[分部积分](@entry_id:136350)的结果。这个定义的核心在于：
1.  **函数的正则性要求极低**：仅需 $u$ 和 $v$ 是局部可积的，这是一个非常弱的条件。
2.  **检验函数空间是关键**：使用 $C_c^\infty(\Omega)$ 作为[检验函数](@entry_id:166589)空间至关重要。它们的无限[光滑性](@entry_id:634843)确保 $\partial^\alpha \varphi$ 总是良定义的；它们的[紧支集](@entry_id:276214)确保了[分部积分](@entry_id:136350)中边界项的消失。任何扩大检验函数空间（例如到 $C^\infty(\Omega)$）或缩小（例如到 $H_0^1(\Omega)$）的尝试都会破坏定义的普适性或使其不自洽。[@problem_id:2560417]
3.  **唯一性**：如果这样的函数 $v$ 存在，它在 $L_{\mathrm{loc}}^1(\Omega)$ 的意义下是唯一的（即在[测度为零](@entry_id:137864)的集合外唯一确定）。

现在，我们回到 $u(x)=|x|$ 的例子 [@problem_id:3037166]。我们寻找它的弱[一阶导数](@entry_id:749425) $v$。根据定义，对于任意 $\varphi \in C_c^\infty(-1,1)$，我们必须有：
$$
\int_{-1}^1 v(x) \varphi(x) \,dx = - \int_{-1}^1 |x| \varphi'(x) \,dx
$$
为了计算右侧积分，我们将积分区间在[奇点](@entry_id:137764) $x=0$ 处分开：
$$
- \int_{-1}^1 |x| \varphi'(x) \,dx = - \int_{-1}^0 (-x) \varphi'(x) \,dx - \int_0^1 x \varphi'(x) \,dx
$$
在每个子区间上分别进行分部积分，并利用 $\varphi(-1)=\varphi(1)=0$：
$$
\int_{-1}^0 x \varphi'(x) \,dx = [x\varphi(x)]_{-1}^0 - \int_{-1}^0 \varphi(x) \,dx = -\int_{-1}^0 \varphi(x) \,dx
$$
$$
- \int_0^1 x \varphi'(x) \,dx = -[x\varphi(x)]_0^1 + \int_0^1 \varphi(x) \,dx = \int_0^1 \varphi(x) \,dx
$$
合并结果，得到：
$$
- \int_{-1}^1 |x| \varphi'(x) \,dx = \int_{-1}^0 (-1)\varphi(x) \,dx + \int_0^1 (1)\varphi(x) \,dx = \int_{-1}^1 \mathrm{sgn}(x) \varphi(x) \,dx
$$
这里 $\mathrm{sgn}(x)$ 是[符号函数](@entry_id:167507)。通过与定义式对比，我们发现 $u(x)=|x|$ 的[弱导数](@entry_id:189356)正是 $v(x) = \mathrm{sgn}(x)$，它是一个 $L_{\mathrm{loc}}^1$ 函数。这完美地捕捉了我们对 $|x|$ “斜率”的直观理解。

### [分布](@entry_id:182848)：[广义函数](@entry_id:182848)的统一理论

[弱导数](@entry_id:189356)的概念非常有用，但它要求导数的结果仍然是一个（局部可积的）函数。然而，[微分](@entry_id:158718)运算可能将一个函数的奇异性增强到无法再用函数来描述的程度。

再次考虑 $u(x)=|x|$。它的[弱导数](@entry_id:189356)是 $v(x) = \mathrm{sgn}(x)$。现在我们尝试计算 $v(x)$ 的[弱导数](@entry_id:189356)，即 $u(x)$ 的[二阶导数](@entry_id:144508)。根据定义，我们寻找 $w \in L_{\mathrm{loc}}^1(\Omega)$ 使得：
$$
\int_{-1}^1 w(x) \varphi(x) \,dx = - \int_{-1}^1 \mathrm{sgn}(x) \varphi'(x) \,dx
$$
计算右侧积分：
$$
- \int_{-1}^1 \mathrm{sgn}(x) \varphi'(x) \,dx = - \int_{-1}^0 (-1)\varphi'(x) \,dx - \int_0^1 (1)\varphi'(x) \,dx = [\varphi(x)]_{-1}^0 - [\varphi(x)]_0^1
$$
利用 $\varphi(-1)=\varphi(1)=0$，我们得到：
$$
(\varphi(0) - \varphi(-1)) - (\varphi(1) - \varphi(0)) = \varphi(0) + \varphi(0) = 2\varphi(0)
$$
因此，我们希望找到一个函数 $w(x)$，使得 $\int_{-1}^1 w(x) \varphi(x) \,dx = 2\varphi(0)$ 对所有[检验函数](@entry_id:166589) $\varphi$ 成立。可以证明，不存在任何 $L_{\mathrm{loc}}^1$ 函数 $w(x)$ 具有此性质。这个操作 $L[\varphi] = 2\varphi(0)$ 描述了一种新的对象，它通过在一点处“取值”来作用于检验函数。

这个对象就是**狄拉克 $\delta$ [分布](@entry_id:182848)** (Dirac delta distribution) 的两倍，记作 $2\delta_0$。这启发我们进一步推广函数的概念。我们不再将函数看作是“点的集合”，而是通过它们如何作用于[检验函数](@entry_id:166589)来定义它们，即通过积分 $\langle u, \varphi \rangle = \int_\Omega u \varphi \,dx$。

**定义 ([分布](@entry_id:182848))**：一个**[分布](@entry_id:182848)** (distribution) $T$ 是定义在检验函数空间 $C_c^\infty(\Omega)$ 上的一个**[连续线性泛函](@entry_id:262913)** (continuous linear functional)。即，$T: C_c^\infty(\Omega) \to \mathbb{R}$（或 $\mathbb{C}$），满足：
1.  **线性性**：$\langle T, a\varphi + b\psi \rangle = a\langle T, \varphi \rangle + b\langle T, \psi \rangle$
2.  **连续性**：如果一列检验函数 $\varphi_j \to \varphi$ 在 $C_c^\infty(\Omega)$ 的拓扑意义下收敛，则 $\langle T, \varphi_j \rangle \to \langle T, \varphi \rangle$。[@problem_id:2560417]

所有 $L_{\mathrm{loc}}^1(\Omega)$ 中的函数 $u$ 都可通过 $\langle T_u, \varphi \rangle = \int u\varphi \,dx$ 定义一个[分布](@entry_id:182848)，称为**正则[分布](@entry_id:182848)** (regular distribution)。但[分布](@entry_id:182848)的概念更广泛，例如 $\delta$ [分布](@entry_id:182848)，定义为 $\langle \delta_{x_0}, \varphi \rangle = \varphi(x_0)$，它是一个[分布](@entry_id:182848)但不是由任何 $L_{\mathrm{loc}}^1$ 函数生成的。

在这个更广阔的[分布](@entry_id:182848)框架中，[微分](@entry_id:158718)的定义变得异常简洁和普适。

**定义 ([分布导数](@entry_id:181138))**：设 $T$ 是一个[分布](@entry_id:182848)。其 $\alpha$ 阶**[分布导数](@entry_id:181138)** (distributional derivative) $\partial^\alpha T$ 是一个新的[分布](@entry_id:182848)，其对任意检验函数 $\varphi$ 的作用定义为：
$$
\langle \partial^\alpha T, \varphi \rangle := (-1)^{|\alpha|} \langle T, \partial^\alpha \varphi \rangle
$$
这个定义是先前[分部积分公式](@entry_id:145262)的直接抽象化。它对**任何**[分布](@entry_id:182848)都有效，并且求导运算总能进行，结果也总是一个[分布](@entry_id:182848)。例如，我们可以计算 $\delta$ [分布](@entry_id:182848)的导数 [@problem_id:3037172]：
$$
\langle \partial^\alpha \delta_{x_0}, \varphi \rangle = (-1)^{|\alpha|} \langle \delta_{x_0}, \partial^\alpha \varphi \rangle = (-1)^{|\alpha|} (\partial^\alpha \varphi)(x_0)
$$
这表明，$\delta$ [分布](@entry_id:182848)的导数作用在检验函数上，等价于对[检验函数](@entry_id:166589)求导后再在 $x_0$ 点取值的操作（带一个符号因子）。

回到我们的例子，我们现在可以说 $u(x)=|x|$ 的二阶[分布导数](@entry_id:181138)是 $u'' = 2\delta_0$ [@problem_id:3037166]。[弱导数](@entry_id:189356)现在可以看作是[分布导数](@entry_id:181138)的一个特例：如果一个函数 $u$ 的[分布导数](@entry_id:181138) $\partial^\alpha u$恰好是一个正则[分布](@entry_id:182848)（即可以由一个 $L_{\mathrm{loc}}^1$ 函数 $v$ 表示），那么 $v$ 就是 $u$ 的[弱导数](@entry_id:189356)。

[分布导数](@entry_id:181138)的一个惊人特性是**[混合偏导数](@entry_id:139334)的[交换性](@entry_id:140240)**。对于经典函数，Clairaut 定理要求[二阶偏导数](@entry_id:635213)连续才能保证[混合偏导数相等](@entry_id:138898)。然而，对于[分布](@entry_id:182848)，这个性质是无条件成立的。对于任意[分布](@entry_id:182848) $T$，我们总是有 $\partial_i \partial_j T = \partial_j \partial_i T$。这可以通过 Fubini 定理和[分布导数](@entry_id:181138)的定义直接证明 [@problem_id:1420118]：
$$
\langle \partial_i \partial_j T, \varphi \rangle = (-1)^2 \langle T, \partial_j \partial_i \varphi \rangle = \langle T, \partial_i \partial_j \varphi \rangle = \langle \partial_j \partial_i T, \varphi \rangle
$$
这里利用了[检验函数](@entry_id:166589) $\varphi$ 的光滑性，保证了其经典[混合偏导数](@entry_id:139334)是相等的。

### 应用：[索博列夫空间](@entry_id:141995)与[偏微分方程](@entry_id:141332)

[弱导数](@entry_id:189356)最重要的应用之一是构建**索博列夫空间** (Sobolev spaces)。这些[函数空间](@entry_id:143478)是研究[偏微分方程](@entry_id:141332)弱解的自然舞台。

**定义 (索博列夫空间)**：给定 $1 \le p \le \infty$ 和一个非负整数 $k$，索博列夫空间 $W^{k,p}(\Omega)$ 定义为：
$$
W^{k,p}(\Omega) = \{ u \in L^p(\Omega) \mid \forall |\alpha| \le k, \partial^\alpha u \in L^p(\Omega) \}
$$
其中 $\partial^\alpha u$ 是 $u$ 的 $\alpha$ 阶[弱导数](@entry_id:189356)。这个空间包含所有自身以及直到 $k$ 阶的所有[弱导数](@entry_id:189356)都属于 $L^p$ 空间的函数。[@problem_id:3033170]

$W^{k,p}(\Omega)$ 配备了范数，例如当 $1 \le p  \infty$ 时：
$$
\|u\|_{W^{k,p}(\Omega)} := \left( \sum_{|\alpha| \le k} \|\partial^\alpha u\|_{L^p(\Omega)}^p \right)^{1/p}
$$
在这个范数下，$W^{k,p}(\Omega)$ 是一个完备的[赋范线性空间](@entry_id:264073)，即一个**[巴拿赫空间](@entry_id:143833)** (Banach space)。它的完备性是其在分析中如此有用的一个关键原因，这可以通过将其视为 $L^p$ 空间乘积的一个[闭子空间](@entry_id:267213)来证明。[@problem_id:3033170]

[索博列夫空间](@entry_id:141995)允许我们将[偏微分方程](@entry_id:141332)的解的概念从经典的“逐点满足方程”的[强解](@entry_id:198344)，推广到“在积分意义下满足方程”的**[弱解](@entry_id:161732)**。例如，对于一个椭圆型方程 $Lu = f$，[弱解](@entry_id:161732) $u$ 通常只需要属于某个[索博列夫空间](@entry_id:141995)，并满足对所有检验函数 $\varphi$ 成立的积分恒等式 $\langle Lu, \varphi \rangle = \langle f, \varphi \rangle$。诸如 Poincaré 不等式这样的工具，它将函数本身的 $L^2$ 范数与它的导数的 $L^2$ 范数联系起来 ($\|u\|_{L^2} \le C \|\nabla u\|_{L^2}$ 对于 $u \in H_0^1(\Omega)$)，对于证明这些[弱解](@entry_id:161732)的存在性和唯一性至关重要。[@problem_id:2560417]

然而，弱解的正则性（即光滑程度）强烈依赖于[微分算子](@entry_id:140145) $L$ 的性质。对于**[椭圆算子](@entry_id:181616)** (elliptic operators)，如[拉普拉斯算子](@entry_id:146319) $\Delta$，存在强大的[正则性理论](@entry_id:194071)，保证了如果[源项](@entry_id:269111) $f$ 是光滑的，那么弱解 $u$ 也将是光滑的。但对于**非[椭圆算子](@entry_id:181616)**，如双曲算子（波动算子）$\partial_{x_1}^2 - \partial_{x_2}^2$，这种正则性会丧失。一个典型的例子是，方程 $(\partial_{x_1}^2 - \partial_{x_2}^2)u = f$ 的解 $u$ 可能只具有有限的正则性，即使 $f$ 非常奇异。例如，函数 $u(x_1, x_2) = |x_1|\phi(x_2)$ 属于 $H^1_{\mathrm{loc}}(\mathbb{R}^2)$ 但不属于 $H^2_{\mathrm{loc}}(\mathbb{R}^2)$，然而它是一个非[椭圆方程](@entry_id:169190)的 distributional solution，其[源项](@entry_id:269111) $f$ 是一个[分布](@entry_id:182848)。这表明，[奇点](@entry_id:137764)可以沿着算子的特征方向传播，而不会被“平滑掉”。[@problem_id:3037161]

### 奇异性的代数与分析

[分布理论](@entry_id:186499)提供了一个强大的[微分](@entry_id:158718)框架，但它在处理代数运算，尤其是乘法时，遇到了深刻的困难。一般而言，两个任意[分布](@entry_id:182848)的乘积是**没有定义的**。

我们可以通过一个例子看到这一点。考虑序列 $f_j(x) = \varphi(x) \sin(jx_1)$，其中 $\varphi \in C_c^\infty(\Omega)$ 是一个非零的[检验函数](@entry_id:166589)。根据 Riemann-Lebesgue 引理，对于任何[检验函数](@entry_id:166589) $\psi$，$\int f_j \psi \, dx \to 0$，因此 $f_j \to 0$ 在[分布](@entry_id:182848)意义下收敛。然而，考虑乘积 $f_j^2(x) = \varphi^2(x) \sin^2(jx_1) = \frac{1}{2}\varphi^2(x)(1 - \cos(2jx_1))$。当 $j \to \infty$ 时，[振荡](@entry_id:267781)项 $\cos(2jx_1)$ 在[分布](@entry_id:182848)意义下也收敛到 0，因此 $f_j^2$ 在[分布](@entry_id:182848)意义下收敛到 $\frac{1}{2}\varphi^2$，这是一个非[零分布](@entry_id:195412)。我们得到了一个悖论：$f_j \to 0$，但 $\lim (f_j \cdot f_j) \neq (\lim f_j) \cdot (\lim f_j) = 0$。[@problem_id:3037174]

这个例子揭示，乘法作为从 $C_c^\infty \times C_c^\infty$ 到 $C_c^\infty$ 的[双线性映射](@entry_id:186502)，在[分布](@entry_id:182848)空间的拓扑结构下并**不是联合连续的** (not jointly continuous)。这就是为什么[分布](@entry_id:182848)的[代数结构](@entry_id:137052)比函数的[代数结构](@entry_id:137052)要复杂得多的根本原因。

为了解决这个问题并精确描述[分布](@entry_id:182848)的奇异性如何相互作用，数学家发展了**微局部分析** (microlocal analysis) 理论。其核心工具是**[波前集](@entry_id:197277)** (wavefront set) $WF(u)$。对于一个[分布](@entry_id:182848) $u$，它的[波前集](@entry_id:197277) $WF(u)$ 是[余切丛](@entry_id:185138) $T^*X \setminus \{0\}$ 的一个[子集](@entry_id:261956)，它不仅记录了[分布](@entry_id:182848) $u$ 在**哪个点** $x$ 是奇异的（这由奇异支集 `sing supp` 完成），还记录了在该点奇异性传播的**方向**（由[余向量](@entry_id:157727) $\xi$ 表示）。

利用[波前集](@entry_id:197277)，Hörmander 提出了一个定义[分布](@entry_id:182848)乘积的准则：

**Hörmander 乘法准则**：如果对于任意点 $x \in X$，[分布](@entry_id:182848) $T$ 和 $S$ 的[波前集](@entry_id:197277)在该点的纤维上不包含方向相反的[余向量](@entry_id:157727)，即对于任意 $(x, \xi) \in WF(T)$，都有 $(x, -\xi) \notin WF(S)$，那么乘积 $TS$ 就是良定义的。

这个准则的直观意义是，只要两个[分布](@entry_id:182848)的奇异性在任何点都不会“迎头相撞”，它们的乘积就可以被赋予明确的含义。一个经典的反例是 $\delta \cdot \mathrm{p.v.}(1/x)$ 在 $\mathbb{R}$ 上的乘积。$\delta$ [分布](@entry_id:182848)和[柯西主值](@entry_id:192761)[分布](@entry_id:182848) $\mathrm{p.v.}(1/x)$都在 $x=0$ 处奇异，并且它们的[波前集](@entry_id:197277)在 $x=0$ 处的纤维都包含了所有非零方向 $\xi$。因此，对于任意 $\xi \neq 0$，$(0, \xi) \in WF(\delta)$ 且 $(0, -\xi) \in WF(\mathrm{p.v.}(1/x))$。Hörmander 准则被违反，因此这个乘积不是良定义的。[@problem_id:3037169]

类似地，微局部分析也为**[分布](@entry_id:182848)的回拉** (pullback of a distribution) 提供了严格的判据。给定一个[光滑映射](@entry_id:203730) $f: Y \to X$ 和一个[分布](@entry_id:182848) $u \in \mathcal{D}'(X)$，我们希望定义 $f^*u \in \mathcal{D}'(Y)$。直观上，如果映射 $f$ 将其定义域“压扁”到 $u$ 的[奇异集](@entry_id:186233)上，可能会产生问题。微局部分析将此精确化：回拉 $f^*u$ 是良定义的，当且仅当 $u$ 的[波前集](@entry_id:197277) $WF(u)$ 与映射 $f$ 的**[法丛](@entry_id:272447)** (conormal bundle) $N_f$ 的交集为空。[法丛](@entry_id:272447) $N_f$ 包含了那些被 $f$ 的[微分](@entry_id:158718)“湮灭”的[余向量](@entry_id:157727)方向。

一个简单的例子可以说明这一点 [@problem_id:3037165]。令 $u(x_1, x_2) = \delta(x_2)$，其奇异性在 $x_2=0$ 直线上，[波前集](@entry_id:197277)方向为 $dx_2$ 方向。考虑映射 $f: \mathbb{R} \to \mathbb{R}^2$，$f(t)=(t,0)$。这个映射的像恰好就是 $u$ 的奇异支集。$f$ 的[法丛](@entry_id:272447)恰好也由 $dx_2$ 方向的余向量构成。因此，$WF(u)$ 和 $N_f$ 严重相交，回拉 $f^*u$ 是未定义的。这与直观相符：试图将一个沿 $x_1$ 轴的线状 $\delta$ [分布](@entry_id:182848)“[拉回](@entry_id:160816)”到这条线自身上，会导致一个无限大的对象。

总之，从[分部积分](@entry_id:136350)这一简单思想出发，[弱导数](@entry_id:189356)和[分布理论](@entry_id:186499)为处理[非光滑函数](@entry_id:175189)提供了一个系统而强大的框架。它不仅是现代[偏微分方程理论](@entry_id:189232)的基石，还通过微局部分析等工具，使我们能够以前所未有的精度来理解和操控函数的奇异性。