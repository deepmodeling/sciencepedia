## 引言
在奇妙而诡谲的量子世界中，[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中的数百万个电子有可能放弃其个体身份，作为一个整体——一个由单一相干相位描述的宏观量子波——进行运动。但当你将两个这样的量子实体放在一起，仅用一层薄薄的绝缘势垒隔开时，会发生什么呢？这种被称为约瑟夫森结的结构，形成了一个独特的量子“铰链”，而储存在这个铰链中的能量——[约瑟夫森能量](@keyword=josephson_energy|lang=zh-CN|style=Feynman)——是现代物理学中最强大、用途最广泛的概念之一。理解这种能量是揭开[宏观量子现象](@keyword=macroscopic_quantum_phenomena|lang=zh-CN|style=Feynman)奥秘并利用其发展革命性技术的关键。本文旨在解读[约瑟夫森能量](@keyword=josephson_energy|lang=zh-CN|style=Feynman)的本质，在抽象的量子理论与切实的实际应用之间架起一座桥梁。

本文的结构旨在循序渐进地构建这种理解。首先，在“原理与机制”部分，我们将深入探讨[约瑟夫森能量](@keyword=josephson_energy|lang=zh-CN|style=Feynman)的起源，将其具象化为一个“搓板”[势能景观](@keyword=potential_energy_landscape|lang=zh-CN|style=Feynman)。我们将探讨这一景观如何决定结对电流的响应，如何产生著名的直流和[交流约瑟夫森效应](@keyword=ac_josephson_effect|lang=zh-CN|style=Feynman)，以及如何构成结作为量子电感和[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)构建模块的双重身份的基础。接下来，“应用与跨学科联系”部分将展示这一原理的巨大效用。我们将看到工程师如何精心塑造[约瑟夫森能量](@keyword=josephson_energy|lang=zh-CN|style=Feynman)景观来为[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机设计稳健的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，它如何解释奇异[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的行为，以及其底层物理学如何提供一种通用语言，适用于从金属电路到超冷原子云等多种多样的系统。

## 原理与机制

想象一场盛大的舞会，每一位舞者都以完美、同步的节奏舞动。这有点像[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)——大量电子（以**[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)**的形式存在）凝聚成一个单一的[宏观量子态](@keyword=macroscopic_quantum_state|lang=zh-CN|style=Feynman)。就像海洋中的一道波浪，这整个[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)可以用一个振幅和，最重要的是，一个单一的、相干的**相位**来描述。这不仅仅是一个数学上的抽象概念；它是一个物理属性，原则上，你可以追踪放在你桌上的一块超导金属的这个属性。

现在，如果你把两个这样的舞厅——每个舞厅都有自己完美[同步](@keyword=entrainment|lang=zh-CN|style=Feynman)的舞蹈——用一条狭窄的走廊连接起来，会发生什么？这就是**[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)**的本质：两个[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)被一层薄薄的绝缘势垒，即“弱连接”隔开。舞者们——[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)——现在可以隧穿过走廊，从一个房间到另一个。问题是，他们的舞蹈之间有何关联？

### 量子相位的舞蹈

你可能认为你需要知道每个房间中舞蹈的[绝对时间](@keyword=absolute_time|lang=zh-CN|style=Feynman)或“相位”，比如说，相对于格林威治的主时钟。但大自然以其优雅的简洁性并不关心这一点。由这两个[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的耦合产生的所有有趣的物理现象，都只取决于**[相对相位](@keyword=relative_phase|lang=zh-CN|style=Feynman)**，$\phi = \phi_1 - \phi_2$，即它们舞蹈节拍的差异。

为什么会这样？原因植根于物理学最深刻的原理之一：对称性。支配整个系统——包括两个[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)和它们之间的连接——的物理定律必须尊重总电荷守恒。这个守恒定律与物理学家所说的全局[规范不变性](@keyword=gauge_invariance|lang=zh-CN|style=Feynman)有着深刻的联系。这意味着，如果我们偷偷地将*两个*[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的相位都移动完全相同的量，任何物理性质都不会改变。能量、电流，任何你可以测量的力，都必须保持不变。要实现这一点，唯一的可能是物理规律不单独依赖于$\phi_1$和$\phi_2$，而只依赖于它们的差值$\phi$，因为$\phi$不受这种全局平移的影响[@problem_id:2832141]。这就像测量一栋建筑中两层楼之间的高度差；重要的是一个球在它们之间下落的距离，而不是它们相对于海平面的绝对高程。这个[相对相位](@keyword=relative_phase|lang=zh-CN|style=Feynman)$\phi$不仅仅是一个记账参数；它成了一个真正的物理变量，一个可以改变、储存能量并驱动电流的自由度。

### [相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman)的能量

如果相对相位$\phi$是一个物理变量，我们应该能够对它做功。而如果我们做功来改变它，结必定将这些功以势能的形式储存起来。确实，存在一个与两个[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)耦合相关的能量，称为**[约瑟夫森能量](@keyword=josephson_energy|lang=zh-CN|style=Feynman)**。这种能量的形式惊人地简单而优雅：

$U(\phi) = -E_J \cos(\phi)$

这里，$E_J$是一个正常数，即[约瑟夫森能量](@keyword=josephson_energy|lang=zh-CN|style=Feynman)，它代表了耦合的强度。更大的$E_J$意味着[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)之间的联系更强。这个优美简洁的余弦函数几乎告诉了我们关于结的基本行为所需知道的一切。

让我们想象一下这个[势能景观](@keyword=potential_energy_landscape|lang=zh-CN|style=Feynman)。它看起来像一系列无限重复的山丘和山谷，很像波纹状的屋顶或老式的**搓板**。系统，就像一个在这个表面上滚动的弹珠，会自然地倾向于停在其中一个山谷的底部[@problem_id:1785364]。这些位于$\phi = 0, \pm 2\pi, \pm 4\pi, \ldots$的山谷是[稳定平衡](@keyword=stable_equilibrium|lang=zh-CN|style=Feynman)点——能量最低的状态。位于$\phi = \pm \pi, \pm 3\pi, \ldots$的山丘顶峰则是[不稳定平衡](@keyword=unstable_equilibrium|lang=zh-CN|style=Feynman)点。从峰顶轻轻一推，弹珠就会滚入山谷。

那么，是什么决定了这些山谷的深度呢？这由[约瑟夫森能量](@keyword=josephson_energy|lang=zh-CN|style=Feynman)$E_J$决定。在这里，我们发现了量子世界与我们的宏观世界之间一个非凡的联系。$E_J$的值与**[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)**$I_c$成正比——这是在没有任何电压或电阻的情况下，能够通过结的最大超导电流。其关系式为：

$E_J = \frac{\hbar I_c}{2e}$

其中$\hbar$是约化普朗克常数，$2e$是一个[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)[@problem_id:1785391] [@problem_id:2862956]。这非同寻常！一个基本的量子能量尺度$E_J$直接与一个你可以用电流表测量的经典电流$I_c$相联系。将相位从谷底（$\cos(\phi)=1$）改变到山顶（$\cos(\phi)=-1$）对应于储存了等于$2E_J$的能量，这相当于完成这一改变所需的功[@problem_id:1766572]。

### 倾斜搓板：电流的作用

如果我们试图强制一个电流通过我们的结，会发生什么？在我们的搓板类比中，施加一个[偏置电流](@keyword=bias_current|lang=zh-CN|style=Feynman)$I_b$就像物理上倾斜整个搓板。势能景观被修改了，获得了一个线性的倾斜：

$U(\phi) = -E_J \left( \cos(\phi) + \frac{I_b}{I_c} \phi \right)$

现在，山谷的底部不再是平坦的[@problem_id:1785380]。弹珠不会停在$\phi=0$处；它会在山谷侧壁上稍微靠上的一个新位置达到平衡，其相位为$\phi_{stable} = \arcsin(I_b/I_c)$。在这一点上，来自正弦势的“力”与来自倾斜的“力”完美平衡。这就是**[直流约瑟夫森效应](@keyword=dc_josephson_effect|lang=zh-CN|style=Feynman)**：一个稳定的、无耗散的超导电流$I_b$流过结，[电压降](@keyword=voltage_droop|lang=zh-CN|style=Feynman)为零，由这个静态的[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman)维持。

随着我们增加偏置电流，我们使搓板倾斜得越来越陡。[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)变得越来越浅，将相位束缚在给定山谷中的能垒开始缩小[@problem_id:2862956]。最终，我们达到[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)，$I_b = I_c$。在这一点上，倾斜是如此严重，以至于山谷完全消失了。不再有稳定点。相位不再被束缚，开始沿着无限倾斜的搓板连续“滚动”下去。

相位的这种滚动就是**[交流约瑟夫森效应](@keyword=ac_josephson_effect|lang=zh-CN|style=Feynman)**。根据第二个基本约瑟夫森关系，变化的相位产生电压：$V = (\hbar/2e) \frac{d\phi}{dt}$。因此，一旦相位开始滚动，结两端就会出现一个有限的、恒定的电压。[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)已经“恢复正常”，恰恰因为相位被释放而产生了电阻。

### 结作为电路元件：[电感](@keyword=inductance|lang=zh-CN|style=Feynman)和[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)

让我们更仔细地观察当结处于和平状态时，有一个小电流通过，其相位在[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)底部附近。对于围绕[平衡点](@keyword=equilibrium_points|lang=zh-CN|style=Feynman)的小幅[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，余弦形状的山谷看起来非常像一个简单的抛物线。在物理学中，势能是二次方的系统是一个谐振子。那么，简单谐振子的电气等效物是什么呢？是[电感](@keyword=inductance|lang=zh-CN|style=Feynman)！

对于小电流和相位（$\sin(\phi) \approx \phi$），两个约瑟夫森关系可以结合起来，得到$V = L_J \frac{dI}{dt}$，其中$L_J = \frac{\hbar}{2eI_c}$ [@problem_id:1214615]。这是电感的定义。所以，这个奇怪的量子器件，在适当的条件下，其行为就像一个线圈。这种**约瑟夫森[电感](@keyword=inductance|lang=zh-CN|style=Feynman)**不仅仅是一个类比；它是一种真实效应，使得这些结可以用于高频电路。

但故事还有更精彩的部分。它不仅仅是一个[经典谐振子](@keyword=classical_harmonic_oscillator|lang=zh-CN|style=Feynman)；它是一个*量子*谐振子。这意味着它的能级是量子化的——它们只能取离散的值。[搓板势](@keyword=washboard_potential|lang=zh-CN|style=Feynman)阱内的这些[量子化能级](@keyword=quantized_energy_levels|lang=zh-CN|style=Feynman)是构建[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)（**qubit**）的魔力成分。最低能级（[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)）可以代表[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的$|0\rangle$态，而上一级能级（第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)）可以作为其$|1\rangle$态。

然而，要构建一个好的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，我们面临一个量子难题。结的行为由两种能量的竞争决定[@problem_id:1785345]。一种是[约瑟夫森能量](@keyword=josephson_energy|lang=zh-CN|style=Feynman)$E_J$，正如我们所见，它创造了想要束缚*相位*$\phi$的[搓板势](@keyword=washboard_potential|lang=zh-CN|style=Feynman)。另一种是**[充电能](@keyword=charging_energy|lang=zh-CN|style=Feynman)量**$E_C = (2e)^2/(2C)$，这是在结的电容$C$上增加一个[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)所需的静电能量成本。[充电能](@keyword=charging_energy|lang=zh-CN|style=Feynman)量偏好具有确定*数量*[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的状态。相位和数量是[共轭变量](@keyword=conjugate_variables|lang=zh-CN|style=Feynman)，就像位置和动量一样——由于不确定性原理，它们不能同时被精确定义。要构建一个**相位[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)**，其状态由其在相位势中的位置定义，我们需要相位是一个明确定义的量。这要求[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)足够深，可以容纳许多不同的量子能级，这个条件在[约瑟夫森能量](@keyword=josephson_energy|lang=zh-CN|style=Feynman)远大于[充电能](@keyword=charging_energy|lang=zh-CN|style=Feynman)量时得到满足：$E_J \gg E_C$。通过精心设计这个比率，科学家可以设计出处于所需量子区域的结。

### 现实世界中的[相干性](@keyword=coherence|lang=zh-CN|style=Feynman)：[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)和[热噪声](@keyword=johnson_nyquist_noise|lang=zh-CN|style=Feynman)

当我们将结构建成电路时，这种相干性的真正力量就显现出来了。如果我们将两个结放在一个[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)路中，我们就创造了一个**[超导量子干涉仪](@keyword=superconducting_quantum_interference_devices|lang=zh-CN|style=Feynman)**（**[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)**）。量子力学的规则要求，围绕任何闭合[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)路累积的总相位必须是$2\pi$的整数倍。这意味着穿过环路中心的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)会在两条路径之间产生[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman)，从而迫使两个结上的相位之间形成特定的关系。这种干涉效应以一种精确周期性的方式调制设备的总[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)：$I_{max} = 2I_c |\cos(\pi \Phi_{ext}/\Phi_0)|$，其中$\Phi_0$是磁通量子[@problem_id:1812702]。设备的电流对磁通量变得极其敏感，每当有一个[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)穿过环路时，它就会闪烁开关。这使得SQUID成为已知的最灵敏的磁力计，能够探测到人脑产生的微弱[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。

然而，这种美丽的量子之舞是脆弱的。世界是一个充满噪声的地方，热能是主要的破坏者。[热涨落](@keyword=thermal_fluctuations|lang=zh-CN|style=Feynman)就像对搓板的随机摇晃。如果热能$k_B T$与[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)的深度$E_J$相当，相位就可能被随机地从一个山谷踢到另一个，从而破坏相干行为[@problem_id:1806355]。为了保护这种脆弱的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)和[超导量子比特](@keyword=superconducting_qubits|lang=zh-CN|style=Feynman)必须在极低的温度下运行，放置在仅比绝对零度高出零点几度的低温恒温器中。构建[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的斗争，在很多方面，就是一场保护这种优雅的、微观的相位之舞免受温暖的、经典世界的混乱扰动的战斗。