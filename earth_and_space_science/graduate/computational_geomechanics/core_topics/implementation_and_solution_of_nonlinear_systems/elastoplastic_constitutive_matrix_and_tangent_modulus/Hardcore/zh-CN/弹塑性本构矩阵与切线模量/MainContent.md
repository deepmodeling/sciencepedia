## 引言
在计算科学与工程领域，精确模拟材料从弹性到塑性阶段的非线性行为是分析结构安全性和变形的基础。实现这一目标的核心在于准确描述应力-应变关系的演化，这正是**弹塑性本构矩阵**与**切线模量**发挥作用的地方。然而，在理论推导与数值实现之间存在一个关键的认知鸿沟：即连续介质层面的瞬时模量与有限元算法中保证收敛性所需的一致性切线模量并非等同。未能深刻理解并正确应用后者，是导致数值模拟效率低下甚至失败的常见原因。

本文旨在系统性地阐明这一核心概念，为读者搭建从理论到实践的桥梁。在**第一章：原理与机制**中，我们将从弹性行为的数学表述出发，逐步构建率无关塑性的控制方程，并最终聚焦于区分和推导连续介质切线模量与计算中至关重要的一致性切线模量。随后，在**第二章：应用与跨学科联系**中，我们将展示这些理论如何在J2塑性、Drucker-Prager和修正剑桥等具体岩土本构模型中得到应用，并探讨其在处理非关联流动、各向异性、大变形及材料失稳等前沿问题中的扩展。最后，**第三章：动手实践**将通过一系列编程练习，引导您亲手实现和验证一致性切线模量的优越性，将理论知识转化为解决实际问题的能力。

## 原理与机制

本章旨在深入探讨弹塑性本构关系的核心——弹塑性本构矩阵和切线模量。在计算力学中，对材料非线性行为的精确和高效数值模拟，很大程度上依赖于对这些概念的深刻理解。我们将从线弹性行为的数学表述出发，逐步构建弹塑性理论的框架，并最终阐明在有限元分析中至关重要的**一致性切线模量 (consistent tangent modulus)** 的原理、推导及其在不同本构模型中的应用。

### 弹性行为的数学表示：基础框架

在计算分析中，描述材料点处应力与应变关系的本构定律必须转化为可进行数值计算的矩阵形式。对于三维问题，应力张量 $\boldsymbol{\sigma}$ 和应变张量 $\boldsymbol{\varepsilon}$ 均为二阶对称张量，包含六个独立分量。将这些张量分量排列成一个 $6 \times 1$ 的列向量是标准做法，这一过程称为 **Voigt 记法**。

然而，在进行这种向量化时，必须谨慎处理剪切分量，以确保张量运算和向量运算之间的能量等价性。具体而言，内功率密度在张量形式下表示为 $p = \boldsymbol{\sigma} : \boldsymbol{\varepsilon}$（双点积），我们要求其在向量形式下等价于向量内积。一种常见的约定是采用所谓的**工程应变 (engineering strain)**，它能够保持功共轭关系 $\boldsymbol{\sigma} : \boldsymbol{\varepsilon} = \boldsymbol{\sigma}_v^T \boldsymbol{\varepsilon}_v$，其中下标 $v$ 表示 Voigt 向量。在该约定下，应力向量直接由张量分量构成，而应变向量中的剪切分量则被乘以一个因子 2 [@problem_id:3522254]。对于一个分量排序为 $\{xx, yy, zz, yz, zx, xy\}$ 的系统，其应力向量 $\boldsymbol{\sigma}_v$ 和工程应变向量 $\boldsymbol{\varepsilon}_v$ 定义为：

$$
\boldsymbol{\sigma}_v = [\sigma_{xx}, \sigma_{yy}, \sigma_{zz}, \sigma_{yz}, \sigma_{zx}, \sigma_{xy}]^T
$$

$$
\boldsymbol{\varepsilon}_v = [\varepsilon_{xx}, \varepsilon_{yy}, \varepsilon_{zz}, 2\varepsilon_{yz}, 2\varepsilon_{zx}, 2\varepsilon_{xy}]^T = [\varepsilon_{xx}, \varepsilon_{yy}, \varepsilon_{zz}, \gamma_{yz}, \gamma_{zx}, \gamma_{xy}]^T
$$

在此约定下，三维各向同性线弹性材料的本构关系 $\boldsymbol{\sigma}_v = D^e \boldsymbol{\varepsilon}_v$ 可以通过一个 $6 \times 6$ 的**弹性刚度矩阵 (elastic stiffness matrix)** $D^e$ 来表示。该矩阵通常用体积模量 $K$ 和剪切模量 $G$ 来参数化，其形式为 [@problem_id:3522303]：

$$
D^e = \begin{pmatrix}
K + \frac{4G}{3} & K - \frac{2G}{3} & K - \frac{2G}{3} & 0 & 0 & 0 \\
K - \frac{2G}{3} & K + \frac{4G}{3} & K - \frac{2G}{3} & 0 & 0 & 0 \\
K - \frac{2G}{3} & K - \frac{2G}{3} & K + \frac{4G}{3} & 0 & 0 & 0 \\
0 & 0 & 0 & G & 0 & 0 \\
0 & 0 & 0 & 0 & G & 0 \\
0 & 0 & 0 & 0 & 0 & G
\end{pmatrix}
$$

这个矩阵结构揭示了各向同性材料的一个基本特性：体积变形（由正应变引起）与剪切变形（由剪应变引起）之间没有耦合。

更深刻的理解来自于**体积-偏量分解 (volumetric-deviatoric decomposition)**。任何对称张量（如应力或应变）都可以分解为一个球张量（体积部分）和一个偏张量（偏量部分）。例如，应变张量可以分解为 $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^{vol} + \boldsymbol{\varepsilon}^{dev}$，其中 $\boldsymbol{\varepsilon}^{vol} = \frac{1}{3}\mathrm{tr}(\boldsymbol{\varepsilon})\boldsymbol{I}$ 是体积应变，$\boldsymbol{\varepsilon}^{dev} = \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{vol}$ 是偏应变。对于各向同性弹性，本构关系可以优雅地分解为两个独立的部分：
$$
p = K \cdot \mathrm{tr}(\boldsymbol{\varepsilon}) \quad \text{和} \quad \boldsymbol{s} = 2G \boldsymbol{\varepsilon}^{dev}
$$
其中 $p = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})$ 是平均应力（或静水压力），$\boldsymbol{s}$ 是偏应力张量。这种分解不仅在物理上直观，也为代数操作提供了便利。弹性刚度矩阵 $D^e$ 也可以通过两个投影算子——体积投影算子 $P^{vol}$ 和偏量投影算子 $P^{dev}$——进行谱分解：$D^e = 3K P^{vol} + 2G P^{dev}$ [@problem_id:3522303]。

本构关系的逆关系由**弹性柔度矩阵 (elastic compliance matrix)** $C^e = (D^e)^{-1}$ 给出，它将应力映射到应变：$\boldsymbol{\varepsilon}_v = C^e \boldsymbol{\sigma}_v$。通过对体积和偏量关系求逆，可以推导出 $C^e$ 的形式 [@problem_id:3522218]：

$$
\boldsymbol{\varepsilon} = \frac{1}{2G}\boldsymbol{s} + \frac{1}{9K}\mathrm{tr}(\boldsymbol{\sigma})\boldsymbol{I} = \frac{1}{2G}\left(\boldsymbol{\sigma} - \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})\boldsymbol{I}\right) + \frac{1}{9K}\mathrm{tr}(\boldsymbol{\sigma})\boldsymbol{I}
$$

将上式转换为 Voigt 记法下的 $6 \times 6$ 矩阵，我们得到 $C^e$。为了使材料在能量上保持稳定，弹性应变能必须是正定的，这要求弹性刚度矩阵 $D^e$（及其逆矩阵 $C^e$）是正定的。通过分析其特征值可以证明，这一条件的物理意义是体积模量和剪切模量必须为正，即 $K > 0$ 和 $G > 0$ [@problem_id:3522218]。

### 率无关塑性：控制方程

当材料的应力状态达到其弹性极限时，便会发生塑性变形。对于率无关塑性，其行为由一组核心方程和条件所支配。这些要素包括：

1.  **屈服函数 (Yield Function)**: 一个标量函数 $f(\boldsymbol{\sigma}, \boldsymbol{\kappa}) \le 0$，它定义了弹性区域的边界。其中 $\boldsymbol{\sigma}$ 是应力张量，$\boldsymbol{\kappa}$ 是一组描述材料历史状态的内变量（例如等效塑性应变）。$f  0$ 表示纯弹性状态，$f=0$ 表示应力位于屈服面上，而 $f > 0$ 在物理上是不允许的。

2.  **塑性势函数 (Plastic Potential)**: 一个标量函数 $g(\boldsymbol{\sigma}, \boldsymbol{\kappa})$，其梯度定义了塑性应变率的方向。塑性流动法则是 $\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}}$，其中 $\dot{\lambda}$ 是非负的**塑性乘子率 (plastic multiplier rate)**。如果 $g=f$，则称为**关联流动法则 (associated flow rule)**；否则为**非关联流动法则 (non-associated flow rule)**。

3.  **加积应变分解 (Additive Strain Decomposition)**: 总应变率 $\dot{\boldsymbol{\varepsilon}}$ 被假定为弹性部分 $\dot{\boldsymbol{\varepsilon}}^e$ 和塑性部分 $\dot{\boldsymbol{\varepsilon}}^p$ 的和：$\dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^e + \dot{\boldsymbol{\varepsilon}}^p$。

这些要素与一组称为 **Karush-Kuhn-Tucker (KKT) 条件**的互补条件相结合，完整地描述了加载和卸载过程 [@problem_id:3522245]：
$$
f \le 0, \quad \dot{\lambda} \ge 0, \quad \dot{\lambda}f = 0
$$
这些条件简洁地表达了：应力状态不能超出屈服面；塑性变形是不可逆的；只有当应力状态位于屈服面上时，才能发生塑性流动（$\dot{\lambda}0$）。

当塑性加载发生时（即 $\dot{\lambda}0$），应力状态必须保持在屈服面上。这意味着屈服函数的时间导数必须为零，即**一致性条件 (consistency condition)**：$\dot{f}=0$。对于一个只依赖于应力和一个标量硬化变量 $\kappa$ 的材料，一致性条件可以展开为：
$$
\dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \dot{\boldsymbol{\sigma}} + \frac{\partial f}{\partial \kappa} \dot{\kappa} = 0
$$
通过这个条件，我们可以推导出弹塑性本构关系的核心——**连续介质弹塑性切线模量 (continuum elastoplastic tangent modulus)** $D^{ep}_{\text{cont}}$。让我们以一个无硬化（理想塑性，$\dot{\kappa}=0$）的非关联模型为例。一致性条件简化为 $N:\dot{\boldsymbol{\sigma}}=0$，其中 $N = \partial f / \partial \boldsymbol{\sigma}$ 是屈服面的法向量。应力率由弹性关系给出：$\dot{\boldsymbol{\sigma}} = D^e : (\dot{\boldsymbol{\varepsilon}} - \dot{\boldsymbol{\varepsilon}}^p)$。将塑性流动法则 $\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} M$（其中 $M = \partial g / \partial \boldsymbol{\sigma}$ 是塑性流动方向）代入，得到：
$$
\dot{\boldsymbol{\sigma}} = D^e : (\dot{\boldsymbol{\varepsilon}} - \dot{\lambda} M)
$$
将此 $\dot{\boldsymbol{\sigma}}$ 的表达式代入一致性条件 $N:\dot{\boldsymbol{\sigma}}=0$ 中，我们便可以求解未知的塑性乘子率 $\dot{\lambda}$ [@problem_id:3522245]：
$$
N : [D^e : (\dot{\boldsymbol{\varepsilon}} - \dot{\lambda} M)] = 0 \implies \dot{\lambda} = \frac{N : D^e : \dot{\boldsymbol{\varepsilon}}}{N : D^e : M}
$$
这个表达式只有在分子 $N : D^e : \dot{\boldsymbol{\varepsilon}}  0$（即弹性试探应力率指向屈服面外部）时才为正，这构成了塑性加载的判据。将 $\dot{\lambda}$ 的表达式代回 $\dot{\boldsymbol{\sigma}}$ 的方程中，我们最终可以得到一个直接关联应力率和应变率的方程 $\dot{\boldsymbol{\sigma}} = D^{ep}_{\text{cont}} : \dot{\boldsymbol{\varepsilon}}$，其中 $D^{ep}_{\text{cont}}$ 的一般形式（考虑硬化模量 $H$）为：
$$
D^{ep}_{\text{cont}} = D^e - \frac{(D^e : M) \otimes (N : D^e)}{H + N : D^e : M}
$$
这个四阶张量 $D^{ep}_{\text{cont}}$ 描述了材料在当前状态下对无穷小应变率的瞬时响应。重要的是要认识到，它是一个**连续介质**层面的概念，其推导不依赖于任何特定的数值时间积分方案。

### 从连续介质到计算：算法切线模量

在计算力学中，我们处理的是有限的时间步或荷载步，而不是无穷小的率。因此，我们需要对上述率形式的本构方程进行时间积分，以获得一个在增量步 $\Delta t$ 内更新应力 $\boldsymbol{\sigma}_{n+1}$ 的算法。一个广泛使用的积分方案是**后向欧拉法 (backward Euler method)**，它构成了所谓的**返回映射算法 (return-mapping algorithm)** 的基础。

为了理解为何需要一种新的切线模量，我们必须将目光从材料点层面转向全局有限元（FEM）分析的背景 [@problem_id:3522208]。一个准静态问题的有限元离散化，最终归结为求解一个大型非线性代数方程组 $R(\boldsymbol{d}) = 0$，其中 $R(\boldsymbol{d})$ 是全局残差向量，$\boldsymbol{d}$ 是节点位移向量。该残差向量通常表示为内力向量与外力向量之差：
$$
R(\boldsymbol{d}) = F_{int}(\boldsymbol{d}) - F_{ext} = \int_{\Omega} B^T \boldsymbol{\sigma}(\boldsymbol{\varepsilon}(\boldsymbol{d})) d\Omega - F_{ext} = 0
$$
这里，$B$ 是应变-位移矩阵。求解该非线性方程组最强大的方法之一是 **Newton-Raphson 迭代法**。在每次迭代中，我们求解一个线性方程组来更新位移增量 $\Delta\boldsymbol{d}$：
$$
K_T \Delta\boldsymbol{d} = -R(\boldsymbol{d}_i)
$$
其中 $K_T = \partial R / \partial \boldsymbol{d}$ 是残差向量的雅可比矩阵，即**全局切线刚度矩阵 (global tangent stiffness matrix)**。通过链式法则，可以推导出 $K_T$ 的结构：
$$
K_T = \frac{\partial R}{\partial \boldsymbol{d}} = \int_{\Omega} B^T \frac{\partial \boldsymbol{\sigma}}{\partial \boldsymbol{\varepsilon}} B d\Omega
$$
Newton-Raphson 方法的一个关键特性是，如果使用精确的雅可比矩阵，它在解的邻域内具有**二次收敛 (quadratic convergence)** 速率。这就引出了核心问题：在非线性本构的离散增量步中，$\partial \boldsymbol{\sigma} / \partial \boldsymbol{\varepsilon}$ 究竟是什么？

它**不是**我们之前推导的连续介质切线模量 $D^{ep}_{\text{cont}}$。原因在于，在 Newton-Raphson 迭代中，$\boldsymbol{\sigma}$ 是由一个数值算法（返回映射算法）计算得到的、关于当前迭代步应变 $\boldsymbol{\varepsilon}$ 的离散函数，我们记为 $\boldsymbol{\sigma}_{n+1} = \mathcal{G}(\boldsymbol{\varepsilon}_{n+1}, \text{state}_n)$。为了获得二次收敛，我们需要的切线模量必须是这个离散更新算法的精确线性化，即 [@problem_id:3522256]：
$$
D^{alg} \equiv \frac{\partial \boldsymbol{\sigma}_{n+1}}{\partial \boldsymbol{\varepsilon}_{n+1}} = \frac{\partial \mathcal{G}(\boldsymbol{\varepsilon}_{n+1}, \text{state}_n)}{\partial \boldsymbol{\varepsilon}_{n+1}}
$$
这个量被称为**算法切线模量 (algorithmic tangent modulus)** 或**一致性切线模量 (consistent tangent modulus)**，因为它与应力积分算法保持一致。

在塑性加载过程中，由于返回映射算法是一个非线性投影过程，$D^{alg}$ 通常与 $D^{ep}_{\text{cont}}$ 不同。只有在纯弹性加载或卸载时，应力更新是线性的，两者才会与弹性矩阵 $D^e$ 一致。如果在 Newton-Raphson 迭代中使用 $D^{ep}_{\text{cont}}$ 或其他近似（如弹性矩阵 $D^e$）来代替 $D^{alg}$，全局雅可比矩阵将是不精确的，迭代法会退化为所谓的拟牛顿法 (quasi-Newton method)，其收敛速率通常会降为线性甚至更慢 [@problem_id:3522256, @problem_id:3522208]。因此，为了实现计算效率和鲁棒性，推导并使用正确的一致性切线模量是现代计算塑性力学的核心任务之一。

### 案例研究：J2 塑性与径向返回算法

为了将一致性切线模量的抽象概念具体化，我们以一个在金属和岩土材料中广泛应用的经典模型为例：带线性各向同性硬化的 **J2 塑性模型**（也称 von Mises 塑性）。其返回映射算法，即**径向返回算法 (radial return algorithm)**，是理解一致性切线模量推导过程的典范 [@problem_id:3522257]。

考虑一个应变增量步 $\Delta\boldsymbol{\varepsilon}$。算法流程如下：

1.  **弹性试探 (Elastic Trial)**: 假定整个增量步是纯弹性的，计算试探应力状态。由于 J2 塑性只由偏应力驱动，体积响应是纯弹性的：$p_{n+1} = p_n + K \cdot \mathrm{tr}(\Delta\boldsymbol{\varepsilon})$。试探偏应力为 $s^{\text{tr}} = s_n + 2G \Delta\boldsymbol{\varepsilon}^{dev}$。

2.  **屈服判断 (Yield Check)**: 使用试探偏应力计算屈服函数值 $f^{\text{tr}} = \sqrt{\frac{3}{2}} \|s^{\text{tr}}\| - \sigma_y(\kappa_n)$。如果 $f^{\text{tr}} \le 0$，则该步骤确实是弹性的，试探应力即为最终应力，算法结束。

3.  **塑性修正 (Plastic Corrector)**: 如果 $f^{\text{tr}}  0$，则发生了塑性变形，试探应力在物理上是不可及的，必须将其“返回”到更新后的屈服面上。对于 J2 关联流动，塑性应变增量是纯偏量的，且其方向与最终的偏应力方向一致。最终的偏应力 $s_{n+1}$ 可以表示为：
    $$
    s_{n+1} = s^{\text{tr}} - 2G \Delta\boldsymbol{\varepsilon}^p = s^{\text{tr}} - 2G \Delta\lambda \sqrt{\frac{3}{2}} n_{n+1}
    $$
    其中 $n_{n+1} = s_{n+1}/\|s_{n+1}\|$ 是最终偏应力方向的单位张量。这个方程表明，$s_{n+1}$ 与 $s^{\text{tr}}$ 共线，因此有 $n_{n+1} = n^{\text{tr}} = s^{\text{tr}}/\|s^{\text{tr}}\|$。这就是“径向返回”名称的由来。

4.  **求解塑性乘子**: 在增量步结束时，一致性条件 $f(s_{n+1}, \kappa_{n+1})=0$ 必须满足。结合硬化定律 $\Delta\kappa = \Delta\lambda$，可以建立一个关于塑性乘子增量 $\Delta\lambda$ 的标量方程，并求得其显式解：
    $$
    \Delta\lambda = \frac{f^{\text{tr}}}{3G + H}
    $$
    其中 $H$ 是线性硬化模量。

5.  **推导一致性切线模量**: 有了 $\Delta\lambda$ 的显式表达式，我们就可以写出 $s_{n+1}$ 关于 $\varepsilon_{n+1}$ (通过 $s^{\text{tr}}$) 的完整函数关系。一致性切线模量 $D^{alg}$ 就是通过对这个复杂的、非线性的函数关系式关于 $\varepsilon_{n+1}$ 求导得到的。这个求导过程涉及对 $\|s^{\text{tr}}\|$ 和 $n^{\text{tr}}$ 等项使用链式法则，过程较为繁琐，但最终可以得到一个精确的解析表达式。对于 J2 塑性，其一致性切线模量可以分解为体积部分和偏量部分。完整的切线模量 $D^{alg} = \partial \sigma_{n+1} / \partial \varepsilon_{n+1}$ 的形式为：
    $$
    D^{alg} = K (\boldsymbol{I} \otimes \boldsymbol{I}) + 2G\alpha I^{\text{dev}} + 2G\left(\frac{H}{3G+H} - \alpha\right) (n^{\text{tr}} \otimes n^{\text{tr}})
    $$
    其中 $\alpha = \frac{\|s_{n+1}\|}{\|s^{\text{tr}}\|}$ 是一个缩放因子，代表了应力返回的程度，$I^{\text{dev}}$ 是四阶偏量投影张量。这个表达式精确地捕捉了返回映射算法的几何和代数特性，是保证 Newton-Raphson 方法二次收敛性的关键。

### 高级专题与复杂性

虽然 J2 塑性模型提供了一个清晰的范例，但在岩土工程实践中，我们经常遇到更复杂的本构行为，这些行为给切线模量的构建带来了新的挑战。

#### 非关联流动与不对称切线模量

许多岩土材料，如砂土和密实黏土，表现出剪胀性（剪切变形伴随着体积膨胀），其塑性体积应变的大小通常与屈服面对应力（压力）的敏感性不匹配。这通过采用不等的屈服函数 $f$ 和塑性势函数 $g$ (即 $f \neq g$) 来建模，导致了**非关联流动**。例如，在 Drucker-Prager 模型中，可以为 $f$ 和 $g$ 分别指定不同的压力敏感性系数 $a$ 和 $b$ [@problem_id:3522233]。在这种情况下，屈服面法向 $N = \partial f / \partial \boldsymbol{\sigma}$ 与塑性流动方向 $M = \partial g / \partial \boldsymbol{\sigma}$ 不再相同。

这种非关联性对弹塑性切线模量有着深远的影响。回顾连续介质切线模量的表达式，其塑性修正项为 $\frac{(D^e : M) \otimes (N : D^e)}{A}$。由于 $M \neq N$，张量外积 $(D^e : M) \otimes (N : D^e)$ 通常不再具有主、次对称性。其结果是，**非关联塑性模型的连续介质和一致性切线模量通常都是非对称的**。在有限元实现中，这意味着全局切线刚度矩阵 $K_T$ 也会变得非对称，需要使用非对称方程求解器，这会增加计算成本。

#### 非光滑屈服面

许多经典的岩土塑性模型，如 **Mohr-Coulomb** 和 **Tresca** 模型，其屈服面在主应力空间中包含**角点 (corners)** 和**棱线 (edges)**。在这些非光滑点上，屈服面的梯度 $\partial f / \partial \boldsymbol{\sigma}$ 不是唯一的，而是由一个称为**次梯度 (subdifferential)** 的集合所描述 [@problem_id:3522276]。

这种梯度的不唯一性带来了根本性的困难。首先，塑性流动方向变得不确定。其次，由于一致性切线模量的推导依赖于对屈服函数的求导，一个唯一的 $D^{alg}$ 也就无从谈起。如果应力状态在迭代过程中恰好落在一个角点或棱线上，标准的返回映射算法会失效，全局 Newton-Raphson 迭代的二次收敛性也会丧失。

为了解决这个问题，研究人员发展了多种专门的算法，主要包括：
*   **角点光滑化/正则化 (Regularization)**: 用一个光滑的函数来近似非光滑的屈服面。
*   **多面塑性 (Multi-surface Plasticity)**: 将角点视为多个光滑屈服面的交点，并同时激活多个塑性流动机制。
*   **非光滑优化算法**: 直接在非光滑框架内求解返回映射问题。
这些高级技术是处理实际岩土材料建模时不可或缺的。

#### 客观性与有限应变

本章的讨论主要局限于小应变理论。当变形显著，以至于物体的几何形状发生大的改变时，必须采用**有限应变 (finite strain)** 理论。在有限应变框架下，一个核心要求是**物质客观性原理 (principle of material frame-indifference)**，即本构关系不能依赖于观察者（坐标系）的刚体运动 [@problem_id:3522226]。

在小应变理论中，由于忽略了转动的影响，这一原理近似满足。但在有限应变中，简单的 Cauchy 应力率 $\dot{\boldsymbol{\sigma}}$ 不是客观的，因为它包含了由材料自旋引起的非物理性变化。为了构建客观的本构关系，必须使用一种**客观应力率 (objective stress rate)**，例如 Jaumann 率或 Truesdell 率。本构关系通常写成如下形式：
$$
\overset{\circ}{\boldsymbol{\sigma}} = \mathbb{D}^{ep} : \boldsymbol{d}
$$
其中 $\overset{\circ}{\boldsymbol{\sigma}}$ 是所选的客观应力率，$\boldsymbol{d}$ 是变形率张量（速度梯度的对称部分）。客观应力率的定义中通常包含当前应力状态 $\boldsymbol{\sigma}$ 和自旋张量 $\boldsymbol{w}$（速度梯度的反对称部分）。这导致在推导一致性切线模量时，会引入额外的、依赖于当前应力状态的项，使得本构关系变得更加复杂。这些是高级计算力学课程中将要深入探讨的主题。