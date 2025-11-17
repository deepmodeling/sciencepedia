## Introduction
The Schrödinger equation provides the complete blueprint for the behavior of quantum systems, but it can only be solved exactly for a handful of highly idealized scenarios. For real-world systems like [multi-electron atoms](@entry_id:157716) and molecules, exact solutions are out of reach, creating a significant gap between fundamental theory and chemical reality. To bridge this gap, we must rely on powerful approximation methods. The variational principle stands as one of the most profound and versatile of these tools, providing a rigorous framework for estimating the energies of quantum systems and laying the groundwork for much of modern computational chemistry.

This article will guide you through the theory and application of this cornerstone principle. The first chapter, **Principles and Mechanisms**, will introduce the variational theorem, walk through its proof, and detail the practical mechanics of the method, including the use of variational parameters and the powerful [linear variational method](@entry_id:150058). Following this, the **Applications and Interdisciplinary Connections** chapter will demonstrate the principle in action, from refining estimates for simple models to its crucial role in describing chemical bonding through Molecular Orbital theory and justifying methods like Hartree-Fock. Finally, the **Hands-On Practices** section will provide you with the opportunity to apply these concepts to solve concrete problems, solidifying your understanding of how this elegant theory becomes a practical tool for every quantum chemist.

## Principles and Mechanisms

The time-independent Schrödinger equation, $\hat{H}\psi = E\psi$, can be solved analytically for only a small number of idealized quantum mechanical systems. For the vast majority of systems of chemical and physical interest, from [multi-electron atoms](@entry_id:157716) to molecules, exact solutions are unattainable. We must, therefore, turn to approximation methods. The [variational principle](@entry_id:145218) provides a powerful and widely applicable framework for finding approximate solutions and is the theoretical foundation for many of the most important methods in modern computational chemistry.

### The Variational Theorem: A Foundation for Approximation

The variational theorem provides a simple yet profound statement about the energy of any possible state of a quantum system. It states that for a system described by a Hamiltonian operator $\hat{H}$, the [expectation value](@entry_id:150961) of the energy for any well-behaved, normalized trial wavefunction $\phi$ is always greater than or equal to the true ground-state energy, $E_0$. This [expectation value](@entry_id:150961), often called the variational integral or Rayleigh quotient, is denoted by $W$:

$$
W = \int \phi^* \hat{H} \phi \,d\tau = \langle \phi | \hat{H} | \phi \rangle \ge E_0
$$

The proof of this theorem is straightforward and illuminating. Let the true, complete, and [orthonormal set](@entry_id:271094) of [eigenfunctions](@entry_id:154705) of the Hamiltonian be $\{\psi_n\}$ with corresponding [energy eigenvalues](@entry_id:144381) $\{E_n\}$, such that $\hat{H}\psi_n = E_n\psi_n$. By convention, we order the energies such that $E_0 \le E_1 \le E_2 \le \dots$. Since this set of eigenfunctions is complete, any well-behaved [trial function](@entry_id:173682) $\phi$ can be expanded as a linear combination of them:

$$
\phi = \sum_{n=0}^{\infty} c_n \psi_n
$$

where $c_n = \langle \psi_n | \phi \rangle$ are the expansion coefficients. If $\phi$ is normalized, then $\langle \phi | \phi \rangle = 1$, which implies:

$$
\langle \sum_m c_m \psi_m | \sum_n c_n \psi_n \rangle = \sum_m \sum_n c_m^* c_n \langle \psi_m | \psi_n \rangle = \sum_m \sum_n c_m^* c_n \delta_{mn} = \sum_{n=0}^{\infty} |c_n|^2 = 1
$$

Now, let's evaluate the variational integral $W$:

$$
W = \langle \phi | \hat{H} | \phi \rangle = \langle \sum_m c_m \psi_m | \hat{H} | \sum_n c_n \psi_n \rangle = \langle \sum_m c_m \psi_m | \sum_n c_n (E_n \psi_n) \rangle
$$

$$
W = \sum_m \sum_n c_m^* c_n E_n \langle \psi_m | \psi_n \rangle = \sum_m \sum_n c_m^* c_n E_n \delta_{mn} = \sum_{n=0}^{\infty} |c_n|^2 E_n
$$

This expression shows that the variational energy is a weighted average of the true [energy eigenvalues](@entry_id:144381), where the weighting factors are the squared magnitudes of the expansion coefficients, $|c_n|^2$. To see the inequality, we subtract the [ground state energy](@entry_id:146823) $E_0$ from $W$:

$$
W - E_0 = \sum_{n=0}^{\infty} |c_n|^2 E_n - E_0 = \sum_{n=0}^{\infty} |c_n|^2 E_n - E_0 \left( \sum_{n=0}^{\infty} |c_n|^2 \right) = \sum_{n=0}^{\infty} |c_n|^2 (E_n - E_0)
$$

Since $E_n \ge E_0$ for all $n$, every term in the summation $(E_n - E_0)$ is non-negative. As $|c_n|^2$ is also non-negative, the entire sum must be greater than or equal to zero: $W - E_0 \ge 0$, which proves the theorem.

The theorem also specifies the condition for equality. The sum $\sum |c_n|^2 (E_n - E_0)$ can only be zero if all terms are zero. For any term where $E_n > E_0$, we must have $c_n=0$. This means that for the equality $W = E_0$ to hold, the expansion of $\phi$ can only contain contributions from [eigenfunctions](@entry_id:154705) that have the energy $E_0$.

In the simplest case, where the ground state is non-degenerate, this means that the [trial function](@entry_id:173682) $\phi$ must be the true ground state [eigenfunction](@entry_id:149030) $\psi_0$ (or a scalar multiple of it). If, by a stroke of insight or luck, one were to choose $\phi = \psi_0$, the variational integral would yield the exact [ground state energy](@entry_id:146823), $W = E_0$ [@problem_id:1416110].

A more subtle situation arises if the ground state is degenerate, meaning there are multiple [linearly independent](@entry_id:148207) [eigenfunctions](@entry_id:154705) (e.g., $\psi_{0,1}, \psi_{0,2}, \dots$) that share the same lowest energy $E_0$. In this scenario, the equality $W = E_0$ holds if the trial function $\phi$ is any linear combination of these degenerate ground-state [eigenfunctions](@entry_id:154705). For instance, if a student constructs a [trial function](@entry_id:173682) $\psi_{trial}$ that is different from a known ground [state function](@entry_id:141111) $\psi_0$ but still finds that its variational energy is exactly $E_0$, the only physical explanation is that the ground state is degenerate, and $\psi_{trial}$ is simply another function within that degenerate ground-state subspace [@problem_id:2144184].

### The Variational Method in Practice

The variational theorem provides the theoretical basis for the **variational method**: a systematic procedure for approximating the ground state energy and wavefunction. The strategy is to devise a [trial function](@entry_id:173682) $\phi$ that depends on one or more adjustable parameters, and then to minimize the calculated variational energy $W$ with respect to those parameters. The resulting minimized energy is the best possible estimate for the ground state energy that can be achieved with that particular form of [trial function](@entry_id:173682).

#### The Rayleigh Quotient and Normalization

In practice, it is often inconvenient to work with [trial functions](@entry_id:756165) that are pre-normalized. Fortunately, the variational principle can be expressed in a form that works for any [trial function](@entry_id:173682), normalized or not. This is achieved using the **Rayleigh quotient**, which we will denote as $E[\phi]$:

$$
E[\phi] = \frac{\langle \phi | \hat{H} | \phi \rangle}{\langle \phi | \phi \rangle} = \frac{\int \phi^* \hat{H} \phi \,d\tau}{\int \phi^* \phi \,d\tau}
$$

This expression is automatically independent of the normalization of $\phi$. To see this, consider two [trial functions](@entry_id:756165) where one is simply a constant multiple of the other, such as $\phi_2 = c \phi_1$. The variational energy for $\phi_2$ is:

$$
E[\phi_2] = \frac{\langle c\phi_1 | \hat{H} | c\phi_1 \rangle}{\langle c\phi_1 | c\phi_1 \rangle} = \frac{c^*c \langle \phi_1 | \hat{H} | \phi_1 \rangle}{c^*c \langle \phi_1 | \phi_1 \rangle} = \frac{|c|^2 \langle \phi_1 | \hat{H} | \phi_1 \rangle}{|c|^2 \langle \phi_1 | \phi_1 \rangle} = E[\phi_1]
$$

The [normalization constant](@entry_id:190182) cancels completely. This is a significant practical advantage, as it allows us to choose [trial functions](@entry_id:756165) with the simplest possible mathematical form, without worrying about normalization until the very end, if at all [@problem_id:1416059].

#### Introducing and Optimizing Variational Parameters

The power of the variational method comes from using flexible [trial functions](@entry_id:756165). We can introduce one or more **variational parameters** into our [trial function](@entry_id:173682), $\phi(\alpha, \beta, \dots)$. The variational energy will then be a function of these parameters, $E(\alpha, \beta, \dots)$. The core of the method is to find the optimal values of these parameters by minimizing the energy. According to the variational principle, this minimized energy will be the tightest possible upper bound on $E_0$ for that family of [trial functions](@entry_id:756165).

The minimization procedure is a standard problem in calculus. For a single parameter $\alpha$, we find the optimal value $\alpha_{\text{opt}}$ by solving the equation:

$$
\frac{dE(\alpha)}{d\alpha} = 0
$$

One must then verify that this solution corresponds to a minimum (e.g., by checking that the second derivative is positive).

For example, suppose a simplified model for a quantum system yields a variational energy that depends on a parameter $\alpha$ as $E(\alpha) = A \alpha^2 + B/\alpha$, where $A$ and $B$ are positive constants [@problem_id:1416091]. To find the best estimate for the [ground state energy](@entry_id:146823), we differentiate with respect to $\alpha$ and set the result to zero:

$$
\frac{dE}{d\alpha} = 2A\alpha - \frac{B}{\alpha^2} = 0
$$

Solving for $\alpha$ gives the optimal value, $\alpha_{\text{opt}}$:

$$
2A\alpha^3 = B \implies \alpha_{\text{opt}} = \left(\frac{B}{2A}\right)^{1/3}
$$

Substituting this value back into the expression for $E(\alpha)$ gives the lowest possible energy for this form of [trial function](@entry_id:173682), our variational estimate for $E_0$.

#### A Worked Example: The Particle in a Box

Let's apply these ideas to a familiar system: a particle of mass $m$ in a one-dimensional box of length $L$. The Hamiltonian inside the box ($0 < x < L$) is $\hat{H} = -\frac{\hbar^2}{2m}\frac{d^2}{dx^2}$. We know the exact ground state energy is $E_1 = \frac{\pi^2 \hbar^2}{2mL^2}$.

Let's propose a simple, unnormalized [trial function](@entry_id:173682) that satisfies the boundary conditions, $\phi(0) = \phi(L) = 0$. A parabolic function is a reasonable choice: $\phi(x) = x(L-x)$ [@problem_id:2023268]. We calculate the Rayleigh quotient:

$$
E_{trial} = \frac{\int_0^L x(L-x) \left( -\frac{\hbar^2}{2m}\frac{d^2}{dx^2} \right) x(L-x) \,dx}{\int_0^L [x(L-x)]^2 \,dx}
$$

First, we evaluate the action of the Hamiltonian on the trial function: $\frac{d^2}{dx^2}(Lx-x^2) = -2$. So, $\hat{H}\phi = -\frac{\hbar^2}{2m}(-2) = \frac{\hbar^2}{m}$.

The numerator integral is:
$$
\int_0^L x(L-x) \left( \frac{\hbar^2}{m} \right) \,dx = \frac{\hbar^2}{m} \int_0^L (Lx-x^2) \,dx = \frac{\hbar^2}{m} \left[ \frac{Lx^2}{2} - \frac{x^3}{3} \right]_0^L = \frac{\hbar^2 L^3}{6m}
$$

The denominator integral is:
$$
\int_0^L (Lx-x^2)^2 \,dx = \int_0^L (L^2x^2 - 2Lx^3 + x^4) \,dx = \left[ \frac{L^2x^3}{3} - \frac{2Lx^4}{4} + \frac{x^5}{5} \right]_0^L = \frac{L^5}{30}
$$

Combining these gives the variational energy:
$$
E_{trial} = \frac{\hbar^2 L^3 / (6m)}{L^5 / 30} = \frac{30\hbar^2}{6mL^2} = \frac{5\hbar^2}{mL^2}
$$

As the [variational principle](@entry_id:145218) guarantees, this energy is higher than the true ground state energy. We can see how good the approximation is by taking the ratio:

$$
\frac{E_{trial}}{E_1} = \frac{5\hbar^2/mL^2}{\pi^2 \hbar^2 / 2mL^2} = \frac{10}{\pi^2} \approx 1.013
$$

Our simple parabolic [trial function](@entry_id:173682) yields an energy that is only about $1.3\%$ above the true ground state energy, demonstrating the remarkable effectiveness of the method.

#### Judging the Quality of a Trial Wavefunction

If we perform two separate variational calculations for the same system using two different families of [trial functions](@entry_id:756165), say $\phi_A$ and $\phi_B$, yielding minimized energies $E_A$ and $E_B$, the variational principle gives us a clear criterion for comparison: the lower energy corresponds to the better trial wavefunction. Both $E_A$ and $E_B$ are upper bounds to $E_0$, so the one that is lower is the tighter bound and thus a better approximation.

Consider, for instance, estimating the [ground state energy](@entry_id:146823) of a particle in an attractive [delta-function potential](@entry_id:189699), $V(x) = -\alpha \delta(x)$ [@problem_id:2144152]. One could propose a Gaussian [trial function](@entry_id:173682), $\psi_G(x, \beta) \propto \exp(-\beta x^2)$, or a Lorentzian trial function, $\psi_L(x, \gamma) \propto (\gamma^2 + x^2)^{-1}$. After optimizing the respective variational parameters $\beta$ and $\gamma$, one finds the minimized energies are $E_G = - \frac{m \alpha^{2}}{\pi \hbar^{2}}$ and $E_L = - \frac{4 m \alpha^{2}}{\pi^{2} \hbar^{2}}$. Since $\frac{1}{\pi} \approx 0.318$ and $\frac{4}{\pi^2} \approx 0.405$, we have $E_L  E_G$ (both are negative). This indicates that, for this specific potential, the Lorentzian functional form allows for a better approximation of the true ground state wavefunction than the Gaussian form, as it yields a lower (tighter) energy bound.

### The Linear Variational Method

A particularly powerful and systematic implementation of the variational principle is the **[linear variational method](@entry_id:150058)**. This approach is the cornerstone of many quantum chemistry techniques. The trial wavefunction $\Psi$ is constructed as a linear combination of a set of $N$ pre-chosen basis functions $\{\phi_1, \phi_2, \dots, \phi_N\}$:

$$
\Psi = \sum_{i=1}^N c_i \phi_i
$$

Here, the basis functions $\phi_i$ are fixed, and the variational parameters are the linear coefficients $c_i$. The goal is to find the set of coefficients $\{c_i\}$ that minimizes the Rayleigh quotient:

$$
E = \frac{\langle \sum_i c_i \phi_i | \hat{H} | \sum_j c_j \phi_j \rangle}{\langle \sum_i c_i \phi_i | \sum_j c_j \phi_j \rangle} = \frac{\sum_{i,j} c_i^* c_j H_{ij}}{\sum_{i,j} c_i^* c_j S_{ij}}
$$

where we have defined the **Hamiltonian matrix** elements $H_{ij} = \langle \phi_i | \hat{H} | \phi_j \rangle$ and the **overlap matrix** elements $S_{ij} = \langle \phi_i | \phi_j \rangle$.

Minimizing $E$ with respect to each coefficient $c_k$ leads to a set of $N$ simultaneous linear equations known as the secular equations, which can be written in matrix form as:

$$
\mathbf{H} \mathbf{c} = E \mathbf{S} \mathbf{c}
$$

This is a [generalized eigenvalue problem](@entry_id:151614). Solving it yields $N$ real eigenvalues (energies) $E_k$ and $N$ corresponding eigenvectors (sets of coefficients) $\mathbf{c}_k$.

The [variational principle](@entry_id:145218) guarantees that the lowest of these [energy eigenvalues](@entry_id:144381), let's call it $E_-$, is an upper bound to the true [ground state energy](@entry_id:146823) $E_0$ [@problem_id:1416060]. That is, $E_- \ge E_0$. The other eigenvalues, $E_k$, are upper bounds to the energies of the higher excited states, a result known as the MacDonald-Hylleraas-Undheim theorem.

A fundamental concept in quantum chemistry is the systematic improvement of calculations by expanding the basis set. Suppose a calculation with a basis of $N$ functions yields a ground state estimate $E_N$. If we then perform a new calculation with an enlarged basis set of $M  N$ functions, which includes all of the original $N$ functions, we obtain a new energy estimate $E_M$ [@problem_id:1416117]. The space of all possible [trial functions](@entry_id:756165) that can be formed by the $M$ basis functions is a superset of the space spanned by the original $N$ functions. Because the second minimization is performed over a larger, more flexible space, it can only find a better (lower) or equally good energy, but never a worse one. Therefore, the relationship between the energies is always:

$$
E_M \le E_N
$$

This principle of non-increasing energy with an expanding basis set is what drives the quest for larger and more complete [basis sets](@entry_id:164015) in high-accuracy computational chemistry.

### Approximating Excited States

The basic [variational principle](@entry_id:145218) guarantees an upper bound for the ground state. However, it can be extended to find approximations for excited states. The general theorem is: if a normalized trial function $\phi$ is orthogonal to the true eigenfunctions of all states with energy lower than $E_k$, then its variational energy $\langle \phi | \hat{H} | \phi \rangle$ is an upper bound to the energy of the $k$-th state, $E_k$.

The practical difficulty is that we usually do not know the true [eigenfunctions](@entry_id:154705) of the lower states. However, two common strategies can be employed.

1.  **Enforced Orthogonality:** We can estimate the first excited state energy, $E_1$, by using a [trial function](@entry_id:173682) $\phi_2$ that we explicitly construct to be orthogonal to a good approximation of the ground state wavefunction, $\phi_1$. For instance, for the [particle in a box](@entry_id:140940), we might use the parabolic function $\phi_1(x) = x(L-x)$ as our approximate ground state. We could then construct an appropriate [trial function](@entry_id:173682) for the first excited state, such as $\phi_2(x) = x(L-x)(2x-L)$, which is orthogonal to $\phi_1$ over the interval $[0, L]$ [@problem_id:1416104]. Calculating the Rayleigh quotient for this $\phi_2$ will yield an energy $W_2$ that is guaranteed to be an upper bound for the true first excited state energy, $E_1$. (Note: Here, $E_1$ refers to the first excited state, not the ground state as in the previous example).

2.  **Symmetry:** A more elegant and powerful approach is available when the system's Hamiltonian possesses symmetry. The [eigenfunctions](@entry_id:154705) of a symmetric Hamiltonian can be classified according to their symmetry properties (e.g., as even or odd with respect to inversion). Functions of different symmetry are automatically orthogonal. If the ground state $\psi_0$ belongs to one symmetry class, we can find an upper bound for the energy of the lowest-lying excited state of a *different* symmetry class by simply choosing a [trial function](@entry_id:173682) with that symmetry. This trial function will be automatically orthogonal to $\psi_0$.

A classic example is the one-dimensional [quantum harmonic oscillator](@entry_id:140678), with its [symmetric potential](@entry_id:148561) $V(x) = \frac{1}{2}m\omega^2x^2$ [@problem_id:2144162]. The ground state is known to be an even function. The first excited state is an odd function. Therefore, to estimate the energy of the first excited state, we can simply choose a trial function that is odd, such as $\psi_t(x) = C x \exp(-ax^2)$. Because this function is odd, its overlap integral with the even ground state is identically zero. A variational calculation on $\psi_t$ will thus directly provide an upper bound for the first excited state energy, $E_1$. In this particular case, this [trial function](@entry_id:173682) has the exact functional form of the true first excited state, and the [variational method](@entry_id:140454) remarkably yields the exact energy, $E_1 = \frac{3}{2}\hbar\omega$.