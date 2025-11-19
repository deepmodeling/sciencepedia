## 引言
在光学和电磁学领域，理解和操控光的偏振是众多现代技术的核心。然而，直接通过麦克斯韦方程组来分析偏振光与复杂光学系统相互作用的过程往往异常繁琐。为了解决这一难题，物理学家开发了琼斯微积分——一套强大而简洁的数学工具，它极大地简化了对完全偏振光的分析。

本文将系统性地引导你掌握琼斯微积分。在“原则与机制”一章中，我们将学习如何使用[琼斯矢量](@entry_id:176164)和矩阵来描述[偏振态](@entry_id:175130)和光学元件。接着，“应用与[交叉](@entry_id:147634)学科联系”一章将展示该工具在光学工程、[材料科学](@entry_id:152226)乃至量子信息等领域的实际应用。最后，“动手实践”部分将通过具体的计算问题，巩固你对理论的理解和应用能力。通过这三章的学习，你将能够建立起一个从基本原理到前沿应用的完整知识体系，为深入探索[光的偏振](@entry_id:262080)世界打下坚实的基础。

## 原则与机制

在对[电磁波](@entry_id:269629)，尤其是光波的研究中，偏振是一个描述其横向[电场](@entry_id:194326)矢量[振动](@entry_id:267781)方向的基本属性。虽然[光的波动性](@entry_id:141075)可以通过麦克斯韦方程组进行完备的描述，但在处理光与各种光学元件相互作用的实际问题时，直接求解波动方程往往极其繁琐。为了简化这一过程，物理学家们发展出了一套强大的数学工具。其中，**琼斯微积分** (Jones Calculus) 以其简洁和强大的功能，在描述完全[偏振光](@entry_id:273160)通过非散射、非吸收（或均匀吸收）光学系统时，成为了不可或缺的分析方法。本章将系统地阐述琼斯微积分的基本原则与核心机制。

### 表示[偏振光](@entry_id:273160)：[琼斯矢量](@entry_id:176164)

琼斯微积分的基石是**[琼斯矢量](@entry_id:176164)** (Jones Vector)，它是一种用二维复数向量来表示沿特定方向（通常约定为 $z$ 轴）传播的单色平面光[波的偏振](@entry_id:262733)状态的数学工具。对于一个在 $x-y$ 平面内[振动](@entry_id:267781)的[电场](@entry_id:194326) $\vec{E}$，其分量可以写成：
$E_x(z,t) = |E_x| \cos(\omega t - kz + \phi_x)$
$E_y(z,t) = |E_y| \cos(\omega t - kz + \phi_y)$

为了更便捷地处理相位关系，我们使用复数表示法。[电场](@entry_id:194326)可以表示为 $\vec{E} = \text{Re}(\vec{\mathcal{E}} e^{-i\omega t})$，其中[复振幅](@entry_id:164138)矢量 $\vec{\mathcal{E}}$ 包含了振幅和相位信息。[琼斯矢量](@entry_id:176164)正是这个[复振幅](@entry_id:164138)矢量在横向平面上的分量表示：

$$
\mathbf{J} = \begin{pmatrix} \mathcal{E}_x \\ \mathcal{E}_y \end{pmatrix} = \begin{pmatrix} |E_x| e^{i\phi_x} \\ |E_y| e^{i\phi_y} \end{pmatrix}
$$

这里，$|E_x|$ 和 $|E_y|$ 是[电场](@entry_id:194326)分量在 $x$ 和 $y$ 轴上的实振幅，而 $\phi_x$ 和 $\phi_y$ 是它们各自的相位。值得注意的是，[琼斯矢量](@entry_id:176164)只关心[电场](@entry_id:194326)分量的大小和它们的**[相对相位](@entry_id:148120)差** $\delta = \phi_y - \phi_x$ [@problem_id:1586916]。一个全局的相位因子 $e^{i\alpha}$ 乘以整个[琼斯矢量](@entry_id:176164)，即 $\begin{pmatrix} |E_x| e^{i(\phi_x+\alpha)} \\ |E_y| e^{i(\phi_y+\alpha)} \end{pmatrix}$，并不会改变光的偏振状态，因为它仅仅代表了整个波形在时间或空间上的一个整体平移。

例如，对于一个[琼斯矢量](@entry_id:176164) $\mathbf{J} = \begin{pmatrix} 1 \\ e^{i\pi/3} \end{pmatrix}$，我们可以将其分量写成 $E_x = 1 \cdot e^{i \cdot 0}$ 和 $E_y = 1 \cdot e^{i\pi/3}$。由此可知，其 $x$ 分量的相位 $\phi_x = 0$，$y$ 分量的相位 $\phi_y = \pi/3$。因此，相对相位差为 $\delta = \phi_y - \phi_x = \pi/3$ [@problem_id:1586916]。

光的强度与[电场](@entry_id:194326)振幅的平方成正比，在琼斯微积分中，我们通常将强度与[琼斯矢量](@entry_id:176164)的模的平方关联起来，即 $I \propto |E_x|^2 + |E_y|^2$。为了方便比较，我们常常使用**归一化[琼斯矢量](@entry_id:176164)**，其定义为满足 $|E_x|^2 + |E_y|^2 = 1$ 的矢量。

### 基本偏振态及其[琼斯矢量](@entry_id:176164)

任何完全偏振态都可以由一组正交的基底态[线性组合](@entry_id:154743)而成。最常用的一组基底是水平[线偏振](@entry_id:273116)和垂直线偏振。

**1. 线性偏振 (Linear Polarization)**

当[电场](@entry_id:194326)的两个分量同相 ($\delta = 0$) 或反相 ($\delta = \pi$) 时，[电场](@entry_id:194326)矢量末端的轨迹是一条直线，这种光被称为**线性偏振光**。
*   **水平[偏振光](@entry_id:273160)** (H-pol) 的[电场](@entry_id:194326)只在 $x$ 方向[振动](@entry_id:267781)，其归一化[琼斯矢量](@entry_id:176164)为：
    $$
    \mathbf{J}_H = \begin{pmatrix} 1 \\ 0 \end{pmatrix}
    $$
*   **垂直[偏振光](@entry_id:273160)** (V-pol) 的[电场](@entry_id:194326)只在 $y$ 方向[振动](@entry_id:267781)，其归一化[琼斯矢量](@entry_id:176164)为：
    $$
    \mathbf{J}_V = \begin{pmatrix} 0 \\ 1 \end{pmatrix}
    $$
这两个矢量构成了一个[正交基](@entry_id:264024)底。我们可以通过计算它们的**[内积](@entry_id:158127)** (inner product) 来验证其正交性。对于两个[琼斯矢量](@entry_id:176164) $\mathbf{A}$ 和 $\mathbf{B}$，其[内积](@entry_id:158127)定义为 $\mathbf{A}^\dagger \mathbf{B}$，其中 $\mathbf{A}^\dagger$ 是 $\mathbf{A}$ 的[共轭转置](@entry_id:147909)。对于 $\mathbf{J}_H$ 和 $\mathbf{J}_V$：
$$
\mathbf{J}_H^\dagger \mathbf{J}_V = \begin{pmatrix} 1^*  0^* \end{pmatrix} \begin{pmatrix} 0 \\ 1 \end{pmatrix} = \begin{pmatrix} 1  0 \end{pmatrix} \begin{pmatrix} 0 \\ 1 \end{pmatrix} = 1 \cdot 0 + 0 \cdot 1 = 0
$$
[内积](@entry_id:158127)为零证实了这两个[基态](@entry_id:150928)是正交的 [@problem_id:1586947]。

对于[振动](@entry_id:267781)方向与 $x$ 轴成 $\theta$ 角的线偏振光，其[电场](@entry_id:194326)分量振幅比为 $\tan\theta$。其归一化[琼斯矢量](@entry_id:176164)可以表示为：
$$
\mathbf{J}_\theta = \begin{pmatrix} \cos\theta \\ \sin\theta \end{pmatrix}
$$
一个实际的例子是，如果一束光通过一个透振轴方向由矢量 $\vec{v} = \hat{x} + 2\hat{y}$ 定义的[线性偏振片](@entry_id:195509)，那么出射光的[琼斯矢量](@entry_id:176164)将与此方向平行，即与 $\begin{pmatrix} 1 \\ 2 \end{pmatrix}$ 成比例。为了得到归一化矢量，我们需要除以其模长 $\sqrt{1^2 + 2^2} = \sqrt{5}$，从而得到归一化的[琼斯矢量](@entry_id:176164)为 $\begin{pmatrix} 1/\sqrt{5} \\ 2/\sqrt{5} \end{pmatrix}$ [@problem_id:1586910]。

**2. [圆偏振](@entry_id:261702) (Circular Polarization)**

当两个[电场](@entry_id:194326)分量的振[幅相](@entry_id:269870)等 ($|E_x| = |E_y|$) 且相对相位差为 $\pm \pi/2$ 时，[电场](@entry_id:194326)矢量末端会描绘出一个圆形轨迹，这便是**圆偏振光**。
*   **右[圆偏振光](@entry_id:198374)** (RCP)，按照物理学（从光源看向接收器）的普遍约定，当 $y$ 分量相位**滞后** $x$ 分量 $\pi/2$ ($\delta = -\pi/2$) 时，其归一化[琼斯矢量](@entry_id:176164)为：
    $$
    \mathbf{J}_R = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ e^{-i\pi/2} \end{pmatrix} = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ -i \end{pmatrix}
    $$
*   **左[圆偏振光](@entry_id:198374)** (LCP)，当 $y$ 分量相位**超前** $x$ 分量 $\pi/2$ ($\delta = +\pi/2$) 时，其归一化[琼斯矢量](@entry_id:176164)为：
    $$
    \mathbf{J}_L = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ e^{i\pi/2} \end{pmatrix} = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ i \end{pmatrix}
    $$

**3. [椭圆偏振](@entry_id:270497) (Elliptical Polarization)**

这是最普遍的偏振形式。当两个分量的振幅和相位关系不满足[线偏振](@entry_id:273116)或圆偏振的特殊条件时，[电场](@entry_id:194326)矢量末端将描绘出一个椭圆，称为**[椭圆偏振光](@entry_id:195140)**。[线偏振](@entry_id:273116)和圆偏振都可以视为[椭圆偏振](@entry_id:270497)的特例。

### 操控偏振：[琼斯矩阵](@entry_id:266533)

琼斯微积分的真正威力在于使用**[琼斯矩阵](@entry_id:266533)** (Jones Matrix) 来描述光学元件对偏振态的改变。当一束[偏振光](@entry_id:273160)（由[琼斯矢量](@entry_id:176164) $\mathbf{J}_{in}$ 描述）通过一个光学元件时，出射[光的偏振](@entry_id:262080)态 $\mathbf{J}_{out}$ 可以通过一个简单的[矩阵乘法](@entry_id:156035)得到：
$$
\mathbf{J}_{out} = \mathbf{M} \mathbf{J}_{in}
$$
其中 $\mathbf{M}$ 是一个 $2 \times 2$ 的复数矩阵，即该光学元件的[琼斯矩阵](@entry_id:266533)。下面我们介绍几种基本光学元件的[琼斯矩阵](@entry_id:266533)。

**1. [线性偏振片](@entry_id:195509) (Linear Polarizer)**

理想的**[线性偏振片](@entry_id:195509)**只允许特定方向（透振轴方向）的[电场](@entry_id:194326)分量通过，而完全阻挡与其正交的分量。对于一个透振轴与 $x$ 轴夹角为 $\theta$ 的[线性偏振片](@entry_id:195509)，其[琼斯矩阵](@entry_id:266533)为：
$$
\mathbf{P}(\theta) = \begin{pmatrix} \cos^2\theta  \cos\theta\sin\theta \\ \cos\theta\sin\theta  \sin^2\theta \end{pmatrix}
$$
这个矩阵具有一个重要的数学性质：它是一个**投影算符** (projection operator)，满足 $\mathbf{P}(\theta)^2 = \mathbf{P}(\theta)$ [@problem_id:1586914]。这个性质的物理意义是，一旦光通过一个偏振片被偏振后，再次通过一个相同方向的偏振片，其偏振状态将不再改变。例如，一束光连续通过两个透振轴均为 $\theta = \pi/3$ 的偏振片，其总效果等同于只通过一个[偏振片](@entry_id:269119) [@problem_id:1586914]。

**2. [相位延迟器](@entry_id:175966)/波片 (Phase Retarder / Wave Plate)**

**[波片](@entry_id:275054)**是由**双折射** (birefringent) 材料制成的光学元件。在这种材料中，沿着不同晶轴方向偏振的光会经历不同的[折射率](@entry_id:168910)。这导致了不同偏振分量之间产生一个相位差。[波片](@entry_id:275054)通常有两个[主轴](@entry_id:172691)：**快轴** (fast axis) 和**慢轴** (slow axis)，分别对应较小和较大的[折射率](@entry_id:168910)。

当[波片](@entry_id:275054)的快轴与 $x$ 轴重合时，它使得 $y$ 分量（沿慢轴）相对于 $x$ 分量（沿快轴）产生一个[相位延迟](@entry_id:186355) $\phi$。其[琼斯矩阵](@entry_id:266533)（忽略[全局相位](@entry_id:147947)）为：
$$
\mathbf{W}(\phi) = \begin{pmatrix} 1  0 \\ 0  e^{-i\phi} \end{pmatrix}
$$
这个[相位延迟](@entry_id:186355) $\phi$ 由材料的[双折射](@entry_id:167246)率差 $\Delta n = n_{slow} - n_{fast}$、波片厚度 $d$ 和光在真空中的波长 $\lambda_0$ 共同决定：
$$
\phi = \frac{2\pi}{\lambda_0} (n_{slow} - n_{fast}) d
$$
这个关系式是设计特定功能[波片](@entry_id:275054)的基础。例如，要将$45^\circ$[线偏振光](@entry_id:165445)转换为左圆偏振光，需要 $y$ 分量振幅与 $x$ 分量相等（由 $45^\circ$ [入射角](@entry_id:192705)保证），且 $y$ 分量[相位超前](@entry_id:269084) $x$ 分量 $\pi/2$。如果快轴在 $x$ 方向，慢轴在 $y$ 方向，我们需要一个使得 $\phi = -\pi/2$（或等效的 $3\pi/2$ 等）的延迟。通过上述公式，我们可以计算出实现这一目标所需的晶体最小厚度 [@problem_id:1806669]。

两种常见的[波片](@entry_id:275054)是：
*   **[半波片](@entry_id:164034) (HWP)**：引入 $\phi = \pi$ 的相位差，其矩阵为 $\mathbf{W}(\pi) = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$。它的作用是将线偏振光的偏振方向相对于快轴做[镜像对称](@entry_id:158730)变换。
*   **[四分之一波片](@entry_id:262260) (QWP)**：引入 $\phi = \pi/2$ 的相位差，其矩阵为 $\mathbf{W}(\pi/2) = \begin{pmatrix} 1  0 \\ 0  -i \end{pmatrix}$。它常被用来将[线偏振光](@entry_id:165445)转换为[圆偏振光](@entry_id:198374)，反之亦然。

理想的非吸收性光学元件，如[波片](@entry_id:275054)，其[琼斯矩阵](@entry_id:266533)是**幺正**的 (unitary)，即 $\mathbf{M}^\dagger \mathbf{M} = \mathbf{I}$ ([单位矩阵](@entry_id:156724))。这意味着出射光的强度等于入射光的强度 ($I_{out} = I_{in}$)，因为 $I_{out} \propto \mathbf{J}_{out}^\dagger \mathbf{J}_{out} = (\mathbf{M}\mathbf{J}_{in})^\dagger (\mathbf{M}\mathbf{J}_{in}) = \mathbf{J}_{in}^\dagger \mathbf{M}^\dagger \mathbf{M} \mathbf{J}_{in} = \mathbf{J}_{in}^\dagger \mathbf{J}_{in} \propto I_{in}$ [@problem_id:1586920]。这与[偏振片](@entry_id:269119)形成鲜明对比，[偏振片](@entry_id:269119)通常是吸收性的，其矩阵不是幺正的。

### 进阶应用与分析

**1. 级联系统 (Cascaded Systems)**

当光束依次通过多个光学元件时，整个系统的总[琼斯矩阵](@entry_id:266533)是各个元件[琼斯矩阵](@entry_id:266533)的乘积。重要的是，矩阵的乘法顺序与光通过元件的顺序相反：
$$
\mathbf{M}_{total} = \mathbf{M}_n \cdots \mathbf{M}_2 \mathbf{M}_1
$$
其中 $\mathbf{M}_1$ 是光首先遇到的元件。

我们可以通过一个例子来理解这个过程：一束[非偏振光](@entry_id:176162)先后通过一个透振轴在$30^\circ$的[偏振片](@entry_id:269119) (LP1)，一个快轴水平的[四分之一波片](@entry_id:262260) (QWP)，以及一个透振轴角度可变的检偏器 (LP2)。要找到透射光强最大的检偏器角度 $\phi$，我们按部就班地追踪[琼斯矢量](@entry_id:176164)的变化。
1.  经过 LP1 后，光变为线偏振光，[琼斯矢量](@entry_id:176164)为 $\mathbf{J}_1 = \begin{pmatrix} \cos(30^\circ) \\ \sin(30^\circ) \end{pmatrix} = \begin{pmatrix} \sqrt{3}/2 \\ 1/2 \end{pmatrix}$。
2.  接着通过 QWP，其矩阵为 $\mathbf{M}_{QWP} = \begin{pmatrix} 1  0 \\ 0  -i \end{pmatrix}$。出射光的[琼斯矢量](@entry_id:176164)为 $\mathbf{J}_2 = \mathbf{M}_{QWP} \mathbf{J}_1 = \begin{pmatrix} \sqrt{3}/2 \\ -i/2 \end{pmatrix}$。这是一种[椭圆偏振光](@entry_id:195140)。
3.  最后，光通过检偏器 LP2，其作用是把 $\mathbf{J}_2$ 投影到它的透振轴 $\mathbf{a}(\phi) = \begin{pmatrix} \cos\phi \\ \sin\phi \end{pmatrix}$ 上。透射光的[复振幅](@entry_id:164138)为 $A(\phi) = \mathbf{a}(\phi)^T \mathbf{J}_2$，强度与 $|A(\phi)|^2$ 成正比。通过计算并最大化这个强度表达式，可以找到最佳的检偏器角度 [@problem_id:1806655]。

**2. 旋转光学元件 (Rotated Components)**

如果一个光学元件的主轴（例如[偏振片](@entry_id:269119)的透振轴或波片的快轴）没有对准坐标轴，我们该如何写出它的[琼斯矩阵](@entry_id:266533)？答案是使用一个[坐标旋转](@entry_id:164444)变换。若一个元件在[主轴](@entry_id:172691)[坐标系](@entry_id:156346)下的矩阵为 $\mathbf{M}_0$，而其[主轴](@entry_id:172691)相对于实验室坐标系的 $x$ 轴旋转了 $\theta$ 角，则它在[实验室坐标系](@entry_id:166991)下的矩阵 $\mathbf{M}$ 为：
$$
\mathbf{M} = \mathbf{R}(\theta) \mathbf{M}_0 \mathbf{R}(-\theta)
$$
其中 $\mathbf{R}(\theta) = \begin{pmatrix} \cos\theta  -\sin\theta \\ \sin\theta  \cos\theta \end{pmatrix}$ 是[坐标系](@entry_id:156346)的[旋转矩阵](@entry_id:140302)。这个公式的直观理解是：首先将入射光的[琼斯矢量](@entry_id:176164)旋转 $-\theta$ 到元件的主轴[坐标系](@entry_id:156346)，然后应用简单的矩阵 $\mathbf{M}_0$，最后再将结果旋转 $\theta$ 回到实验室坐标系 [@problem_id:1586908]。

**3. 偏振的本征态 (Eigenstates of Polarization)**

对于一个给定的光学元件，是否存在某些特殊的[偏振态](@entry_id:175130)，使得光在通过该元件后，其偏振形式保持不变（仅可能有一个整体的相位变化）？答案是肯定的，这些状态被称为该元件的**偏振本征态** (eigenstates of polarization)。在数学上，它们对应于该元件[琼斯矩阵](@entry_id:266533)的**本征矢量** (eigenvectors)。
$$
\mathbf{M} \mathbf{J}_{eigen} = \lambda \mathbf{J}_{eigen}
$$
其中 $\mathbf{J}_{eigen}$ 是本征态对应的[琼斯矢量](@entry_id:176164)，$\lambda$ 是复数**[本征值](@entry_id:154894)** (eigenvalue)，其模长代表振幅的变化，相位代表整体相移。

以一个快轴沿垂直 ($y$ 轴) 方向的[半波片](@entry_id:164034)为例 [@problem_id:1586921]。此时慢轴在 $x$ 轴方向，相比快轴有 $\pi$ 的[相位延迟](@entry_id:186355)。其[琼斯矩阵](@entry_id:266533)为（忽略[全局相位](@entry_id:147947)）:
$$
\mathbf{M}_{HWP,y} = \begin{pmatrix} e^{-i\pi}  0 \\ 0  1 \end{pmatrix} = \begin{pmatrix} -1  0 \\ 0  1 \end{pmatrix}
$$
不难发现，该矩阵的本征矢量是：
*   $\mathbf{J}_H = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$，对应[本征值](@entry_id:154894) $\lambda = -1$。
*   $\mathbf{J}_V = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$，对应[本征值](@entry_id:154894) $\lambda = 1$。
这表明，对于这个[半波片](@entry_id:164034)，水平线偏振光和垂直[线[偏振](@entry_id:165445)光](@entry_id:273160)是它的[本征态](@entry_id:149904)。当这两种偏振光通过该[半波片](@entry_id:164034)时，它们的偏振形式（[线偏振](@entry_id:273116)）和方向（水平或垂直）都保持不变，仅仅是获得了一个整体的相位因子。而其他任何偏振态，如$45^\circ$线偏振光或圆偏振光，在通过该[半波片](@entry_id:164034)后，其偏振形式都会发生改变，因此它们不是该元件的本征态 [@problem_id:1586921]。

本征态的概念为我们理解和设计光学系统提供了更深层次的视角，它揭示了光与物质相互作用中固有的对称性和[不变性](@entry_id:140168)。

综上所述，琼斯微积分通过将[偏振态](@entry_id:175130)抽象为复数矢量，将光学元件的作用抽象为[矩阵变换](@entry_id:156789)，为[偏振光学](@entry_id:270461)的分析和计算提供了一个既严谨又高效的框架。从描述基本的[偏振态](@entry_id:175130)，到分析复杂光学系统的行为，再到揭示偏振的本征态，琼斯微积分为我们深入探索光的奥秘铺平了道路。