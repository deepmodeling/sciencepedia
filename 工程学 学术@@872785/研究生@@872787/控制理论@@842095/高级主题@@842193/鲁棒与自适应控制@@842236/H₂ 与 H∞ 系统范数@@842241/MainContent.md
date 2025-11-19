## 引言
在[现代控制系统](@entry_id:269478)设计中，仅仅确保系统稳定是远远不够的。工程师们更关心系统的性能——它如何响应外部扰动？它在[模型不确定性](@entry_id:265539)面前有多稳健？系统范数为此提供了一套严谨而强大的数学语言，用以量化线性系统的“增益”或“大小”，从而精确回答这些性能问题。然而，不同的性能目标需要不同的度量标准，这正是控制理论中最为核心的两种范数——$\mathcal{H}_2$与$\mathcal{H}_\infty$范数——发挥作用的地方。它们分别从“平均能量”和“峰值增益”这两个截然不同的角度刻画系统行为，但如何选择和使用它们常常是初学者的困惑所在。

本文旨在系统性地厘清$\mathcal{H}_2$与$\mathcal{H}_\infty$范数的理论与实践。我们将首先在 **“原理与机制”** 一章中，深入探讨两种范数的基本定义、物理内涵以及计算方法，并着重对比它们在衡量系统性能上的根本差异。接着，在 **“应用与跨学科联系”** 一章，我们将展示这些理论工具如何在鲁棒控制、[模型降阶](@entry_id:171175)、[滤波器设计](@entry_id:266363)等实际工程问题中发挥关键作用，并揭示其与信号处理、机器学习等领域的深刻联系。最后，通过 **“动手实践”** 中的具体计算练习，读者将巩固所学知识，并掌握范数计算的核心技能。让我们从这两种范数的基本原理开始，一同探索现代控制分析与设计的精髓。

## 原理与机制

在对控制系统进行分析与设计时，我们不仅需要判断其稳定性，还常常需要量化其性能。例如，我们可能想知道系统对扰动的抑制能力有多强，或者在面对不确定性时其鲁棒性如何。系统范数为此提供了一套严谨的数学工具，用于衡量线性时不变（LTI）系统的“大小”或“增益”。在本章中，我们将深入探讨两种最重要的系统范数：$\mathcal{H}_2$范数和$\mathcal{H}_\infty$范数。我们将从它们的基本定义出发，揭示其深刻的物理内涵，并探讨其计算方法与适用条件。

### $\mathcal{H}_\infty$范数：峰值增益的度量

$\mathcal{H}_\infty$范数是[鲁棒控制理论](@entry_id:163253)的基石，它量化了系统在所有频率和所有输入方向上的“最坏情况”或峰值增益。

#### 定义与物理内涵

对于一个[传递函数矩阵](@entry_id:271746)$G(s)$，如果它在右半复平面$\\{s \in \mathbb{C} : \mathrm{Re}(s) > 0\\}$是解析的，并且在虚轴上是有界的，那么它就属于**[Hardy空间](@entry_id:173385)$\mathcal{H}_\infty$** [@problem_id:2711593]。对于一个稳定的[LTI系统](@entry_id:271946)，其[传递函数](@entry_id:273897)的所有极点都在左半平面，因此天然满足在[右半平面](@entry_id:277010)解析的条件。

$\mathcal{H}_\infty$范数的定义为：
$$
\\|G\\|_{\infty} \triangleq \sup_{\omega \in \mathbb{R}} \\bar{\\sigma}\\big(G(j\\omega)\\big)
$$
其中，$G(j\\omega)$是系统在[角频率](@entry_id:261565)$\omega$处的频率响应矩阵，$\bar{\sigma}(\cdot)$表示矩阵的最大奇异值。

这个定义背后有着清晰的物理意义。对于一个[LTI系统](@entry_id:271946)，$\mathcal{H}_\infty$范数等于其作为从输入信号空间$\mathcal{L}_2$到输出信号空间$\mathcal{L}_2$的算子的**[诱导范数](@entry_id:163775)** [@problem_id:2901535]。换言之，它描述了系统对单位能量输入信号所能产生的最大能量输出的增益：
$$
\\|G\\|_{\infty} = \\sup_{u(t) \in \\mathcal{L}_2, u \neq 0} \\frac{\\|y(t)\\|_{2}}{\\|u(t)\\|_{2}}
$$
其中，$\\|u(t)\\|_{2}^2 = \\int_{-\infty}^{\infty} u(t)^T u(t) dt$是信号的能量。因此，$\mathcal{H}_\infty$范数是系统能量增益的最坏情况度量。我们可以通过构造一个[能量集中](@entry_id:203621)在峰值频率和最差输入方向上的带限输入信号序列来逼近这个上确界 [@problem_id:2901535]。

#### 单输入单输出（SISO）系统

对于单输入单输出（SISO）系统，$G(j\omega)$是一个标量复数。矩阵的[奇异值](@entry_id:152907)退化为[复数的模](@entry_id:634598)。因此，定义简化为 [@problem_id:2711592]：
$$
\\|G\\|_{\infty} = \\sup_{\omega \in \mathbb{R}} |G(j\\omega)|
$$
这正是频率响应的[波特图](@entry_id:275309)上幅值曲线的峰值。对于一个有理[传递函数](@entry_id:273897)$G(s)$，$|G(j\omega)|^2 = G(j\omega)G(-j\omega)$是一个关于$\omega^2$的[有理函数](@entry_id:154279)。因此，我们可以通过求解$\frac{d}{d\omega}\left(|G(j\omega)|^2\right)=0$来找到所有可能的峰值频率，然后将这些频率的幅值与[直流增益](@entry_id:267449)（$\omega=0$处）进行比较，从而确定其$\mathcal{H}_\infty$范数 [@problem_id:2711592]。

#### 多输入多输出（MIMO）系统：增益的方向性

对于多输入多输出（MIMO）系统，增益不仅依赖于频率，还依赖于输入的**方向**。在特定频率$\omega_0$下，最大[奇异值](@entry_id:152907)$\bar{\sigma}(G(j\omega_0))$给出了该频率下的最大可能增益。这个最大增益是通过一个特定的输入方向实现的，该方向由$G(j\omega_0)$的**[右奇异向量](@entry_id:754365)**给出。具体来说，如果$v_1$是与最大奇异值$\sigma_1 = \bar{\sigma}(G(j\omega_0))$相关联的[右奇异向量](@entry_id:754365)，那么当输入相量为$v_1$时，输出相量$u_1 = G(j\omega_0)v_1$将与相应的**[左奇异向量](@entry_id:751233)**对齐，并且其范数被放大了$\sigma_1$倍，即$\\|u_1\\|_2 = \\sigma_1 \\|v_1\\|_2$ [@problem_id:2711602]。因此，$\mathcal{H}_\infty$范数不仅告诉我们最坏情况下的增益是多少，其对应的[奇异向量](@entry_id:143538)还揭示了在哪个频率、以何种输入方向组合时会发生这种情况。

#### 范数有限的条件

一个关键问题是：对于一个由[状态空间实现](@entry_id:166670)$(A, B, C, D)$描述的[稳定LTI系统](@entry_id:260867)（即$A$是Hurwitz矩阵），$\mathcal{H}_\infty$范数何时是有限的？

我们知道，当$\omega \to \infty$时，$G(j\omega) = C(j\omega I - A)^{-1}B + D$趋近于常数矩阵$D$。由于$A$是稳定的，对于所有有限的$\omega$，$G(j\omega)$都是有界的。因此，只要$D$本身是有限的（对于任何有限维矩阵这总是成立的），整个[频率响应](@entry_id:183149)函数就是有界的。这意味着，对于一个内部稳定的[LTI系统](@entry_id:271946)，其$\mathcal{H}_\infty$范数是有限的**当且仅当系统是真（proper）的**。系统是否为严格真（strictly proper，即$D=0$）并不影响$\mathcal{H}_\infty$范数的有限性 [@problem_id:2711613] [@problem_id:2711615]。

### $\mathcal{H}_2$范数：系统能量的度量

与$\mathcal{H}_\infty$范数关注峰值增益不同，$\mathcal{H}_2$范数提供了一种衡量系统“平均”或“总”增益的方式，通常与系统能量相关。

#### 定义与物理内涵

对于一个在右半平面解析的[传递函数矩阵](@entry_id:271746)$G(s)$，如果它在虚轴边界上的积分是有限的，那么它就属于**[Hardy空间](@entry_id:173385)$\mathcal{H}_2$** [@problem_id:2711593]。其范数的平方定义为：
$$
\\|G\\|_{2}^2 \triangleq \frac{1}{2\pi} \int_{-\infty}^{\infty} \mathrm{tr}\big(G(j\omega)^* G(j\omega)\big) \mathrm{d}\omega
$$
其中，$\mathrm{tr}(\cdot)$表示[矩阵的迹](@entry_id:139694)，$\mathrm{tr}(M^*M)$等于矩阵$M$的[Frobenius范数](@entry_id:143384)的平方$\|M\|_F^2$。

这个定义同样具有深刻的物理意义，可以通过两种等价的方式来理解：

1.  **脉冲响应能量**：根据[Parseval定理](@entry_id:139215)，频率域的积分等价于时域的积分。对于一个因果[LTI系统](@entry_id:271946)，其$\mathcal{H}_2$范数的平方等于其脉冲[响应矩阵](@entry_id:754302)$g(t)$的总能量 [@problem_id:2711590] [@problem_id:2901535]：
    $$
    \\|G\\|_{2}^2 = \int_{0}^{\infty} \mathrm{tr}\big(g(t)^T g(t)\big) \mathrm{d}t = \int_{0}^{\infty} \\|g(t)\\|_F^2 \mathrm{d}t
    $$
    这表示$\mathcal{H}_2$范数衡量的是系统在受到[单位脉冲](@entry_id:272155)输入后，其输出的总能量。它反映了系统对瞬时扰动的响应有多“剧烈”或多“持久”。

2.  **白噪声响应[方差](@entry_id:200758)**：$\mathcal{H}_2$范数在[随机控制](@entry_id:170804)中也扮演着核心角色。如果系统的输入是一组不相关的、零均值、单位[功率谱密度](@entry_id:141002)的[白噪声](@entry_id:145248)信号，那么系统[稳态](@entry_id:182458)输出向量的总[方差](@entry_id:200758)恰好等于$\|G\|_{2}^2$ [@problem_id:2901535]。因此，$\mathcal{H}_2$范数量化了系统对持续随机扰动的放大程度。

#### 范数有限的条件

与$\mathcal{H}_\infty$范数不同，$\mathcal{H}_2$范数的有限性对系统提出了更严格的要求。为了使积分$\int_{-\infty}^{\infty} \|G(j\omega)\|_F^2 d\omega$收敛，被积函数必须在$\omega \to \infty$时趋于零。

我们已经知道$\lim_{\omega\to\infty} G(j\omega) = D$。因此，为了使[积分收敛](@entry_id:139742)，必须有$\lim_{\omega\to\infty} \|G(j\omega)\|_F^2 = \|D\|_F^2 = 0$，这当且仅当$D=0$时成立 [@problem_id:2711590] [@problem_id:2711615]。

因此，对于一个内部稳定的[LTI系统](@entry_id:271946)，其$\mathcal{H}_2$范数是有限的**当且仅当系统是严格真（strictly proper）的**。任何带有直接馈通项（$D \neq 0$）的系统，其$\mathcal{H}_2$范数都是无穷大的 [@problem_id:2711587]。

### 对比$\mathcal{H}_2$与$\mathcal{H}_\infty$：峰值 vs. 能量

$\mathcal{H}_2$和$\mathcal{H}_\infty$范数从不同角度刻画了系统的增益。$\mathcal{H}_\infty$关注的是频率响应的**峰值**，而$\mathcal{H}_2$关注的是[频率响应](@entry_id:183149)的**积分**（即总能量）。一个系统的$\mathcal{H}_\infty$范数可能很小，但如果其带宽很宽，它的$\mathcal{H}_2$范数可能会很大。反之，一个系统可能在某个狭窄的频带内有很高的[谐振峰](@entry_id:271281)（高$\mathcal{H}_\infty$范数），但由于[能量集中](@entry_id:203621)，其总能量（$\mathcal{H}_2$范数）可能并不大。

我们可以通过一个简单的例子来阐明这种差异 [@problem_id:2711591]。考虑一个一阶低通滤波器$G(s) = \frac{ka}{s+a}$，其中$k, a > 0$。
其$\mathcal{H}_\infty$范数是[直流增益](@entry_id:267449)，即：
$$
\\|G\\|_{\infty} = \sup_{\omega} \left| \frac{ka}{j\omega+a} \right| = \frac{ka}{\sqrt{\omega^2+a^2}} \bigg|_{\omega=0} = k
$$
其$\mathcal{H}_2$范数可通过计算脉冲响应$g(t) = ka e^{-at}$的能量得到：
$$
\\|G\\|_{2}^2 = \int_0^{\infty} (ka e^{-at})^2 dt = k^2 a^2 \int_0^{\infty} e^{-2at} dt = k^2 a^2 \left[ \frac{e^{-2at}}{-2a} \right]_0^{\infty} = \frac{k^2 a}{2} \implies \\|G\\|_{2} = k \sqrt{\frac{a}{2}}
$$
现在，我们比较两个系统：
$G_1(s)$：$k_1=2, a_1=1$ $\implies \\|G_1\\|_{\infty} = 2, \\|G_1\\|_{2} = 2\sqrt{1/2} = \sqrt{2}$
$G_2(s)$：$k_2=1.5, a_2=4$ $\implies \\|G_2\\|_{\infty} = 1.5, \\|G_2\\|_{2} = 1.5\sqrt{4/2} = 1.5\sqrt{2}$

比较范数值：
$\mathcal{H}_\infty$范数：$\\|G_1\\|_{\infty} = 2 > \\|G_2\\|_{\infty} = 1.5$
$\mathcal{H}_2$范数：$\\|G_1\\|_{2} = \\sqrt{2} \approx 1.414  \\|G_2\\|_{2} = 1.5\sqrt{2} \approx 2.121$

这个例子清晰地表明，系统$G_1$具有更高的峰值增益（对特定低频输入的放大能力更强），而系统$G_2$尽管峰值增益较低，但由于其更宽的带宽（由更大的$a_2$决定），其对脉冲或白噪声的总能量放大作用更强。因此，根据我们是更关心抑制最坏情况下的谐波扰动（选择$\mathcal{H}_\infty$）还是抑制宽带随机扰动（选择$\mathcal{H}_2$），对这两个系统的“优劣”排序会截然相反。

### 状态空间计算方法

虽然范数定义在时域或[频域](@entry_id:160070)，但通过系统的状态空间模型$(A,B,C,D)$可以更高效地进行计算。

#### $\mathcal{H}_2$范数的计算

对于一个稳定的、严格真的系统（$A$是Hurwitz矩阵，$D=0$），其$\mathcal{H}_2$范数的平方可以通过求解**[Lyapunov方程](@entry_id:165178)**得到 [@problem_id:2711590] [@problem_id:2713825]。
$$
\\|G\\|_{2}^2 = \mathrm{tr}(C P C^T) = \mathrm{tr}(B^T Q B)
$$
其中，$P$和$Q$分别是**可控性Gramian**和**可观性Gramian**，它们是以下[Lyapunov方程](@entry_id:165178)的唯一半正定解：
可控性[Lyapunov方程](@entry_id:165178): $A P + P A^T + B B^T = 0$
可观性[Lyapunov方程](@entry_id:165178): $A^T Q + Q A + C^T C = 0$

这个公式将范数的计算从一个无限积分问题转化为一个[线性矩阵方程](@entry_id:203443)的求解问题，这在计算上要高效得多。

例如，对于由以下矩阵指定的[MIMO系统](@entry_id:268566) [@problem_id:2713825]：
$$
A=\\begin{bmatrix} -1  0  0 \\\\ 0  -2  0 \\\\ 0  0  -3 \\end{bmatrix},\\quad B=\\begin{bmatrix} 1  0 \\\\ 0  1 \\\\ 1  1 \\end{bmatrix},\\quad C=\\begin{bmatrix} 1  0  1 \\\\ 0  1  1 \\end{bmatrix}
$$
我们可以首先求解[可控性](@entry_id:148402)[Lyapunov方程](@entry_id:165178)$A X+X A^{T}+B B^{T}=0$得到$X=P$。由于$A$是对角的，方程可以逐元素求解，得到：
$$
X = \\begin{bmatrix} \\frac{1}{2}  0  \\frac{1}{4} \\\\ 0  \\frac{1}{4}  \\frac{1}{5} \\\\ \\frac{1}{4}  \\frac{1}{5}  \\frac{1}{3} \\end{bmatrix}
$$
然后，计算$\mathcal{H}_2$范数的平方：
$$
\\|G\\|_{2}^2 = \\mathrm{tr}(C X C^T) = \\mathrm{tr}\\left( \\begin{bmatrix} \\frac{16}{12}  \\dots \\\\ \\dots  \\frac{59}{60} \\end{bmatrix} \\right) = \\frac{4}{3} + \\frac{59}{60} = \\frac{139}{60}
$$
因此，$\mathcal{H}_2$范数为$\sqrt{139/60} \approx 1.522$。

#### $\mathcal{H}_\infty$范数的计算

$\mathcal{H}_\infty$范数的计算通常更为复杂，没有像$\mathcal{H}_2$范数那样的闭式解析解。它通常需要通过迭代算法来求解，例如，通过**$\gamma$-迭代**。该方法基于一个重要定理：$\|G\|_{\infty}  \gamma$当且仅当某个与$G$和$\gamma$相关的Hamiltonian矩阵在虚轴上没有[特征值](@entry_id:154894)。通过对$\gamma$进行二分搜索，可以以任意精度逼近$\mathcal{H}_\infty$范数。

### 扩展与探讨

#### [离散时间系统](@entry_id:263935)

$\mathcal{H}_2$和$\mathcal{H}_\infty$的概念可以自然地推广到离散时间系统$G(z)$。此时，我们关注的是[单位圆](@entry_id:267290)上的频率响应$G(e^{j\omega})$。

-   $\mathcal{H}_\infty$范数定义为$\sup_{\omega \in [-\pi, \pi]} \bar{\sigma}(G(e^{j\omega}))$，其物理意义（诱导$\ell_2$增益）保持不变 [@problem_id:2711600]。
-   $\mathcal{H}_2$范数定义变为$\left( \frac{1}{2\pi} \int_{-\pi}^{\pi} \mathrm{tr}(G(e^{j\omega})^* G(e^{j\omega})) d\omega \right)^{1/2}$，等价于脉冲响应序列的能量$\sum_{k=0}^{\infty} \|h[k]\|_F^2$ [@problem_id:2711600]。
-   [状态空间](@entry_id:177074)计算公式中的[Lyapunov方程](@entry_id:165178)被替换为相应的**离散Lyapunov（Stein）方程**。例如，[可控性](@entry_id:148402)Gramian $P$满足$A P A^T - P + B B^T = 0$。
-   一个重要的区别是，在[离散时间系统](@entry_id:263935)中，即使$D \neq 0$，$\mathcal{H}_2$范数也可以是有限的。这是因为离散脉冲$h[0]=D$的$\ell_2$能量是有限的（即$\|D\|_F^2$），不像连续时间狄拉克$\delta$函数那样能量无穷大 [@problem_id:2711600]。

#### 内部稳定性与外部稳定性

$\mathcal{H}_2$和$\mathcal{H}_\infty$范数是定义在[传递函数](@entry_id:273897)$G(s)$上的，因此它们是系统**输入-输出**（外部）特性的度量。一个系统的内部状态矩阵$A$可能是不稳定的（非Hurwitz），但由于**极点-零点对消**，其[传递函数](@entry_id:273897)$G(s)$可能是稳定的。这种对消发生在[不稳定模式](@entry_id:263056)是不可控或不可观的时候 [@problem_id:2711587]。在这种情况下，只要$G(s)$本身是稳定且（严格）真的，其范数就可以是有限的。然而，这种系统在物理上是**内部不稳定**的。尽管从输入到输出的映射是有界的，但系统内部的某些状态会发散。因此，在实际应用中，我们不仅要求系统范数有限，更要求其实现是内部稳定的。