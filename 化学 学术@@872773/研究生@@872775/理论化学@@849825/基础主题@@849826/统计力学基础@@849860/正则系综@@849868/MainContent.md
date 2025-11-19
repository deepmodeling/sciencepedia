## 引言
[正则系综](@entry_id:142391)是[统计力](@entry_id:194984)学的核心基石，为理解与外界环境存在能量交换的物理和化学系统提供了强大的理论框架。然而，如何从微观层面（如单个分子的能级与构型）精确预测和解释我们宏观世界中可测量的热力学性质（如温度、压强、热容），始终是理论科学面临的中心问题。本文旨在系统性地解答这一问题，为读者构建一个关于[正则系综](@entry_id:142391)的完整知识体系。

本文将分为三个章节，首先在“原理与机制”中，我们将从第一性原理出发，推导玻尔兹曼分布，并揭示[配分函数](@entry_id:193625)作为连接微观与宏观世界的数学桥梁的核心作用。接着，在“应用与跨学科联系”一章，我们将展示[正则系综](@entry_id:142391)如何在物理、化学、生物及[材料科学](@entry_id:152226)等多个领域中被用来解释从理想气体到复杂生物大分子的各种现象。最后，通过“动手实践”部分，读者将有机会运用所学知识解决具体问题，从而加深对理论的理解。

## 原理与机制

在理解了[正则系综](@entry_id:142391)作为描述与大热库进行能量交换的[封闭系统](@entry_id:139565)的基本框架之后，本章将深入探讨其核心的数学与物理原理。我们将从第一性原理出发，推导正则[概率分布](@entry_id:146404)，阐明[正则配分函数](@entry_id:154330)作为中心角色的意义，并揭示其如何成为连接微观[量子态](@entry_id:146142)与宏观[热力学性质](@entry_id:146047)的桥梁。此外，我们还将探讨[能量涨落](@entry_id:148029)的物理内涵以及该系综在分子系统中的具体应用。

### 正则[分布](@entry_id:182848)的物理基础

正则系综描述的是一个粒子数 $N$ 和体积 $V$ 固定，但与一个温度恒为 $T$ 的巨大热库（heat bath）接触，可以自由交换能量的系统。其核心问题是：在[热平衡](@entry_id:141693)状态下，该系统处于能量为 $E_i$ 的特定微观状态 $i$ 的概率 $p_i$ 是多少？这个问题的答案，即玻尔兹曼分布，并非一个基本公设，而是可以从更基本的[统计力](@entry_id:194984)学原理——微正则系综的等概率原理——中推导出来的。

为了进行推导，我们考虑一个由我们感兴趣的系统 $S$ 和一个巨大的[热库](@entry_id:143608) $B$ 组成的复合“宇宙”。这个复合系统是完全孤立的，其总能量 $E_{\mathrm{tot}}$ 是一个守恒量。根据[微正则系综](@entry_id:141513)的基本假设，这个孤立的复合系统在总能量为 $E_{\mathrm{tot}}$ 的所有可及微观状态上是等[概率分布](@entry_id:146404)的。

推导过程依赖于一系列关键的物理假设 [@problem_id:2811761]：

1.  **弱耦合假设 (Weak Coupling)**：系统与[热库](@entry_id:143608)之间的相互作用能 $E_{\mathrm{int}}$ 必须足够小，可以忽略不计。这意味着总能量近似为两部分之和，$E_{\mathrm{tot}} \approx E_S + E_B$。此假设保证了系统和[热库](@entry_id:143608)各自的[能谱](@entry_id:181780)基本不受相互作用的扰动，它们的主要作用是促成能量交换。

2.  **大[热库](@entry_id:143608)假设 (Large Bath)**：热库远大于系统（例如，粒子数 $N_B \gg N_S$）。这保证了系统能量 $E_S$ 的任何变化相对于总能量 $E_{\mathrm{tot}}$ 都是微不足道的（$E_S \ll E_{\mathrm{tot}}$）。因此，热库的温度 $T$ 不会因为与系统[交换能](@entry_id:137069)量而发生改变。

3.  **[遍历性假设](@entry_id:147104) (Ergodicity)**：在足够长的时间内，复合系统会经历所有总能量为 $E_{\mathrm{tot}}$ 的可及微观状态。

基于这些假设，系统 $S$ 处于某个特定微观状态 $i$（能量为 $E_i$）的概率 $p_i$ 正比于[热库](@entry_id:143608) $B$ 与之相容的微观状态数 $\Omega_B$。当系统能量为 $E_i$ 时，热库的能量必须为 $E_B = E_{\mathrm{tot}} - E_i$。因此，
$$
p_i \propto \Omega_B(E_{\mathrm{tot}} - E_i)
$$

利用玻尔兹曼关系式 $S_B = k_B \ln \Omega_B$，其中 $S_B$ 是热库的熵，$k_B$ 是玻尔兹曼常数，我们可以将上式写为：
$$
p_i \propto \exp\left( \frac{S_B(E_{\mathrm{tot}} - E_i)}{k_B} \right)
$$

由于 $E_i \ll E_{\mathrm{tot}}$，我们可以将热库的熵 $S_B(E_{\mathrm{tot}} - E_i)$ 在 $E_{\mathrm{tot}}$ 附近进行泰勒展开，并保留到线性项：
$$
S_B(E_{\mathrm{tot}} - E_i) \approx S_B(E_{\mathrm{tot}}) - \left( \frac{\partial S_B}{\partial E_B} \right)_{E_B=E_{\mathrm{tot}}} E_i
$$

根据[热力学](@entry_id:141121)定义，熵对能量的偏导数即为温度的倒数：$\left( \frac{\partial S_B}{\partial E_B} \right) = \frac{1}{T}$。由于热库巨大，其温度 $T$ 是一个恒定的参数。定义[逆温](@entry_id:140086) $\beta = \frac{1}{k_B T}$，我们得到：
$$
S_B(E_{\mathrm{tot}} - E_i) \approx S_B(E_{\mathrm{tot}}) - \frac{E_i}{T} = S_B(E_{\mathrm{tot}}) - k_B \beta E_i
$$

代入概率表达式中，
$$
p_i \propto \exp\left( \frac{S_B(E_{\mathrm{tot}})}{k_B} - \beta E_i \right) = \exp\left( \frac{S_B(E_{\mathrm{tot}})}{k_B} \right) \exp(-\beta E_i)
$$

由于 $\exp(S_B(E_{\mathrm{tot}})/k_B)$ 是一个不依赖于系统微观状态 $i$ 的常数，我们可以将其吸收到归一化常数中，从而得到核心结果：
$$
p_i \propto \exp(-\beta E_i)
$$

为了将此比例关系转变为等式，我们必须对所有可能的微观状态进行归一化，即 $\sum_i p_i = 1$。这引入了**[正则配分函数](@entry_id:154330) (Canonical Partition Function)** $Z$：
$$
Z(\beta, V, N) = \sum_i \exp(-\beta E_i)
$$

最终，系统处于微观状态 $i$ 的概率为：
$$
p_i = \frac{\exp(-\beta E_i)}{Z}
$$
这就是著名的**[玻尔兹曼分布](@entry_id:142765)**。它表明，在给定温度下，系统处于某个状态的概率仅由该状态的能量决定，能量越高的状态，其占据概率呈指数级下降。

### [正则配分函数](@entry_id:154330)：核心物理量

[配分函数](@entry_id:193625) $Z$ 不仅仅是一个[归一化常数](@entry_id:752675)，它是正则系综的中心数学构造，包含了系统在给定 $N, V, T$ 条件下所有的[热力学](@entry_id:141121)信息。

对于经典系统，其微观状态由相空间中的点 $\Gamma = (\mathbf{q}, \mathbf{p})$ 描述，[配分函数](@entry_id:193625)的求和形式被积分取代：
$$
Z = \frac{1}{N! h^{3N}} \int \exp(-\beta H(\Gamma)) \, d\Gamma
$$
其中 $H(\Gamma)$ 是系统的[哈密顿量](@entry_id:172864)，$d\Gamma = d^{3N}q \, d^{3N}p$ 是相空间体积元。因子 $h^{3N}$ (其中 $h$ 是[普朗克常数](@entry_id:139373))使得 $Z$ 无量纲化，并与量子力学中的[态密度](@entry_id:147894)相联系。而 $N!$ 因子则是为了修正经典粒子可分辨性带来的过度计数问题，这对于处理不可区分的粒子至关重要 [@problem_id:2008512]。

#### 配分[函数的收敛](@entry_id:152305)性

[正则系综](@entry_id:142391)的数学有效性取决于[配分函数](@entry_id:193625) $Z$ 的收敛性。一个发散的[配分函数](@entry_id:193625)通常预示着物理模型的不自洽或热力学平衡态的不存在 [@problem_id:2811797]。

1.  **[能谱](@entry_id:181780)的下界**：对于物理系统，能量谱通常是有下界的（$E_i \ge E_0$），以保证系统的稳定性。例如，如果一个经典系统的势能 $U(q)$ 没有下界（即可以趋于 $-\infty$），那么 $\exp(-\beta U(q))$ 因子将会在某些构型区域内趋于无穷大，导致构型积分发散。这对应于物理上的系统坍缩，例如库仑吸引势若无短程排斥，原子就会坍缩。因此，一个稳定的[热力学系统](@entry_id:188734)要求其[哈密顿量](@entry_id:172864)有下界 [@problem_id:2811797]。

2.  **[能谱](@entry_id:181780)的[上界](@entry_id:274738)与[态密度](@entry_id:147894)增长**：
    -   如果[能谱](@entry_id:181780)是无[上界](@entry_id:274738)的，为了使 $Z = \sum_i g_i \exp(-\beta E_i)$ 收敛（$g_i$ 为[能级简并](@entry_id:140812)度），[玻尔兹曼因子](@entry_id:141054) $\exp(-\beta E_i)$ 必须随着能量 $E_i$ 的增加而衰减得足够快。对于正温度（$\beta > 0$），这是天然满足的。收敛的关键在于简并度 $g_i$ 的增长速度不能超过指数衰减的速度。如果态密度 $\Omega(E)$ 的增长慢于指数形式，例如 $\Omega(E) \sim E^\alpha$（亚[指数增长](@entry_id:141869)），[配分函数](@entry_id:193625)对任何 $\beta > 0$ 都是收敛的 [@problem_id:2811797]。
    -   然而，如果态密度呈[指数增长](@entry_id:141869)，$\Omega(E) \asymp \exp(\alpha E)$，则[配分函数](@entry_id:193625)的被积函数行为如 $\exp((\alpha - \beta)E)$。此时，只有当 $\beta > \alpha$ (即温度 $T  1/(k_B \alpha)$)时，[配分函数](@entry_id:193625)才会收敛。临界温度 $T_c = 1/(k_B \alpha)$（有时称为 Hagedorn 温度）标志着一个[相变](@entry_id:147324)的发生，超过此温度，系统无法形成平衡态 [@problem_id:2811797]。
    -   对于[负绝对温度](@entry_id:137353)（$\beta  0$）的情况，$\exp(-\beta E_i) = \exp(|\beta| E_i)$ 是一个增长因子。要使[配分函数](@entry_id:193625)收敛，系统的[能谱](@entry_id:181780)必须有[上界](@entry_id:274738)。这在某些特殊系统（如核自旋系统）中可以实现。

3.  **[经典理想气体](@entry_id:156161)**：对于[经典理想气体](@entry_id:156161)，其动[能谱](@entry_id:181780)是无界的 ($p_i^2/2m$)。然而，动能部分的[配分函数](@entry_id:193625)积分 $\int \exp(-\beta p^2/2m) d^3p$ 是一个标准的[高斯积分](@entry_id:187139)，其结果是收敛的，例如在三维空间中为 $(2\pi m k_B T)^{3/2}$。因此，动量域的无界性本身不会导致[配分函数](@entry_id:193625)发散 [@problem_id:2811797]。

### 通往[热力学](@entry_id:141121)的桥梁

[配分函数](@entry_id:193625) $Z$ 的核心价值在于它与宏观热力学势的直接联系。在[正则系综](@entry_id:142391) $(T, V, N)$ 的自然变量下，与之对应的热力学势是**亥姆霍兹自由能 (Helmholtz Free Energy)** $F$。它们之间的关系是：
$$
F(T, V, N) = -k_B T \ln Z(T, V, N)
$$
这个简单的方程是[统计力](@entry_id:194984)学和[热力学](@entry_id:141121)之间的核心桥梁 [@problem_id:1981245]。一旦我们通过微观模型计算出 $Z$，就可以通过[微分](@entry_id:158718)运算得到所有其他的宏观[热力学](@entry_id:141121)量。

例如，从[热力学基本关系](@entry_id:144320) $dF = -SdT - PdV + \mu dN$，我们可以立即得到熵 $S$、压强 $P$ 和化学势 $\mu$ 的表达式：
$$
S = -\left(\frac{\partial F}{\partial T}\right)_{V,N}, \quad P = -\left(\frac{\partial F}{\partial V}\right)_{T,N}, \quad \mu = \left(\frac{\partial F}{\partial N}\right)_{T,V}
$$

我们也可以直接从[配分函数](@entry_id:193625) $Z$ 出发推导这些量。

**内能 (Internal Energy, $U$)**:
系统的[平均能量](@entry_id:145892)，即内能 $U$，是能量的[期望值](@entry_id:153208) $\langle E \rangle$。
$$
U = \langle E \rangle = \sum_i p_i E_i = \frac{1}{Z} \sum_i E_i \exp(-\beta E_i)
$$
注意到 $\frac{\partial Z}{\partial \beta} = \sum_i (-E_i) \exp(-\beta E_i) = -Z \langle E \rangle$。因此，我们得到一个非常重要的关系 [@problem_id:487646]：
$$
U = -\frac{1}{Z} \frac{\partial Z}{\partial \beta} = -\left(\frac{\partial \ln Z}{\partial \beta}\right)_{V,N}
$$

**压强 (Pressure, $P$)**:
压强可以通过亥姆霍兹自由能对体积的[偏导数](@entry_id:146280)得到：
$$
P = -\left(\frac{\partial F}{\partial V}\right)_{T,N} = k_B T \left(\frac{\partial \ln Z}{\partial V}\right)_{T,N}
$$
这个公式允许我们从一个微观模型计算宏观的[物态方程](@entry_id:194191)。例如，考虑一个改进的[理想气体模型](@entry_id:191415)，其中粒子本身占据了体积 $b$，使得可用体积为 $V - Nb$。其[配分函数](@entry_id:193625)为 $Z(N, V, T) = \frac{[c(V - Nb)T^3]^N}{N!}$。利用上述公式 [@problem_id:1996088]：
$$
\ln Z = N[\ln c + \ln(V - Nb) + 3\ln T] - \ln(N!)
$$
$$
P = k_B T \left( \frac{\partial \ln Z}{\partial V} \right)_{T,N} = k_B T \left( N \frac{1}{V - Nb} \right) = \frac{N k_B T}{V - Nb}
$$
这正是著名的[范德华方程](@entry_id:140886)的压强修正项，它直接从[配分函数](@entry_id:193625)的体积依赖性中推导出来。

### [正则系综](@entry_id:142391)中的[能量涨落](@entry_id:148029)

与能量固定的微正则系综不同，[正则系综](@entry_id:142391)中的系统能量不是一个定值，而是在与热库的能量交换中围绕平均值 $U$ 涨落。这些涨落的大小并非任意，而是与系统的宏观响应函数直接相关。

能量的[方差](@entry_id:200758) $\sigma_E^2$ 被定义为：
$$
\sigma_E^2 = \langle (E - \langle E \rangle)^2 \rangle = \langle E^2 \rangle - \langle E \rangle^2
$$
我们可以通过对 $\ln Z$ 求[二阶导数](@entry_id:144508)来计算它。可以证明：
$$
\frac{\partial^2 \ln Z}{\partial \beta^2} = \langle E^2 \rangle - \langle E \rangle^2
$$
因此，$\sigma_E^2 = \left(\frac{\partial^2 \ln Z}{\partial \beta^2}\right)_{V,N}$。又因为 $U = -\left(\frac{\partial \ln Z}{\partial \beta}\right)_{V,N}$，我们还可以得到 $\sigma_E^2 = -\left(\frac{\partial U}{\partial \beta}\right)_{V,N}$。

系统的恒容[热容](@entry_id:137594) $C_V$ 定义为 $C_V = \left(\frac{\partial U}{\partial T}\right)_{V,N}$。利用[链式法则](@entry_id:190743) $\frac{\partial}{\partial \beta} = \frac{dT}{d\beta} \frac{\partial}{\partial T} = -k_B T^2 \frac{\partial}{\partial T}$，我们得到一个深刻的联系 [@problem_id:1996111]：
$$
\sigma_E^2 = -\frac{\partial U}{\partial \beta} = - \left( -k_B T^2 \frac{\partial U}{\partial T} \right) = k_B T^2 C_V
$$
于是，
$$
C_V = \frac{\sigma_E^2}{k_B T^2}
$$
这个关系是一个**涨落-耗散定理 (fluctuation-dissipation theorem)** 的简单例子。它表明，一个宏观响应函数（[热容](@entry_id:137594) $C_V$，描述系统对温度变化的响应）与一个微观[平衡态](@entry_id:168134)的涨落量（[能量方差](@entry_id:156656) $\sigma_E^2$）直接成正比。一个系统的[热容](@entry_id:137594)越大，其内部的[能量涨落](@entry_id:148029)就越剧烈。

#### [热力学极限](@entry_id:143061)下的涨落

对于宏观系统，[能量涨落](@entry_id:148029)是否显著？我们可以通过计算相对涨落 $\sigma_E / U$ 来评估。对于一个含有 $N$ 个粒子的经典单原子[理想气体](@entry_id:200096)，我们有 $U = \frac{3}{2}N k_B T$ 和 $C_V = \frac{3}{2}N k_B$。代入涨落公式 [@problem_id:1963079]：
$$
\sigma_E^2 = k_B T^2 C_V = k_B T^2 \left(\frac{3}{2}N k_B\right) = \frac{3}{2}N (k_B T)^2
$$
因此，[标准差](@entry_id:153618)为 $\sigma_E = \sqrt{\frac{3}{2}N} k_B T$。相对涨落为：
$$
\frac{\sigma_E}{U} = \frac{\sqrt{\frac{3}{2}N} k_B T}{\frac{3}{2}N k_B T} = \frac{1}{\sqrt{\frac{3}{2}N}} = \sqrt{\frac{2}{3N}}
$$
这个结果表明，能量的相对涨落与 $1/\sqrt{N}$ 成正比。对于宏观系统，例如 $N \sim 10^{23}$，这个相对涨落小到可以忽略不计。这解释了为什么在宏观尺度上，正则系综和微正则系综给出的[热力学](@entry_id:141121)结果是等价的：尽管能量在微观上不断涨落，但其相对大小在[热力学极限](@entry_id:143061)下趋于零，使得能量看起来如同一个固定值。

### 应用与延展

#### [分子配分函数](@entry_id:152768)的因子分解

在理论化学中，我们常常处理由分子组成的系统。要计算系统的[总配分函数](@entry_id:190183) $Q_N = q^N/N!$，关键是计算单个分子的[配分函数](@entry_id:193625) $q$。如果分子的总[哈密顿量](@entry_id:172864) $\hat{H}$ 可以近似地写成几个独立自由度之和，那么[分子配分函数](@entry_id:152768) $q$ 就可以[因子分解](@entry_id:150389)为各个部分的乘积。这是一个极其强大的简化 [@problem_id:2811749]。
$$
\hat{H} \approx \hat{H}_{\mathrm{trans}} + \hat{H}_{\mathrm{rot}} + \hat{H}_{\mathrm{vib}} + \hat{H}_{\mathrm{elec}} \quad \Rightarrow \quad q = q_{\mathrm{trans}} q_{\mathrm{rot}} q_{\mathrm{vib}} q_{\mathrm{elec}}
$$
这个分解的物理依据如下：
1.  **[平动](@entry_id:187700)与内部分离**：在无外场时，分子的质心平动运动可以与内部运动（转动、[振动](@entry_id:267781)、电子）精确分离。
2.  **电子与核运动分离**：**玻恩-奥本海默 (Born-Oppenheimer) 近似**基于电子质量远小于[原子核](@entry_id:167902)，认为电子能瞬时适应核构型的变化。这使得我们可以先求解[固定核](@entry_id:169539)构型下的[电子薛定谔方程](@entry_id:177999)，得到[势能面](@entry_id:147441)，然后在该[势能面](@entry_id:147441)上求解核的运动。
3.  **[振动](@entry_id:267781)与转动分离**：**[刚性转子-谐振子](@entry_id:169758) (Rigid-Rotor Harmonic-Oscillator, RRHO) 近似**将分子的转动视为一个具有固定[键长](@entry_id:144592)和键角的刚体，将[振动](@entry_id:267781)视为在平衡构型附近的小位移[简谐运动](@entry_id:148744)。这忽略了转动-[振动耦合](@entry_id:756495)（如[离心畸变](@entry_id:156195)效应）。这种近似的合理性在于，对于多数分子在常温下，[振动](@entry_id:267781)幅度很小，转动引起的[键长](@entry_id:144592)变化也小，使得耦合能量远小于 $k_B T$ 和主要的[能级间距](@entry_id:181168)。
4.  **电子基态主导**：多数分子的电子激发能很高（$\gg k_B T$），因此在通常温度下，只有电子基态有显著布居。此时，$q_{\mathrm{elec}}$ 简化为[基态](@entry_id:150928)的简并度 $g_0$。

#### [经典极限](@entry_id:148587)与[量子统计](@entry_id:143815)

经典[统计力](@entry_id:194984)学是[量子统计力学](@entry_id:140244)在特定条件下的近似。这个条件可以通过**[热德布罗意波长](@entry_id:143992) (thermal de Broglie wavelength)** $\Lambda$ 来量化 [@problem_id:2811751]。对于质量为 $m$ 的粒子，其定义为：
$$
\Lambda = \frac{h}{\sqrt{2\pi m k_B T}}
$$
$\Lambda$ 可以被理解为一个粒子在热运动下的平均[量子波包](@entry_id:197756)大小。经典统计（即[麦克斯韦-玻尔兹曼统计](@entry_id:746908)）成立的判据是，粒子的平均间距远大于其[热德布罗意波长](@entry_id:143992)，这意味着粒子间的[波函数](@entry_id:147440)重叠可以忽略。用粒子[数密度](@entry_id:268986) $n=N/V$ 表示，这个条件是：
$$
n^{-1/3} \gg \Lambda \quad \text{或等价地} \quad n\Lambda^3 \ll 1
$$
这个无量纲量 $n\Lambda^3$ 可以看作是“每个[量子态](@entry_id:146142)体积 $\Lambda^3$ 内的[平均粒子数](@entry_id:151202)”。当 $n\Lambda^3 \ll 1$ 时，[量子态](@entry_id:146142)是稀疏填充的，量子交换效应（源于[玻色子](@entry_id:138266)或[费米子](@entry_id:146235)的对称性要求）可以忽略，此时使用修正了不可区分性的经典[配分函数](@entry_id:193625) $Q_N = q^N/N!$ 是准确的。该条件也正是[亥姆霍兹自由能](@entry_id:136442)的经典表达式 $F/N = k_B T [\ln(n\Lambda^3) - 1]$ 成立的区域。

反之，当 $n\Lambda^3 \gtrsim 1$ 时（低温或高密度），量子效应变得显著，必须使用费米-狄拉克或[玻色-爱因斯坦统计](@entry_id:139965)来描述系统。

#### [统计系综](@entry_id:149738)的比较与选择

最后，将正则系综置于更广阔的背景中是有益的。[统计力](@entry_id:194984)学中有三个最基本的系综，它们的选择取决于[系统与环境](@entry_id:142270)的相互作用方式 [@problem_id:2811802]：

-   **微正则系综 (NVE)**：描述一个完全孤立的系统，其粒子数 $N$、体积 $V$ 和能量 $E$ 都是固定的。其[概率分布](@entry_id:146404)在能量为 $E$ 的所有可及微观态上是均匀的。这适用于理论分析，如孤立星团或气相[单分子反应](@entry_id:167301)。

-   **[正则系综 (NVT)](@entry_id:747104)**：描述一个与热库接触的封闭系统，其 $N$ 和 $V$ 固定，但能量 $E$ 可以涨落，由温度 $T$ 控制。其[概率分布](@entry_id:146404)是玻尔兹曼分布 $p_i \propto \exp(-\beta E_i)$。这是模拟和理论研究中最常用的系综，适用于描述恒温下的凝聚相物质或溶剂中的分子。

-   **[巨正则系综](@entry_id:141562) ($\mu$VT)**：描述一个与粒子和热的复合大库接触的[开放系统](@entry_id:147845)，其体积 $V$、温度 $T$ 和化学势 $\mu$ 固定，而粒子数 $N$ 和能量 $E$ 都在涨落。其[概率分布](@entry_id:146404)为 $p_{i,N} \propto \exp[-\beta(E_{i,N} - \mu N)]$。这适用于研究吸附现象、相平衡或[化学反应](@entry_id:146973)平衡等粒子数可变的系统。

这三大系综通过[勒让德变换](@entry_id:146727)相互关联，并在[热力学极限](@entry_id:143061)下给出等价的宏观热力学性质。选择哪个系综，取决于哪个模型能最自然地反映实验或模拟所施加的物理约束。