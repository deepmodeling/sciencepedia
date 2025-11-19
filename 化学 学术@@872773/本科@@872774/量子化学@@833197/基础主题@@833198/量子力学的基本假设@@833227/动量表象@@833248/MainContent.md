## 引言
在量子力学的学习中，我们通常首先接触的是位置表象，它通过[波函数](@entry_id:147440) $\psi(x)$ 来描述粒子的状态。这种方法虽然直观，但在处理许多物理问题时，尤其是在涉及散射、周期性系统或[动量守恒](@entry_id:149964)的场景中，并非总是最有效或最具洞察力的工具。动量，作为与位置同等重要的基本物理量，提供了一个全新的、功能强大的视角来审视量子世界。

这就引出了一个关键问题：我们能否构建一个以动量为基础的数学框架，从而简化某些特定问题的求解，并揭示位置表象中不甚明显的物理规律？动量表象正是对这个问题的回答，它不仅是另一种数学技巧，更是一种深刻的物理观念。

本文将系统地引导你进入动量表象的世界。在“原理与机制”一章中，我们将通过[傅里叶变换](@entry_id:142120)建立[动量空间波函数](@entry_id:272371)，并学习核心算符的表达形式。接着，在“应用与[交叉](@entry_id:147634)学科联系”中，我们将看到动量表象如何应用于解决从基础量子现象到凝聚态物理中的具体问题。最后，“动手实践”部分将提供精选的练习，帮助你巩固所学知识并将其付诸实践。通过掌握这一强大的分析工具，你将能够更灵活、更深刻地理解和解决量子力学问题。

## 原理与机制

在量子力学中，我们描述一个系统所选择的数学框架被称为**表象 (representation)**。正如我们可以用不同的[坐标系](@entry_id:156346)（如笛卡尔坐标或极坐标）来描述空间中的同一点，我们也可以用不同的[基矢](@entry_id:199546)集合来展开一个[量子态](@entry_id:146142)。在前面的章节中，我们主要使用了位置表象，其中[量子态](@entry_id:146142)由一个位置的函数——[波函数](@entry_id:147440) $\psi(x)$ 来描述。然而，位置表象并非总是最方便或最具洞察力的选择。

本章将介绍一种与之对偶且功能强大的替代表象——**动量表象 (momentum representation)**。在动量表象中，[量子态](@entry_id:146142)由动量的函数 $\phi(p)$ 来描述。这种视角在处理散射问题、周期性系统（如晶体中的电子）以及任何动量守恒起核心作用的物理过程中，都显示出其独特的优势。我们将系统地阐述动量表象的基本原理，定义其核心算符，并探讨其在解决具体量子问题中的应用。

### [动量空间波函数](@entry_id:272371)

动量表象的基础是**动量算符** $\hat{p}$ 的本征态。这些[本征态](@entry_id:149904)，记为 $|p\rangle$，满足本征方程：
$$
\hat{p} |p\rangle = p |p\rangle
$$
其中 $p$ 是动量[本征值](@entry_id:154894)，是一个实数。与位置本征态 $\{|x\rangle\}$ 构成了位置空间的[完备基](@entry_id:143908)底一样，动量[本征态](@entry_id:149904) $\{|p\rangle\}$ 也构成了[希尔伯特空间](@entry_id:261193)中的一个完备连续基底。

任何一个[量子态](@entry_id:146142) $|\psi\rangle$ 都可以用这个基底来展开。展开系数本身就是一个关于动量 $p$ 的[连续函数](@entry_id:137361)，我们将其定义为**[动量空间波函数](@entry_id:272371)**，记为 $\phi(p)$：
$$
\phi(p) \equiv \langle p | \psi \rangle
$$
这个函数 $\phi(p)$ 包含了关于粒子[动量分布](@entry_id:162113)的全部信息。

位置空间[波函数](@entry_id:147440) $\psi(x) = \langle x | \psi \rangle$ 和[动量空间波函数](@entry_id:272371) $\phi(p)$ 描述的是同一个物理状态，因此它们之间必然存在确定的数学关系。这个关系就是**[傅里叶变换](@entry_id:142120) (Fourier Transform)**。给定一种常见的物理学约定，它们之间的变换对为 [@problem_id:2103678] [@problem_id:1382798]：
$$
\phi(p) = \frac{1}{\sqrt{2\pi\hbar}} \int_{-\infty}^{\infty} \psi(x) \exp\left(-\frac{ipx}{\hbar}\right) dx
$$
$$
\psi(x) = \frac{1}{\sqrt{2\pi\hbar}} \int_{-\infty}^{\infty} \phi(p) \exp\left(\frac{ipx}{\hbar}\right) dp
$$
其中 $\hbar$ 是约化普朗克常数。这两个积分公式构成了连接位置与动量这两个互补世界的桥梁。

与位置[波函数](@entry_id:147440)相似，动量[波函数](@entry_id:147440)也具有概率的诠释。根据量子力学的基本假设，模方 $|\phi(p)|^2$ 代表了在动量空间中找到粒子的**[概率密度](@entry_id:175496) (probability density)**。具体来说，$|\phi(p)|^2 dp$ 是在一次测量中，发现粒子动量在 $p$ 到 $p+dp$ 这个无穷小区间内的概率。因此，要计算粒子动量落在有限区间 $[p_1, p_2]$ 内的总概率，我们只需对[概率密度](@entry_id:175496)进行积分 [@problem_id:1382768]：
$$
P(p_1 \le p \le p_2) = \int_{p_1}^{p_2} |\phi(p)|^2 dp
$$
由于粒子必然具有某个动量值，所以对所有可能的动量积分，总概率必须为1，这就是[归一化条件](@entry_id:156486)：
$$
\int_{-\infty}^{\infty} |\phi(p)|^2 dp = 1
$$

作为一个具体的例子，考虑一个一维粒子，其归一化的动量[波函数](@entry_id:147440)为一个三角形函数 [@problem_id:1382768]。例如，$\phi(p) = C(1 - |p|/p_0)$ 对于 $|p| \le p_0$ 成立，在其他地方为零。通过[归一化条件](@entry_id:156486) $\int_{-p_0}^{p_0} C^2(1 - |p|/p_0)^2 dp = 1$ 可以确定常数 $C$。一旦知道了归一化的[波函数](@entry_id:147440)，我们就可以计算任何动量区间的概率，例如，动量在 $[0, p_0/2]$ 区间的概率可以通过计算积分 $\int_{0}^{p_0/2} |\phi(p)|^2 dp$ 来得到。

### 动量表象中的算符

为了在动量表象中进行完整的量子力学计算，我们必须知道物理可观测量（如动量、位置、能量等）的算符如何作用于动量[波函数](@entry_id:147440) $\phi(p)$。

#### 动量算符 $\hat{p}$

在动量表象中，动量算符的表达形式极其简单。根据定义，$\phi(p)$ 是态矢量在动量本征基上的投影。因此，算符 $\hat{p}$ 作用于态矢量 $|\psi\rangle$ 之后，其在动量表象中的形式为 $\langle p | \hat{p} | \psi \rangle$。利用 $\hat{p}$ 的[厄米性](@entry_id:141899)（$\hat{p}^\dagger = \hat{p}$）和本征方程 $\hat{p}|p\rangle = p|p\rangle$，我们有：
$$
(\hat{p}\phi)(p) \equiv \langle p | \hat{p} | \psi \rangle = p \langle p | \psi \rangle = p\phi(p)
$$
因此，在动量表象中，**[动量算符](@entry_id:151743)** $\hat{p}$ 的作用仅仅是**乘以动量变量** $p$ [@problem_id:1382777]。
$$
\hat{p}_{\text{动量表象}} \rightarrow p
$$
这与位置表象中位置算符 $\hat{x}$ 的作用是乘以 $x$ 完全类似。一个算符在其自身的表象中总是表现为简单的乘法。

#### 位置算符 $\hat{x}$

位置算符 $\hat{x}$ 在动量表象中的形式则不那么平凡。我们可以通过它与[傅里叶变换](@entry_id:142120)的关系来推导。我们想知道 $(\hat{x}\phi)(p) = \langle p | \hat{x} | \psi \rangle$ 是什么。为此，我们插入一个完备的位置[基矢](@entry_id:199546)恒等式 $\int |x\rangle\langle x| dx = 1$：
$$
(\hat{x}\phi)(p) = \int \langle p | \hat{x} | x \rangle \langle x | \psi \rangle dx
$$
由于 $\hat{x}|x\rangle = x|x\rangle$，上式变为：
$$
(\hat{x}\phi)(p) = \int \langle p | x \rangle x \langle x | \psi \rangle dx = \int \langle p | x \rangle x \psi(x) dx
$$
我们知道位置与动量[本征态](@entry_id:149904)的[内积](@entry_id:158127)是平面波 $\langle p | x \rangle = \frac{1}{\sqrt{2\pi\hbar}} \exp(-ipx/\hbar)$。代入后得到：
$$
(\hat{x}\phi)(p) = \frac{1}{\sqrt{2\pi\hbar}} \int [x \psi(x)] \exp(-ipx/\hbar) dx
$$
这个表达式正是函数 $x\psi(x)$ 的[傅里叶变换](@entry_id:142120)。利用[傅里叶变换](@entry_id:142120)的一个重要性质，即变量的乘法对应于变换域中的[微分](@entry_id:158718)，我们可以得到其最终形式。具体来说，观察到：
$$
i\hbar \frac{d}{dp} \exp(-ipx/\hbar) = i\hbar \left(-\frac{ix}{\hbar}\right) \exp(-ipx/\hbar) = x \exp(-ipx/\hbar)
$$
将此关系代入积分中，并将对 $p$ 的[微分](@entry_id:158718)提到积分外，我们得到 [@problem_id:1382789] [@problem_id:1382779]：
$$
(\hat{x}\phi)(p) = \frac{1}{\sqrt{2\pi\hbar}} \int \psi(x) \left(i\hbar \frac{d}{dp} \exp(-ipx/\hbar)\right) dx = i\hbar \frac{d}{dp} \left( \frac{1}{\sqrt{2\pi\hbar}} \int \psi(x) \exp(-ipx/\hbar) dx \right)
$$
括号内的表达式正是 $\phi(p)$ 的定义，因此我们得到了**位置算符**在动量表象中的形式：
$$
\hat{x}_{\text{动量表象}} \rightarrow i\hbar \frac{d}{dp}
$$
这个结果揭示了位置和动量之间深刻的对偶性。在位置表象中，$\hat{x} \rightarrow x$ 且 $\hat{p} \rightarrow -i\hbar \frac{d}{dx}$；而在动量表象中，$\hat{p} \rightarrow p$ 且 $\hat{x} \rightarrow i\hbar \frac{d}{dp}$ [@problem_id:1382779]。两个算符的角色发生了互换，从一个乘法算符变成一个[微分](@entry_id:158718)算符，只是相差一个负号。这个负号的差异源于我们定义[傅里叶变换](@entry_id:142120)对时指数上符号的选择。

#### [正则对易关系](@entry_id:185041)与[期望值](@entry_id:153208)

有了算符的具体形式，我们就可以在动量表象中验证量子力学的基本假设。其中最核心的就是**[正则对易关系](@entry_id:185041)** $[\hat{x}, \hat{p}] = \hat{x}\hat{p} - \hat{p}\hat{x} = i\hbar$。让我们在一个任意的测试函数 $\phi(p)$ 上验证它 [@problem_id:2103674]：
$$
\begin{align*}
[\hat{x}, \hat{p}] \phi(p)  &= \left(i\hbar \frac{d}{dp}\right)(p \phi(p)) - p \left(i\hbar \frac{d}{dp} \phi(p)\right) \\
 &= i\hbar \left( \phi(p) + p \frac{d\phi(p)}{dp} \right) - i\hbar p \frac{d\phi(p)}{dp} \\
 &= i\hbar \phi(p)
\end{align*}
$$
这个结果表明，对易关系 $[\hat{x}, \hat{p}] = i\hbar$ 是一个不依赖于表象的普适算符恒等式，我们的算符定义是自洽的。

同样，我们可以在动量表象中计算任意[可观测量](@entry_id:267133)的**[期望值](@entry_id:153208) (expectation value)**。对于一个由算符 $\hat{A}$ 代表的可观测量 $A$，其[期望值](@entry_id:153208)的通用表达式为：
$$
\langle A \rangle = \int_{-\infty}^{\infty} \phi^*(p) \hat{A}_p \phi(p) dp
$$
其中 $\hat{A}_p$ 是算符 $\hat{A}$ 在动量表象中的形式。例如，位置的[期望值](@entry_id:153208)是 [@problem_id:1382789]：
$$
\langle x \rangle = \int_{-\infty}^{\infty} \phi^*(p) \left(i\hbar \frac{d}{dp}\right) \phi(p) dp
$$
而动量的[期望值](@entry_id:153208)则是：
$$
\langle p \rangle = \int_{-\infty}^{\infty} \phi^*(p) p \phi(p) dp
$$
我们可以利用这个框架计算更复杂的量。例如，要计算位置的平方的[期望值](@entry_id:153208) $\langle x^2 \rangle$，我们需要应用算符 $\hat{x}^2 = (i\hbar \frac{d}{dp})^2 = -\hbar^2 \frac{d^2}{dp^2}$ [@problem_id:1382788]。对于一个由高斯动量[波包](@entry_id:154698) $\phi(p) = N \exp(-\alpha(p-p_0)^2 / (2\hbar^2))$ 描述的粒子，其 $\langle x^2 \rangle$ 的计算过程就涉及到对该函数求[二阶导数](@entry_id:144508)并积分。

### 应用与推论

动量表象不仅是一个自洽的数学框架，更在解决物理问题和理解量子现象中发挥着关键作用。

#### [海森堡不确定性原理](@entry_id:171099)

**[海森堡不确定性原理](@entry_id:171099)**指出，我们无法同时精确地知道一个粒子的位置和动量，其不确定度的乘积有一个下限：$\Delta x \Delta p \ge \hbar/2$。动量表象为这一原理提供了深刻的数学诠释。

位置和动量[波函数](@entry_id:147440)通过[傅里叶变换](@entry_id:142120)联系在一起。[傅里叶变换](@entry_id:142120)的一个基本性质是，一个函数在原[空间分布](@entry_id:188271)越窄（即越局域化），其在变换空间中的[分布](@entry_id:182848)就越宽（即越弥散）。直观地讲，要构建一个空间上非常尖锐的[波包](@entry_id:154698)，你需要叠加大量不同波长（即不同动量）的平面波，这导致其[动量分布](@entry_id:162113)非常广泛。

我们可以通过一个[高斯波包](@entry_id:151158)的例子来定量地验证这一点 [@problem_id:1382796]。考虑一个位置空间中的高斯[波函数](@entry_id:147440) $\psi(x) = A \exp(-ax^2)$。通过直接计算，可以得到其位置不确定度 $\Delta x = \sqrt{\langle x^2 \rangle - \langle x \rangle^2} = 1/(2\sqrt{a})$。其动量不确定度 $\Delta p$ 可以通过[傅里叶变换](@entry_id:142120)得到动量[波函数](@entry_id:147440)（它也是一个[高斯函数](@entry_id:261394)）来计算，也可以直接在位置表象中使用动量算符 $\hat{p} = -i\hbar d/dx$ 计算得到 $\Delta p = \hbar\sqrt{a}$。两者的乘积为：
$$
\Delta x \Delta p = \left( \frac{1}{2\sqrt{a}} \right) (\hbar\sqrt{a}) = \frac{\hbar}{2}
$$
这个结果恰好达到了不确定性原理的下限，这样的波包被称为**最小不确定度[波包](@entry_id:154698)**。这个计算清楚地表明，当我们试图通过增大参数 $a$ 来使粒子在空间上更加局域化（$\Delta x$ 变小）时，其[动量分布](@entry_id:162113)必然会变得更加弥散（$\Delta p$ 变大），以保持其乘积为一个常数。

#### 空间平移与薛定谔方程

动量表象在处理空间变换和求解薛定谔方程时也异常强大。

考虑一个简单的**空间平移**操作，将粒子的[波函数](@entry_id:147440)从 $\psi(x)$ 移动到 $\psi(x-x_0)$。在动量表象中，这个操作会如何体现呢？通过[傅里叶变换](@entry_id:142120)的“[时移定理](@entry_id:173986)”（在这里是“位移定理”），我们可以直接得到结果 [@problem_id:1382798]：
$$
\phi_{\text{new}}(p) = \mathcal{F}[\psi(x-x_0)] = \exp\left(-\frac{ipx_0}{\hbar}\right) \mathcal{F}[\psi(x)] = \exp\left(-\frac{ipx_0}{\hbar}\right) \phi_{\text{old}}(p)
$$
一个在位置空间中的平移，在动量空间中仅仅表现为一个依赖于动量 $p$ 的**相位因子**的乘法。这个简单的关系在固体物理学中至关重要，是[布洛赫定理](@entry_id:137461)的数学基础。

更重要的是，动量表象为求解**定态薛定谔方程** $\hat{H}\psi = E\psi$ 提供了另一条途径。将方程变换到[动量空间](@entry_id:148936)，我们得到：
$$
(\hat{H}\phi)(p) = E\phi(p)
$$
[哈密顿算符](@entry_id:144286) $\hat{H} = \frac{\hat{p}^2}{2m} + V(\hat{x})$ 在动量表象中的形式变为：
$$
\hat{H}_p = \frac{p^2}{2m} + V\left(i\hbar \frac{d}{dp}\right)
$$
动能项变成了一个简单的乘法因子，这通常是使用动量表象的主要动机。然而，势能项 $V(\hat{x})$ 通常会变成一个复杂的[微分](@entry_id:158718)或积分算符。对于一个局域势 $V(x)$，其在动量表象中通常是一个积分算符：
$$
(V(\hat{x})\phi)(p) = \int \tilde{V}(p-p') \phi(p') dp'
$$
其中 $\tilde{V}(q)$ 是[势能函数](@entry_id:200753) $V(x)$ 的[傅里叶变换](@entry_id:142120)。

尽管[势能](@entry_id:748988)项变复杂了，但在某些情况下，动量表象中的方程反而更容易处理。一个经典的例子是**狄拉克 $\delta$ 函数势** $V(x) = -\alpha \delta(x)$ [@problem_id:2103678]。在位置表象，这是一个带有[奇异点](@entry_id:199525)的[微分方程](@entry_id:264184)。而在动量表象中，由于 $\delta$ 函数的[傅里叶变换](@entry_id:142120)是一个常数，薛定谔方程变成一个代数[积分方程](@entry_id:138643)：
$$
\left(\frac{p^2}{2m} - E\right) \phi(p) = \frac{\alpha}{2\pi\hbar} \int_{-\infty}^{\infty} \phi(p') dp'
$$
这个方程可以通过简单的代数运算和积分求解，从而得到该[势阱](@entry_id:151413)中唯一束缚态的能量 $E = -m\alpha^2/(2\hbar^2)$。这个例子雄辩地证明了根据问题选择合适表象的重要性。

### [动量空间](@entry_id:148936)中的[时间演化](@entry_id:153943)

一个[量子态](@entry_id:146142)的动力学由**[含时薛定谔方程](@entry_id:137898)** $i\hbar \frac{\partial}{\partial t}|\Psi(t)\rangle = \hat{H}|\Psi(t)\rangle$ 决定。在动量表象中，它表现为对动量[波函数](@entry_id:147440) $\phi(p,t)$ 的[偏微分方程](@entry_id:141332)：
$$
i\hbar \frac{\partial}{\partial t} \phi(p,t) = \hat{H}_p \phi(p,t)
$$

对于一个**定态 (stationary state)**，即能量的本征态，其[时间演化](@entry_id:153943)非常简单。若初始态为 $\phi(p,0) = \phi_n(p)$，对应能量 $E_n$，则任意时刻的态为：
$$
\phi_n(p,t) = \phi_n(p) \exp(-iE_n t / \hbar)
$$
其动量[概率密度](@entry_id:175496) $|\phi_n(p,t)|^2 = |\phi_n(p)|^2$ 不随时间改变。这正是“定态”的含义。

然而，对于一个由多个能量本征态构成的**叠加态**，情况则变得有趣得多。考虑一个初始态是两个定态 $\phi_1(p)$ 和 $\phi_2(p)$ 的叠加 [@problem_id:1382780]：
$$
\phi(p,0) = c_1 \phi_1(p) + c_2 \phi_2(p)
$$
其时间演化为：
$$
\phi(p,t) = c_1 \phi_1(p) \exp(-iE_1 t / \hbar) + c_2 \phi_2(p) \exp(-iE_2 t / \hbar)
$$
此时的动量概率密度为：
$$
\begin{align*}
|\phi(p,t)|^2  = |c_1 \phi_1(p)|^2 + |c_2 \phi_2(p)|^2 + 2\text{Re}\left[c_1^* c_2 \phi_1^*(p) \phi_2(p) \exp(i(E_1-E_2)t/\hbar)\right]
\end{align*}
$$
除了不随时间变化的项外，还出现了一个**干涉项**，它以角频率 $\omega = (E_2-E_1)/\hbar$ [振荡](@entry_id:267781)。这意味着，对于一个非定态，其动量（和位置）的[概率分布](@entry_id:146404)会随[时间演化](@entry_id:153943)，展现出所谓的**[量子拍](@entry_id:155286) (quantum beats)**。

这个[振荡](@entry_id:267781)行为引出了一个重要现象——**量子复兴 (quantum revival)**。干涉项中的相位因子 $\exp(-i\Delta E t / \hbar)$ 决定了演化的周期性。当时间 $T$ 满足 $\Delta E \cdot T / \hbar = 2\pi k$（其中 $k$ 为整数）时，相位因子回到1，动量[概率分布](@entry_id:146404) $|\phi(p,T)|^2$ 将完全恢复到其初始时刻的形态 $|\phi(p,0)|^2$。对于一个[两能级系统](@entry_id:196082)，其最短的复兴周期为 [@problem_id:1382780]：
$$
T = \frac{2\pi\hbar}{|E_2 - E_1|}
$$
这一现象清晰地展示了[量子动力学](@entry_id:138183)中由[能量量子化](@entry_id:137825)和态[叠加原理](@entry_id:144649)共同导致的相干演化行为。

总之，动量表象不仅是解决量子力学问题的有力工具，它还提供了理解量子世界基本原理（如[不确定性原理](@entry_id:141278)和对偶性）的深刻视角。掌握在不同表象之间灵活切换的能力，是深入理解[量子化学](@entry_id:140193)和物理的关键技能之一。