## 引言
在自然界和科学实验中，完全孤立的系统极为罕见。更为普遍的图景是，我们所关注的系统——无论是单个分子、一块晶体，还是复杂的[生物大分子](@entry_id:265296)——都沉浸在一个巨大的环境中，并与其不断交换能量。当系统与这个温度恒定的“[热储](@entry_id:143608)”达到热平衡时，我们该如何描述它的行为？又该如何从其微观的量子或经典状态，预测其宏观的[热力学性质](@entry_id:146047)？

本文旨在系统地回答这些问题，其核心是介绍[统计力](@entry_id:194984)学中一个至关重要的理论框架：正则系综。我们将首先在“原理与机制”一章中，深入探讨[正则系综](@entry_id:142391)的基石——[玻尔兹曼分布](@entry_id:142765)，并引入其核心数学工具——[配分函数](@entry_id:193625)。你将学到这个看似简单的“状态求和”如何神奇地编码了系统的全部[热力学](@entry_id:141121)信息。随后，在“应用与跨学科联系”一章中，我们将通过物理学、化学、[生物物理学](@entry_id:154938)等领域的生动案例，展示[正则系综](@entry_id:142391)理论的强大解释力和预测能力。最后，“动手实践”部分将提供具体的计算练习，帮助你将理论知识转化为解决实际问题的技能。通过这趟旅程，你将掌握连接微观世界与宏观世界的关键钥匙。

## 原理与机制

在[统计力](@entry_id:194984)学中，我们研究的系统很少是完全孤立的。更常见的情况是，一个我们感兴趣的“系统”（例如，一个分子、一块晶体或一瓶气体）与一个巨大的“环境”或“热储”进行能量交换。这种设置——系统与恒定温度的热储接触并达到热平衡——在物理、化学和生物学中无处不在。描述这种系统的理论框架被称为**正则系综 (canonical ensemble)**。本章将深入探讨[正则系综](@entry_id:142391)的基本原理，并阐明其核心工具——**[配分函数](@entry_id:193625) (partition function)**——如何成为连接微观[量子态](@entry_id:146142)与宏观[热力学性质](@entry_id:146047)的桥梁。

### [正则系综](@entry_id:142391)与玻尔兹曼分布

想象一个我们感兴趣的小系统 S，它与一个非常大的[热储](@entry_id:143608) R 处于热接触状态。热储的特点是它足够大，以至于即使与系统 S [交换能](@entry_id:137069)量，其自身温度 $T$ 始终保持不变。S 和 R 组成的复合系统 (S+R) 是孤立的，其总能量 $E_{total}$ 是恒定的。

由于 S 和 R 之间可以交换能量，系统 S 的能量 $E_s$ 并不是一个定值，而是在不同时刻可以取不同的值。我们的目标是，在系统与热储达到[热平衡](@entry_id:141693)时，求出系统 S 处于某个特定微观状态 $s$（能量为 $E_s$）的概率 $P_s$。

根据等概率原理，对于孤立的复合系统，任何总能量为 $E_{total}$ 的可及微观状态都是等可能出现的。假设系统 S 处于能量为 $E_s$ 的状态 $s$ 时，热储 R 的能量就是 $E_R = E_{total} - E_s$。系统 S 处于状态 $s$ 的概率 $P_s$ 正比于热储 R 可及的微观状态数 $\Omega_R(E_R)$。即：
$P_s \propto \Omega_R(E_{total} - E_s)$。

利用[热储](@entry_id:143608)的熵 $S_R = k_B \ln \Omega_R$，我们可以写出 $\ln P_s \approx \text{const} + \ln \Omega_R(E_{total} - E_s) = \text{const} + \frac{S_R(E_{total} - E_s)}{k_B}$。由于系统 S 的能量 $E_s$ 远小于[热储](@entry_id:143608)的总能量 $E_{total}$，我们可以对熵 $S_R$ 在 $E_{total}$ 附近进行泰勒展开：
$S_R(E_{total} - E_s) \approx S_R(E_{total}) - \left(\frac{\partial S_R}{\partial E_R}\right)_{E_R=E_{total}} E_s$。
根据[热力学](@entry_id:141121)定义，$\left(\frac{\partial S_R}{\partial E_R}\right) = \frac{1}{T}$。因此，
$\ln P_s \approx \text{const} - \frac{E_s}{k_B T}$。
由此，我们得到了著名的**玻尔兹曼分布 (Boltzmann distribution)**：
$P_s \propto \exp\left(-\frac{E_s}{k_B T}\right)$。

这个结果极为重要：在与温度为 $T$ 的[热储](@entry_id:143608)平衡时，系统处于一个高能量状态的概率呈指数衰减。这个指数因子 $\exp(-\beta E_s)$ 被称为**[玻尔兹曼因子](@entry_id:141054) (Boltzmann factor)**，其中 $\beta = \frac{1}{k_B T}$ 是一个在[统计力](@entry_id:194984)学中非常方便的参数，称为**[逆温](@entry_id:140086)度 (inverse temperature)**。

### [正则配分函数](@entry_id:154330)：对所有状态求和

为了将上述比例关系转化为等式，我们需要对所有可能的状态进行归一化。系统处于某个状态的概率之和必须为1。因此，概率 $P_s$ 的精确表达式是：
$P_s = \frac{\exp(-\beta E_s)}{\sum_j \exp(-\beta E_j)}$。

分母部分是对系统所有可能的微观状态 $j$ 的[玻尔兹曼因子](@entry_id:141054)求和，它被称为**[正则配分函数](@entry_id:154330) (canonical partition function)**，用符号 $Z$ 表示：
$Z = \sum_s \exp(-\beta E_s)$。
[配分函数](@entry_id:193625)的德语是 *Zustandssumme*，意为“状态求和”，$Z$ 因此得名。它是[正则系综](@entry_id:142391)中最重要的核心量。一旦知道了[配分函数](@entry_id:193625)，我们就可以计算出系统处于任何特定状态的概率。

在实际计算中，常常有多个微观状态拥有相同的能量，这种情况称为**简并 (degeneracy)**。如果能量为 $E_i$ 的能级有 $g_i$ 个简并的微观状态，我们可以将求和按能级进行分组：
$Z = \sum_{i} g_i \exp(-\beta E_i)$，
其中求和 $i$ 遍历所有不同的能级。

让我们通过一个具体的例子来理解如何计算[配分函数](@entry_id:193625)。考虑一个被限制在[晶格](@entry_id:196752)中的原子，它只有两个可及的能级：能量为 $0$ 的[基态](@entry_id:150928)（非简并，即 $g_0=1$）和能量为 $\Delta$ 的第一[激发态](@entry_id:261453)（三重简并，即 $g_1=3$）。该原子与温度为 $T$ 的[热储](@entry_id:143608)接触。根据[配分函数](@entry_id:193625)的定义，我们可以直接写出其[配分函数](@entry_id:193625) [@problem_id:1994942]：
$Z = g_0 \exp(-\beta E_0) + g_1 \exp(-\beta E_1) = 1 \cdot \exp(0) + 3 \cdot \exp(-\beta \Delta) = 1 + 3\exp(-\beta\Delta)$。

有了[配分函数](@entry_id:193625)，我们就能计算处于特定能级的概率。例如，该原子处于第一[激发态](@entry_id:261453)的概率是：
$P_{excited} = \frac{3\exp(-\beta\Delta)}{Z} = \frac{3\exp(-\beta\Delta)}{1 + 3\exp(-\beta\Delta)}$。
这个简单的例子展示了[配分函数](@entry_id:193625)作为归一化因子的直接作用。然而，它的威力远不止于此。

### [从配分函数推导热力学](@entry_id:140625)性质

[配分函数](@entry_id:193625)的深刻意义在于，它包含了系统所有的[热力学](@entry_id:141121)信息。通过对[配分函数](@entry_id:193625)进行数学运算，我们可以系统地推导出所有宏观[热力学](@entry_id:141121)量。

#### [平均能量](@entry_id:145892)

系统的平均能量 $\langle E \rangle$ 是所有可能状态能量的加权平均，权重即为各状态的概率：
$\langle E \rangle = \sum_s P_s E_s = \frac{1}{Z} \sum_s E_s \exp(-\beta E_s)$。
我们可以注意到，求和项 $\sum_s E_s \exp(-\beta E_s)$ 与[配分函数](@entry_id:193625) $Z = \sum_s \exp(-\beta E_s)$ 对 $\beta$ 的导数有关：
$-\frac{\partial Z}{\partial \beta} = \sum_s E_s \exp(-\beta E_s)$。
因此，平均能量可以简洁地表示为：
$\langle E \rangle = -\frac{1}{Z} \frac{\partial Z}{\partial \beta} = -\frac{\partial \ln Z}{\partial \beta}$。

这个公式功能强大。对于前述的[两能级原子](@entry_id:159911)系统 [@problem_id:1994942]，我们可以立即计算其[平均能量](@entry_id:145892)：
$\ln Z = \ln(1 + 3\exp(-\beta\Delta))$
$\langle E \rangle = -\frac{\partial}{\partial\beta} \ln(1 + 3\exp(-\beta\Delta)) = - \frac{1}{1 + 3\exp(-\beta\Delta)} \cdot (-3\Delta \exp(-\beta\Delta)) = \frac{3\Delta \exp(-\beta\Delta)}{1 + 3\exp(-\beta\Delta)}$。
将 $\beta = 1/(k_B T)$ 代回，即可得到平均能量与温度的函数关系。

#### 亥姆霍兹自由能、熵和[热容](@entry_id:137594)

[配分函数](@entry_id:193625)与[热力学](@entry_id:141121)的联系通过**亥姆霍兹自由能 (Helmholtz free energy)** $F$ 建立：
$F = -k_B T \ln Z = -\frac{1}{\beta} \ln Z$。
这个关系是[统计力](@entry_id:194984)学和[热力学](@entry_id:141121)之间的桥梁。一旦我们从微观状态计算出 $Z$，我们就可以通过 $F$ 得到所有其他的宏观[热力学](@entry_id:141121)量。

例如，熵 $S$ 可以通过 $F$ 对温度的导数得到：
$S = -\left(\frac{\partial F}{\partial T}\right)_V = \frac{\partial}{\partial T}(k_B T \ln Z) = k_B \ln Z + k_B T \frac{\partial \ln Z}{\partial T}$。
利用[链式法则](@entry_id:190743) $\frac{\partial}{\partial T} = \frac{d\beta}{dT} \frac{\partial}{\partial \beta} = -\frac{1}{k_B T^2} \frac{\partial}{\partial \beta}$，我们得到：
$S = k_B \ln Z + k_B T \left(-\frac{1}{k_B T^2}\right) \frac{\partial \ln Z}{\partial \beta} = k_B \ln Z - \frac{1}{T} (-\langle E \rangle) = \frac{\langle E \rangle - F}{T}$。
这正是[热力学](@entry_id:141121)关系 $F=U-TS$（在[统计力](@entry_id:194984)学中，内能 $U$ 即为[平均能量](@entry_id:145892) $\langle E \rangle$）的再现。该公式 $S = k_B(\ln Z + \beta \langle E \rangle)$ 允许我们计算系统的熵 [@problem_id:1994952]。

另一个重要的[热力学](@entry_id:141121)量是**[定容热容](@entry_id:147536) (heat capacity at constant volume)** $C_V$，它衡量系统储存能量的能力：
$C_V = \left(\frac{\partial \langle E \rangle}{\partial T}\right)_V$。
利用链式法则，我们再次将对 $T$ 的导数转换成对 $\beta$ 的导数：
$C_V = \frac{\partial \langle E \rangle}{\partial \beta} \frac{d\beta}{dT} = \frac{\partial}{\partial \beta} \left(-\frac{\partial \ln Z}{\partial \beta}\right) \left(-\frac{1}{k_B T^2}\right) = \frac{1}{k_B T^2} \frac{\partial^2 \ln Z}{\partial \beta^2}$。

#### [能量涨落](@entry_id:148029)

[正则系综](@entry_id:142391)中的系统能量不是固定的，它围绕平均值 $\langle E \rangle$ 涨落。涨落的幅度可以通过能量的[均方差](@entry_id:153618) $\sigma_E^2 = \langle (E - \langle E \rangle)^2 \rangle = \langle E^2 \rangle - \langle E \rangle^2$ 来度量。
类似于 $\langle E \rangle$ 的推导，我们可以证明 $\langle E^2 \rangle = \frac{1}{Z} \frac{\partial^2 Z}{\partial \beta^2}$。经过一些代数运算可以得到一个非常优美的关系：
$\sigma_E^2 = \frac{\partial^2 \ln Z}{\partial \beta^2}$。
将这个结果与上面 $C_V$ 的表达式联系起来，我们得到了一个深刻的结论 [@problem_id:1994959]：
$\sigma_E^2 = k_B T^2 C_V$。
这个**涨落-耗散定理 (fluctuation-dissipation theorem)** 的一个实例表明，系统的[能量涨落](@entry_id:148029)幅度直接与其[热容](@entry_id:137594)成正比。热容大的系统，其[能量涨落](@entry_id:148029)也更剧烈。这为宏观的热容提供了一个清晰的微观物理解释。

### [多粒子系统](@entry_id:192694)：可区分性与[量子统计](@entry_id:143815)

到目前为止，我们主要关注单个粒子或系统的[配分函数](@entry_id:193625)。当系统由多个粒子组成时，情况会变得更加复杂，特别是需要考虑粒子是否可以区分以及它们遵循的量子统计规律。

#### 可区分的[无相互作用粒子](@entry_id:152322)

最简单的情况是系统由 $N$ 个可区分且无相互作用的粒子组成，例如固定在[晶格](@entry_id:196752)不同位置的[分子开关](@entry_id:154643) [@problem_id:1994972]。由于粒子是可区分的（例如通过它们的位置来区分），系统的总状态可以由每个粒子的状态来唯一确定。因为粒子间没有相互作用，系统的总能量就是每个粒子能量的总和，$E_{total} = \epsilon_1 + \epsilon_2 + \dots + \epsilon_N$。
[总配分函数](@entry_id:190183) $Z_N$ 可以写成：
$Z_N = \sum_{\text{all states}} \exp[-\beta(\epsilon_1 + \dots + \epsilon_N)] = \left(\sum_{s_1} e^{-\beta\epsilon_{s_1}}\right) \left(\sum_{s_2} e^{-\beta\epsilon_{s_2}}\right) \dots \left(\sum_{s_N} e^{-\beta\epsilon_{s_N}}\right)$。
如果所有粒子都是相同的，它们的单粒子[配分函数](@entry_id:193625) $Z_1$ 都一样。因此，[总配分函数](@entry_id:190183)就是单粒子[配分函数](@entry_id:193625)的 $N$ 次方：
$Z_N = (Z_1)^N$。
系统的总平均能量也相应地为 $U = N \langle E_1 \rangle = -N \frac{\partial \ln Z_1}{\partial \beta}$。

#### 不可区分的[无相互作用粒子](@entry_id:152322)：[量子统计](@entry_id:143815)

在量子世界中，同类粒子是**不可区分 (indistinguishable)** 的。交换两个同类粒子的位置不会产生一个新的物理状态。这要求我们重新审视如何构建[多体系统](@entry_id:144006)的状态。此时，我们不能简单地将单粒子[配分函数](@entry_id:193625)相乘。相反，我们必须直接枚举整个系统的多体能级。

**1. [玻色子](@entry_id:138266) (Bosons)**：服从[玻色-爱因斯坦统计](@entry_id:139965)的粒子，如[光子](@entry_id:145192)和某些原子。任意数量的[玻色子](@entry_id:138266)可以占据同一个单粒子[量子态](@entry_id:146142)。
考虑一个由两个不可区分的[玻色子](@entry_id:138266)组成的系统，它们可以占据能量为 $0$ 和 $\epsilon$ 的两个单粒子能级 [@problem_id:1994969]。多体系统的状态由每个能级上的粒子数 $(n_0, n_1)$ 决定，且总粒子数 $n_0 + n_1 = 2$。可能的占据方式有：
- 两个粒子都在[基态](@entry_id:150928)：$(n_0, n_1) = (2, 0)$，总能量 $E = 2 \cdot 0 = 0$。
- 一个在[基态](@entry_id:150928)，一个在[激发态](@entry_id:261453)：$(n_0, n_1) = (1, 1)$，总能量 $E = 1 \cdot 0 + 1 \cdot \epsilon = \epsilon$。
- 两个粒子都在[激发态](@entry_id:261453)：$(n_0, n_1) = (0, 2)$，总能量 $E = 2 \cdot \epsilon = 2\epsilon$。
系统的[配分函数](@entry_id:193625)是对这三种可能的多体状态求和：
$Z = \exp(-\beta \cdot 0) + \exp(-\beta \cdot \epsilon) + \exp(-\beta \cdot 2\epsilon) = 1 + \exp(-\beta\epsilon) + \exp(-2\beta\epsilon)$。
可以看到，这个结果与可区分粒子的 $(Z_1)^2 = (e^{-\beta \cdot 0} + e^{-\beta \epsilon})^2 = 1 + 2e^{-\beta\epsilon} + e^{-2\beta\epsilon}$ 不同。

**2. [费米子](@entry_id:146235) (Fermions)**：服从[费米-狄拉克统计](@entry_id:140706)的粒子，如电子、质子和中子。它们遵循**[泡利不相容原理](@entry_id:141850) (Pauli exclusion principle)**，即两个或多个全同[费米子](@entry_id:146235)不能占据同一个[量子态](@entry_id:146142)。

让我们考虑一个更复杂的例子：两个无相互作用的电子（自旋为 $1/2$ 的[费米子](@entry_id:146235)）被限制在[一维无限深势阱](@entry_id:271157)中，并且只能占据最低的两个空间能级 $n=1$ 和 $n=2$ [@problem_id:1994932]。单粒子能级为 $E_n = \frac{n^2 \pi^2 \hbar^2}{2mL^2}$。每个空间能级 $n$ 还可以容纳自旋向上 ($\uparrow$) 和自旋向下 ($\downarrow$) 两个状态。因此，我们有四个单粒子“自旋-[轨道](@entry_id:137151)”态：$(n=1, \uparrow)$, $(n=1, \downarrow)$, $(n=2, \uparrow)$, $(n=2, \downarrow)$。
根据泡利原理，两个电子必须占据这四个态中的不同两个。我们一共有 $\binom{4}{2} = 6$ 种可能的多体状态。按总能量分组：
- 一个电子在 $(1, \uparrow)$，另一个在 $(1, \downarrow)$。总能量 $E = E_1 + E_1 = 2E_1$。这是一种组合方式（简并度为1）。
- 一个电子在 $n=1$ 能级，另一个在 $n=2$ 能级。电子的自旋可以是任意组合，总共有 $2 \times 2=4$ 种方式。总能量 $E = E_1 + E_2 = E_1 + 4E_1 = 5E_1$。简并度为4。
- 一个电子在 $(2, \uparrow)$，另一个在 $(2, \downarrow)$。总能量 $E = E_2 + E_2 = 8E_1$。简并度为1。

该系统的[配分函数](@entry_id:193625)就是对这几种可能性的玻尔兹曼因子求和：
$Z = 1 \cdot \exp(-2\beta E_1) + 4 \cdot \exp(-5\beta E_1) + 1 \cdot \exp(-8\beta E_1)$。
从这个 $Z$ 出发，就可以用标准公式 $\langle E \rangle = -\frac{\partial \ln Z}{\partial \beta}$ 计算系统的平均能量。这个例子清楚地展示了[量子统计](@entry_id:143815)如何深刻地影响系统的[热力学](@entry_id:141121)行为。

### [经典极限](@entry_id:148587)与连续系统

当温度很高或[粒子质量](@entry_id:156313)很大时，[量子能级](@entry_id:136393)之间的间距相对于热能 $k_B T$ 会变得非常小。在这种情况下，能谱可以近似看作是连续的，对[量子态](@entry_id:146142)的求和可以被积分所替代。这就是**经典极限 (classical limit)**。

#### 从求和到积分

考虑一个质量为 $m$ 的粒子被限制在长度为 $L$ 的一维盒子里。其[量子能级](@entry_id:136393)为 $E_n = \frac{n^2 \pi^2 \hbar^2}{2mL^2}$ ($n=1, 2, \dots$)。单粒子[配分函数](@entry_id:193625)是 $Z_1 = \sum_{n=1}^\infty \exp(-\beta E_n)$。在高温极限下，$k_B T \gg E_n$ 的[能级间距](@entry_id:181168)，求和可以近似为积分 [@problem_id:1994962]：
$Z_1 \approx \int_0^\infty \exp\left(-\beta \frac{n^2 \pi^2 \hbar^2}{2mL^2}\right) dn$。
这是一个标准的[高斯积分](@entry_id:187139)，结果为 $Z_1 = L \sqrt{\frac{mk_B T}{2\pi\hbar^2}}$。这个结果与[热德布罗意波长](@entry_id:143992)有关，表明了[配分函数](@entry_id:193625)与粒子运动的“量子体积”之间的联系。

#### [经典相空间](@entry_id:195767)积分

更一般地，在经典力学中，一个系统的状态由其[广义坐标](@entry_id:156576) $\mathbf{q}$ 和[广义动量](@entry_id:165699) $\mathbf{p}$ 在**相空间 (phase space)** 中的一个点来描述。经典[配分函数](@entry_id:193625)的定义是对应于量子求和的相空间积分：
$Z_1 = \frac{1}{h^d} \int \exp(-\beta H(\mathbf{q}, \mathbf{p})) d^d q d^d p$。
这里 $H(\mathbf{q}, \mathbf{p})$ 是系统的[哈密顿量](@entry_id:172864)（即总能量），$d$是系统的自由度数目，$h$ 是普朗克常数，作为相空间微元的体积单位出现，确保了[配分函数](@entry_id:193625)的无量纲性（在与量子结果对比时）。

让我们看一个例子：一个质量为 $m$ 的经典粒子被限制在半径为 $R$ 的球面（一个二维表面）上自由运动 [@problem_id:1994939]。
- 自由度 $d=2$。
- [哈密顿量](@entry_id:172864)只有动能：$H = \frac{p_x^2 + p_y^2}{2m}$（在任何局部切平面上）。
- 坐标积分 $\int d^2q$ 是粒子可及的“体积”，即球的表面积 $A = 4\pi R^2$。
- 动量积分 $\int \exp(-\beta \frac{p_x^2+p_y^2}{2m}) dp_x dp_y$ 是两个独立[高斯积分](@entry_id:187139)的乘积，结果为 $\frac{2\pi m}{\beta}$。
将各部分组合起来，得到单粒子[配分函数](@entry_id:193625)：
$Z_1 = \frac{1}{h^2} (4\pi R^2) \left(\frac{2\pi m}{\beta}\right) = \frac{8\pi^2 m R^2 k_B T}{h^2}$。
这个例子展示了如何通过将相空间积分解耦为坐标部分（构型积分）和动量部分来简化计算。

#### 连续变量的[概率分布](@entry_id:146404)

玻尔兹曼因子不仅给出离散状态的概率，也给出连续变量的[概率密度](@entry_id:175496)。对于一个处于势场 $V(x)$ 中的经典粒子，其在位置 $x$ 附近被发现的概率密度 $P(x)$ 正比于 $\exp(-\beta V(x))$ [@problem_id:1994973]。
$P(x) dx \propto \exp(-\beta V(x)) dx$。
一个很好的例子是用[光镊](@entry_id:157699)捕获的微小颗粒。其[势能](@entry_id:748988)可以近似为一维谐振子势 $V(x) = \frac{1}{2}\kappa x^2$。因此，其位置的概率密度函数是一个[高斯分布](@entry_id:154414)：
$P(x) = \mathcal{N} \exp\left(-\frac{\kappa x^2}{2k_B T}\right)$。
其中 $\mathcal{N}$ 是[归一化常数](@entry_id:752675)。这个[分布](@entry_id:182848)的形状直接反映了粒子在[热涨落](@entry_id:143642)下的行为，其宽度与温度的平方根成正比。这为我们提供了一个从实验测量的粒子位置[分布](@entry_id:182848)来直接推断温度或[陷阱刚度](@entry_id:198164)的方法。

#### [量子谐振子](@entry_id:140678)：一个贯穿始终的模型

量子谐振子（QHO）是[统计力](@entry_id:194984)学中的一个基石模型，其能级为 $E_n = \hbar\omega(n+1/2)$。它的[配分函数](@entry_id:193625)可以通过对一个[几何级数](@entry_id:158490)求和得到 [@problem_id:1994980]：
$Z = \sum_{n=0}^\infty \exp[-\beta\hbar\omega(n+1/2)] = \frac{\exp(-\beta\hbar\omega/2)}{1-\exp(-\beta\hbar\omega)} = \frac{1}{2\sinh(\beta\hbar\omega/2)}$。
有了这个[配分函数](@entry_id:193625)，我们可以计算任何我们感兴趣的量。例如，[振子](@entry_id:271549)处于第一[激发态](@entry_id:261453) ($n=1$) 的概率为：
$P_1 = \frac{\exp(-\beta E_1)}{Z} = \exp(-\beta\hbar\omega) - \exp(-2\beta\hbar\omega)$。
同样，我们可以用标准公式计算其[平均能量](@entry_id:145892)、[热容](@entry_id:137594)和熵 [@problem_id:1994952]，这些结果在描述[晶格振动](@entry_id:140970)（[声子](@entry_id:140728)）和分子振动等方面有着广泛的应用。

本章通过引入正则系综和[配分函数](@entry_id:193625)的概念，系统地展示了如何从微观的能级结构和统计规律出发，推导出宏观的热力学性质。[配分函数](@entry_id:193625)作为一个中心枢纽，连接了微观世界和宏观世界，是[统计力](@entry_id:194984)学中最强大和最优雅的工具之一。