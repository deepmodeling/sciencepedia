## Introduction
The [quantum mechanics of light](@entry_id:171461) and other bosonic systems is built upon the rigorous but often abstract formalism of Hilbert space. While this mathematical structure is complete, it can lack the intuitive appeal of classical mechanics, where a system's state is simply a point evolving in a tangible phase space of position and momentum. The challenge, then, is to find a representation of quantum states that retains the full rigor of quantum theory while providing a more visual and intuitive framework. This is the central problem addressed by the coherent [state representation](@entry_id:141201) and its associated phase-space quasiprobability distributions. These powerful tools map abstract quantum operators and density matrices onto functions on a classical-like phase space, providing an invaluable bridge between the quantum and classical worlds.

This article provides a comprehensive exploration of this essential formalism. In the first section, **Principles and Mechanisms**, we will construct the three most important phase-space representations—the Wigner, Glauber-Sudarshan P, and Husimi Q functions—and explore their fundamental properties and interrelations. We will then see how this framework is applied in the second section, **Applications and Interdisciplinary Connections**, to analyze quantum dynamics, characterize states, process quantum information, and even tackle problems in thermodynamics, [nuclear physics](@entry_id:136661), and gravitation. Finally, the **Hands-On Practices** section will offer a series of guided problems to solidify your computational understanding of these representations. We begin by delving into the foundational principles that allow us to build this powerful bridge to phase space.

## Principles and Mechanisms

In the preceding section, we introduced the foundational concepts of quantum states of light. While the Hilbert space formalism provides a complete and rigorous description, its abstract nature can often obscure physical intuition. Classical mechanics, in contrast, benefits from the intuitive picture of a system's state evolving as a point in phase space. This section introduces a powerful set of tools—phase-space quasiprobability distributions—that bridge these two worlds. These representations map quantum states and operators onto functions on a classical-like phase space, providing a framework for visualization, calculation, and deeper insight into the nature of quantum phenomena. We will explore the three most prominent of these: the Wigner function, the Glauber-Sudarshan P-representation, and the Husimi Q-function.

### The Wigner Function and the Weyl Correspondence

The first and most direct bridge between the [quantum operator algebra](@entry_id:190050) and classical phase-space functions is the Wigner-Weyl correspondence. This formalism provides a unique rule to map any [quantum operator](@entry_id:145181) to a corresponding function on phase space, known as its Weyl symbol.

#### The Wigner-Weyl Transformation

For a single-mode system described by [position and momentum operators](@entry_id:152590), $\hat{q}$ and $\hat{p}$, which satisfy the [canonical commutation relation](@entry_id:150454) $[\hat{q}, \hat{p}] = i\hbar$, the phase space is spanned by the corresponding classical variables $(q, p)$. The **Weyl symbol** $A_W(q, p)$ of an operator $\hat{A}$ is defined through the following [integral transform](@entry_id:195422):

$A_W(q, p) = \int_{-\infty}^{\infty} dy \, \exp(-ipy/\hbar) \langle q + y/2 | \hat{A} | q - y/2 \rangle$

Here, $|q \rangle$ represents the eigenstates of the position operator $\hat{q}$. This definition provides a systematic method for translating quantum operators into phase-space functions. A crucial property of this transformation is its linearity: the Weyl symbol of a sum of operators is the sum of their individual Weyl symbols.

In quantum optics, it is often more convenient to work with a dimensionless [complex amplitude](@entry_id:164138) $\alpha$, which combines the position and momentum quadratures. A common definition is:

$\alpha = \sqrt{\frac{m\omega}{2\hbar}} q + \frac{i}{\sqrt{2m\omega\hbar}} p$

This complex number $\alpha$ defines a point in phase space. The operators $\hat{q}$ and $\hat{p}$ are related to the [annihilation and creation operators](@entry_id:194608), $\hat{a}$ and $\hat{a}^\dagger$, as:

$\hat{a} = \sqrt{\frac{m\omega}{2\hbar}} \hat{q} + \frac{i}{\sqrt{2m\omega\hbar}} \hat{p}$

$\hat{a}^\dagger = \sqrt{\frac{m\omega}{2\hbar}} \hat{q} - \frac{i}{\sqrt{2m\omega\hbar}} \hat{p}$

Given the direct correspondence between the definitions of $\alpha$ and $\hat{a}$, it is perhaps not surprising, yet fundamentally important, that the Weyl symbol of the [annihilation operator](@entry_id:149476) $\hat{a}$ is simply the complex variable $\alpha$ [@problem_id:653525]. This can be shown by applying the linearity of the Weyl transform to the definition of $\hat{a}$, using the known symbols for the basic operators, $q_W(q,p) = q$ and $p_W(q,p) = p$.

$a_W(q,p) = \sqrt{\frac{m\omega}{2\hbar}} q_W(q,p) + \frac{i}{\sqrt{2m\omega\hbar}} p_W(q,p) = \sqrt{\frac{m\omega}{2\hbar}} q + \frac{i}{\sqrt{2m\omega\hbar}} p = \alpha$

A general and extremely useful property of the Wigner-Weyl correspondence relates an operator to its adjoint. The Weyl symbol of the [adjoint operator](@entry_id:147736) $\hat{A}^\dagger$ is the complex conjugate of the Weyl symbol of $\hat{A}$ [@problem_id:653426]:

$(\hat{A}^\dagger)_W(q, p) = [A_W(q, p)]^*$

Applying this rule to the [creation operator](@entry_id:264870) $\hat{a}^\dagger$, we immediately find its Weyl symbol to be the [complex conjugate](@entry_id:174888) of $\alpha$:

$(a^\dagger)_W(q, p) = [a_W(q,p)]^* = \alpha^*$

#### Operator Ordering and Weyl Symbols

The [non-commutativity](@entry_id:153545) of [quantum operators](@entry_id:137703) introduces a subtlety that has no classical parallel. While the Weyl symbol of a sum of operators is the sum of their symbols, the Weyl symbol of a product of operators is *not*, in general, the product of their symbols. That is, $(\hat{A}\hat{B})_W \neq A_W B_W$.

This complication is intimately related to operator ordering. The Wigner-Weyl correspondence is naturally associated with **symmetrically ordered** (or Weyl ordered) products. For any two operators, the Weyl symbol of their symmetrically ordered product is the product of their individual Weyl symbols. For example, the Weyl symbol for the operator $\frac{1}{2}(\hat{A}\hat{B} + \hat{B}\hat{A})$ is simply $A_W B_W$.

This provides a clear prescription for finding the Weyl symbol of any operator product: first, express the product in its symmetrically ordered form, and then replace the operators with their corresponding symbols. Let's consider the physically important [number operator](@entry_id:153568) $\hat{n} = \hat{a}^\dagger \hat{a}$ [@problem_id:653332]. This product is not symmetric. We can symmetrize it using the commutation relation $[\hat{a}, \hat{a}^\dagger] = 1$:

$\hat{n} = \hat{a}^\dagger \hat{a} = \frac{1}{2}(\hat{a}^\dagger \hat{a} + \hat{a}\hat{a}^\dagger) - \frac{1}{2}[\hat{a}^\dagger, \hat{a}] = \frac{1}{2}\{\hat{a}^\dagger, \hat{a}\} + \frac{1}{2}$

The first term is now symmetrically ordered. Taking the Weyl transform, we replace the symmetrized product with the product of the symbols $(a^\dagger)_W a_W = \alpha^* \alpha = |\alpha|^2$, and the constant $1/2$ transforms into itself. This yields the Weyl symbol for the [number operator](@entry_id:153568):

$n_W(\alpha, \alpha^*) = |\alpha|^2 - \frac{1}{2}$

The term $-1/2$ is a direct quantum correction arising from the non-commutativity of the [creation and annihilation operators](@entry_id:147121). It reflects the zero-point energy of the vacuum.

### The Wigner Function as a State Representation

The power of the Weyl correspondence is fully realized when we apply it to the density operator $\hat{\rho}$, which encapsulates all information about a quantum state. The **Wigner function** $W(\alpha)$ of a state $\hat{\rho}$ is defined as the Weyl symbol of the [density operator](@entry_id:138151), typically with a normalization factor of $1/\pi$. (Note: Normalization conventions may vary; we will adopt a convention consistent with dimensionless $\alpha$).

$W(\alpha) = \frac{1}{\pi} \int d^2\beta \, \exp(\alpha\beta^* - \alpha^*\beta) \text{Tr}(\hat{\rho} \hat{D}(\beta))$

where $\hat{D}(\beta) = \exp(\beta\hat{a}^\dagger - \beta^*\hat{a})$ is the displacement operator. The Wigner function has several key properties:
1.  It is always a real-valued function.
2.  It is normalized: $\int W(\alpha) d^2\alpha = 1$.
3.  The marginal distributions yield the correct probability distributions for position and momentum.
4.  Crucially, it is not necessarily non-negative. Regions where $W(\alpha)  0$ are unequivocal signatures of the non-classical nature of a state.

#### Calculating Observables

The primary utility of the Wigner function lies in the calculation of expectation values. The [expectation value](@entry_id:150961) of any operator $\hat{A}$ is given by the phase-space average of its Weyl symbol $A_W$ weighted by the Wigner function:

$\langle \hat{A} \rangle = \text{Tr}(\hat{\rho}\hat{A}) = \int A_W(\alpha, \alpha^*) W(\alpha) d^2\alpha$

This formula is remarkably powerful. For instance, consider calculating the expectation value of a generalized quadrature operator $\hat{X}_\theta = \hat{X}\cos\theta + \hat{P}\sin\theta$, where $\hat{X}$ and $\hat{P}$ are dimensionless quadratures related to $\hat{a}$ by $\hat{a} = (\hat{X}+i\hat{P})/\sqrt{2}$. The corresponding Weyl symbol is $X_W \cos\theta + P_W \sin\theta = x\cos\theta + p\sin\theta$. For a [coherent state](@entry_id:154869) $|\alpha_0\rangle$ with $\alpha_0 = (x_0 + ip_0)/\sqrt{2}$, its Wigner function is a Gaussian centered at $(x_0, p_0)$ [@problem_id:653403]. The expectation value is then simply the average of $x\cos\theta + p\sin\theta$ over this Gaussian, which yields the mean value:

$\langle \hat{X}_\theta \rangle = \int (x\cos\theta + p\sin\theta) W_{\alpha_0}(x,p) \,dx\,dp = x_0\cos\theta + p_0\sin\theta$

This confirms that the center of the Wigner function corresponds to the mean quadrature amplitudes of the state.

#### Wigner Functions of Important States

For a **[coherent state](@entry_id:154869)** $|\alpha_0\rangle$, the Wigner function is a minimum-uncertainty, two-dimensional Gaussian centered on $\alpha_0$ in phase space. It is strictly non-negative, reflecting the [coherent state](@entry_id:154869)'s status as the "most classical" quantum state:

$W_{\alpha_0}(\alpha) = \frac{2}{\pi} \exp(-2|\alpha - \alpha_0|^2)$

In stark contrast, the Wigner functions for non-classical states, such as **Fock states** $|n\rangle$, exhibit more complex structures. Using an elegant formulation based on the displaced [parity operator](@entry_id:148434), one can derive the Wigner function for the Fock state $|n\rangle$ [@problem_id:653358]. The result involves Laguerre polynomials $L_n(x)$:

$W_n(\alpha) = \frac{2}{\pi}(-1)^n \exp(-2|\alpha|^2) L_n(4|\alpha|^2)$

For the vacuum state ($n=0$), this reduces to a Gaussian centered at the origin, as $L_0(x)=1$. For any $n>0$, the Laguerre polynomial has roots, causing the Wigner function to oscillate and take on negative values. These negative regions are a hallmark of [quantum interference](@entry_id:139127) in phase space and are a definitive indicator that Fock states are profoundly non-classical.

#### Global Properties from Phase-Space Integrals

Global properties of a quantum state can be expressed as integrals over its Wigner function. A key example is the **purity** of a state, $\mathcal{P} = \text{Tr}(\hat{\rho}^2)$, which measures the degree of mixture. This quantity is directly related to the "spikiness" of the Wigner function. The general formula for the overlap of two states is [@problem_id:653454]:

$\text{Tr}(\hat{\rho}_1 \hat{\rho}_2) = \pi \int W_1(\alpha) W_2(\alpha) d^2\alpha$

By setting $\hat{\rho}_1 = \hat{\rho}_2 = \hat{\rho}$, we find the purity is proportional to the integrated square of the Wigner function [@problem_id:653422]:

$\mathcal{P} = \text{Tr}(\hat{\rho}^2) = \pi \int [W(\alpha)]^2 d^2\alpha$

For a [pure state](@entry_id:138657) like a coherent state $|\alpha_0\rangle$, this integral evaluates to 1. For a mixed state, such as an incoherent mixture $\hat{\rho} = \frac{1}{2}(|\alpha_0\rangle\langle\alpha_0| + |-\alpha_0\rangle\langle-\alpha_0|)$, the Wigner function is the sum of two separated Gaussians. The integral of its square contains cross-terms that depend on the separation of the Gaussians. The resulting purity is $\mathcal{P} = \frac{1}{2}(1 + \exp(-4|\alpha_0|^2))$. As the separation $|\alpha_0|$ increases, the overlap term vanishes and the purity approaches $1/2$, the value for an equal mixture of two orthogonal states.

### Representations for Specific Operator Orderings: P and Q

While the Wigner function is associated with symmetric ordering, many physical processes, particularly photodetection, are most naturally described by normally ordered operators (all [creation operators](@entry_id:191512) to the left of all [annihilation operators](@entry_id:180957)). This motivates the use of quasiprobability distributions tailored to specific orderings.

#### The Glauber-Sudarshan P-Representation

The **Glauber-Sudarshan P-representation** expresses the density operator as a statistical mixture of coherent state projectors:

$\hat{\rho} = \int P(\alpha) |\alpha\rangle\langle\alpha| d^2\alpha$

The function $P(\alpha)$ is a [quasiprobability distribution](@entry_id:203668) whose primary virtue is the elegant simplification it brings to calculating normally ordered expectation values [@problem_id:653336]:

$\langle (\hat{a}^\dagger)^m \hat{a}^n \rangle = \text{Tr}[\hat{\rho} (\hat{a}^\dagger)^m \hat{a}^n] = \int P(\alpha) (\alpha^*)^m \alpha^n d^2\alpha$

This formula replaces a quantum trace operation with a classical-like phase-space average. The character of the $P(\alpha)$ function is a powerful diagnostic of the state's quantum nature.
- For classical-like states (e.g., [thermal light](@entry_id:165211), laser light far above threshold), $P(\alpha)$ is a well-behaved, non-negative probability distribution. For a simple statistical mixture of two [coherent states](@entry_id:154533), $\hat{\rho} = p|\alpha\rangle\langle\alpha| + (1-p)|\beta\rangle\langle\beta|$, the P-function is a sum of two Dirac delta functions: $P(\gamma) = p\delta^{(2)}(\gamma-\alpha) + (1-p)\delta^{(2)}(\gamma-\beta)$. Using this representation, one can readily calculate [photon statistics](@entry_id:175965), such as the Mandel Q parameter, which for this state is always non-negative, indicating super-Poissonian statistics arising from the classical mixture of intensities [@problem_id:653475].
- For non-classical states, $P(\alpha)$ can become negative or highly singular, making it more of a mathematical distribution than a classical probability density. For a Fock state $|n\rangle$, which has no classical analogue, the P-function is extraordinarily singular, involving high-order derivatives of the two-dimensional Dirac [delta function](@entry_id:273429) centered at the origin [@problem_id:653536].

The highly singular and non-positive nature of $P(\alpha)$ is the price paid for the convenience of calculating normally ordered moments. It is the P-representation's way of encoding uniquely quantum features like sub-Poissonian statistics.

#### The Husimi Q-Function

At the other end of the ordering spectrum is the **Husimi Q-function**, associated with anti-normally ordered operators ([annihilation operators](@entry_id:180957) to the left of [creation operators](@entry_id:191512)). It is defined as the expectation value of the density operator in a coherent state:

$Q(\alpha) = \frac{1}{\pi} \langle\alpha|\hat{\rho}|\alpha\rangle$

The Q-function is essentially a projection of the state onto the basis of [coherent states](@entry_id:154533). It has the appealing properties of always being non-negative ($0 \le Q(\alpha) \le 1/\pi$) and smoother than both the Wigner and P-functions. It can be thought of as a "blurred" version of the Wigner function. Because [coherent states](@entry_id:154533) are themselves overcomplete and not orthogonal, the Q-function represents a loss of information compared to the [density matrix](@entry_id:139892) or the Wigner function, but its smoothness makes it an excellent tool for visualization. For example, for a [mixed state](@entry_id:147011) like $\hat{\rho} = \frac{1}{5}|0\rangle\langle 0| + \frac{2}{5}|1\rangle\langle 1| + \frac{2}{5}|2\rangle\langle 2|$, the Q-function is a smooth, bell-shaped distribution whose maximum value can be found by standard calculus, providing a clear picture of the state's extent in phase space [@problem_id:653452].

### Interrelations Between Representations

The Wigner, Glauber-Sudarshan, and Husimi functions are not independent descriptions but are different "views" of the same underlying quantum state, connected by mathematical transformations. Their relationship can be understood as a hierarchy of smoothing.

The P-function is the most fundamental in this hierarchy but also the most potentially singular. The Wigner function can be obtained from the P-function via a Gaussian convolution, which has a smoothing effect [@problem_id:653491]:

$W(\alpha) = \frac{2}{\pi} \int \exp(-2|\alpha - \beta|^2) P(\beta) d^2\beta$

This convolution explains why the Wigner function is generally better behaved than the P-function; the sharp singularities in $P(\alpha)$ for non-classical states are blurred out into the oscillating positive and negative regions of $W(\alpha)$. Similarly, the Q-function is a further smoothing of the Wigner function.

Conversely, one can recover the P-function from the Wigner function by inverting the smoothing operation. This [deconvolution](@entry_id:141233) is accomplished by a [differential operator](@entry_id:202628). By analyzing the convolution in the Fourier domain, one can show that the transformation is given by [@problem_id:653491]:

$P(\alpha) = \exp\left(\frac{1}{8} \nabla_\alpha^2\right) W(\alpha)$

where $\nabla_\alpha^2$ is the Laplacian in the phase-space plane. This relationship elegantly reveals the source of the P-function's difficult nature. The Laplacian operator acts as a high-pass filter, amplifying sharp features. When applied to a Wigner function with gentle variations, this "un-smoothing" process can generate the highly [singular distributions](@entry_id:265958) characteristic of non-classical states.

In summary, the three major quasiprobability distributions offer a complementary toolkit for [quantum optics](@entry_id:140582). The Wigner function provides a direct link to symmetrically ordered operators and a neutral phase-space portrait. The P-function offers unparalleled convenience for normally ordered calculations, vividly highlighting non-classicality through its potential singularity. The Q-function provides a non-negative, smoothed picture ideal for visualization. Together, they constitute a rich and intuitive language for describing the dynamics and properties of quantum light.