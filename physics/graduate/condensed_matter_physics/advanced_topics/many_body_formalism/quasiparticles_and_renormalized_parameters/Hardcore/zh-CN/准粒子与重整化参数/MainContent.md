## 引言
在包含大量相互作用粒子的量子系统中，例如金属中的电子海洋，直接求解其行为是一个几乎不可能完成的任务。然而，物理学的一个深刻洞见是，尽管微观相互作用极其复杂，系统的低能行为却往往能被一个更简单的图像所描述。这个图像的核心就是“准粒子”——一种行为类似自由粒子、但其性质已被周围环境深刻改变的有效激发。准粒子的概念是整个近代凝聚态物理学的基石，它为我们理解从普通金属到奇异超导体等各种材料的性质提供了统一的语言。本文旨在系统地揭示准粒子的奥秘，解决“相互作用如何改变粒子行为”这一核心问题。

为实现这一目标，本文将分为三个循序渐进的部分。在“原理与机制”一章中，我们将从格林函数和自能等第一性原理工具出发，严谨地构建准粒子的理论框架，并阐明有效质量、准粒子权重等重整化参数的物理起源。接下来，在“应用与跨学科交叉”一章中，我们将展示这一理论框架如何与实验紧密结合，解释比热、磁化率、ARPES光谱等真实可测的物理量，并将其应用拓展到强关联体系、超导体和狄拉克材料等前沿领域。最后，“动手实践”部分提供了一系列计算问题，旨在帮助读者通过实际操作，加深对重整化思想和准粒子动力学的理解。通过这趟旅程，读者将掌握连接微观相互作用与宏观可观测量的关键理论工具。

## 原理与机制

在相互作用的多体费米子系统中，例如金属中的电子，单个粒子的行为由于与其他所有粒子持续的相互作用而变得极其复杂。直接求解包含所有相互作用的薛定谔方程通常是不可行的。然而，一个深刻的见解是，尽管相互作用很强，系统的低能激发谱仍然可能具有相对简单的结构。这些低能激发，而非裸露的电子本身，成为了描述系统热力学和输运性质的有效自由度。这些激发被称为**准粒子**（quasiparticles）。本章旨在从第一性原理出发，系统地阐述准粒子的概念、其由相互作用决定的重整化性质，以及描述其集体行为的现象学理论。

### 准粒子：从裸粒子到“穿衣”的激发

在没有相互作用的费米气体中，激发系统最简单的方式是从费米面以下（占据态）移走一个粒子，或在费米面以上（未占态）增加一个粒子。这些粒子-空穴激发是能量和动量都确定的、寿命无限长的本征态。当我们“绝热地”缓慢开启粒子间的相互作用时，一个核心问题是：这些简单的单粒子激发会发生什么？[@problem_id:3013287]

**绝热连续性原理**（principle of adiabatic continuity）为我们提供了概念上的指引。该原理假设，在不经历相变的前提下，相互作用系统的基态和低能激发态与非相互作用系统中的对应态之间存在一一对应关系。这意味着，一个裸露的、自由的电子在穿上由周围粒子云组成的“外衣”（dressing cloud）后，会转变为一个准粒子。这个准粒子仍然带有与原始粒子相同的量子数（如电荷和自旋），但其性质，如能量和质量，会被显著地**重整化**（renormalized）。

#### 格林函数与准粒子极点

描述这一转变的严谨数学工具是**单粒子格林函数**（single-particle Green's function），$G(\mathbf{k}, \omega)$。它描述了在系统中加入或移走一个动量为 $\mathbf{k}$、能量为 $\omega$ 的粒子的传播子。对于相互作用系统，格林函数可以通过戴森方程（Dyson's equation）与**自能**（self-energy）$\Sigma(\mathbf{k}, \omega)$ 联系起来。对于一个延迟格林函数 $G^R(\mathbf{k}, \omega)$，其形式为：
$$
G^R(\mathbf{k},\omega)=\frac{1}{\omega-\epsilon_{\mathbf{k}}-\Sigma^R(\mathbf{k},\omega)}
$$
其中 $\epsilon_{\mathbf{k}}$ 是裸粒子的色散关系（能量相对于化学势 $\mu$）。自能 $\Sigma^R(\mathbf{k}, \omega)$ 是一个复函数，包含了所有相互作用的复杂效应。

一个寿命无限长的粒子对应于格林函数在实轴上的一个极点。在相互作用系统中，一个稳定的或长寿命的准粒子对应于 $G^R(\mathbf{k}, \omega)$ 在复频率平面上靠近实轴的一个极点 [@problem_id:3013236]。如果我们将自能 $\Sigma^R = \mathrm{Re}\Sigma^R + i\mathrm{Im}\Sigma^R$ 分为实部和虚部，这个极点的位置 $\omega_p = E^*_{\mathbf{k}} - i\Gamma_{\mathbf{k}}$ 由方程 $\omega_p - \epsilon_{\mathbf{k}} - \Sigma^R(\mathbf{k}, \omega_p) = 0$ 决定。在准粒子图像成立的情况下，$\mathrm{Im}\Sigma^R$ 很小，我们可以近似求解：

*   **准粒子能量** $E^*_{\mathbf{k}}$ 由方程的实部决定：$E^*_{\mathbf{k}} - \epsilon_{\mathbf{k}} - \mathrm{Re}\Sigma^R(\mathbf{k}, E^*_{\mathbf{k}}) = 0$。这表明相互作用通过自能的实部使裸粒子能量 $\epsilon_{\mathbf{k}}$ 发生了移动，从而定义了重整化的准粒子色散。

*   **准粒子衰变率** $\Gamma_{\mathbf{k}}$ 与自能的虚部有关。它代表了准粒子由于与其他激发相互作用而衰变的可能性，其寿命为 $\tau_{\mathbf{k}} \propto 1/\Gamma_{\mathbf{k}}$。

需要强调的是，准粒子与**集体模式**（collective modes）有着本质区别。准粒子是单粒子谱的特征，对应于 $G^R$ 的极点。而集体模式，如等离激元（plasmons）或零声（zero sound），是系统中粒子-空穴对的相干叠加，表现为密度-密度等两体关联函数的极点 [@problem_id:3013236]。

### 准粒子的性质：自能的角色

格林函数在准粒子极点 $\omega \approx E^*_{\mathbf{k}}$ 附近的行为，揭示了准粒子的核心性质。通过在 $E^*_{\mathbf{k}}$ 附近对戴森方程的分母进行泰勒展开，我们可以得到格林函数的近似形式 [@problem_id:3013283]：
$$
G^R(\mathbf{k},\omega) \approx \frac{Z_{\mathbf{k}}}{\omega - E^*_{\mathbf{k}} + i\Gamma_{\mathbf{k}}}
$$
这个表达式中出现了两个关键的重整化参数：准粒子权重 $Z_{\mathbf{k}}$ 和衰变率 $\Gamma_{\mathbf{k}}$。

#### 准粒子权重 $Z$

**准粒子权重**（quasiparticle residue），或称为**重整化因子** $Z_{\mathbf{k}}$，由下式给出：
$$
Z_{\mathbf{k}} = \left( 1 - \left.\frac{\partial \mathrm{Re}\Sigma^R(\mathbf{k},\omega)}{\partial\omega}\right|_{\omega=E^*_{\mathbf{k}}} \right)^{-1}
$$
$Z_{\mathbf{k}}$ 的值在 $0$ 和 $1$ 之间（$0  Z_{\mathbf{k}} \le 1$）。$Z_{\mathbf{k}}=1$ 对应于无相互作用的情况。当相互作用开启时，$Z_{\mathbf{k}}  1$。从物理上看，$Z_{\mathbf{k}}$ 度量了准粒子激发中“裸粒子”的成分。它可以被严谨地证明等于单粒子态 $c_{\mathbf{k}}^{\dagger}|\Psi_0^N\rangle$（在 $N$ 粒子基态 $|\Psi_0^N\rangle$ 上创建一个裸粒子）与真实的 $(N+1)$ 粒子系统最低能级本征态 $|\Psi_{\mathbf{k}}^{N+1}\rangle$（即单准粒子态）之间的交叠的模方：$Z_{\mathbf{k}} = |\langle\Psi_{\mathbf{k}}^{N+1}|c_{\mathbf{k}}^{\dagger}|\Psi_0^N\rangle|^2$ [@problem_id:3013284]。相互作用将部分裸粒子的谱权重转移到了更复杂的、非相干的多粒子-空穴激发中，形成了所谓的“非相干背景”（incoherent background），从而使得 $Z_{\mathbf{k}}  1$。

#### 寿命、谱函数与费米液体判据

**谱函数**（spectral function）$A(\mathbf{k}, \omega) = -\frac{1}{\pi}\mathrm{Im}G^R(\mathbf{k}, \omega)$ 是一个可以直接通过角分辨光电子能谱（ARPES）等实验手段测量的量。它给出了在系统中以能量 $\omega$ 移走一个动量为 $\mathbf{k}$ 的电子的概率。对于一个具有良好定义的准粒子，其谱函数在 $E^*_{\mathbf{k}}$ 附近呈现为一个尖锐的洛伦兹峰 [@problem_id:3013283]：
$$
A(\mathbf{k},\omega) \approx \frac{Z_{\mathbf{k}}}{\pi} \frac{\Gamma_{\mathbf{k}}}{(\omega - E^*_{\mathbf{k}})^2 + \Gamma_{\mathbf{k}}^2}
$$
这个洛伦兹峰的积分面积恰好等于准粒子权重 $Z_{\mathbf{k}}$，而其半高全宽（HWHM）就是衰变率 $\Gamma_{\mathbf{k}}$。衰变率与自能虚部的关系为 $\Gamma_{\mathbf{k}} = -Z_{\mathbf{k}}\mathrm{Im}\Sigma^R(\mathbf{k}, E^*_{\mathbf{k}})$。准粒子的寿命 $\tau_{\mathbf{k}}$ 与衰变率成反比，$\tau_{\mathbf{k}} = \hbar/\Gamma_{\mathbf{k}}$。

朗道费米液体理论的核心在于，靠近费米面的准粒子寿命极长。在零温下，一个能量为 $E^*_{\mathbf{k}}$ 的准粒子衰变的主要途径是产生其他粒子-空穴对。对于三维短程相互作用，相空间分析表明，其衰变率与能量的平方成正比，即 $\Gamma_{\mathbf{k}} \propto (E^*_{\mathbf{k}} - \mu)^2$。这意味着，当准粒子能量趋近于费米能 $\mu$ 时，其衰变率比能量本身更快地趋于零 ($\Gamma_{\mathbf{k}}/|E^*_{\mathbf{k}}-\mu| \to 0$) [@problem_id:3013255]。这保证了费米面上的准粒子是无限长寿命的、定义良好的激发，这是费米液体图像得以成立的根本原因 [@problem_id:3013287]。

### 重整化参数与现象学理论

准粒子概念的强大之处在于，它允许我们建立一个描述低能物理的有效理论——朗道费米液体理论。该理论将复杂的微观相互作用打包到少数几个现象学参数中。

#### 有效质量与动量分布

相互作用不仅移动了能量，还改变了准粒子的动力学。准粒子的群速度由其重整化色散决定：$\mathbf{v}^*_{\mathbf{k}} = \nabla_{\mathbf{k}} E^*_{\mathbf{k}}$。这定义了**有效质量** $m^*$。一个常见的误解是认为有效质量仅仅由权重因子决定，即 $m^*/m = 1/Z_{\mathbf{k}}$。这是不完整的。完整的关系式依赖于自能对动量的导数 [@problem_id:3013284]：
$$
\frac{m}{m^*} = Z_{\mathbf{k}_F} \left( 1 + \frac{m}{k_F} \left.\frac{\partial \mathrm{Re}\Sigma^R(k,0)}{\partial k}\right|_{k=k_F} \right)
$$
只有当自能与动量无关时，简化的关系 $m/m^* = Z_{\mathbf{k}_F}$ 才成立。

另一个相互作用的直接后果体现在**动量分布函数** $n(\mathbf{k})$ 上。在零温下的无相互作用费米气体中，$n(\mathbf{k})$ 在费米面 $k_F$ 处有一个从1到0的阶跃。在相互作用的费米液体中，这个阶跃仍然存在，但其高度被减小到恰好等于准粒子权重 $Z_{\mathbf{k}_F}$ [@problem_id:3013284]。这个结论，即**卢廷格定理**（Luttinger's theorem）的一个推论，表明费米面的体积（一个尖锐的特征）在相互作用下保持不变，这深刻地反映了粒子数守恒。

#### 朗道相互作用函数

朗道理论进一步假设，总能量是准粒子分布函数 $n_{\mathbf{k}\sigma}$ 的一个泛函。对于偏离平衡分布的小扰动 $\delta n_{\mathbf{k}\sigma}$，能量的变化可以展开为：
$$
\delta E = \sum_{\mathbf{k}\sigma} E^*_{\mathbf{k}\sigma} \delta n_{\mathbf{k}\sigma} + \frac{1}{2V} \sum_{\mathbf{k}\sigma, \mathbf{k}'\sigma'} f_{\mathbf{k}\sigma, \mathbf{k}'\sigma'} \delta n_{\mathbf{k}\sigma} \delta n_{\mathbf{k}'\sigma'}
$$
这里的 $f_{\mathbf{k}\sigma, \mathbf{k}'\sigma'}$ 是**朗道相互作用函数**，它描述了两个准粒子之间的剩余有效相互作用。从物理上，它对应于两个位于费米面上的准粒子之间零能动量交换的**前向散射振幅**（forward-scattering amplitude）[@problem_id:3013240]。这个函数是能量泛函的二阶泛函导数，因此它必须是对称的：$f_{\mathbf{k}\sigma, \mathbf{k}'\sigma'} = f_{\mathbf{k}'\sigma', \mathbf{k}\sigma}$ [@problem_id:3013240]。

对于各向同性系统，该函数只依赖于动量 $\mathbf{k}$ 和 $\mathbf{k}'$ 之间的夹角 $\theta$ 以及自旋。它可以被分解为自旋对称 ($f^s$) 和自旋反对称 ($f^a$) 两部分，并展开为勒让德多项式 [@problem_id:3013272]：
$$
f_{\sigma\sigma'}(\theta) = \sum_{l=0}^\infty \left( f_l^s + f_l^a \boldsymbol{\sigma} \cdot \boldsymbol{\sigma}' \right) P_l(\cos\theta)
$$
通过乘以态密度 $N(0)$，可以得到无量纲的**朗道参数** $F_l^s = N(0)f_l^s$ 和 $F_l^a = N(0)f_l^a$。这些参数直接与宏观可观测量相联系：

*   **压缩率** $\kappa$ 由 $F_0^s$ 决定：$\kappa/\kappa_{free} \propto (1+F_0^s)^{-1}$。
*   **自旋磁化率** $\chi$ 由 $F_0^a$ 决定：$\chi/\chi_{Pauli} \propto (1+F_0^a)^{-1}$。
*   在**伽利略不变系统**（如液氦-3）中，有效质量与 $F_1^s$ 有着精确的关系：$m^*/m = 1 + F_1^s/3$ [@problem_id:3013240] [@problem_id:3013272]。

此外，费米液体的稳定性要求满足**波梅兰丘克不等式**（Pomeranchuk inequalities）：$1 + F_l^{s,a}/(2l+1)  0$ [@problem_id:3013272]。

### 准粒子图像的动力学与失效

#### 朗道动力学方程

朗道理论的范畴还可以扩展到动力学。准粒子[分布函数](@entry_id:145626) $n_{\mathbf{k}}(\mathbf{r}, t)$ 的演化由一个半经典的**朗道动力学方程**（或称玻尔兹曼-朗道方程）描述 [@problem_id:3013218]：
$$
\frac{\partial n_{\mathbf{k}}}{\partial t} + \nabla_{\mathbf{k}} \varepsilon_{\mathbf{k}} \cdot \nabla_{\mathbf{r}} n_{\mathbf{k}} - \nabla_{\mathbf{r}} \varepsilon_{\mathbf{k}} \cdot \nabla_{\mathbf{k}} n_{\mathbf{k}} = I_{\mathrm{coll}}[n]
$$
其中，$\varepsilon_{\mathbf{k}}(\mathbf{r},t) = E^*_{\mathbf{k}} + U_{\mathrm{ext}} + \sum_{\mathbf{k}'} f_{\mathbf{k}\mathbf{k}'} \delta n_{\mathbf{k}'}$ 是包含外场和朗道平均场效应的总能量。该方程左边的三项分别代表：分布的局域时间演化、由重整化速度 $\mathbf{v}^*_{\mathbf{k}} = \nabla_{\mathbf{k}}\varepsilon_{\mathbf{k}}$ 引起的实空间漂移、以及由总能量的空间梯度（力）引起的动量空间加速。右边的**碰撞积分** $I_{\mathrm{coll}}[n]$ 描述了准粒子间的散射，它驱动系统趋向局域平衡。这个方程是连接微观准粒子性质与宏观输运现象（如电导率、热导率）的桥梁。

#### 费米液体的稳定性与失效

费米液体是一个非常稳固的物态，但它并非无条件存在。从**重整化群**（Renormalization Group, RG）的角度看，描述朗道参数的前向散射相互作用在RG流中是**边缘的**（marginal），意味着它们在低能下不会增长从而破坏费米液体结构 [@problem_id:3013258]。然而，其他类型的相互作用，例如吸引相互作用下的**BCS（库珀）散射通道**，同样是边缘的，但它会导致RG流发散，引发向超导态的相变。这代表了费米液体的一种失稳，但会进入另一种有序的、仍然有准粒子（所谓Bogoliubov准粒子）的基态。

真正的准粒子图像的崩溃，即**非费米液体**（non-Fermi liquid）的形成，发生在更极端的情况下。一个非费米液体态的标志是尖锐准粒子峰的消失 [@problem_id:3013255]。这可以通过两个关键判据来识别：
1.  **准粒子权重消失**：$Z_{\mathbf{k}_F} \to 0$。这意味着单粒子激发与任何长寿命的准稳态都没有交叠。
2.  **衰变率过大**：即使 $Z  0$，如果衰变率与能量成正比或更慢地减小，即 $\lim_{\omega\to 0} |\mathrm{Im}\Sigma^R(\omega)|/|\omega| \neq 0$，那么准粒子峰的宽度与能量相当，激发在衰变之前甚至无法完成一次振荡，从而失去其作为粒子的意义。

一个典型的例子是**莫特绝缘体**（Mott insulator）。在半满填充的哈伯德模型中，强烈的在位库仑排斥 $U$ 使得电子局域化并打开能隙，即使能带理论预言其为金属。在这种状态下，单粒子谱中没有低能激发，准粒子权重 $Z$ 严格为零 [@problem_id:3013268]。准粒子图像完全失效。有趣的是，即使在这种情况下，卢廷格定理的精髓依然得以保留。原本由格林函数极点定义的费米面，被一个由格林函数零点定义的“卢廷格面”所取代，即 $G^R(\mathbf{k}, \omega=0)=0$ 的动量曲面。这个曲面所包围的体积仍然由粒子数决定，这展示了物理学基本守恒律的深刻性和普适性 [@problem_id:3013268]。