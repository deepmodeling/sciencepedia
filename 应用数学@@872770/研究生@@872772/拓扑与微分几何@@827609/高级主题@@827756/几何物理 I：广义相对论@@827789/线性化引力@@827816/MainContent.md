## 引言
广义相对论将[引力](@entry_id:175476)描述为时空的弯曲，但其核心的爱因斯坦场方程极其复杂，难以求解。然而，在宇宙的许多场景中，如太阳系或遥远天体传来的[引力](@entry_id:175476)波，[引力场](@entry_id:169425)非常微弱。在这种情况下，线性化[引力](@entry_id:175476)理论应运而生，它将复杂的时空几何简化为平直时空上的微小涟漪。这种强大的近似方法不仅保留了广义相对论的深刻物理内涵，还为预测[引力](@entry_id:175476)波等新现象提供了可能。本文旨在系统地引导读者掌握线性化[引力](@entry_id:175476)的精髓。

在“原理和机制”一章中，我们将建立线性化理论的数学基础，探讨[度规微扰](@entry_id:160321)与规范自由度的概念。接着，在“应用与跨学科联系”一章中，我们将展示该理论如何在天体物理学、宇宙学和量子物理学中大放异彩。最后，通过“动手实践”部分，读者将有机会运用所学知识解决具体问题，巩固理解。

## 原理和机制

在前一章中，我们介绍了广义相对论的核心思想，即[引力](@entry_id:175476)并非一种力，而是时空本身因物质和能量的存在而发生的弯曲。求解完整、[非线性](@entry_id:637147)的爱因斯坦场方程是一项艰巨的任务，通常只在高度对称的理想化情况下才有可能。然而，在许多重要的物理情境中，例如在太阳系中或在遥远天体产生的[引力](@entry_id:175476)波传播到地球时，[引力场](@entry_id:169425)非常微弱。在这些情况下，我们可以将[时空几何](@entry_id:139497)视为平直的[闵可夫斯基时空](@entry_id:156421)的微小偏离。这种处理方法被称为**线性化[引力](@entry_id:175476)** (linearized gravity)，它极大地简化了爱因斯坦的理论，同时保留了其丰富的物理内涵，为我们理解[引力](@entry_id:175476)的基本机制和预测新的物理现象（如[引力](@entry_id:175476)波）提供了强有力的工具。本章将系统地阐述线性化[引力](@entry_id:175476)的核心原理与机制。

### [度规微扰](@entry_id:160321)与规范不变性

线性化[引力](@entry_id:175476)的出发点是将时空度规张量 $g_{\mu\nu}$ 分解为一个固定的平直背景度规 $\eta_{\mu\nu}$ 和一个小的微扰 $h_{\mu\nu}$：
$$g_{\mu\nu} = \eta_{\mu\nu} + h_{\mu\nu}$$
其中 $|h_{\mu\nu}| \ll 1$。在本章中，我们采用 $(-,+,+,+)$ 的度规符号，即 $\eta_{\mu\nu} = \text{diag}(-1, 1, 1, 1)$。这意味着 $h_{\mu\nu}$ 的所有分量的[绝对值](@entry_id:147688)都远小于1，因此我们可以忽略所有高于 $h_{\mu\nu}$ 一阶的项。在这种近似下，度规的逆 $g^{\mu\nu}$ 可以写为 $g^{\mu\nu} \approx \eta^{\mu\nu} - h^{\mu\nu}$，其中指标由 $\eta^{\mu\nu}$ 升降（例如，$h^{\mu\nu} = \eta^{\mu\alpha}\eta^{\nu\beta}h_{\alpha\beta}$）。

广义相对论的一个基本特征是**[广义协变性](@entry_id:159290)**，即物理定律在任意坐标变换下形式不变。在线性化理论中，这体现为一种称为**规范自由度** (gauge freedom) 的对称性。考虑一个无穷小的坐标变换：
$$x^\mu \to x'^\mu = x^\mu - \xi^\mu(x)$$
其中 $\xi^\mu(x)$ 是一个时空坐标的任意小的矢量场。在这种变换下，[度规微扰](@entry_id:160321)会发生改变。可以证明，变换后的[度规微扰](@entry_id:160321) $h'_{\mu\nu}$ 与原微扰 $h_{\mu\nu}$ 的关系为：
$$h'_{\mu\nu}(x') \approx h_{\mu\nu}(x) + \partial_\mu \xi_\nu + \partial_\nu \xi_\mu$$
其中 $\partial_\mu \equiv \frac{\partial}{\partial x^\mu}$，且 $\xi_\nu = \eta_{\nu\rho}\xi^\rho$。这表明，$h_{\mu\nu}$ 和 $h'_{\mu\nu}$ 描述的是同一个物理实在，它们只是在不同[坐标系](@entry_id:156346)下的表现。它们被称为**规范等效**的。

一个特别重要的概念是“纯规范”微扰。如果我们从一个完全平直的闵可夫斯基时空（即 $h_{\mu\nu}=0$）开始，然后进行上述的无穷小[坐标变换](@entry_id:172727)，我们就会在新的[坐标系](@entry_id:156346)中“凭空”产生一个非零的[度规微扰](@entry_id:160321) [@problem_id:1829192]：
$$h'_{\mu\nu} = \partial_\mu \xi_\nu + \partial_\nu \xi_\mu$$
这种微扰并不代表真实的[引力场](@entry_id:169425)，它仅仅是[坐标系](@entry_id:156346)选择的人为产物。例如，考虑一个由矢量场 $\xi^\mu(x) = A^\mu \cos(k_\rho x^\rho)$ 生成的微扰，其中 $A^\mu = (0, A, 0, 0)$，$k^\mu = (\frac{\omega}{c}, 0, 0, \frac{\omega}{c})$。这个矢量场只在 $x$ 方向有分量，但它依赖于 $t$ 和 $z$ 坐标。由此产生的[度规微扰](@entry_id:160321)分量之一 $h'_{13}$ 可以通过计算 $\partial_1 \xi_3 + \partial_3 \xi_1$ 得到。由于 $\xi_3=0$，我们只需计算 $\partial_3 \xi_1 = \partial_z (A \cos(\omega(z/c - t)))$，结果为 $h'_{13}(t,z) = -\frac{A \omega}{c} \sin(\omega(\frac{z}{c} - t))$。这个非零的微扰分量看起来像一个波，但它不携带任何物理效应。

物理[引力场](@entry_id:169425)的标志是它能够产生潮汐力，使邻近的自由下落物体相互加速。在数学上，这由**黎曼曲率张量** $R^\alpha{}_{\beta\mu\nu}$ 描述。一个真实的[引力场](@entry_id:169425)必须对应一个非零的[曲率张量](@entry_id:181383)。在线性化理论中，黎曼张量 $R^{(1)}_{\mu\nu\rho\sigma}$ 可以表示为[度规微扰](@entry_id:160321)的[二阶导数](@entry_id:144508)的线性组合：
$$R^{(1)}_{\mu\nu\rho\sigma} = \frac{1}{2} (\partial_\rho\partial_\nu h_{\mu\sigma} - \partial_\sigma\partial_\nu h_{\mu\rho} - \partial_\rho\partial_\mu h_{\nu\sigma} + \partial_\sigma\partial_\mu h_{\nu\rho})$$
我们可以通过直接代入来验证一个纯规范微扰 $h_{\mu\nu} = \partial_\mu \xi_\nu + \partial_\nu \xi_\mu$ 所产生的曲率。假定偏导数可以交换次序，经过一番代数计算，可以发现所有项都精确地相互抵消 [@problem_id:1829180]。因此，对于任何纯规范微扰，我们有：
$$R^{(1)}_{\mu\nu\rho\sigma} = 0$$
这一结果至关重要：它表明[规范自由度](@entry_id:160491)所产生的[度规微扰](@entry_id:160321)不产生任何时空曲率，因此不对应任何物理可观测的[引力](@entry_id:175476)效应。真正的[引力场](@entry_id:169425)蕴含在那些不能通过[坐标变换](@entry_id:172727)消除的[度规微扰](@entry_id:160321)分量之中。

### 弱场的几何

为了从[度规微扰](@entry_id:160321) $h_{\mu\nu}$ 计算曲率，我们首先需要计算**[克里斯托费尔符号](@entry_id:159831)** (Christoffel symbols)，它描述了时空的联络（即如何对矢量进行[平行输运](@entry_id:160671)）。在线性化近似下，克里斯托费尔符号为：
$$\Gamma^{(1)\lambda}_{\mu\nu} = \frac{1}{2}\eta^{\lambda\rho}(\partial_\mu h_{\nu\rho} + \partial_\nu h_{\mu\rho} - \partial_\rho h_{\mu\nu})$$
这个公式是[连接度](@entry_id:185181)规和[时空几何](@entry_id:139497)的桥梁。例如，考虑一个[对角形式](@entry_id:264850)的微扰，其非零分量为 $h_{00} = f(t)$ 和 $h_{11} = g(x)$ [@problem_id:1836976]。利用上述公式，我们可以计算出所有非零的[克里斯托费尔符号](@entry_id:159831)。例如，对于 $\Gamma^{0}_{00}$：
$$\Gamma^{0}_{00} = \frac{1}{2}\eta^{0\rho}(2\partial_0 h_{0\rho} - \partial_\rho h_{00}) = \frac{1}{2}\eta^{00}(2\partial_0 h_{00} - \partial_0 h_{00}) = \frac{1}{2}(-1)\partial_0 h_{00} = -\frac{1}{2}\dot{f}(t)$$
其中 $\dot{f} \equiv df/dt$。类似地，可以发现 $\Gamma^{1}_{11} = \frac{1}{2}g'(x)$，其中 $g' \equiv dg/dx$。所有其他分量均为零。这个例子清晰地展示了度规分量的时空变化率如何直接转化为克里斯托费尔符号的非零分量。

有了克里斯托费尔符号，我们就可以构建线性的**里奇张量** (Ricci tensor) $R^{(1)}_{\mu\nu}$ 和**[里奇标量](@entry_id:158934)** (Ricci scalar) $R^{(1)}$：
$$R^{(1)}_{\mu\nu} = \partial_\rho \Gamma^{(1)\rho}_{\mu\nu} - \partial_\nu \Gamma^{(1)\rho}_{\mu\rho}$$
$$R^{(1)} = \eta^{\mu\nu} R^{(1)}_{\mu\nu}$$
这些量是爱因斯坦场方程的核心组成部分。经过一些代数运算，里奇标量可以直接用[度规微扰](@entry_id:160321)及其迹 $h = \eta^{\mu\nu}h_{\mu\nu}$ 表示为一个更紧凑的形式：
$$R^{(1)} = \partial_\mu \partial_\nu h^{\mu\nu} - \Box h$$
其中 $\Box = \eta^{\mu\nu}\partial_\mu\partial_\nu = -\frac{1}{c^2}\frac{\partial^2}{\partial t^2} + \nabla^2$ 是[达朗贝尔算符](@entry_id:275913)。这个表达式在实际计算中非常有用 [@problem_id:986833]。

### 线性化爱因斯坦方程

爱因斯坦场方程 $G_{\mu\nu} = \frac{8\pi G}{c^4} T_{\mu\nu}$ 在线性化近似下，其左侧的爱因斯坦张量 $G_{\mu\nu} = R_{\mu\nu} - \frac{1}{2}g_{\mu\nu}R$ 也被线性化为 $G^{(1)}_{\mu\nu}$。直接用 $h_{\mu\nu}$ 表达 $G^{(1)}_{\mu\nu}$ 会得到一个相当复杂的表达式。为了简化它，我们引入一个非常有用的辅助场，称为**迹反转[度规微扰](@entry_id:160321)** (trace-reversed metric perturbation) $\bar{h}_{\mu\nu}$：
$$\bar{h}_{\mu\nu} = h_{\mu\nu} - \frac{1}{2}\eta_{\mu\nu}h$$
其中 $h = \eta^{\alpha\beta}h_{\alpha\beta}$ 是 $h_{\mu\nu}$ 的迹。这个定义的巧妙之处在于它简化了场方程的结构。首先，我们可以计算 $\bar{h}_{\mu\nu}$ 的迹 $\bar{h} = \eta^{\mu\nu}\bar{h}_{\mu\nu}$：
$$\bar{h} = \eta^{\mu\nu}(h_{\mu\nu} - \frac{1}{2}\eta_{\mu\nu}h) = h - \frac{1}{2}h(\eta^{\mu\nu}\eta_{\mu\nu}) = h - \frac{1}{2}h \cdot 4 = -h$$
因此，在四维时空中，迹反转操作会使迹变号 [@problem_id:1836964]。反过来，我们也可以用 $\bar{h}_{\mu\nu}$ 及其迹 $\bar{h}$ 来表示 $h_{\mu\nu}$：$h_{\mu\nu} = \bar{h}_{\mu\nu} - \frac{1}{2}\eta_{\mu\nu}\bar{h}$。

作为一个具体的计算练习，考虑一个对角微扰 $h_{\mu\nu} = \text{diag}(2\Phi, 2\Phi, 2\Phi, 2\Phi)$ [@problem_id:1836993]。其迹为 $h = \eta^{\mu\nu}h_{\mu\nu} = (-1)(2\Phi) + (1)(2\Phi) + (1)(2\Phi) + (1)(2\Phi) = 4\Phi$。那么 $\bar{h}_{00}$ 分量为：
$$\bar{h}_{00} = h_{00} - \frac{1}{2}\eta_{00}h = 2\Phi - \frac{1}{2}(-1)(4\Phi) = 4\Phi$$
而空间分量 $\bar{h}_{ii}$ (对 $i=1,2,3$ 不求和) 为：
$$\bar{h}_{ii} = h_{ii} - \frac{1}{2}\eta_{ii}h = 2\Phi - \frac{1}{2}(1)(4\Phi) = 0$$
因此，$\bar{h}_{\mu\nu} = \text{diag}(4\Phi, 0, 0, 0)$。

利用 $\bar{h}_{\mu\nu}$，线性化的爱因斯坦张量可以写成一个更简洁的形式。更进一步，我们可以利用规范自由度来施加一个称为**[洛伦兹规范](@entry_id:153650)** (Lorenz gauge) 的条件：
$$\partial_\mu \bar{h}^{\mu\nu} = 0$$
在这个规范下，线性化的爱因斯坦场方程最终呈现为一个优美的波动方程形式：
$$\Box \bar{h}_{\mu\nu} = -\frac{16\pi G}{c^4} T_{\mu\nu}$$
这个[方程组](@entry_id:193238)是线性化[引力](@entry_id:175476)的核心动力学方程。它表明，物质-能量（由能量-动量张量 $T_{\mu\nu}$ 描述）作为源，产生了以光速传播的[度规微扰](@entry_id:160321)场 $\bar{h}_{\mu\nu}$。

### 应用 I：[牛顿极限](@entry_id:260781)

线性化[引力](@entry_id:175476)的一个重要成功之处在于它能在适当的近似下恢复我们熟悉的[牛顿引力](@entry_id:159796)理论。这为广义相对论提供了坚实的实验基础，并确立了度规分量与[牛顿引力](@entry_id:159796)势之间的联系。

首先，我们考虑一个质量为 $m$ 的非相对论性检验粒子（速度 $v \ll c$）在一个静态（不随时间变化）的弱[引力场](@entry_id:169425)中运动。根据广义相对论，自由下落的粒子遵循测地线方程：
$$\frac{d^2 x^\mu}{d\tau^2} + \Gamma^\mu_{\alpha\beta} \frac{dx^\alpha}{d\tau} \frac{dx^\beta}{d\tau} = 0$$
在静态、弱场且主要由大质量源产生的[引力场](@entry_id:169425)中，一个很好的近似是只保留 $h_{00}$ 分量，并令其他 $h_{\mu\nu}$ 分量为零。在这种情况下，唯一显著的克里斯托费尔符号是 $\Gamma^i_{00} = -\frac{1}{2}\partial_i h_{00}$（其中 $i$ 是空间指标）。对于慢速运动的粒子，$d\tau \approx dt$，且 $\frac{dx^0}{dt}=c$ 远大于 $\frac{dx^i}{dt}$。因此，[测地线方程](@entry_id:264349)的空间部分近似为：
$$\frac{d^2 x^i}{dt^2} + \Gamma^i_{00} \left(\frac{dx^0}{dt}\right)^2 \approx 0 \implies \vec{a} = \frac{d^2 \vec{x}}{dt^2} \approx -c^2 \vec{\Gamma}_{00} = \frac{c^2}{2}\vec{\nabla}h_{00}$$
如果我们将这个结果与[牛顿引力定律](@entry_id:167292) $\vec{a} = -\vec{\nabla}\Phi$ 进行比较，其中 $\Phi$ 是牛顿引力势，我们就能建立 $h_{00}$ 和 $\Phi$ 之间的联系：$\frac{c^2}{2}\vec{\nabla}h_{00} = -\vec{\nabla}\Phi$。积分可得 $h_{00} = -\frac{2\Phi}{c^2}$ （积分常数可通过在无穷远处场为零来确定）[@problem_id:1836967]。

其次，我们可以从场方程的角度来验证这个关系。考虑一个由静态、非相对论性物质（“尘埃”）组成的源，其质量密度为 $\rho(\vec{x})$。其能量-动量张量为 $T_{00}=\rho c^2$，其他分量为零。由于场是静态的，$\Box$ 算符简化为拉普拉斯算符 $\nabla^2$。线性化爱因斯坦方程的 $(0,0)$ 分量变为：
$$\nabla^2 \bar{h}_{00} = -\frac{16\pi G}{c^4}T_{00} = -\frac{16\pi G \rho}{c^2}$$
与牛顿引力的泊松方程 $\nabla^2 \Phi = 4\pi G \rho$ 相比，我们得到 $\nabla^2 \bar{h}_{00} = -\frac{4}{c^2}\nabla^2\Phi$，这意味着 $\bar{h}_{00} = -\frac{4\Phi}{c^2}$。为了将此结果与 $h_{00}$ 联系起来，我们注意到对于静态尘埃源，在[洛伦兹规范](@entry_id:153650)下，方程的解具有 $\bar{h}_{ii}=0$ 的性质。因此，迹反转微扰的迹为 $\bar{h} = \eta^{\mu\nu}\bar{h}_{\mu\nu} = \eta^{00}\bar{h}_{00} = -\bar{h}_{00}$。利用迹反转的[逆关系](@entry_id:274206) $h_{\mu\nu} = \bar{h}_{\mu\nu} - \frac{1}{2}\eta_{\mu\nu}\bar{h}$，可得 $h_{00} = \bar{h}_{00} - \frac{1}{2}\eta_{00}\bar{h} = \bar{h}_{00} - \frac{1}{2}(-1)(-\bar{h}_{00}) = \frac{1}{2}\bar{h}_{00}$。综合这些结果，我们最终得到 $h_{00} = \frac{1}{2}\bar{h}_{00} = -\frac{2\Phi}{c^2}$ [@problem_id:986793]。这与从[测地线方程](@entry_id:264349)得到的结果完全一致，表明了理论的自洽性。

这个 $h_{00} = -2\Phi/c^2$ 的关系有一个直接的可观测效应：**引力红移** (gravitational redshift)。对于一个静止在[引力场](@entry_id:169425)中的时钟，其固有时 $d\tau$ 与[坐标时](@entry_id:263720) $dt$ 的关系为 $d\tau = \sqrt{-g_{00}} dt/c$。在线性化近似下，$g_{00} = -1+h_{00}$，所以：
$$d\tau = \frac{1}{c}\sqrt{1-h_{00}} dt \approx \frac{1}{c}\left(1 - \frac{1}{2}h_{00}\right) dt$$
由于 $h_{00}$ 通常是负值（例如，在吸引人的质量周围 $\Phi  0$），[引力场](@entry_id:169425)越强（$|h_{00}|$ 越大），固有时钟走得越慢。考虑两个分别位于 $\vec{r}_A$ 和 $\vec{r}_B$ 的时钟。A 处时钟以频率 $\nu_A$ 发射电磁信号，B 处接收到的频率为 $\nu_B$。频率与固有时成反比，$\nu \propto 1/\Delta\tau$。因此，[频率比](@entry_id:202730)为：
$$\frac{\nu_B}{\nu_A} = \frac{\Delta\tau_A}{\Delta\tau_B} \approx \frac{1 - \frac{1}{2}h_{00}(\vec{r}_A)}{1 - \frac{1}{2}h_{00}(\vec{r}_B)} \approx \left(1 - \frac{1}{2}h_{00}(\vec{r}_A)\right)\left(1 + \frac{1}{2}h_{00}(\vec{r}_B)\right) \approx 1 + \frac{1}{2}(h_{00}(\vec{r}_B) - h_{00}(\vec{r}_A))$$
分数频率偏移为 $\frac{\Delta\nu}{\nu} \approx \frac{1}{2}(h_{00}(\vec{r}_B) - h_{00}(\vec{r}_A))$。将 $h_{00} = -2\Phi/c^2$ 代入，得到 $\frac{\Delta\nu}{\nu} \approx \frac{\Phi(\vec{r}_A) - \Phi(\vec{r}_B)}{c^2}$。这就是著名的引力红移公式。例如，在一个由 $h_{00} = -A(x^2+y^2)$ 描述的假设[引力场](@entry_id:169425)中，一个位于原点的观测者 A ($h_{00,A}=0$) 接收到来自位于 $(L,0,0)$ 的时钟 B ($h_{00,B}=-AL^2$) 的信号，其频率偏移为 $\frac{\Delta\nu}{\nu} \approx \frac{1}{2}(-AL^2 - 0) = -\frac{1}{2}AL^2$ [@problem_id:1878705]。负号表示接收到的频率更低（红移），这与光从[引力势](@entry_id:160378)更深处（B点）传向[引力势](@entry_id:160378)较浅处（A点）的物理预期相符。

### 应用 II：[引力](@entry_id:175476)波

线性化[引力](@entry_id:175476)的第二个伟大预测是**[引力](@entry_id:175476)波** (gravitational waves) 的存在。在远离物质源的真空区域（$T_{\mu\nu}=0$），线性化爱因斯坦方程变为齐次波动方程：
$$\Box \bar{h}_{\mu\nu} = 0$$
这个方程的解代表了以光速 $c$ 传播的时空几何的涟漪。一个特别重要的解是[平面波解](@entry_id:195230)，形式为 $\bar{h}_{\mu\nu}(x) = \text{Re}(C_{\mu\nu} e^{ik_\alpha x^\alpha})$，其中 $C_{\mu\nu}$ 是一个常数张量（极化张量），$k^\alpha$ 是[波矢](@entry_id:178620)，满足 $k_\alpha k^\alpha = 0$（表明以光速传播）。

通过进一步利用规范自由度，我们可以选择一个特别方便的规范，称为**[横向无迹规范](@entry_id:273582)** (Transverse-Traceless, TT gauge)。在这个规范下，[度规微扰](@entry_id:160321)满足：
1.  **横向条件**: $k^\mu h^{TT}_{\mu\nu} = 0$。对于沿 $z$ 轴传播的波 ($k^\mu = (\omega/c, 0, 0, \omega/c)$)，这意味着所有带有时空指标 $0$ 或 $3$ 的分量都与波的传播方向有关，可以被设为零（更准确地说是 $h^{TT}_{0\mu} = 0$ 且 $\sum_j k_j h^{TT}_{j i} = 0$）。物理扰动只存在于垂直于传播方向的平面上（$xy$ 平面）。
2.  **无迹条件**: $h^{TT\mu}_{\mu} = \eta^{\mu\nu}h^{TT}_{\mu\nu} = 0$。

在[TT规范](@entry_id:273582)下，一个沿 $z$ 轴传播的[引力](@entry_id:175476)波的所有信息都包含在 $xy$ 平面上的 $2 \times 2$ 对称无迹矩阵 $h^{TT}_{ij}$ 中。一个对称的 $2 \times 2$ 矩阵有三个独立分量，无迹条件又去掉一个，所以只剩下两个独立的物理自由度。这对应于[引力](@entry_id:175476)波的两种**极化** (polarization) 状态。它们通常被称为“加”极化 ($+$) 和“叉”极化 ($\times$)，其标准极化张量 $e^+_{ij}$ 和 $e^\times_{ij}$ 为：
$$e^+_{ij} = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}, \quad e^\times_{ij} = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}$$
一个通用的沿 $z$ 轴传播的[引力](@entry_id:175476)波可以写成这两种极化的线性叠加：
$$h^{TT}_{ij}(t, z) = H_+(t-z/c) e^+_{ij} + H_\times(t-z/c) e^\times_{ij}$$
其中 $H_+$ 和 $H_\times$ 是两个任意的波形函数。这种极化基底的选择与定义 $xy$ 平面的坐标轴有关。如果我们在一个以角速度 $\Omega$ 旋转的[坐标系](@entry_id:156346)中定义极化基底，那么在固定的实验室坐标系看来，极化张量的分量也会随[时间演化](@entry_id:153943)。例如，如果极化基底是相对于旋转矢量 $\mathbf{u}(t) = (\cos(\Omega t), \sin(\Omega t), 0)$ 和 $\mathbf{v}(t) = (-\sin(\Omega t), \cos(\Omega t), 0)$ 定义的，那么实验室坐标系中的加极化张量的 $xy$ 分量将是 $e_{xy}^+(t) = u_x u_y - v_x v_y = \cos(\Omega t)\sin(\Omega t) - (-\sin(\Omega t))\cos(\Omega t) = \sin(2\Omega t)$ [@problem_id:1120610]。

[引力](@entry_id:175476)波不仅仅是时空的几何游戏，它们还真实地携带能量和动量。然而，能量-动量本身是[引力场](@entry_id:169425)的源，这使得定义[引力场](@entry_id:169425)的能量变得非常棘手。在线性化理论的框架下，可以证明，[引力](@entry_id:175476)波的能量是一种二阶效应，正比于 $h^2$。我们可以定义一个**有效能量-动量张量** $T^{\text{GW}}_{\mu\nu}$，它代表了在一个时空区域内（远大于波长）平均的、由[引力波携带的能量](@entry_id:262866)和动量：
$$T^{\text{GW}}_{\mu\nu} = \frac{c^4}{32\pi G} \langle \partial_\mu h^{TT}_{\alpha\beta} \partial_\nu h^{TT\alpha\beta} \rangle$$
这里的尖括号 $\langle \dots \rangle$ 表示对几个波周期进行时间平均。[能量流](@entry_id:142770)密度（单位时间单位面积通过的能量），或称能流，由分量 $P^z = c T^{0z}_{\text{GW}}$ 给出。

我们来计算一个沿 $z$ 方向传播的单色、圆极化[引力](@entry_id:175476)波的能流 [@problem_id:986821]。其[度规微扰](@entry_id:160321)分量可写为 $h_{xx} = H_0 \cos(\omega(t-z/c))$，$h_{yy} = -H_0 \cos(\omega(t-z/c))$，以及 $h_{xy} = h_{yx} = H_0 \sin(\omega(t-z/c))$。[能流密度](@entry_id:266056)为 $\mathcal{F}_z = c T^{0z}$，其中 $T^{0z} = -T_{0z}$（在我们的度规符号下）。$T_{0z}$ 可由下式计算：
$$T_{0z} = \frac{c^4}{32\pi G} \langle \partial_0 h_{ij} \partial_z h^{ij} \rangle = \frac{c^3}{32\pi G} \langle (\partial_t h_{ij}) (\partial_z h_{ij}) \rangle$$
对于平面波 $h_{ij}(t-z/c)$，我们有 $\partial_z h_{ij} = -\frac{1}{c} \partial_t h_{ij}$。因此 $T_{0z} = -\frac{c^2}{32\pi G} \langle \sum_{i,j} (\partial_t h_{ij})^2 \rangle$。导数的平方和为 $\sum (\partial_t h_{ij})^2 = (\partial_t h_{xx})^2 + (\partial_t h_{yy})^2 + 2(\partial_t h_{xy})^2 = 2 H_0^2\omega^2$。这是一个常数，所以它的平均值就是它本身。代入后得到 $T_{0z} = -\frac{c^2 H_0^2 \omega^2}{16\pi G}$。最终能流为：
$$\mathcal{F}_z = c(-T_{0z}) = \frac{c^3 \omega^2 H_0^2}{16\pi G}$$
这个结果表明，[引力](@entry_id:175476)波的[能量流](@entry_id:142770)与振幅的平方和频率的平方成正比，这与[电磁波](@entry_id:269629)的行为类似。正是这种能量的携带，使得我们可以通过精密的探测器（如LIGO和Virgo）探测到来自宇宙深处的[引力](@entry_id:175476)波，开启了[引力波天文学](@entry_id:750021)的新时代。