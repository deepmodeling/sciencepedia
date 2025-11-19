## 引言
在物理学和工程学中，我们遇到的许多现象，从热量在材料中的[扩散](@entry_id:141445)到波在介质中的传播，都由[非齐次偏微分方程](@entry_id:173155)（PDE）描述。这些方程中的“非齐次项”（或称[源项](@entry_id:269111)）代表了外部驱动力、内部热源或物质的产生，是理解系统真实行为的关键。然而，直接求解这些方程往往极具挑战性。本文旨在系统性地介绍一种强大而优雅的求解工具——**[本征函数展开](@entry_id:177104)法**（Method of Eigenfunction Expansion），它为解决这类问题提供了一条清晰的路径。

该方法的核心思想在于利用与问题相关的[线性算子](@entry_id:149003)的“指纹”——即[本征函数](@entry_id:154705)，来构建解。它巧妙地将一个复杂的多变量[偏微分方程](@entry_id:141332)问题，转化为一系列我们更熟悉、更易于处理的单变量[常微分方程](@entry_id:147024)（ODE）。本文将填补从分离变量法求解齐次问题到处理复杂非齐次问题之间的知识鸿沟，向读者展示如何系统地应用这一技巧。

在接下来的章节中，你将学到：
-   在**第一章：原理与机制**中，我们将深入探讨该方法的核心数学原理，即如何利用[本征函数的正交性](@entry_id:150712)实现PDE到ODE的转化，并学习处理[非齐次边界条件](@entry_id:750645)、变系数算子等复杂情况的策略。
-   在**第二章：应用与交叉学科联系**中，我们将跨越学科界限，展示该方法在[振动](@entry_id:267781)、热传导、量子力学、结构力学等不同领域的广泛应用，揭示其作为一种普适性分析工具的深刻价值。
-   最后，在**第三章：动手实践**中，你将通过解决具体问题来巩固所学知识，将理论应用于实践。

让我们首先从该方法的基础——其核心原理与机制——开始我们的探索之旅。

## 原理与机制

本章旨在系统阐述求解[非齐次偏微分方程](@entry_id:173155)的**[本征函数展开](@entry_id:177104)法** (Method of Eigenfunction Expansion)。此方法的核心思想是利用与问题相关的[线性空间](@entry_id:151108)算子的本征函数，将一个复杂的[偏微分方程](@entry_id:141332)（PDE）转化为一组相对简单的常微分方程（ODE）。这种转化极大地简化了求解过程，尤其适用于具有[齐次边界条件](@entry_id:750371)的线性问题。我们将从基本原理出发，逐步探讨该方法的应用、推广及其在不同物理情境下的具体表现。

### 核心原理：叠加与正交性

考虑一个一般的线性[非齐次偏微分方程](@entry_id:173155)，其形式可写为：

$$
\frac{\partial u}{\partial t} = \mathcal{L}[u] + F(\boldsymbol{x}, t)
$$

或

$$
\frac{\partial^2 u}{\partial t^2} = \mathcal{L}[u] + F(\boldsymbol{x}, t)
$$

其中，$u(\boldsymbol{x}, t)$ 是待求函数（如温度或位移），$\boldsymbol{x}$ 代表空间坐标，$t$ 代表时间。$\mathcal{L}$ 是一个作用于空间变量的[线性微分算子](@entry_id:174781)（例如，[拉普拉斯算子](@entry_id:146319) $\nabla^2$），而 $F(\boldsymbol{x}, t)$ 是已知的**源项**或**强迫项**。该方程还需满足一组给定的边界条件和初始条件。

[本征函数展开](@entry_id:177104)法的第一步，也是最关键的一步，是考虑与空间算子 $\mathcal{L}$ 和相应的**[齐次边界条件](@entry_id:750371)**关联的**本征值问题**。该问题通常写为：

$$
\mathcal{L}[\phi_n(\boldsymbol{x})] = -\lambda_n \phi_n(\boldsymbol{x})
$$

其中，$\phi_n(\boldsymbol{x})$ 是算子 $\mathcal{L}$ 的**[本征函数](@entry_id:154705)**，$\lambda_n$ 是对应的**[本征值](@entry_id:154894)**。对于许多物理上有意义的算子（如 Sturm-Liouville 算子），其本征函数集 $\{\phi_n(\boldsymbol{x})\}$ 构成一个**完备**且**正交**的基。这意味着任何满足相同[齐次边界条件](@entry_id:750371)的函数都可以唯一地表示为这些本征函数的线性组合。

正交性通常由如下[内积](@entry_id:158127)关系定义（可能包含一个权函数 $w(\boldsymbol{x})$）：

$$
\int_{\Omega} \phi_n(\boldsymbol{x}) \phi_m(\boldsymbol{x}) w(\boldsymbol{x}) d\boldsymbol{x} = C_n \delta_{nm}
$$

其中 $\Omega$ 是问题的空间域，$C_n$ 是[归一化常数](@entry_id:752675)，$\delta_{nm}$ 是克罗内克 δ 函数。

[本征函数](@entry_id:154705)法的核心策略在于，将待求的解 $u(\boldsymbol{x}, t)$ 和已知的[源项](@entry_id:269111) $F(\boldsymbol{x}, t)$ 同时展开为此[本征函数](@entry_id:154705)基：

$$
u(\boldsymbol{x}, t) = \sum_{n=1}^{\infty} u_n(t) \phi_n(\boldsymbol{x})
$$

$$
F(\boldsymbol{x}, t) = \sum_{n=1}^{\infty} f_n(t) \phi_n(\boldsymbol{x})
$$

这里的系数 $u_n(t)$ 是未知的待求时间函数，而系数 $f_n(t)$ 可以通过利用[本征函数的正交性](@entry_id:150712)从已知的 $F(\boldsymbol{x}, t)$ 中计算出来，这个过程称为**分析**（analysis）：

$$
f_n(t) = \frac{\int_{\Omega} F(\boldsymbol{x}, t) \phi_n(\boldsymbol{x}) w(\boldsymbol{x}) d\boldsymbol{x}}{\int_{\Omega} \phi_n^2(\boldsymbol{x}) w(\boldsymbol{x}) d\boldsymbol{x}}
$$

将这些级数代入原始的 PDE，神奇的事情发生了：[偏微分方程](@entry_id:141332)被转化为一系列关于系数 $u_n(t)$ 的[常微分方程](@entry_id:147024)。

### 将[偏微分方程](@entry_id:141332)转化为[常微分方程](@entry_id:147024)

让我们通过一个具体的例子来演示这个转化过程。考虑一个一维反应[扩散](@entry_id:141445)系统 [@problem_id:2119334]，其控制方程为：

$$
\frac{\partial u}{\partial t} = \frac{\partial^2 u}{\partial x^2} - u + \sin(3x), \quad x \in (0, \pi)
$$

边界条件为 $u(0, t) = 0, u(\pi, t) = 0$，初始条件为 $u(x, 0) = \sin(x)$。

这里的空间算子是 $\mathcal{L} = \frac{d^2}{dx^2} - 1$。相关的[本征值问题](@entry_id:142153)是 $\phi''(x) - \phi(x) = -\lambda \phi(x)$，或者更习惯地，我们考虑与 $\frac{d^2}{dx^2}$ 相关的[本征值问题](@entry_id:142153) $\phi''(x) = -\mu \phi(x)$。对于狄利克雷（Dirichlet）边界条件 $\phi(0) = \phi(\pi) = 0$，我们熟知其本征函数为 $\phi_n(x) = \sin(nx)$，[本征值](@entry_id:154894)为 $\mu_n = n^2$（对于 $n=1, 2, \dots$）。

现在，我们将解 $u(x, t)$ 和[源项](@entry_id:269111) $F(x, t) = \sin(3x)$ 按此[基展开](@entry_id:746689)：

$$
u(x, t) = \sum_{n=1}^{\infty} T_n(t) \sin(nx)
$$

[源项](@entry_id:269111) $\sin(3x)$ 本身就是 $n=3$ 的[本征函数](@entry_id:154705)，所以其展开非常简单：$F(x, t) = f_3(t)\sin(3x)$，其中 $f_3(t)=1$，而对所有 $n \neq 3$，$f_n(t)=0$。

将级数代入 PDE：

$$
\sum_{n=1}^{\infty} T_n'(t) \sin(nx) = \sum_{n=1}^{\infty} T_n(t) (-n^2) \sin(nx) - \sum_{n=1}^{\infty} T_n(t) \sin(nx) + \sin(3x)
$$

整理后得到：

$$
\sum_{n=1}^{\infty} [T_n'(t) + (n^2+1) T_n(t)] \sin(nx) = \sin(3x)
$$

利用 $\sin(nx)$ 在 $[0, \pi]$ 上的正交性，我们可以对等式两边每一项的系数进行匹配。这为我们提供了两类常微分方程：

- 当 $n = 3$ 时：$T_3'(t) + (3^2+1) T_3(t) = 1 \implies T_3'(t) + 10 T_3(t) = 1$
- 当 $n \neq 3$ 时：$T_n'(t) + (n^2+1) T_n(t) = 0$

至此，一个[偏微分方程](@entry_id:141332)被成功地分解为无穷多个独立的[常微分方程](@entry_id:147024)。

为了求解这些 ODE，我们还需要[初始条件](@entry_id:152863)。将初始条件 $u(x, 0) = \sin(x)$ 进行展开：

$$
u(x, 0) = \sum_{n=1}^{\infty} T_n(0) \sin(nx) = \sin(x)
$$

通过比较系数，我们得到 $T_1(0) = 1$，且对于所有 $n \neq 1$，$T_n(0) = 0$。

现在我们可以求解这些带有[初始条件](@entry_id:152863)的 ODE：
- 对于 $n=1$：$T_1'(t) + 2T_1(t) = 0$，$T_1(0)=1$。解为 $T_1(t) = \exp(-2t)$。
- 对于 $n=3$：$T_3'(t) + 10T_3(t) = 1$，$T_3(0)=0$。这是一个一阶线性非齐次 ODE，其解为 $T_3(t) = \frac{1}{10}(1 - \exp(-10t))$。
- 对于所有其他 $n \neq 1, 3$：$T_n'(t) + (n^2+1)T_n(t) = 0$，$T_n(0)=0$。这唯一的解是 $T_n(t) = 0$。

最后，我们将求得的系数代回级数展开，重构出最终解：

$$
u(x, t) = T_1(t)\sin(x) + T_3(t)\sin(3x) = \exp(-2t) \sin(x) + \frac{1}{10}(1 - \exp(-10t)) \sin(3x)
$$

这个过程完整地展示了[本征函数展开](@entry_id:177104)法的威力：它将一个多变量问题（PDE）[解耦](@entry_id:637294)为一系列单变量问题（ODE），从而大大简化了求解。

### 处理复杂性与变体

在理想情况下，PDE 的算子、边界条件和[源项](@entry_id:269111)都非常“友好”。然而，在实际应用中，我们经常遇到各种复杂情况。本节将探讨如何调整和扩展[本征函数](@entry_id:154705)法以应对这些挑战。

#### [非齐次边界条件](@entry_id:750645)

[本征函数展开](@entry_id:177104)法的一个基本要求是边界条件必须是**齐次的**（例如 $u=0$ 或 $\partial u / \partial x = 0$）。当面临**[非齐次边界条件](@entry_id:750645)**时，例如在一个长度为 $\pi$ 的杆中，一端温度随时间变化 $u(0, t) = A_0 \cos(\omega t)$，另一端保持为零 $u(\pi, t) = 0$ [@problem_id:2119347]，我们不能直接应用该方法。

解决方法是引入一个辅助函数。我们将解 $u(x, t)$ 分解为两部分：

$$
u(x, t) = v(x, t) + w(x, t)
$$

其中，$v(x, t)$ 是一个我们构造的、相对简单的函数，其唯一目的是满足给定的[非齐次边界条件](@entry_id:750645)。而余下的函数 $w(x, t)$ 则将满足对应的[齐次边界条件](@entry_id:750371)，从而可以应用[本征函数展开](@entry_id:177104)法。

对于上述例子 [@problem_id:2119347]，我们可以选择一个在空间上是线性的函数 $v(x,t) = a(t)x + b(t)$。通过代入边界条件：
$v(0, t) = b(t) = A_0 \cos(\omega t)$
$v(\pi, t) = a(t)\pi + b(t) = 0 \implies a(t) = -\frac{1}{\pi} A_0 \cos(\omega t)$

因此，我们得到辅助函数：
$$
v(x, t) = A_0 \cos(\omega t) \left(1 - \frac{x}{\pi}\right)
$$
这个函数在 $x=0$ 和 $x=\pi$ 处精确地满足了原问题的[非齐次边界条件](@entry_id:750645)。

现在，我们考察 $w(x, t) = u(x, t) - v(x, t)$ 所满足的方程。它的边界条件是齐次的：
$w(0, t) = u(0, t) - v(0, t) = A_0 \cos(\omega t) - A_0 \cos(\omega t) = 0$
$w(\pi, t) = u(\pi, t) - v(\pi, t) = 0 - 0 = 0$

将 $u = v+w$ 代入原[热传导方程](@entry_id:194763) $\frac{\partial u}{\partial t} = \alpha^2 \frac{\partial^2 u}{\partial x^2}$，我们得到：

$$
\frac{\partial w}{\partial t} + \frac{\partial v}{\partial t} = \alpha^2 \left( \frac{\partial^2 w}{\partial x^2} + \frac{\partial^2 v}{\partial x^2} \right)
$$

整理后得到 $w(x, t)$ 满足的方程：

$$
\frac{\partial w}{\partial t} = \alpha^2 \frac{\partial^2 w}{\partial x^2} - \left( \frac{\partial v}{\partial t} - \alpha^2 \frac{\partial^2 v}{\partial x^2} \right)
$$

这个方程是一个带有新的[源项](@entry_id:269111) $Q(x, t) = - (\frac{\partial v}{\partial t} - \alpha^2 \frac{\partial^2 v}{\partial x^2})$ 和[齐次边界条件](@entry_id:750371)的非齐次 PDE。对于我们构造的 $v(x, t)$，由于它在 $x$ 上是线性的，$\frac{\partial^2 v}{\partial x^2} = 0$。因此，新的源项为：

$$
Q(x, t) = - \frac{\partial v}{\partial t} = A_0 \omega \sin(\omega t) \left(1 - \frac{x}{\pi}\right)
$$

现在，问题已转化为求解 $w(x, t)$ 的[标准形式](@entry_id:153058)，可以应用[本征函数展开](@entry_id:177104)法。

#### 空间变化的系数：Sturm-Liouville 问题

在许多物理系统中，材料的属性并非[均匀分布](@entry_id:194597)，这导致 PDE 中的系数是空间位置的函数。例如，考虑一个非均匀杆的热传导问题 [@problem_id:2119367] [@problem_id:2119373]，其方程可能形如：

$$
\frac{\partial u}{\partial t} = \frac{\partial}{\partial x} \left( p(x) \frac{\partial u}{\partial x} \right) + q(x) u + F(x, t)
$$

这里的空间算子 $\mathcal{L}[u] = \frac{d}{dx}(p(x)\frac{du}{dx}) + q(x)u$ 是一个**Sturm-Liouville 算子**。这类算子及其在高维的推广，具有一套完备的本征函数理论。其本征函数 $\phi_n(x)$ 关于一个特定的**权函数** $w(x)$ 正交。

在某些情况下，通过巧妙的**[变量替换](@entry_id:141386)**，可以将复杂的 Sturm-Liouville 问题转化为我们更熟悉的形式。例如，对于方程 $\frac{\partial u}{\partial t} = \frac{\partial}{\partial x}\left(x^2 \frac{\partial u}{\partial x}\right) + \dots$ 在区间 $[1, e]$ 上 [@problem_id:2119367]，我们可以引入新的空间坐标 $y = \ln x$。通过链式法则，可以证明原算子被转换为：

$$
\frac{\partial}{\partial x}\left(x^2 \frac{\partial u}{\partial x}\right) \implies \frac{\partial^2 v}{\partial y^2} + \frac{\partial v}{\partial y}
$$

其中 $v(y, t) = u(e^y, t)$。这样，方程的复杂性从变系数的[二阶导数](@entry_id:144508)项转移到了一个新的一阶导数项。这个[一阶导数](@entry_id:749425)项可以通过另一次变换，即设 $v(y, t) = \exp(-y/2) z(y, t)$ 来消除，最终得到一个[标准形式](@entry_id:153058)的反应[扩散方程](@entry_id:170713)：

$$
\frac{\partial z}{\partial t} = \frac{\partial^2 z}{\partial y^2} - \frac{1}{4}z + \tilde{F}(y,t)
$$

这个方程现在具有[常系数](@entry_id:269842)，并且可以在新的[坐标系](@entry_id:156346) $y \in [0, 1]$ 上使用标准的 $\sin(n\pi y)$ [基函数](@entry_id:170178)进行展开求解 [@problem_id:2119373]。完成求解后，只需通过[逆变](@entry_id:192290)换 $u(x, t) = x^{-1/2} z(\ln x, t)$ 即可得到原始问题的解。这一系列变换展示了在应用[本征函数展开](@entry_id:177104)法之前，对问题进行预处理的重要性。

#### [稳态解](@entry_id:200351)与源项分析

对于[耗散系统](@entry_id:151564)（如热传导），当时间趋于无穷时，系统通常会达到一个不随时间变化的**[稳态](@entry_id:182458)**（steady-state）。此时 $\frac{\partial u}{\partial t} = 0$，PDE 退化为一个关于空间变量的 ODE 或椭圆型 PDE。例如，对于[热方程](@entry_id:144435) $u_t = \alpha^2 u_{xx} + Q(x)$，其[稳态解](@entry_id:200351) $u_{ss}(x)$ 满足：

$$
-\alpha^2 \frac{d^2 u_{ss}}{dx^2} = Q(x)
$$

[本征函数展开](@entry_id:177104)法为分析[稳态解](@entry_id:200351)与热源之间的关系提供了深刻的洞见。将 $u_{ss}(x)$ 和 $Q(x)$ 都展开为本征函数（例如 $\sin(\frac{n\pi x}{L})$）的级数：

$$
u_{ss}(x) = \sum_{n=1}^{\infty} b_n \sin\left(\frac{n\pi x}{L}\right), \quad Q(x) = \sum_{n=1}^{\infty} q_n \sin\left(\frac{n\pi x}{L}\right)
$$

代入[稳态](@entry_id:182458)方程，我们得到：

$$
-\alpha^2 \sum_{n=1}^{\infty} b_n \left( - \left(\frac{n\pi}{L}\right)^2 \right) \sin\left(\frac{n\pi x}{L}\right) = \sum_{n=1}^{\infty} q_n \sin\left(\frac{n\pi x}{L}\right)
$$

通过匹配系数，我们发现解的[模态系数](@entry_id:752057) $b_n$ 与源的[模态系数](@entry_id:752057) $q_n$ 之间存在一个简单的代数关系：

$$
\alpha^2 \left(\frac{n\pi}{L}\right)^2 b_n = q_n \quad \text{或} \quad b_n = \frac{L^2}{\alpha^2 n^2 \pi^2} q_n
$$

这个关系是双向的。一方面，如果我们知道热源 $Q(x)$，我们可以计算其[傅里叶系数](@entry_id:144886) $q_n$，然后直接得到[稳态解](@entry_id:200351)的傅里叶系数 $b_n$，从而重构出 $u_{ss}(x)$ [@problem_id:2119351]。另一方面，如果我们通过实验测量得到了[稳态解](@entry_id:200351) $u_{ss}(x)$，我们就可以反推出热源 $Q(x)$ 的空间分布 [@problem_id:2119370]。例如，如果观测到[稳态解](@entry_id:200351)仅仅是第三个本征模态 $u_{ss}(x) = B \sin(\frac{3\pi x}{L})$，这意味着只有 $b_3 = B$ 非零。根据上述关系，必然也只有 $q_3$ 非零，其值为 $q_3 = \alpha^2 (\frac{3\pi}{L})^2 B$。因此，热源必须是 $Q(x) = \frac{9\pi^2 \alpha^2 B}{L^2} \sin(\frac{3\pi x}{L})$。这揭示了系统的响应特性：系统的空间结构在很大程度上是由驱动它的源项的空间结构决定的。

#### [双曲系统](@entry_id:260647)中的共振现象

对于[波动方程](@entry_id:139839)等双曲型系统，[本征函数展开](@entry_id:177104)法揭示了一个至关重要的物理现象：**共振** (resonance)。考虑一个受外力驱动的弦[振动](@entry_id:267781)问题 [@problem_id:2119324]：

$$
\frac{\partial^2 u}{\partial t^2} = c^2 \frac{\partial^2 u}{\partial x^2} + F(x, t)
$$

与热方程不同，这里时间导数是二阶的。将解和[源项](@entry_id:269111)按[本征函数](@entry_id:154705) $\phi_n(x) = \sin(\frac{n\pi x}{L})$ 展开，我们得到的常微分方程是二阶的：

$$
\ddot{T}_n(t) + c^2 \left(\frac{n\pi}{L}\right)^2 T_n(t) = f_n(t)
$$

这个方程是一个[受迫振动](@entry_id:167019)方程。$\omega_n = \frac{n\pi c}{L}$ 是弦的第 $n$ 个**固有[振动频率](@entry_id:199185)**。如果外力项 $f_n(t)$ 是周期性的，例如 $f_n(t) \propto \sin(\omega t)$，其中 $\omega$ 是**驱动频率**，那么方程的[特解](@entry_id:149080)（强迫响应）的振幅将依赖于 $\omega$ 和 $\omega_n$ 的关系。

[特解](@entry_id:149080)的振幅与 $1/(\omega_n^2 - \omega^2)$ 成正比 [@problem_id:2119324]。当驱动频率 $\omega$ 远小于或远大于固有频率 $\omega_n$ 时，振幅保持在一个有限的水平。然而，当驱动频率 $\omega$ 接近某个固有频率 $\omega_n$ 时，分母 $\omega_n^2 - \omega^2$ 趋近于零，导致强迫响应的振幅急剧增大。在理想的无阻尼情况下（$\omega = \omega_n$），振幅会随时间[线性增长](@entry_id:157553)，趋于无穷。这就是共振现象，它在工程和物理学中具有极其重要的意义，从桥梁的设计到乐器的发声原理都离不开对它的理解。

### 对高维问题的推广

[本征函数展开](@entry_id:177104)法可以自然地推广到二维或三维空间。例如，对于一个在矩形域 $[0, L] \times [0, H]$ 上[振动](@entry_id:267781)的膜，其[二维波动方程](@entry_id:164503)为 [@problem_id:2119340]：

$$
\frac{\partial^2 u}{\partial t^2} = c^2 \left( \frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} \right) + F(x,y,t)
$$

在固定边界（Dirichlet 条件）下，空间算子 $\nabla^2 = \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2}$ 的[本征函数](@entry_id:154705)可以通过[分离变量法](@entry_id:168509)得到，它们是两个一维[本征函数](@entry_id:154705)的乘积：

$$
\phi_{nm}(x, y) = \sin\left(\frac{n\pi x}{L}\right) \sin\left(\frac{m\pi y}{H}\right)
$$

对应的[本征值](@entry_id:154894)为 $\lambda_{nm} = \left(\frac{n\pi}{L}\right)^2 + \left(\frac{m\pi}{H}\right)^2$。

求解过程与一维情况完全类似：将解 $u(x, y, t)$ 和[源项](@entry_id:269111) $F(x, y, t)$ 按这个二维[本征函数](@entry_id:154705)基进行展开：

$$
u(x, y, t) = \sum_{n=1}^{\infty} \sum_{m=1}^{\infty} u_{nm}(t) \phi_{nm}(x, y)
$$

代入 PDE 后，同样会得到一系列关于时间系数 $u_{nm}(t)$ 的[常微分方程](@entry_id:147024)：

$$
\ddot{u}_{nm}(t) + c^2 \lambda_{nm} u_{nm}(t) = f_{nm}(t)
$$

每个 ODE 描述了一个独立的[振动](@entry_id:267781)模态 $(n, m)$ 的[时间演化](@entry_id:153943)。通过求解这些 ODE 并将结果叠加，即可获得完整解。如果[源项](@entry_id:269111)的[空间分布](@entry_id:188271)恰好与某个特定的本征函数 $\phi_{nm}$ 相匹配，那么只有对应的那个模态 $u_{nm}(t)$ 会被激发，极大地简化了计算 [@problem_id:2119340]。

总而言之，[本征函数展开](@entry_id:177104)法是一个强大而系统的工具，它利用了[线性算子的谱](@entry_id:263200)理论，将复杂的时空演化[问题分解](@entry_id:272624)为一系列独立的时间演化模态。通过理解如何处理[非齐次边界条件](@entry_id:750645)、变系数、不同类型的方程以及高维问题，我们可以将这一方法应用于物理和工程中广泛的非齐次问题。