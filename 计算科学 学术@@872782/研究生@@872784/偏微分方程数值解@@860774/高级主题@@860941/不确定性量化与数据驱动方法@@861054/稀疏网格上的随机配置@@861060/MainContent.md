## 引言
在现代科学与工程领域，精确的数值模拟是理解和预测复杂物理现象的关键。然而，这些模型往往受到输入[参数不确定性](@entry_id:264387)的影响，如材料属性、几何形状或边界条件的变化。量化这些不确定性对模型输出的影响，即[不确定性量化](@entry_id:138597)（UQ），对于可靠的设计和决策至关重要。一个核心挑战是“[维数灾难](@entry_id:143920)”：随着不确定参数数量的增加，传统数值方法的计算成本会呈指数级增长，使得精确分析变得遥不可及。本文旨在介绍一种强大且高效的非侵入式UQ方法——[稀疏网格](@entry_id:139655)[随机配置法](@entry_id:174778)，它通过利用问题内在的光滑性结构，巧妙地攻克了[高维积分](@entry_id:143557)和插值的难题。

为了全面掌握这一技术，本文将分三部分展开。首先，在“原理与机制”一章中，我们将深入剖析该方法的数学基础，从[参数化](@entry_id:272587)PDE的表述到[Smolyak算法](@entry_id:139824)的精巧构造，揭示其如何战胜维数灾难。接着，在“应用与跨学科联系”一章中，我们将展示该方法在地下水流、[结构力学](@entry_id:276699)等领域的实际应用，并探讨其如何处理时间依赖、几何不确定性及非光滑响应等复杂挑战。最后，通过“动手实践”部分提供的具体练习，读者将有机会亲手实现[稀疏网格](@entry_id:139655)的构建和应用，将理论知识转化为实践能力。

## 原理与机制

本章旨在深入探讨[稀疏网格](@entry_id:139655)[随机配置法](@entry_id:174778)的核心原理与关键机制。在前一章介绍其基本动机与应用背景之后，我们将系统性地剖析该方法的数学框架、算法构造、收敛性理论以及针对复杂问题的进阶策略。我们将从[参数化偏微分方程](@entry_id:753165)（PDE）的数学表述出发，逐步揭示[稀疏网格](@entry_id:139655)法如何通过高维空间中的巧妙构造，高效地攻克不确定性量化中的“维数灾难”挑战。

### [参数化偏微分方程](@entry_id:753165)与关注量

不确定性量化（UQ）的许多问题都可以抽象为一个依赖于一组不确定参数的[偏微分方程](@entry_id:141332)模型。从数学上讲，我们考虑一个定义在有界Lipschitz物理域 $D \subset \mathbb{R}^n$ 上的参数化PDE。令参数向量为 $\boldsymbol{y} \in \Gamma \subset \mathbb{R}^d$，其中参数空间 $\Gamma$ 配备了一个[概率密度函数](@entry_id:140610) $\rho(\boldsymbol{y})$。对于每一个确定的参数值 $\boldsymbol{y}$，我们求解一个确定性PDE。在泛函分析的框架下，这通常表述为[变分形式](@entry_id:166033)：寻找解 $u(\boldsymbol{y}) \in V$，使得对于所有检验函数 $v \in V$ 都成立：
$$
a(u, v; \boldsymbol{y}) = F(v; \boldsymbol{y})
$$
这里，$V$ 是一个合适的[希尔伯特空间](@entry_id:261193)（例如，$V = H_0^1(D)$），$a(\cdot, \cdot; \boldsymbol{y})$ 是一个依赖于参数 $\boldsymbol{y}$ 的双线性形式，而 $F(\cdot; \boldsymbol{y})$ 是一个线性泛函。当[双线性形式](@entry_id:746794) $a$ 对于[参数空间](@entry_id:178581) $\Gamma$ 中的每一个 $\boldsymbol{y}$ 都是连续且强制的（coercive），[Lax-Milgram定理](@entry_id:137966)保证了对每一个 $\boldsymbol{y}$，PDE都存在唯一解 $u(\boldsymbol{y})$。

在实际应用中，我们通常不关心完整的解场 $u(\boldsymbol{y})$，因为它是一个高维甚至无穷维的对象。我们更感兴趣的是一个或多个从解中提取出的标量，称之为**关注量**（Quantity of Interest, QoI）。QoI是一个可测泛函 $Q: V \to \mathbb{R}$，它可以是解在某一点的值 $u(x_0; \boldsymbol{y})$、在某个区域上的平均值 $\int_{\Omega} u(x; \boldsymbol{y}) \, \mathrm{d}x$，或是跨越某个边界的通量等。因此，UQ的核心任务就转化为研究从参数到关注量的映射 $\boldsymbol{y} \mapsto Q(u(\boldsymbol{y}))$，并计算其统计特性，如期望、[方差](@entry_id:200758)等 [@problem_id:3447861]。例如，[期望值](@entry_id:153208)由以下[高维积分](@entry_id:143557)给出：
$$
\mathbb{E}[Q(u(\boldsymbol{y}))] = \int_{\Gamma} Q(u(\boldsymbol{y})) \, \rho(\boldsymbol{y}) \, \mathrm{d}\boldsymbol{y}
$$
这个积分的被积函数 $Q(u(\boldsymbol{y}))$ 通常没有解析表达式，其每一次求值都需要进行一次昂贵的PDE数值求解。这正是[随机配置法](@entry_id:174778)旨在解决的计算挑战。

### 不确定性的[参数化](@entry_id:272587)表示：[Karhunen-Loève展开](@entry_id:751050)

在许多物理问题中，不确定性最初是以随机场的形式出现的，例如在地下水流动模型中，渗透率系数 $a(x, \omega)$ 是一个随空间位置 $x$ 变化的[随机过程](@entry_id:159502)。为了将这类无穷维不确定性输入转化为一个有限维的参数化PD[E模](@entry_id:160271)型，**Karhunen-Loève (K-L) 展开**是一种标准且有效的方法。

一个二阶[随机场](@entry_id:177952) $a(x, \omega)$ 可以被展开为：
$$
a(x, \omega) = \bar{a}(x) + \sum_{j=1}^{\infty} \sqrt{\lambda_j} \phi_j(x) y_j(\omega)
$$
其中，$\bar{a}(x)$ 是均值场；$(\lambda_j, \phi_j)$ 是[随机场](@entry_id:177952)协[方差](@entry_id:200758)算子的[特征值](@entry_id:154894)-特征函数对，且[特征值](@entry_id:154894)按降序[排列](@entry_id:136432) $\lambda_1 \ge \lambda_2 \ge \dots \ge 0$；$y_j(\omega)$ 是一组互不相关的标准[随机变量](@entry_id:195330)。[特征值](@entry_id:154894) $\lambda_j$ 代表了模态 $\phi_j(x)$ 对总[方差](@entry_id:200758)的贡献。如果[特征值](@entry_id:154894)衰减得很快，我们就可以截断此展开，只保留前 $d$ 项，从而得到一个有限维的近似：
$$
a_d(x, \boldsymbol{y}) = \bar{a}(x) + \sum_{j=1}^{d} \sqrt{\lambda_j} \phi_j(x) y_j
$$
这里，我们用一个有限维的参数向量 $\boldsymbol{y} = (y_1, \dots, y_d) \in \mathbb{R}^d$ 代替了抽象的[随机变量](@entry_id:195330)。通过这种方式，一个具有[随机场](@entry_id:177952)输入的PDE问题被转化为了一个[参数化](@entry_id:272587)的PDE问题。

K-L展开的[特征值](@entry_id:154894)衰减特性直接关系到参数空间中不同方向的“重要性”。对关注量 $Q$ 关于参数分量 $y_j$ 的敏感性进行分析可以发现，其一阶导数 $\partial Q / \partial y_j$ 的大小（在[能量范数](@entry_id:274966)意义下）通常与 $\sqrt{\lambda_j}$ 成正比 [@problem_id:3447821]。这意味着，具有较大[特征值](@entry_id:154894) $\lambda_j$ 的参数方向对模型输出的影响更大。这一洞察是构建**各向异性（anisotropic）**[稀疏网格](@entry_id:139655)的关键，即在更重要的参数方向上分配更多的计算资源（更高阶的插值或求积规则）。

### 方法论辨析：[随机配置法](@entry_id:174778)的位置

在进入[稀疏网格](@entry_id:139655)的构造细节之前，有必要将其置于[不确定性量化方法](@entry_id:756298)的广阔图景中进行比较。三种主流方法是：

1.  **[蒙特卡洛](@entry_id:144354)（[Monte Carlo](@entry_id:144354), MC）法**：通过从[概率分布](@entry_id:146404) $\rho(\boldsymbol{y})$ 中抽取大量独立同分布的样本点 $\boldsymbol{y}^{(k)}$，对每个样本点求解确定性PDE得到 $Q(\boldsymbol{y}^{(k)})$，最后通过样本均值 $\frac{1}{N} \sum_{k=1}^N Q(\boldsymbol{y}^{(k)})$ 来近似期望。MC法的优点在于其[收敛率](@entry_id:146534) $\mathcal{O}(N^{-1/2})$ 与参数空间的维度 $d$ 无关，且对关注量映射 $Q(\boldsymbol{y})$ 的光滑性要求极低（仅需[方差](@entry_id:200758)有限，即 $Q \in L^2(\Gamma, \rho)$）。它的缺点是[收敛速度](@entry_id:636873)慢。

2.  **随机配置（Stochastic Collocation, SC）法**：在[参数空间](@entry_id:178581) $\Gamma$ 中选择一组精心设计的“[配置点](@entry_id:169000)”，在这些点上[求解PDE](@entry_id:138485)，然后基于这些点值构造一个全局的代理模型（通常是[多项式插值](@entry_id:145762)），最后对这个廉价的代理模型进行积分来计算统计量。[稀疏网格](@entry_id:139655)法是SC的一种高效实现。SC法的[收敛速度](@entry_id:636873)依赖于 $Q(\boldsymbol{y})$ 的光滑性。对于光滑（甚至解析）的映射，SC法可以达到远超MC法的收敛速度。

3.  **侵入式随机Galerkin（intrusive Stochastic Galerkin, SG）法**：将解 $u(x, \boldsymbol{y})$ 展开为关于 $\boldsymbol{y}$ 的[多项式混沌](@entry_id:196964)[基函数](@entry_id:170178)，即 $u(x, \boldsymbol{y}) \approx \sum_{\alpha} u_{\alpha}(x) \Psi_{\alpha}(\boldsymbol{y})$。将此展开代入原PDE，并利用[Galerkin投影](@entry_id:145611)，会得到一个关于所有未知系数场 $u_{\alpha}(x)$ 的庞大的、耦合的确定性PDE系统。

这三种方法在两个关键维度上有所区别：**光滑性假设**和**侵入性**。
- **[光滑性](@entry_id:634843)**：MC法要求最低，SC法需要函数具有一定的混合正则性以获得快速收敛，而SG法通常需要函数关于参数是解析的才能展现其谱收敛的威力。
- **侵入性**：MC和SC都是**非侵入式**的，它们将现有的确定性[PDE求解器](@entry_id:753289)当作一个“黑箱”来重复调用，无需修改求解器代码。而SG法是**侵入式**的，它彻底改变了待解方程的形式，需要专门开发新的求解器来求解那个耦合的大系统 [@problem_id:3447802]。

[稀疏网格](@entry_id:139655)[随机配置法](@entry_id:174778)正好处在一个“甜点区”：它既能利用解的[光滑性](@entry_id:634843)获得高[收敛率](@entry_id:146534)，又保持了非侵入式的优点，使其能够方便地与现有的大型计算软件相结合。

### [稀疏网格](@entry_id:139655)的构造：[Smolyak算法](@entry_id:139824)

[稀疏网格](@entry_id:139655)的核心思想是，通过一种名为**Smolyak构造**的组合技术，以一种比标准[张量积](@entry_id:140694)更“稀疏”的方式来组合低维的插值或求积规则，从而缓解[维数灾难](@entry_id:143920)。

#### 从算子角度理解

让我们从算子的角度来构建[稀疏网格](@entry_id:139655)插值。首先，在每个参数维度 $j \in \{1, \dots, d\}$，我们定义一个一维插值算子的层级序列 $\{U_i^{(j)}\}_{i \in \mathbb{N}}$。这里的索引 $i$ 代表“层级”，层级越高，插值精度越高（通常意味着使用的节点数越多）。我们假设这些算子建立在**嵌套节点**上，即用于 $U_{i-1}^{(j)}$ 的节点集是 $U_i^{(j)}$ 节点集的[子集](@entry_id:261956)。

接着，我们定义**层级差分算子**（或称层级余差算子）：
$$
\Delta_i^{(j)} := U_i^{(j)} - U_{i-1}^{(j)}
$$
并约定 $U_0^{(j)} \equiv 0$。这个算子 $\Delta_i^{(j)}$ 捕捉了从层级 $i-1$ 提升到层级 $i$ 时所增加的“新信息”。有了这个定义，任何一个一维算子 $U_k^{(j)}$ 都可以表示为一个伸缩求和：$U_k^{(j)} = \sum_{i=1}^k \Delta_i^{(j)}$。

一个 $d$ 维的**全[张量积](@entry_id:140694)插值算子**，其每个维度都采用层级 $q$ 的规则，可以写作：
$$
\mathcal{T}_d^q = \bigotimes_{j=1}^d U_q^{(j)} = \bigotimes_{j=1}^d \left( \sum_{i_j=1}^q \Delta_{i_j}^{(j)} \right) = \sum_{i_1=1}^q \dots \sum_{i_d=1}^q \left( \bigotimes_{j=1}^d \Delta_{i_j}^{(j)} \right) = \sum_{\|\boldsymbol{i}\|_{\infty} \le q} \bigotimes_{j=1}^d \Delta_{i_j}^{(j)}
$$
这里，多重指标 $\boldsymbol{i} = (i_1, \dots, i_d) \in \mathbb{N}^d$。这个求和遍历了一个[超立方体](@entry_id:273913)[指标集](@entry_id:268489)。

Smolyak构造的精髓在于，它用一个更小的、基于 $\ell_1$ 范数的单纯形（simplex-like）[指标集](@entry_id:268489)来替换这个[超立方体](@entry_id:273913)[指标集](@entry_id:268489)。**各向同性Smolyak[稀疏网格](@entry_id:139655)插值算子** $\mathcal{A}_d^q$ 定义为 [@problem_id:3447838]：
$$
\mathcal{A}_{q,d} = \sum_{|\boldsymbol{i}|_1 \le q+d-1} \bigotimes_{j=1}^d \Delta_{i_j}^{(j)} \quad \text{其中} \quad |\boldsymbol{i}|_1 = \sum_{j=1}^d i_j, \; \boldsymbol{i} \in \mathbb{N}^d
$$
此处的层级 $q$ 是一个[抽象层级](@entry_id:268900)，具体的[指标集](@entry_id:268489)形式取决于层级定义。一个常见的选择是使用总次数（Total Degree）[指标集](@entry_id:268489)，它优先包含了低阶[交互作用](@entry_id:176776)（即少数几个 $i_j$ 较大而其余很小）和纯一维的贡献，而舍弃了所有维度上层级都很高的复杂[交互作用](@entry_id:176776)，这些通常对光滑函数贡献较小。

#### 从层级[基函数](@entry_id:170178)角度理解

Smolyak构造也可以通过层级[基函数](@entry_id:170178)来理解。在一维情况下，与嵌套节点和层级差分空间 $W_\ell = \text{range}(\Delta_\ell)$ 相关联，我们可以定义一套**层级[基函数](@entry_id:170178)** $\{\psi_{\ell,k}\}_{k \in \Delta K(\ell)}$。这些[基函数](@entry_id:170178) $\psi_{\ell,k}$ 的特点是，它在层级 $\ell$ 的“新”节点 $y_{\ell,k}$ 上取值为1，而在所有更低层级（$\ell'  \ell$）的节点以及同层级的其他新节点上取值为0。

多维的层级[基函数](@entry_id:170178) $\phi_{\boldsymbol{\ell},\boldsymbol{k}}(\boldsymbol{y})$ 则通过一维层级[基函数](@entry_id:170178)的张量积来构造：
$$
\phi_{\boldsymbol{\ell},\boldsymbol{k}}(\boldsymbol{y}) = \prod_{i=1}^d \psi_{\ell_i,k_i}(y_i)
$$
其中多重指标 $\boldsymbol{\ell}=(\ell_1, \dots, \ell_d)$ 代表层级，$\boldsymbol{k}=(k_1, \dots, k_d)$ 代表每个维度内新节点的索引。

[稀疏网格](@entry_id:139655)[插值函数](@entry_id:262791) $I_q[f](\boldsymbol{y})$ 就可以表示为这些层级[基函数](@entry_id:170178)的[线性组合](@entry_id:154743) [@problem_id:3447810]：
$$
I_q[f](\boldsymbol{y}) = \sum_{\boldsymbol{\ell} \in L_q} \sum_{\boldsymbol{k} \in \Delta K(\boldsymbol{\ell})} \alpha_{\boldsymbol{\ell},\boldsymbol{k}} \, \phi_{\boldsymbol{\ell},\boldsymbol{k}}(\boldsymbol{y})
$$
这里的[指标集](@entry_id:268489) $L_q$ 与Smolyak算子定义中的类似（例如，$L_q = \{\boldsymbol{\ell} \in \mathbb{N}_0^d : \|\boldsymbol{\ell}\|_1 \le q\}$，具体形式取决于层级定义）。系数 $\alpha_{\boldsymbol{\ell},\boldsymbol{k}}$ 被称为**层级余差（hierarchical surpluses）**。它们可以通过一个[递归公式](@entry_id:160630)计算得出，其物理意义是函数在[稀疏网格](@entry_id:139655)点 $\boldsymbol{y}_{\boldsymbol{\ell},\boldsymbol{k}}$ 上的真实值与用所有“更低层级”[基函数](@entry_id:170178)构成的插值在该点上的值的差。这再次体现了“新信息”的思想。

### 从插值到求积

构造了[稀疏网格](@entry_id:139655)[插值函数](@entry_id:262791) $I_q[f]$ 后，我们便可以用它来近似原函数的期望：
$$
\mathbb{E}[f] = \int_{\Gamma} f(\boldsymbol{y}) \rho(\boldsymbol{y}) \mathrm{d}\boldsymbol{y} \approx \int_{\Gamma} I_q[f](\boldsymbol{y}) \rho(\boldsymbol{y}) \mathrm{d}\boldsymbol{y}
$$
由于 $I_q[f]$ 是已知[基函数](@entry_id:170178)的[线性组合](@entry_id:154743)，其积分可以精确计算。这个过程等价于一个**[稀疏网格](@entry_id:139655)求积法则**。一个[稀疏网格](@entry_id:139655)求积算子 $Q_q^{(d)}$ 具有与插值算子 $\mathcal{A}_d^q$ 完全相同的Smolyak组合结构，只不过它组合的是一维求积法则的差分 $\Delta_i^{Q,(j)}$。

一个关键的理论与实践问题是：插值的积分是否等于对原函数使用求积法则？即，是否 $\int_{\Gamma} (\mathcal{A}_d^q[f]) \, \mathrm{d}\mu = Q_q^{(d)}[f]$ 对所有函数 $f$ 成立？答案是肯定的，前提是所使用的一维求积法则是**插值型的（interpolatory）** [@problem_id:3447843]。这意味着，在每个维度 $j$ 和每个层级 $i$，一维求积法则 $Q_i^{(j)}$ 必须使用与插值算子 $U_i^{(j)}$ 完全相同的节点集，并且其权重被精确地设置为对应[拉格朗日基](@entry_id:751105)函数的积分。在这种情况下，求积法则对于插值空间内的任何函数都是精确的，从而保证了上述等式的成立。[Clenshaw-Curtis求积](@entry_id:147876)法则就是一个典型的例子，它与基于[切比雪夫点](@entry_id:634016)的多项式插值是对应的插值型求积。

### 收敛性与[误差分析](@entry_id:142477)

[稀疏网格](@entry_id:139655)法的强大威力来源于它对特定[光滑性](@entry_id:634843)函数的优异逼近能力。

#### [光滑性](@entry_id:634843)假设：参数[解析性](@entry_id:140716)

[稀疏网格](@entry_id:139655)法之所以能获得高速收敛，其理论基础在于被逼近的函数——即参数到关注量的映射 $\boldsymbol{y} \mapsto Q(u(\boldsymbol{y}))$——具有高度的光滑性，特别是**参数解析性**。对于一类重要的PDE问题，即系数对参数呈仿射依赖（affine dependence）的情况：
$$
a(x, \boldsymbol{y}) = a_0(x) + \sum_{j=1}^{\infty} y_j a_j(x)
$$
可以证明，如果均值场 $a_0(x)$ 是一致正定的（即 $a_0(x) \ge a_{\min} > 0$），并且扰动项 $a_j(x)$ 的 $L^\infty$ 范数满足一定的可加性条件，那么解映射 $\boldsymbol{y} \mapsto u(\boldsymbol{y})$ 就可以从实数域的参数空间 $\Gamma$ [解析延拓](@entry_id:147225)到复数域中的一个多维椭圆或多圆盘区域内 [@problem_id:3447856]。这种解析性保证了基于[多项式逼近](@entry_id:137391)的方法能够取得极快的收敛速度。

#### [收敛率](@entry_id:146534)：战胜[维数灾难](@entry_id:143920)

当函数具有一定的[光滑性](@entry_id:634843)时（例如，有界混合导数），不同网格构造方法的收敛误差 $E$ 作为总计算点数 $N$ 的函数，其表现差异巨大 [@problem_id:3447830]：

-   **全[张量积网格](@entry_id:755861)**：其误差衰减形式为 $\mathcal{O}(N^{-r/d})$，其中 $r$ 是一维规则的代数[收敛阶](@entry_id:146394)数。这个形式是“[维数灾难](@entry_id:143920)”的直接体现：随着维度 $d$ 的增加，收敛变得异常缓慢。

-   **[稀疏网格](@entry_id:139655)**：其误差衰减形式为 $\mathcal{O}(N^{-r} (\log N)^{k})$，其中 $k$ 是一个与 $d$ 和 $r$ 相关的常数。尽管分母中存在对数项，但其[收敛率](@entry_id:146534)对维度 $d$ 的依赖性已大大减弱。对于给定的精度要求 $\epsilon$，全[张量积网格](@entry_id:755861)所需的点数 $N_{\mathrm{TP}} \sim \mathcal{O}(\epsilon^{-d/r})$，而[稀疏网格](@entry_id:139655)所需的点数 $N_{\mathrm{SG}} \sim \mathcal{O}(\epsilon^{-1/r} |\log \epsilon|^{d-1})$。这从根本上说明了[稀疏网格](@entry_id:139655)法为何能够有效地处理中高维度下的光滑函数逼近问题。

#### 稳定性：[Lebesgue常数](@entry_id:196241)

插值过程的稳定性由**[Lebesgue常数](@entry_id:196241)** $\Lambda$ 来衡量，它定义为插值算子在[无穷范数](@entry_id:637586)下的[算子范数](@entry_id:752960)。$\Lambda$ 的大小反映了[插值函数](@entry_id:262791)对被[插值函数](@entry_id:262791)微小扰动的敏感程度。对于基于嵌套Clenshaw-Curtis节点（[切比雪夫点](@entry_id:634016)的一种）的[稀疏网格](@entry_id:139655)插值，其[Lebesgue常数](@entry_id:196241) $\Lambda_{N,d}$ 随总点数 $N$ 和维度 $d$ 的增长是温和的，其上界为 $\mathcal{O}((\log N)^{d})$ [@problem_id:3447846]。这种对数多项式的增长保证了只要原函数足够光滑，[插值误差](@entry_id:139425)就不会被算子本身放大到失控的程度，从而确保了方法的稳定性和收敛性。

### 进阶策略与实际考量

标准的各向同性[稀疏网格](@entry_id:139655)法在实践中可以通过多种方式进行改进，以适应更复杂的问题。

#### 各向异性与维度[自适应稀疏网格](@entry_id:136425)

如前所述，源于K-L展开等方法的[参数化](@entry_id:272587)模型，其不同参数维度的重要性往往不同。**各向异性（anisotropic）[稀疏网格](@entry_id:139655)**正是利用了这一点，它在Smolyak构造的[指标集](@entry_id:268489)求和中为不同维度分配不同的权重，从而在“重要”方向上使用更高层级的规则。

**维度自适应（dimension-adaptive）**算法则将这一思想推向极致 [@problem_id:3447867]。它是一种贪心算法，从一个最小的[指标集](@entry_id:268489)（如只包含原点）开始，迭代地扩充网格。在每一步：
1.  维护一个当前已采纳的多重[指标集](@entry_id:268489) $\mathcal{I}$（要求是“向下闭合的”，即若一个指标在集合中，则其所有“前辈”指标也在集合中）及其“可采纳边界” $\mathcal{B}(\mathcal{I})$。
2.  对于边界上的每一个候选指标 $\boldsymbol{\alpha} \in \mathcal{B}(\mathcal{I})$，通过少量试探性计算，估计其对总误差（如总[方差](@entry_id:200758)）的贡献，例如 $c_{\boldsymbol{\alpha}} \approx \mathbb{E}[(\Delta_{\boldsymbol{\alpha}} Q)^2]$。
3.  选择贡献最大的那个候选指标 $\boldsymbol{\alpha}^* = \arg\max_{\boldsymbol{\alpha} \in \mathcal{B}(\mathcal{I})} c_{\boldsymbol{\alpha}}$，将其加入到 $\mathcal{I}$ 中。
4.  更新可采纳边界，并重复此过程，直到估计的总误差低于某个阈值。

这种自适应策略能够自动“发现”问题内在的各向异性和低维结构，将计算资源精确地投入到对结果影响最大的参数维度和交互作用上，从而实现极高的[计算效率](@entry_id:270255)。

#### 处理非光滑问题：多单元法

[稀疏网格](@entry_id:139655)法卓越的收敛性依赖于函数的光滑性。当参数到解的映射存在不连续或“扭结”（kinks）时，例如PDE系数在[参数空间](@entry_id:178581)中存在跳跃，全局多项式插值会遭遇[收敛率](@entry_id:146534)骤降和[Gibbs振荡](@entry_id:749902)现象。

为了解决这一难题，**[多单元随机配置法](@entry_id:752238)（multi-element stochastic collocation）**应运而生 [@problem_id:3447800]。其核心思想是**[分而治之](@entry_id:273215)**：
1.  **[参数空间](@entry_id:178581)剖分**：将参数空间 $\Gamma$ 剖分为若干个不重叠的子区域（“单元”）$\{\Gamma_e\}$。关键在于，剖分的边界必须与函数不光滑的位置对齐。
2.  **局部插值**：在每一个单元 $\Gamma_e$ 内部，函数是光滑的。因此，可以在每个单元上独立地构建一个高阶的局部[稀疏网格](@entry_id:139655)插值。
3.  **分片组合**：最终的全局代理模型是一个分片函数，由所有单元上的局部[插值函数](@entry_id:262791)拼接而成。

通过这种方式，[多项式插值](@entry_id:145762)的威力被限制在函数表现良好的区域内，避免了跨越不连续边界，从而在每个单元内部都能恢复高阶[收敛率](@entry_id:146534)。整个问题的总误差就分解为各个单元上的误差之和，使得对分片光滑函数的有效逼近成为可能。