## 引言
在[绝对零度](@keyword=absolute_zero|lang=zh-CN|style=Feynman)的[量子流体](@keyword=quantum_fluids|lang=zh-CN|style=Feynman)领域，物质以一种既静止又永恒运动的悖论状态存在。虽然系统处于其最低能量的基态，但[量子力学](@keyword=quantum_mechanics|lang=zh-CN|style=Feynman)规定了粒子之间存在一个复杂的相关网络，从而创造出一种微妙的、[凝固](@keyword=solidification|lang=zh-CN|style=Feynman)的结构。与此同时，这种流体能够以特定的、[量子化](@keyword=quantization|lang=zh-CN|style=Feynman)的方式[振动](@keyword=vibrational_motion|lang=zh-CN|style=Feynman)，这被称为元激发。这就引出了一个基本问题：流体的静态结构是否与其动态行为有关？本文通过探讨费曼关系来填补这一知识空白，该关系是连接这两个看似不同世界的深刻原理。在接下来的章节中，我们将首先深入研究该关系的“原理与机制”，阐述费曼的直观论证及其严格的理论基础。随后，在“应用与跨学科联系”部分，我们将看到这个优雅的公式如何为从[超流体](@keyword=superfluid|lang=zh-CN|style=Feynman)中的[声波](@keyword=sound_waves|lang=zh-CN|style=Feynman)到[液氦](@keyword=liquid_helium|lang=zh-CN|style=Feynman)中神秘的元激发子等不同系统中的实验观察提供有力的解释，展示其作为现代[凝聚态物理学](@keyword=condensed_matter_physics|lang=zh-CN|style=Feynman)基石的作用。

## 原理与机制

想象一种在[绝对零度](@keyword=absolute_zero|lang=zh-CN|style=Feynman)的完美静止的[量子流体](@keyword=quantum_fluids|lang=zh-CN|style=Feynman)。这是一片由相互作用的粒子组成的广阔而宁静的海洋。你可能会将其想象成完全均匀且毫无特征的。但这是一个量子世界，即使在其最低能量状态——基态——也存在着一种持续不断、错综复杂的关联之舞。粒子并非随机[分布](@keyword=generalized_functions|lang=zh-CN|style=Feynman)；由于它们之间的相互作用和它们的量子本性，它们的位置与邻近粒子相关联。我们如何描述这种微妙的、[凝固](@keyword=solidification|lang=zh-CN|style=Feynman)的结构呢？

另一方面，如果我们轻轻“拨动”这片流体，比如说用一个[中子](@keyword=neutrons|lang=zh-CN|style=Feynman)去撞击它，我们就能让它[振动](@keyword=vibrational_motion|lang=zh-CN|style=Feynman)起来。就像吉他弦一样，它不能以任何频率[振动](@keyword=vibrational_motion|lang=zh-CN|style=Feynman)；它有一套特定的允许“音符”，或者说激发模式。这些是系统的元激发，每一个都有一个特征能量$\epsilon$，这个能量取决于它的[波长](@keyword=wavelength|lang=zh-CN|style=Feynman)，或者更精确地说，是它的[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman)$\mathbf{k}$。

现在，问题来了：流体的这两个方面——其静态的、[凝固](@keyword=solidification|lang=zh-CN|style=Feynman)的关联结构和其动态的、[振动](@keyword=vibrational_motion|lang=zh-CN|style=Feynman)的响应——是否相关？这似乎是合理的。流体的结构方式必然决定了它的[振动](@keyword=vibrational_motion|lang=zh-CN|style=Feynman)方式。正是[理查德·费曼](@keyword=richard_feynman|lang=zh-CN|style=Feynman)以其特有的物理直觉，揭示了它们之间深刻而优美的联系。这就是费曼关系，一个看似简单的公式，却在[量子流体](@keyword=quantum_fluids|lang=zh-CN|style=Feynman)的静态和动态世界之间架起了一座强大的桥梁。

### 连接两个世界的桥梁：静态结构与动态激发

让我们首先更好地感受一下我们的两个[主角](@keyword=principal_angles|lang=zh-CN|style=Feynman)。

第一个是**[静态结构因子](@keyword=static_structure_factor|lang=zh-CN|style=Feynman)**，记作$S(\mathbf{k})$。你可以把它想象成流体的“团块性谱”。如果你拍下所有粒子位置的快照并分析它们的[排列](@keyword=permutations|lang=zh-CN|style=Feynman)方式，$S(\mathbf{k})$会告诉你，在对应于[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman)$\mathbf{k}$的特定长度尺度上，你能找到多大的[密度](@keyword=density|lang=zh-CN|style=Feynman)变化。对于给定的$\mathbf{k}$，一个大的$S(\mathbf{k})$意味着流体在该尺度上非常“成团”或高度相关。$S(\mathbf{k}) = 1$的值将对应于完全不相关、随机的气体。对于真实的流体，相互作用使粒子在短距离内相互避开，并以更复杂的方式组织起来，从而导致非平凡的[结构因子](@keyword=structure_factor|lang=zh-CN|style=Feynman)。至关重要的是，$S(\mathbf{k})$是实验学家可以使用[X射线](@keyword=x_rays|lang=zh-CN|style=Feynman)或[中子散射](@keyword=neutron_scattering|lang=zh-CN|style=Feynman)实验直接测量的物理量。

我们的第二个[主角](@keyword=principal_angles|lang=zh-CN|style=Feynman)是**激发谱**$\epsilon(\mathbf{k})$。这是[流体运动](@keyword=fluid_motion|lang=zh-CN|style=Feynman)的“规则手册”。它是一个[色散关系](@keyword=dispersion_relations|lang=zh-CN|style=Feynman)，告诉你创造一个[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman)为$\mathbf{k}$的单一[集体激发](@keyword=collective_excitations|lang=zh-CN|style=Feynman)——一个[振动](@keyword=vibrational_motion|lang=zh-CN|style=Feynman)量子——所需要的能量代价$\epsilon$。这些激发不仅仅是单个粒子的运动；它们是[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)，是整个系统的集体波状运动。

费曼的洞见是用一个优雅的关系将这两个量联系起来：

$$ \epsilon(\mathbf{k}) = \frac{\hbar^2 k^2}{2m S(\mathbf{k})} $$

其中，$m$是流体中单个粒子的质量，$\hbar$是[约化普朗克常数](@keyword=reduced_planck_constant|lang=zh-CN|style=Feynman)。这个公式堪称奇迹。它告诉我们，如果我们知道基态中的静态关联，我们就能立即预测其元激发的能量！或者反过来说，如果我们测量[激发能](@keyword=excitation_energies|lang=zh-CN|style=Feynman)，我们就能推断出其底层结构。

### 费曼的“[单模](@keyword=simple_modules|lang=zh-CN|style=Feynman)”直觉

费曼是如何得出这个结论的？他的论证是物理推理的一个优美典范。想象我们想在基态$|\Psi_0\rangle$中创造一个[动量](@keyword=momentum|lang=zh-CN|style=Feynman)为$\hbar\mathbf{k}$的激发。最简单、最天真的方法可能是只选择一个粒子并给它一个[动量](@keyword=momentum|lang=zh-CN|style=Feynman)。但这不完全正确。一个真正的[集体激发](@keyword=collective_excitations|lang=zh-CN|style=Feynman)涉及*所有*粒子的协调运动。

费曼为这个[激发态](@keyword=excited_states|lang=zh-CN|style=Feynman)提出了一个绝妙的[变分波函数](@keyword=variational_wavefunction|lang=zh-CN|style=Feynman)。他推断，一个携带[动量](@keyword=momentum|lang=zh-CN|style=Feynman)$\hbar\mathbf{k}$的激发本质上是一个[密度波](@keyword=density_wave|lang=zh-CN|style=Feynman)。产生[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman)为$\mathbf{k}$的[密度涨落](@keyword=density_fluctuations|lang=zh-CN|style=Feynman)的算符是$\hat{\rho}_{\mathbf{k}} = \sum_j \exp(i \mathbf{k} \cdot \mathbf{r}_j)$，其中求和遍及所有粒子。因此，对于[激发态](@keyword=excited_states|lang=zh-CN|style=Feynman)[波函数](@keyword=wave_functions|lang=zh-CN|style=Feynman)$|\Psi_{\mathbf{k}}\rangle$的一个很好的猜测，就是用这个[密度算符](@keyword=density_operator|lang=zh-CN|style=Feynman)作用于基态得到的结果：$|\Psi_{\mathbf{k}}\rangle = \hat{\rho}_{\mathbf{k}} |\Psi_0\rangle$。

现在，在[量子力学](@keyword=quantum_mechanics|lang=zh-CN|style=Feynman)中，一个态的能量是[哈密顿量](@keyword=hamiltonian|lang=zh-CN|style=Feynman)的[期望值](@keyword=e_value|lang=zh-CN|style=Feynman)。[静态结构因子](@keyword=static_structure_factor|lang=zh-CN|style=Feynman)$S(\mathbf{k})$，除去一个因子$N$（[粒子数](@keyword=occupation_numbers|lang=zh-CN|style=Feynman)），正好是这个所提出的[波函数](@keyword=wave_functions|lang=zh-CN|style=Feynman)的归一化因子：$N S(\mathbf{k}) = \langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} \hat{\rho}_{\mathbf{k}} | \Psi_0 \rangle$。当你计算这个态的[动能](@keyword=kinetic_energy|lang=zh-CN|style=Feynman)[期望值](@keyword=e_value|lang=zh-CN|style=Feynman)并把所有部分组合在一起时，费曼关系就应运而生了。它源于这样一个假设：给定[动量](@keyword=momentum|lang=zh-CN|style=Feynman)的最低能量激发就是这种简单的、集体的“[单模](@keyword=simple_modules|lang=zh-CN|style=Feynman)”[密度涨落](@keyword=density_fluctuations|lang=zh-CN|style=Feynman)。

### 严格的检验：博戈留波夫的世界

这个直观的论证很有力，但它正确吗？我们可以在一个可以[从头计算](@keyword=ab_initio_calculations|lang=zh-CN|style=Feynman)所有东西的系统中对其进行检验：一个[弱相互作用](@keyword=weak_nuclear_force|lang=zh-CN|style=Feynman)的[玻色-爱因斯坦凝聚](@keyword=bose_einstein_condensation|lang=zh-CN|style=Feynman)（BEC）。对于这样的系统，我们不必猜测激发的具体形式。[博戈留波夫理论](@keyword=bogoliubov_theory|lang=zh-CN|style=Feynman)提供了一种严格的方法来[对角化](@keyword=diagonalization|lang=zh-CN|style=Feynman)[哈密顿量](@keyword=hamiltonian|lang=zh-CN|style=Feynman)并找到真正的低能激发。

利用博戈留波夫的工具，可以独立地推导出激发谱$\epsilon(\mathbf{k})$和[静态结构因子](@keyword=static_structure_factor|lang=zh-CN|style=Feynman)$S(\mathbf{k})$的表达式。结果如下：
$$ \epsilon(\mathbf{k}) = \sqrt{\frac{\hbar^2 k^2}{2m} \left( \frac{\hbar^2 k^2}{2m} + 2gn \right)} $$
$$ S(\mathbf{k}) = \frac{\hbar^2 k^2 / (2m)}{\epsilon(\mathbf{k})} $$
其中$gn$表示气体中[相互作用能](@keyword=interaction_energy|lang=zh-CN|style=Feynman)的强度。现在，让我们来检验费曼的公式。如果我们重新[排列](@keyword=permutations|lang=zh-CN|style=Feynman)第二个方程，我们得到$\epsilon(\mathbf{k}) = \frac{\hbar^2 k^2}{2m S(\mathbf{k})}$。这正是费曼关系！一个完整的微观理论证实了费曼简单的变分论证，这一事实有力地证明了它所包含的深刻真理[@problem_id:1264338]。

### 普适的声音交响乐

该关系在长波极限（即[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman)$k$非常小）下尤其具有启发性。在任何[超流体](@keyword=superfluid|lang=zh-CN|style=Feynman)中，无论是[玻色子](@keyword=bosons|lang=zh-CN|style=Feynman)还是[费米子](@keyword=fermions|lang=zh-CN|style=Feynman)构成的，最低能量的长波激发都是[声波](@keyword=sound_waves|lang=zh-CN|style=Feynman)——[声子](@keyword=phonon|lang=zh-CN|style=Feynman)。就像空气中的声音一样，它们的能量与其[动量](@keyword=momentum|lang=zh-CN|style=Feynman)成[线性](@keyword=linearity|lang=zh-CN|style=Feynman)比例关系：$\epsilon(\mathbf{k}) \approx \hbar c_s k$，其中$c_s$是[声速](@keyword=speed_of_sound|lang=zh-CN|style=Feynman)。

费曼关系告诉我们，在这种极限情况下，[结构因子](@keyword=structure_factor|lang=zh-CN|style=Feynman)$S(\mathbf{k})$会是什么样的呢？代入[声子](@keyword=phonon|lang=zh-CN|style=Feynman)能量，我们得到：
$$ \hbar c_s k \approx \frac{\hbar^2 k^2}{2m S(\mathbf{k})} \implies S(\mathbf{k}) \approx \frac{\hbar k}{2m c_s} $$
这是一个惊人的预测！它说，对于*任何*低温下的[超流体](@keyword=superfluid|lang=zh-CN|style=Feynman)，[静态结构因子](@keyword=static_structure_factor|lang=zh-CN|style=Feynman)必须从零开始[线性](@keyword=linearity|lang=zh-CN|style=Feynman)增加。这条线的斜率与材料中的[声速](@keyword=speed_of_sound|lang=zh-CN|style=Feynman)直接相关。这种普适行为已在从[玻色子](@keyword=bosons|lang=zh-CN|style=Feynman)[液氦](@keyword=liquid_helium|lang=zh-CN|style=Feynman)到[费米子](@keyword=fermions|lang=zh-CN|style=Feynman)BCS[超流体](@keyword=superfluid|lang=zh-CN|style=Feynman)[@problem_id:1270745]和[幺正费米气体](@keyword=unitary_fermi_gas|lang=zh-CN|style=Feynman)[@problem_id:1265861]等截然不同的系统中得到证实。

但还有更多。[声速](@keyword=speed_of_sound|lang=zh-CN|style=Feynman)不仅仅是一个抽象的参数；它是流体的一个宏观[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)属性，与它抵抗压缩的能力（即[可压缩性](@keyword=compressibility|lang=zh-CN|style=Feynman)）有关。通过将费曼关系与“[可压缩性求和规则](@keyword=compressibility_sum_rule|lang=zh-CN|style=Feynman)”等[热力学恒等式](@keyword=thermodynamic_identity|lang=zh-CN|style=Feynman)相结合，人们可以在[微观结构](@keyword=microstructure|lang=zh-CN|style=Feynman)因子$S(\mathbf{k})$与宏观[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)[导数](@keyword=derivative|lang=zh-CN|style=Feynman)$\partial \mu / \partial n$之间建立直接联系，其中$\mu$是[化学势](@keyword=partial_molar_gibbs_energy|lang=zh-CN|style=Feynman)，$n$是[密度](@keyword=density|lang=zh-CN|style=Feynman)[@problem_id:507493]。这便将单个粒子的量子之舞与你可以在实验室测量的宏观属性联系起来，完美地统一了微观和宏观世界。

### 元激发子之谜

费曼关系的辉煌成就不仅限于低[动量](@keyword=momentum|lang=zh-CN|style=Feynman)世界。其最著名的成功案例是解释了[超流氦-4](@keyword=superfluid_helium_4|lang=zh-CN|style=Feynman)激发谱中的一个奇特特征。当实验学家使用[中子散射](@keyword=neutron_scattering|lang=zh-CN|style=Feynman)来测量$\epsilon(k)$时，他们发现了一些奇怪的现象。在最初的[线性](@keyword=linearity|lang=zh-CN|style=Feynman)、类[声子](@keyword=phonon|lang=zh-CN|style=Feynman)上升之后，能量曲线达到一个峰值，然后在一个有限[动量](@keyword=momentum|lang=zh-CN|style=Feynman)$p_0$处下降到一个[局部极小值](@keyword=local_minimum|lang=zh-CN|style=Feynman)，之后再次上升。这个位于极小值处的特殊激发被命名为**元激发子（roton）**。

费曼关系$\epsilon(p) = p^2 / (2m S(p))$对此有何解释？要让$\epsilon(p)$在$p_0$处有一个[局部极小值](@keyword=local_minimum|lang=zh-CN|style=Feynman)，量$p^2/S(p)$也必须在该处处于极小值。这只有在[静态结构因子](@keyword=static_structure_factor|lang=zh-CN|style=Feynman)$S(p)$在相同的[动量](@keyword=momentum|lang=zh-CN|style=Feynman)$p_0$附近有一个明显的*峰值*时才会发生。$S(p)$中的峰值意味着在相应的长度尺度上存在强烈的结构有序性。本质上，费曼关系告诉物理学家：“如果你在动[力学](@keyword=mechanics|lang=zh-CN|style=Feynman)中看到一个元激发子极小值，你必须在静态结构中找到一个峰值。”当[中子散射](@keyword=neutron_scattering|lang=zh-CN|style=Feynman)实验被用来测量$S(p)$时，他们发现的正是如此——一个强烈的峰值恰好出现在元激发子[动量](@keyword=momentum|lang=zh-CN|style=Feynman)处！

这种联系是如此稳固，以至于我们可以将其用作一个定量工具。我们可以将被测量的[中子散射](@keyword=neutron_scattering|lang=zh-CN|style=Feynman)强度与元激发子的性质联系起来[@problem_id:203703]。我们甚至可以预测，当我们通过施加压力来挤压[液氦](@keyword=liquid_helium|lang=zh-CN|style=Feynman)时，元激发子[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)$\Delta$应该如何变化，这是基于[结构因子](@keyword=structure_factor|lang=zh-CN|style=Feynman)的峰值如何随压力变化来预测的[@problem_id:505062]。

### 拓展边界

费曼关系的力量远远超出了[液氦](@keyword=liquid_helium|lang=zh-CN|style=Feynman)这个经典例子。它在各种现代[量子系统](@keyword=quantum_systems|lang=zh-CN|style=Feynman)中都成立。

在一维世界中，[量子效应](@keyword=quantum_effects|lang=zh-CN|style=Feynman)被增强，我们发现了像不可穿越[玻色子](@keyword=bosons|lang=zh-CN|style=Feynman)的[Tonks-Girardeau气体](@keyword=tonks_girardeau_gas|lang=zh-CN|style=Feynman)这样的系统。在这里，物理学可以被精确求解，我们发现[静态结构因子](@keyword=static_structure_factor|lang=zh-CN|style=Feynman)具有一个简单的[线性](@keyword=linearity|lang=zh-CN|style=Feynman)形式，$S(k) \propto k$。将此代入费曼关系，可以得到一个同样简单的激发谱预测[@problem_id:1098999]，这再次与更复杂的计算相符。

即使在系统变得各向异性时，该关系依然有效。考虑一种[超冷原子气体](@keyword=ultracold_atomic_gases|lang=zh-CN|style=Feynman)，这些原子同时也是微小的磁体（偶极原子）。如果你用一个外部场使所有这些磁体对齐，它们之间的力就取决于它们的方向。流体在所有方向上不再是相同的。因此，基态关联$S(\mathbf{k})$和[激发能](@keyword=excitation_energies|lang=zh-CN|style=Feynman)$E(\mathbf{k})$都取决于[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman)$\mathbf{k}$的*方向*，而不仅仅是其大小。然而，费曼关系仍然成立，正确地将各向异性的结构与各向异性的动[力学](@keyword=mechanics|lang=zh-CN|style=Feynman)联系起来[@problem_id:1276305]。

从其直观的起源到严格的证实，再到其在解释元激发子方面的惊人成功，费曼关系是我们理解[量子流体](@keyword=quantum_fluids|lang=zh-CN|style=Feynman)的基石。它证明了物理学中深刻的统一性，向我们展示了一个系统的宁静静态结构和其动态的勃勃生机是同一枚量子硬币的两面。

