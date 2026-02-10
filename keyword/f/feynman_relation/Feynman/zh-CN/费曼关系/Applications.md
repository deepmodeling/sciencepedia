## 应用与跨学科联系

在了解了赫尔曼-费曼定理的基本原理之后，你可能会想：“这一切都非常优雅，但它到底有什么*用*？”这是一个合理的问题，答案也异常广泛。这个[能量导数](@keyword=energy_derivative|lang=zh-CN|style=Feynman)与[哈密顿量](@keyword=hamiltonian|lang=zh-CN|style=Feynman)[导数](@keyword=derivative|lang=zh-CN|style=Feynman)[期望值](@keyword=e_value|lang=zh-CN|style=Feynman)之间的简单关系，并非某个晦涩的理论奇谈。它是一个强大的透镜，通过它我们可以理解和预测物质的行为，从分子中原子的舞蹈，到[化学反应](@keyword=chemical_reactions|lang=zh-CN|style=Feynman)中的光芒闪烁，甚至进入了科学领域中[人工智能](@keyword=artificial_intelligence|lang=zh-CN|style=Feynman)的新兴世界。这是物理学中那些深刻的定理之一，似乎提供了一份“免费的午餐”——如果你知道一件事（[哈密顿量](@keyword=hamiltonian|lang=zh-CN|style=Feynman)如何变化），你就能以惊人的简易性得到另一件事（能量如何变化）。

让我们来探索这份“免费的午餐”可以在哪里享用。

### 化学家的工具箱：塑造分子与反应

想象一下你想建造任何东西——一座桥、一辆车、一种[酶](@keyword=enzymes|lang=zh-CN|style=Feynman)。你需要知道力。什么是[推力](@keyword=thrust|lang=zh-CN|style=Feynman)？什么是拉力？原子和分子的世界并无不同。为了预测[蛋白质](@keyword=proteins|lang=zh-CN|style=Feynman)如何折叠成其活性形状，药物如何与其靶点结合，或者[催化剂](@keyword=catalysts|lang=zh-CN|style=Feynman)如何加速反应，我们需要知道每个原子在每一瞬间所受的力。但是，你如何计算一个[原子核](@keyword=nucleus|lang=zh-CN|style=Feynman)所受的力？它正被一团由复杂[波函数](@keyword=wave_functions|lang=zh-CN|style=Feynman)描述的飞速运动的[电子](@keyword=electrons|lang=zh-CN|style=Feynman)所冲击。

赫尔曼-费曼定理提供了一个惊人简单的答案。力就是能量相对于[原子核](@keyword=nucleus|lang=zh-CN|style=Feynman)位置的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)。因此，如果我们让参数$\lambda$是一个核坐标，比如说$R_{\alpha}$，该定理告诉我们力分量$F_{\alpha}$是：

$F_{\alpha} = -\frac{\mathrm{d}E}{\mathrm{d}R_{\alpha}} = - \left\langle \psi \left| \frac{\partial H}{\partial R_{\alpha}} \right| \psi \right\rangle$

算符$\frac{\partial H}{\partial R_{\alpha}}$原来不过是势能的[梯度](@keyword=gradient|lang=zh-CN|style=Feynman)——它简单地与[电子](@keyword=electrons|lang=zh-CN|style=Feynman)和其他[原子核](@keyword=nucleus|lang=zh-CN|style=Feynman)对该[原子核](@keyword=nucleus|lang=zh-CN|style=Feynman)施加的经典[静电力](@keyword=electrostatic_forces|lang=zh-CN|style=Feynman)有关。所以，要找到[量子力学力](@keyword=quantum_mechanical_forces|lang=zh-CN|style=Feynman)，你“只需”计算经典力算符的[期望值](@keyword=e_value|lang=zh-CN|style=Feynman)！这一洞见是整个*[从头算](@keyword=ab_initio|lang=zh-CN|style=Feynman)*[分子动力学](@keyword=molecular_dynamics|lang=zh-CN|style=Feynman)领域的理论引擎，使我们能够生成[分子运动](@keyword=molecular_motion|lang=zh-CN|style=Feynman)的动画，其中的力是直接根据[量子力学](@keyword=quantum_mechanics|lang=zh-CN|style=Feynman)定律计算的[@problem_id:2903788]。

当然，自然界很少会提供完全免费的午餐。简单的赫尔曼-费曼关系只有在我们的[波函数](@keyword=wave_functions|lang=zh-CN|style=Feynman)$\psi$是[薛定谔方程](@keyword=schrödinger_equation|lang=zh-CN|style=Feynman)的*精确*解时才完全成立。在[计算化学](@keyword=computational_chemistry|lang=zh-CN|style=Feynman)的现实世界中，我们几乎总是使用由有限[基组](@keyword=basis_sets|lang=zh-CN|style=Feynman)（通常是以每个[原子核](@keyword=nucleus|lang=zh-CN|style=Feynman)为中心的[原子轨道](@keyword=atomic_orbitals|lang=zh-CN|style=Feynman)）构建的近似[波函数](@keyword=wave_functions|lang=zh-CN|style=Feynman)。当一个[原子核](@keyword=nucleus|lang=zh-CN|style=Feynman)移动时，以它为中心的[基函数](@keyword=basis_functions|lang=zh-CN|style=Feynman)也会移动。这意味着我们用来测量[波函数](@keyword=wave_functions|lang=zh-CN|style=Feynman)的“尺子”在我们试图计算[导数](@keyword=derivative|lang=zh-CN|style=Feynman)时正在改变。这引入了一个修正项，一个由我们描述框架本身运动引起的虚拟力。这个项就是著名的**[Pulay力](@keyword=pulay_forces|lang=zh-CN|style=Feynman)**[@problem_id:2457267] [@problem_id:2922374]。承认这些力的存在是得到正确答案的关键一步，这是一个谦卑的提醒：我们的近似会产生真实的物理后果。

### 世界[碰撞](@keyword=collision|lang=zh-CN|style=Feynman)之处：光与生命的物理学

当考虑单个孤立的[能级](@keyword=energy_levels|lang=zh-CN|style=Feynman)时，该定理的简单形式工作得非常好。但是当两个[能级](@keyword=energy_levels|lang=zh-CN|style=Feynman)非常接近，甚至试图[交叉](@keyword=chiasmata|lang=zh-CN|style=Feynman)时会发生什么呢？这并非罕见现象；当分子[吸收](@keyword=absorption|lang=zh-CN|style=Feynman)光时，这种情况时有发生，并且是理解[光化学](@keyword=photochemistry|lang=zh-CN|style=Feynman)、视觉和[光合作用](@keyword=photosynthesis|lang=zh-CN|style=Feynman)的关键。

在这些被称为**[避免交叉](@keyword=avoided_crossings|lang=zh-CN|style=Feynman)**或**[锥形交叉](@keyword=conical_intersections|lang=zh-CN|style=Feynman)**的点上，系统进入一个微妙、高风险的状态。简单的赫尔曼-费曼定理似乎失效了。你不能再谈论单个[能级](@keyword=energy_levels|lang=zh-CN|style=Feynman)的“那个”[导数](@keyword=derivative|lang=zh-CN|style=Feynman)，因为[能级](@keyword=energy_levels|lang=zh-CN|style=Feynman)正在混合。但这种“失效”实际上是物理学变得有趣的标志。该定理并没有被打破；它被推广了。对于两个能量上接近的不[同态](@keyword=structure_preserving_map|lang=zh-CN|style=Feynman)$|m\rangle$和$|n\rangle$，一个“非对角”版本的定理将它们的相互作用与[哈密顿量](@keyword=hamiltonian|lang=zh-CN|style=Feynman)的变化联系起来[@problem_id:2655304] [@problem_id:2873418]：

$(E_n - E_m) \langle \psi_m | \partial_{\lambda} \psi_n \rangle = \langle \psi_m | \partial_{\lambda} H | \psi_n \rangle$

左边的项$\langle \psi_m | \partial_{\lambda} \psi_n \rangle$被称为**[非绝热耦合](@keyword=nonadiabatic_coupling|lang=zh-CN|style=Feynman)**。它衡量了当我们改变参数$\lambda$（例如，移动原子）时，态$|n\rangle$的特性向态$|m\rangle$方向变化的程度。仔细看这个方程。耦合与[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)$E_n - E_m$成反比。当[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)$\Delta = E_n - E_m$在[避免交叉](@keyword=avoided_crossings|lang=zh-CN|style=Feynman)点附近缩小到几乎为零时，[非绝热耦合](@keyword=nonadiabatic_coupling|lang=zh-CN|style=Feynman)会变得巨大，其标度为$\mathcal{O}(1/\Delta)$[@problem_id:2922374]。

这种爆发性的行为意味着，即使是核位置的微小震颤也可能导致[电子态](@keyword=electronic_states|lang=zh-CN|style=Feynman)的灾难性混合。系统在[吸收](@keyword=absorption|lang=zh-CN|style=Feynman)一个[光子](@keyword=photons|lang=zh-CN|style=Feynman)后可能一直安稳地处于一个能面上，但突然之间可能“跳”到另一个能面上。这种超快的、非辐射的跃迁是视觉第一步——你眼中视网醛分子的异构化——以及无数其他[光化学](@keyword=photochemistry|lang=zh-CN|style=Feynman)过程背后的基本机制。广义的赫尔曼-费曼关系为我们提供了[量化](@keyword=quantization|lang=zh-CN|style=Feynman)这种关键的、改变世界的跳跃的关键。

### 更深层的结构：[简并](@keyword=degeneracy|lang=zh-CN|style=Feynman)中的统一

那么，当处在一个精确的[简并](@keyword=degeneracy|lang=zh-CN|style=Feynman)点，即多个态共享完全相同的能量时，我们该怎么办？在这里，从[简并](@keyword=degeneracy|lang=zh-CN|style=Feynman)群中任意挑选一个态并将其代入简单的赫尔曼-费曼公式会得到无意义的结果。问题在于，一个任意的态是“不稳定”的——对系统的无限小扰动会立即打破[简并](@keyword=degeneracy|lang=zh-CN|style=Feynman)，并挑选出原始态的一个非常特定的组合。

物理学以其优雅提供了一条稳健的前进之路。我们必须在[简并态](@keyword=degenerate_states|lang=zh-CN|style=Feynman)的[子空间](@keyword=subspace|lang=zh-CN|style=Feynman)内对扰动算符$\partial_{\lambda} H$进行[对角化](@keyword=diagonalization|lang=zh-CN|style=Feynman)。这个小[矩阵](@keyword=matrix|lang=zh-CN|style=Feynman)的[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)给出了[分裂](@keyword=fission|lang=zh-CN|style=Feynman)[能级](@keyword=energy_levels|lang=zh-CN|style=Feynman)的真实一阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)，其[特征向量](@keyword=eigenvector|lang=zh-CN|style=Feynman)告诉我们应该使用的“正确”的态——即那些赫尔曼-费曼定理对它们各自成立的态[@problem_id:2457267] [@problem_id:2922374] [@problem_id:2930781]。

我们甚至可以做出一个更深刻、与基无关的陈述。如果我们不关心单个[能级](@keyword=energy_levels|lang=zh-CN|style=Feynman)如何[分裂](@keyword=fission|lang=zh-CN|style=Feynman)，而只关心由$m$个态组成的[简并](@keyword=degeneracy|lang=zh-CN|style=Feynman)群整体的行为，我们可以简单地将它们的[能量导数](@keyword=energy_derivative|lang=zh-CN|style=Feynman)相加。这个和被证明等于投影到[简并](@keyword=degeneracy|lang=zh-CN|style=Feynman)[子空间](@keyword=subspace|lang=zh-CN|style=Feynman)上的扰动[算符的迹](@keyword=trace_of_an_operator|lang=zh-CN|style=Feynman)[@problem_id:2922374] [@problem_id:2930781]：

$\sum_{k=1}^{m} \frac{dE_k}{d\lambda} = \mathrm{Tr}[P_0 \, \partial_{\lambda}H]$

其中$P_0$是到该[子空间](@keyword=subspace|lang=zh-CN|style=Feynman)的[投影算符](@keyword=projection_operators|lang=zh-CN|style=Feynman)。这个“求和规则”之所以优美，是因为迹与你选择的基无关。它告诉我们，即使单个态的属性变得模糊不清，集体[流形](@keyword=manifolds|lang=zh-CN|style=Feynman)的一个稳健、具有物理意义的属性仍然存在。它在模糊中找到了统一。

### 新前沿：费曼与学习机器

或许赫尔曼-费曼原理最令人惊讶的应用是在前沿的[科学机器学习](@keyword=scientific_machine_learning|lang=zh-CN|style=Feynman)（ML）领域。几十年来，模拟分子意味着费力地计算[波函数](@keyword=wave_functions|lang=zh-CN|style=Feynman)，然后用它们来计算力。这个过程虽然准确，但计算成本高昂。如今，一种新的[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)正在兴起：教一个[机器学习](@keyword=machine_learning|lang=zh-CN|style=Feynman)模型（如[神经网络](@keyword=neural_networks|lang=zh-CN|style=Feynman)）在仅给定原子位置的情况下预测分子的能量。

但至关重要的力呢？我们是否需要单独教机器关于力的知识？赫尔曼-费曼定理给出了一个惊人的“不”。如果一个ML模型是可[微分](@keyword=differential|lang=zh-CN|style=Feynman)的（[神经网络](@keyword=neural_networks|lang=zh-CN|style=Feynman)就是如此），并且已经被训练能准确预测能量面$E_{\text{ML}}(\mathbf{R})$，那么我们基本上可以免费得到力，只需对模型关于原子位置取解析[导数](@keyword=derivative|lang=zh-CN|style=Feynman)，$\mathbf{F} = -\nabla_{\mathbf{R}} E_{\text{ML}}(\mathbf{R})$ [@problem_id:2903788]。该定理保证，如果学习到的能量是正确的，那么该能量的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)也将是正确的力。这一原理支撑了ML驱动的[分子模拟](@keyword=molecular_simulations|lang=zh-CN|style=Feynman)革命，使科学家能够模拟更大规模的系统、更长的时间，从而加速了新药和新材料的发现。

这种联系也教给我们一个关于学习和预测本质的基本教训。假设你想要一个ML模型来预测分子的[偶极矩](@keyword=dipole_moment|lang=zh-CN|style=Feynman)，这是其能量相对于外部[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)$\boldsymbol{\mathcal{E}}$的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)。你能够仅用无场能量计算来训练一个模型，然后以某种方式对一个它从未见过的变量求导吗？当然不能。要学习一个响应属性，模型必须是相应扰动的函数。它必须在包含[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)效应的数据上进行训练。[导数](@keyword=derivative|lang=zh-CN|style=Feynman)$\partial E / \partial \boldsymbol{\mathcal{E}}$只有在$\boldsymbol{\mathcal{E}}$是函数的输入时才有意义[@problem_id:2903788]。这是一个既涉及数学逻辑又涉及物理[因果关系](@keyword=causality|lang=zh-CN|style=Feynman)的点，赫尔曼-费曼框架完美地阐释了这一点。

从维系分子的力，到促成视觉的[量子跃迁](@keyword=quantum_transitions|lang=zh-CN|style=Feynman)，再到[机器学习](@keyword=machine_learning|lang=zh-CN|style=Feynman)的逻辑，费曼关系揭示的不是一个狭隘的公式，而是关于物理定律深层结构的陈述——一条连接着科学世界中多样而迷人角落的统一之线。