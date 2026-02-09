## 引言
在原子尺度上，物质的宏观性质——无论是半导体的电学特性、催化剂的活性，还是结构材料的强度——都由其内部原子的精确排布所决定。然而，我们如何才能“看见”这个肉眼无法企及的、高度有序的微观世界呢？X射线衍射（XRD）技术正是我们探索[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)的“火眼金睛”，是连接材料微观构造与宏观性能的核心桥梁。它解决了如何无损、精确地获取晶体内部原子三维坐标这一根本性科学问题。

本文将系统地引导您深入XRD的世界。在第一部分“原理与机制”中，我们将揭示X射线与晶体相互作用的物理本质，从衍射的基本条件到决定衍射强度的结构因子，并探讨晶体学中核心的“相位问题”。随后的“应用与交叉学科联系”部分将展示XRD在[物相鉴定](@keyword=phase_identification|lang=zh-CN|style=Feynman)、纳米结构表征、应变工程乃至生命科学等前沿领域的强大应用，并探讨其与[中子衍射](@keyword=neutron_diffraction|lang=zh-CN|style=Feynman)、[同步辐射](@keyword=synchrotron_radiation|lang=zh-CN|style=Feynman)等技术的协同作用。最后，在“动手实践”部分，您将通过具体的计算练习，将理论知识转化为解决实际问题的能力。这趟旅程将使您不仅理解XRD的“是什么”，更掌握其“为什么”和“怎么用”。

## 原理与机制

### 波与[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)的共舞：衍射的本质

想象一下，向一片平静的湖面投下一颗石子，你会看到一圈圈涟漪向外扩散。现在，想象一下，如果水面上不是空无一物，而是有规律地插着一排排柱子，比如桥墩。当涟漪遇到这些柱子时，每一根柱子都会成为一个新的波源，激起自己的涟漪。这些数不清的次级涟漪会相互叠加、干涉，在某些方向上它们会“步调一致”，形成特别强的水波；而在另一些方向上，它们会“相互抵消”，水面归于平静。这，就是衍射的精髓。

在[X射线衍射](@keyword=x_ray_diffraction_(xrd)|lang=zh-CN|style=Feynman)（XRD）的世界里，X射线就是那圈涟漪，而晶体中周期性排列的原子，就是那一排排的桥墩。然而，故事比这稍微复杂一些。当一束X射线光子撞击晶体时，可能发生两种主要的散射过程 ([@problem_id:4312713])。一种是**[康普顿散射](@keyword=compton_scatter|lang=zh-CN|style=Feynman)**（Compton scattering），光子像台球一样撞击并“踢走”一个电子。在这个过程中，光子会损失一部分能量，改变其波长。这种散射是“非弹性”的，并且由于被踢出的电子的位置具有随机性，散射波之间失去了固定的相位关系，是“非相干”的。它们对我们的[晶体结构分析](@keyword=crystal_structure_analysis|lang=zh-CN|style=Feynman)来说，就像音乐会中的背景噪音，形成了一片弥散的背景信号。

我们真正感兴趣的是另一种过程——**汤姆逊散射**（Thomson scattering），在晶体学中常称为瑞利散射。在这里，光子与原子中的束缚电子相互作用，使其振荡，并以相同的频率（即相同的能量和波长）向外辐射X射线。这是一个“弹性”过程。更关键的是，光子传递的动量由整个晶体，一个宏观物体来吸收。想象一下试图推动一颗尘埃与推动一堵墙的区别：由于晶体的质量极其巨大，它吸收动量后获得的动能几乎为零。因此，光子的能量损失可以忽略不计，保证了散射波的波长与入射波严格一致。这种散射是“相干”的，意味着从不同原子散射出的X射线波之间保持着确定的相位关系。正是这些相干的、能量不变的散射[波的叠加](@keyword=wave_superposition|lang=zh-CN|style=Feynman)与干涉，构成了我们赖以解析[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)的衍射信号。

### 晶体的语言：真实空间与[倒易空间](@keyword=reciprocal_space_2|lang=zh-CN|style=Feynman)

我们如何才能精确地描述这些相干波在何时何地会形成建设性干涉，从而产生一个“衍射峰”呢？答案隐藏在一个美妙的数学概念中：倒易空间。

晶体的核心特征是其周期性——其内部的电子密度 $\rho(\mathbf{r})$ 是一个[周期函数](@keyword=periodic_functions|lang=zh-CN|style=Feynman)。在数学上，任何[周期函数](@keyword=periodic_functions|lang=zh-CN|style=Feynman)都可以被分解为一系列简单的正弦或余弦[波的叠加](@keyword=wave_superposition|lang=zh-CN|style=Feynman)，这就是[傅里叶分析](@keyword=fourier_analysis|lang=zh-CN|style=Feynman)的思想。对于三维的晶体，这些基础波是平面波，形式为 $\exp(i\mathbf{G}\cdot\mathbf{r})$。为了让这些平面波与[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)的周期性“兼容”，它们的波矢量 $\mathbf{G}$ 必须满足一个特殊条件：对于[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)中的任意平移矢量 $\mathbf{R}$，[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)的值必须保持不变，即 $\exp(i\mathbf{G}\cdot(\mathbf{r}+\mathbf{R})) = \exp(i\mathbf{G}\cdot\mathbf{r})$。这简化为 $\exp(i\mathbf{G}\cdot\mathbf{R}) = 1$ ([@problem_id:4312746])。

所有满足这个条件的矢量 $\mathbf{G}$ 的集合，就构成了一个新的、离散的点阵，我们称之为**[倒易晶格](@keyword=reciprocal_lattice|lang=zh-CN|style=Feynman)**（reciprocal lattice）。这是一个令人惊叹的对偶关系：一个在真[实空间](@keyword=real_space|lang=zh-CN|style=Feynman)中的[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)，唯一地对应着一个在“[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman)量空间”（或称为[倒易空间](@keyword=reciprocal_space_2|lang=zh-CN|style=Feynman)）中的[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)。这个[倒易晶格](@keyword=reciprocal_lattice|lang=zh-CN|style=Feynman)可以由一组基矢量 $\mathbf{b}_i$ 生成，它们与真实[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)的[基矢](@keyword=basis_vector|lang=zh-CN|style=Feynman)量 $\mathbf{a}_i$ 通过简洁的关系 $\mathbf{a}_i \cdot \mathbf{b}_j = 2\pi \delta_{ij}$ 唯一确定，其中 $\delta_{ij}$ 是克罗内克符号。

[倒易晶格](@keyword=reciprocal_lattice|lang=zh-CN|style=Feynman)中的每一个点 $\mathbf{G}_{hkl}$ 都不是抽象的数学符号，它携带着关于真实[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)的丰富物理信息 ([@problem_id:4312746])。矢量 $\mathbf{G}_{hkl}$ 的方向垂直于真实[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)中一组特定的[晶面](@keyword=planes_in_crystallography|lang=zh-CN|style=Feynman)（由[密勒指数](@keyword=miller_indices|lang=zh-CN|style=Feynman) $(hkl)$ 标记），而它的大小则与这组晶面的间距 $d_{hkl}$ 成反比：$|\mathbf{G}_{hkl}| = 2\pi/d_{hkl}$。因此，整个[倒易晶格](@keyword=reciprocal_lattice|lang=zh-CN|style=Feynman)就像是真实[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)的一幅“X光片”，它以一种简洁的方式编码了晶体中所有可能的[晶面](@keyword=planes_in_crystallography|lang=zh-CN|style=Feynman)朝向和间距信息。例如，一个面心立方（FCC）[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)的[倒易晶格](@keyword=reciprocal_lattice|lang=zh-CN|style=Feynman)，恰好是一个[体心立方](@keyword=body_centered_cubic|lang=zh-CN|style=Feynman)（BCC）[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)，反之亦然 ([@problem_id:4312746])。

### “咔哒”一声的条件：[厄瓦尔德球](@keyword=ewald_sphere|lang=zh-CN|style=Feynman)

现在我们有了描述实验的工具和描述晶体的工具。衍射的发生，就是这两个世界交汇的瞬间。

在实验中，入射X射线的波矢量为 $\mathbf{k}_i$，散射X射线的[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman)量为 $\mathbf{k}_f$。由于散射是弹性的，它们的长度相等，$|\mathbf{k}_i| = |\mathbf{k}_f| = 2\pi/\lambda$。实验中测量的核心物理量是**[散射矢量](@keyword=scattering_vector|lang=zh-CN|style=Feynman)**（scattering vector）$\mathbf{Q} = \mathbf{k}_f - \mathbf{k}_i$ ([@problem_id:4312761])。$\mathbf{Q}$ 的大小和方向由X射线波长 $\lambda$ 和[散射角](@keyword=scattering_angle|lang=zh-CN|style=Feynman) $2\theta$ 决定，$|\mathbf{Q}| = (4\pi/\lambda)\sin\theta$。它是一个由实验者控制的变量。

另一方面，晶体自身的属性由其[倒易晶格矢量](@keyword=reciprocal_lattice_vectors|lang=zh-CN|style=Feynman) $\mathbf{G}$ 描述，这是一个固定的、离散的集合。

衍射峰出现的条件，即所有原子散射波同相叠加的条件，被证明等价于一个极其简洁的方程，称为**[劳厄条件](@keyword=laue_condition|lang=zh-CN|style=Feynman)**（Laue condition）：实验的[散射矢量](@keyword=scattering_vector|lang=zh-CN|style=Feynman) $\mathbf{Q}$ 必须恰好等于晶体的一个[倒易晶格矢量](@keyword=reciprocal_lattice_vectors|lang=zh-CN|style=Feynman) $\mathbf{G}$ ([@problem_id:4312761])。

$\mathbf{Q} = \mathbf{G}$

这个条件有一个非常直观的几何诠释，即**[厄瓦尔德球](@keyword=ewald_sphere|lang=zh-CN|style=Feynman)**（Ewald sphere）构造 ([@problem_id:4312721])。想象一下，在倒易空间中：
1. 将[倒易晶格](@keyword=reciprocal_lattice|lang=zh-CN|style=Feynman)的原点 $(000)$ 放在这里。
2. 将入射X射线的波矢量 $\mathbf{k}_i$ 的末端放在这个原点上。
3. 以 $\mathbf{k}_i$ 的始端为球心，以其长度 $k = 2\pi/\lambda$ 为半径，画一个球面。这个球面就是[厄瓦尔德球](@keyword=ewald_sphere|lang=zh-CN|style=Feynman)。

这个球面上所有的点都代表了可能的[弹性散射](@keyword=elastic_scattering|lang=zh-CN|style=Feynman)方向。现在，[劳厄条件](@keyword=laue_condition|lang=zh-CN|style=Feynman) $\mathbf{k}_f - \mathbf{k}_i = \mathbf{G}$ 可以改写为 $\mathbf{k}_f = \mathbf{k}_i + \mathbf{G}$。从几何上看，这意味着只有当某个[倒易晶格](@keyword=reciprocal_lattice|lang=zh-CN|style=Feynman)点 $\mathbf{G}$ 恰好落在[厄瓦尔德球](@keyword=ewald_sphere|lang=zh-CN|style=Feynman)面上时，才会有一个对应的 $\mathbf{k}_f$ 同时满足弹性和干涉两个条件，从而产生一个可观测到的衍射峰。这个优雅的构造完美地统一了能量守恒（球的半径）和动量匹配（$\mathbf{Q}=\mathbf{G}$）两个基本要求，生动地解释了为什么我们只能在特定的、离散的角度上“看到”[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)。对于非晶材料，由于不存在离散的倒易点阵，它们只会产生宽泛的散射晕，而不是尖锐的衍射峰 ([@problem_id:4312761])。

### 原子的交响乐：为何有些峰强，有些峰弱？

我们已经知道衍射峰会出现在何处（当 $\mathbf{Q} = \mathbf{G}$ 时），但它们的强度由什么决定呢？为什么有些峰非常明亮，而有些却很微弱，甚至完全消失？

答案在于晶体单胞内部的原子排布。衍射峰的振幅（其平方正比于强度）由**[结构因子](@keyword=the_structure_factor|lang=zh-CN|style=Feynman)**（structure factor）$F(\mathbf{G})$ 决定 ([@problem_id:4312739])。[结构因子](@keyword=the_structure_factor|lang=zh-CN|style=Feynman)可以想象成在一个[单胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)内，所有原子散射波的“合奏”。每个原子的贡献包含两个部分：
1.  **[原子散射因子](@keyword=atomic_scattering_factor|lang=zh-CN|style=Feynman)**（atomic form factor）$f_j(\mathbf{G})$：代表了第 $j$ 个原子自身的散射能力。它本质上是原子电子云密度的傅里叶变换，取决于原子种类和散射角。
2.  **相因子**（phase factor）$\exp(i\mathbf{G}\cdot\mathbf{r}_j)$：取决于原子 $j$ 在[单胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)中的相对位置 $\mathbf{r}_j$。

因此，总的结构因子是所有原子贡献的总和：
$$ F(\mathbf{G}) = \sum_{j} f_j(\mathbf{G}) \exp(i\mathbf{G}\cdot\mathbf{r}_j) $$

这就像一个合唱团。总音量不仅取决于每个歌手的嗓门有多大 ($f_j$)，还取决于他们站在舞台上的位置 ($\mathbf{r}_j$)。如果所有歌手的声波到达听众处时都同相，声音就会很响亮；如果因为位置不同导致声波相位相反，声音就会相互抵消。

这种“抵消”效应在[晶体学](@keyword=crystallography|lang=zh-CN|style=Feynman)中至关重要，它会导致衍射峰的**消光**（absences or extinctions）。有些消光是**系统性消光**（systematic absences），它们是晶体[空间群对称性](@keyword=space_group_symmetry|lang=zh-CN|style=Feynman)的直接体现 ([@problem_id:4312748], [@problem_id:4312699])。例如，在一个体心立方（BCC）[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)中，由于中心原子相对于角落原子的 $(\frac{1}{2}, \frac{1}{2}, \frac{1}{2})$ 平移，对于所有满足 $h+k+l$ 为奇数的 $(hkl)$ 衍射，结构因子中的相因子恰好导致完全抵消，使得 $F(\mathbf{G})$ 恒等于零。类似的，[滑移面](@keyword=slip_planes|lang=zh-CN|style=Feynman)和[螺旋轴](@keyword=screw_axis|lang=zh-CN|style=Feynman)等[对称元素](@keyword=symmetry_elements|lang=zh-CN|style=Feynman)也会导致特定类型的衍射峰系统性地“沉默”，例如 $2_1$ [螺旋轴](@keyword=screw_axis|lang=zh-CN|style=Feynman)会使其轴向上的奇数级反射消失 ([@problem_id:4312699])。这些消光规律是鉴定晶体[空间群](@keyword=space_groups|lang=zh-CN|style=Feynman)的决定性证据，它们不依赖于原子种类或具体的原子坐标。

与此相对的是**偶然消光**（accidental extinctions）。这种情况发生在某个非系统性消[光的衍射](@keyword=light_diffraction|lang=zh-CN|style=Feynman)方向上，由于单胞内不同种类原子的散射因子和位置的特定组合，导致[结构因子](@keyword=the_structure_factor|lang=zh-CN|style=Feynman)恰好为零 ([@problem_id:4312748])。这种消光是“脆弱的”，如果我们换掉其中一种原子，或者利用**[反常色散](@keyword=anomalous_dispersion|lang=zh-CN|style=Feynman)**效应（见下文）改变某个原子的散射因子，这个“偶然”为零的衍射峰就可能重新出现。

### 未解之谜：相位问题

至此，我们似乎已经拥有了揭示原子世界的所有工具。晶体的电子密度 $\rho(\mathbf{r})$ 是[结构因子](@keyword=the_structure_factor|lang=zh-CN|style=Feynman) $F(\mathbf{G})$ 的[逆傅里叶变换](@keyword=inverse_fourier_transform|lang=zh-CN|style=Feynman)。这意味着，如果我们能测量出所有衍射峰的 $F(\mathbf{G})$——包括其振幅和相位——我们就能直接计算出电子密度，从而“看到”原子在晶体中的精确位置。

然而，自然在这里给我们设下了一个巨大的障碍。我们的探测器记录的是X射线的能量流，也就是强度 $I(\mathbf{G})$，它正比于结构因子振幅的平方，$|F(\mathbf{G})|^2$。在这个平方的过程中，所有关于复数 $F(\mathbf{G})$ 的相位信息都丢失了 ([@problem_id:4312709])。这就是晶体学中著名的**相位问题**（phase problem）。这好比我们听了一场交响乐录音，能够精确测量出每种乐器（小提琴、大号、钢琴）在每个音符上的音量大小，却没有记录下它们各自在何时奏响。没有了相位（时间）信息，我们永远无法重构出原始的旋律和和声。

幸运的是，科学家们发展出了一系列巧妙的方法来“找回”丢失的相位：
- **[帕特森函数](@keyword=patterson_function|lang=zh-CN|style=Feynman)**（Patterson function）：直接利用强度数据 $|F(\mathbf{G})|^2$ 进行傅里叶变换，可以得到一张原子间矢量图。虽然它不能直接给出原子位置，但为寻找重原子等提供了关键线索 ([@problem_id:4312709])。
- **[反常色散](@keyword=anomalous_dispersion|lang=zh-CN|style=Feynman)**（anomalous dispersion）：当入射X射线能量接近某个元素的[吸收边](@keyword=absorption_edge|lang=zh-CN|style=Feynman)时，该元素的[原子散射因子](@keyword=atomic_scattering_factor|lang=zh-CN|style=Feynman)会变得复杂且依赖于能量，特别是会产生一个显著的虚部 $f''$ ([@problem_id:4312745])。这个效应源于共振[电子跃迁](@keyword=electronic_transitions|lang=zh-CN|style=Feynman)，与[光电吸收](@keyword=photoelectric_absorption|lang=zh-CN|style=Feynman)密切相关。其真实的色散部分 $f'$ 则由[克拉默斯-克勒尼希关系](@keyword=kramers_kronig_relations|lang=zh-CN|style=Feynman)（Kramers-Kronig relations）决定。这种效应打破了通常的弗里德尔定律（$I(\mathbf{G})=I(-\mathbf{G})$），使得成对的衍射点强度不再相等。这些强度的微小差异包含了宝贵的相位信息，可以通过多波长反常衍射（MAD）或单波长反常衍射（SAD）等技术提取出来 ([@problem_id:4312709])。
- **直接法**（direct methods）与**[迭代法](@keyword=method_of_successive_approximations|lang=zh-CN|style=Feynman)**（iterative methods）：这些方法基于一些基本的物理约束，例如电子密度必须是正值且由离散的原子构成。利用这些约束，可以通过统计学或迭代计算的方式，从已知的振幅数据中高概率地推导出相位 ([@problem_id:4312709])。

### 现实世界的印记：不完美性与峰形

到目前为止，我们讨论的都是一个理想化的世界：无限大、完全周期性、原子静止不动的[完美晶体](@keyword=perfect_crystal|lang=zh-CN|style=Feynman)，它产生的衍射峰应该是无限尖锐的狄拉克 $\delta$ 函数。然而，真实世界的材料，尤其是在[纳米电子学](@keyword=nanoscale_electronics|lang=zh-CN|style=Feynman)中研究的那些，远非如此完美。它们的“不完美”恰恰在衍射峰的形状上留下了独特的印记。

- **热振动**：晶体中的原子并非静止，而是在其[平衡位置](@keyword=equilibrium_position|lang=zh-CN|style=Feynman)附近不停地振动。这种热“模糊”效应并不会使衍射峰变宽，但会减弱其强度。这种衰减由**[德拜-瓦勒因子](@keyword=debye_waller_factor|lang=zh-CN|style=Feynman)**（Debye-Waller factor）描述 ([@problem_id:4312738])。其物理图像是，原子的热运动破坏了完美的相[干性](@keyword=stemness|lang=zh-CN|style=Feynman)，尤其是在大角度（对应探测更精细的结构）时，这种破坏效应更为显著。该因子与原子的[均方根位移](@keyword=root_mean_square_displacement|lang=zh-CN|style=Feynman) $\langle u^2 \rangle$ 相关，通常用[温度因子](@keyword=b_factor|lang=zh-CN|style=Feynman) $B = 8\pi^2 \langle u^2 \rangle$ 来量化。

- **有限尺寸**：[纳米材料](@keyword=nanomaterials|lang=zh-CN|style=Feynman)的晶粒尺寸是有限的，通常在纳米尺度。这种有限的相干衍射区域会导致衍射峰的**尺寸展宽**（size broadening） ([@problem_id:4312736])。这源于傅里叶变换的一个基本性质（[不确定性原理](@keyword=uncertainty_principle|lang=zh-CN|style=Feynman)）：真实空间中的尺寸越小（晶粒尺寸 $L$），倒易空间中的分布就越宽（峰宽 $\Delta q \sim 1/L$）。换算成角度，这种展宽的宽度 $\Delta(2\theta)$ 近似与 $1/\cos\theta$ 成正比。

- **[微应变](@keyword=microstrain|lang=zh-CN|style=Feynman)**：晶体中可能存在各种缺陷、掺杂或不均匀的应[力场](@keyword=force_field|lang=zh-CN|style=Feynman)，导致[晶面间距](@keyword=interplanar_spacing|lang=zh-CN|style=Feynman) $d$ 在不同区域存在微小的波动。这种晶格畸变被称为**[微应变](@keyword=microstrain|lang=zh-CN|style=Feynman)**（microstrain），它同样会导致衍射[峰展宽](@keyword=peak_broadening|lang=zh-CN|style=Feynman) ([@problem_id:4312736])。其原理很简单：根据[布拉格定律](@keyword=bragg_s_law|lang=zh-CN|style=Feynman)， $d$ 的一个分布范围，自然就对应了衍射角 $\theta$ 的一个分布范围。这种展宽的角度依赖性与尺寸展宽不同，其宽度 $\Delta(2\theta)$ 近似与 $\tan\theta$ 成正比。通过分析衍射峰宽随角度的变化，我们就可以区分并量化这两种对[纳米材料](@keyword=nanomaterials|lang=zh-CN|style=Feynman)性能至关重要的微结构特征。

- **[仪器展宽](@keyword=instrumental_broadening|lang=zh-CN|style=Feynman)**：最后，我们使用的衍射仪本身也不是完美的。[X射线源](@keyword=x_ray_source|lang=zh-CN|style=Feynman)并非一个点，光路系统存在发散，探测器也有有限的分辨率。所有这些因素共同贡献了**[仪器展宽](@keyword=instrumental_broadening|lang=zh-CN|style=Feynman)**（instrumental broadening） ([@problem_id:4312751])。多种独立的、微小的[随机误差](@keyword=stochastic_error|lang=zh-CN|style=Feynman)源叠加，根据中心极限定理，倾向于产生一个**高斯**（Gaussian）形的峰。而像[X射线谱](@keyword=x_ray_spectra|lang=zh-CN|style=Feynman)线自身的宽度等效应，则更接近**洛伦兹**（Lorentzian）形。因此，一个真实的仪器峰形通常是两者的卷积，常用一个**沃伊特**（Voigt）函数或伪沃伊特函数来近似。此外，在最常见的布拉格-布伦塔诺几何中，轴向发散还会在衍射峰的低角度侧引入一个特有的不对称拖尾 ([@problem_id:4312751])。

综上所述，一个在屏幕上看到的真实衍射峰，是晶体固有结构信息（理想的 $\delta$ 函数峰位）、单胞内原子交响乐（结构因子决定的强度）、热振动的衰减、纳米尺寸和[微应变](@keyword=microstrain|lang=zh-CN|style=Feynman)的展宽，以及仪器本身印记的复杂卷积。理解和解构这每一个环节，正是[X射线衍射](@keyword=x_ray_diffraction_(xrd)|lang=zh-CN|style=Feynman)这门艺术的魅力所在。