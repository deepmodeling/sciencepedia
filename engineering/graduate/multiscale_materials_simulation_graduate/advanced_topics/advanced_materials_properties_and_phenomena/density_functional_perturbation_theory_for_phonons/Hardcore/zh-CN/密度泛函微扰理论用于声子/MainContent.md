## 引言
[晶格振动](@entry_id:140970)，或称声子，是决定材料宏观物理性质（如热、电、光、力学行为）的微观基础。精确地从第一性原理预测[声子谱](@entry_id:753408)，对于材料的设计和理解至关重要。然而，传统方法如“冻结声子”法因计算成本高昂且适用性有限，面临巨大挑战。[密度泛函微扰理论](@entry_id:196807)（DFPT）的出现，为这一难题提供了革命性的解决方案。它作为一种高效、普适的[线性响应方法](@entry_id:751324)，能够直接在晶体原胞内计算任意[波矢](@entry_id:178620)的声子，极大地推动了[计算材料科学](@entry_id:1122793)的发展。

本文旨在为读者提供一个关于DFPT计算声子的全面指南。我们将分三个章节展开：在“原理与机制”中，我们将深入剖析DFPT的理论核心，从[力常数](@entry_id:156420)到自洽响应循环；接着，在“应用与跨学科交叉”中，我们将展示DFPT如何在[结构稳定性](@entry_id:147935)、[热力学](@entry_id:172368)、[电子输运](@entry_id:136976)等多个领域发挥关键作用；最后，在“动手实践”部分，读者将通过具体的计算练习来巩固所学知识。通过这一结构化的学习路径，读者将全面掌握DFPT的理论精髓与实践应用。

## 原理与机制

在上一章引言的基础上，本章深入探讨从第一性原理计算声子谱的核心理论框架——[密度泛函微扰理论](@entry_id:196807)（Density Functional Perturbation Theory, DFPT）。我们将系统地阐述该理论的基石、自洽计算的机制，以及它如何与固体中重要的物理现象相关联。

### 从[力常数](@entry_id:156420)到[声子色散](@entry_id:142059)

在[玻恩-奥本海默近似](@entry_id:146252)下，[晶格动力学](@entry_id:145448)的核心在于描述原子离开其平衡位置时系统总能量的变化。对于简谐近似，能量相对于原子位移的展开只保留到二阶项。描述这些二阶能量变化的物理量是**[原子间力常数](@entry_id:750716) (interatomic force constants, IFCs)**。它被严格定义为总能量 $E$ 对原子位移 $u$ 的[二阶偏导数](@entry_id:635213) ：

$$
C_{\kappa\alpha, \kappa'\beta}(\mathbf{R}) = \left. \frac{\partial^2 E}{\partial u_{\kappa\alpha}(\mathbf{0}) \partial u_{\kappa'\beta}(\mathbf{R})} \right|_{\{\mathbf{u}\}=\mathbf{0}}
$$

其中，$u_{\kappa\alpha}(\mathbf{0})$ 表示位于参考[原胞](@entry_id:159354)（$\mathbf{L}=\mathbf{0}$）中第 $\kappa$ 个原子沿笛卡尔方向 $\alpha$ 的位移，而 $u_{\kappa'\beta}(\mathbf{R})$ 则是位于[晶格矢量](@entry_id:161583)为 $\mathbf{R}$ 的[原胞](@entry_id:159354)中第 $\kappa'$ 个原子沿 $\beta$ 方向的位移。[力常数](@entry_id:156420)描述了一个原子位移在[晶格](@entry_id:148274)中另一个原子上引起的恢复力。

一旦获得了[实空间](@entry_id:754128)的[力常数](@entry_id:156420)，我们就可以通过求解一个[本征值问题](@entry_id:142153)来获得[声子频率](@entry_id:1129612)和振动模式。为此，我们构造**动力学矩阵 (dynamical matrix)** $D(\mathbf{q})$，它是[力常数](@entry_id:156420)矩阵的傅里叶变换。为了得到一个标准的厄米[本征值问题](@entry_id:142153)，通常会引入原子质量 $M_\kappa$ 进行加权 ：

$$
D_{\kappa\alpha, \kappa'\beta}(\mathbf{q}) = \frac{1}{\sqrt{M_\kappa M_{\kappa'}}} \sum_{\mathbf{R}} C_{\kappa\alpha, \kappa'\beta}(\mathbf{R}) e^{i\mathbf{q}\cdot\mathbf{R}}
$$

求解该动力学矩阵的本征方程：

$$
\sum_{\kappa'\beta} D_{\kappa\alpha, \kappa'\beta}(\mathbf{q}) e_{\kappa'\beta}^{\nu}(\mathbf{q}) = \omega_{\nu}^2(\mathbf{q}) e_{\kappa\alpha}^{\nu}(\mathbf{q})
$$

其本征值 $\omega_{\nu}^2(\mathbf{q})$ 给出声子频率的平方，其中 $\mathbf{q}$ 是波矢，$\nu$ 是[声子支](@entry_id:189965)的索引。对应的本征矢量 $e_{\kappa\alpha}^{\nu}(\mathbf{q})$ 是**声子[极化矢量](@entry_id:269389) (polarization vectors)**，描述了该模式下各个原子的相对振动幅度和方向。由于动力学矩阵是[厄米矩阵](@entry_id:155147)，其本征矢量构成一个正交归一的完备集，满足正交[归一化条件](@entry_id:156486) ：

$$
\sum_{\kappa\alpha} e_{\kappa\alpha}^{\nu}(\mathbf{q})^* e_{\kappa\alpha}^{\nu'}(\mathbf{q}) = \delta_{\nu\nu'}
$$

因此，从第一性原理计算[声子谱](@entry_id:753408)的根本任务，就是精确地计算[原子间力常数](@entry_id:750716)。

### DFPT 方法：通过[线性响应](@entry_id:146180)计算[力常数](@entry_id:156420)

直接根据定义通过[有限位移法](@entry_id:749383)（即“冻结声子”法）计算二阶[能量导数](@entry_id:170468)是可行的，但这需要在一个包含声子波长的超胞中进行多次独立的自洽计算，计算量巨大，且仅限于与超胞周期匹配的有理[波矢](@entry_id:178620) $\mathbf{q}$。[密度泛函微扰理论](@entry_id:196807)（DFPT）提供了一种更为高效和普适的分析方法。

DFPT 的核心思想是利用[线性响应理论](@entry_id:145737)，通过计算电子系统对**单色（monochromatic）**原子位移微扰的响应来直接获得任意[波矢](@entry_id:178620) $\mathbf{q}$ 的动力学矩阵。这种方法的关键优势在于，它可以在晶体的[原胞](@entry_id:159354)内完成计算，而无需构建超胞。

这一巨大简化源于[晶格](@entry_id:148274)周期性所施加的对称性约束，通常被称为**广义[布洛赫定理](@entry_id:137461) (generalized Bloch's theorem)** 。一个具有波矢 $\mathbf{q}$ 的单色声子微扰，其位移场在不同[原胞](@entry_id:159354)间的关系为 $u_{\kappa\alpha}(\mathbf{R}) \propto e^{i\mathbf{q}\cdot\mathbf{R}}$。这种周期性的微扰势 $\Delta V_{\text{ext}}(\mathbf{r}; \mathbf{q})$ 具有[协变](@entry_id:634097)性，即在[晶格矢量](@entry_id:161583) $\mathbf{R}$ 的平移下，它会获得一个相位因子 $e^{i\mathbf{q}\cdot\mathbf{R}}$。线性响应理论确保了所有响应量，包括一阶电子密度 $\Delta n(\mathbf{r}; \mathbf{q})$ 和自洽有效势 $\Delta V_{\text{eff}}(\mathbf{r}; \mathbf{q})$，都具有相同的协变性 ：

$$
\Delta f(\mathbf{r}+\mathbf{R}; \mathbf{q}) = e^{i\mathbf{q}\cdot\mathbf{R}} \Delta f(\mathbf{r}; \mathbf{q})
$$

这意味着这些响应量可以表示为一个[晶格](@entry_id:148274)[周期函数](@entry_id:139337)与平面波 $e^{i\mathbf{q}\cdot\mathbf{r}}$ 的乘积。这一性质使得整个响应问题的求解可以被严格限制在单个[原胞](@entry_id:159354)内。

在[电子能带](@entry_id:175335)的语言中，这个携带晶体动量 $\mathbf{q}$ 的微扰势，其作用是将一个未受扰的、位于波矢 $\mathbf{k}$ 的[布洛赫态](@entry_id:147552) $|\psi_{n\mathbf{k}}\rangle$ 与位于波矢 $\mathbf{k}+\mathbf{q}$ 的一系列态耦合起来。因此，对 $|\psi_{n\mathbf{k}}\rangle$ 的[一阶修正](@entry_id:155896) $|\Delta\psi_{n\mathbf{k}}\rangle$ 将具有 $\mathbf{k}+\mathbf{q}$ 的[晶体动量](@entry_id:136369)  。

### 自洽线性响应循环

DFPT 的计算过程是一个自洽迭代循环，旨在精确求解电子系统对原子位移的线性响应。

1.  **初始微扰**: [声子模式](@entry_id:201212)的原子位移产生一个对电子的一阶**裸微扰势 (bare perturbation potential)**，即离子实与电子相互作用势的一阶变化量 $\Delta V_{\text{ion}}^{(1)}(\mathbf{r}; \mathbf{q})$。

2.  **电子响应**: 这个微扰势导致了占据的科恩-尚 (Kohn-Sham, KS) 轨道发生一阶变化 $|\Delta\psi_{n\mathbf{k}}^{(1)}\rangle$。

3.  **密度响应**: 轨道的一阶变化会引起电子密度的一阶变化 $\Delta n^{(1)}(\mathbf{r}; \mathbf{q})$。对于非[自旋极化](@entry_id:164038)体系，其表达式为 ：
    $$
    \Delta n^{(1)}(\mathbf{r}; \mathbf{q}) = 2 \sum_{n\mathbf{k}}^{\text{occ}} \text{Re} \{ \psi_{n\mathbf{k}}^{(0)*}(\mathbf{r}) \Delta\psi_{n\mathbf{k}}^{(1)}(\mathbf{r}; \mathbf{q}) \}
    $$
    其中，$\psi_{n\mathbf{k}}^{(0)}$ 是未受扰的 KS 轨道，求和遍历所有占据态。

4.  **[屏蔽势](@entry_id:193863)**: 诱导出的电荷密度 $\Delta n^{(1)}$ 会反过来产生一个**[屏蔽势](@entry_id:193863) (screening potential)**，它包含两部分：一阶哈特里（Hartree）势 $\Delta V_H^{(1)}$ 和一阶交换关联（exchange-correlation, XC）势 $\Delta V_{xc}^{(1)}$。
    $$
    \Delta V_H^{(1)}(\mathbf{r}; \mathbf{q}) = \int \frac{\Delta n^{(1)}(\mathbf{r}'; \mathbf{q})}{|\mathbf{r}-\mathbf{r}'|} d\mathbf{r}'
    $$
    $$
    \Delta V_{xc}^{(1)}(\mathbf{r}; \mathbf{q}) = \int f_{\text{xc}}(\mathbf{r}, \mathbf{r}') \Delta n^{(1)}(\mathbf{r}'; \mathbf{q}) d\mathbf{r}'
    $$
    其中 $f_{\text{xc}}(\mathbf{r}, \mathbf{r}') = \frac{\delta V_{\text{xc}}[n](\mathbf{r})}{\delta n(\mathbf{r}')}$ 是交换关联核，它描述了 XC 势对密度变化的非局域响应 。

5.  **[自洽循环](@entry_id:138158)**: 总的一阶自洽势是裸微扰与[屏蔽势](@entry_id:193863)之和：
    $$
    \Delta V_{\text{scf}}^{(1)} = \Delta V_{\text{ion}}^{(1)} + \Delta V_H^{(1)} + \Delta V_{xc}^{(1)}
    $$
    这个新的自洽势被代入步骤2，用于计算新的轨道响应。这个过程反复迭代，直到输入的 $\Delta V_{\text{scf}}^{(1)}$ 和通过响应计算得到的输出势一致为止。值得强调的是，仅仅使用裸微扰势 $\Delta V_{\text{ion}}^{(1)}$ 而忽略电子的屏蔽效应是完全错误的，这将导致与实验严重偏离的结果 。

### 斯特恩海默方程：求解响应[波函数](@entry_id:201714)

在[自洽循环](@entry_id:138158)中，核心的计算步骤是从给定的微扰势 $\Delta V_{\text{scf}}^{(1)}$ 计算轨道的[一阶修正](@entry_id:155896) $|\Delta\psi_{n\mathbf{k}}^{(1)}\rangle$。标准微扰理论提供的“对态求和 (sum-over-states)”公式需要计算并遍历所有空的（导带）KS 态，这在计算上是极其昂贵甚至是不可行的。

DFPT 通过求解一个线性方程组——**斯特恩海默方程 (Sternheimer equation)** 来巧妙地绕过这个问题  ：

$$
(\hat{H}^{(0)} - \epsilon_{n\mathbf{k}}^{(0)}) |\Delta\psi_{n\mathbf{k}}^{(1)}\rangle = -\hat{P}_c \Delta V_{\text{scf}}^{(1)} |\psi_{n\mathbf{k}}^{(0)}\rangle
$$

这里，$\hat{H}^{(0)}$ 和 $\epsilon_{n\mathbf{k}}^{(0)}$ 是未受扰的 KS 哈密顿量和本征值。$\hat{P}_c = \hat{1} - \sum_{m \in \text{occ}} |\psi_{m,\mathbf{k+q}}\rangle\langle\psi_{m,\mathbf{k+q}}|$ 是[投影算符](@entry_id:154142)，它将右侧的源项投影到所有未占据（导带）子空间上。这个方程可以通过高效的迭代方法求解，而无需显式计算任何空态。

然而，求解斯特恩海默方程存在一个微妙的数学问题。对于一个占据态 $|\psi_{n\mathbf{k}}^{(0)}\rangle$，左侧的算符 $(\hat{H}^{(0)} - \epsilon_{n\mathbf{k}}^{(0)})$ 是奇异的，因为它作用于与 $|\psi_{n\mathbf{k}}^{(0)}\rangle$ 简并的任何态（包括其自身）时结果为零。这意味着 $|\Delta\psi_{n\mathbf{k}}^{(1)}\rangle$ 的解不是唯一的，存在一个[规范自由度](@entry_id:160491) 。

解决这个问题的标准方法是选择一个特定的规范。**[平行输运](@entry_id:160671)规范 (parallel-transport gauge)** 是最常用的选择，它要求轨道的[一阶修正](@entry_id:155896)必须与整个占据子空间正交：

$$
\langle\psi_{m\mathbf{k}}^{(0)}|\Delta\psi_{n\mathbf{k}}^{(1)}\rangle = 0, \quad \text{对于所有占据态 } m
$$

这个条件物理上对应于，微扰引起的轨道演化中不包含占据态之间的任意幺正混合。在斯特恩海默方程中，这个条件通过[投影算符](@entry_id:154142) $\hat{P}_c$ 的作用来自然实现，它确保了解 $|\Delta\psi_{n\mathbf{k}}^{(1)}\rangle$ 完全位于导带子空间内，从而在该空间中唯一地确定了解 。即使存在占据态简并，此方法依然适用，因为它等效于在简并子空间中选择了能够[对角化](@entry_id:147016)微扰矩阵的“正确”零阶基。

### 从响应到[物理可观测量](@entry_id:154692)

一旦通过 DFPT 求解出自洽的线性响应量，就可以计算出[力常数](@entry_id:156420)以及其他相关的物理量。

根据赫尔曼-费曼（Hellmann-Feynman）定理，作用在原子核上的力可以直接从基态电子密度计算。[力常数](@entry_id:156420)是力的导数，因此可以通过计算力对原子位移的线性响应来获得。在 DFPT 框架下，这等效于利用已求得的一阶密度 $n^{(1)}$ 和一阶势 $V_{\text{scf}}^{(1)}$ 来[计算动力学](@entry_id:204520)矩阵的[矩阵元](@entry_id:186505) $D_{\kappa\alpha, \kappa'\beta}(\mathbf{q})$ 。通过在 $\mathbf{q}$ 点网格上[计算动力学](@entry_id:204520)矩阵，再进行[逆傅里叶变换](@entry_id:178300)，即可得到实空间的[力常数](@entry_id:156420) $C_{\kappa\alpha,\kappa'\beta}(\mathbf{R})$ 。

值得注意的是，在DFPT中计算的核心物理量——一阶自洽势 $\Delta V_{\text{scf}}^{(1)}$ ——具有双重作用。它不仅决定了[力常数](@entry_id:156420)，其在不同电子态之间的矩阵元 $\langle \psi_{m,\mathbf{k+q}} | \Delta V_{\text{scf}}^{(1)} | \psi_{n,\mathbf{k}} \rangle$ 也正是描述[电子散射](@entry_id:159023)过程的**[电子-声子耦合](@entry_id:139197) (electron-phonon coupling)** [矩阵元](@entry_id:186505)。这充分体现了 DFPT 理论框架的统一性与强大功能 。

### 重要的物理约束与效应

任何可靠的声子计算都必须满足基本的物理对称性，并能正确描述由[长程相互作用](@entry_id:140725)引起的效应。

#### [平移不变性](@entry_id:195885)与[声学求和规则](@entry_id:746229)

晶体的总能量在整体刚性平移下保持不变。这一基本对称性对[力常数](@entry_id:156420)施加了一个严格的约束，即**[声学求和规则](@entry_id:746229) (Acoustic Sum Rule, ASR)** ：

$$
\sum_{\mathbf{R},\kappa'} C_{\kappa\alpha,\kappa'\beta}(\mathbf{R}) = 0
$$

这条规则对于任意的 $\kappa, \alpha, \beta$ 都成立。它物理解释为，当整个晶体发生均匀位移时，每个原子受到的合力必须为零。在倒易空间中，ASR 确保了在[布里渊区](@entry_id:142395)中心（$\mathbf{q}=\mathbf{0}$），动力学矩阵有三个本征值为零。这三个[零频模式](@entry_id:166697)对应于沿三个笛卡尔方向的刚性平移，即[声学支](@entry_id:138762)声子。ASR 是检验声子计算准确性的一个重要判据。

#### 极性材料中的 LO-TO 劈裂

在[离子晶体](@entry_id:138598)等极性材料中，长程[库仑相互作用](@entry_id:747947)扮演着至关重要的角色。当原子振动时，若产生净的宏观[电偶极矩](@entry_id:178520)，则会形成一个[宏观电场](@entry_id:196409)。对于**纵向光学 (Longitudinal Optical, LO)** 声子，其极化方向平行于[波矢](@entry_id:178620) $\mathbf{q}$，产生的[宏观电场](@entry_id:196409)会提供一个额外的恢复力，从而使其频率高于对应的**横向光学 (Transverse Optical, TO)** 声子（其极化方向垂直于 $\mathbf{q}$，不产生[宏观电场](@entry_id:196409)）。这种在 $\mathbf{q} \to \mathbf{0}$ 处 LO 和 TO 模式的频率差被称为 **LO-TO 劈裂 (LO-TO splitting)**。

这种效应源于库仑相互作用的长程特性，导致动力学矩阵在 $\mathbf{q} \to \mathbf{0}$ 极限下存在一个**非解析项 (non-analytic term)**。标准的 DFPT 计算本质上是短程的，无法直接捕捉到这一效应。因此，必须在 DFPT 计算出的动力学矩阵之上，额外添加这个非解析修正项。该修正项依赖于材料的**[玻恩有效电荷](@entry_id:144855) (Born effective charges)** $Z^*$ 和**高频[介电张量](@entry_id:194185) (high-frequency dielectric tensor)** $\epsilon^{\infty}$，后两者本身也可以通过 DFPT 对外加电场的响应来计算  。该非解析项的形式为：

$$
D^{\text{NA}}_{\kappa\alpha, \kappa'\beta}(\mathbf{q} \to \mathbf{0}) = \frac{4\pi}{\Omega \sqrt{M_{\kappa} M_{\kappa'}}} \frac{ (\mathbf{q} \cdot Z_{\kappa}^*)_{\alpha} (\mathbf{q} \cdot Z_{\kappa'}^*)_{\beta} }{ \mathbf{q} \cdot \epsilon^{\infty} \cdot \mathbf{q} }
$$

其中 $\Omega$ 是原胞体积。这个修正项正确地描述了 LO-TO 劈裂的大小及其对 $\mathbf{q}$ 方向的依赖性。

#### 金属中的[科恩反常](@entry_id:144730)

在金属中，巡游电子可以有效地屏蔽离子实之间的相互作用。这种屏蔽效应由电子气的**静态[磁化率](@entry_id:138219) (static susceptibility)** $\chi(\mathbf{q})$ 描述。$\chi(\mathbf{q})$ 的值反映了电子系统在受到[波矢](@entry_id:178620)为 $\mathbf{q}$ 的外部电势扰动时，形成[电荷密度波](@entry_id:146282)的能力。

根据林哈德（Lindhard）理论，$\chi(\mathbf{q})$ 在某些特殊的 $\mathbf{q}$ 矢量处可以呈现非解析行为（例如，其导数发散）。这些特殊矢量被称为**[费米面嵌套](@entry_id:144440)矢量 (Fermi surface nesting vectors)**，它们能够将[费米面](@entry_id:137798)上的大量电子态相互连接。当声子的波矢 $\mathbf{q}$ 恰好等于一个嵌套矢量时，电子的屏蔽能力会发生急剧变化，从而导致[声子频率](@entry_id:1129612) $\omega(\mathbf{q})$ 在该点出现一个下凹或扭折（kink）。这种在[声子色散](@entry_id:142059)谱中由[电子-声子相互作用](@entry_id:140708)引起的非解析特征，被称为**[科恩反常](@entry_id:144730) (Kohn anomaly)** 。

对于一个简单的三维[自由电子气模型](@entry_id:155154)，其[费米面](@entry_id:137798)是一个半径为 $k_F$ 的球体。最强的嵌套条件发生在连接费米球上两个相对点时，即 $q = 2k_F$。因此，在这类金属的[声子谱](@entry_id:753408)中，人们预计会在纵向[声学支](@entry_id:138762)的 $q \approx 2k_F$ 处观察到[科恩反常](@entry_id:144730)。DFPT 能够从第一性原理出发，通过精确计算电子对声子微扰的响应，自然地再现这一微妙的[电子-声子耦合](@entry_id:139197)效应。