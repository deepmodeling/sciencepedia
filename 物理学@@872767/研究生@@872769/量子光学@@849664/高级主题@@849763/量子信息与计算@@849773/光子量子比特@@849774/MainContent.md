## 引言
[光子](@entry_id:145192)，作为光的量子化基本单元，是构建未来[量子技术](@entry_id:142946)的关键构件之一。凭借其高速、低噪声的传播特性和丰富的可操控自由度，[光子](@entry_id:145192)[量子比特](@entry_id:137928)（photonic qubits）已成为量子光学和[量子信息科学](@entry_id:150091)领域的研究核心。它们不仅是探索量子力学基本奥秘的理想平台，也是将[量子优势](@entry_id:137414)转化为实用技术的关键媒介。然而，从抽象的[量子理论](@entry_id:145435)到稳定、可控的物理实现，需要克服诸如环境噪声、粒子损耗和生成过程不完美等一系列挑战。

本文旨在系统性地梳理[光子](@entry_id:145192)[量子比特](@entry_id:137928)的核心知识体系，为读者构建一个从基本原理到前沿应用的完整认知框架。文章将分为三个主要部分，引领读者逐步深入[光子](@entry_id:145192)[量子比特](@entry_id:137928)的世界。首先，在“原理与机制”一章中，我们将深入剖析[光子](@entry_id:145192)[量子比特](@entry_id:137928)的物理表示、生成方法、标志性的量子干涉行为以及不可避免的[退相干](@entry_id:145157)过程。接着，“应用与跨学科连接”一章将展示这些基本原理如何在[量子通信](@entry_id:138989)、[量子计算](@entry_id:142712)和[量子传感](@entry_id:138398)等领域催生革命性的技术，并揭示其与凝聚态物理等领域的深刻联系。最后，通过一系列精心设计的“动手实践”问题，读者将有机会运用所学知识解决具体问题，从而将理论理解转化为实践能力。

## 原理与机制

本章深入探讨构成[光子](@entry_id:145192)[量子比特](@entry_id:137928)研究核心的基本原理和物理机制。我们将从[光子](@entry_id:145192)[量子比特](@entry_id:137928)的物理实现方式入手，介绍其生成和表征的关键技术，剖析其独特的[量子干涉](@entry_id:139127)行为，并探讨其在验证量子力学基本原理（如非定域性）中的应用。最后，我们将分析在现实世界中影响[光子](@entry_id:145192)[量子比特](@entry_id:137928)性能的[退相干](@entry_id:145157)过程，并建立描述这些过程的数学框架。

### [光子](@entry_id:145192)[量子比特](@entry_id:137928)的表示：编码与[状态空间](@entry_id:177074)

[量子比特](@entry_id:137928)（qubit）是量子信息的基本单元，是一个双能级量子系统。对于[光子](@entry_id:145192)而言，其丰富的物理属性为实现[量子比特](@entry_id:137928)提供了多种途径，每种编码方案都有其独特的优势和挑战。

最直观的编码方式是**偏振编码**。利用[光子](@entry_id:145192)的横向[电场](@entry_id:194326)[振动](@entry_id:267781)方向，我们可以将水平[偏振态](@entry_id:175130)（Horizontal）和垂直偏振态（Vertical）定义为计算[基矢](@entry_id:199546)，分别记作 $|H\rangle$ 和 $|V\rangle$。任何[偏振态](@entry_id:175130)都可以表示为这两个[基矢](@entry_id:199546)的线性叠加，例如，对角[偏振态](@entry_id:175130)可以写作 $|\psi\rangle = \frac{1}{\sqrt{2}}(|H\rangle + |V\rangle)$。这种编码方式易于通过波片和偏振分束器等标准光学元件进行操控和测量。

另一种重要的编码方案是**路径编码**。在这种方案中，信息被编码在[光子](@entry_id:145192)所处的空间模式（例如，[光纤](@entry_id:273502)或[波导](@entry_id:198471)）中。一个常见的实现是**[双轨编码](@entry_id:167964) (dual-rail encoding)**，其中逻辑态 $|0\rangle_L$ 和 $|1\rangle_L$ 分别对应于单[光子](@entry_id:145192)存在于两个不同的空间模式（例如，路径 A 或路径 B）中。在双模[福克空间](@entry_id:143624) (two-mode Fock space) 中，这可以严谨地定义为 $|0\rangle_L \equiv |1\rangle_a |0\rangle_b$ 和 $|1\rangle_L \equiv |0\rangle_a |1\rangle_b$，其中 $|n\rangle_k$ 表示模式 $k$ 中有 $n$ 个[光子](@entry_id:145192) [@problem_id:708602] [@problem_id:708594]。马赫-曾德干涉仪（Mach-Zehnder interferometer）是实现对路径编码[量子比特](@entry_id:137928)进行任意幺正操作的典型物理系统。

单个[光子](@entry_id:145192)可以同时在多个自由度上携带量子信息，甚至在自身的多个自由度之间[形成纠缠](@entry_id:139137)，这种现象被称为**超纠缠 (hyperentanglement)**。考虑一个单[光子](@entry_id:145192)，其状态同时由其路径（$\mathcal{H}_P$，由路径 $|A\rangle$ 和 $|B\rangle$ 张成）和偏振（$\mathcal{H}_{pol}$，由 $|H\rangle$ 和 $|V\rangle$ 张成）共同描述。一个有趣的例子是如下的内部[纠缠态](@entry_id:152310) [@problem_id:708626]：
$$
|\psi\rangle = \frac{1}{\sqrt{2}} \left( \cos\theta |A\rangle|H\rangle + \sin\theta |A\rangle|V\rangle + \sin\theta |B\rangle|H\rangle + \cos\theta |B\rangle|V\rangle \right)
$$
在这个态中，我们无法为[光子](@entry_id:145192)的路径和偏振分别指定一个确定的[量子态](@entry_id:146142)；它们是相互纠缠的。为了量化这种内部纠缠的程度，我们可以考察其中一个子系统（例如路径）的混合度。为此，我们需要计算路径子系统的**[约化密度矩阵](@entry_id:146315) (reduced density matrix)** $\rho_P$，它通过在偏振自由度上对总系统的[密度矩阵](@entry_id:139892) $|\psi\rangle\langle\psi|$ 进行求迹 (trace) 得到：$\rho_P = \text{Tr}_{pol}(|\psi\rangle\langle\psi|)$。计算可得 $\rho_P$ 在 $\{|A\rangle, |B\rangle\}$ 基下的矩阵形式为：
$$
\rho_P = \begin{pmatrix} \frac{1}{2}  \sin\theta\cos\theta \\ \sin\theta\cos\theta  \frac{1}{2} \end{pmatrix}
$$
该[密度矩阵的本征值](@entry_id:204442)为 $\lambda_\pm = \frac{1 \pm \sin(2\theta)}{2}$。纠缠的程度可以通过**纠缠熵 (entropy of entanglement)** $S$ 来量化，其定义为子系统[约化密度矩阵](@entry_id:146315)的[冯·诺依曼熵](@entry_id:143216) (von Neumann entropy)：$S(\rho_P) = -\text{Tr}(\rho_P \log_2 \rho_P) = -\sum_i \lambda_i \log_2 \lambda_i$。对于此例，[纠缠熵](@entry_id:140818)为：
$$
S = -\frac{1+\sin(2\theta)}{2}\log_2\frac{1+\sin(2\theta)}{2} - \frac{1-\sin(2\theta)}{2}\log_2\frac{1-\sin(2\theta)}{2}
$$
这个结果表明，通过改变参数 $\theta$，我们可以连续地调控单个[光子](@entry_id:145192)内部自由度之间的纠缠程度。当 $\theta = \frac{\pi}{4}$ 时，$\sin(2\theta)=1$，此时 $\lambda_+=1, \lambda_-=0$，纠缠熵为0，态是路径与偏振的可分离态。当 $\theta=0$ 或 $\theta=\frac{\pi}{2}$ 时，$\sin(2\theta)=0$，此时 $\lambda_+=\lambda_-=1/2$，[纠缠熵](@entry_id:140818)达到最大值1，对应于最大[纠缠态](@entry_id:152310)。

### [光子](@entry_id:145192)[量子比特](@entry_id:137928)的产生：光源及其特性

可靠地按需生成单个[光子](@entry_id:145192)和[纠缠光子对](@entry_id:188235)是光量子技术的基石。**[自发参量下转换](@entry_id:162093) (Spontaneous Parametric Down-Conversion, SPDC)** 和 **自发[四波混频](@entry_id:164327) (Spontaneous Four-Wave Mixing, SFWM)** 是两种最主要的生成技术。在这些非线性光学过程中，一个或两个高能量的泵浦[光子](@entry_id:145192)被湮灭，同时产生一对低能量的信号 (signal) 和闲置 (idler) [光子](@entry_id:145192)。

在理想情况下，我们可以利用这些过程产生最大纠缠的[贝尔态](@entry_id:140749)。例如，在II型SPDC中，通过将泵浦激[光的偏振](@entry_id:262080)精确设置为对角方向，可以产生偏振纠缠态 $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|H_sV_i\rangle + |V_sH_i\rangle)$。然而，在实际实验中，泵浦激光的偏振可能存在不稳定性，例如其水平和垂直分量之间存在一个随机的相位涨落 $\delta$。这导致产生的[双光子](@entry_id:201392)态依赖于该涨落：$|\Psi(\delta)\rangle_{si} = \frac{1}{\sqrt{2}}(|H_sV_i\rangle + e^{i\delta}|V_sH_i\rangle)$。如果 $\delta$ 在实验测量时间内随机变化，那么我们实际得到的将是一个混合态，其[密度矩阵](@entry_id:139892) $\rho_{si}$ 是所有可能纯态的统计平均。假设 $\delta$ 服从零均值、标准差为 $\sigma_\delta$ 的高斯分布，通过对 $|\Psi(\delta)\rangle\langle\Psi(\delta)|$ 进行加权平均，我们可以计算出最终态的**纯度 (purity)** $\mathcal{P} = \text{Tr}(\rho_{si}^2)$，结果为 [@problem_id:708673]：
$$
\mathcal{P} = \frac{1 + e^{-\sigma_\delta^2}}{2}
$$
当涨落为零 ($\sigma_\delta=0$) 时，纯度为1，我们得到理想的纯[纠缠态](@entry_id:152310)。随着涨落增大，纯度下降，最终趋近于 $0.5$，表示态的[相干性](@entry_id:268953)严重退化。

除了[纠缠光子对](@entry_id:188235)外，通过探测[光子](@entry_id:145192)对中的一个[光子](@entry_id:145192)（例如闲置[光子](@entry_id:145192)）来预报另一个[光子](@entry_id:145192)（信号[光子](@entry_id:145192)）的存在，是制备**宣告式[单光子源](@entry_id:143467) (heralded single-photon source)** 的标准方法。这类光源的质量，特别是宣告出的单[光子](@entry_id:145192)的纯度，极大地依赖于[光子](@entry_id:145192)对的**联合谱振幅 (Joint Spectral Amplitude, JSA)** $f(\omega_s, \omega_i)$。JSA 描述了信号和闲置[光子](@entry_id:145192)频率之间的关联，其模平方 $|f(\omega_s, \omega_i)|^2$ 被称为**联合[谱强度](@entry_id:176230) (Joint Spectral Intensity, JSI)**。JSA 的形状由[能量守恒](@entry_id:140514)、动量守恒（相位匹配条件）以及施加在信号和闲置光路上的任何光[谱滤波](@entry_id:755173)共同决定。在一个典型的SFWM设置中，JSA可以近似建模为泵浦场[光谱](@entry_id:185632)包络、信号光滤波器和闲置光滤波器的乘积 [@problem_id:708754]。例如，若泵浦、信号和闲置滤波器均具有高斯型[光谱](@entry_id:185632)，其带宽分别为 $\sigma_p, \sigma_s, \sigma_i$，则JSI可以表示为频率[失谐](@entry_id:148084) $\delta_s = \omega_s - \omega_{s0}$ 和 $\delta_i = \omega_i - \omega_{i0}$ 的函数。若闲置光滤波器中心频率有 $\Delta$ 的偏移，则JSI为：
$$
I(\delta_s, \delta_i) = \exp\left(-\frac{(\delta_s+\delta_i)^2}{\sigma_p^2}-\frac{\delta_s^2}{\sigma_s^2}-\frac{(\delta_i-\Delta)^2}{\sigma_i^2}\right)
$$
这个表达式直观地展示了如何通过工程设计（选择泵浦带宽和滤波器参数）来塑造[光子](@entry_id:145192)对的谱关联特性。

为了更深刻地理解谱关联及其对宣告单[光子](@entry_id:145192)纯度的影响，我们可以使用**[施密特分解](@entry_id:145934) (Schmidt decomposition)** 将JSA展开：
$$
f(\omega_s, \omega_i) = \sum_{k=1}^{\infty} \sqrt{\lambda_k} \phi_k(\omega_s) \psi_k(\omega_i)
$$
其中 $\{\phi_k\}$ 和 $\{\psi_k\}$ 是信号和闲置[光子](@entry_id:145192)各自的正交归一的施密特模式（Schmidt modes），$\lambda_k$ 是非负的[施密特系数](@entry_id:137823)，满足 $\sum_k \lambda_k = 1$。[双光子](@entry_id:201392)态的谱纠缠程度可以通过**[施密特数](@entry_id:141441) (Schmidt number)** $K$ 来量化，其定义为 $K = (\sum_k \lambda_k^2)^{-1}$。$K=1$ 表示谱是可分离的（无纠缠），$K1$ 表示存在谱纠缠。宣告出的信号[光子](@entry_id:145192)的状态由[约化密度矩阵](@entry_id:146315) $\rho_s = \text{Tr}_i(|\Psi\rangle\langle\Psi|)$ 描述，其纯度 $\mathcal{P} = \text{Tr}(\rho_s^2)$ 与[施密特数](@entry_id:141441)之间存在一个简洁而深刻的关系 [@problem_id:708615]：
$$
\mathcal{P} = \frac{1}{K}
$$
这个关系式揭示了一个核心原理：[双光子](@entry_id:201392)源的谱纠缠度（由 $K$ 量化）直接决定了宣告[单光子源](@entry_id:143467)的纯度（由 $\mathcal{P}$ 量化）。为了获得高纯度的单[光子](@entry_id:145192)（$\mathcal{P} \to 1$），必须设计光源使其JSA是谱可分离的（$K \to 1$）。

### [量子干涉](@entry_id:139127)：[光子](@entry_id:145192)[量子比特](@entry_id:137928)的标志

[量子干涉](@entry_id:139127)，特别是多[光子](@entry_id:145192)干涉，是量子光学区别于经典光学的标志性现象。其中最著名的例子是**洪-欧-曼德尔 (Hong-Ou-Mandel, HOM) 效应**。当两个完全不可区分的单[光子](@entry_id:145192)同时从不同输入端口进入一个50:50的平衡[分束器](@entry_id:145251)时，量子力学预言这两个[光子](@entry_id:145192)将永远从同一个输出端口出来，这种现象称为“聚束 (bunching)”。在输出两端同时探测到[光子](@entry_id:145192)的符合计数将降为零，形成所谓的“HOM dip”。

这一效应可以推广到更一般的情况，例如使用一个功率[反射率](@entry_id:155393)为 $R$、透射率为 $T$（$R+T=1$）的非平衡[分束器](@entry_id:145251) [@problem_id:708832]。[分束器](@entry_id:145251)对输入模式算符的变换关系为 $\hat{b}_1 = \sqrt{T}\hat{a}_1 + i\sqrt{R}\hat{a}_2$ 和 $\hat{b}_2 = i\sqrt{R}\hat{a}_1 + \sqrt{T}\hat{a}_2$。对于[不可区分光子](@entry_id:192605)输入态 $|\psi_{in}\rangle = \hat{a}_1^\dagger \hat{a}_2^\dagger |0,0\rangle$，输出态中两[光子](@entry_id:145192)分别在不同输出端口的振幅为 $(T-R)$。因此，符合探测概率为 $P_c(0) = (T-R)^2$。相比之下，如果两个[光子](@entry_id:145192)是可区分的（例如到达时间相差很大），则干涉消失，总的符合概率是两条经典路径概率之和，$P_c(\infty) = R^2 + T^2$。HOM干涉的**可见度 (visibility)** $V$ 定义为 $V = \frac{P_c(\infty) - P_c(0)}{P_c(\infty)}$（在分母为$P_c(\infty)$的定义下）。更标准的定义为 $V = \frac{P_c(\infty) - P_c(0)}{P_c(\infty) + P_c(0)}$，其结果为：
$$
V = \frac{R(1-R)}{1-3R+3R^2}
$$
可见，只有在 $R=T=0.5$ 的平衡[分束器](@entry_id:145251)情况下，$(T-R)^2=0$，才能观察到完美的符合计数相消，即 $V=1$ (在$V = 1-P_c(0)/P_c(\infty)$定义下)。

[光子](@entry_id:145192)的可区分性会抑制甚至完全破坏HOM干涉。一个经典的例子是，当两个[光子](@entry_id:145192)具有可区分的[偏振态](@entry_id:175130)时，例如一个 $|H\rangle$ [偏振光](@entry_id:273160)子和一个 $|V\rangle$ 偏振光子同时进入一个50:50[分束器](@entry_id:145251)的不同端口 [@problem_id:708639]。由于偏振提供了“路径”信息（原则上可以判断哪个[光子](@entry_id:145192)来自哪个输入端口），HOM干涉消失了。然而，有趣的是，通过在输出端进行巧妙的测量，我们可以“擦除”这些区分信息，从而恢复干涉。如果在输出端口 c 和 d 分别放置偏振方向为 $+\theta$ 和 $-\theta$ 的检偏器，然后测量符合计数，我们发现符合探测的概率为：
$$
P_{coin} = \frac{1}{4}\sin^2(2\theta)
$$
这个结果表明，尽管输入[光子](@entry_id:145192)是可区分的，但在特定的投影测量基下，[量子干涉](@entry_id:139127)得以重现。当 $\theta = 0$ 或 $\pi/2$ 时，检偏器与输入偏振对齐，没有不确定性，符合概率为零。当 $\theta = \pi/4$ 时，检偏器设置在对角基，使得我们无法从探测结果中判断[光子](@entry_id:145192)的原始偏振，此时干涉效应最强，符合概率达到最大值 $1/4$。这一现象是**量子擦除 (quantum erasure)** 的一个精妙例证。

### 纠缠与[非定域性](@entry_id:140165)：探测量子基础

利用[光子](@entry_id:145192)[量子比特](@entry_id:137928)产生的纠缠对是检验量子力学基本原理、特别是**[贝尔定理](@entry_id:141056) (Bell's theorem)** 的理想平台。[贝尔定理](@entry_id:141056)指出，任何遵从[定域实在论](@entry_id:144981) (local realism) 的理论对[纠缠粒子](@entry_id:153691)测量结果的关联程度都有一个上限，而量子力学预言的关联可以超越这个上限。

**[CHSH不等式](@entry_id:138761)**是[贝尔不等式](@entry_id:156237)的一个实验友好版本。在典型的CHSH实验中，Alice和Bob共享大量处于最大纠缠态（如单态 $|\Psi^-\rangle = \frac{1}{\sqrt{2}}(|HV\rangle - |VH\rangle)$）的[光子](@entry_id:145192)对。他们各自独立地选择测量设置（对[光子](@entry_id:145192)进行偏振测量的角度，$a$ 或 $a'$ for Alice, $b$ 或 $b'$ for Bob），并计算关联量 $S = E(a, b) + E(a, b') + E(a', b) - E(a', b')$，其中 $E(a, b)$ 是他们在各自设定下测量结果的关联[期望值](@entry_id:153208)。[定域实在论](@entry_id:144981)要求 $|S| \le 2$，而量子力学预言，对于 $|\Psi^-\rangle$ 态，关联函数为 $E(a,b) = -\cos(2(a-b))$，通过巧妙地选择测量角度（例如，$a=0, a'=\pi/4, b=\pi/8, b'=-\pi/8$），$|S|$ 的最大值可以达到 $2\sqrt{2} \approx 2.828$，即所谓的**齐雷尔松界 (Tsirelson's bound)**，这显著地违背了[贝尔不等式](@entry_id:156237)。

在真实的实验中，各种噪声和不完美性会削弱观测到的[量子关联](@entry_id:136327)。例如，假设Bob的测量装置存在一个随机的角度误差 $\delta$，该误差服从某个[概率分布](@entry_id:146404) $p(\delta)$ [@problem_id:708640]。实验测得的关联函数 $\bar{E}(a,b)$ 实际上是理想关联函数在所有可能误差上的平均值。如果角度误差 $\delta$ 服从最大角展宽为 $\Delta_0$ 的对称三角分布，那么平均后的关联函数会受到一个衰减因子的影响：
$$
\bar{E}(a,b) = -\left(\frac{\sin\Delta_0}{\Delta_0}\right)^2 \cos(2(a-b))
$$
因此，在这种[噪声模型](@entry_id:752540)下，CHSH参量的最大值被降低为：
$$
|\bar{S}|_{max} = 2\sqrt{2} \left(\frac{\sin\Delta_0}{\Delta_0}\right)^2
$$
这个结果定量地描述了[测量误差](@entry_id:270998)如何降低[贝尔不等式的违背](@entry_id:202735)程度。随着误差范围 $\Delta_0$ 的增加，衰减因子迅速减小，当噪声足够大时，$|\bar{S}|_{max}$ 可能会降到2以下，使得实验结果无法再排除[定域实在论](@entry_id:144981)。

### 退相干与[量子信道](@entry_id:145403)：[光子](@entry_id:145192)[量子比特](@entry_id:137928)的宿命

[量子态](@entry_id:146142)是脆弱的，与环境的任何不期望的相互作用都会导致[量子信息](@entry_id:137721)的损失，这一过程称为**[退相干](@entry_id:145157) (decoherence)**。退相干将纯态转变为混合态，并破坏量子叠加和纠缠。描述这种演化的数学工具是**量子信道 (quantum channel)**，也称为完全正定保迹 (CPTP) 映射。

一个[量子信道](@entry_id:145403) $\mathcal{E}$ 对密度矩阵 $\rho$ 的作用可以通过**[算符和表示](@entry_id:140073) (operator-sum representation)** 来描述，$\mathcal{E}(\rho) = \sum_k E_k \rho E_k^\dagger$，其中 $\{E_k\}$ 被称为**[克劳斯算符](@entry_id:144882) (Kraus operators)**，满足 $\sum_k E_k^\dagger E_k = I$（对于[保迹映射](@entry_id:146926)）。

对于[光子](@entry_id:145192)[量子比特](@entry_id:137928)，最主要的两种[退相干](@entry_id:145157)机制是[光子](@entry_id:145192)损耗和相位[抖动](@entry_id:200248)。

**幅度阻尼信道 (Amplitude Damping Channel, ADC)** 是描述[光子](@entry_id:145192)损耗的典型模型。它描述了[激发态](@entry_id:261453) $|1\rangle$ 以概率 $\gamma$ 衰减到[基态](@entry_id:150928) $|0\rangle$ 的过程。其[克劳斯算符](@entry_id:144882)为 [@problem_id:708593]：
$$
E_0 = \begin{pmatrix} 1  0 \\ 0  \sqrt{1-\gamma} \end{pmatrix}, \quad E_1 = \begin{pmatrix} 0  \sqrt{\gamma} \\ 0  0 \end{pmatrix}
$$
当一个[纠缠对](@entry_id:160576)中的一个[光子](@entry_id:145192)（比如B）经过这样一个损耗信道时，整个系统的纠缠会降低。对于初始处于 $|\Psi^-\rangle$ 态的系统，如果[光子](@entry_id:145192)B经历损耗概率为 $\gamma$ 的ADC，那么末态的纠缠度可以用**并发度 (Concurrence)** $C$ 来衡量。计算表明，并发度从初始值1衰减为 [@problem_id:708593]：
$$
C(\rho_{out}) = \sqrt{1-\gamma}
$$
这清晰地展示了粒子数不守恒的损耗过程是如何破坏纠缠的。对于[双轨编码](@entry_id:167964)的[量子比特](@entry_id:137928)，其中一个路径（例如模式'b'）的损耗不仅会降低相干性，还会导致**[泄漏误差](@entry_id:146224) (leakage error)**，即将逻辑态 $|1\rangle_L$ 变为非逻辑态（真空态 $|0\rangle_a|0\rangle_b$）[@problem_id:708602]。在这种情况下，我们可以通过将信道作用结果投影回逻辑[子空间](@entry_id:150286)来定义一个**有效信道** $\tilde{\mathcal{E}}$。该有效信道与理想恒等信道的接近程度可以用**过程保真度 (process fidelity)** $F_{pro}$ 来衡量。对于模式'b'存在损耗的有效信道，其过程保真度为：
$$
F_{pro} = \frac{1}{4}\left(1+\sqrt{1-\gamma}\right)^2
$$

**退相位信道 (Dephasing Channel)** 描述了[量子态](@entry_id:146142)不同分量之间相对相位的随机化过程，而不改变各分量的布居数。对于路径编码的[量子比特](@entry_id:137928)，例如在马赫-曾德干涉仪中，一个臂的光程长度因热涨落而随机变化，就会引入一个随机相位 $\phi$。这个过程可以用一个幺正变换 $U(\phi) = |0\rangle\langle 0| + e^{i\phi}|1\rangle\langle 1|$ 来描述。如果 $\phi$ 服从零均值、标准差为 $\sigma_\phi$ 的高斯分布，那么平均效应就是一个退相位信道 [@problem_id:708594]。

为了完整地表征一个[量子信道](@entry_id:145403) $\mathcal{E}$，我们可以利用**崔-雅米奥科夫斯基同构 (Choi-Jamiolkowski isomorphism)**，它将一个作用于 $\mathcal{H}$ 的信道 $\mathcal{E}$ 映射到一个定义在 $\mathcal{H} \otimes \mathcal{H}$ 上的态，即**过程矩阵 (process matrix)** 或**崔矩阵 (Choi matrix)** $\chi_\mathcal{E}$：
$$
\chi_\mathcal{E} = (I \otimes \mathcal{E})(|\Phi^+\rangle\langle\Phi^+|)
$$
其中 $I$ 是恒等映射，$|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$ 是一个最大[纠缠态](@entry_id:152310)。$\chi_\mathcal{E}$ 包含了关于信道 $\mathcal{E}$ 的所有信息。例如，对于上述由高斯[相位噪声](@entry_id:264787)引起的退相位信道，我们可以计算其过程矩阵的非对角元。在计算基 $\{|00\rangle, |01\rangle, |10\rangle, |11\rangle\}$ 下，[矩阵元](@entry_id:186505) $\chi_{14}$（第一行第四列）的值为 [@problem_id:708594]：
$$
\chi_{14} = \frac{1}{2}\exp\left(-\frac{\sigma_\phi^2}{2}\right)
$$
这个矩阵元直接关联于信道的相干保持能力。当[相位噪声](@entry_id:264787)为零（$\sigma_\phi=0$）时，$\chi_{14}=1/2$，对应于理想的恒等信道。随着噪声增强，该值指数衰减至零，表明信道完全破坏了[相干性](@entry_id:268953)。通过测量过程矩阵的所有元素，我们可以对未知的量子过程进行完整的层析 (tomography)，这对于校准和验证量子设备至关重要。