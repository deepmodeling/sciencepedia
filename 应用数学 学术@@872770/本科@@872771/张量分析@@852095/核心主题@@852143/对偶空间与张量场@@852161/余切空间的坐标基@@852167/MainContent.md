## 引言
在探索光滑流形的几何结构时，我们首先会遇到[切空间](@entry_id:199137)的概念，它描述了在某一点所有可能的速度方向。然而，这只故事的一半。一个同样深刻的问题是：我们如何“度量”或“评估”这些[速度矢量](@entry_id:269648)？这个问题的答案将我们引向一个对偶的世界——[余切空间](@entry_id:270516)（cotangent space）。[余切空间](@entry_id:270516)由作用于切矢量并产生标量的线性函数（称为[1-形式](@entry_id:270392)或[余矢量](@entry_id:157727)）构成，它为我们提供了一种不依赖于坐标选择的、描述物理和几何量的强大语言。然而，尽管其定义抽象，理解其具体结构，特别是其[坐标基](@entry_id:270149)，是掌握[张量分析](@entry_id:161423)并将其应用于实际问题的关键。

本文旨在系统地阐明[余切空间](@entry_id:270516)[坐标基](@entry_id:270149)的理论与实践。我们将从三个层面逐步深入：
- 在 **“原理与机制”** 一章中，我们将建立[余切空间](@entry_id:270516)[坐标基](@entry_id:270149)的数学基础，详细阐释其定义、与切空间基的对偶关系、分量计算方法以及在坐标变换下的行为。
- 接着，在 **“应用与跨学科联系”** 一章中，我们将展示这些抽象概念如何在物理学（如[电磁场](@entry_id:265881)、哈密顿力学）、几何学（如[子流形](@entry_id:159439)、黎曼度量）和[热力学](@entry_id:141121)等多个领域中找到具体的应用和深刻的体现。
- 最后，**“动手实践”** 部分将通过具体计算题，引导读者亲手应用所学知识，巩固对[1-形式](@entry_id:270392)的计算和几何直觉的理解。

通过本次学习，读者将能够从根本上理解什么是[1-形式](@entry_id:270392)，并熟练地在不同[坐标系](@entry_id:156346)下使用它们，为进一步学习更高级的微分几何和理论物理打下坚实的基础。

## 原理与机制

在理解了[流形](@entry_id:153038)上某一点的切空间作为所有可能[速度矢量](@entry_id:269648)的集合后，我们自然会引出一个对偶的概念：如何“度量”这些矢量？这便引导我们进入[余切空间](@entry_id:270516)（cotangent space）的领域。[余切空间](@entry_id:270516)是[切空间](@entry_id:199137)的[对偶空间](@entry_id:146945)，其元素——[余矢量](@entry_id:157727)（covectors）或称为1-形式（one-forms）——是作用于切矢量并产生标量的线性映射。本章将深入探讨[余切空间](@entry_id:270516)的结构，特别是其[坐标基](@entry_id:270149)的定义、性质与变换规律。

### [余切空间](@entry_id:270516)与[余矢量](@entry_id:157727)的基本概念

在[流形](@entry_id:153038) $M$ 上的某一点 $p$，其切空间 $T_p M$ 是一个[向量空间](@entry_id:151108)。一个在点 $p$ 的**余矢量** $\omega$ 是一个从 $T_p M$ 到实数集 $\mathbb{R}$ 的[线性映射](@entry_id:185132)（即线性泛函）：
$$
\omega: T_p M \to \mathbb{R}
$$
线性性质意味着对于任意两个切矢量 $V, W \in T_p M$ 和任意实数 $a, b \in \mathbb{R}$，都满足：
$$
\omega(aV + bW) = a\,\omega(V) + b\,\omega(W)
$$
在点 $p$ 的所有[余矢量](@entry_id:157727)的集合构成了另一个[向量空间](@entry_id:151108)，称为**[余切空间](@entry_id:270516)**，记作 $T_p^* M$。这个空间之所以被称为切空间的**[对偶空间](@entry_id:146945)**，正是因为其元素定义在切空间的元素之上。[余矢量](@entry_id:157727) $\omega$ 作用于切矢量 $V$ 的结果 $\omega(V)$ 是一个标量，它提供了一种度量或投影 $V$ 的方式。

### [余切空间](@entry_id:270516)的[坐标基](@entry_id:270149)

正如我们可以为切空间选择一组[基矢](@entry_id:199546)一样，我们也可以为[余切空间](@entry_id:270516)找到一组对应的基底。最自然的选择是与[局部坐标系](@entry_id:751394) $(x^1, x^2, \dots, x^n)$ 相关联的基底。

我们知道，[局部坐标系](@entry_id:751394) $(x^1, \dots, x^n)$ 诱导了切空间 $T_p M$ 的一组[坐标基](@entry_id:270149)矢 $\{ \frac{\partial}{\partial x^1}, \frac{\partial}{\partial x^2}, \dots, \frac{\partial}{\partial x^n} \}$。与此对应，存在一组**对偶基**（dual basis），记作 $\{dx^1, dx^2, \dots, dx^n\}$，它们是[余切空间](@entry_id:270516) $T_p^* M$ 的一组基底。

这组对偶基的定义并非凭空产生，而是通过它们与切空间[基矢](@entry_id:199546)的作用关系来确立的。其核心定义关系是：
$$
dx^i\left(\frac{\partial}{\partial x^j}\right) = \delta^i_j
$$
其中 $\delta^i_j$ 是**克罗内克（Kronecker）δ符号**，当 $i=j$ 时其值为1，当 $i \neq j$ 时其值为0。这个关系式是理解余矢量[坐标基](@entry_id:270149)的基石。它表明，基[余矢量](@entry_id:157727) $dx^i$ 的作用是从一个切矢量中“提取”出其第 $i$ 个分量。

这个定义的美妙之处在于，它直接揭示了任何一个[余矢量](@entry_id:157727) $\omega$ 在这组基下的分量是什么。若将 $\omega$ 展开为基的线性组合：
$$
\omega = \omega_1 dx^1 + \omega_2 dx^2 + \dots + \omega_n dx^n = \sum_{i=1}^n \omega_i dx^i
$$
那么，$\omega$ 作用在第 $j$ 个[基矢](@entry_id:199546) $\frac{\partial}{\partial x^j}$ 上时，根据线性和对偶关系，我们得到：
$$
\omega\left(\frac{\partial}{\partial x^j}\right) = \left(\sum_{i=1}^n \omega_i dx^i\right)\left(\frac{\partial}{\partial x^j}\right) = \sum_{i=1}^n \omega_i dx^i\left(\frac{\partial}{\partial x^j}\right) = \sum_{i=1}^n \omega_i \delta^i_j = \omega_j
$$
这告诉我们一个至关重要的结论：**余矢量 $\omega$ 在基 $\{dx^i\}$ 下的第 $j$ 个分量 $\omega_j$ ，恰好就是 $\omega$ 作用在第 $j$ 个[基矢](@entry_id:199546)量 $\frac{\partial}{\partial x^j}$ 上得到的值** [@problem_id:1499301]。例如，在一个[三维流形](@entry_id:193484)的[局部坐标](@entry_id:181200) $(x^1, x^2, x^3)$ 中，如果一个1-形式 $\omega$ 作用于[基矢](@entry_id:199546)量的结果是 $\omega(\frac{\partial}{\partial x^1}) = -5$，$\omega(\frac{\partial}{\partial x^2}) = \pi$ 和 $\omega(\frac{\partial}{\partial x^3}) = \sqrt{2}$，那么我们可以立即写出 $\omega$ 的分量表达式：
$$
\omega = -5 dx^1 + \pi dx^2 + \sqrt{2} dx^3
$$
其分量为 $\begin{pmatrix}-5  \pi  \sqrt{2}\end{pmatrix}$。

为了更具体地理解对偶关系，我们可以通过一个在不同[坐标系](@entry_id:156346)下的计算来验证它。考虑二维平面上的极坐标 $(r, \theta)$。其[切空间](@entry_id:199137)[基矢](@entry_id:199546)为 $\{\frac{\partial}{\partial r}, \frac{\partial}{\partial \theta}\}$，[余切空间](@entry_id:270516)[基矢](@entry_id:199546)为 $\{dr, d\theta\}$。根据定义，我们应该有 $dr(\frac{\partial}{\partial \theta}) = 0$。我们可以通过将两者都转换到[笛卡尔坐标系](@entry_id:169789) $(x, y)$下来直接计算以验证此言不虚 [@problem_id:1499308]。
首先，坐标变换关系为 $x = r \cos\theta$，$y = r \sin\theta$。[逆变](@entry_id:192290)换为 $r = \sqrt{x^2 + y^2}$。
1-形式 $dr$ 可以通过[全微分](@entry_id:171747)得到：
$$
dr = \frac{\partial r}{\partial x} dx + \frac{\partial r}{\partial y} dy = \frac{x}{\sqrt{x^2+y^2}} dx + \frac{y}{\sqrt{x^2+y^2}} dy = \frac{x}{r} dx + \frac{y}{r} dy
$$
切矢量 $\frac{\partial}{\partial \theta}$ 可以通过链式法则表达：
$$
\frac{\partial}{\partial \theta} = \frac{\partial x}{\partial \theta} \frac{\partial}{\partial x} + \frac{\partial y}{\partial \theta} \frac{\partial}{\partial y} = -r \sin\theta \frac{\partial}{\partial x} + r \cos\theta \frac{\partial}{\partial y}
$$
现在计算 $dr(\frac{\partial}{\partial \theta})$：
$$
dr\left(\frac{\partial}{\partial \theta}\right) = \left(\frac{x}{r} dx + \frac{y}{r} dy\right) \left(-r \sin\theta \frac{\partial}{\partial x} + r \cos\theta \frac{\partial}{\partial y}\right)
$$
利用线性和 $dx(\frac{\partial}{\partial x})=1, dx(\frac{\partial}{\partial y})=0$ 等关系，上式变为：
$$
\frac{x}{r}(-r \sin\theta) + \frac{y}{r}(r \cos\theta) = -x \sin\theta + y \cos\theta
$$
将 $x=r\cos\theta$ 和 $y=r\sin\theta$ 代入，得到：
$$
- (r\cos\theta)\sin\theta + (r\sin\theta)\cos\theta = 0
$$
计算结果为0，这完美地印证了对偶基的定义 $dr(\frac{\partial}{\partial \theta})=\delta^r_\theta=0$。

### 余矢量的作用：分量计算与线性性质

一旦我们拥有了余矢量和切矢量的分量表示，计算它们之间的作用就变得非常直观。设[余矢量](@entry_id:157727) $\omega = \omega_i dx^i$ 和切矢量 $V = V^j \frac{\partial}{\partial x^j}$（这里使用了爱因斯坦求和约定，即对重复的上下指标求和），它们的作用结果为：
$$
\omega(V) = (\omega_i dx^i)\left(V^j \frac{\partial}{\partial x^j}\right) = \omega_i V^j dx^i\left(\frac{\partial}{\partial x^j}\right) = \omega_i V^j \delta^i_j = \omega_j V^j
$$
这个结果的形式类似于向量的[点积](@entry_id:149019)：将对应分量相乘再求和。

让我们通过一个实例来应用这个公式 [@problem_id:1499307]。考虑 $\mathbb{R}^2$ 上的[1-形式](@entry_id:270392) $\omega = y dx - x dy$ 和一条[参数化](@entry_id:272587)曲线 $\gamma(t) = (x(t), y(t)) = (t^2, 3t-1)$。曲线在任意一点的切矢量是 $V = \gamma'(t) = \frac{dx}{dt}\frac{\partial}{\partial x} + \frac{dy}{dt}\frac{\partial}{\partial y}$。在 $t=2$ 时，我们有：
- 点的坐标：$x(2) = 2^2 = 4$, $y(2) = 3(2)-1 = 5$。
- 在该点，$\omega$ 的分量为 $(\omega_x, \omega_y) = (y, -x) = (5, -4)$。
- 切矢量的分量：$\dot{x}(t)=2t \Rightarrow \dot{x}(2)=4$, $\dot{y}(t)=3 \Rightarrow \dot{y}(2)=3$。所以 $V$ 的分量为 $(V^x, V^y) = (4, 3)$。

现在，我们可以计算 $\omega(V)$：
$$
\omega(V) = \omega_x V^x + \omega_y V^y = (5)(4) + (-4)(3) = 20 - 12 = 8
$$
这个计算过程清晰地展示了[1-形式](@entry_id:270392)如何“测量”一个矢量：它将矢量的分量与自身的分量进行加权求和。

此外，由于一个矢量空间中的元素可以由其在基底上的作用来唯一确定，如果两个[余矢量](@entry_id:157727) $\alpha$ 和 $\beta$ 对任意矢量 $V$ 的作用都成比例，例如 $\alpha(V) = k \cdot \beta(V)$，那么它们的 respective 分量也必须满足同样的关系。即 $\alpha_i = k \cdot \beta_i$ [@problem_id:1499288]。这是因为 $\alpha_i V^i = k (\beta_i V^i)$ 对任意 $V^i$ 成立，这只有在系数相等时才可能。

### [标量场](@entry_id:151443)的[微分](@entry_id:158718)：梯度与1-形式

余矢量最重要和最常见的来源之一是[标量场](@entry_id:151443)（或0-形式）的**[微分](@entry_id:158718)**（differential）。给定一个光滑的标量函数 $f(x^1, \dots, x^n)$，它的[微分](@entry_id:158718) $df$ 是一个[1-形式](@entry_id:270392)场。$df$ 在点 $p$ 对矢量 $V \in T_p M$ 的作用被定义为函数 $f$ 沿 $V$ 方向的[方向导数](@entry_id:189133)，$V[f]$。

要找到 $df$ 在[坐标基](@entry_id:270149) $\{dx^i\}$ 下的分量，我们只需按照之前的结论，计算它在[基矢](@entry_id:199546)量 $\frac{\partial}{\partial x^j}$ 上的作用：
$$
(df)_j = df\left(\frac{\partial}{\partial x^j}\right) = \frac{\partial}{\partial x^j}[f] = \frac{\partial f}{\partial x^j}
$$
因此，我们得到了一个极为重要的公式：
$$
df = \frac{\partial f}{\partial x^1} dx^1 + \frac{\partial f}{\partial x^2} dx^2 + \dots + \frac{\partial f}{\partial x^n} dx^n = \sum_i \frac{\partial f}{\partial x^i} dx^i
$$
这表明，标量场 $f$ 的[微分](@entry_id:158718) $df$ 是一个1-形式，其在[坐标基](@entry_id:270149)下的分量恰好是 $f$ 对各个坐标的偏导数。这正是我们熟悉的**梯度**（gradient）概念在微分几何中的精确表述。梯度 $\nabla f$ 的分量就是[1-形式](@entry_id:270392) $df$ 的分量。

例如，对于三维空间中的[标量场](@entry_id:151443) $\Phi(x, y, z) = z \arctan(\frac{y}{x})$ [@problem_id:1499290]，我们可以通过计算[偏导数](@entry_id:146280)来找到其[微分](@entry_id:158718) $d\Phi$：
- $\frac{\partial \Phi}{\partial x} = -\frac{zy}{x^2 + y^2}$
- $\frac{\partial \Phi}{\partial y} = \frac{zx}{x^2 + y^2}$
- $\frac{\partial \Phi}{\partial z} = \arctan(\frac{y}{x})$

于是，[1-形式](@entry_id:270392) $d\Phi$ 为：
$$
d\Phi = -\frac{zy}{x^2 + y^2} dx + \frac{zx}{x^2 + y^2} dy + \arctan\left(\frac{y}{x}\right) dz
$$
这个公式的普适性在于它适用于任何[坐标系](@entry_id:156346)。例如，在球坐标 $(r, \theta, \phi)$ 下，函数 $f$ 的[微分](@entry_id:158718)同样是 $df = \frac{\partial f}{\partial r}dr + \frac{\partial f}{\partial \theta}d\theta + \frac{\partial f}{\partial \phi}d\phi$。因此，$df$ 在 $d\theta$ 方向的分量就是 $\frac{\partial f}{\partial \theta}$ [@problem_id:1499278]。

### 坐标变换下的基与分量

一个核心问题是，当[坐标系](@entry_id:156346)改变时，[余矢量](@entry_id:157727)的基和分量是如何变换的？这对于理解张量的本质至关重要。

假设我们有两套[坐标系](@entry_id:156346)，旧坐标 $(x^1, \dots, x^n)$ 和新坐标 $(x'^1, \dots, x'^n)$。
首先考虑**基[余矢量](@entry_id:157727)的变换**。新[坐标基](@entry_id:270149) $dx'^j$ 本身是新坐标函数 $x'^j(x^1, \dots, x^n)$ 的[微分](@entry_id:158718)。根据上一节的[微分](@entry_id:158718)公式，我们可以立即写出：
$$
dx'^j = \sum_i \frac{\partial x'^j}{\partial x^i} dx^i
$$
这就是基余矢量的变换法则。变换矩阵的元素是[雅可比矩阵](@entry_id:264467) $J_{ij} = \frac{\partial x'^j}{\partial x^i}$ 的元素。

例如，从笛卡尔坐标 $(x, y)$ 到新坐标 $(u, v)$，其中 $u = 2x - y$ 和 $v = x + 3y$ [@problem_id:1499279]。新基底 $du$ 和 $dv$ 可以表示为：
$$
du = \frac{\partial u}{\partial x} dx + \frac{\partial u}{\partial y} dy = 2dx - dy
$$
$$
dv = \frac{\partial v}{\partial x} dx + \frac{\partial v}{\partial y} dy = dx + 3dy
$$
这是一个简单的[线性变换](@entry_id:149133)。对于更复杂的[非线性变换](@entry_id:636115)，如笛卡尔坐标到极坐标 $(r, \theta)$，我们需要先写出 $r(x,y)$ 和 $\theta(x,y)$，然后求偏导 [@problem_id:1499292]。例如，$r = \sqrt{x^2+y^2}$，$\theta = \arctan(y/x)$。
$$
dr = \frac{\partial r}{\partial x} dx + \frac{\partial r}{\partial y} dy = \frac{x}{r}dx + \frac{y}{r}dy = \cos(\theta)dx + \sin(\theta)dy
$$
$$
d\theta = \frac{\partial \theta}{\partial x} dx + \frac{\partial \theta}{\partial y} dy = -\frac{y}{r^2}dx + \frac{x}{r^2}dy = -\frac{\sin(\theta)}{r}dx + \frac{\cos(\theta)}{r}dy
$$
这些关系可以用矩阵形式表示，变换矩阵即为 $\frac{\partial(r,\theta)}{\partial(x,y)}$。

接下来考虑**[余矢量](@entry_id:157727)分量的变换**。一个[余矢量](@entry_id:157727) $\omega$ 是一个几何对象，它不依赖于[坐标系](@entry_id:156346)的选择，但其分量表示依赖于所选的基。我们有：
$$
\omega = \sum_i \omega_i dx^i = \sum_j \omega'_j dx'^j
$$
为了找到新旧分量 $(\omega'_j)$ 和 $(\omega_i)$ 之间的关系，我们需要反向的[基变换](@entry_id:189626)关系，即如何用 $dx'^j$ 表示 $dx^i$。这由逆雅可比矩阵给出：$dx^i = \sum_j \frac{\partial x^i}{\partial x'^j} dx'^j$。代入上式：
$$
\omega = \sum_i \omega_i \left( \sum_j \frac{\partial x^i}{\partial x'^j} dx'^j \right) = \sum_j \left( \sum_i \omega_i \frac{\partial x^i}{\partial x'^j} \right) dx'^j
$$
与 $\omega = \sum_j \omega'_j dx'^j$ 比较系数，我们得到分量的变换法则：
$$
\omega'_j = \sum_i \omega_i \frac{\partial x^i}{\partial x'^j}
$$
这个变换法则被称为**[协变变换](@entry_id:198397)**（covariant transformation），这也是[余矢量](@entry_id:157727)被称为“[协变矢量](@entry_id:263917)”的原因。

一个重要的推论是，在一个[坐标系](@entry_id:156346)中具有常数分量的[余矢量场](@entry_id:186855)，在另一个[坐标系](@entry_id:156346)中其分量通常不是常数。例如，考虑笛卡尔坐标系中分量恒定的1-形式 $\omega = A dx + B dy$，其中 $A,B$ 为常数 [@problem_id:1499312]。我们想知道它在极[坐标基](@entry_id:270149) $\{dr, d\theta\}$ 下的分量 $\omega_r, \omega_\theta$。我们可以使用更直接的方法：将旧基底 $dx, dy$ 用新基底 $dr, d\theta$ 表示。从 $x=r\cos\theta, y=r\sin\theta$ 出发，我们得到：
$$
dx = \cos\theta dr - r\sin\theta d\theta
$$
$$
dy = \sin\theta dr + r\cos\theta d\theta
$$
代入 $\omega$ 的表达式：
$$
\omega = A(\cos\theta dr - r\sin\theta d\theta) + B(\sin\theta dr + r\cos\theta d\theta)
$$
整理 $dr$ 和 $d\theta$ 的系数：
$$
\omega = (A\cos\theta + B\sin\theta) dr + (-Ar\sin\theta + Br\cos\theta) d\theta
$$
因此，我们得到极坐标下的分量：
$$
\omega_r = A\cos\theta + B\sin\theta
$$
$$
\omega_\theta = r(B\cos\theta - A\sin\theta)
$$
显然，即使 $A, B$ 是常数，新分量 $\omega_r$ 和 $\omega_\theta$ 也是坐标 $(r, \theta)$ 的函数。这深刻地揭示了“分量”的坐标依赖性。

### 推广：[非坐标基](@entry_id:160990)及其对偶基

对偶性的概念不仅限于[坐标基](@entry_id:270149)。对于[切空间](@entry_id:199137) $T_p M$ 的任意一组基 $\{E_1, \dots, E_n\}$（不一定是[坐标基](@entry_id:270149)），都存在唯一的一组[余切空间](@entry_id:270516)的对偶基 $\{\epsilon^1, \dots, \epsilon^n\}$，其定义关系依然是：
$$
\epsilon^i(E_j) = \delta^i_j
$$
寻找这组对偶基是一个[求解线性方程组](@entry_id:169069)的过程。假设我们知道新[基矢](@entry_id:199546) $E_j$ 和旧[基矢](@entry_id:199546) $\frac{\partial}{\partial x^k}$ 的关系 $E_j = M^k_j \frac{\partial}{\partial x^k}$，以及待求的对偶基 $\epsilon^i$ 和旧对偶基 $dx^k$ 的关系 $\epsilon^i = (A^T)^i_k dx^k$。通过定义关系可以证明，[系数矩阵](@entry_id:151473) $A$ 是 $M$ 的[逆矩阵](@entry_id:140380)，即 $A = M^{-1}$。

让我们通过一个例子来说明 [@problem_id:1499303]。在 $\mathbb{R}^2$ 中，设新的[切空间](@entry_id:199137)基为：
$E_1 = 2\frac{\partial}{\partial x} + \frac{\partial}{\partial y}$
$E_2 = \frac{\partial}{\partial x} - 3\frac{\partial}{\partial y}$

我们寻找对偶基 $\epsilon^1 = a_{11} dx + a_{12} dy$ 和 $\epsilon^2 = a_{21} dx + a_{22} dy$。
根据定义 $\epsilon^1(E_1) = 1$ 和 $\epsilon^1(E_2) = 0$，我们得到[方程组](@entry_id:193238)：
$$
\begin{cases} (a_{11} dx + a_{12} dy)(2\frac{\partial}{\partial x} + \frac{\partial}{\partial y}) = 2a_{11} + a_{12} = 1 \\ (a_{11} dx + a_{12} dy)(\frac{\partial}{\partial x} - 3\frac{\partial}{\partial y}) = a_{11} - 3a_{12} = 0 \end{cases}
$$
解得 $a_{11} = \frac{3}{7}, a_{12} = \frac{1}{7}$。所以 $\epsilon^1 = \frac{3}{7}dx + \frac{1}{7}dy$。
同理，根据 $\epsilon^2(E_1) = 0$ 和 $\epsilon^2(E_2) = 1$，我们得到：
$$
\begin{cases} 2a_{21} + a_{22} = 0 \\ a_{21} - 3a_{22} = 1 \end{cases}
$$
解得 $a_{21} = \frac{1}{7}, a_{22} = -\frac{2}{7}$。所以 $\epsilon^2 = \frac{1}{7}dx - \frac{2}{7}dy$。
因此，对偶基的系数矩阵为 $\begin{pmatrix} 3/7  1/7 \\ 1/7  -2/7 \end{pmatrix}$，这恰好是[基变换矩阵](@entry_id:184480) $M=\begin{pmatrix} 2  1 \\ 1  -3 \end{pmatrix}$ 的[逆矩阵](@entry_id:140380)。

### 物理与几何应用：功与线积分

[1-形式](@entry_id:270392)在物理学和几何学中有广泛应用，其中一个经典例子是描述[力场](@entry_id:147325)和功。一个[力场](@entry_id:147325)可以被模型化为一个1-形式场 $\omega$。当一个粒子沿着路径 $C$ 移动时，[力场](@entry_id:147325)对粒子做的总功 $W$ 就是 $\omega$ 沿着路径 $C$ 的**[线积分](@entry_id:141417)**：
$$
W = \int_C \omega
$$
如果路径 $C$ 由参数 $t$ 给出，$\gamma(t) = (x^1(t), \dots, x^n(t))$，那么路径的切矢量（速度矢量）为 $V(t) = \frac{d\gamma}{dt}$。无穷小功 $dW$ 就是 $\omega$ 作用在[无穷小位移](@entry_id:202209) $V dt$ 上，即 $dW = \omega(V)dt$。总功就是对 $t$ 的积分。

考虑一个例子 [@problem_id:1499309]，在极坐标中，一个[力场](@entry_id:147325)对应的1-形式为 $\omega = \alpha r^2 d\theta$，其中 $\alpha$ 是常数。我们要计算一个粒子沿半径为 $R$ 的圆形路径从 $\theta=0$ 运动到 $\theta=2\pi$ 一周所做的功。
路径可以[参数化](@entry_id:272587)为 $r(t) = R$ (常数)，$\theta(t) = t$，其中 $t$ 从 $0$到 $2\pi$。
沿着这条路径，$dr=0$，所以[1-形式](@entry_id:270392) $\omega$ 简化为 $\omega|_C = \alpha R^2 d\theta$。
总功为：
$$
W = \int_C \alpha R^2 d\theta = \int_0^{2\pi} \alpha R^2 d\theta = \alpha R^2 [\theta]_0^{2\pi} = 2\pi\alpha R^2
$$
若 $\alpha = 3.0 \, \text{J} \cdot \text{m}^{-2}$ 且 $R=2.0 \, \text{m}$，则 $W = 2\pi (3.0)(2.0)^2 = 24\pi \approx 75.4 \, \text{J}$。
这个例子中，沿闭合路径的功不为零，这在物理上意味着该[力场](@entry_id:147325)是**[非保守场](@entry_id:265048)**。在数学上，这对应于1-形式 $\omega$ 不是一个**恰当形式**（exact form），即它不能被写成某个标量势函数 $f$ 的[微分](@entry_id:158718) $df$。这为我们深入研究[微分形式的积分](@entry_id:158607)性质和更高级的拓扑概念（如[德拉姆上同调](@entry_id:158673)）埋下了伏笔。