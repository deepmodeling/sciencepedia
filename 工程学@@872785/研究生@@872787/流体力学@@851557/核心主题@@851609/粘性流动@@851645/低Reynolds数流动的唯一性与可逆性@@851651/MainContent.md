## 引言
在微观世界中，从细菌的游动到微流控芯片中的液滴输运，流体的行为由粘性力主导，而[惯性力](@entry_id:169104)则微不足道。这一领域被称为[低雷诺数流](@entry_id:267536)动，其物理直觉与我们宏观经验大相径庭。描述这类流动的[斯托克斯方程](@entry_id:196346)具有线性和时间无关的特性，这赋予了流体运动两个看似简单却极为深刻的属性：[解的唯一性](@entry_id:143619)和[时间可逆性](@entry_id:274492)。然而，这些属性的严格条件是什么？它们又如何解释了微生物为何采用螺旋鞭毛而非简单摆动鳍片来游泳？本文旨在系统性地解答这些问题。

本文将分为三个核心部分，带领读者深入理解[低雷诺数流](@entry_id:267536)动的独特世界。在“原则与机制”一章中，我们将首先通过能量耗散论证等方法，严格证明[斯托克斯流](@entry_id:138636)[解的唯一性](@entry_id:143619)，并探讨[时间可逆性](@entry_id:274492)如何导出著名的[洛伦兹互易定理](@entry_id:187647)和[扇贝定理](@entry_id:189448)。同时，我们也将分析在何种条件下这些基本原则会被打破。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些理论如何在生物物理、软物质和微工程等领域得到应用，特别是如何利用它们来理解和设计微观游泳策略。最后，“动手实践”部分将提供一系列问题，以巩固和加深对这些核心概念的理解。现在，让我们从探究[斯托克斯流](@entry_id:138636)的基本原则与机制开始。

## 原则与机制

在[低雷诺数流](@entry_id:267536)动的领域，[斯托克斯方程](@entry_id:196346)的线性和时间无关性赋予了流体运动两个至关重要的基本属性：[解的唯一性](@entry_id:143619)（uniqueness）和运动的[时间可逆性](@entry_id:274492)（time-reversibility）。这些属性不仅是理论分析的基石，也深刻地影响了我们对微观世界中运动和输运现象的理解。本章旨在深入阐释这些核心原则，并通过一系列思想实验和具体案例，探讨其成立的条件以及被打破的各种物理机制。

### [斯托克斯流](@entry_id:138636)的唯一性

[斯托克斯流](@entry_id:138636)的[唯一性定理](@entry_id:166861)指出，在给定适当的边界条件下，描述不可压缩[牛顿流体](@entry_id:263796)在低雷诺数下[稳态](@entry_id:182458)运动的[斯托克斯方程](@entry_id:196346)，其解是唯一的。这一性质是[斯托克斯流](@entry_id:138636)理论强大预测能力的保证。其证明通常依赖于一个优雅的[能量耗散](@entry_id:147406)论证。

#### [能量耗散](@entry_id:147406)与唯一性证明

我们首先考虑一个被流体占据的有界、固定的区域 $V$，其边界为 $\partial V$。流体的运动由[稳态](@entry_id:182458)[斯托克斯方程](@entry_id:196346)描述：
$$ \nabla \cdot \boldsymbol{\sigma} = \nabla p - \mu \nabla^2 \mathbf{u} = \mathbf{0} $$
$$ \nabla \cdot \mathbf{u} = 0 $$
其中 $\mathbf{u}$ 是速度场，$p$ 是压[力场](@entry_id:147325)，$\mu$ 是流体的[动力粘度](@entry_id:268228)。[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 定义为 $\boldsymbol{\sigma} = -p\mathbf{I} + 2\mu\mathbf{E}$，其中 $\mathbf{E} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T)$ 是应变率张量。

为了证明[解的唯一性](@entry_id:143619)，我们采用反证法。假设对于同一组边界条件，存在两个不同的解 $(\mathbf{u}_1, p_1)$ 和 $(\mathbf{u}_2, p_2)$。由于[斯托克斯方程](@entry_id:196346)是线性的，它们的差值场 $(\mathbf{u}_d, p_d) = (\mathbf{u}_1 - \mathbf{u}_2, p_1 - p_2)$ 也必须满足[斯托克斯方程](@entry_id:196346)：
$$ \nabla p_d - \mu \nabla^2 \mathbf{u}_d = \mathbf{0} $$
$$ \nabla \cdot \mathbf{u}_d = 0 $$
同时，差值流在边界上也满足对应的齐次（零）边界条件。

接下来，我们考察这个假设的“差值流”所对应的总粘性耗散率 $\Phi_d$。单位体积的[粘性耗散](@entry_id:143708)率为 $\phi = 2\mu(\mathbf{E}:\mathbf{E})$。对于差值流，总[耗散率](@entry_id:748577)为：
$$ \Phi_d = \int_V 2\mu (\mathbf{E}_d : \mathbf{E}_d) \, dV $$
其中 $\mathbf{E}_d$ 是与 $\mathbf{u}_d$ 相关联的应变率张量。利用矢量恒等式和散度定理，我们可以证明这个耗散率与在边界上由差值流的应力所做的功相等：
$$ \Phi_d = \int_V \nabla\mathbf{u}_d : (2\mu\mathbf{E}_d) \, dV = \int_V \nabla\mathbf{u}_d : (\boldsymbol{\sigma}_d + p_d\mathbf{I}) \, dV = \int_{\partial V} \mathbf{u}_d \cdot (\boldsymbol{\sigma}_d \cdot \mathbf{n}) \, dS $$
这里 $\mathbf{n}$ 是指向区域 $V$ 外部的[单位法向量](@entry_id:178851)。

证明的关键在于论证边界积分项为零。考虑常见的[混合边界条件](@entry_id:176456)：在部分边界 $\partial V_u$ 上给定速度 $\mathbf{u} = \mathbf{g}(\mathbf{x})$，在剩余边界 $\partial V_t$ 上给定牵[引力](@entry_id:175476) $\mathbf{t} = \boldsymbol{\sigma} \cdot \mathbf{n} = \mathbf{h}(\mathbf{x})$。由于两个解 $(\mathbf{u}_1, p_1)$ 和 $(\mathbf{u}_2, p_2)$ 满足相同的边界条件，差值流 $\mathbf{u}_d$ 在 $\partial V_u$ 上为零，而差值牵[引力](@entry_id:175476) $\boldsymbol{\sigma}_d \cdot \mathbf{n}$ 在 $\partial V_t$ 上为零。因此，无论何种情况，被积函数 $\mathbf{u}_d \cdot (\boldsymbol{\sigma}_d \cdot \mathbf{n})$ 在整个边界 $\partial V$ 上处处为零。

这直接导致了 $\int_{\partial V} \mathbf{u}_d \cdot (\boldsymbol{\sigma}_d \cdot \mathbf{n}) \, dS = 0$。因此，差值流的总耗散率 $\Phi_d$ 必须为零 [@problem_id:673634]。由于被积函数 $2\mu(\mathbf{E}_d : \mathbf{E}_d)$ 是非负的，总耗散率为零的唯一可能性是应变率张量 $\mathbf{E}_d$ 在整个流体域内处处为零。对于[不可压缩流体](@entry_id:181066)，这意味着速度场 $\mathbf{u}_d$ 只能是[刚体运动](@entry_id:193355)（[平动](@entry_id:187700)加转动）。然而，由于在边界 $\partial V_u$（其面积不为零）上 $\mathbf{u}_d = \mathbf{0}$，这种[刚体运动](@entry_id:193355)必然是零运动。因此，$\mathbf{u}_d = \mathbf{0}$，即 $\mathbf{u}_1 = \mathbf{u}_2$。压[力场](@entry_id:147325) $p_d$ 此时最多为一个常数，但在[流体力学](@entry_id:136788)中，压力通常是相对于某个参考点定义的，因此我们也可以认为 $p_1 = p_2$。这就证明了[斯托克斯流](@entry_id:138636)[解的唯一性](@entry_id:143619)。

#### 推广至复杂边界条件与耦合物理场

这个基于[能量耗散](@entry_id:147406)的论证方法异常强大，可以推广到更复杂的情形。例如，考虑在边界上存在滑移的情况，如纳维-滑移（Navier-slip）条件。在一个特定的案例中 [@problem_id:673636]，边界条件被设定为无穿透（$\mathbf{u} \cdot \mathbf{n} = 0$），而切向牵[引力](@entry_id:175476) $\mathbf{t}_t$ 与切向速度 $\mathbf{u}_t$ 通过一个包含表面[拉普拉斯算子](@entry_id:146319) $\nabla_S^2$ 的复杂关系式 $\mathbf{t}_t = -\alpha \mathbf{u}_t + \epsilon \nabla_S^2 \mathbf{u}_t$ 相联系。

在这种情况下，我们可以构造一个广义的总耗散泛函 $\mathcal{D}$，它不仅包含体内的[粘性耗散](@entry_id:143708)，还包括边界上的[能量耗散](@entry_id:147406)项：
$$ \mathcal{D}[\mathbf{w}] = 2\mu \int_V (\mathbf{E}_w : \mathbf{E}_w) \, dV + \int_{\partial V} \alpha |\mathbf{w}|^2 \, dS + \epsilon \int_{\partial V} |\nabla_S \mathbf{w}|^2 \, dS $$
通过与之前类似的推导，可以证明对于差值流 $\mathbf{w}$，这个广义耗散泛函 $\mathcal{D}[\mathbf{w}]$ 的值必须为零。由于泛函中的每一项（体内耗散、滑移摩擦耗散、[表面梯度](@entry_id:261146)耗散）都是非负的，这迫使差值流 $\mathbf{w}$ 必须为零，从而再次证明了[解的唯一性](@entry_id:143619) [@problem_id:673636]。

该思想还可以进一步推广到多物理场耦合的问题。例如，在模拟[电渗流](@entry_id:167540)的系统中，流体运动与[电势](@entry_id:267554)场 $\psi$ 相互耦合 [@problem_id:673650]。此时，控制[方程组](@entry_id:193238)变为：
$$ -\nabla p + \mu \nabla^2 \mathbf{u} + \alpha_0 \psi \mathbf{k} = \mathbf{0} $$
$$ D \nabla^2 \psi - \gamma_0 (\mathbf{u} \cdot \mathbf{k}) = 0 $$
其中 $\alpha_0, D, \gamma_0$ 是[耦合系数](@entry_id:273384)。即使在这种更复杂的线性耦合系统中，我们依然可以构造一个总的“能量”泛函 $\mathcal{G}$，它结合了粘性耗散和[电势](@entry_id:267554)场的“耗散”：
$$ \mathcal{G} = \int_{\mathcal{V}} \left( 2\mu (\mathbf{S}_d : \mathbf{S}_d) + \frac{\alpha_0 D}{\gamma_0} |\nabla \psi_d|^2 \right) dV $$
通过对差值场 $(\mathbf{u}_d, p_d, \psi_d)$ 的方程进行巧妙的代数运算和积分，可以证明 $\mathcal{G}=0$。由于所有系数均为正，这再次意味着 $\mathbf{u}_d = \mathbf{0}$ 和 $\nabla \psi_d = \mathbf{0}$（结合边界条件可得 $\psi_d=0$），从而保证了耦合系统[解的唯一性](@entry_id:143619) [@problem_id:673650]。

#### [非稳态流](@entry_id:269993)的唯一性

对于非[稳态](@entry_id:182458)（时间依赖）的[斯托克斯流](@entry_id:138636)，唯一性同样成立，前提是初始条件、边界条件和体力项完全相同。非[稳态](@entry_id:182458)[斯托克斯方程](@entry_id:196346)为：
$$ \rho \frac{\partial \mathbf{u}}{\partial t} = -\nabla p + \mu \nabla^2 \mathbf{u} + \mathbf{f} $$
证明思路与[稳态](@entry_id:182458)情况类似，但考察的是差值流 $\mathbf{w} = \mathbf{u}_1 - \mathbf{u}_2$ 的动能 $E(t) = \frac{1}{2}\rho \int_V |\mathbf{w}|^2 dV$ 的时间演化。对动能求时间导数，并利用差值流满足的控制方程，可以得到：
$$ \frac{dE}{dt} = -\Phi_d + \int_V \mathbf{w} \cdot (\mathbf{f}_1 - \mathbf{f}_2) dV $$
其中 $\Phi_d$ 是差值流的[粘性耗散](@entry_id:143708)率。在一个标准的唯一性证明中，我们假设两个解对应完全相同的问题，即 $\mathbf{f}_1 = \mathbf{f}_2$，因此体力项的积分为零。同时，两个解的初始速度和边界速度相同，这意味着初始动能 $E(0)=0$，并且差值流的边界速度为零（导致 $\Phi_d$ 的边界积分为零）。于是我们得到：
$$ \frac{dE}{dt} = -\Phi_d \le 0 $$
由于初始动能为零，且其变化率永不为正，动能 $E(t)$ 必须在所有时刻保持为零。这证明了 $\mathbf{w}=\mathbf{0}$，即解是唯一的。

一个有趣的旁例是，如果两个解对应不同的体力项，例如 $\Delta\mathbf{f} = \mathbf{f}_1 - \mathbf{f}_2 \neq \mathbf{0}$，那么唯一性就不再保证。在这种情况下，[体力](@entry_id:174230)项的积分 $\int_V \mathbf{w} \cdot \Delta\mathbf{f} dV$ 充当了能量源。即使系统从静止开始（$E(0)=0$），这个源项也可以向差值流中注入能量，抵抗[粘性耗散](@entry_id:143708)，使得差值流的动能增长并最终达到一个非零的[稳态](@entry_id:182458)值。这突显了唯一性定理成立的严格条件：不仅[初始和边界条件](@entry_id:750648)要相同，作用在流体上的[体力](@entry_id:174230)也必须完全一致 [@problem_id:673642]。

### [时间可逆性](@entry_id:274492)及其推论

[斯托克斯流](@entry_id:138636)的第二个标志性特征是[时间可逆性](@entry_id:274492)。这一特性源于控制方程中惯性项的缺失，导致方程在[时间反演](@entry_id:182076)变换下保持不变。

#### [斯托克斯方程](@entry_id:196346)的[时间反演不变性](@entry_id:152159)

完整的纳维-斯托克斯方程包含时间导数项 $\rho \frac{\partial \mathbf{u}}{\partial t}$ 和[对流](@entry_id:141806)项 $\rho \mathbf{u} \cdot \nabla \mathbf{u}$。这两项在时间反演（$t \to -t$）下会改变符号，破坏了方程的对称性。然而，在[稳态](@entry_id:182458)[斯托克斯流](@entry_id:138636)的极限下，这些项被忽略，剩下的方程 $\nabla p = \mu \nabla^2 \mathbf{u}$ 不再显式包含时间。这意味着，如果一个边界运动 $\mathbf{U}(t)$ 产生了流场 $\mathbf{u}(\mathbf{x},t)$ 和压[力场](@entry_id:147325) $p(\mathbf{x},t)$，那么反向的边界运动 $-\mathbf{U}(-t)$ 将会产生反向的流场 $-\mathbf{u}(\mathbf{x},-t)$ 和不变的压[力场](@entry_id:147325) $p(\mathbf{x},-t)$。流体的运动轨迹就像一部可以完美倒带的电影，这是宏观世界中因惯性而不可想象的。

#### [洛伦兹互易定理](@entry_id:187647)

[时间可逆性](@entry_id:274492)的一个深刻数学体现是[洛伦兹互易定理](@entry_id:187647)（Lorentz Reciprocal Theorem）。该定理为同一流体域内的任意两个[斯托克斯流](@entry_id:138636)场 $(\mathbf{u}^{(1)}, \boldsymbol{\sigma}^{(1)})$ 和 $(\mathbf{u}^{(2)}, \boldsymbol{\sigma}^{(2)})$ 建立了一个优美的关系：
$$ \int_S \mathbf{u}^{(1)} \cdot (\boldsymbol{\sigma}^{(2)} \cdot \mathbf{n}) \, dS = \int_S \mathbf{u}^{(2)} \cdot (\boldsymbol{\sigma}^{(1)} \cdot \mathbf{n}) \, dS $$
这个定理本质上是斯托克斯算子自伴性质的积分形式。它在[低雷诺数流](@entry_id:267536)[体力](@entry_id:174230)学中有广泛应用，特别是在[边界积分方法](@entry_id:746943)和悬浮粒子动力学中。

一个重要的推论是关于描述刚性粒子运动的宏观[输运系数](@entry_id:136790)的对称性。一个在流体中运动的任意形状的刚性粒子，其受到的[流体动力](@entry_id:750449) $\mathbf{F}$ 和力矩 $\mathbf{T}$ 与其自身的平动速度 $\mathbf{U}$ 和[角速度](@entry_id:192539) $\boldsymbol{\Omega}$ 之间存在线性关系，可以由一个 $6 \times 6$ 的“宏伟阻力矩阵” $\mathcal{R}$ 描述：
$$ \begin{pmatrix} \mathbf{F} \\ \mathbf{T} \end{pmatrix} = \mathcal{R} \begin{pmatrix} \mathbf{U} \\ \boldsymbol{\Omega} \end{pmatrix} = \begin{pmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{C} & \mathbf{D} \end{pmatrix} \begin{pmatrix} \mathbf{U} \\ \boldsymbol{\Omega} \end{pmatrix} $$
其中 $\mathbf{A}, \mathbf{B}, \mathbf{C}, \mathbf{D}$ 是 $3 \times 3$ 的张量。通过巧妙地应用[洛伦兹互易定理](@entry_id:187647)，可以证明这个矩阵是对称的，即 $\mathbf{A} = \mathbf{A}^T$, $\mathbf{D} = \mathbf{D}^T$, 以及最重要的[交叉](@entry_id:147634)项关系 $\mathbf{B} = \mathbf{C}^T$。

例如，我们可以考虑两个思想实验 [@problem_id:673682]：
1.  粒子以纯[平动](@entry_id:187700)速度 $\mathbf{U}_1$ 运动（$\boldsymbol{\Omega}_1 = \mathbf{0}$），受到力 $\mathbf{F}_1$ 和力矩 $\mathbf{T}_1$。
2.  同一粒子以纯转动速度 $\boldsymbol{\Omega}_2$ 运动（$\mathbf{U}_2 = \mathbf{0}$），受到力 $\mathbf{F}_2$ 和力矩 $\mathbf{T}_2$。

将这两个流场代入[洛伦兹互易定理](@entry_id:187647)，经过推导可以得到一个简洁的关系：
$$ \mathbf{U}_1 \cdot \mathbf{F}_2 = \mathbf{T}_1 \cdot \boldsymbol{\Omega}_2 $$
这个结果揭示了[平动](@entry_id:187700)和转动之间的深刻耦合：由转动引起的力与由平动引起的力矩之间存在直接的对称关系。这正是 $\mathbf{C}^T = \mathbf{B}$ 的一种表现形式。

#### [扇贝定理](@entry_id:189448)：往复运动无法产生净位移

[时间可逆性](@entry_id:274492)最著名的推论或许是 E. M. Purcell 提出的“[扇贝定理](@entry_id:189448)”（Scallop Theorem）。该定理断言：在[斯托克斯流](@entry_id:138636)中，一个通过周期性、时间可逆的形变来运动的物体，在一个运动周期结束后，其净位移为零。

一个运动被称为“往复的”（reciprocal）或时间可逆的，如果其形变序列在后半周期是前半周期的精确时间倒序。例如，一个扇贝通过打开和关闭贝壳来运动，如果它打开和关闭的动作完全一样，只是顺序相反，那么这个运动就是往复的。

数学上，如果一个游泳者的形状由一组[广义坐标](@entry_id:156576) $\mathbf{q}(t)$ 描述，一个周期为 $T$ 的往复运动满足 $\mathbf{q}(t) = \mathbf{q}(T-t)$。由于[斯托克斯方程](@entry_id:196346)的线性，游泳者的瞬时速度 $\mathbf{U}(t)$ 与其形变速率 $\dot{\mathbf{q}}(t)$ 呈线性关系，即 $\mathbf{U}(t) = \mathbf{M}(\mathbf{q}(t)) \cdot \dot{\mathbf{q}}(t)$。

一个周期内的总位移 $\Delta\mathbf{r}$ 是速度对时间的积分：
$$ \Delta\mathbf{r} = \int_0^T \mathbf{U}(t) \, dt = \int_0^T \mathbf{M}(\mathbf{q}(t)) \cdot \dot{\mathbf{q}}(t) \, dt $$
我们可以将积分分为两部分：
$$ \Delta\mathbf{r} = \int_0^{T/2} \mathbf{M}(\mathbf{q}(t)) \cdot \dot{\mathbf{q}}(t) \, dt + \int_{T/2}^T \mathbf{M}(\mathbf{q}(t)) \cdot \dot{\mathbf{q}}(t) \, dt $$
对于第二部分积分，我们进行换元 $s = T-t$。由于 $\mathbf{q}(t) = \mathbf{q}(T-t) = \mathbf{q}(s)$，我们有 $\dot{\mathbf{q}}(t) = \frac{d}{dt}\mathbf{q}(T-t) = -\dot{\mathbf{q}}(s)$。代入后发现：
$$ \int_{T/2}^T \mathbf{M}(\mathbf{q}(t)) \cdot \dot{\mathbf{q}}(t) \, dt = \int_{T/2}^0 \mathbf{M}(\mathbf{q}(s)) \cdot (-\dot{\mathbf{q}}(s)) \, (-ds) = - \int_0^{T/2} \mathbf{M}(\mathbf{q}(s)) \cdot \dot{\mathbf{q}}(s) \, ds $$
这恰好与第一部分积分相互抵消。因此，总位移 $\Delta\mathbf{r} = \mathbf{0}$ [@problem_id:673710]。

[扇贝定理](@entry_id:189448)的启示是革命性的：在没有惯性的世界里游泳，必须打破时间对称性。游泳者必须执行非往复的运动，即其“划水”和“收回”的动作序列必须是不同的。这就是为什么细菌使用螺旋状的[鞭毛](@entry_id:145161)（旋转运动是非往复的），而草履虫使用纤毛进行波动（[行波](@entry_id:185008)运动也是非往复的）来在水中前进。

### 唯一性的破坏机制

尽管[斯托克斯流](@entry_id:138636)的唯一性在广泛条件下成立，但在某些特定情况下，这一基本原则会被打破。理解这些非唯一性出现的机制，对于认识真实物理系统的复杂性以及斯托克斯模型本身的局限性至关重要。

#### 几何奇异性与非唯一解

当流体域包含尖角（几何[奇异点](@entry_id:199525)）时，[斯托克斯方程](@entry_id:196346)的解可能不再唯一。在这种情况下，除了由[非齐次边界条件](@entry_id:750645)产生的“特解”之外，方程本身还可能存在满足[齐次边界条件](@entry_id:750371)的非[平凡解](@entry_id:155162)，即所谓的“本征函数”（eigenfunctions）。

一个经典的例子是在二维楔形区域中的流动。通过[分离变量法](@entry_id:168509)，可以寻找形如 $\psi(r, \theta) = r^{\lambda+1} f(\theta)$ 的流函数解，其中 $\psi$ 满足双谐和方程 $\nabla^4 \psi = 0$。这会导出一个关于 $f(\theta)$ 的常微分方程，其解依赖于[特征值](@entry_id:154894) $\lambda$。对于特定的楔角和边界条件组合，可能存在具有正实部的[特征值](@entry_id:154894) $\lambda$。

例如，在一个直角楔形区域（$0 \le \theta \le \pi/2$）中，如果一边是无滑移壁面（$\theta=0$），另一边是无剪切应力的自由表面（$\theta=\pi/2$），则存在一系列离散的[特征值](@entry_id:154894)，其中最小的正值为 $\lambda=2$ [@problem_id:673696]。这个[特征值](@entry_id:154894)对应的本征流场在角点附近有有限的[能量耗散](@entry_id:147406)，并且满足所有[齐次边界条件](@entry_id:750371)。这意味着，任何一个满足[非齐次边界条件](@entry_id:750645)的特定解，都可以叠加上任意倍数的这个本征解，而整个系统仍然是[斯托克斯方程](@entry_id:196346)的一个有效解。因此，解不再是唯一的。这种现象通常与角点附近出现的一系列涡旋（Moffatt eddies）有关。

#### 本构[非线性](@entry_id:637147)：宾汉流体

当流体的本构关系（[应力与应变率](@entry_id:263123)的关系）为[非线性](@entry_id:637147)时，即使在零[雷诺数](@entry_id:136372)下，[解的唯一性](@entry_id:143619)也可能被破坏。宾汉（Bingham）流体就是一个典型的例子。这种材料在所受[剪切应力](@entry_id:137139)低于某个屈服应力 $\tau_y$ 时表现为刚性固体，只有当应力超过 $\tau_y$ 时才开始像[粘性流](@entry_id:136330)体一样流动。

考虑一个由弹簧连接的密度不同的双球系统，垂直悬浮在宾汉流体中 [@problem_id:673694]。上球受到向上的[浮力](@entry_id:144145)，下球受到向下的重力。在[牛顿流体](@entry_id:263796)中，系统会达到一个唯一的[平衡位置](@entry_id:272392)，此时弹簧力精确地平衡了每个球所受的净重力。然而，在宾汉流体中，情况大为不同。

为了使球在流体中移动，作用在球上的[净力](@entry_id:163825)（重力、[浮力](@entry_id:144145)与弹簧力的[合力](@entry_id:163825)）必须大到足以克服流体的屈服阻力 $F_y$。如果净力小于 $F_y$，流体在球周围表现为固体，将球“锁定”在原位。对于这个双球系统，这意味着只要弹簧力 $T$ 满足条件 $|W - T| \le F_y$（其中 $W$ 是每个球的净重力大小），系统就可以保持静止。这对应着一个连续范围的可能弹簧长度 $L$，而不是一个唯一值。这个允许的长度范围 $\Delta L$ 正比于屈服力 $F_y$，即 $\Delta L = 2F_y/k$，其中 $k$ 是[弹簧常数](@entry_id:167197)。这清晰地展示了由材料本构[非线性](@entry_id:637147)导致的静态平衡构型的非唯一性。

#### 惯性与边界耦合的[非线性](@entry_id:637147)

即使是非常微弱的惯性效应，在与其它[非线性](@entry_id:637147)因素（如可变形边界）耦合时，也可能导致解的非唯一性。一个典型的例子是发生在两块柔性[平行板](@entry_id:269827)之间的亥辽-肖（Hele-Shaw）流 [@problem_id:673670]。

在这种流动中，板间距 $b$ 会因[流体压力](@entry_id:142203) $p$ 而改变，例如 $b(p) = b_0 - \alpha p$。描述该系统的简化一维动量方程包含一个小的惯性项 $\rho u \frac{du}{dx}$。将流率 $Q=uWb$ 和压力依赖的间距 $b(p)$ 代入[动量方程](@entry_id:197225)并积分，最终会得到一个联系总流量 $Q$ 和[总压](@entry_id:265293)降 $\Delta P$ 的[非线性](@entry_id:637147)代数方程。这个方程通常是关于 $Q$ 的二次或更高次方程。

对于特定的参数范围，这个方程可能对同一个[压降](@entry_id:267492) $\Delta P$ 产生多个实数解 $Q$。这意味着，对于给定的驱动压力，系统中可能存在多个不同的稳定流速。这种现象被称为[多稳态](@entry_id:180390)（multistability），是系统出现滞回（hysteresis）行为的根源。从数学上看，这种非唯一性的出现源于惯性项（$Q^2$ 项）和边界柔性（通过 $b(p)$ 引入的[非线性](@entry_id:637147)）的共同作用，它们打破了纯粹[粘性流](@entry_id:136330)动所具有的线性关系。当一个表征系统特性的无量纲参数 $\mathcal{K}$（它综合了粘性、惯性、几何和柔性效应）超过某个临界值时，例如 $\mathcal{K}_{max}=1$，[稳态解](@entry_id:200351)便不复存在，预示着流动的失稳 [@problem_id:673670]。

#### 维度与边界问题：斯托克斯悖论

最后，一个著名且具有启发性的“非唯一性”案例是二维无界域中的斯托克斯悖论（Stokes' Paradox）。这个悖论指出，在二维空间中，无法找到一个同时满足在圆柱表面无滑移（$\mathbf{u}=\mathbf{0}$）和在无穷远处为均匀来流（$\mathbf{u} \to U\hat{\mathbf{x}}$）的[斯托克斯流](@entry_id:138636)解。

尝试求解这个问题时，得到的[流函数](@entry_id:266505)通解中必然包含一个对数增长项，形如 $r \ln(r)$ [@problem_id:673684]。这个项导致速度场在 $r \to \infty$ 时也随 $\ln(r)$ 发散，这与无穷远处为[均匀流](@entry_id:272775)的物理边界条件相矛盾。

斯托克斯悖论的根源在于[二维流](@entry_id:266853)动中惯性项在[远场](@entry_id:269288)的相对重要性。在三维中，扰动速度随距离衰减得足够快（如 $1/r$），使得在远场惯性项 $\mathbf{u} \cdot \nabla \mathbf{u}$（衰减如 $1/r^3$）比粘性项 $\nabla^2 \mathbf{u}$（衰减如 $1/r^3$）更快地变得无足轻重。但在二维中，扰动速度衰减较慢（如常数或 $\ln r$），导致在[远场](@entry_id:269288)惯性项（衰减如 $1/r$）相对于粘性项（衰减如 $1/r^2$）变得越来越重要。因此，即使在整体雷诺数很低的情况下，忽略惯性项的[斯托克斯假设](@entry_id:195909)在二维无界域的[远场](@entry_id:269288)中也是不成立的。这个“悖论”实际上揭示了[斯托克斯流](@entry_id:138636)模型在特定维度和边界条件下的[适用范围](@entry_id:636189)限制，而非数学上的内在矛盾。