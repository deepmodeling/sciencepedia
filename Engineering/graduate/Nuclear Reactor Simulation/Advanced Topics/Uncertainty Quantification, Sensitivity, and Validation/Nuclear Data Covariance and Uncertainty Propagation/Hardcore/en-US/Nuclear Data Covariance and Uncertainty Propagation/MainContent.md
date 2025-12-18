## Introduction
Predicting the behavior of nuclear reactors with high fidelity is a cornerstone of modern nuclear engineering. While deterministic simulations provide best-estimate values for critical parameters, these predictions are inherently incomplete without a rigorous quantification of their uncertainty. The fundamental nuclear data—cross sections, fission yields, decay data—that underpin these simulations are not known with perfect precision. This knowledge gap introduces uncertainty that propagates through complex physics models, impacting the reliability of safety assessments and design margins. Addressing this challenge requires a systematic framework for representing and propagating these uncertainties.

This article provides a graduate-level exploration of [nuclear data covariance](@entry_id:1128921) and [uncertainty propagation](@entry_id:146574), guiding you from foundational theory to practical application. It is structured to build a comprehensive understanding of this critical topic. The first chapter, **Principles and Mechanisms**, establishes the mathematical language of uncertainty, defining the covariance matrix and deriving the "[sandwich rule](@entry_id:1131198)" for first-order uncertainty propagation. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these methods are applied to quantify uncertainties in real-world reactor analysis, from criticality and [control rod worth](@entry_id:1123006) to accident scenarios and fuel depletion. Finally, the **Hands-On Practices** section provides opportunities to apply these concepts through targeted problems, reinforcing the theoretical knowledge with practical implementation skills. By navigating these chapters, you will gain the expertise to perform and interpret rigorous uncertainty analyses in nuclear reactor simulations.

## Principles and Mechanisms

Having established the importance of [uncertainty quantification](@entry_id:138597) in the preceding chapter, we now turn to the fundamental principles and mathematical mechanisms that govern the representation and propagation of nuclear data uncertainties. This chapter will define the core statistical concepts, derive the primary methods for uncertainty propagation, and explore the physical origins of nuclear data covariances, providing a rigorous foundation for the simulation practices discussed later.

### Defining Uncertainty: The Covariance Matrix

At the heart of [uncertainty analysis](@entry_id:149482) lies the need to characterize not only the uncertainty of individual parameters but also their interdependencies. While the variance of a single parameter quantifies its uncertainty, **covariance** captures the degree to which two parameters vary together.

For a vector of nuclear data parameters, such as [multigroup cross sections](@entry_id:1128302), represented as a random vector $\boldsymbol{\sigma} = (\sigma_1, \sigma_2, \ldots, \sigma_n)^\top$ with mean values $\boldsymbol{\mu} = (\mu_1, \mu_2, \ldots, \mu_n)^\top$, the uncertainty structure is fully described by the **covariance matrix**, $\mathbf{C}$. The element $C_{ij}$ of this matrix is the covariance between parameters $\sigma_i$ and $\sigma_j$:

$$
C_{ij} = \operatorname{Cov}(\sigma_i, \sigma_j) = \mathbb{E}[(\sigma_i - \mu_i)(\sigma_j - \mu_j)]
$$

where $\mathbb{E}[\cdot]$ denotes the expectation operator. The diagonal elements of this matrix, $C_{ii} = \mathbb{E}[(\sigma_i - \mu_i)^2]$, are the **variances** of the individual parameters, denoted $\operatorname{Var}(\sigma_i)$ .

A dimensionless and more interpretable measure of interdependence is the **correlation coefficient**, $\rho_{ij}$, defined as:

$$
\rho_{ij} = \frac{\operatorname{Cov}(\sigma_i, \sigma_j)}{\sqrt{\operatorname{Var}(\sigma_i)\operatorname{Var}(\sigma_j)}} = \frac{C_{ij}}{\sqrt{C_{ii}C_{jj}}}
$$

The correlation coefficient ranges from $-1$ (perfect anti-correlation) to $+1$ (perfect positive correlation), with $0$ indicating no linear correlation. While covariance entries carry units that are the product of the units of the corresponding parameters (e.g., barns squared ($\text{b}^2$) for two cross sections), the correlation coefficient is always dimensionless .

Any valid covariance matrix must possess two fundamental mathematical properties. First, it must be **symmetric**, meaning $C_{ij} = C_{ji}$, which follows directly from the [commutative property](@entry_id:141214) of multiplication in its definition. Second, it must be **positive semidefinite**. This property ensures that the variance of any [linear combination](@entry_id:155091) of the parameters is non-negative, a physical necessity. For any constant vector $\mathbf{a} \in \mathbb{R}^n$, the variance of the scalar quantity $Y = \mathbf{a}^\top\boldsymbol{\sigma}$ is given by $\operatorname{Var}(Y) = \mathbf{a}^\top \mathbf{C} \mathbf{a}$. Since variance cannot be negative, we must have $\mathbf{a}^\top \mathbf{C} \mathbf{a} \ge 0$ for any choice of $\mathbf{a}$. This is the definition of a [positive semidefinite matrix](@entry_id:155134). Equality to zero is possible if there exists a perfect [linear dependency](@entry_id:185830) among the parameters, which corresponds to a singular covariance matrix .

The choice of units for the parameters affects the numerical values in the covariance matrix. If a set of cross sections $\boldsymbol{\sigma}$ is uniformly rescaled by a constant factor $\alpha$ (e.g., converting from barns to $\text{m}^2$), the new covariance matrix $\tilde{\mathbf{C}}$ is related to the original by $\tilde{C}_{ij} = \alpha^2 C_{ij}$. However, the correlation coefficients $\rho_{ij}$ are invariant under such a scaling, as the factor $\alpha^2$ cancels between the numerator and denominator .

### Propagation of Uncertainty: The First-Order Linear Method

Once the input uncertainties are characterized by a covariance matrix, the next step is to propagate their effects through a reactor physics model to quantify the uncertainty in an output quantity of interest, or **response**, such as the [effective multiplication factor](@entry_id:1124188), $k_{\text{eff}}$. Let the response be a [differentiable function](@entry_id:144590) of the input data vector, $y = f(\mathbf{x})$.

The most common method for uncertainty propagation is based on a first-order Taylor series expansion of the model $f(\mathbf{x})$ around the mean value of the inputs, $\boldsymbol{\mu}$:

$$
y = f(\mathbf{x}) \approx f(\boldsymbol{\mu}) + \mathbf{J}(\boldsymbol{\mu})(\mathbf{x} - \boldsymbol{\mu})
$$

Here, $\mathbf{J}(\boldsymbol{\mu})$ is the **Jacobian matrix** of the function $f$ evaluated at the mean $\boldsymbol{\mu}$. Its entries, $J_{ij} = \partial f_i / \partial x_j$, are the **unnormalized first-order sensitivity coefficients**, which quantify the absolute change in an output component $f_i$ per unit change in an input parameter $x_j$  . For a scalar response, the Jacobian is a row vector of these sensitivities.

This [linear approximation](@entry_id:146101) shows that small deviations in the input, $\delta\mathbf{x} = \mathbf{x} - \boldsymbol{\mu}$, are linearly transformed into deviations in the output, $\delta\mathbf{y} \approx \mathbf{J} \delta\mathbf{x}$. Applying the definition of covariance to this linear transformation yields the celebrated **"[sandwich rule](@entry_id:1131198)"** for first-order uncertainty propagation:

$$
\mathbf{C}_y \approx \mathbf{J} \mathbf{C}_x \mathbf{J}^\top
$$

where $\mathbf{C}_x$ is the covariance matrix of the input vector $\mathbf{x}$ and $\mathbf{C}_y$ is the approximated covariance matrix of the output vector $\mathbf{y}$ . This formula is the cornerstone of linear uncertainty analysis. It shows how the Jacobian acts as a [linear operator](@entry_id:136520) that maps input variances and covariances into the output space, mixing them to generate the final uncertainty structure.

For the common case of a single scalar response, $R$, the Jacobian becomes a row vector of sensitivities $\mathbf{S}^\top = [\partial R/\partial x_1, \ldots, \partial R/\partial x_n]$, and the output covariance matrix becomes a single number: the variance of the response, $\operatorname{Var}(R)$. The formula simplifies to:

$$
\operatorname{Var}(R) \approx \mathbf{S}^\top \mathbf{C}_x \mathbf{S} = \sum_{i=1}^{n} \sum_{j=1}^{n} S_i S_j C_{ij}
$$

This expanded form reveals that the total output variance is a sum of terms involving the variances of each input ($S_i^2 C_{ii}$) and cross-terms involving the covariances between different inputs ($S_i S_j C_{ij}$ for $i \ne j$). These cross-terms can either increase or decrease the total uncertainty depending on the signs of the sensitivities and the covariances  . For instance, consider a response $R$ with a positive sensitivity to a fission cross section $x_1$ ($S_1 > 0$) and a negative sensitivity to a capture cross section $x_2$ ($S_2  0$). If these two cross sections are anti-correlated ($C_{12}  0$), as is often the case, the product $S_1 S_2 C_{12}$ will be positive, thereby *increasing* the total propagated uncertainty compared to the case where the correlation is ignored.

It is often more intuitive to work with dimensionless **[normalized sensitivity](@entry_id:1128895) coefficients**, defined as $s_i = \left(\frac{x_i}{R}\right)\frac{\partial R}{\partial x_i}$. This coefficient quantifies the fractional change in the response $R$ for a given fractional change in the input $x_i$. For example, a [normalized sensitivity](@entry_id:1128895) of $s_i = 1$ implies that a $1\%$ increase in $x_i$ leads to a $1\%$ increase in $R$ . Using normalized sensitivities, the propagated *relative* variance can be expressed in a similar sandwich form:

$$
\frac{\operatorname{Var}(R)}{R^2} \approx \mathbf{s}^\top \mathbf{C}_{\mathrm{rel}} \mathbf{s}
$$

where $\mathbf{s}$ is the vector of normalized sensitivities and $(\mathbf{C}_{\mathrm{rel}})_{ij} = C_{ij}/(x_i x_j)$ is the relative covariance matrix of the inputs.

### Assumptions and Limitations of Linear Propagation

The elegance and [computational efficiency](@entry_id:270255) of the first-order method come at the cost of several underlying assumptions. The method is an approximation, and its validity hinges on the function $f(\mathbf{x})$ being "sufficiently linear" over the region of the input space where the probability distribution of $\mathbf{x}$ has significant weight. Formally, this requires that the second-order [remainder term](@entry_id:159839) in the Taylor expansion, which involves the Hessian matrix of second derivatives, is negligible compared to the first-order term .

Linear propagation can incur significant error under several conditions:
1.  **Strong Nonlinearity**: If the [response function](@entry_id:138845) exhibits significant curvature, the [linear approximation](@entry_id:146101) breaks down. In reactor physics, strong nonlinearities can arise from temperature feedback effects (like Doppler broadening of resonances), complex self-shielding phenomena, or burnup-dependent effects.
2.  **Large Input Uncertainties**: Even for a model with mild nonlinearity, large input uncertainties mean that the model is sampled far from the expansion point $\boldsymbol{\mu}$, where [linear approximation](@entry_id:146101) is less accurate. The quadratic error term scales with the square of the perturbation magnitude, becoming dominant for large perturbations.
3.  **Non-[differentiability](@entry_id:140863)**: The method relies on the existence of derivatives. If the model contains "if-then" logic, thresholds, or [piecewise functions](@entry_id:160275), the Jacobian may be undefined or discontinuous, invalidating the approach .

Furthermore, even when the [linear approximation](@entry_id:146101) provides an accurate estimate of the output variance (a second moment), it may fail to capture other important features of the output distribution. If the input distribution is Gaussian, the linear method implicitly approximates the output distribution as Gaussian. However, any nonlinearity in the model will introduce non-Gaussian features, such as skewness (asymmetry) or [kurtosis](@entry_id:269963) (heavy tails), into the true output distribution. This can lead to a significant misestimation of extreme [quantiles](@entry_id:178417) and tail probabilities, a critical issue in safety analysis where margins and rare event probabilities are of primary concern .

### The Physical Basis of Nuclear Data Covariances

The off-diagonal elements in [nuclear data covariance](@entry_id:1128921) matrices are not arbitrary; they reflect underlying physical relationships and correlations introduced during the experimental and theoretical evaluation process. Neglecting them, by assuming the covariance matrix is diagonal, is equivalent to making a physically unjustified assumption of independence, which can lead to significant bias in uncertainty estimates  .

Several physical mechanisms give rise to these crucial correlations:
*   **Shared Model Parameters**: Nuclear reaction models (e.g., optical models, resonance theories) use a set of parameters that influence calculated cross sections over broad energy ranges and for multiple reaction channels. Uncertainty in a single resonance parameter (e.g., its energy or width) will simultaneously affect the cross section in multiple energy groups that the resonance spans, thereby inducing a positive correlation between those group cross sections . Similarly, an uncertainty in a parameter of a statistical model like the Hauser-Feshbach theory can create correlations between different reaction channels (e.g., $(n, \gamma)$ and $(n, n')$).
*   **Conservation Laws**: Physical constraints and conservation laws are a major source of negative correlations. For instance, the total probability for an [inelastic scattering](@entry_id:138624) event from energy $E$ must sum to one when integrated over all possible final energies $E'$. An uncertainty that increases the probability of scattering to one energy range must be balanced by a decrease in the probability of scattering to other ranges. This creates anti-correlations between the corresponding multigroup [scattering matrix](@entry_id:137017) elements . A similar principle applies to the prompt fission [neutron spectrum](@entry_id:752467), $\chi(E)$, which must be normalized to unity .
*   **Experimental Methods**: Many nuclear data experiments measure ratios of cross sections or measure a cross section relative to a well-known standard (e.g., $^{1}$H [elastic scattering](@entry_id:152152)). Uncertainty in the standard cross section then propagates to all measurements that used it, inducing a common-mode correlation among them.

These physically-grounded covariances are captured in evaluated [nuclear data libraries](@entry_id:1128922), such as those in the **ENDF-6 format**. A practical challenge is that this format often stores covariance data compactly. For example, a covariance sub-library (e.g., `MF=32` or `MF=33`) might provide a lower-triangular list of dimensionless **relative covariance** entries, $m_{ij} = \operatorname{Cov}(\sigma_i, \sigma_j) / (\sigma_i \sigma_j)$. To use this data in [uncertainty propagation](@entry_id:146574), one must first reconstruct the full, symmetric, absolute covariance matrix $\mathbf{C}$ with the correct physical units. This is accomplished via a [congruence transformation](@entry_id:154837):

$$
\mathbf{C} = \mathbf{S} \mathbf{M} \mathbf{S}
$$

where $\mathbf{M}$ is the full symmetric relative covariance matrix reconstructed from the tabulated list, and $\mathbf{S}$ is a [diagonal matrix](@entry_id:637782) containing the mean values of the cross sections, $\sigma_i$. This transformation correctly scales the dimensionless relative data to produce an absolute covariance matrix with units of, for example, $\text{b}^2$ .

### Advanced Topics in Uncertainty Modeling

While the [first-order method](@entry_id:174104) provides a powerful baseline, rigorous [uncertainty quantification](@entry_id:138597) often requires more sophisticated approaches to handle the complexities of reactor physics and data analysis.

#### Epistemic versus Aleatory Uncertainty

It is crucial to distinguish between two fundamental types of uncertainty. **Epistemic uncertainty** arises from a lack of knowledge and is, in principle, reducible by acquiring more data or improving models. The uncertainty in fundamental nuclear data constants falls into this category. **Aleatory uncertainty**, in contrast, represents inherent randomness or variability in a system that cannot be reduced, even with perfect knowledge. Examples include manufacturing tolerances in fuel fabrication or stochastic fluctuations in turbulent flow .

These two types of uncertainty require different treatment. Epistemic uncertainty in nuclear data can be reduced by assimilating new experimental information, for example through Bayesian updating. Aleatory uncertainty, being a feature of the physical system itself, can only be characterized, not eliminated. Propagating mixed uncertainties often requires a nested or two-level sampling approach, where an outer loop samples from the distribution of epistemic parameters (e.g., different plausible nuclear data files) and an inner loop, for each epistemic sample, performs many calculations sampling the aleatory variables. This allows for the separation of the total output uncertainty into its epistemic and aleatory components .

#### Covariance of Constrained Quantities

Special care must be taken when modeling uncertainties for quantities that are subject to a physical constraint. A prime example is the prompt fission neutron spectrum $\boldsymbol{\chi}$, which is a probability distribution and must satisfy the normalization constraint $\sum_g \chi_g = 1$. This constraint imposes a mathematical requirement on its covariance matrix $\mathbf{C}_\chi$: it must be singular, with row and column sums equal to zero. That is, $\mathbf{C}_\chi \mathbf{1} = \mathbf{0}$, where $\mathbf{1}$ is a vector of ones. This reflects the fact that any valid perturbation to the spectrum must conserve the total probability; an increase in one group must be balanced by a decrease in others. Standard methods for generating such constrained covariance matrices involve projecting an unconstrained [prior covariance](@entry_id:1130174) onto the valid subspace or using a transformation (such as the logistic or "[softmax](@entry_id:636766)" transformation) that inherently respects the constraint . Similar constraints apply to fission product yields and scattering matrices.

#### Handling Incomplete Covariance Information

A common practical challenge is that evaluated data libraries may not provide complete covariance information for all relevant parameters. When a covariance value is missing, an assumption must be made. Several scientifically defensible strategies exist to address this, and the choice can significantly impact the final decision-making process .
*   **Point Imputation**: A simple approach is to assume a value, for instance, setting the unknown [correlation coefficient](@entry_id:147037) $\rho$ to zero (assuming independence). While easy, this may be non-conservative and can lead to a false sense of security.
*   **Bounding Analysis**: A more robust approach is to perform a [worst-case analysis](@entry_id:168192) by propagating uncertainty across the full valid range of the unknown parameter (e.g., $\rho \in [-1, 1]$). This reveals the sensitivity of the result to the missing information and identifies whether the design is robust under all plausible assumptions.
*   **Informed Analysis**: If external information, such as results from integral benchmark experiments, can be used to constrain the plausible range of the missing parameter (e.g., $\rho \in [0, 0.5]$), the analysis can be performed over this reduced, physically-informed range.
*   **Probabilistic Imputation**: One can assign a probability distribution to the unknown parameter (e.g., a [uniform distribution](@entry_id:261734) over its valid range) and propagate this "second-order" uncertainty, for example, using Monte Carlo methods. This yields a distribution of possible outcomes and can quantify the risk associated with a decision under ignorance.

The choice among these strategies depends on the context, the available information, and the level of conservatism required for the application. Acknowledging and systematically treating missing covariance data is a hallmark of rigorous [uncertainty analysis](@entry_id:149482).