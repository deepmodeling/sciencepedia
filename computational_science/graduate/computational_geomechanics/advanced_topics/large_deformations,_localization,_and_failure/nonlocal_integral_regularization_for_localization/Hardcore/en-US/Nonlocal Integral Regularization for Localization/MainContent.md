## Introduction
The failure of quasi-brittle materials like concrete and rock is often characterized by [strain localization](@entry_id:176973), where deformation concentrates into narrow bands. In classical continuum mechanics, models with [material softening](@entry_id:169591) predict these bands to have zero width, leading to a [pathological mesh dependency](@entry_id:184469) in numerical simulations and an ill-posed mathematical problem. This critical knowledge gap prevents reliable prediction of structural failure. Nonlocal integral regularization emerges as a powerful method to resolve this issue by incorporating a physical length scale directly into the constitutive law, ensuring that simulation results are objective and physically meaningful.

This article provides a comprehensive exploration of the nonlocal integral framework. The journey begins in the **"Principles and Mechanisms"** chapter, where we will dissect the fundamental concept of [spatial averaging](@entry_id:203499), examine the properties of the kernel functions that define the nonlocal interaction, and understand the physical significance of the characteristic length. We will also uncover the analytical underpinnings of regularization through Taylor series expansions and [spectral analysis](@entry_id:143718). Next, the **"Applications and Interdisciplinary Connections"** chapter will demonstrate the model's practical power, showing how it captures phenomena like the size effect, models complex [anisotropic materials](@entry_id:184874), and relates to other advanced frameworks such as [gradient-enhanced models](@entry_id:162584) and Peridynamics. Finally, the **"Hands-On Practices"** section will provide a series of targeted problems, bridging the gap between theory and computation by guiding you through numerical implementation and analysis. This structured approach will equip you with a deep, functional understanding of one of the most important [regularization techniques](@entry_id:261393) in modern [computational geomechanics](@entry_id:747617).

## Principles and Mechanisms

The fundamental premise of integral-type [nonlocal regularization](@entry_id:752666) is to replace a local state variable, which drives material degradation, with its spatially weighted average. This operation introduces a length scale into the constitutive formulation, reflecting the inherent scale of microstructural interactions that are homogenized in classical continuum theories. This section delineates the core principles of this approach, the properties of its components, and the mechanisms by which it restores [well-posedness](@entry_id:148590) to the [boundary value problem](@entry_id:138753).

### The Nonlocal Averaging Principle

In a local continuum model, the evolution of a material state variable, such as damage or plastic strain at a point $\boldsymbol{x}$, is determined solely by quantities defined at that same point. In contrast, an integral nonlocal model postulates that the evolution of the state at $\boldsymbol{x}$ is governed by a regularized field variable, $\bar{q}(\boldsymbol{x})$, which is computed by averaging the [local field](@entry_id:146504), $q(\boldsymbol{\xi})$, over a finite neighborhood of $\boldsymbol{x}$. Mathematically, this is expressed through a convolution integral:

$$
\bar{q}(\boldsymbol{x}) = \int_{\Omega} \alpha(\boldsymbol{x}, \boldsymbol{\xi}) \, q(\boldsymbol{\xi}) \, \mathrm{d}\boldsymbol{\xi}
$$

Here, $\Omega$ is the domain of the body, $\boldsymbol{\xi}$ is the integration variable representing all source points, and $\alpha(\boldsymbol{x}, \boldsymbol{\xi})$ is a weighting function, commonly referred to as the **kernel** or **[influence function](@entry_id:168646)**. This kernel dictates the strength of the interaction between the source point $\boldsymbol{\xi}$ and the receiver point $\boldsymbol{x}$.

A critical consideration is the choice of the local field $q$ to be regularized. The principle of **[material frame indifference](@entry_id:166014)** (or objectivity) requires that [constitutive laws](@entry_id:178936) must be independent of the observer's [rigid body motion](@entry_id:144691). This implies that any quantity subjected to [spatial averaging](@entry_id:203499), which involves points at different locations, must be an objective scalar. Scalar invariants, such as the accumulated equivalent plastic strain or an equivalent strain measure driving damage, are ideal candidates because their values do not depend on the orientation of the coordinate system. Averaging a non-objective quantity, such as a component of a strain or stress tensor, would yield a nonlocal field whose value depends on the observer's frame, violating this fundamental principle and leading to a physically unsound model .

### Kernel Functions: Properties and Design

The [kernel function](@entry_id:145324) is the heart of the [nonlocal operator](@entry_id:752663), and its mathematical properties are crucial for the physical and numerical consistency of the model. For a kernel $w$ that depends only on the distance $r = |\boldsymbol{x} - \boldsymbol{\xi}|$, the following properties are generally required :

1.  **Non-negativity**: $w(r) \ge 0$. This ensures that the nonlocal value is a true weighted average, which is physically intuitive. Kernels that may change sign, such as a sinc function, are generally not suitable as they can lead to non-physical results  .

2.  **Symmetry (Isotropy)**: The kernel is an even function, depending only on the distance $r$. This reflects material isotropy, where the influence of neighboring points is independent of direction.

3.  **Normalization (Partition of Unity)**: The integral of the kernel over its entire support must be unity. For an infinite domain, this is expressed as $\int_{-\infty}^{\infty} w(|r|) \, \mathrm{d}r = 1$. This property ensures that the [nonlocal operator](@entry_id:752663) correctly reproduces a constant field (a "patch test"). If $q(\boldsymbol{\xi}) = q_0$ is a constant, the normalization guarantees that $\bar{q}(\boldsymbol{x}) = q_0$.

4.  **Finite Second Moment**: The second moment of the kernel, $m_2 = \int_{-\infty}^{\infty} r^2 w(|r|) \, \mathrm{d}r$, must be finite. As will be discussed later, this property is essential for the [asymptotic equivalence](@entry_id:273818) to gradient models and ensures that the characteristic length is well-defined. Kernels with "heavy tails" that decay too slowly, such as the Cauchy-Lorentz function, may have an infinite second moment and are therefore unsuitable .

Several functions satisfy these criteria and are commonly used in practice. Two prominent examples are the **Gaussian kernel**:
$$
w(r) = C_A \exp\left(-\frac{r^2}{\ell^2}\right)
$$
and the **exponential kernel**:
$$
w(r) = C_E \exp\left(-\frac{|r|}{\ell}\right)
$$
where $\ell$ is the [characteristic length](@entry_id:265857) and $C_A, C_E$ are normalization constants. Another choice with [compact support](@entry_id:276214) is the **triangular (hat) kernel** .

### The Characteristic Length: Physical Meaning and Calibration

The parameter $\ell$ embedded in the [kernel function](@entry_id:145324) is the **characteristic length** (or internal length). It is the most significant parameter introduced by the [nonlocal regularization](@entry_id:752666).

#### Physical Meaning
The [characteristic length](@entry_id:265857) $\ell$ is not a numerical artifact; it is an **intrinsic material parameter** that represents the length scale of microstructural interactions. In [geomaterials](@entry_id:749838), this can be related to the size of the largest aggregates in concrete, the grain size in rock, or the extent of the micro-cracking zone that precedes the formation of a macroscopic crack—the so-called Fracture Process Zone (FPZ). Consequently, $\ell$ governs the minimum width of any localization band that can form in the material . Any attempt to set $\ell$ as a function of the [numerical discretization](@entry_id:752782) (e.g., the finite element size) is fundamentally flawed, as it would make the material model itself mesh-dependent, defeating the purpose of achieving objective simulations  .

The direct link between $\ell$ and the localization width can be illustrated with a simple example. Consider a one-dimensional bar where a localized strain band of width $w$ and magnitude $\varepsilon_{\mathrm{in}}$ forms symmetrically around $x=0$. Using an exponential kernel $w(r) = (2\ell)^{-1} \exp(-|r|/\ell)$, the nonlocal strain at the center of the band can be calculated as:
$$
\bar{\varepsilon}(0) = \int_{-w/2}^{w/2} \frac{1}{2\ell} \exp\left(-\frac{|\xi|}{\ell}\right) \varepsilon_{\mathrm{in}} \, \mathrm{d}\xi = \varepsilon_{\mathrm{in}} \left( 1 - \exp\left(-\frac{w}{2\ell}\right) \right)
$$
If [material softening](@entry_id:169591) is triggered when $\bar{\varepsilon}(0)$ reaches a threshold $\varepsilon_{\mathrm{th}}$, the required band width $w$ is given by $w = -2\ell \ln(1 - \varepsilon_{\mathrm{th}}/\varepsilon_{\mathrm{in}})$ . This result explicitly shows that for a softening instability to occur, a finite band width $w$ proportional to the internal length $\ell$ is required. The singularity of a zero-width strain band is thus prevented.

#### Calibration
Since $\ell$ is a material property, it must be calibrated from experimental observations. The most robust calibration procedures target physical phenomena that are directly governed by the internal length scale:

-   **Fracture Energy ($G_f$)**: The fracture energy is the energy dissipated per unit area of a crack. In a nonlocal model, the total dissipated energy is approximately the product of the energy dissipated per unit volume (determined by the softening law) and the volume of the localization band. The band's volume is proportional to $\ell$. Therefore, to reproduce a specific material fracture energy $G_f$, the parameters of the local softening law must be scaled with $\ell$. It is incorrect to assume that any choice of softening law will yield an objective $G_f$ simply by virtue of using a nonlocal model with $\ell > 0$ . A consistent model requires a coupled calibration of the softening parameters and $\ell$ to match the target $G_f$  .

-   **Size Effect**: Quasi-brittle materials exhibit a size effect, where the structural strength and post-peak response of geometrically similar specimens change with the absolute size of the structure. This phenomenon is governed by the ratio of the structural dimension to the material's internal length $\ell$. Matching the experimentally observed [size effect law](@entry_id:171636) is a powerful and reliable method for calibrating $\ell$ .

### Application in Bounded Domains: The Challenge of Normalization

When applying the nonlocal integral to a finite body, a complication arises near the boundaries. For a point $\boldsymbol{x}$ close to a boundary, the support of the kernel function is truncated by the domain boundary $\partial\Omega$. If one were to use the [normalization constant](@entry_id:190182) derived for an infinite domain, the integral of the kernel over the truncated domain would be less than one: $\int_{\Omega} w(|\boldsymbol{x}-\boldsymbol{\xi}|) \, \mathrm{d}\boldsymbol{\xi}  1$.

This violation of the [partition of unity](@entry_id:141893) has a significant physical consequence: it causes an artificial stiffening of the material response near boundaries, as a constant field would be mapped to a smaller value . This can spuriously affect where localization initiates and progresses.

To ensure the model is consistent everywhere, especially if localization can occur near boundaries, a **position-dependent [renormalization](@entry_id:143501)** is required. The [nonlocal operator](@entry_id:752663) is redefined using a corrected kernel $\alpha(x,\xi)$:
$$
\bar{q}(x) = \int_{\Omega} \frac{w(|x-\xi|)}{C(x)} q(\xi) \, \mathrm{d}\xi, \quad \text{where} \quad C(x) = \int_{\Omega} w(|x-\xi|) \, \mathrm{d}\xi
$$
This procedure guarantees that the [normalization condition](@entry_id:156486) $\int_{\Omega} \alpha(x,\xi) \, \mathrm{d}\xi = 1$ is satisfied for every point $x \in \Omega$, thus ensuring the correct reproduction of constant fields throughout the entire domain  .

For a 1D bar on the domain $\Omega=[0,L]$ with an exponential kernel $w(r) = \exp(-r/\ell)$, the position-dependent normalization factor $C(x)$ can be calculated explicitly:
$$
C(x) = \int_0^L \exp\left(-\frac{|x-\xi|}{\ell}\right) \mathrm{d}\xi = \ell \left( 2 - e^{-x/\ell} - e^{-(L-x)/\ell} \right)
$$
As expected, for a point $x$ deep inside the domain ($x \gg \ell$ and $L-x \gg \ell$), the exponential terms vanish and $C(x)$ approaches $2\ell$, which is the integral of the unnormalized kernel over the infinite line, $\int_{-\infty}^{\infty} \exp(-|r|/\ell) \mathrm{d}r = 2\ell$ .

### Analytical Mechanisms of Regularization

The regularizing effect of the nonlocal integral can be understood through two key analytical perspectives: its relationship to [gradient-enhanced models](@entry_id:162584) and its filtering properties in Fourier space.

#### Asymptotic Equivalence to Gradient Models

For a smooth local field $\varepsilon(x)$, the nonlocal integral can be analyzed by performing a Taylor series expansion of $\varepsilon(\xi)$ around the point $x$. Let us consider the integral in the form $\bar{\varepsilon}(x) = \int_{-\infty}^{\infty} w(r)\varepsilon(x+r)\mathrm{d}r$, where $w(r)$ is an even, normalized kernel. Expanding $\varepsilon(x+r)$ around $r=0$:
$$
\varepsilon(x+r) = \varepsilon(x) + r\varepsilon'(x) + \frac{r^2}{2}\varepsilon''(x) + O(r^3)
$$
Substituting this into the integral yields:
$$
\bar{\varepsilon}(x) = \varepsilon(x) \int_{-\infty}^{\infty} w(r)\mathrm{d}r + \varepsilon'(x) \int_{-\infty}^{\infty} r w(r)\mathrm{d}r + \frac{\varepsilon''(x)}{2} \int_{-\infty}^{\infty} r^2 w(r)\mathrm{d}r + \dots
$$
Due to the normalization and symmetry of $w(r)$, the [first integral](@entry_id:274642) is 1 and the second integral (the first moment) is 0. Truncating at the second-order term, we obtain the gradient approximation  :
$$
\bar{\varepsilon}(x) \approx \varepsilon(x) + \left(\frac{m_2}{2}\right) \varepsilon''(x)
$$
where $m_2 = \int_{-\infty}^{\infty} r^2 w(r)\mathrm{d}r$ is the second moment of the kernel. This reveals that, to second order, the integral model is equivalent to an implicit gradient model of the form $\bar{\varepsilon}(x) \approx \varepsilon(x) + \ell_g^2 \varepsilon''(x)$, with the squared gradient length parameter given by $\ell_g^2 = m_2/2$. This connection highlights the importance of the kernel's finite second moment. For the exponential kernel $w(r) = (2\ell)^{-1} \exp(-|r|/\ell)$, the second moment is $m_2 = 2\ell^2$, which gives a gradient length $\ell_g = \ell$ . This equivalence provides a clear link between the integral formulation and differential regularization models .

#### Spectral Analysis and Stabilization of Short Wavelengths

The most profound insight into the regularization mechanism comes from spectral (Fourier) analysis. The nonlocal averaging, being a convolution, has a simple representation in Fourier space. If $\hat{q}(k)$ is the Fourier transform of the [local field](@entry_id:146504) $q(x)$, then the Fourier transform of the nonlocal field, $\hat{\bar{q}}(k)$, is given by the product:
$$
\hat{\bar{q}}(k) = \hat{w}(k) \hat{q}(k)
$$
where $\hat{w}(k)$ is the Fourier transform of the [kernel function](@entry_id:145324). This function $\hat{w}(k)$, also called the transfer function or symbol, modulates the amplitude of each harmonic component of the local field based on its [wavenumber](@entry_id:172452) $k$.

For the common kernels used in regularization, $\hat{w}(k)$ acts as a **[low-pass filter](@entry_id:145200)**:
-   For long wavelengths ($k \to 0$), $\hat{w}(k) \to 1$. The [nonlocal operator](@entry_id:752663) preserves large-scale features of the field.
-   For short wavelengths ($k \to \infty$), $\hat{w}(k) \to 0$. The operator strongly attenuates or damps high-frequency oscillations.

For instance, the Fourier transform of the Gaussian kernel $w(r) = (\sqrt{\pi}\ell)^{-1} \exp(-r^2/\ell^2)$ is $\hat{w}(k) = \exp(-k^2 \ell^2/4)$ . For the exponential kernel $w(r) = (2\ell)^{-1}\exp(-|r|/\ell)$, it is $\hat{w}(k) = (1 + k^2 \ell^2)^{-1}$ . Both exhibit the characteristic [low-pass filter](@entry_id:145200) behavior.

This filtering property is the key to stabilizing the short-wavelength instabilities that plague local softening models. Consider an incremental [constitutive relation](@entry_id:268485) linearized around a homogeneous state, which for a harmonic perturbation $\delta\varepsilon(x)$ gives an incremental stress $\delta\sigma(x) = E_{\mathrm{eff}}(k) \delta\varepsilon(x)$. The effective tangent modulus $E_{\mathrm{eff}}(k)$ depends on the wavenumber $k$. A typical form derived from a [nonlocal damage model](@entry_id:181532) is :
$$
E_{\mathrm{eff}}(k) = E_{\mathrm{loc}} \left[ 1 - r \hat{w}(k) \right]
$$
where $E_{\mathrm{loc}}$ is the local tangent modulus (positive) and $r > 1$ is a parameter indicating that the material is in the softening regime.

In a local model, $\ell=0$, so $\hat{w}(k)=1$ for all $k$. This gives $E_{\mathrm{eff}}(k) = E_{\mathrm{loc}}(1-r)  0$, meaning perturbations of all wavelengths are unstable. In the nonlocal model, as $k \to \infty$, $\hat{w}(k) \to 0$, and thus $E_{\mathrm{eff}}(k) \to E_{\mathrm{loc}} > 0$. The material model remains stiff for very short wavelengths, preventing their unbounded growth.

Instability ($E_{\mathrm{eff}}(k)  0$) is confined to a range of low wavenumbers. The boundary of this unstable range is defined by a **critical wavenumber** $k_c$ where the stiffness vanishes: $E_{\mathrm{eff}}(k_c) = 0$. This leads to the condition $1 - r \hat{w}(k_c) = 0$. For wavenumbers $|k|  k_c$, perturbations can grow, while for $|k| > k_c$, they are stabilized. The existence of a non-zero critical [wavenumber](@entry_id:172452) $k_c$ implies that the instability will manifest with a finite, characteristic wavelength of the order of $2\pi/k_c$, which corresponds to the finite width of the localization band. For the Gaussian kernel, the dimensionless critical [wavenumber](@entry_id:172452) $\eta_c = k_c \ell / 2$ is found to be $\eta_c = \sqrt{\ln(r)}$ . This elegant result demonstrates how the [nonlocal regularization](@entry_id:752666) transforms an ill-posed problem, unstable at all scales, into a well-posed one with a selected, finite-width failure mode.