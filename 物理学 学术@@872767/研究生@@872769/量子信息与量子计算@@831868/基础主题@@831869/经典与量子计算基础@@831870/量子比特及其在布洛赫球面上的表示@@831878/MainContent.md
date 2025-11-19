## 引言
作为[量子信息](@entry_id:137721)的基本构成单元，[量子比特](@entry_id:137928)（qubit）的性质和操控是整个[量子信息科学](@entry_id:150091)的基石。然而，其在抽象的[复希尔伯特空间](@entry_id:185216)中的数学描述，虽然精确，却往往缺乏直观性，使得理解其状态、演化和测量变得颇具挑战。本文旨在填补这一认知鸿沟，通过引入布洛赫球（Bloch Sphere）这一强大的可视化工具，将单个[量子比特](@entry_id:137928)的复杂行为转化为三维空间中直观的几何图像。

本文将引导读者系统性地掌握[量子比特](@entry_id:137928)的几何表示法。在第一部分“原理与机制”中，我们将建立[量子比特](@entry_id:137928)态（包括纯态和[混合态](@entry_id:141568)）与布洛赫球上矢量之间的严格对应关系，并探讨[幺正演化](@entry_id:145020)与[退相干](@entry_id:145157)过程的几何动力学。接下来的“应用与跨学科联系”部分，将展示布洛赫[球模型](@entry_id:161388)如何在[量子计算](@entry_id:142712)、[量子控制](@entry_id:136347)、[量子计量学](@entry_id:138980)乃至与相对论的交叉领域中，提供深刻的物理洞见和解决问题的框架。最后，通过“动手实践”环节，读者将有机会巩固所学，解决具体的计算和分析问题。让我们首先深入布洛赫球的核心，探索其背后的原理与机制。

## 原理与机制

继前一章对[量子比特](@entry_id:137928)作为量子信息基本单元的介绍之后，本章将深入探讨其数学描述和几何[表示的核](@entry_id:202190)心原理与机制。我们将建立[量子比特](@entry_id:137928)状态与一个三维空间中的矢量之间的精确对应关系，即[布洛赫矢量](@entry_id:144181)（Bloch vector）。这一强大的可视化工具不仅为单个[量子比特](@entry_id:137928)的[纯态](@entry_id:141688)和[混合态](@entry_id:141568)提供了直观的几何图像，也为理解[量子门](@entry_id:143510)操作、退相干过程以及更高级的[几何相位](@entry_id:138449)等概念奠定了坚实的基础。

### [量子比特](@entry_id:137928)状态及其几何表示

一个[量子比特](@entry_id:137928)的状态可以用一个二维[复希尔伯特空间](@entry_id:185216) $\mathcal{H}$ 中的矢量来描述。最常用的基底是计算基底，由两个正交归一的态 $|0\rangle$ 和 $|1\rangle$ 构成。任何纯[量子比特](@entry_id:137928)态 $|\psi\rangle$ 都可以写成这两个[基态](@entry_id:150928)的线性叠加：
$$
|\psi\rangle = \alpha |0\rangle + \beta |1\rangle
$$
其中，$\alpha$ 和 $\beta$ 是复数，称为概率幅，且满足[归一化条件](@entry_id:156486) $|\alpha|^2 + |\beta|^2 = 1$。

然而，为了更全面地描述量子系统（包括那些与环境有相互作用的系统），我们需要引入**密度矩阵**（density matrix） $\rho$。对于一个[纯态](@entry_id:141688) $|\psi\rangle$，其[密度矩阵](@entry_id:139892)定义为 $\rho = |\psi\rangle\langle\psi|$。如果一个系统可能以概率 $p_i$ 处于一系列纯态 $|\psi_i\rangle$ 中的某一个，那么该系统的状态被称为**[混合态](@entry_id:141568)**（mixed state），其密度矩阵为这些纯态[密度矩阵](@entry_id:139892)的[凸组合](@entry_id:635830)：$\rho = \sum_i p_i |\psi_i\rangle\langle\psi_i|$。

密度矩阵具有三个基本性质：(1) [厄米性](@entry_id:141899)（$\rho^\dagger = \rho$）；(2) 单位迹（$\text{Tr}(\rho) = 1$）；(3) [半正定性](@entry_id:147720)（$\rho \ge 0$，即其[本征值](@entry_id:154894)非负）。一个态的**纯度**（purity）可以通过 $\text{Tr}(\rho^2)$ 来衡量。对于纯态，$\text{Tr}(\rho^2) = 1$；对于混合态，$\text{Tr}(\rho^2)  1$。

对于任何单[量子比特](@entry_id:137928)的[密度矩阵](@entry_id:139892)，我们可以利用[泡利矩阵](@entry_id:139493)（Pauli matrices）$\vec{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$ 将其进行分解。[泡利矩阵](@entry_id:139493)定义如下：
$$
\sigma_x = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}, \quad \sigma_y = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}, \quad \sigma_z = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}
$$
由于[泡利矩阵](@entry_id:139493)与单位矩阵 $I$ 构成了一个完备的 $2 \times 2$ 厄米矩阵基底，任何单[量子比特](@entry_id:137928)密度矩阵 $\rho$ 都可以唯一地表示为：
$$
\rho = \frac{1}{2}(I + \vec{r} \cdot \vec{\sigma}) = \frac{1}{2}(I + r_x \sigma_x + r_y \sigma_y + r_z \sigma_z)
$$
这里的矢量 $\vec{r} = (r_x, r_y, r_z)$ 是一个三维实矢量，被称为**[布洛赫矢量](@entry_id:144181)**。它的分量可以通过 $\rho$ 计算得到：$r_i = \text{Tr}(\rho \sigma_i)$。

[布洛赫矢量](@entry_id:144181)为我们提供了一个优雅的几何图像。密度矩阵的[半正定性](@entry_id:147720)条件等价于 $|\vec{r}|^2 \le 1$。这意味着所有可能的单[量子比特](@entry_id:137928)态都可以被映射到三维[欧几里得空间](@entry_id:138052)中一个半径为1的实心球内的点，这个球被称为**布洛赫球**（Bloch ball）。

- **纯态**（Pure states）对应于 $|\vec{r}|^2 = 1$，它们位于布洛赫球的表面，这个球面被称为**布洛赫球层**（Bloch sphere）。
- **[混合态](@entry_id:141568)**（Mixed states）对应于 $|\vec{r}|^2  1$，它们位于布洛赫球的内部。
- **[最大混合态](@entry_id:137775)**（Maximally mixed state）$\rho = I/2$ 对应于球心 $\vec{r} = (0,0,0)$，其纯度最低，$\text{Tr}(\rho^2) = 1/2$。

[布洛赫矢量](@entry_id:144181)的长度 $|\vec{r}|$ 直接关联于[态的纯度](@entry_id:185476)，其关系为 $|\vec{r}| = \sqrt{2\text{Tr}(\rho^2) - 1}$。

一个重要的现象是，一个[多体系统](@entry_id:144006)的纯态，其子系统的状态可能是混合的。这种现象是[量子纠缠](@entry_id:136576)的直接后果。例如，考虑一个处于纠缠态 $| \psi \rangle = \cos\theta |01\rangle - \sin\theta |10\rangle$ 的[双量子比特系统](@entry_id:203437) [@problem_id:170020]。为了得到第一个[量子比特](@entry_id:137928)的状态，我们需要计算其**[约化密度矩阵](@entry_id:146315)**（reduced density matrix） $\rho_1$，即对第二个[量子比特](@entry_id:137928)的自由度求[偏迹](@entry_id:146482)：
$$
\rho_1 = \text{Tr}_2(|\psi\rangle\langle\psi|) = \cos^2\theta |0\rangle\langle0| + \sin^2\theta |1\rangle\langle1| = \begin{pmatrix} \cos^2\theta  0 \\ 0  \sin^2\theta \end{pmatrix}
$$
这个密度矩阵对应的[布洛赫矢量](@entry_id:144181)为 $\vec{r}_1 = (0, 0, \cos^2\theta - \sin^2\theta) = (0, 0, \cos(2\theta))$。其长度为 $|\vec{r}_1| = |\cos(2\theta)|$。除非 $\theta$ 是 $\pi/2$ 的整数倍（此时系统无纠缠），否则 $|\vec{r}_1|  1$，表明第一个[量子比特](@entry_id:137928)处于一个[混合态](@entry_id:141568)。这直观地展示了纠缠如何将信息[分布](@entry_id:182848)在整个系统中，导致局部子系统失去纯度。

### 布洛赫球上的几何学

布洛赫球不仅是一个表示工具，其上的几何结构与[量子态](@entry_id:146142)的物理性质密切相关。

#### 状态、可观测量与几何关系

任何纯态都可以通过球面坐标 $(\theta, \phi)$ 参数化，其中 $\theta \in [0, \pi]$ 是极角，$\phi \in [0, 2\pi)$ 是方位角：
$$
|\psi(\theta, \phi)\rangle = \cos(\frac{\theta}{2})|0\rangle + e^{i\phi}\sin(\frac{\theta}{2})|1\rangle
$$
这个态对应的[布洛赫矢量](@entry_id:144181)为 $\vec{r} = (\sin\theta\cos\phi, \sin\theta\sin\phi, \cos\theta)$。特别地，计算[基态](@entry_id:150928) $|0\rangle$ 和 $|1\rangle$ 分别对应于北极点 $(\theta=0, \vec{r}=(0,0,1))$ 和南极点 $(\theta=\pi, \vec{r}=(0,0,-1))$。

两个相互**正交**的纯态，如任意[厄米算符](@entry_id:153410)的两个本征态，在布洛赫球上总是对应于一对**对跖点**（antipodal points）。例如，考虑算符 $A = \frac{1}{\sqrt{2}}(\sigma_x + \sigma_z)$ [@problem_id:170048]。这个算符可以写成 $\vec{n} \cdot \vec{\sigma}$ 的形式，其中 $\vec{n} = (\frac{1}{\sqrt{2}}, 0, \frac{1}{\sqrt{2}})$。其本征态的[布洛赫矢量](@entry_id:144181)恰好与 $\vec{n}$ 和 $-\vec{n}$ 方向平行，即 $\vec{r}_+ = \vec{n}$ 和 $\vec{r}_- = -\vec{n}$。这两个矢量指向对跖点，它们之间的**大圆距离**（great-circle distance），即两个矢量之间的夹角，为 $\pi$ [弧度](@entry_id:171693)。

可观测量的[期望值](@entry_id:153208)也具有清晰的几何解释。对于一个由单位矢量 $\vec{n}$ 定义的可观测量 $\hat{O} = \vec{n} \cdot \vec{\sigma}$，其在态 $\rho(\vec{r})$ 下的[期望值](@entry_id:153208)为 $\langle \hat{O} \rangle = \text{Tr}(\rho \hat{O}) = \vec{r} \cdot \vec{n}$。这个简单的[内积](@entry_id:158127)关系揭示了深刻的几何意义：所有使得该可观测量[期望值](@entry_id:153208)等于某个常数 $C$ 的[纯态](@entry_id:141688)集合，其[布洛赫矢量](@entry_id:144181) $\vec{r}$ 必须满足方程 $\vec{r} \cdot \vec{n} = C$。在布洛赫球层（$|\vec{r}|=1$）上，这个方程定义了一个平面与球面的交集，即一个**圆** [@problem_id:170027]。例如，对于[可观测量](@entry_id:267133) $\hat{O}$（由 $\vec{n} = (\frac{1}{\sqrt{2}}, 0, \frac{1}{\sqrt{2}})$ 定义）和[期望值](@entry_id:153208) $C=1/2$，这些态构成的圆的半径为 $\sqrt{1-C^2} = \sqrt{1 - (1/2)^2} = \sqrt{3}/2$。

#### 距离与可区分性

态空间中的距离衡量了[量子态](@entry_id:146142)之间的可区分性。对于两个[纯态](@entry_id:141688) $|\psi_a\rangle$ 和 $|\psi_b\rangle$，它们的**保真度**（fidelity）定义为 $F = |\langle \psi_a | \psi_b \rangle|^2$。利用[布洛赫矢量](@entry_id:144181)表示，可以证明保真度与两个态矢量 $\vec{r}_a$ 和 $\vec{r}_b$ 之间的夹角直接相关 [@problem_id:170137]：
$$
F = \text{Tr}(\rho_a \rho_b) = \frac{1}{2}(1 + \vec{r}_a \cdot \vec{r}_b)
$$
当两个态相同时，$\vec{r}_a = \vec{r}_b$，[内积](@entry_id:158127)为1，保真度为1。当两个态正交时，$\vec{r}_a = -\vec{r}_b$，[内积](@entry_id:158127)为-1，保真度为0。

更根本地，量子力学中[射影希尔伯特空间](@entry_id:188975)上的自然度量是**[富比尼-施图迪度量](@entry_id:160475)**（Fubini-Study metric）。对于单[量子比特](@entry_id:137928)，可以证明其线元 $ds_{FS}^2$ 与[布洛赫球面](@entry_id:138823)上的标准欧几里得[线元](@entry_id:196833) $ds_E^2 = (d\theta)^2 + \sin^2\theta(d\phi)^2$ 成正比 [@problem_id:170033]：
$$
ds_{FS}^2 = \frac{1}{4} ds_E^2
$$
这个 $1/4$ 的[比例因子](@entry_id:266678)确认了布洛赫球的欧几里得几何是描述[纯态](@entry_id:141688)可区分性的物理相关的几何。

对于更一般的[混合态](@entry_id:141568)，**[布雷斯距离](@entry_id:141297)**（Bures distance）$D_B$ 是一个重要的度量。它通过保真度定义，对于两个单[量子比特](@entry_id:137928)态，保真度为 $F(\rho_1, \rho_2) = \frac{1}{2} ( 1 + \vec{r}_1 \cdot \vec{r}_2 + \sqrt{(1-|\vec{r}_1|^2)(1-|\vec{r}_2|^2)} )$。[布雷斯距离](@entry_id:141297)则为 $D_B = \sqrt{2(1 - \sqrt{F})}$ [@problem_id:170160]。[布雷斯距离](@entry_id:141297)在整个布洛赫球内部定义了一个非欧几里得的黎曼几何。例如，我们可以计算由布雷斯度量诱导的体积元，并对整个布洛赫球积分，得到其总"量子体积"为 $\pi^2/8$ [@problem_id:169996]，这与欧几里得体积 $4\pi/3$ 显著不同。

### [布洛赫矢量](@entry_id:144181)的动力学

[量子态](@entry_id:146142)的演化在布洛赫球图像中表现为[布洛赫矢量](@entry_id:144181)的运动。

#### [幺正演化](@entry_id:145020)即旋转

一个闭合量子系统的演化由幺正算符 $U$ 描述，$\rho' = U\rho U^\dagger$。对于单[量子比特](@entry_id:137928)，任何[幺正演化](@entry_id:145020)都对应于布洛赫球的一次**旋转**。一个绕轴 $\hat{n}$ 旋转角度为 $\alpha$ 的操作可以表示为：
$$
U = R_{\hat{n}}(\alpha) = \exp(-i\frac{\alpha}{2}\hat{n}\cdot\vec{\sigma}) = \cos(\frac{\alpha}{2})I - i\sin(\frac{\alpha}{2})\hat{n}\cdot\vec{\sigma}
$$
注意，[布洛赫矢量](@entry_id:144181)的旋转角度 $\alpha$ 是[量子态](@entry_id:146142)相位因子 $\alpha/2$ 的两倍，这是$SU(2)$群与$SO(3)$群之间二对一映射关系的体现。

给定一个幺[正矩阵](@entry_id:149490) $U$，我们可以通过将其分解为上述标准形式来确定其等效的[旋转轴](@entry_id:187094) $\hat{n}$ 和旋转角 $\alpha$。一系列的量子门操作，例如相继施加一个绕 $z$ 轴的旋转 $R_z(\beta_1)$ 和一个绕 $x$ 轴的旋转 $R_x(\beta_2)$，其总效果 $U = R_x(\beta_2)R_z(\beta_1)$ 等效于另一次单一的旋转 $R_{\hat{n}}(\alpha)$ [@problem_id:170155]。通过展开并比较[泡利矩阵](@entry_id:139493)的系数，我们可以求解出新的[旋转轴](@entry_id:187094)和角度。例如，在这种情况下，等效旋转轴在 $xy$ 平面上的投影大小为 $\frac{|\sin(\beta_2/2)|}{\sqrt{1 - \cos^2(\beta_1/2)\cos^2(\beta_2/2)}}$。

这一性质是[量子计算](@entry_id:142712)的基础，任何单比特门都可以分解为绕两个不同轴的旋转。例如，我们可以计算一个初态为 $|0\rangle$ 的[量子比特](@entry_id:137928)在相继经过 $U_x = \exp(-i \frac{\pi}{3} \sigma_x)$ 和 $U_y = \exp(-i \frac{\pi}{6} \sigma_y)$ 两个门之后，末态与初态的保真度 [@problem_id:170021]。

旋转的[非对易性](@entry_id:153545)是量子力学的一个核心特征。两个[无穷小旋转](@entry_id:166635)的群对易子 $R_x(\delta)R_y(\epsilon)R_x(-\delta)R_y(-\epsilon)$，在最低阶近似下，等效于一个绕着 $z$ 轴的单一旋转，其旋转角正比于 $\delta\epsilon$ [@problem_id:170023]。这与生成元（泡利矩阵）的李代数关系 $[\sigma_x, \sigma_y] = 2i\sigma_z$ 直接相关。

#### 几何相位

当一个量子系统在[参数空间](@entry_id:178581)中经历一个闭合路径的[绝热演化](@entry_id:153352)后，除了获得一个与时间相关的动力学相位外，它还会获得一个仅依赖于路径几何形状的**几何相位**（geometric phase），或称**[贝里相位](@entry_id:159450)**（Berry phase）。

在布洛赫球上，一个沿着极角 $\theta_0$ 恒定的纬线（即 $\phi$ 从 $0$ 变到 $2\pi$）[绝热演化](@entry_id:153352)的[纯态](@entry_id:141688)，其获得的[几何相位](@entry_id:138449)为 $\gamma_g = -\pi(1 - \cos\theta_0)$ [@problem_id:170049]。这个结果恰好是路径在球心所张立体角 $\Omega = 2\pi(1 - \cos\theta_0)$ 的负一半（对于自旋-1/2系统）。

几何相位的概念也可以推广到非绝热的、由一系列离散幺正操作构成的循环演化。例如，一个本征态在经历一系列旋转后回到自身，其总相位 $\gamma_{total}$ 可以分解为动力学部分 $\gamma_d$ 和几何部分 $\gamma_g$ [@problem_id:170105]。通过计算总[演化算符](@entry_id:182628)的[本征值](@entry_id:154894)得到总相位，并根据演化路径[计算动力学](@entry_id:204520)相位，两者之差即为[几何相位](@entry_id:138449)。

### [开放量子系统](@entry_id:138632)：非[幺正演化](@entry_id:145020)

现实世界中的[量子比特](@entry_id:137928)总是与环境相互作用，导致其演化不再是纯粹的幺正旋转，而是一种更普适的[量子操作](@entry_id:145906)，称为**量子通道**（quantum channel）。这种演化通常会导致纯态变为混合态，这个过程称为**退相干**（decoherence）。在布洛赫球图像中，这种非[幺正演化](@entry_id:145020)表现为一种**[仿射变换](@entry_id:144885)**（affine transformation），即 $\vec{r}' = M\vec{r} + \vec{d}$，其中 $M$ 是一个 $3 \times 3$ 的实矩阵，$\vec{d}$ 是一个[位移矢量](@entry_id:262782)。这不仅包括旋转，还包括缩放和平移。

一个量子通道可以用**[算符和表示](@entry_id:140073)**（operator-sum representation）来描述，$\rho' = \mathcal{E}(\rho) = \sum_k E_k \rho E_k^\dagger$，其中 $E_k$ 是[克劳斯算符](@entry_id:144882)（Kraus operators）。

一个典型的例子是**[振幅阻尼](@entry_id:146861)通道**（amplitude damping channel），它模拟了[激发态](@entry_id:261453) $|1\rangle$ 到[基态](@entry_id:150928) $|0\rangle$ 的[能量弛豫](@entry_id:136820)过程。其[克劳斯算符](@entry_id:144882)为 $E_0 = \begin{pmatrix} 1  0 \\ 0  \sqrt{1-\gamma} \end{pmatrix}$ 和 $E_1 = \begin{pmatrix} 0  \sqrt{\gamma} \\ 0  0 \end{pmatrix}$，其中 $\gamma$ 是衰变概率。这个通道会将[布洛赫矢量](@entry_id:144181)作如下变换：
$$
r'_x = \sqrt{1-\gamma} \, r_x, \quad r'_y = \sqrt{1-\gamma} \, r_y, \quad r'_z = (1-\gamma) \, r_z + \gamma
$$
这个变换将整个布洛赫球压缩并移动，使其变成一个以 $(0,0,\gamma)$ 为中心，半轴为 $(\sqrt{1-\gamma}, \sqrt{1-\gamma}, 1-\gamma)$ 的**椭球** [@problem_id:170042]。这个椭球的体积为 $\frac{4\pi}{3}(1-\gamma)^2$，它直观地展示了状态空间是如何因与环境的相互作用而收缩的。对于一个初始的[纯态](@entry_id:141688)，经过这个通道后，其[布洛赫矢量](@entry_id:144181)的长度会缩短，态变为混合态 [@problem_id:170133]。

另一个重要的例子是**广义[相位阻尼](@entry_id:147888)通道**（generalized phase damping channel），它模拟了[相干性](@entry_id:268953)的损失。这个通道会保持[布洛赫矢量](@entry_id:144181)的 $z$ 分量不变，但会缩放其 $xy$ 平面上的分量，导致[布洛赫矢量](@entry_id:144181)向 $z$ 轴收缩 [@problem_id:170157]。

更一般地，任何满足Gorini-Kossakowski-Sudarshan-Lindblad (GKSL) 主方程的演化，$\frac{d\rho}{dt} = -i[H, \rho] + \sum_k ( L_k \rho L_k^\dagger - \frac{1}{2}\{L_k^\dagger L_k, \rho\} )$，都对应于[布洛赫矢量](@entry_id:144181)的一个[微分](@entry_id:158718)仿射变换 $\frac{d\vec{r}}{dt} = M\vec{r} + \vec{d}$。其中[哈密顿量](@entry_id:172864) $H$ 贡献了旋转部分，而林德布劳德算符（Lindblad operators）$L_k$ 同时贡献了旋转、缩放和平移 [@problem_id:170024]。

### 高级几何观点与多[量子比特](@entry_id:137928)连接

布洛赫球的几何图像可以被推广和深化，并与其他物理和数学领域建立联系。

#### 球极投影与[莫比乌斯变换](@entry_id:157570)

通过**球极投影**（stereographic projection），我们可以将[布洛赫球面](@entry_id:138823)（除去一个点）映射到整个复平面 $\mathbb{C}$。一个常用的约定是将态 $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$ 映射到复数 $z = \beta/\alpha$。在这种映射下，任何单[量子比特](@entry_id:137928)的幺正操作 $U$ 都对应于复平面上的一次**莫比乌斯变换**（Möbius transformation）：$z' = \frac{az+b}{cz+d}$。例如，[量子计算](@entry_id:142712)中至关重要的**阿达马门**（Hadamard gate）$H = \frac{1}{\sqrt{2}}\begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}$，其诱导的莫比乌斯变换为 $z' = \frac{1-z}{1+z}$ [@problem_id:170052]。这一联系为利用[复分析](@entry_id:167282)的强大工具来研究[量子操作](@entry_id:145906)提供了途径。

#### 马约拉纳恒星表示

对于具有 $N$ 个[量子比特](@entry_id:137928)的**对称[纯态](@entry_id:141688)**（等价于一个自旋为 $J=N/2$ 的粒子），**马约拉纳恒星表示**（Majorana stellar representation）将其几何地表示为[布洛赫球面](@entry_id:138823)上的 $N$ 个点（称为“恒星”）。这些恒星的位置由一个与该[量子态](@entry_id:146142)相关的马约拉纳多项式的根确定。这种表示法为高维对称[子空间](@entry_id:150286)中的纠缠提供了直观的几何图像。例如：
- 对于双比特[贝尔态](@entry_id:140749) $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$，它对应于一个自旋-1系统。其马约拉纳表示由两颗恒星构成，它们位于布洛赫球赤道的对跖点上，例如 $y$ 轴上的 $(0,1,0)$ 和 $(0,-1,0)$ [@problem_id:170035]。
- 对于三比特的 $|W\rangle$ 态，其恒星表示由三颗星构成：一颗在南极点，另两颗重合在北极点 [@problem_id:170091]。
恒星的[分布](@entry_id:182848)模式可以用来对不同类型的[多体纠缠](@entry_id:142544)进行分类。

#### 多[量子比特](@entry_id:137928)态的几何

描述一个一般的[多量子比特系统](@entry_id:142942)的状态空间几何极其复杂。但对于某些重要的[子集](@entry_id:261956)，我们仍能获得直观的几何图像。例如**贝尔对[角态](@entry_id:145477)**（Bell-diagonal states），它是一类双[量子比特](@entry_id:137928)态。其物理合法性（[密度矩阵](@entry_id:139892)的[半正定性](@entry_id:147720)）要求其关联张量的三个对角元 $(c_x, c_y, c_z)$ 必须位于一个由顶点 $(1,1,-1)$, $(1,-1,1)$, $(-1,1,1)$ 和 $(-1,-1,-1)$ 构成的**四面体**内部 [@problem_id:170132]。这个四面体为我们提供了一个高维[状态空间](@entry_id:177074)中特定[截面](@entry_id:154995)的具体形状。

最后，值得一提的是，单[量子比特](@entry_id:137928)的变换与[狭义相对论](@entry_id:275552)中的[洛伦兹群](@entry_id:139964)之间存在深刻的数学联系。$SU(2)$群（单比特[幺正门](@entry_id:152157)）与旋转群$SO(3)$的双重[覆盖关系](@entry_id:269334)，可以推广到$SL(2, \mathbb{C})$群（[洛伦兹群](@entry_id:139964)的[旋量表示](@entry_id:141362)）与[洛伦兹群](@entry_id:139964)$SO^+(1,3)$之间的关系。这允许一些物理的量子通道被描述为四维[闵可夫斯基时空](@entry_id:156421)中的洛伦兹变换作用于一个四维矢量 $(1, \vec{r})$ 的结果 [@problem_id:170061]。这种不寻常的联系揭示了量子信息几何与[时空几何](@entry_id:139497)之间潜在的深层统一。

本章通过布洛赫球这一核心工具，系统地阐述了单[量子比特](@entry_id:137928)的静态几何性质、动态演化规律及其与更广泛物理概念的联系，为后续学习[多量子比特系统](@entry_id:142942)和量子算法打下了坚实的基础。