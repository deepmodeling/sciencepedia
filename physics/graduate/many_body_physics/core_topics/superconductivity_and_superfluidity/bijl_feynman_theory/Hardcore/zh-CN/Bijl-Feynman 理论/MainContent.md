## 引言
在量子多体物理学的广阔领域中，理解系统的集体行为是核心挑战之一。与单个粒子的独立运动不同，强相互作用系统中的低能激发通常表现为所有粒子协同参与的集体模式，即“元激发”。Bijl-Feynman理论正是为描述这些元激发而生，它提供了一个极其优美且富有物理直观性的框架，成为了现代多体物理的基石。该理论解决了如何从系统的基态性质出发，预测其动力学响应这一根本性问题，深刻地揭示了微观结构与宏观动力学之间的内在联系。

本文将系统地引导读者深入探索Bijl-Feynman理论的精髓。在第一章“原理与机制”中，我们将从第一性原理出发，详细推导其核心公式，阐明其物理内涵和理论基础，如f-求和规则。随后的“应用与跨学科联系”一章将展示该理论在解释真实物理现象（如超流氦的旋子之谜）和跨领域应用（如冷原子和等离子体）中的强大威力。最后，通过“动手实践”部分提供的具体计算问题，读者将有机会亲手应用所学知识，将抽象的理论概念转化为解决实际问题的能力。通过这一结构化的学习路径，我们将共同领略这一理论的简洁之美及其在物理学中的深远影响。

## 原理与机制

本章深入探讨Bijl-Feynman理论的核心原理与机制。我们将系统地推导其核心公式，阐明其物理内涵，并探讨其在各种量子多体系统中的应用与扩展。我们的目标是建立一个坚实的理论框架，使读者能够理解和应用这一描述量子流体中元激发的强大工具。

### 费曼变分激发态

在量子多体系统中，特别是像液氦这样的量子流体中，最低能量的激发不是单个粒子的运动，而是集体模式。Richard Feynman提出了一个极具物理直观性的变分波函数来描述这种最简单的元激发。其基本思想是在系统的基态上创建一个密度波。

我们考虑一个由$N$个相同粒子组成的系统，其精确的、归一化的基态波函数为 $|\Psi_0\rangle$。Feynman通过在一个均匀的基态背景上引入一个平面波形式的密度涨落来构造激发态。这种涨落由**密度涨落算符** $\hat{\rho}_{\mathbf{k}}$ 产生：
$$
\hat{\rho}_{\mathbf{k}} = \sum_{j=1}^N e^{-i\mathbf{k} \cdot \hat{\mathbf{r}}_j}
$$
其中 $\hat{\mathbf{r}}_j$ 是第$j$个粒子的位置算符，$\mathbf{k}$ 是波矢。这个算符是其自身厄米共轭的傅里叶分量，即 $\hat{\rho}_{\mathbf{k}}^\dagger = \hat{\rho}_{-\mathbf{k}}$。

将此算符作用于基态，我们得到Feynman变分激发态（未归一化）$|\tilde{\Psi}_\mathbf{k}\rangle$：
$$
|\tilde{\Psi}_\mathbf{k}\rangle = \hat{\rho}_{\mathbf{k}} |\Psi_0\rangle
$$
这个态在物理上代表了一个动量为$\hbar\mathbf{k}$的元激发。为了处理这个态，首先需要计算它的模方。这个计算引出了一个至关重要的物理量——**静态结构因子** $S(k)$：
$$
\langle \tilde{\Psi}_\mathbf{k} | \tilde{\Psi}_\mathbf{k} \rangle = \langle \Psi_0 | \hat{\rho}_{\mathbf{k}}^\dagger \hat{\rho}_{\mathbf{k}} | \Psi_0 \rangle = \langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} \hat{\rho}_{\mathbf{k}} | \Psi_0 \rangle \equiv N S(k)
$$
静态结构因子 $S(k)$（其中 $k=|\mathbf{k}|$）完全由系统的**基态**性质决定，它描述了基态中粒子位置的关联性。通过中子散射等实验可以直接测量$S(k)$。因此，归一化的Feynman激发态可以写为：
$$
|\Psi_\mathbf{k}\rangle = \frac{1}{\sqrt{N S(k)}} \hat{\rho}_{\mathbf{k}} |\Psi_0\rangle
$$

这些Feynman态构成了一组理想的元激发基矢。一个重要的性质是它们之间的**正交性**。对于两个不同的波矢 $\mathbf{k} \neq \mathbf{k}'$，我们可以计算其交叠积分 [@problem_id:1098949]：
$$
\langle \Psi_{\mathbf{k}'} | \Psi_{\mathbf{k}} \rangle = \frac{1}{N \sqrt{S(k') S(k)}} \langle \Psi_0 | \hat{\rho}_{-\mathbf{k}'} \hat{\rho}_{\mathbf{k}} | \Psi_0 \rangle
$$
由于系统的平移不变性，对于一个均匀的流体，只有当总波矢为零时，矩阵元才能非零。$\hat{\rho}_{-\mathbf{k}'} \hat{\rho}_{\mathbf{k}}$ 算符携带的净波矢为 $\mathbf{k} - \mathbf{k}' \neq 0$。因此，它在均匀基态上的期望值为零。这意味着：
$$
\langle \Psi_{\mathbf{k}'} | \Psi_{\mathbf{k}} \rangle = 0 \quad (\text{for } \mathbf{k} \neq \mathbf{k}')
$$
这证实了Feynman态构成了一个正交集。更进一步，系统的哈密顿量在这些态之间也是对角的。如果哈密顿量 $\hat{H}$ 具有平移不变性，它与总动量算符对易。由于 $|\Psi_\mathbf{k}\rangle$ 是总动量为 $\hbar\mathbf{k}$ 的本征态（假设基态动量为零），而 $|\Psi_{\mathbf{k}'}\rangle$ 是总动量为 $\hbar\mathbf{k}'$ 的本征态，根据量子力学基本原理，当 $\mathbf{k} \neq \mathbf{k}'$ 时，它们之间的哈密顿量矩阵元必定为零 [@problem_id:1099000]：
$$
\langle \Psi_{\mathbf{k}'} | \hat{H} | \Psi_{\mathbf{k}} \rangle = 0 \quad (\text{for } \mathbf{k} \neq \mathbf{k}')
$$
这表明Feynman态是哈密顿量的近似本征态，从而为计算激发能谱提供了坚实的基础。

### Bijl-Feynman 激发能谱

利用变分原理，我们可以估算激发态 $|\Psi_\mathbf{k}\rangle$ 的能量。激发能 $\epsilon_F(k)$ 是该态的能量期望值与基态能量 $E_0$ 之差：
$$
\epsilon_F(k) = \frac{\langle \Psi_\mathbf{k} | \hat{H} | \Psi_\mathbf{k} \rangle}{\langle \Psi_\mathbf{k} | \Psi_\mathbf{k} \rangle} - E_0 = \frac{\langle \Psi_\mathbf{k} | \hat{H} - E_0 | \Psi_\mathbf{k} \rangle}{\langle \Psi_\mathbf{k} | \Psi_\mathbf{k} \rangle}
$$
由于 $\hat{H}|\Psi_0\rangle = E_0|\Psi_0\rangle$，分子可以简化为一个对易子形式：
$$
\langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} (\hat{H} - E_0) \hat{\rho}_{\mathbf{k}} | \Psi_0 \rangle = \langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} [\hat{H}, \hat{\rho}_{\mathbf{k}}] | \Psi_0 \rangle
$$
因此，激发能的表达式为：
$$
\epsilon_F(k) = \frac{\langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} [\hat{H}, \hat{\rho}_{\mathbf{k}}] | \Psi_0 \rangle}{N S(k)}
$$
为了计算这个表达式，我们需要计算对易子 $[\hat{H}, \hat{\rho}_{\mathbf{k}}]$。考虑一个典型的多体哈密顿量，包含动能项 $\hat{T}$ 和仅依赖于粒子间距离的对相互作用势能项 $\hat{V}$：
$$
\hat{H} = \hat{T} + \hat{V} = \sum_{i=1}^N \frac{\hat{\mathbf{p}}_i^2}{2m} + \sum_{1 \le i  j \le N} U(\hat{\mathbf{r}}_i - \hat{\mathbf{r}}_j)
$$
首先，我们考察势能部分的贡献。由于 $\hat{V}$ 和 $\hat{\rho}_{\mathbf{k}}$ 都只依赖于位置算符，它们是可对易的乘法算符，因此 $[\hat{V}, \hat{\rho}_{\mathbf{k}}] = 0$。这意味着在Feynman的简单变分图像中，激发能完全来自于动能的改变，势能部分对激发能的直接贡献为零 [@problem_id:1098933]。

现在我们计算动能部分的对易子 $[\hat{T}, \hat{\rho}_{\mathbf{k}}]$。利用基本对易关系 $[\hat{p}_x, f(x)] = -i\hbar \frac{\partial f}{\partial x}$，经过一番代数运算可以得到：
$$
[\hat{T}, \hat{\rho}_{\mathbf{k}}] = \sum_{j=1}^N \left[ \frac{\hat{\mathbf{p}}_j^2}{2m}, e^{-i\mathbf{k}\cdot\hat{\mathbf{r}}_j} \right] = \sum_{j=1}^N \left( \frac{\hbar^2 k^2}{2m} - \frac{\hbar}{m} \mathbf{k}\cdot\hat{\mathbf{p}}_j \right) e^{-i\mathbf{k}\cdot\hat{\mathbf{r}}_j}
$$
将此结果代入能量分子，得到：
$$
\langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} [\hat{T}, \hat{\rho}_{\mathbf{k}}] | \Psi_0 \rangle = \frac{\hbar^2 k^2}{2m} \langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} \hat{\rho}_{\mathbf{k}} | \Psi_0 \rangle - \frac{\hbar}{m} \sum_j \mathbf{k} \cdot \langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} e^{-i\mathbf{k}\cdot\hat{\mathbf{r}}_j} \hat{\mathbf{p}}_j | \Psi_0 \rangle
$$
由于基态是时间反演不变的，其总动量流为零，因此第二项的期望值为零。于是，我们得到能量分子的表达式：
$$
\langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} [\hat{H}, \hat{\rho}_{\mathbf{k}}] | \Psi_0 \rangle = \frac{\hbar^2 k^2}{2m} \langle \Psi_0 | \hat{\rho}_{-\mathbf{k}} \hat{\rho}_{\mathbf{k}} | \Psi_0 \rangle = \frac{\hbar^2 k^2}{2m} N S(k)
$$
将此结果代入激发能公式，我们便得到了著名的**Bijl-Feynman公式**:
$$
\epsilon_F(k) = \frac{\hbar^2 k^2}{2m S(k)}
$$
这个公式是多体物理学中最优雅和深刻的结果之一。它将一个动力学性质（激发能谱 $\epsilon(k)$）与一个纯粹的静态、结构性质（基态的静态结构因子 $S(k)$）直接联系起来。

值得注意的是，这个能量公式的分子可以通过一个更普适和严格的途径得到，即**f-求和规则**（f-sum rule）。该规则源于对双重对易子 $\langle \Psi_0 | [\hat{\rho}_{\mathbf{k}}^\dagger, [\hat{H}, \hat{\rho}_{\mathbf{k}}]] | \Psi_0 \rangle$ 的计算。对于任何一个速度无关的势能，这个双重对易子的值都是一个与具体相互作用无关的普适常数 [@problem_id:1099013]：
$$
\langle \Psi_0 | [\hat{\rho}_{\mathbf{k}}^\dagger, [\hat{H}, \hat{\rho}_{\mathbf{k}}]] | \Psi_0 \rangle = \frac{N \hbar^2 k^2}{m}
$$
通过在求和规则的表达式中插入完备的能量本征态集，可以证明它等于 $2m$ 乘以动态结构因子 $S(k, \omega)$ 的一阶频率矩。在Feynman的单模图像中，这直接给出了能量分子的精确值，从而为Bijl-Feynman公式提供了更深层次的理论支持。这个分子也与纵向流-流关联函数直接相关，从物理上代表了与密度波相关的总动能 [@problem_id:1098978]。

### 物理内涵与渐进行为

Bijl-Feynman公式 $\epsilon_F(k) = \frac{\hbar^2 k^2}{2m S(k)}$ 的结构极富启发性。分子 $\frac{\hbar^2 k^2}{2m}$ 是一个动量为 $\hbar k$ 的**自由粒子**的能量。分母中的静态结构因子 $S(k)$ 则体现了**多体效应**的修正。

*   **长波极限 (声子)**: 在小波矢 $k \to 0$ 极限下，由于粒子数守恒和流体可压缩性的热力学关系，静态结构因子呈现线性行为 [@problem_id:1098962]：
    $$
    S(k) \approx \frac{\hbar k}{2mc_s} \quad (\text{as } k \to 0)
    $$
    其中 $c_s$ 是系统的声速。将此形式代入Bijl-Feynman公式，得到：
    $$
    \epsilon_F(k) \approx \frac{\hbar^2 k^2}{2m (\hbar k / 2mc_s)} = \hbar c_s k
    $$
    这正是声子（量子化的声波）的线性色散关系。这表明Feynman理论正确地描述了量子流体中的长波长集体激发。

*   **短波极限 (类自由粒子)**: 在大波矢 $k \to \infty$ 极限下，我们探测的是粒子间距极小的尺度。在此尺度下，粒子间的关联变得无关紧要，系统行为趋向于自由粒子。这意味着 $S(k) \to 1$。此时，Feynman能谱趋向于自由粒子的能量：
    $$
    \epsilon_F(k) \approx \frac{\hbar^2 k^2}{2m} \quad (\text{as } k \to \infty)
    $$
    更精确地，对于大$k$，$S(k)$ 的渐近形式通常为 $S(k) = 1 - C/k^4 + \dots$。将此代入Feynman公式并展开，可以得到对自由粒子能谱的领头阶修正 [@problem_id:1098936]：
    $$
    \epsilon_F(k) = \frac{\hbar^2 k^2}{2m(1 - C/k^4)} \approx \frac{\hbar^2 k^2}{2m} (1 + C/k^4) = \frac{\hbar^2 k^2}{2m} + \frac{\hbar^2 C}{2m k^2}
    $$
    这个修正项反映了在高能撞击中粒子间短程排斥势的“硬核”效应。

### 应用与理论验证

Bijl-Feynman理论的巨大成功在于它不仅具有正确的渐进行为，还能对具体的物理系统做出相当准确的预测，并与其他理论形成优美的自洽。

#### 弱相互作用[玻色气体](@entry_id:155364)与Bogoliubov理论

对Bijl-Feynman理论最强有力的验证之一来自于它与弱相互作用[玻色气体](@entry_id:155364)Bogoliubov理论的完美契合。Bogoliubov理论通过对哈密顿量进行二次近似，并进行正则变换，精确地求解了弱相互作用玻色凝聚体的基态和元激发谱。

我们可以反过来，将Bogoliubov理论计算出的基态性质代入Bijl-Feynman公式，看能否重现Bogoliubov的激发谱。在Bogoliubov理论中，可以计算出系统的静态结构因子为 [@problem_id:1099011]：
$$
S_{Bog}(k) = \frac{\epsilon_k^0}{\epsilon_B(k)}
$$
其中 $\epsilon_k^0 = \frac{\hbar^2 k^2}{2m}$ 是自由粒子能量，而 $\epsilon_B(k) = \sqrt{\epsilon_k^0 (\epsilon_k^0 + 2gn_0)}$ 是著名的Bogoliubov激发谱（$g$是相互作用强度，$n_0$是凝聚体密度）。

现在，将这个 $S_{Bog}(k)$ 代入Bijl-Feynman公式：
$$
\epsilon_F(k) = \frac{\hbar^2 k^2}{2m S_{Bog}(k)} = \frac{\epsilon_k^0}{\epsilon_k^0 / \epsilon_B(k)} = \epsilon_B(k)
$$
结果表明，Bijl-Feynman公式精确地重现了Bogoliubov的激发谱！这并非巧合。更深层次的原因在于，对于弱相互作用[玻色气体](@entry_id:155364)，Feynman的变分激发态 $|\Psi_\mathbf{k}\rangle$ 与Bogoliubov理论中的准粒子激发态是**完全相同的**。通过计算这两个归一化态之间的交叠积分（即振子强度 $Z(k)$），可以证明 $Z(k)=1$ [@problem_id:1098941]。这解释了为什么变分法在这种情况下能够给出精确解：因为变分试验函数恰好就是真实的本征态。

#### 从能谱到结构

Bijl-Feynman公式的威力还在于其可逆性。如果我们通过实验（如中子散射）或唯象理论得到了激发谱 $\epsilon(k)$，我们就可以反推出基态的静态结构因子 $S(k) = \frac{\hbar^2 k^2}{2m \epsilon(k)}$。这为我们提供了一条从动力学性质探测静态结构的途径。

例如，对于一个具有Bogoliubov谱的系统，我们可以反向推导出其$S(k)$ [@problem_id:1098982]。对于真实的液氦，其著名的声子-roton（旋子）谱曲线也可以用来预测$S(k)$的形状。将唯象的Landau旋子谱 $E(k) = \Delta + \frac{\alpha}{2}(k-k_0)^2$ 代入，就可以计算出在旋子极小值附近$S(k)$的行为，并预测其峰值位置和大小 [@problem_id:1098946]。一旦$S(k)$被确定，就可以进一步计算其他基态性质，例如关联能等，展示了激发谱与基态热力学性质之间的深刻联系 [@problem_id:1098982]。

#### 与动态结构因子的关系

Feynman的理论本质上是一个**单模近似**（Single-Mode Approximation, SMA）。它假设对于给定的动量 $\hbar\mathbf{k}$，所有的激发谱权重都集中在一个单一的、能量为 $\epsilon_F(k)$ 的锐利激发峰上。用动态结构因子 $S(\mathbf{k}, \omega)$ 来描述，即：
$$
S_{SMA}(\mathbf{k}, \omega) = S(k) \delta(\omega - \epsilon_F(k)/\hbar)
$$
这个近似自动满足了动态结构因子的零阶矩（定义了$S(k)$）和一阶矩（f-求和规则）。然而，对于更高阶的频率矩，SMA的预测可能偏离精确的求和规则结果，偏差的大小反映了真实谱中多模激发（多声子过程）的重要性 [@problem_id:1098953] [@problem_id:1098962]。类似地，通过Kramers-Kronig关系，可以用$S(\mathbf{k}, \omega)$计算系统的响应函数，如静态磁化率$\chi(\mathbf{k})$。SMA提供了一种简便的估算方法，其准确性取决于单模图像的有效性 [@problem_id:1098996]。

### 超越单模近似：激发与相互作用

尽管Bijl-Feynman理论取得了巨大成功，但它毕竟是一个近似。其核心的变分波函数 $\hat{\rho}_\mathbf{k}|\Psi_0\rangle$ 过于简单。例如，它预测的液氦旋子能量约为实验值的两倍。这表明需要更精致的变分波函数。

#### 背流与Feynman-Cohen理论

Feynman和Cohen意识到，当一个原子在流体中移动时，周围的原子会协同运动以“填补”它留下的空隙，这种效应被称为**背流**（backflow）。在Feynman激发态的基础上引入描述背流的修正项，可以构造出Feynman-Cohen (FC) 变分波函数。这极大地改善了变分能量，特别是对旋子区域的描述。一个唯象的FC能量可以表示为：
$$
E_{FC}(k) = \frac{\epsilon_F(k)}{1+B(k)}
$$
其中$B(k)$是一个描述背流效应的函数。值得注意的是，虽然$E_{FC}(k)$更准确，但如果将其用于单模近似，将不再严格满足f-求和规则 [@problem_id:1098960]。这揭示了一个深刻的道理：激发谱的改进必须伴随着对激发态波函数本身的更深入理解，单模图像本身可能已经不足。

#### 多声子态及其相互作用

真实的量子流体不仅存在单个元激发，还存在多个元激发同时存在的状态，以及它们之间的相互作用。最简单的多激发态可以由多个密度算符作用于基态来构造，例如双声子态 $|\Psi_{\mathbf{k}_1, \mathbf{k}_2}\rangle = \hat{\rho}_{\mathbf{k}_1}\hat{\rho}_{\mathbf{k}_2}|\Psi_0\rangle$。

计算这些多声子态的性质，如归一化系数和能量，不可避免地会涉及到高阶关联函数，如三点和四点结构因子 [@problem_id:1098965]。在随机相位近似(RPA)等近似下，可以得到双声子态的激发能。其能量通常不等于两个单声子能量之和，差值即为**相互作用能** $\delta E_{12}$ [@problem_id:1098968]。这表明Feynman声子并非理想的玻色子，它们之间存在残余的相互作用。

这种相互作用可以导致一个声子衰变为两个或多个其他声子。描述这类过程的跃迁矩阵元，例如 $\langle\Psi_{\mathbf{q}, \mathbf{k}-\mathbf{q}}|\hat{V}|\Psi_{\mathbf{k}}\rangle$，与系统的三体关联性质直接相关 [@problem_id:1098956]。对这些相互作用的深入研究，是理解量子流体输运性质和有限温度下行为的关键。

最后，一旦激发谱（无论是简单的Feynman谱还是更精确的实验谱）被确定，它就可以用来计算系统的宏观热力学性质。例如，通过对所有模式的零点能求和，可以估算基态能量的关联部分；通过考虑有限温度下的热占据，可以计算比热等物理量 [@problem_id:1098985]。这充分体现了元激发概念作为连接微观动力学与宏观热力学桥梁的核心作用。