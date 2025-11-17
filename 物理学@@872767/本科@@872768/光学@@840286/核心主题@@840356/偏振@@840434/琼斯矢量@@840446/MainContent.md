## 引言
光的偏振是其最基本的性质之一，对它的精确描述和操控是现代光学、[光子](@entry_id:145192)学技术和科学研究的核心。然而，仅仅定性地描述光为“水平偏振”或“[圆偏振](@entry_id:261702)”远不足以应对复杂[光学系统设计](@entry_id:164820)和精密测量的需求。我们需要一个能够量化[电场](@entry_id:194326)分量振幅和相位关系的数学语言，以预测和控制光与物质相互作用后的行为。琼斯代数（Jones Calculus）正是为解决这一问题而生的强大工具，它为完全偏振光提供了一个简洁而优雅的分析框架。

本文旨在系统性地介绍琼斯矢量及其相关理论。通过学习本文，您将能够掌握使用琼斯代数分析偏振问题的核心技能。
- 在“**原理与机制**”一章中，我们将建立琼斯矢量和[琼斯矩阵](@entry_id:266533)的数学基础，学习如何表示各种基本偏振态，并理解光学元件如何通过矩阵运算改变[光的偏振](@entry_id:262080)。
- 接下来，在“**应用与交叉学科联系**”一章中，我们将探讨琼斯代数在[光学系统设计](@entry_id:164820)、[材料表征](@entry_id:161346)、[光通信](@entry_id:200237)乃至与量子力学类比等领域的广泛实际应用，展示其理论的强大生命力。
- 最后，通过“**动手实践**”部分，您将有机会运用所学知识解决具体的计算问题，从而巩固和深化理解。

让我们首先深入第一章，探索琼斯代数的基本原理和核心机制。

## 原理与机制

在理解光的偏振现象时，我们需要一个能够精确描述[电场](@entry_id:194326)矢量[振动](@entry_id:267781)方向、振幅和相位关系的数学框架。琼斯矢量 ([Jones vector](@entry_id:265773)) 和[琼斯矩阵](@entry_id:266533) ([Jones matrix](@entry_id:266533)) 共同构成的琼斯代数 ([Jones calculus](@entry_id:182044)) 为完全偏振光提供了一个简洁而强大的分析工具。本章将系统地阐述琼斯代数的根本原理及其在光学[系统分析](@entry_id:263805)中的应用机制。

### 使用琼斯矢量表示[偏振态](@entry_id:175130)

为了超越对偏振的定性描述，我们需要一种能够捕捉[电场](@entry_id:194326)分量之间微妙相位关系的形式化语言。琼斯矢量正是为此而生。

#### 定义与构建

对于一束沿 $z$ 轴正方向传播的单色平面[电磁波](@entry_id:269629)，其[电场](@entry_id:194326)可以分解为在 $x$ 和 $y$ 方向上相互正交的分量。琼斯矢量是一个 $2 \times 1$ 的复数列表，其元素分别为 $x$ 和 $y$ 方向[电场](@entry_id:194326)分量的[复振幅](@entry_id:164138)。其[标准形式](@entry_id:153058)为：

$$
\mathbf{J} = \begin{pmatrix} \tilde{E}_x \\ \tilde{E}_y \end{pmatrix}
$$

这里的 $\tilde{E}_x$ 和 $\tilde{E}_y$ 是复数，它们包含了每个分量的振幅和初始相位信息。瞬时[电场](@entry_id:194326)矢量 $E_x(z, t)$ 和 $E_y(z, t)$ 可以通过取复数表达式的实部来获得：

$$
E_x(z, t) = \text{Re}(\tilde{E}_x e^{i(kz - \omega t)})
$$
$$
E_y(z, t) = \text{Re}(\tilde{E}_y e^{i(kz - \omega t)})
$$

其中 $k$ 是波数，$\omega$ 是[角频率](@entry_id:261565)。

为了具体理解琼斯矢量的构建过程，我们考虑一个[电场](@entry_id:194326)分量由下式给出的光波 [@problem_id:2237419]：
$E_x(z, t) = E_0 \cos(kz - \omega t)$
$E_y(z, t) = E_0 \cos(kz - \omega t - \frac{\pi}{2})$

根据[欧拉公式](@entry_id:176440) $e^{i\theta} = \cos\theta + i\sin\theta$，我们可以将 $E_x$ 的[复振幅](@entry_id:164138)直接取为实数 $E_0$，因为 $\text{Re}(E_0 e^{i(kz - \omega t)}) = E_0 \cos(kz - \omega t)$。对于 $E_y$ 分量，我们需要找到一个[复振幅](@entry_id:164138) $\tilde{E}_y$ 使得其满足给定的表达式。注意到 $\cos(\alpha - \frac{\pi}{2}) = \sin(\alpha)$，而 $\text{Re}(-i e^{i\alpha}) = \text{Re}(-i(\cos\alpha + i\sin\alpha)) = \sin\alpha$。因此，我们可以将 $\tilde{E}_y$ 写为 $\tilde{E}_y = E_0 e^{-i\pi/2} = -iE_0$。这样，该光波的琼斯矢量为：

$$
\mathbf{J} = \begin{pmatrix} E_0 \\ -iE_0 \end{pmatrix}
$$

#### 归一化与[全局相位](@entry_id:147947)

光波的强度 $I$ 正比于[电场](@entry_id:194326)振幅的平方和，即 $I \propto |\tilde{E}_x|^2 + |\tilde{E}_y|^2$。在理论分析中，为了专注于[偏振态](@entry_id:175130)本身而不受光强的绝对大小影响，我们通常使用**归一化琼斯矢量** (normalized [Jones vector](@entry_id:265773)s)。归一化要求矢量的模长为 1，即 $|\tilde{E}_x|^2 + |\tilde{E}_y|^2 = 1$。对于上述例子，矢量的模方为 $|E_0|^2 + |-iE_0|^2 = 2E_0^2$。因此，归一化后的琼斯矢量为：

$$
\mathbf{J}_{\text{norm}} = \frac{1}{\sqrt{2}E_0} \begin{pmatrix} E_0 \\ -iE_0 \end{pmatrix} = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ -i \end{pmatrix}
$$

另一个至关重要的概念是**[全局相位](@entry_id:147947)** (global phase)。将一个琼斯矢量乘以任意一个复相位因子 $e^{i\phi}$（其中 $\phi$ 是实数），并不会改变光波的物理偏振状态。这是因为这个因子会同时作用于 $E_x$ 和 $E_y$，在计算可观测的物理量（如偏振椭圆的形状和方向）时会被抵消。例如，在一次实验中，两位研究者可能因为选择了不同的相位零点而得到看似不同的琼斯矢量，如 $\mathbf{J}_A = \begin{pmatrix} 4 \\ 1+2i \end{pmatrix}$ 和 $\mathbf{J}_B = \begin{pmatrix} 12+16i \\ -5+10i \end{pmatrix}$ [@problem_id:2237426]。然而，经过仔细计算可以发现 $\mathbf{J}_B = (3+4i)\mathbf{J}_A$。这意味着两个矢量仅相差一个复数常数因子，它们描述的是完全相同的偏振状态，具有完全相同的物理性质，例如相同的偏振椭圆方位角。因此，在琼斯代数中，$\mathbf{J}$ 和 $c\mathbf{J}$ (其中 $c$ 是任意非零复数) 代表同一种偏振。

### 基本[偏振态](@entry_id:175130)的琼斯矢量

利用琼斯矢量的定义，我们可以系统地表示所有基本偏振类型。

#### [线偏振光](@entry_id:165445)

当[电场](@entry_id:194326)的两个分量同相（相位差为 0）或反相（相位差为 $\pi$）[振动](@entry_id:267781)时，合成的[电场](@entry_id:194326)矢量尖端将始终沿着一条直线往复运动。这种光被称为**[线偏振光](@entry_id:165445)** (linearly polarized light)。其数学条件是两个[复振幅](@entry_id:164138) $\tilde{E}_x$ 和 $\tilde{E}_y$ 之间的相位差 $\delta$ 为 $\pi$ 的整数倍，即 $\delta = m\pi$，$m \in \mathbb{Z}$ [@problem_id:2237406]。这等价于比值 $\tilde{E}_y / \tilde{E}_x$ 是一个实数。

一些重要的线偏振态的归一化琼斯矢量包括：
- **水平偏振光 (H-pol):** [电场](@entry_id:194326)沿 $x$ 轴[振动](@entry_id:267781)。
  $$ \mathbf{J}_H = \begin{pmatrix} 1 \\ 0 \end{pmatrix} $$
- **垂直偏振光 (V-pol):** [电场](@entry_id:194326)沿 $y$ 轴[振动](@entry_id:267781)。
  $$ \mathbf{J}_V = \begin{pmatrix} 0 \\ 1 \end{pmatrix} $$
- **与 $x$ 轴成 $\theta$ 角的线偏振光:**
  $$ \mathbf{J}_{\theta} = \begin{pmatrix} \cos\theta \\ \sin\theta \end{pmatrix} $$

#### 圆偏振光

当两个[电场](@entry_id:194326)分量的振[幅相](@entry_id:269870)等，且相位差恰好为 $\pm\pi/2$ 时，合成的[电场](@entry_id:194326)矢量尖端将描绘出一个圆形轨迹。这种光被称为**圆偏振光** (circularly polarized light)。对于一个琼斯矢量 $\mathbf{J} = \begin{pmatrix} a \\ b \end{pmatrix}$，其为[圆偏振光](@entry_id:198374)的充要条件是：$|a| = |b|$ 且 $\text{Re}(a^*b) = 0$ [@problem_id:2237361]。

根据[电场](@entry_id:194326)矢量旋转方向的惯例，我们定义：
- **[右旋圆偏振](@entry_id:267955)光 (RCP):** [电场](@entry_id:194326)矢量顺时针旋转（从观察者的角度看）。这对应于 $E_y$ 的相位滞后 $E_x$ $\pi/2$。
  $$ \mathbf{J}_R = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ -i \end{pmatrix} $$
  这正是我们在第一个例子中推导出的矢量 [@problem_id:2237419]。
- **左旋圆偏振光 (LCP):** [电场](@entry_id:194326)矢量逆时针旋转。这对应于 $E_y$ 的[相位超前](@entry_id:269084) $E_x$ $\pi/2$。
  $$ \mathbf{J}_L = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ i \end{pmatrix} $$

#### [椭圆偏振光](@entry_id:195140)

**[椭圆偏振光](@entry_id:195140)** (elliptically polarized light) 是最普遍的偏振形式，[线偏振](@entry_id:273116)和圆偏振都是其特例。当[电场](@entry_id:194326)两个分量的振幅不相等，和/或它们的相位差既不是 $0$ 或 $\pi$ 的整数倍，也不是 $\pi/2$ 的奇数倍时，就会产生[椭圆偏振光](@entry_id:195140)。例如，如果一束 $+45^\circ$ 的线偏振光通过一个使其垂直分量产生 $\pi/4$ [相位延迟](@entry_id:186355)的[波片](@entry_id:275054)，其出射光的琼斯矢量为 $\frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ e^{-i\pi/4} \end{pmatrix}$，这便是一个[椭圆偏振](@entry_id:270497)态 [@problem_id:2237400]。

### [琼斯矩阵](@entry_id:266533)：描述光学元件

琼斯代数的真正威力在于它能将光学元件对[偏振态](@entry_id:175130)的改变，模拟为简单的矩阵乘法。任何理想的、不引起退偏的线性光学元件都可以用一个 $2 \times 2$ 的**[琼斯矩阵](@entry_id:266533)** ([Jones matrix](@entry_id:266533)) $\mathbf{M}$ 来表示。如果入射光的琼斯矢量为 $\mathbf{J}_{\text{in}}$，则通过该元件后的出射光琼斯矢量 $\mathbf{J}_{\text{out}}$ 为：

$$
\mathbf{J}_{\text{out}} = \mathbf{M} \mathbf{J}_{\text{in}}
$$

#### 关键光学元件的[琼斯矩阵](@entry_id:266533)

- **[线性偏振片](@entry_id:195509) (Linear Polarizer):**
  一个理想的[线性偏振片](@entry_id:195509)只允许特定方向的[电场](@entry_id:194326)分量通过。对于一个透振轴与 $x$ 轴夹角为 $\theta$ 的偏振片，其[琼斯矩阵](@entry_id:266533)为 [@problem_id:2237434]：
  $$
  \mathbf{P}(\theta) = \begin{pmatrix} \cos^2\theta  \sin\theta\cos\theta \\ \sin\theta\cos\theta  \sin^2\theta \end{pmatrix}
  $$
  特殊情况包括：
  - 水平[偏振片](@entry_id:269119) ($\theta = 0$): $\mathbf{P}(0) = \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix}$
  - 垂直偏振片 ($\theta = \pi/2$): $\mathbf{P}(\pi/2) = \begin{pmatrix} 0  0 \\ 0  1 \end{pmatrix}$

- **[相位延迟器](@entry_id:175966) (Phase Retarder) / [波片](@entry_id:275054) (Wave Plate):**
  [相位延迟器](@entry_id:175966)是一种[双折射](@entry_id:167246)材料，它对其快轴和慢轴方向的偏振分量引入不同的相移。当快轴与坐标轴对齐时，其[琼斯矩阵](@entry_id:266533)是对角矩阵。例如，一个快轴沿 $x$ 轴（水平方向）的延迟器，它使 $y$ 分量相对于 $x$ 分量产生一个 $\delta$ 的相位延迟，其[琼斯矩阵](@entry_id:266533)为 [@problem_id:2237387] [@problem_id:2237400]：
  $$
  \mathbf{M}(\delta) = \begin{pmatrix} 1  0 \\ 0  e^{-i\delta} \end{pmatrix}
  $$
  这里我们遵循了相位“延迟”对应于负号相位的惯例。常用的[波片](@entry_id:275054)是该矩阵的特例：
  - **[半波片](@entry_id:164034) (Half-Wave Plate, HWP):** $\delta = \pi$。$\mathbf{M}_{\text{HWP}} = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$。
  - **[四分之一波片](@entry_id:262260) (Quarter-Wave Plate, QWP):** $\delta = \pi/2$。$\mathbf{M}_{\text{QWP}} = \begin{pmatrix} 1  0 \\ 0  -i \end{pmatrix}$。

#### 光学系统的本征态

在分析光学系统时，一个非常深刻的概念是**本征态** (eigenstates)，也称为[本征偏振](@entry_id:167256) (eigenpolarizations)。一个偏振态如果通过某个光学元件后，其偏振形式保持不变（仅可能附加一个全局相移），那么这个[偏振态](@entry_id:175130)就是该元件的一个[本征态](@entry_id:149904)。在数学上，[本征态](@entry_id:149904)是[琼斯矩阵](@entry_id:266533)的**本征矢量**。

以快轴水平的[半波片](@entry_id:164034)为例，其[琼斯矩阵](@entry_id:266533)为 $\mathbf{M}_{\text{HWP}} = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$ [@problem_id:2237405]。其本征矢量恰好是水平[偏振光](@entry_id:273160) $\begin{pmatrix} 1 \\ 0 \end{pmatrix}$（[本征值](@entry_id:154894)为 1）和垂直偏振光 $\begin{pmatrix} 0 \\ 1 \end{pmatrix}$（[本征值](@entry_id:154894)为 -1）。这意味着，当水平或垂直偏振光通过这个[半波片](@entry_id:164034)时，它们的偏振方向不会改变。而其他任何偏振态，如 $+45^\circ$ [线偏振光](@entry_id:165445) $\frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix}$，则会被改变为 $\frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ -1 \end{pmatrix}$（即 $-45^\circ$ [线偏振光](@entry_id:165445)），因此它不是该[半波片](@entry_id:164034)的[本征态](@entry_id:149904)。

### 偏振的矢量空间诠释与应用

琼斯代数最优雅的方面在于它将偏振态置于一个二维复矢量空间 $\mathbb{C}^2$ 中，这使得线性代数的强大工具得以应用。

#### 正交性与基底变换

在 $\mathbb{C}^2$ 空间中，我们可以定义两个琼斯矢量 $\mathbf{J}_1$ 和 $\mathbf{J}_2$ 的**[内积](@entry_id:158127)** (inner product)：

$$
\langle \mathbf{J}_1 | \mathbf{J}_2 \rangle = \mathbf{J}_1^\dagger \mathbf{J}_2
$$

其中 $\mathbf{J}_1^\dagger$ 是 $\mathbf{J}_1$ 的[厄米共轭](@entry_id:191215)（[转置](@entry_id:142115)并取复共轭）。如果 $\langle \mathbf{J}_1 | \mathbf{J}_2 \rangle = 0$，则称这两个偏振态是**正交的** (orthogonal)。物理上，这意味着一束处于 $|\mathbf{J}_2\rangle$ 态的光无法通过一个理想的 $|\mathbf{J}_1\rangle$ [偏振片](@entry_id:269119)。

最明显的正交基是水平和垂直偏振态：$\langle \mathbf{J}_H | \mathbf{J}_V \rangle = \begin{pmatrix} 1  0 \end{pmatrix} \begin{pmatrix} 0 \\ 1 \end{pmatrix} = 0$。同样，右旋和左旋圆偏振态也构成一组重要的正交基 [@problem_id:2237416]：

$$
\langle \mathbf{J}_R | \mathbf{J}_L \rangle = \frac{1}{\sqrt{2}}\begin{pmatrix} 1  i \end{pmatrix} \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ i \end{pmatrix} = \frac{1}{2}(1 + i^2) = 0
$$

任何[偏振态](@entry_id:175130)都可以表示为一组正交基的线性组合。例如，将水平偏振光分解到[圆偏振](@entry_id:261702)基上 [@problem_id:2237398]：
$$
\mathbf{J}_H = \frac{1}{\sqrt{2}}(\mathbf{J}_R + \mathbf{J}_L)
$$
这个简单的关系揭示了一个深刻的物理事实：[线偏振光](@entry_id:165445)可以被看作是等幅度的右旋和左旋[圆偏振光](@entry_id:198374)的叠加。

#### 计算透射强度

[内积](@entry_id:158127)的另一个关键应用是计算光通过偏振元件后的强度。如果一束归一化的入射光 $|\psi_{\text{in}}\rangle$ 通过一个理想的、只允许 $|\phi\rangle$ 态通过的偏振片，那么透射光的[复振幅](@entry_id:164138)为[内积](@entry_id:158127) $c = \langle \phi | \psi_{\text{in}} \rangle$。透射的**强度**与该振幅的模方成正比，即透射强度与初始强度的比值为：

$$
\frac{I_{\text{trans}}}{I_{\text{in}}} = |\langle \phi | \psi_{\text{in}} \rangle|^2
$$

这个规则是[马吕斯定律](@entry_id:272427) (Malus's Law) 的广义形式。考虑一个初始为任意[线偏振](@entry_id:273116)角 $\theta$ 的光束，其琼斯矢量为 $|\psi_{\text{in}}\rangle = \begin{pmatrix} \cos\theta \\ \sin\theta \end{pmatrix}$，当它通过一个理想的[右旋圆偏振](@entry_id:267955)片时，透射的强度比例为 [@problem_id:2237416] [@problem_id:2237383]：

$$
\frac{I_f}{I_0} = |\langle \mathbf{J}_R | \psi_{\text{in}} \rangle|^2 = \left| \frac{1}{\sqrt{2}}\begin{pmatrix} 1  i \end{pmatrix} \begin{pmatrix} \cos\theta \\ \sin\theta \end{pmatrix} \right|^2 = \left| \frac{1}{\sqrt{2}}(\cos\theta + i\sin\theta) \right|^2 = \left| \frac{1}{\sqrt{2}}e^{i\theta} \right|^2 = \frac{1}{2}
$$

这个结果出人意料地与初始线偏振角 $\theta$ 无关。它表明任何线偏振光都包含等量的右旋和左旋圆偏振分量，因此通过一个理想[圆偏振](@entry_id:261702)片后，强度总是减半。

琼斯代数还可以轻松处理非理想元件。假设一个不完美的[圆偏振](@entry_id:261702)片能透射 82% 的[右旋圆偏振](@entry_id:267955)光强度，而完全吸收左旋[圆偏振光](@entry_id:198374) [@problem_id:2237398]。当一束水平偏振光入射时，我们知道其强度在右旋和左旋分量上各占一半。因此，总的透射强度比例为：

$$
\frac{I_{\text{trans}}}{I_0} = 0.82 \times \frac{1}{2} + 0 \times \frac{1}{2} = 0.41
$$

综上所述，琼斯代数不仅为描述偏振态提供了精确的数学语言，还通过矩阵运算将光学元件的作用系统化，并通过矢量空间的[内积](@entry_id:158127)和投影，为计算强度和分析偏振变换提供了强有力的工具。它是现代[偏振光学](@entry_id:270461)中不可或缺的基础。