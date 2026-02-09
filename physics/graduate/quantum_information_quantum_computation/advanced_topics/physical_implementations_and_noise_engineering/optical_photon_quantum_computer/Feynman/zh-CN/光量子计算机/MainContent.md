## 引言
我们正处在一场新计算革命的黎明，而基于光的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机是这场变革中最有前途的选手之一。它们承诺以光速处理信息，并能天然地抵抗某些类型的噪声。但是，我们究竟如何用纯粹的光来构建一台功能强大的计算机？从单个[光子](@keyword=photon|lang=zh-CN|style=Feynman)到一个可编程的设备，这条道路上充满了哪些深刻的物理挑战和精妙的工程智慧？

本文旨在系统地回答这些问题，为你揭开[光学量子计算机](@keyword=optical_quantum_computer|lang=zh-CN|style=Feynman)的神秘面纱。我们将带领你踏上一段从基本原理到前沿应用的旅程，深入探索这个融合了量子力学、[光学工程](@keyword=optical_engineering|lang=zh-CN|style=Feynman)和信息科学的迷人领域。

- 在第一部分“**原理与机制**”中，我们将像钟表匠一样拆解这台未来的机器，探究其核心构件：[光子](@keyword=photon|lang=zh-CN|style=Feynman)如何成为[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，如何按需制造单个[光子](@keyword=photon|lang=zh-CN|style=Feynman)，以及如何巧妙地让它们相互“交谈”以执行逻辑运算。

- 接着，在“**应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系**”部分，我们将把目光投向远方，探索这台强大的机器能够解决哪些独一无二的问题，它如何帮助我们模拟宇宙的奥秘，以及它如何与凝聚态物理、宇宙学乃至生物学等领域产生惊人的交集。

- 最后，“**动手实践**”部分将为你提供一系列精心设计的问题，让你有机会亲自运用所学知识，加深对[光子](@keyword=photon|lang=zh-CN|style=Feynman)干涉、资源态构建和量子测量等核心概念的理解。

现在，让我们一同启程，进入这个由[光子](@keyword=photon|lang=zh-CN|style=Feynman)编织的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)世界。

## 原理与机制

在上一章中，我们对[光学量子计算机](@keyword=optical_quantum_computer|lang=zh-CN|style=Feynman)的宏伟蓝图有了初步的认识。现在，让我们像钟表匠拆解一枚精密的怀表一样，深入其内部，探究那些驱动这台未来机器运转的核心原理与机制。这趟旅程将充满惊喜，因为我们将看到，大自然最优美的法则，是如何在一个个微小的光学元件中被巧妙地驾驭和编排的。

### [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的化身：[光子](@keyword=photon|lang=zh-CN|style=Feynman)

想象一下用纯粹的光来建造一台计算机。这听起来像是科幻小说，但它正是光学[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的核心思想。我们选择的主角，就是光的量子化身——**[光子](@keyword=photon|lang=zh-CN|style=Feynman)**。为什么是[光子](@keyword=photon|lang=zh-CN|style=Feynman)？首先，它们是宇宙中最快的信使，以光速飞行，这意味着信息处理的潜力速度极快。其次，它们天生“不合群”，很难与其他物质发生相互作用，这使得它们在传输过程中能很好地保持自身的[量子状态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，免受环境噪声的干扰。

然而，凡事皆有两面性。[光子](@keyword=photon|lang=zh-CN|style=Feynman)的这种“孤僻”性格也带来了最大的挑战：如何让它们相互“交谈”以执行计算？毕竟，计算机的核心在于[逻辑门](@keyword=logic_gates|lang=zh-CN|style=Feynman)，而逻辑门需要比特之间发生相互作用。这便是我们整个探索之旅中需要不断面对和解决的核心矛盾。

为了将[光子](@keyword=photon|lang=zh-CN|style=Feynman)变成[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)（qubit），我们需要给它赋予两种可以区分的状态，来代表量子世界里的 $|0\rangle$ 和 $|1\rangle$。最常见的方法有两种：

1.  **偏振编码**：利用[光子](@keyword=photon|lang=zh-CN|style=Feynman)的偏振方向。例如，我们可以定义水平偏振 $|H\rangle$ 为 $|0\rangle$，垂直偏振 $|V\rangle$ 为 $|1\rangle$。
2.  **路径编码（[双轨编码](@keyword=dual_rail_encoding|lang=zh-CN|style=Feynman)）**：利用[光子](@keyword=photon|lang=zh-CN|style=Feynman)在空间中的位置。想象一个[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)有两条路径，上路径和下路径。我们可以定义[光子](@keyword=photon|lang=zh-CN|style=Feynman)走上路径为 $|0\rangle$，走下路径为 $|1\rangle$。

现在，我们有了[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)。接下来，我们需要解决如何创造它们，以及如何让它们相互作用。

### 构建基础：量子源与逻辑门

如同任何建筑都需要砖块和水泥，[光学量子计算机](@keyword=optical_quantum_computer|lang=zh-CN|style=Feynman)也需要最基本的构件：可靠的[单光子源](@keyword=single_photon_source|lang=zh-CN|style=Feynman)和能操纵它们的[量子逻辑门](@keyword=quantum_logic_gates|lang=zh-CN|style=Feynman)。

#### 制造单[光子](@keyword=photon|lang=zh-CN|style=Feynman)：“宣告”的技巧

你可能会想，制造一个单[光子](@keyword=photon|lang=zh-CN|style=Feynman)，不就像打开一个很暗的手电筒，让[光子](@keyword=photon|lang=zh-CN|style=Feynman)一个一个出来吗？事实远非如此简单。一个极其微弱的光源，其[光子](@keyword=photon|lang=zh-CN|style=Feynman)数的分布遵循[泊松分布](@keyword=poisson_distribution|lang=zh-CN|style=Feynman)，这意味着你总是有一定概率同时得到零个、一个、两个或更多的[光子](@keyword=photon|lang=zh-CN|style=Feynman)。而对于[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)，我们需要的是一个“按需”的、确定的[单光子源](@keyword=single_photon_source|lang=zh-CN|style=Feynman)。

为了解决这个问题，物理学家们发明了一种绝妙的技巧，名为**预告（heralding）**。这个想法源于一个称为**[自发参量下转换](@keyword=spontaneous_parametric_down_conversion|lang=zh-CN|style=Feynman)（SPDC）**或**自发[四波混频](@keyword=four_wave_mixing|lang=zh-CN|style=Feynman)（SFWM）**的[非线性光学](@keyword=nonlinear_optics|lang=zh-CN|style=Feynman)过程。在这个过程中，一个高能量的“泵浦”[光子](@keyword=photon|lang=zh-CN|style=Feynman)进入一块特殊的晶体后，会分裂成一对能量较低的孪生[光子](@keyword=photon|lang=zh-CN|style=Feynman)，我们称之为“信号[光子](@keyword=photon|lang=zh-CN|style=Feynman)”和“闲置[光子](@keyword=photon|lang=zh-CN|style=Feynman)”。

这对孪生[光子](@keyword=photon|lang=zh-CN|style=Feynman)是“心有灵犀”的，它们总是一同产生。于是，我们可以把一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)（比如闲置[光子](@keyword=photon|lang=zh-CN|style=Feynman)）送到一个探测器上。当这个探测器“咔哒”一响，它就像一个信使在向我们“宣告”：它的孪生兄弟——信号[光子](@keyword=photon|lang=zh-CN|style=Feynman)——此刻已经诞生，并且正沿着预设的路径飞来！这样，我们就得到了一个被“宣告”的单[光子](@keyword=photon|lang=zh-CN|style=Feynman)。

然而，现实世界总比理想模型要复杂。如果我们为了提高产生[光子](@keyword=photon|lang=zh-CN|style=Feynman)对的效率而增强泵浦光的功率，晶体偶尔会“过于激动”，一次产生*两对*甚至更多的孪生[光子](@keyword=photon|lang=zh-CN|style=Feynman)。这时，即使闲置[光子](@keyword=photon|lang=zh-CN|style=Feynman)的探测器只响了一声（因为它可能无法分辨一个还是两个[光子](@keyword=photon|lang=zh-CN|style=Feynman)），我们以为的“单[光子](@keyword=photon|lang=zh-CN|style=Feynman)”信号光路中，实际上可能存在两个[光子](@keyword=photon|lang=zh-CN|style=Feynman)。

这种多[光子](@keyword=photon|lang=zh-CN|style=Feynman)“污染”是[单光子源](@keyword=single_photon_source|lang=zh-CN|style=Feynman)质量的关键指标，可以用**[二阶相干函数](@keyword=second_order_coherence_function|lang=zh-CN|style=Feynman) $g^{(2)}(0)$** 来衡量。对于一个完美的[单光子源](@keyword=single_photon_source|lang=zh-CN|style=Feynman)，$g^{(2)}(0)$ 应该为零。而对于一个通过 SPDC 过程产生的预告[单光子源](@keyword=single_photon_source|lang=zh-CN|style=Feynman)，如果产生[光子](@keyword=photon|lang=zh-CN|style=Feynman)对的概率为 $p$，其 $g^{(2)}(0)$ 值恰好为 $2p$ ([@problem_id:107144])。这意味着产生概率越高，光源的多[光子](@keyword=photon|lang=zh-CN|style=Feynman)“噪声”就越大。同样，在基于 SFWM 的光源中， heralded 信号[光子](@keyword=photon|lang=zh-CN|style=Feynman)模式中出现两个[光子](@keyword=photon|lang=zh-CN|style=Feynman)与一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)的概率之比，会随着泵浦功率的增强而增大 ([@problem_id:107025])。这揭示了一个根本性的权衡：在光学[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)中，我们需要在“数量”和“质量”之间做出精妙的平衡。

#### 让[光子](@keyword=photon|lang=zh-CN|style=Feynman)相互作用：挑战的核心

有了单[光子](@keyword=photon|lang=zh-CN|style=Feynman)，我们如何让它们执行逻辑运算？这触及了光学[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的核心难题。

##### A. 线性光学与干涉的力量

既然[光子](@keyword=photon|lang=zh-CN|style=Feynman)之间不直接作用，物理学家们转向了它们最本质的量子特性：**干涉**。当两个或多个[光子](@keyword=photon|lang=zh-CN|style=Feynman)在路径上相遇时，它们的[概率幅](@keyword=probability_amplitude|lang=zh-CN|style=Feynman)会发生干涉，导致一些看似不可思议的后果。

最经典的例子是**洪-欧-曼德尔（Hong-Ou-Mandel）效应**。想象一个简单的50:50**分束器**——一个光学版本的十字路口。如果两个完全相同（无法区分）的[光子](@keyword=photon|lang=zh-CN|style=Feynman)同时从两个不同的输入端口进入这个[分束器](@keyword=beam_splitter|lang=zh-CN|style=Feynman)，你可能会以为它们各有50%的概率从任意一个输出端口出来。但量子力学的预测令人惊讶：它们总是会“抱团”从同一个输出端口出来！它们的[概率幅](@keyword=probability_amplitude|lang=zh-CN|style=Feynman)发生了相消干涉，使得它们分开走的情况永远不会发生。

这种[量子干涉](@keyword=quantum_interference|lang=zh-CN|style=Feynman)是线性光学计算的基石。通过设计由多个[分束器](@keyword=beam_splitter|lang=zh-CN|style=Feynman)和[移相器](@keyword=phase_shifter|lang=zh-CN|style=Feynman)组成的复杂**[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)**，我们可以实现多[光子](@keyword=photon|lang=zh-CN|style=Feynman)间的复杂干涉模式。例如，在一个实现所谓“离散傅里叶变换”的三端口干涉仪中，输入 $|1,1,0\rangle$（即端口1和2各有一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)）态，它散射到输出 $|1,0,1\rangle$ 态的概率可以通过计算一个特定子矩阵的**积和式（permanent）**得到，结果为 $1/9$ ([@problem_id:107048])。当我们将三个不可区分的[光子](@keyword=photon|lang=zh-CN|style=Feynman)注入一个四端口[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)时，它们全部“挤”在同一个输出端口的概率也可以被精确计算出来 ([@problem_id:107089])。这些计算的背后，都隐藏着比经典概率论更深刻的[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)统计规律。

##### B. 非线性光学：难以捉摸的直接互动

虽然线性[光学干涉](@keyword=optical_interference|lang=zh-CN|style=Feynman)非常强大，但仅靠它本身，无法构建通用的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机。我们需要一个真正的**受控逻辑门**，即一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)的状态能控制另一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)的状态。

一种看似直接的方法是利用**[非线性光学](@keyword=nonlinear_optics|lang=zh-CN|style=Feynman)介质**。在这种介质中，一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)的存在可以稍微改变介质的[折射率](@keyword=refractive_index|lang=zh-CN|style=Feynman)，从而影响后来[光子](@keyword=photon|lang=zh-CN|style=Feynman)的相位。这就是所谓的**[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)克尔（cross-Kerr）非线性效应**。理论上，我们可以利用它来实现一个受控相位（CZ）门：仅当两个[光子](@keyword=photon|lang=zh-CN|style=Feynman)同时存在时，才给系统施加一个特定的相移。

然而，这种效应在单一[光子](@keyword=photon|lang=zh-CN|style=Feynman)层面上极其微弱。更重要的是，它要求两个[光子](@keyword=photon|lang=zh-CN|style=Feynman)波包在时间和空间上完美重叠。如果两个[光子](@keyword=photon|lang=zh-CN|style=Feynman)脉冲的到达时间有微小的延迟 $\tau$，它们之间的相互作用就会减弱，所施加的相位就不再是理想值，导致[逻辑门](@keyword=logic_gates|lang=zh-CN|style=Feynman)的保真度下降 ([@problem_id:106996])。这凸显了利用非线性效应制造确定性[光子](@keyword=photon|lang=zh-CN|style=Feynman)逻辑门在工程上的巨大挑战。

##### C. [腔量子电动力学](@keyword=cavity_quantum_electrodynamics|lang=zh-CN|style=Feynman)：寻找中间人

为了实现更强的相互作用，研究人员转向了一种更巧妙的方案：找一个“中间人”。这个中间人通常是一个被囚禁在两个高[反射率](@keyword=reflectance|lang=zh-CN|style=Feynman)镜片（形成一个**[光学微腔](@keyword=optical_microcavity|lang=zh-CN|style=Feynman)**）之间的**原子**。

其工作原理大致如下：第一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)进入微腔，与原子发生强烈相互作用，改变原子的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。然后，当第二个[光子](@keyword=photon|lang=zh-CN|style=Feynman)进入微腔时，它“看到”的是一个状态已经改变的原子，因此它与原子相互作用的方式也随之改变。[光子](@keyword=photon|lang=zh-CN|style=Feynman)离开后，原子的状态可以恢复。通过这种方式，第一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)间接地影响了第二个[光子](@keyword=photon|lang=zh-CN|style=Feynman)，实现了它们之间的逻辑门操作。实现这种[强相互作用](@keyword=strong_nuclear_force|lang=zh-CN|style=Feynman)的前提是，[光子](@keyword=photon|lang=zh-CN|style=Feynman)能够被原子-微腔系统高效地吸收和释放。在特定条件下，通过精确调节系统参数，可以让入射[光子](@keyword=photon|lang=zh-CN|style=Feynman)被完美吸收，这是实现高效[量子逻辑门](@keyword=quantum_logic_gates|lang=zh-CN|style=Feynman)的关键一步 ([@problem_id:107149])。

### 计算机的蓝图：测量驱动的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)

直接用[光子](@keyword=photon|lang=zh-CN|style=Feynman)搭建像经典计算机那样的电路（所谓的“线路模型”）非常困难。因此，一种截然不同的计算[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)——**[基于测量的量子计算](@keyword=measurement_based_quantum_computing|lang=zh-CN|style=Feynman)（MBQC）**，或称**[单向量子计算](@keyword=one_way_quantum_computing|lang=zh-CN|style=Feynman)**——在光学领域大放异彩。

这个模型的思想非常革命性：计算过程被分为两步。首先，不惜代价地制备一个巨大且高度纠缠的“资源态”，通常是**[簇态](@keyword=cluster_states|lang=zh-CN|style=Feynman)（cluster state）**。这个[簇态](@keyword=cluster_states|lang=zh-CN|style=Feynman)就像一块空白的画布。然后，真正的计算过程，仅仅是在这块“画布”上进行一系列的单[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)**测量**。你选择测量哪个比特、以及在什么基底下测量，就决定了你在执行什么[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)。测量过程会消耗掉这个资源态，因此它被称为“单向”计算。

#### 编织资源：[簇态](@keyword=cluster_states|lang=zh-CN|style=Feynman)的融合

如何制备巨大的[簇态](@keyword=cluster_states|lang=zh-CN|style=Feynman)？一个强大的技术是“**融合**”。我们可以先制备许多小的[纠缠态](@keyword=entangled_state|lang=zh-CN|style=Feynman)（比如双[光子](@keyword=photon|lang=zh-CN|style=Feynman)贝尔态或三[光子](@keyword=photon|lang=zh-CN|style=Feynman) GHZ 态），然后像拼接积木一样，通过在不同小[纠缠态](@keyword=entangled_state|lang=zh-CN|style=Feynman)的成员之间进行特定的贝尔基测量（BSM），将它们“粘合”成一个更大的[簇态](@keyword=cluster_states|lang=zh-CN|style=Feynman)。

有趣的是，这个融合过程通常是**概率性**的。贝尔基测量有四种可能的结果，并非每种结果都能成功地将[簇态](@keyword=cluster_states|lang=zh-CN|style=Feynman)连接起来。例如，在尝试将两个三[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的[簇态](@keyword=cluster_states|lang=zh-CN|style=Feynman)融合成一个四[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的线性[簇态](@keyword=cluster_states|lang=zh-CN|style=Feynman)时，根据测量结果的不同，我们需要对剩下的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)进行不同的“修正”操作。在某些情况下，修正操作非常简单，我们称之为成功；在另一些情况下，则可能失败。你可能需要进行多次尝试，直到获得成功的测量结果。计算表明，利用特定的融合方案，成功的总概率可能为 $1/2$ ([@problem_id:107038])。这个概率取决于具体的物理实现细节，比如所用分束器的类型 ([@problem_id:107053])。这种概率性是光学[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的一个内在特征，也是它与许多其他平台的重要区别。

#### 运行程序：测量的力量

一旦我们有了[簇态](@keyword=cluster_states|lang=zh-CN|style=Feynman)资源，计算就变得异常“简单”：只需测量。举个例子，在一个三[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的线性[簇态](@keyword=cluster_states|lang=zh-CN|style=Feynman)上实现一个单比特的转动操作，需要依次对第一个和第二个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)进行特定角度的测量。

这个过程的精妙之处在于，第一个测量的结果会影响第二个测量的基底选择，形成一种“前馈”机制。然而，这也意味着任何控制上的误差都会直接影响计算结果。假设在执行一个旨在实现绕Z轴旋转 $R_z(\theta)$ 的操作时，我们对第一个比特的测量基底有一个微小的角度误差 $\delta$。这个小小的失误，会导致最终输出到第三个比特上的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)与理想态的保真度下降为 $\cos^2(\delta/2)$ ([@problem_id:107116])。这清晰地展示了在 MBQC 框架下，精确的[量子测量](@keyword=quantum_measurement|lang=zh-CN|style=Feynman)控制是何等重要。

### 共同的敌人：驯服噪声与损耗

建造一台能工作的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机，就像在暴风雨中搭建一座精巧的纸牌屋。我们必须时刻与各种错误来源作斗争。在光学平台中，最主要的敌人是[光子](@keyword=photon|lang=zh-CN|style=Feynman)损耗和[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)。

#### 最大的难题：[光子](@keyword=photon|lang=zh-CN|style=Feynman)丢失

[光子](@keyword=photon|lang=zh-CN|style=Feynman)不爱相互作用的特性使它们成为优秀的量子信息载体，但也使它们极易在[光纤](@keyword=optical_fiber|lang=zh-CN|style=Feynman)或光学元件中被吸收或散射掉，从而“丢失”。一个多比特的计算中，哪怕只丢失了一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)，也可能导致整个计算失败。

幸运的是，[光子](@keyword=photon|lang=zh-CN|style=Feynman)丢失是一种**可擦除错误**。以[双轨编码](@keyword=dual_rail_encoding|lang=zh-CN|style=Feynman)为例，一个物理量子比特由两个模式中恰好一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)来表示。如果在这个双轨中我们一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)都探测不到，我们就明确地知道这个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的信息被“擦除”了。我们知道错误发生了，也知道它发生在哪里。

这使得纠错变得相对容易。我们可以使用**[重复码](@keyword=repetition_code|lang=zh-CN|style=Feynman)**来保护信息。例如，将一个逻辑量子比特的信息编码到三个双轨物理量子比特上。如果其中一个物理量子比特因为[光子](@keyword=photon|lang=zh-CN|style=Feynman)丢失而被擦除，我们只需对剩下的两个完好的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)进行测量，并采用“少数服从多数”的原则，就能恢复出原始的逻辑状态 ([@problem_id:107017])。这种主动的**[量子纠错](@keyword=quantum_error_correction|lang=zh-CN|style=Feynman)**策略，是通往大规模、[容错](@keyword=fault_tolerance|lang=zh-CN|style=Feynman)光学[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的必由之路。

#### [隐形](@keyword=cloaking|lang=zh-CN|style=Feynman)的敌人：[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)

即使[光子](@keyword=photon|lang=zh-CN|style=Feynman)没有丢失，它的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)也可能被环境“污染”，这个过程称为**退相干**。

想象一下，我们想利用两个不同路径产生的 $|HV\rangle$ 和 $|VH\rangle$ 来制备一个完美的偏振[纠缠态](@keyword=entangled_state|lang=zh-CN|style=Feynman)。如果因为技术不完美，导致其中一条路径的[光子](@keyword=photon|lang=zh-CN|style=Feynman)比另一条晚到了一点点，这个时间上的**可区分性**就会像一个窃听者，泄露了[光子](@keyword=photon|lang=zh-CN|style=Feynman)的“来源路径”信息。根据量子力学的基本原理，“哪条路径”信息会削弱甚至摧毁干涉效应，从而降低了最终态的纠缠度 ([@problem_id:107140])。同样，如果一个处于不同时间[模式叠加](@keyword=superposition_of_modes|lang=zh-CN|style=Feynman)态的[光子](@keyword=photon|lang=zh-CN|style=Feynman)，其一部分在[光纤](@keyword=optical_fiber|lang=zh-CN|style=Feynman)中经历了**[色散](@keyword=frequency_dispersion|lang=zh-CN|style=Feynman)**，导致[波包](@keyword=wave_packets|lang=zh-CN|style=Feynman)变形，它也会与未经历[色散](@keyword=frequency_dispersion|lang=zh-CN|style=Feynman)的部分产生可区分性，从而导致整个系统纯度的下降 ([@problem_id:107067])。

另一种常见的噪声源是**[相位噪声](@keyword=phase_noise|lang=zh-CN|style=Feynman)**。例如，在一个由[马赫-曾德干涉仪](@keyword=mach_zehnder_interferometer|lang=zh-CN|style=Feynman)构成的[量子逻辑门](@keyword=quantum_logic_gates|lang=zh-CN|style=Feynman)中，如果用于调控的[移相器](@keyword=phase_shifter|lang=zh-CN|style=Feynman)受到[温度波](@keyword=temperature_wave|lang=zh-CN|style=Feynman)动等经典噪声的干扰，其施加的相位 $\phi$ 会随机[抖动](@keyword=dither|lang=zh-CN|style=Feynman)。这种[抖动](@keyword=dither|lang=zh-CN|style=Feynman)会“冲刷”掉[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)的[相干性](@keyword=coherence|lang=zh-CN|style=Feynman)，使得一个原本[纯态](@keyword=pure_states|lang=zh-CN|style=Feynman)的输入，经过这个有噪声的门之后，变成了一个保真度较低的混合态 ([@problem_id:106991])。

然而，聪明的编码方案可以帮助我们对抗这类噪声。[双轨编码](@keyword=dual_rail_encoding|lang=zh-CN|style=Feynman)就是一个绝佳的例子。逻辑信息被编码在两根[光纤](@keyword=optical_fiber|lang=zh-CN|style=Feynman)中[光子](@keyword=photon|lang=zh-CN|style=Feynman)的*相对*相位上。如果环境导致两根[光纤](@keyword=optical_fiber|lang=zh-CN|style=Feynman)同时经历了相同的相位[抖动](@keyword=dither|lang=zh-CN|style=Feynman)（即所谓的**[共模噪声](@keyword=common_mode_noise|lang=zh-CN|style=Feynman)**），这个[抖动](@keyword=dither|lang=zh-CN|style=Feynman)对于两根[光纤](@keyword=optical_fiber|lang=zh-CN|style=Feynman)而言是相同的，它们的[相对相位](@keyword=relative_phase|lang=zh-CN|style=Feynman)差则保持不变！因此，[逻辑量子比特](@keyword=logical_qubits|lang=zh-CN|style=Feynman)的信息得以完美保存。通过设计，我们可以使得系统的保真度只对两根[光纤](@keyword=optical_fiber|lang=zh-CN|style=Feynman)的*差异*噪声敏感，而对[共模噪声](@keyword=common_mode_noise|lang=zh-CN|style=Feynman)免疫 ([@problem_id:107085])。这体现了一种被动式的、从硬件设计层面就内建的[纠错](@keyword=error_correction|lang=zh-CN|style=Feynman)智慧。

在这一章中，我们从[光子](@keyword=photon|lang=zh-CN|style=Feynman)的基本属性出发，一路探索了如何制造它们、如何让它们相互作用、如何将它们组织成计算机，以及如何保护它们免受错误的侵扰。我们看到，光学[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的道路充满了挑战，但也充满了基于深刻物理原理的精妙解决方案。这正是一场在光的王国里，集物理洞察与工程智慧于一体的伟大冒险。