## 引言
[弹性波](@entry_id:196203)是探究固体内部信息和传递能量的重要方式。从揭示地球深处奥秘的地震波，到检测工程材料微小缺陷的超声波，对[弹性波传播](@entry_id:201422)的研究具有深刻的理论意义和广泛的应用价值。然而，要精确描述和预测波在[复杂介质](@entry_id:164088)中的行为，需要一个坚实的[数学物理](@entry_id:265403)基础，这往往是初学者面临的主要挑战。本文旨在为读者构建一个关于固体[弹性波传播](@entry_id:201422)的系统性知识框架，弥合基础理论与前沿应用之间的鸿沟。

文章的结构旨在引导您逐步深入这一领域。在“原理与机制”一章中，我们将从[弹性动力学](@entry_id:175818)的基本控制方程出发，严格推导[P波](@entry_id:178440)和S波的存在与特性，并探讨[能量传播](@entry_id:202589)与界面行为，为您奠定坚实的理论基础。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些基础理论如何应用于[地球物理学](@entry_id:147342)、地震学和[材料科学](@entry_id:152226)等领域，解决从震源机制反演到[非线性](@entry_id:637147)超声检测等实际问题，揭示理论的强大生命力。最后，通过“动手实践”部分，您将有机会通过解决具体的计算与推导问题，将抽象的理论知识转化为解决实际问题的能力。通过这种从基础到应用的[结构化学](@entry_id:176683)习路径，您将能够全面掌握固体[弹性波传播](@entry_id:201422)的核心知识。

## 原理与机制

本章旨在深入探讨[弹性波](@entry_id:196203)在固体中传播的核心原理与物理机制。我们将从[弹性动力学](@entry_id:175818)的基本控制方程出发，系统推导在不同类型介质（包括各向同性与[各向异性介质](@entry_id:187796)）中波动现象的数学描述。内容将涵盖两种基本波型——[纵波](@entry_id:172335)（P波）与横波（S波）——的定义、传播特性及其物理差异。此外，我们还将建立[弹性波](@entry_id:196203)的[能量守恒](@entry_id:140514)定律，并讨论波在介质界面处的行为。本章的论述将为后续章节中更复杂的波动问题，如反射、透射、散射及[导波](@entry_id:269489)传播等，奠定坚实的理论基础。

### [弹性动力学](@entry_id:175818)控制方程

任何连续介质动力学问题的分析都建立在三个基本支柱之上：运动学关系、[动量守恒](@entry_id:149964)（或运动方程）以及材料的本构关系。对于[弹性波传播](@entry_id:201422)问题，这三者共同构成了描述位移场随时间和空间演化的完整数学框架。

#### [小应变近似](@entry_id:754971)

在[固体力学](@entry_id:164042)中，描述材料变形最精确的度量之一是[格林-拉格朗日应变张量](@entry_id:187745)（Green–Lagrange strain tensor）$\mathbf{E}$，其定义为：
$$ \mathbf{E} = \frac{1}{2}(\mathbf{F}^{\mathsf{T}}\mathbf{F} - \mathbf{I}) $$
其中 $\mathbf{F} = \mathbf{I} + \nabla \mathbf{u}$ 是变形梯度张量，$\mathbf{u}$ 是[位移矢量场](@entry_id:196067)，$\mathbf{I}$ 是单位张量。将 $\mathbf{F}$ 代入，可以得到应变与[位移梯度](@entry_id:165352)的非[线性关系](@entry_id:267880)：
$$ E_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i}) + \frac{1}{2}u_{k,i}u_{k,j} $$
此处 $u_{i,j}$ 代[表位](@entry_id:175897)移分量 $u_i$ 对坐标 $x_j$ 的偏导数。

对于大多数[弹性波](@entry_id:196203)问题，例如[地震波](@entry_id:164985)或[无损检测](@entry_id:273209)中的超声波，[质点](@entry_id:186768)的位移振幅远小于波长，这导致[位移梯度](@entry_id:165352)非常小。因此，我们可以进行线性化处理，这一过程被称为**[小应变近似](@entry_id:754971)**（small-strain approximation）。该近似的核心假设是[位移梯度张量](@entry_id:748571) $\nabla \mathbf{u}$ 的所有分量都远小于1，即 $|u_{i,j}| \ll 1$。在此条件下，上式中的二次项 $u_{k,i}u_{k,j}$ 是一个二阶小量，可以忽略不计。由此，我们得到了线性的**[无穷小应变张量](@entry_id:167211)**（infinitesimal strain tensor）$\boldsymbol{\varepsilon}$：
$$ \varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i}) $$
值得强调的是，条件 $|u_{i,j}| \ll 1$ 不仅意味着应变（[位移梯度](@entry_id:165352)的对称部分）很小，也意味着[刚体转动](@entry_id:191086)（[位移梯度](@entry_id:165352)的反对称部分）同样很小。对于一个振幅为 $|\mathbf{A}|$、波数为 $|\mathbf{k}|$ 的[平面波](@entry_id:189798)，[位移梯度](@entry_id:165352)的大小与乘积 $|\mathbf{k}||\mathbf{A}|$ 成正比。因此，[小应变近似](@entry_id:754971)的有效性要求 $|\mathbf{k}||\mathbf{A}| \ll 1$。这一条件澄清了一个常见的误解：仅仅位移振幅 $|\mathbf{A}|$ 很小是不够的；振[幅相](@entry_id:269870)对于波长 $\lambda = 2\pi/|\mathbf{k}|$ 必须很小才行 [@problem_id:2676954]。

#### 本构关系与[纳维-柯西方程](@entry_id:189211)

描述[材料力学](@entry_id:201885)行为的本构关系将[应力与应变](@entry_id:137374)联系起来。对于线弹性、[各向同性材料](@entry_id:170678)，该关系由[广义胡克定律](@entry_id:203555)（Hooke's Law）给出，其张量形式为：
$$ \sigma_{ij} = \lambda \delta_{ij} \varepsilon_{kk} + 2\mu \varepsilon_{ij} $$
其中 $\boldsymbol{\sigma}$ 是柯西[应力张量](@entry_id:148973)（Cauchy stress tensor），$\lambda$ 和 $\mu$ 是材料的**拉梅参数**（Lamé parameters），$\delta_{ij}$ 是克罗内克符号（Kronecker delta），$\varepsilon_{kk} = \nabla \cdot \mathbf{u}$ 是应变张量的迹，代表体积应变（dilatation）。参数 $\mu$ 也被称为剪切模量（shear modulus）。

最后，我们将[运动学](@entry_id:173318)关系和本构关系代入动量守恒定律的[微分形式](@entry_id:146747)，即[柯西运动方程](@entry_id:204126)（在无[体力](@entry_id:174230)情况下）：
$$ \rho \frac{\partial^2 u_i}{\partial t^2} = \frac{\partial \sigma_{ij}}{\partial x_j} $$
其中 $\rho$ 是材料密度。将应力表达式代入，并考虑到材料是均匀的（即 $\lambda$ 和 $\mu$ 是常数），经过一系列的[微分](@entry_id:158718)运算，可以得到一个完全用[位移场](@entry_id:141476) $\mathbf{u}$ 表达的控制方程 [@problem_id:2676930] [@problem_id:2676974]：
$$ \rho \frac{\partial^2 u_i}{\partial t^2} = (\lambda + \mu)\frac{\partial}{\partial x_i}\left(\frac{\partial u_k}{\partial x_k}\right) + \mu \frac{\partial^2 u_i}{\partial x_j \partial x_j} $$
上式即为著名的**纳维-柯西[弹性动力学](@entry_id:175818)方程**（Navier-Cauchy equation of elastodynamics）。用更简洁的矢量符号表示为：
$$ \rho \frac{\partial^2 \mathbf{u}}{\partial t^2} = (\lambda + \mu) \nabla(\nabla \cdot \mathbf{u}) + \mu \nabla^2 \mathbf{u} $$
这个矢量[二阶偏微分方程](@entry_id:175326)是研究线性弹性固体中波传播的出发点。

### 均匀各向同性固体中的[平面波](@entry_id:189798)

为了求解[纳维-柯西方程](@entry_id:189211)，我们寻找最简单的一类解——[平面波解](@entry_id:195230)。这类解假设[位移场](@entry_id:141476)在空间中以正弦形式传播。

#### [平面波解](@entry_id:195230)与[克里斯托费尔方程](@entry_id:180126)

我们假设一个时间谐和的[平面波解](@entry_id:195230)具有如下形式：
$$ \mathbf{u}(\mathbf{x}, t) = \mathbf{A} \exp[i(\mathbf{k} \cdot \mathbf{x} - \omega t)] $$
其中 $\mathbf{A}$ 是复数振幅矢量，决定了[质点](@entry_id:186768)[振动](@entry_id:267781)的极化方向；$\mathbf{k}$ 是[波矢](@entry_id:178620)量，其方向为[波的传播](@entry_id:144063)方向，大小 $k=|\mathbf{k}|$ 为波数；$\omega$ 是角频率。将此解代入[纳维-柯西方程](@entry_id:189211)，[微分](@entry_id:158718)运算转变为代数运算 [@problem_id:2676950]：
- 时间[二阶导数](@entry_id:144508)：$\frac{\partial^2 \mathbf{u}}{\partial t^2} \rightarrow -\omega^2 \mathbf{u}$
- [梯度的散度](@entry_id:270716)：$\nabla(\nabla \cdot \mathbf{u}) \rightarrow -(\mathbf{k} \cdot \mathbf{A})\mathbf{k}$
- 矢量拉普拉斯算子：$\nabla^2 \mathbf{u} \rightarrow -k^2 \mathbf{u}$

代入后，消去公共因子 $\exp[i(\mathbf{k} \cdot \mathbf{x} - \omega t)]$，我们得到一个关于振幅矢量 $\mathbf{A}$ 的代数方程：
$$ \rho \omega^2 \mathbf{A} = (\lambda + \mu)(\mathbf{k} \cdot \mathbf{A})\mathbf{k} + \mu k^2 \mathbf{A} $$
这个方程被称为**[克里斯托费尔方程](@entry_id:180126)**（Christoffel equation）。它是一个关于 $\mathbf{A}$ 的[特征值问题](@entry_id:142153)，只有当 $\mathbf{A}$ 满足特定条件时，非零解才存在。这些条件定义了介质中可能存在的波的类型。

#### 两种基本波型：[P波与S波](@entry_id:177682)

[克里斯托费尔方程](@entry_id:180126)的解揭示了在各向同性介质中存在两种截然不同的波型，它们的极化特性和[传播速度](@entry_id:189384)都不同。

**[纵波](@entry_id:172335)（P波）**

第一种可能性是[振动](@entry_id:267781)方向与传播方向平行，即 $\mathbf{A} \parallel \mathbf{k}$。这意味着 $\mathbf{A}$ 和 $\mathbf{k}$ 共线，因此它们的叉积为零：$\mathbf{k} \times \mathbf{A} = \mathbf{0}$。这种情况对应于**无旋波**（irrotational wave），因为其[位移场](@entry_id:141476)的旋度为零：$\nabla \times \mathbf{u} = i(\mathbf{k} \times \mathbf{A})\exp(\dots) = \mathbf{0}$ [@problem_id:2676950]。

在这种情况下，$\mathbf{k} \cdot \mathbf{A}$ 非零。[克里斯托费尔方程](@entry_id:180126)简化为：
$$ \rho \omega^2 \mathbf{A} = [(\lambda + \mu)k^2 + \mu k^2] \mathbf{A} = (\lambda + 2\mu)k^2 \mathbf{A} $$
为了得到非零的振幅 $\mathbf{A}$，必须满足以下的色散关系：
$$ \rho \omega^2 = (\lambda + 2\mu)k^2 $$
波的相速度 $c = \omega/k$ 因此为：
$$ c_p = \sqrt{\frac{\lambda + 2\mu}{\rho}} $$
这种波被称为**[纵波](@entry_id:172335)**（longitudinal wave）或**[P波](@entry_id:178440)**（primary/pressure wave），因为其[质点](@entry_id:186768)[振动](@entry_id:267781)方向与[波的传播](@entry_id:144063)方向一致，就像声波在空气中传播一样。它们是引起体积变化的[压缩波](@entry_id:747596)。

**横波（[S波](@entry_id:174890)）**

第二种可能性是[振动](@entry_id:267781)方向与传播方向垂直，即 $\mathbf{A} \perp \mathbf{k}$。这意味着它们的[点积](@entry_id:149019)为零：$\mathbf{k} \cdot \mathbf{A} = 0$。这种情况对应于**[螺线管](@entry_id:261182)波**或**无散波**（solenoidal wave），因为其[位移场](@entry_id:141476)的散度为零：$\nabla \cdot \mathbf{u} = i(\mathbf{k} \cdot \mathbf{A})\exp(\dots) = 0$ [@problem_id:2676950]。

在这种情况下，[克里斯托费尔方程](@entry_id:180126)中的 $(\lambda + \mu)(\mathbf{k} \cdot \mathbf{A})\mathbf{k}$ 项消失，方程急剧简化为：
$$ \rho \omega^2 \mathbf{A} = \mu k^2 \mathbf{A} $$
其[色散关系](@entry_id:140395)为：
$$ \rho \omega^2 = \mu k^2 $$
对应的相速度为：
$$ c_s = \sqrt{\frac{\mu}{\rho}} $$
这种波被称为**[横波](@entry_id:269527)**（transverse wave）或**S波**（secondary/shear wave），因为其[质点](@entry_id:186768)[振动](@entry_id:267781)方向垂直于[波的传播](@entry_id:144063)方向。这种[波的传播](@entry_id:144063)依赖于介质抵抗[剪切变形](@entry_id:170920)的能力，因此它与剪切模量 $\mu$ 直接相关。流体由于 $\mu=0$ 不能传播S波。对于一个给定的传播方向 $\mathbf{k}$，存在一个二维平面与之垂直，因此[S波](@entry_id:174890)有两个独立的极化方向，但它们的传播速度相同。

总结来说，对于给定的传播方向 $\mathbf{k}$，P波的极化方向 $\mathbf{A}$ 与 $\mathbf{k}$ 的夹角为 $0$ [弧度](@entry_id:171693)，而S波的极化方向与 $\mathbf{k}$ 的夹角为 $\pi/2$ [弧度](@entry_id:171693) [@problem_id:2676950]。

#### [亥姆霍兹分解](@entry_id:181767)视角

P波和[S波](@entry_id:174890)的独立性可以通过**[亥姆霍兹分解](@entry_id:181767)**（Helmholtz decomposition）得到更深刻的理解。任何一个矢量场（如此处的位移场 $\mathbf{u}$）都可以分解为一个[无旋场](@entry_id:183486)（标量势 $\phi$ 的梯度）和一个[无散场](@entry_id:260932)（矢量势 $\mathbf{\Psi}$ 的旋度）之和：
$$ \mathbf{u} = \nabla\phi + \nabla \times \mathbf{\Psi} $$
其中 $\nabla \times (\nabla \phi) = \mathbf{0}$，$\nabla \cdot (\nabla \times \mathbf{\Psi}) = 0$。

将这个分解代入[纳维-柯西方程](@entry_id:189211)，并分别取其[散度和旋度](@entry_id:270881)，可以证明方程[解耦](@entry_id:637294)为两个独立的波动方程 [@problem_id:2676976]：
- 一个关于体积变化 $\theta = \nabla \cdot \mathbf{u} = \nabla^2 \phi$ 的标量[波动方程](@entry_id:139839)：
$$ \frac{\partial^2 \theta}{\partial t^2} = c_p^2 \nabla^2 \theta \quad \text{with} \quad c_p = \sqrt{\frac{\lambda + 2\mu}{\rho}} $$
- 一个关于旋转 $\boldsymbol{\omega} = \nabla \times \mathbf{u} = \nabla \times (\nabla \times \mathbf{\Psi})$ 的矢量[波动方程](@entry_id:139839)：
$$ \frac{\partial^2 \boldsymbol{\omega}}{\partial t^2} = c_s^2 \nabla^2 \boldsymbol{\omega} \quad \text{with} \quad c_s = \sqrt{\frac{\mu}{\rho}} $$
这清晰地表明，无旋的P波（体积变形的传播）和无散的[S波](@entry_id:174890)（[剪切变形](@entry_id:170920)的传播）在均匀各向同性介质中是独立传播的，互不耦合。

#### 物理诠释与[材料稳定性](@entry_id:183933)

P波和S波的速度表达式蕴含着丰富的[物理信息](@entry_id:152556)。首先，对于任何物理上稳定的弹性材料，必须满足 $\mu > 0$ 和 $\lambda+2\mu > 0$。这些**稳定性条件**确保了材料在受到剪切或压缩时会抵[抗变](@entry_id:192290)形并存储正的[应变能](@entry_id:162699)，而不是自发坍塌。这些条件直接保证了 $c_p$ 和 $c_s$ 都是正实数 [@problem_id:2676976]。

由于 $\lambda$ 和 $\mu$ 对于稳定材料都是正的，显然有 $\lambda+2\mu > \mu$，这意味着**P波的[传播速度](@entry_id:189384)总是快于S波** ($c_p > c_s$) 。这也就是为什么在地震发生后，地震台总是先接收到[P波](@entry_id:178440)，然后才是破坏性更强的[S波](@entry_id:174890)。

波速比 $c_p/c_s$ 是一个只依赖于[材料弹性](@entry_id:751729)常数比值的[无量纲参数](@entry_id:169335)。它可以方便地用[泊松比](@entry_id:158876)（Poisson's ratio）$\nu = \frac{\lambda}{2(\lambda+\mu)}$ 来表示 [@problem_id:2676976]：
$$ \frac{c_p}{c_s} = \sqrt{\frac{\lambda+2\mu}{\mu}} = \sqrt{\frac{2\nu}{1-2\nu} + 2} = \sqrt{\frac{2(1-\nu)}{1-2\nu}} $$
这个比值在地球物理和[材料科学](@entry_id:152226)中有重要应用。例如，在不可压缩极限下（$\nu \to 0.5$），分母趋于零，这意味着 $\lambda \to \infty$，[P波](@entry_id:178440)速度 $c_p$ 趋于无穷大，而S波速度 $c_s$ 保持有限。这表明[不可压缩材料](@entry_id:159741)会瞬时传递体积扰动 [@problem_id:2676959]。

### [弹性波](@entry_id:196203)中的能量

波的传播本质上是能量的传播。理解能量在弹性介质中的流动对于评估波的强度和衰减至关重要。

#### 能量密度与能量通量

在弹性介质中，总的机械能密度 $E$ 是单位体积内的动能密度 $K$ 和[应变能密度](@entry_id:200085) $W$ 之和：
$$ E = K + W = \frac{1}{2}\rho \dot{\mathbf{u}} \cdot \dot{\mathbf{u}} + W(\boldsymbol{\varepsilon}) $$
其中 $\dot{\mathbf{u}}$ 是质点速度。对于[超弹性材料](@entry_id:190241)，[应力张量](@entry_id:148973)可以由[应变能密度函数](@entry_id:755490)对求导得到，$\boldsymbol{\sigma} = \partial W / \partial \boldsymbol{\varepsilon}$。

通过计算总能量密度 $E$ 对时间的导数，并结合运动方程和本构关系，可以推导出一个局域的[能量守恒](@entry_id:140514)定律 [@problem_id:2676993]：
$$ \frac{\partial E}{\partial t} + \nabla \cdot \mathbf{Q} = 0 $$
这个方程的形式与电磁学中的坡印亭定理非常相似。其中，$\mathbf{Q}$ 被称为**[能量通量](@entry_id:266056)矢量**或**Umov-[Poynting矢量](@entry_id:269386)**，它描述了单位时间穿过单位面积的[能量流](@entry_id:142770)。其表达式为：
$$ \mathbf{Q} = -\boldsymbol{\sigma} \cdot \dot{\mathbf{u}} \quad \text{or} \quad Q_i = -\sigma_{ij}\dot{u}_j $$
负号的出现是由于符号约定的选择，它表示 $\mathbf{Q}$ 指向能量流出的方向。这个矢量描述了机械功如何通过应力在介质中传递。

#### [平面波](@entry_id:189798)的[能量传播](@entry_id:202589)

我们可以将上述理论应用于一个具体的例子：沿 $x_1$ 方向传播的[P波](@entry_id:178440)，其[位移场](@entry_id:141476)为 $\mathbf{u}(\mathbf{x}, t) = U_0 \cos(k x_1 - \omega t) \mathbf{e}_1$。通过计算应力 $\sigma_{11}$ 和速度 $\dot{u}_1$，我们可以得到[能量通量](@entry_id:266056)的大小：
$$ |\mathbf{Q}| = \sqrt{(\lambda+2\mu)\rho} \, U_0^2 \omega^2 \sin^2(k x_1 - \omega t) $$
这是一个瞬时值，它随时间和空间[振荡](@entry_id:267781)。在实际应用中，我们更关心其在一个周期内的平均值。对时间求平均，考虑到 $\langle \sin^2(\cdot) \rangle = 1/2$，我们得到时间平均的能量通量大小，也即波的**强度**（intensity）：
$$ \langle |\mathbf{Q}| \rangle = \frac{1}{2} \sqrt{(\lambda+2\mu)\rho} \, U_0^2 \omega^2 = \frac{1}{2} (\rho c_p) (U_0 \omega)^2 $$
这个结果意义重大：波的强度与材料的**[声阻抗](@entry_id:267232)**（acoustic impedance）$\rho c_p$、振幅 $U_0$ 的平方以及频率 $\omega$ 的平方成正比 [@problem_id:2676993]。这解释了为什么高频、高振幅的波携带更多的能量。

### [各向异性介质](@entry_id:187796)与界面中的波传播

现实世界中的许多材料，如晶体和[复合材料](@entry_id:139856)，都表现出各向异性，即它们的弹性特性随方向变化。这导致了更复杂的波传播行为。

#### [各向异性介质](@entry_id:187796)中的波

对于一般的[各向异性介质](@entry_id:187796)，其本构关系由一个四阶[刚度张量](@entry_id:176588) $C_{ijkl}$ 描述：$\sigma_{ij} = C_{ijkl}\varepsilon_{kl}$。遵循与各向同性情况类似的推导，将[平面波解](@entry_id:195230)代入运动方程，可以得到一般形式的[克里斯托费尔方程](@entry_id:180126) [@problem_id:2676964]：
$$ \Gamma_{ik} A_k = \rho c^2 A_i $$
其中，$\mathbf{\Gamma}$ 是**[克里斯托费尔声学张量](@entry_id:186595)**（Christoffel acoustic tensor），其分量为：
$$ \Gamma_{ik} = C_{ijkl} n_j n_l $$
它依赖于传播方向的单位矢量 $\mathbf{n}$。由于刚度[张量的对称性](@entry_id:202126)（$C_{ijkl}=C_{klij}$），$\mathbf{\Gamma}$ 是一个对称张量。这意味着对于任何传播方向 $\mathbf{n}$，总存在三个实数[特征值](@entry_id:154894)（对应三个相速度的平方）和三个相互正交的[特征向量](@entry_id:151813)（极化方向）。

然而，与各向同性介质不同，在一般传播方向上，这三个极化方向通常既不严格平行也不严格垂直于传播方向 $\mathbf{n}$。因此，它们被称为**准[纵波](@entry_id:172335)**（quasi-longitudinal, qL）和两个**准[横波](@entry_id:269527)**（quasi-transverse, qS）。

#### [慢度面](@entry_id:189732)与群速度

为了更好地可视化[各向异性介质](@entry_id:187796)中的波速，我们引入**慢度矢量**（slowness vector）$\mathbf{s} = \mathbf{n}/c$。它的方向是相速度的方向，大小是相速度的倒数。[克里斯托费尔方程](@entry_id:180126)的特征值问题可以重写为关于 $\mathbf{s}$ 的方程，$\det(C_{ijkl}s_j s_l - \rho \delta_{ik}) = 0$。

这个方程在三维慢度空间 $(s_1, s_2, s_3)$ 中定义了三个[曲面](@entry_id:267450)，称为**[慢度面](@entry_id:189732)**（slowness surface）。每个面对应一种波型（qL, qS1, qS2）。从原点到[慢度面](@entry_id:189732)上一点的距离，就是该方向上相应波型的慢度值 $1/c$ [@problem_id:2676964]。

在[各向异性介质](@entry_id:187796)中，波的[能量传播](@entry_id:202589)方向（由**群速度** $\mathbf{v}_g = \nabla_{\mathbf{k}}\omega$ 给出）与相速度方向通常不一致。一个深刻的几何关系是：群[速度矢量](@entry_id:269648)的方向总是垂直于其在[慢度面](@entry_id:189732)上的对应点。这意味着能量会沿着[慢度面](@entry_id:189732)的[法线](@entry_id:167651)方向传播。这种现象导致能量束的偏离，是[各向异性声](@entry_id:158017)学中的一个核心特征。

#### 界面处的波相互作用

当[弹性波](@entry_id:196203)遇到两种不同材料的界面时，会发生反射和透射。要确定反射波和透射波的振幅与方向，必须在界面上施加**边界条件**。

对于一个**完美黏合**（perfectly bonded）的界面，其物理含义是界面两侧的材料作为一个整体运动，没有分离也无相对滑移。这可以从两个基本物理原理导出相应的数学条件 [@problem_id:2BEF926]：

1.  **[运动学](@entry_id:173318)相容性（位移连续）**: 为了保证材料的连续性，没有间隙或重叠，界面上[位移矢量](@entry_id:262782)必须是连续的。
    $$ \mathbf{u}^{(1)} = \mathbf{u}^{(2)} \quad \text{at the interface} $$

2.  **[动力学平衡](@entry_id:187220)（牵[引力](@entry_id:175476)连续）**: 根据[牛顿第三定律](@entry_id:166652)（作用力与反作用力），作用在界面任意一小块面积上的力必须是平衡的。通过对一个跨越界面的“药盒”形微元体应用动量守恒定律，并让其厚度趋于零，可以证明界面上的牵[引力](@entry_id:175476)矢量必须连续。牵[引力](@entry_id:175476)矢量定义为 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$，其中 $\mathbf{n}$ 是界面的法向量。
    $$ \boldsymbol{\sigma}^{(1)}\mathbf{n} = \boldsymbol{\sigma}^{(2)}\mathbf{n} \quad \text{at the interface} $$
    这表示跨界面的[法向应力](@entry_id:260622)（[正应力](@entry_id:260622)）和切向应力（剪切应力）都是连续的。

这两个边界条件——位移连续和牵[引力](@entry_id:175476)连续——是求解[弹性波](@entry_id:196203)在界面处[反射与透射](@entry_id:156002)问题的基础。它们构成了[联立方程](@entry_id:193238)组，可以解出所有出射波的振幅。在特定情况下，例如波在具有对称性的分层介质中传播，[S波](@entry_id:174890)还可以进一步解耦为在入射面内[振动](@entry_id:267781)的SV波（shear-vertical）和垂直于入射面[振动](@entry_id:267781)的SH波（shear-horizontal）[@problem_id:2676963]。