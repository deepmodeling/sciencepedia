## 引言
在泛函分析中，一项核心任务是理解[巴拿赫空间](@entry_id:143833)上的[有界线性算子](@entry_id:180446)。除了算子本身，其与标量乘法的相互作用也至关重要。这引出了一个基本问题：对于一个给定的算子 $T$ 和一个复数 $\lambda$，算子 $\lambda I - T$ 在什么条件下是可逆的？这个问题是[谱理论](@entry_id:275351)的入口，它引导我们定义了现代分析中两个极其重要的概念：豫解集与豫解算子。

本文旨在系统地阐述这两个概念及其在理论和应用中的深刻意义。文章被构造成一个从基础到应用的完整学习路径。
- 在“**原理与机制**”一章中，我们将奠定理论基础，精确定义豫解集、谱和豫解算子，并深入探讨它们的基本代数与拓扑性质，例如第一豫解恒等式和豫[解集](@entry_id:154326)的开性。
- 接着，在“**应用与跨学科联系**”一章中，我们将展示这些抽象概念的强大威力，通过一系列范例，探索它们如何应用于从有限维矩阵到数学物理中的[微分与积分](@entry_id:141565)算子等广泛问题。
- 最后，“**动手实践**”部分将提供具体的计算问题，旨在将理论知识转化为解决实际问题的能力，从而巩固学习成果。

通过这趟旅程，读者将认识到豫解算子不仅是一个计算工具，更是一种统一的语言，用以揭示各类[线性系统](@entry_id:147850)内在的结构与行为。

## 原理与机制

在研究巴拿赫空间上的[有界线性算子](@entry_id:180446)时，我们不仅关心算子本身，还非常关心它与标量乘法算子的关系。一个核心问题是：对于一个给定的算子 $T$ 和一个复数 $\lambda$，算子 $\lambda I - T$ 是否可逆？这个看似简单的问题是谱理论的入口，它引导我们定义[算子理论](@entry_id:139990)中最重要的两个概念：豫[解集](@entry_id:154326)和谱。本章将系统地阐述这些概念的原理及其深刻的内涵。

### 豫[解集](@entry_id:154326)与豫解算子

设 $X$ 是一个复巴拿赫空间，$T$ 是作用于 $X$ 上的一个[有界线性算子](@entry_id:180446)。

**豫[解集](@entry_id:154326) (Resolvent Set)** $T$ 的豫解集，记为 $\rho(T)$，是所有使得算子 $(\lambda I - T)$ 存在有界逆算子的复数 $\lambda \in \mathbb{C}$ 的集合。换言之，$\lambda \in \rho(T)$ 当且仅当 $(\lambda I - T)$ 是一个从 $X$ 到 $X$ 的[双射](@entry_id:138092)，并且其逆算子是有界的。

**谱 (Spectrum)** $T$ 的谱，记为 $\sigma(T)$，是豫[解集](@entry_id:154326)在复平面 $\mathbb{C}$ 中的补集，即 $\sigma(T) = \mathbb{C} \setminus \rho(T)$。谱中的元素被称为谱值。

**豫解算子 (Resolvent Operator)** 对于任意 $\lambda \in \rho(T)$，我们将有界的逆算子 $(\lambda I - T)^{-1}$ 称为 $T$ 在 $\lambda$ 处的豫解算子，并记为 $R_{\lambda}(T)$。因此，对于 $\lambda \in \rho(T)$，我们有：
$$
R_{\lambda}(T) = (\lambda I - T)^{-1}
$$
并且它满足：
$$
R_{\lambda}(T)(\lambda I - T) = (\lambda I - T)R_{\lambda}(T) = I
$$
其中 $I$ 是[恒等算子](@entry_id:204623)。

为了理解这些抽象的定义，我们从一些具体的例子开始。

#### 有限维空间的情形

在有限维空间中，谱的概念与我们在线性代数中熟悉的[特征值](@entry_id:154894)概念紧密相关。考虑一个作用在有限维[复希尔伯特空间](@entry_id:185216) $\mathbb{C}^n$ 上的线性算子 $T$。根据线性代数的知识，一个方阵可逆当且仅当其[行列式](@entry_id:142978)不为零。因此，算子 $(\lambda I - T)$ 可逆等价于矩阵 $(\lambda I - T)$ 的[行列式](@entry_id:142978)非零。这意味着豫[解集](@entry_id:154326) $\rho(T)$ 是所有使得[特征多项式](@entry_id:150909) $\det(\lambda I - T)$ 不为零的 $\lambda$ 的集合。相应地，谱 $\sigma(T)$ 恰好是所有使得 $\det(\lambda I - T) = 0$ 的 $\lambda$ 的集合，这正是算子 $T$ 的所有[特征值](@entry_id:154894)的集合。

例如，让我们考虑在 $\mathbb{C}^2$ 上由矩阵
$$
T = \begin{pmatrix} 1  4 \\ 1  1 \end{pmatrix}
$$
表示的算子 [@problem_id:1899236]。要确定其豫[解集](@entry_id:154326)，我们首先计算 $\lambda I - T$ 的[行列式](@entry_id:142978)：
$$
\det(\lambda I - T) = \det\begin{pmatrix} \lambda-1  -4 \\ -1  \lambda-1 \end{pmatrix} = (\lambda-1)^2 - 4
$$
令[行列式](@entry_id:142978)为零，我们得到 $(\lambda-1)^2 = 4$，解得 $\lambda - 1 = \pm 2$，即 $\lambda = 3$ 或 $\lambda = -1$。这两个值构成了算子 $T$ 的谱 $\sigma(T) = \{-1, 3\}$。因此，豫[解集](@entry_id:154326)是复平面上除去这两个点的所有点，即 $\rho(T) = \mathbb{C} \setminus \{-1, 3\}$。

#### 一个简单的无限维例子

现在考虑一个更简单但作用于任意非平凡[巴拿赫空间](@entry_id:143833) $X$ 上的算子——零算子 $T=0$，它将每个向量映射到[零向量](@entry_id:156189) [@problem_id:1899196]。对于任意 $\lambda \in \mathbb{C}$，我们考察算子 $\lambda I - T = \lambda I$。如果 $\lambda = 0$，则该算子为零算子，它显然不是可逆的（因为它不是单射）。因此，$0 \in \sigma(0)$。如果 $\lambda \neq 0$，则算子 $\lambda I$ 是一个非零标量乘以[恒等算子](@entry_id:204623)，它的逆算子是 $(\lambda I)^{-1} = \frac{1}{\lambda}I$。这个逆算子显然是有界的，其范数为 $|\frac{1}{\lambda}|$。因此，所有非零复数都属于零算子的豫解集。

总结起来，对于零算子 $T=0$：
- 谱为 $\sigma(0) = \{0\}$。
- 豫解集为 $\rho(0) = \mathbb{C} \setminus \{0\}$。
- 对于任意 $\lambda \in \rho(0)$，豫解算子为 $R_{\lambda}(0) = \frac{1}{\lambda}I$。

这个例子虽然简单，但清晰地展示了对于无限维空间中的算子，谱可以是一个非常简单的集合。

### 豫解算子的基本代数性质

豫解算子有一些非常重要的代数性质，这些性质是[谱理论](@entry_id:275351)的基石。

#### 与原算子的交换性

一个直接但至关重要的观察是，豫解算子 $R_{\lambda}(T)$ 与原算子 $T$ 是可交换的。这一点可以从定义直接导出。我们有：
$$
(\lambda I - T)T = \lambda T - T^2 = T(\lambda I - T)
$$
用 $R_{\lambda}(T)$ 从左边和右边同时乘以这个等式，我们得到：
$$
R_{\lambda}(T)(\lambda I - T)T R_{\lambda}(T) = R_{\lambda}(T)T(\lambda I - T)R_{\lambda}(T)
$$
由于 $R_{\lambda}(T)(\lambda I - T) = I$ 和 $(\lambda I - T)R_{\lambda}(T) = I$，上式简化为：
$$
T R_{\lambda}(T) = R_{\lambda}(T) T
$$
这个交换性在许多计算中都至关重要。例如，利用这个性质，我们可以推导出豫解算子与 $T$ 的多项式之间的关系。从 $R_{\lambda}(T)(\lambda I - T) = I$ 出发，我们有 $\lambda R_{\lambda}(T) - R_{\lambda}(T)T = I$。由于交换性，这等价于 $\lambda R_{\lambda}(T) - T R_{\lambda}(T) = I$，整理后得到一个非常有用的关系：
$$
T R_{\lambda}(T) = \lambda R_{\lambda}(T) - I
$$
这个关系式允许我们将 $T$ 作用于豫解算子的表达式用豫解算子本身来表示 [@problem_id:1899192]。

#### 第一豫解恒等式

豫解算子最重要的性质之一是**第一豫解恒等式**（或称[希尔伯特恒等式](@entry_id:266640)）。该恒等式描述了在豫解集中两个不同点处的豫解算子之间的关系。对于 $\rho(T)$ 中任意两个不同的点 $\lambda$ 和 $\mu$，我们有：
$$
R_{\lambda}(T) - R_{\mu}(T) = (\mu - \lambda) R_{\lambda}(T) R_{\mu}(T)
$$
这个恒等式的推导是一个优雅的代数技巧 [@problem_id:1890653]。我们从一个简单的观察开始：
$$
\lambda I - T = (\mu I - T) + (\lambda - \mu)I
$$
用 $R_{\lambda}(T)$ 从左边乘以这个等式，得到：
$$
I = R_{\lambda}(T)(\mu I - T) + (\lambda - \mu)R_{\lambda}(T)I
$$
现在，用 $R_{\mu}(T)$ 从右边乘以等式：
$$
R_{\mu}(T) = R_{\lambda}(T)(\mu I - T)R_{\mu}(T) + (\lambda - \mu)R_{\lambda}(T)R_{\mu}(T)
$$
由于 $(\mu I - T)R_{\mu}(T) = I$，上式简化为：
$$
R_{\mu}(T) = R_{\lambda}(T) + (\lambda - \mu)R_{\lambda}(T)R_{\mu}(T)
$$
整理后即得第一豫解恒等式。

这个恒等式有几个深刻的推论。首先，将等式两边交换 $\lambda$ 和 $\mu$ 的位置，我们得到 $R_{\mu}(T) - R_{\lambda}(T) = (\lambda - \mu) R_{\mu}(T) R_{\lambda}(T)$。与原式比较，我们发现 $R_{\lambda}(T) R_{\mu}(T) = R_{\mu}(T) R_{\lambda}(T)$。这意味着任意两点的豫解算子是相互交换的。

其次，这个恒等式表明 $R_{\lambda}(T)$ 作为 $\lambda$ 的函数，在 $\rho(T)$ 上是（算子范数意义下的）解析的。如果我们让 $\mu \to \lambda$，等式可以写成：
$$
\frac{R_{\mu}(T) - R_{\lambda}(T)}{\mu - \lambda} = -R_{\lambda}(T)R_{\mu}(T)
$$
取极限 $\mu \to \lambda$，我们得到 $R_{\lambda}(T)$ 对 $\lambda$ 的导数：
$$
\frac{d}{d\lambda} R_{\lambda}(T) = -R_{\lambda}(T)^2
$$

### 豫[解集](@entry_id:154326)的拓扑性质与豫解范数

#### 豫[解集](@entry_id:154326)是开集

[谱理论](@entry_id:275351)中的一个基本结果是：**任何[有界线性算子](@entry_id:180446) $T$ 的豫解集 $\rho(T)$ 都是复平面 $\mathbb{C}$ 上的一个开集。** 这反过来意味着谱 $\sigma(T)$ 是一个[闭集](@entry_id:136446)。

这个结论的证明依赖于**[诺伊曼级数](@entry_id:191685) (Neumann series)** 的思想。假设 $\lambda_0 \in \rho(T)$，我们希望证明在 $\lambda_0$ 附近的一个小邻域内的所有点也都属于 $\rho(T)$。对于一个靠近 $\lambda_0$ 的复数 $\lambda$，我们可以写出：
$$
\lambda I - T = (\lambda_0 I - T) + (\lambda - \lambda_0)I = (\lambda_0 I - T) \left[ I - (\lambda_0 - \lambda)(\lambda_0 I - T)^{-1} \right]
$$
令 $S = (\lambda_0 - \lambda)R_{\lambda_0}(T)$。如果算子 $I - S$ 可逆，那么 $\lambda I - T$ 作为两个可逆算子的乘积，其本身也是可逆的。根据[诺伊曼级数](@entry_id:191685)的收敛性，只要 $S$ 的算子范数小于 1，即 $\|S\|  1$，算子 $I-S$ 就是可逆的。这个条件是：
$$
\|(\lambda_0 - \lambda)R_{\lambda_0}(T)\| = |\lambda - \lambda_0| \|R_{\lambda_0}(T)\|  1
$$
这等价于：
$$
|\lambda - \lambda_0|  \frac{1}{\|R_{\lambda_0}(T)\|}
$$
这表明，以 $\lambda_0$ 为中心，半径为 $r = 1/\|R_{\lambda_0}(T)\|$ 的开圆盘内的所有 $\lambda$ 都属于 $\rho(T)$。因此，$\rho(T)$ 是一个开集。

这个证明不仅是理论上的，它还为我们提供了一个具体的方法来估计豫解集中区域的大小。考虑在[巴拿赫空间](@entry_id:143833) $C([0, 1])$ (即区间 $[0, 1]$ 上的连续[复值函数](@entry_id:196054)空间，配备[上确界范数](@entry_id:145717)) 上的乘法算子 $(Tf)(x) = xf(x)$ [@problem_id:1899197]。这个[算子的谱](@entry_id:272027)是函数 $x$ 在 $[0, 1]$ 上的值域，即 $\sigma(T) = [0, 1]$。对于任何 $\lambda \notin [0, 1]$，豫解算子为 $(R_\lambda(T)g)(x) = \frac{g(x)}{\lambda-x}$。其范数为：
$$
\|R_\lambda(T)\| = \sup_{\|g\|_\infty = 1} \left\| \frac{g(x)}{\lambda-x} \right\|_\infty = \sup_{x \in [0,1]} \frac{1}{|\lambda-x|} = \frac{1}{\min_{x \in [0,1]} |\lambda-x|} = \frac{1}{\text{dist}(\lambda, \sigma(T))}
$$
根据上述理论，对于给定的 $\lambda_0 \in \rho(T)$，我们可以保证以 $\lambda_0$ 为中心，半径 $r_{\text{max}} = 1/\|R_{\lambda_0}(T)\| = \text{dist}(\lambda_0, \sigma(T))$ 的开圆盘完全包含在 $\rho(T)$ 中。例如，如果取 $\lambda_0 = 2+2i$，那么它到谱 $[0,1]$ 的距离是它到点 $1$ 的距离，即 $|(2+2i) - 1| = |1+2i| = \sqrt{5}$。因此，我们确信开圆盘 $D(2+2i, \sqrt{5})$ 内的所有复数都属于该算子的豫[解集](@entry_id:154326)。

#### 豫解范数的行为

豫解算子的范数 $\|R_\lambda(T)\|$ 包含了关于谱的重要信息。

**大 $\lambda$ 的[渐近行为](@entry_id:160836):** 当 $|\lambda|$ 趋于无穷大时，会发生什么？直观上，当 $\lambda$ 非常大时，算子 $\lambda I - T$ 由 $\lambda I$ 主导，因此它的行为应该类似于 $\lambda I$。我们可以通过代数变形来精确描述这一点 [@problem_id:1899213]。对于 $|\lambda|  \|T\|$ 的情况，我们有 $\|T/\lambda\| = \|T\|/|\lambda|  1$。此时，我们可以写出：
$$
R_\lambda(T) = (\lambda I - T)^{-1} = \left(\lambda(I - \lambda^{-1}T)\right)^{-1} = \frac{1}{\lambda}(I - \lambda^{-1}T)^{-1}
$$
由于 $\|\lambda^{-1}T\|  1$，我们可以使用[诺伊曼级数](@entry_id:191685)展开：
$$
(I - \lambda^{-1}T)^{-1} = \sum_{n=0}^{\infty} (\lambda^{-1}T)^n = I + \lambda^{-1}T + \lambda^{-2}T^2 + \dots
$$
因此，
$$
R_\lambda(T) = \frac{1}{\lambda} (I + \lambda^{-1}T + \dots)
$$
取范数，我们看到当 $|\lambda| \to \infty$ 时，级数部分趋向于[恒等算子](@entry_id:204623) $I$ (其范数为1)，所以 $\|R_\lambda(T)\|$ 的行为主要由因子 $1/\lambda$ 决定。更精确地，
$$
\lim_{|\lambda| \to \infty} \|R_\lambda(T)\| = 0
$$
并且其衰减速度与 $1/|\lambda|$ 成正比。这个性质，结合豫解算子的[解析性](@entry_id:140716)，可以用来证明任何[有界算子](@entry_id:264879)的谱都是非空的[紧集](@entry_id:147575)。

**与谱的距离关系:** 豫解范数与点 $\lambda$ 到谱 $\sigma(T)$ 的距离密切相关。我们有以下[一般性](@entry_id:161765)的不等式：
$$
\|R_\lambda(T)\| \ge \frac{1}{\text{dist}(\lambda, \sigma(T))}
$$
其中 $\text{dist}(\lambda, \sigma(T)) = \inf_{\mu \in \sigma(T)} |\lambda - \mu|$。这个结果源于[谱半径](@entry_id:138984)公式。对于**[正规算子](@entry_id:270585)** (即满足 $T^*T = TT^*$ 的算子，例如自伴算子、[酉算子](@entry_id:151194)和[有限维空间](@entry_id:151571)中的[正规矩阵](@entry_id:185943))，这个不等式可以加强为等式：
$$
\|R_\lambda(T)\| = \frac{1}{\text{dist}(\lambda, \sigma(T))} \quad (\text{当 } T \text{ 是正规算子时})
$$
这个等式非常强大，它将一个分析量（算子范数）与一个几何量（到谱的距离）直接联系起来。

让我们通过一个[正规算子](@entry_id:270585)的例子来验证这个等式。考虑在 $\mathbb{C}^4$ 上由[对角矩阵](@entry_id:637782) $T = \text{diag}(1, 2i, -2i, 4)$ 定义的算子 [@problem_id:1899193]。这是一个[正规算子](@entry_id:270585)，其谱就是对角线上的元素集合 $\sigma(T) = \{1, 2i, -2i, 4\}$。对于任意 $\lambda \in \rho(T)$，豫解算子也是对角矩阵 $R_\lambda(T) = \text{diag}(\frac{1}{\lambda-1}, \frac{1}{\lambda-2i}, \frac{1}{\lambda+2i}, \frac{1}{\lambda-4})$。[对角算子](@entry_id:262993)的范数是其对角元素模长的最大值。因此：
$$
\|R_\lambda(T)\| = \max\left\{ \frac{1}{|\lambda-1|}, \frac{1}{|\lambda-2i|}, \frac{1}{|\lambda+2i|}, \frac{1}{|\lambda-4|} \right\} = \frac{1}{\min\{|\lambda-1|, |\lambda-2i|, |\lambda+2i|, |\lambda-4|\}} = \frac{1}{\text{dist}(\lambda, \sigma(T))}
$$
例如，对于 $\lambda = 2.5$，它到谱中各点的距离分别为 $|2.5-1|=1.5$, $|2.5-4|=1.5$, $|2.5 \pm 2i|=\sqrt{(2.5)^2+2^2}=\sqrt{10.25}$。最短距离是 $1.5 = 3/2$。因此，$\|R_{2.5}(T)\| = 1 / (3/2) = 2/3$。

这个等式对于无限维[正规算子](@entry_id:270585)同样成立。例如，对于 $L^2([0,1])$ 上的乘法算子 $(Tf)(x) = g(x)f(x)$，它是一个[正规算子](@entry_id:270585)，其谱是函数 $g(x)$ 的值域的[闭包](@entry_id:148169)。其豫解范数同样满足 $\|R_\lambda(T)\| = 1/\text{dist}(\lambda, \sigma(T))$ [@problem_id:1872415]。

### 特殊[算子的谱](@entry_id:272027)

豫[解集](@entry_id:154326)和谱的结构与算子本身的性质密切相关。对于某些特殊类型的算子，我们可以对其谱的性质做出更强的断言。

#### 自伴算子

如果一个希尔伯特空间上的[有界线性算子](@entry_id:180446) $T$ 满足 $T = T^*$（其中 $T^*$ 是 $T$ 的伴随算子），则称 $T$ 是**[自伴算子](@entry_id:152188)**。自伴算子在量子力学中扮演核心角色，代表可观测的物理量。一个基本结果是：**[自伴算子](@entry_id:152188)的谱必定是实数集的[子集](@entry_id:261956)**，即 $\sigma(T) \subset \mathbb{R}$。

我们可以利用豫解算子的范数来证明这一点 [@problem_id:1899210]。我们的目标是证明任何非实数的复数 $\lambda = a+ib$（其中 $b \neq 0$）都属于豫解集 $\rho(T)$。考虑算子 $\lambda I - T$。对于任意非零向量 $x \in H$，我们计算[内积](@entry_id:158127) $\langle (\lambda I - T)x, x \rangle$：
$$
\langle (\lambda I - T)x, x \rangle = \langle \lambda x - Tx, x \rangle = \lambda \langle x, x \rangle - \langle Tx, x \rangle = (a+ib)\|x\|^2 - \langle Tx, x \rangle
$$
由于 $T$ 是自伴的，$\langle Tx, x \rangle$ 是一个实数。因此，上述[内积](@entry_id:158127)的虚部为：
$$
\text{Im}\langle (\lambda I - T)x, x \rangle = b\|x\|^2
$$
另一方面，根据柯西-施瓦茨不等式，我们有 $|\text{Im}\langle (\lambda I - T)x, x \rangle| \le |\langle (\lambda I - T)x, x \rangle| \le \|(\lambda I - T)x\| \|x\|$。结合两式，得到：
$$
|b|\|x\|^2 \le \|(\lambda I - T)x\| \|x\|
$$
对于 $x \neq 0$，两边消去 $\|x\|$，我们获得一个关键的下界：
$$
\|(\lambda I - T)x\| \ge |b|\|x\|
$$
这个不等式表明 $\lambda I - T$ 是一个[单射](@entry_id:183792)，并且在其值域上存在逆，且逆的范数有界 $\|R_\lambda(T)y\| \le \frac{1}{|b|}\|y\|$。通过进一步的论证可以证明其值域是整个空间，从而 $\lambda I - T$ 是可逆的。这不仅证明了非实数 $\lambda$ 属于豫[解集](@entry_id:154326)，还给出了豫解范数的一个上界：
$$
\|R_\lambda(T)\| \le \frac{1}{|b|} = \frac{1}{|\text{Im}(\lambda)|}
$$

#### 可逆算子与[谱映射定理](@entry_id:264489)

如果算子 $T$ 是可逆的（即 $0 \notin \sigma(T)$），那么它的逆算子 $T^{-1}$ 的谱与 $T$ 的谱之间有什么关系呢？**[谱映射定理](@entry_id:264489)**的一个简单形式回答了这个问题。对于一个可逆算子 $T$，我们有：
$$
\sigma(T^{-1}) = \left\{ \frac{1}{\lambda} : \lambda \in \sigma(T) \right\}
$$
这个结论的证明基于一个简单的代数关系。对于任意非零复数 $\mu$，我们考察算子 $T^{-1} - \mu I$ 的[可逆性](@entry_id:143146)。
$$
T^{-1} - \mu I = T^{-1}(I - \mu T) = -\mu T^{-1} (T - \mu^{-1} I)
$$
由于 $-\mu T^{-1}$ 是可逆的，算子 $T^{-1} - \mu I$ 的可逆性完[全等](@entry_id:273198)价于算子 $T - \mu^{-1} I$ 的[可逆性](@entry_id:143146)。换言之，$\mu \in \rho(T^{-1})$ 当且仅当 $\mu^{-1} \in \rho(T)$。取其补集，我们得到 $\mu \in \sigma(T^{-1})$ 当且仅当 $\mu^{-1} \in \sigma(T)$。

让我们看一个在希尔伯特空间 $\ell^2(\mathbb{N})$ 上的例子 [@problem_id:1899249]。考虑一个[对角算子](@entry_id:262993) $T$ 的定义如下：
$$
T(x_1, x_2, \dots) = \left(\frac{2n+3}{2n+1} x_n\right)_{n=1}^\infty
$$
这是一个[对角算子](@entry_id:262993)，其对角[线元](@entry_id:196833)素为 $a_n = \frac{2n+3}{2n+1}$。这些元素是 $T$ 的[特征值](@entry_id:154894)，因此它们都属于谱。注意到当 $n \to \infty$ 时，$a_n = 1 + \frac{2}{2n+1} \to 1$。由于谱是[闭集](@entry_id:136446)，极限点 $1$ 也必须在谱中。因此，$\sigma(T) = \{ \frac{2n+3}{2n+1} : n \in \mathbb{N} \} \cup \{1\}$。由于所有 $a_n \ge 5/3  0$，所以 $0 \notin \sigma(T)$，算子 $T$ 可逆。根据[谱映射定理](@entry_id:264489)，其逆[算子的谱](@entry_id:272027)为：
$$
\sigma(T^{-1}) = \left\{ \frac{1}{\lambda} : \lambda \in \sigma(T) \right\} = \left\{ \frac{2n+1}{2n+3} : n \in \mathbb{N} \right\} \cup \{1\}
$$
这个例子很好地说明了在无限维空间中，谱不仅包含[特征值](@entry_id:154894)，还可能包含[特征值](@entry_id:154894)的[聚点](@entry_id:177089)。

总结来说，豫[解集](@entry_id:154326)和豫解算子是[分析算子](@entry_id:746429)性质的强大工具。通过研究豫解算子的代数、拓扑和分析性质，我们能够揭示[算子谱](@entry_id:276315)的深刻结构，并将其与算子的代数属性（如自伴性、正规性）联系起来。这些原理构成了现代泛函分析和[算子理论](@entry_id:139990)的基石。