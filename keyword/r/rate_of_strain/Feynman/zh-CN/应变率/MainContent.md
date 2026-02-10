## 引言
运动不仅仅是从一点移动到另一点。对于任何能够改变形状的物体——从流动的河流到正在锻造的金属块——简单的速度概念是不足够的。我们如何精确描述变形体内发生的拉伸、剪切和扭曲？答案在于一个强大的数学概念，它捕捉了形状变化的本质：[应变率](@keyword=rate_of_strain|lang=zh-CN|style=Feynman)。本文将带领读者深入了解这个基本量。我们将从“原理与机制”部分开始，通过解构运动来揭示应变率张量，探索其数学性质和深刻的物理意义，从体积变化到其与能量和功率的联系。随后，在“应用与跨学科联系”部分，我们将看到这一个概念如何成为跨越不同领域的统一语言，解释[非牛顿流体](@keyword=non_newtonian_fluids|lang=zh-CN|style=Feynman)的行为、高温下固体的[蠕变](@keyword=creep|lang=zh-CN|style=Feynman)，乃至生物生长的力学。

## 原理与机制

想象一下你在一条河里漂浮。如果整条河以相同的速度移动，你只是顺流而下。这是纯粹的平移。但如果靠近右岸的水比靠近左岸的水流得快呢？你就会开始旋转。如果你前方的水比你后方的水流得快呢？你就会被拉伸。简单的速度概念不足以描述像河流、正在锻造的金属块或流过机翼的空气这样的[连续体](@keyword=continuum|lang=zh-CN|style=Feynman)的丰富运动。我们需要一种方法来捕捉速度如何从一点到另一点*变化*。

### 解构运动：从速度到变形

完成这项工作的工具是一个称为**速度梯度**的数学对象，表示为 $\mathbf{L} = \nabla\mathbf{v}$。它是一个[张量](@keyword=tensor|lang=zh-CN|style=Feynman)，充当了流场特征的完整局部地图。如果你告诉它附近一个水粒子的相对位置，它就能告诉你你们之间的速度差异。[速度梯度](@keyword=velocity_gradient|lang=zh-CN|style=Feynman)的非凡之处在于，它总能被分解为两个不同的部分：一个对称部分和一个反对称（或称斜对称）部分。

$$
\mathbf{L} = \mathbf{d} + \mathbf{W}
$$

反对称部分 $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T)$，被称为**[自旋张量](@keyword=spin_tensor|lang=zh-CN|style=Feynman)**（或[涡量张量](@keyword=vorticity_tensor|lang=zh-CN|style=Feynman)）。它描述了刚体的[局部旋转](@keyword=local_rotation|lang=zh-CN|style=Feynman)速率——也就是我们河流类比中的旋转部分。如果一个物体正在进行纯刚体旋转，比如一个旋转的陀螺，它的速度梯度将是纯反对称的，而这个[张量](@keyword=tensor|lang=zh-CN|style=Feynman) $\mathbf{W}$ 将完美地捕捉其角速度 [@problem_id:2917882]。

对称部分 $\mathbf{d} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T)$，是我们故事的主角。它被称为**变形率[张量](@keyword=tensor|lang=zh-CN|style=Feynman)**，或更简单地称为**应变率**。这个[张量](@keyword=tensor|lang=zh-CN|style=Feynman)描述了所有实际改变物体形状的运动——拉伸、压缩和剪切。一个运动被定义为“刚性”运动，当且仅当其变形率处处为零 [@problem_id:2917882]。任何物体要弯曲、拉伸或流动，其应变率张量必须非零。正是这个量将坚硬的石头与流动的水或变形的金属区分开来。

### 变形率的剖析

让我们来剖析这个[张量](@keyword=tensor|lang=zh-CN|style=Feynman) $\mathbf{d}$，看看它的分量告诉我们什么。它是一个 3x3 矩阵，每个元素都有直接的物理意义。

主对角线上的元素 $d_{11}$、$d_{22}$ 和 $d_{33}$ 代表沿坐标轴的**伸长率**（如果为负，则为收缩率）。想象一个材料块，其速度场由 $\mathbf{v} = (k_1 x_1, k_2 x_2, k_3 x_3)$ 给出。离原点越远的点沿各轴移动得越快。快速计算表明，该流动的[应变率张量](@keyword=rate_of_strain_tensor|lang=zh-CN|style=Feynman)是完全对角的：

$$
\mathbf{d} = \begin{pmatrix} k_1  0  0 \\ 0  k_2  0 \\ 0  0  k_3 \end{pmatrix}
$$

这表示沿 $x_1$、$x_2$ 和 $x_3$ 轴的纯拉伸或压缩，拉伸率由常数 $k_1$、$k_2$ 和 $k_3$ 给出 [@problem_id:1551728]。

这些对角元素之和是[张量](@keyword=tensor|lang=zh-CN|style=Feynman)的**迹**，$\text{tr}(\mathbf{d}) = d_{11} + d_{22} + d_{33}$。这个标量具有深刻的物理意义：它是**[体积应变率](@keyword=volumetric_strain_rate|lang=zh-CN|style=Feynman)**，即单位体积的体积变化率 [@problem_id:1805673]。如果你想知道一小块流[体膨胀](@keyword=volume_expansion|lang=zh-CN|style=Feynman)或被压缩的速度有多快，你只需要计算其[应变率张量](@keyword=rate_of_strain_tensor|lang=zh-CN|style=Feynman)的迹。如果 $\text{tr}(\mathbf{d}) = 0$，则材料正在进行**不可压缩**流动；即使其形状可能在剧烈扭曲，其体积也不会改变。这对于大多数液体来说是一个极好的近似，并且是模拟[金属塑性](@keyword=metal_plasticity|lang=zh-CN|style=Feynman)流动的基石性假设 [@problem_id:2671330]。

非对角元素，如 $d_{12}$，描述了**剪切率**。它们衡量材料线之间的角度变化速度。例如，分量 $d_{12} = \frac{1}{2}(\frac{\partial v_1}{\partial x_2} + \frac{\partial v_2}{\partial x_1})$ 量化了最初平行于 $x_1$ 和 $x_2$ 轴的两条线段之间夹角减小速率的一半 [@problem_id:2917882]。一个非零的剪切率意味着在材料中绘制的一个假想正方形正在变形为一个菱形 [@problem_id:1788899]。

即使在同时存在拉伸和剪切的复杂流动中，我们也可以问：是否存在一些特殊的方向，使得[线元](@keyword=line_element|lang=zh-CN|style=Feynman)只被拉伸而没有旋转？答案是肯定的。这些方向被称为**[主应变](@keyword=principal_strains|lang=zh-CN|style=Feynman)方向**，相应的拉伸率被称为**[主应变率](@keyword=principal_strain_rates|lang=zh-CN|style=Feynman)**。在数学上，它们是[应变率张量](@keyword=rate_of_strain_tensor|lang=zh-CN|style=Feynman) $\mathbf{d}$ 的[特征向量](@keyword=eigenvector|lang=zh-CN|style=Feynman)和[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman) [@problem_id:1490159]。这是物理学中一个优美的片段：[张量](@keyword=tensor|lang=zh-CN|style=Feynman)的抽象数学属性（其[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)和[特征向量](@keyword=eigenvector|lang=zh-CN|style=Feynman)）直接对应于变形最直观的物理方面（最大拉伸的方向和大小）。

### 应变率的真实本质

我们称 $\mathbf{d}$ 为“[应变率](@keyword=rate_of_strain|lang=zh-CN|style=Feynman)”，这强烈暗示它是某个应变量的时间[导数](@keyword=derivative|lang=zh-CN|style=Feynman)。让我们看看这是否属实。在**小变形**的世界里，位移是微小的，我们定义[无穷小应变张量](@keyword=infinitesimal_strain_tensor|lang=zh-CN|style=Feynman)为 $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^T)$，其中 $\mathbf{u}$ 是[位移场](@keyword=displacement_field|lang=zh-CN|style=Feynman)。如果我们对这个应变张量取物质时间导数（即，我们跟随一个粒子并询问其应变如何变化），我们会得到一个非常简单的结果。在小应变近似下，这个时间[导数](@keyword=derivative|lang=zh-CN|style=Feynman)恰好等于变形率[张量](@keyword=tensor|lang=zh-CN|style=Feynman)：

$$
\dot{\boldsymbol{\varepsilon}} = \mathbf{d}
$$

这个结果 [@problem_id:2917882] 是对我们直觉的一个关键检验，并证实了“[应变率](@keyword=rate_of_strain|lang=zh-CN|style=Feynman)”这个名称。

但是**大变形**的情况又如何呢？在这种情况下，物体可以发生剧烈的拉伸和扭曲。此时，[无穷小应变张量](@keyword=infinitesimal_strain_tensor|lang=zh-CN|style=Feynman)已不再适用。我们需要一个更稳健的度量，比如**右 Cauchy-Green 变形[张量](@keyword=tensor|lang=zh-CN|style=Feynman)**，$\mathbf{C} = \mathbf{F}^T \mathbf{F}$，其中 $\mathbf{F}$ 是完整的变形梯度。该[张量](@keyword=tensor|lang=zh-CN|style=Feynman)准确地测量了材料纤维长度的平方变化。它的变化率是多少？在一个真正深刻的结果中，可以证明，Cauchy-Green [张量](@keyword=tensor|lang=zh-CN|style=Feynman)的[物质时间导数](@keyword=material_time_derivative|lang=zh-CN|style=Feynman)与变形率[张量](@keyword=tensor|lang=zh-CN|style=Feynman) $\mathbf{D}$（$\mathbf{d}$ 在大变形下的对应物）直接相关：

$$
\dot{\mathbf{C}} = 2 \mathbf{F}^T \mathbf{D} \mathbf{F}
$$

而如果我们考虑相对于当前状态的应变，关系会变得更加清晰。相对 Cauchy-Green [张量](@keyword=tensor|lang=zh-CN|style=Feynman)在其计算瞬间的时间[导数](@keyword=derivative|lang=zh-CN|style=Feynman)，恰好是变形率[张量](@keyword=tensor|lang=zh-CN|style=Feynman)的两倍 [@problem_id:1536980]。这巩固了 $\mathbf{D}$ 作为应变的真正、基本的“速度计”的角色，对任何变形都有效，无论多大。

### 变形的“货币”：功与功率

所以，应变率张量告诉我们材料形状如何变化。为什么这在物理学和工程学中如此重要？因为它与力和能量密不可分。

当你使[材料变形](@keyword=material_deformation|lang=zh-CN|style=Feynman)时，你对它做了功。你做内功的速率——即功率——使材料升温、储存弹性势能或驱动[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)。事实证明，这个单位体积的内功率 $\mathcal{P}_{int}$ 由一个异常简洁的表达式给出：

$$
\mathcal{P}_{int} = \boldsymbol{\sigma} : \mathbf{d}
$$

这里，$\boldsymbol{\sigma}$ 是**Cauchy 应力张量**（内部力的真实物理度量），“:”符号表示双[点积](@keyword=dot_product|lang=zh-CN|style=Feynman)，这是一种将两个[张量](@keyword=tensor|lang=zh-CN|style=Feynman)“相乘”得到一个标量的方法。这种关系意味着应力和应变率是**[功共轭](@keyword=work_conjugacy|lang=zh-CN|style=Feynman)**的。它们形成一对。应力是连续介质的“力”，而应变率是变形的“速度”。它们的乘积就是功率。这一核心关系源于[虚功原理](@keyword=principle_of_virtual_work|lang=zh-CN|style=Feynman)，是几乎所有描述材料行为的[本构定律](@keyword=constitutive_laws|lang=zh-CN|style=Feynman)的基础 [@problem_id:2886630]。它是连接运动的运动学（$\mathbf{d}$）和力的动力学（$\boldsymbol{\sigma}$）的桥梁。

### 揭示复杂性：弹性、塑性及其他

这种[功共轭](@keyword=work_conjugacy|lang=zh-CN|style=Feynman)关系使我们有能力模拟极其复杂的材料行为。以一个金属曲别针为例。如果你轻轻弯曲它，它会弹回。这是**弹性**变形。如果你弯得太厉害，它就会保持弯曲。这是**塑性**变形。[应变率张量](@keyword=rate_of_strain_tensor|lang=zh-CN|style=Feynman)使我们能够建立一个优美的框架来描述这一点。

关键思想是，总变形是一个永久的塑性部分和一个可恢复的弹性部分的组合。在[有限变形理论](@keyword=finite_deformation_theory|lang=zh-CN|style=Feynman)中，这通过变形梯度的[乘法分解](@keyword=multiplicative_decomposition|lang=zh-CN|style=Feynman)来表示，$\mathbf{F} = \mathbf{F}^e \mathbf{F}^p$ [@problem_id:2671330]。当我们观察速率时，奇妙的事情发生了。总变形率 $\mathbf{D}$ 可以加法分解为一个弹性部分和一个塑性部分：

$$
\mathbf{D} = \mathbf{D}^e + \mathbf{D}^p
$$

现在，让我们用这个分解来考察[应力功率](@keyword=stress_power|lang=zh-CN|style=Feynman)：
$$
\mathcal{P}_{int} = \boldsymbol{\tau} : \mathbf{D} = \boldsymbol{\tau} : \mathbf{D}^e + \boldsymbol{\tau} : \mathbf{D}^p
$$
（这里我们使用 Kirchhoff 应力 $\boldsymbol{\tau}$，它是 Cauchy 应力的近亲，并且天然地与单位参考体积的 $\mathbf{D}$ [功共轭](@keyword=work_conjugacy|lang=zh-CN|style=Feynman)。）

每一项都有清晰的物理意义。项 $\boldsymbol{\tau} : \mathbf{D}^e$ 代表以可恢复的[弹性势能](@keyword=elastic_potential_energy|lang=zh-CN|style=Feynman)形式储存的功率，就像压缩弹簧中的能量一样。第二项 $\mathcal{D} = \boldsymbol{\tau} : \mathbf{D}^p$ 是**[塑性耗散](@keyword=plastic_dissipation|lang=zh-CN|style=Feynman)**。这是不可逆地以热量形式损失的功率。这就是为什么来[回弯](@keyword=backbending|lang=zh-CN|style=Feynman)曲曲别针时它会变热！[热力学第二定律](@keyword=second_law_of_thermodynamics|lang=zh-CN|style=Feynman)要求这种耗散永远不能为负，即 $\mathcal{D} \ge 0$ [@problem_id:2671330]。

从一个简单的速度梯度概念出发，我们已经深入到[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)的核心。应变率张量不仅仅是一个数学定义；它是一个基本的量，衡量着形状变化的本质，支配着能量的流动，并使我们能够区分弹性的固体和流动的塑性金属。这是物理原理统一力量的证明，展示了运动的几何学如何与力的力学和能量定律深刻而优美地联系在一起。