## 引言
[中心极限定理](@entry_id:143108)（Central Limit Theorem, CLT）是概率论与统计学的基石，它以其惊人的普适性，解释了为何正态分布在自然界与科学研究中无处不在。然而，许多研究者对CLT的理解往往停留在“大量[独立同分布随机变量](@entry_id:270381)之和近似正态分布”这一基本表述上，而忽略了其深刻的数学内涵、成立的边界条件，以及应对现代复杂数据（如相依、异质或高维数据）所必需的强大推广。本文旨在弥合这一知识鸿沟，为研究生水平的读者提供一个关于中心极限定理的全面而深入的视角，重点突出其在医学统计建模中的核心作用。

为实现这一目标，本文将分为三个紧密相连的章节。在第一章 **“原理与机制”** 中，我们将从经典的Lindeberg-Lévy定理出发，通过特征函数进行严谨的[数学证明](@entry_id:137161)，并探讨近似的精度（[Berry-Esseen定理](@entry_id:261040)）和修正（Edgeworth展开）。此外，本章还将介绍CLT的关键推广，如适用于非同分布数据的[Lindeberg-Feller定理](@entry_id:195247)和处理相依数据的[鞅中心极限定理](@entry_id:198119)，为后续应用奠定坚实的理论基础。

随后的第二章 **“应用与跨学科联系”** 将展示CLT在实践中的巨大威力。我们将探讨如何运用Delta方法推导复杂统计量（如对数比值比）的分布，如何处理生存分析中的删失数据，以及如何应对高维数据分析带来的挑战。本章还将跨越学科界限，揭示CLT如何为遗传学的易患性-[阈值模型](@entry_id:172428)和[计算神经科学](@entry_id:274500)的漂移-[扩散模型](@entry_id:142185)等科学理论提供数学支撑。

最后，在 **“动手实践”** 章节中，读者将有机会通过解决一系列精心设计的问题，将理论知识转化为实践技能，从而真正掌握中心极限定理在不同场景下的应用。通过这趟从理论到应用的旅程，读者将深刻理解[中心极限定理](@entry_id:143108)不仅是一个孤立的数学结论，更是连接理论概率与应用统计的强大桥梁。

## 原理与机制

### 基本原理：经典[中心极限定理](@entry_id:143108)

[中心极限定理](@entry_id:143108) (Central Limit Theorem, CLT) 是概率论和统计学中最重要的基石之一。其核心思想在于，大量独立随机变量的均值，在适当的中心化和尺度变换后，其分布会趋向于一个正态分布——无论[原始变量](@entry_id:753733)自身的分布形态如何。这种“万流归宗”于高斯分布的现象，揭示了自然界和工程实践中正态分布普遍存在性的深刻原因。

最基础且应用最广泛的是 **Lindeberg-Lévy 中心极限定理**。该定理考虑一个独立同分布 (independent and identically distributed, i.i.d.) 的随机变量序列 $\{X_i\}_{i=1}^n$，其共同的期望为 $\mathbb{E}[X_i] = \mu$，方差为 $\operatorname{Var}(X_i) = \sigma^2$，其中 $0  \sigma^2  \infty$。我们关注的是样本均值 $\bar{X}_n = \frac{1}{n}\sum_{i=1}^n X_i$。

首先，我们需要理解样本均值自身的收敛行为。根据 **[弱大数定律](@entry_id:159016) (Weak Law of Large Numbers, WLLN)**，当样本量 $n$ 趋于无穷时，样本均值 $\bar{X}_n$ 会在概率上收敛于总体期望 $\mu$。这意味着，对于任意小的正数 $\epsilon$，$\mathbb{P}(|\bar{X}_n - \mu| \ge \epsilon)$ 的概率会随着 $n$ 的增大而趋向于 $0$。这一结论可以通过计算 $\bar{X}_n$ 的方差并应用切比雪夫不等式 (Chebyshev's inequality) 来证明。由于 $X_i$ 独立，我们有：
$$ \operatorname{Var}(\bar{X}_n) = \operatorname{Var}\left(\frac{1}{n}\sum_{i=1}^n X_i\right) = \frac{1}{n^2} \sum_{i=1}^n \operatorname{Var}(X_i) = \frac{n\sigma^2}{n^2} = \frac{\sigma^2}{n} $$
因为 $\operatorname{Var}(\bar{X}_n) \to 0$，所以 $(\bar{X}_n - \mu)$ 的分布会逐渐坍缩，最终集中在 $0$ 这一点上。这是一个 **退化分布 (degenerate distribution)**，它无法为我们提供关于 $\bar{X}_n$ 围绕 $\mu$ 波动的任何有用信息 [@problem_id:4986715]。

[中心极限定理](@entry_id:143108)的精妙之处在于它找到了一个“恰到好处”的尺度因子，使得样本均值的波动既不消失也不发散。这个尺度因子正是 $\sqrt{n}$。通过考察中心化和尺度变换后的统计量 $Z_n = \sqrt{n}(\bar{X}_n - \mu)$，我们发现其方差是稳定的：
$$ \operatorname{Var}(Z_n) = \operatorname{Var}(\sqrt{n}(\bar{X}_n - \mu)) = n \operatorname{Var}(\bar{X}_n) = n \left(\frac{\sigma^2}{n}\right) = \sigma^2 $$
[中心极限定理](@entry_id:143108)断言，这个经过“稳定化”处理的随机变量 $Z_n$ 的分布将收敛于一个非退化的正态分布。具体而言：
$$ Z_n = \sqrt{n}(\bar{X}_n - \mu) \xrightarrow{d} \mathcal{N}(0, \sigma^2) \quad \text{as } n \to \infty $$
其中 $\xrightarrow{d}$ 表示 **[依分布收敛](@entry_id:275544) (convergence in distribution)**。

我们可以利用 **特征函数 (characteristic function)** 对此进行严格证明。一个随机变量 $X$ 的[特征函数](@entry_id:186820)定义为 $\phi_X(t) = \mathbb{E}[\exp(itX)]$。为了简化证明，我们首先对变量进行标准化。令 $Y_i = X_i - \mu$，则 $\mathbb{E}[Y_i] = 0$ 且 $\operatorname{Var}(Y_i) = \sigma^2$。于是 $Z_n$ 可以写为 $Z_n = \frac{1}{\sqrt{n}}\sum_{i=1}^n Y_i$。

由于 $Y_i$ 相互独立且同分布，它们共享同一个[特征函数](@entry_id:186820) $\phi_Y(t)$。$Z_n$ 的特征函数 $\phi_{Z_n}(t)$ 可以表示为：
$$ \phi_{Z_n}(t) = \mathbb{E}\left[\exp\left(it \frac{1}{\sqrt{n}}\sum_{j=1}^n Y_j\right)\right] = \prod_{j=1}^n \mathbb{E}\left[\exp\left(i \frac{t}{\sqrt{n}} Y_j\right)\right] = \left[\phi_Y\left(\frac{t}{\sqrt{n}}\right)\right]^n $$
由于 $Y_i$ 的二阶矩有限，其[特征函数](@entry_id:186820) $\phi_Y(s)$ 在 $s=0$ 附近可以进行[泰勒展开](@entry_id:145057)。根据[特征函数](@entry_id:186820)的性质，其在原点的各阶导数与[随机变量的矩](@entry_id:174539)相关：$\phi_Y(0) = 1$, $\phi_Y'(0) = i\mathbb{E}[Y_1] = 0$，以及 $\phi_Y''(0) = i^2\mathbb{E}[Y_1^2] = -\operatorname{Var}(Y_1) = -\sigma^2$。因此，$\phi_Y(s)$ 的二阶泰勒展开为：
$$ \phi_Y(s) = 1 - \frac{\sigma^2 s^2}{2} + o(s^2) $$
令 $s = t/\sqrt{n}$，我们得到：
$$ \phi_Y\left(\frac{t}{\sqrt{n}}\right) = 1 - \frac{\sigma^2 t^2}{2n} + o\left(\frac{1}{n}\right) $$
代入 $\phi_{Z_n}(t)$ 的表达式中，并取极限：
$$ \lim_{n\to\infty} \phi_{Z_n}(t) = \lim_{n\to\infty} \left[1 - \frac{\sigma^2 t^2}{2n} + o\left(\frac{1}{n}\right)\right]^n = \exp\left(-\frac{\sigma^2 t^2}{2}\right) $$
这个极限形式正是均值为 $0$、方差为 $\sigma^2$ 的正态分布 $\mathcal{N}(0, \sigma^2)$ 的特征函数。根据 **Lévy [连续性定理](@entry_id:262016) (Lévy's continuity theorem)**，[特征函数](@entry_id:186820)的逐点收敛等价于分布的[弱收敛](@entry_id:146650)，从而完成了证明 [@problem_id:4986766]。

这个结果在医学统计中具有深远的实践意义。例如，在大型临床试验中，研究人员可能测量某种生物标志物在大量患者中的水平。即使该标志物在个体内的分布是高度[偏态](@entry_id:178163)或非正态的，中心极限定理保证了只要样本量足够大，样本均值 $\bar{X}_n$ 的[抽样分布](@entry_id:269683)就可以近似地看作一个正态分布 $\mathcal{N}(\mu, \sigma^2/n)$。这使得研究人员能够构建关于总体均值 $\mu$ 的[置信区间](@entry_id:138194)和进行假设检验，为评估药物疗效、制定公共卫生政策提供了坚实的理论基础 [@problem_id:4986766]。

### 从理论到实践：标准化与 Slutsky 定理

经典[中心极限定理](@entry_id:143108)给出了 $\sqrt{n}(\bar{X}_n - \mu)$ 的[渐近分布](@entry_id:272575)，但其方差 $\sigma^2$ 在实际应用中通常是未知的。为了构造可计算的[检验统计量](@entry_id:167372)或[置信区间](@entry_id:138194)，我们必须用样本数据来估计 $\sigma$。一个自然的估计量是样本标准差 $S_n$，其平方定义为无偏样本方差：
$$ S_n^2 = \frac{1}{n-1}\sum_{i=1}^n (X_i - \bar{X}_n)^2 $$
我们可以证明，$S_n^2$ 是 $\sigma^2$ 的一个 **[相合估计量](@entry_id:266642) (consistent estimator)**，即当 $n \to \infty$ 时，$S_n^2 \xrightarrow{p} \sigma^2$，其中 $\xrightarrow{p}$ 表示 **[依概率收敛](@entry_id:145927) (convergence in probability)**。这一结论可以由大数定律和[连续映射定理](@entry_id:269346) (Continuous Mapping Theorem) 得到 [@problem_id:4986841]。

用 $S_n$ 替换理论公式中的 $\sigma$，我们得到 **Student 化统计量 (Studentized statistic)**：
$$ T_n = \frac{\sqrt{n}(\bar{X}_n - \mu)}{S_n} $$
这个统计量的[渐近分布](@entry_id:272575)可以通过 **Slutsky 定理** 确定。Slutsky 定理是一个强大的工具，它描述了[依分布收敛](@entry_id:275544)和依概率收敛之间的相互作用。定理指出，如果 $A_n \xrightarrow{d} A$ 且 $B_n \xrightarrow{p} b$（其中 $b$ 是一个常数），则 $A_n / B_n \xrightarrow{d} A/b$。

我们可以将 $T_n$ 重写为：
$$ T_n = \frac{\sqrt{n}(\bar{X}_n - \mu)/\sigma}{S_n/\sigma} $$
根据中心极限定理，分子 $\sqrt{n}(\bar{X}_n - \mu)/\sigma \xrightarrow{d} Z \sim \mathcal{N}(0,1)$。根据 $S_n^2$ 的相合性及[连续映射定理](@entry_id:269346)，$S_n \xrightarrow{p} \sigma$，因此分母 $S_n/\sigma \xrightarrow{p} 1$。应用 Slutsky 定理，我们得出结论：
$$ T_n = \frac{\sqrt{n}(\bar{X}_n - \mu)}{S_n} \xrightarrow{d} \mathcal{N}(0,1) $$
这意味着，即使在 $\sigma$ 未知的情况下，只要样本量足够大，$T_n$ 的分布也可以用[标准正态分布](@entry_id:184509)来近似。这为基于 Z 检验和[正态近似](@entry_id:261668)[置信区间](@entry_id:138194)的[统计推断](@entry_id:172747)提供了合法性 [@problem_id:4986715] [@problem_id:4986841]。

值得强调的是，这个[渐近正态性](@entry_id:168464)的结论与著名的 **Student's t 分布** 既有联系又有区别。当原始数据 $X_i$ *严格*服从正态分布 $N(\mu, \sigma^2)$ 时，对于任意有限样本量 $n>1$，$T_n$ 的分布是**精确的** Student's t 分布，自由度为 $n-1$。这个精确结果依赖于正态分布一个独特的性质：样本均值 $\bar{X}_n$ 与样本方差 $S_n^2$ 相互独立。

然而，对于非正态数据，$\bar{X}_n$ 与 $S_n^2$ 通常不独立，$T_n$ 在有限样本下的精确分布是未知且复杂的。[中心极限定理](@entry_id:143108)与 Slutsky 定理的美妙之处在于，它们保证了无论原始分布如何（只要方差有限），$T_n$ 的分布在 $n \to \infty$ 时都将收敛到[标准正态分布](@entry_id:184509)。由于 Student's t 分布在其自由度趋于无穷时也收敛于[标准正态分布](@entry_id:184509)（例如，$\lim_{n\to\infty} (t_{0.975, n-1} - z_{0.975}) = 0$），因此[正态近似](@entry_id:261668)和 t 分布近似在样本量很大时是等价的 [@problem_id:4986841]。

### 完善近似：[收敛速度](@entry_id:146534)与展开式

[中心极限定理](@entry_id:143108)描述了一种极限行为，但并未说明对于有限的样本量 $n$，[正态近似](@entry_id:261668)的“好坏”程度。为了定量评估近似误差，我们需要更精细的工具。

**Berry-Esseen 定理** 为我们提供了[正态近似](@entry_id:261668)误差的一个非渐近上界。该定理指出，在经典 CLT 的 i.i.d. 设定下，如果额外假设第三绝对[中心矩](@entry_id:270177) $\rho = \mathbb{E}[|X_1 - \mu|^3]$ 有限，则存在一个[普适常数](@entry_id:165600) $C$，使得：
$$ \sup_{x \in \mathbb{R}} |\mathbb{P}(Z_n \le x) - \Phi(x)| \le C \frac{\rho}{\sigma^3 \sqrt{n}} $$
其中 $Z_n = \sqrt{n}(\bar{X}_n - \mu)/\sigma$，$x$ 是实数，$\Phi(x)$ 是标准正态分布的[累积分布函数 (CDF)](@entry_id:264700)。最新的研究成果已将普适常数 $C$ 的[上界](@entry_id:274738)压缩至 $0.4748$ 以下 [@problem_id:4957909]。

这个定理揭示了三个关键信息：
1.  **[收敛速度](@entry_id:146534)**：近似误差的衰减速度为 $n^{-1/2}$。这个速度是“最优”的，意味着对于某些分布，误差确实是以这个速率下降的。
2.  **分布形状的影响**：误差上界与一个无量纲的量 $\rho/\sigma^3$ 成正比。这个量可以看作是原始分布标准化后的偏度的一种度量。分布越对称、尾部越轻（$\rho/\sigma^3$ 越小），[正态近似](@entry_id:261668)就越快地变得准确。
3.  **非渐近性**：这是一个对任意 $n \ge 1$ 都成立的界，而不仅仅是一个极限性质。

除了提供[误差界](@entry_id:139888)限，我们还可以寻求一个比正态分布更精确的近似分布，这就是 **Edgeworth 展开 (Edgeworth expansion)** 的目标。Edgeworth 展开是 $Z_n$ 的 CDF（或 PDF）关于 $n^{-1/2}$ 的一个[渐近级数](@entry_id:168392)。它通过在正态分布的基础上增加修正项来捕捉原始分布的偏度和峰度等高阶特征。

通过对 $Z_n$ 的[特征函数](@entry_id:186820)进行更精确的展开，并进行[傅里叶逆变换](@entry_id:178300)，我们可以得到其 CDF $F_n(z)$ 的一阶 Edgeworth 展开：
$$ F_n(z) \approx \Phi(z) - \frac{\lambda_3}{6\sqrt{n}}(z^2 - 1)\phi(z) $$
其中 $\phi(z)$ 是标准正态概率密度函数 (PDF)，$\lambda_3 = \kappa_3/\sigma^3$ 是标准化的第三 **累积量 (cumulant)**，它等于分布的偏度系数。这个 $O(n^{-1/2})$ 的修正项直接与分布的偏度（由 $\lambda_3$ 体现）相关。如果分布是左偏的 ($\lambda_3  0$)，修正项会调整[正态近似](@entry_id:261668)，反之亦然。这个修正项包含了 $(z^2 - 1)\phi(z)$，它与标准正态 PDF 的二阶导数成正比，后者是第二阶 **Hermite 多项式** 的一种形式 [@problem_id:4957899]。

### 拓宽视野：[中心极限定理](@entry_id:143108)的推广

经典 CLT 的 [i.i.d. 假设](@entry_id:634392)在许多复杂的[统计模型](@entry_id:755400)中并不满足。幸运的是，中心极限定理的精神可以推广到更广泛的场景。

#### Lindeberg-Feller [中心极限定理](@entry_id:143108)

当随机变量是独立的但**非同分布**时，Lindeberg-Feller CLT 提供了一个强大的框架。这种情况常见于多中心临床研究或具有[异方差性](@entry_id:136378)的回归模型中。考虑一个 **三角阵列 (triangular array)** $\{X_{n,k}\}_{k=1, \dots, n; n \ge 1}$，其中每一行内的变量是独立的，$\mathbb{E}[X_{n,k}]=0$，$\operatorname{Var}(X_{n,k})=\sigma_{n,k}^2$。令 $S_n = \sum_{k=1}^n X_{n,k}$ 和 $s_n^2 = \sum_{k=1}^n \sigma_{n,k}^2$。

Lindeberg-Feller CLT 指出，如果 **Lindeberg 条件** 成立，则标准化总和 $S_n/s_n$ 依分布收敛于标准正态分布。Lindeberg 条件要求对于任意 $\epsilon > 0$：
$$ \lim_{n\to\infty} \frac{1}{s_n^2} \sum_{k=1}^n \mathbb{E}\left[X_{n,k}^2 \mathbf{1}\{|X_{n,k}| > \epsilon s_n\}\right] = 0 $$
其中 $\mathbf{1}\{\cdot\}$ 是[指示函数](@entry_id:186820)。这个条件在直觉上意味着，对于整个和的方差 $s_n^2$ 而言，来自任何单个随机变量尾部的贡献都是渐近可忽略的。换言之，没有任何一个变量的方差在总体中占据主导地位 [@problem_id:4986717]。

#### [鞅中心极限定理](@entry_id:198119)

当变量之间存在依赖性时，经典 CLT 及其直接推广不再适用。然而，对于特定类型的依赖结构，例如 **鞅差序列 (martingale difference sequence)**，CLT 仍然成立。在纵向生物统计学研究中，患者按顺序入组，每个新患者的数据可能依赖于之前所有患者的信息。如果第 $k$ 个患者的某个残差项 $X_k$ 在给定历史信息 $\mathcal{F}_{k-1}$ 的条件下的期望为零，即 $\mathbb{E}[X_k | \mathcal{F}_{k-1}] = 0$，则 $\{X_k, \mathcal{F}_k\}$ 构成一个[鞅](@entry_id:267779)差序列。

对于这类序列，总和 $S_n = \sum_{k=1}^n X_k$ 形成一个鞅。**[鞅中心极限定理](@entry_id:198119) (Martingale Central Limit Theorem, MCLT)** 指出，在满足两个核心条件时，$S_n$（或其标准化形式）的分布将收敛到正态分布：
1.  **可预测二次变差的收敛**：可预测二次变差 $\langle S \rangle_n = \sum_{k=1}^n \mathbb{E}[X_k^2 | \mathcal{F}_{k-1}]$ [依概率收敛](@entry_id:145927)于一个常数 $\sigma^2$。这可以看作是方差稳定条件的推广。
2.  **条件 Lindeberg 条件**：$\sum_{k=1}^n \mathbb{E}[X_k^2 \mathbf{1}\{|X_k| > \epsilon\} | \mathcal{F}_{k-1}]$ [依概率收敛](@entry_id:145927)于 $0$。这确保了单个项的贡献是渐近可忽略的。

在这些条件下，$S_n \xrightarrow{d} \mathcal{N}(0, \sigma^2)$ [@problem_id:4957876]。

#### [广义中心极限定理](@entry_id:262272)与[稳定分布](@entry_id:194434)

经典 CLT 及其上述推广都依赖于一个根本前提：方差是有限的。当这个条件被打破时会发生什么？例如，在分析某些医疗成本数据时，可能会观察到极端的“[重尾](@entry_id:274276)”现象，导致样本方差随样本量的增加而无休止地增长。

如果一个分布的尾部概率 $\mathbb{P}(|X| > x)$ 随 $x$ 的衰减慢于任何 $x^{-2}$ 的函数，那么其方差就是无穷大的。特别地，对于服从 **正则变化 (regularly varying)** 尾部，即 $\mathbb{P}(|X| > x) \sim c x^{-\alpha} L(x)$（其中 $L(x)$ 是缓变函数）的分布：
-   当 $\alpha \ge 2$ 时，方差有限，经典 CLT 适用。
-   当 $\alpha \in (0, 2)$ 时，方差无穷大，经典 CLT 失效。

在这种情况下，**[广义中心极限定理](@entry_id:262272) (Generalized Central Limit Theorem)** 指出，独立同分布变量的和，在适当的中心化和尺度变换后，其极限分布不再是正态分布，而是一类被称为 **$\alpha$-[稳定分布](@entry_id:194434) ($\alpha$-stable distribution)** 的分布。

对于 $\alpha \in (1, 2)$ 的情况，期望 $\mu$ 仍然是有限的。此时，正确的尺度因子不再是 $n^{1/2}$，而是 $n^{1/\alpha}$。由于 $\alpha  2$，所以 $1/\alpha > 1/2$，这意味着样本均值的波动比经典情况更大。具体来说，我们有：
$$ \frac{\sum_{i=1}^n X_i - n\mu}{a_n} \xrightarrow{d} S_\alpha $$
其中 $a_n$ 是一个满足 $n \mathbb{P}(|X| > a_n) \to \text{const}$ 的序列（其量级为 $n^{1/\alpha}$），$S_\alpha$ 是一个非高斯的 $\alpha$-[稳定分布](@entry_id:194434)。这也意味着，样本均值 $\bar{X}_n$ 仍然依概率收敛于 $\mu$（由强[大数定律](@entry_id:140915)保证），但其围绕 $\mu$ 的波动，即 $(\bar{X}_n - \mu)$，的衰减速度是 $n^{-(1-1/\alpha)}$，这比经典 CLT 的 $n^{-1/2}$ 速度要慢 [@problem_id:4845102]。

### 应用的延伸：多维 CLT 与 Delta 方法

中心极限定理的应用并不仅限于单变量。

#### 多元中心极限定理与 Cramér-Wold 方法

对于 $\mathbb{R}^d$ 空间中的 i.i.d. 随机向量序列 $\{\mathbf{X}_i\}$，其[均值向量](@entry_id:266544)为 $\boldsymbol{\mu}$，协方差矩阵为 $\boldsymbol{\Sigma}$。多元[中心极限定理](@entry_id:143108)指出：
$$ \sqrt{n}(\bar{\mathbf{X}}_n - \boldsymbol{\mu}) \xrightarrow{d} \mathcal{N}_d(\mathbf{0}, \boldsymbol{\Sigma}) $$
其中 $\mathcal{N}_d$ 是一个 $d$ 维[多元正态分布](@entry_id:175229)。

证明多元 CLT 的一个优雅而强大的工具是 **Cramér-Wold 方法**。该方法指出，一个随机向量序列 $Y_n$ [依分布收敛](@entry_id:275544)于 $Y$，当且仅当对于任意固定的向量 $t \in \mathbb{R}^d$，其一维投影 $t^\top Y_n$ [依分布收敛](@entry_id:275544)于 $t^\top Y$。因此，要证明多元 CLT，我们只需证明对于任意 $t \in \mathbb{R}^d$，标量随机变量 $t^\top (\sqrt{n}(\bar{\mathbf{X}}_n - \boldsymbol{\mu}))$ 收敛于 $t^\top \mathcal{N}_d(\mathbf{0}, \boldsymbol{\Sigma})$ 的分布。由于[线性变换](@entry_id:143080)不改变正态性，后者的分布是 $\mathcal{N}(0, t^\top \boldsymbol{\Sigma} t)$。而 $t^\top (\sqrt{n}(\bar{\mathbf{X}}_n - \boldsymbol{\mu}))$ 可以看作是标量随机变量 $t^\top \mathbf{X}_i$ 的标准化均值，因此可以应用一维 CLT 来证明。Cramér-Wold 方法将一个复杂的多维问题简化为无穷多个简单的一维问题 [@problem_id:3043375]。

#### Delta 方法

在数据分析中，我们常常对样本均值的某个函数 $g(\bar{X}_n)$ 感兴趣，例如，对神经元发放率取对数以稳定方差。**Delta 方法** 提供了一种确定 $g(\bar{X}_n)$ [渐近分布](@entry_id:272575)的通用技术。

假设 $g(x)$ 在点 $\mu$ 处可微，且 $g'(\mu) \neq 0$。根据一阶泰勒展开，当 $\bar{X}_n$ 接近 $\mu$ 时，我们有：
$$ g(\bar{X}_n) \approx g(\mu) + g'(\mu)(\bar{X}_n - \mu) $$
对上式重新整理并乘以 $\sqrt{n}$：
$$ \sqrt{n}(g(\bar{X}_n) - g(\mu)) \approx g'(\mu) \left[\sqrt{n}(\bar{X}_n - \mu)\right] $$
由于 $\sqrt{n}(\bar{X}_n - \mu) \xrightarrow{d} \mathcal{N}(0, \sigma^2)$，右侧是这个渐近正态变量的一个常数倍。根据[正态分布的性质](@entry_id:273225)，我们得到 Delta 方法的结论：
$$ \sqrt{n}(g(\bar{X}_n) - g(\mu)) \xrightarrow{d} \mathcal{N}(0, [g'(\mu)]^2 \sigma^2) $$
这个结果表明，经过变换后，统计量仍然是渐近正态的，但其方差被乘以了导数在均值处取值的平方。这为基于变换后数据的[统计推断](@entry_id:172747)提供了理论依据 [@problem_id:4145435]。