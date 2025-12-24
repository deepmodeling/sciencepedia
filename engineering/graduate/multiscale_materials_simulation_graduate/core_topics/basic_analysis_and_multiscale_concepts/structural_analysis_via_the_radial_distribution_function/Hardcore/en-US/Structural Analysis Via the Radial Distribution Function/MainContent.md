## Introduction
Understanding the structure of materials at the atomic level is fundamental to predicting their properties. While the average density provides a starting point, it fails to capture the intricate spatial arrangements of particles that define a substance as a solid, liquid, or gas. To bridge this gap, we turn to a more powerful statistical tool: the **Radial Distribution Function (RDF)**, commonly denoted as $g(r)$. The RDF moves beyond simple density to describe the probability of finding a particle at a given distance from another, offering a detailed fingerprint of a material's local and long-range order.

This article provides a graduate-level exploration of the RDF, designed to equip you with the theoretical knowledge and practical skills to use it effectively in [structural analysis](@entry_id:153861). In the first chapter, **Principles and Mechanisms**, we will establish the formal definition of the RDF, explore its connection to thermodynamic properties like the Potential of Mean Force, and delve into the practicalities of its computation in simulations, including algorithm design and [error analysis](@entry_id:142477). Next, in **Applications and Interdisciplinary Connections**, we will see how the RDF is used to decode the complex structures of liquids and glasses, validate [interatomic potentials](@entry_id:177673), and serve as a bridge between static structure and material dynamics. Finally, the **Hands-On Practices** chapter will challenge you to apply these concepts through targeted exercises, solidifying your ability to translate theoretical understanding into practical computational skill.

## Principles and Mechanisms

### Formal Definition and Physical Interpretation of the Radial Distribution Function

To characterize the structure of a many-particle system, we move beyond the average density and consider the spatial correlations between particles. While the one-particle density, $n^{(1)}(\mathbf{r})$, describes the average number of particles per unit volume at a position $\mathbf{r}$, it provides limited information. For a macroscopically [homogeneous system](@entry_id:150411) of $N$ particles in a volume $V$, this density is simply a constant, $n^{(1)}(\mathbf{r}) = \rho = N/V$.

A more detailed picture emerges from the **two-particle density**, $n^{(2)}(\mathbf{r}_1, \mathbf{r}_2)$, which is defined as the [ensemble average](@entry_id:154225) of finding a pair of distinct particles simultaneously at positions $\mathbf{r}_1$ and $\mathbf{r}_2$. Formally, this is written as:
$$
n^{(2)}(\mathbf{r}_1, \mathbf{r}_2) = \left\langle \sum_{i \neq j} \delta(\mathbf{r}_1 - \mathbf{r}_i) \delta(\mathbf{r}_2 - \mathbf{r}_j) \right\rangle
$$
where the sum is over all distinct pairs of particles $(i, j)$, and the angle brackets denote an average over an equilibrium ensemble of microstates.

In a system devoid of correlations—such as an ideal gas—the positions of any two particles are statistically independent. In this case, the two-particle density would simply factorize into the product of the one-particle densities: $n^{(2)}(\mathbf{r}_1, \mathbf{r}_2) \approx n^{(1)}(\mathbf{r}_1)n^{(1)}(\mathbf{r}_2) = \rho^2$. The **radial distribution function (RDF)**, denoted $g(r)$, is a dimensionless function that quantifies the deviation of the actual system from this uncorrelated ideal. For a homogeneous and isotropic system, where correlations depend only on the scalar separation $r = |\mathbf{r}_2 - \mathbf{r}_1|$, the RDF is formally defined by the relation :
$$
n^{(2)}(\mathbf{r}_1, \mathbf{r}_2) = \rho^2 g(|\mathbf{r}_1 - \mathbf{r}_2|)
$$

This definition provides a direct physical interpretation. The [conditional probability density](@entry_id:265457) of finding a particle at $\mathbf{r}_2$, given that a particle is located at $\mathbf{r}_1$, is $P(\mathbf{r}_2|\mathbf{r}_1) = n^{(2)}(\mathbf{r}_1, \mathbf{r}_2) / n^{(1)}(\mathbf{r}_1)$. For our [homogeneous system](@entry_id:150411), this simplifies to $P(\mathbf{r}_2|\mathbf{r}_1) = (\rho^2 g(r)) / \rho = \rho g(r)$. Thus, **$\rho g(r)$ represents the average local number density of particles at a distance $r$ from an arbitrarily chosen central particle.**

From this interpretation, we can find the average number of particles, $dN$, within a thin spherical shell of radius $r$ and thickness $dr$ around a central particle. This is the product of the local density at that radius and the volume of the shell, $dV = 4\pi r^2 dr$:
$$
dN = (\rho g(r)) \times (4\pi r^2 dr) = 4\pi \rho r^2 g(r) dr
$$
This expression is fundamental to nearly all applications of the RDF.

A key property of $g(r)$ in fluids and [amorphous solids](@entry_id:146055) is its [asymptotic behavior](@entry_id:160836). In systems with [short-range interactions](@entry_id:145678) and no long-range order, the influence of a particle at one position on a particle far away becomes negligible. This is known as the **cluster decomposition principle**. At large separations, the particle positions become uncorrelated, and the two-particle density factorizes, $n^{(2)}(r) \to \rho^2$. Substituting this into the definition of $g(r)$ implies that correlations vanish and :
$$
\lim_{r\to\infty} g(r) = 1
$$
This means that at large distances, the local density around a particle converges to the average bulk density, as one would intuitively expect.

### The Pair Correlation Function and its Relation to Structure

While $g(r)$ measures the local structure relative to an ideal gas baseline, it is often convenient to work with a function that directly isolates the correlated part of the structure. This is the **total correlation function**, more commonly known as the **[pair correlation function](@entry_id:145140)**, defined as :
$$
h(r) = g(r) - 1
$$

By substituting the interpretation $g(r) = \rho(r)/\rho$, where $\rho(r)$ is the local density, we find that $h(r) = (\rho(r) - \rho) / \rho$. This shows that $h(r)$ is the fractional deviation of the local density from the average bulk density.

The properties of $h(r)$ directly mirror those of $g(r)$:
-   Where $h(r) > 0$, there is an excess of particles compared to a random distribution (positive correlation). This is typical for the first few shells of neighbors in a liquid.
-   Where $h(r)  0$, there is a deficit of particles ([negative correlation](@entry_id:637494)). For particles with a repulsive core, $g(r) \to 0$ as $r \to 0$, so $h(r) \to -1$ in this limit.
-   As correlations vanish at large distances, $\lim_{r\to\infty} h(r) = 0$. The function $h(r)$ thus directly represents the "correlation" that decays with distance.

The typical RDF for a simple liquid exhibits a characteristic shape reflecting its disordered but structured nature. At very small $r$, repulsive interatomic forces dominate, leading to an [excluded volume](@entry_id:142090) where $g(r) \approx 0$. This is followed by a sharp first peak, corresponding to the first "shell" of nearest neighbors, held in a transient **cage** by the central particle. Beyond this first peak, $g(r)$ shows a series of oscillations of decreasing amplitude that eventually decay to unity, reflecting the progressively weaker ordering of the second, third, and subsequent neighbor shells.

### Extracting Physical Information from $g(r)$

The radial distribution function is not merely a qualitative descriptor; it is a gateway to quantitative information about a material's structure, phase, and even its dynamic tendencies.

#### Coordination Number

One of the most direct quantities that can be extracted from $g(r)$ is the **coordination number**, $N_c(R)$, defined as the average number of particles contained within a sphere of radius $R$ around a central particle. It is calculated by integrating the number of particles in each spherical shell, $dN$, from the center out to radius $R$:
$$
N_c(R) = \int_0^R 4\pi \rho r^2 g(r) dr
$$
In practice, one is often interested in the number of nearest neighbors. While there is no unique definition for this in a disordered liquid, a standard convention is to define the first coordination shell as extending to the first minimum of the RDF, denoted $r_m$. The [coordination number](@entry_id:143221) of the first shell is then $N_c(r_m)$.

To illustrate, consider a numerical calculation based on binned RDF data from a simulation . Suppose a simulation of a liquid with density $\rho = 32\,\mathrm{nm}^{-3}$ yields a set of $g(r_i)$ values at bin midpoints $r_i$ with a bin width of $\Delta r$. The [coordination number](@entry_id:143221) up to the first minimum, $r_m = 0.33\,\mathrm{nm}$, can be computed by approximating the integral with a Riemann sum (e.g., the [midpoint rule](@entry_id:177487)):
$$
N_c(r_m) = 4\pi\rho \int_0^{r_m} r^2 g(r) dr \approx 4\pi\rho \sum_{i} r_i^2 g(r_i) \Delta r
$$
Using the data provided in the problem—for instance, $g(0.225\,\mathrm{nm}) = 2.60$ at the peak and $g(0.325\,\mathrm{nm}) = 1.10$ near the minimum—and summing over all bins up to $r_m$, one can obtain a quantitative measure of local packing, such as a [coordination number](@entry_id:143221) of approximately 9.4. This demonstrates how a directly measurable structural feature, $g(r)$, is processed to yield a chemically intuitive quantity.

#### Distinguishing Phases of Matter

The form of $g(r)$ serves as a powerful fingerprint for the phase of matter.
-   **Ideal Gas**: No correlations exist, so the local density is the bulk density everywhere. Thus, $g(r) = 1$ for all $r$.
-   **Liquid**: Exhibits [short-range order](@entry_id:158915), characterized by broad, damped peaks, but lacks long-range order, as shown by $g(r) \to 1$.
-   **Crystalline Solid**: Possesses long-range periodic order. In the ideal, zero-temperature limit, particles occupy fixed lattice sites. The $g(r)$ for a perfect crystal consists of a series of discrete, infinitely sharp delta functions at radii corresponding to the coordination shells of the Bravais lattice. The weight of each delta function is proportional to the [coordination number](@entry_id:143221) of that shell.

This allows $g(r)$ to be used for [crystal structure identification](@entry_id:161918) . For example, consider the Face-Centered Cubic (FCC) and Body-Centered Cubic (BCC) structures. While the absolute peak positions depend on the lattice parameter, $a$, the *ratios* of these positions are universal geometric constants.
-   For an **FCC** lattice, the nearest neighbors are at a distance of $r_1 = a/\sqrt{2}$, and the next-nearest neighbors are at $r_2 = a$. The ratio is $(r_2/r_1)_{\mathrm{FCC}} = \sqrt{2} \approx 1.414$.
-   For a **BCC** lattice, the nearest neighbors are at $r_1 = a\sqrt{3}/2$, and the next-nearest neighbors are at $r_2 = a$. The ratio is $(r_2/r_1)_{\mathrm{BCC}} = 2/\sqrt{3} \approx 1.155$.

The distinct sequence of peak position ratios, combined with the different sequence of coordination numbers (e.g., first shell: 12 for FCC, 8 for BCC), provides an unambiguous way to distinguish between these crystal structures from the RDF alone.

#### Connection to Thermodynamics and Dynamics

The structural information in $g(r)$ is deeply connected to the system's thermodynamics and dynamics. A key concept bridging these domains is the **Potential of Mean Force (PMF)**, defined as:
$$
W(r) = -k_B T \ln g(r)
$$
where $k_B$ is the Boltzmann constant and $T$ is the temperature. The PMF can be interpreted as the effective interaction potential between two particles held at a fixed separation $r$, averaged over all possible configurations of the surrounding particles. The peaks in $g(r)$ correspond to minima in $W(r)$, representing stable arrangements, while minima in $g(r)$ correspond to maxima in $W(r)$, representing energetic barriers.

This framework allows us to connect the static structure to dynamic processes. For example, the stability of the nearest-neighbor cage in a liquid can be related to its [structural relaxation](@entry_id:263707) time, $\tau$, which characterizes how long a particle remains trapped by its neighbors . In a simple model, the escape from this cage is treated as an activated process. The energy barrier for this process, $\Delta W$, is the difference in the PMF between the first minimum (the top of the barrier) and the first peak (the bottom of the well): $\Delta W = W(r_{min,1}) - W(r_{peak,1})$. The relaxation time can then be described by an Arrhenius-like relation:
$$
\tau = \tau_0 \exp\left(\frac{\Delta W}{k_B T}\right) = \tau_0 \exp\left(\ln\left[\frac{g(r_{peak,1})}{g(r_{min,1})}\right]\right) = \tau_0 \frac{g(r_{peak,1})}{g(r_{min,1})}
$$
This powerful result shows that the ratio of the first peak height to the first minimum depth in $g(r)$ directly relates to the liquid's [structural stability](@entry_id:147935). A liquid with a higher peak and a deeper minimum (a larger ratio) will have a much longer relaxation time and behave in a more "glass-like" manner.

### Practical Computation and Analysis of $g(r)$

#### Generalization to Different Dimensions

The definition of the RDF is general, but the formula for extracting it from pair counts depends on the dimensionality of the system. The key is the volume element of a "spherical shell" in $d$-dimensional space. The surface area of a $(d-1)$-dimensional sphere of radius $r$ is $S_{d-1}(r) = \frac{2\pi^{d/2}}{\Gamma(d/2)}r^{d-1}$. The number of neighbors in a shell of thickness $dr$ is then $dN^{(d)} = \rho g(r) S_{d-1}(r) dr$.

Let's consider specific cases :
-   **3D**: $S_2(r) = 4\pi r^2$, giving the familiar $dN^{(3D)} = \rho g(r) 4\pi r^2 dr$.
-   **2D**: The "shell" is an [annulus](@entry_id:163678). Its area is the circumference of a circle times the thickness, $S_1(r)dr = 2\pi r dr$. Thus, $dN^{(2D)} = \rho g(r) 2\pi r dr$.
-   **1D**: The system is a line. The "shell" at a distance $r$ from the origin consists of two points, $-r$ and $+r$. The total "volume" (length) of the region $[r, r+dr] \cup [-r-dr, -r]$ is $2dr$. Thus, $S_0(r) = 2$, and $dN^{(1D)} = \rho g(r) 2 dr$.

This dimensional dependence also affects the scaling of the coordination number. For a uniform distribution ($g(r)=1$), the coordination number $N_c(R)$ scales with the volume of a $d$-ball, i.e., $N_c^{(d)}(R) \propto R^d$. This highlights that the $r$-dependent geometric factors are crucial and not just arbitrary normalization constants.

#### Algorithmic Implementation in Simulations

In molecular simulations, $g(r)$ is typically computed by histogramming the distances between all pairs of particles. A naive approach would be to calculate the distance for all $\binom{N}{2}$ pairs, an $O(N^2)$ operation that is computationally prohibitive for large systems.

A more efficient strategy is the **cell-list** (or neighbor-list) method . The simulation box is divided into a grid of cells with an edge length at least as large as the maximum radius of interest for the RDF, $r_c$. To find neighbors of a particle, one only needs to check for particles in its own cell and adjacent cells. This reduces the number of candidate pairs dramatically, leading to an algorithm with a computational cost that scales nearly linearly with the number of particles, $N$.

The expected computational work, $W$, can be estimated. There is an initial setup cost to assign particles to cells, which is linear in $N$. The main cost comes from calculating distances for pairs within the [cutoff radius](@entry_id:136708). For a system with uniform density, the expected number of pairs within $r_c$ of each other is proportional to $N \rho r_c^3$. Combining these gives a total expected work of:
$$
W \approx C_1 N + C_2 N \rho r_c^3
$$
where $C_1$ and $C_2$ are constants. For a cubic box of side $L$, this can be written more precisely as $W = N + \frac{2\pi N(N-1) r_c^3}{3L^3}$. This analysis shows that the cost is primarily determined by the number of particles and the physical density of pairs within the cutoff sphere, not the total number of pairs in the system.

#### Common Artifacts and Corrections

When computing $g(r)$ in a simulation with **Periodic Boundary Conditions (PBC)**, one must use the **Minimum Image Convention (MIC)** to ensure that the distance between any two particles is the shortest possible distance, considering all periodic images. This is equivalent to centering the reference particle in a Wigner-Seitz cell of the periodic lattice (for a cubic box, this is a cube of side $L$) and only considering neighbor particles within this cell.

This procedure introduces a geometric artifact . For any radius $r \le L/2$, the entire spherical shell is contained within the MIC cube, and the calculation is unbiased. However, for $r > L/2$, the sphere of radius $r$ extends beyond the faces of the MIC cube. The MIC algorithm will fail to count pairs in the truncated parts of the shell, leading to a systematic underestimation of $g(r)$. This is why RDFs are typically only reported for $r \le L/2$.

It is possible to derive an exact geometric bias factor, $B(r)$, such that the measured RDF, $\hat{g}(r)$, is related to the true RDF by $\hat{g}(r) = B(r) g(r)$. For a cubic box in the range $L/2 \le r \le L/\sqrt{2}$, the sphere intersects the six faces of the cube but not its edges or corners. The volume of the sampled region is the total volume of the spherical shell minus the volume of the six truncated spherical caps. The area of one such cap, cut by a plane at distance $L/2$ from the center, is $2\pi r h$, where the cap height is $h = r - L/2$. The total area of the six caps is $6 \times 2\pi r (r - L/2)$. The fraction of the total spherical area $4\pi r^2$ that is correctly sampled is:
$$
B(r) = \frac{4\pi r^2 - 6 \times 2\pi r(r - L/2)}{4\pi r^2} = \frac{6\pi r L - 8\pi r^2}{4\pi r^2} = \frac{3L}{2r} - 2
$$
While this correction can be applied, it is often simpler and safer to restrict analysis to $r \le L/2$.

#### Error Analysis and Optimization

The estimation of $g(r)$ via histogramming involves a classic **bias-variance tradeoff** . The choice of bin width, $\Delta r$, is critical.
-   **Bias**: Using a finite bin width means we are approximating the value of $g(r)$ over an interval. This introduces a [systematic error](@entry_id:142393), or bias, which is related to the curvature of $g(r)$. A larger $\Delta r$ leads to a larger averaging volume and potentially greater bias.
-   **Variance**: The number of pairs in each bin is subject to statistical fluctuations. A smaller $\Delta r$ results in a smaller bin volume, fewer counts per bin, and thus a higher relative [statistical error](@entry_id:140054), or variance.

The total error is often quantified by the **Mean Squared Error (MSE)**, defined as $\mathrm{MSE} = (\mathrm{Bias})^2 + \mathrm{Variance}$. For an optimal measurement, one seeks the bin width $\Delta r_\star$ that minimizes the MSE.

A formal derivation under the assumption that the particle count in a bin follows Poisson statistics shows that the squared bias scales as $(\Delta r)^4$, while the variance scales as $(\Delta r)^{-1}$ . The MSE can be written as:
$$
\mathrm{MSE}(r, \Delta r) \approx A (\Delta r)^4 + \frac{B}{\Delta r}
$$
where $A$ depends on the second derivative of the function $r^2 g(r)$ and $B$ depends on $g(r)$, the number of samples $S$, and the density $\rho$. Minimizing this expression with respect to $\Delta r$ yields the optimal bin width:
$$
\Delta r_{\star}(r) = \left( \frac{36 g(r)}{\pi S \rho r^2 \left(g''(r) + \frac{4g'(r)}{r}\right)^2} \right)^{1/5}
$$
This result formalizes the tradeoff: where $g(r)$ is rapidly changing (large derivatives), a smaller bin width is required to minimize bias, whereas in flatter regions, a larger bin width can be used to improve statistics without sacrificing accuracy.

### Advanced Topic: Anisotropic Systems

The standard RDF, $g(r)$, assumes [isotropy](@entry_id:159159). However, many systems, such as [liquid crystals](@entry_id:147648), polymers under shear, or materials under strain, are **anisotropic**. In these cases, the [pair correlation function](@entry_id:145140) depends not just on the separation distance $r$, but also on the direction of the [separation vector](@entry_id:268468), $\mathbf{\hat{r}}$. We must then work with a directional [pair correlation function](@entry_id:145140), $g(\mathbf{r})$.

A practical way to probe anisotropy is to compute a **directional RDF**, $g(r, \hat{\mathbf{n}})$, by restricting the pair-counting histogram to separation vectors that lie within a certain [solid angle](@entry_id:154756) around a specific direction $\hat{\mathbf{n}}$ . If the system is isotropic, $g(r, \hat{\mathbf{n}})$ will be independent of $\hat{\mathbf{n}}$ within statistical noise. If it is anisotropic, $g(r, \hat{\mathbf{n}})$ will show [systematic variation](@entry_id:1132810) with $\hat{\mathbf{n}}$.

The critical challenge is to determine if observed variations are statistically significant or just noise. This requires a formal [hypothesis test](@entry_id:635299). Simple methods, such as performing multiple t-tests between different directions, are statistically invalid because they ignore the complex correlations in simulation data and the problem of [multiple comparisons](@entry_id:173510), leading to a high rate of false positives.

Two robust, [non-parametric methods](@entry_id:138925) are particularly well-suited for this task:

1.  **Permutation Tests**: Define a global [test statistic](@entry_id:167372) that measures the total deviation of the directional RDFs from their mean, e.g., $T = \sum_{k,j} w_j (\hat{g}(r_j, \hat{\mathbf{n}}_k) - \hat{g}_0(r_j))^2$. Under the [null hypothesis](@entry_id:265441) of isotropy, the directional labels are interchangeable. One can generate a null distribution for $T$ by randomly permuting the directional labels of the pair vectors *within each simulation frame*. This shuffling preserves the underlying correlation structure of the data. The [p-value](@entry_id:136498) is the fraction of [permutations](@entry_id:147130) that yield a statistic $T_{\text{perm}} \ge T_{\text{obs}}$. This is an [exact test](@entry_id:178040) that makes minimal assumptions about the data.

2.  **Spherical Harmonic Decomposition and Bootstrapping**: A more formal approach is to expand the full [pair correlation function](@entry_id:145140) in a basis of spherical harmonics, $Y_{lm}(\Omega)$: $g(r, \Omega) = \sum_{l=0}^\infty \sum_{m=-l}^{l} g_{lm}(r) Y_{lm}(\Omega)$. Isotropy implies that all coefficients with angular momentum index $l \ge 1$ must be zero; all structural information is in the $g_{00}(r)$ term. Anisotropy is therefore encoded in the non-zero values of the $g_{lm}(r)$ coefficients for $l \ge 1$. One can define a [test statistic](@entry_id:167372) as the total "energy" in these anisotropic modes. To assess its significance, a **[block bootstrap](@entry_id:136334)** procedure can be used. By resampling entire blocks of consecutive simulation frames, this method preserves the temporal correlations in the data, allowing for the construction of a valid [confidence interval](@entry_id:138194) or p-value for the anisotropy metric.

These advanced statistical techniques are essential for moving beyond qualitative observation to making rigorous, quantitative claims about the presence and magnitude of anisotropy from simulation data.