## 引言
橡胶、凝胶和许多生物组织等软材料在工程和自然界中无处不在，它们的共同特点是能够承受巨大的、可恢复的变形。传统的线性弹性理论在这种大变形、高度[非线性](@entry_id:637147)的场景下完全失效，这促使我们必须发展更先进的力学框架。超弹性理论应运而生，它通过一个标量的[应变能函数](@entry_id:178435)来描述材料的全部力学响应。在众多超弹性模型中，新胡克（Neo-Hookean）模型和穆尼-里夫林（Mooney-Rivlin）模型因其简洁性与实用性的完美结合，成为了[非线性固体力学](@entry_id:171757)领域的基石。

本文旨在为读者提供一个关于新胡克与[穆尼-里夫林模型](@entry_id:177592)的全面而深入的理解。我们将不仅仅满足于公式的罗列，而是要揭示其背后的物理原理与数学结构。通过接下来的三个章节，您将系统地学习：

首先，在**“原理与机制”**一章中，我们将从有限变形的[运动学](@entry_id:173318)出发，建立描述大变形的数学语言，并基于[热力学原理](@entry_id:142232)和[材料对称性](@entry_id:190289)，严格推导出新胡克与[穆尼-里夫林模型](@entry_id:177592)的[本构方程](@entry_id:138559)。我们还将探讨[不可压缩性约束](@entry_id:750592)的深刻含义，并审视这些[唯象模型](@entry_id:273816)的适用边界。

接着，在**“应用与跨学科联系”**一章中，我们将把理论付诸实践。通过分析[材料参数辨识](@entry_id:751733)、薄膜/厚壁[结构分析](@entry_id:153861)、[生物力学](@entry_id:153973)建模以及与[高分子](@entry_id:150543)物理的联系等具体案例，您将看到这些模型如何成为解决真实世界问题的强大工具。同时，我们也会探讨在有限元分析中实现这些模型所面临的数值挑战，如“[体积锁定](@entry_id:172606)”及其解决方案。

最后，**“动手实践”**部分将提供一系列精心设计的练习题，引导您亲手进行[运动学](@entry_id:173318)计算和[应力分析](@entry_id:168804)。通过这些实践，您将能够巩固所学知识，将抽象的理论转化为具体的分析能力。

## 原理与机制

本章深入探讨了[超弹性材料](@entry_id:190241)（尤其是类橡胶材料）[本构模型](@entry_id:174726)的理论基础。我们首先建立描述[大变形](@entry_id:167243)的运动学框架，然后引入指导本构关系建立的基本物理原理。在此基础上，我们将推导新胡克（Neo-Hookean）和 Mooney-Rivlin 这两种经典[唯象模型](@entry_id:273816)的具体形式，并探讨它们在不可压缩和可压缩情况下的应用。最后，我们将审视这些模型的局限性，并讨论捕捉更复杂材料行为（如应变硬化、滞后和 Mullins 效应）所需的理论扩展。

### 有限变形的运动学基础

为了精确描述材料从初始参考构型到当前构型的变形，我们必须采用[有限应变理论](@entry_id:176941)的语言。考虑一个物[质点](@entry_id:186768)，其在参考构型中的位置由向量 $\mathbf{X}$ 描述，在变形后，其在当前构型中的位置为 $\mathbf{x}$。变形的局部特性由**变形梯度张量**（**deformation gradient tensor**）$\mathbf{F}$ 完全捕捉，其定义为：
$$
\mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}}
$$
$\mathbf{F}$ 衡量了物质点邻域内的局部拉伸和旋转。它的[行列式](@entry_id:142978) $J = \det \mathbf{F}$ 表示体积的变化率，即当前构型中的一个微元体积与参考构型中对应微元体积之比。因此，$J > 0$ 是物理上必须满足的条件。

变形梯度 $\mathbf{F}$ 本身包含刚体旋转信息，而材料的[应变能](@entry_id:162699)不应依赖于观察者的刚体运动。因此，我们需要构造纯粹衡量“变形”或“拉伸”的张量。最常用的两个是**右柯西-格林变形张量**（**right Cauchy–Green deformation tensor**）$\mathbf{C}$ 和**左柯西-格林变形张量**（**left Cauchy–Green deformation tensor**）$\mathbf{B}$：
$$
\mathbf{C} = \mathbf{F}^{T}\mathbf{F}
$$
$$
\mathbf{B} = \mathbf{F}\mathbf{F}^{T}
$$
$\mathbf{C}$ 定义在参考构型上，而 $\mathbf{B}$ 定义在当前构型上。两者都是对称正定张量，它们的[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)描述了变形的**主拉伸**（**principal stretches**）大小和方向。

为了更直观地理解变形，我们可以考虑一个纯三轴拉伸的例子，其主拉伸分别为 $\lambda_1, \lambda_2, \lambda_3$。在与主方向对齐的[坐标系](@entry_id:156346)中，变形梯度 $\mathbf{F}$ 是一个[对角矩阵](@entry_id:637782)：
$$
\mathbf{F} = \begin{pmatrix} \lambda_{1} & 0 & 0 \\ 0 & \lambda_{2} & 0 \\ 0 & 0 & \lambda_{3} \end{pmatrix}
$$
此时，[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 也为对角阵，其对角元是主拉伸的平方 [@problem_id:2664630]：
$$
\mathbf{C} = \mathbf{F}^{T}\mathbf{F} = \begin{pmatrix} \lambda_{1}^{2} & 0 & 0 \\ 0 & \lambda_{2}^{2} & 0 \\ 0 & 0 & \lambda_{3}^{2} \end{pmatrix}
$$
为了构建一个不依赖于[坐标系](@entry_id:156346)选择的[本构模型](@entry_id:174726)，我们通常使用张量**[不变量](@entry_id:148850)**（**invariants**）。对于[对称张量](@entry_id:148092) $\mathbf{C}$，其三个**[主不变量](@entry_id:193522)**（**principal invariants**）$I_1, I_2, I_3$ 定义如下：
$$
I_1 = \mathrm{tr}(\mathbf{C})
$$
$$
I_2 = \frac{1}{2} \left[ (\mathrm{tr}(\mathbf{C}))^2 - \mathrm{tr}(\mathbf{C}^2) \right]
$$
$$
I_3 = \det(\mathbf{C})
$$
这些[不变量](@entry_id:148850)是张量 $\mathbf{C}$ 特征多项式的系数，因此它们与[坐标系](@entry_id:156346)的选择无关。利用上述三轴拉伸的例子，我们可以将这些抽象的[不变量](@entry_id:148850)与物理上直观的主拉伸联系起来。它们是主拉伸平方 $\lambda_1^2, \lambda_2^2, \lambda_3^2$ 的初等[对称多项式](@entry_id:153581) [@problem_id:2664630]：
$$
I_1 = \lambda_{1}^{2} + \lambda_{2}^{2} + \lambda_{3}^{2}
$$
$$
I_2 = \lambda_{1}^{2}\lambda_{2}^{2} + \lambda_{2}^{2}\lambda_{3}^{2} + \lambda_{3}^{2}\lambda_{1}^{2}
$$
$$
I_3 = \lambda_{1}^{2}\lambda_{2}^{2}\lambda_{3}^{2}
$$
同时，我们注意到 $I_3 = (\lambda_1 \lambda_2 \lambda_3)^2 = (\det \mathbf{F})^2 = J^2$，这直接将第三[不变量](@entry_id:148850)与体积变化联系起来。

### [本构模型](@entry_id:174726)的基本原理

建立一个物理上合理的本构模型需要遵循一系列基本原理。对于[超弹性材料](@entry_id:190241)，最重要的两个原理是**标架无关性**（**frame-indifference**）和**[材料对称性](@entry_id:190289)**（**material symmetry**），例如各向同性。

**[标架无关性原理](@entry_id:200995)**（又称**[客观性原理](@entry_id:185412)**，**principle of material objectivity**）要求材料的本构响应（此处为[应变能](@entry_id:162699)）不依赖于观察者的刚体运动。这意味着，如果在当前构型上施加一个任意的刚体旋转 $\mathbf{R}$（$\mathbf{R}$ 为真正交张量），[应变能函数](@entry_id:178435) $W$ 的值不应改变，即 $W(\mathbf{R}\mathbf{F}) = W(\mathbf{F})$。通过极分解定理，任何可逆的变形梯度 $\mathbf{F}$ 都可以唯一地分解为一个[旋转张量](@entry_id:191990) $\mathbf{R}_p$ 和一个[对称正定](@entry_id:145886)的右[拉伸张量](@entry_id:193200) $\mathbf{U}$，即 $\mathbf{F} = \mathbf{R}_p \mathbf{U}$。利用标架无关性，我们可以选择 $\mathbf{R} = \mathbf{R}_p^T$，从而证明 $W$ 只能是 $\mathbf{U}$ 的函数：$W(\mathbf{F}) = W(\mathbf{U})$。由于 $\mathbf{C} = \mathbf{U}^2$ 且 $\mathbf{U}$ 是 $\mathbf{C}$ 的唯一正定平方根，这等价于说[应变能](@entry_id:162699)只能是[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 的函数，即存在一个函数 $\widehat{W}$ 使得 $W(\mathbf{F}) = \widehat{W}(\mathbf{C})$ [@problem_id:2664596]。这样，我们就从本构关系中剔除了刚体旋转的影响。

**[材料对称性](@entry_id:190289)原理**描述了材料内部的对称性。对于**各向同性**（**isotropic**）材料，其力学响应不随材料方向的改变而改变。这意味着，如果在参考构型上施加一个任意的旋转 $\mathbf{Q}$，[应变能函数](@entry_id:178435)的值也不应改变，即 $W(\mathbf{F}\mathbf{Q}) = W(\mathbf{F})$。将此条件与标架无关性的结果相结合，我们得到 $\widehat{W}(\mathbf{C}) = \widehat{W}(\mathbf{Q}^T\mathbf{C}\mathbf{Q})$。这个数学表达式正是一个**各向同性标量值张量函数**的定义。根据[张量表示](@entry_id:180492)理论的一个基本定理，任何满足此条件的函数 $\widehat{W}(\mathbf{C})$ 都可以表示为其张量宗量 $\mathbf{C}$ 的[主不变量](@entry_id:193522)的函数 [@problem_id:2664596]。因此，对于一个各向同性的[超弹性材料](@entry_id:190241)，其[应变能密度函数](@entry_id:755490)最终可以写成：
$$
W = \bar{W}(I_1, I_2, I_3)
$$
由于[不变量](@entry_id:148850) $I_1, I_2, I_3$ 是主拉伸 $\lambda_i$ 的[对称函数](@entry_id:177113)，这也意味着[应变能](@entry_id:162699) $W$ 必然是主拉伸的[对称函数](@entry_id:177113)，即交换任意两个主拉伸的值，应变能不变。反之亦然，根据[对称函数](@entry_id:177113)基本定理，任何关于主拉伸的[对称函数](@entry_id:177113)都可以表示为[不变量](@entry_id:148850)的函数。这两种表达方式是等价的 [@problem_id:2664596]。

### [应力-应变关系](@entry_id:274093)的[热力学](@entry_id:141121)推导

[超弹性材料](@entry_id:190241)的应力状态完全由其[应变能密度函数](@entry_id:755490) $W$ 决定。这一关系可以从热力学第二定律严格推导出来。对于[等温过程](@entry_id:143096)，Clausius-Duhem 不等式（或称[耗散不等式](@entry_id:188634)）的局部形式为：
$$
\mathcal{D}_{m} = \mathcal{P}_{int} - \dot{W} \ge 0
$$
其中 $\mathcal{D}_{m}$ 是单位参考体积的力学[耗散率](@entry_id:748577)，$\mathcal{P}_{int}$ 是内[应力功率](@entry_id:182907)，$\dot{W}$ 是单位参考体积亥姆霍兹自由能（即[应变能](@entry_id:162699)）的时间变化率。

对于[超弹性材料](@entry_id:190241)，我们假设变形过程是可逆的，不存在[能量耗散](@entry_id:147406)，即 $\mathcal{D}_{m} = 0$。内[应力功率](@entry_id:182907)可以表示为第一皮奥拉-基尔霍夫（Piola-Kirchhoff）应力张量 $\mathbf{P}$ 与变形梯度率 $\dot{\mathbf{F}}$ 的[点积](@entry_id:149019)：$\mathcal{P}_{int} = \mathbf{P} : \dot{\mathbf{F}}$。[应变能](@entry_id:162699) $W$ 是 $\mathbf{C}$ 的函数，因此其变化率由[链式法则](@entry_id:190743)给出：$\dot{W} = \frac{\partial W}{\partial \mathbf{C}} : \dot{\mathbf{C}}$。利用运动学关系 $\dot{\mathbf{C}} = \dot{\mathbf{F}}^T \mathbf{F} + \mathbf{F}^T \dot{\mathbf{F}}$，并经过一系列张量运算，可以证明 $\dot{W} = 2 \mathbf{F} \frac{\partial W}{\partial \mathbf{C}} : \dot{\mathbf{F}}$ [@problem_id:2664664]。

将这些关系代入[耗散不等式](@entry_id:188634)，我们得到：
$$
\left( \mathbf{P} - 2 \mathbf{F} \frac{\partial W}{\partial \mathbf{C}} \right) : \dot{\mathbf{F}} = 0
$$
由于此式对任意变形过程（即任意 $\dot{\mathbf{F}}$）都成立，因此括号内的项必须为零。这给出了[第一皮奥拉-基尔霍夫应力](@entry_id:163971)的本构表达式：$\mathbf{P} = 2 \mathbf{F} \frac{\partial W}{\partial \mathbf{C}}$。

在实际应用中，我们更关心当前构型下的真实应力，即**柯西应力张量**（**Cauchy stress tensor**）$\boldsymbol{\sigma}$。它与 $\mathbf{P}$ 的关系为 $\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-T}$。联立两个 $\mathbf{P}$ 的表达式，并进行整理，我们最终得到柯西应力的通用表达式 [@problem_id:2664664]：
$$
\boldsymbol{\sigma} = \frac{2}{J} \mathbf{F} \frac{\partial W}{\partial \mathbf{C}} \mathbf{F}^T
$$
这个重要的公式将柯西[应力与应变](@entry_id:137374)能函数通过其对变形张量 $\mathbf{C}$ 的导数联系起来，构成了超[弹性理论](@entry_id:184142)的核心。

### 不[可压缩超弹性模型](@entry_id:167064)

许多类橡胶材料在承受剪切和拉伸变形时，其体积变化非常微小，因此在建模时通常被理想化为**不可压缩**（**incompressible**）材料。这一假设极大地简化了[本构关系](@entry_id:186508)。

不可压缩性意味着体积比 $J$ 恒等于1，即 $J = \det \mathbf{F} = 1$。这导致第三[不变量](@entry_id:148850) $I_3 = J^2 = 1$ 成为一个固定的约束，而非一个独立的变量。因此，不可压缩[各向同性材料](@entry_id:170678)的[应变能函数](@entry_id:178435)仅依赖于前两个[不变量](@entry_id:148850) [@problem_id:2664596]：
$$
W = \tilde{W}(I_1, I_2)
$$

**[静水压力](@entry_id:275365)的作用**
[不可压缩性](@entry_id:274914)是一个[运动学](@entry_id:173318)约束。为了在满足[平衡方程](@entry_id:172166)的同时维持这一约束，材料内部会产生一个额外的应[力场](@entry_id:147325)。在变分原理中，这个约束通过引入一个**拉格朗日乘子场**（**Lagrange multiplier field**）$p(\mathbf{X})$ 来施加。这个[拉格朗日乘子](@entry_id:142696)在物理上对应一个**静水压力**（**hydrostatic pressure**）。柯西应力张量因此被分解为一个由本构律决定的[部分和](@entry_id:162077)一个由[静水压力](@entry_id:275365)决定的部分。对于[不可压缩材料](@entry_id:159741)，柯西应力的一般形式为：
$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}_e - p \mathbf{I}
$$
其中 $\boldsymbol{\sigma}_e$ 是由[应变能函数](@entry_id:178435) $W$ 决定的“弹性”部分，$-p\mathbf{I}$ 是[静水压力](@entry_id:275365)部分。重要的是，**$p$ 不是一个材料常数，也不是由本构律决定的**。它是一个未知的场变量，其值必须通过求解包含平衡方程、不可压缩约束和边界条件的完整[边值问题](@entry_id:193901)来确定 [@problem_id:2664634]。除非在边界上施加了[绝对压力](@entry_id:144445)或牵[引力](@entry_id:175476)基准，否则静水压力 $p$ 只能确定到一个任意的附加常数 [@problem_id:2664634]。

**不可压缩[新胡克模型](@entry_id:165881)**
最简单和最经典的[超弹性](@entry_id:159356)模型之一是**不可压缩[新胡克模型](@entry_id:165881)**（**incompressible Neo-Hookean model**）。其[应变能密度函数](@entry_id:755490)仅线性依赖于第一个[不变量](@entry_id:148850) $I_1$：
$$
W = C_1(I_1 - 3) = \frac{\mu}{2}(I_1 - 3)
$$
其中 $\mu = 2C_1$ 是材料的**[剪切模量](@entry_id:167228)**（**shear modulus**），常数-3是为了保证在未变形状态下（$I_1 = 3$）[应变能](@entry_id:162699)为零。

对于不可压缩[各向同性材料](@entry_id:170678)，柯西应力的一般表达式为 $\boldsymbol{\sigma} = -p\mathbf{I} + 2\frac{\partial W}{\partial I_1}\mathbf{B} - 2\frac{\partial W}{\partial I_2}\mathbf{B}^{-1}$。对于[新胡克模型](@entry_id:165881)，我们有 $\frac{\partial W}{\partial I_1} = C_1 = \mu/2$ 且 $\frac{\partial W}{\partial I_2} = 0$。代入后，我们得到不可压缩[新胡克模型](@entry_id:165881)的[本构方程](@entry_id:138559) [@problem_id:2664598]：
$$
\boldsymbol{\sigma} = \mu \mathbf{B} - p \mathbf{I}
$$
这个简洁的表达式表明，新胡克材料的应力由[剪切模量](@entry_id:167228)、[左柯西-格林张量](@entry_id:186163)和一个待定的静水压力场共同决定。

**不可压缩 Mooney-Rivlin 模型**
为了更好地拟合某些橡胶材料在中[等应变](@entry_id:184570)范围内的力学行为，**Mooney-Rivlin 模型**在[应变能函数](@entry_id:178435)中增加了一个[线性依赖](@entry_id:185830)于 $I_2$ 的项：
$$
W = C_{10}(I_1 - 3) + C_{01}(I_2 - 3)
$$
其中 $C_{10}$ 和 $C_{01}$ 是材料常数。[新胡克模型](@entry_id:165881)可以视为 Mooney-Rivlin 模型在 $C_{01}=0$ 时的特例。该模型的柯西应力为：
$$
\boldsymbol{\sigma} = -p\mathbf{I} + 2C_{10}\mathbf{B} - 2C_{01}\mathbf{B}^{-1}
$$
对于小应变情况，Mooney-Rivlin 材料的[剪切模量](@entry_id:167228)为 $\mu = 2(C_{10} + C_{01})$。$C_{01}$ 项的存在对材料在[大变形](@entry_id:167243)下的行为有显著影响。例如，在[单轴拉伸](@entry_id:188287)实验中，主拉伸为 $\lambda$ 时，Mooney-Rivlin 模型预测的名义应力（[第一皮奥拉-基尔霍夫应力](@entry_id:163971)）为 [@problem_id:2664626]：
$$
P_{11}^{\mathrm{MR}}(\lambda) = 2C_{10}(\lambda - \lambda^{-2}) + 2C_{01}(1 - \lambda^{-3})
$$
而[新胡克模型](@entry_id:165881)（在相同的剪切模量 $\mu$ 下，即 $2C_{10}=\mu$）的预测为 $P_{11}^{\mathrm{NH}}(\lambda) = \mu(\lambda - \lambda^{-2})$。当 $\lambda \to \infty$ 时，[新胡克模型](@entry_id:165881)的[应力-应变曲线](@entry_id:159459)的[切线](@entry_id:268870)模量趋近于 $\mu$，而 Mooney-Rivlin 模型的[切线](@entry_id:268870)模量趋近于 $2C_{10} = \mu - 2C_{01}$。这意味着，如果 $C_{01}>0$，Mooney-Rivlin 模型在大拉伸下的刚度会比具有相同小应变[剪切模量](@entry_id:167228)的[新胡克模型](@entry_id:165881)更“软” [@problem_id:2664626]。

### 可压缩模型与等容-[体积分](@entry_id:171119)解

尽管不可压缩假设在许多情况下是有效的，但所有真实材料都是可压缩的。为了建立能够描述体积变化的可压缩模型，同时避免非物理的剪切-体积耦合效应（例如，纯剪切变形不应产生[静水压力](@entry_id:275365)，纯体积膨胀不应产生剪切应力），通常采用**等容-[体积分](@entry_id:171119)解**（**isochoric-volumetric split**）的方法。

该方法的核心思想是将[应变能函数](@entry_id:178435) $W$ 分解为两部分：一部分只与形状改变（[等容变形](@entry_id:196451)）有关，另一部分只与体积改变有关：
$$
W = W_{\mathrm{iso}}(\bar{I}_1, \bar{I}_2) + U(J)
$$
这里，$U(J)$ 是一个仅依赖于体积比 $J$ 的函数，用于描述材料的体积响应。$W_{\mathrm{iso}}$ 是等容部分的应变能，它依赖于**修正[不变量](@entry_id:148850)**（**modified invariants**）$\bar{I}_1$ 和 $\bar{I}_2$。这些[不变量](@entry_id:148850)由**修正[右柯西-格林张量](@entry_id:174156)** $\bar{\mathbf{C}}$ 计算得出，其定义为：
$$
\bar{\mathbf{C}} = J^{-2/3}\mathbf{C}
$$
这个定义确保了 $\det(\bar{\mathbf{C}}) = 1$，即 $\bar{\mathbf{C}}$ 仅包含[等容变形](@entry_id:196451)的信息。修正[不变量](@entry_id:148850)则为 $\bar{I}_1 = \mathrm{tr}(\bar{\mathbf{C}})$ 和 $\bar{I}_2 = \frac{1}{2} [(\mathrm{tr}(\bar{\mathbf{C}}))^2 - \mathrm{tr}(\bar{\mathbf{C}}^2)]$。这种分解形式，结合在参考状态下 $U'(1)=0$ 的条件，可以确保剪切和体积响应的[解耦](@entry_id:637294) [@problem_id:2664691]。值得注意的是，使用未经修正的[不变量](@entry_id:148850) $I_1, I_2$ 与 $U(J)$ 的简单叠加形式，如 $W(I_1, I_2) + U(J)$，是无法实现这种解耦的，因为 $I_1$ 和 $I_2$ 本身就依赖于体积变化 $J$ [@problem_id:2664691]。

基于这种分解，**可压缩 Mooney-Rivlin 模型**的[应变能函数](@entry_id:178435)可以写作 [@problem_id:2582958]：
$$
W = C_{1}(\bar{I}_{1} - 3) + C_{2}(\bar{I}_{2} - 3) + U(J)
$$
在此模型中，材料参数 $C_1$ 和 $C_2$ 完[全控制](@entry_id:275827)了材料的偏应力（剪切）响应，而函数 $U(J)$ 则完[全控制](@entry_id:275827)了其体积响应（例如，体模量 $K_0 = U''(1)$）。小应变[剪切模量](@entry_id:167228)由 $\mu_0 = 2(C_1 + C_2)$ 给出，它独立于体积[响应函数](@entry_id:142629) $U(J)$ [@problem_id:2582958] [@problem_id:2664691]。

### [唯象模型](@entry_id:273816)的局限性与扩展

虽然[新胡克模型](@entry_id:165881)和 Mooney-Rivlin 模型在描述橡胶材料中等到[大应变](@entry_id:751152)行为方面取得了巨大成功，但它们是唯象的，并未完全捕捉到所有复杂的物理现象。

**大拉伸下的[应变硬化](@entry_id:160669)**
实验表明，当橡胶被拉伸到接近其分子链伸展极限时，其刚度会急剧增加，这种现象称为**[应变硬化](@entry_id:160669)**（**strain stiffening**）或“锁定”。新胡克和 Mooney-Rivlin 模型的[应力-应变关系](@entry_id:274093)本质上是拉伸比 $\lambda$ 的有理多项式函数，它们在任何有限拉伸下都是光滑且有限的，无法描述这种应力急剧上升的现象 [@problem_id:2664604]。为了捕捉这种行为，需要引入具有奇异性的[应变能函数](@entry_id:178435)。例如，**Gent 模型**的[应变能函数](@entry_id:178435)为：
$$
W = -\frac{\mu J_m}{2} \ln \left(1 - \frac{I_1-3}{J_m}\right)
$$
其中 $J_m$ 是一个与分子链极限伸长相关的材料常数。当 $I_1$ 趋近于其极限值 $I_{1, \max} = 3+J_m$ 时，对数项的宗量趋于零，导致[应变能](@entry_id:162699)和应力趋于无穷大。这在数学上引入了一个有限拉伸极限 $\lambda_{\max}$，从而成功地模拟了链锁定导致的急剧[硬化](@entry_id:177483)现象 [@problem_id:2664604]。

**非弹性效应：滞后与 Mullins 效应**
标准的[超弹性](@entry_id:159356)模型本质上是**保守的**（**conservative**），即应力只依赖于当前的变形状态，而与加载历史无关。这意味着在任何一个闭合的加载-卸载循环中，做的净功为零，加载和卸载的[应力-应变曲线](@entry_id:159459)完全重合。因此，这类模型无法描述实验中普遍观察到的**滞后现象**（**hysteresis**，即加载-卸载曲线形成一个封闭的环，面积代表能量耗散）和**Mullins 效应**（**Mullins effect**，即材料在初次加载后的再次加载过程中，应力会显著低于初次加载的水平，表现出[应力软化](@entry_id:176824)）[@problem_id:2664635]。

要模拟这些非弹性、不可逆的现象，必须扩展本构框架，引入描述材料内部状态演化的**内变量**（**internal variables**），并确保整个模型符合[热力学第二定律](@entry_id:142732)（即耗散非负）。
*   为了捕捉**滞后现象**，通常需要引入**粘弹性**（**viscoelasticity**）机制，其中内变量可以代表粘性网络的非平衡状态。这会导致与应变率相关的能量耗散。
*   为了捕捉**Mullins 效应**，通常采用**[伪弹性](@entry_id:159612)**（**pseudo-elasticity**）或**[损伤力学](@entry_id:178377)**（**damage mechanics**）的框架。其中，内变量可以是一个与历史最[大应变](@entry_id:751152)相关的“损伤”或“软化”参数，它会改变材料的弹性响应，从而使应力-应变行为依赖于加载历史 [@problem_id:2664635]。

总之，新胡克和 Mooney-Rivlin 模型为理解[非线性弹性](@entry_id:185743)提供了一个强大而简洁的框架，但它们的适用性受限于其纯粹弹性和唯象的本质。更精确的[材料建模](@entry_id:751724)需要结合基于微观物理的洞察和更复杂的、包含内变量的[热力学一致的](@entry_id:755906)本构理论。