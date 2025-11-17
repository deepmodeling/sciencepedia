## 引言
[量子相位估计算法](@entry_id:147578)（Quantum Phase Estimation, QPE）是现代[量子计算](@entry_id:142712)的基石算法之一，它为精确求解酉算符的[本征值问题](@entry_id:142153)提供了强大的量子工具。在[量子化学](@entry_id:140193)等领域，精确计算分子的[基态](@entry_id:150928)和[激发态](@entry_id:261453)能量是理解和预测[化学反应](@entry_id:146973)的关键，然而这一任务对于[经典计算](@entry_id:136968)机而言，随着体系规模的增长，计算复杂度呈指数级攀升，构成了所谓的“指数墙”难题。[QPE算法](@entry_id:147578)通过巧妙地将难以直接测量的能量值映射为可高精度估计的相位，为突破这一瓶颈开辟了全新的道路。

本文旨在全面而深入地剖析[QPE算法](@entry_id:147578)。在第一章“原理与机制”中，我们将从能量与相位的映射关系出发，揭示[相位回踢](@entry_id:140587)的核心量子效应，并逐步构建完整的算法流程，同时探讨其精度、局限性与优化策略。随后的第二章“应用与跨学科连接”将重点展示QPE如何应用于[量子化学](@entry_id:140193)中的分子能量估算，并讨论从初态制备到容错资源估算的实际挑战，同时将其联系到物理学和计算机科学等其他领域。最后，“动手实践”部分将通过具体问题，帮助读者巩固理论知识并应用于解决实际问题。

现在，让我们首先深入其内部，探究[QPE算法](@entry_id:147578)得以成立的精妙原理与核心机制。

## 原理与机制

[量子相位估计算法](@entry_id:147578)（Quantum Phase Estimation, QPE）是[量子计算](@entry_id:142712)中最为核心的算法之一，其重要性不仅在于它本身能够以极高的精度测量酉算符的本征相位，更在于它构成了许多其他著名量子算法（如秀尔算法）的基础。在[量子化学](@entry_id:140193)领域，QPE 为精确计算分子[哈密顿量](@entry_id:172864)的本征能量提供了一条有力的途径。本章旨在深入剖析 QPE 的基本原理与核心机制，从能量与相位的映射关系出发，逐步揭示算法如何通过量子力学特有的方式提取这些信息，并探讨其精度、局限性及实际应用中的重要考量。

### 核心原理：从能量到相位的映射

在[量子化学](@entry_id:140193)中，我们的目标是求解[定态](@entry_id:137260)薛定谔方程 $H\lvert\psi_E\rangle = E\lvert\psi_E\rangle$，其中 $H$ 是分子的[电子哈密顿量](@entry_id:177588)（一个厄米算符），$E$ 是其本征能量（一个实数），$\lvert\psi_E\rangle$ 是对应的[本征态](@entry_id:149904)。[量子计算](@entry_id:142712)机无法直接存储和输出连续的能量值 $E$。然而，量子系统可以自然地演化。根据[含时薛定谔方程](@entry_id:137898)，一个[能量本征态](@entry_id:152154)随时间的演化由酉算符 $U(t) = \exp(-iHt/\hbar)$ 描述：

$$
U(t)\lvert\psi_E\rangle = \exp(-iHt/\hbar)\lvert\psi_E\rangle = \exp(-iEt/\hbar)\lvert\psi_E\rangle
$$

这个方程是连接经典[哈密顿量](@entry_id:172864)谱问题与[量子计算](@entry_id:142712)相位问题的桥梁。我们可以看到，能量本征态 $\lvert\psi_E\rangle$ 恰好也是[时间演化算符](@entry_id:196774) $U(t)$ 的本征态。其对应的[本征值](@entry_id:154894)是一个复数 $\lambda = \exp(-iEt/\hbar)$，其模为 1，位于复平面的[单位圆](@entry_id:267290)上。这与厄米算符 $H$ 的[本征值](@entry_id:154894) $E$ 必须为实数形成了鲜明对比 [@problem_id:2931326]。

QPE 算法的设计目标正是为了测量酉算符的[本征值](@entry_id:154894)。为了方便，算法通常将[本征值](@entry_id:154894)写成 $e^{2\pi i \phi}$ 的形式，其中 $\phi \in [0, 1)$ 被称为**本征相位**。通过比较两种形式，我们可以建立能量 $E$ 和相位 $\phi$ 之间的直接关系：

$$
\exp(2\pi i \phi) = \exp(-iEt/\hbar)
$$

这等价于指数部分相差 $2\pi i$ 的整数倍，即 $2\pi i \phi = -iEt/\hbar + 2\pi i k$（其中 $k$ 为某个整数）。由于 $\phi$ 被定义在 $[0, 1)$ 区间内，我们可以用模运算得到一个明确的关系：

$$
\phi = \left( -\frac{Et}{2\pi\hbar} \right) \pmod 1
$$

这个关系式是 QPE 用于能量计算的基石。它表明，如果我们能够通过 QPE 算法精确地测量出与能量 $E$ 相关的相位 $\phi$，我们就可以通过下式反解出能量 $E$：

$$
E = -\frac{2\pi\hbar}{t}(\phi - k)
$$

这里的整数 $k$ 带来了所谓的**周期性模糊**或**相位缠绕 (phase wrapping)** 问题。这将在后续章节详细讨论。

### 核心机制：[相位回踢](@entry_id:140587)

QPE 算法如何测量相位 $\phi$ 呢？其核心机制是一种被称为**[相位回踢](@entry_id:140587) (phase kickback)** 的量子效应。为了理解这一机制，我们暂时简化问题，考虑一个单比特的**控制寄存器**和一个承载[本征态](@entry_id:149904) $\lvert\psi\rangle$ 的**系统寄存器**。设 $U\lvert\psi\rangle = e^{i\theta}\lvert\psi\rangle$，其中 $\theta$ 是我们想要估计的相位角（在之前的表示中，$\theta = 2\pi\phi$ 或 $\theta = -Et/\hbar$）。

算法步骤如下 [@problem_id:2931378]：

1.  **初始化**：将系统寄存器置于本征态 $\lvert\psi\rangle$。将控制比特通过阿达马门 (Hadamard gate) 置于叠加态 $\lvert+\rangle = (\lvert0\rangle + \lvert1\rangle)/\sqrt{2}$。系统的总初始状态为：
    $$
    \lvert\Psi_{\text{init}}\rangle = \frac{1}{\sqrt{2}}(\lvert0\rangle + \lvert1\rangle) \otimes \lvert\psi\rangle = \frac{1}{\sqrt{2}}(\lvert0\rangle\lvert\psi\rangle + \lvert1\rangle\lvert\psi\rangle)
    $$

2.  **受控演化**：施加一个**受控-$U$** 门 ($CU$)，其中控制比特为第一个比特，系统寄存器为目标。$CU$ 门的作用是：当控制比特为 $\lvert0\rangle$ 时，目标不变；当控制比特为 $\lvert1\rangle$ 时，对目标施加 $U$ 算符。根据[量子力学的线性](@entry_id:146991)性质，我们可以分别对叠加态的每一项施加 $CU$：
    $$
    \begin{aligned}
    \lvert\Psi_{\text{final}}\rangle  = CU \left( \frac{1}{\sqrt{2}}(\lvert0\rangle\lvert\psi\rangle + \lvert1\rangle\lvert\psi\rangle) \right) \\
     = \frac{1}{\sqrt{2}} (CU(\lvert0\rangle\lvert\psi\rangle) + CU(\lvert1\rangle\lvert\psi\rangle)) \\
     = \frac{1}{\sqrt{2}} (\lvert0\rangle \otimes I\lvert\psi\rangle + \lvert1\rangle \otimes U\lvert\psi\rangle)
    \end{aligned}
    $$

3.  **[相位回踢](@entry_id:140587)**：利用 $U\lvert\psi\rangle = e^{i\theta}\lvert\psi\rangle$ 的性质，我们得到：
    $$
    \lvert\Psi_{\text{final}}\rangle = \frac{1}{\sqrt{2}} (\lvert0\rangle\lvert\psi\rangle + \lvert1\rangle \otimes e^{i\theta}\lvert\psi\rangle)
    $$
    由于 $e^{i\theta}$ 是一个标量，我们可以将其提到前面：
    $$
    \lvert\Psi_{\text{final}}\rangle = \frac{1}{\sqrt{2}} (\lvert0\rangle\lvert\psi\rangle + e^{i\theta}\lvert1\rangle\lvert\psi\rangle) = \left( \frac{\lvert0\rangle + e^{i\theta}\lvert1\rangle}{\sqrt{2}} \right) \otimes \lvert\psi\rangle
    $$

观察最终状态，我们发现一个奇妙的现象：系统寄存器的状态 $\lvert\psi\rangle$ 保持不变，但其[本征值](@entry_id:154894)对应的相位 $e^{i\theta}$ 却被“踢回”到了控制比特的状态上，修改了 $\lvert1\rangle$ 分量的[相对相位](@entry_id:148120)。此时，系统寄存器与控制寄存器并未纠缠。如果对控制比特进行测量（例如在 $X$ 或 $Y$ 基下），测量结果的[统计分布](@entry_id:182030)将依赖于相位角 $\theta$。例如，对该控制比特测量[泡利算符](@entry_id:144061) $\sigma_x$ 和 $\sigma_y$ 的[期望值](@entry_id:153208)，会得到 $\langle \sigma_x \rangle = \cos\theta$ 和 $\langle \sigma_y \rangle = \sin\theta$ [@problem_id:2931378]。这表明，相位信息已经成功地被编码到了控制比特上。

### 完整算法：从二进制展开到量子[傅里叶逆变换](@entry_id:178300)

单个控制比特只能提供关于相位的有限信息。为了获得高精度的估计，标准 QPE 算法使用一个包含 $m$ 个比特的**相位寄存器**（即控制寄存器）。其目标是将相位 $\phi$ 以二[进制](@entry_id:634389)小数的形式 $0.\phi_1\phi_2\dots\phi_m$ 估算出来。

完整算法流程如下：

1.  **初始化**：将 $m$ 个比特的相位寄存器通过阿达马变换置于均匀叠加态：
    $$
    \lvert\Psi_0\rangle = \left( \frac{1}{\sqrt{2^m}}\sum_{j=0}^{2^m-1} \lvert j \rangle \right) \otimes \lvert \psi_E \rangle
    $$
    其中 $\lvert j \rangle$ 是相位寄存器的计算[基态](@entry_id:150928)。

2.  **受控演化序列**：依次对相位寄存器的第 $k$ 个比特（$k=0, 1, \dots, m-1$）施加受控的 $U^{2^k}$ 门。这意味着，对于相位寄存器中的每一个[基态](@entry_id:150928) $\lvert j \rangle = \lvert j_{m-1}\dots j_1 j_0 \rangle$，系统寄存器 $\lvert \psi_E \rangle$ 会被施加 $\prod_{k=0}^{m-1} (U^{2^k})^{j_k} = U^{\sum_k j_k 2^k} = U^j$ 操作。由于 $U^j\lvert \psi_E \rangle = (e^{2\pi i\phi})^j \lvert \psi_E \rangle = e^{2\pi i j\phi} \lvert \psi_E \rangle$，总状态变为：
    $$
    \lvert\Psi_1\rangle = \left( \frac{1}{\sqrt{2^m}}\sum_{j=0}^{2^m-1} e^{2\pi i j\phi} \lvert j \rangle \right) \otimes \lvert \psi_E \rangle
    $$
    请注意这里的相位符号约定。在某些文献或问题中，如 [@problem_id:2931330], [@problem_id:2931364]，[时间演化算符](@entry_id:196774)被定义为 $e^{-iH\tau}$，而酉算符的本征相位被定义为 $e^{2\pi i \phi}$，这将导致关系式 $\phi = -E\tau/(2\pi) \pmod 1$。这仅是一个符号约定问题，物理原理是相同的。此处我们为保持一致性，统一使用 $e^{2\pi i j\phi}$。

3.  **量子傅里叶逆变换 (iQFT)**：对相位寄存器施加 iQFT。iQFT 的作用是将一个以[相位编码](@entry_id:753388)的[傅里叶基](@entry_id:201167)态转换回计算[基态](@entry_id:150928)。其变换规则为：
    $$
    \text{iQFT} \left( \sum_{j=0}^{2^m-1} f_j \lvert j \rangle \right) = \sum_{y=0}^{2^m-1} \left( \frac{1}{\sqrt{2^m}} \sum_{j=0}^{2^m-1} e^{-2\pi i jy/2^m} f_j \right) \lvert y \rangle
    $$
    将我们的状态 $\lvert\Psi_1\rangle$ 代入，相位寄存器的状态变为：
    $$
    \frac{1}{2^m} \sum_{y=0}^{2^m-1} \left( \sum_{j=0}^{2^m-1} e^{2\pi i j(\phi - y/2^m)} \right) \lvert y \rangle
    $$
    这个求和项在 $\phi = y/2^m$ 时会产生一个非常尖锐的峰值。

4.  **测量**：在计算基下测量相位寄存器。如果 $\phi$ 恰好可以表示为一个 $m$ 比特的二[进制](@entry_id:634389)小数，即 $\phi = y_0/2^m$ for some integer $y_0$，那么测量将以 100% 的概率得到结果 $y_0$。在更一般的情况下，测量结果将以高概率出现在最接近 $2^m\phi$ 的整数值附近。测量结果 $y$ 给出相位的估计值 $\tilde{\phi} = y/2^m$。

### 解读算法输出：精度与模糊性

QPE 的输出不是一个完美的答案，它受到精度和系统性模糊的双重限制。理解这两个方面对于有效使用该算法至关重要。

#### [能量分辨率](@entry_id:180330)

QPE 的精度由两个参数共同决定：相位寄存器的比特数 $m$ 和基准演化时间 $t$。$m$ 个比特的寄存器可以将相位 $\phi$ 分辨到 $1/2^m$ 的精度。我们将这个相位分辨率 $\delta\phi \approx 1/2^m$ 转换回[能量分辨率](@entry_id:180330) $\delta E$。从关系式 $E \approx (2\pi\hbar/t)\phi$（忽略周期性模糊），我们有：

$$
\delta E \approx \frac{2\pi\hbar}{t} \delta\phi \approx \frac{2\pi\hbar}{t \cdot 2^m}
$$

这个结果表明 [@problem_id:2931368]，为了提高[能量分辨率](@entry_id:180330)（即减小 $\delta E$），我们可以增加相位寄存器的比特数 $m$，或者增加基准演化时间 $t$。总的有效演化时间是 $T \propto t \cdot 2^m$，因此[能量分辨率](@entry_id:180330)反比于总演化时间，$\delta E \propto 1/T$。

#### 混叠与相位缠绕

QPE 最大的一个系统性问题是**[混叠](@entry_id:146322) (aliasing)** 或相位缠绕。由于相位是模 $1$ 的，两个不同的能量 $E_a$ 和 $E_b$ 可能会映射到同一个相位 $\phi$。这种情况发生的条件是 [@problem_id:2931330]：

$$
\left( -\frac{E_a t}{2\pi\hbar} \right) \equiv \left( -\frac{E_b t}{2\pi\hbar} \right) \pmod 1
$$

这等价于 $(E_a - E_b)t / (2\pi\hbar)$ 是一个非零整数。这意味着，能量谱被“折叠”到了一个宽度为 $2\pi\hbar/t$ 的窗口内。任何能量差恰好是这个窗口宽度的整数倍的能级将变得无法区分。

为了确保对于一个已知的能量范围 $[E_{\min}, E_{\max}]$ 内的所有能量都能被唯一地识别，我们必须保证该范围内的任意两个不同能量都不会发生混叠。这要求能量范围的最大宽度 $W = E_{\max} - E_{\min}$ 小于[混叠](@entry_id:146322)窗口的宽度 [@problem_id:2931326] [@problem_id:2931330]：$W  \frac{2\pi\hbar}{t}$ 或 $t  \frac{2\pi\hbar}{W}$。

例如，如果我们知道一个[哈密顿量](@entry_id:172864)的算符范数有界，$\|H\| \le B$，那么其[能谱](@entry_id:181780)必然位于 $[-B, B]$ 区间内，最大能量宽度为 $2B$。为保证对任何此类[哈密顿量](@entry_id:172864)都不发生[混叠](@entry_id:146322)，我们必须选择 $t  2\pi\hbar / (2B) = \pi\hbar/B$ [@problem_id:2931347]。

这里就体现了一个核心的**权衡关系**：
*   **增加 $t$**：可以提高[能量分辨率](@entry_id:180330) $\delta E$，使得我们能分辨更近的能级。
*   **减小 $t$**：可以扩大无[混叠](@entry_id:146322)的能量窗口，使得我们可以处理具有更宽能谱的系统。

#### 模糊性的缓解策略

幸运的是，我们有策略来处理这种模糊性。

1.  **能量平移**：一个简单有效的方法是平移[哈密顿量](@entry_id:172864)。我们可以模拟一个新的[哈密顿量](@entry_id:172864) $H' = H - E_{\text{ref}}I$，其中 $E_{\text{ref}}$ 是一个已知的参考能量，例如通过[经典计算](@entry_id:136968)得到的对目标能量的粗略估计。$H'$ 的本征能量变为 $E' = E - E_{\text{ref}}$。这样，QPE 测量的是与 $E'$ 相关的相位。通过选择合适的 $E_{\text{ref}}$，我们可以将目标能量 $E$ 附近的能谱平移到接近零点的位置，从而确保其对应的相位 $\phi'$ 落在主窗口 $[0, 1)$ 内，避免了混叠。这个过程不会改变[能级间距](@entry_id:181168)，因此[能量分辨率](@entry_id:180330) $\delta E$ 保持不变 [@problem_id:2931368]。

2.  **非公度演化时间**：一个更高级的技巧是使用两个（或更多）不同的基准演化时间 $\tau_1$ 和 $\tau_2$ 来进行 QPE，且它们的比值是无理数。如果两个不同的能量 $E_a$ 和 $E_b$ 在两次实验中都给出了相同的相位，那么必须同时满足 $(E_a - E_b)\tau_1/(2\pi\hbar) = k_1$ 和 $(E_a - E_b)\tau_2/(2\pi\hbar) = k_2$，其中 $k_1, k_2$ 是整数。这意味着 $\tau_1/\tau_2 = k_1/k_2$ 必须是一个有理数。如果我们从一开始就选择 $\tau_1/\tau_2$ 为无理数，那么除了 $E_a=E_b$ 的平凡情况外，这种混叠永远不会发生。在理想情况下，这可以完全消除[混叠](@entry_id:146322)的模糊性 [@problem_id:2931330]。

### 高级主题与算法细节

#### 叠加态与[简并态](@entry_id:274678)的处理

到目前为止，我们主要假设系统寄存器的初始态是[哈密顿量](@entry_id:172864)的一个非简并本征态。在实际应用中，情况可能更为复杂。

*   **叠加态输入**：如果初始态是多个本征[态的叠加](@entry_id:273993) $\lvert\psi\rangle = \sum_k c_k \lvert E_k\rangle$，会发生什么？根据[量子力学的线性](@entry_id:146991)[叠加原理](@entry_id:144649)，QPE 的最终状态将是每个本征态独立进行 QPE 后结果的叠加。具体来说，最终的测量结果 $y$ 的[概率分布](@entry_id:146404)将是每个分量产生的[概率分布](@entry_id:146404)的非相干加权和 [@problem_id:2931364]：
    $$
    p(y) = \sum_k |c_k|^2 p(y | E_k)
    $$
    其中 $p(y | E_k)$ 是输入为纯[本征态](@entry_id:149904) $\lvert E_k\rangle$ 时得到结果 $y$ 的概率。一个至关重要的结论是，QPE 过程本身是幺正的，它不会改变系统寄存器中不同能量本征态的布居数。如果在 QPE 结束后测量系统寄存器的能量，发现其处于[基态](@entry_id:150928) $\lvert E_0\rangle$ 的概率仍然是 $|c_0|^2$ [@problem_id:2931364]。

*   **简并态输入**：如果[哈密顿量](@entry_id:172864)存在简并，即多个正交的本征态 $\lvert d_1\rangle, \dots, \lvert d_r\rangle$ 对应同一个能量 $E_d$，而初始态是这些简并[态的叠加](@entry_id:273993) $\lvert\psi\rangle = \sum_{j=1}^r c_j \lvert d_j\rangle$，QPE 的行为会非常清晰。因为所有这些分量都具有完全相同的能量 $E_d$，它们在时间演化下会获得完全相同的相位因子。因此，QPE 会像处理单个[本征态](@entry_id:149904)一样，精确地估计出这个共享的相位 $\phi_d = -E_d t/(2\pi\hbar) \pmod 1$。测量相位寄存器不会提供任何关于叠加系数 $\{c_j\}$ 的信息，系统寄存器也不会在简并[子空间](@entry_id:150286)内塌缩，其状态在测量后依然是 $\lvert\psi\rangle$ [@problem_id:2931317]。为了区分这些简并态，我们需要引入另一个与 $H$ 对易的对称性算符 $S$，并利用 $S$ 的不同[本征值](@entry_id:154894)来标记和区分这些简并态 [@problem_id:2931317]。

#### 计量学优势：[海森堡极限](@entry_id:145391)

QPE 的一个根本优势在于其极高的资源效率，这在[量子计量学](@entry_id:138980)框架下可以被精确地描述。假设我们的目标是以精度 $\varepsilon$ 估计能量 $E$。一个经典的方法，如拉姆齐[干涉法](@entry_id:158511) (Ramsey spectroscopy)，需要重复进行 $\nu$ 次实验，每次演化固定的时间 $t$。这种方法的精度受限于散粒噪声，总演化时间资源 $T = \nu t$ 与精度 $\varepsilon$ 的关系为 $T = \Theta(1/\varepsilon^2)$。这被称为**[标准量子极限](@entry_id:137097)**或**散粒噪声极限** [@problem_id:2931305]。

相比之下，QPE 实现了所谓的**[海森堡极限](@entry_id:145391)**。在 QPE 中，为了达到精度 $\varepsilon \sim 1/(\tau 2^m)$，总的相干演化时间为 $T = \tau \sum_{k=0}^{m-1} 2^k = \tau(2^m - 1) \approx \tau 2^m$。结合这两个关系，我们得到 $T = \Theta(1/\varepsilon)$。这种资源 scaling 关系，即资源与精度成反比，是量子力学允许的最高计量精度。

QPE 实现[海森堡极限](@entry_id:145391)的根本原因，在于它能够在一个相干过程中，让系统经历指数级增长的演化时间序列 ($t_k \propto 2^k$)，从而将相位信息高效地累积起来。量子[傅里叶逆变换](@entry_id:178300)只是一个高效的“读出”步骤。即使没有 iQFT，采用自适应测量策略（如基塔耶夫算法）同样可以利用[指数增长](@entry_id:141869)的演化时间达到[海森堡极限](@entry_id:145391) [@problem_id:2931305]。

#### 实现考量与算法变体

在实际的[量子计算](@entry_id:142712)机上实现 QPE，需要将抽象的 $U(t) = e^{-iHt}$ 算符分解为基本[量子门](@entry_id:143510)。对于分子[哈密顿量](@entry_id:172864) $H = \sum_j \alpha_j P_j$（其中 $P_j$ 是泡利串），通常采用**[特罗特-铃木分解](@entry_id:637528) (Trotter-Suzuki decomposition)** 来近似 $U(t)$。例如，一阶 Trotter 公式为：
$$
U(t) \approx \left( \prod_j e^{-i(\alpha_j t/r)P_j} \right)^r
$$
其中 $r$ 是 Trotter 步数。QPE 需要的受控 $U$ 门则通过实现每个泡利指数项的受控版本来构造。分析表明，将一个泡利指数项 $e^{-i\theta P_j}$ 变为受控版本，其带来的额外 CNOT 门代价是一个很小的常数（例如，在标准模型下为 2 个 CNOT），与泡利串 $P_j$ 的权重无关。因此，实现受控-$U$ 的总 CNOT 代价开销与 Trotter 分解中的项数 $L$ 和步数 $r$ 成正比，即 $2Lr$ [@problem_id:2931300]。

标准 QPE 算法对硬件要求很高，尤其是需要一个包含多个比特且能保持长时间相干的相位寄存器，并能执行复杂的多比特 iQFT。为了降低资源需求，发展出了几种算法变体 [@problem_id:2931351]：

*   **标准 QPE**：需要 $m$ 个辅助比特。系统寄存器和所有 $m$ 个辅助比特都必须在整个算法（总时长为 $\Theta(2^m)$）期间保持相干。[电路深度](@entry_id:266132)最大。

*   **迭代式 QPE (iQPE)**：仅需 1 个辅助比特。它逐一估计相位的每一位。在第 $k$ 轮，通过测量和经典反馈来校正下一轮的演化。这极大地减少了辅助比特数量和 iQFT 的需求，但代价是算法必须串行执行 $m$ 轮，总运行时间仍然很长。

*   **半经典 QPE**：类似于 iQPE，但其 iQFT 是通过经典计算和反馈实现的。

一个关键的共同点是，如果系统寄存器的本征态在算法中途不能被重新制备，那么无论采用哪种变体，系统寄存器都必须在所有受控演化步骤的总时长内（即 $\Theta(2^m)$）保持相干。因此，虽然 iQPE 等变体节省了辅助比特，但它们并不能缓解对系统寄存器长[相干时间](@entry_id:176187)的核心要求 [@problem_id:2931351]。