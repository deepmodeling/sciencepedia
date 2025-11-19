## 引言
在物理学从[艾萨克·牛顿](@entry_id:175889)（Isaac Newton）的矢量力学向基于能量的[分析力学](@entry_id:166738)演进的过程中，[哈密顿原理](@entry_id:175601)（Hamilton's Principle）扮演了基石性的角色。它代表了一次深刻的[范式](@entry_id:161181)转换，不再关注瞬时的力与加速度，而是从一个全局的、积分的视角审视运动：自然界在所有可能的路径中，偏爱那条使“作用量”这一物理量取驻值的路径。这一优雅的陈述不仅简化了复杂系统的分析，更揭示了物理定律背后深层的对称性与统一性。本文旨在系统地阐述[哈密顿原理](@entry_id:175601)，解决从基本概念到高级应用中的知识鸿沟。

在接下来的内容中，我们将分三个部分展开探索。第一部分**“原理与机制”**将深入[哈密顿原理](@entry_id:175601)的核心，阐明作用量、拉格朗日量等基本概念，并推导其强大的计算工具——欧拉-拉格朗日方程。第二部分**“应用与跨学科联系”**将展示该原理的强大威力，探讨其在处理[约束系统](@entry_id:164587)、相对论、电磁学乃至[经典场论](@entry_id:149475)等不同物理分支中的应用。最后，**“动手实践”**部分将提供一系列具体问题，引导读者将理论知识应用于解决实际的力学问题，从而巩固和深化理解。

## 原理与机制

在经典力学的发展历程中，从艾萨克·牛顿（Isaac Newton）基于力和加速度的矢量力学，到约瑟夫·拉格朗日（Joseph-Louis Lagrange）和威廉·哈密顿（William Rowan Hamilton）发展的基于能量和[变分原理](@entry_id:198028)的[分析力学](@entry_id:166738)，标志着一次深刻的[范式](@entry_id:161181)转换。[哈密顿原理](@entry_id:175601)，又称[平稳作用量原理](@entry_id:151723)，是[分析力学](@entry_id:166738)的基石。它将物理定律的表述从瞬时的因果关系（力导致加速度）提升到了一个全局的、积分的视角：在所有可能的运动路径中，自然选择的那条路径将使一个称为“作用量”的物理量取驻值。本章将深入探讨[哈密顿原理](@entry_id:175601)的起源、数学表述及其在物理学多个分支中的广泛应用。

### [作用量原理](@entry_id:154742)与拉格朗日量

[哈密顿原理](@entry_id:175601)的核心是**作用量（Action）**，它是一个泛函，记作 $S$。对于一个由一组[广义坐标](@entry_id:156576) $q = (q_1, q_2, \dots, q_n)$ 描述的力学系统，其在时间间隔 $[t_1, t_2]$ 内的运动路径 $q(t)$ 所对应的作用量定义为**[拉格朗日量](@entry_id:174593)（Lagrangian）** $L$ 的时间积分：

$$
S[q(t)] = \int_{t_1}^{t_2} L(q(t), \dot{q}(t), t) dt
$$

这里的 $\dot{q}(t)$ 表示[广义速度](@entry_id:178456)，即[广义坐标](@entry_id:156576)对时间的导数。拉格朗日量 $L$ 是一个标量函数，它完全描述了系统的动力学特性。

**[哈密顿原理](@entry_id:175601)（Hamilton's Principle）**断言：在所有连接起始构型 $q(t_1)$ 和终止构型 $q(t_2)$ 的可能路径中，系统实际遵循的物理路径是使作用量 $S$ 取**驻值（stationary value）**的那一条。用[变分学](@entry_id:197464)的语言来说，这意味着作用量的一阶变分 $\delta S$ 为零：

$$
\delta S = \delta \int_{t_1}^{t_2} L(q, \dot{q}, t) dt = 0
$$

这个原理将复杂的矢量[微分方程](@entry_id:264184)问题转化为了一个标量函数的[变分问题](@entry_id:756445)，极大地简化了力学分析，尤其是在处理[约束系统](@entry_id:164587)和对称性问题时显示出无与伦比的优势。

### 从[牛顿力学](@entry_id:162125)到[达朗贝尔原理](@entry_id:166612)与[哈密顿原理](@entry_id:175601)

[哈密顿原理](@entry_id:175601)并非凭空出现，它可以从牛顿力学的基础上通过[达朗贝尔原理](@entry_id:166612)（[d'](@entry_id:189153)Alembert's principle）推导出来，从而揭示了[分析力学](@entry_id:166738)与牛顿力学之间的深刻联系。[达朗贝尔原理](@entry_id:166612)将动力学问题转化为静力学问题，它指出，对于任何满足约束的[虚位移](@entry_id:168781) $\delta\mathbf{r}_i$，主动力 $\mathbf{F}_i$ 和[惯性力](@entry_id:169104) $-m_i\ddot{\mathbf{r}}_i$ 所做的总[虚功](@entry_id:176403)为零：

$$
\sum_{i=1}^N (\mathbf{F}_i - m_i\ddot{\mathbf{r}}_i) \cdot \delta\mathbf{r}_i = 0
$$

为了从这个瞬时关系得到一个积分原理，我们将其在时间区间 $[t_1, t_2]$ 上进行积分 [@problem_id:1092769]。我们考虑的路径变分在端点处为零，即 $\delta\mathbf{r}_i(t_1) = \delta\mathbf{r}_i(t_2) = \mathbf{0}$。

积分的第一部分涉及主动力所做的[虚功](@entry_id:176403)。对于保守系统，力可以由一个标量[势能函数](@entry_id:200753) $V$ 的梯度得到，$\mathbf{F}_i = -\nabla_{\mathbf{r}_i} V$。因此，$\sum_i \mathbf{F}_i \cdot \delta\mathbf{r}_i = -\sum_i \nabla_{\mathbf{r}_i} V \cdot \delta\mathbf{r}_i = -\delta V$。

积分的第二部分涉及惯性力。我们使用分部积分法来处理这一项：
$$
\int_{t_1}^{t_2} \sum_i (-m_i\ddot{\mathbf{r}}_i) \cdot \delta\mathbf{r}_i dt = \sum_i \left[ -m_i\dot{\mathbf{r}}_i \cdot \delta\mathbf{r}_i \right]_{t_1}^{t_2} + \int_{t_1}^{t_2} \sum_i m_i\dot{\mathbf{r}}_i \cdot \delta\dot{\mathbf{r}}_i dt
$$
由于端点处的变分为零，边界项 $\left[ -m_i\dot{\mathbf{r}}_i \cdot \delta\mathbf{r}_i \right]_{t_1}^{t_2}$ 消失。剩下的积分项可以被识别为系统动能 $T = \sum_i \frac{1}{2}m_i|\dot{\mathbf{r}}_i|^2$ 的变分，因为 $\delta T = \sum_i m_i\dot{\mathbf{r}}_i \cdot \delta\dot{\mathbf{r}}_i$。因此，惯性力[虚功](@entry_id:176403)的[时间积分](@entry_id:267413)等于动能积分的变分：$\int_{t_1}^{t_2} \delta T dt = \delta \int_{t_1}^{t_2} T dt$。

将两部分合并，[达朗贝尔原理](@entry_id:166612)的[时间积分](@entry_id:267413)形式变为：
$$
\int_{t_1}^{t_2} (\delta T - \delta V) dt = \delta \int_{t_1}^{t_2} (T - V) dt = 0
$$
这正是[哈密顿原理](@entry_id:175601)，它同时揭示了对于保守系统，拉格朗日量具有一个非常简洁和重要的形式：$L = T - V$，即动能与[势能](@entry_id:748988)之差。

### 欧拉-拉格朗日方程：动力学的计算引擎

[哈密顿原理](@entry_id:175601) $\delta S = 0$ 是一个优美的物理陈述，但要从中提取出具体的[运动方程](@entry_id:170720)，我们需要运用变分法的工具。考虑作用量 $S$ 的变分：
$$
\delta S = \int_{t_1}^{t_2} \delta L(q, \dot{q}, t) dt = \int_{t_1}^{t_2} \left( \frac{\partial L}{\partial q} \delta q + \frac{\partial L}{\partial \dot{q}} \delta \dot{q} \right) dt
$$
注意到 $\delta \dot{q} = \frac{d}{dt}(\delta q)$，我们可以对第二项进行分部积分：
$$
\int_{t_1}^{t_2} \frac{\partial L}{\partial \dot{q}} \frac{d}{dt}(\delta q) dt = \left[ \frac{\partial L}{\partial \dot{q}} \delta q \right]_{t_1}^{t_2} - \int_{t_1}^{t_2} \frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}}\right) \delta q dt
$$
由于路径在端点是固定的，$\delta q(t_1) = \delta q(t_2) = 0$，所以边界项为零。代入 $\delta S$ 的表达式，我们得到：
$$
\delta S = \int_{t_1}^{t_2} \left( \frac{\partial L}{\partial q} - \frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}}\right) \right) \delta q dt = 0
$$
因为路径变分 $\delta q(t)$ 在 $(t_1, t_2)$ 区间内是任意的，为了使积分恒为零，被积函数中 $\delta q$ 的系数必须处处为零。这就给出了著名的**[欧拉-拉格朗日方程](@entry_id:137827)（Euler-Lagrange Equation）**：

$$
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}_j}\right) - \frac{\partial L}{\partial q_j} = 0, \quad (j=1, \dots, n)
$$

这个[方程组](@entry_id:193238)是[拉格朗日力学](@entry_id:147054)的核心。一旦系统的拉格朗日量 $L$ 被确定，就可以通过求解这组[二阶常微分方程](@entry_id:204212)来确定系统的运动轨迹。

### 拉格朗日量的合理性与唯一性

我们已经看到 $L=T-V$ 的形式可以从[达朗贝尔原理](@entry_id:166612)自然导出。现在我们从两个角度来进一步巩固其合理性。

首先，我们可以证明，对于[保守系统](@entry_id:167760)，$L=T-V$ 的[拉格朗日方程](@entry_id:175419)与[牛顿第二定律](@entry_id:274217)在[广义坐标](@entry_id:156576)下的表述是完全等价的 [@problem_id:1092809]。考虑动能 $T$ 对[广义坐标](@entry_id:156576)和[广义速度](@entry_id:178456)的导数所构成的项：
$$
\mathcal{K}_j = \frac{d}{dt}\left(\frac{\partial T}{\partial \dot{q}_j}\right) - \frac{\partial T}{\partial q_j}
$$
通过链式法则和[坐标变换](@entry_id:172727)关系 $\mathbf{r}_i = \mathbf{r}_i(q_1, \dots, q_n)$，可以证明该表达式等于[广义力](@entry_id:169699) $Q_j$ 的定义：
$$
\mathcal{K}_j = \sum_{i=1}^N m_i \ddot{\mathbf{r}}_i \cdot \frac{\partial \mathbf{r}_i}{\partial q_j} = \sum_{i=1}^N \mathbf{F}_i \cdot \frac{\partial \mathbf{r}_i}{\partial q_j} \equiv Q_j
$$
对于[拉格朗日量](@entry_id:174593) $L=T-V$，欧拉-拉格朗日方程可以写为 $\mathcal{K}_j - \frac{\partial (-V)}{\partial q_j} = 0$，即 $\mathcal{K}_j + \frac{\partial V}{\partial q_j} = 0$。这等价于 $Q_j = -\frac{\partial V}{\partial q_j}$，这恰好是保守力的[广义力](@entry_id:169699)表达式。这表明[拉格朗日方法](@entry_id:142825)完美地重现了[牛顿力学](@entry_id:162125)的结果。

其次，我们还可以反向论证 $L=T-V$ 这种形式的“唯一性” [@problem_id:1092637]。假设存在一个更普遍的[拉格朗日量](@entry_id:174593)形式 $L = \alpha T^a - \gamma V^b$，其中 $T$ 是动能，$V$ 是[势能](@entry_id:748988)，而 $\alpha, \gamma, a, b$ 是待定常数。通过将这个 $L$ 代入欧拉-拉格朗日方程，并要求所得的[运动方程](@entry_id:170720)对于任意势能 $V$ 和任意物理轨迹都必须与牛顿第二定律 $m\ddot{\mathbf{x}} = -\nabla V$ 等价，我们可以确定这些常数。推导过程表明，为了消除不应出现的项（如与 $\dot{T}$ 成比例的项）并匹配各项的系数，必须满足 $a=1$ 和 $b=1$，并且 $\alpha = \gamma$。这意味着任何能够普适地描述保守系统动力学的拉格朗日量，必然具有 $L \propto (T-V)$ 的形式。这深刻地揭示了 $T-V$ 这一组合在经典力学中的基础地位。

### [拉格朗日量](@entry_id:174593)的性质与推广

#### [规范不变性](@entry_id:137857)

拉格朗日量的一个重要特性是其非唯一性。具体来说，如果我们将一个关于坐标和时间的任意函数 $F(q,t)$ 的全时间导数 $\frac{dF}{dt}$ 添加到原有的[拉格朗日量](@entry_id:174593) $L$ 上，得到一个新的拉格朗日量 $L' = L + \frac{dF}{dt}$，那么 $L$ 和 $L'$ 描述的物理系统的运动方程是完全相同的 [@problem_id:1092805]。

我们可以通过直接计算 $\frac{dF}{dt}$ 对欧拉-拉格朗日方程的贡献来证明这一点。令 $\Delta L = \frac{dF}{dt} = \frac{\partial F}{\partial q}\dot{q} + \frac{\partial F}{\partial t}$。其对运动方程的贡献是：
$$
\frac{\partial (\Delta L)}{\partial q} - \frac{d}{dt}\left(\frac{\partial (\Delta L)}{\partial \dot{q}}\right) = \left( \frac{\partial^2 F}{\partial q^2}\dot{q} + \frac{\partial^2 F}{\partial q \partial t} \right) - \frac{d}{dt}\left( \frac{\partial F}{\partial q} \right)
$$
由于 $\frac{d}{dt}\left( \frac{\partial F}{\partial q} \right) = \frac{\partial^2 F}{\partial q^2}\dot{q} + \frac{\partial^2 F}{\partial t \partial q}$，上式两项正好完全抵消，结果为零。因此，作用量 $S'$ 和 $S$ 的变分只相差一个与路径无关的边界项 $F(q_2, t_2) - F(q_1, t_1)$，它们会导出相同的[运动方程](@entry_id:170720)。这种在[拉格朗日量](@entry_id:174593)变换下[运动方程](@entry_id:170720)保持不变的性质被称为**规范不变性（Gauge Invariance）**，它是现代物理中一个极其深刻和普遍的对称性概念的雏形。

#### 高阶导数理论

通常，我们假设[拉格朗日量](@entry_id:174593)只依赖于 $q$ 和 $\dot{q}$。这导致了二阶运动方程，与[牛顿物理学](@entry_id:270449)的经验相符（给定初始位置和速度即可唯一确定未来运动）。但我们也可以探索依赖于更[高阶导数](@entry_id:140882)（如加速度 $\ddot{q}$）的[拉格朗日量](@entry_id:174593)，即 $L(q, \dot{q}, \ddot{q}, t)$ [@problem_id:1092777]。通过类似的变分演算，但这次需要对变分中的 $\delta\ddot{q}$ 项进行两次分部积分，并要求在端点处 $\delta q$ 和 $\delta\dot{q}$ 均为零，我们可以得到推广的[欧拉-拉格朗日方程](@entry_id:137827)，即**奥斯特罗格拉德斯基（Ostrogradsky）方程**：
$$
\frac{\partial L}{\partial q} - \frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}}\right) + \frac{d^2}{dt^2}\left(\frac{\partial L}{\partial \ddot{q}}\right) = 0
$$
这类理论会导致四阶或更高阶的[运动方程](@entry_id:170720)，需要更多的初始条件来确定轨迹。更重要的是，奥斯特罗格拉德斯基定理指出，这类理论（除少数特殊情况外）通常会导致系统能量无下界，从而产生物理上的不稳定性。这为经典物理学乃至现代物理[场论](@entry_id:155241)中，为何基本作用量通常只包含[一阶导数](@entry_id:749425)提供了深刻的理论依据。

### 原理的应用与扩展

[哈密顿原理](@entry_id:175601)的强大之处在于其形式的普适性，使其能够优雅地应用于[牛顿力学](@entry_id:162125)难以处理或形式繁琐的领域。

#### [非保守系统](@entry_id:166237)：[广义力](@entry_id:169699)

当系统中存在[非保守力](@entry_id:163431)（如[摩擦力](@entry_id:171772)、空气阻力）时，这些力不能由一个[势能函数](@entry_id:200753)导出。此时，我们不能简单地使用 $L=T-V$。解决方法是，将力分为保守[部分和](@entry_id:162077)非保守部分。保守力仍包含在拉格朗日量中，而[非保守力](@entry_id:163431)的效应则通过**[广义力](@entry_id:169699)（Generalized Force）** $Q_j^{\text{nc}}$ 添加到[欧拉-拉格朗日方程](@entry_id:137827)的右边：
$$
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}_j}\right) - \frac{\partial L}{\partial q_j} = Q_j^{\text{nc}}
$$
其中 $L$ 只包含[保守力](@entry_id:170586)和动能，而 $Q_j^{\text{nc}} = \sum_i \mathbf{F}_i^{\text{nc}} \cdot \frac{\partial \mathbf{r}_i}{\partial q_j}$。

例如，考虑一个在空气中摆动的单摆，受到与速度成正比的阻力 $\mathbf{F}_d = -b\mathbf{v}$ [@problem_id:2195451]。设摆角为 $\theta$，摆长为 $L$。拉格朗日量为 $L = T - V = \frac{1}{2}mL^2\dot{\theta}^2 - mgL(1-\cos\theta)$。阻力对应的[广义力](@entry_id:169699)为 $Q_{\theta}^{\text{nc}} = \mathbf{F}_d \cdot \frac{d\mathbf{r}}{d\theta} = (-bL\dot{\theta}\mathbf{e}_{\theta}) \cdot (L\mathbf{e}_{\theta}) = -bL^2\dot{\theta}$。代入方程得到：
$$
\frac{d}{dt}(mL^2\dot{\theta}) - (-mgL\sin\theta) = -bL^2\dot{\theta}
$$
整理后得到[阻尼摆](@entry_id:163713)的运动方程：$\ddot{\theta} + \frac{b}{m}\dot{\theta} + \frac{g}{L}\sin\theta = 0$。这清晰地展示了如何将耗散效应纳入[拉格朗日框架](@entry_id:751113)。

#### [相对论力学](@entry_id:263483)

[哈密顿原理](@entry_id:175601)的应用范围远超[牛顿力学](@entry_id:162125)。在狭义相对论中，一个[静止质量](@entry_id:264101)为 $m_0$ 的[自由粒子](@entry_id:148748)的作用量是 $\int -m_0 c^2 d\tau$，其中 $d\tau = dt\sqrt{1-v^2/c^2}$ 是固有时。因此，对于在[势能](@entry_id:748988) $V(x)$ 中运动的一维相对论性粒子，其[拉格朗日量](@entry_id:174593)为 [@problem_id:2195461]：
$$
L = -m_0 c^2 \sqrt{1 - \frac{\dot{x}^2}{c^2}} - V(x)
$$
应用[欧拉-拉格朗日方程](@entry_id:137827)，我们首先计算对 $\dot{x}$ 的[偏导数](@entry_id:146280)：
$$
\frac{\partial L}{\partial \dot{x}} = \frac{m_0 \dot{x}}{\sqrt{1 - \dot{x}^2/c^2}} \equiv p
$$
这个量正是[相对论动量](@entry_id:159500) $p$。对 $x$ 的偏导数则为 $\frac{\partial L}{\partial x} = -\frac{dV}{dx}$。因此，运动方程为：
$$
\frac{dp}{dt} - \left(-\frac{dV}{dx}\right) = 0 \quad \Rightarrow \quad \frac{dp}{dt} = -\frac{dV}{dx}
$$
这正是相对论版的牛顿第二定律，表明[作用量原理](@entry_id:154742)能够无缝地过渡到相对论框架，只需采用正确的拉格朗日量形式。

#### 从粒子到场：[经典场论](@entry_id:149475)

[哈密顿原理](@entry_id:175601)最深刻的推广之一是将其应用于场论，即自由度为无穷大的[连续系统](@entry_id:178397)。此时，我们引入**拉格朗日密度（Lagrangian Density）** $\mathcal{L}$，它不仅是场变量 $\phi(\mathbf{x}, t)$ 及其时间导数的函数，还是其空间导数的函数。作用量则是在时空区域上的积分：
$$
S = \int \mathcal{L}(\phi, \partial_t \phi, \nabla \phi) d^3x dt
$$
应用[变分原理](@entry_id:198028)，可得到[场的欧拉-拉格朗日方程](@entry_id:173994)。一个经典的例子是描述一根被拉紧的、均匀柔性弦的横向[振动](@entry_id:267781) [@problem_id:2195483]。设弦的[线密度](@entry_id:158735)为 $\rho$，张力为 $T$，横向位移为 $y(x,t)$。该系统的拉格朗日密度为动能密度与势能密度之差：
$$
\mathcal{L} = \frac{1}{2}\rho \left(\frac{\partial y}{\partial t}\right)^2 - \frac{1}{2}T \left(\frac{\partial y}{\partial x}\right)^2
$$
其中第一项是动能密度，第二项是弦因拉伸而产生的[弹性势能](@entry_id:168893)密度。应用于[场的欧拉-拉格朗日方程](@entry_id:173994)：
$$
\frac{\partial}{\partial t}\left(\frac{\partial\mathcal{L}}{\partial(\partial_t y)}\right) + \frac{\partial}{\partial x}\left(\frac{\partial\mathcal{L}}{\partial(\partial_x y)}\right) - \frac{\partial\mathcal{L}}{\partial y} = 0
$$
计算各[偏导数](@entry_id:146280)并代入，我们得到：
$$
\frac{\partial}{\partial t}(\rho \frac{\partial y}{\partial t}) + \frac{\partial}{\partial x}(-T \frac{\partial y}{\partial x}) - 0 = 0 \quad \Rightarrow \quad \rho \frac{\partial^2 y}{\partial t^2} - T \frac{\partial^2 y}{\partial x^2} = 0
$$
整理后即为标准的[一维波动方程](@entry_id:164824) $\frac{\partial^2 y}{\partial t^2} = \frac{T}{\rho} \frac{\partial^2 y}{\partial x^2}$，其中[波速](@entry_id:186208)的平方为 $v^2 = T/\rho$。这个例子完美展示了[作用量原理](@entry_id:154742)如何从一个简单的能量表达式中生成支配波动现象的[偏微分方程](@entry_id:141332)，为[电磁场](@entry_id:265881)理论和[量子场论](@entry_id:138177)奠定了基础。

### 作用量作为[生成函数](@entry_id:146702)：[哈密顿-雅可比理论](@entry_id:165642)一瞥

到目前为止，我们视作用量为一个待求驻值的数学工具。然而，当把作用量 $S$ 沿着真实的物理路径计算出来时，它本身就成了一个具有深刻物理意义的函数，称为**[哈密顿主函数](@entry_id:169605)（Hamilton's Principal Function）**。它被看作是系统演化始末状态（坐标和时间）的函数，即 $S(q_2, t_2; q_1, t_1)$。

这个函数蕴含了系统的全部动力学信息。例如，对于一个[能量守恒](@entry_id:140514)的系统，系统的总能量 $E$ 可以通过[哈密顿主函数](@entry_id:169605)对末端时间的偏导数得到：
$$
E = -\frac{\partial S}{\partial t_2}
$$
考虑一个一维[谐振子](@entry_id:155622)，其拉格朗日量为 $L = \frac{m}{2}\dot{q}^2 - \frac{m\omega^2}{2}q^2$ [@problem_id:2056207]。通过求解[运动方程](@entry_id:170720)并沿着连接 $(q_1, t_1)$ 和 $(q_2, t_2)$ 的经典路径对拉格朗日量进行积分，可以得到[哈密顿主函数](@entry_id:169605)的显式表达式。这个计算虽然繁琐，但其结果 $S$ 是一个仅依赖于端点坐标 $q_1, q_2$ 和时间间隔 $T=t_2-t_1$ 的函数。对这个函数求关于 $T$ 的偏导数并取负号，就能精确地恢复出系统的总能量 $E$，其表达式完全由端点信息决定。

这个例子揭示了[作用量原理](@entry_id:154742)的更深层次结构：作用量不仅是一个用于导出运动方程的工具，它还是一个“生成函数”，其偏导数能够生成系统的其他重要物理量（如能量、动量）。这一思想是通往更高级的[哈密顿-雅可比理论](@entry_id:165642)的门户，并且在量子力学的[路径积分表述](@entry_id:145051)中扮演着核心角色，其中[量子跃迁](@entry_id:145857)的概率幅与连接始末态的所有可能路径的作用量 $\exp(iS/\hbar)$ 的总和相关。