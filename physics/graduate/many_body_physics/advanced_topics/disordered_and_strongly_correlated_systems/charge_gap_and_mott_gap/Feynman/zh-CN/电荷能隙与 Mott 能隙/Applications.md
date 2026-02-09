## 应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系

现在，我们已经费尽心力地构建了理解[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)的理论框架，是时候推开大门，看看它如何与真实世界联系起来了。这个看似抽象的“电子卡壳”概念，真的能*解释*任何现象吗？正如我们将要看到的，答案是响亮的“能”。从一块材料如何响应挤压，到它如何传导热量和电流，甚至到在扭曲的碳片中发现的革命性新物理，[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)并非一个理论上的奇珍，而是现代[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)故事中的核心角色。

故事的起点在于区分不同类型的材料。我们知道，有些材料是导体，有些是绝缘体。但为什么会这样？通常，我们会想到所谓的能带理论——一个完美的单粒[子图](@keyword=subgraph|lang=zh-CN|style=Feynman)像，它在解释简单[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)等方面非常成功。然而，当电子之间的相互作用变得不可忽视时，这个简单的图像就崩溃了。如果我们将一个系统中电子之间的在位库伦排斥能 $U$ 与其动能（由带宽 $W$ 表征）进行比较，我们会发现物理学的面貌会根据 $U/W$ 这个比率发生戏剧性的变化。当 $U/W$ 很小时，我们处于**弱关联**区域，[能带理论](@keyword=electronic_band_theory|lang=zh-CN|style=Feynman)大致成立。但当 $U/W \gtrsim 1$ 时，我们就进入了**强关联**的奇异世界，[莫特物理](@keyword=mott_physics|lang=zh-CN|style=Feynman)学正是这个世界的主角 [@problem_id:2861965]。在这一章，我们将探索这个世界的广阔疆域。

### 确凿的指纹：我们如何知道它的存在？

一个理论，无论多么优美，如果不能在实验上被证实，终究只是空中楼阁。那么，我们如何才能在实验室里“看到”[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)呢？答案在于寻找它留下的、无法被其他理论解释的独特“指纹”。

#### [热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)指纹：电子可压缩性

想象一下，你试图将更多的电子“挤入”一个材料中。在普通金属中，这相对容易，因为在费米能级附近有大量的可用态。但在一个有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的系统中，情况就大为不同了。[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)意味着，在[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)下，增加或移除一个电子需要克服一个有限的能量势垒。

因此，在零温下，如果你稍微改变化学势（这相当于改变了挤入电子的“意愿”），只要这个改变不足以跨越[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，系统中的电子数密度 $n$ 就不会发生任何变化。电子[可压缩性](@keyword=compressibility|lang=zh-CN|style=Feynman)的定义是 $\kappa = \frac{1}{n^2} \frac{\partial n}{\partial \mu}$。既然 $\frac{\partial n}{\partial \mu} = 0$，那么[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)的电子[可压缩性](@keyword=compressibility|lang=zh-CN|style=Feynman)在零温下严格为零 [@problem_id:1108422]。这个系统在电学上是“不可压缩的”！

当然，世界并非处于零温。当温度 $T > 0$ 时，热量可以“激活”一些电子，使它们跃过[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。因此，可压缩性不再是零，但它会受到[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的强烈抑制，其大小与 $\exp(-\Delta / (2k_B T))$ 成正比，其中 $\Delta$ 是[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的大小 [@problem_id:1108375]。通过测量[可压缩性](@keyword=compressibility|lang=zh-CN|style=Feynman)随温度的变化，物理学家就可以像侦探一样，推断出隐藏在材料内部的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)大小。

#### 光谱与输运指纹：与金属的鲜明对比

莫特绝缘体与金属之间的区别是根本性的。我们可以通过一系列实验探针来揭示这些差异 [@problem_id:2974434]。
- **导电性**：金属在零频下有完美的导电性，这体现为一个有限的**[德鲁德权重](@keyword=drude_weight|lang=zh-CN|style=Feynman)** $D > 0$。而[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)是绝缘的，其[德鲁德权重](@keyword=drude_weight|lang=zh-CN|style=Feynman) $D=0$。
- **可压缩性**：如上所述，金属是可压缩的 ($\kappa > 0$)，而[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)在低温下是不可压缩的 ($\kappa \approx 0$)。
- **单粒子谱函数 $A(\mathbf{k}, \omega)$**：这是最直接的证据。对于金属，[谱函数](@keyword=spectral_function|lang=zh-CN|style=Feynman)在费米能级 ($\omega=0$) 附近显示一个尖锐的“[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)峰”，其权重为 $Z$。而对于[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)，[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)峰完全消失 ($Z=0$)，[谱函数](@keyword=spectral_function|lang=zh-CN|style=Feynman)在 $\omega=0$ 处打开一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，所有[谱权重](@keyword=spectral_weight|lang=zh-CN|style=Feynman)都被推到高能量的上哈勃带和低能量的下哈勃带中。

用光照射材料是另一种强大的探测手段。[光子](@keyword=photon|lang=zh-CN|style=Feynman)的吸收与材料的光学[电导率](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman) $\sigma_1(\omega)$ 直接相关。对于[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)，只有当光子能量 $\hbar\omega$ 大于或等于[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman) $\Delta$ 时，电子才能被激发，从而吸收[光子](@keyword=photon|lang=zh-CN|style=Feynman)。因此，光学电导率在 $\omega  \Delta/\hbar$ 的频率范围内为零，并在 $\Delta/\hbar$ 处出现一个吸收边。有趣的是，通过对光学电导率的积分，我们甚至可以反推出系统中电子动能的平均值，这为我们提供了一个连接宏观光学响应与微观量子力学的窗口 [@problem_id:1108435]。

然而，事情还有一个微妙之处。“[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)”这个词其实有多种含义，这取决于你如何去测量它 [@problem_id:3006241]。
- **输运[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta_{\mathrm{tr}}$**：通过测量电阻随温度的变化（激活行为）推断出的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。它通常与创建一对自由载流子（[电子和空穴](@keyword=electrons_and_holes|lang=zh-CN|style=Feynman)）所需能量的一半有关，即 $\Delta_{\mathrm{tr}} \approx \Delta_c/2$，其中 $\Delta_c$ 是基础的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。
- **光学[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta_{\mathrm{opt}}$**：通过光学吸收测量的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。这对应于用一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)产生一个束缚在一起的[电子-空穴对](@keyword=electron_hole_pair|lang=zh-CN|style=Feynman)（激子）。由于[激子束缚能](@keyword=exciton_binding_energy|lang=zh-CN|style=Feynman)的存在，光学[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)通常略小于真正的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta_c$。
- **单粒子[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta_{\mathrm{sp}}$**：通过光电子能谱（PES）和逆光[电子能谱](@keyword=electron_energy_spectrum|lang=zh-CN|style=Feynman)（IPES）直接测量的、移除一个电子和添加一个电子所需能量的差值。这最接近于我们理论上定义的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta_c$。
理解这三者之间的区别至关重要，它提醒我们，每一次“测量”都是对系统的一次特定方式的“提问”，而不同的问题自然会得到不完全相同的答案。

### 并非孤军奋战：如何区分[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)

自然界充满了各种机制，它们都可能导致材料绝缘。证明一种材料是[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)，不仅需要找到“莫特”的证据，还需要排除其他可能性。

#### 莫特 vs. 派尔斯（Peierls）

派尔斯绝缘体是电子与晶格振动（[声子](@keyword=phonons|lang=zh-CN|style=Feynman)）耦合的产物。在[一维链](@keyword=one_dimensional_chains|lang=zh-CN|style=Feynman)中，[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)发生周期性畸变（二聚化），使得[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)加倍，从而在费米能级处打开一个能带隙。这与莫特机制截然不同。
- **驱动力**：派尔斯是**电子-[声子](@keyword=phonons|lang=zh-CN|style=Feynman)**相互作用；莫特是**电子-电子**相互作用。
- **对称性**：派尔斯绝缘体打破了[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的[平移对称性](@keyword=translational_symmetry|lang=zh-CN|style=Feynman)，可以通过[X射线衍射](@keyword=x_ray_diffraction|lang=zh-CN|style=Feynman)等手段观测到新的“[超晶格](@keyword=superlattices|lang=zh-CN|style=Feynman)”峰。而莫特绝缘体（在最纯粹的形式下）不破坏任何空间对称性。
- **自旋激发**：这是最关键的区别之一。在一维情况下，派尔斯[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)同时作用于[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)和自旋，因此自旋激发是**有隙的**。而[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)只束缚了[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，自旋自由度依然存在，形成所谓的“[自旋液体](@keyword=spin_liquids|lang=zh-CN|style=Feynman)”，其自旋激发是**无隙的**。

因此，一个决定性的实验是同时进行衍射和磁化率测量。如果在材料中没有观测到[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)畸变，并且在低温下[磁化率](@keyword=susceptibility|lang=zh-CN|style=Feynman)保持有限值（表明存在无隙的自旋激发），那么我们就有了强有力的证据证明它是一个莫特绝缘体，而非派尔斯绝缘体。[共轭聚合物](@keyword=conjugated_polymers|lang=zh-CN|style=Feynman)等材料正是研究这两种机制竞争的理想平台 [@problem_id:2996695] [@problem_id:2910336]。

#### 莫特 vs. 安德森（Anderson）

[安德森绝缘体](@keyword=anderson_insulator|lang=zh-CN|style=Feynman)完全是另一回事。它源于**无序**。当[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中的势场非常混乱时，电子波的量子干涉效应会导致电子被“局域”在空间的某个小区域内，无法长程传输，从而导致绝缘。
- **驱动力**：安德森是**无序**；莫特是**相互作用**。
- **[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)**：莫特绝缘体在[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)处有一个“硬”的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)为零。而[安德森绝缘体](@keyword=anderson_insulator|lang=zh-CN|style=Feynman)可以没有真正的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，其[费米能级处的态密度](@keyword=density_of_states_at_the_fermi_level|lang=zh-CN|style=Feynman)可以为有限值，只是所有这些态都是局域的。
- **输运**：两者在低温下的导电机制也不同。[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)表现为[热激活](@keyword=thermal_activation|lang=zh-CN|style=Feynman)行为，而[安德森绝缘体](@keyword=anderson_insulator|lang=zh-CN|style=Feynman)则遵循所谓的“[变程跳跃](@keyword=variable_range_hopping|lang=zh-CN|style=Feynman)”导电，其电导率与温度的关系更为复杂 [@problem_id:2800117]。

#### 莫特 vs. 斯莱特（Slater）

这是一个更为精妙的区分。斯莱特绝缘体也是由电子相互作用驱动的，但它的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)直接来源于**磁有序**（通常是反铁磁有序）。磁有序使得晶胞加倍，类似于派尔斯机制，从而打开[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。而莫特绝缘体，正如我们所强调的，其[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的存在并不以磁有序为前提。动态[平均场理论](@keyword=mean_field_theory|lang=zh-CN|style=Feynman)（DMFT）等现代[多体理论](@keyword=many_body_theory|lang=zh-CN|style=Feynman)的一个伟大成就，就是清晰地展示了即使在强制保持系统为顺磁性的情况下，只要相互作用足够强，一个纯粹由关联驱动的[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)依然可以打开 [@problem_id:3006185]。这突显了[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)作为一种独特的、纯粹的量子多体现象的本质。

### 广阔的宇宙：[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科的联系

[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)的概念并非象牙塔里的玩物，它的触角延伸到了物理、化学和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)的许多分支。

- **高压物理学**：压力是调控材料性质的强大工具。对[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)施加压力，会使原子间距变小，电子[波函数重叠](@keyword=wavefunction_overlap|lang=zh-CN|style=Feynman)增加，从而增大了动能项中的跳跃积分 $t$。当压力足够大时，$t$ 的增大会使得系统的 $U/W$ 比率减小，最终可以关闭[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)，使材料从绝缘体转变为金属。这种由压力驱动的“绝缘体-金属转变”是凝聚态物理中的一个核心现象，对于理解地球和行星内部等极端条件下的[物质状态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)至关重要 [@problem_id:1108423] [@problem_id:1108390]。

- **[热电学](@keyword=thermoelectrics|lang=zh-CN|style=Feynman)**：[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)在热电[能量转换](@keyword=energy_conversion|lang=zh-CN|style=Feynman)方面也显示出有趣的潜力。塞贝克（Seebeck）效应描述了温差如何产生电压。在高温下，[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)中的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)载流子（空穴和双占位电子）具有很高的构型熵。这导致了巨大的塞贝克系数，其数值直接与[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman) $\Delta$ 相关。一个简单的模型甚至给出了一个优美的关系式：$S \cdot T = -\Delta/(2e)$ [@problem_id:1108432]。

- **[晶格动力学](@keyword=crystal_lattice_dynamics|lang=zh-CN|style=Feynman)**：真实的电子并非在僵硬的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中运动，它们会与[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)（[声子](@keyword=phonons|lang=zh-CN|style=Feynman)）“对话”。当一个电子移动时，它会吸引周围的正离子，使[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)发生畸变，就像一个人走在柔软的床垫上。这个被[声子](@keyword=phonons|lang=zh-CN|style=Feynman)云“装饰”起来的电子被称为“[极化子](@keyword=polarons|lang=zh-CN|style=Feynman)”。这种[电子-声子耦合](@keyword=electron_phonon_coupling|lang=zh-CN|style=Feynman)会有效地改变电子之间的相互作用，从而对[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)的大小进行[重整化](@keyword=renormalization|lang=zh-CN|style=Feynman)。例如，它可能会减小打开[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)所需的能量，其减小量与耦合常数 $g$ 和[声子](@keyword=phonons|lang=zh-CN|style=Feynman)频率 $\omega_E$ 有关，修正项可表示为 $-2g^2/(\hbar\omega_E)$ [@problem_id:1108381]。

- **电子学**：任何绝缘体都有其极限。如果在一个[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)两端施加一个足够强的电场，这个电场最终会把电子从下哈勃带中“撕扯”出来，通过量子隧穿效应跃迁到上哈勃带，从而导致绝缘体的击穿。这种现象类似于[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)中的[齐纳击穿](@keyword=zener_breakdown|lang=zh-CN|style=Feynman)，其[临界电场](@keyword=critical_electric_field|lang=zh-CN|style=Feynman) $E_c$ 大小与[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta$ 的平方成正比 [@problem_id:1108394]。

### 现代前沿：激动人心的新发现

[莫特物理](@keyword=mott_physics|lang=zh-CN|style=Feynman)学远未终结，它正处在一系列激动人心的现代研究的中心。

- **掺杂[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)与高温超导**：如果从一个半满的莫特绝缘体中拿走或添加少量电子（即“掺杂”），会发生什么？系统不会像普通[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)那样简单地变成导体，而是会变成一种非常奇特的金属。原来的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)被“填充”，在费米能级处出现一个极其狭窄的、权重正比于[掺杂浓度](@keyword=doping_concentration|lang=zh-CN|style=Feynman) $\delta$ 的“[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)峰”，而大部分[谱权重](@keyword=spectral_weight|lang=zh-CN|style=Feynman)仍然留在高能量的哈勃带中。这种“[谱权重转移](@keyword=spectral_weight_transfer|lang=zh-CN|style=Feynman)”是[强关联物理](@keyword=strongly_correlated_physics|lang=zh-CN|style=Feynman)的核心特征 [@problem_id:2842807]。更重要的是，这个奇特的金属态正是铜基[高温超导体](@keyword=high_temperature_superconductors|lang=zh-CN|style=Feynman)的“母体”！理解掺杂莫特绝缘体，被认为是解开[高温超导](@keyword=high_temperature_superconductivity|lang=zh-CN|style=Feynman)之谜的关键一步。

- **转角电子学（Twistronics）**：近年来一个惊人的发现是，我们可以通过简单地将两层原子材料（如石墨烯）相互扭转一个微小的“[魔角](@keyword=magic_angle|lang=zh-CN|style=Feynman)”，来“凭空”创造出[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)。在这个[魔角](@keyword=magic_angle|lang=zh-CN|style=Feynman)下，电子的动[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)宽被极大地压平，使得相对较弱的电子相互作用 $U$ 也能轻易地主导物理，即 $U/W \gg 1$。通过扭转角度来调控带宽，为我们提供了一种前所未有的、精妙绝伦的方式来工程化电子关联效应 [@problem_id:1108461]。

- **[超快动力学](@keyword=ultrafast_dynamics|lang=zh-CN|style=Feynman)**：借助飞秒（$10^{-15}$秒）激光技术，物理学家现在可以进行“泵浦-探测”实验。他们可以用一束强激光（泵浦）在极短的时间内激发[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)，使其“熔化”成金属态，然后用另一束延迟的激光（探测）来“拍摄”这一过程。通过时间分辨的光电子能谱（tr-ARPES）等技术，我们几乎可以实时“观看”[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)的崩溃和重组 [@problem_id:2491185]。这为我们打开了一扇研究非[平衡态](@keyword=equilibrium_states|lang=zh-CN|style=Feynman)量子动力学的大门。

- **拓扑莫特绝缘体**：物理学的两大革命——[强关联物理](@keyword=strongly_correlated_physics|lang=zh-CN|style=Feynman)和拓扑物理——在这里相遇，催生了“拓扑[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)”这一前沿概念。想象一个系统，其中强大的相互作用使[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)完[全局域](@keyword=global_fields|lang=zh-CN|style=Feynman)，形成莫特绝缘体；但与此同时，系统中存在很强的[自旋-轨道耦合](@keyword=l_s_coupling|lang=zh-CN|style=Feynman)。这时，可能会发生一种奇特的“[电子分数化](@keyword=electron_fractionalization|lang=zh-CN|style=Feynman)”现象：电子分解为一个携带[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的“[电荷子](@keyword=holon|lang=zh-CN|style=Feynman)”和一个携带自旋的“[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)”。[电荷子](@keyword=holon|lang=zh-CN|style=Feynman)被锁定，但[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)可以在材料中自由运动，并形成一个具有非[平凡拓扑](@keyword=trivial_topology|lang=zh-CN|style=Feynman)性质的能带结构！其结果是，材料的体态是绝缘的，但在其边界上，会出现由[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)构成的、受拓扑保护的、无法被轻易破坏的导电边缘态。这些边缘态是电中性的，但可以传输自旋。这是[量子多体物理](@keyword=quantum_many_body_physics|lang=zh-CN|style=Feynman)与拓扑学结合产生的最迷人的景象之一 [@problem_id:2525967]。

从一个简单的图像——电子由于相互推挤而无法移动——出发，我们踏上了一段穿越凝聚态物理几乎所有重要领域的旅程。[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)不仅仅是一个“[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)”，它是一个窗口，透过它，我们窥见了量子多体世界深邃、奇异而又统一的内在之美。而这段旅程，还远未结束。