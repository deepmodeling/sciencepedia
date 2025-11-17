## 引言
缓增[分布](@entry_id:182848)是现代分析学，特别是函数分析中的一个基石性概念，它由法国数学家[Laurent Schwartz](@entry_id:261056)在20世纪中叶创立。这一理论深刻地推广了函数的概念，为处理经典分析中难以驾驭的对象——例如物理学中的点电荷、信号处理中的瞬时脉冲，或数学中的[奇异点](@entry_id:199525)——提供了统一而严谨的数学框架。传统函数理论在面对这些具有“无限”集中或无限增长特性的理想化模型时常常捉襟见肘，而[分布理论](@entry_id:186499)的出现恰好填补了这一知识空白，使得[微分](@entry_id:158718)、积分和[傅里叶变换](@entry_id:142120)等强大工具能够在更广阔的舞台上施展。

本文将带领读者系统地学习缓增[分布](@entry_id:182848)的理论与实践。通过以下三个章节的探索，你将掌握如何从数学上精确定义这些[广义函数](@entry_id:182848)，并学会运用它们来解决实际问题：
- 在“原理与机制”一章中，我们将从[Schwartz空间](@entry_id:266248)出发，建立缓增[分布](@entry_id:182848)的严格定义，区分正则[分布](@entry_id:182848)与[奇异分布](@entry_id:265958)，并详细阐述[分布](@entry_id:182848)的求导、乘法和[傅里叶变换](@entry_id:142120)等核心运算。
- 接着，在“应用与交叉学科联系”一章中，我们将展示该理论在物理学、工程学和信号处理等领域的强大威力，看它如何为[静电学](@entry_id:140489)、结构力学和理想采样等问题提供清晰的数学描述。
- 最后，在“动手实践”部分，你将通过解决具体问题来巩固所学知识，将抽象的理论转化为实际的计算能力。

## 原理与机制

继引言之后，本章将深入探讨缓增[分布理论](@entry_id:186499)的核心原理与机制。我们将从其严格的数学定义出发，探索如何识别与构造缓增[分布](@entry_id:182848)，并阐述在其上定义的各种运算，如求导、乘法和收敛。最后，我们将讨论一些深刻的结构性定理，这些定理揭示了缓增[分布](@entry_id:182848)的内在本质。

### 缓增[分布](@entry_id:182848)的定义

缓增[分布](@entry_id:182848)的概念是对传统函数概念的深刻推广，它为处理在经典分析中行为奇异（如点脉冲）或增长过快（如多项式）的对象提供了一个坚实的框架。其定义建立在测试[函数空间](@entry_id:143478)与[连续线性泛函](@entry_id:262913)这两个基石之上。

#### 从函数到泛函：[Schwartz空间](@entry_id:266248)

我们首先需要一个合适的“标尺”来“测量”我们感兴趣的[广义函数](@entry_id:182848)。这个标尺就是**[Schwartz空间](@entry_id:266248)**，记为 $\mathcal{S}(\mathbb{R})$。它由所有在实数轴 $\mathbb{R}$ 上无限次可微（即光滑）的[复值函数](@entry_id:196054) $\phi(x)$ 组成，这些函数及其所有阶的导数在无穷远处都以比任何多项式的倒数更快的速度衰减。

更形式化地，一个函数 $\phi$ 属于 $\mathcal{S}(\mathbb{R})$，如果对于任意非负整数 $\alpha$ 和 $\beta$，其对应的**[半范数](@entry_id:264573)** $p_{\alpha, \beta}(\phi)$ 都是有限的：
$$
p_{\alpha, \beta}(\phi) = \sup_{x \in \mathbb{R}} \left| x^{\alpha} \frac{d^{\beta}\phi(x)}{dx^{\beta}} \right| \lt \infty
$$
这个[半范数](@entry_id:264573)族定义了 Schwartz 空间的拓扑结构。$x^\alpha$ 项保证了函数及其导数在 $|x| \to \infty$ 时的快速衰减，而 $\frac{d^\beta}{dx^\beta}$ 项则要求函数无限光滑。[高斯函数](@entry_id:261394) $\exp(-x^2)$ 是 Schwartz 空间中函数的典型例子。

#### 连续性与缓增[分布](@entry_id:182848)

有了测试函数空间，我们便可以定义**缓增[分布](@entry_id:182848)**（Tempered Distribution）。一个缓增[分布](@entry_id:182848) $T$ 是 Schwartz 空间 $\mathcal{S}(\mathbb{R})$ 上的一个**[连续线性泛函](@entry_id:262913)**。这意味着 $T$ 是一个映射 $T: \mathcal{S}(\mathbb{R}) \to \mathbb{C}$，满足：
1.  **线性性**: 对任意 $\phi, \psi \in \mathcal{S}(\mathbb{R})$ 和 $a, b \in \mathbb{C}$，有 $\langle T, a\phi + b\psi \rangle = a\langle T, \phi \rangle + b\langle T, \psi \rangle$。
2.  **连续性**: 如果一列测试函数 $\phi_n$ 在 $\mathcal{S}(\mathbb{R})$ 的拓扑中收敛到 $0$，那么[复数序列](@entry_id:175041) $\langle T, \phi_n \rangle$ 收敛到 $0$。

连续性条件有一个更实用、更具体的等价表述：存在一个正常数 $C$ 以及一对非负整数 $M$ 和 $N$，使得对于所有的测试函数 $\phi \in \mathcal{S}(\mathbb{R})$，以下不等式成立 [@problem_id:1884903]：
$$
|\langle T, \phi \rangle| \leq C \max_{0 \leq \alpha \leq M, 0 \leq \beta \leq N} p_{\alpha, \beta}(\phi)
$$
这个不等式直观地说明，[分布](@entry_id:182848) $T$ 的作用受制于测试函数自身及其导数的有限个“衰减-[振荡](@entry_id:267781)”度量。

#### 正则缓增[分布](@entry_id:182848)：缓增函数

许多普通的函数自身就可以被看作是缓增[分布](@entry_id:182848)。一个局部可积的函数 $f(x)$ 可以通过积分定义一个**正则[分布](@entry_id:182848)** $T_f$：
$$
\langle T_f, \phi \rangle = \int_{-\infty}^{\infty} f(x)\phi(x)dx
$$
然而，并非所有[局部可积函数](@entry_id:175678)都能定义一个缓增[分布](@entry_id:182848)。为了确保上述积分对所有 $\phi \in \mathcal{S}(\mathbb{R})$ 都收敛，并且 $T_f$ 满足连续性条件，函数 $f(x)$ 的增长速度必须受到限制。

我们称一个函数 $f(x)$ 是**缓增**的（或称**[多项式增长](@entry_id:177086)**的），如果存在常数 $C > 0$ 和一个非负整数 $k$，使得对于所有 $x \in \mathbb{R}$，不等式 $|f(x)| \le C(1+|x|)^{k}$ 成立 [@problem_id:1884904] [@problem_id:1884888]。一个基本定理指出，一个[局部可积函数](@entry_id:175678) $f$ 定义了一个正则缓增[分布](@entry_id:182848)，当且仅当 $f$ 是一个缓增函数。

例如，函数 $f_1(x) = x^{10} \sin(\sqrt{1+x^2})$ 是缓增的，因为 $|f_1(x)| \leq |x|^{10} \leq (1+|x|)^{10}$。函数 $f_2(x) = \exp(-x^2)$ 是有界的，因此也是缓增的（取 $k=0$）。函数 $f_4(x) = \frac{\ln(2+x^2)}{1+|x|}$ 也是缓增的，因为它可以被 $1+|x|$ 控制。这些函数都定义了正则缓增[分布](@entry_id:182848) [@problem_id:1884904]。

相反，像 $f(x) = \exp(ax^2)$ ($a>0$) 或 $h(x) = \cosh(2x)$ 这样的[指数增长](@entry_id:141869)函数，它们的增长速度超过任何多项式，因此它们不是缓增函数。我们可以找到一个 Schwartz 函数 $\phi(x)$（例如一个尾部形如 $\exp(-|x|)$ 的函数），使得积分 $\int f(x)\phi(x)dx$ 发散。因此，[指数增长](@entry_id:141869)的函数不能定义缓增[分布](@entry_id:182848) [@problem_id:1884913] [@problem_id:1884888]。

对于有界[连续函数](@entry_id:137361) $f(x)$，证明其定义了一个缓增[分布](@entry_id:182848)的方法极具启发性。设 $B = \sup_{x \in \mathbb{R}}|f(x)|$，我们有：
$$
|\langle T_f, \phi \rangle| \le B \int_{-\infty}^{\infty} |\phi(x)|dx
$$
为了将上式与 Schwartz [半范数](@entry_id:264573)联系起来，我们引入一个可积的权重因子：
$$
|\phi(x)| = \frac{(1+x^2)|\phi(x)|}{1+x^2} \le \frac{\sup_{y \in \mathbb{R}}|(1+y^2)\phi(y)|}{1+x^2}
$$
积分后得到：
$$
\int_{-\infty}^{\infty} |\phi(x)|dx \le \left(\int_{-\infty}^{\infty}\frac{dx}{1+x^2}\right) \sup_{y \in \mathbb{R}}|(1+y^2)\phi(y)| = \pi \sup_{y \in \mathbb{R}}|(1+y^2)\phi(y)|
$$
由于 $\sup |(1+y^2)\phi(y)| \le \sup |\phi(y)| + \sup |y^2\phi(y)| = p_{0,0}(\phi) + p_{2,0}(\phi)$，这就证明了 $|\langle T_f, \phi \rangle|$ 可以被[半范数](@entry_id:264573) $p_{0,0}$ 和 $p_{2,0}$ 的组合所控制，从而满足了缓增[分布](@entry_id:182848)的定义 [@problem_id:1884903]。这一技巧表明，任何 $L^p(\mathbb{R})$ 空间中的函数（对于 $1 \le p \le \infty$）都能定义一个缓增[分布](@entry_id:182848) [@problem_id:1884913]。

#### 奇异缓增[分布](@entry_id:182848)：[超越函数](@entry_id:271750)

[分布理论](@entry_id:186499)的真正威力在于它能够严谨地处理那些不是传统意义上函数的“奇异”对象。

**狄拉克 $\delta$ [分布](@entry_id:182848)**是其中最著名的例子。它被定义为一个在原点处取值的泛函：
$$
\langle \delta_0, \phi \rangle = \phi(0)
$$
更一般地，对于任意点 $a \in \mathbb{R}$，$\langle \delta_a, \phi \rangle = \phi(a)$。这是一个**[奇异分布](@entry_id:265958)**，因为它不能表示为任何[局部可积函数](@entry_id:175678)的积分。
我们可以验证 $\delta_a$ 是一个缓增[分布](@entry_id:182848)。其作用的大小可以被最简单的[半范数](@entry_id:264573) $p_{0,0}(\phi) = \sup_x |\phi(x)|$ 控制：
$$
|\langle \delta_a, \phi \rangle| = |\phi(a)| \le \sup_{x \in \mathbb{R}} |\phi(x)| = p_{0,0}(\phi)
$$
这满足连续性条件，其中 $C=1, M=0, N=0$。类似地，一个由狄拉克[分布](@entry_id:182848)组成的有限线性组合 $T = \sum_{i=1}^{M} c_i \delta_{a_i}$ 也是一个缓增[分布](@entry_id:182848)。其范数界为：
$$
|\langle T, \phi \rangle| \le \sum_{i=1}^{M} |c_i||\phi(a_i)| \le \left(\sum_{i=1}^{M} |c_i|\right) \sup_x |\phi(x)| = \left(\sum_{i=1}^{M} |c_i|\right) p_{0,0}(\phi)
$$
这里，最小的 $M$ 和 $N$ 均为 $0$，常数 $C$ 可以取为 $\sum_{i=1}^{M} |c_i|$ [@problem_id:1884871]。

另一个重要的[奇异分布](@entry_id:265958)是**[柯西主值](@entry_id:192761)[分布](@entry_id:182848)** $T_{pv} = \text{p.v.}(\frac{1}{x})$，其定义为：
$$
\langle T_{pv}, \phi \rangle = \lim_{\epsilon \to 0^+} \int_{|x| \ge \epsilon} \frac{\phi(x)}{x} dx
$$
这个[分布](@entry_id:182848)处理了函数 $1/x$ 在原点的不[可积奇点](@entry_id:634345)。为了证明它是一个缓增[分布](@entry_id:182848)，我们可以将积分区域分为 $|x| \ge 1$ 和 $|x| \lt 1$ 两部分。
对于 $|x| \ge 1$ 的远场部分，我们有：
$$
\left| \int_{|x| \ge 1} \frac{\phi(x)}{x} dx \right| \le \int_{|x| \ge 1} \frac{|x\phi(x)|}{x^2} dx \le p_{1,0}(\phi) \int_{|x| \ge 1} \frac{1}{x^2} dx = 2p_{1,0}(\phi)
$$
对于 $|x| \lt 1$ 的近场部分，利用对称性可以消去[奇点](@entry_id:137764)：
$$
\int_{\epsilon \le |x|  \lt 1} \frac{\phi(x)}{x} dx = \int_{\epsilon}^1 \frac{\phi(x)-\phi(-x)}{x} dx
$$
根据[中值定理](@entry_id:141085)，$\phi(x)-\phi(-x) = 2x \phi'(\xi_x)$，其中 $\xi_x \in (-x,x)$。因此，积分部分的大小可以被 $\sup|\phi'(t)| = p_{0,1}(\phi)$ 控制。最终我们得到：
$$
|\langle T_{pv}, \phi \rangle| \le 2p_{1,0}(\phi) + 2p_{0,1}(\phi)
$$
这表明 $T_{pv}$ 是一个缓增[分布](@entry_id:182848)，其连续性依赖于测试函数的衰减性质（由 $p_{1,0}$ 体现）和[光滑性](@entry_id:634843)（由 $p_{0,1}$ 体现）[@problem_id:1884889]。

### 缓增[分布](@entry_id:182848)的运算

[分布理论](@entry_id:186499)的一个强大之处在于它允许我们将微积分中的标准运算（如求导、乘法）推广到奇异对象上。

#### [分布](@entry_id:182848)的导数

一个[分布](@entry_id:182848) $T$ 的**导数** $T'$ 被定义为其作用在测试函数导数上的结果，但带有一个负号。这个定义源于对正则[分布](@entry_id:182848)进行分部积分的观察：
$$
\langle (T_f)', \phi \rangle = \int f'(x)\phi(x)dx = - \int f(x)\phi'(x)dx = -\langle T_f, \phi' \rangle
$$
我们把这个关系提升为定义：对于任何缓增[分布](@entry_id:182848) $T$，其导数 $T'$ 也是一个缓增[分布](@entry_id:182848)，定义为：
$$
\langle T', \phi \rangle = -\langle T, \phi' \rangle \quad \text{for all } \phi \in \mathcal{S}(\mathbb{R})
$$
这个定义使得任何[分布](@entry_id:182848)都具有任意阶的导数，并且求导是一个连续操作。例如，我们可以计算 $\delta_0$ 的导数 $\delta_0'$：
$$
\langle \delta_0', \phi \rangle = -\langle \delta_0, \phi' \rangle = -\phi'(0)
$$
这意味着，那个将测试函数映射到其在原点的导数值的泛函 $L(\phi) = \phi'(0)$，实际上就是[分布](@entry_id:182848) $-\delta_0'$ [@problem_id:1884890]。这个简单的例子揭示了一个深刻的联系：对[分布](@entry_id:182848)求导，可以产生更高阶的“奇异性”。

#### 与[光滑函数](@entry_id:267124)的乘积

我们不能任意地将两个[分布](@entry_id:182848)相乘，这在数学上是一个著名难题（施瓦茨不可能定理）。然而，我们可以定义一个[分布](@entry_id:182848) $T$ 与一个**[光滑函数](@entry_id:267124)** $f \in C^\infty(\mathbb{R})$ 的乘积 $fT$。这个定义同样源自分部积分的启发，其作用方式为：
$$
\langle fT, \phi \rangle = \langle T, f\phi \rangle
$$
这里要求 $f$ 是光滑的，是为了保证对于任意 $\phi \in \mathcal{S}(\mathbb{R})$，乘积 $f\phi$ 仍然是一个合法的测试函数，即 $f\phi \in \mathcal{S}(\mathbb{R})$。如果 $f$ 只是一个普通函数，例如有不连续点，那么 $f\phi$ 可能不再光滑，导致 $\langle T, f\phi \rangle$ 没有定义。

一个典型的例子可以说明为何乘子需要光滑。考虑尝试定义[符号函数](@entry_id:167507) $\text{sgn}(x)$ 对应的[分布](@entry_id:182848)与 $\delta_0$ 的乘积。如果试图套用乘法定义，会得到 $\langle \text{sgn} \cdot \delta_0, \phi \rangle = \langle \delta_0, \text{sgn} \cdot \phi \rangle$。然而，如果 $\phi(0) \neq 0$，函数 $\psi(x) = \text{sgn}(x)\phi(x)$ 在 $x=0$ 处不连续，因此 $\psi$ 不是一个合法的测试函数，$\delta_0$ 无法作用于它。因此，由于 $\text{sgn}(x)$ 在 $x=0$ 处的不连续性（非光滑），乘积 $\text{sgn}(x)\delta_0$ 在标准[分布理论](@entry_id:186499)中是**无定义的** [@problem_id:1884905]。

#### 缓增[分布](@entry_id:182848)的收敛

序列 $\{T_n\}$ 在[分布](@entry_id:182848)意义上**收敛**于 $T$（记为 $T_n \to T$），指的是对于每一个固定的测试函数 $\phi \in \mathcal{S}(\mathbb{R})$，[复数序列](@entry_id:175041) $\langle T_n, \phi \rangle$ 都收敛到 $\langle T, \phi \rangle$。这种收敛也称为弱-*收敛。

分析这种收敛常常需要借助强大的分析工具，如[黎曼-勒贝格引理](@entry_id:140988)和[勒贝格控制收敛定理](@entry_id:158548)。考虑一个例子，序列 $f_n(x) = C \sin^2(nx) + D\exp(-x^2/n^2)$ 对应的[分布](@entry_id:182848) $T_n$。我们需要计算 $\lim_{n \to \infty} \langle T_n, \phi \rangle$：
$$
\lim_{n \to \infty} \int_{-\infty}^{\infty} \left(C \frac{1-\cos(2nx)}{2} + D\exp(-x^2/n^2)\right) \phi(x) dx
$$
根据[黎曼-勒贝格引理](@entry_id:140988)，高度[振荡](@entry_id:267781)的项 $\int \cos(2nx)\phi(x)dx$ 在 $n \to \infty$ 时趋于 $0$。对于 $\exp(-x^2/n^2)$ 项，其[逐点极限](@entry_id:193549)为 $1$。由于 $|\exp(-x^2/n^2)\phi(x)| \le |\phi(x)|$，且 $\phi(x)$ 可积，根据[控制收敛定理](@entry_id:137784)，我们可以[交换极限](@entry_id:141487)和积分的顺序。因此，极限为：
$$
\langle T, \phi \rangle = \int_{-\infty}^{\infty} \left(\frac{C}{2} + D\right)\phi(x)dx
$$
这表明[分布](@entry_id:182848)序列 $T_n$ 收敛到一个由[常数函数](@entry_id:152060) $g(x) = \frac{C}{2} + D$ 生成的正则[分布](@entry_id:182848) [@problem_id:1884870]。

### 缓增[分布](@entry_id:182848)的结构与应用

最后，我们探讨几个揭示缓增[分布](@entry_id:182848)更深层结构的定理和应用。

#### 导数作为[差商](@entry_id:136462)的极限

[分布导数](@entry_id:181138)的定义 $\langle T', \phi \rangle = -\langle T, \phi' \rangle$ 虽然在代数上简洁，但似乎与微积分中导数是[差商](@entry_id:136462)极限的直观相去甚远。实际上，这两者是统一的。定义平移算子 $(\tau_h \phi)(x) = \phi(x-h)$，其在[分布](@entry_id:182848)上的作用为 $\langle \tau_h T, \phi \rangle = \langle T, \tau_{-h} \phi \rangle$。我们可以构造[分布](@entry_id:182848)的[差商](@entry_id:136462)：
$$
D_h = \frac{\tau_{-h} T - T}{h}
$$
一个基本结果是，当 $h \to 0$ 时，$D_h$ 在[分布](@entry_id:182848)意义上收敛于 $T'$。也就是说，对任意 $\phi \in \mathcal{S}(\mathbb{R})$：
$$
\lim_{h \to 0} \langle D_h, \phi \rangle = \langle T', \phi \rangle
$$
我们可以验证这一点。根据[差商](@entry_id:136462)和伴随算子的定义，对任意 $\phi \in \mathcal{S}(\mathbb{R})$：
$$
\lim_{h \to 0} \langle D_h, \phi \rangle = \lim_{h \to 0} \left\langle \frac{\tau_{-h} T - T}{h}, \phi \right\rangle = \left\langle T, \lim_{h \to 0} \frac{\tau_h \phi - \phi}{h} \right\rangle
$$
由于 $\frac{\tau_h \phi - \phi}{h}(x) = \frac{\phi(x-h)-\phi(x)}{h}$ 在 $\mathcal{S}$ 中收敛于 $-\phi'(x)$，并且 $T$ 是连续的，我们得到：
$$
\lim_{h \to 0} \langle D_h, \phi \rangle = \langle T, -\phi' \rangle = \langle T', \phi \rangle
$$
这证实了导数定义的一致性 [@problem_id:1884873]。

#### [傅里叶变换](@entry_id:142120)与周期[分布](@entry_id:182848)

[傅里叶变换](@entry_id:142120)是缓增[分布理论](@entry_id:186499)的中心工具，因为 Schwartz 空间在[傅里叶变换](@entry_id:142120)下是封闭的。一个[分布](@entry_id:182848) $T$ 的**[傅里叶变换](@entry_id:142120)** $\hat{T}$ 同样是一个缓增[分布](@entry_id:182848)，其定义为：
$$
\langle \hat{T}, \phi \rangle = \langle T, \hat{\phi} \rangle
$$
其中 $\hat{\phi}(\xi) = \int e^{-ix\xi}\phi(x)dx$。这个定义将函数的[傅里叶变换](@entry_id:142120)性质（如求导变为乘多项式）完美地推广到了[分布](@entry_id:182848)。例如，$(\widehat{T'})(\xi) = i\xi \hat{T}(\xi)$。

[傅里叶变换](@entry_id:142120)在分析周期性结构时尤为强大。一个重要的结果是，一个周期为 $P$ 的[分布](@entry_id:182848)，其[傅里叶变换](@entry_id:142120)的**支撑集**（即[分布](@entry_id:182848)不为零的区域）必定位于一个离散的格点上，即 $\{ \frac{2\pi k}{P} \mid k \in \mathbb{Z} \}$。这意味着[周期信号](@entry_id:266688)的[频谱](@entry_id:265125)是离散的。

例如，考虑一个周期为 $P$ 的脉冲串 $T = \sum_{n \in \mathbb{Z}} (\delta_{nP} - \alpha \delta_{nP}'')$。利用[傅里叶变换的线性](@entry_id:268418)和求导性质，我们可以计算出其[傅里叶变换](@entry_id:142120) $\hat{T}$。$\widehat{\delta_a}(\xi) = e^{-ia\xi}$，而 $\widehat{\delta_a''}(\xi) = (i\xi)^2 e^{-ia\xi} = -\xi^2 e^{-ia\xi}$。因此，
$$
\hat{T}(\xi) = \sum_{n \in \mathbb{Z}} (1+\alpha\xi^2) e^{-inP\xi} = (1+\alpha\xi^2) \sum_{n \in \mathbb{Z}} e^{-inP\xi}
$$
根据泊松求和公式，$\sum_{n \in \mathbb{Z}} e^{-inP\xi} = \frac{2\pi}{P} \sum_{k \in \mathbb{Z}} \delta(\xi - \frac{2\pi k}{P})$。因此，$\hat{T}$ 是一个位于[频域](@entry_id:160070)格点上的狄拉克梳：
$$
\hat{T}(\xi) = \frac{2\pi}{P} \sum_{k \in \mathbb{Z}} \left(1+\alpha\left(\frac{2\pi k}{P}\right)^2\right) \delta\left(\xi - \frac{2\pi k}{P}\right)
$$
其系数 $c_k = \frac{2\pi}{P}(1+\alpha(\frac{2\pi k}{P})^2)$ 反映了原始信号在每个谐波频率上的强度 [@problem_id:1884916]。

#### [缓增分布的结构定理](@entry_id:270246)

最后，一个深刻的**结构定理**揭示了所有缓增[分布](@entry_id:182848)的“基本形态”。该定理指出，任何缓增[分布](@entry_id:182848) $T \in \mathcal{S}'(\mathbb{R})$ 都可以表示为某个缓增[连续函数](@entry_id:137361) $g(x)$ 的有限阶导数。即，存在一个非负整数 $k$ 和一个满足 $|g(x)| \le C(1+|x|)^N$ 的[连续函数](@entry_id:137361) $g$，使得：
$$
T = \frac{d^k g}{dx^k} \quad (\text{在分布意义上})
$$
这个定理意味着，无论一个[分布](@entry_id:182848)多么“奇异”（如 $\delta_0$ 或其导数），它总可以通过对一个行为良好的[连续函数](@entry_id:137361)求有限次导数得到。从另一个角度看，任何[分布](@entry_id:182848)在经过足够多次“积分”后，总会变得“正则”（至少是连续的）。

我们可以用[柯西主值](@entry_id:192761)[分布](@entry_id:182848) $\text{p.v.}(\frac{1}{x})$ 来具体说明这个定理。我们已经知道 $(\ln|x|)' = \text{p.v.}(\frac{1}{x})$。但函数 $\ln|x|$ 在原点不连续。然而，如果我们再积一次，考虑 $g_0(x) = x\ln|x|$（它在原点是连续的，值为 $0$），我们发现它的二阶[分布导数](@entry_id:181138)是 $(\ln|x|+1)'=\text{p.v.}(\frac{1}{x})$。因此，对于 $T = \text{p.v.}(\frac{1}{x})$，我们可以取 $k=2$。满足 $g'' = T$ 的一般连续解是 $g(x) = x\ln|x| - x + ax + b$，其中 $a,b$ 是常数。通过施加特定的边界条件，例如 $g(1)=-1$ 和 $\int_{-1}^1 g(x)dx = -4/3$，我们可以唯一地确定 $g(x) = x\ln|x| - \frac{1}{3}x - \frac{2}{3}$ [@problem_id:1884882]。这个例子完美地展示了结构定理如何将一个[奇异分布](@entry_id:265958)与一个更具体的、行为良好的函数联系起来。