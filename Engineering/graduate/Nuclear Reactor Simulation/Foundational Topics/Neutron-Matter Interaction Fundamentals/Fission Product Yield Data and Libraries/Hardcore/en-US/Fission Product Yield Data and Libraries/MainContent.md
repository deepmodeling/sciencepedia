## Introduction
In the heart of a nuclear reactor, the fission process creates not only energy but also a vast array of new nuclides known as fission products. These products are far from inert; they profoundly influence reactor safety, performance, and the long-term characteristics of spent fuel. To accurately simulate and predict reactor behavior, from short-term power transients to long-term fuel depletion, a precise understanding of the quantity and type of each fission product created is indispensable. This crucial information is quantified in Fission Product Yield (FPY) data libraries, which form the bedrock of modern reactor analysis. This article bridges the gap between fundamental nuclear physics and applied reactor simulation, providing a detailed exploration of FPY data.

Across three chapters, you will gain a multi-faceted understanding of this critical topic. The journey begins with the **Principles and Mechanisms** governing the formation of fission products, detailing their physical origins and the standardized formats used to catalog them. Next, we will explore the extensive **Applications and Interdisciplinary Connections**, demonstrating how FPY data is the linchpin for safety analyses, fuel cycle calculations, and even multi-physics feedback loops. Finally, a series of **Hands-On Practices** will provide opportunities to apply this knowledge to practical problems encountered in the field. We will start by examining the foundational definitions of fission yields and the physical laws that shape them.

## Principles and Mechanisms

Following the introduction to the role of fission products in reactor physics, this chapter delves into the fundamental principles and mechanisms that govern their creation and the formalisms used to represent this information in [nuclear data libraries](@entry_id:1128922). A precise understanding of [fission product yield](@entry_id:1125035) data is indispensable for accurate simulations of fuel depletion, decay heat, [reactor kinetics](@entry_id:160157), and radiological source terms. We will begin with the foundational definitions of fission yields, proceed to the underlying nuclear physics that shapes their distributions, discuss their practical representation in data libraries, and conclude with the advanced topic of uncertainty quantification through covariance data.

### Fundamental Definitions of Fission Yield

The production of fission products is an inherently [stochastic process](@entry_id:159502). For a given fission event—characterized by a specific fissioning nuclide and incident neutron energy—a vast spectrum of nuclide pairs can be formed. Fission product yield data provides the probability distribution for the formation of these nuclides.

#### Independent and Cumulative Yields

Two primary definitions are used to quantify fission yields, distinguished by the timescale on which they are considered .

The **independent fission yield**, denoted $y_{i}^{\text{ind}}$, represents the expected number of atoms of a specific nuclide $i$ produced directly per fission event. This quantity is evaluated at the instant immediately following the emission of prompt neutrons from the nascent fission fragments, but *before* any subsequent radioactive decay (e.g., $\beta$-decay) of the fragments themselves. It is the primary, direct source term from fission. The evolution of the concentration $N_i$ of a nuclide $i$ in a reactor is governed by a balance equation that includes sources and sinks:

$ \frac{dN_i}{dt} = \sum_{f} y_{f,i}^{\text{ind}} R_{f} + \sum_{j \neq i} \lambda_j b_{j \to i} N_j - (\lambda_i + \sigma_{a,i} \phi) N_i + \dots $

Here, the first term on the right-hand side represents the direct production of nuclide $i$ from the fission of all fissile nuclides $f$, where $y_{f,i}^{\text{ind}}$ is the [independent yield](@entry_id:1126457) and $R_f$ is the fission rate of nuclide $f$. The second term accounts for the production of $i$ via the [radioactive decay](@entry_id:142155) of its precursors $j$, with decay constant $\lambda_j$ and branching fraction $b_{j \to i}$. The third term accounts for losses of nuclide $i$ through its own decay ($\lambda_i$) and neutron absorption ($\sigma_{a,i}\phi$). A rigorous depletion calculation must use independent yields for the fission source term and explicitly solve the full network of decay equations to correctly model the time-dependent build-up from precursors.

The **cumulative fission yield**, denoted $y_{i}^{\text{cum}}$, represents the total expected number of atoms of nuclide $i$ produced per fission event after an infinite time, assuming no neutron flux. It is the sum of the [independent yield](@entry_id:1126457) of nuclide $i$ and the independent yields of all its precursors in the isobaric (constant [mass number](@entry_id:142580)) decay chain. For a nuclide $i$ that is the endpoint of a decay chain starting from precursors $j_1, j_2, \dots$:

$ y_{i}^{\text{cum}} = y_{i}^{\text{ind}} + \sum_{k} (\text{branching fractions}) \times y_{j_k}^{\text{ind}} $

Using cumulative yields directly as the fission source term in a depletion calculation is an approximation that implicitly assumes all precursors decay instantaneously into the nuclide of interest. This approach is only valid for very long-lived or stable nuclides whose precursors are all extremely short-lived compared to the simulation timescale, and is generally avoided in modern high-fidelity codes . Fission yields are fundamental nuclear data, properties of a specific fission reaction ($t, E$), and are not dependent on the reactor's operational history, such as flux level or [irradiation](@entry_id:913464) time.

#### Normalization and Conservation Principles

For the vast majority of fission events in a reactor, a single nucleus splits into two fragments, a process known as **[binary fission](@entry_id:136239)**. The contribution from ternary fission (producing three fragments, often including a light particle like an alpha particle) is typically negligible for inventory calculations. Based on the conservation of [baryons](@entry_id:193732), the production of exactly two fragments per fission event imposes a powerful constraint on the yields. The sum of the independent yields over all possible primary fission products must equal two :

$ \sum_{i} y_{i}^{\text{ind}} = 2 $

This normalization is a fundamental check on the physical consistency of any evaluated fission yield data set.

A similar conservation principle applies to cumulative yields. If we assume that every [radioactive decay](@entry_id:142155) chain initiated by a primary fission fragment eventually terminates in a stable or very long-lived nuclide, and no nuclei are lost in the process, then the total number of nuclei must be conserved throughout the decay process. This implies that the sum of the cumulative yields over all nuclides must also be equal to two. We can demonstrate this formally . Let $P_{j \to i}$ be the probability that a primary fragment $j$ ultimately decays into a final nuclide $i$. The [cumulative yield](@entry_id:1123290) of nuclide $i$ is the sum of contributions from all primary fragments that can lead to it:

$ y_{i}^{\text{cum}} = \sum_{j} P_{j \to i} \, y_{j}^{\text{ind}} $

Summing over all final nuclides $i$:

$ \sum_{i} y_{i}^{\text{cum}} = \sum_{i} \sum_{j} P_{j \to i} \, y_{j}^{\text{ind}} = \sum_{j} y_{j}^{\text{ind}} \left( \sum_{i} P_{j \to i} \right) $

The inner sum, $\sum_{i} P_{j \to i}$, is the total probability that an initial nucleus $j$ decays into *any* final nucleus. By conservation of nuclei, this sum must be exactly one. Therefore:

$ \sum_{i} y_{i}^{\text{cum}} = \sum_{j} y_{j}^{\text{ind}} = 2 $

This elegant result confirms that the normalization to two fragments is preserved when transitioning from the [independent yield](@entry_id:1126457) basis to the [cumulative yield](@entry_id:1123290) basis.

### The Physics of Fission Yield Distributions

The observed patterns in fission product yields—the familiar double-humped [mass distribution](@entry_id:158451), the specific charge distributions for each mass chain, and the partitioning into isomeric states—are direct consequences of the underlying [nuclear structure](@entry_id:161466) and dynamics of the fissioning system.

#### Mass Distribution: The Role of Shell Effects and Excitation Energy

The most striking feature of low-energy fission (e.g., thermal neutron fission of $^{235}$U) is its predominantly **asymmetric mass split**. Instead of breaking into two nearly equal halves, the nucleus preferentially splits into a lighter fragment with [mass number](@entry_id:142580) $A \approx 95$ and a heavier fragment with $A \approx 140$. This phenomenon cannot be explained by simple macroscopic models.

The **[liquid drop model](@entry_id:141747)**, which treats the nucleus as a charged, deformable fluid drop, predicts that symmetric fission should be energetically favored to minimize surface energy. The observed asymmetry is a profound manifestation of quantum mechanical **shell effects** . As the nucleus deforms, nascent fragments begin to form. The [total potential energy](@entry_id:185512) of the system is a sum of the macroscopic liquid-drop energy and a microscopic [shell correction](@entry_id:754768) term, $\delta E_{\text{shell}}$. This correction is strongly negative (i.e., stabilizing) for nuclei with proton or neutron numbers near "[magic numbers](@entry_id:154251)" (e.g., 50, 82). For a heavy actinide like $^{236}$U$^*$, asymmetric shapes that allow the heavy fragment to approach the doubly magic configuration of $^{132}$Sn ($Z=50, N=82$) are energetically favored. This creates a deep "valley" in the potential energy surface, guiding the fissioning system towards an asymmetric split.

This picture also explains the strong **energy dependence** of the [mass distribution](@entry_id:158451) . As the incident neutron energy increases, the excitation energy $E^*$ of the [compound nucleus](@entry_id:159470) rises. This is analogous to increasing the **[nuclear temperature](@entry_id:157828)** $T$ (a simple Fermi gas model suggests $E^* \propto T^2$). At higher temperatures, nucleons are excited across the shell gaps, effectively "washing out" the shell structure. As the stabilizing influence of $\delta E_{\text{shell}}$ diminishes, the macroscopic liquid-drop energy, which favors symmetry, becomes dominant. Consequently, as incident energy increases, the "valley" between the two asymmetric peaks fills in, and the yield of symmetric fission products increases. Simultaneously, the increased thermal energy broadens the distribution around the peaks. A statistical model based on the probability of occupying a certain shape configuration, $P(\alpha) \propto \exp(-U(\alpha)/T)$, where $\alpha$ is a mass-asymmetry coordinate and $U(\alpha)$ is the potential energy, effectively captures both the trend towards symmetry and the broadening of the mass peaks with increasing excitation energy.

#### From Pre-Neutron Fragments to Post-Neutron Products

The fission fragments are initially formed in highly [excited states](@entry_id:273472) and de-excite by emitting prompt neutrons. The yields measured immediately after scission are called **pre-neutron-emission yields**, while the yields of the final products, which are what are typically measured and cataloged, are **post-neutron-emission yields**. The number of neutrons emitted, $\nu_{\text{prompt}}$, is itself a function of the fragment's mass, exhibiting a characteristic "sawtooth" shape.

To relate the post-neutron mass $A_{\text{post}}$ to the pre-neutron mass $A_{\text{pre}}$, one must account for this mass-dependent neutron emission, $\nu_{\text{prompt}}(A_{\text{pre}})$ . The expected post-neutron [mass number](@entry_id:142580), $E[A_{\text{post}}]$, can be derived from the pre-neutron [mass distribution](@entry_id:158451) $Y_{\text{pre}}(A)$ using the law of total expectation:

$ E[A_{\text{post}}] = \sum_{A} E[A_{\text{post}} | A_{\text{pre}}=A] \cdot Y_{\text{pre}}(A) $

Given a pre-neutron mass $A$, the expected post-neutron mass is simply $A - \nu_{\text{prompt}}(A)$. Therefore, the final relation is:

$ E[A_{\text{post}}] = \sum_{A} [A - \nu_{\text{prompt}}(A)] Y_{\text{pre}}(A) $

For example, considering a hypothetical light-fragment pre-neutron yield distribution peaked at $A=95$ with $Y_{\text{pre}}(94)=0.3$, $Y_{\text{pre}}(95)=0.5$, $Y_{\text{pre}}(96)=0.2$, and a corresponding neutron emission of $\nu_{\text{prompt}}(94)=2.8$, $\nu_{\text{prompt}}(95)=2.5$, $\nu_{\text{prompt}}(96)=2.2$, the expected post-neutron mass would be calculated as:

$ E[A_{\text{post}}] = (94-2.8) \times 0.3 + (95-2.5) \times 0.5 + (96-2.2) \times 0.2 = 92.37 $

This illustrates how the final measured [mass distribution](@entry_id:158451) is a convolution of the initial pre-neutron [mass distribution](@entry_id:158451) and the physics of prompt neutron emission.

#### Isotopic Charge Distribution

For any given mass chain $A$, the total yield $Y(A)$ is distributed among several isobars (nuclides with the same $A$ but different [atomic number](@entry_id:139400) $Z$). The conditional probability $P(Z|A)$ that a fragment of mass $A$ has charge $Z$ is known as the **[charge distribution](@entry_id:144400)**.

A sophisticated semi-empirical model for this distribution is the **Wahl $Z_p$ model** . This model posits that for a fixed $A$, the independent yields of isobars follow a Gaussian distribution centered around a **most probable charge**, $Z_p(A)$. This distribution is modulated by factors accounting for the enhanced stability of nuclei with even numbers of protons or neutrons (odd-even effects).

The most probable charge $Z_p(A)$ is based on the Unchanged Charge Distribution (UCD) hypothesis, which assumes the fragments have the same proton-to-nucleon ratio as the fissioning [compound nucleus](@entry_id:159470) $(Z_F, A_F)$. However, it includes a crucial correction term $\Delta(A)$ for charge polarization, an effect where the light fragment tends to have a slightly higher charge density:

$ Z_p(A) = \frac{Z_F}{A_F} A + \Delta(A) $

The full [charge distribution](@entry_id:144400) model allows evaluators to estimate the nuclide-specific [independent yield](@entry_id:1126457) $Y(Z,A)$ from the mass yield $Y(A)$ using the fundamental relation of conditional probability:

$ Y(Z,A) = Y(A) \cdot P(Z|A) $

where the distribution $P(Z|A)$ is normalized such that $\sum_Z P(Z|A) = 1$ for each [mass number](@entry_id:142580) $A$. This ensures that $\sum_Z Y(Z,A) = Y(A)$, preserving consistency.

#### Partitioning Yields into Isomeric States

Many fission products can be formed in either their ground state or one or more long-lived [excited states](@entry_id:273472) known as **isomeric (or metastable) states**. The [independent yield](@entry_id:1126457) for a nuclide $(Z,A)$ is therefore a sum of yields to its ground state, $Y(Z,A,g)$, and all its isomeric states, $Y(Z,A,m)$. The partitioning of yield between these states is quantified by the **isomeric yield ratio (IR)** . For a nuclide with one isomer, it is defined as:

$ \text{IR} \equiv \frac{Y(Z,A,m)}{Y(Z,A,m)+Y(Z,A,g)} $

This ratio is determined by the de-excitation process of the primary fission fragment. Fragments are formed with high excitation energy and significant angular momentum. They first de-excite by emitting prompt neutrons, and then undergo a **gamma-ray cascade** to shed the remaining energy and angular momentum. According to angular momentum [selection rules](@entry_id:140784), each gamma transition can only change the [nuclear spin](@entry_id:151023) $J$ by a small amount (typically $|\Delta J| \le 2$).

The outcome of the cascade depends on two main factors:
1.  **Initial Angular Momentum:** Fragments formed with higher initial angular momentum are more likely to become "trapped" in a high-spin isomeric state during the cascade. Therefore, increasing the average initial spin of the fragments tends to increase the isomeric yield ratio for a high-[spin isomer](@entry_id:755230).
2.  **Gamma-ray Excitation Energy:** A higher initial excitation energy (after neutron emission) allows for a longer gamma cascade (more transitions). A longer cascade provides more opportunities for the nucleus to shed angular momentum and reach the low-spin ground state. Consequently, for a high-[spin isomer](@entry_id:755230), increasing the available gamma-ray energy tends to *decrease* the isomeric yield ratio.

These dependencies mean that the isomeric yield ratio is, in general, a function of the incident neutron energy that caused the fission, as higher energy fission leads to fragments with different distributions of spin and excitation energy.

### Representation in Nuclear Data Libraries

The physical principles described above are translated into numerical data and stored in standardized formats for use in simulation codes. The most widely used format is the **Evaluated Nuclear Data File (ENDF)**.

#### The ENDF-6 Format for Fission Yield Data

In the ENDF-6 format, [fission product yield](@entry_id:1125035) data is stored in **File 8 (MF=8)**, which is designated for radioactivity and fission-product yield data . Within this file, different types of data are distinguished by a **Reaction Type (MT) number**:
*   **MT=454**: Contains **independent** fission product yields.
*   **MT=459**: Contains **cumulative** fission product yields.

Each section (a specific MF/MT combination) is associated with a particular **fissioning parent nuclide** (e.g., $^{235}\text{U}$, $^{239}\text{Pu}$). The data within the section is provided for one or more discrete **incident neutron energies** (e.g., $0.0253 \text{ eV}$ for thermal, or values representing fast or high-energy spectra).

The yield data for each energy point consists of a list of fission products. Each product nuclide is identified by a numerical code :
*   **ZAP**: An integer given by $1000 \times Z + A$, where $Z$ is the [atomic number](@entry_id:139400) and $A$ is the [mass number](@entry_id:142580).
*   **LISO**: An isomeric state flag, where $LISO=0$ indicates the ground state and $LISO>0$ indicates a metastable state.

For each listed product, the file provides the yield value and its uncertainty. The independent yields within each energy subsection are evaluated and processed to conform to the [normalization condition](@entry_id:156486) $\sum y_i^{\text{ind}} = 2$.

#### Distinguishing Yield Data from Decay Data

Crucially, MF=8 also contains [radioactive decay](@entry_id:142155) data, which includes half-lives, decay modes, and branching ratios for unstable nuclides. This decay data is identified by **MT=457**. A common source of error in processing ENDF files is confusing yield data with decay data. The distinction is unambiguous :
*   **Yield Data (MT=454, 459):** Is keyed to the *fissioning parent* nuclide and is dependent on *incident neutron energy*.
*   **Decay Data (MT=457):** Is keyed to the *decaying product* nuclide and is an intrinsic property, hence it has *no incident energy dependence*.

A data processing code must therefore use the parent nuclide, the incident energy, and the MT number to correctly retrieve the desired fission yield data.

#### Isomeric Yield Representation

Data libraries must also handle the distinction between yields for a nuclide as a whole and yields for its specific states. The **elemental yield** $Y(Z,A)$ is the total yield for a given nuclide, summed over all its isomeric states. The **state-resolved yield** $Y(Z,A,m)$ is the yield into a specific state $m$ .

These are related by **isomeric ratios**, $R_m(Z,A)$, which represent the fraction of the total elemental yield that goes to state $m$:

$ Y(Z,A,m) = R_m(Z,A) \cdot Y(Z,A) $

For this relationship to be consistent, the isomeric ratios for a given nuclide must sum to one: $\sum_m R_m(Z,A) = 1$. This ensures that the global normalization is preserved when moving between representations: $\sum_{Z,A,m} Y(Z,A,m) = \sum_{Z,A} Y(Z,A) = 2$. If a depletion code tracks isomeric states explicitly but is only provided with elemental yield data, it must use a consistent set of isomeric ratios to partition the source term among the ground and [metastable states](@entry_id:167515).

### Fission Yield Covariance Data

The fission yield values published in evaluated libraries are not known with perfect precision; they are mean values of a distribution. For uncertainty quantification (UQ), it is essential to know not only the variance of each individual yield but also the correlations between the yields of different nuclides. This information is encoded in a **[fission product yield](@entry_id:1125035) covariance matrix**, $\mathbf{C}$.

#### The Covariance Matrix and Its Properties

Let $\mathbf{Y}$ be the vector of independent yields for $N$ different nuclides. The covariance matrix is an $N \times N$ matrix whose elements are $C_{ij} = \text{Cov}(Y_i, Y_j)$. By definition, any covariance matrix must be **symmetric** ($C_{ij} = C_{ji}$) and **positive semidefinite**. Positive semidefiniteness means that the variance of any linear combination of the yields, $\text{Var}(\mathbf{a}^T \mathbf{Y}) = \mathbf{a}^T \mathbf{C} \mathbf{a}$, must be non-negative for any vector $\mathbf{a}$ .

#### Constraints Imposed by Normalization and Positivity

The physical constraints on fission yields impose mathematical constraints on the covariance matrix. The most important is the normalization sum rule. If the total yield is constrained to be exactly 2 for *every possible realization* of the yield vector (not just on average), i.e., $\mathbf{1}^T \mathbf{Y} = 2$, then this has a profound impact on the covariance matrix. The variance of the sum must be zero:

$ \text{Var}(\mathbf{1}^T \mathbf{Y}) = \mathbf{1}^T \mathbf{C} \mathbf{1} = 0 $

More strongly, if the sum is constant for every realization, it can be shown that the sum of each row and each column of the covariance matrix must be zero :

$ \mathbf{C} \mathbf{1} = \mathbf{0} \quad \text{and} \quad \mathbf{1}^T \mathbf{C} = \mathbf{0}^T $

This implies that the matrix $\mathbf{C}$ is **singular**, with at least one eigenvalue equal to zero (the corresponding eigenvector being $\mathbf{1}$). This property ensures that if one yield is perturbed upwards, the sum of all other yields must be perturbed downwards by the same amount to maintain the total sum. It is important to note that this does not require all off-diagonal correlations to be negative; positive correlations within a subgroup of nuclides can be balanced by negative correlations with other nuclides.

A second physical constraint is that yields must be non-negative, $Y_i \ge 0$. If one samples yield vectors from a [multivariate normal distribution](@entry_id:267217) defined by $\mathbf{C}$, there is a non-zero probability of obtaining unphysical negative yields. To address this, transformations are sometimes used. A common approach is the **lognormal parameterization**, where the vector of logarithms of the yields, $\mathbf{Z} = \ln \mathbf{Y}$, is modeled as a [multivariate normal distribution](@entry_id:267217). This inherently enforces positivity ($Y_i = \exp(Z_i) > 0$). The covariance matrix of $\mathbf{Y}$ is then induced by the exponential transformation and is distinct from the covariance matrix of $\mathbf{Z}$ . Understanding these mathematical properties is critical for the correct propagation of fission yield uncertainties in reactor analysis.