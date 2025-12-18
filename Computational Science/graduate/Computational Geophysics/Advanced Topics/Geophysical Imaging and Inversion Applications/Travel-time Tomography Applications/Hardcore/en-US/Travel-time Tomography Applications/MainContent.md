## Introduction
Travel-time [tomography](@entry_id:756051) is a powerful geophysical method used to create images of the Earth's interior, from the near-surface to the deep mantle, by analyzing the travel times of seismic waves. Its applications are vast, spanning resource exploration, earthquake hazard assessment, and fundamental planetary science. However, moving from raw travel-time data to a reliable subsurface image is a complex process fraught with theoretical and practical challenges. This article addresses the knowledge gap between basic principles and advanced, real-world application, providing a comprehensive guide for students and practitioners. It systematically demystifies the entire tomographic workflow, from the physics of wave propagation to the art of interpreting a final tomogram.

The journey begins in the "Principles and Mechanisms" chapter, where we will establish the theoretical foundation of [tomography](@entry_id:756051). You will learn how travel times are modeled using the Eikonal equation, how the inverse problem is formulated and stabilized, and how to quantify the reliability of a tomographic image. Next, the "Applications and Interdisciplinary Connections" chapter will bridge theory and practice, exploring how these principles are adapted to tackle complex geological settings, incorporate multiple data types, and even probe the interiors of other planets. Finally, the "Hands-On Practices" section offers concrete exercises to solidify your understanding, guiding you through the implementation of key algorithms in the tomographic toolkit. By the end, you will have a robust framework for applying and critically evaluating [travel-time tomography](@entry_id:756150) in a variety of scientific contexts.

## Principles and Mechanisms

Travel-time tomography operates on a set of core principles that connect the physical propagation of waves through a medium to the mathematical framework used to invert for that medium's properties. This chapter elucidates these principles, beginning with the physics of the forward problem—how travel times are generated—and progressing to the mechanisms of the inverse problem—how an image of the subsurface is reconstructed from those travel times. We will explore the theoretical foundations, the practical choices in numerical implementation, and the methods for assessing the quality of the resulting tomographic models.

### The Forward Problem: Modeling Seismic Travel Times

The forward problem in [travel-time tomography](@entry_id:756150) consists of predicting the travel time of a seismic wave between a known source and receiver, given a model of the medium's properties. The fundamental property governing [wave propagation](@entry_id:144063) speed is the **slowness** field, $s(\mathbf{x})$, defined as the reciprocal of the [velocity field](@entry_id:271461), $s(\mathbf{x}) = 1/v(\mathbf{x})$.

#### The Eikonal Equation: From Waves to Rays

The theoretical underpinning of [travel-time tomography](@entry_id:756150) is the **[eikonal equation](@entry_id:143913)**. It is not a fundamental law of physics in itself, but rather a powerful and accurate approximation derived from the full acoustic or [elastic wave equation](@entry_id:748864) in a specific physical regime. The full wave equation describes complex phenomena including amplitude variations, diffraction, and interference. However, [travel-time tomography](@entry_id:756150) is concerned primarily with the phase of the wave, specifically the arrival time of the wavefront.

In the **high-frequency asymptotic limit**, where the wavelength of the seismic wave is much smaller than the characteristic length scale over which the medium's properties vary, the wavefield can be effectively described by [geometric optics](@entry_id:175028). Under this approximation, the complex wavefield $U(\mathbf{x})$ at a given [angular frequency](@entry_id:274516) $\omega$ can be represented using the Wentzel-Kramers-Brillouin (WKB) [ansatz](@entry_id:184384) as a rapidly varying phase component and a slowly varying amplitude component:

$U(\mathbf{x}) = A(\mathbf{x}) \exp(\mathrm{i} \omega T(\mathbf{x}))$

Here, $A(\mathbf{x})$ is the amplitude and $T(\mathbf{x})$ is the phase function, which is physically interpreted as the travel-time field. By substituting this form into the frequency-domain wave equation (the Helmholtz equation) and considering the limit as $\omega \to \infty$, one finds that the leading-order term yields a nonlinear [partial differential equation](@entry_id:141332) governing only the travel-time field $T(\mathbf{x})$. This is the [eikonal equation](@entry_id:143913) :

$|\nabla T(\mathbf{x})| = s(\mathbf{x})$

The [eikonal equation](@entry_id:143913) states that the magnitude of the spatial gradient of the travel-time field at any point is equal to the medium's slowness at that point. Geometrically, this implies that the [gradient vector](@entry_id:141180) $\nabla T$, which is always normal to the wavefronts (surfaces of constant travel time), has a length equal to the local slowness. This [high-frequency approximation](@entry_id:750288) elegantly decouples the travel time from wave amplitude and provides the foundational equation for ray-based tomography.

#### Travel Time in Homogeneous Media: A First Principle Example

To build intuition for the [eikonal equation](@entry_id:143913), consider the simplest possible medium: a homogeneous, isotropic medium where the velocity $v$ is constant everywhere, and thus the slowness $s = 1/v$ is also constant. According to **Fermat's principle**, which states that a wave travels between two points along the path of minimum time, the ray path in a homogeneous medium must be a straight line—the path of shortest distance.

Let a source be located at $\mathbf{x}_{\mathrm{s}}$. The travel time $T$ to any other point $\mathbf{x}$ is simply the Euclidean distance between the points divided by the constant velocity:

$T(\mathbf{x}) = \frac{\|\mathbf{x} - \mathbf{x}_{\mathrm{s}}\|}{v} = s \|\mathbf{x} - \mathbf{x}_{\mathrm{s}}\|$

We can verify that this simple and intuitive result satisfies the [eikonal equation](@entry_id:143913). The gradient of the travel-time field is:

$\nabla T(\mathbf{x}) = \nabla \left( s \sqrt{(x-x_s)^2 + (y-y_s)^2 + (z-z_s)^2} \right) = s \frac{\mathbf{x} - \mathbf{x}_{\mathrm{s}}}{\|\mathbf{x} - \mathbf{x}_{\mathrm{s}}\|}$

The magnitude of this gradient is:

$|\nabla T(\mathbf{x})| = \left\| s \frac{\mathbf{x} - \mathbf{x}_{\mathrm{s}}}{\|\mathbf{x} - \mathbf{x}_{\mathrm{s}}\|} \right\| = s \left\| \frac{\mathbf{x} - \mathbf{x}_{\mathrm{s}}}{\|\mathbf{x} - \mathbf{x}_{\mathrm{s}}\|} \right\| = s \cdot 1 = s$

This confirms that the travel time in a homogeneous medium is a valid solution to the [eikonal equation](@entry_id:143913). For example, in a medium with a [constant velocity](@entry_id:170682) of $v = 5.50 \, \mathrm{km/s}$, the travel time from a source at $(0,0,0) \, \mathrm{km}$ to a receiver at $(12,5,3) \, \mathrm{km}$ is calculated by first finding the distance $d = \sqrt{12^2 + 5^2 + 3^2} = \sqrt{178} \, \mathrm{km}$, and then the travel time $T = d/v = \sqrt{178} / 5.50 \approx 2.426 \, \mathrm{s}$ .

#### Ray Tracing and Fermat's Principle

In a heterogeneous medium where slowness $s(\mathbf{x})$ varies with position, ray paths are no longer straight lines. Fermat's principle still holds: the ray follows the path $\gamma$ that minimizes the travel-time functional:

$T[\gamma] = \int_{\gamma} s(\mathbf{x}) \, \mathrm{d}l$

where $\mathrm{d}l$ is the arc-length element. Rays bend according to Snell's law, curving towards regions of higher slowness (lower velocity) to minimize overall travel time. Finding these paths is the task of **[ray tracing](@entry_id:172511)**.

A powerful and general framework for [ray tracing](@entry_id:172511) is provided by Hamiltonian mechanics. The problem can be cast in terms of a Hamiltonian $H(\mathbf{x}, \mathbf{p}) = v(\mathbf{x}) \|\mathbf{p}\| = \|\mathbf{p}\| / s(\mathbf{x})$, where $\mathbf{x}$ is position and $\mathbf{p} = \nabla T$ is the slowness vector ([canonical momentum](@entry_id:155151)). The ray's trajectory is then governed by Hamilton's canonical equations, a system of [first-order ordinary differential equations](@entry_id:264241) (ODEs). A common approach for finding the specific ray connecting a source $\mathbf{x}_{\mathrm{s}}$ to a receiver $\mathbf{x}_{\mathrm{r}}$ is the **shooting method**, which iteratively adjusts the initial take-off angle of the ray at the source until it "hits" the receiver .

A crucial simplification often made in [tomography](@entry_id:756051) is the **straight-[ray approximation](@entry_id:167996)**, which assumes that rays travel in straight lines between sources and receivers, even in a heterogeneous medium. This approximation is computationally convenient but is only valid when velocity gradients are small. When significant velocity variations exist, such as a linear [velocity gradient](@entry_id:261686) or a localized low-velocity anomaly, true rays will bend. Neglecting this curvature by using a straight-[ray approximation](@entry_id:167996) can lead to significant errors in the computed travel times. For example, in a medium with a vertical speed gradient, rays will curve upwards, and the straight-line travel time will be systematically longer than the true curved-ray (least) time. Similarly, rays will bend to avoid a low-velocity anomaly, again resulting in a shorter travel time than a straight path that passes through it. Quantifying this error, $\Delta T = |T_{\text{straight}} - T_{\text{curved}}|$, is essential for assessing the validity of the straight-ray assumption for a given model .

#### Numerical Methods for Computing Travel-Time Fields

While Hamiltonian [ray tracing](@entry_id:172511) is fundamental, various numerical methods have been developed to solve the [forward problem](@entry_id:749531) efficiently, especially for finding first-arrival times across an entire grid. These methods can be broadly categorized into path-based and field-based approaches .

- **Path-Based Methods**: These methods compute travel times for individual source-receiver pairs.
    - **Shooting methods**, as described above, solve a [two-point boundary value problem](@entry_id:272616) by integrating the ray equations. They are flexible but can be computationally expensive and, critically, are not guaranteed to find the global first-arrival path in the presence of multipathing. They can get "trapped" on a path corresponding to a local minimum in travel time (e.g., a reflection).
    - **Bending methods** start with an initial path (e.g., a straight line) and iteratively deform or "bend" it to minimize the travel time according to Fermat's principle. Like shooting methods, they are local optimizers and may converge to a later-arriving stationary path rather than the global first arrival.

- **Field-Based Methods**: These methods compute the entire travel-time field $T(\mathbf{x})$ from a source throughout a discretized domain.
    - The **Fast Marching Method (FMM)** is a highly efficient grid-based algorithm that solves the [eikonal equation](@entry_id:143913) directly. It propagates the solution outwards from the source, respecting causality by always advancing the wavefront from the "trial" grid point with the smallest travel time. This ordered propagation, typically managed with a min-priority heap, guarantees that FMM computes the first-arrival time at every grid point. It correctly handles complex wavefronts, including caustics, by naturally selecting the [viscosity solution](@entry_id:198358) to the [eikonal equation](@entry_id:143913). For a grid with $N$ nodes, its computational complexity is typically $O(N \log N)$.
    - **Shortest-[path graph](@entry_id:274599) methods** treat the grid as a graph where nodes are grid points and edges connect neighbors. Edge weights are assigned based on the travel time between adjacent nodes. An algorithm like **Dijkstra's algorithm** can then be used to find the shortest path (in travel time) from the source node to all other nodes. This approach is conceptually similar to FMM and also guarantees finding the first arrivals on the discrete graph.

For many tomographic applications, where the first-arrival travel-time field is required, field-based methods like FMM are preferred due to their efficiency and their inherent ability to find the globally shortest time paths, a property not guaranteed by path-based methods like shooting or bending .

### The Inverse Problem: From Travel Times to Earth Structure

The [inverse problem](@entry_id:634767) aims to reconstruct the slowness field $s(\mathbf{x})$ from a set of observed travel times. This is almost always an [ill-posed problem](@entry_id:148238), meaning that a solution may not be unique, stable, or even exist. Therefore, the process involves careful [discretization](@entry_id:145012), [linearization](@entry_id:267670), and regularization.

#### Discretization and Linearization

The continuous slowness field $s(\mathbf{x})$ must first be represented by a finite number of parameters. This is the process of **[model parameterization](@entry_id:752079)**.

##### Model Parameterization: Cells vs. Nodes

A common choice is to divide the domain into a grid of rectangular cells and assume the slowness is constant within each cell. This is a **piecewise-constant cell parameterization**. The sensitivity matrix (or Jacobian) entry $G_{rk}$ for ray $r$ and cell $k$ is simply the length of the ray segment within that cell. Since a ray only intersects a small subset of all cells, the resulting Jacobian matrix is very sparse. However, this parameterization allows for sharp, discontinuous jumps in slowness between adjacent cells. These high-frequency variations can be difficult to constrain with smooth, integrating ray data, often leading to an [ill-conditioned problem](@entry_id:143128) with very small singular values corresponding to "checkerboard" artifacts .

An alternative is **continuous nodal interpolation**. Here, slowness values are defined at the nodes of the grid, and the slowness at any point within an element is interpolated from the values at the element's corners (e.g., using bilinear shape functions). This enforces continuity in the slowness field across element boundaries. The Jacobian entry $G_{rj}$ for ray $r$ and node $j$ is the integral of the shape function for node $j$ along the ray path. Since a ray passing through an element is influenced by all four of that element's nodes, the Jacobian becomes less sparse than in the cell-based case. The key advantage is that the enforced smoothness acts as an implicit regularizer, disallowing the [high-frequency modes](@entry_id:750297) that plague piecewise-constant models. This typically increases the smallest singular values of the Jacobian, resulting in a better-conditioned (though not necessarily well-conditioned) inverse problem .

##### Velocity vs. Slowness Parameterization

Another fundamental choice is whether to parameterize the model in terms of slowness $s$ or velocity $v$. Under the fixed-[ray approximation](@entry_id:167996), the travel time for a ray is a linear sum of the cell slownesses it traverses: $t = \sum L_j s_j$. Thus, a **slowness [parameterization](@entry_id:265163)** yields a linear [forward problem](@entry_id:749531). In contrast, the travel time is a nonlinear function of velocity: $t = \sum L_j / v_j$. A **velocity parameterization** therefore leads to a nonlinear inverse problem .

This choice has significant statistical implications. If we assume a Gaussian prior distribution on our model parameters, assuming a Gaussian prior on slowness is different from assuming one on velocity. A Gaussian prior on velocity $v$ induces a non-Gaussian prior on slowness $s=1/v$, and vice-versa. Because the inverse relationship is nonlinear, the mean of the induced distribution is not simply the reciprocal of the original mean (by Jensen's inequality, $E[1/v] > 1/E[v]$), introducing a potential bias.

In practice, nonlinear problems are often handled by linearizing the forward operator around a [reference model](@entry_id:272821) $\mathbf{v}_0$. The sensitivity matrix for velocity perturbations, $\mathbf{G}_v$, can be shown to be $\mathbf{G}_v = \mathbf{L}\mathbf{J}$, where $\mathbf{L}$ is the path-length matrix and $\mathbf{J}$ is a [diagonal matrix](@entry_id:637782) with entries $J_{jj} = -1/v_{0,j}^2$. This [linearization](@entry_id:267670) makes the problem locally linear-Gaussian, but the effective prior and variance structure now depends on the [reference model](@entry_id:272821) $\mathbf{v}_0$ through the Jacobian $\mathbf{J}$ . The linearity of the slowness [parameterization](@entry_id:265163) often makes it a more direct and convenient choice.

##### The Linearized System

After parameterization and [linearization](@entry_id:267670), the problem is typically expressed in the standard [linear form](@entry_id:751308):

$\mathbf{d} = \mathbf{G}\mathbf{m} + \boldsymbol{\epsilon}$

Here, $\mathbf{d}$ is the data vector of $N$ travel-time residuals (observed minus reference travel times), $\mathbf{m}$ is the model vector of $M$ perturbations to the [reference model](@entry_id:272821) (e.g., slowness perturbations), $\mathbf{G}$ is the $N \times M$ sensitivity matrix, and $\boldsymbol{\epsilon}$ is a vector of measurement errors.

#### Solving the Inverse Problem: Regularized Least Squares

Directly inverting the equation $\mathbf{m} = \mathbf{G}^{-1}\mathbf{d}$ is rarely possible, as $\mathbf{G}$ is usually rectangular, ill-conditioned, or both. Instead, we seek a model $\mathbf{m}$ that "best fits" the data in a least-squares sense, while also satisfying some prior constraints on the model's properties.

##### Weighted Least Squares and Data Covariance

Not all data are created equal. Travel-time measurements (or "picks") have varying uncertainties, due to factors like [signal-to-noise ratio](@entry_id:271196) or emergent arrivals. It is desirable to give more weight to high-quality data and less weight to noisy data. This is achieved through **[weighted least squares](@entry_id:177517)**. If we assume the measurement errors are independent but have different variances $\sigma_i^2$, the errors are described by a diagonal covariance matrix $\mathbf{C}_d = \mathrm{diag}(\sigma_1^2, \dots, \sigma_N^2)$. The appropriate [misfit function](@entry_id:752010) to minimize is the heteroscedastic weighted least-squares misfit, often expressed as the squared Mahalanobis distance :

$\phi(\mathbf{m}) = \frac{1}{2} (\mathbf{d} - \mathbf{G}\mathbf{m})^{\top} \mathbf{C}_d^{-1} (\mathbf{d} - \mathbf{G}\mathbf{m}) = \frac{1}{2} \sum_{i=1}^{N} \frac{(d_i - (\mathbf{G}\mathbf{m})_i)^2}{\sigma_i^2}$

Minimizing this function has two key properties. First, each data residual is weighted by the inverse of its variance, $1/\sigma_i^2$. This means that data points with small uncertainty (small $\sigma_i$) have a large weight and will exert a stronger pull on the solution. Second, under the assumption of Gaussian noise, minimizing this [misfit function](@entry_id:752010) is equivalent to finding the **Maximum Likelihood Estimator (MLE)** for the model $\mathbf{m}$. Furthermore, this weighted problem can be transformed into an equivalent ordinary least-squares problem via **prewhitening**, where the data and sensitivity matrix are transformed as $\mathbf{d}' = \mathbf{C}_d^{-1/2}\mathbf{d}$ and $\mathbf{G}' = \mathbf{C}_d^{-1/2}\mathbf{G}$ . Ignoring this [heteroscedasticity](@entry_id:178415) leads to an unbiased estimate (if the noise is zero-mean) but one with a generally larger variance than the correctly weighted estimate, as guaranteed by the Gauss-Markov theorem.

##### Regularization: Stabilizing the Solution

Even with weighting, the tomographic [inverse problem](@entry_id:634767) is typically ill-conditioned. There may be parts of the model that are poorly sampled by rays, leading to non-uniqueness and large, unphysical oscillations in the solution. **Regularization** is the process of adding a penalty term to the [objective function](@entry_id:267263) to enforce desirable properties on the solution, such as smoothness. The regularized [objective function](@entry_id:267263) is:

$\min_{\mathbf{m}} \left\{ \frac{1}{2} \|\mathbf{d} - \mathbf{G}\mathbf{m}\|_{\mathbf{C}_d^{-1}}^2 + \lambda^2 R(\mathbf{m}) \right\}$

where $R(\mathbf{m})$ is the regularization functional and $\lambda$ is a [regularization parameter](@entry_id:162917) that controls the trade-off between fitting the data and satisfying the prior constraint.

##### Tikhonov vs. Total Variation Regularization

The choice of regularizer $R(\mathbf{m})$ encodes our prior assumption about the Earth's structure .
- **Tikhonov Regularization**: The most common choice is to penalize the squared $\ell_2$ norm of the model's gradient, $R(\mathbf{m}) = \|\nabla \mathbf{m}\|_2^2$. This penalty grows quadratically with the gradient's magnitude, strongly penalizing large changes and thus promoting **smooth solutions**. It is mathematically convenient and effective when the true [geology](@entry_id:142210) is expected to vary smoothly. However, its diffusion-like behavior will blur and smear sharp geological interfaces, such as faults or stratigraphic boundaries, into smooth ramps.

- **Total Variation (TV) Regularization**: An alternative is to penalize the $\ell_1$ norm of the model's gradient, $R(\mathbf{m}) = \|\nabla \mathbf{m}\|_1$. This penalty grows linearly with the gradient's magnitude, making it much more tolerant of large, isolated jumps. The $\ell_1$ norm is known to promote **sparsity**; in this context, it promotes a sparse gradient map, meaning the model is encouraged to be **piecewise-constant** or "blocky". TV regularization is therefore far superior at preserving sharp interfaces, provided the underlying [geology](@entry_id:142210) is indeed blocky in nature. The success of TV regularization relies on this model assumption being appropriate and on the data (ray coverage) being sufficient to resolve the interfaces. From a theoretical standpoint, if the model's gradient is sparse, and the forward operator satisfies certain conditions (akin to the Restricted Isometry Property in [compressed sensing](@entry_id:150278)), TV regularization can provide highly accurate reconstructions of blocky models .

The choice between Tikhonov and TV regularization is thus a choice of prior: do we believe the subsurface is predominantly smooth or blocky?

#### Assessing the Solution: Model Resolution

Once an inverse solution $\widehat{\mathbf{m}}$ is computed, it is crucial to assess its reliability. Since the solution is a blurred and imperfect representation of the true Earth, we must ask: how much can we trust the features we see in the tomogram?

##### The Model Resolution Matrix

In a linear, regularized inversion, the estimated model $\widehat{\mathbf{m}}$ is a linear function of the true data $\mathbf{d}_{\text{true}} = \mathbf{G}\mathbf{m}_{\text{true}}$. The relationship between the estimated model and the true model is described by the **[model resolution matrix](@entry_id:752083)**, $\mathbf{R}$, such that $\widehat{\mathbf{m}} = \mathbf{R} \mathbf{m}_{\text{true}}$. For a Tikhonov-regularized GLS problem, this matrix is given by :

$\mathbf{R} = \left(\mathbf{G}^{\mathsf{T}}\mathbf{C}_d^{-1}\mathbf{G} + \lambda^2 \mathbf{L}^{\mathsf{T}}\mathbf{L}\right)^{-1}\mathbf{G}^{\mathsf{T}}\mathbf{C}_d^{-1}\mathbf{G}$

where $\mathbf{L}$ is the regularization operator (e.g., a [gradient operator](@entry_id:275922)). If resolution were perfect, $\mathbf{R}$ would be the identity matrix, $\mathbf{I}$. In reality, $\mathbf{R}$ is a non-diagonal matrix that quantifies how the inversion process smears the true model.

##### Point-Spread Functions

The interpretation of $\mathbf{R}$ is made clear through the concept of a **[point-spread function](@entry_id:183154) (PSF)**. The $k$-th column of the [resolution matrix](@entry_id:754282), $\mathbf{R}_{:,k}$, is the result of applying the entire tomographic inversion process to a hypothetical "true" model that is zero everywhere except for a single spike (a discrete [delta function](@entry_id:273429)) at the $k$-th model cell. Thus, the $k$-th column of $\mathbf{R}$ shows how a single point anomaly at location $k$ is "imaged" by the tomography. It is the [point-spread function](@entry_id:183154) for that location in the model.

The width of the PSF indicates the degree of smearing and thus quantifies the spatial resolution; a wider PSF means lower resolution. The shape of the PSF is also informative. In regions of anisotropic ray coverage, the PSF is typically elongated, with smearing being most pronounced in directions with poor ray sampling. Examining these PSFs is a critical step in interpreting a tomographic image, helping to distinguish well-resolved geological features from artifacts of the inversion process .

### Advanced Topics and Extensions

The principles outlined above form the basis of isotropic [travel-time tomography](@entry_id:756150). However, the Earth is often more complex. A key extension is accounting for seismic anisotropy.

#### Incorporating Anisotropy

Seismic anisotropy is the directional dependence of wave propagation speed. A common form is **Vertical Transverse Isotropy (VTI)**, characteristic of finely layered sedimentary basins or aligned mineral fabrics in the mantle. In a VTI medium, wave speed depends on the angle of propagation relative to the vertical symmetry axis.

This introduces a fundamental complication: the direction of [energy propagation](@entry_id:202589) (**group velocity**, $\mathbf{v}_{\mathrm{g}}$) is generally different from the direction of [wavefront](@entry_id:197956) propagation (**phase velocity**, $v_{\mathrm{P}}$). A seismic ray follows the path of the group velocity vector. However, the travel time along this path is determined by the local slowness, which is related to the [phase velocity](@entry_id:154045). For weak VTI, parameterized by Thomsen's parameters $\epsilon$ and $\delta$ (where $|\epsilon| \ll 1$ and $|\delta| \ll 1$), the relationship between these quantities can be approximated .

The P-wave phase velocity $v_{\mathrm{P}}(\theta)$ depends on the [phase angle](@entry_id:274491) $\theta$ with respect to the vertical axis, with a standard weak-anisotropy approximation being:

$v_{\mathrm{P}}(\theta) \approx V_{\mathrm{P}0} \left( 1 + \delta \sin^2\theta \cos^2\theta + \epsilon \sin^4\theta \right)$

where $V_{\mathrm{P}0}$ is the vertical P-wave velocity. The group velocity vector $\mathbf{v}_{\mathrm{g}}$ can be derived from this expression. To first order in the anisotropy parameters, the magnitude of the [group velocity](@entry_id:147686) is approximately equal to the phase velocity, $\|\mathbf{v}_{\mathrm{g}}\| \approx v_{\mathrm{P}}(\theta)$. However, the [group velocity](@entry_id:147686) direction, given by the group angle $\psi$, deviates from the phase angle $\theta$. The deviation, $\psi - \theta$, is proportional to the derivative $\mathrm{d}v_{\mathrm{P}}/\mathrm{d}\theta$ and is non-zero for an [anisotropic medium](@entry_id:187796).

This means that to correctly compute travel time in an [anisotropic medium](@entry_id:187796), one must trace a ray in the direction of the group velocity $\psi$, but at each point along the path, calculate the travel time increment $\mathrm{d}T = \mathrm{d}l / \|\mathbf{v}_{\mathrm{g}}\|$ using the velocity corresponding to the underlying phase angle $\theta$. Incorporating this more complex physics is a crucial step in producing accurate tomographic images in many parts of the Earth.