## 引言
核[磁共振](@keyword=magnetic_resonance|lang=zh-CN|style=Feynman)（NMR）波谱学是化学家不可或缺的工具，为[分子结构](@keyword=molecular_structure|lang=zh-CN|style=Feynman)提供了无与伦比的洞察力。然而，解读复杂的[光谱](@keyword=optical_spectra|lang=zh-CN|style=Feynman)往往是一个模棱两可的难题。如果我们能仅用量子力学的基本定律，从头开始预测NMR谱，会怎么样呢？这正是[密度泛函理论](@keyword=density_functional_theory|lang=zh-CN|style=Feynman)（DFT）的承诺，这种计算方法彻底改变了我们将理论模型与实验现实联系起来的能力。本文旨在弥合[量子理论](@keyword=quantum_theory|lang=zh-CN|style=Feynman)与实用[光谱学](@keyword=optical_spectroscopy|lang=zh-CN|style=Feynman)之间的鸿沟，解释如何从[第一性原理计算](@keyword=ab_initio_calculations|lang=zh-CN|style=Feynman)出[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)微妙的磁性。它解决了将电子的复杂舞蹈转化为实验室中观察到的精确化学位移和耦合常数的挑战。以下章节将引导您了解支配核屏蔽的核心量子力学原理，然后探索其广泛的应用，从解决合成化学中的[立体化学](@keyword=stereochemistry|lang=zh-CN|style=Feynman)难题到描绘结构生物学中的分子相互作用。我们的旅程始于电子云如何屏蔽[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的基础物理学，这正是[化学位移](@keyword=chemical_shift|lang=zh-CN|style=Feynman)的真正起源。

## 原理与机制

为了理解我们如何能从[第一性原理计算](@keyword=ab_initio_calculations|lang=zh-CN|style=Feynman)出NMR谱的精细信号，我们必须踏上一段旅程，它始于单个[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)在[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中的简单舞蹈，终于量子力学和[统计系综](@keyword=statistical_ensembles|lang=zh-CN|style=Feynman)的复杂世界。这是一个关于宇宙基本定律如何通过电子的演绎，产生我们从分子中获取的丰富信息的故事。

### [原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的磁性生命：屏蔽

想象一个[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)，如氢或碳原子，它是一个带有磁性的小陀螺。当我们将它置于一个强大的、均匀的外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)（我们称之为$\mathbf{B}_{0}$）中时，它不会像指南针那样简单地对齐。相反，它开始围绕[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)方向进动，或称摇摆，就像一个旋转的陀螺在地球[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)中摇摆一样。这个进动的频率，即[拉莫尔频率](@keyword=larmor_frequency|lang=zh-CN|style=Feynman)，是[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)特有的“歌声”。如果所有相同类型的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)都以相同的频率歌唱，那么NMR谱将会相当乏味——只有一个尖锐的单峰。

但分子中的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)并非孤立存在。它被一团电子云所包围。而这些电子并非被动的旁观者。当外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)$\mathbf{B}_{0}$开启时，作为运动中的[带电粒子](@keyword=charged_particle|lang=zh-CN|style=Feynman)，电子被激发产生新的环流模式。根据电磁学的美妙原理——[楞次定律](@keyword=lenz_s_law|lang=zh-CN|style=Feynman)，这些[感应电流](@keyword=induced_current|lang=zh-CN|style=Feynman)会产生它们自己的微小[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)$\mathbf{B}_{\text{ind}}$，这个[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)通常会*对抗*外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。

深藏在这片电子云中的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)，并不会感受到$\mathbf{B}_{0}$的全部力量。相反，它经历的是一个略微减弱的*有效*[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)：$\mathbf{B}_{\text{eff}} = \mathbf{B}_{0} + \mathbf{B}_{\text{ind}}$。由于感应[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)与外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)方向相反，我们说[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)被电子**屏蔽**了。我们可以定义一个比例常数，即**[屏蔽常数](@keyword=shielding_constant|lang=zh-CN|style=Feynman)**$\sigma$，来量化这种效应：$\mathbf{B}_{\text{ind}} = -\sigma \mathbf{B}_{0}$。因此，[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)实际感受到的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)是$\mathbf{B}_{\text{eff}} = \mathbf{B}_{0}(1 - \sigma)$。

这就是一切的关键。在分子中，每个[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)都有独特的化学环境，独特的电子“茧”。羰基$(\text{C=O})$中的碳原子与甲基$(-\text{CH}_3)$中的碳原子拥有不同的电子云。因此，每个[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)都有不同的[屏蔽常数](@keyword=shielding_constant|lang=zh-CN|style=Feynman)$\sigma$，并以略微不同的频率进动。NM[R波](@keyword=r_wave|lang=zh-CN|style=Feynman)谱仪检测这些微小的频率差异，为我们提供一张具有多个峰的[光谱](@keyword=optical_spectra|lang=zh-CN|style=Feynman)，这是[分子结构](@keyword=molecular_structure|lang=zh-CN|style=Feynman)的独特指纹。

出于实用目的，我们不报告绝对频率。相反，我们测量相对于标准参考化合物（通常是[四甲基硅烷](@keyword=tetramethylsilane|lang=zh-CN|style=Feynman)，TMS）的[频率偏移](@keyword=frequency_shifting|lang=zh-CN|style=Feynman)。这为我们提供了熟悉的**化学位移**标度，用$\delta$表示，单位为[百万分率](@keyword=parts_per_million|lang=zh-CN|style=Feynman)（ppm）。关系很简单：一个被屏蔽较少（$\sigma$较小）的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)将以更高的频率共振，并具有更大、更“低场”的[化学位移](@keyword=chemical_shift|lang=zh-CN|style=Feynman)。根据惯例，化学位移定义为$\delta \approx (\sigma_{\text{ref}} - \sigma) \times 10^6$ ppm [@problem_id:3697551]。

### 更深层次的审视：屏蔽张量

然而，物理学很少像一个单一数字那么简单。[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)所经历的屏蔽不仅取决于其电[子环](@keyword=subring|lang=zh-CN|style=Feynman)境，还取决于分子相对于外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的取向。分子并非一个完美的球形物体。如果[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)沿键轴方向与垂直于键轴方向，所感应的电子电流将会有所不同。

为了捕捉这种方向依赖性，我们必须将[屏蔽常数](@keyword=shielding_constant|lang=zh-CN|style=Feynman)$\sigma$从一个简单的标量提升为一个**化学屏蔽张量**$\boldsymbol{\sigma}$。这是一个数学对象，由一个3x3矩阵表示，它关联了外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)矢量和感应[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)矢量：$\mathbf{B}_{\text{ind}} = -\boldsymbol{\sigma} \mathbf{B}_{0}$。这个张量的九个分量完全描述了当[分子翻滚](@keyword=molecular_tumbling|lang=zh-CN|style=Feynman)和转动时[屏蔽效应](@keyword=shielding_effect|lang=zh-CN|style=Feynman)如何变化。

那么，为什么我们在液体样品中为每个独特的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)只观察到一个尖锐的单峰呢？因为在液体中，分子以每秒数十亿次的速度疯狂地翻滚。它们探索了相对于外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的所有可能取向。而NMR实验在更长的时间尺度上进行，只看到了平均效应。这种旋转平均的屏蔽称为**各向同性屏蔽**$\sigma_{\text{iso}}$。在这里，大自然向我们展示了一个数学上优雅的时刻：各向同性屏蔽就是屏蔽张量三个对角[线元](@keyword=line_element|lang=zh-CN|style=Feynman)素的平均值，这个量被称为迹：$\sigma_{\text{iso}} = \frac{1}{3}\mathrm{Tr}(\boldsymbol{\sigma}) = \frac{1}{3}(\sigma_{xx} + \sigma_{yy} + \sigma_{zz})$ [@problem_id:3697551]。方向依赖性屏蔽的复杂舞蹈，在[分子运动](@keyword=molecular_motion|lang=zh-CN|style=Feynman)的混沌中平均后，简化成了一个单一、可测量的数字。

### 量子引擎：DFT如何计算屏蔽

知道屏蔽*存在*是一回事；从头开始计算它则是另一回事。要做到这一点，我们必须求助于现代化学的动力室：量子力学。屏蔽张量$\boldsymbol{\sigma}$是分子电[子基](@keyword=subbasis|lang=zh-CN|style=Feynman)态的一个性质。[密度泛函理论](@keyword=density_functional_theory|lang=zh-CN|style=Feynman)（DFT）是一种特别强大且流行的量子力学方法，用于寻找这个[基态](@keyword=ground_state|lang=zh-CN|style=Feynman)的能量和电子密度。

能量与屏蔽之间的联系是深刻的。用微扰理论的语言来说，屏蔽张量正是*总电子能量*($E$)相对于外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)($\mathbf{B}$)和所讨论[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的[磁偶极矩](@keyword=magnetic_dipole_moments|lang=zh-CN|style=Feynman)($\boldsymbol{\mu}_{K}$)的*混合[二阶导数](@keyword=second_derivative|lang=zh-CN|style=Feynman)* [@problem_id:2454762] [@problem_id:3697551]。用数学术语表示，张量的一个分量由下式给出：
$$ \sigma_{\alpha\beta}(K) = \frac{\partial^2 E}{\partial B_\alpha \partial \mu_{K,\beta}} $$
这意味着屏蔽告诉我们[分子能量](@keyword=molecular_energy|lang=zh-CN|style=Feynman)如何*响应*同时受到两种不同磁探针的扰动。

这种响应可以从概念上分解为两个相反的贡献，最早由Norman Ramsey描述：

*   **[抗磁屏蔽](@keyword=diamagnetic_shielding|lang=zh-CN|style=Feynman)($\sigma_d$)：** 这是[基态](@keyword=ground_state|lang=zh-CN|style=Feynman)电子云的直接、直观的响应，其作用类似于一个完美的微观[涡流](@keyword=vortex_flow|lang=zh-CN|style=Feynman)来对抗外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。它总是增加屏蔽（降低化学位移），并由电子云在未受扰动状态下的形状决定。

*   **[顺磁屏蔽](@keyword=paramagnetic_shielding|lang=zh-CN|style=Feynman)($\sigma_p$)：** 这一贡献纯粹是量子力学的，没有经典类比。外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)可以扰动分子的电子波函数，使其与更高能量的[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)混合。这种混合可以感应出电流，在[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)附近，这些电流通常会*增强*外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，导致[去屏蔽](@keyword=deshielding|lang=zh-CN|style=Feynman)（[化学位移](@keyword=chemical_shift|lang=zh-CN|style=Feynman)增加）。这种效应对已占分子[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)和未占（虚拟）[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)之间的[能隙](@keyword=band_gaps|lang=zh-CN|style=Feynman)特别敏感。较小的[能隙](@keyword=band_gaps|lang=zh-CN|style=Feynman)通常会导致较大的顺磁贡献和更[去屏蔽](@keyword=deshielding|lang=zh-CN|style=Feynman)的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman) [@problem_id:2454762]。无处不在的[抗磁屏蔽](@keyword=diamagnetic_shielding|lang=zh-CN|style=Feynman)与结构敏感的顺磁去屏蔽之间的平衡决定了最终的化学位移。

### 计算的艺术：构建虚拟波谱仪

有了这个理论框架，我们就可以在计算机内部构建一个“虚拟波谱仪”。但就像任何精密仪器一样，它必须经过仔细校准。要得到正确的答案，需要密切关注DFT计算的细节。

#### 选择正确的泛函

“泛函”是DFT计算的核心；它是我们用于描述电子间复杂的交换和相关相互作用的近似方法。正如我们所见，[顺磁屏蔽](@keyword=paramagnetic_shielding|lang=zh-CN|style=Feynman)项对[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)之间的[能隙](@keyword=band_gaps|lang=zh-CN|style=Feynman)很敏感。简单泛函（如GGA）的一个普遍弱点是**自相互作用误差**：一个电子会错误地与自身相互作用。这个误差倾向于使电子云过于弥散，并人为地降低虚拟[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)的能量，从而缩小了已占[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)和未占[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)之间的[能隙](@keyword=band_gaps|lang=zh-CN|style=Feynman)。

这就是**杂化泛函**发挥作用的地方。它们通过混入一部分来自计算成本更高的[Hartree-Fock理论](@keyword=hartree_fock_theory|lang=zh-CN|style=Feynman)的“精确”交换能来“修正”自相互作用误差。这种校正倾向于降低已占[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)的能量并提高虚拟[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)的能量，从而扩大[能隙](@keyword=band_gaps|lang=zh-CN|style=Feynman) [@problem_id:1373600]。其结果通常是对[顺磁屏蔽](@keyword=paramagnetic_shielding|lang=zh-CN|style=Feynman)的计算更加准确，因此能更好地预测最终的化学位移 [@problem_id:2454762]。

#### 选择正确的“透镜”：[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)

为了求解量子力学方程，我们使用一组预定义的数学函数来描述分子[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)，这组函数称为**[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)**。可以把它想象成计算机观察分子的“透镜”组。计算磁学性质比单纯计算总能量要求高得多，它需要一套特别高质量的透镜。我们需要一个在各处都足够柔性的[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)：
*   需要**紧凑函数**（具有大指数）来精确描述[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)附近电子密度的形状，这对计算抗磁项至关重要。
*   需要**[弥散函数](@keyword=diffuse_functions|lang=zh-CN|style=Feynman)**（具有小指数）来描述电子云稀疏的外部区域，这对于模拟[离域](@keyword=delocalization|lang=zh-CN|style=Feynman)体系中负责[屏蔽效应](@keyword=shielding_effect|lang=zh-CN|style=Feynman)的长程电子电流至关重要。
*   [基组](@keyword=basis_set|lang=zh-CN|style=Feynman)还必须是**非收缩的**，这为计算提供了足够的灵活性，以准确描述计算顺磁响应所需的[基态](@keyword=ground_state|lang=zh-CN|style=Feynman)和虚拟[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman) [@problem_id:3697535]。

#### [规范原点问题](@keyword=gauge_origin_problem|lang=zh-CN|style=Feynman)：一个视角问题

在这里，我们遇到了一个极其微妙而重要的原理。计算出的物理性质不应依赖于我们为计算选择的任意[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)。这就是**规范不变性**原理。然而，对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的量子力学描述涉及一个称为矢量势$\mathbf{A}$的数学构造，其形式取决于一个称为**规范原点**$\mathbf{R}_0$的任意点的选择。

使用有限、固定的[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)进行简单计算，可能会得到一个随坐标原点移动而改变的屏蔽值！这是一个计算上的赝象——物理上的无稽之谈。解决方案与问题本身一样优雅：我们使用**规范包含[原子轨道](@keyword=atomic_orbitals|lang=zh-CN|style=Feynman)（GIAOs）**。在这种方法中，每个原子[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)都携带自己的局域规范原点，而不是拥有一个全局原点。这种[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)式方法巧妙地将规范不变性直接构建到计算中，确保我们的最终答案与[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)无关，正如任何物理性质都必须具备的那样 [@problem_id:3723539] [@problem_id:3725712]。

### 从单个分子到真实世界

到目前为止，我们的计算都集中在真空中一个单一、静态的分子上。而真实的NMR样品是一个繁华的都市，分子在溶剂中不断运动和相互作用。为了弥合理论与现实之间的差距，我们必须考虑这种复杂性。

#### 构象异构体的舞蹈

许多分子是柔性的，能够扭转和翻转成不同的形状，即**构象异构体**。在室温下的溶液中，一个分子并非以单一形状存在，而是作为所有可及构象异构体的动态系综存在，并迅速相互转换。NMR实验速度较慢，观察到的是所有这些构象异构体化学位移的加权平均值。

高质量的计算工作流程必须模拟这一现实 [@problem_id:2656396]。该过程包括：
1.  进行彻底的搜索以识别所有低能量构象异构体。
2.  计算每个构象异构体 $i$ 的[NMR屏蔽](@keyword=nmr_shielding|lang=zh-CN|style=Feynman)值 $\sigma_i$。
3.  计算每个构象异构体的相对布居数 $p_i$。这一点至关重要：布居数由**吉布斯自由能** ($G_i$) 决定，它不仅包括电子能，还包括零点[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)、热能和熵的贡献。仅使用电子能是一个常见但重大的错误。
4.  最终预测的屏蔽值是系综的**玻尔兹曼加权平均值**：$\langle\sigma\rangle = \sum_i p_i \sigma_i$。这个[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学平均值是与实验测量相对应的恰当理论值 [@problem_id:3725712]。

#### 溶剂的怀抱

烧瓶中的分子并非处于真空中；它们不断受到溶剂分子的碰撞和影响。这既可以改变构象异构体的几何形状，也可以改变它们的相对能量。一种常见的方法是使用**[可极化连续介质模型](@keyword=polarizable_continuum_model|lang=zh-CN|style=Feynman)（PCM）**，该模型将溶剂视为一个均匀的介[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)，围绕着一个包含溶质分子的空腔。

但有时，这种“海洋”模型是不够的。特定的相互作用，比如羟基质子和DMSO溶剂分子之间的[氢键](@keyword=hydrogen_bonding|lang=zh-CN|style=Feynman)，是具有[方向性](@keyword=directivity|lang=zh-CN|style=Feynman)和电子性的。连续介质模型无法捕捉这种特定“握手”的本质。在这些情况下，需要更复杂的**混合簇-连续介质模型**。我们构建一个“超分子”，由我们的溶质和一到两个形成[氢键](@keyword=hydrogen_bonding|lang=zh-CN|style=Feynman)的[显式溶剂](@keyword=explicit_solvent|lang=zh-CN|style=Feynman)分子组成。然后将这整个簇嵌入到可极化连续介质中，以考虑体相溶剂的影响。这种细致、多尺度的方​​法对于准确预测参与强、特定溶剂相互作用的质子的[化学位移](@keyword=chemical_shift|lang=zh-CN|style=Feynman)至关重要 [@problem_id:3691146]。

### [超越标准模型](@keyword=beyond_the_standard_model|lang=zh-CN|style=Feynman)：更重、更快、更奇特

一个物理理论的美妙之处在于其能够扩展到新的前沿领域。对于[NMR计算](@keyword=nmr_calculation|lang=zh-CN|style=Feynman)而言，这意味着要处理含有重元素或未配对电子的分子。

#### 相对论效应

当一个分子含有像溴或碘这样的重原子时，其[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)附近的电子会被加速到非常高的速度，接近光速的一小部分。在这里，我们必须超越标准的非[相对论量子力学](@keyword=relativistic_quantum_mechanics|lang=zh-CN|style=Feynman)，考虑Einstein的相对论。

*   **[标量相对论效应](@keyword=scalar_relativistic_effects|lang=zh-CN|style=Feynman)：** 这些是解释快速运动电子相对论质量增加的校正。它们导致核心[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)的收缩，这会影响[键长](@keyword=bond_length|lang=zh-CN|style=Feynman)，从而影响即使是连接在重中心上的轻原子的[NMR屏蔽](@keyword=nmr_shielding|lang=zh-CN|style=Feynman) [@problem_id:3698608]。

*   **[自旋-轨道耦合](@keyword=spin_orbit_coupling|lang=zh-CN|style=Feynman)：** 这是电子的内禀自旋与其自身绕核轨道运动产生的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)之间的相互作用。这种效应是[磷光](@keyword=phosphorescence|lang=zh-CN|style=Feynman)等现象的原因。对于NMR，它导致了“重原子对轻原子”（HALA）效应，即像[碘](@keyword=iodine|lang=zh-CN|style=Feynman)这样的重原子上的强[自旋-轨道耦合](@keyword=spin_orbit_coupling|lang=zh-CN|style=Feynman)可以引起与其直接键合的碳原子的[化学位移](@keyword=chemical_shift|lang=zh-CN|style=Feynman)发生显著变化 [@problem_id:3698608]。

#### 顺磁性体系

我们讨论的整个框架都假设分子没有未配对电子（一个“闭壳层”体系）。如果我们有一个顺磁性分子，例如带有未配对电子的过渡金属[配合物](@keyword=coordination_compound|lang=zh-CN|style=Feynman)，情况就完全改变了。未配对电子本身就是一个强大的磁源，主导着局域磁环境。

标准的DFT屏蔽计算将会彻底失败。理论必须扩展以包含由未配对电子自旋与核自旋相互作用产生的新机制 [@problem_id:2656414]：
*   **[接触位移](@keyword=contact_shift|lang=zh-CN|style=Feynman)** 源于少量未配对电子自旋密度直接转移到[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)上。
*   **赝[接触位移](@keyword=contact_shift|lang=zh-CN|style=Feynman)** 是一种穿透空间的偶极相互作用，它取决于[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)和电子自旋之间的距离和角度，并且仅在分子的磁化率是各向异性的情况下才会出现。

计算这些效应需要能够处理[超精细相互作用](@keyword=hyperfine_interactions|lang=zh-CN|style=Feynman)和[自旋-轨道耦合](@keyword=spin_orbit_coupling|lang=zh-CN|style=Feynman)的开壳层DFT方法。理论能够适应并解释这些奇特物种的NMR，证明了其强[大性](@keyword=largeness_property|lang=zh-CN|style=Feynman)和普适性。从质子的简单摇摆到金属[配合物](@keyword=coordination_compound|lang=zh-CN|style=Feynman)中电子的相对论舞蹈，DFT为我们提供了一个统一且可预测的窗口，来窥探分子的磁性生命。

