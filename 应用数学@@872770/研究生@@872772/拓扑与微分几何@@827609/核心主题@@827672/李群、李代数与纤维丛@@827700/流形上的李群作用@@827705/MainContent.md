## 引言
对称性是贯穿于自然科学与数学的普适性指导原则。在现代几何学与物理学中，连续对称性由李群来精确描述。当这些对称性体现在一个几何空间（即一个[光滑流形](@entry_id:160799)）上时，我们便进入了[李群](@entry_id:137659)在[流形](@entry_id:153038)上的作用这一研究领域。这一理论不仅为理解[流形](@entry_id:153038)的内在几何结构提供了强有力的工具，也构成了从经典力学中的[守恒定律](@entry_id:269268)到[量子场论](@entry_id:138177)中基本[粒子分类](@entry_id:189151)的数学基石。然而，从抽象的群公理到其在具体几何和物理问题中的深刻应用，存在着一条概念上的鸿沟。本文旨在系统地跨越这一鸿沟，为读者铺设一条从基本原理到前沿应用的清晰路径。

在接下来的内容中，我们将分三步深入探索这一宏伟的图景。首先，在“原理与机制”一章中，我们将奠定理论基础，详细阐述群作用、[轨道](@entry_id:137151)、稳定子、[商空间](@entry_id:274314)以及在[辛几何](@entry_id:160783)背景下的[矩映射](@entry_id:178341)等核心概念。随后，在“应用与交叉学科联系”一章中，我们将展示这些抽象原理如何转化为解决实际问题的锐利工具，探索其在[几何力学](@entry_id:169959)、黎曼几何结构理论以及现代[规范理论](@entry_id:142992)中的广泛应用。最后，通过“动手实践”环节，读者将有机会通过解决具体问题来巩固和深化对核心概念的理解。通过这一结构化的学习旅程，我们将揭示[李群作用](@entry_id:634789)如何成为连接代数、几何与物理的坚固桥梁。

## 原理与机制

在本章中，我们将深入探讨[李群作用](@entry_id:634789)于[流形](@entry_id:153038)的原理和核心机制。我们将从[群作用](@entry_id:268812)的基本定义开始，逐步引入[轨道](@entry_id:137151)、稳定子、基本向量场等关键概念。随后，我们将讨论如何利用[群作用](@entry_id:268812)来构造新的[流形](@entry_id:153038)（即[商空间](@entry_id:274314)），并研究这些作用在[黎曼几何](@entry_id:160508)和[辛几何](@entry_id:160783)等不同几何结构下的表现，最终引出[矩映射](@entry_id:178341)这一深刻概念。

### [李群作用](@entry_id:634789)的基本定义

[李群](@entry_id:137659)在[流形](@entry_id:153038)上的**光滑左作用** (smooth left action) 是一个[光滑映射](@entry_id:203730) $\Phi: G \times M \to M$，其中 $G$ 是一个[李群](@entry_id:137659)，$M$ 是一个光滑流形。为方便起见，我们通常将 $\Phi(g, p)$ 记作 $g \cdot p$ 或 $gp$。此映射必须满足以下两个公理：

1.  **单位元公理 (Identity)**：对于 $G$ 中的单位元 $e$，以及 $M$ 中的任意点 $p$，必须有 $e \cdot p = p$。
2.  **[相容性公理](@entry_id:138545) (Compatibility)**：对于 $G$ 中的任意两个元素 $g_1, g_2$，以及 $M$ 中的任意点 $p$，必须有 $g_1 \cdot (g_2 \cdot p) = (g_1 g_2) \cdot p$。

其中 $g_1 g_2$ 表示 $G$ 中的群乘法。

让我们通过一个具体的例子来理解这个定义。考虑二维实线性群 $GL(2, \mathbb{R})$，即所有 $2 \times 2$ 可逆实矩阵构成的李群，以及二维欧几里得平面 $M = \mathbb{R}^2$。一个很自然的作用方式是矩阵与向量的标准乘法，即 $\Phi(A, \mathbf{x}) = A\mathbf{x}$。我们可以验证这是否构成一个光滑左作用。

-   **[光滑性](@entry_id:634843)**：由于[矩阵乘法](@entry_id:156035)的每个分量都是矩阵元素和向量分量的多项式，因此该映射是光滑的。
-   **单位元**：$GL(2, \mathbb{R})$ 的单位元是单位矩阵 $I$。我们有 $I \cdot \mathbf{x} = I\mathbf{x} = \mathbf{x}$，满足单位元公理。
-   **相容性**：对于任意 $A, B \in GL(2, \mathbb{R})$，我们有 $A \cdot (B \cdot \mathbf{x}) = A(B\mathbf{x}) = (AB)\mathbf{x} = (AB) \cdot \mathbf{x}$，满足[相容性公理](@entry_id:138545)。

因此，矩阵乘法确实定义了一个光滑左作用。值得注意的是，并非任何看似合理的映射都能构成[群作用](@entry_id:268812)。例如，映射 $\Phi(A, \mathbf{x}) = A^{-1}\mathbf{x}$ 违反了[相容性公理](@entry_id:138545)，因为它会导致 $(BA)^{-1}$ 而非 $(AB)^{-1}$，这实际上定义了一个**右作用**。而映射 $\Phi(A, \mathbf{x}) = \mathbf{x} + \mathbf{v}_A$（其中 $\mathbf{v}_A$ 是 $A$ 的第一列）则违反了单位元公理。

一个作用的**忠实性** (faithfulness) 是一个重要的属性。如果唯一能在[流形](@entry_id:153038) $M$ 上“什么都不做”的群元素是单位元 $e$，那么该作用就是**忠实的**。形式上，如果 $g \cdot p = p$ 对所有 $p \in M$ 成立能够推出 $g=e$，则作用是忠实的。上面 $GL(2, \mathbb{R})$ 在 $\mathbb{R}^2$ 上的标准作用是忠实的，因为若 $A\mathbf{x} = \mathbf{x}$ 对所有 $\mathbf{x}$ 成立，则必有 $A=I$。然而，考虑另一个作用 $\Phi(A, \mathbf{x}) = (\det A)\mathbf{x}$，它满足作用的公理，但却不是忠实的。任何[行列式](@entry_id:142978)为 $1$ 的矩阵（即 $A \in SL(2, \mathbb{R})$）都会使所有点 $\mathbf{x}$ 保持不动，但这些矩阵并非都是[单位矩阵](@entry_id:156724)。

### [轨道](@entry_id:137151)与稳定子：作用的几何结构

当一个群 $G$ 作用于[流形](@entry_id:153038) $M$ 时，它会将 $M$ 分割成一系列不相交的[子集](@entry_id:261956)，称为[轨道](@entry_id:137151)。

给定一点 $p \in M$，其**[轨道](@entry_id:137151)** (orbit) 定义为该点在群 $G$ 作用下能够到达的所有点的集合：
$$
\mathcal{O}_p = G \cdot p = \{ g \cdot p \mid g \in G \}
$$
[轨道](@entry_id:137151)的概念使我们能够对作用进行分类。如果整个[流形](@entry_id:153038) $M$ 就是一个单一的[轨道](@entry_id:137151)，即对于任意两点 $p, q \in M$，都存在一个 $g \in G$ 使得 $g \cdot p = q$，那么这个作用被称为**传递的** (transitive)。此时，$M$ 也被称为**[齐性空间](@entry_id:271488)** (homogeneous space)。例如，$SO(3)$（三维旋转群）在球面 $S^2$ 上的标准作用是传递的，因为球面上任意一点都可以通过旋转到达其他任意一点。

与[轨道](@entry_id:137151)密切相关的概念是稳定子。点 $p \in M$ 的**稳定子** (stabilizer) 或**[迷向子群](@entry_id:200360)** (isotropy subgroup) 是 $G$ 中使 $p$ 保持不变的所有元素的集合：
$$
G_p = \{ g \in G \mid g \cdot p = p \}
$$
稳定子 $G_p$ 是 $G$ 的一个李[子群](@entry_id:146164)。[轨道](@entry_id:137151)与稳定子之间存在深刻的联系：[轨道](@entry_id:137151) $\mathcal{O}_p$ 微分同胚于[商空间](@entry_id:274314) $G/G_p$。这一关系引出了一个在维数计算中极为有用的基本定理——**[轨道](@entry_id:137151)-稳定子定理** (Orbit-Stabilizer Theorem)：
$$
\dim(\mathcal{O}_p) = \dim(G) - \dim(G_p)
$$
这一定理将[轨道](@entry_id:137151)这一几何对象的维度，与群和[子群](@entry_id:146164)这两个纯代数对象的维度联系了起来。

一个重要的作用类型是[李群](@entry_id:137659) $G$ 在其自身或其李代数上的**[共轭作用](@entry_id:143328)** (conjugation action)。例如，$U(n)$（$n \times n$ 幺[正矩阵](@entry_id:149490)群）可以通过[共轭作用](@entry_id:143328)于 $n \times n$ 复[矩阵空间](@entry_id:261335) $M_n(\mathbb{C})$：$(A, X) \mapsto AXA^{-1} = AXA^{\dagger}$。在这种情况下，矩阵 $X$ 的稳定子 $G_X = \{ A \in U(n) \mid AXA^{\dagger} = X \}$ 就是与 $X$ 可交换的幺[正矩阵](@entry_id:149490)集合，这也被称为 $X$ 在 $G$ 中的**[中心化子](@entry_id:146604)** (centralizer)。

让我们通过一个例子来应用[轨道](@entry_id:137151)-稳定子定理。考虑 $U(3)$ [共轭作用](@entry_id:143328)于矩阵 $X = \begin{pmatrix} \lambda  1  0 \\ 0  \lambda  0 \\ 0  0  \mu \end{pmatrix}$（其中 $\lambda \neq \mu$）。要计算其[轨道](@entry_id:137151) $\mathcal{O}_X$ 的维数，我们首先需要计算其稳定子 $G_X$ 的维数。稳定子中的元素 $A \in U(3)$ 必须满足 $AX = XA$。通过[分块矩阵](@entry_id:148435)计算可以发现，这样的 $A$ 必须是块[对角形式](@entry_id:264850) $\begin{pmatrix} M  0 \\ 0  a \end{pmatrix}$，其中 $M$ 与 $J_2(\lambda)$ 可交换，这意味着 $M$ 是一个形如 $\alpha I_2 + \beta N$ 的上三角矩阵，且 $M$ 必须是幺正的。进一步分析表明，这样的 $M$ 只能是[对角矩阵](@entry_id:637782) $\begin{pmatrix} \alpha  0 \\ 0  \alpha \end{pmatrix}$ 且 $|\alpha|=1$。因此，稳定子 $G_X$ 同构于 $U(1) \times U(1)$，其维数为 $\dim(G_X) = 1+1=2$。由于 $\dim(U(3)) = 3^2 = 9$，根据[轨道](@entry_id:137151)-稳定子定理，我们得到[轨道](@entry_id:137151)的维数 $\dim(\mathcal{O}_X) = 9 - 2 = 7$。

计算稳定子的维数通常归结为分析通勤关系，如在计算 $U(3)$ 中某个[对角矩阵](@entry_id:637782) $H$ 的中心化子维数时一样。若 $H$ 有[重根](@entry_id:151486)的[特征值](@entry_id:154894)，则通勤于 $H$ 的矩阵必须保持其特征[子空间](@entry_id:150286)，这使得该矩阵呈[块对角结构](@entry_id:746869)，其维数可以通过各块的维数之和求得。

### 无穷小作用：基本向量场

[李群作用](@entry_id:634789)是宏观的几何变换，而其在每一点的“无穷小”版本则由其[李代数](@entry_id:137954) $\mathfrak{g}$ 描述。对于[李代数](@entry_id:137954)中的任意一个元素 $X \in \mathfrak{g}$，它在[流形](@entry_id:153038) $M$ 上都诱导了一个**基本向量场** (fundamental vector field) $X_M$（有时也记作 $X^\#$）。在任意点 $p \in M$，该向量场定义为由 $X$ 生成的[单参数子群](@entry_id:181957)作用于 $p$ 所形成的曲线在该点的[切向量](@entry_id:265494)：
$$
X_M(p) = \frac{d}{dt}\bigg|_{t=0} (\exp(tX) \cdot p)
$$
这里，$\exp(tX)$ 是[李代数](@entry_id:137954)元素 $tX$ 的[指数映射](@entry_id:137184)，是 $G$ 中的一条[单参数子群](@entry_id:181957)。

基本向量场是连接李代数（[代数结构](@entry_id:137052)）和[流形](@entry_id:153038)上向量场（几何与分析结构）的桥梁。映射 $X \mapsto X_M$ 是一个李代数**反同态**，即 $[X, Y]_M = -[X_M, Y_M]$，其中前者是 $\mathfrak{g}$ 中的李括号，后者是[向量场的李括号](@entry_id:193400)。

计算基本向量场是理解无穷小作用的关键。例如，考虑李群 $SL(2, \mathbb{R})$ 通过[莫比乌斯变换](@entry_id:157570) $g \cdot z = \frac{az+b}{cz+d}$ 作用于上半平面 $\mathbb{H}$。其[李代数](@entry_id:137954) $\mathfrak{sl}(2, \mathbb{R})$ 的一组标准基是 $H = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$, $E = \begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix}$, $F = \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix}$。
-   对于 $H$，$\exp(tH) = \begin{pmatrix} e^t  0 \\ 0  e^{-t} \end{pmatrix}$，作用为 $z \mapsto e^{2t}z$。其基本向量场为 $H_M(z) = \frac{d}{dt}|_{t=0} (e^{2t}z) = 2z = 2x\frac{\partial}{\partial x} + 2y\frac{\partial}{\partial y}$。
-   对于 $E$，$\exp(tE) = \begin{pmatrix} 1  t \\ 0  1 \end{pmatrix}$，作用为 $z \mapsto z+t$。其基本向量场为 $E_M(z) = \frac{d}{dt}|_{t=0} (z+t) = 1 = \frac{\partial}{\partial x}$。
-   对于 $F$，$\exp(tF) = \begin{pmatrix} 1  0 \\ t  1 \end{pmatrix}$，作用为 $z \mapsto \frac{z}{tz+1}$。其基本向量场为 $F_M(z) = \frac{d}{dt}|_{t=0} \frac{z}{tz+1} = -z^2 = -(x^2-y^2)\frac{\partial}{\partial x} - 2xy\frac{\partial}{\partial y}$。

一旦我们获得了这些基本向量场，就可以研究它们[对流](@entry_id:141806)形上函数的无穷小作用，即**李导数** $\mathcal{L}_{X_M} f = X_M(f)$。

此外，当[流形](@entry_id:153038) $M$ 具有[黎曼度量](@entry_id:754359)时，我们可以计算基本向量场的几何性质，如其范数。例如，在[庞加莱圆盘模型](@entry_id:273836)中，$SU(1,1)$ 的作用是等距变换。对应于绕原点旋转的生成元 $X_R \in \mathfrak{su}(1,1)$，其基本向量场为 $(X_R^\#)_w = iw$。在庞加莱度量 $ds^2 = \frac{4 (du^2 + dv^2)}{(1-|w|^2)^2}$ 下，该向量场在半径为 $r_0$ 的圆上的范数为 $\lVert X_R^\# \rVert = \frac{2r_0}{1-r_0^2}$。这表明，尽管旋转在欧氏度量下是“刚性”的，但在双曲度量下，其[无穷小生成元](@entry_id:270424)的长度却依赖于它在[流形](@entry_id:153038)上的位置。

### 商空间与[齐性空间](@entry_id:271488)

群作用的一个核心应用是构造新的[流形](@entry_id:153038)。给定一个作用 $G \times M \to M$，我们可以将[轨道空间](@entry_id:148658) $M/G$——即所有[轨道](@entry_id:137151)的集合——赋予[商拓扑](@entry_id:150384)。一个自然的问题是：在什么条件下，$M/G$ 本身也是一个[光滑流形](@entry_id:160799)，并且使得典范投影 $\pi: M \to M/G$ 是一个[光滑映射](@entry_id:203730)？

答案由**[商流形定理](@entry_id:637743)** (Quotient Manifold Theorem) 给出。该定理指出，如果李群 $G$ 在[流形](@entry_id:153038) $M$ 上的光滑作用同时是**自由的** (free) 且**正则的** (proper)，那么[商空间](@entry_id:274314) $M/G$ 唯一地具有一个[光滑流形](@entry_id:160799)结构，使得投影 $\pi: M \to M/G$ 是一个光滑满射（更确切地说，是一个**淹没** (submersion)）。

-   **[自由作用](@entry_id:268835)**：作用是自由的，意味着所有稳定子都是平凡的，即 $G_p = \{e\}$ 对所有 $p \in M$ 成立。这保证了每个[轨道](@entry_id:137151) $G \cdot p$ 都与群 $G$ 本身微分同胚。这是 $M \to M/G$ 成为一个**主 $G$-丛** (principal $G$-bundle) 的必要条件。

-   **正则作用**：作用是正则的，这是一个拓扑条件，粗略地说，它防止[轨道](@entry_id:137151)在[流形](@entry_id:153038)中“无界地堆积”或“缠绕自身”。正式地，映射 $(g, p) \mapsto (p, g \cdot p)$ 是一个[正则映射](@entry_id:266266)（紧集的[原像](@entry_id:150899)是紧集）。正则性保证了[商空间](@entry_id:274314) $M/G$ 是一个豪斯多夫空间，并且允许我们构造所谓的**切片** (slices)，这是构建 $M/G$ 上[局部坐标](@entry_id:181200)卡的关键工具。

一个重要的特例是，如果作用群 $G$ 是紧的，那么任何光滑作用都是正则的。因此，[紧李群](@entry_id:146703)的[自由作用](@entry_id:268835)总能产生一个光滑的[商流形](@entry_id:190622)。

当作用是传递的时候，[流形](@entry_id:153038) $M$ 是一个[齐性空间](@entry_id:271488)，且 $M \cong G/G_p$。这时，[商流形定理](@entry_id:637743)的条件变得至关重要。例如，群 $SO^+(1,2)$ 是[路径连通](@entry_id:148704)的，但它作用的二维[双曲面](@entry_id:170736) $H = \{(t,x,y) \mid -t^2+x^2+y^2=-1\}$ 由两个不连通的叶构成。由于群是连通的，它不能将一个叶上的点映到另一个叶上，因此作用不是传递的。这揭示了一个普遍原理：如果一个连通[李群](@entry_id:137659)传递地作用于[流形](@entry_id:153038) $M$，则 $M$ 也必须是连通的。

[齐性空间](@entry_id:271488) $M=G/H$ 的几何结构可以完全由其[代数结构](@entry_id:137052)决定。例如，我们可以在 $G$ 的李代数 $\mathfrak{g}$ 上定义一个[内积](@entry_id:158127)，然后将其“投影”到商空间上，从而在 $M$ 上诱导一个[黎曼度量](@entry_id:754359)。具体而言，如果我们将 $\mathfrak{g}$ 分解为 $\mathfrak{g} = \mathfrak{h} \oplus \mathfrak{m}$（其中 $\mathfrak{h}$ 是 $H$ 的[李代数](@entry_id:137954)），并且在 $\mathfrak{m}$ 上的[内积](@entry_id:158127)在 $H$ 的伴随作用下不变，那么这个[内积](@entry_id:158127)就能在 $G/H$ 上诱导一个良定义的[黎曼度量](@entry_id:754359)。通过在 $S^2 \cong SO(3)/SO(2)$ 上执行此过程，我们可以从 $SO(3)$ 上的[左不变度量](@entry_id:637439)导出球面上的标准度量（或其常数倍），并计算其面积等几何量。

### [辛流形](@entry_id:161608)上的作用与[矩映射](@entry_id:178341)

当[李群作用](@entry_id:634789)于一个**[辛流形](@entry_id:161608)** $(M, \omega)$（即配备了一个闭的、非退化的[2-形式](@entry_id:188008) $\omega$ 的[流形](@entry_id:153038)）时，我们会遇到更为丰富的结构。如果群作用保持辛形式不变（即对任意 $g \in G$，$g^*\omega = \omega$），这个作用被称为**辛作用** (symplectic action)。

对于一类特别重要的辛作用，称为**哈密顿作用** (Hamiltonian action)，[群的对称性](@entry_id:136707)与物理中的[守恒量](@entry_id:150267)通过一个称为**[矩映射](@entry_id:178341)** (moment map) 的对象联系在一起。[矩映射](@entry_id:178341)是一个[光滑映射](@entry_id:203730) $\mu: M \to \mathfrak{g}^*$，其中 $\mathfrak{g}^*$ 是李代数 $\mathfrak{g}$ 的对偶空间。它由以下核心方程定义：
$$
d\langle \mu, \xi \rangle = -i(\xi_M)\omega
$$
对于所有的 $\xi \in \mathfrak{g}$。这里，$\langle \cdot, \cdot \rangle$ 是 $\mathfrak{g}^*$ 和 $\mathfrak{g}$ 之间的配对，$i(\xi_M)\omega$ 是辛形式 $\omega$ 与基本向量场 $\xi_M$ 的**[内积](@entry_id:158127)** (interior product)。

这个方程的含义是，对于[李代数](@entry_id:137954)中的每个元素 $\xi$，函数 $H_\xi = \langle \mu, \xi \rangle: M \to \mathbb{R}$ 的[微分](@entry_id:158718)（一个1-形式）等于由 $\xi$ 生成的无穷小流（向量场 $\xi_M$）“插入”到[辛形式](@entry_id:165896)中所产生的[1-形式](@entry_id:270392)。换句话说，$H_\xi$ 是生成该流的[哈密顿函数](@entry_id:172864)。根据诺特定理，这意味着 $H_\xi$ 是一个[守恒量](@entry_id:150267)。因此，[矩映射](@entry_id:178341)将[群的对称性](@entry_id:136707)（由 $\mathfrak{g}$ 的元素[参数化](@entry_id:272587)）与系统的守恒量（由[矩映射](@entry_id:178341)的分量给出）联系起来。

让我们从一个最基本的例子开始。考虑圆群 $G=S^1$ 在辛平面 $(\mathbb{R}^2, \omega=dx \wedge dy)$ 上的标准旋转作用。李代数 $\mathfrak{g}$ 可以等同于 $\mathbb{R}$，我们取基底 $\xi=1$。该作用生成的[单参数子群](@entry_id:181957)是绕原点的旋转，其基本向量场是 $\xi_M = -y\frac{\partial}{\partial x} + x\frac{\partial}{\partial y}$。现在我们计算[内积](@entry_id:158127)：
$$
i(\xi_M)\omega = i(-y\frac{\partial}{\partial x} + x\frac{\partial}{\partial y})(dx \wedge dy) = -y(i(\frac{\partial}{\partial x})\omega) + x(i(\frac{\partial}{\partial y})\omega) = -y(dy) + x(-dx) = -x dx - y dy
$$
根据[矩映射](@entry_id:178341)的定义，我们有 $d\mu = d\langle\mu, 1\rangle = -i(\xi_M)\omega = xdx + ydy$。这个1-形式是一个恰当形式，它是函数 $f(x,y) = \frac{1}{2}(x^2+y^2)$ 的[微分](@entry_id:158718)。因此，在相差一个常数的意义下，[矩映射](@entry_id:178341)为 $\mu(x,y) = \frac{1}{2}(x^2+y^2) = \frac{1}{2}r^2$。这正是物理中绕 $z$ 轴旋转的角动量的平方（或其分量），一个我们熟知的[守恒量](@entry_id:150267)。

这个思想可以推广。例如，考虑 $U(1)$ 在 $\mathbb{C}^2$ 上的加权作用 $\Phi_{e^{i\theta}}(z_1, z_2) = (e^{ip\theta}z_1, e^{iq\theta}z_2)$，其中 $p, q$ 是整数权重。在标准辛结构 $\omega = \frac{i}{2}(dz_1 \wedge d\bar{z}_1 + dz_2 \wedge d\bar{z}_2)$ 下，我们可以通过类似的计算，并施加[归一化条件](@entry_id:156486) $\mu(0,0)=0$，推导出其[矩映射](@entry_id:178341)为：
$$
\mu(z_1, z_2) = \frac{p|z_1|^2 + q|z_2|^2}{2}
$$
这个例子展示了作用中的权重如何直接体现在[矩映射](@entry_id:178341)（即守恒量）的表达式中。[矩映射](@entry_id:178341)在[几何量子化](@entry_id:159174)、[拓扑场论](@entry_id:191691)和[辛约化](@entry_id:170200)等领域扮演着至关重要的角色，是现代几何与物理交叉研究的基石之一。