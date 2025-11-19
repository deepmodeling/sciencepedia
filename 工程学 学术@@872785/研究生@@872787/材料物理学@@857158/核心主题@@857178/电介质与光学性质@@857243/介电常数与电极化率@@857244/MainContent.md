## 引言
[电介质](@entry_id:147163)材料是现代科学与工程技术中无处不在的基础构件，从微电子芯片中的栅极绝缘层到高压输电系统中的[绝缘子](@entry_id:188413)，再到[光通信](@entry_id:200237)中的[光纤](@entry_id:273502)，其身影无处不在。理解这些材料如何响应外加[电场](@entry_id:194326)是设计和优化相关器件的核心。描述这种响应的两个关键物理量——[介电常数](@entry_id:146714)（$\epsilon_r$）和[电极化率](@entry_id:144209)（$\chi_e$）——因此成为材料物理领域的中心议题。然而，要真正掌握这些概念，需要跨越从宏观唯象描述到微观量子起源的多个层次，并理解其在不同学科交叉领域的具体体现，这正是本章旨在解决的知识鸿沟。

本文将系统性地引导读者深入探索[介电常数](@entry_id:146714)与[电极化率](@entry_id:144209)的完整物理图景。在“原理与机制”一章中，我们将首先在宏观电磁学框架下精确定义相关物理量，然后深入探讨[洛伦兹振子模型](@entry_id:274156)、克劳修斯-莫索提关系等经典理论，并进一步延伸至由因果律和晶体对称性所施加的普适约束，最终触及现代[第一性原理计算](@entry_id:198754)的前沿视角。接下来的“应用与跨学科连接”一章将展示这些基本原理如何在器件工程、[复合材料](@entry_id:139856)、[光子](@entry_id:145192)学、固态物理乃至生物物理等多样化情境中发挥作用，揭示理论与实践的紧密联系。最后，通过“动手实践”部分，读者将有机会通过解决具体的计算问题，将理论知识转化为可操作的技能，从而巩固和深化对这一核心主题的理解。

## 原理与机制

在上一章介绍[电介质](@entry_id:147163)的基本概念之后，本章将深入探讨描述[电介质](@entry_id:147163)响应的核心物理原理与微观机制。我们将从宏观[电动力学](@entry_id:158759)框架出发，建立[极化强度](@entry_id:188176)、[电位移场](@entry_id:273493)以及[电极化率](@entry_id:144209)等关键物理量之间的关系。随后，我们将深入微观层面，探究[材料的介电特性](@entry_id:198949)如何源于其原子和分子的结构。最后，我们将讨论描述[介电响应](@entry_id:140146)的更高级理论框架，包括各向异性、因果性约束以及现代[第一性原理计算](@entry_id:198754)方法，从而构建一个从现象到本质、从经典到量子的完整物理图像。

### 宏观[电动力学](@entry_id:158759)中的[电介质](@entry_id:147163)

#### 极化与束缚[电荷](@entry_id:275494)

当[电介质](@entry_id:147163)置于外[电场](@entry_id:194326)中时，其内部的束缚[电荷](@entry_id:275494)会发生有限的位移，正负电荷中心不再重合，形成微观的电偶极子。**极化强度 (Polarization)** 矢量 $\mathbf{P}$ 被定义为材料单位体积内的净电偶极矩，它是一个宏观平均量，量化了材料的整体极化程度。

一个关键的物理后果是，非均匀的极化会在材料内部和表面产生净[电荷](@entry_id:275494)。这些[电荷](@entry_id:275494)被称为**束缚[电荷](@entry_id:275494) (bound charges)**，因为它们不能像导体中的自由电子一样自由移动。我们可以从[电荷守恒](@entry_id:264158)的基本原理出发，推导出束缚电荷密度与极化强度之间的关系 [@problem_id:2814008]。考虑一个非均匀极化的区域，如果[极化矢量](@entry_id:269389)场 $\mathbf{P}$ 从某一点发散（即 $\nabla \cdot \mathbf{P} > 0$），这意味着微观偶极子的正[电荷](@entry_id:275494)端指向外部，而负[电荷](@entry_id:275494)端指向内部，从而在该点附近留下了净的负[电荷](@entry_id:275494)。相反，如果 $\mathbf{P}$ 汇聚于一点（$\nabla \cdot \mathbf{P}  0$），则会积累净的正[电荷](@entry_id:275494)。因此，体束缚[电荷密度](@entry_id:144672) $\rho_b$ 与[极化强度的散度](@entry_id:190771)直接相关：

$$ \rho_b = -\nabla \cdot \mathbf{P} $$

类似地，在[电介质](@entry_id:147163)的表面，如果[极化矢量](@entry_id:269389)具有一个指向表面外部的法向分量，偶极子的正[电荷](@entry_id:275494)端就会暴露在表面上，形成一层正的表面电荷。因此，面束缚电荷密度 $\sigma_b$ 由[极化强度](@entry_id:188176)在表面[法线](@entry_id:167651)方向上的投影决定，其中 $\hat{\mathbf{n}}$ 是指向介质外部的[单位法向量](@entry_id:178851)：

$$ \sigma_b = \mathbf{P} \cdot \hat{\mathbf{n}} $$

理解束缚[电荷](@entry_id:275494)是至关重要的，因为它们和[自由电荷](@entry_id:264392)一样，都是产生[电场](@entry_id:194326)的源。

#### [电位移场](@entry_id:273493)与[本构关系](@entry_id:186508)

在真空中，[电场](@entry_id:194326) $\mathbf{E}$ 的源是总[电荷密度](@entry_id:144672) $\rho_{\text{tot}}$，高斯定律写作 $\nabla \cdot \mathbf{E} = \rho_{\text{tot}} / \epsilon_0$。在[电介质](@entry_id:147163)内部，总[电荷](@entry_id:275494)由[自由电荷](@entry_id:264392) $\rho_{\text{free}}$（例如，掺杂引入的载流子）和束缚[电荷](@entry_id:275494) $\rho_b$ 组成。将 $\rho_b = -\nabla \cdot \mathbf{P}$ 代入，我们得到：

$$ \nabla \cdot \mathbf{E} = \frac{\rho_{\text{free}} + \rho_b}{\epsilon_0} = \frac{\rho_{\text{free}} - \nabla \cdot \mathbf{P}}{\epsilon_0} $$

为了简化方程，使其只依赖于我们通常能够直接控制的自由电荷，物理学家引入了一个辅助场——**[电位移矢量](@entry_id:197092) (electric displacement field)** $\mathbf{D}$ [@problem_id:2981396] [@problem_id:2814054]。$\mathbf{D}$ 的**定义**为：

$$ \mathbf{D} \equiv \epsilon_0 \mathbf{E} + \mathbf{P} $$

这个定义是普遍成立的，不依赖于材料的具体性质。通过这个定义，[高斯定律](@entry_id:141493)在介质中的形式被优美地简化为：

$$ \nabla \cdot \mathbf{D} = \rho_{\text{free}} $$

这表明，[电位移场](@entry_id:273493)的源仅仅是自由电荷。

然而，为了求解一个具体的电磁学问题，我们需要一个封闭的[方程组](@entry_id:193238)。目前我们有三个矢量场（$\mathbf{E}$、$\mathbf{P}$、$\mathbf{D}$），但只有两个独立的方程（$\mathbf{D}$ 的定义和高斯定律）。第三个方程来自于材料自身的属性，它描述了材料在外场作用下会如何响应，这个关系被称为**本构关系 (constitutive relation)**。

对于许多材料，在不太强的[电场](@entry_id:194326)下，其响应是线性的。对于**线性、各向同性、均匀 (linear, isotropic, homogeneous, LIH)** 的[电介质](@entry_id:147163)，极化强度 $\mathbf{P}$ 与诱导它的[电场](@entry_id:194326) $\mathbf{E}$ 成正比：

$$ \mathbf{P} = \epsilon_0 \chi_e \mathbf{E} $$

这里的比例系数 $\chi_e$ 是一个无量纲的标量，称为**[电极化率](@entry_id:144209) (electric susceptibility)**。它表征了材料被极化的难易程度。$\epsilon_0$ 是一个约定俗成的因子，以保证 $\chi_e$ 在[国际单位制](@entry_id:172547)中是无量纲的。

将此[本构关系](@entry_id:186508)代入 $\mathbf{D}$ 的定义，我们得到 $\mathbf{D}$ 和 $\mathbf{E}$ 之间的[线性关系](@entry_id:267880)：

$$ \mathbf{D} = \epsilon_0 \mathbf{E} + \epsilon_0 \chi_e \mathbf{E} = \epsilon_0 (1 + \chi_e) \mathbf{E} $$

我们通常也将 $\mathbf{D}$ 与 $\mathbf{E}$ 的关系写为 $\mathbf{D} = \epsilon \mathbf{E}$，其中 $\epsilon$ 是材料的**绝对[介电常数](@entry_id:146714) (absolute permittivity)**。对比可知，$\epsilon = \epsilon_0 (1 + \chi_e)$。更常用的是**[相对介电常数](@entry_id:267815) (relative permittivity)** $\epsilon_r$（在工程领域也常被称为[介电常数](@entry_id:146714)），定义为 $\epsilon_r = \epsilon / \epsilon_0$。因此，我们得到了连接宏观[介电常数](@entry_id:146714)与[电极化率](@entry_id:144209)的基本关系：

$$ \epsilon_r = 1 + \chi_e $$

需要强调的是，对于[时变电场](@entry_id:197741)，材料的响应并非瞬时的，这导致 $\chi_e$ 和 $\epsilon_r$ 通常是频率 $\omega$ 的复函数，我们将在后续章节详细讨论。

### 极化的微观起源

宏观的[介电常数](@entry_id:146714)和极化率最终是由材料的微观结构决定的。为了建立宏观与微观之间的桥梁，我们需要考虑单个原子或分子是如何响应[电场](@entry_id:194326)的，以及这些微观响应如何汇集成宏观的[极化强度](@entry_id:188176)。

#### [洛伦兹振子模型](@entry_id:274156)

一个经典且富有洞察力的微观模型是**[洛伦兹振子模型](@entry_id:274156) (Lorentz oscillator model)** [@problem_id:2814058]。该模型将介质中的束缚电子（或离子）视为一个受谐振子恢复力束缚的[带电粒子](@entry_id:160311)。在外加[电场](@entry_id:194326) $E(t)$ 的驱动下，这个[带电粒子](@entry_id:160311)（[电荷](@entry_id:275494)为 $q$，质量为 $m$）的[运动方程](@entry_id:170720)可以写成一个受迫阻尼[振动](@entry_id:267781)方程：

$$ m \frac{d^2x}{dt^2} + m\gamma \frac{dx}{dt} + m\omega_0^2 x(t) = qE(t) $$

其中 $x$ 是[电荷](@entry_id:275494)相对于[平衡位置](@entry_id:272392)的位移，$\omega_0$ 是束缚的固有谐振频率，$\gamma$ 是描述[能量耗散](@entry_id:147406)的[阻尼系数](@entry_id:163719)。在频率为 $\omega$ 的时谐[电场](@entry_id:194326) $E(\omega)$ 作用下，[稳态解](@entry_id:200351)给出位移的[复振幅](@entry_id:164138) $x(\omega)$:

$$ x(\omega) = \frac{q E(\omega)}{m(\omega_0^2 - \omega^2 - i\omega\gamma)} $$

单个[振子](@entry_id:271549)产生的电偶极矩为 $p(\omega) = qx(\omega)$。材料的微观**极化率 (polarizability)** $\alpha(\omega)$ 定义为单个偶极矩与作用于其上的*局域*[电场](@entry_id:194326) $E_{\text{loc}}$ 之间的比例系数，$p(\omega) = \alpha(\omega) E_{\text{loc}}(\omega)$。在此模型中（暂时假设 $E_{\text{loc}} = E$），我们得到：

$$ \alpha(\omega) = \frac{q^2}{m(\omega_0^2 - \omega^2 - i\omega\gamma)} $$

这个表达式清晰地展示了极化率的共振特性。当驱动频率 $\omega$ 接近固有频率 $\omega_0$ 时，响应被急剧放大。极化率的虚部与阻尼项 $\gamma$ 相关，描述了材料对[电磁能](@entry_id:264720)量的吸收。

#### 局域电场与克劳修斯-莫索提关系

在稀疏介质（如低压气体）中，原子或分子间距很大，可以近似认为作用在每个分子上的[局域电场](@entry_id:194304)就是宏观的平均[电场](@entry_id:194326) $\mathbf{E}$。此时，[宏观极化](@entry_id:141855)强度 $\mathbf{P}$ 就是单个偶极矩 $\mathbf{p}$ 与数密度 $N$ 的简单乘积：$\mathbf{P} = N\mathbf{p} = N\alpha\mathbf{E}$。由此可得[电极化率](@entry_id:144209) $\chi_e = N\alpha/\epsilon_0$。

然而，在固体和液体等稠密介质中，一个分子感受到的局域电场 $\mathbf{E}_{\text{loc}}$ 显著不同于宏观平均场 $\mathbf{E}$。$\mathbf{E}_{\text{loc}}$ 除了包含外场和样品宏观表面束缚[电荷](@entry_id:275494)贡献的 $\mathbf{E}$ 之外，还必须包含周围其他被极化了的偶极子所产生的[电场](@entry_id:194326)。

为了估算这个局域场，洛伦兹提出了一个巧妙的论证 [@problem_id:3001546]。他假设在所考察的分子周围挖一个虚拟的球形空腔，这个[空腔](@entry_id:197569)足够大，可以包含许多分子，但相对于整个样品又足够小。该分子处的局域电场可以分解为三部分：(1) 宏观场 $\mathbf{E}$；(2) 虚拟球腔表面上的束缚[电荷](@entry_id:275494)所产生的[电场](@entry_id:194326)；(3) 球腔内部其他分立偶极子产生的[电场](@entry_id:194326)。

对于具有立方对称性的晶体或各向同性的随机介质，可以证明第 (3) 部分的贡献因对称性而为零。而第 (2) 部分，即均匀极化的介质中一个球形空腔中心的[电场](@entry_id:194326)，是一个标准的[静电学](@entry_id:140489)结果，其值为 $\mathbf{P}/(3\epsilon_0)$。因此，著名的**洛伦兹[局域电场](@entry_id:194304) (Lorentz local field)** 为：

$$ \mathbf{E}_{\text{loc}} = \mathbf{E} + \frac{\mathbf{P}}{3\epsilon_0} $$

由于 $\mathbf{P}$ 通常与 $\mathbf{E}$ 同向，这意味着在稠密介质中，[局域场](@entry_id:146504)比宏观场更强，从而增强了极化响应。将 $\mathbf{P} = N\mathbf{p} = N\alpha\mathbf{E}_{\text{loc}}$ 和洛伦兹局域场表达式联立，经过代数推导，可以得到联系宏观[相对介电常数](@entry_id:267815) $\epsilon_r$ 和微观极化率 $\alpha$ 的**克劳修斯-莫索提关系 (Clausius-Mossotti relation)**：

$$ \frac{\epsilon_r(\omega) - 1}{\epsilon_r(\omega) + 2} = \frac{N \alpha(\omega)}{3\epsilon_0} $$

这个关系比稀疏介质的近似深刻得多。它表明 $\epsilon_r$ 不仅与 $N\alpha$ 成正比，还通过一个[非线性](@entry_id:637147)的方式依赖于自身。一个有趣（但需谨慎对待）的推论是，当分母 $1-N\alpha/(3\epsilon_0)$ 趋于零时，即使没有外场，材料也可能出现自发极化，这被称为“[极化灾变](@entry_id:137085)”。虽然这个简单的模型不能完全描述铁电性等复杂现象，但它正确地指出了集体相互作用可以驱动[相变](@entry_id:147324)的可能性。例如，在某些铁电体中，存在一种所谓的“[软模式](@entry_id:137007)”，即某个晶格振动模式的固有频率 $\omega_{0,j}$ 随着温度接近居里点而趋于零。根据[洛伦兹模型](@entry_id:144803)，静态[极化率](@entry_id:143513) $\alpha(0) \propto 1/\omega_0^2$ 将会发散，通过克劳修斯-莫索提关系，这会导致静态[介电常数](@entry_id:146714) $\epsilon_r(0)$ 的急剧增大 [@problem_id:2814058]。

### 因果性、耗散与各向异性

#### 因果律与克拉默-克勒尼希关系

物理上，任何系统的响应都不能先于施加给它的驱动，这一基本原则被称为**因果律 (causality)**。对于[电介质](@entry_id:147163)，这意味着极化 $\mathbf{P}(t)$ 只能由过去和当前的[电场](@entry_id:194326) $\mathbf{E}(t' \le t)$ 决定。在频率域中，因果律对响应函数（如[电极化率](@entry_id:144209) $\chi_e(\omega)$）的数学性质施加了非常强的约束。

它要求复函数 $\chi_e(\omega)$ 在复频率平面的上半平面是解析的。这一解析性的一个深刻后果是，$\chi_e(\omega)$ 的实部 $\chi_e'(\omega)$（与[色散](@entry_id:263750)有关）和虚部 $\chi_e''(\omega)$（与能量吸收有关）不是独立的，而是通过一组[积分变换](@entry_id:186209)相互关联。这组关系被称为**克拉默-克勒尼希关系 (Kramers-Kronig relations)** [@problem_id:2814054]。其中一个关系式为：

$$ \chi_e'(\omega) = \frac{2}{\pi} \mathcal{P} \int_0^\infty \frac{\omega' \chi_e''(\omega')}{\omega'^2 - \omega^2} d\omega' $$

其中 $\mathcal{P}$ 表示[柯西主值](@entry_id:192761)积分。这个关系意味着，只要我们知道了材料在所有频率下的吸收谱（$\chi_e''(\omega')$），我们原则上就可以计算出它在任意频率下的[色散](@entry_id:263750)行为（$\chi_e'(\omega)$）。

举一个具体的例子，我们可以计算静态[介电常数](@entry_id:146714)。令 $\omega=0$，上式简化为：

$$ \chi_e'(0) = \frac{2}{\pi} \int_0^\infty \frac{\chi_e''(\omega')}{\omega'} d\omega' $$

这说明，材料的静态（零频）[极化能力](@entry_id:151274)是由其在所有非零频率下的吸收谱积分决定的。即使是在一个与静态测量相距甚远的频率 $\omega_0$ 处的吸收峰，也会对静态[介电常数](@entry_id:146714)做出贡献。例如，对于一个假想的、只有一个位于 $\omega_0$ 的尖锐吸收峰的材料，其吸收谱可模型化为 $\chi_e''(\omega) = C \delta(\omega - \omega_0)$，其中 $C$ 是吸收强度。利用[K-K关系](@entry_id:140966)，我们可以直接计算出其对静态极化率的贡献为 $\chi_e'(0) = 2C/(\pi\omega_0)$，相应的静态[相对介电常数](@entry_id:267815)为 $\epsilon_r(0) = 1 + 2C/(\pi\omega_0)$ [@problem_id:564488]。

#### [各向异性电介质](@entry_id:196150)

对于晶体材料，其内部结构在不同方向上并非完全相同，这导致其电学响应也依赖于方向，即**各向异性 (anisotropy)**。在这种情况下，[极化矢量](@entry_id:269389) $\mathbf{P}$ 和[电场](@entry_id:194326)矢量 $\mathbf{E}$ 通常不再平行。本构关系必须推广为张量形式 [@problem_id:2814054]：

$$ P_i = \epsilon_0 \sum_{j=1}^3 \chi_{ij} E_j $$

这里，$\chi_{ij}$ 是一个 $3 \times 3$ 的电[极化率张量](@entry_id:191938)。同样，[介电常数](@entry_id:146714)也成为一个张量 $\epsilon_{ij} = \epsilon_0(\delta_{ij} + \chi_{ij})$，其中 $\delta_{ij}$ 是克罗内克符号。

物理对称性原理对 $\epsilon_{ij}$ 张量的分量施加了严格的限制 [@problem_id:2814036]。
*   **[能量守恒](@entry_id:140514)与[热力学稳定性](@entry_id:142877)**：对于一个无损耗的介质，储存在介质中的[电场能量密度](@entry_id:261497)为 $U = \frac{1}{2}\mathbf{E} \cdot \mathbf{D} = \frac{1}{2} \sum_{ij} E_i \epsilon_{ij} E_j$。在静态情况下，$\epsilon_{ij}$ 是实数。热力学稳定性要求对于任何非零[电场](@entry_id:194326)，储存的能量必须为正，这意味着静态[介电张量](@entry_id:194185) $\epsilon_{ij}$ 必须是**正定**的。
*   **[微观可逆性](@entry_id:136535) (Onsager 关系)**：在没有破坏时间反演对称性（如外[磁场](@entry_id:153296)）的效应下，线性响应系数张量必须是对称的，即 $\epsilon_{ij} = \epsilon_{ji}$。这被称为倒易关系。
*   **晶体对称性 (Neumann 原理)**：**[诺伊曼原理](@entry_id:136408) (Neumann's principle)** 指出，材料任何物理性质的对称性必须包含其晶体点[群的对称性](@entry_id:136707)。这意味着[介电张量](@entry_id:194185)在晶体的所有对称操作下必须保持不变。例如，对于一个具有特定[点群对称性](@entry_id:141230)的晶体，我们可以通过应用其[对称操作](@entry_id:143398)（如旋转、反映）来确定 $\epsilon_{ij}$ 中哪些分量必须为零，哪些分量之间必须相等。作为一个实例，对于具有 $2/m$ 单斜[点群对称性](@entry_id:141230)的晶体，若将2次[旋转轴](@entry_id:187094)取为 $y$ 轴，则[诺伊曼原理](@entry_id:136408)要求 $\epsilon_{xy}$ 和 $\epsilon_{yz}$ 分量必须为零，而 $\epsilon_{xz}$ 分量则允许非零，最终张量的形式为 $\begin{pmatrix} \epsilon_{xx}  0  \epsilon_{xz} \\ 0  \epsilon_{yy}  0 \\ \epsilon_{xz}  0  \epsilon_{zz} \end{pmatrix}$ [@problem_id:2814024]。

当存在外[磁场](@entry_id:153296) $\mathbf{B}_0$ 时，时间反演对称性被破坏，[介电张量](@entry_id:194185)不再需要是对称的。此时，**Onsager-Casimir 关系**要求 $\epsilon_{ij}(\omega, \mathbf{B}_0) = \epsilon_{ji}(\omega, -\mathbf{B}_0)$。这种非对称的[介电张量](@entry_id:194185)是[法拉第效应](@entry_id:202412)等[非互易光学](@entry_id:270650)现象的根源。

### 高级主题与现代视角

#### [空间色散](@entry_id:141344)

在前面的讨论中，我们隐含地假设了响应是局域的，即某一点的极化 $\mathbf{P}(\mathbf{r})$ 只由同一点的[电场](@entry_id:194326) $\mathbf{E}(\mathbf{r})$ 决定。然而，在更一般的情况下，响应可以是**非局域的**：$\mathbf{P}(\mathbf{r})$ 可能还依赖于其邻近点 $\mathbf{r}'$ 处的[电场](@entry_id:194326)。这种效应被称为**[空间色散](@entry_id:141344) (spatial dispersion)** [@problem_id:2814010]。

在傅里叶空间中，[非局域性](@entry_id:140165)表现为[介电张量](@entry_id:194185)不仅依赖于频率 $\omega$，还依赖于[波矢](@entry_id:178620) $\mathbf{k}$，即 $\epsilon_{ij}(\mathbf{k}, \omega)$。对于一个各向同性的介质，$\epsilon_{ij}(\mathbf{k}, \omega)$ 的形式受到[旋转对称](@entry_id:137077)性的限制。它可以被唯一地分解为两个标量函数，分别描述对纵向（$\mathbf{E} \parallel \mathbf{k}$）和横向（$\mathbf{E} \perp \mathbf{k}$）[电场](@entry_id:194326)的响应：

$$ \varepsilon_{ij}(\mathbf{k},\omega) = \varepsilon_T(k,\omega)\left(\delta_{ij}-\frac{k_i k_j}{k^2}\right) + \varepsilon_L(k,\omega)\frac{k_i k_j}{k^2} $$

其中 $\epsilon_L$ 和 $\epsilon_T$ 分别是**纵向 (longitudinal)** 和**横向 (transverse)** 介电函数，它们只依赖于 $k=|\mathbf{k}|$。$\epsilon_L(k, \omega)$ 描述了对[纵波](@entry_id:172335)（如[等离激元](@entry_id:146184)）的响应，而 $\epsilon_T(k, \omega)$ 描述了对[横波](@entry_id:269527)（如[光子](@entry_id:145192)）的响应。只有在忽略[空间色散](@entry_id:141344)的近似下（即 $k \to 0$），$\epsilon_L$ 和 $\epsilon_T$ 才趋于相等。此外，如果材料还具有空间[反演对称性](@entry_id:269948)，则[介电张量](@entry_id:194185)必须满足 $\epsilon_{ij}(\mathbf{k}, \omega) = \epsilon_{ij}(-\mathbf{k}, \omega)$，这排除了自然[旋光性](@entry_id:139326)等效应。

#### 第一性原理视角：TDDFT与[激子](@entry_id:147299)

经典模型为介电现象提供了深刻的物理图像，但要对真实材料进行定量预测，则需要借助于量子力学的**第一性原理 (first-principles)** 计算。**[含时密度泛函理论](@entry_id:200019) (Time-Dependent Density Functional Theory, TDDFT)** 是计算材料光学和介电性质的最重要工具之一 [@problem_id:2814028]。

在 TDDFT 框架下，相互作用体系的密度响应函数 $\chi$ 可以通过一个类似戴森的方程与无相互作用的科恩-沈（Kohn-Sham）[响应函数](@entry_id:142629) $\chi_0$ 联系起来：

$$ \chi = \chi_0 + \chi_0 (v + f_{xc}) \chi $$

这里，$v$ 是裸[库仑相互作用](@entry_id:747947)，$f_{xc}$ 是**交换关联核 (exchange-correlation kernel)**，它包含了所有复杂的量子[多体效应](@entry_id:173569)。对于晶体，这些量都是在[倒易晶格矢量](@entry_id:263351)[基矢](@entry_id:199546)下的矩阵，矩阵的非对角元自然地包含了之前讨论的微观局域电场效应。宏观介电函数 $\epsilon_M(\omega)$ 可以通过著名的 Adler-Wiser 公式，从这个微观[介电矩阵](@entry_id:144203)的逆的头部（$\mathbf{G}=\mathbf{G}'=\mathbf{0}$）元素得到。

TDDFT 的一个巨大成功在于揭示了描述[半导体](@entry_id:141536)和绝缘体光学吸收谱中**激子 (excitons)**——电子-空穴束缚对——的本质。标准的局域或半局域近似下的 $f_{xc}$ 是短程的，它无法正确描述电子和空穴之间的长程库仑吸引。结果是，这些计算无法预测在材料[带隙](@entry_id:191975)下方出现的激子吸收峰。

现代研究表明，为了正确描述[激子](@entry_id:147299)，交换关联核 $f_{xc}$ 必须具有一个长程部分，其在倒空间中表现为 $\sim -1/|\mathbf{q}|^2$ 的形式。这个吸引性的长程修正（Long-Range Correction, LRC）部分抵消了裸[库仑相互作用](@entry_id:747947) $v$ 的排斥性，使得净的电子-空穴相互作用在长波极限下变为吸引，从而能够形成束缚的[激子](@entry_id:147299)态。这个长程核直接影响宏观[介电函数](@entry_id:136859) $\epsilon_M(\omega)$ 的计算结果，能够准确地再现实验中观测到的[激子](@entry_id:147299)吸收峰的位置和强度，标志着我们对材料[介电响应](@entry_id:140146)的理解达到了一个新的深度。