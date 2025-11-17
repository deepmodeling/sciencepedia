## 引言
量子纠错是实现大规模[容错量子计算](@entry_id:142498)的基石，而如何系统性地设计出性能优越的量子纠错码则是一个核心挑战。幸运的是，我们无需从零开始。长达数十年的经典[纠错码](@entry_id:153794)理论为我们提供了丰富而强大的数学工具和现成的码族。本文旨在搭建一座从经典编码到[量子编码](@entry_id:141173)的桥梁，解决如何利用经典码的成熟结构来应对量子世界中独特错误类型的问题。

通过阅读本文，您将踏上一段从基础到前沿的探索之旅。在“原理与机制”一章中，我们将深入剖析将经典码转化为量子码的核心配方，从基础的 Calderbank-Shor-Steane (CSS) 构造到更普适的厄米构造和纠缠辅助方法，揭示其背后的数学原理。随后，在“应用与交叉学科联系”一章，您将看到这些理论如何应用于[里德-穆勒码](@entry_id:266423)、[戈莱码](@entry_id:264283)等著名经典码族，并领略其与代数拓扑、群论等领域产生的深刻共鸣。最后，“动手实践”部分将提供具体的练习，帮助您将理论知识转化为解决实际问题的能力，真正掌握从经典码构建量子码的精髓。

## 原理与机制

本章旨在系统性地阐述如何利用经典[纠错码](@entry_id:153794)的丰富理论和结构来构建[量子纠错码](@entry_id:266787)。我们将从最基础的Calderbank-Shor-Steane (CSS) 构造出发，逐步深入到更高级和更普适的方法，如厄米构造 (Hermitian construction)、[纠缠辅助量子纠错码](@entry_id:144178) (EAQEC)、基于环的码以及子系统码。本章的目标是揭示这些构造方法背后的数学原理和核心机制，并通过具体的例子阐明其应用。

### [稳定子码](@entry_id:143150)的[辛表示](@entry_id:183193)框架

[量子稳定子码](@entry_id:137507)的核心思想是将量子码空间定义为[稳定子群](@entry_id:137216) $S$ 的公共+1特征空间。[稳定子群](@entry_id:137216)是[泡利群](@entry_id:136414) $\mathcal{P}_n$ 的一个[阿贝尔子群](@entry_id:142799)。要使一个[稳定子码](@entry_id:143150)有效，其所有生成元必须相互对易。这一对易条件可以被优雅地映射到经典线性代数的框架中。

考虑一个作用于 $n$ 个[量子比特](@entry_id:137928)的系统，其对应的“相空间”是一个在[有限域](@entry_id:142106) $\mathbb{F}_2$ 上的 $2n$ 维[向量空间](@entry_id:151108) $\mathbb{F}_2^{2n}$。该空间中的任意向量 $v$ 可以表示为 $v = (x|z)$，其中 $x, z \in \mathbb{F}_2^n$ 分别对应于泡利 $X$ 和 $Z$ 算子的位置。例如，向量 $(e_i|e_j)$ 对应于泡利算子 $X_i Z_j$，其中 $e_i$ 是第 $i$ 个分量为1的[单位向量](@entry_id:165907)。

在这个空间中，我们可以定义一个**辛[内积](@entry_id:158127)** (symplectic inner product)。对于任意两个向量 $u = (u_x|u_z)$ 和 $v = (v_x|v_z)$，其辛[内积](@entry_id:158127)定义为：
$$ (u|v)_s = u_x \cdot v_z + u_z \cdot v_x \pmod 2 $$
其中“$\cdot$”表示 $\mathbb{F}_2^n$ 中的标准欧几里得[点积](@entry_id:149019)。两个泡利算子 $P_u$ 和 $P_v$ 对易的充分必要条件是其对应的向量 $u$ 和 $v$ 的辛[内积](@entry_id:158127)为零，即 $(u|v)_s = 0$。

因此，一个有效的[稳定子群](@entry_id:137216) $S$ 对应于 $\mathbb{F}_2^{2n}$ 中的一个**迷向[子空间](@entry_id:150286)** (isotropic subspace) $\mathcal{S}$。迷向[子空间](@entry_id:150286)的定义是 $\mathcal{S} \subseteq \mathcal{S}^{\perp_s}$，其中 $\mathcal{S}^{\perp_s}$ 是 $\mathcal{S}$ 在辛[内积](@entry_id:158127)下的**辛对偶** (symplectic dual) 或**[零化子](@entry_id:155446)** (annihilator)：
$$ \mathcal{S}^{\perp_s} = \{ v \in \mathbb{F}_2^{2n} \mid (v|u)_s = 0 \text{ for all } u \in \mathcal{S} \} $$
辛[内积](@entry_id:158127)是非简并的，这意味着对于任意子空间 $\mathcal{S}$，其维度与其辛对偶的维度之和等于整个空间的维度：
$$ \dim(\mathcal{S}) + \dim(\mathcal{S}^{\perp_s}) = 2n $$
一个[稳定子码](@entry_id:143150)编码的[逻辑量子比特](@entry_id:142662)数 $K$ 由 $\mathcal{S}$ 和 $\mathcal{S}^{\perp_s}$ 之间的关系确定。逻辑算子对应于商空间 $\mathcal{S}^{\perp_s} / \mathcal{S}$ 中的元素。因此，逻辑量子比特数 $K$ 为：
$$ K = \dim(\mathcal{S}^{\perp_s}) - \dim(\mathcal{S}) $$
结合维度公式，我们也可以得到 $K = 2n - 2\dim(\mathcal{S}^{\perp_s})$ 或者 $K = 2n - 2\dim(\mathcal{S})$ 吗？不，是 $K = \dim(\mathcal{S}^{\perp_s}) - \dim(\mathcal{S}) = (2n - \dim(\mathcal{S})) - \dim(\mathcal{S}) = 2n - 2\dim(\mathcal{S})$。

我们可以通过一个例子来理解这个框架。考虑一个经典码 $C \subseteq \mathbb{F}_2^n$，我们可以通过**对角嵌入** (diagonal embedding) 将其映射到辛空间 $\mathbb{F}_2^{2n}$ 中，定义为 $\mathcal{D}(C) = \{ (c|c) \mid c \in C \}$。这是一个维度为 $\dim(\mathcal{D}(C)) = \dim(C)$ 的[子空间](@entry_id:150286)。我们可以验证这个[子空间](@entry_id:150286)总是迷向的，因为对于任意两个元素 $(c_1|c_1), (c_2|c_2) \in \mathcal{D}(C)$，它们的辛[内积](@entry_id:158127)为 $(c_1|c_1)_s \cdot (c_2|c_2) = c_1 \cdot c_2 + c_1 \cdot c_2 = 2(c_1 \cdot c_2) \equiv 0 \pmod 2$。

例如，考虑一阶[里德-穆勒码](@entry_id:266423) (Reed-Muller code) $C = RM(1,3)$ [@problem_id:100918]。这是一个长度 $n=2^3=8$ 的码，其维度 $k = \binom{3}{0} + \binom{3}{1} = 4$。其对角嵌入 $\mathcal{D}(C)$ 是 $\mathbb{F}_2^{16}$ 中的一个4维[子空间](@entry_id:150286)。利用维度公式，其辛对偶的维度为 $\dim(\mathcal{D}(C)^{\perp_s}) = 2n - \dim(\mathcal{D}(C)) = 16 - 4 = 12$。

### Calderbank-Shor-Steane (CSS) 构造

[CSS构造](@entry_id:137974)是利用经典码构建量子码最直接和最著名的方法之一。其核心思想是分别使用两个经典码来处理 $X$ 型错误（位翻转）和 $Z$ 型错误（相位翻转）。

#### 二元[CSS码](@entry_id:143038)

给定两个长度为 $n$ 的经典二元[线性码](@entry_id:261038) $C_X$ 和 $C_Z$。我们构造一个[稳定子群](@entry_id:137216)，其生成元由两部分组成：
1.  $Z$ 型稳定子：由 $C_Z$ 的校验矩阵 $H_Z$ 的行向量定义。这些稳定子用于探测 $X$ 型错误。
2.  $X$ 型稳定子：由 $C_X$ 的校验矩阵 $H_X$ 的行向量定义。这些稳定子用于探测 $Z$ 型错误。

在[辛表示](@entry_id:183193)框架下，这对应于选择[稳定子空间](@entry_id:269618)为 $\mathcal{S} = C_X^{\perp} \times C_Z \subseteq \mathbb{F}_2^{2n}$。其中 $C_X^\perp$ 是 $C_X$ 的欧几里得对偶码，其[生成矩阵](@entry_id:275809)即为 $C_X$ 的校验矩阵 $H_X$ 的行。

为了使所有稳定子生成元相互对易，这个[子空间](@entry_id:150286) $\mathcal{S}$ 必须是迷向的。对于任意 $(u|v) \in C_X^\perp \times C_Z$ 和 $(u'|v') \in C_X^\perp \times C_Z$，我们需要 $((u|v)|(u'|v'))_s = u \cdot v' + v \cdot u' = 0$。由于 $u, u'$ 来自 $C_X^\perp$，$v, v'$ 来自 $C_Z$，这个条件可以简化为 $u \cdot v' = 0$ 对所有 $u \in C_X^\perp, v' \in C_Z$ 都成立。这等价于 $C_Z \subseteq (C_X^\perp)^\perp = C_X$。然而，通常的表述是 $C_X^\perp \subseteq C_Z$。让我们重新审视一下：$Z$ 型稳定子由 $C_Z$ 的校验矩阵 $H_Z$ 定义，这意味着[稳定子空间](@entry_id:269618)对应 $C_Z^\perp$。$X$ 型稳定子由 $C_X$ 的校验矩阵 $H_X$ 定义，[稳定子空间](@entry_id:269618)对应 $C_X^\perp$。不，这是错误的。$Z$ 型稳定子形如 $Z(c)$ 其中 $c \in C_Z$。$X$ 型稳定子形如 $X(c')$ 其中 $c' \in C_X$。[稳定子群](@entry_id:137216) $S$ 由 $\{X(c) \mid c \in C_X\}$ 和 $\{Z(c') \mid c' \in C_Z\}$ 生成。对易条件 $[X(c), Z(c')] = 0$ 要求 $c \cdot c' = 0$。这必须对所有 $c \in C_X, c' \in C_Z$ 成立，即 $C_X \subseteq C_Z^\perp$ 或 $C_Z \subseteq C_X^\perp$。传统上，我们选择的生成元是 $\{X(c) \mid c \in C_1\}$ 和 $\{Z(c) \mid c \in C_2\}$。对易条件要求 $C_1 \subseteq C_2^\perp$。这样，[稳定子空间](@entry_id:269618)为 $\mathcal{S} \approx C_1 \times C_2$。

让我们遵循标准教材。稳定子由 $H_X$ 的行（用于 $X$ 型）和 $H_Z$ 的行（用于 $Z$ 型）定义。$C_X$ 是由 $H_X$ 校验的码，$C_Z$ 是由 $H_Z$ 校验的码。对易条件要求 $H_X H_Z^T = 0$。这意味着 $H_X$ 的每一行都与 $H_Z$ 的每一行正交。这等价于 $C_Z^\perp \subseteq C_X$。

如果这个**对偶包含** (dual-containment) 条件成立，那么就可以构造一个有效的[CSS码](@entry_id:143038)。其编码的[逻辑量子比特](@entry_id:142662)数 $K$ 为：
$$ K = \dim(C_X) + \dim(C_Z) - n $$
其中 $n$ 是码长，$\dim(C_X)$ 和 $\dim(C_Z)$ 分别是两个经典码的维度。

一个特别重要且简洁的特例是**对偶包含码** (dual-containing code)。如果我们只使用一个经典码 $C$，并令 $C_X = C$ 和 $C_Z = C^\perp$，那么对偶包含条件 $C_Z^\perp \subseteq C_X$ 就变成了 $(C^\perp)^\perp \subseteq C$，即 $C \subseteq C$，这是平凡成立的。此时，$K = \dim(C) + \dim(C^\perp) - n = \dim(C) + (n - \dim(C)) - n = 0$。这不是我们想要的。

正确的构造是，我们选择两个码 $C_1, C_2$ 并要求 $C_2^\perp \subseteq C_1$。[稳定子群](@entry_id:137216)由 $H_1$ (对 $C_1$) 的行生成 $X$ 型稳定子，由 $H_2$ (对 $C_2$) 的行生成 $Z$ 型稳定子。逻辑比特数为 $K = \dim(C_1) - \dim(C_2^\perp) = k_1+k_2-n$。
一个更常见的特例是使用一个**自正交码** (self-orthogonal code) $C$，满足 $C \subseteq C^\perp$。如果我们令 $C_1 = C^\perp$ 和 $C_2=C$，则条件 $C_2^\perp \subseteq C_1$ 变为 $C^\perp \subseteq C^\perp$，平凡成立。此时 $K = \dim(C^\perp) + \dim(C) - n = (n-k)+k-n=0$。这也不对。

让我们回到问题中的描述。[@problem_id:100896] 明确指出，对于[CSS码](@entry_id:143038)，$C_X^\perp \subseteq C_Z$。当使用单个对偶包含码 $C^\perp \subseteq C$ 时，我们选择 $C_X=C_Z=C$。此时条件 $C^\perp \subseteq C$ 得到满足，逻辑比特数为 $K = \dim(C) + \dim(C) - n = 2k-n$。

如何判断一个码是否为对偶包含码？如果一个码 $C$ 由校验矩阵 $H$ 定义，那么 $C^\perp \subseteq C$ 的条件等价于 $H H^T = 0$。
例如，考虑一个由以下 $4 \times 8$ 校验矩阵 $H$ 定义的经典码 $C$ [@problem_id:100896]：
$$ H = \begin{pmatrix} 1  1  1  1  0  0  0  0 \\ 0  0  1  1  1  1  0  0 \\ 0  0  0  0  1  1  1  1 \\ 1  1  0  0  0  0  1  1 \end{pmatrix} $$
可以验证该矩阵满足 $H H^T = 0$。此码的长度为 $n=8$。通过行化简可以发现 $\text{rank}(H)=3$。因此，经典码的维度是 $k = n - \text{rank}(H) = 8 - 3 = 5$。由此构造的量子[CSS码](@entry_id:143038)编码的逻辑量子比特数为 $K = 2k-n = 2(5) - 8 = 2$。

我们可以使用具有良好[对偶性质](@entry_id:276134)的著名码族来构造[CSS码](@entry_id:143038)。例如，[里德-穆勒码](@entry_id:266423) $RM(r,m)$ 的对偶是 $RM(m-r-1, m)$。要满足条件 $C_2^\perp \subseteq C_1$，我们可以选择 $C_1 = RM(r_1, m)$ 和 $C_2 = RM(r_2, m)$，条件变为 $RM(m-r_2-1, m) \subseteq RM(r_1, m)$。根据[里德-穆勒码](@entry_id:266423)的性质，这等价于 $m-r_2-1 \le r_1$。例如，当 $m=5, r_1=3, r_2=2$ 时 [@problem_id:100920]，条件是 $5-2-1=2 \le 3$，成立。此时码长 $n=2^5=32$， $k_1 = \dim(RM(3,5)) = \sum_{i=0}^3 \binom{5}{i} = 26$， $k_2 = \dim(RM(2,5)) = \sum_{i=0}^2 \binom{5}{i} = 16$。逻辑量子比特数为 $K=k_1+k_2-n = 26+16-32=10$。

#### Qudit CSS 码

[CSS构造](@entry_id:137974)可以推广到 $q$ 元量子系统（qudit），其中 $q=p^m$ 是一个素数的幂。此时，我们使用定义在有限域 $\mathbb{F}_q$ 上的经典码。对易关系 $Z(v)X(u) = \omega^{\text{Tr}(v \cdot u)} X(u)Z(v)$，其中 $\omega=e^{2\pi i/p}$，$\text{Tr}: \mathbb{F}_q \to \mathbb{F}_p$ 是[迹映射](@entry_id:194370)。
对易条件变为 $\text{Tr}(v \cdot u) = 0$。如果我们从两个码 $C_1, C_2 \subseteq \mathbb{F}_q^n$ 构造，则需要 $C_2 \subseteq C_1^{\perp_{Tr}}$，其中 $C_1^{\perp_{Tr}}$ 是 $C_1$ 的**迹对偶** (trace-dual)。满足此条件时，编码的逻辑 qudit 数为 $k=k_1+k_2-n$，其中 $k_1=\dim(C_1), k_2=\dim(C_2)$ [@problem_id:100841]。

### 厄米构造 (Hermitian Construction)

当底层的量子系统是 qudit 时，特别是在 $\mathbb{F}_q$ 上，一种极其强大的构造方法是使用定义在二次扩张域 $\mathbb{F}_{q^2}$ 上的经典码。这种方法被称为厄米构造。

设 $\mathbb{F}_{q^2}$ 是一个有限域。其[弗罗贝尼乌斯自同构](@entry_id:154475) (Frobenius automorphism) $z \mapsto z^q$ 定义了一个共轭运算 $\bar{z} = z^q$。基于此，我们定义**[厄米内积](@entry_id:141742)** (Hermitian inner product)：
$$ (u, v)_H = \sum_{i=1}^n u_i \bar{v_i} $$
一个码 $C \subseteq \mathbb{F}_{q^2}^n$ 的**厄米对偶** (Hermitian dual) 是 $C^{\perp_H} = \{v \in \mathbb{F}_{q^2}^n \mid (c, v)_H = 0 \text{ for all } c \in C\}$。[厄米内积](@entry_id:141742)是非简并的，因此 $\dim(C) + \dim(C^{\perp_H}) = n$。

与欧几里得[内积](@entry_id:158127)相比，[厄米内积](@entry_id:141742)具有不同的性质。例如，在 $\mathbb{F}_4 = \{0, 1, \omega, \omega^2\}$ 上，共轭运算为 $\bar{\omega}=\omega^2, \overline{\omega^2}=\omega$。一个向量可能与其自身是欧几里得正交的，但不是厄米正交的 [@problem_id:100923]。

厄米构造的核心思想是，如果一个经典码 $C \subseteq \mathbb{F}_{q^2}^n$ 满足**厄米自正交** (Hermitian self-orthogonal) 条件，即 $C \subseteq C^{\perp_H}$，那么就可以从中导出一个 $\mathbb{F}_q$ 上的[量子稳定子码](@entry_id:137507)。该量子码编码的逻辑 qudit 数 $k$ 为：
$$ k = \dim(C^{\perp_H}) - \dim(C) = n - 2\dim(C) $$
这个公式直接源于[稳定子码](@entry_id:143150)的[辛表示](@entry_id:183193)框架，其中稳定子和逻辑算[子空间](@entry_id:150286)与 $C$ 和 $C^{\perp_H}$ 相关联。例如，如果一个码长为 $n=11$、维度为 $k_{cl}=4$ 的码 $C$ over $\mathbb{F}_9$ 满足 $C \subseteq C^{\perp_H}$，那么其厄米对偶的维度是 $\dim(C^{\perp_H}) = 11-4=7$。由此得到的 $\mathbb{F}_3$ 上的量子码将编码 $k = 7-4=3$ 个逻辑qutrit [@problem_id:100917]。

一个相关但不同的情况是**厄米对偶包含** (Hermitian dual-containing) 条件 $C^{\perp_H} \subseteq C$。这种情况（有时称为CRS构造）产生的量子码编码的逻辑 qudit 数为 $K = 2k-n$，其中 $k=\dim(C)$。其量子距离 $D$ 由 $C$ 中不属于 $C^{\perp_H}$ 的最小重量码字决定：$D = \min\{\text{wt}(c) \mid c \in C \setminus C^{\perp_H}\}$ [@problem_id:100892]。

厄米构造在构建具有优良参数的量子码方面特别有效，尤其是量子[MDS码](@entry_id:272386)（即达到量子[Singleton界](@entry_id:269293)的码）。通过精心选择广义[里德-所罗门码](@entry_id:142231) (GRS code) 的参数，可以确保其满足厄米自正交或对偶包含条件，从而产生量子[MDS码](@entry_id:272386) [@problem_id:100854]。

### 超越自正交性：[纠缠辅助量子纠错码](@entry_id:144178)

标准[稳定子码](@entry_id:143150)和[CSS码](@entry_id:143038)的构造都依赖于某种形式的自正交性或对偶包含条件。如果一个经典码不满足这些条件，我们是否就无法用它来构建量子码？答案是否定的。通过允许发送方和接收方之间预先共享**纠缠态**（例如贝尔对），我们可以放宽这些限制。这就是**[纠缠辅助量子纠错码](@entry_id:144178)** (Entanglement-Assisted Quantum Error-Correcting Codes, EAQEC) 的思想。

所需的纠缠资源量 $c$（以 ebit 或 e-dit 计量）恰好弥补了经典码通勤条件的“失败”程度。对于从单个经典码 $C$ 构建的EAQEC，这个失败程度由码与其对偶的交集，即**码的壳** (hull of the code)，来量化。

在二元情况下，对于一个经典码 $C \subseteq \mathbb{F}_2^n$，其欧几里得壳为 $C \cap C^\perp$。所需的纠缠比特数 $c$ 就等于这个壳的维度：
$$ c = \dim(C \cap C^\perp) $$
这个维度可以通过[生成矩阵](@entry_id:275809) $G$ 或校验矩阵 $H$ 计算。使用[生成矩阵](@entry_id:275809) $G$，维度为 $c = k - \text{rank}(GG^T)$，其中 $k=\dim(C)$ [@problem_id:100909]。使用校验矩阵 $H$，维度为 $c = \text{rank}(HH^T)$ [@problem_id:100964]。
一旦确定了所需的纠缠数 $c$，编码的[逻辑量子比特](@entry_id:142662)数 $K$ 就由以下公式给出：
$$ K = k - c \quad \text{或更通用的} \quad K = 2k - n + c $$
这两个公式看似不同，但描述的是不同类型的EAQEC构造。例如，使用校验矩阵 $H$ 定义稳定子，所需的纠缠为 $c = \text{rank}(HH^T)$，逻辑比特数为 $K = n - 2\text{rank}(H) + c = k - (n-k) + c = 2k-n+c$ [@problem_id:100964]。

这个框架可以推广到两个经典码 $C_1, C_2$ 的情况。类似于[CSS构造](@entry_id:137974)，我们可以从 $C_1$ 和 $C_2$ 构建一个EAQEC。所需的纠缠比特数 $c$ 由 $H_1 H_2^T$ 的秩决定，而逻辑量子比特数 $K$ 仍然是 $K = k_1+k_2-n$ [@problem_id:100939]。

对于 qudit 码，特别是基于 $\mathbb{F}_{q^2}$ 上经典码的构造，所需的纠缠量由**厄米壳** (Hermitian hull) $C \cap C^{\perp_H}$ 的维度给出 [@problem_id:100878]：
$$ c = \dim(C \cap C^{\perp_H}) $$

### 基于环上码的构造

除了在有限域上定义经典码，我们还可以在更复杂的[代数结构](@entry_id:137052)——环 (ring)——上定义码，并从中构建量子码。这种方法已被证明非常富有成果。

#### $\mathbb{Z}_4$ 构造

一种经典方法是使用在整数模4环 $\mathbb{Z}_4 = \{0, 1, 2, 3\}$ 上定义的[线性码](@entry_id:261038)。对于一个 $\mathbb{Z}_4$ 上的[线性码](@entry_id:261038) $C$，如果它是**自对偶**的（即 $C=C^\perp$，其中对偶是在 $\mathbb{Z}_4$ 上定义的），我们可以通过一个特定的映射导出一个二元量子[CSS码](@entry_id:143038)。

这个过程涉及两个步骤：
1.  定义一个二元码 $C_1 = \{c \pmod 2 \mid c \in C\}$。这是将 $C$ 中所有码字的每个分量模2约化后得到的码。
2.  定义另一个二元码 $C_0 = \{v \in \mathbb{F}_2^n \mid 2v \in C\}$。这里的 $2v$ 是将二元向量 $v$ 的 $1$ 映射为 $\mathbb{Z}_4$ 中的 $2$， $0$ 映射为 $0$ 后得到的向量。

如果 $C$ 是自对偶的，那么可以证明 $C_0 \subseteq C_1$。因此，我们可以使用 $(C_1, C_0)$ 这对码来构建一个标准的二元[CSS码](@entry_id:143038)（技术上是 $\text{CSS}(C_1, C_0^\perp)$，但由于 $C_0 \subseteq C_1 \implies C_1^\perp \subseteq C_0^\perp$，对易条件成立）。该量子码编码的[逻辑量子比特](@entry_id:142662)数 $K$ 为：
$$ K = \dim(C_1) - \dim(C_0) $$
例如，给定一个 $\mathbb{Z}_4$ 上的[自对偶码](@entry_id:143974) $C$ 的[生成矩阵](@entry_id:275809) $G$，我们可以通过计算 $G \pmod 2$ 的秩来确定 $\dim(C_1)$。然后，通过分析哪些系数线性组合会产生所有分量均为偶数的码字，我们可以找到 $C_0$ 的结构并计算其维度 $\dim(C_0)$，最终得到 $K$ [@problem_id:100788]。

#### 基于 $R = \mathbb{F}_2[u]/(u^2=0)$ 的构造

另一种方法是使用在环 $R = \mathbb{F}_2[u]/(u^2=0)$ 上定义的码。这个环的元素形式为 $a+bu$，其中 $a,b \in \mathbb{F}_2$。如果一个 $R$ 上的[线性码](@entry_id:261038) $C$ 是自正交的（即对于任意 $c, c' \in C$，它们的欧几里得[内积](@entry_id:158127)为零），我们也可以构建一个二元量子码。

这个过程也涉及定义两个相关的二元码：
1.  $C_1 = \{ a \in \mathbb{F}_2^n \mid \exists b \in \mathbb{F}_2^n \text{ s.t. } a+ub \in C \}$。这是码字中“非 $u$”部分的集合。
2.  $C_2 = \{ b \in \mathbb{F}_2^n \mid ub \in C \}$。这是码字中 $u$ 的系数部分的集合，但仅限于那些“非 $u$”部分为零的码字。

$C$ 的自正交性保证了 $C_2 \subseteq C_1^\perp$。这允许我们构建一个[CSS码](@entry_id:143038) $Q = \text{CSS}(C_1^\perp, C_2)$。其逻辑量子比特数 $k_q$ 为：
$$ k_q = \dim(C_1^\perp) - \dim(C_2) = n - \dim(C_1) - \dim(C_2) $$
通过分析 $C$ 的生成元，我们可以推导出 $C_1$ 和 $C_2$ 的结构和维度，从而计算出 $k_q$ [@problem_id:100926]。

### 子系统码与规范群

到目前为止我们讨论的都是[稳定子码](@entry_id:143150)。**子系统码** (subsystem code) 是[稳定子码](@entry_id:143150)的一个重要推广。在[稳定子码](@entry_id:143150)中，任何可测量的、与所有稳定子生成元对易但又不属于[稳定子群](@entry_id:137216)的算子都是逻辑算子。而在子系统码中，我们把这些算子中的一部分指定为**规范算子** (gauge operators)。

规范算子与稳定子生成元一起构成**规范群** (gauge group) $\mathcal{G}$。规范[群的中心](@entry_id:141952)，即与所有规范算子都对易的元素构成的[子群](@entry_id:146164)，才是真正的[稳定子群](@entry_id:137216) $S = Z(\mathcal{G})$。逻辑算子是那些与整个[规范群](@entry_id:144761) $\mathcal{G}$ 对易，但又不属于 $\mathcal{G}$ 的算子。这种区分允许我们忽略由规范算子引起的“错误”，只关注那些连稳定子都无法探测的错误。

我们可以从任何一个[稳定子码](@entry_id:143150)构造出一个子系统码。只需选择一个或多个稳定子生成元，并将它们“提升”为规范算子。例如，从 $[[7,1,3]]$ [Steane码](@entry_id:144943)开始，其[稳定子群](@entry_id:137216)由6个生成元 $\{S_1, \dots, S_6\}$ 构成。如果我们选择 $S_1$ 作为规范算子 $\bar{Z}_G = S_1$，并引入一个与之[反交换的](@entry_id:262442)共轭规范算子 $\bar{X}_G$（例如 $\bar{X}_G=X_1$），那么新的[稳定子群](@entry_id:137216)就只有5个生成元 $\{S_2, \dots, S_6\}$。新的[规范群](@entry_id:144761) $\mathcal{G}' = \langle S_2, \dots, S_6, \bar{Z}_G, \bar{X}_G \rangle$。这个新的子系统码的参数，如距离，会因此发生改变 [@problem_id:100826]。

子系统码提供了一个更灵活的框架，许多重要的量子码，如**Bacon-Shor码**，本质上就是子系统码。在一个 $M \times L$ 的二维网格上，Bacon-Shor码的规范群由局部的、作用在相邻[量子比特](@entry_id:137928)上的 $X_i X_{i+1}$ 和 $Z_j Z_{j+1}$ 型算子生成。这些生成元可以看作是经典[重复码](@entry_id:267088)的[量子模拟](@entry_id:145469)。该码编码一个[逻辑量子比特](@entry_id:142662)，逻辑算子是作用于整行或整列的全局算子 [@problem_id:100938]。有趣的是，如果我们将一个逻辑算子（例如作用于第一列的 $\bar{Z}_1$）加入到[规范群](@entry_id:144761)中，它会与原有的一个[规范自由度](@entry_id:160491)结合，导致[逻辑量子比特](@entry_id:142662)数从1降为0 [@problem_id:100938]。

这种基于图论和经典[重复码](@entry_id:267088)结构的构造思想可以推广。例如，我们可以在一个完全图 $K_N$ 上构建一个Bacon-Shor类型的码，其中每个顶点是一个[量子比特](@entry_id:137928)，每条边 $(i, j)$ 对应一对规范生成元 $X_i X_j$ 和 $Z_i Z_j$。通过分析该规范[群的中心](@entry_id:141952)化子，我们可以确定逻辑算子的结构和数量 [@problem_id:100811]。这种方法将我们从依赖于特定[有限域](@entry_id:142106)上的代数码，引向了更具组合和拓扑风格的量子码构造，为设计具有特定容错特性的量子码开辟了新的途径。