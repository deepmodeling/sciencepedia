## 引言
在[统计力](@entry_id:194984)学的研究中，我们常常从最简单的理想模型——孤立系统入手，其能量、体积和粒子数均固定不变。描述这类系统的理论框架是[微正则系综](@entry_id:141513)。然而，在现实的物理和化学实验中，我们更常遇到的情况是研究对象并非孤立，而是与一个巨大的、温度恒定的环境（即[热库](@entry_id:143608)）进行着能量交换。为了描述这类更为普遍的系统，我们需要一个新的[统计系综](@entry_id:149738)——正则系综。本文的核心主题，**[正则配分函数](@entry_id:154330)**，正是这一系综的基石。

本文旨在解决从描述孤立系统的[微正则系综](@entry_id:141513)到描述恒温系统的正则系综的理论跨越，并揭示[正则配分函数](@entry_id:154330)作为连接微观世界与宏观[热力学](@entry_id:141121)现象的强大数学工具的意义。它不仅是一个简单的[归一化常数](@entry_id:752675)，更是蕴含了系统全部[热力学](@entry_id:141121)信息的“宝库”。

在接下来的内容中，我们将分步深入探索[正则配分函数](@entry_id:154330)。在“**原理与机制**”一章中，我们将从[统计力](@entry_id:194984)学的基本假设出发，推导出著名的玻尔兹曼分布和[正则配分函数](@entry_id:154330)的定义，并建立它与亥姆霍兹自由能之间的关键联系，展示如何由此推导所有宏观[热力学性质](@entry_id:146047)。随后，在“**应用与跨学科联系**”一章中，我们将通过一系列从理想气体到[DNA解链](@entry_id:181106)的实例，展示[配分函数](@entry_id:193625)在物理、化学、生物和[材料科学](@entry_id:152226)等领域的强大解释力和预测能力。最后，“**动手实践**”部分将提供具体的计算练习，帮助你巩固和应用所学知识。

## 原理与机制

在上一章中，我们介绍了[统计力](@entry_id:194984)学的基本假设，特别是等概率原理，它构成了[微正则系综](@entry_id:141513)的理论基础。然而，在现实世界的实验中，完全孤立的系统是罕见的。更常见的情况是，我们研究的系统（例如，烧杯中的[化学反应](@entry_id:146973)、晶体中的一块磁性材料）与一个巨大的、温度恒定的环境（[热库](@entry_id:143608)）进行能量交换。这种场景由**[正则系综](@entry_id:142391) (canonical ensemble)** 来描述，其中系统的粒子数 $N$ 和体积 $V$ 固定，而温度 $T$ 由热库决定。本章将深入探讨正则系综的核心——[正则配分函数](@entry_id:154330)，揭示它如何从第一性原理出发，成为连接微观[量子态](@entry_id:146142)与宏观[热力学](@entry_id:141121)世界的关键桥梁。

### [正则系综](@entry_id:142391)与玻尔兹曼分布

想象一个我们感兴趣的小系统 $S$，它具有一组离散的[能量本征态](@entry_id:152154) $\{|i\rangle\}$，其对应的能量为 $\{E_i\}$。该系统与一个非常大的热库 $R$ 处于热接触状态。系统和[热库](@entry_id:143608)共同构成一个总能量为 $E_{\text{tot}}$ 的孤立复合系统 $S+R$。根据微正则系综的基本假设，这个复合系统的所有可及微观状态都是等概率的。

我们的目标是确定系统 $S$ 处于特定微观状态 $|i\rangle$（能量为 $E_i$）的概率 $p_i$。当系统 $S$ 处于能量为 $E_i$ 的状态时，根据[能量守恒](@entry_id:140514)，[热库](@entry_id:143608) $R$ 的能量必须是 $E_R = E_{\text{tot}} - E_i$。由于复合系统的所有微观状态都是等概率的，那么系统 $S$ 处于状态 $|i\rangle$ 的概率 $p_i$ 就正比于[热库](@entry_id:143608)在能量为 $E_R$ 时所拥有的微观状态数 $\Omega_R(E_{\text{tot}} - E_i)$。

$$
p_i \propto \Omega_R(E_{\text{tot}} - E_i)
$$

为了处理这个表达式，我们利用熵的定义 $S_R(E) = k_B \ln \Omega_R(E)$，其中 $k_B$ 是玻尔兹曼常数。因此，我们可以写出：

$$
p_i \propto \exp\left( \frac{S_R(E_{\text{tot}} - E_i)}{k_B} \right)
$$

由于热库非常大，系统 $S$ 的能量 $E_i$ 远小于总能量 $E_{\text{tot}}$ ($E_i \ll E_{\text{tot}}$)。这使得我们可以将[热库](@entry_id:143608)的熵 $S_R$ 在 $E_{\text{tot}}$ 附近进行[泰勒展开](@entry_id:145057)，并保留到一阶项：

$$
S_R(E_{\text{tot}} - E_i) \approx S_R(E_{\text{tot}}) - E_i \left( \frac{\partial S_R}{\partial E} \right)_{E=E_{\text{tot}}}
$$

根据[热力学](@entry_id:141121)定义，熵对能量的偏导数定义了[热库](@entry_id:143608)的温度 $T$：

$$
\left( \frac{\partial S_R}{\partial E} \right)_{V,N} = \frac{1}{T}
$$

将此关系代入熵的展开式，我们得到：

$$
S_R(E_{\text{tot}} - E_i) \approx S_R(E_{\text{tot}}) - \frac{E_i}{T}
$$

将这个近似结果代回概率表达式 $p_i$ 中：

$$
p_i \propto \exp\left( \frac{S_R(E_{\text{tot}})}{k_B} - \frac{E_i}{k_B T} \right) = \exp\left( \frac{S_R(E_{\text{tot}})}{k_B} \right) \exp\left( -\frac{E_i}{k_B T} \right)
$$

由于 $\exp(S_R(E_{\text{tot}})/k_B)$ 是一个不依赖于系统状态 $i$ 的常数，它可以被吸收到比例常数中。因此，我们得到了著名的**玻尔兹曼分布 (Boltzmann distribution)**：

$$
p_i \propto \exp\left( -\frac{E_i}{k_B T} \right) = \exp(-\beta E_i)
$$

这里我们引入了**[逆温](@entry_id:140086)度 (inverse temperature)** $\beta \equiv 1/(k_B T)$。这个结果是[统计力](@entry_id:194984)学的基石之一。它表明，在与恒温[热库](@entry_id:143608)接触的系统中，系统处于较高能量状态的概率会呈指数级下降。这种抑制效应源于一个深刻的物理事实：当系统占据一个高能量状态 $E_i$ 时，它从热库中“借走”了能量，导致[热库](@entry_id:143608)可用的微观状态数量呈指数级减少，从而使得这种情况发生的可能性大大降低 [@problem_id:2812033]。

值得一提的是，玻尔兹曼分布也可以通过信息论中的**[最大熵原理](@entry_id:142702) (principle of maximum entropy)** 导出。该方法寻求在满足已知约束条件（如归一化概率 $\sum p_i = 1$ 和固定的平均能量 $\langle E \rangle = \sum p_i E_i$）下，使系统的[吉布斯-香农熵](@entry_id:152991) $S = -k_B \sum p_i \ln p_i$ 最大化的[概率分布](@entry_id:146404)。这个最“无偏见”的[分布](@entry_id:182848)恰好就是玻尔兹曼分布，其中[拉格朗日乘子](@entry_id:142696) $\beta$ 通过[热力学](@entry_id:141121)关系被识别为[逆温](@entry_id:140086)度 [@problem_id:2812033]。

### [正则配分函数](@entry_id:154330)：定义与物理意义

玻尔兹曼分布给出了概率的比例关系，为了得到一个真正的[概率分布](@entry_id:146404)，我们必须对其进行归一化。所有状态的概率之和必须为1：$\sum_i p_i = 1$。归一化常数，通常用 $Z$（或 $Q$）表示，被称为**[正则配分函数](@entry_id:154330) (canonical partition function)**。

对于一个具有离散能级 $E_i$ 和简并度 $g_i$ 的系统，[配分函数](@entry_id:193625)的定义为：

$$
Z(T, V, N) = \sum_{i \text{ (levels)}} g_i \exp(-\beta E_i)
$$

等效地，如果我们对所有微观状态 $j$ 求和（不考虑简并度），则定义为：

$$
Z(T, V, N) = \sum_{j \text{ (states)}} \exp(-\beta E_j)
$$

有了[配分函数](@entry_id:193625)，任何特定状态 $i$ 的概率就可以精确地写为：

$$
p_i = \frac{g_i \exp(-\beta E_i)}{Z}
$$

让我们通过一个简单的例子来理解如何计算[配分函数](@entry_id:193625)。考虑一个被限制在[晶格缺陷](@entry_id:270099)处的电子，它只能处于三个非简并的能级：基态能量为 $E_0=0$，第一[激发态](@entry_id:261453)能量为 $E_1=\epsilon$，第二[激发态](@entry_id:261453)能量为 $E_2=3\epsilon$ [@problem_id:1996272]。该系统的[配分函数](@entry_id:193625)就是三个[玻尔兹曼因子](@entry_id:141054)的和：

$$
Z = \exp(-\beta \cdot 0) + \exp(-\beta \epsilon) + \exp(-\beta \cdot 3\epsilon) = 1 + \exp(-\beta \epsilon) + \exp(-3\beta \epsilon)
$$

如果能级存在简并，我们也必须将其考虑在内。例如，一个系统基态能量为0（非简并），而能量为 $\epsilon$ 的第一[激发态](@entry_id:261453)是三重简并的 [@problem_id:2008459]。其单粒子[配分函数](@entry_id:193625)为：

$$
z = 1 \cdot \exp(-\beta \cdot 0) + 3 \cdot \exp(-\beta \epsilon) = 1 + 3\exp(-\beta \epsilon)
$$

[配分函数](@entry_id:193625)的物理意义远不止是一个[归一化常数](@entry_id:752675)。它实际上是对系统在给定温度下“[热力学](@entry_id:141121)可及”的状态总数的有效度量。
- 在**低温极限** ($T \to 0$, $\beta \to \infty$)，指数项 $\exp(-\beta E_i)$ 对于所有 $E_i > E_0$（[基态能量](@entry_id:263704)）的能级都趋近于零。因此，$Z \approx g_0 \exp(-\beta E_0)$，[配分函数](@entry_id:193625)主要由[基态](@entry_id:150928)贡献。系统几乎肯定处于其[基态](@entry_id:150928)。
- 在**高温极限** ($T \to \infty$, $\beta \to 0$)，所有指数项 $\exp(-\beta E_i)$ 都趋近于1。因此，$Z \approx \sum_i g_i$，即系统所有可能状态的总数。此时，所有状态都变得几乎等概率可及。

### 通往[热力学](@entry_id:141121)之桥：亥姆霍兹自由能

[配分函数](@entry_id:193625)的真正威力在于它与宏观[热力学](@entry_id:141121)量之间的深刻联系。这个联系是通过**亥姆霍兹自由能 (Helmholtz free energy)** $F$ 建立的，其自然变量恰好是正则系综中固定的参数 $(T, V, N)$ [@problem_id:1981245]。它们之间的核心关系是：

$$
F(T, V, N) = -k_B T \ln Z(T, V, N)
$$

这个方程是[统计力](@entry_id:194984)学中最重要和最有用的关系之一，它构成了从微观世界（由 $Z$ 描述的[量子态](@entry_id:146142)总和）到宏观世界（由热力学势 $F$ 描述）的桥梁。我们可以从第一性原理严格推导出这个关系 [@problem_id:2824955]。

我们从[吉布斯-香农熵](@entry_id:152991)公式 $S = -k_B \sum_i p_i \ln p_i$ 开始。将正则[分布](@entry_id:182848)的概率 $p_i = \exp(-\beta E_i) / Z$ 代入：

$$
\ln p_i = -\beta E_i - \ln Z
$$

$$
S = -k_B \sum_i p_i (-\beta E_i - \ln Z) = k_B \beta \sum_i p_i E_i + k_B \ln Z \sum_i p_i
$$

我们识别出两个关键部分：$\sum_i p_i E_i$ 是系统的[平均能量](@entry_id:145892)，即内能 $U$；而 $\sum_i p_i = 1$ 是概率的[归一化条件](@entry_id:156486)。代入 $\beta = 1/(k_B T)$，我们得到：

$$
S = k_B \frac{1}{k_B T} U + k_B \ln Z = \frac{U}{T} + k_B \ln Z
$$

整理这个方程，我们得到 $U - TS = -k_B T \ln Z$。根据[热力学](@entry_id:141121)定义， $F \equiv U - TS$，因此我们证明了 $F = -k_B T \ln Z$ [@problem_id:488938]。这个推导仅依赖于[统计力](@entry_id:194984)学的基本定义，无需对系统的[能谱](@entry_id:181780)做任何额外假设。

### 从[配分函数](@entry_id:193625)推导所有[热力学性质](@entry_id:146047)

一旦我们通过计算 $Z$ 得到了[亥姆霍兹自由能](@entry_id:136442) $F$，我们就可以通过标准的偏导数关系，像打开一个宝库一样，提取出系统的所有宏观热力学性质。

- **内能 $U$**: 内能是系统能量的系综平均值 $\langle E \rangle$。
  $$
  U = \langle E \rangle = \sum_i E_i p_i = \frac{1}{Z} \sum_i E_i g_i \exp(-\beta E_i)
  $$
  我们可以通过对 $\ln Z$ 求导得到一个更紧凑的表达式。注意到 $\partial(\exp(-\beta E_i)) / \partial \beta = -E_i \exp(-\beta E_i)$，我们有：
  $$
  U = -\frac{1}{Z} \frac{\partial}{\partial \beta} \sum_i g_i \exp(-\beta E_i) = -\frac{1}{Z} \frac{\partial Z}{\partial \beta} = -\left( \frac{\partial \ln Z}{\partial \beta} \right)_{V,N}
  $$
  这个公式非常有用，但需要注意的是，它隐含了一个假设，即能级 $E_i$ 本身不依赖于温度 $T$（或 $\beta$）。如果能级由于某种原因依赖于温度，这个公式就需要修正 [@problem_id:2824955]。

- **熵 $S$**: 从[热力学](@entry_id:141121)关系 $S = -(\partial F / \partial T)_{V,N}$ 和 $F = -k_B T \ln Z$ 出发：
  $$
  S = -\frac{\partial}{\partial T} (-k_B T \ln Z) = k_B \ln Z + k_B T \left( \frac{\partial \ln Z}{\partial T} \right)_{V,N}
  $$
  利用链式法则 $\partial/\partial T = (\partial \beta / \partial T) (\partial/\partial \beta) = -(1/k_B T^2)(\partial/\partial \beta)$ 和上面 $U$ 的表达式，我们可以将第二项改写为 $k_B T (U/(k_B T^2)) = U/T$。因此，我们重新得到了之[前推](@entry_id:158718)导出的关系：
  $$
  S = k_B \ln Z + \frac{U}{T}
  $$

- **压强 $p$**: 压强可以通过 $p = -(\partial F / \partial V)_{T,N}$ 得到：
  $$
  p = k_B T \left( \frac{\partial \ln Z}{\partial V} \right)_{T,N}
  $$

- **[定容热容](@entry_id:147536) $C_V$**: [热容](@entry_id:137594)是内能随温度的变化率，$C_V = (\partial U / \partial T)_V$。利用链式法则，我们可以将其与能量的涨落联系起来：
  $$
  C_V = \left( \frac{\partial U}{\partial T} \right)_V = \frac{\partial U}{\partial \beta} \frac{\partial \beta}{\partial T} = \left( \frac{\partial}{\partial \beta} \left( -\frac{\partial \ln Z}{\partial \beta} \right) \right) \left( -\frac{1}{k_B T^2} \right) = \frac{1}{k_B T^2} \left( \frac{\partial^2 \ln Z}{\partial \beta^2} \right)
  $$
  我们注意到，能量的[方差](@entry_id:200758)（或涨落的平方）$\langle (\Delta E)^2 \rangle = \langle E^2 \rangle - \langle E \rangle^2$ 也等于 $(\partial^2 \ln Z / \partial \beta^2)$。因此，我们得到了一个深刻的关系：
  $$
  C_V = \frac{\langle (\Delta E)^2 \rangle}{k_B T^2}
  $$
  这表明，系统的热容直接与它在给定温度下能量的涨落幅度成正比。一个系统的热容越大，意味着它在吸收能量时，能量更多地[分布](@entry_id:182848)在内部的涨落中，而不是直接提升整体温度。在低温极限下，系统被“冻结”在[基态](@entry_id:150928)附近，[能量涨落](@entry_id:148029)很小，因此热容趋于零 [@problem_id:2008484]。

- **[能量涨落](@entry_id:148029)**: 对于一个宏观系统，尽管其能量在与热库的交换中不断涨落，但这些涨落相对于[平均能量](@entry_id:145892)来说是极其微小的。例如，对于一个包含 $N$ 个粒子的单原子[理想气体](@entry_id:200096)，可以严格证明其[平均能量](@entry_id:145892) $\langle E \rangle = \frac{3}{2} N k_B T$，而其[能量涨落](@entry_id:148029)的[标准差](@entry_id:153618) $\sqrt{\langle (\Delta E)^2 \rangle} = \sqrt{\frac{3}{2} N} k_B T$。因此，相对涨落的大小为 [@problem_id:2671908]：
  $$
  \frac{\sqrt{\langle (\Delta E)^2 \rangle}}{\langle E \rangle} = \frac{\sqrt{\frac{3}{2} N} k_B T}{\frac{3}{2} N k_B T} = \sqrt{\frac{2}{3N}} \propto \frac{1}{\sqrt{N}}
  $$
  当 $N$ 是宏观[数量级](@entry_id:264888)（例如[阿伏伽德罗常数](@entry_id:141949) $\sim 10^{23}$）时，相对涨落小到完全可以忽略不计。这解释了为什么在宏观尺度上，[正则系综](@entry_id:142391)的能量可以被认为是一个确定值，从而与微正则系综的描述在[热力学极限](@entry_id:143061)下是等价的。

### [多粒子系统](@entry_id:192694)

到目前为止，我们的讨论大多集中在单个粒子或单个系统上。将这些概念推广到由大量粒子组成的系统时，我们需要考虑粒子间的相互作用和它们的**可区分性 (distinguishability)**。

#### 可分离[哈密顿量](@entry_id:172864)
在许多情况下，一个复杂系统的总[哈密顿量](@entry_id:172864)可以写成几个互不相关的部分之和。例如，一个分子的总能量可以近似地看作是[平动能](@entry_id:170705)、[转动能和振动能](@entry_id:143118)的和：$\hat{H} = \hat{H}_{\text{trans}} + \hat{H}_{\text{rot}} + \hat{H}_{\text{vib}}$。如果这些[哈密顿量](@entry_id:172864)算符是相互对易的，那么总系统的[配分函数](@entry_id:193625)就可以分解为各子系统[配分函数](@entry_id:193625)的乘积 [@problem_id:2824955]：
$$
Z = \text{Tr}(e^{-\beta(\hat{H}_{\text{trans}} + \hat{H}_{\text{rot}} + \hat{H}_{\text{vib}})}) = \text{Tr}(e^{-\beta\hat{H}_{\text{trans}}} e^{-\beta\hat{H}_{\text{rot}}} e^{-\beta\hat{H}_{\text{vib}}}) = Z_{\text{trans}} Z_{\text{rot}} Z_{\text{vib}}
$$
由于 $F = -k_B T \ln Z$，[配分函数](@entry_id:193625)的乘积形式意味着亥姆霍兹自由能是可加的：
$$
F = F_{\text{trans}} + F_{\text{rot}} + F_{\text{vib}}
$$
这种分解极大地简化了对复杂分子系统的计算。

#### 可区分与不可区分粒子
考虑一个由 $N$ 个无相互作用的粒子组成的系统。
- 如果粒子是**可区分的 (distinguishable)**，例如固定在[晶格](@entry_id:196752)不同位置上的原子，那么每个粒子都可以独立地处于任何单粒子能态。系统的[总配分函数](@entry_id:190183)就是单个粒子[配分函数](@entry_id:193625) $z$ 的 $N$ 次方 [@problem_id:2008512]：
  $$
  Z_N^{(\text{dist})} = z^N
  $$

- 如果粒子是**不可区分的 (indistinguishable)**，例如气体中的同种分子，情况就变得复杂了。交换任意两个粒子的位置不会产生一个新的物理微观状态。如果我们仍然使用 $z^N$ 作为[配分函数](@entry_id:193625)，就会严重高估状态的数量。

在高温、低密度的经典极限（即[麦克斯韦-玻尔兹曼统计](@entry_id:746908)），我们可以用一个简单的修正因子来处理这个问题。由于有 $N!$ 种方式可以[排列](@entry_id:136432) $N$ 个粒子，我们将可区分粒子的[配分函数](@entry_id:193625)除以 $N!$ 来修正这种重复计数 [@problem_id:2008512]：
$$
Z_N^{(\text{indist})} \approx \frac{z^N}{N!}
$$
必须强调，这是一个近似。在低温或高密度下，量子效应变得显著，必须使用[费米-狄拉克统计](@entry_id:140706)或[玻色-爱因斯坦统计](@entry_id:139965)来进行更精确的计算 [@problem_id:2824955]。

#### [吉布斯佯谬](@entry_id:141027)与 $1/N!$ 因子的必要性
这个 $1/N!$ 因子不仅仅是一个数学修正，它具有深刻的物理后果，其必要性可以通过著名的**[吉布斯佯谬](@entry_id:141027) (Gibbs paradox)** 来阐明 [@problem_id:2671881]。

想象一个容器，中间用隔板分成两半，两边都装有相同温度、压强和体积的同种理想气体（每边有 $N$ 个粒子）。如果我们移除隔板，直觉告诉我们，由于两边的气体是完全相同的，系统的宏观状态没有改变，因此熵应该不变。

然而，如果我们使用可区分粒子的[配分函数](@entry_id:193625) $Z_N^{(\text{dist})} = z^N$ 来计算熵，我们会发现混合过程导致了熵增加 $\Delta S = 2N k_B \ln 2$。这个非零的“[混合熵](@entry_id:161398)”是荒谬的，因为它意味着仅仅移除一个想象中的隔板就能自发地创造熵。

这个佯谬的根源在于将[全同粒子](@entry_id:142755)错误地当作可区分的。如果我们引入 $1/N!$ 因子，计算得到的亥姆霍兹自由能 $F$ 和熵 $S$ 将是**广延量 (extensive quantities)**。广延量意味着当系统大小（$N$ 和 $V$）加倍时，该物理量也加倍。使用修正后的[配分函数](@entry_id:193625) $Z_N^{(\text{indist})} = z^N/N!$ 计算得到的熵（即[萨克-特特罗德方程](@entry_id:139525)）是广延的，此时移除隔板导致的[熵变](@entry_id:138294)为零，佯谬得以解决 [@problem_id:2671881]。$1/N!$ 因子确保了化学势 $\mu = (\partial F / \partial N)_{T,V}$ 的正确形式，从而消除了混合相同气体的虚假[热力学](@entry_id:141121)驱动力 [@problem_id:2671881]。

#### 经典极限与相空间
最后，值得一提的是[正则配分函数](@entry_id:154330)在经典力学中的对应形式。对于一个由 $N$ 个[不可区分粒子](@entry_id:142755)组成的经典系统，其[哈密顿量](@entry_id:172864)为 $H(\mathbf{p}, \mathbf{q})$，[配分函数](@entry_id:193625)由对相[空间的积](@entry_id:151742)分给出：
$$
Z = \frac{1}{N! h^{3N}} \int d^{3N}\mathbf{p} \, d^{3N}\mathbf{q} \, \exp(-\beta H(\mathbf{p}, \mathbf{q}))
$$
这个表达式中包含了两个重要的修正因子：
1.  $1/N!$：我们刚刚讨论过的，用于修正不可区分粒子的重复计数。
2.  $1/h^{3N}$：其中 $h$ 是普朗克常数。这个因子源于量子力学的[不确定性原理](@entry_id:141278)，它将连续的[经典相空间](@entry_id:195767)划分为一个个体积为 $h^{3N}$ 的“量子单元”。引入这个因子不仅解决了量纲问题（[配分函数](@entry_id:193625)本身必须是无量纲的），也深刻地揭示了经典[统计力](@entry_id:194984)学本质上是[量子统计力学](@entry_id:140244)在高温极限下的近似 [@problem_id:2824955]。

综上所述，[正则配分函数](@entry_id:154330) $Z$ 是一个极其强大的理论工具。它不仅通过玻尔兹曼因子编码了系统微观能级的[分布](@entry_id:182848)信息，更通过与亥姆霍兹自由能的简单关系，为我们提供了一条从微观量子世界通往宏观[热力学](@entry_id:141121)世界的康庄大道。掌握[配分函数](@entry_id:193625)的计算和应用，是理解和预测物质[热力学性质](@entry_id:146047)的关键所在。