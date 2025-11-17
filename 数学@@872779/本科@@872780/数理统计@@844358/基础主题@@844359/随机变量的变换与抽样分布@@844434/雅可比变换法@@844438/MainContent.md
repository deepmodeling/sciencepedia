## 引言
在科学与工程的众多领域中，我们经常需要分析由已知[随机变量](@entry_id:195330)通过[函数变换](@entry_id:141095)得到的新变量的统计特性。例如，物理学家可能关心由[粒子速度](@entry_id:196946)[分布](@entry_id:182848)决定的动能[分布](@entry_id:182848)，而金融分析师则需要从资产的日收益率[分布](@entry_id:182848)推断其长期价值的[分布](@entry_id:182848)。虽然存在多种方法，但当处理连续型[随机变量](@entry_id:195330)，尤其是多维情况时，缺乏一个系统性的框架会使问题变得异常复杂。雅可比变换法（Jacobian method）正是填补这一空白的强大数学工具，它为这类问题提供了一个统一而严谨的解决方案。

本文旨在全面阐释[雅可比方法](@entry_id:270947)。在“原理与机制”一章中，我们将从单变量变换出发，逐步深入到多维变换，揭示雅可比行列式作为概率密度缩放因子的核心机制。接着，在“应用与跨学科联系”一章中，我们将展示该方法如何在物理学、工程学、经济学和[多元统计学](@entry_id:172773)中解决实际问题，例如在[坐标系](@entry_id:156346)变换和推导关键统计量[分布](@entry_id:182848)中的应用。最后，“动手实践”部分将提供一系列练习，帮助读者巩固理论知识并将其应用于具体情境。通过本文的学习，您将掌握一个在[不确定性建模](@entry_id:268420)和数据分析中不可或缺的分析工具。

## 原理与机制

在概率论与统计学的研究中，我们常常需要理解一个或多个[随机变量](@entry_id:195330)经过某个[函数变换](@entry_id:141095)后，其[概率分布](@entry_id:146404)如何随之改变。例如，在物理学中，我们可能知道一个粒子的速度[分布](@entry_id:182848)，并希望推导出其动能的[分布](@entry_id:182848)；在经济学中，我们可能对资产收益率的[分布](@entry_id:182848)有模型，但更关心其长期累积价值的[分布](@entry_id:182848)。解决这类问题的核心工具是[随机变量的变换](@entry_id:267283)方法，其中，**[雅可比方法](@entry_id:270947) (Jacobian method)** 提供了一个系统而强大的框架，尤其适用于处理连续型[随机变量](@entry_id:195330)的多维变换。本章将深入探讨这一方法的基本原理、数学机制及其在各种情境下的应用。

### 单变量变换：从累积分布函数到[概率密度函数](@entry_id:140610)

我们从最简单的情形开始：假设已知连续型[随机变量](@entry_id:195330) $X$ 的[概率密度函数](@entry_id:140610) (PDF) 为 $f_X(x)$，我们想要求出新[随机变量](@entry_id:195330) $Y = g(X)$ 的[概率密度函数](@entry_id:140610) $f_Y(y)$。

最基本、最普适的方法是**[累积分布函数法](@entry_id:268506) (CDF method)**。根据定义，$Y$ 的[累积分布函数 (CDF)](@entry_id:264700) 是 $F_Y(y) = P(Y \le y)$。通过代入 $Y=g(X)$，我们可以将其表示为关于 $X$ 的一个概率：

$F_Y(y) = P(g(X) \le y)$

一旦我们求出了 $F_Y(y)$ 的表达式，其概率密度函数就可以通过求导得到：$f_Y(y) = \frac{d}{dy}F_Y(y)$。

虽然CDF法在理论上总是可行的，但当变换函数 $g(X)$ 是严格单调时，我们可以推导出一个更直接的公式。假设 $y = g(x)$ 是一个严格单调（递增或递减）的[可微函数](@entry_id:144590)。这意味着它存在一个唯一的[反函数](@entry_id:141256) $x = g^{-1}(y) = h(y)$。

如果 $g$ 是严格单调递增的，那么 $g(x) \le y$ 等价于 $x \le h(y)$。因此，
$F_Y(y) = P(X \le h(y)) = F_X(h(y))$

对 $y$ 求导，并应用[链式法则](@entry_id:190743)，我们得到：
$f_Y(y) = \frac{d}{dy} F_X(h(y)) = f_X(h(y)) \cdot \frac{dh(y)}{dy}$

如果 $g$ 是严格单调递减的，那么 $g(x) \le y$ 等价于 $x \ge h(y)$。因此，
$F_Y(y) = P(X \ge h(y)) = 1 - F_X(h(y))$

对 $y$ 求导，我们得到：
$f_Y(y) = -f_X(h(y)) \cdot \frac{dh(y)}{dy}$

注意到，对于单调递减函数，其导数 $h'(y)$ 为负。因此，我们可以将这两种情况统一为一个公式：

$f_Y(y) = f_X(h(y)) \left| \frac{dh(y)}{dy} \right|$

这里的 $\left| \frac{dh(y)}{dy} \right|$ 就是单变量变换的**[雅可比行列式](@entry_id:137120) (Jacobian determinant)** 的[绝对值](@entry_id:147688)。它在公式中的作用至关重要，可以直观地理解为一个**缩放因子**。当变换将一个区间 $dx$ 映射到一个区间 $dy$ 时，概率“质量”必须守恒，即 $f_Y(y)|dy| \approx f_X(x)|dx|$。因此，$f_Y(y) \approx f_X(x) \left| \frac{dx}{dy} \right|$，这与我们的公式完全一致。它量化了变换对[概率密度](@entry_id:175496)进行的拉伸或压缩。

#### 示例：[柯西分布](@entry_id:266469)的倒数

让我们通过一个具体的例子来理解这个公式。在物理学和金融学中常见的[柯西分布](@entry_id:266469)，其概率密度函数为：
$f_X(x) = \frac{\gamma}{\pi \left( (x - x_0)^2 + \gamma^2 \right)}, \quad -\infty  x  \infty$

其中 $x_0$ 是峰值[位置参数](@entry_id:176482)，$\gamma > 0$ 是[尺度参数](@entry_id:268705)。现在，我们考虑一个新的[随机变量](@entry_id:195330) $Y = 1/X$，这在电路中对应于电阻与[电导](@entry_id:177131)的关系。我们的目标是求出 $Y$ 的PDF $f_Y(y)$ [@problem_id:1313188]。

1.  **确定变换及其[反函数](@entry_id:141256)**：变换为 $y = g(x) = 1/x$。其[反函数](@entry_id:141256)为 $x = h(y) = 1/y$。这个变换在 $(-\infty, 0)$ 和 $(0, \infty)$ 上都是严格单调的。

2.  **计算[雅可比行列式](@entry_id:137120)**：[反函数的导数](@entry_id:158287)是 $\frac{dh(y)}{dy} = -\frac{1}{y^2}$。其[绝对值](@entry_id:147688)为 $\left| \frac{dh(y)}{dy} \right| = \frac{1}{y^2}$。

3.  **应用变换公式**：将 $x=1/y$ 和[雅可比行列式](@entry_id:137120)代入公式：
    $f_Y(y) = f_X(h(y)) \left| \frac{dh(y)}{dy} \right| = f_X\left(\frac{1}{y}\right) \cdot \frac{1}{y^2}$
    $f_Y(y) = \frac{\gamma}{\pi \left( (\frac{1}{y} - x_0)^2 + \gamma^2 \right)} \cdot \frac{1}{y^2}$

4.  **化简表达式**：为了使表达式更清晰，我们整理分母中的项：
    $f_Y(y) = \frac{\gamma}{\pi \left( \frac{(1 - x_0y)^2}{y^2} + \gamma^2 \right)} \cdot \frac{1}{y^2} = \frac{\gamma}{\pi \left( (1 - x_0y)^2 + \gamma^2y^2 \right)}$

这个结果就是 $Y$ 的[概率密度函数](@entry_id:140610)。有趣的是，一个广义[柯西分布](@entry_id:266469)的倒数仍然是一个形式类似[柯西分布](@entry_id:266469)的变量。

### 多维变换与雅可比矩阵

当变换涉及多个[随机变量](@entry_id:195330)时，单变量的方法可以自然地推广。假设我们有一个 $n$ 维随机向量 $\mathbf{X} = (X_1, \dots, X_n)$，其联合PDF为 $f_\mathbf{X}(x_1, \dots, x_n)$。我们定义一个新的随机向量 $\mathbf{Y} = (Y_1, \dots, Y_n)$，其中每个 $Y_i$ 都是 $X_j$ 的函数：
$Y_1 = g_1(X_1, \dots, X_n)$
$...$
$Y_n = g_n(X_1, \dots, X_n)$

我们记这个变换为 $\mathbf{Y} = \mathbf{g}(\mathbf{X})$。为了求出 $\mathbf{Y}$ 的联合PDF $f_\mathbf{Y}(\mathbf{y})$，我们假设该变换是可逆的，即存在反变换 $\mathbf{X} = \mathbf{g}^{-1}(\mathbf{Y}) = \mathbf{h}(\mathbf{Y})$:
$X_1 = h_1(Y_1, \dots, Y_n)$
$...$
$X_n = h_n(Y_1, \dots, Y_n)$

此时，单变量导数的角色由**[雅可比矩阵](@entry_id:264467) (Jacobian matrix)** $J$ 来扮演。这个矩阵是反变换 $\mathbf{h}$ 所有一阶[偏导数](@entry_id:146280)的集合：
$J = \begin{pmatrix}
\frac{\partial x_1}{\partial y_1}  \frac{\partial x_1}{\partial y_2}  \cdots  \frac{\partial x_1}{\partial y_n} \\
\frac{\partial x_2}{\partial y_1}  \frac{\partial x_2}{\partial y_2}  \cdots  \frac{\partial x_2}{\partial y_n} \\
\vdots  \vdots  \ddots  \vdots \\
\frac{\partial x_n}{\partial y_1}  \frac{\partial x_n}{\partial y_2}  \cdots  \frac{\partial x_n}{\partial y_n}
\end{pmatrix}$

多维变换的公式为：
$f_\mathbf{Y}(\mathbf{y}) = f_\mathbf{X}(\mathbf{h}(\mathbf{y})) \left| \det(J) \right|$

这里的 $|\det(J)|$ 是雅可比矩阵[行列式](@entry_id:142978)的[绝对值](@entry_id:147688)，它代表了从 $\mathbf{y}$ 空间的一个微小体积元 $d\mathbf{y}$ 到 $\mathbf{x}$ 空间对应体积元 $d\mathbf{x}$ 的**局部[体积缩放因子](@entry_id:158899)**。[概率守恒](@entry_id:149166)的直观思想 $f_\mathbf{X}(\mathbf{x}) d\mathbf{x} = f_\mathbf{Y}(\mathbf{y}) d\mathbf{y}$ 在这里被精确地表述为 $d\mathbf{x} = |\det(J)| d\mathbf{y}$。

#### 示例：二维正态分布的旋转

一个经典的应用是考察二维标准正态分布的[旋转不变性](@entry_id:137644)。假设一个粒子在二维平面上的位置坐标 $(X, Y)$ 是由两个独立的、服从标准正态分布 $N(0, 1)$ 的[随机变量](@entry_id:195330)决定的。它们的联合PDF是：
$f_{X,Y}(x,y) = f_X(x) f_Y(y) = \frac{1}{\sqrt{2\pi}}\exp\left(-\frac{x^2}{2}\right) \cdot \frac{1}{\sqrt{2\pi}}\exp\left(-\frac{y^2}{2}\right) = \frac{1}{2\pi}\exp\left(-\frac{x^2+y^2}{2}\right)$

现在，我们将[坐标系](@entry_id:156346)绕原点逆时针旋转一个固定的角度 $\theta$，得到新的坐标 $(X', Y')$ [@problem_id:1313200]：
$X' = X \cos\theta - Y \sin\theta$
$Y' = X \sin\theta + Y \cos\theta$

为了应用[雅可比方法](@entry_id:270947)，我们需要找到反变换，即用 $(x', y')$ 表示 $(x, y)$。这相当于将[坐标系](@entry_id:156346)顺时针旋转 $\theta$（或逆时针旋转 $-\theta$）：
$x = x' \cos\theta + y' \sin\theta$
$y = -x' \sin\theta + y' \cos\theta$

接下来，我们计算反变换的[雅可比矩阵](@entry_id:264467) $J$：
$J = \begin{pmatrix}
\frac{\partial x}{\partial x'}  \frac{\partial x}{\partial y'} \\
\frac{\partial y}{\partial x'}  \frac{\partial y}{\partial y'}
\end{pmatrix} = \begin{pmatrix}
\cos\theta  \sin\theta \\
-\sin\theta  \cos\theta
\end{pmatrix}$

其[行列式](@entry_id:142978)为 $\det(J) = \cos^2\theta - (-\sin^2\theta) = \cos^2\theta + \sin^2\theta = 1$。
这意味着[旋转变换](@entry_id:200017)是**保体积**的，其[雅可比行列式](@entry_id:137120)的[绝对值](@entry_id:147688)为1。

最后，我们将反变换代入原始PDF，并乘以[雅可比行列式](@entry_id:137120)的[绝对值](@entry_id:147688)：
$f_{X',Y'}(x',y') = f_{X,Y}(x(x',y'), y(x',y')) |\det(J)|$
指数项中的 $x^2+y^2$ 变为：
$x^2+y^2 = (x' \cos\theta + y' \sin\theta)^2 + (-x' \sin\theta + y' \cos\theta)^2$
展开后，交叉项 $2x'y'\cos\theta\sin\theta$ 相互抵消，得到：
$x^2+y^2 = (x'^2\cos^2\theta + y'^2\sin^2\theta) + (x'^2\sin^2\theta + y'^2\cos^2\theta) = x'^2(\cos^2\theta+\sin^2\theta) + y'^2(\sin^2\theta+\cos^2\theta) = x'^2+y'^2$
这个量在旋转下是不变的，它就是到原点距离的平方。因此，新的联合PDF为：
$f_{X',Y'}(x',y') = \frac{1}{2\pi}\exp\left(-\frac{x'^2+y'^2}{2}\right) \cdot 1$

结果表明，变换后的[随机变量](@entry_id:195330) $(X', Y')$ 与原始的 $(X, Y)$ 具有完全相同的联合分布！这从数学上证明了二维标准正态分布的**旋转对称性**。

### 重要应用：[坐标系](@entry_id:156346)变换与[随机数生成](@entry_id:138812)

[雅可比方法](@entry_id:270947)在不同[坐标系](@entry_id:156346)间的转换中扮演着核心角色，最著名的例子之一就是[笛卡尔坐标系](@entry_id:169789)与极[坐标系](@entry_id:156346)之间的转换。

#### 示例：[Box-Muller变换](@entry_id:139753)

如何从计算机容易生成的[均匀分布](@entry_id:194597)随机数，得到在模拟和[统计推断](@entry_id:172747)中至关重要的[正态分布](@entry_id:154414)随机数？**[Box-Muller变换](@entry_id:139753)**给出了一个绝妙的答案 [@problem_id:1926672]。该方法取两个独立的、服从 $(0, 1)$ 区间上[均匀分布](@entry_id:194597)的[随机变量](@entry_id:195330) $U_1$ 和 $U_2$，然后通过以下变换生成两个独立的标准正态[随机变量](@entry_id:195330) $X$ 和 $Y$：
$X = \sqrt{-2 \ln U_1} \cos(2\pi U_2)$
$Y = \sqrt{-2 \ln U_1} \sin(2\pi U_2)$

要证明这一点，我们可以反向操作。让我们定义极坐标变量 $R = \sqrt{X^2+Y^2}$ 和 $\Theta = \arctan(Y/X)$。上面的变换等价于：
$R = \sqrt{-2 \ln U_1} \implies U_1 = \exp(-R^2/2)$
$\Theta = 2\pi U_2 \implies U_2 = \Theta/(2\pi)$

我们现在从 $U_1, U_2$ 的简单[分布](@entry_id:182848)出发，推导 $X, Y$ 的[分布](@entry_id:182848)。首先求出中间变量 $(R, \Theta)$ 的联合分布。
由于 $U_1, U_2$ 独立，其联合PDF为 $f_{U_1,U_2}(u_1, u_2) = 1$ (在 $u_1, u_2 \in (0,1)$ 的单位正方形内)。
我们先求 $R$ 和 $\Theta$ 的PDF。对于 $r \ge 0$，$R$的CDF为：
$F_R(r) = P(R \le r) = P(\sqrt{-2 \ln U_1} \le r) = P(U_1 \ge \exp(-r^2/2)) = 1 - \exp(-r^2/2)$
其PDF为 $f_R(r) = \frac{dF_R(r)}{dr} = r \exp(-r^2/2)$，这是**[瑞利分布](@entry_id:184867) (Rayleigh distribution)**。
对于 $\theta \in [0, 2\pi)$，$\Theta = 2\pi U_2$ 是一个简单的线性伸缩，其PDF为 $f_\Theta(\theta) = \frac{1}{2\pi}$，即在 $[0, 2\pi)$ 上的[均匀分布](@entry_id:194597)。
由于 $R$ 和 $\Theta$ 分别只依赖于独立的 $U_1$ 和 $U_2$，所以它们也是[相互独立](@entry_id:273670)的。因此，它们的联合PDF为：
$f_{R,\Theta}(r,\theta) = f_R(r)f_\Theta(\theta) = \frac{r}{2\pi}\exp(-r^2/2)$

现在，我们进行从极坐标 $(R, \Theta)$ 到[笛卡尔坐标](@entry_id:167698) $(X, Y)$ 的标准变换：
$x = r \cos\theta, \quad y = r \sin\theta$
这个变换的雅可比行列式（注意这次是正向变换）的[绝对值](@entry_id:147688)是：
$|\det \begin{pmatrix} \frac{\partial x}{\partial r}  \frac{\partial x}{\partial \theta} \\ \frac{\partial y}{\partial r}  \frac{\partial y}{\partial \theta} \end{pmatrix}| = |\det \begin{pmatrix} \cos\theta  -r\sin\theta \\ \sin\theta  r\cos\theta \end{pmatrix}| = r$

根据多维变换公式的另一种形式，$f_{X,Y}(x,y) = f_{R,\Theta}(r(x,y), \theta(x,y)) \left| \frac{\partial(r,\theta)}{\partial(x,y)} \right| = \frac{f_{R,\Theta}(r,\theta)}{|\frac{\partial(x,y)}{\partial(r,\theta)}|}$，我们有：
$f_{X,Y}(x,y) = \frac{f_{R,\Theta}(r, \theta)}{r} = \frac{\frac{r}{2\pi}\exp(-r^2/2)}{r} = \frac{1}{2\pi}\exp(-r^2/2)$
将 $r^2 = x^2+y^2$ 代入，得到：
$f_{X,Y}(x,y) = \frac{1}{2\pi}\exp\left(-\frac{x^2+y^2}{2}\right) = \left(\frac{1}{\sqrt{2\pi}}\exp\left(-\frac{x^2}{2}\right)\right)\left(\frac{1}{\sqrt{2\pi}}\exp\left(-\frac{y^2}{2}\right)\right)$
这正是两个独立的标准正态分布[随机变量](@entry_id:195330)的联合PDF。

这个问题 [@problem_id:1313156] 则展示了逆过程。如果已知信号源的径向距离平方 $R^2$ 服从均值为2的指数分布（等价于 $R$ 服从[瑞利分布](@entry_id:184867)），且[到达角](@entry_id:265527) $\Theta$ 在 $[0, 2\pi]$ 上[均匀分布](@entry_id:194597)，那么通过同样的极坐标到笛卡尔坐标变换，可以证明其[笛卡尔坐标](@entry_id:167698) $(X,Y)$ 是两个独立的标准正态变量。

#### 推广至三维：球[坐标变换](@entry_id:172727)

[雅可比方法](@entry_id:270947)可以轻松推广到更高维度。例如，在三维空间中，我们经常使用[球坐标系](@entry_id:167517) $(R, \Theta, \Phi)$。考虑一个定位误差模型，其中沿三个正交轴的误差 $X, Y, Z$ [相互独立](@entry_id:273670)且均服从标准正态分布。我们可能对总误差的径向大小 $R = \sqrt{X^2+Y^2+Z^2}$ 更感兴趣 [@problem_id:1925824]。

$X, Y, Z$ 的联合PDF为 $f_{X,Y,Z}(x,y,z) = (2\pi)^{-3/2} \exp\left(-\frac{x^2+y^2+z^2}{2}\right)$。
球[坐标变换](@entry_id:172727)为：
$x = r\sin\theta\cos\phi$
$y = r\sin\theta\sin\phi$
$z = r\cos\theta$
这个变换的雅可比行列式[绝对值](@entry_id:147688)为 $|J| = r^2\sin\theta$。
变换后的联合PDF为：
$f_{R,\Theta,\Phi}(r,\theta,\phi) = f_{X,Y,Z}(x,y,z) |J| = (2\pi)^{-3/2} \exp\left(-\frac{r^2}{2}\right) r^2\sin\theta$
为了得到 $R$ 的边际PDF $f_R(r)$，我们需要对所有可能的角度进行积分：
$f_R(r) = \int_0^{2\pi} \int_0^\pi f_{R,\Theta,\Phi}(r,\theta,\phi) d\theta d\phi$
$f_R(r) = (2\pi)^{-3/2} r^2 \exp\left(-\frac{r^2}{2}\right) \int_0^{2\pi} d\phi \int_0^\pi \sin\theta d\theta$
由于 $\int_0^{2\pi} d\phi = 2\pi$ 且 $\int_0^\pi \sin\theta d\theta = 2$，积分结果为 $4\pi$。
$f_R(r) = (2\pi)^{-3/2} r^2 \exp\left(-\frac{r^2}{2}\right) (4\pi) = \sqrt{\frac{2}{\pi}} r^2 \exp\left(-\frac{r^2}{2}\right), \quad r \ge 0$
这就是**卡方分布 (Chi distribution)** 在自由度为3时的PDF。有了这个PDF，我们就可以计算总误差大小的[期望值](@entry_id:153208) $E[R]$ 或其他统计量了。

### 处理非[一对一变换](@entry_id:148028)：辅助变量法

[雅可比方法](@entry_id:270947)要求变换是可逆的（一对一）。但很多情况下，我们关心的变换并非如此，例如，我们可能想求 $Z=g(X,Y)$ 的[分布](@entry_id:182848)，这是一个从二维到一维的映射。在这种情况下，我们可以引入一个**辅助变量**来构造一个可逆的二维到二维的变换。

一个常见的辅助[变量选择](@entry_id:177971)是 $W=X$ 或 $W=Y$。然后，我们应用[雅可比方法](@entry_id:270947)求出 $(Z,W)$ 的联合PDF，最后通[过积分](@entry_id:753033)消去辅助变量 $W$，得到 $Z$ 的边际PDF。

#### 示例：指数分布[随机变量](@entry_id:195330)之比

假设两个独立电子元件的寿命 $X$ 和 $Y$ 均服从参数为 $\lambda$ 的指数分布，即 $f(t) = \lambda \exp(-\lambda t)$ for $t > 0$。我们想要求出它们寿命之比 $Z = X/Y$ 的[分布](@entry_id:182848) [@problem_id:1925843]。

1.  **引入辅助变量**：这是一个从 $(X,Y)$ 到 $Z$ 的多对一变换。我们引入一个辅助变量，例如 $W=Y$，来构造一个从 $(X,Y)$ 到 $(Z,W)$ 的可逆变换。
    $Z = X/Y$
    $W = Y$

2.  **求反变换**：从 $(Z,W)$ 解出 $(X,Y)$：
    $Y = W$
    $X = ZY = ZW$

3.  **计算[雅可比行列式](@entry_id:137120)**：反变换的雅可比矩阵为：
    $J = \begin{pmatrix} \frac{\partial x}{\partial z}  \frac{\partial x}{\partial w} \\ \frac{\partial y}{\partial z}  \frac{\partial y}{\partial w} \end{pmatrix} = \begin{pmatrix} w  z \\ 0  1 \end{pmatrix}$
    其[行列式](@entry_id:142978)为 $\det(J) = w$。

4.  **应用变换公式**：$X$ 和 $Y$ 的联合PDF为 $f_{X,Y}(x,y) = \lambda^2 \exp(-\lambda(x+y))$ (因独立性)。
    $(Z,W)$ 的联合PDF为：
    $f_{Z,W}(z,w) = f_{X,Y}(zw, w) |\det(J)| = \lambda^2 \exp(-\lambda(zw+w)) \cdot |w|$
    由于 $X,Y > 0$，所以 $Z,W > 0$，因此 $|w|=w$。
    $f_{Z,W}(z,w) = \lambda^2 w \exp(-\lambda w(1+z))$，定义域为 $z>0, w>0$。

5.  **求[边际[分](@entry_id:264862)布](@entry_id:182848)**：为了得到 $Z$ 的PDF，我们对 $w$ 进行积分：
    $f_Z(z) = \int_0^\infty f_{Z,W}(z,w) dw = \int_0^\infty \lambda^2 w \exp(-\lambda(1+z)w) dw$
    这是一个Gamma积分。令 $a = \lambda(1+z)$，积分变为 $\lambda^2 \int_0^\infty w \exp(-aw) dw$。利用 $\int_0^\infty t \exp(-at) dt = 1/a^2$，我们得到：
    $f_Z(z) = \lambda^2 \cdot \frac{1}{(\lambda(1+z))^2} = \frac{1}{(1+z)^2}$，对于 $z>0$。

这个结果非常简洁，并且不依赖于参数 $\lambda$。这个[分布](@entry_id:182848)被称为 F [分布](@entry_id:182848)的一种特殊形式 ($F(2,2)$)。对于两个独立[均匀分布](@entry_id:194597)变量的差的[绝对值](@entry_id:147688) [@problem_id:1313153]，也可以使用这种辅助变量法，或者采用更直接的几何法或卷积法，最终会得到一个三角分布。

### 高等应用：[矩阵空间](@entry_id:261335)的变换

[雅可比方法](@entry_id:270947)的原理非常深刻，可以从[向量空间](@entry_id:151108)推广到更抽象的数学对象，例如[矩阵空间](@entry_id:261335)。在[随机矩阵理论](@entry_id:142253)等前沿领域，理解[随机矩阵](@entry_id:269622)分解（如[特征值分解](@entry_id:272091)或[奇异值分解](@entry_id:138057)）后各个组成部分的[联合分布](@entry_id:263960)是核心问题。

例如，考虑一个 $2 \times 2$ 随机矩阵 $X$，其四个元素是独立的标准正态[随机变量](@entry_id:195330)。我们可以对其进行[奇异值分解 (SVD)](@entry_id:172448) $X = U \Sigma V^T$，其中 $U$ 和 $V$ 是旋转矩阵（可由角度 $\theta_U, \theta_V$ 参数化），$\Sigma$ 是由奇异值 $\sigma_1 \ge \sigma_2 \ge 0$ 构成的[对角矩阵](@entry_id:637782) [@problem_id:1925814]。

这个分解定义了一个从4个矩阵元素 $(x_{11}, x_{12}, x_{21}, x_{22})$ 到4个SVD参数 $(\sigma_1, \sigma_2, \theta_U, \theta_V)$ 的复杂变换。通过运用微分形式计算相应的[雅可比行列式](@entry_id:137120)，可以证明其值为 $(\sigma_1^2 - \sigma_2^2)$。由于原始正态分布的密度函数在正交变换下具有不变性（即 $\operatorname{tr}(X^T X) = \sigma_1^2+\sigma_2^2$），我们可以直接写出SVD参数的联合PDF：
$f(\sigma_1, \sigma_2, \theta_U, \theta_V) \propto (\sigma_1^2 - \sigma_2^2) \exp\left(-\frac{\sigma_1^2+\sigma_2^2}{2}\right)$
其中，$\propto$ 表示正比于。经过归一化后，其精确形式为：
$f(\sigma_1, \sigma_2, \theta_U, \theta_V) = (2\pi)^{-2} (\sigma_1^2 - \sigma_2^2) \exp\left(-\frac{\sigma_1^2+\sigma_2^2}{2}\right)$
这个结果揭示了奇异值之间存在一种“排斥”效应（由因子 $\sigma_1^2 - \sigma_2^2$ 体现，当 $\sigma_1$ 接近 $\sigma_2$ 时密度趋于0），而角度是[均匀分布](@entry_id:194597)的。这展示了[雅可比方法](@entry_id:270947)在解决现代科学研究中的复杂[分布](@entry_id:182848)问题时的强大威力。

总结而言，[雅可比方法](@entry_id:270947)为我们提供了一套将一个[随机变量](@entry_id:195330)（或向量）的[概率分布](@entry_id:146404)信息“传递”给其[函数变换](@entry_id:141095)后新变量的系统性工具。其核心在于通过[雅可比行列式](@entry_id:137120)来量化和校正局部空间体积的变化，从而确保[概率守恒](@entry_id:149166)。从简单的单变量函数到复杂的多维[矩阵分解](@entry_id:139760)，这一原理贯穿始终，是概率论与统计学中不可或缺的基石。