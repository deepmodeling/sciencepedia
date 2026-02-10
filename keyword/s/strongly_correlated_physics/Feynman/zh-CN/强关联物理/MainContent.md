## 引言
在许多简单金属中，电子几乎可以自由移动，在广阔的导电海洋中，它们之间的相互排斥只是一个微不足道的细节。这就是[独立电子近似](@keyword=independent_electron_approximation|lang=zh-CN|style=Feynman)所描绘的世界。但是，当电子拥挤在一起，被迫发生强相互作用时，会发生什么呢？它们再也不能被视为独立的个体；它们的集体行为催生了一个奇异而迷人的新现实。这就是[强关联物理](@keyword=strongly_correlated_physics|lang=zh-CN|style=Feynman)的领域，在这里，简单的规则被打破，并导致了挑战传统理解的现象。本文旨在填补简单模型留下的知识空白，探索当[电子-电子相互作用](@keyword=electron_electron_interactions|lang=zh-CN|style=Feynman)占据主导地位时会发生什么。

接下来的章节将引导您踏上进入这个复杂世界的思想探险。首先，在“原理与机制”一章中，我们将探讨基本概念，例如独立电[子图](@keyword=subgraph|lang=zh-CN|style=Feynman)像为何失效，以及纯粹的排斥作用如何出人意料地产生磁性。我们还将审视决定材料最终命运的各种竞争性量子效应之间的激烈对决。随后，“应用与跨学科联系”一章将展示这些原理如何解决真实材料中长期存在的谜题，如何使我们能够构建人工量子系统，并在物理学、化学和计算机科学之间建立起强大的联系。

## 原理与机制

想象一个挤满舞者的舞厅。如果舞厅非常宽敞，舞者很少，他们每个人都可以自由地跳着华尔兹，几乎不用在意他人。这就是像铜这样的典型金属中电子的简单而美丽的图景。电子，也就是我们的舞者，形成一片“海洋”，在[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中滑行，基本上忽略了它们之间的相互排斥。这就是**[独立电子近似](@keyword=independent_electron_approximation|lang=zh-CN|style=Feynman)**，对于许多材料来说，它非常有效。但是，如果我们缩小舞厅或让舞厅里挤满舞者，会发生什么呢？他们开始相互碰撞。他们再也无法保持独立。他们的舞蹈变成了一场复杂的集体编舞，充满了错综复杂的互动。这就是**[强关联物理](@keyword=strongly_correlated_physics|lang=zh-CN|style=Feynman)**的世界。

### 独立电子图像的失效

在电子的量子世界里，竞争存在于两种基本趋势之间。一方面，动能促使[电子离域](@keyword=electron_delocalization|lang=zh-CN|style=Feynman)，将其[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)扩展到整个晶体。可以把这想象成舞者们想要利用整个舞池的愿望。这个过程的能量标度是**带宽**，我们可以称之为 $W$。另一方面，两个电子之间强大的库仑排斥使得它们占据同一个小空间（例如同一个原子）在能量上代价高昂。这就是在位排斥能，$U$。

电子的命运取决于无量纲比值 $U/W$ [@problem_id:2861965]。

-   当 $U/W \ll 1$ 时，动能获胜。电子具有高迁移率，它们之间的排斥作用只是一个小麻烦，独立电子图像依然成立。我们称这类系统为**弱关联**系统。

-   当 $U/W \gtrsim 1$ 时，库仑排斥占主导地位。两个电子处于同一原子位置的能量代价如此之高，以至于它们的运动受到极大阻碍。独立电子图像完全失效。在这里，我们进入了**强关联系统**这个迷人而奇异的领域。在这种情况下，电子的集体行为催生了从单个孤立电子的角度来看无法想象的现象。这场舞蹈变成了一场复杂的、纠缠的表演，每个舞者的动作都与所有其他舞者紧密相连。

这种集体舞蹈的首个也是最令人震惊的后果之一，体现在那些根据所有简单计算都应该是闪亮金属，但实际上却是绝缘体的材料中。在所谓的**[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)**中，半填充（每个原子一个电子）状态下的电子被锁定在原位。这并非因为没有可供移动的空余能态，而是因为移动到相邻位置将意味着双重占据该位置，从而招致巨大的能量惩罚 $U$。由排斥造成的交通堵塞，将一个本应是金属的材料变成了绝缘体。

### 排斥作用的意外创造：磁性

所以，电子被困住了，因它们之间的相互厌恶而动弹不得。但它们并未完全冻结。每个电子都拥有一个内在的量子属性：自旋。你可以把它想象成一个微小的陀螺，可以指向“上”或“下”。虽然电子的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)是局域的，但它们的自旋仍然可以相互通信。如何实现呢？通过一种被称为**虚过程**的精妙量子力学技巧。

想象两个相邻的位置，每个位置都被一个电子占据。一个电子可以在瞬间从真空中“借用”一个量级为 $U$ 的能量（得益于[海森堡不确定性原理](@keyword=heisenberg_s_uncertainty_principle|lang=zh-CN|style=Feynman)），然后跳到邻近的位置上，形成一个双占据位点。这个高能态是“虚”的，因为它无法持久；电子必须几乎立即跳回，偿还其能量债务。这次短暂过程的[持续时间](@keyword=holding_times|lang=zh-CN|style=Feynman)非常微小，量级为 $\Delta t \approx \hbar/U$ [@problem_id:3020842]。

现在，奇妙之处来了。让我们用一个简单的双位点模型，一个“Hubbard 二聚体”，来考虑这两个相邻电子的自旋 [@problem_id:1263650]。

-   如果两个电子具有**反平行自旋**（一个向上，一个向下），这个虚[跳跃过程](@keyword=jump_processes|lang=zh-CN|style=Feynman)是允许的。电子可以跳到相邻位点再跳回来。事实证明，与它们仅仅停留在原位相比，这次短暂进入高能态的“出游”实际上*降低*了双电子系统的总能量。

-   如果两个电子具有**平行自旋**（都向上或都向下），[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)禁止它们处于同一位点。虚跳跃被完全阻止。这种构型的能量不受影响。

令人震惊的结果是，具有反平行自旋的态的能量低于具有平行自旋的态。系统因此倾向于让相邻的自旋指向相反的方向。这是一种有效的磁相互作用，一种**反铁磁**耦合，它并非源于任何基本的磁力，而纯粹是由动能和[库仑排斥](@keyword=coulomb_repulsion|lang=zh-CN|style=Feynman)产生的！这种机制被称为**[超交换作用](@keyword=superexchange_interaction|lang=zh-CN|style=Feynman)**。这种涌现出的磁[耦合强度](@keyword=coupling_strength|lang=zh-CN|style=Feynman) $J$ 近似为 $J = 4t^2/U$，其中 $t$ 是与带宽 $W$ 相关的跳跃振幅。在大自然的一次深刻转折中，排斥作用创造了一种吸引形式——对特定自旋排列的能量偏好。

### 巨头对决：近藤 vs. RKKY

当我们考虑含有两种不同类型电子的材料时，情况变得更加复杂：一类是轻的、巡游的“导电”电子[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)，另一类是具有强磁矩的局域电子阵列，例如[稀土元素](@keyword=rare_earth_elements_2|lang=zh-CN|style=Feynman)的 $f$ 轨道电子。这就是**[近藤晶格](@keyword=kondo_lattice|lang=zh-CN|style=Feynman)模型**的设定 [@problem_id:3018897]，它为两种相互竞争的有序原理之间的激烈对决搭建了舞台。

一方是 **[Ruderman-Kittel-Kasuya-Yosida](@keyword=ruderman_kittel_kasuya_yosida|lang=zh-CN|style=Feynman) (RKKY) 相互作用**。一个局域磁矩与[导电电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)海洋相互作用，使其附近的[电子自旋](@keyword=electron_spin|lang=zh-CN|style=Feynman)极化。这种自旋极化不是局域的；它像池塘中的涟漪一样在电子海洋中传播。当这个涟漪到达另一个遥远的局域磁矩时，它会影响后者的取向。这就在局域磁矩之间产生了一种由导电电子介导的、有效的[长程相互作用](@keyword=long_range_interactions|lang=zh-CN|style=Feynman)。RKKY 相互作用试图将所有[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)锁定在一个集体的磁有序态中，例如反铁磁态。这种相互作用的特征能量标度，我们称之为 $T_{\mathrm{RKKY}}$，它随着底层的[交换耦合](@keyword=exchange_coupling|lang=zh-CN|style=Feynman) $J$ 以[幂律](@keyword=power_laws|lang=zh-CN|style=Feynman)形式增长：$T_{\mathrm{RKKY}} \propto J^2$ [@problem_id:2998371]。

另一方是**[近藤效应](@keyword=kondo_effect|lang=zh-CN|style=Feynman)**。这是一个更内在、更局域的过程。单个局域磁矩不与其他磁矩通信，而是与周围的[导电电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)纠缠在一起，捕获一个电子形成量子力学的自旋单态。在这种单态中，局域磁矩的自旋被屏蔽它的[导电电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)的集体自旋完美抵消。该[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)实际上从磁性景观中消失了——它被“屏蔽”或“[淬灭](@keyword=quenching|lang=zh-CN|style=Feynman)”了。这是一个微妙的[多体效应](@keyword=many_body_effects|lang=zh-CN|style=Feynman)，具有一个特征能量标度，即[近藤温度](@keyword=kondo_temperature|lang=zh-CN|style=Feynman) $T_K$，它*指数地*依赖于耦合强度：$T_K \propto \exp(-1/(J\rho_0))$，其中 $\rho_0$ 是导电电子的态密度 [@problem_id:2998371]。

材料的命运取决于这场对决的结果。$T_{\mathrm{RKKY}}$ 和 $T_K$ 哪个更强？正如 Doniach 最初所概述的，答案关键取决于 $J$ 的值 [@problem_id:3018897]。

-   对于**小的 $J$**，RKKY 相互作用的幂律依赖关系 ($J^2$) 超过了指数级小的近藤标度。RKKY 相互作用获胜，系统在低温下发生磁有序。

-   对于**大的 $J$**，近藤标度的指数依赖关系比任何[幂律](@keyword=power_laws|lang=zh-CN|style=Feynman)增长得都快得多。[近藤效应](@keyword=kondo_effect|lang=zh-CN|style=Feynman)大获全胜。每个局域磁矩都被单独屏蔽和[淬灭](@keyword=quenching|lang=zh-CN|style=Feynman)，系统变成一个非磁性金属。

这种竞争可以在一个[临界耦合](@keyword=critical_coupling|lang=zh-CN|style=Feynman) $J_c$ 处导致一个零温**量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)**，从而将磁有序相与一个新颖的顺磁性金属[相分离](@keyword=phase_separation|lang=zh-CN|style=Feynman)开来。

### 奇异新粒子的诞生

当近藤效应赢得对决时，所产生的金属绝非寻常。屏蔽过程不仅使磁矩消失，它还从根本上改变了[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)载流子。局域的 $f$-电子及其专属的[导电电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)屏蔽云结合在一起，形成一个全新的复合体：一个**[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)**。而这个[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)异常迟缓。

这催生了**重费米子**材料。在低温[相干态](@keyword=coherent_states|lang=zh-CN|style=Feynman)下，现已变为巡游的 $f$-电子与宽的[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)杂化，在[费米能](@keyword=fermi_energy|lang=zh-CN|style=Feynman)量处形成一个新的、非常窄的电子[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)。固态物理学的一个基本结果告诉我们，粒子的有效质量 $m^*$ 与其[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的曲率成反比。一个非常平坦的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)意味着非常小的曲率，这也就意味着一个真正巨大的有效质量 [@problem_id:2986264]。这些材料中的[准粒子有效质量](@keyword=quasiparticle_effective_mass|lang=zh-CN|style=Feynman)可以达到裸电子质量的数百甚至数千倍。就好像电子变成了微小的铅粒。这种显著的质量增强不仅是理论上的好奇之物，它在材料的[低温比热](@keyword=low_temperature_specific_heat|lang=zh-CN|style=Feynman)中被直接观测为一个巨大的峰，其线性系数 $\gamma$ 与[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman) $m^*$ 直接成正比 [@problem_id:2986264]。

这一转变带来了一个深刻的后果，它被一个称为 **Luttinger 定理**的深刻结果所捕捉。该定理指出，费米面的体积——即在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中分隔已占据和未占据电子态的边界——由载流[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)的总数确定 [@problem_id:3018914]。在磁性态中，$f$-电子是[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)，它们不被算作载流子。系统拥有一个由导电电子数量决定的“小”费米面。但在[重费米子](@keyword=heavy_fermion|lang=zh-CN|style=Feynman)态中，$f$-电子已经变得巡游；它们现在是[带电费米液体](@keyword=charged_fermi_liquid|lang=zh-CN|style=Feynman)的一部分！它们必须被计入总数。这意味着[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)必须突然增大为一个“大”费米面，其体积同时包含了[导电电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)和 $f$-电子。

在分隔这两个态的[量子临界点](@keyword=quantum_critical_point|lang=zh-CN|style=Feynman)上究竟发生了什么？系统必须以某种方式处理其[费米面体积](@keyword=fermi_surface_volume|lang=zh-CN|style=Feynman)的不连续跳跃。一个正常的金属态（“费米液体”）无法做到这一点。自然界解决这个悖论的唯一方法就是让[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)这个概念本身瓦解。在[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)溶解成一锅混沌的、[强相互作用](@keyword=strong_nuclear_force|lang=zh-CN|style=Feynman)的汤。这就是**[非费米液体](@keyword=non_fermi_liquids|lang=zh-CN|style=Feynman)**，一种真正奇异的量子物质状态，其性质挑战了我们对金属的标准描述 [@problem_id:3007632]。

新粒子和新相的涌现是一个贯穿始终的主题。在[一维系统](@keyword=one_dimensional_systems|lang=zh-CN|style=Feynman)中，这种瓦解甚至更为剧烈。一个[电子激发](@keyword=electronic_promotion|lang=zh-CN|style=Feynman)可以真正地分解成两个独立的实体：一个携带电子[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)但没有自旋的**空穴子**（holon），以及一个携带自旋但[电中性](@keyword=charge_neutrality|lang=zh-CN|style=Feynman)的**[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)**（spinon）[@problem_id:3006193]。这种被称为**[自旋-电荷分离](@keyword=spin_charge_separation|lang=zh-CN|style=Feynman)**的现象是强关联最引人注目的表现之一。

从简单的电子交通堵塞开始，一个全新的现象宇宙涌现而出：源于排斥的磁性、重塑物质[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的对决、重如原子的粒子，以及电子本身的瓦解。这就是[强关联物理](@keyword=strongly_correlated_physics|lang=zh-CN|style=Feynman)的思想探险，在这里，整体不仅大于部分之和，而且与部分之和有着本质的不同。