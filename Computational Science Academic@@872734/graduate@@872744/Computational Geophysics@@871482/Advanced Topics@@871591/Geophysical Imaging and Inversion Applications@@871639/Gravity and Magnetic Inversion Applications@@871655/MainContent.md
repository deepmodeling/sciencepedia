## Introduction
Gravity and magnetic surveys are foundational tools in [geophysics](@entry_id:147342), providing a non-invasive window into the Earth's subsurface structure. However, the raw data they produce—subtle variations in the gravitational and magnetic fields—are only an indirect expression of the underlying geology. The central challenge, and the core topic of this article, is the inverse problem: how can we transform these surface measurements into a reliable three-dimensional model of physical properties like density and [magnetic susceptibility](@entry_id:138219)? This article provides a comprehensive guide to modern gravity and [magnetic inversion](@entry_id:751628). We will first establish the theoretical foundation in the **Principles and Mechanisms** chapter, exploring the physics of the forward problem and the mathematical necessity of regularization. Next, in **Applications and Interdisciplinary Connections**, we will examine how these principles are applied in practice, from advanced data processing and [joint inversion](@entry_id:750950) to uncertainty quantification. Finally, the **Hands-On Practices** section offers practical exercises to solidify understanding and build key computational skills, bridging the gap between theory and application.

## Principles and Mechanisms

This chapter delves into the fundamental principles and operative mechanisms that govern gravity and [magnetic inversion](@entry_id:751628). We will begin by constructing the forward problem, which mathematically describes how a given subsurface distribution of physical properties generates an observable geophysical signal. We will then explore the inherent challenges of the inverse problem—recovering the subsurface structure from these signals—and introduce the rigorous mathematical framework of regularization required to find stable and geologically meaningful solutions. Finally, we will discuss methods for appraising the quality and limitations of these solutions.

### The Forward Problem: From Physical Laws to Linear Operators

The [forward problem](@entry_id:749531) in potential field geophysics consists of predicting the gravitational or magnetic field at a set of observation points, given a known distribution of mass density or magnetic sources. This process is the foundation upon which the [inverse problem](@entry_id:634767) is built.

#### Governing Equations and Potential Fields

The gravitational field is rooted in Newton's law of [universal gravitation](@entry_id:157534). For a continuous mass density distribution, $\rho(\mathbf{r})$, the relationship between the gravitational potential, $\Phi(\mathbf{r})$, and the density is described by **Poisson's equation**. This fundamental local relationship can be derived from first principles, namely Newton's law for a [point mass](@entry_id:186768) and the [divergence theorem](@entry_id:145271). For a [point mass](@entry_id:186768) $M$ at the origin, the gravitational field is $\mathbf{g}(\mathbf{r}) = -G M \mathbf{r} / |\mathbf{r}|^3$. By applying the divergence theorem to the flux of this field through a closed surface, we arrive at the [differential form](@entry_id:174025), $\nabla \cdot \mathbf{g} = -4\pi G \rho$. Since the gravitational field is conservative ($\nabla \times \mathbf{g} = \mathbf{0}$), it can be expressed as the negative gradient of a scalar potential, $\mathbf{g} = -\nabla\Phi$. Substituting this into the previous expression yields Poisson's equation for gravity [@problem_id:3601372]:

$$
\nabla^2 \Phi(\mathbf{r}) = 4\pi G \rho(\mathbf{r})
$$

Here, $\nabla^2$ is the Laplacian operator, and $G$ is the universal gravitational constant. This equation states that the Laplacian of the [gravitational potential](@entry_id:160378) at any point is directly proportional to the mass density at that same point. In regions free of anomalous mass ($\rho=0$), this simplifies to **Laplace's equation**, $\nabla^2 \Phi = 0$. For this forward problem to be well-posed, we must assume that the density distribution $\rho(\mathbf{r})$ is of [compact support](@entry_id:276214) (i.e., confined to a finite volume) and that the potential vanishes at infinity, $\lim_{|\mathbf{r}| \to \infty} \Phi(\mathbf{r}) = 0$.

The physics of [magnetostatics](@entry_id:140120) presents both similarities and crucial differences. In regions free of electrical currents, as is the case for most geophysical applications, Ampère's law simplifies to $\nabla \times \mathbf{H} = \mathbf{0}$, where $\mathbf{H}$ is the [magnetic field intensity](@entry_id:197932). This implies that $\mathbf{H}$ is also a [conservative field](@entry_id:271398) and can be represented by a [magnetic scalar potential](@entry_id:185708), $\phi_m$, such that $\mathbf{H} = -\nabla\phi_m$. However, a key distinction from gravity arises from Gauss's law for magnetism, which states that there are no [magnetic monopoles](@entry_id:142817): $\nabla \cdot \mathbf{B} = 0$, where $\mathbf{B}$ is the [magnetic flux density](@entry_id:194922). Using the [constitutive relation](@entry_id:268485) $\mathbf{B} = \mu_0(\mathbf{H} + \mathbf{M})$, where $\mu_0$ is the [permeability of free space](@entry_id:276113) and $\mathbf{M}$ is the [magnetization vector](@entry_id:180304), we find that the [magnetic scalar potential](@entry_id:185708) also obeys a Poisson-type equation [@problem_id:3601352]:

$$
\nabla^2 \phi_m = \nabla \cdot \mathbf{M}
$$

Comparing the two, we see a fundamental difference in the source terms. For gravity, the source of the potential field is the [scalar density](@entry_id:161438), $\rho$. For magnetics, the source is the *divergence* of the vector magnetization, $\nabla \cdot \mathbf{M}$. This quantity, sometimes called the effective magnetic charge density, involves a differential operator acting on the source property. This distinction has profound implications for the non-uniqueness and characteristics of the [inverse problem](@entry_id:634767) for each method.

#### Discretization and the Forward Operator

To solve these problems computationally, we discretize the subsurface into a set of cells or voxels, typically rectangular [prisms](@entry_id:265758), within which the physical property ([density contrast](@entry_id:157948) or magnetic susceptibility) is assumed to be constant. The total measured field is then the linear superposition of the contributions from all cells.

For gravity, the observable is often the vertical component of the gravitational acceleration, $g_z$. This is related to the potential by $g_z(\mathbf{r}) = \partial \Phi(\mathbf{r}) / \partial z$ (assuming $z$ is positive downwards). The integral form for $g_z$ at an observation point $\mathbf{r}_i$ due to a density distribution $\rho(\mathbf{r}')$ is:

$$
g_z(\mathbf{r}_i) = G \int_V \rho(\mathbf{r}') \frac{z_i - z'}{|\mathbf{r}_i - \mathbf{r}'|^3} dV'
$$

If we discretize the subsurface into $N_m$ prisms, each with a constant [density contrast](@entry_id:157948) $m_j$, the measurement at the $i$-th location becomes a sum:

$$
d_i = \sum_{j=1}^{N_m} m_j \left( G \int_{V_j} \frac{z_i - z'}{|\mathbf{r}_i - \mathbf{r}'|^3} dV' \right)
$$

This can be written as a [linear matrix equation](@entry_id:203443), $\mathbf{d} = \mathbf{G}\mathbf{m}$, where $\mathbf{d} \in \mathbb{R}^{N_d}$ is the vector of $N_d$ data measurements, $\mathbf{m} \in \mathbb{R}^{N_m}$ is the vector of model parameters (the density contrasts), and $\mathbf{G} \in \mathbb{R}^{N_d \times N_m}$ is the **sensitivity matrix** or **forward operator**. Each element $G_{ij}$ of this matrix represents the sensitivity of the $i$-th datum to the $j$-th model parameter. From the equation above, it is clear that $G_{ij}$ is precisely the integral of the gravity kernel over the volume of the $j$-th prism, representing the gravity effect at point $i$ for a prism $j$ with unit density [@problem_id:3601367].

For a right rectangular prism, this integral can be solved analytically. The resulting [closed-form expression](@entry_id:267458), first derived by Nagy (1966), allows for the efficient and exact computation of the forward response. The solution is expressed as a triple summation over the eight corners of the prism [@problem_id:3601361]:

$$
G_{ij} = -G \sum_{l=1}^2 \sum_{k=1}^2 \sum_{p=1}^2 (-1)^{l+k+p} \left[ x_l \ln(y_k + r_{lkp}) + y_k \ln(x_l + r_{lkp}) - z_p \arctan\left(\frac{x_l y_k}{z_p r_{lkp}}\right) \right]
$$

where $x_l, y_k, z_p$ are the signed offsets from the observation point to the corner coordinates of the prism, and $r_{lkp}$ is the distance to the corner. This formula is a fundamental building block in many [gravity inversion](@entry_id:750042) codes.

The kernel of the forward operator for vertical gravity, $K \propto (z_i - z') / |\mathbf{r}_i - \mathbf{r}'|^3$, has specific properties that influence the inversion. It is not radially symmetric but has a dipole-like character. In the [far-field](@entry_id:269288) regime, its magnitude decays as the inverse square of the distance, $|G_{ij}| \propto R_{ij}^{-2}$, where $R_{ij}$ is the distance from receiver to cell. For observations at a fixed height, the sensitivity decays as the inverse cube of the lateral distance, $|G_{ij}| \propto r_{\text{lat}}^{-3}$ [@problem_id:3601392]. This rapid decay of sensitivity with distance is a primary source of the challenges in inversion.

### The Inverse Problem: Inherent Ill-Posedness

The [inverse problem](@entry_id:634767)—determining the model parameters $\mathbf{m}$ from the data vector $\mathbf{d}$—is significantly more challenging than the forward problem. Geophysical inverse problems are almost always **ill-posed**. A problem is considered well-posed in the sense of Hadamard if a solution exists, is unique, and depends continuously on the data. Inverse problems in gravity and magnetics typically violate the conditions of uniqueness and, most critically, stability [@problem_id:3601389].

The lack of stability can be understood by examining the physics of potential fields in the frequency domain. A potential field measured at an altitude $z_0$ above a source plane can be seen as an **[upward continuation](@entry_id:756371)** of the field from the source level. In the horizontal Fourier domain, this operation corresponds to multiplying the field's spectrum by a factor of $\exp(-|\mathbf{k}|z_0)$, where $\mathbf{k}$ is the horizontal wavenumber vector. This exponential term acts as a strong **low-pass filter**: high-[wavenumber](@entry_id:172452) (short-wavelength) components of the source field are severely attenuated with observation height.

The inverse process, which involves inferring the source-level field from the observed data, is equivalent to downward continuation. In the Fourier domain, this requires dividing by $\exp(-|\mathbf{k}|z_0)$, or multiplying by $\exp(|\mathbf{k}|z_0)$. This inverse operator is a [high-pass filter](@entry_id:274953) that exponentially amplifies high-frequency content. Since any real-world measurement contains noise, the high-frequency components of this noise will be catastrophically amplified, completely overwhelming the signal and rendering the solution unstable. This violation of continuous dependence on the data—where a small perturbation in the data (noise) leads to an arbitrarily large change in the solution—is the essence of the [ill-posedness](@entry_id:635673) of potential field inversion [@problem_id:3601389].

From a functional analysis perspective, the forward operator $\mathbf{G}$ is a **[compact operator](@entry_id:158224)**. A key property of such operators is that they have a sequence of singular values that converges to zero. The inverse operator, $\mathbf{G}^{-1}$, would have singular values that are the reciprocal of these, meaning they would grow without bound. An unbounded inverse directly corresponds to the violation of Hadamard's stability condition [@problem_id:3601389].

### Regularization: Taming the Ill-Posed Problem

To overcome [ill-posedness](@entry_id:635673), we must introduce additional information or constraints to select a single, stable, and geologically plausible solution from the infinite family of models that may fit the data. This process is called **regularization**.

The most common approach is **Tikhonov regularization**. Instead of simply minimizing the [data misfit](@entry_id:748209), we minimize a composite objective function that includes both a [data misfit](@entry_id:748209) term and a model objective (or regularization) term:

$$
\Phi(\mathbf{m}) = \Phi_d(\mathbf{m}) + \lambda^2 \Phi_m(\mathbf{m}) = \lVert \mathbf{W_d} (\mathbf{G} \mathbf{m} - \mathbf{d}) \rVert_2^2 + \lambda^2 \lVert \mathbf{W_m} \mathbf{L} \mathbf{m} \rVert_2^2
$$

This formulation can be rigorously derived from a Bayesian perspective as a **Maximum a Posteriori (MAP)** estimate. The [likelihood function](@entry_id:141927) $p(\mathbf{d}|\mathbf{m})$, assuming Gaussian noise, gives rise to the [data misfit](@entry_id:748209) term $\Phi_d$. The [prior probability](@entry_id:275634) distribution $p(\mathbf{m})$, which encodes our beliefs about the model's structure (e.g., that it is smooth), gives rise to the model objective term $\Phi_m$. Minimizing the negative logarithm of the [posterior probability](@entry_id:153467) $p(\mathbf{m}|\mathbf{d})$ leads directly to the Tikhonov objective function [@problem_id:3601438].

Let's dissect the components of this [objective function](@entry_id:267263):

*   **Data Misfit Term $\Phi_d$**: The term $\lVert \mathbf{G} \mathbf{m} - \mathbf{d} \rVert_2^2$ measures the squared difference between the observed data and the data predicted by a given model $\mathbf{m}$. The **[data weighting](@entry_id:635715) matrix**, $\mathbf{W_d}$, is used to account for data uncertainties. If the data errors are Gaussian with a covariance matrix $\mathbf{C_d}$, the optimal choice is a matrix such that $\mathbf{W_d}^T \mathbf{W_d} = \mathbf{C_d}^{-1}$. For uncorrelated errors with standard deviations $\sigma_i$, $\mathbf{W_d}$ is a diagonal matrix with entries $1/\sigma_i$. This process, known as "whitening," ensures that all data points contribute appropriately to the objective function based on their reliability.

*   **Model Objective Term $\Phi_m$**: This term penalizes models that are considered geologically implausible. Its structure is defined by the **smoothing operator** $\mathbf{L}$ and the **model weighting matrix** $\mathbf{W_m}$.
    *   If $\mathbf{L}=\mathbf{I}$ (the identity matrix), we are performing zero-order Tikhonov regularization, which seeks a solution with the smallest overall magnitude (smallest norm).
    *   More commonly, $\mathbf{L}$ is a finite-difference operator that approximates the spatial gradient of the model. In this case, the term $\lVert \mathbf{L} \mathbf{m} \rVert_2^2$ penalizes roughness, promoting a spatially smooth solution.

*   **Trade-off Parameter $\lambda$**: This crucial parameter controls the balance between the two terms. A small $\lambda$ prioritizes fitting the data, risking an unstable, noisy solution. A large $\lambda$ prioritizes the model constraint (e.g., smoothness), potentially at the expense of adequately fitting the data. A common strategy for selecting an optimal $\lambda$ is the **[discrepancy principle](@entry_id:748492)**, which chooses $\lambda$ such that the weighted [data misfit](@entry_id:748209) achieves its expected statistical value (e.g., for whitened residuals, $\Phi_d(\mathbf{m}_\lambda) \approx N_d$, the number of data points) [@problem_id:3601438].

#### A Deeper Look at Depth Weighting

A critical component of the model weighting matrix $\mathbf{W_m}$ in potential field inversion is **depth weighting**. As established, the sensitivity of gravity and magnetic data decays rapidly with the depth of the source. For gravity, the kernel decays asymptotically as $z^{-2}$, while for magnetics it is typically $z^{-3}$ [@problem_id:3601394]. Without any correction, a regularized inversion will always find it "easier" to explain the data with shallow sources rather than deeper ones, creating a strong bias and concentrating the recovered model near the surface.

To counteract this, we introduce a depth weighting function $w(z)$ into the model objective term. The goal is to choose $w(z)$ such that the inversion is equally sensitive to sources at all depths. This can be achieved by ensuring that the diagonal elements of the data-term contribution to the [normal equations](@entry_id:142238), $(\mathbf{G}^T\mathbf{G})_{jj}$, and the model-term contribution, $\lambda(\mathbf{W}^T\mathbf{W})_{jj}$, have the same asymptotic decay with depth [@problem_id:3601368].

For 3D [gravity inversion](@entry_id:750042) over a finite survey area, the diagonal elements of $\mathbf{G}^T\mathbf{G}$ can be shown to decay as $(G^T G)_{jj} \propto z_j^{-4}$. The diagonal of the model term is $(\mathbf{W}^T\mathbf{W})_{jj} \propto w(z_j)^2$. To balance these, we require $w(z_j)^2 \propto z_j^{-4}$, which implies $w(z_j) \propto z_j^{-2}$. A practical form of this weighting function is:

$$
w(z) = (z+z_0)^{-2}
$$

The small positive offset $z_0$ is crucial to prevent the weighting function from becoming infinite at the surface ($z=0$), which would artificially suppress any near-surface structure. It regularizes the weighting function itself and is typically chosen to be on the order of the [cell size](@entry_id:139079) near the surface [@problem_id:3601368]. By incorporating such a depth weighting function, we effectively neutralize the geometric decay of the kernel, allowing the inversion to recover structures at depth in a more balanced manner [@problem_id:3601394].

### Assessing the Solution: Resolution and Recoverability

After obtaining a regularized solution $\widehat{\mathbf{m}}$, we must ask: how does this estimated model relate to the true, unknown model $\mathbf{m}_{\text{true}}$? The **[model resolution matrix](@entry_id:752083)**, $\mathbf{R}$, provides the answer.

For a linear inverse problem solved with Tikhonov regularization, the estimated model can be written as a [linear transformation](@entry_id:143080) of the true model [@problem_id:3601362]:

$$
\widehat{\mathbf{m}} = (\mathbf{G}^T\mathbf{G} + \lambda^2 \mathbf{W}_m^T\mathbf{W}_m)^{-1}\mathbf{G}^T\mathbf{d} = (\mathbf{G}^T\mathbf{G} + \lambda^2 \mathbf{W}_m^T\mathbf{W}_m)^{-1}\mathbf{G}^T\mathbf{G} \mathbf{m}_{\text{true}}
$$

The matrix that maps the true model to the estimated model is the [resolution matrix](@entry_id:754282):

$$
\mathbf{R} = (\mathbf{G}^T\mathbf{G} + \lambda^2 \mathbf{W}_m^T\mathbf{W}_m)^{-1}\mathbf{G}^T\mathbf{G}
$$

The relationship $\widehat{\mathbf{m}} = \mathbf{R} \mathbf{m}_{\text{true}}$ reveals that our solution is a smoothed or filtered version of the true model. In an ideal case with perfect resolution, $\mathbf{R}$ would be the identity matrix, meaning $\widehat{\mathbf{m}} = \mathbf{m}_{\text{true}}$. However, due to [ill-posedness](@entry_id:635673) and regularization, this is never achievable.

Each row of the [resolution matrix](@entry_id:754282), say the $i$-th row, acts as an **[averaging kernel](@entry_id:746606)** or **[point-spread function](@entry_id:183154)**. The $i$-th recovered parameter, $\widehat{m}_i$, is a weighted average of all the true model parameters: $\widehat{m}_i = \sum_j R_{ij} m_{\text{true},j}$. If the $i$-th row of $\mathbf{R}$ is a sharp spike at index $j=i$ and zero elsewhere, the resolution for the $i$-th parameter is high. If the row is broad and spread out, it indicates that the recovered parameter $\widehat{m}_i$ is an average of a large region of the true model, and the resolution is low.

The structure of $\mathbf{R}$ is determined by both the physics of the problem (via $\mathbf{G}$) and the choice of regularization (via $\lambda$ and $\mathbf{W}_m$). As the [regularization parameter](@entry_id:162917) $\lambda$ increases, the point-spread functions become broader and their peak amplitudes decrease, signifying a loss of resolution. Furthermore, due to the natural decay of the potential field kernels, model parameters corresponding to deeper cells will inherently have broader, lower-amplitude point-spread functions than shallower cells. The [resolution matrix](@entry_id:754282) thus provides a powerful quantitative tool to understand where in the model we have good recoverability and where our solution is poorly constrained [@problem_id:3601362] [@problem_id:3601394].