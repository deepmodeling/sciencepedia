## Introduction
The discovery of the Higgs boson was a landmark achievement, completing the particle content of the Standard Model and confirming a theoretical framework conceived decades earlier. At its heart, Higgs physics addresses a fundamental puzzle: why do the force-carrying $W$ and $Z$ bosons, as well as fundamental fermions, have mass, when the underlying [electroweak symmetry](@entry_id:149377) of nature forbids it? This article provides a comprehensive exploration of the Higgs mechanism, the elegant solution to this problem, and its profound consequences for our understanding of the universe.

This exploration is divided into three parts. The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork, explaining the necessity of a new mechanism to preserve [unitarity](@entry_id:138773), detailing the process of spontaneous symmetry breaking, and deriving how the Higgs field generates mass for the particles of the Standard Model. The second chapter, **Applications and Interdisciplinary Connections**, will shift focus to the phenomenological world, examining how the Higgs boson is studied at colliders, used as a probe for new physics, and connected to grand cosmological questions like inflation and the [fate of the universe](@entry_id:159375). Finally, the **Hands-On Practices** section provides concrete problems to solidify your understanding of these core concepts. We begin by delving into the theoretical principles that make the Higgs boson an indispensable component of modern physics.

## Principles and Mechanisms

The introduction of the Higgs boson and its associated mechanism represents a paradigm shift in our understanding of fundamental particle physics. It provides a coherent and testable explanation for the [origin of mass](@entry_id:161752) for the electroweak [gauge bosons](@entry_id:200257) and fundamental fermions, phenomena that are strictly forbidden by the underlying $SU(2)_L \times U(1)_Y$ [gauge symmetry](@entry_id:136438) of the Standard Model (SM). This chapter will elucidate the core principles of the Higgs mechanism, beginning with the theoretical motivations, proceeding through the mechanics of [spontaneous symmetry breaking](@entry_id:140964), and culminating in an exploration of its subtle but profound consequences for precision physics and the ultimate stability of our universe.

### The Theoretical Imperative for a New Mechanism

At its core, the [electroweak theory](@entry_id:137910) is a [gauge theory](@entry_id:142992), a class of theories whose profound success in describing forces is built upon the principle of [local gauge invariance](@entry_id:154219). A direct consequence of this principle is that the force-carrying gauge bosons must be massless. While this holds true for the photon of quantum electrodynamics, it is in stark contradiction with the experimental observation of the massive $W^\pm$ and $Z$ bosons, which mediate the [weak force](@entry_id:158114). Simply adding mass terms for these bosons by hand into the Lagrangian would explicitly break the underlying [gauge symmetry](@entry_id:136438), rendering the theory non-renormalizable and thus devoid of predictive power at high energies.

A more subtle but equally profound issue arises when we consider the high-energy behavior of massive vector bosons. The scattering of longitudinally polarized $W$ bosons, for instance, presents a significant theoretical challenge. The **Goldstone Boson Equivalence Theorem** provides a powerful insight into this problem. It states that at center-of-mass energies $\sqrt{s}$ much greater than the vector boson mass $m_W$, the [scattering amplitude](@entry_id:146099) for a process involving longitudinally polarized vector bosons ($W_L, Z_L$) becomes equivalent to the amplitude for the corresponding would-be Goldstone bosons ($w, z$) that were "eaten" to give the bosons mass.

Let us consider the scattering process $W^+_L W^-_L \to Z_L Z_L$ in a hypothetical version of the Standard Model without a Higgs boson. Using the equivalence theorem, we can analyze the corresponding Goldstone boson process, $\pi^+ \pi^- \to \pi^0 \pi^0$. In a low-energy effective theory, the interaction among these Goldstone bosons leads to a [scattering amplitude](@entry_id:146099) $\mathcal{M}$ that grows with energy. For this specific process, the amplitude is found to be $\mathcal{M} = s/v^2$, where $v$ is the electroweak [vacuum expectation value](@entry_id:146340) (approximately $246$ GeV) and $s$ is the Mandelstam variable representing the [center-of-mass energy](@entry_id:265852) squared.

The amplitude can be decomposed into partial waves, $a_J(s)$, for each angular momentum state $J$. The [s-wave](@entry_id:754474) ($J=0$) partial amplitude, $a_0$, is obtained by projecting out the spherically symmetric component of the full amplitude. For $\mathcal{M} = s/v^2$, this projection yields:
$$
a_0(s) = \frac{1}{32\pi} \int_{-1}^{1} d(\cos\theta) \mathcal{M} = \frac{s}{16\pi v^2}
$$
A fundamental principle of quantum mechanics, the [unitarity](@entry_id:138773) of the S-matrix, requires that probability is conserved. This imposes a strict bound on the partial wave amplitudes, typically expressed as $|\text{Re}(a_0)| \le C$, where $C$ is a constant of order one. The amplitude we have calculated, $a_0(s) \propto s$, grows without limit as the energy increases. Inevitably, it will violate the [unitarity](@entry_id:138773) bound. The energy scale at which this violation occurs can be estimated by setting $a_0(s) = C$, which gives $s = 16\pi C v^2$. The corresponding energy scale is $\sqrt{s} = 4v\sqrt{\pi C}$ [@problem_id:671298]. For $C=1/2$, this scale is approximately $1.2$ TeV.

This result is of paramount importance. It signals that the simple effective theory of Goldstone bosons must break down at or before the TeV scale. The theory is incomplete, and new physics must emerge to restore [unitarity](@entry_id:138773). The Higgs mechanism provides the most elegant and, as confirmed by experiment, correct solution to this puzzle.

### Spontaneous Symmetry Breaking and Mass Generation

The solution to the mass problem lies in the concept of **Spontaneous Symmetry Breaking (SSB)**. SSB occurs when the ground state of a system, its vacuum, possesses less symmetry than the physical laws (the Lagrangian) that govern it.

Imagine a scalar field $\phi$ with a potential energy density given by:
$$
V(\phi) = -\frac{\mu^2}{2} \phi^2 + \frac{\lambda}{4} \phi^4
$$
where $\mu^2$ and $\lambda$ are positive real constants. This potential, often called the "Mexican hat" potential, is symmetric under the reflection $\phi \to -\phi$. However, the lowest energy states, or vacua, do not respect this symmetry. The minimum of the potential is not at $\phi=0$, but rather at the values $\phi_0 = \pm v$, where $v = \sqrt{\mu^2/\lambda}$. The system must choose one of these degenerate ground states. Once a choice is made, say $\langle \phi \rangle = +v$, the reflection symmetry of the vacuum is lost. This non-zero value of the field in the vacuum is known as a **[vacuum expectation value](@entry_id:146340) (VEV)**.

The true genius of the **Higgs mechanism** is to apply this principle to a theory with a *local*, or gauge, symmetry. The consequences are dramatic. To illustrate this, let's consider a toy model with an $SO(3)$ gauge symmetry, which is spontaneously broken to an $SO(2)$ subgroup [@problem_id:782477]. Let the theory contain a triplet of real [scalar fields](@entry_id:151443), $\vec{\phi} = (\phi_1, \phi_2, \phi_3)^T$, and three gauge bosons $A_\mu^a$. The scalar Lagrangian is:
$$
\mathcal{L} = \frac{1}{2} (D_\mu \vec{\phi})^T (D^\mu \vec{\phi}) + \frac{\mu^2}{2} (\vec{\phi}^T \vec{\phi}) - \frac{\lambda}{4} (\vec{\phi}^T \vec{\phi})^2
$$
The potential drives the scalar field to acquire a VEV with magnitude $v = \sqrt{\mu^2/\lambda}$. We can choose to align this VEV along the third direction without loss of generality: $\langle \vec{\phi} \rangle = (0, 0, v)^T$.

Let's examine the consequences of this VEV.
First, we analyze the spectrum of scalar particles by considering small fluctuations around the vacuum: $\vec{\phi}(x) = (0, 0, v+h(x))^T$. The field $h(x)$ represents excitations in the magnitude of the [scalar field](@entry_id:154310) away from the vacuum. The mass of this particle is determined by the curvature of the potential in that direction. The mass-squared is found to be $m_H^2 = 2\lambda v^2 = 2\mu^2$. This is the **Higgs boson**, a physical scalar particle. The fluctuations in the other directions, corresponding to movements along the valley of the potential, are the massless **Goldstone bosons**.

Next, we inspect the scalar kinetic term, $\frac{1}{2} (D_\mu \vec{\phi})^T (D^\mu \vec{\phi})$. Substituting the VEV $\langle \vec{\phi} \rangle$ into this term reveals a piece of the Lagrangian that is quadratic in the gauge fields:
$$
\mathcal{L}_{mass} = \frac{1}{2} (g \epsilon_{ijk} A_\mu^j \langle \phi_k \rangle)^2 = \frac{g^2 v^2}{2} (A_\mu^1 A^{1\mu} + A_\mu^2 A^{2\mu})
$$
This is precisely the form of a mass term for the gauge bosons $A_\mu^1$ and $A_\mu^2$. They have acquired a mass $m_A = gv$. The generators corresponding to these two bosons are "broken" as they transform the vacuum state $\langle\vec{\phi}\rangle$ into a different state. The third [gauge boson](@entry_id:274088), $A_\mu^3$, remains massless because its corresponding generator leaves the vacuum invariant ($SO(2)$ rotation around the 3-axis). The two would-be Goldstone bosons have been absorbed, becoming the [longitudinal polarization](@entry_id:202391) modes of the now-massive $A_\mu^1$ and $A_\mu^2$ bosons.

This toy model demonstrates the essential features of the Higgs mechanism: a [scalar field](@entry_id:154310) acquires a VEV, breaking a gauge symmetry. Some gauge bosons acquire mass, while one physical scalar Higgs boson remains. Crucially, the parameters of the Lagrangian are directly related to physical observables. For instance, we can express the dimensionless self-coupling $\lambda$ in terms of the physical masses and the gauge coupling $g$: $\lambda = \frac{g^2 m_H^2}{2 m_A^2}$ [@problem_id:782477].

### The Higgs Mechanism in the Standard Model

The application of this mechanism to the Standard Model's $SU(2)_L \times U(1)_Y$ [electroweak symmetry](@entry_id:149377) is a direct, albeit more algebraically complex, extension of the principles outlined above.

The SM introduces a complex scalar doublet $\Phi$ with [weak hypercharge](@entry_id:149263) $Y=1/2$:
$$
\Phi = \begin{pmatrix} \phi^+ \\ \phi^0 \end{pmatrix}
$$
The Lagrangian for the Higgs sector contains a kinetic term and a potential:
$$
\mathcal{L}_{\text{Higgs}} = (D_\mu \Phi)^\dagger (D^\mu \Phi) - V(\Phi), \quad \text{with} \quad V(\Phi) = -\mu^2 (\Phi^\dagger \Phi) + \lambda (\Phi^\dagger \Phi)^2
$$
For $\mu^2 > 0$ and $\lambda > 0$, SSB occurs. The minimum of the potential is at $\Phi^\dagger \Phi = v^2/2$, where $v = \sqrt{\mu^2/\lambda}$. We choose a vacuum state that preserves electromagnetic charge, so only the neutral component of the doublet acquires a VEV. In the **unitary gauge**, we parameterize the Higgs field in terms of the single physical Higgs boson field, $h(x)$:
$$
\Phi(x) = \frac{1}{\sqrt{2}} \begin{pmatrix} 0 \\ v+h(x) \end{pmatrix}
$$
The three other scalar degrees of freedom ($\phi^+, \phi^-$, and the imaginary part of $\phi^0$) have been absorbed to become the longitudinal components of the $W^+, W^-,$ and $Z$ bosons.

#### Gauge Boson and Fermion Masses

The origin of the [gauge boson](@entry_id:274088) masses lies entirely within the Higgs kinetic term $(D_\mu \Phi)^\dagger (D^\mu \Phi)$. The [covariant derivative](@entry_id:152476) is $D_\mu = \partial_\mu - i g \frac{\tau^a}{2} W_\mu^a - i g' \frac{Y}{2} B_\mu$. Substituting the Higgs field in the unitary gauge into this term and isolating the parts quadratic in the gauge fields yields the mass terms. This procedure correctly generates masses for the $W^\pm$ and $Z$ bosons, while leaving the photon massless. It predicts their masses to be:
$$
m_W = \frac{gv}{2}, \quad m_Z = \frac{\sqrt{g^2+g'^2}v}{2}
$$
Furthermore, this same kinetic term dictates the interactions between the Higgs boson and the [gauge bosons](@entry_id:200257). For example, the interaction vertex between one Higgs boson and two $Z$ bosons is described by the term $\mathcal{L}_{hZZ} = C_{hZZ} h Z_\mu Z^\mu$. By expanding the kinetic term and isolating terms linear in $h$ and quadratic in the $Z$ field, we can calculate the coupling constant $C_{hZZ}$ [@problem_id:336681]. The calculation reveals:
$$
C_{hZZ} = \frac{v(g^2+g'^2)}{4} = \frac{m_Z^2}{v}
$$
This direct relationship between a particle's mass and its coupling to the Higgs is a hallmark prediction of the SM Higgs mechanism.

A similar challenge exists for [fermion masses](@entry_id:155586). An explicit mass term like $m_f \bar{\psi}_f \psi_f = m_f(\bar{\psi}_{f,L} \psi_{f,R} + \bar{\psi}_{f,R} \psi_{f,L})$ is forbidden by gauge invariance, because left-handed and right-handed fermions transform differently under $SU(2)_L$. The solution is the introduction of **Yukawa couplings** between the Higgs doublet and the fermions. For a generic fermion $f$, this interaction is of the form:
$$
\mathcal{L}_{\text{Yukawa}} = -y_f \left( (\bar{\psi}_L \Phi) \psi_R + \bar{\psi}_R (\Phi^\dagger \psi_L) \right)
$$
After SSB, when we substitute $\Phi(x) = \frac{1}{\sqrt{2}} (0, v+h(x))^T$, this Lagrangian term becomes:
$$
\mathcal{L}_{\text{Yukawa}} \to - \frac{y_f v}{\sqrt{2}} (\bar{\psi}_{f,L} \psi_{f,R} + \bar{\psi}_{f,R} \psi_{f,L}) - \frac{y_f}{\sqrt{2}} h(x) (\bar{\psi}_{f,L} \psi_{f,R} + \bar{\psi}_{f,R} \psi_{f,L})
$$
This single term achieves two goals simultaneously. The first part is a mass term, identifying the [fermion mass](@entry_id:159379) as $m_f = y_f v / \sqrt{2}$. The second part is an [interaction term](@entry_id:166280) between the Higgs boson and the fermion, with a [coupling strength](@entry_id:275517) $g_{Hff} = y_f/\sqrt{2} = m_f/v$. Once again, the coupling of the Higgs boson to a particle is directly proportional to that particle's mass.

This prediction is directly testable through Higgs boson decays. For a Higgs boson heavy enough to decay into a fermion-antifermion pair ($m_H > 2m_f$), the partial decay width can be calculated. The squared [matrix element](@entry_id:136260) is proportional to $g_{Hff}^2 \propto m_f^2$. The full calculation for the decay width $\Gamma(H \to f\bar{f})$ yields [@problem_id:206679]:
$$
\Gamma(H \to f\bar{f}) = \frac{N_c m_f^2 m_H}{8\pi v^2} \left(1 - \frac{4m_f^2}{m_H^2}\right)^{3/2}
$$
where $N_c$ is the number of colors ($N_c=3$ for quarks, $N_c=1$ for leptons). This formula beautifully encapsulates the principle: the heavier the fermion, the stronger its interaction with the Higgs, and the more probable the decay.

### Probing the Higgs Sector: Self-Interactions and High-Energy Behavior

The Higgs mechanism is more than just a source of mass; it predicts a rich structure of self-interactions that are essential for the consistency of the theory and provide a window into the fundamental nature of the electroweak vacuum.

By expanding the Higgs potential $V(\Phi)$ around its [vacuum expectation value](@entry_id:146340), we uncover terms involving powers of the physical Higgs field $h(x)$:
$$
V(h) = \frac{1}{2}(2\lambda v^2)h^2 + \lambda v h^3 + \frac{\lambda}{4} h^4 - \frac{\lambda v^4}{4}
$$
The term quadratic in $h$ confirms the Higgs mass, $m_h^2 = 2\lambda v^2$. The subsequent terms describe **trilinear ($h^3$) and quartic ($h^4$) Higgs self-interactions**. These interactions are crucial. The trilinear coupling, for example, is what allows the Higgs mechanism to solve the [unitarity](@entry_id:138773) problem in $W_L W_L$ scattering mentioned earlier.

The strengths of these couplings are fixed by the parameters of the potential. The Lagrangian term for the trilinear coupling is typically written as $-\frac{\lambda_{hhh}}{3!}h^3$. From the expansion of the potential, we identify $\lambda_{hhh} = 6\lambda v$. Using the relation $m_h^2 = 2\lambda v^2$, we can express this purely in terms of physical observables:
$$
\lambda_{hhh} = \frac{3m_h^2}{v}
$$
These relationships provide stringent tests of the SM. For instance, we can compute the ratio of the trilinear Higgs self-coupling to the quartic coupling between two Higgs bosons and two Z bosons, $g_{hhZZ}$ [@problem_id:428722]. The latter coupling arises from the Higgs kinetic term and is found to be $g_{hhZZ} = m_Z^2/v^2$. Their ratio is:
$$
\frac{\lambda_{hhh}}{g_{hhZZ}} = \frac{3m_h^2/v}{m_Z^2/v^2} = \frac{3m_h^2 v}{m_Z^2}
$$
Measuring these different couplings independently and verifying such relations is a primary goal of the high-luminosity [particle collider](@entry_id:188250) program.

The Goldstone Boson Equivalence Theorem, which motivated our search for the Higgs, also serves as a powerful calculational tool at high energies. Consider the scattering process $W^+_L W^-_L \to HH$. At energies $\sqrt{s} \gg m_W, m_H$, the amplitude is given by the corresponding Goldstone boson process $\phi^+\phi^- \to HH$. The interaction Lagrangian contains a four-point contact term, $-\lambda \phi^+\phi^- H^2$, which gives a tree-level scattering amplitude $\mathcal{M} = -2\lambda$. Expressing this in terms of physical quantities gives [@problem_id:208319]:
$$
\mathcal{M}(W^+_L W^-_L \to HH) \approx -2\lambda = -\frac{m_H^2}{v^2}
$$
Unlike the Higgs-less case, this amplitude does not grow with energy, thus preserving [unitarity](@entry_id:138773). The Higgs boson and its self-interactions are precisely what is required to tame the problematic high-energy behavior of the [electroweak theory](@entry_id:137910).

### The Higgs Sector and Precision Physics: Custodial Symmetry

The specific structure of the SM Higgs sector—a single complex SU(2) doublet—has subtle consequences that can be tested with extraordinary precision. One such consequence is an accidental global symmetry of the Higgs potential known as **[custodial symmetry](@entry_id:156356)**.

The potential $V(\Phi) = \lambda(\Phi^\dagger\Phi - v^2/2)^2$ depends only on the magnitude $\Phi^\dagger\Phi = |\phi^0|^2 + |\phi^+|^2$. This expression has a symmetry larger than the gauged $SU(2)_L \times U(1)_Y$. It is also invariant under an $SU(2)_R$ transformation that acts on the doublet as $\Phi \to U_R \Phi$, where $U_R$ is an $SU(2)$ matrix. Combined, the full symmetry of the potential is $SU(2)_L \times SU(2)_R$. When the Higgs acquires a VEV, this symmetry is broken to the diagonal subgroup, $SU(2)_C$, called custodial $SU(2)$.

This [custodial symmetry](@entry_id:156356) protects the relationship between the $W$ and $Z$ boson masses. It is the reason why the electroweak **$\rho$ parameter**, defined as $\rho = m_W^2 / (m_Z^2 \cos^2\theta_W)$, is exactly equal to 1 at tree level.

However, [custodial symmetry](@entry_id:156356) is not exact in the full Standard Model. It is broken by two effects:
1.  The $U(1)_Y$ hypercharge interaction, since the gauge coupling $g'$ is not zero.
2.  The Yukawa couplings, which are different for the "up-type" and "down-type" quarks within an $SU(2)_L$ doublet (e.g., $y_t \gg y_b$).

These symmetry-breaking effects induce [radiative corrections](@entry_id:157711) to the $\rho$ parameter, such that $\rho = 1 + \Delta\rho$. The dominant contribution comes from the large mass splitting in the third-generation quark doublet $(t, b)$. The difference in mass leads to a difference in the one-loop self-energies of the $W$ boson (which couples $t$ to $b$) and the neutral $Z$ boson (which couples $t$ to $t$ and $b$ to $b$). This difference can be calculated and provides a correction to $\rho$ that is proportional to the mass-squared difference, $\Delta\rho \propto m_t^2 - m_b^2$. A precise calculation, neglecting the bottom quark mass, gives the one-loop contribution to the relevant self-energy difference as [@problem_id:182498]:
$$
\Delta\Pi = \Pi_{WW}(0) - \Pi_{33}(0) = \frac{N_c g^2 m_t^2}{32\pi^2}
$$
This leads to a positive correction $\Delta\rho$, which has been measured with high precision and agrees remarkably well with the theoretical prediction, providing strong indirect evidence for the SM structure and the large mass of the top quark even before its discovery.

### The Higgs at High Energies: Vacuum Stability

The discovery of the Higgs boson completed the particle content of the Standard Model, but it also opened a new line of inquiry into the ultimate nature of our universe. The parameters of the Higgs potential, particularly the self-coupling $\lambda$, are not [fundamental constants](@entry_id:148774). They evolve with the energy scale at which they are measured, a behavior described by **Renormalization Group Equations (RGEs)**.

The evolution, or "running," of $\lambda$ is determined by a competition between different quantum effects:
*   The Higgs self-interaction itself contributes positively to the RGE, tending to make $\lambda$ grow with energy.
*   The gauge couplings ($g, g'$) also provide positive contributions, driving $\lambda$ up [@problem_id:182463]. For instance, the one-loop contribution from gauge bosons to the part of the effective potential that renormalizes $\lambda$ is proportional to $(3g^4 + \frac{3}{2}(g^2+g'^2)^2)$.
*   Yukawa couplings, dominated by the top quark, contribute negatively. The top quark loop contribution is proportional to $-y_t^4$ and powerfully drives $\lambda$ down.

The fate of $\lambda$ at very high energies, such as the Planck scale, depends on the precise measured values of the Higgs mass (which fixes $\lambda$ at the electroweak scale) and the [top quark mass](@entry_id:160842) (which fixes $y_t$). The RGE for $\lambda$ can be written schematically as:
$$
16\pi^2 \frac{d\lambda}{dt} = \beta_\lambda = (24\lambda^2 + ...) + (12\lambda y_t^2 - ...) - 6y_t^4 + ...
$$
where $t = \ln(\mu)$ is the energy scale. The interplay between these terms can lead to interesting high-energy behavior. For example, one could ask if there exists an ultraviolet "fixed point," a value where the ratio of couplings $R = \lambda/y_t^2$ becomes constant ($dR/dt=0$). Solving for such a fixed point using the simplified RGEs reveals a stable solution $R^* = (\sqrt{65}-1)/16$, suggesting a possible non-trivial structure for the theory at high energies [@problem_id:182458].

Remarkably, with the measured values of $m_H \approx 125$ GeV and $m_t \approx 173$ GeV, the negative pull from the top quark is very strong. The RGEs predict that $\lambda$ decreases with energy and may become negative at a very high scale, $\Lambda \sim 10^{10} - 10^{12}$ GeV. If $\lambda$ becomes negative, the Higgs potential turns over and is no longer bounded from below, leading to a catastrophic instability. This implies that our current electroweak vacuum is not the true, lowest-energy state of the universe, but is merely a [local minimum](@entry_id:143537)—it is **metastable**.

The decay from this false vacuum to the true vacuum would occur via quantum tunneling, nucleating a bubble of true vacuum that would then expand at nearly the speed of light. The rate of this decay, $\Gamma/V$, can be estimated semiclassically and is exponentially suppressed by the Euclidean action of the "bounce" solution, $B$: $\Gamma/V \propto \exp(-B)$. In the thin-wall approximation, valid when the energy difference $\Delta V$ between the false and true vacua is small, the bounce action is given by $B = 27\pi^2 S_1^4 / (2 (\Delta V)^3)$, where $S_1$ is the surface tension of the bubble wall.

We can illustrate this with a toy potential $V(\phi) = \frac{\lambda}{4}(\phi^2-\sigma^2)^2 + \frac{\delta}{2\sigma}\phi$, where a small term proportional to $\delta$ breaks the degeneracy between the two minima. In this model, the energy difference is $\Delta V = \delta$ and the surface tension can be calculated as $S_1 \propto \sqrt{\lambda}\sigma^3$. The resulting bounce action is $B \propto \lambda^2 \sigma^{12} / \delta^3$ [@problem_id:182472]. The lifetime of the vacuum is extremely sensitive to the parameters of the potential. For the Standard Model, the calculated lifetime of our vacuum is many orders of magnitude longer than the current age of the universe, so there is no immediate danger. Nevertheless, the possibility that our universe exists in a metastable state is a profound implication of Higgs physics, connecting the properties of the smallest known particles to the ultimate fate of the cosmos.