## 引言
在[黎曼几何](@entry_id:160508)与几何分析的研究中，一个基本问题是如何在给定的[流形](@entry_id:153038)之间寻找“典范”或“最优美”的映照。[调和映照](@entry_id:187821) (Harmonic maps) 作为[狄利克雷能量](@entry_id:276589)泛函的[临界点](@entry_id:144653)，为此提供了一个完美的答案。它们不仅在几何上具有极佳的性质，还在拓扑学、[数学物理](@entry_id:265403)等领域扮演着关键角色。然而，一个基本的问题随之而来：对于任意两个[流形](@entry_id:153038)，这样的典范映照是否总能存在？

本文聚焦于解决这一存在性问题的里程碑式成果——[Eells-Sampson定理](@entry_id:204524)。该定理为一类重要的几何情境，即当目标[流形](@entry_id:153038)具有[非正截面曲率](@entry_id:275356)时，给出了肯定的回答。文章旨在为读者提供一个关于该定理的全面而深入的理解。

为实现这一目标，我们将分三个核心章节展开：
1.  **原理与机制**：我们将从[狄利克雷能量](@entry_id:276589)和[张力场](@entry_id:188540)等基本概念出发，精确陈述 Eells-Sampson 定理，并详细剖析其证明的核心工具——[调和映照热流](@entry_id:200511)。本章将揭示[非正曲率](@entry_id:203441)假设是如何成为保证热流方法成功的关键。
2.  **应用与跨学科联系**：我们将探讨 Eells-Sampson 定理的深刻推论，如唯一性、凸包性，并将其思想推广至等变映照和到奇异度量空间的[调和映照](@entry_id:187821)。本章还将展示该理论与[Ricci流](@entry_id:145202)、Teichmüller理论等领域的交叉联系。
3.  **动手实践**：通过一系列精心设计的计算练习，我们将帮助读者将理论知识转化为具体的分析能力，加深对[Bochner公式](@entry_id:187951)、热流收敛性等关键概念的理解。

通过这一结构化的学习路径，读者将不仅掌握 Eells-Sampson 定理本身，更能领会其背后深刻的[几何分析](@entry_id:157700)思想，并为探索更前沿的研究领域奠定坚实的基础。

## 原理与机制

在理解了调和映照的基本概念之后，本章将深入探讨将[紧流形](@entry_id:158804)映入[非正曲率](@entry_id:203441)空间时调和映照存在性的核心原理与机制。我们将首先精确定义所要最小化的泛函——[狄利克雷能量](@entry_id:276589)，及其一阶变分——[张力场](@entry_id:188540)。随后，我们将陈述 Eells-Sampson 定理，并详细阐述其证明的关键方法：[调和映照热流](@entry_id:200511)。我们将剖析[非正曲率](@entry_id:203441)假设在确保热流长时存在且收敛至一个[调和映照](@entry_id:187821)的过程中所扮演的决定性角色。

### 基本概念：能量与调和映照

[变分法](@entry_id:163656)是[几何分析](@entry_id:157700)中的一个核心工具，其思想是在给定的函数或几何对象空间中，通过最小化某个“能量”泛函来寻找“最佳”或“典范”的代表。对于[流形](@entry_id:153038)间的映照，这个[能量泛函](@entry_id:170311)就是[狄利克雷能量](@entry_id:276589)。

#### [狄利克雷能量](@entry_id:276589)泛函

给定一个紧的 $m$ 维黎曼流形 $(M, g)$ 和一个完备的[黎曼流形](@entry_id:261160) $(N, h)$，对于一个光滑映照 $u: (M, g) \to (N, h)$，其 **[狄利克雷能量](@entry_id:276589) (Dirichlet energy)** 定义为：
$$
E(u) = \frac{1}{2}\int_{M} |du|^2 d\operatorname{vol}_{g}
$$
其中 $d\operatorname{vol}_{g}$ 是由度量 $g$ 诱导的体积元。被积函数 $|du|^2$ 是映照 $u$ 的[微分](@entry_id:158718) $du: T_x M \to T_{u(x)} N$ 在每一点 $x \in M$ 的范数的平方，这个范数是由源空间度量 $g$ 和目标空间度量 $h$ 共同诱导的。

为了更清晰地理解这一点，我们可以在[局部坐标](@entry_id:181200)中展开这个表达式。设 $\{x^i\}$ 是 $M$ 上的[局部坐标](@entry_id:181200)，$\{y^\alpha\}$ 是 $N$ 上的[局部坐标](@entry_id:181200)。度量张量 $g$ 和 $h$ 的分量分别为 $g_{ij}$ 和 $h_{\alpha\beta}$。$g$ 的[逆矩阵](@entry_id:140380)分量为 $g^{ij}$。映照 $u$ 的[微分](@entry_id:158718)作用于[基向量](@entry_id:199546)为 $du(\frac{\partial}{\partial x^i}) = \frac{\partial u^\alpha}{\partial x^i} \frac{\partial}{\partial y^\alpha}$。能量密度 $|du|^2$ 是[微分](@entry_id:158718) $du$ 的[希尔伯特-施密特范数](@entry_id:265114) (Hilbert-Schmidt norm) 的平方，其定义为 $T_x M$ 的一个[标准正交基](@entry_id:147779) $\{e_i\}$ 在 $du$ 下的像的范数平方和，即 $|du|^2_x = \sum_{i=1}^m |du_x(e_i)|_h^2$。在[局部坐标](@entry_id:181200)中，这等价于：
$$
|du|^2 = g^{ij} h_{\alpha\beta} \frac{\partial u^\alpha}{\partial x^i} \frac{\partial u^\beta}{\partial x^j}
$$
这个表达式清楚地显示了能量密度是如何同时依赖于源度量 $g$ (通过 $g^{ij}$) 和目标度量 $h$ (通过 $h_{\alpha\beta}$) 的。另一种等价且非常重要的表述方式是利用[拉回](@entry_id:160816)张量 $u^*h$。$u^*h$ 是 $M$ 上的一个 $(0,2)$ 型张量，其分量为 $(u^*h)_{ij} = h_{\alpha\beta} \frac{\partial u^\alpha}{\partial x^i} \frac{\partial u^\beta}{\partial x^j}$。于是，能量密度可以简洁地写成 $u^*h$ 关于度量 $g$ 的迹：
$$
|du|^2 = g^{ij}(u^*h)_{ij} = \operatorname{tr}_{g}(u^*h)
$$
[@problem_id:2995288]

[能量泛函](@entry_id:170311)对度量的依赖性具有深刻的几何意义。例如，如果我们对度量进行常数缩放，设 $g' = \lambda g$ 且 $h' = \mu h$，其中 $\lambda, \mu$ 为正常数，$M$ 的维数为 $m$。那么逆度量变为 $(g')^{ij} = \lambda^{-1}g^{ij}$，[体积元](@entry_id:267802)变为 $d\operatorname{vol}_{g'} = \lambda^{m/2} d\operatorname{vol}_{g}$。新的[能量泛函](@entry_id:170311) $E_{g',h'}(u)$ 与原[能量泛函](@entry_id:170311) $E_{g,h}(u)$ 的关系为：
$$
E_{g',h'}(u) = \mu \lambda^{\frac{m}{2} - 1} E_{g,h}(u)
$$
特别地，如果只缩放目标度量 $h'=\mu h$ 而保持源度量不变（即 $\lambda=1$），能量将线性地缩放：$E_{h'}(u) = \mu E_h(u)$。

一个尤为重要的特殊情况发生在源[流形](@entry_id:153038) $M$ 的维数 $m=2$ 时。此时，能量泛函在源度量的 **[共形变换](@entry_id:159863) (conformal transformations)** 下保持不变。也就是说，如果我们将 $g$ 替换为 $g' = \Omega g$（其中 $\Omega$ 是 $M$ 上的任意正光滑函数），[能量泛函](@entry_id:170311)的值不会改变。这是因为当 $m=2$ 时，缩放因子 $\lambda^{\frac{m}{2} - 1} = \lambda^{1 - 1} = 1$。这个二维[共形不变性](@entry_id:191867)是调和映照理论与弦理论、复分析等领域产生深刻联系的基础。[@problem_id:2995288]

#### [张力场](@entry_id:188540)与调和映照

**调和映照 (Harmonic maps)** 被定义为[狄利克雷能量](@entry_id:276589)泛函 $E(u)$ 的[临界点](@entry_id:144653)。为了找到这些[临界点](@entry_id:144653)，我们需要计算能量的一阶变分。这个变分导数（在 $L^2$ 意义下）被称为 **[张力场](@entry_id:188540) (tension field)**，记作 $\tau(u)$。

从几何上看，[张力场](@entry_id:188540)衡量了映照 $u$ “偏离”调和状态的程度。它的内蕴定义是映照[微分](@entry_id:158718)的[协变导数](@entry_id:152476)（也称为映照的[第二基本形式](@entry_id:161454)）关于源度量 $g$ 的迹：
$$
\tau(u) = \operatorname{trace}_{g}(\nabla du)
$$
这里，$\nabla du$ 是一个取值于 $u^*TN$ 的 $M$ 上的 $(0,2)$ 型张量，其定义为 $(\nabla du)(X,Y) = \nabla^{u^*TN}_{X}(du(Y)) - du(\nabla^{M}_{X}Y)$，其中 $X, Y$ 是 $M$ 上的向量场，$\nabla^M$ 是 $M$ 上的列维-奇维塔联络，$\nabla^{u^*TN}$ 是从 $N$ 上的[列维-奇维塔联络](@entry_id:161107) $\nabla^N$ 诱导到[拉回丛](@entry_id:159346) $u^*TN$ 上的联络。

在[局部坐标](@entry_id:181200)中，[张力场](@entry_id:188540) $\tau(u)$ 的第 $\alpha$ 个分量可以计算得出：
$$
\tau(u)^\alpha = g^{ij} \left( \frac{\partial^2 u^\alpha}{\partial x^i \partial x^j} - \Gamma^{k}_{ij} \frac{\partial u^\alpha}{\partial x^k} + \Gamma^{\alpha}_{\beta\gamma}(u) \frac{\partial u^\beta}{\partial x^i} \frac{\partial u^\gamma}{\partial x^j} \right)
$$
其中 $\Gamma^{k}_{ij}$ 是 $(M,g)$ 的克里斯托费尔符号，$\Gamma^{\alpha}_{\beta\gamma}$ 是 $(N,h)$ 的[克里斯托费尔符号](@entry_id:159831)。[@problem_id:2995337]

因此，一个映照 $u$ 是调和映照的充要条件是它的[张力场](@entry_id:188540)恒为零，即 $\tau(u) = 0$。

我们必须仔细区分内蕴的[张力场](@entry_id:188540) $\tau(u)$ 和坐标依赖的拉普拉斯算子 $\Delta u$。后者通常被定义为将源[流形](@entry_id:153038)上的[拉普拉斯-贝尔特拉米算子](@entry_id:267002) $\Delta_M$ 作用于映照的每个坐标分量 $u^\alpha$ 上，即 $(\Delta u)^\alpha = \Delta_M u^\alpha = g^{ij}(\frac{\partial^2 u^\alpha}{\partial x^i \partial x^j} - \Gamma^{k}_{ij} \frac{\partial u^\alpha}{\partial x^k})$。对比[张力场](@entry_id:188540)的表达式，我们发现：
$$
\tau(u)^\alpha = (\Delta u)^\alpha + g^{ij} \Gamma^{\alpha}_{\beta\gamma}(u) \frac{\partial u^\beta}{\partial x^i} \frac{\partial u^\gamma}{\partial x^j}
$$
显然，$\tau(u)$ 与 $\Delta u$ 仅在目标[流形](@entry_id:153038)是平坦的（即 $\Gamma^{\alpha}_{\beta\gamma} = 0$，例如欧氏空间 $\mathbb{R}^n$ 使用标准[坐标系](@entry_id:156346)）时才相等。对于一般的弯曲目标[流形](@entry_id:153038)，$\tau(u) = 0$ 是一个[非线性](@entry_id:637147)的[偏微分方程组](@entry_id:172573)，其[非线性](@entry_id:637147)项 $g^{ij} \Gamma^{\alpha}_{\beta\gamma} \dots$ 精确地捕捉了目标[流形](@entry_id:153038)的几何（曲率）。将 $\tau(u)$ 误认为 $\Delta u$ 会忽略掉目标[流形](@entry_id:153038)几何的关键影响。[@problem_id:2995337]

### Eells-Sampson 定理：存在性与正则性

有了能量和调和性的概念，我们现在可以陈述本章的核心定理。Eells 和 Sampson 在 1964 年的开创性工作中证明了一个深刻的结果，保证了在特定几何条件下，每个[同伦类](@entry_id:149365)中都存在一个典范的[调和映照](@entry_id:187821)。

#### 定理陈述

**Eells-Sampson 定理**：设 $(M,g)$ 是一个紧的、无边的黎曼流形，$(N,h)$ 是一个完备的、截面曲率非正（即对任意点 $x \in N$ 和任意二维切[子空间](@entry_id:150286) $\sigma \subset T_xN$，其截面曲率 $K_N(\sigma) \le 0$）的[黎曼流形](@entry_id:261160)。那么，对于从 $M$ 到 $N$ 的任意连续映照 $f_0: M \to N$，存在一个光滑的调和映照 $u: M \to N$，它与 $f_0$ 同伦。

此外，这个通过 Eells-Sampson 方法构造的[调和映照](@entry_id:187821) $u$ 在其[同伦类](@entry_id:149365)中最小化[狄利克雷能量](@entry_id:276589)。如果目标[流形](@entry_id:153038)的[截面曲率](@entry_id:159738)处处为负（$K_N  0$），那么在每个[同伦类](@entry_id:149365)中的这个调和代表是唯一的。[@problem_id:2995309]

#### 能量景观：两种曲率的故事

Eells-Sampson 定理的意义在于，它在每个拓扑类（[同伦类](@entry_id:149365)）中都找到了一个几何上最优美的代表——能量[最小元](@entry_id:265018)。[非正曲率](@entry_id:203441)的假设至关重要，它极大地简化了能量泛函的“景观”。

为了理解这一点，我们可以对比目标[流形曲率](@entry_id:187680)为正的情况。一个经典的例子是映照 $f: \mathbb{S}^2 \to \mathbb{S}^2$。在这种情况下，$K_N  0$。对于任意非零的度数 $d \in \mathbb{Z}$，存在无穷多个不同的[调和映照](@entry_id:187821)，它们都是[能量泛函](@entry_id:170311)的（全局）极小值。例如，所有度数为 $d$ 的全纯映照（有理函数）和反全纯映照都是能量[极小元](@entry_id:266349)，并且通过与目标球面 $\mathbb{S}^2$ 的[等距变换](@entry_id:150881)（旋转）复合，可以生成无穷多个不同的[极小元](@entry_id:266349)。[@problem_id:2995351] 这表明，当目标[流形](@entry_id:153038)具有正曲率时，能量景观可能非常复杂，充满了大量的局部极小值。

相比之下，[非正曲率](@entry_id:203441)假设排除了这种复杂性。正如我们将在后面看到的，当 $K_N \le 0$ 时，能量泛函沿着“[测地线](@entry_id:269969)路径”是凸的。这意味着一个[同伦类](@entry_id:149365)中的任何局部极小值自动成为该类中的[全局极小值](@entry_id:165977)，并且在严格负曲率的情况下，这个极小值是唯一的。[@problem_id:2995351] 这种简化的能量景观是 Eells-Sampson 证明方法能够成功的根本原因。

### 证明机制：[调和映照热流](@entry_id:200511)

Eells 和 Sampson 的证明是构造性的，他们引入了一种[几何流](@entry_id:195216)动——**[调和映照热流](@entry_id:200511) (harmonic map heat flow)**，通过模拟热量[扩散](@entry_id:141445)的过程，将任意初始映照“演化”成一个[调和映照](@entry_id:187821)。

#### 梯度流方法

寻找能量泛函 $E(u)$ 的极小值的一个自然方法是[梯度下降法](@entry_id:637322)。在无限维的映照空间中，这对应于一个梯度流。[调和映照热流](@entry_id:200511)正是[狄利克雷能量](@entry_id:276589)关于 $L^2$ 度量的负[梯度流](@entry_id:635964)。

流动的演化方程定义为：
$$
\frac{\partial u}{\partial t} = \tau(u)
$$
其中 $u(t) = u(\cdot, t)$ 是一个依赖于时间 $t$ 的映照族，其初值为给定的映照 $u(\cdot, 0) = u_0$。

要证明这确实是一个梯度流，我们需要计算能量的一阶变分。对于任意变分向量场 $V \in \Gamma(u^*TN)$（它是映照空间在 $u$ 点的一个切向量），能量的一阶变分为：
$$
dE_u(V) = \left.\frac{d}{ds}\right|_{s=0} E(u_s) = -\int_M \langle \tau(u), V \rangle_h d\operatorname{vol}_g
$$
这里的 $\langle \cdot, \cdot \rangle_h$ 是 $N$ 上由度量 $h$ 诱导的[内积](@entry_id:158127)。另一方面，变分向量场空间上的 $L^2$ [内积](@entry_id:158127)定义为 $\langle\langle V, W \rangle\rangle_{L^2} = \int_M \langle V, W \rangle_h d\operatorname{vol}_g$。根据梯度 $\operatorname{grad}_{L^2}E(u)$ 的定义，它必须满足 $dE_u(V) = \langle\langle \operatorname{grad}_{L^2}E(u), V \rangle\rangle_{L^2}$。比较两个表达式，我们立即得到：
$$
\operatorname{grad}_{L^2}E(u) = -\tau(u)
$$
因此，负梯度流方程 $\frac{\partial u}{\partial t} = -\operatorname{grad}_{L^2}E(u)$ 恰好就是[调和映照热流](@entry_id:200511)方程 $\frac{\partial u}{\partial t} = \tau(u)$。[@problem_id:2995346]

沿着这个流动，能量随时间的变化率为：
$$
\frac{d}{dt}E(u(t)) = dE_{u(t)}\left(\frac{\partial u}{\partial t}\right) = -\int_M \left\langle \tau(u(t)), \frac{\partial u}{\partial t} \right\rangle_h d\operatorname{vol}_g = -\int_M |\tau(u(t))|^2_h d\operatorname{vol}_g \le 0
$$
这个 **[能量耗散](@entry_id:147406)恒等式** 表明，只要映照不是调和的（即 $\tau(u) \neq 0$），能量就会严格下降。这为流动最终会收敛到一个能量的[临界点](@entry_id:144653)——即[调和映照](@entry_id:187821)——提供了希望。[@problem_id:2995346]

#### 全局存在性与收敛：曲率的角色

证明热流方法成功的关键在于证明这个流动会长时存在（即不会在有限时间内“爆炸”或形成[奇点](@entry_id:137764)），并且当 $t \to \infty$ 时会收敛到一个光滑的调和映照。这正是[非正曲率](@entry_id:203441)假设发挥魔力的地方。证明过程可分为四个步骤。[@problem_id:2995265]

1.  **[短时存在性](@entry_id:193885)**：[调和映照热流](@entry_id:200511)方程是一个[拟线性](@entry_id:637689)的[抛物型偏微分方程](@entry_id:168935)组。对于光滑的初值，根据标准的[抛物型方程](@entry_id:144670)理论，在紧流形上总能保证解在某个短时间区间 $[0, \varepsilon)$ 内唯一存在且光滑。[@problem_id:2995265]

2.  **[先验估计](@entry_id:186098)**：这是整个证明的核心。为了将解从短时延拓到长时，我们必须证明解及其各阶导数在任何有限时间区间内都是一致有界的。
    
    *   **[梯度估计](@entry_id:164549)**：关键的估计是对能量密度 $e(u) = \frac{1}{2}|du|^2$ 的逐点[上界](@entry_id:274738)估计。这通过一个精巧的 **Bochner 技巧** 实现。我们计算 $e(u)$ 沿着热流的演化方程，得到一个形式为 $(\partial_t - \Delta_M)e(u)$ 的表达式。这个表达式包含三部分：一个耗散项 $-|\nabla du|^2$，一个与源[流形](@entry_id:153038) $M$ 的里奇曲率相关的项，以及一个与目标[流形](@entry_id:153038) $N$ 的[黎曼曲率张量](@entry_id:160189) $R^N$ 相关的项。
    
    至关重要的观察是，当目标[流形](@entry_id:153038)的截面曲率 $K_N \le 0$ 时，与 $R^N$ 相关的项总是具有“好的”符号（它对 $(\partial_t - \Delta_M)e(u)$ 的贡献是非正的）。[@problem_id:2995274] 这使得我们可以得到一个形如 $(\partial_t - \Delta_M)e(u) \le C e(u)$ 的[微分不等式](@entry_id:137452)（在更仔细的处理下，甚至可以得到一个更好的不等式）。
    
    然后，应用 **抛物极大值原理**，我们可以得到对能量密度最大值 $\sup_M e(\cdot, t)$ 的控制。这个控制保证了 $|du|$ 不会在有限时间内发生爆破。[@problem_id:2995255] 值得注意的是，仅仅知道总能量 $\int_M e(u) d\text{vol}_g$ 有界是不足以排除逐点爆破的，必须要有逐点的 $L^\infty$ 估计。[@problem_id:2995255]

    *   **像域估计**：我们还需要确保映照的像 $u(M,t)$ 不会“逃逸”到 $N$ 的无穷远处。这再次利用了 $K_N \le 0$ 的一个深刻几何性质。在[非正曲率](@entry_id:203441)空间中，任意点 $p \in N$ 的平方距离函数 $f(x) = d_N(x,p)^2$ 是[凸函数](@entry_id:143075)。更精确地说，它的黑塞矩阵满足 $\operatorname{Hess}(f)(v,v) \ge 2|v|^2$。[@problem_id:2995290] 将此性质应用于函数 $d_N(u(x,t),p)^2$ 并结合极大值原理，可以证明 $u(M \times [0,T))$ 的像始终包含在一个固定的紧[子集](@entry_id:261956)内。[@problem_id:2995265]

3.  **长时存在性**：一旦获得了对映照 $u$ 及其梯度 $|du|$ 的一致[先验界](@entry_id:636648)，标准的抛物型[正则性理论](@entry_id:194071)（例如，Schauder 估计）就会自动给出对所有高阶导数的一致界。这排除了任何形式的爆破，从而可以将解从任意时间 $T$ 延拓到 $T+\varepsilon$，最终证明解在整个时间轴 $[0, \infty)$ 上都存在。[@problem_id:2995265]

4.  **收敛性**：[能量耗散](@entry_id:147406)恒等式告诉我们 $\int_0^\infty \int_M |\tau(u)|^2 d\text{vol}_g dt  \infty$。这意味着存在一个时间序列 $t_j \to \infty$，使得 $\tau(u(\cdot, t_j))$ 的 $L^2$ 范数趋于 $0$。由于我们有所有阶导数的一致界，根据 Arzelà-Ascoli 定理，我们可以从 $\{u(\cdot, t_j)\}$ 中提取一个在 $C^\infty$ 拓扑下收敛的子列，其极限为一个光滑映照 $u_\infty$。由连续性可知，$\tau(u_\infty) = \lim_{j\to\infty} \tau(u(t_j)) = 0$，因此 $u_\infty$ 是一个[调和映照](@entry_id:187821)。由于整个热流过程是一个连续形变，极限映照 $u_\infty$ 与初始映照 $u_0$ 必然[同伦](@entry_id:139266)。[@problem_id:2995265]

### 稳定性与凸性：[极小元](@entry_id:266349)的几何

Eells-Sampson 构造出的调和映照不仅是能量的[临界点](@entry_id:144653)，而且是稳定的极小值点。这同样根植于目标[流形](@entry_id:153038)的[非正曲率](@entry_id:203441)性质。

#### 调和映照的稳定性

一个[临界点](@entry_id:144653)的稳定性由[能量泛函](@entry_id:170311)的二阶变分符号决定。对于一个调和映照 $u$ 和任意变分向量场 $V$，二阶变分的公式为：
$$
\left.\frac{d^2}{dt^2}\right|_{t=0} E(u_t) = \int_M \left( |\nabla V|^2 - \sum_{i=1}^m \langle R^N(du(e_i), V)V, du(e_i) \rangle_h \right) d\operatorname{vol}_g
$$
其中 $\{e_i\}$ 是 $T_xM$ 的一个标准正交基。曲率项 $\langle R^N(A,B)B,A \rangle$ 正是截面曲率 $K_N(A \wedge B)$ 乘以一个非负的 Gram [行列式](@entry_id:142978)。当 $K_N \le 0$ 时，这个曲率项 $\langle R^N(\dots) \rangle$ 总是非正的。因此，在积分号下的被积函数是 $|\nabla V|^2$（非负）减去一个非正项，结果必然是非负的。
$$
|\nabla V|^2 - \sum_{i=1}^m \underbrace{\langle R^N(du(e_i), V)V, du(e_i) \rangle_h}_{\le 0} \ge 0
$$
一个非负函数的积分必然是非负的，所以二阶变分 $\ge 0$。这表明，在[非正曲率](@entry_id:203441)目标[流形](@entry_id:153038)中，任何调和映照都是[能量泛函](@entry_id:170311)的稳定[临界点](@entry_id:144653)，即[局部极小值](@entry_id:143537)。[@problem_id:2995347]

#### 能量景观的凸性

我们可以对[能量景观](@entry_id:147726)的几何有更深刻的理解。考虑一个特殊的同伦路径，称为 **逐点测地同伦 (pointwise-geodesic homotopy)**，即对每个 $x \in M$，曲线 $t \mapsto f_t(x)$ 都是 $N$ 中的一条[测地线](@entry_id:269969)。Eells 和 Sampson 证明了，当 $K_N \le 0$ 时，能量泛函 $E(f_t)$ 作为 $t$ 的函数是[凸函数](@entry_id:143075)，即 $\frac{d^2}{dt^2}E(f_t) \ge 0$。[@problem_id:2995351]

这个凸性具有强大的推论。特别地，如果 $N$ 是一个哈达玛[流形](@entry_id:153038)（Hadamard manifold），即完备、单连通且 $K_N \le 0$，那么任意两点由唯一的[测地线](@entry_id:269969)连接。这意味着任意两个映照 $f_0, f_1: M \to N$ 也由一个唯一的逐点测地同伦连接。

现在，假设 $f_{loc}$ 是能量在一个[同伦类](@entry_id:149365)中的一个局部极小值。它必然是一个[调和映照](@entry_id:187821)，因此 $\tau(f_{loc})=0$。对于[同伦类](@entry_id:149365)中任意其他映照 $f_{any}$，我们构造连接它们的唯一逐点测地[同伦](@entry_id:139266) $f_t$（其中 $f_0=f_{loc}, f_1=f_{any}$）。令 $\phi(t) = E(f_t)$。由于 $\phi(t)$ 是[凸函数](@entry_id:143075)，且其在 $t=0$ 处的导数 $\phi'(0) = - \int \langle \tau(f_0), V_0 \rangle = 0$，这必然意味着 $\phi(t)$ 在 $[0,1]$ 上是单调不减的。因此 $\phi(1) \ge \phi(0)$，即 $E(f_{any}) \ge E(f_{loc})$。这表明，任何[局部极小值](@entry_id:143537)实际上是该[同伦类](@entry_id:149365)中的全局极小值。[@problem_id:2995351]

这一结论完美地描绘了[非正曲率](@entry_id:203441)目标[流形](@entry_id:153038)下[能量景观](@entry_id:147726)的优美几何：它没有“陷阱”般的虚假局部极小值，使得梯度流方法能够可靠地找到真正的全局最小值。这与正曲率情况下能量景观的复杂性形成了鲜明的对比，也从根本上解释了 Eells-Sampson 定理为何成立。