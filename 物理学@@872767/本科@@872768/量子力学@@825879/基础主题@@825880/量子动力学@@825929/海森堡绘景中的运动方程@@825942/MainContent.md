## 引言
在量子力学的世界里，描述一个系统如何随时间演化是其核心任务之一。通常，我们习惯于[薛定谔绘景](@entry_id:144112)，其中系统的状态（[波函数](@entry_id:147440)）是时间的函数，而像位置、动量这样的[物理可观测量](@entry_id:154692)则由不随时间变化的算符来表示。然而，这并非唯一的视角。存在一种与之完[全等](@entry_id:273198)价但概念上截然不同的描述方式——[海森堡绘景](@entry_id:141162)。它颠覆了我们通常的直觉：在这里，[量子态](@entry_id:146142)本身是静止的、永恒不变的，而所有的时间演化信息都蕴含在算符自身的动态变化之中。

这种视角的转换不仅仅是数学上的游戏，它解决了一个根本性的问题：如何更直接地将[量子动力学](@entry_id:138183)与我们所熟知的经典力学联系起来？[海森堡绘景](@entry_id:141162)通过其核心的运动方程，优雅地构建了[量子对易子](@entry_id:194337)与经典泊松括号之间的桥梁，使得牛顿定律和哈密顿方程在量子世界中找到了惊人的对应形式。这为我们理解[对称性与守恒](@entry_id:154858)定律的关系提供了前所未有的清晰度。本文旨在系统地介绍[海森堡绘景](@entry_id:141162)，帮助读者掌握这一强大的理论工具。

在接下来的章节中，我们将踏上一段从基础到应用的探索之旅。在**第一章：原理与机制**中，我们将推导[海森堡运动方程](@entry_id:140445)，并通过[自由粒子](@entry_id:148748)、[谐振子](@entry_id:155622)等经典案例，深入理解其物理内涵以及与[埃伦费斯特定理](@entry_id:151868)的联系。随后，在**第二章：应用与[交叉](@entry_id:147634)学科联系**中，我们将视野扩展到更广阔的物理领域，探讨[海森堡绘景](@entry_id:141162)如何被用于分析原子物理中的[自旋进动](@entry_id:149995)、凝聚态物理中的[集体激发](@entry_id:145026)乃至[相对论量子力学](@entry_id:148643)中的奇特效应。最后，在**第三章：动手实践**中，你将有机会通过解决具体问题来巩固所学知识，亲身体验运用海森堡方程分析量子系统的过程。通过这一系列的学习，你将能够从一个新的维度把握量子动力学的精髓。

## 原理与机制

在量子力学中，系统的动力学可以通过两种等价的绘景来描述：[薛定谔绘景](@entry_id:144112)和[海森堡绘景](@entry_id:141162)。在前面章节介绍的[薛定谔绘景](@entry_id:144112)中，系统的状态矢量（[波函数](@entry_id:147440)）随[时间演化](@entry_id:153943)，而对应于[物理可观测量](@entry_id:154692)（如位置、动量）的算符通常是固定不变的。然而，[海森堡绘景](@entry_id:141162)提供了一种替代的、同样深刻的视角。在这种绘景中，系统的状态矢量是恒定的，而算符本身则包含了全部的时间演化信息。这种方法不仅在形式上与经典哈密顿力学有着惊人的相似之处，而且为理解[守恒定律](@entry_id:269268)和系统对称性提供了强有力的工具。本章将深入探讨[海森堡绘景](@entry_id:141162)的原理及其核心机制——[海森堡运动方程](@entry_id:140445)。

### [海森堡运动方程](@entry_id:140445)

在[海森堡绘景](@entry_id:141162)中，一个物理可观测量 $A$ 对应的算符 $A_H(t)$ 的时间演化，是由其在[薛定谔绘景](@entry_id:144112)中对应的算符 $A_S$（通常是时间无关的）通过一个幺正变换来定义的：

$$
A_H(t) = U^\dagger(t) A_S U(t)
$$

其中 $U(t) = \exp(-iHt/\hbar)$ 是[时间演化算符](@entry_id:196774)，而 $H$ 是系统的[哈密顿量](@entry_id:172864)。为了找到算符 $A_H(t)$ 如何随时间变化的[动力学方程](@entry_id:751029)，我们对其求时间导数：

$$
\frac{dA_H}{dt} = \frac{\partial U^\dagger}{\partial t} A_S U + U^\dagger A_S \frac{\partial U}{\partial t} + U^\dagger \frac{\partial A_S}{\partial t} U
$$

由于 $H$ 被假定为不显含时间，我们有 $\frac{\partial U}{\partial t} = -\frac{i}{\hbar}HU$ 和 $\frac{\partial U^\dagger}{\partial t} = \frac{i}{\hbar}U^\dagger H$。代入上式，得到：

$$
\frac{dA_H}{dt} = \frac{i}{\hbar}U^\dagger H A_S U - \frac{i}{\hbar}U^\dagger A_S H U + \left(\frac{\partial A_S}{\partial t}\right)_H
$$

注意到 $U^\dagger H A_S U = (U^\dagger H U) (U^\dagger A_S U) = H_H A_H$，并且 $U^\dagger A_S H U = (U^\dagger A_S U) (U^\dagger H U) = A_H H_H$。如果[哈密顿量](@entry_id:172864)本身不显含时间，那么 $H_H = U^\dagger H U = H$。因此，方程可以被重写为：

$$
\frac{dA_H(t)}{dt} = \frac{i}{\hbar}[H, A_H(t)] + \left(\frac{\partial A_S}{\partial t}\right)_H
$$

这就是著名的 **[海森堡运动方程](@entry_id:140445)**。方程的第一项描述了由系统[哈密顿量](@entry_id:172864)驱动的内在动力学，形式上是算符 $A_H$ 与[哈密顿量](@entry_id:172864) $H$ 的对易子。第二项 $(\frac{\partial A_S}{\partial t})_H$ 表示在[薛定谔绘景](@entry_id:144112)中算符本身的任何显式时间依赖性，经过变换后进入[海森堡绘景](@entry_id:141162)。对于大多数基本的可观测量，如位置、动量和自旋，其在[薛定谔绘景](@entry_id:144112)中的算符是不显含时间的，因此这一项为零。

### 与经典力学的联系

[海森堡运动方程](@entry_id:140445)最引人注目的特点之一是它与经典[哈密顿力学](@entry_id:146202)的深刻类比。在经典力学中，一个物理量 $f(q, p, t)$ 的[全时间导数](@entry_id:172646)由泊松括号给出：$\frac{df}{dt} = \{f, H\} + \frac{\partial f}{\partial t}$。量子力学中的对应关系是 $\frac{1}{i\hbar}[\cdot, \cdot] \leftrightarrow \{\cdot, \cdot\}$。这种对应关系不仅仅是形式上的，它揭示了[量子动力学](@entry_id:138183)在某种极限下回归到[经典动力学](@entry_id:177360)，这就是所谓的 **[埃伦费斯特定理](@entry_id:151868) (Ehrenfest's Theorem)**。取[海森堡运动方程](@entry_id:140445)的[期望值](@entry_id:153208)，我们得到：

$$
\frac{d\langle A \rangle}{dt} = \frac{i}{\hbar}\langle [H, A] \rangle + \left\langle \frac{\partial A}{\partial t} \right\rangle
$$

这个结果表明，可观测量[期望值的时间演化](@entry_id:153265)遵循一个由[量子对易子](@entry_id:194337)决定的定律。

让我们通过几个具体的例子来感受这种联系的力量。

#### 恒[力场](@entry_id:147325)中的粒子

考虑一个质量为 $m$ 的粒子在一维恒[力场](@entry_id:147325) $F$ 中运动，其[势能](@entry_id:748988)为 $V(x) = -Fx$。系统的[哈密顿量](@entry_id:172864)是 $H = \frac{p^2}{2m} - Fx$。我们来计算[动量算符](@entry_id:151743) $p_H(t)$ 的时间演化 [@problem_id:2092074]。根据[海森堡运动方程](@entry_id:140445)：

$$
\frac{dp_H(t)}{dt} = \frac{i}{\hbar}[H, p_H(t)] = \frac{i}{\hbar} \left[ \frac{p_H^2}{2m} - Fx_H, p_H \right]
$$

由于 $p_H$ 与自身及其任意次方都对易，即 $[p_H^2, p_H] = 0$，我们只需要计算：

$$
\frac{dp_H(t)}{dt} = \frac{i}{\hbar} [-Fx_H, p_H] = -\frac{iF}{\hbar}[x_H, p_H]
$$

使用基本对易关系 $[x_H(t), p_H(t)] = i\hbar$（我们稍后将证明这个关系在时间演化中保持不变），我们得到：

$$
\frac{dp_H(t)}{dt} = -\frac{iF}{\hbar}(i\hbar) = F
$$

这个结果 $\frac{d p_H}{dt} = F$ 是牛顿第二定律在[量子力学中的算符](@entry_id:262952)形式。它表明，在恒[力场](@entry_id:147325)中，[动量算符](@entry_id:151743)以一个恒定的速率变化，其速率就是经典力的大小。

#### 量子谐振子

现在考虑一个更复杂的系统：一维量子谐振子，其[哈密顿量](@entry_id:172864)为 $H = \frac{p^2}{2m} + \frac{1}{2}m\omega^2 x^2$。我们可以求解位置和[动量算符](@entry_id:151743)的[运动方程](@entry_id:170720) [@problem_id:2092081]。

首先是位置算符 $x_H(t)$：

$$
\frac{dx_H(t)}{dt} = \frac{i}{\hbar}[H, x_H] = \frac{i}{\hbar} \left[ \frac{p_H^2}{2m}, x_H \right] = \frac{i}{2m\hbar} [p_H^2, x_H]
$$

利用[对易关系](@entry_id:136780)恒等式 $[A^2, B] = A[A,B] + [A,B]A$ 和 $[p_H, x_H] = -i\hbar$，我们有 $[p_H^2, x_H] = p_H(-i\hbar) + (-i\hbar)p_H = -2i\hbar p_H$。因此：

$$
\frac{dx_H(t)}{dt} = \frac{i}{2m\hbar}(-2i\hbar p_H) = \frac{p_H(t)}{m}
$$

这个结果与经典物理中速度的定义完全一致。

接下来是[动量算符](@entry_id:151743) $p_H(t)$：

$$
\frac{dp_H(t)}{dt} = \frac{i}{\hbar}[H, p_H] = \frac{i}{\hbar} \left[ \frac{1}{2}m\omega^2 x_H^2, p_H \right] = \frac{im\omega^2}{2\hbar} [x_H^2, p_H]
$$

同样地，我们有 $[x_H^2, p_H] = x_H[x_H, p_H] + [x_H, p_H]x_H = x_H(i\hbar) + (i\hbar)x_H = 2i\hbar x_H$。代入得到：

$$
\frac{dp_H(t)}{dt} = \frac{im\omega^2}{2\hbar}(2i\hbar x_H) = -m\omega^2 x_H(t)
$$

综上所述，我们得到了一组耦合的算符[微分方程](@entry_id:264184)：

$$
\frac{dx_H(t)}{dt} = \frac{p_H(t)}{m}, \quad \frac{dp_H(t)}{dt} = -m\omega^2 x_H(t)
$$

这组方程在形式上与描述[经典谐振子](@entry_id:153404)的[哈密顿方程](@entry_id:156213)是完全相同的。这清晰地展示了[量子动力学](@entry_id:138183)与[经典动力学](@entry_id:177360)之间深刻的结构性联系。

#### [自由粒子](@entry_id:148748)

[自由粒子](@entry_id:148748)是上述情况的一个特例，其中势能 $V(x)=0$。此时[哈密顿量](@entry_id:172864)为 $H = p^2/2m$。动量的运动方程变为 $\frac{dp_H}{dt} = \frac{i}{\hbar}[p_H^2/2m, p_H] = 0$，这意味着[动量算符](@entry_id:151743)是一个不随时间变化的常量：$p_H(t) = p_H(0) \equiv p$。

位置的[运动方程](@entry_id:170720)仍然是 $\frac{dx_H}{dt} = \frac{p_H}{m} = \frac{p}{m}$。这是一个简单的[微分方程](@entry_id:264184)，其解为：

$$
x_H(t) = x_H(0) + \frac{p}{m}t \equiv x + \frac{p}{m}t
$$

这个结果与我们对自由粒子在经典世界中运动的直觉完全吻合。利用这个解，我们可以计算更复杂的算符，例如位置平方算符 $x_H^2(t)$ [@problem_id:2092076]。由于 $x$ 和 $p$ 不对易，我们必须小心处理乘法顺序：

$$
x_H^2(t) = \left(x + \frac{t}{m}p\right)^2 = \left(x + \frac{t}{m}p\right)\left(x + \frac{t}{m}p\right) = x^2 + \frac{t}{m}(xp + px) + \frac{t^2}{m^2}p^2
$$

中间的交叉项被写成了对称化的形式 $xp+px$，这直接反映了算符的非对易性。此外，我们注意到，在[哈密顿量](@entry_id:172864)中增加一个常数势能 $V_0$ 并不会改变任何对易子 $[H, x]$ 或 $[H, p]$ 的值，因为常数与所有算符都对易。因此，一个恒定的[势能](@entry_id:748988)背景不会影响[可观测量](@entry_id:267133)的动力学演化，这与经典力学中[势能](@entry_id:748988)零点的选择是任意的这一事实相一致 [@problem_id:2092104]。

### [对称性与守恒](@entry_id:154858)定律

[海森堡绘景](@entry_id:141162)为理解物理学中最深刻的联系之一——[对称性与守恒](@entry_id:154858)定律之间的关系——提供了一个清晰的框架。从[海森堡运动方程](@entry_id:140445) $\frac{dA_H}{dt} = \frac{i}{\hbar}[H, A_H]$（假设 $A_S$ 不显含时间）可以立即得出一个核心结论：

**如果一个[可观测量](@entry_id:267133)的算符 $A$ 与[哈密顿量](@entry_id:172864) $H$ 对易（即 $[A, H] = 0$），那么该算符在[海森堡绘景](@entry_id:141162)中就是时间无关的，即 $\frac{dA_H}{dt} = 0$。这个[可观测量](@entry_id:267133)就是一个[守恒量](@entry_id:150267)，或称为[运动常数](@entry_id:150267)。**

这个原理是诺特定理（Noether's theorem）在量子力学中的体现。[哈密顿量](@entry_id:172864)的某种对称性，表现为它与某个操作（如平移、旋转）的算符对易，直接导致与该操作相关的物理量守恒。

#### 角动量守恒

考虑一个粒子在三维[中心势](@entry_id:148563)场 $V(r)$ 中运动，其中 $r = \sqrt{x^2+y^2+z^2}$。[哈密顿量](@entry_id:172864)为 $H = \frac{\vec{P}^2}{2m} + V(r)$。这种[哈密顿量](@entry_id:172864)在空间旋转下是不变的，我们期望角动量是守恒的。让我们来验证角动量的 $z$ 分量 $L_z = X P_y - Y P_x$ 是否守恒 [@problem_id:2092102]。我们需要计算 $[L_z, H]$。

首先，$[L_z, \vec{P}^2] = [L_z, P_x^2] + [L_z, P_y^2] + [L_z, P_z^2]$。利用基本[对易关系](@entry_id:136780)可以证明，这个对易子为零。

接下来，计算 $[L_z, V(r)]$。由于 $V(r)$ 只是位置算符的函数，它与位置算符对易，但与动量算符不对易。计算结果为：

$$
[L_z, V(r)] = -i\hbar\left(X\frac{\partial V}{\partial y}-Y\frac{\partial V}{\partial x}\right)
$$

对于[中心势](@entry_id:148563)，$V$ 仅通过 $r$ 依赖于坐标，因此其[偏导数](@entry_id:146280)为 $\frac{\partial V}{\partial x} = \frac{dV}{dr}\frac{\partial r}{\partial x} = V'(r)\frac{X}{r}$ 和 $\frac{\partial V}{\partial y} = V'(r)\frac{Y}{r}$。代入上式：

$$
[L_z, V(r)] = -i\hbar\left(X \frac{V'(r)Y}{r} - Y \frac{V'(r)X}{r}\right) = -\frac{i\hbar V'(r)}{r}(XY - YX) = 0
$$

因为 $[X,Y]=0$。所以，我们证明了 $[L_z, H] = 0$。根据我们的原理，这意味着 $\frac{dL_{z,H}}{dt} = 0$，$L_z$ 是一个[守恒量](@entry_id:150267)。对于任意态，其[期望值](@entry_id:153208) $\langle L_z \rangle$ 也是一个不随时间变化的常数。

#### [宇称不守恒](@entry_id:160658)的例子

现在看一个对称性被破坏的例子。考虑一个处于均匀静电场 $\mathcal{E}$ 中的[谐振子](@entry_id:155622)，其[哈密顿量](@entry_id:172864)为 $H = \frac{p_x^2}{2m} + \frac{1}{2}m\omega^2 x^2 - q\mathcal{E}x$ [@problem_id:2092114]。线性项 $-q\mathcal{E}x$ 破坏了系统的空间[反演对称性](@entry_id:269948)。[宇称算符](@entry_id:148434) $\Pi$ 的作用是 $\Pi x \Pi^{-1} = -x$ 和 $\Pi p_x \Pi^{-1} = -p_x$。[谐振子](@entry_id:155622)部分 $H_0 = \frac{p_x^2}{2m} + \frac{1}{2}m\omega^2 x^2$ 是宇称不变的，即 $[H_0, \Pi] = 0$。但是，对于整个[哈密顿量](@entry_id:172864)：

$$
[H, \Pi] = [H_0 - q\mathcal{E}x, \Pi] = -q\mathcal{E}[x, \Pi]
$$

从 $\Pi x = -x\Pi$ 可以推导出 $[x, \Pi] = x\Pi - \Pi x = x\Pi - (-x\Pi) = 2x\Pi$。因此：

$$
[H, \Pi] = -2q\mathcal{E}x\Pi \neq 0
$$

由于[哈密顿量](@entry_id:172864)与[宇称算符](@entry_id:148434)不对易，宇称不再是守恒量。其[时间演化](@entry_id:153943)由海森堡方程给出：

$$
\frac{d\Pi_H(t)}{dt} = \frac{i}{\hbar}[H, \Pi_H(t)] = \frac{i}{\hbar}(-2q\mathcal{E} x_H(t) \Pi_H(t)) = -\frac{2iq\mathcal{E}}{\hbar} x_H(t) \Pi_H(t)
$$

这个非零结果表明，如果系统初始处于一个宇称确定的状态，它将不会一直保持在该状态。对称性的破坏直接导致了相应[守恒定律](@entry_id:269268)的失效。

### 求解运动方程：以[谐振子](@entry_id:155622)为例

[海森堡运动方程](@entry_id:140445)不仅是形式上的工具，它们也是可以被求解的[微分方程](@entry_id:264184)。对于量子谐振子，使用产生和[湮灭算符](@entry_id:165390) $a$ 和 $a^\dagger$ 会使问题大大简化。[哈密顿量](@entry_id:172864)可以写成 $H = \hbar \omega (a^\dagger a + \frac{1}{2})$，它们满足对易关系 $[a, a^\dagger] = 1$。

让我们求解[湮灭算符](@entry_id:165390) $a_H(t)$ 的运动方程 [@problem_id:2092064] [@problem_id:2092066]。首先计算对易子：

$$
[H, a] = [\hbar \omega (a^\dagger a + \frac{1}{2}), a] = \hbar\omega [a^\dagger a, a] = \hbar\omega(a^\dagger[a,a] + [a^\dagger, a]a) = \hbar\omega(0 + (-1)a) = -\hbar\omega a
$$

根据海森堡方程：

$$
\frac{da_H(t)}{dt} = \frac{i}{\hbar}[H, a_H(t)] = \frac{i}{\hbar}(-\hbar\omega a_H(t)) = -i\omega a_H(t)
$$

这是一个简单的[一阶线性常微分方程](@entry_id:164502)，其解为：

$$
a_H(t) = a_H(0) \exp(-i\omega t) = a_S \exp(-i\omega t)
$$

类似地，可以求得[产生算符](@entry_id:191512)的解为 $a_H^\dagger(t) = a_S^\dagger \exp(i\omega t)$。这些解非常优美：在[海森堡绘景](@entry_id:141162)中，谐振子的产生和[湮灭算符](@entry_id:165390)（量子力学中的“[简正模](@entry_id:139640)”）以经典的[振荡频率](@entry_id:269468) $\omega$ 进行简单的谐波演化。

### 高级应用与形式属性

#### 对易关系的保持

量子力学的一个基本支柱是[正则对易关系](@entry_id:185041)，如 $[x, p] = i\hbar$。一个自然的问题是：这个关系在[时间演化](@entry_id:153943)中是否保持不变？也就是说，$[x_H(t), p_H(t)]$ 是否恒等于 $i\hbar$？我们可以通过计算其时间导数来验证这一点 [@problem_id:2092093]。利用导数的莱布尼兹律：

$$
\frac{d}{dt}[A_H, B_H] = \left[\frac{dA_H}{dt}, B_H\right] + \left[A_H, \frac{dB_H}{dt}\right]
$$

对于一个一般的[哈密顿量](@entry_id:172864) $H = \frac{p^2}{2m} + V(x)$，我们已经知道 $\frac{dx_H}{dt} = \frac{p_H}{m}$ 和 $\frac{dp_H}{dt} = -\frac{\partial V(x_H)}{\partial x_H}$。代入上式：

$$
\frac{d}{dt}[x_H, p_H] = \left[\frac{p_H}{m}, p_H\right] + \left[x_H, -\frac{\partial V}{\partial x_H}\right]
$$

第一项 $[\frac{p_H}{m}, p_H]$ 为零，因为 $p_H$ 与自身对易。第二项 $[x_H, -\frac{\partial V}{\partial x_H}]$ 也为零，因为 $\frac{\partial V}{\partial x_H}$ 是 $x_H$ 的函数，而 $x_H$ 与自身的任意函数都对易。因此：

$$
\frac{d}{dt}[x_H(t), p_H(t)] = 0
$$

这表明 $[x_H(t), p_H(t)]$ 是一个不随时间变化的量。由于在 $t=0$ 时它等于 $[x_S, p_S] = i\hbar$，所以它在所有时刻都等于 $i\hbar$。基本对易关系是动力学演化的一个[不变量](@entry_id:148850)，这保证了量子理论在时间演化过程中的自洽性。

#### [量子维里定理](@entry_id:176645)

[海森堡绘景](@entry_id:141162)的框架也是推导一些深刻物理定理的有力工具，例如 **[量子维里定理](@entry_id:176645) (quantum virial theorem)**。该定理建立了在定态中，系统[平均动能](@entry_id:146353)与平均[势能](@entry_id:748988)之间的关系。

考虑一个处于[哈密顿量](@entry_id:172864) $H$ 的[本征态](@entry_id:149904)（定态）$|\psi\rangle$ 的系统。对于任何不显含时间的算符 $G$，其[期望值](@entry_id:153208) $\langle G \rangle = \langle \psi | G | \psi \rangle$ 是不随时间变化的。因此，$\frac{d\langle G \rangle}{dt} = 0$。根据[埃伦费斯特定理](@entry_id:151868)，这意味着 $\langle [H, G] \rangle = 0$。

我们选择一个特殊的算符，称为维里算符 $G = \vec{x} \cdot \vec{p}$（更严格地说是其厄米化形式 $\frac{1}{2}(\vec{x} \cdot \vec{p} + \vec{p} \cdot \vec{x})$）。通过计算对易子 $[H, G]$，我们可以得到一个有用的关系 [@problem_id:2092068]。计算过程表明：

$$
[H, G] = \left[\frac{\vec{p}^2}{2m} + V(\vec{x}), \vec{x} \cdot \vec{p}\right] = i\hbar \left(-\frac{\vec{p}^2}{m} + \vec{x} \cdot \nabla V\right)
$$

（这里为了简化，我们使用了非厄米形式的 $G$，但最终结果相同）。因此，在[定态](@entry_id:137260)下 $\langle [H, G] \rangle = 0$ 意味着：

$$
\left\langle -\frac{\vec{p}^2}{m} + \vec{x} \cdot \nabla V \right\rangle = 0
$$

注意到动能 $T = \frac{\vec{p}^2}{2m}$，上式可以写为：

$$
2\langle T \rangle = \langle \vec{x} \cdot \nabla V \rangle
$$

这就是[量子维里定理](@entry_id:176645)的一般形式。对于一个[幂律](@entry_id:143404)[中心势](@entry_id:148563) $V(r) = \alpha r^n$，我们有 $\vec{x} \cdot \nabla V = n V$。在这种情况下，[维里定理](@entry_id:146441)简化为 $2\langle T \rangle = n \langle V \rangle$。如果我们知道系统的总能量 $E = \langle T \rangle + \langle V \rangle$，就可以利用这个关系分别求解[平均动能](@entry_id:146353)和平均势能：

$$
\langle T \rangle = \frac{n}{n+2} E, \quad \langle V \rangle = \frac{2}{n+2} E
$$

例如，对于[库仑势](@entry_id:154276)（$n=-1$），我们有 $2\langle T \rangle = -\langle V \rangle$；对于[谐振子势](@entry_id:750179)（$n=2$），我们有 $2\langle T \rangle = 2\langle V \rangle$，即 $\langle T \rangle = \langle V \rangle$。这些都是量子力学中非常著名且有用的结果。

总之，[海森堡绘景](@entry_id:141162)和它的运动方程不仅提供了一种与[薛定谔绘景](@entry_id:144112)等价的动力学描述，更重要的是，它揭示了量子力学与经典力学之间深刻的结构对应，阐明了[对称性与守恒](@entry_id:154858)定律的内在联系，并为求解量子系统的动力学演化和推导普适定理提供了强大的数学框架。