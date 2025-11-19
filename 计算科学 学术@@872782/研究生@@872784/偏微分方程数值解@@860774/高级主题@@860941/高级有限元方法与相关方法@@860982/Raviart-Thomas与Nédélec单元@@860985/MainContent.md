## 引言
在[偏微分方程](@entry_id:141332)的数值求解中，尤其是在模拟[电磁场](@entry_id:265881)或流体速度等矢量场时，传统的有限元方法常常因施加了过强的连续性约束而失效，导致产生非物理的[伪解](@entry_id:275285)。为了解决这一核心难题，研究人员开发了专门的向量有限元，其中Raviart-Thomas (RT) 与Nédélec (ND) 元是最为基础和关键的两种。它们的设计初衷就是为了精确地模拟矢量场在物理上应满足的法向或切向连续性，从而保证数值解的稳定性和准确性。

本文将带领读者全面深入地理解这两类重要的有限元。在“原理与机制”一章中，我们将从$H(\mathrm{div})$和$H(\mathrm{curl})$函数空间出发，揭示其构造的核心思想和与[de Rham复形](@entry_id:178752)的深刻联系。随后，在“应用与跨学科联系”一章中，我们将展示这些“保结构”方法如何在[计算电磁学](@entry_id:265339)、地球物理和[固体力学](@entry_id:164042)等前沿领域中解决实际问题。最后，通过“动手实践”部分的精选练习，读者将有机会亲手构建和分析这些单元，将理论知识转化为实践能力。

## 原理与机制

在[数值求解偏微分方程](@entry_id:634353)，特别是那些源于电磁学和[流体力学](@entry_id:136788)的方程时，我们遇到的未知量通常是矢量场，例如[电场](@entry_id:194326)、[磁通量密度](@entry_id:194922)或流体速度。简单地对矢量场的每个分量使用标准的（拉格朗日）有限元方法，往往会导致数值解出现非物理的[振荡](@entry_id:267781)或[伪模式](@entry_id:163321)（spurious modes）。这些问题的根源在于，标准的有限元空间强制了过强的连续性（即所有分量在单元间都连续），而这与矢量场在物理上应满足的内在约束（例如法向或切向连续性）不符。

为了解决这一根本性问题，研究人员发展了特殊的有限元，即[混合有限元](@entry_id:178533)或向量有限元。其中，**Raviart-Thomas (RT) 元**和**Nédélec 元**是最为重要和基础的两族。本章将深入探讨这两类有限元的基本原理和工作机制。我们将从它们所依赖的数学框架——特定的 Sobolev 空间——出发，阐明其构造原则，揭示其与 de Rham 复形的深刻联系，并讨论在实际计算中必须处理的映射和定向问题。

### 矢量 Sobolev 空间：$H(\mathrm{div})$ 与 $H(\mathrm{curl})$

传统有限元方法所基于的数学框架是 Sobolev 空间 $H^1(\Omega)$，它要求函数本身及其一阶[弱导数](@entry_id:189356)都平方可积。对于矢量场 $\boldsymbol{v}$，其自然推广是 $(H^1(\Omega))^d$，但这要求 $\boldsymbol{v}$ 的每个分量都在单元间连续。然而，许多物理定律并不要求如此强的连续性。

例如，在无界面[电荷](@entry_id:275494)的介质分界面上，[电位移矢量](@entry_id:197092) $\boldsymbol{D}$ 的法向分量 $\boldsymbol{D} \cdot \boldsymbol{n}$ 是连续的，而其切向分量通常不连续。类似地，在无[表面电流](@entry_id:261791)的介质分界面上，[电场](@entry_id:194326)强度 $\boldsymbol{E}$ 的切向分量 $\boldsymbol{n} \times \boldsymbol{E}$ 是连续的，而其法向分量通常不连续。这些物理现象启发我们定义更合适的[函数空间](@entry_id:143478)。

**$H(\mathrm{div})$ 空间**（或称为散度空间）是为那些散度有物理意义的矢量场（如 $\boldsymbol{D}$, $\boldsymbol{B}$, $\boldsymbol{J}$）设计的。它定义为：
$$
H(\mathrm{div};\Omega) = \{ \boldsymbol{v} \in (L^2(\Omega))^d : \nabla \cdot \boldsymbol{v} \in L^2(\Omega) \}
$$
这是一个 Hilbert 空间，其范数为 $\| \boldsymbol{v} \|_{H(\mathrm{div})} = (\| \boldsymbol{v} \|^2_{L^2} + \| \nabla \cdot \boldsymbol{v} \|^2_{L^2})^{1/2}$。对于 $H(\mathrm{div})$ 空间中的函数，其边界上的**法向迹（normal trace）** $\boldsymbol{v} \cdot \boldsymbol{n}$ 是有定义的。这可以通过[格林公式](@entry_id:173118)（Green's identity）以弱形式来理解。对于[光滑函数](@entry_id:267124) $\boldsymbol{v}$ 和标量函数 $w$，我们有：
$$
\int_\Omega (\nabla \cdot \boldsymbol{v}) w \, dx + \int_\Omega \boldsymbol{v} \cdot \nabla w \, dx = \int_{\partial \Omega} (\boldsymbol{v} \cdot \boldsymbol{n}) w \, dS
$$
对于一般的 $\boldsymbol{v} \in H(\mathrm{div};\Omega)$ 和 $w \in H^1(\Omega)$，上式左侧定义了一个关于 $w$ 的[有界线性泛函](@entry_id:271069)。这个泛函的值仅依赖于 $w$ 在边界 $\partial \Omega$ 上的迹。因此，它可以在对偶意义下定义 $\boldsymbol{v}$ 的法向迹 $\gamma_n(\boldsymbol{v})$。这个[迹算子](@entry_id:183665)是一个从 $H(\mathrm{div};\Omega)$ 到一个较弱的边界空间 $H^{-1/2}(\partial \Omega)$ 的[有界线性算子](@entry_id:180446) [@problem_id:3438126] [@problem_id:3334033]。$H(\mathrm{div})$ **协调（conforming）**的离散化关键在于保证分片多项式函数在所有内部单元边界上的法向迹是单值的，即法向分量连续。

**$H(\mathrm{curl})$ 空间**（或称为旋度空间）则是为那些旋度有物理意义的矢量场（如 $\boldsymbol{E}$, $\boldsymbol{H}$）设计的。它定义为：
$$
H(\mathrm{curl};\Omega) = \{ \boldsymbol{v} \in (L^2(\Omega))^d : \nabla \times \boldsymbol{v} \in (L^2(\Omega))^d \}
$$
其范数为 $\| \boldsymbol{v} \|_{H(\mathrm{curl})} = (\| \boldsymbol{v} \|^2_{L^2} + \| \nabla \times \boldsymbol{v} \|^2_{L^2})^{1/2}$。与 $H(\mathrm{div})$ 空间类似，通过广义的[斯托克斯定理](@entry_id:264534)（Stokes' theorem），可以为 $H(\mathrm{curl})$ 空间中的函数定义**切向迹（tangential trace）**。对于[光滑函数](@entry_id:267124) $\boldsymbol{v}$ 和 $\boldsymbol{w}$，我们有：
$$
\int_\Omega (\nabla \times \boldsymbol{v}) \cdot \boldsymbol{w} \, dx - \int_\Omega \boldsymbol{v} \cdot (\nabla \times \boldsymbol{w}) \, dx = \int_{\partial \Omega} (\boldsymbol{n} \times \boldsymbol{v}) \cdot \boldsymbol{w} \, dS
$$
这同样允许我们在[弱形式](@entry_id:142897)下定义切向迹 $\gamma_t(\boldsymbol{v}) = \boldsymbol{n} \times \boldsymbol{v}|_{\partial \Omega}$。该[迹算子](@entry_id:183665)将 $H(\mathrm{curl};\Omega)$ 映射到一个边界上的切向矢量场空间，例如在三维情况下是 $H^{-1/2}(\mathrm{div}_\Gamma, \Gamma)$ [@problem_id:3334033]。$H(\mathrm{curl})$ **协调**的离散化关键就在于保证分片多项式函数在所有内部单元边界上的切向迹是单值的，即切向分量连续 [@problem_id:3329984]。

### Raviart-Thomas 元与 Nédélec 元的构造

Raviart-Thomas 元和 Nédélec 元正是为了满足上述 $H(\mathrm{div})$ 和 $H(\mathrm{curl})$ 的协调性要求而精心设计的。

#### Raviart-Thomas (RT) 元

**Raviart-Thomas 元** 是一族 $H(\mathrm{div})$-协调的有限元。其核心思想是通过合理选择局部[多项式空间](@entry_id:144410)和自由度（degrees of freedom, DoFs）来确保法向分量的连续性。

在二维的[三角形单元](@entry_id:167871) $K$ 上，阶数为 $k$ 的局部 RT 空间 $\mathrm{RT}_k(K)$ 定义为：
$$
\mathrm{RT}_k(K) = (\mathbb{P}_k(K))^2 + \boldsymbol{x} \mathbb{P}_k(K)
$$
其中 $\mathbb{P}_k(K)$ 是在 $K$ 上的最高次数为 $k$ 的标量[多项式空间](@entry_id:144410)，$(\mathbb{P}_k(K))^2$ 是其对应的矢量[多项式空间](@entry_id:144410)，$\boldsymbol{x} = (x,y)$ 是位置矢量。这个定义的精妙之处在于，对于该空间中的任意矢量场 $\boldsymbol{v}$，其散度 $\nabla \cdot \boldsymbol{v}$ 是一个次数最高为 $k$ 的多项式，即 $\nabla \cdot \boldsymbol{v} \in \mathbb{P}_k(K)$。同时，其在任意边 $e$ 上的法向迹 $\boldsymbol{v} \cdot \boldsymbol{n}_e$ 也是一个次数最高为 $k$ 的一维多项式。

这个局部空间的维数可以通过简单的多项式空间维数计算得到。例如，在二维情况下，其维数为 $(k+1)(k+3)$ [@problem_id:3438155]。

为了确保全局的 $H(\mathrm{div})$-协调性，$\mathrm{RT}_k$ 元的自由度被定义为：
1.  在每个（$d-1$ 维）面上，法向分量 $\boldsymbol{v} \cdot \boldsymbol{n}$ 对 $\mathbb{P}_k$ 空间中所有多项式的矩（即积分）。
2.  在单元内部，矢量场 $\boldsymbol{v}$ 对次数低于某个值的矢量[多项式空间](@entry_id:144410)的矩。

由于相邻单元共享同一个面上的法向矩自由度，这就强制了法向分量 $\boldsymbol{v} \cdot \boldsymbol{n}$ 在该面上是唯一的，从而保证了全局的法向连续性。

**示例：最低阶 RT 元 ($RT_0$)**

考虑二维参考三角形 $\widehat{T}$，其顶点为 $(0,0), (1,0), (0,1)$。$RT_0(\widehat{T})$ 空间由形如 $\boldsymbol{v}(\boldsymbol{x}) = \boldsymbol{a} + b\boldsymbol{x}$ 的矢量场构成，其中 $\boldsymbol{a} \in \mathbb{R}^2$ 是常数矢量， $b \in \mathbb{R}$ 是标量。其维数为 $(0+1)(0+3)=3$。自由度是通量，即在三条边上的法向分量积分。
与边 $\widehat{e}_1$（从 $(0,0)$ 到 $(1,0)$，法向量 $\widehat{\boldsymbol{n}}_1=(0,-1)$）相关的[基函数](@entry_id:170178) $\widehat{\phi}_1$ 满足 $\int_{\widehat{e}_1} \widehat{\phi}_1 \cdot \widehat{\boldsymbol{n}}_1 ds = 1$ 以及在另外两条边上的通量为 $0$。通过求解一个简单的线性方程组，我们可以确定这个[基函数](@entry_id:170178)为 $\widehat{\phi}_1(x,y) = (x, y-1)$。这个具体的例子清晰地展示了[基函数](@entry_id:170178)如何与几何和自由度定义紧密联系在一起 [@problem_id:3438157]。

值得注意的是，还存在其他 $H(\mathrm{div})$-[协调元](@entry_id:178102)族，如 **Brezzi-Douglas-Marini (BDM)** 元和 **Brezzi-Douglas-Fortin-Marini (BDFM)** 元。它们在局部[多项式空间](@entry_id:144410)和自由度定义上与 RT 元有所不同，从而导致了不同的散度空间和收敛性质，但构造思想是类似的 [@problem_id:3438139]。

#### Nédélec 元

**Nédélec 元**（也称为**边元**，edge elements）是一族 $H(\mathrm{curl})$-协调的有限元。其构造思想与 RT 元对偶，旨在通过自由度的设置来保证切向分量的连续性 [@problem_id:3438126]。

在三维[四面体单元](@entry_id:168311) $K$ 上，最低阶 Nédélec 元（第一类）的局部空间包含次数为 $1$ 的矢量多项式。其自由度被定义为：
1.  在每个边 $e$ 上，切向分量 $\boldsymbol{v} \cdot \boldsymbol{t}$ 的积分（环量），即 $\int_e \boldsymbol{v} \cdot \boldsymbol{t} \, ds$。

由于相邻单元共享边，将自由度与全局唯一的边关联，就保证了 $\boldsymbol{v} \cdot \boldsymbol{t}$ 在整条边上是连续的。对于适当选择的[多项式空间](@entry_id:144410)，这足以保证在整个共享面上切向分量的连续性，从而实现全局的 $H(\mathrm{curl})$-协调性 [@problem_id:3329984]。更高阶的 Nédélec 元则在边、面和体上定义了更多的矩自由度，以匹配更高次的多项式空间。

### de Rham 复形：统一的数学结构

Raviart-Thomas 元和 Nédélec 元并非孤立的发明，它们是嵌入在一个深刻的数学结构——**de Rham 复形（de Rham complex）**——中的离散对应物。这个结构不仅统一了梯度、[旋度和散度](@entry_id:269913)算子，还为避免[伪模式](@entry_id:163321)提供了理论基础。

在三维可缩（contractible）区域 $\Omega$ 上，连续的 de Rham 复形是一个算[子序列](@entry_id:147702)：
$$
H^1(\Omega) \xrightarrow{\nabla} H(\mathrm{curl};\Omega) \xrightarrow{\nabla \times} H(\mathrm{div};\Omega) \xrightarrow{\nabla \cdot} L^2(\Omega) \to 0
$$
这个序列被称为**[正合序列](@entry_id:151503)（exact sequence）**，意味着在每一步，前一个算子的像空间（range）恰好等于后一个[算子的核](@entry_id:272757)空间（kernel）。例如，$\mathrm{range}(\nabla) = \ker(\nabla \times)$，这正是矢量分析中的基本恒等式“[梯度的旋度](@entry_id:274168)为零”在函数空间层面的体现。同样，$\mathrm{range}(\nabla \times) = \ker(\nabla \cdot)$ 对应于“[旋度的散度](@entry_id:271562)为零”。

这个序列与电磁学完美对应 [@problem_id:3313859]：
- $H^1(\Omega)$：容纳[标量势](@entry_id:276177)（如[静电势](@entry_id:188370) $\phi$）。
- $H(\mathrm{curl};\Omega)$：容纳[电场](@entry_id:194326) $\boldsymbol{E}$ 或[磁场](@entry_id:153296) $\boldsymbol{H}$。
- $H(\mathrm{div};\Omega)$：容纳[电位移](@entry_id:269383) $\boldsymbol{D}$ 或[磁感应强度](@entry_id:144179) $\boldsymbol{B}$。
- $L^2(\Omega)$：容纳[电荷密度](@entry_id:144672) $\rho$。

有限元方法的目标是构造一个离散的 de Rham 复形，由有限元空间 $S_h \subset H^1(\Omega), N_h \subset H(\mathrm{curl};\Omega), RT_h \subset H(\mathrm{div};\Omega), Q_h \subset L^2(\Omega)$ 构成，并保持正合性。使用[拉格朗日元](@entry_id:168612)、Nédélec 元和 Raviart-Thomas 元的特定组合可以实现这一点。

一个至关重要的性质是**[交换图](@entry_id:747516)（commuting diagram）**属性。这意味着存在从连续空间到离散空间的投影（或插值）算子 $\Pi$，它与微分算子“交换”，例如 [@problem_id:3438139] [@problem_id:3438126]：
$$
\nabla \times (\Pi^1 \boldsymbol{v}) = \Pi^2 (\nabla \times \boldsymbol{v})
$$
其中 $\Pi^1: H(\mathrm{curl};\Omega) \to N_h$ 和 $\Pi^2: H(\mathrm{div};\Omega) \to RT_h$ 是投影算子。

当离散复形是正合的，并且存在交换投影时，离散系统就能精确地再现[连续系统](@entry_id:178397)的核心结构。这尤其在求解[特征值问题](@entry_id:142153)（如麦克斯韦[谐振腔](@entry_id:274488)问题）时至关重要，因为它能从根本上消除由不恰当离散化引入的、非物理的**[伪模式](@entry_id:163321)** [@problem_id:3350344]。

### 实际实现中的考虑：映射与定向

将理论上的有限元应用于实际问题（特别是对于弯曲边界或[非均匀网格](@entry_id:752607)）时，必须处理从标准[参考单元](@entry_id:168425)到物理单元的[几何映射](@entry_id:749852)。

#### Piola 变换

从参考单元 $\widehat{K}$ 到物理单元 $K$ 的映射 $F: \widehat{K} \to K$ 由[雅可比矩阵](@entry_id:264467) $\mathbf{J}$ 描述。为了在映射后保持矢量场的关键物理性质（即法向通量或切向环量），我们需要使用特殊的变换，即 **Piola 变换（Piola transform）**。存在两种主要的 Piola 变换 [@problem_id:3438186]：

1.  **协变 Piola 变换（Covariant Piola Transform）**：用于 $H(\mathrm{curl})$ 空间（Nédélec 元）。其定义为 $\boldsymbol{w}(\boldsymbol{x}) = \mathbf{J}^{-T} \widehat{\boldsymbol{w}}(\widehat{\boldsymbol{x}})$，其中 $\widehat{\boldsymbol{x}} = F^{-1}(\boldsymbol{x})$。这个变换的设计目的是保持切向分量的积分不变：
    $$
    \int_e \boldsymbol{w} \cdot \boldsymbol{t} \, ds = \int_{\widehat{e}} \widehat{\boldsymbol{w}} \cdot \widehat{\boldsymbol{t}} \, d\widehat{s}
    $$

2.  **[逆变](@entry_id:192290) Piola 变换（Contravariant Piola Transform）**：用于 $H(\mathrm{div})$ 空间（Raviart-Thomas 元）。其定义为 $\boldsymbol{v}(\boldsymbol{x}) = \frac{1}{\det \mathbf{J}} \mathbf{J} \widehat{\boldsymbol{v}}(\widehat{\boldsymbol{x}})$。这个变换的设计目的是保持法向分量的积分不变（即通量守恒）：
    $$
    \int_f \boldsymbol{v} \cdot \boldsymbol{n} \, dS = \int_{\widehat{f}} \widehat{\boldsymbol{v}} \cdot \widehat{\boldsymbol{n}} \, d\widehat{S}
    $$
    同时，该变换还保证了[散度算子](@entry_id:265975)的一个优美变换性质：$\nabla_{\boldsymbol{x}} \cdot \boldsymbol{v} = \frac{1}{\det \mathbf{J}} \nabla_{\widehat{\boldsymbol{x}}} \cdot \widehat{\boldsymbol{v}}$。

需要注意的是，当映射 $F$ 非仿射时（即物理单元是弯曲的），即使[参考单元](@entry_id:168425)上的[基函数](@entry_id:170178)是多项式，经过 Piola 变换后在物理单元上的函数通常不再是多项式，而是有理函数。

#### 边和面的定向

在组装全局有限元矩阵时，自由度与网格的几何实体（如边和面）相关联。每个实体都需要一个全局一致的**定向（orientation）**，例如，为每条边指定一个从头到尾的切向，或为每个面指定一个法向。然而，在局部单元的计算中，边和面的[局部定向](@entry_id:264384)通常由其顶点的局部编号顺序导出。

这个[局部定向](@entry_id:264384)可能与预设的全局定向相反。为了保证在单元间共享的自由度值是唯一的，并且组装过程是正确的，必须在程序实现中处理这种定向不匹配的问题。标准做法是，在计算局部单元矩阵的贡献时，将[局部定向](@entry_id:264384)与全局定向进行比较。如果两者相反，则需要对相应的自由度或矩阵项乘以一个 $-1$ 的符号因子。这个看似微小的细节对于保证全局连续性和最终矩阵的正确性至关重要 [@problem_id:3438136]。

总之，Raviart-Thomas 和 Nédélec 元通过精巧地设计局部[函数空间](@entry_id:143478)和自由度，成功地构建了与 $H(\mathrm{div})$ 和 $H(\mathrm{curl})$ 空间协调的离散方法。它们不仅满足了[偏微分方程](@entry_id:141332)的内在结构要求，而且通过 de Rham 复形这一强大框架，为开发稳定、收敛且无[伪模式](@entry_id:163321)的高性能[数值算法](@entry_id:752770)铺平了道路。