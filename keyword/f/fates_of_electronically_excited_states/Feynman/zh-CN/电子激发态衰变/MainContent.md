## 引言
当一个分子吸收光时，它会跃迁到一个高能量的[电子激发态](@keyword=excited_electronic_states|lang=zh-CN|style=Feynman)。但这个高能状态是短暂的，分子最终必须返回其稳定的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。在激发和弛豫之间的短暂瞬间发生了什么？这个问题是[光物理学](@keyword=photophysics|lang=zh-CN|style=Feynman)领域的核心，因为分子所采取的路径决定了一切，从材料的颜色和亮度到光合作用的效率。其挑战在于理解各种衰变通道之间的复杂竞争，其中一些产生光，而另一些仅以热量形式耗散能量。本文全面概述了电子激发态的各种归宿。第一章“原理与机制”将介绍基本概念，包括[Jablonski图](@keyword=jablonski_diagram|lang=zh-CN|style=Feynman)、[Kasha规则](@keyword=kasha_s_rule|lang=zh-CN|style=Feynman)，以及支配光发射与[非辐射衰变](@keyword=non_radiative_decay|lang=zh-CN|style=Feynman)之间竞争的量子规则。第二章“应用与跨学科联系”将展示这些原理如何在自然界和技术中得到利用，从萤火虫的光和光合作用的引擎，到先进OLED显示器的设计和[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)的基础。

## 原理与机制

想象一个分子，静静地处于其最低能量状态，即**[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)**。突然，它被一个光粒子——[光子](@keyword=photon|lang=zh-CN|style=Feynman)——击中。就像被锤子敲响的钟，分子被激发到一个高能量状态，即**电子激发态**。接下来会发生什么？它会以一道明亮的光芒释放这新获得的能量吗？它会仅仅升温并[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)吗？它会经历一种奇怪的转变，在短暂的瞬间改变其本质吗？这是[光物理学](@keyword=photophysics|lang=zh-CN|style=Feynman)的核心问题，答案是一个关于竞争、量子规则以及周围世界深刻影响的迷人故事。

### 激发的火花

在衰变的故事开始之前，必须有一个创造的时刻。分子最初是如何被激发的呢？最常见的方式，也是我们关注的重点，是通过吸收光，这个过程称为**[光致发光](@keyword=photoluminescence|lang=zh-CN|style=Feynman)**。想象一下你在灯下“充电”的夜光星星。它们吸收光能，然后慢慢地重新发射出来。这与萤火虫或荧光棒产生的光有根本的不同。在后两者的情况下，能量并非来自外部光源，而是来自[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)中释放的能量。这被称为**[化学发光](@keyword=chemiluminescence|lang=zh-CN|style=Feynman)** [@problem_id:1312069]。在这两种情况下，最终的行为是相同的：一个被激发的分子弛豫并发射一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)。但在我们的旅程中，我们将跟随一个刚刚吸收了[光子](@keyword=photon|lang=zh-CN|style=Feynman)的分子的命运，踏上[光致发光](@keyword=photoluminescence|lang=zh-CN|style=Feynman)的道路。

### 岔路口：主要途径

一旦我们的分子充满了多余的电子能量，它就发现自己处于一个十字路口，有多条路径可以回到平静的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。这些路径被精美地组织在一个称为**[Jablonski图](@keyword=jablonski_diagram|lang=zh-CN|style=Feynman)**的概念图中，分为两大类：辐射途径和非辐射途径。

*   **辐射途径**是那些“爱表现”的途径。它们通过发射[光子](@keyword=photon|lang=zh-CN|style=Feynman)来释放能量。其中最主要的是**荧光**，这是一种明亮、快速的发射，当[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)分子返回[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)而其[电子自旋](@keyword=electron_spin|lang=zh-CN|style=Feynman)构型不发生改变时发生。

*   **非辐射途径**是无声的窃贼。它们将能量以热量的形式耗散到分子周围的环境中，而不产生任何光。它们是荧光的主要竞争者。

在分子*内部*发生的最重要的两个非辐射过程是**内转换（IC）**和**系间窜越（ISC）** [@problem_id:2179283]。内转换是*相同*自旋的电子态之间的跃迁，基本上是将电子能量转化为振动能——可以把它想象成分子通过“[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)”使自己平静下来。系间窜越是一个更神秘的过程：一个到具有*不同*[自旋多重度](@keyword=spin_multiplicity|lang=zh-CN|style=Feynman)的电子态的非辐射跳跃。这就像分子施展了一个量子力学魔术，翻转了其中一个电子的自旋。

最后，在任何给定的电子态内，分子可以通过与邻近分子（如溶剂分子）的碰撞迅速释放多余的[振动能](@keyword=vibrational_energy|lang=zh-CN|style=Feynman)。这个冷却过程被称为**[振动弛豫](@keyword=vibrational_relaxation|lang=zh-CN|style=Feynman)（VR）**。这是一个极其快速的非辐射过程，确保分子能迅速沉降到其所处的任何电子能级的底部。

### 大级联与[Kasha规则](@keyword=kasha_s_rule|lang=zh-CN|style=Feynman)

所以我们有这样一个选项菜单：荧光、[内转换](@keyword=internal_conversion|lang=zh-CN|style=Feynman)、[系间窜越](@keyword=intersystem_crossing|lang=zh-CN|style=Feynman)和[振动弛豫](@keyword=vibrational_relaxation|lang=zh-CN|style=Feynman)。分子会选择哪一个？答案很简单：这是一场竞赛。**最快的过程获胜。**

让我们想象我们的分子吸收了一个能量非常高的[光子](@keyword=photon|lang=zh-CN|style=Feynman)，不仅将其提升到第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)（$S_1$），还提升到了第二（$S_2$）甚至第三（$S_3$）[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)。人们可能天真地[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)看到所有这些态都发出荧光。但在绝大多数情况下，我们看不到。我们几乎只看到来自*最低*[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman) $S_1$ 的光。这个非凡的观察结果被称为**[Kasha规则](@keyword=kasha_s_rule|lang=zh-CN|style=Feynman)** [@problem_id:2837609]。

为什么？这又回到了竞赛上。更高[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)之间（$S_3 \to S_2 \to S_1$）的[振动弛豫](@keyword=vibrational_relaxation|lang=zh-CN|style=Feynman)和内转换速率快得惊人，通常发生在飞秒或皮秒（$10^{-15}$ 到 $10^{-12}$ 秒）的时间尺度上。相比之下，荧光的速率要慢得多，通常需要纳秒（$10^{-9}$ 秒）。这就像一个球从楼梯上弹跳下来。每下一级台阶的跳跃（VR和IC）都非常快，而从楼梯侧面飞出去（从高台阶发出荧光）的机会非常小。分子以非辐射方式迅速地沿着电子态的阶梯级联下降，直到它“卡”在第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman) $S_1$ 的底部。$S_1$ 和[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)（$S_0$）之间的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)要大得多，根据一个称为“[能隙定律](@keyword=energy_gap_law|lang=zh-CN|style=Feynman)”的原理，这使得向[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的内转换变得慢得多。现在，荧光终于有机会参与竞争。[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)分子的布居在 $S_1$ 态上累积，主要的光就是从这个态发射出来的 [@problem_id:2782150]。

### [量子产率](@keyword=quantum_yield|lang=zh-CN|style=Feynman)：为竞赛计分

我们可以用数字来描述这场竞争。任何特定过程的效率都由其**[量子产率](@keyword=quantum_yield|lang=zh-CN|style=Feynman)** $\Phi$ 来描述。[荧光量子产率](@keyword=fluorescence_quantum_yield|lang=zh-CN|style=Feynman) $\Phi_f$ 就是实际发出荧光的[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)分子的分数。如果 $\Phi_f = 0.8$，这意味着80%被激发的分子成功地发射了一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)。

[量子产率](@keyword=quantum_yield|lang=zh-CN|style=Feynman)由所有竞争性衰变途径的相对速率决定。如果一个处于 $S_1$ 态的分子能以速率常数 $k_f$ 发出荧光，以速率 $k_{IC}$ 进行内转换，并以速率 $k_{ISC}$ 进行系间窜越，那么总衰变速率为 $k_{total} = k_f + k_{IC} + k_{ISC}$。荧光的[量子产率](@keyword=quantum_yield|lang=zh-CN|style=Feynman)就是其速率与总速率之比：

$$
\Phi_f = \frac{k_f}{k_{total}} = \frac{k_f}{k_f + k_{IC} + k_{ISC}}
$$

这个简单的公式功能非常强大。对于具有特定速率常数的染料，我们可以精确预测其吸收的能量中有多少将转化为光，多少将转化为热量，以及多少将被转移到神秘的[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)中 [@problem_id:2565043]。

### 三重态：[慢光](@keyword=slow_light|lang=zh-CN|style=Feynman)之境

当一个分子发生[系间窜越](@keyword=intersystem_crossing|lang=zh-CN|style=Feynman)时会发生什么？它进入一个被称为**[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)**的新能级簇，其中最低的是 $T_1$。从 $T_1$ 态返回[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)（$S_0$）也需要一次自旋翻转，这是一个量子力学上的“禁戒”过程。因为它被禁戒，所以它非常缓慢。与荧光的纳秒级时间不同，这种新的辐射过程，称为**磷光**，可能需要微秒、毫秒，甚至几秒钟！这就是“夜光”物品背后的秘密。它们的能量来自长寿命[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)布居的缓慢、持续的光泄漏。

系间窜越的效率，以及因此而来的[磷光](@keyword=phosphorescence|lang=zh-CN|style=Feynman)亮度，关键取决于[速率常数](@keyword=rate_constants|lang=zh-CN|style=Feynman) $k_{ISC}$。两个分子可能看起来几乎一模一样，吸收相同的光，并具有相同的内在荧光速率，但一个可能是明亮的荧光体，而另一个则是强烈的[磷光](@keyword=phosphorescence|lang=zh-CN|style=Feynman)体。唯一的区别是，[磷光](@keyword=phosphorescence|lang=zh-CN|style=Feynman)分子具有快得多的系间窜越速率，在荧光发生之前就将[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)布居转移到了三重态 [@problem_id:1482027]。

是什么使得这个自旋翻转的ISC过程在某些分子中快，而在另一些分子中慢？答案在于一种微妙的量子现象，称为**[自旋-轨道耦合](@keyword=l_s_coupling|lang=zh-CN|style=Feynman)（SOC）**。这种效应源于[电子自旋](@keyword=electron_spin|lang=zh-CN|style=Feynman)与其自身围绕原子核的[轨道运动](@keyword=orbital_motion|lang=zh-CN|style=Feynman)之间的相互作用，它起到了单重态和三重态的“混合器”的作用。SOC的强度随分子中原子的[原子序数](@keyword=atomic_number|lang=zh-CN|style=Feynman)（$Z$）急剧增加。这就是为什么含有溴或碘等重原子的分子中[磷光](@keyword=phosphorescence|lang=zh-CN|style=Feynman)现象常常很显著。例如，在碘分子（$I_2$）中，SOC非常强，以至于它彻底打乱了各态的[单重态和三重态](@keyword=singlet_and_triplet_states|lang=zh-CN|style=Feynman)特性，使得[系间窜越](@keyword=intersystem_crossing|lang=zh-CN|style=Feynman)非常高效，并显著缩短了某些[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的寿命 [@problem_id:2940708]。这种“[重原子效应](@keyword=heavy_atom_effect_2|lang=zh-CN|style=Feynman)”是一个绝佳的例子，说明了一个通常与高能物理相关的[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)效应，如何支配着我们周围分子的光的颜色和[持续时间](@keyword=holding_times|lang=zh-CN|style=Feynman)。

### 外部影响：当分子并非独自行动

一个[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)分子并非一座孤岛。它的环境可以极大地改变其命运。

#### 猝灭：窃取光芒

想象一下我们准备发出荧光的[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)分子。在它发光之前，溶液中的另一个分子——一个**猝灭剂**——与它碰撞并窃取了它的能量。猝灭剂被激发（或发生[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)），而我们原来的分子则在没有发光的情况下回到[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。最臭名昭著的猝灭剂之一是分子氧（$O_2$），这就是为什么许多荧光实验都在脱氧溶液中进行的原因。

猝灭的效率取决于一个简单但至关重要的因素：[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)分子能存活多久？其寿命（$\tau_0$）越长，它在溶液中游荡并找到猝灭剂的时间就越多。**[Stern-Volmer方程](@keyword=stern_volmer_equation|lang=zh-CN|style=Feynman)**完美地描述了这一点，它表明荧光的减少与猝灭剂浓度和[激发态寿命](@keyword=lifetime_of_excited_state|lang=zh-CN|style=Feynman)成正比 [@problem_id:1524239]。这就是为什么寿命为毫秒到秒级的磷光对猝灭极其敏感，而寿命为纳秒级的荧光则要稳健得多。[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)存活时间如此之长，几乎肯定会被像氧气这样的猝灭剂“捕获”，而单重态的存在转瞬即逝，常常能安然无恙地逃脱 [@problem_id:1999520]。

#### 激基复合物与激基缔合物：[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的团队合作

有时，“猝灭剂”并非恶意的一方，而是一个合作伙伴。如果一个[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)分子 $M^*$ 与一个相同的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)分子 $M$ 碰撞，它们可以形成一个临时的、束缚的[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)二聚体，称为**激基复合物** $(MM)^*$。这个[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)复合物是一个具有自身独特性质的新物种。与原始[单体](@keyword=monomer|lang=zh-CN|style=Feynman)相比，其发射通常是宽峰、无[精细结构](@keyword=fine_structure|lang=zh-CN|style=Feynman)且向更长波长移动（[红移](@keyword=redshift|lang=zh-CN|style=Feynman)）。激基复合物的典型标志是其特征性发光仅在高浓度下出现，此时[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)分子找到[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)伙伴的机会很高 [@problem_id:2943137]。

如果[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)分子 $D^*$ 反而找到了一个不同物种的伙伴，一个受体 $A$，它们可以形成一个**激基缔合物**（[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)复合物）$(DA)^*$。这些尤其引人入胜，因为它们通常涉及电子转移，形成一个具有显著[电荷转移](@keyword=charge_transfer|lang=zh-CN|style=Feynman)特性的状态 $(D^{\delta+}A^{\delta-})^*$。这使得激基缔合物具有很大的[电偶极矩](@keyword=electric_dipole_moment|lang=zh-CN|style=Feynman)。在极性溶剂（如水）中，溶剂分子会重新取向以稳定这种[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)分离，从而降低激基缔合物的能量。其结果是一个显著的光谱特征：随着[溶剂极性](@keyword=solvent_polarity|lang=zh-CN|style=Feynman)的增加，从激基缔合物发出的光的颜色会逐渐红移。这种[溶剂化显色效应](@keyword=solvatochromism|lang=zh-CN|style=Feynman)是识别这些瞬态、协作性[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的有力工具 [@problem_id:2943137]。

从最初吸收单个[光子](@keyword=photon|lang=zh-CN|style=Feynman)，到速率、自旋和分子伙伴的复杂舞蹈，[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的归宿是化学本身的缩影——量子规则、动力学竞争和[环境影响](@keyword=environmental_impact|lang=zh-CN|style=Feynman)的动态相互作用，用光与色彩描绘着世界。