## 引言
在现代计算岩土力学中，对地质材料[非线性](@entry_id:637147)行为的精确模拟是解决复杂工程问题的基础。有限元法（FEM）中的牛顿-拉夫逊（Newton-Raphson）迭代法是求解这些高度非线性系统的强大工具，但其高效性（即二次收敛率）依赖于一个严格的前提：使用精确的切线刚度矩阵。这一要求直接引出了本文的核心主题——**本构更新的一致性线性化（consistent linearization of constitutive updates）**。它解决了在离散数值计算中如何维持理论收敛性的关键知识缺口，是连接非线性材料本构理论与高效数值算法之间的桥梁。

本文将系统地引导读者深入理解这一关键数值技术。在第一章“**原理与机制**”中，我们将阐明一致性线性化的基本原理，辨析算法切线与连续介质切线的区别，并详细介绍作为非线性来源的返回映射算法及其线性化推导过程。随后的“**应用与交叉学科联系**”章节将展示这一技术在各种高级本构模型、多物理场耦合问题以及跨尺度分析中的广泛应用，突显其作为通用工具的强大能力。最后，在“**动手实践**”部分，读者将有机会通过具体问题，将理论知识应用于实践，从而巩固对一致性线性化重要性的理解。

## 原理与机制

本章在前一章介绍的背景基础上，深入探讨计算非弹性力学中本构关系更新的一致性线性化（consistent linearization of constitutive updates）的核心原理与关键机制。我们将从理论基础出发，逐步解析为何需要一致性线性化、它与传统连续介质理论有何区别、如何推导它，并最终讨论在复杂地质材料模型中遇到的实际挑战。

### 在非线性有限元中一致性线性化的基本原理

在准静态地质力学问题的有限元分析中，求解的核心任务是在每个载荷（或时间）增量步结束时，找到满足全局平衡方程的节点位移场 $\mathbf{u}$。该平衡方程通常表示为一个非线性代数方程组：
$$
\mathbf{R}(\mathbf{u}) = \mathbf{f}_{\text{ext}} - \mathbf{f}_{\text{int}}(\mathbf{u}) = \mathbf{0}
$$
其中，$\mathbf{f}_{\text{ext}}$ 是外力向量，$\mathbf{f}_{\text{int}}(\mathbf{u})$ 是与位移场 $\mathbf{u}$ 相关的内力向量。内力向量通过在求解域 $\Omega$ 上对每个材料点的应力进行积分得到：
$$
\mathbf{f}_{\text{int}}(\mathbf{u}) = \int_{\Omega} \mathbf{B}^{\mathsf{T}} \boldsymbol{\sigma}_{n+1} \, \mathrm{d}\Omega
$$
这里，$\mathbf{B}$ 是应变-位移矩阵，$\boldsymbol{\sigma}_{n+1}$ 是增量步结束时的柯西应力张量。由于地质材料（如土壤和岩石）通常表现出非线性行为（例如弹塑性），应力 $\boldsymbol{\sigma}_{n+1}$ 是应变 $\boldsymbol{\varepsilon}_{n+1}$ 的一个复杂的、非线性的函数，而应变又依赖于位移 $\mathbf{u}$。这使得全局平衡方程 $\mathbf{R}(\mathbf{u}) = \mathbf{0}$ 成为一个高度非线性的系统。

解决此类非线性系统的标准方法是 **牛顿-拉夫逊（Newton-Raphson, NR）迭代法**。在第 $k$ 次迭代中，我们通过求解一个线性方程组来计算位移修正量 $\Delta \mathbf{u}^{(k)}$：
$$
\mathbf{K}_{\text{used}}(\mathbf{u}^{(k)}) \, \Delta \mathbf{u}^{(k)} = - \mathbf{R}(\mathbf{u}^{(k)})
$$
然后更新位移：$\mathbf{u}^{(k+1)} = \mathbf{u}^{(k)} + \Delta \mathbf{u}^{(k)}$。其中，$\mathbf{K}_{\text{used}}$ 是所使用的切线刚度矩阵。

牛顿-拉夫逊方法的一个关键特性是其 **二次收敛率**。这意味着在解的附近，每次迭代的误差大约是前一次迭代误差的平方。这种快速收敛性对于求解大规模、高度非线性的工程问题至关重要。然而，二次收敛率的实现有一个严格的前提：迭代中使用的切线矩阵 $\mathbf{K}_{\text{used}}$ 必须是残差向量 $\mathbf{R}$ 相对于未知量 $\mathbf{u}$ 的 **精确雅可比矩阵（exact Jacobian）**，我们称之为 **一致性切线刚度矩阵（consistent tangent stiffness matrix）** $\mathbf{K}_{\ast}$。

根据链式法则，这个精确的雅可比矩阵可以推导为：
$$
\mathbf{K}_{\ast}(\mathbf{u}) = \frac{\partial \mathbf{R}}{\partial \mathbf{u}} = - \frac{\partial \mathbf{f}_{\text{int}}}{\partial \mathbf{u}} = - \int_{\Omega} \mathbf{B}^{\mathsf{T}} \frac{\partial \boldsymbol{\sigma}_{n+1}}{\partial \boldsymbol{\varepsilon}_{n+1}} \frac{\partial \boldsymbol{\varepsilon}_{n+1}}{\partial \mathbf{u}} \, \mathrm{d}\Omega = \int_{\Omega} \mathbf{B}^{\mathsf{T}} \left( \frac{\partial \boldsymbol{\sigma}_{n+1}}{\partial \boldsymbol{\varepsilon}_{n+1}} \right) \mathbf{B} \, \mathrm{d}\Omega
$$
这个推导明确地显示，全局一致性切线刚度矩阵 $\mathbf{K}_{\ast}$ 的核心是材料点层面的导数 $\frac{\partial \boldsymbol{\sigma}_{n+1}}{\partial \boldsymbol{\varepsilon}_{n+1}}$。这个量，即增量步结束时的应力对该步结束时总应变的精确导数，被称为 **算法（或一致性）切线模量（algorithmic or consistent tangent modulus）**，记为 $\mathbb{C}^{\text{alg}}$。

因此，为了在全局牛顿-拉夫逊迭代中实现二次收敛，我们必须使用基于 $\mathbb{C}^{\text{alg}}$ 构建的切线刚度矩阵。如果使用任何近似的切线模量，例如弹性模量 $\mathbb{C}_{e}$ 或某个割线模量 $\mathbb{C}_{\text{sec}}$，那么 $\mathbf{K}_{\text{used}} \neq \mathbf{K}_{\ast}$。这种方法被称为非精确牛顿法（inexact Newton method），其收敛率通常会从二次退化为线性，显著增加求解所需的迭代次数 [@problem_id:3508064]。这正是我们不辞辛劳去推导和实现复杂的 $\mathbb{C}^{\text{alg}}$ 的根本原因。

### 算法切线与连续介质切线

理解算法切线模量的关键在于将其与传统连续介质力学中的 **连续介质切线模量（continuum tangent modulus）** $\mathbb{C}$ 区分开来。

**连续介质切线模量** $\mathbb{C}$ 描述了材料的瞬时响应，它从本构关系的速率形式中导出。对于弹塑性材料，其定义为 $\dot{\boldsymbol{\sigma}} = \mathbb{C} : \dot{\boldsymbol{\varepsilon}}$。
- 在弹性状态下，$\dot{\boldsymbol{\varepsilon}}^p = 0$，因此 $\dot{\boldsymbol{\sigma}} = \mathbb{C}^e : \dot{\boldsymbol{\varepsilon}}$，此时连续介质切线即为弹性模量 $\mathbb{C} = \mathbb{C}^e$。
- 在塑性加载状态下，必须满足塑性一致性条件 $\dot{f}=0$。通过求解该条件，可以推导出连续介质弹塑性切线模量 $\mathbb{C}^{\text{ep}}$：
$$
\mathbb{C} = \mathbb{C}^{\text{ep}} = \mathbb{C}^e - \frac{(\mathbb{C}^e : \mathbf{m}) \otimes (\mathbf{m} : \mathbb{C}^e)}{\mathbf{m} : \mathbb{C}^e : \mathbf{m} + H'}
$$
其中 $\mathbf{m} = \partial f / \partial \boldsymbol{\sigma}$ 是屈服面法向，而 $H'$ 是硬化模量。$\mathbb{C}^{\text{ep}}$ 代表了材料在屈服时真实的瞬时刚度。

相比之下，**算法切线模量** $\mathbb{C}^{\text{alg}}$ 是一个纯粹的数值概念。它描述了在有限大小的时间（或载荷）增量步 $\Delta t$ 之后，离散更新后的应力 $\boldsymbol{\sigma}_{n+1}$ 对该步结束时的总应变 $\boldsymbol{\varepsilon}_{n+1}$ 的敏感度，即 $\mathbb{C}^{\text{alg}} = \frac{\partial \boldsymbol{\sigma}_{n+1}}{\partial \boldsymbol{\varepsilon}_{n+1}}$。它的表达式是通过对用于计算 $\boldsymbol{\sigma}_{n+1}$ 的整个离散数值算法（例如，返回映射算法）进行精确求导而得到的。

这两者之间的关系至关重要 [@problem_id:3508074]：
1.  **对于纯线性弹性行为**，本构关系本身是线性的，其离散积分也是线性的。因此，$\mathbb{C}^{\text{alg}} = \mathbb{C} = \mathbb{C}^e$。
2.  **对于弹塑性材料的弹性步**（例如，卸载或中性加载），由于没有塑性修正，离散更新等同于弹性更新，因此 $\mathbb{C}^{\text{alg}} = \mathbb{C} = \mathbb{C}^e$。
3.  **对于弹塑性材料的塑性步**，对于任何有限的增量步长 $\Delta t > 0$，$\mathbb{C}^{\text{alg}}$ 和 $\mathbb{C}^{\text{ep}}$ 通常是 **不相等** 的。$\mathbb{C}^{\text{alg}}$ 的表达式通常更为复杂，它不仅依赖于步末的状态，还依赖于离散化方案（如后向欧拉法）以及屈服面的曲率等。
4.  **一致性检验**：一个合理的数值格式必须满足，当步长趋于零时，离散算子应收敛于连续算子。对于算法切线，这意味着在极限情况下 $\lim_{\Delta t \to 0} \mathbb{C}^{\text{alg}} = \mathbb{C}^{\text{ep}}$。这个性质证明了我们所使用的数值线性化是与底层连续介质模型相容的。

简而言之，$\mathbb{C}$ 是物理模型的切线，而 $\mathbb{C}^{\text{alg}}$ 是数值算法的切线。为了数值效率（二次收敛），我们必须在全局刚度矩阵中使用后者。

### 返回映射算法：非线性的来源

为了推导 $\mathbb{C}^{\text{alg}}$，我们必须首先理解并形式化地描述计算 $\boldsymbol{\sigma}_{n+1}$ 的数值算法。在率无关弹塑性力学中，最常用的方法是 **返回映射算法（return-mapping algorithm）**，它通常基于 **后向欧拉（Backward Euler）** 积分格式。该算法将一个增量步分为两个概念上的步骤 [@problem_id:3508100]：

1.  **弹性预测（Elastic Predictor）**：首先，假设整个增量步是纯弹性的。基于上一时刻的应力 $\boldsymbol{\sigma}_n$ 和应变增量 $\Delta\boldsymbol{\varepsilon}$，计算出一个 **试探应力（trial stress）** $\boldsymbol{\sigma}^{\text{tr}}$：
    $$
    \boldsymbol{\sigma}^{\text{tr}} = \boldsymbol{\sigma}_n + \mathbb{C}^e : \Delta\boldsymbol{\varepsilon} = \mathbb{C}^e : (\boldsymbol{\varepsilon}_{n+1} - \boldsymbol{\varepsilon}^p_n)
    $$
    在试探步中，所有内变量（如塑性应变 $\boldsymbol{\varepsilon}^p$ 和硬化变量 $\mathbf{q}$）保持不变。

2.  **屈服检查（Yield Check）**：用试探应力代入屈服函数 $f(\boldsymbol{\sigma}, \mathbf{q})$ 进行判断：
    -   如果 $f(\boldsymbol{\sigma}^{\text{tr}}, \mathbf{q}_n) \le 0$，说明试探应力位于或处于屈服面内部，弹性假设成立。该增量步是弹性的，最终应力就是试探应力：$\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}^{\text{tr}}$。
    -   如果 $f(\boldsymbol{\sigma}^{\text{tr}}, \mathbf{q}_n) > 0$，说明试探应力超出了屈服面，弹性假设不成立。必须进行 **塑性修正（Plastic Corrector）**。

3.  **塑性修正（Plastic Corrector）**：当发生塑性加载时，步末的真实状态 $(\boldsymbol{\sigma}_{n+1}, \mathbf{q}_{n+1})$ 必须满足离散化的本构方程和一致性条件。对于后向欧拉格式，所有与塑性流动相关的量都在步末时刻 $t_{n+1}$ 进行评估。这会形成一个局部非线性方程组，其未知数通常包括 $\boldsymbol{\sigma}_{n+1}$、$\mathbf{q}_{n+1}$ 和塑性乘子增量 $\Delta\lambda$。这个方程组通常表示为一个局部残差向量 $\mathbf{R}_{\text{local}}$ 等于零 [@problem_id:3508107]：
    $$
    \mathbf{R}_{\text{local}}(\boldsymbol{\sigma}_{n+1}, \mathbf{q}_{n+1}, \Delta\lambda) = 
    \begin{bmatrix}
    \boldsymbol{\sigma}_{n+1} - \boldsymbol{\sigma}^{\text{tr}} + \Delta\lambda \, \mathbb{C}^e : \mathbf{n}_{n+1} \\
    \mathbf{q}_{n+1} - \mathbf{q}_n - \Delta\lambda \, \mathbf{h}_{n+1} \\
    f(\boldsymbol{\sigma}_{n+1}, \mathbf{q}_{n+1})
    \end{bmatrix}
    = \mathbf{0}
    $$
    其中，第一个方程是应力更新的离散形式，第二个是硬化规律的离散形式，第三个是塑性一致性条件。$\mathbf{n}_{n+1} = \partial g / \partial \boldsymbol{\sigma}|_{n+1}$ 是塑性流动方向，$\mathbf{h}_{n+1}$ 是硬化演化函数。这个系统必须与离散的 **卡罗需-库恩-塔克（Karush-Kuhn-Tucker, KKT）** 条件一起求解：
    $$
    \Delta\lambda \ge 0, \quad f(\boldsymbol{\sigma}_{n+1}, \mathbf{q}_{n+1}) \le 0, \quad \Delta\lambda \cdot f(\boldsymbol{\sigma}_{n+1}, \mathbf{q}_{n+1}) = 0
    $$
    求解这个局部非线性方程组的过程，就是将试探应力“返回”到更新后的屈服面上的过程。从几何上看，对于结合了各向同性弹性和关联流动法则的von Mises塑性模型，这个返回路径是沿径向的（**径向返回**）。更一般地，对于标准的关联塑性模型，返回映射被证明是在由弹性柔度张量 $\mathbb{C}^{-1}$ 定义的能量范数下，将试探应力投影到屈服面上的 **最近点投影（closest-point projection）** [@problem_id:3508100]。

### 算法切线模量的推导

既然我们已经将本构更新形式化为一个局部非线性方程组 $\mathbf{R}_{\text{local}} = \mathbf{0}$，那么算法切线模量 $\mathbb{C}^{\text{alg}}$ 就可以通过对这个方程组进行线性化来得到。其核心思想是应用 **隐函数定理（Implicit Function Theorem）**。

因为在收敛状态下，对于任何（导致塑性加载的）总应变 $\boldsymbol{\varepsilon}_{n+1}$，局部残差 $\mathbf{R}_{\text{local}}$ 恒为零，所以其对 $\boldsymbol{\varepsilon}_{n+1}$ 的全导数也必须为零：
$$
\frac{d\mathbf{R}_{\text{local}}}{d\boldsymbol{\varepsilon}_{n+1}} = \frac{\partial \mathbf{R}_{\text{local}}}{\partial \mathbf{z}} \frac{d\mathbf{z}}{d\boldsymbol{\varepsilon}_{n+1}} + \frac{\partial \mathbf{R}_{\text{local}}}{\partial \boldsymbol{\varepsilon}_{n+1}} = \mathbf{0}
$$
其中 $\mathbf{z}$ 代表局部未知量 $(\boldsymbol{\sigma}_{n+1}, \mathbf{q}_{n+1}, \Delta\lambda)$ 的集合（或其简化形式）。$\frac{\partial \mathbf{R}_{\text{local}}}{\partial \mathbf{z}}$ 是局部问题的雅可比矩阵。通过求解这个线性方程组，我们可以得到局部未知量对总应变的导数，并最终组合出 $\mathbb{C}^{\text{alg}} = \frac{d\boldsymbol{\sigma}_{n+1}}{d\boldsymbol{\varepsilon}_{n+1}}$。

为了具体说明这个过程，我们考虑一个一维小应变弹塑性模型，其弹性模量为 $E$，线性硬化模量为 $H$ [@problem_id:3508061]。塑性加载时的局部残差方程组可以简化为：
$$
\begin{align*}
r_f = \sigma_{n+1} - \sigma_{y0} - H q_{n+1} = 0 \\
r_q = q_{n+1} - q_n - \Delta\lambda = 0
\end{align*}
$$
其中，$\sigma_{n+1}$ 可以用试探应力表示为 $\sigma_{n+1} = E(\varepsilon_{n+1} - \varepsilon^p_n - \Delta\lambda)$。我们将局部未知量视为 $(\Delta\lambda, q_{n+1})$。
首先，将 $\sigma_{n+1}$ 代入 $r_f$ 得到关于未知量的残差向量 $\mathbf{R}(\Delta\lambda, q_{n+1}; \varepsilon_{n+1})$。然后，对 $\mathbf{R} = \mathbf{0}$ 关于 $\varepsilon_{n+1}$ 求全导数：
$$
\frac{\partial \mathbf{R}}{\partial (\Delta\lambda, q_{n+1})} \begin{pmatrix} d\Delta\lambda/d\varepsilon_{n+1} \\ dq_{n+1}/d\varepsilon_{n+1} \end{pmatrix} + \frac{\partial \mathbf{R}}{\partial \varepsilon_{n+1}} = \mathbf{0}
$$
计算出局部雅可比矩阵 $\mathbf{J} = \frac{\partial \mathbf{R}}{\partial (\Delta\lambda, q_{n+1})} = \begin{pmatrix} -E  -H \\ -1  1 \end{pmatrix}$ 和 $\frac{\partial \mathbf{R}}{\partial \varepsilon_{n+1}} = \begin{pmatrix} E \\ 0 \end{pmatrix}$。
求解该线性系统 $\mathbf{J} \begin{pmatrix} d\Delta\lambda/d\varepsilon_{n+1} \\ dq_{n+1}/d\varepsilon_{n+1} \end{pmatrix} = -\begin{pmatrix} E \\ 0 \end{pmatrix}$，我们得到：
$$
\frac{d\Delta\lambda}{d\varepsilon_{n+1}} = \frac{E}{E+H}
$$
最后，对 $\sigma_{n+1} = E(1 - \Delta\lambda/\varepsilon_{n+1})$ 的表达式求导（假设 $\varepsilon_n=0, \varepsilon^p_n=0$），我们得到算法切线模量：
$$
\mathbb{C}^{\text{alg}} = \frac{d\sigma_{n+1}}{d\varepsilon_{n+1}} = E \left( 1 - \frac{d\Delta\lambda}{d\varepsilon_{n+1}} \right) = E \left( 1 - \frac{E}{E+H} \right) = \frac{EH}{E+H}
$$
这个结果直观地表示了弹塑性刚度，它相当于一个弹性弹簧（刚度 $E$）和一个塑性硬化弹簧（刚度 $H$）串联后的等效刚度。这个简单的例子清晰地展示了如何通过系统地线性化离散更新算法来获得一致性切线模量。

### 高阶议题与实践挑战

在将一致性线性化应用于实际的复杂地质力学模型时，会出现一系列理论和数值上的挑战。

#### 有限应变与客观性

当地质材料经历大变形时，必须使用 **有限应变（finite strain）** 理论。在有限应变框架下，一个核心要求是 **物质框架无关性（material frame indifference）**，或称 **客观性（objectivity）**。这意味着本构关系不能依赖于观察者的刚体运动。由于柯西应力的常规时间导数 $\dot{\boldsymbol{\sigma}}$ 是非客观的，我们必须使用一种 **客观应力率（objective stress rate）**，例如Jaumann率或Green-Naghdi率。

这些客观率通常在与材料一起旋转的 **协同旋转（corotational）** 坐标系中定义。因此，有限应变下的返回映射算法通常包括三个步骤：1) 将张量旋转到协同旋转系；2) 在该坐标系中进行（小应变形式的）积分更新；3) 将结果旋转回当前的全局空间坐标系。

一致性线性化此时必须应用于这 **整个** 算法流程，包括所有的旋转操作。$\mathbb{C}^{\text{alg}}$ 的推导将包含额外的“几何”项，这些项来自于对旋转张量本身的微分。至关重要的是，用于线性化的客观率定义必须与用于积分更新的客观率定义 **完全一致**。如果在应力更新时使用Jaumann率，但在线性化时却错误地使用了Green-Naghdi率的公式，那么得到的切线模量就是不一致的。这不仅会破坏全局牛顿法的二次收敛性，还可能破坏算法切线模量本身的客观性 [@problem_id:3508040]。

#### 非光滑屈服面

许多经典的地质材料模型，如 **Mohr-Coulomb** 模型和 **Tresca** 模型，其屈服面在主应力空间中是分段线性的，存在 **棱角（corners）** 和 **顶点（apices）**。在这些非光滑点，屈服面的法向（即塑性流动方向）不是唯一的，导致 $\partial f / \partial \boldsymbol{\sigma}$ 未定义或不连续。这对返回映射算法及其线性化构成了严峻挑战。

-   **顶点奇点**：以Mohr-Coulomb模型的顶点为例，该点对应于静水压力状态（即偏应力为零，$q=0$）。在此点，洛德角（Lode angle）$\theta$ 未定义，导致屈服函数不可微。一个常见的处理方法是 **正则化（regularization）**，即用一个光滑的曲面（如双曲线）来“磨圆”顶点。例如，一个正则化的屈服函数可以是 $f_\varepsilon(\boldsymbol{\sigma}) = \alpha p + \sqrt{q^2 + \varepsilon^2} - k$，其中 $\varepsilon$ 是一个小的正则化参数。通过对这个光滑函数求导，我们可以得到一个在顶点处也良定义的梯度，从而可以一致地推导 $\mathbb{C}^{\text{alg}}$ [@problem_id:3508038]。

-   **棱角穿越**：当一个加载步的应力路径穿越了屈服面的一个棱角时（例如，从Tresca六边形的一个面移动到相邻的面），问题变得更加复杂。在棱角处，塑性流动方向是两个相邻面法向的线性组合。对于整个加载步，不存在一个单一的 $\mathbb{C}^{\text{alg}}$ 可以描述其行为。正确的处理方法是 **步长分割（step partitioning）**。算法需要首先精确计算出应力路径到达棱角所需的时间（或应变）增量 $\Delta t_1$。然后，将原始步长 $\Delta t$ 分割为两个子步：$\Delta t_1$ 和 $\Delta t_2 = \Delta t - \Delta t_1$。对每个子步，应力路径都位于一个光滑的面上，因此可以分别计算其对应的一致性切线模量。这种方法虽然增加了计算的复杂性，但却是处理非光滑塑性的严格途径 [@problem_id:3508023]。

#### 数值稳定性与实现策略

除了理论上的复杂性，实际实现中还存在许多影响算法鲁棒性和效率的问题。

-   **饱和软化/硬化**：在某些材料模型中，硬化或软化模量可能随着塑性变形的累积而趋于零（例如，理想塑性或饱和软化）。当硬化模量接近零时，局部本构问题的雅可比矩阵可能变得奇异或病态。这会导致用于求解局部非线性方程组的牛顿法失效，从而使整个计算过程停滞。为了解决这个问题，可以引入正则化技术，例如微小的 **粘性（viscosity）** 来保证速率依赖性，或者在程序中为硬化模量设置一个极小的下限，以维持局部雅可比矩阵的良态性 [@problem_id:3508030]。

-   **收敛控制**：当全局牛顿步长较大时，它可能为局部本构求解器提供一个远离解的“坏”的初始试探状态，导致局部牛顿迭代发散。为了增强算法的鲁棒性，需要在全局和局部层面进行收敛控制。然而，这两者的方式有本质区别 [@problem_id:3508036]。
    -   **全局层面**：可以使用 **线搜索（line search）** 或信赖域等全局化策略。例如，线搜索在计算出牛顿方向 $\Delta\mathbf{u}$ 后，会寻找一个最优的步长因子 $\alpha \in (0, 1]$ 来更新位移 $\mathbf{u}_{k+1} = \mathbf{u}_k + \alpha \Delta\mathbf{u}$，以确保某种形式的“下降”条件。这个过程不影响 $\mathbf{K}_{\text{cons}}$ 的计算，因此与一致性线性化兼容。
    -   **局部层面**：**不应** 在局部本构求解器的牛顿迭代中使用线搜索。因为这样做会使局部求解过程（即最终的 $(\boldsymbol{\sigma}_{n+1}, \mathbf{q}_{n+1})$）成为一个关于输入应变 $\boldsymbol{\varepsilon}_{n+1}$ 的非光滑函数，从而破坏了应用隐函数定理推导 $\mathbb{C}^{\text{alg}}$ 的前提，最终导致全局二次收敛性的丧失。
    -   正确的做法是，在局部迭代中检测其是否发散。检测方法可以是 **算法性的**（例如，监测局部残差范数是否增大）或 **物理性的**（例如，检查是否违反了热力学第二定律，即计算出的塑性耗散是否为负）。一旦检测到局部发散，应中止当前计算，并向全局求解器发出信号，要求减小全局步长（例如，通过全局线搜索或步长自适应控制），然后用一个更小的全局步长重新尝试。