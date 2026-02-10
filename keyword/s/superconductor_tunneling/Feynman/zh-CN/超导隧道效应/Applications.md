## 应用与跨学科联系

既然我们已经探索了控制电子进入[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)和在[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)之间隧穿的奇特而美妙的规则，我们可以问一个始终是物理学核心的问题：“那又怎样？”它对我们有什么好处？事实证明，答案是惊人的。单粒子和库珀对跨越绝缘势垒的精巧量子舞蹈，不仅仅是一种实验室里的奇观。它是一些有史以来最精确测量工具背后的引擎，是构建未来[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的关键，是洞悉物质本质的独特窗口，也是物理定律统一性的惊人例证。

在本章中，我们将踏上探索这些应用的旅程。我们将看到相同的基本原理如何在截然不同的背景下显现，以曾经属于科幻小说的方式改变我们的世界。我们不会纠缠于复杂的数学，而是像物理学家那样，尝试掌握每种应用背后的*思想*——去欣赏其基本原理中的美与力量。

### 精密度的艺术：计量学与标准

[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)最深刻的后果之一是它能够将电压和电流的宏观世界与[基本常数](@keyword=fundamental_constants|lang=zh-CN|style=Feynman)的不变世界联系起来。想象一下，试图创建一个完全可复现的一伏特标准。几十年来，[计量学](@keyword=metrology|lang=zh-CN|style=Feynman)家依赖于仔细校准的[电化学电池](@keyword=electrochemical_cells|lang=zh-CN|style=Feynman)，但这些电池容易漂移并受环境变化影响。[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)提供了一条摆脱这种不确定性的途径。

当一个约瑟夫森结沐浴在精确频率为 $f$ 的微波辐射中时，原本平滑的电流-电压曲线会分裂成一系列完全平坦、间距完美的电压台阶。这些就是我们讨论过的“[夏皮罗台阶](@keyword=shapiro_steps|lang=zh-CN|style=Feynman)”。其神奇之处在于，第 $n$ 步的电压 $V_n$ 由一个精确且不可改变的公式给出：

$$
V_n = n \left( \frac{h}{2e} \right) f
$$

看看这个方程。在右边，我们有一个整数 $n$，频率 $f$（可以使用原子钟稳定到令人难以置信的精度），以及自然界两个最基本的常数：普朗克常数 $h$ 和基本电荷 $e$。这里没有任何关于特定材料、温度或结本身的混乱之处。可以说，电压是通过将[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的量子相位锁定到外部时钟的“滴答”声中被“计数”出来的[@problem_id:2832151]。根据国际协议，这种效应现在是伏特法定定义的基础。任何时候你使用一个校准过的电压表，你都在依赖一个发生在某个国家标准实验室的低温[恒温器](@keyword=thermostats|lang=zh-CN|style=Feynman)中的[宏观量子现象](@keyword=macroscopic_quantum_phenomena|lang=zh-CN|style=Feynman)。

但是，我们一开始如何知道我们是否有一个“好”的结呢？在这里，理论再次提供了一个优美的自我检验方法。对于两个相同[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)之间的理想结，其[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman) $I_c$ 和其正常态电阻 $R_n$ 的乘积仅取决于材料的超导能隙 $\Delta_0$：

$$
I_c R_n = \frac{\pi \Delta_0}{2e}
$$

这就是著名的Ambegaokar–Baratoff关系。它告诉实验者，如果他们测量其器件的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)和正常电阻，其乘积应该具有一个仅由[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)决定的特定、普适的值[@problem_id:2862998]。这是一个简单、优雅的质量控制测试，它将一个微观量子性质（$\Delta_0$）与两个易于测量的宏观电学特性联系起来。

### 探测无形：[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)

如果说[交流约瑟夫森效应](@keyword=ac_josephson_effect|lang=zh-CN|style=Feynman)给了我们世界上最好的电压表，那么[直流约瑟夫森效应](@keyword=dc_josephson_effect|lang=zh-CN|style=Feynman)则给了我们最灵敏的磁力计。这种设备被称为[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)，即[超导量子干涉仪](@keyword=superconducting_quantum_interference_devices|lang=zh-CN|style=Feynman)（Superconducting QUantum Interference Device），这个名字揭示了一切。

想象一个超导电路分成两条路径，每条臂上都有一个[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)，然后重新汇合形成一个环路[@problem_id:1806369]。当一股库珀对电流接近这个分叉口时，其量子波函数分裂并同时沿着两条路径传播。当路径重新组合时，[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的两个部分发生干涉，就像经典[双缝实验](@keyword=double_slit_experiment|lang=zh-CN|style=Feynman)中的光波一样。能够通过该设备的总超流取决于这两个量子波是[相长干涉](@keyword=constructive_interference|lang=zh-CN|style=Feynman)还是相消干涉。

那么，是什么控制这种干涉呢？是[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。阿哈罗诺夫-玻姆效应告诉我们，穿过环路的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi_B$ 会在两条路径之间引入一个相对相位差。通过改变[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)，我们可以将总[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)从最大值（相长干涉）[调制](@keyword=modulation|lang=zh-CN|style=Feynman)到最小值（相消干涉），然后再回来。[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)的灵敏度如此之高，以至于相当于单个红细胞[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)一小部分的磁通量变化，就足以引起其电流的可测量变化。

这种无与伦比的灵敏度开辟了新的研究领域。[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)是脑磁图（MEG）中的有源元件，这是一种通过探测神经电流产生的微弱[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)来绘制人脑活动的无创技术。它们被用于地球物理勘探中寻找矿藏，以及在基础物理学中搜寻像轴子这样的奇异粒子。SQUID是量子力学“怪异性”——叠加和干涉——可以被用来制造强大实用工具的终极证明。

### 构建未来：[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机与放大器

到目前为止，我们一直将约瑟夫森结视为无源器件。但它们最令人兴奋的角色可能是作为[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的有源核心。要构建一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)——经典比特的量子版本——你需要一个至少有两个可以控制的离散能级的系统。一个[简谐振子](@keyword=simple_harmonic_oscillator|lang=zh-CN|style=Feynman)，比如弹簧上的质量块或者由电感（$L$）和电容（$C$）构成的[标准电路](@keyword=canonical_circuits|lang=zh-CN|style=Feynman)，是行不通的，因为它的能级都是等间距的。如果你试图将它从[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)激发到第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)，你同样有可能将它激发到第二、三和更高的能级。

这就是[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)施展其魔力的地方。当你在[LC电路](@keyword=lc_circuits|lang=zh-CN|style=Feynman)中用一个约瑟夫森结替换标准电感时，奇妙的事情发生了。这个结的行为不像一个简单的线性电感。它充当一个*非线性、可调谐的[电感](@keyword=inductance|lang=zh-CN|style=Feynman)*[@problem_id:2832172]。它的“[电感](@keyword=inductance|lang=zh-CN|style=Feynman)”取决于流过它的电流量！这种非线性打破了能级的对称性。[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)（$|0\rangle$）和第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)（$|1\rangle$）之间的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)现在不同于第一和第二[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)之间的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。这一特性，称为[非谐性](@keyword=anharmonicity|lang=zh-CN|style=Feynman)，允许我们使用微波精确地寻址 $|0\rangle \leftrightarrow |1\rangle$ 跃迁，而不干扰更高的能级。这个器件——一个[并联](@keyword=parallel_connection|lang=zh-CN|style=Feynman)电容的约瑟夫森结——就是著名的“transmon”[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，是构建大规模[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的主要候选者之一。

然而，[库珀对隧穿](@keyword=cooper_pair_tunneling|lang=zh-CN|style=Feynman)的这一优美应用有一个克星：单粒子（[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)）隧穿。transmon[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的频率对其电环境极其敏感。如果一个游离的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)——一个被打破的库珀对——隧穿到[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的小超导岛上，它会改变局域的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)环境，并导致[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)频率的随机漂移[@problem_id:742188]。这种“[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)毒化”是退相干的主要来源，[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)是[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)失去其[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)的过程。这是一个完美但又令人沮丧的例子，说明了隧穿的两个方面：库珀对的[相干隧穿](@keyword=coherent_tunneling|lang=zh-CN|style=Feynman)构建了我们的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，而单粒子的[随机隧穿](@keyword=stochastic_tunneling|lang=zh-CN|style=Feynman)却在密谋摧毁它。

### 洞悉物质之窗：作为谱学工具的隧穿

我们已经看到了如何使用隧穿来构建器件。但是，如果我们反过来，用一个隧道结来探测[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)本身的基本性质呢？

隧穿进入[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的单粒子电流不仅仅是电压的[平滑函数](@keyword=smoothing_functions|lang=zh-CN|style=Feynman)。它是一个信息丰富的景观。微分[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman) $dI/dV$ 是超导[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)的直接映射。测量它使我们能够亲眼看到[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta$。

但还有更多。如果我们非常仔细地观察[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)*之上*的[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)，或者更进一步，观察它的二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman) $d^2I/dV^2$，我们会看到一系列微妙的摆动和凸起。很长一段时间里，这些被认为是纯粹的瑕疵。我们现在知道它们是来自材料内部的信息。这些特征对应于非弹性隧穿：一个[电子隧穿](@keyword=electron_tunnelling|lang=zh-CN|style=Feynman)过势垒，进入[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)，并在此过程中，通过创造一个[声子](@keyword=phonons|lang=zh-CN|style=Feynman)——一个[晶格振动](@keyword=crystal_lattice_vibrations|lang=zh-CN|style=Feynman)的量子——来放弃一点能量。这些特征出现在对应于[能隙能量](@keyword=bandgap_energy|lang=zh-CN|style=Feynman)和[声子](@keyword=phonons|lang=zh-CN|style=Feynman)能量之和的电压处，$eV \approx \Delta + \hbar\omega_{phonon}$ [@problem_id:2818832]。

通过仔细分析这些凸起的位置和形状，物理学家可以反向推演并重建[电子-声子相互作用](@keyword=electron_phonon_interaction|lang=zh-CN|style=Feynman)的整个谱，这个函数被称为[Eliashberg谱函数](@keyword=eliashberg_spectral_function|lang=zh-CN|style=Feynman)，$\alpha^2F(\omega)$ [@problem_id:2986493]。这个函数本质上是结合电子形成[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的“胶水”的配方。隧道谱学使我们能够真正地听到负责超导性的[晶格振动](@keyword=crystal_lattice_vibrations|lang=zh-CN|style=Feynman)模式。这是一个极其强大的能力，将一个简单的结变成了一台用于[量子物质](@keyword=quantum_matter|lang=zh-CN|style=Feynman)的精密显微镜。

这种测量微小能量沉积的能力也使[超导隧道结](@keyword=superconducting_tunnel_junction|lang=zh-CN|style=Feynman)（STJs）成为非凡的[粒子探测器](@keyword=particle_detectors|lang=zh-CN|style=Feynman)[@problem_id:407067]。当一个[X射线](@keyword=x_ray|lang=zh-CN|style=Feynman)[光子](@keyword=photon|lang=zh-CN|style=Feynman)或其他高能粒子被[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)吸收时，其能量迅速转化为一阵被打破的[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)，即[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)。产生的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)数量与沉积的能量成正比。通过测量由此产生的单粒子隧道电流脉冲，我们可以以远超传统[半导体探测器](@keyword=semiconductor_detectors|lang=zh-CN|style=Feynman)的分辨率确定入射粒子的能量。这使得STJ探测器成为从[X射线](@keyword=x_ray|lang=zh-CN|style=Feynman)天文学到[材料分析](@keyword=materials_analysis|lang=zh-CN|style=Feynman)等领域的重要工具。

### 物理学的统一性：无处不在的[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)

也许所有课程中最美的一课是，[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)不仅仅关乎[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)。它是量子力学的一个普适原理。只要你有两个[宏观量子态](@keyword=macroscopic_quantum_state|lang=zh-CN|style=Feynman)——两个由单一集体[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)描述的系统——被弱连接，它就会出现。

考虑一个[玻色-爱因斯坦凝聚](@keyword=bose_einstein_condensation|lang=zh-CN|style=Feynman)（BEC），这是一种物质状态，其中数百万个超冷原子失去其个体身份，并凝聚成一个单一的量子“[超原子](@keyword=superatoms|lang=zh-CN|style=Feynman)”。如果你将一个BEC捕获在一个双阱势中，原子可以从一个阱隧穿到另一个。就像约瑟夫森结中的[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)一样，这种隧穿可以在两个凝聚体之间建立相干的相位关系。人们可以观察到*原子*的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)电流来回流动，并且这种原子电流对力和旋转极其敏感，就像SQUID对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)一样。描述双阱中BEC的数学与约瑟夫森结的数学是相同的[@problem_id:1252197]。这是同样的物理学，只是演员不同。

这个统一的主题甚至延伸到了研究的前沿。在神秘的高温[铜氧化物超导体](@keyword=cuprate_superconductors|lang=zh-CN|style=Feynman)中，材料由堆叠的、准二维的[铜氧平面](@keyword=cuo2_planes|lang=zh-CN|style=Feynman)组成。这些平面之间的[电子输运](@keyword=electron_transport|lang=zh-CN|style=Feynman)可以被理解为一种约瑟夫森隧穿，其中输运的性质——无论是库珀对的相干流动还是单粒子的非相干跳跃——都为这些神秘材料的潜在物理学提供了深刻的线索[@problem_id:3009339]。

从伏特的日常定义到对[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的探索，从窥探[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的核心到在[冷原子](@keyword=cold_atoms|lang=zh-CN|style=Feynman)云中看到相同的物理学，超导隧穿现象揭示了量子力学的深刻力量和统一性。这是一个完美的例子，说明了对一个源于纯粹好奇心的奇异物理效应的探索，如何能绽放出改变世界的技术和深刻科学见解的森林。