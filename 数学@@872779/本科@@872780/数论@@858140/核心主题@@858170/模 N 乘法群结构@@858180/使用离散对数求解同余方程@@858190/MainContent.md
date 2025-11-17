## 引言
在数论的探索中，指数同余方程 $a^x \equiv b \pmod n$ 是一类具有挑战性但又至关重要的 问题。简单地逐一尝试指数值在模数很大时并不可行，这揭示了我们需要一个更系统、更强大的理论工具来“解开”指数的束缚。这个工具就是**[离散对数](@entry_id:266196)**——一个在有限群世界中扮演着与传统对数相似角色的强大概念，它能巧妙地将复杂的指[数乘](@entry_id:155971)法关系转化为简单的线性加法关系。

本文将带领读者深入探索[离散对数](@entry_id:266196)的世界，全面掌握其原理与应用。在“**原理与机制**”一章中，我们将严格定义[离散对数](@entry_id:266196)，探讨其存在的[代数结构](@entry_id:137052)基础（循环群与[原根](@entry_id:163633)），并阐明其如何将指数[同余](@entry_id:143700)方程转化为[线性同余](@entry_id:150485)方程的核心机制。接着，在“**应用与跨学科联系**”一章中，我们将视野扩展到更广阔的领域，展示[离散对数](@entry_id:266196)如何在高等数论、[现代密码学](@entry_id:274529)（如[Diffie-Hellman密钥交换](@entry_id:144570)）以及前沿的[量子计算](@entry_id:142712)中扮演关键角色。最后，通过“**动手实践**”部分，读者将有机会亲手应用如BSGS和Pohlig-Hellman等核心算法，将理论知识转化为解决实际问题的能力。通过这三个层层递进的章节，你将构建起一个关于[离散对数](@entry_id:266196)的完整而坚实的知识体系。

## 原理与机制

在上一章中，我们介绍了[同余](@entry_id:143700)方程的基本概念。本章将深入探讨一类特殊的指数同余方程，并引入一个强大的理论工具——**[离散对数](@entry_id:266196)**。正如传统对数将乘法运算转化为加法运算一样，[离散对数](@entry_id:266196)将有限群中的乘法关系转化为整数模加法关系，从而为解决复杂的指数同余问题提供了一条系统性的路径。我们将首先严格定义[离散对数](@entry_id:266196)，探讨其存在的条件，然后阐述其核心应用机制，并最终介绍几种计算[离散对数](@entry_id:266196)的关键算法。

### [离散对数](@entry_id:266196)的概念

我们从熟悉的实数对数开始类比。对于正实数 $g$ 和 $h$，对数 $\log_g(h)$ 是唯一的实数 $x$，使得 $g^x = h$。这个运算将乘法关系 $h_1 h_2 = h_3$ 转化为加法关系 $\log_g(h_1) + \log_g(h_2) = \log_g(h_3)$。我们的目标是在有限群的离散世界中建立类似的结构。

考虑一个阶为 $n$ 的有限**循环群** $G$，其生成元为 $g$。这意味着 $G$ 中的每一个元素 $h$ 都可以表示为 $g$ 的某个整数次幂。也就是说，对于任意 $h \in G$，都存在一个整数 $k$ 使得 $h = g^k$。然而，这个指数 $k$ 并不是唯一的。由于[群的阶](@entry_id:137115)为 $n$，生成元 $g$ 的阶也为 $n$，即 $g^n = e$（其中 $e$ 是群的单位元）。因此，如果 $h = g^k$，那么对于任意整数 $m$，我们都有 $g^{k+mn} = g^k \cdot (g^n)^m = h \cdot e^m = h$。这表明所有与 $k$ 模 $n$ [同余](@entry_id:143700)的整数都是合法的指数。

为了使“对数”成为一个定义良好的函数（即每个输入对应唯一的输出），我们不能简单地将其值域设为整数集 $\mathbb{Z}$。正确的做法是将其值域定义为模 $n$ 的整数[剩余类](@entry_id:185226)环 $\mathbb{Z}/n\mathbb{Z}$。

**定义 ([离散对数](@entry_id:266196))**：设 $G$ 是一个由 $g$ 生成的阶为 $n$ 的[有限循环群](@entry_id:147298)。对于任意元素 $h \in G$，其以 $g$ 为底的**[离散对数](@entry_id:266196)**（或称为**指数**）被定义为一个映射 $\log_g: G \to \mathbb{Z}/n\mathbb{Z}$。该映射将 $h$ 映到唯一的[剩余类](@entry_id:185226) $[k] \in \mathbb{Z}/n\mathbb{Z}$，使得 $g^k = h$。通常，我们会选择该[剩余类](@entry_id:185226)中的最小非负代表，即满足 $g^k = h$ 的那个唯一的 $k \in \{0, 1, \dots, n-1\}$。[@problem_id:3089881]

这个定义是稳健的。**存在性**由 $G$ 是循环群且由 $g$ 生成保证。**唯一性**则源于：若 $g^k = g^{k'}$，则 $g^{k-k'} = e$。因为 $g$ 的阶是 $n$，这必然意味着 $n$ 整除 $k-k'$，即 $k \equiv k' \pmod n$。因此，在 $\mathbb{Z}/n\mathbb{Z}$ 中，$[k]$ 和 $[k']$ 是同一个元素。

这个[离散对数](@entry_id:266196)映射 $\log_g$ 不仅仅是一个函数，它还是一个**[群同构](@entry_id:147371)**。它将[乘法群](@entry_id:155975) $(G, \cdot)$ 与加法群 $(\mathbb{Z}/n\mathbb{Z}, +)$ 联系起来。对于任意 $h_1, h_2 \in G$，我们有：
$$ \log_g(h_1 h_2) \equiv \log_g(h_1) + \log_g(h_2) \pmod n $$
这个性质是[离散对数](@entry_id:266196)威力的核心，因为它将 $G$ 中的乘法问题转化为了 $\mathbb{Z}/n\mathbb{Z}$ 中的加法问题，而后者通常是线性且更易于处理的。同样，指数关系也得以线性化 [@problem_id:3089897]：
$$ \log_g(h^k) \equiv k \cdot \log_g(h) \pmod n $$

### [离散对数](@entry_id:266196)的舞台：循环群

[离散对数](@entry_id:266196)工具的有效应用，其前提是底所在的[代数结构](@entry_id:137052)是一个循环群。在数论中，我们最常应用的场景是模 $n$ 的乘法群 $(\mathbb{Z}/n\mathbb{Z})^\times$。

**定义 (模 n 的单位群)**：对于正整数 $n$，模 $n$ 的**单位群** $(\mathbb{Z}/n\mathbb{Z})^\times$ 是由所有与 $n$ 互质的模 $n$ [剩余类](@entry_id:185226)组成的集合，其运算为模 $n$ 乘法。这个[群的阶](@entry_id:137115)由[欧拉函数](@entry_id:634684) $\varphi(n)$ 给出。

当 $(\mathbb{Z}/n\mathbb{Z})^\times$ 是一个循环群时，存在一个生成元 $g$，称为模 $n$ 的**[原根](@entry_id:163633)**。这意味着群中的每一个元素都可以表示为 $g$ 的幂。在这种情况下，我们可以为群中的所有元素定义一个统一的[离散对数](@entry_id:266196)“[坐标系](@entry_id:156346)”。

一个核心问题是：对于哪些整数 $n$，群 $(\mathbb{Z}/n\mathbb{Z})^\times$ 是循环群？数论中的一个基本定理给出了完整的答案。

**定理 (原根存在定理)**：模 $n$ 的[乘法群](@entry_id:155975) $(\mathbb{Z}/n\mathbb{Z})^\times$ 是[循环群](@entry_id:138668)，当且仅当 $n$ 的取值为 $1, 2, 4$，$p^k$ 或 $2p^k$，其中 $p$ 是一个奇素数，$k \ge 1$ 是一个整数。[@problem_id:3089859]

这个定理至关重要。它告诉我们，在模一个奇素数 $p$ 或其幂 $p^k$ 的情况下，我们总能找到一个[原根](@entry_id:163633)，从而可以对所有非零元素使用[离散对数](@entry_id:266196)。例如，对于任意奇素数 $p$，群 $(\mathbb{Z}/p\mathbb{Z})^\times$ 都是阶为 $p-1$ 的[循环群](@entry_id:138668)。

为什么循环性如此关键？设想我们要解一个一般形式的[同余](@entry_id:143700)方程 $a^x \equiv b \pmod m$，其中 $a, b \in (\mathbb{Z}/m\mathbb{Z})^\times$。
- **如果 $(\mathbb{Z}/m\mathbb{Z})^\times$ 是[循环群](@entry_id:138668)**，设其生成元为 $g$，阶为 $n = \varphi(m)$。我们可以计算出 $\log_g a$ 和 $\log_g b$。方程变形为 $(g^{\log_g a})^x \equiv g^{\log_g b} \pmod m$，这等价于指数上的一个**单一[线性同余](@entry_id:150485)方程**：
$$ x \cdot \log_g a \equiv \log_g b \pmod n $$
解这个[线性同余](@entry_id:150485)方程，就能得到 $x$ 的值。

- **如果 $(\mathbb{Z}/m\mathbb{Z})^\times$ 不是[循环群](@entry_id:138668)**，那么不存在一个单一的生成元。根据[有限阿贝尔群基本定理](@entry_id:145889)，该[群同构](@entry_id:147371)于若干个循环[群的直积](@entry_id:143585)，例如 $(\mathbb{Z}/m\mathbb{Z})^\times \cong C_{n_1} \times C_{n_2} \times \dots \times C_{n_k}$。此时，一个元素不再由单个指数描述，而是由一个指数元组 $(k_1, k_2, \dots, k_k)$ 描述。因此，原来的一个指数同余方程 $a^x \equiv b \pmod m$ 会分解成一个**线性[同余[方程](@entry_id:154048)组](@entry_id:193238)**，每个分量对应一个 [@problem_id:3089861]：
$$ \begin{cases} x \cdot \alpha_1 \equiv \beta_1 \pmod{n_1} \\ x \cdot \alpha_2 \equiv \beta_2 \pmod{n_2} \\ \vdots \\ x \cdot \alpha_k \equiv \beta_k \pmod{n_k} \end{cases} $$
这虽然仍然可以求解，但比单个方程要复杂得多。例如，$(\mathbb{Z}/8\mathbb{Z})^\times = \{1, 3, 5, 7\}$ 就不是循环群，因为其中每个非单位[元素的阶](@entry_id:145276)都是 $2$。它同构于 $C_2 \times C_2$。

### 核心机制：求解[同余](@entry_id:143700)方程

掌握了[离散对数](@entry_id:266196)的概念及其适用范围后，我们来系统地考察其在求解[同余](@entry_id:143700)方程中的应用。

#### 基本应用

考虑一个指数[同余](@entry_id:143700)方程 $g^{ax+b} \equiv y \pmod p$，其中 $p$ 是一个奇素数，$g$ 是模 $p$ 的一个[原根](@entry_id:163633)。群 $(\mathbb{Z}/p\mathbb{Z})^\times$ 的阶为 $n=p-1$。由于 $g$ 是生成元，[离散对数](@entry_id:266196)映射 $\log_g: (\mathbb{Z}/p\mathbb{Z})^\times \to \mathbb{Z}/n\mathbb{Z}$ 是一个定义良好的同构。我们可以对同余方程两边同时取[离散对数](@entry_id:266196)：
$$ \log_g(g^{ax+b}) \equiv \log_g(y) \pmod n $$
根据[离散对数](@entry_id:266196)的性质，这立即转化为一个关于未知数 $x$ 的[线性同余](@entry_id:150485)方程：
$$ ax+b \equiv \log_g(y) \pmod n $$
或者写作：
$$ ax \equiv \log_g(y) - b \pmod n $$
这个从指[数域](@entry_id:155558)到线性域的转换是[离散对数](@entry_id:266196)方法的核心。原指数[同余](@entry_id:143700)方程解的存在性与解的个数，现在完[全等](@entry_id:273198)价于这个[线性同余](@entry_id:150485)方程。根据[线性同余](@entry_id:150485)理论，该方程有解当且仅当 $\gcd(a, n)$ 整除 $\log_g(y) - b$。若有解，则模 $n$ 恰好有 $\gcd(a, n)$ 个不同的解。[@problem_id:3089887]

**例题**：求解 $3^x \equiv 5^7 \cdot 2^9 \pmod{29}$。
这里，$p=29$ 是一个素数，群 $(\mathbb{Z}/29\mathbb{Z})^\times$ 的阶为 $n=28$。已知 $g=2$ 是一个[原根](@entry_id:163633)。我们对原方程两边取以 $2$ 为底的[离散对数](@entry_id:266196)，得到一个在 $\mathbb{Z}/28\mathbb{Z}$ 中的[线性方程](@entry_id:151487) [@problem_id:3089884]：
$$ \log_2(3^x) \equiv \log_2(5^7 \cdot 2^9) \pmod{28} $$
$$ x \cdot \log_2(3) \equiv 7 \cdot \log_2(5) + 9 \cdot \log_2(2) \pmod{28} $$
通过计算（例如，逐个计算 $2$ 的幂次模 $29$），我们可以得到 $\log_2(3) = 5$ 和 $\log_2(5) = 22$。而根据定义，$\log_2(2) = 1$。代入方程：
$$ 5x \equiv 7 \cdot 22 + 9 \pmod{28} $$
$$ 5x \equiv 154 + 9 \equiv 163 \equiv 23 \pmod{28} $$
这是一个标准的[线性同余](@entry_id:150485)方程。为解此方程，我们需求 $5$ 模 $28$ 的逆元。由于 $5 \cdot 17 = 85 = 3 \cdot 28 + 1$，所以 $5^{-1} \equiv 17 \pmod{28}$。方程两边同乘以 $17$：
$$ x \equiv 23 \cdot 17 = 391 \equiv 27 \pmod{28} $$
因此，原指数[同余](@entry_id:143700)方程的解为 $x \equiv 27 \pmod{28}$。

#### 推广与复杂情况

[离散对数](@entry_id:266196)方法的应用不仅限于底是[原根](@entry_id:163633)的理想情况。

**1. 当底不是生成元时**
考虑方程 $a^x \equiv h \pmod p$，其中 $a$ 不是[原根](@entry_id:163633)。设 $a$ 在 $(\mathbb{Z}/p\mathbb{Z})^\times$ 中的阶为 $d$。由于 $a$ 不是[原根](@entry_id:163633)，$d$ 是 $p-1$ 的一个真因子。此时，由 $a$ 生成的[子群](@entry_id:146164) $\langle a \rangle = \{ a^k \pmod p \mid k \in \mathbb{Z} \}$ 只包含 $d$ 个元素，是 $(\mathbb{Z}/p\mathbb{Z})^\times$ 的一个[真子群](@entry_id:141915)。
- **可解性**：方程 $a^x \equiv h \pmod p$ 有解的**充要条件**是 $h$ 必须属于由 $a$ 生成的[子群](@entry_id:146164)，即 $h \in \langle a \rangle$。如果 $h$ 不在这个[子群](@entry_id:146164)中，方程无解。[@problem_id:3089851]
- **求解过程**：若 $h \in \langle a \rangle$，我们可以在[子群](@entry_id:146164) $\langle a \rangle$ 内部定义[离散对数](@entry_id:266196) $\log_a h$。此时，方程 $a^x \equiv h$ 等价于指数上的[线性同余](@entry_id:150485) $x \equiv \log_a h \pmod d$。注意，这里的模数是 $a$ 的阶 $d$，而不是群的阶 $p-1$。
- **解的个数**：方程 $x \equiv \log_a h \pmod d$ 在模 $d$ 意义下有唯一解。但如果我们考虑在完整的 $\mathbb{Z}/(p-1)\mathbb{Z}$ 环中的解，由于 $x$ 满足 $x=k d + \log_a h$ 的形式，在 $0$ 到 $p-2$ 的范围内，总共有 $(p-1)/d$ 个解。

例如，在模 $29$ 下， $g=4$ 的阶是 $14$（因为 $4^{14} \equiv (2^2)^{14} = 2^{28} \equiv 1 \pmod{29}$）。因此，$4^x \equiv h \pmod{29}$ 仅当 $h$ 是模 $29$ 的二次剩余时才有解。当有解时，例如 $4^x \equiv 16 \pmod{29}$，我们知道 $x=2$ 是一个解，其[解集](@entry_id:154326)为 $x \equiv 2 \pmod{14}$，即在模 $28$ 意义下有两个解：$x=2$ 和 $x=16$。[@problem_id:3089851]

**2. 当模数是[合数](@entry_id:263553)时**
考虑方程 $g^x \equiv h \pmod n$，其中 $n$ 是[合数](@entry_id:263553)。我们可以利用[中国剩余定理](@entry_id:144030)（CRT）将问题分解。设 $n$ 的[素数幂](@entry_id:636094)[因子分解](@entry_id:150389)为 $n = p_1^{k_1} p_2^{k_2} \cdots p_t^{k_t}$。原[同余](@entry_id:143700)方程等价于一个[同余方程组](@entry_id:154048)：
$$ \begin{cases} g^x \equiv h \pmod{p_1^{k_1}} \\ g^x \equiv h \pmod{p_2^{k_2}} \\ \vdots \\ g^x \equiv h \pmod{p_t^{k_t}} \end{cases} $$
我们可以对每个[素数幂](@entry_id:636094)模 $p_i^{k_i}$ 单独求解。在每个子问题中，我们都在群 $(\mathbb{Z}/p_i^{k_i}\mathbb{Z})^\times$ 中工作。设 $g$ 在该群中的阶为 $\text{ord}_{p_i^{k_i}}(g)$。求解 $g^x \equiv h \pmod{p_i^{k_i}}$ 会得到一个关于 $x$ 的[线性同余](@entry_id:150485)方程：
$$ x \equiv x_i \pmod{\text{ord}_{p_i^{k_i}}(g)} $$
通过为每个 $i=1, \dots, t$ 求解，我们得到一个关于 $x$ 的线性[同余[方程](@entry_id:154048)组](@entry_id:193238)。最后，再次使用中国剩余定理（或简单代换）求解这个关于 $x$ 的[方程组](@entry_id:193238)。最终解的模将是所有子问题中 $g$ 的阶的最小公倍数，即 $L = \text{lcm}(\text{ord}_{p_1^{k_1}}(g), \dots, \text{ord}_{p_t^{k_t}}(g))$。

**例题**：求解 $2^x \equiv 217 \pmod{275}$。
首先分解模数：$275 = 25 \cdot 11 = 5^2 \cdot 11$。方程等价于系统：
1.  $2^x \equiv 217 \equiv 17 \pmod{25}$
2.  $2^x \equiv 217 \equiv 8 \pmod{11}$

对于第一个方程，我们在 $(\mathbb{Z}/25\mathbb{Z})^\times$ 中求解。该[群阶](@entry_id:144396)为 $\varphi(25)=20$。通过计算 $2$ 的幂次，我们发现 $2^{13} \equiv 17 \pmod{25}$。$2$ 在模 $25$ 下的阶是 $20$。所以 $x \equiv 13 \pmod{20}$。

对于第二个方程，我们在 $(\mathbb{Z}/11\mathbb{Z})^\times$ 中求解。该[群阶](@entry_id:144396)为 $\varphi(11)=10$。$2^x \equiv 8 = 2^3 \pmod{11}$。$2$ 在模 $11$ 下的阶是 $10$。所以 $x \equiv 3 \pmod{10}$。

现在我们有一个关于 $x$ 的系统：
$$ \begin{cases} x \equiv 13 \pmod{20} \\ x \equiv 3 \pmod{10} \end{cases} $$
注意到第二个同余式是第一个的推论（若 $x=20k+13$，则 $x \equiv 13 \equiv 3 \pmod{10}$），所以系统是相容的，其解就是更强的那个条件：$x \equiv 13 \pmod{20}$。最终解的模是 $\text{lcm}(20, 10) = 20$。[@problem_id:3089847]

### 计算[离散对数](@entry_id:266196)的算法

到目前为止，我们假设[离散对数](@entry_id:266196) $\log_g(h)$ 是可以“计算”出来的。然而，对于大的群，计算[离散对数](@entry_id:266196)是一个非常困难的问题，这一困难性正是许多现代公钥密码体制（如[Diffie-Hellman密钥交换](@entry_id:144570)和DSA[数字签名](@entry_id:269311)）安全性的基础。尽管如此，在特定条件下，存在比暴力枚举（尝试所有可能的指数）更有效的算法。

#### Pohlig-Hellman 算法

当群的阶 $m$ 是一个**平滑数**（即其所有素因子都很小）时，[Pohlig-Hellman算法](@entry_id:272142)非常有效。其核心思想与我们处理[合数](@entry_id:263553)模的方法类似：利用中国剩余定理将大问题分解为多个小问题。

设群 $G = \langle g \rangle$ 的阶为 $m$，其[素数幂](@entry_id:636094)分解为 $m = p_1^{e_1} p_2^{e_2} \cdots p_r^{e_r}$。我们的目标是计算 $x = \log_g h$。该算法分别计算 $x$ 模每个 $p_i^{e_i}$ 的值，然后用[中国剩余定理](@entry_id:144030)合并结果。

为了求 $x \pmod{p_i^{e_i}}$，我们设 $x_i = x \pmod{p_i^{e_i}}$。考虑元素 $g' = g^{m/p_i^{e_i}}$ 和 $h' = h^{m/p_i^{e_i}}$。$g'$ 的阶为 $p_i^{e_i}$。我们有：
$$ (g')^x = g^{x \cdot m/p_i^{e_i}} = (g^x)^{m/p_i^{e_i}} = h^{m/p_i^{e_i}} = h' $$
由于 $x \equiv x_i \pmod{p_i^{e_i}}$，所以 $g'^{x_i} = g'^{x} = h'$。现在问题转化为在阶为 $p_i^{e_i}$ 的[子群](@entry_id:146164) $\langle g' \rangle$ 中求解[离散对数](@entry_id:266196) $x_i = \log_{g'} h'$。如果 $p_i$ 很小，这个问题就容易解决（例如，通过逐级提升或小规模的BSGS）。

在获得所有 $x_i \equiv x \pmod{p_i^{e_i}}$ 后，就可以通过中国剩余定理得到唯一的 $x \pmod m$。[@problem_id:3089875]

#### Baby-Step Giant-Step (BSGS) 算法

这是一个通用的[时空权衡](@entry_id:755997)算法，适用于任何[有限循环群](@entry_id:147298)。其[时间复杂度](@entry_id:145062)和[空间复杂度](@entry_id:136795)大约都是 $O(\sqrt{m})$，其中 $m$ 是[群的阶](@entry_id:137115)。

要解 $g^x \equiv h \pmod p$，其中[群阶](@entry_id:144396)为 $m$。设 $N = \lceil\sqrt{m}\rceil$。我们可以将 $x$ 写成 $x = iN - j$ 的形式，其中 $1 \le i \le N$ 且 $0 \le j  N$。方程变为 $g^{iN-j} \equiv h$，即 $g^{iN} \equiv h g^j$。

算法步骤如下：
1.  **Baby Steps**: 计算并存储所有 $h \cdot g^j \pmod p$ 的值，以及对应的 $j$，其中 $j$ 从 $0$ 到 $N-1$。通常使用[哈希表](@entry_id:266620)来存储，以实现快速查找。
2.  **Giant Steps**: 依次计算 $(g^N)^i \pmod p$，其中 $i$ 从 $1$ 到 $N$。对于每个计算出的值，检查它是否存在于第一步的[哈希表](@entry_id:266620)中。
3.  **Collision**: 如果找到匹配，即 $(g^N)^i \equiv h \cdot g^j$，那么我们就找到了一个解 $x = iN - j$。

该算法保证能找到解，因为 $x$ 一定可以表示为所需形式。例如，在计算 $\log_2(37) \pmod{101}$ 时（[群阶](@entry_id:144396) $m=100$），我们可以取 $N=10$。计算 baby steps $37 \cdot 2^j$ for $j=0..9$ 和 giant steps $(2^{10})^i$ for $i=1..10$，最终会找到碰撞，从而确定对数值。[@problem_id:3089897]

#### 指数微积分方法 (Index Calculus Method)

这是一种更高级的、针对特定群（如 $(\mathbb{Z}/p\mathbb{Z})^\times$）的[亚指数时间](@entry_id:263548)算法。它对非常大的素数 $p$ 比BSGS更有效。

其基本思想是：
1.  **选择[因子基](@entry_id:637504)**: 选择一个由小素数组成的集合 $\mathcal{B}=\{q_1, q_2, \dots, q_t\}$。
2.  **收集关系**: 随机选择指数 $e$，计算 $g^e \pmod p$。如果结果可以完全分解为[因子基](@entry_id:637504)中素数的乘积（即 $g^e \equiv \prod q_j^{a_j} \pmod p$），我们就记录下这个关系。对这个关系两边取[离散对数](@entry_id:266196)，得到一个关于[因子基](@entry_id:637504)元素对数的线性方程：$e \equiv \sum a_j \log_g(q_j) \pmod{p-1}$。
3.  **[求解线性系统](@entry_id:146035)**: 重复第二步，直到收集到足够多的（至少 $t$ 个独立的）[线性方程](@entry_id:151487)。然后求解这个[线性方程组](@entry_id:148943)，得到[因子基](@entry_id:637504)中每个素数的[离散对数](@entry_id:266196) $\log_g(q_j)$。
4.  **求解目标**: 现在要计算 $\log_g(h)$。我们随机选择一个指数 $s$，计算 $h \cdot g^s \pmod p$，并检查结果是否能分解为[因子基](@entry_id:637504)中的素数。如果 $h \cdot g^s \equiv \prod q_j^{b_j} \pmod p$，那么取对数得到 $\log_g(h) + s \equiv \sum b_j \log_g(q_j) \pmod{p-1}$。由于 $\log_g(q_j)$ 都已知，我们可以直接解出 $\log_g(h)$。

**例题**：假设在群 $(\mathbb{F}_p)^\times$ 中（$p-1=100$），我们有[因子基](@entry_id:637504) $\mathcal{B}=\{2,3,5\}$，并收集到如下关系 [@problem_id:3089894]：
- $g^{23} \equiv 2^1 \cdot 3^2 \pmod p \implies 23 \equiv \log_g(2) + 2\log_g(3) \pmod{100}$
- $g^{14} \equiv 2^3 \cdot 5^1 \pmod p \implies 14 \equiv 3\log_g(2) + \log_g(5) \pmod{100}$
- $g^{35} \equiv 3^1 \cdot 5^2 \pmod p \implies 35 \equiv \log_g(3) + 2\log_g(5) \pmod{100}$

这是一个关于 $\log_g(2), \log_g(3), \log_g(5)$ 的三元线性方程组。解出它们后，我们就可以计算任何能被 $2,3,5$ 分解的数的[离散对数](@entry_id:266196)。例如，要计算 $\log_g(60)$，由于 $60 = 2^2 \cdot 3 \cdot 5$，我们有：
$$ \log_g(60) \equiv 2\log_g(2) + \log_g(3) + \log_g(5) \pmod{100} $$
将解出的值代入即可。

本章我们系统地建立了[离散对数](@entry_id:266196)的理论框架，从其定义、存在条件，到解决各类指数[同余](@entry_id:143700)方程的核心机制，最后介绍了三种重要的计算算法。[离散对数](@entry_id:266196)不仅是数论中一个优美的理论工具，更是连接纯粹数学与[现代密码学](@entry_id:274529)等应用领域的关键桥梁。