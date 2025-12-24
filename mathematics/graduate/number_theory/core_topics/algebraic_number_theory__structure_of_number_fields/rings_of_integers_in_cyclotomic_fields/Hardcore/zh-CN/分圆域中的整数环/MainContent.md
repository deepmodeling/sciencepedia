## 引言
分圆域及其[整数环](@entry_id:181003)是[代数数论](@entry_id:148067)研究中一类至关重要的对象。它们既足够具体，允许进行显式计算，又具有丰富的[代数结构](@entry_id:137052)，集中展现了数域算术的诸多核心现象。尽管有理数域 $\mathbb{Q}$ 中的算术法则早已为人熟知，但当我们将视线投向[分圆域](@entry_id:153828)这类更广阔的代数世界时，一系列基本问题便浮出水面：这个新世界里的“整数”是什么？我们熟悉的素数在其中如何分解？其乘法可[逆元](@entry_id:140790)素又具有怎样的结构？

本文旨在系统地回答这些问题，为读者构建一幅关于分圆域整数环的清晰图景。在接下来的内容中，我们将分三步展开：第一章“原理与机制”将奠定理论基石，从分圆域的定义出发，详细阐述其整数环的确定、判别式的计算以及素理想的分解规律。第二章“应用与跨学科联系”将展示这些理论的强大威力，探索其在解决费马大定理等经典数论难题中的关键作用，并揭示其与[类域论](@entry_id:155687)乃至现代[量子计算](@entry_id:142712)等领域的深刻联系。最后，第三章“动手实践”将通过具体的计算和编程练习，帮助读者将抽象的理论转化为可操作的技能。

通过本次学习，您不仅将掌握分圆域算术的核心工具，更将领略到纯粹数学理论如何跨越时空，在不同领域中绽放其独特的魅力。让我们首先进入“原理与机制”部分，深入探索分圆域[整数环](@entry_id:181003)的[代数结构](@entry_id:137052)。

## 原理与机制

在介绍性章节之后，我们现在深入探讨分圆域的整数环的[代数结构](@entry_id:137052)。本章的目标是系统地阐述其核心原理与机制，包括其[整数环](@entry_id:181003)的确定、[判别式](@entry_id:174614)的计算，以及[素理想](@entry_id:154026)在其[整数环](@entry_id:181003)中的分解规律。我们将从基本定义出发，逐步建立起描述这些丰富结构的理论框架。

### [分圆域](@entry_id:153828)及其次数

我们研究的中心对象是**分圆域 (cyclotomic field)**。对于给定的正整数 $n$，一个**$n$次[本原单位根](@entry_id:153052) (primitive $n$-th root of unity)** $\zeta_n$ 是一个复数，其[乘法阶](@entry_id:636522)恰好为 $n$。这意味着 $\zeta_n^n=1$，但对于任何满足 $1 \le k  n$ 的整数 $k$，都有 $\zeta_n^k \ne 1$。将 $\zeta_n$ 添加到有理数域 $\mathbb{Q}$ 中，我们便得到了 $n$ 次分圆域，记为 $K_n = \mathbb{Q}(\zeta_n)$。

任何域扩张的度都是一个基本的量。对于[分圆域](@entry_id:153828) $K_n/\mathbb{Q}$，其次数由 $\zeta_n$ 在 $\mathbb{Q}$ 上的极小多项式 $m_{\zeta_n, \mathbb{Q}}(x)$ 的次数决定。由于 $\zeta_n$ 是多项式 $x^n-1$ 的根，所以 $m_{\zeta_n, \mathbb{Q}}(x)$ 必然是 $x^n-1$ 的一个因式。

一个关键的洞察在于确定 $\zeta_n$ 的所有代数共轭。一个域嵌入 $\sigma: K_n \hookrightarrow \mathbb{C}$ 保持 $\mathbb{Q}$ 不变，因此它将 $\zeta_n$ 映到其极小多项式的另一个根。由于 $\sigma$ 是一个同构，它保持元素的[乘法阶](@entry_id:636522)。因此，$\sigma(\zeta_n)$ 的阶也必须是 $n$，这意味着 $\sigma(\zeta_n)$ 也必须是一个 $n$ 次[本原单位根](@entry_id:153052)。所有 $n$ 次[本原单位根](@entry_id:153052)的集合可以表示为 $\{\zeta_n^a \mid 1 \le a \le n, \gcd(a,n)=1\}$，其中 $\gcd(a,n)$ 表示 $a$ 和 $n$ 的[最大公约数](@entry_id:142947)。这个集合中恰好有 $\varphi(n)$ 个元素，其中 $\varphi$ 是**[欧拉函数](@entry_id:634684) (Euler's totient function)**。

代数数论中一个不平凡的基础性定理指出，所有这些 $n$ 次[本原单位根](@entry_id:153052)确实都是 $\zeta_n$ 在 $\mathbb{Q}$ 上的代数共轭。这意味着，对于任何满足 $\gcd(a,n)=1$ 的整数 $a$，都存在一个域嵌入 $\sigma_a$ 使得 $\sigma_a(\zeta_n) = \zeta_n^a$。因此，$\zeta_n$ 的极小多项式恰好是以所有这些 $\varphi(n)$ 个[本原单位根](@entry_id:153052)为根的[首一多项式](@entry_id:152311)。这个多项式被称为 **$n$ 次[分圆多项式](@entry_id:155668) ($n$-th cyclotomic polynomial)**，记为 $\Phi_n(x)$：
$$
\Phi_n(x) = \prod_{\substack{1 \le a \le n \\ \gcd(a,n)=1}} (x - \zeta_n^a)
$$
这个多项式在 $\mathbb{Q}$ 上是不可约的。因此，[分圆域](@entry_id:153828)的次数为：
$$
[K_n : \mathbb{Q}] = \deg(\Phi_n(x)) = \varphi(n)
$$
这一结论是分圆域理论的基石。

### 分圆域的整数环

要研究分圆域中的算术，我们必须首先确定其**[整数环](@entry_id:181003) (ring of integers)**。一个**[代数整数](@entry_id:151672) (algebraic integer)** 是指某个整系数[首一多项式](@entry_id:152311)的[复根](@entry_id:172941)。对于一个[数域](@entry_id:155558) $K$（即 $\mathbb{Q}$ 的[有限扩张](@entry_id:152412)），其[整数环](@entry_id:181003) $\mathcal{O}_K$ 定义为 $K$ 中所有[代数整数](@entry_id:151672)构成的集合。这个集合是一个环，也是 $\mathbb{Z}$ 在 $K$ 中的**[整闭](@entry_id:149392)包 (integral closure)**。

在[分圆域](@entry_id:153828) $K_n = \mathbb{Q}(\zeta_n)$ 中，$\zeta_n$ 本身是一个[代数整数](@entry_id:151672)，因为它是整系数[首一多项式](@entry_id:152311) $x^n-1=0$ 的根。由于 $\mathcal{O}_{K_n}$ 是一个环，它必然包含所有由 $\mathbb{Z}$ 和 $\zeta_n$ 生成的元素，即由 $\zeta_n$ 的整系数多项式构成的环 $\mathbb{Z}[\zeta_n]$。因此，我们总是有 $\mathbb{Z}[\zeta_n] \subseteq \mathcal{O}_{K_n}$。

一个深刻且至关重要的定理指出，这个包含关系实际上是一个等式。对于任何正整数 $n$，[分圆域](@entry_id:153828) $K_n = \mathbb{Q}(\zeta_n)$ 的[整数环](@entry_id:181003)恰好就是 $\mathbb{Z}[\zeta_n]$：
$$
\mathcal{O}_{K_n} = \mathbb{Z}[\zeta_n]
$$
这个结论是[分圆域](@entry_id:153828)理论的支柱之一。它表明集合 $\{1, \zeta_n, \zeta_n^2, \dots, \zeta_n^{\varphi(n)-1}\}$ 不仅是 $K_n$ 的一组 $\mathbb{Q}$-基，而且是 $\mathcal{O}_{K_n}$ 的一组**[整基](@entry_id:190217) (integral basis)**。一个[数域](@entry_id:155558)如果其[整数环](@entry_id:181003)可以由某个元素 $\alpha$ 的幂次生成（即 $\mathcal{O}_K = \mathbb{Z}[\alpha]$），则称该域是**单衍的 (monogenic)**。因此，所有分圆域都是单衍的。值得注意的是，并非所有数域都具有此性质。

### 迹、范数与[判别式](@entry_id:174614)

为了深入研究整数[环的结构](@entry_id:150907)，我们需要引入三个基本工具：迹、范数和判别式。对于一个次数为 $d$ 的[数域](@entry_id:155558) $K/\mathbb{Q}$ 和任意元素 $\alpha \in K$，其**迹 (trace)** $\mathrm{Tr}_{K/\mathbb{Q}}(\alpha)$ 和**范数 (norm)** $\mathrm{N}_{K/\mathbb{Q}}(\alpha)$ 分别定义为其所有 $d$ 个 $\mathbb{Q}$-嵌入 $\sigma_i: K \hookrightarrow \mathbb{C}$ 的像的总和与总乘积：
$$
\mathrm{Tr}_{K/\mathbb{Q}}(\alpha) = \sum_{i=1}^d \sigma_i(\alpha) \quad \text{and} \quad \mathrm{N}_{K/\mathbb{Q}}(\alpha) = \prod_{i=1}^d \sigma_i(\alpha)
$$
这些映射的一个基本性质是，如果 $\alpha$ 是一个[代数整数](@entry_id:151672)（即 $\alpha \in \mathcal{O}_K$），那么它的[迹和范数](@entry_id:155207)都是有理整数，即 $\mathrm{Tr}_{K/\mathbb{Q}}(\alpha) \in \mathbb{Z}$ 且 $\mathrm{N}_{K/\mathbb{Q}}(\alpha) \in \mathbb{Z}$。

**判别式 (discriminant)** $\mathrm{Disc}(K)$ 是衡量整数环“大小”或“密度”的一个[不变量](@entry_id:148850)。对于 $\mathcal{O}_K$ 的任意一组[整基](@entry_id:190217) $\{b_1, \dots, b_d\}$，判别式定义为如下[矩阵的行列式](@entry_id:148198)：
$$
\mathrm{Disc}(K) = \det\left( (\mathrm{Tr}_{K/\mathbb{Q}}(b_i b_j))_{1 \le i,j \le d} \right)
$$
一个关键事实是，[判别式](@entry_id:174614)的值不依赖于[整基](@entry_id:190217)的选择。这是因为任何两组[整基](@entry_id:190217)之间的转换矩阵 $B$ 的[行列式](@entry_id:142978)都为 $\pm 1$（即 $B \in GL_d(\mathbb{Z})$），而判别式在新基下的变换规律为乘以 $(\det B)^2=1$。

对于单衍域 $K = \mathbb{Q}(\alpha)$ 且 $\mathcal{O}_K = \mathbb{Z}[\alpha]$，[域判别式](@entry_id:198568)恰好等于 $\alpha$ 的极小[多项式的判别式](@entry_id:148721)。由于[分圆域](@entry_id:153828) $K_n = \mathbb{Q}(\zeta_n)$ 是单衍的，其判别式就是[分圆多项式](@entry_id:155668) $\Phi_n(x)$ 的判别式。这个联系是计算分圆[域[判别](@entry_id:198568)式](@entry_id:174614)和研究其算术性质的出发点。

### [整数环](@entry_id:181003)中的算术：[素理想分解](@entry_id:197179)

[代数数论](@entry_id:148067)的核心问题之一是理解有理素数 $p$ 在数域[整数环](@entry_id:181003) $\mathcal{O}_K$ 中如何分解为[素理想](@entry_id:154026)的乘积。[判别式](@entry_id:174614)为此提供了关键信息：一个素数 $p$ 在 $K$ 中**[分歧](@entry_id:193119) (ramifies)**（即 $(p)\mathcal{O}_K$ 的某个素[理想因子](@entry_id:137944)的指数大于 1）当且仅当 $p$ 整除[域判别式](@entry_id:198568) $\mathrm{Disc}(K)$。

对于分圆域 $\mathbb{Q}(\zeta_n)$，一个基本定理指出，整除其[判别式](@entry_id:174614)的素数恰好是那些整除 $n$ 的素数。因此，我们得到了一个清晰的划分：
- 如果 $p \nmid n$，素数 $p$ 在 $\mathbb{Q}(\zeta_n)$ 中是**未分歧的 (unramified)**。
- 如果 $p \mid n$，素数 $p$ 在 $\mathbb{Q}(\zeta_n)$ 中是**分歧的 (ramified)**。

#### 未分歧情形：$p \nmid n$

当素数 $p$ 与 $n$ [互素](@entry_id:143119)时，其分解行为由**戴德金定理 (Dedekin[d'](@entry_id:189153)s Theorem)** 完美描述。由于 $\mathcal{O}_{K_n} = \mathbb{Z}[\zeta_n]$，理想 $(p)$ 在 $\mathcal{O}_{K_n}$ 中的分解方式与[分圆多项式](@entry_id:155668) $\Phi_n(x)$ 在有限域 $\mathbb{F}_p$ 上分解为不[可约多项式](@entry_id:148759)的方式完全一致。

对于此种情形，一个优美的定理成立：当 $p \nmid n$ 时，$\Phi_n(x)$ 在 $\mathbb{F}_p[x]$ 上的所有不可约因子的次数都相同。这个公共次数记为 $f$，它等于 $p$ 在乘法群 $(\mathbb{Z}/n\mathbb{Z})^\times$ 中的阶。换言之，$f$ 是满足 $p^f \equiv 1 \pmod{n}$ 的最小正整数。

于是，理想 $(p)$ 在 $\mathcal{O}_{K_n}$ 中分解为 $r = \varphi(n)/f$ 个不同的素理想的乘积：
$$
(p) = \mathfrak{p}_1 \mathfrak{p}_2 \cdots \mathfrak{p}_r
$$
其中每个素理想 $\mathfrak{p}_i$ 的**惯性指数 (inertia degree)** $f(\mathfrak{p}_i|p)$ 都等于 $f$。这意味着每个剩[余域](@entry_id:139336) $\mathcal{O}_{K_n}/\mathfrak{p}_i$ 都是 $\mathbb{F}_p$ 的 $f$ 次扩张，即 $\mathcal{O}_{K_n}/\mathfrak{p}_i \cong \mathbb{F}_{p^f}$。

例如，考虑 $K = \mathbb{Q}(\zeta_{105})$ 和素数 $p=2$。这里 $n=105 = 3 \times 5 \times 7$，显然 $2 \nmid 105$。我们需要计算 $2$ 在 $(\mathbb{Z}/105\mathbb{Z})^\times$ 中的阶。根据中国剩余定理，这等价于计算 $2$ 分别在模 $3, 5, 7$ 下的阶，并取其最小公倍数。
- 模 3: $2^2 \equiv 1 \pmod 3$ (阶为 2)
- 模 5: $2^4 \equiv 1 \pmod 5$ (阶为 4)
- 模 7: $2^3 \equiv 1 \pmod 7$ (阶为 3)
因此，$f = \mathrm{lcm}(2, 4, 3) = 12$。这意味着在 $\mathbb{Q}(\zeta_{105})$ 中，理想 $(2)$ 分解为 $\varphi(105)/12 = 48/12 = 4$ 个不同的[素理想](@entry_id:154026)，每个素理想的惯性指数都是 $12$。

#### 分歧情形：$p \mid n$

当素数 $p$ 整除 $n$ 时，情况变得更加复杂，分歧现象出现。设 $n = p^k m$，其中 $k = v_p(n) \ge 1$ 且 $\gcd(p,m)=1$。$p$ 在 $K_n = \mathbb{Q}(\zeta_n)$ 中的分歧行为完全由子域 $\mathbb{Q}(\zeta_{p^k})$ 决定，因为另一个子域 $\mathbb{Q}(\zeta_m)$ 在 $p$ 处是未[分歧](@entry_id:193119)的。

在[子域](@entry_id:155812) $L = \mathbb{Q}(\zeta_{p^k})$ 中，素数 $p$ 是**[完全分歧的](@entry_id:189971) (totally ramified)**。这意味着在 $\mathcal{O}_L$ 中，$(p)$ 只分解为一个素理想的幂次，其**[分歧指数](@entry_id:186386) (ramification index)** 等于扩张次数 $[L:\mathbb{Q}] = \varphi(p^k)$。因此，对于 $K_n/\mathbb{Q}$ 中位于 $p$ 之上的任意素理想 $\mathfrak{P}$，其[分歧指数](@entry_id:186386)为：
$$
e(\mathfrak{P}|p) = \varphi(p^k) = p^k - p^{k-1} = p^{k-1}(p-1)
$$

这个公式使我们能够区分两种不同类型的分歧：
- **驯[分歧](@entry_id:193119) (Tame Ramification)**：当[分歧指数](@entry_id:186386) $e$ 不被 $p$ 整除时发生。根据公式 $e = p^{k-1}(p-1)$，$e$ 不被 $p$ 整除当且仅当 $k-1=0$，即 $k=1$。因此，如果 $p$ 仅一次整除 $n$ ($v_p(n)=1$)，则[分歧](@entry_id:193119)是驯的。
- **[野分歧](@entry_id:149250) (Wild Ramification)**：当[分歧指数](@entry_id:186386) $e$ 被 $p$ 整除时发生。这发生在 $k-1 \ge 1$，即 $k \ge 2$ 的情况下。因此，如果 $p^2$ 整除 $n$ ($v_p(n) \ge 2$)，则分歧是野的。

### [整数环](@entry_id:181003)中的单位

整数环的最后一个重要组成部分是其乘法可[逆元](@entry_id:140790)素的集合，即**单位群 (group of units)** $\mathcal{O}_K^\times$。根据[狄利克雷单位定理](@entry_id:155550)，这个群的结构是[有限生成](@entry_id:156447)的。在[分圆域](@entry_id:153828)中，有一类可以明确构造的单位，称为**[分圆单位](@entry_id:184331) (cyclotomic units)**。

对于任何与 $n$ [互素](@entry_id:143119)的整数 $a$，考虑元素
$$
u_a = \frac{1 - \zeta_n^a}{1 - \zeta_n}
$$
我们可以证明 $u_a$ 是 $\mathcal{O}_{K_n}$ 中的一个单位。首先，利用几何级数求和公式，我们有 $u_a = 1 + \zeta_n + \dots + \zeta_n^{a-1}$。这表明 $u_a$ 是 $\zeta_n$ 的一个整系数多项式，因此 $u_a \in \mathbb{Z}[\zeta_n] = \mathcal{O}_{K_n}$，即 $u_a$ 是一个[代数整数](@entry_id:151672)。

其次，我们计算其范数。$u_a$ 的代数共轭是 $\sigma_c(u_a) = \frac{1 - \zeta_n^{ac}}{1 - \zeta_n^c}$，其中 $\gcd(c,n)=1$。
$$
\mathrm{N}_{K_n/\mathbb{Q}}(u_a) = \prod_{\substack{1 \le c  n \\ \gcd(c,n)=1}} \frac{1 - \zeta_n^{ac}}{1 - \zeta_n^c}
$$
由于 $\gcd(a,n)=1$，映射 $c \mapsto ac$ 是群 $(\mathbb{Z}/n\mathbb{Z})^\times$ 的一个[置换](@entry_id:136432)。这意味着分子中的乘积项只是对分母中乘积项的重新[排列](@entry_id:136432)。由于乘法是可交换的，分子和分母相等，因此 $\mathrm{N}_{K_n/\mathbb{Q}}(u_a) = 1$。

一个范数为 $\pm 1$ 的[代数整数](@entry_id:151672)必为一个单位。因此，$u_a \in \mathcal{O}_{K_n}^\times$。这些由 $u_a$（对于不同的 $a$）生成的单位构成了[分圆单位](@entry_id:184331)群的一个重要[子群](@entry_id:146164)。一个深刻的结果（与[类数公式](@entry_id:202401)相关）表明，这个[分圆单位](@entry_id:184331)群在整个[单位群](@entry_id:184012) $\mathcal{O}_{K_n}^\times$ 中具有有限的指数，这揭示了分圆域算术结构的更深层次的联系。