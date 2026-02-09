## 引言
线性弹性理论与胡克定律是理解固体材料在外力作用下如何变形的基石，构成了从地球物理学到结构工程等众多科学与技术领域的理论核心。这一理论以其简洁的数学形式描述了应力与应变之间的线性关系，为我们预测和分析从微观晶格到宏观地质构造的力学行为提供了强有力的工具。然而，要真正掌握其精髓，不仅需要理解其基本概念，更要深入其背后的数学框架、物理假设及其适用边界。本文旨在系统性地解决这一知识需求，为读者构建一个关于线性弹性的完整知识体系。

本文将引导读者分三步深入探索线性弹性的世界。在“原理与机制”一章中，我们将从应变张量的精确定义及其线性化假设出发，逐步推导适用于各向同性及各向异性材料的胡克定律，并阐明各类弹性模量的物理意义与相互联系。接下来，在“应用与跨学科联系”一章，我们将展示这些理论原理如何转化为解决真实世界问题的强大武器，通过横跨地球物理、材料科学、工程乃至生物力学的案例，彰显其惊人的普适性。最后，“动手实践”部分将提供一系列精心设计的计算练习，帮助读者将理论知识应用于实践，巩固并深化理解。现在，让我们从其最核心的理论基础开始。

## 原理与机制

在介绍章节之后，我们现在深入探讨线性弹性理论的核心原理与力学机制。本章旨在从基本定义出发，系统地构建描述地质材料在小变形下应力-应变响应的数学框架。我们将从应变的精确定义及其线性化假设开始，推导各向同性材料的胡克定律，并阐明各种弹性模量（如拉梅参数、杨氏模量、泊松比和体积模量）的物理意义及它们之间的内在联系。随后，我们将探讨在地球物理学中至关重要的各向异性问题，并介绍一些支配弹性系统行为的普适性原理，如应变协调性和互易定理。最后，我们将通过一个简单的粘弹性模型，揭示线性弹性理论作为更广义流变模型瞬时响应极限的深刻内涵。

### 应变张量的定义及其线性化

描述一个连续介质的变形，我们首先需要一个数学工具来量化其内部各点位形的改变。我们引入**位移场** $\mathbf{u}(\mathbf{X})$，它表示材料中初始位置为 $\mathbf{X}$ 的物质点在变形后相对于初始位置的矢量偏移，即其最终位置为 $\mathbf{x} = \mathbf{X} + \mathbf{u}(\mathbf{X})$。

变形的局部特性由**变形梯度张量** $\mathbf{F}$ 描述，其定义为空间坐标 $\mathbf{x}$ 对物质坐标 $\mathbf{X}$ 的梯度：
$$
\mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}}
$$
利用位移场的定义，我们可以将 $\mathbf{F}$ 与位移场联系起来：
$$
\mathbf{F} = \frac{\partial (\mathbf{X} + \mathbf{u})}{\partial \mathbf{X}} = \frac{\partial \mathbf{X}}{\partial \mathbf{X}} + \frac{\partial \mathbf{u}}{\partial \mathbf{X}} = \mathbf{I} + \nabla \mathbf{u}
$$
其中, $\mathbf{I}$ 是二阶单位张量，而 $\mathbf{G} = \nabla \mathbf{u}$ 是**位移梯度张量**。

应变是衡量材料内部相对伸长和角度变化的无量纲量。一个精确且在刚体转动下不变的应变量是**格林-拉格朗日应变张量** (Green-Lagrange strain tensor) $\mathbf{E}$，其定义为：
$$
\mathbf{E} = \frac{1}{2}(\mathbf{F}^{\top}\mathbf{F} - \mathbf{I})
$$
将 $\mathbf{F} = \mathbf{I} + \mathbf{G}$ 代入上式，我们得到 $\mathbf{E}$ 与位移梯度 $\mathbf{G}$ 之间的关系：
$$
\mathbf{E} = \frac{1}{2}((\mathbf{I} + \mathbf{G})^{\top}(\mathbf{I} + \mathbf{G}) - \mathbf{I}) = \frac{1}{2}(\mathbf{I} + \mathbf{G}^{\top} + \mathbf{G} + \mathbf{G}^{\top}\mathbf{G} - \mathbf{I}) = \frac{1}{2}(\mathbf{G} + \mathbf{G}^{\top}) + \frac{1}{2}\mathbf{G}^{\top}\mathbf{G}
$$
这个表达式是完全非线性的。然而，在计算地球物理的许多应用中，如地震波传播或地壳的潮汐响应，位移梯度非常小。这构成了**线性弹性理论**的基础。

当位移梯度足够小时，即其范数（例如，算子范数）$\|\mathbf{G}\|_2 \ll 1$，则二次项 $\frac{1}{2}\mathbf{G}^{\top}\mathbf{G}$ 的贡献远小于线性项。我们可以定义**无穷小应变张量** (infinitesimal strain tensor) $\boldsymbol{\varepsilon}$ 为位移梯度的对称部分：
$$
\boldsymbol{\varepsilon} = \frac{1}{2}(\mathbf{G} + \mathbf{G}^{\top}) = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^{\top})
$$
此时，格林-拉格朗日应变张量 $\mathbf{E}$ 可以近似为 $\boldsymbol{\varepsilon}$。这种线性化所引入的误差是 $\mathbf{E} - \boldsymbol{\varepsilon} = \frac{1}{2}\mathbf{G}^{\top}\mathbf{G}$。为了量化这个误差，我们可以考虑一个具体情景：假设通过大地测量观测到某地壳区域的位移梯度范数上界为 $\|\mathbf{G}(\mathbf{X})\|_2 \le 10^{-3}$。利用矩阵范数的性质，我们可以估算被忽略的非线性项的范数上界 [@problem_id:3607932]：
$$
\|\mathbf{E} - \boldsymbol{\varepsilon}\|_2 = \left\| \frac{1}{2}\mathbf{G}^{\top}\mathbf{G} \right\|_2 \le \frac{1}{2}\|\mathbf{G}^{\top}\|_2\|\mathbf{G}\|_2 = \frac{1}{2}\|\mathbf{G}\|_2^2 \le \frac{1}{2}(10^{-3})^2 = 5 \times 10^{-7}
$$
这个数值极小，表明对于绝大多数小变形的地球物理问题，使用无穷小应变张量 $\boldsymbol{\varepsilon}$ 是一个非常精确的近似。在后续的讨论中，我们将默认采用此线性化应变定义。

### 各向同性材料的胡克定律

在弹性力学中，**应力**描述了物体内部相互作用力的强度和方向，由**柯西应力张量** (Cauchy stress tensor) $\boldsymbol{\sigma}$ 表示。线性弹性理论的核心假设是应力与应变之间存在线性关系，这被称为**广义胡克定律** (generalized Hooke's law)：
$$
\sigma_{ij} = C_{ijkl} \varepsilon_{kl}
$$
其中 $C_{ijkl}$ 是一个四阶张量，称为**弹性刚度张量** (elastic stiffness tensor)。

对于许多地球物理问题，将材料假设为**各向同性** (isotropic) 是一个有效的一阶近似。各向同性意味着材料的力学性质在所有方向上都是相同的，这极大地简化了刚度张量 $\mathbf{C}$。对于各向同性材料，其刚度张量可以仅用两个独立的标量常数来表示。这使得应力-应变关系呈现出一种标准形式 [@problem_id:3607930]：
$$
\boldsymbol{\sigma} = \lambda \operatorname{tr}(\boldsymbol{\varepsilon}) \mathbf{I} + 2\mu \boldsymbol{\varepsilon}
$$
这里的 $\lambda$ 和 $\mu$ 是两个弹性常数，被称为**拉梅参数** (Lamé parameters)。$\operatorname{tr}(\boldsymbol{\varepsilon})$ 是应变张量的迹，代表了材料的**体积应变** (volumetric strain)，即 $\varepsilon_v = \varepsilon_{11} + \varepsilon_{22} + \varepsilon_{33}$。

这个关系式揭示了一个深刻的物理图像：各向同性材料的响应可以分解为体积响应和剪切响应。为了更清楚地看到这一点，我们可以将应力张量和应变张量分解为球量部分（体积部分）和偏量部分（剪切部分）。

**1. 体积响应 (Volumetric Response)**

我们对胡克定律方程两边取迹：
$$
\operatorname{tr}(\boldsymbol{\sigma}) = \operatorname{tr}(\lambda \operatorname{tr}(\boldsymbol{\varepsilon}) \mathbf{I} + 2\mu \boldsymbol{\varepsilon}) = \lambda \operatorname{tr}(\boldsymbol{\varepsilon}) \operatorname{tr}(\mathbf{I}) + 2\mu \operatorname{tr}(\boldsymbol{\varepsilon})
$$
在三维空间中，$\operatorname{tr}(\mathbf{I}) = 3$，因此：
$$
\operatorname{tr}(\boldsymbol{\sigma}) = (3\lambda + 2\mu) \operatorname{tr}(\boldsymbol{\varepsilon})
$$
定义**平均正向应力** (mean normal stress) 为 $p_m = \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})$。则上式可写为 $p_m = (\lambda + \frac{2}{3}\mu) \operatorname{tr}(\boldsymbol{\varepsilon})$。这表明平均正向应力与体积应变成正比。比例系数定义为**体积模量** (bulk modulus) $K$：
$$
K = \lambda + \frac{2}{3}\mu
$$
体积模量 $K$ 衡量了材料抵抗均匀压缩的能力。

**2. 剪切响应 (Deviatoric Response)**

应力张量和应变张量可以分解为：
$$
\boldsymbol{\sigma} = \mathbf{s} + \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})\mathbf{I} = \mathbf{s} + p_m\mathbf{I}
$$
$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}_{\mathrm{dev}} + \frac{1}{3}\operatorname{tr}(\boldsymbol{\varepsilon})\mathbf{I}
$$
其中 $\mathbf{s}$ 和 $\boldsymbol{\varepsilon}_{\mathrm{dev}}$ 分别是**偏应力张量** (deviatoric stress tensor) 和**偏应变张量** (deviatoric strain tensor)，它们都是无迹的。将这些分解代入胡克定律：
$$
\mathbf{s} + p_m\mathbf{I} = \lambda \operatorname{tr}(\boldsymbol{\varepsilon}) \mathbf{I} + 2\mu (\boldsymbol{\varepsilon}_{\mathrm{dev}} + \frac{1}{3}\operatorname{tr}(\boldsymbol{\varepsilon})\mathbf{I}) = 2\mu \boldsymbol{\varepsilon}_{\mathrm{dev}} + (\lambda + \frac{2}{3}\mu)\operatorname{tr}(\boldsymbol{\varepsilon})\mathbf{I}
$$
利用 $p_m = K \operatorname{tr}(\boldsymbol{\varepsilon})$ 和 $K = \lambda + \frac{2}{3}\mu$，我们发现方程两边的球量部分（与 $\mathbf{I}$ 成比例的部分）相等。因此，我们得到了一个仅关于偏量部分的简洁关系：
$$
\mathbf{s} = 2\mu \boldsymbol{\varepsilon}_{\mathrm{dev}}
$$
这个关系表明偏应力与偏应变成正比，比例系数为 $2\mu$。这证实了拉梅第二参数 $\mu$ 的物理意义：它是**剪切模量** (shear modulus)，衡量材料抵抗形状改变（剪切变形）的能力。

**3. 柔度形式 (Compliance Form)**

胡克定律的“刚度形式”将应力表示为应变的函数。在许多情况下，将应变表示为应力的函数，即“柔度形式”，也同样有用。我们可以通过代数运算反转刚度形式的方程。如上所述，$\operatorname{tr}(\boldsymbol{\varepsilon}) = \frac{\operatorname{tr}(\boldsymbol{\sigma})}{3\lambda+2\mu}$。将其代入 $\boldsymbol{\varepsilon} = \frac{1}{2\mu}(\boldsymbol{\sigma} - \lambda \operatorname{tr}(\boldsymbol{\varepsilon})\mathbf{I})$，我们得到：
$$
\boldsymbol{\varepsilon} = \frac{1}{2\mu}\boldsymbol{\sigma} - \frac{\lambda \operatorname{tr}(\boldsymbol{\sigma})}{2\mu(3\lambda+2\mu)}\mathbf{I}
$$
这个形式在处理应力边界条件问题时特别方便。更有启发性的是，我们可以将其用偏应力 $s$ 和静水压力 $p = -p_m = -\frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})$ 来表示 [@problem_id:3607913]。经过推导，可得一个优雅的解耦形式：
$$
\boldsymbol{\varepsilon} = \frac{1}{2\mu}\mathbf{s} - \frac{1}{3K}p\mathbf{I}
$$
这个方程清晰地表明，总应变是剪切变形和体积变形的线性叠加：剪切应变由偏应力通过剪切模量 $\mu$ 决定，而体积应变由静水压力通过体积模量 $K$ 决定。

### 工程弹性模量及其相互关系

虽然拉梅参数 $(\lambda, \mu)$ 和体积模量 $K$ 在理论上很方便，但在工程和实验地球物理学中，另外两个弹性常数——**杨氏模量** (Young's modulus) $E$ 和**泊松比** (Poisson's ratio) $\nu$——更为常用。

- **杨氏模量 $E$**：定义于单轴应力测试中，即只有一个方向（如 $x_1$ 方向）有正向应力 $\sigma_{11}$，而所有其他应力分量为零。杨氏模量是该方向上的应力与应变之比：$E = \sigma_{11}/\varepsilon_{11}$。它衡量材料在单轴拉伸或压缩下的刚度。
- **泊松比 $\nu$**：在相同的单轴测试中，材料在受力方向上伸长（或缩短）的同时，会在垂直于受力方向的横向收缩（或膨胀）。泊松比定义为横向应变与轴向应变之比的负值：$\nu = -\varepsilon_{22}/\varepsilon_{11} = -\varepsilon_{33}/\varepsilon_{11}$。它描述了材料的横向变形效应。

这五种弹性模量 $(\lambda, \mu, K, E, \nu)$ 并非各自独立；对于各向同性材料，任意两个都可以确定其他所有。通过在单轴应力条件下分析各向同性胡克定律，我们可以推导出它们之间的转换关系 [@problem_id:3607879]。关键的推导步骤如下：

1.  在单轴应力条件下 ($\sigma_{11} \neq 0, \sigma_{22}=\sigma_{33}=0$)，利用胡克定律的 $\sigma_{22}=0$ 分量和泊松比的定义，可以建立 $\lambda$ 和 $\mu$ 之间的关系：$\lambda(1-2\nu) = 2\mu\nu$。
2.  然后，利用 $\sigma_{11}$ 分量和杨氏模量的定义，结合上述关系，可以推导出 $E = 2\mu(1+\nu)$。
3.  联立以上两式，即可解出所有转换公式。

以下是一些最常用的转换公式：
- 从 $(E, \nu)$ 到 $(\lambda, \mu, K)$:
  $$
  \mu = \frac{E}{2(1+\nu)}, \quad \lambda = \frac{E\nu}{(1+\nu)(1-2\nu)}, \quad K = \frac{E}{3(1-2\nu)}
  $$
- 从 $(\lambda, \mu)$ 到 $(E, \nu, K)$:
  $$
  E = \frac{\mu(3\lambda+2\mu)}{\lambda+\mu}, \quad \nu = \frac{\lambda}{2(\lambda+\mu)}, \quad K = \lambda + \frac{2}{3}\mu
  $$
这些关系在地球物理建模中至关重要，因为不同的测量技术（如地震波速、实验室岩石力学测试）可能直接提供不同类型的弹性模量。

### 地球物理学中的各向异性

尽管各向同性模型非常有用，但地球内部的许多材料，如沉积岩、片岩或含有定向裂缝的岩石，其力学性质具有明显的方向依赖性。这种现象称为**各向异性** (anisotropy)。

对于一般的各向异性材料，刚度张量 $C_{ijkl}$ 的81个分量由于应力张量和应变张量的对称性以及应变能的存在（要求 $C_{ijkl}=C_{klij}$），可以减少到21个独立的弹性常数。为了方便表示，通常采用**Voigt表示法** (Voigt notation)，将四阶的刚度张量 $C_{ijkl}$ 和二阶的应力/应变张量分别映射为一个 $6 \times 6$ 的刚度矩阵 $\mathbf{C}$ 和 $6 \times 1$ 的应力/应变矢量 [@problem_id:3607929]。应力矢量和应变矢量的标准形式为：
$$
\boldsymbol{\sigma} = [\sigma_{11}, \sigma_{22}, \sigma_{33}, \sigma_{23}, \sigma_{13}, \sigma_{12}]^{\mathsf{T}}
$$
$$
\boldsymbol{\varepsilon} = [\varepsilon_{11}, \varepsilon_{22}, \varepsilon_{33}, 2\varepsilon_{23}, 2\varepsilon_{13}, 2\varepsilon_{12}]^{\mathsf{T}}
$$
注意，为了保持功共轭关系，应变矢量中的剪切分量是张量分量的两倍（工程剪应变）。此时，胡克定律写为简洁的矩阵形式 $\boldsymbol{\sigma} = \mathbf{C}\boldsymbol{\varepsilon}$。

根据材料对称性的不同，独立弹性常数的数量可以进一步减少：

- **正交各向异性 (Orthotropic Anisotropy)**：材料具有三个相互正交的对称面。这将其独立常数减少到9个。其刚度矩阵具有块对角形式，耦合了正向应力与正向应变，以及剪应力与剪应变。

- **横向各向异性 (Transverse Isotropy)**：材料具有一个对称轴，在垂直于该轴的平面内是各向同性的。这在地球科学中非常常见，例如，水平沉积的页岩层理导致了绕垂直轴旋转不变的性质，称为**垂直横向各向异性 (VTI)**。VTI材料的独立弹性常数减少到5个 [@problem_id:3607925]。其Voigt刚度矩阵形式为：
$$
\mathbf{C}_{\mathrm{VTI}} = \begin{pmatrix} C_{11} & C_{11} - 2 C_{66} & C_{13} & 0 & 0 & 0 \\ C_{11} - 2 C_{66} & C_{11} & C_{13} & 0 & 0 & 0 \\ C_{13} & C_{13} & C_{33} & 0 & 0 & 0 \\ 0 & 0 & 0 & C_{44} & 0 & 0 \\ 0 & 0 & 0 & 0 & C_{44} & 0 \\ 0 & 0 & 0 & 0 & 0 & C_{66} \end{pmatrix}
$$

各向异性导致了许多与直觉不符的现象。例如，对于正交各向异性材料，沿不同主轴的杨氏模量是不同的 ($E_1 \neq E_2 \neq E_3$)。此外，泊松比也变得复杂。在主轴 $i$ 方向施加单轴应力，在主轴 $j$ 方向测得的泊松比为 $\nu_{ij}$。一般情况下，$\nu_{ij} \neq \nu_{ji}$。然而，由于柔度矩阵 $\mathbf{S} = \mathbf{C}^{-1}$ 必须是对称的，即 $S_{ij} = S_{ji}$，这导致了一个重要的互易关系：$\nu_{ij}/E_i = \nu_{ji}/E_j$ [@problem_id:3607927]。这表明，虽然泊松比本身不对称，但经过相应方向杨氏模量的归一化后，则恢复了对称性。

### 弹性系统的基本原理

除了本构关系，还有一些普适性原理论述了弹性系统的整体行为。

#### 应变协调性

我们从位移场出发定义了应变场。但反过来，如果我们从实验（如大地测量或应变仪）中获得一个应变场 $\boldsymbol{\varepsilon}(\mathbf{x})$，我们如何确定它是否对应一个真实的、物理上可能的连续位移场 $\mathbf{u}(\mathbf{x})$？

这个问题的答案在于**应变协调性条件** (strain compatibility conditions)，也称为**圣维南协调方程** (Saint-Venant compatibility equations)。这些条件本质上是确保从应变场积分到位移场时，结果是单值且连续的。其推导基于一个基本事实：如果位移场 $\mathbf{u}$ 足够光滑，其二阶偏导数的求导次序可以交换，例如 $u_{i,jk} = u_{i,kj}$。通过对应变定义式进行微分和组合，可以消去位移场 $\mathbf{u}$，得到一个只包含应变分量及其二阶导数的方程组 [@problem_id:3607881]：
$$
\varepsilon_{ij,kl} + \varepsilon_{kl,ij} - \varepsilon_{ik,jl} - \varepsilon_{jl,ik} = 0
$$
这里逗号表示对坐标的偏微分。这个四阶张量方程包含了81个标量方程，但由于各种对称性，最终只有6个是独立的。在二维平面应变问题中，它们简化为一个著名的方程：
$$
\frac{\partial^{2} \varepsilon_{xx}}{\partial y^{2}} + \frac{\partial^{2} \varepsilon_{yy}}{\partial x^{2}} = 2 \frac{\partial^{2} \varepsilon_{xy}}{\partial x \partial y}
$$
对于一个**单连通区域**（即区域内任何闭合回路都可以连续收缩为一个点），满足协调方程是存在一个单值位移场（在刚体运动的意义上是唯一的）的充分必要条件。如果区域不是单连通的（例如，包含一个孔洞），即使协调方程满足，积分结果也可能依赖于路径，这对应于位错等晶体缺陷的存在。

#### 互易定理

**贝蒂互易定理** (Betti's reciprocity theorem) 是线性弹性静力学中一个优美而深刻的原理。它关联了同一个弹性体在两组不同载荷下的响应。

考虑一个弹性体，在其上施加第一组载荷，包括体力 $\mathbf{b}^{(1)}$ 和面力 $\mathbf{t}^{(1)}$，由此产生的位移场为 $\mathbf{u}^{(1)}$。然后，移除第一组载荷，施加第二组载荷 $\mathbf{b}^{(2)}$ 和 $\mathbf{t}^{(2)}$，产生的位移场为 $\mathbf{u}^{(2)}$。贝蒂定理指出：第一组载荷在第二组位移场上所做的功，等于第二组载荷在第一组位移场上所做的功。数学上表示为 [@problem_id:3607915]：
$$
\int_{\Omega} \mathbf{b}^{(1)} \cdot \mathbf{u}^{(2)} dV + \int_{\partial\Omega} \mathbf{t}^{(1)} \cdot \mathbf{u}^{(2)} dS = \int_{\Omega} \mathbf{b}^{(2)} \cdot \mathbf{u}^{(1)} dV + \int_{\partial\Omega} \mathbf{t}^{(2)} \cdot \mathbf{u}^{(1)} dS
$$
该定理的成立依赖于弹性刚度张量的对称性 ($C_{ijkl}=C_{klij}$)。这个看似抽象的定理在工程和地球物理中有重要应用，例如，它是边界元法的基础，并可用于推导格林函数。我们可以通过一个简单的例子来验证它：一根一端固定的杆，在两种不同加载情况（均布体力 vs. 端点集中力）下，通过分别求解位移场并计算互易功积分，可以精确地验证两侧的相等性 [@problem_id:3607915]。

### 超越线性弹性：与粘弹性的联系

地球材料在短时间尺度（如地震波传播）下表现出弹性，但在长时间尺度（如地幔对流、冰川后回弹）下则表现出粘性流动。连接这两种行为的是**粘弹性** (viscoelasticity) 理论。

最简单的粘弹性模型之一是**麦克斯韦模型** (Maxwell model)，它由一个理想弹簧（代表弹性）和一个粘性阻尼器（代表粘性）串联而成。弹簧的本构关系是 $\sigma = E\varepsilon_e$，阻尼器是 $\sigma = \eta\dot{\varepsilon}_v$，其中 $E$ 是杨氏模量，$\eta$ 是粘度。由于是串联，总应变是两者之和 $\varepsilon = \varepsilon_e + \varepsilon_v$，而应力在两者中相等。对总应变求时间导数，我们得到麦克斯韦模型的本构方程：
$$
\dot{\varepsilon}(t) = \frac{\dot{\sigma}(t)}{E} + \frac{\sigma(t)}{\eta}
$$
这个模型为我们理解弹性响应的本质提供了一个有趣的视角。考虑一个在 $t=0$ 时刻突然施加并保持恒定的应力 $\sigma_0$。这意味着应力历史是一个阶跃函数 $\sigma(t) = \sigma_0 H(t)$，其导数 $\dot{\sigma}(t)$ 是一个在 $t=0$ 处的狄拉克 $\delta$ 函数。

分析材料在加载瞬间 ($t \to 0^+$) 的响应，我们可以通过对本构方程在一个包含 $t=0$ 的无穷小时间区间上积分来得到 [@problem_id:3607936]。积分结果表明，在加载的瞬间，应变跃变为 $\varepsilon(0^+) = \sigma_0/E$。这与一个纯弹性材料的响应完全相同。这个结果的物理解释是：在瞬时加载下，粘性阻尼器来不及发生形变（需要有限时间流动），因此所有变形都由弹性弹簧承担。这表明，线性弹性响应可以被看作是更普适的粘弹性响应在时间尺度趋于零时的极限。这个概念对于将在不同时间尺度上观测到的地球物理现象（如地震波速和长期形变）联系起来至关重要。