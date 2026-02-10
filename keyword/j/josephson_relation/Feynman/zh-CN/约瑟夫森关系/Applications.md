## 应用与跨学科联系

如果我告诉您，两个几乎只有一行文字的简单方程，却构成了我们国际[电压标准](@keyword=voltage_standard|lang=zh-CN|style=Feynman)的基础，让我们能够窃听人脑的私语，为[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的引擎提供动力，甚至引导我们搜寻宇宙中最难以捉摸的一些粒子，您会怎么想？这听起来像是科幻小说，但这却是约瑟夫森关系的现实。在探究了支配这些效应的量子力学原理之后，我们现在来到了故事中激动人心的部分：亲眼见证它们的实际应用。我们将目睹这些关于相位和电流的抽象概念如何演变成一系列令人惊叹的技术和科学工具，并重塑了我们的世界。这不仅仅是一份应用清单；它证明了自然界深刻而又常常出人意料的统一性，即一个单一、优雅的概念可以成为打开无数扇门的钥匙。

### 终极标尺：伏特的量子标准

想象一下用一把橡皮尺来建造摩天大楼——这把尺子的长度会随着温度、湿度和一天中的时间而改变。你的建筑将会是一场灾难。几个世纪以来，[计量学](@keyword=metrology|lang=zh-CN|style=Feynman)家——研究测量的科学家——在伏特单位上面临着类似的问题。标准伏特基于化学电池，而化学电池不稳定且容易漂移。我们需要的不是一个更好的*物体*，而是一条更好的*自然定律*来作为标准。

[交流约瑟夫森效应](@keyword=ac_josephson_effect|lang=zh-CN|style=Feynman)以最壮观的方式提供了答案。正如我们所见，当一个约瑟夫森结被特定频率 $f$ 的微波照射时，其原本平滑的电流-电压曲线上会出现一系列完全平坦的、恒定电压的台阶。这些就是著名的[夏皮罗台阶](@keyword=shapiro_steps|lang=zh-CN|style=Feynman)。其神奇之处在于这些台阶出现的位置。第 $n$ 级台阶的电压由一个惊人简单且稳健的公式给出：

$$ V_n = n \frac{h}{2e} f $$

请仔细看这个方程。电压 $V_n$ 取决于一个整数 $n$（我们可以数出来）、微波频率 $f$（可以用原子钟的精度测量），以及两个自然界最基本常数的比值：普朗克常数 $h$ 和[基本电荷](@keyword=elementary_charge|lang=zh-CN|style=Feynman) $e$。方程中没有任何关于结的材料、尺寸、[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)或温度的信息。电压台阶是普适的。[@problem_id:560913]

这一现象是[锁相](@keyword=phase_locking_2|lang=zh-CN|style=Feynman)的一个绝佳例子。由直流电压驱动的结自身内部[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)与外部微波驱动[同步](@keyword=entrainment|lang=zh-CN|style=Feynman)。这就像推一个孩子荡秋千：如果你以恰当的频率（或其整数倍）去推，你就能锁定在一个稳定、高振幅的运动中。在这里，结的量子相位锁定在微波场上，迫使平均电压取这些量子化的值之一。[@problem_id:2832204] 自1990年以来，国际伏特标准就是基于这种效应定义的。我们不再依赖于“橡皮尺”；我们拥有了一把量子标尺，其刻度是由物理学自身坚定不移的定律所绘制的。

### 量子听诊器：SQUID与无穷小的测量

量子力学常常与不确定性联系在一起，但它也是一个无与伦比的精确领域。如果我们不是用一个，而是用两个[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)，并将它们[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成一个[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)路，我们就创造了一个具有近乎神奇灵敏度的设备：[超导量子干涉仪](@keyword=superconducting_quantum_interference_devices|lang=zh-CN|style=Feynman)，简称[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)。

其原理与著名的[双缝实验](@keyword=double_slit_experiment|lang=zh-CN|style=Feynman)直接类似，只不过对象是超导电流而非单个电子。一个偏置电流到达环路后会分流，一部分通过一个结，另一部分通过另一个结。然后，两股超导电流重新汇合。就像光波一样，这两条量子路径可以发生[相长干涉](@keyword=constructive_interference|lang=zh-CN|style=Feynman)（叠加成一个大的总电流）或相消干涉（相互抵消）。是什么控制着这种干涉呢？是穿过环路的磁通量 $\Phi$。

正如我们从[相位相干性](@keyword=phase_coherence|lang=zh-CN|style=Feynman)原理中推导出的，磁通量在两条路径之间施加了一个相对[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)。结果是，该设备能承载的总最大超导电流（其[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)）会随着外加磁通量而剧烈[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)：

$$ I_c(\Phi) = 2I_{c0} \left| \cos\left( \frac{\pi\Phi}{\Phi_0} \right) \right| $$

在这里，$I_{c0}$ 是单个结的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)，而 $\Phi_0 = h/2e$ 是磁通量量子——一个极其微小的磁通量单位。[@problem_id:2997615] [@problem_id:3018086] [@problem_id:3018030] 这个公式告诉我们，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)的电流对[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)的变化极其敏感。仅仅单个磁通量量子的一小部分变化，就会引起[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)的巨大改变。这使得[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)成为科学界已知的最灵敏的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)探测器，能够测量比地球[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)弱数十亿倍的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。

这个“量子听诊器”为我们打开了认识世界的新窗口。在医学领域，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)阵列被用于脑磁图（MEG），以绘制人脑电活动产生的微弱[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，为[癫痫](@keyword=epilepsy|lang=zh-CN|style=Feynman)、阿尔茨海默病和认知功能研究提供见解。在地质学领域，它们被搭载在飞行器上飞越地形，以探[测地球](@keyword=geodesic_balls|lang=zh-CN|style=Feynman)[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的微小变化，帮助定位矿床和地下水资源。在[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)领域，它们被用来探测纳米尺度上新奇材料的磁性。

### [量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的核心：用结来构建

故事并未止于测量。正是那允许我们制造出世界上最好标尺的物理学，也为一种新型世界——[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机——提供了核心构件。

事实证明，单个约瑟夫森结是一个近乎完美的无损非线性[电感](@keyword=inductance|lang=zh-CN|style=Feynman)。当与[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)结合时，它形成一个非线性[电子振荡器](@keyword=electronic_oscillator|lang=zh-CN|style=Feynman)。像任何[振荡器](@keyword=oscillators|lang=zh-CN|style=Feynman)一样，它有一个自然共振频率，称为结等离子体频率，它取决于其[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman) $I_c$ 和电容 $C$。[@problem_id:2863017] 但由于[约瑟夫森能量](@keyword=josephson_energy|lang=zh-CN|style=Feynman)的正弦特性，这个量子[振荡器](@keyword=oscillators|lang=zh-CN|style=Feynman)的能级不是[均匀分布](@keyword=uniform_distribution|lang=zh-CN|style=Feynman)的——它们是非谐的。这就像一根吉他弦，其第一个[泛音](@keyword=overtones|lang=zh-CN|style=Feynman)不是基频的两倍，而是略有不同。

这种非谐性是一份礼物。它使我们能够分离出最低的两个能态——[基态](@keyword=basis_states|lang=zh-CN|style=Feynman) $|0\rangle$ 和第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman) $|1\rangle$——并将它们用作一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)（qubit）。这种类型的[超导量子比特](@keyword=superconducting_qubits|lang=zh-CN|style=Feynman)被称为“transmon”，是当今构建大规模量子处理器的主流平台之一。

但是我们如何控制这些[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)并让它们进行计算呢？在这里，SQUID再次华丽登场。如果我们将[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)中的单个结替换为[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)环路，[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的有效[约瑟夫森能量](@keyword=josephson_energy|lang=zh-CN|style=Feynman)就变得可以通过外部[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)进行调控。[@problem_id:2997597] 由于[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的跃迁频率直接依赖于这个[约瑟夫森能量](@keyword=josephson_energy|lang=zh-CN|style=Feynman)，我们获得了按需改变[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)“颜色”的能力，只需用一个微小的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)轻轻“挠”它一下。这种频率可调性是关键所在：我们可以让两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)发生共振以使它们相互作用并执行[量子门](@keyword=quantum_computing_gates|lang=zh-CN|style=Feynman)，然后迅速将它们[失谐](@keyword=detuning|lang=zh-CN|style=Feynman)以关闭相互作用。[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)不仅仅是一个组件；它正是现代超导量子处理器的心脏。

### 洞察物质灵魂之窗：探索基础物理

到目前为止，我们一直在用[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)来*构建*东西。但也许它最深刻的作用是作为一种发现的工具，一把解开物质基本秘密的钥匙。

#### 揭示[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的对称性

我们常常将[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)想象成简单、均匀的库珀对海洋。但大自然远比这更有创造力。[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的量子波函数可以有不同的“形状”或对称性，就像原子中电子的轨道一样。常规类型被称为*s波*，它是球对称的。但其他类型，如在高温[铜氧化物超导体](@keyword=cuprate_superconductors|lang=zh-CN|style=Feynman)中发现的*d波*对称性，则更为复杂，具有正负号交替的瓣状结构。

人们如何才能证明这样的事情呢？[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)通过一个设计巧妙的“相位敏感”实验给出了答案。想象一个在*d波*[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的方形晶体角上制作的SQUID，其中一个结在'a'面上，另一个在'b'面上。由于*d波*对称性，序参数在一个晶轴上为正号，而在另一个晶轴上为负号。隧穿到这些面时，一个结的行为正常，而另一个结的行为就像它内置了一个内禀的 $\pi$ [相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)——它变成了一个“$\pi$结”。

这个内禀的 $\pi$ 相移完全改变了[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)的干涉图样。在零[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)时，它不再显示[相长干涉](@keyword=constructive_interference|lang=zh-CN|style=Feynman)，而是显示相消干涉。整个[干涉图样](@keyword=interference_pattern|lang=zh-CN|style=Feynman)移动了半个[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)量子，即 $\Phi_0/2$。[@problem_id:2869653] 在20世纪90年代初观察到这一[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)是一项里程碑式的成果，为高温超导的非常规*d波*性质提供了最强有力的证据之一。这是一个利用[量子干涉](@keyword=quantum_interference|lang=zh-CN|style=Feynman)为[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)内部量子结构“画像”的案例。

#### 追寻马约拉纳费米子

我们的旅程在凝聚态物理的绝对前沿结束：寻找[马约拉纳费米子](@keyword=majorana_fermions|lang=zh-CN|style=Feynman)。这些是奇特的粒子，它们是自身的反粒子，被预测存在于“拓扑”[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的末端，作为零能态。找到它们是一个圣杯，不仅对于基础科学如此，也因为它们可能掌握着构建固有[容错量子计算机](@keyword=fault_tolerant_quantum_computer|lang=zh-CN|style=Feynman)的关键。

但是，你如何“看到”一个能量为零、[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为零的粒子呢？[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)再次提供了一条潜在的生命线。当一个[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)由[拓扑超导体](@keyword=topological_superconductors|lang=zh-CN|style=Feynman)制成时，两端的[马约拉纳模](@keyword=majorana_modes|lang=zh-CN|style=Feynman)可以相互作用。这种相互作用催生了一个奇特的新过程：*单个电子*在结上的[相干隧穿](@keyword=coherent_tunneling|lang=zh-CN|style=Feynman)，而不是通常的[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)。这导致了一个 $4\pi$ 周期的[电流-相位关系](@keyword=current_phase_relation|lang=zh-CN|style=Feynman)，而不是标准的 $2\pi$ 周期。

如果施加一个电压 $V$，这种奇特的周期性应该表现为“[分数交流约瑟夫森效应](@keyword=fractional_ac_josephson_effect|lang=zh-CN|style=Feynman)”。产生的电流应该以 $f = eV/h$ 的频率[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，这恰好是传统效应频率的一半。[@problem_id:1214583] [@problem_id:2869685] 观察到这个减半的频率将是马约拉纳物理学的确凿证据。这些实验极具挑战性；这种脆弱的[量子效应](@keyword=quantum_effects|lang=zh-CN|style=Feynman)很容易被破坏底层对称性的杂散[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)或其他缺陷所掩盖。[@problem_id:2869685] 尽管如此，探索仍在继续，而[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)在这场高风险的粒子搜寻中充当了我们最灵敏的探针。

从平淡无奇的伏特定义到对新粒子的奇异探索，约瑟夫森关系提供了一条惊人地多功能的线索，连接了广阔的科学技术领域。它有力地提醒我们，在量子世界里，最简单的规则往往会导致最丰富、最美丽的后果。