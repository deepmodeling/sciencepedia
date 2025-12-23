## 引言
在[计算工程](@entry_id:178146)、物理学及现代数据科学中，我们频繁处理超越简单向量和矩阵的复杂[多维系统](@entry_id:274301)。传统的数学表示法在面对如应力状态、[材料各向异性](@entry_id:204117)或高维数据集时，很快会变得冗长且易于出错。[张量标记法](@entry_id:272140)与指标约定正是为解决这一挑战而生，它提供了一种极为高效、严谨且优美的语言来描述和操作这些多维物理量和数学结构。

本文旨在为读者构建一个关于[张量表示法](@entry_id:272140)的完整知识框架。我们将首先在“原理与机制”一章中，系统学习爱因斯坦求和约定等核心规则，理解张量的内在定义与坐标变换规律。接着，在“应用与跨学科联系”一章中，我们将探索这套语言如何贯穿于连续介质力学、相对论、[材料科学](@entry_id:152226)乃至机器学习等前沿领域，展示其强大的统一性和实用性。最后，通过“动手实践”的练习，您将有机会应用所学知识解决具体问题。

让我们从奠定基础开始，深入学习张量语言的原理与机制。

## 原理与机制

本章旨在深入探讨[张量标记法](@entry_id:272140)及其相关指标约定的基本原理与核心机制。我们将从爱因斯坦求和约定的基本规则出发，系统地建立一个严谨的框架，用于理解和操作张量这一在[计算工程](@entry_id:178146)中无处不在的数学工具。通过本章的学习，读者将能够熟练运用指标符号来表达复杂的物理和几何关系，并理解这些表达方式背后深刻的数学结构。

### [张量标记法](@entry_id:272140)的基础：爱因斯坦求和约定

在处理[多维系统](@entry_id:274301)时，传统的矩阵和[向量表示](@entry_id:166424)法很快就会变得冗长和繁琐。[张量标记法](@entry_id:272140)，特别是**爱因斯坦求和约定 (Einstein Summation Convention)**，为我们提供了一种极为高效和强大的语言。其核心思想非常简洁：**在一个单项式中，任何重复出现的指标（一个在上，一个在下，或在[笛卡尔坐标系](@entry_id:169789)下均为下标）都表示对该指标所有可能的取值进行求和。**

例如，在三维欧几里得空间中，向量 $\boldsymbol{y}$ 与 $\boldsymbol{x}$ 通过矩阵 $\boldsymbol{A}$ 的线性变换关系 $\boldsymbol{y} = \boldsymbol{A}\boldsymbol{x}$，可以写为：
$y_i = \sum_{j=1}^{3} A_{ij} x_j$
在爱因斯坦求和约定下，我们可以省略[求和符号](@entry_id:264401) $\sum$，直接写为：
$y_i = A_{ij} x_j$
这里的指标 $j$ 在右侧出现了两次，因此它是一个**[哑指标](@entry_id:188070) (dummy index)** 或**求和指标 (summation index)**，表示需要对 $j$ 从 1 到 3 进行求和。而指标 $i$ 在每一项中只出现一次，它是一个**[自由指标](@entry_id:189430) (free index)**。一个张量方程的正确性要求等号两边的[自由指标](@entry_id:189430)必须完全一致。

这些规则是如此精确和无歧义，以至于它们可以被形式化并用于构建计算机程序，以自动验证复杂的[张量缩并](@entry_id:193373)表达式。例如，一个计算程序可以解析一个形如 `"ij,jk->ik"` 的字符串，并确认其有效性。这代表了[矩阵乘法](@entry_id:156035) $C_{ik} = A_{ij} B_{jk}$。程序会识别出 $j$ 是一个[哑指标](@entry_id:188070)（在左侧出现两次），而 $i$ 和 $k$ 是[自由指标](@entry_id:189430)（在左侧各出现一次），并且[自由指标](@entry_id:189430)与右侧的 `ik` 完全匹配。相反，像 `"ijj->ij"` 这样的表达式则被视为无效，因为[哑指标](@entry_id:188070) $j$ 不应出现在表示结果的右侧 。基于此，我们可总结出以下核心规则：

1.  **[自由指标](@entry_id:189430)**: 在表达式的单项中仅出现一次的指标。它必须在等式的两边同时出现。
2.  **[哑指标](@entry_id:188070)**: 在表达式的单项中成对出现的指标，表示对该指标进行求和。[哑指标](@entry_id:188070)只是求和过程中的一个占位符，可以用任何其他未被占用的字母替换，例如 $A_{ij}x_j$ 与 $A_{ik}x_k$ 表示完全相同的运算。
3.  **有效性**: 在标准的[张量代数](@entry_id:161671)中，一个指标在一个单项中出现的次数不能超过两次。

此约定中最基本的张量是**[克罗内克δ](@entry_id:265321) (Kronecker Delta)**，记作 $\delta_{ij}$。其定义为：
$$
\delta_{ij} = \begin{cases} 1  \text{ if } i=j \\ 0  \text{ if } i \neq j \end{cases}
$$
[克罗内克δ](@entry_id:265321) 的一个关键作用是**指标替换**。例如，考虑缩并 $\delta_{ij} v_j$：
$$
\delta_{ij} v_j = \delta_{i1}v_1 + \delta_{i2}v_2 + \delta_{i3}v_3
$$
当 $i=1$ 时，上式结果为 $v_1$；当 $i=2$ 时，结果为 $v_2$，以此类推。因此，我们可以简洁地写出：
$$
\delta_{ij} v_j = v_i
$$
这个性质使得[克罗内克δ](@entry_id:265321)在张量运算中扮演着类似于[单位矩阵](@entry_id:156724)的角色。

### 张量的定义与坐标变换

虽然我们经常通过其分量来操作张量，但张量的真正定义是独立于任何特定[坐标系](@entry_id:156346)的。一个**张量 (tensor)** 是一个[多重线性映射](@entry_id:274221)，它将一组向量和/或[对偶向量](@entry_id:161217)映射到一个标量。例如，一个二阶[协变张量](@entry_id:634493) $T$ 是一个双线性函数，它接受两个向量 $\boldsymbol{u}$ 和 $\boldsymbol{v}$ 作为输入，输出一个标量 $T(\boldsymbol{u}, \boldsymbol{v})$。

张量的分量是在选定一组[基向量](@entry_id:199546) $\{\boldsymbol{e}_i\}$ 后才出现的。例如，一个三阶[协变张量](@entry_id:634493) $T$ 在此基下的分量被定义为 $T_{ijk} = T(\boldsymbol{e}_i, \boldsymbol{e}_j, \boldsymbol{e}_k)$。

张量的核心特性在于其分量在[坐标系](@entry_id:156346)变换下的特定变换规律。考虑一个从原始[坐标系](@entry_id:156346)[基向量](@entry_id:199546) $\{\boldsymbol{e}_i\}$ 到新的正交基 $\{\boldsymbol{e}'_p\}$ 的被动[旋转变换](@entry_id:200017)，其关系由一个[正交矩阵](@entry_id:169220) $Q$ 定义：$\boldsymbol{e}'_p = Q_{pi} \boldsymbol{e}_i$。新[坐标系](@entry_id:156346)下的张量分量 $T'_{pqr}$ 可以根据其定义和张量的[多重线性](@entry_id:151506)性质推导出来 ：
$$
T'_{pqr} = T(\boldsymbol{e}'_p, \boldsymbol{e}'_q, \boldsymbol{e}'_r) = T(Q_{pi}\boldsymbol{e}_i, Q_{qj}\boldsymbol{e}_j, Q_{rk}\boldsymbol{e}_k)
$$
利用 $T$ 的三线性性质，我们可以将标量系数 $Q$ 提出：
$$
T'_{pqr} = Q_{pi} Q_{qj} Q_{rk} T(\boldsymbol{e}_i, \boldsymbol{e}_j, \boldsymbol{e}_k)
$$
最终得到三阶张量的变换法则：
$$
T'_{pqr} = Q_{pi} Q_{qj} Q_{rk} T_{ijk}
$$
这个方程精确地表明，一个量之所以被称为张量，正是因为它在[坐标变换](@entry_id:172727)下遵循这样的特定规律。对于不同阶数和类型的张量（协变、逆变或混合），其变换法则会相应地包含 $Q$ 或其逆（对于正交变换即其转置 $Q^T$）的乘积。

一个实际的应用是在[计算图](@entry_id:636350)形学或机器人学中描述连续的几何变换。假设我们想对一个向量 $\boldsymbol{x}$ 先进行缩放，然后进行旋转。缩放由张量 $S$ 表示，旋转由张量 $R$ 表示。变换后的向量 $\boldsymbol{x}'$ 可以通过指标符号清晰地表达。首先，缩放操作作用于 $x_k$，得到一个中间向量 $y_j = S_{jk} x_k$。然后，[旋转操作](@entry_id:140575)作用于 $y_j$，得到最终向量 $x'_i = R_{ij} y_j$。将两者结合，我们得到复合变换：
$$
x'_i = R_{ij} (S_{jk} x_k) = R_{ij} S_{jk} x_k
$$
这表明张量乘积的顺序（从右到左）对应于几何操作的施加顺序。一般情况下，张量乘法不满足交换律，即 $R_{ij} S_{jk} \neq S_{ij} R_{jk}$，这意味着“先缩放再旋转”与“先旋转再缩放”的结果通常是不同的。然而，在一个特殊情况下，即当缩放是各向同性的（uniform scaling, $S_{ij} = s \delta_{ij}$，其中 $s$ 是一个标量），此时 $S$ 与任何张量都可交换，操作的顺序变得无关紧要 。

### 度量张量：[协变与逆变](@entry_id:189600)分量

在标准的笛卡尔坐标系中，[基向量](@entry_id:199546)是正交且归一化的，这极大地简化了计算。然而，在许多[计算工程](@entry_id:178146)问题中，如有限元方法 (FEM) 中处理不规则网格或[曲面](@entry_id:267450)时，我们必须使用**[曲线坐标系](@entry_id:172561) (curvilinear coordinates)**，其[基向量](@entry_id:199546)可能既不正交也不归一。

在这种[广义坐标](@entry_id:156576)系中，我们需要区分两种类型的[基向量](@entry_id:199546)和两种类型的向量分量。给定一组**[协变基](@entry_id:198968)向量 (covariant basis vectors)** $\{\boldsymbol{e}_i\}$，我们可以定义一组**[逆变基](@entry_id:197906)向量 (contravariant basis vectors)** 或称**对偶基 (dual basis)** $\{\boldsymbol{e}^i\}$，它们满足对偶关系：
$$
\boldsymbol{e}^i \cdot \boldsymbol{e}_j = \delta^i_j
$$
其中 $\delta^i_j$ 是[克罗内克δ](@entry_id:265321)。一个向量 $\boldsymbol{v}$ 可以用这两种[基向量](@entry_id:199546)来表示，从而得到两种分量：
1.  **协变分量 (covariant components)** $v_j$，通过将[向量投影](@entry_id:147046)到[协变基](@entry_id:198968)上得到：$v_j = \boldsymbol{v} \cdot \boldsymbol{e}_j$。
2.  **[逆变分量](@entry_id:185440) (contravariant components)** $v^i$，作为向量在[协变基](@entry_id:198968)下的展开系数：$\boldsymbol{v} = v^i \boldsymbol{e}_i$。

这两种分量之间的转换，以及描述[广义坐标](@entry_id:156576)系几何性质的核心工具，是**度量张量 (metric tensor)**。其**协变分量** $g_{ij}$ 定义为[协变基](@entry_id:198968)向量之间的[内积](@entry_id:158127)：
$$
g_{ij} = \boldsymbol{e}_i \cdot \boldsymbol{e}_j
$$
类似地，其**[逆变分量](@entry_id:185440)** $g^{ij}$ 定义为[逆变基](@entry_id:197906)向量之间的[内积](@entry_id:158127)，$g^{ij} = \boldsymbol{e}^i \cdot \boldsymbol{e}^j$。可以证明，$g^{ij}$ 构成的矩阵是 $g_{ij}$ 构成[矩阵的逆](@entry_id:140380)矩阵，即 $g^{ik} g_{kj} = \delta^i_j$。

度量张量的关键作用是“[升降指标](@entry_id:161292)”。我们可以通过与度量张量进行缩并，在协变和[逆变分量](@entry_id:185440)之间进行转换。要从[逆变分量](@entry_id:185440) $v^j$ 得到[协变](@entry_id:634097)分量 $v_i$，我们进行如下推导 ：
$$
v_i = \boldsymbol{v} \cdot \boldsymbol{e}_i = (v^j \boldsymbol{e}_j) \cdot \boldsymbol{e}_i = v^j (\boldsymbol{e}_j \cdot \boldsymbol{e}_i) = g_{ji} v^j
$$
由于度量张量是对称的 ($g_{ji}=g_{ij}$)，我们得到：
$$
v_i = g_{ij} v^j
$$
这个操作被称为**降低指标 (lowering an index)**。反之，要从协变分量 $v_j$ 得到[逆变分量](@entry_id:185440) $v^i$，我们可以用逆度量张量 $g^{ik}$ 乘以 $v_k = g_{kj} v^j$：
$$
g^{ik} v_k = g^{ik} g_{kj} v^j = \delta^i_j v^j = v^i
$$
因此，我们得到**升高指标 (raising an index)** 的法则：
$$
v^i = g^{ij} v_j
$$
在[笛卡尔坐标系](@entry_id:169789)中，[基向量](@entry_id:199546)是正交归一的，所以 $g_{ij} = \boldsymbol{e}_i \cdot \boldsymbol{e}_j = \delta_{ij}$。在这种特殊情况下，$g^{ij}$ 也等于 $\delta_{ij}$，因此 $v_i = \delta_{ij} v^j = v^i$。[协变与逆变](@entry_id:189600)分量没有区别，这就是为什么在基础物理和工程课程中通常不区分它们。然而，在[广义坐标](@entry_id:156576)和非欧空间（如广义相对论）中，这种区分至关重要。

### 工程力学中的张量运算与分解

[张量标记法](@entry_id:272140)在连续介质力学等领域显示出其巨大的威力，它能简洁地描述物质的变形和流动。一个核心概念是**[速度梯度张量](@entry_id:270928) (velocity gradient tensor)**，$L_{ij} = \frac{\partial v_i}{\partial x_j}$，它描述了[速度场](@entry_id:271461) $\boldsymbol{v}$ 在空间中的变化率。

[速度梯度张量](@entry_id:270928)可以被分解为对称和反对称两个部分，这两部分具有截然不同的物理意义：
$$
L_{ij} = \frac{1}{2}(L_{ij} + L_{ji}) + \frac{1}{2}(L_{ij} - L_{ji}) = D_{ij} + W_{ij}
$$

- **[应变率张量](@entry_id:266108) (Rate-of-Deformation Tensor)** $D_{ij}$ 是 $L_{ij}$ 的对称部分，它描述了流体微元的变形速率（伸长和剪切）。其定义为：
  $$
  D_{ij} = \frac{1}{2} \left( \frac{\partial v_i}{\partial x_j} + \frac{\partial v_j}{\partial x_i} \right)
  $$

- **[涡量张量](@entry_id:189621) (Vorticity Tensor)** $W_{ij}$ (有时也记为 $\omega_{ij}$) 是 $L_{ij}$ 的反对称部分，它描述了流体微元的刚体旋转速率。其定义为：
  $$
  W_{ij} = \frac{1}{2} \left( \frac{\partial v_i}{\partial x_j} - \frac{\partial v_j}{\partial x_i} \right)
  $$
  对于一个给定的速度场，例如 $\boldsymbol{v}(x) = (ax_2^2\exp(bx_1), c x_3\sin(dx_2), ex_1x_2^3)$，我们可以通过计算偏导数并代入上述定义，直接得到[涡量张量](@entry_id:189621)的所有分量 。

应变率张量 $D_{ij}$ 本身还可以进一步分解。其迹 $D_{kk} = D_{11} + D_{22} + D_{33}$ 等于[速度场](@entry_id:271461)的散度 $\nabla \cdot \boldsymbol{v}$，代表了单位体积的体积变化率。我们可以将 $D_{ij}$ 分解为一个**球量 (spherical)** [部分和](@entry_id:162077)一个**偏量 (deviatoric)** 部分：
$$
D_{ij} = \frac{1}{3} D_{kk} \delta_{ij} + D'_{ij}
$$
这里，第一项 $\frac{1}{3} D_{kk} \delta_{ij}$ 是一个对角矩阵，代表了各向同性的体积膨胀或收缩，被称为**[体积应变率](@entry_id:272471)**。第二项 $D'_{ij} = D_{ij} - \frac{1}{3} D_{kk} \delta_{ij}$ 是**偏应变率张量**，它是一个迹为零的张量 ($D'_{kk} = 0$)，代表了保持体积不变的形状改变（[剪切变形](@entry_id:170920)）。

在塑性力学中，材料的屈服通常与偏应力或[偏应变](@entry_id:201263)率的大小有关，而不是总应力或总应变率。因此，能够量化偏[应变率张量](@entry_id:266108)的“大小”非常重要。这是通过**[张量不变量](@entry_id:203254) (tensor invariants)** 来实现的。[不变量](@entry_id:148850)是张量分量的某种组合，其值不随[坐标系](@entry_id:156346)的旋转而改变。对于偏应变率张量，其第二[不变量](@entry_id:148850) $J_2$ 是一个关键参数，定义为：
$$
J_2 = \frac{1}{2} D'_{ij} D'_{ij} = \frac{1}{2} \sum_{i=1}^3 \sum_{j=1}^3 (D'_{ij})^2
$$
$J_2$ 正比于所有[偏应变](@entry_id:201263)率分量平方和，因此可以衡量[剪切变形](@entry_id:170920)的强度。给定一个速度场，我们可以先计算速度梯度，然后求出应变率张量 $D_{ij}$，接着分解得到其偏量部分 $D'_{ij}$，最后计算出 $J_2$ 的值 。

### [高阶张量](@entry_id:200122)的应用

虽然[二阶张量](@entry_id:199780)（如应力、应变率）在工程中最为常见，但更高阶的张量在描述材料本构关系等复杂现象时是不可或缺的。

#### [弹性张量](@entry_id:170728)与对称性

在[线性弹性](@entry_id:166983)理论中，应力张量 $\sigma_{ij}$ 和[应变张量](@entry_id:193332) $\epsilon_{kl}$ 通过一个四阶的**[弹性张量](@entry_id:170728) (elasticity tensor)** $C_{ijkl}$ 联系起来：
$$
\sigma_{ij} = C_{ijkl} \epsilon_{kl}
$$
在三维空间中，一个没有任何对称性的[四阶张量](@entry_id:181350)有 $3^4 = 81$ 个独立分量。然而，物理原理为 $C_{ijkl}$ 强加了显著的对称性，从而大大减少了独立分量的数量 。

1.  **次对称性 (Minor Symmetries)**:
    *   由于[应力张量](@entry_id:148973)是对称的（$\sigma_{ij} = \sigma_{ji}$，源于[力矩平衡](@entry_id:752138)），我们必然有 $C_{ijkl} = C_{jikl}$。
    *   由于[应变张量](@entry_id:193332)也是对称的（$\epsilon_{kl} = \epsilon_{lk}$，源于其定义），我们可以定义一个对称化的[弹性张量](@entry_id:170728)，使得 $C_{ijkl} = C_{ijlk}$ 而不改变本构关系。
    这两条次对称性意味着 $C_{ijkl}$ 在前两个指标和后两个指标上都是对称的。这使得我们可以将 $9 \times 9$ 的关系矩阵简化为一个 $6 \times 6$ 的矩阵（使用Voigt标记法），独立分量数从 $81$ 减少到 $36$。

2.  **主对称性 (Major Symmetry)**:
    如果材料存在一个[应变能密度函数](@entry_id:755490) $W(\epsilon)$，使得 $\sigma_{ij} = \frac{\partial W}{\partial \epsilon_{ij}}$，并且[本构关系](@entry_id:186508)是线性的（$W = \frac{1}{2} C_{ijkl} \epsilon_{ij} \epsilon_{kl}$），那么根据[混合偏导数的对称性](@entry_id:146941)，我们有：
    $$
    C_{ijkl} = \frac{\partial^2 W}{\partial \epsilon_{ij} \partial \epsilon_{kl}} = \frac{\partial^2 W}{\partial \epsilon_{kl} \partial \epsilon_{ij}} = C_{klij}
    $$
    这被称为主对称性。它意味着之前提到的 $6 \times 6$ 关系矩阵本身也是对称的。一个对称的 $6 \times 6$ 矩阵的独立分量数为 $\frac{6(6+1)}{2} = 21$。
因此，对于最一般的线性[弹性各向异性](@entry_id:196053)材料，其[本构关系](@entry_id:186508)仅由 $21$ 个独立的弹性常数确定。

#### [各向同性张量](@entry_id:195105)与几何解释

一个张量如果其分量在任意[坐标系](@entry_id:156346)旋转下都保持不变，则称其为**[各向同性张量](@entry_id:195105) (isotropic tensor)**。
- 零阶[各向同性张量](@entry_id:195105)是标量。
- 不存在非零的一阶[各向同性张量](@entry_id:195105)。
- 唯一的二阶[各向同性张量](@entry_id:195105)（在[比例因子](@entry_id:266678)之外）是[克罗内克δ](@entry_id:265321), $\delta_{ij}$。
- 最一般的四阶[各向同性张量](@entry_id:195105)可以表示为三个基本张量的线性组合：
  $$
  C_{ijkl} = \lambda \delta_{ij} \delta_{kl} + \mu (\delta_{ik} \delta_{jl} + \delta_{il} \delta_{jk}) + \gamma (\delta_{ik} \delta_{jl} - \delta_{il} \delta_{jk})
  $$
  其中 $\lambda, \mu, \gamma$ 是标量常数。

这些由[克罗内克δ](@entry_id:265321)构建的张量可以作为投影算子，从一个张量中提取出特定的部分。例如，我们可以构建一个[四阶张量](@entry_id:181350) $P_{ijkl}$，它能将任何二阶张量 $A_{kl}$ 投影到其对称、无迹（偏量）的部分。这个[投影算子](@entry_id:154142)本身必须是各向同性的，并且可以唯一地确定为 ：
$$
P_{ijkl} = \frac{1}{2} (\delta_{ik} \delta_{jl} + \delta_{il} \delta_{jk}) - \frac{1}{3} \delta_{ij} \delta_{kl}
$$
这里的 $\frac{1}{2}(\dots)$ 部分将 $A_{kl}$ 对称化，而 $-\frac{1}{3}\delta_{ij}\delta_{kl}$ 部分则减去了其迹的相应部分，从而得到一个对称无迹的张量。

最后，为了给抽象的二阶张量一个几何图像，我们可以考虑其定义的二次型[曲面](@entry_id:267450)。例如，类似于柯西应力二次曲面，一个对称[二阶张量](@entry_id:199780) $T_{ij}$ 可以定义一个[曲面](@entry_id:267450) $x_i T_{ij} x_j = 1$。从原点到该[曲面](@entry_id:267450)沿单位方向 $\boldsymbol{n}$ 的径向距离 $r(n)$ 可以通过代入 $x_i = r(n) n_i$ 来确定 ：
$$
(r(n) n_i) T_{ij} (r(n) n_j) = r(n)^2 (n_i T_{ij} n_j) = 1
$$
解出 $r(n)$ 得到：
$$
r(n) = \frac{1}{\sqrt{n_i T_{ij} n_j}}
$$
这个[曲面](@entry_id:267450)（通常是一个椭球）的形状和方位完全地表征了张量 $T_{ij}$。其主轴方向对应于张量的[特征向量](@entry_id:151813)，而主轴的长度则与[特征值](@entry_id:154894)相关。

### 高级主题：[客观率](@entry_id:198692)与标架无关性

在处理[大变形](@entry_id:167243)或随时间快速旋转的系统时，[连续介质力学](@entry_id:155125)的一个核心要求是**标架无关性 (frame-indifference)** 或称**客观性 (objectivity)**。这意味着材料的[本构定律](@entry_id:178936)（例如[应力与应变率](@entry_id:263123)的关系）不应依赖于观察者。一个观察者相对于另一个观察者可能在做[刚体运动](@entry_id:193355)（平移和旋转）。

一个空间二阶张量（如柯西应力 $\sigma_{ij}$）在叠加了一个由[旋转张量](@entry_id:191990) $Q_{ip}(t)$ 描述的刚体旋转后，其分量变换为 $\sigma^{*}_{ij} = Q_{ip} \sigma_{pq} Q_{jq}$。客观性要求一个张量的时间变化率（如应力率）也必须遵循同样的变换法则。然而，标准的**[物质时间导数](@entry_id:190892) (material time derivative)** $\dot{\sigma}_{ij}$ 却不满足此要求。对其变换法则求导会得到包含 $\dot{Q}$ 的额外项，破坏了客观性。

为了修正这一点，我们需要定义**[客观应力率](@entry_id:199282) (objective stress rates)**。这些“率”通过在[物质导数](@entry_id:172646)上增加一些项来抵消[坐标系](@entry_id:156346)旋转带来的非客观影响。常见的[客观率](@entry_id:198692)定义都形如：
$$
\mathring{\sigma}_{ij} = \dot{\sigma}_{ij} + \sigma_{ik} L_{kj} - L_{ik} \sigma_{kj}
$$
其中 $L$ 是某种[自旋张量](@entry_id:187346) (skew-symmetric tensor)。不同的[客观率](@entry_id:198692)选择不同的[自旋张量](@entry_id:187346) ：

- **[Jaumann 率](@entry_id:185572) (Jaumann rate)**, $\overset{\triangle}{\sigma}_{ij}$，使用[涡量张量](@entry_id:189621) $W_{ij} = \frac{1}{2}(v_{i,j} - v_{j,i})$ 作为[自旋张量](@entry_id:187346)。它测量的是应力相对于物质微元平均转动[角速度](@entry_id:192539)的变化率。
  $$
  \overset{\triangle}{\sigma}_{ij} = \dot{\sigma}_{ij} + \sigma_{ik}W_{kj} - W_{ik}\sigma_{kj}
  $$

- **Green-Naghdi 率 (Green-Naghdi rate)**, $\overset{\nabla}{\sigma}_{ij}$，使用由变形梯度 $F_{ij}$ 的极分解 $F_{ij}=R_{ik}U_{kj}$ 中[旋转张量](@entry_id:191990) $R$ 计算出的自旋 $\Omega_{ij} = \dot{R}_{ik}R_{jk}$。它测量的是应力在材料本身内禀旋转的[坐标系](@entry_id:156346)下的变化率。
  $$
  \overset{\nabla}{\sigma}_{ij} = \dot{\sigma}_{ij} + \sigma_{ik}\Omega_{kj} - \Omega_{ik}\sigma_{kj}
  $$

可以证明，这两种率以及其他类似的率都满足客观性要求，即在叠加刚体运动后，它们都遵循正确的[张量变换法则](@entry_id:185176)。在纯[刚体运动](@entry_id:193355)（即 $D_{ij}=0$）的特殊情况下，材料的[涡量](@entry_id:142747)恰好等于其内禀旋转速率（$W_{ij}=\Omega_{ij}$），此时 [Jaumann 率](@entry_id:185572)和 Green-Naghdi 率是完[全等](@entry_id:273198)价的。在[计算固体力学](@entry_id:169583)的大变形问题中，正确选择和使用[客观率](@entry_id:198692)对于获得精确和物理上一致的结果至关重要。