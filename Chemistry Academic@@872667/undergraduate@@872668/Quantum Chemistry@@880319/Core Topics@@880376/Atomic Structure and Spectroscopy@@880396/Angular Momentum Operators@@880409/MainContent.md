## Introduction
Angular momentum is a cornerstone concept in physics, describing the [rotational motion](@entry_id:172639) of objects from spinning planets to orbiting electrons. In the classical world, it is a continuous vector quantity. However, when we transition to the quantum realm, this familiar picture is replaced by a far more structured and powerful framework. Describing the rotational properties of particles like electrons requires a new set of tools: [quantum mechanical operators](@entry_id:270630). These operators and their unique mathematical relationships unlock the quantized nature of the subatomic world, revealing non-intuitive principles that have profound physical consequences. This article addresses the fundamental question of how to formally define and work with [angular momentum in quantum mechanics](@entry_id:142408).

This article will systematically guide you through the theory and application of angular momentum operators. In the first section, **"Principles and Mechanisms,"** we will build the mathematical foundation, starting from the classical definition and promoting it to quantum operators. We will derive the crucial [commutation relations](@entry_id:136780) that govern all of angular momentum theory, use algebraic methods to uncover the quantized eigenvalue spectrum, and introduce the concept of intrinsic spin. Next, in **"Applications and Interdisciplinary Connections,"** we will explore how these abstract principles are applied to explain tangible physical phenomena, from the architecture of the atom and the interpretation of spectroscopic data to the dynamics of particles in magnetic fields. Finally, the **"Hands-On Practices"** section provides an opportunity to apply these concepts and solidify your understanding by tackling representative problems.

## Principles and Mechanisms

### The Quantum Mechanical Definition of Angular Momentum

In classical mechanics, the [angular momentum of a particle](@entry_id:178745) with [position vector](@entry_id:168381) $\vec{r}$ and [linear momentum](@entry_id:174467) $\vec{p}$ is defined as the [vector cross product](@entry_id:156484) $\vec{L} = \vec{r} \times \vec{p}$. This vector quantity describes the [rotational motion](@entry_id:172639) of the particle about the origin. To transition to quantum mechanics, we employ the [correspondence principle](@entry_id:148030), promoting the classical position and momentum variables to their respective [quantum mechanical operators](@entry_id:270630). The [position operator](@entry_id:151496) is simply $\hat{\mathbf{r}} = (x, y, z)$, and the [momentum operator](@entry_id:151743) in the [position representation](@entry_id:154751) is $\hat{\mathbf{p}} = -i\hbar(\frac{\partial}{\partial x}, \frac{\partial}{\partial y}, \frac{\partial}{\partial z})$.

The quantum mechanical [angular momentum operator](@entry_id:155961) $\hat{\mathbf{L}}$ is thus defined as $\hat{\mathbf{L}} = \hat{\mathbf{r}} \times \hat{\mathbf{p}}$. Expanding the [cross product](@entry_id:156749) yields the Cartesian components of the [angular momentum operator](@entry_id:155961):

$\hat{L}_x = \hat{y}\hat{p}_z - \hat{z}\hat{p}_y = -i\hbar(y\frac{\partial}{\partial z} - z\frac{\partial}{\partial y})$

$\hat{L}_y = \hat{z}\hat{p}_x - \hat{x}\hat{p}_z = -i\hbar(z\frac{\partial}{\partial x} - x\frac{\partial}{\partial z})$

$\hat{L}_z = \hat{x}\hat{p}_y - \hat{y}\hat{p}_x = -i\hbar(x\frac{\partial}{\partial y} - y\frac{\partial}{\partial x})$

These operators act on wavefunctions to extract information about the angular momentum of the state they describe. For instance, if a wavefunction $\psi$ is an eigenfunction of an [angular momentum operator](@entry_id:155961), a measurement of that component of angular momentum will yield a definite, quantized value.

### The Fundamental Commutation Relations

A defining feature of quantum mechanics is that the order of operations matters. The degree to which two operators, $\hat{A}$ and $\hat{B}$, fail to commute is quantified by their **commutator**, defined as $[\hat{A}, \hat{B}] = \hat{A}\hat{B} - \hat{B}\hat{A}$. The properties of angular momentum are entirely dictated by the [commutation relations](@entry_id:136780) among its components. These, in turn, derive from the [canonical commutation relations](@entry_id:185041) for position and momentum: $[\hat{x}_i, \hat{x}_j] = 0$, $[\hat{p}_i, \hat{p}_j] = 0$, and $[\hat{x}_i, \hat{p}_j] = i\hbar\delta_{ij}$, where $i, j$ can be $x, y,$ or $z$.

Let us compute the commutator $[\hat{L}_x, \hat{L}_y]$ directly from the definitions [@problem_id:1352078]:
$$
[\hat{L}_x, \hat{L}_y] = [\hat{y}\hat{p}_z - \hat{z}\hat{p}_y, \hat{z}\hat{p}_x - \hat{x}\hat{p}_z]
$$
Expanding this expression and using [commutator identities](@entry_id:200165) such as $[\hat{A}\hat{B}, \hat{C}] = \hat{A}[\hat{B}, \hat{C}] + [\hat{A}, \hat{C}]\hat{B}$, we find that many terms vanish. For example, $[\hat{y}\hat{p}_z, \hat{x}\hat{p}_z] = 0$. The non-vanishing terms arise from commutators like $[\hat{y}\hat{p}_z, \hat{z}\hat{p}_x]$ and $[\hat{z}\hat{p}_y, \hat{x}\hat{p}_z]$.
A careful evaluation yields:
$$
[\hat{y}\hat{p}_z, \hat{z}\hat{p}_x] = -i\hbar\hat{y}\hat{p}_x
$$
$$
[\hat{z}\hat{p}_y, \hat{x}\hat{p}_z] = i\hbar\hat{x}\hat{p}_y
$$
Combining all terms, we arrive at a remarkably compact and significant result:
$$
[\hat{L}_x, \hat{L}_y] = i\hbar(\hat{x}\hat{p}_y - \hat{y}\hat{p}_x) = i\hbar\hat{L}_z
$$
By cyclically permuting the indices $(x \rightarrow y, y \rightarrow z, z \rightarrow x)$, we obtain the complete set of [angular momentum commutation relations](@entry_id:150953):
$$
[\hat{L}_x, \hat{L}_y] = i\hbar\hat{L}_z
$$
$$
[\hat{L}_y, \hat{L}_z] = i\hbar\hat{L}_x
$$
$$
[\hat{L}_z, \hat{L}_x] = i\hbar\hat{L}_y
$$
These relations form a Lie algebra known as $\mathfrak{su}(2)$ and are the foundation of the quantum theory of angular momentum.

The fact that these commutators are non-zero has profound physical consequences. According to the [generalized uncertainty principle](@entry_id:161890), if two operators do not commute, the corresponding physical observables cannot be simultaneously measured with arbitrary precision. This means that we cannot know the values of $L_x$, $L_y$, and $L_z$ at the same time. If a quantum state has a definite value for $L_z$, its values for $L_x$ and $L_y$ must be uncertain.

Imagine a student who claims it is possible to prepare a non-trivial state $|\psi\rangle$ (one for which the angular momentum is not zero) that is a [simultaneous eigenstate](@entry_id:180828) of both $\hat{L}_x$ and $\hat{L}_z$, with non-zero eigenvalues $\lambda_x$ and $\lambda_z$ respectively [@problem_id:1979277]. Let's test this claim. If it were true, then $\hat{L}_x|\psi\rangle = \lambda_x|\psi\rangle$ and $\hat{L}_z|\psi\rangle = \lambda_z|\psi\rangle$. Applying the commutator $[\hat{L}_x, \hat{L}_z]$ to this state would give $(\hat{L}_x\hat{L}_z - \hat{L}_z\hat{L}_x)|\psi\rangle = (\lambda_x\lambda_z - \lambda_z\lambda_x)|\psi\rangle = 0$. However, from the [commutation relation](@entry_id:150292), we have $[\hat{L}_x, \hat{L}_z]|\psi\rangle = -i\hbar\hat{L}_y|\psi\rangle$. Equating these results implies $-i\hbar\hat{L}_y|\psi\rangle = 0$, which means $\hat{L}_y|\psi\rangle = 0$. Now, consider the commutator $[\hat{L}_y, \hat{L}_z] = i\hbar\hat{L}_x$. Applying this to $|\psi\rangle$ gives $(\hat{L}_y\hat{L}_z - \hat{L}_z\hat{L}_y)|\psi\rangle = \lambda_z\hat{L}_y|\psi\rangle - \hat{L}_z(0) = 0$. But it must also equal $i\hbar\hat{L}_x|\psi\rangle = i\hbar\lambda_x|\psi\rangle$. This leads to the conclusion that $\lambda_x = 0$. A similar argument with $[\hat{L}_x, \hat{L}_y]$ shows that $\lambda_z=0$. The student's claim is therefore incorrect; a non-trivial state cannot have definite values for two different components of angular momentum.

### Total Angular Momentum and Simultaneous Observables

While the components of angular momentum are mutually incompatible, there is a related quantity that is compatible with them. This is the **square of the total angular momentum**, defined as the operator:
$$
\hat{L}^2 = \hat{L}_x^2 + \hat{L}_y^2 + \hat{L}_z^2
$$
Let's investigate the commutation of $\hat{L}^2$ with one of its components, say $\hat{L}_z$ [@problem_id:1352059].
$$
[\hat{L}^2, \hat{L}_z] = [\hat{L}_x^2 + \hat{L}_y^2 + \hat{L}_z^2, \hat{L}_z] = [\hat{L}_x^2, \hat{L}_z] + [\hat{L}_y^2, \hat{L}_z] + [\hat{L}_z^2, \hat{L}_z]
$$
The last term is zero. For the first term, we use the identity $[\hat{A}^2, \hat{B}] = \hat{A}[\hat{A}, \hat{B}] + [\hat{A}, \hat{B}]\hat{A}$:
$$
[\hat{L}_x^2, \hat{L}_z] = \hat{L}_x[\hat{L}_x, \hat{L}_z] + [\hat{L}_x, \hat{L}_z]\hat{L}_x = \hat{L}_x(-i\hbar\hat{L}_y) + (-i\hbar\hat{L}_y)\hat{L}_x = -i\hbar(\hat{L}_x\hat{L}_y + \hat{L}_y\hat{L}_x)
$$
Similarly, for the second term:
$$
[\hat{L}_y^2, \hat{L}_z] = \hat{L}_y[\hat{L}_y, \hat{L}_z] + [\hat{L}_y, \hat{L}_z]\hat{L}_y = \hat{L}_y(i\hbar\hat{L}_x) + (i\hbar\hat{L}_x)\hat{L}_y = i\hbar(\hat{L}_y\hat{L}_x + \hat{L}_x\hat{L}_y)
$$
Summing these contributions, we find they exactly cancel. Therefore:
$$
[\hat{L}^2, \hat{L}_z] = 0
$$
By symmetry, $\hat{L}^2$ commutes with all its components: $[\hat{L}^2, \hat{L}_i] = 0$ for $i=x, y, z$.

The physical significance of this result is immense. Because $\hat{L}^2$ and any one component (conventionally chosen as $\hat{L}_z$) commute, they possess a common set of eigenfunctions. This means we can find quantum states for which both the magnitude of the total angular momentum and its projection onto the z-axis have definite, simultaneously measurable values. This is why atomic and molecular states are labeled by the [quantum numbers](@entry_id:145558) $l$ and $m$, corresponding to the eigenvalues of $\hat{L}^2$ and $\hat{L}_z$, respectively. However, since $[\hat{L}_x, \hat{L}_y] \neq 0$, we cannot simultaneously specify the values of $\hat{L}^2, \hat{L}_x, \hat{L}_y$, and $\hat{L}_z$ [@problem_id:1352059]. The standard choice is to specify the eigenvalues of the commuting set $\{\hat{L}^2, \hat{L}_z\}$.

### The Eigenvalue Spectrum of Angular Momentum

The eigenvalues of $\hat{L}^2$ and $\hat{L}_z$ can be derived purely from their [commutation relations](@entry_id:136780), a testament to the power of algebraic methods in quantum mechanics. Let $| \psi \rangle$ be a [simultaneous eigenstate](@entry_id:180828):
$$
\hat{L}^2 |\psi\rangle = \lambda |\psi\rangle
$$
$$
\hat{L}_z |\psi\rangle = \mu |\psi\rangle
$$
To explore the possible values of $\lambda$ and $\mu$, we introduce the **[ladder operators](@entry_id:156006)**:
$$
\hat{L}_+ = \hat{L}_x + i\hat{L}_y \quad \text{(raising operator)}
$$
$$
\hat{L}_- = \hat{L}_x - i\hat{L}_y \quad \text{(lowering operator)}
$$
Using the fundamental commutation relations, one can show that:
$$
[\hat{L}_z, \hat{L}_\pm] = \pm\hbar\hat{L}_\pm \quad \text{and} \quad [\hat{L}^2, \hat{L}_\pm] = 0
$$
The second relation confirms that applying $\hat{L}_\pm$ to an eigenstate of $\hat{L}^2$ yields another [eigenstate](@entry_id:202009) with the same $\hat{L}^2$ eigenvalue. The first relation reveals the "ladder" property. Consider the state $\hat{L}_+ |\psi\rangle$:
$$
\hat{L}_z (\hat{L}_+ |\psi\rangle) = (\hat{L}_+\hat{L}_z + [\hat{L}_z, \hat{L}_+])|\psi\rangle = (\hat{L}_+\mu + \hbar\hat{L}_+)|\psi\rangle = (\mu + \hbar)(\hat{L}_+ |\psi\rangle)
$$
The new state $\hat{L}_+ |\psi\rangle$ is an [eigenstate](@entry_id:202009) of $\hat{L}_z$ with its eigenvalue raised by $\hbar$. Similarly, $\hat{L}_- |\psi\rangle$ has an eigenvalue of $\mu - \hbar$.

For a physically realistic system, the projection of angular momentum cannot be infinite. For a fixed [total angular momentum](@entry_id:155748) (fixed $\lambda$), there must be a maximum and a minimum value for the projection $\mu$. Let's call the [eigenstate](@entry_id:202009) with the maximum eigenvalue $\mu_{max}$ as $|\psi_{top}\rangle$ and the one with the minimum $\mu_{min}$ as $|\psi_{bot}\rangle$. At these extremes, the [ladder operators](@entry_id:156006) must yield the null state:
$$
\hat{L}_+ |\psi_{top}\rangle = 0 \quad \text{and} \quad \hat{L}_- |\psi_{bot}\rangle = 0
$$
By using the identities $\hat{L}^2 = \hat{L}_-\hat{L}_+ + \hat{L}_z^2 + \hbar\hat{L}_z$ and $\hat{L}^2 = \hat{L}_+\hat{L}_- + \hat{L}_z^2 - \hbar\hat{L}_z$, we can relate $\lambda$ to $\mu_{max}$ and $\mu_{min}$. Applying the first identity to $|\psi_{top}\rangle$ gives $\lambda = \mu_{max}^2 + \hbar\mu_{max}$. Applying the second to $|\psi_{bot}\rangle$ gives $\lambda = \mu_{min}^2 - \hbar\mu_{min}$.

By convention, we re-parameterize the eigenvalues. We define a quantum number $l$ such that $\mu_{max} = l\hbar$, and a [quantum number](@entry_id:148529) $m$ such that $\mu = m\hbar$. The algebraic analysis shows that $\mu_{min} = -l\hbar$, and that the difference between the maximum and minimum values, $l\hbar - (-l\hbar) = 2l\hbar$, must be an integer multiple of $\hbar$. This implies that $2l$ must be an integer, meaning $l$ can be an integer or a half-integer: $l = 0, 1/2, 1, 3/2, \dots$. The eigenvalue of $\hat{L}^2$ is then found to be $\lambda = \hbar^2 l(l+1)$, and for a given $l$, the [magnetic quantum number](@entry_id:145584) $m$ takes the $2l+1$ values: $m = -l, -l+1, \dots, l-1, l$ [@problem_id:2623853]. For the state with the minimum [magnetic quantum number](@entry_id:145584), $m=-l$, applying the lowering operator yields $\hat{L}_- |l, -l\rangle = 0$, confirming it is indeed the bottom of the ladder [@problem_id:2125665].

For **[orbital angular momentum](@entry_id:191303)**, which arises from the spatial motion of a particle, there is an additional constraint. The wavefunction must be single-valued in space. In [spherical coordinates](@entry_id:146054), the operator $\hat{L}_z$ is $-i\hbar \frac{\partial}{\partial\phi}$. The eigenfunction's dependence on the azimuthal angle $\phi$ is $\exp(im\phi)$. For the wavefunction to be single-valued, we must have $\exp(im\phi) = \exp(im(\phi+2\pi))$, which requires $m$ to be an integer. Since $m$ takes values up to $l$, this forces the [orbital angular momentum quantum number](@entry_id:167573) $l$ to also be an integer: $l=0, 1, 2, \dots$ [@problem_id:2623853].

### Realizations of Angular Momentum: Operators and Wavefunctions

The abstract algebraic framework comes to life when we consider its action on specific functions. The simultaneous eigenfunctions of $\hat{L}^2$ and $\hat{L}_z$ in spherical coordinates are the well-known **[spherical harmonics](@entry_id:156424)**, denoted $Y_{l,m}(\theta, \phi)$.

The raising operator $\hat{L}_+$, when expressed in spherical coordinates, takes the form $\hat{L}_+ = \hbar e^{i\phi}(\frac{\partial}{\partial\theta} + i\cot\theta\frac{\partial}{\partial\phi})$. Let's see its action on the state $Y_{1,0}(\theta, \phi) = \sqrt{\frac{3}{4\pi}}\cos\theta$ [@problem_id:2099713].
$$
\hat{L}_+ Y_{1,0} = \hbar e^{i\phi} \left( \frac{\partial}{\partial\theta} + i\cot\theta\frac{\partial}{\partial\phi} \right) \left(\sqrt{\frac{3}{4\pi}}\cos\theta\right)
$$
Since $Y_{1,0}$ is independent of $\phi$, the second term in the parenthesis gives zero.
$$
\hat{L}_+ Y_{1,0} = \hbar e^{i\phi} \sqrt{\frac{3}{4\pi}} (-\sin\theta) = -\hbar \sqrt{\frac{3}{4\pi}} \sin\theta e^{i\phi}
$$
The spherical harmonic for $l=1, m=1$ is $Y_{1,1}(\theta, \phi) = -\sqrt{\frac{3}{8\pi}}\sin\theta e^{i\phi}$. We can see that our result is proportional to $Y_{1,1}$.
$$
\hat{L}_+ Y_{1,0} = \hbar \sqrt{2} \left(-\sqrt{\frac{3}{8\pi}}\sin\theta e^{i\phi}\right) = \hbar\sqrt{2} Y_{1,1}
$$
This explicitly demonstrates the "raising" action, transforming the state from $m=0$ to $m=1$. The coefficient $\hbar\sqrt{2}$ matches the general formula $\hat{L}_+|l,m\rangle = \hbar\sqrt{l(l+1)-m(m+1)}|l,m+1\rangle$ for $l=1, m=0$.

We can also apply the operators in their Cartesian representation. Consider the function $\psi(x,y,z) = Cxy$. Applying the full $\hat{L}^2$ operator to this function involves a sequence of partial differentiations [@problem_id:2143166]. A step-by-step calculation reveals:
$$
\hat{L}_x^2 \psi = \hbar^2 Cxy
$$
$$
\hat{L}_y^2 \psi = \hbar^2 Cxy
$$
$$
\hat{L}_z^2 \psi = 4\hbar^2 Cxy
$$
Summing these gives the action of the [total angular momentum](@entry_id:155748) squared operator:
$$
\hat{L}^2 \psi = (\hat{L}_x^2 + \hat{L}_y^2 + \hat{L}_z^2)\psi = (1+1+4)\hbar^2 Cxy = 6\hbar^2 Cxy
$$
Since $6\hbar^2$ can be written as $\hbar^2 \times 2(2+1)$, we see that the function $\psi = Cxy$ is an eigenfunction of $\hat{L}^2$ with quantum number $l=2$.

### Conservation of Angular Momentum

In classical physics, angular momentum is conserved for a system subject to a [central force](@entry_id:160395). The same principle holds in quantum mechanics. A quantity is conserved if its corresponding operator commutes with the Hamiltonian, $\hat{H}$. For a particle of mass $m$ in a central potential $V(r)$, where $r = \sqrt{x^2+y^2+z^2}$, the Hamiltonian is $\hat{H} = \frac{\hat{p}^2}{2m} + V(r)$.

Let's check the commutator $[\hat{H}, \hat{L}_z]$ [@problem_id:1979272].
$$
[\hat{H}, \hat{L}_z] = \left[\frac{\hat{p}_x^2 + \hat{p}_y^2 + \hat{p}_z^2}{2m}, \hat{L}_z\right] + [V(r), \hat{L}_z]
$$
The kinetic energy term commutes with $\hat{L}_z$ because $[\hat{p}_x^2, \hat{L}_z] = -i\hbar(\hat{p}_x\hat{p}_y+\hat{p}_y\hat{p}_x)$ and $[\hat{p}_y^2, \hat{L}_z] = i\hbar(\hat{p}_y\hat{p}_x+\hat{p}_x\hat{p}_y)$ cancel each other out, while $[\hat{p}_z^2, \hat{L}_z]=0$.
For the potential energy term, we use $[V(r), \hat{L}_z] = [V(r), \hat{x}\hat{p}_y - \hat{y}\hat{p}_x] = \hat{x}[V(r), \hat{p}_y] - \hat{y}[V(r), \hat{p}_x]$. Using the relation $[f(\vec{r}), \hat{p}_j] = i\hbar \frac{\partial f}{\partial x_j}$, we get:
$$
[V(r), \hat{L}_z] = i\hbar\left(\hat{x}\frac{\partial V}{\partial y} - \hat{y}\frac{\partial V}{\partial x}\right) = i\hbar\left(x\frac{y}{r}\frac{dV}{dr} - y\frac{x}{r}\frac{dV}{dr}\right) = 0
$$
Since both parts of the Hamiltonian commute with $\hat{L}_z$, we have $[\hat{H}, \hat{L}_z]=0$. A similar derivation shows $[\hat{H}, \hat{L}^2]=0$. This means that for any system in a central potential, such as an electron in a hydrogen atom, the total angular momentum and its z-component are conserved quantities. Their eigenvalues, characterized by $l$ and $m$, are "[good quantum numbers](@entry_id:262514)" used to label the [stationary states](@entry_id:137260) ([energy eigenstates](@entry_id:152154)) of the system.

### Intrinsic Spin and the Combination of Angular Momenta

The algebraic structure of angular momentum is general. It applies not only to orbital motion but also to an intrinsic, purely quantum mechanical property of particles called **spin**. Spin angular momentum, denoted by $\hat{\mathbf{S}}$, obeys the same [commutation relations](@entry_id:136780): $[\hat{S}_x, \hat{S}_y] = i\hbar\hat{S}_z$, etc. However, the spin quantum number $s$ is not constrained by wavefunction single-valuedness and can be a half-integer.

The electron, a fundamental particle, is a fermion with an intrinsic [spin quantum number](@entry_id:142550) $s=1/2$. The magnitude of an electron's spin is constant. The eigenvalue of the total spin squared operator, $\hat{S}^2$, is given by the same general formula we derived: $s(s+1)\hbar^2$. For an electron, this value is [@problem_id:1352054]:
$$
s(s+1)\hbar^2 = \frac{1}{2}\left(\frac{1}{2}+1\right)\hbar^2 = \frac{3}{4}\hbar^2
$$
The [spin projection](@entry_id:184359) quantum number, $m_s$, can take the values $-s, \dots, s$, which for an electron means $m_s = -1/2$ or $m_s = +1/2$, often called "spin down" and "spin up".

In atoms, an electron possesses both orbital angular momentum $\hat{\mathbf{L}}$ and spin angular momentum $\hat{\mathbf{S}}$. These two momenta can interact, a phenomenon known as **spin-orbit coupling**. The interaction energy is proportional to the operator $\hat{\mathbf{L}} \cdot \hat{\mathbf{S}}$. To understand this term, it is useful to define the **total angular momentum** operator $\hat{\mathbf{J}} = \hat{\mathbf{L}} + \hat{\mathbf{S}}$.

The square of this [total angular momentum operator](@entry_id:149439) is:
$$
\hat{J}^2 = (\hat{\mathbf{L}} + \hat{\mathbf{S}}) \cdot (\hat{\mathbf{L}} + \hat{\mathbf{S}}) = \hat{L}^2 + \hat{S}^2 + 2\hat{\mathbf{L}} \cdot \hat{\mathbf{S}}
$$
This identity provides an elegant way to handle the spin-orbit term by rewriting it as:
$$
\hat{\mathbf{L}} \cdot \hat{\mathbf{S}} = \frac{1}{2}(\hat{J}^2 - \hat{L}^2 - \hat{S}^2)
$$
In the presence of spin-orbit coupling, the individual momenta $\hat{\mathbf{L}}$ and $\hat{\mathbf{S}}$ are no longer conserved, but the [total angular momentum](@entry_id:155748) $\hat{\mathbf{J}}$ is. The states of the atom are thus best described by quantum numbers $j, l,$ and $s$. The expectation value of the [spin-orbit interaction](@entry_id:143481) can be readily calculated. For a state with [quantum numbers](@entry_id:145558) $j, l,$ and $s$, the [expectation value](@entry_id:150961) is [@problem_id:1398403]:
$$
\langle \hat{\mathbf{L}} \cdot \hat{\mathbf{S}} \rangle = \frac{1}{2} \langle \hat{J}^2 - \hat{L}^2 - \hat{S}^2 \rangle = \frac{\hbar^2}{2} [j(j+1) - l(l+1) - s(s+1)]
$$
For example, consider an electron in a state with $l=1$ (a p-orbital) and $s=1/2$. The possible [total angular momentum](@entry_id:155748) quantum numbers are $j = l+s = 3/2$ and $j = l-s = 1/2$. For the state with $j=3/2$, the spin-orbit energy term is:
$$
\langle \hat{\mathbf{L}} \cdot \hat{\mathbf{S}} \rangle = \frac{\hbar^2}{2} \left[ \frac{3}{2}\left(\frac{5}{2}\right) - 1(2) - \frac{1}{2}\left(\frac{3}{2}\right) \right] = \frac{\hbar^2}{2} \left[ \frac{15}{4} - 2 - \frac{3}{4} \right] = \frac{\hbar^2}{2} [1] = \frac{\hbar^2}{2}
$$
This powerful technique of [combining angular momenta](@entry_id:193812) is central to [atomic spectroscopy](@entry_id:155968) and understanding the fine structure of atomic energy levels.