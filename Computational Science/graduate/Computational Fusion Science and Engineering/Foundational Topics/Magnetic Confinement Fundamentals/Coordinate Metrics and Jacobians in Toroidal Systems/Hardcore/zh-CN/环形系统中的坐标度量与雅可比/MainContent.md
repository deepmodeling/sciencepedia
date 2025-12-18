## 引言
在受控核聚变研究领域，[托卡马克](@entry_id:160432)和[仿星器](@entry_id:160569)等环形装置是实现持久聚变反应的最有希望的途径。然而，这些装置固有的环形几何结构给物理描述带来了巨大的挑战。我们熟悉的、无处不在的[笛卡尔坐标系](@entry_id:169789)在这种弯曲、封闭的空间中变得力不从心，无法有效描述等离子体的复杂边界和内部嵌套的磁面结构。为了精确地建立和求解描述等离子体行为的物理方程，我们必须掌握一套更为强大的数学语言——[曲线坐标系](@entry_id:172561)及其相关的几何工具。

本文旨在系统地填补这一知识缺口，为读者提供在环形系统中进行物理分析和[计算建模](@entry_id:144775)所需的几何基础。我们将从最基本的原理出发，深入探讨坐标[度规张量](@entry_id:160222)和雅可比行列式这两个核心概念。读者将学习到，这些看似抽象的数学量是如何精确地量化空间的局部弯曲、长度、面积和体积，并成为连接理论物理与计算模拟的桥梁。

在接下来的章节中，我们将分步构建这一知识体系。首先，在“原理与机制”一章中，我们将建立[曲线坐标系](@entry_id:172561)的数学框架，从[笛卡尔坐标](@entry_id:167698)出发推导出[协变基](@entry_id:198968)矢、[度规张量](@entry_id:160222)和[雅可比行列式](@entry_id:137120)，并阐明它们在矢量和[张量分析](@entry_id:161423)中的作用。随后，在“应用与跨学科联系”一章中，我们将展示这些工具在解决实际聚变问题中的威力，例如推导安全因子、进行磁面平均以分析输运，以及处理[仿星器](@entry_id:160569)和偏滤器中的复杂几何。最后，在“动手实践”部分，读者将通过具体的计算练习，巩固对理论的理解，并学习如何在实践中处理[坐标奇点](@entry_id:159160)等高级挑战。

## 原理与机制

在研究[托卡马克](@entry_id:160432)等环形[磁约束聚变](@entry_id:180408)装置中的等离子体物理时，我们必须放弃全局适用的[笛卡尔坐标系](@entry_id:169789)，转而使用能够适应复杂几何边界和内部[磁结构](@entry_id:201216)的[曲线坐标系](@entry_id:172561)。本章将从第一性原理出发，系统地阐述在环形系统中定义和使用[曲线坐标系](@entry_id:172561)所需的核心几何工具——[度规张量](@entry_id:160222)和雅可比行列式，并探讨它们在物理方程坐标变换中的关键作用。

### 从笛卡尔坐标到[曲线坐标](@entry_id:178535)：环形系统的基础

为了描述[环形等离子体](@entry_id:202484)，我们通常采用一套与环对称性相匹配的坐标。一个简单而基础的模型是圆形[截面](@entry_id:154995)的环形坐标系 $(r, \theta, \phi)$。此处的 $r$ 是小半径，表示从环形[截面](@entry_id:154995)中心到某点的距离；$\theta$ 是极向角，描述在[截面](@entry_id:154995)内的位置；$\phi$ 是环向角，描述沿环主体的位置。这些[曲线坐标](@entry_id:178535)通过一个映射与三维[欧几里得空间](@entry_id:138052)中的[笛卡尔坐标](@entry_id:167698) $(x, y, z)$ 联系起来。

一个标准的[参数化](@entry_id:265163)映射如下  ：
$$
x(r,\theta,\phi) = (R_0 + r \cos\theta)\cos\phi
$$
$$
y(r,\theta,\phi) = (R_0 + r \cos\theta)\sin\phi
$$
$$
z(r,\theta,\phi) = r \sin\theta
$$
其中 $R_0$ 是环的大半径，即从[对称轴](@entry_id:177299)到环体中心的距离。为保证坐标的有效性，我们通常假定 $r < R_0$，以避免几何自交。这个映射是后续所有几何量推导的起点。空间中任意一点的位置矢量 $\mathbf{r}$ 可以表示为这些坐标的函数：
$$
\mathbf{r}(r, \theta, \phi) = x(r, \theta, \phi)\,\hat{\mathbf{x}} + y(r, \theta, \phi)\,\hat{\mathbf{y}} + z(r, \theta, \phi)\,\hat{\mathbf{z}}
$$
其中 $(\hat{\mathbf{x}}, \hat{\mathbf{y}}, \hat{\mathbf{z}})$ 是[笛卡尔坐标系](@entry_id:169789)的单位基矢。

### 几何的语言：基矢与度规张量

在[曲线坐标系](@entry_id:172561)中，描述局部几何性质的基本工具是**[协变基](@entry_id:198968)矢**（covariant basis vectors）。对于任意一组[曲线坐标](@entry_id:178535) $(u^1, u^2, u^3)$，其[协变基](@entry_id:198968)矢 $\mathbf{e}_i$ 定义为位置矢量 $\mathbf{r}$ 沿该坐标方向的变化率：
$$
\mathbf{e}_i = \frac{\partial \mathbf{r}}{\partial u^i}
$$
这些基矢构成了每个点上的一个[局部坐标](@entry_id:181200)基底。它们的方向和长度随空间位置而变化，精确地捕捉了坐标网格的扭曲和伸缩。

对于我们之前定义的环形坐标系 $(r, \theta, \phi)$，我们可以通过对位置矢量 $\mathbf{r}$ 求[偏导数](@entry_id:146280)，直接计算出三个[协变基](@entry_id:198968)矢 ：

$$
\mathbf{e}_r = \frac{\partial \mathbf{r}}{\partial r} = \cos\theta \cos\phi \,\hat{\mathbf{x}} + \cos\theta \sin\phi \,\hat{\mathbf{y}} + \sin\theta \,\hat{\mathbf{z}}
$$

$$
\mathbf{e}_\theta = \frac{\partial \mathbf{r}}{\partial \theta} = -r \sin\theta \cos\phi \,\hat{\mathbf{x}} - r \sin\theta \sin\phi \,\hat{\mathbf{y}} + r \cos\theta \,\hat{\mathbf{z}}
$$

$$
\mathbf{e}_\phi = \frac{\partial \mathbf{r}}{\partial \phi} = -(R_0 + r \cos\theta) \sin\phi \,\hat{\mathbf{x}} + (R_0 + r \cos\theta) \cos\phi \,\hat{\mathbf{y}}
$$

有了[基矢](@entry_id:199546)，我们就可以定义**[协变](@entry_id:634097)[度规张量](@entry_id:160222)**（covariant metric tensor）$g_{ij}$。它的分量由[基矢](@entry_id:199546)之间的点积给出：
$$
g_{ij} = \mathbf{e}_i \cdot \mathbf{e}_j
$$
[度规张量](@entry_id:160222)是描述空间局部几何性质的核心，它包含了所有关于长度和角度的信息。空间中两点间的无穷小距离平方（[线元](@entry_id:196833)）$ds^2$ 可以用度规张量表示为：
$$
ds^2 = d\mathbf{r} \cdot d\mathbf{r} = \sum_{i,j} \left(\frac{\partial \mathbf{r}}{\partial u^i} \cdot \frac{\partial \mathbf{r}}{\partial u^j}\right) du^i du^j = \sum_{i,j} g_{ij} du^i du^j
$$

让我们为环形坐标系计算度规张量的分量  。对角分量为：
$$
g_{rr} = \mathbf{e}_r \cdot \mathbf{e}_r = (\cos\theta \cos\phi)^2 + (\cos\theta \sin\phi)^2 + (\sin\theta)^2 = 1
$$
$$
g_{\theta\theta} = \mathbf{e}_\theta \cdot \mathbf{e}_\theta = (-r \sin\theta \cos\phi)^2 + (-r \sin\theta \sin\phi)^2 + (r \cos\theta)^2 = r^2
$$
$$
g_{\phi\phi} = \mathbf{e}_\phi \cdot \mathbf{e}_\phi = (R_0 + r \cos\theta)^2 (\sin^2\phi + \cos^2\phi) = (R_0 + r \cos\theta)^2
$$
非对角分量，例如 $g_{r\theta}$，计算如下：
$$
g_{r\theta} = \mathbf{e}_r \cdot \mathbf{e}_\theta = -r \sin\theta \cos\theta (\cos^2\phi + \sin^2\phi) + r \sin\theta \cos\theta = 0
$$
通过类似的计算可以验证 $g_{r\phi} = 0$ 和 $g_{\theta\phi} = 0$。由于所有非对角分量均为零，我们得出结论：这个标准的圆形环坐标系是**正交**（orthogonal）的。这意味着在任意点，三个坐标轴方向都是相互垂直的。

对于[正交坐标](@entry_id:166074)系，我们可以定义**标度因子**（scale factors）$h_i = \sqrt{g_{ii}}$（无求和）。它们代表了[协变基](@entry_id:198968)矢的长度，即 $h_i = \|\mathbf{e}_i\|$。对于我们的例子：
$$
h_r = 1, \quad h_\theta = r, \quad h_\phi = R_0 + r \cos\theta
$$
[线元](@entry_id:196833) $ds^2$ 可以简化为各方向[弧长](@entry_id:191173)平方和：
$$
ds^2 = h_r^2 dr^2 + h_\theta^2 d\theta^2 + h_\phi^2 d\phi^2 = (dr)^2 + (r d\theta)^2 + ((R_0 + r \cos\theta) d\phi)^2
$$
这里，$dl_r = dr$，$dl_\theta = r d\theta$ 和 $dl_\phi = (R_0 + r \cos\theta) d\phi$ 分别是沿 $r, \theta, \phi$ 方向的无穷小[弧长](@entry_id:191173)。

### [度量空间](@entry_id:138860)：雅可比行列式与[体积元](@entry_id:267802)

在进行积分（如计算总粒子数或总能量）时，我们需要知道如何在[曲线坐标系](@entry_id:172561)中表示一个无穷小[体积元](@entry_id:267802) $dV$。这引出了**雅可比行列式**（Jacobian determinant）的概念。雅可比行列式 $J$ 衡量了[坐标变换](@entry_id:172727)导致的[体积缩放](@entry_id:197908)。它有两种等价的定义方式。

第一种定义来自于多元微[积分中的变量替换](@entry_id:140343)，即[坐标变换矩阵](@entry_id:151446)的行列式：
$$
J = \det\left(\frac{\partial(x,y,z)}{\partial(u^1,u^2,u^3)}\right) = \det\begin{pmatrix} \frac{\partial x}{\partial u^1} & \frac{\partial x}{\partial u^2} & \frac{\partial x}{\partial u^3} \\ \frac{\partial y}{\partial u^1} & \frac{\partial y}{\partial u^2} & \frac{\partial y}{\partial u^3} \\ \frac{\partial z}{\partial u^1} & \frac{\partial z}{\partial u^2} & \frac{\partial z}{\partial u^3} \end{pmatrix}
$$
矩阵的列向量正是[协变基](@entry_id:198968)矢 $\mathbf{e}_i$ 在[笛卡尔坐标系](@entry_id:169789)下的分量。因此，这个行列式等价于三个[协变基](@entry_id:198968)矢的[标量三重积](@entry_id:177480)（scalar triple product）：
$$
J = \mathbf{e}_1 \cdot (\mathbf{e}_2 \times \mathbf{e}_3)
$$
这个定义的结果带有一个符号，其正负取决于坐标系 $(u^1, u^2, u^3)$ 是[右手系](@entry_id:166669)还是左手系。

第二种定义将[雅可比行列式](@entry_id:137120)与[度规张量](@entry_id:160222)直接联系起来  。可以证明，[度规张量](@entry_id:160222)的行列式 $g = \det(g_{ij})$ 与雅可比行列式的平方满足关系：
$$
g = J^2 \quad \implies \quad |J| = \sqrt{g}
$$
这揭示了一个深刻的联系：空间的局部几何（由 $g_{ij}$ 描述）直接决定了体积的度量。

让我们再次以环形坐标系为例，计算其[雅可比行列式](@entry_id:137120)。使用第二种方法，因为我们已经知道[度规张量](@entry_id:160222)是对角的 ：
$$
g = \det(g_{ij}) = g_{rr} g_{\theta\theta} g_{\phi\phi} = (1)(r^2)(R_0 + r \cos\theta)^2
$$
因此，雅可比行列式的绝对值为：
$$
|J| = \sqrt{g} = \sqrt{r^2(R_0 + r \cos\theta)^2} = r(R_0 + r \cos\theta)
$$
（这里我们假定 $r \ge 0$ 且 $R_0 + r\cos\theta > 0$）。

这个结果具有清晰的几何解释 。一个无穷小体积元 $dV$ 可以看作是由三个正交的[弧长](@entry_id:191173) $dl_r, dl_\theta, dl_\phi$ 围成的一个微小长方体，其体积为 $dV = dl_r dl_\theta dl_\phi$。代入我们之前得到的[弧长](@entry_id:191173)表达式：
$$
dV = (dr) \cdot (r d\theta) \cdot ((R_0 + r \cos\theta) d\phi) = r(R_0 + r \cos\theta) \,dr d\theta d\phi
$$
比较 $dV = |J| dr d\theta d\phi$，我们立即得到 $|J| = r(R_0 + r \cos\theta)$。这个结果告诉我们，[体积元](@entry_id:267802)被拉伸了两个因子：
- 因子 $r$：这是从极向[角位移](@entry_id:171094) $d\theta$ 转换为[弧长](@entry_id:191173) $dl_\theta = r d\theta$ 所需的半径。
- 因子 $R_0 + r \cos\theta$：这是环向坐标的有效半径 $R = R_0 + r \cos\theta$。沿环向的[弧长](@entry_id:191173)为 $dl_\phi = R d\phi$。这个半径在环的外侧（$\theta=0$）最大，在内侧（$\theta=\pi$）最小，这解释了为何环外侧的体积元比内侧大。

### [曲线坐标系](@entry_id:172561)中的矢量与张量

在[曲线坐标系](@entry_id:172561)中处理矢量和张量时，我们需要区分两种类型的分量：**[逆变分量](@entry_id:185440)** (contravariant components) 和 **[协变](@entry_id:634097)分量** (covariant components)。

#### [协变与逆变](@entry_id:189600)分量

一个矢量 $\mathbf{V}$ 是一个不依赖于坐标系的几何对象。它可以展开在[协变基](@entry_id:198968)矢 $\mathbf{e}_i$ 上：
$$
\mathbf{V} = V^i \mathbf{e}_i \quad (\text{Einstein求和约定})
$$
这里的 $V^i$ 就是矢量的**[逆变分量](@entry_id:185440)**。

我们也可以引入一套**对偶基矢**（dual basis vectors）$\mathbf{e}^j$，其定义为 $\mathbf{e}^j \cdot \mathbf{e}_i = \delta^j_i$，其中 $\delta^j_i$ 是克罗内克符号。矢量 $\mathbf{V}$ 同样可以展开在对偶[基矢](@entry_id:199546)上：
$$
\mathbf{V} = V_j \mathbf{e}^j
$$
这里的 $V_j$ 就是矢量的**[协变](@entry_id:634097)分量**。[协变](@entry_id:634097)分量可以通过将矢量与[协变基](@entry_id:198968)矢做点积得到：$V_i = \mathbf{V} \cdot \mathbf{e}_i$。

[度规张量](@entry_id:160222)的作用正是在这两种分量之间进行转换，即所谓的“[升降指标](@entry_id:161292)” 。
将 $V_i = \mathbf{V} \cdot \mathbf{e}_i$ 与 $\mathbf{V} = V^j \mathbf{e}_j$ 结合，我们得到：
$$
V_i = (V^j \mathbf{e}_j) \cdot \mathbf{e}_i = (\mathbf{e}_j \cdot \mathbf{e}_i) V^j = g_{ij} V^j
$$
这便是“降低指标”的公式。为了“升高指标”，我们需要引入**逆变度规张量** $g^{ij}$，它定义为[协变](@entry_id:634097)度规张量矩阵 $(g_{ij})$ 的逆矩阵，即 $g^{ik}g_{kj} = \delta^i_j$。通过它，我们可以得到：
$$
V^i = g^{ij} V_j
$$
对于我们的正交环形坐标系，协变度规张量是[对角矩阵](@entry_id:637782)：
$$
g_{ij} = \begin{pmatrix} 1 & 0 & 0 \\ 0 & r^2 & 0 \\ 0 & 0 & (R_0 + r \cos\theta)^2 \end{pmatrix}
$$
其逆矩阵（逆变度规张量）同样是[对角矩阵](@entry_id:637782)，其对角元是原矩阵对角元的倒数 ：
$$
g^{ij} = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1/r^2 & 0 \\ 0 & 0 & 1/(R_0 + r \cos\theta)^2 \end{pmatrix}
$$
例如，给定一个矢量的协变分量 $A_\varphi = \gamma (R_0 + r\cos\theta)^3$，我们可以计算其逆变环向分量 $A^\varphi$：
$$
A^\varphi = g^{\varphi j} A_j = g^{\varphi\varphi} A_\varphi = \frac{1}{(R_0 + r \cos\theta)^2} \cdot \gamma (R_0 + r\cos\theta)^3 = \gamma (R_0 + r \cos\theta)
$$

#### 矢量与张量分量的坐标变换

当从一个坐标系 $u^i$ 变换到另一个坐标系 $u^{\prime a}$ 时，矢量和张量的分量也会随之改变。这个变换法则可以从[链式法则](@entry_id:190743)直接导出。

考虑从[柱坐标](@entry_id:271645) $(R, \phi, Z)$ 到环坐标 $(r, \theta, \phi)$ 的变换。一个矢量场 $\mathbf{V}$ 在[柱坐标](@entry_id:271645)中的分量为 $(V_R, V_\phi, V_Z)$。我们希望找到它在环坐标正交归一基底 $(\hat{\mathbf{e}}_r, \hat{\mathbf{e}}_\theta, \hat{\mathbf{e}}_\phi)$ 下的分量 $(V_r, V_\theta, V_\phi)$ 。通过将两个基底都用[笛卡尔](@entry_id:925811)[基矢](@entry_id:199546)表示，可以找到它们之间的关系：
$$
\hat{\mathbf{e}}_r = \cos\theta \hat{\mathbf{e}}_R + \sin\theta \hat{\mathbf{e}}_Z
$$
$$
\hat{\mathbf{e}}_\theta = -\sin\theta \hat{\mathbf{e}}_R + \cos\theta \hat{\mathbf{e}}_Z
$$
$$
\hat{\mathbf{e}}_\phi = \hat{\mathbf{e}}_\phi
$$
通过点积 $\mathbf{V} \cdot \hat{\mathbf{e}}_i$ 可以得到新分量：
$$
V_r = V_R \cos\theta + V_Z \sin\theta
$$
$$
V_\theta = -V_R \sin\theta + V_Z \cos\theta
$$
$$
V_\phi = V_\phi
$$
这个变换在 $(R,Z)$ 平面（即极向[截面](@entry_id:154995)）上等价于一个[坐标轴旋转](@entry_id:178802)，而环向分量保持不变。最终结果可以写作一个行矩阵：$\begin{pmatrix} V_{R} \cos\theta + V_{Z} \sin\theta & -V_{R} \sin\theta + V_{Z} \cos\theta & V_{\phi} \end{pmatrix}$。

这个思想可以推广到更高阶的张量。例如，一个二阶[逆变张量](@entry_id:636697) $T$ 的分量在[坐标变换](@entry_id:172727)下的法则是 ：
$$
T^{\prime ab} = \frac{\partial u^{\prime a}}{\partial u^i} \frac{\partial u^{\prime b}}{\partial u^j} T^{ij}
$$
其中 $\frac{\partial u^{\prime a}}{\partial u^i}$ 是坐标变换的[雅可比矩阵](@entry_id:178326)的元素。例如，考虑一个在[柱坐标系](@entry_id:266798) $(R, Z, \phi)$ 中只有对角分量 $T^{RR}=A$, $T^{ZZ}=C$, $T^{\phi\phi}=B$ 的张量，我们可以计算它在环坐标系中的 $T^{\theta\theta}$ 分量。根据变换法则：
$$
T^{\theta\theta} = \left(\frac{\partial \theta}{\partial R}\right)^2 T^{RR} + \left(\frac{\partial \theta}{\partial Z}\right)^2 T^{ZZ}
$$
通过计算反向变换的[雅可比矩阵](@entry_id:178326)，我们可以得到 $\frac{\partial \theta}{\partial R} = -\frac{\sin\theta}{r}$ 和 $\frac{\partial \theta}{\partial Z} = \frac{\cos\theta}{r}$。代入后得到：
$$
T^{\theta\theta} = A \left(-\frac{\sin\theta}{r}\right)^2 + C \left(\frac{\cos\theta}{r}\right)^2 = \frac{A \sin^2\theta + C \cos^2\theta}{r^2}
$$
这个例子展示了如何利用几何工具系统地处理物理量在不同坐标系之间的转换。

### 高等坐标系及其[奇点](@entry_id:266699)

#### [磁通坐标](@entry_id:1125149)系

在[磁约束聚变](@entry_id:180408)中，等离子体的输运主要沿磁力线方向发生，而垂直于磁面的输运则慢得多。因此，使用与磁面相适应的坐标系——**[磁通坐标](@entry_id:1125149)系**（flux coordinates）——会极大地简化物理模型。通常，我们使用 $(\psi, \theta, \phi)$，其中 $\psi$ 是标记嵌套磁面的**极向磁通**，$\theta$ 和 $\phi$ 依然是某种角度坐标。

在这种坐标系中，$\psi$ 通常是小半径 $r$ 的函数，$\psi=\psi(r)$。我们可以利用链式法则计算相关的几何量。例如，[协变基](@entry_id:198968)矢 $\mathbf{e}_\psi$ 变为 ：
$$
\mathbf{e}_\psi = \frac{\partial \mathbf{r}}{\partial \psi} = \frac{\partial \mathbf{r}}{\partial r} \frac{dr}{d\psi}
$$
这会直接影响到[雅可比行列式](@entry_id:137120)。对于前述的圆形[截面](@entry_id:154995)环，使用 $(\psi, \theta, \phi)$ 坐标，[雅可比行列式](@entry_id:137120)变为：
$$
J = \mathbf{e}_\psi \cdot (\mathbf{e}_\theta \times \mathbf{e}_\phi) = \left(\frac{dr}{d\psi} \mathbf{e}_r\right) \cdot (\mathbf{e}_\theta \times \mathbf{e}_\phi) = \frac{dr}{d\psi} [ \mathbf{e}_r \cdot (\mathbf{e}_\theta \times \mathbf{e}_\phi) ]
$$
代入之前为 $(r,\theta,\phi)$ 坐标系计算的[标量三重积](@entry_id:177480)，我们得到（注意符号）：
$$
J = -r(R_0 + r \cos\theta)\frac{dr}{d\psi}
$$
这个雅可比行列式定义了[体积元](@entry_id:267802) $dV = |J| d\psi d\theta d\phi$，它是数值求解输运方程的基础。它的逆 $J^{-1} = \nabla\psi \cdot (\nabla\theta \times \nabla\phi)$ 在理论分析中也同样重要。

#### [坐标奇点](@entry_id:159160)：磁轴与X点

虽然[曲线坐标系](@entry_id:172561)非常强大，但它们并非处处完美。在某些特殊点或线上，坐标系可能变得病态，这被称为**[坐标奇点](@entry_id:159160)**（coordinate singularities）。理解这些[奇点](@entry_id:266699)的性质对于保证数值计算的稳定性和准确性至关重要 。

**1. 磁轴 (Magnetic Axis, $r \to 0$)**

磁轴是环形磁面的中心，在几何上对应于 $r=0$ 的线。
- **[奇点](@entry_id:266699)性质**：当 $r \to 0$ 时，极向角 $\theta$ 变得没有意义，就像极坐标在原点角度未定义一样。这是一个典型的[坐标奇点](@entry_id:159160)。
- **几何量行为**：
    - 磁通梯度：若 $\psi \propto r^2$，则 $|\nabla \psi| \propto r \to 0$。
    - 度规分量：极向[弧长](@entry_id:191173) $dl_\theta = r d\theta \to 0$，导致[协变](@entry_id:634097)分量 $g_{\theta\theta} = r^2 \to 0$。其对应的[逆变分量](@entry_id:185440) $g^{\theta\theta} = 1/r^2 \to \infty$。同时，$g^{\psi\psi} = |\nabla\psi|^2 \propto r^2 \to 0$，而 $g_{\psi\psi} \propto 1/r^2 \to \infty$。
    - [雅可比行列式](@entry_id:137120)：尽管一些度规分量发散或趋于零，但它们的乘积在 $J^2 = g = g_{\psi\psi} g_{\theta\theta} g_{\phi\phi}$ 中相互抵消。$J^2 \approx (\frac{1}{r^2})(r^2)(R_0^2) = R_0^2$，因此雅可比行列式 $J$ 趋于一个**有限常数**。

**2. X点 (X-point)**

X点是磁分界面（separatrix）上的一个特殊点，磁面的拓扑结构在此处发生改变。它是 $\psi$ 的一个鞍点。
- **[奇点](@entry_id:266699)性质**：在[X点](@entry_id:1134148)，$\nabla\psi=0$，所以 $\psi$ 不能作为[局部坐标](@entry_id:181200)。同时，靠近分界面的磁面[周长](@entry_id:263239)会发散，使得定义一个单调的极向角 $\theta$ 变得困难。因此，$\psi$ 和 $\theta$ 坐标都在此失效。
- **几何量行为**：
    - 磁通梯度：$|\nabla\psi| \to 0$。
    - 度规分量：磁面[周长](@entry_id:263239)发散意味着[弧长](@entry_id:191173)元 $dl_\theta$ 在某些区域会变得非常大，因此 $g_{\theta\theta} \to \infty$。其对应的[逆变分量](@entry_id:185440) $g^{\theta\theta} \to 0$。由于 $|\nabla\psi| \to 0$，我们有 $g^{\psi\psi}=|\nabla\psi|^2 \to 0$，而其[协变](@entry_id:634097)伙伴 $g_{\psi\psi}$ 则会发散。
    - 雅可比行列式：$J$ 的表达式可以写作 $J = R\sqrt{g_{\theta\theta}}/|\nabla\psi|$。由于分子 $\sqrt{g_{\theta\theta}} \to \infty$ 而分母 $|\nabla\psi| \to 0$，雅可比行列式 $J$ 趋向于**无穷大**。

这些[奇点](@entry_id:266699)的存在，要求在进行[数值模拟](@entry_id:146043)时采用特殊的[网格生成技术](@entry_id:751906)或坐标系定义，以避免除以零或数值[溢出](@entry_id:172355)的问题，是计算聚变科学中的一个核心挑战。