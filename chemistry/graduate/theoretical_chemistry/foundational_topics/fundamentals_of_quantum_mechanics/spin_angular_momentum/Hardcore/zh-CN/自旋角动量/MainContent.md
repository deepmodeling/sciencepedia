## 引言
自旋角动量是现代量子理论的基石之一，是一个没有经典对应物的纯粹量子力学概念。尽管其最初是为解释原子光谱中的精细结构而引入的一个内禀自由度，但自旋的深远影响已远远超出了原子物理的范畴，渗透到化学、物理和材料科学的各个角落。然而，从抽象的数学形式（如泡利矩阵和SU(2)代数）到其在解释和预测真实世界现象（如分子磁性、光化学反应路径和磁共振信号）中的强大能力，这之间存在一条需要系统性搭建的认知桥梁。

本文旨在构建这座桥梁，带领读者全面而深入地理解自旋角动量。我们将从第一章 **“原理与机制”** 出发，奠定坚实的理论基础，深入探讨自旋的代数结构、其相对论起源以及角动量耦合的核心规则。随后，在第二章 **“应用与跨学科联系”** 中，我们将把这些抽象原理付诸实践，展示自旋如何在原子光谱、分子磁性、计算化学和磁共振等多个领域扮演决定性角色。最后，通过第三章 **“动手实践”** 中的精选问题，读者将有机会亲手应用所学知识，解决具体的物理和化学问题，从而将理论理解转化为实践能力。

## 原理与机制

在上一章引论之后，我们现在深入探讨电子自旋角动量的核心原理与机制。虽然自旋和轨道角动量在形式上共享相同的代数结构，但自旋的起源、特性及其在化学系统中的表现形式，揭示了深刻的物理学原理，这些原理超越了经典类比，并对我们理解电子结构、光谱学和化学反应性至关重要。

### 自旋的代数框架

角动量在量子力学中的基本定义源于其作为空间旋转生成元的角色。任何满足以下对易关系的算符矢量 $\hat{\mathbf{J}} = (\hat{J}_x, \hat{J}_y, \hat{J}_z)$ 都被定义为角动量：
$$
[\hat{J}_i, \hat{J}_j] = i\hbar \varepsilon_{ijk} \hat{J}_k
$$
其中 $\varepsilon_{ijk}$ 是 Levi-Civita 符号。这个代数结构，即 $\mathfrak{su}(2)$ 李代数，是所有角动量理论的基石。电子的 **自旋角动量** $\hat{\mathbf{S}}$ 与轨道角动量 $\hat{\mathbf{L}}$ 一样，也遵循这套对易关系。

纯粹从代数出发，我们可以构建一个 Casimir 算符 $\hat{\mathbf{J}}^2 = \hat{J}_x^2 + \hat{J}_y^2 + \hat{J}_z^2$，它与所有分量 $\hat{J}_i$ 对易。因此，我们可以找到 $\hat{\mathbf{J}}^2$ 和其中一个分量（按惯例是 $\hat{J}_z$）的共同本征态，记为 $|j, m_j\rangle$。这些态满足：
$$
\hat{\mathbf{J}}^2 |j, m_j\rangle = \hbar^2 j(j+1) |j, m_j\rangle
$$
$$
\hat{J}_z |j, m_j\rangle = \hbar m_j |j, m_j\rangle
$$
代数推导表明，量子数 $j$ 可以取非负整数或半整数值 ($j = 0, \frac{1}{2}, 1, \frac{3}{2}, \dots$)，而对于给定的 $j$，磁量子数 $m_j$ 可以取 $2j+1$ 个值，从 $-j$ 到 $+j$ 以整数步长变化。

为了方便地在这些本征态之间移动，我们定义 **升降算符** $\hat{J}_\pm = \hat{J}_x \pm i\hat{J}_y$。利用基本的对易关系，可以推导出它们与 $\hat{J}_z$ 的对易关系：
$$
[\hat{J}_z, \hat{J}_\pm] = \pm\hbar \hat{J}_\pm
$$
这个关系表明，当 $\hat{J}_\pm$ 作用于一个 $m_j$ 本征态时，会产生一个新的本征态，其磁量子数变为 $m_j \pm 1$。因此，它们被称为阶梯算符。通过计算态 $\hat{J}_\pm|j, m_j\rangle$ 的模方，可以得到其具体的变换规则 [@problem_id:2807527]：
$$
\hat{J}_\pm |j, m_j\rangle = \hbar \sqrt{j(j+1) - m_j(m_j \pm 1)} |j, m_j \pm 1\rangle
$$
这个公式是量子力学中角动量理论的核心。对于电子，实验发现其固有（自旋）角动量量子数 $s=\frac{1}{2}$。这意味着磁自旋量子数 $m_s$ 只能取两个值：$+\frac{1}{2}$ (自旋向上，或 $\alpha$) 和 $-\frac{1}{2}$ (自旋向下，或 $\beta$)。

### 自旋-1/2 系统与泡利矩阵

对于电子这个最重要的自旋-1/2系统，角动量代数可以被具体地表示为矩阵。自旋态的希尔伯特空间是二维的，其标准基矢为 $\alpha = |\frac{1}{2}, +\frac{1}{2}\rangle$ 和 $\beta = |\frac{1}{2}, -\frac{1}{2}\rangle$。在矩阵表示中，它们通常写为：
$$
\alpha \equiv \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad \beta \equiv \begin{pmatrix} 0 \\ 1 \end{pmatrix}
$$
根据 $\hat{S}_z$ 的本征值方程，其矩阵表示是：
$$
\hat{S}_z = \frac{\hbar}{2} \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}
$$
我们可以利用前面推导的升降算符作用规则来构建 $\hat{S}_x$ 和 $\hat{S}_y$ 的矩阵。对于 $s=\frac{1}{2}$ 系统 [@problem_id:2807527]：
$$
\hat{S}_+ |\tfrac{1}{2}, -\tfrac{1}{2}\rangle = \hbar |\tfrac{1}{2}, +\tfrac{1}{2}\rangle, \quad \hat{S}_- |\tfrac{1}{2}, +\tfrac{1}{2}\rangle = \hbar |\tfrac{1}{2}, -\tfrac{1}{2}\rangle
$$
所有其他作用（如 $\hat{S}_+$ 作用于自旋向上态）均为零。由此可得 $\hat{S}_\pm$ 的矩阵表示：
$$
\hat{S}_+ = \hbar \begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix}, \quad \hat{S}_- = \hbar \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix}
$$
通过反解 $\hat{S}_x = \frac{1}{2}(\hat{S}_+ + \hat{S}_-)$ 和 $\hat{S}_y = \frac{1}{2i}(\hat{S}_+ - \hat{S}_-)$，我们得到所有三个自旋算符的完整矩阵表示 [@problem_id:2807571]：
$$
\hat{S}_x = \frac{\hbar}{2} \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}, \quad \hat{S}_y = \frac{\hbar}{2} \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}, \quad \hat{S}_z = \frac{\hbar}{2} \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}
$$
这些矩阵可以被方便地表示为 $\hat{S}_i = \frac{\hbar}{2} \sigma_i$，其中 $\sigma_i$ 是无量纲的 **泡利矩阵**：
$$
\sigma_x = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}, \quad \sigma_y = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}, \quad \sigma_z = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}
$$
泡利矩阵是量子信息和相对论量子力学中的核心数学工具。它们除了满足角动量代数的缩放版本 $[\sigma_i, \sigma_j] = 2i \varepsilon_{ijk} \sigma_k$ 外，还满足一个重要的反对易关系：
$$
\{\sigma_i, \sigma_j\} = \sigma_i \sigma_j + \sigma_j \sigma_i = 2\delta_{ij}\mathbb{I}_2
$$
其中 $\mathbb{I}_2$ 是 $2 \times 2$ 单位矩阵。这个关系表明，不同的泡利矩阵是反对易的，而任何一个泡利矩阵的平方都是单位矩阵。结合对易和反对易关系，可以推导出一个极为有用的泡利矩阵乘积恒等式 [@problem_id:2807571]：
$$
\sigma_i \sigma_j = \delta_{ij}\mathbb{I}_2 + i \varepsilon_{ijk} \sigma_k
$$
这个恒等式的一个优雅应用是计算两个任意矢量 $\mathbf{a}$ 和 $\mathbf{b}$ 与泡利矩阵矢量 $\boldsymbol{\sigma}$ 的点积的乘积：
$$
(\boldsymbol{\sigma}\cdot \mathbf{a})(\boldsymbol{\sigma}\cdot \mathbf{b}) = (\mathbf{a} \cdot \mathbf{b})\mathbb{I}_{2} + i \boldsymbol{\sigma} \cdot (\mathbf{a} \times \mathbf{b})
$$
这个结果在处理自旋与磁场或与其他自旋相互作用的哈密顿量时非常有用。

### 自旋的几何与相对论本质

为什么自旋量子数可以是半整数，而轨道角动量量子数必须是整数？这个问题的答案揭示了自旋深刻的几何和拓扑根源。

考虑一个绕任意轴 $\hat{n}$ 旋转 $2\pi$ 的操作。从经典直觉来看，这会将系统带回到其初始状态。对于一个量子态，这意味着旋转后的态最多与初始态相差一个相位因子。旋转算符为 $\hat{R}_{\hat{n}}(\theta) = \exp(-i\theta \hat{n}\cdot\hat{\mathbf{J}}/\hbar)$。对于一个 $2\pi$ 旋转，本征态 $|j,m_j\rangle$ 的变换为：
$$
\hat{R}_{\hat{n}}(2\pi) |j, m_j\rangle = e^{-i 2\pi m_j} |j, m_j\rangle
$$
如果 $j$ 是整数（如轨道角动量 $\ell$），则所有的 $m_j$ 也都是整数，因此 $e^{-i 2\pi m_j}=1$。旋转 $2\pi$ 后，态函数不变。然而，如果 $j$ 是半整数（如自旋 $s=\frac{1}{2}$），则所有的 $m_j$ 都是半整数，因此 $e^{-i 2\pi m_j}=e^{-i\pi(2m_j)}=-1$。这意味着，对于一个自旋-1/2粒子，旋转 $2\pi$ 后，其态函数会乘以 $-1$ [@problem_id:2121694]。需要旋转 $4\pi$ 才能使其态函数恢复原状。这种奇异的“双值”行为是 **旋量 (spinor)** 的标志性特征。

这种差异的根本原因在于旋转群的拓扑结构 [@problem_id:2807499]。轨道角动量态是定义在三维物理空间 $\mathbb{R}^3$ 上的波函数 $\psi(\mathbf{r})$。这些函数必须是单值的，这意味着它们必须构成三维空间旋转群 $\mathrm{SO}(3)$ 的单值表示。在 $\mathrm{SO}(3)$ 中，绕任何轴旋转 $2\pi$ 都等同于恒等变换。因此，作用在波函数上的幺正算符必须是单位算符 $\hat{\mathbb{1}}$，这排除了半整数 $\ell$ 的可能性。

然而，自旋态存在于一个抽象的“内部”希尔伯特空间中。在量子力学中，物理态是由希尔伯特空间中的“射线”（即相差一个相位因子的所有矢量）来描述的。这意味着对称性操作（如旋转）只需要以“投影”方式表示即可，即允许变换后产生一个相位因子。$\mathrm{SO}(3)$ 群并非单连通的，它允许多值的投影表示。这些表示对应于其 **普适覆盖群** $\mathrm{SU}(2)$ 的单值线性表示。在 $\mathrm{SU}(2)$ 群中，对应于物理空间中 $2\pi$ 旋转的元素是 $-\mathbb{I}_2$，而不是 $\mathbb{I}_2$。因此，作用在自旋态上的幺正算符可以是 $-\hat{\mathbb{1}}$，这正好允许了半整数自旋量子数 $s$ 的存在 [@problem_id:2807499], [@problem_id:2121694]。

自旋不仅是一个数学上的可能性，更是相对论的要求。在非相对论量子力学中，自由粒子的轨道角动量是守恒的。然而，在 **Dirac 相对论量子力学** 中，情况并非如此。自由粒子的 Dirac 哈密顿量 $\hat{H}_D = c \boldsymbol{\alpha} \cdot \hat{\mathbf{p}} + \beta m c^2$ 与轨道角动量算符 $\hat{\mathbf{L}}$ 并不对易 [@problem_id:1397419]。例如，可以计算出：
$$
[\hat{H}_D, \hat{L}_z] = i\hbar c (\alpha_y \hat{p}_x - \alpha_x \hat{p}_y) \neq 0
$$
这表明轨道角动量本身不守恒，好像有一个“内部力矩”在作用。为了恢复角动量守恒，必须引入一个额外的角动量，即自旋。通过定义一个 $4\times4$ 的自旋算符 $\hat{\mathbf{S}}$，可以证明总角动量 $\hat{\mathbf{J}} = \hat{\mathbf{L}} + \hat{\mathbf{S}}$ 与 Dirac 哈密顿量是对易的，$[\hat{H}_D, \hat{\mathbf{J}}] = 0$。因此，自旋是洛伦兹对称性下一个不可避免的自然产物。

### 角动量的耦合

当一个系统中存在多个角动量来源时（例如，一个电子的轨道和自旋，或多个电子的自旋），它们会相互作用。总角动量是各分量之和，例如 $\hat{\mathbf{J}} = \hat{\mathbf{L}} + \hat{\mathbf{S}}$ 或 $\hat{\mathbf{S}} = \hat{\mathbf{S}}_1 + \hat{\mathbf{S}}_2$。一个非常有用的技巧是将相互作用项（通常是点积形式）用总角动量和分角动量的平方算符来表示。考虑两个角动量 $\hat{\mathbf{J}}_1$ 和 $\hat{\mathbf{J}}_2$，总角动量为 $\hat{\mathbf{J}} = \hat{\mathbf{J}}_1 + \hat{\mathbf{J}}_2$。对其平方：
$$
\hat{\mathbf{J}}^2 = (\hat{\mathbf{J}}_1 + \hat{\mathbf{J}}_2) \cdot (\hat{\mathbf{J}}_1 + \hat{\mathbf{J}}_2) = \hat{\mathbf{J}}_1^2 + \hat{\mathbf{J}}_2^2 + 2\hat{\mathbf{J}}_1 \cdot \hat{\mathbf{J}}_2
$$
（假设 $\hat{\mathbf{J}}_1$ 和 $\hat{\mathbf{J}}_2$ 的分量对易，例如轨道和自旋，或不同粒子的角动量）。由此得到所谓的 **Dirac 自旋交换恒等式**：
$$
\hat{\mathbf{J}}_1 \cdot \hat{\mathbf{J}}_2 = \frac{1}{2}(\hat{\mathbf{J}}^2 - \hat{\mathbf{J}}_1^2 - \hat{\mathbf{J}}_2^2)
$$
这个关系极为强大，因为它将一个复杂的矢量点积算符转换为了三个对角化的标量算符的组合。

一个直接的应用是 **自旋-轨道耦合**。原子中的自旋-轨道相互作用哈密顿量包含一项 $\hat{H}_{SO} \propto \hat{\mathbf{L}} \cdot \hat{\mathbf{S}}$。利用上述恒等式 [@problem_id:2141059]，该项变为：
$$
\hat{\mathbf{L}} \cdot \hat{\mathbf{S}} = \frac{1}{2}(\hat{\mathbf{J}}^2 - \hat{\mathbf{L}}^2 - \hat{\mathbf{S}}^2)
$$
由于总角动量本征态 $|j, m_j, \ell, s\rangle$ 是 $\hat{\mathbf{J}}^2, \hat{\mathbf{L}}^2, \hat{\mathbf{S}}^2$ 的共同本征态，$\hat{H}_{SO}$ 在这个基底下是自动对角的，其能量贡献可以直接计算为 $\frac{1}{2}[j(j+1) - \ell(\ell+1) - s(s+1)]\hbar^2$。

另一个关键应用是 **两个自旋-1/2 电子的耦合** [@problem_id:2807550]。这是理解化学键、分子磁性和电子结构的基础。两个电子的自旋空间是四维的，由乘积基矢 $\{|\uparrow\uparrow\rangle, |\uparrow\downarrow\rangle, |\downarrow\uparrow\rangle, |\downarrow\downarrow\rangle\}$ 张成。在这个耦合图像中，态是总自旋 $\hat{\mathbf{S}} = \hat{\mathbf{S}}_1 + \hat{\mathbf{S}}_2$ 的本征态 $|S, M_S\rangle$。根据角动量加法规则，$s_1=\frac{1}{2}, s_2=\frac{1}{2}$ 可以耦合得到总自旋 $S = |s_1-s_2|, \dots, s_1+s_2$，即 $S=0$ 和 $S=1$。
-   **单重态 (Singlet)**: $S=0, M_S=0$。
-   **三重态 (Triplet)**: $S=1$, $M_S = -1, 0, 1$。

利用升降算符或 Clebsch-Gordan 系数，可以构建出这些总自旋本征态：
$$
\begin{cases}
|1, 1\rangle = |\uparrow\uparrow\rangle \\
|1, 0\rangle = \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle + |\downarrow\uparrow\rangle) \\
|1, -1\rangle = |\downarrow\downarrow\rangle
\end{cases} \quad \text{(Triplet)}
$$
$$
|0, 0\rangle = \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle) \quad \text{(Singlet)}
$$
这些态是 Heisenberg **交换哈密顿量** $\hat{H} = J \hat{\mathbf{s}}_1 \cdot \hat{\mathbf{s}}_2 = (J/\hbar^2) \hat{\mathbf{S}}_1 \cdot \hat{\mathbf{S}}_2$ 的本征态。利用 Dirac 恒等式，其能量本征值为：
$$
E_S = \frac{J}{2\hbar^2} (\hbar^2 S(S+1) - \hbar^2 s_1(s_1+1) - \hbar^2 s_2(s_2+1)) = \frac{J}{2} (S(S+1) - \frac{3}{2})
$$
对于单重态 ($S=0$)，$E_{singlet} = -\frac{3}{4}J$。对于三重态 ($S=1$)，$E_{triplet} = +\frac{1}{4}J$。因此，单重态与三重态之间的能量差为 $\Delta E = E_{triplet} - E_{singlet} = J$ [@problem_id:2807550]。这个简单的结果构成了分子磁性理论的基石。

### 多电子波函数中的自旋与自旋污染

在量子化学计算中，波函数通常近似为 **斯莱特行列式 (Slater determinants)**。理解自旋算符如何作用于这些行列式至关重要 [@problem_id:2807576]。
一个由 $n_\alpha$ 个 $\alpha$ 自旋轨道和 $n_\beta$ 个 $\beta$ 自旋轨道构成的斯莱特行列式，永远是总自旋 $z$ 分量算符 $\hat{S}_z = \sum_i \hat{s}_{z,i}$ 的本征函数，其本征值为：
$$
M_S = \frac{1}{2}(n_\alpha - n_\beta)
$$
然而，一个斯莱特行列式 **通常不是** 总自旋平方算符 $\hat{S}^2$ 的本征函数。这是因为 $\hat{S}^2$ 可以写成 $\hat{S}^2 = \hat{S}_- \hat{S}_+ + \hat{S}_z^2 + \hbar \hat{S}_z$。升降算符 $\hat{S}_\pm$ 会将一个 $\beta$ 自旋翻转为 $\alpha$ 自旋（或反之）。当 $\hat{S}_\pm$ 作用于一个行列式时，会产生一个新的行列式（或行列式的线性组合）。除非这些新产生的行列式恰好为零或与原行列式成比例，否则原行列式就不是 $\hat{S}^2$ 的本征函数。

这种情况导致了在 **非限制性 Hartree-Fock (UHF)** 方法中的一个普遍问题，称为 **自旋污染 (spin contamination)**。在 UHF 中，$\alpha$ 和 $\beta$ 电子使用不同的空间轨道，导致 $\hat{S}_\pm$ 的作用通常会产生与原行列式线性无关的新行列式。结果，UHF 波函数虽然是 $\hat{S}_z$ 的本征函数，但却是多个不同总自旋 $S$ 的态的混合物。

只有在特殊情况下，单个斯莱特行列式才是纯的自旋态：
1.  **闭壳层限制性 Hartree-Fock (RHF) 波函数**：所有轨道成对占据。任何自旋翻转都会导致两个电子占据同一个自旋轨道，根据泡利不相容原理，行列式为零。因此 $\hat{S}_\pm \Psi = 0$，可以推得 $S=0$。
2.  **高自旋开壳层 ROHF 型波函数**：例如，所有未成对电子都具有 $\alpha$ 自旋。此时，$\hat{S}_+ \Psi = 0$，该态是“最高权重态”，其 $S=M_S$。

自旋污染的程度可以通过计算 $\langle \hat{S}^2 \rangle$ 的期望值来量化。对于一个纯的自旋态，$\langle \hat{S}^2 \rangle$ 应为 $\hbar^2 S(S+1)$。任何偏离这个理想值的都表示存在污染。例如，一个名义上的单重态 ($S=0$) 如果被三重态 ($S=1$) 污染，其波函数可以模型化为 $|\Psi\rangle = c_s|0,0\rangle + c_t|1,0\rangle$。其 $\langle \hat{S}^2 \rangle$ 的期望值为 [@problem_id:2807560]：
$$
\langle \hat{S}^2 \rangle = \langle \Psi | \hat{S}^2 | \Psi \rangle = |c_s|^2 \cdot 0 + |c_t|^2 \cdot (1(2)\hbar^2) = 2|c_t|^2 \hbar^2
$$
这个结果清晰地表明，$\langle \hat{S}^2 \rangle$ 的非零值直接正比于三重态污染的概率 $|c_t|^2$。因此，$\langle \hat{S}^2 \rangle$ 是衡量 UHF 波函数质量的一个重要指标。

### 时间反演对称性与克莱默斯简并

除了旋转对称性，量子系统中还存在一个更微妙的对称性——时间反演对称性，它对自旋系统有深远的影响。**时间反演算符** $\hat{\Theta}$ 是一个反幺正算符，它反转动量和角动量（包括自旋），但不改变位置：$\hat{\Theta}\hat{\mathbf{p}}\hat{\Theta}^{-1} = -\hat{\mathbf{p}}$, $\hat{\Theta}\hat{\mathbf{S}}\hat{\Theta}^{-1} = -\hat{\mathbf{S}}$。

$\hat{\Theta}$ 的一个关键性质是其平方的行为。对于一个包含 $N$ 个电子的系统，$\hat{\Theta}^2 = (-1)^N \hat{\mathbb{1}}$。这意味着：
-   对于电子数为偶数的系统（总自旋为整数），$\hat{\Theta}^2 = +\hat{\mathbb{1}}$。
-   对于电子数为奇数的系统（总自旋为半整数），$\hat{\Theta}^2 = -\hat{\mathbb{1}}$。

**克莱默斯定理 (Kramers' Theorem)** 指出：对于一个具有半整数总自旋的系统，如果其哈密顿量 $\hat{H}$ 在时间反演下是不变的（即 $[\hat{H}, \hat{\Theta}]=0$，这在没有外磁场时通常成立），那么该系统的每个能量本征态都至少是二重简并的 [@problem_id:2807500]。

证明思路如下：若 $|\psi\rangle$ 是一个能量为 $E$ 的本征态，则其时间反演伙伴 $|\phi\rangle = \hat{\Theta}|\psi\rangle$ 也具有相同的能量 $E$。我们可以证明 $|\psi\rangle$ 和 $|\phi\rangle$ 必定是线性无关的。如果假设它们线性相关，即 $\hat{\Theta}|\psi\rangle = c|\psi\rangle$，那么应用两次 $\hat{\Theta}$ 会得到 $\hat{\Theta}^2|\psi\rangle = |c|^2|\psi\rangle$。但对于半整数自旋系统，我们又有 $\hat{\Theta}^2|\psi\rangle = -|\psi\rangle$。这两个结果合在一起意味着 $|c|^2 = -1$，这对于任何复数 $c$ 都是不可能的。因此，假设不成立，$|\psi\rangle$ 和 $\hat{\Theta}|\psi\rangle$ 必须是两个不同的、简并的态。

这对简并的态 $(\psi, \Theta\psi)$ 被称为一个 **克莱默斯对 (Kramers pair)**，它们所具有的简并性被称为 **克莱默斯简并 (Kramers degeneracy)**。这个简并性非常顽强：
-   它不依赖于任何空间对称性。即使在一个完全不对称的手性分子中，只要电子数是奇数，所有能级都必须是二重简并的 [@problem_id:2807500]。
-   任何保持时间反演对称性的微扰，如自旋-轨道耦合、自旋-转动耦合或静态电场（晶体场），都不能解除克莱默斯简并 [@problem_id:2807500]。
-   唯一能解除克莱默斯简并的是破坏时间反演对称性的微扰，最典型的例子就是外加磁场。这一性质是电子顺磁共振 (EPR) 光谱等技术的基础。