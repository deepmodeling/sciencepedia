## 引言
在[计算地球物理学](@entry_id:747618)中，[偏微分方程](@entry_id:141332)（PDEs）是描述从[地震波传播](@entry_id:165726)到[地幔对流](@entry_id:203493)等各种物理现象的通用语言。然而，经典的强形式解法在面对具有断层、地层界面和材料突变等复杂地质现实时，往往力不从心。这正是[微分方程](@entry_id:264184)的变分与弱形式发挥关键作用的地方，它们提供了一个强大而灵活的数学框架，不仅能够处理不光滑和不连续的问题，而且是现代数值方法（如[有限元法](@entry_id:749389)）的理论基石。本文旨在系统地揭示这一核心理论。在接下来的章节中，我们将首先在“原理与机制”中深入探讨支撑[弱形式](@entry_id:142897)的数学基础，如[索博列夫空间](@entry_id:141995)和伽辽金方法。随后，在“应用与[交叉](@entry_id:147634)学科联系”中，我们将展示这些原理如何应用于解决复杂的地质建模、[多物理场耦合](@entry_id:171389)及[地球物理反演](@entry_id:749866)等实际问题。最后，通过“动手实践”部分的引导，读者将了解如何将这些理论思想转化为解决前沿问题的具体步骤，从而全面掌握这一计算科学的支柱性概念。

## 原理与机制

在上一章介绍的基础上，本章将深入探讨[偏微分方程](@entry_id:141332)（PDEs）的变分和[弱形式](@entry_id:142897)的数学原理与机制。这些是现代[计算地球物理学](@entry_id:747618)中有限元方法（FEM）等数值技术的核心。我们将从为何需要弱解开始，系统地构建支撑这些方法的数学框架，并探讨在处理地球物理学中常见的复杂问题（如[材料不连续性](@entry_id:751728)、不可压缩性和[对流](@entry_id:141806)主导输运）时出现的关键概念和高级技术。

### [弱形式](@entry_id:142897)的语言：[索博列夫空间](@entry_id:141995)

经典[PDE理论](@entry_id:189232)通常要求解具有足够阶数的连续导数，以便在域内的每一点上逐点满足方程。然而，在[地球物理学](@entry_id:147342)中，我们经常遇到诸如断层、岩层界面或材料属性突变等不连续性。例如，一个具有分层电导率或渗透率的地质模型 [@problem_id:3618393]，其控制方程的系数是分段常数或不连续的。在这种情况下，经典解可能不存在，或者至少在物理上不现实。为了克服这些限制，我们转向**[弱解](@entry_id:161732)（weak solutions）**的概念，它放宽了对解的光滑度要求。

[弱解](@entry_id:161732)的数学框架是建立在**[索博列夫空间](@entry_id:141995)（Sobolev spaces）**之上的。对于一个给定的域 $\Omega$，最基本的[索博列夫空间](@entry_id:141995)之一是 $H^1(\Omega)$。

**索博列夫空间 $H^1(\Omega)$** 由所有在 $L^2(\Omega)$ 中平方可积的函数组成，这些函数的**弱一阶导数（weak first derivatives）**也存在且在 $L^2(\Omega)$ 中平方可积。函数 $u$ 的[弱导数](@entry_id:189356) $v_i = \partial_{x_i} u$ 是通过积分恒等式来定义的，该恒等式源于分部积分：
$$
\int_{\Omega} u \, \frac{\partial \phi}{\partial x_i} \, dx = - \int_{\Omega} v_i \, \phi \, dx
$$
对于所有具有[紧支集](@entry_id:276214)的无限可微测试函数 $\phi \in C_c^\infty(\Omega)$。这个定义将[微分](@entry_id:158718)运算从可能不光滑的函数 $u$ 转移到了无限光滑的测试函数 $\phi$ 上。空间 $H^1(\Omega)$ 的范数定义为：
$$
\|u\|_{H^1}^2 = \|u\|_{L^2}^2 + \|\nabla u\|_{L^2}^2 = \int_{\Omega} |u|^2 \, dx + \int_{\Omega} |\nabla u|^2 \, dx
$$

在处理边值问题时，一个关键问题是如何理解并施加边界条件。对于 $H^1(\Omega)$ 中的函数，其在边界 $\partial\Omega$ 上的取值并非逐点明确定义。然而，对于具有足够正则性（例如，有界[Lipschitz域](@entry_id:751354)）的域，**[迹算子](@entry_id:183665)（trace operator）** $\operatorname{Tr}$ 提供了一个严谨的方式来定义函数在边界上的“值”。[迹算子](@entry_id:183665)是一个连续线性映射，它将函数 $u \in H^1(\Omega)$ 映射到边界上的[函数空间](@entry_id:143478) $H^{1/2}(\partial\Omega)$。对于光滑函数，$\operatorname{Tr}(u)$ 就是其在边界上的普通限制。

边界条件分为两类：**本质边界条件（essential boundary conditions）**和**自然边界条件（natural boundary conditions）**。本质边界条件，如狄利克雷（Dirichlet）条件（$u=g$），直接施加在解的函数空间上。自然边界条件，如诺伊曼（Neumann）或罗宾（Robin）条件，则是在推导弱形式的过程中自然出现的。

为了处理齐次[本质边界条件](@entry_id:173524)（$u=0$ on $\partial\Omega$），我们引入了一个特殊的[子空间](@entry_id:150286) $H^1_0(\Omega)$。这个空间可以被定义为光滑且在 $\Omega$ 内部具有[紧支集](@entry_id:276214)的[函数空间](@entry_id:143478) $C_c^\infty(\Omega)$ 在 $H^1$ 范数下的闭包。对于有界[Lipschitz域](@entry_id:751354)，它等价于 $H^1(\Omega)$ 中迹为零的函数构成的[子空间](@entry_id:150286) [@problem_id:3618364]：
$$
H^1_0(\Omega) = \{u \in H^1(\Omega) : \operatorname{Tr}(u) = 0 \text{ on } \partial \Omega\}
$$
在 $H^1_0(\Omega)$ 空间上，**[庞加莱不等式](@entry_id:142086)（Poincaré inequality）**成立，它表明存在一个常数 $C_P > 0$ 使得：
$$
\|u\|_{L^2(\Omega)} \leq C_P \|\nabla u\|_{L^2(\Omega)} \quad \text{for all } u \in H^1_0(\Omega)
$$
这意味着在 $H^1_0(\Omega)$ 上，$H^1$ [半范数](@entry_id:264573) $\|\nabla u\|_{L^2}$ 与完整的 $H^1$ 范数是等价的。这一性质在理论分析和数值计算中都至关重要。

### 构建[弱形式](@entry_id:142897)：伽辽金方法

一旦我们有了合适的函数空间，就可以构建[弱形式](@entry_id:142897)。其核心思想是将[微分方程](@entry_id:264184)乘以一个**测试函数（test function）**，然后在整个域上积分，并使用分部积分（即高维的散度定理）将导数从待求解的函数 $u$ 转移到测试函数上。这个过程被称为**伽辽金方法（Galerkin method）**。

我们以泊松方程（Poisson's equation）为例，这是一个描述[稳态热传导](@entry_id:177666)或[水头](@entry_id:750444)[分布](@entry_id:182848)的典型[椭圆方程](@entry_id:169190)。考虑齐次[狄利克雷边界条件](@entry_id:173524)：
$$
-\Delta u = f \quad \text{in } \Omega, \qquad u = 0 \quad \text{on } \partial\Omega
$$
我们寻求一个解 $u \in H_0^1(\Omega)$。选择任意测试函数 $v \in H_0^1(\Omega)$，将方程两边乘以 $v$ 并在 $\Omega$ 上积分：
$$
-\int_{\Omega} (\Delta u) v \, dx = \int_{\Omega} f v \, dx
$$
使用分部积分（[格林第一恒等式](@entry_id:170345)）：
$$
\int_{\Omega} \nabla u \cdot \nabla v \, dx - \int_{\partial\Omega} (\nabla u \cdot \mathbf{n}) v \, dS = \int_{\Omega} f v \, dx
$$
其中 $\mathbf{n}$ 是边界上的外法向[单位向量](@entry_id:165907)。由于测试函数 $v \in H_0^1(\Omega)$，它在边界 $\partial\Omega$ 上的迹为零，因此边界积分项消失。这就得到了该问题的**[弱形式](@entry_id:142897)（weak formulation）**：寻找 $u \in H_0^1(\Omega)$，使得对于所有 $v \in H_0^1(\Omega)$，下式成立：
$$
\int_{\Omega} \nabla u \cdot \nabla v \, dx = \int_{\Omega} f v \, dx
$$

如果问题包含自然边界条件，它们会在推导过程中自然地融入[弱形式](@entry_id:142897)。考虑一个[稳态扩散](@entry_id:154663)-反应模型，带有诺伊曼和罗宾（Robin）[混合边界条件](@entry_id:176456) [@problem_id:3618388]：
$$
- \nabla \cdot ( \kappa \nabla u ) + \sigma u = f \quad \text{in } \Omega
$$
$$
\kappa \, \partial_{n} u = 0 \quad \text{on } \Gamma_N, \qquad \kappa \, \partial_{n} u + \beta \, u = h \quad \text{on } \Gamma_R
$$
由于边界上没有处处指定 $u$ 的值，我们选择[函数空间](@entry_id:143478)为 $H^1(\Omega)$。将PDE乘以测试函数 $v \in H^1(\Omega)$ 并积分，分部积分后得到：
$$
\int_{\Omega} \kappa \nabla u \cdot \nabla v \, dx + \int_{\Omega} \sigma u v \, dx - \int_{\partial\Omega} (\kappa \partial_n u) v \, dS = \int_{\Omega} f v \, dx
$$
边界积分可以分解到 $\Gamma_N$ 和 $\Gamma_R$ 上。在 $\Gamma_N$ 上，$\kappa \partial_n u = 0$，积分项为零。在 $\Gamma_R$ 上，我们用[罗宾条件](@entry_id:153384)代入 $\kappa \partial_n u = h - \beta u$。整理后得到[弱形式](@entry_id:142897)：寻找 $u \in H^1(\Omega)$，使得对于所有 $v \in H^1(\Omega)$：
$$
\underbrace{\int_{\Omega} (\kappa \nabla u \cdot \nabla v + \sigma u v) \, dx + \int_{\Gamma_R} \beta u v \, dS}_{a(u,v)} = \underbrace{\int_{\Omega} f v \, dx + \int_{\Gamma_R} h v \, dS}_{L(v)}
$$
这个方程可以写成抽象形式 $a(u,v) = L(v)$，其中 $a(\cdot,\cdot)$ 是一个**[双线性形式](@entry_id:746794)（bilinear form）**，$L(\cdot)$ 是一个**[线性泛函](@entry_id:276136)（linear functional）**。

弱形式的[适定性](@entry_id:148590)（存在唯一解）通常由**[Lax-Milgram定理](@entry_id:137966)**保证，该定理要求双线性形式 $a(v,v)$ 在所选的[函数空间](@entry_id:143478)上是**强制的（coercive）**，即存在常数 $C>0$ 使得 $a(v,v) \ge C \|v\|^2$。对于上面的例子，如果没有狄利克雷边界条件，[常数函数](@entry_id:152060)（其梯度为零）可能使得[双线性形式](@entry_id:746794)的强制性失效。然而，正的罗宾系数 $\beta > 0$ 引入的边界项 $\int_{\Gamma_R} \beta v^2 \, dS$ 惩罚了在 $\Gamma_R$ 上非零的函数，从而消除了[常数函数](@entry_id:152060)的零空间，确保了在整个 $H^1(\Omega)$ 空间上的强制性，保证了[解的唯一性](@entry_id:143619) [@problem_id:3618388]。

### 从连续到离散：有限元方法

有限元方法（FEM）的核心是将无穷维的弱问题离散化。我们不再在整个函数空间 $V$ （如 $H^1(\Omega)$）中寻找解，而是在其一个精心挑选的有限维[子空间](@entry_id:150286) $V_h \subset V$ 中寻找一个近似解 $u_h$。这个[子空间](@entry_id:150286)通常由定义在网格单元上的分片多项式函数构成。

根据[伽辽金原理](@entry_id:167636)，我们要求[弱形式](@entry_id:142897)对 $V_h$ 中的所有测试函数 $v_h$ 都成立。如果 $\{\phi_j\}_{j=1}^N$ 是 $V_h$ 的一组[基函数](@entry_id:170178)，那么近似解可以写成这些[基函数](@entry_id:170178)的[线性组合](@entry_id:154743)：
$$
u_h(x,t) = \sum_{j=1}^{N} U_j(t) \phi_j(x)
$$
其中 $U_j(t)$ 是待求的未知系数（通常是节点上的函数值）。将 $u_h$ 代入[弱形式](@entry_id:142897)，并选择测试函数为每一个[基函数](@entry_id:170178) $v_h = \phi_i$，我们便得到一个 $N \times N$ 的代数方程组。

以一维[瞬态热扩散](@entry_id:176511)问题为例 [@problem_id:3618393]：
$$
c(x)\,\frac{\partial u}{\partial t} - \frac{\partial}{\partial x}\left(k(x)\,\frac{\partial u}{\partial x}\right)=s(x,t)
$$
其弱形式为：寻找 $u(\cdot, t) \in H_0^1(0,L)$，使得对所有 $v \in H_0^1(0,L)$，
$$
\int_{0}^{L} c(x)\,\frac{\partial u}{\partial t}\,v \,dx + \int_{0}^{L} k(x)\frac{\partial u}{\partial x}\frac{dv}{dx} \,dx = \int_{0}^{L} s(x,t)v \,dx
$$
将 $u_h(x,t) = \sum_j U_j(t) \phi_j(x)$ 和 $v = \phi_i(x)$ 代入，得到一个[常微分方程](@entry_id:147024)（ODE）组：
$$
M \frac{d\mathbf{U}}{dt} + K \mathbf{U} = \mathbf{S}(t)
$$
其中 $\mathbf{U}$ 是未知系数向量，矩阵各项为：
- **质量矩阵 (Mass Matrix)**: $M_{ij} = \int_{0}^{L} c(x)\,\phi_i(x)\phi_j(x) \,dx$。它与热容 $c(x)$ 相关，代表了系统的[热惯性](@entry_id:147003)或能量存储能力。
- **[刚度矩阵](@entry_id:178659) (Stiffness Matrix)**: $K_{ij} = \int_{0}^{L} k(x)\frac{d\phi_i}{dx}\frac{d\phi_j}{dx} \,dx$。它与[热导率](@entry_id:147276) $k(x)$ 相关，代表了通过[扩散](@entry_id:141445)进行的节点间热量传输。
- **[载荷向量](@entry_id:635284) (Load Vector)**: $S_i(t) = \int_{0}^{L} s(x,t)\phi_i(x) \,dx$。

这种方法的美妙之处在于它能自然地处理不连续的系数。例如，如果热导率 $k(x)$ 在 $x=L/2$ 处有跳跃，计算刚度矩阵时只需将积分区间相应地分开即可。对于一个在 $x_1=L/2$ 处具有节点的分片线性[基函数](@entry_id:170178) $\phi_1$，其对角线刚度项 $K_{11}$ 的计算如下 [@problem_id:3618393]：
$$
K_{11} = \int_{0}^{L} k(x) \left(\frac{d\phi_1}{dx}\right)^2 dx = \int_{0}^{L/2} k_1 \left(\frac{2}{L}\right)^2 dx + \int_{L/2}^{L} k_2 \left(-\frac{2}{L}\right)^2 dx = \frac{2(k_1+k_2)}{L}
$$

### 变分公式化中的高级课题

许多地球物理问题无法用简单的标量[椭圆方程](@entry_id:169190)描述。它们可能涉及向量场、[多物理场耦合](@entry_id:171389)或不连续解，需要更高级的变分技术。

#### 向量场问题与混合公式

当地球物理模型涉及向量场时，例如[达西流](@entry_id:748165)中的流体通量或电磁学中的[电场](@entry_id:194326)，我们需要使用更专门的索博列夫空间。

- **$H(\mathrm{div}, \Omega)$ 空间**：由平方可积的向量场组成，其散度也是平方可积的。这个空间天然适用于那些以[散度算子](@entry_id:265975)为特征的物理定律，如[质量守恒](@entry_id:204015)。对于 $\boldsymbol{u} \in H(\mathrm{div}, \Omega)$，其法向分量迹 $\gamma_n(\boldsymbol{u}) = \boldsymbol{u} \cdot \boldsymbol{n}$ 在边界上是良定义的。这使得施加法向通量这类自然边界条件变得直接。[达西流](@entry_id:748165)的混合公式就是一个典型应用，其中流体通量 $\boldsymbol{u}$ 就属于 $H(\mathrm{div}, \Omega)$ [@problem_id:3618377]。

- **$H(\mathrm{curl}, \Omega)$ 空间**：由平方可积的向量场组成，其旋度也是平方可积的。这个空间是求解麦克斯韦方程组等以[旋度算子](@entry_id:184984)为核心的问题的自然选择。对于 $\boldsymbol{E} \in H(\mathrm{curl}, \Omega)$，其切向分量迹 $\gamma_t(\boldsymbol{E}) = \boldsymbol{n} \times \boldsymbol{E}$ 在边界上是良定义的。这使得施加[理想电导体边界条件](@entry_id:753304)（$\boldsymbol{n} \times \boldsymbol{E} = \boldsymbol{0}$）这类[本质边界条件](@entry_id:173524)成为可能 [@problem_id:3618377]。

这些问题通常导致**混合公式（mixed formulations）**，其中多个未知场（如速度和压力）被同时求解。这类问题往往具有**[鞍点](@entry_id:142576)结构（saddle-point structure）**。例如，考虑不可压缩[斯托克斯流](@entry_id:138636)（creeping flow），它可以被看作一个[能量最小化](@entry_id:147698)问题，约束条件是[速度场散度](@entry_id:178755)为零 [@problem_id:3618400]。使用**拉格朗日乘子（Lagrange multiplier）**方法来处理这个约束，会自然地引入压[力场](@entry_id:147325) $p$ 作为乘子。得到的[弱形式](@entry_id:142897)是：寻找速度 $\boldsymbol{u}$ 和压力 $p$，使得
$$
a(\boldsymbol{u},\boldsymbol{v}) + b(\boldsymbol{v},p) = \ell(\boldsymbol{v})
$$
$$
b(\boldsymbol{u},q) = 0
$$
对所有测试函数 $(\boldsymbol{v}, q)$ 成立。这里的 $b(\cdot,\cdot)$ 是耦合速度和压力的项，例如 $b(\boldsymbol{v},p) = -\int_\Omega p (\nabla \cdot \boldsymbol{v}) \, dx$。

对于这类[鞍点问题](@entry_id:174221)，[Lax-Milgram定理](@entry_id:137966)不再适用。其离散版本的稳定性和[适定性](@entry_id:148590)依赖于一个关键的[相容性条件](@entry_id:637057)，即**Babuška–Brezzi (BB)条件**或**[inf-sup条件](@entry_id:746626)** [@problem_id:3618373]。这个条件要求速度和压力的[有限元近似](@entry_id:166278)空间 $V_h$ 和 $Q_h$ 之间必须保持一种平衡：
$$
\inf_{q_h \in Q_h} \sup_{\boldsymbol{v}_h \in V_h} \frac{b(\boldsymbol{v}_h, q_h)}{\|\boldsymbol{v}_h\|_{V} \|q_h\|_{Q}} \ge \beta > 0
$$
其中 $\beta$ 是一个不依赖于网格尺寸 $h$ 的正常数。如果这个条件不被满足（例如，对速度和压力使用简单的等阶分片线性元 $P_1/P_1$），压力解可能会出现非物理的棋盘状[振荡](@entry_id:267781)。在[地球物理学](@entry_id:147342)中，诸如Biot[孔隙弹性](@entry_id:174851)模型等耦合问题也存在类似的[鞍点](@entry_id:142576)结构，需要满足[inf-sup条件](@entry_id:746626)来保证压[力场](@entry_id:147325)的稳定 [@problem_id:3618428]。满足此条件的[稳定有限元](@entry_id:176475)对包括泰勒-胡德（Taylor-Hood）单元（如速度用 $P_2$ 元，压力用 $P_1$ 元）或MINI单元。

#### 替代方法与稳定化方法

除了使用满足[inf-sup条件](@entry_id:746626)的单元对外，还有其他方法来处理[鞍点问题](@entry_id:174221)或其它挑战。

- **罚方法 (Penalty Method)**：作为拉格朗日乘子法的替代，罚方法通过在能量泛函中加入一个惩罚项来近似地施加约束。例如，对于不可压缩流，可以最小化泛函 $J_\lambda(\boldsymbol{u}) = J(\boldsymbol{u}) + \frac{\lambda}{2} \int_\Omega (\nabla \cdot \boldsymbol{u})^2 \, dx$，其中 $\lambda \gg 1$ 是一个大的罚参数 [@problem_id:3618400]。这种方法的好处是它消除了压力未知数，得到了一个关于速度的[对称正定系统](@entry_id:172662)。然而，其缺点是当 $\lambda \to \infty$ 时，系统矩阵的条件数会变得非常大，导致数值求解困难。压[力场](@entry_id:147325)可以通过关系式 $p_\lambda = -\lambda \nabla \cdot \boldsymbol{u}_\lambda$ 后处理得到。

- **处理[不连续性](@entry_id:144108)与界面**: [弱导数](@entry_id:189356)的概念提供了一个强大的工具来理解和模拟不连续性。一个在界面 $\Gamma$ 上有跳跃的函数，其[弱梯度](@entry_id:756667)不仅包含在光滑区域的经典梯度，还包含一个集中在界面上的**[分布](@entry_id:182848)项（distributional term）**。例如，一个跨越 $x=0$ 从0跳跃到3的函数 $u(x,y)$，其[弱梯度](@entry_id:756667)就是 $3 \boldsymbol{e}_x \delta_\Gamma$，其中 $\delta_\Gamma$ 是沿界面 $\Gamma$ 的[狄拉克测度](@entry_id:197577) [@problem_id:3618365]。这个奇异项在弱形式中精确地描述了跨界面的通量[跳跃条件](@entry_id:750965)。

- **弱施加[狄利克雷边界条件](@entry_id:173524)：[Nitsche方法](@entry_id:175793)**: 传统上，本质边界条件通过限制[函数空间](@entry_id:143478)（例如使用 $H^1_0(\Omega)$）来强施加。**[Nitsche方法](@entry_id:175793)**提供了一种在变分框架内弱施加这些条件的方式 [@problem_id:3618432]。它通过在[双线性形式](@entry_id:746794)中添加三个边界项来实现：一个保证一致性的项，一个保持对称性的项，以及一个惩罚项。例如，对于泊松问题，Nitsche法的[弱形式](@entry_id:142897)为：
$$
a_h(u_h, v_h) = \int_{\Omega} \nabla u_h \cdot \nabla v_h \,dx - \int_{\partial\Omega} (\partial_n u_h v_h + \partial_n v_h u_h) \,dS + \int_{\partial\Omega} \frac{\gamma}{h} u_h v_h \,dS
$$
其中 $h$ 是网格尺寸，$\gamma$ 是一个足够大的无量纲惩罚参数。为了保证强制性，$\gamma$ 的值必须足够大以抵消由分部积分产生的负边界项。通过使用**[逆迹不等式](@entry_id:750809)**，可以证明只要 $\gamma$ 大于某个临界值（该值仅依赖于单元形状和多项式次数），该方法就是稳定的 [@problem_id:3618432]。[Nitsche方法](@entry_id:175793)在处理不[贴体网格](@entry_id:746935)和复杂边界几何时特别有用。

- **非自伴问题的稳定化：SUPG**: 对于像[对流](@entry_id:141806)占优的输运问题（$-\epsilon \Delta u + \mathbf{b} \cdot \nabla u = f$，其中[扩散](@entry_id:141445)系数 $\epsilon$ 很小），标准的伽辽金方法会产生严重的非物理[振荡](@entry_id:267781)。这是因为双线性形式不再对称，其反对称部分（[对流](@entry_id:141806)项）没有提供强制性。**流线迎风/[彼得罗夫-伽辽金](@entry_id:174072) (SUPG)** 方法通过修改测试函数来解决这个问题 [@problem_id:3618398]。测试函数被构造成 $w = v + \tau_e (\mathbf{b} \cdot \nabla v)$，其中 $\tau_e$ 是一个在每个单元上计算的稳定化参数。这种选择在标准[弱形式](@entry_id:142897)的基础上，增加了一个与问题残差 $R(u) = -\epsilon \Delta u + \mathbf{b} \cdot \nabla u - f$ 相关的项：
$$
\sum_e \int_{T_e} \tau_e (\mathbf{b} \cdot \nabla v) R(u_h) \, dx
$$
这个附加项在流线方向上引入了[人工扩散](@entry_id:637299)，有效地抑制了[振荡](@entry_id:267781)，同时保持了方法的一致性。稳定化参数 $\tau_e$ 的最优选择通常与单元尺寸和局部[Péclet数](@entry_id:141791)相关，旨在平衡稳定性和数值耗散。

总之，变分和弱形式为求解地球物理学中的PDEs提供了一个强大而灵活的框架。通过选择合适的索博列夫空间和精心设计的[变分形式](@entry_id:166033)，我们可以严谨地处理各种复杂的物理现象，并为稳健的[数值离散化](@entry_id:752782)奠定坚实的基础。