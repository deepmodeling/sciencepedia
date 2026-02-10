## 引言
从我们计算机芯片中的硅，到生产燃料的[催化剂](@keyword=catalyst|lang=zh-CN|style=Feynman)，材料的性质都由其内部电子错综复杂的量子之舞所支配。对于[晶体固体](@keyword=crystalline_solids|lang=zh-CN|style=Feynman)而言，这提出了一个看似不可能的挑战：我们如何能为一个拥有近乎无限数量原子的[系统建模](@keyword=systems_modeling|lang=zh-CN|style=Feynman)？答案在于[周期性密度泛函理论](@keyword=periodic_density_functional_theory|lang=zh-CN|style=Feynman) (pDFT)，这是一个强大的计算框架，已经彻底改变了[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)、物理学和化学。通过利用晶体固有的对称性，pDFT 将一个棘手的问题转化为一个可解的问题，使我们能够以前所未有的精度预测和设计材料。本文旨在揭示pDFT的核心概念并展示其广泛的能力。第一章“原理与机制”将解析使pDFT得以运作的理论和计算机制，从布洛赫定理的优雅到[赝势](@keyword=effective_core_potentials|lang=zh-CN|style=Feynman)的巧妙实用。随后，“应用与跨学科联系”一章将探讨pDFT如何在科学和工程领域作为不可或缺的工具，从设计新型[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)到理解复杂的[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)。

## 原理与机制

我们怎么可能[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)理解固体晶体的性质呢？一粒盐中所含的原子数量比全世界所有海滩上的沙粒还要多。为这样一个系统写下薛定谔方程将是徒劳之举。然而，我们每天都在这样做。诀窍不在于为无限数量的原子解决问题，而在于为一个原子解决问题，然后认识到晶体的每一部分都必须以完全相同的方式行事。周期性[密度泛函理论 (DFT)](@keyword=density_functional_theory_dft|lang=zh-CN|style=Feynman) 的深刻之美就在于对这种对称性的利用——这是一个关于我们如何驯服无限的故事。

### 描述无限：[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)与基元

在求解任何方程之前，我们必须首先描述我们的研究对象：晶体本身。一个完美的晶体是重复的奇迹。它是一个结构，如果你在恰当的方向上移动恰当的距离，它看起来完全没有变化。这就是**平移对称性**的性质。

为了在数学上捕捉这一点，我们只需要两条信息 [@problem_id:1768601]。首先，我们需要定义那些使晶体保持不变的基本“平移”。这些平移由一组矢量，即**[布拉菲晶格](@keyword=bravais_lattices|lang=zh-CN|style=Feynman)矢量**（例如 $\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3$）来描述，它们定义了一个称为**[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)**的重复三维盒子。通过在所有方向上无限堆叠这些[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)，我们就可以构建出整个晶体。

其次，我们必须指明其中一个晶胞*内部*有什么。是一个硅原子吗？是一对钠离子和氯离子吗？单个晶胞内的一组原子及其坐标被称为**基元**。

就是这样。[晶格矢量](@keyword=lattice_vectors|lang=zh-CN|style=Feynman)和原子基元共同完全定义了电子量子力学戏剧将要展开的几何舞台。它们定义了由原子核产生的外部势 $V_{\text{ext}}(\mathbf{r})$ 的周期性景观，这是任何DFT计算的基本输入。

### 伟大的简化：[布洛赫定理](@keyword=bloch_s_theorem|lang=zh-CN|style=Feynman)

现在我们来到了使周期性固体计算成为可能的核心“魔术”：**布洛赫定理**。在周期性势中运动的电子的薛定谔方程（或者更准确地说，在DFT中的[Kohn-Sham方程](@keyword=kohn_sham_equations|lang=zh-CN|style=Feynman)）有一种非常特殊的解。该定理源于势是周期性的这一简单事实，它指出，电子[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman) $\psi(\mathbf{r})$ 本身并非完全周期性的。那也太简单了！相反，它们是我们所称的**[布洛赫波](@keyword=bloch_waves|lang=zh-CN|style=Feynman)**。

[布洛赫波](@keyword=bloch_waves|lang=zh-CN|style=Feynman)的形式为 $\psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r})$，其中 $u_{n\mathbf{k}}(\mathbf{r})$ 是一个*真正*具有[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)周期性的函数。这意味着什么？这意味着从一个[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)到下一个晶胞的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)并非完全相同，而是仅仅乘以一个相位因子 $e^{i\mathbf{k}\cdot\mathbf{R}}$，其中 $\mathbf{R}$ 是连接这两个晶胞的[晶格矢量](@keyword=lattice_vectors|lang=zh-CN|style=Feynman)。

矢量 $\mathbf{k}$ 是一种新的标签，一个新的[量子数](@keyword=quantum_numbers|lang=zh-CN|style=Feynman)，称为**晶体动量**。它存在于一个称为**[倒易空间](@keyword=reciprocal_space|lang=zh-CN|style=Feynman)**的空间中，对于给定的晶体，我们只需要考虑一个称为**[第一布里渊区](@keyword=first_brillouin_zone|lang=zh-CN|style=Feynman)**的有限体积内的 $\mathbf{k}$ 矢量。

[布洛赫定理](@keyword=bloch_s_theorem|lang=zh-CN|style=Feynman)的结果是惊人的 [@problem_id:2450984]。它告诉我们，不必一次性求解无限晶体中的所有电子。相反，这个宏大而棘手的问题被分解（或“[块对角化](@keyword=block_diagonalization|lang=zh-CN|style=Feynman)”）为无限多个小得多的独立问题——每个可能的 $\mathbf{k}$ 值对应一个问题。这些小问题中的每一个都可以在*单个晶胞*内解决。我们用在$\mathbf{k}$空间中对布里渊区有限体积进行积分的问题，换下了无限实空间的问题。我们驯服了无限。

### 计算工具箱：[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)与赝势

所以，对于每个 $\mathbf{k}$，我们必须在[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)中求解一个[本征值问题](@keyword=eigenvalue_problems|lang=zh-CN|style=Feynman)。我们如何在计算机上做到这一点？我们需要将[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的周期性部分 $u_{n\mathbf{k}}(\mathbf{r})$ 表示为一系列更简单、已知的函数的和。这些已知函数的集合就是我们的**[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)**。

#### 无偏的选择：[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)

对于一个周期函数，最自然和无偏的函数集是什么？[傅里叶分析](@keyword=fourier_analysis|lang=zh-CN|style=Feynman)给出了明确的答案：[正弦波和余弦波](@keyword=sine_and_cosine_waves|lang=zh-CN|style=Feynman)，或者更方便地，形式为 $e^{i\mathbf{G}\cdot\mathbf{r}}$ 的[复平面](@keyword=complex_plane|lang=zh-CN|style=Feynman)波，其中 $\mathbf{G}$ 是**[倒易晶格](@keyword=reciprocal_lattice|lang=zh-CN|style=Feynman)**的矢量。这个[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)在数学上与实空间[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)相关。

因此，我们可以将[布洛赫函数](@keyword=bloch_functions|lang=zh-CN|style=Feynman)展开为平面波的和：
$$ \psi_{n\mathbf{k}}(\mathbf{r}) = \sum_{\mathbf{G}} c_{n\mathbf{k}}(\mathbf{G})\,e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{r}} $$
原则上，这个和是无限的。在实践中，我们只需要包括动能 $\frac{\hbar^2 |\mathbf{k}+\mathbf{G}|^2}{2m_e}$ 低于某个**[动能截断](@keyword=kinetic_energy_cutoff|lang=zh-CN|style=Feynman)** $E_{\text{cut}}$ 的平面波 [@problem_id:2088778]。这个截断值是一个极好的参数：它是一个我们可以调节的单一旋钮。通过增加 $E_{\text{cut}}$，我们可以系统地提高计算的准确性，使我们的[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)越来越完备。

这种选择具有优美的性质 [@problem_id:2625215]。[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)彼此之间完全正交，它们不与原子位置绑定（这使得力的计算更简单），并且它们与局域势的相互作用可以使用[快速傅里叶变换 (FFT)](@keyword=fast_fourier_transform_(fft)|lang=zh-CN|style=Feynman) [算法](@keyword=algorithm|lang=zh-CN|style=Feynman)以极快的速度计算。然而，它们充满了整个[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)，这意味着所需的[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)数量与[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)的体积成正比，这在模拟大盒子中的孤立分子时是一个缺点。

#### 巧妙的技巧：[赝势](@keyword=effective_core_potentials|lang=zh-CN|style=Feynman)

然而，有一个问题。电子的真实[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在原子核附近剧烈[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，特别是对于紧密束缚的芯电子。描述这些摆动将需要一个天文数字般高的[能量截断](@keyword=energy_cutoff|lang=zh-CN|style=Feynman)，使得平面波方法毫无用处。

解决方案是另一个非常聪明的想法：**[赝势](@keyword=effective_core_potentials|lang=zh-CN|style=Feynman)** [@problem_id:2460278]。芯电子在很大程度上是惰性的，不参与化学键合。而形成[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)的价电子，由于[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)，被禁止占据与芯电子相同的空间。这种排斥作用表现为一种强大的排斥力。赝势方法利用了这一点。我们移除了芯电子，并用一个更弱、更平滑的赝势取代了原子核强大、奇异的[库仑势](@keyword=coulomb_potential|lang=zh-CN|style=Feynman)。这个有效势经过精心构建，以模仿原子核和芯电子的综合效应，包括[泡利排斥](@keyword=pauli_repulsion|lang=zh-CN|style=Feynman)。

其结果是价电子的赝[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在原子核附近平滑且无节点，但在原子之间重要的键合区域与真实[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)完全相同。由于这些赝[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)是平滑的，它们可以用少得多的[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)来描述，使计算在计算上变得可行。这是现代平面波DFT如此成功的核心原因。

### 拼凑谜题：从k空间到物理性质

我们现在已经为一组离散的$\mathbf{k}$点解决了问题。我们如何回到宏观性质，如总能量或电子密度？

#### [布里渊区积分](@keyword=brillouin_zone_integration|lang=zh-CN|style=Feynman)

物理可观测量是通过对整个[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)内所有电子的贡献进行平均得到的。例如，总电子密度 $n(\mathbf{r})$ 是通过对所有占据带 $n$ 的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)平方 $|\psi_{n\mathbf{k}}(\mathbf{r})|^2$ 求和，并对[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)中所有晶体动量 $\mathbf{k}$ 进行积分而得到的 [@problem_id:2901346]。
$$ n(\mathbf{r}) = 2 \sum_n \int_{\text{BZ}} \frac{d\mathbf{k}}{\Omega_{\text{BZ}}} \, f_{n\mathbf{k}} |\psi_{n\mathbf{k}}(\mathbf{r})|^2 $$
这里，$f_{n\mathbf{k}}$ 是该态的占据数（在零温下，占据为1，未占据为0），因子2考虑了自旋，而 $\Omega_{\text{BZ}}$ 是布里渊区的体积。

在计算机中，我们无法执行真正的积分。我们用在离散的**[k点](@keyword=k_points|lang=zh-CN|style=Feynman)**网格上的有限和来近似它，每个[k点](@keyword=k_points|lang=zh-CN|style=Feynman)都有特定的权重 [@problem_id:2901346] [@problem_id:2759532]。这个[k点](@keyword=k_points|lang=zh-CN|style=Feynman)网格的密度是另一个必须收敛的关键参数，就像[能量截断](@keyword=energy_cutoff|lang=zh-CN|style=Feynman)一样。

#### 巨大的分水岭：绝缘体与金属

精确计算所需的[k点](@keyword=k_points|lang=zh-CN|style=Feynman)数量显著地取决于材料的电子性质 [@problem_id:2759532]。

在**绝缘体**中，最高填充带（价带）和最低空带（[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)）之间存在有限的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。所有[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)要么完全填满，要么完全空着。对于像总能量这样的量，被积函数是$\mathbf{k}$的一个平滑、缓变的函数。这样的[平滑函数](@keyword=smoothing_functions|lang=zh-CN|style=Feynman)可以用一个惊人稀疏的[k点](@keyword=k_points|lang=zh-CN|style=Feynman)网格来精确积分。在k空间中的这种行为反映了实空间中的一个深刻性质：在绝缘体中，电子关联是短程的。晶体一侧的电子几乎不知道远处电子的存在。这就是电子物质的“[近视](@keyword=myopia|lang=zh-CN|style=Feynman)性” [@problem_id:2759532]。

在**金属**中，情况截然不同。一个或多个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)仅部分填充，占据态和非占据态之间的能量边界在[k空间](@keyword=k_space|lang=zh-CN|style=Feynman)中形成一个尖锐的表面，称为**[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)**。占据函数在这个表面上从1突变为0。试图对具有陡峭悬崖的函数进行[数值积分](@keyword=numerical_integration|lang=zh-CN|style=Feynman)要困难得多；它需要一个非常密集的[k点](@keyword=k_points|lang=zh-CN|style=Feynman)网格来精确描绘费米面。这种数学上的困难反映了不同的物理现实：金属中的电子关联是长程和[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的。金属中的电子形成了一个高度集体、相互关联的“海洋”。

这个根本区别解释了为什么对于一个非常大的绝缘体超胞，有时仅在布里渊区中心（$\Gamma$点）的一个[k点](@keyword=k_points|lang=zh-CN|style=Feynman)就足够了。实空间中的大超胞对应于倒易空间中的小布里渊区，因此单个点有效地对物理性质进行了很好的采样。对于金属而言，这个技巧会惨败。

### DFT的艺术与灵魂：[交换相关泛函](@keyword=exchange_correlation_functional|lang=zh-CN|style=Feynman)

到目前为止，我们一直专注于问题的“周期性”部分。但“密度泛函理论”部分本身包含着一个深刻的挑战。如果我们知道**交换相关 (XC) 泛函** $E_{\text{xc}}[n]$ 的确切形式，DFT将是一个精确的理论。但我们不知道。这是我们被迫做出的一个核心近似，也是DFT计算中大多数定量误差的来源。

其中一个最著名的缺点是“[带隙问题](@keyword=band_gap_problem|lang=zh-CN|style=Feynman)” [@problem_id:2463438]。像[局域密度近似](@keyword=local_density_approximation|lang=zh-CN|style=Feynman) (LDA) 和[广义梯度近似 (GGA)](@keyword=generalized_gradient_approximation_(gga)|lang=zh-CN|style=Feynman) 这样的标准泛函系统性地、严重地低估了[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)和绝缘体的[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。这是由于一个隐蔽的“自相互作用误差”，即电子错误地与自身相互作用。杂化泛函，如B3LYP，混合了一部分来自[Hartree-Fock理论](@keyword=hartree_fock_theory|lang=zh-CN|style=Feynman)的[精确交换](@keyword=exact_exchange|lang=zh-CN|style=Feynman)来部分纠正这个误差。虽然在分子中很受欢迎，但像B3LYP这样的固定比例[杂化泛函](@keyword=hybrid_functionals|lang=zh-CN|style=Feynman)对于固体来说并非万能药。

对固体的关键洞见是**[介电屏蔽](@keyword=dielectric_shielding|lang=zh-CN|style=Feynman)** [@problem_id:2454292]。在固体中，两个电子之间的长程库仑相互作用被材料中所有其他电子的集体响应所“屏蔽”。这种相互作用在长距离处变弱。为固体设计的现代泛函，如Heyd-Scuseria-Ernzerhof (HSE) 泛函，就是建立在这个物理原理之上的。它们只在短程使用完全的、昂贵的[精确交换](@keyword=exact_exchange|lang=zh-CN|style=Feynman)，然后在长程平滑地切换回一个更近似（但在计算上更便宜，且对屏蔽系统物理上更好）的泛函。这种“屏蔽交换”方法比老一代泛函为固体的[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)和其他性质提供了更均衡、更准确的描述。

### 感受力：结构与力学

DFT不仅限于计算电子能量。其最强大的能力之一是计算原子上的力。**[Hellmann-Feynman定理](@keyword=hellmann_feynman_theorem|lang=zh-CN|style=Feynman)**为此提供了一种优雅的方法：原子核上的力就是势对核位置[导数](@keyword=derivative|lang=zh-CN|style=Feynman)的[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman)。这使我们能够执行**[几何优化](@keyword=geometric_optimization|lang=zh-CN|style=Feynman)**，即根据计算出的力移动原子，直到所有力都为零，从而找到材料的[稳定平衡](@keyword=stable_equilibrium|lang=zh-CN|style=Feynman)结构。

通过计算总能量对整个晶胞应变的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)，我们还可以计算宏观**应力张量** [@problem_id:2894181]。这将量子力学能量直接与体弹性模量等力学性质联系起来。然而，出现了一个微妙之处。如果我们的[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)本身随着我们对[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)施加应变而改变（对于固定截断能的[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)和以原子为中心的轨道都是如此），[Hellmann-Feynman定理](@keyword=hellmann_feynman_theorem|lang=zh-CN|style=Feynman)就不完整了。必须包括一个额外的校正项，称为**[Pulay力](@keyword=pulay_forces|lang=zh-CN|style=Feynman)**或应力，以解释[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)的变化。

### 基石：电中性

最后，我们必须提到一个支撑着整个周期性固体理论的微妙而深刻的约束。由于库仑相互作用是长程的，除非每个[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)内的总[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)都精确为零，否则无限晶体的总静电能将会发散 [@problem_id:2994353]。原子核的正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)必须被电子的负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)完美平衡。这个**[电中性条件](@keyword=electroneutrality_condition|lang=zh-CN|style=Feynman)**是一个基本前提。我们无法模拟由纯电子构成的稳定、无限的晶体；它会分崩离析。这个条件确保了静电问题是适定的，并且每晶胞的能量是一个有限、有意义的量，使得周期性DFT的整个大厦能够建立在坚实的基础上。

从对重复模式的简单描述，到布洛赫定理的天才之举，再到[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)的实用工具和交换相关的深层物理，周期性DFT为理解和预测构成我们世界的材料的性质提供了一个强大而又出人意料地优美的框架。