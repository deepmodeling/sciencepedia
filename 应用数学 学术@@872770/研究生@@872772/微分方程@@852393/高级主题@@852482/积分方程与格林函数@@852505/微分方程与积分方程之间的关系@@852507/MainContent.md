## 引言
[微分方程](@entry_id:264184)与积分方程是[数学物理](@entry_id:265403)中描述自然现象的两种基本语言。[微分方程](@entry_id:264184)以其强大的局部描述能力，精确刻画了系统在任意时刻和位置的瞬时变化规律；而积分方程则通过对系统在整个时空域内的行为进行累积，提供了全局性的视角。尽管它们形式不同，但在许多情况下，两者描述的是同一个物理现实，构成了一个问题的等价表述。

然而，在面对具体问题时，选择哪一种表述并非无足轻重。直接求解一个复杂的[微分方程](@entry_id:264184)可能极为困难，尤其是在处理奇异[源项](@entry_id:269111)、复杂边界条件或需要证明解的存在性时。这便引出了一个核心问题：我们能否利用这两种表述的等价性，将一个困难的[微分方程](@entry_id:264184)问题转化为一个更易于分析或求解的积分方程问题？

本文旨在系统地回答这一问题，为读者揭示[微分方程](@entry_id:264184)与[积分方程](@entry_id:138643)之间深刻而实用的联系。
*   在**第一章：原理与机制**中，我们将深入探讨转换的核心技术，学习如何将初值问题（IVP）与[Volterra积分方程](@entry_id:146652)联系起来，以及如何利用格林函数将边值问题（BVP）重构为[Fredholm积分方程](@entry_id:277002)。
*   在**第二章：应用与跨学科联系**中，我们将视野拓宽到量子力学、[连续介质力学](@entry_id:155125)、[金融数学](@entry_id:143286)等多个领域，展示这一对偶性思想如何作为一种强大的策略，用以解决前沿科学与工程中的复杂问题。
*   最后，在**第三章：动手实践**中，您将有机会通过解决具体问题，亲手实践这些转换技巧，从而巩固理论知识，加深理解。

通过本次学习，您将掌握在两种数学语言之间灵活切换的能力，为分析和解决复杂系统模型打下坚实的基础。

## 原理与机制

[微分方程](@entry_id:264184)与积分方程是描述物理系统和数学现象的两种等价但视角不同的语言。[微分方程](@entry_id:264184)以其局部性，描述了系统在任意一点的[瞬时变化率](@entry_id:141382)；而积分方程则以其全局性，将系统在整个域上的行为整合起来。在前一章介绍其背景后，本章将深入探讨这两种表述之间的基本原理和转换机制。我们将看到，初值问题（IVP）与[Volterra积分方程](@entry_id:146652)密切相关，而边值问题（BVP）则与[Fredholm积分方程](@entry_id:277002)相对应。理解这些转换不仅能加深我们对解的结构的认识，还能为理论分析和数值计算提供强大的工具。

### [初值问题](@entry_id:144620)与[Volterra积分方程](@entry_id:146652)

[初值问题](@entry_id:144620)指定了在一个初始点上的状态（例如，位置和速度），并由一个[微分方程](@entry_id:264184)决定其后续的演化。这种固有的“因果”结构——当前状态仅依赖于过去的状态——自然地导向一种特定类型的[积分方程](@entry_id:138643)。

#### 从[微分方程](@entry_id:264184)到积分方程

考虑一个一般的 $n$ 阶[线性常微分方程](@entry_id:276013)[初值问题](@entry_id:144620)。其核心思想是通过反[复积分](@entry_id:202758)将微分算子转化为积分算子。每积分一次，就会引入一个由初始条件确定的常数。

让我们通过一个具体的例子来阐明这个过程。考虑一个二阶线性非齐次[常微分方程](@entry_id:147024)，其系数随[自变量](@entry_id:267118) $x$ 变化[@problem_id:1134821]：
$$
\frac{d^2y}{dx^2} + (2\alpha x) \frac{dy}{dx} + (\beta^2 x^2) y = F_0 \cos(\omega x)
$$
[初始条件](@entry_id:152863)在 $x=0$ 处给出：
$$
y(0) = y_0, \quad \frac{dy}{dx}(0) = y_0'
$$
为了将其转化为[积分方程](@entry_id:138643)，我们首先定义一个新函数 $u(x)$ 代表最高阶导数：
$$
u(x) = \frac{d^2y}{dx^2}
$$
现在，我们对 $u(x)$ 从初始点 $0$ 到任意点 $x$ 进行积分，并利用初始条件 $y'(0) = y_0'$：
$$
\int_0^x u(t) dt = \int_0^x \frac{d^2y}{dt^2} dt = \frac{dy}{dx}(x) - \frac{dy}{dx}(0)
$$
由此解出 $\frac{dy}{dx}(x)$：
$$
\frac{dy}{dx}(x) = y_0' + \int_0^x u(t) dt
$$
再次对上式积分，并利用[初始条件](@entry_id:152863) $y(0) = y_0$：
$$
\int_0^x \frac{dy}{dt}(t) dt = y(x) - y(0) = \int_0^x \left( y_0' + \int_0^t u(s) ds \right) dt
$$
$$
y(x) = y_0 + y_0'x + \int_0^x \left( \int_0^t u(s) ds \right) dt
$$
通过使用柯西重[复积分](@entry_id:202758)公式 $\int_a^x \int_a^t f(s) ds dt = \int_a^x (x-s) f(s) ds$，我们可以将[二重积分](@entry_id:198869)简化为单重积分：
$$
y(x) = y_0 + y_0'x + \int_0^x (x-t) u(t) dt
$$
现在我们有了 $y(x)$ 和 $\frac{dy}{dx}(x)$ 的积分表达式。将它们代回原始的[微分方程](@entry_id:264184)：
$$
u(x) + (2\alpha x) \left( y_0' + \int_0^x u(t) dt \right) + (\beta^2 x^2) \left( y_0 + y_0'x + \int_0^x (x-t) u(t) dt \right) = F_0 \cos(\omega x)
$$
将方程整理成 $u(x)$ 的标准[积分方程](@entry_id:138643)形式 $u(x) = f(x) + \int_0^x K(x, t) u(t) dt$：
$$
u(x) = F_0 \cos(\omega x) - (2\alpha x) y_0' - (\beta^2 x^2)(y_0 + y_0'x) - \int_0^x \left[ 2\alpha x + \beta^2 x^2 (x-t) \right] u(t) dt
$$
这是一个 **[Volterra积分方程](@entry_id:146652)**。它的积分上限是变量 $x$，这正反映了[初值问题](@entry_id:144620)的因果特性：在 $x$ 点的解依赖于区间 $[0, x]$ 上的历史。此处的已知函数 $f(x)$ 和积分核 $K(x, t)$ 分别为：
$$
f(x) = F_0 \cos(\omega x) - 2\alpha x y_0' - \beta^2 x^2 y_0 - \beta^2 x^3 y_0'
$$
$$
K(x, t) = -2\alpha x - \beta^2 x^2(x-t)
$$
这个过程是完全通用的，可以应用于任何线性[初值问题](@entry_id:144620)。

#### 从[积分方程](@entry_id:138643)到[微分方程](@entry_id:264184)

反向转换，即从[Volterra积分方程](@entry_id:146652)恢复到[微分方程](@entry_id:264184)，通常通过应用 **[莱布尼茨积分法则](@entry_id:145735)** 来实现：
$$
\frac{d}{dx} \int_{a(x)}^{b(x)} g(x,t) dt = g(x, b(x)) \frac{db}{dx} - g(x, a(x)) \frac{da}{dx} + \int_{a(x)}^{b(x)} \frac{\partial g}{\partial x}(x,t) dt
$$
当处理形如 $y(x) = f(x) + \int_0^x K(x, t) y(t) dt$ 的[Volterra方程](@entry_id:270442)时，由于积分下限是常数，上限是 $x$，该法则简化为：
$$
\frac{dy}{dx} = f'(x) + K(x,x)y(x) + \int_0^x \frac{\partial K(x,t)}{\partial x} y(t) dt
$$
如果核 $K(x,t)$ 的结构足够简单（例如，它是 $x$ 和 $t$ 的多项式，或者是所谓的“差分核” $K(x-t)$），重[复微分](@entry_id:170277)最终可以消除积分项，从而得到一个常微分方程。

例如，考虑一个由以下[Volterra积分方程](@entry_id:146652)定义的函数 $y(x)$[@problem_id:1135020]：
$$
y(x) = (\alpha x + \beta e^{\gamma x}) + \int_0^x (c_1 + c_2(x-t)) y(t) dt
$$
对 $x$ [微分](@entry_id:158718)一次，应用[莱布尼茨法则](@entry_id:157949)。这里的核 $K(x,t) = c_1 + c_2(x-t)$，因此 $K(x,x) = c_1$ 并且 $\frac{\partial K}{\partial x} = c_2$。
$$
y'(x) = (\alpha + \beta\gamma e^{\gamma x}) + K(x,x)y(x) + \int_0^x \frac{\partial K}{\partial x} y(t) dt
$$
$$
y'(x) = (\alpha + \beta\gamma e^{\gamma x}) + c_1 y(x) + c_2 \int_0^x y(t) dt
$$
积分项依然存在。我们再次对 $x$ [微分](@entry_id:158718)：
$$
y''(x) = (\beta\gamma^2 e^{\gamma x}) + c_1 y'(x) + c_2 \frac{d}{dx}\int_0^x y(t) dt
$$
根据[微积分基本定理](@entry_id:201377)，$\frac{d}{dx}\int_0^x y(t) dt = y(x)$。因此，我们得到一个[二阶线性常微分方程](@entry_id:189146)：
$$
y''(x) = c_1 y'(x) + c_2 y(x) + \beta\gamma^2 e^{\gamma x}
$$
[初始条件](@entry_id:152863)可以通过在 $x=0$ 处计算 $y(x)$ 和 $y'(x)$ 的表达式来找到。从原始积分方程，当 $x=0$ 时积分消失，得到 $y(0) = f(0) = \beta$。从 $y'(x)$ 的表达式，当 $x=0$ 时积分也消失，得到 $y'(0) = f'(0) + c_1 y(0) = (\alpha + \beta\gamma) + c_1 \beta$。这样，我们就完整地将一个[积分方程](@entry_id:138643)问题转化为了一个等价的初值问题[@problem_id:1134951]。

这个转换对于某些特殊形式的[Fredholm积分方程](@entry_id:277002)也有效。如果一个[Fredholm方程](@entry_id:266485)的核包含一个[Heaviside阶跃函数](@entry_id:275119) $\Theta(x-t)$，它实际上被限制在一个变化的积分域上[@problem_id:1134794]。例如，核 $K(x,t) = \lambda \sin(\alpha(x-t)) \Theta(x-t)$ 使得积分 $\int_0^{\infty} K(x, t) y(t) dt$ 实际上等于 $\int_0^x \lambda \sin(\alpha(x-t)) y(t) dt$，这正是一个Volterra[形式的积分](@entry_id:158607)。

#### 系统与迭代解

将单个ODE转换为[Volterra方程](@entry_id:270442)的思想可以直接推广到一阶ODE系统。考虑一个系统[@problem_id:1134854]：
$$
\begin{cases}
\frac{dy_1}{dt} = g_1(t, y_1, y_2) \\
\frac{dy_2}{dt} = g_2(t, y_1, y_2)
\end{cases}
$$
带有[初始条件](@entry_id:152863) $y_1(0) = y_{1,0}$ 和 $y_2(0) = y_{2,0}$。对每个方程从 $0$ 到 $t$ 积分，我们得到一个耦合的[Volterra积分方程](@entry_id:146652)组：
$$
y_1(t) = y_{1,0} + \int_0^t g_1(s, y_1(s), y_2(s)) ds
$$
$$
y_2(t) = y_{2,0} + \int_0^t g_2(s, y_1(s), y_2(s)) ds
$$
这种积分形式是证明解的存在性和唯一性的[Picard-Lindelöf定理](@entry_id:136826)的基础，并且它直接引出了一个构造解的迭代方法，即 **[Picard迭代法](@entry_id:159269)**。从初始猜测（通常是初始条件本身）开始：
$$
y_1^{(0)}(t) = y_{1,0}, \quad y_2^{(0)}(t) = y_{2,0}
$$
然后通过将前一次的迭代结果代入积分的右侧来生成下一次的近似解：
$$
y_i^{(n+1)}(t) = y_{i,0} + \int_0^t g_i(s, y_1^{(n)}(s), y_2^{(n)}(s)) ds
$$
例如，对于系统 $\frac{dy_1}{dt} = \alpha t y_1 + \beta y_2$ 和 $\frac{dy_2}{dt} = \gamma y_1 + \delta t^2 y_2$，其第一次迭代 $y_1^{(1)}(t)$ 的计算如下[@problem_id:1134854]：
$$
y_1^{(1)}(t) = y_{1,0} + \int_0^t (\alpha s y_1^{(0)}(s) + \beta y_2^{(0)}(s)) ds = y_{1,0} + \int_0^t (\alpha s y_{1,0} + \beta y_{2,0}) ds
$$
$$
y_1^{(1)}(t) = y_{1,0} + \frac{\alpha y_{1,0}}{2}t^2 + \beta y_{2,0}t
$$
在适当的条件下，这个迭代序列会收敛到真实的解。

### [边值问题](@entry_id:193901)与[Fredholm积分方程](@entry_id:277002)

与初值问题不同，[边值问题](@entry_id:193901)在区域的多个点（边界）上施加约束。这破坏了简单的[因果结构](@entry_id:159914)，因为域内任一点的解都可能受到所有边界的影响。这种“全局”相互依赖性由[Fredholm积分方程](@entry_id:277002)来描述，其积分区间是固定的。这种转换的关键工具是 **格林函数（Green's function）**。

#### [格林函数](@entry_id:147802)的作用

对于一个[线性微分算子](@entry_id:174781) $L$ 和一个边值问题 $L[y](x) = f(x)$（带有[齐次边界条件](@entry_id:750371)），其解可以表示为一个[积分变换](@entry_id:186209)：
$$
y(x) = \int_a^b G(x, \xi) f(\xi) d\xi
$$
这里的核 $G(x, \xi)$ 就是该算子和边界条件对应的格林函数。从物理上看，格林函数 $G(x, \xi)$ 代表了系统在点 $x$ 处的响应，这个响应是由位于点 $\xi$ 的一个单位点源（由狄拉克 $\delta$ 函数 $\delta(x-\xi)$ 描述）引起的。因此，[格林函数](@entry_id:147802)被定义为以下问题的解：
$$
L[G(x, \xi)] = \delta(x-\xi)
$$
同时 $G(x, \xi)$ 作为 $x$ 的函数，必须满足与 $y(x)$ 相同的[齐次边界条件](@entry_id:750371)。

#### 构造[格林函数](@entry_id:147802)

让我们为二阶算子 $L = \frac{d^2}{dx^2} + k^2$ 在区间 $[0, L]$ 上，带有周期性边界条件 $y(0)=y(L), y'(0)=y'(L)$ 的情况构造格林函数[@problem_id:1134738]。我们需要求解：
$$
\frac{d^2G}{dx^2} + k^2 G = \delta(x-\xi)
$$
1.  **[求解齐次方程](@entry_id:184715)**: 在 $x \neq \xi$ 的区域，方程为 $G'' + k^2 G = 0$。通解为 $A\cos(kx) + B\sin(kx)$。因此，我们可以为 $x  \xi$ 和 $x > \xi$ 分别写出解：
    $$
    G(x, \xi) = \begin{cases} G_1(x) = a\cos(kx) + b\sin(kx),  x  \xi \\ G_2(x) = c\cos(kx) + d\sin(kx),  x > \xi \end{cases}
    $$
2.  **施加连接条件**: 在 $x=\xi$ 处，[格林函数](@entry_id:147802)必须是连续的，但其[一阶导数](@entry_id:749425)有一个大小为 $1$ 的跳跃（对于算子 $y''$）。
    $$
    G_1(\xi) = G_2(\xi) \quad (\text{连续性})
    $$
    $$
    G_2'(\xi) - G_1'(\xi) = 1 \quad (\text{导数跳跃})
    $$
3.  **施加边界条件**: [格林函数](@entry_id:147802)本身必须满足周期性边界条件：
    $$
    G_1(0) = G_2(L) \implies a = c\cos(kL) + d\sin(kL)
    $$
    $$
    G_1'(0) = G_2'(L) \implies bk = -ck\sin(kL) + dk\cos(kL)
    $$
4.  **求解系数**: 通过求解由这四个条件组成的代数方程组，可以确定系数 $a, b, c, d$（它们将是 $\xi$ 的函数）。经过一番代数运算，可以得到一个紧凑的表达式。例如，对于这个问题，在 $kL \neq 2n\pi$（确保解存在且唯一）的条件下，格林函数为：
    $$
    G(x, \xi) = \frac{1}{2k\sin(\frac{kL}{2})} \cos\left(k\left(\frac{L}{2} - |x-\xi|\right)\right)
    $$
一旦得到[格林函数](@entry_id:147802)，任何边值问题 $y''+k^2y=f(x)$ 的解就可直接写为 $y(x) = \int_0^L G(x,\xi) f(\xi) d\xi$。

#### 从积分形式恢复[边值问题](@entry_id:193901)

反过来，给定一个作为[Fredholm积分方程](@entry_id:277002)核的[格林函数](@entry_id:147802)，我们也可以恢复出其对应的[微分算子](@entry_id:140145)和边界条件[@problem_id:1134874]。
1.  **确定边界条件**: [格林函数](@entry_id:147802) $G(x, \xi)$ 作为 $x$ 的函数，必须在边界上满足[齐次边界条件](@entry_id:750371)。因此，只需检查 $G(x, \xi)$ 在边界点的值。例如，如果对于所有的 $\xi \in [1, R]$ 都有 $G(1, \xi) = 0$ 和 $G(R, \xi) = 0$，那么对应的边界条件就是 $y(1)=0$ 和 $y(R)=0$。
2.  **确定[微分算子](@entry_id:140145)**: 在 $x \neq \xi$ 的区域，格林函数是[齐次微分方程](@entry_id:166017) $L[y]=0$ 的解。通常[格林函数](@entry_id:147802)可以表示为 $C(\xi) u_1(x)$ (for $x  \xi$) 和 $D(\xi) u_2(x)$ (for $x > \xi$) 的形式，其中 $u_1(x)$ 和 $u_2(x)$ 是[齐次方程](@entry_id:163650)的两个[线性无关解](@entry_id:185441)。我们可以将猜测的算子 $L$ 应用于 $u_1(x)$ 或 $u_2(x)$，并要求结果为零，从而确定算子中的未知系数。

#### 验证解

我们可以通过直接计算来验证积分解确实满足原始的[微分方程](@entry_id:264184)。考虑[泊松方程](@entry_id:143763) $y''(x) = f(x)$，带有[混合边界条件](@entry_id:176456) $y(0)=0, y'(L)=0$。其解由 $y(x) = \int_0^L G(x, x') f(x') dx'$ 给出，其中[格林函数](@entry_id:147802)为 $G(x, x') = -\min(x, x')$[@problem_id:1134984]。

让我们代入一个[源项](@entry_id:269111) $f(x) = \alpha x$ 并验证。首先，写出积分表达式：
$$
y(x) = \int_0^L (-\min(x, x')) (\alpha x') dx' = -\alpha \left[ \int_0^x x' \cdot x' dx' + \int_x^L x \cdot x' dx' \right]
$$
计算积分：
$$
y(x) = -\alpha \left[ \frac{x^3}{3} + x \left( \frac{L^2-x^2}{2} \right) \right] = \alpha \left( \frac{x^3}{6} - \frac{xL^2}{2} \right)
$$
现在对这个显式解求导两次：
$$
y'(x) = \alpha \left( \frac{3x^2}{6} - \frac{L^2}{2} \right) = \alpha \left( \frac{x^2}{2} - \frac{L^2}{2} \right)
$$
$$
y''(x) = \alpha x
$$
结果恰好是原始的源项 $f(x)$。同时，我们可以检查边界条件：$y(0) = 0$ 和 $y'(L) = \alpha(\frac{L^2}{2} - \frac{L^2}{2}) = 0$，确认此解是正确的。

### [特征值问题](@entry_id:142153)与Fredholm替代定理

[积分方程](@entry_id:138643)的框架在处理特征值问题和研究解的存在性条件时尤其强大。

#### [齐次方程](@entry_id:163650)与[特征值](@entry_id:154894)

一个[Sturm-Liouville特征值](@entry_id:175904)问题，如 $L[y] = -\lambda w(x) y$ 加上[齐次边界条件](@entry_id:750371)，可以被转化为一个齐次[Fredholm积分方程](@entry_id:277002)：
$$
y(x) = \lambda \int_a^b G(x, \xi) w(\xi) y(\xi) d\xi
$$
其中 $G(x, \xi)$ 是与算子 $L$ 和相应边界条件关联的[格林函数](@entry_id:147802)。[微分算子](@entry_id:140145)的[特征值](@entry_id:154894) $\lambda_n$ 与积分算子的[特征值](@entry_id:154894) $\mu_n$ 互为倒数关系。

考虑一个固定-自由杆的[振动](@entry_id:267781)问题，其数学模型是一个[Sturm-Liouville问题](@entry_id:173382)[@problem_id:1134814]：
$$
y''(x) + \lambda y = 0, \quad y(0)=0, \quad y'(L)=0
$$
这个边值问题等价于齐次[Fredholm积分方程](@entry_id:277002) $y(x) = \lambda \int_0^L \min(x, \xi) y(\xi) d\xi$。我们可以从这个[积分方程](@entry_id:138643)出发，通过两[次微分](@entry_id:175641)（如前所述）恢复出[微分方程](@entry_id:264184)和边界条件。然后，求解这个我们熟悉的[微分方程](@entry_id:264184)[特征值问题](@entry_id:142153)：
通解为 $y(x) = A\sin(\sqrt{\lambda}x) + B\cos(\sqrt{\lambda}x)$。
$y(0)=0 \implies B=0$。
$y'(L)=0 \implies A\sqrt{\lambda}\cos(\sqrt{\lambda}L)=0$。
为得到非平凡解，$A \neq 0$，因此 $\cos(\sqrt{\lambda}L)=0$。这要求 $\sqrt{\lambda}L = \frac{(2n+1)\pi}{2}$ for $n=0, 1, 2, \dots$。
最小的正[特征值](@entry_id:154894)（基频）对应于 $n=0$：
$$
\lambda_1 = \left( \frac{\pi}{2L} \right)^2 = \frac{\pi^2}{4L^2}
$$

#### 解的存在性：Fredholm替代定理

对于非[齐次方程](@entry_id:163650) $L[y]=f$，其解是否存在？**Fredholm替代定理** 给出了一个深刻的答案。该定理指出：
 对于方程 $L[y]=f$，解存在的充要条件是，源项 $f$ 与相应齐次伴随问题 $L^\dagger[z]=0$ 的所有解（即 $L^\dagger$ 的[零空间](@entry_id:171336)）正交。

这里的正交性是针对标准的 $L^2$ [内积](@entry_id:158127)定义的，即 $\langle f, z \rangle = \int_a^b f(x) \overline{z(x)} dx = 0$。如果算子是自伴随的（$L^\dagger = L$），那么 $f$ 必须与齐次问题 $L[z]=0$ 的所有解正交。

这个定理在物理上对应于共振现象。如果驱动力 $f$ 的某个分量与系统的某个固有模式（齐次解）“同频”，那么系统将产生无限的响应，导致没有[稳态解](@entry_id:200351)，除非该驱动分量为零。

考虑一个周期边值问题[@problem_id:1134873]：
$$
y''(x) + 9y(x) = f(x), \quad x \in [0, 2\pi]
$$
其中 $y(0)=y(2\pi), y'(0)=y'(2\pi)$。这里的算子 $L = d^2/dx^2 + 9$ 是自伴随的。相应的齐次问题 $z''+9z=0$ 的周期解（零空间）由 $z_1(x) = \cos(3x)$ 和 $z_2(x) = \sin(3x)$ 张成。

现在，假设驱动项为 $f(x) = \cos(3x) + \alpha \cos(2x)\cos(x)$。为了使解存在， $f(x)$ 必须与 $\cos(3x)$ 和 $\sin(3x)$ 都正交。
利用[三角恒等式](@entry_id:165065) $\cos(2x)\cos(x) = \frac{1}{2}(\cos(3x) + \cos(x))$，我们可以重写 $f(x)$：
$$
f(x) = \left(1 + \frac{\alpha}{2}\right)\cos(3x) + \frac{\alpha}{2}\cos(x)
$$
现在我们施加正交条件。由于 $f(x)$ 是偶函数，它自动与[奇函数](@entry_id:173259) $\sin(3x)$ 在 $[0, 2\pi]$ 上正交。我们只需考虑与 $\cos(3x)$ 的正交性：
$$
\int_0^{2\pi} f(x) \cos(3x) dx = 0
$$
$$
\int_0^{2\pi} \left[ \left(1 + \frac{\alpha}{2}\right)\cos^2(3x) + \frac{\alpha}{2}\cos(x)\cos(3x) \right] dx = 0
$$
利用积分 $\int_0^{2\pi} \cos^2(3x) dx = \pi$ 和 $\int_0^{2\pi} \cos(x)\cos(3x) dx = 0$，我们得到：
$$
\left(1 + \frac{\alpha}{2}\right)\pi + 0 = 0 \implies 1 + \frac{\alpha}{2} = 0 \implies \alpha = -2
$$
因此，只有当 $\alpha = -2$ 时，[驱动项](@entry_id:165986)中与系统固有模式 $\cos(3x)$ 共振的部分被精确抵消，方程才有解。

本章系统地展示了[微分方程](@entry_id:264184)和[积分方程](@entry_id:138643)之间的深刻联系。从[Volterra方程](@entry_id:270442)对初值问题的因果描述，到[Fredholm方程](@entry_id:266485)和[格林函数](@entry_id:147802)对[边值问题](@entry_id:193901)的全局刻画，再到Fredholm替代定理对解存在性的精辟论断，这一系列转换和概念为我们分析和求解各类[微分方程](@entry_id:264184)提供了丰富而强大的理论框架。