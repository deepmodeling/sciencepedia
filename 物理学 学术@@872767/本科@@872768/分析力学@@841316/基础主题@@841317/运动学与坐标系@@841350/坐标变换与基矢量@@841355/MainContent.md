## 引言
在物理学的宏伟画卷中，运动的描述是其最核心的篇章。然而，描述运动的语言——[坐标系](@entry_id:156346)——的选择，往往决定了我们能否清晰地洞察物理规律的内在和谐。一个僵硬、不[匹配问题](@entry_id:275163)几何特征的[坐标系](@entry_id:156346)会使最简单的运动也变得异常繁琐，而一个精心选择的[坐标系](@entry_id:156346)则能化繁为简，让复杂的动力学问题迎刃而解。本文旨在系统地解决这一基本问题：我们如何在一个通用的数学框架下，自由地穿梭于不同的[坐标系](@entry_id:156346)之间？

本文将带领读者踏上一段从具体到抽象的旅程，构建起对坐标变换和[基向量](@entry_id:199546)的深刻理解。在“原理与机制”一章中，我们将从熟悉的[笛卡尔坐标系](@entry_id:169789)出发，深入学习如何定义和推导柱坐标、球坐标等[曲线坐标系](@entry_id:172561)的[基向量](@entry_id:199546)，并掌握它们之间变换的代数工具，如[旋转矩阵](@entry_id:140302)和Jacobian[行列式](@entry_id:142978)。接着，在“应用与跨学科联系”一章中，我们将看到这些数学工具如何在旋转参考系动力学、刚体运动、电磁学甚至[狭义相对论](@entry_id:275552)等广阔领域中大放异彩，揭示不同物理分支间的深刻联系。最后，通过“动手实践”部分，读者将有机会亲手解决具体问题，将理论知识转化为解决实际物理场景的强大能力。这趟旅程将为深入学习[分析力学](@entry_id:166738)乃至整个理论物理打下坚实的几何与[运动学](@entry_id:173318)基础。

## 原理与机制

在[分析力学](@entry_id:166738)中，我们描述物理系统运动的能力，在很大程度上取决于我们选择的数学框架。虽然[牛顿定律](@entry_id:163541)等基本物理原理在形式上是普适的，但它们在不同[坐标系](@entry_id:156346)中的数学表达却可能千差万别。一个精心选择的[坐标系](@entry_id:156346)可以极大地简化问题的求解过程，揭示系统内蕴的对称性。本章的目标是建立一个关于[坐标变换](@entry_id:172727)和相应[基向量](@entry_id:199546)变换的严谨框架。我们将从熟悉的[笛卡尔坐标系](@entry_id:169789)出发，逐步推广到更一般化的[曲线坐标系](@entry_id:172561)，并深入探讨这些变换背后的基本原理和[运动学](@entry_id:173318)机制。

### [基向量](@entry_id:199546)与[坐标系](@entry_id:156346)

描述空间中的一个点，最直接的方法是使用笛卡尔坐标系。在一个三维空间中，这通常由一个固定的原点和一组固定的、相互正交的单位[基向量](@entry_id:199546) $(\hat{i}, \hat{j}, \hat{k})$ 构成。空间中任意一点的位置向量 $\vec{r}$ 都可以唯一地表示为这些[基向量](@entry_id:199546)的线性组合：$\vec{r} = x\hat{i} + y\hat{j} + z\hat{k}$。这个体系的巨大优势在于其**全局性**和**不变性**：[基向量](@entry_id:199546)在空间中的每一点都是相同且固定的。

然而，许多物理问题具有特定的几何对称性，例如中心力场问题中的[球对称性](@entry_id:272852)或[绕轴旋转](@entry_id:185161)问题中的[轴对称](@entry_id:173333)性。在这些情况下，使用能够反映这种对称性的[坐标系](@entry_id:156346)会更加自然和便捷。这类[坐标系](@entry_id:156346)被称为**[曲线坐标系](@entry_id:172561)**（curvilinear coordinate systems）。与笛卡尔坐标系不同，[曲线坐标系](@entry_id:172561)的[基向量](@entry_id:199546)通常是**局域的**（local）和**位置依赖的**（position-dependent）。

要从根本上理解[曲线坐标系](@entry_id:172561)的[基向量](@entry_id:199546)，最系统的方法是通过位置向量对坐标的偏导数来定义它们。[假设空间](@entry_id:635539)中的一个点由一组[广义坐标](@entry_id:156576) $(q^1, q^2, q^3)$ 描述，其笛卡尔位置向量为 $\vec{r}(q^1, q^2, q^3)$。那么，在任意点，对应于坐标 $q^i$ 的**[协变基](@entry_id:198968)向量**（covariant basis vector） $\mathbf{e}_i$ 定义为：
$$
\mathbf{e}_i = \frac{\partial \vec{r}}{\partial q^i}
$$
这个向量的方向沿着该点的 $q^i$ 坐标线（即保持其他坐标不变时 $q^i$ 增加的方向）的[切线](@entry_id:268870)方向。这些[基向量](@entry_id:199546)的长度并不一定是单位长度，并且它们之间也未必正交。为了方便，我们通常会使用归一化后的**单位[基向量](@entry_id:199546)** $\hat{e}_i = \mathbf{e}_i / |\mathbf{e}_i|$。

#### 柱坐标与[球坐标](@entry_id:146054)

让我们通过两个最重要的[曲线坐标系](@entry_id:172561)来具体说明这个定义。

**[柱坐标系](@entry_id:266798) (Cylindrical Coordinates)**
柱坐标 $(\rho, \phi, z)$ 与笛卡尔坐标 $(x, y, z)$ 的关系为：
$$
x = \rho \cos\phi, \quad y = \rho \sin\phi, \quad z = z
$$
位置向量可以写作 $\vec{r} = \rho \cos\phi \hat{i} + \rho \sin\phi \hat{j} + z \hat{k}$。
根据定义，我们可以求出[协变基](@entry_id:198968)向量：
-   $\mathbf{e}_{\rho} = \frac{\partial \vec{r}}{\partial \rho} = \cos\phi \hat{i} + \sin\phi \hat{j}$
-   $\mathbf{e}_{\phi} = \frac{\partial \vec{r}}{\partial \phi} = -\rho \sin\phi \hat{i} + \rho \cos\phi \hat{j}$
-   $\mathbf{e}_{z} = \frac{\partial \vec{r}}{\partial z} = \hat{k}$

计算这些向量的模长：$|\mathbf{e}_{\rho}| = \sqrt{\cos^2\phi + \sin^2\phi} = 1$， $|\mathbf{e}_{\phi}| = \sqrt{(-\rho\sin\phi)^2 + (\rho\cos\phi)^2} = \rho$，以及 $|\mathbf{e}_{z}| = 1$。
因此，归一化后的单位[基向量](@entry_id:199546)为：
-   $\hat{\rho} = \cos\phi \hat{i} + \sin\phi \hat{j}$
-   $\hat{\phi} = -\sin\phi \hat{i} + \cos\phi \hat{j}$
-   $\hat{z} = \hat{k}$

可以看到，$\hat{\rho}$ 和 $\hat{\phi}$ 的方向取决于方位角 $\phi$，它们随着点的位置而改变。在一个半径为 $R$ 的圆盘边缘运动的传感器，其位置为 $(x, y)$，其沿逆时针方向的切向单位向量就可以用这种方式表达。由于 $x=R\cos\phi$ 和 $y=R\sin\phi$，代入 $\hat{\phi}$ 的表达式可得 $\hat{\phi} = - (y/R) \hat{i} + (x/R) \hat{j} = \frac{-y\hat{i} + x\hat{j}}{R}$，这与通过几何直觉得到的结果一致 [@problem_id:2042351]。

**球坐标系 (Spherical Coordinates)**
在物理学中，球坐标 $(r, \theta, \phi)$ 通常定义如下：$r$ 是径向距离，$ \theta$ 是从正 $z$ 轴向下测量的极角 ($0 \le \theta \le \pi$)，$ \phi$ 是在 $xy$ 平面内从正 $x$ 轴测量的方位角 ($0 \le \phi  2\pi$)。
$$
x = r \sin\theta \cos\phi, \quad y = r \sin\theta \sin\phi, \quad z = r \cos\theta
$$
位置向量为 $\vec{r} = r \sin\theta \cos\phi \hat{i} + r \sin\theta \sin\phi \hat{j} + r \cos\theta \hat{k}$。
我们再次应用偏导数的定义来推导单位[基向量](@entry_id:199546) [@problem_id:2042373]：
-   $\mathbf{e}_r = \frac{\partial \vec{r}}{\partial r} = \sin\theta\cos\phi \hat{i} + \sin\theta\sin\phi \hat{j} + \cos\theta \hat{k}$。其模长 $|\mathbf{e}_r|=1$，所以 $\hat{r} = \mathbf{e}_r$。
-   $\mathbf{e}_\theta = \frac{\partial \vec{r}}{\partial \theta} = r\cos\theta\cos\phi \hat{i} + r\cos\theta\sin\phi \hat{j} - r\sin\theta \hat{k}$。其模长 $|\mathbf{e}_\theta|=r$。因此，单位向量 $\hat{\theta} = \frac{\mathbf{e}_\theta}{r} = \cos\theta\cos\phi \hat{i} + \cos\theta\sin\phi \hat{j} - \sin\theta \hat{k}$。
-   $\mathbf{e}_\phi = \frac{\partial \vec{r}}{\partial \phi} = -r\sin\theta\sin\phi \hat{i} + r\sin\theta\cos\phi \hat{j}$。其模长 $|\mathbf{e}_\phi|=r\sin\theta$。因此，[单位向量](@entry_id:165907) $\hat{\phi} = \frac{\mathbf{e}_\phi}{r\sin\theta} = -\sin\phi \hat{i} + \cos\phi \hat{j}$。

这组[基向量](@entry_id:199546) $(\hat{r}, \hat{\theta}, \hat{\phi})$ 是相互正交的，构成一个[右手系](@entry_id:166669)。然而，至关重要的是，除了在特殊点（如 $z$ 轴上 $\hat{\phi}$ 未定义）外，它们的方向在空间中是逐点变化的，依赖于 $\theta$ 和 $\phi$。

### [坐标变换](@entry_id:172727)与基变换

从一个[坐标系转换](@entry_id:263003)到另一个[坐标系](@entry_id:156346)，不仅涉及到点坐标的代数关系变化，也隐含着[基向量](@entry_id:199546)之间的[线性变换](@entry_id:149133)关系。

#### [变换矩阵](@entry_id:151616)

我们已经得到了将[曲线坐标系](@entry_id:172561)的[基向量](@entry_id:199546)用笛卡尔基[向量表示](@entry_id:166424)的表达式。例如，在二维极坐标中：
$$
\hat{r} = \cos\theta \hat{i} + \sin\theta \hat{j}
$$
$$
\hat{\theta} = -\sin\theta \hat{i} + \cos\theta \hat{j}
$$
这可以写成矩阵形式：
$$
\begin{pmatrix} \hat{r} \\ \hat{\theta} \end{pmatrix} = \begin{pmatrix} \cos\theta  \sin\theta \\ -\sin\theta  \cos\theta \end{pmatrix} \begin{pmatrix} \hat{i} \\ \hat{j} \end{pmatrix}
$$
这个 $2 \times 2$ 的矩阵是一个**[旋转矩阵](@entry_id:140302)** $M(\theta)$。因为它联系的是两组正交单位基，所以它是一个**[正交矩阵](@entry_id:169220)**（orthogonal matrix），满足 $M^{-1} = M^T$（其逆等于其转置）。这个性质使得求解逆变换变得异常简单，即如何用极[坐标基](@entry_id:270149)向量来表示笛卡尔[基向量](@entry_id:199546) [@problem_id:2042359]。我们只需将上述关系左乘 $M(\theta)^{-1} = M(\theta)^T$：
$$
\begin{pmatrix} \hat{i} \\ \hat{j} \end{pmatrix} = \begin{pmatrix} \cos\theta  -\sin\theta \\ \sin\theta  \cos\theta \end{pmatrix} \begin{pmatrix} \hat{r} \\ \hat{\theta} \end{pmatrix}
$$
展开后得到：
$$
\hat{i} = \cos\theta \hat{r} - \sin\theta \hat{\theta}
$$
$$
\hat{j} = \sin\theta \hat{r} + \cos\theta \hat{\theta}
$$
这组关系在进行矢量运算，例如将作用在物体上的恒力（如重力，通常用 $\hat{j}$ 或 $\hat{k}$ 表示）分解到局域的极坐标或球坐标基上时，非常有用。

#### 变换下的[不变量](@entry_id:148850)

物理定律的正确性不应依赖于观察者选择的[坐标系](@entry_id:156346)。这意味着，在[坐标变换](@entry_id:172727)下，某些物理量应该保持不变。

一个矢量本身是一个几何对象，它的方向和大小是内在属性，不因[坐标系](@entry_id:156346)的改变而改变。然而，它的**分量**（components）会随着基的改变而改变。如果一个矢量 $\vec{V}$ 在 $S$ 系中的分量为列向量 $\mathbf{V}$，在一个旋转到 $S'$ 系中的分量为 $\mathbf{V}'$，那么 $\mathbf{V}'=R\mathbf{V}$，其中 $R$ 是旋转矩阵。

一个更基本的**[不变量](@entry_id:148850)**（invariant）是标量。两个矢量的**标积**（scalar product or dot product）就是一个典型的例子。标积的结果是一个不依赖于[坐标系](@entry_id:156346)的纯数。我们可以从代数上证明这一点：
假设有两个矢量 $\vec{A}$ 和 $\vec{B}$。在 $S$ 系中，它们的标积为 $\vec{A} \cdot \vec{B} = \mathbf{A}^T \mathbf{B}$。在 $S'$ 系中，标积为 $\vec{A}' \cdot \vec{B}' = \mathbf{A}'^T \mathbf{B}'$。代入变换关系 $\mathbf{A}' = R\mathbf{A}$ 和 $\mathbf{B}' = R\mathbf{B}$，我们得到：
$$
\mathbf{A}'^T \mathbf{B}' = (R\mathbf{A})^T (R\mathbf{B}) = \mathbf{A}^T R^T R \mathbf{B}
$$
由于 $R$ 是一个正交[旋转矩阵](@entry_id:140302)，$R^T R = I$（[单位矩阵](@entry_id:156724)）。因此：
$$
\vec{A}' \cdot \vec{B}' = \mathbf{A}^T I \mathbf{B} = \mathbf{A}^T \mathbf{B} = \vec{A} \cdot \vec{B}
$$
这证明了标积在[坐标旋转](@entry_id:164444)下是不变的。这个性质非常强大。例如，如果已知两个矢量在一个[坐标系](@entry_id:156346) $S$ 中的分量，我们就可以立即知道它们在任何其他[旋转坐标系](@entry_id:170324) $S'$ 中的标积，而无需知道具体的旋转矩阵 [@problem_id:2042366]。

#### Jacobian[行列式与体积](@entry_id:192291)元

坐标变换在积分运算中扮演着关键角色，尤其是在计算质量、[转动惯量](@entry_id:174608)等[多重积分](@entry_id:146170)时。从笛卡尔坐标 $(x, y, z)$ 变换到[曲线坐标](@entry_id:178535) $(q^1, q^2, q^3)$ 时，无穷小体积元 $dV$ 也需要相应变换。
$$
dV = dx\,dy\,dz = |J| \,dq^1\,dq^2\,dq^3
$$
这里的 $|J|$ 是**Jacobian[行列式](@entry_id:142978)**的[绝对值](@entry_id:147688)，它是一个缩放因子，反映了坐标变换如何拉伸或压缩空间。Jacobian矩阵 $J$ 定义为：
$$
J = \frac{\partial(x, y, z)}{\partial(q^1, q^2, q^3)} = \begin{pmatrix} \frac{\partial x}{\partial q^1}  \frac{\partial x}{\partial q^2}  \frac{\partial x}{\partial q^3} \\ \frac{\partial y}{\partial q^1}  \frac{\partial y}{\partial q^2}  \frac{\partial y}{\partial q^3} \\ \frac{\partial z}{\partial q^1}  \frac{\partial z}{\partial q^2}  \frac{\partial z}{\partial q^3} \end{pmatrix}
$$
Jacobian[行列式的几何意义](@entry_id:200059)是，它是由三个[协变基](@entry_id:198968)向量 $\mathbf{e}_1, \mathbf{e}_2, \mathbf{e}_3$ 张成的无穷小平行六面体的体积。

对于[球坐标系](@entry_id:167517)，我们可以计算出其Jacobian[行列式](@entry_id:142978)。经过直接但稍显繁琐的计算，可以得到一个简洁的结果：
$$
J = \det\begin{pmatrix} \frac{\partial x}{\partial r}  \frac{\partial x}{\partial \theta}  \frac{\partial x}{\partial \phi} \\ \frac{\partial y}{\partial r}  \frac{\partial y}{\partial \theta}  \frac{\partial y}{\partial \phi} \\ \frac{\partial z}{\partial r}  \frac{\partial z}{\partial \theta}  \frac{\partial z}{\partial \phi} \end{pmatrix} = r^2\sin\theta
$$
因此，[球坐标系](@entry_id:167517)中的体积元为 $dV = r^2\sin\theta \,dr\,d\theta\,d\phi$。这个 $r^2\sin\theta$ 因子在任何涉及球坐标的体积或[面积分](@entry_id:275394)中都至关重要。例如，在计算一个密度非均匀的球形部件的质量时，必须在积分中包含这个因子，否则结果将是错误的 [@problem_id:2042399]。

### [基向量](@entry_id:199546)的运动学

在动力学问题中，我们关心的是物体如何随时间运动。当使用[曲线坐标系](@entry_id:172561)描述一个运动的质点时，其坐标 $q^i(t)$ 是时间的函数。由于[基向量](@entry_id:199546) $\hat{e}_i$ 的方向依赖于坐标 $q^i$，所以当[质点](@entry_id:186768)运动时，描述其位置的局域[基向量](@entry_id:199546)本身也在随时间变化，即使它们始终保持单位长度。为了计算速度 ($\vec{v} = d\vec{r}/dt$) 和加速度 ($\vec{a} = d\vec{v}/dt$)，我们必须能够计算这些[基向量](@entry_id:199546)的时间导数。

[基向量](@entry_id:199546) $\hat{e}_i$ 是坐标 $(q^1, q^2, q^3)$ 的函数，而坐标又是时间的函数，因此我们可以使用链式法则来计算其时间导数：
$$
\dot{\hat{e}}_i = \frac{d\hat{e}_i}{dt} = \sum_j \frac{\partial \hat{e}_i}{\partial q^j} \frac{dq^j}{dt} = \sum_j \dot{q}^j \frac{\partial \hat{e}_i}{\partial q^j}
$$
这是一个极其重要的结果。它表明，[基向量](@entry_id:199546)的变化率是[广义速度](@entry_id:178456) $\dot{q}^j$ 的[线性组合](@entry_id:154743)。

让我们以[球坐标系](@entry_id:167517)为例，完整地推导其[基向量](@entry_id:199546)的时间导数 [@problem_id:2042387]。我们需要计算 $\dot{\hat{r}}$, $\dot{\hat{\theta}}$, 和 $\dot{\hat{\phi}}$。这些导数本身是矢量，因此可以将它们分解在 $(\hat{r}, \hat{\theta}, \hat{\phi})$ 基上。

1.  **$\dot{\hat{r}}$的计算**:
    $$
    \dot{\hat{r}} = \dot{\theta} \frac{\partial \hat{r}}{\partial \theta} + \dot{\phi} \frac{\partial \hat{r}}{\partial \phi}
    $$
    通过对 $\hat{r}$ 的表达式求偏导，我们发现 $\frac{\partial \hat{r}}{\partial \theta} = \hat{\theta}$ 和 $\frac{\partial \hat{r}}{\partial \phi} = \sin\theta \hat{\phi}$。
    因此, $\dot{\hat{r}} = \dot{\theta}\hat{\theta} + \dot{\phi}\sin\theta \hat{\phi}$。

2.  **$\dot{\hat{\theta}}$的计算**:
    $$
    \dot{\hat{\theta}} = \dot{\theta} \frac{\partial \hat{\theta}}{\partial \theta} + \dot{\phi} \frac{\partial \hat{\theta}}{\partial \phi}
    $$
    同样，可以求得 $\frac{\partial \hat{\theta}}{\partial \theta} = -\hat{r}$ 和 $\frac{\partial \hat{\theta}}{\partial \phi} = \cos\theta \hat{\phi}$。
    因此, $\dot{\hat{\theta}} = -\dot{\theta}\hat{r} + \dot{\phi}\cos\theta \hat{\phi}$。

3.  **$\dot{\hat{\phi}}$的计算**:
    $$
    \dot{\hat{\phi}} = \dot{\theta} \frac{\partial \hat{\phi}}{\partial \theta} + \dot{\phi} \frac{\partial \hat{\phi}}{\partial \phi}
    $$
    我们发现 $\frac{\partial \hat{\phi}}{\partial \theta} = 0$，而 $\frac{\partial \hat{\phi}}{\partial \phi} = -(\sin\theta \hat{r} + \cos\theta \hat{\theta})$。
    因此, $\dot{\hat{\phi}} = -\dot{\phi}(\sin\theta \hat{r} + \cos\theta \hat{\theta}) = -\dot{\phi}\sin\theta \hat{r} - \dot{\phi}\cos\theta \hat{\theta}$。

我们可以将这组关系整理成矩阵形式：
$$
\begin{pmatrix} \dot{\hat{r}} \\ \dot{\hat{\theta}} \\ \dot{\hat{\phi}} \end{pmatrix} = \begin{pmatrix} 0  \dot{\theta}  \dot{\phi}\sin\theta \\ -\dot{\theta}  0  \dot{\phi}\cos\theta \\ -\dot{\phi}\sin\theta  -\dot{\phi}\cos\theta  0 \end{pmatrix} \begin{pmatrix} \hat{r} \\ \hat{\theta} \\ \hat{\phi} \end{pmatrix}
$$
这个 $3 \times 3$ 矩阵是一个**反对稱矩阵**（anti-symmetric matrix）。这并非偶然。对于任何刚性旋转的[坐标基](@entry_id:270149)，其[基向量](@entry_id:199546)的时间导数都可以表示为一个反对称矩阵与[基向量](@entry_id:199546)本身的乘积。这个矩阵的元素实际上编码了该局域[坐标系](@entry_id:156346)相对于惯性系的瞬时**角[速度矢量](@entry_id:269648)** $\vec{\omega}$ 的分量。

掌握了这些导数后，我们就可以通过对位置矢量 $\vec{r} = r\hat{r}$ 进行[微分](@entry_id:158718)来得到速度和加速度在球坐标系中的完整表达式。例如，速度为 $\vec{v} = \dot{\vec{r}} = \dot{r}\hat{r} + r\dot{\hat{r}} = \dot{r}\hat{r} + r\dot{\theta}\hat{\theta} + r\dot{\phi}\sin\theta \hat{\phi}$。

### 旋转的深入探讨

三维空间中的旋转行为比平移要复杂得多，其中最关键的特性是**[非对易性](@entry_id:153545)**（non-commutativity）：旋转的最终结果取决于旋转操作的顺序。

#### [无穷小旋转](@entry_id:166635)

尽管有限角度的旋转是不可交换的，但**[无穷小旋转](@entry_id:166635)**（infinitesimal rotations）却近似可交换，并且可以像矢量一样叠加。考虑一个位置矢量 $\vec{r}_0$ 绕一个由单位矢量 $\hat{n}$ 定义的轴旋转一个无穷小角度 $d\phi$。利用[Rodrigues旋转公式](@entry_id:165151)并在[小角度近似](@entry_id:145423)下（$\cos(d\phi) \approx 1, \sin(d\phi) \approx d\phi$），旋转后的矢量 $\vec{r}'$ 可以表示为 [@problem_id:2042371]：
$$
\vec{r}' \approx \vec{r}_0 + d\phi (\hat{n} \times \vec{r}_0)
$$
这个简单的[线性关系](@entry_id:267880)是[刚体动力学](@entry_id:142040)的基础，它将无穷小转动 $d\phi\hat{n}$ 与位置矢量的变化 $d\vec{r} = \vec{r}' - \vec{r}_0$ 直接联系起来。

#### [旋转生成元](@entry_id:154292)与对易子

为了更深刻地理解旋转的结构，我们可以引入**[旋转生成元](@entry_id:154292)**（generator of rotation）的概念。对于绕某个轴 $i$ 的旋转矩阵 $R_i(\theta)$，其生成元 $M_i$ (在物理学中常称为$J_i$) 定义为：
$$
M_i = \left. \frac{d R_i(\theta)}{d\theta} \right|_{\theta=0}
$$
生成元捕捉了旋转在[恒等变换](@entry_id:264671)处的“[瞬时变化率](@entry_id:141382)”。对于小角度，有 $R_i(\theta) \approx I + \theta M_i$。

让我们考察绕 $x$ 轴和 $y$ 轴旋转的生成元 [@problem_id:2042382]。通过对相应的[旋转矩阵](@entry_id:140302)求导，我们得到：
$$
M_x = \begin{pmatrix} 0  0  0 \\ 0  0  -1 \\ 0  1  0 \end{pmatrix}, \quad M_y = \begin{pmatrix} 0  0  1 \\ 0  0  0 \\ -1  0  0 \end{pmatrix}
$$
旋转的[非对易性](@entry_id:153545)体现在这些生成元的代数关系中。我们可以计算它们的**对易子**（commutator），定义为 $[M_x, M_y] = M_x M_y - M_y M_x$。
$$
M_x M_y = \begin{pmatrix} 0  0  0 \\ 1  0  0 \\ 0  0  0 \end{pmatrix}, \quad M_y M_x = \begin{pmatrix} 0  1  0 \\ 0  0  0 \\ 0  0  0 \end{pmatrix}
$$
所以，
$$
[M_x, M_y] = \begin{pmatrix} 0  -1  0 \\ 1  0  0 \\ 0  0  0 \end{pmatrix}
$$
我们立即认出这个结果。它正是绕 $z$ 轴旋转的生成元 $M_z$！这个关系 $[M_x, M_y] = M_z$ (以及它的[循环置换](@entry_id:272913)) 是三维旋转群[SO(3)](@entry_id:138200)的[李代数](@entry_id:137954)的核心。它精确地量化了旋转的顺序是如何重要的：先绕 $x$ 轴再绕 $y$ 轴的[无穷小旋转](@entry_id:166635)，与先绕 $y$ 轴再绕 $x$ 轴的[无穷小旋转](@entry_id:166635)，其差异是一个绕 $z$ 轴的[无穷小旋转](@entry_id:166635)。

### [广义坐标](@entry_id:156576)与张量

到目前为止，我们主要关注的是[正交坐标](@entry_id:166074)系。然而，[分析力学](@entry_id:166738)的框架允许我们使用更广义、甚至非正交的[坐标系](@entry_id:156346)。这就引出了张量的概念。

#### [协变基](@entry_id:198968)、[逆变基](@entry_id:197906)与度规张量

我们已经定义了**[协变基](@entry_id:198968)向量** $\mathbf{e}_i = \partial \vec{r} / \partial q^i$。它们与坐标线相切。在[非正交坐标](@entry_id:194871)系中，为了方便地分解矢量，我们还需要引入**[逆变基](@entry_id:197906)向量**（contravariant basis vector）或称**对偶[基向量](@entry_id:199546)**（dual basis vector） $\mathbf{e}^j$。它们由关系式 $\mathbf{e}_i \cdot \mathbf{e}^j = \delta_i^j$ 定义，其中 $\delta_i^j$ 是Kronecker delta。几何上，$\mathbf{e}^j$ 垂直于由除 $\mathbf{e}_j$ 之外的所有其他[协变基](@entry_id:198968)[向量张成](@entry_id:152883)的超曲面。

[坐标系](@entry_id:156346)的所有內蕴几何信息——即[基向量](@entry_id:199546)的长度和它们之间的夹角——都被编码在一个称为**度规张量**（metric tensor）的对象中。其协变分量 $g_{ij}$ 定义为[协变基](@entry_id:198968)向量之间的标积：
$$
g_{ij} = \mathbf{e}_i \cdot \mathbf{e}_j
$$
例如，对于一个由 $u=y/x, v=x^2+y^2$ 定义的非[正交曲线坐标](@entry_id:190233)系，我们可以计算[度规张量](@entry_id:160222)的分量。为了计算 $g_{uu} = \mathbf{e}_u \cdot \mathbf{e}_u$，我们需要先求出 $\mathbf{e}_u = \partial \vec{r} / \partial u$。这需要将 $x, y$ 表示为 $u, v$ 的函数，然后求偏导。完成这个计算后，我们可以得到 $g_{uu}$ [@problem_id:2042353]。这个过程虽然可能涉及复杂的代数运算，但它系统地揭示了[坐标系](@entry_id:156346)局域的几何结构。

#### 矢量与赝矢量

我们讨论的变换大多是连续的旋转。还有一种离散的变换也极为重要，即**[宇称变换](@entry_id:159187)**（parity transformation），或称空间反演。它将空间中每一点的位置矢量反号：$\vec{r} \to -\vec{r}$，即 $(x,y,z) \to (-x,-y,-z)$。

在[宇称变换](@entry_id:159187)下，不同的物理量表现不同。
- **[真矢量](@entry_id:190731)**（True Vector）或**[极矢量](@entry_id:184542)**（Polar Vector）：像位置、速度、力这样的矢量，在[宇称变换](@entry_id:159187)下会反号。$\vec{V} \to \vec{V}' = -\vec{V}$。
- **[赝矢量](@entry_id:196296)**（Pseudovector）或**[轴矢量](@entry_id:196296)**（Axial Vector）：像角动量、力矩、[磁场](@entry_id:153296)这样的矢量，在[宇称变换](@entry_id:159187)下符号保持不变。$\vec{P} \to \vec{P}' = +\vec{P}$。

一个典型的[赝矢量](@entry_id:196296)是由两个[极矢量](@entry_id:184542)的叉积生成的。考虑 $\vec{C} = \vec{A} \times \vec{B}$，其中 $\vec{A}$ 和 $\vec{B}$ 是[极矢量](@entry_id:184542)。在[宇称变换](@entry_id:159187)下，$\vec{A}' = -\vec{A}$ and $\vec{B}' = -\vec{B}$。那么新的[叉积](@entry_id:156672)为：
$$
\vec{C}' = \vec{A}' \times \vec{B}' = (-\vec{A}) \times (-\vec{B}) = (-1)(-1)(\vec{A} \times \vec{B}) = +\vec{C}
$$
可见，[叉积](@entry_id:156672)的结果 $\vec{C}$ 在[宇称变换](@entry_id:159187)下并未反号，因此它是一个[赝矢量](@entry_id:196296) [@problem_id:2042347]。区分矢量和[赝矢量](@entry_id:196296)在研究物理定律的对称性和守恒律时至关重要，特别是在电磁学和粒子物理学中。

本章我们建立了一套用于处理坐标变换和[基向量](@entry_id:199546)的数学工具。从具体的极坐标和[球坐标](@entry_id:146054)，到广义的[度规张量](@entry_id:160222)和[旋转生成元](@entry_id:154292)，这些概念构成了描述经典力学乃至更广阔物理领域的语言。掌握它们，是深入理解物理世界几何结构的必经之路。