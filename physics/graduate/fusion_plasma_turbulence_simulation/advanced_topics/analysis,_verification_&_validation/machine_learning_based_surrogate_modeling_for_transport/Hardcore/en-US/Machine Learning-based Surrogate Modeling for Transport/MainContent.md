## Introduction
In the quest for fusion energy, accurately predicting the behavior of magnetically [confined plasmas](@entry_id:1122875) over long timescales is a paramount challenge. This task is complicated by turbulent transport—a phenomenon driven by small-scale instabilities that is computationally prohibitive to simulate directly within macroscopic transport codes. Machine learning-based surrogate models have emerged as a powerful solution, offering a data-driven bridge between high-fidelity physics and practical, large-scale simulation. This article provides a graduate-level exploration of these advanced computational tools, addressing the critical need for fast yet physically reliable transport models.

The journey begins in the **Principles and Mechanisms** chapter, where we will deconstruct the surrogate model, examining its role as a physical closure, the methods for encoding fundamental transport physics like critical gradients, and the techniques for ensuring physical consistency. Next, the **Applications and Interdisciplinary Connections** chapter demonstrates the real-world utility of these models, covering their integration into complex transport solvers, their application in [uncertainty quantification](@entry_id:138597), and their relevance to other scientific domains. Finally, the **Hands-On Practices** chapter offers practical exercises to reinforce these concepts, allowing you to build and validate your own [physics-informed models](@entry_id:753434). By the end of this article, you will have a comprehensive understanding of how to build, validate, and deploy [surrogate models](@entry_id:145436) to accelerate scientific discovery in fusion energy and beyond.

## Principles and Mechanisms

### The Surrogate Model as a Physical Closure

In the [predictive modeling](@entry_id:166398) of magnetically confined fusion plasmas, a central challenge lies in bridging the vast separation of scales between the rapid, small-scale turbulent motions that drive transport and the slow, macroscopic evolution of plasma profiles. While first-principles models like gyrokinetics provide a high-fidelity description of turbulence, their computational expense prohibits their direct use in long-time transport simulations. Surrogate models offer a solution by providing a computationally inexpensive, data-driven approximation of the turbulent transport response.

Fundamentally, a surrogate acts as a **[closure relation](@entry_id:747393)** within a system of macroscopic transport equations. Consider, for example, the evolution of the [ion temperature](@entry_id:191275) $T_i$ described by the flux-surface averaged conservation law:

$$
\partial_t \! \left(\frac{3}{2} n_i T_i\right) + \frac{1}{V'(\psi)} \frac{\partial}{\partial \psi} \left(V'(\psi) Q_i(\psi,t)\right) = S_i(\psi,t)
$$

Here, $\psi$ is a radial flux coordinate, $n_i$ is the ion density, $Q_i$ is the radial ion heat flux density, $V'(\psi)$ is the differential flux-surface volume, and $S_i$ represents heat [sources and sinks](@entry_id:263105). To solve this equation, a closure is needed—a model that specifies the [turbulent flux](@entry_id:1133512) $Q_i$ as a function of the plasma state. The surrogate model provides this closure, acting as a map $f: \mathcal{X} \to \mathcal{Y}$ from a space of plasma state parameters, $\mathcal{X}$, to a space of turbulent fluxes or transport coefficients, $\mathcal{Y}$ .

The construction of the input space $\mathcal{X}$, or the process of **feature engineering**, is paramount for creating a physically meaningful and generalizable surrogate. The governing gyrokinetic equations possess certain similarity properties, which can be expressed in terms of a set of [dimensionless parameters](@entry_id:180651). By training a surrogate on these dimensionless features, we embed fundamental physical scaling laws, enabling the model to generalize across different devices and operating regimes. The canonical set of local dimensionless parameters includes :

*   **Normalized gradient scale lengths**, $R/L_X \equiv -R (1/X) dX/dr$ for $X \in \{T_i, T_e, n\}$, which represent the free energy gradients that drive turbulence.
*   **Safety factor $q$ and magnetic shear $\hat{s} \equiv (r/q) dq/dr$**, which describe the magnetic field geometry and its radial variation, critical for mode stability and saturation.
*   **Normalized gyroradius $\rho^* = \rho_i/a$**, the ratio of the ion Larmor radius to the machine size, which sets the fundamental scale of turbulence and governs gyro-Bohm scaling ($Q \propto \rho^{*2}$).
*   **Plasma beta $\beta \equiv 2\mu_0 n T/B^2$**, the ratio of plasma pressure to magnetic pressure, which quantifies the importance of electromagnetic effects.
*   **Normalized collisionality $\nu^*$**, which compares the collision frequency to characteristic orbital frequencies and determines the role of [collisional damping](@entry_id:202128).

Based on the structure of the map $f$, we can distinguish two primary [surrogate modeling](@entry_id:145866) paradigms :

1.  **Local (or Scalar) Surrogates**: These models implement a pointwise map, $f: \mathbb{R}^d \to \mathbb{R}^m$. The input is a vector of local [dimensionless parameters](@entry_id:180651) at a single radial position $\psi$, and the output is a vector of local fluxes or [transport coefficients](@entry_id:136790) at that same position. This approach assumes that transport is determined solely by local plasma conditions, a common but not universally valid assumption.

2.  **Nonlocal (or Operator) Surrogates**: These models are mathematically formulated as operators acting on [function spaces](@entry_id:143478), $\mathcal{F}: \mathcal{H} \to \mathcal{H}$. They take entire radial profiles of input parameters (e.g., $T_i(\psi)$, $q(\psi)$) and map them to entire radial profiles of output fluxes (e.g., $Q_i(\psi)$). This structure allows the flux at one location, $\psi$, to depend on plasma parameters at other locations, $\psi'$, capturing **nonlocal transport effects** that are known to arise from the [large-scale structure](@entry_id:158990) of turbulent eddies or the propagation of turbulence from one region to another.

### Encoding Fundamental Transport Physics

A successful surrogate must do more than simply fit data; it must faithfully reproduce the key physical phenomena of turbulent transport. Two such phenomena are the existence of [critical gradient](@entry_id:748055) thresholds and the fundamental connection between transport and instability drives.

#### Critical Gradient Thresholds

Many forms of plasma microturbulence, such as the **Ion Temperature Gradient (ITG)** mode, are characterized by an instability threshold. The instability is driven by the free energy in the temperature gradient, but it is only triggered when the normalized gradient $R/L_{T_i}$ exceeds a certain **critical gradient**, $(R/L_{T_i})_{\text{crit}}$ . The conditions for stability are:
*   $R/L_{T_i} \le (R/L_{T_i})_{\text{crit}}$: The plasma is stable, and turbulent transport is suppressed ($Q_i \approx 0$).
*   $R/L_{T_i} > (R/L_{T_i})_{\text{crit}}$: The plasma is unstable, leading to turbulence and a non-zero heat flux, $Q_i > 0$.

This threshold behavior results in a highly nonlinear, "stiff" transport response. A physically valid surrogate model for $Q_i$ must capture this stiffness. The model's output should be negligible for subcritical gradients and should increase sharply as the gradient becomes supercritical. The model should learn to predict the flux as a nonlinear function of the **supercriticality**, defined as the difference $R/L_{T_i} - (R/L_{T_i})_{\text{crit}}$. This is a crucial piece of physics that a purely linear model would fail to capture.

#### Quasilinear Dynamics as a Physical Prior

The connection between transport and [linear instability](@entry_id:1127282) can be formalized through **[quasilinear theory](@entry_id:753966)**. For weakly nonlinear, electrostatic turbulence, the ion heat flux can be derived from the linearized [gyrokinetic equation](@entry_id:1125856). This leads to a spectral expression for the flux of the form :

$$
Q_i \propto \sum_k C_k \, \gamma_k |\phi_k|^2
$$

Here, the sum is over all [unstable modes](@entry_id:263056) with wavenumber $k$. The flux contribution from each mode is proportional to its **[linear growth](@entry_id:157553) rate** $\gamma_k$ and its saturated amplitude squared $|\phi_k|^2$. This expression reveals a fundamental principle: turbulent transport is a direct consequence of growing instabilities ($\gamma_k > 0$). In the absence of a free-energy drive, all modes are stable ($\gamma_k \le 0$), and the [turbulent flux](@entry_id:1133512) vanishes.

This theoretical result provides a powerful physical prior for [surrogate modeling](@entry_id:145866). While a full surrogate aims to capture more complex nonlinear effects beyond this simple model (such as the determination of the saturated amplitude $|\phi_k|^2$ through [nonlinear saturation](@entry_id:1128869) rules), the quasilinear form suggests that the linear growth rates $\gamma_k$ are highly informative features. A surrogate can be trained to learn the mapping from fundamental dimensionless parameters to fluxes, implicitly learning this connection, or it could even use pre-computed linear stability properties as direct inputs.

### Methodologies for Surrogate Construction: A Bayesian Perspective

A variety of machine learning techniques can be employed to build [surrogate models](@entry_id:145436). Among the most powerful and physically appealing are Bayesian methods, such as **Gaussian Process (GP) regression**, which provide not only predictions but also principled uncertainty estimates.

A Gaussian Process defines a prior distribution over functions. A function $f(\mathbf{x})$ is said to be drawn from a GP, written $f(\mathbf{x}) \sim \mathcal{GP}(m(\mathbf{x}), k(\mathbf{x}, \mathbf{x}'))$, if any finite collection of its values has a joint multivariate Gaussian distribution. The GP is fully specified by a mean function $m(\mathbf{x})$ and a covariance or **[kernel function](@entry_id:145324)** $k(\mathbf{x}, \mathbf{x}')$ . The kernel encodes our prior beliefs about the properties of the function, such as its smoothness and [characteristic length scales](@entry_id:266383).

Given a set of training data (noisy observations of the true flux), the GP prior can be updated to a posterior distribution. The posterior provides a predictive distribution for the flux at any new input point, characterized by a [posterior mean](@entry_id:173826) (the prediction) and a posterior variance (the uncertainty).

The choice of kernel is where physical insight can be directly embedded into the model :

*   **Smoothness**: The [differentiability](@entry_id:140863) of the function is controlled by the kernel. For instance, the Matérn family of kernels has a parameter $\nu$ that directly controls the mean-square [differentiability](@entry_id:140863) of the function. This allows us to encode prior knowledge about how smooth we expect the transport response to be.
*   **Feature Relevance**: The **Automatic Relevance Determination (ARD)** mechanism assigns a separate characteristic length-scale, $l_j$, to each input feature $x_j$. After training, a small length-scale indicates that the function varies rapidly along that dimension, implying the feature is highly relevant. A large length-scale implies the feature has little influence. This provides a data-driven way to discover the most important physical parameters.
*   **Periodicity**: For inputs that are naturally periodic, such as geometric angles in a tokamak, a periodic kernel can be used to enforce the corresponding symmetry in the surrogate's predictions, ensuring that $f(x) = f(x+P)$ for some period $P$.

### Ensuring Physical Consistency: Constraints and Symmetries

A purely data-driven surrogate, trained only to minimize prediction error, can easily produce outputs that violate fundamental physical laws, especially when extrapolating outside its training domain. Such violations can lead to unphysical results and [numerical instability](@entry_id:137058) when the surrogate is coupled to a transport solver. Therefore, it is essential to enforce physical consistency.

#### System-Level Constraints
When a local surrogate is integrated into a global transport code, several system-level constraints become critical for a stable and physical evolution :

1.  **Conservative Form**: The surrogate must predict fluxes that are then used within a divergence operator. It must not introduce spurious source or sink terms.
2.  **Ambipolarity**: In steady-state, the net radial electric current must vanish to maintain [quasineutrality](@entry_id:184567). This imposes the **[ambipolarity](@entry_id:746396) constraint** on particle fluxes: $\sum_s Z_s e \Gamma_{s,r} = 0$. For a simple electron-ion plasma ($Z_i=1$), this simplifies to $\Gamma_{i,r} = \Gamma_{e,r}$ . A multi-channel surrogate predicting particle fluxes must satisfy this condition.
3.  **Galilean Invariance**: The laws of physics are independent of the observer's [inertial frame](@entry_id:275504). Consequently, turbulent momentum flux must depend on velocity *gradients* (shear), not on the absolute bulk velocity of the plasma.

#### Thermodynamic Consistency
The Second Law of Thermodynamics dictates that the irreversible entropy production from turbulence must be non-negative. This translates into a mathematical constraint on the [transport matrix](@entry_id:756135) $D$ that relates thermodynamic forces $g$ (gradients) to fluxes $F$ via a [linear response](@entry_id:146180) model $F = -Dg$. The entropy production rate is proportional to $\sigma = g^T D g$, and the condition $\sigma \ge 0$ requires the symmetric part of the [transport matrix](@entry_id:756135), $S = \frac{1}{2}(D + D^T)$, to be **positive semidefinite** .

Several strategies exist to enforce such physical constraints :

*   **Constrained Architectures**: Design the neural network architecture such that its output is guaranteed to satisfy the constraint. For the positive semidefinite requirement on $S$, one can parameterize the [transport matrix](@entry_id:756135) as $D(x) = B(x)^T B(x) + A(x)$, where $B(x)$ is a general matrix produced by the network and $A(x)$ is a skew-symmetric matrix. This structure inherently guarantees that the symmetric part $S = B^T B$ is positive semidefinite.

*   **Physics-Informed Loss Functions**: Augment the standard data-fitting loss function with a penalty term that punishes violations of physical laws. For the entropy constraint, one could add a term like $\mathcal{L}_{\text{entropy}} = \max(0, -\lambda_{\min}(S))$, where $\lambda_{\min}(S)$ is the minimum eigenvalue of the symmetric part of the predicted [transport matrix](@entry_id:756135). This "soft" constraint guides the training towards a physically consistent solution.

*   **Post-hoc Projection**: Train an unconstrained surrogate and then, at inference time, project its output onto the physically valid manifold. For instance, if a surrogate predicts ion and electron fluxes $\mu_i$ and $\mu_e$ with variances $\sigma_i^2$ and $\sigma_e^2$ that violate [ambipolarity](@entry_id:746396), one can find the single, enforced flux $\Gamma^\star$ that is most consistent with both predictions by solving a weighted [least-squares problem](@entry_id:164198). This yields the inverse-variance weighted average :
    $$
    \Gamma^{\star} = \frac{ \mu_{i}/\sigma_{i}^{2} + \mu_{e}/\sigma_{e}^{2} }{ 1/\sigma_{i}^{2} + 1/\sigma_{e}^{2} }
    $$

#### Impact on Numerical Stability
Enforcing physical consistency is not merely an aesthetic choice; it is often crucial for the [numerical stability](@entry_id:146550) of the transport solver. Consider a surrogate for diffusivity $\hat{\chi}$ used in a stiff transport PDE. The error of the surrogate can be decomposed into bias and variance. While machine learning typically focuses on minimizing total mean squared error, the *structure* of the error is critical for stability . High variance in the surrogate's prediction means there is a non-zero probability of sampling a physically pathological value, such as a **negative diffusivity** ($\hat{\chi}  0$). A negative diffusivity corresponds to anti-diffusion, which can destabilize even numerically robust implicit time-stepping schemes. In contrast, a surrogate with a small, controlled positive bias and low variance might have a slightly higher MSE but will be far more stable, as it avoids predicting unphysical, destabilizing values. This illustrates the importance of the **bias-variance tradeoff** in the context of [physics-informed modeling](@entry_id:166564): a small sacrifice in data-fitting accuracy can yield a dramatic improvement in the stability and reliability of the coupled simulation.

### Operating Within the Domain of Validity

A surrogate model is only reliable within its domain of validity—the region of the input space that is well-represented by the training data. Making predictions for inputs far from this domain constitutes **extrapolation**, where the model's output is highly uncertain and likely unphysical. A critical component of a surrogate modeling workflow is therefore **Out-of-Distribution (OOD) detection**: a mechanism to flag inputs for which the model's prediction cannot be trusted.

A robust definition of the model's valid domain should be based on the distribution of data in the **learned feature space** $\mathbb{R}^d$ of the neural network, not the original input space $\mathbb{R}^p$ . An input is considered in-distribution (an interpolation point) if its [feature vector](@entry_id:920515) $\mathbf{z} = \phi(\mathbf{x})$ lies in a high-density region of the training feature distribution.

A practical method for OOD detection can be implemented as follows :
1.  Fit a density model, such as a Gaussian Mixture Model (GMM), $\hat{p}(\mathbf{z})$, to the feature vectors of the training data, $\{\mathbf{z}_i\}_{i=1}^N$.
2.  Use the **[negative log-likelihood](@entry_id:637801) (NLL)**, $\ell(\mathbf{z}) = -\log \hat{p}(\mathbf{z})$, as an OOD score. High NLL corresponds to low data density.
3.  To set a decision threshold, compute the NLL scores for all training points, $\{\ell(\mathbf{z}_i)\}_{i=1}^N$.
4.  Choose the threshold $\tau_\alpha^\ell$ as the $(1-\alpha)$-quantile of these empirical scores.
5.  At deployment, for a new input $\mathbf{x}_*$, compute its score $\ell(\phi(\mathbf{x}_*))$. If the score exceeds the threshold $\tau_\alpha^\ell$, flag the input as OOD.

This method allows a user to specify a desired false alarm rate $\alpha$—the fraction of true in-distribution points that will be incorrectly flagged as OOD. It provides a principled, quantitative way to assess the reliability of a surrogate's prediction at runtime, which is an indispensable tool for the safe and effective use of machine learning in scientific simulation.