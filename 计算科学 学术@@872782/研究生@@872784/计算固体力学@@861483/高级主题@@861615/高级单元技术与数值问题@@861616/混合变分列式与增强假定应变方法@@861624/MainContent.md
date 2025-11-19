## 引言
在[计算固体力学](@entry_id:169583)领域，[有限元法](@entry_id:749389)（FEM）是不可或缺的分析工具，但标准的位移法在处理特定约束问题时会面临严峻挑战。当模拟薄壁结构或[近不可压缩材料](@entry_id:752388)时，常会遇到被称为“数值闭锁”的现象，导致计算结果过刚且严重失真。为了克服这一根本性缺陷，学术界发展出了以[混合变分格式](@entry_id:752029)和增强假设应变（EAS）方法为代表的一系列高级技术。这些方法通过从根本上修改[变分原理](@entry_id:198028)，引入额外的场变量或局部增强应变，从而恢复了数值解的准确性和鲁棒性。本文旨在系统性地剖析这些方法的理论精髓与应用实践。在接下来的内容中，读者将首先在“原理与机制”一章深入学习数值闭锁的根源、混合变分法的数学框架及其[稳定性理论](@entry_id:149957)，以及[EAS方法](@entry_id:748781)的设计思想。随后，“应用与跨学科[交叉](@entry_id:147634)”一章将展示这些技术在[材料塑性](@entry_id:186852)、[结构稳定性](@entry_id:147935)、多物理场耦合等前沿问题中的强大威力。最后，“动手实践”部分将提供一系列精心设计的练习，帮助读者将理论知识转化为解决实际问题的能力。

## 原理与机制

在上一章引言的基础上，本章旨在深入探讨[混合变分格式](@entry_id:752029)与增强假设应变方法的核心科学原理与作用机制。这些高级有限元技术被开发出来的首要动机，是为了克服标准位移[有限元法](@entry_id:749389)在处理特定物理问题时遇到的严[重数](@entry_id:136466)值困难，即“数值闭锁”（numerical locking）。我们将首先剖析数值闭锁的两种主要形式，然后建立用于解决这些问题的混合变分法的数学框架，并阐述其[稳定性理论](@entry_id:149957)。最后，我们将详细介绍增强假设应变（EAS）方法的设计思想、实现细节以及在实际应用中的若干高级议题。

### 数值闭锁现象

数值闭锁是指在某些极限情况下（如结构厚度趋于零或材料近乎不可压缩时），低阶有限元单元会表现出与其物理行为不符的、过于刚硬的响应。这种非物理性的刚度源于有限元[离散空间](@entry_id:155685)无法精确满足该极限情况下的运动学约束。

#### 剪切闭锁

**剪切闭锁**（Shear locking）主要出现在使用独立插值转角和位移的梁、板、[壳单元](@entry_id:176094)中，例如基于[Timoshenko梁理论](@entry_id:169054)或[Mindlin-Reissner板理论](@entry_id:751988)的单元。为了理解其机理，我们考虑一个薄板单元 [@problem_id:3582047]。板的总应变能由[弯曲能](@entry_id:174691)和横向剪切能两部分构成。对于厚度为 $t$ 的板，其弯曲能与 $t^3$ 成正比，而剪切能与 $t$ 成正比。当板非常薄（$t \to 0$）时，物理上其变形应以弯曲为主，横向剪切应变几乎为零，因此剪切能的贡献相对于弯曲能可以忽略不计。

然而，对于一个低阶单元（如四节点双线性单元），其位移和转角场采用低阶[多项式插值](@entry_id:145762)。在[纯弯曲](@entry_id:202969)状态下，精确的运动学关系（Kirchhoff约束），例如 $\gamma_{xz} = \beta_x - \frac{\partial w}{\partial x} = 0$，要求转角 $\beta_x$ 等于横向位移 $w$ 的导数。对于[双线性插值](@entry_id:170280)而言，$\beta_x$ 是线性的，而 $\frac{\partial w}{\partial x}$ 也是线性的，但这两个线性场通常无法在整个单元上精确匹配以满足零剪切约束，除非在非常特定的网格和变形模式下。这种**[运动学](@entry_id:173318)不协调**（kinematic incompatibility）导致单元即使在[纯弯曲](@entry_id:202969)载荷下也会产生虚假的、非零的寄生剪切应变（parasitic shear strains）。

由于剪切能与 $t$ 成正比，而[弯曲能](@entry_id:174691)与 $t^3$ 成正比，当 $t \to 0$ 时，即使很小的寄生剪切应变也会产生远大于弯曲能的能量惩罚。为了最小化总能量，有限元解将极力抑制弯曲变形，以避免产生巨大的剪切能，从而表现出远超实际的刚度。这就是剪切闭锁的本质：[离散空间](@entry_id:155685)无法在满足边界条件的同时正确表示零剪切的弯曲状态，导致能量惩罚项被错误地激活。

#### 体积闭锁

**体积闭锁**（Volumetric locking）发生在模拟[近不可压缩材料](@entry_id:752388)时，例如当泊松比 $\nu \to 0.5$ 或体积模量 $\kappa \to \infty$ 的情况 [@problem_id:3582047]。物理上，不可压缩性意味着材料在变形过程中[体积保持](@entry_id:141001)不变，即[体积应变](@entry_id:267252) $\operatorname{tr}(\boldsymbol{\varepsilon}) = \nabla \cdot \boldsymbol{u}$ 必须为零。

在标准的位移有限元法中，这一约束通常通过罚函数法来近似施加。材料的[应变能密度](@entry_id:200085)可以分解为偏量部分和体积部分，后者形如 $\frac{\kappa}{2} (\operatorname{tr}(\boldsymbol{\varepsilon}))^2$。当 $\kappa$ 是一个非常大的数时，这一项成为一个巨大的能量惩罚项，迫使离散解的体积应变 $\operatorname{tr}(\boldsymbol{\varepsilon}_h) = \nabla \cdot \boldsymbol{u}_h$ 趋近于零。

问题在于，对于低阶单元（如[Q4单元](@entry_id:176936)），由位移[插值函数](@entry_id:262791)决定的离散散度空间 $\nabla \cdot \boldsymbol{u}_h$ 非常有限。例如，对于一个双线性[Q4单元](@entry_id:176936)，其位移分量的导数是线性的，因此散度 $\nabla \cdot \boldsymbol{u}_h$ 也是一个线性函数。在一个由多个此类单元构成的网格中，要逐点满足 $\nabla \cdot \boldsymbol{u}_h = 0$ 会对节点位移施加过多的约束。通常，离散空间中唯一能满足此条件的平凡解是零位移。为了避免巨大的体积能惩罚，单元会抵抗几乎所有形式的变形，从而表现出虚假的、极高的刚度。经典的Cook膜问题就是一个展示体积闭锁的典型算例，其中使用标准[Q4单元](@entry_id:176936)在[近不可压缩](@entry_id:752387)情况下会得到严重偏小（过于刚硬）的位移解 [@problem_id:3582105]。

### 混合[变分法](@entry_id:163656)的数学框架

为了克服数值闭锁，混合[变分法](@entry_id:163656)引入了除位移之外的独立变量场（如应力、应变或压力），从而放宽了由[位移场](@entry_id:141476)插值带来的过强约束。

#### 从强形式到[鞍点问题](@entry_id:174221)

我们以[近不可压缩](@entry_id:752387)弹性问题为例，阐述如何构建一个[混合变分格式](@entry_id:752029)。其强形式包括[平衡方程](@entry_id:172166)、本构关系和运动学约束 [@problem_id:3582041]：
$$
\begin{cases}
-\nabla \cdot \boldsymbol{\sigma} = \boldsymbol{f}  \text{ in } \Omega \\
\boldsymbol{\sigma} = 2\mu\boldsymbol{\varepsilon}'(\boldsymbol{u}) - p\boldsymbol{I} \\
\nabla \cdot \boldsymbol{u} = 0
\end{cases}
$$
这里，$\boldsymbol{\sigma}$ 是柯西应力，$\boldsymbol{u}$ 是位移，$\boldsymbol{f}$ 是[体力](@entry_id:174230)。我们将静水压力 $p$ 视为一个独立的未知场，一个拉格朗日乘子，其作用就是强制执行不可压缩约束 $\nabla \cdot \boldsymbol{u} = 0$。

为了得到弱形式，我们将[平衡方程](@entry_id:172166)乘以一个[虚位移](@entry_id:168781)（检验函数）$\boldsymbol{w}$ 并在域 $\Omega$ 上积分。通过[分部积分](@entry_id:136350)（[散度定理](@entry_id:143110)），并将应力本构代入，可以得到[动量方程](@entry_id:197225)的弱形式。同时，我们将不可压缩约束乘以一个虚压力（检验函数）$q$ 并在域上积分。这样，我们得到一个寻找 $(\boldsymbol{u},p)$ 对的混合[变分问题](@entry_id:756445)，它具有典型的**[鞍点问题](@entry_id:174221)**（saddle-point problem）结构：

寻找 $(\boldsymbol{u}, p) \in V \times Q$，使得对于所有检验函数 $(\boldsymbol{w}, q) \in V \times Q$ 均满足：
$$
\begin{cases}
a(\boldsymbol{u}, \boldsymbol{w}) + b(\boldsymbol{w}, p) = \ell(\boldsymbol{w}) \\
b(\boldsymbol{u}, q) = 0
\end{cases}
$$
对于上述不可压缩弹性问题，具体的双线性形式 $a(\cdot, \cdot)$、$b(\cdot, \cdot)$ 和[线性泛函](@entry_id:276136) $\ell(\cdot)$ 为 [@problem_id:3582041]：
$$
a(\boldsymbol{u}, \boldsymbol{w}) := \int_{\Omega} 2\mu\boldsymbol{\varepsilon}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\boldsymbol{w}) \, \mathrm{d}\Omega
$$
$$
b(\boldsymbol{w}, p) := -\int_{\Omega} p (\nabla \cdot \boldsymbol{w}) \, \mathrm{d}\Omega
$$
$$
\ell(\boldsymbol{w}) := \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{w} \, \mathrm{d}\Omega + \int_{\Gamma_N} \boldsymbol{t} \cdot \boldsymbol{w} \, \mathrm{d}s
$$
其中 $V$ 是满足狄利克雷边界条件的位移[函数空间](@entry_id:143478)（如 $[H^1(\Omega)]^d$ 的一个[子空间](@entry_id:150286)），而 $Q$ 是压力[函数空间](@entry_id:143478)（如 $L^2(\Omega)$）。第一个方程代表[虚功原理](@entry_id:138749)，而第二个方程以[弱形式](@entry_id:142897)强制施加了不可压缩约束。

#### 算子形式与物理意义

这个[鞍点问题](@entry_id:174221)在离散后会导出一个具有特定块结构的线性方程组：
$$
\begin{pmatrix} A  B^\top \\ B  0 \end{pmatrix}
\begin{pmatrix} \mathbf{u} \\ \mathbf{p} \end{pmatrix}
=
\begin{pmatrix} \mathbf{f} \\ \mathbf{0} \end{pmatrix}
$$
这里，矩阵 $A$ 对应于[双线性形式](@entry_id:746794) $a(\cdot, \cdot)$，通常是（半）正定的，代表了系统的刚度。矩阵 $B$ 对应于[双线性形式](@entry_id:746794) $b(\cdot, \cdot)$，它将[位移场](@entry_id:141476)与压[力场](@entry_id:147325)耦合起来，代表了约束。具体来说，算子 $B$ 在[分布](@entry_id:182848)意义下对应于负[散度算子](@entry_id:265975) $(-\nabla \cdot)$，而其[转置](@entry_id:142115) $B^\top$ 对应于[梯度算子](@entry_id:275922) $(\nabla)$ [@problem_id:3582041]。$\boldsymbol{u}$ 的物理意义是位移场，而 $p$ 是作为[拉格朗日乘子](@entry_id:142696)引入的静水压力。

通过引入独立的压[力场](@entry_id:147325) $p$，体积响应（由 $p$ 控制）和[偏应力](@entry_id:163323)响应（由 $a(\cdot, \cdot)$ 中的项控制）被[解耦](@entry_id:637294)。这避免了在位移法中因 $\kappa \to \infty$ 而导致的病态问题。只要选择的离散位移空间 $V_h$ 和压力空间 $Q_h$ 是“兼容”的，这种方法就能有效消除体积闭锁 [@problem_id:3582105]。

### [适定性](@entry_id:148590)与[稳定性理论](@entry_id:149957)

混合[变分问题](@entry_id:756445)的[适定性](@entry_id:148590)（解的存在性、唯一性和稳定性）并非自然而然得到保证，它依赖于[双线性形式](@entry_id:746794) $a(\cdot, \cdot)$ 和 $b(\cdot, \cdot)$ 满足的一系列关键条件，即著名的Babuška-Brezzi (BB) 理论，或称为[LBB条件](@entry_id:746626)。

#### 连续问题的[Babuška-Brezzi条件](@entry_id:746625)

对于一个抽象的[鞍点问题](@entry_id:174221)，其[适定性](@entry_id:148590)由两个核心条件保证 [@problem_id:3582069]：

1.  **$a(\cdot, \cdot)$ 在 $b(\cdot, \cdot)$ 核空间上的强制性 (Coercivity on the kernel)**：
    存在常数 $\alpha > 0$，使得对于所有满足 $b(\boldsymbol{v},q) = 0, \forall q \in Q$ 的 $\boldsymbol{v} \in V$（即 $\boldsymbol{v} \in \ker B$），都有：
    $$
    a(\boldsymbol{v},\boldsymbol{v}) \ge \alpha \|\boldsymbol{v}\|_{V}^{2}
    $$
    这个条件确保了在满足约束的[子空间](@entry_id:150286)内，问题是良定的。它控制了对约束“不可见”的解的分量。

2.  **$b(\cdot, \cdot)$ 的[inf-sup条件](@entry_id:746626) (The inf-sup condition)**：
    存在常数 $\beta > 0$，使得：
    $$
    \inf_{q \in Q \setminus \{0\}} \sup_{\boldsymbol{v} \in V \setminus \{0\}} \frac{b(\boldsymbol{v},q)}{\|\boldsymbol{v}\|_{V} \|q\|_{Q}} \ge \beta
    $$
    这个条件，也称为Ladyzhenskaya–Babuška–Brezzi (LBB) 条件，是[混合方法](@entry_id:163463)理论的基石。它保证了约束算子 $B$ 的稳定性和值域的闭合性，从而确保了拉格朗日乘子场（如压力 $p$）的解是唯一且稳定的。直观上，它要求对于任何一个[检验函数](@entry_id:166589) $q$，总能找到一个检验函数 $\boldsymbol{v}$，使得 $b(\boldsymbol{v},q)$ 不会“太小”，从而在方程中对 $q$ 施加有效控制。

这两个条件与[双线性形式](@entry_id:746794)的有界性一起，是[混合问题](@entry_id:634383)[适定性](@entry_id:148590)的充分必要条件。

#### 离散[inf-sup条件](@entry_id:746626)及其重要性

当我们将问题离散化，选择有限维[子空间](@entry_id:150286) $V_h \subset V$ 和 $Q_h \subset Q$ 时，这两个条件必须在离散层面上得到满足，并且常数需要与网格尺寸 $h$ 无关 [@problem_id:3582040]。特别是离散[inf-sup条件](@entry_id:746626)，要求存在一个与 $h$ 无关的常数 $\beta_0 > 0$，使得：
$$
\inf_{q_h \in Q_h \setminus \{0\}} \sup_{\boldsymbol{v}_h \in V_h \setminus \{0\}} \frac{b(\boldsymbol{v}_h, q_h)}{\|\boldsymbol{v}_h\|_{V} \|q_h\|_{Q}} \ge \beta_0
$$
这个**均匀稳定性**条件至关重要。如果选择的[离散空间](@entry_id:155685)对 $(V_h, Q_h)$ 使得离散inf-sup常数 $\beta_h \to 0$ 随着[网格加密](@entry_id:168565) ($h \to 0$)，将会导致一系列严重的数值问题：

*   **伪压力[振荡](@entry_id:267781)**：压力解可能会出现非物理的、棋盘格状的[振荡](@entry_id:267781)模式，并且这种[振荡](@entry_id:267781)不会随着[网格加密](@entry_id:168565)而消失，压[力场](@entry_id:147325)的误差甚至可能停滞不前 [@problem_id:3582040]。
*   **收敛性丧失**：误差估计常数通常与 $\beta_h^{-1}$ 或 $\beta_h^{-2}$ 成正比，因此 $\beta_h \to 0$ 意味着无法保证最优的收敛阶。
*   **系统矩阵病态**：[鞍点系统](@entry_id:754480)[矩阵的条件数](@entry_id:150947)，特别是其舒尔补的[条件数](@entry_id:145150)，会随着 $\beta_h^{-2}$ 的速度增长，这给迭代求解器的性能和[预处理器](@entry_id:753679)的设计带来了巨大挑战 [@problem_id:3582040]。

因此，[混合有限元](@entry_id:178533)的设计核心就在于构造满足离散[LBB条件](@entry_id:746626)的[插值函数](@entry_id:262791)空间对 $(V_h, Q_h)$。例如，经典的[Taylor-Hood单元](@entry_id:165658)（位移用二次插值，压力用线性插值）就是一种稳定的单元。

### 增强假设应变 (EAS) 方法

增强假设应变（Enhanced Assumed Strain, EAS）方法提供了一种在标准位移单元框架内绕过[LBB条件](@entry_id:746626)的巧妙途径，它通过在单元内部局部增强应变场来消除闭锁。

#### 核心思想：应变场的局部增强

[EAS方法](@entry_id:748781)基于多场[变分原理](@entry_id:198028)，如Hu-Washizu三场[变分原理](@entry_id:198028)。其核心思想是将单元的总应变 $\boldsymbol{\varepsilon}$ 分解为一个与[位移场](@entry_id:141476)**协调**（compatible）的部分 $\boldsymbol{\varepsilon}^c$ 和一个**增强**（enhanced）的部分 $\boldsymbol{\varepsilon}^*$ [@problem_id:3582076]：
$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^c(\boldsymbol{u}) + \boldsymbol{\varepsilon}^*(\boldsymbol{\alpha})
$$
其中，$\boldsymbol{\varepsilon}^c = \mathbf{B}\boldsymbol{u}$ 是通过标准位移插值得到的应变场，而 $\boldsymbol{\varepsilon}^* = \mathbf{G}\boldsymbol{\alpha}$ 是通过一组独立的、仅在单元内部有效的**增强模式** $\mathbf{G}$ 和内部参数 $\boldsymbol{\alpha}$ 来定义的。

这些内部参数 $\boldsymbol{\alpha}$ 不与相邻单元共享，可以通过**[静态凝聚](@entry_id:176722)**（static condensation）在单元层面被消去。这意味着最终的[单元刚度矩阵](@entry_id:139369)仍然只涉及节点位移自由度，可以无缝地集成到标准的有限元程序集中。从效果上看，EAS可以被理解为一种在单元内部执行的、满足局部[inf-sup条件](@entry_id:746626)的混合方法，从而在不改变全局位移插值的情况下恢复了稳定性 [@problem_id:3582040]。

#### EAS模式的设计准则

成功的EAS单元设计依赖于对增强应变模式 $\boldsymbol{\varepsilon}^*$ 的精心选择，必须满足以下关键准则：

1.  **正交性与补空间思想**：增强模式必须与协调应变空间线性无关，以提供真正“缺失”的变形模式。例如，为了克服[Q4单元](@entry_id:176936)的体积闭锁，需要引入协调应变空间（线性函数）中所没有的更高阶的[体积应变](@entry_id:267252)模式 [@problem_id:3582076]。

2.  **通过[分片检验](@entry_id:162864) (Patch Test)**：这是保证收敛性的基本一致性要求。一个单元，无论其形状如何，当置于一个常应变场中时，必须能够精确地重现这个常应变状态。在EAS的框架下，这意味着当施加一个常应力/应变状态时，增强参数 $\boldsymbol{\alpha}$ 必须为零。这导出了一个关键的[正交性条件](@entry_id:168905)：增强应变场在单元上的积分必须为零 [@problem_id:3582076] [@problem_id:3582057]。
    $$
    \int_{\Omega_e} \boldsymbol{\varepsilon}^* d\Omega = \mathbf{0}
    $$
    对于任意形状的等参元，其体积微元 $d\Omega = \det(\mathbf{J}) d\xi d\eta$，其中[雅可比行列式](@entry_id:137120) $\det(\mathbf{J})$ 是坐标 $(\xi, \eta)$ 的函数。因此，更严格的条件是：
    $$
    \int_{-1}^{1}\int_{-1}^{1} \mathbf{G}(\xi, \eta) \det(\mathbf{J}(\xi, \eta)) d\xi d\eta = \mathbf{0}
    $$
    对于一般[四边形单元](@entry_id:176937)，$\det(\mathbf{J})$ 是 $(\xi, \eta)$ 的线性函数。因此，简单地选择在父单元上均值为零的模式（如 $\xi$ 或 $\eta$）是不够的，因为它们与 $\det(\mathbf{J})$ 的线性项相乘后积分不为零 [@problem_id:3582093]。

#### 基于[气泡函数](@entry_id:176111)的EAS构造

满足任意几何形状下[分片检验](@entry_id:162864)的一个稳健方法是，从**气泡位移函数**（bubble displacement functions）中导出增强应变场 [@problem_id:3582093]。[气泡函数](@entry_id:176111)是在单元边界上为零，仅在单元内部非零的位移模式。如果我们将增强应变场定义为这些气泡位移场的对称梯度：
$$
\boldsymbol{\varepsilon}^* = \operatorname{sym}(\nabla \boldsymbol{w}^*)
$$
其中 $\boldsymbol{w}^*|_{\partial \Omega_e} = \mathbf{0}$。根据[散度定理](@entry_id:143110)，其在单元上的积分为：
$$
\int_{\Omega_e} \boldsymbol{\varepsilon}^* d\Omega = \int_{\Omega_e} \operatorname{sym}(\nabla \boldsymbol{w}^*) d\Omega = \operatorname{sym}\left( \int_{\partial\Omega_e} \boldsymbol{w}^* \otimes \boldsymbol{n} \, dS \right) = \mathbf{0}
$$
由于 $\boldsymbol{w}^*$ 在边界上为零，这个积分恒为零，从而自动满足了任意几何形状下的[分片检验](@entry_id:162864)。著名的Simo-Rifai五参数EAS单元就是基于此原理构造的，它能有效地同时解决剪切和体积闭锁问题 [@problem_id:3582093]。

### 实现中的关键问题与高等议题

#### [伪零能模式](@entry_id:755267)的产生与识别

虽然[EAS方法](@entry_id:748781)功能强大，但如果增强模式选择不当，可能会引入**[伪零能模式](@entry_id:755267)**（spurious zero-energy modes），也称为[沙漏模式](@entry_id:174855)（hourglass modes）。这是一种非[刚体运动](@entry_id:193355)的变形模式，但其产生的[应变能](@entry_id:162699)为零，导致[单元刚度矩阵](@entry_id:139369)是奇异的（或[秩亏](@entry_id:754065)的）。

一个有限元单元的刚度矩阵 $\mathbf{K}$ 的秩应该等于其自由度数减去刚体运动模式数。对于一个三维实体单元，有6个刚体运动模式。对于Mindlin-Reissner板单元，有3个刚体运动模式（一个平移，两个转动）[@problem_id:3582075]。如果刚度[矩阵的零空间](@entry_id:152429)维数（$n_0 = \text{DOF} - \mathrm{rank}(\mathbf{K})$）大于[刚体运动](@entry_id:193355)模式数 $R$，那么多出来的 $n_0 - R$ 个[零能模式](@entry_id:172472)就是[伪模式](@entry_id:163321)。

例如，在一个Mindlin-Reissner板单元中，如果通过EAS增强完全消除了剪切应变能的贡献，那么最终的刚度矩阵将只剩下[弯曲刚度](@entry_id:180453) $\mathbf{K}_{bb}$。由于纯粹的横向位移 $w$ 的变形（非刚体运动）不产生[弯曲能](@entry_id:174691)，这将导致多个与 $w$ 相关的[伪零能模式](@entry_id:755267)，使得单元不稳定 [@problem_id:3582075]。因此，EAS模式的设计必须在“足够丰富以消除闭锁”和“不过于丰富以至引入[伪模式](@entry_id:163321)”之间取得精妙的平衡。

#### [非线性](@entry_id:637147)分析中的[一致切线刚度](@entry_id:166500)

在[非线性](@entry_id:637147)问题中，求解过程通常采用[Newton-Raphson](@entry_id:177436)[迭代法](@entry_id:194857)，其[收敛速度](@entry_id:636873)依赖于[切线刚度矩阵](@entry_id:170852)的质量。对于EAS单元，由于内部参数 $\boldsymbol{\alpha}$ 通过[静态凝聚](@entry_id:176722)与节点位移 $\boldsymbol{u}$ 关联起来，即 $\boldsymbol{\alpha} = \boldsymbol{\alpha}(\boldsymbol{u})$，在计算总的[切线刚度矩阵](@entry_id:170852) $\mathbf{K}_T = \frac{\partial \mathbf{R}_c(\boldsymbol{u})}{\partial \boldsymbol{u}}$ 时，必须考虑这种依赖性 [@problem_id:3582094]。

完整的、考虑了所有依赖关系的[切线刚度矩阵](@entry_id:170852)称为**[一致切线刚度](@entry_id:166500)**（consistent tangent stiffness）。如果忽略了 $\boldsymbol{\alpha}$ 对 $\boldsymbol{u}$ 的依赖性（即在求导时将 $\boldsymbol{\alpha}$ 视为常数），得到的将是一个不一致的[切线](@entry_id:268870)矩阵。使用[一致切线刚度](@entry_id:166500)可以保证[Newton-Raphson法](@entry_id:140620)在解的邻域内具有二次收敛性，而使用不一致的[切线刚度](@entry_id:166213)通常会将收敛速度降低到线性，甚至导致不收敛 [@problem_id:3582094]。因此，在[非线性](@entry_id:637147)EAS单元的实现中，正确推导和实现[一致切线刚度](@entry_id:166500)对于计算效率和稳健性至关重要。