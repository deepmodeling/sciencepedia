## 引言
在量子力学的世界里，从描述一个孤立的粒子到描绘一个由众多相互关联的粒子构成的宇宙，我们需要一套更强大、更精妙的数学语言。当单个量子系统组合在一起时，它们所形成的复合系统展现出许多超越其各部分简单加和的奇特性质，其中最著名的便是量子纠缠。那么，我们如何从数学上精确地描述这些多体系统？我们又如何理解和运用它们所独有的[量子关联](@entry_id:136327)呢？

本文旨在系统性地解决这一知识鸿沟。我们将深入探讨描述[复合量子系统](@entry_id:193313)的基本框架——张量积形式主义。通过学习本章，您将掌握构建[多体量子系统](@entry_id:161678)[状态空间](@entry_id:177074)和算符的核心方法，并理解[量子纠缠](@entry_id:136576)这一核心概念的物理内涵与数学表达。

我们将分三个阶段展开：首先，在“原理与机制”一章中，您将学习[张量积](@entry_id:140694)的定义、[可分态与纠缠态](@entry_id:153112)的区别、复合系统算符的构造以及[全同粒子](@entry_id:142755)对称性的要求。接着，在“应用与跨学科联系”一章中，我们将展示这些抽象原理如何在量子信息、凝聚态物理、[统计力](@entry_id:194984)学等前沿领域中发挥关键作用，从而将理论与实际应用紧密联系起来。最后，“动手实践”部分将提供具体的练习，帮助您巩固所学，将理论知识转化为解决实际问题的能力。

## 原理与机制

在量子力学中，当我们从单个、孤立的系统转向由多个子系统构成的复合系统时，描述物理现实的数学框架会经历一次深刻的扩展。本章旨在阐述描述[复合量子系统](@entry_id:193313)的基本原理，并探讨由此产生的关键机制，如[量子纠缠](@entry_id:136576)、算符的构造以及[全同粒子](@entry_id:142755)系统的特殊对称性要求。

### 复合系统的[希尔伯特空间](@entry_id:261193)：张量积

描述单个量子系统的基本公设是，系统的状态由其希尔伯特空间 $\mathcal{H}$ 中的一个矢量（态矢量）所描述。那么，当我们考虑一个由两个子系统 A 和 B 组成的复合系统时，其状态空间是怎样的呢？假设子系统 A 的希尔伯特空间为 $\mathcal{H}_A$，子系统 B 的希尔伯特空间为 $\mathcal{H}_B$。量子力学的一个核心公设断言，该复合系统的总希尔伯特空间是这两个[子空间](@entry_id:150286)**张量积（tensor product）**，记为：

$$ \mathcal{H} = \mathcal{H}_A \otimes \mathcal{H}_B $$

这个构造的直接后果是，复合系统的状态空间维度是各子系统空间维度的乘积。若 $\dim(\mathcal{H}_A) = N$ 且 $\dim(\mathcal{H}_B) = M$，则 $\dim(\mathcal{H}) = N \times M$。例如，一个由两个[量子比特](@entry_id:137928)（qubit）组成的系统，每个[量子比特](@entry_id:137928)都是一个二维系统（$\dim(\mathcal{H}_{qubit}) = 2$），其复合系统的[希尔伯特空间](@entry_id:261193)维度为 $2 \times 2 = 4$。更一般地，一个系统可能包含不同种类的自由度，例如一个粒子既有自旋又有某种内部的“味”自由度。如果其自旋空间是二维的（如自旋-1/2粒子），而“味”空间是三维的，那么描述该粒子总状态的希尔伯特空间维度将是 $2 \times 3 = 6$ [@problem_id:2086849]。

如果 $\{|i\rangle_A\}_{i=1}^N$ 是 $\mathcal{H}_A$ 的一组[标准正交基](@entry_id:147779)，$\{ |j\rangle_B \}_{j=1}^M$ 是 $\mathcal{H}_B$ 的一组[标准正交基](@entry_id:147779)，那么复合空间 $\mathcal{H}$ 的一组[标准正交基](@entry_id:147779)可以通过取它们所有可能的[张量积](@entry_id:140694)来构造：$\{ |i\rangle_A \otimes |j\rangle_B \}_{i=1, j=1}^{N,M}$。为了简洁，我们通常将 $|i\rangle_A \otimes |j\rangle_B$ 缩写为 $|i, j\rangle$ 或 $|ij\rangle$。

复合系统中的任意一个纯态 $|\Psi\rangle$ 都可以表示为这组[基矢](@entry_id:199546)量的线性叠加：

$$ |\Psi\rangle = \sum_{i,j} c_{ij} |i, j\rangle $$

其中 $c_{ij}$ 是复数系数，且满足[归一化条件](@entry_id:156486) $\sum_{i,j} |c_{ij}|^2 = 1$。

#### [可分态与纠缠态](@entry_id:153112)

在复合系统的所有可能状态中，存在两类截然不同的状态：

1.  **[可分态](@entry_id:142281)（Separable States）**或**积态（Product States）**：这类状态可以写成两个子系统各自状态的张量积形式：
    $$ |\Psi\rangle = |\psi\rangle_A \otimes |\phi\rangle_B $$
    其中 $|\psi\rangle_A \in \mathcal{H}_A$ 和 $|\phi\rangle_B \in \mathcal{H}_B$。这意味着子系统 A 和 B 具有各自确定的[量子态](@entry_id:146142)。例如，考虑一个[双量子比特系统](@entry_id:203437)，其中第一个[量子比特](@entry_id:137928)处于态 $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$，第二个[量子比特](@entry_id:137928)处于态 $|-\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)$。该复合系统的总状态是一个积态 $|\Psi\rangle = |+\rangle \otimes |-\rangle$。利用张量积的[双线性性](@entry_id:146819)质，我们可以将其在计算基 $\{|00\rangle, |01\rangle, |10\rangle, |11\rangle\}$ 中展开 [@problem_id:2086846]：
    $$ |\Psi\rangle = \left(\frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)\right) \otimes \left(\frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)\right) = \frac{1}{2}(|00\rangle - |01\rangle + |10\rangle - |11\rangle) $$
    这表明，即使子系统各自处于叠加态，只要总状态可以[因式分解](@entry_id:150389)，它仍然是一个[可分态](@entry_id:142281)。

2.  **纠缠态（Entangled States）**：任何不能写成上述积态形式的复合系统状态都称为纠缠态。这些状态体现了量子力学中最非经典的特性。对于一个纠缠态，我们无法为任何一个子系统赋予一个独立的、确定的[量子态](@entry_id:146142)；相反，子系统们的状态是内在关联的，对一个子系统的测量结果会瞬间影响到另一个子系统的状态，无论它们相隔多远。典型的纠缠态例子包括贝尔态，如：
    $$ |\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle) $$
    以及
    $$ |\Psi^-\rangle = \frac{1}{\sqrt{2}}(|01\rangle - |10\rangle) $$
    在这类状态中，系数 $c_{ij}$ 的矩阵无法分解为两个向量的外积。例如，状态 $|\psi(\theta)\rangle = \cos\theta |00\rangle + \sin\theta |11\rangle$ [@problem_id:2086887] 和 $|\psi\rangle = \cos\theta |01\rangle + \sin\theta |10\rangle$ [@problem_id:2086879] 都是纠缠态，除非 $\theta$ 取特定的值（如 $0$ 或 $\pi/2$）使其中一项消失。在复合系统的希尔伯特空间中，绝大多数状态都是纠缠态。

### 复合系统上的算符

作用于复合系统希尔伯特空间 $\mathcal{H} = \mathcal{H}_A \otimes \mathcal{H}_B$ 上的线性算符也具有特定的结构。

最简单的算符是只作用于其中一个子系统的算符。例如，一个只作用于子系统 A 的算符 $\hat{O}_A$ 在复合空间中的完整形式是 $\hat{O}_A \otimes \hat{I}_B$，其中 $\hat{I}_B$ 是在子系统 B 的[希尔伯特空间](@entry_id:261193)上的恒等算符。这个算符只改变状态矢量中与 A 相关的部分，而保持 B 的部分不变。例如，在一个双粒子系统中，测量第一个粒子位置的算符应写作 $\hat{x}_1 \otimes \hat{I}_2$ [@problem_id:2086865]，而测量第一个粒子 z-方向自旋的算符则为 $\hat{S}_{1z} \otimes \hat{I}_2$ [@problem_id:2102256]。

更一般的算符可以表示为两个子系统上算符的张量积，形式为 $\hat{O}_A \otimes \hat{O}_B$。这种算符同时作用于两个子系统，通常描述了子系统间的某种联合属性或相互作用。

在许多物理情境中，系统的总[可观测量](@entry_id:267133)是各个子系统相应可观测量之和。例如，一个由两个非相互作用粒子组成的系统的总[哈密顿量](@entry_id:172864) $\hat{H}$ 是它们各自[哈密顿量](@entry_id:172864)之和。在张量积表述中，这应严谨地写为：

$$ \hat{H} = \hat{H}_1 \otimes \hat{I}_2 + \hat{I}_1 \otimes \hat{H}_2 $$

有时为了简洁，这会被缩写为 $\hat{H} = \hat{H}_1 + \hat{H}_2$ [@problem_id:2086865]。同样，一个双[粒子系统](@entry_id:180557)的总 z-方向自旋是 $\hat{S}_{z, \text{total}} = \hat{S}_{1z} \otimes \hat{I}_2 + \hat{I}_1 \otimes \hat{S}_{2z}$ [@problem_id:2086862]。

#### 矩阵表示：[克罗内克积](@entry_id:182766)

在给定了[基矢](@entry_id:199546)的情况下，算符可以表示为矩阵。[张量积](@entry_id:140694)算符 $\hat{A} \otimes \hat{B}$ 的矩阵表示可以通过**[克罗内克积](@entry_id:182766)（Kronecker product）**得到。如果 $\hat{A}$ 是一个 $m \times n$ 矩阵，$\hat{B}$ 是一个 $p \times q$ 矩阵，它们的克罗内克积 $\hat{A} \otimes \hat{B}$ 是一个 $(mp) \times (nq)$ 的[分块矩阵](@entry_id:148435)：

$$ \hat{A} \otimes \hat{B} = \begin{pmatrix} A_{11}\hat{B}  A_{12}\hat{B}  \cdots \\ A_{21}\hat{B}  A_{22}\hat{B}  \cdots \\ \vdots  \vdots  \ddots \end{pmatrix} $$

例如，要构建双[量子比特](@entry_id:137928)算符 $\hat{\sigma}_x \otimes \hat{\sigma}_y$ 在计算基 $\{|00\rangle, |01\rangle, |10\rangle, |11\rangle\}$ 下的 $4 \times 4$ 矩阵，我们使用[泡利矩阵](@entry_id:139493)的表示 [@problem_id:2086858]：

$$ \hat{\sigma}_x = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}, \quad \hat{\sigma}_y = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix} $$

$$ \hat{\sigma}_x \otimes \hat{\sigma}_y = \begin{pmatrix} 0 \cdot \hat{\sigma}_y  1 \cdot \hat{\sigma}_y \\ 1 \cdot \hat{\sigma}_y  0 \cdot \hat{\sigma}_y \end{pmatrix} = \begin{pmatrix} \begin{pmatrix} 0  0 \\ 0  0 \end{pmatrix}  \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix} \\ \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}  \begin{pmatrix} 0  0 \\ 0  0 \end{pmatrix} \end{pmatrix} = \begin{pmatrix} 0  0  0  -i \\ 0  0  i  0 \\ 0  -i  0  0 \\ i  0  0  0 \end{pmatrix} $$

这个矩阵精确地描述了 $\hat{\sigma}_x \otimes \hat{\sigma}_y$ 算符如何作用于任意一个双[量子比特](@entry_id:137928)态的系数向量。

### 测量、[期望值](@entry_id:153208)与对易关系

对于处于状态 $|\Psi\rangle$ 的复合系统，测量某个可观测量 $\hat{O}$ 的[期望值](@entry_id:153208)由 $\langle \hat{O} \rangle = \langle\Psi|\hat{O}|\Psi\rangle$ 给出。[张量积](@entry_id:140694)结构对[期望值](@entry_id:153208)的计算有重要影响。

对于一个积态 $|\Psi\rangle = |\psi\rangle_A \otimes |\phi\rangle_B$ 和一个积算符 $\hat{O} = \hat{O}_A \otimes \hat{O}_B$，[期望值](@entry_id:153208)可以分解为各个子系统[期望值](@entry_id:153208)的乘积：

$$ \langle\Psi|\hat{O}_A \otimes \hat{O}_B|\Psi\rangle = \left( \langle\psi|_A \otimes \langle\phi|_B \right) (\hat{O}_A \otimes \hat{O}_B) \left( |\psi\rangle_A \otimes |\phi\rangle_B \right) = \langle\psi|_A \hat{O}_A |\psi\rangle_A \cdot \langle\phi|_B \hat{O}_B |\phi\rangle_B $$

这个性质非常有用。例如，要计算作用于第一个粒子的算符 $\hat{S}_{1z} \otimes \hat{I}_2$ 在积态 $| \downarrow \rangle_1 \otimes |1, -1\rangle_2$ 下的[期望值](@entry_id:153208)，我们得到 $\langle \hat{S}_{1z} \rangle \langle \hat{I}_2 \rangle = \langle \hat{S}_{1z} \rangle \cdot 1$，因此问题简化为计算子系统1的[期望值](@entry_id:153208) [@problem_id:2102256]。

对于一个加和形式的算符，如 $\hat{O} = \hat{O}_A \otimes \hat{I}_B + \hat{I}_A \otimes \hat{O}_B$，其[期望值](@entry_id:153208)是各项[期望值](@entry_id:153208)之和：

$$ \langle \hat{O} \rangle = \langle\Psi|\hat{O}_A \otimes \hat{I}_B|\Psi\rangle + \langle\Psi|\hat{I}_A \otimes \hat{O}_B|\Psi\rangle $$

如果态是可分的，即 $|\Psi\rangle = |\psi\rangle_A \otimes |\phi\rangle_B$，那么这个表达式进一步简化为 $\langle \hat{O} \rangle = \langle \hat{O}_A \rangle_A + \langle \hat{O}_B \rangle_B$，即两个子系统[期望值](@entry_id:153208)的简单相加。这种简化是解决类似问题 [@problem_id:2086862] 的一个有效途径。

然而，如果系统处于一个纠缠态，这种分解通常是不可能的。必须在完整的复合系统希尔伯特空间中进行计算。例如，计算一个具有相互作用的[哈密顿量](@entry_id:172864) $H = \alpha (\sigma_x \otimes I_f) + \beta (I_s \otimes F_z)$ 在一个非[可分态](@entry_id:142281)下的[期望值](@entry_id:153208)，需要分别计算每一项，并不能将态分解 [@problem_id:2086849]。类似地，计算一个[纠缠态](@entry_id:152310) $|\psi(\theta)\rangle$ 下的联合[可观测量](@entry_id:267133) $\sigma_x \otimes \sigma_x$ 的[期望值](@entry_id:153208)，也必须直接进行计算，其结果 $\sin(2\theta)$ 清晰地展示了[期望值](@entry_id:153208)如何依赖于纠缠的程度 [@problem_id:2086887]。

#### 算符的[对易关系](@entry_id:136780)

算符的[对易关系](@entry_id:136780)决定了它们所对应的物理量是否可以同时精确测量。这个原理也适用于复合系统。对于两个[复合算符](@entry_id:152160) $\hat{\mathcal{O}}_A = \hat{A}_1 \otimes \hat{A}_2$ 和 $\hat{\mathcal{O}}_B = \hat{B}_1 \otimes \hat{B}_2$，它们的对易子可以利用 $(A \otimes B)(C \otimes D) = (AC \otimes BD)$ 的性质来计算：

$$ [\hat{\mathcal{O}}_A, \hat{\mathcal{O}}_B] = (\hat{A}_1 \otimes \hat{A}_2)(\hat{B}_1 \otimes \hat{B}_2) - (\hat{B}_1 \otimes \hat{B}_2)(\hat{A}_1 \otimes \hat{A}_2) = \hat{A}_1\hat{B}_1 \otimes \hat{A}_2\hat{B}_2 - \hat{B}_1\hat{A}_1 \otimes \hat{B}_2\hat{A}_2 $$

这个表达式并不总是能简化。然而，在一个常见的情况下，例如当其中一个算符只作用于一个子系统时，计算会变得简单。考虑算符 $\hat{\mathcal{O}}_A = \hat{S}_{1,z} \otimes \hat{I}_2$ 和 $\hat{\mathcal{O}}_B = \hat{S}_{1,x} \otimes \hat{S}_{2,x}$ [@problem_id:2086857]。它们的对易子是：

$$ [\hat{\mathcal{O}}_A, \hat{\mathcal{O}}_B] = [ \hat{S}_{1,z} \otimes \hat{I}_2, \hat{S}_{1,x} \otimes \hat{S}_{2,x} ] = (\hat{S}_{1,z} \hat{S}_{1,x}) \otimes (\hat{I}_2 \hat{S}_{2,x}) - (\hat{S}_{1,x} \hat{S}_{1,z}) \otimes (\hat{S}_{2,x} \hat{I}_2) $$
$$ = [\hat{S}_{1,z}, \hat{S}_{1,x}] \otimes \hat{S}_{2,x} = (i\hbar \hat{S}_{1,y}) \otimes \hat{S}_{2,x} = i\hbar (\hat{S}_{1,y} \otimes \hat{S}_{2,x}) $$

由于对易子不为零，这两个算符 $\hat{\mathcal{O}}_A$ 和 $\hat{\mathcal{O}}_B$ 不对易。这带来的直接物理后果是，它们所对应的物理量（粒子1的z-自旋和两粒子x-自旋的关联）不能被同时精确地测量。这也意味着，通常情况下，一个算符的本征态不会是另一个算符的[本征态](@entry_id:149904)。

### 系统动力学与专题讨论

#### [时间演化](@entry_id:153943)

复合系统的状态随时间的演化由薛定谔方程决定，其形式解为 $|\Psi(t)\rangle = \hat{U}(t) |\Psi(0)\rangle$，其中[时间演化算符](@entry_id:196774)为 $\hat{U}(t) = \exp(-i\hat{H}t/\hbar)$。

对于一个**非相互作用**的系统，[哈密顿量](@entry_id:172864)是可加的，即 $\hat{H} = \hat{H}_1 \otimes \hat{I}_2 + \hat{I}_1 \otimes \hat{H}_2$。由于 $[\hat{H}_1 \otimes \hat{I}_2, \hat{I}_1 \otimes \hat{H}_2] = 0$，指数算符可以分解：

$$ \hat{U}(t) = \exp\left(-\frac{i(\hat{H}_1 \otimes \hat{I}_2 + \hat{I}_1 \otimes \hat{H}_2)t}{\hbar}\right) = \exp\left(-\frac{i\hat{H}_1 t}{\hbar}\right) \otimes \exp\left(-\frac{i\hat{H}_2 t}{\hbar}\right) = \hat{U}_1(t) \otimes \hat{U}_2(t) $$

这意味着总的[时间演化算符](@entry_id:196774)是各个子系统[演化算符](@entry_id:182628)的张量积。其重要推论是，如果系统初始处于一个积态 $|\Psi(0)\rangle = |\psi_1(0)\rangle \otimes |\psi_2(0)\rangle$，那么在任意时刻 $t$，它将依然是一个积态：$|\Psi(t)\rangle = |\psi_1(t)\rangle \otimes |\psi_2(t)\rangle$。子系统各自独立演化，互不干扰。这极大地简化了对非相互作用[系统动力学](@entry_id:136288)的分析。例如，在计算一个非相互作用双[粒子系统](@entry_id:180557)中第一个粒子位置的[期望值](@entry_id:153208)随时间的变化时，我们完全可以忽略第二个粒子的存在，只需关注第一个粒子态的演化即可 [@problem_id:2086865]。

相反，如果[哈密顿量](@entry_id:172864)包含**[相互作用项](@entry_id:637283)**（形如 $\hat{O}_A \otimes \hat{O}_B$ 的项），则 $\hat{H}$ 通常不能写成两部分之和，[演化算符](@entry_id:182628) $\hat{U}(t)$ 也不能分解。在这种情况下，即使系统初始处于积态，[演化过程](@entry_id:175749)也会自动地将其变为纠缠态。这正是自然界中产生纠缠的主要动力学机制。

#### 全同粒子与[交换对称性](@entry_id:151892)

当复合系统由**全同粒子（identical particles）**组成时，量子力学引入了一个全新的对称性要求，即**全同性原理（symmetrization postulate）**。这意味着系统的状态矢量在交换任意两个[全同粒子](@entry_id:142755)时，必须表现出特定的对称性。

我们引入**[交换算符](@entry_id:156554)（swap operator）** $\hat{S}$，其作用是交换两个粒子的状态：$\hat{S}(|\psi\rangle \otimes |\phi\rangle) = |\phi\rangle \otimes |\psi\rangle$。由于交换两次会恢复原状（$\hat{S}^2 = \hat{I}$），[交换算符](@entry_id:156554)的[本征值](@entry_id:154894)只能是 $+1$ 和 $-1$。
*   **对称态（Symmetric States）**：$\hat{S}|\Psi\rangle_{symm} = +1 \cdot |\Psi\rangle_{symm}$
*   **反对称态（Anti-symmetric States）**：$\hat{S}|\Psi\rangle_{anti} = -1 \cdot |\Psi\rangle_{anti}$

全同性原理指出，由全同**[玻色子](@entry_id:138266)（bosons）**组成的系统，其状态必须是**对称的**；而由全同**[费米子](@entry_id:146235)（fermions）**组成的系统，其状态必须是**反对称的**。

我们可以构建[投影算符](@entry_id:154142)，将任意一个二粒子态投影到对称或反对称[子空间](@entry_id:150286)中。它们分别是：
*   对称[子空间](@entry_id:150286)[投影算符](@entry_id:154142)：$\hat{P}_{symm} = \frac{1}{2}(\hat{I} + \hat{S})$
*   反对称[子空间](@entry_id:150286)[投影算符](@entry_id:154142)：$\hat{P}_{anti} = \frac{1}{2}(\hat{I} - \hat{S})$

考虑一个初始时被制备在非对称化的积态 $|\Psi_{init}\rangle = |\psi_a\rangle \otimes |\psi_b\rangle$ 的双[粒子系统](@entry_id:180557)。如果对该系统进行一次理想的对称性测量，其被发现处于对称[子空间](@entry_id:150286)的概率由[玻恩定则](@entry_id:154470)给出：$P_{symm} = \langle \Psi_{init} | \hat{P}_{symm} | \Psi_{init} \rangle$。
进行计算 [@problem_id:2086855]：
$$ P_{symm} = \frac{1}{2} \langle \psi_a \psi_b | (\hat{I} + \hat{S}) | \psi_a \psi_b \rangle = \frac{1}{2} (\langle \psi_a \psi_b | \psi_a \psi_b \rangle + \langle \psi_a \psi_b | \hat{S} | \psi_a \psi_b \rangle) $$
$$ = \frac{1}{2} (\langle \psi_a | \psi_a \rangle \langle \psi_b | \psi_b \rangle + \langle \psi_a \psi_b | \psi_b \psi_a \rangle) = \frac{1}{2} (1 + \langle \psi_a | \psi_b \rangle \langle \psi_b | \psi_a \rangle) = \frac{1}{2}(1 + |\langle \psi_a | \psi_b \rangle|^2) $$
这个结果表明，找到系统处于对称态的概率不仅取决于态是否被正确制备，还依赖于两个单粒子态 $|\psi_a\rangle$ 和 $|\psi_b\rangle$ 之间的交叠。如果它们是正交的（$\langle \psi_a | \psi_b \rangle = 0$），概率是 $1/2$。

#### 再探纠缠：[约化密度矩阵](@entry_id:146315)与纯度

我们如何量化一个态的纠缠程度？一个强大的工具是**[约化密度矩阵](@entry_id:146315)（reduced density matrix）**。对于一个处于[纯态](@entry_id:141688) $|\Psi\rangle$ 的复合系统，其[密度矩阵](@entry_id:139892)为 $\rho = |\Psi\rangle\langle\Psi|$。如果我们只对子系统 A 感兴趣，而忽略（或说“追踪掉”）子系统 B 的信息，我们可以通过**[偏迹](@entry_id:146482)（partial trace）**运算得到 A 的[约化密度矩阵](@entry_id:146315)：

$$ \rho_A = \text{Tr}_B(\rho) = \sum_k \langle k|_B \rho |k\rangle_B $$
其中 $\{|k\rangle_B\}$ 是子系统 B 的任意一组[标准正交基](@entry_id:147779)。

[约化密度矩阵](@entry_id:146315)的性质揭示了纠缠的本质：
*   如果复合系统的总状态 $|\Psi\rangle$ 是一个**[可分态](@entry_id:142281)**，即 $|\Psi\rangle = |\psi\rangle_A \otimes |\phi\rangle_B$，那么 $\rho_A = |\psi\rangle_A \langle\psi|_A$。在这种情况下，$\rho_A$ 描述的是一个**纯态**。
*   如果总状态 $|\Psi\rangle$ 是一个**[纠缠态](@entry_id:152310)**，那么 $\rho_A$ 将描述一个**混合态（mixed state）**。这意味着，即使整个系统处于一个确定的纯态，其任何一个子系统本身却不处于任何确定的纯态。子系统的“不确定性”正是纠缠的体现。

我们可以用**纯度（purity）** $P = \text{Tr}(\rho_A^2)$ 来量化 $\rho_A$ 的混合程度。对于[纯态](@entry_id:141688)，$\rho_A^2 = \rho_A$，因此 $P=1$。对于混合态，$P  1$。纯度越低，混合程度越高，也即原复合态的纠缠程度越高。

让我们以态 $|\psi\rangle = \cos\theta |01\rangle + \sin\theta |10\rangle$ 为例来具体计算 [@problem_id:2086879]。其[密度矩阵](@entry_id:139892)为 $\rho = |\psi\rangle\langle\psi|$。对子系统 B 取[偏迹](@entry_id:146482)，我们得到 A 的[约化密度矩阵](@entry_id:146315)：
$$ \rho_A = \cos^2\theta |0\rangle\langle 0| + \sin^2\theta |1\rangle\langle 1| $$
这是一个[对角矩阵](@entry_id:637782)，其[本征值](@entry_id:154894)为 $\cos^2\theta$ 和 $\sin^2\theta$。其纯度为：
$$ P = \text{Tr}(\rho_A^2) = (\cos^2\theta)^2 + (\sin^2\theta)^2 = \cos^4\theta + \sin^4\theta = 1 - 2\sin^2\theta\cos^2\theta = 1 - \frac{1}{2}\sin^2(2\theta) $$
为了使纠缠最大化，我们需要最小化纯度 $P$。这发生在 $\sin^2(2\theta)$ 取最大值 1 时，即当 $\theta = \pi/4$ 时。此时，纯度达到最小值 $P_{min} = 1 - 1/2 = 1/2$。这对应于[贝尔态](@entry_id:140749) $|\Psi^+\rangle = \frac{1}{\sqrt{2}}(|01\rangle + |10\rangle)$，它是一个最大[纠缠态](@entry_id:152310)。这个例子清晰地展示了如何通过[约化密度矩阵](@entry_id:146315)和纯度来定量地分析和理解量子纠缠。