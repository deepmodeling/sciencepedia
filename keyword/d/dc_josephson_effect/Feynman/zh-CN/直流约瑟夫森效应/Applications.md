## 应用与跨学科联系

我们已经揭示了[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)的非凡原理——这条奇特而美妙的电流之河，无需电压即可流动，由量子力学相位的无形之手引导——我们自然会问：“它有什么用？”这是一个合理的问题。一个奇特的现象是一回事，一个有用的现象又是另一回事。事实证明，答案是[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)不仅仅是一个理论上的奇观，它是一扇门。它为我们提供了一个独特的窗口来窥探量子世界，并提供了一套如此精致的工具，以至于彻底改变了测量技术，开辟了全新的科学技术领域。在本章中，我们将探索其实用的一面，从电子学和灵敏探测器，到[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)和[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的最前沿。

### 作为量子电路元件的结

从本质上讲，约瑟夫森结是一种新型的电子元件。但是是哪种呢？如果我们观察它在极小电流和[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman)下的行为，一个令人惊讶且极其有用的特性便浮现出来。回想一下，结两端的电压与相位变化的速度成正比（$V \propto d\phi/dt$），而电流与相位本身有关（对于小 $\phi$，$I \approx I_c \phi$）。如果我们将这两者结合起来，我们会发现电压与*电流*的变化率成正比（$V \propto dI/dt$）。这正是电感的定义！

但这不是你祖父那辈由线圈制成的[电感](@keyword=inductance|lang=zh-CN|style=Feynman)。这是一个**约瑟夫森电感**，一个纯粹的量子力学元件，其电感值由[基本常数](@keyword=fundamental_constants|lang=zh-CN|style=Feynman)和结的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)决定，$L_J = \hbar / (2e I_c)$ [@problem_id:1214615]。这是一个没有[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)、没有线圈的电感，诞生于超导相位的量子刚性。此外，它的响应是非线性的；它仅在极小电流下才像一个简单的电感。这种独特的非线性不是缺陷，而是一个特性。它是创建[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机基本构件——即[超导量子比特](@keyword=superconducting_qubits|lang=zh-CN|style=Feynman)——的关键要素。transmon[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)是构建大规模量子处理器的主要候选者之一，它不过是一个约瑟夫森结与一个[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)的组合。结的非线性[电感](@keyword=inductance|lang=zh-CN|style=Feynman)确保了该电路的能级不是均匀间隔的，从而允许我们隔离和操纵单个[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)——[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的‘0’和‘1’。

### 大尺度[量子干涉](@keyword=quantum_interference|lang=zh-CN|style=Feynman)：SQUID

如果我们将两个这样的量子导体[并联](@keyword=parallel_connection|lang=zh-CN|style=Feynman)，形成一个闭合的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)路，会发生什么？我们会创造出一个设备，它相当于杨氏著名的光的[双缝实验](@keyword=double_slit_experiment|lang=zh-CN|style=Feynman)的电子版本。我们创造了一个[超导量子干涉仪](@keyword=superconducting_quantum_interference_devices|lang=zh-CN|style=Feynman)（Superconducting QUantum Interference Device），简称SQUID。

想象一下[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)到达环路。它会分裂，一部分[量子波函数](@keyword=quantum_wavefunction|lang=zh-CN|style=Feynman)通过一个结，另一部分通过另一个结。就像光波穿过两个狭缝一样，这两条电子路径在另一端重新组合时可以相互干涉。是什么控制这种干涉呢？是[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。穿过环路的磁通量 $\Phi$ 会在两条路径之间引起一个相对相移，其大小恰好为 $2\pi \Phi / \Phi_0$，其中 $\Phi_0 = h/2e$ 是基本[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)。

因此，该设备在无电阻情况下所能承载的总电流——即其[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)——取决于两条路径是[相长干涉](@keyword=constructive_interference|lang=zh-CN|style=Feynman)还是[相消干涉](@keyword=destructive_interference|lang=zh-CN|style=Feynman)。其结果是量子力学在宏观尺度上令人惊叹的直接展示。[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)作为[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)的函数而[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，其优美简单的数学形式反映了两个[波的干涉](@keyword=wave_interference|lang=zh-CN|style=Feynman) [@problem_id:2997615] [@problem_id:3018030] [@problem_id:957819]：

$$I_c(\Phi) = \sqrt{I_1^2 + I_2^2 + 2 I_1 I_2 \cos\left(\frac{2\pi\Phi}{\Phi_0}\right)}$$

对于相同的结（$I_1 = I_2 = I_{c0}$），这简化为 $I_c(\Phi) = 2I_{c0} |\cos(\pi\Phi/\Phi_0)|$。当磁通量是 $\Phi_0$ 的整数倍时，电流最大化；当磁通量是[半整数](@keyword=half_integers|lang=zh-CN|style=Feynman)倍时，电流被完全抑制。磁通量的最微小变化都会引起最大电流的可测量变化。

这种非凡的灵敏度是SQUID主要应用的基础：作为世界上最灵敏的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)探测器。要制造一个磁力计，只需让一个略大于其最大[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)的恒定电流通过SQUID。这迫使SQUID进入电阻状态，产生一个微小的电压。由于[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)对磁通量如此敏感，这个产生的电压成为穿过环路的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的一个高度灵敏、周期性的度量 [@problem_id:1812683]。[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)现在被用于测量人脑产生的微弱[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)（脑磁图描记术），探测潜艇，以及在地球深处寻找矿藏。

与光学的类比甚至更深。将一个单一、宽的[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)置于[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中，其行为就像一个被光照亮的单缝，产生[衍射图样](@keyword=diffraction_patterns|lang=zh-CN|style=Feynman) [@problem_id:2997632]。[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)在结的宽度上产生连续的相移，导致[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)的不同部分相互干涉。由此产生的总[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)描绘出一个与光的[夫琅禾费衍射](@keyword=fraunhofer_diffraction|lang=zh-CN|style=Feynman)图样形式相同的图案，其中磁通量扮演着缝宽的角色。这是一个惊人的证实，即相同的波动原理既支配着光，也支配着[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的宏伟[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。

### 探索新材料与新物理的探针

也许[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)最深远的应用不是制造设备，而是在基础科学发现中。它提供了一个独特的工具来探测超导性本身的本质。

首先，该效应使我们能够直接掌握材料的微观特性。著名的[Ambegaokar-Baratoff关系](@keyword=ambegaokar_baratoff_relation|lang=zh-CN|style=Feynman)表明，一个结的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)与超导能隙 $\Delta$ 成正比，与结的正常态电阻 $R_N$ 成反比 [@problem_id:608269]。这意味着通过测量一个简单的电流和电阻，我们就可以推断出超导态最基本的参数之一。

但联系更深。[量子波函数](@keyword=quantum_wavefunction|lang=zh-CN|style=Feynman)的相位不仅仅是一个数字；它有一个结构，一种对称性。在传统的“[s波](@keyword=s_waves|lang=zh-CN|style=Feynman)”[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)是球对称的，在所有方向上都具有相同的符号。但在1980年代，物理学家发现了“高温”[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)，理论表明其配对态是不同的，具有所谓的“$d_{x^2-y^2}$”对称性。这种状态像一个四叶草：[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)沿两个轴为正，沿中间的两个轴为负。

人们如何可能“看到”这种符号变化？[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)提供了答案。约瑟夫森电流的大小取决于两个[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的重叠。如果你在一个s波（总是为正）和一个p波（奇宇称，意味着它在一侧为正，另一侧为负）[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)之间制造一个结，由于对称性，所有方向上的总[重叠积分](@keyword=overlap_integral|lang=zh-CN|style=Feynman)为零。在理想条件下，不应该有[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)流动 [@problem_id:1203107]！

这一原理在1990年代的一系列精彩实验中被用来证明高温超导体的 $d$ 波性质。科学家们构建了一个“角结SQUID”，其中两个结被制作在一个单一 $d$ 波晶体的正交面上 [@problem_id:2802605]。由于 $d$ 波对称性，一个结具有正耦合，另一个结具有负耦合。这种符号翻转等同于在其中一个结中内置了一个 $\pi$ 的内禀相移。当放置在SQUID环路中时，这个内禀的 $\pi$ [相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)会翻转[干涉图样](@keyword=interference_pattern|lang=zh-CN|style=Feynman)：[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)的最大值现在出现在[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)量子半整数倍处，而最小值出现在整数倍处。观察到这种移动了的图样是证明 $d$ 波配对的“确凿证据”，这一发现重塑了整个领域。环路中的这样一个“$\pi$结”甚至可以导致在[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)下自发产生半个[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)量子，这是一种称为自发轨道矩的美妙现象 [@problem_id:2802605]。

### 前沿：介观与原子尺度结

[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)的故事仍在书写中。物理学家现在正在探索用单个原子、一个分子或一个称为量子点的微小[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)岛来替代绝缘势垒的结。在这些[介观系统](@keyword=mesoscopic_systems|lang=zh-CN|style=Feynman)中，约瑟夫森电流由存在于“势垒”内部的离散[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)——即安德烈夫束缚态——承载 [@problem_id:83761]。通过研究这些奇异结中的[电流-相位关系](@keyword=current_phase_relation|lang=zh-CN|style=Feynman)，我们以前所未有的细节了解了[量子输运](@keyword=quantum_transport|lang=zh-CN|style=Feynman)。这些研究不仅仅是学术性的；它们正推动着电子学的终极微型化，并对理解未来量子器件的行为至关重要。从课堂上的奇观到[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的核心，从宏观量子怪现象到窥探物质对称性的显微镜，[直流约瑟夫森效应](@keyword=dc_josephson_effect|lang=zh-CN|style=Feynman)证明了量子力学的深邃之美、统一性以及惊人的实用性。