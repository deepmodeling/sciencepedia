## Introduction
Accurate [interatomic potentials](@entry_id:177673) are the cornerstone of [molecular dynamics simulations](@entry_id:160737), enabling the study of complex systems at an atomistic level. However, the development of these potentials is a formidable challenge, representing a classic [inverse problem](@entry_id:634767): how do we derive the parameters of a simple mathematical function that can accurately reproduce the intricate physics captured by high-level quantum mechanical calculations or precise experimental measurements? This article provides a comprehensive guide to the modern fitting procedures designed to solve this problem, bridging the gap between raw data and predictive molecular models.

This exploration is structured into three distinct parts. The journey begins in **Principles and Mechanisms**, where we will uncover the statistical foundations of [parameter fitting](@entry_id:634272), deriving the widely used weighted [least-squares method](@entry_id:149056) from the principled framework of Maximum Likelihood Estimation. We will learn how to construct composite objective functions that intelligently balance diverse data types like energies, forces, and stresses. Following this, **Applications and Interdisciplinary Connections** will showcase these methods in action, from the practical art of [force field parameterization](@entry_id:174757) for [biomolecules](@entry_id:176390) to specialized applications in materials science, [computational spectroscopy](@entry_id:201457), and [coarse-grained modeling](@entry_id:190740), culminating in an introduction to the powerful paradigm of Bayesian inference. Finally, **Hands-On Practices** will offer a series of targeted problems to solidify your understanding of concepts such as [model diagnostics](@entry_id:136895), [uncertainty quantification](@entry_id:138597), and handling correlated data. Together, these sections provide a graduate-level roadmap for mastering the theory and practice of fitting [interatomic potentials](@entry_id:177673).

## Principles and Mechanisms

The development of accurate [interatomic potentials](@entry_id:177673) is an exercise in solving an inverse problem: given a set of observations derived from either high-fidelity quantum mechanical calculations or experimental measurements, we seek to determine the parameters of a model [potential energy function](@entry_id:166231) that best reproduce these observations. This chapter elucidates the fundamental principles and mechanisms that underpin modern fitting procedures, progressing from the statistical foundations of objective functions to the practical construction of robust training workflows and advanced methods for diagnosing and remedying model deficiencies.

### The Probabilistic Foundation of Parameter Fitting

At its core, the process of fitting a potential is a form of statistical inference. We postulate a parametric functional form for the potential energy, $E(\mathbf{R}; \boldsymbol{\theta})$, where $\mathbf{R}$ represents the atomic coordinates of a configuration and $\boldsymbol{\theta}$ is a vector of parameters we wish to determine. Our reference data, such as energies $E^{\mathrm{QM}}$ and forces $\mathbf{F}^{\mathrm{QM}}$ from quantum mechanics, are treated as observations of a "true" underlying system. The discrepancy between our model's prediction and the reference data is then attributed to a combination of [model-form error](@entry_id:274198) (the functional form is an approximation) and inherent noise in the reference data itself. This total discrepancy, or residual, is modeled as a random variable.

A powerful and widely adopted approach is to model these residuals as being drawn from a Gaussian distribution. This choice is not arbitrary; it is rigorously justified by the **Central Limit Theorem (CLT)**. The total error in any given observable is the aggregate of many small, approximately independent contributions. For instance, in a Density Functional Theory (DFT) calculation, sources of error include the use of a finite basis set, incomplete treatment of electron correlation, convergence thresholds for the [self-consistent field](@entry_id:136549), and numerical integration grid inaccuracies. Likewise, the misspecification of the classical potential's functional form can be viewed as the sum of many small, localized deviations from the true potential energy surface. The CLT states that the sum of a large number of independent random variables will be approximately normally distributed. Therefore, modeling the energy and force residuals as [independent and identically distributed](@entry_id:169067) (i.i.d.) Gaussian random variables is a statistically robust and principled choice [@problem_id:3413113].

Let us formalize this. Consider a dataset of $K$ configurations. For each configuration $i$, we have a reference energy $E^{\mathrm{QM}}_{i}$ and a set of reference forces $\mathbf{F}^{\mathrm{QM}}_{i}$. Our model, with parameters $\boldsymbol{\theta}$ and a trainable energy offset $b$ (to account for the arbitrary zero of energy), predicts energy $E_{i}(\boldsymbol{\theta})$ and forces $\mathbf{F}_{i}(\boldsymbol{\theta}) = -\nabla_{\mathbf{R}_{i}}E_{i}(\boldsymbol{\theta})$. The noise model is:

$E^{\mathrm{QM}}_{i} = E_{i}(\boldsymbol{\theta}) + b + \varepsilon^{E}_{i}$
$F^{\mathrm{QM}}_{i,a} = F_{i,a}(\boldsymbol{\theta}) + \varepsilon^{F}_{i,a}$

where $\varepsilon^{E}_{i} \sim \mathcal{N}(0, \sigma_{E}^{2})$ and each force component residual $\varepsilon^{F}_{i,a} \sim \mathcal{N}(0, \sigma_{F}^{2})$ are assumed to be independent Gaussian noise terms. Note that we assign distinct variances, $\sigma_{E}^{2}$ and $\sigma_{F}^{2}$, to the energy and force residuals, as their characteristic error magnitudes are generally different.

Under this model, the probability of observing a single energy data point $E^{\mathrm{QM}}_{i}$ given the parameters is given by the Gaussian probability density function (PDF):
$p(E^{\mathrm{QM}}_{i} | \boldsymbol{\theta}, b, \sigma_{E}) = \frac{1}{\sqrt{2\pi\sigma_E^2}} \exp\left(-\frac{(E^{\mathrm{QM}}_{i} - E_i(\boldsymbol{\theta}) - b)^2}{2\sigma_E^2}\right)$

Assuming independence across all energy and force observations, the [joint likelihood](@entry_id:750952) of observing the entire dataset is the product of the individual probabilities. It is more convenient to work with the logarithm of the likelihood (the [log-likelihood](@entry_id:273783)), which transforms this product into a sum. The joint [log-likelihood](@entry_id:273783) for a dataset of $K$ configurations with a total of $D$ force components is [@problem_id:3413113]:

$\ln \mathcal{L}(\boldsymbol{\theta}, b, \sigma_E, \sigma_F) = C - \frac{1}{2\sigma_E^2}\sum_{i=1}^{K} (E^{\mathrm{QM}}_{i} - E_i(\boldsymbol{\theta}) - b)^2 - \frac{1}{2\sigma_F^2}\sum_{i=1}^{K}\sum_{a=1}^{D_i} (F^{\mathrm{QM}}_{i,a} - F_{i,a}(\boldsymbol{\theta}))^2$

where $C$ is a constant that does not depend on the parameters $\boldsymbol{\theta}$ and $b$. The principle of **Maximum Likelihood Estimation (MLE)** dictates that we should choose the parameters that maximize this function. Maximizing $\ln \mathcal{L}$ is equivalent to minimizing its negative, which, after discarding the constant $C$ and the leading factor of $1/2$, is equivalent to minimizing the weighted sum of squared errors:

$J(\boldsymbol{\theta}, b) = \frac{1}{\sigma_E^2}\sum_{i=1}^{K} (E_i(\boldsymbol{\theta}) + b - E^{\mathrm{QM}}_{i})^2 + \frac{1}{\sigma_F^2}\sum_{i=1}^{K}\sum_{a=1}^{D_i} (F_{i,a}(\boldsymbol{\theta}) - F^{\mathrm{QM}}_{i,a})^2$

This derivation provides the fundamental bridge between the probabilistic MLE framework and the widely used method of **weighted least-squares**. It reveals that the optimal statistical weights for each term in the objective function are the inverse of the corresponding error variances.

### Constructing a Composite Objective Function

Real-world potential fitting rarely relies on a single type of data. A robust potential must simultaneously reproduce energies, forces, and often stresses (or virials), which are related to the response of the system to deformation. The MLE framework provides a natural way to construct a composite [objective function](@entry_id:267263) for these heterogeneous data types.

#### Inverse-Variance Weighting and Data Normalization

The principle derived above is general: for any set of independent [observables](@entry_id:267133), the maximum likelihood estimator is obtained by minimizing a [sum of squared residuals](@entry_id:174395), where each residual is weighted by the inverse of its [error variance](@entry_id:636041) [@problem_id:3413125]. An observable with a smaller variance (i.e., a more precise measurement) contributes more heavily to the [objective function](@entry_id:267263).

When constructing a composite objective, we must also account for the physical nature of the observables. Some quantities, like total energy and the virial tensor, are **extensive**, meaning their magnitude scales with system size. Others, like forces on individual atoms and stress, are **intensive**. The variance of the residuals for [extensive properties](@entry_id:145410) also scales with system size. For instance, if we assume that the error in the total energy arises from the sum of independent, local atomic contributions each having variance $\sigma_e^2$, then the variance of the total energy error for a system of $N_i$ atoms is $\text{Var}(\Delta E_i) = N_i \sigma_e^2$. Similarly, the variance of the virial residual can be shown to scale with the square of the cell volume, $\text{Var}(\Delta W_{i,\mu\nu}) = V_i^2 \sigma_S^2$, where $\sigma_S^2$ is the variance of the corresponding stress component residual [@problem_id:3413228].

A properly constructed objective function must incorporate these [scaling relations](@entry_id:136850). A general, dimensionless objective function for fitting energies ($E$), forces ($F$), and virials ($W$) can be written as [@problem_id:3413228]:

$J(\boldsymbol{\theta}) = w_E L_E + w_F L_F + w_W L_W$

where $w_E, w_F, w_W$ are user-defined dimensionless weights to balance the overall contribution of each data type, and the individual loss terms $L_E, L_F, L_W$ represent the mean squared normalized error for each observable class:

$L_E = \frac{1}{M} \sum_{i=1}^{M} \frac{\left(E_i(\boldsymbol{\theta}) - E_i^{\mathrm{QM}}\right)^2}{N_i \sigma_E^2}$

$L_F = \frac{1}{\sum_{i=1}^{M} 3N_i} \sum_{i=1}^{M} \frac{1}{\sigma_F^2} \sum_{a=1}^{N_i} \sum_{\alpha} \left(F_{i,a,\alpha}(\boldsymbol{\theta}) - F_{i,a,\alpha}^{\mathrm{QM}}\right)^2$

$L_W = \frac{1}{6M} \sum_{i=1}^{M} \frac{1}{V_i^2 \sigma_S^2} \sum_{\mu \le \nu} \left(W_{i,\mu\nu}(\boldsymbol{\theta}) - W_{i,\mu\nu}^{\mathrm{QM}}\right)^2$

Here, $\sigma_E^2$ is the variance of the energy residual *per atom*, $\sigma_F^2$ is the variance per force component, and $\sigma_S^2$ is the variance per stress component. The denominators $M$, $\sum_{i=1}^{M} 3N_i$, and $6M$ normalize by the number of data points of each type.

#### The Value of Fitting Forces and Stresses

While energies are the most fundamental quantity, including their derivatives—forces and stresses—in the training data provides substantially more information about the shape and curvature of the [potential energy surface](@entry_id:147441).

Mathematically, this can be understood by examining the **Hessian** of the objective function, $\mathbf{H}_{ab} = \frac{\partial^2 J}{\partial \theta_a \partial \theta_b}$, which describes the curvature of the loss landscape. A well-conditioned Hessian (with no near-zero eigenvalues) is crucial for efficient and stable [parameter optimization](@entry_id:151785). For a simple [pairwise potential](@entry_id:753090) $\phi(r;\boldsymbol{\theta})$, the Hessian of an energy-only [loss function](@entry_id:136784) involves terms related to first and second derivatives of the potential with respect to parameters, like $\phi_{,a}$ and $\phi_{,ab}$. In contrast, the Hessian of a force-based loss function involves terms related to derivatives of the force, such as products of $\phi_{r,a}$ and $\phi_{r,b}$ (where $\phi_r$ is the radial derivative of $\phi$). This direct inclusion of gradient information often leads to a better-conditioned optimization problem, helping to disentangle parameters that might have similar effects on the total energy but different effects on forces [@problem_id:3413134].

Fitting to stress tensors calculated for configurations under various applied strains is particularly powerful. As described by linear elasticity, the stress response $\boldsymbol{\sigma}$ to a small strain $\boldsymbol{\varepsilon}$ is $\boldsymbol{\sigma} \approx \boldsymbol{\sigma}_{0} + \mathbb{C} : \boldsymbol{\varepsilon}$, where $\mathbb{C}$ is the [elastic stiffness tensor](@entry_id:196425). By including training data from configurations with both volumetric strains (changing volume) and shear strains (changing shape), the fitting procedure implicitly constrains the model to reproduce the material's pressure-volume relationship (related to the [bulk modulus](@entry_id:160069)) and its response to shear deformation (related to the shear moduli). This directly embeds macroscopic, experimentally relevant elastic properties into the potential [@problem_id:3413119].

#### Balancing Data Types in Practice

Even with correct per-point inverse-variance weighting and normalization, a practical issue often arises from dataset imbalance. A typical training set may contain thousands of force components for every one energy value. If naively summed, the force contribution to the total loss would completely dominate the energy contribution. To mitigate this, a common strategy is to choose the global weights ($w_E, w_F, \dots$) to equalize the *expected total contribution* of each data type to the [loss function](@entry_id:136784). For a simple energy-force objective, this leads to a relative weighting factor $\lambda = w_F/w_E$ (or vice-versa) that depends on both the number of data points and their respective variances [@problem_id:3413151]:

$\lambda^{\star} = \frac{\text{Expected Energy Loss}}{\text{Expected Force Loss}} = \frac{N_E \sigma_E^2}{D_F \sigma_F^2}$

where $N_E$ is the number of energy data points and $D_F$ is the total number of force components. This ensures that, on average, both data modalities contribute meaningfully to the [parameter optimization](@entry_id:151785).

### Fitting to Experimental and Structural Data

While quantum mechanical data provide a detailed picture of the [potential energy surface](@entry_id:147441), [interatomic potentials](@entry_id:177673) can also be refined against experimental data or results from higher-level simulations. A prime example is fitting to structural information, such as the **radial distribution function (RDF)**, $g(r)$, which can be measured via neutron or X-ray scattering experiments.

In the limit of a very low-density gas, where interactions between more than two particles are negligible, there exists a direct and simple relationship between the [pair potential](@entry_id:203104) $U(r)$ and the RDF. The probability of finding two particles at a separation $r$ is governed by the Boltzmann factor of their interaction energy. This leads to the **Boltzmann inversion** formula [@problem_id:3413123]:

$U(r) = -k_B T \ln(g(r))$

where $k_B$ is the Boltzmann constant and $T$ is the temperature. This equation suggests a straightforward method for extracting a [pair potential](@entry_id:203104) directly from an experimentally measured RDF.

However, this simple relation breaks down at the finite densities characteristic of liquids and solids. At any non-zero density, the arrangement of particles around a central pair is influenced by the surrounding medium. The RDF is more generally related to the **Potential of Mean Force (PMF)**, $W(r)$, defined by $g(r) \equiv \exp(-\beta W(r))$, where $\beta=1/(k_B T)$. The PMF represents the effective potential between two particles, averaged over all configurations of all other particles in the system. It includes not only the direct interaction $U(r)$ but also indirect, solvent-mediated contributions. At finite density, $W(r) \neq U(r)$ due to these many-body correlation effects. Theoretical frameworks like the Mayer [cluster expansion](@entry_id:154285) or the Born-Green-Yvon (BGY) hierarchy formally show that $W(r)$ can be expressed as a series expansion in density, with $U(r)$ as the leading term [@problem_id:3413123]. Therefore, while Boltzmann inversion can provide a useful first approximation, more sophisticated iterative methods are required to deconvolve the true [pair potential](@entry_id:203104) $U(r)$ from the PMF obtained from a measured $g(r)$ at finite density.

### Diagnosing and Addressing Model Deficiencies

The process of fitting is not always straightforward. Even with a well-constructed objective function and high-quality data, one may encounter fundamental issues related to the model's structure or the information content of the data.

#### Parameter Identifiability and the Fisher Information Matrix

A critical concept in [model fitting](@entry_id:265652) is **[parameter identifiability](@entry_id:197485)**. A parameter is identifiable if it can be uniquely determined from the available data. We distinguish between two types:

1.  **Structural Non-identifiability**: This occurs when the mathematical structure of the model itself makes it impossible to determine a parameter, even with perfect, noise-free data. A classic example is attempting to fit an absolute energy offset parameter, $E_0$, using only relative energies and forces. Since forces are derivatives of the potential energy, they are independent of any constant offset. Likewise, relative energies, $E(r_i) - E(r_{ref})$, are also independent of $E_0$. Consequently, no amount of such data can ever determine the value of $E_0$ [@problem_id:3413181].

2.  **Practical Non-[identifiability](@entry_id:194150)**: This arises when parameters are structurally identifiable in theory, but are so highly correlated in their effect on the observables that they cannot be reliably disentangled from a finite, noisy dataset. For example, two parameters in a complex potential might have nearly identical effects on the energy over the sampled range of configurations, making their individual values difficult to pinpoint.

The primary tool for diagnosing identifiability issues is the **Fisher Information Matrix (FIM)**, $\mathcal{I}$. For a model with parameters $\boldsymbol{\theta}$ and [observables](@entry_id:267133) $\mathbf{y}$, the FIM is related to the sensitivity of the model's predictions to parameter changes. Under the assumption of Gaussian noise, its elements are given by $\mathcal{I}_{ab} \approx \sum_k \frac{1}{\sigma_k^2} \frac{\partial y_k}{\partial \theta_a} \frac{\partial y_k}{\partial \theta_b}$. The FIM is the Hessian of the [negative log-likelihood](@entry_id:637801) (near the minimum) and its inverse, $\mathcal{I}^{-1}$, approximates the covariance matrix of the estimated parameters (the Cramér-Rao bound).

The eigenspectrum of the FIM provides a powerful diagnostic:
-   A **zero eigenvalue** indicates that the FIM is singular, which is a definitive signature of [structural non-identifiability](@entry_id:263509). The corresponding eigenvector reveals the combination of parameters that is unconstrained by the data (e.g., the direction of the $E_0$ parameter) [@problem_id:3413181].
-   A **very small, non-zero eigenvalue** relative to the largest eigenvalue indicates [practical non-identifiability](@entry_id:270178). The ratio of the largest to [smallest eigenvalue](@entry_id:177333) (the condition number) is large, and the model is termed "sloppy." The eigenvector associated with the small eigenvalue points along a "sloppy" direction in [parameter space](@entry_id:178581), corresponding to a combination of parameters that is very poorly constrained by the data. The degree of sloppiness can be quantified by the ratio $S = \lambda_{\min} / \lambda_{\max}$ [@problem_id:3413239].

#### Regularization for Ill-Posed Problems

When a fitting problem is ill-posed, either due to non-identifiability or the use of a highly flexible model (like a tabulated potential), a powerful remedy is **regularization**. Regularization involves adding a penalty term to the [objective function](@entry_id:267263) that encodes prior knowledge or desired properties of the solution, such as smoothness.

Consider fitting a tabulated [pair potential](@entry_id:203104) $V(r)$, where the potential values $v_i = V(r_i)$ at a set of grid points are the parameters. Without constraints, a least-squares fit can produce an unphysically oscillatory potential that overfits the noise in the data. To enforce smoothness, we can add a **Tikhonov regularization** term that penalizes the curvature of the potential. A discrete approximation to the integrated squared second derivative, $\int (V''(r))^2 dr$, can be constructed using a finite-difference approximation on the grid [@problem_id:3413240]. The regularized [objective function](@entry_id:267263) takes the form:

$\Phi(\mathbf{v}) = \frac{1}{2}\|\mathbf{A}\mathbf{v} - \mathbf{y}\|_{\mathbf{W}}^{2} + \frac{\alpha}{2} \|\mathbf{L}\mathbf{v}\|^{2}$

Here, the first term is the standard weighted least-squares [data misfit](@entry_id:748209), and the second is the regularization penalty. $\mathbf{L}$ is a matrix representing the discrete second derivative operator, and $\alpha$ is a hyperparameter that controls the strength of the smoothness penalty.

The effect of this regularization can be understood by examining the Hessian of the new objective, $\mathbf{H} = \mathbf{A}^{\mathsf{T}}\mathbf{W}\mathbf{A} + \alpha \mathbf{L}^{\mathsf{T}}\mathbf{L}$. The data-fitting term, $\mathbf{A}^{\mathsf{T}}\mathbf{W}\mathbf{A}$, may be ill-conditioned or singular. The regularization term, $\alpha \mathbf{L}^{\mathsf{T}}\mathbf{L}$, is designed to "lift" the problematic small eigenvalues of the Hessian. Spectral analysis shows that the eigenvalues of $\mathbf{L}^{\mathsf{T}}\mathbf{L}$ are largest for high-frequency (oscillatory) modes of the potential vector $\mathbf{v}$. Thus, the regularizer selectively penalizes non-smooth solutions, improving the conditioning of the Hessian and guiding the optimization toward a physically plausible, smooth potential that still honors the data [@problem_id:3413240]. This technique is a cornerstone of modern machine learning potentials and other flexible fitting paradigms.