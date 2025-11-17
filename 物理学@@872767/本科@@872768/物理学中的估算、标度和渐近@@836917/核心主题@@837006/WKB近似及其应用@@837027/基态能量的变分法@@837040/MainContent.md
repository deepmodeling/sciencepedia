## 引言
在量子力学的广阔世界中，精确求解薛定谔方程以揭示系统行为的奥秘，往往仅限于少数高度理想化的模型。对于现实世界中普遍存在的、涉及复杂相互作用的多体系统，我们必须依赖近似方法来获得洞察。其中，变分法（Variational Method）脱颖而出，成为最强大、应用最广泛的近似技术之一，它为我们提供了一种系统性地估算系统基态能量的有效途径。本文旨在填补理论学习与实际应用之间的鸿沟，全面解析变分法的精髓。

我们将通过三个章节的深入探讨，带领读者从基本原理走向前沿应用。在“原理与机制”一章中，我们将奠定[变分法](@entry_id:163656)的理论基石，详细拆解其操作步骤。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章，我们将展示变分法如何作为一种通用框架，在原子物理、凝聚态物理乃至[量子化学](@entry_id:140193)等多个领域解决关键问题。最后，“动手实践”部分将通过具体问题，巩固读者对理论的理解和计算能力。通过本次学习，你将不仅掌握一个强大的计算工具，更能领会一种深刻的物理思维方式，从而能够探索那些无法精确求解的、丰富多彩的量子世界。

## 原理与机制

在量子力学中，精确求解薛定谔方程仅对少数理想化系统是可行的。对于包含复杂相互作用或[多体系统](@entry_id:144006)的绝大多数物理问题，我们必须依赖近似方法。[变分法](@entry_id:163656)（Variational Method）是最强大和应用最广泛的近似技术之一，它为我们估算系统的[基态能量](@entry_id:263704)提供了一个严格的上限。本章将深入探讨变分法的基本原理、实践步骤及其在各种物理情境下的应用。

### 变分原理

[变分法](@entry_id:163656)的数学基础是[瑞利-里兹定理](@entry_id:194531)（Rayleigh-Ritz theorem）。该原理指出：对于一个给定的量子系统，其[哈密顿算符](@entry_id:144286)为 $H$，真实的基态能量为 $E_0$。对于任意一个满足[系统边界](@entry_id:158917)条件的归一化“试探”[波函数](@entry_id:147440) $|\psi\rangle$，其能量的[期望值](@entry_id:153208) $\langle E \rangle$ 永远不会低于真实的基态能量。数学上，这一原理表述为：

$$
\langle E \rangle = \frac{\langle \psi | H | \psi \rangle}{\langle \psi | \psi \rangle} \ge E_0
$$

这个不等式是[变分法](@entry_id:163656)的核心。为了理解其来源，我们可以将任意[试探函数](@entry_id:756165) $|\psi\rangle$ 在[哈密顿算符](@entry_id:144286) $H$ 的完备本征函数基 $|\phi_n\rangle$下展开。这些[本征函数](@entry_id:154705)满足 $H|\phi_n\rangle = E_n |\phi_n\rangle$，其中 $E_0 \le E_1 \le E_2 \le \dots$ 是系统的本征能量谱。

$$
|\psi\rangle = \sum_{n=0}^{\infty} c_n |\phi_n\rangle
$$

其中 $c_n = \langle \phi_n | \psi \rangle$ 是展开系数。由于 $|\phi_n\rangle$ 构成了正交归一基，我们有 $\sum_n |c_n|^2 = 1$。现在，我们计算[能量期望值](@entry_id:174035)：

$$
\langle H \rangle = \langle \psi | H | \psi \rangle = \left( \sum_m c_m^* \langle \phi_m | \right) H \left( \sum_n c_n |\phi_n\rangle \right) = \sum_{m,n} c_m^* c_n \langle \phi_m | H | \phi_n \rangle
$$

利用本征方程 $H|\phi_n\rangle = E_n |\phi_n\rangle$ 和[本征函数](@entry_id:154705)间的正交性 $\langle \phi_m | \phi_n \rangle = \delta_{mn}$，上式简化为：

$$
\langle H \rangle = \sum_{n=0}^{\infty} |c_n|^2 E_n
$$

由于 $E_n \ge E_0$ 对所有 $n$ 成立，我们可以得到：

$$
\langle H \rangle = \sum_n |c_n|^2 E_n \ge \sum_n |c_n|^2 E_0 = E_0 \left( \sum_n |c_n|^2 \right) = E_0
$$

这个不等式直观地告诉我们，真实的[基态](@entry_id:150928)[波函数](@entry_id:147440) $|\phi_0\rangle$ 是唯一能够使[能量期望值](@entry_id:174035)达到其绝对最小值 $E_0$ 的函数。任何我们猜测的、不同于 $|\phi_0\rangle$ 的[试探函数](@entry_id:756165)，都不可避免地混入了能量更高的[激发态](@entry_id:261453) $|\phi_n\rangle$（其中 $n>0$）的成分，从而使其平均能量被抬高。[变分法](@entry_id:163656)的精髓就在于，通过系统地优化我们的“猜测”，来尽可能地逼近这个真实的基态能量。

### [变分法](@entry_id:163656)的实践

[变分原理](@entry_id:198028)本身只是提供了一个[上界](@entry_id:274738)，而“变分方法”则是指一套系统性的程序，用以寻找这个[上界](@entry_id:274738)的最小值，从而获得对[基态能量](@entry_id:263704)的最佳估计。这个过程通常包含三个步骤。

#### 选择试探波函数

这是变分法中最具创造性的一步，其成败直接决定了最终估计的精度。一个好的试探波函数 $\psi(\vec{r}, \alpha, \beta, \dots)$ 应具备以下特征：

1.  **物理合理性**：函数必须遵守系统施加的基本物理约束。例如，它必须在[势能](@entry_id:748988)为无穷大的区域为零，并在无穷远处趋于零以保证可归一化。一个经典的例子是估算宽度为 $2a$ 的一维[无限深方势阱](@entry_id:136391)（$V(x)=0$ for $|x|< a$, $V(x)=\infty$ for $|x|\ge a$）的[基态能量](@entry_id:263704)。一个合适的[试探函数](@entry_id:756165)族可以是 $\psi_b(x) = A(a^2 - x^2)^b$，其中 $b>0$。这个函数形式巧妙地保证了在边界 $x=\pm a$ 处[波函数](@entry_id:147440)为零 [@problem_id:1945828]。

2.  **对称性**：[试探函数](@entry_id:756165)应具备与[哈密顿算符](@entry_id:144286)相同的对称性。如果[势函数](@entry_id:176105) $V(\vec{r})$ 是对称的（例如，偶函数），那么我们知道其[基态](@entry_id:150928)[波函数](@entry_id:147440)也具有相同的对称性（[偶函数](@entry_id:163605)）。选择一个具有正确对称性的[试探函数](@entry_id:756165)可以大大简化计算并提高精度。例如，对于一个由 $V(x) = \lambda (x^2 - a^2)^2$ 描述的对称双阱势，一个明智的[试探函数](@entry_id:756165)是两个[高斯函数](@entry_id:261394)的对称叠加，形式为 $\psi(x) = A(\exp(-\alpha(x-a)^2) + \exp(-\alpha(x+a)^2))$。这个函数形式直观地捕捉了粒子在两个[势阱](@entry_id:151413)底部出现概率最大的物理图像 [@problem_id:1945864]。

3.  **灵活性**：函数应包含一个或多个可调节的**变分参数**（如 $\alpha, \beta, \dots$）。这些参数赋予了[试探函数](@entry_id:756165)族一定的“柔性”，使其能够通过调整自身形状来更好地模拟真实的[基态](@entry_id:150928)[波函数](@entry_id:147440)，从而在[能量泛函](@entry_id:170311)的空间中探索更低的值。

#### 计算[能量期望值](@entry_id:174035)

选定[试探函数](@entry_id:756165) $\psi(\vec{r}, \alpha, \dots)$ 后，下一步是计算[能量期望值](@entry_id:174035) $E(\alpha, \dots)$。

$$
E(\alpha, \dots) = \frac{\int \psi^* H \psi \, d\tau}{\int \psi^* \psi \, d\tau}
$$

通常，我们会分别计算分子（[哈密顿量](@entry_id:172864)[期望值](@entry_id:153208)）和分母（归一化积分），因为[试探函数](@entry_id:756165)中的[归一化常数](@entry_id:752675)会在相除时消去。[哈密顿算符](@entry_id:144286) $H = T+V$ 由[动能算符](@entry_id:265633) $T = -\frac{\hbar^2}{2m}\nabla^2$ 和[势能](@entry_id:748988)算符 $V$ 组成。

势能[期望值](@entry_id:153208) $\langle V \rangle$ 的计算通常是直接的，即 $\int V(\vec{r}) |\psi|^2 d\tau$。

动能[期望值](@entry_id:153208) $\langle T \rangle$ 的计算可以通过两种方式进行。第一种是直接将[拉普拉斯算符](@entry_id:146319) $\nabla^2$ 作用于 $\psi$。第二种通常更为便捷，即通过分部积分（或[格林第一恒等式](@entry_id:170345)）将其转化为：

$$
\langle T \rangle = -\frac{\hbar^2}{2m} \int \psi^* (\nabla^2 \psi) \, d\tau = \frac{\hbar^2}{2m} \int |\nabla \psi|^2 \, d\tau
$$

这一转化要求[波函数](@entry_id:147440)在积分边界上为零，这对于束缚态问题总是成立的。但需要注意，如果[试探函数](@entry_id:756165)的[一阶导数](@entry_id:749425)在某些点不连续（例如有尖点），或者[高阶导数](@entry_id:140882)发散，则需要谨慎处理。例如，在问题[@problem_id:1945828]中，为了使分部积分有效且动能[期望值](@entry_id:153208)有限，需要变分参数 $b > 1/2$。

我们以一个在一维“V”形[势阱](@entry_id:151413) $V(x) = \lambda|x|$ 中运动的粒子为例，完整演示这一过程。我们选择一个在原点有尖点的指数形式[试探函数](@entry_id:756165) $\psi(x) = C \exp(-\alpha|x|)$，其中 $\alpha$ 是变分参数 [@problem_id:1945860]。

- **动能[期望值](@entry_id:153208)** $\langle T \rangle$:
  $\psi'(x) = -\alpha \cdot \text{sgn}(x) \cdot \psi(x)$，所以 $|\psi'(x)|^2 = \alpha^2 |\psi(x)|^2$ (除了 $x=0$ 点)。
  $$ \langle T \rangle = \frac{\frac{\hbar^2}{2m} \int_{-\infty}^{\infty} \alpha^2 |\psi|^2 dx}{\int_{-\infty}^{\infty} |\psi|^2 dx} = \frac{\hbar^2 \alpha^2}{2m} $$

- **[势能](@entry_id:748988)[期望值](@entry_id:153208)** $\langle V \rangle$:
  $$ \langle V \rangle = \frac{\int_{-\infty}^{\infty} (\lambda|x|) |C \exp(-\alpha|x|)|^2 dx}{\int_{-\infty}^{\infty} |C \exp(-\alpha|x|)|^2 dx} = \frac{2\lambda \int_0^{\infty} x \exp(-2\alpha x) dx}{2 \int_0^{\infty} \exp(-2\alpha x) dx} $$
  利用标准积分 $\int_0^{\infty} x^n \exp(-ax) dx = n!/a^{n+1}$，我们得到：
  $$ \langle V \rangle = \lambda \frac{1/(2\alpha)^2}{1/(2\alpha)} = \frac{\lambda}{2\alpha} $$
  因此，能量函数为：
  $$ E(\alpha) = \langle T \rangle + \langle V \rangle = \frac{\hbar^2 \alpha^2}{2m} + \frac{\lambda}{2\alpha} $$

#### 最小化能量

最后一步是调整变分参数，以找到[能量期望值](@entry_id:174035)的最小值。这通过求解一组[偏微分方程](@entry_id:141332)来实现：

$$
\frac{\partial E}{\partial \alpha} = 0, \quad \frac{\partial E}{\partial \beta} = 0, \quad \dots
$$

解出的参数值 $(\alpha_*, \beta_*, \dots)$ 对应于给定[试探函数](@entry_id:756165)族内的最优选择。将这些最优参数代回能量表达式 $E(\alpha, \dots)$，便可得到[基态能量](@entry_id:263704)的最佳估计值 $E_{min}$。

继续“V”形[势阱](@entry_id:151413)的例子[@problem_id:1945860]，我们对 $E(\alpha)$ 求导并令其为零：

$$
\frac{dE}{d\alpha} = \frac{\hbar^2 \alpha}{m} - \frac{\lambda}{2\alpha^2} = 0 \quad \implies \quad \alpha_*^3 = \frac{m\lambda}{2\hbar^2}
$$

将最优参数 $\alpha_* = (\frac{m\lambda}{2\hbar^2})^{1/3}$ 代回 $E(\alpha)$，得到能量的最小估计值。利用[最小化条件](@entry_id:203120) $\frac{\hbar^2 \alpha_*}{m} = \frac{\lambda}{2\alpha_*^2}$，我们可以写出 $\frac{\hbar^2\alpha_*^2}{2m} = \frac{\lambda}{4\alpha_*}$。因此：

$$
E_{min} = E(\alpha_*) = \frac{\hbar^2\alpha_*^2}{2m} + \frac{\lambda}{2\alpha_*} = \frac{\lambda}{4\alpha_*} + \frac{\lambda}{2\alpha_*} = \frac{3\lambda}{4\alpha_*} = \frac{3\lambda}{4}\left(\frac{2\hbar^2}{m\lambda}\right)^{1/3} = \frac{3}{2^{5/3}}\left(\frac{\lambda^2 \hbar^2}{m}\right)^{1/3}
$$
这个结果给出了基态能量的一个上界。其依赖于 $m, \hbar, \lambda$ 的缩放关系是稳健的。

### 结果的诠释：准确性与局限性

[变分法](@entry_id:163656)得到的结果是一个能量上限，其与真实值之间的差距完全取决于我们最初选择的[试探函数](@entry_id:756165)族的好坏。

#### “猜测越好，结果越优”

一个更接近真实[基态](@entry_id:150928)[波函数](@entry_id:147440)形态的[试探函数](@entry_id:756165)，会得到一个更低（因此更精确）的能量估计。我们可以通过一个例子来清晰地看到这一点：再次考虑一维[无限深方势阱](@entry_id:136391)。其真实的[基态](@entry_id:150928)[波函数](@entry_id:147440)是 $\phi_0(x) = \sqrt{1/a} \cos(\frac{\pi x}{2a})$，其在原点附近是平坦的。

在问题[@problem_id:1945838]中，我们比较了两个[试探函数](@entry_id:756165)：
1.  抛物线型: $\psi_1(x) = a^2 - x^2$
2.  四次型: $\psi_2(x) = (a^2 - x^2)^2$

计算得到的能量估计分别为 $E_1 = \frac{5\hbar^2}{4ma^2}$ 和 $E_2 = \frac{3\hbar^2}{2ma^2}$。真实的[基态能量](@entry_id:263704)是 $E_0 = \frac{\pi^2\hbar^2}{8ma^2} \approx \frac{1.2337 \hbar^2}{ma^2}$。而我们的估计值是 $E_1 = \frac{1.25 \hbar^2}{ma^2}$ 和 $E_2 = \frac{1.5 \hbar^2}{ma^2}$。

有趣的是，尽管四次函数在视觉上似乎更“平坦”，但抛物线函数 $E_1$ 却给出了更接近真实能量的估计。这说明“接近”是一个需要通过积分来衡量的全局属性。抛物线函数在整个区间内更好地模拟了余弦函数的形状。更一般地，对于形式为 $\psi_b(x) \propto (a^2 - x^2)^b$ 的[试探函数](@entry_id:756165)族[@problem_id:1945828]，通过最小化能量，可以发现最优参数 $b_{opt} = (2+\sqrt{6})/4 \approx 1.11$。这个最优值非常接近 $b=1$ 的抛物线情况，它给出的能量估计 $E_{min} = \frac{\hbar^2}{8ma^2}(5+2\sqrt{6}) \approx \frac{1.237 \hbar^2}{ma^2}$，比 $E_1$ 和 $E_2$ 都更接近真实值。这完美展示了引入变分参数如何系统地改善我们的估计。

#### 当变分法给出精确解时

变分法有一个美妙的特性：如果所选择的[试探函数](@entry_id:756165)族恰好包含了真实的[基态](@entry_id:150928)[波函数](@entry_id:147440)，那么变分最小化过程必然会找到这个精确解，并给出确切的基态能量 $E_0$。

一个完美的例子是二维[各向异性谐振子](@entry_id:746448)，其[势能](@entry_id:748988)为 $V(x,y) = \frac{1}{2}m(\omega_x^2 x^2 + \omega_y^2 y^2)$ [@problem_id:1945877]。其[基态](@entry_id:150928)[波函数](@entry_id:147440)的精确形式是两个方向上高斯函数的乘积。如果我们选择一个形式完全匹配的[试探函数](@entry_id:756165) $\psi(x,y) = A \exp(-(\alpha x^2 + \beta y^2))$，其中 $\alpha$ 和 $\beta$ 是变分参数，最小化过程将精确地找到 $\alpha_* = \frac{m\omega_x}{2\hbar}$ 和 $\beta_* = \frac{m\omega_y}{2\hbar}$。代入这些最优参数后，我们得到的能量 $E_{min} = \frac{\hbar}{2}(\omega_x + \omega_y)$，这正是该系统精确的[基态能量](@entry_id:263704)。

另一个例子是半谐振子势阱（$V(x)=\infty$ for $x \le 0$，$V(x)=\frac{1}{2}m\omega^2 x^2$ for $x > 0$）[@problem_id:1945854]。该系统的[基态](@entry_id:150928)[波函数](@entry_id:147440)必须在 $x=0$ 处为零，且在 $x>0$ 区域满足薛定谔方程。这恰好与全[谐振子](@entry_id:155622)的第一[激发态](@entry_id:261453)（一个奇函数）在 $x>0$ 的部分相匹配。如果我们选择一个具有正确函数形式的[试探函数](@entry_id:756165)，如 $\psi(x) = A x \exp(-\alpha x^2)$，变分法将同样给出精确的基态能量 $E_0 = \frac{3}{2}\hbar\omega$。

#### 当[试探函数](@entry_id:756165)形式不同时

在大多数实际应用中，我们并不知道真实[波函数](@entry_id:147440)的精确形式。这时，变分法依然能提供一个有价值的能量[上界](@entry_id:274738)。氢[原子基态](@entry_id:194487)就是一个很好的例子 [@problem_id:1945871]。其精确的[基态](@entry_id:150928)[波函数](@entry_id:147440)是指数衰减的，$\phi_0(r) \propto \exp(-r/a_0)$。如果我们选择一个计算上更方便的[高斯函数](@entry_id:261394)作为[试探函数](@entry_id:756165)，$\psi(r) = A \exp(-\beta r^2)$，会发生什么呢？

[高斯函数](@entry_id:261394)在原点附近与[指数函数](@entry_id:161417)相似，但在大 $r$ 处衰减得快得多。这是一个函数形式上的根本差异。通过[变分法](@entry_id:163656)最小化能量，我们得到一个最佳估计 $E_{estimate} = -\frac{m_e e^4}{12\pi^3 \epsilon_0^2 \hbar^2}$。与精确的基态能量 $E_{exact} = -\frac{m_e e^4}{32\pi^2 \epsilon_0^2 \hbar^2}$相比，我们发现：

$$
\frac{E_{estimate}}{E_{exact}} = \frac{32\pi^2}{12\pi^3} = \frac{8}{3\pi} \approx 0.849
$$

由于能量是负的，一个数值上更小（[绝对值](@entry_id:147688)更小）的能量意味着一个更高的能量值（$0.849 E_{exact} > E_{exact}$）。这证实了[变分原理](@entry_id:198028)：我们的估计值确实是真实基态能量的一个[上界](@entry_id:274738)。尽管[试探函数](@entry_id:756165)的函数形式是“错误”的，但我们仍然得到了一个距离真实值不到16%的合理估计。

### 高等应用

[变分法](@entry_id:163656)的威力远不止于估算单粒子系统的能量，它在量子物理的许多前沿领域都扮演着核心角色。

#### 证明束缚态的存在

除了定量计算能量，变分法还可以用来回答定性的问题，例如“一个给定的[势阱](@entry_id:151413)是否足够深以支持一个束缚态？”。束缚态的定义是能量为负的状态（$E<0$）。根据[变分原理](@entry_id:198028)，如果我们能找到**任何**一个归一化的[试探函数](@entry_id:756165) $|\psi\rangle$，使得其[能量期望值](@entry_id:174035) $\langle E \rangle$ 为负，那么我们就可以断定，真实的基态能量 $E_0$ 必定也为负（因为 $E_0 \le \langle E \rangle  0$），因此系统至少存在一个束缚态。

一个经典的问题是在二维空间中，一个吸引性的 $\delta$ 函数势 $V(\vec{\rho}) = -\alpha \delta^{(2)}(\vec{\rho})$ 需要多大的强度 $\alpha$ 才能束缚一个粒子 [@problem_id:1945841]。我们使用一个简单的指数[试探函数](@entry_id:756165) $\psi(\rho) = C \exp(-b\rho)$。计算得到的[能量期望值](@entry_id:174035)为：

$$
E(b) = \frac{\hbar^2 b^2}{2m} - \frac{2\alpha b^2}{\pi} = b^2 \left( \frac{\hbar^2}{2m} - \frac{2\alpha}{\pi} \right)
$$

这个表达式的符号完全由括号内的项决定。要使 $E(b)$ 可能为负，括号内的项必须为负，即：

$$
\frac{\hbar^2}{2m} - \frac{2\alpha}{\pi}  0 \quad \implies \quad \alpha  \frac{\pi\hbar^2}{4m}
$$

这揭示了一个深刻的结果：在二维空间中，一个任意弱的吸引势并不总能形成束缚态，它必须达到一个临界强度 $\alpha_{crit} = \frac{\pi\hbar^2}{4m}$。[变分法](@entry_id:163656)为我们提供了一种优雅的方式来确定这一阈值。

#### 多体系统

[变分法](@entry_id:163656)是处理[多电子原子](@entry_id:157716)、分子和凝聚态物质等复杂[多体系统](@entry_id:144006)的基石。这些系统的[哈密顿量](@entry_id:172864)包含所有粒子间的相互作用，使得精确求解变得不可能。

例如，考虑两个被囚禁在一维[谐振子势](@entry_id:750179)阱中、并通过接触势 $V_{int} = \lambda\delta(x_1-x_2)$ 相互作用的[玻色子](@entry_id:138266) [@problem_id:1945882]。系统的[哈密顿量](@entry_id:172864)为：

$$
H = \sum_{i=1}^{2}\left[-\frac{\hbar^{2}}{2m}\frac{\partial^{2}}{\partial x_{i}^{2}}+\frac{1}{2}m\omega^{2}x_{i}^{2}\right]+\lambda\,\delta(x_{1}-x_{2})
$$

由于粒子是[玻色子](@entry_id:138266)，它们的总[波函数](@entry_id:147440) $\Psi(x_1, x_2)$ 必须在交换粒子[坐标时](@entry_id:263720)保持对称。一个简单的[试探函数](@entry_id:756165)是单个高斯函数的乘积 $\Psi(x_1, x_2) = C \exp(-\alpha(x_1^2 + x_2^2))$，它自然满足对称性要求。

计算[能量期望值](@entry_id:174035)时，除了各粒子独立的动能和谐振子势能外，还需计算[相互作用能](@entry_id:264333)：

$$
\langle V_{int} \rangle = \lambda \int \!\! \int |\Psi(x_1, x_2)|^2 \delta(x_1 - x_2) \,dx_1 dx_2 = \lambda \int |\Psi(x, x)|^2 \,dx
$$

最终，总[能量期望值](@entry_id:174035) $E(\alpha)$ 成为动能、势能和[相互作用能](@entry_id:264333)三项之和，每一项都依赖于变分参数 $\alpha$。通过最小化这个总能量，我们可以估算相互作用如何改变系统的基态能量。这种方法可以推广到更复杂的系统，构成了[Hartree-Fock理论](@entry_id:160358)和[密度泛函理论](@entry_id:139027)等现代计算化学和物理方法的基础。

总之，变分法不仅是估算基态能量的实用工具，更是一种深刻的物理思维方式。它将寻找[基态](@entry_id:150928)的问题转化为一个[泛函最小化](@entry_id:184561)问题，使我们能够利用强大的数学分析工具来探索那些无法精确求解的、丰富多彩的量子世界。