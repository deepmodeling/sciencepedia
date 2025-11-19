## 引言
在[现代机器学习](@entry_id:637169)中，许多任务的本质可以归结为在一个复杂的[函数空间](@entry_id:143478)中寻找一个最优函数。无论是拟[合数](@entry_id:263553)据点、分类样本，还是发现数据中的低维结构，我们都需要一个既有丰富[表达能力](@entry_id:149863)又具备良好数学性质的函数框架。然而，传统的[函数空间](@entry_id:143478)（如[L²空间](@entry_id:272636)）在处理单个数据点的函数值时会遇到理论上的困难。为了解决这一根本问题，并为[非线性](@entry_id:637147)数据分析提供坚实的理论基础，**[再生核](@entry_id:262515)[希尔伯特空间](@entry_id:261193)（Reproducing Kernel Hilbert Space, RKHS）**应运而生。

本文旨在系统地揭开RKHS的神秘面纱，为读者构建一个从理论到实践的完整知识体系。我们将带领您深入探索这一优雅而强大的数学工具，理解它为何能成为支撑[现代机器学习](@entry_id:637169)诸多算法的理论支柱。

-   在 **原理与机制** 章节中，我们将深入RKHS的数学核心，从其基本定义和关键的“再生性质”出发，揭示核函数与[函数空间几何](@entry_id:202345)结构之间的深刻联系。您将理解“[表示定理](@entry_id:637872)”的革命性意义，以及它如何将无限维的函数学习问题巧妙地转化为有限维的计算问题。
-   在 **应用与跨学科联系** 章节中，我们将视野从理论转向实践，展示RKHS如何在[支持向量机](@entry_id:172128)（SVM）、[核主成分分析](@entry_id:634172)（KPCA）等经典算法中大放异彩。您还将看到RKHS如何通过定制化的[核函数](@entry_id:145324)，优雅地处理序列、集合乃至图等复杂数据结构，并一窥其在统计学、控制理论等领域的跨学科影响力。
-   在 **动手实践** 章节中，我们将通过一系列精心设计的练习，将理论知识转化为可操作的技能。您将亲手实现[核方法](@entry_id:276706)的核心计算，体验从选择核函数到应用它的完整流程。

通过这三个章节的层层递进，您将不仅掌握RKHS的“是什么”和“为什么”，更能理解“怎么用”，从而在面对复杂的学习任务时，能够更加自信地运用[核方法](@entry_id:276706)这一强大工具。让我们一同开启这段探索之旅，领略函数空间之美。

## 原理与机制

在机器学习领域，我们经常处理由函数构成的空间。在这些空间中，希尔伯特空间（Hilbert space）因其完备的[内积](@entry_id:158127)结构而备受青睐，它允许我们严谨地定义角度、距离和正交性等几何概念。然而，在标准的[函数空间](@entry_id:143478)（如 $L^2$ 空间）中，一些看似基本的操作实际上可能非常复杂，甚至没有良好定义。例如，对于 $L^2$ 空间中的一个函数 $f$，其在单个点 $x$ 上的取值 $f(x)$ 是没有意义的，因为空间中的元素是函数的等价类，它们在零测集上的差异被忽略了。

**[再生核](@entry_id:262515)希尔伯特空间（Reproducing Kernel Hilbert Space, RKHS）**应运而生，它是一类特殊的[希尔伯特空间](@entry_id:261193)，旨在克服这一限制。其核心特征是，空间中的所有函数都表现出良好的“行为”，使得点态求值（pointwise evaluation）不仅有意义，而且是一个“容易”的运算。这种良好的性质为在复杂函数空间中进行学习和优化提供了坚实的理论基础和强大的计算工具。

### [再生核](@entry_id:262515)希尔伯特空间的本质

一个定义在集合 $\mathcal{X}$ 上的函数构成的希尔伯特空间 $\mathcal{H}$ 被称为[再生核](@entry_id:262515)希尔伯特空间，如果对于任意 $x \in \mathcal{X}$，**点态求值泛函**（point evaluation functional）$E_x: \mathcal{H} \to \mathbb{C}$（或 $\mathbb{R}$）都是连续的。该泛函的定义为 $E_x(f) = f(x)$。

“连续”在这里是一个关键的技术性要求。在[赋范向量空间](@entry_id:274725)中，一个线性泛函是连续的，当且仅当它是**有界的**。这意味着对于每个 $x$，存在一个常数 $C_x \ge 0$，使得对于所有 $f \in \mathcal{H}$，不等式 $|f(x)| \le C_x \|f\|_{\mathcal{H}}$ 成立。这表明，如果一个函数在空间中的范数很小，那么它在任何一点的取值幅度也必然受到限制。

根据[泛函分析](@entry_id:146220)中著名的**[里斯表示定理](@entry_id:140012)**（Riesz Representation Theorem），对于希尔伯特空间 $\mathcal{H}$ 中的任意一个[连续线性泛函](@entry_id:262913)，都存在空间中一个唯一的元素，可以通过[内积](@entry_id:158127)来“表示”该泛函。将此定理应用于点态求值泛函 $E_x$，我们得到一个深刻的结论：对于每一个 $x \in \mathcal{X}$，都存在一个唯一的函数，我们记为 $K_x$，它属于 $\mathcal{H}$ 并且满足：
$$
f(x) = E_x(f) = \langle f, K_x \rangle_{\mathcal{H}} \quad \forall f \in \mathcal{H}
$$
这个等式被称为 **再生性质**（reproducing property），因为它通过与函数 $K_x$ 的[内积](@entry_id:158127)“再生”了函数 $f$ 在点 $x$ 的值。

函数 $K_x$ 本身依赖于点 $x$。我们可以定义一个二元函数 $K: \mathcal{X} \times \mathcal{X} \to \mathbb{C}$，称为**[再生核](@entry_id:262515)**（reproducing kernel），其定义为 $K(x, y) = K_y(x)$。将 $f = K_y$ 代入再生性质的表达式中，我们得到：
$$
K_y(x) = \langle K_y, K_x \rangle_{\mathcal{H}}
$$
结合[再生核](@entry_id:262515)的定义，我们有 $\langle K_y, K_x \rangle_{\mathcal{H}} = K(x, y)$。通过[内积](@entry_id:158127)的[共轭对称性](@entry_id:144131)，我们还得到 $K(y, x) = \overline{K(x, y)}$，这表明[核函数](@entry_id:145324)是埃尔米特对称的（对于实值函数空间，则是对称的）。

再生性质是RKHS的基石，它直接带来了一系列重要的推论。通过应用[内积](@entry_id:158127)的**柯西-[施瓦茨不等式](@entry_id:202153)**（Cauchy-Schwarz inequality），我们可以立即得到函数值的一个[上界](@entry_id:274738)：
$$
|f(x)| = |\langle f, K_x \rangle_{\mathcal{H}}| \le \|f\|_{\mathcal{H}} \|K_x\|_{\mathcal{H}}
$$
我们可以进一步计算 $K_x$ 的范数。利用再生性质，我们有：
$$
\|K_x\|_{\mathcal{H}}^2 = \langle K_x, K_x \rangle_{\mathcal{H}} = K_x(x) = K(x, x)
$$
因此，我们得到了一个更具体、更有用的不等式 [@problem_id:2321084]：
$$
|f(x)| \le \|f\|_{\mathcal{H}} \sqrt{K(x, x)}
$$
这个不等式优美地揭示了函数在某点的可能取值范围是如何被其自身的全局“能量”（由范数 $\|f\|_{\mathcal{H}}$ 度量）以及[核函数](@entry_id:145324)在该点对角线上的值 $K(x, x)$ 所共同约束的。$K(x,x)$ 的大小可以被看作是特征空间中点 $x$ 映射的“长度”的平方，它反映了函数在该点附近变化的“自由度”。

这个界限的另一个重要推论是，RKHS中的[范数收敛](@entry_id:261322)蕴含着点态收敛。考虑一个在 $\mathcal{H}$ 中按[范数收敛](@entry_id:261322)到 $f$ 的函数序列 $\{f_n\}_{n=1}^{\infty}$，即 $\lim_{n \to \infty} \|f_n - f\|_{\mathcal{H}} = 0$。对于任意固定的点 $x \in \mathcal{X}$，我们有 [@problem_id:1887220]：
$$
|f_n(x) - f(x)| = |(f_n - f)(x)| \le \|f_n - f\|_{\mathcal{H}} \sqrt{K(x, x)}
$$
由于右侧当 $n \to \infty$ 时趋于零，左侧也必然趋于零。这意味着 $\lim_{n \to \infty} f_n(x) = f(x)$。因此，在RKHS中，[函数的收敛](@entry_id:152305)是一种非常“稳定”和“良好”的行为，这与某些函数空间（如$L^p$空间）中可能出现的奇异收敛现象形成鲜明对比。

### 构建和理解RKHS

尽管RKHS的抽象定义非常优雅，但我们如何具体地构建和感知它们呢？存在几种互补的视角。

#### 从特征映射出发

对于机器学习从业者而言，最直观的构建方式始于一个**特征映射**（feature map）$\phi: \mathcal{X} \to \mathcal{F}$。这个映射将输入空间 $\mathcal{X}$ 中的数据点转换到一个（可能维度更高甚至无限维的）**[特征空间](@entry_id:638014)** $\mathcal{F}$，该[特征空间](@entry_id:638014)是一个[希尔伯特空间](@entry_id:261193)。

我们可以通过特征空间中的[内积](@entry_id:158127)来定义[核函数](@entry_id:145324)：
$$
k(x, x') = \langle \phi(x), \phi(x') \rangle_{\mathcal{F}}
$$
这个[核函数](@entry_id:145324)所对应的RKHS $\mathcal{H}$，恰好是所有形如 $f(x) = \langle w, \phi(x) \rangle_{\mathcal{F}}$ 的函数的集合，其中 $w$ 是[特征空间](@entry_id:638014) $\mathcal{F}$ 中的一个向量。对于这样的函数，其RKHS范数被自然地定义为 $\|f\|_{\mathcal{H}} = \|w\|_{\mathcal{F}}$。

在这种构造下，再生性质的验证变得非常直接。代表求值点 $x$ 的函数 $K_x$ 正是 $k(x, \cdot) = \langle \phi(x), \phi(\cdot) \rangle_{\mathcal{F}}$，这对应于在特征空间中选择 $w = \phi(x)$。于是，对于任意 $f \in \mathcal{H}$（对应向量 $w$），其[内积](@entry_id:158127)为：
$$
\langle f, K_x \rangle_{\mathcal{H}} = \langle w, \phi(x) \rangle_{\mathcal{F}} = f(x)
$$
这完美地满足了再生性质。这个视角强化了“[核函数](@entry_id:145324)是[特征空间](@entry_id:638014)中[内积](@entry_id:158127)”或“核函数度量了样本相似度”的直观理解。例如，当特征映射是有限维的，如 $\phi: \mathbb{R} \to \mathbb{R}^d$，那么RKHS就是所有形式为 $f(x) = w^\top \phi(x)$ 的函数的集合，其范数为 $\|f\|_{\mathcal{H}} = \|w\|_2$ [@problem_id:3170349]。

#### 从[函数空间](@entry_id:143478)和[内积](@entry_id:158127)出发

另一种更深刻的视角是，从一个预先定义好的函数空间和[内积](@entry_id:158127)出发，然后去寻找它对应的[再生核](@entry_id:262515)。这种方法能让我们理解特定的范数（通常代表某种“能量”或“平滑度”）是如何与特定的[核函数](@entry_id:145324)关联起来的。

一个经典的例子是与**布朗运动**（Brownian motion）相关的RKHS [@problem_id:3047265]。考虑在区间 $[0, 1]$ 上所有满足 $f(0)=0$ 的[绝对连续函数](@entry_id:158609)构成的空间，并为其赋予[内积](@entry_id:158127)：
$$
\langle f, g \rangle_{\mathcal{H}} = \int_0^1 f'(t)g'(t)dt
$$
这个[内积](@entry_id:158127)定义的范数 $\|f\|_{\mathcal{H}}^2 = \int_0^1 (f'(t))^2 dt$ 衡量了函数的总“能量”或“变化剧烈程度”。我们可以证明，这个希尔伯特空间是一个RKHS，其[再生核](@entry_id:262515)恰好是 $k(x, t) = \min(x, t)$ [@problem_id:2161521]。

为了验证这一点，我们首先需要确认对于任意固定的 $x \in [0,1]$，函数 $K_x(t) = k(x, t) = \min(x, t)$ 属于我们的[函数空间](@entry_id:143478)。显然，$K_x(0) = \min(x, 0) = 0$。它的导数（在[分布](@entry_id:182848)意义下）是[阶梯函数](@entry_id:159192) $\frac{d}{dt}K_x(t) = \mathbf{1}_{[0, x]}(t)$，这是一个[平方可积函数](@entry_id:200316)。因此，$K_x \in \mathcal{H}$。

接下来，我们验证再生性质。对于任意一个空间中的函数 $f$，我们计算它与 $K_x$ 的[内积](@entry_id:158127)：
$$
\langle f, K_x \rangle_{\mathcal{H}} = \int_0^1 f'(t) \left( \frac{d}{dt}K_x(t) \right) dt = \int_0^1 f'(t) \mathbf{1}_{[0, x]}(t) dt = \int_0^x f'(t) dt
$$
根据微积分基本定理，由于 $f$ 是绝对连续的且 $f(0)=0$，上式等于 $f(x) - f(0) = f(x)$。再生性质得到完美验证。

这个例子深刻地揭示了，一个衡量函数“非平滑度”的[内积](@entry_id:158127)，与一个形式简单但意义深远的核函数（它同时也是标准[布朗运动的[协方差函](@entry_id:635074)数](@entry_id:265031)）之间存在着一一对应的关系。

### [核方法](@entry_id:276706)在机器学习中的威力

RKHS理论之所以在机器学习中如此重要，并不仅仅因为其数学上的优美，更在于它催生了以**[核技巧](@entry_id:144768)**（kernel trick）为核心的一系列强大算法。这些算法能够在高维甚至无限维的[特征空间](@entry_id:638014)中求解学习问题，而计算成本却只依赖于样本数量，与特征空间的维度无关。

#### [表示定理](@entry_id:637872)

[核方法](@entry_id:276706)的计算可行性几乎完全依赖于**[表示定理](@entry_id:637872)**（Representer Theorem）。该定理指出，对于一大类正则化[经验风险最小化](@entry_id:633880)问题，其最优解可以表示为在训练样本点上求值的[核函数](@entry_id:145324)的[线性组合](@entry_id:154743)。

具体来说，考虑如下形式的[优化问题](@entry_id:266749)：
$$
\min_{f \in \mathcal{H}} \mathcal{L}(f(x_1), \dots, f(x_N)) + \lambda \|f\|_{\mathcal{H}}^2
$$
其中，$\mathcal{L}$ 是一个任意的[损失函数](@entry_id:634569)，它度量模型预测与真实标签之间的差异；$\lambda \|f\|_{\mathcal{H}}^2$ 是一个正则化项，用于惩罚模型的“复杂度”（由RKHS范数定义）。[表示定理](@entry_id:637872)断言，这个问题的解 $f^*$ 必然具有如下形式：
$$
f^*(\cdot) = \sum_{i=1}^N \alpha_i k(x_i, \cdot)
$$
其中 $\alpha_i$ 是一些待求的系数。这个定理的直观解释是，任何与所有训练样本的[核函数](@entry_id:145324) $k(x_i, \cdot)$ 正交的函数分量 $f_{\perp}$，在所有训练点 $x_j$ 上的取值都为零（$f_{\perp}(x_j) = \langle f_{\perp}, K_{x_j} \rangle = 0$），因此它对[损失函数](@entry_id:634569) $\mathcal{L}$ 没有任何贡献，但却会增加总的范数。为了最小化[目标函数](@entry_id:267263)，这个正交分量必须为零。

[表示定理](@entry_id:637872)的意义是革命性的：它将一个在无限维函数空间中寻找最优函数 $f$ 的问题，转化为了一个在 $N$ 维空间中寻找最优系数向量 $\boldsymbol{\alpha} = (\alpha_1, \dots, \alpha_N)^\top$ 的问题，其中 $N$ 是训练样本的数量。

#### 应用：[核方法](@entry_id:276706)

[表示定理](@entry_id:637872)与[核技巧](@entry_id:144768)携手，将众多经典的线性算法提升到了[非线性](@entry_id:637147)的维度。

**[核岭回归](@entry_id:636718) (Kernel Ridge Regression, KRR)**
KRR旨在解决回归问题，其目标函数为：
$$
\min_{f \in \mathcal{H}} \sum_{i=1}^N (y_i - f(x_i))^2 + \lambda \|f\|_{\mathcal{H}}^2
$$
根据[表示定理](@entry_id:637872)，解的形式为 $f(x) = \sum_{j=1}^N \alpha_j k(x_j, x)$。将此形式代入[目标函数](@entry_id:267263)，我们得到一个关于 $\boldsymbol{\alpha}$ 的[优化问题](@entry_id:266749)。记 $\mathbf{y}$ 为标签向量，$\mathbf{K}$ 为 $N \times N$ 的**[格拉姆矩阵](@entry_id:203297)**（Gram matrix），其元素为 $K_{ij} = k(x_i, x_j)$。预测向量为 $\mathbf{K}\boldsymbol{\alpha}$，正则化项为 $\lambda \boldsymbol{\alpha}^\top \mathbf{K} \boldsymbol{\alpha}$。求解该二次规划问题，最终可以得到一个简单的[线性方程组的解](@entry_id:150455) [@problem_id:3170349] [@problem_id:3170321]：
$$
(\mathbf{K} + \lambda' I) \boldsymbol{\alpha} = \mathbf{y}
$$
（其中 $\lambda'$ 与原始的 $\lambda$ 成正比）。这是一个 $N \times N$ 的[线性系统](@entry_id:147850)，其计算复杂度只与样本数 $N$ 相关，与[特征空间](@entry_id:638014)的维度完全无关。当核函数是[非线性](@entry_id:637147)的（如高斯核），KRR能够学习到比任何[线性模型](@entry_id:178302)都复杂得多的函数关系，这在处理[非线性](@entry_id:637147)数据时显示出巨大优势 [@problem_id:3170349]。

**[支持向量机](@entry_id:172128) (Support Vector Machine, SVM)**
SVM是另一个受益于[核技巧](@entry_id:144768)的经典算法 [@problem_id:2433192]。其原始（primal）问题是在特征空间中寻找一个[最大间隔超平面](@entry_id:751772)来分离数据，由权重向量 $w$ 定义。如果[特征空间](@entry_id:638014)是无限维的，直接优化 $w$ 是不可能的。

然而，通过[拉格朗日对偶](@entry_id:638042)，SVM的**[对偶问题](@entry_id:177454)**（dual problem）的[目标函数](@entry_id:267263)可以被表述为仅依赖于[特征空间](@entry_id:638014)中样本映射的**[内积](@entry_id:158127)** $\langle \phi(x_i), \phi(x_j) \rangle$。此时，[核技巧](@entry_id:144768)便可大显身手：我们无需知道具体的映射 $\phi$，也无需在高维空间中进行计算，只需将[内积](@entry_id:158127)替换为核函数 $k(x_i, x_j)$ 即可。优化过程变成了求解一个只依赖于 $N$ 个[拉格朗日乘子](@entry_id:142696) $\alpha_i$ 的二次规划问题。最终的决策函数 $f(x) = \text{sign}(\sum_{i=1}^N \alpha_i y_i k(x_i, x) + b)$ 也完全通过核函数进行计算。这就是SVM能够使用如**[径向基函数](@entry_id:754004)（RBF）核**等对应于无限维特征空间的[核函数](@entry_id:145324)，而计算上依然完全可行的根本原因。

### 对[核方法](@entry_id:276706)的深入洞察

#### 最小范数插值

作为KRR的一个特例，当我们让正则化系数 $\lambda \to 0$ 时，问题就变成了寻找一个能够完美**插值**（interpolate）训练数据（即 $f(x_i) = y_i$ for all $i$）并且具有**最小RKHS范数**的函数 [@problem_id:1294233]。这可以被看作是寻找一个满足数据约束的“最平滑”或“最简单”的函数。

根据[表示定理](@entry_id:637872)，解的形式仍为 $f(\cdot) = \sum_{j=1}^N \alpha_j k(x_j, \cdot)$。插值条件 $f(x_i) = y_i$ 转化为[线性系统](@entry_id:147850) $\mathbf{K}\boldsymbol{\alpha} = \mathbf{y}$。如果[核函数](@entry_id:145324)是严格正定的，那么 $\mathbf{K}$ 可逆，我们得到 $\boldsymbol{\alpha} = \mathbf{K}^{-1}\mathbf{y}$。

这个最小范数[插值函数](@entry_id:262791)的平方范数有一个非常简洁的表达式 [@problem_id:1294233]：
$$
\|f\|_{\mathcal{H}}^2 = \boldsymbol{\alpha}^\top \mathbf{K} \boldsymbol{\alpha} = (\mathbf{K}^{-1}\mathbf{y})^\top \mathbf{K} (\mathbf{K}^{-1}\mathbf{y}) = \mathbf{y}^\top \mathbf{K}^{-1} \mathbf{y}
$$
这个结果在**[高斯过程](@entry_id:182192)**（Gaussian Processes）等领域中扮演着核心角色，它直接将数据点的值通过格拉姆矩阵的逆与模型的“复杂度”或“能量”联系起来。一个具体的计算实例可以参见 [@problem_id:2161521]，其中就应用了此原理来确定信号在某一点的值。

#### RKHS的几何学：不只是函数的集合

一个值得深思的问题是：一个函数集合是否唯一确定了它的RKHS结构？答案是否定的。一个RKHS不仅是一个函数的集合，它还被赋予了一个特定的[内积](@entry_id:158127)（即几何结构）。不同的核函数可以生成相同的函数集合，但赋予它们不同的范数，从而构成不同的RKHS [@problem_id:3170305]。

例如，在一个[有限集](@entry_id:145527)合 $\mathcal{X} = \{x_1, \dots, x_N\}$ 上，任何一个由严格正定[格拉姆矩阵](@entry_id:203297) $\mathbf{K}$ 生成的核，其对应的RKHS作为函数集合都是 $\mathbb{R}^N$（即所有定义在 $\mathcal{X}$ 上的函数）。然而，不同核的范数是不同的。对于一个由函数值向量 $\mathbf{f}$ 代表的函数，其平方范数为 $\|f\|_{\mathcal{H}_k}^2 = \mathbf{f}^\top \mathbf{K}^{-1} \mathbf{f}$。

这意味着，即使两个核（比如[单位矩阵](@entry_id:156724) $K_1=I$ 对应的核和另一个非[对角矩阵](@entry_id:637782) $K_2$ 对应的核）可以表示完全相同的函数类，当它们被用于KRR等[正则化方法](@entry_id:150559)时，由于正则化项 $\|f\|_{\mathcal{H}}^2$ 的形式不同，它们对“函数复杂度”的惩罚方式也不同，最终会导致不同的学习结果。因此，选择核函数，实际上是在为[函数空间](@entry_id:143478)选择一种特定的几何结构，这种结构反映了我们对解的[先验信念](@entry_id:264565)。

#### [偏差-方差权衡](@entry_id:138822)与[模型复杂度](@entry_id:145563)

[正则化参数](@entry_id:162917) $\lambda$ 在KRR中扮演着控制**偏差-方差权衡**（bias-variance tradeoff）的关键角色 [@problem_id:3170310]。KRR的预测值可以写成一个作用于观测值 $\mathbf{y}$ 的线性**[平滑算子](@entry_id:636528)**（smoother）：$\hat{\mathbf{y}} = \mathbf{K}(\mathbf{K} + \lambda' I)^{-1}\mathbf{y} = S_\lambda \mathbf{y}$。

模型的复杂度可以通过**[有效自由度](@entry_id:161063)**（effective degrees of freedom）来量化，定义为 $\text{df}(\lambda) = \text{tr}(S_\lambda)$。通过对格拉姆矩阵 $\mathbf{K}$ 进行[特征值分解](@entry_id:272091) $\mathbf{K} = U \text{diag}(\mu_i) U^\top$，我们得到：
$$
\text{df}(\lambda) = \sum_{i=1}^N \frac{\mu_i}{\mu_i + \lambda'}
$$
这个表达式清晰地展示了 $\lambda$ 的作用：
-   当 $\lambda \to 0$ 时，$\text{df}(\lambda) \to N$（假设 $\mathbf{K}$ 满秩）。模型具有高自由度，能紧密拟合训练数据，导致**低偏差**但可能**高[方差](@entry_id:200758)**。
-   当 $\lambda \to \infty$ 时，$\text{df}(\lambda) \to 0$。模型受到强烈约束（预测值趋向于零），自由度极低，导致**高偏差**但**低[方差](@entry_id:200758)**。

因此，选择合适的 $\lambda$ 就是在寻找一个最佳的[平衡点](@entry_id:272705)，以最小化总体的[预测误差](@entry_id:753692)。

#### 核的选择与[函数光滑性](@entry_id:161935)

不同的核函数隐含了关于待学习函数**光滑性**（smoothness）的不同先验假设。这个深刻的联系可以通过**[博赫纳定理](@entry_id:183496)**（Bochner's theorem）来揭示 [@problem_id:3170321]。对于一个平稳核（即 $k(x, x') = \psi(x-x')$），该定理指出[核函数](@entry_id:145324)是正定的，当且仅当 $\psi$ 是一个非负测度的[傅里叶变换](@entry_id:142120)。这个测度的密度函数 $S(\omega)$ 被称为**谱密度**（spectral density）。

RKHS的范数在傅里叶域中可以表示为：
$$
\|f\|_{\mathcal{H}}^2 \propto \int_{\mathbb{R}^d} \frac{|\hat{f}(\omega)|^2}{S(\omega)} d\omega
$$
其中 $\hat{f}(\omega)$ 是函数 $f$ 的[傅里叶变换](@entry_id:142120)。为了使范数有限，函数 $f$ 的[傅里叶变换](@entry_id:142120) $\hat{f}(\omega)$ 在高频区域的衰减速度必须比 $\sqrt{S(\omega)}$ 更快。这意味着谱密度 $S(\omega)$ 的衰减速度决定了RKHS中函数的光滑程度：
-   **高斯核 (Gaussian kernel)**: 其谱密度呈指数衰减（$S(\omega) \propto \exp(-\omega^2)$）。这要求 $\hat{f}(\omega)$ 必须以超快的速度衰减，这意味着RKHS中的函数是无限次可微的（$C^\infty$），即非常光滑。
-   **拉普拉斯核 (Laplace kernel)**: 其谱密度呈多项式衰减（$S(\omega) \propto (1+\omega^2)^{-1}$）。这对 $\hat{f}(\omega)$ 的衰减要求较弱，因此其RKHS中的[函数光滑性](@entry_id:161935)较低（例如，仅一阶可微）。

因此，选择高斯核相当于假设[目标函数](@entry_id:267263)是极其平滑的，而选择拉普拉斯核则更适合可能存在“[尖点](@entry_id:636792)”或变化更剧烈的函数，这使得后者在面对某些类型的噪声或离群点时可能表现出更强的鲁棒性 [@problem_id:3170321]。选择核函数，本质上就是为学习问题注入关于解的结构和性质的先验知识。