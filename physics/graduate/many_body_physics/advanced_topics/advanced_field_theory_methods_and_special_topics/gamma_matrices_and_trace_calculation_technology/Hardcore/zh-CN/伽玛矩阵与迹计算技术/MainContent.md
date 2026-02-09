## 引言
在相对论性量子力学的宏伟框架中，狄拉克伽玛矩阵不仅是描述自旋为1/2的费米子（如电子和夸克）的数学语言，更是量子场论（QFT）计算的基石。从预测粒子散射的概率到探索物质的基本对称性，几乎所有与费米子相关的计算都不可避免地要处理由这些矩阵构成的复杂表达式。然而，直接处理这些矩阵乘积既繁琐又容易出错，这构成了一个显著的知识应用障碍：我们如何才能系统、高效地从这些抽象的矩阵链中提取出可与实验相比对的物理预测？

本文旨在填补这一鸿沟，为读者提供一套关于伽玛矩阵代数及其迹计算技术的完整指南。我们将超越伽玛矩阵的表象，专注于其普适的代数结构，这使得计算结果具有不依赖于特定表示的洛伦兹协变性。通过本文的学习，读者将掌握一套强大的计算工具，能够自信地应对量子场论中遇到的各种迹算问题。

文章分为三个核心部分：首先，在“**原理与机制**”一章中，我们将深入探讨伽玛矩阵的定义性特征——克利福德代数，并由此推导出一系列核心的代数恒等式和迹计算规则，包括对费曼斜杠符号和手性矩阵 $\gamma^5$ 的讨论。接着，在“**应用与交叉学科联系**”一章中，我们将展示这些技术如何在量子电动力学（QED）、标准模型乃至更前沿的物理研究中发挥关键作用，将抽象的理论转化为具体的物理预测。最后，通过“**动手实践**”环节，读者将有机会通过解决具体问题来巩固和应用所学知识，从而真正内化这些强大的计算方法。

## 原理与机制

本章深入探讨狄拉克伽玛矩阵的代数结构及其迹计算技术。这些矩阵是相对论性量子力学和量子场论的基石，为描述费米子的行为提供了数学框架。掌握这些矩阵的代数性质和迹的计算方法，对于计算散射截面、衰变率等可观测物理量至关重要。

### 伽玛矩阵的基本代数性质

#### 核心定义：克利福德代数

伽玛矩阵 $\gamma^\mu$ 并非由其具体数值表示来定义，而是由它们所满足的基本代数关系——**克利福德代数 (Clifford Algebra)**——来定义。在维度为 $d$ 的时空中，对于 $\mu, \nu = 0, 1, \dots, d-1$，其反对易关系为：

$$
\{\gamma^\mu, \gamma^\nu\} \equiv \gamma^\mu\gamma^\nu + \gamma^\nu\gamma^\mu = 2\eta^{\mu\nu}I
$$

在此，$\eta^{\mu\nu}$ 是闵可夫斯基度规张量（我们约定其符号为 $(+,-,-,\dots,-)$），而 $I$ 是伽玛矩阵作用的旋量空间中的单位矩阵，其维度取决于时空维度 $d$。在计算中，这个单位矩阵 $I$ 常常被省略。这个反对易关系是所有伽玛矩阵代数运算的出发点。

一个直接的推论是单个伽玛矩阵的平方。通过在上述关系中设置 $\mu = \nu$（此处不对 $\mu$ 求和），我们得到：

$$
\gamma^\mu\gamma^\mu + \gamma^\mu\gamma^\mu = 2(\gamma^\mu)^2 = 2\eta^{\mu\mu}I
$$

因此，

$$
(\gamma^\mu)^2 = \eta^{\mu\mu}I
$$

这意味着 $\gamma^0$ 的平方是 $+I$，而所有空间分量（$\mu=1, 2, \dots, d-1$）的平方是 $-I$。

#### 爱因斯坦求和约定下的矩阵收缩

在量子场论的计算中，我们经常遇到伽玛矩阵链中洛伦兹指标的收缩。利用爱因斯坦求和约定（一个上指标和一个下指标成对出现时，表示对该指标所有可能的值求和），我们可以推导一些极为有用的恒等式。

最基本的收缩是 $\gamma^\mu \gamma_\mu$。通过使用度规张量降低指标 $\gamma_\mu = \eta_{\mu\nu}\gamma^\nu$，我们得到：

$$
\gamma^\mu \gamma_\mu = \eta_{\mu\nu} \gamma^\mu \gamma^\nu = \frac{1}{2} \eta_{\mu\nu} (\gamma^\mu \gamma^\nu + \gamma^\nu \gamma^\mu) = \frac{1}{2} \eta_{\mu\nu} (2\eta^{\mu\nu}I) = \eta_{\mu\nu}\eta^{\mu\nu}I
$$

由于 $\eta_{\mu\nu}\eta^{\mu\nu} = \delta^\mu_\mu$ 是时空的维度 $d$，我们得到一个普适的恒等式：

$$
\gamma^\mu \gamma_\mu = d \cdot I
$$

例如，在一个6维时空中，这个收缩的结果就是 $6I$ [@problem_id:1142801]。这个简单的结果威力强大，可以快速简化看似复杂的表达式。例如，对于一个全收缩的八个伽玛矩阵的乘积 $\gamma^\mu \gamma^\nu \gamma^\rho \gamma^\sigma \gamma_\sigma \gamma_\rho \gamma_\nu \gamma_\mu$，我们可以从内向外逐对应用此规则：$\gamma^\sigma \gamma_\sigma = dI$，表达式变为 $d \cdot \gamma^\mu \gamma^\nu \gamma^\rho \gamma_\rho \gamma_\nu \gamma_\mu$。重复此过程，最终得到 $d^4 I$ [@problem_id:1142781]。

另一个在圈图计算中常见的结构是 "三明治" 型收缩，如 $\gamma^\mu \gamma^\rho \gamma_\mu$。我们可以通过使用反对易关系来简化它：

$$
\gamma^\mu \gamma^\rho \gamma_\mu = (2\eta^{\mu\rho}I - \gamma^\rho\gamma^\mu)\gamma_\mu = 2\eta^{\mu\rho}\gamma_\mu - \gamma^\rho(\gamma^\mu\gamma_\mu) = 2\gamma^\rho - d\gamma^\rho = (2-d)\gamma^\rho
$$

这个结果表明，将一个伽玛矩阵用一对收缩的伽玛矩阵“夹”起来，会得到一个正比于原伽玛矩阵的项，系数依赖于时空维度 $d$ [@problem_id:1142814]。通过迭代使用这个技巧，我们可以简化更长的矩阵链。例如，表达式 $\gamma^\mu \gamma^\nu \gamma^\rho \gamma_\nu \gamma_\mu$ 可以分步简化：首先简化内部的 $\gamma^\nu \gamma^\rho \gamma_\nu = (2-d)\gamma^\rho$，则整个表达式变为 $(2-d)\gamma^\mu \gamma^\rho \gamma_\mu$。再次应用该规则，我们得到最终结果 $(2-d)^2 \gamma^\rho$ [@problem_id:1142809]。

#### 费曼斜杠符号及其性质

理查德·费曼引入了一种极为便利的记法，称为**费曼斜杠符号 (Feynman slash notation)**，它将一个四维矢量 $a^\mu$ 与伽玛矩阵的内积写为：

$$
\not{a} \equiv a_\mu \gamma^\mu
$$

由于矢量分量 $a_\mu$ 是标量，它们与伽玛矩阵可以交换位置。利用这个记法，克利福德代数的核心关系可以被重写。例如，考虑两个任意矢量 $a$ 和 $b$：

$$
\not{a}\not{b} + \not{b}\not{a} = a_\mu b_\nu \gamma^\mu \gamma^\nu + b_\nu a_\mu \gamma^\nu \gamma^\mu = a_\mu b_\nu (\gamma^\mu \gamma^\nu + \gamma^\nu \gamma^\mu) = a_\mu b_\nu (2\eta^{\mu\nu}I) = 2(a \cdot b)I
$$

其中 $a \cdot b = a_\mu b^\mu = \eta_{\mu\nu}a^\mu b^\nu$ 是两个四维矢量的洛伦兹标量积。这个恒等式 $\not{a}\not{b} + \not{b}\not{a} = 2(a \cdot b)I$ 是进行伽玛矩阵计算时最常用的工具之一 [@problem_id:1142744]。

当两个矢量相同时，我们得到一个特别重要的结果：

$$
(\not{p})^2 = \not{p}\not{p} = \frac{1}{2}(\not{p}\not{p} + \not{p}\not{p}) = \frac{1}{2}(2(p \cdot p)I) = p^2 I
$$

这个关系式 $(\not{p})^2 = p^2 I$ 表明，斜杠矢量矩阵的平方是一个与单位矩阵成正比的简单标量。这个性质有一个优雅的推论，即关于 $\not{p}$ 矩阵的行列式。由于 $(\not{p})^2 = p^2 I$，$\not{p}$ 的任何特征值 $\lambda$ 必须满足 $\lambda^2 = p^2$，因此特征值为 $\pm\sqrt{p^2}$。在四维时空中，伽玛矩阵是 $4 \times 4$ 的，可以证明每个特征值都出现两次。因此，行列式是所有特征值的乘积：

$$
\det(\not{p}) = (\sqrt{p^2})(\sqrt{p^2})(-\sqrt{p^2})(-\sqrt{p^2}) = (p^2)^2
$$

这是一个普适的结论，对于任何四维矢量 $p^\mu$ 都成立 [@problem_id:1142707]。

### 手性矩阵 $\gamma^5$ 及其作用 (在 $D=4$ 维)

#### 定义与核心性质

在四维时空中，除了四个基本的伽玛矩阵 $\gamma^\mu$ 外，我们还定义了第五个伽玛矩阵，即**手性矩阵 (chirality matrix)** $\gamma^5$：

$$
\gamma^5 \equiv i\gamma^0\gamma^1\gamma^2\gamma^3
$$

这个定义中的因子 $i$ 确保了 $\gamma^5$ 的两个关键性质：
1.  **它与所有四个 $\gamma^\mu$ 反对易**：$\{\gamma^5, \gamma^\mu\} = 0$ 对所有的 $\mu=0,1,2,3$ 成立。
2.  **它的平方是单位矩阵**：$(\gamma^5)^2 = I$。

第一个性质是其最重要的特征。它可以直接推广到任何斜杠矢量上，因为 $\not{p}$ 是 $\gamma^\mu$ 的线性组合：

$$
\{\gamma^5, \not{p}\} = p_\mu \{\gamma^5, \gamma^\mu\} = p_\mu \cdot 0 = 0
$$

这表明 $\gamma^5$ 与任何斜杠矢量都反对易 [@problem_id:1142643]。这个性质在构建弱相互作用的 V-A 理论等手性理论中起着核心作用。

#### 维度与 $\gamma^5$ 的存在性

值得注意的是，一个与所有 $\gamma^\mu$ 都反对易的非平凡矩阵（即 "$\gamma^5$-like" 矩阵）的存在性，是时空维度的函数。它只在**偶数**维度的时空中存在。

我们可以通过考虑候选矩阵 $\Gamma = \gamma^0\gamma^1\cdots\gamma^{d-1}$ 来理解这一点。将 $\Gamma$ 与任意一个 $\gamma^\mu$ 对易，需要将 $\gamma^\mu$ 穿过另外 $d-1$ 个不同的伽玛矩阵，每次交换都会产生一个负号。因此，我们有：

$$
\Gamma \gamma^\mu = (\gamma^0\cdots\gamma^{d-1})\gamma^\mu = (-1)^{d-1} \gamma^\mu (\gamma^0\cdots\gamma^{d-1}) = (-1)^{d-1} \gamma^\mu \Gamma
$$

-   如果 $d$ 是偶数，则 $d-1$ 是奇数，$\Gamma \gamma^\mu = -\gamma^\mu \Gamma$。$\Gamma$ 与所有 $\gamma^\mu$ 反对易。
-   如果 $d$ 是奇数，则 $d-1$ 是偶数，$\Gamma \gamma^\mu = +\gamma^\mu \Gamma$。$\Gamma$ 与所有 $\gamma^\mu$ 对易。

在奇数维度下，根据舒尔引理 (Schur's Lemma) 的一个推论，任何与所有伽玛矩阵（在一个不可约表示中）都对易的矩阵必然正比于单位矩阵 $I$。因此，在奇数维度下，$\Gamma$ 正比于 $I$，它显然不满足反对易关系。这意味着在奇数维度下，不可能构造一个非平凡的、与所有 $\gamma^\mu$ 都反对易的 $\gamma^5$ 矩阵 [@problem_id:1142690]。这一事实是理解为什么许多涉及手性的标准恒等式仅在四维（或偶数维）时空中成立的关键。

### 伽玛矩阵乘积的代数

#### 乘积的分解

处理伽玛矩阵乘积的一个强大技巧，是将其分解为对称和反对称的部分。任何两个伽玛矩阵的乘积都可以写成：

$$
\gamma^\mu\gamma^\nu = \frac{1}{2}(\gamma^\mu\gamma^\nu + \gamma^\nu\gamma^\mu) + \frac{1}{2}(\gamma^\mu\gamma^\nu - \gamma^\nu\gamma^\mu) = \eta^{\mu\nu}I + \frac{1}{2}[\gamma^\mu, \gamma^\nu]
$$

右边的第二项，即对易子，定义了旋量表示下洛伦兹群的生成元，记为 $\sigma^{\mu\nu} = \frac{i}{2}[\gamma^\mu, \gamma^\nu]$。因此，我们有 $[\gamma^\mu, \gamma^\nu] = -2i\sigma^{\mu\nu}$。代入上式，我们得到一个非常有用的分解：

$$
\gamma^\mu\gamma^\nu = \eta^{\mu\nu}I - i\sigma^{\mu\nu}
$$

这个分解让我们可以将任意两个斜杠矢量的乘积 $\not{p}\not{q}$ 展开到由 16 个基元 $\Gamma_A = \{I, \gamma^\mu, \sigma^{\mu\nu}, i\gamma^5\gamma^\mu, \gamma^5\}$ 构成的完备基上。

$$
\not{p}\not{q} = p_\mu q_\nu \gamma^\mu \gamma^\nu = p_\mu q_\nu (\eta^{\mu\nu}I - i\sigma^{\mu\nu}) = (p \cdot q)I - i p_\mu q_\nu \sigma^{\mu\nu}
$$

这个表达式清楚地显示了 $\not{p}\not{q}$ 的标量部分是 $p \cdot q$，张量部分由反对称系数张量 $-\frac{i}{2}(p_\mu q_\nu - p_\nu q_\mu)$ 给出 [@problem_id:1142871]。一个有趣的推论是，由于 $\gamma^5$ 与 $\gamma^\mu$ 反对易，可以证明它与 $\sigma^{\mu\nu}$ 对易，因此也与 $[\not{p}, \not{q}] = \not{p}\not{q} - \not{q}\not{p} = -2i p_\mu q_\nu \sigma^{\mu\nu}$ 对易 [@problem_id:1142720]。

#### 高阶恒等式

对于更长的伽玛矩阵链，也存在类似的分解。在四维时空中，三个伽玛矩阵的乘积可以被完全分解为：

$$
\gamma^\mu\gamma^\nu\gamma^\rho = \eta^{\mu\nu}\gamma^\rho - \eta^{\mu\rho}\gamma^\nu + \eta^{\nu\rho}\gamma^\mu + i\epsilon^{\mu\nu\rho\sigma}\gamma_\sigma \gamma^5
$$

其中 $\epsilon^{\mu\nu\rho\sigma}$ 是完全反对称的列维-奇维塔符号（约定 $\epsilon^{0123}=+1$）。这个恒等式 [@problem_id:1142806] 在处理涉及三个伽玛矩阵乘积的复杂表达式时非常有用，它将乘积分解为对称的度规张量项和完全反对称的轴矢量项。

这些分解技巧的背后是伽玛矩阵代数的完备性。在四维时空中，16个矩阵 $\Gamma_A$ 构成了 $4 \times 4$ 矩阵空间的一个完备基。这意味着任何 $4 \times 4$ 矩阵都可以表示为它们的线性组合。这一性质是**菲尔兹恒等式 (Fierz Identities)** 的基础，后者用于重排涉及四个费米子场的双线性型乘积，例如将 $(\bar{a}\gamma^\mu b)(\bar{c}\gamma_\mu d)$ 形式的项改写为 $(\bar{a}\Gamma^A d)(\bar{c}\Gamma'_A b)$ 形式的线性组合。这些恒等式在研究四费米子相互作用（如弱衰变）时至关重要 [@problem_id:1142634] [@problem_id:1142808]。

### 迹技术：通往可计算预测的关键

在量子场论中，为了得到不依赖于旋量具体选择的物理结果（如散射截面），我们通常需要对费米子线上的伽玛矩阵链取迹 (Trace)。迹运算将矩阵映射到一个标量，从而消除了旋量指标。

#### 迹的基本性质与恒等式

迹运算具有两个基本性质：**线性** ($\text{Tr}(A+B) = \text{Tr}(A)+\text{Tr}(B)$) 和**循环性** ($\text{Tr}(ABC) = \text{Tr}(BCA) = \text{Tr}(CAB)$)。所有迹的计算都依赖于这两个性质以及克利福德代数。

-   **奇数个伽玛矩阵的迹**：在存在 $\gamma^5$ 矩阵的偶数维时空（如 $D=4$）中，任意奇数个伽玛矩阵乘积的迹为零。
    $$
    \text{Tr}(\gamma^{\mu_1} \gamma^{\mu_2} \cdots \gamma^{\mu_{2n+1}}) = 0
    $$
    证明如下：令 $M = \gamma^{\mu_1} \cdots \gamma^{\mu_{2n+1}}$。插入单位矩阵 $I = (\gamma^5)^2$ 并利用循环性：
    $$
    \text{Tr}(M) = \text{Tr}(M (\gamma^5)^2) = \text{Tr}(\gamma^5 M \gamma^5)
    $$
    然后将 $\gamma^5$ 穿过 $M$ 中的每一个 $\gamma^\mu$ 矩阵，由于有奇数个，每次反对易都会产生一个负号，总共得到一个负号：
    $$
    \text{Tr}(\gamma^5 M \gamma^5) = \text{Tr}((-1)^{2n+1} M (\gamma^5)^2) = -\text{Tr}(M)
    $$
    因此，$\text{Tr}(M) = -\text{Tr}(M)$，这意味着 $\text{Tr}(M)=0$。然而，这个结论在奇数维度时空中不成立，因为不存在这样的 $\gamma^5$ 矩阵 [@problem_id:1142712]。

-   **单个伽玛矩阵的迹**：$\text{Tr}(\gamma^\mu)=0$。这可以看作是上述规则在 $n=0$ 时的特例。但需要注意的是，这个性质并非对所有克利福德代数的表示都成立。例如，在一维时空中，$d=1$，$(\gamma^0)^2=I_1=1$，一个合法的表示是 $\gamma^0 = 1$（$1 \times 1$ 矩阵），其迹显然不为零 [@problem_id:1142786]。然而，在物理应用中（$D \ge 2$）所使用的伽玛矩阵表示中，此性质通常成立。

#### 偶数个伽玛矩阵的迹

偶数个伽玛矩阵的迹通常不为零，并且可以表示为度规张量的组合。

-   **两个伽玛矩阵的迹**：
    $$
    \text{Tr}(\gamma^\mu\gamma^\nu) = \text{Tr}(2\eta^{\mu\nu}I - \gamma^\nu\gamma^\mu) = 2\eta^{\mu\nu}\text{Tr}(I) - \text{Tr}(\gamma^\mu\gamma^\nu)
    $$
    在四维时空中，伽玛矩阵是 $4 \times 4$ 的，所以 $\text{Tr}(I)=4$。因此，$2\text{Tr}(\gamma^\mu\gamma^\nu) = 2\eta^{\mu\nu} \cdot 4$，即：
    $$
    \text{Tr}(\gamma^\mu\gamma^\nu) = 4\eta^{\mu\nu}
    $$

-   **四个伽玛矩阵的迹**：这是最常用也是最重要的迹公式之一。通过反复应用反对易关系，可以推导出：
    $$
    \text{Tr}(\gamma^\mu\gamma^\nu\gamma^\rho\gamma^\sigma) = 4(\eta^{\mu\nu}\eta^{\rho\sigma} - \eta^{\mu\rho}\eta^{\nu\sigma} + \eta^{\mu\sigma}\eta^{\nu\rho})
    $$
    这个公式是将费曼图计算结果转化为可观测量的核心。例如，在计算康普顿散射等过程中，会出现形如 $\text{Tr}(\not{p}_1\not{p}_2\not{p}_3\not{p}_4)$ 的项。通过展开斜杠符号并应用上述公式，可以得到：
    $$
    \text{Tr}(\not{p}_1\not{p}_2\not{p}_3\not{p}_4) = 4[(p_1 \cdot p_2)(p_3 \cdot p_4) - (p_1 \cdot p_3)(p_2 \cdot p_4) + (p_1 \cdot p_4)(p_2 \cdot p_3)]
    $$
    这个表达式完全由四维动量的标量积构成 [@problem_id:1142779]。
    
    在维度正规化等技术中，我们需要将此公式推广到任意 $d$ 维。此时，矩阵的维度 $N = 2^{\lfloor d/2 \rfloor}$，所以 $\text{Tr}(I)=N$。迹公式中的整体因子 4 变为 $N$ [@problem_id:1142742]：
    $$
    \text{Tr}(\gamma^\mu\gamma^\nu\gamma^\rho\gamma^\sigma) = 2^{\lfloor d/2 \rfloor}(\eta^{\mu\nu}\eta^{\rho\sigma} - \eta^{\mu\rho}\eta^{\nu\sigma} + \eta^{\mu\sigma}\eta^{\nu\rho})
    $$

#### 涉及 $\gamma^5$ 的迹恒等式 (在 $D=4$ 维)

包含 $\gamma^5$ 的迹有其独特的规则，这些规则在研究宇称破缺和手性对称性时至关重要。

-   **$\text{Tr}(\gamma^5) = 0$**。证明：$\text{Tr}(\gamma^5) = \text{Tr}(\gamma^5(\gamma^0)^2) = \text{Tr}(\gamma^0\gamma^5\gamma^0) = \text{Tr}(-\gamma^5(\gamma^0)^2) = -\text{Tr}(\gamma^5)$，因此迹为零。这个结果也意味着，例如，`Tr(γ⁰γ¹γ²γ³) = Tr(-iγ⁵) = -iTr(γ⁵)=0`，这是一个实数 [@problem_id:1142696]。

-   **$\text{Tr}(\gamma^5 \gamma^\mu \gamma^\nu) = 0$**。这个恒等式表明 $\gamma^5$ 与两个伽玛矩阵乘积的迹为零。一个严谨的证明方法是引入第三个与 $\mu, \nu$ 不同的指标 $\rho$，并利用 $\gamma^\rho$ 反对易穿过其他矩阵的性质，最终证明该迹等于其自身的相反数，故必须为零 [@problem_id:1142731]。
    这一规则可以推广：只要与 $\gamma^5$ 相乘的伽玛矩阵个数少于4个，其迹就为零。

-   **$\text{Tr}(\gamma^5 \gamma^\mu \gamma^\nu \gamma^\rho \gamma^\sigma) = -4i\epsilon^{\mu\nu\rho\sigma}$**。这是第一个包含 $\gamma^5$ 且不为零的重要迹公式。它将四个伽玛矩阵与手性矩阵的迹和完全反对称的列维-奇维塔符号联系起来。注意，如果指标 $\mu, \nu, \rho, \sigma$ 中有任何重复，$\epsilon$ 符号将为零，迹也为零，这与克利福德代数的结果是一致的。

掌握这些规则后，我们可以计算更复杂的表达式。例如，考虑计算 $\text{Tr}[(\not{a} + i \not{b} \gamma_5)(\not{c} + i \not{d} \gamma_5)]$。展开乘积并逐项取迹 [@problem_id:1142892]：
1.  $\text{Tr}(\not{a}\not{c}) = a_\mu c_\nu \text{Tr}(\gamma^\mu\gamma^\nu) = 4a_\mu c_\nu \eta^{\mu\nu} = 4(a \cdot c)$。
2.  $\text{Tr}(i\not{a}\not{d}\gamma_5) = i a_\mu d_\nu \text{Tr}(\gamma^\mu\gamma^\nu\gamma_5) = 0$。
3.  $\text{Tr}(i\not{b}\gamma_5\not{c}) = i b_\mu c_\nu \text{Tr}(\gamma^\mu\gamma_5\gamma^\nu) = i b_\mu c_\nu \text{Tr}(-\gamma_5\gamma^\mu\gamma^\nu)=0$。
4.  $\text{Tr}(-\not{b}\gamma_5\not{d}\gamma_5) = -b_\mu d_\nu \text{Tr}(\gamma^\mu\gamma_5\gamma^\nu\gamma_5) = -b_\mu d_\nu \text{Tr}(-\gamma^\mu\gamma^\nu\gamma_5\gamma_5) = b_\mu d_\nu \text{Tr}(\gamma^\mu\gamma^\nu) = 4(b \cdot d)$。

将所有项相加，我们得到一个简洁的结果：$4(a \cdot c + b \cdot d)$。这个例子完美地展示了如何组合运用各种迹规则来解决实际问题。