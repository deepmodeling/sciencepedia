## 引言
在量子世界中，任何一个现实的系统都不可避免地与周围环境发生相互作用，成为一个“[开放量子系统](@entry_id:138632)”。完整地描述这类系统的演化通常需要借助[密度矩阵](@entry_id:139892)和主方程，但这不仅在计算上代价高昂，而且掩盖了单个量子实体在连续观测下所经历的丰富而随机的动力学过程。我们如何才能既精确模拟系统，又获得关于其个体行为的直观物理图像呢？

本文深入探讨了解决这一挑战的强大工具：[波函数](@entry_id:147440)[蒙特卡洛](@entry_id:144354)（WFMC）方法，也称[量子跃迁方法](@entry_id:141708)。这一理论框架将确定性的[主方程](@entry_id:142959)演化巧妙地“展开”为大量随机的[量子轨迹](@entry_id:180347)，每一条轨迹都对应着一个被连续监测的单个量子系统的可能演化历史。通过学习本文，你将掌握[开放量子系统](@entry_id:138632)模拟的一种核心[范式](@entry_id:161181)。

文章的结构将引导你逐步深入这一领域。我们首先在“原则与机制”一章中，揭示该方法背后的数学形式和物理内涵，解释系统如何在非厄米[哈密顿量](@entry_id:172864)下连续演化，又如何被瞬时的量子跃迁所打断。接着，在“应用与跨学科连接”一章中，我们将展示这一方法如何被应用于分析[光子统计](@entry_id:175965)、实现测量诱导纠缠、理解量子相变，并与[量子热力学](@entry_id:140152)等前沿领域建立联系。最后，通过“动手实践”部分提供的练习，你将有机会亲自应用这些概念，巩固所学知识。

## 原则与机制

在“引言”部分，我们已经了解到，[开放量子系统](@entry_id:138632)的完整描述需要使用密度矩阵 $\rho(t)$，其演化遵循一个主方程。然而，对于数值模拟而言，直接求解[主方程](@entry_id:142959)的计算成本会随着系统维度的增加而急剧上升。此外，[密度矩阵](@entry_id:139892)描述的是一个系综的平均行为，它掩盖了单个量子系统在连续测量下可能展现出的丰富动力学过程。[波函数](@entry_id:147440)[蒙特卡洛](@entry_id:144354)（Wave Function Monte Carlo, WFMC）方法，也称为[量子跃迁方法](@entry_id:141708)，提供了一种强大的替代方案。它将[主方程](@entry_id:142959)的确定性演化“展开”为大量纯[量子态](@entry_id:146142) $|\psi(t)\rangle$ 的[随机轨迹](@entry_id:755474)的集合，而这些轨迹的系综平均则精确地复现了[密度矩阵的演化](@entry_id:185083)。本章将深入探讨这一方法背后的核心原则与关键机制。

### [量子轨迹](@entry_id:180347)的形式化

[量子轨迹](@entry_id:180347)方法的基础，是将描述[密度算符](@entry_id:138151)在一个无穷小时间步 $dt$ 内演化的林德布拉德（Lindblad）主方程，重新表述为一组由[克劳斯算符](@entry_id:144882)（Kraus operators）定义的[量子操作](@entry_id:145906)。

#### 主方程的展开

一个典型的马尔可夫[开放量子系统](@entry_id:138632)的动力学由戈里尼-科萨科夫斯基-苏达尔尚-林德布拉德（Gorini–Kossakowski–Sudarshan–Lindblad, GKSL）主方程描述 [@problem_id:2822564]：
$$
\frac{d\rho(t)}{dt} = -\frac{i}{\hbar}[H(t), \rho(t)] + \sum_k \left( L_k \rho(t) L_k^\dagger - \frac{1}{2}\{L_k^\dagger L_k, \rho(t)\} \right)
$$
其中 $H(t)$ 是系统的厄米[哈密顿量](@entry_id:172864)，描述了相干演化；$L_k$ 是所谓的“跃迁算符”或“林德布拉德算符”，描述了[系统与环境](@entry_id:142270)之间的不可逆相互作用，例如[光子](@entry_id:145192)发射或[退相干](@entry_id:145157)。花括号 $\{\cdot, \cdot\}$ 代表[反对易子](@entry_id:139754)。

为了将此方程展开为[随机轨迹](@entry_id:755474)，我们考虑在一个小的时间步 $\delta t$ 内的演化。此[演化过程](@entry_id:175749)可以表示为一个完全正定保迹（Completely Positive and Trace-Preserving, CPTP）映射。该映射可以分解为一组[克劳斯算符](@entry_id:144882) $\{K_\alpha\}$ 的和：
$$
\rho(t+\delta t) = \sum_\alpha K_\alpha \rho(t) K_\alpha^\dagger
$$
保迹条件要求 $\sum_\alpha K_\alpha^\dagger K_\alpha = \mathbb{I}$，其中 $\mathbb{I}$ 是单位算符。在[量子跃迁](@entry_id:145857)的图像中，我们将这些[克劳斯算符](@entry_id:144882)分为两类：一个描述“无跃迁”事件的算符 $K_0$，以及一系列描述不同类型“量子跃迁”事件的算符 $\{K_k\}$（其中 $k \ge 1$）。

#### 无跃迁演化与非厄米[哈密顿量](@entry_id:172864)

“无跃迁”事件对应于在时间间隔 $\delta t$ 内，我们没有探测到任何由环境引起的突变（如[光子](@entry_id:145192)发射）。该过程的[克劳斯算符](@entry_id:144882)取为：
$$
K_0 = \mathbb{I} - \frac{i}{\hbar}H_{\mathrm{eff}} \delta t
$$
其中 $H_{\mathrm{eff}}$ 是一个尚未确定的[有效哈密顿量](@entry_id:748813)。而对于第 $k$ 种跃迁，其发生的概率在 $\delta t$ 内应为一阶小量，因此其[克劳斯算符](@entry_id:144882)可以设为：
$$
K_k = \sqrt{\delta t} L_k
$$
现在，我们可以利用保迹条件 $\sum_k K_k^\dagger K_k = \mathbb{I}$ 来确定 $H_{\mathrm{eff}}$ 的形式。将上述算符代入并保留至 $\delta t$ 的一阶项：
$$
(\mathbb{I} + \frac{i}{\hbar} H_{\mathrm{eff}}^\dagger \delta t)(\mathbb{I} - \frac{i}{\hbar} H_{\mathrm{eff}} \delta t) + \sum_k (\sqrt{\delta t} L_k^\dagger)(\sqrt{\delta t} L_k) = \mathbb{I}
$$
展开后得到：
$$
\mathbb{I} - \frac{i}{\hbar}(H_{\mathrm{eff}} - H_{\mathrm{eff}}^\dagger)\delta t + \sum_k L_k^\dagger L_k \delta t + \mathcal{O}(\delta t^2) = \mathbb{I}
$$
为了使此式成立，$\delta t$ 的一阶项必须为零，这意味着：
$$
H_{\mathrm{eff}} - H_{\mathrm{eff}}^\dagger = -i\hbar \sum_k L_k^\dagger L_k
$$
这个关系揭示了 $H_{\mathrm{eff}}$ 必须是一个**非厄米[哈密顿量](@entry_id:172864)**。其厄米部分就是系统的[哈密顿量](@entry_id:172864) $H$，而非厄米部分则由跃迁算符决定。标准的有效哈密顿量形式为 [@problem_id:2822564]：
$$
H_{\mathrm{eff}} = H - \frac{i\hbar}{2} \sum_k L_k^\dagger L_k
$$
这个非厄米项的物理意义至关重要。它导致了在无跃迁演化过程中，[量子态](@entry_id:146142)的模长（norm）不再守恒。考虑一个[纯态](@entry_id:141688) $|\psi(t)\rangle$ 在 $H_{\mathrm{eff}}$ 下的演化，其模长的变化率为：
$$
\frac{d}{dt}\langle\psi|\psi\rangle = \frac{1}{i\hbar}\langle\psi|(H_{\mathrm{eff}}^\dagger - H_{\mathrm{eff}})|\psi\rangle = -\sum_k \langle\psi|L_k^\dagger L_k|\psi\rangle \le 0
$$
这表明，只要系统不发生跃迁，其态矢量的模长就会持续衰减。衰减的速率恰好等于所有可能的跃迁事件的总发生率。

#### [量子跃迁](@entry_id:145857)与态投影

当一个量子跃迁确实发生时，它会将系统投影到一个新的状态。在时间间隔 $\delta t$ 内，发生第 $k$ 种跃迁的概率为：
$$
\delta p_k = \langle\psi(t)| K_k^\dagger K_k |\psi(t)\rangle = \delta t \langle\psi(t)| L_k^\dagger L_k |\psi(t)\rangle
$$
相应地，在 $\delta t$ 内不发生任何跃迁的概率为 $\delta p_{\text{no jump}} = 1 - \sum_k \delta p_k$。

让我们考虑一个简单的例子：一个处于[激发态](@entry_id:261453) $|e\rangle$ 的二能级原子，它能以速率 $\Gamma$ [自发辐射](@entry_id:140032)一个[光子](@entry_id:145192)到[基态](@entry_id:150928) $|g\rangle$。这个过程只有一个跃迁算符 $L = \sqrt{\Gamma}|g\rangle\langle e| = \sqrt{\Gamma}\sigma_-$。那么 $H_{\mathrm{eff}} = -\frac{i\hbar}{2} L^\dagger L = -\frac{i\hbar\Gamma}{2}|e\rangle\langle e|$（此处我们忽略了原子的自由[哈密顿量](@entry_id:172864)，因为它只贡献一个[全局相位](@entry_id:147947)）。初始状态为 $|\psi(0)\rangle = |e\rangle$。在无穷小时间 $\delta t$ 内，无跃迁演化后的（未归一化）态为：
$$
|\tilde{\psi}(\delta t)\rangle = \left(\mathbb{I} - \frac{i}{\hbar}H_{\mathrm{eff}}\delta t\right)|\psi(0)\rangle = \left(1 - \frac{\Gamma\delta t}{2}\right)|e\rangle
$$
这个未归一化态的模方为 $\langle\tilde{\psi}(\delta t)|\tilde{\psi}(\delta t)\rangle = (1 - \frac{\Gamma\delta t}{2})^2 \approx 1 - \Gamma\delta t$。这正是我们期望的无跃迁概率 [@problem_id:2113465]。这个结果阐明了一个核心概念：**在无跃迁演化下，态模方的衰减正好对应于跃迁事件尚未发生的概率。**

如果一个跃迁（例如，探测到一个[光子](@entry_id:145192)）被确定发生了，系统状态会经历一个瞬时的、随机的“跳变”。旧的状态 $|\psi(t)\rangle$ 会被投影到新的（归一化）状态 $|\psi'(t)\rangle$：
$$
|\psi(t)\rangle \rightarrow |\psi'(t)\rangle = \frac{L_k |\psi(t)\rangle}{\| L_k |\psi(t)\rangle \|}
$$
这个过程是[量子测量](@entry_id:272490)理论中投影假设的直接体现。正是这些随机的、离散的[量子跃迁](@entry_id:145857)，与连续的、确定性的非厄米演化相结合，构成了单个[量子轨迹](@entry_id:180347)的完整图像 [@problem_id:2822564]。

### 模拟算法及其物理解释

基于上述形式化理论，我们可以构建一个具体的蒙特卡洛模拟算法，并探讨其轨迹所蕴含的物理意义。

#### [蒙特卡洛算法](@entry_id:269744)步骤

模拟一个量子系统随[时间演化](@entry_id:153943)的单条轨迹，通常遵循以下步骤：

1.  **初始化**：在 $t=0$ 时，选择一个初始[纯态](@entry_id:141688) $|\psi(0)\rangle$。
2.  **无跃迁演化**：将当前态 $|\psi(t)\rangle$ 在非厄米[哈密顿量](@entry_id:172864) $H_{\mathrm{eff}}$ 下演化一个微小的时间步 $\delta t$，得到未归一化的末态 $|\tilde{\psi}(t+\delta t)\rangle = \exp(-iH_{\mathrm{eff}}\delta t/\hbar)|\psi(t)\rangle$。为简化计算，通常使用一阶近似：$|\tilde{\psi}(t+\delta t)\rangle \approx (\mathbb{I} - iH_{\mathrm{eff}}\delta t/\hbar)|\psi(t)\rangle$。
3.  **计算跃迁概率**：计算总的跃迁概率 $\delta p = \sum_k \delta p_k = \sum_k \delta t \langle\psi(t)| L_k^\dagger L_k |\psi(t)\rangle = 1 - \langle\tilde{\psi}(t+\delta t)|\tilde{\psi}(t+\delta t)\rangle$。
4.  **随机决策**：生成一个在 $[0, 1)$ 区间内[均匀分布](@entry_id:194597)的随机数 $\epsilon$。
5.  **执行或不执行跃迁**：
    *   如果 $\epsilon  \delta p$，则发生了一次跃迁。需要进一步确定是哪一种跃迁（如果存在多个跃迁通道），然后根据相应的跃迁算符 $L_k$ 更新系统状态：$|\psi(t+\delta t)\rangle = L_k |\psi(t)\rangle / \| L_k |\psi(t)\rangle \|$。
    *   如果 $\epsilon \ge \delta p$，则没有跃迁发生。系统状态被简单地归一化：$|\psi(t+\delta t)\rangle = |\tilde{\psi}(t+\delta t)\rangle / \sqrt{\langle\tilde{\psi}(t+\delta t)|\tilde{\psi}(t+\delta t)\rangle}$。
6.  **迭代**：将时间推进到 $t+\delta t$，并重复步骤2至5。

通过重复此过程，我们就能生成一条代表单个量子系统随机演化历史的**[量子轨迹](@entry_id:180347)**。

#### 条件动力学与无跃迁轨迹

每一条[量子轨迹](@entry_id:180347)都代表了一种**条件动力学**（conditional dynamics），即系统在给定了特定测量记录（例如，在某个时间段内探测到/未探测到[光子](@entry_id:145192)）的条件下所遵循的演化路径。

例如，考虑一个初始处于[基态](@entry_id:150928) $|g\rangle$ 的二能级原子，被一个共振[激光](@entry_id:194225)场驱动（[拉比频率](@entry_id:154019)为 $\Omega$），同时存在[自发辐射](@entry_id:140032)（速率为 $\gamma$）。如果我们持续监测但始终没有探测到任何出射[光子](@entry_id:145192)，那么系统的演化就完全由非厄米[哈密顿量](@entry_id:172864) $H_{\mathrm{eff}} = \frac{\hbar\Omega}{2}\sigma_x - \frac{i\hbar\gamma}{2}|e\rangle\langle e|$ 决定。在这种“无跃迁”的条件下，系统的[布洛赫矢量](@entry_id:144181)（Bloch vector）会遵循一条特定的轨迹，最终趋向于[基态](@entry_id:150928) $|g\rangle$ [@problem_id:769886]。这与无条件演化（由[主方程](@entry_id:142959)描述）下系统会趋向一个混合[稳态](@entry_id:182458)形成鲜明对比。这揭示了观测本身如何影响我们对系统状态的认知。

对于一个初始处于任意混合态 $\rho(0)$ 的系统，我们也可以计算在一段时间 $t$ 内始终没有发生跃迁的概率。这个概率由下式给出：
$$
P_{\text{no-jump}}(t) = \mathrm{Tr}[K(t)\rho(0)K^\dagger(t)]
$$
其中 $K(t) = \exp(-iH_{\mathrm{eff}}t/\hbar)$ 是有限时间的无跃迁[演化算符](@entry_id:182628)。对于一个经历[自发辐射](@entry_id:140032)的二能级原子，其跃迁算符为 $L=\sqrt{\gamma}\sigma_-$，[有效哈密顿量](@entry_id:748813)为 $H_{\mathrm{eff}} = H_0 - \frac{i\hbar\gamma}{2}|e\rangle\langle e|$。可以计算出，无跃迁概率为 $P_{\text{no-jump}}(t) = \rho_{gg}(0) + \rho_{ee}(0)e^{-\gamma t}$ [@problem_id:769847]。这个结果非常直观：初始处于[基态](@entry_id:150928)的部分 $\rho_{gg}(0)$ 永远不会发生跃迁，因此它对无跃迁概率的贡献是常数；而初始处于[激发态](@entry_id:261453)的部分 $\rho_{ee}(0)$ 则会以指数形式衰减，其存活到时间 $t$ 的概率就是 $e^{-\gamma t}$。

#### [等待时间分布](@entry_id:262786)

无跃迁概率 $P_{\text{no-jump}}(t)$ 与一个重要的物理可观测量——**[等待时间分布](@entry_id:262786)** $w(t)$ 密切相关。$w(t)$ 定义为第一次跃迁（例如，第一次[光子](@entry_id:145192)发射）恰好发生在时间 $t$ 的[概率密度](@entry_id:175496)。它等于无跃迁概率的衰减率：
$$
w(t) = -\frac{d}{dt}P_{\text{no-jump}}(t)
$$
这也可以被证明等价于在时间 $t$ 的总跃迁率，由未归一化的[波函数](@entry_id:147440)计算得出：$w(t) = \sum_k \langle\psi_{\text{un}}(t)|L_k^\dagger L_k|\psi_{\text{un}}(t)\rangle$，其中 $|\psi_{\text{un}}(t)\rangle$ 是由初始态在 $H_{\mathrm{eff}}$ 下演化得到的未归一化[波函数](@entry_id:147440)。

对于一个从[基态](@entry_id:150928)开始、被共振[激光](@entry_id:194225)驱动的二能级原子（[拉比频率](@entry_id:154019) $\Omega$，衰减率 $\gamma$），我们可以通过求解[含时薛定谔方程](@entry_id:137898)得到[激发态](@entry_id:261453)布居数 $|c_e(t)|^2$ 在无跃迁条件下的演化。然后，[等待时间分布](@entry_id:262786)就是 $w(t) = \gamma |c_e(t)|^2$。计算结果显示，这个[分布](@entry_id:182848)并非简单的指数衰减，而是在短时间内呈现[振荡](@entry_id:267781)行为，反映了[拉比振荡](@entry_id:137940)与衰减之间的竞争 [@problem_id:769960]。这种[振荡](@entry_id:267781)被称为[量子芝诺效应](@entry_id:141919)的体现，即频繁的“观测”（此处体现为无跃迁的条件）会抑制系统向[激发态](@entry_id:261453)的跃迁。

### 恢复系综动力学与进阶主题

尽管单条轨迹是随机的，但通过对大量独立生成的轨迹进行系综平均，我们可以精确地恢复由[主方程](@entry_id:142959)描述的确定性、无条件的系综动力学。

#### 从轨迹到[主方程](@entry_id:142959)

让我们来验证这一点。考虑在时间 $t$ 处于[纯态](@entry_id:141688) $|\psi(t)\rangle$ 的系综，其[密度矩阵](@entry_id:139892)为 $\rho(t) = |\psi(t)\rangle\langle\psi(t)|$。在时间 $t+\delta t$，新的系综平均密度矩阵 $\rho(t+\delta t)$ 是所有可能结果的加权平均：即无跃迁情况和各种跃迁情况的贡献之和。
$$
\rho(t+\delta t) \approx (1 - \sum_k \delta p_k) \frac{|\tilde{\psi}\rangle\langle\tilde{\psi}|}{\langle\tilde{\psi}|\tilde{\psi}\rangle} + \sum_k \delta p_k \frac{L_k|\psi\rangle\langle\psi|L_k^\dagger}{\|L_k|\psi\rangle\|^2}
$$
其中 $|\tilde{\psi}\rangle = (\mathbb{I} - iH_{\mathrm{eff}}\delta t/\hbar)|\psi\rangle$。将各项展开至 $\delta t$ 的一阶，经过一番代数运算，我们发现上式可以简化为：
$$
\rho(t+\delta t) \approx \rho(t) + \delta t \left( -\frac{i}{\hbar}[H, \rho(t)] + \sum_k \left( L_k \rho(t) L_k^\dagger - \frac{1}{2}\{L_k^\dagger L_k, \rho(t)\} \right) \right)
$$
这恰好是[林德布拉德主方程](@entry_id:146324)的积分形式。这证明了[量子轨迹](@entry_id:180347)方法的[自洽性](@entry_id:160889)：系综平均忠实地复现了主方程的动力学。因此，我们可以通过计算系综平均来得到诸如[稳态](@entry_id:182458)布居数之类的物理量 [@problem_id:769993] [@problem_id:769915]。例如，对于一个受共振驱动、同时存在自发辐射（速率 $\Gamma$）和非相干泵浦（速率 $W$）的[二能级系统](@entry_id:138452)，通过求解[稳态](@entry_id:182458)下的[布洛赫方程](@entry_id:153789)（该方程可由主方程导出），可以得到其[稳态](@entry_id:182458)[激发态](@entry_id:261453)布居数为 $\rho_{ee}^{ss} = \frac{\Omega^2 + W\Gamma + W^2}{2\Omega^2 + (\Gamma+W)^2}$ [@problem_id:769915]。

#### 缀饰态、[本征值](@entry_id:154894)与[奇异点](@entry_id:199525)

非厄米有效哈密顿量 $H_{\mathrm{eff}}$ 的[本征值](@entry_id:154894)和本征矢量本身就包含了深刻的[物理信息](@entry_id:152556)。由于 $H_{\mathrm{eff}}$ 非厄米，其[本征值](@entry_id:154894) $E_\pm$ 通常是复数：
$$
E_\pm = \mathcal{E}_\pm - i\frac{\hbar\gamma_\pm}{2}
$$
其实部 $\mathcal{E}_\pm$ 对应于系统“[缀饰态](@entry_id:143646)”（dressed states）的能量，而其虚部则决定了这些缀饰态的衰减速率 $\gamma_\pm$。因此，通过[对角化](@entry_id:147016) $H_{\mathrm{eff}}$，我们可以直接获得系统在与环境相互作用下的模式的能量和寿命。例如，对于一个受[激光](@entry_id:194225)驱动并同时经历[自发辐射](@entry_id:140032)（速率 $\Gamma$）和纯退相（速率 $\gamma_\phi$）的二能级原子，其 $H_{\mathrm{eff}}$ 的[本征值](@entry_id:154894)之和等于其迹。通过这一性质，可以简洁地证明两个[缀饰态](@entry_id:143646)的衰减率之和为 $\gamma_+ + \gamma_- = \Gamma + 2\gamma_\phi$ [@problem_id:770063]。

非厄米系统一个独特的特性是**[奇异点](@entry_id:199525)**（Exceptional Points, EPs）的存在。在[参数空间](@entry_id:178581)的某个[奇异点](@entry_id:199525)上，[哈密顿量](@entry_id:172864)的两个或多个[本征值](@entry_id:154894)及其对应的本征矢量会同时合并。这与厄米系统中本征矢量始终保持正交的情况截然不同。[奇异点](@entry_id:199525)通常标志着[系统动力学](@entry_id:136288)行为的[相变](@entry_id:147324)，例如从[振荡](@entry_id:267781)衰减模式转变为[过阻尼衰减](@entry_id:274692)模式。考虑一个由增益模式（[增益率](@entry_id:139329)为 $\gamma_a$）和损耗模式（损耗率为 $\gamma_b$）通过[耦合强度](@entry_id:275517) $J$ 相互作用的系统，其[有效哈密顿量](@entry_id:748813)为非厄米矩阵。通过求解其[本征值](@entry_id:154894)，可以发现当[耦合强度](@entry_id:275517)达到临界值 $J_c = \frac{\gamma_a + \gamma_b}{2}$ 时，两个[本征值](@entry_id:154894)合并，系统出现[奇异点](@entry_id:199525) [@problem_id:770091]。

#### 集[体效应](@entry_id:261475)与纠缠生成

[量子跃迁](@entry_id:145857) formalism 也可以自然地推广到多体系统，并用于研究集体效应和纠缠的产生。考虑两个空间上分离的二能级原子，它们都向真空中辐射[光子](@entry_id:145192)。如果一个远处的探测器同时监视这两个原子，它无法分辨[光子](@entry_id:145192)来自哪个原子。因此，探测到一个[光子](@entry_id:145192)所对应的量子跃迁必须由一个**集体跃迁算符**来描述：
$$
C_D = \sqrt{\eta\gamma} \left( e^{-i\mathbf{k}\cdot\mathbf{r}_1}\sigma_-^{(1)} + e^{-i\mathbf{k}\cdot\mathbf{r}_2}\sigma_-^{(2)} \right)
$$
其中 $\sigma_-^{(j)}$ 是第 $j$ 个原子的下降算符，$\mathbf{k}$ 是[光子](@entry_id:145192)[波矢](@entry_id:178620)，相位因子 $e^{-i\mathbf{k}\cdot\mathbf{r}_j}$ 记录了[光子](@entry_id:145192)从原子 $j$ 传播到探测器的[路径信息](@entry_id:169683)。

一个引人注目的结果是，这种集体测量能够产生纠缠。假设两个原子最初处于完全分离的[激发态](@entry_id:261453) $|ee\rangle$。当探测器记录到第一个[光子](@entry_id:145192)时，系统状态会根据集体跃迁算符 $C_D$ 进行投影。计算表明，投影后的新状态是 $| \psi' \rangle \propto (e^{-i\phi_1}|ge\rangle + e^{-i\phi_2}|eg\rangle)$，这是一个最大纠缠的[贝尔态](@entry_id:140749) [@problem_id:769964]。这个例子生动地展示了量子跃迁（即测量过程）如何将一个分离的系统转化为一个纠缠的系统，凸显了[量子跃迁方法](@entry_id:141708)在研究多体量子现象和[量子信息处理](@entry_id:158111)中的强大威力。