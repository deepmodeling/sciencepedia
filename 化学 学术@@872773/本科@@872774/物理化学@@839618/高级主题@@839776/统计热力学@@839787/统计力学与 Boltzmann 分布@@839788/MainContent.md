## 引言
物理世界呈现出两个截然不同的层面：由原子和分子遵循量子力学规则构成的微观世界，以及我们日常经验中由温度、压力和体积等宏观量所描述的[热力学](@entry_id:141121)世界。如何在这两个层面之间建立一座坚实的桥梁，一直是物理化学的核心挑战之一。[统计力](@entry_id:194984)学正是为应对这一挑战而生，它提供了一套强大的理论框架，能够从微观粒子的统计行为出发，精确地预测和解释宏观系统的整体性质。

本文旨在深入探讨[统计力](@entry_id:194984)学的中心支柱——[玻尔兹曼分布](@entry_id:142765)与[配分函数](@entry_id:193625)。我们将揭示这些概念如何量化了温度对微观粒子能量[分布](@entry_id:182848)的控制作用，并展示[配分函数](@entry_id:193625)如何像一个“万能钥匙”一样，解锁了系统的所有[热力学](@entry_id:141121)秘密。通过本文的学习，你将能够理解从单个分子的量子能级到材料整体[热力学](@entry_id:141121)行为的完整推导路径。

在接下来的内容中，我们将分三个章节展开：
- **原理与机制** 将奠定理论基础，详细推导[玻尔兹曼分布](@entry_id:142765)，定义[配分函数](@entry_id:193625)，并阐明如何通过它计算内能、压强、热容等关键[热力学](@entry_id:141121)量，同时也会探讨涨落和[负温度](@entry_id:140023)等高级概念。
- **应用与跨学科联系** 将展示这些原理的强大威力，通过[化学反应](@entry_id:146973)、[材料科学](@entry_id:152226)、生物物理乃至计算机科学中的具体实例，说明[统计力](@entry_id:194984)学如何成为解决多样化科学问题的通用语言。
- **动手实践** 将提供一系列计算练习，帮助你将理论知识应用于具体问题，从而加深对核心概念的理解和掌握。

## 原理与机制

[统计力](@entry_id:194984)学的核心目标是建立微观量子世界与宏观[热力学](@entry_id:141121)世界之间的桥梁。在上一章中，我们介绍了系综、微观态和宏观态等基本概念。本章将深入探讨这一联系的核心——[玻尔兹曼分布](@entry_id:142765)与[配分函数](@entry_id:193625)，并阐明它们如何成为从单个分子的性质预测材料整体[热力学](@entry_id:141121)行为的强大工具。

### 玻尔兹曼分布与[配分函数](@entry_id:193625)

想象一个与巨大热库接触并达到热平衡的系统，其温度恒定为 $T$。这种系统可以通过[正则系综](@entry_id:142391)来描述。根据[统计力](@entry_id:194984)学的基本假设，系统处于具有能量 $E_i$ 的特定[微观态](@entry_id:147392) $i$ 的概率 $P_i$ 与一个指数因子成正比，这个因子被称为**[玻尔兹曼因子](@entry_id:141054)**。

$$ P_i \propto \exp\left(-\frac{E_i}{k_B T}\right) $$

其中 $k_B$ 是[玻尔兹曼常数](@entry_id:142384)。这个关系式——**[玻尔兹曼分布](@entry_id:142765)**——是[统计力](@entry_id:194984)学中最核心的概念之一。它告诉我们，在给定的温度下，能量越低的微观态被占据的概率越高。随着能量 $E_i$ 的增加，其占据概率呈指数衰减。

为了将这种正比关系转化为等式，我们需要一个[归一化常数](@entry_id:752675)。所有可能微观态的概率之和必须为1，即 $\sum_i P_i = 1$。因此，我们可以定义一个量 $Q$，它等于所有玻尔兹曼因子的总和：

$$ Q = \sum_i \exp\left(-\frac{E_i}{k_B T}\right) $$

这个量 $Q$ 被称为**[正则配分函数](@entry_id:154330)**（Canonical Partition Function）。它的名字来源于其物理意义：它描述了系统的总概率是如何在所有可及的微观态之间被“分配”的。一旦我们知道了[配分函数](@entry_id:193625)，任意微观态 $i$ 的概率就可以精确地写为：

$$ P_i = \frac{\exp\left(-\frac{E_i}{k_B T}\right)}{Q} $$

在许多物理和化学问题中，我们更关心的是系统处于某个特定**能级**（Energy Level）的概率，而不是某个特定的微观态。一个能级可能包含多个能量相同的[量子态](@entry_id:146142)，这种现象称为**简并**（degeneracy）。如果能量为 $E_j$ 的能级具有 $g_j$ 个简并态，那么系统处于该能级的概率 $P_j$ 就是这 $g_j$ 个态的概率之和。由于这些态的能量相同，它们的玻尔兹曼因子也相同，因此：

$$ P_j = \frac{g_j \exp\left(-\frac{E_j}{k_B T}\right)}{Q} $$

相应地，[配分函数](@entry_id:193625)的求和也可以按照能级来计算，将每个能级的简并度考虑在内：

$$ Q = \sum_j g_j \exp\left(-\frac{E_j}{k_B T}\right) $$

其中求和遍历所有不同的能级 $j$。这个形式在实际计算中更为常用。

例如，考虑一个简化的三能级[原子模型](@entry_id:137207)。其[基态能量](@entry_id:263704)为 $E_0 = 0$，无简并（$g_0=1$）。第一[激发态](@entry_id:261453)能量为 $E_1 = \epsilon$，是双重简并的（$g_1=2$）。第二[激发态](@entry_id:261453)能量为 $E_2 = 3\epsilon$，也是双重简并的（$g_2=2$）。假定更高能级的能量远大于 $k_B T$，可以忽略不计。该原子的[分子配分函数](@entry_id:152768) $q$（对于单个粒子，我们常用小写 $q$ 表示）为：
$$ q = \sum_{j=0}^{2} g_j \exp\left(-\frac{E_j}{k_B T}\right) = 1 \cdot \exp(0) + 2 \cdot \exp\left(-\frac{\epsilon}{k_B T}\right) + 2 \cdot \exp\left(-\frac{3\epsilon}{k_B T}\right) $$
$$ q = 1 + 2\exp\left(-\frac{\epsilon}{k_B T}\right) + 2\exp\left(-\frac{3\epsilon}{k_B T}\right) $$
利用这个[配分函数](@entry_id:193625)，我们可以计算原子处于任一能级的概率。例如，找到该原子处于第一[激发态](@entry_id:261453)（能量为 $\epsilon$）的概率为 [@problem_id:2006307]：
$$ P_1 = \frac{g_1 \exp\left(-\frac{\epsilon}{k_B T}\right)}{q} = \frac{2 \exp\left(-\frac{\epsilon}{k_B T}\right)}{1 + 2 \exp\left(-\frac{\epsilon}{k_B T}\right) + 2 \exp\left(-\frac{3\epsilon}{k_B T}\right)} $$
这个例子清晰地展示了简并度 $g_j$ 如何直接影响能级的占据概率。

### [配分函数](@entry_id:193625)的计算

[配分函数](@entry_id:193625)的计算是应用[统计力](@entry_id:194984)学的关键一步。对于简单的模型系统，[配分函数](@entry_id:193625)常常可以求得一个解析的**[闭合形式](@entry_id:271343)**（closed-form expression）。

考虑一个具有六个离散、非简并电子能级的假想分子，其能级为 $E_n = (n-1)\epsilon$，其中 $n=1, 2, ..., 6$。这是一个有限能级系统。其[配分函数](@entry_id:193625)是一个有限项的和 [@problem_id:2006292]：
$$ Q = \sum_{n=1}^{6} \exp\left(-\frac{(n-1)\epsilon}{k_B T}\right) = \sum_{m=0}^{5} \exp\left(-\frac{m\epsilon}{k_B T}\right) $$
这是一个[公比](@entry_id:275383)为 $r = \exp(-\epsilon/k_B T)$ 的几何级数。利用有限[几何级数](@entry_id:158490)求和公式 $\sum_{m=0}^{N-1} r^m = (1-r^N)/(1-r)$，我们得到：
$$ Q = \frac{1 - \left[\exp\left(-\frac{\epsilon}{k_B T}\right)\right]^6}{1 - \exp\left(-\frac{\epsilon}{k_B T}\right)} = \frac{1 - \exp\left(-\frac{6\epsilon}{k_B T}\right)}{1 - \exp\left(-\frac{\epsilon}{k_B T}\right)} $$

对于具有无限多个能级的系统，只要[能级间距](@entry_id:181168)足够大，[配分函数](@entry_id:193625)级数也可能收敛。一个典型的例子是吸附在固体表面的双原子分子，其[振动](@entry_id:267781)可以近似为一维[量子谐振子](@entry_id:140678)。其[振动能级](@entry_id:193001)为 $E_n = n\epsilon$，$n=0, 1, 2, \ldots$。[配分函数](@entry_id:193625)是一个无限几何级数 [@problem_id:2006276]：
$$ q_{vib} = \sum_{n=0}^{\infty} \exp\left(-\frac{n\epsilon}{k_B T}\right) = \sum_{n=0}^{\infty} \left[\exp\left(-\frac{\epsilon}{k_B T}\right)\right]^n $$
由于 $\epsilon > 0$ 且 $T > 0$，[公比](@entry_id:275383) $r = \exp(-\epsilon/k_B T)$ 的[绝对值](@entry_id:147688)小于1，因此该级数收敛于：
$$ q_{vib} = \frac{1}{1 - \exp\left(-\frac{\epsilon}{k_B T}\right)} $$
得到[配分函数](@entry_id:193625)后，计算特定能级的占据概率就变得很简单。例如，该分子处于[振动](@entry_id:267781)[基态](@entry_id:150928)（$n=0$, $E_0 = 0$）的概率为：
$$ P_0 = \frac{\exp(-0/k_B T)}{q_{vib}} = \frac{1}{q_{vib}} = 1 - \exp\left(-\frac{\epsilon}{k_B T}\right) = 1 - \exp(-\beta\epsilon) $$
其中我们引入了常用的简写符号 $\beta = 1/(k_B T)$。

[配分函数](@entry_id:193625)也让我们能够方便地计算不同能级上的粒子数布居比。例如，对于一个[双原子分子](@entry_id:148655)转动模型，其[转动能级](@entry_id:155495)为 $E_J = k_B \Theta_{rot} J(J+1)$，简并度为 $g_J = 2J+1$，其中 $\Theta_{rot}$ 是[特征转动温度](@entry_id:149376)。在温度 $T=\Theta_{rot}$ 时，处于第一激发[转动能级](@entry_id:155495)（$J=1$）与[基态](@entry_id:150928)（$J=0$）的分子数之比 $N_1/N_0$ 为 [@problem_id:2006279]：
$$ \frac{N_1}{N_0} = \frac{P_1}{P_0} = \frac{g_1 \exp(-E_1/k_B T)}{g_0 \exp(-E_0/k_B T)} = \frac{(2 \cdot 1 + 1)}{(2 \cdot 0 + 1)} \exp\left(-\frac{E_1 - E_0}{k_B \Theta_{rot}}\right) $$
代入 $E_1 = k_B \Theta_{rot} \cdot 1(1+1) = 2k_B \Theta_{rot}$ 和 $E_0=0$，我们得到：
$$ \frac{N_1}{N_0} = 3 \exp\left(-\frac{2k_B \Theta_{rot}}{k_B \Theta_{rot}}\right) = 3 \exp(-2) $$
这个结果表明，尽管 $J=1$ 能级能量更高，但由于其简并度更大，其布居数可能仍然相当可观。

### [配分函数](@entry_id:193625)的物理意义

[配分函数](@entry_id:193625)的数值大小本身蕴含着深刻的物理意义。粗略地讲，**[配分函数](@entry_id:193625)是系统在给定温度下有效可及的[量子态](@entry_id:146142)的数量**。

为了理解这一点，我们来比较一个氩原子在标准条件下的[平动配分函数](@entry_id:136950) $q_{trans}$ 和[电子配分函数](@entry_id:168969) $q_{elec}$ [@problem_id:2006296]。
对于一个质量为 $m$ 的粒子在体积为 $V=L^3$ 的立方盒子中的[平动](@entry_id:187700)，其[配分函数](@entry_id:193625)为：
$$ q_{trans} = V \left(\frac{2\pi m k_B T}{h^2}\right)^{3/2} $$
其中 $h$ 是普朗克常数。对于一个在边长为 $10.0\,\text{cm}$ 立方容器中，温度为 $298.15\,\text{K}$ 的氩原子，$m_{Ar} = 6.634 \times 10^{-26}\,\text{kg}$，计算可得 $q_{trans} \approx 2.44 \times 10^{29}$。这是一个巨大的数值。

另一方面，氩原子的电子基态是无简并的（$g_0=1$），我们可以将其能量设为 $\epsilon_0=0$。其第一[电子激发](@entry_id:190531)态的能量约为 $\epsilon_1 = 1.843 \times 10^{-18}\,\text{J}$。在 $T=298.15\,\text{K}$ 时，热能 $k_B T \approx 4.12 \times 10^{-21}\,\text{J}$。显然 $\epsilon_1 \gg k_B T$。其[电子配分函数](@entry_id:168969)（只考虑这两能级）为：
$$ q_{elec} = g_0 \exp\left(-\frac{\epsilon_0}{k_B T}\right) + g_1 \exp\left(-\frac{\epsilon_1}{k_B T}\right) \approx 1 \cdot \exp(0) + 1 \cdot \exp\left(-\frac{1.843 \times 10^{-18}}{4.12 \times 10^{-21}}\right) $$
$$ q_{elec} \approx 1 + \exp(-448) \approx 1 $$
[电子配分函数](@entry_id:168969)的值约等于1。

$q_{trans}$ 和 $q_{elec}$ 之间巨大的[数量级](@entry_id:264888)差异（比值为 $2.44 \times 10^{29}$）揭示了一个核心物理图像：
- **[平动能](@entry_id:170705)级**：对于宏观尺寸的容器，[平动能](@entry_id:170705)级间隔极小，远小于热能 $k_B T$。因此，在室温下，有海量的[平动](@entry_id:187700)[量子态](@entry_id:146142)是“热可及的”，系统可以轻易地占据它们。这导致了巨大的 $q_{trans}$。
- **电子能级**：电子能级之间的能量间隔通常很大，远大于室温下的 $k_B T$。因此，除了[基态](@entry_id:150928)之外，几乎所有[激发态](@entry_id:261453)都“热不可及”。系统几乎完全被“冻结”在电[子基](@entry_id:151637)态上，因此有效可及的[量子态](@entry_id:146142)数量约等于[基态](@entry_id:150928)的简并度，即 $q_{elec} \approx g_0 = 1$。

这个例子生动地说明了[配分函数](@entry_id:193625)如何量化一个系统在特定温度下的自由度或可探索的微观状态空间的大小。

### [配分函数](@entry_id:193625)与[热力学](@entry_id:141121)

[配分函数](@entry_id:193625)的真正威力在于它包含了系统的所有[热力学](@entry_id:141121)信息。通过对[配分函数](@entry_id:193625)进行数学运算，我们可以导出所有的宏观[热力学](@entry_id:141121)量。

#### 内能

系统的平均能量 $\langle E \rangle$，即[热力学](@entry_id:141121)内能 $U$，可以通过对[配分函数](@entry_id:193625) $Q$ 求导得到。回忆 $\langle E \rangle = \sum_i P_i E_i = \frac{1}{Q} \sum_i E_i \exp(-\beta E_i)$。观察到 $\frac{\partial Q}{\partial \beta} = \sum_i (-E_i) \exp(-\beta E_i) = -UQ$。因此，我们得到联系内能和[配分函数](@entry_id:193625)的第一个“桥梁方程”：

$$ U = -\frac{1}{Q}\frac{\partial Q}{\partial \beta} = -\left(\frac{\partial \ln Q}{\partial \beta}\right)_{N,V} $$

利用 $\beta = 1/(k_B T)$ 和[链式法则](@entry_id:190743)，也可以将其写成对温度 $T$ 的导数：

$$ U = k_B T^2 \left(\frac{\partial \ln Q}{\partial T}\right)_{N,V} $$

#### 压强

同样，系统的压强 $P$ 也可以从[配分函数](@entry_id:193625)中导出。这需要从[亥姆霍兹自由能](@entry_id:136442) $A$ 开始。在[热力学](@entry_id:141121)中，其[微分形式](@entry_id:146747)为 $dA = -SdT - PdV + \mu dN$。因此，压强可以表示为 $P = -(\partial A / \partial V)_{T,N}$。而在[统计力](@entry_id:194984)学中，亥姆霍兹自由能与[配分函数](@entry_id:193625)的关系是 $A = -k_B T \ln Q$。将此关系代入，我们得到压强的表达式 [@problem_id:2006284]：

$$ P = -\left(\frac{\partial (-k_B T \ln Q)}{\partial V}\right)_{T,N} = k_B T \left(\frac{\partial \ln Q}{\partial V}\right)_{T,N} $$

#### 应用示例

假设我们有一个由 $N$ 个可分辨的非相互作用粒子组成的系统，其单个粒子的[配分函数](@entry_id:193625)为 $q(V,T) = \alpha V T^{3/2}$，其中 $\alpha$ 是常数（这实际上是[理想单原子气体](@entry_id:138760)的模型）。由于粒子可分辨，[总配分函数](@entry_id:190183)为 $Q = q^N = (\alpha V T^{3/2})^N$。因此 $\ln Q = N (\ln \alpha + \ln V + \frac{3}{2} \ln T)$。

我们可以利用上述桥梁方程来计算这个系统的宏观性质 [@problem_id:2006309]：
- **内能 $U$**：
$$ U = k_B T^2 \left(\frac{\partial \ln Q}{\partial T}\right)_V = k_B T^2 \left( N \frac{\partial}{\partial T} \left(\frac{3}{2} \ln T\right) \right) = k_B T^2 \left( N \frac{3}{2T} \right) = \frac{3}{2} N k_B T $$
- **压强 $P$**：
$$ P = k_B T \left(\frac{\partial \ln Q}{\partial V}\right)_T = k_B T \left( N \frac{\partial}{\partial V} (\ln V) \right) = k_B T \left( \frac{N}{V} \right) = \frac{N k_B T}{V} $$
这个结果正是[理想气体状态方程](@entry_id:137803) $PV = N k_B T$。从这两个结果中，我们可以得到一个重要的比值：
$$ \frac{PV}{U} = \frac{N k_B T}{\frac{3}{2} N k_B T} = \frac{2}{3} $$
这个例子展示了只要知道[配分函数](@entry_id:193625)的形式，我们就可以通过纯粹的数学推导得出系统的宏观[热力学](@entry_id:141121)方程。

#### 恒容热容

恒容热容 $C_V$ 定义为 $C_V = (\partial U / \partial T)_V$。它衡量了系统在体积不变的情况下，温度每升高一度所吸收的能量。利用内能的表达式，我们可以将 $C_V$ 也与[配分函数](@entry_id:193625)联系起来。

一个重要的应用是计算晶体的[热容](@entry_id:137594)。考虑一个由 $N$ 个独立、可分辨的三维量子谐振子组成的晶体模型（爱因斯坦模型）。在高温极限下（$k_B T \gg h\nu$），每个[振子](@entry_id:271549)在每个方向（x, y, z）上的平均能量趋近于 $k_B T$（[能量均分定理](@entry_id:136972)）。因此，每个三维[振子](@entry_id:271549)的[平均能量](@entry_id:145892)为 $3k_B T$。对于一摩尔原子（$N=N_A$），总内能 $U_m = N_A (3k_B T) = 3RT$。其[摩尔热容](@entry_id:144045)为 [@problem_id:2006312]：
$$ C_{V,m} = \left(\frac{\partial U_m}{\partial T}\right)_V = \frac{\partial}{\partial T}(3RT) = 3R $$
其中 $R = N_A k_B$ 是理想气体常数。这个结果 $C_{V,m} \approx 3R$ 就是经典的**[杜隆-珀蒂定律](@entry_id:191078)**，它成功地解释了许多固体在高温下的[热容](@entry_id:137594)。[统计力](@entry_id:194984)学不仅重现了这个经典结果，还能通过完整的谐振子[配分函数](@entry_id:193625)模型解释在低温下热容如何偏离 $3R$ 并趋于零。

### 高级主题：涨落与特殊系综

[配分函数](@entry_id:193625)不仅能给出[热力学](@entry_id:141121)量的平均值，还能描述这些量的统计**涨落**。

一个处于正则系综中的系统，其温度是固定的，但其能量不是。能量会在其平均值 $\langle E \rangle$ 附近涨落。能量的[方差](@entry_id:200758) $\sigma_E^2 = \langle E^2 \rangle - \langle E \rangle^2$ 是衡量涨落大小的指标。可以证明，这个[方差](@entry_id:200758)与系统的[热容](@entry_id:137594) $C_V$ 直接相关 [@problem_id:2006321]：

$$ \sigma_E^2 = -\frac{\partial \langle E \rangle}{\partial \beta} $$

利用 $C_V = (\partial \langle E \rangle / \partial T)_V$ 和链式法则 $C_V = \frac{\partial \langle E \rangle}{\partial \beta} \frac{d\beta}{dT} = \frac{\partial \langle E \rangle}{\partial \beta} (-\frac{1}{k_B T^2})$，我们可以消去导数项，得到一个优美的关系：

$$ \sigma_E^2 = k_B T^2 C_V $$

这个公式是**涨落-耗散定理**的一个例子。它表明，一个系统对温度变化的响应（由 $C_V$ 体现）与其内部能量的自发涨落（由 $\sigma_E^2$ 体现）是内在相关的。热容越大的系统，其[能量涨落](@entry_id:148029)也越剧烈。

#### 配分[函数的收敛](@entry_id:152305)性与最高温度

[正则系综](@entry_id:142391)的整个框架都建立在[配分函数](@entry_id:193625) $Q = \sum g_j \exp(-\beta E_j)$ 是一个[收敛级数](@entry_id:147778)的前提下。对于大多数物理系统，当 $j \to \infty$ 时，$E_j \to \infty$，指数项 $\exp(-\beta E_j)$ 会迅速趋于零，确保级数收敛。

然而，在一些特殊的理论模型中，能级的简并度 $g_j$ 可能随能量增长得非常快，以至于压倒了[玻尔兹曼因子](@entry_id:141054)的指数衰减。例如，考虑一个假想系统，其能级为 $E_n = \epsilon \ln(n)$，简并度为 $g_n \sim n^k$（$k>0$）。其[配分函数](@entry_id:193625)的求和项在 $n$ 很大时表现为 [@problem_id:2006252]：
$$ g_n \exp(-\beta E_n) \sim n^k \exp(-\beta \epsilon \ln n) = n^k n^{-\beta \epsilon} = n^{-(\beta\epsilon - k)} $$
这个[级数的收敛](@entry_id:136768)性取决于幂指数。根据[p-级数](@entry_id:139707)判别法，级数 $\sum n^{-s}$ 当且仅当 $s > 1$ 时收敛。因此，该系统的[配分函数](@entry_id:193625)收敛的条件是 $\beta\epsilon - k > 1$。
当温度升高，$\beta$ 减小，$\beta\epsilon - k$ 的值也随之减小。当 $\beta\epsilon - k = 1$ 时，[配分函数](@entry_id:193625)开始发散。这个[临界点](@entry_id:144653)对应的温度被称为**Hagedorn温度** $T_H$：
$$ \beta_H = \frac{k+1}{\epsilon} \implies T_H = \frac{1}{k_B \beta_H} = \frac{\epsilon}{(k+1)k_B} $$
当系统温度接近 $T_H$ 时，其热容会发散，系统无法通过升温来吸收更多能量。这意味着对于这类系统，存在一个热力学平衡的最高温度上限。

#### [负绝对温度](@entry_id:137353)

最后，我们来探讨一个看似矛盾的概念：**[负绝对温度](@entry_id:137353)**。这并非指低于绝对[零度](@entry_id:156285)，而是一种存在于特定系统中的、比任何正温度都“更热”的状态。

[负温度](@entry_id:140023)的概念源于熵对能量的导数定义：$\frac{1}{T} = (\frac{\partial S}{\partial U})_{N,V}$。通常情况下，向系统增加能量 $U$ 会增加其熵 $S$，所以 $\frac{\partial S}{\partial U} > 0$，温度 $T$ 为正。

然而，考虑一个由 $N$ 个固定的双能级粒子组成的[孤立系统](@entry_id:159201)，能级为 $0$ 和 $\epsilon$。该系统的总能量 $U$ 有一个上限 $N\epsilon$。
- 当 $U=0$ 时，所有粒子都在[基态](@entry_id:150928)，只有一种构型，熵 $S=0$。
- 随着 $U$ 增加，粒子被激发到高能态，可以[排列](@entry_id:136432)的方式（[微观态](@entry_id:147392)数 $\Omega$）增多，熵 $S=k_B \ln \Omega$ 也随之增加。
- 当 $U=N\epsilon/2$ 时，高低能级各有 $N/2$ 个粒子，此时的构型数 $\Omega$ 达到最大值，熵也达到峰值。
- 当 $U$ 继续增加，超过 $N\epsilon/2$ 时，意味着[激发态](@entry_id:261453)的粒子数超过了[基态](@entry_id:150928)的粒子数（**布居数反转**）。此时，要容纳更多能量，就必须让更多的粒子处于[激发态](@entry_id:261453)，这反而减少了可能的构型数。例如，当 $U=N\epsilon$ 时，所有粒子都在[激发态](@entry_id:261453)，又只有一种构型，熵再次变为0。

因此，在这个系统中，当能量 $U > N\epsilon/2$ 时，熵 $S$ 随能量 $U$ 的增加而减少，即 $(\frac{\partial S}{\partial U})  0$。这直接导致了 $T  0$。

例如，对于一个由 $N=1.00 \times 10^{20}$ 个粒子组成的双能级系统，能级差 $\epsilon = 3.00 \times 10^{-21}\,\text{J}$，若其总能量为 $U = 2.25 \times 10^{-1}\,\text{J}$，我们可以计算其温度。总能量上限为 $N\epsilon = 3.00 \times 10^{-1}\,\text{J}$。由于 $U  N\epsilon/2$，我们预期一个[负温度](@entry_id:140023)。利用公式 $T = \frac{\epsilon}{k_B \ln(\frac{N\epsilon-U}{U})}$ 推导，可以算出该系统的温度约为 $-198\,\text{K}$ [@problem_id:2006253]。

[负温度](@entry_id:140023)系统是真实存在的（例如在某些核自旋系统和[激光](@entry_id:194225)介质中），它们具有[布居数反转](@entry_id:155020)和有界能谱的共同特征。一个[负温度](@entry_id:140023)系统与任何正温度系统接触时，热量会从负温系统流向正温系统，这正是它比所有正温度都“更热”的含义。这一概念深刻地揭示了温度的统计本质，远超我们日常的直观感受。