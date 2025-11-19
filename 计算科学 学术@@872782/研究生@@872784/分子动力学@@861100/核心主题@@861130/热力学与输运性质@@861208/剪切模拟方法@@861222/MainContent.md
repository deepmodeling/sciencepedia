## 引言
在连接原子尺度的微观世界与宏观材料行为的探索中，[非平衡分子动力学](@entry_id:752558)（NEMD）扮演着至关重要的角色。尤其是在研究流体和[软物质](@entry_id:150880)的力学响应时，模拟材料在剪切作用下的行为是理解其[流变性](@entry_id:152243)质（如黏度、弹性和塑性）的关键。然而，在有限尺寸的周期性模拟盒子中施加一个连续、无限的剪切流场，带来了一个根本性的挑战：如何使宏观的连续变形与微观的离散周期性边界相容？本文旨在系统性地解决这一问题，为读者提供一套完整、精确的[剪切流模拟](@entry_id:754759)理论与实践框架。

为了实现这一目标，本文将分为三个核心部分。首先，在“原理与机制”一章中，我们将深入探讨非平衡定常态的基本概念，建立涨落速度的理论基础，并详细推导[Lees-Edwards边界条件](@entry_id:751228)和SLLOD运动方程，揭示它们如何协同工作以构建一个物理上自洽的剪切环境。接着，在“应用与跨学科联系”一章中，我们将展示这些方法如何应用于[计算流变学](@entry_id:747633)，以测量材料的宏观响应，并探讨其如何连接[连续介质力学](@entry_id:155125)和[非平衡统计力学](@entry_id:155589)等更广阔的理论领域。最后，通过“动手实践”部分提供的一系列具体问题，读者将有机会将理论知识转化为实际的计算技能，从而加深对算法实现细节和物理内涵的理解。通过这一结构化的学习路径，本文将引导你全面掌握现代剪切[模拟方法](@entry_id:751987)的核心精髓。

## 原理与机制

在[非平衡分子动力学](@entry_id:752558)（NEMD）中模拟流体在剪切作用下的行为，需要一套专门的理论和算法框架。与[平衡态](@entry_id:168134)模拟不同，剪切系统本质上处于一个由外部驱动维持的[稳态](@entry_id:182458)，持续有能量输入和耗散。本章将系统阐述在周期性边界条件下施加均匀[剪切流](@entry_id:266817)的核心原理与关键机制，内容涵盖流场分解、边界条件构建、运动方程推导、[能量平衡](@entry_id:150831)与恒温控制，以及相关物性（如黏度）的计算方法。

### 流动分解：流场速度与涨落速度

在研究非平衡系统时，首要任务是将微观粒子的运动分解为两部分：[宏观有序](@entry_id:155481)的集体运动和微观无序的热运动。对于一个受均匀剪切的系统，我们可以定义一个**流场速度（streaming velocity）** $\mathbf{u}(\mathbf{r})$，它描述了流体在空间位置 $\mathbf{r}$ 处的平均宏观速度。对于一个[速度梯度张量](@entry_id:270928)恒定的[均匀流](@entry_id:272775)，该关系是线性的：$\mathbf{u}(\mathbf{r}) = \boldsymbol{\kappa} \cdot \mathbf{r}$。一个标准的平面[Couette流](@entry_id:260750)，即剪切流方向为 $x$ 方向，速度梯度方向为 $y$ 方向，其流场速度由剪切速率 $\dot{\gamma}$ 定义为 $\mathbf{u}(\mathbf{r}) = \dot{\gamma}y\hat{\mathbf{x}}$。

相应地，粒子 $i$ 的**涨落速度（peculiar velocity）** $\mathbf{c}_i$ 被定义为其总速度 $\mathbf{v}_i$ 相对于其所在位置 $\mathbf{r}_i$ 处的流场速度的差值：

$$
\mathbf{c}_i = \mathbf{v}_i - \mathbf{u}(\mathbf{r}_i)
$$

这个分解至关重要，因为它将粒子的总动能划分为与宏观流动相关的有序动能和与热运动相关的无序动能。非平衡态下的[热力学性质](@entry_id:146047)，如**温度**，以及[输运性质](@entry_id:203130)，如**应力**和**热流**，必须在流体的**局域静止参考系（local rest frame）**中定义。这个[参考系](@entry_id:169232)就是随着流场速度 $\mathbf{u}$ 一起运动的[参考系](@entry_id:169232)。因此，所有这些物理量的计算都必须基于涨落速度 $\mathbf{c}_i$ [@problem_id:3445250]。

例如，系统的[动理学温度](@entry_id:751035) $T$ 正比于涨落动能的平均值，即 $\frac{d}{2} N k_B T = \sum_{i=1}^N \frac{1}{2} m_i \langle \mathbf{c}_i^2 \rangle$，其中 $d$ 是空间维度，$N$ 是粒子数，$k_B$ 是玻尔兹曼常数。如果错误地使用总速度 $\mathbf{v}_i$ 来计算温度，将会把宏观流动的动能（$\frac{1}{2} m_i \mathbf{u}(\mathbf{r}_i)^2$）错误地计入热能，导致温度的严重高估，且该“温度”会依赖于粒子在梯度方向的位置。

同理，[应力张量](@entry_id:148973)和热流等输运系数的[本构关系](@entry_id:186508)是在局域静止参考系中构建的，它们描述的是由分子热运动引起的动量和能量的[扩散输运](@entry_id:150792)，而非宏观流动的[对流输运](@entry_id:149512)。因此，在计算这些量的动理学贡献时，必须使用涨落速度，以剥离[对流](@entry_id:141806)项的干扰。

为了更深刻地理解这一点，我们可以思考一个思想实验：如果[恒温器](@entry_id:169186)错误地作用于粒子的总速度 $\mathbf{v}_i$ 而不是涨落速度 $\mathbf{c}_i$，会发生什么？在这种情况下，[恒温器](@entry_id:169186)会试图移除所有动能，包括宏观流动的有序动能。这在宏观上等效于施加了一个与流场速度方向相反的[体力](@entry_id:174230) $\mathbf{f}(y) \propto -\mathbf{u}(y)$。在[稳态](@entry_id:182458)下，这个非物理的[体力](@entry_id:174230)必须由应力梯度来平衡，即 $\frac{d \sigma_{xy}}{dy} \neq 0$。这将导致[剪切应力](@entry_id:137139) $\sigma_{xy}$ 沿梯度方向呈现非均匀的抛物线[分布](@entry_id:182848)。同时，由于[恒温器](@entry_id:169186)从系统不同位置移除能量的速率不同（在流速大的地方移除更多），会导致能量平衡被破坏，最终形成一个非均匀的温度[分布](@entry_id:182848)，其剖面通常在流速为零的中心处最高，在边界处最低 [@problem_id:3445252]。这清晰地表明，为了获得物理上正确的均匀[剪切流模拟](@entry_id:754759)，必须将控制和测量的对象都限定在涨落速度上。

### 周期性边界条件下的剪切：Lees-Edwards方法

在分子动力学模拟中，周期性边界条件（PBC）是模拟宏观体系的标准技术。然而，对于剪切流，一个根本性的矛盾出现了：流场[速度剖面](@entry_id:266404) $\mathbf{u}(\mathbf{r}) = \dot{\gamma}y\hat{\mathbf{x}}$ 要求模拟盒的“顶面”（如 $y=L_y/2$）相对于“底面”（$y=-L_y/2$）以速度 $\dot{\gamma}L_y$ 滑動。这与标准立方体周期性盒子的静态[晶格结构](@entry_id:145664)不相容。

**[Lees-Edwards边界条件](@entry_id:751228)（Lees-Edwards boundary conditions, LEBC）** 通过引入一个随时间变形的（或“滑动的”）周期性映像，巧妙地解决了这个问题 [@problem_id:3445316]。其核心思想是定义一个随流场变形的**协剪切[参考系](@entry_id:169232)（co-shearing frame）**。在这个[参考系](@entry_id:169232)中，周期性是静态且正交的。而在我们观察的实验室参考系中，边界是滑动的。

让我们通过一个[仿射变换](@entry_id:144885)来 formalize 这个过程。设实验室坐标为 $\mathbf{r}$，协剪切坐标为 $\mathbf{r}_{cs}$。一个在协剪切[坐标系](@entry_id:156346)中静止的点，在实验室系中将以流场速度运动。在时间 $t$ 内，这个点在 $x$ 方向的位移为 $\dot{\gamma} y t$。因此，从协剪切坐标到实验室坐标的变换是：

$$
\mathbf{r} = \begin{pmatrix} 1  \dot{\gamma} t  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix} \mathbf{r}_{cs}
$$

反之，从实验室坐标到协剪切坐标的变换为：

$$
\mathbf{r}_{cs} = \begin{pmatrix} 1  -\dot{\gamma} t  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix} \mathbf{r}
$$

当一个粒子在时刻 $t$ 穿过 $y$ 方向的边界时（例如，从 $y$ 移动到 $y - sL_y$，其中 $s=\pm 1$），我们可以在简单的协剪切[坐标系](@entry_id:156346)中处理这个事件。粒子在协剪切[坐标系](@entry_id:156346)中的 $y_{cs}$ 坐标平移了 $-sL_y$。然后，我们再将新的协剪切[坐标变换](@entry_id:172727)回实验室坐标。整个过程可以总结为：

$$
\mathbf{r}_{\text{new}} = \mathbf{A}^{-1}(t) \left( \mathbf{A}(t)\mathbf{r}_{\text{old}} - \begin{pmatrix} 0 \\ sL_y \\ 0 \end{pmatrix} \right) = \mathbf{r}_{\text{old}} - \mathbf{A}^{-1}(t) \begin{pmatrix} 0 \\ sL_y \\ 0 \end{pmatrix}
$$

其中 $\mathbf{A}(t)$ 是从实验室到协剪切的变换矩阵。计算得出，这个变换等效于以下的坐标重映规则：

$$
\begin{cases}
x'  = x - s \dot{\gamma} t L_y \\
y'  = y - s L_y \\
z'  = z
\end{cases}
$$

其中，总应变 $\gamma(t)=\dot{\gamma}t$ 表示了周期性映像在 $x$ 方向上相对于 $y$ 方向平移 $L_y$ 时的总位移。

LEBC 是为平面[Couette流](@entry_id:260750)设计的。对于更一般的[均匀流](@entry_id:272775)，如[单轴拉伸](@entry_id:188287)（$\boldsymbol{\kappa}=\text{diag}(\dot{\epsilon},-\dot{\epsilon}/2,-\dot{\epsilon}/2)$）或双轴拉伸（$\boldsymbol{\kappa}=\text{diag}(\dot{\epsilon},\dot{\epsilon},-2\dot{\epsilon})$），模拟盒本身会在拉伸方向上伸长，在压缩方向上收缩。在这种情况下，需要使用更广义的周期性边界条件，如Kraynik-Reinelt算法，它允许模拟盒的[晶格](@entry_id:196752)[基矢](@entry_id:199546)随[时间演化](@entry_id:153943)，并通过周期性的[晶格](@entry_id:196752)重构来避免盒子形状变得过于狭长，从而维持模拟的稳定性 [@problem_id:3445260]。

### 剪切系统的[运动方程](@entry_id:170720)：[SLLOD算法](@entry_id:754951)

与边界条件相容的运动方程对于正确模拟[剪切流](@entry_id:266817)至关重要。**[SLLOD算法](@entry_id:754951)**（其名称是DOLLS的历史倒写，并无特殊含义）提供了一套与LEBC完全相容的[运动方程](@entry_id:170720)。SLLOD方程直接描述涨落动量 $\mathbf{p}_i = m_i\mathbf{c}_i$ 的演化 [@problem_id:3445299]。

我们可以从牛顿第二定律 $\dot{\mathbf{v}}_i = \mathbf{F}_i/m_i$ 和涨落动量的定义出发推导。对 $\mathbf{p}_i$ 求时间导数：

$$
\dot{\mathbf{p}}_i = m_i \dot{\mathbf{v}}_i - m_i \frac{d}{dt}\mathbf{u}(\mathbf{r}_i(t)) = \mathbf{F}_i - m_i (\mathbf{v}_i \cdot \nabla)\mathbf{u}(\mathbf{r}_i)
$$

注意到 $(\mathbf{v}_i \cdot \nabla)\mathbf{u}$ 可以写作 $\boldsymbol{\kappa} \cdot \mathbf{v}_i$。然后，将 $\mathbf{v}_i$ 用涨落速度和流场速度表示，$\mathbf{v}_i = \mathbf{c}_i + \mathbf{u}(\mathbf{r}_i) = \mathbf{p}_i/m_i + \boldsymbol{\kappa}\cdot\mathbf{r}_i$。代入后得到：

$$
\dot{\mathbf{p}}_i = \mathbf{F}_i - m_i \boldsymbol{\kappa} \cdot (\mathbf{p}_i/m_i + \boldsymbol{\kappa}\cdot\mathbf{r}_i) = \mathbf{F}_i - \boldsymbol{\kappa} \cdot \mathbf{p}_i - m_i (\boldsymbol{\kappa} \cdot \boldsymbol{\kappa}) \cdot \mathbf{r}_i
$$

[SLLOD算法](@entry_id:754951)忽略了 $\boldsymbol{\kappa}^2$ 的高阶项，因为它与驱动流动的线性响应无关。因此，SLLOD的动量方程为：

$$
\dot{\mathbf{p}}_i = \mathbf{F}_i - \boldsymbol{\kappa} \cdot \mathbf{p}_i
$$

对于 $\mathbf{u}(\mathbf{r})=\dot{\gamma}y\hat{\mathbf{x}}$，[速度梯度张量](@entry_id:270928) $\boldsymbol{\kappa}$ 只有一个非零分量 $\kappa_{xy}=\dot{\gamma}$。此时，SLLOD方程简化为：

$$
\dot{\mathbf{p}}_i = \mathbf{F}_i - \dot{\gamma}p_{iy}\hat{\mathbf{x}}
$$

值得注意的是，[SLLOD算法](@entry_id:754951)在物理上是自洽的。历史上曾有另一种算法，称为Doll's tensor算法，其动量方程中的剪切项为 $-\boldsymbol{\kappa}^T \cdot \mathbf{p}_i$。对于简单剪切，这意味着[驱动项](@entry_id:165986)变为 $-\dot{\gamma}p_{ix}\hat{\mathbf{y}}$。这两种算法的区别在于如何处理流动的旋转部分。[SLLOD算法](@entry_id:754951)源于[坐标系](@entry_id:156346)的精确变换，正确地包含了流动的应变和旋转部分，因此对于中心力作用的系统，它能保持角动量守恒，从而保证应力[张量的对称性](@entry_id:202126)（$\sigma_{xy} = \sigma_{yx}$）。而Doll's tensor算法则不正确地处理了旋转，相当于对系统施加了一个非物理的扭矩，导致应力张量出现人为的反对称部分 [@problem_id:3445314]。

### [能量平衡](@entry_id:150831)与[恒温器](@entry_id:169186)

在[剪切流模拟](@entry_id:754759)中，剪切力持续对系统做功，将[机械能](@entry_id:162989)转化为内能，这个过程称为**黏性加热（viscous heating）**。单位时间内输入系统的功率 $\dot{W}$ 与剪切应力和剪切速率成正比：

$$
\dot{W} = -V \sigma_{xy} \dot{\gamma}
$$

其中 $V$ 是系统体积，$\sigma_{xy}$ 是[剪切应力](@entry_id:137139)。为维持系统处于[非平衡稳态](@entry_id:141783)，必须通过**恒温器（thermostat）**以相同的速率 $\dot{Q}$ 将这些多余的热量移除。因此，在[稳态](@entry_id:182458)下，[能量平衡方程](@entry_id:191484)为：

$$
\langle \dot{W} \rangle = \langle \dot{Q} \rangle
$$

这个平衡关系是检验NEMD模拟正确性的一个基本标准 [@problem_id:3445273]。

不同的[恒温器](@entry_id:169186)通过不同的机制移除热量。例如，**高斯等动能[恒温器](@entry_id:169186)（Gaussian isokinetic thermostat）**通过引入一个摩擦项 $-\alpha\mathbf{p}_i$ 来精确地保持系统的总涨落动能 $K = \sum_i \mathbf{p}_i^2 / (2m_i)$ 恒定。通过对[动能守恒](@entry_id:177660)条件 $\dot{K}=0$ 求解，可以得到[摩擦系数](@entry_id:150354) $\alpha$ 的瞬时表达式 [@problem_id:3445299] [@problem_id:3445251]：

$$
\alpha = \frac{\sum_{i=1}^{N} \mathbf{p}_i \cdot (\mathbf{F}_i/m_i) - \sum_{i=1}^{N} m_i^{-1} \mathbf{p}_i \cdot (\boldsymbol{\kappa} \cdot \mathbf{p}_i)}{\sum_{j=1}^{N} m_j^{-1} (\mathbf{p}_j \cdot \mathbf{p}_j)} = \frac{\dot{W}_{\text{forces}} + \dot{W}_{\text{shear}}}{2K}
$$

在这种情况下，[恒温器](@entry_id:169186)移出热量的速率为 $\dot{Q} = 2\alpha K$。其他[恒温器](@entry_id:169186)，如Nosé-Hoover或[Langevin恒温器](@entry_id:142944)，也有各自的能量移除机制，但最终都必须满足[稳态](@entry_id:182458)[能量平衡](@entry_id:150831)。

### 物性测量：应力与黏度

NEMD剪切模拟的一个主要目标是计算流体的[流变性](@entry_id:152243)质，其中最基本的是**剪切黏度（shear viscosity）** $\eta$。对于牛顿流体，剪切黏度定义为[剪切应力](@entry_id:137139)与剪切速率之比的负值：

$$
\eta = - \frac{\langle \sigma_{xy} \rangle}{\dot{\gamma}}
$$

这里的关键是计算微观的**应力张量（stress tensor）** $\boldsymbol{\sigma}$。根据Irving-Kirkwood理论，应力张量的瞬时表达式包含动理学和位形（或维里）两部分贡献。在均匀剪切的[稳态](@entry_id:182458)下，其[空间平均](@entry_id:203499)的 $xy$ 分量为 [@problem_id:3445259]：

$$
\sigma_{xy} = -\frac{1}{V} \left[ \sum_{i=1}^{N} m_i c_{ix} c_{iy} + \frac{1}{2} \sum_{i \neq j} r_{ij,x} F_{ij,y} \right]
$$

- **[动理学](@entry_id:136901)贡献**: $\sum_i m_i c_{ix} c_{iy}$，源于粒子涨落运动所携带的[动量输运](@entry_id:139628)。再次强调，这里必须使用涨落速度分量 $c_{ix}$ 和 $c_{iy}$。
- **位形贡献**: $\frac{1}{2} \sum_{i \neq j} r_{ij,x} F_{ij,y}$，源于粒子间相互作用力的传递。$\mathbf{r}_{ij} = \mathbf{r}_i - \mathbf{r}_j$ 是粒子对的距离矢量，$\mathbf{F}_{ij}$ 是粒子 $j$ 对粒子 $i$ 的作用力。在LEBC下，$\mathbf{r}_{ij}$ 必须使用满足剪切周期性的最小映像约定来计算。

通过在模拟过程中计算 $\sigma_{xy}$ 的[时间平均](@entry_id:267915)值 $\langle \sigma_{xy} \rangle$，就可以得到系统的宏观剪切黏度。

### 高级主题：[长程相互作用](@entry_id:140725)下的剪切模拟

当系统中存在长程相互作用（如静电作用）时，通常需要使用Ewald求和或其快速傅里叶变换版本（如PME）。这些方法依赖于系统的周期性，将相互作用分解为[实空间](@entry_id:754128)和倒易空间（Reciprocal Space）两部分。在LEBC下，[实空间](@entry_id:754128)[晶格](@entry_id:196752)是随时间变形的，这意味着[倒易空间](@entry_id:754151)[晶格](@entry_id:196752)也必须相应地演化，才能保持与变形的[实空间](@entry_id:754128)[晶格](@entry_id:196752)的对偶关系 [@problem_id:3445278]。

一个变形的实空间[晶格](@entry_id:196752)由[基矢](@entry_id:199546)矩阵 $A(t) = F(t)A_0$ 描述，其中 $F(t)$ 是变形梯度张量，$A_0$ 是初始的正交[晶格](@entry_id:196752)矩阵。相应的[倒易空间](@entry_id:754151)[基矢](@entry_id:199546)矩阵 $B(t)$ 由关系 $A(t)^T B(t) = 2\pi I$ 定义。可以证明，$B(t)$ 的演化遵循：

$$
B(t) = (F(t)^T)^{-1} B_0
$$

因此，一个[倒易晶格矢量](@entry_id:263351)（[波矢](@entry_id:178620)）$\mathbf{k}$ 的演化规则为 $\mathbf{k}(t) = (F(t)^T)^{-1} \mathbf{k}_0$。对于简单[剪切流](@entry_id:266817)，这具体表现为：

$$
k_x(t) = k_{0x}, \quad k_y(t) = k_{0y} - \gamma(t)k_{0x}, \quad k_z(t) = k_{0z}
$$

这正是[SLLOD算法](@entry_id:754951)对涨落动量中粒子位置的对偶变量（即[波矢](@entry_id:178620)）的演化方程。这个协变与反协变的演化规则保证了Ewald求和中核心的相位因子是不变的：

$$
\mathbf{k}(t) \cdot \mathbf{r}(t) = \mathbf{k}_0 \cdot \mathbf{r}_0
$$

这一[不变性](@entry_id:140168)是LEBC与Ewald求和方法能够兼容的理论基础，它确保了即使在[剪切变形](@entry_id:170920)的[晶格](@entry_id:196752)中，我们依然可以一致地计算[长程相互作用](@entry_id:140725)，为模拟[离子液体](@entry_id:272592)、[胶体悬浮液](@entry_id:267678)等[复杂流体](@entry_id:198415)在剪切下的行为提供了可能。