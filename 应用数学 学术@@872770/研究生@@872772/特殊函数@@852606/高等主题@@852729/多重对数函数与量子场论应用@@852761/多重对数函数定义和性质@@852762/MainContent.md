## 引言
[多重对数](@entry_id:204271)函数 (Polylogarithm) 是一种深刻而强大的特殊函数，它在从纯粹数学到理论物理的广阔领域中扮演着意想不到的核心角色。尽管其形式看似简单，但它却像一座桥梁，连接着[解析数论](@entry_id:158402)、代数几何与[量子场论](@entry_id:138177)等看似毫无关联的学科。然而，对于许多学生和研究者而言，[多重对数](@entry_id:204271)函数往往显得抽象和零散，缺乏一个系统性的框架来理解其内在的统一性与强大的应用潜力。本文旨在填补这一空白，为读者提供一个全面而深入的指南。

通过本文的学习，您将踏上一段从基础理论到前沿应用的探索之旅。在第一章“原理与机制”中，我们将从最基本的[幂级数](@entry_id:146836)和积分定义出发，系统推导其核心解析性质和重要的函数方程。随后，在第二章“应用与[交叉](@entry_id:147634)学科联系”中，我们将见证这些理论如何被巧妙地应用于解决复杂的[定积分](@entry_id:147612)、[无穷级数求和](@entry_id:161691)问题，并揭示其在数论、[量子统计力学](@entry_id:140244)和拓扑学中的深刻印记。最后，在第三章“动手实践”中，您将有机会通过解决一系列精心设计的问题，将所学知识付诸实践，从而真正内化并掌握这一强大的数学工具。

## 原理与机制

本章在前一章介绍性概述的基础上，深入探讨[多重对数](@entry_id:204271)函数 (Polylogarithm) 的核心数学原理和内在机制。我们将从其基本定义出发，系统地推导其关键属性，并展示这些属性如何被用于解决看似无关的级数求和与积分计算问题。本章旨在为读者提供一个坚实的理论基础，以便在后续章节中探索其在物理学和数论等领域中的高级应用。

### 基本定义与表示

[多重对数](@entry_id:204271)函数，记为 $\mathrm{Li}_s(z)$，是一个关于复阶数 $s$ 和复变量 $z$ 的[特殊函数](@entry_id:143234)。其最基本的定义形式是一个幂级数。

#### 幂级数定义

对于任意复数 $s$ 和满足 $|z| < 1$ 的复数 $z$，[多重对数](@entry_id:204271)函数定义为：
$$
\mathrm{Li}_s(z) = \sum_{k=1}^{\infty} \frac{z^k}{k^s}
$$
这个级数在[单位圆盘](@entry_id:172324) $|z| < 1$ 内[绝对收敛](@entry_id:146726)。当 $|z|=1$ 时，[级数的收敛](@entry_id:136768)性取决于 $s$ 的值，通常要求 $\Re(s) > 1$。通过解析延拓，[函数的定义域](@entry_id:162002)可以扩展到更大的复平面范围。

根据阶数 $s$ 的不同，[多重对数](@entry_id:204271)函数有不同的[别名](@entry_id:146322)。$s=2$ 的情况被称为[二重对数函数](@entry_id:181236) (Dilogarithm)，$s=3$ 称为三重对数函数 (Trilogarithm)，以此类推。特别地，$s=1$ 的情况，有时称为单对数函数 (Unilogarithm)，与我们熟知的自然对数函数有着直接的联系。

当 $s=1$ 时，我们得到：
$$
\mathrm{Li}_1(z) = \sum_{k=1}^{\infty} \frac{z^k}{k}
$$
这正是对数函数 $\ln(1-z)$ 的[麦克劳林级数](@entry_id:146685)的[相反数](@entry_id:151709)。因此，我们有了一个至关重要的恒等式：
$$
\mathrm{Li}_1(z) = -\ln(1-z)
$$
此关系在 $|z| \le 1, z \ne 1$ 时成立，其中 $\ln$ 表示[复对数](@entry_id:174857)的[主分支](@entry_id:164844)。这个简单的关系揭示了[多重对数](@entry_id:204271)函数家族与基本[初等函数](@entry_id:181530)之间的深刻联系，并为计算特定类型的无穷级数提供了有力的工具。例如，我们可以利用这个关系来计算傅里葉级数形式的求和。

考虑一个形如 $S = \sum_{k=1}^{\infty} \frac{\cos(k\theta)}{k}$ 的级数。我们可以注意到，该级数是 $\sum_{k=1}^{\infty} \frac{(e^{i\theta})^k}{k}$ 的实部。根据定义，后者正是 $\mathrm{Li}_1(e^{i\theta})$。因此：
$$
S = \Re\left( \sum_{k=1}^{\infty} \frac{(e^{i\theta})^k}{k} \right) = \Re(\mathrm{Li}_1(e^{i\theta})) = \Re(-\ln(1-e^{i\theta}))
$$
利用[复对数](@entry_id:174857)实部的性质 $\Re(\ln(w)) = \ln|w|$，我们得到：
$$
S = -\ln|1-e^{i\theta}|
$$
通过简单的[复数运算](@entry_id:195031)，我们知道 $|1-e^{i\theta}| = |1 - (\cos\theta + i\sin\theta)| = \sqrt{(1-\cos\theta)^2 + \sin^2\theta} = \sqrt{2 - 2\cos\theta} = \sqrt{4\sin^2(\frac{\theta}{2})} = 2|\sin(\frac{\theta}{2})|$。于是，
$$
S = -\ln\left(2\left|\sin\left(\frac{\theta}{2}\right)\right|\right)
$$
以 $\theta = \frac{\pi}{3}$ 为例，我们可以立即求出级数的值 [@problem_id:742802]：
$$
\sum_{k=1}^{\infty} \frac{\cos(k\pi/3)}{k} = -\ln\left(2\sin\left(\frac{\pi}{6}\right)\right) = -\ln\left(2 \cdot \frac{1}{2}\right) = -\ln(1) = 0
$$

#### 积分表示

[多重对数](@entry_id:204271)函数的另一个核心面向是其积分表示。这种表示不仅扩展了[函数的定义域](@entry_id:162002)，还揭示了不同阶数的[多重对数](@entry_id:204271)函数之间的递归关系。从 $\mathrm{Li}_1(z) = -\ln(1-z) = \int_0^z \frac{dt}{1-t}$ 出发，我们可以观察到一个模式。

对 $\mathrm{Li}_s(z)$ 的级数定义式[逐项积分](@entry_id:138696)，可以得到一个递归关系。考虑从 $\mathrm{Li}_s(t)$ 到 $\mathrm{Li}_{s+1}(z)$：
$$
\int_0^z \frac{\mathrm{Li}_s(t)}{t} dt = \int_0^z \frac{1}{t} \sum_{k=1}^{\infty} \frac{t^k}{k^s} dt = \sum_{k=1}^{\infty} \frac{1}{k^s} \int_0^z t^{k-1} dt = \sum_{k=1}^{\infty} \frac{1}{k^s} \frac{z^k}{k} = \sum_{k=1}^{\infty} \frac{z^k}{k^{s+1}} = \mathrm{Li}_{s+1}(z)
$$
于是，我们得到了一个优美的递归积分定义：
$$
\mathrm{Li}_{s+1}(z) = \int_0^z \frac{\mathrm{Li}_s(t)}{t} dt
$$
这个关系是[多重对数](@entry_id:204271)函数理论的基石之一。特别地，对于[二重对数函数](@entry_id:181236) $\mathrm{Li}_2(z)$，我们有 [@problem_id:742678] [@problem_id:742859] [@problem_id:742695] [@problem_id:742705]：
$$
\mathrm{Li}_2(z) = \int_0^z \frac{\mathrm{Li}_1(t)}{t} dt = -\int_0^z \frac{\ln(1-t)}{t} dt
$$
这个积分表示在复平面上除去从 $[1, \infty)$ 的射线外均成立，为研究[二重对数函数](@entry_id:181236)的性质提供了强大的分析工具。

### 核心解析性质

[多重对数](@entry_id:204271)函数拥有一系列重要的[解析性](@entry_id:140716)质，其中最实用的是关于其导数的递归关系。

#### 导数递归关系

从上述的积分递归关系 $\mathrm{Li}_{s+1}(z) = \int_0^z \frac{\mathrm{Li}_s(t)}{t} dt$，根据[微积分基本定理](@entry_id:201377)，两边对 $z$ 求导，我们立刻得到一个关于阶数 $s$ 的降阶关系：
$$
\frac{d}{dz}\mathrm{Li}_{s+1}(z) = \frac{\mathrm{Li}_s(z)}{z}
$$
或者，更普遍地写为：
$$
\frac{d}{dz}\mathrm{Li}_s(z) = \frac{\mathrm{Li}_{s-1}(z)}{z}
$$
这个关系式极其有用，因为它将高阶[多重对数](@entry_id:204271)函数的导数与一个更低阶（也因此通常更简单）的[多重对数](@entry_id:204271)函数联系起来。例如，对于[二重对数函数](@entry_id:181236)，其导数就是：
$$
\frac{d}{dz}\mathrm{Li}_2(z) = \frac{\mathrm{Li}_1(z)}{z} = -\frac{\ln(1-z)}{z}
$$
这一性质结合链式法则，使得计算包含[多重对数](@entry_id:204271)函数的复杂表达式的导数变得可行。例如，我们来计算函数 $f(z) = \mathrm{Li}_3(z^2)$ 在 $z=i$ 处的导数 [@problem_id:742690]。
根据链式法则和导数递归关系：
$$
f'(z) = \frac{d}{dz}\mathrm{Li}_3(z^2) = \frac{\mathrm{Li}_2(z^2)}{z^2} \cdot \frac{d(z^2)}{dz} = \frac{\mathrm{Li}_2(z^2)}{z^2} \cdot 2z = \frac{2\mathrm{Li}_2(z^2)}{z}
$$
在 $z=i$ 处求值：
$$
f'(i) = \frac{2\mathrm{Li}_2(i^2)}{i} = \frac{2\mathrm{Li}_2(-1)}{i}
$$
我们将在下一节看到，$\mathrm{Li}_2(-1)$ 是一个已知的特殊值，等于 $-\frac{\pi^2}{12}$。代入后得到：
$$
f'(i) = \frac{2(-\pi^2/12)}{i} = -\frac{\pi^2}{6i} = \frac{i\pi^2}{6}
$$
这个例子展示了导数公式在具体计算中的威力。同样，该性质也是证明[多重对数](@entry_id:204271)函数恒等式的主要工具 [@problem_id:742801]。

### 特殊值与相关常数

[多重对数](@entry_id:204271)函数在某些特殊点上的取值，与数学中一些著名的常数和函数紧密相关，如黎曼ζ函数和卡塔兰常数。

#### 在 $z=1$ 和 $z=-1$ 处的值

根据级数定义，当 $z=1$ 时，[多重对数](@entry_id:204271)函数的值直接与黎曼ζ函数 (Riemann zeta function) $\zeta(s)$ 挂钩：
$$
\mathrm{Li}_s(1) = \sum_{k=1}^{\infty} \frac{1^k}{k^s} = \sum_{k=1}^{\infty} \frac{1}{k^s} = \zeta(s)
$$
其中一个最著名的结果是欧拉在1734年解决的巴塞尔问题 (Basel problem)，即 $\mathrm{Li}_2(1) = \zeta(2) = \frac{\pi^2}{6}$ [@problem_id:742678] [@problem_id:742695]。

当 $z=-1$ 时，我们得到一个[交错级数](@entry_id:143758)，其值与[狄利克雷η函数](@entry_id:183462) (Dirichlet eta function) $\eta(s)$ 相关：
$$
\mathrm{Li}_s(-1) = \sum_{k=1}^{\infty} \frac{(-1)^k}{k^s} = -\sum_{k=1}^{\infty} \frac{(-1)^{k-1}}{k^s} = -\eta(s)
$$
$\eta(s)$ 与 $\zeta(s)$ 的关系为 $\eta(s) = (1-2^{1-s})\zeta(s)$。因此，我们可以计算出另一个重要的二重对数值：
$$
\mathrm{Li}_2(-1) = -\eta(2) = -(1-2^{1-2})\zeta(2) = -\frac{1}{2}\zeta(2) = -\frac{\pi^2}{12}
$$
这两个特殊值 $\mathrm{Li}_2(1)$ 和 $\mathrm{Li}_2(-1)$ 在计算[定积分](@entry_id:147612)时非常有用。例如，考虑积分 $I = \int_0^1 \frac{\ln(1-x^2)}{x} dx$ [@problem_id:742678]。通过对数性质 $\ln(1-x^2) = \ln(1-x) + \ln(1+x)$，积分可以分解为两部分：
$$
I = \int_0^1 \frac{\ln(1-x)}{x} dx + \int_0^1 \frac{\ln(1+x)}{x} dx
$$
第一部分根据 $\mathrm{Li}_2(z)$ 的积分表示，即为 $-\mathrm{Li}_2(1) = -\frac{\pi^2}{6}$。第二部分同样可以写成积分形式，但其自变量为 $-x$。令 $u=-x$，积分变为 $-\int_0^{-1} \frac{\ln(1-u)}{u}du$，这正是 $-\mathrm{Li}_2(-1) = -(-\frac{\pi^2}{12}) = \frac{\pi^2}{12}$。因此：
$$
I = -\frac{\pi^2}{6} + \frac{\pi^2}{12} = -\frac{\pi^2}{12}
$$

#### 在[单位圆](@entry_id:267290)上的值

[多重对数](@entry_id:204271)函数在复平面的[单位圆](@entry_id:267290)上的取值也极为丰富。一个典型的例子是求级数 $\sum_{n=1}^\infty \frac{\cos(n\pi/3)}{n^2}$ 的值 [@problem_id:742805]。这个级数可以看作是 $\mathrm{Li}_2(e^{i\pi/3})$ 的实部。对于[单位圆](@entry_id:267290)上的点 $z=e^{i\theta}$，$\mathrm{Li}_2(z)$ 的值可以通过一个已知的[解析延拓](@entry_id:147225)公式计算：
$$
\mathrm{Li}_2(e^{i\theta}) = \frac{\pi^2}{6} - \frac{\theta(2\pi-\theta)}{4} + i \cdot \mathrm{Cl}_2(\theta) \quad (0 \le \theta \le 2\pi)
$$
其中 $\mathrm{Cl}_2(\theta) = \sum_{k=1}^\infty \frac{\sin(k\theta)}{k^2}$ 是[克劳森函数](@entry_id:193617) (Clausen function)。我们关心的只是实部，所以：
$$
\Re(\mathrm{Li}_2(e^{i\theta})) = \frac{\pi^2}{6} - \frac{\theta(2\pi-\theta)}{4}
$$
令 $\theta = \pi/3$，我们得到：
$$
\sum_{n=1}^\infty \frac{\cos(n\pi/3)}{n^2} = \Re(\mathrm{Li}_2(e^{i\pi/3})) = \frac{\pi^2}{6} - \frac{(\pi/3)(2\pi-\pi/3)}{4} = \frac{\pi^2}{6} - \frac{5\pi^2/9}{4} = \frac{\pi^2}{6} - \frac{5\pi^2}{36} = \frac{\pi^2}{36}
$$

#### 与卡塔兰常数的联系

在 $z=i$ 这个特殊的点上，[二重对数函数](@entry_id:181236)与另一个著名的数学常数——卡塔兰常数 (Catalan's constant) $G$ 产生了联系 [@problem_id:742684]。卡塔兰常数的定义是：
$$
G = \sum_{n=0}^{\infty} \frac{(-1)^n}{(2n+1)^2} = \frac{1}{1^2} - \frac{1}{3^2} + \frac{1}{5^2} - \dots
$$
我们来考察 $\mathrm{Li}_2(i)$ 的[级数表示](@entry_id:175860)：
$$
\mathrm{Li}_2(i) = \sum_{k=1}^{\infty} \frac{i^k}{k^2}
$$
将级数按 $k$ 的奇偶性分开。当 $k=2n$ (偶数项) 时，项为 $\frac{i^{2n}}{(2n)^2} = \frac{(-1)^n}{4n^2}$。这些项的和为 $\frac{1}{4} \sum_{n=1}^\infty \frac{(-1)^n}{n^2} = \frac{1}{4}\mathrm{Li}_2(-1) = -\frac{\pi^2}{48}$。当 $k=2n-1$ (奇数项) 时，项为 $\frac{i^{2n-1}}{(2n-1)^2} = i \frac{(-1)^{n-1}}{(2n-1)^2}$。这些项的和为 $i \sum_{n=1}^\infty \frac{(-1)^{n-1}}{(2n-1)^2} = iG$。
将两部分合并，我们得到一个优美的结果：
$$
\mathrm{Li}_2(i) = -\frac{\pi^2}{48} + iG
$$
因此，卡塔兰常数 $G$ 正是 $\mathrm{Li}_2(i)$ 的虚部：$\Im(\mathrm{Li}_2(i)) = G$。

### [二重对数函数](@entry_id:181236)的[函数方程](@entry_id:199663)

[二重对数函数](@entry_id:181236)满足一系列令人惊叹的函数方程（恒等式），这些方程是其理论的核心，也是其在高等数学和物理中广泛应用的基础。证明这些恒等式的一个常用且强大的技巧是：构造一个包含恒等式两边项的函数，证明其导数为零，从而表明该函数是一个常数，最后通过在一个特殊点（如 $z=0$）求值来确定这个常数。

#### [欧拉反射公式](@entry_id:139367) (Euler's Reflection Formula)

这个公式建立了 $\mathrm{Li}_2(x)$ 和 $\mathrm{Li}_2(1-x)$ 之间的关系。考虑函数 [@problem_id:742695]：
$$
F(x) = \mathrm{Li}_2(x) + \mathrm{Li}_2(1-x) + \ln(x)\ln(1-x)
$$
对其求导，利用导数公式和[乘法法则](@entry_id:144424)：
$$
F'(x) = \left(-\frac{\ln(1-x)}{x}\right) + \left(-\frac{\ln(1-(1-x))}{1-x} \cdot (-1)\right) + \left(\frac{1}{x}\ln(1-x) + \ln(x)\frac{-1}{1-x}\right)
$$
$$
F'(x) = -\frac{\ln(1-x)}{x} - \frac{\ln(x)}{1-x} + \frac{\ln(1-x)}{x} - \frac{\ln(x)}{1-x} = 0
$$
由于导数为零，$F(x)$ 必为常数 $C$。为了确定 $C$，我们可以取极限 $x \to 1^-$。此时 $\mathrm{Li}_2(x) \to \mathrm{Li}_2(1) = \zeta(2)$，$\mathrm{Li}_2(1-x) \to \mathrm{Li}_2(0) = 0$，而 $\lim_{x\to 1^-} \ln(x)\ln(1-x) = 0$。因此 $C = \zeta(2)$。于是我们得到[欧拉反射公式](@entry_id:139367)：
$$
\mathrm{Li}_2(x) + \mathrm{Li}_2(1-x) = \frac{\pi^2}{6} - \ln(x)\ln(1-x)
$$

#### 兰登恒等式 (Landen's Identity)

兰登恒等式联系了 $\mathrm{Li}_2(z)$ 和 $\mathrm{Li}_2(\frac{z}{z-1})$。考虑函数 [@problem_id:742859]：
$$
F(z) = \mathrm{Li}_2(z) + \mathrm{Li}_2\left(\frac{z}{z-1}\right) + \frac{1}{2}\ln^2(1-z)
$$
对其求导：
$$
F'(z) = \frac{d}{dz}\mathrm{Li}_2(z) + \frac{d}{dz}\mathrm{Li}_2\left(\frac{z}{z-1}\right) + \frac{d}{dz}\left(\frac{1}{2}\ln^2(1-z)\right)
$$
我们逐项计算导数：
- $\frac{d}{dz}\mathrm{Li}_2(z) = -\frac{\ln(1-z)}{z}$
- 对于第二项，使用[链式法则](@entry_id:190743)，令 $u = \frac{z}{z-1}$。那么 $1-u = \frac{1}{1-z}$ 且 $\frac{du}{dz} = -\frac{1}{(z-1)^2}$。
$$ \frac{d}{dz}\mathrm{Li}_2(u) = -\frac{\ln(1-u)}{u} \frac{du}{dz} = -\frac{\ln(\frac{1}{1-z})}{\frac{z}{z-1}} \left(-\frac{1}{(z-1)^2}\right) = \frac{\ln(1-z)(z-1)}{z} \left(-\frac{1}{(z-1)^2}\right) = \frac{\ln(1-z)}{-z(z-1)} = \frac{\ln(1-z)}{z(1-z)} $$
- 对于第三项：
$$ \frac{d}{dz}\left(\frac{1}{2}\ln^2(1-z)\right) = \ln(1-z) \cdot \frac{-1}{1-z} = -\frac{\ln(1-z)}{1-z} $$
将三项相加：
$$ F'(z) = -\frac{\ln(1-z)}{z} + \frac{\ln(1-z)}{z(1-z)} - \frac{\ln(1-z)}{1-z} $$
通分后，分子变为 $-\ln(1-z)(1-z) + \ln(1-z) - z\ln(1-z)$，展开后各项抵消为 0。因此 $F'(z)=0$。
$F'(z)$ 为零。在 $z=0$ 处求值，$\mathrm{Li}_2(0)=0$ 和 $\ln(1)=0$，所以 $F(0)=0$。故我们有兰登恒等式：
$$
\mathrm{Li}_2(z) + \mathrm{Li}_2\left(\frac{z}{z-1}\right) = -\frac{1}{2}\ln^2(1-z)
$$

#### 倍数公式 (Duplication Formula)

此公式将 $\mathrm{Li}_2(z^2)$ 与 $\mathrm{Li}_2(z)$ 和 $\mathrm{Li}_2(-z)$ 联系起来。考虑函数 [@problem_id:742705]：
$$
F(z) = \mathrm{Li}_2(z^2) - 2(\mathrm{Li}_2(z) + \mathrm{Li}_2(-z))
$$
对其求导：
$$
\frac{d}{dz}\mathrm{Li}_2(z^2) = -\frac{\ln(1-z^2)}{z^2} \cdot 2z = -\frac{2\ln(1-z^2)}{z}
$$
$$
\frac{d}{dz}(\mathrm{Li}_2(z) + \mathrm{Li}_2(-z)) = -\frac{\ln(1-z)}{z} - \frac{\ln(1-(-z))}{z} \cdot (-1) = -\frac{\ln(1-z)}{z} - \frac{\ln(1+z)}{z} = -\frac{\ln(1-z^2)}{z}
$$
所以，$F'(z) = -\frac{2\ln(1-z^2)}{z} - 2\left(-\frac{\ln(1-z^2)}{z}\right) = 0$。
$F(z)$ 是一个常数。在 $z=0$ 处求值，$F(0) = \mathrm{Li}_2(0) - 2(\mathrm{Li}_2(0) + \mathrm{Li}_2(0)) = 0$。因此，我们得到了倍数公式：
$$
\mathrm{Li}_2(z^2) = 2\mathrm{Li}_2(z) + 2\mathrm{Li}_2(-z)
$$
这些函数方程是[二重对数函数](@entry_id:181236)理论的精髓，它们揭示了函数内部深刻的[代数结构](@entry_id:137052)。

### [生成函数](@entry_id:146702)与广义谐波数

[多重对数](@entry_id:204271)函数与[组合数学](@entry_id:144343)中的对象，如广义[谐波](@entry_id:181533)数 (generalized harmonic numbers)，也存在着密切的联系。广义[谐波](@entry_id:181533)数定义为：
$$
H_n^{(s)} = \sum_{k=1}^n \frac{1}{k^s}
$$
[多重对数](@entry_id:204271)函数正是 $H_n^{(s)}$ 的一个重要的[生成函数](@entry_id:146702)。考虑序列 $\{H_n^{(s)}\}_{n\ge1}$ 的生成函数 $\sum_{n=1}^\infty H_n^{(s)} z^n$。这个级数可以看作是两个级数的柯西乘积 (Cauchy product)：
$$
\left(\sum_{j=1}^\infty \frac{z^j}{j^s}\right) \left(\sum_{m=0}^\infty z^m\right) = \mathrm{Li}_s(z) \cdot \frac{1}{1-z}
$$
展开柯西乘积， $z^n$ 的系数为 $\sum_{k=1}^n \frac{1}{k^s} \cdot 1^{n-k} = H_n^{(s)}$。因此，我们得到一个非常重要的[生成函数](@entry_id:146702)关系 [@problem_id:742804]：
$$
\sum_{n=1}^\infty H_n^{(s)} z^n = \frac{\mathrm{Li}_s(z)}{1-z}
$$
这个关系式为处理包含[谐波](@entry_id:181533)数的级数提供了强大的工具。例如，要计算[交错级数](@entry_id:143758) $S = \sum_{n=1}^\infty (-1)^n H_n^{(4)}$，我们只需在上述生成函数中取 $s=4$ 和 $z=-1$：
$$
S = \frac{\mathrm{Li}_4(-1)}{1-(-1)} = \frac{\mathrm{Li}_4(-1)}{2}
$$
利用特殊值 $\mathrm{Li}_4(-1) = -\eta(4) = -(1-2^{1-4})\zeta(4) = -\frac{7}{8}\zeta(4)$ 和 $\zeta(4) = \frac{\pi^4}{90}$，我们得到：
$$
S = \frac{1}{2} \left(-\frac{7}{8} \cdot \frac{\pi^4}{90}\right) = -\frac{7\pi^4}{1440}
$$
这展示了[多重对数](@entry_id:204271)函数作为连接连续分析（积分、级数）和离散结构（谐波数）的桥梁作用。

本章系统地介绍了[多重对数](@entry_id:204271)函数的定义、核心解析性质、特殊值、重要的函数方程以及它作为[生成函数的应用](@entry_id:196295)。这些原理和机制共同构成了理解和应用这一强大数学工具的基础。