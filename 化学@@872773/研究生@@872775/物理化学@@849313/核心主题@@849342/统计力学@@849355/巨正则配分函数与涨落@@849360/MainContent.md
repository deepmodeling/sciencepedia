## 引言
在[统计力](@entry_id:194984)学中，我们描述物理系统行为的能力取决于我们选择的[统计系综](@entry_id:149738)，而这又由系统与其环境的相互作用方式决定。对于与外界隔绝或仅[交换能](@entry_id:137069)量的[封闭系统](@entry_id:139565)，孤立系综和正则系综提供了有效的理论工具。然而，自然界和实验室中的许多系统——从催化剂表面的分子吸附到细胞内的离子平衡——本质上是开放的，它们能与周围环境自由地[交换能](@entry_id:137069)量和物质。那么，我们如何为这些粒子数不恒定的系统建立一个严格的统计描述？更重要的是，系统粒子数的自发涨落本身是否蕴含着关于系统内在性质的深刻信息？

本文旨在系统地回答这些问题，核心工具是**[巨正则系综](@entry_id:141562)**。这是一个为恒定温度（T）、体积（V）和化学势（μ）下的[开放系统](@entry_id:147845)量身定制的强大理论框架。通过学习本文，读者将能够穿过微观细节的迷雾，掌握连接微观涨落与[宏观可观测量](@entry_id:751601)（如压强和[压缩系数](@entry_id:272630)）的普适规律。

文章将分为三个核心部分展开：
- 在 **原理和机制** 一章中，我们将从[统计力](@entry_id:194984)学第一性原理出发，推导[巨正则分布](@entry_id:151114)和[巨配分函数](@entry_id:154455)，并建立其与核心热力学势——[巨势](@entry_id:136286)的联系。您将学习到[粒子数涨落](@entry_id:151853)如何与[热力学](@entry_id:141121)[响应函数](@entry_id:142629)定量地关联起来。
- 接着，在 **应用与[交叉](@entry_id:147634)学科联系** 一章中，我们将展示该理论的强大解释力，探讨其如何应用于[表面吸附](@entry_id:268937)、[液态理论](@entry_id:182111)、[相变](@entry_id:147324)临界现象乃至[量子气体](@entry_id:162017)等横跨[物理化学](@entry_id:145220)、凝聚态物理和生物物理的多个前沿领域。
- 最后，在 **动手实践** 部分，我们提供了一系列精心设计的问题，旨在引导您将理论知识应用于具体计算，从而加深对[巨正则系综](@entry_id:141562)及其涨落理论的理解。

让我们首先进入第一章，深入探索[巨正则系综](@entry_id:141562)的基本原理和内在机制。

## 原理和机制

在对系统进行统计描述时，我们选择的系综取决于系统与其环境的相互作用方式。[正则系综](@entry_id:142391)适用于与恒温热库[交换能](@entry_id:137069)量但粒子数固定的[封闭系统](@entry_id:139565)。然而，在化学和[材料科学](@entry_id:152226)的许多场景中，我们感兴趣的系统是开放的——它不仅可以与周围的巨大“库”[交换能](@entry_id:137069)量，还可以交换粒子。例如，气体分子在催化剂表面的吸附、溶液中溶质与溶剂的相互作用，或者仅仅是宏观流体中我们人为划定的一小块区域。对于这些系统，温度 $T$ 和体积 $V$ 仍是良好定义的控制变量，但粒子数 $N$ 会发生涨落。取而代之的[控制变量](@entry_id:137239)是化学势 $\mu$，它由粒子库设定。描述此类系统的[统计力](@entry_id:194984)学框架便是[巨正则系综](@entry_id:141562)（Grand Canonical Ensemble, GCE）。

### [巨正则系综](@entry_id:141562)：开放系统的统计描述

为了给处于固定温度 $T$、体积 $V$ 和化学势 $\mu$ 的系统建立统计描述，我们考虑一个与巨大[热库](@entry_id:143608)和粒子库接触的小系统。这个小系统和库共同构成一个孤立的复合系统，其总能量 $E_{\text{tot}}$ 和总粒子数 $N_{\text{tot}}$ 是守恒的。根据[统计力](@entry_id:194984)学的基本假设，这个孤立的复合系统处于任何一个可及微观状态的概率是相等的。

我们的目标是找到小系统处于某个特定微观状态 $i$（具有能量 $E_i$ 和粒子数 $N_i$）的概率 $P_i$。这个概率正比于当小系统处于状态 $i$ 时，库所能占据的微观状态数 $\Omega_{\text{r}}(E_{\text{r}}, N_{\text{r}})$。由于能量和粒子数守恒，库的能量为 $E_{\text{r}} = E_{\text{tot}} - E_i$，粒子数为 $N_{\text{r}} = N_{\text{tot}} - N_i$。因此，
$$
P_i \propto \Omega_{\text{r}}(E_{\text{tot}} - E_i, N_{\text{tot}} - N_i)
$$
利用[玻尔兹曼熵公式](@entry_id:136916) $S = k_{\mathrm{B}} \ln \Omega$，其中 $k_{\mathrm{B}}$ 是玻尔兹曼常数，我们可以用库的熵 $S_{\text{r}}$ 来表示这个概率：
$$
P_i \propto \exp\left( \frac{S_{\text{r}}(E_{\text{tot}} - E_i, N_{\text{tot}} - N_i)}{k_{\mathrm{B}}} \right)
$$
由于库远大于小系统，我们有 $E_i \ll E_{\text{tot}}$ 和 $N_i \ll N_{\text{tot}}$。因此，我们可以将库的熵 $S_{\text{r}}$ 在 $E_{\text{tot}}$ 和 $N_{\text{tot}}$ 附近进行泰勒展开：
$$
S_{\text{r}}(E_{\text{tot}} - E_i, N_{\text{tot}} - N_i) \approx S_{\text{r}}(E_{\text{tot}}, N_{\text{tot}}) - E_i \left(\frac{\partial S_{\text{r}}}{\partial E_{\text{r}}}\right)_{N_{\text{r}},V_{\text{r}}} - N_i \left(\frac{\partial S_{\text{r}}}{\partial N_{\text{r}}}\right)_{E_{\text{r}},V_{\text{r}}}
$$
根据[热力学基本关系](@entry_id:144320) $dS = \frac{1}{T}dE + \frac{p}{T}dV - \frac{\mu}{T}dN$，我们识别出[偏导数](@entry_id:146280)：$(\partial S_{\text{r}}/\partial E_{\text{r}}) = 1/T$ 和 $(\partial S_{\text{r}}/\partial N_{\text{r}}) = -\mu/T$。将它们代入，得到：
$$
S_{\text{r}}(E_{\text{tot}} - E_i, N_{\text{tot}} - N_i) \approx S_{\text{r}}(E_{\text{tot}}, N_{\text{tot}}) - \frac{E_i}{T} + \frac{\mu N_i}{T}
$$
代入概率表达式中，常数项 $S_{\text{r}}(E_{\text{tot}}, N_{\text{tot}})$ 可以被吸收到归一化常数里。定义[逆温](@entry_id:140086)度 $\beta \equiv 1/(k_{\mathrm{B}} T)$，我们得到小系统处于微观状态 $i$ 的概率：
$$
P_i \propto \exp[-\beta(E_i - \mu N_i)]
$$
这个表达式是[巨正则分布](@entry_id:151114)的核心，它表明在高化学势和低能量的状态下，系统出现的概率更高。

为了将这个比例关系转化为等式，我们需要对所有可能的状态求和，得到归一化因子。这个因子被称为**[巨配分函数](@entry_id:154455) (grand canonical partition function)**，记作 $\Xi$：
$$
\Xi(T, V, \mu) = \sum_i \exp[-\beta(E_i - \mu N_i)]
$$
其中，求和遍历所有可能的粒子数 $N$ 以及每个 $N$ 对应的所有能量本征态。有了[巨配分函数](@entry_id:154455)，任意微观状态 $i$ 的概率就可以精确地写为：
$$
P_i = \frac{1}{\Xi} \exp[-\beta(E_i - \mu N_i)]
$$
这个框架与[正则系综](@entry_id:142391)形成对比，在[正则系综](@entry_id:142391)中，粒子数 $N$ 是固定的，微观状态的权重仅由能量决定，即 $\exp(-\beta E)$。 [@problem_id:2675545]

### [巨势](@entry_id:136286)及其[热力学](@entry_id:141121)意义

每个[统计系综](@entry_id:149738)都对应一个特征热力学势，该势在系综的[控制变量](@entry_id:137239)下达到极值。对于在恒定 $T$, $V$, $\mu$ 下的[巨正则系综](@entry_id:141562)，这个[热力学势](@entry_id:140516)是**[巨势](@entry_id:136286) (grand potential)**，记为 $\Omega$。

通过最大化总熵的原理可以推断，系统[达到平衡](@entry_id:170346)的条件等价于最小化系统的某个函数。这个函数正是[巨势](@entry_id:136286) $\Omega$，其定义为内能 $U$ 的[勒让德变换](@entry_id:146727)：
$$
\Omega \equiv U - TS - \mu N
$$
其[微分形式](@entry_id:146747)为 $d\Omega = -S dT - p dV - N d\mu$，这表明 $\Omega$ 的自然变量确实是 $(T, V, \mu)$。在这些变量固定的条件下，平衡态对应于 $d\Omega=0$，即 $\Omega$ 达到最小值。 [@problem_id:2675525]

[巨势](@entry_id:136286)与[巨配分函数](@entry_id:154455)的联系是[统计力](@entry_id:194984)学和[热力学](@entry_id:141121)之间的桥梁。通过计算系统的平均熵 $S = -k_{\mathrm{B}} \sum_i P_i \ln P_i$，可以推导出这个至关重要的关系：
$$
\Omega(T, V, \mu) = -k_{\mathrm{B}}T \ln \Xi(T, V, \mu)
$$
这个方程使得我们可以从微观状态的求和（计算 $\Xi$）直接得到一个宏观[热力学](@entry_id:141121)量（$\Omega$）。

此外，对于一个宏观均匀系统，根据[欧拉定理](@entry_id:138104)，内能 $U$ 是其广延变量 $S, V, N$ 的一次齐次函数，满足 $U = TS - pV + \mu N$。将此关系代入 $\Omega$ 的定义，我们得到一个非常实用的结果：
$$
\Omega = (TS - pV + \mu N) - TS - \mu N = -pV
$$
结合上面两个关于 $\Omega$ 的方程，我们得到 $pV = k_{\mathrm{B}}T \ln \Xi$。这直接将压强这个宏观可测量与微观的[配分函数](@entry_id:193625)联系起来。需要注意的是，[吉布斯自由能](@entry_id:146774) $G$ 和亥姆霍兹自由能 $F$ 与[巨势](@entry_id:136286) $\Omega$ 的关系可以通过[勒让德变换](@entry_id:146727)联系起来，在平衡时 $\Omega = F - \mu N$。 [@problem_id:2675504] 这意味着对于给定的 $\mu$，系统会选择一个粒子数 $N$ 来最小化 $F - \mu N$ 这一组合。

### 系综的联系与粒子不可分辨性

[巨配分函数](@entry_id:154455)的计算可以进一步分解。我们可以先按粒子数 $N$ 分类，然后对每个给定的 $N$ 求和。定义**[逸度](@entry_id:136534) (fugacity)** $z = \exp(\beta\mu)$，[巨配分函数](@entry_id:154455)可以重写为：
$$
\Xi(T, V, \mu) = \sum_{N=0}^{\infty} e^{\beta\mu N} \left( \sum_{j(N)} e^{-\beta E_{N,j}} \right) = \sum_{N=0}^{\infty} z^N Q_N(T, V)
$$
括号中的项正是具有 $N$ 个粒子的系统的**[正则配分函数](@entry_id:154330) (canonical partition function)** $Q_N(T,V)$。这个表达式优雅地表明，[巨配分函数](@entry_id:154455)是[正则配分函数](@entry_id:154330)以[逸度](@entry_id:136534)为变量的生成函数。 [@problem_id:2675539]

在计算 $Q_N$ 时，一个至关重要的物理原理必须被考虑：**全同粒子的不可分辨性 (indistinguishability)**。
*   在完全的量子力学处理中，系统的[波函数](@entry_id:147440)必须根据粒子是[玻色子](@entry_id:138266)（对称）还是[费米子](@entry_id:146235)（反对称）进行（反）对称化。这种对称性要求已经内在地解决了粒子不可分辨性问题，因此 $Q_N$ 是对这些合法的[量子态](@entry_id:146142)的直接求和，无需额外因子。 [@problem_id:2675539]
*   在经典[统计力](@entry_id:194984)学中，情况则更为微妙。如果我们天真地将 $N$ 个粒子的相空间体积积分，就好像它们是可区分的一样，我们会得到 $Q_N^{\text{dist}} = [Q_1(T,V)]^N$（对于无相互作用的粒子）。然而，交换任意两个粒子的标签并不会产生一个新的物理状态。对于 $N$ 个粒子，存在 $N!$ 种[排列](@entry_id:136432)。为了纠正这种重复计数，我们必须引入**[吉布斯因子](@entry_id:148667) (Gibbs factor)** $1/N!$。因此，对于经典系统，正确的[正则配分函数](@entry_id:154330)是：
$$
Q_N(T,V) = \frac{1}{N!} [Q_1(T,V)]^N
$$
这个修正至关重要。如果忽略 $1/N!$ 因子，计算出的熵将不具有[广延性](@entry_id:144932)，这会导致著名的**[吉布斯佯谬](@entry_id:141027)**：混合两种完全相同的气体时，会得出[熵增](@entry_id:138799)加的荒谬结论。在[巨正则系综](@entry_id:141562)的框架下，包含 $1/N!$ 因子能确保[巨势](@entry_id:136286) $\Omega$ 是体积 $V$ 的广延量，并且压强 $p$ 是一个不依赖于系统大小的内涵量。 [@problem_id:2675541]

#### 实例：[经典理想气体](@entry_id:156161)

让我们用[经典理想气体](@entry_id:156161)来验证整个理论框架的[自洽性](@entry_id:160889)。对于单个粒子，其[正则配分函数](@entry_id:154330)为 $Q_1(T,V) = V/\Lambda^3$，其中 $\Lambda = h/\sqrt{2\pi m k_{\mathrm{B}} T}$ 是[热德布罗意波长](@entry_id:143992)。包含不可分辨性修正后，$N$ 个理想气体分子的[正则配分函数](@entry_id:154330)为 $Q_N = \frac{1}{N!} (V/\Lambda^3)^N$。

将其代入[巨配分函数](@entry_id:154455)的定义中：
$$
\Xi(T,V,\mu) = \sum_{N=0}^{\infty} z^N \frac{1}{N!} \left(\frac{V}{\Lambda^3}\right)^N = \sum_{N=0}^{\infty} \frac{1}{N!} \left(\frac{zV}{\Lambda^3}\right)^N
$$
我们立刻认出这是[指数函数](@entry_id:161417)的泰勒级数展开，因此：
$$
\Xi(T,V,\mu) = \exp\left(\frac{zV}{\Lambda^3}\right) = \exp\left[ \frac{V}{\Lambda^3} \exp(\beta\mu) \right]
$$
现在，我们可以利用 $\Omega = -pV$ 和 $\Omega = -k_{\mathrm{B}} T \ln \Xi$ 来计算压强：
$$
pV = k_{\mathrm{B}} T \ln \Xi = k_{\mathrm{B}} T \left( \frac{zV}{\Lambda^3} \right)
$$
为了得到我们熟悉的状态方程，我们需要将上式与[平均粒子数](@entry_id:151202) $\langle N \rangle$ 联系起来。[平均粒子数](@entry_id:151202)可以通过对 $\ln \Xi$ 求导得到：
$$
\langle N \rangle = z \left( \frac{\partial \ln \Xi}{\partial z} \right)_{T,V} = z \left( \frac{V}{\Lambda^3} \right)
$$
将此结果代入压强表达式，我们得到 $pV = k_{\mathrm{B}} T \langle N \rangle$，这正是[理想气体状态方程](@entry_id:137803)。这个推导完美地展示了[巨正则系综](@entry_id:141562)如何从微观第一性原理出发，正确地再现了宏观[热力学定律](@entry_id:202285)。 [@problem_id:2675482]

### 涨落与宏观响应

[巨正则系综](@entry_id:141562)的一个强大之处在于它能自然地描述和量化物理量的涨落，特别是粒子数的涨落。由于系统是开放的，粒子数 $N$ 不再是一个固定参数，而是一个会围绕其平均值 $\langle N \rangle$ 波动的[随机变量](@entry_id:195330)。

从[巨配分函数](@entry_id:154455)出发，我们可以导出计算[粒子数涨落](@entry_id:151853)的关键公式。[平均粒子数](@entry_id:151202) $\langle N \rangle$ 是对 $\ln \Xi$ 的[一阶导数](@entry_id:749425)：
$$
\langle N \rangle = \frac{1}{\beta} \left( \frac{\partial \ln \Xi}{\partial \mu} \right)_{T,V} = - \left( \frac{\partial \Omega}{\partial \mu} \right)_{T,V}
$$
粒子数的[方差](@entry_id:200758) $\text{Var}(N) = \langle (\Delta N)^2 \rangle = \langle N^2 \rangle - \langle N \rangle^2$ 则与[二阶导数](@entry_id:144508)有关。通过简单的代数运算可以证明：
$$
\langle (\Delta N)^2 \rangle = \frac{1}{\beta^2} \left( \frac{\partial^2 \ln \Xi}{\partial \mu^2} \right)_{T,V} = k_{\mathrm{B}} T \left( \frac{\partial \langle N \rangle}{\partial \mu} \right)_{T,V} = -k_{\mathrm{B}} T \left( \frac{\partial^2 \Omega}{\partial \mu^2} \right)_{T,V}
$$
这个关系是一个深刻的**涨落-耗散定理 (fluctuation-dissipation theorem)** 的实例。 [@problem_id:2675545] [@problem_id:2675525] 它表明，系统在平衡态自发产生的[粒子数涨落](@entry_id:151853)（左侧），正比于系统对外界化学势变化的响应（即 $\partial \langle N \rangle / \partial \mu$，右侧）。一个对化学势变化非常敏感的系统，其[粒子数涨落](@entry_id:151853)也必然剧烈。

#### 涨落与等温[压缩系数](@entry_id:272630)

涨落理论最引人注目的成果之一，是它将微观涨落与宏观可测量的[材料性质](@entry_id:146723)联系起来。考虑一个宏观流体中的一小块体积为 $v$ 的区域。这个小区域可以被看作一个处于[巨正则系综](@entry_id:141562)的系统，其周围的流体充当着热库和粒子库。我们想要计算这个小区域内的[粒子数涨落](@entry_id:151853) $\langle (\Delta N_v)^2 \rangle$。

根据上面的涨落公式，我们有：
$$
\langle (\Delta N_v)^2 \rangle = k_{\mathrm{B}} T \left( \frac{\partial \langle N_v \rangle}{\partial \mu} \right)_{T,v}
$$
由于这个小区域是宏观均匀流体的一部分，其[平均粒子数](@entry_id:151202) $\langle N_v \rangle$ 等于宏观密度 $\rho$ 乘以其体积 $v$，即 $\langle N_v \rangle = \rho v$。代入上式，得到：
$$
\langle (\Delta N_v)^2 \rangle = k_{\mathrm{B}} T v \left( \frac{\partial \rho}{\partial \mu} \right)_T
$$
为了将此式与更熟悉的物理量联系起来，我们需要利用[热力学恒等式](@entry_id:142524)。[吉布斯-杜亥姆方程](@entry_id:139274)在恒温下为 $V dp = N d\mu$，或者 $(\partial p / \partial \mu)_T = N/V = \rho$。利用[链式法则](@entry_id:190743)，我们可以将对 $\mu$ 的求导转为对 $p$ 的求导：
$$
\left( \frac{\partial \rho}{\partial \mu} \right)_T = \left( \frac{\partial \rho}{\partial p} \right)_T \left( \frac{\partial p}{\partial \mu} \right)_T = \rho \left( \frac{\partial \rho}{\partial p} \right)_T
$$
宏观的**等温[压缩系数](@entry_id:272630) (isothermal compressibility)** $\kappa_T$ 定义为 $\kappa_T = -\frac{1}{V}(\frac{\partial V}{\partial p})_{T,N}$。通过简单的变换可以证明 $(\partial \rho / \partial p)_T = \rho \kappa_T$。将这些关系全部代入，我们最终得到：
$$
\langle (\Delta N_v)^2 \rangle = k_{\mathrm{B}} T v \rho^2 \kappa_T
$$
这个著名的公式表明，一个区域内的[粒子数涨落](@entry_id:151853)直接正比于该物质的等温[压缩系数](@entry_id:272630)。 [@problem_id:2675479] 容易被压缩的流体（$\kappa_T$ 大）会表现出更剧烈的[密度涨落](@entry_id:143540)。这个结果优雅地连接了微观世界的[粒子数涨落](@entry_id:151853)和宏观世界的力学响应性质。

我们可以通过一个具体的模型来验证这些关系。考虑一个[晶格](@entry_id:196752)气体模型，其中体积为 $V$ 的系统被划分为 $M=V/v_0$ 个独立的[晶格](@entry_id:196752)位点，每个位点要么为空，要么被一个粒子占据。其[巨配分函数](@entry_id:154455)为 $\Xi = (1 + q(T) e^{\beta\mu})^M$。通过对 $\ln\Xi$ 求导，我们可以分别计算出压强 $P$、密度 $\rho$ 和[压缩系数](@entry_id:272630) $\kappa_T$，并验证它们之间满足所有[热力学恒等式](@entry_id:142524)，包括吉布斯-杜亥姆关系 $(\partial P/\partial\mu)_T = \rho$ 和涨落-[压缩系数](@entry_id:272630)关系。 [@problem_id:2675486]

### [热力学极限](@entry_id:143061)与[系综等价性](@entry_id:141226)

[统计力](@entry_id:194984)学的一块基石是**[系综等价性](@entry_id:141226) (ensemble equivalence)** 原理。该原理指出，在**[热力学极限](@entry_id:143061)**下（即 $N, V \to \infty$，同时保持密度 $\rho = N/V$ 恒定），对于具有[短程相互作用](@entry_id:145678)且远离[相变](@entry_id:147324)点的系统，不同系综（如正则系综和[巨正则系综](@entry_id:141562)）对宏观[热力学性质](@entry_id:146047)的预言是相同的。

在[巨正则系综](@entry_id:141562)中，粒子数 $N$ 是涨落的。然而，其涨落的相对大小如何随系统尺寸变化？[粒子数涨落](@entry_id:151853)的标准差 $\sigma_N = \sqrt{\langle (\Delta N)^2 \rangle}$ 是一个广延量，正比于 $V^{1/2}$。而[平均粒子数](@entry_id:151202) $\langle N \rangle$ 也正比于 $V$。因此，相对涨落：
$$
\frac{\sigma_N}{\langle N \rangle} \sim \frac{V^{1/2}}{V} = V^{-1/2}
$$
在[热力学极限](@entry_id:143061)下（$V \to \infty$），相对涨落趋于零。 [@problem_id:267498] 这意味着粒子数的[概率分布](@entry_id:146404)变得极其尖锐，集中在平均值 $\langle N \rangle$ 附近。因此，一个开放系统在宏观尺度上变得与一个粒子数恰好固定为 $\langle N \rangle$ 的封闭系统几乎无法区分。这就是[系综等价性](@entry_id:141226)的根源：压强、能量密度等内涵量和广延量的密度在不同系综中的计算结果会趋于一致。 [@problem_id:2675498]

然而，必须强调的是，[系综等价性](@entry_id:141226)不适用于涨落量本身。例如，在[正则系综](@entry_id:142391)中，粒子数[方差](@entry_id:200758)恒为零，而在[巨正则系综](@entry_id:141562)中，它是一个正比于体积的非零值。此外，[系综等价性](@entry_id:141226)也适用于局域[可观测量](@entry_id:267133)。在一个宏观大系统内部的一个小的、有限的区域里，其统计性质由周围环境的内涵参量（$T, \mu$）决定，而与整个[大系统](@entry_id:166848)的边界条件是采用[正则系综](@entry_id:142391)还是[巨正则系综](@entry_id:141562)无关。 [@problem_id:2675498]

最后，[巨正则系综](@entry_id:141562)为研究[相变](@entry_id:147324)提供了强有力的理论工具。对于有限体积的系统，[巨配分函数](@entry_id:154455) $\Xi$ 是逸度 $z$ 的一个系数为正的多项式，因此对于所有正实数 $z$，$\ln \Xi$ 都是解析的，这意味着有限系统不会发生严格意义上的[相变](@entry_id:147324)。[相变](@entry_id:147324)是[热力学极限](@entry_id:143061)下的突变行为，它表现为 $\ln \Xi$ 对 $z$ 的非[解析性](@entry_id:140716)。根据著名的**杨-[李理论](@entry_id:148240) (Yang-Lee theory)**，这种非解析性源于[巨配分函数](@entry_id:154455)在[复逸度](@entry_id:160351)平面上的零点（即**[杨-李零点](@entry_id:160960)**）在[热力学极限](@entry_id:143061)下向实轴“收缩”并“夹断”[实轴](@entry_id:148276)所致。这些零点的[分布](@entry_id:182848)和行为，编码了系统发生[相变](@entry_id:147324)的全部信息。 [@problem_id:2675483]