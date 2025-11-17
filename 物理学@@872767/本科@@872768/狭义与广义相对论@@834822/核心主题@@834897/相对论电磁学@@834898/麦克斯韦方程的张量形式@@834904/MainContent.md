## 引言
经典电磁学是物理学的一大支柱，其核心——[麦克斯韦方程组](@entry_id:150940)——完美地描述了电、磁及光的现象。然而，这些以三维矢量写出的方程，却掩盖了其与爱因斯坦[狭义相对论](@entry_id:275552)之间深刻的内在联系。尽管麦克斯韦理论本身是相对论性的，但其形式却不具备明显的[洛伦兹协变性](@entry_id:161987)，这构成了一个亟待解决的理论美学与结构性问题。如何以一种能彰显时空统一性的语言来重述电磁理论，正是本文将要探讨的核心。

本文将带领读者进入四维时空的张量世界，系统地解决这一问题。通过学习本文，你将掌握将[麦克斯韦方程组](@entry_id:150940)改写为协变形式的强大工具。在“原理与机制”一章中，我们将引入[四维势](@entry_id:188407)和电磁场张量，将看似独立的电场和磁场统一为单一的几何客体，并推导出简洁优美的张量形式麦克斯韦方程。随后，在“应用与跨学科联系”一章中，我们将展示这一形式的威力，探讨它如何简化相对论性问题，并自然地延伸至广义相对论和[量子理论](@entry_id:145435)等前沿领域。最后，通过“动手实践”部分，你将有机会亲自运用这些概念解决具体问题，从而巩固所学。让我们一同开始这段揭示电磁学深刻对称性之美的旅程。

## 原理与机制

在[狭义相对论](@entry_id:275552)的框架下，物理定律必须在所有[惯性参考系](@entry_id:276742)中具有相同的形式，即[协变](@entry_id:634097)性。麦克斯韦的经典电磁学理论，尽管其本身已与相对论兼容，但其以三维矢量写出的形式却掩盖了这种深刻的对称性。为了揭示电磁学内蕴的[洛伦兹协变性](@entry_id:161987)，我们必须将其重写为四维时空的语言，即张量语言。本章将系统地阐述[电磁场](@entry_id:265881)的[张量表示法](@entry_id:272140)，统一[麦克斯韦方程组](@entry_id:150940)，并探讨由此产生的深刻物理后果。

### 场与势的统一：[电磁张量](@entry_id:272274)

在[经典电动力学](@entry_id:270496)中，[电场](@entry_id:194326) $\vec{E}$ 和[磁场](@entry_id:153296) $\vec{B}$ 是通过电标势 $\phi$ 和磁矢势 $\vec{A}$ 引入的。相对论将时间和空间统一为四维时空，同样，它也将电标势和[磁矢势](@entry_id:141246)统一为一个单一的物理量——**[四维势](@entry_id:188407)** (four-potential) $A^{\mu}$。

[四维势](@entry_id:188407)是一个[四维矢量](@entry_id:275085)，其分量定义为：
$$ A^{\mu} = (\phi/c, A_x, A_y, A_z) = (\phi/c, \vec{A}) $$
其中 $c$ 是[真空中的光速](@entry_id:272753)。第零个分量（时间分量）与电[标势](@entry_id:276177)成正比，而其余三个空间分量构成了经典的三维磁矢势。

物理场，即[电场和磁场](@entry_id:261347)，是从这个更基本的[四维势](@entry_id:188407)导出的。[电场和磁场](@entry_id:261347)的所有信息被统一编码在一个二阶[反对称张量](@entry_id:199349)中，称为**[电磁场强度张量](@entry_id:267409)** (electromagnetic field strength tensor)，记为 $F_{\mu\nu}$。它由[四维势](@entry_id:188407)的“四维旋度”定义：
$$ F_{\mu\nu} = \partial_{\mu} A_{\nu} - \partial_{\nu} A_{\mu} $$
这里，$\partial_{\mu} \equiv \frac{\partial}{\partial x^{\mu}}$ 是四维[梯度算子](@entry_id:275922)，其中 $x^{\mu} = (ct, x, y, z)$ 是时空坐标。

#### 内在的[反对称性](@entry_id:261893)

从电磁场张量的定义式出发，一个至关重要的数学属性立刻显现出来。如果我们交换张量中的两个指标，我们会得到：
$$ F_{\nu\mu} = \partial_{\nu} A_{\mu} - \partial_{\mu} A_{\nu} = -(\partial_{\mu} A_{\nu} - \partial_{\nu} A_{\mu}) = -F_{\mu\nu} $$
这表明 $F_{\mu\nu}$ 必然是一个**[反对称张量](@entry_id:199349)** [@problem_id:1838931]。这一性质是其定义的直接推论，不依赖于势 $A_{\mu}$ 的具体形式。反对称性意味着对角分量恒为零，因为当 $\mu = \nu$ 时，$F_{\mu\mu} = -F_{\mu\mu}$，这只有在 $F_{\mu\mu} = 0$ 时才成立。因此，一个 $4 \times 4$ 的[反对称张量](@entry_id:199349)只有 $6$ 个独立分量，这恰好对应于[电场](@entry_id:194326)的三个分量和[磁场](@entry_id:153296)的三个分量。

#### [规范不变性](@entry_id:137857)

[四维势](@entry_id:188407) $A_{\mu}$ 并非唯一可测的。我们可以对它进行**规范变换** (gauge transformation) 而不改变任何可观测的物理量。规范变换通过一个任意的光滑[标量场](@entry_id:151443) $\Lambda(x^{\alpha})$ 来实现：
$$ A'_{\mu} = A_{\mu} + \partial_{\mu}\Lambda $$
让我们考察在此变换下场强度张量如何变化。新的张量 $F'_{\mu\nu}$ 由新的势 $A'_{\mu}$ 计算得出：
$$ F'_{\mu\nu} = \partial_{\mu}A'_{\nu} - \partial_{\nu}A'_{\mu} = \partial_{\mu}(A_{\nu} + \partial_{\nu}\Lambda) - \partial_{\nu}(A_{\mu} + \partial_{\mu}\Lambda) $$
利用导数的线性性质，上式可以展开为：
$$ F'_{\mu\nu} = (\partial_{\mu}A_{\nu} - \partial_{\nu}A_{\mu}) + (\partial_{\mu}\partial_{\nu}\Lambda - \partial_{\nu}\partial_{\mu}\Lambda) $$
由于我们假设 $\Lambda$ 是一个足够光滑的函数，其二阶[混合偏导数](@entry_id:139334)的求导次序可以交换，即 $\partial_{\mu}\partial_{\nu}\Lambda = \partial_{\nu}\partial_{\mu}\Lambda$。因此，括号中的第二项为零 [@problem_id:1838936]。我们最终得到：
$$ F'_{\mu\nu} = F_{\mu\nu} $$
这表明[电磁场强度张量](@entry_id:267409)在[规范变换](@entry_id:176521)下保持不变。这揭示了一个深刻的物理原理：势本身不是物理实在，它们包含非物理的自由度，而由它们导出的场才是与物理实在直接对应的。

### 解码[电磁张量](@entry_id:272274)

现在我们来具体揭示[电磁张量](@entry_id:272274)的 $6$ 个独立分量与我们熟悉的[电场](@entry_id:194326) $\vec{E}$ 和[磁场](@entry_id:153296) $\vec{B}$ 之间的精确关系。为此，我们需要计算 $F^{\mu\nu}$ 的各个分量。$F^{\mu\nu}$ 是 $F_{\mu\nu}$ 的逆变形式，通过[闵可夫斯基度规](@entry_id:154660) $\eta^{\mu\nu}$ 提[升指标](@entry_id:265340)得到，$F^{\mu\nu} = \eta^{\mu\alpha}\eta^{\nu\beta}F_{\alpha\beta}$。我们采用 $(+,-,-,-)$ 的度规符号约定。

#### [电场](@entry_id:194326)分量

[电场](@entry_id:194326)分量隐藏在 $F^{\mu\nu}$ 的“时空”混合分量中，即一个指标为 $0$，另一个为空间指标 $i \in \{1, 2, 3\}$。例如，我们来计算 $F^{01}$。根据定义：
$$ F^{01} = \partial^{0} A^{1} - \partial^{1} A^{0} $$
在 $(+,-,-,-)$ 符号约定下，逆变四维梯度为 $\partial^{\mu} = (\frac{1}{c}\frac{\partial}{\partial t}, -\vec{\nabla})$。因此，$\partial^0 = \frac{1}{c}\frac{\partial}{\partial t}$ 且 $\partial^1 = -\frac{\partial}{\partial x^1} = -\frac{\partial}{\partial x}$。同时，[四维势](@entry_id:188407) $A^{\mu} = (\phi/c, A_x, A_y, A_z)$。代入这些定义：
$$ F^{01} = \left(\frac{1}{c}\frac{\partial}{\partial t}\right)A_x - \left(-\frac{\partial}{\partial x}\right)\left(\frac{\phi}{c}\right) = \frac{1}{c}\left(\frac{\partial A_x}{\partial t} + \frac{\partial \phi}{\partial x}\right) $$
我们知道[电场](@entry_id:194326)的定义是 $\vec{E} = -\vec{\nabla}\phi - \frac{\partial \vec{A}}{\partial t}$。其 $x$ 分量为 $E_x = -\frac{\partial \phi}{\partial x} - \frac{\partial A_x}{\partial t}$。比较我们为 $F^{01}$ 推导的表达式，可以发现：
$$ F^{01} = -\frac{1}{c} E_x $$
通过类似的计算，我们可以得到所有[电场](@entry_id:194326)分量与张量分量的关系 [@problem_id:1838954]：
$$ E_x = -c F^{01}, \quad E_y = -c F^{02}, \quad E_z = -c F^{03} $$
或者更紧凑地写作 $E_i = -c F^{0i}$。

#### [磁场](@entry_id:153296)分量

[磁场](@entry_id:153296)分量则编码在 $F^{\mu\nu}$ 的纯空间分量中，即两个指标都为空间指标 $i,j \in \{1, 2, 3\}$。例如，我们计算 $F^{12}$：
$$ F^{12} = \partial^{1} A^{2} - \partial^{2} A^{1} = \left(-\frac{\partial}{\partial x}\right)A_y - \left(-\frac{\partial}{\partial y}\right)A_x = \frac{\partial A_x}{\partial y} - \frac{\partial A_y}{\partial x} $$
我们知道[磁场](@entry_id:153296)的定义是 $\vec{B} = \vec{\nabla} \times \vec{A}$。其 $z$ 分量为 $B_z = \frac{\partial A_y}{\partial x} - \frac{\partial A_x}{\partial y}$。比较可知：
$$ F^{12} = -B_z $$
通过对其他空间分量进行类似的计算，我们可以发现[磁场](@entry_id:153296)分量与张量分量之间的关系可以用[列维-奇维塔符号](@entry_id:193594) $\epsilon_{ijk}$ 简洁地表示：
$$ F^{ij} = -\epsilon^{ijk} B_k $$
其中 $\epsilon^{123}=+1$。这等价于以下关系 [@problem_id:1838967]：
$$ B_x = -F^{23}, \quad B_y = -F^{31} = F^{13}, \quad B_z = -F^{12} $$

#### 矩阵表示

综上所述，逆变[电磁场强度张量](@entry_id:267409) $F^{\mu\nu}$ 的矩阵形式完整地展示了电场和磁场的统一：
$$ F^{\mu\nu} = \begin{pmatrix} 0  -E_x/c  -E_y/c  -E_z/c \\ E_x/c  0  -B_z  B_y \\ E_y/c  B_z  0  -B_x \\ E_z/c  -B_y  B_x  0 \end{pmatrix} $$
这张矩阵清晰地展示了 $F^{\mu\nu}$ 是一个[反对称张量](@entry_id:199349)，其对角线元素为零。时间-空间分量对应于[电场](@entry_id:194326)，而空间-空间分量对应于[磁场](@entry_id:153296)。洛伦兹变换作用于这个张量时，会混合其所有分量，从而将[电场和磁场](@entry_id:261347)相互转化，这正是[相对论电动力学](@entry_id:160964)的核心特征。

### [麦克斯韦方程组的协变形式](@entry_id:197529)

有了描述场和源的张量语言，我们现在可以将四个麦克斯韦方程组重写为两个异常简洁的张量方程。

首先，我们需要将[电荷密度](@entry_id:144672) $\rho$ 和电流密度 $\vec{J}$ 统一为**[四维流密度](@entry_id:262568)** (four-current density) $J^{\mu}$：
$$ J^{\mu} = (c\rho, J_x, J_y, J_z) = (c\rho, \vec{J}) $$
$J^{\mu}$ 是一个[四维矢量](@entry_id:275085)，它描述了时空中[电荷](@entry_id:275494)的[分布](@entry_id:182848)和运动。例如，对于一个在惯性系 S' 中静止的[电荷](@entry_id:275494) $q$，其在该[参考系](@entry_id:169232)中的[电荷密度](@entry_id:144672)为 $\rho' = q\delta^3(\vec{r}')$，电流密度为 $\vec{J}'=0$。如果另一个[参考系](@entry_id:169232) S'' 相对于 S' 以速度 $-\vec{u}$ 运动，那么在 S'' 中观测到的电荷密度和电流密度就是 $J^{\mu''}$ 的分量。例如，若 $\vec{u}=u\hat{y}$，则在 S'' 中，[电荷](@entry_id:275494) $q$ 以速度 $-u\hat{y}$ 运动，其电荷密度为 $\rho'' = q\delta^3(\vec{r}'')$（由于[洛伦兹收缩](@entry_id:199078)效应，严格的表达式需要包含一个$\gamma$因子，但在原点处的狄拉克函数表示下，这一效应被吸收到积分中），而电流密度则为 $\vec{J}'' = q(-u\hat{y})\delta^3(\vec{r}'') = (0, -qu\delta^3(\vec{r}''), 0)$。因此，在原点 $t''=0, \vec{r}''=0$ 处，[电荷密度](@entry_id:144672)为 $\rho'' = q\delta^3(\vec{0})$，电流的 y 分量为 $J''_y = -qu\delta^3(\vec{0})$ [@problem_id:1838953]。

#### 有源麦克斯韦方程

包含[源项](@entry_id:269111)的两个麦克斯韦方程——[高斯电场定律](@entry_id:146732)和[安培-麦克斯韦定律](@entry_id:266368)——可以被统一为一个张量方程：
$$ \partial_{\mu} F^{\mu\nu} = \mu_0 J^{\nu} $$
其中 $\mu_0$ 是[真空磁导率](@entry_id:186031)。这个方程被称为**非齐次麦克斯韦方程** (inhomogeneous Maxwell's equation)。它指出，[电磁场张量](@entry_id:158921)的四维散度等于源（[四维流密度](@entry_id:262568)）。

让我们通过考察这个方程的不同分量来验证它确实包含了经典的定律。
当 $\nu=0$ 时，方程为 $\partial_{\mu} F^{\mu 0} = \mu_0 J^{0}$。展开对 $\mu$ 的求和：
$$ \partial_0 F^{00} + \partial_1 F^{10} + \partial_2 F^{20} + \partial_3 F^{30} = \mu_0 (c\rho) $$
根据 $F^{\mu\nu}$ 的矩阵形式，我们有 $F^{00}=0$，$F^{10} = E_x/c$，$F^{20} = E_y/c$，$F^{30} = E_z/c$。同时，$\partial_0 = \frac{1}{c}\frac{\partial}{\partial t}$，$\partial_i = \frac{\partial}{\partial x^i}$。代入后得到：
$$ 0 + \frac{\partial (E_x/c)}{\partial x} + \frac{\partial (E_y/c)}{\partial y} + \frac{\partial (E_z/c)}{\partial z} = \mu_0 c\rho $$
$$ \frac{1}{c} (\nabla \cdot \vec{E}) = \mu_0 c\rho \implies \nabla \cdot \vec{E} = \mu_0 c^2 \rho $$
利用关系式 $c^2 = 1/(\epsilon_0 \mu_0)$，我们得到 $\nabla \cdot \vec{E} = \rho/\epsilon_0$，这正是**[高斯电场定律](@entry_id:146732)** [@problem_id:1838961]。

若取 $\nu=1, 2, 3$ (空间分量)，通过类似的推导，可以得到**[安培-麦克斯韦定律](@entry_id:266368)**的三个分量。

#### 无源麦克斯韦方程

另外两个不含[源项](@entry_id:269111)的麦克斯韦方程——高斯[磁场](@entry_id:153296)定律和[法拉第感应定律](@entry_id:146175)——则被统一为另一个张量方程：
$$ \partial_{\lambda} F_{\mu\nu} + \partial_{\mu} F_{\nu\lambda} + \partial_{\nu} F_{\lambda\mu} = 0 $$
这个方程被称为**齐次麦克斯韦方程** (homogeneous Maxwell's equation) 或[比安基恒等式](@entry_id:261685) (Bianchi identity)。事实上，这个方程并不是一个独立的动力学定律，而是[场张量](@entry_id:186486)由[四维势](@entry_id:188407)导出的数学推论 ($F_{\mu\nu} = \partial_\mu A_\nu - \partial_\nu A_\mu$)。

同样，我们可以通过选择不同的指标组合来重现经典的定律。例如，我们选择 $(\lambda, \mu, \nu) = (0, 1, 3)$ [@problem_id:1838962]：
$$ \partial_{0} F_{13} + \partial_{1} F_{30} + \partial_{3} F_{01} = 0 $$
我们需要[协变张量](@entry_id:634493) $F_{\mu\nu}$ 的分量。$F_{0i} = E_i/c$ 以及 $F_{ij} = -\epsilon_{ijk}B_k$。利用[反对称性](@entry_id:261893) $F_{\mu\nu}=-F_{\nu\mu}$，我们有：
*   $F_{13} = -\epsilon_{13k}B_k = -\epsilon_{132}B_2 = -(-1)B_y = B_y$
*   $F_{30} = -F_{03} = -E_z/c$
*   $F_{01} = E_x/c$

代入方程中：
$$ \frac{\partial}{\partial(ct)} B_y + \frac{\partial}{\partial x}(-E_z/c) + \frac{\partial}{\partial z}(E_x/c) = 0 $$
两边同乘以 $c$ 并整理：
$$ \frac{\partial B_y}{\partial t} - \frac{\partial E_z}{\partial x} + \frac{\partial E_x}{\partial z} = 0 \implies \frac{\partial E_x}{\partial z} - \frac{\partial E_z}{\partial x} = -\frac{\partial B_y}{\partial t} $$
这正是**[法拉第感应定律](@entry_id:146175)** $(\nabla \times \vec{E})_y = -(\frac{\partial \vec{B}}{\partial t})_y$ 的 y 分量。选择其他空间指标组合，如 $(\lambda, \mu, \nu) = (1, 2, 3)$，则会导出**高斯[磁场](@entry_id:153296)定律** $\nabla \cdot \vec{B} = 0$。

### 基本推论与扩展

将麦克斯韦方程组写成[协变](@entry_id:634097)形式，不仅使其形式优美简洁，更重要的是，它揭示了电磁理论更深层次的结构和基本守恒律。

#### 电荷守恒

电荷守恒定律是物理学中最基本的原理之一。在张量形式中，它不再是一个需要额外假设的公理，而是麦克斯韦方程的直接数学推论。取非齐次麦克斯韦方程 $\partial_{\nu} F^{\mu\nu} = \mu_0 J^{\mu}$，然后对其两边作用四维[散度算子](@entry_id:265975) $\partial_{\mu}$：
$$ \partial_{\mu}\partial_{\nu} F^{\mu\nu} = \mu_0 \partial_{\mu} J^{\mu} $$
方程左边涉及对张量 $F^{\mu\nu}$ 作用两个偏导算子。由于[偏导数](@entry_id:146280)可以交换次序，$\partial_{\mu}\partial_{\nu}$ 是一个对指标 $\mu, \nu$ 对称的算子。然而，它作用的对象 $F^{\mu\nu}$ 是一个[反对称张量](@entry_id:199349)。一个[对称算子](@entry_id:272489)作用于一个[反对称张量](@entry_id:199349)并对所有指标求和的结果必然为零。具体来说：
$$ \partial_{\mu}\partial_{\nu} F^{\mu\nu} = - \partial_{\mu}\partial_{\nu} F^{\nu\mu} $$
交换[哑指标](@entry_id:188070) $\mu \leftrightarrow \nu$，上式变为 $- \partial_{\nu}\partial_{\mu} F^{\mu\nu}$。由于偏导数可交换，这等于 $- \partial_{\mu}\partial_{\nu} F^{\mu\nu}$。因此我们有 $\partial_{\mu}\partial_{\nu} F^{\mu\nu} = - \partial_{\mu}\partial_{\nu} F^{\mu\nu}$，这意味着 $\partial_{\mu}\partial_{\nu} F^{\mu\nu} = 0$。
所以，麦克斯韦方程的左边恒为零，这意味着右边也必须为零：
$$ \mu_0 \partial_{\mu} J^{\mu} = 0 \implies \partial_{\mu} J^{\mu} = 0 $$
这正是**[电荷守恒](@entry_id:264158)的连续性方程** [@problem_id:1838906]。它表明[四维流密度](@entry_id:262568)的散度为零，即[电荷](@entry_id:275494)不能凭空产生或消失。

#### 能量、动量与应力

[电磁场](@entry_id:265881)本身携带能量和动量。这些物理量以及它们在空间中的流动（通量）被统一在一个对称的[二阶张量](@entry_id:199780)中，即**[电磁应力-能量张量](@entry_id:267456)** (electromagnetic stress-energy tensor) $T^{\mu\nu}$。其定义为：
$$ T^{\mu\nu} = \frac{1}{\mu_0} \left( -F^{\mu\alpha}F^{\nu}{}_{\alpha} + \frac{1}{4} \eta^{\mu\nu} F_{\lambda\sigma}F^{\lambda\sigma} \right) $$
这个张量的各个分量具有明确的物理意义：
*   $T^{00}$ 是[电磁场](@entry_id:265881)的**能量密度**。
*   $T^{0i}$ 是[能量通量](@entry_id:266056)密度，即**坡印亭矢量** (Poynting vector) 的第 $i$ 个分量。
*   $T^{i0}$ 是[动量密度](@entry_id:271360)。
*   $T^{ij}$ (其中 $i,j$ 为空间指标) 构成**[麦克斯韦应力张量](@entry_id:153513)** (Maxwell stress tensor)。它描述了动量的流动。对角分量 $T^{ii}$（不求和）表示作用在垂直于 $i$ 轴的单位面积上、沿 $i$ 方向的**法向应力**（压力或张力）[@problem_id:1838919]。非对角分量 $T^{ij}$ ($i \neq j$) 则表示**切向应力**（剪应力）。

[电磁场](@entry_id:265881)与带电物质相互作用时，总的能量和动量是守恒的。这表现为场的能量动量与物质的能量动量之间的交换。这一[守恒定律](@entry_id:269268)的[微分形式](@entry_id:146747)是：
$$ \partial_{\mu} T^{\mu\nu}_{\text{matter}} + \partial_{\mu} T^{\mu\nu}_{\text{field}} = 0 $$
场的应力-能量张量的四维散度描述了场传递给物质的[四维力](@entry_id:273918)密度。通过相当复杂的代数运算，并同时使用齐次和非齐次两个麦克斯韦方程，可以证明 [@problem_id:1838937]：
$$ \partial_{\mu} T^{\mu\nu} = -F^{\nu\alpha}J_{\alpha} $$
右边的项 $f^{\nu} = F^{\nu\alpha}J_{\alpha}$ 正是作用在[电荷](@entry_id:275494)和电流[分布](@entry_id:182848)上的**洛伦兹[四维力](@entry_id:273918)密度** (Lorentz four-force density)。这个方程优雅地表达了[能量-动量守恒](@entry_id:194427)：[电磁场](@entry_id:265881)[应力-能量张量](@entry_id:146544)的散度（代表场自身能量动量的变化率）等于场对物质施加的力的负值。

#### [拉格朗日表述](@entry_id:188652)

电磁理论的[协变](@entry_id:634097)形式也可以从一个更基本的出发点——[作用量原理](@entry_id:154742)——导出。整个系统的动力学由一个称为**拉格朗日密度** (Lagrangian density) $\mathcal{L}$ 的标量描述。对于与[四维电流](@entry_id:199021) $J^{\mu}$ 相互作用的[电磁场](@entry_id:265881)，其拉格朗日密度为：
$$ \mathcal{L} = -\frac{1}{4\mu_0} F_{\mu\nu}F^{\mu\nu} - J_{\mu} A^{\mu} $$
第一项是场的动能项，是[场强张量](@entry_id:159746)的[洛伦兹不变量](@entry_id:161821)；第二项是场与源的[相互作用项](@entry_id:637283)。根据最小作用量原理，将[四维势](@entry_id:188407) $A_{\nu}$ 的每个分量视为独立的场，应用[欧拉-拉格朗日方程](@entry_id:137827)：
$$ \partial_{\mu}\left(\frac{\partial\mathcal{L}}{\partial(\partial_{\mu}A_{\nu})}\right) - \frac{\partial\mathcal{L}}{\partial A_{\nu}} = 0 $$
可以推导出非齐次麦克斯韦方程 $\partial_{\mu}F^{\mu\nu} = \mu_0 J^{\nu}$。

这种表述方法的强大之处在于其灵活性和普适性。例如，我们可以探讨修改理论的后果。假设[光子](@entry_id:145192)具有一个微小的静止质量 $m_{\gamma}$，我们可以在拉格朗日密度中增加一个质量项 [@problem_id:1838934]：
$$ \mathcal{L}_{\text{mass}} = \frac{c^2 m_{\gamma}^2}{2\mu_0 \hbar^2} A_{\mu} A^{\mu} $$
这个新项对欧拉-拉格朗日方程的贡献是 $\frac{\partial \mathcal{L}_{\text{mass}}}{\partial A_{\nu}}$。我们来计算它。首先，将 $A^{\mu}$ 写成协变分量的形式 $A^{\mu}=g^{\mu\rho}A_{\rho}$：
$$ \mathcal{L}_{\text{mass}} = \frac{c^2 m_{\gamma}^2}{2\mu_0 \hbar^2} g^{\mu\rho} A_{\mu} A_{\rho} $$
对其求关于 $A_{\nu}$ 的偏导数：
$$ \frac{\partial \mathcal{L}_{\text{mass}}}{\partial A_{\nu}} = \frac{c^2 m_{\gamma}^2}{2\mu_0 \hbar^2} (g^{\nu\rho}A_{\rho} + g^{\mu\nu}A_{\mu}) = \frac{c^2 m_{\gamma}^2}{\mu_0 \hbar^2} g^{\nu\rho}A_{\rho} = \frac{c^2 m_{\gamma}^2}{\mu_0 \hbar^2} A^{\nu} $$
对于时间分量 $\nu=0$，我们有 $A^0 = \phi/c$，因此质量项的贡献为：
$$ \frac{c^2 m_{\gamma}^2}{\mu_0 \hbar^2} A^{0} = \frac{c^2 m_{\gamma}^2}{\mu_0 \hbar^2} \frac{\phi}{c} = \frac{c m_{\gamma}^2}{\mu_0 \hbar^2} \phi $$
将所有项加在一起，得到的场方程（称为[普罗卡方程](@entry_id:753764)，Proca equation）会变为 $\partial_{\mu}F^{\mu\nu} + \frac{c^2 m_{\gamma}^2}{\hbar^2}A^{\nu} = \mu_0 J^{\nu}$。这展示了[拉格朗日形式主义](@entry_id:158185)如何系统地从一个基本假设（[拉格朗日量](@entry_id:174593)）出发，推导出场的[运动方程](@entry_id:170720)，并方便地引入新的物理效应。