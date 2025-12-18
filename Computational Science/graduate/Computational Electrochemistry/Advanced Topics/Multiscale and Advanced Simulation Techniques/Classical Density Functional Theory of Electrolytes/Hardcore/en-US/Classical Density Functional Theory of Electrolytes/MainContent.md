## Introduction
Understanding the behavior of [electrolytes](@entry_id:137202) at interfaces is a cornerstone of modern electrochemistry, materials science, and biophysics. While classical theories like the Poisson-Boltzmann model provide a foundational starting point, they neglect crucial physical effects such as finite ion size and electrostatic correlations, leading to inaccurate predictions under many realistic conditions. Classical Density Functional Theory (cDFT) emerges as a powerful and physically rich framework that overcomes these limitations by building directly from the principles of statistical mechanics.

This article provides a comprehensive overview of cDFT for electrolytes, designed to bridge fundamental theory with practical application. In the first chapter, **Principles and Mechanisms**, we will deconstruct the theory from the ground up, exploring its thermodynamic basis in the [variational principle](@entry_id:145218) and the systematic construction of the [free energy functional](@entry_id:184428). Following this, the **Applications and Interdisciplinary Connections** chapter will demonstrate how cDFT is used to model the electrochemical double layer, predict measurable quantities like capacitance, and connect to broader topics in [colloid science](@entry_id:204096) and [materials modeling](@entry_id:751724). Finally, the **Hands-On Practices** section offers an opportunity to solidify these concepts through guided computational problems. We begin by examining the fundamental tenets that make cDFT a versatile tool for studying [inhomogeneous fluids](@entry_id:187276).

## Principles and Mechanisms

Classical Density Functional Theory (cDFT) provides a powerful and versatile framework for studying the equilibrium properties of [inhomogeneous fluids](@entry_id:187276), such as [electrolytes](@entry_id:137202) at interfaces. Rooted in the principles of statistical mechanics, cDFT recasts the problem of determining the microscopic structure of a fluid from a description of particle coordinates to a description based on average [number density](@entry_id:268986) fields, $\rho_i(\mathbf{r})$. The central tenet of the theory is a variational principle: for a system in contact with reservoirs of fixed temperature $T$ and chemical potentials $\{\mu_i\}$, the equilibrium density profiles $\{\rho_i(\mathbf{r})\}$ are those that minimize a unique functional, the **[grand potential functional](@entry_id:144711)** $\Omega[\{\rho_i\}]$.

This chapter elucidates the fundamental principles and mechanisms underpinning cDFT for [electrolytes](@entry_id:137202). We will construct the key functionals from first principles, dissect their components, and explore the physical meaning embedded within their mathematical structure.

### Thermodynamic Potentials and the Variational Principle

In the grand canonical ensemble, the thermodynamic state of an open system is described by its volume $V$, temperature $T$, and the chemical potentials $\{\mu_i\}$ of its constituent species. The equilibrium state corresponds to the minimum of the grand potential. In cDFT, this principle is elevated to a functional form. The grand potential is expressed as a functional of the set of all possible density profiles $\{\rho_i(\mathbf{r})\}$:
$$
\Omega[\{\rho_i\}] = F[\{\rho_i\}] + \sum_{i} \int \rho_i(\mathbf{r}) \left( V_i^{\text{ext}}(\mathbf{r}) - \mu_i \right) d\mathbf{r}
$$
Here, $V_i^{\text{ext}}(\mathbf{r})$ is the external potential acting on species $i$ (e.g., from a charged wall or confining geometry), and $F[\{\rho_i\}]$ is the **intrinsic Helmholtz free energy functional**. The equilibrium density profiles are the unique functions $\{\rho_i^{\text{eq}}(\mathbf{r})\}$ that satisfy the variational condition $\delta \Omega / \delta \rho_i(\mathbf{r}) = 0$ for all $i$ and $\mathbf{r}$.

This functional form is part of a larger structure of thermodynamic potentials connected by **Legendre transforms**. Starting with the canonical ensemble (fixed particle numbers $\{N_i\}$, $V$, $T$), the Helmholtz free energy $A$ is the fundamental potential. In cDFT, it is a functional of the densities and external fields. By applying Legendre transforms, we can switch to other ensembles. For instance, transforming with respect to the volume $V$ and its conjugate variable, the pressure $p$, yields the Gibbs free energy functional $G[\{\rho_i\}; p, T] = A[\{\rho_i\}] + pV$. Transforming with respect to the particle numbers $N_i = \int \rho_i(\mathbf{r}) d\mathbf{r}$ and their conjugate chemical potentials $\mu_i$ yields the [grand potential functional](@entry_id:144711) $\Omega[\{\rho_i\}] = A[\{\rho_i\}] - \sum_i \mu_i N_i$. This systematic structure allows for the modeling of electrolytes under various thermodynamic constraints .

The cornerstone of the theory is the intrinsic Helmholtz functional, $F[\{\rho_i\}]$. It is a **[universal functional](@entry_id:140176)** in that it depends only on the temperature and the nature of the interparticle interactions, but not on the external potentials $\{V_i^{\text{ext}}\}$. This universality is formally established through the **constrained-search principle**, a classical analogue of the Levy-Lieb formulation in quantum DFT. The functional $F[\{\rho_i\}]$ is defined as the minimum of the [expectation value](@entry_id:150961) of the internal energy and entropy term, taken over all possible $N$-particle probability distributions $P$ that integrate to the given one-body densities $\{\rho_i(\mathbf{r})\}$ :
$$
F[\{\rho_i\}] = \min_{P \to \{\rho_i\}} \left\{ \int d\mathbf{r}^N \, P(\mathbf{r}^N) \left[ U_{\text{int}}(\mathbf{r}^N) + k_{\mathrm{B}} T \ln P(\mathbf{r}^N) \right] \right\}
$$
where $U_{\text{int}}(\mathbf{r}^N)$ is the total potential energy from interparticle interactions. While this definition is exact and conceptually fundamental, it is not computationally practical. Therefore, the common practice in cDFT is to decompose $F[\{\rho_i\}]$ into parts that are either known exactly or can be accurately approximated:
$$
F[\{\rho_i\}] = F_{\text{id}}[\{\rho_i\}] + F_{\text{ex}}[\{\rho_i\}]
$$
Here, $F_{\text{id}}[\{\rho_i\}]$ is the exactly known [free energy functional](@entry_id:184428) of an ideal gas, and $F_{\text{ex}}[\{\rho_i\}]$ is the **excess free energy functional**, which contains all the complexities arising from particle interactions.

### The Ideal Gas Contribution

The ideal gas functional, $F_{\text{id}}$, accounts for the translational entropy of [non-interacting particles](@entry_id:152322). Its exact form, derived from the [classical partition function](@entry_id:1122429) for [indistinguishable particles](@entry_id:142755), is given by:
$$
F_{\text{id}}[\{\rho_i\}] = k_{\mathrm{B}} T \sum_i \int \rho_i(\mathbf{r})\left[ \ln\left(\Lambda_i^3 \rho_i(\mathbf{r})\right) - 1 \right] d\mathbf{r}
$$
The derivation of this expression from first principles is instructive. It involves three key steps: (1) evaluating the momentum integrals in the [canonical partition function](@entry_id:154330), which introduces the **thermal de Broglie wavelength** $\Lambda_i = h/\sqrt{2\pi m_i k_{\mathrm{B}} T}$; (2) incorporating the Gibbs factor $1/N_i!$ for each species to account for [particle indistinguishability](@entry_id:152187) and ensure entropy is extensive (avoiding the Gibbs paradox); and (3) using Stirling's approximation for $\ln(N_i!)$, which gives rise to the "$-1$" term in the integrand. An equivalent route is through the grand canonical ensemble, where the Legendre transform from the grand potential to the intrinsic free energy naturally yields this form .

An important conceptual point concerns the appearance of the thermal de Broglie wavelength $\Lambda_i$, which depends on Planck's constant $h$ and particle mass $m_i$. While its presence is essential for the dimensional correctness and proper normalization of the free energy, all equilibrium observables in classical statistical mechanics must be independent of $\Lambda_i$. This is indeed the case. In any equilibrium calculation, such as determining a density profile in contact with a bulk reservoir, the term $k_{\mathrm{B}} T \ln(\Lambda_i^3)$ appears as an additive constant in the chemical potential. When equating the local chemical potential to that of the bulk reservoir, this constant term cancels out. Alternatively, one can view this term as being absorbed into a redefinition of the standard-state chemical potential or activity. Consequently, equilibrium density profiles, pressures, and correlation functions are independent of the particle masses in classical systems .

### The Excess Free Energy: Modeling Interactions

The excess free energy functional, $F_{\text{ex}}$, is the heart of the theory's predictive power and is where physical approximations are introduced. For typical models of electrolytes, such as the primitive model (charged hard spheres in a [dielectric continuum](@entry_id:748390)), it is convenient to further decompose this term based on the nature of the interactions:
$$
F_{\text{ex}}[\{\rho_i\}] = F_{\text{ex}}^{\text{hs}}[\{\rho_i\}] + F_{\text{el}}[\{\rho_i\}] + \dots
$$
where $F_{\text{ex}}^{\text{hs}}$ accounts for the short-range, harsh repulsions (hard-sphere interactions) and $F_{\text{el}}$ accounts for the long-range electrostatic (Coulomb) interactions.

#### Mean-Field Electrostatics

The simplest and most common approximation for the electrostatic contribution is the **mean-field** or **Hartree approximation**. This approach treats the electrostatic energy as that of the average charge density, $\rho_c(\mathbf{r}) = \sum_i z_i e \rho_i(\mathbf{r})$, interacting with its own average electrostatic potential, $\phi(\mathbf{r})$. This approximation neglects correlations in the fluctuations of charge density. The mean-field electrostatic functional can be written in three equivalent and useful forms :

1.  **Double Integral Form:** Based on [pairwise additivity](@entry_id:193420) of the Coulomb potential $v_c(\mathbf{r}) = 1/(4\pi \epsilon |\mathbf{r}|)$, where $\epsilon$ is the medium's permittivity. The prefactor of $1/2$ corrects for double-counting each interaction pair.
    $$
    F_{\text{el}}^{\text{MF}}[\{\rho_i\}] = \frac{1}{2}\sum_{i,j} \iint d\mathbf{r}\,d\mathbf{r}'\,\big(z_i e\,\rho_i(\mathbf{r})\big)\,v_c(\mathbf{r}-\mathbf{r}')\,\big(z_j e\,\rho_j(\mathbf{r}')\big)
    $$

2.  **Charge-Potential Form:** This form is intuitive, representing the energy of assembling the charge distribution within the potential it generates.
    $$
    F_{\text{el}}^{\text{MF}}[\{\rho_i\}] = \frac{1}{2}\int \rho_c(\mathbf{r})\,\phi(\mathbf{r})\,d\mathbf{r}, \quad \text{where } \phi(\mathbf{r})=\int v_c(\mathbf{r}-\mathbf{r}')\,\rho_c(\mathbf{r}')\,d\mathbf{r}'
    $$

3.  **Field Energy Form:** This expresses the energy as the total energy stored in the electric field $\mathbf{E} = -\nabla\phi$. This form is particularly useful in [variational calculus](@entry_id:197464).
    $$
    F_{\text{el}}^{\text{MF}}[\{\rho_i\}] = \frac{\epsilon}{2}\int |\nabla\phi(\mathbf{r})|^2\,d\mathbf{r}, \quad \text{where } -\nabla \cdot (\epsilon \nabla \phi) = \rho_c
    $$

A critical issue with the mean-field functional arises for point-like ions. The expression implicitly includes the interaction of each ion with itself, leading to a divergent [self-energy](@entry_id:145608). To correct this, a **regularization** procedure is necessary. The standard approach is to subtract the sum of the self-energies of all individual ions. This subtracted energy for species $i$ is a constant, $E_{\text{self}}(q_i)$, which depends on the regularization scheme but not on the particle positions. The total subtracted term is $\sum_i N_i E_{\text{self}}(q_i)$. In the [grand potential functional](@entry_id:144711), this term has the form $-\sum_i \mu_i^{\text{self}} N_i$, which means it can be absorbed into a redefinition of the chemical potentials, $\mu_i^* = \mu_i + E_{\text{self}}(q_i)$. Since this only shifts the reference energy for each species by a constant amount, it does not affect the physical structure or thermodynamic response properties, such as the Debye [screening length](@entry_id:143797), which are determined by the functional form of the Euler-Lagrange equations .

#### Hard-Sphere Repulsion and Fundamental Measure Theory

Modeling the short-range repulsive interactions, which prevent particles from occupying the same space, is crucial for any realistic fluid theory. For [electrolytes](@entry_id:137202), this is typically handled by the **[hard-sphere model](@entry_id:145542)**. While simple local density approximations exist, the state-of-the-art approach is **Fundamental Measure Theory (FMT)**. FMT is a non-local functional that is constructed based on the geometry of the constituent particles.

In FMT, the hard-sphere excess free energy is written as an integral over a free energy density, $\Phi$, which is a function of a set of **weighted densities**, $\{n_\alpha(\mathbf{r})\}$:
$$
F_{\text{ex}}^{\text{hs}}[\{\rho_i\}] = k_{\mathrm{B}} T \int \Phi(\{n_\alpha(\mathbf{r})\}) \,d\mathbf{r}
$$
The weighted densities are themselves non-local quantities, defined as convolutions of the true number densities $\{\rho_i\}$ with geometric **weight functions** $\{w_\alpha^{(i)}\}$ characteristic of the particle shapes. For hard spheres of radii $\{R_i\}$, the weight functions are derived from the Minkowski functionals of a sphere: volume, surface area, integral [mean curvature](@entry_id:162147), and Euler characteristic. The scalar weighted densities are defined as:
$$
n_{\alpha}(\mathbf{r}) = \sum_i (\rho_i * w_\alpha^{(i)})(\mathbf{r}) = \sum_i \int \rho_i(\mathbf{r}') w_\alpha^{(i)}(\mathbf{r}-\mathbf{r}') \,d\mathbf{r}'
$$
The most important scalar weight functions are $w_3^{(i)}(\mathbf{r}) = \Theta(R_i-|\mathbf{r}|)$, an [indicator function](@entry_id:154167) for the sphere's volume, and $w_2^{(i)}(\mathbf{r}) = \delta(R_i-|\mathbf{r}|)$, a Dirac delta function on the sphere's surface. The theory also includes vector weighted densities to correctly capture the physics of anisotropic packing. The genius of FMT lies in its construction of $\Phi$: it is an algebraic function of the weighted densities designed to be exact in several important limits, including the low-density limit and the zero-dimensional (single cavity) limit .

To make the abstract concept of weighted densities concrete, consider a simple system of hard spheres of radius $R$ near a planar hard wall at $z=0$. A simplified model for the density profile is $\rho(z) = \rho_b \Theta(z-R)$. The weighted density $n_3(z)$ is the convolution of this profile with the volume weight function $w_3(r) = \Theta(R-r)$. The result of this convolution for $0 \le z \le 2R$ is $n_3(z) = \rho_b \frac{\pi}{3}(2R-z)^2(R+z)$. This expression has a clear geometric meaning: it is the bulk density $\rho_b$ multiplied by the volume of intersection between a test sphere of radius $R$ centered at $z$ and the fluid half-space $z' \ge R$. The weighted densities thus act as "probes" that sense the local geometric environment and smoothly encode packing constraints into the functional .

The most crucial mechanism of any hard-sphere functional is its ability to prevent unphysical overlap. FMT achieves this with remarkable elegance. The free energy density $\Phi$ is constructed with terms that diverge as the local [packing fraction](@entry_id:156220), represented by the weighted density $n_3(\mathbf{r})$, approaches its physical limit. For example, a common form of $\Phi$ contains terms like $-\ln(1-n_3)$ and $(1-n_3)^{-2}$. As $n_3(\mathbf{r}) \to 1^-$, $\Phi \to +\infty$. This means the free energy cost to create a configuration with no available free volume is infinite. In the context of the variational principle, even a very strong external attraction (e.g., from a highly charged electrode) cannot overcome this infinite penalty. The Euler-Lagrange equations, which determine the equilibrium density, include the functional derivative $\delta F_{\text{ex}}^{\text{hs}} / \delta \rho_i(\mathbf{r})$, which acts as a hard-sphere excess chemical potential. This term diverges to $+\infty$ as $n_3(\mathbf{r}) \to 1^-$, providing a powerful repulsive force that balances any attraction and ensures the [density profile](@entry_id:194142) remains physically realistic at all points in space .

### Connection to Liquid State Theory

The cDFT framework is deeply connected to traditional liquid state theories, such as those based on [integral equations](@entry_id:138643). This connection is made explicit through the **[direct correlation function](@entry_id:158301)**. The two-body [direct correlation function](@entry_id:158301), $c_{ij}^{(2)}(\mathbf{r}, \mathbf{r}')$, is formally defined as the second functional derivative of the excess [free energy functional](@entry_id:184428) with respect to the densities:
$$
c_{ij}^{(2)}(\mathbf{r}, \mathbf{r}') = -\beta \frac{\delta^2 F_{\text{ex}}[\{\rho_k\}]}{\delta \rho_i(\mathbf{r}) \delta \rho_j(\mathbf{r}')} \quad \text{where } \beta = (k_{\mathrm{B}}T)^{-1}
$$
For a homogeneous bulk fluid, this function depends only on the separation, $c_{ij}(\mathbf{r}-\mathbf{r}')$. It describes the "direct" part of the correlation between two particles, mediated by the interaction potential. The total correlation, described by the total correlation function $h_{ij}(r) = g_{ij}(r) - 1$, where $g_{ij}(r)$ is the [radial distribution function](@entry_id:137666), also includes indirect paths mediated by chains of other particles.

The **Ornstein-Zernike (OZ) equation** provides the exact relation between the direct and total correlation functions. For a multi-component bulk fluid, the OZ equation reads:
$$
h_{ij}(\mathbf{r}) = c_{ij}(\mathbf{r}) + \sum_{\ell} \rho_{\ell} \int c_{i\ell}(\mathbf{r}-\mathbf{r}') h_{\ell j}(\mathbf{r}') \,d\mathbf{r}'
$$
This relation is fundamental. In cDFT, if one has an approximation for $F_{\text{ex}}$, one can compute $c_{ij}$ by differentiation and then solve the OZ equation for $h_{ij}$ and the pair structure. Conversely, integral equation theories start with an approximation (a [closure relation](@entry_id:747393)) for $c_{ij}$ and use the OZ equation. Thus, cDFT provides a route to constructing and understanding the [direct correlation function](@entry_id:158301) from a free energy perspective .

### A Complete Functional: The Primitive Model Example

By combining these principles, we can construct a state-of-the-art functional for the primitive model of a multi-component electrolyte. The [grand potential functional](@entry_id:144711) combines the exact ideal gas term, the FMT functional for hard-sphere repulsion, and the mean-field functional for electrostatics (after regularization). The full expression provides a complete and computationally tractable model for studying a wide range of electrochemical phenomena :
$$
\Omega[\{\rho_i\}] = F_{\text{id}}[\{\rho_i\}] + F_{\text{ex}}^{\text{hs}}[\{\rho_i\}] + F_{\text{el}}^{\text{MF}}[\{\rho_i\}] + \sum_i \int \rho_i(\mathbf{r}) \left( V_i^{\text{ext}}(\mathbf{r}) - \mu_i \right) d\mathbf{r}
$$
Each term is explicitly defined as discussed:
-   $F_{\text{id}}[\{\rho_i\}] = k_{\mathrm{B}} T \sum_i \int \rho_i(\mathbf{r})\left[ \ln\left(\Lambda_i^3 \rho_i(\mathbf{r})\right) - 1 \right] d\mathbf{r}$
-   $F_{\text{ex}}^{\text{hs}}[\{\rho_i\}] = k_{\mathrm{B}} T \int \Phi(\{n_\alpha(\mathbf{r})\}) \,d\mathbf{r}$ (using the FMT construction)
-   $F_{\text{el}}^{\text{MF}}[\{\rho_i\}] = \frac{1}{2}\int \rho_c(\mathbf{r})\,\phi(\mathbf{r})\,d\mathbf{r}$ (with the implicit understanding of [self-energy correction](@entry_id:754667))

Minimizing this functional yields the equilibrium density profiles, from which all thermodynamic and structural properties of the electrolyte interface can be derived. The principles and mechanisms detailed in this chapter provide the foundation for both understanding these models and for developing more advanced theories that go beyond the [mean-field approximation](@entry_id:144121) to include electrostatic correlations.