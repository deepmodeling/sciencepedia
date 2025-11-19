## Introduction
The interaction between light and matter is a cornerstone of physics, but in the regime of low light intensity, this relationship is deceptively simple and linear. When powerful lasers illuminate a material, the response becomes dramatically more complex and fascinating, ushering in the field of [nonlinear optics](@entry_id:141753). At the heart of this field lie the **nonlinear susceptibilities**, denoted $\chi^{(n)}$, which are intrinsic material properties that quantify the strength and nature of this nonlinear response. Understanding the origin, properties, and consequences of these susceptibilities is essential for harnessing and interpreting the vast array of phenomena that emerge when light's intensity is sufficient to alter the medium through which it propagates. This article addresses the fundamental question of what governs these nonlinear coefficients, bridging the gap from microscopic quantum interactions to macroscopic optical effects.

Over the next three chapters, you will embark on a systematic exploration of this topic. First, the chapter on **Principles and Mechanisms** will lay the theoretical groundwork, deriving the form of nonlinear susceptibilities from both classical and quantum mechanical models and detailing the profound impact of [material symmetry](@entry_id:173835). Next, the chapter on **Applications and Interdisciplinary Connections** will showcase how these principles are applied in technologies like frequency conversion and [materials characterization](@entry_id:161346), and how they connect optics to fields as diverse as condensed matter physics and [gravitation](@entry_id:189550). Finally, the **Hands-On Practices** section provides an opportunity to apply this theoretical knowledge to concrete problems, solidifying your understanding of the concepts. We begin by delving into the fundamental principles that dictate the very existence and form of the nonlinear response.

## Principles and Mechanisms

The interaction of light with matter gives rise to a polarization $\mathbf{P}$ that acts as a [source term](@entry_id:269111) in Maxwell's equations, mediating the propagation of light. In the regime of linear optics, this polarization is directly proportional to the incident electric field $\mathbf{E}$. However, when the intensity of the light field becomes comparable to the internal atomic fields, this linear relationship breaks down. The material's response becomes nonlinear, and the induced polarization is more accurately described by a [power series expansion](@entry_id:273325) in the electric field:

$$
P_i = \epsilon_0 \left( \sum_j \chi_{ij}^{(1)} E_j + \sum_{j,k} \chi_{ijk}^{(2)} E_j E_k + \sum_{j,k,l} \chi_{ijkl}^{(3)} E_j E_k E_l + \dots \right)
$$

Here, $P_i$ is the $i$-th Cartesian component of the polarization vector, $E_j$ are the components of the electric field, and $\epsilon_0$ is the [permittivity of free space](@entry_id:272823). The coefficients $\chi^{(n)}$ are the **nonlinear optical susceptibilities**, which are tensor quantities that intrinsically characterize the material's nonlinear response. The first-order susceptibility, $\chi^{(1)}$, governs linear optical phenomena like refraction and absorption. The higher-order terms, $\chi^{(2)}$ (second-order) and $\chi^{(3)}$ (third-order), are responsible for a vast array of nonlinear optical effects, such as [second-harmonic generation](@entry_id:145639), [sum-frequency generation](@entry_id:168681), and [four-wave mixing](@entry_id:164327). This chapter delves into the fundamental principles that govern the form and function of these nonlinear susceptibilities.

### Classical Origins: The Anharmonic Oscillator Model

A highly instructive, albeit classical, picture of nonlinearity emerges from the **[anharmonic oscillator](@entry_id:142760) model**. In this model, we consider a solid to be a collection of atoms, where each atom's valence electron is bound to the nucleus by a potential. For small displacements, this potential is harmonic, leading to a linear restoring force. However, for larger displacements induced by a strong electric field, the potential becomes anharmonic.

Let us model an electron of charge $q$ and mass $m$ as a one-dimensional oscillator. Its displacement from equilibrium, $x(t)$, under the influence of a driving electric field $E(t)$ can be described by an [equation of motion](@entry_id:264286) that includes anharmonic terms:

$$
\ddot{x} + \gamma \dot{x} + \omega_0^2 x + \alpha x^2 + \beta x^3 = \frac{q}{m} E(t)
$$

Here, $\omega_0$ is the natural resonant frequency of the harmonic oscillator, $\gamma$ is a damping coefficient representing loss mechanisms, and $\alpha$ and $\beta$ are anharmonic coefficients that quantify the strength of the nonlinearity. The terms $\alpha x^2$ and $\beta x^3$ correspond to quadratic and cubic deviations from a purely harmonic restoring force, $-m\omega_0^2 x$. These are the terms that give rise to $\chi^{(2)}$ and $\chi^{(3)}$ responses, respectively.

To see how, we can solve this equation perturbatively. Let the driving field consist of two distinct frequencies, $E(t) = \frac{1}{2} ( E_1 e^{-i\omega_1 t} + E_2 e^{-i\omega_2 t} + \text{c.c.} )$. We expand the displacement $x(t)$ in powers of the field strength: $x(t) = x^{(1)}(t) + x^{(2)}(t) + \dots$.

The first-order (linear) response, $x^{(1)}(t)$, satisfies the driven [harmonic oscillator](@entry_id:155622) equation. In the frequency domain, its solution is:

$$
x^{(1)}(\omega_j) = \frac{q E_j / m}{\omega_0^2 - \omega_j^2 - i\gamma\omega_j}
$$

The denominator, often written as $D(\omega_j) = \omega_0^2 - \omega_j^2 - i\gamma\omega_j$, reveals the characteristic resonant enhancement of the response when a driving frequency $\omega_j$ approaches the natural frequency $\omega_0$.

The second-order response, $x^{(2)}(t)$, is driven by the nonlinearity acting on the first-order solution. The equation for $x^{(2)}$ is:

$$
\ddot{x}^{(2)} + \gamma \dot{x}^{(2)} + \omega_0^2 x^{(2)} = -\alpha [x^{(1)}(t)]^2
$$

The term $[x^{(1)}(t)]^2$ contains frequency components at $2\omega_1$, $2\omega_2$, DC ($\omega_1 - \omega_1$), and, most importantly for our example, the sum and difference frequencies $\omega_1 \pm \omega_2$. For instance, considering the sum-frequency component at $\omega_s = \omega_1 + \omega_2$, the driving term is proportional to $E_1 E_2 e^{-i(\omega_1+\omega_2)t}$. Solving for the displacement at this new frequency yields:

$$
x^{(2)}(\omega_s) = -\frac{\alpha}{2} \frac{x^{(1)}(\omega_1) x^{(1)}(\omega_2)}{D(\omega_s)} = -\frac{\alpha}{2} \frac{(q/m)^2 E_1 E_2}{D(\omega_1) D(\omega_2) D(\omega_s)}
$$

The [macroscopic polarization](@entry_id:141855) is $P(t) = N q x(t)$, where $N$ is the density of oscillators. The second-order polarization at the sum frequency is therefore $P^{(2)}(\omega_s) = N q x^{(2)}(\omega_s)$. By comparing this to the phenomenological definition $P^{(2)}(\omega_s) = \epsilon_0 \chi^{(2)}(-\omega_s; \omega_1, \omega_2) E_1 E_2$, we can identify the [second-order susceptibility](@entry_id:166773) for [sum-frequency generation](@entry_id:168681) [@problem_id:696597]:

$$
\chi^{(2)}(-(\omega_1+\omega_2); \omega_1, \omega_2) = -\frac{N q^3 \alpha}{2\epsilon_{0}m^{2} D(\omega_1+\omega_2) D(\omega_1) D(\omega_2)}
$$

This expression elegantly encapsulates the key features of the [second-order susceptibility](@entry_id:166773): it is proportional to the density of [nonlinear oscillators](@entry_id:266739) ($N$) and the strength of the anharmonicity ($\alpha$), and it exhibits a triple resonance behavior, being enhanced when any of the input frequencies or the generated sum frequency approaches the material's natural resonance $\omega_0$.

### Quantum Mechanical Origins

While the classical model provides valuable intuition, a rigorous description of nonlinear susceptibilities must be rooted in quantum mechanics. In the quantum picture, nonlinearities arise from the interaction of the light field with the discrete energy levels of atoms or molecules. The response is calculated using [perturbation theory](@entry_id:138766), typically within the [density matrix formalism](@entry_id:183082), which correctly accounts for both coherent evolution and relaxation processes.

Let's consider a generic three-level quantum system (e.g., an atom) with energy levels $E_1, E_2, E_3$. The transition frequencies are $\omega_{ij} = (E_i - E_j)/\hbar$. Suppose a laser field at frequency $\omega$ drives the system. A process like **[two-photon absorption](@entry_id:182758) (TPA)**, where the atom is excited from state $|1\rangle$ to $|3\rangle$ by absorbing two photons, is a third-order process described by $\chi^{(3)}$. Perturbation theory shows that the susceptibility for this process contains terms that depend on the energy denominators corresponding to the intermediate steps of the interaction.

For TPA in a cascade system where transitions $|1\rangle \leftrightarrow |2\rangle$ and $|2\rangle \leftrightarrow |3\rangle$ are allowed, the dominant contribution to the susceptibility near resonance ($2\omega \approx \omega_{31}$) has the form:

$$
\chi^{(3)} \propto \frac{\mu_{12}^2 \mu_{23}^2}{(\omega_{21} - \omega - i\gamma_{21}) (\omega_{31} - 2\omega - i\gamma_{31})}
$$

Here, $\mu_{ij}$ are the transition dipole matrix elements, and $\gamma_{ij}$ are the [dephasing](@entry_id:146545) rates (related to the inverse of the coherence time $T_2$) for the respective transitions. The term $(\omega_{21} - \omega - i\gamma_{21})$ represents the energy denominator for the first photon absorption to the *virtual* or real intermediate state $|2\rangle$. The term $(\omega_{31} - 2\omega - i\gamma_{31})$ corresponds to the completion of the two-photon transition to the final state $|3\rangle$.

The physical processes of [absorption and dispersion](@entry_id:159734) are encoded in the complex nature of the susceptibility. The energy absorbed by the medium is proportional to the imaginary part, $\text{Im}[\chi^{(n)}]$, while the nonlinear change in the refractive index is related to the real part, $\text{Re}[\chi^{(n)}]$. For the TPA process discussed, we can define a one-photon detuning $\Delta_1 = \omega_{21} - \omega$ and a two-photon [detuning](@entry_id:148084) $\Delta_2 = \omega_{31} - 2\omega$. The imaginary part of the susceptibility, which governs the TPA rate, then takes on a complex lineshape that depends on both detunings and decay rates [@problem_id:696546]:

$$
\text{Im}[\chi^{(3)}] \propto \frac{(\Delta_1^2 - \gamma_{21}^2)\gamma_{31} + 2\Delta_1\gamma_{21}\Delta_2}{(\Delta_1^2 + \gamma_{21}^2)^2 (\Delta_2^2 + \gamma_{31}^2)}
$$

This expression reveals rich physical phenomena, such as [electromagnetically induced transparency](@entry_id:164772) (EIT) and Autler-Townes splitting, which arise from quantum interference effects when multiple resonant pathways are involved. The [quantum formalism](@entry_id:197347) thus provides a complete and accurate framework for calculating the nonlinear susceptibilities, including their resonant behavior and [complex structure](@entry_id:269128).

### Symmetry Properties of Susceptibility Tensors

The [nonlinear susceptibility](@entry_id:136819) $\chi^{(n)}$ is a tensor of rank $(n+1)$. Its components, $\chi_{ijk...}^{(n)}$, relate the $i$-th component of the induced polarization to the product of the $j, k, \dots$ components of the electric fields. The values of these tensor elements are not arbitrary; they are profoundly constrained by symmetries, both intrinsic to the definition and extrinsic from the physical structure of the medium.

#### Intrinsic Permutation Symmetry

This fundamental symmetry arises from the indistinguishability of photons. For a process involving multiple fields at the same frequency, the order in which they are written in the [susceptibility tensor](@entry_id:189500) is immaterial. For example, in [second-harmonic generation](@entry_id:145639) (SHG), where two photons of frequency $\omega$ create one photon of frequency $2\omega$, the polarization is $P_i(2\omega) = \epsilon_0 \sum_{j,k} \chi_{ijk}^{(2)}(-2\omega; \omega, \omega) E_j(\omega) E_k(\omega)$. Since $E_j E_k = E_k E_j$, only the symmetric part of the tensor contributes. Thus, we must have $\chi_{ijk}^{(2)} = \chi_{ikj}^{(2)}$. This reduces the number of independent components of the $\chi^{(2)}$ tensor from $3^3=27$ to $18$. This property allows the use of the contracted **Voigt notation**, where pairs of indices $(jk)$ are mapped to a single index, simplifying the [tensor representation](@entry_id:180492).

#### Kleinman's Symmetry

A further, powerful simplification known as **Kleinman's symmetry** applies under specific conditions. If all interacting frequencies (including input and output) are far from any material resonances, the nonlinear process can be considered nearly instantaneous and lossless. In this limit, the [nonlinear polarization](@entry_id:272949) can be derived from an effective energy density function $U(\mathbf{E})$.

Consider the third-order contribution to this energy density, $U^{(3)} = -\frac{1}{3}\epsilon_0 \sum_{i,j,k} C_{ijk} E_i E_j E_k$, where $C_{ijk}$ is a constant tensor that can be assumed to be fully symmetric in all its indices. The polarization is then found by differentiating this energy with respect to the field: $P_i = - \partial U^{(3)} / \partial E_i$. This yields $P_i^{(2)} = \epsilon_0 \sum_{j,k} C_{ijk} E_j E_k$. Comparing this with the definition $P_i^{(2)} = \epsilon_0 \sum_{j,k} \chi^{(2)}_{ijk} E_j E_k$, we find that $\chi^{(2)}_{ijk} = C_{ijk}$. Since $C_{ijk}$ is fully symmetric, the [susceptibility tensor](@entry_id:189500) $\chi^{(2)}_{ijk}$ must also be symmetric with respect to any permutation of its indices ($i, j, k$) [@problem_id:696592]. This implies, for example, that $\chi_{ijk}^{(2)} = \chi_{jik}^{(2)} = \chi_{kji}^{(2)}$, etc. This symmetry drastically reduces the number of independent $\chi^{(2)}$ elements and provides useful relationships between coefficients for different nonlinear processes (e.g., relating the [electro-optic effect](@entry_id:270669) to SHG).

#### Spatial Symmetry of the Medium

The most restrictive and practically important symmetry constraints are imposed by the spatial symmetry of the optical medium itself. The [susceptibility tensor](@entry_id:189500) must remain invariant under all symmetry operations (rotations, reflections, inversion) of the material's [crystal point group](@entry_id:183880).

The most dramatic consequence is for materials possessing **inversion symmetry**. Such media are called **centrosymmetric**. Under the inversion operation, the position vector $\mathbf{r}$ transforms to $-\mathbf{r}$. As a [polar vector](@entry_id:184542), the electric field also inverts, $\mathbf{E} \to -\mathbf{E}$, and so must the polarization, $\mathbf{P} \to -\mathbf{P}$. Let's examine the polarization expansion:
$P_i \to -P_i$.
For the $\chi^{(2)}$ term, $\sum_{j,k} \chi_{ijk}^{(2)} E_j E_k \to \sum_{j,k} \chi_{ijk}^{(2)} (-E_j) (-E_k) = \sum_{j,k} \chi_{ijk}^{(2)} E_j E_k$.
For the relation $-P_i \propto \chi^{(2)} E^2$ to hold, we must have $\chi_{ijk}^{(2)} = -\chi_{ijk}^{(2)}$, which implies that all components of $\chi^{(2)}$ must be zero. By the same logic, all even-order susceptibilities ($\chi^{(4)}$, $\chi^{(6)}$, etc.) must vanish in the bulk of a centrosymmetric medium. This is a crucial selection rule: second-order nonlinear effects like SHG are forbidden in materials like glass, gases, and silicon (in its bulk crystal form). They can only occur in **non-centrosymmetric** crystals (e.g., KDP, LiNbO$_3$), or at surfaces and interfaces where inversion symmetry is broken.

Third-order effects, described by $\chi^{(3)}$, are permitted in all media, as the term $E^3$ transforms to $(-E)^3 = -E^3$, consistent with inversion symmetry. Even in highly symmetric crystals, the $\chi^{(3)}$ tensor is sparse. For a centrosymmetric cubic crystal (point group $O_h$), symmetry dictates that there are only three independent non-zero elements: $\chi_{xxxx}$, $\chi_{xxyy}$, and $\chi_{xyyx}$ (and their permutations like $\chi_{yyyy}$, $\chi_{zzxx}$, etc.). The relative values of these components determine the polarization dependence of $\chi^{(3)}$ effects. For example, in a [four-wave mixing](@entry_id:164327) experiment, the intensity of the generated signal depends critically on the polarization of the input beams. By measuring the signal for different polarization configurations, one can directly probe the ratios between these tensor elements [@problem_id:696512].

For [non-centrosymmetric crystals](@entry_id:162159), the surviving elements of $\chi^{(2)}$ depend on the specific point group. For a crystal of class D4 (422), symmetry reduces the tensor to only two independent elements, often denoted in Voigt notation as $d_{14}$ and $d_{36}$ (with the constraint $d_{25}=-d_{14}$). The efficiency of a nonlinear process like SHG then depends on the propagation direction and polarization of the light relative to the crystal axes. This is captured by the **effective nonlinear coefficient**, $d_{eff}$, which is a [scalar projection](@entry_id:148823) of the tensor onto the interacting field polarizations. For instance, in a D4 crystal, the process where two ordinary waves (o-waves) combine to form an [extraordinary wave](@entry_id:200108) (e-wave) has an effective coefficient $|d_{eff,ooe}| = |d_{36}\sin\theta\sin(2\phi)|$, while the process of two e-waves creating an o-wave has $|d_{eff,eeo}| = |d_{14}\sin(2\theta)|$. Optimizing the nonlinear conversion efficiency involves choosing the crystal orientation ($\theta, \phi$) to maximize $d_{eff}$ for the desired interaction, a technique known as [phase matching](@entry_id:161268) [@problem_id:696576].

### Macroscopic versus Microscopic Response: The Local Field

The macroscopic susceptibility $\chi^{(n)}$ describes the bulk response of a medium. It is fundamentally related to the nonlinear response of the individual atoms or molecules that constitute the medium. This microscopic response is characterized by the **molecular hyperpolarizabilities** ($\alpha$, $\beta$, $\gamma$, etc.) in the expansion of the induced [molecular dipole moment](@entry_id:152656), $p$, in terms of the *local* electric field, $E_{loc}$, experienced by the molecule:

$$
p = \alpha E_{loc} + \beta E_{loc}^2 + \gamma E_{loc}^3 + \dots
$$

The local field $E_{loc}$ is not the same as the macroscopic field $E$ that appears in Maxwell's equations. $E_{loc}$ is the field at the site of a single molecule, resulting from the superposition of the external field and the fields produced by all other polarized molecules in the medium. In a dense, isotropic medium, a common approximation for this field is the **Lorentz local field**:

$$
E_{loc} = E + \frac{P}{3 \epsilon_0}
$$

This relation shows that the local field is enhanced by the collective polarization of the medium. To find the connection between the macroscopic $\chi^{(3)}$ and the microscopic $\gamma$, we can use a self-consistent approach. The [macroscopic polarization](@entry_id:141855) is the density of molecular dipoles, $P=Np$. Substituting the expressions for $P$ and $E_{loc}$ and collecting terms of the same order in the macroscopic field $E$, one can establish a relationship between the coefficients. This procedure reveals that the macroscopic susceptibility is not simply the number density times the microscopic [hyperpolarizability](@entry_id:202797). For the third-order case, the relationship is [@problem_id:696665]:

$$
\chi^{(3)} = \frac{N \gamma}{\epsilon_0} \left( \frac{n^2+2}{3} \right)^4
$$

The factor $L = (n^2+2)/3$ is the Lorentz local-field factor, where $n$ is the linear refractive index of the medium. This result shows that the macroscopic nonlinear response is significantly modified by the dielectric environment, with the fourth power of the local-field factor indicating a strong dependence of $\chi^{(3)}$ effects on the linear optical properties of the host medium.

### Fundamental Relations and Consequences

The framework of nonlinear susceptibilities is governed by deep physical principles, including causality and energy conservation, which lead to universal relationships between different optical properties.

#### The Kramers-Kronig Relations

The principle of **causality**—that a response cannot precede its cause—imposes a strict mathematical relationship between the real and imaginary parts of any [linear response function](@entry_id:160418). These are the **Kramers-Kronig relations**. They state that the real part of the response at a given frequency can be determined by an integral of the imaginary part over all frequencies, and vice versa.

Remarkably, analogous relations exist for nonlinear susceptibilities. For the [third-order susceptibility](@entry_id:185586) $\chi^{(3)}(-\omega; \omega, \omega, -\omega)$, which describes intensity-dependent effects, its real part determines the [nonlinear refractive index](@entry_id:175662) ($n_2$), and its imaginary part determines the two-photon [absorption coefficient](@entry_id:156541) ($\beta$). A Kramers-Kronig-like relation connects these two quantities [@problem_id:696596]:

$$
n_2(\omega) = \frac{c}{\pi} \mathcal{P} \int_0^{\infty} \frac{\beta(\omega')}{(\omega')^2 - \omega^2} d\omega'
$$

where $\mathcal{P}$ denotes the Cauchy [principal value](@entry_id:192761). This relationship is profound: it implies that if a material exhibits [two-photon absorption](@entry_id:182758) at any frequency, it must also have a [nonlinear refractive index](@entry_id:175662) across the entire spectrum. One cannot exist without the other. For example, by measuring the TPA spectrum $\beta(\omega')$ of a semiconductor, one can use this integral to predict its [nonlinear refractive index](@entry_id:175662) $n_2$ at a different frequency, a critical parameter for applications in [all-optical switching](@entry_id:195336) and laser systems.

#### The Manley-Rowe Relations

The **Manley-Rowe relations** are a direct consequence of energy conservation in a lossless nonlinear medium. In a quantum picture, a [three-wave mixing](@entry_id:196165) process like [sum-frequency generation](@entry_id:168681) ($\omega_3 = \omega_1 + \omega_2$) corresponds to the [annihilation](@entry_id:159364) of one photon at $\omega_1$ and one at $\omega_2$ for every photon created at $\omega_3$. This conservation of photon number flux leads to a simple relationship between the rates of change of the intensities of the interacting beams.

From the coupled-wave equations that describe the evolution of the field amplitudes $A_j(z)$ in a lossless medium, one can derive the change in intensity $I_j \propto n_j |A_j|^2$ along the propagation direction $z$. For a sum-frequency process, it can be shown that [@problem_id:696552]:

$$
\frac{1}{\omega_1} \frac{dI_1}{dz} = \frac{1}{\omega_2} \frac{dI_2}{dz} = -\frac{1}{\omega_3} \frac{dI_3}{dz}
$$

The quantity $I_j/\omega_j$ is proportional to the [photon flux](@entry_id:164816) (number of photons per unit area per unit time) in the $j$-th beam. The relations state that the rate at which photons are removed from the beams at $\omega_1$ and $\omega_2$ is exactly equal to the rate at which they are added to the beam at $\omega_3$. These relations are general for any parametric process in a lossless medium and provide a powerful tool for analyzing power flow and conversion efficiency.

### Advanced Topics in Nonlinear Response

The standard description of nonlinear susceptibilities can be extended to include more complex phenomena that go beyond the simple [power series expansion](@entry_id:273325) in the [local electric field](@entry_id:194304).

#### Cascaded Nonlinearities

While $\chi^{(2)}$ processes are forbidden in centrosymmetric media, it is possible for a sequence of second-order effects in a [non-centrosymmetric crystal](@entry_id:158606) to mimic a third-order response. This is known as a **cascaded nonlinearity**.

A prominent example involves optical [rectification](@entry_id:197363) followed by the linear electro-optic (Pockels) effect. An intense optical field at frequency $\omega$ can generate a DC polarization through optical [rectification](@entry_id:197363), a $\chi^{(2)}(0; \omega, -\omega)$ process. This polarization creates an internal static electric field $E(0)$ in the crystal. This DC field then modulates the refractive index experienced by the original optical wave via the Pockels effect, which is described by $\chi^{(2)}(\omega; \omega, 0)$. The result is an additional [nonlinear polarization](@entry_id:272949) at frequency $\omega$ that is proportional to $|E(\omega)|^2 E(\omega)$, exactly the form of a $\chi^{(3)}$ process.

By combining the equations for these two steps, one can derive an effective [third-order susceptibility](@entry_id:185586). For an optical field polarized along the z-axis of a crystal, the effective susceptibility is given by [@problem_id:696640]:

$$
\chi_{zzzz, eff}^{(3)} = -\frac{2}{3} \frac{[\chi_{zzz}^{(2)}]^2}{\epsilon_{zr}(0)} = -\frac{2}{3} \frac{n_z^8(\omega) r_{zzz}^2}{\epsilon_{zr}(0)}
$$

where we have used Kleinman symmetry and the relation between $\chi^{(2)}$ and the Pockels coefficient $r_{zzz}$. This cascaded susceptibility can be very large, sometimes exceeding the intrinsic electronic $\chi^{(3)}$ of a material, and can be engineered by choosing materials with large $\chi^{(2)}$ and by controlling [phase matching](@entry_id:161268).

#### Spatial Nonlocality and Wavevector Dependence

The entire framework presented thus far operates under the **[electric dipole approximation](@entry_id:150449)**, which assumes the material response is local. That is, the polarization at a point $\mathbf{r}$ depends only on the electric field at that same point, $\mathbf{P}(\mathbf{r}, t) = f(\mathbf{E}(\mathbf{r}, t))$. This approximation holds when the wavelength of light is much larger than the characteristic scale of the material's response (e.g., molecular size or [lattice constant](@entry_id:158935)).

When this condition is not met, or for a more complete description, one must consider **spatial nonlocality**. The polarization at $\mathbf{r}$ then depends on the electric fields in a neighborhood around $\mathbf{r}$. In the frequency domain, this spatial nonlocality manifests as a dependence of the [susceptibility tensor](@entry_id:189500) on the wavevectors of the interacting fields: $\chi^{(n)}(\omega_1, \mathbf{k}_1; \omega_2, \mathbf{k}_2; \dots)$.

This wavevector dependence can be treated perturbatively by expanding the susceptibility in powers of $\mathbf{k}$. The zeroth-order term is the standard, local electric-dipole susceptibility. The [first-order correction](@entry_id:155896), linear in $k$, arises from the first spatial moment of the nonlocal response kernel. This correction term introduces contributions from [magnetic dipole](@entry_id:275765) and [electric quadrupole](@entry_id:262852) interactions, which are typically much weaker than the electric dipole term but can become significant or give rise to new nonlinear phenomena, especially at interfaces or in chiral media. The leading-order nonlocal correction to the [third-order susceptibility](@entry_id:185586) can be expressed as a [linear combination](@entry_id:155091) of the [wavevector](@entry_id:178620) components [@problem_id:696669]:

$$
\Delta\chi_{ijkl}^{(3)}(\mathbf{k}_1, \mathbf{k}_2, \mathbf{k}_3) = -i \sum_{a=1}^3 \sum_{m=x,y,z} k_{a,m} \Gamma_{ijklm}^{(a)}
$$

where $\Gamma_{ijklm}^{(a)}$ are tensors representing the first spatial moments of the nonlocal response function. This extension of the susceptibility concept provides a bridge to understanding phenomena like nonlinear [optical activity](@entry_id:139326) and SHG from isotropic surfaces, completing our systematic exploration of the principles and mechanisms governing nonlinear optical susceptibilities.