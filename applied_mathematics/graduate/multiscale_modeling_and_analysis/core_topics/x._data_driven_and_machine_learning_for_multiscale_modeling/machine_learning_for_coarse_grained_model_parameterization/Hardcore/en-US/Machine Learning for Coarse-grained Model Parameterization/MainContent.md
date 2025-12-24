## Introduction
Coarse-grained (CG) modeling is a cornerstone of computational science, enabling the simulation of complex systems over length and time scales inaccessible to high-resolution, atomistic models. The central challenge in this multiscale approach lies in parameterizing the CG model—defining the effective interactions that accurately represent the underlying fine-grained physics. Traditional CG potentials are often based on simple, pairwise-additive functional forms that fail to capture the true complexity of the effective energy landscape. This landscape, known as the Potential of Mean Force (PMF), is an inherently many-body, state-dependent free energy that also gives rise to complex dynamical effects. This article addresses how machine learning (ML) provides a powerful new paradigm to overcome these limitations by creating highly expressive and physically consistent CG models directly from data.

In the chapters that follow, we will embark on a comprehensive exploration of this rapidly evolving field. We begin in **Principles and Mechanisms** by establishing the statistical mechanical foundations of coarse-graining, dissecting the nature of the PMF, and understanding the dynamical challenges described by the Mori-Zwanzig formalism. This theoretical groundwork will highlight why ML methods are not just useful but necessary. Next, in **Applications and Interdisciplinary Connections**, we will survey the practical implementation of these ideas, from bottom-up parameterization techniques like [force matching](@entry_id:749507) and [relative entropy minimization](@entry_id:754220) in molecular simulation to the analogous problem of subgrid-scale closure in climate and fluid dynamics. Finally, the **Hands-On Practices** section provides an opportunity to engage directly with key concepts, offering practical exercises in enforcing physical symmetries, implementing constraints, and ensuring the [numerical stability](@entry_id:146550) of learned models. Through this journey, you will gain a deep, principled understanding of how to leverage machine learning to build the next generation of coarse-grained models.

## Principles and Mechanisms

The parameterization of coarse-grained (CG) models is fundamentally an act of translating information from a high-resolution, fine-grained (FG) system to a lower-resolution representation. The success of this translation hinges on a deep understanding of the statistical mechanical principles that govern the relationship between scales. This chapter elucidates these core principles, establishing the theoretical foundation upon which [robust machine learning](@entry_id:635133) (ML) parameterization strategies are built. We will explore the nature of coarse-grained energy landscapes, the origin of many-body and [non-conservative forces](@entry_id:164833), and the essential physical constraints, such as symmetry and [thermodynamic consistency](@entry_id:138886), that any valid CG model must satisfy.

### The Coarse-Graining Map and the Potential of Mean Force

The first step in any coarse-graining procedure is the definition of a **coarse-graining map**, a mathematical rule that projects the vast configuration space of the fine-grained system onto a simpler, lower-dimensional space of coarse-grained variables. Let the state of an atomistic system be described by the coordinates $q \in \mathbb{R}^{3N}$ of its $N$ atoms. A CG map $\xi: \mathbb{R}^{3N} \to \mathbb{R}^m$ defines a set of $m$ coarse variables $x = \xi(q)$, where typically $m \ll 3N$.

This map is generally a **many-to-one** function: a multitude of distinct atomistic configurations $q$ will correspond to the exact same coarse-grained configuration $x$. The map can be **deterministic**, where $x$ is a fixed function of $q$ (e.g., the center of mass of a group of atoms), or it can be **stochastic**, specified by a [conditional probability distribution](@entry_id:163069), or Markov kernel, $q(x|q')$ . A stochastic map, which assigns a distribution of possible coarse states to a single fine-grained state, can be viewed as a deterministic function of both the fine-grained state and an [auxiliary random variable](@entry_id:270091), such as an independent random seed .

Once the CG variables $x$ are defined, the central question becomes: what is the effective energy landscape that governs their behavior? In the framework of equilibrium statistical mechanics, this landscape is the **Potential of Mean Force (PMF)**. The PMF, denoted $U_{\mathrm{PMF}}(x)$, is the equilibrium free energy of the system when the coarse variables are constrained to the value $x$. For a system in the [canonical ensemble](@entry_id:143358) at an inverse temperature $\beta = 1/(k_B T)$, the [equilibrium probability](@entry_id:187870) distribution of the microstates $q$ is $p_{atom}(q) \propto \exp(-\beta U(q))$, where $U(q)$ is the atomistic potential energy. The [marginal probability](@entry_id:201078) density of observing the CG variables at a specific configuration $x$ is obtained by integrating over all microstates consistent with that constraint:

$$
p(x) = \int \delta(x - \xi(q)) p_{atom}(q) dq \propto \int \delta(x - \xi(q)) e^{-\beta U(q)} dq
$$

The PMF is defined as the potential whose Boltzmann factor gives this [marginal probability](@entry_id:201078) density, up to a [normalization constant](@entry_id:190182):

$$
p(x) \propto e^{-\beta U_{\mathrm{PMF}}(x)}
$$

By combining these definitions, we arrive at the formal expression for the PMF as a constrained free energy :

$$
U_{\mathrm{PMF}}(x) = -k_B T \ln \left( \int e^{-\beta U(q)} \delta(x - \xi(q)) dq \right) + C
$$

where $C$ is an arbitrary additive constant. The negative gradient of the PMF, $-\nabla_x U_{\mathrm{PMF}}(x)$, defines the **mean force** acting on the coarse variables. This force is the [conditional expectation](@entry_id:159140) of the true atomistic force, projected onto the coarse coordinates, averaged over all microstates $q$ that map to the coarse state $x$ . A crucial point is that, by its very definition as the gradient of a [scalar potential](@entry_id:276177), the mean force field is always conservative (i.e., its curl is zero), regardless of whether the underlying CG map $\xi(q)$ is linear or nonlinear.

For a homogeneous and isotropic fluid of [identical particles](@entry_id:153194), a common coarse-grained descriptor is the distance $r$ between two particles. The corresponding structural information is captured by the **radial distribution function (RDF)**, $g(r)$. In this context, the PMF between the two particles, often denoted $w(r)$, can be directly related to the RDF. The probability of finding two particles at a separation $r$ is proportional to both $g(r)$ and $\exp(-\beta w(r))$. By enforcing the physical convention that the [potential of mean force](@entry_id:137947) goes to zero at infinite separation, where the particles are uncorrelated and $g(r) \to 1$, we can establish an exact relationship :

$$
U_{\mathrm{PMF}}(r) = -k_B T \ln g(r)
$$

This fundamental equation links the microscopic structure of a fluid, an observable quantity, to its effective interaction free energy. As we will see, this relationship is both a cornerstone of [liquid-state theory](@entry_id:182111) and a source of significant challenges in parameterization. For example, if a simulation yields a CG [radial distribution function](@entry_id:137666) of the form $g(r) = \exp(-a \exp(-(r/\sigma)^2))$, this relationship immediately provides the corresponding PMF as $U_{\mathrm{PMF}}(r) = a k_B T \exp(-(r/\sigma)^2)$ .

### The Representability Challenge: Many-Body and State-Dependent Potentials

A central challenge in coarse-graining is that the PMF is a far more complex object than typical atomistic potentials. Even if the underlying fine-grained potential $U(q)$ is a simple sum of pairwise interactions, the resulting $U_{\mathrm{PMF}}(x)$ is, in general, a **[many-body potential](@entry_id:197751)** .

This emergent many-body character arises directly from the act of [marginalization](@entry_id:264637). The PMF between two coarse-grained sites, say $x_I$ and $x_J$, is not just their direct interaction. It is a free energy, which includes the averaged effects of all the integrated-out degrees of freedom. The interaction between sites $I$ and $J$ is mediated by the surrounding "sea" of other particles. The configuration of this medium is, in turn, influenced by the presence of a third coarse site, $x_K$. Consequently, the effective interaction between $I$ and $J$ depends on the position of $K$, which is the definition of a [three-body interaction](@entry_id:1133110). This logic extends to all orders, coupling all coarse sites. Mathematically, the logarithm in the definition of the PMF acts as a generator of connected correlation functions, which correspond to the irreducible two-body, three-body, and higher-order terms in a [many-body expansion](@entry_id:173409) of the potential .

The approximation that the PMF is pairwise additive is therefore a severe simplification. This has profound implications for common parameterization schemes like the **Inverse Boltzmann (IB) method**. The IB method uses the relation derived above to define an effective pair potential, $U_{IB}(r) \equiv -k_B T \ln g(r)$. The hope is that this potential, when used in a simulation, will reproduce the target structure $g(r)$. However, this is only an approximation. The PMF, $w(r) = -k_B T \ln g(r)$, is not equal to the true underlying pair potential, $u(r)$, at finite densities. The **Yvon-Born-Green (YBG) hierarchy** from [liquid-state theory](@entry_id:182111) shows that the gradient of the PMF is the sum of the gradient of the direct pair potential and an integral term involving the three-body correlation function, $g^{(3)}$. This integral term, which represents the indirect force mediated by the fluid, vanishes only in the zero-density limit ($\rho \to 0$) or in a trivial two-particle system. Therefore, the IB method is exact only under these conditions . At any realistic density, $U_{IB}(r)$ is not the true [pair potential](@entry_id:203104), and using it in a new simulation will not perfectly reproduce the target $g(r)$.

This issue is formalized by **Henderson's theorem**, which states that for a system known to be described by a pairwise-additive Hamiltonian, the pair structure $g(r)$ at a fixed temperature and density uniquely determines the pair potential $u(r)$ (up to an irrelevant constant). The key assumption is [pairwise additivity](@entry_id:193420). Since coarse-graining generates an exact [effective potential](@entry_id:142581) (the PMF) that is inherently many-body, the premise of Henderson's theorem is violated. There is no guarantee that *any* pair potential can reproduce the $g(r)$ generated by a many-body system . In practice, [iterative methods](@entry_id:139472) like Iterative Boltzmann Inversion (IBI) use the IB potential as a starting point and refine it to find the *effective* pair potential that best reproduces the target $g(r)$ at a specific state point .

Furthermore, as a free energy, the PMF is inherently a function of the thermodynamic state, i.e., $U_{\mathrm{PMF}}(x; T, \rho)$. The temperature dependence can be made explicit through the [fundamental thermodynamic relation](@entry_id:144320) $A = E - TS$, where $A$ is the Helmholtz free energy. Since the PMF is a conditional free energy, it can be decomposed into a conditional energy $E(x)$ and a [conditional entropy](@entry_id:136761) $S(x)$:

$$
U_{\mathrm{PMF}}(x; T) = E(x) - T S(x) + C(T)
$$

where $C(T)$ is an $x$-independent function of temperature . This decomposition shows that the PMF is linear in temperature, with the slope determined by the system's entropy at a given coarse configuration. This has critical implications for the **transferability** of CG models. A potential parameterized at one temperature will not be accurate at another unless this explicit temperature dependence is built into the model form. A purely [pairwise potential](@entry_id:753090) derived from structure matching at one state point is an [effective potential](@entry_id:142581) that implicitly averages over many-body and entropic effects specific to that state point, and is thus generally not transferable [@problem_id:3776298, 3776355].

### The Dynamics Challenge: Non-Conservative and Memory Effects

While the PMF correctly describes the [equilibrium probability](@entry_id:187870) distribution of the coarse variables, using it as the potential in a simple dynamical model is, in general, incorrect. The dynamics of the CG variables are coupled to the fast, integrated-out degrees of freedom, leading to non-trivial effects that are not captured by a purely conservative potential.

The **Mori-Zwanzig (MZ) [projection operator](@entry_id:143175) formalism** provides a rigorous framework for deriving the exact equation of motion for a set of coarse variables . Starting from the underlying Hamiltonian dynamics of the full system, the MZ formalism yields a **Generalized Langevin Equation (GLE)**. The effective force in the GLE is composed of three distinct terms :

1.  **The Mean Force**: This is the [conservative force](@entry_id:261070), given by $-\nabla_x U_{\mathrm{PMF}}(x)$, which we have already discussed. It represents the averaged force on the coarse variables.

2.  **The Memory Term**: This is a dissipative or friction force that is non-local in time. It takes the form of a [convolution integral](@entry_id:155865) over the past history of the coarse variables' velocities: $\int_0^t K(\tau) v(t-\tau) d\tau$. The function $K(\tau)$ is the **[memory kernel](@entry_id:155089)**, and its presence means the system's evolution is non-Markovian—its future depends not just on the present, but on its past. This term represents the systematic drag the slow variables experience as they move through the fast degrees of freedom.

3.  **The Fluctuating Force**: This is a stochastic force, $R(t)$, that represents the random kicks on the slow variables from the thermal motion of the fast variables. By construction, this force is "orthogonal" to the coarse variables, meaning it has [zero correlation](@entry_id:270141) with them at the initial time.

A crucial aspect of the GLE is the **Fluctuation-Dissipation Theorem (FDT)**. This theorem states that the dissipative memory kernel $K(\tau)$ and the statistical properties of the fluctuating force $R(t)$ are not independent. They are intimately linked by the relation $\langle R(t) R(t')^T \rangle = k_B T K(|t-t'|)$. This theorem is a statement of detailed balance at the microscopic level: the energy dissipated by the friction must, on average, be replenished by the random force to maintain the system in [thermodynamic equilibrium](@entry_id:141660) at the correct temperature .

A purely [conservative dynamics](@entry_id:196755), such as Hamiltonian dynamics with the PMF as the potential, is incorrect because it completely neglects both the memory and fluctuating forces . Only in the specific case of significant **time-scale separation**—where the fast variables decorrelate much more quickly than the [characteristic time scale](@entry_id:274321) of the slow variables—can the memory kernel be approximated as a Dirac [delta function](@entry_id:273429), $K(\tau) \approx 2\Gamma \delta(\tau)$. In this **Markovian limit**, the GLE simplifies to the familiar overdamped Langevin equation:

$$
\dot{x} = -\Gamma^{-1} \nabla_x U_{\mathrm{PMF}}(x) + \sqrt{2 k_B T \Gamma^{-1}}\,\eta(t)
$$

where $\eta(t)$ is white noise. Only under this approximation does the PMF become the correct potential to use in a standard Langevin simulation to reproduce both equilibrium and (approximate) dynamical properties .

### Principles for Machine Learning Parameterization

The complexities outlined above—[many-body interactions](@entry_id:751663), state-point dependence, and [non-conservative forces](@entry_id:164833)—motivate the use of machine learning to create highly expressive and physically consistent coarse-grained models. The following principles must guide the design and training of such models.

#### Symmetry Constraints

Any ML potential intended to model an isolated physical system must respect the fundamental symmetries of physics. The potential energy must be invariant to rigid-body motions (translations and rotations) of the entire system. This symmetry is described by the Euclidean group $E(3)$. For a potential $U(x)$ depending on particle coordinates $x = (x_1, \dots, x_N)$, this means $U(g \cdot x) = U(x)$ for any rotation $R$ and translation $t$ that constitute the group action $g$. This invariance implies that the potential can only be a function of internal coordinates, such as inter-particle distances, angles, and dihedrals, which are themselves invariant.

The forces, being the negative gradient of the potential, $F_{\mathrm{CG}}(x) = -\nabla_x U(x)$, must transform **equivariantly**. This means that if the system is rotated, the force vectors must rotate along with it: $F_{\mathrm{CG}}(g \cdot x) = (I_N \otimes R) F_{\mathrm{CG}}(x)$. These symmetry constraints have two immediate consequences, often known as Noether's theorem for continuous symmetries:
1.  **Translational Invariance** implies that the sum of all forces on the system must be zero: $\sum_i F_i(x) = 0$.
2.  **Rotational Invariance** implies that the total torque on the system must be zero: $\sum_i x_i \times F_i(x) = 0$.

ML architectures, such as Graph Neural Networks (GNNs) built on invariant features, are designed to hard-code these symmetries, ensuring physically plausible models by construction .

#### Thermodynamic Consistency and Transferability

To build transferable models, ML architectures must be able to represent the state-point dependence of the PMF. A powerful strategy is to design the model to explicitly reflect the thermodynamic structure $U_{\mathrm{PMF}}(x; T) = E(x) - T S(x) + C(T)$. An ML model of the form $U_{\theta}(x;T) = A_{\theta}(x) - T B_{\theta}(x) + C_{\theta}(T)$, where separate networks or parametric functions learn the energetic component $A_{\theta}(x)$, the entropic component $B_{\theta}(x)$, and the offset $C_{\theta}(T)$, can learn from data at several temperatures and then interpolate or extrapolate to new temperatures in a thermodynamically consistent manner .

For dynamical models, [thermodynamic consistency](@entry_id:138886) requires adherence to the FDT. An ML model that learns only the mean force is incomplete. An architecture that attempts to learn [non-conservative forces](@entry_id:164833) must represent the dissipation and fluctuation components in a coupled manner. For example, a model could consist of a GNN for the conservative mean force, a [recurrent neural network](@entry_id:634803) to represent the [memory kernel](@entry_id:155089), and a learned stochastic driving term whose covariance is explicitly linked to the output of the memory kernel and the system temperature. Such composite architectures are necessary to capture the physics of the GLE correctly .

#### Identifiability and Model Sloppiness

Finally, a practical consideration in any parameterization is **[identifiability](@entry_id:194150)**: given a set of observational data, can the model parameters be uniquely and precisely determined? We distinguish between two types:

1.  **Structural Identifiability**: This concerns the theoretical uniqueness of parameters in an idealized, noise-free setting. A model is structurally non-identifiable if different sets of parameters produce the exact same observable output. For example, if one tries to determine the friction $\gamma$ and stiffness $k$ of a harmonic system from its normalized autocorrelation function $R(t) = \exp(-(k/\gamma) t)$, only the ratio $k/\gamma$ is identifiable. Any pair $(k, \gamma)$ and $(\alpha k, \alpha \gamma)$ will produce the same $R(t)$, leading to a ridge of equivalent solutions in the [loss landscape](@entry_id:140292). Adding noise to data cannot fix this fundamental ambiguity .

2.  **Practical Identifiability**: This concerns the precision with which parameters can be estimated from finite, noisy data. A model may be structurally identifiable, but if the observational data are not sufficiently sensitive to changes in some parameters or combinations of parameters, it can be practically non-identifiable. This phenomenon, known as **[parameter sloppiness](@entry_id:268410)**, manifests as a [loss landscape](@entry_id:140292) with extremely elongated, narrow valleys. The curvature of the loss function (described by its Hessian matrix, or the Fisher Information Matrix) is very large in some directions ("stiff" parameters) but very small in others ("sloppy" parameters). For instance, if one fits the unnormalized autocorrelation $C(t) = (k_B T/k) \exp(-(k/\gamma) t)$, both $k$ and $\gamma$ are structurally identifiable. However, if the data are restricted to very short times $t \ll \gamma/k$, the model is very insensitive to changes in $\gamma$, leading to a sloppy parameter direction and high uncertainty in its estimated value .

Understanding the [identifiability](@entry_id:194150) of a model given a set of target [observables](@entry_id:267133) is crucial for designing effective parameterization strategies and for quantifying the uncertainty in the resulting CG models. Machine learning parameterization does not escape these fundamental statistical limitations; it is simply a more powerful tool for navigating them.