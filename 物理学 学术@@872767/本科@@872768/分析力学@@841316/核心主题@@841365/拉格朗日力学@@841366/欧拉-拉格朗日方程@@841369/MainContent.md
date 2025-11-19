## 引言
[欧拉-拉格朗日方程](@entry_id:137827)是[分析力学](@entry_id:166738)的基石，它提供了一个基于能量的、强大而优美的视角来理解物理世界的运动规律。相较于直接处理矢量力和加速度的[牛顿力学](@entry_id:162125)，[拉格朗日方法](@entry_id:142825)通过[作用量原理](@entry_id:154742)这一更为基本的概念，为描述从单个粒子到整个宇宙的动力学演化提供了一个统一的框架。它解决了在处理复杂系统，特别是含有约束和多自由度的系统时，牛顿方法所面临的困难，避免了对繁琐约束力的直接分析。

本文将带领读者分三步深入探索欧拉-拉格朗日方程的奥秘。在“原理与机制”一章中，我们将从[作用量原理](@entry_id:154742)出发，详细推导标准的欧拉-拉格朗日方程，并探讨其在多自由度、高阶导数及[场论](@entry_id:155241)中的各种推广形式，同时揭示其与[守恒定律](@entry_id:269268)的深刻联系。接着，在“应用与跨学科联系”一章中，我们将展示该方程如何在经典力学、电磁学、几何学乃至相对论中作为核心工具，解决各类实际问题，彰显其惊人的普适性。最后，通过“动手实践”环节，读者将有机会亲手应用所学知识，解决具体的[变分问题](@entry_id:756445)，从而巩固并深化理解。

## 原理与机制

在[分析力学](@entry_id:166738)中，我们寻求描述物理系统演化的[普适性原理](@entry_id:137218)。相比于直接处理力与加速度的[牛顿力学](@entry_id:162125)，[拉格朗日力学](@entry_id:147054)提供了一种基于能量的、更为优雅和强大的数学框架。这一框架的核心是[作用量原理](@entry_id:154742)（Principle of Action）以及从中推导出的[欧拉-拉格朗日方程](@entry_id:137827)（Euler-Lagrange Equation）。本章将深入探讨欧拉-拉格朗日方程的原理、推导、多种推广形式及其在解决物理问题中的应用。

### [作用量原理](@entry_id:154742)与标准的[欧拉-拉格朗日方程](@entry_id:137827)

[分析力学](@entry_id:166738)的一个基本假设是**最小作用量原理**（Principle of Least Action），更准确地说是**[平稳作用量原理](@entry_id:151723)**（Principle of Stationary Action）。该原理指出，一个物理系统从一个状态演化到另一个状态时，其真实运动路径是使某个称为**作用量**（Action）的积分量取“平稳值”（即[极值](@entry_id:145933)或[鞍点](@entry_id:142576)）的路径。

对于一个由[广义坐标](@entry_id:156576) $q(t)$ 描述的系统，其作用量 $S$ 通常定义为一个称为**[拉格朗日量](@entry_id:174593)**（Lagrangian） $L$ 的函数对时间的积分。拉格朗日量本身是[广义坐标](@entry_id:156576) $q$、[广义速度](@entry_id:178456) $\dot{q}$ 以及时间 $t$ 的函数，即 $L(q, \dot{q}, t)$。作用量 $S$ 是一个**泛函**（functional），它的输入是一个函数（即路径 $q(t)$），输出是一个标量值：

$$S[q(t)] = \int_{t_1}^{t_2} L(q(t), \dot{q}(t), t) dt$$

在经典力学中，对于一个保守系统，[拉格朗日量](@entry_id:174593)被定义为系统的动能 $T$ 与势能 $U$之差：$L = T - U$。

我们的目标是找到使作用量 $S$ 取平稳值的路径 $q(t)$。为此，我们考虑对真实路径 $q(t)$ 施加一个微小的变分 $\delta q(t) = \epsilon \eta(t)$，其中 $\epsilon$ 是一个微小参数，$\eta(t)$ 是一个在端点处为零（即 $\eta(t_1) = \eta(t_2) = 0$）的任意光滑函数。[平稳作用量原理](@entry_id:151723)要求作用量的一阶变分为零，即 $\delta S = 0$，这等价于：

$$\left.\frac{dS[q + \epsilon\eta]}{d\epsilon}\right|_{\epsilon=0} = 0$$

通过[链式法则](@entry_id:190743)和分部积分法，可以证明上述条件等价于路径 $q(t)$ 满足一个[微分方程](@entry_id:264184)，这就是**[欧拉-拉格朗日方程](@entry_id:137827)**：

$$\frac{\partial L}{\partial q} - \frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}}\right) = 0$$

这个方程是[拉格朗日力学](@entry_id:147054)的基石。它将一个复杂的[变分问题](@entry_id:756445)转化为了一个[微分方程](@entry_id:264184)求解问题。

为了更好地理解该方程的运用，让我们从一个纯数学的例子开始。考虑寻找一个函数 $y(x)$，它连接 $(0,0)$ 和 $(1,2)$ 两点，并使得泛函 $J[y] = \int_0^1 ((y')^2 + y y') dx$ 取平稳值 [@problem_id:2141487]。这里的“拉格朗日量”为 $L(y, y') = (y')^2 + y y'$。我们计算其对 $y$ 和 $y'$ 的偏导数：

$$\frac{\partial L}{\partial y} = y'$$
$$\frac{\partial L}{\partial y'} = 2y' + y$$

将它们代入欧拉-拉格朗日方程（此时自变量为 $x$ 而非 $t$）：

$$\frac{d}{dx}\left(\frac{\partial L}{\partial y'}\right) - \frac{\partial L}{\partial y} = \frac{d}{dx}(2y' + y) - y' = (2y'' + y') - y' = 2y'' = 0$$

我们得到了一个极其简洁的[常微分方程](@entry_id:147024) $y''=0$。其通解为 $y(x) = c_1 x + c_0$。利用边界条件 $y(0)=0$ 和 $y(1)=2$，我们确定常数 $c_0=0$ 和 $c_1=2$。因此，所求的函数为 $y(x) = 2x$。

在更普遍的情况下，[拉格朗日量](@entry_id:174593)可能显式地依赖于[自变量](@entry_id:267118)（如时间 $t$ 或空间坐标 $x$）。例如，考虑泛函 $J[y] = \int_0^1 ( (y')^2 + y^2 - 2y e^x ) dx$ [@problem_id:2141517]。这里的拉格朗日量为 $L(x, y, y') = (y')^2 + y^2 - 2y e^x$。我们再次应用欧拉-拉格朗日方程：

$$\frac{\partial L}{\partial y} = 2y - 2e^x$$
$$\frac{\partial L}{\partial y'} = 2y'$$

代入方程得到：

$$(2y - 2e^x) - \frac{d}{dx}(2y') = 0$$
$$2y - 2e^x - 2y'' = 0$$

整理后，我们得到一个二阶非齐次[线性常微分方程](@entry_id:276013) $y'' - y = -e^x$。这个例子表明，当拉格朗日量显式地依赖于自变量时，通常会在最终的运动方程中产生一个“[驱动项](@entry_id:165986)”或“[源项](@entry_id:269111)”。

### 欧拉-拉格朗日方程的推广

[标准形式](@entry_id:153058)的欧拉-拉格朗日方程可以被推广，以处理更复杂的物理情境，例如多自由度系统、高阶导数问题以及场论。

#### 多自由度系统

对于一个由 $N$ 个[广义坐标](@entry_id:156576) $\{q_1, q_2, \dots, q_N\}$ 描述的系统，其拉格朗日量是所有坐标和速度的函数 $L(q_1, \dots, q_N, \dot{q}_1, \dots, \dot{q}_N, t)$。[作用量原理](@entry_id:154742)要求对每一个坐标的独立变分，作用量都保持平稳。这导致我们得到一个包含 $N$ 个耦合[微分方程](@entry_id:264184)的[方程组](@entry_id:193238)，每个方程对应一个[广义坐标](@entry_id:156576) $q_i$：

$$\frac{\partial L}{\partial q_i} - \frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}_i}\right) = 0, \quad \text{for } i=1, 2, \dots, N$$

一个典型的例子是二维[离子阱](@entry_id:192565)中的[带电粒子运动](@entry_id:262424)模型 [@problem_id:2141522]。假设一个质量为 $m$ 的粒子在 $xy$ 平面内运动，其动能为 $T = \frac{1}{2}m(\dot{x}^2 + \dot{y}^2)$，[势能](@entry_id:748988)为 $U(x, y) = \alpha(x^2 - y^2)$。系统的拉格朗日量为：

$$L(x, y, \dot{x}, \dot{y}) = T - U = \frac{1}{2}m(\dot{x}^2 + \dot{y}^2) - \alpha(x^2 - y^2)$$

我们分别对 $x$ 和 $y$ 坐标应用[欧拉-拉格朗日方程](@entry_id:137827)。

对于 $x$ 坐标：
$$\frac{\partial L}{\partial x} = -2\alpha x, \quad \frac{\partial L}{\partial \dot{x}} = m\dot{x}$$
方程为：$-2\alpha x - \frac{d}{dt}(m\dot{x}) = 0 \implies m\ddot{x} + 2\alpha x = 0$。

对于 $y$ 坐标：
$$\frac{\partial L}{\partial y} = 2\alpha y, \quad \frac{\partial L}{\partial \dot{y}} = m\dot{y}$$
方程为：$2\alpha y - \frac{d}{dt}(m\dot{y}) = 0 \implies m\ddot{y} - 2\alpha y = 0$。

我们得到了两个独立的[运动方程](@entry_id:170720)：$\ddot{x} = -\frac{2\alpha}{m}x$ 和 $\ddot{y} = \frac{2\alpha}{m}y$。这清晰地展示了[拉格朗日方法](@entry_id:142825)如何系统地导出多自由度系统的运动方程。

#### 依赖[高阶导数](@entry_id:140882)的泛函

在某些领域，如弹性力学中，系统的能量不仅依赖于位移及其一阶导数，还可能依赖于更高阶的导数。例如，一根梁的弯曲能量与其曲率相关，而曲率由位移函数的[二阶导数](@entry_id:144508) $y''(x)$ 描述。对于一个依赖于 $y''$ 的泛函 $J[y] = \int L(x, y, y', y'') dx$，其[欧拉-拉格朗日方程](@entry_id:137827)（有时称为**[欧拉-泊松方程](@entry_id:749105)**）推广为：

$$\frac{\partial L}{\partial y} - \frac{d}{dx}\left(\frac{\partial L}{\partial y'}\right) + \frac{d^2}{dx^2}\left(\frac{\partial L}{\partial y''}\right) = 0$$

考虑一个长度为 $L$ 的弹性梁，其总[势能](@entry_id:748988)由泛函 $J[y] = \int_{0}^{L} ( \frac{1}{2} (y'')^2 + y \sin(\frac{\pi x}{L}) ) dx$ 给出 [@problem_id:2141489]。这里的[拉格朗日量](@entry_id:174593) $L = \frac{1}{2}(y'')^2 + y \sin(\frac{\pi x}{L})$ 依赖于 $y''$。我们计算各偏导数：

$$\frac{\partial L}{\partial y} = \sin\left(\frac{\pi x}{L}\right), \quad \frac{\partial L}{\partial y'} = 0, \quad \frac{\partial L}{\partial y''} = y''$$

代入[欧拉-泊松方程](@entry_id:749105)，得到：

$$\sin\left(\frac{\pi x}{L}\right) - \frac{d}{dx}(0) + \frac{d^2}{dx^2}(y'') = 0$$

这给出了描述梁形变的四阶[微分方程](@entry_id:264184) $y^{(4)}(x) = -\sin(\frac{\pi x}{L})$。求解这个方程并应用边界条件，就可以确定梁的平衡形状。

#### [场论](@entry_id:155241)中的应用

[作用量原理](@entry_id:154742)的威力远不止于处理离散坐标。在物理学中，场（如[电磁场](@entry_id:265881)或[引力场](@entry_id:169425)）在时空中的每一点都有值。场的行为也可以通过[作用量原理](@entry_id:154742)来描述。此时，拉格朗日量被一个**拉格朗日密度** $\mathcal{L}$ 替代，作用量是对整个时空区域的积分。

例如，对于一个定义在 $xy$ 平面上的标量场 $u(x, y)$，其拉格朗日密度可能依赖于场 $u$ 及其偏导数 $u_x = \frac{\partial u}{\partial x}$ 和 $u_y = \frac{\partial u}{\partial y}$。作用量为 $J[u] = \iint_\Omega \mathcal{L}(u, u_x, u_y) \,dx\,dy$。此时的欧拉-拉格朗日方程变为一个[偏微分方程](@entry_id:141332)：

$$\frac{\partial \mathcal{L}}{\partial u} - \frac{\partial}{\partial x}\left(\frac{\partial \mathcal{L}}{\partial u_x}\right) - \frac{\partial}{\partial y}\left(\frac{\partial \mathcal{L}}{\partial u_y}\right) = 0$$

考虑一个拉格朗日密度为 $\mathcal{L}(u_x, u_y) = u_x^2 - u_y^2$ 的系统 [@problem_id:2141494]。各偏导数为：

$$\frac{\partial \mathcal{L}}{\partial u} = 0, \quad \frac{\partial \mathcal{L}}{\partial u_x} = 2u_x, \quad \frac{\partial \mathcal{L}}{\partial u_y} = -2u_y$$

代入场论的欧拉-拉格朗日方程：

$$0 - \frac{\partial}{\partial x}(2u_x) - \frac{\partial}{\partial y}(-2u_y) = 0 \implies -2u_{xx} + 2u_{yy} = 0$$

这正是标准的[一维波动方程](@entry_id:164824) $u_{xx} - u_{yy} = 0$（若将 $y$ 视为时间）。这表明，许多基本的物理场方程都可以从一个简洁的[作用量原理](@entry_id:154742)中推导出来。

### 对称性、[守恒定律](@entry_id:269268)与[第一积分](@entry_id:261013)

[拉格朗日形式主义](@entry_id:158185)的一个深刻之处在于它揭示了系统的**对称性**（Symmetry）与**[守恒定律](@entry_id:269268)**（Conservation Law）之间的内在联系。这一联系由 [Noether 定理](@entry_id:145690)（Noether's Theorem）给出。简而言之，如果系统的拉格朗日量在某种连续变换下保持不变（即具有某种对称性），那么系统就必定存在一个相应的[守恒量](@entry_id:150267)。

#### [循环坐标](@entry_id:166220)与守恒动量

一个常见的对称性是空间平移不变性。如果[拉格朗日量](@entry_id:174593) $L$ 不显式地依赖于某个[广义坐标](@entry_id:156576) $q_k$，即 $\frac{\partial L}{\partial q_k} = 0$，则称 $q_k$ 是一个**[循环坐标](@entry_id:166220)**（cyclic coordinate）或**[可忽略坐标](@entry_id:166220)**（ignorable coordinate）。

在这种情况下，[欧拉-拉格朗日方程](@entry_id:137827) $\frac{\partial L}{\partial q_k} - \frac{d}{dt}(\frac{\partial L}{\partial \dot{q}_k}) = 0$ 简化为：

$$\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}_k}\right) = 0$$

这意味着量 $\frac{\partial L}{\partial \dot{q}_k}$ 不随时间变化，是一个守恒量。我们定义这个守恒量为坐标 $q_k$ 的**广义[共轭动量](@entry_id:172203)**（generalized conjugate momentum），记作 $p_k$：

$$p_k \equiv \frac{\partial L}{\partial \dot{q}_k} = \text{constant}$$

例如，考虑一个在一维空间中自由运动的相对论性粒子 [@problem_id:2141488]。其[拉格朗日量](@entry_id:174593)为 $L(\dot{x}) = -m_0 c^2 \sqrt{1 - \dot{x}^2/c^2}$，其中 $m_0$ 是[静止质量](@entry_id:264101)，$c$ 是光速。我们注意到，$L$ 不依赖于位置坐标 $x$，因此 $x$ 是一个[循环坐标](@entry_id:166220)。这意味着与 $x$ 共轭的动量是守恒的。我们计算这个守恒量：

$$p_x = \frac{\partial L}{\partial \dot{x}} = -m_0 c^2 \cdot \frac{1}{2\sqrt{1-\dot{x}^2/c^2}} \cdot \left(-\frac{2\dot{x}}{c^2}\right) = \frac{m_0 \dot{x}}{\sqrt{1-\dot{x}^2/c^2}}$$

这个表达式正是相对论中的动量。[拉格朗日方法](@entry_id:142825)自动地告诉我们，由于空间是均匀的（拉格朗日量与 $x$ 无关），系统的动量必须守恒。

#### 贝尔特拉米等式与[能量守恒](@entry_id:140514)

另一个重要的对称性是[时间平移不变性](@entry_id:270209)。如果[拉格朗日量](@entry_id:174593) $L$ 不显式地依赖于时间 $t$，即 $\frac{\partial L}{\partial t} = 0$，那么系统也存在一个守恒量。这个守恒量可以通过**贝尔特拉米等式**（Beltrami Identity）找到。对于只有一个自变量的系统，该等式表述为：

$$L - y' \frac{\partial L}{\partial y'} = \text{constant}$$

对于多自由度系统，它推广为 $\sum_i \dot{q}_i \frac{\partial L}{\partial \dot{q}_i} - L = \text{constant}$。这个[守恒量](@entry_id:150267)被称为系统的**[哈密顿量](@entry_id:172864)**（Hamiltonian），通常对应于系统的总能量。

贝尔特拉米等式在求解问题时非常有用，因为它能直接给出一个运动的“[第一积分](@entry_id:261013)”，从而将二阶的欧拉-拉格朗日方程降为一阶方程。

例如，考虑泛函 $J[y] = \int y^n \sqrt{1 + (y')^2} dx$ [@problem_id:2141485]。其[拉格朗日量](@entry_id:174593) $L(y, y') = y^n \sqrt{1 + (y')^2}$ 不显式依赖于 $x$。因此，我们可以应用贝尔特拉米等式。首先计算：

$$\frac{\partial L}{\partial y'} = y^n \frac{y'}{\sqrt{1+(y')^2}}$$

代入贝尔特拉米等式，守恒量为：

$$F(y, y') = L - y' \frac{\partial L}{\partial y'} = y^n \sqrt{1+(y')^2} - y' \left(\frac{y^n y'}{\sqrt{1+(y')^2}}\right)$$
$$= \frac{y^n (1+(y')^2) - y^n (y')^2}{\sqrt{1+(y')^2}} = \frac{y^n}{\sqrt{1+(y')^2}}$$

因此，沿着[极值](@entry_id:145933)路径，$\frac{y^n}{\sqrt{1+(y')^2}}$ 必然是一个常数。

这个技巧也适用于物理问题，如光学。根据**[费马原理](@entry_id:175608)**（Fermat's Principle），光线在两点间的传播路径是使光程（或传播时间）最短的路径。在[折射率](@entry_id:168910)为 $n(y)$ 的介质中，光线的传播时间泛函为 $T[y] = \frac{1}{c} \int n(y) \sqrt{1+(y')^2} dx$ [@problem_id:2141491]。这里的“[拉格朗日量](@entry_id:174593)” $L(y,y') = n(y)\sqrt{1+(y')^2}$ 不显式依赖于 $x$。因此，我们可以立即使用贝尔特拉米等式得到一个[守恒量](@entry_id:150267)（这在光学中被称为斯涅尔定律的一般形式），从而大大简化求解过程。

### [约束系统](@entry_id:164587)与边界条件

在许多实际问题中，系统的运动受到某些限制，即**约束**（constraints）。此外，[变分问题](@entry_id:756445)的端点也未必是固定的。[拉格朗日形式主义](@entry_id:158185)提供了处理这些复杂情况的系统方法。

#### 约束与[拉格朗日乘子法](@entry_id:176596)

如果一个系统的约束可以用[代数方程](@entry_id:272665) $f(q_1, \dots, q_N, t) = 0$ 来描述，这种约束被称为**[完整约束](@entry_id:140686)**（holonomic constraint）。处理这类约束的强大工具是**拉格朗日乘子法**（Method of Lagrange Multipliers）。

其思想是引入一个新的待定函数 $\lambda(t)$（[拉格朗日乘子](@entry_id:142696)），并构建一个新的、无约束的[拉格朗日量](@entry_id:174593) $L'$：

$$L' = L + \lambda(t) f(\mathbf{q}, t)$$

然后对这个增广的[拉格朗日量](@entry_id:174593) $L'$ 和所有坐标 $q_i$ 应用欧拉-拉格朗日方程。这样，我们得到一组方程，其中包含了待定的乘子 $\lambda(t)$。这些方程与约束方程本身联立，就足以确定所有 $q_i(t)$ 和 $\lambda(t)$。

[拉格朗日乘子](@entry_id:142696)具有深刻的物理意义：它与维持约束所需的**[约束力](@entry_id:170052)**（force of constraint）直接相关。具体来说，[广义约束力](@entry_id:178528) $Q_i$ 等于 $\lambda \frac{\partial f}{\partial q_i}$。

以经典的单摆为例 [@problem_id:2083806]，一个质量为 $m$ 的质点通过长度为 $L$ 的轻杆连接到[固定点](@entry_id:156394)。在[笛卡尔坐标系](@entry_id:169789)中，动能为 $T = \frac{1}{2}m(\dot{x}^2 + \dot{y}^2)$，[势能](@entry_id:748988)为 $U=mgy$（设 $y$ 轴竖直向上）。约束条件为杆长固定，即 $f(x,y) = x^2 + y^2 - L^2 = 0$。

[增广拉格朗日量](@entry_id:177042)为：
$$L' = \frac{1}{2}m(\dot{x}^2 + \dot{y}^2) - mgy + \lambda(t)(x^2 + y^2 - L^2)$$

对 $x$ 和 $y$ 的欧拉-拉格朗日方程为：
$$\frac{\partial L'}{\partial x} - \frac{d}{dt}\left(\frac{\partial L'}{\partial \dot{x}}\right) = 2\lambda x - m\ddot{x} = 0 \implies m\ddot{x} = 2\lambda x$$
$$\frac{\partial L'}{\partial y} - \frac{d}{dt}\left(\frac{\partial L'}{\partial \dot{y}}\right) = -mg + 2\lambda y - m\ddot{y} = 0 \implies m\ddot{y} = 2\lambda y - mg$$

这里的 $2\lambda x$ 和 $2\lambda y$ 分别是约束力（即杆的张力）在 $x$ 和 $y$ 方向的分量。因此，张力的大小 $T$ 与 $\lambda$ 直接相关。通过求解这组方程以及[约束方程](@entry_id:138140)，我们不仅能得到摆的运动轨迹，还能同时解出维持该运动所需的张力。

#### 自然边界条件与横截条件

我们之[前推](@entry_id:158718)导[欧拉-拉格朗日方程](@entry_id:137827)时假设了路径的端点是固定的。然而，在某些问题中，端点可能不是一个固定的点，而是可以在某条曲线上自由滑动。在这种情况下，变分原理不仅给出了路径应遵循的[微分方程](@entry_id:264184)，还额外给出了路径在端点处必须满足的**自然边界条件**（natural boundary condition）。

考虑一个泛函 $J[y] = \int_a^b L(x, y, y') dx$，其中起点 $(a, y(a))$ 固定，而终点 $(b, y(b))$ 可以在一条给定的曲线 $g(x,y)=0$ 上自由移动。在推导过程中，由于终点变分 $(\delta b, \delta y(b))$ 不再为零，分部积分会产生一个边界项。为了使作用量的一阶变分为零，这个边界项必须消失。这导致了所谓的**横截条件**（transversality condition）：

$$\left[L - y' \frac{\partial L}{\partial y'}\right]_{x=b} \delta b + \left[\frac{\partial L}{\partial y'}\right]_{x=b} \delta y_b = 0$$

其中 $(\delta b, \delta y_b)$ 是沿终端曲线 $g(x,y)=0$ 的任意微小位移。

例如，考虑一个路径从点 $(0, \sqrt{2})$ 出发，终止于水平直线 $y=1$ 上，并使泛函 $J[y] = \int_0^b (y^2 + (y')^2) dx$ 取平稳值 [@problem_id:2322666]。

首先，欧拉-拉格朗日方程 $y'' - y = 0$ 给出路径的基本形式 $y(x) = \alpha \cosh x + \beta \sinh x$。
其次，在终端 $x=b$ 处，路径位于直线 $y=1$ 上。这意味着任何允许的变分都必须保持 $y$ 不变，即 $\delta y_b=0$，而 $\delta b$ 是任意的。代入横截条件，我们得到：

$$\left[L - y' \frac{\partial L}{\partial y'}\right]_{x=b} = 0$$

对于 $L = y^2 + (y')^2$，这个条件变为 $[y^2 + (y')^2 - y'(2y')]_{x=b} = y(b)^2 - y'(b)^2 = 0$。结合路径必须满足的[微分方程](@entry_id:264184)和这个自然边界条件，我们就可以唯一地确定路径和其终点坐标 $b$。

综上所述，欧拉-拉格朗日方程及其推广是[分析力学](@entry_id:166738)和数学物理中一个极其强大的工具。它不仅能系统地导出运动方程，还能深刻地揭示物理定律背后的[对称性与守恒律](@entry_id:160300)，并能优雅地处理复杂的约束和边界问题。