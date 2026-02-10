## 应用与跨学科联系

现在我们已经熟悉了[瑞利-里兹变分原理](@keyword=rayleigh_ritz_variational_principle|lang=zh-CN|style=Feynman)的机制，你可能会想，“它有什么用呢？” 这是一个合理的问题。物理学中的一个原理不仅仅是一个巧妙的数学技巧；它的价值取决于它所打开的大门，它所解开的谜团，以及它所提供的工具。[变分原理](@keyword=variational_principles|lang=zh-CN|style=Feynman)不仅仅是一个工具；它更像一把万能钥匙，开启了横跨量子力学、化学乃至未来[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)领域的洞见。对于物理学家和化学家来说，它是导航在无法精确求解的[多粒子系统](@keyword=many_particle_systems|lang=zh-CN|style=Feynman)这个极其复杂世界里的指南针。

### 一次好猜测的力量：从直觉到洞见

对于几乎任何比氢原子更复杂的系统，薛定谔方程都出了名地难以精确求解。但如果我们不需要一个*精确*的答案呢？如果一个“足够好”的答案仍然能提供深刻的物理洞见呢？这正是变分原理首次展现其魔力的地方。它告诉我们，我们对系统[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)所做的任何猜测，无论多么粗糙，都会给我们一个*等于或高于*真实基态能量的能量值。猜测越好，我们离真实值就越近。

让我们来玩个游戏。想象一个被困在长度为 $L$ 的一维盒子里的粒子。从前面的章节我们知道，真实的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)是一个光滑的[正弦波](@keyword=sinusoid|lang=zh-CN|style=Feynman)，$\sin(\pi x / L)$。但假设我们不知道这一点。一个合理、直观的猜测会是什么样呢？我们知道粒子不可能在盒子外面，所以[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在墙壁处，$x=0$ 和 $x=L$，必须为零。一个能做到这一点的非常简单的函数是抛物线，形式为 $\phi(x) = x(L-x)$。它不是正确答案——与光滑的[正弦波](@keyword=sinusoid|lang=zh-CN|style=Feynman)相比，它的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)有一个[尖点](@keyword=cusps|lang=zh-CN|style=Feynman)——但它有正确的“感觉”。

如果我们将这个简单的抛物线猜测代入变分法的机器中，我们会计算出一个近似能量。惊人的结果是，这个粗糙的猜测得出的能量仅比精确的基态能量高出约 $1.3\%$！[@problem_id:2960252] 这是第一个美丽的教训：[变分原理](@keyword=variational_principles|lang=zh-CN|style=Feynman)是极其宽容的。即使是一个源于物理直觉的、定性上合理的猜测，也能提供一个在定量上相当出色的能量估计。能量在真实[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)附近是“驻定”的，所以[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)中的小误差会导致能量中更小的二阶误差。

### [化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)的诞生

该原理的力量远不止于优化能量估算。它可以构建整个概念框架。在化学领域，其最惊人的成功或许在于解释了[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)的存在本身。考虑最简单的分子，[氢分子离子](@keyword=hydrogen_molecule_ion|lang=zh-CN|style=Feynman) $\mathrm{H_{2}^{+}}$，它只有两个质子共享一个电子。

我们如何描述这个分子中的电子？一个极其简单而有力的想法，即原子轨道的线性组合（LCAO），是猜测分子轨道是其母体[原子轨道](@keyword=atomic_orbitals|lang=zh-CN|style=Feynman)的某种混合。也就是说，我们假设电子的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman) $\psi$ 是以质子 A 为中心的 $1s$ 轨道 $\phi_A$ 和以质子 B 为中心的 $1s$ 轨道 $\phi_B$ 的混合。我们将[试探函数](@keyword=trial_function|lang=zh-CN|style=Feynman)写为 $\psi = c_A \phi_A + c_B \phi_B$，其中 $c_A$ 和 $c_B$ 是混合系数。

我们不知道正确的混合比例。所以，我们让变分原理为我们决定！我们问：$c_A$ 和 $c_B$ 取什么值才能使[能量最小化](@keyword=energy_minimization|lang=zh-CN|style=Feynman)？当我们启动这个程序时，奇妙的事情发生了。数学推导给出的不是一个解，而是两个！[@problem_id:2652439]

一个解对应于[原子轨道](@keyword=atomic_orbitals|lang=zh-CN|style=Feynman)的同相组合（$c_A = c_B$），它将电子密度堆积在两个质子*之间*。这种增强的密度充当了静电“胶水”，屏蔽了质子间的相互排斥并同时吸引它们。所得状态的能量低于分离的原子；这就是**[成键分子轨道](@keyword=bonding_molecular_orbitals|lang=zh-CN|style=Feynman)**。另一个解对应于反相组合（$c_A = -c_B$），它在两个质子之间产生一个[节面](@keyword=nodal_planes|lang=zh-CN|style=Feynman)——一个电子密度为零的区域。没有了胶水，质子之间会强烈排斥。这个状态的能量高于分离的原子；它就是**[反键分子轨道](@keyword=antibonding_molecular_orbitals|lang=zh-CN|style=Feynman)**。

想一想发生了什么。我们从一个简单、直观的猜测和一个基本的最小化原理出发，结果得出了构成现代化学基础的化学键合的整个定性图像。变分原理不仅给了我们一个数字；它还告诉了我们一个关于分子为何存在的故事。

### 现代计算的指南针

在超级计算机时代，化学家和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)家几乎从不精确求解薛定谔方程。相反，他们使用复杂的近似方法，而[变分原理](@keyword=variational_principles|lang=zh-CN|style=Feynman)是他们不可或缺的向导。

现代计算化学的核心在于对[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)做出一个非常有根据的猜测。这个“猜测”是由一组称为**[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)**的预定义数学函数构建的。变分原理提供了一个明确的改进策略：你的[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)越灵活、越完备，[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)就有越多的自由度来找到其真实形状，你计算出的能量就会越低——因此也越好。如果你用一个小[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)计算一个分子的能量，然后再用一个更大、更灵活的[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)计算，能量保证会降低（或保持不变）[@problem_id:2460566]。这使得化学家可以通过使用一系列不断改进的[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)来系统地逼近他们理论模型的“正确”答案，并且始终知道他们正朝着正确的方向前进。

该原理也解释了一些行业内不那么明显的技巧。例如，为了精确模拟甲烷（$CH_4$），计算化学家会在碳原子的[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)中包含 $d$ 型函数。这乍一看很奇怪，因为[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)碳原子的[电子构型](@keyword=electron_configurations|lang=zh-CN|style=Feynman)是 $1s^22s^22p^2$，在 $d$ 轨道上没有电子。我们是说碳原子被提升到了一个更高的能态吗？完全不是。[变分原理](@keyword=variational_principles|lang=zh-CN|style=Feynman)揭示了真相：$d$ 函数的存在不是为了像[原子轨道](@keyword=atomic_orbitals|lang=zh-CN|style=Feynman)那样被“占据”。它们是提供必要角向灵活性的数学工具，使得 $s$ 和 $p$ 轨道能够扭曲或*极化*，形成与氢原子之间强[共价键](@keyword=covalent_bonding|lang=zh-CN|style=Feynman)的最佳形状。通过混入一小部分 $d$ 函数，[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)可以更好地将电子密度转移到成键区域，从而降低总能量。变分原理用一个更好的答案来奖励这种增加的灵活性，不是因为原子“使用”了它的 $d$ 轨道，而是因为对[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)的数学描述得到了改善[@problem_id:2450943]。

这揭示了其背后物理学深刻而优美的一面。在计算中实施的[变分方法](@keyword=variational_methods|lang=zh-CN|style=Feynman)，就像一个自动雕刻机。我们给它一块“黏土”（[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)），它会不懈地雕刻和塑造它，以在这些限制内找到可能的最低能量形式。

此外，该原理还提供了一个关键的“安全网”。基于变分原理的方法，如[组态相互作用](@keyword=configuration_interaction|lang=zh-CN|style=Feynman)（CI），所得到的能量是在给定[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)内对真实能量的严格上限。例如，一次CISD（包含单激发和双激发的CI）计算给出的能量 $E_{\mathrm{CISD}}$ 保证高于或等于精确能量 $E_{\mathrm{FCI}}$，因为它的搜索空间是全空间的子集[@problem_id:2452159]。这与其它流行的方法，如 Møller–Plesset 微扰理论（例如 MP2），形成了鲜明对比，后者不是变分的。一次 MP2 计算有时可能会“过头”并给出一个非物理地*低于*精确答案的能量。[变分方法](@keyword=variational_methods|lang=zh-CN|style=Feynman)绝不会犯这种错误。

### 谨慎地航行在量子世界

这个原理很强大，但并非万无一失。它有其自身的精妙之处，理解它们能加深我们对量子世界的欣赏。

量子领域最深刻的规则之一是，由相同[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)（如电子）组成的系统的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)必须是反对称的——即如果你交换任意两个粒子，它必须变号。如果我们忽略这条规则会发生什么？假设我们构建一个试探波函数，它只是单电子函数的简单乘积，即所谓的哈特里乘积。这个函数不是反对称的。如果我们使用这个“非法”[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)来最小化能量，我们可能会发现一个*低于*真实[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)[基态能量](@keyword=ground_state_energy_2|lang=zh-CN|style=Feynman)的能量值[@problem_id:2912814]。这是否违反了[变分原理](@keyword=variational_principles|lang=zh-CN|style=Feynman)？不！该原理承诺的是对*相同对称性类别中*最低能量状态的上限。因为我们的无对称性[试探函数](@keyword=trial_function|lang=zh-CN|style=Feynman)不属于反[对称空间](@keyword=symmetric_spaces|lang=zh-CN|style=Feynman)，所以它为绝对（[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)）[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)提供了一个界限，而不是[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。通过忽略[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)，我们让我们假设的电子挤进了同一个低能态，从而获得了一个非物理的低能量。这惊人地展示了泡利原理的力量：[反对称性](@keyword=anti_symmetry|lang=zh-CN|style=Feynman)是一种*提高*系统能量的约束，它赋予了[元素周期表结构](@keyword=periodic_table_structure|lang=zh-CN|style=Feynman)，并防止所有物质坍缩成一个致密的团块。

该原理对更低能量的不懈追求也可能产生计算假象。在计算两个分子A和B之间的弱相互作用能时，一个简单的方法是计算A-B二聚体的能量，然后减去孤立的A和B的能量。然而，在二聚体计算中，分子A可以“借用”分子B的[基函数](@keyword=basis_functions|lang=zh-CN|style=Feynman)来降低自身的能量，这是它在孤立时没有的非物理优势。这种现象被称为[基组重叠误差](@keyword=basis_set_superposition_error|lang=zh-CN|style=Feynman)（BSSE），会导致人为增强的[相互作用能](@keyword=interaction_energy|lang=zh-CN|style=Feynman)[@problem_id:2927936]。[变分原理](@keyword=variational_principles|lang=zh-CN|style=Feynman)在寻找最低能量方面非常有效，以至于它会利用计算设置中的任何缺陷。需要基于对这种效应的理解进行巧妙的校正，才能获得具有物理意义的结果。

### 超越[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)：探索激发世界

到目前为止，我们一直关注[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。但世界充满了色彩、光化学和视觉——所有这些都是[电子激发态](@keyword=excited_electronic_states|lang=zh-CN|style=Feynman)的现象。[变分原理](@keyword=variational_principles|lang=zh-CN|style=Feynman)也可以扩展到寻找这些状态。Courant-Fischer“最小-最大”定理告诉我们，第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)，例如，是在*受限于与[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)正交的约束下*，使能量最小化的状态。更高的状态是通过依次强制与所有更低的状态正交来找到的。

像单激发[组态相互作用](@keyword=configuration_interaction|lang=zh-CN|style=Feynman)（CIS）这样的方法就应用了这一思想。它们在仅由哈特里-福克[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的单激发构成的空间内寻找最低能量的状态[@problem_id:2452248]。这是在该有限[模型空间](@keyword=model_space|lang=zh-CN|style=Feynman)内的“变分”搜索。然而，一个关键的微妙之处出现了。与[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)不同，CIS [激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的能量*不*保证是该[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)真实能量的上限。原因在于，真实的[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)不仅包含单激发，还包含双激发、三激发和更高阶的激发，而CIS忽略了这些。此外，计算出的*激发能*（[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)和基态能量之差）会受到不可预测的误差抵消的影响，因为这两个态的[近似误差](@keyword=approximation_error|lang=zh-CN|style=Feynman)是不同的。这突显了描述[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的挑战性增加，在[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)中，[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)[变分原理](@keyword=variational_principles|lang=zh-CN|style=Feynman)的“安全网”被削弱了。

### 前沿：[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机中的古老原理

人们可能会认为，一个诞生于量子理论黎明时期的原理，现在应该早已被取代。恰恰相反，它比以往任何时候都更加重要，并且正处于[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机最有前途的应用之一的核心位置。

[变分量子本征求解器](@keyword=variational_quantum_eigensolver|lang=zh-CN|style=Feynman)（VQE）是一种旨在在近期量子设备上寻找分子能量的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)。其策略是纯粹的[瑞利-里兹方法](@keyword=rayleigh_ritz_method|lang=zh-CN|style=Feynman)。一台[经典计算](@keyword=classical_computation|lang=zh-CN|style=Feynman)机为[量子线路](@keyword=quantum_circuits|lang=zh-CN|style=Feynman)提出一组参数 $\boldsymbol{\theta}$。然后，该线路在[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)上制备一个[试探波函数](@keyword=trial_wavefunction|lang=zh-CN|style=Feynman) $| \psi(\boldsymbol{\theta}) \rangle$。[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机测量哈密顿量的[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman) $\langle \psi(\boldsymbol{\theta}) | \hat{H} | \psi(\boldsymbol{\theta}) \rangle$。这个能量值被反馈给经典计算机，后者充当优化器，提出一组新的参数来降低能量。这个“混合”的量子-经典循环正是变分原理在起作用，寻找[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机所能创造出的最优[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)。

但在这里，我们也面临一个挑战：VQE 会自然地试图找到[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)，这种现象被称为“[变分坍缩](@keyword=variational_collapse|lang=zh-CN|style=Feynman)”。我们如何才能找到[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)呢？答案再一次是，对称性。如果目标[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)具有与[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)不同的对称性（例如，属于不同的不可约表示），我们可以设计[量子线路](@keyword=quantum_circuits|lang=zh-CN|style=Feynman)，使其*只*产生具有正确目标对称性的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)。这迫使 VQE 在*该对称性扇区内*寻找最低能量状态，从而巧妙地避免了向[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的坍缩，并允许我们描绘出[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的能量图景[@problem_id:2823802]。

从一个关于“好猜测”的简单想法，到解释[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)，指导全球计算工作，再到为未来的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机提供动力，[瑞利-里兹变分原理](@keyword=rayleigh_ritz_variational_principle|lang=zh-CN|style=Feynman)揭示了它的本质：它不仅仅是一个公式，而是一个关于自然如何运作的深刻、统一且持久美丽的思想。它证明了在科学中，最强大的思想往往是最简单的。