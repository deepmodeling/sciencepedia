## 引言
在探索物理世界的过程中，我们常常使用平均值来描述一个宏观系统的状态，例如气体的平均能量或磁体的平均磁化强度。然而，一个系统并非静止地处于其平均状态，微观粒子永不停息的热运动导致物理量在平均值附近持续地涨落。这些涨落并非无足轻重的“噪音”，它们蕴含着关于系统稳定性、[相变](@entry_id:147324)行为以及对外界扰动响应方式的深刻信息。本文旨在填补仅靠平均值描述所留下的知识空白，系统地介绍量化这些涨落的强大数学语言——[统计矩](@entry_id:268545)。

本文将引导读者深入理解均值、[方差](@entry_id:200758)及更[高阶矩](@entry_id:266936)的物理意义和计算方法。在“原理与机制”一章中，我们将建立矩的数学定义，并展示如何巧妙地利用[统计力](@entry_id:194984)学中的核心工具——[配分函数](@entry_id:193625)——来生成任意阶的矩，从而将复杂的求和计算简化为优雅的[微分](@entry_id:158718)运算。接下来，在“应用与跨学科联系”一章中，我们将通过热容、量子统计、高分子物理和生物系统等一系列实例，展示这些统计概念如何将微观世界的涨落与宏观世界的[响应函数](@entry_id:142629)联系起来，彰显其在不同科学领域中的普适性和强大威力。最后，“实践练习”部分将提供具体的计算问题，帮助读者巩固所学知识，将理论应用于实践。

## 原理与机制

在[统计力](@entry_id:194984)学中，我们通常关注系统的宏观性质，这些性质是其微观组分（如原子或分子）行为的集体体现。平均值，例如系统的平均能量 $\langle E \rangle$ 或[平均粒子数](@entry_id:151202) $\langle N \rangle$，为我们提供了对这些宏观性质的初步描述。然而，仅有平均值并不足以完整地刻画一个系统。系统并非静止地处于其平均状态，而是围绕该平均值不断地进行着微观的涨落。理解这些涨落的性质和幅度，对于深入揭示系统的[热力学](@entry_id:141121)行为、稳定性以及它如何响应外部扰动至关重要。本章将系统地介绍描述这些涨落的数学工具——矩，并阐明它们与宏观可测量量之间的深刻联系。

### [统计矩](@entry_id:268545)：量化涨落的语言

为了超越平均值的描述，我们需要引入更高阶的统计量。对于一个物理量 $A$（例如能量 $E$、位置 $x$ 或磁化强度 $M$），其[概率分布](@entry_id:146404)为 $P(A)$，我们可以定义它的一系列**矩**（moments）。

**[原点矩](@entry_id:165197)**（moment about the origin）被定义为 $A$ 的各次幂的平均值：
$$
\langle A^n \rangle = \sum_i A_i^n P(A_i) \quad \text{(对于离散变量)}
$$
$$
\langle A^n \rangle = \int A^n P(A) \,dA \quad \text{(对于连续变量)}
$$
其中 $n$ 是一个非负整数。$n=1$ 时的第一[原点矩](@entry_id:165197)就是我们熟悉的**平均值**（mean）或[期望值](@entry_id:153208)，记为 $\langle A \rangle$。

然而，为了描述[分布](@entry_id:182848)在平均值周围的散布情况，**[中心矩](@entry_id:270177)**（central moments）更为有用。第 $n$ 阶[中心矩](@entry_id:270177) $\mu_n$ 被定义为 $A$ 与其平均值之差的 $n$ 次幂的[期望值](@entry_id:153208)：
$$
\mu_n = \langle (A - \langle A \rangle)^n \rangle
$$
最重要的[中心矩](@entry_id:270177)是[二阶中心矩](@entry_id:200758)，即**[方差](@entry_id:200758)**（variance），记为 $\sigma_A^2$：
$$
\sigma_A^2 = \mu_2 = \langle (A - \langle A \rangle)^2 \rangle = \langle A^2 - 2A\langle A \rangle + \langle A \rangle^2 \rangle = \langle A^2 \rangle - 2\langle A \rangle\langle A \rangle + \langle A \rangle^2 = \langle A^2 \rangle - \langle A \rangle^2
$$
[方差](@entry_id:200758)衡量了物理量 $A$ 的值偏离其平均值的典型平方距离。[方差](@entry_id:200758)的平方根 $\sigma_A$ 被称为**[标准差](@entry_id:153618)**（standard deviation），它具有与 $A$ 相同的量纲，直观地表示了[分布](@entry_id:182848)的宽度。

高阶[中心矩](@entry_id:270177)也提供了关于[分布](@entry_id:182848)形状的更多信息。例如，三阶[中心矩](@entry_id:270177) $\mu_3$ 与[分布](@entry_id:182848)的**偏度**（skewness）有关，它描述了[分布](@entry_id:182848)的不对称性。对于一个关于其平均值对称的[分布](@entry_id:182848)，所有奇数阶[中心矩](@entry_id:270177)（$\mu_3, \mu_5, \dots$）均为零。一个很好的物理例子是处于[热平衡](@entry_id:141693)状态的[理想气体](@entry_id:200096)中，单个速度分量（如 $v_x$）的[分布](@entry_id:182848)，即麦克斯韦-玻尔兹曼分布。该[分布函数](@entry_id:145626) $P(v_x)$ 是关于 $v_x=0$ 的偶函数，因此平均速度 $\langle v_x \rangle = 0$。由于其对称性，其三阶矩也必然为零 [@problem_id:1979424]：
$$
\langle v_x^3 \rangle = \int_{-\infty}^{\infty} v_x^3 P(v_x) \,dv_x = 0
$$
这是因为被积函数 $v_x^3 P(v_x)$ 是一个[奇函数](@entry_id:173259)，在对称区间上的积分为零。

四阶[中心矩](@entry_id:270177) $\mu_4$ 则与[分布](@entry_id:182848)的**[峰度](@entry_id:269963)**（kurtosis）有关，它衡量了[分布](@entry_id:182848)尾部的“厚重”程度，即出现极端值的倾向性。我们将在本章末尾进一步探讨这些[高阶矩](@entry_id:266936)。

### 从[配分函数](@entry_id:193625)到能量矩：[正则系综](@entry_id:142391)的方法

在[统计力](@entry_id:194984)学中，直接根据定义通过求和或积分来计算矩，有时会相当繁琐。幸运的是，系综理论提供了一个极其强大和优雅的工具，它允许我们从一个核心函数——**[配分函数](@entry_id:193625)**（partition function）——出发，通过简单的[微分](@entry_id:158718)运算来生成所有矩。

在**正则系综**中，系统与一个恒定温度 $T$ 的大[热库](@entry_id:143608)接触，其粒子数 $N$ 和体积 $V$ 固定。系统的核心是[正则配分函数](@entry_id:154330) $Z$，定义为所有可能[微观态](@entry_id:147392)的[玻尔兹曼因子](@entry_id:141054)的总和：
$$
Z = \sum_i \exp(-\beta E_i)
$$
其中 $i$ 遍历所有微观态， $E_i$ 是[微观态](@entry_id:147392) $i$ 的能量，而 $\beta = (k_B T)^{-1}$，$k_B$ 是[玻尔兹曼常数](@entry_id:142384)。

让我们看看如何从 $Z$ 中提取能量的矩。考虑 $Z$ 对 $\beta$ 的[偏导数](@entry_id:146280)：
$$
\frac{\partial Z}{\partial \beta} = \sum_i (-E_i) \exp(-\beta E_i)
$$
这与[平均能量](@entry_id:145892) $\langle E \rangle$ 的表达式非常相似：
$$
\langle E \rangle = \sum_i E_i P_i = \frac{\sum_i E_i \exp(-\beta E_i)}{Z} = -\frac{1}{Z} \frac{\partial Z}{\partial \beta} = -\frac{\partial \ln Z}{\partial \beta}
$$
这个优美的关系表明，[平均能量](@entry_id:145892)可以直接通过对[配分函数](@entry_id:193625)的对数求导得到。

更进一步，我们可以对 $\beta$ 求[二阶导数](@entry_id:144508)。这引出了能量的[方差](@entry_id:200758)：
$$
\frac{\partial^2 \ln Z}{\partial \beta^2} = \frac{\partial}{\partial \beta} \left( \frac{1}{Z}\frac{\partial Z}{\partial \beta} \right) = \frac{1}{Z}\frac{\partial^2 Z}{\partial \beta^2} - \frac{1}{Z^2}\left(\frac{\partial Z}{\partial \beta}\right)^2 = \frac{\sum_i E_i^2 e^{-\beta E_i}}{Z} - \left(\frac{\sum_i -E_i e^{-\beta E_i}}{Z}\right)^2 = \langle E^2 \rangle - \langle E \rangle^2
$$
因此，能量的[方差](@entry_id:200758) $\sigma_E^2$ 由下式给出：
$$
\sigma_E^2 = \langle E^2 \rangle - \langle E \rangle^2 = \frac{\partial^2 \ln Z}{\partial \beta^2} = -\frac{\partial \langle E \rangle}{\partial \beta}
$$
这些公式是[统计力](@entry_id:194984)学中的核心工具。它们将计算所有能量矩的复杂求和问题，简化为对[配分函数](@entry_id:193625) $\ln Z$ 求导的解析问题。$\ln Z$ 因此常被称为**[累积量生成函数](@entry_id:748109)**（cumulant-generating function）。

**示例 1：一个解析模型**
考虑一个由 $N$ 个可区分的非相互作用粒子组成的系统，其[配分函数](@entry_id:193625)已知为 $Z(\beta) = (a\beta)^{-N}$，其中 $a$ 是一个具有能量量纲的常数 [@problem_id:1979458]。我们可以直接应用上述公式。首先计算 $\ln Z$：
$$
\ln Z = -N \ln(a\beta) = -N(\ln a + \ln \beta)
$$
系统的[平均能量](@entry_id:145892)为：
$$
\langle E \rangle = -\frac{\partial \ln Z}{\partial \beta} = -(-N/\beta) = \frac{N}{\beta} = N k_B T
$$
能量的[方差](@entry_id:200758)为：
$$
\sigma_E^2 = \frac{\partial^2 \ln Z}{\partial \beta^2} = \frac{\partial}{\partial \beta} \left(\frac{N}{\beta}\right) = \frac{N}{\beta^2} = N (k_B T)^2
$$
这个例子干净利落地展示了从[配分函数](@entry_id:193625)求矩的威力。

**示例 2：一个离散量子系统**
让我们考虑一个更具体的物理模型：一个可以处于三个非简并[量子能级](@entry_id:136393) $E_1=0$, $E_2=\epsilon$, $E_3=4\epsilon$ 的单粒子系统 [@problem_id:1979422]。
其[配分函数](@entry_id:193625)为：
$$
Z = \exp(-\beta \cdot 0) + \exp(-\beta \epsilon) + \exp(-4\beta \epsilon) = 1 + \exp(-\beta \epsilon) + \exp(-4\beta \epsilon)
$$
我们可以直接根据定义计算平均能量和能量的平方的平均值：
$$
\langle E \rangle = \frac{0 \cdot e^{-\beta \cdot 0} + \epsilon \cdot e^{-\beta\epsilon} + 4\epsilon \cdot e^{-4\beta\epsilon}}{Z} = \frac{\epsilon e^{-\beta\epsilon} + 4\epsilon e^{-4\beta\epsilon}}{Z}
$$
$$
\langle E^2 \rangle = \frac{0^2 \cdot e^{-\beta \cdot 0} + \epsilon^2 \cdot e^{-\beta\epsilon} + (4\epsilon)^2 \cdot e^{-4\beta\epsilon}}{Z} = \frac{\epsilon^2 e^{-\beta\epsilon} + 16\epsilon^2 e^{-4\beta\epsilon}}{Z}
$$
然后，[方差](@entry_id:200758) $\sigma_E^2 = \langle E^2 \rangle - \langle E \rangle^2$ 可以通过代数运算得到。虽然可行，但过程略显繁琐。
或者，我们可以使用导数法。平均能量为：
$$
\langle E \rangle = -\frac{\partial \ln Z}{\partial \beta} = -\frac{1}{Z} \frac{\partial Z}{\partial \beta} = -\frac{1}{Z} (-\epsilon e^{-\beta\epsilon} - 4\epsilon e^{-4\beta\epsilon}) = \frac{\epsilon e^{-\beta\epsilon} + 4\epsilon e^{-4\beta\epsilon}}{Z}
$$
这与直接计算的结果一致。[能量方差](@entry_id:156656)则可以通过对 $\langle E \rangle$ 再次关于 $\beta$ 求导得到，这通常比直接计算 $\langle E^2 \rangle$ 并做减法要简洁。

### 涨落-耗散定理：从微观涨落到宏观响应

矩（特别是[方差](@entry_id:200758)）的物理意义远不止是描述[分布](@entry_id:182848)的宽度。它们与系统对外部扰动的宏观响应函数（如[热容](@entry_id:137594)、磁化率）之间存在着深刻而普适的联系。这类关系被称为**涨落-耗散定理**（fluctuation-dissipation theorems）。

#### 热容与[能量涨落](@entry_id:148029)

[定容热容](@entry_id:147536) $C_V$ 定义为系统平均能量随温度的变化率：
$$
C_V = \left( \frac{\partial \langle E \rangle}{\partial T} \right)_V
$$
我们可以利用链式法则将其与 $\beta$ 联系起来：
$$
C_V = \frac{\partial \langle E \rangle}{\partial \beta} \frac{\partial \beta}{\partial T}
$$
我们已经知道 $\frac{\partial \langle E \rangle}{\partial \beta} = -\sigma_E^2$，而 $\frac{\partial \beta}{\partial T} = \frac{\partial}{\partial T}(1/k_B T) = -1/(k_B T^2)$。将这两者结合，我们得到一个非凡的结果 [@problem_id:1979439]：
$$
C_V = (-\sigma_E^2) \left( -\frac{1}{k_B T^2} \right) = \frac{\sigma_E^2}{k_B T^2}
$$
这个公式是统计物理的基石之一。它表明，一个宏观可测量的[热力学](@entry_id:141121)量——[热容](@entry_id:137594)，正比于系统微观能量的[方差](@entry_id:200758)。一个具有高热容的系统，意味着我们只需注入少量热量就能显著提高其温度，同时也意味着其内部的[能量涨落](@entry_id:148029)非常剧烈。这个关系提供了一种通过测量宏观响应来探测微观涨落的方法，反之亦然。

#### 磁化率与磁化涨落

类似的关系也存在于其他[响应函数](@entry_id:142629)中。考虑一个处于外部[磁场](@entry_id:153296) $H$ 中的磁性系统。系统的[哈密顿量](@entry_id:172864)现在依赖于 $H$。系统的总磁化强度 $M$ 是与[磁场](@entry_id:153296) $H$ 共轭的变量。等温磁化率 $\chi_T$ 定义为在[零场](@entry_id:199169)附近，平均磁化强度随外场的变化率：
$$
\chi_T = \left( \frac{\partial \langle M \rangle}{\partial H} \right)_{T, H \to 0}
$$
可以证明，[磁化率](@entry_id:138219)与磁化强度的涨落之间存在如下关系：
$$
\chi_T = \frac{1}{k_B T} \sigma_M^2(H=0) = \beta \sigma_M^2(H=0)
$$
其中 $\sigma_M^2(H=0)$ 是在零外场下系统总磁化强度的[方差](@entry_id:200758)。这再次说明，系统对外部扰动（[磁场](@entry_id:153296)）的[线性响应](@entry_id:146180)（磁化率）由系统在没有扰动时自发的内部涨落（磁化涨落）所决定。

作为一个例子，考虑一个由 $N$ 个独立的、可区分的自旋-1/2 [磁偶极子](@entry_id:275765)组成的顺磁体，每个[磁偶极子](@entry_id:275765)的磁矩为 $\mu$ [@problem_id:1979400]。在[零场](@entry_id:199169)极限下，每个偶极子向上和向下的概率相等，均为 $1/2$。单个偶极子的磁矩 $m_i$ 的平均值为 $\langle m_i \rangle = 0$。其[方差](@entry_id:200758)为 $\sigma_{m_i}^2 = \langle m_i^2 \rangle - \langle m_i \rangle^2 = (\mu^2 \cdot \frac{1}{2} + (-\mu)^2 \cdot \frac{1}{2}) - 0^2 = \mu^2$。由于各偶极子是独立的，总磁化强度 $M = \sum_i m_i$ 的[方差](@entry_id:200758)等于各[方差](@entry_id:200758)之和：
$$
\sigma_M^2(H=0) = \sum_{i=1}^N \sigma_{m_i}^2 = N\mu^2
$$
代入涨落-耗散关系，我们立即得到该系统的磁化率：
$$
\chi_T = \frac{N\mu^2}{k_B T}
$$
这就是著名的[居里定律](@entry_id:147420)，它描述了顺磁材料的[磁化率](@entry_id:138219)与温度成反比。我们通过分析[零场](@entry_id:199169)下的涨落，直接推导出了一个关键的宏观响应行为。

### [连续系统](@entry_id:178397)中的矩

对于位置、动量等连续变量，计算矩的原理是相同的，只是求和被积分所取代。例如，对于一个在一维空间中运动的经典粒子，如果其势能为 $V(x)$，那么在温度 $T$ 下，其位置的[概率密度函数](@entry_id:140610)为：
$$
\rho(x) = \frac{\exp(-\beta V(x))}{Z_x}
$$
其中，$Z_x = \int \exp(-\beta V(x)) dx$ 是**位形[配分函数](@entry_id:193625)**（configurational partition function），积分范围是所有允许的位置。

与能量矩类似，我们可以通过对 $Z_x$ 的参数求导来得到位置的矩。考虑一个粒子被限制在 $x=0$ 到 $x=L$ 的区间内，并受到[线性势](@entry_id:160860)场 $V(x) = \alpha x$ 的作用 [@problem_id:1979446]。
这里的位形[配分函数](@entry_id:193625)是：
$$
Z_x(\beta, \alpha) = \int_0^L \exp(-\beta \alpha x) \,dx = \frac{1 - \exp(-\beta \alpha L)}{\beta \alpha}
$$
为了求得 $\langle x \rangle$ 和 $\sigma_x^2$，我们可以将 $-\beta \alpha$ 视为一个整体参数，记为 $k = -\beta \alpha$。然而，更通用的方法是注意到 $\langle x^n \rangle$ 可以通过对 $Z_x$ 关于 $(-\beta \alpha)$ 求导得到。一个更优雅的技巧是利用 $\ln Z_x$ 作为生成函数。可以证明：
$$
\langle x \rangle = -\frac{1}{\beta} \frac{\partial \ln Z_x}{\partial \alpha}, \quad \sigma_x^2 = \langle x^2 \rangle - \langle x \rangle^2 = -\frac{1}{\beta} \frac{\partial \langle x \rangle}{\partial \alpha} = \frac{1}{\beta^2} \frac{\partial^2 \ln Z_x}{\partial \alpha^2}
$$
通过对 $Z_x$ 求导，我们可以得到该系统位置的平均值和[方差](@entry_id:200758)，并分析它们如何依赖于温度 $T$ 和[势场](@entry_id:143025)强度 $\alpha$。例如，在高温极限下 ($\beta \alpha L \ll 1$)，粒子近似[均匀分布](@entry_id:194597)，$\langle x \rangle \to L/2$，$\sigma_x^2 \to L^2/12$。在低温或强场极限下，粒子则被“推”到势能最低的 $x=0$ 处，$\langle x \rangle \to 0$ 且 $\sigma_x^2 \to 0$。

### [巨正则系综](@entry_id:141562)中的[粒子数涨落](@entry_id:151853)

当系统不仅可以与[热库](@entry_id:143608)[交换能](@entry_id:137069)量，还可以与粒子库交换粒子时，我们使用**[巨正则系综](@entry_id:141562)**来描述它。此时，系统的温度 $T$、体积 $V$ 和化学势 $\mu$ 是固定的，而能量 $E$ 和粒子数 $N$ 会发生涨落。

这个系综的核心是**[巨配分函数](@entry_id:154455)** $\mathcal{Z}$：
$$
\mathcal{Z} = \sum_N \sum_{i(N)} \exp(-\beta(E_{i(N)} - \mu N))
$$
其中第一个求和遍历所有可能的粒子数 $N$，第二个求和遍历给定粒子数 $N$ 下的所有微观能态 $i(N)$。

与[正则系综](@entry_id:142391)完全类似，$\ln \mathcal{Z}$ 也是一个[累积量生成函数](@entry_id:748109)，这次是针对能量和粒子数。[平均粒子数](@entry_id:151202) $\langle N \rangle$ 和其[方差](@entry_id:200758) $\sigma_N^2$ 可以通过对 $\ln \mathcal{Z}$ 关于化学势 $\mu$ 求导得到：
$$
\langle N \rangle = \frac{1}{\beta} \frac{\partial \ln \mathcal{Z}}{\partial \mu}
$$
$$
\sigma_N^2 = \langle N^2 \rangle - \langle N \rangle^2 = \frac{1}{\beta^2} \frac{\partial^2 \ln \mathcal{Z}}{\partial \mu^2}
$$
考虑一个简单的[量子点模型](@entry_id:266819)，它只有一个能量为 $\epsilon$ 的电子能级 [@problem_id:1979437]。根据[泡利不相容原理](@entry_id:141850)，该能级要么为空 ($N=0$)，要么被一个电子占据 ($N=1$)。其[巨配分函数](@entry_id:154455)为：
$$
\mathcal{Z} = \underbrace{\exp(-\beta(0 - \mu \cdot 0))}_{N=0} + \underbrace{\exp(-\beta(\epsilon - \mu \cdot 1))}_{N=1} = 1 + \exp(-\beta(\epsilon - \mu))
$$
平均占据数（[平均粒子数](@entry_id:151202)）为：
$$
\langle N \rangle = \frac{0 \cdot 1 + 1 \cdot \exp(-\beta(\epsilon - \mu))}{\mathcal{Z}} = \frac{1}{1 + \exp(\beta(\epsilon-\mu))}
$$
这就是著名的**[费米-狄拉克分布](@entry_id:138909)**。由于该系统只能取 $N=0$ 或 $N=1$，因此 $N^2=N$。所以 $\langle N^2 \rangle = \langle N \rangle$。粒子数[方差](@entry_id:200758)为：
$$
\sigma_N^2 = \langle N^2 \rangle - \langle N \rangle^2 = \langle N \rangle - \langle N \rangle^2 = \langle N \rangle (1 - \langle N \rangle)
$$
将 $\langle N \rangle$ 的表达式代入，我们便得到了[粒子数涨落](@entry_id:151853)的幅度。这个涨落幅度在 $\epsilon = \mu$ 时达到最大，此时能级被占据和未被占据的概率相等。与[热容](@entry_id:137594)和磁化率类似，[粒子数涨落](@entry_id:151853)也与一个宏观[响应函数](@entry_id:142629)——等温[压缩系数](@entry_id:272630) $\kappa_T$ 相关。

### [高阶矩](@entry_id:266936)与[分布](@entry_id:182848)形状

最后，我们回到更高阶的矩，它们提供了关于[分布](@entry_id:182848)形状的更精细信息。

#### [协方差与相关性](@entry_id:262778)

对于多个[随机变量](@entry_id:195330)，我们可以定义**协[方差](@entry_id:200758)**（covariance）来衡量它们之间的[线性相关](@entry_id:185830)性。对于两个变量 $A$ 和 $B$，其协[方差](@entry_id:200758)为：
$$
\text{cov}(A, B) = \langle (A - \langle A \rangle)(B - \langle B \rangle) \rangle = \langle AB \rangle - \langle A \rangle \langle B \rangle
$$
如果 $A$ 和 $B$ **统计独立**（statistically independent），那么 $\langle AB \rangle = \langle A \rangle \langle B \rangle$，因此它们的协[方差](@entry_id:200758)为零。在物理系统中，不同自由度之间的独立性常常导致协[方差](@entry_id:200758)为零。例如，在[经典理想气体](@entry_id:156161)中，由于[哈密顿量](@entry_id:172864)是可分离的（$H = \frac{1}{2m}(p_x^2+p_y^2+p_z^2)$），不同方向的速度分量 $v_x, v_y, v_z$ 是统计独立的。因此，它们的协[方差](@entry_id:200758)为零 [@problem_id:1979459]：
$$
\langle v_x v_y \rangle = \langle v_x \rangle \langle v_y \rangle = 0 \cdot 0 = 0
$$

#### [峰度](@entry_id:269963)与[特征函数](@entry_id:186820)

[标准化](@entry_id:637219)四阶[中心矩](@entry_id:270177)，即**峰度**（kurtosis），$\kappa = \mu_4 / \sigma^4$，常被用来与标准的高斯（正态）[分布](@entry_id:182848)进行比较。对于任何[高斯分布](@entry_id:154414)，其[峰度](@entry_id:269963)都恰好为 3。对于一维麦克斯韦-玻尔兹曼速度[分布](@entry_id:182848)（本质上是一个高斯分布），我们可以通过计算积分来验证这一点 [@problem_id:1979471]。
$$
P(v_x) \propto \exp\left(-\frac{m v_x^2}{2 k_B T}\right)
$$
我们发现 $\mu = \langle v_x \rangle = 0$，[方差](@entry_id:200758) $\sigma^2 = \langle v_x^2 \rangle = k_B T / m$，而四阶矩 $\mu_4 = \langle v_x^4 \rangle = 3 (k_B T / m)^2$。因此，峰度为：
$$
\kappa = \frac{\mu_4}{\sigma^4} = \frac{3 (k_B T / m)^2}{(k_B T / m)^2} = 3
$$
这证实了气体[粒子速度](@entry_id:196946)分量的[分布](@entry_id:182848)具有与[高斯分布](@entry_id:154414)相同的“尾部”特征。

最后，值得一提的是，正如[配分函数](@entry_id:193625)可以生成能量或粒子数的矩一样，任何[概率分布](@entry_id:146404)的矩都可以从其**特征函数**（characteristic function）$\phi(k) = \langle e^{ikX} \rangle$ 中生成。通过对 $\phi(k)$ 在 $k=0$ 处进行泰勒展开，可以发现各阶矩是展开系数。具体而言：
$$
\langle X^n \rangle = \frac{1}{i^n} \left. \frac{d^n \phi(k)}{dk^n} \right|_{k=0}
$$
例如，我们可以通过测量动量的[特征函数](@entry_id:186820) $\phi(k) = \langle e^{ikp} \rangle$ 来确定系统的[平均动能](@entry_id:146353) [@problem_id:1979438]。平均动能为 $\langle E_k \rangle = \langle p^2/2m \rangle$。根据上述关系，$\langle p^2 \rangle = -\left. \frac{d^2 \phi(k)}{dk^2} \right|_{k=0}$。因此：
$$
\langle E_k \rangle = -\frac{1}{2m} \left. \frac{d^2 \phi(k)}{dk^2} \right|_{k=0}
$$
这再次体现了[统计力](@entry_id:194984)学中的一个中心思想：一个精心构造的“生成函数”（无论是[配分函数](@entry_id:193625)还是[特征函数](@entry_id:186820)）蕴含了系统的全部统计信息，可以通过简单的数学运算（如[微分](@entry_id:158718)）来提取这些信息。