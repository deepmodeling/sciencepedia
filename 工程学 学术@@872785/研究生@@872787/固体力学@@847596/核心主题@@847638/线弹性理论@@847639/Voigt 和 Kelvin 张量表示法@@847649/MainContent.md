## 引言
在连续介质力学中，对称二阶张量（如应力和应变）是描述材料状态的基石。尽管[张量表示](@entry_id:180492)具有内在的物理优雅性，但在进行数值计算和工程分析时，将其转换为更易于操作的向量和矩阵形式是必不可少的。然而，这种转换并非没有代价，不同的记法约定可能导致数学上的不一致性，甚至引发错误的计算结果。本文旨在解决这一知识鸿沟，即如何选择和应用一种既实用又在数学上严谨的[张量表示法](@entry_id:272140)。

为此，我们将系统地探讨和比较两种主流的记法：Voigt记法和[Kelvin记法](@entry_id:193193)。

*   在“原理与机制”一章中，我们将深入剖析这两种记法的数学基础，揭示它们在处理[对称张量](@entry_id:148092)六维空间时的根本区别，特别是关于保持[内积](@entry_id:158127)（[Frobenius内积](@entry_id:153693)）的等距特性。
*   随后，在“应用与交叉学科联系”一章中，我们将展示这些记法如何应用于表示材料本构律、分析[材料对称性](@entry_id:190289)、执行[坐标变换](@entry_id:172727)，以及它们在[计算力学](@entry_id:174464)、有限元分析乃至数据驱动的实验力学中的核心作用。
*   最后，通过“动手实践”部分，您将有机会通过解决具体问题来巩固所学知识，亲身体验不同记法在实际计算中的细微差别和影响。

通过本文的学习，读者将能够理解Voigt和[Kelvin记法](@entry_id:193193)的优缺点，并根据具体应用场景做出明智的选择，从而在理论研究和工程实践中更准确、更高效地处理张量运算。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，对称二阶张量，如应力张量 $\boldsymbol{\sigma}$ 和[小应变张量](@entry_id:754968) $\boldsymbol{\varepsilon}$，是描述材料物理[状态和](@entry_id:193625)变形的核心数学工具。尽管这些张量在三维空间中以内蕴的、与坐标无关的形式存在，但在进行数值计算和解析推导时，将它们表示为矩阵或向量形式往往更为便捷。本章旨在系统地阐述和比较将对称[二阶张量](@entry_id:199780)及其上的线性算子（如[四阶弹性张量](@entry_id:188318)）表示为六维向量和 $6 \times 6$ 矩阵的各种记法，重点探讨 Voigt 记法和 Kelvin 记法的原理、优缺点及其在理论分析和计算中的应用。

### [对称张量](@entry_id:148092)的[向量空间](@entry_id:151108)及其维度

首先，我们考虑描述物理量的数学空间。在三维欧几里得空间 $\mathbb{R}^3$ 中，一个二阶张量 $\boldsymbol{T}$ 是一个从 $\mathbb{R}^3$ 到自身的线性映射。所有此类张量的集合构成一个[向量空间](@entry_id:151108)，记为 $L(\mathbb{R}^3, \mathbb{R}^3)$。通过选取一组基（例如[标准正交基](@entry_id:147779) $\{\boldsymbol{e}_1, \boldsymbol{e}_2, \boldsymbol{e}_3\}$），任何[二阶张量](@entry_id:199780) $\boldsymbol{T}$ 都可以唯一地由一个 $3 \times 3$ 的实数矩阵 $[T_{ij}]$ 表示，其中 $T_{ij} = \boldsymbol{e}_i \cdot (\boldsymbol{T}\boldsymbol{e}_j)$。这建立了 $L(\mathbb{R}^3, \mathbb{R}^3)$ 与 $3 \times 3$ [矩阵空间](@entry_id:261335) $\mathbb{R}^{3 \times 3}$ 之间的同构关系。因此，所有[二阶张量](@entry_id:199780)构成的[向量空间](@entry_id:151108)是九维的。

然而，在[固体力学](@entry_id:164042)中，我们主要关注的是**对称[二阶张量](@entry_id:199780)**，例如柯西[应力张量](@entry_id:148973)和[无穷小应变张量](@entry_id:167211)。一个张量 $\boldsymbol{T}$ 被称为对称的，如果它等于其[转置](@entry_id:142115)，即 $\boldsymbol{T} = \boldsymbol{T}^\top$。在任意[正交基](@entry_id:264024)下，该条件等价于其分量矩阵满足 $T_{ij} = T_{ji}$。所有对称[二阶张量](@entry_id:199780)的集合构成 $L(\mathbb{R}^3, \mathbb{R}^3)$ 的一个[子空间](@entry_id:150286)，我们称之为**对称[子空间](@entry_id:150286)**，记作 $\mathsf{Sym}$。

为了确定 $\mathsf{Sym}$ 的维度，我们只需计算一个对称 $3 \times 3$ 矩阵的独立分量数目。一个通用的 $3 \times 3$ 矩阵有 9 个分量。对称条件 $T_{12} = T_{21}$、$T_{13} = T_{31}$ 和 $T_{23} = T_{32}$ 施加了 3 个独立的约束。因此，独立分量的数量为 $9 - 3 = 6$。这些独立分量可以被看作是 3 个对角分量（$T_{11}, T_{22}, T_{33}$）和 3 个独立的非对角分量（例如，$T_{12}, T_{13}, T_{23}$）。由此可见，对称[二阶张量](@entry_id:199780)的[向量空间](@entry_id:151108) $\mathsf{Sym}$ 是一个**六维**空间 [@problem_id:2709608]。这一结论是所有将[对称张量](@entry_id:148092)表示为六维向量的记法的基础。

### Voigt 记法：一种实用但有缺陷的约定

将一个六维空间中的元素表示为一个六维向量是一种自然的想法。**Voigt 记法**正是基于这种思想，它通过将[对称张量](@entry_id:148092)的独立分量堆叠成一个列向量来实现。然而，这种堆叠的顺序并非唯一，不同的文献和软件可能采用不同的约定，例如 $(11, 22, 33, 23, 13, 12)$ 或 $(11, 22, 33, 12, 13, 23)$ 等。这种顺序的模糊性是导致不同来源之间符号或因子不一致的潜在原因之一 [@problem_id:2709609]。

更重要的是，Voigt 记法存在两种主流的变体，其区别在于如何处理剪切分量 [@problem_id:2709589]。

#### 张量 Voigt 记法 (Tensorial Voigt Notation)

这种记法直接使用张量的独立分量。以[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 和 $(11, 22, 33, 23, 13, 12)$ 顺序为例，其 Voigt 向量为：
$$
[\varepsilon]^{\mathrm{V}} = \begin{pmatrix} \varepsilon_{11} & \varepsilon_{22} & \varepsilon_{33} & \varepsilon_{23} & \varepsilon_{13} & \varepsilon_{12} \end{pmatrix}^{\mathsf T}
$$
应力张量 $\boldsymbol{\sigma}$ 的表示也遵循同样的方式。

#### 工程 Voigt 记法 (Engineering Voigt Notation)

在工程实践中，尤其是在[有限元分析](@entry_id:138109)中，更常用的是引入**工程剪切应变** $\gamma_{ij} = 2\varepsilon_{ij}$（当 $i \neq j$ 时）。采用这种定义，应变向量被写为：
$$
[\varepsilon]^{\mathrm{V, eng}} = \begin{pmatrix} \varepsilon_{11} & \varepsilon_{22} & \varepsilon_{33} & \gamma_{23} & \gamma_{13} & \gamma_{12} \end{pmatrix}^{\mathsf T} = \begin{pmatrix} \varepsilon_{11} & \varepsilon_{22} & \varepsilon_{33} & 2\varepsilon_{23} & 2\varepsilon_{13} & 2\varepsilon_{12} \end{pmatrix}^{\mathsf T}
$$
而应力向量通常不引入因子 $2$：
$$
[\sigma]^{\mathrm{V, eng}} = \begin{pmatrix} \sigma_{11} & \sigma_{22} & \sigma_{33} & \sigma_{23} & \sigma_{13} & \sigma_{12} \end{pmatrix}^{\mathsf T}
$$
这种不对称定义的动机在于它保持了**[功共轭](@entry_id:194957)**关系。单位体积的[应变能密度](@entry_id:200085) $W$（或内[功率密度](@entry_id:194407) $\dot{W}$）在张量形式下为 $W = \frac{1}{2} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}$。展开后为：
$$
W = \frac{1}{2} \left( \sigma_{11}\varepsilon_{11} + \sigma_{22}\varepsilon_{22} + \sigma_{33}\varepsilon_{33} + 2\sigma_{12}\varepsilon_{12} + 2\sigma_{13}\varepsilon_{13} + 2\sigma_{23}\varepsilon_{23} \right)
$$
使用工程 Voigt 记法，上式可以简洁地写成两个向量的[点积](@entry_id:149019)形式：
$$
W = \frac{1}{2} \left( \sigma_{11}\varepsilon_{11} + \dots + \sigma_{23}(2\varepsilon_{23}) + \dots \right) = \frac{1}{2} ([\sigma]^{\mathrm{V, eng}})^{\mathsf T} [\varepsilon]^{\mathrm{V, eng}}
$$
这种形式的便利性使得工程 Voigt 记法在数值计算中广受欢迎。当使用这种记法表示[胡克定律](@entry_id:149682) $\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}$ 时，对应的矩阵形式 $[\sigma]^{\mathrm{V, eng}} = \mathbf{C}^{\mathrm{V, eng}} [\varepsilon]^{\mathrm{V, eng}}$ 中的 $6 \times 6$ 刚度矩阵 $\mathbf{C}^{\mathrm{V, eng}}$ 的分量可以直接通过张量分量的指标替换得到，即 $C_{IJ} = C_{ijkl}$，无需引入任何额外的数值因子 [@problem_id:2615073]。例如，对于各向同性材料，剪切项的关系 $\sigma_{12} = 2G\varepsilon_{12}$ 转化为 $\sigma_{6} = G \gamma_{12} = G \varepsilon_{6}$，因此刚度矩阵中对应的对角元就是[剪切模量](@entry_id:167228) $G$ [@problem_id:2709589]。

### 等距映射的需求：Frobenius [内积](@entry_id:158127)

尽管 Voigt 记法具有实用性，但它存在一个根本性的数学缺陷：它不是一个**[等距映射](@entry_id:150881)** (isometry)。换言之，它不能保持张量空间固有的几何结构。[对称张量](@entry_id:148092)空间 $\mathsf{Sym}$ 作为一个[向量空间](@entry_id:151108)，可以装备一个自然的[内积](@entry_id:158127)，即 **Frobenius [内积](@entry_id:158127)**（也称[双点积](@entry_id:748648)）：
$$
\langle \boldsymbol{A}, \boldsymbol{B} \rangle_F = \boldsymbol{A} : \boldsymbol{B} \equiv \mathrm{tr}(\boldsymbol{A}^\top \boldsymbol{B}) = \sum_{i,j=1}^3 A_{ij} B_{ij}
$$
由于张量 $\boldsymbol{A}$ 和 $\boldsymbol{B}$ 是对称的，此[内积](@entry_id:158127)可以展开为：
$$
\langle \boldsymbol{A}, \boldsymbol{B} \rangle_F = \sum_{i=1}^3 A_{ii}B_{ii} + \sum_{i \neq j} A_{ij}B_{ij} = \sum_{i=1}^3 A_{ii}B_{ii} + 2\sum_{1 \le i \lt j \le 3} A_{ij}B_{ij}
$$
现在，我们考察张量 Voigt 向量 $[\boldsymbol{A}]^{\mathrm{V}}$ 和 $[\boldsymbol{B}]^{\mathrm{V}}$ 在 $\mathbb{R}^6$ 中的标准欧几里得[点积](@entry_id:149019)：
$$
[\boldsymbol{A}]^{\mathrm{V}} \cdot [\boldsymbol{B}]^{\mathrm{V}} = \sum_{i=1}^3 A_{ii}B_{ii} + \sum_{1 \le i \lt j \le 3} A_{ij}B_{ij}
$$
对比两个表达式可以清楚地看到，Voigt 向量的[点积](@entry_id:149019)在计算剪切项时，相比于 Frobenius [内积](@entry_id:158127)缺少了一个因子 $2$ [@problem_id:2709588]。这意味着 Voigt 映射扭曲了张量空间中的“距离”和“角度”，它不是一个保持[内积](@entry_id:158127)的等距映射。这一缺陷在进行需要保持几何结构的操作（如张量函数求导、谱分解或[坐标旋转](@entry_id:164444)）时，会引入复杂的修正因子或导致不一致性。

### Kelvin 记法：一种等距正交表示

为了克服 Voigt 记法的缺陷，我们寻求一种新的[向量表示](@entry_id:166424)法，它能保持 Frobenius [内积](@entry_id:158127)，即成为一个[等距映射](@entry_id:150881)。这个问题引导我们直接推导**Kelvin 记法**（在某些文献中也称为 **Mandel 记法**）[@problem_id:2709609]。

我们的目标是定义一个映射 $\boldsymbol{\varepsilon} \mapsto [\varepsilon]^\mathrm{K}$，使得对于任意[对称张量](@entry_id:148092) $\boldsymbol{A}$ 和 $\boldsymbol{B}$，都满足 $\langle \boldsymbol{A}, \boldsymbol{B} \rangle_F = ([\boldsymbol{A}]^\mathrm{K})^\top [\boldsymbol{B}]^\mathrm{K}$。通过对比 Frobenius [内积](@entry_id:158127)和欧几里得[点积](@entry_id:149019)的展开式，我们发现只有剪切项存在差异。为了弥补这个因子 $2$，我们必须在[向量表示](@entry_id:166424)中对剪切分量进行缩放。具体而言，如果我们将剪切分量乘以 $\sqrt{2}$，那么在[点积](@entry_id:149019)中，$(\sqrt{2}A_{ij})(\sqrt{2}B_{ij}) = 2A_{ij}B_{ij}$，正好与 Frobenius [内积](@entry_id:158127)中的项相匹配。

因此，Kelvin 向量被定义为（采用与之前相同的顺序）：
$$
[\varepsilon]^\mathrm{K} = \begin{pmatrix} \varepsilon_{11} & \varepsilon_{22} & \varepsilon_{33} & \sqrt{2}\varepsilon_{23} & \sqrt{2}\varepsilon_{13} & \sqrt{2}\varepsilon_{12} \end{pmatrix}^{\mathsf T}
$$
这个定义确保了映射的等距性。例如，对于一个只含 $\varepsilon_{12}=a$ 和 $\eta_{12}=b$ 的纯剪切张量，其 Frobenius [内积](@entry_id:158127)为 $\boldsymbol{\varepsilon}:\boldsymbol{\eta} = 2ab$，而它们的 Kelvin 向量[点积](@entry_id:149019)为 $(\sqrt{2}a)(\sqrt{2}b) = 2ab$，两者完全吻合。若不使用 $\sqrt{2}$ 因子，结果将是 $ab$，这违反了等距要求 [@problem_id:2709611]。

这个 $\sqrt{2}$ 因子的出现有更深刻的根源。一个从[内积空间](@entry_id:271570)到 $\mathbb{R}^n$ 的[等距映射](@entry_id:150881)，本质上是在该空间中选取一组**标准正交基**（orthonormal basis），并将任意元素表示为在该基下的坐标。对于[对称张量](@entry_id:148092)空间 $\mathsf{Sym}$，一组[标准正交基](@entry_id:147779)可以由以下张量构成 [@problem_id:2697058, @problem_id:2686473]：
$$
\begin{aligned}
\boldsymbol{B}_1 = \boldsymbol{e}_1 \otimes \boldsymbol{e}_1, \quad \boldsymbol{B}_2 = \boldsymbol{e}_2 \otimes \boldsymbol{e}_2, \quad \boldsymbol{B}_3 = \boldsymbol{e}_3 \otimes \boldsymbol{e}_3 \\
\boldsymbol{B}_4 = \frac{\boldsymbol{e}_2 \otimes \boldsymbol{e}_3 + \boldsymbol{e}_3 \otimes \boldsymbol{e}_2}{\sqrt{2}}, \quad \boldsymbol{B}_5 = \frac{\boldsymbol{e}_1 \otimes \boldsymbol{e}_3 + \boldsymbol{e}_3 \otimes \boldsymbol{e}_1}{\sqrt{2}}, \quad \boldsymbol{B}_6 = \frac{\boldsymbol{e}_1 \otimes \boldsymbol{e}_2 + \boldsymbol{e}_2 \otimes \boldsymbol{e}_1}{\sqrt{2}}
\end{aligned}
$$
可以验证，这些基张量在 Frobenius [内积](@entry_id:158127)下是单位正交的，即 $\boldsymbol{B}_I : \boldsymbol{B}_J = \delta_{IJ}$。任意对称张量 $\boldsymbol{\varepsilon}$ 在这组基下的坐标 $c_I = \boldsymbol{\varepsilon} : \boldsymbol{B}_I$ 恰好构成了 Kelvin 向量 $[\varepsilon]^\mathrm{K}$ [@problem_id:2709611]。例如，$c_4 = \boldsymbol{\varepsilon} : \boldsymbol{B}_4 = (\varepsilon_{23} + \varepsilon_{32})/\sqrt{2} = \sqrt{2}\varepsilon_{23}$。

张量 Voigt 向量 $[\varepsilon]^\mathrm{V}$ 和 Kelvin 向量 $[\varepsilon]^\mathrm{K}$ 之间的转换关系由一个对角矩阵 $\mathsf{T}$ 描述，即 $[\varepsilon]^{\mathrm{K}} = \mathsf{T} [\varepsilon]^{\mathrm{V}}$。根据定义，这个矩阵为 [@problem_id:2709595]：
$$
\mathsf{T} = \mathrm{diag}(1, 1, 1, \sqrt{2}, \sqrt{2}, \sqrt{2})
$$

### 对[四阶张量](@entry_id:181350)和本构律的影响

记法的选择对表示[四阶张量](@entry_id:181350)（如[弹性张量](@entry_id:170728) $\mathbb{C}$）的 $6 \times 6$ 矩阵有深远影响。一个[四阶张量](@entry_id:181350) $\mathbb{C}$ 是一个作用于对称张量空间 $\mathsf{Sym}$ 的线性算子。将此算[子表示](@entry_id:141094)为一个 $6 \times 6$ 矩阵 $\mathbf{C}$，需要首先选择 $\mathsf{Sym}$ 的一组基。不同的基（即不同的向量化记法）会得到不同的[矩阵表示](@entry_id:146025) [@problem_id:2709588]。

设 $\mathbf{C}_\mathrm{V}$ 和 $\mathbf{C}_\mathrm{K}$ 分别是[弹性张量](@entry_id:170728)在张量 Voigt 记法和 Kelvin 记法下的[矩阵表示](@entry_id:146025)。它们代表同一个[线性算子](@entry_id:149003)在不同基下的表示，因此它们之间通过一个**相似变换**相关联 [@problem_id:2709588]：
$$
\mathbf{C}_\mathrm{K} = \mathsf{T} \mathbf{C}_\mathrm{V} \mathsf{T}^{-1}
$$
其中 $\mathsf{T} = \mathrm{diag}(1, 1, 1, \sqrt{2}, \sqrt{2}, \sqrt{2})$ [@problem_id:2697058]。

Kelvin 记法的核心优势在于，由于它对应于一组[标准正交基](@entry_id:147779)，[线性算子](@entry_id:149003) $\mathbb{C}$ 的重要属性会被其[矩阵表示](@entry_id:146025) $\mathbf{C}_\mathrm{K}$ 直接继承：
1.  **对称性**：在[线性弹性](@entry_id:166983)中，[应变能](@entry_id:162699)的存在要求[弹性张量](@entry_id:170728)具有主对称性，即 $C_{ijkl} = C_{klij}$。这个性质意味着算子 $\mathbb{C}$ 是**自伴**的（self-adjoint）。当且仅当使用[标准正交基](@entry_id:147779)（即 Kelvin 记法）时，一个自伴[算子的[矩阵表](@entry_id:153664)示](@entry_id:146025)才是对称矩阵，即 $\mathbf{C}_\mathrm{K} = \mathbf{C}_\mathrm{K}^\top$。这一性质对于理论分析和[数值算法](@entry_id:752770)至关重要 [@problem_id:2709588, @problem_id:2686473, @problem_id:2709609]。
2.  **正定性**：如果[弹性张量](@entry_id:170728) $\mathbb{C}$ 是正定的（对应于[材料稳定性](@entry_id:183933)），即对所有非零应变 $\boldsymbol{\varepsilon}$，[应变能密度](@entry_id:200085) $W = \frac{1}{2}\boldsymbol{\varepsilon}:\mathbb{C}:\boldsymbol{\varepsilon} > 0$，那么其 Kelvin 矩阵 $\mathbf{C}_\mathrm{K}$ 也是一个[正定矩阵](@entry_id:155546)，其所有[特征值](@entry_id:154894)均为正 [@problem_id:2686473]。
3.  **谱分析**：算子 $\mathbb{C}$ 的[特征值](@entry_id:154894)与矩阵 $\mathbf{C}_\mathrm{K}$ 的[特征值](@entry_id:154894)完全相同。[特征向量](@entry_id:151813)之间也通过 Kelvin 映射一一对应。这使得我们可以在 $\mathbb{R}^6$ 空间中方便地进行特征分析 [@problem_id:2686473]。例如，对于[各向同性弹性](@entry_id:203237)体 $\mathbb{C}:\boldsymbol{\varepsilon} = \lambda \mathrm{tr}(\boldsymbol{\varepsilon})\mathbf{I} + 2\mu\boldsymbol{\varepsilon}$，其 Kelvin 矩阵有两个不同的[特征值](@entry_id:154894)：与体积应变（对应于张量 $\mathbf{I}$）相关的[特征值](@entry_id:154894) $3\lambda+2\mu$（多重度为 1），以及与[偏应变](@entry_id:201263)相关的[特征值](@entry_id:154894) $2\mu$（多重度为 5）。
4.  **[旋转变换](@entry_id:200017)**：在[坐标旋转](@entry_id:164444)下，张量 $\boldsymbol{T}$ 变换为 $\mathbf{Q}\boldsymbol{T}\mathbf{Q}^\top$（$\mathbf{Q}$ 为旋转矩阵）。在 Kelvin 记法下，描述此变换的 $6 \times 6$ 矩阵是正交的，因为它保持了范数（Frobenius [内积](@entry_id:158127)）。然而，在 Voigt 记法下，相应的变换矩阵通常不是正交的 [@problem_id:2709588]。

综上所述，Voigt 记法因其在特定应用（如有限元）中的便利性而被广泛使用，但其数学上的不一致性可能导致理论推导的复杂化。相比之下，Kelvin 记法通过保持空间的[内积](@entry_id:158127)结构，提供了一个严谨且一致的框架，特别适用于需要进行谱分析、[坐标变换](@entry_id:172727)和理论推导的场合。选择哪种记法取决于具体的应用需求和对数学严谨性的要求。