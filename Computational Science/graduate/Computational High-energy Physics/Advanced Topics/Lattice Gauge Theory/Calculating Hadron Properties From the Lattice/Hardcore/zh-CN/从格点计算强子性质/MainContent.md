## 引言
量子色动力学（QCD）是描述夸克和胶子之间[强相互作用](@entry_id:159198)的基本理论，它成功地解释了高能区的物理现象。然而，在低能区，强相互作用的[耦合强度](@entry_id:275517)变得非常大，导致微扰论失效。这使得从第一性原理出发理解[强子](@entry_id:158325)（如质子、中子、介子）的质量、内部结构以及它们之间的相互作用成为[理论物理学](@entry_id:154070)中的一个核心挑战。[格点量子色动力学](@entry_id:143754)（Lattice QCD）正是为了解决这一难题而发展的最成功的非微扰数值方法，它通过将时空离散化，使得在计算机上进行大规模[数值模拟](@entry_id:137087)成为可能。

本文旨在系统地阐述如何利用[格点QCD](@entry_id:143754)来计算[强子](@entry_id:158325)的各种物理属性。我们将从理论基础出发，逐步深入到具体的计算技术和前沿应用，揭示理论与实际计算之间的紧密联系。通过学习本文，读者将能够理解格点计算的完[整流](@entry_id:197363)程，从构建理论框架到最终获得与实验可比的物理结果。

文章的结构如下：第一章“**原理和机制**”将奠定理论基础，详细介绍如何在离散格点上构建一个保持规范不变性的QCD理论，如何处理格点上的[费米子](@entry_id:146235)，以及如何从欧几里得时空的关联函数中提取[强子质量](@entry_id:204733)和[矩阵元](@entry_id:186505)等物理信息。我们还将讨论如何系统地分析和控制离散化等系统误差。第二章“**应用与跨学科交叉**”将展示这些方法的强大威力，通过一系列实例，如[强子谱学](@entry_id:155019)、[形状因子](@entry_id:152312)计算、强子间相互作用研究，以及对基本对称性的探索，说明[格点QCD](@entry_id:143754)如何在[核物理](@entry_id:136661)和粒子物理等领域中发挥关键作用。最后，第三章“**动手实践**”提供了一系列具体的计算练习，旨在帮助读者将理论知识转化为实践技能，加深对核心计算步骤的理解。

## 原理和机制

### 从连续理论到格点：规范不变性的构建

量子色动力学（QCD）的格点表述通过将连续的[闵可夫斯基时空](@entry_id:156421)替换为欧几里得时空的离散格点，为研究强相互作用的非微扰特性提供了一个第一性原理的数值计算框架。这一转变的核心挑战在于如何在离散化的时空上保持理论的[局域规范不变性](@entry_id:154219)。在连续理论中，规范不变性由[规范场](@entry_id:159627) $A_\mu(x)$ 的[协变导数](@entry_id:152476)保证。在格点上，这一角色由定义在相邻格点之间的**连结变量（link variables）** $U_\mu(x)$ 扮演。

一个连结变量 $U_\mu(x)$ 是一个属于[规范群](@entry_id:144761)（对QCD而言是 $SU(3)$）的矩阵，它连接了格点 $x$ 与其在 $\mu$ 方向上的邻居 $x+a\hat\mu$，其中 $a$ 是格点间距。连结变量可以被理解为[平行输运](@entry_id:160671)算符，它将信息从一个格点以规范[协变](@entry_id:634097)的方式输运到另一个格点。它与连续规范场 $A_\mu(x)$ 的关系通过路径排序指数（path-ordered exponential）给出 ：
$$
U_\mu(x) = \mathcal{P}\exp\left( i g \int_{x}^{x+a\hat\mu} A_\nu(y) dy^\nu \right) \approx \mathcal{P}\exp\left( i g \int_{0}^{a} ds\; A_\mu(x+s\hat\mu) \right)
$$
其中 $g$ 是规范耦合常数。在朴素[连续极限](@entry_id:162780) $a \to 0$ 下，该表达式可以展开为：
$$
U_\mu(x) = \mathbf{1} + igaA_\mu(x) + \mathcal{O}(a^2)
$$
这揭示了连结变量与连续规范场之间的直接联系。

在局域[规范变换](@entry_id:176521) $\Omega(x) \in SU(3)$ 下，夸克场 $\psi(x)$ 的变换规则为 $\psi(x) \to \Omega(x)\psi(x)$。为了使描述夸克在格点间“跳跃”的项 $\bar\psi(x)U_\mu(x)\psi(x+a\hat\mu)$ 保持不变，连结变量必须按下述方式变换：
$$
U_\mu(x) \longrightarrow \Omega(x) U_\mu(x) \Omega^\dagger(x+a\hat\mu)
$$
这个变换规则确保了 $\bar\psi'(x)U'_\mu(x)\psi'(x+a\hat\mu) = \bar\psi(x)\Omega^\dagger(x) \left(\Omega(x) U_\mu(x) \Omega^\dagger(x+a\hat\mu)\right) \Omega(x+a\hat\mu)\psi(x+a\hat\mu) = \bar\psi(x)U_\mu(x)\psi(x+a\hat\mu)$，从而在[费米子](@entry_id:146235)动力学中实现了[局域规范不变性](@entry_id:154219)。

纯规范理论的[拉格朗日量](@entry_id:174593)，即杨-米尔斯作用量，在格点上通过威尔逊（Wilson）提出的由连结变量构成的闭合环路来构造。单个连结变量的迹 $\mathrm{Tr}\,U_\mu(x)$ 并非规范不变的，因为它在变换下会变为 $\mathrm{Tr}\left(U_\mu(x)\Omega^\dagger(x+a\hat\mu)\Omega(x)\right)$。然而，任何闭合环路的迹都是规范不变的。最简单的非平庸闭合环路是**平头钉（plaquette）**，它是由同一平面内四个连结变量构成的 $1 \times 1$ 小方块：
$$
U_{\mu\nu}(x) = U_\mu(x) U_\nu(x+a\hat\mu) U_\mu^\dagger(x+a\hat\nu) U_\nu^\dagger(x)
$$
这是一个从格点 $x$ 出发并返回到 $x$ 的平行输运算符。根据连结变量的变换规则，平头钉的变换为 $U_{\mu\nu}(x) \to \Omega(x) U_{\mu\nu}(x) \Omega^\dagger(x)$。利用迹的循环[不变性](@entry_id:140168)，$\mathrm{Tr}\,U_{\mu\nu}(x)$ 是一个规范不变的量。在[连续极限](@entry_id:162780)下，可以证明平头钉与[场强张量](@entry_id:159746) $F_{\mu\nu}$ 相关：
$$
U_{\mu\nu}(x) = \exp\left(iga^2 F_{\mu\nu}(x) + \mathcal{O}(a^3)\right)
$$
因此，**威尔逊规范作用量（Wilson gauge action）** 通过对所有平头钉的迹求和来构造，其形式为：
$$
S_G[U] = \beta \sum_{x, \mu\lt\nu} \left(1 - \frac{1}{N_c} \mathrm{Re}\,\mathrm{Tr}\,U_{\mu\nu}(x)\right)
$$
其中 $\beta = 2N_c/g^2$，$N_c=3$ 是颜色数。在[连续极限](@entry_id:162780) $a \to 0$ 下，该作用量正比于 $\int d^4x\, \mathrm{Tr}\left[F_{\mu\nu}(x)F^{\mu\nu}(x)\right]$，从而正确地复现了杨-米尔斯作用量 。

这种构造方法可以推广到任意空间分离的算符。例如，一个规范不变的介子算符可以连接两个不同的格点 $x$ 和 $y$，形式为 $\mathcal{O}_{\Gamma}(x,y) = \bar q(x)\,\Gamma\,W(x,y)\,q(y)$。其中 $W(x,y)$ 是连接 $y$ 到 $x$ 的任意路径上的连结变量的有序乘积，称为**威尔逊线（Wilson line）**。由于 $W(x,y)$ 的变换性质为 $W(x,y) \to \Omega(x)W(x,y)\Omega^\dagger(y)$，整个算符的[规范不变性](@entry_id:137857)得以保证 。

### 物质场：[费米子](@entry_id:146235)离散化与手征对称性

将[费米子](@entry_id:146235)置于格点上引入了一个深刻的难题，即**[费米子](@entry_id:146235)加倍问题（fermion doubling problem）**。Nielsen-Ninomiya 定理指出，任何具有局域性、平移不变性、[厄米性](@entry_id:141899)且在[连续极限](@entry_id:162780)下具有正确手征对称性的格点[费米子](@entry_id:146235)作用量，都不可避免地会产生额外的、非物理的[费米子](@entry_id:146235)副本（称为“加倍子”或“味道”）。几种主流的[费米子](@entry_id:146235)离散化方案通过以不同方式规避该定理的假设来解决此问题 。

1.  **[交错费米子](@entry_id:755338)（Staggered Fermions）**：该方案通过“自旋对角化”变换，将朴素[费米子](@entry_id:146235)作用量产生的16个加倍子减少为4个物理“味道”（tastes）。[费米子](@entry_id:146235)场被简化为单分量场 $\chi(x)$，[分布](@entry_id:182848)在[超立方体](@entry_id:273913)的各个角落。其狄拉克算符为：
    $$
    D_{\mathrm{st}}(x,y) = m\,\delta_{x,y} + \frac{1}{2a}\sum_{\mu} \eta_{\mu}(x)\Big[U_{\mu}(x)\,\delta_{x+\hat\mu,y} - U_{\mu}^{\dagger}(x-\hat\mu)\,\delta_{x-\hat\mu,y}\Big]
    $$
    其中 $\eta_{\mu}(x)$ 是依赖于格点坐标的Kogut-Susskind相因子。在无质量极限 $m=0$ 时，[交错费米子](@entry_id:755338)作用量保留了一种残余的 $U(1)_\varepsilon$ 手征对称性，这可以保护[费米子质量](@entry_id:155586)免受加法[重整化](@entry_id:143501)。然而，在有限格点间距 $a>0$ 时，描述4个味道之间变换的 $SU(4)$ **味道对称性**被破坏，导致本应简并的[强子谱](@entry_id:137624)（如π介子）出现劈裂。这些劈裂是 $\mathcal{O}(a^2)$ 的离散效应（对于改进作用量）。为了模拟单味夸克，[交错费米子](@entry_id:755338)需要采用“四次方根技巧”，这一步骤的理论基础仍在积极讨论中。

2.  **畴壁[费米子](@entry_id:146235)（Domain-Wall Fermions, DWF）**：此方案引入了一个额外的第五维，其大小为 $L_s$。通过巧妙地设计一个五维狄拉克算符，手征性相反的零模被束缚在第五维的两个边界（“[畴壁](@entry_id:144723)”）上。物理的四维夸克被等同于这些边界模。在 $L_s$ 有限时，左右手模之间存在微弱的耦合，导致手征对称性被轻微地显式破坏。这种破坏的程度由一个**剩余质量** $m_{\mathrm{res}}$ 来量化，它随 $L_s$ 的增大而指数衰减。通过选择足够大的 $L_s$，可以实现非常好的近似手征对称性。DWF没有味道加倍问题。

3.  **重叠[费米子](@entry_id:146235)（Overlap Fermions）**：该方案在理论上最为优雅。它直接构造了一个满足**金斯帕-威尔逊关系（Ginsparg-Wilson relation）**的狄拉克算符 $D_{\mathrm{ov}}$：
    $$
    \{D_{\mathrm{ov}}, \gamma_5\} = a D_{\mathrm{ov}} \gamma_5 D_{\mathrm{ov}}
    $$
    满足此关系的算符具有一种精确的**格点手征对称性**，即使在有限格点间距 $a$ 上也成立。一个典型的构造是Neuberger算符：
    $$
    D_{\mathrm{ov}} = \frac{\rho}{a}\left[ 1 + \gamma_{5}\,\mathrm{sign}\big(H_{W}(-\rho)\big) \right], \quad H_{W}(-\rho) \equiv \gamma_{5}\left(D_{W} - \frac{\rho}{a}\right)
    $$
    其中 $D_W$ 是威尔逊-狄拉克算符，$\rho$ 是一个参数。这种精确的手征对称性杜绝了加法[质量重整化](@entry_id:139777)，并保证了格点上有精确的[指标定理](@entry_id:637636)。与DWF一样，重叠[费米子](@entry_id:146235)也没有味道加倍问题。

在[强子谱学](@entry_id:155019)计算中，[交错费米子](@entry_id:755338)计算成本较低，但需要仔细处理味道[对称性破缺](@entry_id:158994)带来的系统误差。[畴壁](@entry_id:144723)和重叠[费米子](@entry_id:146235)提供了更清晰的手征行为，代价是显著增加的计算成本 。

### 系统误差：离散效应与Symanzik改进

格点离散化引入的误差称为**离散效应（discretization effects）**或**截断误差（cutoff effects）**。**[Symanzik有效理论](@entry_id:755707)（Symanzik effective theory, SET）**为系统地分析和消除这些误差提供了理论框架。其核心思想是，一个局域格点作用量 $S_L$ 描述的物理，对于壳层（on-shell）规范不变的[可观测量](@entry_id:267133)而言，等价于一个由无穷多个局域算符构成的连续有效拉格朗日量 $\mathcal{L}_{eff}$ ：
$$
\mathcal{L}_{eff} = \mathcal{L}_{QCD}^{(4)} + a \mathcal{L}^{(5)} + a^2 \mathcal{L}^{(6)} + \dots
$$
其中 $\mathcal{L}_{QCD}^{(4)}$ 是标准的四维连续[QCD拉格朗日量](@entry_id:158089)。$\mathcal{L}^{(d-4)}$ 是由所有维度为 $d$、且与格点作用量具有相同对称性的规范不变算符组成的线性组合，其系数由 $a^{d-4}$ 压低。物理量（如[强子质量](@entry_id:204733)）的离散误差的主导行为由有效[拉格朗日量](@entry_id:174593)中维度最低（$d>4$）的非零算符项决定。

-   **威尔逊规范作用量**：由于其对称性，所有维度为5的纯规范算符都为零。最低阶的修正来自维度为6的算符，因此其离散误差为 $\mathcal{O}(a^2)$。
-   **[威尔逊费米子](@entry_id:146106)作用量**：标准[威尔逊费米子](@entry_id:146106)作用量显式地破坏了手征对称性。这允许一个维度为5的算符 $\bar\psi \sigma_{\mu\nu} F_{\mu\nu} \psi$ 出现在有效[拉格朗日量](@entry_id:174593)中，导致[强子质量](@entry_id:204733)等物理量通常存在 $\mathcal{O}(a)$ 的离散误差 。
-   **$\mathcal{O}(a)$ 改进**：为了消除这些主导的 $\mathcal{O}(a)$ 误差，可以向作用量中添加一个反冲项。对于[威尔逊费米子](@entry_id:146106)，这个反冲项是**Sheikholeslami-Wohlert (SW)项**或“**三叶草项（clover term）**”。通过恰当地调节其系数 $c_{\mathrm{SW}}$，可以使有效[拉格朗日量](@entry_id:174593)中维度为5的算符的系数为零。这样改进后的作用量，其离散误差的[主导项](@entry_id:167418)变为 $\mathcal{O}(a^2)$。值得注意的是，即使作用量是 $\mathcal{O}(a)$ 改进的，用于计算矩阵元的[复合算符](@entry_id:152160)（如流算符）通常也需要各自独立的改进，才能确保[矩阵元](@entry_id:186505)也没有 $\mathcal{O}(a)$ 误差 。
-   **自动$\mathcal{O}(a)$改进**：在某些特定情况下，即使没有明确添加反冲项，$\mathcal{O}(a)$ 误差也会由于对称性而自动消失。一个重要的例子是处于**最大扭转角（maximal twist）**的**扭质量[威尔逊费米子](@entry_id:146106)（twisted-mass Wilson fermions）**，对于宇称偶的[可观测量](@entry_id:267133)，其离散误差自动从 $\mathcal{O}(a^2)$ 开始 。

满足金斯帕-威尔逊关系的[费米子](@entry_id:146235)（如重叠[费米子](@entry_id:146235)）由于其精确的格点手征对称性，自动禁止了所有破坏手征性的低维算符，因此其离散误差天然就是 $\mathcal{O}(a^2)$ 或更高阶。

### 从欧几里得到物理世界：关联函数与[谱表示](@entry_id:153219)

[格点QCD](@entry_id:143754)计算是在欧几里得时空中通过[路径积分](@entry_id:156701)进行的，其权重因子为 $e^{-S_E}$，其中 $S_E$ 是[欧几里得作用量](@entry_id:144897)。这与物理的[闵可夫斯基时空](@entry_id:156421)（权重为 $e^{iS_M}$）不同。两者之间的桥梁是**威克转动（Wick rotation）**，$t \to -i t_E$。一个欧几里得关联函数可以被[解析延拓](@entry_id:147225)到[闵可夫斯基时空](@entry_id:156421)，从而提取物理信息。这一过程的有效性依赖于严格的理论基础，即**Osterwalder-Schrader (OS) 公理**，其中最关键的是**反射正性（reflection positivity）**。它保证了从欧几里得理论重构出的闵可夫斯基理论是幺正的，并且具有正定的能谱 。

在格点上，我们计算的是欧几里得**两点关联函数（two-point correlation function）**。对于一个具有特定强子[量子数](@entry_id:145558)的插值算符 $O(x)$，其零动量投影的两点函数定义为：
$$
C_E(t) = a^3 \sum_{\mathbf{x}} \langle O_E(t, \mathbf{x}) O_E^\dagger(0, \mathbf{0}) \rangle_E
$$
这里的[期望值](@entry_id:153208) $\langle \dots \rangle_E$ 是通过对所有场组态进行路径积分得到的，权重为 $e^{-S_E}$。利用[传递矩阵](@entry_id:145510)（transfer-matrix）形式，可以将此关联函数表示为对[哈密顿量](@entry_id:172864) $\hat{H}$ 的所有能量本征态 $|n\rangle$ 的求和，即**[谱分解](@entry_id:173707)（spectral decomposition）**：
$$
C_E(t) = \sum_{n} |\langle 0| \hat{O} |n\rangle|^2 e^{-E_n t}
$$
其中 $E_n$ 是[能量本征值](@entry_id:144381)（$E_0$ 为[真空能](@entry_id:155067)量，已设为零），$\langle 0| \hat{O} |n\rangle$ 是算符 $\hat{O}$ 连接真空与态 $|n\rangle$ 的**重叠因子（overlap factor）**。这个表达式表明，欧几里得关联函数随时间 $t$ 指数衰减，衰减速率由[能量本征值](@entry_id:144381)决定。

与之对应，闵可夫斯基时空中的时间排序两点函数 $C_M(t) = \langle 0| \mathrm{T}\, O_M(t)\, O_M^\dagger(0) |0\rangle$，对于 $t>0$ 的[谱表示](@entry_id:153219)为：
$$
C_M(t) = \sum_n |\langle 0|O_M|n\rangle|^2 e^{-i E_n t}
$$
它随时间[振荡](@entry_id:267781)。比较两者形式，可以看出它们通过解析延拓 $t \to -it_E$ 联系在一起 。

### 提取[强子质量](@entry_id:204733)：两点函数与有效质量

从两点关联函数的[谱分解](@entry_id:173707)可以看出，在欧几里得时间 $t$ 足够大时，关联函数将由能量最低的态，即[基态](@entry_id:150928)（质量为 $m_H = E_0$）所主导：
$$
C(t) \approx |\langle 0|\hat{O}|H\rangle|^2 e^{-m_H t} \quad (t \to \infty)
$$
这为提取[基态](@entry_id:150928)[强子质量](@entry_id:204733) $m_H$ 提供了直接途径。一个强大的诊断工具是**[有效质量](@entry_id:142879)（effective mass）**，其定义为：
$$
m_{\text{eff}}(t) = \ln\left[\frac{C(t)}{C(t+1)}\right]
$$
在只有[基态](@entry_id:150928)贡献的理想情况下，$C(t)/C(t+1) = e^{m_H}$，因此 $m_{\text{eff}}(t)$ 精确等于 $m_H$。在实际情况中，关联函数总是包含来自[激发态](@entry_id:261453)的**污染（contamination）**。将谱展开式代入，可以分析有效质量的行为 。考虑[基态](@entry_id:150928)和第一[激发态](@entry_id:261453)（能量为 $E_1$），关联函数近似为：
$$
C(t) \approx |Z_0|^2 e^{-E_0 t} + |Z_1|^2 e^{-E_1 t} = |Z_0|^2 e^{-E_0 t} \left(1 + \frac{|Z_1|^2}{|Z_0|^2} e^{-(E_1-E_0)t}\right)
$$
其中 $Z_n = \langle 0|\hat{O}|n\rangle$。有效质量将表现为：
$$
m_{\text{eff}}(t) \approx E_0 + \mathcal{O}(e^{-\Delta E \cdot t})
$$
其中 $\Delta E = E_1 - E_0$ 是[能隙](@entry_id:191975)。这意味着，随着 $t$ 增大，[有效质量](@entry_id:142879)会从一个较高的值逐渐趋近于基态能量 $E_0$，形成一个“**平台（plateau）**”。平台区的数值即为所求的[强子质量](@entry_id:204733)。

在有限时间维度的格点上，周期性边界条件会导致“**绕回效应（wrap-around effect）**”。关联函数的形式变为：
$$
C(t) = \sum_n |Z_n|^2 \left( e^{-E_n t} + e^{-E_n (T-t)} \right)
$$
其中 $T$ 是时间维度的总长度。当 $t \approx T/2$ 时，向后传播的项 $e^{-E_n(T-t)}$ 不可忽略，会导致有效质量平台被破坏。为了处理这种情况，可以使用**双曲余弦[有效质量](@entry_id:142879)（hyperbolic-cosine effective mass）**：
$$
m_{\text{eff}}^{\cosh}(t) = \operatorname{arcosh}\left(\frac{C(t-1)+C(t+1)}{2C(t)}\right)
$$
这个定义恰好能消除单态贡献中的绕回效应，因为它精确地反解了 $\cosh$ 函数形式，从而在 $t \approx T/2$ 附近也能给出稳定的平台 。

### 改进信号：算符涂抹

为了更快地达到有效质量平台并降低[统计误差](@entry_id:755391)，关键在于构造一个能最大化[基态](@entry_id:150928)重叠因子 $|Z_0|^2$ 并同时最小化[激发态](@entry_id:261453)重叠因子 $|Z_{n>0}|^2$ 的插值算符。物理上，[基态](@entry_id:150928)[强子](@entry_id:158325)是一个具有一定空间尺度的束缚态，而[激发态](@entry_id:261453)通常具有更复杂的[节点结构](@entry_id:151019)或更小的空间尺度。因此，一个点状的局域算符通常与[激发态](@entry_id:261453)有显著的重叠。

**规范不变涂抹（gauge-invariant smearing）**技术通过将夸克场在空间上“涂抹”开来，构造出一个扩展的、更“平滑”的算符，使其[波函数](@entry_id:147440)更接近[基态](@entry_id:150928)强子的[波函数](@entry_id:147440)。**高斯涂抹（Gaussian smearing）**或**Wuppertal涂抹**是一种常用方法 。它通过迭代应用一个规范[协变](@entry_id:634097)的空间[跳跃算符](@entry_id:155707)来实现。这个过程等效于对夸克场作用一个规范协变拉普拉斯算符的指数：
$$
\psi^{(S)}(x) \approx (e^{\sigma^2 \nabla_c^2} \psi)(x)
$$
其中 $\sigma$ 是涂抹半径，$\nabla_c^2$ 是规范协变拉普拉斯算符。重要的是：
1.  **规范[协变](@entry_id:634097)性**：涂抹过程必须使用空间方向的连结变量来保持规范[协变](@entry_id:634097)性，即涂抹后的场 $\psi^{(S)}$ 与原场 $\psi$ 具有相同的规范变换性质。这保证了由涂抹场构建的强子算符仍然是规范不变的，无需额外的[规范固定](@entry_id:142821)。
2.  **空间局域性**：涂抹必须严格限制在每个固定的时间片内，只涉及空间方向的跃迁。任何涉及时间方向的涂抹都会改变传递矩阵，从而改变理论的[能谱](@entry_id:181780) $E_n$，这是不允许的。
3.  **效果**：正确的涂抹会改变重叠因子 $Z_n$，但不会改变[能量本征值](@entry_id:144381) $E_n$。它通过压低[激发态](@entry_id:261453)贡献，使有效质量平台在更早的时间 $t$ 开始，从而提高了信号质量 。

### 提取[矩阵元](@entry_id:186505)：三点函数与分析方法

除了质量，[强子](@entry_id:158325)的另一个重要属性是其内部结构，这由各种流算符（如电磁流或轴矢流）的**[矩阵元](@entry_id:186505)**来描述，例如形状因子。这些[矩阵元](@entry_id:186505)可以通过计算**三点关联函数（three-point correlation function）**来提取。一个典型的三点函数形式如下 ：
$$
C^{3\text{pt}}(t,T) = \langle O_f(T)\,J(t)\,O_i^\dagger(0)\rangle
$$
其中 $O_i^\dagger(0)$ 在 $t=0$ 时刻产生一个初态强子，$O_f(T)$ 在 $t=T$ 时刻湮灭一个末态强子，$J(t)$ 是在中间时刻 $t$ 插入的流算符。通过插入完备的能量本征态，其谱分解为：
$$
C^{3\text{pt}}(t,T) = \sum_{n,m} Z_{f,n}^* Z_{i,m} \langle n|J|m \rangle e^{-E_n(T-t)} e^{-E_m t}
$$
其中 $Z_{k,n} = \langle n|O_k^\dagger|\Omega \rangle$。当时间间隔 $t$ 和 $T-t$ 都足够大时，此和式由初末态均为[基态](@entry_id:150928)的项主导：
$$
C^{3\text{pt}}(t,T) \approx Z_{f,0}^* Z_{i,0} \langle f|J|i\rangle e^{-E_f(T-t)} e^{-E_i t}
$$
其中 $\langle f|J|i\rangle$ 就是我们希望得到的[基态](@entry_id:150928)矩阵元。为了从三点函数中分离出这个矩阵元，并处理[激发态](@entry_id:261453)污染，发展了几种标准方法：

1.  **平台法（Plateau Method）**：构造一个三点函数与二点函数的比值，旨在抵消指数衰减项和重叠因子 $Z_n$。例如，对于 $i=f$ 的情况，一个常见的比值为：
    $$
    R(t,T) = \frac{C^{3\text{pt}}(t,T)}{C^{2\text{pt}}(T)} \sqrt{\frac{C^{2\text{pt}}(T-t)C^{2\text{pt}}(t)}{C^{2\text{pt}}(T-t+a)C^{2\text{pt}}(t-a)}} \times \dots
    $$
    （具体的比值形式有多种变体）。在 $t \to \infty$ 和 $T-t \to \infty$ 的极限下，这个比值会趋于一个与 $t$ 无关的常数平台，其值正比于[矩阵元](@entry_id:186505) $\langle f|J|i\rangle$。主导的系统误差来自[激发态](@entry_id:261453)，其压低因子为 $\exp(-\Delta E \cdot \min(t, T-t))$ 。

2.  **两态拟合法（Two-State Method）**：不依赖于取渐近极限，而是构建一个包含[基态](@entry_id:150928)和第一[激发态](@entry_id:261453)的理论模型来直接拟合关联函数数据。对二点和三点函数进行联合拟合，模型参数包括[基态](@entry_id:150928)和[激发态](@entry_id:261453)的能量、重叠因子，以及所有相关的矩阵元（如 $\langle f|J|i\rangle, \langle f'|J|i\rangle, \langle f|J|i'\rangle$ 等）。这种方法可以在[激发态](@entry_id:261453)污染还比较显著的较小时间间隔上提取信息，从而可能改善统计精度 。

3.  **求和法（Summation Method）**：对一个归一化的比值（类似于平台法中的比值）在流插入时间 $t$ 上求和。例如，对 $S(T) = \sum_{t} C^{3\text{pt}}(t,T)$ 进行分析。可以证明，经过合适的归一化后，这个求和量随 $T$ [线性增长](@entry_id:157553)，其斜率正比于所求的[矩阵元](@entry_id:186505)。该方法能有效平均掉部分[激发态](@entry_id:261453)污染，其剩余的系统误差随 $T$ 的压低比平台法更强，通常为 $\mathcal{O}(e^{-\Delta E \cdot T})$ 。

### 连接到物理单位：标度设定

格点计算本身产生的是无量纲的数字，如 $am_H$ 或 $w_0/a$。为了将这些结果转换为物理单位（如MeV或fm），必须确定格点间距 $a$ 的物理值。这个过程称为**标度设定（scale setting）**。它通过将一个在格点上精确计算出的物理量与其实验测量值或约定值进行匹配来完成 。

选择用于标度设定的物理量 $O_{\text{ref}}$ 时，希望它对模拟参数（如夸克质量）的依赖性较弱，并且能在实验和格点上都被高精度地确定。常用的标度设定物理量包括一些[强子质量](@entry_id:204733)（如$\Omega$重子质量 $m_\Omega$）或从**梯度流（gradient flow）**中定义的标度（如 $t_0$ 或 $w_0$）。

标度设定策略分为两种：

1.  **绝对标度设定（Absolute Scale Setting）**：通常在模拟参数（特别是夸克质量）已调谐到接近其物理值的“[参考系](@entry_id:169232)综”上进行。例如，如果在[参考系](@entry_id:169232)综 $\mathcal{R}$ 上测得无量纲量 $(w_0/a)_\mathcal{R}$，则格点间距为：
    $$
    a_\mathcal{R} = \frac{w_0^{\text{phys}}}{(w_0/a)_\mathcal{R}}
    $$
    其中 $w_0^{\text{phys}}$ 是 $w_0$ 的物理值（例如 $0.1715\,\text{fm}$）。类似地，如果使用 $m_\Omega$：
    $$
    a_\mathcal{R} [\text{fm}] = \frac{(a m_\Omega)_\mathcal{R}}{m_\Omega^{\text{phys}}[\text{MeV}]} \cdot (\hbar c)[\text{MeV fm}]
    $$
    

2.  **相对标度设定（Relative Scale Setting）**：用于确定不同系综（例如具有不同夸克质量或格点间距的系综）之间的格点间距比值。例如，要确定系综 $\mathcal{A}$ 相对于[参考系](@entry_id:169232)综 $\mathcal{R}$ 的格点间距 $a_\mathcal{A}$，可以假设物理量 $w_0$ 在两个系综上是相同的，即 $a_\mathcal{R}(w_0/a)_\mathcal{R} \approx a_\mathcal{A}(w_0/a)_\mathcal{A}$。由此得到：
    $$
    a_\mathcal{A} \approx a_\mathcal{R} \frac{(w_0/a)_\mathcal{R}}{(w_0/a)_\mathcal{A}}
    $$
    此方法的优点是不需要知道 $w_0^{\text{phys}}$ 的[绝对值](@entry_id:147688)。然而，它忽略了标度设定物理量本身对夸克质量等参数的依赖性，这会引入系统误差。如果用不同的物理量（如 $w_0$ 和 $m_\Omega$）进行相对标度设定，得到的结果可能会有差异，这个差异就反映了这种系统误差 。

### 连接到连续区方案：算符重整化

格点正则化是一种依赖于截断 $a$ 的[正则化方案](@entry_id:159370)。在格点上计算出的裸（bare）矩阵元与在连续区中定义的、并在某个普适方案（如 $\overline{\mathrm{MS}}$）下[重整化](@entry_id:143501)的[矩阵元](@entry_id:186505)不同。为了进行有意义的比较，必须计算**[重整化](@entry_id:143501)常数（renormalization constants）** $Z_\mathcal{O}$，它将格点算符与连续区算符联系起来：$\mathcal{O}^{\text{ren}} = Z_\mathcal{O} \mathcal{O}^{\text{bare}}$。

一个强大的非微扰[重整化](@entry_id:143501)方法是**正则化无关动量相减（Regularization-Independent Momentum Subtraction, RI/MOM）**方案 。该方法在固定的规范（通常是朗道规范）下，通过对夸克-胶子格林函数施加[重整化](@entry_id:143501)条件来确定[重整化](@entry_id:143501)常数。其核心思想是，在某个动量标度 $\mu$ 下，要求经过重整化的截断格林函数（amputated Green's function）等于其[树图](@entry_id:276372)（tree-level）值。

然而，RI/MOM方案本身是依赖于规范和动量构型的，不便于与其他实验或理论结果直接比较。因此，它通常作为一个中间步骤，后续会通过一个微扰计算的**匹配因子（matching factor）**将其匹配到普适的 $\overline{\mathrm{MS}}$ 方案。整个流程如下：
1.  在格点上非微扰地计算 $Z_\mathcal{O}^{\mathrm{RI}}(\mu, a)$。
2.  在连续区[微扰理论](@entry_id:138766)中计算匹配因子 $C^{\mathrm{RI}\to\overline{\mathrm{MS}}}(\mu) = Z_\mathcal{O}^{\overline{\mathrm{MS}}}(\mu) / Z_\mathcal{O}^{\mathrm{RI}}(\mu)$。
3.  得到 $Z_\mathcal{O}^{\overline{\mathrm{MS}}}(\mu, a) = C^{\mathrm{RI}\to\overline{\mathrm{MS}}}(\mu) \cdot Z_\mathcal{O}^{\mathrm{RI}}(\mu, a)$。
4.  使用 $\overline{\mathrm{MS}}$ 方案下的**[反常维度](@entry_id:147674)（anomalous dimension）**和重整化群方程（RGE），将结果从标度 $\mu$ 演化到任何其他感兴趣的标度 $\mu'$ 。

在实际操作中，选择[重整化标度](@entry_id:153146) $\mu$ 至关重要。为了保证计算的可靠性，$\mu$ 必须处于一个“窗口”中：$\Lambda_{\mathrm{QCD}} \ll \mu \ll \pi/a$。$\mu$ 必须远大于 $\Lambda_{\mathrm{QCD}}$ 以避免强的[非微扰效应](@entry_id:148492)（如自发手征对称破缺引起的赝标[介子](@entry_id:184535)极点污染）；同时 $\mu$ 必须远小于格点截断 $\pi/a$ 以控制 $\mathcal{O}((a\mu)^2)$ 的离散误差 。

### 一个微妙的挑战：拓扑与冻结

[QCD真空](@entry_id:150509)具有非平庸的拓扑结构，由[瞬子](@entry_id:153491)等[规范场](@entry_id:159627)组态所表征。这种结构由一个整数**拓扑荷（topological charge）** $Q$ 来描述。在[欧几里得路径积分](@entry_id:148498)中，我们需要对所有拓扑扇区进行采样。

在格点上，[拓扑荷](@entry_id:142322)的朴素离散化会受到大的紫外涨落污染，不会得到整数值。一个现代且可靠的测量方法是利用[梯度流](@entry_id:635964)。通过将规范场演化到一个正的流时间 $t$，可以有效抹平紫外噪音。在流时间 $t>0$ 时，从[流化](@entry_id:192588)场计算出的拓扑荷密度 $q_t(x)$ 是一个有限的算符，无需额外[重整化](@entry_id:143501)。其全空间积分 $Q_t = a^4 \sum_x q_t(x)$ 在[连续极限](@entry_id:162780) $a \to 0$ 下会收敛到整数 。

在现代[格点模拟](@entry_id:751176)中，随着格点间距 $a$ 变小，一个严峻的挑战出现了，即**拓扑冻结（topological freezing）**。[MCMC算法](@entry_id:751788)在不同拓扑扇区之间跃迁的势垒随 $a$ 减小而急剧增高，导致算法被“冻结”在单个或少数几个拓扑扇区内，无法对所有扇区进行有效采样。

如果模拟长时间停留在某个固定的拓扑扇区 $Q$ 内，测量的物理量（如[强子质量](@entry_id:204733) $m_H$）会相对于在所有扇区上正确平均的结果产生系统偏差。这个偏差的大小与体积的倒数成正比，其主导项为 ：
$$
\langle m_H \rangle_Q - m_H(\theta=0) \propto \frac{1}{\chi_t V}
$$
其中 $V$ 是时空四维体积，$\chi_t = \langle Q^2 \rangle / V$ 是**拓扑磁化率（topological susceptibility）**。这个偏差由物理量对真空角 $\theta$ 的依赖性决定。因此，拓扑冻结会对[高精度计算](@entry_id:200567)构成一个严重的系统误差来源，必须仔细评估和处理。