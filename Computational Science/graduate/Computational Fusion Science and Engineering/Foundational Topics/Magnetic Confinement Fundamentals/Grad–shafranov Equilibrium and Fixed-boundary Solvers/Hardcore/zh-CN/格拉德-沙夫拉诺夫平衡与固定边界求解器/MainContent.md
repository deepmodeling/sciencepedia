## 引言
在磁约束聚变研究中，实现并维持稳定的等离子体位形是达成[聚变反应](@entry_id:749665)的首要条件。描述这种宏观平衡状态的核心理论工具是 Grad-Shafranov (GS) 方程，它是[托卡马克](@entry_id:160432)等[轴对称](@entry_id:1130776)装置[物理设计](@entry_id:1129644)的基石。然而，从基础的[磁流体动力学](@entry_id:264274)原理到能够解决实际问题的数值求解器，再到其在复杂聚变现象分析中的广泛应用，这之间存在着理论与实践的鸿沟。本文旨在系统性地跨越这一鸿沟，为读者提供一个关于 GS 平衡及其[固定边界求解器](@entry_id:1125044)的全面视角。

接下来，我们将通过三个章节展开论述。第一章“原理与机制”将从理想 MHD 方程出发，严谨地推导出 [Grad-Shafranov 方程](@entry_id:190950)，阐明其数学结构和物理内涵。第二章“应用与跨学科联系”将展示[平衡解](@entry_id:174651)的巨大实用价值，探讨其如何作为输入，应用于等离子体稳定性分析、位形控制以及大规模[集成建模](@entry_id:1124521)等前沿领域。最后，在“动手实践”部分，读者将有机会通过具体的编程任务，亲手实现并验证本文讨论的核心算法。让我们首先深入“原理与机制”，探索构建[等离子体平衡](@entry_id:184963)世界的物理定律与数学框架。

## 原理与机制

本章旨在深入探讨描述[轴对称](@entry_id:1130776)磁约束[聚变[等离子体平](@entry_id:1125409)衡](@entry_id:184963)的物理原理与数学机制。我们将从[理想磁流体动力学](@entry_id:198478)（MHD）的基本方程出发，系统地推导出 Grad-Shafranov 方程，阐明其结构，并讨论求解该方程的固定边界问题的核心概念。内容将涵盖从物理基础到数值实现的关键环节，为理解和应用固定边界平衡求解器奠定坚实的理论基础。

### [理想磁流体动力学](@entry_id:198478)平衡的基础

在磁约束[聚变等离子体](@entry_id:1125407)的宏观描述中，单流体[磁流体动力学](@entry_id:264274)（MHD）模型提供了最基本的理论框架。一个处于[平衡态](@entry_id:270364)的等离子体，其宏观参数（如压强、密度、磁场）不随时间演化。在许多聚变装置（如[托卡马克](@entry_id:160432)）的核心区域，等离子体可以被近似地视为处于静态平衡。描述这种平衡的核心方程是力平衡方程。

完整的单流体[动量方程](@entry_id:197225)为：
$$
\rho \left( \frac{\partial \mathbf{v}}{\partial t} + (\mathbf{v} \cdot \nabla) \mathbf{v} \right) = \mathbf{J} \times \mathbf{B} - \nabla \cdot \mathbf{P} + \rho_e \mathbf{E} + \mathbf{F}_{\text{ext}}
$$
其中 $\rho$ 是质量密度，$\mathbf{v}$ 是流体速度，$\mathbf{J}$ 是电流密度，$\mathbf{B}$ 是磁场，$\mathbf{P}$ 是压强张量，$\rho_e$ 是[电荷密度](@entry_id:144672)，$\mathbf{E}$ 是电场，$\mathbf{F}_{\text{ext}}$ 是外部[体力](@entry_id:174230)（如[引力](@entry_id:189550)）。

为了得到 Grad-Shafranov 方程所描述的理想静态平衡，我们需要引入一系列简化假设 。这些假设构成了我们分析的基石：
1.  **静态假设 (Static Assumption)**：我们考虑的是一个不随时间变化的[稳态](@entry_id:139253) ($\partial / \partial t = 0$)，并且等离子体没有宏观流动 ($\mathbf{v} = \mathbf{0}$)。这使得[动量方程](@entry_id:197225)左侧的惯性项 $\rho (\partial \mathbf{v} / \partial t + (\mathbf{v} \cdot \nabla) \mathbf{v})$ 为零。
2.  **[理想磁流体动力学](@entry_id:198478) (Ideal MHD)**：我们假设等离子体是理想导体，其电阻为零。根据[理想欧姆定律](@entry_id:185600) $\mathbf{E} + \mathbf{v} \times \mathbf{B} = \mathbf{0}$，在静态条件下 ($\mathbf{v} = \mathbf{0}$)，这意味着电场 $\mathbf{E}$ 也为零。同时，我们忽略黏性效应。
3.  **各向同性标量压强 (Isotropic Scalar Pressure)**：假设压强张量是各向同性的，$\mathbf{P} = p\mathbf{I}$，其中 $p$ 是标量压强，$\mathbf{I}$ 是单位张量。因此，压强[梯度力](@entry_id:166847)简化为 $-\nabla \cdot (p\mathbf{I}) = -\nabla p$。
4.  **[准中性](@entry_id:197419) (Quasineutrality)**：在宏观尺度上，等离子体被认为是[电中性](@entry_id:138647)的，即净电荷密度 $\rho_e \approx 0$。这使得[静电力](@entry_id:203379)项 $\rho_e \mathbf{E}$ 可以忽略。
5.  **忽略外力 (Negligible External Forces)**：与巨大的[电磁力](@entry_id:196024)和压强[梯度力](@entry_id:166847)相比，[引力](@entry_id:189550)等外力 $\mathbf{F}_{\text{ext}}$ 在[聚变等离子体](@entry_id:1125407)中是微不足道的，可以安全地忽略。

在这些假设下，复杂的动量方程急剧简化，成为一个优雅的平衡关系式，即**静态理想MHD力[平衡方程](@entry_id:172166)**：
$$
\nabla p = \mathbf{J} \times \mathbf{B}
$$
这个方程表明，在理想静态平衡中，驱动等离子体膨胀的压强[梯度力](@entry_id:166847) ($\nabla p$) 恰好被磁场与电流相互作用产生的洛伦兹力 ($\mathbf{J} \times \mathbf{B}$) 所约束，从而形成稳定的位形。这是所有[托卡马克平衡](@entry_id:204576)理论的出发点。

### [轴对称](@entry_id:1130776)与磁通函数 $\psi$

[托卡马克](@entry_id:160432)等环形装置具有天然的[几何对称性](@entry_id:189059)——[轴对称](@entry_id:1130776)。这意味着在[柱坐标系](@entry_id:266798) $(R, \phi, Z)$ 中，所有物理量都与环向角 $\phi$ 无关，即 $\partial / \partial \phi = 0$。这一对称性极大地简化了问题的维度，使我们能够从三维矢量问题转化为二维标量问题。

这一转化的关键在于引入一个标量函数，即**极向磁通函数 (poloidal magnetic flux function)** $\psi(R,Z)$。根据[麦克斯韦方程组](@entry_id:150940)中的磁场无散定律 $\nabla \cdot \mathbf{B} = 0$，在[轴对称](@entry_id:1130776)条件下，我们可以证明存在一个函数 $\psi(R,Z)$，其[等值面](@entry_id:196027)恰好构成了磁[场线](@entry_id:172226)所在的曲面，即**磁面 (magnetic surfaces)**。

为了更精确地理解 $\psi$ 的定义及其与磁面的关系 ，我们从磁矢量势 $\mathbf{A}$ ($\mathbf{B} = \nabla \times \mathbf{A}$) 出发。$\psi(R,Z)$ 被定义为：
$$
\psi(R,Z) \equiv \frac{1}{2\pi} \oint_{\text{torus at }(R,Z)} \mathbf{A} \cdot d\mathbf{\ell}
$$
其中积分路径是一个位于特定 $(R,Z)$ 位置、沿环向的闭合回路，$d\mathbf{\ell} = R d\phi \mathbf{e}_{\phi}$。在[轴对称](@entry_id:1130776)规范下，$\mathbf{A}$ 的各分量也与 $\phi$ 无关，因此该定义可以简化为 $\psi(R,Z) = R A_{\phi}(R,Z)$，其中 $A_{\phi}$ 是[磁矢量势](@entry_id:141246)的环向分量。

$\psi$ 的[等值面](@entry_id:196027)是磁面，意味着磁场矢量 $\mathbf{B}$ 处处与 $\psi$ 的[等值面](@entry_id:196027)相切。在数学上，这等价于 $\mathbf{B}$ 与 $\psi$ 的梯度 $\nabla \psi$ 处处正交。我们可以证明这一点：
首先，利用 $\mathbf{B} = \nabla \times \mathbf{A}$ 和[轴对称](@entry_id:1130776)条件，磁场的极向分量（即在 $R-Z$ 平面内的分量）可以表示为：
$$
B_R = -\frac{\partial A_{\phi}}{\partial Z} = -\frac{1}{R} \frac{\partial \psi}{\partial Z}
$$
$$
B_Z = \frac{1}{R} \frac{\partial (R A_{\phi})}{\partial R} = \frac{1}{R} \frac{\partial \psi}{\partial R}
$$
标量函数 $\psi(R,Z)$ 的梯度为 $\nabla \psi = \frac{\partial \psi}{\partial R} \mathbf{e}_R + \frac{\partial \psi}{\partial Z} \mathbf{e}_Z$。现在计算 $\mathbf{B}$ 和 $\nabla \psi$ 的点积：
$$
\mathbf{B} \cdot \nabla \psi = B_R \frac{\partial \psi}{\partial R} + B_Z \frac{\partial \psi}{\partial Z} = \left(-\frac{1}{R} \frac{\partial \psi}{\partial Z}\right) \frac{\partial \psi}{\partial R} + \left(\frac{1}{R} \frac{\partial \psi}{\partial R}\right) \frac{\partial \psi}{\partial Z} = 0
$$
这个结果 $\mathbf{B} \cdot \nabla \psi = 0$ 明确地证明了磁场线位于 $\psi$ 的[等值面](@entry_id:196027)上。因此，$\psi$ 的[等值面](@entry_id:196027)就是嵌套的环形磁面，它们构成了[等离子体约束](@entry_id:203546)的基本拓扑结构。值得注意的是，$\psi$ 的定义在[规范变换](@entry_id:176521) $\mathbf{A} \to \mathbf{A} + \nabla \chi$（对于单值标量函数 $\chi$）下是不变的，保证了其物理意义的确定性。

### 用 $\psi$ 表示磁场

通过引入 $\psi$，我们不仅得到了磁面的几何描述，还能用它来定量表示磁场分量。如前所述，极向磁场 $\mathbf{B}_p = B_R \mathbf{e}_R + B_Z \mathbf{e}_Z$ 的两个分量完全由 $\psi$ 的一阶[偏导数](@entry_id:146280)决定 ：
$$
B_R = -\frac{1}{R} \frac{\partial \psi}{\partial Z} \quad \text{和} \quad B_Z = \frac{1}{R} \frac{\partial \psi}{\partial R}
$$
这组关系可以用一个更紧凑的矢量形式表示：
$$
\mathbf{B}_p = \frac{1}{R} \nabla \psi \times \mathbf{e}_{\phi}
$$
这个表达式清晰地显示了 $\mathbf{B}_p$ 位于 $R-Z$ 平面内，并且处处垂直于 $\nabla \psi$，再次印证了磁[场线](@entry_id:172226)与 $\psi$ 等值面相切。

极向磁场的模长 $|\mathbf{B}_p|$ 同样可以由 $\psi$ 导出：
$$
|\mathbf{B}_p| = \sqrt{B_R^2 + B_Z^2} = \sqrt{\left(-\frac{1}{R} \frac{\partial \psi}{\partial Z}\right)^2 + \left(\frac{1}{R} \frac{\partial \psi}{\partial R}\right)^2} = \frac{1}{R} \sqrt{\left(\frac{\partial \psi}{\partial R}\right)^2 + \left(\frac{\partial \psi}{\partial Z}\right)^2}
$$
注意到 $\nabla \psi$ 的模长为 $|\nabla \psi| = \sqrt{(\partial \psi / \partial R)^2 + (\partial \psi / \partial Z)^2}$，我们可以得到一个非常重要的关系：
$$
|\mathbf{B}_p| = \frac{|\nabla \psi|}{R}
$$
这个关系揭示了[托卡马克](@entry_id:160432)位形的一个基本几何特征：对于给定的磁面间距（即 $|\nabla \psi|$），极向磁场在环内侧（小 $R$）比在外侧（大 $R$）更强。这是因为在环内侧，相同的磁通量必须穿过更小的面积。

### 平衡的任意函数：$p(\psi)$ 与 $F(\psi)$

现在我们回到力[平衡方程](@entry_id:172166) $\nabla p = \mathbf{J} \times \mathbf{B}$。这个方程不仅约束了磁场位形，还对压强 $p$ 和[环向磁场](@entry_id:756057) $B_{\phi}$ 的[空间分布](@entry_id:188271)施加了严格的限制。

首先，考察压强 $p$。将力平衡方程与磁场 $\mathbf{B}$ 做点积，我们得到：
$$
\mathbf{B} \cdot \nabla p = \mathbf{B} \cdot (\mathbf{J} \times \mathbf{B}) = 0
$$
$\mathbf{B} \cdot \nabla p = 0$ 意味着压强 $p$ 沿着磁[场线](@entry_id:172226)的[方向导数](@entry_id:189133)为零，即压强在每根磁[场线](@entry_id:172226)上都是常数。由于磁场线密集地分布在磁面上，这要求压强在整个磁面上都必须是常数。换言之，压强 $p$ 仅仅是磁通函数 $\psi$ 的函数，而不能独立地依赖于 $(R,Z)$。我们将其记为 **$p(\psi)$** 。这个结论是理想 MHD 平衡理论的基石之一。指定函数 $p(\psi)$ 就相当于定义了等离子体在不同磁面上的压强分布。

其次，考察[环向磁场](@entry_id:756057) $B_{\phi}$。在[轴对称](@entry_id:1130776)条件下，力[平衡方程](@entry_id:172166)的环向分量为 $(\mathbf{J} \times \mathbf{B})_{\phi} = J_R B_Z - J_Z B_R = 0$。这表明极向电流密度 $\mathbf{J}_p$ 必须与极向磁场 $\mathbf{B}_p$ 平行。通过[安培定律](@entry_id:140092) $\mu_0 \mathbf{J} = \nabla \times \mathbf{B}$，可以进一步证明，为了维持这种平衡，乘积 $R B_{\phi}$ 也必须是一个磁通函数。我们定义**环向场函数 $F$**：
$$
F(\psi) \equiv R B_{\phi}
$$
这个函数 $F(\psi)$ 同样是平衡位形的一个自由度。它决定了[环向磁场](@entry_id:756057)的大小，即 $B_{\phi} = F(\psi) / R$。$F(\psi)$ 的导数 $dF/d\psi$ 与极向电流密度直接相关，是驱动极向电流的源。

综上所述，一个[轴对称](@entry_id:1130776)的理想 MHD 平衡位形完全由三个要素确定：
1.  一个二维[标量场](@entry_id:151443)——极向磁通函数 $\psi(R,Z)$。
2.  两个一维标量函数——压强剖面 $p(\psi)$ 和[环向场](@entry_id:194478)函数 $F(\psi)$。

这两个函数 $p(\psi)$ 和 $F(\psi)$ 被称为**平衡的任意函数**，因为在理想 MHD 理论框架内，它们的形式不受基本方程的唯一限制，可以自由指定。

### Grad-Shafranov 方程的推导与结构

有了 $\psi$、$p(\psi)$ 和 $F(\psi)$ 这三个构建模块，我们现在可以将它们整合到一个统一的方程中。这个方程就是著名的 **Grad-Shafranov (GS) 方程**。

GS 方程的推导始于安培定律 $\mu_0 \mathbf{J} = \nabla \times \mathbf{B}$。将其代入力平衡方程 $\nabla p = \mathbf{J} \times \mathbf{B}$，得到：
$$
\nabla p = \frac{1}{\mu_0} (\nabla \times \mathbf{B}) \times \mathbf{B}
$$
将磁场分解为极向和环向部分 $\mathbf{B} = \mathbf{B}_p + B_{\phi}\mathbf{e}_{\phi}$，并利用 $\mathbf{B}_p = ( \nabla \psi \times \mathbf{e}_{\phi}) / R$ 和 $B_{\phi} = F(\psi)/R$ 进行代数运算和展开，最终可以得到一个关于 $\psi$ 的二维[偏微分](@entry_id:194612)方程。

这个过程的一个关键环节是认识到平衡的存在性要求力密度场 $\mathbf{J} \times \mathbf{B}$ 必须是一个[保守场](@entry_id:137555)，即其旋度为零。由于 $\mathbf{J} \times \mathbf{B} = \nabla p$，而任何[梯度的旋度](@entry_id:274168)恒为零（$\nabla \times (\nabla p) = \mathbf{0}$），这个条件是自动满足的。这从根本上保证了力平衡方程与磁场拓扑的相容性 。

最终得到的 Grad-Shafranov 方程的[标准形式](@entry_id:153058)为：
$$
\Delta^* \psi = - \mu_0 R^2 \frac{dp}{d\psi} - F(\psi) \frac{dF}{d\psi}
$$
这里的 $\Delta^*$ 是 Grad-Shafranov 算子，定义为：
$$
\Delta^* \psi \equiv R^2 \nabla \cdot \left( \frac{1}{R^2} \nabla \psi \right) = \frac{\partial^2 \psi}{\partial R^2} - \frac{1}{R} \frac{\partial \psi}{\partial R} + \frac{\partial^2 \psi}{\partial Z^2}
$$
GS 方程是一个二阶、半线性（或称[拟线性](@entry_id:637689)）的椭圆型[偏微分](@entry_id:194612)方程。
-   **椭圆型**：意味着它的解是“平滑”的，并且在区域内任何一点的值都受到整个边界值的影响，这与描述扩散或平衡的物理过程相符。
-   **半线性**：因为最高阶（二阶）导数项是线性的，而[非线性](@entry_id:637147)体现在右侧的源项中，源项通过 $p(\psi)$ 和 $F(\psi)$ 依赖于解 $\psi$ 本身。

方程的右侧是源项，由两部分组成：
-   第一项 $-\mu_0 R^2 \frac{dp}{d\psi}$ 与等离子体压强梯度有关，主要贡献于环向电流。
-   第二项 $-F(\psi) \frac{dF}{d\psi}$ 与[环向磁场](@entry_id:756057)的梯度有关，主要贡献于极向电流。

GS 方程的本质是[轴对称](@entry_id:1130776)下的安培定律的环向分量，它将磁场位形 ($\psi$) 与驱动该位形的电流源 ($p', F F'$) 联系在了一起。

### 固定边界问题

要从 GS 方程解出唯一的 $\psi(R,Z)$，我们必须提供边界条件。在[计算聚变科学](@entry_id:1122784)中，一类重要且常见的问题是**固定边界问题 (fixed-boundary problem)** 。

在数学上，一个固定边界问题是在一个预先指定的二维区域 $\Omega$（代表等离子体的极向[截面](@entry_id:154995)）内求解 GS 方程，并在这个区域的边界 $\partial \Omega$ 上施加狄利克雷边界条件 (Dirichlet boundary condition)，即直接规定 $\psi$ 在边界上的值：
$$
\psi|_{\partial \Omega} = \psi_b
$$
通常，边界值 $\psi_b$ 是一个常数，这表明我们预设的边界 $\partial \Omega$ 本身就是一个磁面。

在物理上，“固定边界”意味着我们人为地规定了等离子体的形状和位置。这个边界通常被设定为**最外闭合磁面 (Last Closed Flux Surface, LCFS)**，它定义了高温等离子体区域的边缘。求解固定边界问题，就是要在给定等离子体形状（由 $\partial \Omega$ 描述）和内部剖面（由 $p(\psi)$ 和 $F(\psi)$ 描述）的前提下，计算出内部磁场的详细结构。

这种方法与“[自由边界问题](@entry_id:636836)”形成对比。在[自由边界问题](@entry_id:636836)中，人们指定的是外部线圈中的电流，而等离子体的边界形状和位置是作为解的一部分自洽地计算出来的。固定边界问题在理论分析和许多数值研究中非常有用，因为它将复杂的几何问题与内部物理问题[解耦](@entry_id:160890)。

### 数值求解机制：[有限差分法](@entry_id:1124968)

GS 方程通常是[非线性](@entry_id:637147)的，并且很少有解析解，因此必须依赖数值方法求解。有限差分法 (Finite Difference Method, FDM) 是最直观和基础的数值方法之一。其核心思想是将求解域离散化为网格，并用[差商](@entry_id:136462)近似代替[偏导数](@entry_id:146280)，从而将[偏微分](@entry_id:194612)方程转化为一个大型[代数方程](@entry_id:272665)组。

我们以在均匀的 $(R,Z)$ 网格上离散化 Grad-Shafranov 算子 $\Delta^*$ 为例 。网格点为 $(R_i, Z_j)$，格点间距为 $\Delta R$ 和 $\Delta Z$。为了保证数值的稳定性和守恒性，最好从算子的自[伴随形式](@entry_id:747524)出发：
$$
\Delta^*\psi = R\frac{\partial}{\partial R}\left(\frac{1}{R}\frac{\partial\psi}{\partial R}\right) + \frac{\partial^2\psi}{\partial Z^2}
$$
在网格点 $(i,j)$ 处，我们可以使用中心差分来近似各个导数。
-   对于 $Z$ 方向的二阶导数，标准的二阶精度近似为：
    $$ \left. \frac{\partial^2\psi}{\partial Z^2} \right|_{i,j} \approx \frac{\psi_{i,j+1} - 2\psi_{i,j} + \psi_{i,j-1}}{(\Delta Z)^2} $$
-   对于 $R$ 方向的复杂项，我们采用一种称为“面心加权”的技巧来保持二阶精度和守恒性。我们将 $R\frac{\partial}{\partial R}(\dots)$ 近似为 $R_i \frac{F_{i+1/2} - F_{i-1/2}}{\Delta R}$，其中 $F = \frac{1}{R}\frac{\partial\psi}{\partial R}$ 是“径向通量”，在格点之间的“面心” $R_{i\pm 1/2}$ 处计算。最终得到的离散形式为：
    $$ \left. R\frac{\partial}{\partial R}\left(\frac{1}{R}\frac{\partial\psi}{\partial R}\right) \right|_{i,j} \approx \frac{R_i}{(\Delta R)^2} \left[ \frac{\psi_{i-1,j}}{R_{i-1/2}} - \left(\frac{1}{R_{i+1/2}} + \frac{1}{R_{i-1/2}}\right)\psi_{i,j} + \frac{\psi_{i+1,j}}{R_{i+1/2}} \right] $$
    其中 $R_{i\pm 1/2} = R_i \pm \Delta R/2$。

将这两个部分组合起来，就得到了在网格点 $(i,j)$ 处关于 $\psi$ 值的五点差分格式。将这个格式应用于所有内部网格点，再结合边界条件，就形成了一个大型的[非线性](@entry_id:637147)代数方程组。这个方程组可以通过迭代方法求解，例如 Picard 迭代或[牛顿法](@entry_id:140116)，最终得到在整个网格上 $\psi$ 的数值解。

### 确定平衡：约束与反演

求解 GS 方程的一个核心挑战是，我们必须预先指定两个任意函数 $p(\psi)$ 和 $F(\psi)$。在实际应用中，我们通常无法直接测量这两个函数，而是拥有一系列[等离子体诊断](@entry_id:189276)信号，例如总等离子体电流 $I_p$、[极向比压](@entry_id:1129912) $\beta_p$、外部磁探针信号等。这就引出了一个[逆问题](@entry_id:143129)：如何从这些实验测量值来重构最符合实际的 $p(\psi)$ 和 $F(\psi)$ 剖面？

首先，一些宏观物理量，如总电流 $I_p$ 和[极向比压](@entry_id:1129912) $\beta_p$，为 $p(\psi)$ 和 $F(\psi)$ 提供了积分约束 。
-   **总等离子体电流 $I_p$**：环向电流密度 $J_{\phi}$ 是由 $p'(\psi)$ 和 $FF'(\psi)$ 决定的。总电流是 $J_{\phi}$ 在整个等离子体[截面](@entry_id:154995)上的积分：
    $$ I_p = \iint_D J_{\phi}(\psi,R) \,dA = \iint_D \left( R\frac{dp}{d\psi} + \frac{1}{\mu_0 R}F(\psi)\frac{dF}{d\psi} \right) dA $$
-   **[极向比压](@entry_id:1129912) $\beta_p$**：它被定义为等离子体平均压强与极向磁场平均[磁压](@entry_id:272413)强的比值：
    $$ \beta_p = \frac{2\mu_0 \langle p \rangle}{\langle B_p^2 \rangle} = \frac{2\mu_0 \iint_D p(\psi) \, dA}{\iint_D |\mathbf{B}_p|^2 \, dA} $$

这两个方程是关于 $p(\psi)$ 和 $F(\psi)$ 的全局积分约束。在实际操作中，研究者通常会假设 $p(\psi)$ 和 $F(\psi)$ 具有某种[参数化](@entry_id:265163)的函数形式，例如多项式或[样条](@entry_id:143749)函数。这两个积分约束可以用来确定[参数化](@entry_id:265163)形式中的两个自由参数（通常是幅值或归一化系数），但它们无法唯一地确定函数的完整“形状”。

为了更精确地重构剖面，需要进行**平衡反演 (equilibrium reconstruction)**。这是一个典型的反问题，通常通过最小化模型预测的诊断信号与实际测量值之间的差异（[残差平方和](@entry_id:174395)）来求解。然而，无约束的反演可能导致非物理的解，例如压强剖面不单调（这通常意味着不稳），或者电流密度出现不合理的空心或反向。

因此，必须在反演过程中施加物理约束 。一个稳健且高效的方法是将此问题构建为一个**二次规划 (Quadratic Program, QP)** 问题。具体做法是：
1.  **保证压强单调性**：假设压强从磁轴向外单调递减，即 $dp/d\psi \le 0$（假设 $\psi$ 由轴心向外增大）。我们可以选择一组非负的基函数 $\phi_i(\psi) \ge 0$，并将 $dp/d\psi$ [参数化](@entry_id:265163)为 $dp/d\psi = -\sum_i u_i \phi_i(\psi)$，同时要求系数 $u_i \ge 0$。这样，压强的[单调性](@entry_id:143760)就通过线性不等式约束得到了严格保证。
2.  **保证物理边界**：对于 $F(\psi)$，其值通常受到工程或物理限制，例如 $F_{\min} \le F(\psi) \le F_{\max}$。通过对 $d(F^2)/d\psi$ 进行积分，可以得到 $F^2(\psi)$ 与其基函数系数的线性关系。因此，对 $F^2(\psi)$ 在一系列离散点上施加边界约束，同样可以转化为关于系数的[线性不等式](@entry_id:174297)约束。

通过这种方式，反演问题变成了一个在满足一系列线性不等式约束的条件下，最小化一个二次目标函数（[残差平方和](@entry_id:174395)）的问题。这是一个[凸优化](@entry_id:137441)问题，存在高效且可靠的算法，能够确保找到唯一的[全局最优解](@entry_id:175747)，从而得到物理上合理的 $p(\psi)$ 和 $F(\psi)$ 剖面。

### 高级主题：[奇点](@entry_id:266699)与正则性

在处理更真实的等离子体位形时，我们会遇到一些导致解的正则性（[光滑性](@entry_id:634843)）降低的[奇点](@entry_id:266699)，这给数值求解带来了挑战。

一个典型的例子是带有**X点 (X-point)** 的**分界面 (separatrix)** 位形 。分界面是分隔开闭合磁面区域（等离子体核心）和开放磁面区域（刮削层）的特殊磁面。在分界面上，通常会存在一个或多个X点，在这些点上极向磁场为零，即 $|\mathbf{B}_p|=0$，等价于 $|\nabla \psi|=0$。

这种位形带来了两类主要的数值困难：
1.  **源项的[不连续性](@entry_id:144108)**：在理想模型中，等离子体压强和电流在分界面处突降为零。这意味着 $p'(\psi)$ 和 $F'(\psi)$ 在分界面上存在跳变。根据椭圆型[偏微分](@entry_id:194612)方程的[正则性理论](@entry_id:194071)，如果源项存在跳变，那么解 $\psi$ 的二阶导数在跨越该界面时也将是不连续的。此时，解 $\psi$ 通常只有 $C^1$ 正则性（即函数本身和[一阶导数](@entry_id:749425)连续，但二阶导数不连续）。对于依赖于解的高[光滑性](@entry_id:634843)的[高阶数值方法](@entry_id:142601)（如[谱方法](@entry_id:141737)或高阶有限元），这种低正则性会严重破坏其收敛速度。
2.  **[几何奇点](@entry_id:186127)**：X点本身是一个[几何奇点](@entry_id:186127)。在X点处，分界面不再是光滑的曲线，而是形成一个“角”。即使源项是光滑的，椭圆方程在带角的区域求解时，其解在角点附近的正则性也会降低。此外，以磁面为基础的坐标系（如 $(\psi, \theta)$ 坐标）在[X点](@entry_id:1134148)处是奇异的，因为坐标变换的[雅可比行列式](@entry_id:137120)与 $1/|\nabla \psi|$ 成正比，会在X点发散。

处理这些[奇点](@entry_id:266699)的常用策略包括：
-   **剖面光滑化**：在数值计算中，人为地将 $p(\psi)$ 和 $F(\psi)$ 在分界面附近进行光滑处理，用一个薄的过渡层来代替理想的突变。这会提高解的全局正则性，从而显著改善高阶[数值方法的收敛性](@entry_id:635470)，但代价是牺牲了部分物理模型的精确性。
-   **[网格加密](@entry_id:168565)**：在[奇点](@entry_id:266699)（如[X点](@entry_id:1134148)）和低正则性区域（如分界面）附近进行自适应的网格加密。特别是对于界面问题，沿法向的各向异性加密可以有效地捕捉解的剧烈变化，恢复数值方法的[收敛阶](@entry_id:146394)。

理解并妥善处理这些[奇点](@entry_id:266699)是开发高精度、高保真度平衡求解器的关键，也是[计算聚变科学](@entry_id:1122784)研究的前沿领域之一。