## 引言
在[材料力学](@entry_id:201885)和固体力学领域，理解材料如何响应外力是所有分析与设计的基石。这种响应的核心在于[本构关系](@entry_id:186508)——即连接应力与应变的数学定律。对于[线性弹性](@entry_id:166983)材料，[广义胡克定律](@entry_id:203555)通过一个四阶[刚度张量](@entry_id:176588)精确地描述了这种关系。然而，这个拥有81个分量的张量在实际工程计算中显得异常繁琐和不直观，构成了理论与应用之间的一道鸿沟。

本文旨在系统地解决这一问题，深入探讨一种强大而高效的简化工具：福伊特（Voigt）记法。通过这种方法，复杂的张量运算可以被转化为更为人熟知的矩阵代数。我们将带领读者穿越理论的深处，揭示这一强大工具的精髓。在“原理与机制”一章中，我们将从第一性原理出发，阐明如何将张量转化为矩阵，批判性地审视其中至关重要的约定，并展示如何根据[材料对称性](@entry_id:190289)构建不同形式的刚度与[柔度矩阵](@entry_id:185679)，最终将其与[材料稳定性](@entry_id:183933)的物理基础联系起来。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这一理论框架如何应用于现实世界，从实验中的[材料表征](@entry_id:161346)，到[复合材料](@entry_id:139856)的设计，再到有限元等[数值模拟](@entry_id:137087)的核心。最后，“动手实践”部分将提供具体的计算问题，帮助读者巩固所学知识。

通过学习本文，您将不仅掌握一种数学技巧，更将获得一个贯穿[连续介质力学](@entry_id:155125)、[材料科学](@entry_id:152226)和计算工程的统一视角，为解决更前沿的力学问题打下坚实的基础。

## 原理与机制

在[线性弹性](@entry_id:166983)理论的框架内，材料的[本构关系](@entry_id:186508)——即[应力与应变](@entry_id:137374)之间的关系——是核心。虽然四阶[刚度张量](@entry_id:176588) $C_{ijkl}$ 以其最完整的形式捕捉了这种关系，但在实际工程计算和分析中，其表示形式显得相当繁琐。本章旨在阐明一种更为简洁和实用的[矩阵表示法](@entry_id:190318)，即 **Voigt 记法**。我们将从其基本原理出发，系统地探讨其不同的约定、构建方法，及其在不同[材料对称性](@entry_id:190289)下的具体形式。最终，我们将把这种数学工具与[材料稳定性](@entry_id:183933)的基本物理原理联系起来。

### 从张量到矩阵：Voigt记法的原理

对于一个[线性弹性](@entry_id:166983)体，在小应变假设下，柯西应力张量 $\boldsymbol{\sigma}$ 和[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon}$ 之间的关系由[广义胡克定律](@entry_id:203555)描述：
$$
\sigma_{ij} = C_{ijkl} \varepsilon_{kl}
$$
其中 $C_{ijkl}$ 是四阶[刚度张量](@entry_id:176588)。由于[应力张量](@entry_id:148973) ($\sigma_{ij} = \sigma_{ji}$) 和[应变张量](@entry_id:193332) ($\varepsilon_{ij} = \varepsilon_{ji}$) 都是对称的二阶张量，它们各自只有 6 个独立分量。这就启发我们将它们表示为 6 维列向量。例如，[应力张量](@entry_id:148973) $\begin{pmatrix} \sigma_{11}  \sigma_{12}  \sigma_{13} \\ \sigma_{21}  \sigma_{22}  \sigma_{23} \\ \sigma_{31}  \sigma_{32}  \sigma_{33} \end{pmatrix}$ 可以被压缩成一个向量形式 $\boldsymbol{\sigma}_V$。

相应地，拥有 $3^4 = 81$ 个分量的四阶[刚度张量](@entry_id:176588)，由于其内在的对称性（主对称性 $C_{ijkl} = C_{klij}$ 和次对称性 $C_{ijkl} = C_{ijlk} = C_{jikl}$），其独立分量最多为 21 个。这种对称结构使得将[四阶张量](@entry_id:181350) $C_{ijkl}$ 重新[排列](@entry_id:136432)为一个 $6 \times 6$ 的对称矩阵 $\mathbf{C}_V$ 成为可能。这样，张量形式的胡克定律就可以转化为一个更为直观的[矩阵方程](@entry_id:203695)：
$$
\boldsymbol{\sigma}_V = \mathbf{C}_V \boldsymbol{\varepsilon}_V
$$
这种从张量到向量和矩阵的转换过程，即为 **Voigt 记法** 或 **Voigt 表示法**。它将复杂的张量运算简化为标准的线性代数运算，极大地便利了数值计算和工程应用。然而，这种简化并非没有代价，其背后隐藏着一些必须仔细处理的约定和细节。

### Voigt记法的约定：一个批判性审视

将张量关系转化为矩阵形式需要建立明确的映射规则，而这些规则并非唯一。错误或不一致的约定是导致弹性力学计算中常见错误的根源。因此，我们必须对这些约定进行批判性的审视。

#### 应变向量：张量[剪应变](@entry_id:175241)与工程[剪应变](@entry_id:175241)

一个核心的约定在于应变向量的定义。考虑两种常见的定义方式：

- **张量[剪应变](@entry_id:175241)向量** $\boldsymbol{\varepsilon}^{(t)}$：直接堆叠[应变张量](@entry_id:193332)的独立分量，例如 $\boldsymbol{\varepsilon}^{(t)} = [\varepsilon_{11}, \varepsilon_{22}, \varepsilon_{33}, \varepsilon_{23}, \varepsilon_{13}, \varepsilon_{12}]^{\mathsf{T}}$。
- **工程[剪应变](@entry_id:175241)向量** $\boldsymbol{\varepsilon}^{(e)}$：在剪切分量上使用工程[剪应变](@entry_id:175241) $\gamma_{ij} = 2\varepsilon_{ij}$（$i \neq j$），例如 $\boldsymbol{\varepsilon}^{(e)} = [\varepsilon_{11}, \varepsilon_{22}, \varepsilon_{33}, \gamma_{23}, \gamma_{13}, \gamma_{12}]^{\mathsf{T}}$。

这两种定义之间的选择对刚度矩阵的最终形式有深远影响。要理解其根本原因，我们必须回到一个不应随表示法改变的物理量：[应变能密度](@entry_id:200085) $W$ 或其增量——[功率密度](@entry_id:194407) $p$。在张量形式中，[功率密度](@entry_id:194407)为 $p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} = \sigma_{ij} \dot{\varepsilon}_{ij}$。利用对称性，我们展开得到：
$$
p = \sigma_{11}\dot{\varepsilon}_{11} + \sigma_{22}\dot{\varepsilon}_{22} + \sigma_{33}\dot{\varepsilon}_{33} + 2\sigma_{23}\dot{\varepsilon}_{23} + 2\sigma_{13}\dot{\varepsilon}_{13} + 2\sigma_{12}\dot{\varepsilon}_{12}
$$
现在，让我们定义一个统一的应力向量 $\boldsymbol{\sigma}_V = [\sigma_{11}, \sigma_{22}, \sigma_{33}, \sigma_{23}, \sigma_{13}, \sigma_{12}]^{\mathsf{T}}$。如果我们希望[功率密度](@entry_id:194407)能简洁地表示为向量[内积](@entry_id:158127) $\boldsymbol{\sigma}_V^{\mathsf{T}} \dot{\boldsymbol{\varepsilon}}_V$，那么[应变率](@entry_id:154778)向量 $\dot{\boldsymbol{\varepsilon}}_V$ 必须是什么形式？
$$
\boldsymbol{\sigma}_V^{\mathsf{T}} \dot{\boldsymbol{\varepsilon}}_V = \sigma_{11}\dot{\varepsilon}_{V1} + \sigma_{22}\dot{\varepsilon}_{V2} + \sigma_{33}\dot{\varepsilon}_{V3} + \sigma_{23}\dot{\varepsilon}_{V4} + \sigma_{13}\dot{\varepsilon}_{V5} + \sigma_{12}\dot{\varepsilon}_{V6}
$$
将此式与[功率密度](@entry_id:194407)的[张量展开](@entry_id:755868)式进行比较，我们发现，为了使两者相等，应变率向量必须是 $\dot{\boldsymbol{\varepsilon}}_V = [\dot{\varepsilon}_{11}, \dot{\varepsilon}_{22}, \dot{\varepsilon}_{33}, 2\dot{\varepsilon}_{23}, 2\dot{\varepsilon}_{13}, 2\dot{\varepsilon}_{12}]^{\mathsf{T}}$。这恰恰对应于工程[剪应变](@entry_id:175241)向量的定义。

因此，采用工程[剪应变](@entry_id:175241) $\gamma_{ij}$ 的 **工程-Voigt 记法** 具有一个重要优点：它使得应力向量和应变向量在能量上是**共轭**的，即 $p = \boldsymbol{\sigma}_V^{\mathsf{T}} \dot{\boldsymbol{\varepsilon}}_V$ 且 $W = \frac{1}{2} \boldsymbol{\sigma}_V^{\mathsf{T}} \boldsymbol{\varepsilon}_V$。这种能量上的一致性使得基于工程[剪应变](@entry_id:175241)的 Voigt 表示法在许多应用中成为首选。

在两种表示法之间转换是可能的 [@problem_id:2918884]。从定义可知，$\boldsymbol{\varepsilon}^{(t)}$ 和 $\boldsymbol{\varepsilon}^{(e)}$ 之间的关系是线性的，可以表示为 $\boldsymbol{\varepsilon}^{(t)} = \mathbf{T} \boldsymbol{\varepsilon}^{(e)}$。通过保持功率表达式的[不变性](@entry_id:140168)，可以推导出对角变换算子 $\mathbf{T}$ 必须为：
$$
\mathbf{T} = \mathrm{diag}(1, 1, 1, \frac{1}{2}, \frac{1}{2}, \frac{1}{2}) = 
\begin{pmatrix}
1  0  0  0  0  0 \\
0  1  0  0  0  0 \\
0  0  1  0  0  0 \\
0  0  0  \frac{1}{2}  0  0 \\
0  0  0  0  \frac{1}{2}  0 \\
0  0  0  0  0  \frac{1}{2}
\end{pmatrix}
$$
这个算子明确了两种应变定义之间的转换关系，并为在不同文献或软件中遇到的不同形式的刚度矩阵之间进行转换提供了基础。**在后续的讨论中，除非特别说明，我们将统一采用能量共轭的工程-Voigt记法**。

#### 索引映射与排序

另一个约定是张量索引对 $(ij)$ 到 Voigt 索引（1到6）的具体映射。一个被广泛采用的映射是：
$$
(11) \leftrightarrow 1, \quad (22) \leftrightarrow 2, \quad (33) \leftrightarrow 3, \quad (23) \leftrightarrow 4, \quad (13) \leftrightarrow 5, \quad (12) \leftrightarrow 6
$$
然而，剪切分量的顺序可以改变。例如，另一个可行的排序是 $(11, 22, 33, 12, 23, 13)$。改变这个顺序会如何影响刚度矩阵？[@problem_id:2918828]

假设我们有两个变体，A 和 B，它们的 Voigt 向量仅因分量排序不同而异。我们可以定义一个[置换矩阵](@entry_id:136841) $\mathbf{P}_{B \leftarrow A}$，它通过行交换将 A 变体的向量重新排序为 B 变体的向量，即 $\boldsymbol{v}^{(B)} = \mathbf{P}_{B \leftarrow A} \boldsymbol{v}^{(A)}$。由于[应变能密度](@entry_id:200085) $W = \frac{1}{2} (\boldsymbol{\varepsilon}^{(V)})^{\mathsf{T}} \mathbf{C}_V \boldsymbol{\varepsilon}^{(V)}$ 是一个与表示法无关的物理标量，我们必须有：
$$
(\boldsymbol{\varepsilon}^{(A)})^{\mathsf{T}} \mathbf{C}^{(A)} \boldsymbol{\varepsilon}^{(A)} = (\boldsymbol{\varepsilon}^{(B)})^{\mathsf{T}} \mathbf{C}^{(B)} \boldsymbol{\varepsilon}^{(B)}
$$
将 $\boldsymbol{\varepsilon}^{(B)} = \mathbf{P} \boldsymbol{\varepsilon}^{(A)}$ 代入右侧（此处令 $\mathbf{P} \equiv \mathbf{P}_{B \leftarrow A}$），我们得到：
$$
(\boldsymbol{\varepsilon}^{(A)})^{\mathsf{T}} \mathbf{C}^{(A)} \boldsymbol{\varepsilon}^{(A)} = (\mathbf{P} \boldsymbol{\varepsilon}^{(A)})^{\mathsf{T}} \mathbf{C}^{(B)} (\mathbf{P} \boldsymbol{\varepsilon}^{(A)}) = (\boldsymbol{\varepsilon}^{(A)})^{\mathsf{T}} \mathbf{P}^{\mathsf{T}} \mathbf{C}^{(B)} \mathbf{P} \boldsymbol{\varepsilon}^{(A)}
$$
由于该等式对任意应变向量 $\boldsymbol{\varepsilon}^{(A)}$ 均成立，我们得到[刚度矩阵](@entry_id:178659)的变换法则：
$$
\mathbf{C}^{(A)} = \mathbf{P}^{\mathsf{T}} \mathbf{C}^{(B)} \mathbf{P} \quad \text{或者} \quad \mathbf{C}^{(B)} = \mathbf{P} \mathbf{C}^{(A)} \mathbf{P}^{\mathsf{T}}
$$
这是一个[相似变换](@entry_id:152935)，它本质上是对矩阵进行相应的行和列的[置换](@entry_id:136432)，以匹配向量分量的重新排序。例如，若 Variant A 采用 $(23, 13, 12) \to (4,5,6)$ 的顺序，而 Variant B 采用 $(12, 23, 13) \to (4,5,6)$ 的顺序，则[置换矩阵](@entry_id:136841)为：
$$
\mathbf{P}_{B \leftarrow A} = 
\begin{pmatrix}
1  0  0  0  0  0 \\
0  1  0  0  0  0 \\
0  0  1  0  0  0 \\
0  0  0  0  0  1 \\
0  0  0  1  0  0 \\
0  0  0  0  1  0
\end{pmatrix}
$$
这强调了在使用和比较文献中的刚度数据时，确认所使用的索引映射顺序的至关重要性。

### 刚度与[柔度矩阵](@entry_id:185679)的构建

在确立了明确的约定（工程[剪应变](@entry_id:175241)，以及标准的索引映射）之后，我们现在可以系统地构建 $6 \times 6$ 的 Voigt 矩阵。

#### 从张量到Voigt矩阵 ($C_{ijkl} \to C_V$)

我们的目标是找到 $6 \times 6$ 矩阵 $\mathbf{C}_V$ 的分量 $C_{IJ}$（其中 $I, J \in \{1, \dots, 6\}$），使得 $\boldsymbol{\sigma}_V = \mathbf{C}_V \boldsymbol{\varepsilon}_V$ 等价于 $\sigma_{ij} = C_{ijkl} \varepsilon_{kl}$。

我们从张量关系出发，展开对 $k, l$ 的求和，并利用应变[张量的对称性](@entry_id:202126) ($\varepsilon_{kl}=\varepsilon_{lk}$) 和[刚度张量](@entry_id:176588)的次对称性 ($C_{ijkl}=C_{ijlk}$):
$$
\sigma_{ij} = C_{ij11}\varepsilon_{11} + C_{ij22}\varepsilon_{22} + C_{ij33}\varepsilon_{33} + 2C_{ij23}\varepsilon_{23} + 2C_{ij13}\varepsilon_{13} + 2C_{ij12}\varepsilon_{12}
$$
现在，我们引入工程[剪应变](@entry_id:175241) $\gamma_{kl} = 2\varepsilon_{kl}$：
$$
\sigma_{ij} = C_{ij11}\varepsilon_{11} + C_{ij22}\varepsilon_{22} + C_{ij33}\varepsilon_{33} + C_{ij23}\gamma_{23} + C_{ij13}\gamma_{13} + C_{ij12}\gamma_{12}
$$
该式对任意应力分量 $\sigma_{ij}$ 均成立。我们可以通过将左侧的 $\sigma_{ij}$ 与右侧 $\boldsymbol{\varepsilon}_V$ 的分量进行匹配，来确定 $\mathbf{C}_V$ 的每一行。

- **Case 1: 正应力分量** ($\sigma_{11}, \sigma_{22}, \sigma_{33}$)
  以 $\sigma_{11}$ 为例 (Voigt 索引 $I=1$):
  $$
  \sigma_{11} = C_{1111}\varepsilon_{11} + C_{1122}\varepsilon_{22} + C_{1133}\varepsilon_{33} + C_{1123}\gamma_{23} + C_{1113}\gamma_{13} + C_{1112}\gamma_{12}
  $$
  与 $\sigma_1 = \sum_{J=1}^6 C_{1J} \varepsilon_J$ 比较，我们立刻得到 $\mathbf{C}_V$ 的第一行：
  $C_{11} = C_{1111}$, $C_{12} = C_{1122}$, $C_{13} = C_{1133}$, $C_{14} = C_{1123}$, $C_{15} = C_{1113}$, $C_{16} = C_{1112}$。

- **Case 2: 剪应力分量** ($\sigma_{23}, \sigma_{13}, \sigma_{12}$)
  以 $\sigma_{23}$ 为例 (Voigt 索引 $I=4$):
  $$
  \sigma_{23} = C_{2311}\varepsilon_{11} + C_{2322}\varepsilon_{22} + C_{2333}\varepsilon_{33} + C_{2323}\gamma_{23} + C_{2313}\gamma_{13} + C_{2312}\gamma_{12}
  $$
  与 $\sigma_4 = \sum_{J=1}^6 C_{4J} \varepsilon_J$ 比较，我们得到 $\mathbf{C}_V$ 的第四行：
  $C_{41} = C_{2311}$, $C_{42} = C_{2322}$, $C_{43} = C_{2333}$, $C_{44} = C_{2323}$, $C_{45} = C_{2313}$, $C_{46} = C_{2312}$。

综合来看，这种转换规则非常直接 [@problem_id:2918861]：
$$
C_{IJ} = C_{ijkl}
$$
其中 Voigt 索引 $I$ 对应张量索引对 $(ij)$，Voigt 索引 $J$ 对应张量索引对 $(kl)$。工程[剪应变](@entry_id:175241)定义中的因子 2 被完全吸收到应变向量的定义中，从而使得[刚度矩阵](@entry_id:178659)的数值转换变得简单。

#### 从Voigt矩阵到张量 ($C_V \to C_{ijkl}$)

逆向转换同样直接 [@problem_id:2918885]。通过比较 $\sigma_{ab} = \sum_{kl} C_{abkl}\varepsilon_{kl}$ 和 $\sigma_A = \sum_J c_{AJ}e_J$（其中 $\boldsymbol{s}$ 和 $\boldsymbol{e}$ 分别是应力和应变向量，$\mathbf{C}_V$ 的分量记为 $c_{AJ}$）这两个表达式，我们可以得到完全相同的映射关系：
$$
C_{ijkl} = c_{IJ}
$$
这里的关键在于，等式两边都必须基于相同的物理关系。例如，要找到 $C_{1323}$，我们识别出索引对 $(1,3)$ 对应 Voigt 索引 $I=5$，索引对 $(2,3)$ 对应 Voigt 索引 $J=4$。因此，$C_{1323} = c_{54}$。由于[刚度矩阵](@entry_id:178659)的对称性 ($c_{54}=c_{45}$)，这等价于 $c_{45}$。这种直接的数值[等价关系](@entry_id:138275)是采用工程-Voigt记法的一个核心优势。

#### [柔度矩阵](@entry_id:185679) ($S_V$)

与刚度关系 $\boldsymbol{\sigma}_V = \mathbf{C}_V \boldsymbol{\varepsilon}_V$ 相反，我们也可以将应变表示为应力的函数，即 $\boldsymbol{\varepsilon}_V = \mathbf{S}_V \boldsymbol{\sigma}_V$。这里的 $\mathbf{S}_V$ 被称为 **Voigt [柔度矩阵](@entry_id:185679)**，它与刚度矩阵互为[逆矩阵](@entry_id:140380)，$\mathbf{S}_V = \mathbf{C}_V^{-1}$。

[柔度矩阵](@entry_id:185679)的分量通常与实验上易于测量的工程常数直接相关，例如杨氏模量 $E_i$、泊松比 $\nu_{ij}$ 和[剪切模量](@entry_id:167228) $G_{ij}$。以最一般的**[正交各向异性](@entry_id:196967)**材料为例，其三个正交的材料主轴与坐标轴重合。我们可以通过叠加单轴应力状态下的应变来构建其[柔度矩阵](@entry_id:185679) [@problem_id:2918865]。

考虑一个沿 1 轴的单轴应力 $\sigma_{11}$，它产生的应变为：
$\varepsilon_{11} = \frac{\sigma_{11}}{E_1}$, $\varepsilon_{22} = -\nu_{12} \varepsilon_{11} = -\frac{\nu_{12}}{E_1} \sigma_{11}$, $\varepsilon_{33} = -\nu_{13} \varepsilon_{11} = -\frac{\nu_{13}}{E_1} \sigma_{11}$。
通过对三个方向的单轴应力状态进行线性叠加，并考虑纯剪切状态下的响应（例如 $\gamma_{12} = \sigma_{12} / G_{12}$），我们可以得到应变分量与所有应力分量的完整关系。例如，总应变 $\varepsilon_{11}$ 为：
$$
\varepsilon_{11} = \frac{1}{E_1}\sigma_{11} - \frac{\nu_{21}}{E_2}\sigma_{22} - \frac{\nu_{31}}{E_3}\sigma_{33}
$$
将这些关系与 $\boldsymbol{\varepsilon}_V = \mathbf{S}_V \boldsymbol{\sigma}_V$ 的矩阵形式进行比较，我们可以确定 $\mathbf{S}_V$ 的分量。例如，$S_{11} = 1/E_1$，$S_{12} = -\nu_{21}/E_2$，$S_{21} = -\nu_{12}/E_1$。

由于应变能的存在要求刚度矩阵和[柔度矩阵](@entry_id:185679)都是对称的，即 $S_{IJ} = S_{JI}$，这立即导出了一组重要的 **互易关系**：
$$
\frac{\nu_{ij}}{E_i} = \frac{\nu_{ji}}{E_j} \quad \text{for } i,j \in \{1,2,3\}, i \neq j
$$
这些关系将12个初始定义的工程常数（3个E，6个$\nu$，3个G）减少到9个独立的常数。最终，[正交各向异性材料](@entry_id:190111)的[柔度矩阵](@entry_id:185679)为：
$$
\mathbf{S}_V = 
\begin{pmatrix}
\frac{1}{E_1}  -\frac{\nu_{12}}{E_1}  -\frac{\nu_{13}}{E_1}  0  0  0 \\
-\frac{\nu_{12}}{E_1}  \frac{1}{E_2}  -\frac{\nu_{23}}{E_2}  0  0  0 \\
-\frac{\nu_{13}}{E_1}  -\frac{\nu_{23}}{E_2}  \frac{1}{E_3}  0  0  0 \\
0  0  0  \frac{1}{G_{23}}  0  0 \\
0  0  0  0  \frac{1}{G_{13}}  0 \\
0  0  0  0  0  \frac{1}{G_{12}}
\end{pmatrix}
$$

### [材料对称性](@entry_id:190289)与[刚度矩阵](@entry_id:178659)的结构

材料的内部[晶体结构](@entry_id:140373)或微观结构对称性对[刚度张量](@entry_id:176588)的分量施加了强有力的约束，从而极大地简化了其 Voigt 矩阵的形式。

#### [正交各向异性材料](@entry_id:190111)

如上所述，当材料主轴与坐标轴对齐时，[正交各向异性材料](@entry_id:190111)的刚度矩阵和[柔度矩阵](@entry_id:185679)都呈现出[块对角结构](@entry_id:746869)。正应力只引起[正应变](@entry_id:204633)，剪应力只引起相应的[剪应变](@entry_id:175241)。其[刚度矩阵](@entry_id:178659) $\mathbf{C}_V$ 的一般形式为 [@problem_id:2918861]：
$$
\mathbf{C}_V = 
\begin{pmatrix}
C_{11}  C_{12}  C_{13}  0  0  0 \\
C_{12}  C_{22}  C_{23}  0  0  0 \\
C_{13}  C_{23}  C_{33}  0  0  0 \\
0  0  0  C_{44}  0  0 \\
0  0  0  0  C_{55}  0 \\
0  0  0  0  0  C_{66}
\end{pmatrix}
$$
该矩阵有9个独立的非零分量。

#### 立方对称材料

对于具有[立方晶体结构](@entry_id:182292)的材料（例如铁、铜、铝），对称性要求更高。通过施加绕[坐标轴旋转](@entry_id:178802) $90^\circ$ 的[对称操作](@entry_id:143398)，可以证明[刚度张量](@entry_id:176588) $C_{ijkl}$ 中任何一个索引出现奇数次的分量都必须为零。这导致了更多的约束 [@problem_id:2918874]：
- $C_{1111} = C_{2222} = C_{3333}$ (记为 $C_{11}$)
- $C_{1122} = C_{1133} = C_{2233} = \dots$ (记为 $C_{12}$)
- $C_{2323} = C_{1313} = C_{1212}$ (记为 $C_{44}$)

因此，立方对称材料只有3个独立的弹性常数。其 Voigt [刚度矩阵](@entry_id:178659)为：
$$
\mathbf{C}_V = 
\begin{pmatrix}
C_{11}  C_{12}  C_{12}  0  0  0 \\
C_{12}  C_{11}  C_{12}  0  0  0 \\
C_{12}  C_{12}  C_{11}  0  0  0 \\
0  0  0  C_{44}  0  0 \\
0  0  0  0  C_{44}  0 \\
0  0  0  0  0  C_{44}
\end{pmatrix}
$$

#### 横观[各向同性材料](@entry_id:170678)

横观[各向同性材料](@entry_id:170678)（例如单向纤维[复合材料](@entry_id:139856)或某些晶体）在一个平面内（称为各向同性平面）具有各向同性，而在垂直于该平面的方向上具有不同的性质。如果[对称轴](@entry_id:177299)是 $x_3$ 轴，则该材料对绕 $x_3$ 轴的任意旋转都保持不变。这比[正交各向异性](@entry_id:196967)对称性更强，但比完全各向同性要弱。

从[正交各向异性](@entry_id:196967)矩阵出发，施加绕 $x_3$ 轴[旋转不变性](@entry_id:137644)的条件，可以推导出额外的约束 [@problem_id:2918862]：
$C_{11} = C_{22}$, $C_{13} = C_{23}$, $C_{44} = C_{55}$, 以及一个非常重要的关系 $C_{66} = \frac{1}{2}(C_{11}-C_{12})$。
这使得独立常数的数量减少到5个 ($C_{11}, C_{12}, C_{13}, C_{33}, C_{44}$)。其 Voigt [刚度矩阵](@entry_id:178659)为：
$$
\mathbf{C}_V = 
\begin{pmatrix}
C_{11}  C_{12}  C_{13}  0  0  0 \\
C_{12}  C_{11}  C_{13}  0  0  0 \\
C_{13}  C_{13}  C_{33}  0  0  0 \\
0  0  0  C_{44}  0  0 \\
0  0  0  0  C_{44}  0 \\
0  0  0  0  0  \frac{1}{2}(C_{11}-C_{12})
\end{pmatrix}
$$

#### [各向同性材料](@entry_id:170678)

[各向同性材料](@entry_id:170678)在所有方向上都具有相同的弹性性质，拥有最高的对称性。它们只有2个独立的弹性常数，通常用[杨氏模量](@entry_id:140430) $E$ 和[泊松比](@entry_id:158876) $\nu$ 或 Lamé 参数 $\lambda$ 和 $\mu$ 来描述。它们之间的关系可以通过分析单轴应力状态下的本构关系来建立 [@problem_id:2918830]：
$$
\mu = \frac{E}{2(1+\nu)} \quad \text{and} \quad \lambda = \frac{E\nu}{(1+\nu)(1-2\nu)}
$$
其中 $\mu$ 也是剪切模量 $G$。

[各向同性材料](@entry_id:170678)可以视为立方对称材料的特例，其中附加的对称性要求 $C_{11} = C_{12} + 2C_{44}$。这等效于 $C_{44} = \frac{1}{2}(C_{11}-C_{12})$，与横观[各向同性材料](@entry_id:170678)的约束 $C_{66} = \frac{1}{2}(C_{11}-C_{12})$ 形式相同，但现在扩展到了所有剪切项。

以 Lamé [参数表示](@entry_id:173803)，[刚度矩阵](@entry_id:178659)为：
$$
\mathbf{C}_V = 
\begin{pmatrix}
\lambda+2\mu  \lambda  \lambda  0  0  0 \\
\lambda  \lambda+2\mu  \lambda  0  0  0 \\
\lambda  \lambda  \lambda+2\mu  0  0  0 \\
0  0  0  \mu  0  0 \\
0  0  0  0  \mu  0 \\
0  0  0  0  0  \mu
\end{pmatrix}
$$
其[逆矩阵](@entry_id:140380)，即[柔度矩阵](@entry_id:185679)，用工程常数 $E$ 和 $\nu$ 表示则更加直观：
$$
\mathbf{S}_V = 
\begin{pmatrix}
\frac{1}{E}  -\frac{\nu}{E}  -\frac{\nu}{E}  0  0  0 \\
-\frac{\nu}{E}  \frac{1}{E}  -\frac{\nu}{E}  0  0  0 \\
-\frac{\nu}{E}  -\frac{\nu}{E}  \frac{1}{E}  0  0  0 \\
0  0  0  \frac{1}{G}  0  0 \\
0  0  0  0  \frac{1}{G}  0 \\
0  0  0  0  0  \frac{1}{G}
\end{pmatrix}
\quad \text{其中 } G = \frac{E}{2(1+\nu)}
$$

### 物理约束：应变能与[材料稳定性](@entry_id:183933)

Voigt 记法不仅仅是一种数学上的便利，它也必须遵守基本的物理定律。其中最重要的是热力学第二定律所引申出的[材料稳定性](@entry_id:183933)准则。

#### Voigt记法中的[应变能密度](@entry_id:200085)

我们之前确立了工程-Voigt记法保持了[应力与应变](@entry_id:137374)的能量共轭关系。为了得到从零应变状态加载到最终应变状态 $\boldsymbol{\varepsilon}_V$ 所需的总[应变能密度](@entry_id:200085) $W$，我们需要对[功率密度](@entry_id:194407)进行积分。假设一个成比例的加载路径 $\boldsymbol{\varepsilon}' = \alpha \boldsymbol{\varepsilon}_V$，其中 $\alpha$ 从 0 变化到 1 [@problem_id:2918890]：
$$
W = \int dW = \int_0^1 \boldsymbol{\sigma}'^{\mathsf{T}} d\boldsymbol{\varepsilon}'
$$
对于线性弹性材料，$\boldsymbol{\sigma}' = \mathbf{C}_V \boldsymbol{\varepsilon}' = \alpha \mathbf{C}_V \boldsymbol{\varepsilon}_V$，且 $d\boldsymbol{\varepsilon}' = \boldsymbol{\varepsilon}_V d\alpha$。代入积分：
$$
W = \int_0^1 (\alpha \mathbf{C}_V \boldsymbol{\varepsilon}_V)^{\mathsf{T}} (\boldsymbol{\varepsilon}_V d\alpha) = \int_0^1 \alpha (\boldsymbol{\varepsilon}_V^{\mathsf{T}} \mathbf{C}_V^{\mathsf{T}} \boldsymbol{\varepsilon}_V) d\alpha
$$
由于 $\mathbf{C}_V$ 是对称的 ($\mathbf{C}_V^{\mathsf{T}} = \mathbf{C}_V$)，表达式简化为：
$$
W = (\boldsymbol{\varepsilon}_V^{\mathsf{T}} \mathbf{C}_V \boldsymbol{\varepsilon}_V) \int_0^1 \alpha d\alpha = \frac{1}{2} \boldsymbol{\varepsilon}_V^{\mathsf{T}} \mathbf{C}_V \boldsymbol{\varepsilon}_V
$$
这是一个优美的二次型表达式，它表明[应变能密度](@entry_id:200085)是应变分量的二次函数，其系数由刚度矩阵的分量决定。例如，对于一个给定的应变状态 $\boldsymbol{\varepsilon}_V = [0.0012, -0.0005, \dots]^{\mathsf{T}}$ 和一个已知的刚度矩阵 $\mathbf{C}_V$，我们可以直接代入计算得到储存在材料中的能量密度 [@problem_id:2918890]。

#### [正定性](@entry_id:149643)条件

物理上，一个处于稳定平衡状态的材料，在受到任何非零的微小扰动（即应变）时，其内能必须增加。如果存在一种变形方式能使材料的内能减少，那么材料就会自发地发生这种变形以寻求更低的能量状态，这表明原始状态是不稳定的。因此，对于任何非零的应变向量 $\boldsymbol{\varepsilon}_V \neq \mathbf{0}$，储存的[应变能密度](@entry_id:200085) $W$ 必须为正：
$$
W = \frac{1}{2} \boldsymbol{\varepsilon}_V^{\mathsf{T}} \mathbf{C}_V \boldsymbol{\varepsilon}_V > 0 \quad \text{for all} \quad \boldsymbol{\varepsilon}_V \neq \mathbf{0}
$$
这正是数学上对一个**正定矩阵**的定义。因此，[材料稳定性](@entry_id:183933)的物理要求直接转化为一个数学约束：**任何物理上现实的[线性弹性](@entry_id:166983)材料，其 Voigt 刚度矩阵 $\mathbf{C}_V$ 必须是对称正定的 (Symmetric Positive Definite, SPD)。** [@problem_id:2918890] [@problem_id:2918819]

#### 稳定性检验

如何检验一个给定的刚度矩阵是否满足[正定性](@entry_id:149643)条件？一个常用且有效的数学工具是 **Sylvester 准则**。该准则指出，一个[对称矩阵](@entry_id:143130)是正定的，当且仅当它的所有**主子式**（leading principal minors）均为正。主子式是矩阵左上角 $k \times k$ 子矩阵的行列式，其中 $k$ 从 1 到矩阵的维度（这里是 6）。

让我们通过一个二维[平面应力](@entry_id:172193)[正交各向异性材料](@entry_id:190111)的例子来说明这一点 [@problem_id:2918819]。其刚度矩阵为 $3 \times 3$：
$$
\mathbf{C}_V = \begin{pmatrix}
C_{11}  C_{12}  0 \\
C_{12}  C_{22}  0 \\
0  0  C_{66}
\end{pmatrix}
$$
根据 Sylvester 准则，为保证稳定性，必须满足：
1.  $\Delta_1 = C_{11} > 0$
2.  $\Delta_2 = \det\begin{pmatrix} C_{11}  C_{12} \\ C_{12}  C_{22} \end{pmatrix} = C_{11}C_{22} - C_{12}^2 > 0$
3.  $\Delta_3 = \det(\mathbf{C}_V) = C_{66}(C_{11}C_{22} - C_{12}^2) > 0$

假设 $C_{11} = 150 \text{ GPa}$, $C_{22} = 100 \text{ GPa}$ 和 $C_{66} = 60 \text{ GPa}$，这些对角项显然满足了部分条件。但第二个条件给出了对耦合项 $C_{12}$ 的一个非平凡约束：
$C_{12}^2  C_{11}C_{22} = 150 \times 100 = 15000 \implies |C_{12}|  \sqrt{15000} \approx 122.5 \text{ GPa}$
这个结果有深刻的物理意义。$C_{12}$ 代表了由 $\varepsilon_{22}$ 引起的 $\sigma_{11}$ 应力（[泊松效应](@entry_id:158876)）。如果这个耦合效应过强（$|C_{12}|$ 过大），就可能存在一种应变状态（例如，一个方向拉伸，另一个方向压缩），使得由耦合项贡献的[负能量](@entry_id:161542)超过了由[主应变](@entry_id:197797)项贡献的正能量，导致总应变能为负，从而引发材料失稳。因此，稳定性要求对材料的[弹性常数](@entry_id:146207)施加了严格的数学界限。对于各向同性材料，这些条件最终会转化为对泊松比的著名约束：$-1  \nu  0.5$。