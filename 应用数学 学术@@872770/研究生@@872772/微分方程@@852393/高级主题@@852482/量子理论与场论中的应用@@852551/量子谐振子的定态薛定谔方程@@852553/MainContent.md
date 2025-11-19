## 引言
[量子谐振子](@entry_id:140678)是量子力学中一个至关重要的模型，它不仅是少数几个能够精确求解的系统之一，更是理解微观世界[振荡](@entry_id:267781)和波动的基石。从[分子振动](@entry_id:140827)到[晶格](@entry_id:196752)[声子](@entry_id:140728)，再到[量子场论](@entry_id:138177)中的粒子激发，[谐振子模型](@entry_id:178080)无处不在。其核心问题在于求解描述粒子在二次[势阱](@entry_id:151413)中运动的定态薛定谔方程，以确定其允许的能量[状态和](@entry_id:193625)对应的[波函数](@entry_id:147440)。本文旨在填补从基础概念到高级应用之间的知识鸿沟，为读者提供一个全面而深入的视角。

通过本文的学习，您将掌握量子谐振子问题的两种主要求解方法，并理解其物理性质和跨学科的重要性。在“**原理与机制**”一章中，我们将首先采用直接[求解微分方程](@entry_id:137471)的解析方法，引出厄米多项式和分立的能谱；随后，我们将介绍更为强大和抽象的代数方法，即利用[升降算符](@entry_id:197899)来构建整个能级阶梯，并探讨定态的物理性质。接下来，在“**应用与跨学科联系**”一章中，我们将展示该模型如何应用于分子物理、凝聚态系统、[量子统计](@entry_id:143815)以及[波动光学](@entry_id:271428)和[相对论量子力学](@entry_id:148643)等看似无关的领域，揭示其背后的普适性。最后，在“**动手实践**”部分，一系列精心设计的问题将引导您运用所学知识解决具体问题，加深对算符操作和模型应用的理解。

## 原理与机制

本章在前一章介绍量子谐振子重要性的基础上，深入探讨其核心的物理原理和数学机制。我们将从两个主要角度来求解一维[量子谐振子](@entry_id:140678)的[定态](@entry_id:137260)薛定谔方程：第一种是直接[求解微分方程](@entry_id:137471)的解析方法，第二种是更为抽象和强大的代数方法（或称算符方法）。随后，我们将利用这些结果来分析谐振子本征态的物理性质，并将其推广到更复杂的情形。

### 谐振子的薛定谔方程：直接求解法

一维[量子谐振子](@entry_id:140678)描述了一个质量为 $m$ 的粒子在二次谐振势 $V(x) = \frac{1}{2}m\omega^2x^2$ 中的运动，其中 $\omega$ 是[振子](@entry_id:271549)的经典[角频率](@entry_id:261565)。其[不含时薛定谔方程](@entry_id:154468)为：
$$
-\frac{\hbar^2}{2m} \frac{d^2\psi(x)}{dx^2} + \frac{1}{2}m\omega^2x^2\psi(x) = E\psi(x)
$$
其中 $\hbar$ 是约化普朗克常数，$E$ 是系统的[能量本征值](@entry_id:144381)，$\psi(x)$ 是对应的能量本征函数。

为了找到物理上可接受的解，[波函数](@entry_id:147440) $\psi(x)$ 必须在 $x \to \pm\infty$ 时趋于零，以保证其可归一化。当 $|x|$ 很大时，[势能](@entry_id:748988)项 $\frac{1}{2}m\omega^2x^2$ 远大于任何有限的能量 $E$，薛定谔方程近似为：
$$
\frac{d^2\psi(x)}{dx^2} \approx \frac{m^2\omega^2}{\hbar^2}x^2\psi(x)
$$
这个方程的渐进行为表明，解函数具有高斯形式 $\exp(-\frac{m\omega}{2\hbar}x^2)$。这启发我们为[基态](@entry_id:150928)（能量最低的态）寻找一个具有此形式的精确解。

#### [基态](@entry_id:150928)的求解

我们假设[基态](@entry_id:150928)[波函数](@entry_id:147440)的形式为一个高斯函数 [@problem_id:1160951]：
$$
\psi_0(x) = A \exp(-\beta x^2)
$$
其中 $A$ 是归一化常数，$\beta$ 是一个待定正常数。我们将这个“试探解”（ansatz）代入薛定谔方程。首先计算其[二阶导数](@entry_id:144508)：
$$
\frac{d\psi_0}{dx} = -2\beta x \psi_0(x)
$$
$$
\frac{d^2\psi_0}{dx^2} = (-2\beta)\psi_0(x) + (-2\beta x)(-2\beta x \psi_0(x)) = (4\beta^2 x^2 - 2\beta)\psi_0(x)
$$
代入薛定谔方程后，等式两边消去共同因子 $\psi_0(x)$：
$$
-\frac{\hbar^2}{2m}(4\beta^2 x^2 - 2\beta) + \frac{1}{2}m\omega^2x^2 = E_0
$$
整理后得到：
$$
\left(-\frac{2\hbar^2\beta^2}{m} + \frac{1}{2}m\omega^2\right)x^2 + \frac{\hbar^2\beta}{m} = E_0
$$
为了使这个方程对所有 $x$ 都成立， $x^2$ 的系数必须为零。这给出了对参数 $\beta$ 的约束：
$$
-\frac{2\hbar^2\beta^2}{m} + \frac{1}{2}m\omega^2 = 0 \implies \beta^2 = \frac{m^2\omega^2}{4\hbar^2}
$$
由于 $\beta$ 必须为正实数以确保[波函数](@entry_id:147440)在无穷远处衰减，我们取其正平方根：
$$
\beta = \frac{m\omega}{2\hbar}
$$
将此 $\beta$ 值代入方程中的常数项，我们便得到[基态能量](@entry_id:263704) $E_0$：
$$
E_0 = \frac{\hbar^2\beta}{m} = \frac{\hbar^2}{m} \left(\frac{m\omega}{2\hbar}\right) = \frac{1}{2}\hbar\omega
$$
这个结果是量子力学中的一个里程碑：[量子谐振子](@entry_id:140678)的最低能量（即**[零点能](@entry_id:142176)**）不是零，而是 $\frac{1}{2}\hbar\omega$。这与经典物理中粒子可以静止在[势阱](@entry_id:151413)底部的观念截然不同，是海森堡不确定性原理的直接体现。

#### [激发态](@entry_id:261453)与宇称

为了寻找[激发态](@entry_id:261453)，我们可以在[高斯函数](@entry_id:261394)前乘以一个 $x$ 的多项式。对于第一[激发态](@entry_id:261453)，我们基于其[波函数](@entry_id:147440)应具有[奇宇称](@entry_id:147965)（即 $\psi_1(-x) = -\psi_1(x)$）的预期，选择试探解为 [@problem_id:1161134]：
$$
\psi_1(x) = A x \exp(-\beta x^2)
$$
将这个形式代入薛定谔方程，通过与[基态](@entry_id:150928)求解类似的步骤——即要求方程对所有 $x$ 成立，需使不同 $x$ 次方的系数分别满足等式——我们能同时确定 $\beta$（结果与[基态](@entry_id:150928)相同，$\beta = \frac{m\omega}{2\hbar}$）和第一[激发态](@entry_id:261453)的能量：
$$
E_1 = \frac{3}{2}\hbar\omega
$$
继续这一过程，可以发现第 $n$ 个能级的[能量本征值](@entry_id:144381)为 $E_n = \hbar\omega(n + \frac{1}{2})$，而对应的[波函数](@entry_id:147440)则与 $n$ 阶**厄米多项式**（Hermite polynomials） $H_n$ 相关。

#### 通解与归一化

一维量子谐振子的第 $n$ 个归一化能量本征函数的一般形式为：
$$
\psi_n(x) = N_n H_n(\alpha x) \exp\left(-\frac{1}{2}\alpha^2 x^2\right)
$$
其中 $\alpha = \sqrt{\frac{m\omega}{\hbar}}$ 是一个方便的[尺度因子](@entry_id:266678)，而 $N_n$ 是归一化常数。[归一化条件](@entry_id:156486)要求[波函数](@entry_id:147440)模平方在全[空间的积](@entry_id:151742)分为1，即 $\int_{-\infty}^{\infty} |\psi_n(x)|^2 dx = 1$。
为了计算这个积分，我们利用厄米多项式的[正交关系](@entry_id:145540)式 [@problem_id:1160952]：
$$
\int_{-\infty}^{\infty} H_n(y) H_k(y) e^{-y^2} dy = \sqrt{\pi} 2^n n! \delta_{nk}
$$
其中 $\delta_{nk}$ 是克罗内克符号。通过变量代换 $y = \alpha x$，我们可以求解归一化常数 $N_n$：
$$
|N_n|^2 \int_{-\infty}^{\infty} [H_n(\alpha x)]^2 e^{-\alpha^2 x^2} dx = |N_n|^2 \frac{1}{\alpha} \int_{-\infty}^{\infty} [H_n(y)]^2 e^{-y^2} dy = 1
$$
代入积分公式，我们得到：
$$
|N_n|^2 \frac{1}{\alpha} \sqrt{\pi} 2^n n! = 1
$$
解出 $N_n$ (取正实数) 得：
$$
N_n = \sqrt{\frac{\alpha}{\sqrt{\pi} 2^n n!}} = \left(\frac{m\omega}{\pi\hbar}\right)^{1/4} \frac{1}{\sqrt{2^n n!}}
$$
至此，我们通过直接求解微分方程的方法，完整地确定了量子谐振子的[能谱](@entry_id:181780)和对应的归一化[波函数](@entry_id:147440)。然而，这种方法对于计算物理量的[期望值](@entry_id:153208)或处理更复杂的问题显得相当繁琐。

### 代数方法：[升降算符](@entry_id:197899)

代数方法为[量子谐振子](@entry_id:140678)问题提供了一个更为优雅和深刻的视角。其核心思想是引入一对算符，它们能够让我们在不同能级之间“攀爬”，而无需直接处理厄米多项式和复杂的积分。

#### [升降算符](@entry_id:197899)的定义与对易关系

我们定义**[湮灭算符](@entry_id:165390)** $\hat{a}$ 和**[产生算符](@entry_id:191512)** $\hat{a}^\dagger$ 如下 [@problem_id:1160936]：
$$
\hat{a} = \sqrt{\frac{m\omega}{2\hbar}} \left( \hat{x} + \frac{i}{m\omega} \hat{p} \right)
$$
$$
\hat{a}^\dagger = \sqrt{\frac{m\omega}{2\hbar}} \left( \hat{x} - \frac{i}{m\omega} \hat{p} \right)
$$
注意，$\hat{a}^\dagger$ 是 $\hat{a}$ 的[厄米共轭](@entry_id:191215)。这两个算符不是[厄米算符](@entry_id:153410)，因此不对应于可观测的物理量。它们的价值在于其代数性质。其中最基本、最重要的性质是它们之间的[对易关系](@entry_id:136780)。利用[正则对易关系](@entry_id:185041) $[\hat{x}, \hat{p}] = i\hbar$，我们可以直接计算 $[\hat{a}, \hat{a}^\dagger]$：
$$
[\hat{a}, \hat{a}^\dagger] = \frac{m\omega}{2\hbar} \left[ \hat{x} + \frac{i}{m\omega} \hat{p}, \hat{x} - \frac{i}{m\omega} \hat{p} \right]
$$
利用对易子的[双线性](@entry_id:146819)和反对称性质，展开上式：
$$
[\hat{a}, \hat{a}^\dagger] = \frac{m\omega}{2\hbar} \left( [\hat{x}, \hat{x}] - \frac{i}{m\omega}[\hat{x}, \hat{p}] + \frac{i}{m\omega}[\hat{p}, \hat{x}] - \left(\frac{i}{m\omega}\right)^2[\hat{p}, \hat{p}] \right)
$$
由于任何算符与自身的对易子为零，且 $[\hat{p}, \hat{x}] = -[\hat{x}, \hat{p}] = -i\hbar$，上式简化为：
$$
[\hat{a}, \hat{a}^\dagger] = \frac{m\omega}{2\hbar} \left( - \frac{i}{m\omega}(i\hbar) + \frac{i}{m\omega}(-i\hbar) \right) = \frac{m\omega}{2\hbar} \left( \frac{\hbar}{m\omega} + \frac{\hbar}{m\omega} \right) = 1
$$
这个简洁的结果 $[\hat{a}, \hat{a}^\dagger] = 1$ 是整个代数方法的基础。

#### [哈密顿量](@entry_id:172864)与[能谱](@entry_id:181780)

下一步是将[哈密顿量](@entry_id:172864) $\hat{H}$ 用 $\hat{a}$ 和 $\hat{a}^\dagger$ 表示。首先，我们可以反解出 $\hat{x}$ 和 $\hat{p}$：
$$
\hat{x} = \sqrt{\frac{\hbar}{2m\omega}}(\hat{a} + \hat{a}^\dagger)
$$
$$
\hat{p} = i\sqrt{\frac{m\hbar\omega}{2}}(\hat{a}^\dagger - \hat{a})
$$
将它们代入[哈密顿量](@entry_id:172864) $\hat{H} = \frac{\hat{p}^2}{2m} + \frac{1}{2}m\omega^2\hat{x}^2$，经过一番代数运算并利用 $[\hat{a}, \hat{a}^\dagger] = 1$ (即 $\hat{a}\hat{a}^\dagger = 1 + \hat{a}^\dagger\hat{a}$)，可以得到一个极为简洁的表达式：
$$
\hat{H} = \hbar\omega \left(\hat{a}^\dagger \hat{a} + \frac{1}{2}\right)
$$
这个形式的[哈密顿量](@entry_id:172864)，连同一个被称为**[粒子数算符](@entry_id:153568)**的厄米算符 $\hat{N} = \hat{a}^\dagger \hat{a}$，极大地简化了求解过程。$\hat{H}$ 和 $\hat{N}$ 拥有共同的本征态，记为 $|n\rangle$。若 $\hat{N}|n\rangle = n|n\rangle$，则 $\hat{H}|n\rangle = \hbar\omega(n+\frac{1}{2})|n\rangle = E_n|n\rangle$。

现在我们来考察 $\hat{a}$ 和 $\hat{a}^\dagger$ 对[能量本征态](@entry_id:152154)的作用。利用 $[\hat{N}, \hat{a}] = -\hat{a}$ 和 $[\hat{N}, \hat{a}^\dagger] = \hat{a}^\dagger$ (这两个关系可由 $[\hat{a}, \hat{a}^\dagger] = 1$ 导出)，可以证明：
- 如果 $|n\rangle$ 是能量为 $E_n$ 的[本征态](@entry_id:149904)，那么 $\hat{a}|n\rangle$ 是能量为 $E_n - \hbar\omega$ 的[本征态](@entry_id:149904)。
- 如果 $|n\rangle$ 是能量为 $E_n$ 的本征态，那么 $\hat{a}^\dagger|n\rangle$ 是能量为 $E_n + \hbar\omega$ 的本征态。
因此，$\hat{a}^\dagger$ 将系统提升一个能量级，称为[产生算符](@entry_id:191512)；$\hat{a}$ 将系统降低一个能量级，称为[湮灭算符](@entry_id:165390)。

由于系统能量必须有下限（[势能](@entry_id:748988)是正定的），必须存在一个不能再被降低的[基态](@entry_id:150928) $|0\rangle$。这意味着对[基态](@entry_id:150928)应用湮灭算符会得到[零矢量](@entry_id:155273)：
$$
\hat{a}|0\rangle = 0
$$
将此作用于[哈密顿量](@entry_id:172864)，我们立即得到[基态能量](@entry_id:263704)：
$$
\hat{H}|0\rangle = \hbar\omega(\hat{a}^\dagger \hat{a} + \frac{1}{2})|0\rangle = \hbar\omega(\hat{a}^\dagger(0) + \frac{1}{2}|0\rangle) = \frac{1}{2}\hbar\omega|0\rangle
$$
这与我们用直接法得到的结果 $E_0 = \frac{1}{2}\hbar\omega$ 完全一致。从[基态](@entry_id:150928)出发，我们可以通过重复应用[产生算符](@entry_id:191512)来构建整个能级阶梯：
$$
E_n = \hbar\omega\left(n + \frac{1}{2}\right), \quad n = 0, 1, 2, \dots
$$
归一化的本征态由下式给出：
$$
|n\rangle = \frac{1}{\sqrt{n!}}(\hat{a}^\dagger)^n |0\rangle
$$
我们可以利用这个公式来具体构造任意[激发态](@entry_id:261453)的[波函数](@entry_id:147440)。例如，要得到第二[激发态](@entry_id:261453) $\psi_2(x)$ [@problem_id:1160937]，我们首先需要[基态](@entry_id:150928)[波函数](@entry_id:147440) $\psi_0(x)$。通过求解[一阶微分方程](@entry_id:173139) $\hat{a}\psi_0(x)=0$，即 $\left(x + \frac{\hbar}{m\omega} \frac{d}{dx}\right)\psi_0(x) = 0$，可以得到（未归一化的）$\psi_0(x) \propto \exp(-\frac{m\omega}{2\hbar}x^2)$。然后，我们应用[产生算符](@entry_id:191512)两次：
$$
\psi_2(x) \propto (\hat{a}^\dagger)^2 \psi_0(x) = \left(\sqrt{\frac{m\omega}{2\hbar}}\right)^2 \left(x - \frac{\hbar}{m\omega} \frac{d}{dx}\right)^2 \exp\left(-\frac{m\omega}{2\hbar}x^2\right)
$$
经过计算和归一化后，可以得到与直接法一致的 $\psi_2(x)$ 的表达式，它正比于二阶厄米多项式 $H_2$ 乘以高斯因子。

### [定态](@entry_id:137260)的物理性质

拥有了能谱和[本征函数](@entry_id:154705)后，我们可以探究谐振子在[定态](@entry_id:137260) $|n\rangle$ 下的各种物理性质。

#### 动能与势能的[期望值](@entry_id:153208)：维里定理

一个重要的关系是[定态](@entry_id:137260)中动能[期望值](@entry_id:153208) $\langle \hat{T} \rangle$ 与势能[期望值](@entry_id:153208) $\langle \hat{V} \rangle$ 的关系。对于[谐振子势](@entry_id:750179)，它们是相等的。这可以作为更普适的**[维里定理](@entry_id:146441)**的一个特例来证明。一种优雅的证明方法是考虑算符 $\hat{G} = \frac{1}{2}(\hat{x}\hat{p} + \hat{p}\hat{x})$ 在[哈密顿量](@entry_id:172864)本征态 $|n\rangle$ 中的[期望值](@entry_id:153208) [@problem_id:1161123]。对于任何定态，任意算符 $\hat{A}$ 的[期望值](@entry_id:153208)不随时间改变，这导致 $\langle n | [\hat{H}, \hat{A}] | n \rangle = 0$。我们计算 $[\hat{H}, \hat{G}]$：
$$
[\hat{H}, \hat{G}] = [\hat{T} + \hat{V}, \hat{G}] = [\hat{T}, \hat{G}] + [\hat{V}, \hat{G}]
$$
利用[正则对易关系](@entry_id:185041)，可以分别计算出：
$$
[\hat{T}, \hat{G}] = \left[\frac{\hat{p}^2}{2m}, \frac{1}{2}(\hat{x}\hat{p} + \hat{p}\hat{x})\right] = -2i\hbar \hat{T}
$$
$$
[\hat{V}, \hat{G}] = \left[\frac{1}{2}m\omega^2\hat{x}^2, \frac{1}{2}(\hat{x}\hat{p} + \hat{p}\hat{x})\right] = 2i\hbar \hat{V}
$$
因此，$[\hat{H}, \hat{G}] = 2i\hbar(\hat{V} - \hat{T})$。其在定态 $|n\rangle$ 中的[期望值](@entry_id:153208)为零：
$$
\langle n | [\hat{H}, \hat{G}] | n \rangle = 2i\hbar(\langle \hat{V} \rangle_n - \langle \hat{T} \rangle_n) = 0
$$
这直接导出 $\langle \hat{T} \rangle_n = \langle \hat{V} \rangle_n$。由于总能量 $E_n = \langle \hat{H} \rangle_n = \langle \hat{T} \rangle_n + \langle \hat{V} \rangle_n$，我们立刻得到：
$$
\langle \hat{T} \rangle_n = \langle \hat{V} \rangle_n = \frac{1}{2}E_n = \frac{1}{2}\hbar\omega\left(n + \frac{1}{2}\right)
$$
这个结果也可以通过**[Hellmann-Feynman定理](@entry_id:173798)**得到 [@problem_id:1160972]。该定理指出，$\frac{dE_n}{d\lambda} = \langle n | \frac{\partial\hat{H}}{\partial\lambda} | n \rangle$。若取参数 $\lambda = \omega$，则 $\frac{\partial\hat{H}}{\partial\omega} = m\omega\hat{x}^2 = \frac{2\hat{V}}{\omega}$。同时 $\frac{dE_n}{d\omega} = \hbar(n+\frac{1}{2})$。联立可得 $\langle \hat{V} \rangle_n = \frac{1}{2}\hbar\omega(n+\frac{1}{2})$，与维里定理结果一致。

#### 物理量的涨落

尽管定态的总能量是确定的（[能量涨落](@entry_id:148029)为零），但其他物理量如动能、势能、位置和动量等，通常具有非零的涨落或不确定度。例如，我们可以计算动能的不确定度 $\Delta T = \sqrt{\langle \hat{T}^2 \rangle - \langle \hat{T} \rangle^2}$ [@problem_id:1160935]。这需要计算 $\langle \hat{T}^2 \rangle = \frac{1}{4m^2}\langle \hat{p}^4 \rangle$。利用[升降算符](@entry_id:197899)表示的[动量算符](@entry_id:151743)，可以计算出 $\langle \hat{p}^4 \rangle$ 在态 $|n\rangle$ 中的[期望值](@entry_id:153208)，最终得到动能的不确定度：
$$
\Delta T = \frac{\hbar\omega}{2\sqrt{2}}\sqrt{n^2+n+1}
$$
这表明，除了在某些特定情况下，动能的测量值会围绕其平均值 $\frac{1}{2}E_n$ [分布](@entry_id:182848)，其[分布](@entry_id:182848)宽度随量子数 $n$ 的增加而增加。

### 超出标准一维模型的讨论

[量子谐振子](@entry_id:140678)模型是解决更复杂问题的基石。

#### 经典对应

量子力学在宏观极限下（即量子数 $n \to \infty$）应过渡到经典力学。对于谐振子，我们可以比较[量子概率](@entry_id:184796)密度 $|\psi_n(x)|^2$ 和经典概率密度 $P_{cl}(x)$ [@problem_id:1160934]。经典粒子在某点 $x$ 附近被找到的概率正比于它在该处停留的时间，反比于其速度 $v(x)$。对于总能量为 $E$ 的[经典谐振子](@entry_id:153404)，$v(x) = \sqrt{\frac{2}{m}(E - \frac{1}{2}m\omega^2x^2)}$。归一化后的经典[概率密度](@entry_id:175496)为：
$$
P_{cl}(x) = \frac{1}{\pi\sqrt{a^2-x^2}}
$$
其中 $a=\sqrt{2E/m\omega^2}$ 是振幅。该[分布](@entry_id:182848)在[粒子速度](@entry_id:196946)最慢的[经典转折点](@entry_id:155557) $x=\pm a$ 处达到最大。而[量子概率](@entry_id:184796)密度 $|\psi_n(x)|^2$ 在[经典禁区](@entry_id:149063)外指数衰减（隧道效应），在经典允许区内[振荡](@entry_id:267781)。当 $n$ 很大时，$|\psi_n(x)|^2$ 的[振荡](@entry_id:267781)[包络线](@entry_id:174062)会逐渐趋近于经典概率密度 $P_{cl}(x)$，这正是**[玻尔对应原理](@entry_id:155683)**的一个完美范例。

#### 高维[谐振子](@entry_id:155622)与简并

对于二维或三维谐振子，如果势能是各向同性的，如 $V(x,y) = \frac{1}{2}m\omega^2(x^2+y^2)$，问题可以在[笛卡尔坐标系](@entry_id:169789)中分离变量，总能量为 $E_{n_x,n_y} = \hbar\omega(n_x+n_y+1)$。由于不同的量子数组合 $(n_x, n_y)$ 可以得到相同的总能量（例如 $n_x+n_y=N$），能级会出现**简并**。

如果势能是各向异性的，如 $\omega_y = 2\omega_x$ [@problem_id:1161118]，总能量为 $E_{n_x,n_y} = \hbar\omega_x(n_x+2n_y+3/2)$。简并的出现取决于是否存在不同的整数对 $(n_x, n_y)$ 使得 $n_x+2n_y$ 的值相同。例如，对于 $n_x+2n_y=2$，存在 $(n_x,n_y)=(2,0)$ 和 $(0,1)$ 两种状态，它们具有相同的能量 $E = \hbar\omega_x(2+3/2)$，因此该能级是二重简并的。

在极坐标下处理二维[各向同性谐振子](@entry_id:190656)时，会出现一个包含[离心势垒](@entry_id:147153)的有效径向势 $V_{\text{eff}}(r) = \frac{1}{2}m\omega^2r^2 + \frac{\hbar^2 m_l^2}{2mr^2}$，其中 $m_l$ 是角动量量子数 [@problem_id:1160959]。这个有效势的极小值位置 $r_0 = \sqrt{\frac{\hbar|m_l|}{m\omega}}$ 对应于具有确定角动量的经典粒子的[稳定圆形轨道](@entry_id:164103)半径。

最后，我们也可以分析对标准[哈密顿量](@entry_id:172864)的微小修改。例如，如果加入一个与动量成正比的项 $\gamma \hat{p}$，可以通过完成平方的方法或直接求解发现，它仅仅是使整个能谱发生一个固定的能量平移 $E \to E - \frac{m\gamma^2}{2}$，而能级间的间隔 $\hbar\omega$ 保持不变。这说明我们为标准[谐振子](@entry_id:155622)发展的求解技术具有广泛的适用性。