## 引言
标量耗散率，通常用符号 $\chi$ 表示，是理解和建模[湍流反应流](@entry_id:1133520)的核心物理量之一。它精确地量化了分子扩散作用下，标量（如温度或物质浓度）梯度被抹平的速率。在燃烧、[环境科学](@entry_id:187998)和化学工程等领域，混合过程往往是控制整体速率的关键步骤。然而，[湍流](@entry_id:151300)的混沌特性与分子层面的[微观混合](@entry_id:751971)之间存在巨大的尺度鸿沟，如何在这两者之间建立桥梁，是现代流[体力](@entry_id:174230)学和[反应流](@entry_id:190741)理论面临的核心难题。标量耗散率正是填补这一知识空白的关键概念，它为我们提供了一个量化局部混合强度的工具，从而能够将宏观的[湍流统计](@entry_id:200093)量与微观的[化学反应动力学](@entry_id:274455)联系起来。

本文将系统性地深入探讨[标量耗散率](@entry_id:754534)的建模理论与应用。在“原理与机制”一章中，我们将从第一性原理出发，推导标量耗散率的定义及其[输运方程](@entry_id:174281)，揭示流场应变如何影响标量梯度的演化，并探讨其在理想[湍流](@entry_id:151300)中的统计行为。接下来，在“应用与交叉学科联系”一章中，我们将展示标量耗散率模型如何在实际工程问题中发挥作用，包括其在雷诺平均（RANS）和[大涡模拟（LES）](@entry_id:273295)中的封闭方法，以及在火焰面模型中预测火焰熄火和壁面淬熄等关键现象的应用。最后，“动手实践”部分将提供具体的计算练习，帮助读者将理论知识应用于解决实际问题，加深对核心概念的理解。通过这三个章节的学习，读者将建立起对标量耗散率从基础理论到前沿应用的全面认识。

## 原理与机制

在本章中，我们将深入探讨标量耗散率的物理原理和数学描述。[标量耗散率](@entry_id:754534)是[湍流混合](@entry_id:202591)与[燃烧建模](@entry_id:201851)中的核心概念，它量化了[分子扩散](@entry_id:154595)抹平标量（如温度或物质浓度）梯度的速率。我们将从其基本定义出发，推导其[输运方程](@entry_id:174281)，并探讨其在[湍流](@entry_id:151300)和反应流中的关键作用。

### 标量耗散率的定义：分子混合的度量

为了理解标量耗散率的起源和物理意义，我们首先考察一个通用无源标量场的方差输运。无源标量是指在流体中被输运，但自身不发生化学反应的量。

#### 从[标量方差](@entry_id:1131255)输运推导

考虑一个由不可压缩流场 $\boldsymbol{u}(\boldsymbol{x},t)$ 输运的无源[标量场](@entry_id:151443) $\phi(\boldsymbol{x},t)$，其分子扩散系数 $D$ 为常数。该标量的输运遵循标准的[对流-扩散方程](@entry_id:1123699)：
$$
\frac{\partial \phi}{\partial t} + \boldsymbol{u} \cdot \nabla \phi = D \nabla^2 \phi
$$
其中，左侧两项分别代表瞬时变化和[对流输运](@entry_id:149512)，右侧项代表[分子扩散](@entry_id:154595)。

为了理解标量场的波动是如何随时间演化的，我们考察 **[标量方差](@entry_id:1131255)** $\phi^2$ 的输运。为方便起见，我们推导 $\frac{\phi^2}{2}$ 的[输运方程](@entry_id:174281)。将上述[标量输运方程](@entry_id:1131253)乘以 $\phi$：
$$
\phi \frac{\partial \phi}{\partial t} + \phi (\boldsymbol{u} \cdot \nabla \phi) = \phi D \nabla^2 \phi
$$
利用[链式法则](@entry_id:190743)，左侧可以重写为：
$$
\frac{\partial}{\partial t}\left(\frac{\phi^2}{2}\right) + \boldsymbol{u} \cdot \nabla\left(\frac{\phi^2}{2}\right) = \phi D \nabla^2 \phi
$$
左侧正是 $\frac{\phi^2}{2}$ 的[物质导数](@entry_id:262900)。为了清晰地分离输运项和源/汇项，我们处理右侧的扩散项。利用矢量恒等式 $\nabla \cdot (s\boldsymbol{A}) = (\nabla s) \cdot \boldsymbol{A} + s(\nabla \cdot \boldsymbol{A})$，我们有：
$$
\nabla \cdot \left(\phi \nabla \phi\right) = |\nabla \phi|^2 + \phi \nabla^2 \phi
$$
因此，$\phi \nabla^2 \phi = \nabla \cdot (\phi \nabla \phi) - |\nabla \phi|^2$。由于 $D$ 是常数，$\phi D \nabla^2 \phi$ 可以写成：
$$
\phi D \nabla^2 \phi = \nabla \cdot (D \phi \nabla \phi) - D |\nabla \phi|^2 = \nabla \cdot \left(D \nabla\left(\frac{\phi^2}{2}\right)\right) - D |\nabla \phi|^2
$$
将此表达式代入 $\frac{\phi^2}{2}$ 的[输运方程](@entry_id:174281)，我们得到：
$$
\frac{\partial}{\partial t}\left(\frac{\phi^2}{2}\right) + \boldsymbol{u} \cdot \nabla\left(\frac{\phi^2}{2}\right) = \nabla \cdot \left(D \nabla\left(\frac{\phi^2}{2}\right)\right) - D |\nabla \phi|^2
$$
这个方程明确地表示了 $\frac{\phi^2}{2}$ 的守恒。左侧是[物质导数](@entry_id:262900)，右侧第一项是分子扩散通量，而最后一项 $- D |\nabla \phi|^2$ 是一个汇项。由于 $D > 0$ 且 $|\nabla \phi|^2 \ge 0$，该项总是小于等于零，代表了由于分子混合导致的 $\frac{\phi^2}{2}$ 的不可逆破坏。

在湍流理论中，我们通常关心的是[标量方差](@entry_id:1131255) $\phi^2$（对于[湍流](@entry_id:151300)脉动 $\phi'$，则是 $\phi'^2$）的耗散。$\phi^2$ 的[输运方程](@entry_id:174281)只是上述方程的两倍，因此其汇项为 $-2D|\nabla \phi|^2$。我们由此定义瞬时 **[标量耗散率](@entry_id:754534) (scalar dissipation rate)** $\chi_\phi$：
$$
\chi_\phi \equiv 2 D |\nabla \phi|^2
$$
这个定义是标量耗散率建[模的基](@entry_id:156416)石。它表示[分子扩散](@entry_id:154595)销毁[标量方差](@entry_id:1131255)的局部速率 。

#### 物理意义与单位

$\chi_\phi$ 的物理意义是[标量场](@entry_id:151443)不均匀性的衰减率。在高标量梯度区域，分子扩散作用显著，将标量场变得更加均匀，这个过程伴随着[标量方差](@entry_id:1131255)的“耗散”。$\chi_\phi$ 的量纲取决于 $\phi$ 的量纲。设 $[\phi]$ 为 $\phi$ 的单位，$D$ 的单位为 $\mathrm{m}^2\,\mathrm{s}^{-1}$，$\nabla\phi$ 的单位为 $[\phi]\,\mathrm{m}^{-1}$。因此：
$$
[\chi_\phi] = [\mathrm{m}^2\,\mathrm{s}^{-1}] \cdot ([\phi]\,\mathrm{m}^{-1})^2 = [\phi]^2\,\mathrm{s}^{-1}
$$
如果 $\phi$ 是一个无量纲的量，例如质量分数或归一化的混合分数，那么 $[\chi_\phi]$ 的单位就是 $\mathrm{s}^{-1}$。在这种情况下，$\chi_\phi$ 可以被理解为一个逆时间尺度，表征了在[分子尺](@entry_id:166706)度上混合发生的快慢。

值得注意的是，标量耗散率 $\chi_\phi$ 与 **湍[动能[耗](@entry_id:751026)散率](@entry_id:748577) (turbulent kinetic energy dissipation rate)** $\varepsilon$ 是两个截然不同的物理量。$\varepsilon$ 来源于牛顿流体的[粘性应力](@entry_id:261328)做功，其标准形式为：
$$
\varepsilon = 2\nu S_{ij} S_{ij}
$$
其中 $\nu$ 是[运动粘度](@entry_id:275614)，$S_{ij} = \frac{1}{2} (\frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i})$ 是应变率张量。$\varepsilon$ 的物理意义是单位质量的流体动能由于粘性摩擦不可逆地转化为内能（热量）的速率。其单位是 $\mathrm{m}^2\,\mathrm{s}^{-3}$ (能量/质量/时间)。

总结来说，$\chi_\phi$ 描述的是标量场不均匀性的衰减，由分子扩散系数 $D$ 介导；而 $\varepsilon$ 描述的是动能的衰减，由运动粘度 $\nu$ 介导。两者在物理过程和量纲上都有本质区别 。

### [标量耗散率](@entry_id:754534)的输运

[标量耗散率](@entry_id:754534) $\chi_\phi$ 本身也是一个随空间和时间变化的场量。理解其自身的输运机制对于[湍流混合](@entry_id:202591)的高级建模至关重要。$\chi_\phi$ 的演化受到流场对流、应变和分子扩散的共同影响。

#### $\chi_\phi$ [输运方程](@entry_id:174281)的推导

我们可以推导 $\chi_\phi$ 的精确[输运方程](@entry_id:174281)。为简化，我们考虑不可压缩流和常数扩散系数 $D$ 的情况。推导过程从标量梯度 $\nabla\phi$ 的[输运方程](@entry_id:174281)开始。对[标量输运方程](@entry_id:1131253)取梯度，我们得到 $\nabla\phi$ 的[物质导数方程](@entry_id:266576)：
$$
\frac{D(\nabla\phi)}{Dt} = -(\nabla\boldsymbol{u})^{\mathrm{T}}\cdot\nabla\phi + D \nabla(\nabla^2\phi)
$$
其中，$\nabla\boldsymbol{u}$ 是[速度梯度张量](@entry_id:270928)。从这个方程出发，可以进一步推导出 $|\nabla\phi|^2$ 的[输运方程](@entry_id:174281)，再乘以 $2D$ 就得到 $\chi_\phi$ 的[输运方程](@entry_id:174281)。经过一系列基于矢量恒等式的严谨推导 ，最终得到的 $\chi_\phi$ 守恒形式的[输运方程](@entry_id:174281)为：
$$
\underbrace{\partial_t\chi_\phi + \nabla\cdot(\mathbf{u}\chi_\phi)}_{\text{对流}} = \underbrace{-4D(\nabla\phi)\cdot(\mathbf{S}\cdot\nabla\phi)}_{\text{应变产生/破坏}} \underbrace{- 4D^2(\nabla^2\phi)^2}_{\text{扩散破坏}} + \underbrace{\nabla\cdot(4D^2(\nabla^2\phi)\nabla\phi)}_{\text{扩散通量}}
$$
这个方程揭示了 $\chi_\phi$ 演化的几个关键机制：
- **对流项**: $\partial_t\chi_\phi + \nabla\cdot(\mathbf{u}\chi_\phi)$ 表示 $\chi_\phi$ 场被[流体速度](@entry_id:267320) $\boldsymbol{u}$ 所输运。
- **应变产生/破坏项**: $-4D(\nabla\phi)\cdot(\mathbf{S}\cdot\nabla\phi)$ 是最重要的项之一，描述了流场应变率张量 $\mathbf{S}$ 与标量梯度 $\nabla\phi$ 相互作用对 $\chi_\phi$ 的影响。
- **扩散破坏项**: $-4D^2(\nabla^2\phi)^2$ 是一个严格的汇项，代表了分子扩散自身对标量梯度方差的平滑作用，从而破坏 $\chi_\phi$。
- **[扩散通量](@entry_id:748422)项**: $\nabla\cdot(4D^2(\nabla^2\phi)\nabla\phi)$ 代表了由标量场曲率驱动的 $\chi_\phi$ 的分子扩散。

#### 流场应变对标量梯度的拉伸

应变产生项 $-4D(\nabla\phi)\cdot(\mathbf{S}\cdot\nabla\phi)$ 尤为重要，因为它联系了流场运动与标量混合。值得注意的是，[速度梯度张量](@entry_id:270928) $\nabla\boldsymbol{u}$ 可以分解为其对称部分（[应变率张量](@entry_id:266108) $\mathbf{S}$）和反对称部分（旋转率张量）。只有对称的应变部分能够改变标量梯度的大小 $|\nabla\phi|^2$，而旋转部分只会改变其方向 。

该项的符号取决于 $\nabla\phi$ 与[应变率张量](@entry_id:266108) $\mathbf{S}$ 的[主轴](@entry_id:172691)方向之间的相对对齐。
- 如果标量梯度 $\nabla\phi$ 的方向与 $\mathbf{S}$ 的拉伸主轴（正特征值对应的[特征向量](@entry_id:151813)方向）对齐，那么二次型 $(\nabla\phi)\cdot(\mathbf{S}\cdot\nabla\phi)$ 为正，导致产生项为负，即 $\chi_\phi$ 减小。这似乎与直觉相反，但它描述的是梯度方向被拉伸，梯度矢量被“稀释”的过程。
- 如果 $\nabla\phi$ 的方向与 $\mathbf{S}$ 的压缩[主轴](@entry_id:172691)（负特征值对应的[特征向量](@entry_id:151813)方向）对齐，二次型为负，导致产生项为正，即 $\chi_\phi$ 增大。这是因为流体压缩使得等标量面更加紧密，梯度增大。

例如，在一个[局部线性](@entry_id:266981)标量场（$\nabla^2\phi=0$）中，$\chi_\phi$ 的[物质导数](@entry_id:262900)完全由应变项决定：$D_t \chi_{\phi} = -4D (\nabla \phi) \cdot (\mathbf{S} \cdot \nabla \phi)$。通过计算在特定应变场和标量梯度下的这个项，我们可以精确量化流场应变对标量混合速率的瞬时影响 。

### [湍流](@entry_id:151300)中的标量耗散率：平均与建模

在[湍流](@entry_id:151300)中，所有场量都表现出随机波动。因此，我们关心的是[标量耗散率](@entry_id:754534)的统计平均行为，以及如何对其进行建模。

#### [标量方差](@entry_id:1131255)收支平衡

在最简单的[湍流](@entry_id:151300)情况——无平均梯度、统计均匀的[各向同性湍流](@entry_id:199323)中，对标量脉动 $\phi'=\phi-\langle\phi\rangle$ 的方差 $\langle\phi'^2\rangle$ 的[输运方程](@entry_id:174281)进行雷诺平均，所有输运项（对流和扩散）由于均匀性假设而消失。方程简化为一个简单的衰减关系 ：
$$
\frac{\mathrm{d}}{\mathrm{d}t}\langle \phi'^2 \rangle = - \langle \chi_\phi \rangle
$$
其中 $\langle\chi_\phi\rangle = \langle 2D|\nabla\phi'|^2 \rangle$ 是平均标量耗散率。这个简洁优美的结果表明，在这种理想[湍流](@entry_id:151300)中，[标量方差](@entry_id:1131255)的衰减速率完全由平均[标量耗散率](@entry_id:754534)决定。

在更现实的情况下，例如存在一个恒定的平均标量梯度 $\mathbf{G} = \nabla\langle\phi\rangle$ 的均匀剪切流中，[标量方差](@entry_id:1131255)的产生和耗散会达到一个统计[稳态](@entry_id:139253)。在这种情况下，[标量方差](@entry_id:1131255)的产生率（由[湍流](@entry_id:151300)脉动速度与平均梯度相互作用产生）必须与[耗散率](@entry_id:748577)相平衡。这个平衡关系可以精确地表示为 ：
$$
\underbrace{-\langle u_j' \phi' \rangle G_j}_{\text{产生}} = \underbrace{D \langle |\nabla \phi'|^2 \rangle}_{\text{耗散}}
$$
其中 $\langle u_j' \phi' \rangle$ 是[湍流标量通量](@entry_id:1133523)。这个关系非常重要，因为它直接将宏观量（湍流通量和平均梯度）与[微观混合](@entry_id:751971)过程（[标量耗散](@entry_id:1131248)）联系起来。将耗散项写成 $\frac{1}{2}\langle\chi_\phi\rangle$，我们得到一个用于计算平均[标量耗散率](@entry_id:754534)的精确关系：
$$
\langle \chi_\phi \rangle = -2 \langle u_j' \phi' \rangle G_j
$$
如果我们采用梯度扩散假设来模拟湍流通量，即 $\langle u_j' \phi' \rangle = -K_t G_j$（其中 $K_t$ 是[湍流](@entry_id:151300)涡扩散系数），那么平均[标量耗散率](@entry_id:754534)就可以被估算为 $\langle \chi_\phi \rangle = 2 K_t |\mathbf{G}|^2$ 。

#### [条件标量耗散率](@entry_id:1122853)与PDF方法

在许多先进的[湍流燃烧模型](@entry_id:1133504)中，例如概率密度函数（PDF）方法，我们需要知道在给定标量 $\phi$ 取某个特定值 $\psi$ 的条件下，[标量耗散率](@entry_id:754534)的[期望值](@entry_id:150961)是多少。这个量被称为 **[条件标量耗散率](@entry_id:1122853) (conditional scalar dissipation rate)**，记为 $\langle \chi_\phi \mid \phi = \psi \rangle$。

它与无条件平均值 $\langle \chi_\phi \rangle$ 通过[全期望定律](@entry_id:265946)联系在一起，即对所有可能的标量值进行加权平均：
$$
\langle \chi_\phi \rangle = \int_{-\infty}^{\infty} \langle \chi_\phi \mid \phi = \psi \rangle \, p_\phi(\psi) \, \mathrm{d}\psi
$$
其中 $p_\phi(\psi)$ 是标量 $\phi$ 的[概率密度函数](@entry_id:140610)。[条件标量耗散率](@entry_id:1122853)是描述湍流混合与化学反应相互作用的核心物理量，因为它量化了在某个特定组分（由 $\psi$ 表示）下混合发生的速率 [@problem_id:4042-000]。

### 在[非预混燃烧](@entry_id:1128819)中的应用：[小火焰模型](@entry_id:749445)

标量耗散率在[非预混燃烧](@entry_id:1128819)的 **[小火焰模型](@entry_id:749445) (flamelet model)** 中扮演着至关重要的角色。

#### 混合分数与小火焰假设

在[非预混燃烧](@entry_id:1128819)中，燃料和氧化剂最初是分离的，燃烧发生在它们混合的区域。我们可以定义一个[守恒标量](@entry_id:1122921)，称为 **混合分数 (mixture fraction)** $Z$，它在纯燃料流中为1，在纯氧化剂流中为0。在扩散系数相等（Lewis number为1）的假设下，$Z$ 的[输运方程](@entry_id:174281)没有化学反应源项，行为与无源标量完全一样 。

**小火焰假设 (flamelet regime)** 认为化学反应的时间尺度 $\tau_{\text{chem}}$ 远小于流场中最小的混合时间尺度 $\tau_{\text{mix}}$（即 Damköhler number $Da = \tau_{\text{mix}}/\tau_{\text{chem}} \gg 1$），并且远小于[湍流](@entry_id:151300)的最小时间尺度 $\tau_K$（即 Karlovitz number $Ka = \tau_{\text{chem}}/\tau_K \ll 1$）。在这种情况下，火焰可以被看作是一系列嵌入在[湍流](@entry_id:151300)场中的、结构近似一维的薄层，即“小火焰” 。这个假设极大地简化了问题：所有的反应标量（如物种质量分数 $Y_k$ 和温度 $T$）不再是三维空间和时间的独立变量，而是仅仅是混合分数 $Z$ 的函数，即 $\phi = \phi(Z)$。

#### [稳态](@entry_id:139253)[小火焰方程](@entry_id:1125053)

通过将物种[输运方程](@entry_id:174281)从物理空间 $(x, y, z)$ 变换到混合分数空间 $(Z)$，我们可以推导出[稳态](@entry_id:139253)[小火焰方程](@entry_id:1125053)。经过严谨的推导，它消除了对流项，最终形式为 ：
$$
\frac{\rho \chi_Z}{2} \frac{d^2\phi}{dZ^2} + \dot{\omega}_\phi = 0
$$
其中，$\rho$ 是密度，$\dot{\omega}_\phi$ 是标量 $\phi$ 的化学反应源项，而 $\chi_Z = 2D|\nabla Z|^2$ 是混合分数的标量耗散率。这个方程的优美之处在于，复杂的[湍流](@entry_id:151300)输运效应被完全封装在了单一参数 $\chi_Z$ 中。左侧第一项代表了标量 $\phi$ 在组分空间（Z空间）中的“扩散”，它与化学反应源项 $\dot{\omega}_\phi$ [相平衡](@entry_id:136822)。

#### [化学计量](@entry_id:137450)标量耗散率与火焰熄火

$\chi_Z$ 的值不是常数，它在流场中变化，反映了局部混合的强度。对于[火焰结构](@entry_id:1125069)而言，最重要的位置是[化学计量](@entry_id:137450)面，即燃料和氧化剂恰好成化学计量比的地方，该处用 $Z=Z_{\text{st}}$ 表示。因此，在化学计量面上的标量耗散率，特别是其条件平均值 $\chi_{\text{st}} \equiv \langle \chi_Z \mid Z = Z_{\text{st}} \rangle$，成为了控制[火焰行为](@entry_id:182450)的关键参数 。

$\chi_{\text{st}}$ 的物理意义是 **火焰所在处的混合速率**。它决定了反应物被输送到反应区的速率，也决定了热量从反应区散失的速率。
- 当 $\chi_{\text{st}}$ 较小时，混合较慢，化学反应有足够的时间完成，火焰处于稳定燃烧状态。
- 当 $\chi_{\text{st}}$ 增大时（例如在强剪切或高[应变率](@entry_id:154778)区域），混合加剧。反应物在反应区停留的时间变短，热量损失也更快。
- 当 $\chi_{\text{st}}$ 超过一个由化学动力学决定的临界值 $\chi_{\text{q}}$（熄火[标量耗散率](@entry_id:754534)）时，[化学反应速率](@entry_id:147315)将跟不上混合速率，导致火焰局部 **熄火 (extinction)** 。因此，$\chi_{\text{st}}$ 是预测非预混火焰熄火的核心参数。

### 高级考虑与模型局限性

虽然标量耗散率模型功能强大，但在应用于实际复杂流动时，仍需考虑一些重要因素。

#### 可变密度的影响

燃烧过程中的巨大热释放导致密度 $\rho$ 发生剧烈变化。在这种[可变密度流](@entry_id:756427)中：
1.  **守恒性**: 混合分数 $Z$ 的[输运方程](@entry_id:174281)，如果从守恒形式出发并利用[连续性方程](@entry_id:195013)，其[非守恒形式](@entry_id:1128837)中 **不会** 出现显式的[速度散度](@entry_id:264117)（膨胀）源项。可变密度的影响是通过改变速度场和密度本身来间接体现的 。
2.  **$\chi_Z$ 定义**: [标量耗散率](@entry_id:754534)的瞬时、逐点定义 $\chi_Z = 2D|\nabla Z|^2$ 保持不变。它是一个纯粹的运动学量，描述[梯度场](@entry_id:264143)的几何特性。
3.  **平均方法**: 在[可变密度流](@entry_id:756427)中，为了使平均后的[输运方程](@entry_id:174281)形式最简洁，标准做法是采用 **[Favre平均](@entry_id:198824) (密度加权平均)**。因此，所有相关的统计量，包括[条件标量耗散率](@entry_id:1122853)，都应该使用Favre条件平均进行定义和建模，以确保与整个建模框架的[自洽性](@entry_id:160889) 。

#### 差异扩散效应

上述理论大多基于一个重要假设：所有物种的分子扩散系数相等（即 Lewis number, $Le_i = 1$）。在现实中，不同物种的扩散速率可能差异巨大（例如，氢气的扩散远快于重碳氢化合物）。这种 **[差异扩散](@entry_id:195870) (differential diffusion)** 效应会破坏混合分数的守恒性。

当我们从具有不同扩散系数 $D_i$ 的物种[输运方程](@entry_id:174281)出发推导 $Z$ 的[输运方程](@entry_id:174281)时，其[扩散通量](@entry_id:748422) $\boldsymbol{j}_Z$ 不再能简化为 Fickian 形式 ($- \rho D_{\text{ref}} \nabla Z$)。其精确形式为 $\boldsymbol{j}_Z = -\rho \sum_{i=1}^{N} b_i D_i \nabla Y_i$。这导致[标量耗散率](@entry_id:754534)的“真实值” $\chi_{Z,\text{true}} = - \frac{2}{\rho}\boldsymbol{j}_Z \cdot \nabla Z$ 与基于参考扩散系数 $D_{\text{ref}}$ 的模型值 $\chi_{Z,\text{mod}} = 2 D_{\text{ref}} |\nabla Z|^2$ 之间产生一个误差 $\Delta \chi_Z$ 。这个误差可以精确表示为：
$$
\Delta \chi_Z = -2 \left( \sum_{i=1}^{N} b_i (D_i - D_{\text{ref}}) \nabla Y_i \right) \cdot \left( \sum_{j=1}^{N} b_j \nabla Y_j \right)
$$
此误差的存在说明，在[差异扩散](@entry_id:195870)效应显著的情况下，简单的[小火焰模型](@entry_id:749445)可能不再准确，需要更复杂的模型来描述燃烧过程。