## 引言
[应力与应变](@entry_id:137374)张量是描述物质如何响应外力并发生变形的基石，构成了从宏伟的桥梁设计到精密的纳米器件制造等所有力学分析的核心语言。无论是在工程实践还是前沿科学研究中，精确量化材料内部的力[分布](@entry_id:182848)（应力）和几何形变（应变）都是理解、预测并最终控制其力学行为的首要前提。然而，如何建立一个能够无缝连接宏观世界与微观尺度的统一力学框架，并解释诸如薄膜内应力、[纳米线](@entry_id:195506)中的[尺度效应](@entry_id:153734)等复杂现象，仍然是一个持续的挑战。

本文旨在系统性地梳理[应力与应变](@entry_id:137374)张量的理论与应用，为读者构建一个从基础到前沿的完整知识体系。在“原理和机制”一章中，我们将从变形运动学出发，严谨地定义应变和应力张量，并探讨将二者联系起来的本构关系，最后延伸至[纳米力学](@entry_id:185346)中的高级概念。接下来，“应用与跨学科[交叉](@entry_id:147634)”一章将通过丰富的案例，展示这些理论如何在[材料科学](@entry_id:152226)、薄膜技术和纳米传感器等领域解决实际问题。最后，“动手实践”部分将提供具体的计算练习，帮助读者巩固所学知识，将抽象的张量理论转化为解决问题的实用技能。

## 原理和机制

本章旨在为应力和[应变张量](@entry_id:193332)的研究奠定坚实的理论基础。我们将从描述物体变形的[运动学](@entry_id:173318)出发，系统地建立应变张量的概念。随后，我们将探讨物体内部的力，并引入[应力张量](@entry_id:148973)作为其数学描述。最后，我们将讨论连接应力与应变的[本构关系](@entry_id:186508)，并深入探讨[纳米力学](@entry_id:185346)领域中特有的一些高级概念，例如表面效应、多尺度建模方法以及[广义连续介质理论](@entry_id:193621)。

### 变形[运动学](@entry_id:173318)——应变的测量

在连续介质力学中，对变形的精确描述是分析[材料力学](@entry_id:201885)行为的第一步。“应变”这一概念正是为了量化变形的程度和性质而引入的。我们将从最普适的有限变形理论出发，逐步过渡到工程实践中更为常用的线性化[小变形理论](@entry_id:174991)。

#### 变形梯度：局部变形的完整描述

想象一个连续体，它在初始时刻占据空间中的一个区域，我们称之为**参考构型**或初始构型，记作 $\Omega_0$。物体中的任意一点在此构型中的位置由物质坐标 $\mathbf{X}$ 描述。当物体受到外力或发生其他物理过程时，它会运动并变形，在当前时刻占据一个新的空间区域，我们称之为**当前构型**，记作 $\Omega_t$。同一点在当前构型中的位置由空间坐标 $\mathbf{x}$ 描述。

连接这两个构型的数学桥梁是**变形映射** $\mathbf{x} = \varphi(\mathbf{X}, t)$。这个映射描述了每个物[质点](@entry_id:186768) $\mathbf{X}$ 如何随时间 $t$ 移动到其当前位置 $\mathbf{x}$。相应地，一个物质点的**[位移场](@entry_id:141476)** $\mathbf{u}$ 定义为其当前位置与初始位置之差：$\mathbf{u}(\mathbf{X}, t) = \varphi(\mathbf{X}, t) - \mathbf{X}$。当物理量表示为物质坐标 $\mathbf{X}$ 的函数时，我们称之为**参考构型描述**或[拉格朗日描述](@entry_id:264498)；当其表示为空间坐标 $\mathbf{x}$ 的函数时，则称为**当前构型描述**或[欧拉描述](@entry_id:264722)。[@problem_id:2788083]

为了描述变形的局部特性，我们考察一个在参考构型中无限小的物质线元 $d\mathbf{X}$。经过变形后，它被映射为当前构型中的一个空间线元 $d\mathbf{x}$。变形[映射的微分](@entry_id:269524)给出了这两个线元之间的[线性关系](@entry_id:267880)：$d\mathbf{x} = \mathbf{F} d\mathbf{X}$。

这里的[二阶张量](@entry_id:199780) $\mathbf{F}$ 被称为**变形梯度张量**，其定义为变形映射对物质坐标的梯度：
$$
\mathbf{F} = \nabla_{\mathbf{X}} \mathbf{x} = \frac{\partial \varphi(\mathbf{X})}{\partial \mathbf{X}}
$$
以分量形式写作 $F_{ij} = \frac{\partial x_i}{\partial X_j}$。变形梯度 $\mathbf{F}$ 是描述局部变形最核心的物理量，它包含了关于局部拉伸、压缩、剪切和刚体旋转的全部信息。

从变形梯度的定义出发，我们可以建立它与[位移梯度](@entry_id:165352)之间的关系。[位移场](@entry_id:141476)的物质梯度（即对 $\mathbf{X}$ 求梯度）为 $\nabla_{\mathbf{X}} \mathbf{u} = \nabla_{\mathbf{X}} (\mathbf{x} - \mathbf{X}) = \nabla_{\mathbf{X}} \mathbf{x} - \nabla_{\mathbf{X}} \mathbf{X} = \mathbf{F} - \mathbf{I}$，其中 $\mathbf{I}$ 是二阶单位张量。这个量，即**物质[位移梯度](@entry_id:165352)** $\nabla_{\mathbf{X}} \mathbf{u}$，在后续的应变定义中扮演重要角色。值得注意的是，它与位移场的空间梯度 $\nabla_{\mathbf{x}} \mathbf{u}$ 是不同的，后者等于 $\mathbf{I} - \mathbf{F}^{-1}$。[@problem_id:2788083]

变形梯度不仅描述了线元的变形，也决定了面元和[体元](@entry_id:267802)的变形。变形前后，一个面元法向量 $\mathbf{N}$ 和面积 $dA$ 会通过著名的**[南森公式](@entry_id:195566) (Nanson's formula)** 变换为新的[法向量](@entry_id:264185) $\mathbf{n}$ 和面积 $da$：$\mathbf{n} da = J \mathbf{F}^{-\mathsf{T}} \mathbf{N} dA$。而一个体积元 $dV$ 则会变为 $dv = J dV$。这里的 $J = \det(\mathbf{F})$ 是变形的[雅可比行列式](@entry_id:137120)，代表了局部的体积变化率。例如，在质量守恒定律中，参考构型下的密度 $\Theta_0(\mathbf{X})$ 和当前构型下的密度 $\theta(\mathbf{x})$ 通过关系 $\Theta_0 = J (\theta \circ \varphi)$ 联系起来，而非简单的复合。[@problem_id:2788083]

#### [有限应变度量](@entry_id:185716)

变形梯度 $\mathbf{F}$ 本身包含了[刚体转动](@entry_id:191086)，而我们通常更关心那些能引起材料内力、导致能量储存的纯粹“形变”。因此，我们需要定义一个对刚体运动不敏感的[应变度量](@entry_id:755495)。

一个关键的构造是**[右柯西-格林张量](@entry_id:174156) (Right Cauchy-Green tensor)** $\mathbf{C}$，定义为：
$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}
$$
我们可以考察两个物质[线元](@entry_id:196833) $d\mathbf{X}_1$ 和 $d\mathbf{X}_2$ 之间的[内积](@entry_id:158127)。变形后，它们的[内积](@entry_id:158127)变为 $d\mathbf{x}_1 \cdot d\mathbf{x}_2 = (\mathbf{F}d\mathbf{X}_1) \cdot (\mathbf{F}d\mathbf{X}_2) = d\mathbf{X}_1^{\mathsf{T}} \mathbf{F}^{\mathsf{T}} \mathbf{F} d\mathbf{X}_2 = d\mathbf{X}_1^{\mathsf{T}} \mathbf{C} d\mathbf{X}_2$。这表明，$\mathbf{C}$ 完全描述了物质邻域内长度和角度的改变。重要的是，如果变形仅仅是一个刚体旋转，$\mathbf{F}$ 将是一个正交张量，此时 $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \mathbf{I}$，表明没有发生形变。

基于此，我们可以定义一个纯粹的[应变度量](@entry_id:755495)——**[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)** $\mathbf{E}$：
$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^{\mathsf{T}}\mathbf{F} - \mathbf{I})
$$
当且仅当没有变形时（即 $\mathbf{C}=\mathbf{I}$），$\mathbf{E}$ 才为零。$\mathbf{E}$ 是一个对称张量，它是描述有限变形的常用[应变度量](@entry_id:755495)之一，完全定义在参考构型上。

为了具体理解这些概念，让我们考虑一个在[纳米力学](@entry_id:185346)中常见的**简单剪切**变形。一个晶体单层膜的变形映射为 $\mathbf{x} = (X_1 + k X_2, X_2, X_3)$，其中 $k$ 是一个无量纲的剪切参数。[@problem_id:2788087]
1.  首先计算变形梯度 $\mathbf{F}$：
    $$
    \mathbf{F} = \begin{pmatrix} 1 & k & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix}
    $$
2.  然后计算[右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$：
    $$
    \mathbf{C} = \begin{pmatrix} 1 & 0 & 0 \\ k & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 1 & k & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} = \begin{pmatrix} 1 & k & 0 \\ k & k^2+1 & 0 \\ 0 & 0 & 1 \end{pmatrix}
    $$
3.  最后得到[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})$：
    $$
    \mathbf{E} = \frac{1}{2} \begin{pmatrix} 0 & k & 0 \\ k & k^2 & 0 \\ 0 & 0 & 0 \end{pmatrix} = \begin{pmatrix} 0 & k/2 & 0 \\ k/2 & k^2/2 & 0 \\ 0 & 0 & 0 \end{pmatrix}
    $$
这个例子清晰地展示了如何从一个给定的变形映射一步步计算出核心的[应变度量](@entry_id:755495)。可以看到，$\mathbf{E}$ 的分量是[非线性](@entry_id:637147)的（包含 $k^2$ 项），这正是[有限应变理论](@entry_id:176941)的特征。

#### 线性化运动学：微[小应变张量](@entry_id:754968)

在许多工程和物理问题中，变形非常微小，即[位移梯度](@entry_id:165352) $\nabla\mathbf{u}$ 的所有分量都远小于1。在这种情况下，我们可以对[有限应变理论](@entry_id:176941)进行线性化，从而得到极大的简化。

将 $\mathbf{F} = \mathbf{I} + \nabla_{\mathbf{X}}\mathbf{u}$ 代入[格林-拉格朗日应变张量](@entry_id:187745)的定义中：
$$
\mathbf{E} = \frac{1}{2}((\mathbf{I} + (\nabla_{\mathbf{X}}\mathbf{u})^{\mathsf{T}})(\mathbf{I} + \nabla_{\mathbf{X}}\mathbf{u}) - \mathbf{I}) = \frac{1}{2}(\nabla_{\mathbf{X}}\mathbf{u} + (\nabla_{\mathbf{X}}\mathbf{u})^{\mathsf{T}} + (\nabla_{\mathbf{X}}\mathbf{u})^{\mathsf{T}}\nabla_{\mathbf{X}}\mathbf{u})
$$
在小变形假设下，[位移梯度](@entry_id:165352)本身已经很小，其二次项 $(\nabla_{\mathbf{X}}\mathbf{u})^{\mathsf{T}}\nabla_{\mathbf{X}}\mathbf{u}$ 可以忽略不计。此外，物质坐标 $\mathbf{X}$ 和空间坐标 $\mathbf{x}$ 近似相等，因此对两者的梯度运算也不再区分，统一用 $\nabla\mathbf{u}$ 表示。于是，我们得到**微[小应变张量](@entry_id:754968) (infinitesimal strain tensor)** 或**柯西[应变张量](@entry_id:193332) (Cauchy's strain tensor)** $\boldsymbol{\varepsilon}$：
$$
\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^{\mathsf{T}})
$$
这个张量是[位移梯度](@entry_id:165352)的对称部分。[位移梯度](@entry_id:165352)的反对称部分则定义为**微小转动张量 (infinitesimal rotation tensor)** $\boldsymbol{\omega}$：
$$
\boldsymbol{\omega} = \frac{1}{2}(\nabla\mathbf{u} - (\nabla\mathbf{u})^{\mathsf{T}})
$$
因此，[位移梯度](@entry_id:165352)可以分解为应变和转动的线性叠加：$\nabla\mathbf{u} = \boldsymbol{\varepsilon} + \boldsymbol{\omega}$。[@problem_id:2788100]

$\boldsymbol{\varepsilon}$ 描述了物体的纯粹形变（拉伸和剪切），而 $\boldsymbol{\omega}$ 描述了物体的局部[刚体转动](@entry_id:191086)。一个重要的物理区别是：只有应变 $\boldsymbol{\varepsilon}$ 会在材料内部产生弹性能，从而引起应力；[刚体转动](@entry_id:191086) $\boldsymbol{\omega}$ 本身不产生[能量储存](@entry_id:264866)。例如，在经典柯西连续体中，[应力功率](@entry_id:182907)密度（单位体积做功的速率）只与[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}$ 有关，而与转动速率 $\dot{\boldsymbol{\omega}}$ 无关。[@problem_id:2788100]

让我们考虑一个纳米晶薄膜晶界附近的二维[位移场](@entry_id:141476) $\mathbf{u}(x,y) = (ax-\theta y, -ay+\theta x)$，其中 $a$ 代表拉伸/压缩，$\theta$ 代表转动。[@problem_id:2788100]
[位移梯度](@entry_id:165352)为 $\nabla\mathbf{u} = \begin{pmatrix} a & -\theta \\ \theta & -a \end{pmatrix}$。
通过分解，我们得到：
-   微[小应变张量](@entry_id:754968)：$\boldsymbol{\varepsilon} = \begin{pmatrix} a & 0 \\ 0 & -a \end{pmatrix}$，这代表了一个在x方向拉伸、y方向压缩的纯[剪切变形](@entry_id:170920)，且体积不变（因为 $\mathrm{tr}(\boldsymbol{\varepsilon}) = a-a=0$）。
-   微小转动张量：$\boldsymbol{\omega} = \begin{pmatrix} 0 & -\theta \\ \theta & 0 \end{pmatrix}$，这代表了一个绕z轴转动 $\theta$ 角的[刚体转动](@entry_id:191086)。

这个例子清晰地展示了[位移梯度](@entry_id:165352)如何包含两种截然不同的运动信息。微[小应变张量](@entry_id:754968)的一个关键性质是其**线性化客观性**：在一个已有的变形场上叠加一个微小的[刚体转动](@entry_id:191086)，不会改变计算出的微[小应变张量](@entry_id:754968) $\boldsymbol{\varepsilon}$。这表明 $\boldsymbol{\varepsilon}$ 是一个真正的形变度量，与观察者的[刚性运动](@entry_id:170523)无关。[@problem_id:2788100]

### 内部力的描述——应力张量

当一个物体变形时，其内部会产生相互作用力来抵抗这种变形。为了描述这些[分布](@entry_id:182848)在体内的力，我们引入应力的概念。

#### 柯西应力张量与traction

想象在连续体内部取一个任意的微小面元，其[单位法向量](@entry_id:178851)为 $\mathbf{n}$。面元一侧的物质会对另一侧的物质施加一个[分布](@entry_id:182848)力。定义**[面力矢量](@entry_id:189429) (traction vector)** $\mathbf{t}(\mathbf{n})$ 为单位面积上所受的力。这个力的大小和方向通常都依赖于面元的方向 $\mathbf{n}$。

一个深刻的结论，即**柯西应力定理 (Cauchy's Stress Theorem)**，指出[面力矢量](@entry_id:189429) $\mathbf{t}(\mathbf{n})$ 与法向量 $\mathbf{n}$ 之间存在[线性关系](@entry_id:267880)。这种关系通过一个[二阶张量](@entry_id:199780)来描述，这个张量就是**柯西[应力张量](@entry_id:148973) (Cauchy stress tensor)** $\boldsymbol{\sigma}$：
$$
\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n}
$$
柯西应力张量 $\boldsymbol{\sigma}(\mathbf{x}, t)$ 是一个场量，它完全描述了物体内某一点 $\mathbf{x}$ 在时刻 $t$ 的应力状态。一旦知道了某一点的 $\boldsymbol{\sigma}$，我们就可以计算作用在任何通过该点的平面上的力。

在经典连续介质力学中（即不考虑体力矩和耦合应力），动量矩[守恒定律](@entry_id:269268)要求柯西应力张量必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$。这是一个非常重要的性质，它将独立分量的数量从9个减少到6个。

#### 主应力与[应力不变量](@entry_id:170526)

由于柯西应力张量 $\boldsymbol{\sigma}$ 是一个实对称二阶张量，根据谱定理，它必然存在三个实[特征值](@entry_id:154894)，称为**主应力 (principal stresses)**，记为 $\sigma_1, \sigma_2, \sigma_3$。对应的三个相互正交的[特征向量](@entry_id:151813) $\mathbf{n}_1, \mathbf{n}_2, \mathbf{n}_3$ 称为**[主方向](@entry_id:276187) (principal directions)**。

在物理上，主方向是指那些应力作用面上只有正应力而没有剪应力的方向。在以主方向为基底的[坐标系](@entry_id:156346)中，[应力张量](@entry_id:148973)呈[对角形式](@entry_id:264850)：
$$
\boldsymbol{\sigma} = \begin{pmatrix} \sigma_1 & 0 & 0 \\ 0 & \sigma_2 & 0 \\ 0 & 0 & \sigma_3 \end{pmatrix}
$$
利用谱分解，我们可以将[应力张量](@entry_id:148973)表示为：
$$
\boldsymbol{\sigma} = \sum_{i=1}^{3} \sigma_i (\mathbf{n}_i \otimes \mathbf{n}_i)
$$
其中 $\otimes$ 表示张量积。这个表达式非常有用。例如，我们可以用它来计算作用在任意平面（[法向量](@entry_id:264185)为 $\mathbf{n}$）上的[面力矢量](@entry_id:189429) $\mathbf{t}(\mathbf{n})$。将 $\mathbf{n}$ 在主方向基底上分解为 $\mathbf{n} = \sum_j c_j \mathbf{n}_j$（其中 $c_j = \mathbf{n} \cdot \mathbf{n}_j$ 是[方向余弦](@entry_id:170591)），代入柯西公式：
$$
\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma}\mathbf{n} = \left(\sum_{i} \sigma_i \mathbf{n}_i \otimes \mathbf{n}_i\right) \left(\sum_{j} c_j \mathbf{n}_j\right) = \sum_{i,j} \sigma_i c_j (\mathbf{n}_i \otimes \mathbf{n}_i)\mathbf{n}_j = \sum_i \sigma_i c_i \mathbf{n}_i
$$
这个结果表明，[面力矢量](@entry_id:189429)在[主方向](@entry_id:276187)上的分量等于相应的主应力乘以[方向余弦](@entry_id:170591)。

例如，假设一个立方晶体纳米薄膜内部某点的[主应力](@entry_id:176761)为 $\sigma_1 = 1.8$ GPa (沿 [100] 方向), $\sigma_2 = 0.6$ GPa (沿 [010] 方向), $\sigma_3 = -0.4$ GPa (沿 [001] 方向)。我们想计算作用在 (122) [晶面](@entry_id:166481)上的面力大小。[@problem_id:2788091]
(122) [晶面](@entry_id:166481)的[单位法向量](@entry_id:178851)为 $\mathbf{n} = \frac{1}{\sqrt{1^2+2^2+2^2}}[1,2,2] = [\frac{1}{3}, \frac{2}{3}, \frac{2}{3}]$。
[方向余弦](@entry_id:170591)为 $c_1=1/3, c_2=2/3, c_3=2/3$。
[面力矢量](@entry_id:189429)为 $\mathbf{t} = \sigma_1 c_1 \mathbf{n}_1 + \sigma_2 c_2 \mathbf{n}_2 + \sigma_3 c_3 \mathbf{n}_3$。
其大小为：
$$
\|\mathbf{t}\| = \sqrt{(\sigma_1 c_1)^2 + (\sigma_2 c_2)^2 + (\sigma_3 c_3)^2} = \sqrt{(1.8 \times \frac{1}{3})^2 + (0.6 \times \frac{2}{3})^2 + (-0.4 \times \frac{2}{3})^2} \approx 0.7688 \text{ GPa}
$$
这个计算过程清晰地展示了主应力概念的实际应用。

### [本构关系](@entry_id:186508)——连接[应力与应变](@entry_id:137374)

我们已经分别介绍了应变（描述变形）和应力（描述[内力](@entry_id:167605)），而将这两者联系起来的，就是材料的**[本构关系](@entry_id:186508) (constitutive relation)**。[本构关系](@entry_id:186508)反映了材料的内在物理属性。

#### 线性弹性与[刚度张量](@entry_id:176588)

对于许多材料，在小变形范围内，[应力与应变](@entry_id:137374)成正比。这就是**线性弹性**假设，其数学表达式为**[广义胡克定律](@entry_id:203555) (Generalized Hooke's Law)**：
$$
\sigma_{ij} = C_{ijkl} \varepsilon_{kl}
$$
这里的[四阶张量](@entry_id:181350) $C_{ijkl}$ 被称为**[刚度张量](@entry_id:176588) (stiffness tensor)** 或[弹性张量](@entry_id:170728)。它包含了描述材料线性弹性行为的所有信息。

对于**[超弹性材料](@entry_id:190241) (hyperelastic materials)**，其行为可以通过一个**[应变能密度函数](@entry_id:755490)** $W(\boldsymbol{\varepsilon})$ 来描述，应力是[应变能](@entry_id:162699)对应变的导数：$\sigma_{ij} = \frac{\partial W}{\partial \varepsilon_{ij}}$。在这种情况下，[刚度张量](@entry_id:176588)就是[应变能](@entry_id:162699)的[二阶导数](@entry_id:144508)：
$$
C_{ijkl} = \frac{\partial^2 W}{\partial \varepsilon_{ij} \partial \varepsilon_{kl}}
$$
由于 $\sigma_{ij}$ 和 $\varepsilon_{kl}$ 都是对称的，且 $W$ 是一个[光滑函数](@entry_id:267124)（[混合偏导数](@entry_id:139334)次序无关），[刚度张量](@entry_id:176588)具有以下对称性：
-   **次对称性 (Minor symmetries)**: $C_{ijkl} = C_{jikl} = C_{ijlk}$
-   **主对称性 (Major symmetry)**: $C_{ijkl} = C_{klij}$
这些对称性将 $3^4=81$ 个独立分量减少到21个，这代表了最一般各向异性[线性弹性](@entry_id:166983)材料所需的[弹性常数](@entry_id:146207)数量。[@problem_id:2788099]

材料的内部对称性会进一步减少[独立弹性常数](@entry_id:203649)的数量。一个重要的特例是**各向同性 (isotropic)** 材料，其力学性质不随方向改变。对于这类材料，[刚度张量](@entry_id:176588)可以仅用两个独立的**拉梅参数 (Lamé parameters)** $\lambda$ 和 $\mu$ 来表示：
$$
C_{ijkl} = \lambda \delta_{ij} \delta_{kl} + \mu (\delta_{ik}\delta_{jl} + \delta_{il}\delta_{jk})
$$
代入胡克定律，我们得到各向同性[线性弹性](@entry_id:166983)材料的[本构关系](@entry_id:186508)：
$$
\boldsymbol{\sigma} = 2\mu\boldsymbol{\varepsilon} + \lambda \mathrm{tr}(\boldsymbol{\varepsilon})\mathbf{I}
$$
这里，$\mu$ 通常被称为[剪切模量](@entry_id:167228)。对于其他[晶体对称性](@entry_id:198772)，独立常数数量也不同，例如，[立方晶体](@entry_id:198932)有3个独立常数，而横观各向同性材料有5个。[@problem_id:2788099]

#### [弹性常数](@entry_id:146207)的[热力学约束](@entry_id:755911)

弹性常数并非可以任意取值，它们必须满足热力学稳定性要求。一个基本原则是，要使材料发生变形，必须对其做正功。这意味着[应变能密度函数](@entry_id:755490) $W(\boldsymbol{\varepsilon})$ 必须是一个正定函数，即对于任何非零应变 $\boldsymbol{\varepsilon}$，都有 $W(\boldsymbol{\varepsilon}) > 0$。

对于各向同性[线性弹性](@entry_id:166983)体，[应变能密度](@entry_id:200085)为 $\psi_{\mathrm{b}} = \frac{1}{2}\boldsymbol{\sigma}:\boldsymbol{\varepsilon} = \mu(\boldsymbol{\varepsilon}:\boldsymbol{\varepsilon}) + \frac{\lambda}{2}(\mathrm{tr}(\boldsymbol{\varepsilon}))^2$。为了保证其[正定性](@entry_id:149643)，我们将[应变张量分解](@entry_id:184653)为**[偏应变](@entry_id:201263)部分** $\boldsymbol{\varepsilon}_{\mathrm{dev}}$ (描述形状改变) 和**体积应变部分** $\frac{1}{3}\mathrm{tr}(\boldsymbol{\varepsilon})\mathbf{I}$ (描述体积改变)。能量密度可以重写为：
$$
\psi_{\mathrm{b}} = \mu (\boldsymbol{\varepsilon}_{\mathrm{dev}} : \boldsymbol{\varepsilon}_{\mathrm{dev}}) + \frac{1}{2}( \lambda + \frac{2}{3}\mu )(\mathrm{tr}(\boldsymbol{\varepsilon}))^2
$$
为了使 $\psi_{\mathrm{b}}$ 对任何非零应变都为正，与形状改变相关的项和与体积改变相关的项必须都为正。这导出以下两个条件：
-   $\mu > 0$ (抵抗[剪切变形](@entry_id:170920))
-   $3\lambda + 2\mu > 0$ (或等价地，体模量 $K = \lambda + \frac{2}{3}\mu > 0$，抵[抗体](@entry_id:146805)积变化)
这些是三维体材料保持稳定所必须满足的条件。[@problem_id:2788105]

### [纳米力学](@entry_id:185346)中的[应力与应变](@entry_id:137374)——[跨尺度](@entry_id:754544)连接

在纳米尺度下，经典[连续介质力学](@entry_id:155125)的一些假设需要被审视和扩展。表面/界面的作用变得异常重要，而连续介质模型与底层原子结构之间的联系也成为研究的核心。

#### [表面应力](@entry_id:191241)与表面能

在纳米材料中，由于其巨大的[比表面积](@entry_id:141558)，表面的力学行为对整体性能有显著影响。我们需要区分两个密切相关但截然不同的概念：**表面能** $\gamma$ 和**表面应力张量** $\boldsymbol{\tau}_s$。

-   **[表面能](@entry_id:161228) (Surface energy)** $\gamma$（或称表面张力）是在恒温恒压下，可逆地创造单位面积新表面所需要做的功。它是一个标量。
-   **表面应力 (Surface stress)** $\boldsymbol{\tau}_s$ 是一个二维的二阶张量，它描述了可逆地拉伸或压缩一个已存在的表面单位长度线段所需要做的功。

这两者之间的关系由**[沙特尔沃思方程](@entry_id:199949) (Shuttleworth equation)** 给出：
$$
\boldsymbol{\tau}_s = \gamma \mathbf{I}_s + \frac{\partial \gamma}{\partial \boldsymbol{\varepsilon}_s}
$$
其中 $\boldsymbol{\varepsilon}_s$ 是表面[应变张量](@entry_id:193332)，$\mathbf{I}_s$ 是二维单位张量。这个方程可以通过对总[表面自由能](@entry_id:159200) $F_s = \int_S \gamma(\boldsymbol{\varepsilon}_s) da$ 进行变分推导得出。[@problem_id:2788080]

这个方程揭示了表面应力与[表面能](@entry_id:161228)的关键区别。对于液体，其表面能 $\gamma$ 与应变无关（液体表面无法承受剪切），因此 $\frac{\partial \gamma}{\partial \boldsymbol{\varepsilon}_s} = \mathbf{0}$，[表面应力](@entry_id:191241)简化为 $\boldsymbol{\tau}_s = \gamma \mathbf{I}_s$。此时，[表面应力](@entry_id:191241)是一个各向同性的张量，其大小就是表面张力。然而，对于固体表面，表面能通常依赖于应变，导致 $\frac{\partial \gamma}{\partial \boldsymbol{\varepsilon}_s}$ 非零。这意味着固体的表面应力通常是各向异性的，并且其值不等于表面能。[@problem_id:2788080] 同样地，[表面弹性](@entry_id:185474)常数也必须满足二维的热力学稳定性条件，例如对于各向同性表面，要求表面[剪切模量](@entry_id:167228) $\mu_s > 0$ 且二维体模量 $\lambda_s + \mu_s > 0$。[@problem_id:2788105]

#### 从原子到连续介质：柯西-玻恩准则与病毒应力

[连续介质力学](@entry_id:155125)中的本构关系（如弹性常数）最终源于原子间的相互作用。**柯西-玻恩准则 (Cauchy-Born rule)** 是连接原子尺度与连续介质尺度的关键假设之一。它断言：如果一个晶体经历宏观均匀变形（由变形梯度 $\mathbf{F}$ 描述），那么其晶格结构也同样按照 $\mathbf{F}$ 进行均匀变形。这意味着变形后的[晶格](@entry_id:196752)[基矢](@entry_id:199546) $\mathbf{a}'_i$ 与变形前的[基矢](@entry_id:199546) $\mathbf{a}_i$ 的关系为 $\mathbf{a}'_i = \mathbf{F} \mathbf{a}_i$。[@problem_id:2788123]

利用这个准则，我们可以从原子间相互作用势推导出连续介质的[应变能密度函数](@entry_id:755490) $W(\mathbf{F})$。例如，对于一个二维正方[晶格](@entry_id:196752)，原子间仅存在最近邻相互作用势 $\phi(r)$。通过计算变形后键长 $r$ 的变化，并将每个原子的键能加和，再除以单位参考面积，我们就可以得到 $W$。对于一个初始边长为 $a$ 的正方[晶格和](@entry_id:189839)势能 $\phi(r) = \frac{k}{2}(r-a)^2$，推导出的[应变能密度](@entry_id:200085)为：[@problem_id:2788123]
$$
W(\mathbf{F}) = \frac{k}{2} \left[ (\sqrt{C_{11}} - 1)^2 + (\sqrt{C_{22}} - 1)^2 \right]
$$
其中 $C_{ij}$ 是[右柯西-格林张量](@entry_id:174156)的分量。这个过程是多尺度建模中的一个典型范例。

另一个连接原子和连续介质的概念是**病毒应力 (virial stress)**。在[分子动力学模拟](@entry_id:160737)中，我们无法像在连续介质中那样定义一个清晰的[截面](@entry_id:154995)来计算应力。病毒应力提供了一种通过统计平均从原子的位置和动量计算宏观应力的方法。它由两部分贡献构成：一部分是**动能项**，来源于原子穿越虚拟边界时携带的动量；另一部分是**位形项**，来源于跨越虚拟边界的原子间相互作用力。[@problem_id:2788129]

病毒应力与柯西应力在概念上有所不同。柯西应力是描述物质在局部[静止参考系](@entry_id:262703)中动量通量的连续场量。而标准病毒应力计算的是[实验室参考系](@entry_id:166991)中的总动量通量，其中包含了由宏观流动（例如剪切流）引起的[对流](@entry_id:141806)项。为了将病毒应力与柯西应力进行严格比较，必须使用相对于局部平均流速的**奇特速度 (peculiar velocity)** 来计算动能项，并进行足够大的时空平均，以消除原子尺度的涨落，获得一个平滑的连续场量。[@problem_id:2788129, ACE]

#### 超越经典连续介质：用于[尺度效应](@entry_id:153734)的广义理论

当材料的特征尺寸（如薄膜厚度、晶粒尺寸）与内部微结构尺度（如[位错](@entry_id:157482)间距）相当时，经典连续介质理论可能失效，材料会表现出“越小越强”等**[尺度效应](@entry_id:153734) (size effects)**。为了描述这些现象，研究者们发展了多种**[广义连续介质理论](@entry_id:193621) (generalized continuum theories)**。

这些理论通过引入额外的自由度或高阶梯度来将[内禀长度尺度](@entry_id:750789)参数引入[本构关系](@entry_id:186508)中。两种有[代表性](@entry_id:204613)的理论是：[@problem_id:2788112]
1.  **[微极理论](@entry_id:202574) (Micropolar or Cosserat elasticity)**：该理论为连续体中的每个点赋予了独立的[转动自由度](@entry_id:141502) $\varphi_i$，以描述颗粒或微观结构的独立旋转。这导致了非对称的力-[应力张量](@entry_id:148973) $\sigma_{ij}$ 和一个全新的**[力偶应力](@entry_id:747952)张量 (couple-stress tensor)** $\mu_{ij}$。
2.  **[应变梯度理论](@entry_id:180517) (Strain-gradient elasticity)**：该理论不引入新的自由度，而是假设材料的应变能不仅依赖于应变 $\varepsilon_{ij}$，还依赖于应变的梯度 $\varepsilon_{ij,k}$。这导致了标准的对称柯西应力 $\sigma_{ij}$ 和一个**[高阶应力](@entry_id:186008)张量 (higher-order stress tensor)** $\tau_{ijk}$。

这些广义理论为模拟和理解[纳米材料](@entry_id:150391)中出现的、经典理论无法解释的复杂力学行为提供了强有力的数学框架。它们是连接微观世界与宏观工程应用的桥梁，在现代[纳米力学](@entry_id:185346)研究中占据着重要地位。