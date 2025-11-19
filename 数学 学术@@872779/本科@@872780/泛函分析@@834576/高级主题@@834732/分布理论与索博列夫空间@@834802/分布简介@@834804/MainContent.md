## 引言
在物理学和工程学的世界中，我们经常遇到一些理想化的概念，例如一个没有体积的点电荷，或是在一瞬间施加的冲击力。这些在单一点上“无限大”而在其他地方为零的“奇异”对象，无法用传统的函数概念来精确描述。经典分析的局限性在此显露无疑，它促使数学家们寻求一个更广阔的舞台。[广义函数](@entry_id:182848)（或称[分布](@entry_id:182848)）理论应运而生，它彻底改变了我们看待函数的方式，不再关注其逐点的值，而是通过它如何“作用”于一组性质优良的“[检验函数](@entry_id:166589)”来定义其身份，为处理奇异性提供了严谨而强大的数学工具。

本文将系统地引导您进入[广义函数](@entry_id:182848)的世界。在第一章“原理与机制”中，我们将从基本定义出发，理解[分布](@entry_id:182848)作为[连续线性泛函](@entry_id:262913)的本质，并学习如何在[分布](@entry_id:182848)上进行[微分](@entry_id:158718)等核心运算，您将看到即便是断点或尖点处，求导也变得自然而一致。随后，在第二章“应用与跨学科联系”中，我们将探索[分布理论](@entry_id:186499)的巨大威力，看它如何作为一种统一的语言，精确描述物理学中的[点电荷](@entry_id:263616)和电偶极子，并成为[求解偏微分方程](@entry_id:138485)的利器。最后，在“动手实践”部分，您将通过具体的计算问题，亲手运用这些抽象概念，巩固并深化您的理解。让我们一同开启这段激动人心的数学之旅，去发现一个超越经典函数的美丽新世界。

## 原理与机制

在经典分析中，函数的概念是核心，但它不足以描述物理学和工程学中出现的许多重要现象，例如点电荷的[电荷密度](@entry_id:144672)或瞬间施加的冲击力。这些理想化的概念在数学上对应于在单个点上“无限”而在其他地方为零的量，这无法用传统函数来严格表示。为了克服这些局限性，数学家们发展了**[广义函数](@entry_id:182848)**（generalized functions）或**[分布](@entry_id:182848)**（distributions）的理论。其核心思想是，一个对象的身份不仅可以通过其逐点的值来确定，还可以通过它对一类“良好”函数的“作用”来确定。

### 从函数到泛函：一个新的视角

让我们首先重新审视普通函数。对于一个行为良好的函数 $f(x)$，我们可以通过它与另一个函数 $\phi(x)$ 的积分来研究其性质：
$$
\int_{-\infty}^{\infty} f(x)\phi(x) \, dx
$$
这个积分值为我们提供了一个关于函数 $f$ 在函数 $\phi$ “探测”下的平均信息。[分布理论](@entry_id:186499)将这一观点提升为基本定义。我们不再关注 $f$ 本身，而是关注由 $f$ 产生的映射关系：对于给定的 $\phi$，赋予一个数值。

为了使这个框架严谨，我们需要精确定义我们所使用的“探针”函数 $\phi$。这些函数被称为**[检验函数](@entry_id:166589)**（test functions），它们构成的空间记为 $\mathcal{D}(\mathbb{R})$。一个函数 $\phi: \mathbb{R} \to \mathbb{R}$ 属于 $\mathcal{D}(\mathbb{R})$，如果它满足两个条件：
1.  **无限可微**：$\phi$ 拥有任意阶的导数，即 $\phi \in C^\infty(\mathbb{R})$。
2.  **[紧支集](@entry_id:276214)**：存在一个[紧集](@entry_id:147575)（即有界闭区间），例如 $[-R, R]$，使得在此区间之外 $\phi(x)$ 恒为零。这个性质称为具有**[紧支集](@entry_id:276214)**（compact support）。

[检验函数](@entry_id:166589)的这些“良好”性质至关重要。无限可微性确保了我们可以对其进行任意[次微分](@entry_id:175641)，而[紧支集](@entry_id:276214)则保证了当我们进行分部积分等操作时，边界项总是为零，这极大地简化了计算。

### [分布](@entry_id:182848)的严格定义

基于上述思想，我们可以给出[分布](@entry_id:182848)的正式定义。一个**[分布](@entry_id:182848)** $T$ 是作用在检验函数空间 $\mathcal{D}(\mathbb{R})$ 上的一个**[连续线性泛函](@entry_id:262913)**。这意味着 $T$ 是一个映射，它将每个检验函数 $\phi \in \mathcal{D}(\mathbb{R})$ 赋予一个标量值（实数或复数），记作 $\langle T, \phi \rangle$，并且这个映射必须满足两个基本属性：线性和连续性。

#### 线性

对于任意[检验函数](@entry_id:166589) $\phi_1, \phi_2 \in \mathcal{D}(\mathbb{R})$ 和任意标量 $a, b \in \mathbb{R}$，泛函 $T$ 必须满足：
$$
\langle T, a\phi_1 + b\phi_2 \rangle = a\langle T, \phi_1 \rangle + b\langle T, \phi_2 \rangle
$$
这个属性是积分线性性质的直接推广。任何不满足此条件的泛函都不能被视为[分布](@entry_id:182848)。例如，考虑一个由 $\langle T, \phi \rangle = \int_{\mathbb{R}} (\phi(x))^2 dx$ 定义的泛函 [@problem_id:1867041]。我们可以验证它是否是线性的。令 $\phi = a\phi_1 + b\phi_2$，则：
$$
\langle T, a\phi_1 + b\phi_2 \rangle = \int_{\mathbb{R}} (a\phi_1(x) + b\phi_2(x))^2 dx = \int_{\mathbb{R}} (a^2\phi_1(x)^2 + 2ab\phi_1(x)\phi_2(x) + b^2\phi_2(x)^2) dx
$$
而另一方面：
$$
a\langle T, \phi_1 \rangle + b\langle T, \phi_2 \rangle = a\int_{\mathbb{R}} \phi_1(x)^2 dx + b\int_{\mathbb{R}} \phi_2(x)^2 dx
$$
显然，这两个表达式在一般情况下不相等。因此，这个泛函是[非线性](@entry_id:637147)的，从而不是一个[分布](@entry_id:182848)。

#### 连续性

[分布](@entry_id:182848)的连续性是一个更技术性的概念。直观地讲，如果一个检验函数序列 $\{\phi_n\}$ 在 $\mathcal{D}(\mathbb{R})$ 的意义下收敛到零（意味着 $\phi_n$ 和它们的所有阶导数都一致收敛到零），那么对应的数值序列 $\langle T, \phi_n \rangle$ 也必须收敛到零。这个条件保证了[分布](@entry_id:182848)不会对[检验函数](@entry_id:166589)的微小扰动做出剧烈的、不稳定的响应。

### [分布](@entry_id:182848)的类别

[分布](@entry_id:182848)可以大致分为两类：那些源于普通函数的正则[分布](@entry_id:182848)，以及那些无法用此种方式表示的[奇异分布](@entry_id:265958)。

#### 正则[分布](@entry_id:182848)

许多我们熟悉的函数都可以自然地定义一个[分布](@entry_id:182848)。如果一个函数 $f(x)$ 是**局部可积的**（locally integrable），即对于任何紧区间 $K \subset \mathbb{R}$，积分 $\int_K |f(x)| \, dx$ 都是有限的，那么它就可以定义一个**正则[分布](@entry_id:182848)** $T_f$，其作用方式为：
$$
\langle T_f, \phi \rangle = \int_{-\infty}^{\infty} f(x)\phi(x) \, dx
$$
由于 $\phi$ 具有[紧支集](@entry_id:276214)，上述积分实际上是在一个有限区间上进行的，而 $f$ 的局部[可积性](@entry_id:142415)保证了这个积分总是有定义的。

一个关键问题是：什么样的函数是局部可积的？让我们考虑函数族 $f(x) = |x|^\alpha$ [@problem_id:1867035]。为了确定 $f(x)$ 何时定义一个正则[分布](@entry_id:182848)，我们需要找到使它局部可积的 $\alpha$ 的范围。在任何不包含原点的紧区间上，$|x|^\alpha$ 都是连续的，因此是可积的。唯一的挑战来自于[奇点](@entry_id:137764) $x=0$。我们只需检验包含原点的任意紧区间（例如 $[-1, 1]$）上的可积性：
$$
\int_{-1}^{1} |x|^\alpha \, dx = 2 \int_{0}^{1} x^\alpha \, dx
$$
通过标准积分计算，我们发现此[积分收敛](@entry_id:139742)当且仅当 $\alpha+1 > 0$，即 $\alpha > -1$。当 $\alpha = -1$ 时，积分为 $2[\ln(x)]_0^1$，发散；当 $\alpha  -1$ 时，积分也发散。因此，只有当 $\alpha > -1$ 时，$f(x) = |x|^\alpha$ 才能定义一个正则[分布](@entry_id:182848)。

有些函数在某点看起来是奇异的，但实际上仍然是局部可积的。例如，考虑由 $f(x) = \frac{\cos(ax)-1}{x^2}$（其中 $a \neq 0$）定义的泛函 [@problem_id:1867032]。在 $x=0$ 处，分母为零，看似存在问题。然而，通过在 $x=0$ 附近对 $\cos(ax)$ 进行[泰勒展开](@entry_id:145057)：
$$
\cos(ax) = 1 - \frac{(ax)^2}{2!} + O(x^4)
$$
我们得到：
$$
f(x) = \frac{(1 - \frac{a^2x^2}{2} + \dots) - 1}{x^2} = -\frac{a^2}{2} + O(x^2)
$$
这表明当 $x \to 0$ 时，$f(x)$ 的极限是 $-\frac{a^2}{2}$。这意味着 $x=0$ 是一个[可去奇点](@entry_id:175597)，函数 $f(x)$ 在包含原点的任何紧集上都是有界从而可积的。因此，$f(x)$ 是一个[局部可积函数](@entry_id:175678)，它为任何非零实数 $a$ 定义了一个正则[分布](@entry_id:182848)。

#### [奇异分布](@entry_id:265958)

[奇异分布](@entry_id:265958)是那些不能表示为 $\langle T_f, \phi \rangle = \int f(x)\phi(x)dx$ 形式的[分布](@entry_id:182848)，其中 $f$ 是一个[局部可积函数](@entry_id:175678)。最著名也是最重要的[奇异分布](@entry_id:265958)是**狄拉克 (Dirac) delta [分布](@entry_id:182848)**。以点 $c$ 为中心的 delta [分布](@entry_id:182848) $\delta_c$ 定义为：
$$
\langle \delta_c, \phi \rangle = \phi(c)
$$
它的作用就是“筛选”出检验函数在点 $c$ 的值。可以证明，不存在任何一个[局部可积函数](@entry_id:175678) $f(x)$ 能够满足 $\int f(x)\phi(x)dx = \phi(c)$ 对所有 $\phi$ 成立。

### [分布](@entry_id:182848)上的运算

[分布理论](@entry_id:186499)的真正威力在于它能够将微积分中的基本运算（如[微分](@entry_id:158718)、乘法）推广到[广义函数](@entry_id:182848)上。

#### [微分](@entry_id:158718)

[分布](@entry_id:182848)的[微分](@entry_id:158718)是其最深刻和最有用的概念之一。我们从正则[分布](@entry_id:182848)的观察中获得启发。假设 $f(x)$ 是一个[可微函数](@entry_id:144590)，其导数 $f'(x)$ 也是局部可积的。那么，由 $f'$ 定义的[分布](@entry_id:182848) $T_{f'}$ 的作用是：
$$
\langle T_{f'}, \phi \rangle = \int_{-\infty}^{\infty} f'(x)\phi(x) \, dx
$$
利用分部积分法（并注意到 $\phi$ 的[紧支集](@entry_id:276214)使得边界项为零），我们得到：
$$
\int_{-\infty}^{\infty} f'(x)\phi(x) \, dx = [f(x)\phi(x)]_{-\infty}^{\infty} - \int_{-\infty}^{\infty} f(x)\phi'(x) \, dx = - \int_{-\infty}^{\infty} f(x)\phi'(x) \, dx = - \langle T_f, \phi' \rangle
$$
这个关系式 $\langle T_{f'}, \phi \rangle = - \langle T_f, \phi' \rangle$ 将导数的作用从 $f$ “转移”到了检验函数 $\phi$ 上。[分布理论](@entry_id:186499)将此关系提升为一个**定义**。对于任意一个[分布](@entry_id:182848) $T$（无论是正则的还是奇异的），它的**[分布导数](@entry_id:181138)** $T'$ 定义为：
$$
\langle T', \phi \rangle \equiv - \langle T, \phi' \rangle
$$
这个定义是革命性的，因为它允许我们为任何[分布](@entry_id:182848)（包括[不连续函数](@entry_id:143848)甚至更奇异的对象）定义导数。

**示例 1：[阶跃函数](@entry_id:159192)的导数**
考虑一个在 $[a, b]$ 上的[特征函数](@entry_id:186820)（或矩形脉冲）$\chi_{[a,b]}(x)$，它在区间内为 1，区间外为 0 [@problem_id:2113995]。这是一个[不连续函数](@entry_id:143848)，在 $x=a$ 和 $x=b$ 处有跳跃。它的[分布导数](@entry_id:181138) $T'_{\chi_{[a,b]}}$ 作用于 $\phi$ 时为：
$$
\langle T'_{\chi_{[a,b]}}, \phi \rangle = - \langle T_{\chi_{[a,b]}}, \phi' \rangle = - \int_{-\infty}^{\infty} \chi_{[a,b]}(x) \phi'(x) \, dx = - \int_a^b \phi'(x) \, dx
$$
根据微积分基本定理，这个积分等于 $-[\phi(x)]_a^b = -(\phi(b) - \phi(a)) = \phi(a) - \phi(b)$。我们认出这个结果正是 $\langle \delta_a, \phi \rangle - \langle \delta_b, \phi \rangle = \langle \delta_a - \delta_b, \phi \rangle$。因此，我们得到了一个优美的结果：
$$
(\chi_{[a,b]})' = \delta_a - \delta_b
$$
一个函数在某点发生单位大小的向上跳跃，其导数就是该点处的一个正 delta [分布](@entry_id:182848)；向下跳跃则对应一个负 delta [分布](@entry_id:182848)。

**示例 2：[连续但不可导](@entry_id:261860)函数的导数**
现在考虑连续的“帐篷函数” $f(x) = \max(0, 1-|x|)$ [@problem_id:1867062]。这个函数在 $x=-1, 0, 1$ 处有“尖角”，在经典意义下不可导。它的[分布导数](@entry_id:181138)是：
$$
\langle T'_f, \phi \rangle = - \int_{-1}^{1} f(x) \phi'(x) \, dx = - \left[ \int_{-1}^{0} (1+x)\phi'(x)dx + \int_{0}^{1} (1-x)\phi'(x)dx \right]
$$
对两个积分分别进行分部积分，经过计算可以得到：
$$
\langle T'_f, \phi \rangle = \int_{-1}^{0} (1) \cdot \phi(x) dx + \int_{0}^{1} (-1) \cdot \phi(x) dx
$$
这个结果可以被看作是一个函数 $g(x)$ 的作用，其中 $g(x)$ 在 $(-1,0)$ 上为 1，在 $(0,1)$ 上为 -1，在其他地方为 0。这正是 $f(x)$ 在其可导区间上的经典导数。[分布导数](@entry_id:181138)自然地填补了不可导点，给出了一个全局一致的导数概念。

#### 与[光滑函数](@entry_id:267124)的乘积

一个[分布](@entry_id:182848) $T$ 可以与一个任意光滑的函数 $f \in C^\infty(\mathbb{R})$ 相乘，得到一个新的[分布](@entry_id:182848) $fT$。其定义也遵循“将操作转移到[检验函数](@entry_id:166589)上”的原则：
$$
\langle fT, \phi \rangle \equiv \langle T, f\phi \rangle
$$
由于 $f$ 是光滑的且 $\phi$ 是检验函数，它们的乘积 $f\phi$ 仍然是一个[检验函数](@entry_id:166589)（无限可微且具有[紧支集](@entry_id:276214)），因此这个定义是合理的。

我们可以结合[微分](@entry_id:158718)和乘法法则来推导[分布](@entry_id:182848)的代数恒等式。例如，让我们来简化表达式 $\alpha (x - \beta) \delta'(x - \gamma)$ [@problem_id:2114007]。根据定义，其作用于 $\phi$ 为：
$$
\langle \alpha (x - \beta) \delta'(x - \gamma), \phi \rangle = \langle \delta'(x - \gamma), \alpha (x - \beta) \phi(x) \rangle
$$
应用导数定义，并令 $\psi(x) = \alpha (x - \beta) \phi(x)$：
$$
= - \langle \delta(x - \gamma), \psi'(x) \rangle = - \psi'(\gamma)
$$
使用[乘法法则](@entry_id:144424)计算 $\psi'(x) = \alpha[\phi(x) + (x-\beta)\phi'(x)]$，于是在 $x=\gamma$ 处的值为 $\psi'(\gamma) = \alpha[\phi(\gamma) + (\gamma-\beta)\phi'(\gamma)]$。代入上式得到：
$$
\langle \alpha (x - \beta) \delta'(x - \gamma), \phi \rangle = -\alpha\phi(\gamma) - \alpha(\gamma-\beta)\phi'(\gamma)
$$
将右边与 delta [分布](@entry_id:182848)及其导数的定义 $\langle \delta_\gamma, \phi \rangle = \phi(\gamma)$ 和 $\langle \delta'_\gamma, \phi \rangle = -\phi'(\gamma)$ 进行比较，我们发现：
$$
-\alpha\phi(\gamma) - \alpha(\gamma-\beta)\phi'(\gamma) = \langle -\alpha\delta_\gamma + \alpha(\gamma-\beta)\delta'_\gamma, \phi \rangle
$$
因此，我们证明了[分布](@entry_id:182848)恒等式：
$$
\alpha (x - \beta) \delta'(x - \gamma) = -\alpha \delta(x - \gamma) + \alpha(\gamma - \beta) \delta'(x - \gamma)
$$
一个重要的特例是令 $\alpha=1, \beta=0, \gamma=0$，得到 $x\delta'(x) = -\delta(x)$。这些规则构成了[分布](@entry_id:182848)的微积分。

### [分布](@entry_id:182848)的收敛

[分布理论](@entry_id:186499)还提供了一种强大的方式来处理[函数序列的极限](@entry_id:142182)，这种[收敛方式](@entry_id:189917)被称为**[分布](@entry_id:182848)收敛**（convergence in the sense of distributions）。一个[分布](@entry_id:182848)序列 $\{T_n\}$ 收敛于[分布](@entry_id:182848) $T$，记作 $T_n \to T$，如果对于每一个[检验函数](@entry_id:166589) $\phi \in \mathcal{D}(\mathbb{R})$，[复数序列](@entry_id:175041) $\langle T_n, \phi \rangle$ 都收敛于复数 $\langle T, \phi \rangle$：
$$
\lim_{n \to \infty} \langle T_n, \phi \rangle = \langle T, \phi \rangle
$$

**示例 1：“新生”的 Delta 函数**
Delta [分布](@entry_id:182848)虽然是奇异的，但它可以被看作是一系列正则[分布](@entry_id:182848)的极限。考虑一个函数序列，其图像越来越高、越来越窄，同时保持其下方的总面积为 1。例如，“帐篷函数”序列 $g_k(x) = k(1-k|x|)$ (当 $|x| \le 1/k$ 时) [@problem_id:2114021]。对于任意[检验函数](@entry_id:166589) $\phi(x)$，可以证明：
$$
\lim_{k \to \infty} \langle T_{g_k}, \phi \rangle = \lim_{k \to \infty} \int_{-1/k}^{1/k} g_k(x)\phi(x) \, dx = \phi(0) = \langle \delta_0, \phi \rangle
$$
这表明函数序列 $g_k(x)$ 在[分布](@entry_id:182848)意义下收敛于 $\delta_0$。这类序列被称为**delta 序列**或**新生 delta 函数**。

**示例 2：剧烈[振荡](@entry_id:267781)的函数**
[分布](@entry_id:182848)收敛不依赖于逐点收敛。考虑函数序列 $f_n(x) = n\cos(nx)$ [@problem_id:1867042]。当 $n \to \infty$ 时，这个序列在任何一点上都不收敛，其振幅和频率都趋于无穷。然而，它对应的[分布](@entry_id:182848)序列 $T_{f_n}$ 却收敛于[零分布](@entry_id:195412)。对于任意 $\phi \in \mathcal{D}(\mathbb{R})$：
$$
\langle T_{f_n}, \phi \rangle = \int_{-\infty}^{\infty} n\cos(nx)\phi(x) \, dx = \int_{-\infty}^{\infty} (\sin(nx))'\phi(x) \, dx = - \int_{-\infty}^{\infty} \sin(nx)\phi'(x) \, dx
$$
根据 **Riemann-Lebesgue 引理**，最后一个积分当 $n \to \infty$ 时趋于 0。因此 $\lim_{n \to \infty} \langle T_{f_n}, \phi \rangle = 0 = \langle 0, \phi \rangle$。这说明，尽管 $f_n(x)$ 本身剧烈[振荡](@entry_id:267781)，但当它们作用于光滑的[检验函数](@entry_id:166589)时，这些[振荡](@entry_id:267781)被“平均掉”了。

**示例 3：导数作为极限**
[分布](@entry_id:182848)的导数也可以通过极限过程来理解。考虑[分布](@entry_id:182848)序列 [@problem_id:1867064]：
$$
T_n = \alpha n^2 (\delta_{1/n} + \delta_{-1/n} - 2\delta_0) + \beta n (\delta_{1/n} - \delta_{-1/n})
$$
让我们考察其作用于 $\phi$ 后的极限。将 $\phi$ 在 0 附近进行泰勒展开：$\phi(h) = \phi(0) + \phi'(0)h + \frac{1}{2}\phi''(0)h^2 + \dots$。令 $h=1/n$，我们发现：
*   $n(\phi(1/n) - \phi(-1/n)) = n(2\phi'(0)/n + O(1/n^3)) \to 2\phi'(0)$
*   $n^2(\phi(1/n) + \phi(-1/n) - 2\phi(0)) = n^2(\phi''(0)/n^2 + O(1/n^4)) \to \phi''(0)$
这些表达式正是数值分析中一阶和[二阶导数](@entry_id:144508)的[中心差分近似](@entry_id:177025)。取极限后，我们得到：
$$
\lim_{n \to \infty} \langle T_n, \phi \rangle = \alpha \phi''(0) + 2\beta\phi'(0)
$$
回顾 delta 导数的定义，$\langle \delta_0', \phi \rangle = -\phi'(0)$ 和 $\langle \delta_0'', \phi \rangle = \phi''(0)$，我们发现[极限分布](@entry_id:174797)是：
$$
T = \alpha \delta_0'' - 2\beta \delta_0'
$$
这个例子优美地揭示了[分布导数](@entry_id:181138)与导数的差分近似之间的深刻联系。

### 进阶主题：[柯西主值](@entry_id:192761)与[分布](@entry_id:182848)的阶

#### [柯西主值](@entry_id:192761)

函数 $f(x) = 1/x$ 在 $x=0$ 附近不是局部可积的，因此它不能直接定义一个正则[分布](@entry_id:182848)。然而，我们可以通过**[柯西主值](@entry_id:192761)** (Cauchy Principal Value) 的方式来赋予它意义。$P_v(1/x)$ [分布](@entry_id:182848)定义为：
$$
\left\langle P_v\left(\frac{1}{x}\right), \phi \right\rangle = \lim_{\epsilon \to 0^+} \left( \int_{-\infty}^{-\epsilon} \frac{\phi(x)}{x}dx + \int_{\epsilon}^{\infty} \frac{\phi(x)}{x}dx \right)
$$
通过对称地挖去原点附近的区间，我们使得这个极限对于所有检验函数都存在且有限 [@problem_id:1867065]。[柯西主值](@entry_id:192761)提供了一种处理非[可积奇点](@entry_id:634345)的方法，在物理学和工程中有重要应用。

#### [分布](@entry_id:182848)的阶

[分布](@entry_id:182848)的连续性条件可以被量化，从而引出**[分布](@entry_id:182848)的阶**（order of a distribution）的概念。一个[分布](@entry_id:182848) $T$ 被称为是 $k$ 阶的，如果它的作用可以被[检验函数](@entry_id:166589)及其直到 $k$ 阶导数的最大值所控制。更形式化地，对于任意紧集 $K$，存在常数 $C$ 使得对所有支集在 $K$ 内的 $\phi$ 都有：
$$
|\langle T, \phi \rangle| \le C \sum_{j=0}^{k} \sup_{x \in K} |\phi^{(j)}(x)|
$$
[分布](@entry_id:182848)的阶是满足此条件的最小整数 $k$。阶数可以看作是衡量[分布](@entry_id:182848)“奇异性”程度的指标。
*   正则[分布](@entry_id:182848)是 **0 阶**的。
*   Dirac delta [分布](@entry_id:182848) $\delta_c$ 也是 **0 阶**的，因为 $|\langle \delta_c, \phi \rangle| = |\phi(c)| \le \sup_x |\phi(x)|$。
*   delta [分布](@entry_id:182848)的导数 $\delta_c'$ 是 **1 阶**的，因为其作用涉及 $\phi'$。
*   可以证明，[柯西主值](@entry_id:192761)[分布](@entry_id:182848) $P_v(1/x)$ 也是 **1 阶**的 [@problem_id:1867065]。

[分布理论](@entry_id:186499)通过将函数的概念从逐点赋值扩展到线性泛函，为数学和物理学提供了一个极其强大和灵活的框架。它不仅能容纳像 delta 函数这样的奇异对象，还能以一种自然和一致的方式将微积分的法则推广到这些对象上。