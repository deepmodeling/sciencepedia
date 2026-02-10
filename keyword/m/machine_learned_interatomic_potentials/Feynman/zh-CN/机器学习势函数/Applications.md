## 应用与跨学科联系

在我们之前的讨论中，我们深入了解了机器学习[原子间势](@keyword=interatomic_potentials|lang=zh-CN|style=Feynman)的内部工作原理，理解了它们如何将极其复杂的量子力学定律提炼成一种计算高效的形式。我们看到，它们本质上是高度复杂的[函数近似](@keyword=function_approximation|lang=zh-CN|style=Feynman)器，被训练来复制原子舞蹈于其上的[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)。

现在，我们提出那个真正重要的问题：我们能用这样的工具*做*什么？正如我们即将看到的，答案是极其广泛的。拥有一个快速而准确的[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)地图，就像是拿到了一把通往材料世界的万能钥匙。它解锁了从原子层面模拟、预测并最终设计物质的能力。这段旅程将带我们从构建势函数本身的复杂工艺，到其在预测材料性质中的应用，甚至到机器学习与量子力学合作解决巨大复杂性问题的前沿领域。

### 锻造工具：构建[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)的艺术与科学

一个有用的势函数并非一蹴而就。它必须有目的地、小心地被锻造。一个MLIP的好坏取决于它所学习的数据，而它的创建是物理学、统计学和计算机科学之间迷人的相互作用。

#### 蓝图：原子世界的图书馆

想象一下你想为一种新合金构建一个[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)。你应该给它喂什么数据？你可能很想只计算其最稳定[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)的能量。但这就像通过背诵一个句子来学习一门语言一样。这样的[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)会极其脆弱，无法描述除了绝对零度下完美的、静止的晶体之外的任何东西。

一个稳健的势函数必须在一个多样化的原[子环](@keyword=subring|lang=zh-CN|style=Feynman)境组合上进行训练，一个原子可能栖居其中的各种可能世界的真实图书馆。正如该领域的最佳实践所示，这个图书馆不仅必须包括完美的晶体，还必须包括受应变的晶体、带有缺陷（如缺失原子，即空位）的晶体，以及材料表面的独特环境[@problem_id:3422821]。此外，由于材料很少处于绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)，我们必须包括原子在有限温度下[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)和碰撞的快照，这些快照可以从简短但高精度的*ab initio*[分子动力学模拟](@keyword=molecular_dynamics_simulations|lang=zh-CN|style=Feynman)中生成。在如此丰富的数据集上训练的[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)，能在广泛的背景下学习相互作用的规则，使其具有可迁移性和强大的功能。

#### 智能探索：主动学习

即使有了这个蓝图，所有可能的原子构型的空间也是天文数字般巨大。我们不可能用昂贵的量子力学计算来计算每一种情景。这时，过程变得巧妙起来。我们不预先生成所有数据，而是采用一种称为**主动学习**的策略。

把它想象成派遣一个聪明的探险家进入[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)的广阔未知地形。我们从在一个小的初始“种子”数据集上训练一个临时的势函数开始。然后，我们使用这个初步模型来运行非常快速的经典模拟。在这些模拟过程中，探险家使用一个特殊的指南针：**不确定性量化**。对于一个给定的原子构型，模型可以估计其自身的不确定性。对于一个由多个神经网络势组成的委员会模型，成员之间的高度[分歧](@keyword=ramification|lang=zh-CN|style=Feynman)标志着高度不确定性[@problem_id:3422821]。对于高斯近似势，预测[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)也起到同样的作用。

当探险家遇到一个[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)不确定的构型——即它在“外推”到未知领域时——它会标记该构型。然后我们对那个特定的、[信息量](@keyword=information_content|lang=zh-CN|style=Feynman)极大的构型进行一次昂贵的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)，并将其添加到我们的训练库中。我们重新训练[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)，并再次派出探险家。这个迭代循环使得[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)能够高效学习，将计算精力精确地集中在最需要的地方。这种查询驱动的方法被证明在降低模型最终[泛化误差](@keyword=generalization_error|lang=zh-CN|style=Feynman)方面比被动抽样随机构型更有效，因为它通过填补其知识中最关键的空白来智能地改进模型[@problem_id:3394195]。

#### 妥协的艺术：多目标拟合

通常，我们需要一个势函数不仅仅是准确预测能量。为了研究力学性质，我们需要它高保真地预测原子上的力和宏观应力张量。这些不同的目标可能是相互竞争的；一套对能量极佳的模型参数可能对力表现平平。

因此，开发一个顶尖的[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)涉及[多目标优化](@keyword=multiobjective_optimization|lang=zh-CN|style=Feynman)。我们定义一个[损失函数](@keyword=loss_functions|lang=zh-CN|style=Feynman)，它是能量、力和应力误差的加权和[@problem_id:3498443]。通过使用不同权重集训练模型，我们描绘出所谓的**帕累托前沿**——一组最优模型，在这些模型上你无法在不牺牲另一个目标（比如能量精度）的情况下改善一个目标（比如力精度）。然后，[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)家可以从这个前沿中选择一个特定的模型，该模型代表了他们特定应用的最佳折衷，无论是研究断裂（力至关重要）还是相稳定性（能量差异是关键）。

### 试金石：确保物理真实性

在我们能够自信地将新锻造的势函数部署到模拟中之前，我们必须对其进行严格的测试，以确保它不仅仅是记住了数据点，而是学到了底层的物理学。

#### 应力、应变与虚功原理

一个最基本的[自洽性](@keyword=self_consistency|lang=zh-CN|style=Feynman)检验将原子的微观世界与力的世界和[连续介质力学](@keyword=continuum_mechanics|lang=zh-CN|style=Feynman)的宏观世界联系起来。描述材料[内力](@keyword=internal_forces|lang=zh-CN|style=Feynman)的应力张量$\boldsymbol{\sigma}$，可以与无穷小变形（应变）下能量的变化相关联。这是[虚功原理](@keyword=principle_of_virtual_work|lang=zh-CN|style=Feynman)的直接结果。

同时，应力张量也可以通过著名的**维里表达式**计算得出，该表达式涉及原子上的力和它们位置的求和[@problem_id:3422800]。这两种计算应力的途径——一种来自能量对应变的导数，另一种来自原子受力——必须得出相同的结果。验证一个[机器学习势函数](@keyword=machine_learning_potentials|lang=zh-CN|style=Feynman)是否满足这个等式，通常称为[应力-应变关系](@keyword=stress_strain_relationship|lang=zh-CN|style=Feynman)，是一个关键的验证步骤[@problem-id:3422788]。通过这个测试的势函数正确地学习了能量、力和变形之间的复杂关系，并且可以被信任用于[材料力学](@keyword=mechanics_of_materials|lang=zh-CN|style=Feynman)响应的模拟。

#### 原子的交响曲：[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)模式

晶体中的原子不是静止的；它们围绕其[平衡位置](@keyword=equilibrium_position|lang=zh-CN|style=Feynman)不断[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。这些[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)不是随机的，而是以同步的模式发生，称为[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式或**[声子](@keyword=phonon|lang=zh-CN|style=Feynman)**。每个模式都有一个特征频率和一种原子位移模式，就像小提琴弦的不同泛音。

这些[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)模式的完整集合——材料的声子谱——可以通过计算势能的[二阶导数](@keyword=second_derivative|lang=zh-CN|style=Feynman)得到，这些[二阶导数](@keyword=second_derivative|lang=zh-CN|style=Feynman)构成一个称为**Hessian矩阵**的矩阵。Hessian矩阵的[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)给出了模式频率的平方，而[特征向量](@keyword=eigenvector|lang=zh-CN|style=Feynman)描述了它们的形状[@problem_id:3446856]。一个MLIP必须能够准确地再现量子力学预测的声子谱。这是一个严格的测试，因为它探测了势能井在最小值附近的细微曲率。比较[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)谱并进行仔细的“[模式匹配](@keyword=pattern_matching|lang=zh-CN|style=Feynman)”以比较[特征向量](@keyword=eigenvector|lang=zh-CN|style=Feynman)的形状，为势函数的保真度提供了深入而详细的验证，这对于预测[热容](@keyword=heat_capacity|lang=zh-CN|style=Feynman)和热导率等热学性质至关重要。

### 回报：预测物质的性质

手握一个经过验证的势函数，我们终于可以开始收获回报。MLIPs使得对数百万个原子进行纳秒或更长时间的分子动力学模拟成为可能，这个尺度远远超出了直接量子力学方法的范围。这为从[第一性原理计算](@keyword=ab_initio_calculations|lang=zh-CN|style=Feynman)大量材料性质打开了大门。

#### 探索新材料：相稳定性与凸包

[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)的核心目标之一是发现新的、稳定的化合物。对于一种[二元合金](@keyword=binary_alloy|lang=zh-CN|style=Feynman)，比如说在元素A和B之间，我们如何知道哪些组分$A_{1-x}B_x$会形成稳定的固体，哪些会自发分离？

[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)提供了一个优美而明确的答案：**凸包**。如果我们将每种可能[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)的形成能作为组分$x$的函数绘制出来，[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)稳定的相将是那些位于这组点集的下[凸包](@keyword=convex_hull|lang=zh-CN|style=Feynman)上的相[@problem_id:3441337]。任何能量高于此[凸包](@keyword=convex_hull|lang=zh-CN|style=Feynman)的结构都是[亚稳态](@keyword=metastable_states|lang=zh-CN|style=Feynman)或不稳定的，并且在有机会的情况下，会分解成凸包上稳定相的混合物。

构建这个[凸包](@keyword=convex_hull|lang=zh-CN|style=Feynman)需要计算数千个候选结构的能量，这对量子力学来说是一项艰巨的任务。在这里，MLIPs大放异彩。它们可以快速预测所有这些候选结构的能量。为确保最高精度，我们可以采用一种**多保真度**方法：对所有结构使用快速的MLIP，然后对一小部分战略性选择的点进行少量昂贵的、高保真度的DFT计算。然后，一个统计模型，如[协同克里金法](@keyword=co_kriging|lang=zh-CN|style=Feynman)，可以学习MLIP和DFT之间的差异，创建一个高精度的、校准过的能量景观。这种MLIPs、DFT和[统计学习](@keyword=statistical_learning|lang=zh-CN|style=Feynman)的强大组合使我们能够以前所未有的速度绘制[相图](@keyword=phase_portrait|lang=zh-CN|style=Feynman)并加速新材料的发现。

#### 晶体的特性：缺陷与表面

真实的材料从不是完美的。它们的性质通常由缺陷主导——缺失的原子、额外的原子，或像表面和晶界那样的界面。例如，金属的强度由[位错](@keyword=dislocation|lang=zh-CN|style=Feynman)（一种[线缺陷](@keyword=line_defects|lang=zh-CN|style=Feynman)）如何移动来控制，而材料的催化活性由其[表面化学](@keyword=surface_chemistry|lang=zh-CN|style=Feynman)决定。

这些缺陷创造了复杂的、非周期性的原[子环](@keyword=subring|lang=zh-CN|style=Feynman)境，模拟起来计算成本高昂。MLIPs使得模拟包含这些缺陷的大型超胞并以量子精度计算其性质成为可能[@problem_id:3422823]。我们可以计算创建一个空位所需的能量，这是理解材料中[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)和蠕变的关键参数。我们可以计算[表面能](@keyword=surface_energy|lang=zh-CN|style=Feynman)，它决定了晶体形状和[润湿](@keyword=wetting|lang=zh-CN|style=Feynman)行为。一个关键的挑战是确保[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)是*可迁移的*——即一个主要在体材料数据上训练的模型仍然能在这些不同的缺陷环境中表现良好。在使用[势函数](@keyword=potential_functions|lang=zh-CN|style=Feynman)进行此类预测之前，严格的测试是必不可少的。

#### 终极[相变](@keyword=phase_change|lang=zh-CN|style=Feynman)：预测熔化

材料的[熔点](@keyword=melting_temperature|lang=zh-CN|style=Feynman)是多少？这个看似简单的问题从第一性原理出发却非常难以回答。它是固相和液相处于完美平衡、具有完全相同[吉布斯自由能](@keyword=gibbs_free_energy|lang=zh-CN|style=Feynman)的温度。

计算熔点最可靠的方法之一是**共存模拟**，即将一块固体材料与其液相在一个模拟盒子中直接接触。通过仔细控制温度，可以找到[固液界面](@keyword=solid_liquid_interface|lang=zh-CN|style=Feynman)保持静止、既不增长也不收缩的点。这些模拟必须足够大以容纳两相，并且足够长以使系统达到平衡。

MLIPs使得这种要求苛刻的模拟成为可能[@problem_id:3500199]。但更令人兴奋的是，它们允许我们更进一步，并提问：我们预测的熔化温度有多可靠？通过在相同数据的略有不同的[子集](@keyword=subset|lang=zh-CN|style=Feynman)上训练一个MLIPs集成模型（一种称为[自助法](@keyword=bootstrap_method|lang=zh-CN|style=Feynman)的技术），我们可以得到一系列预测的[熔点](@keyword=melting_temperature|lang=zh-CN|style=Feynman)。这些预测的散布直接度量了我们结果中的不确定性，这种不确定性源于训练数据的局限性。这种分析可能会揭示，例如，我们的预测不确定是因为我们的训练集缺乏对远离平衡结构的液体构型的足够覆盖。这种物理模拟和[统计不确定性](@keyword=statistical_uncertainty|lang=zh-CN|style=Feynman)量化的融合，代表了[计算材料科学](@keyword=computational_materials_science|lang=zh-CN|style=Feynman)在成熟度和预测能力上的重大飞跃。

### 前沿：混合模型与未来

展望未来，MLIPs的角色正在从简单地替代量子力学演变为成为其智能伙伴。化学和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)中许多最有趣的现象，如催化或电池运行，都涉及一个关键事件（如[化学键](@keyword=chemical_bonding|lang=zh-CN|style=Feynman)的断裂）发生在一个特定的、小的区域——酶的[活性位点](@keyword=active_site|lang=zh-CN|style=Feynman)、催化剂的表面——嵌入在一个更大的环境中。

用昂贵的QM方法处理整个系统是计算上的浪费。前沿在于**混合QM/ML模型**[@problem_id:3462491]。在这些方案中，小的、化学活性区域由高精度QM描述，而广阔的、不那么关键的周围环境由快速可靠的MLIP处理。关键的挑战是无缝地耦合这两个区域，确保总能量是一致的，并且在界面处不会产生人为的、“伪”力。如果做得正确，这种QM/ML嵌入方法提供了两全其美的优势：描述键断裂和形成所需的量子精度，以及模拟现实环境所需的计算速度。这种强大的协同作用有望解锁前所未有规模和复杂性的模拟，推动我们建模、理解和设计能力的边界。