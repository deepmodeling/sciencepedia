## 引言
[玻色-爱因斯坦凝聚体](@entry_id:145990)（Bose-Einstein Condensate, BEC）作为一种宏观量子物态，其丰富的动力学行为——从[集体振荡](@entry_id:158973)到拓扑缺陷的形成——对理论物理提出了独特的挑战。精确描述这一包含大量相互作用粒子的[多体量子系统](@entry_id:161678)演化是理解其奇特性质的关键，但完整的[量子多体问题](@entry_id:146763)往往难以求解。时变[格罗斯-皮塔耶夫斯基方程](@entry_id:137849)（Time-dependent Gross-Pitaevskii Equation, TDGPE）正是在这一背景下应运而生，它通过一种巧妙的平均场近似，将复杂问题转化为一个更易于处理的[非线性波](@entry_id:273091)函数方程，成为了现代[冷原子物理学](@entry_id:136963)的理论基石，并为连接理论与实验提供了有力工具。

本文旨在系统性地阐述 TDGPE 理论及其广泛应用，为读者搭建起从基础原理到前沿应用的知识桥梁。在接下来的内容中，读者将首先在 **“原理与机制”** 一章中深入学习 TDGPE 的推导、其等效的[量子流体动力学](@entry_id:144356)表述，以及它如何解释超流性和[元激发](@entry_id:140859)等基本概念。随后，在 **“应用与[交叉](@entry_id:147634)学科联系”** 一章中，我们将通过孤子、[量子涡旋](@entry_id:147375)和[量子湍流](@entry_id:160221)等具体实例，展示 TDGPE 在解释实验现象和连接凝聚态物理、量子光学及宇宙学等领域的强大能力。最后，**“动手实践”** 部分将提供具体的计算练习，帮助读者将理论知识转化为实践技能。让我们从深入理解该方程的基本原理开始，踏上探索宏观[量子动力学](@entry_id:138183)世界的旅程。

## 原理与机制

在对玻色-爱因斯坦凝聚体（Bose-Einstein Condensate, BEC）的动力学行为进行理论描述时，**时变[格罗斯-皮塔耶夫斯基方程](@entry_id:137849)（Time-dependent Gross-Pitaevskii Equation, TDGPE）** 占据了核心地位。此方程在平均场近似的框架内，将[多体量子系统](@entry_id:161678)的复杂性简化为一个对[宏观波函数](@entry_id:143853) $\Psi(\mathbf{r}, t)$ 的[非线性薛定谔方程](@entry_id:159056)。本章将深入探讨 TDGPE 的基本原理、其等效的[流体动力学](@entry_id:136788)表述，以及它所揭示的凝聚体[集体激发](@entry_id:145026)和超流等关键物理机制。

### [格罗斯-皮塔耶夫斯基方程](@entry_id:137849)：一个[经典场论](@entry_id:149475)

从根本上说，TDGPE 可以被视为描述凝聚体序参量场 $\Psi(\mathbf{r}, t)$ 的经典[运动方程](@entry_id:170720)。这一观点源于系统的作用量 $S[\Psi^*, \Psi]$。对于一个由质量为 $m$ 的[玻色子](@entry_id:138266)组成的稀薄、弱[相互作用气体](@entry_id:144962)，其拉格朗日密度 $\mathcal{L}$ 可以写为：

$$
\mathcal{L} = i\hbar \Psi^* \frac{\partial \Psi}{\partial t} - \frac{\hbar^2}{2m} |\nabla \Psi|^2 - V_{ext}(\mathbf{r})|\Psi|^2 - \frac{g}{2} |\Psi|^4
$$

其中，第一项是与[时间演化](@entry_id:153943)相关的动力学项，第二项是动能密度，第三项 $V_{ext}(\mathbf{r})$ 是外[势场](@entry_id:143025)（例如[磁光阱](@entry_id:160929)）的势能，最后一项描述了原子间的[接触相互作用](@entry_id:150822)。参数 $g$ 是[相互作用强度](@entry_id:192243)常数。根据最小作用量原理 $\delta S / \delta \Psi^* = 0$，我们可以直接导出 TDGPE [@problem_id:1181606]：

$$
i\hbar \frac{\partial \Psi(\mathbf{r},t)}{\partial t} = \left( -\frac{\hbar^2}{2m} \nabla^2 + V_{ext}(\mathbf{r}) + g|\Psi(\mathbf{r},t)|^2 \right) \Psi(\mathbf{r},t)
$$

在这个方程中，[宏观波函数](@entry_id:143853) $\Psi(\mathbf{r}, t)$ 被归一化到总粒子数 $N = \int |\Psi|^2 d^3r$，因此 $|\Psi|^2 = n(\mathbf{r},t)$ 代表了凝聚体的原子数密度。方程右边的三项分别代表了动能、外场势能和[平均场相互作用](@entry_id:200557)能。

[相互作用参数](@entry_id:750714) $g$ 封装了原子间相互作用的微观细节，它与 s-波[散射长度](@entry_id:142881) $a_s$ 密切相关，对于三维系统，$g = 4\pi\hbar^2 a_s / m$。$g > 0$ 对应排斥相互作用，而 $g  0$ 对应吸引相互作用。通过量纲分析可以验证，为使 $g|\Psi|^2$ 这一项具有能量量纲，$g$ 的量纲必须是能量乘以体积，即 $[M][L]^5[T]^{-2}$ [@problem_id:1782409]。

对于不随时间演化的**定态（stationary state）**，其解具有形式 $\Psi(\mathbf{r}, t) = \psi(\mathbf{r}) e^{-i\mu t/\hbar}$，其中 $\mu$ 被称为**化学势**。将此形式代入 TDGPE，可得到不含时间的[格罗斯-皮塔耶夫斯基方程](@entry_id:137849)（GPE）：

$$
\mu \psi(\mathbf{r}) = \left( -\frac{\hbar^2}{2m} \nabla^2 + V_{ext}(\mathbf{r}) + g|\psi(\mathbf{r})|^2 \right) \psi(\mathbf{r})
$$

这是一个[非线性](@entry_id:637147)[本征值问题](@entry_id:142153)，其[本征值](@entry_id:154894)即为化学势 $\mu$。对于一个没有外[势阱](@entry_id:151413)的均匀凝聚体 ($V_{ext} = 0$)，其[基态](@entry_id:150928)解是空间均匀的，$\psi(\mathbf{r}) = \sqrt{n_0}$，其中 $n_0$ 是常数密度。在这种情况下，动能项为零，GPE 简化为一个简单的代数关系：$\mu = g n_0$ [@problem_id:1181606]。这个关系表明，在均匀体系中，化学势正比于[相互作用能](@entry_id:264333)密度。

### [流体动力学](@entry_id:136788)图像：量子流体

TDGPE 的一个极其深刻且有用的解释来自于其[流体动力学](@entry_id:136788)形式。通过引入 **Madelung 变换**，我们将复数场 $\Psi$ 分解为其振幅和相位：

$$
\Psi(\mathbf{r}, t) = \sqrt{n(\mathbf{r}, t)} e^{i S(\mathbf{r}, t)}
$$

这里 $n(\mathbf{r}, t)$ 是前面提到的原子密度，而 $S(\mathbf{r}, t)$ 是[波函数](@entry_id:147440)的相位。基于相位的梯度，我们可以定义一个速度场，即**超流速度（superfluid velocity）**：

$$
\mathbf{v}_s(\mathbf{r}, t) = \frac{\hbar}{m} \nabla S(\mathbf{r}, t)
$$

将 Madelung 变换代入 TDGPE 并分离实部和虚部，可以得到两组分别描述密度和速度演化的方程，这组方程在形式上与经典[流体力学](@entry_id:136788)方程惊人地相似。虚部给出了粒子数守恒的**[连续性方程](@entry_id:195013)**：

$$
\frac{\partial n}{\partial t} + \nabla \cdot (n \mathbf{v}_s) = 0
$$

而实部则给出了一个类似于**[欧拉方程](@entry_id:177914)**的[动力学方程](@entry_id:751029)，描述了流体元如何在外力作用下加速：

$$
m\left(\frac{\partial \mathbf{v}_s}{\partial t} + (\mathbf{v}_s \cdot \nabla)\mathbf{v}_s\right) = -\nabla(V_{ext} + gn + V_q)
$$

这个方程右边的力来自于三部分：外势 $V_{ext}$ 的梯度、[平均场相互作用](@entry_id:200557)（可视为一种压力，其势为 $gn$）的梯度，以及一个纯粹的量子效应——**[量子势](@entry_id:193380)（quantum potential）** $V_q$ 的梯度。这个[量子势](@entry_id:193380)的表达式为 [@problem_id:649535]：

$$
V_q = -\frac{\hbar^2}{2m}\frac{\nabla^2\sqrt{n}}{\sqrt{n}}
$$

[量子势](@entry_id:193380)源于[波函数](@entry_id:147440)动能项中与振幅（密度）空间变化相关的部分。它体现了[波函数](@entry_id:147440)的刚性：系统倾向于抵抗密度的剧烈变化，因为这会带来巨大的动能代价。这种抵抗表现为一种内部压力，即**量子压力（quantum pressure）**。量子压力在密度变化剧烈的区域（例如凝聚体边界或涡旋核心处）变得至关重要。

量子压力的概念可以被进一步推广为一个**量子应力张量（quantum stress tensor）** $\mathbf{\Pi}_Q$。作用在流[体元](@entry_id:267802)上的量子力密度可以表示为该[张量的散度](@entry_id:191736) $\mathbf{f}_Q = \nabla \cdot \mathbf{\Pi}_Q$。对于静态系统，其分量形式为 [@problem_id:1276581]：

$$
\Pi_{ij}(\mathbf{r}) = \frac{\hbar^2}{2m} \left[ \left( \partial_i \sqrt{n} \right) \left( \partial_j \sqrt{n} \right) - \sqrt{n} \left( \partial_i \partial_j \sqrt{n} \right) \right]
$$

例如，在一个沿 $z$ 轴变化的密度界面（如 $n(z) \propto 1 + \tanh(z/L)$），即使系统是静态的，也会存在一个非零的对角分量 $\Pi_{zz}$，它描述了沿 $z$ 方向为维持该密度剖面所需的内部应力 [@problem_id:1276581]。

动能（量子压力）和相互作用能之间的竞争定义了一个[特征长度尺度](@entry_id:266383)，称为**愈合长度（healing length）** $\xi$：

$$
\xi = \frac{\hbar}{\sqrt{2mgn_0}}
$$

愈合长度描述了当凝聚体受到局部扰动（例如一个硬边界或一个缺陷）时，其密度恢复到体密度 $n_0$ 所需的距离。在这个尺度上，动能和相互作用能处于同一量级。

### [元激发](@entry_id:140859)与[超流性](@entry_id:159036)

凝聚体的低能动力学行为通常由其[基态](@entry_id:150928)附近的小振幅[集体振荡](@entry_id:158973)模式主导，这些模式被称为**[元激发](@entry_id:140859)（elementary excitations）**或**[准粒子](@entry_id:136584)（quasiparticles）**。通过线性化 TDGPE，我们可以求解这些[元激发](@entry_id:140859)的能量-动量关系，即**[色散关系](@entry_id:140395)（dispersion relation）**。

考虑一个均匀凝聚体[基态](@entry_id:150928) $\Psi_0 = \sqrt{n_0}e^{-i\mu t/\hbar}$，并引入一个小的微扰 $\delta\psi$。我们将总[波函数](@entry_id:147440)写为 $\Psi = e^{-i\mu t/\hbar}[\sqrt{n_0} + \delta\psi(\mathbf{r}, t)]$。为了求解微扰的动力学，通常将其分解为具有确定频率 $\omega$ 的正频和负频分量：

$$
\delta\psi(\mathbf{r}, t) = u(\mathbf{r}) e^{-i\omega t} + v^*(\mathbf{r}) e^{i\omega t}
$$

将此形式代入 TDGPE 并只保留 $\delta\psi$ 的线性项，可以得到一组关于[准粒子](@entry_id:136584)振幅 $u(\mathbf{r})$ 和 $v(\mathbf{r})$ 的耦合方程，即**博戈留波夫-德热纳方程（Bogoliubov-de Gennes equations, BdG）** [@problem_id:1184670]。

对于均匀系统，BdG 方程的解是平面波，$u, v \propto e^{i\mathbf{k}\cdot\mathbf{r}}$。求解这些方程可以得到著名的**博戈留波夫色散关系**，它给出了动量为 $\hbar\mathbf{k}$ 的[元激发](@entry_id:140859)的能量 $E_k = \hbar\omega_k$ [@problem_id:1184670]：

$$
E_k = \sqrt{\frac{\hbar^2 k^2}{2m} \left( \frac{\hbar^2 k^2}{2m} + 2 g n_0 \right)} = \sqrt{\epsilon_k (\epsilon_k + 2\mu)}
$$

其中 $\epsilon_k = \hbar^2 k^2 / (2m)$ 是[自由粒子](@entry_id:148748)的动能。这个色散关系完美地揭示了相互作用如何改变系统的激发谱：
*   **长波极限（$k \to 0$）**：当动量很小时，$\epsilon_k$ 项远小于 $2gn_0$ 项。色散关系近似为线性 $E_k \approx \hbar k \sqrt{gn_0/m}$。这对应于声波（**[声子](@entry_id:140728)**）的传播，其速度为**声速（speed of sound）** $c_s = \sqrt{gn_0/m}$ [@problem_id:229718]。
*   **短波极限（$k \to \infty$）**：当动量很大时，$\epsilon_k$ 占主导地位，色散关系趋近于自由粒子的形式 $E_k \approx \epsilon_k + gn_0$，即一个具有化学势能量偏移的抛物线。

[元激发](@entry_id:140859)的[色散](@entry_id:263750)谱是理解**[超流性](@entry_id:159036)（superfluidity）** 的关键。根据**[朗道判据](@entry_id:161354)（Landau's criterion）**，一个以速度 $v_s$ 流动的超流体，只有当它能够以守恒能量和动量的方式产生[元激发](@entry_id:140859)时，才会受到阻力。这个过程在能量上变得有利的最小速度，即**临界速度（critical velocity）** $v_c$，由[色散关系](@entry_id:140395)的最小值决定：

$$
v_c = \min_{k0} \frac{E_k}{\hbar k}
$$

将博戈留波夫[色散关系](@entry_id:140395)代入此判据，我们发现该比值的最小值出现在 $k \to 0$ 的极限处，其结果恰好是系统的声速 [@problem_id:1276666]：

$$
v_c = \sqrt{\frac{g n_0}{m}} = c_s
$$

这意味着，只要凝聚体的流动速度低于声速，它就无法通过产生单个[元激发](@entry_id:140859)来耗散能量，从而能够无摩擦地流动。当流速超过声速（即[超音速流](@entry_id:262511)动，$v_s  c_s$）时，[朗道判据](@entry_id:161354) $v_s  E_k / (\hbar k)$ 会在一个特定的波矢范围 $[k_{min}, k_{max}]$ 内被满足。在这个范围内产生激发现已在能量上变得可行，这会导致超流的衰减和阻力的出现 [@problem_id:1276647]。

### 囚禁凝聚体中的[集体动力学](@entry_id:204455)

在实际实验中，BEC 通常被囚禁在[谐振子势](@entry_id:750179)阱 $V_{ext}(\mathbf{r}) = \frac{1}{2} m (\omega_x^2 x^2 + \omega_y^2 y^2 + \omega_z^2 z^2)$ 中。TDGPE 同样能够描述囚禁凝聚体的各种[集体振荡](@entry_id:158973)模式。

一个特别引人注目的结果是**[科恩定理](@entry_id:143958)（Kohn's theorem）**。该定理指出，在谐振子势阱中，凝聚体[重心](@entry_id:273519)的运动完全不受粒子间相互作用的影响。通过计算重心[期望值](@entry_id:153208) $\langle z \rangle(t) = \frac{1}{N} \int z |\Psi|^2 d^3r$ 的时间演化，可以利用 TDGPE 导出一个简单的谐[振子运动方程](@entry_id:195641) [@problem_id:649532]：

$$
\frac{d^2}{dt^2}\langle z \rangle = -\omega_z^2 \langle z \rangle
$$

这表明，凝聚体重心的**[偶极振荡](@entry_id:261900)（dipole oscillation）** 频率严格等于阱的频率 $\omega_z$，无论[相互作用强度](@entry_id:192243) $g$ 是多少。这个结果的深层含义是，在谐振子势中，[质心运动](@entry_id:178374)与系统的内部自由度（如形状、密度[分布](@entry_id:182848)等）是解耦的。

然而，对于其他不改变[重心](@entry_id:273519)的集体模式，其频率则强烈依赖于相互作用。一个典型的例子是**单极（呼吸）模式（monopole breathing mode）**，即凝聚体尺寸的周期性扩张和收缩。在相互作用能远大于动能的**托马斯-费米（Thomas-Fermi, TF）** 近似下，[三维各向同性谐振子](@entry_id:195671)阱中的[呼吸模式](@entry_id:158261)频率为 $\omega_{br,TF} = \sqrt{5}\omega$。

当考虑动能（即量子压力）的贡献时，这个频率会发生修正。我们可以将量子压力视为一种微扰。利用一个[变分方法](@entry_id:163656)，[呼吸模式](@entry_id:158261)频率的平方可以表示为[基态](@entry_id:150928)[势能](@entry_id:748988) $E_{pot}$、动能 $E_{kin}$ 和[均方根半径](@entry_id:146552) $\langle r^2 \rangle$ 的函数。通过将动能视为一个小量，用[无量纲参数](@entry_id:169335) $\zeta = E_{kin} / (N\mu)$ 来量化其影响，可以计算出对 TF 结果的[一阶修正](@entry_id:155896) [@problem_id:1276619]。对于三维[谐振子](@entry_id:155622)阱中的情况，修正后的频率平方为：

$$
\omega_{br}^2 = \left(5 - \frac{7}{3}\zeta\right)\omega^2
$$

这个结果清晰地展示了量子压力如何软化（降低）[呼吸模式](@entry_id:158261)的频率，为我们提供了一个定量理解动[能效](@entry_id:272127)应在[集体动力学](@entry_id:204455)中作用的实例。

综上所述，时变[格罗斯-皮塔耶夫斯基方程](@entry_id:137849)不仅为描述[玻色-爱因斯坦凝聚体](@entry_id:145990)提供了一个坚实的理论框架，还通过其[流体动力学](@entry_id:136788)形式和对[元激发](@entry_id:140859)的预测，深刻地揭示了[量子流体](@entry_id:140332)的丰富物理内涵，从无摩擦的超流到复杂的集体振荡模式。