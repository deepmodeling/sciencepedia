## Introduction
The unification of the electromagnetic and weak forces into a single [electroweak theory](@entry_id:137910) represents a monumental achievement of modern particle physics and a cornerstone of the Standard Model. However, this elegant unification initially presented a significant puzzle: its underlying SU(2)L x U(1)Y [gauge symmetry](@entry_id:136438) required massless [force carriers](@entry_id:161434), in stark contrast to the experimentally observed massive W and Z bosons. This article explores the resolution to this conflict through the mechanism of [spontaneous symmetry breaking](@entry_id:140964). We will first dissect the core theoretical framework in **Principles and Mechanisms**, examining how the Higgs field generates mass, the resulting phenomenological relations, and the constraints of unitarity. Next, in **Applications and Interdisciplinary Connections**, we will witness the theory's predictive power through its applications in particle phenomenology, [nuclear physics](@entry_id:136661), and cosmology. Finally, **Hands-On Practices** will offer the opportunity to engage directly with key calculations. Our journey begins with the fundamental principles that govern this profound description of nature.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms of the Electroweak Theory as described by the Standard Model. We will dissect the process of [electroweak symmetry breaking](@entry_id:161363), explore the generation of particle masses, and examine the profound theoretical consequences and constraints that arise from this framework, including its high-energy behavior and its sensitivity to quantum corrections.

### The Higgs Mechanism and Mass Generation for Gauge Bosons

The unification of the electromagnetic and weak forces is described by a [gauge theory](@entry_id:142992) based on the [symmetry group](@entry_id:138562) $SU(2)_L \times U(1)_Y$. This theory initially posits four massless [gauge bosons](@entry_id:200257): a triplet $W^a_\mu$ for the [weak isospin](@entry_id:158166) group $SU(2)_L$ and a singlet $B_\mu$ for the [weak hypercharge](@entry_id:149263) group $U(1)_Y$. However, experimental evidence clearly indicates that the mediators of the [weak force](@entry_id:158114), the $W^\pm$ and $Z$ bosons, are massive. The mechanism responsible for breaking the [electroweak symmetry](@entry_id:149377) and generating these masses, while leaving the photon of electromagnetism massless, is known as the **Higgs mechanism**.

This mechanism introduces a [complex scalar field](@entry_id:159799), the Higgs field $\Phi$, which is a doublet under $SU(2)_L$ and carries a [weak hypercharge](@entry_id:149263) $Y=1/2$. The dynamics of this field are governed by the Lagrangian, which includes a kinetic term and a potential:
$$
\mathcal{L}_{\text{Higgs}} = (D_\mu \Phi)^\dagger (D^\mu \Phi) - V(\Phi)
$$
The [covariant derivative](@entry_id:152476) $D_\mu$ couples the Higgs field to the [gauge bosons](@entry_id:200257):
$$
D_\mu = \partial_\mu + i g \frac{\tau^a}{2} W_\mu^a + i g' \frac{1}{2} B_\mu
$$
Here, $g$ and $g'$ are the [coupling constants](@entry_id:747980) for $SU(2)_L$ and $U(1)_Y$ respectively, and $\tau^a$ are the Pauli matrices. The Higgs potential is given by:
$$
V(\Phi) = \mu^2 (\Phi^\dagger \Phi) + \lambda (\Phi^\dagger \Phi)^2
$$
For [electroweak symmetry breaking](@entry_id:161363) to occur, the parameter $\mu^2$ must be negative. This gives the potential a "Mexican hat" shape, and the ground state of the theory is not at $\Phi=0$ but rather in a minimum where the field acquires a non-zero **[vacuum expectation value](@entry_id:146340) (VEV)**, denoted by $v$. The magnitude of the VEV is given by $|\langle \Phi \rangle|^2 = -\frac{\mu^2}{2\lambda} \equiv \frac{v^2}{2}$. We can choose a specific direction in the internal space for this vacuum, for instance:
$$
\langle \Phi \rangle = \Phi_0 = \frac{1}{\sqrt{2}} \begin{pmatrix} 0 \\ v \end{pmatrix}
$$
This non-zero VEV spontaneously breaks the $SU(2)_L \times U(1)_Y$ symmetry. The remaining unbroken symmetry corresponds to a generator that leaves the vacuum state invariant. A [linear combination](@entry_id:155091) of the $SU(2)_L$ generator $T^3$ and the $U(1)_Y$ generator $Y$ annihilates the vacuum, defining the electric charge operator $Q = T^3 + Y/2$. This leaves an unbroken $U(1)_{em}$ symmetry, which is identified with electromagnetism.

The mass terms for the [gauge bosons](@entry_id:200257) arise from the Higgs kinetic term, $(D_\mu \Phi)^\dagger (D^\mu \Phi)$, when we expand the Higgs field around its VEV. Substituting $\Phi_0$ into the kinetic term gives:
$$
\mathcal{L}_{\text{mass}} = (D_\mu \Phi_0)^\dagger (D^\mu \Phi_0) = \left| \left( i g \frac{\tau^a}{2} W_\mu^a + i g' \frac{1}{2} B_\mu \right) \Phi_0 \right|^2
$$
Let's evaluate the action of the derivative on the VEV:
$$
D_\mu \Phi_0 = \frac{iv}{2\sqrt{2}} \left( g(W_\mu^1\tau^1 + W_\mu^2\tau^2 + W_\mu^3\tau^3) + g'B_\mu \mathbb{I}_2 \right) \begin{pmatrix} 0 \\ 1 \end{pmatrix} = \frac{iv}{2\sqrt{2}} \begin{pmatrix} g(W_\mu^1 - iW_\mu^2) \\ -gW_\mu^3 + g'B_\mu \end{pmatrix}
$$
The Lagrangian term becomes:
$$
\mathcal{L}_{\text{mass}} = \frac{v^2}{8} \left| g(W_\mu^1 - iW_\mu^2) \right|^2 + \frac{v^2}{8} (gW_\mu^3 - g'B_\mu)^2
$$
By defining the charged vector boson fields as $W_\mu^\pm = \frac{1}{\sqrt{2}}(W_\mu^1 \mp iW_\mu^2)$, the first term can be rewritten as:
$$
\frac{g^2 v^2}{4} W_\mu^+ W^{-\mu} = M_W^2 W_\mu^+ W^{-\mu}
$$
This reveals the mass of the charged $W$ bosons: $M_W = \frac{gv}{2}$.

The second term involves a mixture of the neutral [gauge fields](@entry_id:159627) $W_\mu^3$ and $B_\mu$. It can be written in a matrix form as:
$$
\mathcal{L}_{\text{mass, neutral}} = \frac{1}{2} \begin{pmatrix} W^3_\mu  & B_\mu \end{pmatrix} \mathcal{M}^2 \begin{pmatrix} W^{3\mu} \\ B^\mu \end{pmatrix} \quad \text{with} \quad \mathcal{M}^2 = \frac{v^2}{4} \begin{pmatrix} g^2  & -gg' \\ -gg' & g'^2 \end{pmatrix}
$$
To find the physical mass [eigenstates](@entry_id:149904), we must diagonalize this mass-squared matrix $\mathcal{M}^2$ [@problem_id:206652]. The eigenvalues $\lambda$ are found by solving the characteristic equation $\det(\mathcal{M}^2 - \lambda \mathbb{I}) = 0$.
$$
\left(\frac{v^2 g^2}{4} - \lambda\right)\left(\frac{v^2 g'^2}{4} - \lambda\right) - \left(-\frac{v^2 gg'}{4}\right)^2 = 0
$$
Expanding this equation gives $\lambda \left( \lambda - \frac{v^2}{4}(g^2 + g'^2) \right) = 0$.
The two eigenvalues are:
$$
\lambda_1 = 0 \quad \text{and} \quad \lambda_2 = \frac{v^2}{4}(g^2 + g'^2)
$$
The zero-mass eigenvalue corresponds to a physical massless [gauge boson](@entry_id:274088), which we identify as the **photon ($A_\mu$)**. The non-zero eigenvalue corresponds to the squared mass of the massive neutral [gauge boson](@entry_id:274088), the **Z boson**.
$$
M_Z^2 = \frac{v^2}{4}(g^2 + g'^2)
$$
The corresponding eigenvectors define the physical fields as linear combinations of the interaction [eigenstates](@entry_id:149904) $W_\mu^3$ and $B_\mu$. This mixing is parameterized by the **[weak mixing angle](@entry_id:158886)**, $\theta_W$, defined by:
$$
\cos\theta_W = \frac{g}{\sqrt{g^2+g'^2}} \quad \text{and} \quad \sin\theta_W = \frac{g'}{\sqrt{g^2+g'^2}}
$$
The mass [eigenstates](@entry_id:149904) are then:
$$
A_\mu = \sin\theta_W W_\mu^3 + \cos\theta_W B_\mu \quad (\text{Photon, massless})
$$
$$
Z_\mu = \cos\theta_W W_\mu^3 - \sin\theta_W B_\mu \quad (Z \text{ boson, mass } M_Z)
$$

### Phenomenological Relations and Probes of New Physics

The structure of the Higgs mechanism leads to tight correlations among the electroweak parameters, providing precise predictions that have been spectacularly confirmed by experiment. Deviations from these predictions would be a clear signal of new physics.

#### The $\rho$ Parameter and Custodial Symmetry

One of the most important predictions of the Standard Model's electroweak sector is the relationship between the $W$ and $Z$ boson masses. Using the definitions of $M_W$ and $M_Z$ derived above, along with the [weak mixing angle](@entry_id:158886), we find:
$$
M_W^2 = \frac{g^2 v^2}{4} \quad \text{and} \quad M_Z^2 = \frac{(g^2+g'^2)v^2}{4} = \frac{g^2 v^2}{4\cos^2\theta_W} = \frac{M_W^2}{\cos^2\theta_W}
$$
This relationship is usually quantified by the **$\rho$ parameter**, defined as:
$$
\rho \equiv \frac{M_W^2}{M_Z^2 \cos^2\theta_W}
$$
At tree level in the Standard Model, the theory predicts $\rho = 1$. This result is not accidental; it is a direct consequence of the [isospin](@entry_id:156514) structure of the Higgs field. The Higgs potential $V(\Phi^\dagger\Phi)$ possesses a global $SU(2)_L \times SU(2)_R$ symmetry, larger than the gauged $SU(2)_L \times U(1)_Y$, which is known as **[custodial symmetry](@entry_id:156356)**. This symmetry is broken to the diagonal subgroup $SU(2)_V$ by the VEV, which protects the ratio of the $W$ and $Z$ masses. The hypercharge coupling $g'$ explicitly breaks this symmetry, and the mass splitting between the $Z$ and $W$ bosons is directly attributable to this breaking [@problem_id:206621]. We can see this explicitly by computing the mass-squared difference:
$$
M_Z^2 - M_W^2 = \frac{v^2}{4}(g^2+g'^2) - \frac{v^2 g^2}{4} = \frac{v^2}{4}(g')^2
$$
This shows that if the [hypercharge](@entry_id:186657) coupling were zero ($g'=0$), the $Z$ and $W$ bosons would be degenerate in mass (as components of an $SU(2)$ triplet), and the [custodial symmetry](@entry_id:156356) would be exact in the gauge sector as well.

The experimental value of $\rho$ is very close to 1, strongly supporting the hypothesis that [electroweak symmetry](@entry_id:149377) is broken by a mechanism that is (at least approximately) custodially symmetric, such as the condensation of an $SU(2)$ doublet. If the Higgs sector were more complex, for instance, involving scalar fields in higher representations of $SU(2)_L$, the tree-level $\rho$ parameter would deviate from unity. Consider a model extended with a real scalar triplet $\vec{\phi}$ with [isospin](@entry_id:156514) $I=1$ and [hypercharge](@entry_id:186657) $Y=0$, which acquires a VEV $\langle\vec{\phi}\rangle = (0, 0, v_t)^T$ in addition to the doublet VEV $v_d$ [@problem_id:206687]. In such a model, the [gauge boson](@entry_id:274088) masses are modified:
$$
M_W^2 = \frac{g^2}{4}(v_d^2 + 4v_t^2) \quad \text{and} \quad M_Z^2 = \frac{g^2+g'^2}{4}v_d^2
$$
The contribution to the $W$ mass from the triplet is larger than to the $Z$ mass because the charged components of the triplet VEV contribute to $M_W$ but not $M_Z$. The $\rho$ parameter becomes:
$$
\rho = \frac{M_W^2}{M_Z^2\cos^2\theta_W} = \frac{g^2(v_d^2 + 4v_t^2)/4}{(g^2+g'^2)v_d^2/4} \frac{g^2+g'^2}{g^2} = \frac{v_d^2 + 4v_t^2}{v_d^2} = 1 + 4\frac{v_t^2}{v_d^2}
$$
The presence of a triplet VEV thus leads to $\rho > 1$. Precise measurements of $\rho$ therefore provide stringent constraints on extensions of the Standard Model Higgs sector.

#### The Higgs Boson and Scalar Sector Interactions

Beyond giving mass to the gauge bosons, the Higgs mechanism predicts the existence of a physical scalar particle: the **Higgs boson ($H$)**. This particle corresponds to the radial excitation of the Higgs field around its VEV. The mass of the Higgs boson is determined by the quartic coupling in the potential: $M_H^2 = 2\lambda v^2$.

The Higgs potential also dictates the self-interactions of the scalar sector. When the Higgs field is parameterized in terms of the physical Higgs $H$ and the Goldstone bosons $\pi_a$ (which become the [longitudinal modes](@entry_id:164178) of the $W^\pm$ and $Z$), the potential contains interaction vertices. For instance, the interaction between one Higgs boson and two Goldstone bosons is of the form $g_{h\pi\pi} H (\vec{\pi} \cdot \vec{\pi})$. Expanding the potential $V = \lambda(\Phi^\dagger\Phi - v^2/2)^2 = \frac{\lambda}{4}(H^2+2vH+\vec{\pi}^2)^2$ to find this coupling [@problem_id:206680], we isolate the term linear in $H$ and quadratic in $\vec{\pi}$ from the cross-term $2(2vH)(\vec{\pi}^2)$:
$$
V \supset \frac{\lambda}{4} [2(2vH)(\vec{\pi}^2)] = \lambda v H \vec{\pi}^2
$$
From this, we identify the coupling constant $g_{h\pi\pi} = \lambda v$. Using the relations for the Higgs mass and VEV, we can express this coupling in terms of [physical observables](@entry_id:154692):
$$
g_{h\pi\pi} = \lambda v = \left( \frac{M_H^2}{2v^2} \right) v = \frac{M_H^2}{2v}
$$
This coupling, and others derived from the [scalar potential](@entry_id:276177), are crucial for understanding the high-energy behavior of the theory.

### High-Energy Behavior and Unitarity Constraints

One of the most compelling theoretical arguments for the existence of the Higgs boson comes from the study of scattering processes involving longitudinally polarized $W$ and $Z$ bosons at high energies.

#### The Goldstone Boson Equivalence Theorem

A powerful tool for analyzing such processes is the **Goldstone Boson Equivalence Theorem (GBET)**. It states that at energies much larger than the vector boson masses ($E \gg M_W, M_Z$), the scattering amplitude for a process involving longitudinally polarized vector bosons is equal to the amplitude of the corresponding process where each longitudinal boson is replaced by its associated Goldstone boson.
$$
\mathcal{M}(\dots V_L \dots) \approx \mathcal{M}(\dots \phi \dots) \quad \text{for } E \gg M_V
$$
This theorem simplifies calculations enormously, as it allows us to compute amplitudes using [scalar field theory](@entry_id:151692), which is much simpler than dealing with polarized vector bosons.

As a direct application, consider the decay of a heavy Higgs boson into two longitudinally polarized $W$ bosons, $H \to W_L^+ W_L^-$ [@problem_id:206635]. Using the GBET, we can calculate the width for the decay $H \to w^+ w^-$. The amplitude for this process is simply the coupling constant $g_{Hw^+w^-} = 2\lambda v$. The [two-body decay](@entry_id:272664) width in the limit $M_H \gg M_W$ is given by:
$$
\Gamma(H \to w^+ w^-) = \frac{|\mathcal{M}|^2}{16\pi M_H} = \frac{(2\lambda v)^2}{16\pi M_H} = \frac{\lambda^2 v^2}{4\pi M_H}
$$
Expressing $\lambda$ and $v$ in terms of $M_H$, $M_W$ and $g$ ($\lambda = M_H^2/(2v^2)$, $v^2=4M_W^2/g^2$), we arrive at the [partial width](@entry_id:156471):
$$
\Gamma(H \to W_L^+ W_L^-) \approx \Gamma(H \to w^+ w^-) = \frac{1}{4\pi M_H} \left(\frac{M_H^2}{2v^2}\right)^2 v^2 = \frac{M_H^3}{16\pi v^2} = \frac{g^2 M_H^3}{64\pi M_W^2}
$$
This result demonstrates a key feature of the Higgs boson: its decay width into vector bosons grows as the cube of its mass, indicating that a very heavy Higgs would be a very broad resonance.

#### Unitarity and the Higgs Mass Bound

The GBET also reveals the crucial role of the Higgs boson in ensuring the consistency of the theory at high energies. Without a Higgs boson, the [scattering amplitudes](@entry_id:155369) for longitudinal vector bosons grow with energy, eventually violating the principle of **unitarity**, which requires that probabilities do not exceed 1.

Let's examine the process $W_L^+ W_L^- \to Z_L Z_L$ [@problem_id:206640]. By the GBET, this is equivalent to $w^+ w^- \to z z$ at high energies. The tree-level amplitude for this scalar scattering process receives contributions from a four-point contact vertex and from an [s-channel](@entry_id:159725) exchange of a Higgs boson. The total amplitude is found to be:
$$
\mathcal{M}(s) = \mathcal{M}_{\text{contact}} + \mathcal{M}_{H\text{-exchange}} = -2\lambda - \frac{(2\lambda v)^2}{s - M_H^2}
$$
Using $M_H^2 = 2\lambda v^2$, this simplifies dramatically:
$$
\mathcal{M}(s) = -2\lambda \left( 1 + \frac{2\lambda v^2}{s - M_H^2} \right) = -2\lambda \left( 1 + \frac{M_H^2}{s - M_H^2} \right) = -\frac{2\lambda s}{s - M_H^2} = -\frac{M_H^2}{v^2} \frac{s}{s - M_H^2}
$$
In a theory without a Higgs boson, only the [gauge boson](@entry_id:274088) self-interactions (corresponding to the contact term) would exist. The amplitude would grow with energy, leading to a violation of unitarity. The Higgs exchange term, however, precisely cancels this bad high-energy behavior. In the high-energy limit ($s \to \infty$), the amplitude approaches a constant value:
$$
\lim_{s \to \infty} \mathcal{M}(s) = -\frac{M_H^2}{v^2}
$$
Unitarity imposes a bound on the partial wave amplitudes, $a_J$. For the s-wave ($J=0$), the condition is $|\text{Re } a_0| \le 1/2$. Since our amplitude is constant at high energy, it only contributes to the s-wave, with $a_0 = \mathcal{M}/(16\pi)$. Applying the unitarity bound gives:
$$
\left| \frac{-M_H^2}{16\pi v^2} \right| \le \frac{1}{2} \implies M_H^2 \le 8\pi v^2
$$
This implies an upper bound on the Higgs mass: $M_H \le \sqrt{8\pi}v \approx 1$ TeV. This powerful argument, made long before the Higgs discovery, demonstrated that if the [electroweak symmetry](@entry_id:149377) is broken by a scalar field, that field must be relatively light to maintain the consistency of the theory.

### Quantum Corrections and the Theoretical Structure

The quantum structure of the [electroweak theory](@entry_id:137910) reveals further profound principles and challenges. Physical predictions must be independent of the unphysical artifacts of quantization, and the parameters of the theory themselves evolve with energy.

#### Gauge Invariance in Quantum Calculations

Quantizing a [gauge theory](@entry_id:142992) often requires fixing a gauge, which can introduce unphysical degrees of freedom and gauge-dependent parameters into intermediate calculations. A fundamental consistency requirement is that all final [physical observables](@entry_id:154692), such as [scattering amplitudes](@entry_id:155369) and decay rates, must be independent of the choice of gauge. This principle of **[gauge invariance](@entry_id:137857)** is maintained in the Standard Model through intricate cancellations.

A clear demonstration of this principle can be seen in calculations performed in a family of covariant gauges known as **$R_\xi$ gauges** [@problem_id:206657]. In these gauges, the vector boson [propagator](@entry_id:139558) contains a gauge-dependent parameter $\xi$. The unphysical Goldstone bosons also propagate, with a mass that depends on $\xi$. A physical amplitude is only obtained when all contributions, including those from Goldstone boson exchange, are summed.

Consider the charged-current scattering process $e^-(p_1) + \nu_e(p_2) \to e^-(p_3) + \nu_e(p_4)$. The [t-channel](@entry_id:161717) amplitude involves the exchange of a $W$ boson and its corresponding Goldstone boson, $G$. The part of the $W$ propagator that depends on the gauge parameter $\xi_W$ is proportional to $(1-\xi_W) q_\mu q_\nu / (q^2 - \xi_W M_W^2)$. When the momentum vectors $q_\mu$ and $q_\nu$ are contracted into the fermion currents, use of the Dirac equation relates them to the [fermion masses](@entry_id:155586). It turns out that this gauge-dependent contribution from the $W$ exchange is exactly cancelled by the contribution from the $G$ exchange diagram. The sum of the two amplitudes is completely independent of $\xi_W$. This explicit cancellation showcases the role of the Goldstone bosons as essential components of the quantized theory, acting as "sentinels" that enforce [gauge invariance](@entry_id:137857).

#### The Running of Couplings

The coupling constants of the Standard Model are not true constants; their values change with the energy scale at which they are measured. This evolution is described by the **Renormalization Group Equations (RGEs)**, governed by beta functions. At one-loop order, the beta function for a gauge coupling $g$ takes the form $\beta(g) = b g^3 / (16\pi^2)$, where the coefficient $b$ depends on the particle content of the theory.

For the $U(1)_Y$ [hypercharge](@entry_id:186657) coupling $g'$, the coefficient $b_1$ is given by $b_1 = \frac{2}{3} \sum_f d_f Y_f^2 + \frac{1}{3} \sum_s d_s Y_s^2$, where the sum is over all fermions $f$ and complex scalars $s$, with $d_i$ being their degrees of freedom and $Y_i$ their hypercharge. Summing the contributions from all three generations of Standard Model fermions and the Higgs doublet gives the coefficient $b_1 = 41/6$ [@problem_id:206682]. The [beta function](@entry_id:143759) is therefore:
$$
\beta(g') = \frac{41 g'^3}{6 (16\pi^2)}
$$
Similarly, Yukawa couplings also run with energy. The top quark Yukawa coupling $y_t$ is particularly important due to its large size. Its one-loop [beta function](@entry_id:143759), neglecting other Yukawa couplings, is [@problem_id:206639]:
$$
\beta(y_t) = \frac{y_t}{16\pi^2} \left( \frac{9}{2}y_t^2 - 8g_3^2 - \frac{9}{4}g_2^2 - \frac{17}{12}g_1^2 \right)
$$
The positive term from the Yukawa [self-interaction](@entry_id:201333) tends to increase the coupling at higher energies, while the negative terms from the gauge interactions tend to decrease it. The balance of these effects determines the high-energy behavior of $y_t$ and has critical implications for the stability of the electroweak vacuum.

#### The Hierarchy Problem and the Veltman Condition

While the Higgs mechanism elegantly solves the problem of [electroweak symmetry breaking](@entry_id:161363), it introduces a new theoretical puzzle known as the **[hierarchy problem](@entry_id:148573)**. In quantum [field theory](@entry_id:155241), the mass of a fundamental scalar particle receives quantum corrections that are quadratically sensitive to the highest energy scale ($\Lambda$) up to which the theory is valid. This implies that if the Standard Model were valid up to the Planck scale ($\sim 10^{19}$ GeV), the Higgs mass would receive enormous corrections, requiring an extreme fine-tuning of the bare Higgs mass parameter to obtain the observed value of $125$ GeV.

The total one-loop quadratically divergent correction to the Higgs mass-squared can be expressed in terms of the particle masses of the theory. A cancellation of this leading divergence occurs if the masses satisfy a specific relation, known as the **Veltman condition** [@problem_id:206672]. This condition arises from demanding that the coefficient of the $\Lambda^2$ divergence vanishes. The coefficient is proportional to the [supertrace](@entry_id:183947) of the second derivative of the field-dependent mass-squared matrix, evaluated at zero Higgs field fluctuation:
$$
\delta M_H^2 \propto \Lambda^2 \sum_i (-1)^{2s_i} N_i \frac{d^2 M_i^2(H)}{dH^2}\bigg|_{H=0} = 0
$$
where $s_i$ is the spin and $N_i$ are the degrees of freedom for particle $i$. The contributions come from the Higgs itself (boson, $s=0$), the $W$ and $Z$ bosons (bosons, $s=1$), and the top quark (fermion, $s=1/2$, contributing with a minus sign). Evaluating the derivatives and summing the contributions from the Higgs ($N_H=1$), $W^\pm$ ($N_W=6$), $Z$ ($N_Z=3$), and top quark ($N_t=2N_c=6$, for $N_c=3$ colors) yields the condition:
$$
3M_H^2 + 6M_W^2 + 3M_Z^2 - 12M_t^2 = 0
$$
$$
M_H^2 + 2M_W^2 + M_Z^2 = 4M_t^2
$$
Plugging in the observed masses of the particles reveals that this condition is not satisfied in nature. The large contribution from the top quark is not cancelled by the boson contributions. The failure of this accidental cancellation to occur highlights the severity of the [hierarchy problem](@entry_id:148573). It suggests that the Standard Model is likely an effective theory and that new physics, such as [supersymmetry](@entry_id:155777) (where every boson has a fermion partner, leading to systematic cancellations) or composite Higgs models, must exist at the TeV scale to stabilize the Higgs mass.