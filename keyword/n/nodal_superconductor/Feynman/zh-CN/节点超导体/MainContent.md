## 引言
[非常规超导体](@keyword=unconventional_superconductors|lang=zh-CN|style=Feynman)的发现挑战了我们对材料如何无阻导电的既有理解。尽管基础的Bardeen-Cooper-Schrieffer (BCS) 理论通过均匀[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的概念完美地解释了常规超导，但它无法说明在这些更新、更复杂的材料中观察到的反常行为。其核心谜团在于它们的[电子结构](@keyword=electronic_structure|lang=zh-CN|style=Feynman)：什么样的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)会产生如此奇特的性质？本文通过引入[节点超导体](@keyword=nodal_superconductor|lang=zh-CN|style=Feynman)的概念来解决这个问题。在第一章 **原理与机制** 中，我们将探讨节点超导的理论框架，将各向异性、符号变化的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)与常规材料的简单各向同性[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)进行对比，并推导出其独特的物理特征，例如[幂律](@keyword=power_laws|lang=zh-CN|style=Feynman)温度依赖性。随后，在 **应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系** 章节中，我们将把焦点转向实验室，审视用于寻找这些节点“指纹”的实验性探究工作和精密技术，并揭示这一物理学如何与从磁学到核科学等不同领域相互联系。

## 原理与机制

因此，我们有了这些在曾经被认为不可能的高温下转变为[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的奇特材料。但它们是如何运作的呢？其内部深处运行的秘密机制是什么？当我们层层剥开，会发现这并非一个简单、完美和谐的故事，而是一场复杂而优美的量子力学规则之舞，伴随着出人意料且优雅的后果。理解这一切的关键在于一个单一的概念：**[超导能隙](@keyword=superconducting_gap|lang=zh-CN|style=Feynman)**。

### [能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的无序性：谷、峰与零点

想象一下你是一个普通金属中的电子。只要有[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)，你几乎可以拥有任何你想要的能量。这有点像一个道路四通八达的繁华都市。但当金属变成[常规超导体](@keyword=conventional_superconductors|lang=zh-CN|style=Feynman)——我们称之为**[s波](@keyword=s_waves|lang=zh-CN|style=Feynman)[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)**——非凡的事情发生了。电子配对形成**库珀对**，一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)就在它们最活跃的能级（费米能）处打开了。这个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，我们称之为 $\Delta$，就像一个禁区。你无法在这个区域内找到任何单个电子态。要打破一个[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)并产生一个激发（一个**[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)**），你必须给它至少 $\Delta$ 的能量。因为无论电子朝哪个方向运动，这个能量都是相同的，所以我们说这个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)是**各向同性**的。它就像一座城堡周围一条深度固定的、完美光滑的圆形护城河。

这个由Bardeen-Cooper-Schrieffer (BCS) 理论所描述的景象是整洁有序的。但事实证明，大自然更有创造力。在许多[非常规超导体](@keyword=unconventional_superconductors|lang=zh-CN|style=Feynman)中，[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)不是一个常数。它是**各向异性**的：它的大小取决于电子在晶体中运动的方向。想象一下，我们的护城河现在深度不同；在某些方向上它很深，而在另一些方向上则很浅。

现在到了关键的转折点。在其中一些材料中，[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)不仅仅是变浅——它在某些特殊方向上完全变为*零*。[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)上这些[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)为零的点或线被称为**节点**。一个常见的例子是**[d波超导体](@keyword=d_wave_superconductors|lang=zh-CN|style=Feynman)**，其[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)具有一种四叶草形状，由一个类似 $\Delta_{\mathbf{k}} = \Delta_{0}(\cos k_{x} - \cos k_{y})$ 的方程描述，其中 $k_x$ 和 $k_y$ 描述了运动方向 [@problem_id:1781839]。沿着 $|k_x| = |k_y|$ 的对角线方向，[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)恰好为零。

这不是一个小细节；它改变了*一切*。节点的存在意味着产生激发没有最低能量成本。你只需付出极小的代价就能打破一个库珀对，只要你朝着正确（节点）的方向推动它。在任何高于绝对零度的温度下，这意味着[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中充满了大量的低能[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)，而这些[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)在其全[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的同类中是根本不存在的。这些[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)是我们故事中的主角，通过追踪它们的踪迹，我们可以揭开[节点超导体](@keyword=nodal_superconductor|lang=zh-CN|style=Feynman)的秘密。

### 节点的指纹：[幂律](@keyword=power_laws|lang=zh-CN|style=Feynman)的力量

我们如何确定这些节点是真实存在的？我们不能简单地看进材料内部看到[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。相反，我们必须成为聪明的侦探。我们必须寻找这片无时无刻不存在的低能[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)海洋所带来的后果。最有力的线索来自于比较物理性质随温度的变化情况。

在全[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，要在低温下产生任何[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)，你必须克服[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta$。[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的数量，以及它们对任何物理性质的贡献，将与一个类似 $\exp(-\Delta / k_B T)$ 的因子成正比。这是一种**指数激活**行为。在低温下，这个数量小得惊人。但对于[节点超导体](@keyword=nodal_superconductor|lang=zh-CN|style=Feynman)，情况就不同了。可用低能态的数量不面临指数壁垒。相反，它遵循温度的**[幂律](@keyword=power_laws|lang=zh-CN|style=Feynman)**，如 $T^n$。寻找节点，[实质](@keyword=parenchyma|lang=zh-CN|style=Feynman)上就是寻找这些幂律。

#### [热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)：一次微小振动的能量

最直接的测试之一是测量**比热**，它告诉我们提高材料温度需要多少能量。在有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，低温下很难加热，因为你需要一大块能量 $\Delta$ 来产生最初几个携带热量的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)。因此，比热是指数级微小的。

然而，在[节点超导体](@keyword=nodal_superconductor|lang=zh-CN|style=Feynman)中，你可以用任何你想要的能量产生[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)，无论多小。一点点热扰动就足以激发它们。这种容易吸收热量的能力反映在比热上。对于二维[d波超导体](@keyword=d_wave_superconductors|lang=zh-CN|style=Feynman)，在低能量 $E$ 处可用的态密度与能量本身成正比，即 $N(E) \propto |E|$。计算表明，这导致[比热](@keyword=specific_heat|lang=zh-CN|style=Feynman)随温度的平方增长，即 $C_V \propto T^2$ [@problem_id:149865] [@problem_id:1781839]。观察到 $T^2$ 依赖性而不是指数依赖性是线节点的“确凿证据”。

#### [磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)：不情愿的入侵者

另一个绝佳的证据来自于[迈斯纳效应](@keyword=the_meissner_effect|lang=zh-CN|style=Feynman)。[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)会排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，但[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)确实能穿透到表面附近一个微小的距离。这个距离就是**[磁穿透深度](@keyword=magnetic_penetration_depth|lang=zh-CN|style=Feynman)**，$\lambda$。$\lambda$ 的值与凝聚到超导态的电子数量——即**[超流密度](@keyword=superfluid_density|lang=zh-CN|style=Feynman)** $n_s$——直接相关。具体来说，关系是 $\lambda^{-2}(T) \propto n_s(T)$ [@problem_id:3009616]。

任何由热能产生的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)都是“正常”流体的一部分，会*减少*[超流密度](@keyword=superfluid_density|lang=zh-CN|style=Feynman)。在全[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)材料中，$n_s$ 在低温下几乎是恒定的，因为产生的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)非常少。所以，$\lambda(T)$ 也几乎是恒定的。但在[节点超导体](@keyword=nodal_superconductor|lang=zh-CN|style=Feynman)中，[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的幂律增长导致 $n_s$ 的可观下降，从而导致 $\lambda(T)$ 的增加。

$\lambda(T)$ 变化的确切方式告诉我们关于节点几何形状的信息。
- 对于**线节点**（如二维d波材料中），发现变化量 $\Delta\lambda(T) = \lambda(T) - \lambda(0)$ 与温度成线性关系：$\Delta\lambda(T) \propto T$ [@problem_id:251928] [@problem_id:3009616]。
- 对于**点节点**（[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)仅在三维费米面上的特定点为零），变化是二次方的：$\Delta\lambda(T) \propto T^2$ [@problem_id:3001995]。

通过极其精确地测量一个微弱[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)如何在我们从绝对零度稍微加热材料时穿透它，我们实际上可以绘制出[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)中零点的维度！这是一个宏观测量揭示深刻微观量子真理的惊人例子。同样的物理也支配着其他磁性，比如**[下临界场](@keyword=lower_critical_field|lang=zh-CN|style=Feynman)** $H_{c1}$，它标志着磁通涡旋首次进入材料的点。对于[节点超导体](@keyword=nodal_superconductor|lang=zh-CN|style=Feynman)，$H_{c1}(T)$ 也随着温度呈现[幂律](@keyword=power_laws|lang=zh-CN|style=Feynman)依赖性下降 [@problem_id:3001995]。

#### 热导率：[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)高速公路

那么导热性呢？在极低温度下，晶体中的热量由[晶格振动](@keyword=crystal_lattice_vibrations|lang=zh-CN|style=Feynman)（[声子](@keyword=phonons|lang=zh-CN|style=Feynman)）和电子携带。在一个非常纯净的晶体中，[声子](@keyword=phonons|lang=zh-CN|style=Feynman)传播很长的距离，主要被样品的边界散射。它们携带热量的能力随着 $T^3$ 迅速下降。那么电子呢？在全[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，电子被锁定在[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)中，只有指数级少数的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)可以携带热量。它是一种极好的热绝缘体。

但绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)下的[节点超导体](@keyword=nodal_superconductor|lang=zh-CN|style=Feynman)则完全不同。即使是极少量的杂质散射也会在节点处形成一个[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)库，这些[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)可以携带热量。在一项卓越的理论发现中，研究表明这些[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)会产生一种**普适热传导**。当 $T \to 0$ 时，热导率除以温度，即 $\kappa/T$，趋于一个常数值，该值仅取决于[基本常数](@keyword=fundamental_constants|lang=zh-CN|style=Feynman)和[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的性质，而*不*取决于杂质的数量[@problem_id:2802521]。这些节点[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)创造了一个具有普适容量的热“高速公路”，这一事实是对整个理论图景最引人注目的证实之一。

### 一种奇特的新工具：“杂质”物理学

你可能会认为晶体中的杂质，或“污垢”，对物理学家来说只是个麻烦。但在非常规超导的世界里，它们成为一种极其强大的诊断工具。关键是理解杂质如何与不同类型的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)发生不同的相互作用。

在常规[s波](@keyword=s_waves|lang=zh-CN|style=Feynman)[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)处处相同。非磁性杂质会散射一个电子，但由于[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)在所有方向上“看起来”都一样，配对不容易被破坏。这就是**[Anderson定理](@keyword=anderson_s_theorem|lang=zh-CN|style=Feynman)**的精髓。因此，[s波](@keyword=s_waves|lang=zh-CN|style=Feynman)[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的[临界温度](@keyword=critical_temperature|lang=zh-CN|style=Feynman) $T_c$ 对非磁性杂质的抵抗力非常强。

现在考虑一个[d波超导体](@keyword=d_wave_superconductors|lang=zh-CN|style=Feynman)。它的[能隙函数](@keyword=gap_function|lang=zh-CN|style=Feynman)不仅是各向异性的，还是符号变化的。它有正的“瓣”和负的“瓣”。[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)中的一个电子可能正愉快地在一个正瓣中巡航。如果它从一个杂质上散射到一个对应于负瓣的方向，配对就会被灾难性地破坏。在[s波](@keyword=s_waves|lang=zh-CN|style=Feynman)材料中无害的非磁性杂质，在d波材料中变成了强有力的**破对子**。因此，[d波超导体](@keyword=d_wave_superconductors|lang=zh-CN|style=Feynman)对无序极为敏感，即使是少量的非磁性杂质也会强烈抑制其 $T_c$ [@problem_id:1828353]。

这种敏感性具有可观察到的后果，为节点图像提供了更多证据。还记得[穿透深度](@keyword=penetration_depth|lang=zh-CN|style=Feynman)的线性温度依赖性 $\Delta\lambda(T) \propto T$ 吗？当你在[d波超导体](@keyword=d_wave_superconductors|lang=zh-CN|style=Feynman)中加入杂质时，这种行为会改变。在极低温度下，出现一个新的区域，其依赖性变为二次方：$\Delta\lambda(T) \propto T^2$ [@problem_id:3009576] [@problem_id:2988279]。这是因为杂质散射“模糊”了完美的节点，在零能量处诱导了一个微小但有限的[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman) [@problem_id:1271961]。我们简直可以观察到节点的指纹以一种可预测的方式被杂质弄脏！

然而，这确实引入了一个可能混淆身份的情况。常规s波[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中的磁性杂质也可能是破对子，并能在[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)内产生态。一个足够“脏”的磁性s波[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)最终可能表现出模仿干净的[节点超导体](@keyword=nodal_superconductor|lang=zh-CN|style=Feynman)的[幂律](@keyword=power_laws|lang=zh-CN|style=Feynman)行为 [@problem_id:2988279]。我们如何区分它们呢？我们必须是优秀的侦探，寻找更多线索。我们检查对*非磁性*杂质的响应。我们寻找“普适”热传导。当所有证据都指向同一个方向时，节点存在的论证就变得不可动摇了 [@problem_id:2802521]。

从[比热](@keyword=specific_heat|lang=zh-CN|style=Feynman)到磁响应再到[热输运](@keyword=heat_transport|lang=zh-CN|style=Feynman)，我们看到一个连贯的故事浮现出来。这些看似迥异的行为——这里的线性上升，那里的二次方下降，一个隐藏在寒冷中的[普适常数](@keyword=universal_constants|lang=zh-CN|style=Feynman)——都被统一起来了。它们都是一个简单、优雅而深刻的事实所带来的后果：在这些奇异的材料中，将电子结合成对的超导“胶水”存在薄弱点。而在那些量子的薄弱点，即节点中，蕴藏着它们全部特性的关键。