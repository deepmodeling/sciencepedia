## 引言
在[微分几何](@entry_id:145818)中，对连续变换和对称性的研究占据着核心地位。无论是描述流体中粒子的运动轨迹，还是刻画物理系统中随[时间演化](@entry_id:153943)的守恒量，我们都需要一个精确的数学框架来捕捉“连续运动”这一概念。[单参数微分同胚群](@entry_id:260697)，通常简称为“流”，正是为此而生的基本工具。它为[流形](@entry_id:153038)上的点如何随单一参数（如时间）平滑演变提供了严谨的描述。

然而，一个全局的、随时间演化的变换（流）与在每一点上的瞬时“速度”（矢量场）之间存在着怎样的深刻联系？我们又如何利用这种联系来量化其他几何对象（如函数或张量场）在这一演化过程中的变化？本文旨在系统性地回答这些问题，弥合宏观变换与微观生成元之间的理论鸿沟。

为实现这一目标，本文将分为三个核心部分。在“原理与机制”一章中，我们将建立流与矢量场之间的双向关系，并引入[李导数](@entry_id:171745)和李括号这两个强大的分析工具。接着，在“应用与跨学科联系”一章中，我们将展示这些抽象概念如何在物理学、动力系统和[流体力学](@entry_id:136788)等领域中找到具体的应用，揭示[对称性与守恒律](@entry_id:160300)的内在联系。最后，通过“动手实践”部分，读者将有机会通过解决具体问题来巩固所学知识。现在，让我们从构成这一切基础的核心原理与机制开始。

## 原理与机制

在本章中，我们将深入探讨[单参数微分同胚群](@entry_id:260697)的数学结构，并阐明其与矢量场之间的深刻联系。我们将从流（flow）的基本定义出发，引入其[无穷小生成元](@entry_id:270424)（infinitesimal generator）的概念，并最终探索李导数（Lie derivative）和李括号（Lie bracket）这两个核心工具。这些概念共同构成了研究[流形](@entry_id:153038)上连续对称性的基础。

### [单参数微分同胚群](@entry_id:260697)：流的定义

在[微分几何](@entry_id:145818)中，我们常常需要描述一个空间中的点如何随着时间的推移而连续地变换。这种连续变换的数学形式化就是**[单参数微分同胚群](@entry_id:260697)（one-parameter group of diffeomorphisms）**，通常简称为**流（flow）**。

一个定义在[流形](@entry_id:153038) $M$ 上的流是一个由实数参数 $t \in \mathbb{R}$ 索引的映射族 $\{\phi_t\}_{t \in \mathbb{R}}$，其中每个 $\phi_t: M \to M$ 都是一个从[流形](@entry_id:153038)到自身的[微分同胚](@entry_id:147249)（即光滑、可逆且逆映射也光滑的映射）。这个映射族必须满足以下两个基本性质：

1.  **单位元性质（Identity Property）**：当参数 $t=0$ 时，映射为恒等映射。也就是说，对于[流形](@entry_id:153038) $M$ 上的任意点 $p$，都有 $\phi_0(p) = p$。

2.  **群性质（Group Property）**：对于任意两个参数 $s, t \in \mathbb{R}$，映射的复合满足 $\phi_t \circ \phi_s = \phi_{t+s}$。这意味着，先演化时间 $s$ 再演化时间 $t$，其效果等同于一次性演化时间 $s+t$。

最直观的流的例子来自于一个均匀的运动。考虑一个在 $n$ 维[欧氏空间](@entry_id:138052) $\mathbb{R}^n$ 中以恒定速度向量 $v$ 运动的[粒子系统](@entry_id:180557)。任何一个点 $p$ 在时间 $t$ 后的位置由 $\phi_t(p) = p + vt$ 给出。我们可以验证这是否构成一个[单参数微分同胚群](@entry_id:260697)。首先，$\phi_0(p) = p + v \cdot 0 = p$，满足单位元性质。其次，我们考察其群性质。一个点 $p$ 先演化时间 $s$，到达 $\phi_s(p) = p + vs$。然后从这个新位置再演化时间 $t$，最终位置为 $\phi_t(\phi_s(p)) = (p + vs) + vt = p + v(s+t)$。这恰好等于一次性演化时间 $s+t$ 的结果，即 $\phi_{s+t}(p) = p+v(s+t)$。因此，$\phi_t \circ \phi_s = \phi_{s+t}$ 成立，这族映射构成了一个流 [@problem_id:1655341]。

然而，并非所有[参数化](@entry_id:272587)的映射族都满足群性质。例如，考虑 $\mathbb{R}^2$ 上的映射族 $\phi_t(x, y) = (x+t, y+t^2)$ [@problem_id:1655336]。当 $t=0$ 时，$\phi_0(x,y) = (x,y)$，单位元性质成立。但当我们计算复合映射时：
$$ (\phi_s \circ \phi_t)(x,y) = \phi_s(x+t, y+t^2) = ((x+t)+s, (y+t^2)+s^2) = (x+s+t, y+s^2+t^2) $$
另一方面，
$$ \phi_{s+t}(x,y) = (x+(s+t), y+(s+t)^2) = (x+s+t, y+s^2+2st+t^2) $$
比较两个结果的第二个分量，我们发现 $y+s^2+t^2 \neq y+s^2+2st+t^2$，除非 $st=0$。由于这个等式并非对所有 $s, t$ 都成立，所以群性质不满足。因此，这个映射族不是一个单参数群。这个例子提醒我们，群性质是一个非常严格的约束，它保证了变换的演化是“均匀”和“一致”的。

### 无穷小生成元：从流到矢量场

流描述了点在[流形](@entry_id:153038)上的连续运动轨迹，而**矢量场（vector field）**则描述了在每一点的瞬时速度。这两者之间存在着本质的联系。给定一个流 $\phi_t$，我们可以通过考察每个点在 $t=0$ 时的“初始速度”来定义一个矢量场，这个矢量场被称为流的**无穷小生成元（infinitesimal generator）**。

对于[流形](@entry_id:153038) $M$ 上的任意点 $p$，曲线 $\gamma_p(t) = \phi_t(p)$ 描述了从 $p$ 点出发的运动轨迹。该曲线在 $t=0$ 时的速度向量就是在点 $p$ 的切空间中的一个元素，我们将其定义为生成元矢量场 $X$ 在 $p$ 点的值 $X_p$：
$$ X_p = \frac{d}{dt}\bigg|_{t=0} \phi_t(p) $$
这个定义为我们提供了一个从给定的流反向求解其生成元矢量场的方法。

让我们看一个具体的例子。考虑 $\mathbb{R}^2$ 上的一个流，它描述了围绕原点的匀速旋转 [@problem_id:1528294]：
$$ \phi_t(x, y) = (x \cos(at) - y \sin(at), x \sin(at) + y \cos(at)) $$
其中 $a$ 是一个非零常数，代表[角速度](@entry_id:192539)。为了找到这个[旋转流](@entry_id:276737)的生成元 $X$，我们对任意一点 $p=(x_0, y_0)$ 计算其在 $t=0$ 时的速度：
$$ X_p = \frac{d}{dt}\bigg|_{t=0} \phi_t(x_0, y_0) = \frac{d}{dt}\bigg|_{t=0} \begin{pmatrix} x_0 \cos(at) - y_0 \sin(at) \\ x_0 \sin(at) + y_0 \cos(at) \end{pmatrix} $$
对每个分量求导，我们得到速度向量为：
$$ \begin{pmatrix} -ax_0 \sin(at) - ay_0 \cos(at) \\ ax_0 \cos(at) - ay_0 \sin(at) \end{pmatrix} $$
在 $t=0$ 时对其求值，得到：
$$ X_p = \begin{pmatrix} -ay_0 \\ ax_0 \end{pmatrix} $$
这意味着在点 $(x_0, y_0)$，生成元矢量场的分量是 $(-ay_0, ax_0)$。因此，生成元矢量场可以写作 $X = -ay \frac{\partial}{\partial x} + ax \frac{\partial}{\partial y}$。这个矢量场在每一点都与位置向量正交且大小成正比，精确地描述了旋转运动的瞬时速度场。

另一个重要的例子是[均匀缩放](@entry_id:267671)流 [@problem_id:1528251]。在 $\mathbb{R}^n$ 上，考虑流 $\phi_t(\mathbf{x}) = e^{at} \mathbf{x}$，其中 $\mathbf{x} = (x^1, \dots, x^n)$。它的生成元 $X$ 在点 $\mathbf{p}=(x^1, \dots, x^n)$ 的第 $i$ 个分量为：
$$ X^i(\mathbf{p}) = \frac{d}{dt}\bigg|_{t=0} (e^{at} x^i) = (a e^{at} x^i)\bigg|_{t=0} = a x^i $$
所以，生成元矢量场是 $X = \sum_{i=1}^n ax^i \frac{\partial}{\partial x^i}$。这个矢量场在每一点都沿着从原点出发的方向，其大小与到原点的距离成正比。

### [积分曲线](@entry_id:161858)：从矢量场到流

上一节我们看到了如何从流得到它的生成元矢量场。反过来，给定一个矢量场 $X$，我们能否重建它所生成的流 $\phi_t$？答案是肯定的，这需要通过求解**[积分曲线](@entry_id:161858)（integral curves）**来实现。

矢量场 $X$ 的一条[积分曲线](@entry_id:161858) $\gamma(t)$ 是一条在[流形](@entry_id:153038)上的路径，它在任意时刻 $t$ 的速度向量都等于该点处的矢量场值，即满足下面的常微分方程（ODE）：
$$ \frac{d\gamma(t)}{dt} = X(\gamma(t)) $$
给定一个初始点 $p$，我们可以求解上述方程并施加[初始条件](@entry_id:152863) $\gamma(0)=p$。这个唯一的解 $\gamma_p(t)$ 就描述了从点 $p$ 开始的运动轨迹。流映射 $\phi_t(p)$ 就是这条[积分曲线](@entry_id:161858)在时间 $t$ 的位置：
$$ \phi_t(p) = \gamma_p(t) $$
因此，寻找一个[矢量场的流](@entry_id:180235)就等价于求解一个以[流形](@entry_id:153038)上所有点为[初始条件](@entry_id:152863)的[常微分方程](@entry_id:147024)族。

让我们回到在 $\mathbb{R}^3$ 中描述匀速运动的常矢量场 $V = \sum_{i=1}^3 c^i \frac{\partial}{\partial x^i}$ [@problem_id:1528297]。为了找到它的流 $\phi_t$，我们需要为任意初始点 $p=(p^1, p^2, p^3)$ 求解[积分曲线](@entry_id:161858)方程。设曲线为 $x(t) = (x^1(t), x^2(t), x^3(t))$，则方程为：
$$ \frac{dx^i(t)}{dt} = V^i(x(t)) = c^i, \quad \text{初始条件 } x^i(0) = p^i $$
对每个分量积分，得到 $x^i(t) = c^i t + K^i$。代入[初始条件](@entry_id:152863)，$p^i = c^i \cdot 0 + K^i$，得出积分常数 $K^i = p^i$。因此，[积分曲线](@entry_id:161858)为 $x^i(t) = p^i + c^i t$。这就给出了流的表达式：
$$ \phi_t(p) = (p^1+c^1t, p^2+c^2t, p^3+c^3t) $$
这与我们最初作为流的例子完全一致，从而完成了从矢量场到流的构造。

### 矢量场的完备性

一个重要的问题是：一个矢量场的[积分曲线](@entry_id:161858)是否总能在任意长的时间 $t \in \mathbb{R}$ 内都存在？答案是否定的。如果一个矢量场的所有[积分曲线](@entry_id:161858)都能被定义在整个[实数轴](@entry_id:147286)上，那么这个矢量场被称为**完备的（complete）**。只有完备的矢量场才能生成一个定义在所有 $t \in \mathbb{R}$ 上的全局[单参数微分同胚群](@entry_id:260697)。

一个矢量场是否完备，不仅取决于矢量场本身，还取决于它所在的[流形](@entry_id:153038)。考虑一个简单的矢量场 $X = \frac{\partial}{\partial x}$。
- 如果[流形](@entry_id:153038)是整个实数线 $\mathbb{R}$，那么从任意点 $x_0$ 出发的[积分曲线](@entry_id:161858)方程为 $\frac{d\gamma}{dt}=1$，解为 $\gamma(t) = x_0+t$。这条曲线对于所有 $t \in \mathbb{R}$ 都停留在 $\mathbb{R}$ 中，因此 $X$ 在 $\mathbb{R}$ 上是完备的。
- 现在，考虑[流形](@entry_id:153038)为开区间 $M=(0,1)$ [@problem_id:1655337]。矢量场仍然是 $X = \frac{\partial}{\partial x}$。如果我们从点 $p = \frac{1}{3}$ 出发，[积分曲线](@entry_id:161858)同样是 $\gamma(t) = \frac{1}{3} + t$。但是，这条曲线必须始终保持在[流形](@entry_id:153038) $M=(0,1)$ 内部，即 $0  \gamma(t)  1$。这要求 $0  \frac{1}{3} + t  1$，解得 $-\frac{1}{3}  t  \frac{2}{3}$。当 $t$ 趋近于 $\frac{2}{3}$ 时，曲线就“逃离”了[流形](@entry_id:153038)。这意味着从 $p=\frac{1}{3}$ 出发的流 $\phi_t(p)$ 只在时间区间 $(-\frac{1}{3}, \frac{2}{3})$ 内有定义。由于流不是对所有 $t \in \mathbb{R}$都有定义，所以矢量场 $X = \frac{\partial}{\partial x}$ 在[流形](@entry_id:153038) $(0,1)$ 上是**不完备的（incomplete）**。

这个例子表明，紧致流形（compact manifold，即闭合且有界的[流形](@entry_id:153038)）上的任何光滑矢量场都是完备的。但在非紧致流形上，即使是像常矢量场这样简单的矢量场也可能是不完备的。

### 李导数：沿流的变化率

有了流和矢量场的概念，我们就可以提出一个核心问题：当一个点沿着[矢量场的流](@entry_id:180235)运动时，其他几何对象（如函数或矢量场）是如何变化的？**[李导数](@entry_id:171745)（Lie derivative）**正是衡量这种变化的工具。

#### 标量函数的[李导数](@entry_id:171745)

考虑一个标量函数 $f: M \to \mathbb{R}$ 和一个矢量场 $X$ 及其生成的流 $\phi_t$。我们可以通过比较点 $p$ 处的函数值 $f(p)$ 和被流推动后的点 $\phi_t(p)$ 处的函数值 $f(\phi_t(p))$ 来考察函数 $f$ 的变化。为了在一个固定的点 $p$ 上进行比较，我们使用**[拉回](@entry_id:160816)映射（pullback）** $\phi_t^*$，它将函数 $f$ 变换为一个新函数 $\phi_t^*f$，其定义为 $(\phi_t^*f)(p) = f(\phi_t(p))$。

函数 $f$ 沿矢量场 $X$ 的李导数 $(\mathcal{L}_X f)$ 定义为[拉回](@entry_id:160816)函数在 $t=0$ 时对时间 $t$ 的变化率：
$$ (\mathcal{L}_X f)(p) = \frac{d}{dt}\bigg|_{t=0} (\phi_t^*f)(p) = \frac{d}{dt}\bigg|_{t=0} f(\phi_t(p)) $$
这个定义直观地捕捉了函数值沿着流线的瞬时变化。

例如，让我们在 $M=\mathbb{R}$上计算函数 $f(x) = x^3 - 2x$ 沿着矢量场 $X = x \frac{\partial}{\partial x}$ 的[李导数](@entry_id:171745) [@problem_id:1528293]。
1.  首先，找到 $X$ 生成的流。[积分曲线](@entry_id:161858)方程为 $\frac{d\gamma}{dt} = \gamma$，初始条件为 $\gamma(0)=x$。解得 $\gamma(t) = x e^t$，所以流是 $\phi_t(x) = x e^t$。
2.  计算[拉回](@entry_id:160816)函数 $(\phi_t^*f)(x) = f(\phi_t(x)) = f(x e^t) = (x e^t)^3 - 2(x e^t) = x^3 e^{3t} - 2x e^t$。
3.  对时间 $t$ 求导并取 $t=0$：
    $$ (\mathcal{L}_X f)(x) = \frac{d}{dt}\bigg|_{t=0} (x^3 e^{3t} - 2x e^t) = (3x^3 e^{3t} - 2x e^t)\bigg|_{t=0} = 3x^3 - 2x $$
幸运的是，有一个更简单的计算方法。利用链式法则，我们可以证明李导数等于函数在矢量场方向上的[方向导数](@entry_id:189133)：
$$ (\mathcal{L}_X f)(p) = \frac{d}{dt}\bigg|_{t=0} f(\phi_t(p)) = df_p\left(\frac{d}{dt}\bigg|_{t=0} \phi_t(p)\right) = df_p(X_p) = X(f) $$
这里的 $X(f)$ 表示将矢量场 $X$ 视为一个作用在函数上的[微分算子](@entry_id:140145)。对于 $X = \sum X^i \frac{\partial}{\partial x^i}$，我们有 $X(f) = \sum X^i \frac{\partial f}{\partial x^i}$。用这个方法重新计算上一个例子：
$$ \mathcal{L}_X f = X(f) = \left(x \frac{\partial}{\partial x}\right)(x^3 - 2x) = x(3x^2 - 2) = 3x^3 - 2x $$
结果完全一致，但计算过程大大简化。

[李导数](@entry_id:171745)作为一个导数算子，满足**[莱布尼茨法则](@entry_id:157949)（Leibniz rule）**，即 $\mathcal{L}_X(fg) = (\mathcal{L}_X f)g + f(\mathcal{L}_X g)$。我们可以通过一个例子来验证这一点 [@problem_id:1528288]。设 $X = -y \frac{\partial}{\partial x} + x \frac{\partial}{\partial y}$（[旋转生成元](@entry_id:154292)），$f(x,y)=x^2+y^2$，$g(x,y)=xy$。
一方面，直接计算 $\mathcal{L}_X(fg)$:
$$ \mathcal{L}_X((x^2+y^2)(xy)) = \mathcal{L}_X(x^3y + xy^3) = (-y \frac{\partial}{\partial x} + x \frac{\partial}{\partial y})(x^3y+xy^3) $$
$$ = -y(3x^2y+y^3) + x(x^3+3xy^2) = -3x^2y^2 - y^4 + x^4 + 3x^2y^2 = x^4 - y^4 $$
另一方面，分别计算每一项：
$$ \mathcal{L}_X f = (-y)(2x) + (x)(2y) = 0 $$
$$ \mathcal{L}_X g = (-y)(y) + (x)(x) = x^2-y^2 $$
根据[莱布尼茨法则](@entry_id:157949)，$(\mathcal{L}_X f)g + f(\mathcal{L}_X g) = 0 \cdot (xy) + (x^2+y^2)(x^2-y^2) = x^4-y^4$。两者结果相同，验证了法则的成立。

#### 对称性与[不变量](@entry_id:148850)

李导数的一个极其重要的应用是识别**对称性**。如果一个函数 $f$ 在沿矢量场 $X$ 的流运动时保持不变，我们就说 $f$ 是**守恒的**或**不变的（invariant）**。从定义上看，这意味着它的[李导数](@entry_id:171745)为零：
$$ \mathcal{L}_X f = 0 $$
在物理学中，这对应于一个[守恒量](@entry_id:150267)。例如，在上面验证[莱布尼茨法则](@entry_id:157949)的例子中，我们发现对于[旋转生成元](@entry_id:154292) $X = -y \frac{\partial}{\partial x} + x \frac{\partial}{\partial y}$，函数 $f(x,y)=x^2+y^2$（半径的平方）的李导数为零，即 $\mathcal{L}_X(x^2+y^2)=0$。这精确地反映了一个几何事实：绕原点旋转不会改变任何点到原点的距离。

更一般地，我们可以考察什么样的函数在旋转下保持不变 [@problem_id:1528263]。考虑一个一般的二次型 $\phi(x,y) = \alpha x^2 + \beta y^2 + \gamma xy$。它的李导数是：
$$ \mathcal{L}_V \phi = (-y\frac{\partial}{\partial x} + x\frac{\partial}{\partial y})(\alpha x^2 + \beta y^2 + \gamma xy) = -y(2\alpha x + \gamma y) + x(2\beta y + \gamma x) $$
$$ = -2\alpha xy - \gamma y^2 + 2\beta xy + \gamma x^2 = \gamma(x^2 - y^2) + 2(\beta - \alpha)xy $$
要使这个函数在旋转下不变，即 $\mathcal{L}_V \phi = 0$ 对所有 $(x,y)$ 成立，必须有 $\gamma=0$ 且 $\beta - \alpha = 0$，即 $\alpha=\beta$。此时 $\phi(x,y) = \alpha(x^2+y^2)$。这表明，任何形式为 $h(x^2+y^2)$（其中 $h$ 是[可微函数](@entry_id:144590)）的函数都是旋转不变的，因为根据链式法则，$\mathcal{L}_V h(x^2+y^2) = h'(x^2+y^2) \mathcal{L}_V(x^2+y^2) = h'(x^2+y^2) \cdot 0 = 0$。

### 李括号：流的相互作用

我们可以将[李导数](@entry_id:171745)的概念从标量函数推广到矢量场。矢量场 $Y$ 沿矢量场 $X$ 的[李导数](@entry_id:171745)，记为 $\mathcal{L}_X Y$，被称为 $X$ 和 $Y$ 的**李括号（Lie bracket）**，通常写作 $[X,Y]$。它衡量了矢量场 $Y$ 如何沿着 $X$ 的流变化。

李括号 $[X,Y]$ 本身也是一个矢量场，其几何意义是深刻的：它度量了由 $X$ 和 $Y$ 生成的流的交换性。具体来说，**[李括号](@entry_id:636461)为零 $[X,Y]=0$ 的充要条件是它们的流相互交换**，即 $\phi_t^X \circ \phi_s^Y = \phi_s^Y \circ \phi_t^X$。

计算[李括号](@entry_id:636461)最直接的方式是将其视为[算子的交换子](@entry_id:261812)。对于任意光滑测试函数 $f$，李括号的作用定义为：
$$ [X,Y]f = X(Y(f)) - Y(X(f)) $$
让我们用一个基本例子来理解这一点。考虑 $\mathbb{R}^2$ 上的两个矢量场 $X=\frac{\partial}{\partial x}$ 和 $Y=\frac{\partial}{\partial y}$ [@problem_id:1655359]。$X$ 生成的是沿 $x$ 轴的平移流 $\phi_t^X(x,y)=(x+t, y)$，$Y$ 生成的是沿 $y$ 轴的平移流 $\phi_s^Y(x,y)=(x, y+s)$。直观上，先向右平移再向上平移，与先向上平移再向右平移，结果是相同的：
$$ (\phi_s^Y \circ \phi_t^X)(x,y) = \phi_s^Y(x+t, y) = (x+t, y+s) $$
$$ (\phi_t^X \circ \phi_s^Y)(x,y) = \phi_t^X(x, y+s) = (x+t, y+s) $$
因为流是可交换的，我们预期它们的[李括号](@entry_id:636461)为零。让我们用定义来验证：
$$ [X,Y]f = \frac{\partial}{\partial x}\left(\frac{\partial f}{\partial y}\right) - \frac{\partial}{\partial y}\left(\frac{\partial f}{\partial x}\right) = \frac{\partial^2 f}{\partial x \partial y} - \frac{\partial^2 f}{\partial y \partial x} $$
根据 Clairaut 定理（[光滑函数](@entry_id:267124)的[混合偏导数相等](@entry_id:138898)），上式等于零。因此 $[X,Y]=0$，这与流的可交换性完全吻合。

在[坐标系](@entry_id:156346)中，李括号有一个方便计算的公式。如果 $X = \sum X^i \frac{\partial}{\partial x^i}$ 和 $Y = \sum Y^j \frac{\partial}{\partial x^j}$，则它们的[李括号](@entry_id:636461) $Z=[X,Y]$ 的第 $k$ 个分量 $Z^k$ 是：
$$ Z^k = [X,Y]^k = \sum_{i} \left( X^i \frac{\partial Y^k}{\partial x^i} - Y^i \frac{\partial X^k}{\partial x^i} \right) = X(Y^k) - Y(X^k) $$
例如，我们来计算在 $\mathbb{R}^3$ 上的两个矢量场 $X = 3x \frac{\partial}{\partial x} + (y + 2x^2) \frac{\partial}{\partial y}$ 和 $Y = -y \frac{\partial}{\partial x} + x \frac{\partial}{\partial y}$ 的李括号 [@problem_id:1528266]。
$X$ 的分量为 $X^1=3x, X^2=y+2x^2, X^3=0$。
$Y$ 的分量为 $Y^1=-y, Y^2=x, Y^3=0$。

计算 $[X,Y]$ 的第一个分量：
$$ [X,Y]^1 = X(Y^1) - Y(X^1) = \left(3x \frac{\partial}{\partial x} + (y + 2x^2) \frac{\partial}{\partial y}\right)(-y) - \left(-y \frac{\partial}{\partial x} + x \frac{\partial}{\partial y}\right)(3x) $$
$$ = (y+2x^2)(-1) - (-y)(3) = -y - 2x^2 + 3y = 2y - 2x^2 $$

计算 $[X,Y]$ 的第二个分量：
$$ [X,Y]^2 = X(Y^2) - Y(X^2) = \left(3x \frac{\partial}{\partial x} + (y + 2x^2) \frac{\partial}{\partial y}\right)(x) - \left(-y \frac{\partial}{\partial x} + x \frac{\partial}{\partial y}\right)(y+2x^2) $$
$$ = (3x)(1) - ((-y)(4x) + (x)(1)) = 3x - (-4xy+x) = 2x+4xy $$

第三个分量显然为零。因此，[李括号](@entry_id:636461)为 $[X,Y] = (2y-2x^2)\frac{\partial}{\partial x} + (2x+4xy)\frac{\partial}{\partial y}$。由于结果不是[零矢量](@entry_id:155273)场，我们可以断定这两个矢量场生成的流是不可交换的。

综上所述，[单参数微分同胚群](@entry_id:260697)（流）及其无穷小生成元（矢量场）是同一几何实在的两个侧面。[李导数](@entry_id:171745)和[李括号](@entry_id:636461)为我们提供了强有力的分析工具，用以研究物体如何沿着流变化，以及不同流之间的相互作用，从而揭示[流形](@entry_id:153038)上深刻的对称性结构。