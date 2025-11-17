## Introduction
In the realm of [quantum optics](@entry_id:140582), the state of the electromagnetic field holds all the information about its physical nature. This state is formally described by a [density operator](@entry_id:138151), a mathematical object residing in an infinite-dimensional Hilbert space. While complete, this abstract description often lacks direct physical intuition, creating a gap between the rigorous [quantum formalism](@entry_id:197347) and a more tangible understanding. How can we visualize the difference between the perfect photon-number certainty of a Fock state and the minimal uncertainty of a coherent state? How do we unambiguously identify a state as "non-classical," possessing properties with no counterpart in the classical world?

This article addresses these questions by introducing the powerful framework of phase-space representations. These mathematical tools map the quantum state onto functions over a two-dimensional phase space, creating a bridge to the intuitive world of classical mechanics. Across three comprehensive chapters, you will gain a deep understanding of this formalism and its profound implications.

The first chapter, "Principles and Mechanisms," lays the foundation by defining the Wigner, Glauber-Sudarshan, and Husimi quasiprobability distributions. It explores their interconnections and shows how they are used to analyze the statistical properties of fundamental states, from the classical-like [coherent state](@entry_id:154869) to the quintessentially quantum Fock and squeezed states. The second chapter, "Applications and Interdisciplinary Connections," demonstrates the power of this formalism beyond foundational theory. It explores how the unique properties of these states are harnessed in quantum information, [metrology](@entry_id:149309), and atom-field interactions, and reveals surprising connections to [condensed matter](@entry_id:747660) physics and [quantum field theory in curved spacetime](@entry_id:158321). Finally, "Hands-On Practices" provides a set of problems to solidify your understanding and develop practical calculation skills. By the end, you will not only be able to describe the states of the quantized field but also appreciate their role as a universal language in modern physics.

## Principles and Mechanisms

The state of a quantized field mode, described by its [density operator](@entry_id:138151) $\hat{\rho}$, contains all possible information about its physical properties. However, the abstract nature of the [density operator](@entry_id:138151), existing in an infinite-dimensional Hilbert space, often obscures direct physical intuition. To bridge this gap between the abstract [quantum formalism](@entry_id:197347) and a more tangible, classical-like intuition, we employ phase-space representations. These mathematical tools map the quantum state onto a function defined over a two-dimensional phase space, analogous to the [classical phase space](@entry_id:195767) of position and momentum. While not true probability distributions, these "quasiprobability" functions provide a powerful visual and computational framework for understanding and classifying quantum states of light.

### Phase-Space Representations and Characteristic Functions

The phase space of a single electromagnetic mode is naturally parameterized by the real and imaginary parts of the [complex amplitude](@entry_id:164138) $\alpha$, which correspond to the [expectation values](@entry_id:153208) of the quadrature operators. There are several key ways to map a quantum state $\hat{\rho}$ onto this space, with the three most prominent being the Glauber-Sudarshan P-representation $P(\alpha)$, the Wigner function $W(\alpha)$, and the Husimi Q-function $Q(\alpha)$.

These distributions are most rigorously defined via their relationship to characteristic functions, which are essentially the Fourier transforms of the distributions. Let us define the displacement operator $\hat{D}(\eta) = \exp(\eta\hat{a}^\dagger - \eta^*\hat{a})$, where $\hat{a}$ and $\hat{a}^\dagger$ are the [annihilation and creation operators](@entry_id:194608) for the mode. The characteristic functions are defined as the [expectation value](@entry_id:150961) of differently ordered forms of this operator.

The **symmetrically-ordered** or **Wigner [characteristic function](@entry_id:141714)** is defined as:
$$
\chi_W(\eta) = \mathrm{Tr}(\hat{\rho} \, \hat{D}(\eta)) = \mathrm{Tr}(\hat{\rho} \, e^{\eta\hat{a}^\dagger - \eta^*\hat{a}})
$$
Its two-dimensional symplectic Fourier transform yields the **Wigner function** $W(\alpha)$:
$$
W(\alpha) = \int \frac{d^2\eta}{\pi^2} e^{\alpha\eta^* - \alpha^*\eta} \chi_W(\eta)
$$
The Wigner function holds a special place as it can take on negative values. This negativity is not a mathematical pathology; rather, it is a definitive and unambiguous signature of a non-classical state, one that has no counterpart in classical statistical optics.

The **normally-ordered characteristic function** is defined using the normally-ordered displacement operator, where all [creation operators](@entry_id:191512) are placed to the left of all [annihilation operators](@entry_id:180957):
$$
\chi_N(\eta) = \mathrm{Tr}(\hat{\rho} \, :\!\hat{D}(\eta)\!:) = \mathrm{Tr}(\hat{\rho} \, e^{\eta\hat{a}^\dagger} e^{-\eta^*\hat{a}})
$$
Its Fourier transform gives the **Glauber-Sudarshan P-representation**:
$$
P(\alpha) = \int \frac{d^2\eta}{\pi^2} e^{\alpha\eta^* - \alpha^*\eta} \chi_N(\eta)
$$
The P-representation serves as a weight function in the expansion of the [density operator](@entry_id:138151) in the coherent state basis, $\hat{\rho} = \int P(\alpha) |\alpha\rangle\langle\alpha| d^2\alpha$. For classical states of light, $P(\alpha)$ is a well-behaved, non-negative probability distribution. However, for non-classical states, it can become highly singular (e.g., involving derivatives of delta functions) and is not a classical probability density.

Finally, the **anti-normally-ordered characteristic function** $\chi_A(\eta) = \mathrm{Tr}(\hat{\rho} \, e^{-\eta^*\hat{a}} e^{\eta\hat{a}^\dagger})$ leads to the **Husimi Q-function**, which can be more directly defined as the expectation value of the density operator in a coherent state $|\alpha\rangle$:
$$
Q(\alpha) = \frac{1}{\pi} \langle \alpha | \hat{\rho} | \alpha \rangle
$$
The Q-function is always non-negative and bounded, $0 \le Q(\alpha) \le 1/\pi$, and can be interpreted as the distribution one would obtain from an idealized simultaneous measurement of both quadratures, limited by the vacuum noise.

A crucial insight into the nature of these representations comes from the relationship between the characteristic functions. Using the Baker-Campbell-Hausdorff (BCH) formula for operators whose commutator is a c-number, $e^{\hat{A}+\hat{B}} = e^{\hat{A}} e^{\hat{B}} e^{-[\hat{A},\hat{B}]/2}$, we can relate the symmetric and normal-ordered displacement operators. With $\hat{A} = \eta\hat{a}^\dagger$ and $\hat{B} = -\eta^*\hat{a}$, we have $[\hat{A},\hat{B}] = -|\eta|^2[\hat{a}^\dagger,\hat{a}] = |\eta|^2$. This yields:
$$
e^{\eta\hat{a}^\dagger - \eta^*\hat{a}} = e^{\eta\hat{a}^\dagger} e^{-\eta^*\hat{a}} e^{-|\eta|^2/2}
$$
Taking the trace with $\hat{\rho}$ on both sides directly connects the Wigner and normally-ordered characteristic functions:
$$
\chi_W(\eta) = \chi_N(\eta) \exp\left(-\frac{1}{2}|\eta|^2\right)
$$
This simple product in the Fourier domain corresponds to a convolution in the phase space domain. By applying the [convolution theorem](@entry_id:143495) to the Fourier transforms that define $W(\alpha)$ and $P(\alpha)$, we find that the Wigner function is a "smoothed" version of the P-representation [@problem_id:738209] [@problem_id:738066]:
$$
W(\alpha) = \int P(\beta) K(\alpha-\beta) \, d^2\beta
$$
The convolution kernel $K(\gamma)$ is the Fourier transform of the Gaussian factor $e^{-|\eta|^2/2}$. Performing this transform yields a Gaussian kernel:
$$
K(\gamma) = \int \frac{d^2\eta}{\pi^2} e^{\gamma\eta^* - \gamma^*\eta} e^{-|\eta|^2/2} = \frac{2}{\pi}\exp(-2|\gamma|^2)
$$
This Gaussian smoothing explains why the Wigner function is always better-behaved than the P-representation. Any singularities or rapid oscillations in $P(\alpha)$ are blurred out in $W(\alpha)$ by this convolution, though regions of negativity may persist.

Furthermore, these characteristic functions provide a direct route to calculating moments of the photon number distribution. The normally ordered moments $\langle (\hat{a}^\dagger)^k \hat{a}^k \rangle$ can be obtained by differentiating $\chi_N(\beta)$. For phase-invariant states, where $\chi_N(\beta)$ depends only on $x = |\beta|^2$, i.e., $\chi_N(\beta) = f(|\beta|^2)$, the mean photon number $\langle n \rangle = \langle \hat{a}^\dagger \hat{a} \rangle$ and the second-order factorial moment $\langle n(n-1) \rangle = \langle \hat{a}^{\dagger 2} \hat{a}^2 \rangle$ are given by the derivatives of $f(x)$ at the origin:
$$
\langle n \rangle = -f'(0) \qquad \langle n(n-1) \rangle = f''(0)
$$
This allows us to express key statistical quantities, such as the **Mandel Q parameter**, directly in terms of the characteristic function. The Mandel Q parameter, defined as $Q_M = (\langle (\Delta n)^2 \rangle - \langle n \rangle) / \langle n \rangle$, quantifies the deviation of the photon number statistics from a Poisson distribution. Using the relations above, we can derive a general expression for it [@problem_id:738308]:
$$
Q_M = \frac{\langle n(n-1) \rangle - \langle n \rangle^2}{\langle n \rangle} = \frac{f''(0) - (-f'(0))^2}{-f'(0)} = -\frac{f''(0)}{f'(0)} - f'(0)
$$
A value of $Q_M=0$ indicates Poissonian statistics (like a coherent state), $Q_M>0$ indicates super-Poissonian statistics (like a thermal state), and $Q_M  0$ indicates sub-Poissonian statistics, a clear signature of a non-classical state.

### A Gallery of Fundamental States

The power of the phase-space formalism becomes evident when applied to the fundamental states of the quantized field.

#### Fock States

The **Fock states**, or [number states](@entry_id:155105) $|n\rangle$, are the eigenstates of the [number operator](@entry_id:153568) $\hat{n} = \hat{a}^\dagger \hat{a}$. They represent the field with a definite, integer number of photons, $n$. These are quintessentially quantum states with no classical analogue. For the single-photon Fock state $|1\rangle$, the density operator is $\hat{\rho} = |1\rangle\langle 1|$. Its normally-ordered [characteristic function](@entry_id:141714) is computed as [@problem_id:738125]:
$$
\chi_N(\beta) = \langle 1 | e^{\beta \hat{a}^\dagger} e^{-\beta^* \hat{a}} | 1 \rangle
$$
By expanding the exponentials as power series, we only need to consider the terms that do not change the photon number from 1 back to 1. The only non-vanishing terms are the zeroth-order term from both series and the first-order term from both series:
$$
\chi_N(\beta) = \langle 1 | (1 + \beta \hat{a}^\dagger + \dots)(1 - \beta^* \hat{a} + \dots) | 1 \rangle = \langle 1|1|1\rangle - \beta\beta^* \langle 1|\hat{a}^\dagger \hat{a}|1\rangle = 1 - |\beta|^2
$$
This simple polynomial form is characteristic of a highly non-classical state. From this result, using the relations derived previously ($f(x) = 1-x$), we find $\langle n \rangle = -f'(0) = 1$ and $\langle n(n-1) \rangle = f''(0) = 0$, giving a Mandel Q parameter of $Q_M = -1$, its minimum possible value.

#### Coherent and Thermal States

**Coherent states** $|\alpha\rangle$ are the eigenstates of the [annihilation operator](@entry_id:149476), $\hat{a}|\alpha\rangle = \alpha|\alpha\rangle$, and are considered the most "classical" of quantum states. Their photon number distribution is Poissonian. A pure coherent state is rarely realized; often, classical uncertainty, such as a fluctuating phase, leads to a [mixed state](@entry_id:147011). A **phase-randomized coherent state**, with amplitude $\alpha = \alpha_0 e^{i\phi}$, is described by the density operator $\hat{\rho} = \frac{1}{2\pi} \int_0^{2\pi} |\alpha_0 e^{i\phi}\rangle\langle\alpha_0 e^{i\phi}| d\phi$. When expanded in the Fock basis, the off-diagonal elements average to zero, leaving a diagonal [density matrix](@entry_id:139892) corresponding to a Poissonian distribution of photon numbers, $P(n) = e^{-|\alpha_0|^2}|\alpha_0|^{2n}/n!$. Despite being a mixed state, its [photon statistics](@entry_id:175965) remain Poissonian. The [second-order coherence function](@entry_id:175172) at zero delay, $g^{(2)}(0) = \langle \hat{a}^{\dagger 2} \hat{a}^2 \rangle / \langle \hat{a}^\dagger \hat{a} \rangle^2$, evaluates to 1, identical to a pure [coherent state](@entry_id:154869) [@problem_id:738137].

In contrast, a **thermal state** describes a field mode in thermal equilibrium with a reservoir at a finite temperature. Its [density operator](@entry_id:138151) is diagonal in the Fock basis with geometrically distributed weights:
$$
\hat{\rho}_{th} = \frac{1}{1+\bar{n}} \sum_{n=0}^{\infty} \left(\frac{\bar{n}}{1+\bar{n}}\right)^n |n\rangle\langle n|
$$
Here, $\bar{n}$ is the mean photon number. Thermal light exhibits [photon bunching](@entry_id:161039), with $g^{(2)}(0) = 2$. Its representation in phase space is particularly illuminating. The Husimi Q-function for a thermal state is a circularly symmetric Gaussian centered at the origin [@problem_id:738242]:
$$
Q(\alpha) = \frac{1}{\pi(1+\bar{n})} \exp\left(-\frac{|\alpha|^2}{1+\bar{n}}\right)
$$
The width of this Gaussian, $\sqrt{1+\bar{n}}$, reflects the combined uncertainty from the vacuum fluctuations (the '1') and the additional thermal fluctuations (the '$\bar{n}$').

#### Squeezed States and Entanglement

**Squeezed states** are a class of non-classical states where the [quantum noise](@entry_id:136608) in one observable quadrature is reduced below the [vacuum level](@entry_id:756402), at the expense of increased noise in the conjugate quadrature. They are generated by the unitary squeezing operator, $\hat{S}(\zeta) = \exp[\frac{1}{2}(\zeta^* \hat{a}^2 - \zeta (\hat{a}^\dagger)^2)]$. For a real squeezing parameter $\zeta = r$, the operator transforms the quadrature operators $\hat{q} = (\hat{a} + \hat{a}^\dagger)/\sqrt{2}$ and $\hat{p} = i(\hat{a}^\dagger - \hat{a})/\sqrt{2}$ as:
$$
\hat{S}^\dagger(r) \hat{q} \hat{S}(r) = \hat{q} e^{-r} \qquad \hat{S}^\dagger(r) \hat{p} \hat{S}(r) = \hat{p} e^{r}
$$
When squeezing is applied to a thermal state, we produce a **squeezed thermal state**. The initial thermal state has symmetric noise in both quadratures, with variance $(\Delta q)^2_{th} = (\Delta p)^2_{th} = \bar{n} + 1/2$. After squeezing, the variances become direction-dependent:
$$
(\Delta q)^2_{STS} = (\bar{n} + 1/2)e^{-2r} \qquad (\Delta p)^2_{STS} = (\bar{n} + 1/2)e^{2r}
$$
The noise asymmetry, or the difference in variances, is $(\Delta p)^2 - (\Delta q)^2 = (2\bar{n}+1)(e^{2r} - e^{-2r})/2 = (2\bar{n}+1)\sinh(2r)$ [@problem_id:738131]. This demonstrates the characteristic trade-off of squeezing: noise is suppressed in one quadrature while being amplified in the other.

Perhaps one of the most profound connections in [quantum optics](@entry_id:140582) is that between entanglement and thermal statistics, exemplified by the **[two-mode squeezed vacuum](@entry_id:147759)**. This state is generated by applying a [two-mode squeezing](@entry_id:183898) operator $\hat{S}_2(r) = \exp(r(\hat{a}_1^\dagger \hat{a}_2^\dagger - \hat{a}_1 \hat{a}_2))$ to the vacuum $|0\rangle_1|0\rangle_2$. The resulting [pure state](@entry_id:138657) is an entangled superposition of twin-photon states:
$$
|\psi\rangle_{12} = \frac{1}{\cosh r} \sum_{n=0}^{\infty} (\tanh r)^n |n\rangle_1 |n\rangle_2
$$
If an observer has access to only one mode (say, mode 1) and is ignorant of the other, the state they perceive is described by the [reduced density operator](@entry_id:190449) $\hat{\rho}_1 = \mathrm{Tr}_2(|\psi\rangle_{12}\langle\psi|_{12})$. By performing this [partial trace](@entry_id:146482), we find a remarkable result [@problem_id:738091]:
$$
\hat{\rho}_1 = \frac{1}{\cosh^2 r} \sum_{n=0}^{\infty} (\tanh^2 r)^n |n\rangle_1 \langle n|_1
$$
This is precisely the [density matrix](@entry_id:139892) of a thermal state. The entanglement in the pure two-mode state manifests as thermal noise in the local, single-mode subsystem. The mean photon number in this thermal state is found by summing the series $\sum_n n P(n)$, which yields $\bar{n}_1 = \sinh^2 r$. This establishes a deep connection: the "temperature" of the reduced state is directly controlled by the degree of entanglement (squeezing parameter $r$) in the global pure state.

### Advanced Non-Classical States and Their Signatures

Beyond the canonical states, more complex "engineered" states can be created through operations like photon addition or subtraction. A prime example is the **single-photon-subtracted squeezed vacuum** (SPSSV), created by applying the [annihilation operator](@entry_id:149476) $\hat{a}$ to a squeezed vacuum state $\hat{S}(r)|0\rangle$. A crucial insight is that this operation, after normalization, is equivalent to squeezing a single-photon Fock state. This can be seen from the operator identity $\hat{a}\hat{S}(r) = \hat{S}(r)(\hat{a}\cosh r - \hat{a}^\dagger \sinh r)$. Applying this to the vacuum $|0\rangle$ gives $\hat{a}\hat{S}(r)|0\rangle = -\sinh r \, \hat{S}(r)|1\rangle$. Thus, up to a [normalization constant](@entry_id:190182), the SPSSV state is $|\psi_{sps}\rangle = \hat{S}(r)|1\rangle$.

This state exhibits pronounced non-classical features. The squeezed vacuum $|\hat{S}(r)|0\rangle$ is a superposition of only even photon-[number states](@entry_id:155105). Applying $\hat{a}$ changes the parity, converting it to a superposition of only odd photon-[number states](@entry_id:155105). The probability of measuring exactly one photon in this state is found to be $P(1) = 1/\cosh^3 r$ [@problem_id:738126].

The most striking feature of the SPSSV state is the negativity of its Wigner function. The Wigner function for a pure Fock state $|1\rangle$ is $W_1(\alpha) = \frac{1}{\pi} e^{-2|\alpha|^2}(4|\alpha|^2-1)$. Since $|\psi_{sps}\rangle = \hat{S}(r)|1\rangle$, its Wigner function is simply the Wigner function of $|1\rangle$ with squeezed coordinates. In the quadrature basis $(x, p)$, we have $W_{sps}(x,p) = W_1(x e^r, p e^{-r})$. The negativity of the Wigner function is a powerful resource, and its magnitude can be quantified by the **negative volume**, $\mathcal{V}^- = \iint_{W0} |W(x,p)| dx dp$. For the SPSSV state, a remarkable result emerges: the negative volume is completely independent of the squeezing parameter $r$ [@problem_id:738113]. A calculation shows that:
$$
\mathcal{V}^- = e^{-1/2} - 1/2 \approx 0.107
$$
This tells us that the squeezing operation merely deforms the shape of the negative region in phase space—stretching it in one direction and compressing it in another—while perfectly preserving its integrated volume. The non-classical character, as quantified by $\mathcal{V}^-$, is an intrinsic property of the underlying single-photon excitation, which is simply "dressed" by the squeezing operation. This highlights the robustness of Wigner function negativity as a fundamental measure of quantumness.