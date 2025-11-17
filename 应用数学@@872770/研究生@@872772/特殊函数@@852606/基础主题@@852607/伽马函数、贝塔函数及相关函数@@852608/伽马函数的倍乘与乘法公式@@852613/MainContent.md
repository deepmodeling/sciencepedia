## 引言
Gamma函数，作为[阶乘](@entry_id:266637)概念在[复数域](@entry_id:153768)上的延拓，是高等数学和理论物理中不可或缺的基本工具。然而，在掌握了其定义、递推关系和[反射公式](@entry_id:198841)等基础性质之后，我们如何才能洞察其更深层次的内在结构呢？许多复杂的计算和理论推导都依赖于Gamma函数在不同点取值之间的精确关系，而这正是本篇文章所要解决的核心问题。

本文将系统地探讨Gamma函数中两个最为强大和优美的恒等式：[Legendre倍角公式](@entry_id:169982)及其一般形式——[Gauss乘法公式](@entry_id:200987)。通过学习这些公式，你将不仅能够理解Gamma函数内部精妙的对称性，还能掌握简化复杂数学表达式的强大技巧。

我们的探索将分为三个部分。在“原理与机制”一章中，我们将从最简单的[倍角公式](@entry_id:173961)入手，逐步推导至[一般性](@entry_id:161765)的[Gauss乘法公式](@entry_id:200987)，并展示其在简化[Pochhammer符号](@entry_id:199791)乘积和处理渐近行为中的应用。接着，在“应用与交叉学科联系”一章中，我们将拓宽视野，探讨这些公式如何在[定积分](@entry_id:147612)计算、数论（如黎曼Zeta[函数方程](@entry_id:199663)）以及几何物理（如高维球体体积）等领域发挥关键作用。最后，“动手实践”部分将提供一系列精心设计的问题，助你将理论知识转化为解决实际问题的能力。

现在，让我们首先进入第一章，深入剖析这些乘法公式的原理与机制，揭开Gamma函数结构之美的第一层面纱。

## 原理与机制

在上一章介绍 Gamma 函数的基本性质之后，本章将深入探讨其更深层次的结构性特性。我们将聚焦于两个密切相关且极为强大的恒等式：Legendre 乘法公式和更具[一般性](@entry_id:161765)的 Gauss 乘法公式。这些公式揭示了 Gamma 函数在不同参数点取值之间的内在联系，不仅是理论推导中的关键工具，也在计算物理、数论和概率统计等领域有着广泛应用。本章将从最简单的[倍角公式](@entry_id:173961)入手，逐步推广至一般情形，并通过一系列应用展示这些公式的原理、机制及其在简化复杂数学表达式中的威力。

### Legendre [倍角公式](@entry_id:173961)：基础情形 ($n=2$)

探索乘法公式的第一步是其最基本、也最常见的形式，即 **Legendre [倍角公式](@entry_id:173961)** (Legendre duplication formula)。该公式建立了 $\Gamma(z)$ 与 $\Gamma(z + 1/2)$ 之间的精确关系。对于所有使得 Gamma 函数有定义的复数 $z$（即 $z$ 不是非正整数），该公式表述为：

$$
\Gamma(z) \Gamma\left(z + \frac{1}{2}\right) = 2^{1-2z} \sqrt{\pi} \Gamma(2z)
$$

这个公式将两个相隔 $1/2$ 的点的 Gamma 函数值与这两点算术平均值的两倍处的 Gamma 函数值联系起来。常数 $\sqrt{\pi}$ 的出现，暗示了 Gamma 函数与圆周及正态分布等概念的深刻关联，这一点从 $\Gamma(1/2) = \sqrt{\pi}$ 也能窥见一斑。

Legendre [倍角公式](@entry_id:173961)不仅本身非常优美，它也为计算某些特定 Gamma 函数值的乘积或比率提供了直接而有效的方法。例如，考虑一个经典的计算问题：求比值 $\frac{\Gamma\left(\frac{1}{4}\right)\Gamma\left(\frac{3}{4}\right)}{\Gamma\left(\frac{1}{2}\right)}$。直接计算 $\Gamma(1/4)$ 和 $\Gamma(3/4)$ 是非常困难的，但我们可以巧妙地利用[倍角公式](@entry_id:173961) [@problem_id:672287]。

注意到表达式的分子形式为 $\Gamma(z)\Gamma(z+1/2)$，其中 $z = 1/4$。我们将 $z = 1/4$ 代入 Legendre [倍角公式](@entry_id:173961)：

$$
\Gamma\left(\frac{1}{4}\right) \Gamma\left(\frac{1}{4} + \frac{1}{2}\right) = 2^{1-2(\frac{1}{4})} \sqrt{\pi} \Gamma\left(2 \cdot \frac{1}{4}\right)
$$

简化后可得：

$$
\Gamma\left(\frac{1}{4}\right) \Gamma\left(\frac{3}{4}\right) = 2^{1/2} \sqrt{\pi} \Gamma\left(\frac{1}{2}\right) = \sqrt{2} \sqrt{\pi} \cdot \sqrt{\pi} = \pi\sqrt{2}
$$

于是，我们要求解的比值就变得非常简单：

$$
\frac{\Gamma\left(\frac{1}{4}\right)\Gamma\left(\frac{3}{4}\right)}{\Gamma\left(\frac{1}{2}\right)} = \frac{\pi\sqrt{2}}{\sqrt{\pi}} = \sqrt{2\pi}
$$

这个例子清晰地展示了[倍角公式](@entry_id:173961)如何将看似无关的 Gamma 函数值联系起来，从而极大地简化了计算。

### Gauss 乘法公式：一般原理

Legendre [倍角公式](@entry_id:173961)是更一般性原理的一个特例。这个一般性原理被称为 **Gauss 乘法公式** (Gauss's multiplication formula)。它将 Gamma 函数在 $n$ 个[等距点](@entry_id:637779)上的值的乘积，与一个单一的 Gamma 函数值联系起来。对于任意正整数 $n \ge 2$ 和复数 $z$ (非非正整数)，该公式表述为：

$$
\prod_{k=0}^{n-1} \Gamma\left(z + \frac{k}{n}\right) = (2\pi)^{\frac{n-1}{2}} n^{\frac{1}{2}-nz} \Gamma(nz)
$$

不难验证，当 $n=2$ 时，该公式退化为 Legendre [倍角公式](@entry_id:173961)：

$$
\Gamma(z)\Gamma\left(z+\frac{1}{2}\right) = (2\pi)^{\frac{1}{2}} 2^{\frac{1}{2}-2z} \Gamma(2z) = \sqrt{2\pi} \cdot 2^{\frac{1}{2}-2z} \Gamma(2z) = \sqrt{\pi} 2^{1-2z} \Gamma(2z)
$$

一个深刻的洞见是，高阶的乘法公式可以由低阶公式迭代导出。以 $n=4$ 的情形为例，我们可以通过两次应用 Legendre [倍角公式](@entry_id:173961) ($n=2$) 来推导出它 [@problem_id:2250284]。考虑乘积：

$$
P(z) = \Gamma(z) \Gamma\left(z + \frac{1}{4}\right) \Gamma\left(z + \frac{1}{2}\right) \Gamma\left(z + \frac{3}{4}\right)
$$

我们可以策略性地将这些项重新组合成两对：

$$
P(z) = \left[\Gamma(z) \Gamma\left(z + \frac{1}{2}\right)\right] \cdot \left[\Gamma\left(z + \frac{1}{4}\right) \Gamma\left(z + \frac{3}{4}\right)\right]
$$

对第一对方括号应用[倍角公式](@entry_id:173961) (令参数为 $z$)：

$$
\Gamma(z) \Gamma\left(z + \frac{1}{2}\right) = 2^{1-2z} \sqrt{\pi} \Gamma(2z)
$$

对第二对方括号应用[倍角公式](@entry_id:173961) (令参数为 $w = z + 1/4$)：

$$
\Gamma\left(z + \frac{1}{4}\right) \Gamma\left(\left(z+\frac{1}{4}\right) + \frac{1}{2}\right) = 2^{1-2(z+\frac{1}{4})} \sqrt{\pi} \Gamma\left(2\left(z+\frac{1}{4}\right)\right) = 2^{\frac{1}{2}-2z} \sqrt{\pi} \Gamma\left(2z + \frac{1}{2}\right)
$$

将这两个结果相乘，我们得到：

$$
P(z) = \left(2^{1-2z} \sqrt{\pi} \Gamma(2z)\right) \cdot \left(2^{\frac{1}{2}-2z} \sqrt{\pi} \Gamma\left(2z + \frac{1}{2}\right)\right) = 2^{\frac{3}{2}-4z} \pi \left[\Gamma(2z) \Gamma\left(2z + \frac{1}{2}\right)\right]
$$

我们再次在方括号内的表达式上应用[倍角公式](@entry_id:173961) (这次令参数为 $2z$)：

$$
\Gamma(2z) \Gamma\left(2z + \frac{1}{2}\right) = 2^{1-4z} \sqrt{\pi} \Gamma(4z)
$$

代入上式，最终得到 $n=4$ 的乘法公式：

$$
P(z) = 2^{\frac{3}{2}-4z} \pi \left(2^{1-4z} \sqrt{\pi} \Gamma(4z)\right) = 2^{\frac{5}{2}-8z} \pi^{\frac{3}{2}} \Gamma(4z)
$$

这个推导过程不仅证明了 $n=4$ 的情况，更重要的是它揭示了乘法公式背后的一种“[自相似](@entry_id:274241)”的递归结构。

Gauss 乘法公式的一个直接应用是计算由 Gamma 函数在有理数点上取值构成的特定乘积。例如，我们可以利用该公式计算 $\Gamma\left(\frac{1}{5}\right) \Gamma\left(\frac{2}{5}\right) \Gamma\left(\frac{3}{5}\right) \Gamma\left(\frac{4}{5}\right)$ 的值 [@problem_id:672432]。这个乘积可以写作 $\prod_{k=1}^{4} \Gamma(k/5)$。
我们应用 Gauss 乘法公式，取 $n=5$ 和 $z=1/5$：

$$
\prod_{k=0}^{4} \Gamma\left(\frac{1}{5} + \frac{k}{5}\right) = (2\pi)^{\frac{5-1}{2}} 5^{\frac{1}{2}-5(\frac{1}{5})} \Gamma\left(5 \cdot \frac{1}{5}\right)
$$

展开左侧乘积：

$$
\Gamma\left(\frac{1}{5}\right) \Gamma\left(\frac{2}{5}\right) \Gamma\left(\frac{3}{5}\right) \Gamma\left(\frac{4}{5}\right) \Gamma(1) = (2\pi)^2 \cdot 5^{-\frac{1}{2}} \cdot \Gamma(1)
$$

由于 $\Gamma(1)=1$，我们可以消去等式两边的 $\Gamma(1)$，得到：

$$
\Gamma\left(\frac{1}{5}\right) \Gamma\left(\frac{2}{5}\right) \Gamma\left(\frac{3}{5}\right) \Gamma\left(\frac{4}{5}\right) = \frac{4\pi^2}{\sqrt{5}}
$$

这个结果再次展示了乘法公式在处理此类问题上的简洁与高效。

### 在简化复杂乘积中的应用

Gauss 乘法公式的威力远不止于计算特定常数。它在符号计算中扮演着重要角色，尤其是在处理涉及 **Pochhammer 符号**（或称上升[阶乘](@entry_id:266637)）的表达式时。Pochhammer 符号 $(x)_n$ 定义为：

$$
(x)_n = x(x+1)\cdots(x+n-1) = \frac{\Gamma(x+n)}{\Gamma(x)}
$$

利用这层关系，许多复杂的 Pochhammer 符号乘积可以通过 Gamma 函数的乘法公式得到惊人的简化。考虑如下表达式 [@problem_id:672233]：

$$
E(z, n) = \frac{(z)_n \left(z+\frac{1}{3}\right)_n \left(z+\frac{2}{3}\right)_n}{(3z)_{3n}}
$$

首先，我们将分子中的每个 Pochhammer 符号都用 Gamma 函数表示：

$$
(z)_n \left(z+\frac{1}{3}\right)_n \left(z+\frac{2}{3}\right)_n = \frac{\Gamma(z+n)}{\Gamma(z)} \cdot \frac{\Gamma(z+\frac{1}{3}+n)}{\Gamma(z+\frac{1}{3})} \cdot \frac{\Gamma(z+\frac{2}{3}+n)}{\Gamma(z+\frac{2}{3})} = \frac{\prod_{k=0}^{2} \Gamma\left((z+n)+\frac{k}{3}\right)}{\prod_{k=0}^{2} \Gamma\left(z+\frac{k}{3}\right)}
$$

现在，我们可以对分子和分母的乘积分别应用 Gauss 乘法公式 ($n=3$)。对于分母，我们直接应用公式。对于分子，我们将参数替换为 $z+n$：

- 分子乘积: $(2\pi) \cdot 3^{\frac{1}{2}-3(z+n)} \Gamma(3(z+n)) = (2\pi) \cdot 3^{\frac{1}{2}-3z-3n} \Gamma(3z+3n)$
- 分母乘积: $(2\pi) \cdot 3^{\frac{1}{2}-3z} \Gamma(3z)$

两式相除，得到：

$$
\frac{(2\pi) \cdot 3^{\frac{1}{2}-3z-3n} \Gamma(3z+3n)}{(2\pi) \cdot 3^{\frac{1}{2}-3z} \Gamma(3z)} = 3^{-3n} \frac{\Gamma(3z+3n)}{\Gamma(3z)} = 3^{-3n} (3z)_{3n}
$$

因此，原表达式 $E(z, n)$ 可以被简化为：

$$
E(z, n) = \frac{3^{-3n} (3z)_{3n}}{(3z)_{3n}} = 3^{-3n}
$$

这个结果出人意料地简洁，它表明原先看似复杂的、依赖于 $z$ 和 $n$ 的表达式，实际上是一个只与 $n$ 有关的常数。这种强大的简化能力是乘法公式在理论物理中（例如，在计算散射振幅的[圈积分](@entry_id:194719)时）被广泛应用的原因之一 [@problem_id:672240]。

同样地，该公式也可以用来简化 Gamma 函数自身的乘积之比。例如，考虑函数 [@problem_id:672223]：

$$
F(z) = \frac{\displaystyle\prod_{k=0}^{3} \Gamma\left(z+\frac{k}{4}\right)}{\displaystyle\prod_{k=0}^{1} \Gamma\left(2z+\frac{k}{2}\right)}
$$

分子是 Gauss 乘法公式中 $n=4$ 的情形，而分母是 $n=2$ (Legendre 公式) 的情形，但其参数为 $2z$。分别应用公式：

- 分子: $\prod_{k=0}^{3} \Gamma\left(z+\frac{k}{4}\right) = (2\pi)^{\frac{3}{2}} 4^{\frac{1}{2}-4z} \Gamma(4z)$
- 分母: $\prod_{k=0}^{1} \Gamma\left(2z+\frac{k}{2}\right) = (2\pi)^{\frac{1}{2}} 2^{\frac{1}{2}-2(2z)} \Gamma(2(2z)) = (2\pi)^{\frac{1}{2}} 2^{\frac{1}{2}-4z} \Gamma(4z)$

将两者相除，$\Gamma(4z)$ 项被消去：

$$
F(z) = \frac{(2\pi)^{\frac{3}{2}} (2^2)^{\frac{1}{2}-4z}}{(2\pi)^{\frac{1}{2}} 2^{\frac{1}{2}-4z}} = (2\pi) \frac{2^{1-8z}}{2^{\frac{1}{2}-4z}} = 2\pi \cdot 2^{1-8z - (\frac{1}{2}-4z)} = 2\pi \cdot 2^{\frac{1}{2}-4z} = \pi 2^{\frac{3}{2}-4z}
$$

最终的表达式 $F(z)$ 仍然依赖于 $z$，但其形式已大大简化，并且不再包含 Gamma 函数。

### 与其他 Gamma 函数恒等式的相互作用

在解决实际问题时，乘法公式很少孤立使用。它常常与 Gamma 函数的其他基本性质，如递推关系 $\Gamma(z+1) = z\Gamma(z)$ 和 Euler [反射公式](@entry_id:198841) $\Gamma(z)\Gamma(1-z) = \frac{\pi}{\sin(\pi z)}$，协同作用。掌握如何组合使用这些工具是深入理解特殊函数的关键。

考虑一个更具挑战性的计算任务：求 $\Gamma\left(\frac{1}{3}\right)\Gamma\left(\frac{5}{6}\right)\Gamma\left(\frac{4}{3}\right)$ 的值 [@problem_id:672461]。这里没有一个单一的公式能直接解决问题。我们需要分步进行：
1.  **简化参数**：利用[递推关系](@entry_id:189264) $\Gamma(z+1)=z\Gamma(z)$，我们可以简化 $\Gamma(4/3)$：
    $$
    \Gamma\left(\frac{4}{3}\right) = \Gamma\left(1+\frac{1}{3}\right) = \frac{1}{3}\Gamma\left(\frac{1}{3}\right)
    $$
    于是原表达式变为 $\frac{1}{3} \Gamma\left(\frac{1}{3}\right)^2 \Gamma\left(\frac{5}{6}\right)$。

2.  **建立联系**：我们需要找到 $\Gamma(1/3)$ 和 $\Gamma(5/6)$ 之间的联系。直接联系不易找到，但我们可以通过 $\Gamma(1/6)$ 作为桥梁。利用 Legendre [倍角公式](@entry_id:173961)，设 $z=1/6$：
    $$
    \Gamma\left(\frac{1}{6}\right)\Gamma\left(\frac{1}{6}+\frac{1}{2}\right) = \Gamma\left(\frac{1}{6}\right)\Gamma\left(\frac{2}{3}\right) = 2^{1-2/6} \sqrt{\pi} \Gamma(2/6) = 2^{2/3}\sqrt{\pi}\Gamma\left(\frac{1}{3}\right)
    $$
3.  **替换与求解**：上式中出现了 $\Gamma(2/3)$，我们可以用[反射公式](@entry_id:198841)将其与 $\Gamma(1/3)$ 联系起来：
    $$
    \Gamma\left(\frac{2}{3}\right) = \Gamma\left(1-\frac{1}{3}\right) = \frac{\pi}{\sin(\pi/3)\Gamma(1/3)} = \frac{2\pi}{\sqrt{3}\Gamma(1/3)}
    $$
    将此结果代入第2步的式子：
    $$
    \Gamma\left(\frac{1}{6}\right) \cdot \frac{2\pi}{\sqrt{3}\Gamma(1/3)} = 2^{2/3}\sqrt{\pi}\Gamma\left(\frac{1}{3}\right)
    $$
    整理后可得 $\Gamma(1/6)$ 与 $\Gamma(1/3)^2$ 的关系。然而，更直接的路径是利用[反射公式](@entry_id:198841)处理 $\Gamma(5/6)$：
    $$
    \Gamma\left(\frac{5}{6}\right) = \Gamma\left(1-\frac{1}{6}\right) = \frac{\pi}{\sin(\pi/6)\Gamma(1/6)} = \frac{2\pi}{\Gamma(1/6)}
    $$
    现在，我们将第2步和第3步的结果结合，解出 $\Gamma(1/6)$，再代入上式。这个过程虽然繁琐，但它展示了在面对复杂问题时，如何灵活地组合运用各种恒等式，将未知量逐步转化为已知量或相互关联的量。完成所有代数运算后，可以得到一个确定的[闭合形式](@entry_id:271343)解。

### 对数与导数形式：与多重 Gamma 函数的关联

对 Gauss 乘法公式两边取对数，我们得到一个关于对数 Gamma 函数的和式恒等式：

$$
\sum_{k=0}^{n-1} \ln\Gamma\left(z+\frac{k}{n}\right) = \frac{n-1}{2}\ln(2\pi) + \left(\frac{1}{2}-nz\right)\ln n + \ln\Gamma(nz)
$$

这个形式在某些应用中更为方便。更有趣的是，通过对这个对数形式的公式求导，我们可以得到一系列关于 **多重 Gamma 函数** (Polygamma functions) 的乘法公式。多重 Gamma 函数 $\psi^{(m)}(z)$ 定义为对数 Gamma 函数的 $m+1$ 阶导数：

$$
\psi^{(m)}(z) = \frac{d^{m+1}}{dz^{m+1}} \ln\Gamma(z)
$$

其中 $m=0$ 对应 **digamma 函数** $\psi(z)$，$m=1$ 对应 **trigamma 函数** $\psi^{(1)}(z)$，以此类推。

对对数乘法公式求 $m+1$ 次导数 ($m \ge 1$)，右边的线性项和常数项消失，我们得到一个非常简洁的公式：

$$
\sum_{k=0}^{n-1} \psi^{(m)}\left(z+\frac{k}{n}\right) = n^{m+1} \psi^{(m)}(nz)
$$

这个公式在计算多重 Gamma 函数在[有理点](@entry_id:195164)上的值的和时非常有用。例如，我们可以用它来计算 **tetragamma 函数** ($m=2$) 的一个和式 [@problem_id:672167]：

$$
S = \sum_{k=0}^{2} \psi^{(2)}\left(\frac{1}{6}+\frac{k}{3}\right)
$$

这里 $n=3$, $z=1/6$。应用上述导数公式 ($m=2$)：

$$
S = 3^{2+1} \psi^{(2)}\left(3 \cdot \frac{1}{6}\right) = 27 \psi^{(2)}\left(\frac{1}{2}\right)
$$

问题转化为计算 $\psi^{(2)}(1/2)$。利用多重 Gamma 函数的[级数表示](@entry_id:175860)：
$\psi^{(m)}(z) = (-1)^{m+1} m! \sum_{j=0}^{\infty} (z+j)^{-(m+1)}$。
当 $z=1/2$ 且 $m=2$ 时：

$$
\psi^{(2)}\left(\frac{1}{2}\right) = (-1)^{3} 2! \sum_{j=0}^{\infty} \frac{1}{(j+1/2)^3} = -2 \sum_{j=0}^{\infty} \frac{8}{(2j+1)^3} = -16 \sum_{j=0}^{\infty} \frac{1}{(2j+1)^3}
$$

奇数倒数三次方之和与 Riemann zeta 函数 $\zeta(3)$ 有关：$\sum_{j=0}^{\infty} \frac{1}{(2j+1)^3} = (1 - 2^{-3})\zeta(3) = \frac{7}{8}\zeta(3)$。因此：

$$
\psi^{(2)}\left(\frac{1}{2}\right) = -16 \cdot \frac{7}{8}\zeta(3) = -14\zeta(3)
$$

最终，我们得到和式的值：

$$
S = 27 \cdot (-14\zeta(3)) = -378\zeta(3)
$$

这个例子揭示了 Gamma 函数乘法公式、多重 Gamma 函数以及 Riemann zeta 函数之间的深刻联系。值得注意的是，对于 digamma 函数 ($m=0$)，由于 $\ln n$ 项的存在，其乘法公式稍有不同 [@problem_id:653874]，需要单独处理。

### 渐近行为与 [Stirling 近似](@entry_id:137296)

除了精确的代数关系，Gauss 乘法公式还与 Gamma 函数的渐近行为密切相关。**[Stirling 近似](@entry_id:137296)公式** 描述了当 $|z| \to \infty$ 时 $\ln\Gamma(z)$ 的行为：

$$
\ln\Gamma(z) \approx \left(z-\frac{1}{2}\right)\ln(z) - z + \frac{1}{2}\ln(2\pi)
$$

将 [Stirling 近似](@entry_id:137296)与对数乘法公式结合，可以用来分析 Gamma 函数和式的渐近极限。考虑如[下极限](@entry_id:145282)问题 [@problem_id:672331]：

$$
L = \lim_{z\to+\infty} \left[ \sum_{k=0}^{2} \ln\Gamma\left(z+\frac{k}{3}\right) - \left(3z-\frac{1}{2}\right)\ln(z) + 3z \right]
$$

直接对和式中的每一项使用 [Stirling 近似](@entry_id:137296)会非常繁琐。更优雅的方法是先用对数乘法公式 ($n=3$) 替换和式：

$$
\sum_{k=0}^{2} \ln\Gamma\left(z+\frac{k}{3}\right) = \ln(2\pi) + \left(\frac{1}{2}-3z\right)\ln 3 + \ln\Gamma(3z)
$$

将此代入极限表达式中：

$$
L = \lim_{z\to+\infty} \left[ \ln(2\pi) + \left(\frac{1}{2}-3z\right)\ln 3 + \ln\Gamma(3z) - \left(3z-\frac{1}{2}\right)\ln(z) + 3z \right]
$$

现在，我们对 $\ln\Gamma(3z)$ 使用 [Stirling 近似](@entry_id:137296)，令参数为 $3z$：

$$
\ln\Gamma(3z) \approx \left(3z-\frac{1}{2}\right)\ln(3z) - 3z + \frac{1}{2}\ln(2\pi)
$$

代入并展开 $\ln(3z) = \ln 3 + \ln z$：

$$
\ln\Gamma(3z) \approx \left(3z-\frac{1}{2}\right)(\ln 3 + \ln z) - 3z + \frac{1}{2}\ln(2\pi)
$$

将这个近似式代入 $L$ 的表达式中，我们观察到大量的项会相互抵消：

- $\left(3z-\frac{1}{2}\right)\ln z$ 项被减去，正好抵消。
- $-3z$ 项与 $+3z$ 项抵消。
- $\ln 3$ 相关的项：$(\frac{1}{2}-3z)\ln 3 + (3z-\frac{1}{2})\ln 3 = 0$，也抵消了。

所有依赖于 $z$ 的主项都消失了，只剩下常数项：

$$
L = \ln(2\pi) + \frac{1}{2}\ln(2\pi) = \frac{3}{2}\ln(2\pi)
$$

这个结果表明，尽管表达式中的每一项都趋于无穷，但它们的组合却收敛到一个优美的常数。这完美地展示了 Gauss 乘法公式作为一个精确的结[构性关系](@entry_id:195492)，如何在[渐近分析](@entry_id:160416)中保持代数上的一致性，并揭示了函数组合的深层行为。

总而言之，Legendre 和 Gauss 乘法公式是理解 Gamma 函数不可或缺的工具。它们不仅提供了具体的计算方法，更揭示了 Gamma 函数在复平面上的对称性和内在结构，并将其与数学中其他核心概念，如 Pochhammer 符号、多重 Gamma 函数、Riemann zeta 函数及[渐近分析](@entry_id:160416)，紧密地联系在一起。