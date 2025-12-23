## 引言
在[计算燃烧学](@entry_id:1122776)领域，准确模拟[湍流](@entry_id:151300)与化学反应的复杂相互作用是核心挑战之一。当我们对控制方程进行[雷诺平均](@entry_id:754341)（RANS）或大涡模拟（LES）滤波时，会产生一个关键的知识鸿沟：如何封闭[化学反应速率](@entry_id:147315)这类高度[非线性](@entry_id:637147)的源项。直接使用平均量计算平均[反应速率](@entry_id:185114)会导致严重误差，因此需要更精密的统计模型来描述亚格子尺度的标量脉动及其对化学过程的影响。[假定概率密度函数](@entry_id:753720)（Presumed PDF）方法正是为解决这一难题而生的一种强大而高效的工程方法。

本文将系统地引导读者深入理解[假定PDF](@entry_id:753720)方法的理论与实践。在“原理与机制”一章中，我们将追溯问题的根源，阐明为何需要统计描述，并详细介绍Beta-PDF等常见函数形式的构建与[参数化](@entry_id:265163)。接下来的“应用与跨学科联系”一章将展示该方法如何与层流火焰面模型等核心燃烧模型相结合，并探讨其在污染物预测、[多维系统](@entry_id:274301)建模以及与机器学习等前沿领域的交叉应用。最后，通过“动手实践”部分的一系列练习，读者将把理论知识转化为解决实际问题的计算技能。

## 原理与机制

在[湍流反应流](@entry_id:1133520)的[数值模拟](@entry_id:146043)中，一个核心挑战是如何处理在求解的控制方程中出现的未封闭项。尤其对于化学反应速率这类高度[非线性](@entry_id:637147)的源项，其平均值的计算远非简单的代数替换。本章将深入探讨[假定概率密度函数](@entry_id:753720)（Presumed Probability Density Function, PDF）方法的基本原理与核心机制。这是一种强大的[统计建模](@entry_id:272466)策略，旨在为[雷诺平均](@entry_id:754341)（RANS）和 [大涡模拟（LES）](@entry_id:273295)中的[非线性](@entry_id:637147)[化学源项](@entry_id:747323)提供[封闭模型](@entry_id:1122505)。我们将从问题的根源出发，阐明为何需要统计描述，介绍并区分不同的平均方法，并详细阐述如何构建和应用几种常见的[假定PDF](@entry_id:753720)形式，最终探讨该方法的局限性及相应的进阶思路。

### [非线性源项](@entry_id:1128871)的封闭问题

在[湍流燃烧](@entry_id:756233)的模拟中，我们求解的是经过时间平均（RANS）或[空间滤波](@entry_id:202429)（LES）的[输运方程](@entry_id:174281)。考虑一个标量场 $\phi(\mathbf{x},t)$（例如，[反应进度](@entry_id:140591)变量或混合分数），其[化学反应速率](@entry_id:147315)由一个[非线性](@entry_id:637147)函数 $\omega(\phi)$ 描述。在经过密度加权的[Favre平均](@entry_id:198824)或滤波（用波浪号 $\sim$ 表示）的方程中，我们需要对平均化学反应源项 $\widetilde{\omega(\phi)}$ 进行建模。

一个初学者可能会直观地认为，可以直接用平均标量 $\tilde{\phi}$ 来计算平均[反应速率](@entry_id:185114)，即 $\widetilde{\omega(\phi)} \approx \omega(\tilde{\phi})$。然而，这种所谓的“层[流化](@entry_id:192588)学”假设在[湍流](@entry_id:151300)环境中通常是严重错误的。其根本原因在于，平均或滤波算子是线性积分运算，而化学反应速率函数 $\omega(\cdot)$ 却是高度[非线性](@entry_id:637147)的。根据[Jensen不等式](@entry_id:144269)，对于一个[非线性](@entry_id:637147)函数 $f$ 和一个[平均算子](@entry_id:746605) $\langle\cdot\rangle$，通常有 $\langle f(x) \rangle \neq f(\langle x \rangle)$。

为了更清晰地理解这一点，我们可以将瞬时标量 $\phi$ 分解为已解尺度部分（平均值）$\tilde{\phi}$ 和未解尺度部分（脉动）$\phi''$，即 $\phi = \tilde{\phi} + \phi''$。然后，将[反应速率](@entry_id:185114)函数 $\omega(\phi)$ 在 $\tilde{\phi}$ 附近进行[泰勒级数展开](@entry_id:138468)：
$$
\omega(\phi) = \omega(\tilde{\phi} + \phi'') = \omega(\tilde{\phi}) + \frac{d\omega}{d\phi}\bigg|_{\tilde{\phi}} \phi'' + \frac{1}{2!}\frac{d^2\omega}{d\phi^2}\bigg|_{\tilde{\phi}} (\phi'')^2 + \dots
$$
对上式进行[Favre平均](@entry_id:198824)，我们得到：
$$
\widetilde{\omega(\phi)} = \omega(\tilde{\phi}) + \frac{d\omega}{d\phi}\bigg|_{\tilde{\phi}} \widetilde{\phi''} + \frac{1}{2}\frac{d^2\omega}{d\phi^2}\bigg|_{\tilde{\phi}} \widetilde{(\phi'')^2} + \dots
$$
根据Favre脉动的定义，其[Favre平均](@entry_id:198824)为零，即 $\widetilde{\phi''} = 0$。因此，上式简化为：
$$
\widetilde{\omega(\phi)} = \omega(\tilde{\phi}) + \frac{1}{2}\frac{d^2\omega}{d\phi^2}\bigg|_{\tilde{\phi}} \widetilde{(\phi'')^2} + \text{高阶项}
$$
这个表达式明确地揭示了问题所在。只要[反应速率](@entry_id:185114) $\omega(\phi)$ 是[非线性](@entry_id:637147)的（即其二阶或更[高阶导数](@entry_id:140882)不为零），并且存在亚格子脉动（即亚格子方差 $\widetilde{(\phi'')^2} > 0$），那么 $\widetilde{\omega(\phi)}$ 就不等于 $\omega(\tilde{\phi})$。等式仅在两种特殊情况下成立：(1) $\omega(\phi)$ 是一个[仿射函数](@entry_id:635019)（即线性函数 $a\phi+b$）；或 (2) 亚格子标量分布是退化的（即方差及所有高阶矩均为零），这在[湍流](@entry_id:151300)中几乎不可能。

为了获得一个精确的表达式，我们可以借助狄拉克 $\delta$ 函数的性质。任何函数都可以写作如下积分形式：
$$
\omega(\phi) = \int \omega(\xi)\,\delta(\phi-\xi)\,d\xi
$$
其中 $\xi$ 是标量 $\phi$ [状态空间](@entry_id:160914)中的一个哑变量。将这个精确的恒等式代入[Favre平均](@entry_id:198824)的定义中，并[交换积分](@entry_id:177036)和平均的顺序，我们得到：
$$
\widetilde{\omega(\phi)} = \frac{\overline{\rho \omega(\phi)}}{\overline{\rho}} = \int \omega(\xi) \left( \frac{\overline{\rho\,\delta(\phi-\xi)}}{\overline{\rho}} \right) d\xi
$$
括号中的项被定义为Favre加权的亚格子PDF，记作 $p^{\ast}_{\phi}(\xi; \mathbf{x}, t)$：
$$
p^{\ast}_{\phi}(\xi; \mathbf{x}, t) \equiv \frac{\overline{\rho\,\delta(\phi-\xi)}}{\overline{\rho}}
$$
这个函数 $p^{\ast}_{\phi}(\xi)$ 描述了在时空点 $(\mathbf{x}, t)$ 的滤波体积内，标量取值为 $\xi$ 的密度加权概率。因此，平均[反应速率](@entry_id:185114)的精确表达式是一个[期望值](@entry_id:150961)：
$$
\widetilde{\omega(\phi)} = \int \omega(\xi)\,p^{\ast}_{\phi}(\xi; \mathbf{x}, t)\,d\xi
$$
这个公式是精确但未封闭的，因为我们并不知道真实的亚格子PDF $p^{\ast}_{\phi}$ 的确切形状。**[假定PDF](@entry_id:753720)方法**的动机正源于此：我们不试图求解 $p^{\ast}_{\phi}$，而是*假定*一个由低阶矩（如平均值和方差）[参数化](@entry_id:265163)的函数形式来近似它。

### 可压缩流中的雷诺平均与[Favre平均](@entry_id:198824)

在深入研究PDF的具体形式之前，必须区分在可压缩流（如燃烧过程）中使用的两种主要平均方法：[雷诺平均](@entry_id:754341)和[Favre平均](@entry_id:198824)。

对于任意标量 $\phi$，**[雷诺平均](@entry_id:754341)**（用上划线 $\bar{\cdot}$ 表示）是标准的系综平均或时间平均，$\bar{\phi} = \langle \phi \rangle$。其脉动定义为 $\phi' = \phi - \bar{\phi}$。然而，在密度 $\rho$ 显著变化的流动中，使用[雷诺平均](@entry_id:754341)会导致平均后的控制方程（如连续性方程和动量方程）中出现大量涉及密度脉动与速度脉动相关性的项，例如[湍流](@entry_id:151300)质量通量 $\overline{\rho'\mathbf{u'}}$，这使得建模变得异常复杂。

为了简化方程形式，我们引入**[Favre平均](@entry_id:198824)**（或密度加权平均，用波浪号 $\sim$ 表示），其定义为 $\tilde{\phi} = \overline{\rho \phi} / \bar{\rho}$。Favre脉动则定义为 $\phi'' = \phi - \tilde{\phi}$，其关键性质是 $\overline{\rho \phi''} = 0$。通过使用[Favre平均](@entry_id:198824)速度 $\tilde{\mathbf{u}}$，平均[连续性方程](@entry_id:195013)可以写成 $\partial_t \bar{\rho} + \nabla \cdot (\bar{\rho}\tilde{\mathbf{u}}) = 0$，其形式与瞬时方程一致，不包含显式的密度-速度相关项。

只有当密度脉动可以忽略不计（$\rho' \approx 0$）时，[Favre平均](@entry_id:198824)才近似等于雷诺平均（$\tilde{\phi} \approx \bar{\phi}$）[@problem_id:4053686, @problem_id:4053711]。在燃烧问题中，由于剧烈的热释放，密度变化通常非常剧烈，因此[Favre平均](@entry_id:198824)是更合适的选择。

与[Favre平均](@entry_id:198824)相对应，我们需要使用**Favre加权PDF**。对于单位质量的量（如质量分数或比焓），其[Favre平均](@entry_id:198824)值 $\tilde{g(\phi)}$ 可以通过Favre PDF $P_F(\eta)$ 计算得到：
$$
\tilde{g(\phi)} = \int g(\eta) \, P_F(\eta) \, \mathrm{d}\eta
$$
其中，Favre PDF的正式定义为：
$$
P_F(\eta) = \frac{\overline{ \rho \, \delta( \eta - \phi ) }}{\bar{ \rho }}
$$
这与我们之前为封闭源项推导出的 $p^{\ast}_{\phi}$ 形式一致。因此，在基于[Favre平均](@entry_id:198824)的RANS或LES模型中，必须使用由Favre矩（如[Favre平均](@entry_id:198824)值 $\tilde{\phi}$ 和Favre方差 $\widetilde{\phi''^2}$）[参数化](@entry_id:265163)的[假定PDF](@entry_id:753720)，以保证模型的一致性。使用雷诺矩来约束Favre PDF会导致系统性的偏差。[@problem_id:4053686, @problem_id:4053711]

### 输运PDF方法与[假定PDF](@entry_id:753720)方法的对比

从理论上讲，除了[假定PDF](@entry_id:753720)的形状外，还有一种更严谨的方法，即直接求解PDF的[输运方程](@entry_id:174281)，这种方法被称为**输运PDF方法**。通过对标量 $\phi$ 的瞬时[输运方程](@entry_id:174281)进行数学推导，可以得到其单点PDF $p(\psi; \mathbf{x}, t)$ 的精确[输运方程](@entry_id:174281)：
$$
\frac{\partial p}{\partial t} + \frac{\partial}{\partial x_j} \left[ p \langle u_j \mid \phi=\psi \rangle \right] = -\frac{\partial}{\partial \psi} \left[ p \langle \omega \mid \phi=\psi \rangle \right] - \frac{\partial}{\partial \psi} \left[ \frac{p}{2} \frac{\partial}{\partial \psi} \langle \chi \mid \phi=\psi \rangle \right]
$$
其中 $\psi$ 是标量[状态空间](@entry_id:160914)中的样本变量。这个方程描述了PDF $p$ 在物理空间中的对流（左侧第二项）以及在组分空间中由于化学反应（右侧第一项）和分子混合（右侧第二项）引起的输运。

然而，这个精确的方程同样是未封闭的。其中出现了几个需要建模的[条件期望](@entry_id:159140)项：
1.  **条件速度 $\langle u_j \mid \phi=\psi \rangle$**: 描述了[湍流](@entry_id:151300)输运，即湍流通量。
2.  **条件[反应速率](@entry_id:185114) $\langle \omega \mid \phi=\psi \rangle$**: 描述了化学反应对PDF形状的影响。
3.  **[条件标量耗散率](@entry_id:1122853) $\langle \chi \mid \phi=\psi \rangle$**: 其中 $\chi = 2D (\nabla\phi)^2$ 是[标量耗散率](@entry_id:754534)，该项描述了分子[微观混合](@entry_id:751971)（micromixing）使PDF趋向于一个狄拉克 $\delta$ 函数的过程。

对这些条件项，尤其是[微观混合](@entry_id:751971)项的建模，是输运PDF方法中的核心挑战。**[假定PDF](@entry_id:753720)方法**则另辟蹊径：它不求解PDF的[输运方程](@entry_id:174281)，而是求解其低阶矩（如平均值和方差）的[输运方程](@entry_id:174281)。然后，通过假定一个由这些已知的低阶矩[参数化](@entry_id:265163)的PDF形状，来计算[非线性](@entry_id:637147)的平均[反应速率](@entry_id:185114)，从而封闭矩方程。这是一种计算上更经济、概念上更直接的工程方法。

### 常见的[假定PDF](@entry_id:753720)形式及其[参数化](@entry_id:265163)

[假定PDF](@entry_id:753720)的选择应基于所模拟标量的物理特性。对于在特定范围内有界的标量，如混合分数或归一化[反应进度](@entry_id:140591)变量，有几种特别常用的PDF形式。

#### Beta-PDF：适用于有界标量

对于一个在 $[0, 1]$ 区间内有界的标量 $\phi$（例如混合分数 $Z$），**Beta分布**是一个非常自然和灵活的选择。其PDF由两个[形状参数](@entry_id:270600) $\alpha > 0$ 和 $\beta > 0$ 决定：
$$
p(\phi; \alpha, \beta) = \frac{\phi^{\alpha-1}(1-\phi)^{\beta-1}}{B(\alpha, \beta)}
$$
其中 $B(\alpha, \beta)$ 是Beta函数，用作[归一化常数](@entry_id:752675)。

在[假定PDF](@entry_id:753720)方法中，我们需要从已知的标量平均值 $\mu$ 和方差 $\sigma^2$（这里代表[Favre平均](@entry_id:198824)值和方差）反解出参数 $\alpha$ 和 $\beta$。Beta分布的均值和方差由以下公式给出：
$$
\mu = \frac{\alpha}{\alpha + \beta}
$$
$$
\sigma^2 = \frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)} = \frac{\mu(1-\mu)}{\alpha+\beta+1}
$$
通过求解这个方程组，我们可以得到 $\alpha$ 和 $\beta$ 的表达式 [@problem_id:4053717, @problem_id:4053686]：
$$
\alpha = \mu \left( \frac{\mu(1-\mu)}{\sigma^2} - 1 \right)
$$
$$
\beta = (1-\mu) \left( \frac{\mu(1-\mu)}{\sigma^2} - 1 \right)
$$
为了使 $\alpha$ 和 $\beta$ 为正，必须满足条件 $\sigma^2  \mu(1-\mu)$。这个条件具有明确的物理意义：对于一个均值为 $\mu$ 且在 $[0,1]$ 内的[随机变量](@entry_id:195330)，其方差的最大可能值为 $\mu(1-\mu)$，这个[极值](@entry_id:145933)对应于一个只在 0 和 1 两点取值的[两点分布](@entry_id:266933)（[伯努利分布](@entry_id:266933)）。任何[连续分布](@entry_id:264735)的方差都必须严格小于这个上限。

#### 双Delta-PDF：适用于完全分离流

在[非预混燃烧](@entry_id:1128819)的极限情况下，燃料和氧化剂在亚格子尺度上可能还未混合，处于**完全分离（perfectly segregated）**状态。这种情况可以用**双Delta-PDF**来理想化地描述。对于一个标量 $\phi$，其形式为：
$$
p(\phi) = a\,\delta(\phi-\phi_1) + (1-a)\,\delta(\phi-\phi_2)
$$
其中 $\phi_1$ 和 $\phi_2$ 是两个纯净流的标量值，而 $a \in [0,1]$ 是对应于 $\phi_1$ 的权重。这个PDF的均值和方差分别为：
$$
\tilde{\phi} = a\phi_1 + (1-a)\phi_2
$$
$$
\widetilde{(\phi'')^2} = a(1-a)(\phi_2-\phi_1)^2
$$
考虑一个以混合分数 $Z$ 为标量的[非预混燃烧](@entry_id:1128819)场景，其中燃料流 $Z=1$，氧化剂流 $Z=0$。双Delta-PDF变为 $p(Z) = a\delta(Z-0) + (1-a)\delta(Z-1)$。在这种情况下，均值 $\tilde{Z} = 1-a$。一个重要的结论是，对于一个[双分子反应](@entry_id:165027)速率 $\dot{\omega} = k Y_F Y_O$，其平均值 $\langle \dot{\omega} \rangle$ 在完全分离状态下为零。这是因为在任何一个瞬时时刻，流体要么是纯燃料（$Y_O=0$），要么是纯氧化剂（$Y_F=0$），因此它们的乘积 $Y_F Y_O$ 恒为零。这从数学上印证了一句燃烧学的格言：“没有混合就没有燃烧”。

#### 从分离到混合的PDF演化

双Delta-PDF和Beta-PDF可以被看作是混合过程的两个极限。一个典型的混合过程可以被建模为PDF从初始的双Delta-PDF（完全分离）向最终的单Delta-PDF（完全混合，方差为零）的演化。在这个过程中，Beta-PDF可以作为中间状态的良好近似。

考虑一个采用均值交换（IEM）模型描述[微观混合](@entry_id:751971)的系统，[标量方差](@entry_id:1131255)的演化遵循指数衰减规律：
$$
\sigma_Z^2(t) = \sigma_Z^2(0)\,\exp\left(-\frac{2t}{\tau_m}\right)
$$
其中 $\tau_m$ 是[微观混合](@entry_id:751971)时间尺度。由于标量是守恒的，其均值 $\tilde{Z}$ 保持不变。在$t=0$时，系统处于双Delta-PDF描述的完全分离状态，方差达到最大值 $\sigma_Z^2(0) = \tilde{Z}(1-\tilde{Z})$。随着时间推移，方差 $\sigma_Z^2(t)$ 减小。我们可以观察Beta-PDF的聚合[形状参数](@entry_id:270600) $\lambda = \alpha+\beta = \frac{\tilde{Z}(1-\tilde{Z})}{\sigma_Z^2} - 1$ 的变化：
-   当 $t=0$ 时，$\sigma_Z^2 = \tilde{Z}(1-\tilde{Z})$，因此 $\lambda = 0$。这对应于Beta分布退化为[两点分布](@entry_id:266933)的极限。
-   当 $t \to \infty$ 时，$\sigma_Z^2 \to 0$，因此 $\lambda \to \infty$。这对应于Beta分布收缩为在均值处的一个狄拉克 $\delta$ [函数的极限](@entry_id:158708)。

这个[演化过程](@entry_id:175749)清晰地描绘了PDF形状如何随着湍流混合的进行而从双峰（分离）变为单峰（混合）并最终变得无限窄（完全混合）。

### 多标量建模：联合PDF与相关性

在更复杂的燃烧模型中，通常需要同时考虑多个标量，例如混合分数 $Z$ 和[反应进度](@entry_id:140591)变量 $c$。在这种情况下，化学反应速率是两个或多个变量的函数，$\omega(\phi, \psi)$，其平均值需要通过联合PDF来计算：
$$
\langle \omega \rangle = \iint \omega(\phi,\psi)\, P_{\phi,\psi}(\phi,\psi)\, \mathrm{d}\phi\, \mathrm{d}\psi
$$
除了每个标量的均值和方差外，它们之间的**协方差** $\mathrm{cov}(\phi,\psi)$ 或**相关系数** $r = \mathrm{cov}(\phi,\psi)/(\sigma_\phi\sigma_\psi)$ 成为描述系统状态的关键参数。

相关性的影响可以通过对[反应速率](@entry_id:185114)的二阶[泰勒展开](@entry_id:145057)来直观理解。展开后的平均[反应速率](@entry_id:185114)近似为：
$$
\langle \omega \rangle \approx \omega(\mu_\phi, \mu_\psi) + \frac{1}{2}\left( \sigma_\phi^2 \omega_{\phi\phi} + 2 \mathrm{cov}(\phi,\psi) \omega_{\phi\psi} + \sigma_\psi^2 \omega_{\psi\psi} \right)
$$
其中 $\omega_{\phi\phi}$, $\omega_{\psi\psi}$, 和 $\omega_{\phi\psi}$ 是在均值点 $(\mu_\phi, \mu_\psi)$ 处求值的[二阶偏导数](@entry_id:635213)。显然，协方差（或[相关系数](@entry_id:147037)）通过与[反应速率](@entry_id:185114)的混合曲率 $\omega_{\phi\psi}$ 相乘来影响平均[反应速率](@entry_id:185114)。

值得注意的是，[相关系数](@entry_id:147037)为零（不相关）并不等同于统计独立，除非这些变量服从[联合高斯](@entry_id:636452)分布。对于一般的PDF，不相关并不能保证联合PDF可以分解为边缘PDF的乘积。

为了构建一个具有给定边缘分布和特定相关性的联合PDF，**[Copula理论](@entry_id:142319)**提供了一个严谨的框架。根据[Sklar定理](@entry_id:143965)，任何[联合分布](@entry_id:263960)函数都可以用其边缘[分布函数](@entry_id:145626)和-一个称为Copula的函数来表示。对于联合PDF，其表达式为：
$$
p(\phi,\psi) = c(F_\phi(\phi), F_\psi(\psi)) \cdot p_\phi(\phi) \cdot p_\psi(\psi)
$$
其中 $p_\phi, p_\psi$ 是边缘PDF，$F_\phi, F_\psi$ 是对应的边缘CDF，而 $c(u,v)$ 是Copula密度函数。通过选择一个带参数 $\theta$ 的Copula族（如高斯Copula或[阿基米德Copula](@entry_id:746507)），联合PDF就依赖于这个参数。然后，可以通过求解如下[积分方程](@entry_id:138643)来确定 $\theta$ 的值，以匹配目标[Pearson相关系数](@entry_id:270276) $r$：
$$
r = \frac{1}{\sigma_\phi \sigma_\psi} \iint (\phi - \mu_\phi)(\psi - \mu_\psi) \, p(\phi,\psi;\theta) \,\mathrm{d}\phi\,\mathrm{d}\psi
$$
这个过程确保了所构建的联合PDF不仅具有正确的边缘分布，还具有期望的相关性结构，为多[标量化](@entry_id:634761)学反应的封闭提供了灵活而强大的工具。

### 局限性与高级方法

尽管[假定PDF](@entry_id:753720)方法应用广泛，但其基本形式（如单标量Beta-PDF）在某些物理条件下会遇到局限。

一个主要挑战是**差示扩散（Differential Diffusion）**。混合分数 $Z$ 的定义基于元素守恒，这保证了它没有[化学源项](@entry_id:747323)。然而，只有当所有组分的[质量扩散系数](@entry_id:149206)都相等时（即所有Lewis数 $Le_i$ 都相等），$Z$ 的扩散通量才能简化为简单的Fickian形式。在实际火焰中，不同组分（如轻质的H$_2$和重质的碳氢燃料）的扩散速率差异显著。这导致 $Z$ 的[输运方程](@entry_id:174281)中出现一个由非Fickian[通量散度](@entry_id:1125154)产生的“表观源项”。这个源项可以系统地改变 $Z$ 的分布，使其偏离简单的Beta-PDF形状。

此外，即使在所有 $Le_i=1$ 的理想情况下，强烈的**热释放**效应也会带来挑战。热释放引起的大幅度温度和密度变化，会使得[输运系数](@entry_id:136790)（如密度 $\rho$ 和扩散系数 $D(T)$）在空间上剧烈变化。这会在 $Z$ 的[输运过程](@entry_id:177992)中引入[非线性](@entry_id:637147)效应，可能产生[偏度](@entry_id:178163)和峰度等高阶矩，而这些是双参数的Beta-PDF无法捕捉的。

为了克服这些局限性，研究者们发展了更为先进的方法。例如，使用包含焓（$h$）的联合PDF $p(Z,h)$ 来同时考虑混合和[热损失](@entry_id:165814)/差示扩散效应，或者采用[条件矩封闭](@entry_id:1122851)（Conditional Moment Closure, CMC）等方法，其中PDF的参数被允许依赖于混合分数或其他[条件变量](@entry_id:747671)。这些方法虽然更为复杂，但能够更准确地捕捉[湍流](@entry_id:151300)与化学反应之间错综复杂的相互作用。