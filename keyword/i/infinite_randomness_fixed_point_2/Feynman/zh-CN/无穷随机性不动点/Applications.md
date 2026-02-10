## 应用与跨学科联系

我们花了一些时间学习一个特殊游戏的规则——[强无序重整化群](@keyword=strong_disorder_renormalization_group|lang=zh-CN|style=Feynman)。这确实是一个奇怪的游戏。我们在[量子自旋链](@keyword=quantum_spin_chain|lang=zh-CN|style=Feynman)中找到最强的键，将它们配对成一个沉静的单态，然后退后一步，看看它的邻居之间诞生了什么新的、更弱的相互作用。我们一步一步地重复这个过程，从高能端到低能端逐步削减系统的自由度。这是一个引人入胜的理论练习，但人们可能会公正地问：这有什么意义？这个抽象的过程与物质、粒子和能量的可触及世界有什么关系？

事实证明，答案是深远的。这个游戏不仅仅是游戏。它的规则支配着数量惊人的真实物理系统的行为，其结果——规则不可避免地导向的[不动点](@keyword=fixed_points|lang=zh-CN|style=Feynman)——描述了一些科学已知的最奇异的物质相。无穷随机性不动点不仅仅是一个数学上的奇趣之物；它是一个统一的原则，揭示了那些随机性不是待平均掉的麻烦，而是量子王国真正主宰的系统的秘密。现在让我们踏上一段旅程，看看这条兔子洞通向何方。

### [无序磁体](@keyword=disordered_magnets|lang=zh-CN|style=Feynman)中的低语

我们的第一站是许多这些思想诞生的地方：一个简单的一维[量子自旋链](@keyword=quantum_spin_chain|lang=zh-CN|style=Feynman)，每个自旋都试图与其邻居反平行[排列](@keyword=permutation|lang=zh-CN|style=Feynman)，但受到从一个键到另一个键随机变化的[相互作用强度](@keyword=interaction_strength|lang=zh-CN|style=Feynman)的阻碍。这就是随机反铁磁海森堡链。在可能的最低温度下，它的状态是什么？

一个传统的磁体要么会稳定在一个整齐的、交替的上-下-上-下模式（[长程有序](@keyword=long_range_order|lang=zh-CN|style=Feynman)），要么其关[联会](@keyword=synapsis|lang=zh-CN|style=Feynman)指数级快速衰减，仿佛它的记忆非常短暂。由无穷随机性不动点主导的系统两者都不是。它进入一个“[随机单态相](@keyword=random_singlet_phase|lang=zh-CN|style=Feynman)”。想象这些自旋是排成一队的人。有些人不是仅仅与他们的直接邻居交谈，而是与队伍中很远的一个伙伴形成了一个牢不可破的键——一个单态——完全忽略了中间的所有人。随着我们的SDRG过程抽取掉最强耦合的对，新的、更弱的、更长程的有效键被形成，导致了跨越所有可能长度尺度的单态层级结构。[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)是由这些嵌套的、长距离配对编织而成的复杂织锦。

这种奇怪的结构有两个显著的、可测量的后果。

首先，它拥有一种幽灵般的序。虽然没有重复的模式，但自旋方向的记忆丧失得异常缓慢。对于相距为$r$的两个自旋，其[无序平均](@keyword=disorder_averaging|lang=zh-CN|style=Feynman)的[自旋-自旋关联](@keyword=spin_spin_correlation|lang=zh-CN|style=Feynman)$C(r)$并非指数衰减，而是遵循一个普适的幂律：$C(r) \sim -r^{-\eta}$。RSRG分析揭示了一个优美而深刻的联系：发现长度为$L$的块体的总自旋平方均值随块体大小呈对数增长。一些数学推导表明，这种对数增长只有在关联以恰好为$\eta=2$的指数衰减时才可能实现。这不是一个近似；这是一个清晰、普适的预测。该系统的有序性超过液体，但比晶体更无序，处于一种“准[长程有序](@keyword=long_range_order|lang=zh-CN|style=Feynman)”的状态。

第二个，也许是最戏剧性的后果，是能量和长度之间的关系。这是“激活标度”的标志。在一个正常系统中，大小为$L$区[域的特征](@keyword=characteristic_of_a_field|lang=zh-CN|style=Feynman)[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)通常按[幂律](@keyword=power_laws|lang=zh-CN|style=Feynman)标度，如$E \sim L^{-z}$。但在这里，标度行为截然不同。要激发一个长度为$L$的区域，必须打破其中最弱的单态，这对应于一个能量标度$\Omega$。SDRG规则规定了两者之间一种奇异的关系：

$$
\ln\left( \frac{1}{\Omega} \right) \propto \sqrt{L}
$$

这个关系，以其[特征指数](@keyword=characteristic_exponent|lang=zh-CN|style=Feynman)$\psi = 1/2$为标志，是无穷随机性不动点的心跳。想想这意味着什么。将链的长度加倍，并不会使[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)减半；它会使逆[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的对数*平方*。能量标度以惊人的、超指数的速率骤降。这是一种极端的“[临界慢化](@keyword=critical_slowing_down|lang=zh-CN|style=Feynman)”。是什么导致了这种情况？在[不动点](@keyword=fixed_points|lang=zh-CN|style=Feynman)处，[键强度](@keyword=bond_strength|lang=zh-CN|style=Feynman)的分布并非在某个平均值附近呈峰值；它变得极其宽，跨越许多[数量级](@keyword=powers_of_ten|lang=zh-CN|style=Feynman)。这就是其名称中“无穷随机性”的由来。要找到一个大小为$L$的区域，你必须穿越一片由指数级弱的键组成的沙漠，这些键对应于指数级小的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。

### 完美的绝缘体：[多体局域化](@keyword=many_body_localization|lang=zh-CN|style=Feynman)

很长一段时间里，这种奇怪的激活标度被看作是某些一维量子磁体的特性。但我们现在相信，它是理解一个更广泛、更深刻现象的关键：一个封闭量子系统中[热化](@keyword=thermalization|lang=zh-CN|style=Feynman)的完全崩溃。

在物理学中，我们通常假设，如果你有一个复杂的、相互作用的系统，并让它独自演化，它最终会达到[热平衡](@keyword=thermal_balance|lang=zh-CN|style=Feynman)。它的各个部分会交换能量和信息，直到关于初始状态的所有记忆都丧失，其性质可以由一个单一的数字来描述：它的温度。这个原则被称为本征态热化假说（ETH）。

但如果一个系统*永远*不热化呢？如果它永远冻结在一个记住其特定起源的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)中呢？这就是**[多体局域化](@keyword=many_body_localization|lang=zh-CN|style=Feynman)（MBL）**的现象。在强无序和量子相互作用同时存在的情况下，一个系统可以转变为终极绝缘体。不仅仅是[导电性](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)差，而是[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)和[能量输运](@keyword=energy_transport|lang=zh-CN|style=Feynman)完全停止的完美绝缘体。

从[热化](@keyword=thermalization|lang=zh-CN|style=Feynman)（各态遍历的）相到MBL相的转变，现在被理解为由一个无穷随机性[不动点](@keyword=fixed_points|lang=zh-CN|style=Feynman)控制。我们刚才在[自旋链](@keyword=spin_chain|lang=zh-CN|style=Feynman)中遇到的所有奇异现象都汹涌回归，但现在具有更广泛的意义。
- **消失的输运**: 激活标度$\ln(1/\text{time}) \propto \sqrt{\text{length}}$，意味着跨越距离$L$传输信息需要指数级长的时间。这立即解释了为什么MBL相是具有零[直流电导率](@keyword=dc_electrical_conductivity|lang=zh-CN|style=Feynman)的完美绝缘体。
- **避免纠缠灾难**: 在一个[热化](@keyword=thermalization|lang=zh-CN|style=Feynman)系统中，量子纠缠像野火一样蔓延，迅速饱和到一个与其子系统大小成正比的“体积律”。在MBL相中，纠缠被驯服了。一个初始态的纠缠随时间仅呈对数级慢速增长，$S(t) \sim \ln(t)$，并且最终的[本征态](@keyword=eigenstates|lang=zh-CN|style=Feynman)表现出“面积律”纠缠，仿佛它们是简单的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)，而不是高度[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)。
- **量子混沌的崩溃**: 热化系统的能级是“混沌的”；它们相互排斥，遵循随机矩阵理论的预测。在MBL相中，这种排斥消失了。能级变得不相关，仿佛它们属于一个简单的、无相互作用的系统，遵循[泊松统计](@keyword=poissonian_statistics|lang=zh-CN|style=Feynman)。

MBL相是一种真正的物质相，与液体或固体截然不同，而无穷随机性[不动点](@keyword=fixed_points|lang=zh-CN|style=Feynman)为描述其性质以及向该相的[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)提供了普适框架。

### 在实验室中探测混沌的边缘

这些不仅仅是理论家的幻想。无穷随机性物理学的奇异预测正在前沿实验中接受检验。

最有前途的平台之一是**[超冷原子](@keyword=ultracold_atoms|lang=zh-CN|style=Feynman)**。通过将原子云捕获在由激光构成的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中，物理学家可以近乎完美地实现像无序[玻色-哈伯德模型](@keyword=bose_hubbard_model|lang=zh-CN|style=Feynman)这样的模型。这个系统可以以超流体的形式存在，其中原子离域化并无阻力地流动，或者在强无序下，成为一个MBL绝缘体。无穷随机性理论对它们之间的转变做出了一个清晰、可检验的预测。[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)刚度$\rho_s$是扭曲超流体相位的能量成本的度量。它是一个宏观的、可测量的量。当系统向MBL转变调谐时，该理论预测$\rho_s$必须以一种非常特殊的方式消失，这种方式由激活标度决定：

$$
\rho_s \propto \exp\left( -\text{const.} \times |\delta|^{-\nu/2} \right)
$$

其中$\delta$是与[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)的距离，$\nu$是另一个普适指数。这个“[本性奇点](@keyword=essential_singularity|lang=zh-CN|style=Feynman)”是底层无穷随机性不动点的直接指纹，是抽象的[重整化群](@keyword=renormalization_group|lang=zh-CN|style=Feynman)过程与具体实验室测量之间惊人的联系。

这些思想的触角甚至延伸得更远，进入了**量子自旋液体**的神秘世界。这些物质状态中，[量子涨落](@keyword=quantum_fluctuations|lang=zh-CN|style=Feynman)如此之强，以至于即使在绝对零度，自旋也从不排序。[Kitaev蜂窝模型](@keyword=kitaev_honeycomb_model|lang=zh-CN|style=Feynman)是描述像$\alpha-\text{RuCl}_3$这样的材料的候选模型，就是这样一个例子。在其纯净形式中，它的激发行为像无质量的二维[狄拉克费米子](@keyword=dirac_fermions|lang=zh-CN|style=Feynman)。当你加入无序时会发生什么？人们可能[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)这种精巧的物理被摧毁。然而，它被转化了。无序在二维中产生了一种新型的无穷随机性不动点，这反过来又重塑了[能量景观](@keyword=energy_landscape|lang=zh-CN|style=Feynman)。态密度被预测出一种新的、非普适的对能量的幂律依赖关系，这是一个可以在谱学实验中寻找的迹象。

从一个简单的自旋链出发，我们已经来到了[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学、凝聚态和原子物理的前沿。强无序游戏的抽象规则为我们提供了一种强大的、统一的语言，来描述随机性主导的物质行为。这是一个优美的例证，说明在物理学中，一个单一的优雅思想如何能照亮一个广阔多样的景观，揭示出隐藏在无序核心深处的深刻联系和一种新的秩序。