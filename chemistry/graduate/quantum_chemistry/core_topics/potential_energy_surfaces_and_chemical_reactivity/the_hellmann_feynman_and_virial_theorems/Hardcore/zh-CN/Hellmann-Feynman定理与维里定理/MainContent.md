## 引言
在量子化学的宏伟理论框架中，海尔曼-费曼（Hellmann-Feynman）定理与维里（Virial）定理是两块熠熠生辉的基石。它们不仅以其数学上的优雅著称，更重要的是，它们在理论与计算之间架起了一座至关重要的桥梁，使我们能够从体系的总能量这一宏观量出发，深刻洞察其内部的微观物理性质。然而，如何精确地将能量对外部参数（如原子核位置、外场强度）的响应与波函数所描述的微观世界中的力、偶极矩等期望值联系起来，同时又如何理解一个稳定体系内部动能与势能之间的精妙平衡，构成了量子化学中的一个核心问题。本文旨在系统性地解决这一问题，为读者提供对这两个定理的全面理解。

在接下来的内容中，我们将分三个章节展开深入的探索。第一章“原理与机制”将从第一性原理出发，详细推导这两个定理，并剖析其成立的严格条件与在近似方法中遇到的挑战，如普莱力（Pulay force）的概念。第二章“应用与跨学科联系”将通过丰富的实例，展示这些定理如何被应用于计算分子性质、解释光谱数据，甚至在凝聚态物理和材料科学等交叉学科中发挥作用。最后，在“动手实践”部分，我们将通过一系列精心设计的计算问题，引导读者亲手应用这些定理，将抽象的理论转化为解决实际问题的能力。通过这一结构化的学习路径，读者将不仅掌握这两个定理的理论精髓，更能领会它们在现代科学研究中的强大威力。

## 原理与机制

本章旨在深入探讨量子化学中两个至关重要的定理：海尔曼-费曼（Hellmann-Feynman）定理和维里（Virial）定理。我们将从第一性原理出发，系统地阐述它们的数学形式、物理内涵、适用条件以及在现代量子化学计算中的实际应用与局限性。这些定理不仅为计算分子性质提供了优雅的理论框架，也为诊断和理解近似计算方法的准确性提供了深刻的洞见。

### 海尔曼-费曼定理：基本原理

海尔曼-费曼（HFT）定理是连接一个量子体系能量对其哈密顿算符中参数的响应与该参数对哈密顿算符导数期望值之间关系的一座核心桥梁。它在计算化学中被广泛用于计算分子力、电偶极矩、极化率等一阶性质。

#### 精确本征态的推导

考虑一个依赖于某个平滑实参数 $\lambda$ 的厄米哈密顿算符 $H(\lambda)$。设 $|\psi(\lambda)\rangle$ 是其归一化的精确本征态，对应的本征值为 $E(\lambda)$，满足定态薛定谔方程：
$$
H(\lambda)|\psi(\lambda)\rangle = E(\lambda)|\psi(\lambda)\rangle
$$
并且归一化条件为 $\langle\psi(\lambda)|\psi(\lambda)\rangle = 1$。能量本征值可以表示为哈密顿算符的期望值：
$$
E(\lambda) = \langle\psi(\lambda)|H(\lambda)|\psi(\lambda)\rangle
$$
为了探究能量如何随参数 $\lambda$ 变化，我们计算其全导数。根据乘积法则，我们得到：
$$
\frac{\mathrm{d}E(\lambda)}{\mathrm{d}\lambda} = \left\langle \frac{\mathrm{d}\psi(\lambda)}{\mathrm{d}\lambda} \middle| H(\lambda) \middle| \psi(\lambda) \right\rangle + \left\langle \psi(\lambda) \middle| \frac{\partial H(\lambda)}{\partial \lambda} \middle| \psi(\lambda) \right\rangle + \left\langle \psi(\lambda) \middle| H(\lambda) \middle| \frac{\mathrm{d}\psi(\lambda)}{\mathrm{d}\lambda} \right\rangle
$$
这个表达式包含了三项：两项涉及波函数对参数的响应（波函数导数项），以及一项涉及哈密顿算符本身的显式变化。海尔曼-费曼定理的精髓在于，对于精确本征态，前述的波函数导数项会精确地抵消。

利用薛定谔方程及其厄米共轭形式 $\langle\psi(\lambda)|H(\lambda) = E(\lambda)\langle\psi(\lambda)|$，我们可以简化第一项和第三项：
$$
\left\langle \frac{\mathrm{d}\psi}{\mathrm{d}\lambda} \middle| H \middle| \psi \right\rangle = E(\lambda) \left\langle \frac{\mathrm{d}\psi}{\mathrm{d}\lambda} \middle| \psi \right\rangle
$$
$$
\left\langle \psi \middle| H \middle| \frac{\mathrm{d}\psi}{\mathrm{d}\lambda} \right\rangle = E(\lambda) \left\langle \psi \middle| \frac{\mathrm{d}\psi}{\mathrm{d}\lambda} \right\rangle
$$
将它们代入能量导数的表达式中，得到：
$$
\frac{\mathrm{d}E}{\mathrm{d}\lambda} = \left\langle \psi \middle| \frac{\partial H}{\partial \lambda} \middle| \psi \right\rangle + E(\lambda) \left( \left\langle \frac{\mathrm{d}\psi}{\mathrm{d}\lambda} \middle| \psi \right\rangle + \left\langle \psi \middle| \frac{\mathrm{d}\psi}{\mathrm{d}\lambda} \right\rangle \right)
$$
括号中的项正是归一化条件 $\langle\psi(\lambda)|\psi(\lambda)\rangle = 1$ 对 $\lambda$ 的导数。由于归一化常数恒为1，其导数必为零：
$$
\frac{\mathrm{d}}{\mathrm{d}\lambda}\langle\psi(\lambda)|\psi(\lambda)\rangle = \left\langle \frac{\mathrm{d}\psi}{\mathrm{d}\lambda} \middle| \psi \right\rangle + \left\langle \psi \middle| \frac{\mathrm{d}\psi}{\mathrm{d}\lambda} \right\rangle = 0
$$
因此，波函数响应项的贡献恰好为零。我们最终得到了海尔曼-费曼定理的标准形式 [@problem_id:2930749] [@problem_id:2930790]：
$$
\frac{\mathrm{d}E(\lambda)}{\mathrm{d}\lambda} = \left\langle \psi(\lambda) \middle| \frac{\partial H(\lambda)}{\partial \lambda} \middle| \psi(\lambda) \right\rangle
$$
此定理表明，能量本征值对参数的全导数，等于哈密顿算符对该参数的偏导数在相应本征态下的期望值。值得注意的是，如果 $|\psi(\lambda)\rangle$ 不是 $H(\lambda)$ 的本征态，上述推导中的能量因子 $E(\lambda)$ 无法被提出，波函数响应项一般不会抵消，定理也就不成立。

#### 全导数与偏导数的辨析

在理解海尔曼-费曼定理时，区分能量 $E$ 的全导数 $\mathrm{d}E/\mathrm{d}\lambda$ 和偏导数 $\partial E/\partial\lambda$至关重要 [@problem_id:2930751]。我们可以将能量视为一个泛函 $E[\psi, \lambda] = \langle\psi|H(\lambda)|\psi\rangle / \langle\psi|\psi\rangle$。对于沿本征态路径 $|\psi(\lambda)\rangle$ 的能量 $E(\lambda) = E[\psi(\lambda), \lambda]$，其全导数根据链式法则应包含两部分：一部分是由于哈密顿算符 $H$ 对 $\lambda$ 的显式依赖（偏导数），另一部分是由于波函数 $|\psi\rangle$ 本身也随 $\lambda$ 变化而产生的隐式依赖。

然而，变分原理告诉我们，精确本征态是能量泛函的驻点。这意味着能量泛函对于波函数的一阶微小变分（在保持归一化的前提下）为零。由于 $|\psi(\lambda)\rangle$ 到 $|\psi(\lambda + \mathrm{d}\lambda)\rangle$ 的变化可以视为一种变分，因此在计算 $\mathrm{d}E/\mathrm{d}\lambda$ 时，由波函数变化所引起的项（泛函导数项）在一阶近似下为零。这正是波函数导数项在海尔曼-费曼定理推导中消失的深层原因。因此，对于精确本征态，能量的全导数等于其对参数的偏导数：
$$
\frac{\mathrm{d}E(\lambda)}{\mathrm{d}\lambda} = \left( \frac{\partial E[\psi, \lambda]}{\partial \lambda} \right)_{\psi=|\psi(\lambda)\rangle} = \left\langle \psi(\lambda) \middle| \frac{\partial H(\lambda)}{\partial \lambda} \middle| \psi(\lambda) \right\rangle
$$
这个等式深刻地揭示了海尔曼-费曼定理与变分原理之间的内在联系。

#### 数学严谨性：定理的有效条件

为了使上述推导在数学上严格成立，需要满足一系列正则性条件 [@problem_id:2930782]。首先，$H(\lambda)$ 必须是定义在一个与 $\lambda$ 无关的稠密域上的自伴算符，并且作为 $\lambda$ 的函数至少是一次连续可微的（$C^1$），这样其导数 $\partial H/\partial \lambda$ 才有明确定义。其次，所考虑的本征值 $E(\lambda)$ 在感兴趣的参数区间 $I$ 内必须是孤立且非简并的。这意味着它与其他能级之间存在一个非零的能隙，并且没有发生能级交叉。根据Kato的微扰理论，这些条件保证了可以选取一个同样是 $C^1$ 的归一化本征矢 $|\psi(\lambda)\rangle$。在这些条件下，海尔曼-费曼定理的标准形式才得以严格保证。

### 量子化学中的推广与应用

尽管海尔曼-费曼定理的原始形式要求精确的本征态，但其思想可以推广到量子化学中广泛使用的近似变分方法，这极大地扩展了它的实用价值。

#### 变分波函数的广义海尔曼-费曼定理

在Hartree-Fock（HF）或多组态自洽场（MCSCF）等变分方法中，我们通过最小化能量泛函来优化一组波函数参数（例如，分子轨道系数 $c_i$）。设 $|\Phi(\lambda)\rangle$ 是一个通过变分优化的归一化近似波函数。能量 $E_{\mathrm{var}}(\lambda) = \langle\Phi(\lambda)|H(\lambda)|\Phi(\lambda)\rangle$ 对 $\lambda$ 的全导数可以写作：
$$
\frac{\mathrm{d}E_{\mathrm{var}}}{\mathrm{d}\lambda} = \frac{\partial E_{\mathrm{var}}}{\partial \lambda} + \sum_i \frac{\partial E_{\mathrm{var}}}{\partial c_i} \frac{\mathrm{d} c_i}{\mathrm{d}\lambda}
$$
由于波函数是变分优化的，能量对于所有变分参数的一阶导数均为零，即 $\partial E_{\mathrm{var}}/\partial c_i = 0$。因此，包含参数响应 $\mathrm{d}c_i/\mathrm{d}\lambda$ 的项全部消失。这导致了一个广义的海尔曼-费曼定理 [@problem_id:2930749] [@problem_id:2930790]：
$$
\frac{\mathrm{d}E_{\mathrm{var}}(\lambda)}{\mathrm{d}\lambda} = \frac{\partial E_{\mathrm{var}}}{\partial \lambda} = \left\langle \Phi(\lambda) \middle| \frac{\partial H(\lambda)}{\partial \lambda} \middle| \Phi(\lambda) \right\rangle
$$
这个结论非常强大，它意味着只要波函数是完全变分优化的，我们就可以像处理精确本征态一样，通过计算一个简单的期望值来得到能量的导数，而无需计算波函数参数对微扰的复杂响应。

#### 参数依赖基组的问题：普莱力

然而，上述广义定理有一个重要的隐藏假设：用于展开波函数的基函数本身不依赖于参数 $\lambda$。在许多实际的量子化学计算中，这个假设并不成立。一个典型的例子是计算原子核上的力，此时参数 $\lambda$ 是原子核坐标 $\mathbf{R}$。通常使用的原子中心基组（如高斯基组）会随着原子核一起移动，这意味着基函数 $\chi_\mu$ 显式地依赖于 $\mathbf{R}$。

当基函数依赖于 $\lambda$ 时，波函数 $|\Phi(\lambda)\rangle$ 除了通过变分系数 $c_i(\lambda)$ 依赖于 $\lambda$ 外，还通过基函数 $\chi_\mu(\lambda)$ 显式地依赖于 $\lambda$。能量的全导数表达式中会出现额外的项，这些项源于基函数的导数，并且通常不为零。这些额外的贡献被称为 **普莱力（Pulay forces）** 或普莱项 [@problem_id:2930751] [@problem_id:2930779]。总的力（能量梯度）表达式变为：
$$
\mathbf{F} = -\frac{\mathrm{d}E}{\mathrm{d}\mathbf{R}} = -\left\langle \Phi \middle| \frac{\partial H}{\partial \mathbf{R}} \middle| \Phi \right\rangle + \mathbf{F}_{\text{Pulay}}
$$
其中第一项是海尔曼-费曼力，第二项就是普莱力。普莱力的出现是因为有限基组下的变分波函数并非哈密顿量的精确本征态，能量对于基函数位置的“变分”并不满足驻点条件。

#### 作为诊断工具的普莱力

普莱力的存在虽然给力的计算带来了复杂性，但也提供了一个有用的诊断工具。普莱项的根源在于基组的不完备性。在一个完备的、不随参数变化的基组中，任何波函数及其导数都可以被精确展开，此时普莱力会自然消失，因为近似波函数会收敛于精确本征态。因此，在实际计算中，普莱力的大小直接反映了所用基组在描述原子核位移响应方面的不足 [@problem_id:2930779]。一个计算中如果普莱力贡献很大，则表明为了获得可靠的几何结构或振动频率，需要使用更大的或更合适的基组。

#### 超越定态：轨道弛豫与响应理论

在某些高级的后-HF相关方法中（如Møller-Plesset微扰理论或截断的组态相互作用），能量并非对所有波函数参数（特别是分子轨道）都是变分最小化的。例如，在MP2能量计算中，所用的轨道是从底层的HF计算中获得的，它们使HF能量最小化，但不一定使MP2能量最小化。

在这种情况下，能量泛函对于某些参数（如轨道旋转参数 $\boldsymbol{\kappa}$）的导数 $\partial E/\partial \boldsymbol{\kappa}$ 不为零。因此，在计算总能量导数 $\mathrm{d}E/\mathrm{d}\lambda$ 时，来自这些非定态参数响应的贡献 $\frac{\partial E}{\partial \boldsymbol{\kappa}} \frac{\mathrm{d}\boldsymbol{\kappa}}{\mathrm{d}\lambda}$ 就不能忽略。这些“轨道弛豫”项必须被计算在内，通常需要求解所谓的“耦合微扰”（coupled-perturbed）方程（如CPHF）来得到响应项 $\mathrm{d}\boldsymbol{\kappa}/\mathrm{d}\lambda$。或者，可以使用Z-向量（Z-vector）方法，它通过引入一个拉格朗日乘子，巧妙地避免了直接求解响应方程，但仍能正确地包含弛豫效应的贡献 [@problem_id:2930740]。

### 维里定理：标度不变性的推论

维里定理是另一个深刻的物理原理，它揭示了在一个稳定束缚体系中，动能和势能的期望值之间存在的确定关系。对于一个由齐次函数势描述的体系，该关系尤为简洁。

#### 从标度变换论证推导

考虑一个由哈密顿量 $H = T+V$ 描述的体系，其精确归一化基态波函数为 $\psi$。我们可以构造一个经过标度变换的、归一化的试探波函数 $\psi_s(\mathbf{r}) = s^{3N/2}\psi(s\mathbf{r})$，其中 $s$ 是一个正的标度因子，$N$ 是粒子数。该试探波函数的能量期望值为 $E(s) = \langle\psi_s|T+V|\psi_s\rangle$。

通过在积分中进行变量替换，可以证明动能和势能算符的期望值如何随 $s$ 标度变换。动能算符 $T$ 包含二阶空间导数（如 $\nabla^2$），因此 $\langle T \rangle$ 与长度的平方成反比，即 $\langle\psi_s|T|\psi_s\rangle = s^2 \langle\psi|T|\psi\rangle$。如果势能 $V$ 是坐标的 $k$ 次齐次函数（即 $V(s\mathbf{r}_1, \dots) = s^k V(\mathbf{r}_1, \dots)$），则其期望值 $\langle V \rangle$ 的标度关系为 $\langle\psi_s|V|\psi_s\rangle = s^{-k} \langle\psi|V|\psi\rangle$。对于量子化学中最重要的库仑势，$V \propto 1/r$，其齐次性为 $k=-1$。

因此，对于库仑体系，标度变换后的能量为：
$$
E(s) = s^2 \langle T \rangle + s \langle V \rangle
$$
由于 $\psi$ 是精确的基态波函数，根据变分原理，能量 $E(s)$ 在 $s=1$ 处必须是驻点，即 $\mathrm{d}E(s)/\mathrm{d}s|_{s=1} = 0$。对 $E(s)$ 求导可得：
$$
\frac{\mathrm{d}E(s)}{\mathrm{d}s} = 2s \langle T \rangle + \langle V \rangle
$$
在 $s=1$ 处取值为零，便得到了库仑体系的维里定理 [@problem_id:2930790]：
$$
2\langle T \rangle + \langle V \rangle = 0
$$
或写为 $2\langle T \rangle = -\langle V \rangle$。这个关系对于任何库仑体系（原子、分子）的精确定态都成立。

#### 基于算符的推导：与海尔曼-费曼定理的联系

维里定理的另一个更具启发性的推导是基于标度变换的生成元，即所谓的“膨胀算符” $D = \frac{1}{2}\sum_i (\mathbf{r}_i \cdot \mathbf{p}_i + \mathbf{p}_i \cdot \mathbf{r}_i)$。对于任何一个定态 $|\psi\rangle$，任何不显含时间的算符 $A$ 的期望值的时间导数为零，这意味着 $\langle[H, A]\rangle = 0$。选择 $A=D$，我们有 $\langle[H, D]\rangle = 0$。

通过计算易位子 $[H, D] = [T, D] + [V, D]$，可以得到 $2\langle T \rangle = \langle \sum_i \mathbf{r}_i \cdot \nabla_i V \rangle$。对于 $k$ 次齐次势，欧拉定理给出 $\sum_i \mathbf{r}_i \cdot \nabla_i V = k V$，于是我们再次得到 $2\langle T \rangle = k \langle V \rangle$。

这两种推导方法实际上是等价的 [@problem_id:2930736]。我们可以将标度变换视为由膨胀算符 $D$ 生成的一个酉变换群 $U(\alpha) = \exp(-i\alpha D/\hbar)$ 的作用。变换后的哈密顿量为 $H(\alpha) = U(\alpha) H U(\alpha)^{-1}$。由于 $H(\alpha)$ 与 $H$ 是酉等价的，它们的本征谱相同，因此任何本征值 $E(\alpha)$ 都不依赖于 $\alpha$，即 $\mathrm{d}E/\mathrm{d}\alpha = 0$。

应用海尔曼-费曼定理，我们有：
$$
\frac{\mathrm{d}E}{\mathrm{d}\alpha} = \left\langle \psi \middle| \frac{\partial H(\alpha)}{\partial \alpha} \middle|_{\alpha=0} \middle| \psi \right\rangle = 0
$$
一个关键的算符恒等式是 $\left( \frac{\partial H(\alpha)}{\partial \alpha} \right)_{\alpha=0} = -\frac{i}{\hbar}[D, H]$。因此，海尔曼-费曼定理直接给出了 $\langle [D, H] \rangle = 0$，这正是易位子推导法的出发点。这个联系揭示了维里定理可以被看作是海尔曼-费曼定理在一个特殊参数（标度因子）下的应用。

#### 微妙之处与有效性条件

维里定理的推导过程同样依赖于一些重要的数学条件。

**边界条件**：无论使用哪种推导方法，在坐标空间中进行计算时都会涉及分部积分，这会产生一个在无穷远处的边界面项。为了使定理成立，这个边界面项必须为零。对于描述原子和分子中电子的束缚态，其波函数 $|\psi(\mathbf{r})\rangle$ 必须在 $r \to \infty$ 时足够快地衰减。仅仅是平方可积（$L^2$ 可积）是不够的。幸运的是，对于有物理意义的势（如库仑势），束缚态的波函数（$E \lt 0$）通常呈指数衰减（例如 $\sim \exp(-\kappa r)$），这足以保证所有相关的边界面项都趋于零 [@problem_id:2930763]。

**核-电/电-电尖点条件**：库仑势在粒子重合点（$r_i \to 0$ 或 $r_{ij} \to 0$）是奇异的。这给涉及 $\nabla V$ 或 $\nabla^2$ 的数学操作带来了挑战。为了保证哈密顿量在这些奇异点附近仍然是良定义的，并且为了使形式上的推导（如分部积分）有效，波函数必须满足所谓的 **Kato尖点条件（cusp conditions）**。例如，在原子单位制下，对于一个电子在核电荷为 $Z$ 的原子核附近，波函数必须满足 $\left.\frac{\partial \bar{\Psi}}{\partial r_{i}}\right|_{r_{i}=0} = -Z \bar{\Psi}(0)$，其中 $\bar{\Psi}$ 是对角度坐标平均后的波函数。这个条件确保了动能的奇异性与势能的奇异性在薛定谔方程中能够精确抵消，从而避免了在维里定理推导中出现额外的分布项 [@problem_id:2930774]。

**作为诊断工具的维里比**：对于近似的变分波函数，维里定理 $2\langle T \rangle + \langle V \rangle = 0$ 通常不被精确满足。维里比 $-\langle V \rangle / (2\langle T \rangle)$ 偏离1的程度，常常被用作衡量波函数质量的一个指标，特别是与基组不完备性相关 [@problem_id:2930779] [@problem_id:2930790]。然而，需要注意的是，如果一个变分计算中包含了对整体标度因子的优化，那么得到的波函数即使在其他方面（如尖点行为）不正确，也能精确满足维里定理，因此该诊断标准需谨慎使用 [@problem_id:2930774]。

### 超越简单情况：简并与锥形交叉

当量子体系的能级出现简并时，海尔曼-费曼定理的简单形式会失效，需要更为精细的处理。这在研究分子的势能面和光化学反应中尤为重要。

#### 简并点处的海尔曼-费曼定理

假设在参数 $\lambda = \lambda_0$ 处，哈密顿量 $H(\lambda_0)$ 的一个本征值 $E_0$ 是 $d$ 重简并的。此时，我们不能任意选取简并子空间中的一个态来应用海尔曼-费曼定理，因为一个任意的线性组合通常不会平滑地演变为 $\lambda \neq \lambda_0$ 时的某个非简并本征态。

正确的处理方法是应用一阶简并微扰理论 [@problem_id:2930729]。我们需要在 $d$ 维简并子空间中，构建并对角化微扰算符 $H' = \partial H/\partial \lambda |_{\lambda_0}$ 的矩阵。该矩阵的本征值 $\{\epsilon_k\}$ 给出的是从简并点 $E_0$ 分裂出去的各个能级曲线的斜率，即 $\mathrm{d}E_k/\mathrm{d}\lambda |_{\lambda_0} = \epsilon_k$。相应的本征矢 $\{|\chi_k\rangle\}$ 是“正确的”零阶波函数，它们能够平滑地连接到非简并区域的本征态。对于每一个这样的正确零阶波函数，一个广义的海尔曼-费曼定理成立：
$$
\frac{\mathrm{d}E_k}{\mathrm{d}\lambda}\bigg|_{\lambda_0} = \epsilon_k = \left\langle \chi_k \middle| \frac{\partial H}{\partial \lambda} \middle|_{\lambda_0} \middle| \chi_k \right\rangle
$$

#### 锥形交叉：绝热图像的破损

分子势能面上的简并点，特别是**锥形交叉（conical intersections）**，是现代光化学的核心概念。在锥形交叉点 $\mathbf{R}_0$ 处，两个绝热电子态的势能面发生接触。在交叉点附近，势能面呈现出双锥形状，这意味着能量对原子核坐标 $\mathbf{R}$ 的导数（即力）是不唯一的，能量函数在 $\mathbf{R}_0$ 点不可微 [@problem_id:2930744]。

因此，标准的海尔曼-费曼定理在锥形交叉点处失效。不仅如此，两个绝热态之间的非绝热耦合项 $\boldsymbol{\tau}_{12}(\mathbf{R}) = \langle \phi_{1} | \nabla_{\mathbf{R}} \phi_{2} \rangle$ 会在交叉点附近发散，通常表现为与距离成反比的奇异性（$\sim 1/||\mathbf{R}-\mathbf{R}_0||$）。这种奇异性标志着玻恩-奥本海默（Born-Oppenheimer）绝热近似的彻底破产，电子和原子核的运动在此区域紧密耦合。尽管在交叉点本身，维里定理对于简并的电子态依然成立，但它无法解决势能面的非解析性问题，也无法恢复海尔曼-费曼力的定义。

#### 准绝热表象

处理锥形交叉附近动力学的标准方法是，从奇异的绝热表象转换到一个光滑的**准绝热（diabatic）表象**。通过一个局域的幺正变换，可以构造一组新的电子基态，使得它们之间的导数耦合（非绝热耦合）为零或可以忽略。在这种表象下，哈密顿量的矩阵元（即所谓的准绝热势能面）是原子核坐标的光滑函数。海尔曼-费曼定理可以应用于这些光滑的准绝热势能元。原本在绝热表象中表现为动力学耦合奇异性的问题，现在被转移到了准绝热势能矩阵的非对角元上，表现为势能耦合 [@problem_id:2930744]。这种表象的转换为在势能面交叉区域进行量子动力学模拟提供了可行的理论基础。