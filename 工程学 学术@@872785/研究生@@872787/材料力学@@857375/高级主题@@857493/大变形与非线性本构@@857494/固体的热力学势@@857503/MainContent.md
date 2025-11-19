## 引言
在现代[材料科学](@entry_id:152226)与工程中，准确预测材料在复杂的机械载荷和热环境下的行为至关重要。为了超越纯粹的经验性描述，我们需要一个能将宏观力学响应与微观物理过程联系起来的严谨理论框架。[热力学势](@entry_id:140516)正是这一框架的基石，它提供了一种从基本物理定律出发，系统地构建材料本构模型并分析其稳定性的强大工具。然而，如何将抽象的[热力学](@entry_id:141121)概念应用于承受复杂应力状态的固体，并用以解决实际工程问题，是许多研究生和研究人员面临的知识鸿沟。

本文旨在系统性地填补这一鸿沟。我们将通过三个循序渐进的章节，全面介绍[固体热力学](@entry_id:159633)势的理论与应用。首先，在“原理与机制”一章中，我们将从连续介质[热力学](@entry_id:141121)的基础出发，定义内能、亥姆霍兹自由能和吉布斯型[势函数](@entry_id:176105)，并阐明如何通过它们推导[本构关系](@entry_id:186508)和稳定性条件。接着，在“应用与交叉学科联系”一章中，我们将展示这一理论框架的强大威力，探讨其在[热弹性](@entry_id:158447)、固态[相变](@entry_id:147324)、[化学-力学耦合](@entry_id:187897)乃至多物理场问题中的具体应用。最后，通过“动手实践”部分提供的计算练习，您将有机会亲手应用这些概念，将理论知识转化为解决实际问题的能力。通过学习本文，您将能够掌握使用[热力学势](@entry_id:140516)分析和建模高级材料行为的核心技能。

## 原理与机制

本章旨在系统性地阐述可变形固体的[热力学势](@entry_id:140516)函数框架。我们将从连续介质[热力学](@entry_id:141121)的第一和第二定律出发，建立描述材料本构行为的热力学势函数，并探讨这些[势函数](@entry_id:176105)在[平衡与稳定性](@entry_id:175068)分析中的核心作用。

### 连续介质[热力学](@entry_id:141121)基础

为了描述固体的[热力学](@entry_id:141121)行为，我们必须将[热力学](@entry_id:141121)基本定律应用于连续介质。考虑一个在参考构形中占据区域 $\Omega_0$ 的物体，其物质点的[能量守恒](@entry_id:140514)（[热力学第一定律](@entry_id:146485)）和[熵增原理](@entry_id:142282)（热力学第二定律）的局域形式是整个理论框架的基石。

**[能量守恒](@entry_id:140514)（第一定律）**

在参考构形中，单位参考体积的内能密度 $u$ 的变化率等于[应力功率](@entry_id:182907)与热量流入率之和。对于一个物质点，其局域[能量平衡方程](@entry_id:191484)可以写作 [@problem_id:2925015]：
$$
\rho_0 \dot{u}_{\text{specific}} = \mathbf{P}:\dot{\mathbf{F}} - \text{Div}\,\mathbf{Q}_0 + r_0
$$
其中，$\rho_0$ 是参考构形下的质量密度，$u_{\text{specific}}$ 是单位质量的内能（比内能），上方的点表示[物质时间导数](@entry_id:190892)。$\mathbf{P}$ 是第一皮奥拉-基尔霍夫（First Piola-Kirchhoff, PK1）应力张量，它与变形梯度率 $\dot{\mathbf{F}}$ 的缩并 $\mathbf{P}:\dot{\mathbf{F}}$ 代表了单位参考体积的**[应力功率](@entry_id:182907)**，即机械功对内能的贡献率。$\mathbf{Q}_0$ 是参考热流矢量，其散度 $\text{Div}\,\mathbf{Q}_0$ 代表了由于[热传导](@entry_id:147831)导致的能量流出率（因此带有负号）。$r_0$ 则是单位参考体积的内部热源率。为简化符号，后续我们将用 $u$ 表示单位参考体积的内能密度，即 $u = \rho_0 u_{\text{specific}}$。

**[熵产生](@entry_id:141771)（第二定律）**

[热力学第二定律](@entry_id:142732)，即**克劳修斯-杜亥姆不等式 (Clausius-Duhem inequality)**，为不可逆过程提供了基本约束。它指出，一个孤立系统的总熵永不减少。其局域形式断言，熵的产生率必须是非负的。结合[能量守恒](@entry_id:140514)，我们可以推导出适用于材料[本构关系](@entry_id:186508)研究的[耗散不等式](@entry_id:188634) [@problem_id:2924983]：
$$
\mathcal{D} = \mathbf{P}:\dot{\mathbf{F}} - \dot{u} + \theta\dot{\eta} - \frac{1}{\theta} \mathbf{Q}_0 \cdot \text{Grad}\,\theta \ge 0
$$
这里，$\theta$ 是绝对温度，$\eta$ 是单位参考体积的熵密度，$\text{Grad}\,\theta$ 是温度在参考构形下的梯度。左侧的量 $\mathcal{D}$ 被定义为单位参考体积的**耗散密度**，它代表了在[热力学过程](@entry_id:141636)中不可逆地转化为热的能量率。

对于**[可逆过程](@entry_id:276625)**（如理想弹性变形），我们假设没有能量耗散，即 $\mathcal{D} = 0$。此外，在许多理论推导中，我们首先会忽略热传导效应（即令 $\mathbf{Q}_0 = \mathbf{0}$）。在这些条件下，上述不等式简化为一个等式，它将机械功与[热力学状态](@entry_id:755916)量的变化直接联系起来：
$$
\dot{u} = \mathbf{P}:\dot{\mathbf{F}} + \theta\dot{\eta}
$$
这个关系是建立弹性固体本构模型的出发点。

### [状态函数](@entry_id:137683)与自然变量：内能

在[热力学](@entry_id:141121)中，系统的状态由一组状态变量完全确定。描述系统能量的函数，如内能，被称为**[状态函数](@entry_id:137683)**。一个[状态函数](@entry_id:137683)的“自然变量”是指当函数以这些变量表达时，其微分形式最为简洁，并且其偏导数对应于重要的物理量。

对于一个纯[热弹性](@entry_id:158447)固体，其[热力学状态](@entry_id:755916)完全由其变形和热状态决定。因此，我们可以假设内能密度 $u$ 是某个[应变度量](@entry_id:755495)和熵密度的函数。根据可逆过程的[能量平衡](@entry_id:150831)关系 $\dot{u} = \theta\dot{\eta} + \dot{w}$（其中 $\dot{w}$ 是[应力功率](@entry_id:182907)），我们可以确定 $u$ 的自然变量 [@problem_id:2924999]。

[应力功率](@entry_id:182907) $\dot{w}$ 的具体形式取决于所选的[应力与应变率](@entry_id:263123)的共轭对。
*   在小应变理论中，[应力功率](@entry_id:182907)为 $\dot{w} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}$，其中 $\boldsymbol{\sigma}$ 是柯西（Cauchy）[应力张量](@entry_id:148973)，$\boldsymbol{\varepsilon}$ 是[无穷小应变张量](@entry_id:167211)。
*   在[有限应变理论](@entry_id:176941)中，一个常用的共轭对[应力功率](@entry_id:182907)为 $\dot{w} = \mathbf{S}:\dot{\mathbf{E}}$，其中 $\mathbf{S}$ 是第二皮奥拉-基尔霍夫（Second Piola-Kirchhoff, PK2）[应力张量](@entry_id:148973)，$\mathbf{E} = \frac{1}{2}(\mathbf{F}^{\mathsf{T}}\mathbf{F} - \mathbf{I})$ 是格林-拉格朗日（Green-Lagrange）应变张量。

此外，**物质[标架无关性原理](@entry_id:200995)（principle of material frame-indifference）**要求本构函数（如能量函数）在[刚体运动](@entry_id:193355)下保持不变。这意味着能量函数不能直接依赖于非客观的变形梯度 $\mathbf{F}$，而必须通过客观的张量（如[右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$ 或应变张量 $\mathbf{E}$）来描述变形。

结合这些考虑，我们可以将内能密度表示为 $u = u(\mathbf{E}, \eta)$。其[全微分](@entry_id:171747)为：
$$
\mathrm{d}u = \frac{\partial u}{\partial \mathbf{E}}:\mathrm{d}\mathbf{E} + \frac{\partial u}{\partial \eta}\mathrm{d}\eta
$$
与[热力学基本关系](@entry_id:144320) $\mathrm{d}u = \mathbf{S}:\mathrm{d}\mathbf{E} + \theta\mathrm{d}\eta$（[微分形式](@entry_id:146747)）进行比较，我们立即得到：
$$
\mathbf{S} = \frac{\partial u}{\partial \mathbf{E}} \quad \text{and} \quad \theta = \frac{\partial u}{\partial \eta}
$$
这表明，对于内能密度 $u$ 而言，其**自然变量**是应变 $\mathbf{E}$ 和熵 $\eta$。

### 亥姆霍兹自由能：[等温过程](@entry_id:143096)的势函数

尽管内能 $u(\mathbf{E}, \eta)$ 在理论上是完备的，但在实际应用中，温度 $\theta$ 通常比熵 $\eta$ 更容易控制和测量。因此，引入一个新的热力学势，使其自然变量包含温度，将更为方便。通过对内能 $u$ 进行关于熵 $\eta$ 的**勒让德变换（Legendre transformation）**，我们定义了**[亥姆霍兹自由能](@entry_id:136442)（Helmholtz free energy）**密度 $\psi$：
$$
\psi = u - \theta\eta
$$
其[微分形式](@entry_id:146747)为 $\mathrm{d}\psi = \mathrm{d}u - \theta\mathrm{d}\eta - \eta\mathrm{d}\theta$。将 $\mathrm{d}u = \mathbf{S}:\mathrm{d}\mathbf{E} + \theta\mathrm{d}\eta$ 代入，可得 [@problem_id:2925025]：
$$
\mathrm{d}\psi = (\mathbf{S}:\mathrm{d}\mathbf{E} + \theta\mathrm{d}\eta) - \theta\mathrm{d}\eta - \eta\mathrm{d}\theta = \mathbf{S}:\mathrm{d}\mathbf{E} - \eta\mathrm{d}\theta
$$
这个简洁的形式表明，亥姆霍兹自由能 $\psi$ 的自然变量是应变 $\mathbf{E}$ 和温度 $\theta$。从这个表达式出发，我们可以直接推导出[热弹性](@entry_id:158447)材料的**[本构关系](@entry_id:186508)**：
$$
\mathbf{S} = \frac{\partial \psi}{\partial \mathbf{E}} \bigg|_{T} \quad \text{and} \quad \eta = -\frac{\partial \psi}{\partial \theta} \bigg|_{\mathbf{E}}
$$
这一对关系是**[超弹性](@entry_id:159356)（hyperelasticity）**理论的基石。它意味着，只要我们能为一种材料找到其亥姆霍兹自由能函数 $\psi(\mathbf{E}, \theta)$，那么该材料的[应力-应变关系](@entry_id:274093)和热响应（熵）就完全确定了。这极大地简化了本构模型的构建。

**应用示例：可压缩Neo-Hookean模型**

为了展示[亥姆霍兹自由能](@entry_id:136442)的威力，我们考虑一个具体的可压缩Neo-Hookean材料模型。其自由能密度函数形式为 [@problem_id:2924962]：
$$
\psi(\mathbf{C},T)=\frac{\mu}{2}(I_{1}-3)-\mu\ln J+\frac{\kappa}{2}(\ln J)^{2}+f(T)
$$
其中 $I_1 = \operatorname{tr}(\mathbf{C})$ 是[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 的第一[不变量](@entry_id:148850)，$J=\det(\mathbf{F})=\sqrt{\det(\mathbf{C})}$ 是体积比，$\mu$ 和 $\kappa$ 是材料常数。根据本构关系 $\mathbf{S} = 2\frac{\partial\psi}{\partial\mathbf{C}}$（这是使用 $\mathbf{C}$ 作为变量时的形式），我们可以计算出PK2应力 $\mathbf{S}$。然后，通过**推前（push-forward）**操作 $\boldsymbol{\sigma} = \frac{1}{J}\mathbf{F}\mathbf{S}\mathbf{F}^{\mathsf{T}}$，可以得到真实的柯西应力 $\boldsymbol{\sigma}$。经过计算，最终的应力表达式为：
$$
\boldsymbol{\sigma} = \frac{1}{J}\left(\mu\mathbf{B} + \left(\kappa\ln J - \mu\right)\mathbf{I}\right)
$$
这里 $\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}}$ 是[左柯西-格林张量](@entry_id:186163)。这个例子清晰地展示了如何从一个标量的[势函数](@entry_id:176105) $\psi$ 出发，通过严谨的[微分](@entry_id:158718)和运动学变换，得到一个描述材料具体力学响应的张量方程。

### 吉布斯型势函数：处理一般应力状态

在许多工程问题中，我们控制的是施加在物体边界上的力（即应力），而不是位移（应变）。类似于从熵到温度的转换，我们希望有一个自然变量包含应力的[热力学势](@entry_id:140516)。

对于流体或承受静水压的固体，其应力状态为 $\boldsymbol{\sigma} = -p\mathbf{I}$，机械功简化为 $-p\mathrm{d}V$。在这种特殊情况下，我们可以定义经典的**[吉布斯自由能](@entry_id:146774)（Gibbs free energy）** $G = U - TS + pV$。其[微分](@entry_id:158718) $\mathrm{d}G = -S\mathrm{d}T + V\mathrm{d}p$ 表明，它的自然变量是温度 $T$ 和压强 $p$ [@problem_id:2924981]。

然而，对于承受一般[剪切应力](@entry_id:137139)的固体，这种简单的形式不再适用。一般固体的应力功不仅包含体积改变的贡献，还包含形状改变（剪切）的贡献。试图简单地用[平均应力](@entry_id:751819) $p = -\frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})$ 来代替[静水压强](@entry_id:141627)是错误的，因为它忽略了由[偏应力张量](@entry_id:267642)和[偏应变](@entry_id:201263)率所做的功 [@problem_id:2924981]。

正确的做法是再次施行[勒让德变换](@entry_id:146727)，这次是对[亥姆霍兹自由能](@entry_id:136442) $\psi$ 中的力学变量（应变）进行变换。在小应变框架下，我们定义一个**吉布斯型[势函数](@entry_id:176105)**密度 $g$：
$$
g(\boldsymbol{\sigma}, T) = \psi(\boldsymbol{\varepsilon}, T) - \boldsymbol{\sigma}:\boldsymbol{\varepsilon}
$$
其[微分形式](@entry_id:146747)为：
$$
\mathrm{d}g = \mathrm{d}\psi - \boldsymbol{\varepsilon}:\mathrm{d}\boldsymbol{\sigma} - \boldsymbol{\sigma}:\mathrm{d}\boldsymbol{\varepsilon} = (-s\mathrm{d}T + \boldsymbol{\sigma}:\mathrm{d}\boldsymbol{\varepsilon}) - \boldsymbol{\varepsilon}:\mathrm{d}\boldsymbol{\sigma} - \boldsymbol{\sigma}:\mathrm{d}\boldsymbol{\varepsilon} = -s\mathrm{d}T - \boldsymbol{\varepsilon}:\mathrm{d}\boldsymbol{\sigma}
$$
其中 $s$ 是单位体积的熵密度。这个结果表明，$g$ 的自然变量是应力 $\boldsymbol{\sigma}$ 和温度 $T$。从 $g(\boldsymbol{\sigma}, T)$ 出发，我们可以得到应变的本构关系 [@problem_id:2924980]：
$$
\boldsymbol{\varepsilon} = -\frac{\partial g}{\partial \boldsymbol{\sigma}} \bigg|_{T}
$$
因此，亥姆霍兹自由能 $\psi(\boldsymbol{\varepsilon}, T)$ 和吉布斯型势函数 $g(\boldsymbol{\sigma}, T)$ 构成了描述[热弹性](@entry_id:158447)材料的两种等价的框架。它们包含了完全相同的物理信息，选择使用哪一个主要取决于问题的边界条件是[位移控制](@entry_id:748569)还是应力控制，这纯粹是出于便利性的考虑，而非物理本质的区别 [@problem_id:2924980]。

### 变分原理与平衡态

[热力学势](@entry_id:140516)函数不仅用于推导本构关系，它们还在确定系统平衡状态方面扮演着核心角色，这通过**[变分原理](@entry_id:198028)**来体现。

**亥姆霍兹自由能[最小化原理](@entry_id:169952)**

考虑一个与恒温[热库](@entry_id:143608)接触（温度恒为 $T_0$）且边界位移固定的[热弹性](@entry_id:158447)体。根据[热力学第二定律](@entry_id:142732)，在没有外界做功的情况下，任何自发过程都将导致系统的亥姆霍兹自由能 $F = \int \psi \,dV$ 减少，即 $\dot{F} \le 0$。因此，系统达到稳定平衡的状态，必然是其总亥姆霍兹自由能达到**最小值**的状态 [@problem_id:2925002]。这意味着，在所有满足[位移边界条件](@entry_id:203261)的可能构形中，真实的平衡构形将使 $F$ 最小化。

**吉布斯型[自由能最小化](@entry_id:183270)原理**

现在考虑一个不同的场景：系统与恒温[热库](@entry_id:143608)接触，但其边界上施加的是恒定的应力（或牵[引力](@entry_id:175476)）。在这种情况下，我们可以证明，驱动系统演化的势函数是 $\Phi = \psi - \boldsymbol{\sigma}:\boldsymbol{\varepsilon}$（其中 $\boldsymbol{\sigma}$ 是常数）。第二定律要求 $\dot{\Phi} \le 0$ [@problem_id:2924995]。因此，在应力控制下，系统达到稳定平衡的状态是使总吉布斯型势函数 $\mathcal{G} = \int g \,dV = \int (\psi - \boldsymbol{\sigma}:\boldsymbol{\varepsilon}) \,dV$ 达到**最小值**的状态 [@problem_id:2925002, @problem_id:2924995]。

这两个对偶的[最小化原理](@entry_id:169952)深刻地揭示了不同[热力学势](@entry_id:140516)的物理意义：它们是在不同约束条件下，系统为达到平衡而寻求最小化的“能量”。

### 热力学稳定性条件

一个平衡状态要能稳定存在，它必须是一个局域的能量极小点。这一要求对热力学势函数的形式施加了严格的数学约束，即**稳定性条件**。

**力学稳定性**

对于[位移控制](@entry_id:748569)的等温系统，[亥姆霍兹自由能](@entry_id:136442) $\psi(\boldsymbol{\varepsilon}, T)$ 必须在平衡应变处是关于应变 $\boldsymbol{\varepsilon}$ 的**严格凸函数**。这意味着其[二阶偏导数](@entry_id:635213)（Hessian矩阵）必须是正定的。在小应变理论中，这个Hessian矩阵正是材料的**等温[切线刚度](@entry_id:166213)张量** $\mathbf{C}^{T}$ [@problem_id:2924973]：
$$
\mathbf{C}^{T}_{ijkl} = \frac{\partial^2\psi}{\partial\varepsilon_{ij}\partial\varepsilon_{kl}}
$$
因此，力学稳定性要求 $\delta\boldsymbol{\varepsilon}:\mathbf{C}^{T}:\delta\boldsymbol{\varepsilon} > 0$ 对所有非零的[对称张量](@entry_id:148092) $\delta\boldsymbol{\varepsilon}$ 成立。这等价于说，[刚度张量](@entry_id:176588) $\mathbf{C}^{T}$ 作为一个 $6 \times 6$ 矩阵的所有[特征值](@entry_id:154894)都必须是严格正的 [@problem_id:2924973]。需要澄清的是，这与[刚体运动](@entry_id:193355)无关；刚体运动对应于零应变，不影响此条件的判断。

**热学稳定性**

除了力学稳定性，系统还必须在热学上是稳定的。这意味着向系统输入热量应导致其温度升高，而非降低。这一物理要求等价于材料的**定应变热容** $c_{\varepsilon}$ 必须是非负的。[热容](@entry_id:137594)与亥姆霍兹自由能的关系为 [@problem_id:2925002, @problem_id:2925025]：
$$
c_{\varepsilon} = \theta \left(\frac{\partial \eta}{\partial \theta}\right)_{\varepsilon} = -\theta \frac{\partial^2\psi}{\partial\theta^2}
$$
由于 $\theta > 0$，热学稳定性条件 $c_{\varepsilon} \ge 0$ 意味着 $\frac{\partial^2\psi}{\partial\theta^2} \le 0$。换言之，[亥姆霍兹自由能](@entry_id:136442) $\psi$ 必须是关于温度 $\theta$ 的**[凹函数](@entry_id:274100)**。

一个[热弹性](@entry_id:158447)材料只有同时满足力学和热学稳定性条件，才能在宏观上表现出稳定的行为。这些条件不仅是理论上的要求，也为检验和约束具体的[本构模型](@entry_id:174726)提供了判据。例如，可以证明，如果等温[刚度张量](@entry_id:176588) $\mathbf{C}^{T}$ 是正定的，那么绝热[刚度张量](@entry_id:176588) $\mathbf{C}^{S}$ 也必然是正定的，这表明材料在绝热条件下表现得更“硬” [@problem_id:2924973]。