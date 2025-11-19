## 引言
在现代泛函分析中，为了理解一个[线性算子](@entry_id:149003)的深层结构，我们往往不直接研究算子本身，而是研究其[预解算子](@entry_id:271964)。[预解算子](@entry_id:271964) $R_\lambda(A) = (A - \lambda I)^{-1}$ 将算子的代数谱性质与[复分析](@entry_id:167282)的强大工具联系在一起，是谱理论的基石。然而，[预解算子](@entry_id:271964)本身是一个依赖于复参数 $\lambda$ 的函数家族，一个核心问题随之产生：不同参数下的[预解算子](@entry_id:271964)之间存在何种联系？这个知识上的缺口，即缺乏对[预解算子](@entry_id:271964)作为 $\lambda$ 的函数的整体结构的理解，正是本章所要解决的。

本文将深入探讨一个解答此问题的关键工具——**[第一预解恒等式](@entry_id:272370)**。通过学习本文，您将掌握这一恒等式如何从简单的代数操作中推导出来，并揭示其背后丰富的理论内涵和广泛的应用价值。
*   在“**原理与机制**”一章中，我们将详细推导[第一预解恒等式](@entry_id:272370)，并探索其直接的理论推论，例如[预解算子](@entry_id:271964)族的[交换性](@entry_id:140240)、解析性，以及它与[算子谱](@entry_id:276315)的紧密联系。
*   接下来，在“**应用与[交叉](@entry_id:147634)学科联系**”一章中，我们将展示这同一个恒等式如何“变身”为量子物理中的[Dyson方程](@entry_id:146246)、[积分方程理论](@entry_id:189100)中的[希尔伯特恒等式](@entry_id:266640)，以及控制理论中的[系统响应](@entry_id:264152)关系，从而领略其作为基础科学原理的强大生命力。
*   最后，在“**动手实践**”部分，我们提供了一系列从具体矩阵计算到抽象[函数空间](@entry_id:143478)应用的练习，帮助您将理论知识内化为解决问题的实用技能。

让我们从[第一预解恒等式](@entry_id:272370)的基本原理出发，开启这段连接抽象理论与具体应用的探索之旅。

## 原理与机制

在研究[有界线性算子](@entry_id:180446) $A$ 的[谱理论](@entry_id:275351)时，[预解算子](@entry_id:271964) $R_\lambda(A)$ 扮演着核心角色。正如前一章所定义，对于复[巴拿赫空间](@entry_id:143833) $X$ 上的[有界线性算子](@entry_id:180446) $A$，其[预解集](@entry_id:261708) $\rho(A)$ 是所有使得算子 $A - \lambda I$ 存在有界逆的复数 $\lambda$ 的集合。对于任意 $\lambda \in \rho(A)$，[预解算子](@entry_id:271964)定义为 $R_\lambda(A) = (A - \lambda I)^{-1}$。[预解算子](@entry_id:271964)将算子的代数性质与[复分析](@entry_id:167282)的强大工具联系起来。本章的核心是探讨一个被称为 **[第一预解恒等式](@entry_id:272370) (first resolvent identity)** 或 **[希尔伯特恒等式](@entry_id:266640) (Hilbert's identity)** 的基本关系式，并揭示其在谱理论中的深刻影响。

### [第一预解恒等式](@entry_id:272370)的推导

[第一预解恒等式](@entry_id:272370)本身源于一个极其简单的代数观察。考虑属于[预解集](@entry_id:261708) $\rho(A)$ 的两个不同复数 $\lambda$ 和 $\mu$。我们可以通过引入和消去同一个项来建立 $A - \lambda I$ 和 $A - \mu I$ 之间的联系：
$$
A - \lambda I = (A - \mu I) + (\mu - \lambda)I
$$
这个等式看似平凡，但它构成了推导的基石。为了从这个关于算子 $A$ 的恒等式转向一个关于其[预解算子](@entry_id:271964)的恒等式，我们需要利用逆算子的定义。

让我们从一个略有不同的形式出发，这能使代数推导更为直接 [@problem_id:1890653]：
$$
A - \lambda I = (A - \mu I) - (\lambda - \mu)I
$$
由于 $\lambda \in \rho(A)$，算子 $R_\lambda(A) = (A - \lambda I)^{-1}$ 存在。我们将上述等式从左边乘以 $R_\lambda(A)$：
$$
R_\lambda(A)(A - \lambda I) = R_\lambda(A)(A - \mu I) - (\lambda - \mu)R_\lambda(A)I
$$
根据逆的定义，$R_\lambda(A)(A - \lambda I) = I$，因此我们得到：
$$
I = R_\lambda(A)(A - \mu I) - (\lambda - \mu)R_\lambda(A)
$$
现在，由于 $\mu$ 同样在[预解集](@entry_id:261708)中，算子 $R_\mu(A) = (A - \mu I)^{-1}$ 也存在。我们将上式从右边乘以 $R_\mu(A)$：
$$
I \cdot R_\mu(A) = \left( R_\lambda(A)(A - \mu I) - (\lambda - \mu)R_\lambda(A) \right) R_\mu(A)
$$
利用算子乘法的[分配律](@entry_id:144084)，得到：
$$
R_\mu(A) = R_\lambda(A)(A - \mu I)R_\mu(A) - (\lambda - \mu)R_\lambda(A)R_\mu(A)
$$
再次利用逆的定义，$(A - \mu I)R_\mu(A) = I$，上式简化为：
$$
R_\mu(A) = R_\lambda(A)I - (\lambda - \mu)R_\lambda(A)R_\mu(A)
$$
移项后，我们便得到了 **[第一预解恒等式](@entry_id:272370)**:
$$
R_\lambda(A) - R_\mu(A) = (\lambda - \mu)R_\lambda(A)R_\mu(A)
$$
这个恒等式建立了在[预解集](@entry_id:261708)中任意两点处的[预解算子](@entry_id:271964)之间的精确关系。它是后续所有讨论的逻辑起点。值得注意的是，虽然我们的推导基于[有界算子](@entry_id:264879)，但该恒等式及其许多推论在更广泛的[闭算子](@entry_id:274252)框架下依然成立。

### 基本代数性质

[第一预解恒等式](@entry_id:272370)揭示了[预解算子](@entry_id:271964)家族丰富的[代数结构](@entry_id:137052)。一些深刻的性质是其直接的推论。

#### [预解算子](@entry_id:271964)的交换性

一个初看之下并不明显的结论是，对于[预解集](@entry_id:261708)中任意两点 $\lambda$ 和 $\mu$，对应的[预解算子](@entry_id:271964)是可交换的，即 $R_\lambda(A)R_\mu(A) = R_\mu(A)R_\lambda(A)$。

我们可以通过对称地书写预解恒等式来证明这一点 [@problem_id:1890629]。首先，对于 $\lambda \neq \mu$，我们可以将恒等式两边同除以 $(\lambda - \mu)$：
$$
R_\lambda(A)R_\mu(A) = \frac{1}{\lambda - \mu} (R_\lambda(A) - R_\mu(A))
$$
现在，交换 $\lambda$ 和 $\mu$ 的角色，恒等式同样成立：
$$
R_\mu(A) - R_\lambda(A) = (\mu - \lambda)R_\mu(A)R_\lambda(A)
$$
同样地，两边同除以 $(\mu - \lambda)$：
$$
R_\mu(A)R_\lambda(A) = \frac{1}{\mu - \lambda} (R_\mu(A) - R_\lambda(A)) = \frac{-1}{\lambda - \mu} (-(R_\lambda(A) - R_\mu(A))) = \frac{1}{\lambda - \mu} (R_\lambda(A) - R_\mu(A))
$$
比较两个表达式的右侧，我们立即得到：
$$
R_\lambda(A)R_\mu(A) = R_\mu(A)R_\lambda(A)
$$
这个[交换性](@entry_id:140240)质是至关重要的。它意味着由不同参数的[预解算子](@entry_id:271964)构成的乘积的顺序可以任意调换。例如，这意味着任意多项式，如 $R_\lambda(A)^n$ 和 $R_\mu(A)^m$，也必然是可交换的。这一性质极大地简化了涉及[预解算子](@entry_id:271964)的代数运算。

#### 其他代数关系

[预解算子](@entry_id:271964)满足的其他代数关系也很有启发性。例如，一个在证明中非常有用的关系是 $(A - \mu I)R_\lambda(A) = I + (\lambda - \mu)R_\lambda(A)$ [@problem_id:1890667]。其推导非常直接：
$$
(A - \mu I)R_\lambda(A) = ((A - \lambda I) + (\lambda - \mu)I)R_\lambda(A) = (A - \lambda I)R_\lambda(A) + (\lambda - \mu)IR_\lambda(A) = I + (\lambda - \mu)R_\lambda(A)
$$
此外，预解恒等式可以推广到三个或更多点。对于[预解集](@entry_id:261708)中三个不同的点 $\lambda, \mu, \nu$，它们满足一个优美的循环关系，有时被称为 **陪链关系 (cocycle relation)** [@problem_id:1890676]。我们可以通过将预解恒等式改写为 $(\lambda-\mu)R_\lambda R_\mu = R_\lambda - R_\mu$ 并对三对点 $(\lambda, \mu)$, $(\mu, \nu)$ 和 $(\nu, \lambda)$ 求和来发现它：
$$
(\lambda - \mu)R_\lambda(A)R_\mu(A) = R_\lambda(A) - R_\mu(A)
$$
$$
(\mu - \nu)R_\mu(A)R_\nu(A) = R_\mu(A) - R_\nu(A)
$$
$$
(\nu - \lambda)R_\nu(A)R_\lambda(A) = R_\nu(A) - R_\lambda(A)
$$
将这三个等式相加，右侧的项会成对抵消：
$$
(R_\lambda(A) - R_\mu(A)) + (R_\mu(A) - R_\nu(A)) + (R_\nu(A) - R_\lambda(A)) = 0
$$
因此，我们得到：
$$
(\lambda - \mu)R_\lambda(A)R_\mu(A) + (\mu - \nu)R_\mu(A)R_\nu(A) + (\nu - \lambda)R_\nu(A)R_\lambda(A) = \mathbf{0}
$$
其中 $\mathbf{0}$ 是零算子。这些关系共同描绘了一幅由[预解算子](@entry_id:271964)构成的丰富[代数结构](@entry_id:137052)的图景。

### [预解式](@entry_id:199555)的解析性

[第一预解恒等式](@entry_id:272370)的最重要推论之一是，算子值函数 $\lambda \mapsto R_\lambda(A)$ 在其定义域 $\rho(A)$ 上是 **解析的 (analytic)**。这意味着它可以局部地表示为一个收敛的算子[幂级数](@entry_id:146836)。

#### [诺伊曼级数](@entry_id:191685)展开

预解恒等式提供了一种从已知点 $\mu \in \rho(A)$ 处的[预解算子](@entry_id:271964) $R_\mu(A)$ 来构造邻近点 $\lambda$ 处的[预解算子](@entry_id:271964) $R_\lambda(A)$ 的方法。首先，我们将恒等式整理为 $R_\lambda(A)$ 的表达式 [@problem_id:1890619]：
$$
R_\lambda(A) - (\lambda - \mu)R_\lambda(A)R_\mu(A) = R_\mu(A)
$$
由于[预解算子](@entry_id:271964)相互交换，我们可以将 $R_\lambda(A)$ 因子提取出来：
$$
R_\lambda(A)(I - (\lambda - \mu)R_\mu(A)) = R_\mu(A)
$$
如果算子 $(I - (\lambda - \mu)R_\mu(A))$ 是可逆的，我们就可以得到 $R_\lambda(A)$ 的一个闭合表达式：
$$
R_\lambda(A) = R_\mu(A) \left(I - (\lambda - \mu)R_\mu(A)\right)^{-1}
$$
在[巴拿赫代数](@entry_id:266869)理论中，如果一个元素 $T$ 的范数 $\|T\|  1$，那么 $(I-T)$ 就是可逆的，并且其逆可以由一个几何级数——**[诺伊曼级数](@entry_id:191685) (Neumann series)**——给出：$(I-T)^{-1} = \sum_{n=0}^{\infty} T^n$。应用到我们的情况，只要 $\|(\lambda - \mu)R_\mu(A)\|  1$，即 $|\lambda - \mu|  1/\|R_\mu(A)\|$，上述逆就存在，并且我们可以得到 $R_\lambda(A)$ 的[幂级数展开](@entry_id:273325) [@problem_id:1890636]：
$$
R_\lambda(A) = R_\mu(A) \sum_{n=0}^{\infty} \left( (\lambda - \mu)R_\mu(A) \right)^n = \sum_{n=0}^{\infty} (\lambda - \mu)^n R_\mu(A)^{n+1}
$$
这个展开式表明，$R_\lambda(A)$ 在点 $\mu$ 的一个邻域内是 $\lambda$ 的一个[解析函数](@entry_id:139584)，其系数由 $R_\mu(A)$ 的幂次给出。由于 $\mu$ 是 $\rho(A)$ 中的任意一点，这证明了[预解算子](@entry_id:271964)在整个[预解集](@entry_id:261708)上是（局部）解析的。

#### [预解算子](@entry_id:271964)的导数

作为[解析函数](@entry_id:139584)，我们可以计算 $R_\lambda(A)$ 关于 $\lambda$ 的导数。利用导数的定义和预解恒等式，这个计算异常简洁 [@problem_id:1890665]。导数的定义是：
$$
\frac{d}{d\lambda} R_\lambda(A) = \lim_{h \to 0} \frac{R_{\lambda+h}(A) - R_\lambda(A)}{h}
$$
将 $\mu = \lambda + h$ 代入预解恒等式，我们有 $R_{\lambda+h}(A) - R_\lambda(A) = (\lambda+h - \lambda)R_{\lambda+h}(A)R_\lambda(A) = h R_{\lambda+h}(A)R_\lambda(A)$。因此，[差商](@entry_id:136462)为：
$$
\frac{R_{\lambda+h}(A) - R_\lambda(A)}{h} = R_{\lambda+h}(A)R_\lambda(A)
$$
由于预解函数是解析的，它必然是连续的。因此，当 $h \to 0$ 时，$R_{\lambda+h}(A)$ 在算子范数下趋近于 $R_\lambda(A)$。取极限得到：
$$
\frac{d}{d\lambda} R_\lambda(A) = R_\lambda(A)^2
$$
这个优美的公式——[预解算子](@entry_id:271964)的导数是它自身的平方——是[谱理论](@entry_id:275351)中的一个经典结果。它再次凸显了预解恒等式的核心作用。

#### 预解恒等式的刻画

反过来，预解恒等式也足以刻画一个函数是否为某个算子的预解函数。更精确地说，如果一个定义在复平面某个开集 $D$ 上的算子值函数 $F(\lambda)$ 满足[第一预解恒等式](@entry_id:272370)，那么它必定是某个固定算子 $T$ 的预解函数，即 $F(\lambda) = (T - \lambda I)^{-1}$ (或 $( \lambda I - T)^{-1}$，取决于具体形式)。

我们可以通过一个具体的例子来说明这一点 [@problem_id:1890634]。假设一个[矩阵值函数](@entry_id:199897) $F(\lambda)$ 满足预解恒等式。为了找到它所对应的算子 $T$，我们只需对其求逆：
$$
(T - \lambda I) = F(\lambda)^{-1}
$$
整理后得到 $T = \lambda I + F(\lambda)^{-1}$。由于 $T$ 是一个不依赖于 $\lambda$ 的固定算子，表达式 $\lambda I + F(\lambda)^{-1}$ 在 $F(\lambda)$ 的定义域内必须是一个常数算子。通过计算这个表达式，我们就能确定 $T$。这个事实表明，[第一预解恒等式](@entry_id:272370)并非[预解算子](@entry_id:271964)的一个偶然属性，而是其内在本质的体现。

### 与谱的联系

[预解算子](@entry_id:271964)在[预解集](@entry_id:261708) $\rho(A)$ 上是解析的，这自然引出一个问题：当 $\lambda$ 从[预解集](@entry_id:261708)逼近谱 $\sigma(A)$ 时，会发生什么？谱是[预解算子](@entry_id:271964)解析性的自然边界。

#### 谱点处[预解算子](@entry_id:271964)的无界性

一个基础而重要的结论是，当 $\lambda$ 趋近于谱中的任意一点 $\lambda_0 \in \sigma(A)$ 时，[预解算子](@entry_id:271964)的范数必定趋于无穷，即 $\|R_\lambda(A)\| \to \infty$。因此，极限 $\lim_{\lambda \to \lambda_0} R_\lambda(A)$ 在算子范数拓扑下是不存在的 [@problem_id:1890626]。

这个结论的证明恰恰依赖于我们之前导出的[诺伊曼级数](@entry_id:191685)展开的[收敛条件](@entry_id:166121)。我们知道，如果 $\mu \in \rho(A)$，那么以 $\mu$ 为中心、半径为 $1/\|R_\mu(A)\|$ 的开圆盘内的所有点也都属于 $\rho(A)$。这意味着，从点 $\mu$ 到谱 $\sigma(A)$ 的距离至少是 $1/\|R_\mu(A)\|$，即：
$$
\text{dist}(\mu, \sigma(A)) \ge \frac{1}{\|R_\mu(A)\|}
$$
这个不等式可以改写为：
$$
\|R_\mu(A)\| \ge \frac{1}{\text{dist}(\mu, \sigma(A))}
$$
现在，让 $\mu \in \rho(A)$ 沿着一条路径逼近谱中的一点 $\lambda_0 \in \sigma(A)$。由于谱是[闭集](@entry_id:136446)，$\text{dist}(\mu, \sigma(A))$ 将趋近于 $\text{dist}(\lambda_0, \sigma(A)) = 0$。根据上述不等式，这意味着 $\|R_\mu(A)\|$ 必须趋于无穷大。因此，[预解算子](@entry_id:271964)不可能在谱点收敛到任何[有界线性算子](@entry_id:180446)。谱正是[预解算子](@entry_id:271964)范数“爆炸”的地方。

#### [谱投影](@entry_id:265201)与[空间分解](@entry_id:755142)

[预解算子](@entry_id:271964)的[解析性](@entry_id:140716)质使其成为构建所谓 **全纯[泛函演算](@entry_id:138358) (holomorphic functional calculus)** 的关键工具。其核心思想是，对于在谱 $\sigma(A)$ 的一个邻域上解析的函数 $f(z)$，可以通过一个围线积分来定义算子 $f(A)$：
$$
f(A) = \frac{1}{2\pi i} \oint_\gamma f(z) R_z(A) \, dz
$$
其中 $\gamma$ 是一条包围 $\sigma(A)$ 的简单闭合围道。

[泛函演算](@entry_id:138358)的一个特别重要的应用是构造 **[谱投影](@entry_id:265201) (spectral projections)**。假设[算子的谱](@entry_id:272027)可以被分解为两个不相交的紧致[子集](@entry_id:261956) $\sigma(A) = \sigma_1 \cup \sigma_2$。我们可以选择两条不相交的闭合围道 $\gamma_1$ 和 $\gamma_2$，使得 $\gamma_1$ 仅包围 $\sigma_1$，而 $\gamma_2$ 仅包围 $\sigma_2$。然后，我们可以定义两个算子：
$$
P_1 = \frac{1}{2\pi i} \oint_{\gamma_1} R_z(A) \, dz \quad \text{和} \quad P_2 = \frac{1}{2\pi i} \oint_{\gamma_2} R_z(A) \, dz
$$
可以证明这两个算子是[投影算子](@entry_id:154142)（即 $P_1^2=P_1, P_2^2=P_2$），它们将空间 $X$ 分解为与谱部分 $\sigma_1$ 和 $\sigma_2$ 相关联的[不变子空间](@entry_id:152829)。

[第一预解恒等式](@entry_id:272370)在这里再次展现了其威力，它可以用来证明这些不同谱部分对应的投影是 **正交的**，即 $P_1 P_2 = \mathbf{0}$ [@problem_id:1890649]。考虑它们的乘积：
$$
P_1 P_2 = \left( \frac{1}{2\pi i} \oint_{\gamma_1} R_z(A) \, dz \right) \left( \frac{1}{2\pi i} \oint_{\gamma_2} R_w(A) \, dw \right) = -\frac{1}{4\pi^2} \oint_{\gamma_1} \oint_{\gamma_2} R_z(A)R_w(A) \, dw \, dz
$$
利用预解恒等式 $R_z(A)R_w(A) = \frac{R_z(A) - R_w(A)}{z-w}$，我们得到：
$$
P_1 P_2 = -\frac{1}{4\pi^2} \oint_{\gamma_1} \oint_{\gamma_2} \frac{R_z(A) - R_w(A)}{z-w} \, dw \, dz
$$
[交换积分次序](@entry_id:200463)并分解积分：
$$
P_1 P_2 = -\frac{1}{4\pi^2} \left( \oint_{\gamma_1} R_z(A) \left( \oint_{\gamma_2} \frac{1}{z-w} \, dw \right) dz - \oint_{\gamma_2} R_w(A) \left( \oint_{\gamma_1} \frac{1}{z-w} \, dz \right) dw \right)
$$
根据[柯西积分定理](@entry_id:194141)，对于固定的 $z \in \gamma_1$，点 $z$ 位于围道 $\gamma_2$ 的外部，因此内部的积分 $\oint_{\gamma_2} \frac{1}{z-w} \, dw = 0$。同样，对于固定的 $w \in \gamma_2$，点 $w$ 位于围道 $\gamma_1$ 的外部，因此 $\oint_{\gamma_1} \frac{1}{z-w} \, dz = 0$。两个积分都为零，因此我们得出结论：
$$
P_1 P_2 = \mathbf{0}
$$
这个结果表明，与不相交谱部分相关联的[子空间](@entry_id:150286)是[相互独立](@entry_id:273670)的。这一深刻的结构性结论，直接源于[预解算子](@entry_id:271964)满足的[第一预解恒等式](@entry_id:272370)。从一个简单的代数恒等式出发，我们最终能够将算子作用的空间根据其谱进行分解，这充分展示了[第一预解恒等式](@entry_id:272370)在现代[算子理论](@entry_id:139990)和数学物理中的基础性地位。