## 引言
在科学与工程的众多领域中，我们常常需要理解系统各部分之间的复杂关系。一个核心问题是：如果我们知道一组输入[随机变量](@entry_id:195330)的统计特性，我们如何预测由这些变量经过某个[函数变换](@entry_id:141095)后得到的输出结果的统计特性？例如，物理学家可能想从[粒子速度](@entry_id:196946)分量的[分布](@entry_id:182848)推断其动能的[分布](@entry_id:182848)，而金融分析师则希望从单个资产的回报率[分布](@entry_id:182848)预测整个投资组合的风险。这个问题引出了[随机变量变换](@entry_id:164667)这一核心概念，而[雅可比方法](@entry_id:270947)（Jacobian Method）正是解决这一问题的最强大和通用的工具。本文旨在系统地介绍[雅可比方法](@entry_id:270947)，解决从已知[分布](@entry_id:182848)推导未知函数[分布](@entry_id:182848)这一知识缺口。

本文将分为三个部分，引领您全面掌握这一方法。在“原理与机制”一章中，我们将从最简单的单变量变换入手，逐步推广到复杂的多变量情形，并深入探讨雅可比[行列式的几何意义](@entry_id:200059)。接着，在“应用与跨学科联系”一章中，我们将展示该方法如何在统计学、信号处理、物理学乃至[计算机视觉](@entry_id:138301)等不同学科中解决实际问题。最后，通过“动手实践”部分，您将有机会通过具体的练习来巩固和应用所学知识，将理论转化为解决问题的能力。

## 原理与机制

在概率论和统计学的研究中，我们经常面临一个核心问题：如果我们知道一个或多个[随机变量](@entry_id:195330)的[概率分布](@entry_id:146404)，那么这些变量的某个函数所构成的新的[随机变量](@entry_id:195330)，其[概率分布](@entry_id:146404)是怎样的？例如，在物理学中，我们可能知道[粒子速度](@entry_id:196946)分量的[分布](@entry_id:182848)，并希望了解其动能的[分布](@entry_id:182848)。在经济学中，我们可能对单个资产的回报率[分布](@entry_id:182848)有模型，但更关心的是由这些资产构成的投资组合的总回报率[分布](@entry_id:182848)。解答这类问题的过程被称为[随机变量的变换](@entry_id:267283)。本章将系统地介绍求解该问题的核心工具——[雅可比方法](@entry_id:270947)（Jacobian Method）。

### 单变量情形：一个基础

我们从最简单的情形开始，即一个[随机变量的函数](@entry_id:271583)。假设我们有[连续随机变量](@entry_id:166541) $X$，其概率密度函数（PDF）为 $f_X(x)$。我们感兴趣的是另一个[随机变量](@entry_id:195330) $Y = g(X)$ 的[概率密度函数](@entry_id:140610) $f_Y(y)$，其中 $g$ 是一个已知的函数。

其基本思想是**[概率守恒](@entry_id:149166)**：一个落在极小区间 $(x, x+dx)$ 内的事件，其概率为 $f_X(x)dx$。经过变换 $g$ 后，这个事件对应于 $Y$ 落在一个相应的区间内，其概率必须相等。

#### 单调变换

最直接的情况是当函数 $g(x)$ 是严格单调（严格递增或递减）且可微时。在这种情况下，$x$ 和 $y$ 之间存在一一对应的关系。我们可以通过 $x = g^{-1}(y)$ 找到唯一的逆变换。

[概率守恒](@entry_id:149166)的原则可以表示为：

$|f_Y(y) dy| = |f_X(x) dx|$

由此，我们可以得到 $Y$ 的[概率密度函数](@entry_id:140610)：

$f_Y(y) = f_X(x) \left| \frac{dx}{dy} \right| = f_X(g^{-1}(y)) \left| \frac{d}{dy}g^{-1}(y) \right|$

这里的 $\left| \frac{dx}{dy} \right|$ 是一个伸缩因子，它说明了从 $x$ 坐标到 $y$ 坐标的映射如何拉伸或压缩[概率密度](@entry_id:175496)。

让我们通过一个具体的工程应用来理解这个过程。在半导体制造中，晶圆的质量控制是一个关键环节。假设由于工艺波动，生产出的圆形晶圆的半径 $R$ 是一个[随机变量](@entry_id:195330)，遵循参数为 $\lambda$ 的[指数分布](@entry_id:273894)，其PDF为 $f_R(r) = \lambda \exp(-\lambda r)$，其中 $r \ge 0$。然而，质量控制部门更关心的是晶圆的面积 $A = \pi R^2$。如何确定面积 $A$ 的概率密度函数 $f_A(a)$？[@problem_id:1313171]

这是一个典型的单调变换问题。对于 $r \gt 0$，$a = g(r) = \pi r^2$ 是一个严格递增函数。

1.  **找出值域**：因为 $R \ge 0$，所以 $A \ge 0$。
2.  **求逆变换**：从 $a = \pi r^2$ 中解出 $r$，得到 $r = g^{-1}(a) = \sqrt{\frac{a}{\pi}}$。
3.  **计算导数**：计算逆[变换的导数](@entry_id:164838)：$\frac{dr}{da} = \frac{d}{da}\sqrt{\frac{a}{\pi}} = \frac{1}{\sqrt{\pi}} \cdot \frac{1}{2\sqrt{a}} = \frac{1}{2\sqrt{\pi a}}$。
4.  **代入公式**：将这些结果代入变换公式：
    $f_A(a) = f_R(g^{-1}(a)) \left| \frac{dr}{da} \right| = f_R\left(\sqrt{\frac{a}{\pi}}\right) \cdot \frac{1}{2\sqrt{\pi a}}$
    
    将 $f_R(r)$ 的表达式代入，得到：
    $f_A(a) = \lambda \exp\left(-\lambda \sqrt{\frac{a}{\pi}}\right) \cdot \frac{1}{2\sqrt{\pi a}} = \frac{\lambda}{2\sqrt{\pi a}} \exp\left(-\lambda \sqrt{\frac{a}{\pi}}\right)$
    
    这个结果给出了对于任意 $a \gt 0$，面积 $A$ 的概率密度。通过这个过程，我们成功地将关于半径的统计知识转化为了关于面积的统计知识。

#### 非单调（多对一）变换

当变换函数 $g(x)$ 不是单调时，情况会变得复杂一些。对于一个给定的 $y$ 值，可能存在多个 $x$ 值（比如 $x_1, x_2, \dots, x_k$）使得 $g(x_i) = y$。这被称为多对一变换。

在这种情况下，落入 $y$ 附近小区间 $dy$ 的总概率是所有这些 $x_i$ 附近小区间 $dx_i$ 贡献的概率之和。因此，我们需要对每个[逆变](@entry_id:192290)换分支的贡献进行求和。

假设对于一个 $y$ 值，存在 $k$ 个解 $x_1(y), x_2(y), \dots, x_k(y)$，那么 $Y$ 的[概率密度函数](@entry_id:140610)为：

$f_Y(y) = \sum_{i=1}^{k} f_X(x_i(y)) \left| \frac{d}{dy}x_i(y) \right|$

这个公式是单调变换公式的自然推广。

考虑一个电子工程中的例子。一个[对数放大器](@entry_id:262927)的输入是一个随机噪声电压 $V_{in}$，其遵循均值为 $0$、标准差为 $\sigma$ 的正态分布，即 $V_{in} \sim \mathcal{N}(0, \sigma^2)$。放大器的输出 $V_{out}$ 由输入电压的[绝对值](@entry_id:147688)的自然对数给出：$V_{out} = \ln(|V_{in}|)$。我们希望找到输出电压 $V_{out}$ 的[概率密度函数](@entry_id:140610)。[@problem_id:1313169]

这是一个典型的多对一（二对一）变换。令 $X = V_{in}$，$Y = V_{out}$。变换函数是 $y = g(x) = \ln(|x|)$。

1.  **求[逆变](@entry_id:192290)换**：对于任意给定的 $y$ 值（可以为正或负），我们试图求解 $x$。方程 $y = \ln(|x|)$ 意味着 $|x| = \exp(y)$。这给出了两个解：
    $x_1(y) = \exp(y)$
    $x_2(y) = -\exp(y)$
2.  **计算导数**：分别计算这两个逆变换分支的导数：
    $\frac{dx_1}{dy} = \exp(y)$
    $\frac{dx_2}{dy} = -\exp(y)$
    它们的[绝对值](@entry_id:147688)都是 $|\exp(y)| = \exp(y)$ （因为 $\exp(y) > 0$）。
3.  **代入公式**：应用多对一变换公式：
    $f_Y(y) = f_X(x_1(y)) \left| \frac{dx_1}{dy} \right| + f_X(x_2(y)) \left| \frac{dx_2}{dy} \right|$
    
    由于 $X$ 的PDF $f_X(x) = \frac{1}{\sqrt{2\pi}\sigma} \exp\left(-\frac{x^2}{2\sigma^2}\right)$ 是一个[偶函数](@entry_id:163605)（即 $f_X(x) = f_X(-x)$），我们有 $f_X(\exp(y)) = f_X(-\exp(y))$。因此，
    
    $f_Y(y) = 2 \cdot f_X(\exp(y)) \cdot \exp(y)$
    
    将 $f_X(x)$ 的表达式代入，并令 $x=\exp(y)$：
    
    $f_Y(y) = 2 \cdot \frac{1}{\sqrt{2\pi}\sigma} \exp\left(-\frac{(\exp(y))^2}{2\sigma^2}\right) \cdot \exp(y) = \frac{2}{\sqrt{2\pi}\sigma} \exp\left(y - \frac{\exp(2y)}{2\sigma^2}\right)$
    
    这个结果描述了[对数放大器](@entry_id:262927)输出电压的完整统计特性，它对于所有实数 $y$ 都有效。

### 多变量情形：[雅可比方法](@entry_id:270947)

现在我们将讨论从一个 $n$ 维随机向量 $\mathbf{X} = (X_1, \dots, X_n)$ 到另一个 $n$ 维随机向量 $\mathbf{Y} = (Y_1, \dots, Y_n)$ 的变换。设变换关系为 $\mathbf{Y} = \mathbf{g}(\mathbf{X})$，即：

$Y_1 = g_1(X_1, \dots, X_n)$
$Y_2 = g_2(X_1, \dots, X_n)$
...
$Y_n = g_n(X_1, \dots, X_n)$

我们假设这个变换是可逆的，即我们可以唯一地解出 $\mathbf{X}$，得到逆变换 $\mathbf{X} = \mathbf{g}^{-1}(\mathbf{Y})$：

$X_1 = h_1(Y_1, \dots, Y_n)$
$X_2 = h_2(Y_1, \dots, Y_n)$
...
$X_n = h_n(Y_1, \dots, Y_n)$

#### 雅可比行列式：几何缩放因子

在单变量情况下，导数的[绝对值](@entry_id:147688) $\left| \frac{dx}{dy} \right|$ 衡量了长度的缩放。在多变量情况下，这个角色由一个称为**雅可比行列式**（Jacobian determinant）的量来扮演。雅可比矩阵 $J$ 是[逆变](@entry_id:192290)换 $\mathbf{X} = \mathbf{h}(\mathbf{Y})$ 中所有偏导数构成的矩阵：

$J = \begin{pmatrix}
\frac{\partial x_1}{\partial y_1}  \frac{\partial x_1}{\partial y_2}  \cdots  \frac{\partial x_1}{\partial y_n} \\
\frac{\partial x_2}{\partial y_1}  \frac{\partial x_2}{\partial y_2}  \cdots  \frac{\partial x_2}{\partial y_n} \\
\vdots  \vdots  \ddots  \vdots \\
\frac{\partial x_n}{\partial y_1}  \frac{\partial x_n}{\partial y_2}  \cdots  \frac{\partial x_n}{\partial y_n}
\end{pmatrix}$

[雅可比行列式](@entry_id:137120)的[绝对值](@entry_id:147688) $|\det(J)|$ 描述了从 $\mathbf{Y}$ 空间中的一个微小[体积元](@entry_id:267802) $d\mathbf{y} = dy_1 \cdots dy_n$ 映射回 $\mathbf{X}$ 空间中对应体积元 $d\mathbf{x} = dx_1 \cdots dx_n$ 时的[体积缩放](@entry_id:197908)比例。即 $d\mathbf{x} = |\det(J)| d\mathbf{y}$。

利用[概率守恒](@entry_id:149166)原则 $f_\mathbf{Y}(\mathbf{y})d\mathbf{y} = f_\mathbf{X}(\mathbf{x})d\mathbf{x}$，我们得到多变量变换的通用公式：

$f_\mathbf{Y}(\mathbf{y}) = f_\mathbf{X}(\mathbf{g}^{-1}(\mathbf{y})) |\det(J)|$

这就是著名的[雅可比方法](@entry_id:270947)。

#### 线性变换

[线性变换](@entry_id:149133)是多变量变换中最简单也最常见的一种。假设变换为 $\mathbf{Y} = A\mathbf{X}$，其中 $A$ 是一个可逆的 $n \times n$ 矩阵。那么[逆变](@entry_id:192290)换是 $\mathbf{X} = A^{-1}\mathbf{Y}$。

在这种情况下，[雅可比矩阵](@entry_id:264467)就是常数矩阵 $J = A^{-1}$。因此，雅可比行列式的[绝对值](@entry_id:147688)为 $|\det(A^{-1})| = \frac{1}{|\det(A)|}$。变换公式变为：

$f_\mathbf{Y}(\mathbf{y}) = f_\mathbf{X}(A^{-1}\mathbf{y}) \frac{1}{|\det(A)|}$

在信号处理中，我们经常遇到对信号进行[线性组合](@entry_id:154743)的情况。例如，假设两个独立的标准正态噪声源 $X$ 和 $Y$（即 $X, Y \sim \mathcal{N}(0,1)$），我们测量到两个量 $U=X$ 和 $V=aX+bY$，其中 $a,b$ 为非零常数。我们想求 $(U,V)$ 的[联合概率密度函数](@entry_id:267139) $f_{U,V}(u,v)$。[@problem_id:1313172]

这里的变换是 $\begin{pmatrix} U \\ V \end{pmatrix} = \begin{pmatrix} 1  0 \\ a  b \end{pmatrix} \begin{pmatrix} X \\ Y \end{pmatrix}$。这是一个[线性变换](@entry_id:149133)。

1.  **求逆变换**：解出 $(X,Y)$，得到 $X = U$ 和 $Y = \frac{V-aU}{b}$。
2.  **计算[雅可比行列式](@entry_id:137120)**：[逆变](@entry_id:192290)换的雅可比矩阵为：
    $J = \begin{pmatrix} \frac{\partial x}{\partial u}  \frac{\partial x}{\partial v} \\ \frac{\partial y}{\partial u}  \frac{\partial y}{\partial v} \end{pmatrix} = \begin{pmatrix} 1  0 \\ -a/b  1/b \end{pmatrix}$
    其[行列式](@entry_id:142978)为 $\det(J) = 1 \cdot \frac{1}{b} - 0 \cdot (-\frac{a}{b}) = \frac{1}{b}$。[绝对值](@entry_id:147688)为 $|\det(J)| = \frac{1}{|b|}$。
3.  **代入公式**：由于 $X, Y$ 独立且服从[标准正态分布](@entry_id:184509)，它们的联合PDF为 $f_{X,Y}(x,y) = f_X(x)f_Y(y) = \frac{1}{2\pi} \exp\left(-\frac{x^2+y^2}{2}\right)$。
    将 $x=u$ 和 $y=(v-au)/b$ 代入，得到 $f_{U,V}(u,v)$:
    $f_{U,V}(u,v) = f_{X,Y}\left(u, \frac{v-au}{b}\right) \left|\frac{1}{b}\right| = \frac{1}{2\pi|b|} \exp\left(-\frac{1}{2}\left[u^2 + \left(\frac{v-au}{b}\right)^2\right]\right)$
    
    这个结果是 $(U,V)$ 的[联合正态分布](@entry_id:272692)的密度函数。从这个联合密度，我们可以进一步推导出条件密度 $f_{V|U}(v|u)$，它将是一个均值为 $au$、[方差](@entry_id:200758)为 $b^2$ 的正态分布。

#### [坐标系](@entry_id:156346)变换

[雅可比方法](@entry_id:270947)在不同[坐标系](@entry_id:156346)之间转换[随机变量](@entry_id:195330)时特别有用，例如在笛卡尔坐标系和极坐标/球坐标系之间。

一个非常优雅的例子是二维标准正态分布的[旋转不变性](@entry_id:137644)。假设一个粒子在二维平面上的位置 $(X,Y)$ 受噪声影响，其坐标 $X$ 和 $Y$ 是两个独立的标准正态[随机变量](@entry_id:195330)。现在我们将[坐标系](@entry_id:156346)逆时针旋转一个角度 $\theta$，得到新的坐标 $(X', Y')$。它们的关系是：
$X' = X \cos\theta - Y \sin\theta$
$Y' = X \sin\theta + Y \cos\theta$
新的坐标 $(X', Y')$ 的[联合分布](@entry_id:263960)是什么？[@problem_id:1313200]

1.  **求逆变换**：将 $(X', Y')$ 的表达式看作关于 $(X, Y)$ 的线性方程组，解得：
    $X = X' \cos\theta + Y' \sin\theta$
    $Y = -X' \sin\theta + Y' \cos\theta$
2.  **计算雅可比行列式**：逆变换的雅可比矩阵为：
    $J = \begin{pmatrix} \cos\theta  \sin\theta \\ -\sin\theta  \cos\theta \end{pmatrix}$
    其[行列式](@entry_id:142978)为 $\det(J) = \cos^2\theta - (-\sin^2\theta) = \cos^2\theta + \sin^2\theta = 1$。
3.  **代入公式**：原始的联合PDF为 $f_{X,Y}(x,y) = \frac{1}{2\pi} \exp\left(-\frac{x^2+y^2}{2}\right)$。我们需要计算 $x^2+y^2$ 用 $x', y'$ 表示的形式。
    $x^2+y^2 = (x'\cos\theta + y'\sin\theta)^2 + (-x'\sin\theta + y'\cos\theta)^2 = (x'^2\cos^2\theta + y'^2\sin^2\theta) + (x'^2\sin^2\theta + y'^2\cos^2\theta) = x'^2+y'^2$。
    
    因此，新的联合PDF为：
    $f_{X',Y'}(x',y') = f_{X,Y}(x(x',y'), y(x',y')) \cdot |\det(J)| = \frac{1}{2\pi} \exp\left(-\frac{x'^2+y'^2}{2}\right) \cdot 1$
    
    我们发现 $f_{X',Y'}(x',y')$ 与 $f_{X,Y}(x,y)$ 具有完全相同的形式。这表明，二维[标准正态分布](@entry_id:184509)在旋转下是不变的，这是一个深刻且有用的性质。

另一个基本变换是从极坐标到笛卡尔坐标。假设我们知道一个点的极坐标 $(R, \Theta)$ 的[分布](@entry_id:182848)，并想求其[笛卡尔坐标](@entry_id:167698) $(X, Y)$ 的[分布](@entry_id:182848)。设 $X = R\cos\Theta$，$Y = R\sin\Theta$。例如，在一个[信号检测](@entry_id:263125)模型中，信号源的径向距离的平方 $U=R^2$ 服从均值为2的[指数分布](@entry_id:273894)，而[到达角](@entry_id:265527) $\Theta$ 在 $[0, 2\pi]$ 上[均匀分布](@entry_id:194597)，且两者独立。求 $(X,Y)$ 的联合PDF。[@problem_id:1313156]

首先，我们需要从 $U=R^2$ 和 $\Theta$ 的[分布](@entry_id:182848)得到 $(R, \Theta)$ 的[联合分布](@entry_id:263960)。$R=\sqrt{U}$ 是一个单调变换，我们可以求得 $R$ 的PDF为 $f_R(r) = r \exp(-r^2/2)$（这是一个[瑞利分布](@entry_id:184867)）。由于 $R$ 和 $\Theta$ 独立，它们的联合PDF为 $f_{R,\Theta}(r,\theta) = f_R(r)f_\Theta(\theta) = \frac{r}{2\pi}\exp(-r^2/2)$。

现在我们从 $(R, \Theta)$ 变换到 $(X, Y)$。这次变换方向是从 $(R,\Theta)$ 到 $(X,Y)$，所以我们需要计算这个“正向”变换的[雅可比行列式](@entry_id:137120)，然后用其倒数。

$J' = \begin{pmatrix} \frac{\partial x}{\partial r}  \frac{\partial x}{\partial \theta} \\ \frac{\partial y}{\partial r}  \frac{\partial y}{\partial \theta} \end{pmatrix} = \begin{pmatrix} \cos\theta  -r\sin\theta \\ \sin\theta  r\cos\theta \end{pmatrix}$

$\det(J') = r\cos^2\theta - (-r\sin^2\theta) = r$。根据多变量变换公式（使用正向变换的[雅可比行列式](@entry_id:137120)时，公式为 $f_{X,Y}(x,y) = f_{R,\Theta}(r(x,y), \theta(x,y)) \frac{1}{|\det(J')|}$），我们有：

$f_{X,Y}(x,y) = f_{R,\Theta}(r, \theta) \frac{1}{|r|} = \frac{\frac{r}{2\pi}\exp(-r^2/2)}{r} = \frac{1}{2\pi}\exp(-r^2/2)$

将 $r^2=x^2+y^2$ 代入，我们得到 $f_{X,Y}(x,y) = \frac{1}{2\pi}\exp\left(-\frac{x^2+y^2}{2}\right)$。这正是两个独立的标准正态变量的联合PDF。这个例子揭示了一个深刻的联系：一个[瑞利分布](@entry_id:184867)的幅度和一个[均匀分布](@entry_id:194597)的相位可以合成为一个二维高斯分布。

这个思想可以推广到三维。如果一个微型机械臂的定位误差在三个正交轴 $X,Y,Z$ 上的分量是独立的标准正态[随机变量](@entry_id:195330)，我们可以通过变换到[球坐标](@entry_id:146054) $(R, \Theta, \Phi)$ 来分析总[误差幅度](@entry_id:169950) $R = \sqrt{X^2+Y^2+Z^2}$ 的[分布](@entry_id:182848)。通过计算3D雅可比行列式（其值为 $r^2\sin\theta$），可以推导出 $R$ 的[概率密度函数](@entry_id:140610)，并计算其[期望值](@entry_id:153208)等统计量。[@problem_id:1925824]

### 高等应用与技巧

[雅可比方法](@entry_id:270947)不仅用于分析现有变量的函数，还被广泛用于从已知[分布](@entry_id:182848)（如[均匀分布](@entry_id:194597)）生成具有特定复杂[分布](@entry_id:182848)的随机数，这是[蒙特卡洛模拟](@entry_id:193493)等计算方法的基石。

#### [随机变量](@entry_id:195330)的生成

一个著名的例子是**[Box-Muller变换](@entry_id:139753)**。该方法能够从两个独立的标准[均匀分布](@entry_id:194597)[随机数生成](@entry_id:138812)两个独立的标准正态分布随机数。一个相关的变换考虑一个在[单位圆盘](@entry_id:172324) $\left\{(v_1, v_2) | v_1^2+v_2^2 \lt 1\right\}$ 内[均匀分布](@entry_id:194597)的随机向量 $(V_1, V_2)$。通过以下变换：

$X_1 = V_1 \sqrt{\frac{-2 \ln(S)}{S}}$, $X_2 = V_2 \sqrt{\frac{-2 \ln(S)}{S}}$，其中 $S = V_1^2+V_2^2$

我们可以证明，得到的[随机变量](@entry_id:195330) $(X_1, X_2)$ 是两个独立的标准正态变量。[@problem_id:1925835] 证明过程涉及一系列巧妙的变量代换（从笛卡尔坐标 $(V_1, V_2)$ 到极坐标 $(R, \Phi)$，再到 $(S, \Phi)$，最后到 $(X_1, X_2)$），每一步都应用了[雅可比方法](@entry_id:270947)，最终揭示了[均匀分布](@entry_id:194597)与正态分布之间的深刻联系。最终结果 $f_{X_1,X_2}(x_1,x_2) = \frac{1}{2\pi}\exp\left(-\frac{x_1^2+x_2^2}{2}\right)$ 再次证实了这一点。

#### 处理非标准变换

[雅可比方法](@entry_id:270947)的核心要求变换函数是可微的。然而，对于一些非标准函数，如 $\min$, $\max$ 或[绝对值](@entry_id:147688)，我们可以通过将定义[域划分](@entry_id:748628)为若干个区域来应用该方法，在每个区域内变换是可微且一一对应的。

例如，考虑两个独立的[指数分布](@entry_id:273894)[随机变量](@entry_id:195330) $X \sim \text{Exp}(\lambda_1)$ 和 $Y \sim \text{Exp}(\lambda_2)$。我们定义新的变量 $U = \min(X, Y)$ 和 $V = X$。我们想求 $(U,V)$ 的联合PDF。[@problem_id:1925825]

这里的变换函数 $(u,v) = (\min(x,y), x)$ 依赖于 $x$ 和 $y$ 的大小关系。
1.  **区域1: $y  x$**。在此区域，$\min(X,Y)=Y$。变换为 $U=Y, V=X$。这是一个简单的变量交换。其逆变换为 $X=V, Y=U$。雅可比行列式的[绝对值](@entry_id:147688)为1。此变换将区域 $\{(x,y)|0 \lt y \lt x\}$ 映射到区域 $\{(u,v)|0 \lt u \lt v\}$。
2.  **区域2: $x \le y$**。在此区域，$\min(X,Y)=X$。变换为 $U=X, V=X$。这意味着 $U=V$。在这种情况下，二维的[概率密度](@entry_id:175496)会坍缩到一条直线上，形成一个[混合分布](@entry_id:276506)（一部分是连续的，一部分是离散的）。

对于题目中要求的 $u \lt v$ 的区域，我们只需要考虑区域1。在该区域内应用[雅可比方法](@entry_id:270947)：
$f_{U,V}(u,v) = f_{X,Y}(x(u,v), y(u,v)) |J| = f_{X,Y}(v,u) \cdot 1$
由于 $X,Y$ 独立， $f_{X,Y}(x,y) = \lambda_1\exp(-\lambda_1x) \cdot \lambda_2\exp(-\lambda_2y)$。
因此，对于 $0 \lt u \lt v$：
$f_{U,V}(u,v) = \lambda_1\lambda_2 \exp(-\lambda_1v - \lambda_2u)$

这种分区域处理的策略极大地扩展了[雅可比方法](@entry_id:270947)的适用范围，使其能够处理包含逻辑判断和非光滑操作的复杂变换。

总而言之，从简单的单变量函数到复杂的多维坐标变换，[雅可比方法](@entry_id:270947)为我们提供了一个统一而强大的框架，用于推导变换后[随机变量](@entry_id:195330)的[分布](@entry_id:182848)。其核心在于通过雅可比行列式来量化局部空间的缩放，从而确保概率在变换前后保持守恒。掌握这一方法对于任何需要进行[概率建模](@entry_id:168598)和数据分析的领域都至关重要。