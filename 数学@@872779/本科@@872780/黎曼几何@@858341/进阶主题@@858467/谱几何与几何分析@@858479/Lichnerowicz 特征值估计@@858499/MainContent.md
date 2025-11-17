## 引言
在[黎曼几何](@entry_id:160508)的宏伟蓝图中，一个永恒且核心的问题是：[流形](@entry_id:153038)的几何形状，尤其是其曲率，如何支配其上定义的函数和算子的行为？[Lichnerowicz特征值估计](@entry_id:192504)为这一深刻问题提供了一个精妙绝伦的解答。它通过一个简洁而有力的不等式，直接将[流形](@entry_id:153038)的局部几何信息（里奇曲率）与[全局分析](@entry_id:188294)属性（拉普拉斯算子的基本[振动频率](@entry_id:199185)）联系起来，成为连接几何与分析的基石之一。本文旨在系统性地揭示这一著名定理的内在逻辑、广泛应用及其深远影响。

本文将引导读者穿越三个层次的探索。在第一章“原理与机制”中，我们将深入其数学核心，从[拉普拉斯算子](@entry_id:146319)和里奇曲率等基本构件出发，逐步推导出关键的Bochner-Weitzenböck公式，并最终完成[Lichnerowicz估计](@entry_id:187368)的完整证明，同时探讨其刚性结论。随后，在第二章“应用与跨学科联系”中，我们将视野拓宽，展示该估计如何在几何学中推导出关于[流形](@entry_id:153038)拓扑和直径的深刻结论，并探讨其如何与概率论中的[随机过程](@entry_id:159502)收敛性、信息论中的[测度集中](@entry_id:265372)现象等领域产生惊人的共鸣。最后，通过第三章“动手实践”中的精选问题，读者将有机会亲手演算关键步骤，将理论知识内化为解决问题的实践能力。通过这段旅程，您将深刻理解[Lichnerowicz估计](@entry_id:187368)不仅是一个优美的数学公式，更是一个理解几何世界内在和谐的强大思想工具。

## 原理与机制

在深入探讨黎曼几何中曲率与分析之间的深刻联系时，一个核心的问题是：一个[流形](@entry_id:153038)的几何形状，特别是其曲率，如何控制其上定义的函数的行为？[Lichnerowicz特征值估计](@entry_id:192504)为这个问题提供了一个精妙而有力的解答。它通过一个优雅的公式，将[里奇曲率](@entry_id:162038)（Ricci curvature）的下界与[拉普拉斯-贝尔特拉米算子](@entry_id:267002)（Laplace-Beltrami operator）的第一个非零[特征值](@entry_id:154894)直接联系起来。本章旨在系统地阐述这一著名估计的原理和推导机制。

### 基础的几何构件

在我们构建[Lichnerowicz估计](@entry_id:187368)的证明之前，必须首先明确我们将要使用的几个关键几何概念。

**[拉普拉斯-贝尔特拉米算子](@entry_id:267002)及其[特征值](@entry_id:154894)**

在一个[黎曼流形](@entry_id:261160) $(M, g)$ 上，对于一个[光滑函数](@entry_id:267124) $f$，其**梯度** $\nabla f$ 是一个向量场，由度量 $g$ 通过关系 $g(\nabla f, X) = df(X)$ 对任意向量场 $X$ 唯一确定。一个向量场 $X$ 的**散度** $\operatorname{div}(X)$ 是其[协变导数](@entry_id:152476) $\nabla X$ 的迹。综合这两者，我们定义**[拉普拉斯-贝尔特拉米算子](@entry_id:267002)** $\Delta$ 作用在函数 $f$ 上为：
$$
\Delta f = \operatorname{div}(\nabla f)
$$
在本书中，我们遵循几何学中的符号约定，该[算子的谱](@entry_id:272027)为非正。因此，我们主要关注算子 $-\Delta$ 的特征值问题。在一个紧致、无边的连通[黎曼流形](@entry_id:261160)上，算子 $-\Delta$ 的谱是一列离散的、非负的[特征值](@entry_id:154894)：
$$
0 = \lambda_0  \lambda_1 \le \lambda_2 \le \dots \to \infty
$$
其中每个[特征值](@entry_id:154894) $\lambda_k$ 都对应一个有限维的特征空间。第一个[特征值](@entry_id:154894) $\lambda_0 = 0$ 总是存在的，其对应的特征函数恰好是[流形](@entry_id:153038)上的常数函数 [@problem_id:3055932]。我们最感兴趣的是**第一个非零[特征值](@entry_id:154894)** $\lambda_1$，它描述了[流形](@entry_id:153038)上“最不平坦”的非平凡[振动](@entry_id:267781)模式。这个[特征值](@entry_id:154894)可以通过**[瑞利商](@entry_id:137794)（Rayleigh quotient）** 进行变分刻画：
$$
\lambda_1 = \inf_{f \in C^\infty(M), f \not\equiv \text{const}, \int_M f \, d\mu = 0} \frac{\int_M |\nabla f|^2 \, d\mu}{\int_M f^2 \, d\mu}
$$
其中 $d\mu$ 是由度量 $g$ 诱导的[体积元](@entry_id:267802)。对于满足 $\Delta f = -\lambda_1 f$ 的特征函数 $f$，通过分部积分（[格林第一恒等式](@entry_id:170345)），我们直接得到一个重要的关系式 [@problem_id:3071814]：
$$
\int_M |\nabla f|^2 \, d\mu = -\int_M f (\Delta f) \, d\mu = \lambda_1 \int_M f^2 \, d\mu
$$

**[里奇曲率](@entry_id:162038)及其下界**

几何信息的核心载体是曲率。[Lichnerowicz估计](@entry_id:187368)所依赖的不是最完整的[黎曼曲率张量](@entry_id:160189)，而是其一个重要的迹——**[里奇曲率张量](@entry_id:271424)** $\operatorname{Ric}$。在一个 $n$ 维[流形](@entry_id:153038)上，$\operatorname{Ric}$ 是一个对称的 $(0,2)$-张量，它在一点 $p$ 对切向量 $X, Y \in T_pM$ 的取值，是通过对[黎曼曲率张量](@entry_id:160189) $R$ 进行迹运算得到的 [@problem_id:3055881]：
$$
\operatorname{Ric}(X,Y) = \operatorname{tr}(Z \mapsto R(Z,X)Y) = \sum_{i=1}^n g(R(e_i,X)Y, e_i)
$$
这里 $\{e_i\}_{i=1}^n$ 是切空间 $T_pM$ 的任意一个[标准正交基](@entry_id:147779)。从物理上看，$\operatorname{Ric}(X,X)$ 描述了沿 $X$ 方向的[测地线](@entry_id:269969)体积元的二阶变化率。

[Lichnerowicz估计](@entry_id:187368)的出发点是一个关于[流形](@entry_id:153038)几何的假设，即[里奇曲率](@entry_id:162038)有一个**逐点下界**。我们假设存在一个常数 $K$，使得不等式
$$
\operatorname{Ric} \ge (n-1)K g
$$
在[流形](@entry_id:153038) $M$ 上处处成立。这个不等式是张量之间的不等式，其精确含义是，对于每一点 $p \in M$ 的任意切向量 $X \in T_pM$，以下关于二次型的实数不等式成立 [@problem_id:3055881]：
$$
\operatorname{Ric}(X,X) \ge (n-1)K g(X,X) = (n-1)K |X|^2
$$
换言之，张量 $\operatorname{Ric} - (n-1)K g$ 在每个[切空间](@entry_id:199137)上都是一个半正定[双线性形式](@entry_id:746794)。当 $K0$ 时，这个条件直观地意味着[流形](@entry_id:153038)在所有方向上都具有正的“平均曲率”。

### 核心机制：Bochner-Weitzenböck 公式

连接分析（拉普拉斯算子）与几何（里奇曲率）的桥梁，是一个被称为**Bochner-Weitzenböck公式**（或简称**[Bochner公式](@entry_id:187951)**）的恒等式。这个公式是[黎曼几何](@entry_id:160508)中一个极其强大的计算工具，它本身是通过交换[协变导数](@entry_id:152476)的顺序并利用曲率张量的定义推导出来的。

对于任意[光滑函数](@entry_id:267124) $f$，其**黑塞张量（Hessian tensor）** $\nabla^2 f$ 是一个对称的 $(0,2)$-张量，定义为 $\nabla^2 f(X,Y) = g(\nabla_X (\nabla f), Y)$。值得注意的是，黑塞[张量的迹](@entry_id:190669)就是[拉普拉斯算子](@entry_id:146319)：$\operatorname{tr}_g(\nabla^2 f) = \Delta f$ [@problem_id:3055903]。

Bochner-Weitzenböck公式描述了梯度范数的平方 $|\nabla f|^2$ 的拉普拉斯，它联系了 $|\nabla f|^2$、函数的黑塞张量 $|\nabla^2 f|^2$、函数拉普拉斯的梯度 $\nabla(\Delta f)$ 以及里奇曲率 [@problem_id:3055923]：
$$
\frac{1}{2} \Delta (|\nabla f|^2) = |\nabla^2 f|^2 + g(\nabla (\Delta f), \nabla f) + \operatorname{Ric}(\nabla f, \nabla f)
$$
这个公式是一个逐点成立的恒等式，对任何[黎曼流形](@entry_id:261160)上的任何[光滑函数](@entry_id:267124)都成立。它的精妙之处在于将[二阶导数](@entry_id:144508)的信息（通过 $|\nabla^2 f|^2$ 和 $\Delta f$）与[流形](@entry_id:153038)的[内蕴几何](@entry_id:158788)（通过 $\operatorname{Ric}$）联系在了一起。

### 从逐点到全局：积分与不等式

为了得到关于全局量（[特征值](@entry_id:154894) $\lambda_1$）的信息，我们需要将逐点成立的[Bochner公式](@entry_id:187951)转化为一个全局的积分关系。

**积分步骤**

假设 $f$ 是对应于第一个非零[特征值](@entry_id:154894) $\lambda_1$ 的[特征函数](@entry_id:186820)，即 $\Delta f = -\lambda_1 f$。将此代入[Bochner公式](@entry_id:187951)，我们得到：
$$
\frac{1}{2} \Delta (|\nabla f|^2) = |\nabla^2 f|^2 + g(\nabla (-\lambda_1 f), \nabla f) + \operatorname{Ric}(\nabla f, \nabla f) = |\nabla^2 f|^2 - \lambda_1 |\nabla f|^2 + \operatorname{Ric}(\nabla f, \nabla f)
$$
现在，我们在整个[流形](@entry_id:153038) $M$ 上对这个等式进行积分。这里，[流形](@entry_id:153038) $M$ **紧致无边**的假设变得至关重要。根据**散度定理**（或斯托克斯定理的特例），任何光滑函数（这里是 $|\nabla f|^2$）的拉普拉斯在紧致无边[流形上的积分](@entry_id:156150)恒为零 [@problem_id:3055914]：
$$
\int_M \Delta (|\nabla f|^2) \, d\mu = \int_M \operatorname{div}(\nabla(|\nabla f|^2)) \, d\mu = 0
$$
因此，我们得到了一个关键的积分恒等式：
$$
0 = \int_M \left( |\nabla^2 f|^2 - \lambda_1 |\nabla f|^2 + \operatorname{Ric}(\nabla f, \nabla f) \right) d\mu
$$
这个等式优雅地平衡了函数的二阶变化、[特征值](@entry_id:154894)以及[流形](@entry_id:153038)的曲率。

**应用不等式**

下一步是将上述积分等式转化为一个不等式，这需要引入两个关键的逐点不等式。

1.  **里奇曲率下界不等式**：我们利用假设 $\operatorname{Ric} \ge (n-1)K g$ 来处理积分中的曲率项。将向量场 $X$ 替换为梯度向量场 $\nabla f$，我们得到逐点不等式：
    $$
    \operatorname{Ric}(\nabla f, \nabla f) \ge (n-1)K |\nabla f|^2
    $$

2.  **黑塞-拉普拉斯不等式**：这是一个纯代数的不等式，它关系到一个对称张量的[弗罗贝尼乌斯范数](@entry_id:143384)（Frobenius norm）的平方与其迹的平方。对于黑塞张量 $\nabla^2 f$，这个不等式表现为：
    $$
    |\nabla^2 f|^2 \ge \frac{1}{n} (\operatorname{tr}(\nabla^2 f))^2 = \frac{1}{n} (\Delta f)^2
    $$
    这个不等式的根源是**柯西-施瓦茨不等式**。考虑在某一点，$n$ 个黑塞张量的[特征值](@entry_id:154894)为 $\mu_1, \dots, \mu_n$。那么 $|\nabla^2 f|^2 = \sum \mu_i^2$ 且 $\Delta f = \sum \mu_i$。在 $\mathbb{R}^n$ 中对向量 $(1, \dots, 1)$ 和 $(\mu_1, \dots, \mu_n)$ 应用柯西-施瓦茨不等式 $(\sum a_ib_i)^2 \le (\sum a_i^2)(\sum b_i^2)$，我们得到 $(\sum \mu_i)^2 \le n (\sum \mu_i^2)$，这正是上述不等式。
    
    这个不等式中的常数 $n$ 是最优的，无法被任何更小的数替代。当且仅当所有[特征值](@entry_id:154894)都相等时，等号成立，即 $\nabla^2 f$ 是度量张量 $g$ 的一个倍数。一个简单的例子可以说明这一点：在[欧氏空间](@entry_id:138052) $\mathbb{R}^n$ 中考虑函数 $f(x) = \frac{a}{2}|x|^2$。它的黑塞张量在每一点都是 $a \cdot \text{Id}$，所有[特征值](@entry_id:154894)都等于 $a$。此时，我们有 $|\nabla^2 f|^2 = na^2$ 和 $(\Delta f)^2 = (na)^2$，不等式 $|\nabla^2 f|^2 \ge \frac{1}{n}(\Delta f)^2$ 变为 $na^2 \ge \frac{1}{n}(na)^2 = na^2$，等号精确成立。这表明任何小于 $n$ 的常数都无法满足这个例子 [@problem_id:3055882]。

**完成推导**

将这两个不等式代入我们的积分恒等式，并利用 $\Delta f = -\lambda_1 f$：
$$
0 \ge \int_M \left( \frac{1}{n}(-\lambda_1 f)^2 - \lambda_1 |\nabla f|^2 + (n-1)K |\nabla f|^2 \right) d\mu
$$
$$
\lambda_1 \int_M |\nabla f|^2 \, d\mu \ge \frac{\lambda_1^2}{n} \int_M f^2 \, d\mu + (n-1)K \int_M |\nabla f|^2 \, d\mu
$$
现在，我们使用之前由分部积分得到的恒等式 $\int_M |\nabla f|^2 d\mu = \lambda_1 \int_M f^2 d\mu$ 来统一积分项：
$$
\lambda_1 (\lambda_1 \int_M f^2 \, d\mu) \ge \frac{\lambda_1^2}{n} \int_M f^2 \, d\mu + (n-1)K (\lambda_1 \int_M f^2 \, d\mu)
$$
由于 $f$ 是非平凡特征函数，$\lambda_1  0$ 且 $\int_M f^2 d\mu  0$。因此，我们可以放心地将不等式两边同除以正数 $\lambda_1 \int_M f^2 d\mu$，得到：
$$
\lambda_1 \ge \frac{\lambda_1}{n} + (n-1)K
$$
整理此式，我们便得到了最终的**[Lichnerowicz特征值估计](@entry_id:192504)**：
$$
\lambda_1 \left(1 - \frac{1}{n}\right) \ge (n-1)K \quad \implies \quad \lambda_1 \ge nK
$$
这个简洁而深刻的结果表明，如果一个[紧致流形](@entry_id:158804)的里奇曲率被一个正常数 $K$ 从下方控制，那么它的基本[振动频率](@entry_id:199185) $\lambda_1$ 也不能任意小，它同样被一个与 $K$ 和维数 $n$ 相关的正常数 $nK$ 从下方控制。这为“正曲率蕴含着几何上的‘刚性’”这一直观感受提供了一个坚实的分析证据。整个推导逻辑链条清晰而严谨，从[Bochner公式](@entry_id:187951)出发，通[过积分](@entry_id:753033)和一系列经典不等式的应用，最终揭示了曲率与谱之间的基本关系 [@problem_id:3055927]。

### 刚性分析：当估计达到最优时

[Lichnerowicz估计](@entry_id:187368) $\lambda_1 \ge nK$ 提出了一个自然的问题：等号何时成立？对这个“等号情形”的分析，将揭示出更加深刻的[几何刚性](@entry_id:189736)，这便是著名的**Lichnerowicz-[Obata定理](@entry_id:185498)**。

如果 $\lambda_1 = nK$，那么在推导过程中的每一个不等式都必须变为等式。这意味着对于任意一个第一[特征函数](@entry_id:186820) $f$，以下两个条件必须逐点成立 [@problem_id:3071874]：

1.  $|\nabla^2 f|^2 = \frac{1}{n}(\Delta f)^2$
2.  $\operatorname{Ric}(\nabla f, \nabla f) = (n-1)K |\nabla f|^2$

第一个条件是黑塞-拉普拉斯不等式的等号情形，它强制要求黑塞张量 $\nabla^2 f$ 必须是度量张量 $g$ 的倍数。结合 $\operatorname{tr}(\nabla^2 f) = \Delta f = -\lambda_1 f$，我们得到一个关键的[偏微分方程](@entry_id:141332)：
$$
\nabla^2 f = \frac{\Delta f}{n} g = -\frac{\lambda_1}{n} f g
$$
将等号条件 $\lambda_1 = nK$ 代入，方程变为：
$$
\nabla^2 f = -K f g
$$
第二个条件则意味着[流形](@entry_id:153038)本身必须是**爱因斯坦[流形](@entry_id:153038)**，其[里奇曲率](@entry_id:162038)处处等于 $(n-1)Kg$。

Obata的[刚性定理](@entry_id:198222)指出，任何一个完备的 $n$ 维[黎曼流形](@entry_id:261160)若存在一个满足方程 $\nabla^2 f = -K f g$（其中 $K0$ 为常数）的非平凡函数 $f$，则该[流形](@entry_id:153038)必定等距于一个半径为 $1/\sqrt{K}$ 的标准 $n$ 维球面 $\mathbb{S}^n$。

这个定理的直观想法是分析函数 $f$ 沿着[测地线](@entry_id:269969)的行为。如果 $\gamma(t)$ 是一条单位速度[测地线](@entry_id:269969)，令 $u(t) = f(\gamma(t))$，那么 $u''(t) = \nabla^2 f(\dot{\gamma}(t), \dot{\gamma}(t)) = -K f(\gamma(t)) g(\dot{\gamma}(t), \dot{\gamma}(t)) = -K u(t)$。因此，$u(t)$ 必须是形如 $A\cos(\sqrt{K}t + \phi)$ 的余弦函数。一个非平凡函数 $f$ 在紧流形上必有[最大值点](@entry_id:634610)和最小值点。从[最大值点](@entry_id:634610)出发的所有[测地线](@entry_id:269969)，其上的函数值 $f$ 都以相同的“频率” $\sqrt{K}$ [振荡](@entry_id:267781)，并且都在距离 $\pi/\sqrt{K}$ 处达到最小值点。这迫使[流形的直径](@entry_id:634967)恰好为 $\pi/\sqrt{K}$，并且具有高度的对称性，最终被证明只能是标[准球](@entry_id:169696)面 [@problem_id:3071874]。

反过来，一个半径为 $R=1/\sqrt{K}$ 的标[准球](@entry_id:169696)面，其[截面曲率](@entry_id:159738)恒为 $K$，里奇曲率恒为 $(n-1)Kg$。通过直接计算可知，其第一个非零[特征值](@entry_id:154894)恰好为 $\lambda_1 = n/R^2 = nK$，对应的[特征函数](@entry_id:186820)（例如，嵌入到 $\mathbb{R}^{n+1}$ 中的坐标函数）满足 $\nabla^2 f = -Kfg$。这些特征函数的维数为 $n+1$ [@problem_id:3055932]。

综上，我们得到完整的刚性结论：对于一个满足 $\operatorname{Ric} \ge (n-1)Kg$ ($K0$) 的 $n$ 维紧致无边黎曼流形，其第一个非零[特征值](@entry_id:154894) $\lambda_1 \ge nK$。并且，等号 $\lambda_1 = nK$ 成立当且仅当该[流形](@entry_id:153038)等距于半径为 $1/\sqrt{K}$ 的标[准球](@entry_id:169696)面 [@problem_id:3055900] [@problem_id:3071814]。

### [适用范围](@entry_id:636189)与局限性

深刻的数学定理往往伴随着严格的适用条件。[Lichnerowicz估计](@entry_id:187368)也不例外，理解其假设的必要性，有助于我们更准确地把握其内涵。

**曲率条件的必要性**

假设 $\operatorname{Ric} \ge (n-1)K g$ 中常数 $K$ 的符号至关重要。如果 $K \le 0$，[Lichnerowicz估计](@entry_id:187368) $\lambda_1 \ge nK$ 只能给出一个非正的下界（例如 $\lambda_1 \ge 0$），这对于一个已知为正的 $\lambda_1$ 来说是平凡的，无法提供任何有意义的正下界。

我们可以通过一个**尺度变换**的论证来理解为何在 $K \le 0$ 时不可能存在一个统一的正下界。假设[流形](@entry_id:153038) $(M,g)$ 满足 $\operatorname{Ric} \ge (n-1)Kg$ 且 $K \le 0$。考虑一个新的度量 $\tilde{g} = c^2 g$，其中 $c$ 是一个大的正常数。里奇曲率在尺度变换下不变，即 $\operatorname{Ric}(\tilde{g}) = \operatorname{Ric}(g)$，而[特征值](@entry_id:154894)则按 $\lambda_1(\tilde{g}) = \lambda_1(g)/c^2$ 的方式缩放。尽管新度量下的曲率条件 $\operatorname{Ric}(\tilde{g}) \ge (n-1)(K/c^2)\tilde{g}$ 仍然满足非正下界的要求，但其[特征值](@entry_id:154894) $\lambda_1(\tilde{g})$ 却可以随着 $c$ 的增大而变得任意小。这意味着，在所有满足非[正里奇曲率](@entry_id:199145)下界的[流形](@entry_id:153038)族中，$\lambda_1$ 的下确界为零。

一个具体的例子是平坦的环面 $\mathbb{T}^n$。其[里奇曲率](@entry_id:162038)恒为零，满足 $K=0$ 的条件。通过拉伸环面的边长，我们可以构造出一族保持平坦（即 $\operatorname{Ric}=0$）但 $\lambda_1$ 可以任意小的[流形](@entry_id:153038)。这直观地表明，当曲率不为正时，[流形](@entry_id:153038)可以“松垮”地向任意尺度伸展，从而使其基本[振动频率](@entry_id:199185)趋于零 [@problem_id:3055878]。

此外，仅仅假设一个更弱的曲率条件，例如只对**标量曲率** $R$ 作出下界 $R \ge n(n-1)K$，是不足以保证 $\lambda_1 \ge nK$ 的。[Bochner公式](@entry_id:187951)的证明本质上依赖于对所有方向 $\nabla f$ 上的里奇曲率进行控制。一个反例可以是乘[积流形](@entry_id:270208) $\mathbb{S}^{n-1} \times \mathbb{S}^1$。通过选择一个非常“细长”的环路因子 $\mathbb{S}^1$，其整体[标量曲率](@entry_id:157547)可以为正，但其第一个[特征值](@entry_id:154894)却可以做得任意小，从而违反[Lichnerowicz估计](@entry_id:187368) [@problem_id:3071814]。

**[流形](@entry_id:153038)结构的必要性**

定理的两个拓扑假设——**紧致性**和**无边性**——也是不可或缺的。

-   **紧致性与无边性**：这两个条件保证了我们可以使用散度定理来断定 $\int_M \Delta (|\nabla f|^2) \, d\mu = 0$。如果[流形](@entry_id:153038)非紧，这个积分通常不为零，因为存在“无穷远处的边界项”。此时，必须引入额外的条件，例如函数的衰减行为，并通过截断函数的技巧来处理 [@problem_id:3055914]。
-   **边界的存在**：如果[流形](@entry_id:153038) $M$ 有非空的边界 $\partial M$，[散度定理](@entry_id:143110)会引入一个边界积分项。即使我们施加[诺伊曼边界条件](@entry_id:142124)（Neumann boundary condition），即 $\frac{\partial f}{\partial \nu}|_{\partial M} = 0$，[Bochner公式](@entry_id:187951)的积分版本中仍会包含一个与边界的第二基本形式相关的项。只有当边界是凸的（convex boundary），这个边界项才能保证有正确的符号，从而使得估计成立。对于具有凹边界的[流形](@entry_id:153038)，$\lambda_1$ 可以小于 $nK$ [@problem_id:3071814]。

总而言之，[Lichnerowicz特征值估计](@entry_id:192504)及其[刚性定理](@entry_id:198222)，是在一组精心选择的几何与拓扑条件下，对曲率与谱之间相互作用的精确刻画。它不仅是一个优美的数学结论，更为我们深入理解黎曼流形的几何分析提供了[范式](@entry_id:161181)和工具。