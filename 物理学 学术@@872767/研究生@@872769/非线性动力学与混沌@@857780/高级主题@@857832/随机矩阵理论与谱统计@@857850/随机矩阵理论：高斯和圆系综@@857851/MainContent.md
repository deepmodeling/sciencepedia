## 引言
[随机矩阵理论](@entry_id:142253)（Random Matrix Theory, RMT）已成为理解复杂系统统计特性的一个强大[范式](@entry_id:161181)，尤其适用于那些底层动力学细节难以企及的系统。它最初为解释重[原子核](@entry_id:167902)的能谱而生，但其原理已被证明具有惊人的普适性。RMT所要解决的核心问题是：如何从由复杂性和基本对称性主导的系统中，绕过求解精确解的困难，提炼出普适的统计规律。本文旨在对这一深刻理论进行一次全面的探索。在第一章“原理与机制”中，我们将深入剖析RMT的核心数学框架，聚焦于经典的高斯与[循环系综](@entry_id:182798)，并推导如维格纳猜想与半[圆律](@entry_id:192228)等基石性成果。紧接着，在“应用与[交叉](@entry_id:147634)学科联系”一章，我们将展示该理论惊人的应用广度，将其抽象模型与量子混沌、介观物理乃至数论中神秘的黎曼ζ[函数零点](@entry_id:176831)等真实世界现象联系起来。最后，“动手实践”部分将提供具体问题，以巩固对这些概念的理解。让我们一同深入这个由随机性催生出深刻秩序的优雅世界。

## 原理与机制

继前一章对随机矩阵理论（Random Matrix Theory, RMT）的背景和物理动机进行概述之后，本章将深入探讨其核心的数学原理和物理机制。我们将从定义经典的[高斯系综](@entry_id:187727)（Gaussian Ensembles）入手，推导其[矩阵元](@entry_id:186505)的基本统计性质。随后，我们将展示如何从矩阵元的联合分布过渡到更为关键的[本征值分布](@entry_id:194746)，并由此导出随机矩阵理论的两个基石性成果：描述[局域标度](@entry_id:178651)上[本征值排斥](@entry_id:136686)的维格纳猜想（Wigner surmise），以及描述全局标度上[本征值](@entry_id:154894)谱密度的维格纳半[圆律](@entry_id:192228)（Wigner's semicircle law）。我们还将探讨在谱的体态（bulk）和边缘（edge）处涌现的普适关联函数。最后，我们将简要介绍与[高斯系综](@entry_id:187727)密切相关的[循环系综](@entry_id:182798)（Circular Ensembles）。

### [高斯系综](@entry_id:187727)：定义与基本性质

[高斯系综](@entry_id:187727)是随机矩阵理论中最基本、最重要的研究对象。它们是根据矩阵所满足的[基本对称性](@entry_id:161256)来分类的。物理上，这些对称性通常与系统在时间反演下的行为相关。存在三种主要的**[高斯系综](@entry_id:187727)**：

1.  **[高斯正交系综](@entry_id:184271) (Gaussian Orthogonal Ensemble, GOE)**：由[实对称矩阵](@entry_id:192806) $H = H^T$ 构成。这类矩阵所描述的系统具有[时间反演不变性](@entry_id:152159)，且[时间反演](@entry_id:182076)算符 $T$ 满足 $T^2 = I$。

2.  **高斯幺正系综 (Gaussian Unitary Ensemble, GUE)**：由复厄米矩阵 $H = H^\dagger$ 构成。这类矩阵描述了不具有[时间反演不变性](@entry_id:152159)的系统。

3.  **高斯辛系综 (Gaussian Symplectic Ensemble, GSE)**：由[四元数](@entry_id:147023)实厄米矩阵构成。这类矩阵描述的系统具有[时间反演不变性](@entry_id:152159)，但[时间反演](@entry_id:182076)算符满足 $T^2 = -I$（例如，具有[半整数自旋](@entry_id:148826)且无[磁场](@entry_id:153296)的情况）。

这些系综的“高斯”特性源于其矩阵元[概率分布](@entry_id:146404)的形式。一个 $N \times N$ [随机矩阵](@entry_id:269622) $H$ 属于[高斯系综](@entry_id:187727)的概率测度由其所有独立[矩阵元](@entry_id:186505)的[联合概率密度函数](@entry_id:267139)（Joint Probability Density Function, JPDF）给出，其一般形式为：
$$
P(H) \propto \exp(-\alpha \operatorname{Tr}(H^2))
$$
其中 $\alpha$ 是一个正实数标度参数。这种形式的选择并非偶然，其关键在于 $\operatorname{Tr}(H^2)$ 在相应的对称变换（对于GOE是[正交变换](@entry_id:155650)，对于GUE是幺正变换）下是不变的。这保证了概率测度在相应的矩阵空间中具有正确的变换性质。

这个 JPDF 意味着矩阵的各个独立元素是服从高斯分布的[随机变量](@entry_id:195330)。具体的[方差](@entry_id:200758)设定则根据系综类型和归一化习惯有所不同。例如，在一个常见的设定中：
*   对于 $2 \times 2$ 的 **GOE** 矩阵 $H = \begin{pmatrix} h_{11}  h_{12} \\ h_{12}  h_{22} \end{pmatrix}$，对角元 $h_{11}, h_{22}$ 和非对角元 $h_{12}$ 是独立的零均值高斯[随机变量](@entry_id:195330)，其[方差](@entry_id:200758)可以设定为 $\text{Var}(h_{11}) = \text{Var}(h_{22}) = \sigma^2$ 以及 $\text{Var}(h_{12}) = \sigma^2/2$ [@problem_id:889379]。
*   对于 $2 \times 2$ 的 **GUE** 矩阵 $H = \begin{pmatrix} a  c - id \\ c + id  b \end{pmatrix}$，实部 $a, b, c, d$ 是独立的零均值高斯[随机变量](@entry_id:195330)。一种常见的[方差](@entry_id:200758)设定是 $\text{Var}(a) = \text{Var}(b) = \sigma^2$ 和 $\text{Var}(c) = \text{Var}(d) = \sigma^2/2$，这意味着对角元 $H_{ii}$ 的[方差](@entry_id:200758)为 $\sigma^2$，而非对角元 $H_{ij}$ 的实部和虚部的[方差](@entry_id:200758)均为 $\sigma^2/2$ [@problem_id:889321]。

在接触[本征值统计](@entry_id:196782)之前，我们可以通过计算矩阵本身的一些统计量来熟悉这些[分布](@entry_id:182848)。例如，考虑上述 $2 \times 2$ GOE 矩阵，其[行列式](@entry_id:142978)为 $D = \det(H) = h_{11}h_{22} - h_{12}^2$。由于 $h_{11}, h_{22}, h_{12}$ [相互独立](@entry_id:273670)且均值为零，我们可以计算[行列式](@entry_id:142978)的[方差](@entry_id:200758) [@problem_id:889379]：
$$
\begin{align}
\text{Var}(D)  = \text{Var}(h_{11}h_{22} - h_{12}^2) = \text{Var}(h_{11}h_{22}) + \text{Var}(h_{12}^2) \\
 = (\mathbb{E}[h_{11}^2]\mathbb{E}[h_{22}^2] - (\mathbb{E}[h_{11}]\mathbb{E}[h_{22}])^2) + (\mathbb{E}[h_{12}^4] - (\mathbb{E}[h_{12}^2])^2) \\
 = (\sigma^2 \cdot \sigma^2 - 0) + (3(\sigma^2/2)^2 - (\sigma^2/2)^2) \\
 = \sigma^4 + 2(\sigma^2/2)^2 = \sigma^4 + \frac{\sigma^4}{2} = \frac{3}{2}\sigma^4
\end{align}
$$
这里我们使用了零均值[高斯变量](@entry_id:276673) $X \sim \mathcal{N}(0, \tau^2)$ 的性质：$\mathbb{E}[X^2] = \tau^2$ 和 $\mathbb{E}[X^4] = 3\tau^4$。

更进一步，我们还可以研究不同[矩阵不变量](@entry_id:195012)之间的关联。例如，在另一个稍有不同的 GOE [方差](@entry_id:200758)设定（$\text{Var}(h_{11}) = \text{Var}(h_{22}) = 2\sigma^2, \text{Var}(h_{12}) = \sigma^2$）下，我们可以计算在给定迹 $T = \text{Tr}(H) = T_0$ 的条件下，[行列式](@entry_id:142978) $D = \det(H)$ 的[条件期望](@entry_id:159140)值 [@problem_id:889320]。通过变量代换 $h_{11}=(T+S)/2, h_{22}=(T-S)/2$，可以证明 $T$ 和 $S=h_{11}-h_{22}$ 是独立的。因此，
$$
\mathbb{E}[D | T=T_0] = \mathbb{E}\left[\frac{T_0^2-S^2}{4} - h_{12}^2\right] = \frac{T_0^2 - \mathbb{E}[S^2]}{4} - \mathbb{E}[h_{12}^2] = \frac{T_0^2 - \text{Var}(S)}{4} - \text{Var}(h_{12})
$$
代入[方差](@entry_id:200758) $\text{Var}(S) = \text{Var}(h_{11}-h_{22}) = 4\sigma^2$ 和 $\text{Var}(h_{12}) = \sigma^2$，我们得到 $\mathbb{E}[D | T=T_0] = \frac{T_0^2}{4} - 2\sigma^2$。这些初步的计算展示了如何直接从矩阵元的[分布](@entry_id:182848)出发进行分析。

### 从[矩阵元](@entry_id:186505)到[本征值](@entry_id:154894)：联合[本征值分布](@entry_id:194746)

尽管[矩阵元](@entry_id:186505)的性质是定义系综的起点，但在物理应用中，我们更关心的是矩阵的**[本征值](@entry_id:154894)** $\{\lambda_i\}$，因为它们通常对应于量子系统的能级。因此，一个核心步骤是从[矩阵元](@entry_id:186505)的 JPDF 转换为[本征值](@entry_id:154894)的 JPDF。

这个变量代换的过程包括两个关键部分：指数项的变换和[雅可比行列式](@entry_id:137120)（Jacobian）的计算。指数项 $\operatorname{Tr}(H^2)$ 在酉（或正交）变换下是不变的，这意味着它可以直接用[本征值](@entry_id:154894)表示：$\operatorname{Tr}(H^2) = \sum_{i=1}^N \lambda_i^2$。

最具变革性的贡献来自于雅可比行列式。从 $N(N+1)/2$ 个独立的实数（GOE情形）或 $N^2$ 个独立的实数（GUE情形）变换到 $N$ 个[本征值](@entry_id:154894)和其余的“角度”变量（描述本征矢量），其[雅可比行列式](@entry_id:137120)中会出现一个因子，这个因子正比于所有[本征值](@entry_id:154894)差的乘积。在积分掉与本征矢量相关的自由度后，我们得到[本征值](@entry_id:154894)的[联合概率密度函数](@entry_id:267139)：
$$
P(\lambda_1, \dots, \lambda_N) = C_{N,\beta} \prod_{1 \le i  j \le N} |\lambda_j - \lambda_i|^\beta \exp\left(-\frac{\beta}{2} \sum_{k=1}^N \lambda_k^2\right)
$$
[@problem_id:889313]。这里的参数 $\beta$ 被称为**戴森指数 (Dyson index)**，它直接反映了矩阵的对称性类别：
*   $\beta=1$ 对应 **GOE** ([实对称矩阵](@entry_id:192806))
*   $\beta=2$ 对应 **GUE** (复厄米矩阵)
*   $\beta=4$ 对应 **GSE** (四元数[厄米矩阵](@entry_id:155147))

这个表达式是随机矩阵理论的中心结果之一。其中，$\prod |\lambda_j - \lambda_i|^\beta$ 这一项，即**范德蒙德[行列式](@entry_id:142978) (Vandermonde determinant)** 的 $\beta$ 次方，是至关重要的。它表明，两个[本征值](@entry_id:154894)靠得很近（$|\lambda_j - \lambda_i| \to 0$）的概率会趋向于零。这种现象被称为**[能级排斥](@entry_id:137654) (level repulsion)**，是[量子混沌](@entry_id:139638)系统能谱的一个标志性特征。戴森指数 $\beta$ 直接控制了排斥的强度：$\beta$ 越大，[本征值](@entry_id:154894)之间靠得太近的可能性就越小。

### [能级间距分布](@entry_id:195657)：维格纳猜想

为了定量地研究[能级排斥](@entry_id:137654)，我们考察**[能级间距分布](@entry_id:195657) (level spacing distribution)** $P(s)$，即相邻[本征值](@entry_id:154894)之间距离 $s$ 的[概率分布](@entry_id:146404)。为了消除对具体能量标度的依赖，通常会对间距进行**展开 (unfolding)**，即用局域平均[能级间距](@entry_id:181168) $\langle s \rangle$ 作为单位来度量间距，研究归一化间距 $S = s / \langle s \rangle$ 的[分布](@entry_id:182848)。

对于 $N \times N$ 的大矩阵，精确计算 $P(s)$ 是一个非常困难的问题。然而，在 $N=2$ 的情况下，计算是完全可行的，并且其结果惊人地准确地描述了大 $N$ 极限下的情形。这个 $N=2$ 的结果被称为**维格纳猜想 (Wigner surmise)**。

让我们以 $2 \times 2$ 的 GOE 矩阵为例来推导它 [@problem_id:889329]。此时 $\beta=1$，两个[本征值](@entry_id:154894) $\lambda_1, \lambda_2$ 的 JPDF 为：
$$
P(\lambda_1, \lambda_2) = C_1 |\lambda_1 - \lambda_2| \exp(-\alpha (\lambda_1^2 + \lambda_2^2))
$$
我们引入新的变量：[能级间距](@entry_id:181168) $s = |\lambda_1 - \lambda_2|$（不妨设 $\lambda_1 \ge \lambda_2$）和能级中心 $E = (\lambda_1 + \lambda_2)/2$。反变换为 $\lambda_1 = E + s/2, \lambda_2 = E - s/2$。该变换的[雅可比行列式](@entry_id:137120)为1。代入 JPDF，我们得到：
$$
P(s, E) ds dE = C_1 s \exp(-\alpha ((E+s/2)^2 + (E-s/2)^2)) ds dE = C_1 s \exp(-\alpha (2E^2 + s^2/2)) ds dE
$$
为了得到只关于 $s$ 的[分布](@entry_id:182848)，我们将 $E$ 从 $-\infty$ 到 $\infty$ 积分掉：
$$
P(s) = \int_{-\infty}^{\infty} P(s, E) dE = C_1 s \exp(-\alpha s^2/2) \int_{-\infty}^{\infty} \exp(-2\alpha E^2) dE
$$
该积分为标准[高斯积分](@entry_id:187139)，其结果正比于 $1/\sqrt{\alpha}$。因此，未归一化的间距[分布](@entry_id:182848)为 $P(s) \propto s \exp(-\alpha s^2/2)$。可以看出，当 $s \to 0$ 时，$P(s) \propto s$，这正是线性排斥的体现。

通过归一化 $\int_0^\infty P(s) ds = 1$ 和计算平均间距 $\langle s \rangle = \int_0^\infty s P(s) ds$，然后进行变量代换 $S = s/\langle s \rangle$，我们可以得到归一化[能级间距](@entry_id:181168)的[分布](@entry_id:182848)，即维格纳猜想对 GOE 的形式：
$$
P(S) = \frac{\pi}{2} S \exp\left(-\frac{\pi}{4} S^2\right)
$$
这个[分布](@entry_id:182848)与任何具体的参数（如 $\alpha$）无关，体现了其普适性。利用这个[分布](@entry_id:182848)，我们可以计算各种概率，例如，归一化间距大于2的概率为 $P(S > 2) = \int_2^\infty P(S) dS = e^{-\pi}$ [@problem_id:889329]。

对于 GUE ($\beta=2$) 和 GSE ($\beta=4$)，可以进行类似的推导。其 JPDF 中的因子分别为 $|\lambda_1 - \lambda_2|^2$ 和 $|\lambda_1 - \lambda_2|^4$。
*   对于 GUE，我们得到 $P(s) \propto s^2 \exp(-c_2 s^2)$，当 $s \to 0$ 时呈现二次排斥 [@problem_id:889321]。归一化后，GUE 的维格纳猜想为 $p(s) = \frac{32}{\pi^2}s^2\exp(-\frac{4s^2}{\pi})$。
*   对于 GSE，我们得到 $P(s) \propto s^4 \exp(-c_4 s^2)$，呈现更强的四次排斥 [@problem_id:889340]。

戴森指数 $\beta$ 对能[谱统计](@entry_id:198528)的核心影响，可以通过一个一般化的计算来体现。考虑 $N=2$ 的高斯 $\beta$-系综，我们可以计算[本征值](@entry_id:154894)间距平方的[期望值](@entry_id:153208)与[本征值](@entry_id:154894)平方[和的期望值](@entry_id:196769)之比 $R(\beta) = \frac{\langle (\lambda_2 - \lambda_1)^2 \rangle}{\langle \lambda_1^2 + \lambda_2^2 \rangle}$。通过适当的变量代换和利用 Gamma 函数的性质，可以得到一个只依赖于 $\beta$ 的简洁结果 [@problem_id:889313]：
$$
R(\beta) = \frac{2(\beta+1)}{\beta+2}
$$
这个结果清晰地表明，随着 $\beta$ 从1（GOE）增加到2（GUE）再到4（GSE），分子（代表排斥）相对于分母（代表整体[能量尺度](@entry_id:196201)）的贡献增大了，与我们关于[能级排斥](@entry_id:137654)随 $\beta$ 增强的图像完全一致。

### 宏观尺度：维格纳半[圆律](@entry_id:192228)

维格纳猜想描述了[能级间距](@entry_id:181168)的局域统计规律。在宏观尺度上，随机矩阵理论的另一个标志性成果是**维格纳半[圆律](@entry_id:192228)**，它描述了在 $N \to \infty$ 极限下[本征值](@entry_id:154894)的全局密度[分布](@entry_id:182848) $\rho(E)$。

研究 $\rho(E)$ 的一个强大工具是**[Stieltjes 变换](@entry_id:196440)**（或称 Green 函数）。对于一个[随机矩阵](@entry_id:269622) $H$，其 [Stieltjes 变换](@entry_id:196440)定义为：
$$
g(z) = \lim_{N\to\infty} \frac{1}{N} \text{Tr} \mathbb{E}\left[ (zI - H)^{-1} \right] = \lim_{N\to\infty} \mathbb{E}\left[ \frac{1}{N} \sum_{i=1}^N \frac{1}{z-\lambda_i} \right] = \int \frac{\rho(E')}{z-E'} dE'
$$
其中 $z = E+i\eta$ 是一个[复变量](@entry_id:175312)，$\eta > 0$。一旦求得 $g(z)$，[本征值](@entry_id:154894)密度就可以通过一个反演公式得到：
$$
\rho(E) = -\frac{1}{\pi} \lim_{\eta \to 0^+} \Im[g(E+i\eta)]
$$
对于大 $N$ 的 GUE 矩阵，可以证明 $g(z)$ 满足一个自洽的[代数方程](@entry_id:272665)。若 GUE 矩阵元的[概率密度](@entry_id:175496)正比于 $\exp(-\frac{N}{2\sigma^2} \text{Tr}(H^2))$，则该方程为 [@problem_id:889381]：
$$
\sigma^2 g(z)^2 - z g(z) + 1 = 0
$$
这是一个关于 $g(z)$ 的二次方程，解为 $g(z) = \frac{z \pm \sqrt{z^2 - 4\sigma^2}}{2\sigma^2}$。根据物理要求，$|z| \to \infty$ 时 $g(z) \sim 1/z$，我们必须选择负号的解。将 $z=E+i\eta$ 代入，取 $\eta \to 0^+$ 的极限，我们发现当 $|E| > 2\sigma$ 时，平方根内的值为正，$\Im[g(E)] = 0$；而当 $|E| \le 2\sigma$ 时，平方根为纯虚数，从而得到非零的虚部。
最终，我们得到[本征值](@entry_id:154894)密度：
$$
\rho(E) = \begin{cases} \frac{1}{2\pi\sigma^2}\sqrt{4\sigma^2 - E^2}  \text{if } |E| \le 2\sigma \\ 0  \text{if } |E| > 2\sigma \end{cases}
$$
这个[分布](@entry_id:182848)的图像是一个以原点为中心、半径为 $2\sigma$ 的半圆形，这便是著名的**维格纳半[圆律](@entry_id:192228)**。其谱密度在中心 $E=0$ 处达到最大值 $\rho_{\max} = \rho(0) = \frac{1}{\pi\sigma}$ [@problem_id:889381]。

### 谱的普适关联：体态与边缘

除了局域的[能级间距](@entry_id:181168)和全局的谱密度，RMT 还对任意尺度上的[本征值](@entry_id:154894)关联给出了普适的预测。这些预测在两个区域尤为重要：**谱体态 (bulk)**，即远离谱边界的区域；和**谱边缘 (edge)**，即谱密度的端点附近。

在谱体态中，经过展开操作后，[本征值](@entry_id:154894)之间的关联函数呈现出一种仅依赖于能量差（以平均[能级间距](@entry_id:181168)为单位）的普适形式。对于 GUE，两点关联函数 $R_2(s)$ 的连通部分，即**两点簇函数** $Y_2(s)$，由所谓的**正弦核 (sine kernel)** 决定 [@problem_id:889396]：
$$
Y_2(s) = -K(s)^2 \quad \text{with} \quad K(s) = \frac{\sin(\pi s)}{\pi s}
$$
这种关联结构导致了**谱刚度 (spectral rigidity)**，即能级数在给定能量区间内的涨落被极大地抑制了。具体来说，长度为 $L$ 的区间内的能级数[方差](@entry_id:200758) $\Sigma^2(L)$ 对于 GUE 并非[线性增长](@entry_id:157553) $\Sigma^2(L) \sim L$（如泊松分布），而是对数增长 $\Sigma^2(L) \sim \frac{1}{\pi^2}\ln L$。正弦核的形式与谱刚度密切相关，其[归一化条件](@entry_id:156486) $\int_0^\infty K(s)^2 ds = 1/2$ 是确保 $\Sigma^2(L)$ 中线性项消失的关键。我们可以通过此条件来确定正弦核的形式。例如，假设核 $K(s)$ 是动量空间中一个区间的[傅里叶变换](@entry_id:142120) $K(s) = \frac{1}{2\pi} \int_{-\alpha}^{\alpha} e^{iks} dk = \frac{\sin(\alpha s)}{\pi s}$，利用该[归一化条件](@entry_id:156486)可唯一确定 $\alpha=\pi$ [@problem_id:889396]。确定了[核函数](@entry_id:145324)后，我们可以计算任意间距处的关联，例如 $Y_2(1/2) = -(\frac{\sin(\pi/2)}{\pi/2})^2 = -4/\pi^2$。

在谱的边缘，例如 GUE 谱的最大[本征值](@entry_id:154894)附近，需要不同的[标度变换](@entry_id:166413)。这里的统计性质由另一种普适的核函数——**艾里核 (Airy kernel)**——所支配。最大[本征值](@entry_id:154894)的[分布](@entry_id:182848)，经过适当的平移和缩放后，收敛于一个普适的[分布](@entry_id:182848)，即**Tracy-Widom [分布](@entry_id:182848)** $F_2(s)$。这个[分布](@entry_id:182848)可以表示为一个作用在区间 $(s, \infty)$ 上的 Fredholm [行列式](@entry_id:142978) $F_2(s) = \det(I - K_{\text{Ai}})_{L^2(s, \infty)}$。艾里核由艾里函数 $\text{Ai}(u)$ 及其导数构成：
$$
K_{\text{Ai}}(x, y) = \frac{\text{Ai}(x)\text{Ai}'(y) - \text{Ai}'(x)\text{Ai}(y)}{x - y}
$$
艾里核具有深刻的数学结构，这种结构源于[艾里函数](@entry_id:198690)满足的[微分方程](@entry_id:264184) $\text{Ai}''(u) - u \text{Ai}(u) = 0$。一个体现其内在对称性的基本性质是，艾里核满足一个重要的[微分](@entry_id:158718)恒等式。定义艾里微分算子 $\mathcal{L}_u = \frac{\partial^2}{\partial u^2} - u$，可以证明 [@problem_id:889317]：
$$
(\mathcal{L}_x - \mathcal{L}_y) K_{\text{Ai}}(x, y) = 0
$$
这个恒等式是艾里核[可积性](@entry_id:142415)的体现，也是求解 Tracy-Widom [分布](@entry_id:182848)所依赖的潘勒韦方程（Painlevé equation）的出发点。

### [循环系综](@entry_id:182798)

除了[高斯系综](@entry_id:187727)，另一族重要的[随机矩阵](@entry_id:269622)系综是**[循环系综](@entry_id:182798) (Circular Ensembles)**，它们由酉矩阵构成，而不是厄米矩阵。它们分别是**循环[正交系](@entry_id:184795)综 (COE)**、**循环幺正系综 (CUE)** 和**循环辛系综 (CSE)**。这些系综在研究[量子混沌](@entry_id:139638)系统的[演化算符](@entry_id:182628)（Floquet 算子）或[散射矩阵](@entry_id:137017)时特别有用，因为这些算子本身就是酉的。

[循环系综](@entry_id:182798)的[概率测度](@entry_id:190821)不再是高斯形式，而是定义在相应[矩阵群](@entry_id:137464)上的**[哈尔测度](@entry_id:142417) (Haar measure)**，这是群上唯一不变的均匀测度。以 CUE 为例，它是 $N \times N$ 酉矩阵群 $U(N)$ 配备了[哈尔测度](@entry_id:142417)构成的系综。

[哈尔测度](@entry_id:142417)的均匀性意味着什么？我们可以通过一个 $2 \times 2$ 的 CUE 矩阵 $U$ 来直观理解 [@problem_id:889345]。一个 $2 \times 2$ [酉矩阵](@entry_id:138978)的任意一列，例如 $(U_{11}, U_{21})^T$，是复二维空间 $\mathbb{C}^2$ 中[单位球](@entry_id:142558)面上的一个[均匀分布](@entry_id:194597)的随机向量。这意味着 $|U_{11}|^2 + |U_{21}|^2 = 1$。令 $x = |U_{11}|^2$，那么 $x$ 的取值范围是 $[0, 1]$。由于在 $\mathbb{C}^2 \cong \mathbb{R}^4$ 的单位三维球面上的[分布](@entry_id:182848)是均匀的，通过恰当的[坐标变换](@entry_id:172727)（例如超球坐标），可以证明 $x$ 的[概率密度函数](@entry_id:140610) $p(x)$ 在其支撑域 $[0, 1]$ 上是一个常数。通过归一化 $\int_0^1 p(x) dx = 1$，我们得到一个非常简洁的结果：
$$
p(x) = 1, \quad \text{for } x \in [0,1]
$$
这个简单的结果深刻地反映了[哈尔测度](@entry_id:142417)的均匀性，并为研究[循环系综](@entry_id:182798)中本征[相角](@entry_id:274491)（eigenphases）的统计性质提供了基础。与[高斯系综](@entry_id:187727)的[本征值分布](@entry_id:194746)在实轴上不同，[循环系综](@entry_id:182798)的[本征值](@entry_id:154894)（均为幺模复数）均匀地[分布](@entry_id:182848)在复平面的单位圆上。而它们[相角](@entry_id:274491)的间距[分布](@entry_id:182848)，在经过展开后，与相应[高斯系综](@entry_id:187727)的[能级间距分布](@entry_id:195657)遵循相同的统计规律。