## 引言
在凝聚态物理与光学领域，理解和操控[光与物质的相互作用](@entry_id:268903)是推动技术发展的核心。其中，[声子](@entry_id:140728)-极化激元作为一种由[光子](@entry_id:145192)与[晶格振动](@entry_id:140970)（[声子](@entry_id:140728)）强烈耦合而形成的混合[准粒子](@entry_id:136584)，构成了这一研究领域的重要基石。它不仅揭示了[电磁波](@entry_id:269629)在极性材料中传播的奇特行为，更为在纳米尺度上调控光能和热能提供了全新的途径。然而，这种[混合态](@entry_id:141568)的本质、其能量-动量关系以及它如何引发宏观光学现象，往往是初学者面临的知识难点。

本文旨在系统地揭开[声子](@entry_id:140728)-[极化激元](@entry_id:142951)的神秘面纱。我们将从最基本的物理图像出发，逐步构建一个完整的理论框架，并将其与前沿的科学应用紧密相连。通过阅读本文，您将深入理解光-物质耦合的内在机制，并掌握分析相关现象的关键工具。

在接下来的“**原理与机制**”一章中，我们将基于经典电磁学和[晶格动力学](@entry_id:145448)，推导[声子](@entry_id:140728)-[极化激元](@entry_id:142951)的[色散关系](@entry_id:140395)，并阐明反交叉、[禁带](@entry_id:175956)等核心概念。随后，在“**应用与跨学科连接**”部分，我们将展示这些理论如何在[纳米光子学](@entry_id:137892)、[近场](@entry_id:269780)热科学和量子技术等领域催生革命性的应用，例如表面模式对光的束缚和对[热辐射](@entry_id:145102)的增强效应。最后，通过“**动手实践**”环节提供的一系列计算问题，您将有机会亲手应用所学知识，巩固对这一迷人物理现象的理解。

## 原理与机制

本章深入探讨[声子](@entry_id:140728)-[极化激元](@entry_id:142951)的物理原理和基本机制。我们将从[晶格动力学](@entry_id:145448)和经典电磁学的基本方程出发，构建一个描述光与极性晶体中[晶格振动](@entry_id:140970)相互作用的理论框架。通过这一框架，我们将推导出极化激元的[色散关系](@entry_id:140395)，揭示其作为[光子](@entry_id:145192)和[声子](@entry_id:140728)混合[准粒子](@entry_id:136584)的内在属性。此外，我们还将讨论阻尼、量子化以及温度等实际因素对[极化激元](@entry_id:142951)性质的影响。

### 离子晶体[介电响应](@entry_id:140146)的[洛伦兹模型](@entry_id:144803)

为了理解[光与物质的相互作用](@entry_id:268903)，我们首先需要一个能够描述物质如何响应[电磁场](@entry_id:265881)的模型。在红外频率范围内，极性离子晶体（如 GaAs 或 SiC）的光学性质主要由晶格振动决定，特别是**光学声子**。[光学声子](@entry_id:136993)是指[晶胞](@entry_id:143489)中不同电性的离子（或原子团）发生相对位移的[集体振动模](@entry_id:160059)式。由于这种相对位移会产生一个[振荡](@entry_id:267781)的电偶极矩，因此该模式可以与[电磁场](@entry_id:265881)直接耦合，这类[声子](@entry_id:140728)被称为**[红外活性](@entry_id:267987)**的。

我们可以将这种红外活性的**横向光学（TO）[声子](@entry_id:140728)**的动力学行为，近似地看作一个受[电场](@entry_id:194326)驱动的[经典谐振子](@entry_id:153404)。考虑一个简化模型，其中每个原胞的离子[相对运动](@entry_id:169798)等效为一个有效[振子](@entry_id:271549)，其约化质量为 $M$，有效电荷为 $Z^*$。在[宏观电场](@entry_id:196409) $E(t)$ 的驱动下，其位移 $u(t)$ 遵循如下的[运动方程](@entry_id:170720) [@problem_id:2852767] [@problem_id:2852791]：

$$
M \ddot{u}(t) + M \gamma \dot{u}(t) + M \omega_{\mathrm{TO}}^{2} u(t) = Z^{*} E(t)
$$

这里，$\omega_{\mathrm{TO}}$ 是[横向光学声子](@entry_id:139212)的固有共振角频率，$\gamma$ 是一个唯象的阻尼常数，代表了[声子散射](@entry_id:140674)等能量耗散过程。

当存在 $N$ 个这样的[振子](@entry_id:271549)单位体积时，它们共同构成了宏观的**[离子极化](@entry_id:145365)强度** $P_{\mathrm{ion}}(t) = N Z^{*} u(t)$。对于一个频率为 $\omega$ 的时谐[电场](@entry_id:194326) $E(t) = \Re\{E(\omega) e^{-i \omega t}\}$，我们可以求解上述[运动方程](@entry_id:170720)，得到[频域](@entry_id:160070)中的[离子极化](@entry_id:145365)强度：

$$
P_{\mathrm{ion}}(\omega) = \frac{N (Z^{*})^2 / M}{\omega_{\mathrm{TO}}^2 - \omega^2 - i\omega\gamma} E(\omega)
$$

材料的总[电位移场](@entry_id:273493) $D(\omega)$ 由真空位移、[电子极化](@entry_id:145269)以及[离子极化](@entry_id:145365)三部分贡献。电子的响应速度远快于离子，在红外波段，我们可以认为[电子极化](@entry_id:145269)是瞬时的，并将其贡献包含在一个与频率无关的**高频[介电常数](@entry_id:146714)** $\epsilon_{\infty}$ 中。因此，总的[电位移场](@entry_id:273493)可以写为 $D(\omega) = \epsilon_0 \epsilon_{\infty} E(\omega) + P_{\mathrm{ion}}(\omega)$，其中 $\epsilon_0$ 是[真空介电常数](@entry_id:204253)。

根据定义，$D(\omega) = \epsilon_0 \epsilon(\omega) E(\omega)$，其中 $\epsilon(\omega)$ 是我们寻求的总的频率依赖的相对[介电函数](@entry_id:136859)。结合以上关系，我们可以推导出介电函数的形式。为简化讨论，我们首先忽略阻尼（$\gamma \to 0$）：

$$
\epsilon(\omega) = \epsilon_{\infty} + \frac{N (Z^{*})^2}{\epsilon_0 M (\omega_{\mathrm{TO}}^2 - \omega^2)}
$$

这个表达式中的微观参数（$N, Z^*, M$）可以通过宏观可测量的量来替代。我们知道，在[静态极限](@entry_id:262480)下（$\omega \to 0$），[介电函数](@entry_id:136859)趋于**静态[介电常数](@entry_id:146714)** $\epsilon(0)$。利用这个关系，我们可以确定振子强度项：$N (Z^{*})^2 / (\epsilon_0 M) = (\epsilon(0) - \epsilon_{\infty}) \omega_{\mathrm{TO}}^2$。将其代回，我们便得到了[介电函数](@entry_id:136859)的标准洛伦兹形式 [@problem_id:2810157] [@problem_id:762809]：

$$
\epsilon(\omega) = \epsilon_{\infty} + \frac{(\epsilon(0) - \epsilon_{\infty})\omega_{\mathrm{TO}}^2}{\omega_{\mathrm{TO}}^2 - \omega^2}
$$

这个公式是理解极性介质中[声子](@entry_id:140728)与[光子](@entry_id:145192)耦合现象的基石。

### 纵向与横向[光学模式](@entry_id:188043)

[介电函数](@entry_id:136859) $\epsilon(\omega)$ 的特殊点——[极点和零点](@entry_id:262457)——具有深刻的物理意义，它们分别对应于材料中不同类型的集体激发。

**横向光学（TO）[声子](@entry_id:140728)**：从介电函数的表达式可以看出，当入射光的频率 $\omega$ 接近 $\omega_{\mathrm{TO}}$ 时，$\epsilon(\omega)$ 出现一个**极点**（发散）。这对应于一个共振现象：一个横向的[电场](@entry_id:194326)能够非常有效地驱动[晶格](@entry_id:196752)产生横向的[偶极振荡](@entry_id:261900)。因此，$\omega_{\mathrm{TO}}$ 被确定为[横向光学声子](@entry_id:139212)的频率 [@problem_id:2852776]。

**纵向光学（LO）[声子](@entry_id:140728)**：与横向波不同，纵向波的极化方向平行于其[波矢](@entry_id:178620)方向。对于一个没有外部[自由电荷](@entry_id:264392)的介质，麦克斯韦方程中的高斯定律要求[电位移场](@entry_id:273493) $\mathbf{D}$ 的散度为零（$\nabla \cdot \mathbf{D} = 0$）。对于一个纵向[平面波](@entry_id:189798)，这意味着 $\mathbf{D}$ 场本身必须为零。然而，这并不意味着[电场](@entry_id:194326) $\mathbf{E}$ 也必须为零。根据关系式 $\mathbf{D} = \epsilon_0 \epsilon(\omega) \mathbf{E}$，只要[介电函数](@entry_id:136859)为零，即 $\epsilon(\omega) = 0$，就可以存在一个非零的纵向[电场](@entry_id:194326)。这种不依赖于外部驱动、仅由材料自身性质决定的自持纵向集体振荡，其频率就被定义为**纵向光学（LO）[声子](@entry_id:140728)**的频率 $\omega_{\mathrm{LO}}$ [@problem_id:2852791] [@problem_id:2852776]。

通过令 $\epsilon(\omega_{\mathrm{LO}}) = 0$，我们可以从介电函数的洛伦兹形式中推导出一个至关重要的关系：

$$
0 = \epsilon_{\infty} + \frac{(\epsilon(0) - \epsilon_{\infty})\omega_{\mathrm{TO}}^2}{\omega_{\mathrm{TO}}^2 - \omega_{\mathrm{LO}}^2}
$$

整理后得到：

$$
\frac{\omega_{\mathrm{LO}}^2}{\omega_{\mathrm{TO}}^2} = \frac{\epsilon(0)}{\epsilon_{\infty}}
$$

这就是著名的**里丹-萨克斯-泰勒（Lyddane-Sachs-Teller, LST）关系** [@problem_id:2852791] [@problem_id:2810157]。它将材料的微观[振动](@entry_id:267781)特性（$\omega_{\mathrm{LO}}$ 和 $\omega_{\mathrm{TO}}$）与宏观介电特性（$\epsilon(0)$ 和 $\epsilon_{\infty}$）直接联系起来。由于在[离子晶体](@entry_id:138598)中，离子[振动](@entry_id:267781)对极化有贡献，$\epsilon(0)$ 总是大于 $\epsilon_{\infty}$，因此 LST 关系预言了 $\omega_{\mathrm{LO}} > \omega_{\mathrm{TO}}$。这个频率差，即所谓的 **LO-TO 劈裂（splitting）**，其根源在于与 LO [声子](@entry_id:140728)相伴的宏观退极化[电场](@entry_id:194326)，它为[晶格振动](@entry_id:140970)提供了额外的恢复力，从而抬高了其频率。

利用 LST 关系，我们可以将介电函数写成一个更为简洁的因式分解形式 [@problem_id:3008337] [@problem_id:2848389]：

$$
\epsilon(\omega) = \epsilon_{\infty} \frac{\omega_{\mathrm{LO}}^2 - \omega^2}{\omega_{\mathrm{TO}}^2 - \omega^2}
$$

这个形式在后续分析中极为方便。

### [声子](@entry_id:140728)-[极化激元](@entry_id:142951)：光与[晶格](@entry_id:196752)的耦合

至此，我们已经建立了描述材料光学响应的模型。现在，我们将这个模型与麦克斯韦方程结合，来考察[电磁波](@entry_id:269629)在这样的极性介质中的传播行为。在没有[自由电流](@entry_id:191634)和[电荷](@entry_id:275494)的非磁性介质中，麦克斯韦方程可以导出一个[波动方程](@entry_id:139839)。对于一个角频率为 $\omega$、[波矢](@entry_id:178620)为 $\mathbf{k}$ 的横向[电磁波](@entry_id:269629)（$\mathbf{k} \perp \mathbf{E}$），其在介质中的传播由以下**色散关系**所描述 [@problem_id:3008337] [@problem_id:2852763]：

$$
k^2 c^2 = \omega^2 \epsilon(\omega)
$$

这里的 $k=|\mathbf{k}|$ 是波矢的大小，$c$ 是[真空中的光速](@entry_id:272753)。这个方程的解 $\omega(k)$ 不再是简单的[线性关系](@entry_id:267880)，如真空中的光（$\omega=ck$）或普通介质中的光（$\omega=ck/n$）。相反，它描述了一种新的激发模式，这种模式既有[电磁场](@entry_id:265881)的性质，又有[晶格振动](@entry_id:140970)的性质。这种[光子](@entry_id:145192)与[声子](@entry_id:140728)强烈耦合形成的混合[准粒子](@entry_id:136584)，被称为**[声子](@entry_id:140728)-[极化激元](@entry_id:142951)（phonon-polariton）**。

将介电函数的[因式分解](@entry_id:150389)形式代入[色散关系](@entry_id:140395)，我们得到描述[声子](@entry_id:140728)-极化激元的[隐式方程](@entry_id:177636)：

$$
k^2 c^2 = \omega^2 \epsilon_{\infty} \frac{\omega_{\mathrm{LO}}^2 - \omega^2}{\omega_{\mathrm{TO}}^2 - \omega^2}
$$

为了让波能够在介质中无衰减地传播，波矢 $k$ 必须是一个实数，这意味着 $k^2$ 必须为正。由于 $\omega^2$ 和 $c^2$ 总是正的，传播的条件就简化为 $\epsilon(\omega) \ge 0$。

分析 $\epsilon(\omega)$ 的正负区间：
- 当 $\omega  \omega_{\mathrm{TO}}$ 或 $\omega > \omega_{\mathrm{LO}}$ 时，$\omega_{\mathrm{LO}}^2 - \omega^2$ 和 $\omega_{\mathrm{TO}}^2 - \omega^2$ 同号，因此 $\epsilon(\omega) > 0$。在这些频率范围内，存在传播的[极化激元](@entry_id:142951)模式。
- 当 $\omega_{\mathrm{TO}}  \omega  \omega_{\mathrm{LO}}$ 时，$\omega_{\mathrm{LO}}^2 - \omega^2 > 0$ 而 $\omega_{\mathrm{TO}}^2 - \omega^2  0$，导致 $\epsilon(\omega)  0$。此时 $k^2  0$，$k$ 成为纯虚数。这意味着入射到材料表面的该频率范围内的[电磁波](@entry_id:269629)无法在体内传播，而是会迅速衰减，并被高效率地反射。这个禁止传播的频率带被称为**[禁带](@entry_id:175956)（stop band）**或**[剩余射线带](@entry_id:147008)（Reststrahlen band）**，其宽度为 $\Delta f = f_{\mathrm{LO}} - f_{\mathrm{TO}}$ [@problem_id:2852763]。例如，对于一个给定的晶体，如果其 TO 和 LO [声子](@entry_id:140728)[波数](@entry_id:172452)分别为 $\tilde{\nu}_{\mathrm{TO}} = 797\,\mathrm{cm}^{-1}$ 和 $\tilde{\nu}_{\mathrm{LO}} = 972\,\mathrm{cm}^{-1}$，其[剩余射线带](@entry_id:147008)的频率宽度就是 $\Delta f = c (\tilde{\nu}_{\mathrm{LO}} - \tilde{\nu}_{\mathrm{TO}}) \approx 5.25\,\mathrm{THz}$。

### [极化激元](@entry_id:142951)的[色散曲线](@entry_id:197598)：一种反[交叉](@entry_id:147634)现象

为了更清晰地理解极化激元的性质，我们需要求解其显式的[色散关系](@entry_id:140395) $\omega(k)$。通过整理关于 $\omega^2$ 的[隐式方程](@entry_id:177636)，我们可以得到一个关于 $\omega^2$ 的[二次方程](@entry_id:163234) [@problem_id:2848389]：

$$
\epsilon_{\infty} \omega^{4} - (k^{2} c^{2} + \epsilon_{\infty} \omega_{\mathrm{LO}}^{2}) \omega^{2} + k^{2} c^{2} \omega_{\mathrm{TO}}^{2} = 0
$$

这个方程的两个解 $\omega_+^2(k)$ 和 $\omega_-^2(k)$ 分别对应**上[极化激元](@entry_id:142951)支（Upper Polariton Branch, UPB）**和**下极化激元支（Lower Polariton Branch, LPB）**：

$$
\omega_{\pm}^{2}(k) = \frac{(k^{2} c^{2} + \epsilon_{\infty} \omega_{\mathrm{LO}}^{2}) \pm \sqrt{(k^{2} c^{2} + \epsilon_{\infty} \omega_{\mathrm{LO}}^{2})^{2} - 4\epsilon_{\infty} k^{2} c^{2} \omega_{\mathrm{TO}}^{2}}}{2\epsilon_{\infty}}
$$

这两条色散曲线完整地描述了[声子](@entry_id:140728)-[极化激元](@entry_id:142951)的能量-动量关系。通过分析其[渐近行为](@entry_id:160836)，我们可以洞察[极化激元](@entry_id:142951)的混合特性 [@problem_id:3008337]：

- 在长波极限下（$k \to 0$）：
    - 下支表现为[光子](@entry_id:145192)特性，其[色散关系](@entry_id:140395)近似为线性 $\omega \approx (c/\sqrt{\epsilon(0)})k$。这是一个在静态[介电常数](@entry_id:146714) $\epsilon(0)$ 背景中传播的[光子](@entry_id:145192)。
    - 上支的起点为 $\omega = \omega_{\mathrm{LO}}$。

- 在短波极限下（$k \to \infty$）：
    - 下支渐近趋于 $\omega \to \omega_{\mathrm{TO}}$。此时，模式的能量主要集中在[晶格振动](@entry_id:140970)中，表现为[声子](@entry_id:140728)特性。
    - 上支再次表现为[光子](@entry_id:145192)特性，其[色散关系](@entry_id:140395)近似为 $\omega \approx (c/\sqrt{\epsilon_{\infty}})k$。这是一个在高频[介电常数](@entry_id:146714) $\epsilon_{\infty}$ 背景中传播的[光子](@entry_id:145192)。

这种行为的最佳诠释是**反交叉（avoided crossing）**或**反耦合**现象。想象一下，如果没有耦合，我们会有两个独立的模式：一个是在介质中传播的[光子](@entry_id:145192)，其[色散](@entry_id:263750)为 $\omega_{\mathrm{ph}}(k) = ck/\sqrt{\epsilon_{\infty}}$（光线）；另一个是与 $k$ 无关的[横向光学声子](@entry_id:139212)，其[色散](@entry_id:263750)为 $\omega = \omega_{\mathrm{TO}}$（水平线）。当光子能量接近[声子](@entry_id:140728)能量时，即在两条“裸”[色散](@entry_id:263750)线的交点附近，光-[声子](@entry_id:140728)耦合变得至关重要。耦合作用使得两个模式“相互推斥”，能量本应简并的两个[态混合](@entry_id:148060)并分裂成两个新的能量本征态——上、下极化激元态。它们在交点处的能量差，即**反[交叉](@entry_id:147634)[能隙](@entry_id:191975)（anticrossing gap）**，正比于[耦合强度](@entry_id:275517)。

我们可以精确计算在假想的[交叉点](@entry_id:147634) $k_c$（定义为 $\omega_{\mathrm{ph}}(k_c)=\omega_{\mathrm{TO}}$）处的频率分裂 $\Delta\omega = \omega_+(k_c) - \omega_-(k_c)$。通过代数计算可以证明，在此特定波矢下，[能隙](@entry_id:191975)的大小为 [@problem_id:2848389]：

$$
\Delta\omega = \omega_{\mathrm{LO}} - \omega_{\mathrm{TO}}
$$

由于 LO-TO 劈裂的存在，$\omega_{\mathrm{LO}}  \omega_{\mathrm{TO}}$，所以这个[能隙](@entry_id:191975)总是非零的，这清晰地证明了反[交叉](@entry_id:147634)的发生。

利用这个完整的[色散关系](@entry_id:140395)，我们可以解决各类具体问题。例如，若想知道在何种频率下，[极化激元](@entry_id:142951)的相速度 $v_p=\omega/k$ 恰好为光速的一半，即 $v_p=c/2$，这等价于求解条件 $\epsilon(\omega)=4$。对于一个具有特定参数的材料，如 $\epsilon_{\infty}=6.00$，$\epsilon(0)=24.0$，$\omega_{\mathrm{TO}}=9.50 \times 10^{13} \text{ s}^{-1}$ 的晶体，通过求解该方程，可以发现在上极化激元支上存在一个频率 $\omega \approx 3.00 \times 10^{14} \text{ s}^{-1}$ 满足此条件 [@problem_id:2810157] [@problem_id:762809]。

### [极化激元](@entry_id:142951)的量子与耗散特性

虽然经典模型非常成功，但一个更完备的图像需要引入量子力学。在量子化框架中，[声子](@entry_id:140728)-极化激元被视为一种**[准粒子](@entry_id:136584)**，即系统的一个真实的玻色型[元激发](@entry_id:140859)。描述该系统的[哈密顿量](@entry_id:172864)可以写为 [@problem_id:2852788]：

$$
H = \hbar \omega_{c} a^{\dagger} a + \hbar \omega_{\mathrm{TO}} b^{\dagger} b + \hbar g (a^{\dagger} b + a b^{\dagger})
$$

这里，$a^\dagger$ ($a$) 和 $b^\dagger$ ($b$) 分别是[光子](@entry_id:145192)和 TO [声子](@entry_id:140728)的产生（湮灭）算符，$\omega_c$ 是特定[波矢](@entry_id:178620) $k$ 下的[光子](@entry_id:145192)频率， $g$ 是耦合速率。通过[对角化](@entry_id:147016)这个[哈密顿量](@entry_id:172864)，我们可以得到新的本征模式——极化激元的产生（湮灭）算符 $p_{L/U}^\dagger$ ($p_{L/U}$)。这些新算符是[光子](@entry_id:145192)和[声子](@entry_id:140728)算符的线性叠加：

$$
p = u a + v b
$$

其中的复数系数 $u$ 和 $v$ 被称为**霍普菲尔德系数（Hopfield coefficients）**。$|u|^2$ 和 $|v|^2$ （满足 $|u|^2 + |v|^2 = 1$）分别代表了该极化激元模式中的**[光子](@entry_id:145192)成分**和**[声子](@entry_id:140728)成分**。这精确地量化了极化激元的混合特性。

在真实材料中，[能量耗散](@entry_id:147406)是不可避免的。[光子](@entry_id:145192)会因腔体泄漏等原因衰减（速率为 $\kappa$），[声子](@entry_id:140728)会因非谐效应等原因衰减（速率为 $\gamma_{\mathrm{ph}}$）。[极化激元](@entry_id:142951)作为一种混合[准粒子](@entry_id:136584)，其寿命或衰减率 $\Gamma_{\mathrm{pol}}$ 将继承其组分的衰减特性。在[弱耦合](@entry_id:140994)近似下，[极化激元](@entry_id:142951)的总衰减率是其[光子](@entry_id:145192)和[声子](@entry_id:140728)部分衰减率的加权平均 [@problem_id:2852788]：

$$
\Gamma_{\mathrm{pol}} = |u|^2 \kappa + |v|^2 \gamma_{\mathrm{ph}}
$$

这个简单的关系式生动地体现了极化激元的混合本质：它的寿命由其是“更像[光子](@entry_id:145192)”还是“更像[声子](@entry_id:140728)”所决定。

耗散的存在也引出了**强耦合**与**[弱耦合](@entry_id:140994)**范畴的重要区分。只有当[耦合强度](@entry_id:275517) $g$ 足够大，能够克服系统的平均耗散时，能量的反[交叉](@entry_id:147634)分裂才能被清晰地分辨出来。此时，系统处于**强耦合范畴**。相反，如果耗散过强，两个模式的[谱线](@entry_id:193408)会合并成一个宽峰，系统则处于**[弱耦合](@entry_id:140994)范畴**。对于一个与[声子](@entry_id:140728)共振的[光学微腔](@entry_id:262849)系统（$\omega_c = \omega_{\mathrm{TO}}$），进入强耦合范畴的临界条件是 [@problem_id:2852770]：

$$
g  \frac{|\kappa - \gamma_{\mathrm{ph}}|}{4}
$$

这个条件是实现基于极化激元量子器件的基础，它要求我们必须使用高[品质因数](@entry_id:201005)（低 $\kappa$）的微腔和低损耗（低 $\gamma_{\mathrm{ph}}$）的[声子](@entry_id:140728)材料。

### 高级主题：非谐效应与温度依赖性

我们之前的讨论都基于[晶格振动](@entry_id:140970)的简谐近似。然而，真实的晶体[势能](@entry_id:748988)并非完美的抛物线形，存在**非谐效应**。这些高阶项导致了[声子](@entry_id:140728)之间的相互作用，使得[声子](@entry_id:140728)的频率和寿命都与温度相关。

例如，一个 TO [声子](@entry_id:140728)可能通过三[声子](@entry_id:140728)过程衰变，这会导致其频率随温度发生变化。一个常见的模型将温度[重整化](@entry_id:143501)的 TO [声子频率](@entry_id:753407)写为 [@problem_id:2852774]：

$$
\omega_{\mathrm{TO}}^{2}(T) = \omega_{\mathrm{TO0}}^{2} + \lambda [2 n_{\mathrm{B}}(\Omega, T) + 1]
$$

其中，$\omega_{\mathrm{TO0}}$ 是零温下的[谐振频率](@entry_id:265742)，$\lambda$ 是非谐[耦合常数](@entry_id:747980)，$n_{\mathrm{B}}(\Omega, T)$ 是参与相互作用的另一个[声子模式](@entry_id:201212)（频率为 $\Omega$）在温度 $T$ 下的[玻色-爱因斯坦分布](@entry_id:145257)。

由于[极化激元](@entry_id:142951)的频率（特别是 LO 频率）通过 LST 关系与 $\omega_{\mathrm{TO}}$ 紧密相连，$\omega_{\mathrm{TO}}(T)$ 的温度依赖性会直接传递给极化激元。我们可以利用前述的理论框架，计算出极化激元频率随温度的变化率 $\frac{d\omega_{\mathrm{UP/LP}}}{dT}$。这使得我们能够通过测量[光谱](@entry_id:185632)（如拉曼[光谱](@entry_id:185632)或红外反射[光谱](@entry_id:185632)）的温度漂移，来反过来研究材料中复杂的非谐相互作用。例如，对于一个具有典型参数的极性晶体，在室温 300 K 附近，其上[极化激元](@entry_id:142951)频率的变化率可能在 $8.33 \times 10^7 \text{ rad s}^{-1} \text{K}^{-1}$ 的量级 [@problem_id:2852774]。这展示了[声子](@entry_id:140728)-[极化激元](@entry_id:142951)理论在分析真实材料复杂物理现象中的强大威力。