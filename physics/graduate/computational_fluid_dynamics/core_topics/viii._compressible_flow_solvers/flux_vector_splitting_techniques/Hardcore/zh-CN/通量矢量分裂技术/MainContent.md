## 引言
在计算科学与工程领域，求解描述流体运动、波的传播以及其他输运现象的双曲守恒律方程是一项核心挑战。这些方程的解往往包含激波、接触间断等不连续结构，对数值方法的稳定性和精度提出了极高要求。通量矢量分裂（Flux Vector Splitting, FVS）技术正是在这样的背景下应运而生，它提供了一种物理直观且数学上稳健的框架，用以构建能够准确捕捉信息传播方向的迎风格式。FVS不仅是计算流体力学（CFD）的基石之一，其蕴含的设计哲学更对众多科学与工程领域的数值模拟产生了深远影响。

本文旨在为读者系统性地构建关于通量矢量分裂技术的完整知识体系。我们将从其最根本的数学与物理思想出发，逐步深入到具体算法的构建与分析，最终展示其在现代计算科学前沿的广泛应用。文章将通过以下三个核心章节展开：第一章“原理与机制”将深入剖析FVS的数学基础、迎风思想的来源，并详细介绍Steger-Warming、Van Leer以及AUSM等经典格式的设计理念与内在缺陷；第二章“应用与跨学科连接”将视野拓宽至实际应用，探讨FVS如何与高阶格式、复杂网格、预处理技术相结合，并展示其在地球物理、磁流体动力学等交叉学科中的强大生命力；最后，第三章“动手实践”将通过一系列精心设计的计算练习，帮助读者将理论知识转化为解决实际问题的能力。通过这一结构化的学习路径，读者将不仅理解FVS“是什么”，更能掌握其“为什么”以及“如何用”。

## 原理与机制

本章深入探讨通量矢量分裂（Flux Vector Splitting, FVS）技术的内在原理与核心机制。我们将从双曲型守恒律的数学基础出发，揭示迎风格式的本质，并系统地阐述几种经典的FVS格式是如何被设计、实现，以及它们各自的优缺点。本章的目标是为读者构建一个关于FVS技术的严谨、系统且深入的知识框架。

### 迎风原理与分裂思想

计算流体力学中求解双曲型守恒律方程组的核心挑战在于如何准确地模拟信息（或波）的传播。形如 $\partial_t \boldsymbol{u} + \nabla \cdot \boldsymbol{f}(\boldsymbol{u}) = \boldsymbol{0}$ 的方程组，其信息传播特性由通量雅可比矩阵 $\boldsymbol{A}_{\boldsymbol{n}}(\boldsymbol{u}) = \partial (\boldsymbol{f} \cdot \boldsymbol{n}) / \partial \boldsymbol{u}$ 的谱特性决定。一个系统被称为**双曲型**（hyperbolic），当且仅当对于任意方向 $\boldsymbol{n}$，其方向通量雅可比矩阵 $\boldsymbol{A}_{\boldsymbol{n}}(\boldsymbol{u})$ 都具有完备的实特征值和线性无关的实特征向量集，即在实数域上是可对角化的 [@problem_id:3386749]。这些实特征值，即特征速度，代表了物理信息沿该方向传播的速度。

正是这种基于实特征值的波状分解结构，为发展**迎风格式**（upwind schemes）提供了数学基础。迎风原理的核心思想是，在计算单元界面上的数值通量时，信息应当从其传播的方向（即上游）获取。对于一个简单的标量平流方程 $\partial_t u + a \partial_x u = 0$，如果速度 $a>0$，信息从左向右传播，界面通量就应由左侧单元的状态决定；反之亦然。

对于如欧拉方程这样的方程组，情况更为复杂，因为存在多个以不同速度（例如 $u-a$, $u$, $u+a$）向不同方向传播的波。为了将迎风思想应用于方程组，数值方法必须能够区分这些不同方向的传播贡献。主要有两种不同的实现哲学：

1.  **通量差分分裂（Flux Difference Splitting, FDS）**：这类方法，也常被称为**近似黎曼求解器（Approximate Riemann Solvers, ARS）**，通过在单元界面上求解一个局部黎曼问题来构建数值通量。它直接模拟左右两个不同状态 $\boldsymbol{u}_L$ 和 $\boldsymbol{u}_R$ 的相互作用，并根据由此产生的波结构（如激波、接触间断和稀疏波）来计算穿过界面的通量。因此，其数值通量是 $\boldsymbol{u}_L$ 和 $\boldsymbol{u}_R$ 的联合函数，例如Roe格式 [@problem_id:3366279]。

2.  **通量矢量分裂（Flux Vector Splitting, FVS）**：与FDS不同，FVS并不直接求解界面上的黎曼问题。它的核心思想是，将物理通量矢量 $\boldsymbol{F}(\boldsymbol{U})$ 本身预先分解为两个部分：一个与正特征值（右行波）相关的部分 $\boldsymbol{F}^+$，另一个与负特征值（左行波）相关的部分 $\boldsymbol{F}^-$。在计算界面通量时，右行波的贡献完全取自左侧单元状态 $\boldsymbol{U}_L$，而左行波的贡献完全取自右侧单元状态 $\boldsymbol{U}_R$。因此，数值通量 $\hat{\boldsymbol{F}}$ 的构造形式为：
    $$
    \hat{\boldsymbol{F}}_{i+1/2} = \boldsymbol{F}^+(\boldsymbol{U}_L) + \boldsymbol{F}^-(\boldsymbol{U}_R)
    $$
    这种方法通过对通量矢量本身的分解来实现迎风特性，而不是通过分析两个状态的差异 [@problem_id:3366279]。

### 通量矢量分裂的耗散机制

FVS格式的迎风特性本质上是通过引入数值耗散（或称人工黏性）来实现的。这种耗散能够抑制非物理性的数值振荡，尤其是在间断（如激波）附近。我们可以通过一个简单的推导来揭示其内在的耗散机制。

给定数值通量 $\hat{\boldsymbol{F}} = \boldsymbol{F}^+(\boldsymbol{U}_L) + \boldsymbol{F}^-(\boldsymbol{U}_R)$，并利用一致性条件 $\boldsymbol{F} = \boldsymbol{F}^+ + \boldsymbol{F}^-$，我们可以将其改写。
首先，$\hat{\boldsymbol{F}} = \boldsymbol{F}(\boldsymbol{U}_L) - \boldsymbol{F}^-(\boldsymbol{U}_L) + \boldsymbol{F}^-(\boldsymbol{U}_R)$。
其次，$\hat{\boldsymbol{F}} = \boldsymbol{F}^+(\boldsymbol{U}_L) + \boldsymbol{F}(\boldsymbol{U}_R) - \boldsymbol{F}^+(\boldsymbol{U}_R)$。
将这两式相加并除以2，得到：
$$
\hat{\boldsymbol{F}} = \frac{1}{2}\left(\boldsymbol{F}(\boldsymbol{U}_L) + \boldsymbol{F}(\boldsymbol{U}_R)\right) - \frac{1}{2}\left[ (\boldsymbol{F}^+(\boldsymbol{U}_R) - \boldsymbol{F}^+(\boldsymbol{U}_L)) - (\boldsymbol{F}^-(\boldsymbol{U}_R) - \boldsymbol{F}^-(\boldsymbol{U}_L)) \right]
$$
对括号中的项进行线性化，即 $\boldsymbol{F}^\pm(\boldsymbol{U}_R) - \boldsymbol{F}^\pm(\boldsymbol{U}_L) \approx \boldsymbol{A}^\pm(\boldsymbol{U}_{R} - \boldsymbol{U}_{L})$，其中 $\boldsymbol{A}^\pm = \partial \boldsymbol{F}^\pm / \partial \boldsymbol{U}$ 是分裂通量的雅可比矩阵。于是，数值通量可以近似写为：
$$
\hat{\boldsymbol{F}} \approx \frac{1}{2}\left(\boldsymbol{F}(\boldsymbol{U}_L) + \boldsymbol{F}(\boldsymbol{U}_R)\right) - \frac{1}{2}\left(\boldsymbol{A}^+ - \boldsymbol{A}^-\right)(\boldsymbol{U}_R - \boldsymbol{U}_L)
$$
由于 $\boldsymbol{A} = \boldsymbol{A}^+ + \boldsymbol{A}^-$，并且 $\boldsymbol{A}^\pm$ 的特征值分别为原雅可比矩阵 $\boldsymbol{A}$ 的正部和负部，我们可以证明 $\boldsymbol{A}^+ - \boldsymbol{A}^- = |\boldsymbol{A}| = \boldsymbol{R}|\boldsymbol{\Lambda}|\boldsymbol{R}^{-1}$，其中 $|\boldsymbol{\Lambda}|$ 是包含特征值绝对值的对角矩阵。最终，我们得到：
$$
\hat{\boldsymbol{F}} \approx \underbrace{\frac{1}{2}\left(\boldsymbol{F}(\boldsymbol{U}_L) + \boldsymbol{F}(\boldsymbol{U}_R)\right)}_{\text{中心部分}} - \underbrace{\frac{1}{2}|\boldsymbol{A}|(\boldsymbol{U}_R - \boldsymbol{U}_L)}_{\text{耗散项}}
$$
这个结果清晰地表明，FVS格式可以被看作一个中心通量加上一个耗散项 [@problem_id:3386755]。耗散项的大小正比于状态的跳跃 $(\boldsymbol{U}_R - \boldsymbol{U}_L)$ 和一个由 $|\boldsymbol{A}|$ 定义的数值黏性矩阵。重要的是，这种耗散是**各向异性**的，它通过矩阵 $|\boldsymbol{A}|$ 将阻尼施加在不同的特征场上，阻尼大小与相应特征波的传播速度 $|\lambda_k|$ 成正比。这正是迎风格式相较于标量人工黏性的优越之处：它能够根据波的物理传播特性自适应地施加稳定化作用。

### Steger-Warming 分裂：早期的特征分裂

Steger和Warming在1981年提出的分裂格式是FVS方法的开创性工作。它巧妙地利用了欧拉方程通量矢量 $\boldsymbol{F}$ 对于守恒变量 $\boldsymbol{U}$ 的一阶齐次函数特性，即 $\boldsymbol{F}(\boldsymbol{U}) = \boldsymbol{A}(\boldsymbol{U})\boldsymbol{U}$。

基于这一特性，通量分裂可以直接通过分裂雅可比矩阵 $\boldsymbol{A}$ 来实现。设 $\boldsymbol{A} = \boldsymbol{R}\boldsymbol{\Lambda}\boldsymbol{R}^{-1}$ 为 $\boldsymbol{A}$ 的谱分解，其中 $\boldsymbol{\Lambda} = \text{diag}(\lambda_1, \dots, \lambda_m)$。Steger-Warming分裂定义了分裂的雅可比矩阵：
$$
\boldsymbol{A}^\pm = \boldsymbol{R} \boldsymbol{\Lambda}^\pm \boldsymbol{R}^{-1}
$$
其中 $\boldsymbol{\Lambda}^\pm$ 是对角矩阵，其对角元为 $\lambda_k^\pm = \frac{1}{2}(\lambda_k \pm |\lambda_k|)$。这等价于 $\lambda_k^+$ 只保留正的特征值，而 $\lambda_k^-$ 只保留负的特征值。分裂的通量由此定义为：
$$
\boldsymbol{F}^\pm(\boldsymbol{U}) = \boldsymbol{A}^\pm(\boldsymbol{U})\boldsymbol{U}
$$
通过将守恒状态矢量 $\boldsymbol{U}$ 投影到雅可比矩阵的特征向量基上，我们可以得到分裂通量的显式表达式。对于一维欧拉方程，其特征值为 $\lambda_1 = u-a$, $\lambda_2 = u$, $\lambda_3 = u+a$，经过推导，正部通量 $\boldsymbol{F}^+$ 可以表示为各个特征波贡献的加权和 [@problem_id:3386784]：
$$
\boldsymbol{F}^+(U) = \frac{\rho}{2\gamma} \lambda_1^{+} \begin{pmatrix} 1 \\ u-a \\ H-ua \end{pmatrix} + \rho\frac{\gamma-1}{\gamma} \lambda_2^{+} \begin{pmatrix} 1 \\ u \\ \frac{u^2}{2} \end{pmatrix} + \frac{\rho}{2\gamma} \lambda_3^{+} \begin{pmatrix} 1 \\ u+a \\ H+ua \end{pmatrix}
$$
其中 $H$ 是总焓。这是一个优美的解析结果，它将复杂的流体动力学通量分解为三个独立的、沿各自特征方向传播的“波包”的线性叠加。

### Steger-Warming 分裂的局限性

尽管Steger-Warming分裂在概念上具有开创性，但在实际应用中很快暴露出一些严重的缺陷，这些缺陷也催生了后续FVS方法的改进。

#### 声速点处的非光滑性与熵破坏

Steger-Warming分裂最核心的问题源于其对特征值符号的“硬”切换。函数 $|\lambda|$ 在 $\lambda=0$ 处是连续但不可微的。这意味着，当流场中某个点的特征速度（例如，跨音速流动中的 $u-a$）穿过零时，分裂通量 $\boldsymbol{F}^\pm$ 对状态变量 $\boldsymbol{U}$ 的导数是不连续的 [@problem_id:3320867]。对于需要计算雅可比矩阵的隐式时间推进格式（如牛顿法），这种不光滑性会导致数值收敛性的严重恶化。

更严重的是，这种不光滑性与一个物理上的谬误直接相关。在特征值为零的点（即声速点），对应特征场的数值耗散（正比于 $|\lambda|$）完全消失了。这使得数值格式在该点附近无法区分物理上正确的稀疏波和非物理的膨胀激波。结果是，在模拟跨音速稀疏波时，该格式可能会错误地收敛到一个带有间断的、熵减的膨胀激波解，这严重违反了热力学第二定律 [@problem_id:3320900]。为了修正这个问题，必须引入额外的“熵修正”（entropy fix），例如人为地在零点附近“磨平”绝对值函数，以保证耗散始终为正。

#### 低马赫数下的过度耗散

Steger-Warming分裂的另一个主要缺点是在低速（低马赫数）流动中表现不佳。其数值扩散系数的大小由最快的波速决定，即 $\nu_{\text{num}} \propto \Delta x \max(|\lambda_k|) = \Delta x (|u|+a)$。我们可以分析数值扩散与物理尺度的关系。定义两个无量纲比率：
$$
R_{\text{acoustic}}(M) = \frac{\nu_{\text{num}}}{a\Delta x}, \qquad R_{\text{convective}}(M) = \frac{\nu_{\text{num}}}{|u|\Delta x}
$$
其中 $M = |u|/a$ 是马赫数。经过推导，我们发现 [@problem_id:3320857]：
$$
R_{\text{acoustic}}(M) = \frac{M+1}{2}, \qquad R_{\text{convective}}(M) = \frac{M+1}{2M}
$$
当马赫数 $M \to 0$ 时，$R_{\text{acoustic}} \to 1/2$，表明数值扩散速度与声速同量级，这是合理的。然而，$R_{\text{convective}} \to \infty$，表明数值扩散远大于物理对流速度 $|u|$。这意味着在低速流动中，格式引入的巨大数值黏性会完全淹没真实的物理对流过程，导致对接触间断、剪切层和边界层等重要流动结构的模拟精度极低，出现严重的“涂抹”现象 [@problem_id:3366279]。

### Van Leer 分裂：光滑分裂的艺术

为了克服Steger-Warming分裂的缺陷，Bram van Leer在1982年提出了一种全新的FVS构造哲学。其核心目标是确保分裂的通量函数及其导数在声速点处都是连续的（$C^1$ 光滑）。

#### 光滑分裂函数的设计

Van Leer不直接分裂特征值，而是为质量、动量和能量通量构造了基于马赫数 $M$ 的光滑多项式分裂函数。以一个无量纲化的特征速度 $z$（例如 $M$ 或 $M \pm 1$）为例，其正分裂函数 $z^+(z)$ 必须满足以下原则 [@problem_id:3386746]：

1.  **超音速一致性**：当 $z \ge 1$ 时，$z^+(z) = z$；当 $z \le -1$ 时，$z^+(z) = 0$。
2.  **亚音速对称性**：$z^+(-z) = -z^-(z)$，其中 $z^- = z - z^+$。
3.  **声速点 $C^1$ 光滑性**：在 $z = \pm 1$ 处，$z^+(z)$ 的函数值和一阶导数值都必须与超音速分支平滑衔接。

基于这些原则，可以推导出在亚音速区域 $|z|1$ 内，满足条件的最低阶多项式是一个二次多项式。最终得到的Van Leer分裂函数为：
$$
z^{+}(z) = 
\begin{cases} 
0,  z \leq -1 \\ 
\frac{1}{4}(z+1)^2,  |z|  1 \\ 
z,  z \geq 1 
\end{cases}
$$
这个函数在整个实数轴上都是 $C^1$ 光滑的。

#### Van Leer 通量矢量分裂格式

Van Leer将这种光滑分裂思想应用于欧拉方程的通量分量。分裂后的正部通量 $\boldsymbol{F}^+$ 可以写成对流项和压力项的组合。以马赫数 $M=u/a$ 为分裂变量，当 $|M|  1$（亚音速）时，分裂的质量通量和压力通量为：
$$
f_{\text{mass}}^\pm = \pm \frac{1}{4} \rho a (M \pm 1)^2
$$
$$
f_{\text{pressure}}^\pm = p \frac{f_{\text{mass}}^\pm}{\rho a} (2 \mp M) = \frac{p}{4}(M \pm 1)^2(2 \mp M)
$$
（注意：文献中有多种Van Leer压力分裂形式，这里仅为示例）。完整的通量矢量分裂形式相当复杂，但其核心思想是通过这些光滑的多项式来构造。一个常见的完整形式如下 [@problem_id:3387432]：
$$
\boldsymbol{F}^{\pm}(U) = 
\begin{bmatrix}
\rho a M^{\pm} \\
\rho a M^{\pm} u + p^{\pm} \\
\rho a M^{\pm} H
\end{bmatrix}
$$
其中 $M^\pm$ 和 $p^\pm$ 是基于上述光滑分裂原则构造的函数。例如，对于 $|M|  1$，
$$
M^{+}(M) = \frac{1}{4}(M + 1)^2, \qquad p^{+}(M,p) = \frac{p}{2}(M+1)
$$
这种构造保证了分裂通量及其雅可比矩阵在声速点是连续的。这不仅解决了Steger-Warming格式在隐式计算中的收敛性问题 [@problem_id:3320867]，也自然地为格式提供了必要的耗散，避免了非物理膨胀激波的产生，无需额外的熵修正 [@problem_id:3320900]。尽管Van Leer格式在低马赫数下的过度耗散问题有所改善，但并未完全根除。

### 物理分裂：AUSM系列格式

FVS的另一种思路是放弃纯数学的特征分解，转而从更物理的直觉出发。其中最具代表性的是**平流上游分裂方法（Advection Upstream Splitting Method, AUSM）**系列格式 [@problem_id:3292934]。

AUSM的核心思想是将欧拉通量 $\boldsymbol{F}$ 分解为一个**对流项（convective part）**和一个**压力项（pressure part）**：
$$
\boldsymbol{F}(\boldsymbol{U}) = \boldsymbol{F}_c(\boldsymbol{U}) + \boldsymbol{F}_p(\boldsymbol{U})
$$
一个直接的分解是：
$$
\boldsymbol{F}_c = \begin{bmatrix} \rho u \\ \rho u^2 \\ \rho H u \end{bmatrix} = u \begin{bmatrix} \rho \\ \rho u \\ \rho H \end{bmatrix}, \qquad \boldsymbol{F}_p = \begin{bmatrix} 0 \\ p \\ 0 \end{bmatrix}
$$
注意这里的能量通量分解方式 $\rho E u + pu = \rho H u$。对流项表示所有守恒量（质量、动量、焓）随流体速度 $u$ 的平流输运，而压力项代表了作用在动量方程中的压力。

在计算界面通量时，AUSM格式分别对这两部分采用不同的迎风策略。它首先通过某种方式在界面上定义一个界面速度 $u_{1/2}$ 和界面压力 $p_{1/2}$，然后根据界面速度的方向（符号）来决定对流输运的贡献来自左侧还是右侧，最后将压力项的贡献加上。
$$
\hat{\boldsymbol{F}}_{1/2} = u_{1/2} \left( \frac{1+\text{sign}(u_{1/2})}{2} \boldsymbol{\Phi}_L + \frac{1-\text{sign}(u_{1/2})}{2} \boldsymbol{\Phi}_R \right) + \boldsymbol{P}_{1/2}
$$
其中 $\boldsymbol{\Phi} = (\rho, \rho u, \rho H)^\top$，$\boldsymbol{P}_{1/2} = (0, p_{1/2}, 0)^\top$。AUSM系列格式的主要区别在于如何定义 $u_{1/2}$ 和 $p_{1/2}$。

这种物理分裂方式相比特征分裂，具有更好的低速流动性能（因为它能更好地解耦声学和对流效应），并且能精确地保持接触间断。它代表了FVS思想向更精细、更物理的方向发展，并衍生出了AUSM+、AUSM+-up等一系列在现代CFD软件中广泛应用的优秀格式。