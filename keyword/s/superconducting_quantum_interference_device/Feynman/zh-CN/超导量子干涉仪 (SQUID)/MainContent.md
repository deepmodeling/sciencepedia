## 引言
[超导量子干涉仪](@keyword=superconducting_quantum_interference_devices|lang=zh-CN|style=Feynman)（SQUID）是磁测量领域无可争议的王者，能够探测到比地球[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)弱数千倍的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。这种无与伦比的灵敏度使其成为科学和医学领域不可或缺的工具，但其工作原理植根于常常与直觉相悖的量子力学原理。本文旨在弥合[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)的惊人能力与其背后的物理学之间的鸿沟。我们将探讨该设备如何利用[宏观量子现象](@keyword=macroscopic_quantum_phenomena|lang=zh-CN|style=Feynman)来实现其非凡的精度。读者将首先踏上“原理与机制”的旅程，揭示[磁通量子化](@keyword=flux_quantization|lang=zh-CN|style=Feynman)和约瑟夫森结如何产生[量子干涉](@keyword=quantum_interference|lang=zh-CN|style=Feynman)效应，将微小的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)变化转化为可测量的电压。随后，“应用与跨学科联系”部分将展示[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)的深远影响，从描绘人脑微弱的磁信号到检验凝聚态物理的前沿。我们的探索始于赋予[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)非凡力量的基本量子效应。

## 原理与机制

要理解[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)这一奇迹，我们不能仅仅看它的电路图。我们必须踏上一段进入奇特而美丽的量子力学世界的旅程，在这个世界里，[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中的量子现象会扩展到我们可以观察和操控的尺度。我们的旅程并非从[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)开始，而是从一个更简单的东西开始：一个普通、无断裂的超导线环。

### [超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的灵魂：相干量子波

想象一下，你将一个金属环冷却到其临界温度以下。一个奇迹般的转变发生了。通常像无组织人群一样拥挤和散射的电子，会配对形成我们称之为**库珀对**的粒子。但更重要的是，所有这些[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)开始以完美的步伐同步运动。它们不再是独立的个体，而是融合成一个单一、巨大、相干的实体，由一个**宏观[量子波函数](@keyword=quantum_wavefunction|lang=zh-CN|style=Feynman)**来描述。可以把它想象成一条环绕[圆环](@keyword=annulus|lang=zh-CN|style=Feynman)流动的无声的概率之河，其中的每一滴水都与所有其他水滴完美和谐地运动。

这个波，像任何行为良好的波一样，具有相位。这里的关键规则是：为了使[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在物理上是合理的，它必须是**单值的**。这意味着，如果你沿着环路绕行一整圈，波的相位必须回到其起始点（或者是2π的整数倍，这是等效的）。它必须与自身完美地衔接，不能有任何扭结或跳跃。

现在，事实证明[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)也会影响这个波的相位。如果一个磁通量 $\Phi$ 穿过环的孔，它会在[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)传播时扭曲其相位。为了让波在绕行一整圈后能与自身平滑地衔接，这种[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)引起的扭曲必须被精确地补偿，这导出了一个惊人的结论：环内捕获的总[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)不能是任意值，而是量子化的。[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)只能以一个[基本常数](@keyword=fundamental_constants|lang=zh-CN|style=Feynman)——**[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)** $\Phi_0$ 的离散整数倍存在 [@problem_id:2824081]。

$$ \Phi = n \Phi_0, \quad \text{其中 } n \text{ 为整数} $$

这个[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)由自然界两个最基本的常数定义：普朗克常数 $h$ 和库珀对的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $2e$。

$$ \Phi_0 = \frac{h}{2e} \approx 2.067834 \times 10^{-15} \text{ 韦伯} $$

这是一个极其微小的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)，但它的存在是量子力学在宏观尺度上展现其力量的直接结果。这个磁通量子 $\Phi_0$，是[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)用来测量磁性世界所使用的“标尺”上的基本“刻度”。

### 引入一个裂缝：[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)

如果我们完美的环不再完美会发生什么？让我们切开环并插入一个“弱连接”。这不仅仅是任何一种断裂；它是一种特殊类型，称为**[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)**。你可以把它想象成夹在环的两个超导端之间的一个极薄的绝缘体切片。它是一个势垒，但对于幽灵般的[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)来说并非不可逾越。它们可以[量子隧穿](@keyword=quantum_mechanical_tunneling|lang=zh-CN|style=Feynman)过去。

Brian Josephson 发现这个弱连接有两个显著的特性。首先，超导电流可以无电压地流过它，但存在一个极限——**[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)** $I_0$。其次，结两侧的量子波相位可以不同，而超导电流的大小取决于这个[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman) $\varphi$，遵循关系式 $I = I_0 \sin(\varphi)$。这个结就像一个门，根据量子[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman)来控制超导电流的流动。

### 环路中的[量子干涉](@keyword=quantum_interference|lang=zh-CN|style=Feynman)：[直流SQUID](@keyword=dc_squid|lang=zh-CN|style=Feynman)

现在，我们准备好构建我们的设备了。我们不是插入一个弱连接，而是在我们的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)中插入*两个*约瑟夫森结，为超导电流的流动创造两条平行路径。这就构成了**直流 (DC) SQUID** [@problem_id:1806317]。你可能听说过著名的[双缝实验](@keyword=double_slit_experiment|lang=zh-CN|style=Feynman)，其中光波穿过两个狭缝并发生干涉。[直流SQUID](@keyword=dc_squid|lang=zh-CN|style=Feynman)就是那个实验的电路等效版本，只不过对象是库珀对的波。

一个[偏置电流](@keyword=bias_current|lang=zh-CN|style=Feynman) $I_b$ 到达SQUID后分流，流经两个结。就像在简单的环中一样，任何穿过环路的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi$ 都会在两条路径之间产生相位差。一条路径的相位被提前，另一条则被延迟。这个[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)精确地与外加磁通量成正比，即 $\Phi / \Phi_0$。

[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)在出现电压之前所能承载的总超导电流——即其总[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman) $I_c(\Phi)$——是流经两个结的电流之和。由于[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)引起的相移，这两股电流会发生干涉。

-   **相长干涉：** 当[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)是[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)的整数倍时 ($\Phi = n\Phi_0$)，两股波电流到达另一侧时相位完全相同。它们相加，SQUID变得“强壮”，能够承载 $2I_0$ 的最大超导电流。

-   **[相消干涉](@keyword=destructive_interference|lang=zh-CN|style=Feynman)：** 奇妙之处就在于此。当磁通量恰好是半整数倍时 ($\Phi = (n + \frac{1}{2})\Phi_0$)，两条路径的相位正好[相差](@keyword=phase_contrast|lang=zh-CN|style=Feynman) $\pi$ [弧度](@keyword=radians|lang=zh-CN|style=Feynman) ($180^\circ$)。两股电流大小相等但方向相反。它们完全相互抵消！该器件能承载的总超导电流为零 [@problem_id:1214601]。

这种干涉模式意味着SQUID的总[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)随磁通量的变化而[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。暂时忽略环路自身的[电感](@keyword=inductance|lang=zh-CN|style=Feynman)，这种关系是一个优美简洁的余弦函数 [@problem_id:3018086]：

$$ I_c(\Phi) = 2I_0 \left|\cos\left(\frac{\pi\Phi}{\Phi_0}\right)\right| $$

SQUID充当了磁通-电流转换器。每当[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)变化仅为单个[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)的一半时，其承载电流的能力就会从最大值急剧变化到最小值。

### 看见无形：从干涉到可测量的电压

我们现在有了一个[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)对磁通量极其敏感的设备。但我们如何读出它的信号呢？我们无法轻易地直接测量[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)。相反，我们使用一个巧妙的技巧。我们让一个恒定的**偏置电流** $I_b$ 流过SQUID，将其值设定为略大于[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)的最小[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)（在我们的理想情况下为零），但小于其最大[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman) ($2I_0$)。

现在，当我们缓慢改变穿过环路的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi$ 时，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman) $I_c(\Phi)$ 会发生[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。
-   当 $I_c(\Phi)$ 很高时（接近[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)整数倍 $n\Phi_0$），它大于我们的[偏置电流](@keyword=bias_current|lang=zh-CN|style=Feynman) $I_b$。SQUID会愉快地以超导电流的形式承载所有电流，其两端的电压为零。
-   当 $I_c(\Phi)$ 降得很低时（接近半整数倍 $(n+\frac{1}{2})\Phi_0$），它再也无法支撑全部的[偏置电流](@keyword=bias_current|lang=zh-CN|style=Feynman) $I_b$。“多余”的电流别无选择，只能流过结的固有电阻，根据[欧姆定律](@keyword=ohm_s_law|lang=zh-CN|style=Feynman)，这会产生一个电压 $V$。

结果是，测得的[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)两端电压 $V(\Phi)$ 随着磁通量的变化而周期性[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。电压的每一次完整[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)都精确对应于一个[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman) $\Phi_0$ 的通量变化 [@problem_id:2498087]。这条周期性的电压-磁通曲线是[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)的标志，可以在实验室中直接测量。实际上，通过测量在外部线圈中产生一次完整电压[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)所需的电流，我们可以进行一个精美的实验来确定 $\Phi_0$ 本身的值 [@problem_id:1775616]。

### 驯服量子：从奇特的传感器到强大的仪器

我们理想化的图景揭示了SQUID的核心。但要使其成为一种实用的仪器，我们必须面对一些现实世界的复杂性，并运用一些非凡的创造力。

#### 自我校正问题：屏蔽与[电感](@keyword=inductance|lang=zh-CN|style=Feynman)

我们简单的模型假设环路本身没有[电感](@keyword=inductance|lang=zh-CN|style=Feynman)。实际上，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)中为屏蔽磁通而流动的环流自身也会产生磁通量。这种效应由一个无量纲参数 $\beta_L = 2LI_c/\Phi_0$ 来量化，其中 $L$ 是环路[电感](@keyword=inductance|lang=zh-CN|style=Feynman) [@problem_id:2862988]。如果 $\beta_L$ 很小，我们简单的模型仍然成立。但随着它变大，屏蔽电流开始“对抗”外部磁通，试图保持环路内部总磁通量恒定。这会扭曲优美的类余弦响应曲线，减小斜率 $|\partial V / \partial \Phi|$（也就是我们的信号！），并且当 $\beta_L \gtrsim 1$ 时，甚至可能导致使传感器变得不可预测的迟滞、多值行为。设计一个好的[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)需要保持这个参数很小。

#### 重复标尺问题：[磁通锁定环](@keyword=flux_locked_loop|lang=zh-CN|style=Feynman)

$V(\Phi)$ 曲线的周期性是一把双刃剑。它对选定偏置点（曲线上最陡峭的部分）周围磁通的微小变化提供了惊人的灵敏度。但它无法让我们测量一个大的、未知的磁通量。读数为0.1伏可能意味着磁通量为 $0.26\Phi_0$，或 $1.26\Phi_0$，或 $2.26\Phi_0$，等等。[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)就像一把只有一个磁通量子长并无限重复的标尺。

解决这个问题的是一项杰出的电子工程技术，称为**[磁通锁定环](@keyword=flux_locked_loop|lang=zh-CN|style=Feynman) (FLL)**。我们不把SQUID的输出电压作为测量值，而是将SQUID用作一个极其灵敏的**零点探测器**。该电路的工作方式如下：
1. 我们将SQUID锁定在其 $V(\Phi)$ 曲线上的一个特[定点](@keyword=fixed_points|lang=zh-CN|style=Feynman)，比如斜率最陡的点。
2. 如果有外部磁通出现，它会开始使[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)偏离这个点，其电压开始变化。
3. FLL电子设备会立即检测到这个电压变化，并将一个电流反馈到与[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)耦合的另一个线圈中。这个反馈电流产生的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)与外部[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)大小相等、符号相反。
4. 这个反馈磁通完美地抵消了外部磁通，将SQUID感受到的总磁通“锁定”回其原始值。SQUID的电压回到其设定点。

我们记录的测量值不是SQUID的电压，而是FLL为保持SQUID零位所需的反馈电流量。这个反馈电流与我们想要测量的外部[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)成正比且呈线性关系。FLL将SQUID从一个[动态范围](@keyword=dynamic_range|lang=zh-CN|style=Feynman)很小、特性奇特的周期性传感器，转变为一个高度线性、宽带、[动态范围](@keyword=dynamic_range|lang=zh-CN|style=Feynman)极大的仪器，其动态范围仅受反馈电子设备功率的限制 [@problem_id:2862912]。

#### 无休止的嗡鸣：与噪声的斗争

最终是什么限制了[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)神一般的灵敏度？与限制任何灵敏测量的东西一样：噪声。SQUID系统一直在与各种波动的嘈杂声进行持续的斗争 [@problem_id:2498055]。
-   **本征噪声**：这来自SQUID本身。分流电阻中电子的热骚动产生了一个白色的**约翰逊-奈奎斯特噪声**基线。更隐蔽的是，在低频下，会出现一种神秘的**$1/f$噪声**，据信它源于结中的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)陷阱或[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中捕获的杂散磁通涡旋的随机跳跃。
-   **[外在噪声](@keyword=extrinsic_noise|lang=zh-CN|style=Feynman)**：[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)是其环境中任何杂散[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的天线——这些[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)可以来自电力线、电梯、附近的设备，甚至是地球[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。

减噪是一门高超的艺术。[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)被放置在带有磁屏蔽层（如[姆金属](@keyword=mu_metal|lang=zh-CN|style=Feynman)甚至超导屏蔽层）的低温[恒温器](@keyword=thermostats|lang=zh-CN|style=Feynman)中。拾取线圈通常配置为**梯度计**——两个反向缠绕的线圈——它们巧妙地抵消了来自远处源的均匀[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，同时对附近样本的局部信号保持敏感。为了对抗本征$1/f$噪声，人们使用巧妙的[调制](@keyword=modulation|lang=zh-CN|style=Feynman)方案，如磁通[调制](@keyword=modulation|lang=zh-CN|style=Feynman)或偏置电流反转，将测量转移到噪声低得多的更高频率。

#### 终极基准：[能量分辨率](@keyword=energy_resolution|lang=zh-CN|style=Feynman)

考虑到所有这些因素，我们如何定义[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)的终极性能？原始磁通噪声（$S_\Phi^{1/2}$，单位通常为 $\mu\Phi_0/\sqrt{\text{Hz}}$）是一种衡量标准，但它取决于SQUID的几何结构（特别是其[电感](@keyword=inductance|lang=zh-CN|style=Feynman) $L$）。一个更基本的[品质因数](@keyword=q_factor_2|lang=zh-CN|style=Feynman)是**[能量分辨率](@keyword=energy_resolution|lang=zh-CN|style=Feynman)** $\epsilon$ [@problem_id:3017995]。这是与磁通噪声相关的SQUID环路中的能量噪声，定义为：

$$ \epsilon = \frac{S_{\Phi}}{2L} $$

这个量的单位是[焦耳](@keyword=joule|lang=zh-CN|style=Feynman)/赫兹（与普朗克常数相同），它提供了一种与几何结构无关的方法来比较不同[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)的内在质量。当今最好的SQUID的[能量分辨率](@keyword=energy_resolution|lang=zh-CN|style=Feynman)仅比普朗克常数 $\hbar$ 大几倍，这正在挑战量子力学所允许的测量极限。正是这种与基本[量子极限](@keyword=quantum_limit|lang=zh-CN|style=Feynman)的接近，使得[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)不仅是一项卓越的技术，更是一个洞察宇宙运作的深刻窗口。