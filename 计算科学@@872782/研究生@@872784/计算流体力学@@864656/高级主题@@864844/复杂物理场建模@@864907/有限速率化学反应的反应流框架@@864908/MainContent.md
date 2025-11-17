## 引言
含[有限速率化学](@entry_id:749365)反应的流动是燃烧、推进系统和化学加工等众多关键工程与科学领域的核心现象。精确预测这些系统的行为，需要我们不仅理解[流体动力学](@entry_id:136788)，还要掌握其与复杂[化学反应](@entry_id:146973)之间错综复杂的相互作用。然而，模拟这种紧密耦合的现象带来了巨大的挑战，主要挑战在于现在需要同时处理多个尺度上截然不同的物理和化学过程，尤其是在计算层面。

本文旨在为读者构建一个关于[有限速率化学](@entry_id:749365)[反应流](@entry_id:190684)模拟的完整知识框架。我们将分三步深入探讨这一主题。在“原理与机制”一章中，我们将从第一性原理出发，系统性地建立描述[反应流](@entry_id:190684)的控制方程，并阐述所需的[热力学](@entry_id:141121)、输运和化学动力学模型。接着，在“应用与跨学科连接”一章中，我们将展示这些理论如何应用于分析典型火焰结构、污染物生成，并延伸至[湍流燃烧](@entry_id:756233)和机理简化等前沿建模技术。最后，“动手实践”部分将提供具体的编程练习，以巩固理论知识并提升解决实际问题的能力。

让我们首先从构建描述这些复杂现象的基础——控制方程和基本物理机制——开始。

## 原理与机制

本章旨在深入阐述描述含[有限速率化学](@entry_id:749365)[反应流](@entry_id:190684)动的基本原理和核心机制。这些流动现象普遍存在于从[内燃机](@entry_id:200042)、[燃气轮机](@entry_id:138181)到天体物理学和[材料合成](@entry_id:152212)的众多科学与工程领域。对这些现象进行精确的[计算流体动力学](@entry_id:147500)（CFD）建模，需要全面理解[流体动力学](@entry_id:136788)、[热力学](@entry_id:141121)、输运现象和[化学动力学](@entry_id:144961)之间的复杂耦合。本章将系统性地构建这一理论框架，从宏观的控制方程出发，深入到微观的物理和化学模型，最终探讨求解这些方程所面临的数值挑战。

### [反应流](@entry_id:190684)的控制方程

任何[反应流](@entry_id:190684)仿真的基础都是一套描述质量、动量、能量和化学[组分守恒](@entry_id:197272)的[偏微分方程](@entry_id:141332)。对于可压缩的多组分[理想气体混合物](@entry_id:149212)，这些方程（即[可压缩Navier-Stokes](@entry_id:747591)方程的拓展形式）在全[守恒形式](@entry_id:747710)下可以表示如下。这套方程构成了我们分析的基石 [@problem_id:3356462]。

- **总[质量守恒](@entry_id:204015)（连续性方程）**:
此方程描述了流体微元中质量随时间的变化率等于流入该微元的净质量通量。
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \boldsymbol{u}) = 0
$$
其中 $\rho$ 是混合物的总密度，$t$ 是时间，$\boldsymbol{u}$ 是[质量平均速度](@entry_id:149575)矢量。

- **组分[质量守恒](@entry_id:204015)**:
对于混合物中的每一种组分 $k$（共 $N_s$ 种），其质量也必须守恒。其局部质量变化归因于随主流的[对流](@entry_id:141806)、相对于主流的[扩散](@entry_id:141445)以及[化学反应](@entry_id:146973)的生成或消耗。
$$
\frac{\partial (\rho Y_k)}{\partial t} + \nabla \cdot \left(\rho Y_k \boldsymbol{u} + \boldsymbol{J}_k\right) = \dot{\omega}_k, \quad k=1,\dots,N_s
$$
此处，$Y_k$ 是组分 $k$ 的**质量分数**，满足 $\sum_{k=1}^{N_s} Y_k = 1$。$\boldsymbol{J}_k$ 是组分 $k$ 的**[扩散](@entry_id:141445)质量通量**，表示组分 $k$ 相对于[质量平均速度](@entry_id:149575) $\boldsymbol{u}$ 的运动。$\dot{\omega}_k$ 是组分 $k$ 的**[质量生成](@entry_id:161427)率**（单位体积单位时间的质量变化），它源于[化学反应](@entry_id:146973)。由于[化学反应](@entry_id:146973)本身不产生或消灭总质量，这些源项必须满足约束 $\sum_{k=1}^{N_s} \dot{\omega}_k = 0$。

- **动量守恒**:
此方程是牛顿第二定律在流体微元上的体现。动量的变化由作用在微元上的[表面力](@entry_id:188034)（压力和粘性力）和[体力](@entry_id:174230)（如重力）引起。
$$
\frac{\partial (\rho \boldsymbol{u})}{\partial t} + \nabla \cdot \left(\rho \boldsymbol{u}\boldsymbol{u} + p \boldsymbol{I} - \boldsymbol{\tau}\right) = \rho \boldsymbol{f}
$$
这里，$\rho \boldsymbol{u}\boldsymbol{u}$ 是动量的[对流通量](@entry_id:158187)，$p$ 是[热力学](@entry_id:141121)压力，$\boldsymbol{I}$ 是单位张量。$\boldsymbol{f}$ 是单位质量的体力加速度。$\boldsymbol{\tau}$ 是**[粘性应力](@entry_id:261328)张量**。对于[牛顿流体](@entry_id:263796)，并采用**[斯托克斯假设](@entry_id:195909)**（Stokes' hypothesis），该[张量表示](@entry_id:180492)为：
$$
\boldsymbol{\tau} = \mu \left[\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^{\mathsf{T}}\right] - \frac{2}{3}\mu(\nabla \cdot \boldsymbol{u})\boldsymbol{I}
$$
其中 $\mu$ 是流体的[动力粘度](@entry_id:268228)。注意[动量方程](@entry_id:197225)中 $\boldsymbol{\tau}$ 前的负号，表示[粘性应力](@entry_id:261328)是作用在流体微元表面上的[内力](@entry_id:167605)。

- **总[能量守恒](@entry_id:140514)**:
此方程是热力学第一定律的表述。流体微元总能量的变化等于[体力](@entry_id:174230)与[表面力](@entry_id:188034)对其做的功以及传入该微元净热量之和。
$$
\frac{\partial (\rho E)}{\partial t} + \nabla \cdot \left[ \boldsymbol{u}(\rho E + p) - \boldsymbol{\tau}\cdot\boldsymbol{u} + \boldsymbol{q} + \sum_{k=1}^{N_s} h_k \boldsymbol{J}_k \right] = \rho \boldsymbol{u}\cdot \boldsymbol{f}
$$
$E = e + \frac{1}{2}|\boldsymbol{u}|^2$ 是单位质量的总能量，由内能 $e$ 和动能组成。方程左侧散度项中的各项分别代表：
1.  $\boldsymbol{u}(\rho E + p)$: 通过[对流输运](@entry_id:149512)的总能量和压力所做的流功。$\rho E + p$ 也可写作 $\rho H$，其中 $H$ 是[总焓](@entry_id:197863)。
2.  $-\boldsymbol{\tau}\cdot\boldsymbol{u}$: 粘性力所做的功（粘性耗散）。
3.  $\boldsymbol{q}$: **[热传导](@entry_id:147831)通量**，通常由傅里叶定律（Fourier's law）描述：$\boldsymbol{q} = -\lambda \nabla T$，其中 $\lambda$ 是[热导率](@entry_id:147276)，$T$ 是温度。
4.  $\sum_{k=1}^{N_s} h_k \boldsymbol{J}_k$: 由组分[扩散](@entry_id:141445)引起的[能量输运](@entry_id:183081)。每种[扩散](@entry_id:141445)的组分 $k$ 都携带其自身的比焓 $h_k$。

值得注意的是，当比焓 $h_k$ 的定义包含了组分在参考温度下的**[标准生成焓](@entry_id:144770)**时，总能量方程中便不再出现显式的[化学反应](@entry_id:146973)热源项。[化学反应](@entry_id:146973)的能量释放或吸收，通过组分[质量分数](@entry_id:161575) $Y_k$ 的变化（由[组分守恒方程](@entry_id:151288)决定）与各自焓值的耦合，被内在地、精确地计入了[能量平衡](@entry_id:150831)中。

### [热力学](@entry_id:141121)与输运性质

上述控制[方程组](@entry_id:193238)是不封闭的，因为它引入了许多未知量，如压力 $p$、比焓 $h_k$、粘度 $\mu$、[热导率](@entry_id:147276) $\lambda$ 以及[扩散通量](@entry_id:748422) $\boldsymbol{J}_k$。为了封闭[方程组](@entry_id:193238)，我们必须提供这些量的物性模型，即**[本构关系](@entry_id:186508)**。

#### [状态方程](@entry_id:274378)与热力学性质

对于许多工程应用中的气体混合物，理想气体假设是一个良好且极具实用价值的近似。

- **[理想气体混合物](@entry_id:149212)状态方程**:
根据[道尔顿分压定律](@entry_id:140483)，混合物的[总压](@entry_id:265293)力是各组分分压之和。对每一种组分应用[理想气体定律](@entry_id:146757)，可以推导出混合物的状态方程 [@problem_id:3356464]：
$$
p = \rho R_m T
$$
其中，$R_m$ 是混合物的**比气体常数**。一个至关重要的结论是，正确的混合法则是对各组分比气体常数 $R_k = R_u / W_k$（$R_u$ 是[普适气体常数](@entry_id:136843)，$W_k$ 是组分 $k$ 的[摩尔质量](@entry_id:146110)）进行质量分数加权平均：
$$
R_m = \sum_{k=1}^{N_s} Y_k R_k
$$
这个关系式也等价于 $R_m = R_u / \bar{W}$，其中 $\bar{W}$ 是混合物的平均[摩尔质量](@entry_id:146110)。需要强调的是，采用[摩尔分数](@entry_id:145460) $X_k$ 对 $R_k$ 进行加权平均通常是错误的。此[状态方程](@entry_id:274378)是一个“状态”关系，它在任何时刻对任何组分成分都成立，与[化学反应](@entry_id:146973)是否达到平衡无关。

当然，在极高压力下，分子的有限体积和分子间作用力变得不可忽略，理想气体假设会失效。在这种情况下，必须采用**[真实气体状态方程](@entry_id:154572)**，例如引入可[压缩因子](@entry_id:145979) $Z(p, T, \boldsymbol{Y})$，将[状态方程](@entry_id:274378)修正为 $p = Z \rho R_m T$ [@problem_id:3356464]。

- **[热力学性质](@entry_id:146047)的计算**:
焓和内能等[热力学性质](@entry_id:146047)是温度和组分的函数。对于热完全气体（比[热容](@entry_id:137594)仅为温度的函数），组分 $k$ 的比焓 $h_k(T)$ 和比内能 $e_k(T)$ 可以通[过积分](@entry_id:753033)其比[热容](@entry_id:137594) $c_{p,k}(T)$ 和 $c_{v,k}(T)$ 得到：
$$
h_k(T) = \Delta h_{f,k}^{0}(T_{\mathrm{ref}}) + \int_{T_{\mathrm{ref}}}^{T} c_{p,k}(T') \, dT'
$$
$$
e_k(T) = h_k(T) - R_k T
$$
其中 $\Delta h_{f,k}^{0}(T_{\mathrm{ref}})$ 是在参考温度 $T_{\mathrm{ref}}$ 下的[标准生成焓](@entry_id:144770)。在计算流体力学中，比热容通常采用经验多项式来表示，例如广泛使用的**NASA七系数多项式** [@problem_id:3356471]。例如，摩尔定[压比](@entry_id:137698)热 $c_{p,k}^{\text{molar}}(T)$ 可以表示为：
$$
\frac{c_{p,k}^{\text{molar}}(T)}{R_{u}} = a_{1,k} + a_{2,k}T + a_{3,k}T^{2} + a_{4,k}T^{3} + a_{5,k}T^{4}
$$
通过对该多项式进行积分，可以方便地计算任意温度下的焓值。混合物的比焓则通过对组分比焓进行[质量分数](@entry_id:161575)加权获得：$h_{\mathrm{mix}}(T, \boldsymbol{Y}) = \sum_k Y_k h_k(T)$。在CFD求解过程中，能量方程给出的往往是混合物焓值，而我们需要求解的是温度。由于 $h_{\mathrm{mix}}(T)$ 是温度的单调递增函数（因为 $c_{p, \mathrm{mix}} = \frac{dh}{dT} > 0$），我们可以通过牛顿-拉夫逊等迭代方法高效地从已知的焓值反解出温度 [@problem_id:3356471]。

#### 组分输运与扩散模型

组分[扩散通量](@entry_id:748422) $\boldsymbol{J}_k$ 的精确描述需要求解复杂的[Stefan-Maxwell方程](@entry_id:192069)，这在计算上非常昂贵。因此，在许多[CFD应用](@entry_id:144462)中，会采用简化的模型，其中最常见的是**混合物平均扩散模型**（mixture-averaged diffusion model）。

在该模型中，组分 $k$ 的[扩散通量](@entry_id:748422) $\boldsymbol{J}_k$ 被近似为由不同物理效应驱动的通量之和。一个常见的形式是 [@problem_id:3356494]：
$$
\boldsymbol{J}_k = - \rho D_{k,m} \nabla Y_k - \rho Y_k D_{T,k} \nabla \ln T
$$
第一项是**[菲克扩散](@entry_id:162897)**（Fickian diffusion），由组分自身的[浓度梯度](@entry_id:136633)驱动，$D_{k,m}$ 是组分 $k$ 在混合物中的[有效扩散系数](@entry_id:183973)。第二项是**热扩散**或**[索雷效应](@entry_id:146479)**（Soret effect），由[温度梯度](@entry_id:136845)驱动，$D_{T,k}$ 是热扩散系数。

一个至关重要的物理约束是，所有[扩散通量](@entry_id:748422)之和必须为零，这是[质量平均速度](@entry_id:149575)定义的直接结果：
$$
\sum_{k=1}^{N_s} \boldsymbol{J}_k = \mathbf{0}
$$
然而，上述简化的通量模型（我们记为 $\boldsymbol{J}_k^{(0)}$）通常不自动满足这个约束。因此，必须施加一个**修正**来强制满足该约束。标准的做法是引入一个所有组分共享的“修正速度” $\boldsymbol{V}_c$，并将修正后的通量定义为 $\boldsymbol{J}_k = \boldsymbol{J}_k^{(0)} + \rho Y_k \boldsymbol{V}_c$。通过强制 $\sum_k \boldsymbol{J}_k = \mathbf{0}$，可以解出所需的修正速度 [@problem_id:3356494]：
$$
\boldsymbol{V}_c = -\frac{1}{\rho} \sum_{j=1}^{N_s} \boldsymbol{J}_j^{(0)}
$$
这个步骤确保了总质量的守恒。

在燃烧学中，**刘易斯数**（Lewis number）$Le_k$ 是一个关键的无量纲参数，它量化了热量[扩散](@entry_id:141445)与[质量扩散](@entry_id:149532)的相对速率：
$$
Le_k = \frac{\lambda}{\rho c_p D_{k,m}} = \frac{\alpha}{D_{k,m}}
$$
其中 $\alpha = \lambda/(\rho c_p)$ 是热扩散系数。当 $Le_k = 1$ 时，热量与组分 $k$ 以相同的速率[扩散](@entry_id:141445)。当 $Le_k \neq 1$ 时，即存在**[差异扩散](@entry_id:195870)**（differential diffusion）。例如，在[预混火焰](@entry_id:203757)中，如果亏缺反应物（limiting reactant）的刘易斯数 $Le_d  1$，意味着该反应物比热量[扩散](@entry_id:141445)得更快。这会导致反应物“泄漏”到火焰面上游更远的地方，在反应区形成局部富集，从而增强[反应速率](@entry_id:139813)并提高[层流火焰速度](@entry_id:202145) $s_L$。反之，如果 $Le_d > 1$，反应物[扩散](@entry_id:141445)慢于热量，导致反应区局部贫化，从而降低[火焰速度](@entry_id:201679) [@problem_id:3356508]。

### [有限速率化学](@entry_id:749365)动力学

[化学源项](@entry_id:747323) $\dot{\omega}_k$ 描述了[化学反应](@entry_id:146973)如何改变流场中的组分构成和能量[分布](@entry_id:182848)。对于[有限速率化学](@entry_id:749365)模型，这些源项的计算基于化学动力学原理。

#### [反应速率](@entry_id:139813)与源项

- **质量作用定律**: 对于一个元（基元）可逆反应 $r$: $\sum_i \nu_{i,r}' \chi_i \leftrightharpoons \sum_i \nu_{i,r}'' \chi_i$，其净[反应速率](@entry_id:139813)（rate of progress）$\dot{q}_r$ 由正向和逆向[反应速率](@entry_id:139813)之差给出 [@problem_id:3356463]：
$$
\dot{q}_r = k_{f,r} \prod_i C_i^{\nu_{i,r}'} - k_{b,r} \prod_i C_i^{\nu_{i,r}''}
$$
这里，$\chi_i$ 是组分 $i$ 的化学式，$\nu_{i,r}'$ 和 $\nu_{i,r}''$ 分别是其作为反应物和产物的[化学计量系数](@entry_id:204082)。关键在于，[反应速率](@entry_id:139813)取决于**摩尔浓度** $C_i$（单位 $\mathrm{mol}/\mathrm{m}^3$），因为它直接反映了单位体积内的分子数密度，而[化学反应](@entry_id:146973)是分子间碰撞的结果。摩尔浓度与质量分数的关系为：
$$
C_i = \frac{\rho Y_i}{W_i}
$$

- **[阿伦尼乌斯定律](@entry_id:261434)**: 反应速率常数 $k_r$ 对温度的依赖性通常通过**广义阿伦尼乌斯公式**描述：
$$
k_r(T) = A_r T^{n_r} \exp\left(-\frac{E_{a,r}}{R_u T}\right)
$$
其中 $A_r$ 是指前因子，$n_r$ 是温度指数，$E_{a,r}$ 是活化能。由于活化能是每摩尔的能量，分母中必须使用[普适气体常数](@entry_id:136843) $R_u$ [@problem_id:3356463]。

- **[质量生成](@entry_id:161427)率**: 组分 $k$ 的总[质量生成](@entry_id:161427)率 $\dot{\omega}_k$ 是其在所有[化学反应](@entry_id:146973) $r$ 中生成率的总和。从摩尔基的[反应速率](@entry_id:139813) $\dot{q}_r$ 转换到质量基的生成率 $\dot{\omega}_k$ 需要乘以摩尔质量 $W_k$ 并加和所有反应的贡献：
$$
\dot{\omega}_k = W_k \sum_r (\nu_{k,r}'' - \nu_{k,r}') \dot{q}_r
$$

#### [反应热](@entry_id:140993)化学

[化学反应](@entry_id:146973)伴随着能量的释放（放热反应）或吸收（[吸热反应](@entry_id:139150)）。反应的焓变 $\Delta h_r(T)$ 是产物的[总焓](@entry_id:197863)与反应物的[总焓](@entry_id:197863)之差。根据**[基尔霍夫定律](@entry_id:180785)**（Kirchhoff's Law），[反应焓](@entry_id:149764)在不同温度下的值可以通过对反应前后比[热容](@entry_id:137594)之差 $\Delta c_p(T)$ 进行积分来关联 [@problem_id:3356492]：
$$
\Delta h_r(T) = \Delta h_r^{\circ}(T_{\mathrm{ref}}) + \int_{T_{\mathrm{ref}}}^{T} \Delta c_p(T') \,dT'
$$
其中 $\Delta c_p(T') = \sum_{\text{products}} \nu_i c_{p,i}(T') - \sum_{\text{reactants}} \nu_i c_{p,i}(T')$。这个关系对于理解温度如何影响反应的能量效应至关重要。

#### 高级动力学模型

实际的[化学反应](@entry_id:146973)机理通常包含比简单的二[分子碰撞](@entry_id:137334)更复杂的过程。例如，**[单分子反应](@entry_id:167301)**和**[三体反应](@entry_id:185833)**的[速率常数](@entry_id:196199)会表现出对压力的依赖性。一个典型的例子是单分子分解或异构化反应，其机理涉及通过与第三方碰撞物 $M$ 碰撞获得能量的中间态 $A^*$。在低压下，[反应速率](@entry_id:139813)与 $[M]$ 成正比；在高压下，[反应速率](@entry_id:139813)与 $[M]$ 无关，达到一个极限值。连接这两个极限的压力区间被称为**坠落区**（fall-off region）。

**Troe 公式**是一种精确拟合坠落区行为的常用方法 [@problem_id:3356514]。它通过引入一个修正因子 $F$ 来修正简单的[Lindemann-Hinshelwood](@entry_id:155779)模型，使得[有效速率常数](@entry_id:202512) $k_{\text{eff}}$ 能够平滑地从低压过渡到[高压极限](@entry_id:190919)。其形式如下：
$$
k_{\text{eff}} = k_{\infty} \left( \frac{P_r}{1+P_r} \right) F
$$
其中 $k_{\infty}$ 是[高压极限](@entry_id:190919)[速率常数](@entry_id:196199)，**折合压力** $P_r = \frac{k_0 [M]_{\text{eff}}}{k_{\infty}}$（$k_0$ 是低压极限速率常数），$[M]_{\text{eff}}$ 是考虑了不同碰撞伙伴效率的有效[三体](@entry_id:265960)浓度。因子 $F$ 的计算涉及复杂的经验公式和多个Troe参数，这些参数通常由理论计算或实验数据拟合得到。

### 数值考量：[刚性问题](@entry_id:142143)

在数值求解[反应流](@entry_id:190684)控制方程时，一个核心挑战是**刚性**（stiffness）。刚性源于系统中存在多个尺度差异巨大的[特征时间尺度](@entry_id:276738)。

#### 时间尺度与刚性

在[反应流](@entry_id:190684)中，主要存在三类时间尺度 [@problem_id:3356485]：
- **[对流](@entry_id:141806)时间尺度**: $\tau_{\text{conv}} = L_c / U$，表示流体穿过一个特征长度为 $L_c$ 的网格所需的时间。
- **[扩散时间尺度](@entry_id:264558)**: $\tau_{\text{diff}} = L_c^2 / D_{\text{mix}}$，表示质量或热量通过[扩散](@entry_id:141445)穿过一个网格所需的时间。
- **化学时间尺度**: $\tau_{\text{chem}}$，表示[化学反应](@entry_id:146973)[达到平衡](@entry_id:170346)或显著改变[组分浓度](@entry_id:197022)所需的时间。

化学时间尺度可以通过对[化学源项](@entry_id:747323) $\boldsymbol{\dot{\omega}}$ 关于组分向量 $\boldsymbol{Y}$ 的**雅可比矩阵** $\boldsymbol{J}_{\omega} = \frac{\partial \boldsymbol{\dot{\omega}}}{\partial \boldsymbol{Y}}$ 进行线性化分析得到。化学时间尺度由该[雅可比矩阵的特征值](@entry_id:264008)的倒数决定，代表了系统中最快的[化学反应](@entry_id:146973)模式：
$$
\tau_{\text{chem}} = \frac{1}{\max(|\text{eig}(\frac{1}{\rho}\boldsymbol{J}_{\omega})|)}
$$
当最快的化学时间尺度远小于[流体动力学](@entry_id:136788)时间尺度（[对流](@entry_id:141806)或[扩散](@entry_id:141445)）时，系统即为**刚性系统**。刚性比可以定义为：
$$
S = \frac{\min(\tau_{\text{conv}}, \tau_{\text{diff}})}{\tau_{\text{chem}}}
$$
如果 $S \gg 1$，则意味着[化学反应](@entry_id:146973)极快。若使用标准的[显式时间积分](@entry_id:165797)方法，为了维持数值稳定性，时间步长 $\Delta t$ 必须小于 $\tau_{\text{chem}}$，这会导致计算成本过高而难以接受。

#### 针对[刚性系统](@entry_id:146021)的数值方法

为了克服刚性问题，需要采用特殊的数值方法。**隐式-显式（IMEX）方法**是一种高效的策略 [@problem_id:3356465]。其核心思想是：对非刚性项（如[对流](@entry_id:141806)和[扩散](@entry_id:141445)）采用计算成本较低的显式格式处理，而对导致刚性的项（[化学源项](@entry_id:747323)）采用具有更好稳定性的[隐式格式](@entry_id:166484)处理。

以一种单步**Rosenbrock-W**方法为例，其求解一个时间步的过程可以归结为求解一个[线性方程组](@entry_id:148943)。对于[半离散化](@entry_id:163562)的[常微分方程组](@entry_id:266774) $\frac{d\mathbf{u}}{dt} = \mathbf{F}^E(\mathbf{u}) + \mathbf{F}^I(\mathbf{u})$（$\mathbf{F}^E$ 为显式项，$\mathbf{F}^I$ 为隐式项），更新步 $\mathbf{k}$ 通过求解以下[线性系统](@entry_id:147850)获得：
$$
(\mathbf{I} - \gamma \Delta t \mathbf{J}_n) \mathbf{k} = \Delta t \left( \mathbf{F}^E(\mathbf{u}_n) + \mathbf{F}^I(\mathbf{u}_n) \right)
$$
其中 $\mathbf{u}_n$ 是当前时刻的状态，$\Delta t$ 是时间步长，$\gamma$ 是方法参数，$\mathbf{J}_n$ 是在 $\mathbf{u}_n$ 处评估的隐式项（[化学源项](@entry_id:747323)）的雅可比矩阵。求解出 $\mathbf{k}$ 后，下一时刻的状态即为 $\mathbf{u}_{n+1} = \mathbf{u}_n + \mathbf{k}$。

这种方法将[非线性](@entry_id:637147)的化学动力学问题在每个时间步内转化为一个线性代数问题，其稳定性不受化学时间尺度的限制，从而允许使用由[流体动力学](@entry_id:136788)决定的、大得多的时间步长。这正是CFD中高效模拟复杂[化学反应](@entry_id:146973)流的关键技术之一。