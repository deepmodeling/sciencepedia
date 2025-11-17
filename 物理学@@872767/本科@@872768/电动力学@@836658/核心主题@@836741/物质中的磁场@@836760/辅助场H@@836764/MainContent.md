## 引言
在研究[电磁场](@entry_id:265881)与物质相互作用时，我们面临着一个核心挑战：物质本身会对电场和磁场做出响应，产生束缚[电荷](@entry_id:275494)和束缚电流，而这些束缚源反过来又会改变总的[电磁场](@entry_id:265881)。直接求解这个高度耦合的系统十分复杂。为了解决这一难题，物理学家引入了两个强大的概念工具——辅助场，即[电位移矢量](@entry_id:197092) $\mathbf{D}$ 和[辅助磁场](@entry_id:261447) $\mathbf{H}$。它们是理解和应用宏观电磁学的基石。

本文旨在系统地阐明辅助场的理论与实践。通过学习本文，您将掌握如何运用这些场来简化复杂的电磁问题，并深刻理解它们在现代科技中的核心作用。

文章将分为三个核心部分展开：
*   在**原理与机制**一章中，我们将详细推导 $\mathbf{D}$ 场和 $\mathbf{H}$ 场的定义，阐明它们如何将自由源从总源中分离出来，并探讨它们在介质边界和[时变场](@entry_id:180620)中的行为。
*   接着，在**应用和跨学科联系**一章中，我们将展示辅助场在工程设计（如[磁路](@entry_id:268480)、变压器）、[机电耦合](@entry_id:142536)（如[磁致伸缩](@entry_id:143327)）以及凝聚态物理（如永磁体和[超导体](@entry_id:191025)）等领域的广泛应用。
*   最后，在**动手实践**部分，您将有机会通过解决具体问题来巩固所学知识。

让我们首先深入**原理与机制**，揭示[辅助场](@entry_id:155519)如何为我们提供[分析物](@entry_id:199209)质中电磁现象的优雅框架。

## 原理与机制

在研究[电磁场](@entry_id:265881)与物质相互作用时，我们从微观层面过渡到宏观层面。在宏观尺度下，我们不再关心单个原子或分子的响应，而是将它们的集[体效应](@entry_id:261475)通过**[极化强度](@entry_id:188176)** $\mathbf{P}$（电偶极矩的体密度）和**磁化强度** $\mathbf{M}$（磁偶极矩的体密度）进行平均化描述。这种处理方式引入了由介质束缚的[电荷](@entry_id:275494)和电流，它们与我们能直接控制的**[自由电荷](@entry_id:264392)**和**[自由电流](@entry_id:191634)**共同构成了总的源。为了简化在介质中求解[电磁场](@entry_id:265881)的问题，物理学家引入了两个[辅助场](@entry_id:155519)——**[电位移矢量](@entry_id:197092)** $\mathbf{D}$ 和**[辅助磁场](@entry_id:261447)** $\mathbf{H}$。本章将深入探讨这两个[辅助场](@entry_id:155519)的定义、物理原理及其在求解电磁学问题中的关键作用。

### 辅助场的引入：分离自由源与束缚源

引入辅助场的根本动机在于，将麦克斯韦方程组中的[源项](@entry_id:269111)与场的响应分离开来。在介质中，总[电荷密度](@entry_id:144672) $\rho_{\text{total}}$ 是[自由电荷](@entry_id:264392)密度 $\rho_f$ 与束缚电荷密度 $\rho_b$ 之和；总[电流密度](@entry_id:190690) $\mathbf{J}_{\text{total}}$ 则是[自由电流](@entry_id:191634)密度 $\mathbf{J}_f$ 与束缚[电流密度](@entry_id:190690) $\mathbf{J}_b$ 之和。束缚源 $\rho_b$ 和 $\mathbf{J}_b$ 本身是介质对[电磁场](@entry_id:265881)响应的结果，这使得直接求解[电场](@entry_id:194326) $\mathbf{E}$ 和[磁场](@entry_id:153296) $\mathbf{B}$ 变得复杂。[辅助场](@entry_id:155519) $\mathbf{D}$ 和 $\mathbf{H}$ 的巧妙之处在于，它们重新定义的[麦克斯韦方程组](@entry_id:150940)的源项将只包含我们能够直接设定和测量的[自由电荷](@entry_id:264392)和[自由电流](@entry_id:191634)。

#### [电位移矢量](@entry_id:197092) D

我们从[高斯定律的微分形式](@entry_id:191832)出发，它将[电场](@entry_id:194326) $\mathbf{E}$ 与空间中的总[电荷密度](@entry_id:144672)联系起来：
$$ \nabla \cdot \mathbf{E} = \frac{\rho_{\text{total}}}{\epsilon_0} = \frac{\rho_f + \rho_b}{\epsilon_0} $$
其中 $\epsilon_0$ 是[真空介电常数](@entry_id:204253)。介质的极化效应产生的束缚[体电荷密度](@entry_id:264747) $\rho_b$ 与极化强度 $\mathbf{P}$ 之间存在一个基本关系：$\rho_b = -\nabla \cdot \mathbf{P}$。这个关系可以通过分析非均匀极化介质内部净[电荷](@entry_id:275494)的积累来导出。例如，在一个球对称的[极化场](@entry_id:197617) $\mathbf{P}(\mathbf{r}) = \alpha r^{3} \hat{\mathbf{r}}$ 中，我们可以通过计算其散度来直接求得束缚[体电荷密度](@entry_id:264747)为 $\rho_b(r) = -5 \alpha r^2$ [@problem_id:1609055]。

将 $\rho_b = -\nabla \cdot \mathbf{P}$ 代入高斯定律，我们得到：
$$ \nabla \cdot \mathbf{E} = \frac{\rho_f - \nabla \cdot \mathbf{P}}{\epsilon_0} $$
移项整理后，可得：
$$ \nabla \cdot (\epsilon_0 \mathbf{E} + \mathbf{P}) = \rho_f $$
这个方程的左边括号内的组合被定义为一个新的矢量场，即**[电位移矢量](@entry_id:197092)** $\mathbf{D}$：
$$ \mathbf{D} \equiv \epsilon_0 \mathbf{E} + \mathbf{P} $$
这样，高斯定律在介质中的形式就被极大地简化了：
$$ \nabla \cdot \mathbf{D} = \rho_f $$
这个方程是[宏观麦克斯韦方程组](@entry_id:201246)的第一个方程。它揭示了 $\mathbf{D}$ 场的深刻物理意义：**$\mathbf{D}$ 场的散度源是自由电荷密度 $\rho_f$**。无论介质内部的极化效应多么复杂，包括由外[电场](@entry_id:194326)引起的感应极化和材料自身固有的“冻结”极化，这些效应都被内含在了 $\mathbf{D}$ 的定义之中。

我们可以通过一个思想实验来加深理解。考虑一个[平行板电容器](@entry_id:266922)，其内部填充了一种特殊介质（[驻极体](@entry_id:199456)），它既有永久性的“冻结”[极化场](@entry_id:197617) $\mathbf{P}_0$，又会在外加[电场](@entry_id:194326)作用下产生感应极化 $\mathbf{P}_{\text{ind}}$。此时总[极化强度](@entry_id:188176)为 $\mathbf{P}_{\text{total}} = \mathbf{P}_0 + \mathbf{P}_{\text{ind}}$。当我们给[电容器](@entry_id:267364)极板上放置自由电荷 $\sigma_f$ 时，根据高斯定律的积分形式 $\oint_S \mathbf{D} \cdot d\mathbf{a} = Q_{f, \text{enclosed}}$，[高斯面](@entry_id:272964)所包围的作为 $\mathbf{D}$ 场源的[电荷](@entry_id:275494)，仅仅是极板上的[自由电荷](@entry_id:264392)，而与介质内部由 $\mathbf{P}_0$ 或 $\mathbf{P}_{\text{ind}}$ 产生的束缚[电荷](@entry_id:275494)无关 [@problem_id:1609057]。这正是引入 $\mathbf{D}$ 场的巨大便利之处。

#### [辅助磁场](@entry_id:261447) H

与[电场](@entry_id:194326)类似，我们对[静磁学](@entry_id:140120)中的安培定律进行推广。在真空中，安培定律为 $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}_{\text{total}}$，其中 $\mathbf{J}_{\text{total}}$ 是总[电流密度](@entry_id:190690)。在磁介质中，总电流由[自由电流](@entry_id:191634) $\mathbf{J}_f$ 和束缚电流 $\mathbf{J}_b$ 构成。束缚电流源于介质的磁化，其体密度与磁化强度 $\mathbf{M}$ 的关系为 $\mathbf{J}_b = \nabla \times \mathbf{M}$。这个关系可以通过分析非均匀磁化介质中微观磁偶极矩环流的宏观效应来理解。例如，对于一个磁化强度为 $\mathbf{M} = k(y^2 \hat{x} - x^2 \hat{y})$ 的材料，我们可以通过计算其旋度得到其内部的[束缚体电流](@entry_id:266207)密度为 $\mathbf{J}_b = -2k(x+y)\hat{z}$ [@problem_id:1822464]。

将 $\mathbf{J}_b = \nabla \times \mathbf{M}$ 代入[安培定律](@entry_id:140092)：
$$ \nabla \times \mathbf{B} = \mu_0 (\mathbf{J}_f + \mathbf{J}_b) = \mu_0 (\mathbf{J}_f + \nabla \times \mathbf{M}) $$
其中 $\mu_0$ 是[真空磁导率](@entry_id:186031)。移项整理后，我们得到：
$$ \nabla \times \left(\frac{\mathbf{B}}{\mu_0} - \mathbf{M}\right) = \mathbf{J}_f $$
我们将括号内的矢量定义为**[辅助磁场](@entry_id:261447)** $\mathbf{H}$：
$$ \mathbf{H} \equiv \frac{\mathbf{B}}{\mu_0} - \mathbf{M} $$
于是，[安培定律](@entry_id:140092)在介质中的形式（[静磁学](@entry_id:140120)情形）简化为：
$$ \nabla \times \mathbf{H} = \mathbf{J}_f $$
这是[宏观麦克斯韦方程组](@entry_id:201246)的第四个方程（在[静磁学](@entry_id:140120)条件下）。它表明，**$\mathbf{H}$ 场的旋度源是[自由电流](@entry_id:191634)密度 $\mathbf{J}_f$**。介质的磁化效应，无论其来源如何，都已被包含在 $\mathbf{H}$ 的定义之内，而不再作为方程的[源项](@entry_id:269111)出现。

考虑一个实际场景：一根长直圆柱导体承载着[均匀分布](@entry_id:194597)的总[自由电流](@entry_id:191634) $I_0$，其外部套有一个具有“冻结”磁化强度 $\mathbf{M} = \frac{k}{s} \hat{\boldsymbol{\phi}}$ 的磁性套筒。根据[安培定律的积分形式](@entry_id:270391) $\oint \mathbf{H} \cdot d\mathbf{l} = I_{f, \text{enc}}$，当我们计算环绕整个装置的一个[安培环路](@entry_id:275261)上的 $\mathbf{H}$ 场线积[分时](@entry_id:274419)，等号右边的“被环绕的电流”仅包括导体中的[自由电流](@entry_id:191634) $I_0$。磁性套筒中的磁化所产生的束缚电流并不会对 $\mathbf{H}$ 场的[环路积分](@entry_id:164828)做出贡献。因此，在装置外部距离轴线 $s_0$ 处，$\mathbf{H}$ 场的大小就是 $\frac{I_0}{2\pi s_0}$，完全不受磁性套筒存在的影响 [@problem_id:1609108]。这清晰地展示了 $\mathbf{H}$ 场与[自由电流](@entry_id:191634)源的直接联系。

### H 场的物理内涵：[退磁场](@entry_id:265717)与[磁标势](@entry_id:185708)

虽然 $\mathbf{D}$ 和 $\mathbf{H}$ 常被视为[辅助场](@entry_id:155519)，但它们具有深刻的物理意义，尤其是在处理[永磁体](@entry_id:189081)等没有自由源的特殊情况时。$\mathbf{B}$ 场是更基本的场，因为它直接决定了对运动[电荷](@entry_id:275494)的作用力（[洛伦兹力](@entry_id:145104)），而 $\mathbf{E}$ 场则决定了对静止[电荷](@entry_id:275494)的作用力。$\mathbf{D}$ 和 $\mathbf{H}$ 则是为了在数学上简化问题而引入的，它们将场的源与材料的响应分离开来。

这种区别在永磁体问题中表现得淋漓尽致。考虑一根均匀磁化的长圆柱形永磁棒，其磁化强度 $\mathbf{M}$ 沿轴线方向，且周围没有[自由电流](@entry_id:191634) [@problem_id:1580855]。
1.  由于没有[自由电流](@entry_id:191634)，安培定律给出 $\nabla \times \mathbf{H} = \mathbf{J}_f = 0$ 在任何地方都成立。
2.  [高斯磁定律](@entry_id:182942) $\nabla \cdot \mathbf{B} = 0$ 是一条普适定律，永远成立。
3.  在磁棒外部，$\mathbf{M} = 0$，因此 $\mathbf{B} = \mu_0 \mathbf{H}$。这意味着在磁棒外部，$\mathbf{B}$ 场和 $\mathbf{H}$ 场方向相同，形态类似于一个螺线管或电偶极子产生的场。
4.  在磁棒内部，情况则大为不同。磁化强度 $\mathbf{M}$ 在磁棒的端面处产生束缚面电流，这些电流产生的[磁感应强度](@entry_id:144179) $\mathbf{B}$ 在磁棒内部大致与 $\mathbf{M}$同向。然而，根据定义 $\mathbf{H} = \mathbf{B}/\mu_0 - \mathbf{M}$，由于有限长度磁棒存在退磁效应，使得内部的 $|\mathbf{B}|  \mu_0 |\mathbf{M}|$。因此，内部的 $\mathbf{H}$ 场方向与 $\mathbf{M}$ 相反。这个内部的 $\mathbf{H}$ 场通常被称为**[退磁场](@entry_id:265717)**，因为它倾向于减弱总的磁化效应。

这个例子突显了 $\mathbf{B}$ 和 $\mathbf{H}$ 的本质区别：$\mathbf{B}$ [场线](@entry_id:172226)是无头无尾的[闭合曲线](@entry_id:264519)（$\nabla \cdot \mathbf{B} = 0$），而 $\mathbf{H}$ [场线](@entry_id:172226)可以有起点和终点，这些起点和终点就表现为“磁荷”。

当一个区域内没有[自由电流](@entry_id:191634)时，即 $\mathbf{J}_f=0$，我们有 $\nabla \times \mathbf{H} = 0$。这个条件在数学上保证了 $\mathbf{H}$ 场可以表示为一个[标量场的梯度](@entry_id:270765)，这与[静电场](@entry_id:268546) $\mathbf{E}$ 的情况完全类似。我们定义**[磁标势](@entry_id:185708)** $\Phi_M$，使得：
$$ \mathbf{H} = -\nabla \Phi_M $$
为了找出[磁标势](@entry_id:185708)的源，我们计算 $\mathbf{H}$ 场的散度：
$$ \nabla \cdot \mathbf{H} = \nabla \cdot \left(\frac{\mathbf{B}}{\mu_0} - \mathbf{M}\right) = \frac{1}{\mu_0}(\nabla \cdot \mathbf{B}) - \nabla \cdot \mathbf{M} $$
由于 $\nabla \cdot \mathbf{B} = 0$，上式简化为 $\nabla \cdot \mathbf{H} = -\nabla \cdot \mathbf{M}$。将 $\mathbf{H} = -\nabla \Phi_M$ 代入，我们得到一个类似于[静电学](@entry_id:140489)[泊松方程](@entry_id:143763)的方程：
$$ \nabla^2 \Phi_M = -(-\nabla \cdot \mathbf{M}) \equiv \rho_M $$
这里，我们定义了等效的**磁[体电荷密度](@entry_id:264747)** $\rho_M = -\nabla \cdot \mathbf{M}$ 和**[磁面](@entry_id:204802)[电荷密度](@entry_id:144672)** $\sigma_M = \mathbf{M} \cdot \hat{\mathbf{n}}$（$\hat{\mathbf{n}}$ 为法向单位矢量）。这意味着在没有[自由电流](@entry_id:191634)的情况下，我们可以把静[磁场](@entry_id:153296)问题转化为一个静电场问题来求解：非均匀的磁化强度 $\mathbf{M}$ 在数学上等效于一个[空间分布](@entry_id:188271)的“磁荷”，这些磁荷产生[磁标势](@entry_id:185708) $\Phi_M$，进而决定了 $\mathbf{H}$ 场。

例如，对于一个厚度为 $d$、磁化强度为 $\mathbf{M}(z) = (M_c + \alpha z)\hat{z}$ 的无限大平板，尽管磁化强度随位置变化，但因为没有[自由电流](@entry_id:191634)，我们依然可以使用[磁标势](@entry_id:185708)方法。通过计算，我们发现等效磁[体电荷密度](@entry_id:264747)为 $\rho_M = -\alpha$，而在上表面（$z=d/2$）和下表面（$z=-d/2$）的[磁面](@entry_id:204802)[电荷密度](@entry_id:144672)分别为 $M_c + \alpha d/2$ 和 $-M_c + \alpha d/2$。利用这些磁荷，可以求出板内的 $\mathbf{H}$ 场为 $\mathbf{H}(z) = -(M_c + \alpha z)\hat{z}$。进而，可以计算出整个平板的[磁标势](@entry_id:185708)差为 $\Delta\Phi_M = M_c d$ [@problem_id:1609094]。这种方法在[永磁体](@entry_id:189081)设计和地磁学等领域非常有用。

### 介质交界面上的边界条件

当[电磁场](@entry_id:265881)穿过两种不同介质的交界面时，场矢量会发生变化。这些变化规律由边界条件描述，它们可以由[麦克斯韦方程组的积分形式](@entry_id:264550)应用于跨越界面的微小“高斯药丸盒”和“[安培环路](@entry_id:275261)”导出。对于[辅助场](@entry_id:155519) $\mathbf{D}$ 和 $\mathbf{H}$，边界条件尤为重要。

假设界面上存在自由面[电荷密度](@entry_id:144672) $\sigma_f$ 和自由面[电流密度](@entry_id:190690) $\mathbf{K}_f$。令 $\hat{\mathbf{n}}$ 为从介质2指向介质1的法向单位矢量，则四个边界条件为：
1.  **$D$ 的法向分量**：$\oint \mathbf{D} \cdot d\mathbf{a} = Q_{f, \text{enclosed}} \implies \mathbf{D}_1 \cdot \hat{\mathbf{n}} - \mathbf{D}_2 \cdot \hat{\mathbf{n}} = \sigma_f$ 或 $D_{1}^{\perp} - D_{2}^{\perp} = \sigma_f$。$\mathbf{D}$ 的法向分量在界面上的跃变等于该处的自由面[电荷密度](@entry_id:144672)。
2.  **$B$ 的法向分量**：$\oint \mathbf{B} \cdot d\mathbf{a} = 0 \implies \mathbf{B}_1 \cdot \hat{\mathbf{n}} - \mathbf{B}_2 \cdot \hat{\mathbf{n}} = 0$ 或 $B_{1}^{\perp} = B_{2}^{\perp}$。$\mathbf{B}$ 的法向分量总是连续的。
3.  **$E$ 的切向分量**：$\oint \mathbf{E} \cdot d\mathbf{l} = 0$（在[静磁学](@entry_id:140120)或变化缓慢的场中）$\implies \mathbf{E}_1^{\parallel} - \mathbf{E}_2^{\parallel} = \mathbf{0}$。$\mathbf{E}$ 的切向分量总是连续的。
4.  **$H$ 的切向分量**：$\oint \mathbf{H} \cdot d\mathbf{l} = I_{f, \text{enc}} \implies \hat{\mathbf{n}} \times (\mathbf{H}_1 - \mathbf{H}_2) = \mathbf{K}_f$。$\mathbf{H}$ 的切向分量在界面上的跃变由与之垂直的自由面电流密度决定。这个关系可以通过对一个跨越界面的无限小矩形环路应用安培定律来严格导出 [@problem_id:589534]。

这些边界条件是解决涉及多种介质的电磁学问题的基石。

让我们通过一个具体的例子来展示这些边界条件的应用。考虑两种磁性材料（[相对磁导率](@entry_id:272081)分别为 $\mu_{r1}, \mu_{r2}$）在 $z=0$ 平面接触，界面上流过沿 $y$ 方向的均匀自由面电流 $\mathbf{K}_f = K_f \hat{\mathbf{y}}$。如果区域1 ($z0$) 中存在一个与 $z$ 轴成 $\theta_1$ 角的[磁感应强度](@entry_id:144179)为 $\mathbf{B}_1$ 的场，我们可以利用边界条件来求解区域2 ($z0$) 中的[辅助磁场](@entry_id:261447) $\mathbf{H}_2$ [@problem_id:1609070]。

首先，分解 $\mathbf{B}_1$ 为法向分量 $B_{1,z}$ 和切向分量 $B_{1,x}$。
- 根据 $B_{1}^{\perp} = B_{2}^{\perp}$，我们得到 $B_{2,z} = B_{1,z}$。于是 $H_{2,z} = B_{2,z} / \mu_2 = B_{1,z} / (\mu_0 \mu_{r2})$。
- 根据 $\hat{\mathbf{z}} \times (\mathbf{H}_2 - \mathbf{H}_1) = \mathbf{K}_f$，我们得到 $H_{2,x} - H_{1,x} = K_f$ 和 $H_{2,y} - H_{1,y} = 0$。由于 $\mathbf{B}_1$ 在 $xz$ 平面内， $H_{1,y}=0$，所以 $H_{2,y}=0$。而 $H_{1,x} = B_{1,x}/\mu_1 = B_{1,x}/(\mu_0 \mu_{r1})$。因此，$H_{2,x} = K_f + H_{1,x}$。
通过上述步骤，我们求得了 $\mathbf{H}_2$ 的所有分量，进而可以计算其大小 $|\mathbf{H}_2| = \sqrt{H_{2,x}^2 + H_{2,z}^2}$。

另一个例子是分析磁[屏蔽效应](@entry_id:136974)。一块[相对磁导率](@entry_id:272081)为 $\mu_r$ 的[磁性材料](@entry_id:137953)平板（区域2）置于真空中（区域1和3）。如果在 $z=0$ 的界面有面电流 $\mathbf{K}_f$，而在 $z=d$ 的界面没有，我们可以追踪场的变化。从区域1到区域2，$\mathbf{B}$ 的法向分量连续，而 $\mathbf{H}$ 的切向分量发生跃变。从区域2到区域3，由于没有面电流，$\mathbf{H}$ 的切向分量连续，同时 $\mathbf{B}$ 的法向分量仍然连续。通过这种方式，我们可以精确地计算出穿过屏蔽材料后，在区域3的[磁场](@entry_id:153296) $\mathbf{B}_3$ [@problem_id:1609050]。这些计算表明，正确区分和使用 $\mathbf{B}$ 和 $\mathbf{H}$ 的边界条件是求解此类问题的关键。

### 完整[宏观麦克斯韦方程组](@entry_id:201246)中的[辅助场](@entry_id:155519)

到目前为止，我们的讨论主要集中在[静电学](@entry_id:140489)和[静磁学](@entry_id:140120)。当场随时间变化时，辅助场 $\mathbf{D}$ 和 $\mathbf{H}$ 依然扮演着核心角色。完整的[宏观麦克斯韦方程组](@entry_id:201246)（也称为[物质中的麦克斯韦方程组](@entry_id:272703)）用这四个场 $(\mathbf{E}, \mathbf{B}, \mathbf{D}, \mathbf{H})$ 写出如下形式：

1.  **高斯定律 ([电场](@entry_id:194326))**: $\nabla \cdot \mathbf{D} = \rho_f$
2.  **高斯定律 ([磁场](@entry_id:153296))**: $\nabla \cdot \mathbf{B} = 0$
3.  **[法拉第感应定律](@entry_id:146175)**: $\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}$
4.  **[安培-麦克斯韦定律](@entry_id:266368)**: $\nabla \times \mathbf{H} = \mathbf{J}_f + \frac{\partial \mathbf{D}}{\partial t}$

在这个完备的[方程组](@entry_id:193238)中，法拉第定律的形式保持不变，因为它描述的是[磁场](@entry_id:153296)变化如何产生[电场](@entry_id:194326)，这是一个不依赖于介质的具体响应方式的基本物理规律。而[安培-麦克斯韦定律](@entry_id:266368)则包含了一个至关重要的项：$\frac{\partial \mathbf{D}}{\partial t}$。这一项被称为**位移电流密度**。在真空中，$\mathbf{D} = \epsilon_0 \mathbf{E}$，该项退化为 $\epsilon_0 \frac{\partial \mathbf{E}}{\partial t}$。在介质中，由于 $\mathbf{D} = \epsilon_0 \mathbf{E} + \mathbf{P}$，[位移电流](@entry_id:190231)包含了[电场](@entry_id:194326)变化和[极化强度](@entry_id:188176)变化两部分的贡献：$\frac{\partial \mathbf{D}}{\partial t} = \epsilon_0 \frac{\partial \mathbf{E}}{\partial t} + \frac{\partial \mathbf{P}}{\partial t}$。其中 $\frac{\partial \mathbf{P}}{\partial t}$ 对应于束缚[电荷](@entry_id:275494)的运动，即**[极化电流](@entry_id:196744)**。

这套[方程组](@entry_id:193238)优雅地描述了[电磁波](@entry_id:269629)在介质中的传播。例如，在一个没有[自由电荷](@entry_id:264392)和[自由电流](@entry_id:191634)的绝缘介质中，[方程组](@entry_id:193238)变为：
$$ \nabla \cdot \mathbf{D} = 0 $$
$$ \nabla \cdot \mathbf{B} = 0 $$
$$ \nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t} $$
$$ \nabla \times \mathbf{H} = \frac{\partial \mathbf{D}}{\partial t} $$
考虑一个沿 $z$ 轴传播的平面[电磁波](@entry_id:269629)，其[辅助磁场](@entry_id:261447)为 $\mathbf{H}(z, t) = \hat{y} H_0 \cos(kz - \omega t)$。我们可以利用[安培-麦克斯韦定律](@entry_id:266368) $\nabla \times \mathbf{H} = \frac{\partial \mathbf{D}}{\partial t}$ 来求解相应的[电位移场](@entry_id:273493) $\mathbf{D}$。计算 $\mathbf{H}$ 的旋度得到 $\nabla \times \mathbf{H} = -\hat{x} k H_0 \sin(kz - \omega t)$。对时间积分，并假设没有静态背景场，我们便可求得[电位移场](@entry_id:273493)为 $\mathbf{D}(z, t) = -\hat{x} \frac{k}{\omega} H_0 \cos(kz - \omega t)$ [@problem_id:1822453]。这个结果展示了在[电磁波](@entry_id:269629)中，$\mathbf{D}$ 场和 $\mathbf{H}$ 场是如何相互耦合、协同传播的，也再次印证了辅助场在[电动力学](@entry_id:158759)中的核心地位。