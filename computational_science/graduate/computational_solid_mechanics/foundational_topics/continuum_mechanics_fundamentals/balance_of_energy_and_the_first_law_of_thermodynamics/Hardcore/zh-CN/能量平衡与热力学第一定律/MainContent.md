## 引言
[能量守恒](@entry_id:140514)，即热力学第一定律，是物理学中最基本的普适原理之一。在[计算固体力学](@entry_id:169583)领域，它不仅是一个抽象的[守恒定律](@entry_id:269268)，更是理解和模拟材料与结构在复杂载荷下行为的基石，精确地描述了机械功、热量与内能之间的转换关系。然而，将这一宏观定律转化为能够处理局部变形、温度演化和能量耗散的、适用于数值计算的控制方程，是工程师和研究人员面临的一大挑战。

本文旨在系统性地阐明这一转化过程及其广泛应用。读者将首先在“原理与机制”一章中深入学习[能量平衡](@entry_id:150831)的局部形式是如何从积分形式推导而来，以及[应力功率](@entry_id:182907)、热传导和耗散等关键机制的物理意义。随后，“应用与跨学科交叉”一章将展示这些原理如何被用来分析真实世界中的[热力耦合](@entry_id:183230)、断裂失效和[多物理场](@entry_id:164478)问题。最后，通过对“动手实践”的介绍，读者将了解到如何利用能量平衡这一强大工具来检验和验证[计算模拟](@entry_id:146373)的物理保真度。

## 原理与机制

本章旨在系统性地阐述可变形固体中[能量平衡](@entry_id:150831)与热力学第一定律的基本原理和关键机制。我们将从最普适的[守恒定律](@entry_id:269268)出发，推导出适用于[计算固体力学](@entry_id:169583)的局部控制方程，并深入探讨力学功、[热传导](@entry_id:147831)和能量耗散之间的相互关系。这些原理构成了[非线性](@entry_id:637147)[热力学耦合](@entry_id:170539)问题[有限元分析](@entry_id:138109)的理论基石。

### [热力学第一定律](@entry_id:146485)：积分形式与局部形式

[热力学第一定律](@entry_id:146485)是[能量守恒](@entry_id:140514)原理在[热力学系统](@entry_id:188734)中的体现。对于一个随流体运动的物质体（material body），其在当前构形下占据的空间域为 $\Omega(t)$，该定律的积分形式断言：系统总能量（内能与动能之和）的时间变化率，等于外界对系统所做的[机械功率](@entry_id:163535)与系统净吸热率之和。

总能量 $E_{total}$ 包括总内能 $E_{int} = \int_{\Omega(t)} \rho e \, \mathrm{d}v$ 和总动能 $K = \int_{\Omega(t)} \frac{1}{2} \rho \boldsymbol{v} \cdot \boldsymbol{v} \, \mathrm{d}v$，其中 $\rho$ 是当前密度，$e$ 是单位质量内能，$\boldsymbol{v}$ 是速度场。

外界对系统所做的[机械功率](@entry_id:163535) $P_{ext}$ 来自于作用在边界 $\partial\Omega(t)$ 上的面力功率和作用在体积 $\Omega(t)$ 内的[体力](@entry_id:174230)功率。面力由柯西应力张量 $\boldsymbol{\sigma}$ 和边界外[法线](@entry_id:167651) $\boldsymbol{n}$ 定义的循迹力 $\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$ 给出。[体力](@entry_id:174230)通常以单位质量的[体力](@entry_id:174230) $\boldsymbol{b}$ 表示。因此，
$$
P_{ext} = \int_{\partial\Omega(t)} \boldsymbol{t} \cdot \boldsymbol{v} \, \mathrm{d}a + \int_{\Omega(t)} \rho \boldsymbol{b} \cdot \boldsymbol{v} \, \mathrm{d}v
$$
其中 $\mathrm{d}a$ 和 $\mathrm{d}v$ 分别是当前构形下的面积和体积微元。

系统的净吸热率 $Q_{net}$ 包括通过边界传入的热量和体内的热源生成的热量。热量传递通过热流矢量 $\boldsymbol{q}$ 描述（约定 $\boldsymbol{q}$ 指向热量流出的方向），而热源则以单位质量的热源项 $r$ 表示。因此，
$$
Q_{net} = - \int_{\partial\Omega(t)} \boldsymbol{q} \cdot \boldsymbol{n} \, \mathrm{d}a + \int_{\Omega(t)} \rho r \, \mathrm{d}v
$$

综合以上各项，[热力学第一定律](@entry_id:146485)的积分形式为 ：
$$
\frac{\mathrm{d}}{\mathrm{d}t} \int_{\Omega(t)} \rho \left( e + \frac{1}{2} \boldsymbol{v} \cdot \boldsymbol{v} \right) \mathrm{d}v = \int_{\partial\Omega(t)} (\boldsymbol{\sigma}\boldsymbol{n}) \cdot \boldsymbol{v} \, \mathrm{d}a + \int_{\Omega(t)} \rho \boldsymbol{b} \cdot \boldsymbol{v} \, \mathrm{d}v - \int_{\partial\Omega(t)} \boldsymbol{q} \cdot \boldsymbol{n} \, \mathrm{d}a + \int_{\Omega(t)} \rho r \, \mathrm{d}v
$$
这个[全局平衡方程](@entry_id:272290)是所有后续推导的基础。然而，对于计算分析，我们更关心的是适用于域内任意一点的局部（[微分](@entry_id:158718)）形式。通过应用[雷诺输运定理](@entry_id:191217) (Reynolds transport theorem) 和散度定理 (divergence theorem)，可将上述[积分方程](@entry_id:138643)转化为总能量的[局部平衡](@entry_id:156295)方程：
$$
\rho \frac{\mathrm{D}}{\mathrm{D}t} \left( e + \frac{1}{2} \boldsymbol{v} \cdot \boldsymbol{v} \right) = \nabla \cdot (\boldsymbol{\sigma}^{\mathsf{T}}\boldsymbol{v}) + \rho \boldsymbol{b} \cdot \boldsymbol{v} - \nabla \cdot \boldsymbol{q} + \rho r
$$
其中 $\frac{\mathrm{D}}{\mathrm{D}t}(\cdot)$ 或 $\dot{(\cdot)}$ 表示[物质时间导数](@entry_id:190892)。

为了分离出内能的变化，我们需要考察动能的平衡。动能的平衡由[线性动量平衡](@entry_id:193575)定律（即柯西第一运动定律）决定，其局部形式为 $\rho \dot{\boldsymbol{v}} = \nabla \cdot \boldsymbol{\sigma} + \rho \boldsymbol{b}$。将此方程与[速度场](@entry_id:271461) $\boldsymbol{v}$做[点积](@entry_id:149019)，我们得到动能[平衡方程](@entry_id:172166)：
$$
\rho \dot{\boldsymbol{v}} \cdot \boldsymbol{v} = (\nabla \cdot \boldsymbol{\sigma} + \rho \boldsymbol{b}) \cdot \boldsymbol{v}
$$
注意到 $\rho \dot{\boldsymbol{v}} \cdot \boldsymbol{v} = \rho \frac{\mathrm{D}}{\mathrm{D}t}(\frac{1}{2}\boldsymbol{v} \cdot \boldsymbol{v})$。从总[能量平衡方程](@entry_id:191484)中减去动能[平衡方程](@entry_id:172166)，即可得到**内能的[局部平衡](@entry_id:156295)方程** ：
$$
\rho \dot{e} = \boldsymbol{\sigma} : \nabla \boldsymbol{v} - \nabla \cdot \boldsymbol{q} + \rho r
$$
这个方程是连续介质[热力学](@entry_id:141121) (continuum thermomechanics) 的核心方程之一。它表明，单位体积内能的增加率等于[应力功率](@entry_id:182907)密度（$\boldsymbol{\sigma} : \nabla \boldsymbol{v}$）、热流的汇聚（$-\nabla \cdot \boldsymbol{q}$）和内部热源（$\rho r$）之和。值得注意的是，[体力](@entry_id:174230)功率项 $\rho \boldsymbol{b} \cdot \boldsymbol{v}$ 在推导过程中被抵消了，因为它直接贡献给动能变化，而不直接改变内能 。

### [应力功率](@entry_id:182907)及其分解

[应力功率](@entry_id:182907)密度项 $\boldsymbol{\sigma} : \nabla \boldsymbol{v}$ 描述了内部应力做功的速率。为了理解其物理意义，我们将[速度梯度张量](@entry_id:270928) $\boldsymbol{L} = \nabla \boldsymbol{v}$ 分解为其对称[部分和](@entry_id:162077)反对称部分：
$$
\boldsymbol{L} = \boldsymbol{d} + \boldsymbol{W}
$$
其中 $\boldsymbol{d} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^{\mathsf{T}})$ 是**变形率张量 (rate-of-deformation tensor)**，代表了材料微元的变形速率；$\boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^{\mathsf{T}})$ 是**[自旋张量](@entry_id:187346) (spin tensor)**，代表了材料微元的[刚体转动](@entry_id:191086)速率。

因此，[应力功率](@entry_id:182907)可以写作：
$$
\boldsymbol{\sigma} : \boldsymbol{L} = \boldsymbol{\sigma} : (\boldsymbol{d} + \boldsymbol{W}) = \boldsymbol{\sigma} : \boldsymbol{d} + \boldsymbol{\sigma} : \boldsymbol{W}
$$
对于经典（非极性）连续介质，[角动量平衡](@entry_id:181848)要求柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 是对称的（$\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$）。一个[对称张量](@entry_id:148092)与一个[反对称张量](@entry_id:199349)的[双点积](@entry_id:748648)恒为零，即 $\boldsymbol{\sigma} : \boldsymbol{W} = 0$。因此，[应力功率](@entry_id:182907)密度简化为 ：
$$
p_{int} = \boldsymbol{\sigma} : \boldsymbol{d}
$$
这揭示了一个深刻的物理事实：只有材料的**变形**（由 $\boldsymbol{d}$ 描述）才会产生内能变化，而材料的**[刚体转动](@entry_id:191086)**（由 $\boldsymbol{W}$ 描述）不会。换言之，[自旋张量](@entry_id:187346) $\boldsymbol{W}$ 在能量上与柯西应力 $\boldsymbol{\sigma}$ 是不共轭的 。

这个原理引出了**功率定理 (theorem of power expended)** ，它将总的外部[机械功率](@entry_id:163535)进行了划分：
$$
\int_{\partial\Omega(t)}(\boldsymbol{\sigma}\boldsymbol{n})\cdot\boldsymbol{v}\,{\mathrm{d}}a+\int_{\Omega(t)}\rho\,\boldsymbol{b}\cdot\boldsymbol{v}\,{\mathrm{d}}v = \frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega(t)}\tfrac{1}{2}\rho\,\boldsymbol{v}\cdot\boldsymbol{v}\,{\mathrm{d}}v+\int_{\Omega(t)}\boldsymbol{\sigma}:\boldsymbol{d}\,{\mathrm{d}}v
$$
此定理表明，外部[机械功率](@entry_id:163535)一部分用于改变物体的宏观动能，另一部分则通过应力做功转化为内能或耗散掉。

### 能量共轭的[应力与应变率](@entry_id:263123)量度

在处理大变形问题时，仅使用柯西应力和变形率张量是不够的，因为它们都在不断变化的当前构形上定义。为了在固定的参考构形 $\Omega_0$ 上建立方程，我们需要引入相应的拉格朗日（Lagrangian）量度。

[能量守恒](@entry_id:140514)原理为我们提供了寻找正确应力-[应变率](@entry_id:154778)配对的途径。我们称一对张量 $(\boldsymbol{A}, \boldsymbol{B})$ 是**能量共轭**的，如果它们的[双点积](@entry_id:748648) $\boldsymbol{A}:\boldsymbol{B}$ 恰好等于单位体积的功率。

我们将单位当前体积的[应力功率](@entry_id:182907) $p_{int} = \boldsymbol{\sigma}:\boldsymbol{d}$ 转换到单位参考体积。考虑到体积变化关系 $\mathrm{d}v = J \mathrm{d}V$，其中 $J = \det(\boldsymbol{F})$ 是变形梯度 $\boldsymbol{F}$ 的[雅可比行列式](@entry_id:137120)，单位参考体积的[应力功率](@entry_id:182907)为 $P_{int} = J(\boldsymbol{\sigma}:\boldsymbol{d}) = J(\boldsymbol{\sigma}:\boldsymbol{L})$。通过一系列张量运算，可以证明以下[等价关系](@entry_id:138275)  ：
$$
P_{int} = J(\boldsymbol{\sigma}:\boldsymbol{d}) = \boldsymbol{P}:\dot{\boldsymbol{F}} = \boldsymbol{S}:\dot{\boldsymbol{E}} = \boldsymbol{\tau}:\boldsymbol{d}
$$
其中：
- $\boldsymbol{F} = \nabla_{\boldsymbol{X}}\boldsymbol{x}$ 是**变形梯度** (deformation gradient)。
- $\boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-\mathsf{T}}$ 是**第一Piola-Kirchhoff (PK1)应力张量** (first Piola-Kirchhoff stress)。它与变形梯度率 $\dot{\boldsymbol{F}}$ 能量共轭。
- $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} - \boldsymbol{I})$ 是**格林-拉格朗日 (Green-Lagrange) [应变张量](@entry_id:193332)** (Green-Lagrange strain)。
- $\boldsymbol{S} = \boldsymbol{F}^{-1}\boldsymbol{P} = J \boldsymbol{F}^{-1}\boldsymbol{\sigma}\boldsymbol{F}^{-\mathsf{T}}$ 是**第二Piola-Kirchhoff (PK2)应力张量** (second Piola-Kirchhoff stress)。它与[格林-拉格朗日应变](@entry_id:170427)率 $\dot{\boldsymbol{E}}$ 能量共轭。
- $\boldsymbol{\tau} = J\boldsymbol{\sigma}$ 是**[基尔霍夫应力](@entry_id:751039)张量** (Kirchhoff stress)。它与变形率张量 $\boldsymbol{d}$ 的乘积 $\boldsymbol{\tau}:\boldsymbol{d}$ 代表单位**参考**体积的功率，这在数值计算中非常有用。

这些共轭对应关系至关重要。例如，在有限元程序中，若使用 PK2 应力，则必须用[格林-拉格朗日应变](@entry_id:170427)率来计算[内力](@entry_id:167605)功。任何不匹配的组合都会违反[能量守恒](@entry_id:140514)。一个直接的推论是，对于任何[刚体运动](@entry_id:193355)，$\boldsymbol{d}=\boldsymbol{0}$ 和 $\dot{\boldsymbol{E}}=\boldsymbol{0}$，因此所有形式的[应力功率](@entry_id:182907)都必须为零 。

### 热方程：传导、热源与耗散

现在我们回到内能[平衡方程](@entry_id:172166)，并将其发展为描述温度演化的**热方程**。这需要引入具体的本构关系。

首先，我们将内能的变化与温度变化联系起来。对于许多固体，一个合理的近似是 $e \approx c T$，其中 $c$ 是比[热容](@entry_id:137594)。于是 $\rho\dot{e} \approx \rho c \dot{T}$。

其次，热流矢量 $\boldsymbol{q}$ 通常由**傅里葉热传导定律 (Fourier's law of heat conduction)** 描述：
$$
\boldsymbol{q} = -\boldsymbol{k} \nabla T
$$
其中 $\boldsymbol{k}$ 是热导率张量。负号表示热量从高温区流向低温区。代入内能方程，[热传导](@entry_id:147831)项变为 $\nabla \cdot (\boldsymbol{k} \nabla T)$ 。

最重要的联系在于[应力功率](@entry_id:182907)项。在[弹塑性](@entry_id:193198)或黏塑性材料中，总[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}$ 可以分解为弹性部分 $\dot{\boldsymbol{\varepsilon}}^e$ 和非弹性（塑性）部分 $\dot{\boldsymbol{\varepsilon}}^p$。[应力功率](@entry_id:182907)相应地分解为：
$$
\boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^e + \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p
$$
其中，弹性功率 $\boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^e$ 是可恢复的，它改变了储存在材料中的弹性应变能。而非弹性功率（或塑性功率）$\mathcal{D} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p$ 是不可逆的，它代表了由于[晶格缺陷](@entry_id:270099)运动、微裂纹等机制所耗散的能量。

这部分耗散的能量大部分会转化为热。**[泰勒-奎尼系数](@entry_id:202069) (Taylor-Quinney coefficient)** $\chi$（一个通常取值为 $0.85 \sim 0.95$ 的常数）描述了塑性功转化为热的比例  。因此，塑性变形产生了一个内在的体积热源，其密度为 $\chi \mathcal{D} = \chi \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p$。

综合以上各项，我们得到了耦合[热力学](@entry_id:141121)问题的温度[演化方程](@entry_id:268137)（[热方程](@entry_id:144435)）：
$$
\rho c \dot{T} = \underbrace{\nabla \cdot (\boldsymbol{k} \nabla T)}_{\text{热传导}} + \underbrace{\rho r}_{\text{外部热源}} + \underbrace{\chi (\boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p)}_{\text{塑性耗散热}}
$$
这个方程清晰地展示了温度场如何受到传导、外部加热和材料内部力学行为的共同影响。边界条件可以是指定的温度（[Dirichlet条件](@entry_id:137096)）、指定的热流（[Neumann条件](@entry_id:165471)）或[对流换热](@entry_id:151349)（[Robin条件](@entry_id:153384)）。

### 热力学势与第二定律

为了构建一个完整的[热力学](@entry_id:141121)框架，我们引入**亥姆霍兹自由能 (Helmholtz free energy)** $\Psi = U - TS$（单位参考体积）或 $\psi = e - Ts$（单位质量），其中 $S$ 或 $s$ 是熵，T 是绝对温度。自由能是一个[热力学势](@entry_id:140516) (thermodynamic potential)，其变化率可以通过[勒让德变换](@entry_id:146727)从第一定律导出 ：
$$
\dot{\Psi} = \dot{U} - \dot{T}S - T\dot{S}
$$
将第一定律的[拉格朗日形式](@entry_id:145697) $\dot{U} = \boldsymbol{P}:\dot{\boldsymbol{F}} - \mathrm{DIV}\,\boldsymbol{Q} + R$ 代入，得到：
$$
\dot{\Psi} = \boldsymbol{P}:\dot{\boldsymbol{F}} - \mathrm{DIV}\,\boldsymbol{Q} + R - S\dot{T} - T\dot{S}
$$
这个表达式虽然看起来更复杂，但它在建立本构关系时极其有用，因为它将状态变量（如应变和温度）与其[共轭变量](@entry_id:147843)（如应力和熵）分离开来。

热力学第二定律要求任何[孤立系统](@entry_id:159201)的熵永不减少。对于连续介质，其局部形式（克劳修斯-杜亨不等式, Clausius-Duhem inequality）要求内部熵产生率 $\xi$必须非负。熵产生率定义为 ：
$$
\rho T \xi = \rho(T\dot{s} - \dot{e}) + \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}} - \frac{1}{T}\boldsymbol{q} \cdot \nabla T \ge 0
$$
通过联立第一定律、自由能定义和第二定律，可以将总耗散（即单位体积的熵产生率乘以[绝对温度](@entry_id:144687) $\rho T \xi$）分解为两个来源。对于一个总应力可以分解为弹性部分 $\boldsymbol{\sigma}_e$ 和黏性（耗散）部分 $\boldsymbol{\sigma}_v$ 的应力，可以证明：
$$
\rho T \xi = \boldsymbol{\sigma}_{v}:\dot{\boldsymbol{\varepsilon}} - \frac{1}{T}\boldsymbol{q} \cdot \nabla T \ge 0
$$
这个结果清晰地表明，不[可逆性](@entry_id:143146)（熵增）有两个来源：一是**力学耗散**（由黏性应力做功），二是**热耗散**（热量流过有限的温差）。第二定律通常要求这两项贡献各自都必须是非负的。例如，结合[傅里叶热传导定律](@entry_id:138911) $\boldsymbol{q}=-\boldsymbol{k}\nabla T$，热耗散项变为 $\frac{1}{T}(\boldsymbol{k}\nabla T)\cdot \nabla T$，只要热导率张量 $\boldsymbol{k}$ 是正定的，该项就非负。

### 应用实例

让我们通过几个例子来具体说明这些原理的应用。

考虑一个尺寸为 $0.5\,\mathrm{m} \times 0.3\,\mathrm{m} \times 0.2\,\mathrm{m}$ 的矩形体，其内部应[力场](@entry_id:147325)、变形率场、热流场和体积热源均为已知函数。要计算该物体总内能的[瞬时变化率](@entry_id:141382) $\frac{\mathrm{d}E_{int}}{\mathrm{d}t}$，我们只需根据第一定律的积分形式计算三个部分的贡献：总[应力功率](@entry_id:182907)、通过边界的总净热流和总体积热源的总和。即 ：
$$
\frac{\mathrm{d}E_{int}}{\mathrm{d}t} = \int_{\Omega_t} \boldsymbol{\sigma} : \boldsymbol{d} \, \mathrm{d}v - \int_{\partial\Omega_t} \boldsymbol{q} \cdot \boldsymbol{n} \, \mathrm{d}a + \int_{\Omega_t} r \, \mathrm{d}v
$$
通过对给定的场函数进行积分，就可以得到一个确定的数值。例如，如果[应力功率](@entry_id:182907)密度为 $0.08 A x + 0.06 B y^2$，热流散度为 $2\alpha x + \beta$，体积热源为常数 $r_0$，则对这些项在给定体积上积分即可求解。

另一个例子是，一个立方体在均匀剪切应力 $\tau$ 和线性速度场 $\boldsymbol{v} = \beta x \boldsymbol{e}_y$ 的作用下变形。其[应力功率](@entry_id:182907)密度为 $\boldsymbol{\sigma}:\boldsymbol{d} = \tau\beta$。若同时存在一个二次温度场 $T = T_0 + ax^2$ 和均匀热源 $r$，根据傅里葉定律，热流散度为 $\nabla \cdot \boldsymbol{q} = -2ak$。因此，总内能的变化率密度为 $\tau\beta + 2ak + r$。将其乘以物体体积，即可得到总内能变化率 。

最后，考虑一个一维黏塑性材料点。其总[应变率](@entry_id:154778)为 $\dot{\varepsilon}$，应力为 $\sigma$，塑性[应变率](@entry_id:154778)为 $\dot{\varepsilon}_p$。在绝熱条件下，[应力功率](@entry_id:182907) $\sigma\dot{\varepsilon}$ 分解为儲存的自由能变化率 $\dot{\psi} = \sigma \dot{\varepsilon}_e$ 和[耗散功率](@entry_id:177328) $\mathcal{D} = \sigma \dot{\varepsilon}_p$。耗散的能量中有一部分 ($\chi \mathcal{D}$) 转化为热量，导致温度上升。因此，温度变化率可直接计算为 $\dot{T} = \frac{\chi \sigma \dot{\varepsilon}_p}{\rho c}$ 。这个简单的例子完美地连接了力学变形、能量耗散和热响应，是理解复杂[热力学耦合](@entry_id:170539)现象的起点。