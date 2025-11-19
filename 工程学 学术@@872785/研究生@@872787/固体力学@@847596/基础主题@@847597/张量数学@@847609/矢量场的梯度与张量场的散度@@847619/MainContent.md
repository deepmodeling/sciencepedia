## 引言
在物理学与工程学中，理解物理量（如速度、应力）如何在空间中[分布](@entry_id:182848)和变化是至关重要的。矢量场的梯度和张量场的散度是[连续介质力学](@entry_id:155125)中描述这种空间变化的最基本、最强大的数学工具。它们解决了将运动的几何描述（运动学）与作用其上的力（动力学）在每一点上精确联系起来的核心问题，构成了现代力学理论的基石。本文将系统地引导读者掌握这两个核心概念。在“原理与机制”一章中，我们将从第一性原理出发，建立它们的数学定义和物理内涵。随后，在“应用与跨学科联系”一章中，我们将探索这些算子如何在[固体力学](@entry_id:164042)、[流体力学](@entry_id:136788)乃至广义相对论等多个领域中发挥作用。最后，通过“动手实践”一章中的一系列计算练习，您将有机会巩固所学知识，并将其应用于解决实际问题。

## 原理与机制

本章旨在深入探讨连续介质力学中两个核心的微分算子：矢量场的梯度与张量场的散度。我们将从基本定义出发，揭示它们的物理内涵，建立它们在运动学、动力学及[本构关系](@entry_id:186508)中的关键联系，并最终将这些概念推广至更广泛的数学框架中。我们假定读者已具备基础的[张量代数](@entry_id:161671)和多元微积分知识。

### 矢量场的梯度

在连续介质力学中，我们关注的物理量，如位移、速度和温度，通常是空间位置的函数，形成所谓的场。理解这些场如何在空间中变化，对于描述材料的变形和受力至关重要。矢量场的梯度正是量化这种空间变化的核心工具。

#### 从方向导数到张量

考虑一个光滑的矢量场 $\mathbf{v}(\mathbf{x})$。在某一点 $\mathbf{x}$，我们想知道沿任意方向 $\mathbf{h}$ 场的变化率，即[方向导数](@entry_id:189133)。这个[方向导数](@entry_id:189133)本身也是一个矢量：
$$
\lim_{\epsilon \to 0} \frac{\mathbf{v}(\mathbf{x}+\epsilon \mathbf{h}) - \mathbf{v}(\mathbf{x})}{\epsilon}
$$
可以证明，对于光滑的矢量场，这个方向导数是方向矢量 $\mathbf{h}$ 的线性函数。因此，必然存在一个二阶张量，我们称之为 $\mathbf{v}$ 的**梯度(gradient)**，记作 $\nabla \mathbf{v}$，它将方向 $\mathbf{h}$ 映射为该方向上的变化率：
$$
(\nabla \mathbf{v}) \mathbf{h} = \lim_{\epsilon \to 0} \frac{\mathbf{v}(\mathbf{x}+\epsilon \mathbf{h}) - \mathbf{v}(\mathbf{x})}{\epsilon}
$$
这个定义是坐标无关的，体现了梯度张量的内在物理意义。它完全捕捉了矢量场在一点附近的所有一阶变化信息。

#### [笛卡尔坐标系](@entry_id:169789)下的分量表示

为了进行具体计算，我们需要在选定的[坐标系](@entry_id:156346)下表示梯度张量的分量。在标准的右手[笛卡尔坐标系](@entry_id:169789)中，设[基矢](@entry_id:199546)量为 $\{\mathbf{e}_1, \mathbf{e}_2, \mathbf{e}_3\}$，位置矢量 $\mathbf{x} = x_i \mathbf{e}_i$，矢量场 $\mathbf{v} = v_i \mathbf{e}_i$。方向导数的第 $i$ 个分量可以写作标量场 $v_i$ 沿 $\mathbf{h}$ 方向的[方向导数](@entry_id:189133)，即 $\nabla v_i \cdot \mathbf{h}$。利用多元微积分的知识，我们知道 $\nabla v_i \cdot \mathbf{h} = \frac{\partial v_i}{\partial x_j} h_j$。

另一方面，$(\nabla \mathbf{v}) \mathbf{h}$ 的第 $i$ 个分量是 $((\nabla \mathbf{v}) \mathbf{h})_i = (\nabla \mathbf{v})_{ij} h_j$。这里我们采用了**爱因斯坦求和约定(Einstein summation convention)**，即在一个单项中重复出现两次的指标（此处为 $j$）表示对该指标的所有可能值（在三维空间中为1, 2, 3）进行求和。这种重复指标称为**[哑指标](@entry_id:188070)(dummy index)**。只出现一次的指标（此处为 $i$）称为**[自由指标](@entry_id:189430)(free index)**，它必须在等式两边保持一致，并标识了张量方程的分量。[@problem_id:2644954]

比较两种表达方式，我们得到：
$$
(\nabla \mathbf{v})_{ij} h_j = \frac{\partial v_i}{\partial x_j} h_j
$$
由于上式对任意方向 $\mathbf{h}$ 均成立，因此我们得到梯度张量的分量表达式：
$$
(\nabla \mathbf{v})_{ij} = \frac{\partial v_i}{\partial x_j}
$$
这个 $3 \times 3$ 的矩阵通常被称为雅可比矩阵。需要强调的是，第一个指标 $i$ 代表矢量的分量，第二个指标 $j$ 代表求导的坐标。其[转置](@entry_id:142115) $(\nabla \mathbf{v})^T_{ij} = (\nabla \mathbf{v})_{ji} = \frac{\partial v_j}{\partial x_i}$ 代表了不同的张量。在本书中，我们统一采用 $(\nabla \mathbf{v})_{ij} = \frac{\partial v_i}{\partial x_j}$ 作为定义。

#### 运动学诠释：[速度梯度张量](@entry_id:270928)

当矢量场 $\mathbf{v}$ 是连续介质中物[质点](@entry_id:186768)的[速度场](@entry_id:271461)时，其梯度 $\mathbf{L} = \nabla \mathbf{v}$ 被称为**[速度梯度张量](@entry_id:270928)(velocity gradient tensor)**。这个张量在描述材料点的局部运动时起着至关重要的作用。它可以唯一地分解为一个对称[部分和](@entry_id:162077)一个反对称部分：
$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$
其中，
$$
\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T) \quad \text{称为形变率张量 (rate of deformation tensor)}
$$
$$
\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T) \quad \text{称为自旋张量 (spin tensor)}
$$
**[形变率张量](@entry_id:184787)** $\mathbf{D}$ 描述了材料微元体形状和尺寸的变化率。它的对角分量 $D_{ii}$ 表示沿坐标轴方向的拉伸或压缩率，非对角分量 $D_{ij}$ ($i \neq j$) 表示相应平面内角度的剪切变化率的一半。

**[自旋张量](@entry_id:187346)** $\mathbf{W}$ 描述了材料微元体的刚性转动速率。它与[速度场的旋度](@entry_id:183606) $\nabla \times \mathbf{v}$ 密切相关，其[轴矢量](@entry_id:196296)（描述转动轴和速率的矢量）为 $\mathbf{w} = \frac{1}{2} \nabla \times \mathbf{v}$。[@problem_id:2644971]

例如，考虑一个二维[速度场](@entry_id:271461) $\mathbf{v}(x,y,z) = (ax - \omega y, \omega x - ay, 0)$。[@problem_id:2644971] 其[速度梯度张量](@entry_id:270928)为：
$$
\mathbf{L} = \begin{pmatrix} \frac{\partial v_x}{\partial x} & \frac{\partial v_x}{\partial y} & \frac{\partial v_x}{\partial z} \\ \frac{\partial v_y}{\partial x} & \frac{\partial v_y}{\partial y} & \frac{\partial v_y}{\partial z} \\ \frac{\partial v_z}{\partial x} & \frac{\partial v_z}{\partial y} & \frac{\partial v_z}{\partial z} \end{pmatrix} = \begin{pmatrix} a & -\omega & 0 \\ \omega & -a & 0 \\ 0 & 0 & 0 \end{pmatrix}
$$
对应的[形变率张量](@entry_id:184787)和[自旋张量](@entry_id:187346)分别为：
$$
\mathbf{D} = \begin{pmatrix} a & 0 & 0 \\ 0 & -a & 0 \\ 0 & 0 & 0 \end{pmatrix}, \quad \mathbf{W} = \begin{pmatrix} 0 & -\omega & 0 \\ \omega & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix}
$$
这清楚地表明，该运动由沿 $x$ 轴的拉伸、沿 $y$ 轴的压缩（由常数 $a$ 描述）以及绕 $z$ 轴的刚性旋转（由常数 $\omega$ 描述）叠加而成。

#### [体积应变率](@entry_id:272471)与矢量场的散度

[形变率张量](@entry_id:184787)的迹 $\mathrm{tr}(\mathbf{D})$ 有一个特别重要的物理意义。迹是指主对角线上元素的和。
$$
\mathrm{tr}(\mathbf{D}) = D_{ii} = \frac{1}{2} (L_{ii} + L^T_{ii}) = \frac{1}{2} \left(\frac{\partial v_i}{\partial x_i} + \frac{\partial v_i}{\partial x_i}\right) = \frac{\partial v_i}{\partial x_i}
$$
这个量 $\frac{\partial v_i}{\partial x_i}$ 正是速度场 $\mathbf{v}$ 的**散度(divergence)**，记作 $\nabla \cdot \mathbf{v}$。因此，我们有一个至关重要的关系：
$$
\nabla \cdot \mathbf{v} = \mathrm{tr}(\nabla \mathbf{v}) = \mathrm{tr}(\mathbf{D})
$$
$\mathrm{tr}(\mathbf{D})$ 被定义为**[体积应变率](@entry_id:272471)(volumetric strain rate)**，它表示材料微元单位体积的相对变化率。如果 $\nabla \cdot \mathbf{v} = 0$，则称运动是**等容的(isochoric)**或不可压缩的。[@problem_id:2644971] [@problem_id:2644961]

在有限变形理论中，局部体积变化由变形梯度 $\mathbf{F} = \mathbf{I} + \nabla \mathbf{u}$ 的[行列式](@entry_id:142978) $J = \det(\mathbf{F})$ 描述，其中 $\mathbf{u}$ 是[位移场](@entry_id:141476)，$J$ 表示变形后体积与参考构型体积之比。当应变很小时（即 $\nabla \mathbf{u}$ 的分量远小于1），我们可以对 $J$ 进行线性化。利用[行列式](@entry_id:142978)在单位张量 $\mathbf{I}$ 附近的展开式 $\det(\mathbf{I} + \mathbf{A}) \approx 1 + \mathrm{tr}(\mathbf{A})$，我们得到：
$$
J = \det(\mathbf{I} + \nabla \mathbf{u}) \approx 1 + \mathrm{tr}(\nabla \mathbf{u}) = 1 + \nabla \cdot \mathbf{u}
$$
这表明，在线性化理论中，位移场的散度 $\nabla \cdot \mathbf{u}$（即无穷小[体积应变](@entry_id:267252) $\varepsilon_v$）近似等于单位体积的改变量 $J-1$。这深刻地揭示了散度作为体积变化度量的几何意义。[@problem_id:2695497]

### [张量场](@entry_id:190170)的散度

正如矢量场的梯度描述了其空间变化，我们也需要一个算子来描述[二阶张量](@entry_id:199780)场（如应力张量场）的空间变化。这个算子就是张量场的散度。

#### 从积分形式到局部形式：[散度定理](@entry_id:143110)

与矢量场的梯度通过方向导数引入不同，[张量场](@entry_id:190170)的散度最自然的引入方式是通过一个推广的**[高斯散度定理](@entry_id:188065)(Gauss's Divergence Theorem)**。考虑一个任意光滑的[控制体积](@entry_id:143882) $V$，其边界为 $\partial V$，外[法线](@entry_id:167651)矢量为 $\mathbf{n}$。对于一个光滑的[二阶张量](@entry_id:199780)场 $\mathbf{T}(\mathbf{x})$，以下积分关系成立：
$$
\int_V (\nabla \cdot \mathbf{T}) \, \mathrm{d}V = \int_{\partial V} \mathbf{T} \mathbf{n} \, \mathrm{d}S
$$
这个定理定义了一个矢量场 $\nabla \cdot \mathbf{T}$，它的[体积分](@entry_id:171119)等于[张量场](@entry_id:190170) $\mathbf{T}$ 与法向矢量 $\mathbf{n}$ 的乘积在边界上的[面积分](@entry_id:275394)。[@problem_id:2644619] [@problem_id:2644987]

#### 物理诠释：力密度

这个定义的物理意义在力学中尤为明显。如果 $\mathbf{T}$ 是柯西应力张量 $\boldsymbol{\sigma}$，根据**柯西应力定理(Cauchy's Stress Theorem)**，作用在边界面元 $\mathrm{d}S$ 上的面力（或称**牵[引力](@entry_id:175476)(traction)**）矢量 $\mathbf{t}$ 由 $\mathbf{t} = \boldsymbol{\sigma} \mathbf{n}$ 给出。因此，散度定理的右侧[面积分](@entry_id:275394) $\int_{\partial V} \boldsymbol{\sigma} \mathbf{n} \, \mathrm{d}S$ 代表了作用在体积 $V$ 上的总[表面力](@entry_id:188034)。

散度定理的左侧是矢量场 $\nabla \cdot \boldsymbol{\sigma}$ 在体积 $V$ 上的积分。这表明 $\nabla \cdot \boldsymbol{\sigma}$ 是一个**力密度(force density)**，即单位体积所受到的由[表面应力](@entry_id:191241)产生的合力。通过取极限，我们可以看到这一点：
$$
(\nabla \cdot \mathbf{T})(\mathbf{x}_0) = \lim_{|V| \to 0} \frac{1}{|V|} \int_{\partial V} \mathbf{T} \mathbf{n} \, \mathrm{d}S
$$
这个表达式清晰地表明，[张量场](@entry_id:190170)的散度在一点的值，等于包围该点的无穷小[体积元](@entry_id:267802)单位体积上所受的净“通量”。当 $\mathbf{T}$ 为[应力张量](@entry_id:148973)时，这正是单位体积所受的净[表面力](@entry_id:188034)。[@problem_id:2644940] [@problem_id:2644619]

#### [笛卡尔坐标系](@entry_id:169789)下的分量表示

我们可以利用[散度定理](@entry_id:143110)的积分定义来推导其在[笛卡尔坐标系](@entry_id:169789)下的分量表达式。考虑上述矢量方程的第 $i$ 个分量：
$$
\int_V (\nabla \cdot \mathbf{T})_i \, \mathrm{d}V = \int_{\partial V} (\mathbf{T} \mathbf{n})_i \, \mathrm{d}S = \int_{\partial V} T_{ij} n_j \, \mathrm{d}S
$$
对于固定的 $i$，我们可以将张量 $\mathbf{T}$ 的第 $i$ 行看作一个矢量场 $\mathbf{r}^{(i)}$，其分量为 $(\mathbf{r}^{(i)})_j = T_{ij}$。于是，右侧的积分变为 $\int_{\partial V} \mathbf{r}^{(i)} \cdot \mathbf{n} \, \mathrm{d}S$。根据标准的矢量散度定理，这个面积分等于 $\int_V (\nabla \cdot \mathbf{r}^{(i)}) \, \mathrm{d}V$。而 $\nabla \cdot \mathbf{r}^{(i)} = \frac{\partial (\mathbf{r}^{(i)})_j}{\partial x_j} = \frac{\partial T_{ij}}{\partial x_j}$。

因此，我们有：
$$
\int_V (\nabla \cdot \mathbf{T})_i \, \mathrm{d}V = \int_V \frac{\partial T_{ij}}{\partial x_j} \, \mathrm{d}V
$$
由于此式对任意体积 $V$ 成立，被积函数必须相等。我们便得到了[张量散度](@entry_id:275263)的分量表达式：
$$
(\nabla \cdot \mathbf{T})_i = \frac{\partial T_{ij}}{\partial x_j}
$$
这表明，[张量散度](@entry_id:275263)这个矢量的第 $i$ 个分量，是张量矩阵第 $i$ 行对应矢量场的散度。[@problem_id:2644954] [@problem_id:2644619]

#### 应用：动量守恒的局部形式

[张量散度](@entry_id:275263)的概念是建立连续介质动力学[局部平衡](@entry_id:156295)方程的基石。动量守恒的积分形式（[牛顿第二定律](@entry_id:274217)）应用于一个随物质运动的体积（即物质体积）$V(t)$，表明其总动量的[物质导数](@entry_id:172646)等于作用于其上的总[表面力](@entry_id:188034)与总体积力之和：
$$
\frac{D}{Dt} \int_{V(t)} \rho \mathbf{v} \, \mathrm{d}V = \int_{\partial V(t)} \mathbf{t} \, \mathrm{d}S + \int_{V(t)} \mathbf{b} \, \mathrm{d}V
$$
其中 $\rho$ 是密度，$\mathbf{b}$ 是单位体积的[体力](@entry_id:174230)。根据[雷诺输运定理](@entry_id:191217)，左侧可写作 $\int_{V(t)} \rho \frac{D\mathbf{v}}{Dt} \mathrm{d}V$。令物[质点](@entry_id:186768)加速度为 $\mathbf{a} = \frac{D\mathbf{v}}{Dt}$。利用 $\mathbf{t} = \boldsymbol{\sigma} \mathbf{n}$ 和[张量散度](@entry_id:275263)定理，[表面力](@entry_id:188034)积分可转换为[体积分](@entry_id:171119) $\int_{V(t)} \nabla \cdot \boldsymbol{\sigma} \, \mathrm{d}V$。将所有项都合并为一个[体积分](@entry_id:171119)，我们得到：
$$
\int_{V(t)} (\rho \mathbf{a} - \nabla \cdot \boldsymbol{\sigma} - \mathbf{b}) \, \mathrm{d}V = \mathbf{0}
$$
由于此式对任意物质体积 $V(t)$ 成立，被积函数必须为零，从而得到**柯西第一运动定律(Cauchy's first law of motion)**的微分形式：
$$
\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \rho \mathbf{a}
$$
在没有加速度（静态平衡）且没有[体力](@entry_id:174230)的情况下，该方程简化为 $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$，这是[弹性静力学](@entry_id:198298)的基本方程。[@problem_id:2644619] [@problem_id:2644971]

一个重要的特例是静水压力场，其应力张量为 $\boldsymbol{\sigma} = -p(\mathbf{x})\mathbf{I}$，其中 $p$ 是压力，$\mathbf{I}$ 是单位张量。其散度为 $(\nabla \cdot \boldsymbol{\sigma})_i = \partial_j(-p \delta_{ij}) = -\partial_i p$。因此，$\nabla \cdot (-p\mathbf{I}) = -\nabla p$。[平衡方程](@entry_id:172166)变为大家所熟知的流体静力学方程 $\nabla p = \mathbf{b}$。[@problem_id:2644619]

### 基本恒等式与运算

掌握了梯度和散度的定义后，我们可以推导出一系列在实际计算中非常有用的恒等式。

#### 外积（并矢）

两个矢量 $\mathbf{a}$ 和 $\mathbf{b}$ 的**[外积](@entry_id:147029)(outer product)**或称**并矢(dyadic product)**，记作 $\mathbf{a} \otimes \mathbf{b}$，是一个[二阶张量](@entry_id:199780)，其分量为：
$$
(\mathbf{a} \otimes \mathbf{b})_{ij} = a_i b_j
$$
这个张量作用于另一个矢量 $\mathbf{c}$ 的结果是：
$$
(\mathbf{a} \otimes \mathbf{b})\mathbf{c} = \mathbf{a}(\mathbf{b} \cdot \mathbf{c})
$$
即，它将矢量 $\mathbf{c}$ 投影到 $\mathbf{b}$ 的方向上，然后将结果乘以矢量 $\mathbf{a}$。[外积](@entry_id:147029)与标量[内积](@entry_id:158127) $\mathbf{a} \cdot \mathbf{b} = a_i b_i$ 有本质区别，前者是[二阶张量](@entry_id:199780)，后者是标量。[@problem_id:2644994]

#### 乘法法则

类似于普通微积分，梯度和[散度算子](@entry_id:265975)也遵循一定的乘法法则。
- 标量场 $\phi$ 和矢量场 $\mathbf{v}$ 乘积的梯度：
  $$
  \nabla(\phi\mathbf{v}) = \mathbf{v} \otimes \nabla\phi + \phi \nabla\mathbf{v}
  $$
  这个恒等式可以通过分量形式 $(\nabla(\phi\mathbf{v}))_{ij} = \partial_j(\phi v_i) = (\partial_j\phi)v_i + \phi(\partial_j v_i)$ 得到验证。[@problem_id:2644961]

- 标量场 $\phi$ 乘以单位张量 $\mathbf{I}$ 的散度：
  $$
  \nabla \cdot (\phi\mathbf{I}) = \nabla\phi
  $$
  这可以看作静水压力情况的推广。[@problem_id:2644961]

- 两个矢量场外积的散度：
  $$
  \nabla \cdot (\mathbf{v} \otimes \mathbf{w}) = (\nabla \mathbf{v})\mathbf{w} + \mathbf{v}(\nabla \cdot \mathbf{w})
  $$
  这个法则的结构类似于函数[乘积的导数](@entry_id:158393)。[@problem_id:2644961]

#### [双点积](@entry_id:748648)与[应力功率](@entry_id:182907)

两个二阶张量 $\mathbf{A}$ 和 $\mathbf{B}$ 的**[双点积](@entry_id:748648)(double-dot product)**，也称冒号积，定义为它们分量乘积的总和：
$$
\mathbf{A}:\mathbf{B} = A_{ij}B_{ij}
$$
这个运算的结果是一个标量。[双点积](@entry_id:748648)与迹运算有关：$\mathbf{A}:\mathbf{B} = \mathrm{tr}(\mathbf{A}^T \mathbf{B})$。[@problem_id:2644954]

在连续介质力学中，单位体积的[内力](@entry_id:167605)所做的功率，即**[应力功率](@entry_id:182907)(stress power)**，由[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 和[速度梯度张量](@entry_id:270928) $\mathbf{L}=\nabla\mathbf{v}$ 的[双点积](@entry_id:748648)给出：
$$
P = \boldsymbol{\sigma}:\mathbf{L} = \sigma_{ij} \frac{\partial v_i}{\partial x_j}
$$
由于柯西应力张量 $\boldsymbol{\sigma}$ 是对称的，而 $\mathbf{L}$ 可以分解为对称的 $\mathbf{D}$ 和反对称的 $\mathbf{W}$，我们有 $\boldsymbol{\sigma}:\mathbf{L} = \boldsymbol{\sigma}:(\mathbf{D}+\mathbf{W}) = \boldsymbol{\sigma}:\mathbf{D} + \boldsymbol{\sigma}:\mathbf{W}$。[对称张量与反对称张量](@entry_id:194720)的[双点积](@entry_id:748648)恒为零，所以 $\boldsymbol{\sigma}:\mathbf{W}=0$。因此，[应力功率](@entry_id:182907)也可以写作：
$$
P = \boldsymbol{\sigma}:\mathbf{D}
$$
这表明，只有引起形变的部分（[形变率张量](@entry_id:184787) $\mathbf{D}$）才做功，刚性转动部分（[自旋张量](@entry_id:187346) $\mathbf{W}$）不做功。[@problem_id:2644954]

### 数学严谨性与高等论题

我们以上的讨论主要基于场是“足够光滑”的假设。现在我们来探讨这个假设的精确含义，并介绍一些更深入的概念。

#### [正则性条件](@entry_id:166962)

为了使一个矢量场或张量场的梯度或散度在经典意义下（即作为处处定义的[连续函数](@entry_id:137361)）存在，场本身必须是**连续可微的(continuously differentiable)**，即属于 $C^1$ 类。如果场仅仅是连续的（$C^0$），我们不能保证其导数处处存在（例如魏尔斯特拉斯函数）。同样，现代数学中更弱的条件，如属于[索博列夫空间](@entry_id:141995) $H^1$（函数及其[弱导数](@entry_id:189356)均平方可積），也不足以保证其经典导数是连续的。因此，在经典连续介质理论中，$C^1$ 正则性是进行[微分](@entry_id:158718)运算的基本要求。[@problem_id:2644987]

#### 相容性与[位错](@entry_id:157482)

我们已经知道，对于一个二次连续可微（$C^2$）的单值位移场 $\mathbf{u}$，其[梯度的旋度](@entry_id:274168)恒为零，即 $\nabla \times (\nabla \mathbf{u}) = \mathbf{0}$。这个条件被称为**相容性条件(compatibility condition)**，它保证了形变场可以由一个连续的、单值的位移场导出。

然而，在晶体材料中，存在一种称为**[位错](@entry_id:157482)(dislocation)**的线缺陷。在[位错](@entry_id:157482)线附近，不存在一个全局定义的单值位移场。例如，一个沿 $z$ 轴的[螺旋位错](@entry_id:182908)，其[位移场](@entry_id:141476)可以表示为 $\mathbf{u} = (0, 0, \frac{b}{2\pi}\arctan(\frac{y}{x}))$。这里的反正切函数是多值的。如果我们计算这个非单值场的[梯度的旋度](@entry_id:274168)，我们会发现它不为零。

令**弹性畸变张量(elastic distortion tensor)** $\boldsymbol{\beta} = \nabla \mathbf{u}$。对于上述[螺旋位错](@entry_id:182908)，其非零分量为 $\beta_{zx} = -\frac{b}{2\pi} \frac{y}{x^2+y^2}$ 和 $\beta_{zy} = \frac{b}{2\pi} \frac{x}{x^2+y^2}$。现在我们计算**[奈氏位错密度张量](@entry_id:186646)(Nye dislocation density tensor)** $\boldsymbol{\alpha} = \nabla \times \boldsymbol{\beta}$，其分量为 $\alpha_{im} = \epsilon_{mjk} \partial_j \beta_{ik}$。经过计算，我们发现在[分布](@entry_id:182848)意义下，其唯一的非零分量是：
$$
\alpha_{zz} = \partial_x \beta_{zy} - \partial_y \beta_{zx} = b\,\delta(x)\delta(y)
$$
其中 $\delta(\cdot)$ 是狄拉克-δ[分布](@entry_id:182848)。这个结果的物理意义是：在 $z$ 轴上存在一个[线密度](@entry_id:158735)为 $b$ 的[螺旋位错](@entry_id:182908)。$\boldsymbol{\alpha}$ 的非零性量化了场的“不相容性”，并直接与“[几何必需位错](@entry_id:187571)”的密度联系起来。这个例子深刻地展示了[梯度算子](@entry_id:275922)在描述材料微结构缺陷中的强大威力。有趣的是，尽管位移场存在[奇点](@entry_id:137764)，其产生的应[力场](@entry_id:147325) $\boldsymbol{\sigma}$ 的散度处处为零（$\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$），表明该静态缺陷场在没有体力的情况下是自平衡的。[@problem_id:2644969]

#### 推广至[曲线坐标系](@entry_id:172561)

本章中推导的分量表达式都基于[笛卡尔坐标系](@entry_id:169789)，其[基矢](@entry_id:199546)量是处处恒定的。当使用[曲线坐标系](@entry_id:172561)（如[圆柱坐标](@entry_id:271645)或球坐标）时，[基矢](@entry_id:199546)量本身也随空间位置变化。求导时必须同时考虑场分量和[基矢](@entry_id:199546)量的变化。这导致了**[协变导数](@entry_id:152476)(covariant derivative)**的概念。

例如，一个[逆变](@entry_id:192290)矢量 $v^i$ 的协变导数（即梯度张量的分量）为：
$$
v^i{}_{;j} = \frac{\partial v^i}{\partial \xi^j} + \Gamma^i_{kj} v^k
$$
一个[协变矢量](@entry_id:263917) $v_i$ 的协变导数为：
$$
v_{i;j} = \frac{\partial v_i}{\partial \xi^j} - \Gamma^k_{ij} v_k
$$
这里的 $\Gamma^k_{ij}$ 是**克氏符号(Christoffel symbols)**，它们描述了[基矢](@entry_id:199546)量的空间变化率，并依赖于度量张量 $g_{ij}$。类似地，一个二阶[逆变张量](@entry_id:636697) $T^{ij}$ 的散度（协变导数后缩并）为：
$$
T^{ij}{}_{;j} = \frac{\partial T^{ij}}{\partial \xi^j} + \Gamma^i_{kj} T^{kj} + \Gamma^j_{kj} T^{ik}
$$
这个表达式可以通过一个更紧凑的公式表示：
$$
T^{ij}{}_{;j} = \frac{1}{\sqrt{g}} \frac{\partial}{\partial \xi^j}(\sqrt{g} T^{ij}) + \Gamma^i_{kj} T^{kj}
$$
其中 $g$ 是度量张量 $g_{ij}$ 的[行列式](@entry_id:142978)。这些公式确保了梯度和散度等物理运算在任意[坐标变换](@entry_id:172727)下保持其张量性质，是广义相对论和现代连续介质力学不可或缺的工具。[@problem_id:2644948]