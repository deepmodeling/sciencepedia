## 引言
[麦克斯韦方程组](@entry_id:150940)是经典电磁学的集大成者，它以无与伦比的优美与深刻统一了电、磁与光学现象。虽然其积分形式为我们提供了宏观尺度上场与源的整体关系，但要真正洞悉电磁世界在每一时空点上的内在运作机制，我们必须转向其更为强大和基础的微分形式。这些方程不仅揭示了[电荷](@entry_id:275494)与电流如何成为场的“源头”，更描绘了一幅变化的[电场](@entry_id:194326)与[磁场](@entry_id:153296)相互激发、在空间中传播的动态画卷。本文旨在为读者提供一个关于麦克斯韦方程组微分形式的全面而深入的理解。

本文将分为三个核心部分。在第一章“原理与机制”中，我们将逐一剖析四个基本方程的物理意义，并推导其重要的物理结论，如电荷守恒和[电磁波](@entry_id:269629)的存在。接着，在第二章“应用与[交叉](@entry_id:147634)学科联系”中，我们将展示这组方程如何被应用于解决[材料科学](@entry_id:152226)、等离子体物理、天文学乃至量子力学中的实际问题，彰显其强大的普适性。最后，在“动手实践”部分，读者将通过具体问题来巩固和应用所学知识。通过这一结构化的学习路径，读者将能深刻领会[麦克斯韦方程组](@entry_id:150940)作为现代物理学和工程学基石的精髓所在。

## 原理与机制

在之前的章节中，我们已经探讨了[麦克斯韦方程组的积分形式](@entry_id:264550)，它描述了[电磁场](@entry_id:265881)在宏观区域内与其中包含的总[电荷](@entry_id:275494)和总电流之间的关系。然而，为了更深入地理解[电磁场](@entry_id:265881)的局域行为——即在空间中每一点上场与源之间的瞬时关系——我们需要引入其微分形式。[微分形式](@entry_id:146747)的麦克斯韦方程组以一种极为凝练和深刻的方式，揭示了电磁现象的内在机制，从[电荷](@entry_id:275494)如何产生[电场](@entry_id:194326)，到变化的场如何相互激发并最终形成光的传播。本章将系统地阐述这四个基本方程的原理，并探讨由它们共同导出的几个基本物理推论。

### 逐条审视：四个基本方程

[麦克斯韦方程组的微分形式](@entry_id:204110)由四个耦合的[一阶偏微分方程](@entry_id:178306)组成，它们构成了经典电磁学的完整公理体系。

#### [高斯电场定律](@entry_id:146732)：[电场](@entry_id:194326)的源头

第一个方程是[高斯电场定律](@entry_id:146732)，其[微分形式](@entry_id:146747)为：
$$ \nabla \cdot \vec{E} = \frac{\rho}{\epsilon_0} $$
其中 $\nabla \cdot \vec{E}$ 是[电场](@entry_id:194326) $\vec{E}$ 的散度，$\rho$ 是该点的电荷密度，$\epsilon_0$ 是[真空介电常数](@entry_id:204253)。这个方程的物理意义非常直观：空间某一点的[电场散度](@entry_id:261010)正比于该点的[电荷密度](@entry_id:144672)。散度衡量了一个矢量场从某点“流出”或“汇入”的程度。因此，高斯定律告诉我们，**正[电荷](@entry_id:275494)是[电场线](@entry_id:277009)的“源头”，负[电荷](@entry_id:275494)是电场线的“汇点”**。在没有[电荷](@entry_id:275494)的地方（$\rho=0$），[电场散度](@entry_id:261010)为零，这意味着电场线既不开始也不结束，它们必须是连续的或者从无穷远处来、到无穷远处去。

为了具体理解这一点，我们可以考虑一个逆向问题：如果我们知道空间中的[电场](@entry_id:194326)[分布](@entry_id:182848)，我们能否反推出产生这个[电场](@entry_id:194326)的电荷分布？[@problem_id:569835] 假设在一个球对称介质中，[电场](@entry_id:194326)由 $\vec{E}(\vec{r}) = \frac{V_0}{r_0} e^{-(r/r_0)^2} \hat{r}$ 给出，其中 $r$ 是径向距离。通过计算该[电场的散度](@entry_id:272995)，我们就能直接得到[电荷密度](@entry_id:144672) $\rho(r)$。在[球坐标系](@entry_id:167517)下，对于一个仅有径向分量 $E_r(r)$ 的矢量场，其散度为 $\nabla \cdot \vec{E} = \frac{1}{r^2}\frac{d}{dr}(r^2 E_r)$。代入给定的 $E_r(r)$ 并求导，我们可以得到：
$$ \rho(r) = \epsilon_0 (\nabla \cdot \vec{E}) = \frac{2\epsilon_0 V_0}{r_0}\frac{1-(r^2/r_0^2)}{r}e^{-(r/r_0)^2} $$
这个结果表明，电荷密度不仅依赖于径向距离，而且在 $r=r_0$ 处符号会发生改变，这对应着一个复杂的、由正负[电荷](@entry_id:275494)层组成的球对称[分布](@entry_id:182848)。这个例子清晰地展示了[微分形式的高斯定律](@entry_id:267348)是如何建立起每一点的[电场](@entry_id:194326)结构与该点电荷密度之间的直接联系。

#### 高斯[磁场](@entry_id:153296)定律：磁单极子的缺席

第二个方程是高斯[磁场](@entry_id:153296)定律：
$$ \nabla \cdot \vec{B} = 0 $$
这个方程的形式异常简洁，但其物理内涵却极为深远。它断言了**[磁场的散度](@entry_id:273621)在任何地方都恒等于零**。这意味着[磁场](@entry_id:153296)是一个[无源场](@entry_id:178017)，不存在像[电荷](@entry_id:275494)那样的“磁荷”或“磁单极子”。[磁场](@entry_id:153296)线永远不会从某一点发出或终止于某一点；它们必须形成闭合的回路，或者从无穷远延伸到无穷远。

这条定律对可能存在的[磁场](@entry_id:153296)形态施加了非常强的限制。例如，一个物理爱好者可能会设想一种纯径向的[磁场](@entry_id:153296)，类似于点电荷产生的[电场](@entry_id:194326) [@problem_id:1807157]。假设在一个[圆柱坐标系](@entry_id:266798) $(s, \phi, z)$ 中，一个[磁场](@entry_id:153296)具有形式 $\vec{B} = f(s) \hat{s}$，即[磁场](@entry_id:153296)方向总是沿着径向向外，且大小仅与径向距离 $s$ 有关。为了使这个场成为一个物理上可能存在的[磁场](@entry_id:153296)，它必须满足 $\nabla \cdot \vec{B} = 0$。在[圆柱坐标系](@entry_id:266798)中，散度表达式为 $\nabla \cdot \vec{B} = \frac{1}{s}\frac{\partial}{\partial s}(s B_s)$。代入 $B_s = f(s)$，我们得到：
$$ \frac{1}{s}\frac{d}{ds}(s f(s)) = 0 $$
这意味着 $s f(s)$ 必须是一个常数，我们称之为 $C$。因此，$f(s) = C/s$。这表明，如果一个纯径向的[磁场](@entry_id:153296)要存在，其强度必须与距离成反比。然而，这样的场在 $s=0$ 处会发散，暗示着在中心轴上存在一个线状的磁单极子源。迄今为止，所有实验都未能证实磁单极子的存在，因此物理学家坚信 $\nabla \cdot \vec{B} = 0$ 是自然界的一条基本定律。

#### [法拉第感应定律](@entry_id:146175)：变化的[磁场](@entry_id:153296)产生[电场](@entry_id:194326)

第三个方程是[法拉第感应定律](@entry_id:146175)，它揭示了电场和磁场之间的动态联系：
$$ \nabla \times \vec{E} = - \frac{\partial \vec{B}}{\partial t} $$
这里的 $\nabla \times \vec{E}$ 是[电场的旋度](@entry_id:182875)，它衡量了场在一点周围的“卷曲”或“环绕”程度。这个方程表明，**变化的[磁场](@entry_id:153296)会在其周围空间中激发出涡旋状的[电场](@entry_id:194326)**。这种[电场](@entry_id:194326)与由静[电荷](@entry_id:275494)产生的无旋[电场](@entry_id:194326)（其旋度 $\nabla \times \vec{E} = 0$）有本质的不同。[感应电场](@entry_id:267314)的[电场线](@entry_id:277009)是闭合的，没有起点和终点。这正是发电机、变压器和电磁炉等设备的工作原理。

我们可以通过一个简单的例子来理解这个关系 [@problem_id:1610328]。考虑一个空间均匀但随时间正弦变化的[磁场](@entry_id:153296) $\vec{B}(t) = B_0 \cos(\omega t) \hat{z}$。根据[法拉第定律](@entry_id:149836)，这个变化的[磁场](@entry_id:153296)必然会感生出一个[电场](@entry_id:194326) $\vec{E}$。我们可能不知道 $\vec{E}$ 场的具体[空间分布](@entry_id:188271)，但我们可以确定它的旋度。直接对 $\vec{B}(t)$ 求时间偏导数：
$$ \frac{\partial \vec{B}}{\partial t} = -B_0 \omega \sin(\omega t) \hat{z} $$
代入法拉第定律，我们立刻得到[电场的旋度](@entry_id:182875)：
$$ \nabla \times \vec{E} = - \left(-B_0 \omega \sin(\omega t) \hat{z}\right) = B_0 \omega \sin(\omega t) \hat{z} $$
这个结果告诉我们，感应出的[电场](@entry_id:194326)在空间中是“卷曲”的，其卷曲的程度和方向（由旋度矢量描述）直接由[磁场](@entry_id:153296)的变化率决定。

#### [安培-麦克斯韦定律](@entry_id:266368)：电流和变化的[电场](@entry_id:194326)产生[磁场](@entry_id:153296)

第四个，也是最后一个方程是[安培-麦克斯韦定律](@entry_id:266368)：
$$ \nabla \times \vec{B} = \mu_0 \vec{J} + \mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t} $$
其中 $\mu_0$ 是[真空磁导率](@entry_id:186031)，$\vec{J}$ 是[电流密度](@entry_id:190690)。这个方程指出了**[磁场](@entry_id:153296)（的旋度）有两个来源：传导电流（$\vec{J}$ 项）和变化的[电场](@entry_id:194326)（$\frac{\partial \vec{E}}{\partial t}$ 项）**。前者是安培最初的发现，即电流周围会产生[磁场](@entry_id:153296)。后者是麦克斯韦的天才补充，被称为**位移电流**。

对于[稳恒电流](@entry_id:271551)的情况，[电场](@entry_id:194326)不随时间变化，$\frac{\partial \vec{E}}{\partial t} = 0$，方程简化为[安培定律](@entry_id:140092)的微分形式：$\nabla \times \vec{B} = \mu_0 \vec{J}$。这表明[稳恒电流](@entry_id:271551)会产生涡旋状的[磁场](@entry_id:153296)。例如，在一个半径为 $R$ 的长直导线中，若电流密度[分布](@entry_id:182848)为 $\vec{J}(s) = J_0 \frac{s}{R} \hat{z}$（即电流密度从中心向外线性增加），那么导线内部任意一点的[磁场](@entry_id:153296)旋度就直接由该点的电流密度决定 [@problem_id:1610332]：
$$ \nabla \times \vec{B} = \mu_0 \vec{J} = \mu_0 J_0 \frac{s}{R} \hat{z} $$

然而，麦克斯韦的位移电流项至关重要。它不仅解决了安培定律在处理含时问题（如[电容器充电](@entry_id:270179)）时的逻辑矛盾，更重要的是，它揭示了一种全新的对称性：变化的[磁场](@entry_id:153296)能产生[电场](@entry_id:194326)，同样，变化的[电场](@entry_id:194326)也能产生[磁场](@entry_id:153296)。正是这种相互激发、互为因果的机制，导致了[电磁波](@entry_id:269629)的存在。

### 麦克斯韦方程组的基本推论

单独看，每个方程都描述了[电磁场](@entry_id:265881)的一个侧面。然而，将它们作为一个整体联立求解时，会涌现出一系列深刻的物理结论。

#### [电荷守恒](@entry_id:264158)：一个必然的[逻辑推论](@entry_id:155068)

电荷守恒定律是物理学中最基本的定律之一，它通常用[连续性方程](@entry_id:195013)来表述：
$$ \frac{\partial \rho}{\partial t} + \nabla \cdot \vec{J} = 0 $$
这个方程表明，一个封闭体积内[电荷](@entry_id:275494)量的减少率（由 $\frac{\partial \rho}{\partial t}$ 体现）必须等于从该体积表面流出的净电流（由 $\nabla \cdot \vec{J}$ 体现）。在[麦克斯韦的理论](@entry_id:270081)框架中，[电荷守恒](@entry_id:264158)并非一个独立的假设，而是内蕴于[方程组](@entry_id:193238)之中的一个必然结果。

我们可以通过对方程进行简单的数学操作来证明这一点。从[安培-麦克斯韦定律](@entry_id:266368)出发：
$$ \nabla \times \vec{B} = \mu_0 \vec{J} + \mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t} $$
对上式两边取散度。根据矢量恒等式，任何[旋度的散度](@entry_id:271562)都为零，即 $\nabla \cdot (\nabla \times \vec{B}) = 0$。于是我们得到：
$$ 0 = \mu_0 (\nabla \cdot \vec{J}) + \mu_0 \epsilon_0 \nabla \cdot \left(\frac{\partial \vec{E}}{\partial t}\right) $$
交换时间和空间求导的顺序，并代入[高斯电场定律](@entry_id:146732) $\nabla \cdot \vec{E} = \rho/\epsilon_0$，上式变为：
$$ 0 = \mu_0 (\nabla \cdot \vec{J}) + \mu_0 \epsilon_0 \frac{\partial}{\partial t} \left(\frac{\rho}{\epsilon_0}\right) = \mu_0 \left(\nabla \cdot \vec{J} + \frac{\partial \rho}{\partial t}\right) $$
除去常数因子 $\mu_0$，我们就得到了连续性方程。这个推导有力地说明了[位移电流](@entry_id:190231)项 $\mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t}$ 的引入是确保理论自洽性的关键。

为了更深刻地体会这种逻辑上的紧密联系，我们可以做一个思想实验 [@problem_id:569985]。假设在一个假想的宇宙里，[安培-麦克斯韦定律](@entry_id:266368)被修改为 $\nabla \times \mathbf{B} = \mu_0 \mathbf{J} + \mu_0 \epsilon_0 \frac{\partial \mathbf{E}}{\partial t} + \alpha \mathbf{E}$，其中 $\alpha$ 是一个新的[物理常数](@entry_id:274598)。重复上述推导过程，我们会发现连续性方程被修改为：
$$ \frac{\partial \rho}{\partial t} + \nabla \cdot \mathbf{J} = - \frac{\alpha}{\mu_0 \epsilon_0} \rho $$
这表明在这个假想宇宙中，[电荷](@entry_id:275494)不再守恒！它可以凭空产生或消失，其产生/消失的速率正比于当地的电荷密度。这个思想实验反过来证明了，我们宇宙中精确的电荷守恒现象，是麦克斯韦方程组特定形式的直接数学后果。

#### [电磁波](@entry_id:269629)：场自身的传播

麦克斯韦理论最辉煌的成就，莫过于预言了[电磁波](@entry_id:269629)的存在，并揭示了光就是一种[电磁波](@entry_id:269629)。这个预言来自于在无源（$\rho=0, \vec{J}=0$）的真空中考察麦克斯韦方程组。

在真空中，四个方程简化为：
1. $\nabla \cdot \vec{E} = 0$
2. $\nabla \cdot \vec{B} = 0$
3. $\nabla \times \vec{E} = - \frac{\partial \vec{B}}{\partial t}$
4. $\nabla \times \vec{B} = \mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t}$

我们可以通过消去 $\vec{B}$ 场来得到一个只关于 $\vec{E}$ 场的方程 [@problem_id:1807154]。对法拉第定律（方程3）两边取旋度：
$$ \nabla \times (\nabla \times \vec{E}) = - \nabla \times \left(\frac{\partial \vec{B}}{\partial t}\right) = - \frac{\partial}{\partial t}(\nabla \times \vec{B}) $$
利用矢量恒等式 $\nabla \times (\nabla \times \vec{A}) = \nabla(\nabla \cdot \vec{A}) - \nabla^2 \vec{A}$，并代入方程1（$\nabla \cdot \vec{E} = 0$），上式左边简化为 $-\nabla^2 \vec{E}$。将方程4代入上式右边，我们得到：
$$ -\nabla^2 \vec{E} = - \frac{\partial}{\partial t} \left(\mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t}\right) = - \mu_0 \epsilon_0 \frac{\partial^2 \vec{E}}{\partial t^2} $$
整理后得到：
$$ \nabla^2 \vec{E} - \mu_0 \epsilon_0 \frac{\partial^2 \vec{E}}{\partial t^2} = \vec{0} $$
这是一个标准的波动方程。它描述了一个矢量场 $\vec{E}$ 在空间中的传播，其传播速度 $v$ 由系数决定，即 $v^2 = 1/(\mu_0 \epsilon_0)$。将当时已知的[真空介电常数](@entry_id:204253) $\epsilon_0$ 和[磁导率](@entry_id:154559) $\mu_0$ 的实验值代入计算，得到的速度值与当时测得的光速惊人地一致。这雄辩地证明了光是一种电磁现象——变化的电场和磁场在空间中相互激发、不断再生，从而形成以光速传播的[电磁波](@entry_id:269629)。

#### [电磁能](@entry_id:264720)量与坡印亭定理

[电磁场](@entry_id:265881)不仅传递信息，也携带能量。单位体积内[电磁场](@entry_id:265881)的能量密度 $u_{em}$ 为：
$$ u_{em} = \frac{1}{2}(\vec{E} \cdot \vec{D} + \vec{B} \cdot \vec{H}) = \frac{1}{2}\left(\epsilon E^2 + \frac{1}{\mu}B^2\right) $$
（在真空中 $\epsilon = \epsilon_0, \mu = \mu_0$）

能量是守恒的。对于[电磁场](@entry_id:265881)，其[能量守恒](@entry_id:140514)定律的[微分形式](@entry_id:146747)被称为**坡印亭定理**：
$$ \frac{\partial u_{em}}{\partial t} + \nabla \cdot \vec{S} = -\vec{J} \cdot \vec{E} $$
其中，$\vec{S} = \vec{E} \times \vec{H}$ (或在真空中 $\vec{S} = \frac{1}{\mu_0}\vec{E} \times \vec{B}$) 被称为**坡印亭矢量**，代表单位时间通过单位面积的[能量流](@entry_id:142770)密度，即能流密度矢量。$\vec{J} \cdot \vec{E}$ 项代表[电场](@entry_id:194326)对[电荷](@entry_id:275494)做功的[功率密度](@entry_id:194407)。该定理表明，空间某点[电磁场能量](@entry_id:265463)密度的增加率，等于流入该点的净能量流，减去场对[电荷](@entry_id:275494)做功而消耗的能量。

我们可以从麦克斯韦的旋度方程出发，推导出坡印亭定理的一部分。考虑无源的线性介质区域（$\vec{J}_f=0$），能量密度的变化率是 [@problem_id:611907]：
$$ \frac{\partial u_{em}}{\partial t} = \epsilon \vec{E} \cdot \frac{\partial \vec{E}}{\partial t} + \frac{1}{\mu} \vec{B} \cdot \frac{\partial \vec{B}}{\partial t} $$
利用无源区的旋度方程 $\nabla \times \vec{H} = \epsilon \frac{\partial \vec{E}}{\partial t}$ 和 $\nabla \times \vec{E} = -\mu \frac{\partial \vec{H}}{\partial t}$ 来替换时间导数项，并注意到 $\vec{B} = \mu\vec{H}$，可得：
$$ \frac{\partial u_{em}}{\partial t} = \vec{E} \cdot (\nabla \times \vec{H}) - \vec{H} \cdot (\nabla \times \vec{E}) $$
这个表达式恰好与坡印亭矢量散度的负值 $-\nabla \cdot \vec{S}$ 相等，这可以通过矢量恒等式 $\nabla \cdot (\vec{E} \times \vec{H}) = \vec{H} \cdot (\nabla \times \vec{E}) - \vec{E} \cdot (\nabla \times \vec{H})$ 得到验证。因此，我们导出了无源区的[能量守恒](@entry_id:140514)定律 $\frac{\partial u_{em}}{\partial t} + \nabla \cdot \vec{S} = 0$。

这个[能量守恒](@entry_id:140514)关系是麦克斯韦理论具有强大预测能力的基石之一，它直接导向了[电磁场](@entry_id:265881)解的**[唯一性定理](@entry_id:166861)**。考虑两个不同的解 $(\vec{E}_1, \vec{B}_1)$ 和 $(\vec{E}_2, \vec{B}_2)$ 对应于相同的源 $(\rho, \vec{J})$ 和边界条件。它们的差值场 $(\delta\vec{E}, \delta\vec{B})$ 将满足无源的[麦克斯韦方程组](@entry_id:150940)。我们可以为这个差值场定义一个能量密度 $u_\delta$ 和坡印亭矢量 $\delta\vec{S}$，并遵循完全相同的步骤推导出差值场的[能量守恒](@entry_id:140514)定律 [@problem_id:569926]：
$$ \nabla \cdot \delta\vec{S} = -\frac{\partial u_\delta}{\partial t} $$
将此式在一个体积 $V$ [内积](@entry_id:158127)分，并使用[散度定理](@entry_id:143110)，可以证明：如果在初始时刻 $t=0$ 差值场为零（即初始条件相同），并且在边界上满足特定条件（例如，在无穷远处场为零），那么在所有后续时刻，体积内的总差值场能量都必须为零。由于 $u_\delta$ 是非负的，这必然要求差值场 $\delta\vec{E}$ 和 $\delta\vec{B}$ 处处为零。这意味着 $\vec{E}_1 = \vec{E}_2$ 且 $\vec{B}_1 = \vec{B}_2$，即解是唯一的。

#### [电磁势](@entry_id:266145)：更深层次的描述

我们已经看到，两个麦克斯韦方程不涉及源，被称为[齐次方程](@entry_id:163650)：$\nabla \cdot \vec{B} = 0$ 和 $\nabla \times \vec{E} = -\frac{\partial \vec{B}}{\partial t}$。这些方程的结构保证了我们可以引入一组更基本的[辅助场](@entry_id:155519)——**标量势 $\phi$ 和矢量势 $\vec{A}$**——来描述[电磁场](@entry_id:265881)。

$\nabla \cdot \vec{B} = 0$ 表明[磁场](@entry_id:153296)是[无散场](@entry_id:260932)。根据矢量分析，任何[无散场](@entry_id:260932)都可以表示为另一个[矢量场的旋度](@entry_id:146155)。因此，我们可以定义矢量势 $\vec{A}$，使得：
$$ \vec{B} = \nabla \times \vec{A} $$
这样，高斯[磁场](@entry_id:153296)定律就自动满足了。

将上式代入法拉第定律，得到 $\nabla \times \vec{E} = -\frac{\partial}{\partial t}(\nabla \times \vec{A})$，移项得：
$$ \nabla \times \left(\vec{E} + \frac{\partial \vec{A}}{\partial t}\right) = 0 $$
这个结果表明，矢量场 $\vec{E} + \frac{\partial \vec{A}}{\partial t}$ 是一个[无旋场](@entry_id:183486)。任何[无旋场](@entry_id:183486)都可以表示为某个标量函数的梯度。因此，我们可以定义标量势 $\phi$，使得：
$$ \vec{E} + \frac{\partial \vec{A}}{\partial t} = -\nabla \phi $$
由此，我们得到[电场](@entry_id:194326) $\vec{E}$ 的表达式：
$$ \vec{E} = -\nabla \phi - \frac{\partial \vec{A}}{\partial t} $$

用势 $\phi$ 和 $\vec{A}$ 来表示场 $\vec{E}$ 和 $\vec{B}$，两个齐次麦克斯韦方程就得到了自动满足。[电磁场](@entry_id:265881)的动力学行为现在完全由关于势的方程（通过将势的表达式代入两个非齐次麦克斯韦方程得到）来描述。虽然势的引入似乎增加了复杂性，但它在高等电动力学和[量子场论](@entry_id:138177)中被证明是更为基本和方便的描述方式。我们可以通过一个具体的场来练习求解[势函数](@entry_id:176105)，例如，对于一组给定的正交驻波场，可以在特定的[规范条件](@entry_id:749730)下（如[库仑规范](@entry_id:273044) $\nabla \cdot \vec{A} = 0$ 且 $\phi = 0$）反解出其对应的矢量势 $\vec{A}$ [@problem_id:569914]。

### 一个统一的框架

本章详细阐述了微分形式的[麦克斯韦方程组](@entry_id:150940)及其重要推论。这些方程并非孤立的规则集合，而是一个逻辑上高度自洽、相互关联的统一体系。通过一个综合性的“逆向问题”，我们可以最直观地体会到这个体系的协同工作机制 [@problem_id:1807148]。

假设在真空中给定了一个特定的、随时间变化的[电场](@entry_id:194326)，例如 $\vec{E}(\vec{r}, t) = \alpha r^{3} t^{2} \hat{\phi}$（在[圆柱坐标系](@entry_id:266798)下）。我们的任务是找出必须存在什么样的[电荷密度](@entry_id:144672) $\rho$ 和电流密度 $\vec{J}$ 才能产生这样的场。解决这个问题需要我们系统地、按部就班地运用整个[麦克斯韦方程组](@entry_id:150940)：

1.  **应用[高斯电场定律](@entry_id:146732)**：计算给定 $\vec{E}$ 场的散度 $\nabla \cdot \vec{E}$。在本例中，$\nabla \cdot \vec{E} = 0$，因此我们立刻得知 $\rho = \epsilon_0 (\nabla \cdot \vec{E}) = 0$。产生该[电场](@entry_id:194326)的源不包含净[电荷](@entry_id:275494)。

2.  **应用法拉第定律**：计算 $\vec{E}$ 场的旋度 $\nabla \times \vec{E}$。根据法拉第定律 $\nabla \times \vec{E} = - \frac{\partial \vec{B}}{\partial t}$，这给了我们[磁场](@entry_id:153296)的变化率。对[时间积分](@entry_id:267413)，就可以求出[磁场](@entry_id:153296) $\vec{B}(\vec{r}, t)$（在确定积分常数后）。

3.  **应用[安培-麦克斯韦定律](@entry_id:266368)**：我们现在同时知道了 $\vec{E}$ 场和 $\vec{B}$ 场。我们可以计算 $\vec{B}$ 的旋度 $\nabla \times \vec{B}$ 和 $\vec{E}$ 的时间导数 $\frac{\partial \vec{E}}{\partial t}$。然后，利用[安培-麦克斯韦定律](@entry_id:266368)的完整形式 $\vec{J} = \frac{1}{\mu_0}\nabla \times \vec{B} - \epsilon_0 \frac{\partial \vec{E}}{\partial t}$，便可求解出最终的电流密度 $\vec{J}$。

这个过程完美地展示了[麦克斯韦方程组](@entry_id:150940)作为一个整体如何运作：从一个场的时空[分布](@entry_id:182848)出发，我们可以唯一地确定其他场以及产生这些场的源[分布](@entry_id:182848)。这正是这组方程强大预测能力的体现，它为所有宏观电磁现象提供了坚实而优美的理论基础。