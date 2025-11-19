## 引言
在物理学与工程学的广阔天地中，[笛卡尔坐标系](@entry_id:169789)以其简洁直观的特性为我们提供了分析众多问题的基础框架。然而，当我们面对具有内在对称性（如球对称或[轴对称](@entry_id:173333)）的系统时——例如行星轨道、流体涡旋或[弯曲时空](@entry_id:159822)，严格的直角坐标网格便显得力不从心。为了更自然、更高效地描述这些现象，我们必须超越笛卡尔的限制，进入一个更普适的数学领域：[曲线坐标系](@entry_id:172561)。

本文旨在系统地引导读者完成这一关键的认知升级。我们将直面从恒定[基矢](@entry_id:199546)到可变[基矢](@entry_id:199546)所带来的核心挑战：当坐标轴本身在空间中弯曲和伸缩时，我们应如何定义距离、角度，又该如何对矢量场进行[微分](@entry_id:158718)？文章将为你揭示这套强大的几何语言是如何构建的，以及它如何成为从经典力学到广义相对论等众多现代科学理论的基石。

在接下来的章节中，你将首先在“原理与机制”中学习到[曲线坐标系](@entry_id:172561)的基石——局域[基矢](@entry_id:199546)、[度规张量](@entry_id:160222)和协变导数，掌握在弯曲坐标网格中进行精确计算的数学工具。随后，在“应用与跨学科联系”中，你将看到这些抽象的工具如何在电磁学、[流体力学](@entry_id:136788)、相对论乃至[量子化学](@entry_id:140193)等不同领域中大放异彩，将复杂问题化繁为简。最后，通过“动手实践”中的具体问题，你将有机会亲手运用所学知识，巩固并深化对这一重要理论的理解。

## 原理与机制

从熟悉的[笛卡尔坐标系](@entry_id:169789)过渡到更广义的[曲线坐标系](@entry_id:172561)，是理解现代物理学和工程学中许多高级概念的关键一步。虽然[笛卡尔坐标系](@entry_id:169789)以其恒定不变的直角[基矢](@entry_id:199546)提供了极大的便利，但自然界和人造系统中的许多问题，其固有的对称性或边界条件，用直线和平面来描述会显得异常笨拙。例如，行星的[轨道](@entry_id:137151)、流体中的涡旋或天线的电磁辐射，在[球坐标](@entry_id:146054)或[柱坐标](@entry_id:271645)等[曲线坐标系](@entry_id:172561)中处理会简单得多。本章旨在系统地阐述在这些更普适的[坐标系](@entry_id:156346)中进行几何和微积分运算所需的基本原理和核心机制。

### 局域[基矢](@entry_id:199546)：[协变基](@entry_id:198968)矢

在三维欧氏空间中，任意一点的位置向量 $\mathbf{r}$ 可以表示为其[笛卡尔坐标](@entry_id:167698) $(x, y, z)$ 的函数，即 $\mathbf{r} = x\mathbf{\hat{i}} + y\mathbf{\hat{j}} + z\mathbf{\hat{k}}$。其中，$(\mathbf{\hat{i}}, \mathbf{\hat{j}}, \mathbf{\hat{k}})$ 是一组[标准正交基](@entry_id:147779)矢，它们在空间中每一点都保持不变。现在，我们引入一组广义曲线坐标 $(u^1, u^2, u^3)$，使得笛卡尔坐标是它们的函数：$x = x(u^1, u^2, u^3)$, $y = y(u^1, u^2, u^3)$, $z = z(u^1, u^2, u^3)$。

在新的[曲线坐标系](@entry_id:172561)中，我们不再拥有一个全局统一的基准。取而代之的是，我们在空间的每一点都定义了一组**局域[基矢](@entry_id:199546) (local basis vectors)**。最自然的一组[基矢](@entry_id:199546)是通过考察当我们沿着某一个坐标方向移动时，位置向量 $\mathbf{r}$ 如何变化来定义的。我们将沿 $u^i$ 坐标曲线的切向向量定义为**[协变基](@entry_id:198968)矢 (covariant basis vectors)** $\mathbf{e}_i$：

$$
\mathbf{e}_i = \frac{\partial \mathbf{r}}{\partial u^i}
$$

这个定义直观地揭示了[协变基](@entry_id:198968)矢的几何意义：$\mathbf{e}_1$ 沿着 $u^2$ 和 $u^3$ 保持不变的 $u^1$ 坐标曲线相切，$\mathbf{e}_2$ 沿着 $u^2$ 坐标曲线相切，以此类推。这组[基矢](@entry_id:199546) $(\mathbf{e}_1, \mathbf{e}_2, \mathbf{e}_3)$ 构成了在点 $(u^1, u^2, u^3)$ 处的局域坐标框架。

例如，考虑由坐标 $(\sigma, \tau, z)$ 定义的抛物柱面[坐标系](@entry_id:156346)，其与笛卡尔坐标的关系为 $x = \sigma \tau$, $y = \frac{1}{2}(\tau^2 - \sigma^2)$, $z = z$。位置向量为 $\mathbf{r} = (\sigma \tau)\mathbf{\hat{i}} + \frac{1}{2}(\tau^2 - \sigma^2)\mathbf{\hat{j}} + z\mathbf{\hat{k}}$。我们可以计算与坐标 $\sigma$ 相关联的[协变基](@entry_id:198968)矢 $\mathbf{e}_\sigma$ [@problem_id:1491018]：

$$
\mathbf{e}_\sigma = \frac{\partial \mathbf{r}}{\partial \sigma} = \frac{\partial x}{\partial \sigma}\mathbf{\hat{i}} + \frac{\partial y}{\partial \sigma}\mathbf{\hat{j}} + \frac{\partial z}{\partial \sigma}\mathbf{\hat{k}} = \tau\mathbf{\hat{i}} - \sigma\mathbf{\hat{j}}
$$

从这个表达式中，一个至关重要的特性显现出来：[协变基](@entry_id:198968)矢 $\mathbf{e}_\sigma$ 的分量依赖于坐标 $\sigma$ 和 $\tau$。这意味着，与笛卡尔[基矢](@entry_id:199546)不同，**[协变基](@entry_id:198968)矢是位置的函数**。它们的大小和方向在空间中从一点到另一点会发生变化。

为了更清晰地说明这一点，我们考察更熟悉的[柱坐标系](@entry_id:266798) $(\rho, \phi, z)$ [@problem_id:1503636]。位置向量为 $\mathbf{r} = (\rho \cos\phi)\mathbf{\hat{i}} + (\rho \sin\phi)\mathbf{\hat{j}} + z\mathbf{\hat{k}}$。与角坐标 $\phi$ 对应的[协变基](@entry_id:198968)矢（有时也记作 $\mathbf{g}_\phi$）为：

$$
\mathbf{g}_\phi = \frac{\partial \mathbf{r}}{\partial \phi} = (-\rho \sin\phi)\mathbf{\hat{i}} + (\rho \cos\phi)\mathbf{\hat{j}}
$$

这个向量的长度是 $|\mathbf{g}_\phi| = \rho$，并且其方向在 $xy$ 平面内总是与径向垂直。如果我们考察这个[基矢](@entry_id:199546)如何随 $\phi$ 变化，即计算它对 $\phi$ 的[偏导数](@entry_id:146280)，我们会发现：

$$
\frac{\partial \mathbf{g}_\phi}{\partial \phi} = \frac{\partial}{\partial \phi} \left( (-\rho \sin\phi)\mathbf{\hat{i}} + (\rho \cos\phi)\mathbf{\hat{j}} \right) = (-\rho \cos\phi)\mathbf{\hat{i}} - (\rho \sin\phi)\mathbf{\hat{j}} = -\rho \mathbf{\hat{\rho}}
$$

其中 $\mathbf{\hat{\rho}}$ 是径向的单位向量。这个结果明确表明，[基矢](@entry_id:199546) $\mathbf{g}_\phi$ 的导数不为零。[基矢](@entry_id:199546)本身在空间中的变化，是[曲线坐标系](@entry_id:172561)理论的核心，也是后续引入[协变导数](@entry_id:152476)等概念的根本原因。

### [度规张量](@entry_id:160222)：测量距离

一旦我们建立了局域[基矢](@entry_id:199546)，下一步就是定义如何在这个框架下测量距离。空间中两个无限接近的点，其位置向量之差 $d\mathbf{r}$ 可以表示为：

$$
d\mathbf{r} = \frac{\partial \mathbf{r}}{\partial u^i} du^i = \mathbf{e}_i du^i
$$

（这里我们使用了爱因斯坦求和约定，即重复的上下标表示对所有坐标分量求和）。这两点之间的距离平方 $ds^2$，即**线元 (line element)**，由 $d\mathbf{r}$ 的自身[点积](@entry_id:149019)给出：

$$
ds^2 = d\mathbf{r} \cdot d\mathbf{r} = (\mathbf{e}_i du^i) \cdot (\mathbf{e}_j du^j) = (\mathbf{e}_i \cdot \mathbf{e}_j) du^i du^j
$$

我们将括号中的量定义为**协变度规张量 (covariant metric tensor)** 的分量：

$$
g_{ij} = \mathbf{e}_i \cdot \mathbf{e}_j
$$

于是，[线元](@entry_id:196833)可以简洁地写为：

$$
ds^2 = g_{ij} du^i du^j
$$

度规张量 $g_{ij}$ 是[曲线坐标系](@entry_id:172561)中最核心的对象。它包含了所有关于空间局部几何的信息：对角分量 $g_{ii} = |\mathbf{e}_i|^2$ 关系到沿坐标曲线的长度尺度，而非对角分量 $g_{ij}$ ($i \neq j$) 则关系到不同坐标曲线之间的夹角。

例如，在二维极坐标 $(r, \theta)$ 中，我们有 $x = r \cos\theta, y = r \sin\theta$。线元 $ds^2 = dx^2 + dy^2$ 可以通过计算[微分](@entry_id:158718)得到：
$dx = \cos\theta dr - r\sin\theta d\theta$
$dy = \sin\theta dr + r\cos\theta d\theta$
代入并化简后得到：
$$
ds^2 = (dr)^2 + r^2 (d\theta)^2
$$
将此表达式与 $ds^2 = g_{ij} du^i du^j$ 对比，我们可以直接读出极坐标下的度规张量分量：$g_{rr} = 1$, $g_{\theta\theta} = r^2$, $g_{r\theta} = 0$。这个结果也可以通过计算[协变基](@entry_id:198968)矢的[点积](@entry_id:149019)得到。这个[线元](@entry_id:196833)公式是计算曲线路径长度的基础。例如，计算一条由 $r(\theta) = r_0 \exp(k\theta)$ 定义的[对数螺线](@entry_id:174157)的[弧长](@entry_id:191173)，就需要对 $ds = \sqrt{r^2 + (\frac{dr}{d\theta})^2} d\theta$ 进行积分 [@problem_id:1503634]。

度规张量的结构直接反映了[坐标系](@entry_id:156346)的**正交性 (orthogonality)**。如果一个[坐标系](@entry_id:156346)是正交的，那么在任意一点，不同的坐标曲线都是相互垂直的。这意味着[协变基](@entry_id:198968)矢是相互正交的，即 $\mathbf{e}_i \cdot \mathbf{e}_j = 0$ 当 $i \neq j$。因此，对于一个[正交坐标](@entry_id:166074)系，度规张量矩阵是一个对角矩阵。我们熟悉的笛卡尔、[柱坐标](@entry_id:271645)和球坐标系都属于[正交坐标](@entry_id:166074)系。

反之，如果一个[坐标系](@entry_id:156346)是非正交的，那么至少存在一对非对角的度规分量 $g_{ij}$ ($i \neq j$) 不为零。考虑一个由 $x = q_1^2 - q_2^2, y = q_1 q_2$ 定义的二维[坐标系](@entry_id:156346) [@problem_id:1491050]。其[协变基](@entry_id:198968)矢为 $\mathbf{e}_1 = 2q_1\mathbf{\hat{i}} + q_2\mathbf{\hat{j}}$ 和 $\mathbf{e}_2 = -2q_2\mathbf{\hat{i}} + q_1\mathbf{\hat{j}}$。非对角度规分量 $g_{12}$ 为：

$$
g_{12} = \mathbf{e}_1 \cdot \mathbf{e}_2 = (2q_1)(-2q_2) + (q_2)(q_1) = -3q_1 q_2
$$

由于 $g_{12}$ 通常不为零，这个[坐标系](@entry_id:156346)是非正交的。

度规张量的[行列式](@entry_id:142978)，记为 $g = \det(g_{ij})$，也具有深刻的几何意义。它与坐标变换的雅可比行列式 $J = \det(\frac{\partial(x,y,z)}{\partial(u^1,u^2,u^3)})$ 有关，具体关系为 $g = J^2$。更重要的是，在[曲线坐标系](@entry_id:172561)中，无穷小体积（或面积）元由 $dV = \sqrt{g} \, du^1 du^2 du^3$ 给出。例如，对于一个由 $x = L u^1 u^2, y = \frac{L}{2}((u^2)^2 - (u^1)^2)$ 定义的二维[坐标系](@entry_id:156346)，其度规张量可以计算为对角阵，对角元为 $g_{11} = g_{22} = L^2((u^1)^2 + (u^2)^2)$ [@problem_id:1491046]。其[行列式](@entry_id:142978)为 $g = \det(g_{ij}) = L^4((u^1)^2+(u^2)^2)^2$。相应的面积元就是 $dA = \sqrt{g} du^1 du^2 = L^2((u^1)^2+(u^2)^2) du^1 du^2$。

### 对偶[基矢](@entry_id:199546)与逆变度规

[协变基](@entry_id:198968)矢 $\mathbf{e}_i$ 构成了描述切空间（即向量所在空间）的一个良好基底。然而，在[张量分析](@entry_id:161423)中，引入一个“对偶”的[基矢](@entry_id:199546)集合会带来极大的便利。这组[基矢](@entry_id:199546)被称为**[逆变基](@entry_id:197906)矢 (contravariant basis vectors)**，记为 $\mathbf{e}^j$，它们通过与[协变基](@entry_id:198968)矢的**互易关系 (reciprocity relation)** 来定义：

$$
\mathbf{e}_i \cdot \mathbf{e}^j = \delta_i^j
$$

其中 $\delta_i^j$ 是克罗内克符号（当 $i=j$ 时为1，否则为0）。这个关系表明，$\mathbf{e}^1$ 垂直于 $\mathbf{e}_2$ 和 $\mathbf{e}_3$ 所在的平面，$\mathbf{e}^2$ 垂直于 $\mathbf{e}_1$ 和 $\mathbf{e}_3$ 所在的平面，以此类推。

与协变度规张量相似，我们可以利用[逆变基](@entry_id:197906)矢定义**[逆变](@entry_id:192290)[度规张量](@entry_id:160222) (contravariant metric tensor)**：

$$
g^{ij} = \mathbf{e}^i \cdot \mathbf{e}^j
$$

协变和[逆变](@entry_id:192290)[度规张量](@entry_id:160222)之间有一个至关重要的代数关系：它们互为矩阵的逆。也就是说，如果我们将 $g_{ij}$ 和 $g^{ij}$ 看作矩阵，那么 $[g_{ij}][g^{jk}] = [\delta_i^k]$，即[单位矩阵](@entry_id:156724)。这个性质可以通过定义推导得出：

$$
g_{ik}g^{kj} = (\mathbf{e}_i \cdot \mathbf{e}_k)(\mathbf{e}^k \cdot \mathbf{e}^j) = \mathbf{e}_i \cdot (\mathbf{e}_k (\mathbf{e}^k \cdot \mathbf{e}^j))
$$

由于 $\mathbf{e}^k$ 构成了[完备基](@entry_id:143908)矢，$\sum_k \mathbf{e}_k (\mathbf{e}^k \cdot \mathbf{A}) = \mathbf{A}$ 对任意向量 $\mathbf{A}$ 成立。令 $\mathbf{A} = \mathbf{e}^j$，我们得到 $\sum_k \mathbf{e}_k (\mathbf{e}^k \cdot \mathbf{e}^j) = \mathbf{e}^j$。因此：

$$
g_{ik}g^{kj} = \mathbf{e}_i \cdot \mathbf{e}^j = \delta_i^j
$$

这个[逆关系](@entry_id:274206)使得我们能够方便地在协变和[逆变分量](@entry_id:185440)之间转换。例如，对于一个[正交坐标](@entry_id:166074)系，其协变度规矩阵 $[g_{ij}]$ 是对角的。其[逆矩阵](@entry_id:140380) $[g^{ij}]$ 也是对角的，对角元素为原矩阵对角元素的倒数。例如，在[抛物线坐标](@entry_id:166304) $(u, v)$ 中，协变度规为 $g_{ij} = (u^2+v^2)\begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}$。其逆变度规就是 $[g^{ij}] = \frac{1}{u^2+v^2}\begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}$ [@problem_id:1503592]。

对于[非正交坐标](@entry_id:194871)系，计算[逆矩阵](@entry_id:140380)会复杂一些。考虑一个由 $x = u + v\cos\alpha, y = v\sin\alpha$ 定义的二维斜角[坐标系](@entry_id:156346) [@problem_id:1503600]。其协变[度规张量](@entry_id:160222)矩阵为：

$$
[g_{ij}] = \begin{pmatrix} 1  \cos\alpha \\ \cos\alpha  1 \end{pmatrix}
$$

其[行列式](@entry_id:142978)为 $\det[g_{ij}] = 1 - \cos^2\alpha = \sin^2\alpha$。利用二维[矩阵求逆](@entry_id:636005)公式，我们得到[逆变](@entry_id:192290)[度规张量](@entry_id:160222)矩阵：

$$
[g^{ij}] = \frac{1}{\sin^2\alpha} \begin{pmatrix} 1  -\cos\alpha \\ -\cos\alpha  1 \end{pmatrix}
$$

从中我们可以读出非对角分量 $g^{uv} = -\frac{\cos\alpha}{\sin^2\alpha}$。

### [曲线坐标系](@entry_id:172561)中的[微分](@entry_id:158718)：[协变导数](@entry_id:152476)

在笛卡尔坐标系中，对一个矢量场 $\mathbf{V} = V_x \mathbf{\hat{i}} + V_y \mathbf{\hat{j}} + V_z \mathbf{\hat{k}}$ 求偏导数很简单，因为[基矢](@entry_id:199546) $(\mathbf{\hat{i}}, \mathbf{\hat{j}}, \mathbf{\hat{k}})$ 是常数：$\frac{\partial \mathbf{V}}{\partial x} = \frac{\partial V_x}{\partial x}\mathbf{\hat{i}} + \dots$。然而，在[曲线坐标系](@entry_id:172561)中，情况变得复杂。一个矢量场可以表示为其分量与局域[基矢](@entry_id:199546)的乘[积之和](@entry_id:266697) $\mathbf{V} = V^i \mathbf{e}_i$。对其求[偏导数](@entry_id:146280)时，根据乘法法则，必须同时考虑分量和[基矢](@entry_id:199546)的变化：

$$
\frac{\partial \mathbf{V}}{\partial u^k} = \frac{\partial (V^i \mathbf{e}_i)}{\partial u^k} = \frac{\partial V^i}{\partial u^k} \mathbf{e}_i + V^i \frac{\partial \mathbf{e}_i}{\partial u^k}
$$

我们已经知道，第二项 $\frac{\partial \mathbf{e}_i}{\partial u^k}$ 通常不为零。这个导数本身也是一个向量，因此可以写成局域[基矢](@entry_id:199546)的[线性组合](@entry_id:154743)：

$$
\frac{\partial \mathbf{e}_i}{\partial u^k} = \Gamma^l_{ki} \mathbf{e}_l
$$

这里的系数 $\Gamma^l_{ki}$ 被称为**[克里斯托费尔符号](@entry_id:159831) (Christoffel symbols)** (或连接系数)，它们精确地量化了[基矢](@entry_id:199546)在空间中的变化率。

我们可以通过一个具体的例子来理解这些系数的来源。在一个二维平面上，一辆探测车使用极坐标 $(r, \theta)$ 导航 [@problem_id:1503644]。其[协变基](@entry_id:198968)矢为 $\mathbf{g}_r = \hat{\mathbf{e}}_r$ 和 $\mathbf{g}_\theta = r \hat{\mathbf{e}}_\theta$。径向[基矢](@entry_id:199546) $\mathbf{g}_r$ 随角度 $\theta$ 的变化率为：

$$
\frac{\partial \mathbf{g}_r}{\partial \theta} = \frac{\partial \hat{\mathbf{e}}_r}{\partial \theta} = \hat{\mathbf{e}}_\theta
$$

为了将结果表示在[协变基](@entry_id:198968)矢 $\{ \mathbf{g}_r, \mathbf{g}_\theta \}$ 下，我们注意到 $\hat{\mathbf{e}}_\theta = \frac{1}{r} \mathbf{g}_\theta$。因此：

$$
\frac{\partial \mathbf{g}_r}{\partial \theta} = 0 \cdot \mathbf{g}_r + \frac{1}{r} \mathbf{g}_\theta
$$

与 $\frac{\partial \mathbf{e}_i}{\partial u^k} = \Gamma^l_{ki} \mathbf{e}_l$ 对比（这里 $i=r, k=\theta$），我们直接读出 $\Gamma^r_{\theta r} = 0$ 和 $\Gamma^\theta_{\theta r} = \frac{1}{r}$。

尽管克里斯托费尔符号可以通过对[基矢](@entry_id:199546)求导来定义，但在实际计算中，更常用的是一个只依赖于度规张量及其导数的公式：

$$
\Gamma^k_{ij} = \frac{1}{2} g^{k\ell} \left( \frac{\partial g_{j\ell}}{\partial u^i} + \frac{\partial g_{i\ell}}{\partial u^j} - \frac{\partial g_{ij}}{\partial u^\ell} \right)
$$

这个公式的强大之处在于，只要给定了一个空间的度规 $g_{ij}$，我们就可以计算出所有的连接系数，而无需知道该空间是否以及如何嵌入到更高维的欧氏空间中。例如，对于由线元 $ds^2 = \frac{1}{v^2}(du^2 + dv^2)$ 定义的[庞加莱半平面](@entry_id:271950)（一种非欧几何空间），我们可以利用此公式计算出 $\Gamma^v_{uu} = \frac{1}{v}$ [@problem_id:1503617]。

有了克里斯托费尔符号，我们就可以定义一个正确的微分算子——**[协变导数](@entry_id:152476) (covariant derivative)**，记为 $\nabla$。它能够正确处理[基矢](@entry_id:199546)的变化，并保证对一个张量求导的结果仍然是一个张量。对于一个逆变矢量场 $V^i$，其[协变导数](@entry_id:152476)的分量为：

$$
(\nabla_k V)^i \equiv V^i_{;k} = \frac{\partial V^i}{\partial u^k} + \Gamma^i_{kj} V^j
$$

对于一个[协变矢量](@entry_id:263917)场 $A_j$，其协变导数的分量为：

$$
(\nabla_k A)_j \equiv A_{j;k} = \frac{\partial A_j}{\partial u^k} - \Gamma^i_{kj} A_i
$$

协变导数由普通[偏导数](@entry_id:146280)和包含克里斯托费尔符号的“修正项”组成。这些修正项恰好抵消了因[基矢](@entry_id:199546)变化而产生的非张量性部分。这个定义可以推广到任意阶的张量。例如，在一个理论模型中，需要计算一个三阶张量 $T^i_{jk}$ 的散度 $R_{jk} = \nabla_i T^i_{jk}$ [@problem_id:1503582]。这需要应用[协变导数](@entry_id:152476)对[混合张量](@entry_id:182079)的完整法则，最终的计算依赖于给定度规（如极坐标度规）下的克里斯托费尔符号。

### 应用：[最短路径](@entry_id:157568)——[测地线](@entry_id:269969)

有了[曲线坐标系](@entry_id:172561)的完整数学工具，我们便可以解决一个基本而深刻的几何问题：寻找连接两点的最短路径。在[平直空间](@entry_id:204618)中，答案是直线。但在一个弯曲的[曲面](@entry_id:267450)或空间（即[黎曼流形](@entry_id:261160)）中，这条路径被称为**[测地线](@entry_id:269969) (geodesic)**。[测地线](@entry_id:269969)是“最直”的可能路径，是自由粒子在没有外力作用下会遵循的轨迹。

描述[测地线](@entry_id:269969)的方程可以通过变分法得到，即寻找使得路径[长度泛函](@entry_id:203503) $S = \int ds = \int \sqrt{g_{ij} \frac{dx^i}{d\tau} \frac{dx^j}{d\tau}} d\tau$ 取[极值](@entry_id:145933)的曲线。这等价于求解一组[二阶常微分方程](@entry_id:204212)，即**[测地线方程](@entry_id:264349)**：

$$
\frac{d^2 x^k}{d\tau^2} + \Gamma^k_{ij} \frac{dx^i}{d\tau} \frac{dx^j}{d\tau} = 0
$$

其中 $\tau$ 是路径的[仿射参数](@entry_id:260625)（如[弧长](@entry_id:191173)）。这个方程优雅地表明，一个物体的“加速度”（左边第一项）是由空间的几何（由[克里斯托费尔符号](@entry_id:159831) $\Gamma^k_{ij}$ 编码）和物体自身的速度共同决定的。

在处理具有对称性的问题时，使用[拉格朗日力学](@entry_id:147054)的[变分方法](@entry_id:163656)通常更为强大。[测地线](@entry_id:269969)问题等价于求解[拉格朗日量](@entry_id:174593) $L = \frac{1}{2} g_{ij} \dot{x}^i \dot{x}^j$ 的[欧拉-拉格朗日方程](@entry_id:137827)。如果度规张量 $g_{ij}$ 不显式依赖于某个坐标 $x^k$（称 $x^k$ 为[循环坐标](@entry_id:166220)），那么根据诺特定理，存在一个守恒量，即与该坐标对应的[广义动量](@entry_id:165699) $p_k = \frac{\partial L}{\partial \dot{x}^k} = g_{ki} \dot{x}^i$。

一个绝佳的例子是研究一个[质点](@entry_id:186768)在由 $z = k\rho^2$ 定义的旋转[抛物面](@entry_id:264713)上的无摩擦运动 [@problem_id:1503639]。首先，我们[参数化曲面](@entry_id:181980)并导出其度规：$ds^2 = (1+4k^2\rho^2)(d\rho)^2 + \rho^2(d\phi)^2$。相应的[拉格朗日量](@entry_id:174593)为 $L = \frac{1}{2} ((1+4k^2\rho^2)\dot{\rho}^2 + \rho^2\dot{\phi}^2)$。

由于度规和拉格朗日量都不显式依赖于角坐标 $\phi$，$\phi$ 是一个[循环坐标](@entry_id:166220)。因此，其对应的[广义动量守恒](@entry_id:168018)：

$$
J = \frac{\partial L}{\partial \dot{\phi}} = g_{\phi\phi}\dot{\phi} = \rho^2 \dot{\phi} = \text{常数}
$$

这个[守恒量](@entry_id:150267)（物理上对应于绕[对称轴](@entry_id:177299)的角动量）在整个[测地线](@entry_id:269969)上保持不变。通过在初始点（例如 $\rho=\rho_0$）将这个[守恒量](@entry_id:150267)与[质点](@entry_id:186768)的初始速度条件联系起来，并在路径的转折点（即[径向速度](@entry_id:159824) $\dot{\rho}=0$ 的点）应用此守恒律，我们可以求解出路径能达到的最小径向距离 $\rho_{\text{min}}$。这个结果，即著名的[克莱罗关系](@entry_id:159248)（Clairaut's relation）的一个特例，展示了[曲线坐标系](@entry_id:172561)的整个理论框架——从定义[基矢](@entry_id:199546)和度规，到利用其对称性寻找守恒律——如何被用来解决复杂的物理问题。