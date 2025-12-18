## 引言
在[计算燃烧学](@entry_id:1122776)及相关领域中，[精确模拟](@entry_id:749142)多组分气体中的物质与能量输运是理解和预测复杂反应流现象的核心。物种扩散，即各组分相对于混合物整体的相对运动，在决定[火焰结构](@entry_id:1125069)、[传播速度](@entry_id:189384)和污染物生成等方面扮演着至关重要的角色。然而，从第一性原理出发的严谨扩散理论，如[Maxwell-Stefan方程](@entry_id:153894)，虽然物理上完备，但其高昂的计算成本使其在包含详细化学反应机理的大规模三维模拟中难以应用。这一物理保真度与[计算效率](@entry_id:270255)之间的矛盾，正是[计算模型](@entry_id:637456)发展所要解决的关键知识缺口。

为了应对这一挑战，混合物平均[扩散模型](@entry_id:142185)应运而生。它提供了一种在计算成本可接受的前提下，对[多组分扩散](@entry_id:1128256)过程进行合理近似的强大工具。本文旨在系统性地阐述混合物平均扩散模型的概念、应用与实践。读者将通过本文学习到：

*   在**原理与机制**章节中，我们将从[质量平均速度](@entry_id:149575)和扩散通量的基本定义出发，揭示模型内在的物理约束，并展示其如何从更严谨的[Maxwell-Stefan方程](@entry_id:153894)近似而来，同时探讨扩散系数的计算方法以及Soret效应等高级修正。
*   在**应用与跨学科联系**章节中，我们将展示该模型在层流和湍流火焰模拟中的核心作用，探讨路易斯数如何影响火焰特性，并分析其在[多相流](@entry_id:146480)和[表面催化](@entry_id:161295)等交叉学科问题中的应用与局限。
*   最后，在**动手实践**部分，我们将通过一系列精心设计的问题，帮助读者巩固对模型关键概念的理解，并将理论知识应用于实际计算中。

现在，让我们首先深入其核心，从“原理与机制”开始，揭开混合物平均扩散模型背后的物理画卷。

## 原理与机制

在多组分[反应流](@entry_id:190741)的[计算模拟](@entry_id:146373)中，准确描述[物质输运](@entry_id:1132066)是至关重要的。在总质量通量中，物种[扩散通量](@entry_id:748422)代表了各组分相对于混合物整体宏观运动的相对输运。本章将深入探讨混合物平均扩散模型（mixture-averaged diffusion model）的原理与机制，从其基本定义出发，关联到更严谨的理论基础，并阐明在燃烧等复杂现象中的实际应用与重要修正。

### 物种扩散的物理学：从分子运动到质量通量

在多组分气体混合物中，每个物种（以 $k$ 为索引）都具有其自身的[平均速度](@entry_id:267649) $\mathbf{u}_k$。然而，从宏观流体力学的角度，我们更关心混合物的整体运动，这通常由**[质量平均速度](@entry_id:149575)**（mass-averaged velocity）或称**[重心](@entry_id:273519)速度**（barycentric velocity）$\mathbf{u}$ 来描述。它被定义为各物种速度以其[质量分数](@entry_id:161575) $Y_k$ 为权重的加权平均：

$$
\mathbf{u} = \sum_{k=1}^{N} Y_k \mathbf{u}_k
$$

其中 $N$ 是混合物中的物种总数。

物种 $k$ 的总质量通量，即单位时间内通过单位面积的物种 $k$ 的质量，由其分密度 $\rho Y_k$ 与其绝对速度 $\mathbf{u}_k$ 的乘积给出，即 $\rho Y_k \mathbf{u}_k$。在质量平均框架下，这个总通量可以分解为两部分：

1.  **对流质量通量（Convective Mass Flux）**：由混合物的整体运动（即[质量平均速度](@entry_id:149575) $\mathbf{u}$）所携带的物种质量通量，其表达式为 $\rho Y_k \mathbf{u}$。
2.  **扩散质量通量（Diffusive Mass Flux）**：由物种相对于混合物整体运动的[相对速度](@entry_id:178060)所引起的质量通量。这个相对速度被称为**扩散速度**（diffusion velocity）$\mathbf{V}_k = \mathbf{u}_k - \mathbf{u}$。因此，扩散质量通量 $\mathbf{J}_k$ 定义为：

$$
\mathbf{J}_k = \rho Y_k \mathbf{V}_k = \rho Y_k (\mathbf{u}_k - \mathbf{u})
$$

这个定义揭示了扩散的本质：它是在[重心](@entry_id:273519)参考系下的质量输运。通过这个定义，物种 $k$ 的总质量通量可以优雅地写成[对流通量](@entry_id:158187)与扩散质量通量之和：$\rho Y_k \mathbf{u}_k = \rho Y_k \mathbf{u} + \mathbf{J}_k$。相应地，物种[质量守恒](@entry_id:204015)方程可以写作：

$$
\frac{\partial}{\partial t}(\rho Y_k) + \nabla \cdot (\rho Y_k \mathbf{u} + \mathbf{J}_k) = \dot{\omega}_k
$$

其中 $\dot{\omega}_k$ 是物种 $k$ 的化学反应源项。这个形式清晰地分离了对流输运（$\nabla \cdot (\rho Y_k \mathbf{u})$）和[扩散输运](@entry_id:150792)（$\nabla \cdot \mathbf{J}_k$）的贡献 。

扩散质量通量的定义直接导出一个至关重要的约束条件。将所有物种的扩散质量通量相加：

$$
\sum_{k=1}^{N} \mathbf{J}_k = \sum_{k=1}^{N} \rho Y_k (\mathbf{u}_k - \mathbf{u}) = \rho \left( \sum_{k=1}^{N} Y_k \mathbf{u}_k \right) - \rho \mathbf{u} \left( \sum_{k=1}^{N} Y_k \right)
$$

根据[质量平均速度](@entry_id:149575)的定义 $\mathbf{u} = \sum_k Y_k \mathbf{u}_k$ 和[质量分数](@entry_id:161575)的定义 $\sum_k Y_k = 1$，上式简化为：

$$
\sum_{k=1}^{N} \mathbf{J}_k = \rho \mathbf{u} - \rho \mathbf{u} (1) = \mathbf{0}
$$

这个 **零扩散质量通量约束（zero net diffusive mass flux constraint）** 是质量平均框架的内在数学结果，它表明所有物种的扩散运动之和不会产生净的[质量输运](@entry_id:151908)。这个约束条件是任何[扩散模型](@entry_id:142185)在质量平均框架下必须满足的物理一致性要求。它也意味着 $N$ 个扩散通量中只有 $N-1$ 个是独立的，第 $N$ 个通量可以由其他 $N-1$ 个通量确定，即 $\mathbf{J}_N = -\sum_{k=1}^{N-1} \mathbf{J}_k$ 。

### 严谨框架：[Maxwell-Stefan方程](@entry_id:153894)

要为[扩散通量](@entry_id:748422) $\mathbf{J}_k$ 构建一个物理模型，我们需要回归到更基本的[分子动力学](@entry_id:147283)理论。在稀薄气体中，描述[多组分扩散](@entry_id:1128256)的严谨理论是 **Maxwell-Stefan 方程**。该理论将[扩散过程](@entry_id:268015)视为一个力平衡过程：作用于某个物种的**[热力学驱动力](@entry_id:1133063)**（通常是[化学势梯度](@entry_id:142294)）与该物种和其他物种之间由于分子碰撞而产生的**分子间摩擦力**相平衡 。

对于一个 $N$ 组分的[理想气体混合物](@entry_id:149212)，在等温、等压条件下，并忽略外力、压力扩散和[热扩散](@entry_id:148740)时，Maxwell-Stefan 方程可以简化为：

$$
\nabla X_k = \sum_{j=1, j \neq k}^{N} \frac{X_k X_j}{D_{kj}} (\mathbf{v}_j - \mathbf{v}_k)
$$

其中 $X_k$ 是物种 $k$ 的[摩尔分数](@entry_id:145460)，$\mathbf{v}_k$ 是物种 $k$ 的[扩散速度](@entry_id:1123720)（在不同参考系下有不同定义），而 $D_{kj}$ 是**二元 Maxwell-Stefan 扩散系数**。这个系数描述了物种 $k$ 和 $j$ 在[二元混合物](@entry_id:168452)中相[互扩散](@entry_id:186107)的能力，它具有对称性，即 $D_{kj} = D_{jk}$。方程的左侧 $\nabla X_k$ 代表了驱动扩散的浓度梯度，右侧则代表了物种 $k$ 与所有其他物种 $j$ 之间的摩擦阻力的总和。

Maxwell-Stefan 方程组提供了一个耦合的、物理上严谨的扩散描述，但直接求解这个线性方程组在大型计算流体力学（CFD）模拟中计算成本高昂，因为它需要求解一个矩阵系统来得到每个物种的扩散通量。这促使了更简洁、[计算效率](@entry_id:270255)更高的近似模型的发展，其中最成功和最广泛使用的就是混合物平均模型。

### 混合物平均近似

**混合物平均近似**的核心思想是，将每个物种 $k$ 的[扩散过程](@entry_id:268015)简化为它在一种假想的、性质为混合物平均的“背景”[气体中的扩散](@entry_id:140992)，从而[解耦](@entry_id:160890)复杂的 Maxwell-Stefan 方程组。

这种近似首先采用一种类似 Fick 定律的形式来描述每个物种的扩散通量，我们称之为初始 Fickian 通量 $\mathbf{J}_k'$：

$$
\mathbf{J}_k' = -\rho D_{k,m} \nabla Y_k
$$

这里，$D_{k,m}$ 是物种 $k$ 的**混合物平均扩散系数**（mixture-averaged diffusion coefficient），它代表了物种 $k$ 在整个混合物中的有效扩散能力。然而，由于每个物种的 $D_{k,m}$ 通常是不同的，直接将这些初始 Fickian 通量相加，其总和一般不为零：

$$
\sum_{k=1}^{N} \mathbf{J}_k' = -\rho \sum_{k=1}^{N} D_{k,m} \nabla Y_k \neq \mathbf{0}
$$

这违反了前面推导出的零净扩散质量通量约束。为了恢复物理一致性，必须对初始通量进行修正。修正方法是为每个物种增加一个共同的**修正通量**（correction flux），其形式为一个对流项 $\rho Y_k \mathbf{V}_c$，其中 $\mathbf{V}_c$ 是一个待定的**修正速度**（correction velocity），对所有物种都相同。修正后的扩散通量 $\mathbf{J}_k$ 为：

$$
\mathbf{J}_k = \mathbf{J}_k' + \rho Y_k \mathbf{V}_c = -\rho D_{k,m} \nabla Y_k + \rho Y_k \mathbf{V}_c
$$

现在，我们强制要求修正后的通量总和为零：

$$
\sum_{k=1}^{N} \mathbf{J}_k = \sum_{k=1}^{N} (-\rho D_{k,m} \nabla Y_k + \rho Y_k \mathbf{V}_c) = \mathbf{0}
$$

分离求和项并提出公因子 $\rho$ 和 $\mathbf{V}_c$：

$$
-\rho \sum_{k=1}^{N} D_{k,m} \nabla Y_k + \rho \mathbf{V}_c \sum_{k=1}^{N} Y_k = \mathbf{0}
$$

利用 $\sum_k Y_k = 1$，我们可以解出修正速度 $\mathbf{V}_c$：

$$
\mathbf{V}_c = \sum_{k=1}^{N} D_{k,m} \nabla Y_k
$$

这个修正速度的物理意义并不是一种新的[扩散机制](@entry_id:158710)，而是一个数学上的修正项，它确保简化的 Fickian 形式与[质量平均速度](@entry_id:149575)的定义相容 。将 $\mathbf{V}_c$ 的表达式代回，我们得到最终的混合物平均扩散通量表达式：

$$
\mathbf{J}_k = -\rho D_{k,m} \nabla Y_k + Y_k \sum_{j=1}^{N} \rho D_{j,m} \nabla Y_j
$$

这个模型在假设某个物种（如空气中的氮气）占主导地位，而其他物种为稀疏组分时最为准确。在典型的碳氢-空气火焰中，氮气作为一种相对惰性的“背景”气体，使得该模型对于主要物种和整体场（如温度、密度）的预测相当可靠。然而，对于质量轻、迁移率高的物种（如 $\mathrm{H}$、$\mathrm{H_2}$），其扩散行为受特定[二元相互作用](@entry_id:195364)的影响更强，混合物平均近似的误差会变得显著 。

### 扩散系数的计算

混合物平均模型的准确性依赖于两个层次的扩散系数：底层的[二元扩散系数](@entry_id:1121572) $D_{kj}$ 和由此构建的混合物平均扩散系数 $D_{k,m}$。

#### [二元扩散系数](@entry_id:1121572) $D_{kj}$

**[二元扩散系数](@entry_id:1121572)** $D_{kj}$ 是描述一对分子 $(k,j)$ 相[互扩散](@entry_id:186107)能力的基础物理量。它可以从气体动理论，特别是通过求解 Boltzmann 方程的 **Chapman-Enskog 理论**，进行[第一性原理计算](@entry_id:198754)。对于模拟分子间作用力为 Lennard-Jones (LJ) 势的稀薄气体，一阶 Chapman-Enskog 理论给出的 $D_{kj}$ 表达式为 ：

$$
D_{kj} = \frac{3}{16p \sigma_{kj}^2 \Omega_{D}^{\ast}(T^{\ast})} \sqrt{\frac{2 k_B^3 T^3}{\pi \mu_{kj}}}
$$

此表达式中的各个参数含义如下：
- $k_B$ 是 Boltzmann 常数。
- $T$ 是[绝对温度](@entry_id:144687)， $p$ 是压力。
- $\mu_{kj} = \frac{m_k m_j}{m_k + m_j}$ 是物种 $k$ 和 $j$ 的**[折合质量](@entry_id:152420)**（reduced mass），$m_k$ 是单个分子的质量。
- $\sigma_{kj}$ 是有效碰撞直径，通常由 Lorentz-Berthelot 混合规则计算：$\sigma_{kj} = (\sigma_k + \sigma_j)/2$。
- $\Omega_{D}^{\ast}(T^{\ast})$ 是无量纲的**扩散[碰撞积分](@entry_id:1122655)**（diffusion collision integral），它是对硬球碰撞模型的修正，考虑了真实分子间的吸[引力](@entry_id:189550)和排斥力。它依赖于无量纲的**折合温度**（reduced temperature）$T^{\ast} = k_BT/\varepsilon_{kj}$，其中 $\varepsilon_{kj}$ 是 LJ 势阱深度，同样通过混合规则计算，如 $\varepsilon_{kj} = \sqrt{\varepsilon_k \varepsilon_j}$。

从这个表达式可以看出，$D_{kj}$ 近似地与 $T^{3/2}$ 成正比，与压力 $p$ 成反比。

#### 混合物平均扩散系数 $D_{k,m}$

有了所有[二元扩散系数](@entry_id:1121572) $D_{kj}$ 后，就可以计算每个物种的**混合物平均扩散系数** $D_{k,m}$。通过对 Maxwell-Stefan 方程进行近似，可以推导出 $D_{k,m}$ 的标准表达式：

$$
D_{k,m} = \frac{1 - Y_k}{\sum_{j \neq k} \frac{X_j}{D_{kj}}}
$$

这个公式直观地表达了物种 $k$ 在混合物中的扩散阻力是其与所有其他物种 $j$ 之间二元扩散阻力（以[摩尔分数](@entry_id:145460) $X_j$ 为权重）的总和。

例如，考虑一个在 $2000\,\mathrm{K}$ 和 $1\,\mathrm{atm}$ 下的甲烷-空气混合物，包含 $\mathrm{CH_4}$、$\mathrm{O_2}$ 和 $\mathrm{N_2}$。如果我们知道该条件下的所有[二元扩散系数](@entry_id:1121572)（$D_{\mathrm{CH_4},\mathrm{O_2}}$, $D_{\mathrm{CH_4},\mathrm{N_2}}$, $D_{\mathrm{O_2},\mathrm{N_2}}$）以及各物种的[质量分数](@entry_id:161575) $Y_k$ 和分子量 $W_k$，我们可以按以下步骤计算每个物种的 $D_{k,m}$ ：
1.  计算混合物的平均分子量 $W_{\mathrm{mix}} = (\sum_k Y_k/W_k)^{-1}$。
2.  计算每个物种的[摩尔分数](@entry_id:145460) $X_k = Y_k \frac{W_{\mathrm{mix}}}{W_k}$。
3.  将 $X_j$ 和 $D_{kj}$ 的值代入上述公式，计算出 $D_{\mathrm{CH_4},m}$、$D_{\mathrm{O_2},m}$ 和 $D_{\mathrm{N_2},m}$。

这个过程展示了混合物平均模型是如何将基于第一性原理的二元[分子相互作用](@entry_id:263767)信息，转化为在多组分环境中进行高效计算的有效参数。

### 燃烧中的高等扩散现象

在燃烧等存在剧烈温度梯度和多种[物种共存](@entry_id:141446)的环境中，除了由浓度梯度驱动的普通扩散外，其他[扩散机制](@entry_id:158710)也变得十分重要。

#### 热扩散（Soret效应）

**[热扩散](@entry_id:148740)**（thermal diffusion），也称为 **Soret 效应**，是一种交叉[输运现象](@entry_id:147655)，即温度梯度可以驱动质量通量。即使在没有浓度梯度的[均匀混合物](@entry_id:146483)中，施加一个温度梯度也会导致物种的部分分离。通常，质量较轻的分子倾向于向高温区域扩散，而质量较重的分子则倾向于向低温区域扩散。

在混合物平均模型中，Soret 效应通过在[扩散通量](@entry_id:748422)表达式中增加一个附加项 $\mathbf{J}_k^{(T)}$ 来引入：

$$
\mathbf{J}_k^{(T)} = -D_{T,k} \frac{\nabla T}{T} = -D_{T,k} \nabla(\ln T)
$$

其中 $D_{T,k}$ 是**[热扩散](@entry_id:148740)系数**（thermal diffusion coefficient）。在实际应用中，通常使用无量纲的**[热扩散](@entry_id:148740)比**（thermal diffusion ratio）$k_{T,k}$，它将[热扩散](@entry_id:148740)与普通扩散联系起来。一种常用的模型形式是  ：

$$
\mathbf{J}_k^{(T)} = -\rho Y_k D_{k,m} k_{T,k} \nabla(\ln T)
$$

包含 Soret 效应后，完整的混合物平均通量模型（未修正前）变为：

$$
\mathbf{J}_k' = -\rho D_{k,m} \nabla Y_k - \rho Y_k D_{k,m} k_{T,k} \nabla(\ln T)
$$

重要的是，Soret 效应贡献的通量总和 $\sum_k \mathbf{J}_k^{(T)}$ 通常不为零。因此，在计算修正速度 $\mathbf{V}_c$ 时必须包含[热扩散](@entry_id:148740)项，以确保总通量守恒：

$$
\mathbf{V}_c = \sum_{k=1}^{N} \left( D_{k,m} \nabla Y_k + Y_k D_{k,m} k_{T,k} \nabla(\ln T) \right)
$$

Soret 效应在氢火焰和富[氢火焰](@entry_id:1126264)中尤为重要。氢气（$\mathrm{H_2}$）和氢原子（$\mathrm{H}$）等轻质组分的[热扩散](@entry_id:148740)系数显著，它们会优先向火焰锋面后的高温区富集。对于 $\mathrm{H_2}$，其 Soret 通量的大小可以与 Fickian 通量相媲美，而对于水蒸气（$\mathrm{H_2O}$）等较重组分，Soret 效应通常可以忽略不计 。

#### 扩散焓流通量与 Lewis 数

物种的扩散不仅输运质量，也同时输运能量。每个扩散的物种都携带着其自身的焓。由物种扩散引起的[能量输运](@entry_id:183081)被称为**扩散焓流通量**（diffusive enthalpy flux），其表达式为：

$$
\mathbf{q}_h = \sum_{k=1}^{N} h_k \mathbf{J}_k
$$

其中 $h_k$ 是物种 $k$ 的单位质量显焓。这个[能量通量](@entry_id:266056)与由温度梯度驱动的**传导热通量**（conductive heat flux）$\mathbf{q}_c = -\lambda \nabla T$（$\lambda$ 为[热导](@entry_id:189019)率）共同构成了总的分子热输运项 $\mathbf{q} = \mathbf{q}_c + \mathbf{q}_h$。[能量守恒方程](@entry_id:748978)中的 $\nabla \cdot \mathbf{q}$ 项必须同时包含这两部分贡献，才能准确描述能量的输运 。需要注意的是，即使总扩散质量通量为零（$\sum_k \mathbf{J}_k = \mathbf{0}$），由于不同物种的焓 $h_k$ 不同，扩散焓流通量 $\mathbf{q}_h$ 通常不为零。

为了量化热量扩散与质量扩散的相对速率，我们引入一个关键的[无量纲参数](@entry_id:169335)——**Lewis 数**（Lewis number），$Le_k$。它被定义为[热扩散率](@entry_id:144337) $\alpha$ 与物种 $k$ 的[质量扩散](@entry_id:149532)率 $D_{k,m}$ 之比：

$$
Le_k = \frac{\alpha}{D_{k,m}} = \frac{\lambda / (\rho c_p)}{D_{k,m}}
$$

其中 $\lambda$ 是混合物的[热导](@entry_id:189019)率，$\rho$ 是密度，$c_p$ 是定压比热容。

Lewis 数的物理意义是热量扩散与[质量扩散](@entry_id:149532)竞争的结果 ：
- **$Le_k = 1$**：热量和物种 $k$ 以相同的速率扩散。这是一个重要的理想化情况，在此假设下，燃烧问题的分析可以大大简化。
- **$Le_k  1$**：物种 $k$ 的扩散比热量扩散快。例如，在贫燃氢气-空气火焰中，氢气 ($Le_{\mathrm{H_2}} \approx 0.3$) 会从火焰面向未燃区快速泄漏，导致火焰锋面处的局部[当量比](@entry_id:1124617)升高，[反应速率](@entry_id:185114)加快。这种“优先扩散”（preferential diffusion）效应可能导致火焰不稳定性和超[绝热火焰温度](@entry_id:146563)。
- **$Le_k  1$**：热量扩散比物种 $k$ 的扩散快。例如，重碳氢燃料（如丙烷）的 Lewis 数大于1。热量会从反应区快速散失到[预热](@entry_id:159073)区，而燃料供应相对较慢，这通常会起到稳定火焰的作用。

因此，Lewis 数是决定预混火焰结构、[传播速度](@entry_id:189384)和稳定性的核心参数。在许多燃烧模拟中，“单位 Lewis 数”（unity Lewis number）假设 ($Le_k = 1$ for all $k$) 是一个常见的简化，但对于涉及轻质燃料（如氢气）或需要精确预测火焰不稳定性的研究，必须考虑真实的、非单位 Lewis 数效应。