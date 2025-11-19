## 引言
[光的偏振](@entry_id:262080)是[电磁波](@entry_id:269629)最基本的性质之一，精确地描述和控制光的偏振态在现代科学和技术中至关重要。从液晶显示屏到先进的量子通信，对偏振的精细操控是实现其功能的核心。然而，当光与各种光学元件（如偏振片、[波片](@entry_id:275054)或生物组织）相互作用时，其偏振态会发生复杂的变化。这提出了一个关键问题：我们如何建立一个系统性的数学框架来预测和分析这些变化？

本文旨在全面介绍解决这一问题的两种强大矩阵方法：[琼斯矢量](@entry_id:176164)算法和穆勒-斯托克斯体系。通过学习本文，您将能够掌握描述和计算[偏振光](@entry_id:273160)行为的完整工具集。在“原理与机制”一章中，我们将奠定理论基础，深入探讨如何用[琼斯矢量](@entry_id:176164)和[斯托克斯矢量](@entry_id:168374)分别表示完全[偏振光](@entry_id:273160)和任意[偏振光](@entry_id:273160)，并学习如何用相应的矩阵来模拟光学元件。随后，在“应用与跨学科联系”一章中，我们将展示这些数学工具的巨大威力，探索它们在[光学系统设计](@entry_id:164820)、[材料科学](@entry_id:152226)、生物[光子](@entry_id:145192)学乃至[量子信息](@entry_id:137721)等前沿领域的实际应用。最后，通过“动手实践”部分，您将有机会运用所学知识解决具体问题，巩固并深化对这些核心概念的理解。

## 原理与机制

在理解了偏振作为[电磁波](@entry_id:269629)的基本属性之后，本章将深入探讨描述和操纵偏振态的数学工具。我们将介绍两种核心的矩阵方法：[琼斯矢量](@entry_id:176164)算法（[Jones calculus](@entry_id:182044)）和穆勒-斯托克斯体系（Mueller-Stokes formalism）。琼斯算法以其简洁性在处理完全偏振光方面表现出色，而穆勒体系则提供了一个更通用的框架，能够描述包括[部分偏振光](@entry_id:267467)和[非偏振光](@entry_id:176162)在内的任何偏振状态。通过掌握这些方法，我们不仅能够精确地描述[光的偏振](@entry_id:262080)，还能预测光与各种光学元件相互作用后的行为。

### 表示偏振光：[琼斯矢量](@entry_id:176164)算法

[琼斯矢量](@entry_id:176164)算法是由 R. Clark Jones 在20世纪40年代发展的，它为描述沿特定方向传播的[单色平面波](@entry_id:264838)的偏振状态提供了一种优雅的数学语言。该方法的核心在于将光的[电场](@entry_id:194326)矢量在垂直于传播方向的平面内的分量表示为一个二维复数矢量。

#### [琼斯矢量](@entry_id:176164)

假设一束[单色光](@entry_id:178750)沿 $z$ 轴正方向传播，其[电场](@entry_id:194326)矢量 $\mathbf{E}$ 在 $x-y$ 平面内[振荡](@entry_id:267781)。这个[电场](@entry_id:194326)可以分解为两个正交分量：

$E_x(z, t) = E_{0x} \cos(kz - \omega t + \phi_x)$
$E_y(z, t) = E_{0y} \cos(kz - \omega t + \phi_y)$

其中，$E_{0x}$ 和 $E_{0y}$ 是沿 $x$ 和 $y$ 轴的振幅，$\phi_x$ 和 $\phi_y$ 是相应的相位。[琼斯矢量](@entry_id:176164)算法通过提取这些分量的[复振幅](@entry_id:164138)来捕捉偏振信息。一个**[琼斯矢量](@entry_id:176164) ([Jones vector](@entry_id:265773))** 定义为一个二维列矢量：

$ \mathbf{J} = \begin{pmatrix} E_x \\ E_y \end{pmatrix} = \begin{pmatrix} E_{0x} \exp(i\phi_x) \\ E_{0y} \exp(i\phi_y) \end{pmatrix} $

这个矢量包含了描述偏振状态所需的所有信息：两个分量的相对振幅 ($E_{0x}/E_{0y}$) 和它们的[相对相位](@entry_id:148120) ($\delta = \phi_y - \phi_x$)。值得注意的是，[琼斯矢量](@entry_id:176164)只适用于**完全偏振光 (fully polarized light)**，即[电场](@entry_id:194326)矢量的尖端在空间中描绘出一个确定的、不随时间改变形状的轨迹（线、圆或椭圆）。

#### 常见的偏振态

利用[琼斯矢量](@entry_id:176164)，我们可以简洁地表示各种基本[偏振态](@entry_id:175130)。

*   **[线偏振光](@entry_id:165445) (Linearly Polarized Light):** 当两个分量同相或反相时（即相对相位差 $\delta=0$ 或 $\delta=\pi$），合成的[电场](@entry_id:194326)沿一条直线[振荡](@entry_id:267781)。若[电场](@entry_id:194326)[振荡](@entry_id:267781)方向与 $x$ 轴成 $\theta$ 角，则 $E_{0y}/E_{0x} = \tan\theta$。忽略一个[整体相位](@entry_id:147947)因子并将总强度归一化后，其[琼斯矢量](@entry_id:176164)可以写为：

    $ \mathbf{J}_{\text{lin}}(\theta) = \begin{pmatrix} \cos\theta \\ \sin\theta \end{pmatrix} $

    例如，水平偏振光（$\theta=0^\circ$）为 $\begin{pmatrix} 1 \\ 0 \end{pmatrix}$，垂直偏振光（$\theta=90^\circ$）为 $\begin{pmatrix} 0 \\ 1 \end{pmatrix}$。对于与 $x$ 轴成 $135^\circ$ 角的[线偏振光](@entry_id:165445)，其归一化[琼斯矢量](@entry_id:176164)为 [@problem_id:1806667]：

    $ \mathbf{J} = \begin{pmatrix} \cos(135^\circ) \\ \sin(135^\circ) \end{pmatrix} = \begin{pmatrix} -1/\sqrt{2} \\ 1/\sqrt{2} \end{pmatrix} $

*   **圆偏振光 (Circularly Polarized Light):** 当两个分量的振[幅相](@entry_id:269870)等（$E_{0x}=E_{0y}$）且相对相位差为 $\pm \pi/2$ 时，[电场](@entry_id:194326)矢量的尖端会描绘出一个圆形。根据[电场](@entry_id:194326)旋转的方向，我们区分两种旋向：

    *   **右旋圆偏振光 (Right-Circularly Polarized, RCP):** $y$ 分量相比 $x$ 分量[相位滞后](@entry_id:172443) $\pi/2$ ($\delta = -\pi/2$)。其归一化[琼斯矢量](@entry_id:176164)为 $\frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ -i \end{pmatrix}$。
    *   **左旋圆偏振光 (Left-Circularly Polarized, LCP):** $y$ 分量相比 $x$ 分量[相位超前](@entry_id:269084) $\pi/2$ ($\delta = +\pi/2$)。其归一化[琼斯矢量](@entry_id:176164)为 $\frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ i \end{pmatrix}$。

*   **[椭圆偏振光](@entry_id:195140) (Elliptically Polarized Light):** 这是最一般的情况，当振幅和相位关系不满足线偏振或[圆偏振](@entry_id:261702)的特定条件时，[电场](@entry_id:194326)矢量尖端描绘出一个椭圆。

#### 光强与归一化

[琼斯矢量](@entry_id:176164)所描述的光波的总**光强 (intensity)** $I$ 与[电场](@entry_id:194326)分量振幅的平方和成正比：

$ I \propto |E_x|^2 + |E_y|^2 = \mathbf{J}^\dagger \mathbf{J} $

其中 $\mathbf{J}^\dagger$ 是[琼斯矢量](@entry_id:176164)的[厄米共轭](@entry_id:191215)（[转置](@entry_id:142115)并取复共轭）。在许多情况下，我们更关心偏振的“状态”而非其绝对强度。此时，我们可以使用**归一化[琼斯矢量](@entry_id:176164) (normalized [Jones vector](@entry_id:265773))**，其分量满足 $|E_x|^2 + |E_y|^2 = 1$。这相当于将总强度设为单位1。

### 模拟光学元件：[琼斯矩阵](@entry_id:266533)

[琼斯矢量](@entry_id:176164)算法的真正威力在于它能够通过矩阵运算来描述光与光学元件的相互作用。一个线性的、非散射的、非 depolarizing 的光学元件对光[偏振态](@entry_id:175130)的改变，可以由一个 2x2 的复数矩阵——**[琼斯矩阵](@entry_id:266533) ([Jones matrix](@entry_id:266533))** $\mathbf{J}_{\text{elem}}$ 来描述。如果入射光的[琼斯矢量](@entry_id:176164)是 $\mathbf{J}_{\text{in}}$，那么出射光的[琼斯矢量](@entry_id:176164) $\mathbf{J}_{\text{out}}$ 就是：

$ \mathbf{J}_{\text{out}} = \mathbf{J}_{\text{elem}} \mathbf{J}_{\text{in}} $

#### 关键光学元件

让我们来看看一些常见光学元件的[琼斯矩阵](@entry_id:266533)。

*   **[线性偏振片](@entry_id:195509) (Linear Polarizer):** 一个理想的[线性偏振片](@entry_id:195509)只允许特定方向的[电场](@entry_id:194326)分量通过，而完全阻挡与其正交的分量。一个透[光轴](@entry_id:175875)沿 $x$ 轴的水平[偏振片](@entry_id:269119)，其[琼斯矩阵](@entry_id:266533)为：

    $ \mathbf{J}_{\text{LP, horiz}} = \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix} $

*   **[相位延迟器](@entry_id:175966) (Phase Retarder) / 波片 (Wave Plate):** 这类元件由双折射材料制成，它对沿着两个相互正交的轴（快轴和慢轴）偏振的光有不同的[折射率](@entry_id:168910)。这导致光通过后，沿这两个轴的分量之间产生一个相位差 $\delta$。如果快轴沿 $x$ 轴，慢轴沿 $y$ 轴，那么 $y$ 分量的相位相对于 $x$ 分量将被延迟 $\delta$。其[琼斯矩阵](@entry_id:266533)为：

    $ \mathbf{W}(\delta) = \begin{pmatrix} 1  0 \\ 0  \exp(-i\delta) \end{pmatrix} $

    两个重要的特例是：
    *   **[四分之一波片](@entry_id:262260) (Quarter-Wave Plate, QWP):** 引入 $\pi/2$ 的相位差 ($\delta = \pi/2$)。其矩阵为 $\mathbf{J}_{\text{QWP}} = \begin{pmatrix} 1  0 \\ 0  -i \end{pmatrix}$。QWP 能将[线偏振光](@entry_id:165445)转换为[圆偏振光](@entry_id:198374)（反之亦然）。
    *   **[半波片](@entry_id:164034) (Half-Wave Plate, HWP):** 引入 $\pi$ 的相位差 ($\delta = \pi$)。其矩阵为 $\mathbf{J}_{\text{HWP}} = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$。HWP 能将线偏振光的偏振方向旋转一个角度。

*   **[旋光](@entry_id:201162)器 (Optical Rotator):** 这类元件（如法拉第旋光器或含手性分子的溶液）能将线偏振光的偏振平面旋转一个角度 $\beta$。其[琼斯矩阵](@entry_id:266533)是一个实值的旋转矩阵：

    $ \mathbf{R}(\beta) = \begin{pmatrix} \cos\beta  -\sin\beta \\ \sin\beta  \cos\beta \end{pmatrix} $

### 使用[琼斯矢量](@entry_id:176164)[算法分析](@entry_id:264228)光学系统

#### 级联系统

当光束依次通过多个光学元件时，整个系统的效果可以通过矩阵的连续相乘来计算。如果光束依次通过[琼斯矩阵](@entry_id:266533)为 $\mathbf{J}_1, \mathbf{J}_2, \ldots, \mathbf{J}_n$ 的元件，那么总的系统[琼斯矩阵](@entry_id:266533) $\mathbf{J}_{\text{sys}}$ 是这些矩阵按**与[光传播](@entry_id:276328)方向相反的顺序**相乘：

$ \mathbf{J}_{\text{sys}} = \mathbf{J}_n \cdots \mathbf{J}_2 \mathbf{J}_1 $

最终的出射光矢量为 $\mathbf{J}_{\text{out}} = \mathbf{J}_{\text{sys}} \mathbf{J}_{\text{in}}$。

一个典型的应用是计算通过一个由偏振片、[波片](@entry_id:275054)和检偏器组成的系统的光强。例如，我们可以分析一个系统，其中光束先通过一个30°的偏振片，然后通过一个快轴水平的QWP，最后通过一个角度为 $\phi$ 的检偏器。通过计算最终[琼斯矢量](@entry_id:176164)的模平方，可以发现最终透射强度与检偏器角度 $\phi$ 的关系，并找到使光强最大化的角度 [@problem_id:1806655]。

另一个重要应用是设计光学元件。例如，要将45°[线偏振光](@entry_id:165445)转换为左旋[圆偏振光](@entry_id:198374)，我们需要引入 $\pi/2$ 的相位差。这可以通过使用一块特定厚度的[双折射晶体](@entry_id:271690)（即一个QWP）来实现。所需厚度 $d$ 直接与晶体的[折射率](@entry_id:168910)差 $(n_y - n_x)$ 和光的波长 $\lambda_0$ 相关，即 $d = \lambda_0 / [4(n_y - n_x)]$ [@problem_id:1806669]。

#### 处理旋转元件

在实际应用中，光学元件的快轴或透[光轴](@entry_id:175875)不一定总是与坐标轴对齐。如果一个[琼斯矩阵](@entry_id:266533)为 $\mathbf{J}$ 的元件被逆时针旋转了 $\theta$ 角，那么其新的[琼斯矩阵](@entry_id:266533) $\mathbf{J}'$ 可以通过一个[相似变换](@entry_id:152935)得到：

$ \mathbf{J}' = \mathbf{R}(\theta) \mathbf{J} \mathbf{R}(-\theta) $

其中 $\mathbf{R}(\theta)$ 是前面定义的旋转矩阵。这个强大的规则使我们能够分析任意方向元件组成的复杂系统。例如，我们可以计算光通过一个水平QWP，再通过一个旋转了30°的QWP后的最终[状态和](@entry_id:193625)强度 [@problem_id:1806688]。

特别值得注意的是，有些元件具有[非互易性](@entry_id:168607)。一个典型的例子是**法拉第旋光器 (Faraday rotator)**，无论光的传播方向如何，它都以相同的物理方向（例如，从上方看总是顺时针）旋转偏振面。这意味着，如果光正向通过它旋转了 $\beta$，反射回来反向通过它时，会再旋转一个 $\beta$，总旋转角度为 $2\beta$，而不是像互易元件那样旋转 $\beta$ 再转回 $-\beta$ 而抵消。这个特性在[光隔离器](@entry_id:266842)等设备中有重要应用 [@problem_id:1806652]。

### 超越完全偏振光：穆勒-斯托克斯体系

#### 琼斯算法的局限性与通用体系的需求

[琼斯矢量](@entry_id:176164)算法功能强大，但它有一个根本性的限制：它只能描述**完全[偏振光](@entry_id:273160)**。自然界和实验室中的许多光源，如白炽灯、[发光二极管](@entry_id:158696)或多模[激光](@entry_id:194225)器，会发出**非偏振光 (unpolarized light)** 或**[部分偏振光](@entry_id:267467) (partially polarized light)**。对于这些情况，[电场](@entry_id:194326)矢量的振幅和相位随时间快速随机变化，无法用单一的[琼斯矢量](@entry_id:176164)来描述。为了处理这些更普遍的情况，我们需要一个基于可测量强度的更通用的框架，这就是穆勒-斯托克斯体系。

#### [斯托克斯矢量](@entry_id:168374)与[部分偏振](@entry_id:187644)

1852年，George Gabriel Stokes 引入了一组四个参数，即**斯托克斯参数 (Stokes parameters)**，它们完全可以表征任何光束的偏振状态。这些参数是通过一系列强度测量来定义的：

*   $S_0$：光束的总强度。
*   $S_1$：水平偏振光强度 ($I_H$) 与垂直[偏振光](@entry_id:273160)强度 ($I_V$)之差，$S_1 = I_H - I_V$。
*   $S_2$：$+45^\circ$线偏振光强度 ($I_{+45}$) 与$-45^\circ$[线偏振光](@entry_id:165445)强度 ($I_{-45}$)之差，$S_2 = I_{+45} - I_{-45}$。
*   $S_3$：右旋圆偏振[光强度](@entry_id:177094) ($I_R$) 与左旋圆偏振光强度 ($I_L$)之差，$S_3 = I_R - I_L$。

这四个实数量被组合成一个列矢量，称为**[斯托克斯矢量](@entry_id:168374) (Stokes vector)**:

$ \mathbf{S} = \begin{pmatrix} S_0 \\ S_1 \\ S_2 \\ S_3 \end{pmatrix} $

以下是一些基本偏振态的[斯托克斯矢量](@entry_id:168374)（强度为 $I_0$）：
*   水平线偏振光: $\begin{pmatrix} I_0  I_0  0  0 \end{pmatrix}^T$
*   $+45^\circ$线偏振光: $\begin{pmatrix} I_0  0  I_0  0 \end{pmatrix}^T$
*   [右旋圆偏振](@entry_id:267955)光: $\begin{pmatrix} I_0  0  0  I_0 \end{pmatrix}^T$
*   左旋圆偏振光: $\begin{pmatrix} I_0  0  0  -I_0 \end{pmatrix}^T$ [@problem_id:1806657]
*   [非偏振光](@entry_id:176162): $\begin{pmatrix} I_0  0  0  0 \end{pmatrix}^T$

该体系的关键优势在于处理**非相干叠加 (incoherent superposition)**。当两束光非相干地（即没有固定的相位关系）混合时，合成光的[斯托克斯矢量](@entry_id:168374)就是各分量[斯托克斯矢量](@entry_id:168374)的简单相加。例如，一束由等强度的[非偏振光](@entry_id:176162)和$+45^\circ$线偏振光混合而成的光，如果总强度为 $I_0$，其[斯托克斯矢量](@entry_id:168374)为 [@problem_id:1806653]：

$ \mathbf{S} = \mathbf{S}_{\text{unpol}} + \mathbf{S}_{+45} = \begin{pmatrix} I_0/2 \\ 0 \\ 0 \\ 0 \end{pmatrix} + \begin{pmatrix} I_0/2 \\ 0 \\ I_0/2 \\ 0 \end{pmatrix} = \begin{pmatrix} I_0 \\ 0 \\ I_0/2 \\ 0 \end{pmatrix} $

#### [偏振度](@entry_id:276690)

对于任何[斯托克斯矢量](@entry_id:168374)，参数之间存在一个重要关系：$S_0^2 \ge S_1^2 + S_2^2 + S_3^2$。等号成立时，光是完全偏振的。不等号表示光是[部分偏振](@entry_id:187644)的。我们可以定义一个**[偏振度](@entry_id:276690) (Degree of Polarization, DoP)** $\mathcal{P}$ 来量化光束中偏振成分的比例：

$ \mathcal{P} = \frac{\sqrt{S_1^2 + S_2^2 + S_3^2}}{S_0} $

$\mathcal{P}$ 的取值范围为0到1，$\mathcal{P}=0$ 对应[非偏振光](@entry_id:176162)，$\mathcal{P}=1$ 对应完全[偏振光](@entry_id:273160)，而 $0  \mathcal{P}  1$ 对应[部分偏振光](@entry_id:267467)。任何[部分偏振光](@entry_id:267467)都可以被看作是完全[偏振光](@entry_id:273160)和[非偏振光](@entry_id:176162)的非相干叠加。

例如，考虑一束由强度为 $I_U$ 的[非偏振光](@entry_id:176162)和强度为 $I_P$ 的线偏振光组成的混合光束。总光束的[偏振度](@entry_id:276690)可以直接计算为 $\mathcal{P} = I_P / (I_U + I_P)$。有趣的是，当这样一束光通过一个理想的QWP时，虽然其偏振形式会改变（例如从部分线性变为部分椭圆），但其[偏振度](@entry_id:276690)保持不变 [@problem_id:1806681]。

### 使用[穆勒矩阵](@entry_id:274422)建模

与[琼斯矢量](@entry_id:176164)算法类似，光学元件在穆勒-斯托克斯体系中由4x4的实数矩阵——**[穆勒矩阵](@entry_id:274422) (Mueller matrix)** $\mathbf{M}$ 来描述。出射光的[斯托克斯矢量](@entry_id:168374) $\mathbf{S}_{\text{out}}$ 与入射光的[斯托克斯矢量](@entry_id:168374) $\mathbf{S}_{\text{in}}$ 的关系为：

$ \mathbf{S}_{\text{out}} = \mathbf{M} \mathbf{S}_{\text{in}} $

对于级联系统，系统总的[穆勒矩阵](@entry_id:274422)同样是各个元件矩阵按相反顺序的乘积 $\mathbf{M}_{\text{sys}} = \mathbf{M}_n \cdots \mathbf{M}_2 \mathbf{M}_1$。

#### 关键元件的[穆勒矩阵](@entry_id:274422)

*   **理想[线性偏振片](@entry_id:195509) (Ideal Linear Polarizer):** 透光轴与水平方向成 $\theta$ 角的偏振片：

    $ \mathbf{M}_{\text{LP}}(\theta) = \frac{1}{2} \begin{pmatrix} 1  \cos(2\theta)  \sin(2\theta)  0 \\ \cos(2\theta)  \cos^2(2\theta)  \cos(2\theta)\sin(2\theta)  0 \\ \sin(2\theta)  \cos(2\theta)\sin(2\theta)  \sin^2(2\theta)  0 \\ 0  0  0  0 \end{pmatrix} $

*   **理想[相位延迟器](@entry_id:175966) (Ideal Retarder):** 快轴与水平方向成 $\theta$ 角，[相位延迟](@entry_id:186355)为 $\delta$：

    $ \mathbf{M}_{\text{Ret}}(\theta, \delta) = \begin{pmatrix} 1  0  0  0 \\ 0  \cos^2(2\theta) + \sin^2(2\theta)\cos\delta  \cos(2\theta)\sin(2\theta)(1-\cos\delta)  -\sin(2\theta)\sin\delta \\ 0  \cos(2\theta)\sin(2\theta)(1-\cos\delta)  \sin^2(2\theta) + \cos^2(2\theta)\cos\delta  \cos(2\theta)\sin\delta \\ 0  \sin(2\theta)\sin\delta  -\cos(2\theta)\sin\delta  \cos\delta \end{pmatrix} $

    这个通用形式可以生成QWP（$\delta=\pi/2$）和HWP（$\delta=\pi$）的矩阵。例如，对于一个快轴方向为 $\theta$ 的[半波片](@entry_id:164034)，其[穆勒矩阵](@entry_id:274422)会耦合 $S_1$ 和 $S_2$ 参数。我们可以通过分析矩阵元素来量化这种耦合效应 [@problem_id:1806704]。

*   **理想旋光器 (Ideal Rotator):** 将偏振面旋转 $\alpha$ 角：

    $ \mathbf{M}_{\text{Rot}}(\alpha) = \begin{pmatrix} 1  0  0  0 \\ 0  \cos(2\alpha)  \sin(2\alpha)  0 \\ 0  -\sin(2\alpha)  \cos(2\alpha)  0 \\ 0  0  0  1 \end{pmatrix} $

    这个矩阵形式清晰地表明，旋光器在 $(S_1, S_2)$ 平面上执行了一个角度为 $2\alpha$ 的旋转，同时保持总强度 $S_0$ 和[圆偏振](@entry_id:261702)分量 $S_3$ 不变。这个特性可以用来从实验测量中识别和量化[旋光](@entry_id:201162)元件。如果一个未知元件保持 $S_0$ 和 $S_3$ 不变，同时将水平偏振光变为15°线偏振光，将45°[线偏振光](@entry_id:165445)变为60°[线偏振光](@entry_id:165445)，我们可以断定它是一个旋光角为15°的旋光器 [@problem_id:1806697]。

#### [琼斯矩阵](@entry_id:266533)与[穆勒矩阵](@entry_id:274422)的关系

对于可以由[琼斯矩阵](@entry_id:266533) $\mathbf{J}$ 描述的非 depolarizing 元件，其对应的[穆勒矩阵](@entry_id:274422) $\mathbf{M}$ 可以通过以下代数关系导出：

$ \mathbf{M} = \mathbf{A} (\mathbf{J} \otimes \mathbf{J}^*) \mathbf{A}^{-1} $

其中 $\otimes$ 是克罗内克积，$\mathbf{J}^*$ 是 $\mathbf{J}$ 的逐元素[复共轭](@entry_id:174690)，而 $\mathbf{A}$ 是一个固定的变换矩阵。这个关系建立了两种 formalism 之间的桥梁，使得我们能够从更基本的[琼斯矩阵](@entry_id:266533)推导出更通用的[穆勒矩阵](@entry_id:274422)。

总之，琼斯和[穆勒矩阵](@entry_id:274422)方法为我们提供了分析和设计[偏振光学](@entry_id:270461)系统的完整工具集。[琼斯矢量](@entry_id:176164)算法简洁、直观，是处理相干、完全偏振光的首选工具。而穆勒-斯托克斯体系则以其普适性见长，能够处理现实世界中更复杂的非偏振和[部分偏振光](@entry_id:267467)，并能描述去偏振等现象，使其在实验偏振测量学（polarimetry）和椭偏仪（ellipsometry）等领域不可或缺。