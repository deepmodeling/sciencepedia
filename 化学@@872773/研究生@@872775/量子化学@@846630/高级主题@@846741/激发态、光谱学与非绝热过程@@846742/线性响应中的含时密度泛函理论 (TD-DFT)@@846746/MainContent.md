## 引言
理解物质如何与光相互作用，是化学、物理学和[材料科学](@entry_id:152226)等众多领域的核心议题。电子激发态在这一过程中扮演着中心角色，决定了从光合作用到[有机发光二极管](@entry_id:146731)（OLED）等一系列关键现象。[含时密度泛函理论](@entry_id:200019)（Time-Dependent Density Functional Theory, TDDFT），特别是其[线性响应](@entry_id:146180)形式，已经成为现代计算科学中预测和诠释电子激发态性质的最重要工具之一。它在计算成本与精度之间取得了卓越的平衡，使得对复杂分子和材料的[光谱](@entry_id:185632)性质进行第一性原理研究成为可能。

然而，TDDFT 的广泛应用背后，是深刻而精妙的理论基础。许多使用者仅将其视为一个“黑箱”工具，这限制了对其计算结果的深入理解和批判性评估。本文旨在填补理论形式与实际应用之间的知识鸿沟。我们将系统地阐述该理论如何从最基本的含时 Kohn-Sham 方程出发，构建出计算[激发光谱](@entry_id:139562)的实用方法，并着重剖析其成功的关键——[交换相关核](@entry_id:195258)的近似——及其带来的固有局限性。

为构建这一全面的理解，本文将分为三个章节。在第一章“原理与机制”中，我们将深入理论核心，推导 Casida 方程，并探讨[绝热近似](@entry_id:143074)等关键概念及其对不同类型电子激发（如电荷转移和里德堡激发）的影响。第二章“应用与交叉学科联系”将展示 TDDFT 的广阔应用前景，从[分子光谱学](@entry_id:148164)到凝聚态物理，再到光[化学动力学模拟](@entry_id:747318)，揭示其作为连接不同科学领域的桥梁作用。最后，在“动手实践”部分，我们将通过具体的计算问题，将理论知识转化为解决实际问题的能力。现在，让我们从其坚实的理论基础开始。

## 原理与机制

本章旨在深入阐述[线性响应含时密度泛函理论](@entry_id:751293) (Time-Dependent Density Functional Theory, TDDFT) 的核心原理与基本机制。我们将从其理论基石——含时 Kohn-Sham 方程出发，系统地推导和解释用于计算[激发光谱](@entry_id:139562)的核心方程，并探讨该理论框架下常用近似方法的内在优势与固有局限。

### 从含时 Kohn-Sham 方程开始

[含时密度泛函理论](@entry_id:200019)的基石是 Runge-Gross 定理，它保证了对于一个给定的初态，体系的含时电子密度 $n(\mathbf{r},t)$ 与其所处的外界标量势 $v_{\text{ext}}(\mathbf{r},t)$ 之间存在[一一对应](@entry_id:143935)关系（相差一个仅与时间相关的函数）。这一定理的深远意义在于，它为构建一个能够精确再现真实相互作用体系密度的、形式上更简单的“虚拟”非相互作用体系提供了合法性。这个虚拟体系被称为 **Kohn-Sham (KS) 体系**。

KS 体系中的电子（或称 KS [轨道](@entry_id:137151) $\phi_{p}(\mathbf{r},t)$）虽然互不直接作用，但它们在一个共同的、局域的有效势场 $v_{\text{s}}(\mathbf{r},t)$ 中演化。每个 KS [轨道](@entry_id:137151)都遵循一个单粒子薛定谔方程，即**含时 Kohn-Sham (TDKS) 方程** [@problem_id:2932867]：
$$
i\frac{\partial}{\partial t}\phi_{p}(\mathbf{r},t) = \left[-\frac{1}{2}\nabla^{2} + v_{\text{s}}(\mathbf{r},t)\right]\phi_{p}(\mathbf{r},t)
$$
（此处及下文均采用[原子单位](@entry_id:166762)）。真实相互作用体系的含时电子密度则通过对占据的 KS [轨道](@entry_id:137151)的模方求和得到：$n(\mathbf{r},t) = \sum_{p}^{\text{occ}} |\phi_{p}(\mathbf{r},t)|^2$。

成功的关键在于有效 KS 势 $v_{\text{s}}(\mathbf{r},t)$ 的构造。它被精确地分解为三个部分：
$$
v_{\text{s}}(\mathbf{r},t) = v_{\text{ext}}(\mathbf{r},t) + v_{\text{H}}[n](\mathbf{r},t) + v_{\text{xc}}[n;\Psi_{0},\Phi_{0}](\mathbf{r},t)
$$
其中，$v_{\text{ext}}(\mathbf{r},t)$ 是体系所受的真实外界势（例如，[原子核](@entry_id:167902)的吸引势和外加[电磁场](@entry_id:265881)）；$v_{\text{H}}[n](\mathbf{r},t)$ 是经典的**哈特里 (Hartree) 势**，它描述了电子密度[分布](@entry_id:182848)产生的平均[静电排斥](@entry_id:162128)，是一个瞬时密度泛函：
$$
v_{\text{H}}[n](\mathbf{r},t) = \int d\mathbf{r}' \frac{n(\mathbf{r}',t)}{|\mathbf{r}-\mathbf{r}'|}
$$
最重要的项是**交换相关 (exchange–correlation, xc) 势** $v_{\text{xc}}(\mathbf{r},t)$。它囊括了所有非经典的、复杂的量子[多体效应](@entry_id:173569)。与瞬时的哈特里势不同，精确的 $v_{\text{xc}}$ 是一个具有“[记忆效应](@entry_id:266709)”的泛函。这意味着在时刻 $t$ 的 $v_{\text{xc}}(\mathbf{r},t)$ 不仅依赖于同一时刻的密度 $n(\mathbf{r},t)$，还依赖于从初始时刻 $t_0$ 到当前时刻 $t$ 的整个密度演化历史 $\{n(\cdot, t')\}_{t' \le t}$。此外，由于 Runge-Gross 映射是针对给定的相互作用体系初态 $\Psi_0$ 建立的，因此精确的 $v_{\text{xc}}$ 泛函也必然依赖于 $\Psi_0$。为了使 KS 体系能够复现密度，其自身也必须从一个特定的初态 $\Phi_0$ (通常是[斯莱特行列式](@entry_id:139034)) 开始演化，因此 $v_{xc}$ 也隐式地依赖于 $\Phi_0$ [@problem_id:2932867]。

值得注意的是，KS 势存在一个[规范自由度](@entry_id:160491)：给 $v_{\text{s}}(\mathbf{r},t)$ 加上一个任意的、仅与时间相关的函数 $c(t)$，并不会改变体系的电子密度。这仅仅会给每个 KS [轨道](@entry_id:137151)附加一个相同的含时相位因子，而在计算密度时此相位因子会被抵消 [@problem_id:2932867]。

### [线性响应理论](@entry_id:145737)：微扰下的密度变化

在许多应用场景中，我们关心的是体系对一个微弱的、含时外界微扰 $\delta v_{\text{ext}}(\mathbf{r},t)$ 的响应。如果微扰足够弱，体系的性质变化（例如电子密度）可以近似地看作是与微扰成线性的，这就是**[线性响应理论](@entry_id:145737)**的范畴。

体系在 $t$ 时刻的密度变化 $\delta n(\mathbf{r}, t)$ 是由所有过去时刻 $t' \le t$ 的微扰共同决定的。这种因果关系可以通过一个时空卷积来表示：
$$
\delta n(\mathbf{r}, t) = \int_{-\infty}^{t} dt' \int d\mathbf{r}' \, \chi(\mathbf{r},t; \mathbf{r}',t') \delta v_{\text{ext}}(\mathbf{r}',t')
$$
这里的核心是**密度-密度响应函数** (或称极化率) $\chi(\mathbf{r},t; \mathbf{r}',t')$，它量化了在 $(\mathbf{r}',t')$ 处的点微扰对 $(\mathbf{r},t)$ 处密度产生的效应。在量子力学中，这个**推迟[响应函数](@entry_id:142629)** $\chi^R$ 可以通过 [Kubo 公式](@entry_id:144041)，由[密度算符](@entry_id:138151)在[海森堡绘景](@entry_id:141162)下的对易子[期望值](@entry_id:153208)给出 [@problem_id:2932807]：
$$
\chi^R(\mathbf{r},\mathbf{r}',t-t') = -i\,\theta(t-t')\,\langle[\hat{n}_{H}(\mathbf{r},t), \hat{n}_{H}(\mathbf{r}',t')]\rangle
$$
其中 $\theta(t-t')$ 是赫维赛德[阶跃函数](@entry_id:159192)，保证了响应的因果性。

在[频域](@entry_id:160070)中处理问题往往更为便捷。若采用[傅里叶变换](@entry_id:142120)约定 $F(\omega) = \int_{-\infty}^{\infty} dt \, e^{i\omega t} F(t)$，那么时域中的卷积就变成了[频域](@entry_id:160070)中的简单乘积：
$$
\delta n(\mathbf{r},\omega) = \int d\mathbf{r}' \, \chi(\mathbf{r},\mathbf{r}',\omega) \, \delta v_{\text{ext}}(\mathbf{r}',\omega)
$$
[响应函数](@entry_id:142629)的因果性对其在复[频域](@entry_id:160070)上的[解析性](@entry_id:140716)质有严格的约束。对于上述[傅里叶变换](@entry_id:142120)约定，$\chi(\omega)$ 在[复频率](@entry_id:266400)平面的[上半平面](@entry_id:199119)（$\operatorname{Im}\omega > 0$）是解析的。此外，对于一个被动的物理系统，能量耗散必须为正，这要求对于正频率 $\omega > 0$，响应函数虚部 $\operatorname{Im}\chi(\omega)$ 必须为负（或零），它直接关联到体系的吸收谱 [@problem_id:2932807]。

### 核心方程：Dyson 型方程

TDDFT [线性响应理论](@entry_id:145737)的精髓在于，它建立了一座桥梁，连接了易于计算的 KS 体系响应与难以企及的真实相互作用体系响应。这通过一个 Dyson 型方程得以实现。

我们定义两个关键的[响应函数](@entry_id:142629) [@problem_id:2683041]：
1.  **相互作用响应函数** $\chi$，描述真实体系密度对**外界势**微扰的响应：$\chi = \frac{\delta n}{\delta v_{\text{ext}}}$。
2.  **Kohn-Sham [响应函数](@entry_id:142629)** $\chi_s$，描述非相互作用 KS 体系密度对**KS 有效势**微扰的响应：$\chi_s = \frac{\delta n}{\delta v_s}$。

$\chi_s$ 可以通过 Adler-Wiser 公式，利用[基态](@entry_id:150928) KS [轨道](@entry_id:137151)和[轨道](@entry_id:137151)能精确计算出来。我们的目标是求 $\chi$。为此，我们利用泛函求导的链式法则。KS 势的微扰 $\delta v_s$ 包含三部分：
$$
\delta v_s(\mathbf{r}, t) = \delta v_{\text{ext}}(\mathbf{r}, t) + \delta v_{\text{H}}(\mathbf{r}, t) + \delta v_{\text{xc}}(\mathbf{r}, t)
$$
其中，哈特里势和[交换相关势](@entry_id:180254)的微扰都是由密度微扰 $\delta n$ 引起的。这引入了两个核心的**[相互作用核](@entry_id:193790)**：
- **哈特里核 (Hartree kernel)** $f_{\text{H}} = \frac{\delta v_{\text{H}}}{\delta n} = \frac{\delta(t-t')}{|\mathbf{r}-\mathbf{r}'|}$。它是瞬时的，因为[库仑相互作用](@entry_id:747947)是瞬时传播的。
- **[交换相关核](@entry_id:195258) (exchange-correlation kernel)** $f_{\text{xc}} = \frac{\delta v_{\text{xc}}}{\delta n}$。精确的 $f_{\text{xc}}$ 和 $v_{xc}$ 一样具有[记忆效应](@entry_id:266709)，即 $f_{\text{xc}}(\mathbf{r},t; \mathbf{r}',t')$ 在 $t' \lt t$ 时不为零。

将这些关系整合到 $\delta n = \chi_s \star \delta v_s$（其中 $\star$ 代表时空积分）中，经过整理，我们得到一个连接 $\chi$ 和 $\chi_s$ 的方程，即 TDDFT 的 **Dyson 型方程** [@problem_id:2683041]：
$$
\chi = \chi_s + \chi_s \star (f_{\text{H}} + f_{\text{xc}}) \star \chi
$$
在[频域](@entry_id:160070)中，该方程形式更简洁，变为一个[矩阵代数](@entry_id:153824)方程：
$$
\chi(\mathbf{r}, \mathbf{r}', \omega) = \chi_s(\mathbf{r}, \mathbf{r}', \omega) + \iint d\mathbf{r}_1 d\mathbf{r}_2 \, \chi_s(\mathbf{r}, \mathbf{r}_1, \omega) \left[f_{\text{H}}(\mathbf{r}_1, \mathbf{r}_2) + f_{\text{xc}}(\mathbf{r}_1, \mathbf{r}_2, \omega)\right] \chi(\mathbf{r}_2, \mathbf{r}', \omega)
$$
这个方程表明，真实体系的响应 $\chi$ 可以看作是 KS 响应 $\chi_s$ 被 Hartree 和交换相关相互作用“修正”或“屏蔽”后的结果。

### Casida 方程：求解[激发能](@entry_id:190368)

体系的[电子激发](@entry_id:190531)能对应于其吸收光谱的峰位，在理论上，这正是相互作用响应函数 $\chi(\omega)$ 的极点。Dyson 型方程指出，$\chi(\omega)$ 的极点出现在使得算符 $[1 - \chi_s(\omega)f_{\text{Hxc}}(\omega)]$ 奇异的频率 $\omega$ 处。将这个问题投影到由 KS 体系的“粒子-空穴”对（即从占据[轨道](@entry_id:137151) $i$ 到未占据[轨道](@entry_id:137151) $a$ 的跃迁）构成的[基组](@entry_id:160309)上，便引出了一个可解的矩阵本征值问题，这便是著名的 **Casida 方程**。

在标准的推导中，该问题最初表现为一个非[厄米矩阵](@entry_id:155147)的广义[本征问题](@entry_id:748835)。然而，通过巧妙的代数变换，它可以转化为一个厄米[本征问题](@entry_id:748835)，形式如下 [@problem_id:2902126]：
$$
\mathbf{\Omega}(\omega) \mathbf{F} = \omega^2 \mathbf{F}
$$
其中，$\omega$ 是体系的激发能，$\mathbf{F}$ 是与之对应的[本征向量](@entry_id:151813)，而厄米矩阵 $\mathbf{\Omega}$ 的矩阵元由下式给出：
$$
\Omega_{ia,jb}(\omega) = \delta_{ij}\delta_{ab}(\varepsilon_{a}-\varepsilon_{i})^{2} + 2\sqrt{(\varepsilon_{a}-\varepsilon_{i})(\varepsilon_{b}-\varepsilon_{j})} K_{ia,jb}(\omega)
$$
这里，$i, j$ 代表占据[轨道](@entry_id:137151)，$a, b$ 代表未占据（虚）[轨道](@entry_id:137151)，$\varepsilon_p$ 是 KS [轨道](@entry_id:137151)的能量。对角项 $(\varepsilon_{a}-\varepsilon_{i})^2$ 是 KS 单粒子跃迁能量的平方，而非对角项则描述了不同单粒子跃迁之间的耦合。这个**[耦合矩阵](@entry_id:191757)元** $K_{ia,jb}$ 的表达式为：
$$
K_{ia,jb}(\omega) = \iint d\mathbf{r} d\mathbf{r}' \, \phi_{i}^{*}(\mathbf{r})\phi_{a}(\mathbf{r}) \, f_{\text{Hxc}}(\mathbf{r},\mathbf{r}',\omega) \, \phi_{j}(\mathbf{r}')\phi_{b}^{*}(\mathbf{r}')
$$
其中 $f_{\text{Hxc}} = f_{\text{H}} + f_{\text{xc}}$ 是 Hartree-exchange-correlation 核的总和。这个表达式清晰地展示了激发能是如何由[基态](@entry_id:150928) KS [轨道](@entry_id:137151) $\phi_p$、[轨道](@entry_id:137151)能 $\varepsilon_p$ 以及核心的[相互作用核](@entry_id:193790) $f_{\text{Hxc}}$ 共同决定的。

为了更具体地理解[耦合矩阵](@entry_id:191757)，我们可以考虑一个简化模型。假设 $f_{\text{Hxc}}$ 是一个局域且与频率无关的核，形式为 $f(x,x') = \kappa \delta(x-x')$。对于一个[一维无限深势阱](@entry_id:271157)中的粒子（其归一化 KS [轨道](@entry_id:137151)为 $\phi_n(x) = \sqrt{2/L} \sin(n\pi x/L)$），我们可以计算从 $i=1$ 到 $a=2$ 的跃迁与其自身的[耦合矩阵](@entry_id:191757)元 $K_{12,12}$。通过积分 $\kappa \int_0^L [\phi_1(x)\phi_2(x)]^2 dx$，可以得到一个具体的数值结果，它正比于 $\kappa/L$ [@problem_id:2932981]。这个例子直观地揭示了[耦合矩阵](@entry_id:191757)元是如何将抽象的理论概念与具体的[轨道形状](@entry_id:137387)和相互作用强度联系起来的。

### 从 Casida 向量到[光谱](@entry_id:185632)：振子强度

求解 Casida 方程不仅能得到[激发能](@entry_id:190368) $\Omega_S$ (即矩阵 $\mathbf{\Omega}$ [本征值](@entry_id:154894)的平方根)，还能得到相应的[本征向量](@entry_id:151813) $\mathbf{F}_S$。通过这些向量，我们可以重构出描述激发过程的关键物理量，并最终模拟出吸收光谱。

首先，与[激发态](@entry_id:261453) $|S\rangle$ 相关的**跃迁密度** $\rho_S(\mathbf{r}) = \langle 0 | \hat{n}(\mathbf{r}) | S \rangle$ 可以在 KS 粒子-空穴[基组](@entry_id:160309)中表示为 [@problem_id:2932982]：
$$
\rho_S(\mathbf{r}) = \sum_{ia} (X_{ia}^S + Y_{ia}^S) \phi_i(\mathbf{r})\phi_a(\mathbf{r})
$$
其中 $X_{ia}^S$ 和 $Y_{ia}^S$ 是从 Casida 向量 $\mathbf{F}_S$ 重构出的幅值，分别对应[粒子-空穴激发](@entry_id:137289)和退激发过程的贡献。跃迁密度本身也与响应函数 $\chi(\omega)$ 在极点 $\omega=\Omega_S$ 处的留数直接相关，即 $\text{Res}[\chi(\mathbf{r},\mathbf{r}';\omega)]_{\omega=\Omega_S} = \rho_S(\mathbf{r})\rho_S(\mathbf{r}')$ [@problem_id:2932982]。

[光谱](@entry_id:185632)的峰强度由**振子强度 (oscillator strength)** $f_S$ 决定，它正比于跃迁偶极矩的模方。在[原子单位](@entry_id:166762)中，其表达式为：
$$
f_S = \frac{2}{3} \Omega_S \|\boldsymbol{\mu}_{0S}\|^2
$$
这里的**跃迁偶极矩** $\boldsymbol{\mu}_{0S}$ 是通过对跃迁密度进行偶极算符积分得到的，最终可以表达为 KS 跃迁偶极积分 $\mathbf{d}_{ia} = \int d\mathbf{r} \, \phi_i(\mathbf{r}) \mathbf{r} \phi_a(\mathbf{r})$ 的[线性组合](@entry_id:154743) [@problem_id:2932982]：
$$
\boldsymbol{\mu}_{0S} = \sum_{ia} (X_{ia}^S + Y_{ia}^S) \mathbf{d}_{ia}
$$
因此，一旦 Casida 方程被求解，我们便拥有了计算吸收光谱所需的所有信息：峰位（由 $\Omega_S$ 给出）和峰强（由 $f_S$ 给出）。

此外，振子强度的总和受到一个重要的物理定律——**Thomas-Reiche-Kuhn (TRK) 求和规则**的约束，即 $\sum_S f_S = N$，其中 $N$ 是系统中的电子总数。在 TDDFT 中，当且仅当[交换相关核](@entry_id:195258)是频率无关（[绝热近似](@entry_id:143074)）且满足某些对称性要求时，这条求和规则才能被严格满足 [@problem_id:2932982]。

### [绝热近似](@entry_id:143074)及其后果

到目前为止，我们讨论的都是精确的理论。然而，精确的含时、含记忆的[交换相关核](@entry_id:195258) $f_{\text{xc}}$ 是未知的。在实际计算中，必须引入近似。最广泛使用的近似是**[绝热近似](@entry_id:143074) (adiabatic approximation)**。

[绝热近似](@entry_id:143074)的核心思想是忽略 $v_{\text{xc}}$ 的[记忆效应](@entry_id:266709)，假设在任意时刻 $t$ 的[交换相关势](@entry_id:180254)只依赖于同一时刻的密度[分布](@entry_id:182848)，并且其函数形式与[基态](@entry_id:150928) DFT 中的 $v_{\text{xc}}^{\text{gs}}$ 相同 [@problem_id:2932946]：
$$
v_{\text{xc}}[n](\mathbf{r}, t) \approx v_{\text{xc}}^{\text{gs}}[n(t)](\mathbf{r})
$$
这一近似直接导致[交换相关核](@entry_id:195258) $f_{\text{xc}}$ 失去了对频率的依赖性。其在时域中变为瞬时作用，即 $f_{\text{xc}}(\mathbf{r},t;\mathbf{r}',t') \propto \delta(t-t')$，而在[频域](@entry_id:160070)中则变为一个与频率 $\omega$ 无关的静态核 $f_{\text{xc}}(\mathbf{r},\mathbf{r}';\omega) = f_{\text{xc}}^{\text{static}}(\mathbf{r},\mathbf{r}')$ [@problem_id:2932946] [@problem_id:2932867]。

若进一步采用**绝热[局域密度近似](@entry_id:138982) (Adiabatic Local Density Approximation, ALDA)**，即[基态](@entry_id:150928)泛函采用 LDA，那么 $f_{\text{xc}}$ 不仅与频率无关，在空间上也变为超局域的，即 $f_{\text{xc}}^{\text{ALDA}}(\mathbf{r},\mathbf{r}') \propto \delta(\mathbf{r}-\mathbf{r}')$ [@problem_id:2932946]。A[LDA](@entry_id:138982) 核的形式可以追溯到[均匀电子气](@entry_id:163911) (HEG) 的物理性质。可以证明，A[LDA](@entry_id:138982) 核等于 HEG 的交换相关化学势对密度的导数，即 $f_{\text{xc}}^{\text{ALDA}} = \partial \mu_{\text{xc}} / \partial n$，这又与交换相关部分的压缩性相关 [@problem_id:2932868]。

尽管[绝热近似](@entry_id:143074)大大简化了计算并取得了巨大成功，但其频率无关的本质也带来了一些严重的系统性缺陷。一个突出的例子是它无法描述**双电子激发**（即涉及两个电子同时被激发的态）。在 TDDFT [线性响应](@entry_id:146180)的框架内，[激发态](@entry_id:261453)被构建为单[粒子-空穴激发](@entry_id:137289)的线性组合。要产生具有显著双激发特征的新极点，[相互作用核](@entry_id:193790) $f_{\text{Hxc}}(\omega)$ 自身必须具有复杂的频率依赖性（例如，在双激发能量附近有极点）。绝热核是频率无关的，因此它只能对已有的单[激发态](@entry_id:261453)进行混合和能量移动，而无法从根本上创造出位于单激发空间之外的[双激发态](@entry_id:187815) [@problem_id:2932911] [@problem_id:2932867] [@problem_id:2932946]。

### 半局域泛函的挑战

除了[绝热近似](@entry_id:143074)带来的问题，许多困难还源于[基态](@entry_id:150928) DFT 中广泛使用的[交换相关泛函](@entry_id:142042)（如 LDA 和 GGA）的空间**半局域 (semilocal)** 特性。

#### 里德堡激发 (Rydberg Excitations)

里德堡激发是指一个电子被激发到离原子或分子核芯很远的、非常弥散的[轨道](@entry_id:137151)上。对于一个中性体系，这个远处的电子感受到的有效势应该渐进行为于 $-1/r$ 的库仑吸引势。只有具备这种长程行为的势才能支持一个收敛到电离阈的、无穷多的里德堡态序列。

然而，所有半局域泛函（[LDA](@entry_id:138982), GGA）产生的[交换相关势](@entry_id:180254) $v_{\text{xc}}(\mathbf{r})$ 都随 $r$ 指数衰减，导致总的 KS 势 $v_s(\mathbf{r})$ 衰减过快。这样一个短程的[势阱](@entry_id:151413)只能束缚有限个数的[激发态](@entry_id:261453)，无法正确描述整个里德堡序列。此外，半局域泛函通常会因为自相互作用误差而高估 HOMO [轨道](@entry_id:137151)的能量（即 $\varepsilon_{\text{HOMO}} > -I$，违反了精确泛函应满足的[电离势定理](@entry_id:178221)）。这两个因素共同作用，导致计算出的高能[激发态](@entry_id:261453)被“压缩”在一个错误的、过低的电离限之下 [@problem_id:2932804]。

解决这一问题的根本途径是修正[基态](@entry_id:150928) KS 势的长程行为。采用**渐进行为修正 (asymptotically corrected)** 的泛函，例如[范围分离杂化泛函](@entry_id:184447) (range-separated hybrids)，可以在保持短程[计算效率](@entry_id:270255)的同时，引入长程部分的[精确交换](@entry_id:178558)，从而强制 $v_s(\mathbf{r})$ 具有正确的 $-1/r$ 尾巴。这恢复了 KS 势中正确的里德堡能级结构，是准确计算里德堡激发谱的关键 [@problem_id:2932804]。

#### 长程[电荷转移激发](@entry_id:174772) (Long-Range Charge-Transfer Excitations)

另一个严峻的挑战是描述分子间或分子内长距离的电荷转移 (CT) 激发。考虑一个电子从给体 (D) 分子转移到受体 (A) 分子，当两者相距很远 (距离为 $R$) 时，其激发能的正确物理行为应为 $\omega_{\text{CT}} \approx I_{\text{D}} - A_{\text{A}} - 1/R$，其中 $I_{\text{D}}$ 是给体的[电离势](@entry_id:198846)，$A_{\text{A}}$ 是受体的电子亲和能，$-1/R$ 项代表了最终形成的[离子对](@entry_id:181407) $\text{D}^+ \cdots \text{A}^-$ 之间的库仑吸引。

当使用绝热半局域泛函（如 GGA）时，TDDFT 计算会遭遇灾难性的失败。这是因为 CT 激发对应的 KS 跃迁是从一个局域在 D 上的占据[轨道](@entry_id:137151)到一个局域在 A 上的[虚轨道](@entry_id:188499)。由于两个[轨道](@entry_id:137151)在空间上几乎没有重叠，描述它们之间相互作用的[耦合矩阵](@entry_id:191757)元 $K_{ia,jb}$，当依赖于一个空间局域的 $f_{\text{xc}}$ 核时，会趋向于零。其结果是，计算出的 CT 激发能可悲地退化为裸的 KS [轨道能级](@entry_id:151753)差 $\omega_{\text{CT}} \approx \varepsilon_{\text{L}}^{\text{A}} - \varepsilon_{\text{H}}^{\text{D}}$。这个值不仅本身就因为半局域泛函的缺陷而严重偏低，而且完全丢失了至关重要的 $-1/R$ 渐进行为。同时，计算出的振子强度也因跃迁偶极矩和耦合的消失而趋于零 [@problem_id:2932919]。

这个失败的根源在于[交换相关核](@entry_id:195258)的**空间局域性**。要正确描述长程 CT 激发，核本身必须具有长程的非局域性，以捕捉相隔遥远的[电子和空穴](@entry_id:274534)之间的相互作用。这再次凸显了[范围分离杂化泛函](@entry_id:184447)等包含长程[精确交换](@entry_id:178558)的方法的重要性。