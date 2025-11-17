## 引言
在[计算流体动力学](@entry_id:147500) (CFD) 领域，对[湍流](@entry_id:151300)进行精确建模是解决绝大多数工程与科学问题的关键。在众多湍流模型中，[雷诺平均纳维-斯托克斯](@entry_id:173045) (RANS) 方法因其在计算成本和精度之间的良好平衡而得到广泛应用。其中，k–ε 模型家族作为RANS方法的基石之一，历经数十年的发展与验证。然而，经典的标准 k–ε 模型主要基于经验公式和对简单流动的标定，这导致其在面对[流动分离](@entry_id:143331)、强[旋流](@entry_id:153202)和高应变率等[复杂流动](@entry_id:747569)现象时，预测能力常常不尽人意，这构成了亟待解决的知识缺口。

为了突破这一局限，重整化群 (Renormalization Group, RNG) k–ε 模型应运而生。它并非简单的经验修正，而是源于对纳维-斯托克斯方程更深层次的理论分析，为[湍流建模](@entry_id:151192)提供了更为坚实的物理基础。本文旨在全面而深入地剖析 [RNG k–ε 模型](@entry_id:754380)。在接下来的内容中，读者将系统地学习：

- **原则与机理**：我们将深入探讨 [RNG k–ε 模型](@entry_id:754380)的理论根基，揭示其如何通过系统性的尺度消除推导出模型方程，并重点分析其响应平均[应变率](@entry_id:154778)的核心修正机理及其与标准模型的本质区别。
- **应用与跨学科联系**：本章将展示该模型如何在航空航天、能源工程、传热及[多相流](@entry_id:146480)等前沿领域解决实际问题，阐明其理论优势如何转化为对[分离流](@entry_id:754694)和复杂传热现象的卓越预测能力。
- **动手实践**：通过一系列精心设计的计算练习，读者将有机会亲手应用所学知识，从量纲分析到[模型比较](@entry_id:266577)，从而巩固对 [RNG k–ε 模型](@entry_id:754380)内在机制和应用场景的理解。

通过这三个章节的学习，您将不仅掌握 [RNG k–ε 模型](@entry_id:754380)的“如何用”，更能深刻理解其“为何如此”，从而在未来的科研与工程实践中做出更明智的模型选择和应用。

## 原则与机理

在[雷诺平均纳维-斯托克斯](@entry_id:173045) (RANS) 框架内，[湍流模型](@entry_id:190404)的核心任务是对未知的[雷诺应力张量](@entry_id:270803) $\tau_{ij} = -\rho \overline{u_i' u_j'}$ 进行封闭。$k$–$\varepsilon$ 模型家族通过引入涡粘性假设 (Boussinesq hypothesis) 来实现这一目标，该假设将雷诺应力与平均应变率张量关联起来。本章旨在深入阐述重整化群 (Renormalization Group, RNG) $k$–$\varepsilon$ 模型的理论基础、核心机理及其在工程应用中的地位和局限性。与基于经验和[量纲分析](@entry_id:140259)构建的标准 $k$–$\varepsilon$ 模型不同，RNG 模型源于对[纳维-斯托克斯方程](@entry_id:142275)更系统的理论分析，从而为处理[复杂流动](@entry_id:747569)提供了更坚实的基础。

### 涡粘性模型的基础

所有双方程涡粘性模型都建立在一个共同的理论基石之上，即[Boussinesq假设](@entry_id:272519)。该假设认为，[湍流](@entry_id:151300)脉动对平均流的作用类似于分子粘性，可以引入一个“[湍流](@entry_id:151300)粘度”或“[涡粘度](@entry_id:155814)” $\mu_t$ （或运动[涡粘度](@entry_id:155814) $\nu_t = \mu_t / \rho$）来描述。对于[不可压缩流](@entry_id:140301)动，[雷诺应力张量](@entry_id:270803)的非各向同性部分被认为与平均应变率张量 $S_{ij} = \frac{1}{2}(\partial \overline{u_i}/\partial x_j + \partial \overline{u_j}/\partial x_i)$ 成[线性关系](@entry_id:267880)：
$$
-\overline{u_i' u_j'} = 2 \nu_t S_{ij} - \frac{2}{3} k \delta_{ij}
$$
这里的关键在于确定[涡粘度](@entry_id:155814) $\nu_t$。为此，双方程模型引入了两个独立的[湍流](@entry_id:151300)特征量，并通过求解它们的输运方程来确定 $\nu_t$。最经典的组合是 **湍动能 (turbulent kinetic energy)** $k$ 和 **湍[动能耗散](@entry_id:751026)率 (dissipation rate of turbulent kinetic energy)** $\varepsilon$。

根据定义，单位质量的[湍动能](@entry_id:262712) $k$ 是速度脉动[方差](@entry_id:200758)的一半，它量化了[湍流](@entry_id:151300)脉动的强度 [@problem_id:3379844]：
$$
k \equiv \frac{1}{2} \overline{u_i' u_i'} = \frac{1}{2} (\overline{u'^2} + \overline{v'^2} + \overline{w'^2})
$$
而 $\varepsilon$ 则代表单位质量的[湍动能](@entry_id:262712)由于分子粘性作用转化为内能的速率。它与速度脉动的微小尺度梯度直接相关 [@problem_id:3379844]：
$$
\varepsilon \equiv \nu \overline{\frac{\partial u_i'}{\partial x_j} \frac{\partial u_i'}{\partial x_j}}
$$
其中 $\nu$ 是流体的运动粘度。一个等价的定义可以通过脉动[应变率张量](@entry_id:266108) $S'_{ij} = \frac{1}{2}(\partial u_i'/\partial x_j + \partial u_j'/\partial x_i)$ 给出，即 $\varepsilon = 2\nu \overline{S'_{ij} S'_{ij}}$。

这两个量的物理维度对于理解模型至关重要。$k$ 的维度是速度的平方，即 $[k] = L^2 T^{-2}$。$\varepsilon$ 的维度是能量耗散率除以质量，即 $[k]/[T] = L^2 T^{-3}$ [@problem_id:3379867]。基于 $k$ 和 $\varepsilon$ 这两个局部[湍流](@entry_id:151300)尺度，我们可以通过[量纲分析](@entry_id:140259)构建一个具有运动粘度维度 ($L^2 T^{-1}$) 的量。假设 $\nu_t \propto k^a \varepsilon^b$，我们有：
$$
L^2 T^{-1} = (L^2 T^{-2})^a (L^2 T^{-3})^b = L^{2a+2b} T^{-2a-3b}
$$
通过匹配 $L$ 和 $T$ 的指数，我们得到 $a=2$ 和 $b=-1$。因此，[涡粘度](@entry_id:155814)的基本形式为：
$$
\nu_t = C_\mu \frac{k^2}{\varepsilon}
$$
其中 $C_\mu$ 是一个无量纲的模型常数。这个关系式是所有 $k$–$\varepsilon$ 模型的核心，它将宏观的[涡粘度](@entry_id:155814)与两个可求解的[湍流](@entry_id:151300)特征量 $k$ 和 $\varepsilon$ 联系起来 [@problem_id:3379867]。

### $k$ 和 $\varepsilon$ 的输运方程

为了在流场中确定 $k$ 和 $\varepsilon$ 的值，模型提供了它们的[偏微分](@entry_id:194612)输运方程。这些方程的形式反映了物理上的[守恒定律](@entry_id:269268)，即某物理量的变化率等于其[扩散](@entry_id:141445)、产生和耗散的总和。$k$ 的精确[输运方程](@entry_id:756133)可以从纳维-斯托克斯方程导出，其模型化形式为：
$$
\frac{Dk}{Dt} = \nabla \cdot \left[ (\nu + \frac{\nu_t}{\sigma_k}) \nabla k \right] + P_k - \varepsilon
$$
而 $\varepsilon$ 的输运方程则更多地依赖于物理建模和[量纲分析](@entry_id:140259)，其标准形式为：
$$
\frac{D\varepsilon}{Dt} = \nabla \cdot \left[ (\nu + \frac{\nu_t}{\sigma_\varepsilon}) \nabla \varepsilon \right] + C_{\varepsilon 1} \frac{\varepsilon}{k} P_k - C_{\varepsilon 2} \frac{\varepsilon^2}{k}
$$
其中 $P_k = -\overline{u_i' u_j'} (\partial \overline{u_i}/\partial x_j)$ 是湍动能的产生项，它描述了平均流动通过应变作用将能量传递给[湍流](@entry_id:151300)脉动的过程。

通过对这些方程中的每一项进行[量纲分析](@entry_id:140259)，我们可以更深刻地理解它们的物理意义 [@problem_id:3379886]。对于 $k$ 方程，所有项 ($Dk/Dt$, $P_k$, $\varepsilon$ 以及[扩散](@entry_id:141445)项) 的维度均为 $L^2 T^{-3}$，即单位质量的能量变化率。对于 $\varepsilon$ 方程，所有项 ($D\varepsilon/Dt$, 产生项，耗散项以及[扩散](@entry_id:141445)项) 的维度均为 $L^2 T^{-4}$。这种[量纲一致性](@entry_id:271193)是任何物理上自洽的输运方程所必须满足的基本要求。

### RNG方法的理论根基

标准 $k$–$\varepsilon$ 模型的方程形式和常数主要基于经验和对简单流动的标定，这限制了其在[复杂流动](@entry_id:747569)中的普适性。相比之下，RNG $k$–$\varepsilon$ 模型源于一种更系统的理论方法——[重整化群理论](@entry_id:188484) [@problem_id:3379916]。

RNG方法的核心思想是 **尺度消除 (scale elimination)** 或 **粗粒化 (coarse-graining)** [@problem_id:3379906]。想象一下在傅里叶空间中观察[湍流](@entry_id:151300)，[湍流](@entry_id:151300)由不同尺度（或[波数](@entry_id:172452)）的涡构成。RNG方法通过系统地积分掉小尺度（高[波数](@entry_id:172452)）的脉动模态，来考察这些被消除的尺度对大尺度（低波数）流动的影响。当从纳维-斯托克斯方程中消除一个薄壳层的高波数模态时，它们对剩余低波数模态的作用表现为一个修正的、等效的粘性项。

对于三维[湍流](@entry_id:151300)，这个由小尺度脉动产生的等效粘性修正 $\Delta\nu$ 是正的。这意味着小[涡流](@entry_id:271366)总是耗散大涡流的能量，这与物理上能量从大尺度向小尺度串级的概念（正向[能量串级](@entry_id:153717)）相符。随着我们不断消除更小的尺度，这个等效粘性会不断累积，导致作用于最[大尺度流动](@entry_id:263652)的“[有效粘度](@entry_id:204056)” $\nu_{eff}$ 增加。RNG方法通过这一严谨的数学过程，推导出了一个依赖于尺度的[有效粘度](@entry_id:204056)，并最终形成了对 RANS 模型中[输运方程](@entry_id:756133)的系统性修正 [@problem_id:3379906]。

### RNG $k$–$\varepsilon$ 模型的关键机理

RNG理论为标准 $k$–$\varepsilon$ 模型带来了关键的修正，使其能够更好地响应平均应变率的影响，从而改善在[复杂流动](@entry_id:747569)（如强剪切、高曲率流动）中的预测能力。

#### 对平均[应变率](@entry_id:154778)的响应：$R_\varepsilon$ 项

RNG模型最显著的改进是在 $\varepsilon$ 输运方程中引入了一个额外的[源项](@entry_id:269111)，通常表示为 $R_\varepsilon$。标准模型中的 $\varepsilon$ 方程无法正确反映平均[应变率](@entry_id:154778)对耗散过程的影响，而 $R_\varepsilon$ 项恰恰弥补了这一缺陷。该项的形式通常写为：
$$
R_\varepsilon = \frac{C_\mu \eta^3 (1 - \eta/\eta_0)}{1 + \beta \eta^3} \frac{\varepsilon^2}{k}
$$
其中，$\eta = Sk/\varepsilon$ 是一个[无量纲参数](@entry_id:169335)，它代表了[湍流](@entry_id:151300)时间尺度 $\tau_t \sim k/\varepsilon$ 与平均应变时间尺度 $\tau_s \sim 1/S$ 的比值（$S = \sqrt{2S_{ij}S_{ij}}$ 是平均[应变率张量](@entry_id:266108)的模）。$\eta_0$ 和 $\beta$ 是从RNG理论推导出的常数（例如 $\eta_0 \approx 4.38$, $\beta \approx 0.012$）。

$R_\varepsilon$ 项的作用是双重的，这取决于 $\eta$ 的大小 [@problem_id:3379849]：
1.  **中[等应变](@entry_id:184570)率 ($0  \eta  \eta_0$)**：此时 $R_\varepsilon$ 为正，它在 $\varepsilon$ 方程中充当一个产生项。这会使得模型预测的 $\varepsilon$ 值增加。根据[涡粘度](@entry_id:155814)公式 $\nu_t = C_\mu k^2/\varepsilon$，$\varepsilon$ 的增加将导致[涡粘度](@entry_id:155814) $\nu_t$ 的减小。标准 $k$–$\varepsilon$ 模型在急剧应变的流动（如冲击射流、分离-再附流动）中往往会过度预测[湍动能](@entry_id:262712)，从而导致[涡粘度](@entry_id:155814)过大。RNG模型通过 $R_\varepsilon$ 项有效地抑制了[涡粘度](@entry_id:155814)，从而提高了对这类流动的预测精度 [@problem_id:3379912]。

2.  **高应变率 ($\eta > \eta_0$)**：此时 $R_\varepsilon$ 变为负值，在 $\varepsilon$ 方程中充当一个耗散项。这会减小 $\varepsilon$ 的值，从而相对地增大了[涡粘度](@entry_id:155814)。这一机制使得模型能够更好地处理具有极高应变率的流动区域。

让我们通过一个具体的例子来理解这一点。考虑一个平面混合层，流速差 $\Delta U = 18\,\mathrm{m/s}$，[动量厚度](@entry_id:150210) $\delta = 0.040\,\mathrm{m}$，测得的[湍动能](@entry_id:262712) $k = 0.020\,\mathrm{m^2\,s^{-2}}$，[耗散率](@entry_id:748577) $\varepsilon = 1.50\,\mathrm{m^2\,s^{-3}}$ [@problem_id:3379912]。我们可以估算平均[应变率](@entry_id:154778) $S \approx \Delta U / \delta = 450\,\mathrm{s^{-1}}$。因此，无量纲应变参数为：
$$
\eta = \frac{Sk}{\varepsilon} = \frac{(450)(0.020)}{1.50} = 6.0
$$
由于 $\eta = 6.0 > \eta_0 = 4.38$，此时 $R_\varepsilon$ 项为负值（计算可得其对每单位体积 $\varepsilon$ [源项](@entry_id:269111)的贡献约为 $-911\,\mathrm{kg \cdot m^{-1} \cdot s^{-4}}$），在 $\varepsilon$ 方程中起到耗散作用，从而降低 $\varepsilon$ 的预测值。

### 模型的应用背景与局限性

RNG $k$–$\varepsilon$ 模型因其理论上的优越性和对复杂应变流动的更佳表现，在许多工程应用中成为一个有吸[引力](@entry_id:175476)的选择。然而，理解其[适用范围](@entry_id:636189)和固有局限性至关重要。

#### 与其他主流模型的比较

在[RANS模型](@entry_id:754068)大家族中，RNG $k$–$\varepsilon$ 模型经常与另外两个高级模型进行比较：**Realizable $k$–$\varepsilon$ 模型** 和 **$k$–$\omega$ SST (Shear Stress Transport) 模型** [@problem_id:3379880]。

*   **壁面附近和[逆压梯度](@entry_id:276169)流动**：对于存在强[逆压梯度](@entry_id:276169)和[流动分离](@entry_id:143331)的[边界层](@entry_id:139416)流动，[SST模型](@entry_id:755302)通常是首选。[SST模型](@entry_id:755302)巧妙地融合了近壁区表现优异的 $k$–$\omega$ 模型和[远场](@entry_id:269288)鲁棒的 $k$–$\varepsilon$ 模型，并加入了应力限制器，使其对分离的预测更为准确。相比之下，RNG $k$–$\varepsilon$ 模型（和其他 $k$–$\varepsilon$ 模型一样）是为高雷诺数区域设计的，在壁面附近需要依赖壁函数或[低雷诺数](@entry_id:204816)修正，处理[分离流](@entry_id:754694)的能力相对较弱。

*   **强旋转和高曲率流动**：Realizable $k$–$\varepsilon$ 模型在这些方面表现突出。它的一个关键特征是 $C_\mu$ 不仅依赖于应变率，还依赖于旋转率张量，这使其能更精确地响应旋转和曲率效应。

*   **常规[高雷诺数流](@entry_id:199822)动**：对于附着[边界层](@entry_id:139416)等“行为良好”的流动，RNG和Realizable模型在使用壁函数时都能提供高效且足够准确的结果。在这种情况下，[SST模型](@entry_id:755302)需要解析近壁区的精细网格可能显得计算成本过高。

#### 根本性局限：各向同性涡粘性

尽管RNG模型在 $\varepsilon$ 方程和 $C_\mu$ 计算上进行了重要改进，但它仍未脱离[Boussinesq假设](@entry_id:272519)的框架。这个线性、各向同性的涡粘性假设是其最根本的局限性 [@problem_id:3379852]。该假设强制[雷诺应力张量](@entry_id:270803)的主轴与平均应变率张量的主轴对齐，并且无法正确描述法向雷诺应力的各向异性。

这一局限性导致RNG $k$–$\varepsilon$ 模型（以及所有线性涡粘性模型）在以下几类流动中表现不佳：

*   **强[旋流](@entry_id:153202)和弯曲[管道流](@entry_id:189531)**：这些流动由法向应力的各向异性驱动产生[二次流](@entry_id:754609)，而线性涡粘性模型无法捕捉这一现象。
*   **三维[边界层](@entry_id:139416)**：例如[后掠翼](@entry_id:272806)上的流动，其雷诺[应力与应变率](@entry_id:263123)之间存在显著的非对准，这是标量 $\nu_t$ 无法描述的。
*   **强非平衡流动**：如激波/[边界层](@entry_id:139416)相互作用、[流动分离](@entry_id:143331)等。在这些流动中，[湍流](@entry_id:151300)的“历史效应”非常重要，而[Boussinesq假设](@entry_id:272519)的局部性使其无法响应这种非平衡状态。

综上所述，RNG $k$–$\varepsilon$ 模型是标准 $k$–$\varepsilon$ 模型的一个重要理论发展，它通过引入对平均应变率的系统性响应，显著改善了对复杂剪切和[拉伸流](@entry_id:198535)动的预测能力。然而，使用者必须清醒地认识到，其作为一种涡粘性模型，在处理由雷诺应力各向异性主导的[复杂流动](@entry_id:747569)时，仍然存在固有的局限性。