## 引言
在初等数论中，[算术基本定理](@entry_id:146420)保证了每个整数都能唯一地分解为素数的乘积，这一性质构成了我们对整数结构理解的基石。然而，当我们将研究对象从有理整数 $\mathbb{Z}$ 扩展到更广泛的[代数数域](@entry_id:637592)的整数环时，这个美好的唯一[因子分解](@entry_id:150389)性质时常会失效。例如，在环 $\mathbb{Z}[\sqrt{-5}]$ 中，数字 $6$ 就存在两种截然不同的[因子分解](@entry_id:150389)。这一发现暴露了我们直观算术知识的局限性，并提出了一个深刻的问题：我们如何在一个更广阔的代数世界中重建算术的秩序？

本文旨在系统地回答这一问题，核心工具便是“理想”这一强大的代数概念。通过引入理想，我们将看到唯一因子分解性质能够以一种更深刻、更普适的形式得以恢复。本文将带领读者深入探索整数环中理想的结构与算术，全面揭示其在现代数论中的基础性地位。

在接下来的内容中，我们将分三个章节展开探讨。在“原理与机制”一章中，我们将从[代数整数](@entry_id:151672)环的定义出发，引入理想的概念，并阐明理想如何恢复唯一因子分[解的唯一性](@entry_id:143619)。我们还将深入分析[素理想](@entry_id:154026)的分解行为和计算分解的关键工具。随后，在“应用与交叉学科联系”一章，我们将通过具体的数论问题（如[费马大定理](@entry_id:204421)的研究背景）和实例，展示[理想理论](@entry_id:184127)的实际应用，并探讨其与伽罗瓦理论、[复分析](@entry_id:167282)等领域的深刻联系。最后，通过“动手实践”部分的练习，您将有机会亲手计算整数环、判断理想是否为[主理想](@entry_id:152760)，并初步接触理想类群，从而将理论知识转化为解决问题的能力。

## 原理与机制

在代数数论中，整数环及其理想的结构是核心研究对象。继引言之后，本章将深入探讨[代数整数](@entry_id:151672)环的基本原理和其理想算术的内部机制。我们将从定义[整数环](@entry_id:181003)这一基本舞台开始，进而引入理想的概念，并阐明理想如何恢复了在某些数域中失去的唯一因子分解性质。随后，我们将详细分析素理想的分解行为，并介绍用于计算这种分解的关键工具，如判别式和戴德金判别法。最后，我们将引出理想类群，这个深刻的[代数结构](@entry_id:137052)精确地衡量了[整数环](@entry_id:181003)在元素层面上偏离唯一因子分解的程度。

### [整数环](@entry_id:181003)：基本舞台

我们研究的起点是整数 $\mathbb{Z}$ 在[数域](@entry_id:155558) $K$（即 $\mathbb{Q}$ 的[有限扩张](@entry_id:152412)）中的推广。这个推广并非任意的，而是遵循一个深刻的代数原则。

一个[数域](@entry_id:155558) $K$ 中的元素 $\alpha$ 如果是某个首一整系数多项式 $f(x) \in \mathbb{Z}[x]$ 的根，即 $f(\alpha) = 0$，则称 $\alpha$ 为**[代数整数](@entry_id:151672)**（algebraic integer）。[数域](@entry_id:155558) $K$ 中所有[代数整数](@entry_id:151672)的集合，记为 $\mathcal{O}_K$，被称为 $K$ 的**[整数环](@entry_id:181003)**（ring of integers）[@problem_id:3085992]。例如，在 $\mathbb{Q}$ 中，唯一的[代数整数](@entry_id:151672)就是普通的整数 $\mathbb{Z}$。在高斯有理[数域](@entry_id:155558) $\mathbb{Q}(i)$ 中，整数环是[高斯整数环](@entry_id:149594) $\mathbb{Z}[i] = \{a+bi \mid a, b \in \mathbb{Z}\}$。

一个自然而重要的问题是：为什么 $\mathcal{O}_K$ 会构成一个环？证明这一点并非易事。虽然证明两个[代数整数](@entry_id:151672)的相反数和乘积仍然是[代数整数](@entry_id:151672)是相对直接的，但证明它们的和也是[代数整数](@entry_id:151672)则需要更强大的工具。一个优雅的证明方法是利用**[有限生成模](@entry_id:148410)**（finitely generated module）的概念。一个关键定理指出：元素 $\alpha \in K$ 是[代数整数](@entry_id:151672)，当且仅当环 $\mathbb{Z}[\alpha]$ 是一个有限生成的 $\mathbb{Z}$-模。基于此，如果 $\alpha$ 和 $\beta$ 都是[代数整数](@entry_id:151672)，那么 $\mathbb{Z}[\alpha]$ 和 $\mathbb{Z}[\beta]$ 都是[有限生成](@entry_id:156447)的 $\mathbb{Z}$-模。由此可以推断，包含 $\alpha+\beta$ 和 $\alpha\beta$ 的环 $\mathbb{Z}[\alpha, \beta]$ 也是一个有限生成的 $\mathbb{Z}$-模。由于[有限生成模](@entry_id:148410)的任何子模也是[有限生成](@entry_id:156447)的，$\mathbb{Z}[\alpha+\beta]$ 和 $\mathbb{Z}[\alpha\beta]$ 都是[有限生成](@entry_id:156447)的 $\mathbb{Z}$-模，这反过来证明了 $\alpha+\beta$ 和 $\alpha\beta$ 都是[代数整数](@entry_id:151672)。因此，$\mathcal{O}_K$ 对加法和乘法封闭，构成一个环 [@problem_id:3085992]。

$\mathcal{O}_K$ 是 $K$ 中的**极大序**（maximal order），其中**序**（order）是指 $K$ 中的一个子环，同时它作为一个 $\mathbb{Z}$-模是自由且秩等于域的次数 $[K:\mathbb{Q}]$。对于任何一个使得 $K=\mathbb{Q}(\alpha)$ 的[代数整数](@entry_id:151672) $\alpha$，环 $\mathbb{Z}[\alpha]$ 都是 $K$ 中的一个序，并且满足 $\mathbb{Z}[\alpha] \subseteq \mathcal{O}_K$ [@problem_id:3086007]。

一个常见的误解是认为所有整数环都具有 $\mathbb{Z}[\alpha]$ 这种简单的形式。然而，事实并非如此。当 $\mathcal{O}_K = \mathbb{Z}[\alpha]$ 对某个 $\alpha \in \mathcal{O}_K$ 成立时，我们称 $\mathcal{O}_K$ 是**单演的**（monogenic）。例如，在二次域 $\mathbb{Q}(\sqrt{5})$ 中，由于 $5 \equiv 1 \pmod{4}$，其[整数环](@entry_id:181003)是 $\mathcal{O}_K = \mathbb{Z}\left[\frac{1+\sqrt{5}}{2}\right]$。元素 $\frac{1+\sqrt{5}}{2}$ 是多项式 $x^2-x-1=0$ 的根，因此是[代数整数](@entry_id:151672)。但是，它并不属于 $\mathbb{Z}[\sqrt{5}] = \{a+b\sqrt{5} \mid a,b \in \mathbb{Z}\}$。这意味着 $\mathbb{Z}[\sqrt{5}]$ 是 $\mathcal{O}_K$ 的一个真子环，$\mathcal{O}_K \neq \mathbb{Z}[\sqrt{5}]$ [@problem_id:3086007]。事实上，存在一些数域，其整数环根本不是单演的。

### 理想：恢复唯一因子分解

在初等数论中，算术基本定理保证了每个整数都能唯一地分解为素数的乘积。然而，在[代数整数](@entry_id:151672)环中，这种美好的性质时常会失去。一个经典的例子是环 $\mathbb{Z}[\sqrt{-5}]$，其中元素 $6$ 有两种截然不同的[因子分解](@entry_id:150389)：
$$ 6 = 2 \cdot 3 = (1+\sqrt{-5})(1-\sqrt{-5}) $$
可以验证，这里的 $2, 3, 1+\sqrt{-5}, 1-\sqrt{-5}$ 都是不可约元素，但它们彼此不相伴。这意味着 $\mathbb{Z}[\sqrt{-5}]$ 不是一个唯一因子分解[整环](@entry_id:155321)（UFD）。

为了挽救这一局面，19世纪的数学家引入了**理想**（ideal）的概念。一个**理想** $\mathfrak{a}$ 是环 $\mathcal{O}_K$ 的一个加法[子群](@entry_id:146164)，并且对于环中任意元素 $r \in \mathcal{O}_K$ 和理想中任意元素 $x \in \mathfrak{a}$，乘积 $rx$ 仍在 $\mathfrak{a}$ 中。由单个元素 $\alpha \in \mathcal{O}_K$ 生成的理想，记为 $(\alpha) = \alpha\mathcal{O}_K = \{ \alpha x \mid x \in \mathcal{O}_K \}$，称为**主理想**（principal ideal）。

需要注意的是，不同的元素可能生成相同的[主理想](@entry_id:152760)。两个元素 $\alpha, \beta \in \mathcal{O}_K$ 生成相同的[主理想](@entry_id:152760)，即 $(\alpha)=(\beta)$，当且仅当它们是**相伴的**（associates），也就是说，存在一个单位 $u \in \mathcal{O}_K^\times$（$\mathcal{O}_K$ 中乘法可逆的元素），使得 $\beta = u\alpha$ [@problem_id:3086011]。

整数环 $\mathcal{O}_K$ 是一类被称为**戴德金整环**（Dedekind domain）的特殊环。戴德金[整环](@entry_id:155321)最重要的性质之一，就是其理想层面的唯一[因子分解定理](@entry_id:749213)：在戴德金[整环](@entry_id:155321)中，任何非零真理想都可以唯一地（不计顺序）分解为**[素理想](@entry_id:154026)**（prime ideals）的乘积。素理想是满足特定条件的理想，即如果[素理想](@entry_id:154026) $\mathfrak{p}$ 包含了两个理想的乘积 $\mathfrak{a}\mathfrak{b}$，则它必定包含 $\mathfrak{a}$ 或 $\mathfrak{b}$。在上面的例子中，虽然元素 $6$ 的分解不唯一，但理想 $(6)$ 在 $\mathbb{Z}[\sqrt{-5}]$ 中的分解是唯一的：
$$ (6) = (2, 1+\sqrt{-5})^2 (3, 1+\sqrt{-5})(3, 1-\sqrt{-5}) $$
这里 $(2, 1+\sqrt{-5})$ 等是素理想。通过转向研究理想的分解，数学家们恢复了唯一因子分解这一关键的算术性质。

### 理想的算术

理想的唯一因子分解性质使我们能够为它们定义一套完整的算术体系，类似于整数的算术。对于 $\mathcal{O}_K$ 中的任意两个非零理想 $\mathfrak{a}$ 和 $\mathfrak{b}$，我们可以定义它们的最大公约数（GCD）和最小公倍数（LCM）。

假设 $\mathfrak{a}$ 和 $\mathfrak{b}$ 的[素理想分解](@entry_id:197179)覆盖了素理想集合 $\{\mathfrak{p}_1, \dots, \mathfrak{p}_k\}$，我们可以写出：
$$ \mathfrak{a} = \prod_{i=1}^{k} \mathfrak{p}_i^{a_i}, \quad \mathfrak{b} = \prod_{i=1}^{k} \mathfrak{p}_i^{b_i} $$
其中指数 $a_i, b_i \ge 0$。

- **[最大公约数 (GCD)](@entry_id:149942)**：两个理想的 GCD 是包含它们的最小理想。在[集合论](@entry_id:137783)意义上，这是它们的和：$\mathrm{GCD}(\mathfrak{a}, \mathfrak{b}) = \mathfrak{a}+\mathfrak{b}$。在因子分解层面，这对应于逐个取每个素理想的最小指数：
$$ \mathrm{GCD}(\mathfrak{a}, \mathfrak{b}) = \prod_{i=1}^{k} \mathfrak{p}_i^{\min(a_i, b_i)} $$

- **最小公倍数 (LCM)**：两个理想的 LCM 是被它们整除的最大理想。在[集合论](@entry_id:137783)意义上，这是它们的交集：$\mathrm{LCM}(\mathfrak{a}, \mathfrak{b}) = \mathfrak{a} \cap \mathfrak{b}$。在因子分解层面，这对应于逐个取每个素理想的最大指数：
$$ \mathrm{LCM}(\mathfrak{a}, \mathfrak{b}) = \prod_{i=1}^{k} \mathfrak{p}_i^{\max(a_i, b_i)} $$

让我们以[高斯整数环](@entry_id:149594) $\mathbb{Z}[i]$ 中的理想 $(6)$ 和 $(10)$ 为例来说明。首先，我们需要将这些[理想分解](@entry_id:148948)为素理想。这需要我们先分解有理素数 $2, 3, 5$ 在 $\mathbb{Z}[i]$ 中的行为：
- $2$ 歧化: $(2) = (1+i)^2$。
- $3$ 保持素性: $(3)$ 是[素理想](@entry_id:154026)。
- $5$ 分裂: $(5) = (2+i)(2-i)$。

因此，理想 $(6)$ 和 $(10)$ 的分解为：
$$ (6) = (2)(3) = (1+i)^2(3) $$
$$ (10) = (2)(5) = (1+i)^2(2+i)(2-i) $$

现在我们可以计算它们的 GCD 和 LCM：
$$ \mathrm{GCD}((6), (10)) = (1+i)^{\min(2,2)}(3)^{\min(1,0)}(2+i)^{\min(0,1)}(2-i)^{\min(0,1)} = (1+i)^2 = (2) $$
$$ \mathrm{LCM}((6), (10)) = (1+i)^{\max(2,2)}(3)^{\max(1,0)}(2+i)^{\max(0,1)}(2-i)^{\max(0,1)} = (1+i)^2(3)(2+i)(2-i) = (2)(3)(5) = (30) $$
这个例子清晰地展示了理想算术如何平行于整数算术 [@problem_id:3086000]。

### 素数的分解：[素理想](@entry_id:154026)在扩张中的行为

代数数论的一个中心问题是：一个有理素数 $p$ 生成的主理想 $(p) \subset \mathbb{Z}$，在被“提升”到数域 $K$ 的整数环 $\mathcal{O}_K$ 中后，其生成的理想 $p\mathcal{O}_K$ 如何分解为[素理想](@entry_id:154026)的乘积？

理想 $p\mathcal{O}_K$ 在 $\mathcal{O}_K$ 中不一定保持素性。原因是商环 $\mathcal{O}_K/p\mathcal{O}_K$ 不一定是一个[整环](@entry_id:155321) [@problem_id:3086004]。根据[环论](@entry_id:143825)，理想 $\mathfrak{a}$ 是[素理想](@entry_id:154026)当且仅当[商环](@entry_id:148632) $R/\mathfrak{a}$ 是整环。$p\mathcal{O}_K$ 的[素理想分解](@entry_id:197179)形式为：
$$ p\mathcal{O}_K = \mathfrak{P}_1^{e_1} \mathfrak{P}_2^{e_2} \cdots \mathfrak{P}_g^{e_g} $$
这里的 $\mathfrak{P}_i$ 是 $\mathcal{O}_K$ 中所有包含 $p$ 的[素理想](@entry_id:154026)，我们称它们**位于 $p$ 之上**（lie over $p$）。这些素理想 $\mathfrak{P}_i$ 与商环 $\mathcal{O}_K/p\mathcal{O}_K$ 的素理想之间存在一一对应关系 [@problem_id:3086015]。

描述这种分解行为有三个关键[不变量](@entry_id:148850) [@problem_id:3085993]：
- **分解数 (decomposition number) $g$**：$p\mathcal{O}_K$ 分解后得到的不同素理想的个数。
- **歧化指数 (ramification index) $e_i$**：每个素理想 $\mathfrak{P}_i$ 在分解式中出现的次数（幂次）。如果对某个 $i$ 有 $e_i > 1$，我们称素数 $p$ 在 $K$ 中**歧化**（ramifies）。
- **[惯性次数](@entry_id:195604) (inertia degree) $f_i$**：每个[素理想](@entry_id:154026) $\mathfrak{P}_i$ 对应的**剩余[域扩张](@entry_id:153187)**的次数 $f_i = [\mathcal{O}_K/\mathfrak{P}_i : \mathbb{Z}/p\mathbb{Z}]$。$\mathcal{O}_K/\mathfrak{P}_i$ 是一个特征为 $p$ 的[有限域](@entry_id:142106)，因此是 $\mathbb{F}_p = \mathbb{Z}/p\mathbb{Z}$ 的一个扩张。

这些[不变量](@entry_id:148850)并非独立的，它们受到一个深刻的恒[等式约束](@entry_id:175290)，该恒等式将它们与数域的次数 $n = [K:\mathbb{Q}]$ 联系起来：
$$ \sum_{i=1}^{g} e_i f_i = n $$
这个公式告诉我们，一个有理素数在数域中的“总度数”被守恒地分配给了它上面的所有素理想的歧化[指数和](@entry_id:199860)[惯性次数](@entry_id:195604)。

根据 $e, f, g$ 的值，我们有几种典型的分解行为：
- **完全分裂 (completely splits)**：如果 $g=n$（此时必然有 $e_i=f_i=1$），$p\mathcal{O}_K$ 分解为 $n$ 个不同的素理想。例如，在 $\mathbb{Q}(\sqrt{13})$ 中，3 完全分裂，因为 $x^2-x-3 \equiv x(x-1) \pmod{3}$，所以 $(3) = (3, \frac{1+\sqrt{13}}{2})(3, \frac{1+\sqrt{13}}{2}-1)$ [@problem_id:3086004]。
- **保持素性/惯性 (remains inert)**：如果 $g=1, e_1=1$（此时 $f_1=n$），$p\mathcal{O}_K$ 自身就是一个[素理想](@entry_id:154026)。
- **歧化 (ramifies)**：如果至少有一个 $e_i > 1$。

### 分解的机制：判别式与戴德金判别法

理论上，我们可以通过分解 $p\mathcal{O}_K$ 来研究素数的行为，但实际操作中如何计算 $e_i, f_i, g$ 呢？这需要更具体的工具。

首先，我们需要区分整数环 $\mathcal{O}_K$ 和它的子环（序）$\mathbb{Z}[\alpha]$。这种区分至关重要，因为许多计算工具首先是在更简单的环 $\mathbb{Z}[\alpha]$ 上建立的。**[判别式](@entry_id:174614)**（discriminant）是衡量这种差异的关键。对于数域 $K$，其**[域判别式](@entry_id:198568)** $D_K$ 是一个[不变量](@entry_id:148850)。而对于由[代数整数](@entry_id:151672) $\alpha$ 生成的序 $\mathbb{Z}[\alpha]$，我们也可以计算其[判别式](@entry_id:174614) $\mathrm{Disc}(\mathbb{Z}[\alpha])$。它们通过以下公式联系 [@problem_id:3085999] [@problem_id:3086007]：
$$ \mathrm{Disc}(\mathbb{Z}[\alpha]) = [\mathcal{O}_K : \mathbb{Z}[\alpha]]^2 D_K $$
其中 $[\mathcal{O}_K : \mathbb{Z}[\alpha]]$ 是加法群的**指数**（index），衡量了 $\mathbb{Z}[\alpha]$ 相对于 $\mathcal{O}_K$ 的“稀疏”程度。这个公式的一个重要推论是，任何整除指数的素数 $p$ 也必定整除 $\mathrm{Disc}(\mathbb{Z}[\alpha])$。

一个素数 $p$ 在 $\mathcal{O}_K$ 中歧化的一个充要条件是 $p$ 整除[域判别式](@entry_id:198568) $D_K$。

计算素数分解最强大的工具之一是**戴德金判别法**（Dedekin[d'](@entry_id:189153)s Criterion）。假设 $K=\mathbb{Q}(\alpha)$，其中 $\alpha$ 是一个[代数整数](@entry_id:151672)，其在 $\mathbb{Z}$ 上的极小多项式为 $f(x)$。戴德金判别法指出：如果一个素数 $p$ **不整除**指数 $[\mathcal{O}_K:\mathbb{Z}[\alpha]]$，那么 $p\mathcal{O}_K$ 的分解方式与多项式 $f(x)$ 在有限域 $\mathbb{F}_p$ 上的分解方式完全一致。即，若 $f(x) \pmod p$ 在 $\mathbb{F}_p[x]$ 中分解为
$$ \bar{f}(x) = \bar{F}_1(x)^{e_1} \bar{F}_2(x)^{e_2} \cdots \bar{F}_g(x)^{e_g} $$
其中 $\bar{F}_i(x)$ 是 $\mathbb{F}_p[x]$ 中互不相同的首一不[可约多项式](@entry_id:148759)，那么 $p\mathcal{O}_K$ 在 $\mathcal{O}_K$ 中的[素理想分解](@entry_id:197179)为
$$ p\mathcal{O}_K = \mathfrak{P}_1^{e_1} \mathfrak{P}_2^{e_2} \cdots \mathfrak{P}_g^{e_g} $$
其中 $\mathfrak{P}_i = (p, F_i(\alpha))$，且 $\mathfrak{P}_i$ 的[惯性次数](@entry_id:195604) $f_i$ 等于多项式 $\bar{F}_i(x)$ 的次数。

当素数 $p$ 整除指数 $[\mathcal{O}_K:\mathbb{Z}[\alpha]]$ 时，戴德金判别法失效。在这种情况下，$\bar{f}(x)$ 的分解模式可能给出错误的分解信息。例如，在 $K=\mathbb{Q}(\sqrt{13})$ 中，取 $\alpha=\sqrt{13}$，则 $f(x)=x^2-13$。我们已经知道 $[\mathcal{O}_K:\mathbb{Z}[\sqrt{13}]]=2$。对于素数 $p=2$，它整除指数，判别法失效。如果我们天真地应用它，$\bar{f}(x) = x^2-13 \equiv x^2-1 = (x+1)^2 \pmod 2$。这似乎预示着 $2$ 在 $\mathcal{O}_K$ 中歧化。然而，真实情况是 $2$ 在 $\mathcal{O}_K$ 中保持素性。这种由指数引起的“虚假”歧化被称为“序的歧化”（essential discriminant divisor）[@problem_id:3015827]。正确的做法是换一个生成元，使得新指数不被 $p$ 整除。对于 $K=\mathbb{Q}(\sqrt{13})$，我们应该使用 $\beta = \frac{1+\sqrt{13}}{2}$，此时 $\mathcal{O}_K = \mathbb{Z}[\beta]$，指数为 1。其极小多项式为 $g(x)=x^2-x-3$。$\bar{g}(x)=x^2+x+1 \pmod 2$ 在 $\mathbb{F}_2[x]$ 中不可约，正确地预示了 $(2)$ 在 $\mathcal{O}_K$ 中保持素性 [@problem_id:3015827]。

### 理想类群：衡量唯一[因子分解](@entry_id:150389)的失败

我们现在回到最初的问题：元素层面的唯一[因子分解](@entry_id:150389)。尽管理想恢复了唯一分解，但一个理想是否为**主理想**成为了一个新的关键问题。

为了系统地研究这个问题，我们引入**分式理想**（fractional ideal）的概念。一个非零分式理想是 $K$ 的一个非零 $\mathcal{O}_K$-子模 $\mathfrak{a}$，满足存在某个非零的 $c \in \mathcal{O}_K$ 使得 $c\mathfrak{a} \subseteq \mathcal{O}_K$。所有非零分式理想在理想乘法下构成一个阿贝尔群，记为 $\mathcal{I}_K$。其中，单位元是 $\mathcal{O}_K$ 本身。

在这个群中，所有由单个元素 $\alpha \in K^\times$ 生成的**主分式理想** $\alpha\mathcal{O}_K$ 构成一个[子群](@entry_id:146164)，记为 $\mathcal{P}_K$ [@problem_id:308589]。

**理想类群**（ideal class group）$\mathrm{Cl}(K)$ 被定义为[商群](@entry_id:145113)：
$$ \mathrm{Cl}(K) = \mathcal{I}_K / \mathcal{P}_K $$
[理想类群](@entry_id:153974)的元素是理想的[等价类](@entry_id:156032)，其中两个理想 $\mathfrak{a}, \mathfrak{b}$ 等价，当且仅当存在一个 $\gamma \in K^\times$ 使得 $\mathfrak{a} = \gamma\mathfrak{b}$。[理想类群](@entry_id:153974)的单位元是[主理想](@entry_id:152760)构成的类。因此，一个理想是主理想，当且仅当它所在的类是单位元。

理想类群的结构精确地衡量了 $\mathcal{O}_K$ 偏离[主理想整环](@entry_id:152359)（[PID](@entry_id:174286)）的程度，进而衡量其偏离唯一因子分解[整环](@entry_id:155321)（UFD）的程度。一个深刻的定理表明，对于戴德金整环（如 $\mathcal{O}_K$），以下三个陈述是等价的 [@problem_id:3015842]：
1. $\mathcal{O}_K$ 是一个[主理想整环](@entry_id:152359)（PID）。
2. $\mathcal{O}_K$ 是一个唯一因子分解[整环](@entry_id:155321)（UFD）。
3. [理想类群](@entry_id:153974) $\mathrm{Cl}(K)$ 是[平凡群](@entry_id:151996)（即只包含单位元）。

换言之，当且仅当所有理想都是[主理想](@entry_id:152760)时，$\mathcal{O}_K$ 才具有元素层面的唯一因子分解。[理想类群](@entry_id:153974)的阶，被称为**[类数](@entry_id:156164)**（class number）$h_K$，如果 $h_K > 1$，则表明存在[非主理想](@entry_id:201831)，从而破坏了唯一[因子分解](@entry_id:150389)。例如，对于 $\mathbb{Q}(\sqrt{-5})$，其类数为 $2$，这解释了我们之前看到的 $6$ 的两种不同分解。一个基本但深刻的结果是，任何数域的类数都是有限的。

需要强调的是，[理想类群](@entry_id:153974)衡量的是**元素**唯一[因子分解](@entry_id:150389)的失败，而不是**理想**唯一[因子分解](@entry_id:150389)的失败。后者对于任何数域的[整数环](@entry_id:181003) $\mathcal{O}_K$ 都是成立的 [@problem_id:3015842]。理想类群的美妙之处在于，它将一个关于算术分解的问题，转化为了一个关于[有限阿贝尔群](@entry_id:136632)结构代数问题。