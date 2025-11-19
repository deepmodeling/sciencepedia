## 引言
[泊松方程](@entry_id:143763)不仅是数学物理中的一个基本方程，更是学习和掌握有限元方法（FEM）的基石。对于许多初学者而言，从抽象的[偏微分方程理论](@entry_id:189232)到具体、高效的计算机代码实现之间存在着一道鸿沟。本文旨在通过深入剖析泊松方程这一[典范模型](@entry_id:198268)问题，系统性地架起这座桥梁，引领读者走过有限元分析的全过程。

本文将从最核心的数学原理出发，逐步深入到高级应用与跨学科的联系。在第一章**“原理与机制”**中，我们将建立[有限元法](@entry_id:749389)的理论基础，详细探讨如何从经典[微分方程](@entry_id:264184)形式过渡到弱形式，并引入伽辽金方法完成离散化。随后的第二章**“应用与[交叉](@entry_id:147634)学科联系”**将视野拓宽，展示如何利用多重网格等高级技术提升[计算效率](@entry_id:270255)，处理边界[奇点](@entry_id:137764)等复杂情况，并揭示[泊松方程](@entry_id:143763)在[计算流体力学](@entry_id:747620)、计算化学等前沿领域中的关键作用。最后，在**“动手实践”**部分，我们将通过一系列精心设计的问题，帮助读者巩固所学，将理论知识转化为实践能力。

现在，让我们从构建解决泊松方程的现代数学框架开始，深入探索其基本原理与实现机制。

## 原理与机制

本章旨在深入探讨[泊松方程](@entry_id:143763)作为有限元方法中一个[典范模型](@entry_id:198268)问题的核心原理与实现机制。我们将从其数学表述出发，逐步过渡到其弱形式，并最终阐明如何通过伽辽金方法和[有限元离散化](@entry_id:193156)来寻求其数值解。本章内容将为后续更复杂的应用和理论分析奠定坚实的基础。

### 模型问题：泊松方程

在深入探讨有限元方法之前，我们首先需要精确定义我们将要处理的连续问题。[泊松方程](@entry_id:143763)是一个[二阶线性偏微分方程](@entry_id:195856)，它在物理学和工程学的众多领域中都有广泛应用，例如静电学、热传导和[流体力学](@entry_id:136788)。其一般形式为：
$$
-\Delta u = f \quad \text{在 } \Omega \text{ 中}
$$
其中 $\Omega \subset \mathbb{R}^d$ 是一个有界区域，$u$ 是待求解的未知函数（例如温度或[电势](@entry_id:267554)），$f$ 是已知的源项，$\Delta$ 是[拉普拉斯算子](@entry_id:146319)，定义为 $\Delta u = \sum_{i=1}^{d} \frac{\partial^2 u}{\partial x_i^2}$。

为了得到唯一解，该方程必须辅以边界条件。常见的边界条件类型包括：
1.  **狄利克雷（Dirichlet）边界条件**：在边界 $\partial\Omega$ 上直接指定函数值，$u = g$。
2.  **诺伊曼（Neumann）边界条件**：在边界上指定函数的[法向导数](@entry_id:169511)，$\partial_{\mathbf{n}} u = g$，其中 $\partial_{\mathbf{n}} u = \nabla u \cdot \mathbf{n}$，$\mathbf{n}$ 为边界上的单位外[法向量](@entry_id:264185)。
3.  **罗宾（Robin）边界条件**：在边界上指定函数值与其[法向导数](@entry_id:169511)的[线性组合](@entry_id:154743)，$\partial_{\mathbf{n}} u + \alpha u = h$。

#### 经典解及其性质

一个自然的起点是**经典解（classical solution）**的概念。一个函数 $u$ 被称为[边值问题](@entry_id:193901)的经典解，如果它在区域内部逐点满足[偏微分方程](@entry_id:141332)，在边界上逐点满足边界条件，并且所有涉及的导数都是经典意义上连续的。为了使方程 $\Delta u = f$ 有意义，函数 $u$ 必须在区域 $\Omega$ 内部是二次连续可微的，即 $u \in C^2(\Omega)$。这就要求[源项](@entry_id:269111) $f$ 至少是连续的，即 $f \in C^0(\Omega)$。为了使边界条件有意义，函数 $u$ 必须能够连续地延伸到边界，即 $u \in C^0(\overline{\Omega})$，其中 $\overline{\Omega} = \Omega \cup \partial\Omega$ 是 $\Omega$ 的[闭包](@entry_id:148169)。相应地，边界数据也必须是连续的。因此，一个经典解的最低正则性要求是：$u \in C^2(\Omega) \cap C^0(\overline{\Omega})$，[源项](@entry_id:269111) $f \in C^0(\Omega)$，狄利克雷边界数据 $g \in C^0(\partial\Omega)$ [@problem_id:2579534]。需要强调的是，这是经典解的*定义*，更高阶的[正则性理论](@entry_id:194071)（如[椭圆正则性理论](@entry_id:203755)）可能会在更强的假设下证明解具有更好的光滑性，例如 $u \in C^2(\overline{\Omega})$。

[泊松方程](@entry_id:143763)是椭圆型[偏微分方程](@entry_id:141332)中最具[代表性](@entry_id:204613)的例子。我们可以从三个方面来刻画其核心性质 [@problem_id:2579536]：
1.  **阶数（Order）**：由于方程中出现的最高阶导数是二阶的（$\frac{\partial^2 u}{\partial x_i^2}$），所以它是一个**二阶**[偏微分方程](@entry_id:141332)。
2.  **线性（Linearity）**：作用于未知函数 $u$ 的算子 $L(u) = -\Delta u$ 是线性的。这意味着对于任意常数 $a, b$ 和函数 $u, v$，该算子满足 $L(au+bv) = aL(u)+bL(v)$。这是因为求导运算本身是线性的。
3.  **均匀椭圆性（Uniform Ellipticity）**：一个一般的[散度形式](@entry_id:748608)二阶算子可以写作 $L(u) = -\nabla \cdot (A(x) \nabla u)$。算子 $L(u) = -\Delta u$ 可以通过取系数矩阵 $A(x)$ 为单位矩阵 $I$ 来得到。均匀椭圆性的定义要求存在一个常数 $\alpha > 0$，使得对于所有向量 $\xi \in \mathbb{R}^d$ 和几乎所有的 $x \in \Omega$，不等式 $\xi^\top A(x) \xi \ge \alpha |\xi|^2$ 成立。对于拉普拉斯算子，$A(x)=I$，我们有 $\xi^\top I \xi = \xi^\top \xi = |\xi|^2$。因此，该不等式对于 $\alpha = 1$ 成立。这表明负[拉普拉斯算子](@entry_id:146319)是**均匀椭圆**的，其椭圆常数为 $1$。这一性质是保证解的存在性、唯一性和稳定性的关键。

### 变分（弱）形式

经典解的概念虽然直观，但其对[函数光滑性](@entry_id:161935)的要求过于苛刻，使得许多在物理上和工程上有意义的问题无法在其框架下求解（例如，当[源项](@entry_id:269111) $f$ 仅是平方可积而不是连续时）。为了克服这一限制，现代[偏微分方程理论](@entry_id:189232)引入了**弱解（weak solution）**的概念，它在更广义的函数空间中寻求问题的解。

#### 索伯列夫空间

弱形式的数学舞台是**索伯列夫空间（Sobolev spaces）**。对于泊松方程，最相关的空间是 $H^1(\Omega)$ 及其[子空间](@entry_id:150286) $H_0^1(\Omega)$ [@problem_id:2579530]。
-   **$H^1(\Omega)$ 空间**：该空间由所有属于 $L^2(\Omega)$（即在 $\Omega$ 上平方可积）的函数 $u$ 组成，其一阶**[弱导数](@entry_id:189356)（weak derivatives）**也属于 $L^2(\Omega)$。函数 $v_i \in L^2(\Omega)$ 被称为 $u$ 的第 $i$ 个弱[偏导数](@entry_id:146280)（记作 $\partial_i u$），如果对于所有光滑且在 $\Omega$ 内具有[紧支集](@entry_id:276214)的[检验函数](@entry_id:166589) $\phi \in C_c^\infty(\Omega)$，[分部积分公式](@entry_id:145262)都成立：$\int_\Omega u (\partial_i \phi) dx = - \int_\Omega v_i \phi dx$。$H^1(\Omega)$ 空间是一个希尔伯特空间，其标[准范数](@entry_id:753960)为 $\lVert u \rVert_{H^1(\Omega)} = \left( \lVert u \rVert_{L^2(\Omega)}^2 + \lVert \nabla u \rVert_{L^2(\Omega)}^2 \right)^{1/2}$，其中 $\lVert \nabla u \rVert_{L^2(\Omega)}^2 = \sum_{i=1}^d \lVert \partial_i u \rVert_{L^2(\Omega)}^2$。
-   **$H_0^1(\Omega)$ 空间**：该空间是处理齐次[狄利克雷边界条件](@entry_id:173524)（$u=0$ on $\partial\Omega$）的自然选择。它被定义为[光滑函数](@entry_id:267124)空间 $C_c^\infty(\Omega)$ 在 $H^1(\Omega)$ 范数下的闭包。直观上，它包含了所有在边界上“消失”的 $H^1(\Omega)$ 函数。对于具有良好边界（如[利普希茨边界](@entry_id:184843)）的区域，这个定义等价于[迹算子](@entry_id:183665)（trace operator）的核，即 $H_0^1(\Omega) = \{u \in H^1(\Omega) : \text{tr}(u)=0 \text{ on } \partial\Omega\}$。
-   **[范数等价](@entry_id:137561)性**：在 $H_0^1(\Omega)$ 空间上，由于**[庞加莱不等式](@entry_id:142086)（Poincaré inequality）**成立（对于有界区域），即存在常数 $C_P$ 使得 $\lVert u \rVert_{L^2(\Omega)} \le C_P \lVert \nabla u \rVert_{L^2(\Omega)}$ 对于所有 $u \in H_0^1(\Omega)$ 都成立，[半范数](@entry_id:264573) $|u|_{H^1(\Omega)} := \lVert \nabla u \rVert_{L^2(\Omega)}$ 成为了一个与完全 $H^1(\Omega)$ [范数等价](@entry_id:137561)的范数。但在 $H^1(\Omega)$ 空间中，由于非零[常数函数](@entry_id:152060)的梯度为零，该[半范数](@entry_id:264573)不是一个范数 [@problem_id:2579530]。

#### 弱形式的推导

推导[弱形式](@entry_id:142897)的核心步骤是：将原[偏微分方程](@entry_id:141332)乘以一个任意的**[检验函数](@entry_id:166589)（test function）** $v$，然后在整个区域 $\Omega$ 上积分，并使用分部积分（即[格林第一恒等式](@entry_id:170345)）将部分导数从待求函数 $u$ 转移到检验函数 $v$ 上。

我们从 $-\Delta u = f$ 出发，两边同乘 $v$ 并积分：
$$
-\int_{\Omega} (\Delta u) v \, dx = \int_{\Omega} f v \, dx
$$
应用[格林第一恒等式](@entry_id:170345)，我们得到：
$$
\int_{\Omega} \nabla u \cdot \nabla v \, dx - \int_{\partial\Omega} (\partial_{\mathbf{n}} u) v \, ds = \int_{\Omega} f v \, dx
$$
这个方程是所有后续推导的基石。如何处理边界积分项 $\int_{\partial\Omega} (\partial_{\mathbf{n}} u) v \, ds$ 取决于具体的边界条件。

-   **齐次狄利克雷边界条件** ($u=0$ on $\partial\Omega$)：在这种情况下，解 $u$ 和检验函数 $v$ 都取自 $H_0^1(\Omega)$。由于该空间中的函数在边界上的迹为零，[检验函数](@entry_id:166589) $v$ 在 $\partial\Omega$ 上为零，导致边界积分项自动消失。[弱形式](@entry_id:142897)简化为：寻找 $u \in H_0^1(\Omega)$，使得对于所有 $v \in H_0^1(\Omega)$，
    $$
    \int_{\Omega} \nabla u \cdot \nabla v \, dx = \int_{\Omega} f v \, dx
    $$

-   **自然边界条件**：诺伊曼和[罗宾边界条件](@entry_id:163914)被称为**自然边界条件（natural boundary conditions）**，因为它们可以直接代入弱形式的边界积分项中，而无需对[函数空间](@entry_id:143478)施加额外约束。对于这些问题，解和检验函数都取自 $H^1(\Omega)$。
    -   **[诺伊曼问题](@entry_id:176713)** ($\partial_{\mathbf{n}} u = g$ on $\partial\Omega$) [@problem_id:2579511]：我们直接用 $g$ 替换 $\partial_{\mathbf{n}} u$，得到弱形式：寻找 $u \in H^1(\Omega)$，使得对于所有 $v \in H^1(\Omega)$，
        $$
        \int_{\Omega} \nabla u \cdot \nabla v \, dx = \int_{\Omega} f v \, dx + \int_{\partial\Omega} g v \, ds
        $$
        值得注意的是，纯[诺伊曼问题](@entry_id:176713)并非对所有数据都有解。通过在原始PDE上积分并应用[散度定理](@entry_id:143110)可知，必须满足**相容性条件（compatibility condition）** $\int_{\Omega} f \, dx + \int_{\partial\Omega} g \, ds = 0$。若满足此条件，解存在但仅在相差一个常数的意义下唯一。
    -   **罗宾问题** ($\partial_{\mathbf{n}} u + \alpha u = h$ on $\partial\Omega$) [@problem_id:2579487]：我们将 $\partial_{\mathbf{n}} u = h - \alpha u$ 代入边界积分，得到弱形式：寻找 $u \in H^1(\Omega)$，使得对于所有 $v \in H^1(\Omega)$，
        $$
        \int_{\Omega} \nabla u \cdot \nabla v \, dx + \int_{\partial\Omega} \alpha u v \, ds = \int_{\Omega} f v \, dx + \int_{\partial\Omega} h v \, ds
        $$
        [罗宾边界条件](@entry_id:163914)有趣的地方在于它能够作为一种桥梁：当 $\alpha \to 0^+$ 时，它趋向于[诺伊曼条件](@entry_id:165471)；当 $\alpha \to +\infty$ 时，它可以被用来近似[狄利克雷条件](@entry_id:137096)，这构成了罚方法的基础 [@problem_id:2579487]。

#### [弱解](@entry_id:161732)与[强解](@entry_id:198344)的关系

在引入弱解之后，一个自然的问题是：一个弱解在何种条件下也是一个[强解](@entry_id:198344)（即满足[微分方程](@entry_id:264184)和边界条件的更光滑的解）？这种等价性是连接现代[PDE理论](@entry_id:189232)和经典理论的桥梁。如果一个弱解 $u$ 恰好具有更高的正则性，例如 $u \in H^2(\Omega)$，并且区域边界足够光滑（例如 $C^2$），那么我们可以通过再次使用[格林公式](@entry_id:173118)证明这个弱解也满足强形式的方程（在 $L^2$ 意义下）[@problem_id:2579524]。这个等价性论证是[有限元误差分析](@entry_id:749282)中证明收敛性的一个关键环节。

### 从连续到离散：伽辽金方法

[弱形式](@entry_id:142897)将原问题转化为一个在无穷维[函数空间](@entry_id:143478)（如 $H_0^1(\Omega)$）中寻找解的抽象问题。**伽辽金方法（Galerkin method）**的核心思想是在这个无穷维空间中选择一个有限维的[子空间](@entry_id:150286) $V_h \subset H_0^1(\Omega)$，并在这个[子空间](@entry_id:150286)中寻找一个近似解 $u_h$。

弱形式可以抽象地写作：寻找 $u \in V$ 使得 $a(u,v) = \ell(v)$ 对所有 $v \in V$ 成立。其中 $a(\cdot,\cdot)$ 是一个[双线性形式](@entry_id:746794)（bilinear form），$\ell(\cdot)$ 是一个[线性泛函](@entry_id:276136)（linear functional）。例如，对于齐次[狄利克雷问题](@entry_id:274408)，$V = H_0^1(\Omega)$，$a(u,v) = \int_{\Omega} \nabla u \cdot \nabla v \, dx$，$\ell(v) = \int_{\Omega} f v \, dx$。

**伽辽金离散问题**则是在有限维[子空间](@entry_id:150286) $V_h \subset V$ 中求解：寻找 $u_h \in V_h$ 使得
$$
a(u_h, v_h) = \ell(v_h) \quad \text{对所有 } v_h \in V_h \text{ 成立}。
$$

这个简单的公式蕴含了伽辽金方法三个基本而深刻的性质 [@problem_id:2579496]：

1.  **[伽辽金正交性](@entry_id:173536)（Galerkin Orthogonality）**：将离散问题的方程从连续问题的方程（限制在 $v_h \in V_h$ 上）中减去，我们立即得到：
    $$
    a(u, v_h) - a(u_h, v_h) = \ell(v_h) - \ell(v_h) = 0
    $$
    利用[双线性形式](@entry_id:746794)的线性性质，这可以写成：
    $$
    a(u - u_h, v_h) = 0 \quad \text{对所有 } v_h \in V_h \text{ 成立}。
    $$
    这个性质被称为[伽辽金正交性](@entry_id:173536)。它表明，近似解的误差 $e = u - u_h$ 在由[双线性形式](@entry_id:746794) $a(\cdot,\cdot)$ 定义的“[能量内积](@entry_id:167297)”下，与整个近似[子空间](@entry_id:150286) $V_h$ 是正交的。

2.  **能量最小化（Energy Minimization）**：如果[双线性形式](@entry_id:746794) $a(\cdot,\cdot)$ 是对称且正定的（即具有[内积](@entry_id:158127)的性质），那么求解伽辽金问题等价于在[子空间](@entry_id:150286) $V_h$ 中最小化一个**能量泛函** $J(w) = \frac{1}{2}a(w,w) - \ell(w)$。伽辽金方程正是这个[能量泛函](@entry_id:170311)的欧拉-拉格朗日方程。

3.  **[Céa引理](@entry_id:165386)（Céa's Lemma）**：[伽辽金正交性](@entry_id:173536)直接导出了一个关于近似误差的[准最优性](@entry_id:167176)估计。利用[双线性形式](@entry_id:746794)的强制性（coercivity, $a(v,v) \ge \alpha \lVert v \rVert_V^2$）和连续性（continuity, $|a(u,v)| \le M \lVert u \rVert_V \lVert v \rVert_V$），我们可以证明：
    $$
    \lVert u - u_h \rVert_V \le \frac{M}{\alpha} \inf_{v_h \in V_h} \lVert u - v_h \rVert_V
    $$
    [Céa引理](@entry_id:165386)表明，伽辽金解 $u_h$ 与真实解 $u$ 的误差，在范数 $\lVert \cdot \rVert_V$ 下，只比[子空间](@entry_id:150286) $V_h$ 中对 $u$ 的最佳逼近误差大一个不依赖于 $h$ 的常数因子。这把数值解的误差问题转化为了一个逼近理论问题：即我们选择的有限维空间 $V_h$ 能够多好地逼近真实解 $u$。

### 有限元方法：一种具体的实现

有限元方法（FEM）是伽辽金方法的一种具体实现，它通过在区域 $\Omega$ 的一个网格剖分 $\mathcal{T}_h$ 上构建分片多项式函数来构造有限维[子空间](@entry_id:150286) $V_h$。对于[泊松方程](@entry_id:143763)，最常用的选择是分片线性函数空间。

#### 单元计算：从物理元到参考元

直接在每个形状各异的网格单元（例如三角形）上计算积分是十分繁琐的。有限元方法通过一个标准化的流程来解决这个问题：将所有计算都转换到一个固定的、简单的**[参考单元](@entry_id:168425)（reference element）** $\hat{K}$（例如，顶点为 $(0,0),(1,0),(0,1)$ 的单位直角三角形）上进行。

这个转换通过一个可逆的**[仿射映射](@entry_id:746332)（affine map）** $x = F_K(\hat{x}) = B_K \hat{x} + b_K$ 实现，它将[参考单元](@entry_id:168425) $\hat{K}$ 上的点 $\hat{x}$ 映射到物理空间中某个具体单元 $K$ 上的点 $x$ [@problem_id:2579523]。通过这个映射，我们可以将物理单元上的积分转换为参考单元上的积分。

1.  **[单元刚度矩阵](@entry_id:139369)（Element Stiffness Matrix）**：$K^e_{ij} = \int_K \nabla \phi_i \cdot \nabla \phi_j \, dx$。其中 $\phi_i$ 是与单元 $K$ 的第 $i$ 个节点关联的[局部基](@entry_id:151573)函数。通过链式法则（$\nabla \phi_i = (B_K^{-1})^\top \nabla_{\hat{x}} \hat{\phi}_i$）和积分变量替换（$dx = |\det(B_K)| d\hat{x}$），我们得到：
    $$
    K^e_{ij} = \int_{\hat{K}} (\nabla_{\hat{x}} \hat{\phi}_i)^\top B_K^{-1} (B_K^{-1})^\top (\nabla_{\hat{x}} \hat{\phi}_j) \, |\det(B_K)| \, d\hat{x}
    $$
    这里 $\hat{\phi}_i$ 是参考单元上的[基函数](@entry_id:170178)。由于 $\hat{\phi}_i$ 是固定的简单多项式（例如线性函数），它们的梯度是常数，因此上式中的被积函数通常也是常数或低阶多项式，易于精确计算。

2.  **[单元载荷向量](@entry_id:748928)（Element Load Vector）**：$f^e_i = \int_K f(x) \phi_i(x) \, dx$。通过类似的变量替换，我们得到：
    $$
    f^e_i = \int_{\hat{K}} f(F_K(\hat{x})) \hat{\phi}_i(\hat{x}) \, |\det(B_K)| \, d\hat{x}
    $$
    这个积分通常需要使用[数值积分](@entry_id:136578)（如高斯求积）来近似计算，因为源项 $f$ 可能是复杂的函数。

例如，对于一个顶点为 $(0,0),(2,0),(0,1)$ 的[三角形单元](@entry_id:167871) $K$ 和[源项](@entry_id:269111) $f(x,y)=x+2y$，其映射矩阵为 $B_K = \begin{pmatrix} 2  0 \\ 0  1 \end{pmatrix}$。利用上述公式和参考单元上的线性[基函数](@entry_id:170178)，我们可以精确计算出[单元刚度矩阵](@entry_id:139369)和[载荷向量](@entry_id:635284)的各项，例如 $K^e_{12} = -1/4$ 和 $f^e_1 = 1/3$ [@problem_id:2579523]。

#### 组装：从局部到全局

在计算出每个单元的[单元刚度矩阵](@entry_id:139369) $K^e$ 和[单元载荷向量](@entry_id:748928) $f^e$ 之后，需要将它们**组装（assemble）**成一个对应于整个离散问题的[大型线性系统](@entry_id:167283) $K U = F$。

这个过程依赖于一个**局部到全局的索引映射**，它将每个单元的局部节点编号（例如1, 2, 3）映射到网格的全局节点编号 [@problem_id:2579546]。组装算法如下：遍历所有单元 $T$，对于每个单元的局部矩阵项 $K^e_{\ell r}$，将其值累加到[全局刚度矩阵](@entry_id:138630)的相应位置 $K_{g(\ell), g(r)}$ 上，其中 $g$ 是该单元的局部到全局映射。

这个过程的一个关键结果是[全局刚度矩阵](@entry_id:138630) $K$ 是**稀疏的（sparse）**。全局矩阵的非零项 $K_{ij}$ 仅当全局节点 $i$ 和 $j$ 同属于某个单元时才存在。这是因为如果节点 $i$ 和 $j$ 不共享同一个单元，那么它们的[全局基函数](@entry_id:749917) $\phi_i$ 和 $\phi_j$ 的**支集（support）**交集至多是零测集（一条边或一个点），导致积分 $\int_\Omega \nabla \phi_i \cdot \nabla \phi_j \, dx$ 为零。对于共享一条边的两个节点，对应的全局矩阵项会接收到来自相邻两个单元的贡献之和 [@problem_id:2579546]。这种稀疏性是有限元方法能够高效求解大规模问题的根本原因。对于纯[诺伊曼问题](@entry_id:176713)，组装出的[全局刚度矩阵](@entry_id:138630)是奇异的（具体来说，是半正定的），其零空间对应于[常数函数](@entry_id:152060)向量，这正是离散层面上的解不唯一性的体现 [@problem_id:2579511]。

### 回归理论：误差与正则性

[Céa引理](@entry_id:165386)告诉我们，有限元解的误差取决于近似空间 $V_h$ 逼近真实解 $u$ 的能力。逼近能力又强烈依赖于真实解 $u$ 本身的光滑程度，即其**正则性（regularity）**。

**[椭圆正则性理论](@entry_id:203755)（Elliptic regularity theory）**研究的就是解的正则性与问题数据（源项 $f$ 和区域 $\Omega$ 的边界 $\partial\Omega$）光滑程度之间的关系 [@problem_id:2579527]。
-   如果区域 $\Omega$ 的边界足够光滑（例如 $C^2$ 或 $C^{1,1}$），或者是一个**[凸多边形](@entry_id:165008)**，并且源项 $f \in L^2(\Omega)$，那么泊松方程（无论是[狄利克雷问题](@entry_id:274408)还是[诺伊曼问题](@entry_id:176713)）的弱解 $u$ 就具有更高的正则性，即 $u \in H^2(\Omega)$，并且满足估计 $\lVert u \rVert_{H^2(\Omega)} \le C \lVert f \rVert_{L^2(\Omega)}$。
-   然而，如果多边形区域是**非凸的**，即存在大于 $\pi$ 的内角（称为**凹角**），那么即使 $f$ 非常光滑，解在凹角附近也会出现**奇性（singularity）**，导致其不属于 $H^2(\Omega)$。例如，在一个L形区域上，解的正则性通常只比 $H^{5/3}(\Omega)$ 稍好一点。

解的正则性直接影响有限元方法的[收敛速度](@entry_id:636873)。对于分片线性元，如果真实解 $u \in H^2(\Omega)$，可以证明[能量范数](@entry_id:274966)的误差以 $O(h)$ 的速度收敛，其中 $h$ 是网格尺寸。但如果 $u$ 的正则性较差（例如在非凸区域上），收敛速度就会相应减慢。因此，对问题正则性的理解对于预测和解释有限元方法的性能至关重要。