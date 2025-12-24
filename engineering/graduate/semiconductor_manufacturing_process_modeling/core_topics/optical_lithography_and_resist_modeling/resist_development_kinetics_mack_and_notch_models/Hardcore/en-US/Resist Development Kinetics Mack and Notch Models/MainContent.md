## Introduction
In the precise world of semiconductor manufacturing, [photolithography](@entry_id:158096) stands as the cornerstone technology for patterning [integrated circuits](@entry_id:265543). A critical, yet complex, step in this process is the development of the photoresist, where a latent chemical image is transformed into a physical, three-dimensional structure. To control and optimize this transformation at the nanoscale, engineers and scientists rely on predictive kinetic models. These models are essential for bridging the gap between the invisible pattern of chemical changes within the resist and the final, tangible topography that defines a device. This article delves into two of the most influential frameworks in this domain: the Mack and Notch models for [resist development kinetics](@entry_id:1130921).

The following sections are designed to provide a graduate-level understanding of this topic. The "Principles and Mechanisms" section will dissect the fundamental equations and physical theories, from the concept of the protected polymer fraction to the principles of cooperative inhibition and [percolation](@entry_id:158786). Following this, the "Applications and Interdisciplinary Connections" section will demonstrate how these models are applied in real-world scenarios, including process control, defect analysis, and TCAD simulations. Finally, the "Hands-On Practices" section offers practical exercises to solidify these concepts, guiding you from analytical derivations to computational model building and calibration.

## Principles and Mechanisms

The development of a photoresist is a complex process involving the transformation of a solid polymer film into a precisely defined three-dimensional structure through spatially selective dissolution. The kinetic models that describe this process are essential tools for simulating and optimizing photolithography. They form a crucial bridge between the latent chemical image formed during exposure and [post-exposure bake](@entry_id:1129982) (PEB) and the final physical relief image. This chapter elucidates the fundamental principles and mechanisms underlying the most prevalent kinetic models, namely the Mack and notch models, providing a rigorous framework for understanding how material properties and process conditions govern the rate of dissolution.

### The Polymer State: The Protected Fraction

The development process for a [chemically amplified resist](@entry_id:192110) (CAR) is controlled by the local chemical state of the polymer matrix. For a positive-tone resist, the polymer is initially insoluble in the aqueous base developer due to the presence of acid-labile **[protecting groups](@entry_id:201163)**. During exposure, a [photoacid generator](@entry_id:1129614) (PAG) creates acid molecules. In the subsequent PEB step, this acid diffuses and catalytically cleaves these [protecting groups](@entry_id:201163), rendering the polymer more hydrophilic and thus more soluble.

To model this, we introduce a central state variable: the **protected fraction**, denoted by $P$. At any position $\mathbf{x}$ within the resist film, $P(\mathbf{x})$ represents the local, normalized concentration of [protecting groups](@entry_id:201163) that remain intact, with $P=1$ corresponding to a fully protected state and $P=0$ corresponding to a fully deprotected state . The evolution of this variable during the PEB is typically described by a pseudo-first-order kinetic equation:

$$
\frac{\partial P(\mathbf{x}, t)}{\partial t} = -k_{\mathrm{deprotect}} C_{\mathrm{H}}(\mathbf{x}, t) P(\mathbf{x}, t)
$$

Here, $C_{\mathrm{H}}(\mathbf{x}, t)$ is the local concentration of acid, and $k_{\mathrm{deprotect}}$ is the temperature-dependent deprotection rate constant. The result of the exposure and bake steps is a spatially varying field $P(\mathbf{x})$ that serves as the primary input for the dissolution model. A lower value of $P$ signifies a higher degree of deprotection and, consequently, a greater susceptibility to dissolution by the developer.

### Bounding Principles of Dissolution Rate

The local [dissolution rate](@entry_id:902626), $R$, defined as the velocity of the receding resist-developer interface normal to the surface, is fundamentally a function of the protected fraction, $P$. Before specifying a particular functional form for $R(P)$, we can establish its universal properties based on physical first principles.

The dissolution process is bounded by two limiting rates. In a region that is completely deprotected, corresponding to the limit $P \to 0$, the [protecting groups](@entry_id:201163) no longer inhibit dissolution. The rate reaches a maximum value, **$R_{\max}$**. This maximum rate is not infinite; it is limited by factors such as the transport of developer molecules to the interface or the intrinsic kinetics of polymer chain [disentanglement](@entry_id:637294) and [solvation](@entry_id:146105) .

Conversely, in a region that is fully protected, where $P \to 1$ (or, in the mathematical idealization of some models, $P \to \infty$), the dissolution is maximally suppressed. However, the rate does not typically fall to zero. There is usually a finite, non-zero minimum dissolution rate, **$R_{\min}$**, which arises from residual pathways such as the slow etching of the polymer backbone itself or dissolution at defect sites that cannot be fully suppressed by [protecting groups](@entry_id:201163). Physical realism dictates that $0 \le R_{\min} \le R_{\max}$ .

Thus, any physically sound dissolution model for a positive-tone resist must satisfy these limiting conditions:

$$
\lim_{P \to 0} R(P) = R_{\max} \quad \text{and} \quad \lim_{P \to 1 \text{ or } \infty} R(P) = R_{\min}
$$

This behavior reflects the fundamental mechanism of site blocking: as the protection level $P$ increases, more dissolution-susceptible sites are blocked, and the rate monotonically decreases from $R_{\max}$ to $R_{\min}$ .

### The Mack Model: A Continuous Description of Dissolution

The **Mack model** provides a powerful and widely adopted phenomenological framework for describing the continuous, [monotonic relationship](@entry_id:166902) between the protected fraction and the [dissolution rate](@entry_id:902626). A generalized form of the Mack model, which encompasses a broad range of observed behaviors, is given by the equation :

$$
R(P) = R_{\min} + (R_{\max} - R_{\min}) \left[1 + \left(\frac{P}{P^*}\right)^n\right]^{-m}
$$

The elegance of this model lies in its physically intuitive parameters, each controlling a distinct aspect of the dissolution curve:

*   **$R_{\min}$ and $R_{\max}$**: These are the minimum and maximum dissolution rates, which define the vertical scale of the rate curve and correspond directly to the rates in fully protected and fully deprotected resist, respectively.

*   **$P^*$**: The **threshold protection fraction**. This parameter is a dimensionless quantity that sets the characteristic protection level around which the transition from high-rate to low-rate dissolution occurs. It defines the horizontal position of the transition. It is important to note that $P^*$ is not generally the value of $P$ where the rate is the average of $R_{\min}$ and $R_{\max}$; that specific point depends on all the exponents .

*   **$n$**: The **contrast parameter**. This positive exponent controls the steepness of the transition. A larger value of $n$ results in a more "switch-like" or abrupt change in dissolution rate as $P$ crosses the threshold $P^*$. The magnitude of the slope of the rate curve, $|dR/dP|$, at the characteristic point $P=P^*$ is directly proportional to $n$.

*   **$m$**: The **notch exponent**. This positive exponent primarily modifies the curvature or "shape" of the transition. Contrary to a simplistic interpretation, it does not merely rescale the rate. Instead, it influences the [asymptotic behavior](@entry_id:160836) and the overall cooperativity of the inhibition process. For instance, the protection fraction corresponding to the inflection point of the rate curve depends on both $n$ and $m$.

The power of this formulation becomes even clearer through **non-dimensionalization**. By introducing a normalized rate $\tilde{R} = (R - R_{\min}) / (R_{\max} - R_{\min})$ and a normalized protection fraction $\tilde{P} = P/P^*$, we can rewrite a variant of the Mack model as :

$$
\tilde{R} = (1 + \tilde{P}^n)^{-m}
$$

This reduced form elegantly demonstrates that the fundamental *shape* of the dissolution response is governed entirely by the dimensionless exponents $n$ and $m$. The parameters $R_{\min}$, $R_{\max}$, and $P^*$ simply scale this universal shape to match the specific dimensions (rates and protection levels) of a particular resist-developer system. Furthermore, for large values of protection ($P \gg P^*$), the model predicts a [power-law decay](@entry_id:262227) where the normalized rate scales as $(P/P^*)^{-mn}$. This gives a characteristic log-log slope of $-mn$, a feature that can be used effectively in fitting the model to experimental data .

### Physical Basis of Threshold and Cooperativity

While the Mack model is phenomenological, its mathematical form is deeply rooted in physical chemical principles. Two concepts are particularly crucial for understanding why these models take the form they do: cooperative inhibition and [percolation](@entry_id:158786).

#### Cooperative Inhibition

The power-law nature of the Mack model can be physically interpreted as a manifestation of **cooperative inhibition**. In simple, non-cooperative dissolution, each unprotected site on the polymer chain would contribute independently to the overall rate. In such a scenario, the dissolution rate would be linearly proportional to the fraction of unprotected sites, $U = 1-P$. However, experimental data often show a much stronger suppression of the [dissolution rate](@entry_id:902626) at high protection levels.

This suggests a cooperative mechanism, where the dissolution of a polymer segment requires the simultaneous availability of multiple adjacent unprotected sites . If a "reactive motif" for dissolution requires $m$ neighboring sites to be unprotected, and the sites are occupied randomly, the probability of finding such a motif scales as $U^m$. The dissolution rate would then be proportional to this probability:

$$
R \propto U^m = (1-P)^m
$$

Taking the logarithm of this relationship, we find that $\ln R = m \ln U + \text{const}$. Therefore, the exponent $m$, which quantifies the degree of [cooperativity](@entry_id:147884), is directly given by the slope of a [log-log plot](@entry_id:274224) of [dissolution rate](@entry_id:902626) versus the unprotected fraction, $d(\ln R) / d(\ln U)$. An experimental finding of a slope greater than 1 is strong evidence for cooperative inhibition. As the cooperativity requirement $m$ increases, the dissolution becomes highly suppressed until a significant fraction of sites are deprotected, leading to a much sharper, "notch-like" transition.

#### The Notch Model and Percolation Theory

The term **notch model** is often used to describe dissolution behavior characterized by an extremely sharp, threshold-like transition. While this can be modeled by using a very large exponent $n$ in the Mack model, the physical origin of such abrupt behavior is best explained by **percolation theory** .

Imagine the resist as a grid or lattice, where each site is either "protected" (insoluble) or "deprotected" (soluble). For the developer to cause macroscopic dissolution, it must be able to form a continuous, connected path of soluble sites from the bulk liquid to the receding interface. Percolation theory predicts the existence of a critical threshold for the fraction of soluble sites.

Framed in terms of the protected fraction $P$, there exists a critical value, the **[percolation threshold](@entry_id:146310)** $P^*$, such that:
*   For $P  P^*$, the soluble sites ($U = 1-P > 1-P^*$) form a spanning cluster that percolates through the material. This connected network allows a sustained flux of developer into the resist, resulting in a finite macroscopic dissolution rate.
*   For $P > P^*$, the soluble sites exist only as finite, isolated clusters. The insoluble, protected sites now form a spanning barrier that blocks developer transport into the bulk of the film. Without a continuous pathway for developer transport, the [effective permeability](@entry_id:1124191) of the medium to the developer vanishes. By the principle of mass conservation, a sustained flux is impossible, and the macroscopic [dissolution rate](@entry_id:902626) becomes negligible .

This [percolation](@entry_id:158786) transition provides a rigorous physical justification for the existence of a sharp "notch" in the [dissolution rate](@entry_id:902626), where the rate plummets as the protection level crosses a critical threshold.

### Interfacial Phenomena: Surface Rate Modification

The term "notch" is also used in a different context to describe localized modifications to the [dissolution rate](@entry_id:902626) near surfaces or geometric corners. A common experimental observation is **surface rate retardation**, where the dissolution at the top surface of the resist is slower than in the bulk, even for a uniform protection fraction $P$.

This phenomenon can be modeled by multiplying the bulk [dissolution rate](@entry_id:902626), $R(P)$, by a depth-dependent factor. One such model, sometimes called a **surface inhibition notch model**, takes the form :

$$
R_{\mathrm{notch}}(P, z) = R(P) \left[ 1 - \beta e^{-z/\lambda} \right]
$$

Here, $z$ is the depth from the top surface. The physical meaning of the parameters can be understood by considering a [steady-state diffusion](@entry_id:154663)-reaction process for an inhibitor species at the surface:

*   **$\beta$**: This dimensionless amplitude represents the **fractional rate suppression at the surface** ($z=0$). For $0  \beta  1$, the rate at the surface, $R(P)(1-\beta)$, is reduced compared to the bulk rate.
*   **$\lambda$**: This is the **[characteristic decay length](@entry_id:183295)** over which the surface inhibition effect diminishes. It represents the [diffusion length](@entry_id:172761) of the inhibitor, determined by the ratio of its diffusivity to its consumption rate within the resist.

Such a model correctly predicts that the [dissolution rate](@entry_id:902626) will be lowest at the surface and will increase with depth, approaching the bulk rate $R(P)$ as $z \gg \lambda$. It is instructive to note that many plausible physical mechanisms, such as the accumulation of a surface inhibitor or the depletion of developer near the surface, lead to this same qualitative prediction of surface rate retardation ($\partial R / \partial z > 0$) . This highlights the importance of carefully comparing model predictions with experimental data, as some systems may exhibit more complex behaviors like surface rate *acceleration* that are not captured by these simple models.

### From Rate Law to Interface Velocity

The dissolution rate functions $R(P)$ we have discussed represent the chemical susceptibility of the polymer. The actual velocity of the dissolution front, $v_n$, also depends on the local availability of developer at the interface. In a **reaction-limited** regime, where developer transport is fast compared to the chemical reaction, the interface velocity is directly proportional to both the developer concentration at the surface, $C_s$, and the polymer's intrinsic reactivity, which we have modeled with $R(P)$ :

$$
v_n = \alpha C_s R(P)
$$

The constant $\alpha$ consolidates factors related to [stoichiometry](@entry_id:140916) and material density. This expression bridges the polymer chemistry encapsulated in $R(P)$ with the developer environment, providing a more complete picture of the [moving boundary problem](@entry_id:154637).

### Model Calibration and Physical Constraints

Finally, it is paramount to recognize that the Mack and notch models are not mere curve-fitting exercises. To be predictive and physically meaningful, the model parameters must be constrained by physical laws and grounded in experimental observation . A scientifically sound calibration workflow must enforce these constraints:

*   The rates $R_{\min}$ and $R_{\max}$ must be non-negative and finite. Their values can be directly informed by [spectroscopic ellipsometry](@entry_id:182271) measurements on unexposed and fully exposed resist films, respectively. $R_{\max}$ is further bounded from above by mass transport limits.
*   The exponents $n$ and $m$ must be positive to ensure the correct monotonic behavior and physical interpretation of the [rate function](@entry_id:154177).
*   In [surface modification](@entry_id:273724) models, the decay length $\lambda$ must be positive to represent a spatially decaying effect.

During [numerical optimization](@entry_id:138060) to fit model parameters to experimental data (e.g., from SEM or AFM [cross-sections](@entry_id:168295)), these constraints must be rigorously enforced. A robust technique is **[reparameterization](@entry_id:270587)**, where constrained parameters are expressed as functions of unconstrained variables (e.g., setting a positive parameter $p = \exp(\theta)$ and optimizing for $\theta$). This ensures that the resulting calibrated model is not only accurate in its predictions but also consistent with the fundamental principles of physics and chemistry that govern the dissolution process.