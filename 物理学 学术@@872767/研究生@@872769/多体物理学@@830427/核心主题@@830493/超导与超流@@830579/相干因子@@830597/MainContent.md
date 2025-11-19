## 引言
在凝聚态物理的广阔天地中，[超导现象](@entry_id:142943)以其零电阻和[完全抗磁性](@entry_id:203008)等宏观量子效应而引人入胜。自Bardeen、Cooper和Schrieffer提出其里程碑式的微观理论（BCS理论）以来，我们理解了超导源于电子通过与[晶格振动](@entry_id:140970)（[声子](@entry_id:140728)）交换而形成的[库珀对](@entry_id:143370)凝聚。然而，一个核心的挑战在于如何将这一微观图像与实验室中观察到的纷繁复杂的实验现象联系起来。[超导体](@entry_id:191025)对[电磁场](@entry_id:265881)、声波、磁杂质乃至隧道电流的响应，为何会呈现出与正常金属截然不同的独特行为？

解答这一问题的关键，在于一个深刻而优雅的概念：**相干因子（coherence factors）**。这些因子是BCS理论的直接产物，它们精确地量化了超导态的基本激发——玻戈留波夫[准粒子](@entry_id:136584)——中电子与空穴成分的混合。正是这种混合的相干性，而非仅仅是[能隙](@entry_id:191975)的存在，从根本上决定了[超导体](@entry_id:191025)与外部世界的相互作用方式。本文旨在系统性地阐明相干因子的物理本质及其在现代超导研究中的核心地位，填补从抽象的理论形式到具体实验解读之间的知识鸿沟。

通过本文的学习，读者将深入理解相干因子的来龙去脉及其物理意义。我们将分三步展开：
*   在**“原理与机制”**一章中，我们将从玻戈留波夫-德热纳（BdG）[哈密顿量](@entry_id:172864)出发，严格推导相干因子，并阐明其作为[准粒子](@entry_id:136584)中电子-空穴混合权重的物理解释。
*   接着，在**“应用与跨学科联系”**一章中，我们将展示相干因子如何在各种关键实验——从经典的核[磁共振](@entry_id:143712)、超[声衰减](@entry_id:189896)，到现代的[扫描隧道显微镜](@entry_id:144958)和[中子散射](@entry_id:142835)——中扮演决定性角色，并揭示如何利用它们来探测包括[非常规超导体](@entry_id:141195)在内的复杂材料的[配对对称性](@entry_id:139531)。
*   最后，通过**“动手实践”**部分提供的计算问题，读者将有机会亲手应用相干因子的概念，解决具体物理问题，从而巩固和深化理解。

## 原理与机制

在本章中，我们将深入探讨超导理论的核心概念之一：**相干因子 (coherence factors)**。这些因子源于BCS（Bardeen-Cooper-Schrieffer）理论中对基本激发（即[准粒子](@entry_id:136584)）的描述，它们不仅揭示了超导态下电子与空穴混合的深刻本质，还直接决定了[超导体](@entry_id:191025)对外部探针的响应。理解相干因子是掌握超导态下各种物理现象，从核[磁共振](@entry_id:143712)到隧道谱，乃至非常规超导的奇异性质的关键。

### 玻戈留波夫[准粒子](@entry_id:136584)与相干因子

在BCS平均场理论中，描述[超导体](@entry_id:191025)的[哈密顿量](@entry_id:172864)可以方便地用Nambu表象来书写。对于一个给定的动量 $\mathbf{k}$，我们可以定义一个两分量[旋量](@entry_id:158054)，称为**[Nambu旋量](@entry_id:145326) (Nambu spinor)**：
$$
\Psi_{\mathbf{k}} = \begin{pmatrix} c_{\mathbf{k}\uparrow} \\ c_{-\mathbf{k}\downarrow}^{\dagger} \end{pmatrix}
$$
其中 $c_{\mathbf{k}\uparrow}$ 是一个消灭动量为 $\mathbf{k}$、自旋向上的电子的算符，而 $c_{-\mathbf{k}\downarrow}^{\dagger}$ 是一个产生动量为 $-\mathbf{k}$、自旋向下的电子的算符，它等效于消灭一个动量为 $\mathbf{k}$、自旋向上的空穴。因此，Nambu空间是一个混合了粒子和空穴自由度的**粒子-空穴空间 (particle-hole space)**。

利用这个[旋量](@entry_id:158054)，BCS[平均场哈密顿量](@entry_id:751814)可以被写成一个紧凑的矩阵形式。对于一个具有动量[反演对称性](@entry_id:269948)的自旋单态[超导体](@entry_id:191025)，[哈密顿量](@entry_id:172864)可以表示为 [@problem_id:2973186]：
$$
H_{\mathrm{MF}} = \sum_{\mathbf{k}} \Psi_{\mathbf{k}}^{\dagger} \mathcal{H}_{\mathbf{k}} \Psi_{\mathbf{k}} + \sum_{\mathbf{k}} \xi_{\mathbf{k}}
$$
其中，$\mathcal{H}_{\mathbf{k}}$ 是一个 $2 \times 2$ 的矩阵，称为**玻戈留波夫-德热纳（Bogoliubov-de Gennes, BdG）[哈密顿量](@entry_id:172864)**:
$$
\mathcal{H}_{\mathbf{k}} = \begin{pmatrix} \xi_{\mathbf{k}} & \Delta_{\mathbf{k}} \\ \Delta_{\mathbf{k}}^* & -\xi_{\mathbf{k}} \end{pmatrix}
$$
这里，$\xi_{\mathbf{k}} = \epsilon_{\mathbf{k}} - \mu$ 是正常态电子相对于化学势 $\mu$ 的能量，$\Delta_{\mathbf{k}}$ 是（通常为复数的）超导配对振幅或[能隙](@entry_id:191975)函数。这个矩阵可以优雅地用作用于Nambu空间的泡利矩阵 $\boldsymbol{\tau}$ 来表示：
$$
\mathcal{H}_{\mathbf{k}} = \xi_{\mathbf{k}}\,\tau_z + \mathrm{Re}\,\Delta_{\mathbf{k}}\,\tau_x - \mathrm{Im}\,\Delta_{\mathbf{k}}\,\tau_y
$$
在这个表述中，$\xi_{\mathbf{k}}\,\tau_z$ 项描述了粒子和空穴的能量（分别为 $+\xi_{\mathbf{k}}$ 和 $-\xi_{\mathbf{k}}$），而耦合到 $\tau_x$ 和 $\tau_y$ 的[能隙](@entry_id:191975)项 $\Delta_{\mathbf{k}}$ 则代表了粒子和空穴之间的混合，这是超导的本质特征。

为了找到系统的本征激发，我们需要[对角化](@entry_id:147016) $\mathcal{H}_{\mathbf{k}}$。求解其[本征值问题](@entry_id:142153) $\mathcal{H}_{\mathbf{k}} \mathbf{v} = E \mathbf{v}$，我们得到本征能量为：
$$
E^2 = \xi_{\mathbf{k}}^2 + |\Delta_{\mathbf{k}}|^2
$$
这给出了著名的BCS[准粒子色散](@entry_id:161746)关系，其正能量分支为 $E_{\mathbf{k}} = \sqrt{\xi_{\mathbf{k}}^2 + |\Delta_{\mathbf{k}}|^2}$。这是一个在[费米面](@entry_id:137798)上打开了大小为 $2|\Delta_{\mathbf{k}}|$ 的[能隙](@entry_id:191975)的激发谱。

对应于正能量 $E_{\mathbf{k}}$ 的归一化本征矢量，我们记为 $\begin{pmatrix} u_{\mathbf{k}}^* \\ v_{\mathbf{k}}^* \end{pmatrix}$ （这种形式是为了与标准的玻戈留波夫变换算符形式保持一致）。通过求解本征方程，我们可以得到这两个系数 [@problem_id:2973213]：
$$
|u_{\mathbf{k}}|^2 = \frac{1}{2} \left(1 + \frac{\xi_{\mathbf{k}}}{E_{\mathbf{k}}}\right)
$$
$$
|v_{\mathbf{k}}|^2 = \frac{1}{2} \left(1 - \frac{\xi_{\mathbf{k}}}{E_{\mathbf{k}}}\right)
$$
这两个系数 $u_{\mathbf{k}}$ 和 $v_{\mathbf{k}}$ 被称为**[BCS相干因子](@entry_id:142994) (BCS coherence factors)**。它们满足[归一化条件](@entry_id:156486) $|u_{\mathbf{k}}|^2 + |v_{\mathbf{k}}|^2 = 1$。

相干因子的相位并非任意的，它们之间以及与[能隙](@entry_id:191975)之间存在固定的关系。一个常见的且自洽的**相位约定 (phase convention)** 是选择 $u_{\mathbf{k}}$ 为实数且非负。在这种约定下，通过求解BdG方程，可以确定 $v_{\mathbf{k}}$ 的相位。如果我们将[能隙](@entry_id:191975)写作 $\Delta_{\mathbf{k}} = |\Delta_{\mathbf{k}}| e^{i\phi_{\mathbf{k}}}$，那么 $v_{\mathbf{k}}$ 就具有形式 $v_{\mathbf{k}} = e^{i\phi_{\mathbf{k}}} |v_{\mathbf{k}}|$。这个相位约定将[能隙](@entry_id:191975)的相位信息编码到了 $v_{\mathbf{k}}$ 中。物理可观测量必须独立于这种约定的选择，这意味着它们必须由规范不变的组合（如 $|u_{\mathbf{k}}|^2$, $|v_{\mathbf{k}}|^2$ 和 $u_{\mathbf{k}}v_{\mathbf{k}}^*$）构成 [@problem_id:2973226]。

[对角化](@entry_id:147016) $\mathcal{H}_{\mathbf{k}}$ 的过程等价于引入一套新的[费米子算符](@entry_id:149120)，即**玻戈留波夫[准粒子](@entry_id:136584) (Bogoliubov quasiparticle)** 算符 $\gamma_{\mathbf{k}\sigma}$，它们是电子算符的线性组合：
$$
\gamma_{\mathbf{k}\uparrow} = u_{\mathbf{k}} c_{\mathbf{k}\uparrow} - v_{\mathbf{k}} c_{-\mathbf{k}\downarrow}^{\dagger}
$$
$$
\gamma_{-\mathbf{k}\downarrow}^{\dagger} = v_{\mathbf{k}}^* c_{\mathbf{k}\uparrow} + u_{\mathbf{k}}^* c_{-\mathbf{k}\downarrow}^{\dagger}
$$
在[准粒子](@entry_id:136584)表象中，[哈密顿量](@entry_id:172864)是对角的：$H_{\mathrm{MF}} = \sum_{\mathbf{k}\sigma} E_{\mathbf{k}} \gamma_{\mathbf{k}\sigma}^{\dagger}\gamma_{\mathbf{k}\sigma} + E_0$，其中 $E_0$ 是[基态能量](@entry_id:263704)。[BCS基态](@entry_id:136275) $|BCS\rangle$ 是[准粒子](@entry_id:136584)的真空态，即对于所有的 $\mathbf{k}$ 和 $\sigma$ 都有 $\gamma_{\mathbf{k}\sigma}|BCS\rangle = 0$。

### 相干因子的物理解释

相干因子的核心物理意义在于它们量化了玻戈留波夫[准粒子](@entry_id:136584)中[电子和空穴](@entry_id:274534)成分的混合程度。从 $\gamma_{\mathbf{k}\uparrow}^{\dagger} = u_{\mathbf{k}}^* c_{\mathbf{k}\uparrow}^{\dagger} - v_{\mathbf{k}}^* c_{-\mathbf{k}\downarrow}$ 的形式可以看出，产生一个[准粒子](@entry_id:136584)是产生一个电子和消灭一个电子（即产生一个空穴）的[相干叠加](@entry_id:170209)。

$|u_{\mathbf{k}}|^2$ 给出了[准粒子](@entry_id:136584)处于**电子态 (electron-like)** 的概率，而 $|v_{\mathbf{k}}|^2$ 给出了其处于**空穴态 (hole-like)** 的概率 [@problem_id:2973213]。这一物理解释在考察几个极限情况时变得尤为清晰 [@problem_id:1766589]：

1.  **远离[费米面](@entry_id:137798)（电子一侧）**: 当 $\xi_{\mathbf{k}} \gg |\Delta_{\mathbf{k}}|$ 时，$E_{\mathbf{k}} \approx \xi_{\mathbf{k}}$。此时，$|u_{\mathbf{k}}|^2 \to 1$ 且 $|v_{\mathbf{k}}|^2 \to 0$。[准粒子](@entry_id:136584)几乎就是一个纯粹的电子。

2.  **远离[费米面](@entry_id:137798)（空穴一侧）**: 当 $\xi_{\mathbf{k}} \ll -|\Delta_{\mathbf{k}}|$ 时，$E_{\mathbf{k}} \approx -\xi_{\mathbf{k}}$。此时，$|u_{\mathbf{k}}|^2 \to 0$ 且 $|v_{\mathbf{k}}|^2 \to 1$。[准粒子](@entry_id:136584)几乎就是一个纯粹的空穴。

3.  **在费米面上**: 当 $\xi_{\mathbf{k}} = 0$ 时，$E_{\mathbf{k}} = |\Delta_{\mathbf{k}}|$。此时，$|u_{\mathbf{k}}|^2 = |v_{\mathbf{k}}|^2 = 1/2$。[准粒子](@entry_id:136584)是[电子和空穴](@entry_id:274534)的等量混合体。

值得注意的是，具有相同[准粒子能量](@entry_id:173936) $E > |\Delta|$ 的两个态，一个位于[费米面](@entry_id:137798)之上（粒子型，$\xi_p = \sqrt{E^2 - |\Delta|^2}$），另一个位于[费米面](@entry_id:137798)之下（空穴型，$\xi_h = -\sqrt{E^2 - |\Delta|^2}$），它们的相干因子是互换的，即 $u_p^2 = v_h^2$ 且 $v_p^2 = u_h^2$ [@problem_id:1111832]。

这种粒子-空穴混合的一个深刻后果是，玻戈留波夫[准粒子](@entry_id:136584)通常不具有确定的[电荷](@entry_id:275494)。我们可以计算创建一个[准粒子](@entry_id:136584)对系统总[电荷](@entry_id:275494)数的平均改变量。这个改变量，即**[准粒子](@entry_id:136584)[电荷](@entry_id:275494) (quasiparticle charge)** 的[期望值](@entry_id:153208)，由以下公式给出 [@problem_id:1111928] [@problem_id:2973238]：
$$
\langle q_{\mathbf{k}} \rangle = e \left( |u_{\mathbf{k}}|^2 - |v_{\mathbf{k}}|^2 \right) = e \frac{\xi_{\mathbf{k}}}{E_{\mathbf{k}}} = e \frac{\xi_{\mathbf{k}}}{\sqrt{\xi_{\mathbf{k}}^2 + |\Delta_{\mathbf{k}}|^2}}
$$
这个结果表明，[准粒子](@entry_id:136584)的[有效电荷](@entry_id:748807)连续地从 $+e$（对 $\xi_{\mathbf{k}} \gg |\Delta_{\mathbf{k}}|$）变化到 $-e$（对 $\xi_{\mathbf{k}} \ll -|\Delta_{\mathbf{k}}|$）。在[费米面](@entry_id:137798)上（$\xi_{\mathbf{k}}=0$），[准粒子](@entry_id:136584)是[电中性](@entry_id:157680)的，这体现了完美的[粒子-空穴对称性](@entry_id:142469)。

### 物理过程中的相干因子：矩阵元的修正

相干因子的重要性在计算各种物理过程的跃迁矩阵元时才完全显现出来。当一个外部探针（如[声子](@entry_id:140728)、[光子](@entry_id:145192)或杂质势）与[超导体](@entry_id:191025)中的电子相互作用时，相应的[哈密顿量](@entry_id:172864)算符需要被转换到[准粒子](@entry_id:136584)表象中。这个转换过程会在跃迁[矩阵元](@entry_id:186505)中引入依赖于相干因子的乘法因子。这些因子的大小甚至符号，极大地改变了超导态相对于正常态的响应。

这些相干因子组合的形式取决于相互作用算符在**时间反演**下的对称性。对于自旋单态[超导体](@entry_id:191025)，我们可以区分几种主要情况：

#### 情况 1：[非相干散射](@entry_id:190180)（标量势）
考虑一个[准粒子](@entry_id:136584)从态 $\mathbf{k}$ 散射到态 $\mathbf{k}'$ 的过程，散射源是一个不依赖于自旋的标量势（如非磁性杂质或纵声[声子](@entry_id:140728)）。这类相互作用算符在[时间反演](@entry_id:182076)下是偶的。计算表明，其散射矩阵元 $M_{\mathbf{k}'\mathbf{k}}$ 与正常态矩阵元 $U_{\mathbf{k}'\mathbf{k}}$ 的关系为 [@problem_id:1111836]：
$$
M_{\mathbf{k}'\mathbf{k}} \propto (u_{\mathbf{k}}u_{\mathbf{k}'} - v_{\mathbf{k}}v_{\mathbf{k}'}) U_{\mathbf{k}'\mathbf{k}}
$$
这个组合 $(u_{\mathbf{k}}u_{\mathbf{k}'} - v_{\mathbf{k}}v_{\mathbf{k}'})$ 被称为**第一类散射相干因子**。一个典型的例子是，当一个[准粒子](@entry_id:136584)被散射到[费米面](@entry_id:137798)的另一侧时（$\xi_{\mathbf{k}} = -\xi_{\mathbf{k}'}$），我们有 $u_{\mathbf{k}} = v_{\mathbf{k}'}$ 和 $v_{\mathbf{k}} = u_{\mathbf{k}'}$。在这种情况下，相干因子变为 $(v_{\mathbf{k}'}u_{\mathbf{k}'} - u_{\mathbf{k}'}v_{\mathbf{k}'}) = 0$ [@problem_id:1766616]。这意味着对于标量势，跨越费米面的大角度散射被完全抑制了！这是[BCS理论](@entry_id:144185)的一个显著预测。

#### 情况 2：自旋反转散射
现在考虑一个使电子自旋反转的相互作用（如磁性杂质）。这类算符在[时间反演](@entry_id:182076)下是奇的。相应的散射矩阵元被一个不同的相干因子修正：
$$
M_{\mathbf{k}'\mathbf{k}} \propto (u_{\mathbf{k}}u_{\mathbf{k}'} + v_{\mathbf{k}}v_{\mathbf{k}'}) U_{\mathbf{k}'\mathbf{k}}
$$
这个组合 $(u_{\mathbf{k}}u_{\mathbf{k}'} + v_{\mathbf{k}}v_{\mathbf{k}'})$ 被称为**第二类散射相干因子**。在上述跨越费米面的散射例子中（$\xi_{\mathbf{k}} = -\xi_{\mathbf{k}'}$），这个因子变为 $(v_{\mathbf{k}'}u_{\mathbf{k}'} + u_{\mathbf{k}'}v_{\mathbf{k}'}) = 2u_{\mathbf{k}'}v_{\mathbf{k}'}$，它通常不为零 [@problem_id:1766616]。因此，与标量散射不同，自旋反转散射在超导态下并未被完全抑制。

这种通过相干因子来区分不同类型相互作用的能力是[BCS理论](@entry_id:144185)的一大成功。Anderson[伪自旋](@entry_id:147053)图像为这些散射因子提供了一个优美的几何解释 [@problem_id:1111861]。

#### 情况 3：[准粒子](@entry_id:136584)对的产生或湮灭
另一类重要的过程涉及从[基态](@entry_id:150928)中产生或湮灭一对[准粒子](@entry_id:136584)，例如[声子](@entry_id:140728)或[光子](@entry_id:145192)的吸收。对于一个耦合到电荷密度的标量探针，产生一对[准粒子](@entry_id:136584)（态 $\mathbf{k}$ 和 $\mathbf{k}'$）的[矩阵元](@entry_id:186505)包含第三种类型的相干因子：
$$
M_{\text{pair}} \propto (u_{\mathbf{k}}v_{\mathbf{k}'} + v_{\mathbf{k}}u_{\mathbf{k}'})
$$
这个因子决定了吸收谱的形状。例如，在 $\xi_{\mathbf{k}}=\xi_{\mathbf{k}'}$ 的特殊情况下，该因子变为 $2u_{\mathbf{k}}v_{\mathbf{k}} = \Delta_{\mathbf{k}}/E_{\mathbf{k}}$ [@problem_id:1111827] [@problem_id:1809295]。这个结果在分析[超导体的电磁响应](@entry_id:146891)时至关重要。

### 实验结果与前沿课题

相干因子的存在对实验测量有着戏剧性的影响，它们是验证[BCS理论](@entry_id:144185)的关键证据，并且至今仍是研究新奇[超导体](@entry_id:191025)的有力工具。

#### 赫贝尔-斯里切特峰

[BCS理论](@entry_id:144185)最著名的预言之一是核[磁共振](@entry_id:143712)（NMR）中**核[自旋-晶格弛豫](@entry_id:165918)率**（$1/T_1$）在[临界温度](@entry_id:146683) $T_c$ 以下会出现一个峰，即**赫贝尔-斯里切特峰 (Hebel-Slichter peak)**。这个现象是相干效应的直接体现 [@problem_id:2988273]。

核自旋的弛豫是由电子自旋的涨落引起的，其相互作用算符是电子**[自旋密度](@entry_id:267742)**，它在[时间反演](@entry_id:182076)下是奇的。因此，相关的跃迁概率受到第二类散射相干因子 $(u_{\mathbf{k}}u_{\mathbf{k}'} + v_{\mathbf{k}}v_{\mathbf{k}'})^2$ 的调制。当温度略低于 $T_c$ 时，[能隙](@entry_id:191975) $\Delta$ 刚刚打开。一方面，[准粒子](@entry_id:136584)[态密度](@entry_id:147894) $N_s(E) \propto E/\sqrt{E^2-\Delta^2}$ 在[能隙](@entry_id:191975)边缘 $E \to \Delta$ 处发散。另一方面，对于[热激发](@entry_id:275697)到[能隙](@entry_id:191975)边缘的[准粒子](@entry_id:136584)之间的散射（$E, E' \approx \Delta$），相干因子 $(u_{\mathbf{k}}u_{\mathbf{k}'} + v_{\mathbf{k}}v_{\mathbf{k}'})^2$ 趋于一个有限的常数。这两种效应的结合——发散的态密度和非零的相干因子——导致 $1/T_1$ 的急剧增强，形成了赫贝尔-斯里切特峰。这种相干效应被称为**[建设性干涉](@entry_id:276464) (constructive interference)**。

#### 其他探针中的相干效应

与NMR形成鲜明对比的是，其他一些探针的响应在超导态下反而被抑制了。

*   **超[声衰减](@entry_id:189896)**: 超声波通过与电子的**电荷密度**耦合而在金属中衰减。[电荷密度](@entry_id:144672)算符在[时间反演](@entry_id:182076)下是偶的，因此跃迁概率受到第一类散射相干因子 $(u_{\mathbf{k}}u_{\mathbf{k}'} - v_{\mathbf{k}}v_{\mathbf{k}'})^2$ 的调制。在[能隙](@entry_id:191975)边缘，$\xi_{\mathbf{k}}, \xi_{\mathbf{k}'} \to 0$，导致 $u \approx v \approx 1/\sqrt{2}$，该因子趋于零。这种**[破坏性干涉](@entry_id:170966) (destructive interference)** 恰好抵消了[态密度](@entry_id:147894)的发散，导致超[声衰减](@entry_id:189896)率在 $T_c$ 以下迅速下降 [@problem_id:2988273]。

*   **电磁吸收**: 对于频率为 $\hbar\omega \ge 2\Delta$ 的[电磁波](@entry_id:269629)吸收，该过程从[基态](@entry_id:150928)产生一对[准粒子](@entry_id:136584)。尽管人们可能预期吸收在阈值 $\hbar\omega=2\Delta$ 处因[联合态密度](@entry_id:143002)的发散而急剧开始，但实际上由于相干因子的作用（此处受[规范不变性](@entry_id:137857)约束，效应类似于情况3），吸收谱在阈值处为零，并平滑地增长。

*   **单粒子隧道谱**: 在正常金属-绝缘体-[超导体](@entry_id:191025)（NIS）结中，[微分](@entry_id:158718)[电导](@entry_id:177131) $dI/dV$ 直接正比于[超导体](@entry_id:191025)中的[准粒子](@entry_id:136584)态密度 $\rho_S(eV)$ [@problem_id:2802528]。这里的相干因子并**不会**抵消[态密度](@entry_id:147894)的发散。其原因是，隧道过程涉及单个电子的注入或移出，其[矩阵元](@entry_id:186505)最终只依赖于 $|u_{\mathbf{k}}|^2$ 或 $|v_{\mathbf{k}}|^2$。当对所有贡献求和时，态密度发散的特征得以保留，从而在 $dI/dV$ 谱上产生尖锐的“相干峰”。

一个更深刻的例子是[超导体](@entry_id:191025)的**[静电屏蔽](@entry_id:192260)**。尽管[能隙](@entry_id:191975)的打开抑制了低能单粒子激发，但相干因子的微妙贡献确保了[超导体](@entry_id:191025)的静态[电荷](@entry_id:275494)[磁化率](@entry_id:138219)与正常态金属相同。这意味着[超导体](@entry_id:191025)仍然是完美的屏蔽体，其[托马斯-费米屏蔽长度](@entry_id:141666)在进入超导态时保持不变 [@problem_id:1111844]。

#### [非常规超导体](@entry_id:141195)的探测

相干因子的概念在研究具有非传统[配对对称性](@entry_id:139531)的**[非常规超导体](@entry_id:141195) (unconventional superconductors)** 时变得更加强大。在这些材料中，[能隙](@entry_id:191975)函数 $\Delta_{\mathbf{k}}$ 可以在[费米面](@entry_id:137798)上改变符号，甚至出现节点（$\Delta_{\mathbf{k}}=0$ 的点或线）。

*   **探测[能隙](@entry_id:191975)符号**: [准粒子](@entry_id:136584)[相干散射](@entry_id:267724)（QPI）是一种利用扫描隧道显微镜（STM）探测[超导体](@entry_id:191025)电子结构的技术。非磁性杂质（标量势）引起的散射强度正比于第一类散射相干因子 $(u_{\mathbf{k}}u_{\mathbf{k}'} - v_{\mathbf{k}}v_{\mathbf{k}'})^2$。由于 $v_{\mathbf{k}}$ 的符号追踪 $\Delta_{\mathbf{k}}$ 的符号，这个因子对 $\Delta_{\mathbf{k}}$ 和 $\Delta_{\mathbf{k}'}$ 的相对符号非常敏感。具体来说，当 $\Delta_{\mathbf{k}}$ 和 $\Delta_{\mathbf{k}'}$ 同号时，散射被抑制；而当它们异号时，散射被增强 [@problem_id:2973161]。这为实验上区分 $s_{++}$（符号不变）和 $s_{\pm}$（符号改变）等配对态提供了决定性的证据。同样，赫贝尔-斯里切特峰的缺失也被认为是[能隙](@entry_id:191975)变号的一个标志，因为费米面上的符号变化导致了相干因子的[破坏性干涉](@entry_id:170966)，从而抑制了峰的出现 [@problem_id:2973160]。

*   **[能隙节点](@entry_id:144519)**: 在具有[能隙节点](@entry_id:144519)的[超导体](@entry_id:191025)（如 $d$-波[超导体](@entry_id:191025)）中，$\Delta_{\mathbf{k}}=0$ 的点是拓扑缺陷。当动量 $\mathbf{k}$ 穿过一个节点时，虽然 $|u_{\mathbf{k}}|$ 和 $|v_{\mathbf{k}}|$ 是连续变化的，但 $v_{\mathbf{k}}$ 的相位会经历一个 $\pi$ 的跳变，这反映了[BdG哈密顿量](@entry_id:145387)拓扑性质的改变 [@problem_id:2973193]。在节点处，如果 $\xi_{\mathbf{k}} \neq 0$，[准粒子](@entry_id:136584)恢复为纯粹的电子或空穴；如果 $\xi_{\mathbf{k}}=0$（即节点恰好在费米面上），[准粒子](@entry_id:136584)则保持电子-空穴的混合特性。

#### 自旋自由度的推广

到目前为止，我们的讨论主要局限于简单的自旋单态、无[自旋轨道](@entry_id:274032)耦合（SOC）的情况，此时 $4\times4$ 的[BdG哈密顿量](@entry_id:145387)可以分解为两个独立的 $2\times2$ 块。然而，在更一般的情况下，这种简化是不可能的 [@problem_id:2973155]。

*   **[自旋轨道](@entry_id:274032)耦合**: 在存在SOC的[非中心对称](@entry_id:157488)[超导体](@entry_id:191025)中，即使是自旋单态配对，电子的自旋也不再是[好量子数](@entry_id:262514)。此时，配对发生在具有相反螺旋度的态之间，导致完整的 $4\times4$ BdG矩阵无法被一个全局的自旋[基矢](@entry_id:199546)分解，[准粒子](@entry_id:136584)是四个Nambu分量的复杂混合。
*   **[自旋三重态配对](@entry_id:144256)**: 在自旋[三重态](@entry_id:156705)[超导体](@entry_id:191025)中，情况更为复杂。只有在特殊情况下，例如当三重态的d矢量（$\mathbf{d}_{\mathbf{k}}$）与SOC矢量（$\mathbf{g}_{\mathbf{k}}$）锁定平行时，体系才能在螺旋度[基矢](@entry_id:199546)下分解为两个 $2\times2$ 块。在一般情况下，完整的 $4\times4$ 结构是必需的。

在这些复杂的情形下，标量的相干因子 $u_{\mathbf{k}}$ 和 $v_{\mathbf{k}}$ 需要被推广为矩阵或矢量形式，但它们的基本作用——编码[准粒子](@entry_id:136584)中不同自由度的混合，并决定物理过程的选择定则——依然保持不变。