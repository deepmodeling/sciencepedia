## 引言
密度泛函理论 (DFT) 是现代计算物理、[计算化学](@entry_id:143039)和材料科学中最重要的基石之一。它提供了一种强大的方法，能够从基本的量子力学原理出发，预测和解释原子、分子和固体的性质，而无需依赖任何经验参数。面对直接求解多电子体系薛定谔方程这一几乎不可能完成的任务，DFT巧妙地将问题转化，用相对简单的电子密度取代了极其复杂的[多体波函数](@entry_id:203043)作为基本变量，从而在计算可行性与物理精度之间取得了卓越的平衡。

本指南将系统地引导您深入[密度泛函理论](@entry_id:139027)的世界。在第一章“原理与机制”中，我们将探索奠定其基础的[Hohenberg-Kohn定理](@entry_id:139793)和实用的[Kohn-Sham方法](@entry_id:263733)，并深入了解决定理论成败的交换关联泛函近似。接着，在第二章“应用与交叉学科联系”中，我们将展示DFT如何在化学、材料科学等多个交叉学科领域中解决从预测分子反应性到模拟超导电性等真实世界的科学问题。最后，第三章“动手实践”部分将提供具体的计算练习，旨在将理论知识转化为解决问题的实践能力，巩固您对DFT计算核心环节的理解。

## 原理与机制

继引言之后，本章将深入探讨[密度泛函理论](@entry_id:139027) (DFT) 的核心科学原理与基本机制。我们将从该理论的严格数学基础出发，逐步构建起一套实用的计算框架，并最终探讨使得DFT成为现代计算科学中强大工具的各种近似方法。我们的目标是不仅阐明“是什么”，更要解释“为什么”，从而为读者提供一个坚实而深入的理解。

### [密度泛函理论](@entry_id:139027)的基石：Hohenberg-Kohn 定理

[密度泛函理论](@entry_id:139027)的整个大厦建立在两条基本定理之上，这两条定理由 Pierre Hohenberg 和 [Walter Kohn](@entry_id:1133945) 于1964年提出。这些定理从根本上改变了我们对多电子体系的看法，将关注点从极其复杂的 [多体波函数](@entry_id:203043) $\Psi(\mathbf{r}_1, \dots, \mathbf{r}_N)$ 转移到了相对简单的 **电子密度 (electron density)** $n(\mathbf{r})$ 上。

对于一个在 Born-Oppenheimer 近似下，由外部势 $v_{\mathrm{ext}}(\mathbf{r})$（通常由原子核产生）所描述的 $N$ 电子体系，其电子密度定义为在真实多体基态[波函数](@entry_id:201714) $\Psi_0$ 下对粒子密度算符 $\hat{n}(\mathbf{r})$ 的[期望值](@entry_id:150961)。由于电子是全同的，这个定义可以简化为：
$$
n(\mathbf{r}) = N \int |\Psi_0(\mathbf{r}, \mathbf{r}_2, \dots, \mathbf{r}_N)|^2 \, d\mathbf{r}_2 \cdots d\mathbf{r}_N
$$
这是一个仅依赖于三个空间坐标的函数，无论系统包含多少电子，这都极大地简化了问题的描述。

**第一 Hohenberg-Kohn (HK) 定理** 提出了一个深刻的唯一性论断：对于一个（非简并的）基态，电子密度 $n(\mathbf{r})$ 唯一地确定了外部势 $v_{\mathrm{ext}}(\mathbf{r})$（最多相差一个无关紧要的常数）。由于 $v_{\mathrm{ext}}(\mathbf{r})$ 和电子数 $N$ 共同定义了系统的哈密顿量 $\hat{H}$，这意味着 $n(\mathbf{r})$ 唯一地确定了整个系统的所有性质，包括基态[波函数](@entry_id:201714)和所有可观测的物理量。这条定理的意义在于，它为将电子密度 $n(\mathbf{r})$ 作为基本变量提供了合法性。原则上，所有信息都已编码在这一看似简单的三维函数中。

**第二 Hohenberg-Kohn (HK) 定理** 则建立了一个[变分原理](@entry_id:198028)。它断言存在一个普适的[能量泛函](@entry_id:170311) $E_v[n]$，其形式为：
$$
E_v[n] = F[n] + \int v_{\mathrm{ext}}(\mathbf{r}) n(\mathbf{r}) \, d\mathbf{r}
$$
其中 $F[n] = \langle \Psi[n] | (\hat{T} + \hat{V}_{ee}) | \Psi[n] \rangle$ 是一个 **[普适泛函](@entry_id:140176) (universal functional)**，它包含了电子的动能 ($\hat{T}$) 和[电子-电子相互作用](@entry_id:139900)能 ($\hat{V}_{ee}$)，并且不依赖于特定的外部势 $v_{\mathrm{ext}}(\mathbf{r})$。第二 HK 定理指出，对于真实的外部势 $v_{\mathrm{ext}}(\mathbf{r})$，当且仅当 $n(\mathbf{r})$ 是该体系的真实基[态密度](@entry_id:147894)时，[能量泛函](@entry_id:170311) $E_v[n]$ 取得其最小值，这个最小值就是体系的[基态能量](@entry_id:263704) $E_0$。

### 严格的[变分原理](@entry_id:198028)：Levy-Lieb 约[束搜索](@entry_id:634146)

最初的 HK 定理在证明上依赖于一个较强的假设，即任何“合理”的密度都必须是某个物理体系的基态密度（即所谓的 **v-[可表示性](@entry_id:635277) (v-representability)** 问题）。为了绕开这一难题并建立一个更具普遍性的框架，Levy 和 Lieb 提出了 **约[束搜索](@entry_id:634146) (constrained-search)** 的构想。

该方法直接从量子力学的 Rayleigh-Ritz 变分原理出发，将对[波函数](@entry_id:201714) $\Psi$ 的最小化过程分解为两步。首先，对于一个给定的、满足基本物理条件的密度 $n(\mathbf{r})$（例如 $n(\mathbf{r}) \ge 0$ 且 $\int n(\mathbf{r}) d\mathbf{r} = N$，即 **[N-可表示性](@entry_id:189302) (N-representability)**），我们搜索所有能够产生该密度的归一化[反对称波函数](@entry_id:153813) $\Psi$，并找到使动能和相互作用能[期望值](@entry_id:150961) $\langle \Psi | \hat{T} + \hat{V}_{ee} | \Psi \rangle$ 最小的那一个。这个最小值就被定义为[普适泛函](@entry_id:140176) $F[n]$ 的值：
$$
F[n] = \min_{\Psi \to n} \langle \Psi | \hat{T} + \hat{V}_{ee} | \Psi \rangle
$$
这里的记号 $\Psi \to n$ 表示搜索所有产生密度 $n$ 的[波函数](@entry_id:201714)。这个定义是“普适的”，因为它不涉及任何特定的外部势。

有了这个定义，基态能量的变分原理就可以被严谨地表述为对所有 N-可表示密度的最小化过程：
$$
E_0 = \min_{n} \left\{ F[n] + \int n(\mathbf{r}) v_{\mathrm{ext}}(\mathbf{r}) \, d\mathbf{r} \right\}
$$
这个表述方式不仅在数学上更为严谨，而且为发展近似泛函提供了清晰的思路：我们的任务就是去近似这个未知的[普适泛函](@entry_id:140176) $F[n]$。

### Kohn-Sham 方法：从相互作用到非相互作用的映射

尽管 HK 定理和 Levy-Lieb 的构想在理论上是完美的，但[普适泛函](@entry_id:140176) $F[n]$ 的确切形式是未知的，并且其动能部分极难直接计算。1965年，[Walter Kohn](@entry_id:1133945) 和 Lu Jeu Sham 提出了一种天才的解决方案，即 **Kohn-Sham (KS) 方法**。其核心思想是引入一个辅助的、虚拟的 **非相互作用电子体系 (non-interacting electron system)**，并巧妙地设计这个体系，使其基[态密度](@entry_id:147894)与我们关心的真实相互作用体系的基态密度 *完全相同*。

为了实现这一点，KS 方法将[普适泛函](@entry_id:140176) $F[n]$ 分解为三个部分：
1.  **非相互作用动能 ($T_s[n]$)**：这是那个具有相同密度 $n(\mathbf{r})$ 的辅助非相互作用体系的动能。它不等于真实体系的动能 $T[n]$。
2.  **哈特里能 ($E_{\mathrm{H}}[n]$)**：这是电子密度云与其自身相互作用的经典静电排斥能，也称为 **经典[库仑能](@entry_id:161936) (classical Coulomb energy)**。
3.  **交换关联能 ($E_{\mathrm{xc}}[n]$)**：这是一个“余项”，它被 *定义* 为包含了所有被忽略的复杂多体量子效应。

因此，总能量泛函可以重写为：
$$
E[n] = T_s[n] + E_{\mathrm{H}}[n] + E_{\mathrm{xc}}[n] + \int v_{\mathrm{ext}}(\mathbf{r}) n(\mathbf{r}) \, d\mathbf{r}
$$
其中，哈特里能的具体形式源于经典静电学，表达式为：
$$
E_{\mathrm{H}}[n] = \frac{1}{2} \iint \frac{n(\mathbf{r}) n(\mathbf{r}')}{|\mathbf{r}-\mathbf{r}'|} \, d\mathbf{r} d\mathbf{r}'
$$
这里的因子 $\frac{1}{2}$ 是为了避免对每一对电子的相互作用进行重复计数。

交换关联能 $E_{\mathrm{xc}}[n]$ 则被定义为：
$$
E_{\mathrm{xc}}[n] = F[n] - T_s[n] - E_{\mathrm{H}}[n] = (T[n] - T_s[n]) + (V_{ee}[n] - E_{\mathrm{H}}[n])
$$
这清楚地表明，$E_{\mathrm{xc}}[n]$ 包含了真实动能与非相互作用动能之差（动能关联部分），以及总的[电子-电子相互作用](@entry_id:139900)能与经典哈特里能之差（所有非经典的交换和关联效应）。

通过对上述[能量泛函](@entry_id:170311)关于轨道进行变分，可以推导出一组有效的单粒子方程，即 **Kohn-Sham 方程**：
$$
\left( -\frac{1}{2}\nabla^2 + v_{s}(\mathbf{r}) \right) \phi_i(\mathbf{r}) = \epsilon_i \phi_i(\mathbf{r})
$$
这里的 $\phi_i$ 是所谓的 **Kohn-Sham 轨道 (Kohn-Sham orbitals)**，$\epsilon_i$ 是其对应的本征能量。电子密度由占据的 KS 轨道构成：$n(\mathbf{r}) = \sum_{i=1}^N |\phi_i(\mathbf{r})|^2$。

至关重要的 **有效势 (effective potential)** $v_s(\mathbf{r})$ 是一个局域的乘性势，其形式为：
$$
v_s(\mathbf{r}) = v_{\mathrm{ext}}(\mathbf{r}) + v_{\mathrm{H}}(\mathbf{r}) + v_{\mathrm{xc}}(\mathbf{r})
$$
其中，$v_{\mathrm{H}}(\mathbf{r}) = \frac{\delta E_{\mathrm{H}}[n]}{\delta n(\mathbf{r})} = \int \frac{n(\mathbf{r}')}{|\mathbf{r}-\mathbf{r}'|} d\mathbf{r}'$ 是哈特里势，而 **交换关联势 (exchange-correlation potential)** $v_{\mathrm{xc}}(\mathbf{r})$ 定义为交换关联能的 **泛函导数 (functional derivative)**：
$$
v_{\mathrm{xc}}(\mathbf{r}) = \frac{\delta E_{\mathrm{xc}}[n]}{\delta n(\mathbf{r})}
$$
由于 $v_s(\mathbf{r})$ 依赖于它所要决定的密度 $n(\mathbf{r})$（通过 $v_{\mathrm{H}}$ 和 $v_{\mathrm{xc}}$），KS 方程必须通过 **[自洽场](@entry_id:136549) (Self-Consistent Field, SCF)** 迭代求解。KS 方法的巨大成功在于，它将一个复杂的相互作用[多体问题](@entry_id:138087)，在形式上转化为了一个更易于处理的非相互作用单粒子问题。所有的复杂性都被巧妙地隐藏在了那个尚待确定的交换关联泛函 $E_{\mathrm{xc}}[n]$ 之中。

### 交换关联泛函的近似：“[雅各布天梯](@entry_id:139901)”

精确的 $E_{\mathrm{xc}}[n]$ 是未知的，DFT 的实用性完全取决于我们能否找到足够精确的近似泛函。对 $E_{\mathrm{xc}}[n]$ 的近似研究构成了一个层次结构，常被比喻为“[雅各布天梯](@entry_id:139901)”，每一级都比前一级更复杂、通常也更精确。

#### [自相互作用误差](@entry_id:260813)

在探讨近似之前，必须理解一个关键概念：**自相互作用误差 (Self-Interaction Error, SIE)**。对于任何单电子体系（如氢原子），真实的[电子-电子相互作用](@entry_id:139900)能应为零。然而，哈特里能 $E_{\mathrm{H}}[n]$ 是一个密度与其自身的经典排斥，对于单电子体系，它是一个非零的正值，代表了电子与其自身电荷云的虚假相互作用。因此，精确的交换关联泛函必须满足一个严格的条件：对于任何单电子密度 $n_{1e}$，必须有 $E_{\mathrm{xc}}^{\mathrm{exact}}[n_{1e}] = -E_{\mathrm{H}}[n_{1e}]$，从而精确地抵消这种虚假的[自相互作用](@entry_id:201333)。许多近似泛函无法满足此条件，这是它们产生误差的一个重要来源。

#### 第一级：局域密度近似 (LDA)

天梯的第一级是 **[局域密度近似](@entry_id:138982) (Local Density Approximation, LDA)**。[LDA](@entry_id:138982) 的核心假设非常简单：在空间中的每一点 $\mathbf{r}$，体系的交换关联能密度只依赖于该点的电子密度值 $n(\mathbf{r})$，并且其函数形式与密度为 $n(\mathbf{r})$ 的 **[均匀电子气](@entry_id:195006) (Uniform Electron Gas, UEG)** 的交换关联能密度相同。

其数学形式为：
$$
E_{\mathrm{xc}}^{\mathrm{LDA}}[n] = \int n(\mathbf{r}) \varepsilon_{\mathrm{xc}}^{\mathrm{UEG}}(n(\mathbf{r})) \, d\mathbf{r}
$$
其中 $\varepsilon_{\mathrm{xc}}^{\mathrm{UEG}}(n)$ 是[均匀电子气](@entry_id:195006)中每个粒子的交换关联能，这是一个已知的（通过解析和数值方法，如[量子蒙特卡洛](@entry_id:144383)）关于密度的函数。[LDA](@entry_id:138982) 的一个重要优点是它自动满足了关于 **交换关联空穴 (exchange-correlation hole)** 的求和规则，这是一个基本的物理约束。然而，由于其纯粹的局域性，LDA 适用于电子密度缓慢变化的体系，而对于密度变化剧烈的体系（如分子和原子表面）则表现不佳，并且它存在显著的[自相互作用误差](@entry_id:260813)。

#### 第二级：[广义梯度近似 (GGA)](@entry_id:140295)

为了改进 [LDA](@entry_id:138982)，天梯的第二级引入了对密度梯度的依赖，即 **[广义梯度近似](@entry_id:274118) (Generalized Gradient Approximation, GGA)**。GGA 不仅考虑了某点的密度 $n(\mathbf{r})$，还考虑了该点密度的变化率 $|\nabla n(\mathbf{r})|$。为了构造一个具有普适性的泛函，梯度通常以无量纲的 **简约密度梯度 (reduced density gradient)** $s$ 的形式出现：
$$
s = \frac{|\nabla n|}{2 k_F n} \propto \frac{|\nabla n|}{n^{4/3}}
$$
其中 $k_F \propto n^{1/3}$ 是局域[费米波矢](@entry_id:140713)。$s$ 衡量了在局域费米波长尺度上密度的变化快慢。

GGA 泛函通常写成对 LDA 的一个增强因子 $F_{\mathrm{xc}}(n, s)$ 的形式：
$$
E_{\mathrm{xc}}^{\mathrm{GGA}}[n] = \int n(\mathbf{r}) \varepsilon_{\mathrm{xc}}^{\mathrm{UEG}}(n(\mathbf{r})) F_{\mathrm{xc}}(n(\mathbf{r}), s(\mathbf{r})) \, d\mathbf{r}
$$
非经验性的 GGA 泛函（如 PBE）是通过强制 $F_{\mathrm{xc}}$ 满足一系列已知的精确物理约束来构建的，而不是通[过拟合](@entry_id:139093)实验数据。这些约束包括：恢复[均匀电子气](@entry_id:195006)极限、正确的坐标标度关系、满足 Lieb-Oxford 界限等。GGA 显著改善了对分子[键能](@entry_id:142761)等性质的描述，是目前最广泛使用的泛函之一。

#### 第三级和第四级：[杂化泛函](@entry_id:164921)

更高层次的近似引入了非局域的成分，通常是精确的 **[哈特里-福克](@entry_id:142303) ([Hartree-Fock](@entry_id:142303), HF) 交换**。其理论基础是 **[绝热连接](@entry_id:199259) (adiabatic connection)** 理论，它通过一个[耦合常数](@entry_id:747980) $\lambda$ 将非相互作用的 KS 体系 ($\lambda=0$) 和完全相互作用的物理体系 ($\lambda=1$) 连接起来。交换关联能可以表示为对 $\lambda$ 从 0 到 1 的积分。

**杂化泛函 (Hybrid functionals)** (天梯第三级) 通过一个简单的[线性插值](@entry_id:137092)来近似这个积分，将一定比例 $\alpha$ 的 HF 精确交换 ($E_x^{\mathrm{HF}}$) 与 DFT 交换（通常来自 GGA）混合在一起：
$$
E_{\mathrm{xc}}^{\mathrm{hyb}}[n] = \alpha E_x^{\mathrm{HF}} + (1-\alpha) E_x^{\mathrm{GGA}} + E_c^{\mathrm{GGA}}
$$
这种混合有助于修正 GGA 的自相互作用误差，并通常能提供更准确的[能带隙](@entry_id:156238)和[反应能](@entry_id:143747)垒。著名的例子包括 B3LYP 和 PBE0。

**[范围分离杂化泛函](@entry_id:184447) (Range-separated hybrid functionals)** 则更为精巧。它们利用[误差函数](@entry_id:176269) $\operatorname{erf}$ 和[互补误差函数](@entry_id:190973) $\operatorname{erfc}$ 将[库仑相互作用](@entry_id:747947)分解为短程和长程部分：
$$
\frac{1}{r} = \frac{\operatorname{erfc}(\mu r)}{r}_{\text{(SR)}} + \frac{\operatorname{erf}(\mu r)}{r}_{\text{(LR)}}
$$
然后对短程和长程的交换作用采取不同的处理方式。例如，HSE 泛函仅在短程混合 HF 交换，而保持长程交换为纯 DFT 形式，这在计算固体的[能带结构](@entry_id:139379)时特别有效，因为它能以较低的计算成本获得接近杂化泛函的精度。

### 物理诠释：KS 本征值与[导数不连续性](@entry_id:136336)

尽管 KS 方程在形式上类似于单粒子薛定谔方程，但 KS 轨道和本征值 $\epsilon_i$ 的物理解释需要特别小心。根据 **Janak 定理**，KS 本征值等于总能量对该轨道占据数的偏导数：$\epsilon_i = \partial E / \partial f_i$。

对于精确的 DFT，可以证明体系的总能量 $E(N)$ 作为电子数 $N$ 的函数，在整数之间是[分段线性](@entry_id:201467)的。这一性质导致了一个深刻的结论：对于一个 $N$ 电子体系，其 **最高占据分子轨道 (HOMO)** 的本征值精确地等于体系负的 **[电离势](@entry_id:198846) (Ionization Potential, IP)**：
$$
\epsilon_{\mathrm{H}}(N) = -I(N) = E(N) - E(N-1)
$$
然而，**最低未占分子轨道 (LUMO)** 的本征值 $\epsilon_{\mathrm{L}}(N)$ *并不* 等于负的 **[电子亲和能](@entry_id:147520) (Electron Affinity, EA)**。这是因为当电子数穿过整数 $N$ 时，精确的交换关联势 $v_{\mathrm{xc}}(\mathbf{r})$ 会发生一个阶跃，这个阶跃是一个空间上均匀的常数，被称为 **[导数不连续性](@entry_id:136336) (derivative discontinuity)**, $\Delta_{\mathrm{xc}}$。

这个[不连续性](@entry_id:144108)修正了 LUMO 本征值与电子亲和能的关系，并直接关系到 **基本[带隙](@entry_id:138445) (fundamental gap)** $E_g = I - A$。精确的关系是：
$$
E_g = I - A = (\epsilon_{\mathrm{L}} - \epsilon_{\mathrm{H}}) + \Delta_{\mathrm{xc}}
$$
其中 $(\epsilon_{\mathrm{L}} - \epsilon_{\mathrm{H}})$ 是 KS [带隙](@entry_id:138445)。这意味着，即使使用精确的泛函，KS [带隙](@entry_id:138445)也与基本[带隙](@entry_id:138445)相差一个 $\Delta_{\mathrm{xc}}$。而对于 [LDA](@entry_id:138982) 和 GGA 这类近似泛函，它们是密度的平滑函数，无法描述这种[导数不连续性](@entry_id:136336)（即 $\Delta_{\mathrm{xc}} \approx 0$）。这正是这些近似泛函系统性地低估半导体和绝缘体[带隙](@entry_id:138445)的根本原因，即所谓的“DFT [带隙问题](@entry_id:143831)”。理解[导数不连续性](@entry_id:136336)对于正确诠释 DFT 计算结果和发展更高级的泛函至关重要。