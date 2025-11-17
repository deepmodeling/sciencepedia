## 引言
正交投影是线性代数中的一个核心概念，它提供了一种将复杂向量分解为更简单、可管理分量的强大方法。其根本思想是在一个给定的[子空间](@entry_id:150286)（本文中为一条直线）中，寻找到一个向量的最佳近似。这一看似简单的几何问题，实际上是解决从数据科学中的[最小二乘拟合](@entry_id:751226)到[计算机图形学](@entry_id:148077)中的阴影计算等众多实际挑战的关键。本文旨在全面解析向量到直线上[正交投影](@entry_id:144168)的理论与实践。

在接下来的内容中，我们将分三步深入探讨这一主题。首先，在“原理与机制”一章中，我们将从几何直觉出发，推导出[正交投影](@entry_id:144168)的代数公式，并揭示其作为[线性变换](@entry_id:149133)的深刻性质，包括其[矩阵表示](@entry_id:146025)和谱特性。接着，在“应用与跨学科联系”一章中，我们将展示这一基本工具如何在物理学、工程学和数据分析等不同领域中发挥作用，连接起抽象理论与具体实践。最后，通过“动手实践”环节，你将有机会通过解决具体问题来巩固和检验所学知识，从而真正掌握正交投影的精髓。

## 原理与机制

在本章中，我们将深入探讨向量到直线上正交投影的核心原理与机制。[正交投影](@entry_id:144168)不仅是线性代数中的一个基本概念，更是在数据科学、计算机图形学和物理学等众多领域中解决实际问题的关键工具。我们将从其几何直觉出发，逐步建立起[代数表示](@entry_id:143783)，并最终揭示其作为一种线性变换的深刻性质。

### 向量的[正交分解](@entry_id:148020)：几何直觉与代数定义

在欧几里得空间中，一个核心思想是将复杂的向量分解为更简单、相互正交的分量。对于任意向量 $\vec{v}$ 和一条过原点的直线 $L$，我们可以将 $\vec{v}$ 唯一地分解为两个向量之和：一个向量 $\vec{p}$ 位于直线 $L$ 上，另一个向量 $\vec{z}$ 与直线 $L$ 正交。

这个位于直线 $L$ 上的分量 $\vec{p}$ 被称为向量 $\vec{v}$ 到直线 $L$ 上的**[正交投影](@entry_id:144168) (orthogonal projection)**。而与 $L$ 正交的分量 $\vec{z}$ 则被称为**正交补向量 (orthogonal component vector)** 或**[残差向量](@entry_id:165091) (residual vector)**。因此，我们有分解式：
$$ \vec{v} = \vec{p} + \vec{z} $$
其中 $\vec{p}$ 平行于 $L$，而 $\vec{z}$ 正交于 $L$。

为了推导计算投影向量 $\vec{p}$ 的通用公式，我们假设直线 $L$ 是由一个非[零向量](@entry_id:156189) $\vec{u}$ 所张成的空间，即 $L = \operatorname{span}\{\vec{u}\}$。根据定义，向量 $\vec{p}$ 必须在直线 $L$ 上，这意味着 $\vec{p}$ 是 $\vec{u}$ 的一个标量倍数。我们可以写成：
$$ \vec{p} = c\vec{u} $$
其中 $c$ 是一个待定标量。

这个分解的关键在于向量 $\vec{z} = \vec{v} - \vec{p}$ 必须与直线 $L$（也就是与向量 $\vec{u}$）正交。在代数上，两个向量正交等价于它们的[点积](@entry_id:149019)为零。因此，我们施加条件：
$$ (\vec{v} - \vec{p}) \cdot \vec{u} = 0 $$
将 $\vec{p} = c\vec{u}$ 代入上式，得到：
$$ (\vec{v} - c\vec{u}) \cdot \vec{u} = 0 $$
利用[点积](@entry_id:149019)的线性性质，我们展开此式：
$$ \vec{v} \cdot \vec{u} - c(\vec{u} \cdot \vec{u}) = 0 $$
由于 $\vec{u}$ 是一个非[零向量](@entry_id:156189)，$\vec{u} \cdot \vec{u} = \|\vec{u}\|^2$ 的值不为零。因此，我们可以解出标量 $c$：
$$ c = \frac{\vec{v} \cdot \vec{u}}{\vec{u} \cdot \vec{u}} $$
将 $c$ 的表达式代回 $\vec{p} = c\vec{u}$，我们便得到了计算任意向量 $\vec{v}$ 到由 $\vec{u}$ 所张成的直线上的[正交投影](@entry_id:144168)的普适公式：
$$ \vec{p} = \operatorname{proj}_{\vec{u}}\vec{v} = \frac{\vec{v} \cdot \vec{u}}{\vec{u} \cdot \vec{u}} \vec{u} $$
这个公式是本章后续所有讨论的基石。一旦我们求得投影向量 $\vec{p}$，正交分量 $\vec{z}$ 便可轻易通过相减得到：$\vec{z} = \vec{v} - \vec{p}$。

为了具体说明这个过程，我们考虑将向量 $\vec{v} = \begin{pmatrix} 2 \\ 5 \end{pmatrix}$ 分解到由 $\vec{u} = \begin{pmatrix} 4 \\ -3 \end{pmatrix}$ 张成的直线上 [@problem_id:1380655]。首先计算所需的[点积](@entry_id:149019)：
$$ \vec{v} \cdot \vec{u} = (2)(4) + (5)(-3) = 8 - 15 = -7 $$
$$ \vec{u} \cdot \vec{u} = (4)^2 + (-3)^2 = 16 + 9 = 25 $$
根据[投影公式](@entry_id:152164)，我们得到投影向量 $\vec{p}$：
$$ \vec{p} = \frac{-7}{25} \vec{u} = \frac{-7}{25} \begin{pmatrix} 4 \\ -3 \end{pmatrix} = \begin{pmatrix} -28/25 \\ 21/25 \end{pmatrix} $$
正交分量 $\vec{z}$ 则是：
$$ \vec{z} = \vec{v} - \vec{p} = \begin{pmatrix} 2 \\ 5 \end{pmatrix} - \begin{pmatrix} -28/25 \\ 21/25 \end{pmatrix} = \begin{pmatrix} 50/25 + 28/25 \\ 125/25 - 21/25 \end{pmatrix} = \begin{pmatrix} 78/25 \\ 104/25 \end{pmatrix} $$
按照定义，$\vec{z}$ 必须与 $\vec{u}$ 正交。我们可以通过计算它们的[点积](@entry_id:149019)来验证这一点，这在概念上是至关重要的 [@problem_id:1380615]。实际上，无论具体的向量是什么，残差向量 $\vec{z} = \vec{v} - \vec{p}$ 与方向向量 $\vec{u}$ 的[点积](@entry_id:149019)恒为零。证明如下：
$$ \vec{z} \cdot \vec{u} = (\vec{v} - \vec{p}) \cdot \vec{u} = \vec{v} \cdot \vec{u} - \vec{p} \cdot \vec{u} $$
将 $\vec{p}$ 的公式代入 $\vec{p} \cdot \vec{u}$：
$$ \vec{p} \cdot \vec{u} = \left( \frac{\vec{v} \cdot \vec{u}}{\vec{u} \cdot \vec{u}} \vec{u} \right) \cdot \vec{u} = \frac{\vec{v} \cdot \vec{u}}{\vec{u} \cdot \vec{u}} (\vec{u} \cdot \vec{u}) = \vec{v} \cdot \vec{u} $$
因此，
$$ \vec{z} \cdot \vec{u} = \vec{v} \cdot \vec{u} - \vec{v} \cdot \vec{u} = 0 $$
这从代数上严格证明了我们的几何构造是自洽的。

### 投影的几何性质：长度与[毕达哥拉斯定理](@entry_id:264352)

[正交分解](@entry_id:148020) $\vec{v} = \vec{p} + \vec{z}$ 的一个优美结果是它与毕达哥拉斯定理（[勾股定理](@entry_id:264352)）的深刻联系。由于向量 $\vec{p}$ 和 $\vec{z}$ 相互正交，它们可以被看作一个直角三角形的两条直角边，而原始向量 $\vec{v}$ 则是该三角形的斜边。

根据毕达哥拉斯定理，我们有：
$$ \|\vec{v}\|^2 = \|\vec{p}\|^2 + \|\vec{z}\|^2 $$
即：
$$ \|\vec{v}\|^2 = \|\operatorname{proj}_{\vec{u}}\vec{v}\|^2 + \|\vec{v} - \operatorname{proj}_{\vec{u}}\vec{v}\|^2 $$
这个关系式蕴含了一个重要的几何意义：投影点 $\vec{p}$ 是直线上距离向量 $\vec{v}$ 端点最近的点。换言之，正交分量 $\vec{z}$ 的长度 $\|\vec{z}\| = \|\vec{v} - \vec{p}\|$ 代表了点 $\vec{v}$ 到直线 $L$ 的最短距离。

例如，考虑计算向量 $\vec{y} = \begin{pmatrix} 2 \\ -5 \\ 3 \end{pmatrix}$ 到由向量 $\vec{u} = \begin{pmatrix} 1 \\ 4 \\ -1 \end{pmatrix}$ 张成的直线的距离 [@problem_id:1380638]。这等价于计算其正交分量 $\vec{z}$ 的模长 $\|\vec{z}\|$。
首先，我们计算投影向量 $\vec{p}$：
$$ \vec{y} \cdot \vec{u} = (2)(1) + (-5)(4) + (3)(-1) = -21 $$
$$ \vec{u} \cdot \vec{u} = 1^2 + 4^2 + (-1)^2 = 18 $$
$$ \vec{p} = \frac{-21}{18} \vec{u} = -\frac{7}{6} \begin{pmatrix} 1 \\ 4 \\ -1 \end{pmatrix} = \begin{pmatrix} -7/6 \\ -28/6 \\ 7/6 \end{pmatrix} = \begin{pmatrix} -7/6 \\ -14/3 \\ 7/6 \end{pmatrix} $$
接着，我们计算正交分量 $\vec{z}$：
$$ \vec{z} = \vec{y} - \vec{p} = \begin{pmatrix} 2 \\ -5 \\ 3 \end{pmatrix} - \begin{pmatrix} -7/6 \\ -14/3 \\ 7/6 \end{pmatrix} = \begin{pmatrix} 19/6 \\ -1/3 \\ 11/6 \end{pmatrix} $$
最后，计算其模长：
$$ \|\vec{z}\| = \sqrt{\left(\frac{19}{6}\right)^2 + \left(-\frac{1}{3}\right)^2 + \left(\frac{11}{6}\right)^2} = \sqrt{\frac{361}{36} + \frac{4}{36} + \frac{121}{36}} = \sqrt{\frac{486}{36}} = \sqrt{\frac{27}{2}} \approx 3.674 $$
这个值就是向量 $\vec{y}$ 的终点到直线 $L$ 的最短距离。

### 投影变换及其[矩阵表示](@entry_id:146025)

至此，我们将投影视为对单个向量的操作。然而，我们可以将这个操作推广为作用于整个[向量空间](@entry_id:151108)的**变换 (transformation)**。对于一个固定的直线 $L = \operatorname{span}\{\vec{u}\}$，我们可以定义一个函数 $T: \mathbb{R}^n \to \mathbb{R}^n$，它将空间中的每一个向量 $\vec{x}$ 映射到它在 $L$ 上的[正交投影](@entry_id:144168)：
$$ T(\vec{x}) = \operatorname{proj}_{\vec{u}}\vec{x} = \frac{\vec{x} \cdot \vec{u}}{\vec{u} \cdot \vec{u}} \vec{u} $$
这个投影变换 $T$ 是一种**[线性变换](@entry_id:149133) (linear transformation)**。这意味着它满足两个基本条件：
1.  可加性: $T(\vec{x} + \vec{y}) = T(\vec{x}) + T(\vec{y})$
2.  齐次性: $T(k\vec{x}) = k T(\vec{x})$ 对于任意标量 $k$

线性代数的一个基本结论是，任何从 $\mathbb{R}^n$到 $\mathbb{R}^m$的线性变换都可以用一个 $m \times n$ 的矩阵来表示。因此，投影变换 $T$ 必然对应一个 $n \times n$ 的**[投影矩阵](@entry_id:154479) (projection matrix)** $P$，使得 $T(\vec{x}) = P\vec{x}$。

为了找到这个矩阵 $P$，我们将[投影公式](@entry_id:152164)用[矩阵乘法](@entry_id:156035)来重写。注意到[点积](@entry_id:149019) $\vec{x} \cdot \vec{u}$ 可以表示为矩阵乘积 $\vec{u}^T\vec{x}$（其中向量被视为列矩阵）。于是，[投影公式](@entry_id:152164)变为：
$$ T(\vec{x}) = \left( \frac{\vec{u}^T\vec{x}}{\vec{u}^T\vec{u}} \right) \vec{u} $$
由于括号中的项 $\frac{\vec{u}^T\vec{x}}{\vec{u}^T\vec{u}}$ 是一个标量，我们可以将其移动到向量 $\vec{u}$ 的左侧：
$$ T(\vec{x}) = \vec{u} \left( \frac{\vec{u}^T\vec{x}}{\vec{u}^T\vec{u}} \right) $$
利用[矩阵乘法](@entry_id:156035)的结合律，我们可以重新组合这个表达式：
$$ T(\vec{x}) = \left( \frac{\vec{u}\vec{u}^T}{\vec{u}^T\vec{u}} \right) \vec{x} $$
这里，$\vec{u}\vec{u}^T$ 是一个**外积 (outer product)**，一个 $n \times 1$ 的列向量乘以一个 $1 \times n$ 的行向量，结果是一个 $n \times n$ 的矩阵。而分母 $\vec{u}^T\vec{u}$ 是一个**[内积](@entry_id:158127) (inner product)**，结果是一个标量（$1 \times 1$ 矩阵）。这样，我们便识别出了[投影矩阵](@entry_id:154479) $P$：
$$ P = \frac{\vec{u}\vec{u}^T}{\vec{u}^T\vec{u}} $$
这个矩阵 $P$ 捕获了向直线 $\operatorname{span}\{\vec{u}\}$ 投影的全部几何信息。

例如，在三维空间中，给定[方向向量](@entry_id:169562) $\vec{u} = \begin{pmatrix} u_1 \\ u_2 \\ u_3 \end{pmatrix}$，[投影矩阵](@entry_id:154479)的分母是 $\|\vec{u}\|^2 = u_1^2 + u_2^2 + u_3^2$，分子是外积矩阵 [@problem_id:1380632]：
$$ \vec{u}\vec{u}^T = \begin{pmatrix} u_1 \\ u_2 \\ u_3 \end{pmatrix} \begin{pmatrix} u_1  u_2  u_3 \end{pmatrix} = \begin{pmatrix} u_1^2  u_1u_2  u_1u_3 \\ u_2u_1  u_2^2  u_2u_3 \\ u_3u_1  u_3u_2  u_3^2 \end{pmatrix} $$
因此，[投影矩阵](@entry_id:154479)为：
$$ P = \frac{1}{u_1^2+u_2^2+u_3^2} \begin{pmatrix} u_1^2  u_1u_2  u_1u_3 \\ u_2u_1  u_2^2  u_2u_3 \\ u_3u_1  u_3u_2  u_3^2 \end{pmatrix} $$
以计算机图形学中的阴影投射为例，若阴影方向由向量 $\vec{u} = \begin{pmatrix} 1 \\ -3 \\ 2 \end{pmatrix}$ 定义，我们可以计算出具体的[投影矩阵](@entry_id:154479) [@problem_id:1380641]。首先，$\vec{u}^T\vec{u} = 1^2 + (-3)^2 + 2^2 = 14$。然后，外积为：
$$ \vec{u}\vec{u}^T = \begin{pmatrix} 1 \\ -3 \\ 2 \end{pmatrix} \begin{pmatrix} 1  -3  2 \end{pmatrix} = \begin{pmatrix} 1  -3  2 \\ -3  9  -6 \\ 2  -6  4 \end{pmatrix} $$
于是，[投影矩阵](@entry_id:154479) $A$ 为：
$$ A = \frac{1}{14} \begin{pmatrix} 1  -3  2 \\ -3  9  -6 \\ 2  -6  4 \end{pmatrix} = \begin{pmatrix} 1/14  -3/14  1/7 \\ -3/14  9/14  -3/7 \\ 1/7  -3/7  2/7 \end{pmatrix} $$
任何向量 $\vec{v}$ 乘以该矩阵 $A$，其结果 $A\vec{v}$ 就是它在 $\vec{u}$ 方向上的投影。

### [投影矩阵](@entry_id:154479)的代数性质

[投影矩阵](@entry_id:154479) $P$ 具有一些非常重要的代数性质，这些性质直接反映了其几何作用。

#### [幂等性](@entry_id:190768) (Idempotence)

[投影矩阵](@entry_id:154479)最重要的性质是**[幂等性](@entry_id:190768)**，即 $P^2 = P$。
这个性质的几何直觉非常清晰：对一个向量进行一次投影，会将其“压”到目标直线上。如果对这个已经位于直线上的结果再进行一次相同的投影，它显然不会发生任何变化。也就是说，对于任意向量 $\vec{x}$，第一次投影得到 $P\vec{x}$，它已经在直线上。第二次投影 $P(P\vec{x})$ 必然等于 $P\vec{x}$。因此，$P^2\vec{x} = P\vec{x}$ 对所有 $\vec{x}$ 成立，这意味着 $P^2=P$。

这一性质在处理迭代变换时非常有用。例如，考虑一个[递归序列](@entry_id:145839) $\vec{v}_k = T(\vec{v}_{k-1}) = P\vec{v}_{k-1}$，其中 $\vec{v}_0$ 是初始向量 [@problem_id:1380646]。
$$ \vec{v}_1 = P\vec{v}_0 $$
$$ \vec{v}_2 = P\vec{v}_1 = P(P\vec{v}_0) = P^2\vec{v}_0 $$
由于 $P^2 = P$，我们得到 $\vec{v}_2 = P\vec{v}_0 = \vec{v}_1$。以此类推，对于所有 $k \ge 1$，我们都有 $\vec{v}_k = \vec{v}_1$。这意味着，无论我们应用投影变换多少次，从第二次开始，结果都将稳定在第一次投影的结果上。

我们也可以从代数上证明 $P^2=P$：
$$ P^2 = \left(\frac{\vec{u}\vec{u}^T}{\vec{u}^T\vec{u}}\right) \left(\frac{\vec{u}\vec{u}^T}{\vec{u}^T\vec{u}}\right) = \frac{\vec{u}(\vec{u}^T\vec{u})\vec{u}^T}{(\vec{u}^T\vec{u})^2} $$
由于 $\vec{u}^T\vec{u}$ 是一个标量，我们可以将其从矩阵中间提出来，并与分母的一个因子相消：
$$ P^2 = \frac{(\vec{u}^T\vec{u})}{(\vec{u}^T\vec{u})^2} (\vec{u}\vec{u}^T) = \frac{\vec{u}\vec{u}^T}{\vec{u}^T\vec{u}} = P $$

#### 对称性 (Symmetry)

正交投影矩阵的另一个关键性质是**对称性**，即 $P^T = P$。
我们可以通过其定义式来证明这一点：
$$ P^T = \left(\frac{\vec{u}\vec{u}^T}{\vec{u}^T\vec{u}}\right)^T = \frac{(\vec{u}\vec{u}^T)^T}{\vec{u}^T\vec{u}} $$
分母 $\vec{u}^T\vec{u}$ 是一个标量，转置不改变它。对于分子，我们使用矩阵乘积的[转置](@entry_id:142115)法则 $(AB)^T = B^TA^T$：
$$ (\vec{u}\vec{u}^T)^T = (\vec{u}^T)^T \vec{u}^T = \vec{u}\vec{u}^T $$
因此，
$$ P^T = \frac{\vec{u}\vec{u}^T}{\vec{u}^T\vec{u}} = P $$
对称性是正交投影区别于[斜投影](@entry_id:752867)的一个标志。这个性质在矩阵计算中非常有用，例如，它可以简化涉及[投影矩阵的迹](@entry_id:155632)的计算 [@problem_id:1380623]。利用[迹的循环性质](@entry_id:153103) $\operatorname{tr}(ABC) = \operatorname{tr}(BCA)$ 和[投影矩阵](@entry_id:154479)的性质，我们可以进行如下化简：
$$ \operatorname{tr}(PMP^T) = \operatorname{tr}(PMP) \quad (\text{因为 } P^T=P) $$
$$ \operatorname{tr}(PMP) = \operatorname{tr}(PP M) = \operatorname{tr}(P^2 M) = \operatorname{tr}(PM) \quad (\text{因为 } P^2=P) $$
这使得原本复杂的表达式变得更加简洁。

### 投影变换的谱分析：秩、核与[特征值](@entry_id:154894)

通过分析[投影矩阵](@entry_id:154479)的秩、核与[特征值](@entry_id:154894)，我们可以从更深层次理解投影变换的几何行为。

#### 秩 (Rank)

线性变换的**秩 (rank)** 是其像空间（或称列空间）的维度。对于投影变换 $T(\vec{x}) = P\vec{x}$，其像空间 $\operatorname{Im}(T)$ 是所有可能的输出向量的集合。根据定义，所有向量都被投影到由 $\vec{u}$ 张成的直线上。因此，像空间就是这条直线本身：
$$ \operatorname{Im}(T) = \operatorname{span}\{\vec{u}\} $$
因为 $\vec{u}$ 是一个非零向量，这个[子空间](@entry_id:150286)的维度是1。所以，任何向一条直线作[正交投影](@entry_id:144168)的矩阵 $P$ 的秩都等于1 [@problem_id:1380614]。这从代数上确认了投影变换将整个空间“压缩”到一条线上的几何事实。

#### 核 (Kernel)

[线性变换](@entry_id:149133)的**核 (kernel)**（或称零空间）是所有被映射到[零向量](@entry_id:156189)的输入向量的集合，即 $\ker(T) = \{\vec{x} \in \mathbb{R}^n \mid T(\vec{x}) = \vec{0}\}$。
对于投影变换，我们要寻找满足以下条件的向量 $\vec{x}$：
$$ P\vec{x} = \frac{\vec{x} \cdot \vec{u}}{\vec{u} \cdot \vec{u}} \vec{u} = \vec{0} $$
由于 $\vec{u} \neq \vec{0}$，上式成立的唯一可能是其标量系数为零：
$$ \vec{x} \cdot \vec{u} = 0 $$
这意味着，投影[变换的核](@entry_id:149509)由所有与直线 $\operatorname{span}\{\vec{u}\}$ 正交的向量组成。这个空间正是直线 $L = \operatorname{span}\{\vec{u}\}$ 的**[正交补](@entry_id:149922)空间 (orthogonal complement)**，记为 $L^\perp$。

在三维空间 $\mathbb{R}^3$ 中，一条直线的正交补是一个通过原点的平面。例如，对于投影到由 $\vec{u} = \begin{pmatrix} 1 \\ 2 \\ 0 \end{pmatrix}$ 张成的直线上的变换，其核是所有满足 $x+2y=0$ 的向量 $\begin{pmatrix} x \\ y \\ z \end{pmatrix}$ 构成的平面。这个平面可以由一组基[向量张成](@entry_id:152883)，例如 $\left\{ \begin{pmatrix} -2 \\ 1 \\ 0 \end{pmatrix}, \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix} \right\}$ [@problem_id:1380652]。
根据秩-零度定理，$\operatorname{rank}(P) + \operatorname{dim}(\ker(P)) = n$。对于到直线的投影，$1 + (n-1) = n$，这与我们的发现完全一致。

#### [特征值与特征向量](@entry_id:748836) (Eigenvalues and Eigenvectors)

[特征向量](@entry_id:151813)是在[线性变换](@entry_id:149133)下方向保持不变（仅被缩放）的特殊向量，即满足 $T(\vec{x}) = \lambda\vec{x}$ 的非[零向量](@entry_id:156189) $\vec{x}$。缩放因子 $\lambda$ 称为对应的**[特征值](@entry_id:154894) (eigenvalue)**。投影变换的[特征向量](@entry_id:151813)和[特征值](@entry_id:154894)具有清晰的几何解释 [@problem_id:1380601]。

- **[特征值](@entry_id:154894) $\lambda = 1$**: 哪些向量在投影后保持不变？显然，任何已经位于投影直线 $L$ 上的向量都满足这个条件。对于任意属于 $L$ 的向量 $\vec{x}$（即 $\vec{x} = c\vec{u}$），它的投影就是它自身，$T(\vec{x}) = \vec{x}$。因此，$1$ 是一个[特征值](@entry_id:154894)，其对应的[特征空间](@entry_id:638014)就是直线 $L$ 本身。

- **[特征值](@entry_id:154894) $\lambda = 0$**: 哪些向量在投影后变成[零向量](@entry_id:156189)？根据我们对核的分析，这些正是所有与直线 $L$ 正交的向量。对于任何属于 $L^\perp$ 的向量 $\vec{x}$，我们有 $T(\vec{x}) = \vec{0} = 0 \cdot \vec{x}$。因此，$0$ 是另一个[特征值](@entry_id:154894)，其对应的特征空间就是[正交补](@entry_id:149922)空间 $L^\perp$。

在 $n$ 维空间中，直线 $L$ 是一维的，其正交补 $L^\perp$ 是 $(n-1)$ 维的。因此，[特征值](@entry_id:154894) 1 的[几何重数](@entry_id:155584)是 1，而[特征值](@entry_id:154894) 0 的[几何重数](@entry_id:155584)是 $n-1$。对于向一条直线作[正交投影](@entry_id:144168)，除了 0 和 1 之外，不存在其他[特征值](@entry_id:154894)。

我们也可以从代数角度证明这一点。若 $\lambda$ 是[投影矩阵](@entry_id:154479) $P$ 的一个[特征值](@entry_id:154894)，则存在[特征向量](@entry_id:151813) $\vec{x} \neq \vec{0}$ 使得 $P\vec{x} = \lambda\vec{x}$。将 $P$ 作用于该式两侧，得到 $P(P\vec{x}) = P(\lambda\vec{x})$，即 $P^2\vec{x} = \lambda(P\vec{x}) = \lambda(\lambda\vec{x}) = \lambda^2\vec{x}$。利用[幂等性](@entry_id:190768) $P^2=P$，我们有 $P\vec{x} = \lambda^2\vec{x}$。
因此，我们得到 $\lambda\vec{x} = \lambda^2\vec{x}$，即 $(\lambda^2 - \lambda)\vec{x} = \vec{0}$。由于 $\vec{x}$ 是非[零向量](@entry_id:156189)，必须有 $\lambda^2 - \lambda = 0$，即 $\lambda(\lambda-1) = 0$。此方程的解为 $\lambda=0$ 或 $\lambda=1$。这证实了，对于任何非平凡的[正交投影](@entry_id:144168)，其全部[特征值](@entry_id:154894)构成的集合为 $\{0, 1\}$。