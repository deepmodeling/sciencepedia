## 引言
量子化场的各种态，如光子态，是构成我们对光与物质微观世界理解的基石，也是量子技术革命的核心资源。然而，仅用纯态的态矢量来描述量子系统，在面对与环境不可避免的相互作用或制备过程不完备的现实情况时，显得力不从心。为了全面理解并驾驭这些系统的量子特性，特别是那些没有经典类比的“非经典”性质，我们需要一个更强大、更普适的理论框架。本文旨在系统地建立这一框架，并展示其在现代物理学和技术前沿的广泛威力。

在接下来的内容中，我们将分三步展开探索。首先，在“原理与机制”一章中，我们将引入密度算符、相空间表示（如维格纳函数）和特征函数等核心数学工具，构建一个坚实的理论基础，用于精确描述和分析任意量子态。随后，在“应用与交叉学科联系”一章，我们将把这些理论工具应用于实践，探索量子态在量子计算、精密测量、凝聚态物理乃至黑洞物理和宇宙学等多个领域的深刻影响，展示这一理论框架的强大解释力和预测力。最后，“动手实践”部分将提供一系列精心设计的问题，帮助读者巩固所学知识，并将抽象概念转化为具体的计算技能。通过这一结构化的学习路径，读者将对量子化场的态建立起一个全面而深入的理解。

## 原理与机制

本章将深入探讨描述光量子态的核心原理与数学机制。我们将超越简单的态矢量描述，引入更为普适的密度算符，并探索在相空间中表示量子态的强大工具。本章将系统地阐述如何通过准概率分布和特征函数来刻画量子态，如何利用光子统计量来揭示其经典或非经典特性，并最终将这些工具应用于分析一些重要的非经典量子态，如压缩态、纠缠态和光子增减态。

### 量子态的表示：从态矢量到相空间

尽管纯量子态可以用希尔伯特空间中的态矢量 $|\psi\rangle$ 来完美描述，但实际系统往往与环境存在相互作用，或者我们对其制备过程的知识不完备。在这种情况下，系统处于一个混合态，必须使用**密度算符** $\hat{\rho}$ 来描述。密度算符是一个更为普适的工具，对于纯态 $|\psi\rangle$，其密度算符为 $\hat{\rho} = |\psi\rangle\langle\psi|$；对于混合态，则为纯态的统计系综 $\hat{\rho} = \sum_i p_i |\psi_i\rangle\langle\psi_i|$，其中 $p_i$ 是系统处于纯态 $|\psi_i\rangle$ 的概率。

在量子光学中，我们通常将任意单模光场态在**福克态 (Fock state)** 基 $\{|n\rangle\}$ 上展开，其中 $|n\rangle$ 是光子数算符 $\hat{n} = \hat{a}^\dagger \hat{a}$ 的本征态，表示场中恰好有 $n$ 个光子。除了福克态，其他一些基本量子态也构成了我们理论工具箱的基石，例如**相干态 (coherent state)** $|\alpha\rangle$（激光的理想模型）和**热态 (thermal state)**（描述与热库平衡的光场）。

然而，仅仅在福克基上展开密度算符（即给出矩阵元 $\rho_{mn} = \langle m|\hat{\rho}|n\rangle$）往往不够直观。为了更好地将量子态与我们对经典振荡器（由其位置和动量，或等效地，其振幅和相位描述）的直观理解联系起来，量子光学发展了一套在**相空间**中表示量子态的强大方法。相空间由一对共轭的**正交算符 (quadrature operators)** 张成，其定义为：
$$
\hat{q} = \frac{1}{\sqrt{2}}(\hat{a} + \hat{a}^{\dagger})
$$
$$
\hat{p} = \frac{i}{\sqrt{2}}(\hat{a}^{\dagger} - \hat{a})
$$
这些算符对应于经典谐振子的归一化位置和动量。我们的目标是将量子态 $\hat{\rho}$ 映射为一个在由复振幅 $\alpha$（其代表了相空间中的一个点，$\alpha = (q+ip)/\sqrt{2}$）构成的平面上的函数。这些函数被称为**准概率分布 (quasi-probability distributions)**。

最常用的准概率分布包括维格纳函数 $W(\alpha)$、格劳伯-苏达尚 P-表示 $P(\alpha)$ 和胡西米 Q-函数 $Q(\alpha)$。

**胡西米 Q-函数 (Husimi Q-function)** 是其中最容易理解的一个。它的定义为密度算符在相干态 $|\alpha\rangle$ 上的投影的期望值，并经过归一化：
$$
Q(\alpha) = \frac{1}{\pi} \langle \alpha | \hat{\rho} | \alpha \rangle
$$
$Q(\alpha)$ 可以被解释为在相空间点 $\alpha$ 附近找到该量子的概率密度。它始终是实数且非负的，就像一个真正的概率分布一样。然而，它描述的是一个被“模糊化”或“平滑化”的量子态视图。

作为一个具体的例子，我们可以计算平均光子数为 $\bar{n}$ 的**热态**的 Q-函数 [@problem_id:738242]。热态的密度算符在福克基下是对角的：
$$
\hat{\rho}_{th} = \frac{1}{1+\bar{n}} \sum_{n=0}^{\infty} \left(\frac{\bar{n}}{1+\bar{n}}\right)^n |n\rangle\langle n|
$$
将其代入 Q-函数的定义，经过一系列计算，包括利用相干态在福克基下的展开 $| \alpha \rangle = \exp(-|\alpha|^2/2) \sum_{n=0}^\infty (\alpha^n / \sqrt{n!}) |n\rangle$ 以及对指数级数的求和，我们得到一个优美的结果：
$$
Q(\alpha) = \frac{1}{\pi(1+\bar{n})} \exp\left(-\frac{|\alpha|^2}{1+\bar{n}}\right)
$$
这表明热态的 Q-函数是一个以原点为中心的高斯函数。其宽度由平均光子数 $\bar{n}$ 决定：$\bar{n}$ 越大，分布越宽，反映了热涨落的增强。当 $\bar{n} \to 0$ 时，热态趋于真空态 $|0\rangle$，其 Q-函数变为 $Q(\alpha) = \frac{1}{\pi}\exp(-|\alpha|^2)$。

与 Q-函数不同，**维格纳函数 (Wigner function)** $W(\alpha)$ 和**格劳伯-苏达尚 P-表示 (Glauber-Sudarshan P-representation)** $P(\alpha)$ 提供了关于量子态更精细的信息。特别是，维格纳函数可以取负值，而其负值区域是量子态**非经典性 (non-classicality)** 的一个明确标志。P-表示则将密度算符表示为相干态投影算符的加权积分，$\hat{\rho} = \int P(\alpha) |\alpha\rangle\langle\alpha| d^2\alpha$。对于非经典态，P-表示可能不是一个行为良好的函数，甚至可能比狄拉克-delta函数更为奇异。

### 特征函数：傅里叶空间中的分析工具

为了系统地研究和联系不同的相空间分布，引入**特征函数 (characteristic functions)** 的概念至关重要。它们本质上是相空间分布的[傅里叶变换](@entry_id:142120)，并与算符的不同排序方式紧密相关。

量子力学中，由于创生算符 $\hat{a}^\dagger$ 和湮灭算符 $\hat{a}$ 不对易（$[\hat{a}, \hat{a}^\dagger] = 1$），包含这些算符的函数其算符顺序至关重要。最常见的排序有：
- **正规排序 (Normal ordering)**：所有 $\hat{a}^\dagger$ 都移动到所有 $\hat{a}$ 的左边，记作 $:\hat{O}:$。
- **对称排序 (Symmetrical ordering)**：所有可能的算符排列被平均。
- **反常规排序 (Anti-normal ordering)**：所有 $\hat{a}^\dagger$ 都移动到所有 $\hat{a}$ 的右边。

与这些排序方式相对应，我们可以定义不同的特征函数。其中最重要的是**正规序特征函数** $\chi_N(\beta)$ 和**对称序（维格纳）特征函数** $\chi_W(\beta)$：
$$
\chi_N(\beta) = \mathrm{Tr}(\hat{\rho} :e^{\beta \hat{a}^\dagger - \beta^* \hat{a}}:) = \mathrm{Tr}(\hat{\rho} e^{\beta \hat{a}^\dagger} e^{-\beta^* \hat{a}})
$$
$$
\chi_W(\beta) = \mathrm{Tr}(\hat{\rho} e^{\beta \hat{a}^\dagger - \beta^* \hat{a}})
$$
其中 $\beta$ 是一个复数。

这两个特征函数之间存在一个简洁而深刻的关系。利用 Baker-Campbell-Hausdorff (BCH) 公式 $e^{\hat{X}+\hat{Y}} = e^{\hat{X}}e^{\hat{Y}}e^{-\frac{1}{2}[\hat{X},\hat{Y}]}$（当 $[\hat{X},\hat{Y}]$ 是一个 c-数时成立），我们可以将 $e^{\beta \hat{a}^\dagger - \beta^* \hat{a}}$ 分解。令 $\hat{X} = \beta \hat{a}^\dagger$ 和 $\hat{Y} = -\beta^* \hat{a}$，它们的对易子是 $[\beta \hat{a}^\dagger, -\beta^* \hat{a}] = -|\beta|^2[\hat{a}^\dagger, \hat{a}] = |\beta|^2$。因此，我们得到：
$$
e^{\beta \hat{a}^\dagger - \beta^* \hat{a}} = e^{\beta \hat{a}^\dagger} e^{-\beta^* \hat{a}} e^{-\frac{1}{2}|\beta|^2}
$$
将此关系代入 $\chi_W(\beta)$ 的定义，立即得到：
$$
\chi_W(\beta) = \chi_N(\beta) \exp\left(-\frac{1}{2}|\beta|^2\right)
$$
这个简单的关系是连接不同相空间表示的枢纽。P-表示和 Wigner 函数分别是 $\chi_N$ 和 $\chi_W$ 的辛傅里叶变换 [@problem_id:738209]：
$$
P(\alpha) = \int \frac{d^2\beta}{\pi^2} e^{\alpha\beta^* - \alpha^*\beta} \chi_N(\beta)
$$
$$
W(\alpha) = \int \frac{d^2\beta}{\pi^2} e^{\alpha\beta^* - \alpha^*\beta} \chi_W(\beta)
$$
结合上述关系，我们可以推导出 Wigner 函数和 P-表示之间的直接联系。由于傅里叶变换中的乘积对应于卷积，我们发现 $W(\alpha)$ 是 $P(\alpha)$ 与一个高斯核函数的卷积 [@problem_id:738066]：
$$
W(\alpha) = \int P(\gamma) K(\alpha-\gamma) \, d^2\gamma
$$
其中卷积核 $K(\delta)$ 是 $e^{-\frac{1}{2}|\beta|^2}$ 的傅里叶变换。通过计算一个标准的高斯积分，可以求得该核函数的形式 [@problem_id:738209]：
$$
K(\delta) = \frac{2}{\pi}\exp(-2|\delta|^2)
$$
这个结果定量地说明了 Wigner 函数是 P-表示经过高斯平滑后的结果。这种平滑作用“抹掉”了 P-表示中可能存在的奇异结构，使得 Wigner 函数总是行为良好，但也因此隐藏了一些非经典态的精细特征。

作为特征函数的一个简单应用，我们可以计算单光子福克态 $|1\rangle$ 的正规序特征函数 $\chi_N(\beta)$ [@problem_id:738125]。其计算过程如下：
$$
\chi_N(\beta) = \langle 1| e^{\beta \hat{a}^\dagger} e^{-\beta^* \hat{a}} |1\rangle
$$
将指数算符展开为泰勒级数，并利用 $\hat{a}|1\rangle = |0\rangle$ 和 $\hat{a}^\dagger|1\rangle = \sqrt{2}|2\rangle$，我们发现只有级数中的低阶项对结果有贡献。具体来说，只有常数项和包含 $\hat{a}^\dagger \hat{a}$ 的项存活下来，最终得到：
$$
\chi_N(\beta) = 1 - |\beta|^2
$$
这个简洁的多项式形式与相干态的指数形式 $\chi_N(\beta) = \exp(\alpha\beta^* - \alpha^*\beta)$ 或热态的高斯形式形成了鲜明对比，反映了福克态独特的非经典性质。

### 光子统计的表征

除了相空间分布，我们还可以通过直接测量光子数的统计量来表征光场。这些统计量为我们提供了判断光场是“类经典”还是“非经典”的实用判据。

#### 二阶相干函数 $g^{(2)}(0)$

**二阶相干函数 (second-order coherence function)** 在零延迟时间的取值 $g^{(2)}(0)$ 是衡量光子到达探测器时是倾向于成团 (bunching) 还是分离 (anti-bunching) 的标准。其定义为：
$$
g^{(2)}(0) = \frac{\langle \hat{a}^\dagger \hat{a}^\dagger \hat{a} \hat{a} \rangle}{\langle \hat{a}^\dagger \hat{a} \rangle^2} = \frac{\langle \hat{n}(\hat{n}-1) \rangle}{\langle \hat{n} \rangle^2}
$$
- $g^{(2)}(0) > 1$：光子聚束 (bunched)，如热光，光子倾向于成群到达。
- $g^{(2)}(0) = 1$：光子无规 (coherent/Poissonian)，如理想激光，光子到达时间不相关。
- $g^{(2)}(0)  1$：光子反聚束 (anti-bunched)，这是一个纯粹的量子效应，意味着探测到一个光子后，紧接着探测到另一个光子的概率降低。这是非经典性的一个标志。

一个有趣的例子是**相位随机化的相干态 (phase-randomized coherent state)** [@problem_id:738137]。该状态通过对一个纯相干态 $|\alpha_0 e^{i\phi}\rangle$ 在所有相位 $\phi$ 上进行平均得到，其密度算符为 $\hat{\rho} = \frac{1}{2\pi} \int_0^{2\pi} d\phi \, |\alpha_0 e^{i\phi}\rangle \langle\alpha_0 e^{i\phi}|$。通过在福克基下展开并进行积分，可以发现该操作会消除所有非对角元，得到一个对角的密度算符，其对角元（即光子数分布 $P(n)$）恰好是泊松分布 $P(n) = e^{-|\alpha_0|^2} \frac{|\alpha_0|^{2n}}{n!}$。对于泊松分布，我们有 $\langle \hat{n}(\hat{n}-1) \rangle = \langle \hat{n} \rangle^2$。因此，对于相位随机化的相干态，我们得到：
$$
g^{(2)}(0) = 1
$$
尽管这个结果与纯相干态相同，但其物理根源不同。它源于一个具有泊松光子数分布的混合态，而不是一个纯的相干态。

#### 曼德尔 Q 参数 (Mandel Q parameter)

**曼德尔 Q 参数 (Mandel Q parameter)** 直接量化了光子数分布的方差 $\langle (\Delta \hat{n})^2 \rangle$ 相对于泊松分布方差（其方差等于均值 $\langle \hat{n} \rangle$）的偏离程度：
$$
Q_M = \frac{\langle (\Delta \hat{n})^2 \rangle - \langle \hat{n} \rangle}{\langle \hat{n} \rangle}
$$
- $Q_M > 0$：超泊松分布 (Super-Poissonian)，光子数涨落大于相干态。
- $Q_M = 0$：泊松分布 (Poissonian)，如相干态。
- $Q_M  0$：亚泊松分布 (Sub-Poissonian)，光子数涨落小于相干态，这是非经典性的另一个明确标志。

特征函数为我们提供了一个计算 $Q_M$ 参数的优雅途径。对于一个相位不变的态，其正规序特征函数只依赖于 $|\beta|^2$，即 $\chi_N(\beta) = f(|\beta|^2)$。通过对 $f(x)$（其中 $x=|\beta|^2$）在 $x=0$ 处进行泰勒展开，可以将其各阶导数与光子数算符的各阶矩联系起来 [@problem_id:738308]。可以证明：
$$
\langle \hat{n} \rangle = -f'(0)
$$
$$
\langle \hat{n}(\hat{n}-1) \rangle = 2 f''(0)
$$
利用这些关系，我们可以将 $Q_M$ 参数完全用特征函数的导数表示：
$$
Q_M = \frac{\langle \hat{n}(\hat{n}-1) \rangle + \langle \hat{n} \rangle - \langle \hat{n} \rangle^2 - \langle \hat{n} \rangle}{\langle \hat{n} \rangle} = \frac{2f''(0) - (-f'(0))^2}{-f'(0)} = -\frac{2 f''(0)}{f'(0)} + f'(0)
$$
这个公式展示了特征函数作为理论工具的强大威力，它将一个抽象的数学构造（特征函数及其导数）与一个可直接测量的物理量（曼德尔 Q 参数）联系起来。

### 重要的非经典态及其性质

有了上述分析工具，我们现在可以研究一些在量子信息和量子计量学中至关重要的非经典态。

#### 压缩态

**压缩态 (Squeezed states)** 是一类其某个正交分量的量子噪声被压缩到标准量子极限（即真空态噪声水平）以下的量子态。单模压缩算符通常写为 $\hat{S}(\zeta) = \exp[\frac{1}{2}(\zeta^* \hat{a}^2 - \zeta (\hat{a}^\dagger)^2)]$，其中 $\zeta = r e^{i\phi}$ 是复压缩参数。当作用在真空态上时，它产生**压缩真空态 (squeezed vacuum)**。

一个更贴近实际的场景是**压缩热态 (squeezed thermal state)**，它由对一个初始平均光子数为 $\bar{n}$ 的热态施加压缩操作得到。压缩操作会如何影响热噪声呢？压缩算符对正交算符的变换规则为 $\hat{S}^\dagger(r)\hat{q}\hat{S}(r) = e^{-r}\hat{q}$ 和 $\hat{S}^\dagger(r)\hat{p}\hat{S}(r) = e^{r}\hat{p}$（这里取 $\phi=0$）。初始热态的两个正交分量具有相同的方差 $(\Delta q_{th})^2 = (\Delta p_{th})^2 = \bar{n} + 1/2$。经过压缩后，新的方差变为：
$$
(\Delta q)^2 = (\bar{n} + 1/2) e^{-2r}
$$
$$
(\Delta p)^2 = (\bar{n} + 1/2) e^{2r}
$$
这表明压缩操作将总的噪声（热噪声和真空噪声之和）在一个方向上压缩，在另一个方向上放大。我们可以计算正交噪声的不对称性 [@problem_id:738131]：
$$
(\Delta p)^2 - (\Delta q)^2 = (\bar{n} + 1/2) (e^{2r} - e^{-2r}) = (2\bar{n}+1)\sinh(2r)
$$
这个结果清晰地展示了压缩强度 $r$ 和初始热噪声 $\bar{n}$ 对噪声分布的共同影响。

#### 纠缠与双模压缩真空

**双模压缩真空 (two-mode squeezed vacuum)** 是连续变量量子信息中原型性的**纠缠态 (entangled state)**。它由双模压缩算符 $\hat{S}_2(r) = \exp(r(\hat{a}_1^\dagger \hat{a}_2^\dagger - \hat{a}_1 \hat{a}_2))$ 作用在双模真空态 $|0\rangle_1 |0\rangle_2$ 上产生。在福克基下，其展开式揭示了两个模式之间完美的光子数关联：
$$
|\psi\rangle_{12} = \frac{1}{\cosh r} \sum_{n=0}^{\infty} (\tanh r)^n |n\rangle_1 |n\rangle_2
$$
这个表达式意味着，如果我们在模式1中测量到 $n$ 个光子，那么我们必然会在模式2中也测量到 $n$ 个光子。尽管整个双模系统处于一个纯态，但如果我们只关注其中一个模式（例如，通过对另一个模式进行**部分迹 (partial trace)** 来忽略它），我们会发现该模式处于一个混合态。

通过计算模式1的约化密度算符 $\hat{\rho}_1 = \mathrm{Tr}_2(|\psi\rangle_{12} \langle\psi|_{12})$，我们得到一个惊人的结果 [@problem_id:738091]：
$$
\hat{\rho}_1 = \frac{1}{\cosh^2 r} \sum_{n=0}^{\infty} (\tanh^2 r)^n |n\rangle_1 \langle n|_1
$$
这个密度算符的形式与我们前面看到的热态完全相同！通过比较，我们可以识别出有效平均光子数 $\bar{n}_1$ 满足 $\frac{\bar{n}_1}{1+\bar{n}_1} = \tanh^2 r$。解出 $\bar{n}_1$，我们得到：
$$
\bar{n}_1 = \sinh^2 r
$$
这个深刻的结果表明，纠缠纯态的局域性质表现为热统计。源于量子关联的涨落，在局域看来，与源于热库的随机涨落无法区分。

#### 量子态工程：光子减法

除了幺正演化，我们还可以通过非幺正操作来“雕刻”量子态，这被称为**量子态工程 (quantum state engineering)**。一个典型的例子就是**光子减法 (photon subtraction)**，即从光场中移走一个光子，这可以通过让光场与一个辅助系统（如一个二能级原子）弱相互作用并进行后选择测量来实现。这个过程在数学上由湮灭算符 $\hat{a}$ 的作用来描述。

将光子减法应用于压缩真空态，会产生有趣的效应。我们知道压缩真空只包含偶数个光子的叠加。对其施加 $\hat{a}$ 算符，由于 $\hat{a}|2m\rangle = \sqrt{2m}|2m-1\rangle$，会将其转变为一个只包含奇数个光子的叠加态。例如，我们可以计算在这个**单光子减法压缩真空态 (single-photon-subtracted squeezed vacuum state, SPSSV)** 中测量到恰好一个光子的概率 $P(1)$ [@problem_id:738126]。经过计算，包括对产生的新态进行归一化（其归一化因子为 $1/\sinh r$），我们得到：
$$
P(1) = \frac{1}{\cosh^3 r}
$$

更有趣的是，SPSSV 态有一个非常简洁的等价描述。利用算符恒等式 $ \hat{a}\hat{S}(r) = \hat{S}(r)(\cosh(r)\hat{a} - \sinh(r)\hat{a}^\dagger) $，我们发现 $\hat{a}|\text{sqz vac}\rangle = \hat{a}\hat{S}(r)|0\rangle = -\sinh(r) \hat{S}(r)|1\rangle$。这意味着，对压缩真空做光子减法，等价于对单光子福克态 $|1\rangle$ 做压缩操作！

这个洞察使我们能够轻松地分析 SPSSV 态的非经典性。例如，我们可以计算其 Wigner 函数的**负体积 (negative volume)** $\mathcal{V}^- = \iint_{W(x,p)0} |W(x,p)| dx dp$，这是衡量非经典性的一个重要指标 [@problem_id:738113]。单光子态 $|1\rangle$ 的 Wigner 函数为 $W_1(x,p) = \frac{1}{\pi} e^{-(x^2+p^2)}(2(x^2+p^2)-1)$，它在相空间中心有一个负值区域。由于 SPSSV 态是一个压缩的单光子态，其 Wigner 函数可以通过对 $W_1$ 的坐标进行拉伸变换得到：$W_{sps}(x,p) = W_1(xe^r, pe^{-r})$。尽管这个变换会把 Wigner 函数的形状从圆形拉伸为椭圆形，但积分区域的变换恰好抵消了坐标拉伸的影响。通过一个坐标变换和在极坐标下的积分，可以计算出负体积，结果为：
$$
\mathcal{V}^- = 2\exp(-1/2) - 1 \approx 0.213
$$
令人惊讶的是，这个负体积是一个与压缩参数 $r$ 无关的常数！这揭示了一个深刻的物理图像：SPSSV 态的非经典性（由 Wigner 函数的负性体现）完全继承自其核心的单光子成分，而压缩操作只是在相空间中重新“塑造”了这种非经典性，并未增加或减少其总量。

本章系统介绍了描述和分析量子光场的关键原理和机制。从基本的相空间表示到高级的非经典性度量，这些工具为我们理解和应用量子世界中光的奇特性质奠定了坚实的基础。