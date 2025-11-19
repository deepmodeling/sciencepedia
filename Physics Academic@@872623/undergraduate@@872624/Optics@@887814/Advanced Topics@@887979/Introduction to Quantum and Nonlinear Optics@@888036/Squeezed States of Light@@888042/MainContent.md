## Introduction
Light, as we experience it, is governed by fundamental quantum limits. The inherent fluctuations, or "noise," in even the most stable laser beams impose a boundary on the precision of our measurements—a barrier known as the Standard Quantum Limit (SQL). But what if we could manipulate this [quantum noise](@entry_id:136608) itself? This question introduces one of the most powerful concepts in modern quantum optics: squeezed states of light. These are uniquely quantum states where uncertainty is not just a limit to be accepted, but a resource to be controlled and redistributed. This article demystifies squeezed light, moving beyond classical intuition to explain how we can "squeeze" the noise in one property of light, such as its phase, to achieve unprecedented measurement sensitivity, at the predictable cost of increasing noise in another property, like its amplitude.

Over the next chapters, you will build a complete picture of this fascinating topic. The journey begins in **Principles and Mechanisms**, where we will explore the quantum mechanical formalism of quadrature operators, the squeezing transformation, and the distinct physical properties of these states. Next, **Applications and Interdisciplinary Connections** will showcase how squeezed light is revolutionizing fields from [gravitational wave detection](@entry_id:159771) in LIGO to continuous-variable quantum computing, and even provides analogues for phenomena in [condensed matter](@entry_id:747660) and gravitational physics. Finally, the **Hands-On Practices** section will allow you to apply these concepts to practical problems, solidifying your understanding of how squeezed states are measured and utilized.

## Principles and Mechanisms

This chapter delves into the fundamental principles and quantum mechanical formalism that describe squeezed states of light. We will move beyond the classical description of light and the semi-classical picture of [coherent states](@entry_id:154533) to explore states where the inherent quantum noise is manipulated. This manipulation allows for the reduction of noise in one observable at the expense of increased noise in another, a process constrained only by the Heisenberg uncertainty principle. We will begin by establishing the phase-space picture of quantum light, introduce the mathematical machinery of the squeezing transformation, explore the unique physical properties of the resulting states, and discuss their generation, evolution, and application.

### Quadratures and the Quantum Phase Space

A single mode of the electromagnetic field can be modeled as a quantum harmonic oscillator. Its quantum state is described using the non-Hermitian **[annihilation operator](@entry_id:149476)** $\hat{a}$ and **[creation operator](@entry_id:264870)** $\hat{a}^\dagger$, which obey the [canonical commutation relation](@entry_id:150454) $[\hat{a}, \hat{a}^\dagger] = 1$. These operators decrease or increase the number of photons in the mode, respectively, when acting on a photon [number state](@entry_id:180241) $|n\rangle$.

While the photon number provides a discrete description, a continuous-variable picture is often more insightful. This is achieved through the **quadrature operators**, which are the quantum mechanical analogues of the real and imaginary parts of the classical field amplitude. They are defined as:
$$ \hat{X}_1 = \frac{1}{2}(\hat{a} + \hat{a}^\dagger) $$
$$ \hat{X}_2 = \frac{1}{2i}(\hat{a} - \hat{a}^\dagger) $$
These Hermitian operators correspond to measurable physical quantities. $\hat{X}_1$ is often called the **amplitude quadrature** and $\hat{X}_2$ the **phase quadrature**. Using the [commutation relation](@entry_id:150292) for $\hat{a}$ and $\hat{a}^\dagger$, it is straightforward to show that the quadrature operators do not commute:
$$ [\hat{X}_1, \hat{X}_2] = \frac{i}{2} $$
This [non-commutativity](@entry_id:153545) leads directly to the **Heisenberg uncertainty principle** for the quadratures:
$$ \Delta X_1 \Delta X_2 \ge \frac{1}{4} $$
where $\Delta X_i = \sqrt{\langle \hat{X}_i^2 \rangle - \langle \hat{X}_i \rangle^2}$ is the standard deviation, or quantum uncertainty, of a measurement of quadrature $\hat{X}_i$.

The state of the field can be visualized as an "uncertainty region" in a phase space with axes $(\langle \hat{X}_1 \rangle, \langle \hat{X}_2 \rangle)$. For the **vacuum state** $|0\rangle$ (which has zero photons, $\hat{a}|0\rangle=0$) and for **[coherent states](@entry_id:154533)** $|\alpha\rangle$ ([eigenstates](@entry_id:149904) of the [annihilation operator](@entry_id:149476), $\hat{a}|\alpha\rangle=\alpha|\alpha\rangle$), the uncertainty is minimized and distributed equally between the quadratures. This results in a circular uncertainty region where $\Delta X_1 = \Delta X_2 = 1/2$. This noise level, where the variance is $(\Delta X_i)^2 = 1/4$, is a fundamental benchmark known as the **Standard Quantum Limit (SQL)** or the shot-noise limit.

### The Squeezing Transformation

A **squeezed state** is any quantum state for which the uncertainty in one quadrature is less than the SQL value of $1/2$. This necessarily implies, due to the uncertainty principle, that the uncertainty in the orthogonal quadrature must be greater than $1/2$.

Squeezed states are generated by applying a **squeezing operator** to an initial state, typically the vacuum or a [coherent state](@entry_id:154869). The single-mode squeezing operator is defined as:
$$ \hat{S}(r, \phi) = \exp\left[ \frac{1}{2} ( \zeta^* \hat{a}^2 - \zeta (\hat{a}^\dagger)^2 ) \right] $$
where $\zeta = r e^{i\phi}$ is a complex number with $r$ being the **squeezing parameter** (a real, non-negative number) and $\phi$ the **squeezing angle**. For simplicity, we will first consider the case where $\phi=0$, so $\zeta = r$ is real. The operator becomes:
$$ \hat{S}(r) = \exp\left[ \frac{r}{2}( \hat{a}^2 - (\hat{a}^\dagger)^2 ) \right] $$
Applying this operator to the vacuum state creates a **squeezed vacuum state**, $|\psi_s\rangle = \hat{S}(r)|0\rangle$.

To understand the effect of this transformation, we examine how the quadrature operators change in the Heisenberg picture. The transformation rules, known as **Bogoliubov transformations**, are:
$$ \hat{S}^\dagger(r) \hat{a} \hat{S}(r) = \hat{a} \cosh r - \hat{a}^\dagger \sinh r $$
$$ \hat{S}^\dagger(r) \hat{a}^\dagger \hat{S}(r) = \hat{a}^\dagger \cosh r - \hat{a} \sinh r $$
Using these, we can find the transformed quadratures:
$$ \hat{S}^\dagger(r) \hat{X}_1 \hat{S}(r) = \frac{1}{2} ( (\hat{a}\cosh r - \hat{a}^\dagger\sinh r) + (\hat{a}^\dagger\cosh r - \hat{a}\sinh r) ) = \hat{X}_1 (\cosh r - \sinh r) = \hat{X}_1 e^{-r} $$
$$ \hat{S}^\dagger(r) \hat{X}_2 \hat{S}(r) = \frac{1}{2i} ( (\hat{a}\cosh r - \hat{a}^\dagger\sinh r) - (\hat{a}^\dagger\cosh r - \hat{a}\sinh r) ) = \hat{X}_2 (\cosh r + \sinh r) = \hat{X}_2 e^{r} $$
The [expectation values](@entry_id:153208) of the quadratures in the squeezed vacuum state are zero, since $\langle 0 | \hat{X}_i | 0 \rangle = 0$. The variances, however, are transformed. For the squeezed vacuum state $|\psi_s\rangle$, the variance of $\hat{X}_1$ is:
$$ (\Delta X_1)_s^2 = \langle \psi_s | \hat{X}_1^2 | \psi_s \rangle = \langle 0 | \hat{S}^\dagger(r) \hat{X}_1^2 \hat{S}(r) | 0 \rangle = \langle 0 | (\hat{S}^\dagger \hat{X}_1 \hat{S})^2 | 0 \rangle = \langle 0 | (\hat{X}_1 e^{-r})^2 | 0 \rangle = e^{-2r} \langle 0 | \hat{X}_1^2 | 0 \rangle = \frac{1}{4}e^{-2r} $$
Similarly, the variance of $\hat{X}_2$ is:
$$ (\Delta X_2)_s^2 = \frac{1}{4}e^{2r} $$
For any positive squeezing parameter $r>0$, we see that $\Delta X_1 < 1/2$ (squeezing) and $\Delta X_2 > 1/2$ (anti-squeezing). The uncertainty principle is preserved, as $(\Delta X_1)_s (\Delta X_2)_s = \frac{1}{4}$, indicating that the squeezed vacuum is a [minimum uncertainty state](@entry_id:193251).

In phase space, this transformation deforms the circular uncertainty region of the vacuum state into an ellipse. The semi-axes of this ellipse are the new standard deviations, $\Delta X_1 = \frac{1}{2}e^{-r}$ and $\Delta X_2 = \frac{1}{2}e^{r}$. For $r>0$, the major axis lies along the $\langle \hat{X}_2 \rangle$ direction and the minor axis along the $\langle \hat{X}_1 \rangle$ direction. The ratio of the length of the major axis to the minor axis is a direct measure of the squeezing strength: $\frac{\Delta X_2}{\Delta X_1} = e^{2r}$ [@problem_id:2256393].

### Physical Properties of Squeezed Light

#### Phase-Dependent Noise

The squeezing is directional. We can define a general quadrature operator dependent on a measurement phase angle $\theta$:
$$ \hat{X}_\theta = \frac{1}{2}(\hat{a}e^{-i\theta} + \hat{a}^\dagger e^{i\theta}) = \hat{X}_1 \cos\theta + \hat{X}_2 \sin\theta $$
For a squeezed vacuum state with squeezing angle $\phi$, the variance of $\hat{X}_\theta$ becomes phase-dependent [@problem_id:2256420]:
$$ (\Delta X_\theta)^2_{squeezed} = \frac{1}{4}[\cosh(2r) - \sinh(2r)\cos(2(\theta - \phi/2))] $$
This expression clearly shows that the noise is minimized (squeezed) when the measurement phase $\theta$ aligns with the squeezing axis ($\theta = \phi/2$) and maximized (anti-squeezed) when it is orthogonal ($\theta = \phi/2 + \pi/2$). If one were to perform measurements with a random, uniformly distributed phase, the benefit of squeezing would be lost on average. The average variance over all phases is:
$$ \overline{(\Delta X)^2} = \frac{1}{2\pi} \int_0^{2\pi} (\Delta X_\theta)^2_{squeezed} \,d\theta = \frac{1}{4}\cosh(2r) $$
Since $\cosh(2r) > 1$ for $r>0$, the average noise of a squeezed state is always greater than the noise of a [coherent state](@entry_id:154869). Squeezing does not eliminate noise; it intelligently redistributes it.

#### Photon Statistics

The terms $(\hat{a}^\dagger)^2$ and $\hat{a}^2$ in the squeezing operator respectively create and annihilate photons in pairs. This has a profound consequence for the photon number statistics of a squeezed vacuum state. When expanded in the basis of photon number (Fock) states $|n\rangle$, a squeezed vacuum state contains contributions only from states with an even number of photons [@problem_id:2256381]:
$$ |\psi_s\rangle = \frac{1}{\sqrt{\cosh r}} \sum_{n=0}^{\infty} \frac{\sqrt{(2n)!}}{2^n n!}(-\tanh r)^n |2n\rangle $$
The probability of measuring an odd number of photons is exactly zero. This two-photon nature is a hallmark of the squeezing process. For example, the ratio of the probability of detecting four photons to that of detecting two photons is given by $P(4)/P(2) = \frac{3}{4}\tanh^2 r$, illustrating how the distribution depends on the squeezing parameter [@problem_id:2256381].

If we apply displacement after squeezing, we generate a **squeezed [coherent state](@entry_id:154869)**, $|\alpha, r\rangle = \hat{D}(\alpha)\hat{S}(r)|0\rangle$. This state has a non-zero mean field amplitude, and its uncertainty ellipse is centered at $(\text{Re}(\alpha), \text{Im}(\alpha))$ in phase space. Its average photon number is the sum of contributions from the coherent displacement and the squeezing itself [@problem_id:2256415]:
$$ \langle \hat{n} \rangle = |\alpha|^2 + \sinh^2(r) $$
The term $\sinh^2(r)$ represents the mean number of photons present in the squeezed vacuum itself.

### Squeezing in Metrology and Quantum Information

#### Surpassing the Standard Quantum Limit

The ability to reduce noise in one quadrature below the SQL makes squeezed states an invaluable resource for high-precision measurements. Consider an [interferometer](@entry_id:261784) designed to measure a tiny phase shift $\delta\phi$. The signal is proportional to this phase shift, while the sensitivity is limited by the quantum noise in the phase quadrature measurement, $\Delta X_2$.

For a standard experiment using [coherent states](@entry_id:154533), the noise floor is the SQL, $\Delta X_{2,c} = 1/2$. The Signal-to-Noise Ratio (SNR) is $\text{SNR}_c \propto 1/\Delta X_{2,c} = 2$. By injecting a **phase-squeezed state**—one specifically prepared to have reduced noise in the phase quadrature—into the unused port of the interferometer, we can reduce the [measurement noise](@entry_id:275238) to $\Delta X_{2,s} = \frac{1}{2}e^{-r}$ [@problem_id:2256394]. The SNR for the squeezed-light-enhanced measurement becomes $\text{SNR}_s \propto 1/\Delta X_{2,s} = 2e^r$. The improvement factor is therefore:
$$ \frac{\text{SNR}_s}{\text{SNR}_c} = e^r $$
This demonstrates a direct enhancement in sensitivity that grows exponentially with the squeezing parameter. It is precisely this principle that enables gravitational wave observatories like LIGO and Virgo to achieve sensitivities beyond the SQL.

It is crucial to match the squeezed quadrature to the measurement task. If we were trying to measure a small change in amplitude, we would use an **amplitude-squeezed state**, which has reduced noise in $\hat{X}_1$. Using an amplitude-squeezed state for a phase measurement would be counterproductive, as its [phase noise](@entry_id:264787) $\Delta X_2$ would be enhanced, degrading the SNR by a factor of $e^{-r}$ compared to the SQL [@problem_id:2256400].

#### Dynamics and Decoherence

The properties of a squeezed state are not static. Under free evolution, governed by the Hamiltonian $\hat{H} = \hbar\omega(\hat{a}^\dagger\hat{a} + 1/2)$, the operators evolve as $\hat{a}(t) = \hat{a}(0)e^{-i\omega t}$. This causes the quadrature operators to rotate into one another:
$$ \hat{X}_1(t) = \hat{X}_1(0)\cos(\omega t) - \hat{X}_2(0)\sin(\omega t) $$
$$ \hat{X}_2(t) = \hat{X}_1(0)\sin(\omega t) + \hat{X}_2(0)\cos(\omega t) $$
This means that a squeezed state's uncertainty ellipse rotates in phase space at the field's frequency $\omega$ [@problem_id:2256411]. A state that is initially amplitude-squeezed will evolve into a phase-squeezed state after a quarter of a period ($t=\pi/(2\omega)$), and back to amplitude-squeezed after half a period.

Furthermore, squeezed states are fragile. Any interaction with the environment, which can be modeled as optical loss, will degrade the squeezing. A common model for loss is mixing the signal mode on a [beam splitter](@entry_id:145251) with a vacuum mode. If a squeezed state with transmissivity $\eta$ passes through a lossy channel, its quadrature variance increases. The new variance for a squeezed quadrature becomes a weighted average of the initial squeezed variance and the vacuum variance [@problem_id:2256409]:
$$ (\Delta X_1)_{out}^2 = \eta (\Delta X_1)_{in}^2 + (1-\eta) (\Delta X_{vac})^2 = \frac{1}{4}[\eta e^{-2r} + (1-\eta)] $$
This degradation limits the achievable [noise reduction](@entry_id:144387) in any real-world experiment. The effective squeezing $r_{\text{eff}}$ after loss is always less than the initial squeezing $r$.

#### Two-Mode Squeezing and Entanglement

Squeezing can also be applied to two distinct modes of light simultaneously, creating profound [quantum correlations](@entry_id:136327). The **[two-mode squeezing](@entry_id:183898) operator** is given by $\hat{S}_2(r) = \exp[r(\hat{a}_1^\dagger \hat{a}_2^\dagger - \hat{a}_1 \hat{a}_2)]$. When applied to a two-mode vacuum state $|0,0\rangle$, it creates a **[two-mode squeezed vacuum](@entry_id:147759)**, also known as an Einstein-Podolsky-Rosen (EPR) state.

This state is entangled. While measurements on either mode individually reveal only thermal-like noise, there are strong correlations between them. These correlations are manifest in joint observables. For instance, consider the joint position operator $\hat{x}_1 - \hat{x}_2$ and the joint momentum operator $\hat{p}_1 + \hat{p}_2$ (where $\hat{x}_k \propto \hat{X}_{1,k}$ and $\hat{p}_k \propto \hat{X}_{2,k}$). The variances of these joint operators are squeezed simultaneously [@problem_id:2256416]:
$$ \Delta^2(\hat{x}_1 - \hat{x}_2) \propto e^{-2r} \quad \text{and} \quad \Delta^2(\hat{p}_1 + \hat{p}_2) \propto e^{-2r} $$
The sum of these variances can be shown to fall below the limit imposed by classical physics or for any unentangled (separable) state, providing a direct confirmation of entanglement. This type of state is a fundamental building block for continuous-variable quantum computing and [quantum communication](@entry_id:138989) protocols.

Finally, it is worth noting the deep mathematical structure underlying these transformations. The set of bilinear operators $\{\frac{1}{2}(\hat{a}^\dagger)^2, \frac{1}{2}\hat{a}^2, \frac{1}{2}(\hat{a}^\dagger\hat{a} + 1/2)\}$ that generate squeezing and rotations form a Lie algebra known as $\mathfrak{su}(1,1)$ [@problem_id:2256431]. This algebraic foundation provides a powerful and elegant framework for analyzing and classifying the operations of [quantum optics](@entry_id:140582).