## 引言
在高维[数值积分](@entry_id:136578)和模拟领域，蒙特卡洛（MC）方法因其简单性和对维度诅咒的相对免疫力而成为一种基石技术。然而，其基于[中心极限定理](@entry_id:143108)的概率性收敛速度 $O(n^{-1/2})$ 意味着要将误差减半，就需要将样本量增加四倍，这在追求高精度时会带来巨大的计算成本。这一固有的局限性催生了一个根本性的问题：我们能否设计出比随机抽样更“好”的样本点，从而系统性地加速收敛？

准[蒙特卡洛](@entry_id:144354)（Quasi-Monte Carlo, QMC）方法正是对这一问题的响亮回答。与依赖随机性的[蒙特卡洛方法](@entry_id:136978)不同，QMC采用确定性的、经过精心设计的“[低差异序列](@entry_id:139452)”，这些点集在积分域内[分布](@entry_id:182848)得异常均匀。其核心思想在于，通过用这种高度均匀的点集替代随机点，可以更有效地“探测”被积函数，从而以更少的样本点数达到更高的精度。本文旨在全面介绍准蒙特卡洛方法，从其数学基础到实际应用，为读者构建一个完整的知识框架。

在接下来的内容中，我们将分三个章节深入探索QMC的世界。首先，在**“原理与机制”**一章中，我们将揭示QMC的理论核心，从量化点集[均匀性](@entry_id:152612)的“差异度”概念，到连接误差与均匀性的[Koksma-Hlawka不等式](@entry_id:146879)，再到Halton和[Sobol'序列](@entry_id:139101)等[低差异序列](@entry_id:139452)的具体构造方法。接着，在**“应用与跨学科联系”**一章中，我们将展示QMC如何在计算金融、统计物理和工程学等领域解决实际的高维问题，并探讨如何通过问题变换和巧妙的[采样策略](@entry_id:188482)来最大化其性能。最后，**“动手实践”**部分提供了一系列精心设计的问题，旨在通过实际计算加深您对[Halton序列](@entry_id:750139)、[误差分析](@entry_id:142477)和[随机化QMC](@entry_id:754041)等关键概念的理解。通过本次学习，您将掌握超越传统[蒙特卡洛方法](@entry_id:136978)的强大工具。

## 原理与机制

在数值积分领域，[蒙特卡洛](@entry_id:144354)（Monte Carlo, MC）方法通过[随机抽样](@entry_id:175193)为高维问题提供了强大的解决方案。然而，其收敛速度受到概率论基本[极限定理](@entry_id:188579)的制约。准蒙特卡洛（Quasi-[Monte Carlo](@entry_id:144354), QMC）方法提供了一种根本不同的途径，旨在通过确定性地选择积分点来超越经典蒙特卡洛方法的收敛瓶颈。本章将深入探讨准[蒙特卡洛方法](@entry_id:136978)的核心原理与机制，阐明其如何从理论上实现卓越的性能，并介绍其关键构件，如均匀性度量、[误差界](@entry_id:139888)、[低差异序列](@entry_id:139452)的构造以及在高维问题中的应用之道。

### 从[方差](@entry_id:200758)控制到差异控制：QMC 的基本思想

标准[蒙特卡洛方法](@entry_id:136978)的核心是利用概率论中的大数定律（Law of Large Numbers, LLN）和[中心极限定理](@entry_id:143108)（Central Limit Theorem, CLT）。考虑积分 $I = \int_{[0,1]^d} f(\boldsymbol{x}) \,\mathrm{d}\boldsymbol{x}$，它可以被视为[随机变量](@entry_id:195330) $f(\boldsymbol{U})$ 的[期望值](@entry_id:153208)，其中 $\boldsymbol{U}$ 在 $[0,1]^d$ 上[均匀分布](@entry_id:194597)。MC 估计量是基于 $n$ 个[独立同分布](@entry_id:169067)（i.i.d.）样本 $\boldsymbol{U}_1, \dots, \boldsymbol{U}_n$ 的样本均值：
$$
\widehat{I}_n = \frac{1}{n} \sum_{i=1}^n f(\boldsymbol{U}_i)
$$
由于样本的独立性，该估计量是无偏的，即 $\mathbb{E}[\widehat{I}_n] = I$。其[均方根误差](@entry_id:170440)（Root-Mean-Square Error, RMSE）由[估计量的方差](@entry_id:167223)决定：
$$
\mathrm{RMSE}(\widehat{I}_n) = \sqrt{\mathbb{E}[(\widehat{I}_n - I)^2]} = \sqrt{\mathrm{Var}(\widehat{I}_n)} = \sqrt{\frac{\mathrm{Var}(f(\boldsymbol{U}))}{n}} = \frac{\sigma}{\sqrt{n}}
$$
其中 $\sigma^2 = \mathrm{Var}(f(\boldsymbol{U}))$ 是被积函数 $f$ 的[方差](@entry_id:200758)。[中心极限定理](@entry_id:143108)进一步揭示了误差的[分布](@entry_id:182848)特性，表明 $\sqrt{n}(\widehat{I}_n - I)$ 在[分布](@entry_id:182848)上收敛于一个均值为 0、[方差](@entry_id:200758)为 $\sigma^2$ 的正态分布。这确认了 MC 误差的随机波动量级为 $O(n^{-1/2})$。因此，MC 方法的精度本质上受制于被积函数的**[方差](@entry_id:200758)**，其收敛速度独立于维度 $d$，但其概率性的 $O(n^{-1/2})$ [收敛阶](@entry_id:146394)是其固有的局限性 [@problem_id:3313818]。

准蒙特卡洛方法则采取了截然不同的哲学。它用一个精心设计的确定性点集 $\boldsymbol{x}_1, \dots, \boldsymbol{x}_n$ 来代替随机样本，形成 QMC 估计量：
$$
\widetilde{I}_n = \frac{1}{n} \sum_{i=1}^n f(\boldsymbol{x}_i)
$$
由于点集是确定性的，$\widetilde{I}_n$ 是一个固定的数值，其误差 $\epsilon_n = \widetilde{I}_n - I$ 也是一个确定的量。因此，诸如“无偏性”或“[方差](@entry_id:200758)”之类的统计概念不再适用。QMC 的目标不再是控制[随机误差](@entry_id:144890)，而是要通过优化点集的[几何分布](@entry_id:154371)来最小化确定性的近似误差。QMC 的核心思想是，如果一个点集在 $[0,1]^d$ 中[分布](@entry_id:182848)得“尽可能均匀”，那么用这些点上的函数值的平均来近似整个区域上的积分，其结果应该会非常精确。这种思想将[误差控制](@entry_id:169753)的[焦点](@entry_id:174388)从统计上的**[方差](@entry_id:200758)控制**（variance control）转移到了几何上的**差异控制**（discrepancy control）[@problem_id:3313773]。

### 量化均匀性：差异度的概念

为了将“[均匀分布](@entry_id:194597)”这一直观概念数学化，QMC 理论引入了**差异度 (discrepancy)** 的概念。差异度旨在衡量一个有限点集偏离理想[均匀分布](@entry_id:194597)的程度。在众多差异度的定义中，**星差异度 (star-discrepancy)** $D_n^*$ 是最核心和最常用的一个。

给定点集 $P = \{\boldsymbol{x}_1, \dots, \boldsymbol{x}_n\} \subset [0,1]^d$，其星差异度定义为：
$$
D_n^*(P) = \sup_{\boldsymbol{t} \in [0,1]^d} \left| \frac{1}{n} \sum_{i=1}^n \mathbf{1}_{\{\boldsymbol{x}_i \in [0, \boldsymbol{t})\}} - \lambda([0, \boldsymbol{t})) \right|
$$
其中：
- $[0, \boldsymbol{t})$ 表示一个锚定在原点的 $d$ 维轴对齐半开超矩形，即 $[0, t_1) \times \dots \times [0, t_d)$。
- $\mathbf{1}_{\{\cdot\}}$ 是指示函数，当点 $\boldsymbol{x}_i$ 位于矩形 $[0, \boldsymbol{t})$ 内时取值为 1，否则为 0。
- $\frac{1}{n} \sum_{i=1}^n \mathbf{1}_{\{\boldsymbol{x}_i \in [0, \boldsymbol{t})\}}$ 是落入矩形 $[0, \boldsymbol{t})$ 内的点所占的**经验比例**。
- $\lambda([0, \boldsymbol{t})) = \prod_{j=1}^d t_j$ 是该矩形的**体积**（即勒贝格测度）。

从几何上看，星差异度 $D_n^*$ 是在所有可能的原点锚定超矩形上，点集经验比例与矩形体积之间差异的[绝对值](@entry_id:147688)的最大值。它捕捉了相对于均匀测度，点集在局部最严重的“过量”或“不足”。一个小的星差异度值意味着该点集在所有从原点出发的尺度上都[分布](@entry_id:182848)得非常均匀 [@problem_id:3313828]。

### 核心误差界：Koksma-Hlawka 不等式

差异度的重要性在于它通过 **Koksma-Hlawka 不等式**直接与 QMC 的[积分误差](@entry_id:171351)联系起来。该不等式为 QMC 方法的确定性误差提供了一个严格的理论[上界](@entry_id:274738)。对于一个在 Hardy-Krause 意义下[有界变差](@entry_id:139291)的函数 $f: [0,1]^d \to \mathbb{R}$，其 QMC [积分误差](@entry_id:171351)满足：
$$
\left| \int_{[0,1]^d} f(\boldsymbol{u}) \,\mathrm{d}\boldsymbol{u} - \frac{1}{n}\sum_{i=1}^n f(\boldsymbol{x}_i) \right| \le V_{\mathrm{HK}}(f) \cdot D_n^*(\{\boldsymbol{x}_i\})
$$
这个不等式优雅地将[积分误差](@entry_id:171351)分解为两个独立的部分：
1.  **$V_{\mathrm{HK}}(f)$**：函数的 **Hardy-Krause 变差**。这是一个衡量函数“摆动”或“复杂性”的量。一个变差较小的函数是相对“平滑”的。
2.  **$D_n^*$**：点集的**星差异度**。如前所述，这是一个纯粹的几何量，衡量点集的[均匀性](@entry_id:152612)。

Koksma-Hlawka 不等式清晰地表明，QMC 误差是由被积函数的内在复杂性和所选点集的几何[均匀性](@entry_id:152612)共同决定的。为了获得一个小的[积分误差](@entry_id:171351)，我们需要一个变差有限的函数和一个差异度小的点集。

**Hardy-Krause 变差** $V_{\mathrm{HK}}(f)$ 的定义较为复杂，它概括了一维 Jordan 变差的概念。其思想是将在所有低维坐标[子空间](@entry_id:150286)上的函数变差进行累加。具体地，令 $S = \{1, \dots, d\}$ 为坐标索引集。对于每个非空[子集](@entry_id:261956) $u \subseteq S$，$g_u(x_u) = f(x_u, \mathbf{1}_{S \setminus u})$ 表示将 $f$ 中不属于 $u$ 的坐标固定为 1 后得到的函数。Hardy-Krause 变差定义为：
$$
V_{\mathrm{HK}}(f) = \sum_{\emptyset \neq u \subseteq \{1,\dots,d\}} V^{(|u|)}(g_u)
$$
其中 $V^{(k)}(g)$ 是 $k$ 维函数 $g$ 的 Vitali 变差，它通过对 $[0,1]^k$ 的任意剖分，累加函数在每个小矩形上的[混合差分](@entry_id:750423)的[绝对值](@entry_id:147688)来计算 [@problem_id:3313817]。这个定义虽然技术性强，但其核心思想是量化函数在各个维度及其组合上的“变化总量”。

### 构造均匀点集：[低差异序列](@entry_id:139452)

Koksma-Hlawka 不等式指明了 QMC 的发展方向：构造星差异度 $D_n^*$ 尽可能小的点集。所谓**[低差异序列](@entry_id:139452) (low-discrepancy sequence)**，就是一个无穷点序列，其前 $N$ 个点的星差异度 $D_N^*$ 随着 $N$ 的增大而快速趋于零，其收敛速度要优于标准 MC 方法的概率性[收敛速度](@entry_id:636873)。

对于许多著名的[低差异序列](@entry_id:139452)，如 Halton 序列、Sobol' 序列和 Faure 序列，其星差异度满足如下的[上界](@entry_id:274738)：
$$
D_N^* \le C_d \frac{(\log N)^d}{N}
$$
其中 $C_d$ 是一个仅依赖于维度 $d$ 的常数。这个 $O\left(\frac{(\log N)^d}{N}\right)$ 的收敛阶在 $N \to \infty$ 时，渐近地优于 MC 的 $O(N^{-1/2})$。这正是 QMC 方法在理论上超越 MC 方法的根源 [@problem_id:3313835]。下面我们介绍两种构造这类序列的主流方法。

#### 基于数论的方法：Van der Corput 和 Halton 序列

许多[低差异序列](@entry_id:139452)的构造始于一维的 **Van der Corput 序列**。其构造基于**根[反函数](@entry_id:141256) (radical-inverse function)** $\phi_b(n)$。给定一个整[数基](@entry_id:634389) $b \ge 2$，任何非负整数 $n$ 都可以唯一地表示为 $b$ [进制](@entry_id:634389)形式：$n = \sum_{k=0}^{m} a_k b^k$。根反函数通过“翻转”这个展开式的小数点来定义：
$$
u_n = \phi_b(n) = \sum_{k=0}^{m} a_k b^{-(k+1)}
$$
例如，在基 $b=2$ 下，整数 $n=6 = (110)_2$ 的根反函数值为 $\phi_2(6) = 0 \cdot 2^{-1} + 1 \cdot 2^{-2} + 1 \cdot 2^{-3} = 0 + 0.25 + 0.125 = 0.375 = (0.011)_2$。通过对 $n=0, 1, 2, \dots$ 依次进行这种变换，我们便得到了 Van der Corput 序列。这个看似简单的操作，却能生成一个在一维区间 $[0,1)$ 上具有极好[均匀分布](@entry_id:194597)特性的序列，其差异度满足 $D_N^* = O(\frac{\log N}{N})$。这一性质保证了序列是[均匀分布](@entry_id:194597)的，即对于任意子区间，点落入其中的频率都趋近于该区间的长度 [@problem_id:3313795]。

为了将这个思想推广到 $d$ 维，**Halton 序列**应运而生。它为每个维度 $j=1, \dots, d$ 选择一个不同的基 $b_j$，然后将第 $n$ 个点定义为：
$$
\boldsymbol{x}_n = (\phi_{b_1}(n), \phi_{b_2}(n), \dots, \phi_{b_d}(n))
$$
一个至关重要的条件是，这些基 $b_1, \dots, b_d$ 必须是**[两两互质](@entry_id:154147)**的整数。如果两个维度使用相同的基（或非[互质](@entry_id:143119)的基），它们的坐标之间会产生强烈的线性相关性，导致点集聚集在低维[子空间](@entry_id:150286)上，从而破坏其在高维空间中的[均匀性](@entry_id:152612)。例如，若 $b_1=b_2$，则所有点都将落在主对角线 $x_1=x_2$ 上。在实践中，为了使差异度[上界](@entry_id:274738)中的常数 $C_d$ 尽可能小，通常选择前 $d$ 个素数作为基 [@problem_id:3313836]。

#### 基于代数的方法：数字网与数字序列

另一大类低差异点集的构造方法是基于[有限域](@entry_id:142106)上的线性代数，称为**数字网 (digital nets)** 和 **数字序列 (digital sequences)**。Sobol' 序列是其中最著名的例子。

这种构造方法的核心思想如下：
1.  选择一个素数幂基 $b$ 和维度 $s$。
2.  为每个维度 $j=1, \dots, s$ 指定一个**[生成矩阵](@entry_id:275809)** $C_j$。这些矩阵的元素来自有限域 $\mathbb{F}_b$。
3.  对于一个整数索引 $n$，首先获取其 $b$ [进制](@entry_id:634389)表示的数字向量 $\boldsymbol{a} = (a_0, a_1, \dots, a_{m-1})^\top$。
4.  通过在[有限域](@entry_id:142106) $\mathbb{F}_b$ 上的[矩阵向量乘法](@entry_id:140544)，为每个维度生成一个输出数字向量：$\boldsymbol{y}_j = C_j \boldsymbol{a} \pmod b$。
5.  最后，将每个输出数字向量 $\boldsymbol{y}_j = (y_{j,1}, \dots, y_{j,m})^\top$ 解释为 $b$ [进制](@entry_id:634389)小数，从而得到该维度的坐标：$x_j = \sum_{k=1}^m y_{j,k} b^{-k}$。

让我们通过一个具体的例子来理解这个过程 [@problem_id:3313784]。设基 $b=3$，维度 $s=2$，并使用以下两个 $3 \times 3$ 的[生成矩阵](@entry_id:275809)：
$$
C_1=\begin{pmatrix} 1  0  2 \\ 0  1  1 \\ 2  2  0 \end{pmatrix}, \quad C_2=\begin{pmatrix} 1  2  1 \\ 2  0  1 \\ 0  1  2 \end{pmatrix}
$$
我们来计算索引 $n=8$ 对应的二维点。
- **步骤 3**: 将 $n=8$ 转换为基 3 表示：$8 = 2 \cdot 3^0 + 2 \cdot 3^1 + 0 \cdot 3^2 = (022)_3$。其数字向量为 $\boldsymbol{a} = (a_0, a_1, a_2)^\top = (2, 2, 0)^\top$。
- **步骤 4**: 在 $\mathbb{F}_3$ 上进行矩阵乘法：
  - 对维度 1：$\boldsymbol{y}_1 = C_1 \boldsymbol{a} = \begin{pmatrix} 1  0  2 \\ 0  1  1 \\ 2  2  0 \end{pmatrix} \begin{pmatrix} 2 \\ 2 \\ 0 \end{pmatrix} = \begin{pmatrix} 2 \\ 2 \\ 8 \end{pmatrix} \equiv \begin{pmatrix} 2 \\ 2 \\ 2 \end{pmatrix} \pmod 3$。
  - 对维度 2：$\boldsymbol{y}_2 = C_2 \boldsymbol{a} = \begin{pmatrix} 1  2  1 \\ 2  0  1 \\ 0  1  2 \end{pmatrix} \begin{pmatrix} 2 \\ 2 \\ 0 \end{pmatrix} = \begin{pmatrix} 6 \\ 4 \\ 2 \end{pmatrix} \equiv \begin{pmatrix} 0 \\ 1 \\ 2 \end{pmatrix} \pmod 3$。
- **步骤 5**: 将输出数字向量转换为坐标：
  - $x_1 = \frac{2}{3^1} + \frac{2}{3^2} + \frac{2}{3^3} = \frac{18+6+2}{27} = \frac{26}{27}$。
  - $x_2 = \frac{0}{3^1} + \frac{1}{3^2} + \frac{2}{3^3} = \frac{0+3+2}{27} = \frac{5}{27}$。
因此，索引 $n=8$ 对应的点是 $(\frac{26}{27}, \frac{5}{27})$。通过精心选择[生成矩阵](@entry_id:275809)，可以确保生成的点集具有极低的差异度。

### “维度灾难”与[有效维度](@entry_id:146824)

尽管 QMC 在理论上具有更优的[收敛阶](@entry_id:146394)，但 $O\left(\frac{(\log N)^d}{N}\right)$ 中的 $(\log N)^d$ 项表明，误差[上界](@entry_id:274738)随着维度 $d$ 的增加而迅速增长。这似乎预示着 QMC 方法会遭遇严重的“[维度灾难](@entry_id:143920)”，使其在高维应用中失效。然而，实践表明 QMC 在许多高维问题中（例如[金融工程](@entry_id:136943)，维度可达数百）依然远胜于 MC。

解释这一现象的关键在于**[有效维度](@entry_id:146824) (effective dimension)** 的概念。这个概念源于对被积函数 $f$ 的 **[ANOVA](@entry_id:275547) (Analysis of Variance) 分解**。对于[平方可积函数](@entry_id:200316) $f \in L^2([0,1]^s)$，它可以被唯一地分解为一系列正交分量的和：
$$
f(\boldsymbol{x}) = \sum_{u \subseteq \{1,\dots,s\}} f_u(\boldsymbol{x}_u)
$$
其中每个分量 $f_u$ 仅依赖于索引集 $u$ 中的变量。由于正交性，函数的总[方差](@entry_id:200758)可以分解为各分量[方差](@entry_id:200758)之和：
$$
\mathrm{Var}(f) = \sum_{\emptyset \neq u \subseteq \{1,\dots,s\}} \mathrm{Var}(f_u)
$$
[有效维度](@entry_id:146824)衡量的是函数[方差](@entry_id:200758)在多大程度上集中于低阶或少数几个变量的相互作用上。它有两种主要定义：
- **叠加意义下的[有效维度](@entry_id:146824) (Effective dimension in the superposition sense)**：在阈值 $\tau \in (0,1)$下，它是最小的整数 $d$，使得所有涉及变量个数不超过 $d$ 的分量所贡献的[方差](@entry_id:200758)之和，占总[方差](@entry_id:200758)的比例至少为 $\tau$。
- **截断意义下的[有效维度](@entry_id:146824) (Effective dimension in the truncation sense)**：在给定坐标排序和阈值 $\tau$ 下，它是最小的整数 $d$，使得仅依赖于前 $d$ 个变量的分量所贡献的[方差](@entry_id:200758)之和，占总[方差](@entry_id:200758)的比例至少为 $\tau$。

QMC 成功的秘诀在于：许多实际问题中的高维函数，其[有效维度](@entry_id:146824)往往很低。这意味着函数的大部分“变化”或“重要性”都由少数几个变量或它们之间的低阶相互作用所驱动。[低差异序列](@entry_id:139452)的一个优良特性是它们在低维投影上具有极好的均匀性。因此，即使名义维度 $s$ 很高，只要函数的[有效维度](@entry_id:146824)很低，QMC [积分误差](@entry_id:171351)主要由这些低维投影上的表现决定，从而能够“战胜”[维度灾难](@entry_id:143920)，取得优异的性能 [@problem_id:3313774]。

### 实用[误差估计](@entry_id:141578)：[随机化](@entry_id:198186)的作用

确定性 QMC 方法的一个主要实践障碍是[误差估计](@entry_id:141578)。由于点集是固定的，[积分误差](@entry_id:171351) $\widetilde{I}_n - I$ 是一个未知但确定的常数。这与 MC 方法不同，后者可以通过样本[方差](@entry_id:200758)来估计随机误差的大小并构造置信区间。虽然 Koksma-Hlawka 不等式提供了误差[上界](@entry_id:274738)，但由于其中涉及的 Hardy-Krause 变差 $V_{\mathrm{HK}}(f)$ 对大多数函数都极难计算，因此该界在实践中几乎无法用于给出具体的误差数值 [@problem_id:3313808]。

为了解决这个问题，**[随机化](@entry_id:198186)准蒙特卡洛 (Randomized Quasi-Monte Carlo, RQMC)** 方法被提了出来。其核心思想是为确定性的低差异点集引入可控的随机性，从而恢复[统计误差](@entry_id:755391)估计的能力，同时保持 QMC 的高[收敛率](@entry_id:146534)。

一个常见的[随机化](@entry_id:198186)技术是**随机[移位](@entry_id:145848) (random shift)**。给定一个确定性点集 $\{\boldsymbol{x}_1, \dots, \boldsymbol{x}_n\}$，生成一个随机向量 $\boldsymbol{\Delta} \sim \mathrm{Unif}([0,1]^d)$，然后构造一个新的随机化点集：
$$
\{\boldsymbol{X}_1, \dots, \boldsymbol{X}_n\}, \quad \text{其中 } \boldsymbol{X}_i = (\boldsymbol{x}_i + \boldsymbol{\Delta}) \pmod 1
$$
其中模 1 运算是逐分量进行的。这种[随机化](@entry_id:198186)有两个关键效果：
1.  **保持低差异结构**：随机[移位](@entry_id:145848)是一种保持点间相对位置的[刚性变换](@entry_id:140326)，因此随机化后的点集仍然保持着原有的低差异特性。
2.  **恢复概率框架**：每个随机化的点 $\boldsymbol{X}_i$ 在 $[0,1]^d$ 上都是[均匀分布](@entry_id:194597)的。这使得 RQMC 估计量 $\hat{I}_{\mathrm{RQMC}} = \frac{1}{n} \sum f(\boldsymbol{X}_i)$ 成为一个对原积分 $I$ 的**[无偏估计量](@entry_id:756290)**。

通过独立地重复 $m$ 次随机化过程，我们可以得到 $m$ 个独立同分布的积分估计值 $\hat{I}_{\mathrm{RQMC}}^{(1)}, \dots, \hat{I}_{\mathrm{RQMC}}^{(m)}$。这时，我们就可以像处理标准 MC 结果一样，对这 $m$ 个值计算样本均值和样本[方差](@entry_id:200758)，并应用[中心极限定理](@entry_id:143108)来构造置信区间。RQMC 的[方差](@entry_id:200758)通常远小于同样点数的 MC [方差](@entry_id:200758)，这意味着它能用更少的计算量达到同样的精度。

综上所述，RQMC 巧妙地结合了 QMC 的高[收敛率](@entry_id:146534)和 MC 的[统计误差](@entry_id:755391)估计能力，使其成为一种既高效又可靠的现代[数值积分](@entry_id:136578)工具 [@problem_id:3313808]。