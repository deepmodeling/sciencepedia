## 引言
双能级系统是量子力学中最为基础，却又极具威力的核心模型之一。尽管现实世界中的量子系统（如原子、分子或人造[量子比特](@entry_id:137928)）通常拥有无数个能级，但在许多重要的物理情境下，它们的行为可以被两个关键的[量子态](@entry_id:146142)有效地主导。掌握这个看似简单的模型，是理解从原子物理、[量子光学](@entry_id:140582)到[化学反应](@entry_id:146973)和[量子计算](@entry_id:142712)等众多前沿领域复杂现象的钥匙。本文旨在系统性地剖析双能级系统的概念，填补从抽象理论到实际应用之间的认知鸿沟。

在接下来的内容中，我们将分三步深入探索双能级系统的世界。首先，在“原理与机制”一章中，我们将奠定理论基础，详细介绍其[哈密顿量](@entry_id:172864)、状态描述、相干动力学以及与环境相互作用的[退相干](@entry_id:145157)过程。接着，在“应用与跨学科连接”一章中，我们将展示该模型如何在原子钟、[激光冷却](@entry_id:138751)、[化学键](@entry_id:138216)乃至基础物理等不同学科中发挥关键作用。最后，通过“动手实践”环节，您将有机会运用所学知识解决具体的物理问题，从而巩固和深化理解。让我们从双能级系统的基本原理开始，揭开其神秘的面纱。

## 原理与机制

本章旨在深入探讨双能级系统的基本原理和核心机制。作为量子力学中最为基础却又极为强大的模型，双能级系统为我们理解从原子物理、[量子光学](@entry_id:140582)到凝聚态物质和[量子信息科学](@entry_id:150091)等众多领域的复杂现象提供了关键的理论框架。我们将从其静态性质出发，逐步引入其与经典和量子场的相互作用，探讨其相干动力学行为，并最终分析其在真实开放环境中的[退相干](@entry_id:145157)与弛豫过程。

### 抽象双能级系统：静态性质

在最抽象的层面上，一个**双能级系统**是任何一个其状态可以用两个[正交基](@entry_id:264024)底[态的叠加](@entry_id:273993)来充分描述的量子系统。这两个基底态通常被标记为 $|g\rangle$ 和 $|e\rangle$（代表[基态](@entry_id:150928)和[激发态](@entry_id:261453)），或 $|0\rangle$ 和 $|1\rangle$（在[量子计算](@entry_id:142712)的语境中）。一个任意的纯态 $|\psi\rangle$ 可以写为：
$$
|\psi\rangle = c_g |g\rangle + c_e |e\rangle
$$
其中 $c_g$ 和 $c_e$ 是复数振幅，满足[归一化条件](@entry_id:156486) $|c_g|^2 + |c_e|^2 = 1$。

#### 通用[哈密顿量](@entry_id:172864)

描述该系统演化的[哈密顿量](@entry_id:172864)算符 $H$ 是一个 $2 \times 2$ 的厄米矩阵。任何这样的矩阵都可以在泡利矩阵 $\vec{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$ 和单位矩阵 $I$ 构成的[完备基](@entry_id:143908)底上展开。一个常见且具有深刻物理意义的[哈密顿量](@entry_id:172864)形式是：
$$
H = \begin{pmatrix} \epsilon  \kappa \\ \kappa^*  -\epsilon \end{pmatrix}
$$
这里，我们假设 $\epsilon$ 是实数，$\kappa$ 可以是复数。这个[哈密顿量](@entry_id:172864)简洁地捕捉了双能级系统的两个核心物理要素 [@problem_id:2387706]：
1.  **能量偏置**：对角项 $\epsilon$ 和 $-\epsilon$ 代表了两个基底态 $|g\rangle$ 和 $|e\rangle$ 之间的能量差的一半。若以 $|g\rangle$ 和 $|e\rangle$ 为能量本征态（即无耦合时），它们的能量将是 $-\epsilon$ 和 $\epsilon$。参数 $\epsilon$ 通常与外部场（如[电场](@entry_id:194326)或[磁场](@entry_id:153296)）导致的能级失谐有关。
2.  **耦合**：非对角项 $\kappa$ 代表了两个基底态之间的相互作用或耦合。这种耦合使得系统可以在 $|g\rangle$ 和 $|e\rangle$ 之间跃迁，并导致[能量本征态](@entry_id:152154)不再是纯粹的 $|g\rangle$ 或 $|e\rangle$，而是它们的叠加。

#### [本征态](@entry_id:149904)与本征能量

为了找到系统的**[能量本征态](@entry_id:152154)**（也称为[定态](@entry_id:137260)）和相应的**本征能量**，我们需要求解[哈密顿量](@entry_id:172864)的本征值问题 $H|\psi\rangle = E|\psi\rangle$。这等价于求解[特征方程](@entry_id:265849) $\det(H - E I) = 0$：
$$
\det\begin{pmatrix} \epsilon - E  \kappa \\ \kappa^*  -(\epsilon + E) \end{pmatrix} = -(\epsilon - E)(\epsilon + E) - |\kappa|^2 = E^2 - \epsilon^2 - |\kappa|^2 = 0
$$
解得两个本征能量为：
$$
E_{\pm} = \pm \sqrt{\epsilon^2 + |\kappa|^2}
$$
这两个能量值代表了系统允许存在的真实能级。较低的能量 $E_- = -\sqrt{\epsilon^2 + |\kappa|^2}$ 对应系统的**[基态](@entry_id:150928)**，而较高的能量 $E_+ = +\sqrt{\epsilon^2 + |\kappa|^2}$ 对应**[激发态](@entry_id:261453)**。能级之间的能量差，即**[能隙](@entry_id:191975)**，为 $\Delta E = E_+ - E_- = 2\sqrt{\epsilon^2 + |\kappa|^2}$。一个重要的现象是**能级反交叉**（level anti-crossing）：即使在两个原始基底态[能量简并](@entry_id:203091)（$\epsilon=0$）的情况下，只要存在耦合（$\kappa \neq 0$），系统能级之间仍然会有一个大小为 $2|\kappa|$ 的[能隙](@entry_id:191975)。耦合作用“推开”了原本会[交叉](@entry_id:147634)的能级。

与能量 $E_-$ 对应的[基态](@entry_id:150928)本征矢量 $|\psi_-\rangle = v_1|g\rangle + v_2|e\rangle$ 的分量比值 $r = v_2/v_1$ 可以通过[求解矩阵方程](@entry_id:196604) $(H - E_- I)|\psi_-\rangle = 0$ 得到。利用第一行方程 $(\epsilon - E_-)v_1 + \kappa v_2 = 0$，我们有 [@problem_id:2387706]：
$$
r = \frac{v_2}{v_1} = -\frac{\epsilon - E_-}{\kappa} = -\frac{\epsilon + \sqrt{\epsilon^2 + |\kappa|^2}}{\kappa}
$$
这个比值揭示了[能量本征态](@entry_id:152154)是如何由原始基底[态混合](@entry_id:148060)而成的。例如，当系统处于[对称点](@entry_id:174836) $\epsilon=0$ 且 $\kappa$ 为实数时，$r = -|\kappa|/\kappa = -\text{sgn}(\kappa)$，这意味着[基态](@entry_id:150928)和[激发态](@entry_id:261453)是 $|g\rangle$ 和 $|e\rangle$ 的等权重叠加态。当耦合很弱（$|\kappa| \ll |\epsilon|$）时，[本征态](@entry_id:149904)近似于原始的基底态。

### 状态的描述：布洛赫球

为了直观地表示一个双能级系统的任意纯态，我们引入了**布洛赫球（Bloch Sphere）**。球的“北极”和“南极”分别代表[激发态](@entry_id:261453) $|e\rangle$ 和[基态](@entry_id:150928) $|g\rangle$。球面上任何一点都唯一对应一个[纯态](@entry_id:141688)。这个对应关系是通过**[布洛赫矢量](@entry_id:144181)** $\vec{r}=(u,v,w)$ 建立的，其分量定义为泡利算符的[期望值](@entry_id:153208)：
$$
u = \langle\psi|\sigma_x|\psi\rangle, \quad v = \langle\psi|\sigma_y|\psi\rangle, \quad w = \langle\psi|\sigma_z|\psi\rangle
$$
对于纯态，[布洛赫矢量](@entry_id:144181)的模长 $|\vec{r}| = \sqrt{u^2+v^2+w^2} = 1$，因此它总位于球面上。

然而，在许多现实情况下，系统可能不处于一个确定的纯态，而是处于不同[纯态](@entry_id:141688)的统计混合中。这种状态被称为**[混合态](@entry_id:141568)**，必须用**[密度算符](@entry_id:138151)（density operator）** $\rho$ 来描述。对于一个双能级系统，任何[密度算符](@entry_id:138151)都可以通过[布洛赫矢量](@entry_id:144181) $\vec{r}$ 进行[参数化](@entry_id:272587) [@problem_id:2820203]：
$$
\rho(\vec{r}) = \frac{1}{2}(I + \vec{r}\cdot \vec{\sigma})
$$
[密度算符](@entry_id:138151)必须满足三个基本性质：(1) 它是厄米的（$\rho = \rho^\dagger$）；(2) 它是半正定的（$\rho \ge 0$，即所有[本征值](@entry_id:154894)非负）；(3) 它的迹为1（$\text{Tr}(\rho) = 1$）。

通过利用泡利矩阵的代数性质 $(\vec{a}\cdot\vec{\sigma})(\vec{b}\cdot\vec{\sigma}) = (\vec{a}\cdot\vec{b})I + i(\vec{a} \times \vec{b})\cdot\vec{\sigma}$，我们可以优雅地找到 $\rho(\vec{r})$ 的[本征值](@entry_id:154894)。具体来说，算符 $\vec{r}\cdot\vec{\sigma}$ 的平方为 $(\vec{r}\cdot\vec{\sigma})^2 = |\vec{r}|^2 I$，这意味着它的[本征值](@entry_id:154894)为 $\pm|\vec{r}|$。由此可得，$\rho(\vec{r})$ 的[本征值](@entry_id:154894)为：
$$
\lambda_{\pm} = \frac{1 \pm |\vec{r}|}{2}
$$
[半正定性](@entry_id:147720)要求 $\lambda_{\pm} \ge 0$，这直接导致了 $|\vec{r}| \le 1$。这个重要的结果表明，所有可能的[量子态](@entry_id:146142)（纯态和[混合态](@entry_id:141568)）都对应于单位球体内的点，这个球体被称为**布洛赫球体（Bloch Ball）**。[纯态](@entry_id:141688)位于球的表面（$|\vec{r}|=1$），而[混合态](@entry_id:141568)则填充其内部（$|\vec{r}|  1$）。[完全混合态](@entry_id:139247) $\rho = I/2$ 对应于球心 $\vec{r}=\vec{0}$。

### 相干动力学：与经典场的相互作用

双能级系统最重要的应用之一是描述其与外部经典[电磁场](@entry_id:265881)的相互作用，例如原子与[激光](@entry_id:194225)场的相互作用。总[哈密顿量](@entry_id:172864)为 $H(t) = H_0 + V(t)$，其中 $H_0$ 是自由[哈密顿量](@entry_id:172864)， $V(t)$ 是描述相互作用的时变项。

为了简化分析，我们通常会变换到一个以场的频率 $\omega$ 旋转的[参考系](@entry_id:169232)，并采用**[旋转波近似](@entry_id:204016)（Rotating Wave Approximation, RWA）**。该近似在近共振驱动（$|\omega - \omega_0| \ll \omega_0$）和[弱耦合](@entry_id:140994)条件下成立，它忽略了高频[振荡](@entry_id:267781)项，从而将一个时变[哈密顿量](@entry_id:172864)简化为一个等效的、不含时的[哈密顿量](@entry_id:172864) $H_{\rm eff}$。在旋转系中，系统的演化就变成了[布洛赫矢量](@entry_id:144181)围绕一个固定的有效磁场方向的进动。

#### [拉比振荡](@entry_id:137940)（共振驱动）

最简单的情形是**共振驱动**，即[激光](@entry_id:194225)频率 $\omega$ 与原子跃迁频率 $\omega_0$ 完全匹配。在这种情况下，旋转系中的有效哈密顿量可以写为 $H_{\rm eff} = \frac{\hbar\Omega}{2}\sigma_x$，其中 $\Omega$ 是**[拉比频率](@entry_id:154019)（Rabi frequency）**，它正比于驱动场的振幅和[原子跃迁](@entry_id:158267)偶极矩。

在这种[哈密顿量](@entry_id:172864)的作用下，如果系统初始处于[基态](@entry_id:150928) $|g\rangle$（布洛赫球南极），其状态将围绕布洛赫球的x轴旋转。经过时间 $T$ 后，状态变为 [@problem_id:747107]：
$$
|\psi(T)\rangle = \cos\left(\frac{\theta}{2}\right)|g\rangle - i\sin\left(\frac{\theta}{2}\right)|e\rangle
$$
这里的 $\theta = \Omega T$ 被称为**脉冲面积（pulse area）**。通过精确控制脉冲的持续时间 $T$ 或强度 $\Omega$，我们可以实现对[量子态](@entry_id:146142)的任意相干操控。例如：
*   **$\pi/2$-脉冲** ($\theta = \pi/2$)：将系统制备到 $|g\rangle$ 和 $|e\rangle$ 的等权重叠加态上，对应于布洛赫球赤道上的一个点。
*   **$\pi$-脉冲** ($\theta = \pi$)：将系统从[基态](@entry_id:150928) $|g\rangle$ 完全翻转到[激发态](@entry_id:261453) $|e\rangle$。

这种由相干驱动引起的[布洛赫矢量](@entry_id:144181)周期性旋转以及布居数在 $|g\rangle$ 和 $|e\rangle$ 之间的周期性[振荡](@entry_id:267781)被称为**[拉比振荡](@entry_id:137940)**。

#### 广义[拉比振荡](@entry_id:137940)（[失谐](@entry_id:148084)驱动）

当驱动场与[原子跃迁](@entry_id:158267)存在**失谐（detuning）** $\Delta = \omega_0 - \omega \neq 0$ 时，情况变得更为复杂。在[旋转波近似](@entry_id:204016)下，旋转系中的[有效哈密顿量](@entry_id:748813)变为 [@problem_id:747208]：
$$
H_{\rm eff} = \frac{\hbar}{2}(\Delta \sigma_z + \Omega \sigma_x) = \frac{\hbar}{2} \vec{\Omega}_{\rm eff} \cdot \vec{\sigma}
$$
这里的有效场矢量为 $\vec{\Omega}_{\rm eff} = (\Omega, 0, \Delta)$。此时，[布洛赫矢量](@entry_id:144181)不再是绕着单纯的x轴或z轴旋转，而是绕着由 $\vec{\Omega}_{\rm eff}$ 定义的轴 $\hat{n} = \vec{\Omega}_{\rm eff} / |\vec{\Omega}_{\rm eff}|$ 进行进动。进动的角频率被称为**广义[拉比频率](@entry_id:154019)**：
$$
\Omega_{\rm gen} = |\vec{\Omega}_{\rm eff}| = \sqrt{\Omega^2 + \Delta^2}
$$
在脉冲持续时间 $\tau$ 内，[布洛赫矢量](@entry_id:144181)绕 $\hat{n}$ 轴旋转的总角度为 $\Theta = \Omega_{\rm gen} \tau$。这些参数，如旋转轴的z分量 $n_z = \Delta/\Omega_{\rm gen}$ 和总旋转角 $\Theta$，共同决定了[失谐](@entry_id:148084)驱动下[量子态](@entry_id:146142)的最终演化 [@problem_id:747208]。

#### [AC斯塔克位移](@entry_id:161492)

在**远[失谐](@entry_id:148084)**极限下，即 $|\Delta| \gg |\Omega|$，系统的动力学呈现出一种特别有用的形式。此时，[激发态](@entry_id:261453)的振幅 $c_e(t)$ 的演化时间尺度远快于[基态](@entry_id:150928)振幅 $c_g(t)$。我们可以运用**绝热消除（adiabatic elimination）**技术，假设[激发态](@entry_id:261453)瞬时地响应[基态](@entry_id:150928)的变化，即令 $\dot{c}_e \approx 0$。通过这个近似，我们可以将[激发态](@entry_id:261453)“消去”，从而得到一个只作用于[基态](@entry_id:150928)的[有效哈密顿量](@entry_id:748813)。

这个过程的结果是，[基态](@entry_id:150928)的能量发生了一个微小的移动，这个移动被称为**[AC斯塔克位移](@entry_id:161492)（AC Stark shift）**或**光致位移（light shift）** [@problem_id:747232]。其大小为：
$$
\delta E_g = -\frac{\hbar\Omega^2}{4\Delta}
$$
这个效应表明，一个远失谐的光场并不会显著地激发原子，而是主要起到“修饰”其能级结构的作用。[AC斯塔克位移](@entry_id:161492)在[原子钟](@entry_id:147849)、[量子逻辑门](@entry_id:142100)和囚禁中性原子等领域有至关重要的应用。

### 与量子场的相互作用：[缀饰态](@entry_id:143646)

前面的讨论假设驱动场是经典的。然而，当双能级系统与一个**量子化**的[电磁场](@entry_id:265881)模式（例如在[光学微腔](@entry_id:262849)中）相互作用时，会出现新的量子现象。描述这种相互作用的[典范模型](@entry_id:198268)是**Jaynes-Cummings模型** [@problem_id:747087]。其[哈密顿量](@entry_id:172864)为：
$$
H_{JC} = \frac{1}{2}\hbar \omega_0 \sigma_z + \hbar \omega a^\dagger a + \hbar g (\sigma_+ a + \sigma_- a^\dagger)
$$
其中第一项是原子[哈密顿量](@entry_id:172864)，第二项是单模光场[哈密顿量](@entry_id:172864)（$a^\dagger, a$ 是[光子](@entry_id:145192)产生和湮灭算符），第三项是[相互作用项](@entry_id:637283)，$g$ 是[耦合强度](@entry_id:275517)。该模型有一个[守恒量](@entry_id:150267)：总激发数 $N = a^\dagger a + \sigma_+\sigma_-$。

考虑共振情况 $\omega = \omega_0$，并考察总激发数为一的[子空间](@entry_id:150286)，该[子空间](@entry_id:150286)由两个态 $|e, 0\rangle$（原子在[激发态](@entry_id:261453)，光场为真空）和 $|g, 1\rangle$（原子在[基态](@entry_id:150928)，光场有一个[光子](@entry_id:145192)）张成。在这个基底下，Jaynes-Cummings[哈密顿量](@entry_id:172864)矩阵为：
$$
H_{N=1} = \begin{pmatrix} \frac{1}{2}\hbar\omega_0  \hbar g \\ \hbar g  \frac{1}{2}\hbar\omega_0 \end{pmatrix}
$$
这个矩阵的结构与我们最初讨论的静态[哈密顿量](@entry_id:172864)惊人地相似。其[本征值](@entry_id:154894)是 $E_{\pm} = \frac{1}{2}\hbar\omega_0 \pm \hbar g$，对应的[本征态](@entry_id:149904)是：
$$
|\pm\rangle = \frac{1}{\sqrt{2}}(|e,0\rangle \pm |g,1\rangle)
$$
这些新的[本征态](@entry_id:149904)被称为**[缀饰态](@entry_id:143646)（dressed states）**。它们不再是纯粹的原子态或[光子](@entry_id:145192)态，而是原子和[光子](@entry_id:145192)的纠缠态。由于相互作用，原本简并的 $|e,0\rangle$ 和 $|g,1\rangle$ [能级分裂](@entry_id:193178)成两个相距 $\Delta E = 2\hbar g$ 的新能级。这个分裂被称为**[真空拉比分裂](@entry_id:145897)（vacuum Rabi splitting）**，是[腔量子电动力学](@entry_id:149422)（Cavity QED）中强耦合的标志性特征。

### [开放量子系统](@entry_id:138632)：弛豫与退相干

真实的量子系统总是与周围环境发生相互作用，这导致了能量的耗散和量子相干性的丧失，这一过程统称为**[退相干](@entry_id:145157)（decoherence）**。

#### 唯象描述：[光学布洛赫方程](@entry_id:171131)

描述开放双能级系统动力学最常用的[唯象模型](@entry_id:273816)是**[光学布洛赫方程](@entry_id:171131)** [@problem_id:747110]。对于一个在没有外部驱动下自由演化的系统，[布洛赫矢量](@entry_id:144181)各分量的方程为：
$$
\frac{du}{dt} = -\omega_0 v - \frac{u}{T_2}
$$
$$
\frac{dv}{dt} = \omega_0 u - \frac{v}{T_2}
$$
$$
\frac{dw}{dt} = -\frac{w - w_{eq}}{T_1}
$$
这里引入了两个关键的[弛豫时间](@entry_id:191572)：
*   **纵向弛豫时间 $T_1$**：描述布居数差 $w$ 弛豫到其热平衡值 $w_{eq}$ 的时间尺度。它代表了能量耗散的速率，例如通过自发辐射从[激发态](@entry_id:261453)衰变到[基态](@entry_id:150928)。因此，$T_1$ 也被称为**布居数[弛豫时间](@entry_id:191572)**。
*   **横向弛豫时间 $T_2$**：描述相干项 $u$ 和 $v$ 衰减到零的时间尺度。它代表了量子叠加态相位关系被破坏的速率。因此，$T_2$ 也被称为**[退相干时间](@entry_id:154396)**或**退相位时间**。

通常，$T_2 \le 2T_1$。$T_2$ 不仅受[能量弛豫](@entry_id:136820)的影响，还受到不引起能量改变的“纯退相位”过程（如环境噪声引起的能级随机波动）的影响。这些方程描述了[布洛赫矢量](@entry_id:144181)如何螺旋式地收缩到[平衡点](@entry_id:272705) $(0, 0, w_{eq})$ 的过程。

#### 退相干的微观模型

虽然[布洛赫方程](@entry_id:153789)提供了有效的唯象描述，但更深入的理解需要从微观层面考虑[系统与环境](@entry_id:142270)的相互作用。

**[费米黄金定则](@entry_id:146239)与环境[态密度](@entry_id:147894)**：[能量弛豫](@entry_id:136820)过程，如自发辐射，可以用**[费米黄金定则](@entry_id:146239)**来描述。该定则指出，从一个初态到一系列末态的跃迁速率正比于耦合强度的平方和末态的**态密度（Density of States, DOS）**。一个引人注目的例子是耦合到超导[谐振腔](@entry_id:274488)中的[量子比特](@entry_id:137928) [@problem_id:747177]。其[自发辐射率](@entry_id:189089) $\Gamma$ 不仅取决于内在的耦合强度 $\gamma_0$，还强烈地依赖于[超导体](@entry_id:191025)中[准粒子激发](@entry_id:138475)的[态密度](@entry_id:147894) $\rho_{rel}(E)$：
$$
\Gamma(\omega_q) = \gamma_0 \cdot \rho_{rel}(\hbar\omega_q)
$$
对于一个BCS[超导体](@entry_id:191025)，其[态密度](@entry_id:147894)在[能隙](@entry_id:191975) $\Delta$ 以下为零，而在[能隙](@entry_id:191975)边缘发散。因此，当我们将[量子比特](@entry_id:137928)的频率 $\omega_q$ 扫过[超导能隙](@entry_id:145058)时，其衰变速率会表现出急剧的变化。这展示了通过设计环境的谱结构（**[能谱](@entry_id:181780)工程**）来控制量子系统[退相干](@entry_id:145157)的可能性。

**噪声谱密度与动力学解耦**：退相位过程通常源于环境噪声导致的系统[哈密顿量](@entry_id:172864)参数（如跃迁频率）的随机波动 $\delta\omega(t)$。这些波动的统计特性可以通过其**噪声谱密度 $S(\omega)$** 来刻画。系统的相干性衰减 $L(\tau) = e^{-\chi(\tau)}$ 中的[退相干](@entry_id:145157)指数 $\chi(\tau)$ 可以通过一个包含 $S(\omega)$ 和一个**滤[波函数](@entry_id:147440)（filter function）** $F(\omega, \tau)$ 的积分来计算。
$$
\chi(\tau) = \frac{1}{2\pi} \int_0^\infty d\omega \, S(\omega) \frac{F(\omega, \tau)}{\omega^2}
$$
滤[波函数](@entry_id:147440) $F(\omega, \tau)$ 由施加在[量子比特](@entry_id:137928)上的控制[脉冲序列](@entry_id:753864)决定。这意味着我们可以通过设计[脉冲序列](@entry_id:753864)来“塑造”系统对不同频率噪声的敏感度。一个典型的例子是**[哈恩回波](@entry_id:139051)（Hahn-echo）**序列 [@problem_id:747005]，它包含一个中心$\pi$脉冲，能有效地滤除低频噪声，从而延长相干时间。这种利用控制脉冲来抑制退相干的技术被称为**动力学解耦（dynamical decoupling）**。

### 时变[哈密顿量](@entry_id:172864)：绝热与非[绝热演化](@entry_id:153352)

最后，我们考虑[哈密顿量](@entry_id:172864)本身随时间缓慢变化的情形。**[绝热定理](@entry_id:142116)（Adiabatic Theorem）**指出，如果一个系统初始处于[哈密顿量](@entry_id:172864)的一个瞬时[本征态](@entry_id:149904)，并且[哈密顿量](@entry_id:172864)变化得足够缓慢，那么系统将始终保持在该瞬时本征态上。

然而，当[哈密顿量](@entry_id:172864)的变化不是无限慢时，系统就有可能从一个瞬时[本征态](@entry_id:149904)跃迁到另一个。描述这种**[非绝热跃迁](@entry_id:199204)**的最著名模型是**[Landau-Zener模型](@entry_id:190135)** [@problem_id:747251]。其[哈密顿量](@entry_id:172864)为：
$$
H(t) = \frac{1}{2}\alpha t \, \sigma_z + V \sigma_x
$$
这描述了一个双能级系统，其能量偏置以速率 $\alpha$ 线性扫描通过一个由耦合 $V$ 产生的宽度为 $2V$ 的反[交叉点](@entry_id:147634)。系统在 $t \to -\infty$ 时处于[基态](@entry_id:150928)，在 $t \to +\infty$ 时发生[非绝热跃迁](@entry_id:199204)到[激发态](@entry_id:261453)的概率为：
$$
P_{na} = \exp\left(-\frac{2\pi V^2}{\hbar\alpha}\right)
$$
这个**[Landau-Zener公式](@entry_id:139974)**揭示了绝热性的关键判据：跃迁概率由[能隙](@entry_id:191975)大小 $V$ 和扫描速率 $\alpha$ 的比值决定。当[扫描速率](@entry_id:137671)很快（$\alpha$ 大）或[能隙](@entry_id:191975)很小（$V$ 小）时，系统倾向于保持其原始的“裸态”（**非绝热的**或**透射的**演化）。反之，当扫描缓慢（$\alpha$ 小）或[能隙](@entry_id:191975)很大（$V$ 大）时，系统将跟随瞬时[本征态](@entry_id:149904)演化（**绝热的**演化）。[Landau-Zener跃迁](@entry_id:148864)在原子与[分子碰撞](@entry_id:137334)、[量子退火](@entry_id:141606)以及[量子比特](@entry_id:137928)的[绝热演化](@entry_id:153352)控制中扮演着核心角色。