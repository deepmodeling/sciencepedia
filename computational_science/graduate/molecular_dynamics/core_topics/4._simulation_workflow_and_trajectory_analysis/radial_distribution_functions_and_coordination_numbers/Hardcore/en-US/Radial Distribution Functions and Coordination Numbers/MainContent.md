## Introduction
In the study of condensed matter, from simple liquids to complex biological macromolecules, understanding the arrangement of constituent particles is paramount. The raw output of a molecular dynamics simulation—a trajectory of atomic coordinates—is a trove of information, but it requires powerful analytical tools to translate this microscopic data into physical insight. The central challenge is to move beyond a mere snapshot of particle positions to a statistical description of structure that reveals the underlying physics and chemistry governing the system. This is precisely the role of the [radial distribution function](@entry_id:137666) (RDF) and its derivative concept, the coordination number.

This article provides a comprehensive exploration of these essential tools. We will begin in the first chapter, **Principles and Mechanisms**, by deriving the RDF from the first principles of statistical mechanics, establishing its profound connection to thermodynamics via the [potential of mean force](@entry_id:137947), and examining how to interpret its signature features. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the versatility of the RDF in practice, showing how it is used to identify [phases of matter](@entry_id:196677), analyze complex mixtures, and validate force fields in fields ranging from materials science to [biophysics](@entry_id:154938). Finally, the **Hands-On Practices** section will offer concrete computational problems to solidify your understanding and build practical analysis skills. By the end, you will be equipped to use the RDF not just as a descriptor, but as an explanatory and predictive tool in your own research.

## Principles and Mechanisms

This chapter delves into the theoretical foundations and practical mechanisms underpinning one of the most fundamental tools in molecular simulation: the radial distribution function. We will begin by deriving its definition from first principles of statistical mechanics, explore its profound connection to thermodynamics through the [potential of mean force](@entry_id:137947), and learn how to interpret its features to distinguish different [phases of matter](@entry_id:196677). Subsequently, we will extend these concepts to multi-component systems and, critically, examine the practical aspects of its computation, including the inherent artifacts introduced by finite simulation sizes and specific thermodynamic ensembles.

### From Particle Densities to the Radial Distribution Function

The structure of a fluid is encoded in the spatial arrangement of its constituent particles. In statistical mechanics, this is formally described by multi-particle density distributions. The simplest is the **one-particle density**, $\rho^{(1)}(\mathbf{r})$, which gives the average number of particles per unit volume at a position $\mathbf{r}$. For a **homogeneous** fluid, this density is uniform throughout space, equal to the bulk [number density](@entry_id:268986) $\rho = N/V$, where $N$ is the number of particles and $V$ is the volume.

Correlations between particles are captured by the **two-particle density**, $\rho^{(2)}(\mathbf{r}_1, \mathbf{r}_2)$. The quantity $\rho^{(2)}(\mathbf{r}_1, \mathbf{r}_2) \mathrm{d}\mathbf{r}_1 \mathrm{d}\mathbf{r}_2$ represents the probability of finding one particle within an infinitesimal [volume element](@entry_id:267802) $\mathrm{d}\mathbf{r}_1$ at $\mathbf{r}_1$ and, simultaneously, another particle within $\mathrm{d}\mathbf{r}_2$ at $\mathbf{r}_2$. If the particles were completely uncorrelated (as in an ideal gas), this joint probability would simply be the product of the individual probabilities: $\rho^{(2)}(\mathbf{r}_1, \mathbf{r}_2) = \rho^{(1)}(\mathbf{r}_1) \rho^{(1)}(\mathbf{r}_2)$.

In any real system with interactions, correlations are significant. We quantify these correlations using the **pair-distribution function**, $g^{(2)}(\mathbf{r}_1, \mathbf{r}_2)$, defined as the ratio of the actual two-particle density to its uncorrelated counterpart :
$$
g^{(2)}(\mathbf{r}_1, \mathbf{r}_2) = \frac{\rho^{(2)}(\mathbf{r}_1, \mathbf{r}_2)}{\rho^{(1)}(\mathbf{r}_1) \rho^{(1)}(\mathbf{r}_2)}
$$
This function measures how the presence of a particle at $\mathbf{r}_1$ influences the density of particles at $\mathbf{r}_2$.

For the vast majority of systems studied in molecular dynamics, such as bulk liquids and gases, we can assume the system is not only homogeneous but also **isotropic** (rotationally invariant).
-   **Homogeneity** implies that correlations depend only on the relative [displacement vector](@entry_id:262782) $\mathbf{r} = \mathbf{r}_2 - \mathbf{r}_1$, so $g^{(2)}(\mathbf{r}_1, \mathbf{r}_2)$ becomes $g^{(2)}(\mathbf{r})$. Also, $\rho^{(1)}(\mathbf{r})$ becomes the constant $\rho$.
-   **Isotropy** implies that correlations depend only on the magnitude of the displacement, $r = |\mathbf{r}|$, not its direction.

Under these two crucial assumptions, the pair-[distribution function](@entry_id:145626) simplifies to a function of a single scalar variable, the separation distance $r$. This simplified function is the **[radial distribution function](@entry_id:137666) (RDF)**, universally denoted as **$g(r)$**.

The definition becomes:
$$
\rho^{(2)}(r) = \rho^2 g(r)
$$
This relationship provides the most common physical interpretation of the RDF: the quantity $\rho g(r)$ represents the average local number density of particles at a distance $r$ from a central, reference particle. Where $g(r) > 1$, particles are more likely to be found than in a uniform random distribution; where $g(r)  1$, they are less likely. As $r \to \infty$, particle positions become uncorrelated, and thus $\lim_{r\to\infty} g(r) = 1$.

### The Potential of Mean Force: Connecting Structure and Thermodynamics

The structural information contained in $g(r)$ has a deep thermodynamic meaning, which is revealed through the **[potential of mean force](@entry_id:137947) (PMF)**, denoted $w(r)$. The PMF is defined as the potential that yields the [mean force](@entry_id:751818) acting between two particles held at a fixed separation $r$, averaged over all configurations of the remaining $N-2$ particles in the system. It represents the effective, solvent-averaged interaction energy between the pair. The fundamental connection between the RDF and the PMF is given by statistical mechanics :
$$
g(r) = \exp\left(-\frac{w(r)}{k_B T}\right) \quad \text{or} \quad w(r) = -k_B T \ln g(r)
$$
where $k_B$ is the Boltzmann constant and $T$ is the temperature.

This equation is extraordinarily powerful. It allows us to interpret the structural features of $g(r)$ in energetic terms. A peak in $g(r)$ (where $g(r) > 1$) corresponds to a minimum (a potential well) in $w(r)$, indicating a thermodynamically favorable separation. A trough in $g(r)$ (where $g(r)  1$) corresponds to a maximum (a [potential barrier](@entry_id:147595)) in $w(r)$, indicating an unfavorable separation. The region where $g(r) \approx 0$ at small $r$ corresponds to an infinitely high repulsive barrier in $w(r)$, representing the excluded volume of the particles.

A frequent point of confusion is the relationship between the PMF, $w(r)$, and the fundamental **bare [pair potential](@entry_id:203104)**, $u(r)$, which describes the interaction between two particles in a vacuum. The PMF can be conceptually decomposed as:
$$
w(r) = u(r) + w_{\text{ind}}(r)
$$
where $w_{\text{ind}}(r)$ is the indirect contribution arising from the averaged influence of the surrounding fluid particles (e.g., [solvation](@entry_id:146105) effects, [entropic forces](@entry_id:137746)). Only in the theoretical **dilute limit** ($\rho \to 0$), where the influence of other particles vanishes, does $w_{\text{ind}}(r) \to 0$ and thus $w(r) \to u(r)$. At any finite density, $w(r) \neq u(r)$, even if the system's Hamiltonian is purely pairwise additive.

More formally, a low-density expansion from statistical mechanics reveals that $g(r) \approx \exp[-\beta u(r)]$ (where $\beta = 1/k_B T$) is only the leading-order term. The first-order correction in density involves contributions from a third particle, mediated by the **Mayer f-function**, $f(r) = \exp[-\beta u(r)] - 1$ :
$$
g(r) \approx e^{-\beta u(r)} \left( 1 + \rho \int f(|\mathbf{r}_1 - \mathbf{r}_3|) f(|\mathbf{r}_2 - \mathbf{r}_3|) \mathrm{d}\mathbf{r}_3 + O(\rho^2) \right)
$$
This expression makes it explicit that deviations between $w(r)$ and $u(r)$ are a direct consequence of density-dependent many-body correlations.

### Interpreting the Radial Distribution Function

#### Qualitative Features and Phases of Matter

The shape of the RDF provides a distinct fingerprint for the phase of matter .

-   **Gas:** In a dilute gas, particles are far apart and interact weakly. The RDF reflects this disorder. It is essentially zero for $r$ less than the particle diameter (due to excluded volume) and quickly rises to approximately $1$ for all larger distances. There are no significant peaks or oscillations, indicating a lack of structural ordering.

-   **Liquid:** Liquids are dense and disordered. The high density enforces a strong local structure due to packing constraints. The RDF of a liquid exhibits a sharp first peak, corresponding to the nearest-neighbor "[solvation shell](@entry_id:170646)." This is followed by a series of subsequent peaks of decreasing amplitude and increasing breadth, reflecting second, third, and further neighbor shells. These oscillations are damped and decay to unity over a distance of a few particle diameters, signifying the presence of **[short-range order](@entry_id:158915)** but the absence of **long-range order**.

-   **Crystal:** Crystalline solids possess long-range periodic order. Their RDFs reflect this underlying lattice structure. It consists of a series of sharp, well-defined peaks at distances corresponding to the successive neighbor shells of the crystal lattice. Unlike in a liquid, these peaks do not decay to unity at large $r$ (in an infinite crystal), indicating persistent **long-range order**. At finite temperature, thermal vibrations cause the peaks to broaden, with the broadening effect increasing for more distant shells.

This distinction is deeply related to the system's scattering properties. The **[static structure factor](@entry_id:141682)**, $S(\mathbf{k})$, which is measurable by X-ray or neutron scattering, is related to the Fourier transform of $g(r)$. The damped, short-range oscillations of a liquid's $g(r)$ transform into broad peaks in $S(\mathbf{k})$. In contrast, the undamped, long-range periodic peaks of a crystal's $g(r)$ transform into a set of infinitely sharp **Bragg peaks** in $S(\mathbf{k})$, located at the [reciprocal lattice vectors](@entry_id:263351).

#### Coordination Number

A key quantitative measure that can be extracted from the RDF is the **[coordination number](@entry_id:143221)**, $N_c(R)$, which is the average number of particles found within a sphere of radius $R$ around a central particle. It is calculated by integrating the local [number density](@entry_id:268986), $\rho g(r)$, over the volume of this sphere, which for an isotropic system is :
$$
N_c(R) = \int_0^R \rho g(r) \, 4\pi r^2 \mathrm{d}r = 4\pi \rho \int_0^R g(r) r^2 \mathrm{d}r
$$
By choosing $R$ to be the position of the first minimum in $g(r)$, this integral provides a robust and widely used definition for the average number of nearest neighbors. This definition is purely structural; it depends only on the observed particle distribution $g(r)$ and is valid regardless of whether the underlying microscopic interactions are pairwise or include many-body terms .

### Application to Multi-Component Systems

The concept of the RDF is readily extended to mixtures. For a [binary mixture](@entry_id:174561) of species $\alpha$ and $\beta$, there are three distinct **partial radial distribution functions**: $g_{\alpha\alpha}(r)$, $g_{\beta\beta}(r)$, and $g_{\alpha\beta}(r)$. The function $g_{\alpha\beta}(r)$ describes the distribution of species $\beta$ around species $\alpha$. It is defined such that the local density of $\beta$ particles at a distance $r$ from a central $\alpha$ particle is given by $\rho_\beta g_{\alpha\beta}(r)$, where $\rho_\beta = N_\beta/V$ is the bulk partial number density of species $\beta$ .

The coordination number of species $\beta$ around species $\alpha$ within a radius $R$, denoted $N_{\alpha\beta}(R)$, is then given by:
$$
N_{\alpha\beta}(R) = 4\pi \rho_\beta \int_0^R g_{\alpha\beta}(r) r^2 \mathrm{d}r
$$
It is crucial to use this **number-based** definition when the goal is to determine the actual number of neighboring particles in a [specific solvation](@entry_id:200144) shell.

For some applications, such as comparing to certain scattering theories or obtaining a single structural profile for the entire mixture, a **mole-fraction-weighted** RDF is sometimes constructed :
$$
g_{\text{mix}}(r) = \sum_{i,j} x_i x_j g_{ij}(r)
$$
where $x_i$ is the mole fraction of species $i$. This function averages over all possible pair types, weighted by their abundance. It provides a global view of the mixture's structure but loses the species-specific detail necessary for calculating coordination numbers like $N_{\alpha\beta}(R)$.

### Computational Practice and Artifacts

#### Estimating $g(r)$ from Simulations

In molecular dynamics, $g(r)$ is typically computed by a histogram method. Across many simulation snapshots, one calculates the distances between all pairs of particles and bins them into a histogram. Let $\langle C(r, \Delta r) \rangle$ be the average number of pairs per configuration found in a radial bin $[r, r+\Delta r)$. The RDF is the ratio of this observed probability to the probability in an ideal gas, normalized by volumes :
$$
\widehat{g}(r) = \frac{ \langle C(r, \Delta r) \rangle / \binom{N}{2} }{ (4\pi r^2 \Delta r) / V } = \frac{V \langle C(r, \Delta r) \rangle}{\binom{N}{2} 4\pi r^2 \Delta r} \approx \frac{2V \langle C(r, \Delta r) \rangle}{N^2 4\pi r^2 \Delta r}
$$
This normalization correctly accounts for the number of pairs, the shell volume, and the system volume, ensuring that $g(r) \to 1$ for large $r$.

#### Finite-Size and Ensemble Effects

The calculation of $g(r)$ from finite simulation cells is subject to several artifacts that must be understood to avoid misinterpretation.

**1. Geometric Truncation and the Minimum Image Convention:**
Simulations use **Periodic Boundary Conditions (PBC)** to mimic an infinite system. The distance between two particles must be calculated using the **Minimum Image Convention (MIC)**, which finds the shortest distance between a particle and all periodic images of another. For an orthorhombic cell of side lengths $L_x, L_y, L_z$, this is done component-wise, e.g., $\Delta x_{\text{MIC}} = \Delta x - L_x \cdot \text{round}(\Delta x / L_x)$ .

The MIC imposes a fundamental limit on the distance at which $g(r)$ can be computed without bias. For a spherical shell of radius $r$ around a central particle to be complete, it must not intersect with its own periodic images. This is guaranteed only if the radius $r$ is less than half the shortest dimension of the periodic cell. For a general [triclinic cell](@entry_id:139679) defined by [lattice vectors](@entry_id:161583) $\mathbf{a}, \mathbf{b}, \mathbf{c}$, this radius of guaranteed isotropy, $r_{\text{iso}}$, is half the length of the shortest lattice vector $\mathbf{L}_{\mathbf{n}} = n_1\mathbf{a} + n_2\mathbf{b} + n_3\mathbf{c}$ over all non-zero integer triplets $(n_1, n_2, n_3)$ :
$$
r_{\text{iso}} = \frac{1}{2} \min_{\mathbf{n} \in \mathbb{Z}^3 \setminus \{\mathbf{0}\}} |\mathbf{L}_{\mathbf{n}}|
$$
For a simple cubic box of side $L$, this reduces to the well-known "half-box" rule, $r  L/2$. Beyond this cutoff, the MIC artificially "folds" longer distances into shorter ones, leading to a systematic undercounting of pairs at large $r$ (causing $g(r)$ to trend towards zero) and a corresponding overcounting at smaller $r$. For example, for a [triclinic cell](@entry_id:139679) with vectors $\mathbf{a} = (3.2, 0, 0)$, $\mathbf{b} = (0.5, 2.8, 0)$, and $\mathbf{c} = (0.2, 0.4, 3.0)$ nm, the shortest lattice vector is $\mathbf{b}$, with length $|\mathbf{b}| \approx 2.844$ nm. The RDF is therefore only guaranteed to be free of geometric artifacts for $r  r_{\text{iso}} = 1.422$ nm .

**2. Canonical Ensemble (NVT) Constraint:**
A more subtle artifact arises from simulating in the canonical (NVT) ensemble, where the total number of particles $N$ is strictly fixed. This constraint suppresses long-wavelength [density fluctuations](@entry_id:143540). In the grand canonical ($\mu$VT) ensemble, where $N$ can fluctuate, [the structure factor](@entry_id:158623) at zero wavevector, $S(0)$, is related to the [isothermal compressibility](@entry_id:140894) $\kappa_T$ by the [compressibility](@entry_id:144559) theorem: $S_{GC}(0) = \rho k_B T \kappa_T$. However, in the NVT ensemble, the lack of total number fluctuations forces $S_{NVT}(0) = 0$.

This discrepancy implies that the long-range behavior of $g(r)$ computed in an NVT simulation is incorrect. Specifically, it must satisfy the integral constraint $\rho \int_V (g(r)-1) \mathrm{d}\mathbf{r} = -1$, which forces $g(r)$ to dip slightly below 1 at large $r$ to compensate for the $g(r)1$ peaks at short range. A correction can be derived to make the NVT result consistent with the grand canonical expectation. For a system of $N$ particles, adding a small constant offset $\delta$ to the computed $g_{NVT}(r)$ restores the correct $S(0)$ value. This correction term is :
$$
\delta = \frac{\rho k_B T \kappa_T}{N}
$$
For example, for a simulation of $N=512$ water particles at standard conditions, this correction is on the order of $\delta \approx 1.21 \times 10^{-4}$. While small, this correction is essential for high-precision studies connecting structure to thermodynamic properties.