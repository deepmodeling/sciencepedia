## 引言
在[计算工程](@entry_id:178146)、物理学和数据科学等众多领域，矩阵的[特征值](@entry_id:154894)是描述线性系统内在属性的核心指标，例如结构的[振动频率](@entry_id:199185)、动力系统的稳定性或数据集的主要变异方向。然而，在现实世界中，系统模型总是会受到[参数不确定性](@entry_id:264387)、[测量误差](@entry_id:270998)或设计变更的影响。这就引出了一个根本性的问题：当描述系统的矩阵发生微小扰动时，其关键的[特征值](@entry_id:154894)会如何变化？量化这种变化的程度，即[特征值](@entry_id:154894)的敏感度，对于评估系统的鲁棒性、指导优化设计以及预测模型行为至关重要。

本文旨在系统性地解答这一问题，为读者构建一个关于[特征值](@entry_id:154894)摄动理论的完整知识框架。文章将分为三个核心部分：

首先，在“原理与机制”一章中，我们将从特征多项式的[不变性](@entry_id:140168)出发，奠定理论基础。我们将推导简单[特征值](@entry_id:154894)敏感度的精确公式，引入衡量其“病态”程度的条件数，并深入探讨当[特征值](@entry_id:154894)出现[重数](@entry_id:136466)，特别是数值计算中极具挑战性的亏损情形时，其行为会发生何种质变。

其次，在“应用与跨学科联系”一章中，我们将跨出纯数学的范畴，展示这些理论如何在[结构力学](@entry_id:276699)、航空航天、[网络科学](@entry_id:139925)、化学生物乃至金融和机器学习等领域中，解决从[结构共振](@entry_id:261212)、颤振分析到[网络鲁棒性](@entry_id:146798)和[模型泛化](@entry_id:174365)能力等一系列实际问题。

最后，“动手实践”部分将通过三个精心设计的计算练习，引导您亲手处理从简单[特征值](@entry_id:154894)的方向敏感度，到非对称矩阵的条件数，再到[亏损特征值](@entry_id:177573)的极端病态行为等关键概念，从而将理论知识转化为可操作的技能。

## 原理与机制

本章旨在深入探讨[矩阵特征值](@entry_id:156365)的摄动理论，重点阐述特征多项式的基本性质以及[特征值](@entry_id:154894)敏感度的核心原理与计算机制。理解[特征值](@entry_id:154894)如何[响应矩阵](@entry_id:754302)的微小变化，在[计算工程](@entry_id:178146)、物理[系统建模](@entry_id:197208)和数据科学等领域至关重要，因为它直接关系到系统稳定性、鲁棒性和[数值分析](@entry_id:142637)的可靠性。

### [特征多项式](@entry_id:150909)及其[不变性](@entry_id:140168)

对于一个给定的 $n \times n$ 复数矩阵 $A \in \mathbb{C}^{n \times n}$，其**特征多项式** (characteristic polynomial) $p_A(\lambda)$ 定义为：
$$
p_A(\lambda) = \det(\lambda I - A)
$$
其中 $I$ 是 $n \times n$ [单位矩阵](@entry_id:156724)，$\lambda \in \mathbb{C}$ 是一个标量变量。根据[代数基本定理](@entry_id:152321)，这个 $n$ 次多项式在[复数域](@entry_id:153768)中有 $n$ 个根（计入[重数](@entry_id:136466)），这些根 $\lambda_1, \lambda_2, \dots, \lambda_n$ 构成了矩阵 $A$ 的**谱** (spectrum)，即其全体**[特征值](@entry_id:154894)** (eigenvalues)。

[特征多项式](@entry_id:150909)可以展开为：
$$
p_A(\lambda) = \lambda^n + c_{n-1}(A)\lambda^{n-1} + \dots + c_1(A)\lambda + c_0(A)
$$
多项式的系数 $c_k(A)$ 与矩阵 $A$ 的[特征值](@entry_id:154894)之间存在深刻的联系。具体而言，这些系数（可能相差一个符号）是[特征值](@entry_id:154894)的**初等[对称多项式](@entry_id:153581)** (elementary symmetric polynomials)。例如，对于一个 $3 \times 3$ 的矩阵，其[特征值](@entry_id:154894)为 $\lambda_1, \lambda_2, \lambda_3$，特征多项式可写为 $p_A(\lambda) = \lambda^3 - s_1 \lambda^2 + s_2 \lambda - s_3$。通过展开 $(\lambda - \lambda_1)(\lambda - \lambda_2)(\lambda - \lambda_3)$ 并比较系数，我们得到：
- $s_1 = \lambda_1 + \lambda_2 + \lambda_3 = \operatorname{tr}(A)$
- $s_2 = \lambda_1\lambda_2 + \lambda_1\lambda_3 + \lambda_2\lambda_3 = \frac{1}{2}\left((\operatorname{tr} A)^2 - \operatorname{tr}(A^2)\right)$
- $s_3 = \lambda_1\lambda_2\lambda_3 = \det(A)$

这里，$\operatorname{tr}(A)$ 表示矩阵 $A$ 的**迹** (trace)，即主对角线元素之和。这些关系，尤其是[迹和行列式](@entry_id:149685)分别等于[特征值](@entry_id:154894)之和与乘积的性质，是线性代数中的基本结论。这些系数与[特征值](@entry_id:154894)的幂和 $p_k(A) = \sum_{i=1}^n \lambda_i^k$ 之间也通过**[牛顿和](@entry_id:153339)** (Newton's sums) 相关联 [@problem_id:2443352]。

一个至关重要的性质是[特征多项式](@entry_id:150909)在**相似变换** (similarity transformation)下的不变性。如果矩阵 $B$ 与 $A$ 相似，即存在一个可逆矩阵 $P$ 使得 $B = P^{-1}AP$，那么它们的[特征多项式](@entry_id:150909)是完全相同的。其推导过程简洁而深刻：
$$
p_B(\lambda) = \det(\lambda I - B) = \det(\lambda I - P^{-1}AP) = \det(P^{-1}(\lambda I - A)P)
$$
利用[行列式的乘法性质](@entry_id:148055) $\det(XYZ) = \det(X)\det(Y)\det(Z)$ 和 $\det(P^{-1}) = (\det(P))^{-1}$，我们得到：
$$
p_B(\lambda) = \det(P^{-1})\det(\lambda I - A)\det(P) = \det(\lambda I - A) = p_A(\lambda)
$$
由于两个多项式对所有 $\lambda$ 都相等，它们的系数必然完全相同，即 $c_k(B) = c_k(A)$ 对所有 $k$ 成立。这意味着[相似矩阵](@entry_id:155833)拥有完全相同的[特征值](@entry_id:154894)及其[代数重数](@entry_id:154240)。这个不变性表明，[特征值](@entry_id:154894)是矩阵所代表的线性变换的内在属性，不随[坐标基](@entry_id:270149)的选择（由 $P$ 体现）而改变。因此，如果一个矩阵族 $B(t) = P(t)^{-1}AP(t)$ 仅仅因为相似变换矩阵 $P(t)$ 随时间 $t$ 变化而变化，其[特征值](@entry_id:154894)将保持恒定，对 $t$ 的敏感度为零 [@problem_id:2443350]。

### [特征值](@entry_id:154894)敏感度：简单[特征值](@entry_id:154894)情形

然而，在计算工程和科学建模中，我们更关心当矩阵**自身**因物理参数、模型误差或[数值离散化](@entry_id:752782)而发生摄动时，其[特征值](@entry_id:154894)会如何变化。考虑一个依赖于参数 $\varepsilon$ 的矩阵族 $A(\varepsilon) = A_0 + \varepsilon E + O(\varepsilon^2)$，其中 $A_0$ 是未摄动矩阵，$E$ 是摄动方向。我们希望了解 $A(\varepsilon)$ 的[特征值](@entry_id:154894) $\lambda_i(\varepsilon)$ 相对于 $A_0$ 的[特征值](@entry_id:154894) $\lambda_i(0)$ 的变化情况，即计算其敏感度（或一阶导数）$\frac{d\lambda_i}{d\varepsilon}\big|_{\varepsilon=0}$。

#### 一阶摄动公式

当[特征值](@entry_id:154894) $\lambda_i$ 是**简单**的（即[代数重数](@entry_id:154240)为1）时，其敏感度有一个优雅的解析表达式。对于[非对称矩阵](@entry_id:153254)，我们需要同时考虑**右[特征向量](@entry_id:151813)** (right eigenvector) $x_i$ 和**左[特征向量](@entry_id:151813)** (left eigenvector) $y_i$，它们分别满足：
$$
A x_i = \lambda_i x_i \quad \text{and} \quad y_i^\top A = \lambda_i y_i^\top
$$
其中 $y_i^\top$ 表示 $y_i$ 的[转置](@entry_id:142115)（在复数域中，通常使用[共轭转置](@entry_id:147909) $y_i^\ast$）。对于一个简单的[特征值](@entry_id:154894) $\lambda_i$，其对应的左、右[特征向量](@entry_id:151813)满足 $y_i^\top x_i \neq 0$。

通过对[特征值方程](@entry_id:192306) $A(\varepsilon)x_i(\varepsilon) = \lambda_i(\varepsilon)x_i(\varepsilon)$ 两边关于 $\varepsilon$ 求导，并在 $\varepsilon=0$ 处取值，再从左侧乘以 $y_i(0)^\top$，经过一番推导可以得到一阶摄动公式 [@problem_id:2776773] [@problem_id:2443335]：
$$
\frac{d\lambda_i}{d\varepsilon}\bigg|_{\varepsilon=0} = \frac{y_i^\top E x_i}{y_i^\top x_i}
$$
这个公式是[特征值](@entry_id:154894)摄动理论的基石。它表明，[特征值](@entry_id:154894)的一阶变化由摄动矩阵 $E$ 在由左、右[特征向量](@entry_id:151813)张成的“方向”上的投影决定。分母 $y_i^\top x_i$ 是一个归一化因子，其非零性保证了简单[特征值](@entry_id:154894)的敏感度是有限的。

#### 特征[向量归一化](@entry_id:149602)的作用

由于[特征向量](@entry_id:151813)的定义只到标量倍数，我们可以对 $x_i$ 和 $y_i$ 进行任意的非零缩放。例如，如果我们将 $x_i$ 替换为 $\alpha x_i$，将 $y_i$ 替换为 $\beta y_i$（其中 $\alpha, \beta$ 是非零标量），那么分子 $y_i^\top E x_i$ 会变为 $\alpha\beta (y_i^\top E x_i)$，分母 $y_i^\top x_i$ 会变为 $\alpha\beta (y_i^\top x_i)$ [@problem_id:2443353]。由于缩放因子 $\alpha\beta$ 从分子和分母中消去，**[特征值](@entry_id:154894)的敏感度值本身与[特征向量](@entry_id:151813)的归一化方式无关**。

尽管如此，选择一种方便的归一化约定可以简化表达式。一种常见的选择是**双正交归一化** (biorthogonal normalization)，即缩放 $x_i$ 和 $y_i$ 使得 $y_i^\top x_i = 1$。在这种约定下，敏感度公式简化为：
$$
\frac{d\lambda_i}{d\varepsilon}\bigg|_{\varepsilon=0} = y_i^\top E x_i
$$
需要强调的是，即使我们通常将右特征[向量归一化](@entry_id:149602)为单位长度，例如 $\|x_i\|_2=1$，这并不意味着 $y_i^\top x_i$ 会自动等于1。除非矩阵具有特殊结构（如对称性），$y_i$ 和 $x_i$ 通常不是平行的向量。

#### [特征值条件数](@entry_id:176727)

从敏感度公式可以推导出一个关于[特征值稳定性](@entry_id:196190)的重要概念。对 $\Delta \lambda_i \approx \frac{y_i^\top (\Delta A) x_i}{y_i^\top x_i}$ 取[绝对值](@entry_id:147688)并使用Cauchy-[Schwarz不等式](@entry_id:202153)，可以得到一个界：
$$
|\Delta \lambda_i| \le \frac{\|y_i\|_2 \|x_i\|_2}{|y_i^\top x_i|} \|\Delta A\|_2
$$
这里的 $\|\cdot\|_2$ 指[谱范数](@entry_id:143091)。上式中的系数被称为简单[特征值](@entry_id:154894) $\lambda_i$ 的**条件数** (condition number)，记为 $c_i$：
$$
c_i = \frac{\|y_i\|_2 \|x_i\|_2}{|y_i^\top x_i|}
$$
[条件数](@entry_id:145150) $c_i$ 量化了[特征值](@entry_id:154894) $\lambda_i$ 对矩阵摄动的最坏情况下的敏感度。$c_i$ 的值越大，表明该[特征值](@entry_id:154894)越“病态”或“敏感”。注意 $c_i \ge 1$。

### 特殊情形与应用

#### 对称与[正规矩阵](@entry_id:185943)：理想情形

当矩阵 $A$ 是**实对称** ($A=A^\top$) 或更一般地是**正规** ($A A^\ast = A^\ast A$) 时，摄动分析大大简化。对于这类矩阵，左、右[特征向量](@entry_id:151813)是相同的（在实对称情况下 $y_i = x_i$）。我们可以选择一组标准正交的[特征向量基](@entry_id:163721)，此时 $\|x_i\|_2=1$ 且 $y_i^\top x_i = x_i^\top x_i = \|x_i\|_2^2 = 1$ [@problem_id:2443353]。

在这种理想情况下，所有[特征值](@entry_id:154894)的条件数 $c_i$ 均为1。这意味着[特征值](@entry_id:154894)的绝对变化不会超过摄动本身的范数，即 $|\Delta \lambda_i| \le \|\Delta A\|_2$。[正规矩阵](@entry_id:185943)的[特征值](@entry_id:154894)是**良态** (well-conditioned) 的。

这一性质在分析系统鲁棒性时非常有用。例如，考虑一个对称正定矩阵 $A$，它在工程中常作为[刚度矩阵](@entry_id:178659)或[协方差矩阵](@entry_id:139155)出现。其[谱范数](@entry_id:143091) $\|A\|_2 = \lambda_{\max}(A)$，其条件数 $\kappa_2(A) = \frac{\lambda_{\max}(A)}{\lambda_{\min}(A)}$。根据**[Weyl不等式](@entry_id:183500)**，对于一个摄动 $E$，我们有 $|\lambda_k(A+E) - \lambda_k(A)| \le \|E\|_2$。若摄动大小以相对形式给出，如 $\|E\|_2 \le \epsilon \|A\|_2$，则最小特征值 $\lambda_{\min}$ 的相对变化满足 [@problem_id:2443286]：
$$
\frac{|\lambda_{\min}(A+E) - \lambda_{\min}(A)|}{\lambda_{\min}(A)} \le \frac{\epsilon \|A\|_2}{\lambda_{\min}(A)} = \epsilon \cdot \kappa_2(A)
$$
这个结果表明，即使单个[特征值](@entry_id:154894)是良态的 ($c_i=1$)，[最小特征值](@entry_id:177333)的**相对**敏感度也可能被矩阵的整体条件数 $\kappa_2(A)$ 放大。一个大的条件数 $\kappa_2(A)$ 意味着矩阵接近奇异，其[最小特征值](@entry_id:177333)对相对摄动非常敏感。

对于[正规矩阵](@entry_id:185943)，其奇异值的大小等于其[特征值](@entry_id:154894)的大小 ($ \sigma_k = |\lambda_k| $)。因此，一个[正规矩阵](@entry_id:185943)到[奇异矩阵](@entry_id:148101)集合的[谱范数](@entry_id:143091)距离，等于其最小[奇异值](@entry_id:152907)，也即其[最小特征值](@entry_id:177333)的模长 $\min_i |\lambda_i(A)|$ [@problem_id:2443335]。

#### 应用：[振动](@entry_id:267781)系统的[频率稳定性](@entry_id:272608)

[特征值](@entry_id:154894)敏感度分析在动力学系统中有直接应用。考虑一个二阶[线性时不变](@entry_id:276287)（LTI）系统，如一个由[质量-弹簧-阻尼器](@entry_id:271783)组成的[振动](@entry_id:267781)系统。其状态空间矩阵 $A(\alpha)$ 的[特征值](@entry_id:154894)决定了系统的模态行为。对于一个[欠阻尼系统](@entry_id:178889)，它会有一对共轭复数[特征值](@entry_id:154894) $\lambda_{\pm} = \sigma \pm i\omega$。
- 实部 $\sigma$ 决定了[振动](@entry_id:267781)的衰减（或增长）速率。
- 虚部 $\omega$ 决定了系统的固有[振动](@entry_id:267781)角频率。

假设系统的一个参数（如弹簧刚度 $k$）受到参数 $\alpha$ 的影响，即 $k=k(\alpha)$。我们可以计算[特征值](@entry_id:154894)虚部对 $\alpha$ 的敏感度 $S_\omega = \frac{d\omega}{d\alpha}$。这个值量化了[振动频率](@entry_id:199185)随参数变化的快慢。$|S_\omega|$ 越小，表明系统的[振动频率](@entry_id:199185)对参数扰动越不敏感，即[频率稳定性](@entry_id:272608)越高 [@problem_id:2443279]。例如，对于一个状态矩阵为 $A(\alpha) = \begin{bmatrix} 0  1 \\ -k(\alpha)/m  -c/m \end{bmatrix}$ 的系统，通过求解[特征方程](@entry_id:265849) $\lambda^2 + \frac{c}{m}\lambda + \frac{k(\alpha)}{m} = 0$，可以直接得到 $\omega(\alpha) = \sqrt{\frac{k(\alpha)}{m} - (\frac{c}{2m})^2}$，并对其求导以评估[频率稳定性](@entry_id:272608)。

### 复杂情形：多重与[亏损特征值](@entry_id:177573)

当[特征值](@entry_id:154894)不再是简单的时候，其摄动行为会变得更加复杂。

#### 半单[重特征值](@entry_id:154579)的分裂

如果一个[特征值](@entry_id:154894) $\lambda_0$ 的[代数重数](@entry_id:154240) $m>1$，但其[几何重数](@entry_id:155584)也等于 $m$，则称该[特征值](@entry_id:154894)是**半单的** (semisimple)。这意味着存在 $m$ 个[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)，构成一个 $m$ 维的特征空间。

在这种情况下，一个一般的摄动 $A(\varepsilon) = A_0 + \varepsilon E$ 通常会导致这个 $m$ [重特征值](@entry_id:154579)**分裂** (split) 成 $m$ 个独立的、简单的新[特征值](@entry_id:154894)。这些新[特征值](@entry_id:154894)的一阶行为不再由单个敏感度值描述，而是由一个 $m \times m$ 的小规模特征值问题决定。

具体而言，设 $V$ 的列是对应于 $\lambda_0$ 的右特征空间的一组基，而 $W$ 的列是左[特征空间](@entry_id:638014)的一组基，并满足双正交条件 $W^\top V = I_m$。那么，摄动后的 $m$ 个[特征值](@entry_id:154894)的一阶近似为：
$$
\lambda_i(\varepsilon) = \lambda_0 + \varepsilon \mu_i + o(\varepsilon) \quad (i=1, \dots, m)
$$
其中，$\mu_1, \dots, \mu_m$ 是 $m \times m$ **投影摄动矩阵** $G = W^\top E V$ 的 $m$ 个[特征值](@entry_id:154894) [@problem_id:2443346]。这个强大的结果将一个 $n \times n$ 矩阵的复杂摄动问题，简化为了在 $m$ 维[子空间](@entry_id:150286)上的一个小得多的特征值问题。

#### [亏损特征值](@entry_id:177573)：无限敏感度

最极端的情况是**[亏损特征值](@entry_id:177573)** (defective eigenvalue)，即其[几何重数](@entry_id:155584)小于[代数重数](@entry_id:154240) $m$。这意味着不存在 $m$ 个线性无关的[特征向量](@entry_id:151813)来张成一个 $m$ 维的[特征空间](@entry_id:638014)。这种情况的典型代表是 Jordan 块。

对于[亏损特征值](@entry_id:177573)，标准的一阶摄动理论完全失效。摄动后的[特征值](@entry_id:154894)不再是关于 $\varepsilon$ 的解析函数，而是表现为分数次幂的形式。考虑一个简单的 $2 \times 2$ Jordan 块 $A_0 = \begin{bmatrix} 0  1 \\ 0  0 \end{bmatrix}$，它有一个[代数重数](@entry_id:154240)为2、[几何重数](@entry_id:155584)为1的[亏损特征值](@entry_id:177573) $\lambda_0=0$。若施加一个摄动 $E = \begin{bmatrix} 0  0 \\ 1  0 \end{bmatrix}$，则摄动矩阵为 $A(\varepsilon) = \begin{bmatrix} 0  1 \\ \varepsilon  0 \end{bmatrix}$。其[特征值](@entry_id:154894)为 $\lambda_{\pm}(\varepsilon) = \pm\sqrt{\varepsilon}$ [@problem_id:2443335]。

这个 $\sqrt{\varepsilon}$ 的依赖关系是关键。其导数 $\frac{d\lambda_\pm}{d\varepsilon} = \pm \frac{1}{2\sqrt{\varepsilon}}$ 在 $\varepsilon \to 0^+$ 时趋于无穷大。这意味着[特征值](@entry_id:154894)对摄动的响应是**无限敏感的**。一个 $O(\varepsilon)$ 的微小摄动，导致了 $O(\sqrt{\varepsilon})$ 的[特征值](@entry_id:154894)变化，其变化率远大于[线性关系](@entry_id:267880)。

我们可以通过一个数值实验来量化这种行为。定义一个**标度化敏感度指标** $s(A,E,t) = \delta(A,E,t)/t$，其中 $\delta$ 是摄动前后谱集的最大偏移。
- 对于具有简单或半单[特征值](@entry_id:154894)的矩阵，当摄动大小 $t \to 0$ 时，$s(A,E,t)$ 会收敛到一个有限的常数。
- 对于具有[亏损特征值](@entry_id:177573)的矩阵，如 $A_1 = \begin{bmatrix} 0  1 \\ 0  0 \end{bmatrix}$，我们发现 $s(A_1,E_1,t) \propto t^{-1/2}$，当 $t \to 0$ 时发散。对于 $3 \times 3$ 的 Jordan 块，敏感度可能更糟，如 $t^{-2/3}$ [@problem_id:2443272]。
这种无限敏感性凸显了[亏损特征值](@entry_id:177573)在数值计算和物理建模中的极端“病态”性质。

### 全局界与局部敏感度

最后，我们将基于导数的局部敏感度分析与提供全局界的理论进行对比。

**Bauer-Fike 定理** 为[可对角化矩阵](@entry_id:150100)的[特征值](@entry_id:154894)摄动提供了一个全局的、统一的界。如果 $A=V\Lambda V^{-1}$，其中 $V$ 是由右[特征向量](@entry_id:151813)组成的矩阵，那么对于 $A+\Delta A$ 的任意[特征值](@entry_id:154894) $\tilde{\lambda}$，都存在 $A$ 的一个[特征值](@entry_id:154894) $\lambda_j$ 使得：
$$
|\tilde{\lambda} - \lambda_j| \le \kappa_2(V) \|\Delta A\|_2
$$
其中 $\kappa_2(V) = \|V\|_2 \|V^{-1}\|_2$ 是[特征向量](@entry_id:151813)矩阵 $V$ 的谱[条件数](@entry_id:145150)。这个界适用于所有[特征值](@entry_id:154894)，其大小由整个[特征向量基](@entry_id:163721)的“倾斜度”或“近[线性相关](@entry_id:185830)性”（由 $\kappa_2(V)$ 度量）决定。

与之相对，我们之[前推](@entry_id:158718)导的基于一阶分析的界是局部的和[特征值](@entry_id:154894)特定的：
$$
|\Delta \lambda_i| \le c_i \|\Delta A\|_2
$$
其中 $c_i$ 是第 $i$ 个[特征值](@entry_id:154894)的[条件数](@entry_id:145150)。

这两个界的关系是：$c_i \le \kappa_2(V)$。Bauer-Fike 定理提供了一个适用于所有[特征值](@entry_id:154894)的、有时可能较为悲观的“最坏情况”估计。而基于 $c_i$ 的局部敏感度分析则更为精细，它能够揭示某些[特征值](@entry_id:154894)可能比其他[特征值](@entry_id:154894)稳定得多。例如，一个矩阵可能整体上有一个很大的 $\kappa_2(V)$（即[特征向量基](@entry_id:163721)接近线性相关），但其中某个[特征值](@entry_id:154894)可能恰好与一个[条件数](@entry_id:145150) $c_i$ 很小的左、右[特征向量](@entry_id:151813)[对相关](@entry_id:203353)联。在这种情况下，Bauer-Fike 界会高估该特定[特征值](@entry_id:154894)的敏感度，而局部一阶分析则能提供更准确的预测 [@problem_id:2443306]。对于[正规矩阵](@entry_id:185943)，$\kappa_2(V)=1$ 且所有 $c_i=1$，两个界重合，再次说明了[正规矩阵](@entry_id:185943)的优良性质。