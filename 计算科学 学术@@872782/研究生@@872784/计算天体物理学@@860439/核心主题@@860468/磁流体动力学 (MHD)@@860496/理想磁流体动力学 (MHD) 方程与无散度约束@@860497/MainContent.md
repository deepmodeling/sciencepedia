## 引言
磁流体动力学（MHD）是理解宇宙中从恒星到星系尺度等离子体现象的核心理论框架。其中，理想MHD模型以其简洁性成为计算模拟的基石。然而，该模型的一个核心支柱——[磁场](@entry_id:153296)[无散约束](@entry_id:755035)（$\nabla \cdot \mathbf{B} = 0$），即不存在磁单极子，给[数值模拟](@entry_id:137087)带来了巨大的挑战。尽管该约束在解析上自然成立，但在离散的计算网格上，[数值误差](@entry_id:635587)极易破坏这一条件，从而产生灾难性的非物理效应，污染模拟结果。

本文旨在系统性地阐述理想MHD方程的理论基础，并深入探讨维持[无散约束](@entry_id:755035)的各类先进数值方法。在接下来的章节中，我们将首先在“原理与机制”中从第一性原理推导理想MHD[方程组](@entry_id:193238)，并详细分析$\nabla \cdot \mathbf{B} \neq 0$ 带来的物理与数值后果。随后，在“应用与[交叉](@entry_id:147634)学科联系”中，我们将通过标准测试问题和天体物理模型，展示这些理论与方法在实际科研中的应用，并探讨其与广义相对论等领域的深刻联系。最后，“动手实践”部分将提供一系列计算练习，旨在帮助读者将理论知识转化为解决实际问题的能力。

## 原理与机制

### [理想磁流体动力学](@entry_id:198478)（MHD）[方程组](@entry_id:193238)

[理想磁流体动力学](@entry_id:198478)（MHD）是描述在特定假设下导电等离子体宏观行为的理论框架。它将流体视为连续介质，并耦合了[流体动力学](@entry_id:136788)与麦克斯韦电磁学。本节将从第一性原理出发，推导[理想磁流体动力学方程组](@entry_id:192486)，并展示其[守恒形式](@entry_id:747710)。

#### 从第一性原理到理想MHD

理想MHD模型并非基本理论，而是从更基础的[麦克斯韦方程组](@entry_id:150940)和[流体方程组](@entry_id:195729)，在适用于天体物理中大尺度、低频现象的一系列假设下简化得出的。理解这些假设对于认识该模型的适用范围和局限性至关重要 [@problem_id:3539096]。

我们从麦克斯韦方程组开始（此处及后续，若无特殊说明，均采用磁导率 $\mu_0=1$ 的单位制）：
$$ \nabla \cdot \boldsymbol{B} = 0 $$
$$ \nabla \times \boldsymbol{E} = -\frac{\partial \boldsymbol{B}}{\partial t} $$
$$ \nabla \cdot \boldsymbol{E} = \rho_e $$
$$ \nabla \times \boldsymbol{B} = \boldsymbol{J} + \frac{\partial \boldsymbol{E}}{\partial t} $$
以及单流体的质量和动量守恒方程：
$$ \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \boldsymbol{v}) = 0 $$
$$ \frac{\partial (\rho \boldsymbol{v})}{\partial t} + \nabla \cdot (\rho \boldsymbol{v}\boldsymbol{v} + p \boldsymbol{I}) = \rho_e \boldsymbol{E} + \boldsymbol{J} \times \boldsymbol{B} $$
其中 $\rho$ 是质量密度，$\boldsymbol{v}$ 是[流体速度](@entry_id:267320)， $p$ 是[热压](@entry_id:159509)强，$\boldsymbol{B}$ 和 $\boldsymbol{E}$ 分别是[磁场](@entry_id:153296)和[电场](@entry_id:194326)，$\rho_e$ 和 $\boldsymbol{J}$ 分别是[电荷密度](@entry_id:144672)和电流密度。

理想MHD的推导依赖于以下核心物理假设：

1.  **[准电中性](@entry_id:184567) (Quasi-neutrality)**：在所研究的宏观尺度上，等离子体被认为是电中性的，即净[电荷密度](@entry_id:144672) $\rho_e \approx 0$。这个假设使得[动量方程](@entry_id:197225)中的静电力项 $\rho_e \boldsymbol{E}$ 可以忽略不计。同时，[电场](@entry_id:194326)的高斯定律简化为 $\nabla \cdot \boldsymbol{E} \approx 0$。

2.  **尺度分离与非相对论极限 (Scale Separation and Non-relativistic Limit)**：我们关注的流体现象的时间尺度远大于[电磁波传播](@entry_id:272130)时间，空间尺度远大于等离子体的微观尺度（如[德拜长度](@entry_id:147934)）。这等价于一个低频、长波长的近似。在这种非相对论极限下（流速 $v \ll c$），安培定律 $\nabla \times \boldsymbol{B} = \boldsymbol{J} + \partial \boldsymbol{E} / \partial t$ 中的位移电流项 $\partial \boldsymbol{E} / \partial t$ 与传导电流项 $\boldsymbol{J}$ 相比可以忽略。其量级分析表明 $|\partial \boldsymbol{E} / \partial t | / |\boldsymbol{J}| \sim (v/c)^2$。因此，安培定律被简化为 $\nabla \times \boldsymbol{B} \approx \boldsymbol{J}$，这直接将[电流密度](@entry_id:190690)与[磁场](@entry_id:153296)的卷曲联系起来。

3.  **无限电导率 (Infinite Conductivity)**：该假设认为等离子体是完美导体，其[电阻率](@entry_id:266481) $\eta \to 0$。[广义欧姆定律](@entry_id:180191)在最简形式下为 $\boldsymbol{E} + \boldsymbol{v} \times \boldsymbol{B} = \eta \boldsymbol{J}$。在无限电导率的极限下，该定律简化为**[理想欧姆定律](@entry_id:185600)**：
    $$ \boldsymbol{E} + \boldsymbol{v} \times \boldsymbol{B} = 0 $$
    这个本构关系是闭合理想MHD[方程组](@entry_id:193238)的关键，它消除了[电场](@entry_id:194326) $\boldsymbol{E}$，使其完全由[速度场](@entry_id:271461)和[磁场](@entry_id:153296)决定。

#### 理想MHD的[守恒形式](@entry_id:747710)

将上述假设应用于基础[方程组](@entry_id:193238)，我们便可以得到理想MHD的守恒律形式，即 $\partial_t \boldsymbol{U} + \nabla \cdot \boldsymbol{F}(\boldsymbol{U}) = 0$，其中 $\boldsymbol{U}$ 是[守恒变量](@entry_id:747720)矢量，$\boldsymbol{F}$ 是通量张量。这对于发展稳定的数值求解方法（即[有限体积法](@entry_id:749372)）至关重要 [@problem_id:3539050]。

- **质量守恒**：连续性方程本身就是[守恒形式](@entry_id:747710)。
  $$ \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \boldsymbol{v}) = 0 $$

- **[动量守恒](@entry_id:149964)**：在[动量方程](@entry_id:197225)中，我们用 $\boldsymbol{J} = \nabla \times \boldsymbol{B}$ 替换电流密度。洛伦兹力项 $\boldsymbol{J} \times \boldsymbol{B}$ 在 $\nabla \cdot \boldsymbol{B} = 0$ 的条件下可以写成一个[张量的散度](@entry_id:191736)，即[麦克斯韦应力张量](@entry_id:153513)的负散度：$(\nabla \times \boldsymbol{B}) \times \boldsymbol{B} = \nabla \cdot (\frac{1}{2}B^2 \boldsymbol{I} - \boldsymbol{B}\boldsymbol{B})$。将此项移到方程左侧，[动量方程](@entry_id:197225)的[守恒形式](@entry_id:747710)为：
  $$ \frac{\partial (\rho \boldsymbol{v})}{\partial t} + \nabla \cdot \left[ \rho \boldsymbol{v}\boldsymbol{v} + \left(p + \frac{1}{2}B^2\right)\boldsymbol{I} - \boldsymbol{B}\boldsymbol{B} \right] = 0 $$
  其中 $p_{tot} = p + \frac{1}{2}B^2$ 被称为[总压](@entry_id:265293)，包含[热压](@entry_id:159509)强和[磁压](@entry_id:272413)强。

- **[磁通量守恒](@entry_id:199588) ([感应方程](@entry_id:750617))**：将[理想欧姆定律](@entry_id:185600) $\boldsymbol{E} = -\boldsymbol{v} \times \boldsymbol{B}$ 代入[法拉第感应定律](@entry_id:146175) $\partial_t \boldsymbol{B} = -\nabla \times \boldsymbol{E}$，得到[感应方程](@entry_id:750617)：
  $$ \frac{\partial \boldsymbol{B}}{\partial t} = \nabla \times (\boldsymbol{v} \times \boldsymbol{B}) $$
  这可以写成[守恒形式](@entry_id:747710) $\partial_t \boldsymbol{B} + \nabla \cdot (\boldsymbol{v}\boldsymbol{B} - \boldsymbol{B}\boldsymbol{v}) = 0$。然而，需要注意的是，从数学上严格推导此[守恒形式](@entry_id:747710)需要引入一个非守恒[源项](@entry_id:269111) $-\boldsymbol{v}(\nabla \cdot \boldsymbol{B})$ [@problem_id:3539050]。只有在 $\nabla \cdot \boldsymbol{B} = 0$ 被严格满足时，该[源项](@entry_id:269111)才为零，[感应方程](@entry_id:750617)才是纯守恒的。

- **[能量守恒](@entry_id:140514)**：总能量密度定义为动能、热能和磁能之和：$E = \frac{1}{2}\rho v^2 + \frac{p}{\gamma - 1} + \frac{1}{2}B^2$。通过对各项求时间导数并利用其他守恒律，可以推导出总能量的守恒方程 [@problem_id:3539021]：
  $$ \frac{\partial E}{\partial t} + \nabla \cdot \left[ \left(E + p + \frac{1}{2}B^2\right)\boldsymbol{v} - (\boldsymbol{B} \cdot \boldsymbol{v})\boldsymbol{B} \right] = 0 $$
  通量项包括[总焓](@entry_id:197863)流 $\left(E + p_{tot}\right)\boldsymbol{v}$ 和[坡印廷通量](@entry_id:189099)的一部分 $-(\boldsymbol{B} \cdot \boldsymbol{v})\boldsymbol{B}$。这个推导同样依赖于 $\nabla \cdot \boldsymbol{B} = 0$ 的条件。

综上，理想MHD的完整守恒[方程组](@entry_id:193238)（八波结构）为：
$$
\frac{\partial}{\partial t}
\begin{pmatrix} \rho \\ \rho\boldsymbol{v} \\ \boldsymbol{B} \\ E \end{pmatrix}
+ \nabla\cdot
\begin{pmatrix}
\rho\boldsymbol{v} \\
\rho\boldsymbol{v}\boldsymbol{v} - \boldsymbol{B}\boldsymbol{B} + (p+\frac{1}{2}B^2)\boldsymbol{I} \\
\boldsymbol{v}\boldsymbol{B} - \boldsymbol{B}\boldsymbol{v} \\
(E + p + \frac{1}{2}B^2)\boldsymbol{v} - (\boldsymbol{v}\cdot\boldsymbol{B})\boldsymbol{B}
\end{pmatrix}
= \boldsymbol{0}
$$
这个[方程组](@entry_id:193238)描述了在理想条件下等离子体的演化。在一维黎曼问题中，沿 $x$ 方向的[动量通量](@entry_id:199796)矢量 $\boldsymbol{F}_{(\rho\boldsymbol{v})}$ 由该通量张量的第一列给出 [@problem_id:3539040]：
$$
\boldsymbol{F}_{(\rho\boldsymbol{v})} = \begin{pmatrix} \rho v_x^2 + p + \frac{1}{2}B^2 - B_x^2 \\ \rho v_x v_y - B_x B_y \\ \rho v_x v_z - B_x B_z \end{pmatrix}
$$

### 散度自由约束 ($\nabla \cdot \mathbf{B} = 0$)

在MHD的理论和数值模拟中，$\nabla \cdot \mathbf{B} = 0$ 约束扮演着核心角色。它不仅是一个初始条件，其维持与否直接关系到物理的准确性和数值的稳定性。

#### 物理与解析含义

从物理上讲，$\nabla \cdot \mathbf{B} = 0$ 是对自然界中从未观测到[磁单极子](@entry_id:142817)这一事实的数学表述。[高斯磁定律](@entry_id:182942)的积分形式 $\oint_S \boldsymbol{B} \cdot d\boldsymbol{A} = 0$ 表明，穿过任何闭合[曲面](@entry_id:267450)的净[磁通量](@entry_id:268943)为零。

这个积分定律有一个重要的直接推论。考虑一个跨越两种不同介质（或一个激波）界面的无限薄的“药丸盒”[高斯面](@entry_id:272964)，可以推导出[磁场](@entry_id:153296)的法向分量在界面上必须是连续的，即 $[B_n] = \boldsymbol{n} \cdot (\boldsymbol{B}_2 - \boldsymbol{B}_1) = 0$，其中 $\boldsymbol{n}$ 是界面的[单位法向量](@entry_id:178851) [@problem_id:3539041]。这是MHD的郎金-雨贡纽跳跃关系之一。如果 $B_n$ 出现不连续，将等价于界面上存在一个磁单极子[面密度](@entry_id:161889)，其值为 $\sigma_m = [B_n] / (4\pi)$ （[高斯单位制](@entry_id:183405)）。

在一维问题中，所有物理量只依赖于一个空间坐标（例如 $x$），该约束简化为 $\partial B_x / \partial x = 0$，这意味着 $B_x$ 必须在整个空间上是均匀的。结合[感应方程](@entry_id:750617)可以进一步证明 $\partial B_x / \partial t = 0$，因此 $B_x$ 是一个时空常数 [@problem_id:3539040]。

从解析上看，理想MHD[方程组](@entry_id:193238)内在地保持了这一约束。对[感应方程](@entry_id:750617) $\partial_t \boldsymbol{B} = \nabla \times (\boldsymbol{v} \times \boldsymbol{B})$ 两边取散度，我们得到：
$$ \frac{\partial}{\partial t}(\nabla \cdot \boldsymbol{B}) = \nabla \cdot (\nabla \times (\boldsymbol{v} \times \boldsymbol{B})) $$
由于任何[旋度的散度](@entry_id:271562)恒为零，上式右边为零。因此，$\frac{\partial}{\partial t}(\nabla \cdot \boldsymbol{B}) = 0$。这意味着如果初始时刻[磁场](@entry_id:153296)是无散的，那么在解析解的演化下，它将永远保持无散 [@problem_id:3539096]。

### 数值挑战及 $\nabla \cdot \mathbf{B} \neq 0$ 的后果

尽管解析上 $\nabla \cdot \mathbf{B} = 0$ 得以保持，但在[数值离散化](@entry_id:752782)过程中，这一特性很容易被破坏。标准的[有限差分](@entry_id:167874)或有限体积方法在离散的[旋度和散度](@entry_id:269913)算子上，通常不满足“散度的旋度恒为零”这一恒等式。因此，即使初始[磁场](@entry_id:153296)是无散的，数值误差也会在每个时间步中引入非零的散度，如同在[计算网格](@entry_id:168560)中凭空制造了“**[数值磁单极子](@entry_id:752810)**”。

#### 伪力和[能量不守恒](@entry_id:276143)

这些[数值磁单极子](@entry_id:752810)的存在会带来灾难性的非物理效应。当 $\nabla \cdot \mathbf{B} \neq 0$ 时，理想MHD[方程组](@entry_id:193238)的[守恒形式](@entry_id:747710)被破坏，出现了伪源项。

在动量方程中，非零散度会引入一个与[磁场](@entry_id:153296)平行的[伪力](@entry_id:169104)。[洛伦兹力](@entry_id:145104) $\boldsymbol{J} \times \boldsymbol{B}$ 的[守恒形式](@entry_id:747710)推导依赖于 $\nabla \cdot \boldsymbol{B} = 0$。当该条件不满足时，[动量方程](@entry_id:197225)中会出现一个[源项](@entry_id:269111) [@problem_id:3539019]：
$$ \frac{\partial (\rho \boldsymbol{v})}{\partial t} + \nabla \cdot \boldsymbol{T} = \boldsymbol{B}(\nabla \cdot \boldsymbol{B}) $$
其中 $\boldsymbol{T}$ 是总应力张量。这个[源项](@entry_id:269111) $\boldsymbol{S} = \boldsymbol{B}(\nabla \cdot \boldsymbol{B})$ 会产生完全非物理的加速度，例如在一个物理力应该为零的静态平衡结构中，数值误差可能导致流体被加速到高速。

类似地，在能量方程中，$\nabla \cdot \mathbf{B} \neq 0$ 也会引入一个伪源项，破坏总能量的守恒 [@problem_id:3539021]。该源项的形式为 $-(\boldsymbol{v} \cdot \boldsymbol{B})(\nabla \cdot \boldsymbol{B})$。在一个强[磁场](@entry_id:153296)的爆炸波问题中，即使初始的散度误差很小，这个源项也可能导致总能量随时间发生显著的、非物理性的增加或减少。

#### 对称性和熵

从更深层次的数学结构来看，$\nabla \cdot \mathbf{B} = 0$ 约束是理想MHD[方程组](@entry_id:193238)具有良好数学性质（如[对称双曲性](@entry_id:755716)）的必要条件。一个可以被“熵变量”对称化的[双曲系统](@entry_id:260647)，保证了其解的良定性和[数值格式](@entry_id:752822)的稳定性。当 $\nabla \cdot \mathbf{B} \neq 0$ 时，[方程组](@entry_id:193238)中出现的非守恒[源项](@entry_id:269111)（如[感应方程](@entry_id:750617)中的 $-\boldsymbol{v}(\nabla \cdot \boldsymbol{B})$）破坏了这种对称结构。这些源项会导致一个与物理耗散无关的熵产生项，使得基于[熵稳定性](@entry_id:749023)的数值方法失效 [@problem_id:3539050]。因此，维持 $\nabla \cdot \mathbf{B} = 0$ 对确保数值解的数学鲁棒性和物理真实性至关重要。

### 维持散度自由约束的数值方法

为了克服[数值磁单极子](@entry_id:752810)问题，[计算天体物理学](@entry_id:145768)家已经发展了多种策略来在数值上控制或消除[磁场散度](@entry_id:271190)。这些方法大致可分为三类：[散度清理](@entry_id:748607)（Divergence Cleaning）、[约束输运](@entry_id:747775)（Constrained Transport）和基于磁矢势（Vector Potential）的方法。

#### [散度清理](@entry_id:748607)方案

这类方法允许 $\nabla \cdot \mathbf{B}$ 在数值上产生，但会引入额外的机制来主动地将其移除或传播出计算区域。

- **Powell八波格式 (Powell's 8-Wave Formulation)**：这是最简单的一种清理方法。它通过在动量、感应和能量方程中系统地保留由 $\nabla \cdot \mathbf{B}$ 产生的非守恒[源项](@entry_id:269111)，将完整的理想MHD[方程组](@entry_id:193238)写成一个8变量（$\rho, \rho\boldsymbol{v}, \boldsymbol{B}, E$）的非守恒[双曲系统](@entry_id:260647)。该系统的一个关键特性是，其特征结构中包含一个以流体速度 $v_n$ 传播的“散度波”。这意味着磁散度误差会随着流体一起平动，而不是在原地累积。然而，这种[平动](@entry_id:187700)本身并不会减少散度的总量 [@problem_id:3539044]。

- **广义拉格朗日乘子法 (GLM)**：GLM方法更为复杂和有效。它引入一个辅助[标量场](@entry_id:151443) $\psi$，并修改[感应方程](@entry_id:750617)和增加一个关于 $\psi$ 的[演化方程](@entry_id:268137)。这个扩展后的9变量系统被设计成具有一对新的特征波，称为“清理波”，它们以预设的速度 $\pm c_h$ 传播。这些[波能](@entry_id:164626)将散度误差以波的形式传出计算区域。通过在 $\psi$ 的[演化方程](@entry_id:268137)中加入一个衰减项，还可以实现对散度误差的耗散。GLM方法的一个显著特点是，清理波的速度 $\pm c_h$ 是在实验室（网格）[参考系](@entry_id:169232)下定义的，与[流体速度](@entry_id:267320)无关，这使得清理更加高效。然而，这也给CFL时间步长带来了额外的限制，$\Delta t$ 必须小于由 $c_h$ 决定的时间尺度 [@problem_id:3539044]。

#### [约束输运](@entry_id:747775)（CT）方案

[约束输运](@entry_id:747775)（CT）方法是一种几何方法，它从根本上防止[数值磁单极子](@entry_id:752810)的产生。其核心思想是采用交错网格，并将[磁场](@entry_id:153296)表示为穿过网格单元面的磁通量。

CT方法利用[法拉第定律](@entry_id:149836)的积分形式（[斯托克斯定理](@entry_id:264534)），$\frac{d}{dt}\int_S \boldsymbol{B}\cdot d\boldsymbol{A} = -\oint_{\partial S} \boldsymbol{E}\cdot d\boldsymbol{l}$。在离散层面，它将定义在单元面（face）上的磁通量的时间更新，与定义在单元边（edge）上的[电动势](@entry_id:203175)（EMF）的[环路积分](@entry_id:164828)联系起来。例如，在一个二维网格中，一个面的通量更新由其两个[边界点](@entry_id:176493)上的[电动势](@entry_id:203175)之差决定 [@problem_id:3539100]。

关键在于，如果每个边上的[电动势](@entry_id:203175)是单值的，并被所有共享该边的面一致地使用，那么可以从数学上证明，围绕任何一个网格单元的所有面的[磁通量](@entry_id:268943)之和（即离散散度）的时间导数恒为零。这意味着，如果初始[磁场](@entry_id:153296)的离散散度为零，那么在整个演化过程中，它将保持为零，直至[机器精度](@entry_id:756332)。CT方法因此能够从结构上保证 $\nabla \cdot \mathbf{B}=0$ [@problem_id:3539041]。这种方法的实现相对复杂，尤其是在非结构网格或[自适应网格](@entry_id:164379)（AMR）上，但其鲁棒性使其成为许多现代MHD代码的首选。

#### 磁矢势（A）方法

另一种从根本上保证 $\nabla \cdot \mathbf{B} = 0$ 的方法是直接演化[磁矢势](@entry_id:141246) $\boldsymbol{A}$，并通过 $\boldsymbol{B} = \nabla \times \boldsymbol{A}$ 来定义[磁场](@entry_id:153296)。由于[旋度的散度](@entry_id:271562)恒为零，这种定义自动满足了散度约束 [@problem_id:3539046]。

然而，这种方法引入了新的复杂性：**规范自由度 (Gauge Freedom)**。演化方程 $\partial_t \boldsymbol{A} = \boldsymbol{v} \times \boldsymbol{B} - \nabla\phi$ 中包含一个未定的标量[规范势](@entry_id:188985) $\phi$。不同的规范选择会影响 $\boldsymbol{A}$ 的非物理（无旋）部分的演化：
- **韦尔规范 (Weyl Gauge, $\phi=0$)**：这是最简单的选择，但它导致规范扰动（即 $\nabla \cdot \boldsymbol{A}$ 的误差）的[特征速度](@entry_id:165394)为零。这意味着规范误差不会传播，而是通过[数值耗散](@entry_id:168584)缓[慢扩散](@entry_id:161635)，并可能在[自适应网格](@entry_id:164379)的粗细网格界面等地方累积，造成问题。
- **[洛伦兹规范](@entry_id:153650) (Lorenz Gauge, $\nabla \cdot \boldsymbol{A} + c_h^{-2} \partial_t \phi = 0$)**：这种选择使得规范自由度以速度 $c_h$ 进行双曲传播，形成一个波方程。这有助于将规范[误差传播](@entry_id:147381)出感兴趣的区域，改善了与[AMR](@entry_id:204220)的兼容性。其代价是引入了基于 $c_h$ 的CFL[时间步长限制](@entry_id:756010)。
- **[库仑规范](@entry_id:273044) (Coulomb Gauge, $\nabla \cdot \boldsymbol{A} = 0$)**：这个规范在每个时间步都强制 $\nabla \cdot \boldsymbol{A}$ 为零。这需要求解一个关于 $\phi$ 的全局[泊松方程](@entry_id:143763)，计算成本非常高昂，且需要合适的边界条件。

因此，演化[磁矢势](@entry_id:141246) $\boldsymbol{A}$ 的方法虽然能完美保持 $\nabla \cdot \mathbf{B} = 0$，但必须仔细处理规范选择及其带来的数值挑战 [@problem_id:3539046]。

### 背景与对比：电阻MHD

为了更好地理解理想MHD的“理想”之处，有必要与**电阻MHD (Resistive MHD)**进行对比。在电阻MHD中，我们考虑一个有限的、非零的[电阻率](@entry_id:266481) $\eta > 0$。

#### 磁流守恒的破坏与[磁重联](@entry_id:188309)

当 $\eta > 0$ 时，[理想欧姆定律](@entry_id:185600)不再成立。[感应方程](@entry_id:750617)变为 [@problem_id:3539115]：
$$ \frac{\partial \boldsymbol{B}}{\partial t} = \nabla \times (\boldsymbol{v} \times \boldsymbol{B}) - \frac{\eta}{\mu_0} \nabla \times (\nabla \times \boldsymbol{B}) $$
与理想情况相比，方程中多出了一项**[磁扩散](@entry_id:187718)项**。在 $\nabla \cdot \boldsymbol{B} = 0$ 的条件下，该项可以写成 $\frac{\eta}{\mu_0}\nabla^2\boldsymbol{B}$。正是这个[扩散](@entry_id:141445)项，使得[磁场](@entry_id:153296)线可以不再“冻结”在流体中，而是能够相[对流](@entry_id:141806)体发生滑移和[扩散](@entry_id:141445)。这打破了**磁流守恒 (Flux Freezing)**，并允许[磁场](@entry_id:153296)拓扑结构发生改变。这一过程被称为**[磁重联](@entry_id:188309) (Magnetic Reconnection)**，它是[太阳耀斑](@entry_id:204045)、[天体物理喷流](@entry_id:266808)等高能现象中的关键物理机制。

此外，电阻的存在意味着能量耗散。总[磁能](@entry_id:268850)的演化方程中会出现一个负定的耗散项 [@problem_id:3539115]：
$$ \frac{dE_B}{dt} = \dots - \eta \int_V \boldsymbol{J}^2 dV $$
这个项代表了[磁能](@entry_id:268850)通过[欧姆加热](@entry_id:190028)（或[焦耳加热](@entry_id:190028)）不可逆地转化为等离子体的内能。

#### 数值重联

一个重要的概念是，即使在模拟理想MHD（即程序中设置 $\eta=0$）时，由于离散化带来的截断误差，数值解中也可能出现类似[磁重联](@entry_id:188309)的现象。这种由[数值误差](@entry_id:635587)引起的耗散被称为**数值[电阻率](@entry_id:266481) (Numerical Resistivity)**。对于一个设计良好的一致性数值格式，当网格分辨率提高时，截断误差会减小，因此数值电阻率和数值重联的速率也应该趋向于零 [@problem_id:3539115]。

最后需要强调的是，严格执行 $\nabla \cdot \mathbf{B} = 0$ 约束的数值方法，并不会阻止**物理**重联的发生。当 $\eta > 0$ 时，重联是物理上允许的，而保持 $\nabla \cdot \mathbf{B} = 0$ 只是确保了这个物理过程是在没有[磁单极子](@entry_id:142817)污染的正确背景下被模拟。在理想MHD的模拟中，保持该约束则是为了最小化非物理的数值重联。