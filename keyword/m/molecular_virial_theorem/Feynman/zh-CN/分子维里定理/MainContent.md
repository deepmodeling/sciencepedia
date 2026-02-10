## 引言
[维里定理](@keyword=virial_theorem|lang=zh-CN|style=Feynman)是物理学和化学的一项基石性原理，但其在理解[化学键合](@keyword=chemical_bonding|lang=zh-CN|style=Feynman)方面的深刻内涵常常被低估。许多化学家持有一种简单的成键模型：原子相互靠近，势能降低，形成稳定的分子。然而，这幅图景在根本上是不完整的，它掩盖了一个更微妙、更引人入胜的现实。本文深入探讨[分子维里定理](@keyword=molecular_virial_theorem|lang=zh-CN|style=Feynman)，以纠正这一观点，揭示支配[分子稳定性](@keyword=molecular_stability|lang=zh-CN|style=Feynman)的[动能与势能](@keyword=kinetic_and_potential_energy|lang=zh-CN|style=Feynman)之间错综复杂的相互作用。我们将首先剖析该定理的核心原理和机制，揭示形成[化学键](@keyword=chemical_bonds|lang=zh-CN|style=Feynman)时令人惊讶的能量“代价”。随后，我们将探索其广泛应用，从[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)中的实用诊断工具，到连接分子、气体乃至恒星的概念桥梁。让我们从审视这一宇宙[平衡](@keyword=equilibrium|lang=zh-CN|style=Feynman)法则的普适规则开始。

## 原理与机制

好了，让我们开始深入探讨。我们已经了解了[维里定理](@keyword=virial_theorem|lang=zh-CN|style=Feynman)的概念，现在我们将对其进行剖析，看看它是如何运作的。它不仅仅是一个陈旧的方程，而是一条关于维系万物聚合的本质的深刻原理。它讲述了一个关于[平衡](@keyword=equilibrium|lang=zh-CN|style=Feynman)、关于稳定性的惊人代价、以及关于分子内部空间[精细结构](@keyword=fine_structure|lang=zh-CN|style=Feynman)的故事。和所有好故事一样，它也有一些出人意料的转折。

### 宇宙的[平衡](@keyword=equilibrium|lang=zh-CN|style=Feynman)法则

首先，让我们从宏观视角来看。想象任何一个由力维系的[粒子系统](@keyword=system_of_particles|lang=zh-CN|style=Feynman)——一个由[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)束缚的太阳系，或一个由[电场力](@keyword=electric_forces|lang=zh-CN|style=Feynman)束缚的原子。体系中存在两种相互对立的基本趋势。一方面是**[动能](@keyword=kinetic_energy|lang=zh-CN|style=Feynman)** ($T$)，即运动的能量。你可以把它看作是“延展”的能量。如果你试图将一个粒子限制在更小的空间里，它会更剧烈地[振动](@keyword=vibrational_motion|lang=zh-CN|style=Feynman)——其[动能](@keyword=kinetic_energy|lang=zh-CN|style=Feynman)会增加。另一方面是**势能** ($V$)，在我们的讨论中，这是吸引的能量。这是“[收缩](@keyword=retraction|lang=zh-CN|style=Feynman)”的能量。对于[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)和[电磁力](@keyword=electromagnetic_forces|lang=zh-CN|style=Feynman)，当物体相互靠近时，这种[吸引势](@keyword=attractive_potential|lang=zh-CN|style=Feynman)会变得更强（更负）。

一个稳定的束缚系统——比如地球绕太阳运行，或者[电子](@keyword=electrons|lang=zh-CN|style=Feynman)绕[原子核](@keyword=nucleus|lang=zh-CN|style=Feynman)运行——就是这场对立中的一种休战状态。[维里定理](@keyword=virial_theorem|lang=zh-CN|style=Feynman)就是定义这种休战条款的协定。它指出，对于一个由力维系的系统，若其势能与距离 $R$ 的幂成正比，即 $V \propto R^n$，那么其长[时间平均](@keyword=time_averages|lang=zh-CN|style=Feynman)[动能和势能](@keyword=kinetic_and_potential_energy|lang=zh-CN|style=Feynman)被锁定在一个严格的关系中：$2\langle T \rangle = n \langle V \rangle$。

现在，事情变得有趣了。对于[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)和[库仑力](@keyword=coulomb_force|lang=zh-CN|style=Feynman)，势能与 $1/R^1$ 成比例，所以我们必须小心。力与 $1/R^2$ 成比例，而势能与 $-1/R$ 成比例。因此，势能是次数为 $n = -1$ 的齐次函数。将此代入我们的协定，便得到著名的结果：

$$
2\langle T \rangle + \langle V \rangle = 0
$$

这对[总能量](@keyword=total_energy|lang=zh-CN|style=Feynman) $\langle E \rangle = \langle T \rangle + \langle V \rangle$ 意味着什么呢？我们可以将 $\langle V \rangle = -2\langle T \rangle$ 代入总[能量方程](@keyword=energy_equation|lang=zh-CN|style=Feynman)，得到 $\langle E \rangle = \langle T \rangle - 2\langle T \rangle = -\langle T \rangle$。由于[动能](@keyword=kinetic_energy|lang=zh-CN|style=Feynman) $\langle T \rangle$ 始终为正（物体在运动！），任何由[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)或[库仑力](@keyword=coulomb_force|lang=zh-CN|style=Feynman)维系的稳定束缚系统的[总能量](@keyword=total_energy|lang=zh-CN|style=Feynman)*必定为负*。这就是这类系统能够自我维持的原因！

与此相反，考虑一个由[理想](@keyword=ideals|lang=zh-CN|style=Feynman)弹簧维系的假想系统，其势能与距离的平方成正比，即 $V \propto R^2$。此时 $n=2$，[维里定理](@keyword=virial_theorem|lang=zh-CN|style=Feynman)将是 $2\langle T \rangle = 2\langle V \rangle$，即 $\langle T \rangle = \langle V \rangle$。[总能量](@keyword=total_energy|lang=zh-CN|style=Feynman)将是 $\langle E \rangle = \langle T \rangle + \langle V \rangle = 2\langle T \rangle$，它始终为正。这样的系统不会自然形成一个稳定的束缚体；它要么会分崩离析，要么会坍缩成一个点 [@problem_id:2465649]。一个稳定的原子或分子存在的可能性本身，就根植于[库仑势](@keyword=coulomb_potential|lang=zh-CN|style=Feynman)的 $1/R$ 特性以及由此产生的维里协定条款。

### [化学键](@keyword=chemical_bonds|lang=zh-CN|style=Feynman)的惊人代价

现在，让我们把视线从宇宙[拉回](@keyword=pullbacks|lang=zh-CN|style=Feynman)到单个[化学键](@keyword=chemical_bonds|lang=zh-CN|style=Feynman)上。我们对成键有一个简单直观的印象：两个原子相互靠近，形成一个[化学键](@keyword=chemical_bonds|lang=zh-CN|style=Feynman)，体系的能量降低。这就像一个球滚到山底。最终状态的势能更低，仅此而已。

事实证明，这幅图景是危险且不完整的。[维里定理](@keyword=virial_theorem|lang=zh-CN|style=Feynman)揭示了一场更为微妙和优美的博弈。

我们来看看成键时的能量变化。[总能量](@keyword=total_energy|lang=zh-CN|style=Feynman)变化 $\Delta E$ 是负值；这就是将分子维系在一起的[键能](@keyword=bond_energy|lang=zh-CN|style=Feynman)。我们将[动能和势能](@keyword=kinetic_and_potential_energy|lang=zh-CN|style=Feynman)的变化定义为 $\delta T$ 和 $\delta V$。因此，$\Delta E = \delta T + \delta V$。[维里定理](@keyword=virial_theorem|lang=zh-CN|style=Feynman) $2\langle T \rangle = -\langle V \rangle$ 必须对[分离](@keyword=fractionation|lang=zh-CN|style=Feynman)的原子和最终的分子都成立。通过将其应用于“之前”和“之后”的状态，我们可以推导出能量*变化量*之间的关系 [@problem_id:2465704]。结果是惊人的：

$$
\delta T = -\Delta E \quad \text{and} \quad \delta V = 2\Delta E
$$

让我们仔细品味一下这个结果。因为 $\Delta E$ 是负值（形成了稳定的[化学键](@keyword=chemical_bonds|lang=zh-CN|style=Feynman)），所以 $\delta T$ 必须是*正值*。[动能](@keyword=kinetic_energy|lang=zh-CN|style=Feynman)竟然*增加*了！而 $\delta V$ 是负值，正如我们所预期的，但势能的下降量是最终稳定能的*两倍*。

为了形成一个稳定的[化学键](@keyword=chemical_bonds|lang=zh-CN|style=Feynman)，自然界达成了一个令人惊讶的交易。[电子](@keyword=electrons|lang=zh-CN|style=Feynman)被挤压

