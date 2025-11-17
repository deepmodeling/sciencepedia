## 引言
在[计算固体力学](@entry_id:169583)领域，张量不仅是描述应力、应变等物理量的数学符号，更是连接理论与计算的桥梁。然而，对于初学者而言，诸如对称性、[转置](@entry_id:142115)、迹与[行列式](@entry_id:142978)等基本概念往往显得抽象，其背后深刻的物理内涵和在数值实践中的关键作用常被忽略。本文旨在填补这一认知鸿沟，系统性地阐明这些张量属性的理论基础及其在现代[计算力学](@entry_id:174464)中的核心地位。

通过本文的学习，读者将深入理解这些基本原理如何塑造我们对材料行为的描述，[并指](@entry_id:276731)导高效、[稳健数值算法](@entry_id:754393)的设计。文章分为三个核心部分：第一章“原理和机制”将深入剖析[转置](@entry_id:142115)、迹、[行列式](@entry_id:142978)和[不变量](@entry_id:148850)的数学定义与物理解释；第二章“应用与交叉学科联系”将展示这些概念如何在构建[本构模型](@entry_id:174726)、设计数值积分格式以及连接力学与数据科学等领域中发挥关键作用；最后的“动手实践”部分则提供了一系列编程练习，帮助读者将理论知识转化为解决实际问题的计算技能。现在，让我们从这些基本原理的探索开始。

## 原理和机制

本章旨在深入探讨[二阶张量](@entry_id:199780)的基本性质及其在[计算固体力学](@entry_id:169583)中的核心作用。我们将从基本操作（如转置和迹）出发，系统地建立对称性、[行列式](@entry_id:142978)和[不变量](@entry_id:148850)等关键概念。这些概念不仅是描述[材料变形](@entry_id:169356)和应力的数学工具，也是构建本构模型和开发高效数值算法的理论基石。本章将通过一系列推导和物理解释，揭示这些抽象概念背后深刻的物理原理和计算机制。

### 基本操作与[张量分解](@entry_id:173366)

在处理描述连续体力学行为的张量时，几个基本操作构成了我们分析的起点。这些操作包括[转置](@entry_id:142115)、迹，以及基于它们定义的[对称与反对称分解](@entry_id:204005)。

**[转置](@entry_id:142115)**（Transpose）操作，对于一个二阶张量 $\mathbf{A}$，其[转置](@entry_id:142115)记为 $\mathbf{A}^T$。在任意[正交坐标](@entry_id:166074)系下，若张量 $\mathbf{A}$ 的分量为 $A_{ij}$，则其转置张量 $\mathbf{A}^T$ 的分量为 $(A^T)_{ij} = A_{ji}$。一个张量如果满足 $\mathbf{A} = \mathbf{A}^T$，则称其为**对称张量**（symmetric tensor）。若满足 $\mathbf{A} = -\mathbf{A}^T$，则称其为**[反对称张量](@entry_id:199349)**（skew-symmetric tensor）或**[斜对称张量](@entry_id:199349)**。

任意一个二阶张量 $\mathbf{A}$ 都可以唯一地分解为一个对称[部分和](@entry_id:162077)一个反对称部分之和：
$$
\mathbf{A} = \mathbf{A}^S + \mathbf{A}^A
$$
其中，对称部分 $\mathbf{A}^S$ 和反对称部分 $\mathbf{A}^A$ 分别定义为：
$$
\mathbf{A}^S = \frac{1}{2}(\mathbf{A} + \mathbf{A}^T)
$$
$$
\mathbf{A}^A = \frac{1}{2}(\mathbf{A} - \mathbf{A}^T)
$$
这个分解在[连续介质运动学](@entry_id:747813)中具有极其重要的物理意义。例如，考虑一个变形体中某物质点的速度场 $\mathbf{v}(\mathbf{x})$，其[空间速度梯度](@entry_id:187198)张量 $\mathbf{L}$ 定义为 $\mathbf{L} = \nabla \mathbf{v}$。$\mathbf{L}$ 描述了该点邻域内速度的局部变化。将 $\mathbf{L}$ 分解为其对称和反对称部分 [@problem_id:3605431]：
$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$
其中，对称部分 $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T)$ 被称为**变形率张量**（rate-of-deformation tensor）或[拉伸张量](@entry_id:193200)，它完全决定了物质微元长度和角度的改变率，即材料的变形速率。反对称部分 $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T)$ 被称为**[自旋张量](@entry_id:187346)**（spin tensor）或[涡量张量](@entry_id:189621)，它描述了物质微元作为一个刚体的瞬时平均转动速率。因此，这一数学分解清晰地将材料的纯变形与刚性转动分离开来。

**迹**（Trace）是另一个基本操作，定义为二阶张量主对角线上分量之和，记为 $\mathrm{tr}(\mathbf{A})$。对于一个 $3 \times 3$ 张量，$\mathrm{tr}(\mathbf{A}) = A_{11} + A_{22} + A_{33}$。迹是一个[线性算子](@entry_id:149003)，即 $\mathrm{tr}(\alpha \mathbf{A} + \beta \mathbf{B}) = \alpha \mathrm{tr}(\mathbf{A}) + \beta \mathrm{tr}(\mathbf{B})$。迹具有以下几个至关重要的性质 [@problem_id:3605405]：

1.  **转置[不变性](@entry_id:140168)**：[张量的迹](@entry_id:190669)与其转置的迹相等，$\mathrm{tr}(\mathbf{A}) = \mathrm{tr}(\mathbf{A}^T)$。这从定义显而易见，因为对角线元素在[转置](@entry_id:142115)操作下保持不变。

2.  **循环不变性**：对于任意两个使得乘积 $\mathbf{AB}$ 和 $\mathbf{BA}$ 均为方阵的张量 $\mathbf{A}$ 和 $\mathbf{B}$，它们的迹满足循环性质：
    $$
    \mathrm{tr}(\mathbf{AB}) = \mathrm{tr}(\mathbf{BA})
    $$
    该性质可以通过指标符号证明：
    $$
    \mathrm{tr}(\mathbf{AB}) = \sum_i (\mathbf{AB})_{ii} = \sum_i \sum_j A_{ij} B_{ji} = \sum_j \sum_i B_{ji} A_{ij} = \sum_j (\mathbf{BA})_{jj} = \mathrm{tr}(\mathbf{BA})
    $$
    这一性质可以推广到多个张量的乘积，例如 $\mathrm{tr}(\mathbf{ABC}) = \mathrm{tr}(\mathbf{BCA}) = \mathrm{tr}(\mathbf{CAB})$。这个循环性质在[计算力学](@entry_id:174464)中具有重要的实用价值。例如，在计算某个[标量不变量](@entry_id:193787)（如能量）对张量变量的导数时，常常出现形如 $\mathrm{tr}(\mathbf{ABC})$ 的项。通过循环重排张量的顺序，可以选择计算成本最低的乘法次序，从而显著提升代码执行效率 [@problem_id:3605405]。

3.  **对称与[反对称张量](@entry_id:199349)乘积的迹**：对于任意对称张量 $\mathbf{S}$ 和[反对称张量](@entry_id:199349) $\mathbf{W}$，它们的乘积的迹为零：
    $$
    \mathrm{tr}(\mathbf{SW}) = 0
    $$
    这个性质表明，[对称张量](@entry_id:148092)和[反对称张量](@entry_id:199349)在由迹定义的[Frobenius内积](@entry_id:153693)空间中是正交的。证明如下：
    $$
    \mathrm{tr}(\mathbf{SW}) = \mathrm{tr}((\mathbf{SW})^T) = \mathrm{tr}(\mathbf{W}^T \mathbf{S}^T) = \mathrm{tr}((-\mathbf{W})\mathbf{S}) = -\mathrm{tr}(\mathbf{WS}) = -\mathrm{tr}(\mathbf{SW})
    $$
    由此可得 $2 \mathrm{tr}(\mathbf{SW}) = 0$，故 $\mathrm{tr}(\mathbf{SW}) = 0$。这一性质在分解[应力功率](@entry_id:182907)等问题中非常有用。

### [行列式](@entry_id:142978)：几何与物理的诠释

[行列式](@entry_id:142978)是另一个与[二阶张量](@entry_id:199780)相关的基本标量。对于一个 $3 \times 3$ 的张量 $\mathbf{F}$，其**[行列式](@entry_id:142978)** $\det(\mathbf{F})$ 不仅仅是一个代数表达式，它具有深刻的几何意义。

从几何上看，$\det(\mathbf{F})$ 代表了[线性变换](@entry_id:149133) $\mathbf{F}$ 对**有向体积**的缩放因子 [@problem_id:3605444]。考虑一个由三个线性无关的向量 $\{\mathbf{v}_1, \mathbf{v}_2, \mathbf{v}_3\}$ 张成的平行六面体，其有向体积为 $\mathbf{v}_1 \cdot (\mathbf{v}_2 \times \mathbf{v}_3)$。经过线性变换 $\mathbf{F}$ 后，这个平行六面体被映射为由 $\{\mathbf{Fv}_1, \mathbf{Fv}_2, \mathbf{Fv}_3\}$ 张成的另一个平行六面体。新平行六面体的有向体积为：
$$
\text{Vol}_{\text{or}}(\mathbf{Fv}_1, \mathbf{Fv}_2, \mathbf{Fv}_3) = \det(\mathbf{F}) \cdot \text{Vol}_{\text{or}}(\mathbf{v}_1, \mathbf{v}_2, \mathbf{v}_3)
$$
其中，[行列式](@entry_id:142978)的符号表示了定向的改变：若 $\det(\mathbf{F}) > 0$，则保持定向（例如，保持右手法则）；若 $\det(\mathbf{F}) < 0$，则反转定向。

这个几何解释为[行列式](@entry_id:142978)最重要的性质之一——**乘法法则**——提供了直观的证明：
$$
\det(\mathbf{AB}) = \det(\mathbf{A}) \det(\mathbf{B})
$$
考虑一个单位立方体，它首先被变换 $\mathbf{B}$ 映射为一个体积为 $\det(\mathbf{B})$ 的平行六面体。随后，变换 $\mathbf{A}$ 作用于这个新的平行六面体。由于 $\mathbf{A}$ 将任意区域的[体积缩放](@entry_id:197908) $\det(\mathbf{A})$ 倍，因此最终的体积是 $(\det(\mathbf{A}))(\det(\mathbf{B}))$。而整个复合变换由 $\mathbf{AB}$ 描述，其[体积缩放因子](@entry_id:158899)就是 $\det(\mathbf{AB})$。因此，上述乘法法则成立 [@problem_id:3605444]。

在[连续介质力学](@entry_id:155125)中，**变形梯度张量** $\mathbf{F}$ 描述了从参考构型到当前构型的局部变形。其[行列式](@entry_id:142978) $J = \det(\mathbf{F})$ 被称为**[雅可比行列式](@entry_id:137120)**，它表示了局部体积的变化率，即当前构型中一个无穷小[体积元](@entry_id:267802)与参考构型中对应体积元之比。物理上，物质不能被压缩至零体积或负体积，因此一个物理上可行的变形必须满足 $J > 0$。对于连续发生的两个变形 $\mathbf{F}_1$ 和 $\mathbf{F}_2$，其总变形为 $\mathbf{F}_{tot} = \mathbf{F}_2 \mathbf{F}_1$，总体积变化率为 $J_{tot} = \det(\mathbf{F}_2 \mathbf{F}_1) = \det(\mathbf{F}_2)\det(\mathbf{F}_1) = J_2 J_1$。取对数后，我们得到 $\ln(J_{tot}) = \ln(J_1) + \ln(J_2)$，这表明对数体积应变是可加的，这一性质在许多[大变形](@entry_id:167243)[本构模型](@entry_id:174726)中被广泛应用。

当一个张量的[行列式](@entry_id:142978)为零时，即 $\det(\mathbf{F})=0$，意味着该[线性变换](@entry_id:149133)是**奇异的**（singular）。从几何上看，这意味着它将一个三维[体积元](@entry_id:267802)“压扁”成一个零体积的集合，例如一个面（如果秩为2）或一条线（如果秩为1）[@problem_id:3605416]。在 $\mathbb{R}^{3 \times 3}$ [矩阵空间](@entry_id:261335)中，所有奇异矩阵的集合在代数和拓扑上构成一个8维的子流形，它将整个9维空间分成了 $\det(\mathbf{F})>0$ 和 $\det(\mathbf{F})<0$ 两个不相连的区域。

### [不变量](@entry_id:148850)、[特征值](@entry_id:154894)与[特征方程](@entry_id:265849)

对于一个给定的[二阶张量](@entry_id:199780)，某些标量值在[坐标系](@entry_id:156346)旋转下保持不变，这些值被称为**[张量不变量](@entry_id:203254)**（tensor invariants）。对于对称[二阶张量](@entry_id:199780)（如[应力张量](@entry_id:148973)或应变张量），最重要的[不变量](@entry_id:148850)是其**[主不变量](@entry_id:193522)**（principal invariants）和**[特征值](@entry_id:154894)**（eigenvalues）。

一个二阶张量 $\mathbf{A}$ 的[特征值](@entry_id:154894) $\lambda$ 和对应的[特征向量](@entry_id:151813) $\mathbf{v}$ 满足特征方程：
$$
\mathbf{A}\mathbf{v} = \lambda\mathbf{v} \quad \text{或} \quad (\mathbf{A} - \lambda\mathbf{I})\mathbf{v} = \mathbf{0}
$$
其中 $\mathbf{I}$ 是单位张量。为使该方程有非零解 $\mathbf{v}$，[系数矩阵](@entry_id:151473) $(\mathbf{A} - \lambda\mathbf{I})$ 必须是奇异的，即其[行列式](@entry_id:142978)为零：
$$
p_A(\lambda) = \det(\mathbf{A} - \lambda\mathbf{I}) = 0
$$
这个方程被称为 $\mathbf{A}$ 的**[特征多项式](@entry_id:150909)**。对于一个 $3 \times 3$ 张量，这是一个关于 $\lambda$ 的三次多项式。通过展开[行列式](@entry_id:142978)，可以证明其一般形式为 [@problem_id:3605429]：
$$
\lambda^3 - I_1(\mathbf{A})\lambda^2 + I_2(\mathbf{A})\lambda - I_3(\mathbf{A}) = 0
$$
其中的系数 $I_1, I_2, I_3$ 就是 $\mathbf{A}$ 的三个[主不变量](@entry_id:193522)。它们可以完全由张量 $\mathbf{A}$ 的[迹和行列式](@entry_id:149685)等运算来定义：
$$
I_1(\mathbf{A}) = \mathrm{tr}(\mathbf{A})
$$
$$
I_2(\mathbf{A}) = \frac{1}{2} \left[ (\mathrm{tr}(\mathbf{A}))^2 - \mathrm{tr}(\mathbf{A}^2) \right]
$$
$$
I_3(\mathbf{A}) = \det(\mathbf{A})
$$
如果张量 $\mathbf{A}$ 的三个[特征值](@entry_id:154894)为 $\lambda_1, \lambda_2, \lambda_3$，那么[特征多项式](@entry_id:150909)也可以写为 $(\lambda - \lambda_1)(\lambda - \lambda_2)(\lambda - \lambda_3) = 0$。通过比较两种形式的[多项式系数](@entry_id:262287)，可以得到[主不变量](@entry_id:193522)与[特征值](@entry_id:154894)之间的直接关系 [@problem_id:3605425]：
$$
I_1 = \lambda_1 + \lambda_2 + \lambda_3
$$
$$
I_2 = \lambda_1\lambda_2 + \lambda_2\lambda_3 + \lambda_3\lambda_1
$$
$$
I_3 = \lambda_1\lambda_2\lambda_3
$$
对于一个对称张量，例如柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$，其[特征值](@entry_id:154894)是实数，被称为**[主应力](@entry_id:176761)**，它们代表了材料在该点受到的最大和最小[法向应力](@entry_id:260622)。[特征向量](@entry_id:151813)则指出了主应力作用的方向，即**主方向**。由于[不变量](@entry_id:148850)在[坐标变换](@entry_id:172727)下保持不变，任何以[主不变量](@entry_id:193522)表示的物理定律（例如各向同性材料的屈服准则或[应变能函数](@entry_id:178435)）都自然地满足[物质客观性原理](@entry_id:191727)。

**[Cayley-Hamilton定理](@entry_id:150551)**指出，任何一个方阵（或张量）都满足其自身的[特征方程](@entry_id:265849)。对于张量 $\mathbf{A}$，这意味着：
$$
\mathbf{A}^3 - I_1(\mathbf{A})\mathbf{A}^2 + I_2(\mathbf{A})\mathbf{A} - I_3(\mathbf{A})\mathbf{I} = \mathbf{0}
$$
这个强大的定理意味着 $\mathbf{A}$ 的任何高于二次的幂都可以表示为 $\mathbf{I}, \mathbf{A}, \mathbf{A}^2$ 的[线性组合](@entry_id:154743)，这在发展和实现本构模型的算法时极为有用 [@problem_id:3605425]。

在计算实践中，常常需要从一个已知的[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 计算其主应力。一个稳健的算法是：首先通过计算迹、平方的[迹和行列式](@entry_id:149685)来确定三个[主不变量](@entry_id:193522) $I_1, I_2, I_3$。然后，求解特征三次方程以获得三个主应力。对于保证有三个实根的对称张量，可以采用稳定的三角函数解法 [@problem_id:3605425]。例如，若已知某点应力张量的三个[不变量](@entry_id:148850)为 $I_1 = 60\,\mathrm{MPa}$, $I_2 = 1100\,\mathrm{MPa}^2$, $I_3 = 6000\,\mathrm{MPa}^3$，则其主应力是三次方程 $\lambda^3 - 60\lambda^2 + 1100\lambda - 6000 = 0$ 的根，解得主应力为 $10\,\mathrm{MPa}, 20\,\mathrm{MPa}, 30\,\mathrm{MPa}$。

### 高级主题与推广

#### 本构模型中的对称性

[张量的对称性](@entry_id:202126)在材料[本构关系](@entry_id:186508)中扮演着核心角色。在小应变线弹性理论中，[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 和[应变张量](@entry_id:193332) $\boldsymbol{\epsilon}$ 通过四阶**[弹性张量](@entry_id:170728)** $\mathbf{C}$ 相关联：$\sigma_{ij} = C_{ijkl} \epsilon_{kl}$。这个[四阶张量](@entry_id:181350)自身也具有重要的对称性 [@problem_id:3605407]：

-   **次对称性**（Minor Symmetries）：由于 $\boldsymbol{\sigma}$ 和 $\boldsymbol{\epsilon}$ 都是[对称张量](@entry_id:148092)，可以不失一般性地假定 $C_{ijkl} = C_{jikl}$ 和 $C_{ijkl} = C_{ijlk}$。这使得 $C_{ijkl}$ 的独立分量从 $3^4=81$ 个减少到 $36$ 个。

-   **主对称性**（Major Symmetry）：如果材料是超弹性的，即存在一个[应变能密度函数](@entry_id:755490) $W(\boldsymbol{\epsilon})$ 使得 $\boldsymbol{\sigma} = \partial W / \partial \boldsymbol{\epsilon}$，那么[弹性张量](@entry_id:170728)是[应变能](@entry_id:162699)的[二阶导数](@entry_id:144508)：$C_{ijkl} = \partial^2 W / (\partial \epsilon_{ij} \partial \epsilon_{kl})$。根据[混合偏导数](@entry_id:139334)的等价性，这要求 $C_{ijkl} = C_{klij}$。这一主对称性将独立分量数从 $36$ 个进一步减少到 $21$ 个，这对应于一个完全各向异性线弹性材料所需的最少弹性常数。

材料本身的晶体或微观结构对称性会施加更多约束，进一步减少独立常数的数量。例如，对于[各向同性材料](@entry_id:170678)，只有 $2$ 个独立常数；对于立方对称材料，有 $3$ 个；对于横观[各向同性材料](@entry_id:170678)，有 $5$ 个。

#### 对称性的物理基础与推广

在经典[连续介质力学](@entry_id:155125)中，柯西应力张量 $\boldsymbol{\sigma}$ 的对称性 ($\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$) 是[角动量守恒](@entry_id:156798)的直接推论。这个推论基于一个关键假设：介质中不存在独立的体偶或面偶矩 [@problem_id:3605437]。

然而，在一些**[广义连续介质理论](@entry_id:193621)**（generalized continuum theories）中，这一假设被放宽。例如，在**微极介质**（micropolar media）或**[Cosserat介质](@entry_id:747932)**理论中，物质点除了平动位移外，还被赋予了独立的[转动自由度](@entry_id:141502)。这导致了**[非对称应力张量](@entry_id:184161)**的出现。在这种理论中，[角动量守恒](@entry_id:156798)方程包含了额外的项，即**协力[应力张量](@entry_id:148973)** $\mathbf{m}$ 的散度和体偶 $\mathbf{c}$ 的贡献。局部[角动量平衡](@entry_id:181848)方程变为：
$$
\varepsilon_{ijk} \sigma_{jk} + m_{ji,j} + c_i = \rho I \ddot{\varphi}_i
$$
其中 $\varepsilon_{ijk} \sigma_{jk}$ 恰好是反对称应力部分的轴向量的两倍。此式表明，应力的反对称部分与协力应力的梯度和体偶[相平衡](@entry_id:136822)，因此 $\boldsymbol{\sigma}$ 不再必须是对称的 [@problem_id:3605437]。这些理论适用于描述具有显著微观结构的材料，如[颗粒材料](@entry_id:750005)、[复合材料](@entry_id:139856)或泡沫材料。即便在这种情况下，$\mathrm{tr}(\boldsymbol{\sigma}) = \mathrm{tr}(\boldsymbol{\sigma}^S)$ 依然成立，意味着与体积变化相关的物理量（如[静水压力](@entry_id:275365)）仍然只取决于应力的对称部分 [@problem_id:3605437]。

#### 转置的普适定义

我们通常认为转置就是交换矩阵的行和列。然而，这个操作的更深层、更普适的定义依赖于[向量空间](@entry_id:151108)中的**[内积](@entry_id:158127)**（inner product）[@problem_id:3605451]。给定一个[内积](@entry_id:158127)为 $\langle \cdot, \cdot \rangle$ 的[向量空间](@entry_id:151108) $V$，一个[线性映射](@entry_id:185132) $\mathbf{A}: V \to V$ 的**转置**（或更准确地说是**伴随**，adjoint）$\mathbf{A}^T$ 是满足以下条件的唯一线性映射：
$$
\langle \mathbf{Ax}, \mathbf{y} \rangle = \langle \mathbf{x}, \mathbf{A}^T\mathbf{y} \rangle \quad \text{对所有 } \mathbf{x}, \mathbf{y} \in V
$$
在一个非正交的基底 $\{ \mathbf{e}_i \}$ 中，[内积](@entry_id:158127)由[度规张量](@entry_id:160222) $g_{ij} = \langle \mathbf{e}_i, \mathbf{e}_j \rangle$ 决定。在这种情况下，可以推导出 $\mathbf{A}^T$ 的分量 $(A^T)^i{}_j$ 与 $\mathbf{A}$ 的分量 $A^i{}_j$ 的关系为：
$$
(A^T)^i{}_j = g^{ik} g_{jl} A^l{}_k
$$
其中 $g^{ik}$ 是[度规张量](@entry_id:160222)的逆。只有当基底是正交的，即 $g_{ij}=\delta_{ij}$ 时，这个复杂的表达式才简化为我们熟悉的 $(A^T)^i{}_j = A^j{}_i$。这个推广揭示了[转置](@entry_id:142115)操作的本质是与空间的度量结构紧密相连的，而不仅仅是一个简单的索引交换。

#### [不变量](@entry_id:148850)的导数

在计算力学中，特别是有限元方法的实现中，我们需要计算标量值张量函数对其张量宗量的导数。例如，为了推导[弹塑性](@entry_id:193198)[本构模型](@entry_id:174726)的**一致性[切线](@entry_id:268870)模量**（consistent tangent modulus），常常需要计算诸如 $J=\det(\mathbf{F})$ 这类[不变量](@entry_id:148850)的导数。

以 $J = \det(\mathbf{F})$ 为例，其对 $\mathbf{F}$ 的梯度是一个二阶张量，记为 $\partial J / \partial \mathbf{F}$。可以严格证明，这个梯度为 [@problem_id:3605417]：
$$
\frac{\partial J}{\partial \mathbf{F}} = J \mathbf{F}^{-T}
$$
其中 $\mathbf{F}^{-T}$ 代表 $\mathbf{F}$ 的逆之[转置](@entry_id:142115)。这个优美的公式，也被称为Jacobi公式，是变分力学和本构理论中的一个基石。它构成了从[应变能函数](@entry_id:178435)（通常表示为[不变量](@entry_id:148850)的函数）推导应力和[切线](@entry_id:268870)模量的基础。