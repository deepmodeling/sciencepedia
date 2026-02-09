## 引言
在量子信息科学的宏伟蓝图中，由两个量子比特构成的系统扮演着基石般的角色。这些系统中最引人入胜的现象莫过于量子纠缠，而贝尔态作为最大纠缠态的典范，是理解和利用这一强大资源的出发点。然而，一个核心的挑战在于：我们如何精确地操控这些纠缠态？在实验中，最容易实现的控制是对单个量子比特进行独立操作，这些操作共同构成了局域幺正群 SU(2) x SU(2)。因此，理解这个群的作用如何影响整个系统的纠缠特性，便成为一个亟待解决的关键问题。本文旨在填补这一知识空白，通过群论和几何学的语言，系统性地揭示贝尔态在局域幺正变换下的深刻对称性。

本文将引导读者分三步深入探索这一主题。在第一章 **“原理与机制”** 中，我们将奠定坚实的数学基础，详细剖析 SU(2) x SU(2) 群的结构、其对应的李代数以及著名的嘉当分解。我们将揭示这一代数结构如何通过一个优美的同态映射，在贝尔基构成的空间中表现为四维旋转群 SO(4) 的作用，从而为纠缠演化提供一个直观的几何图像。

随后，在第二章 **“应用与交叉学科联系”** 中，我们将展示这些看似抽象的原理如何在实践中大放异彩。我们将探讨如何利用这些对称性来设计量子门、实现纠缠交换协议，并量化和表征量子纠缠。此外，我们还将触及更深层次的联系，揭示这些对称性如何与微分几何中的贝里相位、辛几何中的动量映射等概念交织在一起。

最后，在第三章 **“动手实践”** 中，您将有机会通过一系列精心设计的问题，亲手应用前两章学到的知识，将理论转化为可计算、可验证的技能，从而真正内化对这一迷人领域的理解。现在，让我们从这些变换背后的基本原理与机制开始，踏上这段探索之旅。

## 原理与机制

在双量子比特系统的研究中，其状态由四维希尔伯特空间 $\mathcal{H} = \mathbb{C}^2 \otimes \mathbb{C}^2$ 中的向量描述。对该系统最重要的变换类别之一是局域幺正操作，它构成了群 $G = SU(2) \times SU(2)$。该群的元素是张量积形式的算子 $U \otimes V$，其中 $U$ 和 $V$ 分别作用于第一个和第二个量子比特。这些操作之所以重要，是因为它们代表了实验上最容易实现的控制类型，即对单个量子比特进行任意旋转。理解这些局域操作如何影响双量子比特态，特别是如何改变它们的纠缠特性，是量子信息科学中的一个核心课题。

### 局域幺正操作与贝尔基

双量子比特系统的一个特殊且极其重要的基是贝尔基 (Bell basis)，它由四个最大纠缠态组成：
$$
|\Phi^\pm\rangle = \frac{1}{\sqrt{2}}(|00\rangle \pm |11\rangle)
$$
$$
|\Psi^\pm\rangle = \frac{1}{\sqrt{2}}(|01\rangle \pm |10\rangle)
$$
这些态是“最大纠缠”的，因为对其中一个量子比特的测量结果会完全确定另一个量子比特的测量结果（在适当的基下），尽管它们可能在空间上是分离的。贝尔态是理解双量子比特纠缠的基石。

当一个局域幺正操作 $U_A \otimes U_B \in SU(2) \times SU(2)$ 作用在一个贝尔态上时，它会将其转换为另一个（通常也是纠缠的）态。我们可以通过考察稳定子 (stabilizer) 算符的期望值来量化这种变化。例如，贝尔态 $|\Phi^+\rangle$ 是算符 $S = \sigma_z \otimes \sigma_z$ 的本征态，本征值为 $+1$。如果我们对系统施加一个操作 $U(\alpha, \beta) = e^{i\alpha\sigma_y} \otimes e^{i\beta\sigma_x}$，系统将演化到新状态 $|\psi(\alpha, \beta)\rangle = U(\alpha, \beta) |\Phi^+\rangle$。新状态下稳定子的期望值变为：
$$
E(\alpha,\beta) = \langle\psi(\alpha,\beta)| \sigma_z \otimes \sigma_z |\psi(\alpha,\beta)\rangle = \langle\Phi^+| U^\dagger(\alpha,\beta) (\sigma_z \otimes \sigma_z) U(\alpha,\beta) |\Phi^+\rangle
$$
利用 $SU(2)$ 中著名的泡利矩阵旋转公式 $e^{-i\theta \vec{n}\cdot\vec{\sigma}} (\vec{m}\cdot\vec{\sigma}) e^{i\theta \vec{n}\cdot\vec{\sigma}} = (\vec{m}_{\parallel} + \vec{m}_{\perp}\cos(2\theta) + (\vec{n}\times\vec{m})\sin(2\theta))\cdot\vec{\sigma}$，我们可以计算出变换后的算符：
$$
U^\dagger(\alpha,\beta) (\sigma_z \otimes \sigma_z) U(\alpha,\beta) = (e^{-i\alpha\sigma_y} \sigma_z e^{i\alpha\sigma_y}) \otimes (e^{-i\beta\sigma_x} \sigma_z e^{i\beta\sigma_x})
$$
对于第一个量子比特，旋转轴为 $\vec{n}=(0,1,0)$，被旋转的向量为 $\vec{m}=(0,0,1)$，旋转角为 $\alpha$。我们得到 $e^{-i\alpha\sigma_y} \sigma_z e^{i\alpha\sigma_y} = \cos(2\alpha)\sigma_z + \sin(2\alpha)\sigma_x$。对于第二个量子比特，旋转轴为 $\vec{n}=(1,0,0)$，被旋转的向量为 $\vec{m}=(0,0,1)$，旋转角为 $\beta$。我们得到 $e^{-i\beta\sigma_x} \sigma_z e^{i\beta\sigma_x} = \cos(2\beta)\sigma_z - \sin(2\beta)\sigma_y$。
由于贝尔态的性质，在计算期望值时，只有 $\sigma_z \otimes \sigma_z$ 项能够存活下来。因此，我们得到一个简洁的结果 [@problem_id:624508]：
$$
E(\alpha,\beta) = \cos(2\alpha)\cos(2\beta)
$$
这个例子清晰地表明，局域旋转改变了纠缠的特性。初始态对 $\sigma_z \otimes \sigma_z$ 的测量有确定性的结果（期望值为1），而变换后的态则具有不确定的结果，其期望值由局域旋转的角度 $\alpha$ 和 $\beta$ 决定。

### 李群与李代数结构

为了更深刻地理解这些变换的结构，我们从李群 $SU(4)$（作用于 $\mathbb{C}^4$ 的幺正算符群）及其李代数 $\mathfrak{su}(4)$ 的视角来分析。$\mathfrak{su}(4)$ 是所有 $4 \times 4$ 的反埃尔米特、无迹矩阵构成的实向量空间。局域幺正操作群 $SU(2) \times SU(2)$ 是 $SU(4)$ 的一个子群，其对应的李代数 $\mathfrak{k} = \mathfrak{su}(2) \oplus \mathfrak{su}(2)$ 是 $\mathfrak{su}(4)$ 的一个子代数。

$\mathfrak{su}(4)$ 代数（共15维）可以根据其在局域子代数 $\mathfrak{k}$（6维）下的变换性质进行分解。这个分解称为**嘉当分解 (Cartan decomposition)** $\mathfrak{su}(4) = \mathfrak{k} \oplus \mathfrak{p}$，其中 $\mathfrak{p}$ 是 $\mathfrak{k}$ 在 $\mathfrak{su}(4)$ 中的正交补（9维）。
*   **局域子代数 $\mathfrak{k}$**：由形如 $i\sigma_j \otimes I$ 和 $I \otimes i\sigma_k$ 的算子张成。这些是局域操作的无穷小生成元。
*   **非局域部分 $\mathfrak{p}$**：由形如 $i\sigma_j \otimes \sigma_k$ 的算子张成。这些生成元负责产生纠缠，因为它们不能分解为两个独立量子比特上的操作。

这个分解的代数结构由以下对易关系定义，这构成了所谓的**黎曼对称空间 (Riemannian symmetric space)** 结构：
1.  $[\mathfrak{k}, \mathfrak{k}] \subseteq \mathfrak{k}$：两个局域生成元的对易子仍然是局域的。这是因为 $\mathfrak{k}$ 本身就是一个李子代数。
2.  $[\mathfrak{k}, \mathfrak{p}] \subseteq \mathfrak{p}$：一个局域生成元和一个非局域生成元的对易子是非局域的。这表明局域操作使非局域的相互作用演化为其他非局域的相互作用。例如，我们可以计算 [@problem_id:624573]：
    $$
    [i\sigma_z \otimes I, i\sigma_x \otimes \sigma_y] = (i\sigma_z)(i\sigma_x) \otimes I\sigma_y - (i\sigma_x)(i\sigma_z) \otimes \sigma_y I = -([\sigma_z, \sigma_x] \otimes \sigma_y) = -(2i\sigma_y) \otimes \sigma_y = -2i(\sigma_y \otimes \sigma_y)
    $$
    结果 $-2i(\sigma_y \otimes \sigma_y)$ 确实是 $\mathfrak{p}$ 中的一个元素。
3.  $[\mathfrak{p}, \mathfrak{p}] \subseteq \mathfrak{k}$：两个非局域生成元的对易子令人惊讶地是局域的。这个性质在量子控制中有重要应用，因为它提供了一种通过组合非局域相互作用来合成纯局域门的方法。考虑两个非局域哈密顿量 $H_1 = i g_1 (\vec{u} \cdot \vec{\sigma}) \otimes (\vec{v} \cdot \vec{\sigma})$ 和 $H_2 = i g_2 (\vec{u} \cdot \vec{\sigma}) \otimes (\vec{w} \cdot \vec{\sigma})$，其中 $\vec{u}, \vec{v}, \vec{w}$ 是相互正交的单位向量 [@problem_id:624472]。它们的对易子为：
    $$
    [H_1, H_2] = -g_1 g_2 [(\vec{u} \cdot \vec{\sigma}) \otimes (\vec{v} \cdot \vec{\sigma}), (\vec{u} \cdot \vec{\sigma}) \otimes (\vec{w} \cdot \vec{\sigma})]
    $$
    由于 $(\vec{u} \cdot \vec{\sigma})^2 = |\vec{u}|^2 I = I$，对易子可以简化为：
    $$
    [H_1, H_2] = -g_1 g_2 (I \otimes [(\vec{v} \cdot \vec{\sigma}), (\vec{w} \cdot \vec{\sigma})]) = -g_1 g_2 (I \otimes 2i ((\vec{v} \times \vec{w}) \cdot \vec{\sigma}))
    $$
    因为 $\vec{u}, \vec{v}, \vec{w}$ 构成右手系正交基，所以 $\vec{v} \times \vec{w} = \vec{u}$。于是我们得到：
    $$
    [H_1, H_2] = -2i g_1 g_2 (I \otimes (\vec{u} \cdot \vec{\sigma}))
    $$
    这是一个纯粹作用于第二个量子比特的局域算子，属于 $\mathfrak{k}$。

### 双量子比特纠缠的几何学：$SU(2) \times SU(2)$ 与 $SO(4)$ 的对应关系

局域幺正操作 $SU(2) \times SU(2)$ 在四维贝尔基张成的空间上的作用具有深刻的几何意义。我们可以将贝尔基 $\{|\Phi^+\rangle, |\Phi^-\rangle, |\Psi^+\rangle, |\Psi^-\rangle\}$ 视为一个四维实向量空间 $V \cong \mathbb{R}^4$ 的标准正交基。一个局域幺正操作 $U \otimes V$ 作用在 $V$ 上，会引起这些基向量的线性组合，这对应于一个 $4 \times 4$ 的实矩阵变换。可以证明，这个变换是一个旋转，即属于特殊正交群 $SO(4)$。

群同态 $SU(2) \times SU(2) \to SO(4)$ 是一个二重覆盖映射，这意味着每对局域幺正操作 $(U, V)$ 对应一个唯一的四维旋转，而每个四维旋转则对应两对局域幺正操作，$(U, V)$ 和 $(-U, -V)$。这个对应关系为我们提供了一个强大的几何视角来分析纠缠的演化。

#### 矢量方法：旋转角

$SO(4)$ 中的任意旋转可以被分解为在两个相互正交的二维平面中的独立旋转，由两个特征旋转角 $\theta_1$ 和 $\theta_2$ 来刻画。这些角度与产生该旋转的 $SU(2) \times SU(2)$ 操作的参数直接相关。若将局域算子写成李代数的指数形式：
$$
U_A = \exp\left(-i \frac{\vec{\phi}_A \cdot \vec{\sigma}}{2}\right) \quad \text{和} \quad U_B = \exp\left(-i \frac{\vec{\phi}_B \cdot \vec{\sigma}}{2}\right)
$$
其中 $\vec{\phi}_A, \vec{\phi}_B \in \mathbb{R}^3$ 是旋转矢量（其方向是旋转轴，模长是旋转角）。那么对应的 $SO(4)$ 旋转的两个特征角由下式给出：
$$
\theta_1 = \frac{1}{2} |\vec{\phi}_A + \vec{\phi}_B| \quad \text{和} \quad \theta_2 = \frac{1}{2} |\vec{\phi}_A - \vec{\phi}_B|
$$
例如，考虑一个操作 $U = U_A \otimes U_B$，其中 $U_A = e^{i \alpha \sigma_x}$ 和 $U_B = e^{i \beta (\cos(\gamma) \sigma_x + \sin(\gamma) \sigma_y)}$ [@problem_id:624518]。首先，我们需要将它们与标准形式对应起来以提取 $\vec{\phi}$ 向量。
对于 $U_A = e^{i \alpha \sigma_x}$，我们有 $-i \frac{\vec{\phi}_A \cdot \vec{\sigma}}{2} = i \alpha \sigma_x$，所以 $\vec{\phi}_A = -2\alpha \hat{x} = (-2\alpha, 0, 0)$。
对于 $U_B = e^{i \beta (\cos\gamma \sigma_x + \sin\gamma \sigma_y)}$，类似地可得 $\vec{\phi}_B = -2\beta (\cos\gamma, \sin\gamma, 0)$。
然后我们可以计算向量和与向量差的模：
$$
|\vec{\phi}_A + \vec{\phi}_B|^2 = (-2\alpha - 2\beta\cos\gamma)^2 + (-2\beta\sin\gamma)^2 = 4(\alpha^2 + \beta^2 + 2\alpha\beta\cos\gamma)
$$
$$
|\vec{\phi}_A - \vec{\phi}_B|^2 = (-2\alpha + 2\beta\cos\gamma)^2 + (2\beta\sin\gamma)^2 = 4(\alpha^2 + \beta^2 - 2\alpha\beta\cos\gamma)
$$
因此，两个特征角分别为 $\theta_1 = \sqrt{\alpha^2 + \beta^2 + 2\alpha\beta\cos\gamma}$ 和 $\theta_2 = \sqrt{\alpha^2 + \beta^2 - 2\alpha\beta\cos\gamma}$。这两个角完全刻画了局域操作在贝尔空间中诱导的几何旋转。

#### 四元数方法：手性分解

理解 $SU(2) \times SU(2) \to SO(4)$ 对应的另一种等价且优雅的方法是使用四元数。我们可以将 $\mathbb{R}^4$ 中的向量 $v=(v_0, v_1, v_2, v_3)$ 等同于一个四元数 $x = v_0 + v_1 \mathbf{i} + v_2 \mathbf{j} + v_3 \mathbf{k}$。$SO(4)$ 中的一个旋转可以由一对单位四元数 $(q, p)$ 通过所谓的**双重表示 (birepresentation)** 来描述：$x \mapsto qxp^{-1}$。其中 $q$ 和 $p$ 分别被称为旋转的左手性和右手性部分。

另一方面，$SU(2)$ 群与单位四元数群同构。一个单位四元数 $q = q_0 + q_1 \mathbf{i} + q_2 \mathbf{j} + q_3 \mathbf{k}$ 可以对应一个 $SU(2)$ 矩阵，例如通过约定 $U(q) = q_0 I - i(q_1\sigma_x + q_2\sigma_y + q_3\sigma_z)$。对于一个局域操作 $U_A \otimes U_B$，与之对应的 $SO(4)$ 旋转的四元数对 $(q, p)$ 就是分别与 $U_A$ 和 $U_B$ 对应的两个四元数。

这个框架允许我们计算 $SO(4)$ 旋转矩阵 $R$ 的一些重要属性。例如，其迹可以被证明为 $\text{Tr}(R) = 4\Re(qp^{-1})$，其中 $\Re$ 表示四元数的实部 [@problem_id:624618]。考虑操作 $U_A = e^{i\alpha\sigma_y}$ 和 $U_B = e^{i\beta\sigma_z}$。
$U_A = \cos\alpha I + i\sin\alpha\sigma_y \implies q = \cos\alpha - \sin\alpha\mathbf{j}$。
$U_B = \cos\beta I + i\sin\beta\sigma_z \implies p = \cos\beta - \sin\beta\mathbf{k}$。
因此 $p^{-1} = \cos\beta + \sin\beta\mathbf{k}$。
计算 $qp^{-1}$：
$$
qp^{-1} = (\cos\alpha - \sin\alpha\mathbf{j})(\cos\beta + \sin\beta\mathbf{k}) = \cos\alpha\cos\beta - \sin\alpha\sin\beta(\mathbf{j}\mathbf{k}) - \sin\alpha\cos\beta\mathbf{j} + \cos\alpha\sin\beta\mathbf{k}
$$
使用四元数乘法规则 $\mathbf{j}\mathbf{k} = \mathbf{i}$，我们得到 $\Re(qp^{-1}) = \cos\alpha\cos\beta$。所以对应的 $SO(4)$ 矩阵的迹为 $\text{Tr}(R) = 4\cos\alpha\cos\beta$。

值得注意的是，一个算子在任何基下的迹都是不变量。因此，算子 $O = U_A \otimes U_B$ 在计算基下的迹等于其在贝尔基下的迹。在计算基下，迹的计算非常简单：
$$
\text{Tr}(O) = \text{Tr}(U_A \otimes U_B) = \text{Tr}(U_A)\text{Tr}(U_B)
$$
对于 $U_A = e^{i\alpha\sigma_y}$，其本征值为 $e^{\pm i\alpha}$，所以 $\text{Tr}(U_A) = 2\cos\alpha$。同理 $\text{Tr}(U_B) = 2\cos\beta$。因此，$\text{Tr}(O) = 4\cos\alpha\cos\beta$ [@problem_id:624497]。这与我们用四元数方法计算得到的 $SO(4)$ 矩阵的迹完全一致。这个结果优美地连接了算子的代数属性（迹）和其在贝尔空间中的几何表示。

### 表示与不变量

我们可以进一步探究贝尔空间上的 $SO(4) \cong SU(2) \times SU(2)$ 表示。李代数 $\mathfrak{so}(4)$ 的生成元可以用 $4 \times 4$ 实反对称矩阵表示。由于 $\mathfrak{so}(4) \cong \mathfrak{su}(2) \oplus \mathfrak{su}(2)$，我们可以分别写出两个 $\mathfrak{su}(2)$ 子代数的生成元。例如，其中一个 $\mathfrak{su}(2)$ 子代数的生成元可以写为 [@problem_id:624483]：
$$
T_1 = \frac{1}{2} \begin{pmatrix} 0  & 1  & 0  & 0 \\ -1 & 0  & 0  & 0 \\ 0  & 0  & 0  & -1 \\ 0  & 0  & 1  & 0 \end{pmatrix}, \quad T_2 = \frac{1}{2} \begin{pmatrix} 0  & 0  & 1  & 0 \\ 0  & 0  & 0  & 1 \\ -1 & 0  & 0  & 0 \\ 0  & -1 & 0  & 0 \end{pmatrix}, \quad T_3 = \frac{1}{2} \begin{pmatrix} 0  & 0  & 0  & 1 \\ 0  & 0  & -1 & 0 \\ 0  & 1  & 0  & 0 \\ -1 & 0  & 0  & 0 \end{pmatrix}
$$
对于一个李代数表示，一个重要的不变量是**二次卡西米尔算子 (quadratic Casimir operator)**，定义为 $C = -\sum_{k} T_k^2$。根据舒尔引理，对于不可约表示，卡西米尔算子是一个与单位矩阵成比例的常数，这个常数值 $c_2$ 标志着该表示。
对于上述生成元，我们可以计算出 $T_k^2 = -\frac{1}{4}I_4$。因此：
$$
C = - \sum_{k=1}^3 T_k^2 = -3 \left(-\frac{1}{4}I_4\right) = \frac{3}{4}I_4
$$
卡西米尔值为 $c_2 = 3/4$。在 $\mathfrak{su}(2)$ 的表示论中，自旋为 $j$ 的不可约表示的卡西米尔值为 $j(j+1)$。因此，$c_2 = 3/4$ 对应于 $j=1/2$（即 $\frac{1}{2}(\frac{1}{2}+1) = \frac{3}{4}$），也就是基本表示。这揭示了每个 $\mathfrak{su}(2)$ 因子在四维贝尔空间上的作用是两个自旋-1/2 表示的直和。

非局域算子 $Y \in \mathfrak{p}$ 虽然不属于 $\mathfrak{so}(4)$ 代数，但它可以通过伴随作用 $[Y, \cdot]$ 对 $\mathfrak{so}(4)$ 的元素进行变换。更有趣的是，二次伴随作用 $\mathcal{M}_Y(X) = [Y, [Y, X]]$ 会将 $\mathfrak{so}(4)$ 的元素映射回自身。这个映射本身可以分解为作用在左手性 $(\mathfrak{su}(2)_L)$ 和右手性 $(\mathfrak{su}(2)_R)$ 子代数上的部分。可以证明，对于形如 $Y=i\sigma_j \otimes \sigma_k$ 的非局域算子，它在左、右两个子代数上的作用强度是相等的 [@problem_id:624514]，这反映了非局域相互作用与局域对称性之间深刻的对称关系。

### 对称性、纠缠与态分类

我们发展起来的群论工具最终是为了理解和分类量子态。一个态的对称性由其**稳定子子群 (stabilizer subgroup)** 来刻画，即所有保持该态不变（最多相差一个全局相位）的变换构成的群。根据轨道-稳定子定理，对称性越高的态（稳定子越大），其在局域幺正变换下的轨道就越小。

*   **乘积态** (如 $|00\rangle$)：纠缠度为零。其稳定子群是 $U(1) \times U(1)$，对应的李代数是二维的，由 $\{i\sigma_z \otimes I, I \otimes i\sigma_z\}$ 张成。
*   **最大纠缠态** (贝尔态)：纠缠度最高。其稳定子群同构于 $SU(2)$，对应的李代数是三维的。例如，对于 $|\Phi^+\rangle$，其稳定子代数由形如 $(A, A^*)$ 的元素构成，其中 $A \in \mathfrak{su}(2)$，$A^*$ 是 $A$ 在标准基下的复共轭。
*   **非最大纠缠态**：纠缠度介于两者之间。它们的对称性也介于两者之间。考虑态 $|\psi\rangle = c |00\rangle + s |11\rangle$，其中 $c, s$ 为实数且 $c^2+s^2=1$。如果 $c \neq s$（例如 $c=\sqrt{3}/2, s=1/2$），它就不是最大纠缠的 [@problem_id:624589]。我们可以通过求解条件 $(A \otimes I + I \otimes B)|\psi\rangle = i\alpha|\psi\rangle$ 来确定其稳定子代数。经过计算可得，唯一的非零解要求 $A = ia_z\sigma_z$ 和 $B = -ia_z\sigma_z$。这意味着稳定子代数是由单个生成元 $(i\sigma_z, -i\sigma_z)$ 张成的一维空间。因此，其对称性低于最大纠缠态。

这种对称性的层级结构直接反映了态的纠缠度。通过稳定子代数的维度，我们可以对双量子比特纯态的局域幺正等价类进行分类。

除了单个态的对称性，我们还可以研究态空间中的不变子空间。考虑所有**贝尔对角态 (Bell-diagonal states)**，其密度矩阵在贝尔基下是对角的 $\rho = \sum_{i=1}^4 p_i |B_i\rangle\langle B_i|$。所有这类态构成的集合是一个三维的四面体。现在我们考察一个连续的局域幺正群 $U(t) = \exp(tK)$ 的作用，其中生成元为 $K = i(\sigma_z \otimes I - I \otimes \sigma_z)$ [@problem_id:624463]。一个态 $\rho$ 在此作用下不变的条件是 $[\rho, K]=0$。
我们发现，贝尔态 $|\Phi^\pm\rangle$ 是 $K$ 的本征态，本征值为0，因此它们是不变的。然而，$|\Psi^\pm\rangle$ 并非 $K$ 的本征态，它们在由自己张成的二维子空间中发生旋转。要使一个贝尔对角态 $\rho$ 在这个旋转下保持不变，它在该旋转子空间上的分量必须是“各向同性”的，即与该子空间中的单位算子成正比。这要求 $\rho$ 在 $|\Psi^+\rangle$ 和 $|\Psi^-\rangle$ 上的布居数相等，即 $p_3=p_4$。这个线性约束将原本三维的贝尔对角态空间缩减为一个二维的仿射子空间。这清晰地展示了系统的代数对称性如何在其状态空间的几何结构上留下印记。