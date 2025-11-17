## 引言
自2012年在欧洲[核子](@entry_id:158389)研究中心（CERN）的[大型强子对撞机（LHC）](@entry_id:158177)上被发现以来，[希格斯玻色子](@entry_id:155560)一直是[粒子物理学](@entry_id:145253)研究的核心。作为标准模型中唯一的基本标量粒子，它通过[希格斯机制](@entry_id:144416)赋予了基本[粒子质量](@entry_id:156313)，完成了标准模型的最后一块拼图。然而，希格斯玻色子的发现并非终点，而是开启了一个全新精确探索时代的大门。当前研究的重点已从“寻找”转向“理解”：它的性质是否与标准模型的预言完全一致？它是否是通往[超越标准模型](@entry_id:161067)（BSM）新物理世界的窗口？

为了回答这些问题，我们必须深入理解希格斯玻色子在[对撞机](@entry_id:192770)上产生和衰变的具体物理过程。本文旨在系统性地阐述这些核心机制及其在前沿物理研究中的应用。读者将通过三个章节的学习，建立一个从基础理论到实际应用的完整知识框架。第一章“原理与机制”将详细介绍希格斯玻色子与标准模型其他粒子的[基本相互作用](@entry_id:749649)，包括树平面耦合和关键的圈图诱导耦合，并构建在对撞机环境中进行精确计算的理论基础。第二章“应用与跨学科联系”将展示如何利用这些原理作为精密工具，来检验标准模型、探测[希格斯玻色子](@entry_id:155560)的内禀属性，并寻找[超对称](@entry_id:155777)等新物理现象。最后，第三章“动手实践”提供了一系列计算问题，旨在帮助读者巩固理论知识并将其付诸实践。

现在，让我们首先进入第一章，深入探讨[希格斯玻色子](@entry_id:155560)产生与衰变的物理原理与核心机制。

## 原理与机制

在介绍性章节之后，我们现在深入探讨[希格斯玻色子](@entry_id:155560)在[对撞机](@entry_id:192770)上产生和衰变的具体物理原理与核心机制。本章将系统地阐述[希格斯玻色子](@entry_id:155560)与标准模型中其他粒子的相互作用，包括树平面耦合和更高阶的[圈图](@entry_id:149287)诱导耦合。我们将在此基础上，构建在强子[对撞机](@entry_id:192770)环境中进行精确计算和现象学预测的理论框架。

### [希格斯玻色子](@entry_id:155560)的[基本相互作用](@entry_id:749649)

[希格斯机制](@entry_id:144416)的核心在于赋予基本粒子质量。这通过[希格斯场](@entry_id:160081)与这些粒子场的直接耦合来实现。在[电弱对称性](@entry_id:149377)自发破缺后，这些耦合表现为物理希格斯玻色子 $H$ 与[费米子](@entry_id:146235)和规范玻色子之间的相互作用顶点。

#### 与物质[费米子](@entry_id:146235)的耦合

[希格斯玻色子](@entry_id:155560)通过汤川（Yukawa）相互作用将其质量赋予[费米子](@entry_id:146235)（夸克和带电轻子）。对于质量为 $m_f$ 的[费米子](@entry_id:146235) $f$，其与希格斯玻色子 $H$ 的相互作用拉格朗日量为：
$$
\mathcal{L}_{\text{Yukawa}} = - \frac{m_f}{v} H \bar{f} f
$$
其中 $v$ 是希格斯场的[真空期望值](@entry_id:146340)（VEV），其值约为 $246 \, \text{GeV}$。这个表达式揭示了一个关键特征：**希格斯[玻色子与[费米](@entry_id:147957)子](@entry_id:146235)的耦合强度正比于[费米子](@entry_id:146235)的质量**。这解释了为何顶夸克（top quark）与希格斯玻色子的相互作用最强，而[希格斯玻色子衰变](@entry_id:158388)到底夸克（bottom quark）对 ($H \to b\bar{b}$) 的分支比远大于其到更轻[费米子](@entry_id:146235)的衰变。

在领头阶（Leading Order, LO），$H \to b\bar{b}$ 衰变的偏[衰变宽度](@entry_id:153846) $\Gamma_{\text{LO}}$ 可以直接从上述[汤川耦合](@entry_id:154951)计算得出。其结果为：
$$
\Gamma_{\text{LO}}(H \to b\bar{b}) = \frac{N_c G_F m_H m_b^2}{4\pi\sqrt{2}} \left(1 - \frac{4m_b^2}{m_H^2}\right)^{3/2}
$$
其中 $N_c=3$ 是夸克的[色荷](@entry_id:151924)数，$G_F$ 是费米常数，$m_H$ 和 $m_b$ 分别是[希格斯玻色子](@entry_id:155560)和底夸克的质量。因子 $\beta = \sqrt{1 - 4m_b^2/m_H^2}$ 是末态夸克在希格斯静止系中的速度，其 $3/2$ 次方来自于相空间和[矩阵元](@entry_id:186505)的组合。

然而，精确的理论预测必须包含量子色动力学（QCD）的[辐射修正](@entry_id:157711)。在次领头阶（Next-to-Leading Order, NLO），出射的 $b\bar{b}$ 对可以辐射出一个胶子。这些修正通常表示为一个修正因子。在 $m_H \gg m_b$ 的极限下（这是一个很好的近似），NLO QCD 修正项 $\delta_{\text{NLO}}$ 为：
$$
\delta_{\text{NLO}} = \frac{17}{3} C_F \frac{\alpha_s(\mu_R)}{\pi}
$$
其中 $C_F = (N_c^2-1)/(2N_c) = 4/3$ 是SU(3)群[基本表示](@entry_id:157678)的二次卡西米尔（Casimir）[不变量](@entry_id:148850)，$\alpha_s(\mu_R)$ 是在[重整化标度](@entry_id:153146) $\mu_R$ 下的[强耦合常数](@entry_id:159543)，通常选取 $\mu_R = m_H$。将此修正因子应用于领头阶的计算，我们得到一个更精确的NLO[衰变宽度](@entry_id:153846) [@problem_id:183044]：
$$
\Gamma_{\text{NLO}}(H \to b\bar{b}) = \Gamma_{\text{LO}}(H \to b\bar{b}) \left(1 + \delta_{\text{NLO}}\right) = \frac{N_c G_F m_H m_b^2}{4\pi\sqrt{2}}\left(1 - \frac{4m_b^2}{m_H^2}\right)^{3/2} \left(1 + \frac{17}{3} C_F \frac{\alpha_s(m_H)}{\pi}\right)
$$
这个例子展示了如何结合基本耦合与高阶修正来获得精确的物理预测。

#### 与[规范玻色子](@entry_id:200257)的耦合

希格斯机制同样赋予了 $W$ 和 $Z$ [规范玻色子质量](@entry_id:147712)。与[费米子](@entry_id:146235)不同，希格斯玻色子与这些[玻色子](@entry_id:138266)的[耦合强度](@entry_id:275517)正比于它们质量的平方 ($m_V^2$)。相关的相互作用顶点，例如 $HZZ$ 顶点，由拉格朗日量中的动能项 $(D_\mu H)^\dagger (D^\mu H)$ 产生，其 Feynman 规则为：
$$
\mathcal{V}^{\mu\nu}_{HZZ} = i \frac{2 m_Z^2}{v} g^{\mu\nu}
$$
这导致了[希格斯玻色子](@entry_id:155560)可以衰变为一对 $W$ 或 $Z$ [玻色子](@entry_id:138266)（如果[运动学](@entry_id:173318)允许，即 $m_H > 2m_V$）。一个深刻的物理现象出现在对这些末态矢量[玻色子](@entry_id:138266)极化状态的研究中。有质量的矢量[玻色子](@entry_id:138266)有三个极化态：两个横向极化态（transverse, $V_T$）和一个[纵向极化](@entry_id:202391)态（longitudinal, $V_L$）。

[纵向极化](@entry_id:202391)矢量与[玻色子](@entry_id:138266)的动量方向相关，在高能极限下，$p^\mu = (E, 0, 0, p_z)$，其[极化矢量](@entry_id:269389) $\epsilon_L^\mu$ 近似为 $p^\mu/m_V$。这种行为与[电弱对称性破缺](@entry_id:161363)的本质紧密相连：纵向分量实际上是[希格斯机制](@entry_id:144416)“吃掉”的[戈德斯通玻色子](@entry_id:156185)（Goldstone boson）的“残余”。因此，涉及纵向矢量[玻色子](@entry_id:138266)的相互作用在高能下表现出独特性质。

考虑 $H \to ZZ$ 衰变，我们可以分别计算其衰变为两对[纵向极化](@entry_id:202391) $Z_L$ [玻色子](@entry_id:138266)和两对横向极化 $Z_T$ [玻色子](@entry_id:138266)的振幅。利用 $HZZ$ 顶点规则和 $Z$ [玻色子](@entry_id:138266)在希格斯静止系中的[极化矢量](@entry_id:269389)，可以计算出相应的[衰变宽度](@entry_id:153846)。结果表明，衰变到纵向模式的振幅平方 $| \mathcal{M}(H \to Z_L Z_L) |^2$ 与衰变到[横向模式](@entry_id:163265)的振幅平方 $| \mathcal{M}(H \to Z_T Z_T) |^2$ 的比值强烈依赖于希格斯质量 [@problem_id:183029]：
$$
\mathcal{R} = \frac{\Gamma(H \to Z_L Z_L)}{\Gamma(H \to Z_T Z_T)} = \frac{|\mathcal{M}_L|^2}{\sum_T|\mathcal{M}_T|^2} = \frac{(m_H^2 - 2m_Z^2)^2}{8m_Z^4}
$$
在 $m_H \gg m_Z$ 的高能极限下，这个比值近似为 $\mathcal{R} \approx \frac{m_H^4}{8m_Z^4}$。这表明**在高能量下，[希格斯玻色子](@entry_id:155560)压倒性地倾向于衰变为[纵向极化](@entry_id:202391)的矢量[玻色子](@entry_id:138266)**。这一现象是[戈德斯通玻色子等效定理](@entry_id:157742)的直接体现，我们将在稍后详细讨论。

#### [希格斯玻色子](@entry_id:155560)的自相互作用

希格斯势 $V(H) = -\mu_H^2 (H^\dagger H) + \lambda (H^\dagger H)^2$ 不仅导致了[电弱对称性破缺](@entry_id:161363)，还预言了[希格斯玻色子](@entry_id:155560)自身的相互作用。将[希格斯场](@entry_id:160081)在[真空期望值](@entry_id:146340) $v$ 附近展开，$H = \frac{1}{\sqrt{2}} \begin{pmatrix} 0 \\ v+h \end{pmatrix}$，势能项会产生包含物理[希格斯场](@entry_id:160081) $h$ 的三线性和四线性相互作用项：
$$
\mathcal{L}_{HHH} = - \frac{1}{3!} \lambda_{HHH} h^3 \quad \text{and} \quad \mathcal{L}_{HHHH} = - \frac{1}{4!} \lambda_{HHHH} h^4
$$
在标准模型中，这些自[耦合常数](@entry_id:747980)由希格斯质量 $m_H$ 和[真空期望值](@entry_id:146340) $v$ 完全确定：$\lambda_{HHH}^{\text{SM}} = \frac{3m_H^2}{v}$ 和 $\lambda_{HHHH}^{\text{SM}} = \frac{3m_H^2}{v^2}$。实验上测量这些自耦合，特别是三线性耦合 $\lambda_{HHH}$，是检验[希格斯机制](@entry_id:144416)和寻找新物理的关键。对 $\lambda_{HHH}$ 最直接的探测来自于双[希格斯玻色子](@entry_id:155560) ($HH$) 的产生过程。

### [圈图](@entry_id:149287)诱导的相互作用

[标准模型拉格朗日量](@entry_id:150338)中没有[希格斯玻色子](@entry_id:155560)与胶子或[光子](@entry_id:145192)这些无质量[规范玻色子](@entry_id:200257)的直接（树平面）耦合。然而，这种相互作用可以通过包含虚粒子（virtual particles）的量子[圈图](@entry_id:149287)（loop diagrams）产生。

#### 有效 $Hgg$ 耦合

在[强子](@entry_id:158325)[对撞机](@entry_id:192770)（如LHC）上，希格斯玻色子的主要产生机制是胶子融合（gluon-gluon fusion），即 $gg \to H$。这个过程由一个夸克圈图介导，其中耦合最强的顶夸克圈的贡献占主导。当希格斯玻色子的质量远小于两倍[顶夸克质量](@entry_id:160842)（$m_H \ll 2m_t$）时，我们可以采用有效场论（Effective Field Theory, EFT）的方法。通过“积分掉”（integrating out）重的顶夸克，其效应被一个局域的[有效算符](@entry_id:183730)所描述：
$$
\mathcal{L}_{\text{eff}} \supset C_{ggH} H \, G_{\mu\nu}^a G^{a, \mu\nu}
$$
其中 $G_{\mu\nu}^a$ 是胶子[场强张量](@entry_id:159746)，$C_{ggH}$ 是一个有效[耦合系数](@entry_id:273384)。这个有效顶点描述了两个胶子如何“融合”成一个希格斯玻色子。

利用这个有效顶点，我们可以计算 $gg \to H$ 的部分子[截面](@entry_id:154995) $\hat{\sigma}(gg \to H)$。由于这是一个 $2 \to 1$ 的共振过程，其[截面](@entry_id:154995)形式为：
$$
\hat{\sigma}(gg \to H) = K \cdot \delta(\hat{s} - m_H^2)
$$
其中 $\hat{s}$ 是[部分子](@entry_id:160627)[质心能量](@entry_id:265852)的平方。有趣的是，通过 crossing symmetry，同一个有效顶点也描述了[希格斯玻色子衰变](@entry_id:158388)为两个胶子的过程 $H \to gg$。其[衰变宽度](@entry_id:153846) $\Gamma(H \to gg)$ 与产生过程的系数 $K$ 之间存在一个普适的、不依赖于有效耦合具体值的关系 [@problem_id:182527]。经过计算可以发现：
$$
K = \frac{\pi^2}{8m_H} \Gamma(H \to gg)
$$
这个关系式连接了两个表面上不同的物理过程，展示了[量子场论](@entry_id:138177)内在结构的深刻一致性。

#### $H\gamma\gamma$ 耦合与[形状因子](@entry_id:152312)

[希格斯玻色子衰变](@entry_id:158388)为两个[光子](@entry_id:145192)（$H \to \gamma\gamma$）是其最重要的发现和研究渠道之一。与 $Hgg$ 耦合类似，由于[光子](@entry_id:145192)不带[电荷](@entry_id:275494)且无质量，这个过程也必须通过圈图发生。任何带[电荷](@entry_id:275494)且与希格斯有耦合的粒子原则上都可以对这个[圈图](@entry_id:149287)做出贡献。在标准模型中，贡献最大的是 $W$ [玻色子](@entry_id:138266)圈和顶夸克圈。

总衰变振幅是这两个贡献的[相干叠加](@entry_id:170209)：$\mathcal{A}_{\text{tot}} = \mathcal{A}_W + \mathcal{A}_t$。每个振幅都可以写成一个共同的[运动学](@entry_id:173318)因子乘以一个依赖于圈中[粒子质量](@entry_id:156313)的无量纲函数，即**[形状因子](@entry_id:152312)**（form factor）。对于自旋为1的 $W$ [玻色子](@entry_id:138266)和自旋为1/2的顶夸克，其振幅分别为：
$$
\mathcal{A}_W \propto A_1(\tau_W) \quad \text{and} \quad \mathcal{A}_t \propto N_c Q_t^2 A_{1/2}(\tau_t)
$$
其中 $N_c=3$ 是夸克[色荷](@entry_id:151924)数，$Q_t=2/3$ 是顶夸克的[电荷](@entry_id:275494)。形状因子 $A_1$ 和 $A_{1/2}$ 是变量 $\tau_i = m_H^2 / (4m_i^2)$ 的函数。

在标准模型中，$m_H \approx 125 \, \text{GeV}$，我们有 $m_H  2m_W$ 和 $m_H  2m_t$，因此 $\tau_W  1$ 且 $\tau_t  1$。一个重要的计算练习是考虑[顶夸克质量](@entry_id:160842)趋于无穷大的极限 ($m_t \to \infty$)，这对应于 $\tau_t \to 0$ [@problem_id:183040]。通过对 $A_{1/2}(\tau_t)$ 进行泰勒展开，可以得到 $\lim_{\tau_t \to 0} A_{1/2}(\tau_t) = 4/3$。这个极限值是一个常数，与顶夸克[有效场论](@entry_id:145328)的结果一致。

利用这个结果，我们可以计算 $W$ 圈和顶夸克圈振幅之比：
$$
\mathcal{R} = \frac{\mathcal{A}_W}{\mathcal{A}_t} = \frac{A_1(\tau_W)}{N_c Q_t^2 A_{1/2}(\tau_t)} \xrightarrow{m_t \to \infty} \frac{A_1(\tau_W)}{N_c Q_t^2 (4/3)}
$$
将 $A_1(\tau_W)$ 的具体表达式代入，可以得到一个精确的数值。在物理上，$\mathcal{A}_W$ 的符号为负，而 $\mathcal{A}_t$ 的符号为正。这意味着在标准模型中，**$W$ [玻色子](@entry_id:138266)圈和顶夸克圈的贡献发生相消干涉**，这显著地减小了 $H \to \gamma\gamma$ 的总[衰变宽度](@entry_id:153846)。这种精妙的相消是标准模型的一个非凡预言，对它的精确测量可以灵敏地探测到任何可能破坏这种平衡的新物理粒子圈的贡献。

#### CP性质与螺旋度选择定則

[有效场论](@entry_id:145328)不仅简化了计算，还揭示了深刻的对称性原理。考虑胶子融合产生一个标量粒子，这个粒子的 CP 性质（CP-even 或 CP-odd）会对其产生过程中的胶子螺旋度组合施加严格的[选择定则](@entry_id:140784)。

一个 CP-偶（CP-even）标量 $H$（如标准模型希格斯）与胶子的有效相互作用由算符 $G_{\mu\nu}^a G^{a, \mu\nu}$ 描述。一个 CP-奇（CP-odd）[赝标量](@entry_id:196696) $A$ 的相互作用则由 $G_{\mu\nu}^a \tilde{G}^{a, \mu\nu}$ 描述，其中 $\tilde{G}^{a, \mu\nu} = \frac{1}{2} \epsilon^{\mu\nu\rho\sigma} G_{\rho\sigma}^a$ 是对偶[场强张量](@entry_id:159746)。

在部分子[质心系](@entry_id:168444)中，可以证明算符 $G \cdot G$ 只会连接相反螺旋度的胶子 ($g_+ g_-$ 或 $g_- g_+$)，而 $G \cdot \tilde{G}$ 只会连接相同螺旋度的胶子 ($g_+ g_+$ 或 $g_- g_-$)。因此，我们得到一个强大的**螺旋度[选择定则](@entry_id:140784)** [@problem_id:182999]：
*   **CP-even 标量 $H$：仅由相反螺旋度的胶子产生，$\mathcal{M}(g_+ g_+ \to H) = \mathcal{M}(g_- g_- \to H) = 0$。**
*   **CP-odd 标量 $A$：仅由相同螺旋度的胶子产生，$\mathcal{M}(g_+ g_- \to A) = \mathcal{M}(g_- g_+ \to A) = 0$。**

更有趣的是，对于质量相同的 CP-even 和 CP-odd 标量，其非零产生振幅的模平方是相等的：
$$
|\mathcal{M}(g_+ g_+ \to A)|^2 = |\mathcal{M}(g_+ g_- \to H)|^2
$$
这个比值仅取决于各自有效[耦合系数](@entry_id:273384)的平方，$|C_A|^2/|C_H|^2$。因此，通过测量末态粒子的[角分布](@entry_id:193827)（这与初态胶子的螺旋度相关），原则上可以直接确定[希格斯玻色子](@entry_id:155560)的 CP 性质。

### 强子对撞机上的希格斯物理

我们将上述基本原理应用于质子-质子（pp）碰撞的现实环境中，这需要将部分子层面的计算与[质子结构](@entry_id:155603)和末态粒子的实验特征相结合。

#### 产生[截面](@entry_id:154995)与[部分子模型](@entry_id:155691)

在[强子](@entry_id:158325)对撞机上，我们碰撞的是质子，它们是夸克和胶子的束缚态。[部分子模型](@entry_id:155691)（Parton Model）允许我们将一个高能[强子](@entry_id:158325)反应“[因子分解](@entry_id:150389)”为一个[部分子](@entry_id:160627)层面的散射过程与描述[部分子](@entry_id:160627)在质子中[动量分布](@entry_id:162113)的**[部分子分布函数](@entry_id:156490)**（Parton Distribution Functions, PDFs）的卷积。

对于 $gg \to H$ 过程，产生一个质量为 $m_H$、[快度](@entry_id:265131)为 $y_H$ 的希格斯玻色子的[微分截面](@entry_id:137333)可以写为 [@problem_id:183038]：
$$
\frac{d\sigma(pp \to H)}{dy_H} = \frac{K}{s} f_g(x_1, Q^2) f_g(x_2, Q^2)
$$
其中 $s$ 是质子对撞的[质心能量](@entry_id:265852)平方，$K$ 是与部分子[截面](@entry_id:154995)相关的常数，$f_g(x, Q^2)$ 是在动量转移标度 $Q$（通常取 $Q \approx m_H$）下的胶子PDF，它给出了在质子中找到一个携带动量分数 $x$ 的胶子的[概率密度](@entry_id:175496)。运动学关系将 $x_1, x_2$ 与 $m_H, y_H$联系起来：
$$
x_1 = \frac{m_H}{\sqrt{s}}e^{y_H} \quad \text{and} \quad x_2 = \frac{m_H}{\sqrt{s}}e^{-y_H}
$$
通过使用一个简化的玩具模型PDF，例如 $f_g(x) = C_g (1-x)^k/x$，并利用描述质子总动量组成的[动量求和规则](@entry_id:159582) $\int_0^1 x f_g(x) dx = M_g$ 来固定[归一化常数](@entry_id:752675) $C_g$，我们可以解析地计算出[微分截面](@entry_id:137333)的形状。例如，在中心[快度](@entry_id:265131)区 $y_H = 0$，我们有 $x_1=x_2=m_H/\sqrt{s}$，[微分截面](@entry_id:137333)达到最大值，其具体数值依赖于PDF在该 $x$ 值的行为。这说明[希格斯玻色子](@entry_id:155560)的产生率[直接探测](@entry_id:748463)了质子内部的胶子[分布](@entry_id:182848)。

#### 共振、本底与干涉

希格斯玻色子是一个不稳定的粒子，它会迅速衰变。在实验上，它表现为一个在其[不变质量](@entry_id:265871)谱上的共振峰。然而，产生相同末态的“本底”（background）过程总是存在。例如，在 $gg \to \gamma\gamma$ 过程中，除了通过希格斯共振产生的信号（$gg \to H \to \gamma\gamma$），还存在一个通过夸克圈图直接产生[光子](@entry_id:145192)对的连续谱本底（$gg \to \gamma\gamma$）。

总振幅是信号振幅 $\mathcal{M}_S$ 和本底振幅 $\mathcal{M}_B$ 的相干叠加：$\mathcal{M}_{\text{tot}} = \mathcal{M}_S + \mathcal{M}_B$。总截面正比于 $|\mathcal{M}_{\text{tot}}|^2 = |\mathcal{M}_S|^2 + |\mathcal{M}_B|^2 + 2\text{Re}(\mathcal{M}_S^* \mathcal{M}_B)$。最后一项是**干涉项**，它可能显著地扭曲共振峰的形状。

信号振幅 $\mathcal{M}_S$ 包含一个 Breit-Wigner 传播子：
$$
\mathcal{M}_S \propto \frac{1}{\hat{s}-m_H^2 + i m_H \Gamma_H}
$$
其中 $\Gamma_H$ 是希格斯总[衰变宽度](@entry_id:153846)。假设本底振幅 $\mathcal{M}_B$ 在共振区附近是实数且变化缓慢。干涉项的贡献将正比于 [@problem_id:183019]：
$$
2\text{Re}(\mathcal{M}_S^* \mathcal M_B) \propto \text{Re} \left( \frac{\mathcal{M}_B}{\hat{s}-m_H^2 - i m_H \Gamma_H} \right) = \frac{\mathcal{M}_B (\hat{s}-m_H^2)}{(\hat{s}-m_H^2)^2 + (m_H\Gamma_H)^2}
$$
这个干涉项在共振点 $\hat{s} = m_H^2$ 处为零，但在共振峰的下方（$\hat{s}  m_H^2$）为负，上方（$\hat{s}  m_H^2$）为正（假设 $\mathcal{M}_B0$）。这导致[共振峰](@entry_id:271281)形状发生从一个对称的 Breit-Wigner 峰到一个不对称的、带有“ dip-peak ”结构的Fano形状的扭曲。对这种形状的精确测量为信号和本底振幅的相对大小和相位提供了宝贵信息。

### 利用希格斯玻色子探测新物理

作为标准模型中唯一的基本标量粒子，希格斯玻色子的性质对超出标准模型的新物理（BSM）极为敏感。精确测量其产生和衰变，以及寻找稀有过程，是粒子物理前沿的核心任务。

#### [戈德斯通玻色子等效定理](@entry_id:157742)与[高能散射](@entry_id:151941)

如前所述，大质量矢量[玻色子](@entry_id:138266)的[纵向极化](@entry_id:202391)分量与[希格斯机制](@entry_id:144416)中的戈德斯通玻色子有着深刻的联系。**[戈德斯通玻色子等效定理](@entry_id:157742)**（Goldstone Boson Equivalence Theorem, GBET）将这一联系形式化：在一个可重整化规范理论中，一个涉及外部[纵向极化](@entry_id:202391)规范玻色子 $V_L$ 的[散射振幅](@entry_id:155369)，在[质心能量](@entry_id:265852) $E \gg m_V$ 的极限下，等于将这些 $V_L$ 替换为相应戈德斯通玻色子 $\phi$ 的等效振幅。
$$
\mathcal{M}(V_{L,1}, V_{L,2}, \dots) \approx \mathcal{M}(\phi_1, \phi_2, \dots) \quad \text{for } E \gg m_V
$$
GBET的巨大威力在于它允许我们将复杂的高能矢量[玻色子](@entry_id:138266)散射问题，转化为一个相对简单的标量[粒子散射](@entry_id:152941)问题来计算。

一个经典的应用是在矢量[玻色子](@entry_id:138266)融合（Vector-Boson Fusion, VBF）过程中产生双希格斯。例如，在高能下，$W_L^+ W_L^- \to HH$ 的[截面](@entry_id:154995)可以通过计算相应的戈德斯通玻色子散射 $\omega^+ \omega^- \to HH$ 来获得 [@problem_id:183085]。这个 $2 \to 2$ 的标量散射过程包含两个图：一个是通过 $H^2 \omega^+ \omega^-$ 顶点的[接触图](@entry_id:267441)，另一个是通过 $s$-channel 虚希格斯交换的图，后者涉及关键的 $HHH$ 三线性自耦合 $\lambda_3$。

利用GBET计算得到的[截面](@entry_id:154995)为：
$$
\hat{\sigma}(W_L W_L \to HH) \approx \hat{\sigma}(\omega\omega \to HH) = \frac{\sqrt{1-\frac{4m_H^2}{\hat{s}}}}{32\pi\hat{s}}\left|\frac{m_H^2}{v^2} - \frac{\lambda_3}{v} \frac{m_H^2}{\hat{s}-m_H^2}\right|^2
$$
这个表达式清楚地显示了[截面](@entry_id:154995)对 $\lambda_3$ 的依赖性。如果 $\lambda_3$ 偏离其标准模型值，[截面](@entry_id:154995)将会改变，从而为探测希格斯势的结构提供了途径。

#### 探测希格斯势：双[希格斯产生](@entry_id:158684)

在LHC上，探测 $\lambda_{HHH}$ 的黄金通道是胶子融合产生的双希格斯过程，$gg \to HH$。在重顶夸克[有效理论](@entry_id:155490)中，该过程由两种类型的[Feynman图](@entry_id:144373)贡献 [@problem_id:183008]：
1.  **“Box”图**：两个胶子通过一个 $gghh$ 有效接触顶点直接产生两个希格斯玻色子。其振幅 $\mathcal{M}_{\square}$ 与 $h^2 G^2$ 算符的系数成正比。
2.  **“Triangle”图**：两个胶子融合产生一个虚的 $s$-channel 希格斯玻色子，该[虚粒子](@entry_id:147959)再分裂成两个末态希格斯玻色子。其振幅 $\mathcal{M}_{\triangle}$ 与 $h G^2$ 算符和三线性耦合 $\lambda_{HHH}$ 的乘积成正比。

总振幅为 $\mathcal{M} = \mathcal{M}_{\square} + \mathcal{M}_{\triangle}$。在标准模型中，这两个振幅发生显著的[相消干涉](@entry_id:170966)。关键的是，$\mathcal{M}_{\triangle}$ 线性地依赖于 $\lambda_{HHH}$。我们可以将 $\lambda_{HHH}$ 参数化为 $\kappa_\lambda \lambda_{HHH}^{\text{SM}}$，其中 $\kappa_\lambda=1$ 对应标准模型。干涉项与纯Box图贡献的比值可以计算为：
$$
R = \frac{2\text{Re}(\mathcal{M}_{\triangle}^* \mathcal{M}_{\square})}{|\mathcal{M}_{\square}|^2} = 2 \text{Re}\left(\frac{\mathcal{M}_{\triangle}}{\mathcal{M}_{\square}}\right) = \frac{6 \kappa_\lambda m_H^2}{\hat{s}-m_H^2}
$$
这个结果表明，干涉项对 $\kappa_\lambda$ 的偏离是线性敏感的。因此，通过精确测量 $gg \to HH$ [截面](@entry_id:154995)及其随[质心能量](@entry_id:265852) $\sqrt{\hat{s}}$ 的变化，我们可以对希格斯三线性自耦合 $\kappa_\lambda$ 进行测量或施加限制。

#### [辐射修正](@entry_id:157711)与[真空稳定性](@entry_id:162028)

最后，[希格斯玻色子](@entry_id:155560)的质量本身也受到巨大的量子[辐射修正](@entry_id:157711)。在标准模型中，最大的修正来自于顶夸克圈，因为它具有最大的[汤川耦合](@entry_id:154951) $y_t$。这些修正对于理解电弱真空的稳定性至关重要。

我们可以利用 Coleman-Weinberg [有效势](@entry_id:142581)的形式来计算这些修正。对于顶夸克圈的贡献，在 $\overline{\text{MS}}$ [重整化方案](@entry_id:154662)下，它对希格斯有效势的[单圈修正](@entry_id:153745) $\Delta V_t$ 会导致希格斯质量平方 $m_h^2$ 发生改变。完整的计算表明，来自顶夸克圈的[单圈修正](@entry_id:153745) $\delta m_h^2$ 为 [@problem_id:183089]：
$$
\delta m_h^2 = - \frac{2 N_c y_t^4 v^2}{(4\pi)^2}
$$
这个修正是负的，并且对顶夸克[汤川耦合](@entry_id:154951)（或质量）的依赖是四次方的，这意味着它非常大。这个负的贡献倾向于降低希格斯四次耦合 $\lambda$ 在高能标下的值。如果 $\lambda$ 在某个高[能标](@entry_id:196201)度下变为负值，我们的电弱真空将不再是稳定或亚稳的，这将预示着标准模型在高能下失效，需要新物理的出现。因此，希格斯质量、[顶夸克质量](@entry_id:160842)和[强耦合常数](@entry_id:159543)的精确值，对于确定我们的宇宙是否处于一个稳定的真空中至关重要，而这一切的核心都源于对希格斯扇区[辐射修正](@entry_id:157711)的深刻理解。