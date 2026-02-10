## 应用与跨学科联系

在理解了[虚时演化](@keyword=imaginary_time_evolution|lang=zh-CN|style=Feynman)作为一种精湛的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)滤波器的原理之后，我们现在踏上一段旅程，去看看这个看似抽象的想法在现实世界中留下了哪些足迹。你可能会感到惊讶。这不仅仅是理论家的玩物；它是一个强大的透镜，通过它我们可以观察和解决横跨惊人广泛科学领域的问题。我们将看到，[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)在[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)中的演化并非那么虚幻。它与我们熟悉的图像模糊过程、深刻的量子隧穿现象、温度的根本定义，以及驱动一些最先进[科学计算](@keyword=scientific_computing|lang=zh-CN|style=Feynman)工具的引擎息息相关。

### 从[量子冷却](@keyword=quantum_cooling|lang=zh-CN|style=Feynman)到图像模糊

让我们从一个相当意想不到的联系开始：模糊一张照片。一个自由量子粒子在[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)中演化的方程，$\partial\psi/\partial\tau = \frac{1}{2}\nabla^2\psi$（在适当单位下），在数学上与[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)或“热”方程完全相同。想象一张初始图像作为一个“[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)”$\psi(x, y, \tau=0)$。像素强度就是这个[函数的振幅](@keyword=oscillation_of_a_function|lang=zh-CN|style=Feynman)。图像中的锐利边缘、精细细节和噪点对应于高频空间分量。用量子力学的语言来说，这些就是高能态。

当我们转动虚时间$\tau$的旋钮时，我们实际上是在求解扩散方程。高频分量比低频分量衰减得快得多。一个锐利的边缘（高频）会迅速变得平滑，而宽泛的形状（低频）则会持续存在。结果如何？图像变得模糊。在图片编辑程序中应用高斯模糊滤镜，本质上就是对一个[自由粒子](@keyword=the_free_particle|lang=zh-CN|style=Feynman)态进行[虚时演化](@keyword=imaginary_time_evolution|lang=zh-CN|style=Feynman)[@problem_id:2441349]。这个有趣的类比给了我们一个强大的直觉：[虚时演化](@keyword=imaginary_time_evolution|lang=zh-CN|style=Feynman)通过平滑掉其高能量的“粗糙边缘”来“冷却”一个量子系统，留下了平静、光滑、低能量的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。

### 探寻分子与材料的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)真相

这种“冷却”或“过滤”特性是[虚时演化](@keyword=imaginary_time_evolution|lang=zh-CN|style=Feynman)最直接和最广泛的应用。对于物理学家和化学家来说，一个系统的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)——其可能达到的最低能量状态——是至关重要的。它决定了[分子结构](@keyword=molecular_structure|lang=zh-CN|style=Feynman)、[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)的性质、材料的磁性等等。

从任何一个合理的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)猜测开始——只要它不与真实[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)完全“正交”——我们就可以在虚时间中对其进行演化。该[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)会稳定而无情地衰减掉所有[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的贡献，在足够长的时间后，留给我们一个高度精确的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)及其能量的近似值[@problem_id:2460933]。这项技术是[计算量子化学](@keyword=computational_quantum_chemistry|lang=zh-CN|style=Feynman)中的一匹“老黄牛”，让我们能够找到，例如，一个分子的稳定构型。

但我们还可以更聪明。问题的对称性可以成为一个强大的盟友。考虑一个在对称双阱势中的粒子，这是一个简单模型，可用于描述像氨这样的分子，其中氮原子可以在氢原子平面的任一侧。真实的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)$\psi_0$是粒子处于两个阱中的偶宇称叠加态。第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)$\psi_1$则是一个[奇宇称](@keyword=odd_parity|lang=zh-CN|style=Feynman)叠加态。通过用一个明确的偶宇称初始态开始[虚时演化](@keyword=imaginary_time_evolution|lang=zh-CN|style=Feynman)，我们保证会收敛到能量最低的偶数态：即[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。如果我们从一个[奇宇称](@keyword=odd_parity|lang=zh-CN|style=Feynman)初始态开始，它将保持奇宇称，因此它必须收敛到能量最低的奇数态：即第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)！通过计算这两种能量$E_0$和$E_1$，我们可以找到能量差$\Delta E = E_1 - E_0$。这个被称为“隧穿分裂”的微小[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，支配着粒子从一个阱隧穿到另一个阱的速率[@problem_id:2441278]。

这种方法的力量不仅限于单粒子。它是理解[多体量子系统](@keyword=many_body_quantum_systems|lang=zh-CN|style=Feynman)奇异世界的关键工具。例如，一个玻色-爱因斯坦凝聚（Bose-Einstein Condensate, BEC）——一种成千上万个原子表现得像单一量子实体的[物质状态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)——的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)由非线性的[Gross-Pitaevskii方程](@keyword=gross_pitaevskii_equation|lang=zh-CN|style=Feynman)描述。通过在[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)中演化一个[试探波函数](@keyword=trial_wavefunction|lang=zh-CN|style=Feynman)，研究人员可以数值求解这个方程，以预测这些奇异[量子流体](@keyword=quantum_fluids|lang=zh-CN|style=Feynman)的形状和性质[@problem_id:2383399]。

### [量子隧穿](@keyword=quantum_mechanical_tunneling|lang=zh-CN|style=Feynman)的秘密路径

到目前为止，我们都将虚时间中的“路径”视为一种计算上的构造。但在[理论物理学](@keyword=theoretical_physics|lang=zh-CN|style=Feynman)最美丽的转折之一中，这条路径本身具有了深刻的物理意义。在20世纪70年代，包括Sidney Coleman在内的物理学家意识到，一个粒子量子力学地隧穿过势垒的最可能路径，是一条在虚时间中的轨迹。

如果我们写下一个能使[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)（或欧几里得）作用量最小化的路径的[运动方程](@keyword=equations_of_motion|lang=zh-CN|style=Feynman)，我们会发现一些非凡之处：它就是牛顿第二定律，$M\ddot{\mathbf{q}} = \nabla V(\mathbf{q})$，但却是针对一个在被*上下颠倒*的势中运动的粒子[@problem_id:2898593]。一个[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)变成了一座山丘，一个势垒变成了一个山谷。

这个隧穿事件可以被描绘成一个粒子从这些倒置山丘之一的顶部静止开始（对应于真实势中的一个极小值），滚入倒置的山谷（真实势垒），然后爬上另一边，在相邻山丘的顶峰处停下来（另一个极小值）。这条连接两个[经典转折点](@keyword=classical_turning_points|lang=zh-CN|style=Feynman)的特殊[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)轨迹被称为**瞬子**。它的作用量给出了隧穿概率的主导阶估计。这个半经典图像既提供了一个惊人直观的可视化，也为[计算化学](@keyword=computational_chemistry|lang=zh-CN|style=Feynman)[反应速率](@keyword=reaction_rates|lang=zh-CN|style=Feynman)和粒子衰变速率提供了一个强大的定量工具，将一个纯粹的量子谜团变成了一个在奇特、颠倒景观上的经典力学问题。

### 虚时间即真实温度

也许所有联系中最深刻、最重要的是[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)与温度之间的联系。我们一直在使用的算符$e^{-\tau \hat{H}}$，可能看起来只是一个方便的投影算符。但在[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的世界里，算符$e^{-\beta \hat{H}}$（其中$\beta = 1/(k_B T)$是[逆温](@keyword=temperature_inversion|lang=zh-CN|style=Feynman)度）才是主角。它是（未归一化的）统计[密度算符](@keyword=density_operator|lang=zh-CN|style=Feynman)，它的迹$Z = \mathrm{Tr}(e^{-\beta \hat{H}})$是配分函数，所有处于热平衡的系统的[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)性质都可以从中导出。

在虚时间中演化一段时长为$\tau=\beta\hbar$的路径积分，正是计算这个[配分函数](@keyword=sum_over_states_2|lang=zh-CN|style=Feynman)的方法。在这种背景下，虚时间不是一个抽象的坐标；它的长度*就是*[逆温](@keyword=temperature_inversion|lang=zh-CN|style=Feynman)度。零温下的模拟对应于在无限长的虚时间维度中的演化。而有限温度下的模拟则对应于在被*紧致化*成一个周长为$\beta\hbar$的圆环的[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)中演化。

这一认识是[热场论](@keyword=finite_temperature_field_theory|lang=zh-CN|style=Feynman)和许多最强大的量子模拟方法的基础。例如，[量子蒙特卡洛](@keyword=quantum_monte_carlo|lang=zh-CN|style=Feynman)（Quantum Monte Carlo, QMC）[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，如用于研究固体中相互作用电子的著名[Hubbard模型](@keyword=hubbard_model|lang=zh-CN|style=Feynman)的[行列式](@keyword=determinant|lang=zh-CN|style=Feynman)QMC方法，在一个[时空](@keyword=space_time|lang=zh-CN|style=Feynman)[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)上模拟系统，其中一个维度就是这个紧致化的[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)[@problem_id:2842847]。通过在这个[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)上抽样构型，这些方法可以计算如[电导率](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)和磁性随温度变化的性质，为[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)提供了不可或缺的见解。这个框架也揭示了深刻的计算挑战，如臭名昭著的“[费米子符号问题](@keyword=fermionic_sign_problem|lang=zh-CN|style=Feynman)”，当粒子的量子性质导致路径积分中出现[相消干涉](@keyword=destructive_interference|lang=zh-CN|style=Feynman)，从而阻碍高效模拟时，这个问题就会出现。

这种联系使我们能够理解粒子在极端热环境中的行为，例如[早期宇宙](@keyword=early_universe|lang=zh-CN|style=Feynman)的原始汤或中子星的内部。一个穿过这个由其他粒子组成的“热汤”的粒子会与[热浴](@keyword=heat_bath|lang=zh-CN|style=Feynman)相互作用，结果，它的[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)可能会改变。[虚时间形式](@keyword=imaginary_time_formalism|lang=zh-CN|style=Feynman)是计算这些粒子性质热修正的标准工具[@problem_id:742474]，这是有限温度宇宙物理学的一个直接且可测量的后果。

### 面向量子系统的现代工具箱

对完整[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)进行暴力演化只对小系统可行。当我们着手解决[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)的重大挑战时，[量子态空间](@keyword=quantum_state_space|lang=zh-CN|style=Feynman)的巨大规模（“维度灾难”）变得势不可挡。在这里，[虚时演化](@keyword=imaginary_time_evolution|lang=zh-CN|style=Feynman)的原理也被改编成了更复杂、更现代的工具。

其中一种方法是**变分[虚时演化](@keyword=imaginary_time_evolution|lang=zh-CN|style=Feynman)（Variational Imaginary Time Evolution, VITE）**[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)。我们不是让[状态向量](@keyword=state_vector|lang=zh-CN|style=Feynman)在无限维的[希尔伯特空间](@keyword=hilbert_spaces|lang=zh-CN|style=Feynman)中自由漫游，而是将其限制在一个由少数参数$\vec{\theta}$描述的、精心选择的低维状态景观中。然后，我们使用McLachlan变分原理来找到这个景观上的“最陡下降”方向——这个方向最能近似真实的虚时动力学。这种投影演化引导参数$\vec{\theta}$朝向描述[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的那组值，为在经典计算机和近期[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机上寻找复杂分子和材料的解提供了一条实际可行的路径[@problem_id:2917648][@problem_id:164994]。

同样这种由虚时间驱动的逐步更新思想，也是一些最先进的经典模拟方法的核心，例如使用**[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)**的方法。对于二维高度纠缠的[多体系统](@keyword=many_body_systems|lang=zh-CN|style=Feynman)，[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)可以表示为一个由相互连接的小[张量](@keyword=tensor|lang=zh-CN|style=Feynman)组成的网络（一个PEPS）。直接找到最优的[张量](@keyword=tensor|lang=zh-CN|style=Feynman)是一个极其困难的问题。但是通过对网络的一小部分局部应用一个[虚时演化](@keyword=imaginary_time_evolution|lang=zh-CN|style=Feynman)门，然后截断结果，人们可以迭代地“冷却”整个[张量网络](@keyword=tensor_networks|lang=zh-CN|style=Feynman)状态，使其趋向于真实的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)[@problem_id:2445438]。

从一个简单的数学戏法 $t \to -i\tau$ 出发，我们发现了一条贯穿[计算机图形学](@keyword=computer_graphics|lang=zh-CN|style=Feynman)、[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)、[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学和[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)前沿的统一主线。最初只是为了找到一根量子“弦”的最低音符的技巧，如今已成为描绘隧穿景象、在量子领域定义温度、以及构建模拟我们所知最复杂量子系统的引擎的方式。这证明了物理世界深刻且常常令人惊讶的统一性。