## 引言
二次扩张中[素数的分歧](@entry_id:634782)现象是[代数数论](@entry_id:148067)的基石。作为最简单的非平凡数[域扩张](@entry_id:153187)，二次域为我们提供了一个理想的“实验室”，以观察和理解在更一般域扩张中[素理想分解](@entry_id:197179)的复杂行为。当我们从有理[数域](@entry_id:155558) $\mathbb{Q}$ 步入二次域 $K$ 时，一个基本问题随之产生：一个有理素数 $p$ 在 $K$ 的整数环中会发生什么？它是否保持素性，还是会分解、甚至“重叠”？解答这个问题，正是[分歧理论](@entry_id:199385)的核心任务。

本文将系统地引导你穿越二次域[分歧理论](@entry_id:199385)的完整景观。在“**原理与机制**”一章中，我们将建立描述素数分解行为的基本框架，引入[分歧指数](@entry_id:186386)、[惯性次数](@entry_id:195604)等关键概念，并揭示[域判别式](@entry_id:198568)如何成为判断[分歧](@entry_id:193119)的“金标准”。随后，在“**应用与跨学科联系**”中，我们将展示这一理论的强大威力，从具体数域的计算实例，到它如何与[局部域](@entry_id:195717)理论、[类域论](@entry_id:155687)以及[解析数论](@entry_id:158402)等更高等的数学结构产生深刻共鸣。最后，通过“**动手实践**”部分，你将有机会亲手运用所学知识解决具体问题，从而将理论内化为技能。

现在，让我们从构建这一理论体系的基础——素数[理想分解](@entry_id:148948)的基本原理与机制——开始我们的探索之旅。

## 原理与机制

在[代数数论](@entry_id:148067)中，[数域](@entry_id:155558)的算术性质是核心研究对象。二次扩张作为最简单非平凡的数[域扩张](@entry_id:153187)，为我们理解更普遍的现象提供了一个理想的试验场。本章将深入探讨有理素数在二次扩张中的分解行为，特别是**[分歧](@entry_id:193119) (ramification)** 现象。我们将从基本定义出发，系统地建立起描述和预测[素数分解](@entry_id:198620)行为的理论框架，并揭示其背后的深刻机制。

### 素数[理想分解](@entry_id:148948)的基本概念

当我们从有理数域 $\mathbb{Q}$ 扩张到二次域 $K = \mathbb{Q}(\sqrt{d})$（其中 $d$ 为无平方因子的整数）时，有理[整数环](@entry_id:181003) $\mathbb{Z}$ 中的素数 $p$ 生成的理想 $(p) = p\mathbb{Z}$ 不再一定是 $K$ 的[整数环](@entry_id:181003) $\mathcal{O}_K$ 中的素理想。作为戴德金[整环](@entry_id:155321) (Dedekind domain)，$\mathcal{O}_K$ 中的每个理想都有唯一的[素理想分解](@entry_id:197179)。因此，理想 $p\mathcal{O}_K$ 会分解为 $\mathcal{O}_K$ 中若干个素理想的乘积。

这个分解过程由三个关键的[不变量](@entry_id:148850)来刻画 [@problem_id:3021871]：

1.  **[分歧指数](@entry_id:186386) (Ramification Index)** $e$：在 $p\mathcal{O}_K$ 的[素理想分解](@entry_id:197179)式 $p\mathcal{O}_K = \mathfrak{p}_1^{e_1} \mathfrak{p}_2^{e_2} \cdots \mathfrak{p}_g^{e_g}$ 中，素理想 $\mathfrak{p}_i$ 的指数 $e_i$ 称为其**[分歧指数](@entry_id:186386)**，记作 $e(\mathfrak{p}_i|p)$。它衡量了 $\mathfrak{p}_i$ 在分解中的“[重数](@entry_id:136466)”。如果对于某个 $i$，有 $e_i > 1$，我们就称素数 $p$ 在 $K$ 中是**分歧的 (ramified)**。

2.  **[惯性次数](@entry_id:195604) (Inertia Degree)** $f$：每个素理想 $\mathfrak{p}_i$ 都定义了一个剩[余域](@entry_id:139336) (residue field) $\mathcal{O}_K/\mathfrak{p}_i$。这个剩[余域](@entry_id:139336)是基域 $\mathbb{Q}$ 的剩[余域](@entry_id:139336) $\mathbb{Z}/p\mathbb{Z} = \mathbb{F}_p$ 的一个[有限扩张](@entry_id:152412)。这个[扩张的次数](@entry_id:151271) $[\mathcal{O}_K/\mathfrak{p}_i : \mathbb{F}_p]$ 称为 $\mathfrak{p}_i$ 的**[惯性次数](@entry_id:195604)**，记作 $f(\mathfrak{p}_i|p)$。它衡量了从 $\mathbb{F}_p$ 到 $\mathcal{O}_K/\mathfrak{p}_i$ 的“扩张程度”。

3.  **分解个数 (Number of Prime Factors)** $g$：在分解式中，不同的素[理想因子](@entry_id:137944) $\mathfrak{p}_i$ 的总个数。

这三个量并非相互独立，它们受到一个深刻的基本恒等式的约束。对于任意[有限扩张](@entry_id:152412) $L/K$，其次数为 $n=[L:K]$，$\mathcal{O}_K$ 中的一个素理想 $\mathfrak{p}$ 在 $\mathcal{O}_L$ 中的分解满足：
$$ \sum_{i=1}^{g} e(\mathfrak{P}_i|\mathfrak{p}) f(\mathfrak{P}_i|\mathfrak{p}) = n $$
其中 $\mathfrak{P}_i$ 是 $\mathcal{O}_L$ 中所有位于 $\mathfrak{p}$ 之上的素理想。

对于二次扩张 $K/\mathbb{Q}$，扩张次数 $n=2$。更重要的是，这是一个伽罗瓦扩张 (Galois extension)。在伽罗瓦扩张中，伽罗瓦群传递地作用于分解后的素理想集合上，这导致所有的[分歧指数](@entry_id:186386)都相等（即 $e_1 = \dots = e_g = e$），所有的[惯性次数](@entry_id:195604)也都相等（即 $f_1 = \dots = f_g = f$）。因此，上述求和公式简化为一个简洁的乘积形式 [@problem_id:3021871]：
$$ e \cdot f \cdot g = 2 $$
这个公式是研究二次域中素数分解的基石。由于 $e, f, g$ 都是正整数，这个方程的整数解只有三种可能。

### 素数分解行为的分类

根据 $efg=2$ 的三种整数解，我们可以将有理素数 $p$ 在二次域 $K$ 中的行为分为三类 [@problem_id:3021905]：

1.  **分裂 (Split)**：对应于 $(e,f,g) = (1,1,2)$。
    在这种情况下，理想 $p\mathcal{O}_K$ 分解为两个不同的素理想的乘积：
    $$ p\mathcal{O}_K = \mathfrak{p}_1 \mathfrak{p}_2, \quad \text{其中 } \mathfrak{p}_1 \neq \mathfrak{p}_2 $$
    这里[分歧指数](@entry_id:186386) $e=1$（因此 $p$ 是非[分歧](@entry_id:193119)的），[惯性次数](@entry_id:195604) $f=1$。$f=1$ 意味着剩余[域扩张](@entry_id:153187)是平凡的，即 $\mathcal{O}_K/\mathfrak{p}_i \cong \mathbb{F}_p$。

2.  **惰性 (Inert)**：对应于 $(e,f,g) = (1,2,1)$。
    在这种情况下，理想 $p\mathcal{O}_K$ 在 $\mathcal{O}_K$ 中保持为素理想：
    $$ p\mathcal{O}_K = \mathfrak{p} $$
    这里[分歧指数](@entry_id:186386) $e=1$（$p$ 也是非[分歧](@entry_id:193119)的），但[惯性次数](@entry_id:195604) $f=2$。这意味着剩[余域](@entry_id:139336) $\mathcal{O}_K/\mathfrak{p}$ 是 $\mathbb{F}_p$ 的一个二次扩张，即一个含有 $p^2$ 个元素的域 $\mathbb{F}_{p^2}$。

3.  **[分歧](@entry_id:193119) (Ramified)**：对应于 $(e,f,g) = (2,1,1)$。
    在这种情况下，理想 $p\mathcal{O}_K$ 分解为一个素理想的平方：
    $$ p\mathcal{O}_K = \mathfrak{p}^2 $$
    这里[分歧指数](@entry_id:186386) $e=2$，这正是“[分歧](@entry_id:193119)”一词的定义。[惯性次数](@entry_id:195604) $f=1$，意味着剩[余域](@entry_id:139336) $\mathcal{O}_K/\mathfrak{p}$ 同构于 $\mathbb{F}_p$。

这三种可能性穷尽了素数在二次域中的所有分解行为。接下来的问题是：对于一个给定的二次域 $K$ 和一个素数 $p$，我们如何预测它会呈现哪种行为？答案与一个[数域](@entry_id:155558)至关重要的[不变量](@entry_id:148850)——**[判别式](@entry_id:174614) (discriminant)**——紧密相连。

### [判别式](@entry_id:174614)的核心作用

数论中的一个基本定理指出：**一个有理素数 $p$ 在数域 $K$ 中[分歧](@entry_id:193119)，当且仅当 $p$ 整除 $K$ 的[域判别式](@entry_id:198568) $\Delta_K$**。这一定理将抽象的[分歧](@entry_id:193119)概念与一个可计算的量联系起来。为了使用这个判别式准则，我们必须首先学会如何计算它。

#### [整数环](@entry_id:181003)与[域判别式](@entry_id:198568)

[域判别式](@entry_id:198568) $\Delta_K$ 定义为 $K$ 的[整数环](@entry_id:181003) $\mathcal{O}_K$ 的任意一组**[整基](@entry_id:190217) (integral basis)** 的[判别式](@entry_id:174614)。对于二次域 $K = \mathbb{Q}(\sqrt{d})$（其中 $d$ 为无平方因子整数），其[整数环](@entry_id:181003) $\mathcal{O}_K$ 和判别式 $\Delta_K$ 的结构取决于 $d$ 模 $4$ 的余数 [@problem_id:3021873]。

一个元素 $\alpha \in K$ 是[代数整数](@entry_id:151672)，当且仅当它在 $\mathbb{Q}$ 上的迹 $\operatorname{Tr}_{K/\mathbb{Q}}(\alpha)$ 和范 $\operatorname{N}_{K/\mathbb{Q}}(\alpha)$ 都是有理整数。对于 $\alpha = x+y\sqrt{d}$ ($x,y \in \mathbb{Q}$)，我们有 $\operatorname{Tr}(\alpha) = 2x$ 和 $\operatorname{N}(\alpha) = x^2-dy^2$。通过分析这两个量为整数的条件，可以导出 $\mathcal{O}_K$ 的完整结构：

-   **情况 1: $d \equiv 2, 3 \pmod{4}$**
    此时，$\mathcal{O}_K$ 中的元素必须有整数坐标，即 $\mathcal{O}_K = \{m+n\sqrt{d} \mid m,n \in \mathbb{Z}\} = \mathbb{Z}[\sqrt{d}]$。一组[整基](@entry_id:190217)是 $\{1, \sqrt{d}\}$。
    [判别式](@entry_id:174614)由[迹配对](@entry_id:187369)[矩阵的行列式](@entry_id:148198)给出：
    $$ \Delta_K = \det \begin{pmatrix} \operatorname{Tr}(1 \cdot 1) & \operatorname{Tr}(1 \cdot \sqrt{d}) \\ \operatorname{Tr}(\sqrt{d} \cdot 1) & \operatorname{Tr}(\sqrt{d} \cdot \sqrt{d}) \end{pmatrix} = \det \begin{pmatrix} 2 & 0 \\ 0 & 2d \end{pmatrix} = 4d $$

-   **情况 2: $d \equiv 1 \pmod{4}$**
    此时，$\mathcal{O}_K$ 的元素可以是半整数坐标的形式，具体为 $\mathcal{O}_K = \{m+n\frac{1+\sqrt{d}}{2} \mid m,n \in \mathbb{Z}\} = \mathbb{Z}[\frac{1+\sqrt{d}}{2}]$。一组[整基](@entry_id:190217)是 $\{1, \frac{1+\sqrt{d}}{2}\}$。
    [判别式](@entry_id:174614)计算如下：
    $$ \Delta_K = \det \begin{pmatrix} \operatorname{Tr}(1) & \operatorname{Tr}(\frac{1+\sqrt{d}}{2}) \\ \operatorname{Tr}(\frac{1+\sqrt{d}}{2}) & \operatorname{Tr}((\frac{1+\sqrt{d}}{2})^2) \end{pmatrix} = \det \begin{pmatrix} 2 & 1 \\ 1 & \frac{1+d}{2} \end{pmatrix} = 2(\frac{1+d}{2}) - 1 = d $$

总结如下：
$$ \Delta_K = \begin{cases} d & \text{若 } d \equiv 1 \pmod{4} \\ 4d & \text{若 } d \equiv 2, 3 \pmod{4} \end{cases} $$
例如，对于 $K=\mathbb{Q}(\sqrt{-77})$，由于 $-77 \equiv 3 \pmod{4}$，其判别式为 $\Delta_K = 4(-77) = -308$。因此，在 $K$ 中分歧的素数恰好是 $308 = 2^2 \cdot 7 \cdot 11$ 的素因子，即 $2, 7, 11$。对于这些素数，它们的分解模式必然是 $(e,f,g)=(2,1,1)$ [@problem_id:3022161]。

### 确定分解行为的机制

我们已经知道如何通过[判别式](@entry_id:174614)识别[分歧素数](@entry_id:183288)。那么对于不[分歧](@entry_id:193119)的素数（即不整除 $\Delta_K$ 的素数），它们是分裂还是惰性呢？

#### Dedekind-Kummer 定理

一个强大的计算工具是 **Dedekind-Kummer 定理**。该定理指出，如果 $K = \mathbb{Q}(\alpha)$，其中 $\alpha$ 是一个[代数整数](@entry_id:151672)，其在 $\mathbb{Z}$ 上的极小多项式为 $f(x)$。对于一个不整除指标 $[\mathcal{O}_K : \mathbb{Z}[\alpha]]$ 的素数 $p$，理想 $p\mathcal{O}_K$ 的分解模式与多项式 $f(x)$ 在模 $p$ 的有限域 $\mathbb{F}_p$ 上的分解模式完全相同。

具体来说，若 $\bar{f}(x) = f(x) \pmod p$ 在 $\mathbb{F}_p[x]$ 中分解为 $\bar{f}(x) = \bar{g}_1(x)^{e_1} \cdots \bar{g}_k(x)^{e_k}$，则 $p\mathcal{O}_K$ 对应地分解为 $p\mathcal{O}_K = \mathfrak{P}_1^{e_1} \cdots \mathfrak{P}_k^{e_k}$。

-   $p$ 分裂 $\iff \bar{f}(x)$ 分解为两个不同的一次因式。
-   $p$ 惰性 $\iff \bar{f}(x)$ 在 $\mathbb{F}_p[x]$ 中不可约。
-   $p$ 分歧 $\iff \bar{f}(x)$ 在 $\mathbb{F}_p$ 的[代数闭包](@entry_id:151964)中有[重根](@entry_id:151486)，即 $\bar{f}(x)$ 与其导数 $\bar{f}'(x)$ 有公共根。

让我们应用此定理于 $K = \mathbb{Q}(\sqrt{d})$ [@problem_id:3021877]。

-   对于奇素数 $p$：
    我们可以选择 $\alpha = \sqrt{d}$，其极小多项式为 $f(x) = x^2-d$。指标 $[\mathcal{O}_K : \mathbb{Z}[\sqrt{d}]]$ 为 $1$ 或 $2$，因此不被任何奇素数 $p$ 整除。定理适用。
    $\bar{f}(x) = x^2 - \bar{d} \pmod p$。其导数为 $2x$。由于 $p$ 是奇素数，$2 \not\equiv 0 \pmod p$，导数的唯一根是 $x=0$。因此，$p$ 分歧当且仅当 $x=0$ 也是 $\bar{f}(x)$ 的根，即 $0^2 - \bar{d} \equiv 0 \pmod p$，这意味着 $p|d$。这与我们通过[判别式](@entry_id:174614)得到的结论（奇[素数分歧](@entry_id:198850)当且仅当 $p|d$）一致。
    对于不分歧的奇素数 $p$（即 $p \nmid d$），$x^2 \equiv d \pmod p$ 是否有解决定了分解行为。这正是[勒让德符号](@entry_id:194530) (Legendre symbol) $\left(\frac{d}{p}\right)$ 的定义：
    -   $p$ 分裂 $\iff \left(\frac{d}{p}\right) = 1$。
    -   $p$ 惰性 $\iff \left(\frac{d}{p}\right) = -1$。

-   对于素数 $p=2$：
    情况变得复杂，因为当 $d \equiv 1 \pmod 4$ 时，指标 $[\mathcal{O}_K : \mathbb{Z}[\sqrt{d}]] = 2$，此时 Dedekind-Kummer 定理对 $f(x)=x^2-d$ 不再适用。
    -   若 $d \equiv 2, 3 \pmod 4$，指标为 $1$，定理适用。$\bar{f}(x) = x^2-d \pmod 2$。若 $d \equiv 2 \pmod 4$，$d$ 为偶数，$\bar{f}(x) \equiv x^2 \pmod 2$。若 $d \equiv 3 \pmod 4$，$d$ 为奇数，$\bar{f}(x) \equiv x^2-1 \equiv (x-1)^2 \pmod 2$。两种情况都有[重根](@entry_id:151486)，因此 $p=2$ 分歧。
    -   若 $d \equiv 1 \pmod 4$，我们必须选择一个使得 $\mathcal{O}_K = \mathbb{Z}[\alpha]$ 的生成元，即 $\alpha = \frac{1+\sqrt{d}}{2}$。其极小多项式为 $g(x) = x^2 - x + \frac{1-d}{4}$ [@problem_id:3021903]。现在指标为 $1$，定理对所有素数都适用。
        $\bar{g}(x) = x^2 - x + \frac{1-d}{4} \pmod 2$。
        -   若 $d \equiv 1 \pmod 8$，则 $\frac{1-d}{4}$ 是偶数，$\bar{g}(x) \equiv x^2-x \equiv x(x-1) \pmod 2$。有两个不同根，因此 $p=2$ **分裂**。
        -   若 $d \equiv 5 \pmod 8$，则 $\frac{1-d}{4}$ 是奇数，$\bar{g}(x) \equiv x^2-x+1 \pmod 2$。此多项式在 $\mathbb{F}_2$ 上不可约，因此 $p=2$ **惰性**。

#### 克罗内克符号的统一表述

上述所有关于非[分歧素数](@entry_id:183288)的结论可以被优雅地统一在**克罗内克符号 (Kronecker symbol)** $\left(\frac{\Delta_K}{\cdot}\right)$ 之下 [@problem_id:3027704]。

**定理**：一个有理素数 $p$ 在二次域 $K$ 中的分解行为由 $\left(\frac{\Delta_K}{p}\right)$ 的值决定：
-   若 $\left(\frac{\Delta_K}{p}\right) = 1$, 则 $p$ **分裂**。
-   若 $\left(\frac{\Delta_K}{p}\right) = -1$, 则 $p$ **惰性**。
-   若 $\left(\frac{\Delta_K}{p}\right) = 0$, 则 $p$ **分歧**。

这个定理完美地概括了所有情况。例如，对于 $p=2$，当 $d \equiv 1 \pmod 4$ 时，$\Delta_K = d$。
-   若 $d \equiv 1 \pmod 8$，$\left(\frac{\Delta_K}{2}\right) = \left(\frac{d}{2}\right) = 1$，$p=2$ 分裂。
-   若 $d \equiv 5 \pmod 8$，$\left(\frac{\Delta_K}{2}\right) = \left(\frac{d}{2}\right) = -1$，$p=2$ 惰性。
这与我们通过 Dedekind-Kummer 定理得到的结果完全吻合 [@problem_id:3021858]。

对于由奇素数组成的[合数](@entry_id:263553)模 $m$，[雅可比符号](@entry_id:191224) (Jacobi symbol) $\left(\frac{\Delta_K}{m}\right) = \prod_{p|m} \left(\frac{\Delta_K}{p}\right)$。值得注意的是，$\left(\frac{\Delta_K}{m}\right)=1$ 并不意味着所有整除 $m$ 的素数都分裂，而只意味着惰性的素因子个数为偶数 [@problem_id:3027704]。

### 更深层的结构

[分歧](@entry_id:193119)现象还可以从更抽象的[代数结构](@entry_id:137052)中理解。

#### [差理想](@entry_id:204193)

**[差理想](@entry_id:204193) (different ideal)** $\mathfrak{D}_{K/\mathbb{Q}}$ 是一个深刻地蕴含了[分歧](@entry_id:193119)信息的 $\mathcal{O}_K$ 理想。它的定义与[迹映射](@entry_id:194370)有关，其逆（称为余[差理想](@entry_id:204193)）为：
$$ \mathfrak{D}^{-1}_{K/\mathbb{Q}} = \{x \in K : \operatorname{Tr}_{K/\mathbb{Q}}(x\mathcal{O}_K) \subseteq \mathbb{Z}\} $$
对于二次域 $K=\mathbb{Q}(\sqrt{d})$，可以证明[差理想](@entry_id:204193)是一个[主理想](@entry_id:152760)，其生成元与我们之前用于 Dedekind-Kummer 定理的极小多项式 $f(x)$ 的导数 $f'(\alpha)$ 直接相关 [@problem_id:3021895]。
-   若 $d \equiv 2, 3 \pmod 4$, $\mathcal{O}_K=\mathbb{Z}[\sqrt{d}]$, $f(x)=x^2-d$, $\mathfrak{D}_{K/\mathbb{Q}} = (f'(\sqrt{d})) = (2\sqrt{d})$。
-   若 $d \equiv 1 \pmod 4$, $\mathcal{O}_K=\mathbb{Z}[\frac{1+\sqrt{d}}{2}]$, $f(x)=x^2-x+\frac{1-d}{4}$, $\mathfrak{D}_{K/\mathbb{Q}} = (f'(\frac{1+\sqrt{d}}{2})) = (\sqrt{d})$。

差[理想的范数](@entry_id:155476)等于[域判别式](@entry_id:198568)的[绝对值](@entry_id:147688)，$N(\mathfrak{D}_{K/\mathbb{Q}}) = |\Delta_K|$。更重要的是，整除[差理想](@entry_id:204193)的素理想，恰好是那些位于[分歧](@entry_id:193119)的有理素数之上的[素理想](@entry_id:154026)。这为[分歧](@entry_id:193119)与[判别式](@entry_id:174614)之间的联系提供了更深层的解释。

#### 无穷[素数的分歧](@entry_id:634782)

[分歧](@entry_id:193119)的概念不仅适用于由有理素数 $p$ 定义的有限素位 (finite places)，也适用于由通常的[绝对值](@entry_id:147688)定义的**无穷素位 (infinite prime)**。$\mathbb{Q}$ 只有一个无穷素位，对应于嵌入 $\mathbb{Q} \hookrightarrow \mathbb{R}$。它在二次域 $K$ 中的行为取决于 $K$ 是否有实嵌入 [@problem_id:3021892]。

这由 $d$ 的符号决定：
-   **[实二次域](@entry_id:636720) ($d > 0$)**：
    $K$ 有两个不同的实嵌入（$a+b\sqrt{d} \mapsto a+b\sqrt{d}$ 和 $a-b\sqrt{d}$）。我们称 $K$ 的**符号差 (signature)** 为 $(r_1, r_2)=(2,0)$，其中 $r_1$ 是实嵌入个数，$r_2$ 是共轭[复嵌入](@entry_id:189961)的对数。此时，我们说无穷素数在 $K$ 中是**分裂**的（非[分歧](@entry_id:193119)的）。这对应于[张量积分解](@entry_id:138873) $K \otimes_{\mathbb{Q}} \mathbb{R} \cong \mathbb{R} \times \mathbb{R}$。[判别式](@entry_id:174614)的符号为 $(-1)^{r_2} = (-1)^0=1$，即 $\Delta_K > 0$。

-   **[虚二次域](@entry_id:197298) ($d < 0$)**：
    $K$ 没有实嵌入，只有一对共轭的[复嵌入](@entry_id:189961)。符号差为 $(r_1, r_2)=(0,1)$。此时，我们说无穷素数在 $K$ 中是**[分歧](@entry_id:193119)**的。这对应于 $K \otimes_{\mathbb{Q}} \mathbb{R} \cong \mathbb{C}$，它是一个域。判别式的符号为 $(-1)^{r_2} = (-1)^1=-1$，即 $\Delta_K < 0$。

因此，[判别式](@entry_id:174614)的符号揭示了无穷[素数的分歧](@entry_id:634782)行为，而[判别式](@entry_id:174614)的素因子揭示了有限[素数的分歧](@entry_id:634782)行为。至此，我们完整地描绘了二次域中各类素数（包括无穷素数）的分解原理与判断机制。