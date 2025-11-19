## 引言
在物理学中，理解一个系统的能量与动量是描述其动力学行为的核心。当我们将这一问题置于爱因斯坦的狭义相对论框架下时，能量和动量不再是孤立的概念，而是统一的[四维动量](@entry_id:272346)向量的不同分量。对于弥散于整个空间的[电磁场](@entry_id:265881)，我们如何描述其能量和动量的[分布](@entry_id:182848)与流动呢？这一问题引出了一个至关重要的数学和物理对象：[电磁应力-能量张量](@entry_id:267456)$T^{\mu\nu}$。它不仅解决了在相对论框架下统一描述场能量、动量和[内应力](@entry_id:193721)的难题，更成为连接电磁学、相对论和[引力](@entry_id:175476)理论的基石。

本文旨在系统地剖析[电磁应力-能量张量](@entry_id:267456)。在接下来的章节中，您将学习到：

- **第一章：原理与机制** 将从第一性原理出发，构建[电磁应力-能量张量](@entry_id:267456)的[协变](@entry_id:634097)形式，深入阐释其各个分量（能量密度、能量通量、[动量密度](@entry_id:271360)和[麦克斯韦应力](@entry_id:199347)）的明确物理意义，并推导其核心的动力学方程——[守恒定律](@entry_id:269268)。

- **第二章：应用和跨学科联系** 将展示该张量在解决实际物理问题中的强大威力，从计算导体间的[电磁力](@entry_id:196024)，到揭示电路中[能量流](@entry_id:142770)动的真实图景，再到它作为[引力源](@entry_id:271552)在广义相对论和宇宙学中的深刻应用。

- **第三章：动手实践** 将通过一系列精心设计的问题，引导您亲手计算张量的分量、应用[守恒定律](@entry_id:269268)，将抽象的理论转化为具体的物理洞察。

通过这趟学习之旅，您将掌握一个不仅在形式上优美，而且在物理上极其深刻的工具，它揭示了[电磁场](@entry_id:265881)作为一个携带能量、动量和应力的动力学实体的本质。

## 原理与机制

在[狭义相对论](@entry_id:275552)的框架下，描述一个物理系统的能量和动量分布需要一个统一的数学对象。[电磁场](@entry_id:265881)的能量和动量也不例外。[电磁应力-能量张量](@entry_id:267456) $T^{\mu\nu}$ 正是这样一个核心工具，它以一种[协变](@entry_id:634097)的形式，将[电磁场](@entry_id:265881)的能量密度、[动量密度](@entry_id:271360)、能量通量以及[动量通量](@entry_id:199796)（即应力）封装在一个单一的四维张量中。本章将深入探讨该张量的定义、其各个分量的物理意义、所遵循的[守恒定律](@entry_id:269268)，以及它的一些基本性质。

### [电磁应力-能量张量](@entry_id:267456)的协变定义

构建[电磁应力-能量张量](@entry_id:267456)的基础是[电磁场张量](@entry_id:158921) $F^{\mu\nu}$。由于 $F^{\mu\nu}$ 本身是规范不变的（即在[四维势](@entry_id:188407) $A^\mu \to A^\mu + \partial^\mu \Lambda$ 的变换下不变），任何由 $F^{\mu\nu}$ 构建的物理量也都自然地继承了这一优良特性。[电磁应力-能量张量](@entry_id:267456) $T^{\mu\nu}$ 必须是一个对称的[二阶张量](@entry_id:199780)，它完全由[场张量](@entry_id:186486) $F^{\mu\nu}$ 和[时空度规](@entry_id:202650) $\eta_{\mu\nu}$ 构成。

在本章中，我们采用闵可夫斯基时空的度规符号为 $(+,-,-,-)$，即 $\eta_{\mu\nu} = \text{diag}(1, -1, -1, -1)$。在此约定下，自由[电磁场](@entry_id:265881)的对称、规范不变的应力-能量张量的[标准形式](@entry_id:153058)为：

$$
T^{\mu\nu} = \frac{1}{\mu_0} \left( -F^{\mu\alpha}F^{\nu}{}_{\alpha} + \frac{1}{4}\eta^{\mu\nu} F_{\alpha\beta}F^{\alpha\beta} \right)
$$

其中 $\mu_0$ 是[真空磁导率](@entry_id:186031)，爱因斯坦求和约定在此适用。$F^{\nu}{}_{\alpha}$ 是通过度规降低指标得到的混合指标张量，即 $F^{\nu}{}_{\alpha} = \eta_{\alpha\beta}F^{\nu\beta}$。这个表达式可以通过对[电磁场的拉格朗日量](@entry_id:198927)密度 $\mathcal{L} = -\frac{1}{4\mu_0}F_{\alpha\beta}F^{\alpha\beta}$ 关于度规 $g^{\mu\nu}$ 进行变分得到，这确保了它在广义相对论中能够作为[引力场](@entry_id:169425)的正确源。[@problem_id:1876832]

从这个定义可以直接看出几个重要属性。首先，张量显然是对称的，即 $T^{\mu\nu} = T^{\nu\mu}$。这一点至关重要，因为它在广义相对论中与对称的爱因斯坦张量相耦合。其次，它只依赖于 $F^{\mu\nu}$，因此是规范不变的。

### 张量分量的物理诠释

为了理解 $T^{\mu\nu}$ 的物理内容，最有效的方法是将其分量与我们熟悉的三维物理量（如[电场](@entry_id:194326) $\vec{E}$ 和[磁场](@entry_id:153296) $\vec{B}$）联系起来。我们使用标准的对应关系（在 SI 单位制和 $c=1$ 的自然单位制下有所不同，这里我们以 SI 为主）：

$$
F^{\mu\nu} = 
\begin{pmatrix}
0  & -E_x/c  & -E_y/c  & -E_z/c \\
E_x/c  & 0  & -B_z  & B_y \\
E_y/c  & B_z  & 0  & -B_x \\
E_z/c  & -B_y  & B_x  & 0
\end{pmatrix}
$$

通过计算 $T^{\mu\nu}$ 的各个分量，我们可以揭示其物理内涵。

#### $T^{00}$：能量密度

$T^{00}$ 分量代表了[电磁场](@entry_id:265881)的能量密度。让我们来显式计算它。根据定义：

$$
T^{00} = \frac{1}{\mu_0} \left( -F^{0\alpha}F^{0}{}_{\alpha} + \frac{1}{4}\eta^{00} F_{\alpha\beta}F^{\alpha\beta} \right)
$$

首先计算第一项。由于 $F^{00}=0$，求和只涉及空间分量 $\alpha = i \in \{1,2,3\}$。我们有 $F^{0}{}_{i} = \eta_{i\beta}F^{0\beta} = \eta_{ii}F^{0i} = -F^{0i}$。因此：
$$
-F^{0\alpha}F^{0}{}_{\alpha} = -F^{0i}F^{0}{}_{i} = -F^{0i}(-F^{0i}) = \sum_{i=1}^3 (F^{0i})^2 = \sum_{i=1}^3 (-E_i/c)^2 = \frac{E^2}{c^2}
$$

接下来计算[标量不变量](@entry_id:193787) $F_{\alpha\beta}F^{\alpha\beta}$。它可以分解为：
$$
F_{\alpha\beta}F^{\alpha\beta} = 2 \left( B^2 - \frac{E^2}{c^2} \right)
$$

将这两部分代入 $T^{00}$ 的表达式，并利用 $\eta^{00}=1$：
$$
T^{00} = \frac{1}{\mu_0} \left( \frac{E^2}{c^2} + \frac{1}{4} \cdot 1 \cdot 2\left(B^2 - \frac{E^2}{c^2}\right) \right) = \frac{1}{\mu_0} \left( \frac{1}{2}\frac{E^2}{c^2} + \frac{1}{2}B^2 \right)
$$

最后，利用关系式 $c^2 = 1/(\epsilon_0\mu_0)$，我们得到：
$$
T^{00} = \frac{1}{2\mu_0} \left(\epsilon_0\mu_0 E^2 + B^2 \right) = \frac{1}{2}\epsilon_0 E^2 + \frac{1}{2\mu_0} B^2
$$

这个结果正是我们所熟知的[电磁场能量](@entry_id:265463)密度 $u_{EM}$。因此，$T^{00} = u_{EM}$。[@problem_id:1876892]

#### $T^{0i}$ 与 $T^{i0}$：能量通量与[动量密度](@entry_id:271360)

$T^{\mu\nu}$ 的时空混合分量 $T^{0i}$ 和 $T^{i0}$ 描述了能量和动量的流动。
- $T^{0i}$ 代表沿 $i$ 方向的能量通量（单位时间通过单位面积的能量）除以 $c$。
- $T^{i0}$ 代表[电磁场](@entry_id:265881)第 $i$ 个动量分量的密度。

由于[张量的对称性](@entry_id:202126)，$T^{0i} = T^{i0}$。这揭示了一个深刻的相对论性结论：能量通量与[动量密度](@entry_id:271360)成正比。

让我们计算 $T^{0i}$ (其中 $i \in \{1,2,3\}$)。由于 $\eta^{0i}=0$，我们只需计算第一项：
$$
T^{0i} = -\frac{1}{\mu_0} F^{0\alpha}F^{i}{}_{\alpha} = -\frac{1}{\mu_0} (F^{00}F^{i}{}_{0} + F^{0k}F^{i}{}_{k})
$$
其中 $k \in \{1,2,3\}$。我们有 $F^{00}=0$，$F^{0k} = -E_k/c$，以及 $F^{i}{}_{k} = \eta_{k\beta}F^{i\beta} = \eta_{kj}F^{ij} = -F^{ik}$。代入后得到：
$$
T^{0i} = -\frac{1}{\mu_0} \left( F^{0k}(-F^{ik}) \right) = \frac{1}{\mu_0} F^{0k}F^{ik}
$$
利用 $F^{ik} = -\epsilon^{ikm}B_m$ (其中 $\epsilon^{ikm}$ 是三维 Levi-Civita 符号)，我们有：
$$
T^{0i} = \frac{1}{\mu_0} \left(-\frac{E_k}{c}\right) \left(-\epsilon^{ikm}B_m\right) = \frac{1}{c\mu_0} \epsilon^{ikm}E_k B_m = \frac{1}{c\mu_0} (\vec{E} \times \vec{B})_i
$$
我们知道坡印亭矢量 (Poynting vector) $\vec{S} = \frac{1}{\mu_0}(\vec{E} \times \vec{B})$ 描述了[电磁场](@entry_id:265881)的[能量通量](@entry_id:266056)。因此，我们得到关系：
$$
T^{0i} = \frac{S_i}{c}
$$
由于对称性，$T^{i0} = S_i/c$。这表明[电磁动量](@entry_id:268129)密度 $\vec{g}$ 为 $\vec{g} = \vec{S}/c^2$。这个问题中的计算 [@problem_id:1548633] 阐明了 $T^{i0}$ 分量与坡印亭矢量的直接联系。

作为一个具体例子，考虑一个以恒定速度 $\vec{v}$ 运动的点电荷。通过计算其产生的电场和磁场，我们可以求出特定时空点的 $T^{0i}$ 分量，从而得到该点处[能量流](@entry_id:142770)动的具体数值 [@problem_id:1876838]。

#### $T^{ij}$：[麦克斯韦应力张量](@entry_id:153513)

$T^{\mu\nu}$ 的纯空间分量 $T^{ij}$（其中 $i,j \in \{1,2,3\}$）构成了三维的[麦克斯韦应力张量](@entry_id:153513)。它描述了动量通量：$T^{ij}$ 是第 $i$ 个动量分量沿 $j$ 方向的通量。根据[牛顿第二定律](@entry_id:274217)，动量的通量就是力，因此 $T^{ij}$ 可以被诠释为作用在垂直于 $j$ 轴的单位面积上的力的第 $i$ 个分量。

- 对角分量 $T^{ii}$ (无求和) 代表法向应力，即作用在垂直于 $i$ 轴的表面上的压力（如果为正）或张力（如果为负）。[@problem_id:1838919]
- 非对角分量 $T^{ij}$ ($i \neq j$) 代表切向应力，即剪应力。[@problem_id:1876847]

让我们显式地计算 $T^{ij}$：
$$
T^{ij} = \frac{1}{\mu_0} \left( -F^{i\alpha}F^{j}{}_{\alpha} + \frac{1}{4}\eta^{ij} F_{\alpha\beta}F^{\alpha\beta} \right)
$$
第一项可以分解为 $F^{i\alpha}F^{j}{}_{\alpha} = F^{i0}F^{j}{}_{0} + F^{ik}F^{j}{}_{k}$。
利用 $F^{i0}=E_i/c$, $F^j{}_0=E_j/c$ 以及 $F^j{}_k=-F^{jk}$，我们有：
$$
F^{i0}F^{j}{}_{0} = (E_i/c)(E_j/c) = \frac{E_i E_j}{c^2}
$$
$$
F^{ik}F^{j}{}_{k} = -F^{ik}F^{jk} = -(-\epsilon^{ikm}B_m)(-\epsilon^{jkn}B_n) = -(\delta^{ij}\delta^{mn} - \delta^{in}\delta^{jm})B_m B_n = -\delta^{ij}B^2 + B_i B_j
$$
所以，$-F^{i\alpha}F^{j}{}_{\alpha} = -(\frac{E_i E_j}{c^2} + B_i B_j - \delta^{ij}B^2)$。

第二项为 $\frac{1}{4}\eta^{ij} F_{\alpha\beta}F^{\alpha\beta} = \frac{1}{4}(-\delta^{ij}) \cdot 2(B^2 - E^2/c^2) = -\frac{1}{2}\delta^{ij}(B^2 - E^2/c^2)$。

合并两项并利用 $1/(\mu_0 c^2) = \epsilon_0$：
$$
\begin{align*}
T^{ij}  &= \frac{1}{\mu_0} \left[ -\frac{E_i E_j}{c^2} - B_i B_j + \delta^{ij}B^2 - \frac{1}{2}\delta^{ij}B^2 + \frac{1}{2}\delta^{ij}\frac{E^2}{c^2} \right] \\
 &= \frac{1}{\mu_0} \left[ -\frac{E_i E_j}{c^2} - B_i B_j + \frac{1}{2}\delta^{ij}B^2 + \frac{1}{2}\delta^{ij}\frac{E^2}{c^2} \right] \\
 &= -\epsilon_0\left(E_i E_j - \frac{1}{2}\delta_{ij}E^2\right) - \frac{1}{\mu_0}\left(B_i B_j - \frac{1}{2}\delta_{ij}B^2\right)
\end{align*}
$$
这个表达式除了一个整体负号外，与传统定义的[麦克斯韦应力张量](@entry_id:153513) $T^{\text{M}}_{ij} = \epsilon_0(E_i E_j - \frac{1}{2}\delta_{ij}E^2) + \frac{1}{\mu_0}(B_i B_j - \frac{1}{2}\delta_{ij}B^2)$ 形式相同。这个负号源于我们对 $T^{ij}$ 的定义，它代表“流出”一个体积元的[动量通量](@entry_id:199796)。因此，作用在[体积元](@entry_id:267802)上的力是[应力张量](@entry_id:148973)散度的负值。我们确认，$T^{ij}$ 确实是三维[麦克斯韦应力张量](@entry_id:153513)在四维时空中的自然推广。[@problem_id:1876866]

### [守恒定律](@entry_id:269268)及其物理意义

应力-能量张量的核心动力学意义体现在它的[守恒定律](@entry_id:269268)中。这个定律描述了[电磁场](@entry_id:265881)与带电物质之间能量和动量的交换。完整的守恒方程为：
$$
\partial_\mu T^{\mu\nu} = -f^\nu_{L}
$$
其中 $\partial_\mu = (\frac{1}{c}\frac{\partial}{\partial t}, \nabla)$ 是四维[梯度算子](@entry_id:275922)，$f^\nu_{L} = F^{\nu\alpha}J_\alpha$ 是[洛伦兹力](@entry_id:145104)的[四维力](@entry_id:273918)密度，$J_\alpha$ 是[四维电流密度](@entry_id:262568)。方程右侧表示场将四维动量转移给物质的速率。[@problem_id:1876838]

#### 无源区域 ($J_\alpha = 0$)

在没有[电荷](@entry_id:275494)和电流的区域，[守恒定律](@entry_id:269268)简化为 $\partial_\mu T^{\mu\nu} = 0$。这是一个四维的[连续性方程](@entry_id:195013)，包含了[能量守恒](@entry_id:140514)和[动量守恒](@entry_id:149964)。

- **[能量守恒](@entry_id:140514) ($\nu=0$):**
  取 $\nu=0$ 分量，我们有 $\partial_\mu T^{\mu 0} = \partial_0 T^{00} + \partial_i T^{i0} = 0$。代入 $T^{00} = u_{EM}$ 和 $T^{i0}=S_i/c$，得到：
  $$
  \frac{1}{c}\frac{\partial u_{EM}}{\partial t} + \frac{1}{c}\nabla \cdot \vec{S} = 0 \implies \frac{\partial u_{EM}}{\partial t} + \nabla \cdot \vec{S} = 0
  $$
  这正是真空中的坡印亭定理，它表明在一个体积内[电磁场能量](@entry_id:265463)的变化率等于通过该体积边界流入的[能量通量](@entry_id:266056)。[@problem_id:1876861]

- **[动量守恒](@entry_id:149964) ($\nu=j$):**
  取空间分量 $\nu=j$，我们有 $\partial_\mu T^{\mu j} = \partial_0 T^{j0} + \partial_i T^{ij} = 0$。代入动量密度 $g_j = T^{j0}/c = S_j/c^2$ 和应力张量 $T^{ij}$，得到：
  $$
  \frac{\partial g_j}{\partial t} + \partial_i T^{ij} = 0
  $$
  这个方程表明，[场动量密度](@entry_id:189791)的变化率等于流入的[动量通量](@entry_id:199796)，即[电磁场](@entry_id:265881)自身的动量是守恒的。

#### 有源区域 ($J_\alpha \neq 0$)

当存在[电荷](@entry_id:275494)和电流时，场与物质之间发生能量和动量交换。

- **能量交换 ($\nu=0$):**
  方程为 $\partial_\mu T^{\mu 0} = -F^{0\alpha}J_\alpha$。右侧可以计算为 $-F^{0i}J_i = -(-E_i/c)(-J_i) = -\frac{1}{c}\vec{E}\cdot\vec{J}$ (其中 $J_i=-J^i$ for $i=1,2,3$)。于是[守恒定律](@entry_id:269268)变为：
  $$
  \frac{\partial u_{EM}}{\partial t} + \nabla \cdot \vec{S} = -\vec{E}\cdot\vec{J}
  $$
  这是包含源项的完整坡印亭定理。右侧 $-\vec{E}\cdot\vec{J}$ 代表[电磁场](@entry_id:265881)对电流做功的[功率密度](@entry_id:194407)，即能量从场转移到物质的速率。

- **动量交换 ($\nu=j$):**
  方程为 $\partial_\mu T^{\mu j} = -F^{j\alpha}J_\alpha$。右侧 $-F^{j\alpha}J_\alpha$ 正是作用在[电荷](@entry_id:275494)上的洛伦兹力密度的负值，即 $-(\rho\vec{E} + \vec{J}\times\vec{B})_j$。因此：
  $$
  \frac{\partial g_j}{\partial t} + \partial_i T^{ij} = -f_j
  $$
  这个方程可以改写为 $\partial_i T^{ij} = -f_j - \frac{\partial g_j}{\partial t}$。它表明，作用在物质上的力密度 $f_j$ 等于[场动量](@entry_id:267786)的时间变化率与动量流出该区域的速率之和的负值。在静态情况下（$\frac{\partial}{\partial t}=0$），这简化为 $\partial_i T^{ij} = -f_j$。这意味着我们可以通过计算[麦克斯韦应力张量](@entry_id:153513)的散度来求得电磁力 [@problem_id:407600]。

### 张量的性质

#### 对称性

如前所述，$T^{\mu\nu}$ 的对称性 $T^{\mu\nu}=T^{\nu\mu}$ 是其定义的一个直接推论。例如，可以直接计算 $T^{12}$ 和 $T^{21}$ 并验证它们相等 [@problem_id:1876847]。这个性质不仅确保了角动量的守恒，在广义相对论中也是必不可少的，因为[引力场](@entry_id:169425)（由度规张量 $g_{\mu\nu}$ 描述）只能与对称的能量-动量源耦合。

#### 迹

[应力-能量张量](@entry_id:146544)的迹 $T^\mu_\mu = \eta_{\mu\nu}T^{\mu\nu}$ 是一个重要的[不变量](@entry_id:148850)。让我们计算它：
$$
T^\mu_\mu = \eta_{\mu\nu} T^{\mu\nu} = \frac{1}{\mu_0} \eta_{\mu\nu} \left( -F^{\mu\alpha}F^{\nu}{}_{\alpha} + \frac{1}{4}\eta^{\mu\nu} F_{\alpha\beta}F^{\alpha\beta} \right)
$$
$$
T^\mu_\mu = \frac{1}{\mu_0} \left( -F^{\mu\alpha}F_{\mu\alpha} + \frac{1}{4}(\eta_{\mu\nu}\eta^{\mu\nu}) F_{\alpha\beta}F^{\alpha\beta} \right)
$$
由于 $F^{\mu\alpha}F_{\mu\alpha} = F_{\alpha\beta}F^{\alpha\beta}$，以及 $\eta_{\mu\nu}\eta^{\mu\nu} = \delta^\mu_\mu = d$（时空的维度），我们得到：
$$
T^\mu_\mu = \frac{1}{\mu_0} \left( -F_{\alpha\beta}F^{\alpha\beta} + \frac{d}{4} F_{\alpha\beta}F^{\alpha\beta} \right) = \frac{d-4}{4\mu_0} F_{\alpha\beta}F^{\alpha\beta}
$$
这个结果 [@problem_id:407561] 揭示了一个非凡的性质：在四维时空（$d=4$）中，[电磁应力-能量张量](@entry_id:267456)的迹恒为零：
$$
T^\mu_\mu = 0
$$
这个性质称为**迹为零** (tracelessness)。它根植于经典电磁理论的**[共形不变性](@entry_id:191867)** (conformal invariance)。这意味着电磁作用在尺度变换下保持不变，这在更高级的[场论](@entry_id:155241)和[弦理论](@entry_id:145688)中具有深远的意义。