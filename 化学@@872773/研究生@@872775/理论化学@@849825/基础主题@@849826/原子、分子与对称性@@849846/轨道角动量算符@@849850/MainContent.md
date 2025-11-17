## 引言
轨道角动量是量子力学中描述微观粒[子空间](@entry_id:150286)运动状态的核心概念，对于理解原子和分子的结构、[光谱](@entry_id:185632)以及[化学反应性](@entry_id:141717)至关重要。从经典力学的行星轨道到量子世界中电子的概率云，角动量的概念发生了深刻的转变，但其核心——[旋转对称](@entry_id:137077)性——得以保留并被赋予了更丰富的内涵。本文旨在系统性地解决一个根本问题：[轨道角动量](@entry_id:191303)在量子力学中是如何被精确描述的，以及这一数学框架如何引出可被实验验证的物理现象？

为了回答这一问题，我们将分三步深入探索。在“原理与机制”一章中，我们将从轨道角动量作为空间[旋转生成元](@entry_id:154292)的根本作用出发，建立其严谨的数学[代数结构](@entry_id:137052)，并揭示[角动量量子化](@entry_id:155651)的内在必然性。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章，我们将把这些抽象的理论应用于具体的物理化学体系，展示它如何解释原子光谱的[简并模式](@entry_id:196301)、分子的[对称性分类](@entry_id:184862)以及[过渡金属配合物的磁性](@entry_id:155300)等关键现象。最后，通过“动手实践”部分，读者将有机会通过解决具体问题来检验和巩固所学知识，将理论真正内化为解决实际问题的能力。

## 原理与机制

本章旨在深入探讨[轨道角动量](@entry_id:191303)算符的数学框架和物理内涵。我们将从其作为空间[旋转生成元](@entry_id:154292)的根本作用出发，推导出其[代数结构](@entry_id:137052)，并由此揭示[角动量量子化](@entry_id:155651)的内在机制。随后，我们会将这一抽象的代数理论与物理实在联系起来，阐明它如何决定了[中心力](@entry_id:267832)场问题（如[类氢原子](@entry_id:164890)）中[波函数](@entry_id:147440)的形态和能级的[简并模式](@entry_id:196301)。最后，我们将讨论角动量理论中的一些高等主题，包括其在多电子体系中的应用，与自旋的区分，以及与之相关的数学物理难题。

### 角动量作为旋转的生成元

在经典力学中，一个绕原点运动的粒子的轨道角动量被定义为其位置矢量 $\mathbf{r}$ 和动量矢量 $\mathbf{p}$ 的叉乘：$\mathbf{L} = \mathbf{r} \times \mathbf{p}$。在量子力学中，我们通过[正则量子化](@entry_id:148501)程序将这个概念引入量子领域，即将经典的[可观测量](@entry_id:267133)替换为相应的[厄米算符](@entry_id:153410)。因此，轨道角动量算符被形式上定义为：
$$ \hat{\mathbf{L}} = \hat{\mathbf{r}} \times \hat{\mathbf{p}} $$
其中 $\hat{\mathbf{r}}$ 和 $\hat{\mathbf{p}}$ 分别是位置算符和动量算符。在位置表象中，$\hat{\mathbf{r}}$ 是乘法算符 $\mathbf{r}$，而[正则动量](@entry_id:155151)算符是[微分](@entry_id:158718)算符 $\hat{\mathbf{p}} = -i\hbar\nabla$。将此代入，我们得到[轨道角动量](@entry_id:191303)算符的具体微分形式：
$$ \hat{\mathbf{L}} = -i\hbar(\mathbf{r} \times \nabla) $$
这个定义不仅仅是一个形式上的推广。它揭示了角动量在量子力学中的一个深刻的物理意义：**[轨道角动量](@entry_id:191303)算符是空间旋转的生成元**。

为了理解这一点，让我们考虑一个标量[波函数](@entry_id:147440) $\psi(\mathbf{r})$ 在一个[无穷小旋转](@entry_id:166635)下的变换行为。当[坐标系](@entry_id:156346)绕单位矢量 $\hat{\mathbf{n}}$ 旋转一个无穷小角度 $\delta\theta$ 时，一个固定的物理点在变换后的[坐标系](@entry_id:156346)中的位置矢量为 $\mathbf{r}' = R^{-1}\mathbf{r}$。然而，描述物理状态的[波函数](@entry_id:147440)在空间同一点的值必须保持不变。这意味着变换后的[波函数](@entry_id:147440) $\psi'$ 在新坐标 $\mathbf{r}$ 的值等于原[波函数](@entry_id:147440)在旧坐标 $R^{-1}\mathbf{r}$ 的值。换句话说，描述[旋转操作](@entry_id:140575)的幺正算符 $U(R)$ 的作用是 $(U(R)\psi)(\mathbf{r}) = \psi(R^{-1}\mathbf{r})$。

对于一个绕 $\hat{\mathbf{n}}$ 轴的[无穷小旋转](@entry_id:166635) $\delta\theta$，逆旋转作用于位置矢量为 $R^{-1}\mathbf{r} \approx \mathbf{r} - \delta\boldsymbol{\theta} \times \mathbf{r}$，其中 $\delta\boldsymbol{\theta} = \delta\theta \hat{\mathbf{n}}$。对[波函数](@entry_id:147440)进行[泰勒展开](@entry_id:145057)，我们得到：
$$ (U(\delta\boldsymbol{\theta})\psi)(\mathbf{r}) = \psi(\mathbf{r} - \delta\boldsymbol{\theta} \times \mathbf{r}) \approx \psi(\mathbf{r}) - (\delta\boldsymbol{\theta} \times \mathbf{r}) \cdot \nabla\psi(\mathbf{r}) $$
利用矢量恒等式 $(\mathbf{a} \times \mathbf{b}) \cdot \mathbf{c} = \mathbf{a} \cdot (\mathbf{b} \times \mathbf{c})$，我们可以重写上式为：
$$ (U(\delta\boldsymbol{\theta})\psi)(\mathbf{r}) \approx \psi(\mathbf{r}) - \delta\boldsymbol{\theta} \cdot (\mathbf{r} \times \nabla)\psi(\mathbf{r}) $$
另一方面，根据[斯通定理](@entry_id:262301) (Stone's theorem)，任何连续的幺正[变换群](@entry_id:203581)都可以由一个自伴算符（即生成元）生成。对于旋转，这个生成元就是[总角动量算符](@entry_id:149439) $\hat{\mathbf{J}}$。对于一个[无穷小旋转](@entry_id:166635)，幺正算符可以写为 $U(\delta\boldsymbol{\theta}) \approx \mathbb{I} - \frac{i}{\hbar}\delta\boldsymbol{\theta} \cdot \hat{\mathbf{J}}$。对于纯[轨道运动](@entry_id:162856)，$\hat{\mathbf{J}} = \hat{\mathbf{L}}$，所以：
$$ (U(\delta\boldsymbol{\theta})\psi)(\mathbf{r}) \approx \left(\mathbb{I} - \frac{i}{\hbar}\delta\boldsymbol{\theta} \cdot \hat{\mathbf{L}}\right)\psi(\mathbf{r}) $$
比较这两个表达式，我们可以清楚地识别出轨道角动量算符 [@problem_id:2792493]：
$$ - \frac{i}{\hbar}\delta\boldsymbol{\theta} \cdot \hat{\mathbf{L}} = - \delta\boldsymbol{\theta} \cdot (\mathbf{r} \times \nabla) \implies \hat{\mathbf{L}} = -i\hbar(\mathbf{r} \times \nabla) $$
这证实了我们的定义，并赋予了 $\hat{\mathbf{L}}$ 作为空间[旋转生成元](@entry_id:154292)的根本地位。

### [角动量算符](@entry_id:153013)的[代数结构](@entry_id:137052)

[角动量算符](@entry_id:153013)的许多核心性质，尤其是其谱的量子化，并非源于其具体的[微分](@entry_id:158718)算符形式，而是源于一个更基本的[代数结构](@entry_id:137052)。这个结构直接由位置和[动量算符](@entry_id:151743)的基本[对易关系](@entry_id:136780)决定。

在量子力学中，位置算符的分量之间以及动量算符的分量之间都是相互对易的，即 $[\hat{r}_i, \hat{r}_j] = 0$ 和 $[\hat{p}_i, \hat{p}_j] = 0$。而位置和动量算符之间的基本[对易关系](@entry_id:136780)为：
$$ [\hat{r}_i, \hat{p}_j] = i\hbar\delta_{ij} $$
其中 $\delta_{ij}$ 是克罗内克（Kronecker）delta。从这些基本关系出发，我们可以推导[轨道角动量](@entry_id:191303)算符各个分量之间的对易关系。[角动量算符](@entry_id:153013)的第 $k$ 个分量可以写为 $L_k = \sum_{ij} \epsilon_{kij} r_i p_j$，其中 $\epsilon_{kij}$ 是列维-奇维塔（Levi-Civita）符号。例如，我们来计算 $[L_x, L_y]$：
$$ [L_x, L_y] = [r_y p_z - r_z p_y, r_z p_x - r_x p_z] $$
利用对易子的性质和基本[对易关系](@entry_id:136780)，经过一番直接但略显繁琐的计算，可以得到一个至关重要的结果：
$$ [L_x, L_y] = i\hbar L_z $$
通过对坐标 $(x, y, z)$ 进行轮换[对称操作](@entry_id:143398)，我们可以得到所有分量之间的对易关系，它们可以紧凑地写成：
$$ [L_i, L_j] = i\hbar \sum_{k} \epsilon_{ijk} L_k $$
这个关系式定义了一个[李代数](@entry_id:137954)，记为 $\mathfrak{so}(3)$，它是三维旋转群 $\mathrm{SO}(3)$ 对应的[李代数](@entry_id:137954)。这个[代数结构](@entry_id:137052)是角动量理论的核心。它表明角动量的不同分量是不能同时精确测量的（除非它们都为零），这体现了不确定性原理。此外，一个重要的物理要求是可观测量的算符必须是[厄米算符](@entry_id:153410)（或更严格地说是自伴算符）。可以证明，基于厄米的位置和动量算符定义的 $\hat{\mathbf{L}} = \hat{\mathbf{r}} \times \hat{\mathbf{p}}$ 的各个分量 $L_i$ 确实是[厄米算符](@entry_id:153410)，即 $L_i^\dagger = L_i$ [@problem_id:2792473]。

接下来，我们引入一个非常重要的算符——总角动量平方算符 $L^2$：
$$ L^2 = L_x^2 + L_y^2 + L_z^2 $$
利用上述代数关系，我们可以证明 $L^2$ 与角动量的任何一个分量都对易 [@problem_id:2792466]：
$$ [L^2, L_i] = 0 \quad (\text{for } i=x, y, z) $$
这个性质意味着 $L^2$ 是一个标量算符，它在旋转操作下保持不变。在群论的语言中，$L^2$ 是 $\mathfrak{so}(3)$ [李代数](@entry_id:137954)的一个卡西米尔算符（Casimir operator）。由于 $L^2$ 与所有 $L_i$ 对易，我们可以找到一组态，它们同时是 $L^2$ 和某一个分量（通常选择 $L_z$）的共同本征态。这为我们标记和分类[量子态](@entry_id:146142)提供了一套强大的量子数体系。

### 角动量[本征态](@entry_id:149904)的谱

现在我们利用上述[代数结构](@entry_id:137052)来确定 $L^2$ 和 $L_z$ 的[本征值](@entry_id:154894)。为此，我们引入**[升降算符](@entry_id:197899)**：
$$ L_+ = L_x + iL_y $$
$$ L_- = L_x - iL_y $$
这些算符不是厄米的（$L_+^\dagger = L_-$），但它们与 $L_z$ 的对易关系非常有用：
$$ [L_z, L+] = \hbar L_+ $$
$$ [L_z, L_-] = -\hbar L_- $$
同时，它们与 $L^2$ 对易：$[L^2, L_{\pm}] = 0$。

假设 $| \psi \rangle$ 是 $L^2$ 和 $L_z$ 的一个共同[本征态](@entry_id:149904)，其[本征值](@entry_id:154894)分别为 $\lambda$ 和 $\mu$。即 $L^2 | \psi \rangle = \lambda | \psi \rangle$ 和 $L_z | \psi \rangle = \mu | \psi \rangle$。现在考察 $L_+ | \psi \rangle$ 这个态。由于 $[L^2, L_+] = 0$，这个新态仍然是 $L^2$ 的本征态，且[本征值](@entry_id:154894)不变。然而，它的 $L_z$ [本征值](@entry_id:154894)发生了改变：
$$ L_z (L_+ | \psi \rangle) = (L_+ L_z + [L_z, L_+]) | \psi \rangle = (L_+ \mu + \hbar L_+) | \psi \rangle = (\mu + \hbar) (L_+ | \psi \rangle) $$
这表明，$L_+$ 算符将一个 $L_z$ [本征值](@entry_id:154894)为 $\mu$ 的态 "提升" 为一个[本征值](@entry_id:154894)为 $\mu + \hbar$ 的态，而 $L^2$ 的[本征值保持](@entry_id:636565)不变。类似地，$L_-$ 会将 $L_z$ 的[本征值](@entry_id:154894) "降低" $\hbar$。

对于一个给定的 $L^2$ [本征值](@entry_id:154894) $\lambda$，由于 $L^2 - L_z^2 = L_x^2 + L_y^2$ 是一个正定算符的平方和，其[期望值](@entry_id:153208)必须非负，这意味着 $\lambda \ge \mu^2$。因此，$L_z$ 的[本征值](@entry_id:154894) $\mu$ 必然有上界和下界。这意味着必定存在一个**最高权重态** $|l, m_{\text{max}}\rangle$，它被 $L_+$ 算符湮灭：$L_+|l, m_{\text{max}}\rangle = 0$。同理，也存在一个**最低权重态** $|l, m_{\text{min}}\rangle$，使得 $L_-|l, m_{\text{min}}\rangle = 0$。

通过将 $L^2$ 表示为 $L^2 = L_-L_+ + L_z^2 + \hbar L_z$ 并作用于[最高权](@entry_id:202808)重态，我们可以确定 $L^2$ 的[本征值](@entry_id:154894)。习惯上，我们用量子数 $l$ 来标记[最高权](@entry_id:202808)重，即 $m_{\text{max}} = l$，并用 $m$ 来标记 $L_z$ 的[本征值](@entry_id:154894)（以 $\hbar$ 为单位）。作用在 $|l,l\rangle$ 上：
$$ L^2|l, l\rangle = (L_-L_+ + L_z^2 + \hbar L_z)|l, l\rangle = (0 + (\hbar l)^2 + \hbar(\hbar l))|l, l\rangle = \hbar^2 l(l+1)|l, l\rangle $$
由于同一系列（由[升降算符](@entry_id:197899)连接的所有态）中的所有态都具有相同的 $L^2$ [本征值](@entry_id:154894)，我们得出结论：$L^2$ 的[本征值](@entry_id:154894)为 $\hbar^2 l(l+1)$。类似地，通过作用于最低权重态并要求[本征值](@entry_id:154894)一致，可以证明 $m_{\text{min}} = -l$。由于[升降算符](@entry_id:197899)每次改变 $m$ 的值都是整数 1，所以从 $-l$ 到 $l$ 的所有 $m$ 值必须以整数步长连接。这导致对于一个给定的 $l$，存在 $2l+1$ 个可能的 $m$ 值：
$$ m = -l, -l+1, \dots, l-1, l $$
这些共同的本征态记为 $|l, m\rangle$，它们满足 [@problem_id:2792466]：
$$ L^2 |l, m\rangle = \hbar^2 l(l+1) |l, m\rangle $$
$$ L_z |l, m\rangle = \hbar m |l, m\rangle $$
到目前为止，这个纯代数的推导允许 $l$ 是非负整数或半整数。

### [轨道角动量](@entry_id:191303)的物理实现

#### [波函数](@entry_id:147440)与整数[量子数](@entry_id:145558)

上述[代数结构](@entry_id:137052)适用于任何满足 $\mathfrak{so}(3)$ [对易关系](@entry_id:136780)的算符，包括自旋。然而，轨道角动量有一个额外的物理约束：它的[本征态](@entry_id:149904)必须是定义在三维物理空间上的**单值[波函数](@entry_id:147440)** $\psi(\mathbf{r})$。这意味着在空间的任何一个点，[波函数](@entry_id:147440)只能有一个确定的值。

这个看似简单的要求具有深刻的后果。考虑一个绕 $z$ 轴旋转 $2\pi$ 的操作。这个操作在物理上是一个[恒等变换](@entry_id:264671)，它将每个点都映射回自身。因此，单值[波函数](@entry_id:147440)在这次旋转后必须回到其原始值，即代表 $2\pi$ 旋转的幺正算符必须是单位算符 $\mathbb{I}$。
$$ U_z(2\pi) = \exp(-i 2\pi L_z / \hbar) = \mathbb{I} $$
将这个算符作用于本征态 $|l, m\rangle$：
$$ \exp(-i 2\pi L_z / \hbar) |l, m\rangle = \exp(-i 2\pi (\hbar m) / \hbar) |l, m\rangle = e^{-i2\pi m} |l, m\rangle $$
为了使结果等于 $|l, m\rangle$，我们必须有 $e^{-i2\pi m} = 1$。这个条件只有当[磁量子数](@entry_id:145584) $m$ 是一个**整数**时才能满足。

既然 $m$ 必须是整数，而对于一个给定的 $l$ 值， $m$ 从 $-l$ 到 $l$ 以整数步长取值，那么 $l$ 本身也必须是**非负整数** ($l = 0, 1, 2, \dots$)。如果 $l$ 是半整数（例如 $l=1/2$），那么 $m$ 的值（$-1/2, 1/2$）将不是整数，从而违反[单值性](@entry_id:174849)要求。这就是为什么[轨道角动量量子数](@entry_id:167573) $l$ 只能取整数值，这与我们稍后将讨论的、可以取半整数的[自旋角动量](@entry_id:149719)形成了鲜明对比 [@problem_id:2792499]。

#### 球坐标中的[角动量算符](@entry_id:153013)

将抽象的[角动量算符](@entry_id:153013)与具体物理问题联系起来的关键一步，是将其在[球坐标](@entry_id:146054) $(r, \theta, \phi)$ 中表示出来。通过繁琐但直接的[坐标变换](@entry_id:172727)，可以得到 $L^2$ 的[微分形式](@entry_id:146747)：
$$ L^2 = -\hbar^2 \left[ \frac{1}{\sin\theta} \frac{\partial}{\partial\theta}\left(\sin\theta \frac{\partial}{\partial\theta}\right) + \frac{1}{\sin^2\theta}\frac{\partial^2}{\partial\phi^2} \right] $$
我们注意到，这恰好是球坐标下[拉普拉斯算符](@entry_id:146319) $\nabla^2$ 的角度部分（乘以 $-\hbar^2$）。拉普拉斯算符可以分解为径向和角度两部分：
$$ \nabla^2 = \frac{1}{r^2}\frac{\partial}{\partial r}\left(r^2\frac{\partial}{\partial r}\right) + \frac{1}{r^2} \nabla^2_{\text{ang}} $$
因此，我们得到了一个至关重要的关系 [@problem_id:2792474]：
$$ L^2 = -\hbar^2 r^2 \left(\nabla^2 - \frac{1}{r^2}\frac{\partial}{\partial r}\left(r^2\frac{\partial}{\partial r}\right)\right) $$
或者更简洁地，作用在仅依赖于角度的函数上时，$L^2 = -\hbar^2 \nabla^2_{\text{ang}}$。

这个关系对于求解[中心力](@entry_id:267832)场问题（即[势能](@entry_id:748988) $V$ 只依赖于径向距离 $r$，$V(\mathbf{r}) = V(r)$）具有决定性意义。这类问题的[哈密顿算符](@entry_id:144286)为：
$$ \hat{H} = -\frac{\hbar^2}{2\mu}\nabla^2 + V(r) = -\frac{\hbar^2}{2\mu} \left( \frac{1}{r^2}\frac{\partial}{\partial r}\left(r^2\frac{\partial}{\partial r}\right) \right) + \frac{L^2}{2\mu r^2} + V(r) $$
由于 $V(r)$ 具有球对称性，[哈密顿算符](@entry_id:144286)与所有[旋转操作](@entry_id:140575)都对易，因此 $[H, L^2] = 0$ 且 $[H, L_z] = 0$。这意味着我们可以寻找 $H, L^2, L_z$ 的共同[本征函数](@entry_id:154705)。由于 $L^2$ 和 $L_z$ 只依赖于角度变量 $(\theta, \phi)$，它们的本征函数只依赖于角度，这正是**球谐函数** $Y_{l}^{m}(\theta, \phi)$。这证明了将总[波函数](@entry_id:147440)分离为径向[部分和](@entry_id:162077)角度部分的合理性：
$$ \psi(r, \theta, \phi) = R_{nl}(r) Y_{l}^{m}(\theta, \phi) $$
代入薛定谔方程后，角度部分 $Y_{l}^{m}$ 被 $L^2$ 算符替换为其[本征值](@entry_id:154894) $\hbar^2 l(l+1)$，从而得到一个只依赖于 $r$ 的**[径向方程](@entry_id:191687)**。值得注意的是，[径向方程](@entry_id:191687)中出现了一个[有效势能](@entry_id:171609)项 $\frac{\hbar^2 l(l+1)}{2\mu r^2}$，这被称为**[离心势垒](@entry_id:147153)**，它具有将粒子推离中心的纯粹的量子力学效应。

#### 数学严谨性：自伴性

在研究生阶段的理论化学中，理解算符的数学严谨性至关重要。一个算符要代表物理可观测量，它必须是自伴的（self-adjoint）。对于像 $L_z = -i\hbar\frac{\partial}{\partial\phi}$ 这样的[微分](@entry_id:158718)算符，自伴性不仅仅是形式上的[厄米共轭](@entry_id:191215)，还依赖于其定义域的恰当选择。

作用于球面上[波函数](@entry_id:147440)的[希尔伯特空间](@entry_id:261193)是 $L^2(S^2, \sin\theta d\theta d\phi)$，其[内积](@entry_id:158127)定义为 $\langle\psi_1|\psi_2\rangle = \int_0^{2\pi}d\phi\int_0^{\pi}d\theta \sin\theta \psi_1^*\psi_2$。为了使 $L_z$ 在这个空间上是自伴的，其定义域 $D(L_z)$ 中的函数除了必须平方可积且其导数也平方可积外，还必须满足一个边界条件。通过分部积分可以证明，这个边界条件正是**[周期性边界条件](@entry_id:147809)**：
$$ \psi(\theta, \phi + 2\pi) = \psi(\theta, \phi) $$
这个数学上保证自伴性所必需的条件，与我们之前基于物理考虑提出的[波函数](@entry_id:147440)[单值性](@entry_id:174849)要求完全一致 [@problem_id:2792458]。这展示了量子力学中物理直觉与数学严谨性之间的深刻和谐。

### 物理体系中的角动量

#### 旋转[对称性与简并](@entry_id:177833)

中心力场中能级的简并性是[旋转对称](@entry_id:137077)性的直接体现。一个系统的[哈密顿量](@entry_id:172864) $H$ 具有[旋转不变性](@entry_id:137644)，意味着它与[旋转群](@entry_id:204412) $\mathrm{SO}(3)$ 的所有生成元 $L_i$ 都对易：$[H, L_i] = 0$。

这一性质直接导致了能级的 $(2l+1)$ 度简并。因为 $[H, L_i]=0$，所以 $H$ 也与[升降算符](@entry_id:197899)对易：$[H, L_{\pm}] = 0$。考虑一个[能量本征态](@entry_id:152154) $|E, l, m\rangle$，即 $H|E, l, m\rangle = E|E, l, m\rangle$。现在考察由 $L_+$ 作用产生的新态：
$$ H(L_+|E, l, m\rangle) = L_+ H |E, l, m\rangle = L_+ (E|E, l, m\rangle) = E(L_+|E, l, m\rangle) $$
这表明新态 $L_+|E, l, m\rangle$（正比于 $|E, l, m+1\rangle$）与原态具有完全相同的能量 $E$。通过反复应用[升降算符](@entry_id:197899)，我们可以连接具有相同 $l$ 值但不同 $m$ 值的所有 $2l+1$ 个状态。由于每一步能量都保持不变，所以这 $2l+1$ 个状态必须是[能量简并](@entry_id:203091)的 [@problem_id:2792484]。

从群论的角度来看，这 $(2l+1)$ 个简并的[本征态](@entry_id:149904)构成了[旋转群](@entry_id:204412) $\mathrm{SO}(3)$ 的一个 $(2l+1)$ 维的**不可约表示**（irrep）。根据[舒尔引理](@entry_id:136779)（Schur's Lemma），任何与一个[不可约表示](@entry_id:263310)的所有算符都对易的算符（如此处的 $H$），在该表示空间上必然是单位矩阵的常数倍。这意味着 $H$ 在这个 $(2l+1)$ 维[子空间](@entry_id:150286)上的作用等同于乘以一个能量常数 $E_{nl}$，因此所有这些态能量相同。能量值可以依赖于 $l$（以及主量子数 $n$），但不能依赖于 $m$ [@problem_id:2792482]。

这种简并性是 $\mathrm{SO}(3)$ 对称性的直接后果，对所有中心力场都成立。然而，在[类氢原子](@entry_id:164890)中，我们观察到额外的“偶然”简并，即具有相同[主量子数](@entry_id:143678) $n$ 但不同 $l$ 的态也是简并的（例如 $2s$ 和 $2p$）。这种更高的简并性源于一个更大的[对称群](@entry_id:146083) $\mathrm{SO}(4)$，它是由角动量和[龙格-楞次矢量](@entry_id:168301)共同生成的。

当对称性被破坏时，简并会解除。例如，施加一个沿 $z$ 轴的外部[磁场](@entry_id:153296) $\mathbf{B} = B\hat{\mathbf{z}}$，会引入一个与 $L_z$ 成正比的哈密顿项（[塞曼效应](@entry_id:154144)）。这破坏了完全的[球对称性](@entry_id:272852)，只保留了绕 $z$ 轴的[旋转对称](@entry_id:137077)性，即对称群从 $\mathrm{SO}(3)$ 降为 $\mathrm{SO}(2)$。$\mathrm{SO}(2)$ 的[不可约表示](@entry_id:263310)是一维的，由量子数 $m$ 标记。因此，原来的 $(2l+1)$ 度简并的能级会分裂成最多 $2l+1$ 个不同的能级，每个能级对应一个特定的 $m$ 值 [@problem_id:2792482]。

#### 多电子体系

在包含多个电子的原子或分子中，[总轨道角动量](@entry_id:265302)算符是各个[电子角动量](@entry_id:198934)算符的矢量和：
$$ \mathbf{L} = \sum_{a=1}^{N} \mathbf{l}_a $$
由于不同电子的算符作用于[希尔伯特空间](@entry_id:261193)的不同部分（张量积结构），它们相互对易：$[\mathbf{l}_{a,i}, \mathbf{l}_{b,j}] = 0$ 当 $a \neq b$ 时。利用这个性质，我们可以证明[总角动量算符](@entry_id:149439)的各个分量仍然满足 $\mathfrak{so}(3)$ 代数 [@problem_id:2792478]：
$$ [L_x, L_y] = \left[\sum_a l_{a,x}, \sum_b l_{b,y}\right] = \sum_{a,b} [l_{a,x}, l_{b,y}] = \sum_a [l_{a,x}, l_{a,y}] = \sum_a i\hbar l_{a,z} = i\hbar L_z $$
这意味着关于单个[电子角动量](@entry_id:198934)的所有代数结论，包括 $L^2$ 的[本征值](@entry_id:154894)形式、$(2L+1)$ 的多重性等，都同样适用于多电子体系的[总轨道角动量](@entry_id:265302) $L$。例如，对于一个孤立原子，其[哈密顿量](@entry_id:172864)具有[旋转不变性](@entry_id:137644)，因此总的 $L$ 和 $M_L$ 是[好量子数](@entry_id:262514)，能级根据[总角动量量子数](@entry_id:164948) $L$ 的值呈现 $(2L+1)$ 度的简并。

#### [轨道角动量](@entry_id:191303)与自旋的区分

我们已经看到，$\mathfrak{so}(3)$ 的[代数结构](@entry_id:137052)允许半整数表示，但轨道角动量由于[波函数](@entry_id:147440)的[单值性](@entry_id:174849)而被限制为整数表示。这自然引出了**[自旋角动量](@entry_id:149719)** $\mathbf{S}$ 的概念，它是一种内禀的角动量，不能用 $\mathbf{r} \times \mathbf{p}$ 的形式描述。

[轨道角动量](@entry_id:191303) $\mathbf{L}$ 和[自旋角动量](@entry_id:149719) $\mathbf{S}$ 在算符层面有根本区别 [@problem_id:2792493]：
1.  **作用空间**：$\mathbf{L}$ 是一个[微分](@entry_id:158718)算符，作用于描述粒子空间[分布](@entry_id:182848)的[轨道](@entry_id:137151)[波函数](@entry_id:147440) $\psi(\mathbf{r})$ 上。$\mathbf{S}$ 则作用于一个有限维的、与空间坐标无关的内禀“自旋空间”上，通常用[矩阵表示](@entry_id:146025)。
2.  **与位置算符的对易性**：由于自旋是内禀属性，[自旋算符](@entry_id:155419)与位置算符对易：$[S_i, r_j] = 0$。而[轨道角动量](@entry_id:191303)作为空间运动的度量，与位置算符不对易：$[L_i, r_j] = i\hbar \epsilon_{ijk} r_k$。
3.  **谱**：$\mathbf{L}$ 的量子数 $l$ 只能是整数。而 $\mathbf{S}$ 的量子数 $s$ 可以是整数或半整数（例如电子的 $s=1/2$）。

对于一个有自旋的粒子，其总的[希尔伯特空间](@entry_id:261193)是[轨道空间](@entry_id:148658)和自旋空间的[张量积](@entry_id:140694) $\mathcal{H} = \mathcal{H}_{\text{orb}} \otimes \mathcal{H}_{\text{spin}}$。真正的空间[旋转生成元](@entry_id:154292)是**[总角动量](@entry_id:155748)** $\mathbf{J} = \mathbf{L} + \mathbf{S}$。

### 高等主题：角算符的不存在性

一个自然而深刻的问题是：是否存在一个与 $L_z$ 正则共轭的方位角算符 $\hat{\Phi}$，类似于位置 $x$ 和动量 $p_x$ 的关系 $[x, p_x] = i\hbar$？如果存在这样一个自伴算符 $\hat{\Phi}$，其谱为整个实数轴 $\mathbb{R}$，那么它将生成一个幺正群 $\exp(is\hat{\Phi})$，该群能够连续地平移 $L_z$ 的谱。

然而，这样的算符是不存在的。这个“禁行定理”可以通过一个优雅的谱论证来证明。如果 $\hat{\Phi}$ 存在，那么它与 $L_z$ 的共轭关系 $\exp(-is\hat{\Phi}) L_z \exp(is\hat{\Phi}) = L_z + \hbar s$ 意味着 $L_z$ 的谱必须在任意实数平移下保持不变。这迫使 $L_z$ 的谱必须是整个实数轴 $\mathbb{R}$。但这与我们已知的 $L_z$ 的[离散谱](@entry_id:150970) $\sigma(L_z) = \hbar\mathbb{Z}$（或在有限维[子空间](@entry_id:150286)中的有限集）形成直接矛盾。

因此，不存在一个良好定义的、与 $L_z$ 正则共轭的自伴角算符。这一结论迫使我们寻找描述角度的替代方案 [@problem_id:2792483]。现代[量子光学](@entry_id:140582)和量子信息理论中采用的方法包括：
1.  使用一对有界的、对易的自伴算符，如 $\widehat{\cos\phi}$ 和 $\widehat{\sin\phi}$。
2.  使用一个幺正的“相位算符” $\hat{U} = e^{i\phi}$。这个算符与 $L_z$ 的关系不是连续平移，而是离散[移位](@entry_id:145848)：$\hat{U}^\dagger L_z \hat{U} = L_z + \hbar$，这与 $L_z$ 的[离散谱](@entry_id:150970)完美兼容。
3.  最普适的框架是[正算符取值测量](@entry_id:138349)（[POVM](@entry_id:138770)），它将角度[可观测量](@entry_id:267133)描述为定义在圆周上的一个[POVM](@entry_id:138770)，而不是与单个自伴算符相关的投影取值测量（PVM）。

理解这一点对于深入研究[量子相位](@entry_id:197087)、角动量-角度[不确定性关系](@entry_id:186128)等前沿课题至关重要。