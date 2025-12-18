## 引言
在[计算固体力学](@entry_id:169583)领域，精确模拟材料的复杂行为是工程设计与科学分析的基石。许多先进材料，如聚合物、生物组织和[土力学](@entry_id:180264)材料，其响应不仅取决于当前状态，还依赖于其经历的整个加载历史（遗传性）或内部微观结构的演化（内变量）。这些本构模型虽然物理意义明确，但其对历史的依赖性为数值计算带来了巨大挑战，特别是[遗传积分](@entry_id:186265)形式需要存储和处理完整的历史数据，导致计算成本过高。本文旨在系统性地解决这一知识鸿沟，为读者提供一套将复杂的遗传性和[内变量模型](@entry_id:750757)转化为计算上高效且数值上稳健的算法的完整指南。

在接下来的内容中，我们将首先在“原理与机制”一章中，深入探讨将[遗传积分](@entry_id:186265)转化为局部内变量[演化方程](@entry_id:268137)的核心思想与数学工具。随后，我们将在“应用与交叉学科联系”一章中，展示这些算法如何在[非线性有限元分析](@entry_id:167596)、[大变形](@entry_id:167243)塑性、岩土力学等多个领域中发挥关键作用，搭建理论与实践的桥梁。最后，通过“动手实践”部分的具体练习，读者将有机会亲手实现并验证这些强大的计算方法。

## 原理与机制

本章旨在阐述遗传性[本构模型](@entry_id:174726)（hereditary models）及其等效的内变量（internal variable）表述的数值实现方法的核心原理与机制。在上一章“引言”的基础上，我们将深入探讨如何将形式上依赖于完整加载历史的积分形式本构关系，转化为一组关于状态变量的[常微分方程](@entry_id:147024)（ODEs）。这种转化是开发计算高效、数值稳定且[热力学一致的](@entry_id:755906)时间步进算法的关键。我们将系统地推导这些算法，并阐明其在[非线性有限元分析](@entry_id:167596)框架中的作用。

### 从[遗传积分](@entry_id:186265)到内变量

许多材料，特别是聚合物、生物组织和土力学材料，其力学响应不仅取决于当前的变形状态，还依赖于其经历的整个加载历史。这类材料的行为通常通过**[遗传积分](@entry_id:186265)**来描述。在[线性粘弹性](@entry_id:181219)理论中，这一原理被精确地表述为**[玻尔兹曼叠加原理](@entry_id:185170)**（Boltzmann superposition principle）。

对于一个小应变、等温的[线性粘弹性](@entry_id:181219)体，其[应力-应变关系](@entry_id:274093)可以通过一个松弛或[蠕变](@entry_id:150410)积分来表示。在松弛表述中，当前时刻 $t$ 的应力张量 $\boldsymbol{\sigma}(t)$ 由[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}(\tau)$ 在整个过去历史 $[0, t]$ 上的加权积分给出：

$$
\boldsymbol{\sigma}(t) = \int_{0}^{t} \mathbf{G}(t-\tau) : \dot{\boldsymbol{\varepsilon}}(\tau) \, \mathrm{d}\tau
$$

此处，[四阶张量](@entry_id:181350) $\mathbf{G}(t)$ 是**松弛模量**，它描述了材料在 $t=0$ 时刻施加单位阶跃应变后，应力随时间的衰减过程。相应地，也存在一个对偶的[蠕变](@entry_id:150410)表述，通过**[蠕变](@entry_id:150410)柔度** $\mathbf{J}(t)$ 将应变历史与应力历史关联起来。松弛模量 $\mathbf{G}(t)$ 和蠕变柔度 $\mathbf{J}(t)$ 并非相互独立，它们通过拉普拉斯域中的关系 $s^2 \hat{\mathbf{G}}(s) : \hat{\mathbf{J}}(s) = \mathbf{I}$ 相互约束，其中 $\hat{\cdot}$ 表示[拉普拉斯变换](@entry_id:159339)，$\mathbf{I}$ 是四阶单位张量。

尽管[遗传积分](@entry_id:186265)形式在物理上直观且强大，但其在数值计算中存在一个重大障碍：为了计算任意时刻 $t$ 的应力，必须存储并积分从 $t=0$ 开始的全部应变历史。对于一个经历成千上万个时间步长的模拟，这将导致不可接受的内存消耗和计算成本。

为了克服这一困难，我们寻求一种等效的、不依赖于遥远历史的**[状态变量](@entry_id:138790)**表述。关键在于松弛模量 $\mathbf{G}(t)$ 的特定数学形式。实验数据表明，许多[粘弹性材料](@entry_id:194223)的松弛行为可以很好地通过一个**[Prony级数](@entry_id:204348)**（或称[广义麦克斯韦模型](@entry_id:169862)）来拟合：

$$
\mathbf{G}(t) = \mathbf{G}_{\infty} + \sum_{i=1}^{N} \mathbf{G}_{i} \exp\left(-\frac{t}{\tau_{i}}\right)
$$

其中，$\mathbf{G}_{\infty}$ 是**长期模量**或**平衡模量**，代表时间趋于无穷时材料的弹性响应。每一对 $(\mathbf{G}_{i}, \tau_{i})$ 分别代表第 $i$ 个松弛模式的模量和**松弛时间**。这种表示形式的优点是它允许我们将[遗传积分](@entry_id:186265)分解。将[Prony级数](@entry_id:204348)代入应力积分表达式中：

$$
\boldsymbol{\sigma}(t) = \mathbf{G}_{\infty} : \int_{0}^{t} \dot{\boldsymbol{\varepsilon}}(\tau) \, \mathrm{d}\tau + \sum_{i=1}^{N} \int_{0}^{t} \mathbf{G}_{i} \exp\left(-\frac{t-\tau}{\tau_{i}}\right) : \dot{\boldsymbol{\varepsilon}}(\tau) \, \mathrm{d}\tau
$$

假设初始应变为零，第一项简化为 $\mathbf{G}_{\infty} : \boldsymbol{\varepsilon}(t)$。对于求和中的每一项，我们可以定义一个**内变量** $\boldsymbol{\xi}_i(t)$，它代表第 $i$ 个松弛模式对总应力的贡献：

$$
\boldsymbol{\xi}_i(t) := \int_{0}^{t} \mathbf{G}_{i} \exp\left(-\frac{t-\tau}{\tau_{i}}\right) : \dot{\boldsymbol{\varepsilon}}(\tau) \, \mathrm{d}\tau
$$

通过引入这些内变量，总应力现在可以写成一个瞬时状态的函数，即当前应变和内变量的函数：

$$
\boldsymbol{\sigma}(t) = \mathbf{G}_{\infty} : \boldsymbol{\varepsilon}(t) + \sum_{i=1}^{N} \boldsymbol{\xi}_i(t)
$$

这些内变量 $\boldsymbol{\xi}_i(t)$ 包含了所有相关的历史信息，因此也被称为**记忆变量**。这种从积分到[状态变量](@entry_id:138790)的转化，是实现高效算法的第一步。

### 内变量的演化方程

将历史依赖性封装到内变量中后，下一步是确定这些变量如何随时间演化。通过对内变量 $\boldsymbol{\xi}_i(t)$ 的定义式进行时间求导，我们可以得到一个描述其局部演化的[常微分方程](@entry_id:147024)（ODE）。利用[莱布尼茨积分法则](@entry_id:145735)，我们发现：

$$
\dot{\boldsymbol{\xi}}_i(t) = -\frac{1}{\tau_i} \boldsymbol{\xi}_i(t) + \mathbf{G}_i : \dot{\boldsymbol{\varepsilon}}(t)
$$

这个结果至关重要：它表明，原本需要回溯整个历史的非局部积分运算，被等效地转化为求解一组[一阶线性常微分方程](@entry_id:164502)。在每个时间步中，我们只需要知道前一步的内变量值 $\boldsymbol{\xi}_i(t_n)$ 和当前步的应变率 $\dot{\boldsymbol{\varepsilon}}(t)$，就可以更新内变量到 $\boldsymbol{\xi}_i(t_{n+1})$，从而避免了存储完整的历史数据。

为了更具体地理解这一点，让我们考虑最简单的[粘弹性模型](@entry_id:175352)：**单个麦克斯韦单元**（Maxwell element）。该模型由一个[弹性模量](@entry_id:198862)为 $E$ 的弹簧和一个粘度为 $\eta$ 的粘壶[串联](@entry_id:141009)而成。其松弛时间为 $\tau = \eta/E$。通过[应力松弛](@entry_id:159905)实验（施加单位阶跃应变），可以推导出其松弛模量为 $G(t) = E \exp(-t/\tau)$。将其代入[遗传积分](@entry_id:186265)，再对[积分方程](@entry_id:138643)进行[微分](@entry_id:158718)，可以得到其等效的[微分形式](@entry_id:146747)[本构方程](@entry_id:138559)：

$$
\dot{\sigma}(t) + \frac{1}{\tau} \sigma(t) = E \dot{\varepsilon}(t)
$$

这正是在[广义麦克斯韦模型](@entry_id:169862)中，对应于单个[Prony级数](@entry_id:204348)项（此时 $\boldsymbol{\xi}_1 = \boldsymbol{\sigma}$）的[演化方程](@entry_id:268137)。这个简单的例子清晰地展示了[遗传积分](@entry_id:186265)形式与微分形式（即内变量演化方程）之间的等价性。

### 算法更新：[演化方程](@entry_id:268137)的离散化

拥有了内变量的[演化方程](@entry_id:268137)（一组ODEs）后，我们便可以采用标准的数值方法在离散的时间步 $[t_n, t_{n+1}]$ 上对其进行积分。然而，数值方法的选择对算法的稳定性和精度至关重要。

#### 稳定性的考量

让我们考察一个典型的演化方程的齐次部分 $\dot{\xi} = -\xi/\tau$，它描述了在没有外部驱动（$\dot{\varepsilon}=0$）时的[应力松弛](@entry_id:159905)。若采用**[前向欧拉法](@entry_id:141238)**（Forward Euler），离散形式为 $\xi_{n+1} = (1 - \Delta t/\tau) \xi_n$。为了保证数值解不发散，其[放大系数](@entry_id:144315)的[绝对值](@entry_id:147688)必须小于等于1，即 $|1 - \Delta t/\tau| \le 1$。这导出了一个[条件稳定性](@entry_id:276568)约束：时间步长 $\Delta t$ 必须小于等于两倍的松弛时间，即 $\Delta t \le 2\tau$。对于包含非常快的松弛过程（$\tau$ 很小）的材料，这将对时间步长施加过于严苛的限制。

相比之下，若采用**[后向欧拉法](@entry_id:139674)**（Backward Euler），离散形式为 $\xi_{n+1} = \xi_n / (1 + \Delta t/\tau)$。其放大系数的[绝对值](@entry_id:147688)为 $1 / (1 + \Delta t/\tau)$。由于 $\Delta t$ 和 $\tau$ 均为正值，这个系数永远在 $(0, 1)$ 区间内。这意味着无论时间步长 $\Delta t$ 多大，数值解总是稳定的。因此，后向欧拉法以及其他隐式积分格式是**无条件稳定**的，这解释了为何它们在[计算固体力学](@entry_id:169583)中被广泛采用。

#### 导出精确的更新公式

对于线性ODEs，我们甚至可以推导出在特定假设下**精确**的离散更新公式。考虑演化方程 $\dot{\boldsymbol{\xi}}_i + \frac{1}{\tau_i} \boldsymbol{\xi}_i = \mathbf{G}_i : \dot{\boldsymbol{\varepsilon}}(t)$。其在时间步 $[t_n, t_{n+1}]$ 上的精确解（通过[积分因子法](@entry_id:167338)）为：

$$
\boldsymbol{\xi}_i(t_{n+1}) = \boldsymbol{\xi}_i(t_n) \exp\left(-\frac{\Delta t}{\tau_i}\right) + \int_{t_n}^{t_{n+1}} \exp\left(-\frac{t_{n+1}-s}{\tau_i}\right) \mathbf{G}_i : \dot{\boldsymbol{\varepsilon}}(s) \, \mathrm{d}s
$$

该公式的最终形式取决于我们在时间步内对应变率 $\dot{\boldsymbol{\varepsilon}}(s)$ 所做的假设。一个常见且有效的假设是**[应变率](@entry_id:154778)在步内为常数**，即 $\dot{\boldsymbol{\varepsilon}}(s) = (\boldsymbol{\varepsilon}_{n+1} - \boldsymbol{\varepsilon}_n) / \Delta t = \Delta\boldsymbol{\varepsilon}/\Delta t$。在此假设下，上式中的积分可以被精确计算，得到如下的递归更新法则：

$$
\boldsymbol{\xi}_{i, n+1} = \boldsymbol{\xi}_{i, n} \exp\left(-\frac{\Delta t}{\tau_i}\right) + \mathbf{G}_i : \left[ \frac{\tau_i}{\Delta t} \left(1 - \exp\left(-\frac{\Delta t}{\tau_i}\right)\right) \right] \Delta\boldsymbol{\varepsilon}
$$

这个公式是“精确的”，因为它精确地积分了在分段线性应变路径假设下的[本构方程](@entry_id:138559)。其他假设，例如假设步内应变为常数 $\varepsilon(s) = \varepsilon_{n+1}$（一种完全隐式的假设），也会导出一个不同的精确更新公式。因此，算法的“精确性”是相对于步内插值假设而言的。

### [热力学一致性](@entry_id:138886)与数值稳定性

一个可靠的[数值算法](@entry_id:752770)不仅要数值稳定，还必须遵守[热力学](@entry_id:141121)的基本定律，即[热力学第二定律](@entry_id:142732)。对于[等温过程](@entry_id:143096)，这通常通过**克劳修斯-杜亨不等式**（Clausius-Duhem inequality）来表述，它要求内能的耗散率必须为非负。

在一个内变量框架中，假设[亥姆霍兹自由能](@entry_id:136442)密度 $\psi$ 是应变 $\boldsymbol{\varepsilon}$ 和内变量 $\boldsymbol{\alpha}$（例如，在[麦克斯韦模型](@entry_id:157958)中，$\boldsymbol{\alpha}$ 可以是[弹性应变](@entry_id:189634)）的函数。克劳修斯-杜亨不等式可以写作 $\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0$。通过标准的Coleman-Noll程序，我们可以从中导出应力的[本构关系](@entry_id:186508)（$\boldsymbol{\sigma} = \partial\psi/\partial\boldsymbol{\varepsilon}$）以及[耗散不等式](@entry_id:188634)。例如，对于[麦克斯韦模型](@entry_id:157958)，这可以导出[胡克定律](@entry_id:149682) $\sigma = E \alpha$ 和非负耗散的要求，后者进而约束了材料参数必须为正（如 $E>0, \eta>0$）。

这一原理可以推广到离散的[数值算法](@entry_id:752770)。一个[热力学一致的](@entry_id:755906)算法应保证在任何时间步内，数值计算出的耗散都是非负的。这可以通过一个**离散[耗散不等式](@entry_id:188634)**来保证。对于一个后向欧拉更新方案，可以证明其满足一个形如 $\Delta\psi + \mathcal{D}^{\text{alg}} \Delta t \ge \text{功}$ 的不等式，其中 $\Delta\psi$ 是自由能的增量，而**算法耗散** $\mathcal{D}^{\text{alg}}$ 是一个保证为非负的量。这个性质是算法[无条件稳定性](@entry_id:145631)的一个更深层次的物理解释，因为它确保了数值解不会凭空产生能量。

具体地，对于采用[后向欧拉法](@entry_id:139674)离散化的[麦克斯韦模型](@entry_id:157958)，我们可以在一个时间步内计算出累积的算法耗散。例如，其表达式为 $\mathcal{D}^{\text{alg}} = \int_{t_n}^{t_{n+1}} \eta \dot{\varepsilon}_v^2 \mathrm{d}t \approx \frac{E^2 \alpha_{n+1}^2 \Delta t}{\eta}$。这表明，我们可以精确量化每个时间步由于[粘性流](@entry_id:136330)动而耗散的能量，并验证其非负性。

### 算法一致性[切线](@entry_id:268870)模量

到目前为止，我们关注的是材料点（或[高斯点](@entry_id:170251)）层面的应力更新。在有限元方法（FEM）的框架中，这些局部计算是求解[全局平衡方程](@entry_id:272290)的子过程。对于[非线性](@entry_id:637147)或含时问题，[全局平衡方程](@entry_id:272290) $\boldsymbol{R}(\boldsymbol{u}) = \boldsymbol{0}$ 通常采用**[牛顿-拉弗森](@entry_id:177436)**（[Newton-Raphson](@entry_id:177436)）[迭代法](@entry_id:194857)求解。

[牛顿法](@entry_id:140116)的核心是线性化残差方程：$\boldsymbol{K}_T \Delta\boldsymbol{u} = -\boldsymbol{R}$，其中 $\boldsymbol{K}_T = \mathrm{d}\boldsymbol{R}/\mathrm{d}\boldsymbol{u}$ 是**[切线刚度矩阵](@entry_id:170852)**，或称[雅可比矩阵](@entry_id:264467)。为了实现[牛顿法](@entry_id:140116)的二次收敛（即在每次迭代中误差以平方速率减小），$\boldsymbol{K}_T$ 必须是残差向量 $\boldsymbol{R}$ 对未知量（位移 $\boldsymbol{u}$）的精确导数。

在材料层面，这意味着我们需要计算应力 $\boldsymbol{\sigma}^{n+1}$ 对总应变 $\boldsymbol{\varepsilon}^{n+1}$ 的[全导数](@entry_id:137587)，即 $\mathbb{C}^{\text{alg}} := \mathrm{d}\boldsymbol{\sigma}^{n+1}/\mathrm{d}\boldsymbol{\varepsilon}^{n+1}$。这个量被称为**算法一致性[切线](@entry_id:268870)模量**（algorithmic consistent tangent modulus）。这里的“一致性”至关重要：该[切线](@entry_id:268870)模量必须是对应力更新**离散算法本身**的精确线性化，而非连续介质[本构方程](@entry_id:138559)的[切线](@entry_id:268870)（即 $\dot{\boldsymbol{\sigma}}/\dot{\boldsymbol{\varepsilon}}$）。

对于一个隐式的内变量更新（由局部残差方程 $\boldsymbol{r}(\boldsymbol{\alpha}^{n+1}, \boldsymbol{\varepsilon}^{n+1}) = \boldsymbol{0}$ 定义），一致性[切线](@entry_id:268870)模量可以通过链式法则和[隐函数定理](@entry_id:147247)导出。其一般形式为：

$$
\mathbb{C}^{\text{alg}} = \frac{\partial \hat{\boldsymbol{\sigma}}}{\partial \boldsymbol{\varepsilon}} - \frac{\partial \hat{\boldsymbol{\sigma}}}{\partial \boldsymbol{\alpha}} \left( \frac{\partial \boldsymbol{r}}{\partial \boldsymbol{\alpha}} \right)^{-1} \frac{\partial \boldsymbol{r}}{\partial \boldsymbol{\varepsilon}}
$$

其中所有[偏导数](@entry_id:146280)都在 $(t_{n+1})$ 时刻评估。第一项是显式贡献（冻结内变量），第二项是由于内变量对应变的隐式依赖而产生的修正。

对于我们之[前推](@entry_id:158718)导的[线性粘弹性](@entry_id:181219)模型的精确更新算法，由于其应力更新是线性的，一致性[切线](@entry_id:268870)模量可以直接从 $\boldsymbol{\sigma}_{n+1}$ 对 $\boldsymbol{\varepsilon}_{n+1}$ 的导数得到。例如，对于常数[应变率](@entry_id:154778)假设，其一致性[切线](@entry_id:268870)标量形式为：

$$
C^{\text{alg}} = G_{\infty} + \sum_{i=1}^{N} G_i \frac{\tau_i}{\Delta t} \left(1 - \exp\left(-\frac{\Delta t}{\tau_i}\right)\right)
$$

使用这个精确的 $\mathbb{C}^{\text{alg}}$ 来组装全局[切线刚度矩阵](@entry_id:170852)，是保证全局牛顿迭代具有最优收敛性的关键。若使用不一致的[切线](@entry_id:268870)（例如，弹性模量或连续介质[切线](@entry_id:268870)模量），收敛速度将退化为线性甚至更慢，显著降低了[计算效率](@entry_id:270255)。