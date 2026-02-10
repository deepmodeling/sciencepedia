## 应用与跨学科联系

在前面的讨论中，我们阐述了[共振价键](@keyword=resonating_valence_bond|lang=zh-CN|style=Feynman)（RVB）态的基本原理。我们看到它是一个激进而优美的思想：一种[物质的量](@keyword=amount_of_substance|lang=zh-CN|style=Feynman)子态，其中自旋并不像列队行进的士兵那样冻结成静态有序的模式，而是形成一个由纠缠对组成的动态、涨落的“液体”。这幅图景，即自旋以所有可能方式配对成单重态的[相干叠加](@keyword=coherent_superposition|lang=zh-CN|style=Feynman)，可能看起来像一个理论上的奇想。但这是多么壮丽的奇想！事实证明，这个简单的概念不仅是一项智力活动；它是一把万能钥匙，开启了通往现代物理学中一些最深刻、最具挑战性问题的大门。在本章中，我们将踏上一段旅程，看看这把钥匙将我们带向何方，从奇异磁体的核心，到[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)中最大的谜题——高温超导，甚至到量子信息和计算的前沿。

### 量子磁体的真正灵魂

让我们从这个想法的起源——量子磁学领域开始。想象一个原子网格，每个原子都带有一个像微型条形磁铁一样的自旋。一条自然基本法则，即海森堡相互作用，规定了许多材料中相邻的自旋倾向于指向相反的方向——形成[反铁磁体](@keyword=antiferromagnets|lang=zh-CN|style=Feynman)。满足这一条件的最简单、最“经典”的方式是[奈尔态](@keyword=néel_state|lang=zh-CN|style=Feynman)：一个完美的棋盘状上下自旋排列。很长一段时间里，这被认为是故事的结局。

但量子世界更为微妙。如果我们不使用这种刚性的经典图像，而是用我们新的[量子液体](@keyword=quantum_liquids|lang=zh-CN|style=Feynman)——RVB 态来描述[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)，会怎么样？对两者进行比较的简单变分计算可以揭示很多信息 [@problem_id:3013872]。在某些简化的假设下——例如，不同的单重态模式重叠不大——人们可能会发现经典的[奈尔态](@keyword=néel_state|lang=zh-CN|style=Feynman)似乎能量更低。这是否意味着我们优美的 RVB 思想是错误的？完全不是！它告诉我们，我们的*近似*过于简单。这个计算突显了这场角逐的真正本质：[奈尔态](@keyword=néel_state|lang=zh-CN|style=Feynman)通过以经典、平均化的方式满足所有键来获得能量，但它完全忽略了量子涨落降低能量的魔力。RVB 态，就其构造而言，正是建立在这些涨落之上的。虽然一个简单的 RVB 试探波函数可能无法捕捉到系统的全部能量，但它正确地指出了故事的主角：[量子纠缠](@keyword=quantum_entanglement|lang=zh-CN|style=Feynman)。更复杂的、放宽了这些粗糙近似的 RVB [波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)，确实被证明是对真实量子[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的绝佳描述。

当自旋被“阻挫”时，RVB 态才真正发挥其作用。想象一下试图在三角[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)上[排列](@keyword=permutation|lang=zh-CN|style=Feynman)反铁磁自旋。如果一个自旋向上，它的邻居希望向下。但是三角形角落的第三个自旋该怎么办呢？它同时是两者的邻居，它不可能同时相对于一个上自旋和一个下自旋都是“下”！[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)几何本身就阻止了简单的棋盘状序的形成。在这种阻挫环境中，自旋别无选择，只能放弃静态[排列](@keyword=permutation|lang=zh-CN|style=Feynman)，进入一种动态的集体舞蹈。RVB 态，我们所说的涨落单重态液体，成为对这种阻挫量子舞蹈的一种极其自然和优雅的描述 [@problem_id:3013823]。正是在这些[阻挫系统](@keyword=frustrated_systems|lang=zh-CN|style=Feynman)中，RVB 态不再仅仅是一个候选者，而是成为物质真实[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的主要竞争者。

### 圣杯：高温超导

RVB 态的故事在1987年发生了戏剧性的转折。一类新材料，即陶瓷铜氧化物，被发现能在惊人的高温下超导。但它们带来了一个谜题。在它们的自然状态下，它们根本不是金属；它们是莫特绝缘体 (Mott insulators)，在这种材料中，强大的电子-电子排斥（$U$）将电子锁定在原位，每个格点一个，从而阻止任何电流流动。然而，如果你通过移除一小部分（$x$）电子——这个过程称为掺杂——在这个刚性结构中“戳”几个洞，它们就会转变为世界上已知的最好的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)。

这怎么可能？杰出的物理学家 Philip Anderson 做出了一个大胆的提议：铜氧化物的绝缘母体态正是一个 RVB [自旋液体](@keyword=spin_liquids|lang=zh-CN|style=Feynman)！这些材料的低能“游戏规则”由所谓的 $t$-$J$ 模型描述，该模型描述了电子在严格禁止双占据的规则下跳跃（$t$），以及由母体绝缘体中虚[电子跳跃](@keyword=electron_hopping|lang=zh-CN|style=Feynman)产生的相邻自旋间的反铁[磁相](@keyword=magnetic_phases|lang=zh-CN|style=Feynman)互作用（$J$）[@problem_id:3013840]。

Anderson 的想法是，绝缘体 RVB 态中已存在的中性[自旋单重态](@keyword=spin_singlet_state|lang=zh-CN|style=Feynman)对是[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中带电[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的*前驱*。为了理解这一点，理论家们开发了一个绝妙的概念工具：从粒子方法 (slave-particle formalism)。想象一个电子不是单个粒子，而是由两个“从粒子”构成：一个中性的、携带自旋的[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)，称为**自旋子 (spinon)**，以及一个无自旋的、携带[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)，称为**空穴子 (holon)**。最初的 RVB 态是配对自旋子的海洋。对系统进行掺杂会引入可移动的空穴子。现在，如果这些作为[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)载体的玻色性空穴子发生玻色-爱因斯坦凝聚，会发生什么？当它们凝聚成一个[相干态](@keyword=coherent_states|lang=zh-CN|style=Feynman)时，它们就“解放”了[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)。它们预先存在的配对被揭示出来，它们披上空穴子的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，成为[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为 $2e$ 的超导电子对 [@problem_id:3013840]！系统自发地打破一个涌现的规范对称性，这是希格斯机制 (Higgs mechanism) 的一个优美例子，从而产生[迈斯纳效应](@keyword=the_meissner_effect|lang=zh-CN|style=Feynman) (Meissner effect)——即[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的排斥，这是[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的决定性特征 [@problem_id:3013840]。

这个非凡的故事可以被具体地数学化。我们必须应用 Gutzwiller 投影算符 $\hat{P}_G = \prod_i (1 - \hat{n}_{i\uparrow}\hat{n}_{i\downarrow})$，它充当一个“禁止双占据”的过滤器。它取一个标准的 Bardeen-Cooper-Schrieffer (BCS) 态，系统地丢弃所有两个电子试图占据同一格点的构型，从而体现由巨大排斥 $U$ 产生的强关联效应 [@problem_id:2994229]。
最终得到的 Gutzwiller 投影 BCS 态：
$$ \lvert\Psi_{\mathrm{RVB}}\rangle = \hat{P}_G \left( \prod_{\mathbf{k}}\left(u_{\mathbf{k}} + v_{\mathbf{k}}\, \hat{c}^\dagger_{\mathbf{k}\uparrow}\hat{c}^\dagger_{-\mathbf{k}\downarrow}\right) \right) \lvert 0 \rangle $$
是对一个源于[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的优美而简洁的描述。此外，由于配对是由短程反铁[磁相](@keyword=magnetic_phases|lang=zh-CN|style=Feynman)互作用 $J$ 介导的，该理论自然地预测超导态应具有特定的空间结构，即所谓的$d_{x^2-y^2}$-波对称性。这是一个惊人的预测，后来被大量实验所证实，为基于 RVB 的机制提供了强有力的证据。

### [奇异金属](@keyword=strange_metals|lang=zh-CN|style=Feynman)：[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)与量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)

RVB 理论的解释力不止于超导性。铜氧化物最奇特的特征之一是“[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)”相。在[超导转变](@keyword=superconducting_transition|lang=zh-CN|style=Feynman)温度之上，在一个常被称为“[奇异金属](@keyword=strange_metals|lang=zh-CN|style=Feynman)”的相图区域，该材料并非传统的金属。实验显示电子谱中存在[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的迹象——仿佛一些对已经形成——但材料没有[零电阻](@keyword=zero_resistance|lang=zh-CN|style=Feynman)，也没有[迈斯纳效应](@keyword=the_meissner_effect|lang=zh-CN|style=Feynman)。

从粒子图像为这个谜题提供了一个直接而自然的解释。[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)就是自旋子已经配对（其能标由 $J$ 设定），但空穴子尚未凝聚以赋予这些对[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)相干性的温度或掺杂区域 [@problem_id:3020732]。所以，你有中性对，但没有超导性。[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)尺度 $\Delta_{\text{pg}}$ 反映了[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)对的结合能，而真正的[超导能隙](@keyword=superconducting_gap|lang=zh-CN|style=Feynman) $\Delta_{\text{sc}}$ 只有在空穴子凝聚时才会出现。这带来了一个优美的预测：超导能隙应与[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)配对振幅和空穴子凝聚密度的乘积成正比，而后者随掺杂浓度 $x$ 变化。这意味着 $\Delta_{\text{sc}}(x) \propto x \cdot \Delta_{\text{pg}}(x)$，这巧妙地解释了为什么超导性呈现穹顶形状，并在非常低的掺杂水平下消失，尽管强[配对关联](@keyword=pairing_correlations|lang=zh-CN|style=Feynman)（[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)）仍然存在。

这种竞争相的概念将 RVB 态从一个特定的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)提升为一种真正的*物质相*。掺杂充当了一个调谐旋钮，使我们能够在一个丰富的[相图](@keyword=phase_portraits|lang=zh-CN|style=Feynman)中导航。例如，在一个阻挫[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)上，仅通过调节掺杂水平，就有可能驱动一个从磁有序态到类 RVB [自旋液体](@keyword=spin_liquids|lang=zh-CN|style=Feynman)相的量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman) [@problem_id:1207511]。能量竞争的胜者敏感地取决于有序化所获得的[磁能](@keyword=magnetic_energy|lang=zh-CN|style=Feynman)与移动空穴所获得的动能之间的平衡，后者在更具“液态”特征的 RVB 态中更大。

### 通往新世界的桥梁：[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)与计算

到目前为止，我们的旅程一直在凝聚态物理的领域内。但 RVB 态的核心要素——纠缠——也是即将到来的量子信息革命的核心资源。这种联系不仅是哲学上的，也是具体的。

考虑一个微小的 RVB 系统：位于正方形四个角上的四个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) (qubit) [@problem_id:108261]。RVB 态是水平配对和垂直配对的叠加。现在，让我们问一个简单的问题：对角线上的两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，比如[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman) 1 和 3，处于什么状态？它们在任何一种构型中都没有直接配对。人们可能猜测它们之间的关联很弱。但直接计算揭示了一个惊人的事实：它们处于一个完美的、最大纠缠的[单重态](@keyword=singlet_state|lang=zh-CN|style=Feynman)中！这就是量子的魔力。态的“共振”性质在甚至不是最近邻的粒子之间建立了长程纠缠。

这具有深远的意义。它表明，那些自然形成 RVB [基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的材料，可以作为物理资源来生成[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)所需的纠缠。解释[高温超导](@keyword=high_temperature_superconductivity|lang=zh-CN|style=Feynman)的物质状态本身，或许也能成为未来量子处理器的基底。这在两个物理学前沿领域之间架起了一座深刻而出人意料的桥梁。更奇异的[自旋液体](@keyword=spin_liquids|lang=zh-CN|style=Feynman)版本，作为 RVB 态的近亲，甚至被预测可以承载“[拓扑量子比特](@keyword=topological_qubit|lang=zh-CN|style=Feynman)”，这种[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)将内在地免受环境噪声的干扰——这是构建[容错量子计算机](@keyword=fault_tolerant_quantum_computer|lang=zh-CN|style=Feynman)的圣杯。

### 驯服猛兽：[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)的语言

你可能想知道，我们如何能对这些极其复杂的[多体纠缠](@keyword=multipartite_entanglement|lang=zh-CN|style=Feynman)态的性质如此自信？我们无法在一张纸上解出 $10^{23}$ 个电子的薛定谔方程。答案在于为应对这一挑战而专门发展的新理论和计算语言，其中最著名的是[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)的语言。

一种称为[投影纠缠对态](@keyword=projected_entangled_pair_states|lang=zh-CN|style=Feynman) (PEPS) 的表示方法，允许我们用简单的构建块——[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)上每个格点的局域[张量](@keyword=tensor|lang=zh-CN|style=Feynman)——来构建复杂的二维[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，例如 RVB 态 [@problem_id:436545]。你可以把它想象成用微小的纠缠“乐高积木”来构建一个极其复杂的量子波函数。全局态的所有物理性质都编码在这些局域[张量](@keyword=tensor|lang=zh-CN|style=Feynman)以及它们如何连接的方式中。

例如，任何态的一个关键属性是其关联长度 $\xi$，它告诉我们两个自旋可以相距多远而仍然能“感觉”到彼此的存在。在 PEPS 框架中，这个全局属性可以从一个“转移矩阵”的谱中计算出来，该[转移矩阵](@keyword=transition_matrix|lang=zh-CN|style=Feynman)是通过收缩系统一个切片上的局域[张量](@keyword=tensor|lang=zh-CN|style=Feynman)构建的。关联长度与该矩阵两个最大[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)之比的对数成反比，即 $\xi = 1/\ln(\Lambda_1 / \Lambda_2)$。一个物理属性（$\xi$）和一个数学属性（矩阵的[谱隙](@keyword=spectral_gap|lang=zh-CN|style=Feynman)）之间的这种非凡联系，使我们能够将 RVB 物理的抽象思想置于强大的计算机上，进行模拟，并提取可验证的预测。

### 结语

我们的旅程至此结束。我们从一个简单、近乎天真的自旋以所有可能方式配对的图像开始。我们看到这一个思想在磁学物理中产生共鸣，为高温超导提供了最令人信服的框架，解释了[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)的奥秘，并与量子信息世界建立了深刻的联系。我们已经看到，一个单一、优雅的概念如何能统一看似毫无关联的广阔现象。这就是理论物理之美与力量所在。这种[纠缠对](@keyword=entangled_pairs|lang=zh-CN|style=Feynman)之舞，最初在[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)的背景下被构想出来，确实是一个普适的主题，是量子世界宏伟乐章中的一个基本主旋律。