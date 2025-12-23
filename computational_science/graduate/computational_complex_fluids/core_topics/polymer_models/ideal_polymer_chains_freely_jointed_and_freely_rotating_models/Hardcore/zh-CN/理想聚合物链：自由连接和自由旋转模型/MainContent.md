## 引言
要理解从塑料瓶到DNA等高分子材料的宏观行为，我们必须深入其微观世界，探索构成它们的长链分子的统计特性。然而，[真实聚合物链](@entry_id:1130709)的复杂性——包含成千上万个原子，并受到复杂的相互作用——使得直接分析几乎不可能。因此，物理学家们发展了一系列简化模型来捕捉其本质行为，其中，**理想高分子链模型**构成了我们理论工具库的基石。这些模型通过战略性地忽略某些次要因素（如链段的体积），使我们能够运用统计力学的强大工具，精确求解链的尺寸、形状和力学响应，从而揭示支配其行为的[普适性原理](@entry_id:137218)。

本文将系统地引导你探索两种最基础、最重要的[理想链](@entry_id:196640)模型。你将学到：

*   **第一章：原理与机制** 将深入剖析[自由连接链](@entry_id:169847)（FJC）和[自由旋转链](@entry_id:181494)（FRC）的定义与统计力学基础。我们将推导它们的核心性质，如[均方末端距](@entry_id:156813)，并解释键角约束如何引入“[记忆效应](@entry_id:266709)”，最终引出[库恩长度](@entry_id:148526)和[持久长度](@entry_id:148195)等关键的[粗粒化](@entry_id:141933)概念。

*   **第二章：应用与交叉学科联系** 将展示这些看似抽象的模型如何在[热力学](@entry_id:172368)、材料科学和[生物物理学](@entry_id:154938)中发挥作用。你将看到[理想链](@entry_id:196640)如何解释[熵弹性](@entry_id:151071)的奥秘，如何用于表征复杂拓扑结构，以及如何与[散射实验](@entry_id:173304)数据建立联系。

*   **第三章：动手实践** 将通过一系列精心设计的计算问题，让你将理论知识付诸实践。你将从头推导模型的关键统计量，并学习如何数值化地处理力-伸长关系，将理论模型与实际数据分析联系起来。

通过这趟旅程，你将建立起对高分子统计物理的坚实理解，从最简单的[随机游走模型](@entry_id:180803)出发，逐步迈向对复杂软物质系统的深刻洞见。让我们首先进入第一章，揭开[理想链](@entry_id:196640)的神秘面纱。

## 原理与机制

在[聚合物物理学](@entry_id:145330)领域，为了从分子层面理解长链分子的宏观性质，我们必须建立能够捕捉其统计行为的简化模型。[理想链](@entry_id:196640)模型构成了这一理论体系的基石。正如其名，“理想”一词意味着我们忽略了现实世界中的诸多复杂性，以便专注于最核心的物理原理。在本章中，我们将系统地探讨两种最基本也是最重要的[理想链](@entry_id:196640)模型：[自由连接链](@entry_id:169847)（Freely-Jointed Chain, FJC）和[自由旋转链](@entry_id:181494)（Freely-Rotating Chain, FRC），并阐明它们背后的统计力学原理与机制。

### 何谓“[理想链](@entry_id:196640)”？

在深入模型细节之前，我们必须首先精确定义“[理想链](@entry_id:196640)”的内涵。在统计力学语境下，一条链被称为**[理想链](@entry_id:196640)**（ideal chain），指的是我们忽略了两种主要的分子内相互作用 ：

1.  **排斥体积相互作用（Excluded-Volume Interactions）**：在真实聚合物中，两个非键合的链段不能占据空间中的同一点。这种无处不在的短程排斥力被称为排斥体积效应。在[理想链](@entry_id:196640)模型中，我们完全忽略了这种效应，允许链段自由地相互穿越。这等效于假设链是“幻影”（phantom），没有任何体积。

2.  **非键合链段间的能量相互作用（Non-bonded Intrachain Energetic Interactions）**：[真实链](@entry_id:185668)段之间除了排斥体积外，还存在范德华力、静电力等长程或短程的能量相互作用。在[理想链](@entry_id:196640)模型中，我们假设这些相互作用不存在，或者它们与溶剂分子之间的相互作用精确地相互抵消。这种情况在物理上对应于所谓的**[θ溶剂](@entry_id:182788)（theta solvent）**条件，此时链的行为如同没有非[键合相互作用](@entry_id:746909)一样。

因此，[理想链](@entry_id:196640)的总构型能量 $U(\{\mathbf{b}_i\})$ 完全由其**局域[共价结构](@entry_id:190662)**所决定的约束（例如，固定的[键长](@entry_id:144592)、键角）来定义。任何超出这些基本[化学键](@entry_id:145092)合约束的相互作用都被置为零。这种简化使得我们可以运用强大的统计力学工具来精确求解模型的性质。从统计力学角度看，一个构型 $\{\mathbf{b}_i\}$ 出现的[概率密度](@entry_id:175496)正比于其[玻尔兹曼权重](@entry_id:137515) $\exp[-U(\{\mathbf{b}_i\})/(k_{\mathrm{B}} T)]$ 。对于[理想链](@entry_id:196640)，能量函数 $U$ 的简化直接导致了构型统计的简化。

### [自由连接链](@entry_id:169847)（FJC）模型：最纯粹的随机游走

[自由连接链模型](@entry_id:192058)是[理想链](@entry_id:196640)概念最直接的体现。它被定义为由 $N$ 个刚性链段（或称“键”）组成的序列，每个链段的长度恒为 $b$。其核心假设是：

**所有键矢量 $\mathbf{b}_i$ 的取向在统计上是相互独立且各向同性的。**

这意味着一个键的指向与其任何一个邻居或更远的键的指向之间没有任何关联。每个键的取向在[单位球](@entry_id:142558)面上均匀分布  。

#### FJC 的统计性质与[均方末端距](@entry_id:156813)

这些定义直接导出了 FJC 的基本统计性质。由于每个键矢量 $\mathbf{b}_i$ 的取向是**各向同性（isotropic）**的，即指向空间中任何方向的概率都相同，其系综平均必然为[零矢量](@entry_id:155273)：
$$
\langle \mathbf{b}_i \rangle = \mathbf{0}
$$
这是因为对于任何一个可能的取向 $\mathbf{b}_i$，都存在一个等概率的相反取向 $-\mathbf{b}_i$，它们在矢量平均中相互抵消。

更重要的是，由于键与键之间**统计独立（statistically independent）**，两个不同键矢量（$i \neq j$）的点积的平均值可以分解为它们各自平均值的点积 ：
$$
\langle \mathbf{b}_i \cdot \mathbf{b}_j \rangle = \langle \mathbf{b}_i \rangle \cdot \langle \mathbf{b}_j \rangle = \mathbf{0} \cdot \mathbf{0} = 0 \quad (\text{当 } i \neq j \text{ 时})
$$
这一结果是 FJC 模型的标志性特征：**所有非对角（或称“交叉”）的键-键相关项均为零** 。在统计力学上，这种独立性源于一个可分解的[总配分函数](@entry_id:190183)，其中总的[玻尔兹曼权重](@entry_id:137515)可以写成每个独立键的权重之积 。

这些性质使得计算聚合物尺寸的关键量度——**[均方末端距](@entry_id:156813)（mean-squared end-to-end distance）** $\langle R^2 \rangle$ 变得异常简单。末端矢量 $\mathbf{R}$ 定义为所有键矢量的总和，$\mathbf{R} = \sum_{i=1}^N \mathbf{b}_i$。其平方大小的平均值为：
$$
\langle R^2 \rangle = \langle \mathbf{R} \cdot \mathbf{R} \rangle = \left\langle \left( \sum_{i=1}^N \mathbf{b}_i \right) \cdot \left( \sum_{j=1}^N \mathbf{b}_j \right) \right\rangle = \sum_{i=1}^N \sum_{j=1}^N \langle \mathbf{b}_i \cdot \mathbf{b}_j \rangle
$$
我们可以将这个双[重求和](@entry_id:275405)分解为对角项（$i=j$）和非对角项（$i \neq j$）：
$$
\langle R^2 \rangle = \sum_{i=1}^N \langle \mathbf{b}_i \cdot \mathbf{b}_i \rangle + \sum_{i \neq j} \langle \mathbf{b}_i \cdot \mathbf{b}_j \rangle
$$
对于对角项，$\langle \mathbf{b}_i \cdot \mathbf{b}_i \rangle = \langle |\mathbf{b}_i|^2 \rangle = b^2$，因为[键长](@entry_id:144592)是固定的。对于非对角项，我们已经证明其为零。因此，求和中的非对角项全部消失，只剩下 $N$ 个对角项：
$$
\langle R^2 \rangle = \sum_{i=1}^N b^2 + 0 = N b^2
$$
这个著名的结果表明，FJC 的[均方末端距](@entry_id:156813)与链的长度（链段数 $N$）成正比。这与经典随机游走的结论一致，意味着聚合物链的特征尺寸（如[均方根](@entry_id:263605)[末端距](@entry_id:175986) $\sqrt{\langle R^2 \rangle}$）与 $N^{1/2}$ 成正比。

### [自由旋转链](@entry_id:181494)（FRC）模型：引入局域刚性

尽管 FJC 模型极具启发性，但它忽略了真实聚合物中一个重要的化学现实：由[共价键](@entry_id:146178)的电子轨道杂化决定的**固定键角**。[自由旋转链](@entry_id:181494)（FRC）模型通过引入这一约束，向更真实的情景迈进了一步。

FRC 模型的定义如下  ：
1.  链由 $N$ 个长度为 $b$ 的刚性键组成。
2.  任意**相邻**的两个键 $\mathbf{b}_i$ 和 $\mathbf{b}_{i+1}$ 之间的夹角被固定为一个常数 $\theta$。
3.  绕键轴的**扭转角（torsional angle）**是自由的，即在 $[0, 2\pi)$ 区间内均匀分布。

重要的是，FRC 仍然是一个“[理想链](@entry_id:196640)”模型，因为它依旧忽略排斥体积和非键合链段间的[长程相互作用](@entry_id:140725) 。新增的约束只是一个局域的、由键合结构决定的能量项。

#### FRC 的键-键相关性：指数衰减的记忆

固定的键角约束彻底改变了模型的统计性质。键与键之间不再是相互独立的。对于相邻的键，其点积的平均值不再为零：
$$
\langle \mathbf{b}_i \cdot \mathbf{b}_{i+1} \rangle = b^2 \cos \theta
$$
这个非零的相关性会在链上传播。为了量化这种传播，我们考虑相隔 $s = |i-j|$ 个键的两个矢量 $\mathbf{b}_i$ 和 $\mathbf{b}_j$ 之间的相关性。我们可以通过对扭转角的平均来推导出一个[递推关系](@entry_id:189264)。给定键矢量 $\mathbf{b}_{k-1}$，下一个键矢量 $\mathbf{b}_k$ 的取向位于一个以 $\mathbf{b}_{k-1}$ 为轴、半角为 $\theta$ 的圆锥面上。由于扭转角是均匀分布的，$\mathbf{b}_k$ 垂直于 $\mathbf{b}_{k-1}$ 的分量在平均后为零。因此，$\mathbf{b}_k$ 在给定 $\mathbf{b}_{k-1}$ 下的条件平均值沿着 $\mathbf{b}_{k-1}$ 方向，其大小为 $b \cos \theta$ ：
$$
\langle \mathbf{b}_k | \mathbf{b}_{k-1} \rangle = (\cos \theta) \mathbf{b}_{k-1}
$$
利用这个关系，我们可以计算 $\langle \mathbf{b}_i \cdot \mathbf{b}_{i+s} \rangle$：
$$
\langle \mathbf{b}_i \cdot \mathbf{b}_{i+s} \rangle = \langle \mathbf{b}_i \cdot \langle \mathbf{b}_{i+s} | \mathbf{b}_{i+s-1} \rangle \rangle = \langle \mathbf{b}_i \cdot ((\cos \theta) \mathbf{b}_{i+s-1}) \rangle = \cos \theta \langle \mathbf{b}_i \cdot \mathbf{b}_{i+s-1} \rangle
$$
这是一个[递推关系](@entry_id:189264)，其解为：
$$
\langle \mathbf{b}_i \cdot \mathbf{b}_j \rangle = b^2 (\cos \theta)^{|i-j|}
$$
这个结果意义深远  。它表明键取向的相关性（或“记忆”）随着它们在链上间隔的增加而**指数衰减**。每经过一个键，相关性就乘以一个因子 $\cos \theta$（由于 $0  \theta  \pi$，所以 $|\cos \theta|  1$）。这种指数衰减行为是具有局域刚性但无[长程相互作用](@entry_id:140725)的链状分子的一个普适特征。

从一个更高等的角度看，这种[几何级数](@entry_id:158490)的衰减可以理解为键取向[演化过程](@entry_id:175749)的传递算符的[本征值问题](@entry_id:142153)。键-键[相关函数](@entry_id:146839)对应于[球谐函数展开](@entry_id:188485)的第一阶（$l=1$）模态，其单步演化的本征值恰好是勒让德多项式 $P_1(\cos \theta) = \cos \theta$ 。经过 $s$ 步后，这个因子就变成了 $(\cos \theta)^s$。

#### FRC 的[均方末端距](@entry_id:156813)

由于 FRC 中存在非零的键-键相关性，其 $\langle R^2 \rangle$ 的计算比 FJC 复杂。我们需要对所有相关项求和：
$$
\langle R^2 \rangle = \sum_{i,j} \langle \mathbf{b}_i \cdot \mathbf{b}_j \rangle = b^2 \sum_{i,j} (\cos \theta)^{|i-j|} = N b^2 + 2b^2 \sum_{s=1}^{N-1} (N-s) (\cos\theta)^s
$$
这个求和形式  是精确的，但形式上比较繁琐。通过对[几何级数](@entry_id:158490)求和，可以得到一个等价的、更紧凑的精确封闭表达式  ：
$$
\langle R^2 \rangle = N b^2 \frac{1 + \cos \theta}{1 - \cos \theta} - \frac{2 b^2 \cos \theta [1 - (\cos \theta)^N]}{(1 - \cos \theta)^2}
$$
这个公式对任意有限的 $N$ 都成立。

#### 特殊极限：FRC 如何回归 FJC？

FRC 模型包含一个参数 $\theta$，调节它可以改变链的局域刚性。一个自然的问题是，FRC 模型在何种条件下会退化为更简单的 FJC 模型？
从[相关函数](@entry_id:146839) $\langle \mathbf{b}_i \cdot \mathbf{b}_j \rangle = b^2 (\cos \theta)^{|i-j|}$ 可以看出，要使所有 $i \neq j$ 的相关项都为零（FJC 的标志），我们必须要求 $\cos \theta = 0$。这对应于一个特定的键角 $\theta = \pi/2$。
当 $\theta = \pi/2$ 时：
*   所有相关项 $\langle \mathbf{b}_i \cdot \mathbf{b}_j \rangle$ 对 $i \neq j$ 均等于零。
*   $\langle R^2 \rangle$ 的精确公式退化为 $\langle R^2 \rangle = N b^2 \frac{1+0}{1-0} - 0 = N b^2$。

因此，当键角为直角时，FRC 模型在二阶统计矩（即涉及两个键矢量的平均值）的层面上与 FJC 模型完全等价 。

### [粗粒化](@entry_id:141933)与普适性：[库恩长度](@entry_id:148526)与[持久长度](@entry_id:148195)

尽管 FRC 的精确公式很优美，但在处理非常长的链（$N \to \infty$）时，我们希望能有一个更简单的描述。这引出了**[粗粒化](@entry_id:141933)（coarse-graining）**和**普适性（universality）**的概念：在远大于局域细节（如单个[键长](@entry_id:144592)和键角）的尺度上，聚合物链的统计行为是否会趋向于一个更简单的、普适的形式？答案是肯定的。

#### [库恩长度](@entry_id:148526) $b_K$

对于一个非常长的 FRC 链（$N \to \infty$），由于 $(\cos \theta)^N \to 0$，其[均方末端距](@entry_id:156813)的表达式渐近于：
$$
\langle R^2 \rangle_{\text{FRC}} \approx N b^2 \frac{1 + \cos \theta}{1 - \cos \theta} \quad (\text{当 } N \gg 1 \text{ 时})
$$
这个结果表明，即使存在局域相关性，长链的 $\langle R^2 \rangle$ 仍然与 $N$ 成正比 。这启发我们将一个具有局域刚性的“真实”链（如 FRC）等效为一个更长的 FJC。这个等效的 FJC 由 $N_K$ 个“**库恩链段（Kuhn segments）**”组成，每个链段的长度为**[库恩长度](@entry_id:148526)（Kuhn length）** $b_K$。
这种等效映射要求两个条件：
1.  总轮廓长度（contour length）保持不变：$L = N b = N_K b_K$。
2.  [均方末端距](@entry_id:156813)相同：$\langle R^2 \rangle_{\text{等效 FJC}} = N_K b_K^2$。

联立这两个方程，我们得到 $\langle R^2 \rangle_{\text{等效 FJC}} = (Nb/b_K) b_K^2 = N b b_K$。将其与 FRC 的渐近结果进行比较：
$$
N b b_K = N b^2 \frac{1 + \cos \theta}{1 - \cos \theta}
$$
解出[库恩长度](@entry_id:148526) $b_K$  ：
$$
b_K = b \frac{1 + \cos \theta}{1 - \cos \theta}
$$
[库恩长度](@entry_id:148526) $b_K$ 可以被视为一个统计上独立的链段的有效长度。它将所有复杂的局域相互作用（在此即键角约束）“打包”进一个单一的参数中。对于 FJC 本身，由于键已经是独立的，其[库恩长度](@entry_id:148526)就是键长 $b$。这个概念极其强大，因为它揭示了一个深刻的[普适性原理](@entry_id:137218)：在足够大的尺度上，许多不同细节的[理想链](@entry_id:196640)模型都表现得像一个简单的[自由连接链](@entry_id:169847) 。

#### [持久长度](@entry_id:148195) $l_p$

**[持久长度](@entry_id:148195)（persistence length）** $l_p$ 是另一个衡量链刚性的关键参数，它自然地出现在连续链模型——**[蠕虫状链](@entry_id:193777)（Worm-like Chain, WLC）**中。在 WLC 模型中，切向矢量 $\mathbf{t}(s)$ 的相关性沿轮廓长度 $s$ 呈指数衰减：$\langle \mathbf{t}(s) \cdot \mathbf{t}(0) \rangle = \exp(-s/l_p)$。
我们可以通过将离散的 FRC 模型与连续的 WLC 模型进行匹配来确定 FRC 的[持久长度](@entry_id:148195)。我们将 FRC 的相关函数 $g(s) = \langle \hat{\mathbf{b}}_i \cdot \hat{\mathbf{b}}_{i+s} \rangle = (\cos\theta)^s$ 中的离散间隔 $s$ 对应于连续轮廓长度 $s \cdot b$  ：
$$
(\cos\theta)^s = \exp(-sb/l_p)
$$
对两边取自然对数，得到 $s \ln(\cos\theta) = -sb/l_p$，由此解出[持久长度](@entry_id:148195)：
$$
l_p = - \frac{b}{\ln(\cos\theta)}
$$
从 WLC 的定义可知，$l_p$ 的物理意义是：**链的切向矢量相关性衰减到其初始值的 $1/e$ 时所经过的轮廓长度** 。它直接量化了链的取向“记忆”能持续多远。当键角 $\theta$ 很小时，链非常刚硬，我们可以用[泰勒展开](@entry_id:145057)得到一个非常有用的近似：$l_p \approx 2b/\theta^2$ 。

### 从离散游走到[连续路径](@entry_id:187361)：[高斯链](@entry_id:154876)与[路径积分](@entry_id:165167)

到目前为止，我们主要关注的是二阶统计矩，如 $\langle R^2 \rangle$。一个更完整的问题是：整个末端矢量 $\mathbf{R}$ 的概率分布 $P(\mathbf{R})$ 是什么形式？

对于 FJC，末端矢量 $\mathbf{R}$ 是一系列[独立同分布](@entry_id:169067)（i.i.d.）的随机矢量 $\mathbf{b}_i$ 的和。根据**[中心极限定理](@entry_id:143108)（Central Limit Theorem, CLT）**，当 $N$ 很大时，这个和的概率分布将趋近于一个高斯分布（正态分布）。需要强调的是，这是一个**渐近**结论，对于任何**有限**的 $N$，其精确分布并非高斯分布 。例如，对于 $N=1$，$\mathbf{R}$ 的末端均匀分布在半径为 $b$ 的球壳上，这与高斯分布迥然不同。

对于 FRC，尽管键矢量不是独立的，但它们的关联是短程的（指数衰减）。广义的中心极限定理同样适用，因此对于大的 $N$，FRC 的末端矢量分布也趋近于高斯分布 。

这一高斯特性是通往聚合物的**路径积分（path integral）**表述的桥梁。考虑一个[连续极限](@entry_id:162780)，其中链段数 $N \to \infty$，键长 $b \to 0$，同时保持总轮廓长度 $L=Nb$ 不变。在这个极限下，离散的随机游走变成了一条连续的随机路径 $\mathbf{r}(s)$，其中 $s \in [0,L]$。
中心极限定理不仅适用于整个链，也适用于链的任意一个宏观部分。路径上的一个增量 $\Delta\mathbf{r} = \mathbf{r}(s_2) - \mathbf{r}(s_1)$ 是大量微小键矢量的和，因此它也服从高斯分布，其方差正比于轮廓长度的增量 $\Delta s = s_2 - s_1$。不同区间上的增量是相互独立的。一个具有平稳、独立高斯增量的连续[随机过程](@entry_id:268487)，正是**[维纳过程](@entry_id:137696)（Wiener process）**（或称布朗运动）的定义。

因此，在[连续极限](@entry_id:162780)下，FJC 模型（以及所有具有[短程关联](@entry_id:158693)的[理想链](@entry_id:196640)模型，如 FRC）都收敛到一个普适的**[高斯链](@entry_id:154876)（Gaussian chain）**模型。描述所有可能[连续路径](@entry_id:187361) $\mathbf{r}(s)$ 的[概率测度](@entry_id:190821)被称为**[维纳测度](@entry_id:189476)（Wiener measure）** 。如果我们还额外施加约束，例如固定链的两个端点 $\mathbf{r}(0)$ 和 $\mathbf{r}(L)$，那么这个条件化的测度就变成了所谓的**[布朗桥](@entry_id:265208)（Brownian bridge）** 。

### 应用：FJC 模型的[熵弹性](@entry_id:151071)

[理想链](@entry_id:196640)模型不仅能描述聚合物的静态尺寸，还能解释其对外部机械力的响应，这便是**[熵弹性](@entry_id:151071)（entropic elasticity）**的起源。

考虑一个 FJC 链，其两端被一个恒定的拉力 $f$ 沿 $z$ 轴方向拉伸 。这个外[力场](@entry_id:147325)会给每个链段带来一个与其取向相关的势能 $U_i = - \mathbf{f} \cdot \mathbf{b}_i = - f b \cos\theta_i$，其中 $\theta_i$ 是第 $i$ 个键与[力场](@entry_id:147325)方向的夹角。

根据统计力学，构型的概率现在由[玻尔兹曼因子](@entry_id:141054) $\exp[-U_i/(k_{\mathrm{B}}T)] = \exp(\beta f b \cos\theta_i)$ 加权，其中 $\beta = 1/(k_{\mathrm{B}}T)$。外力倾向于使链段沿其方向排列（$\cos\theta_i \to 1$），从而降低体系的能量。然而，这种排列会减少系统可及的构型数目，即降低了**构型熵（configurational entropy）**。聚合物的响应正是在最小化能量和最大化熵之间的平衡。值得注意的是，这种弹性完全源于熵的贡献，与改变[键长](@entry_id:144592)或键角的**焓弹性**（energetic elasticity）无关 。

由于 FJC 中的链段是独立的，我们可以通过计算单个链段的[配分函数](@entry_id:140048) $z_1$ 来求解整个链的性质。通过对所有取向进行积分，可以得到链的平均伸长量 $R$ 是力的[非线性](@entry_id:637147)函数：
$$
\frac{R}{Nb} = \coth\left(\frac{fb}{k_{\mathrm{B}}T}\right) - \frac{k_{\mathrm{B}}T}{fb} \equiv \mathcal{L}\left(\frac{fb}{k_{\mathrm{B}}T}\right)
$$
这里的 $\mathcal{L}(x)$ 是著名的**郎之万函数（Langevin function）**。这条[力-伸长曲线](@entry_id:198766)展现了两个截然不同的物理区域 ：

1.  **[弱力](@entry_id:152942)区（$fb \ll k_{\mathrm{B}}T$）**：此时，热扰动占主导，链段近乎随机取向。郎之万函数可以近似为 $\mathcal{L}(x) \approx x/3$。伸长量与力呈线性关系 $R \approx (Nb^2 / (3k_{\mathrm{B}}T))f$。这正是胡克定律的形式，其[有效弹簧常数](@entry_id:171743) $K_{\text{eff}} = 3k_{\mathrm{B}}T / (Nb^2)$ 与温度成正比，与链长成反比。这表明链的抵抗力完全来自熵。

2.  **强力区（$fb \gg k_{\mathrm{B}}T$）**：此时，外力占主导，几乎所有链段都被拉直。郎之万函数趋近于 1，链的伸长量 $R$ 饱和于其最大轮廓长度 $Nb$。这个上限是一个纯粹的几何约束，而非能量壁垒。

这种从线性响应到[非线性饱和](@entry_id:1128869)的行为是[熵弹性](@entry_id:151071)的典型特征，也是 FJC 模型最成功的应用之一。它为橡胶等高分子材料的弹性行为提供了基本的分[子图](@entry_id:273342)像。