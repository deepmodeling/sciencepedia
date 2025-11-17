## 引言
当我们从熟悉的有理[数域](@entry_id:155558) $\mathbb{Q}$ 迈向更广阔的[代数数域](@entry_id:637592) $K$ 时，一个根本性的问题随之产生：我们应当如何推广“整数”这一概念？在有理数中，[整数环](@entry_id:181003) $\mathbb{Z}$ 构成了算术的基石。同样，在每个[数域](@entry_id:155558) $K$ 中，我们也希望找到一个扮演类似角色的特殊子环，即**[代数整数](@entry_id:151672)环** $\mathcal{O}_K$。然而，这个推广过程并非一帆风顺，我们很快会发现，整数环 $\mathbb{Z}$ 最宝贵的性质——唯一[因子分解定理](@entry_id:749213)——在许多[代数整数](@entry_id:151672)环中不再成立。这一挑战促使19世纪的数学家发展出了一套更深刻的理论，用“理想”的语言重建了算术的和谐。

本文旨在系统地介绍数域的[整数环](@entry_id:181003)这一[代数数论](@entry_id:148067)的中心对象。我们将分为三个章节，引领读者逐步深入其丰富的结构与应用：

- **第一章：原理与机制** 将详细阐述[代数整数](@entry_id:151672)环的定义、其作为自由$\mathbb{Z}$-模的加法结构（[整基](@entry_id:190217)），以及其复杂的乘法结构，重点探讨从元素分解的失效到[理想唯一分解](@entry_id:636803)的恢复过程，并介绍[单位群](@entry_id:184012)的结构。

- **第二章：应用与[交叉](@entry_id:147634)学科联系** 将展示这些抽象理论如何应用于解决具体问题，例如丢番图方程，并揭示其与伽罗瓦理论、[模论](@entry_id:139410)乃至代数几何等其他数学分支的深刻联系。

- **第三章：动手实践** 将通过一系列精心设计的问题，帮助读者巩固理解，将理论知识转化为解决实际计算和证明的能力。

通过本次学习，你将掌握[代数整数](@entry_id:151672)环的核心性质，理解唯一[因子分解](@entry_id:150389)如何通过理想得到挽救，并领略这一理论在现代数学中的强大威力与优美之处。

## 原理与机制

在数域的研究中，从有理数 $\mathbb{Q}$ 扩展到更广阔的[代数数域](@entry_id:637592) $K$ 时，我们面临着一个核心挑战：整数的概念应如何推广？正如 $\mathbb{Z}$ 在 $\mathbb{Q}$ 中扮演着基础算术结构的角色，我们在每个[数域](@entry_id:155558) $K$ 中也寻求一个与之对应的特殊[子环](@entry_id:154194)，它将继承 $\mathbb{Z}$ 的诸多优良代数性质。这个被称为**[代数整数](@entry_id:151672)环**（ring of integers）的结构，记作 $\mathcal{O}_K$，是代数数论的中心研究对象。本章将系统地阐述 $\mathcal{O}_K$ 的基本原理和内在机制，揭示其作为 $\mathbb{Z}$ 的自然推广所具备的深刻[代数结构](@entry_id:137052)。

### [代数整数](@entry_id:151672)环：定义与结构

#### [代数整数](@entry_id:151672)的定义

我们首先需要精确定义什么是“整数”的推广。一个复数 $\alpha$ 如果是某个以整数为系数的**[首一多项式](@entry_id:152311)**（monic polynomial）的根，那么它就被称为**[代数整数](@entry_id:151672)**（algebraic integer）。换言之，存在一个形如 $p(x) = x^n + c_{n-1}x^{n-1} + \dots + c_0$ 的多项式，其中所有系数 $c_i$ 均为整数（$c_i \in \mathbb{Z}$），使得 $p(\alpha) = 0$ [@problem_id:1818871]。

这个定义与**代数数**（algebraic number）的定义有细微但关键的区别。代数数是整系数多项式（不要求首一）的根，这等价于它是以有理数为系数的[首一多项式](@entry_id:152311)的根。所有[代数整数](@entry_id:151672)都是代数数，但反之不然。例如，$\frac{1}{2}$ 是[代数数](@entry_id:150888)，因为它是[首一多项式](@entry_id:152311) $x - \frac{1}{2}$ 的根，其系数在 $\mathbb{Q}$ 中。然而，可以证明 $\frac{1}{2}$ 并非任何整系数[首一多项式](@entry_id:152311)的根，因此它不是一个[代数整数](@entry_id:151672)。实际上，一个有理数是[代数整数](@entry_id:151672)当且仅当它是一个普通整数 [@problem_id:3023017]。

#### [整数环](@entry_id:181003) $\mathcal{O}_K$

对于一个给定的[数域](@entry_id:155558) $K$（即 $\mathbb{Q}$ 的[有限域](@entry_id:142106)扩张），其**[整数环](@entry_id:181003)** $\mathcal{O}_K$ 定义为 $K$ 中所有[代数整数](@entry_id:151672)的集合。从[抽象代数](@entry_id:145216)的角度看，$\mathcal{O}_K$ 是 $\mathbb{Z}$ 在 $K$ 中的**[整闭](@entry_id:149392)包**（integral closure），即 $K$ 中所有在 $\mathbb{Z}$ 上整的元素的集合 [@problem_id:3023017]。

一个深刻且基础的定理指出，$\mathcal{O}_K$ 不仅仅是一个集合，它确实构成了一个环。这意味着任意两个 $K$ 中的[代数整数](@entry_id:151672)，它们的和与积依然是[代数整数](@entry_id:151672)。例如，我们知道 $\sqrt{2}$ 和 $\sqrt{3}$ 都是[代数整数](@entry_id:151672)（它们分别是 $x^2-2=0$ 和 $x^2-3=0$ 的根），因此 $1+\sqrt{2}$ 也是（它是 $x^2-2x-1=0$ 的根）。它们的和 $\alpha = 1 + \sqrt{2} + \sqrt{3}$ 也必定是一个[代数整数](@entry_id:151672)。我们可以通过构造其最小多项式来验证这一点。通过一系列代数变形，可以发现 $\alpha$ 是首一整系数多项式 $x^4 - 4x^3 - 4x^2 + 16x - 8 = 0$ 的根，从而直接证实了其[代数整数](@entry_id:151672)的身份 [@problem_id:1818871]。

需要注意的是，虽然 $\mathcal{O}_K$ 是一个环，但它通常不是一个域。这是因为一个非单位的[代数整数](@entry_id:151672)的逆元不一定是[代数整数](@entry_id:151672)。例如，$2 \in \mathcal{O}_K$（对于任何 $K$），但其[逆元](@entry_id:140790) $\frac{1}{2}$ 如前所述，通常不是[代数整数](@entry_id:151672) [@problem_id:3023017]。一个[代数整数](@entry_id:151672)的逆元也是[代数整数](@entry_id:151672)，当且仅当这个元素是 $\mathcal{O}_K$ 中的一个**单位**（unit）。

#### 加法结构：[整基](@entry_id:190217)

从加法结构的角度看，[整数环](@entry_id:181003) $\mathcal{O}_K$ 具有非常规则和优美的结构。作为一个加法群，$\mathcal{O}_K$ 是一个**自由阿贝尔群**（free abelian group），其秩等于[数域](@entry_id:155558)的次数 $n = [K:\mathbb{Q}]$。这意味着存在一组基底 $\omega_1, \dots, \omega_n \in \mathcal{O}_K$，称为**[整基](@entry_id:190217)**（integral basis），使得 $\mathcal{O}_K$ 中的每个元素 $\alpha$ 都可以唯一地表示为这些基元的整[线性组合](@entry_id:154743)：
$$ \alpha = c_1 \omega_1 + \dots + c_n \omega_n, \quad c_i \in \mathbb{Z} $$
这表明 $\mathcal{O}_K$ 是一个秩为 $n$ 的**[有限生成](@entry_id:156447)$\mathbb{Z}$-模** [@problem_id:3022904]。

对于一个由[代数整数](@entry_id:151672) $\alpha$ 生成的数域 $K=\mathbb{Q}(\alpha)$，一个自然的问题是，集合 $\{1, \alpha, \dots, \alpha^{n-1}\}$ 是否构成一个[整基](@entry_id:190217)？答案是：不一定。由 $\alpha$ 生成的环 $\mathbb{Z}[\alpha]$ 只是 $\mathcal{O}_K$ 的一个[子环](@entry_id:154194)，在代数上称为一个**序**（order）。在某些情况下，$\mathbb{Z}[\alpha]$ 就是完整的[整数环](@entry_id:181003) $\mathcal{O}_K$，但在另一些情况下，它只是一个[真子集](@entry_id:152276)。

一个经典的例子是二次域。对于由无平方因子整数 $d$ 生成的二次域 $K = \mathbb{Q}(\sqrt{d})$，其整数环 $\mathcal{O}_K$ 的[整基](@entry_id:190217)取决于 $d$ 模 $4$ 的余数：
- 如果 $d \equiv 2, 3 \pmod{4}$，则 $\mathcal{O}_K = \mathbb{Z}[\sqrt{d}]$，[整基](@entry_id:190217)为 $\{1, \sqrt{d}\}$。
- 如果 $d \equiv 1 \pmod{4}$，则 $\mathcal{O}_K$ 严格大于 $\mathbb{Z}[\sqrt{d}]$。此时，一个额外的[代数整数](@entry_id:151672) $\omega = \frac{1+\sqrt{d}}{2}$ 存在于 $\mathcal{O}_K$ 中，但它显然不在 $\mathbb{Z}[\sqrt{d}]$ 内。例如，对于 $K=\mathbb{Q}(\sqrt{13})$（因为 $13 \equiv 1 \pmod{4}$），元素 $\omega = \frac{1+\sqrt{13}}{2}$ 的最小多项式是 $x^2 - x - 3 = 0$，这是一个整系数[首一多项式](@entry_id:152311)，因此 $\omega$ 是一个[代数整数](@entry_id:151672)。但由于其系数不是整数，它不属于 $\mathbb{Z}[\sqrt{13}]$ [@problem_id:1818872]。在这种情况下，$\mathcal{O}_K$ 的一个[整基](@entry_id:190217)是 $\{1, \frac{1+\sqrt{13}}{2}\}$。

#### 判别式与指标

如何判断 $\mathbb{Z}[\alpha]$ 是否为完整的 $\mathcal{O}_K$？**[判别式](@entry_id:174614)**（discriminant）为此提供了关键工具。对于[数域](@entry_id:155558) $K$ 的任意一组 $n$ 个元素，可以定义它们的判别式。[整基](@entry_id:190217)的判别式是一个不依赖于基选择的域[不变量](@entry_id:148850)，记为 $D_K$ 或 $\text{disc}(\mathcal{O}_K)$。对于序 $\mathbb{Z}[\alpha]$，其基 $\{1, \alpha, \dots, \alpha^{n-1}\}$ 的判别式恰好等于 $\alpha$ 的最小多项式 $f(x)$ 的判别式 $\text{disc}(f)$。

这两个[判别式](@entry_id:174614)通过一个重要公式相联系：
$$ \text{disc}(\mathbb{Z}[\alpha]) = [\mathcal{O}_K : \mathbb{Z}[\alpha]]^2 \cdot \text{disc}(\mathcal{O}_K) $$
其中 $[\mathcal{O}_K : \mathbb{Z}[\alpha]]$ 是加法群的**指标**（index），表示[陪集](@entry_id:147145) $\mathcal{O}_K / \mathbb{Z}[\alpha]$ 的大小。这个公式表明，任何整除指标的素数，也必须整除[多项式判别式](@entry_id:154854) $\text{disc}(f)$。这为我们从一个已知的序 $\mathbb{Z}[\alpha]$ 出发，系统地寻找完整的[整数环](@entry_id:181003) $\mathcal{O}_K$ 提供了一条途径。我们只需检查那些整除 $\text{disc}(f)$ 的素数，看是否存在更大的包含 $\mathbb{Z}[\alpha]$ 的序 [@problem_id:1818861]。例如，对于 $f(x) = x^3 - x^2 - 2x - 8$，其[判别式](@entry_id:174614)为 $-2012 = -4 \cdot 503 = -2^2 \cdot 503$。这意味着，如果 $\mathbb{Z}[\alpha]$ 不是完整的[整数环](@entry_id:181003)，那么指标 $[\mathcal{O}_K : \mathbb{Z}[\alpha]]$ 的素因子只可能来自集合 $\{2, 503\}$ [@problem_id:1818861]。

### 乘法结构：单位与因子分解

#### [单位群](@entry_id:184012) $\mathcal{O}_K^\times$

[整数环](@entry_id:181003)的乘法结构比加法结构要复杂得多。我们首先关注其中的可[逆元](@entry_id:140790)素，即**单位**。$\mathcal{O}_K$ 中所有单位构成的[乘法群](@entry_id:155975)记为 $\mathcal{O}_K^\times$。**[狄利克雷单位定理](@entry_id:155550)**（Dirichlet's Unit Theorem）是描述这一[群结构](@entry_id:146855)的基石。该定理指出，$\mathcal{O}_K^\times$ 是一个[有限生成阿贝尔群](@entry_id:156372)，其结构为：
$$ \mathcal{O}_K^\times \cong \mu(K) \times \mathbb{Z}^{r_1+r_2-1} $$
其中 $\mu(K)$ 是 $K$ 中[单位根](@entry_id:143302)构成的[有限循环群](@entry_id:147298)，而 $r_1$ 是 $K$ 的**实嵌入**（real embeddings）数目，$r_2$ 是**共轭[复嵌入](@entry_id:189961)**（pairs of complex embeddings）的对数。数域的次数 $n$ 与这两个数的关系是 $n = r_1 + 2r_2$。

$\mathcal{O}_K^\times$ 的秩 $r = r_1+r_2-1$ 是一个核心[不变量](@entry_id:148850)。为了计算它，我们需要确定 $r_1$ 和 $r_2$。如果 $K = \mathbb{Q}(\alpha)$，其中 $\alpha$ 是不[可约多项式](@entry_id:148759) $p(x)$ 的根，那么 $r_1$ 正是 $p(x)$ 的实根个数，而 $2r_2$ 是其虚根个数。例如，对于由不[可约多项式](@entry_id:148759) $p(x) = x^5 - 5x + 1$ 的根生成的数域 $K$，其次数 $n=5$。通过微积分方法分析 $p'(x)$ 的零点，可以确定 $p(x)$ 有 3 个实根和 2 个共轭[复根](@entry_id:172941)。因此，$r_1=3, r_2=1$，[单位群的秩](@entry_id:150706)为 $r = 3+1-1=3$ [@problem_id:1788504]。这个秩与 $\mathcal{O}_K$ 作为 $\mathbb{Z}$-模的秩 $n=5$ 是截然不同的概念 [@problem_id:3022904]。

#### [唯一因子分解的失效](@entry_id:155196)

整数环 $\mathbb{Z}$ 最重要的性质之一是**唯一[因子分解定理](@entry_id:749213)**（[算术基本定理](@entry_id:146420)），即每个整数可以唯一地分解为素数的乘积。我们自然希望这种性质能够推广到 $\mathcal{O}_K$。然而，历史表明，这通常是不成立的。

一个经典的例子发生在二次域 $K = \mathbb{Q}(\sqrt{-5})$ 中，其[整数环](@entry_id:181003)是 $\mathcal{O}_K = \mathbb{Z}[\sqrt{-5}]$。考虑元素 $6$ 的分解：
$$ 6 = 2 \cdot 3 = (1 + \sqrt{-5})(1 - \sqrt{-5}) $$
可以证明，这里的四个因子 $2, 3, 1+\sqrt{-5}, 1-\sqrt{-5}$ 都是 $\mathcal{O}_K$ 中的**不可约元素**（irreducible element），即它们不能再分解为两个非单位的乘积。同时，它们彼此之间并非**相伴**（associate）关系（即相差一个单位因子，这里的单位只有 $\pm 1$）。因此，我们得到了两种本质上不同的将 $6$ 分解为不可约元素的方式。这表明 $\mathcal{O}_K$ 不是一个**唯一因子分解[整环](@entry_id:155321)**（Unique Factorization Domain, UFD）[@problem_id:3010834]。

#### 补救：理想的唯一[因子分解](@entry_id:150389)

[唯一因子分解的失效](@entry_id:155196)是19世纪数论发展的一个重大障碍。 Ernst Kummer 和 Richard Dedekind 最终通过引入**理想**（ideal）的概念，以一种更深刻的方式恢复了唯一性。他们证明，虽然元素的[唯一分解](@entry_id:152313)可能失败，但[理想的唯一分解](@entry_id:154997)永远成立。

[整数环](@entry_id:181003) $\mathcal{O}_K$ 是一类特殊的环，称为**戴德金[整环](@entry_id:155321)**（Dedekind domain）。戴德金[整环](@entry_id:155321)的定义性质之一就是：环中的每个非零真理想都可以唯一地（不计顺序）分解为**素理想**（prime ideal）的乘积 [@problem_id:3021231]。

让我们回到 $\mathbb{Z}[\sqrt{-5}]$ 的例子。元素 $2, 3, 1+\sqrt{-5}, 1-\sqrt{-5}$ 虽然是不可约的，但它们生成的**主理想** $(2), (3), (1+\sqrt{-5}), (1-\sqrt{-5})$ 却不是[素理想](@entry_id:154026)。它们可以进一步分解为[素理想](@entry_id:154026)的乘积：
- $(2) = \mathfrak{p}_2^2$，其中 $\mathfrak{p}_2 = (2, 1+\sqrt{-5})$
- $(3) = \mathfrak{p}_3 \mathfrak{q}_3$，其中 $\mathfrak{p}_3 = (3, 1+\sqrt{-5})$, $\mathfrak{q}_3 = (3, 1-\sqrt{-5})$
- $(1+\sqrt{-5}) = \mathfrak{p}_2 \mathfrak{p}_3$
- $(1-\sqrt{-5}) = \mathfrak{p}_2 \mathfrak{q}_3$

现在，我们再来看理想 $(6)$ 的分解。无论是从 $(2)(3)$ 出发，还是从 $(1+\sqrt{-5})(1-\sqrt{-5})$ 出发，我们都得到了相同的唯一[素理想分解](@entry_id:197179)：
$$ (6) = (2)(3) = (\mathfrak{p}_2^2)(\mathfrak{p}_3 \mathfrak{q}_3) = \mathfrak{p}_2^2 \mathfrak{p}_3 \mathfrak{q}_3 $$
$$ (6) = (1+\sqrt{-5})(1-\sqrt{-5}) = (\mathfrak{p}_2 \mathfrak{p}_3)(\mathfrak{p}_2 \mathfrak{q}_3) = \mathfrak{p}_2^2 \mathfrak{p}_3 \mathfrak{q}_3 $$
这样，唯一性在理想的层面上得到了完美的恢复。元[素分解](@entry_id:198620)的非唯一性，根源在于不可约元素生成的理想可能不是素理想 [@problem_id:3010834]。

### [素理想分解](@entry_id:197179)的实践

#### 有理素数的分解

[理想唯一分解](@entry_id:636803)理论的核心应用在于研究有理素数 $p$ 在 $\mathcal{O}_K$ 中如何分解。给定一个素数 $p \in \mathbb{Z}$，它在 $\mathcal{O}_K$ 中生成的主理想 $p\mathcal{O}_K$ 会分解为一系列[素理想](@entry_id:154026)的乘积：
$$ p\mathcal{O}_K = \mathfrak{p}_1^{e_1} \mathfrak{p}_2^{e_2} \cdots \mathfrak{p}_g^{e_g} $$
这里的 $\mathfrak{p}_i$ 是 $\mathcal{O}_K$ 中互不相同的素理想，它们都“位于”$p$ 之上（即 $\mathfrak{p}_i \cap \mathbb{Z} = (p)$）。每个[素理想](@entry_id:154026) $\mathfrak{p}_i$ 都有两个重要的[不变量](@entry_id:148850)：
- **[分歧指数](@entry_id:186386)**（ramification index）$e_i$：它在分解式中出现的幂次。
- **剩余次数**（residue degree）$f_i$：定义为商环构成的[有限域](@entry_id:142106)的扩张次数 $f_i = [\mathcal{O}_K/\mathfrak{p}_i : \mathbb{Z}/p\mathbb{Z}]$。

这些[不变量](@entry_id:148850)受一个基本恒[等式约束](@entry_id:175290)：
$$ \sum_{i=1}^{g} e_i f_i = n = [K:\mathbb{Q}] $$
这个公式是研究[素数分解](@entry_id:198620)行为的基石 [@problem_id:3021231]。

#### 惰性、分裂与分歧

根据分解方式的不同，我们称有理素数 $p$ 在 $K$ 中有三种基本行为：
1.  **惰性**（inert）：$p\mathcal{O}_K$ 保持为一个素理想（即 $g=1, e_1=1, f_1=n$）。
2.  **分裂**（split）：$p\mathcal{O}_K$ 分解为多个不同的[素理想](@entry_id:154026)（$g > 1$）。一个特别重要的情形是**完全分裂**（splits completely），此时 $p\mathcal{O}_K$ 分解为 $n$ 个不同的[素理想](@entry_id:154026)，且每个理想的 $e_i=1, f_i=1$ [@problem_id:3021231]。
3.  **[分歧](@entry_id:193119)**（ramify）：至少有一个[分歧指数](@entry_id:186386) $e_i > 1$。注意，分歧不一定意味着只有一个素因子（即“完全分歧”）[@problem_id:3021231]。

素数的分解行为与商环 $\mathcal{O}_K/p\mathcal{O}_K$ 的结构密切相关。这个[商环](@entry_id:148632)是一个整环（从而没有零因子）当且仅当 $p\mathcal{O}_K$ 是一个素理想，即 $p$ 是惰性的。如果 $p$ 分裂或[分歧](@entry_id:193119)，那么 $p\mathcal{O}_K$ 不是[素理想](@entry_id:154026)，此时[商环](@entry_id:148632) $\mathcal{O}_K/p\mathcal{O}_K$ 将含有非零的零因子 [@problem_id:1818874]。

对于二次域 $K=\mathbb{Q}(\sqrt{d})$，奇素数 $p$ 的分解行为可以由**[勒让德符号](@entry_id:194530)** $(\frac{d}{p})$ 简单判定：
- $(\frac{d}{p}) = 1 \iff p$ 分裂。
- $(\frac{d}{p}) = -1 \iff p$ 惰性。
- $(\frac{d}{p}) = 0 \iff p$ [分歧](@entry_id:193119)。

例如，在 $K=\mathbb{Q}(\sqrt{-5})$ 中，对于素数 $3$ 和 $7$，我们计算[勒让德符号](@entry_id:194530) $(\frac{-5}{3})=1$ 和 $(\frac{-5}{7})=1$，表明它们都在 $\mathcal{O}_K$ 中分裂。因此，商环 $\mathcal{O}_K/3\mathcal{O}_K$ 和 $\mathcal{O}_K/7\mathcal{O}_K$ 都含有[零因子](@entry_id:151051) [@problem_id:1818874]。

#### [理想的范数](@entry_id:155476)与类群

**[理想的范数](@entry_id:155476)**（norm of an ideal）$\mathfrak{a}$ 定义为其商环的大小，即 $N(\mathfrak{a}) = |\mathcal{O}_K/\mathfrak{a}|$。对于一个位于 $p$ 之上的素理想 $\mathfrak{p}$，其范数与剩余次数的关系为 $N(\mathfrak{p}) = p^{f}$ [@problem_id:3021231]。

$\mathcal{O}_K$ 是不是一个 UFD，取决于其所有理想是否都是[主理想](@entry_id:152760)。为了量化这种偏离，我们引入**理想类群**（ideal class group）$Cl(K)$ 的概念。这是一个[有限阿贝尔群](@entry_id:136632)，其元素是 $\mathcal{O}_K$ 的理想“类”。它的阶 $h_K = |Cl(K)|$ 称为**[类数](@entry_id:156164)**（class number）。$h_K=1$ 当且仅当 $\mathcal{O}_K$ 是一个[主理想整环](@entry_id:152359)（PID），进而当且仅当它是一个唯一因子分解整环。

**[闵可夫斯基界](@entry_id:154247)**（Minkowski bound）为计算[类数](@entry_id:156164)提供了一个强大的工具。它保证每个理想类中都存在一个范数不超过某个特定界限的理想。通过分析范数较小的[素理想](@entry_id:154026)的行为，我们就可以确定类[群的生成元](@entry_id:137215)及其结构。例如，在 $\mathbb{Z}[\sqrt{-5}]$ 中，[闵可夫斯基界](@entry_id:154247)约为 $2.848$。我们只需研究范数为 $2$ 的[素理想](@entry_id:154026) $\mathfrak{p}_2 = (2, 1+\sqrt{-5})$。可以证明这个理想不是主理想，但它的平方 $\mathfrak{p}_2^2 = (2)$ 是[主理想](@entry_id:152760)。这意味着 $\mathfrak{p}_2$ 在[类群](@entry_id:182524)中的阶是 $2$，从而推导出[类数](@entry_id:156164) $h_K=2$ [@problem_id:3010834]。

### 几何视角：整数格

[代数数论](@entry_id:148067)的深刻之处在于它与几何学的优美联系。通过**[典范嵌入](@entry_id:267644)**（canonical embedding），我们可以将抽象的数域 $K$ 映射到一个具体的[欧氏空间](@entry_id:138052)中。

设 $K$ 有 $r_1$ 个实嵌入 $\sigma_i$ 和 $r_2$ 对共轭[复嵌入](@entry_id:189961) $(\tau_j, \bar{\tau}_j)$。我们可以定义一个嵌入映射 $\iota: K \to \mathbb{R}^{r_1} \times \mathbb{C}^{r_2}$。通过将每个 $\mathbb{C}$ 等同于 $\mathbb{R}^2$（通过 $z \mapsto (\text{Re}(z), \text{Im}(z))$），我们得到了一个从 $K$ 到 $\mathbb{R}^n$（其中 $n=r_1+2r_2$）的映射。

在这个几何图像下，整数环 $\mathcal{O}_K$ 展现为一个 $\mathbb{R}^n$ 中的满秩**格**（lattice），即一个离散的、具有周期性结构的加法[子群](@entry_id:146164)。这个格的一个**基本区域**（fundamental domain）的体积，即格的[协体积](@entry_id:186549)（covolume），与[数域的判别式](@entry_id:200799) $D_K$ 有着惊人的联系 [@problem_id:1818857]：
$$ \text{vol}(\mathbb{R}^n / \iota(\mathcal{O}_K)) = 2^{-r_2} \sqrt{|D_K|} $$
这个公式将一个纯代数的量（判别式）与一个纯几何的量（体积）联系起来，是数论中代数与几何交融之美的典范。它不仅提供了对判别式的几何直观，也成为证明[狄利克雷单位定理](@entry_id:155550)和计算类数的闵可夫斯基理论的基石。

综上所述，[数域](@entry_id:155558)的整数环 $\mathcal{O}_K$ 是一个具有丰富结构的代数对象。其加法结构是一个自由 $\mathbb{Z}$-模，乘法结构则由[单位群](@entry_id:184012)和理想的唯一[因子分解](@entry_id:150389)来刻画。对[素理想分解](@entry_id:197179)行为的研究，以及从几何角度将其视为一个格，共同构成了现代[代数数论](@entry_id:148067)的理论核心。