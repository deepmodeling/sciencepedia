## 引言
[一阶常微分方程](@entry_id:264241)是描述世界动态变化的基础数学语言，从物理系统的运动到[生物种群](@entry_id:200266)的演化，其应用无处不在。对于理工科学生而言，在深入学习[偏微分方程](@entry_id:141332)等更高级的数学物理方法之前，对[一阶常微分方程](@entry_id:264241)的理论和求解技巧进行一次系统性的回顾至关重要。本文旨在填补这一学习衔接上的需求，为读者构建一个坚实的基础。在接下来的内容中，我们将首先在“原理与机制”一章中，重新审视解的[存在性与唯一性](@entry_id:263101)，并系统梳理各类标准方程的求解方法；随后，在“应用与跨学科联系”一章中，我们将探索这些方程如何在物理、化学、生物及工程等多元领域中解决实际问题；最后，“动手实践”部分将提供精选习题，帮助读者巩固所学。通过这一结构化的学习路径，读者将能透彻理解[一阶常微分方程](@entry_id:264241)的核心，并为后续的学习与研究做好充分准备。

## 原理与机制

在深入探讨[偏微分方程](@entry_id:141332)的广阔领域之前，我们必须首先巩固[一阶常微分方程](@entry_id:264241)（ODE）的基础。这些方程是描述系统[瞬时变化率](@entry_id:141382)的数学语言，它们在物理学、工程学、生物学和经济学等众多领域中无处不在。本章旨在回顾求解[一阶常微分方程](@entry_id:264241)的核心原理和关键机制，为后续更复杂的分析奠定坚实的基础。我们将从解的[存在性与唯一性](@entry_id:263101)等基本理论问题入手，系统地梳理各类标准方程的求解方法，并探讨一些特殊的方程形式及其几何意义。

### 基本概念与定性分析

一个[一阶常微分方程](@entry_id:264241)通常可以表示为 $y' = f(x, y)$ 的形式，其中 $y' = \frac{dy}{dx}$ 表示函数 $y(x)$ 对自变量 $x$ 的导数。一个**解（solution）**是指一个函数 $y(x)$，当它被代入方程时，使得方程成为一个恒等式。通常，一个[微分方程](@entry_id:264184)会拥有一个包含任意常数的解族，称为**通解（general solution）**。若再给定一个**[初始条件](@entry_id:152863)**，如 $y(x_0) = y_0$，则该问题被称为**初值问题（Initial Value Problem, IVP）**，其解（如果唯一）是一个不含任意常数的**特解（particular solution）**。

在求得解析解之前，我们往往可以通过定性分析来理解解的大致行为。**[方向场](@entry_id:171896)（direction field）**是进行定性分析的有力工具，它在 $xy$ 平面上的每个点 $(x, y)$ 处绘制一个斜率为 $f(x, y)$ 的小线段，从而描绘出解曲线可能的[切线](@entry_id:268870)方向。

对于一类特殊的方程——**[自治方程](@entry_id:175719)（autonomous equations）**，其形式为 $\frac{dy}{dt} = f(y)$，即变化率仅依赖于函数值 $y$ 本身，而与自变量 $t$ 无关。对于这类系统，我们可以通过分析**[平衡点](@entry_id:272705)（equilibrium points）**来预测其长期行为。[平衡点](@entry_id:272705)是指导数 $\frac{dy}{dt}$ 为零的状态，即满足 $f(y)=0$ 的点。

一个典型的例子是描述 autocatalytic reaction （自催化反应）或种群增长的[逻辑斯谛方程](@entry_id:265689)（logistic equation）[@problem_id:2130067]。考虑一个反应物浓度 $C(t)$ 的变化率由以下方程决定：
$$ \frac{dC}{dt} = k C (C_{max} - C) $$
其中 $k$ 和 $C_{max}$ 是正的常数。[平衡点](@entry_id:272705)是使得 $\frac{dC}{dt} = 0$ 的 $C$ 值。显然，我们有两个[平衡点](@entry_id:272705)：$C_1 = 0$ 和 $C_2 = C_{max}$。

[平衡点](@entry_id:272705)的**稳定性（stability）**决定了系统在受到微小扰动后是会回到[平衡点](@entry_id:272705)还是远离它。要判断稳定性，我们可以考察函数 $f(C)$ 在[平衡点](@entry_id:272705) $C^*$ 附近的导数 $f'(C^*)$ 的符号。
*   如果 $f'(C^*) \lt 0$，则当 $C$ 略微偏离 $C^*$ 时，$\frac{dC}{dt}$ 的符号会促使 $C$ 回归到 $C^*$。这样的[平衡点](@entry_id:272705)称为**稳定[平衡点](@entry_id:272705)（stable equilibrium point）**或**吸引子（attractor）**。
*   如果 $f'(C^*) \gt 0$，则 $C$ 的微小偏离会被放大，导致其远离 $C^*$。这样的[平衡点](@entry_id:272705)称为**不稳定平衡点（unstable equilibrium point）**或**排斥子（repeller）**。

对于上述[逻辑斯谛模型](@entry_id:268065)，我们有 $f(C) = kC(C_{max} - C)$，其导数为 $f'(C) = k(C_{max} - 2C)$。
*   在 $C_1=0$ 处，$f'(0) = kC_{max} \gt 0$，因此 $C=0$ 是一个不稳定平衡点。
*   在 $C_2=C_{max}$ 处，$f'(C_{max}) = k(C_{max} - 2C_{max}) = -kC_{max} \lt 0$，因此 $C=C_{max}$ 是一个稳定[平衡点](@entry_id:272705)。

这意味着，只要初始浓度 $C(0)$ 处于 $(0, C_{max})$ 区间内，浓度 $C(t)$ 就会随着时间的推移而增加（因为在此区间内 $\frac{dC}{dt} \gt 0$），并最终趋近于稳定的平衡状态 $C_{max}$。

### 解的[存在性与唯一性](@entry_id:263101)

在着手求解一个初值问题 $y' = f(x, y)$, $y(x_0) = y_0$ 之前，一个基本的问题是：解是否存在？如果存在，它是否唯一？**皮卡-林德洛夫[存在性与唯一性](@entry_id:263101)定理（Picard-Lindelöf existence and uniqueness theorem）**为我们提供了回答这个问题的准则。

该定理指出，如果函数 $f(x, y)$ 以及它关于 $y$ 的偏导数 $\frac{\partial f}{\partial y}$ 在一个包含初始点 $(x_0, y_0)$ 的某个矩形区域 $R$ 内都是连续的，那么在包含 $x_0$ 的某个区间内，该初值问题存在唯一的解。

让我们通过一个例子来理解这一定理的应用[@problem_id:2130086]。考虑[微分方程](@entry_id:264184)：
$$ y' = \frac{y}{\sqrt{x}} $$
这里，$f(x, y) = \frac{y}{\sqrt{x}}$。为了应用[存在性与唯一性](@entry_id:263101)定理，我们还需要计算其关于 $y$ 的偏导数：
$$ \frac{\partial f}{\partial y} = \frac{1}{\sqrt{x}} $$
要使 $f(x, y)$ 和 $\frac{\partial f}{\partial y}$ 均为[连续函数](@entry_id:137361)，自变量 $x$ 必须大于零，即 $x \gt 0$。对于任何满足 $x_0 \gt 0$ 的初始点 $(x_0, y_0)$，我们总能找到一个完全位于[右半平面](@entry_id:277010)（$x \gt 0$）的矩形区域包含该点。因此，定理保证了对于任何定义在 $x \gt 0$ 区域内的[初始条件](@entry_id:152863)，都存在一个唯一的局部解。

反之，当定理的条件不被满足时，[解的唯一性](@entry_id:143619)就可能丧失。一个经典的例子是方程 $y' = \alpha \sqrt{|y|}$，其中 $\alpha$ 是一个正常数，初始条件为 $y(0) = 0$ [@problem_id:2130065]。
在这里，$f(t, y) = \alpha \sqrt{|y|}$ 在原点 $(0, 0)$ 是连续的。但是，当 $y \to 0$ 时，其关于 $y$ 的[偏导数](@entry_id:146280) $\frac{\partial f}{\partial y}$ 趋于无穷，因此在任何包含 $y=0$ 的区域内都不满足定理的第二个条件（即关于 $y$ 的[利普希茨连续性](@entry_id:142246)）。

这导致了非唯一解的出现。首先，我们能立即验证**[平凡解](@entry_id:155162)（trivial solution）** $y_1(t) = 0$ 对于所有 $t$ 都满足该[初值问题](@entry_id:144620)。
然而，通过分离变量法（我们将在稍后讨论），我们可以求得另一个非平凡解。假设 $y \gt 0$，则方程为 $y' = \alpha \sqrt{y}$。分离变量并积分：
$$ \int y^{-1/2} dy = \int \alpha dt \implies 2\sqrt{y} = \alpha t + C $$
应用初始条件 $y(0)=0$，我们得到 $C=0$，因此 $2\sqrt{y} = \alpha t$。解出 $y$ 得到 $y_2(t) = \frac{1}{4}\alpha^2 t^2$（对于 $t \ge 0$）。不难验证，这个解也满足[微分方程](@entry_id:264184)和[初始条件](@entry_id:152863)。

更有趣的是，我们可以构造出无穷多个解。我们可以将[平凡解](@entry_id:155162)和抛物线解“拼接”起来。例如，对于任何常数 $c \gt 0$，函数
$$ y(t) = \begin{cases} 0  \text{if } 0 \le t  c \\ \frac{1}{4}\alpha^2 (t-c)^2  \text{if } t \ge c \end{cases} $$
都是该[初值问题](@entry_id:144620)的有效解。这些解在 $t=c$ 处是连续且可微的（左右导数均为0），并且满足 $y(0)=0$。这个例子深刻地揭示了[存在性与唯一性](@entry_id:263101)定理中条件的必要性。

### [一阶常微分方程](@entry_id:264241)的标准求解方法

当解的存在性和唯一性得到保证后，我们的任务便是寻找解的具体形式。下面我们回顾几种最常见的[一阶常微分方程](@entry_id:264241)的求解技术。

#### 可分离变量方程

如果一个[微分方程](@entry_id:264184)可以写成 $\frac{dy}{dx} = g(x)h(y)$ 的形式，或者更对称地写成 $M(x)dx + N(y)dy = 0$，则称其为**可分离变量方程（separable equation）**。求解这类方程的策略非常直接：将所有含 $x$ 的项和 $dx$ 移到一边，所有含 $y$ 的项和 $dy$ 移到另一边，然后对两边分别积分。

例如，在一个[材料科学](@entry_id:152226)实验中，晶体细丝的长度 $L(t)$ 随时间 $t$ 的增长率由 $\frac{dL}{dt} = \frac{Ct}{L}$ 描述 [@problem_id:2130090]。这是一个可分离变量方程。我们可以将其重写为：
$$ L \, dL = C t \, dt $$
对两边进行定积分，从初始状态 $(t=0, L=L_0)$ 到任意状态 $(t, L)$：
$$ \int_{L_0}^{L} s \, ds = \int_{0}^{t} C\tau \, d\tau $$
$$ \frac{1}{2}L^2 - \frac{1}{2}L_0^2 = \frac{1}{2}Ct^2 $$
整理后得到 $L^2 = L_0^2 + Ct^2$。这个隐式解描述了细丝长度随时间变化的规律。

#### 线性方程

形如 $\frac{dy}{dx} + P(x)y = Q(x)$ 的方程被称为**[一阶线性常微分方程](@entry_id:164502)（first-order linear ODE）**。这[类方程](@entry_id:144428)的求解有一个系统的程序，即**[积分因子法](@entry_id:167338)（method of integrating factors）**。

其核心思想是找到一个函数 $\mu(x)$，称为**[积分因子](@entry_id:177812)（integrating factor）**，当方程两边同乘以 $\mu(x)$ 后，方程的左边恰好可以写成乘积 $\mu(x)y(x)$ 的导数。
$$ \mu(x)\frac{dy}{dx} + \mu(x)P(x)y = \mu(x)Q(x) $$
我们希望左边等于 $\frac{d}{dx}(\mu(x)y) = \mu(x)\frac{dy}{dx} + \frac{d\mu}{dx}y$。比较两式可知，我们需要 $\frac{d\mu}{dx} = \mu(x)P(x)$。这是一个可分离变量方程，解出 $\mu(x)$ 得到：
$$ \mu(x) = \exp\left(\int P(x)dx\right) $$
[积分因子](@entry_id:177812)找到后，原方程变为 $\frac{d}{dx}(\mu(x)y) = \mu(x)Q(x)$，两边积分即可求解。

考虑方程 $(1+t^2)\frac{dy}{dt} + 2ty = t^2$ [@problem_id:2130053]。首先，我们将其写成标准形式：
$$ \frac{dy}{dt} + \frac{2t}{1+t^2}y = \frac{t^2}{1+t^2} $$
这里 $P(t) = \frac{2t}{1+t^2}$。[积分因子](@entry_id:177812)为：
$$ \mu(t) = \exp\left(\int \frac{2t}{1+t^2} dt\right) = \exp(\ln(1+t^2)) = 1+t^2 $$
将原方程（[标准形式](@entry_id:153058)）两边乘以 $\mu(t) = 1+t^2$，我们得到：
$$ (1+t^2)\frac{dy}{dt} + 2ty = t^2 $$
注意到左边正好是 $\frac{d}{dt}((1+t^2)y)$。因此，方程化为：
$$ \frac{d}{dt}((1+t^2)y) = t^2 $$
对两边积分，$\int \frac{d}{dt}((1+t^2)y) dt = \int t^2 dt$，得到 $(1+t^2)y = \frac{t^3}{3} + C$。通过初始条件（例如 $y(0)=0$）可以确定常数 $C$，从而得到特解。

#### 恰当方程

一个形如 $M(x, y)dx + N(x, y)dy = 0$ 的[微分方程](@entry_id:264184)，如果存在一个二元函数 $\Phi(x, y)$，使得它的[全微分](@entry_id:171747) $d\Phi = \frac{\partial \Phi}{\partial x}dx + \frac{\partial \Phi}{\partial y}dy$ 恰好等于方程的左边，即 $\frac{\partial \Phi}{\partial x} = M(x, y)$ 且 $\frac{\partial \Phi}{\partial y} = N(x, y)$，那么该方程就被称为**恰当方程（exact equation）**。此时，原方程等价于 $d\Phi = 0$，其通解就是 $\Phi(x, y) = C$。

判断一个方程是否为恰当方程的充要条件（在区域良性时）是：
$$ \frac{\partial M}{\partial y} = \frac{\partial N}{\partial x} $$
如果该条件满足，我们可以通过积分来重建[势函数](@entry_id:176105) $\Phi(x, y)$。首先对 $M(x, y)$ 关于 $x$ 积分：
$$ \Phi(x, y) = \int M(x, y) dx + g(y) $$
其中 $g(y)$ 是一个只依赖于 $y$ 的“积分常数”。然后，对这个表达式求关于 $y$ 的偏导，并令其等于 $N(x, y)$，以此来确定 $g(y)$。

考虑一个[保守力场](@entry_id:164320)中的等势线问题 [@problem_id:2130043]，其[微分方程](@entry_id:264184)为：
$$ (y \cos(xy) + 2x) dx + (x \cos(xy) - 2y) dy = 0 $$
这里，$M(x, y) = y \cos(xy) + 2x$，$N(x, y) = x \cos(xy) - 2y$。我们检验其恰当性：
$$ \frac{\partial M}{\partial y} = \cos(xy) - xy\sin(xy) $$
$$ \frac{\partial N}{\partial x} = \cos(xy) - xy\sin(xy) $$
由于 $\frac{\partial M}{\partial y} = \frac{\partial N}{\partial x}$，方程是恰当的。我们来寻找[势函数](@entry_id:176105) $\Phi(x, y)$：
$$ \Phi(x, y) = \int (y \cos(xy) + 2x) dx = \sin(xy) + x^2 + g(y) $$
接着，求其关于 $y$ 的偏导并令其等于 $N$：
$$ \frac{\partial \Phi}{\partial y} = x \cos(xy) + g'(y) = N(x, y) = x \cos(xy) - 2y $$
比较可知 $g'(y) = -2y$，积分得到 $g(y) = -y^2$（积分常数可并入最终解的常数 $C$）。因此，[势函数](@entry_id:176105)为 $\Phi(x, y) = \sin(xy) + x^2 - y^2$，该方程的通解为 $\sin(xy) + x^2 - y^2 = C$。

#### 通过[积分因子](@entry_id:177812)化为恰当方程

如果一个方程 $Mdx + Ndy = 0$ 本身不是恰当的，即 $\frac{\partial M}{\partial y} \neq \frac{\partial N}{\partial x}$，有时我们可以通过乘以一个[积分因子](@entry_id:177812) $\mu(x, y)$ 将其转化为恰当方程 $\mu M dx + \mu N dy = 0$。寻找[积分因子](@entry_id:177812)通常很困难，但在某些特殊情况下，我们可以假设[积分因子](@entry_id:177812)只依赖于单个变量。

例如，如果我们假设存在一个只依赖于 $x$ 的[积分因子](@entry_id:177812) $\mu(x)$，那么转化后的方程的恰当性条件为 $\frac{\partial (\mu M)}{\partial y} = \frac{\partial (\mu N)}{\partial x}$。展开得到 $\mu \frac{\partial M}{\partial y} = \frac{d\mu}{dx}N + \mu \frac{\partial N}{\partial x}$。整理后可得：
$$ \frac{1}{\mu}\frac{d\mu}{dx} = \frac{\frac{\partial M}{\partial y} - \frac{\partial N}{\partial x}}{N} $$
如果上式右边恰好是一个只依赖于 $x$ 的函数，那么我们的假设就成立，并且可以通[过积分](@entry_id:753033)求出 $\mu(x)$。

考虑方程 $(x^2+y^2+x)dx + xy dy = 0$ [@problem_id:2130069]。这里 $M = x^2+y^2+x$，$N = xy$。$\frac{\partial M}{\partial y} = 2y$，$\frac{\partial N}{\partial x} = y$，方程不恰当。我们尝试寻找一个[积分因子](@entry_id:177812) $\mu(x)$：
$$ \frac{\frac{\partial M}{\partial y} - \frac{\partial N}{\partial x}}{N} = \frac{2y - y}{xy} = \frac{y}{xy} = \frac{1}{x} $$
由于结果只依赖于 $x$，我们的假设是正确的。于是我们解方程 $\frac{1}{\mu}\frac{d\mu}{dx} = \frac{1}{x}$，得到 $\ln|\mu| = \ln|x| + C_0$。取最简单的非零解，$\mu(x) = x$。将原方程乘以 $x$，得到新的恰当方程 $(x^3+xy^2+x^2)dx + x^2y dy = 0$，然后就可以用恰当方程的方法求解。

### 变换方法与特殊[非线性方程](@entry_id:145852)

许多非线性方程无法直接求解，但可以通过巧妙的变量代换将其转化为我们已经掌握的[标准形式](@entry_id:153058)，如可分离变量方程或线性方程。

#### 变量代换法

变量代换是一种普适的思想。如果方程 $\frac{dy}{dx} = f(x, y)$ 中的 $f(x, y)$ 具有某种特殊结构，例如可以表示为 $g(ax+by)$ 的形式，那么代换 $z = ax+by$ 往往能简化问题。

考虑方程 $\frac{dy}{dx} = (x+y)^2 - 1$ [@problem_id:2130077]。这里的右侧是 $x+y$ 的函数。我们引入新变量 $z(x) = x+y(x)$。对其求导得到 $\frac{dz}{dx} = 1 + \frac{dy}{dx}$。从原方程解出 $\frac{dy}{dx} = z^2 - 1$，代入得：
$$ \frac{dz}{dx} = 1 + (z^2 - 1) = z^2 $$
这是一个关于 $z$ 的可分离变量方程。分离变量并积分 $\int z^{-2} dz = \int dx$，得到 $-\frac{1}{z} = x + C$。解出 $z = -\frac{1}{x+C}$。最后，将 $z = x+y$ 代回，得到原方程的通解 $y(x) = -\frac{1}{x+C} - x$。

#### [伯努利方程](@entry_id:204262)

**[伯努利方程](@entry_id:204262)（Bernoulli equation）**是形如 $\frac{dy}{dx} + P(x)y = Q(x)y^n$ 的一类非线性方程，其中 $n$ 是任意实数（$n \neq 0, 1$）。

通过代换 $u(x) = y(x)^{1-n}$，可以将[伯努利方程](@entry_id:204262)转化为一个关于 $u(x)$ 的一阶[线性方程](@entry_id:151487)。对 $u$ 求导：
$$ \frac{du}{dx} = (1-n)y^{-n}\frac{dy}{dx} $$
将原方程两边同乘以 $(1-n)y^{-n}$，然后进行代换，即可得到一个标准[线性方程](@entry_id:151487)，再用[积分因子法](@entry_id:167338)求解。

在等离子体物理的一个模型中，能量密度 $y(x)$ 演化遵循方程 $\frac{dy}{dx} - \frac{3}{2x}y = 2x y^{-1/2}$ [@problem_id:2130049]。这是一个[伯努利方程](@entry_id:204262)，其中 $n = -1/2$。我们使用代换 $u = y^{1 - (-1/2)} = y^{3/2}$。
求导得 $\frac{du}{dx} = \frac{3}{2}y^{1/2}\frac{dy}{dx}$。为了在原方程中引入这一项，我们将原方程两边同乘以 $\frac{3}{2}y^{1/2}$：
$$ \frac{3}{2}y^{1/2}\frac{dy}{dx} - \frac{9}{4x}y^{3/2} = 3x $$
用 $u$ 和 $\frac{du}{dx}$ 代换，得到一个关于 $u$ 的[线性方程](@entry_id:151487)：
$$ \frac{du}{dx} - \frac{9}{4x}u = 3x $$
这个线性方程可以通过[积分因子法](@entry_id:167338)求解，得到 $u(x)$ 的表达式，最后通过 $y = u^{2/3}$ 还原即可得到原方程的解。

### 特殊方程与几何包络

最后，我们介绍一类具有优美几何解释的特殊方程——[克莱罗方程](@entry_id:167993)，它联系了[微分方程](@entry_id:264184)的解与几何曲线的包络。

**[克莱罗方程](@entry_id:167993)（Clairaut's equation）**具有标准形式：
$$ y = x \frac{dy}{dx} + f\left(\frac{dy}{dx}\right) $$
令 $p = \frac{dy}{dx}$，方程变为 $y = xp + f(p)$。将此式对 $x$ 求导：
$$ \frac{dy}{dx} = p = \left(p + x \frac{dp}{dx}\right) + f'(p)\frac{dp}{dx} $$
整理后得到：
$$ \left(x + f'(p)\right)\frac{dp}{dx} = 0 $$
这个方程的解来自两种可能：

1.  **通解**：$\frac{dp}{dx} = 0$，这意味着 $p = C$（一个常数）。将 $p=C$ 代回原方程 $y = xp + f(p)$，我们得到一个直线族：
    $$ y = Cx + f(C) $$
    这就是[克莱罗方程](@entry_id:167993)的通解。

2.  **[奇异解](@entry_id:172996)**：$x + f'(p) = 0$。这个方程以及原方程 $y = xp + f(p)$ 共同构成了[参数方程](@entry_id:172360)组（以 $p$ 为参数），它定义了一条曲线。这条曲线是通解所代表的直线族的**包络（envelope）**，并且它本身也是原[微分方程](@entry_id:264184)的一个解，称为**[奇异解](@entry_id:172996)（singular solution）**。

在[几何光学](@entry_id:175509)中，一个特定系统的光线族满足其 $y$ 轴截距是其斜率的倒数 [@problem_id:2130061]。设一条光线的斜率为 $p = \frac{dy}{dx}$，其方程为 $y=px+b$。根据条件，$b = 1/p$。因此，这个光线族满足[微分方程](@entry_id:264184)：
$$ y = x p + \frac{1}{p} $$
这是一个[克莱罗方程](@entry_id:167993)，其中 $f(p) = 1/p$。
*   其**通解**是一个直线族，通过令 $p=C$ 得到：
    $$ y = Cx + \frac{1}{C} $$
*   其**[奇异解](@entry_id:172996)**（包络）由以下[参数方程](@entry_id:172360)组给出：
    $$ y = xp + \frac{1}{p} \quad \text{和} \quad x + f'(p) = x - \frac{1}{p^2} = 0 $$
    从第二个方程解出 $x = \frac{1}{p^2}$。代入第一个方程得到 $y = (\frac{1}{p^2})p + \frac{1}{p} = \frac{2}{p}$。我们现在需要消去参数 $p$。从 $y = 2/p$ 得到 $p = 2/y$。代入 $x = 1/p^2$ 得到 $x = \frac{1}{(2/y)^2} = \frac{y^2}{4}$。
    因此，[奇异解](@entry_id:172996)是抛物线 $y^2 = 4x$。这条抛物线在光学中被称为**焦散线（caustic curve）**，它是该直线族中每一条直线的[切线](@entry_id:268870)。

对[一阶常微分方程](@entry_id:264241)的这些原理和机制的掌握，是理解和求解描述各类物理系统和数学模型的[偏微分方程](@entry_id:141332)所不可或缺的基础。