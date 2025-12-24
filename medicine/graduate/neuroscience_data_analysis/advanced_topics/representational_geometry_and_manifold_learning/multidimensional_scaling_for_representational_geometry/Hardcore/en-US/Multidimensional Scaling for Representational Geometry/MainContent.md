## Introduction
In the quest to understand the brain, neuroscientists are often confronted with a deluge of high-dimensional data. How do patterns of neural activity encode information about the world? Answering this question requires methods that can distill complex, high-dimensional neural representations into a form that is both quantitatively rigorous and intuitively understandable. Multidimensional Scaling (MDS) provides a powerful framework for this task, transforming matrices of pairwise neural dissimilarities into low-dimensional maps, or "representational geometries," where spatial relationships reveal the structure of the brain's internal code. This article offers a comprehensive exploration of MDS for uncovering these hidden geometries.

In the first chapter, **Principles and Mechanisms**, we will dissect the core mechanics of MDS, exploring the foundational differences between metric and nonmetric approaches and detailing the elegant mathematics behind classical MDS and the robust optimization of iterative methods. Next, in **Applications and Interdisciplinary Connections**, we will see these principles in action, demonstrating how MDS serves as a cornerstone of Representational Similarity Analysis in neuroscience and how its core concepts extend to diverse fields like [virology](@entry_id:175915) and chemistry. Finally, the **Hands-On Practices** chapter provides an opportunity to solidify your understanding through practical exercises, guiding you from raw data to interpretable geometric visualizations. Through this structured journey, you will gain the expertise to leverage MDS as a versatile tool for data exploration and [hypothesis testing](@entry_id:142556).

## Principles and Mechanisms

Multidimensional Scaling (MDS) encompasses a family of techniques designed to create a [spatial representation](@entry_id:1132051) of items from a matrix of pairwise dissimilarities. In the context of neuroscience, this involves taking a Representational Dissimilarity Matrix (RDM), which quantifies the dissimilarity between neural activity patterns evoked by different stimuli, and translating it into a "map" or "representational geometry." This map consists of a configuration of points in a low-dimensional Euclidean space, where the distances between points reflect the dissimilarities between the corresponding neural patterns. The principles and mechanisms governing this process depend critically on the assumptions made about the nature of the input dissimilarities. We will explore two major families of MDS: metric and nonmetric.

### Metric Multidimensional Scaling: Preserving Distance Scales

Metric MDS operates under the assumption that the input dissimilarities, $\delta_{ij}$, are measured on a ratio or interval scale, meaning they are directly comparable to Euclidean distances. This approach seeks to find a configuration of points whose inter-point distances, $d_{ij}$, are as close as possible to the original dissimilarities.

#### Classical MDS: An Analytic Solution

The foundational metric approach is **[classical multidimensional scaling](@entry_id:1122428)**, also known as Torgerson-Gower scaling. It provides an elegant, non-iterative solution when the input dissimilarities are assumed to be true Euclidean distances. The procedure's ingenuity lies in its ability to convert distances into inner products, from which coordinates can be derived via [eigendecomposition](@entry_id:181333) .

Let us assume we have a set of $n$ points $\{x_1, \dots, x_n\}$ in a Euclidean space, and their configuration is centered at the origin, i.e., $\sum_{i=1}^n x_i = \mathbf{0}$. Let $X$ be the $n \times p$ matrix whose rows are the coordinate vectors $x_i^\top$. The **Gram matrix**, $B = XX^\top$, contains the pairwise inner products of these vectors, $B_{ij} = x_i^\top x_j$. The squared Euclidean distance between points $x_i$ and $x_j$ is given by:

$d_{ij}^2 = \|x_i - x_j\|^2 = (x_i - x_j)^\top(x_i - x_j) = x_i^\top x_i + x_j^\top x_j - 2x_i^\top x_j = B_{ii} + B_{jj} - 2B_{ij}$

Classical MDS solves the inverse problem: given a matrix of squared dissimilarities $D^{(2)}$ with entries $\delta_{ij}^2$, how can we recover the Gram matrix $B$ and, from it, the coordinates $X$? The key is a procedure known as **double centering**. We define a **centering matrix** $J = I - \frac{1}{n}\mathbf{1}\mathbf{1}^\top$, where $I$ is the $n \times n$ identity matrix and $\mathbf{1}$ is an $n \times 1$ column vector of ones. This matrix projects data onto a space orthogonal to the vector $\mathbf{1}$, effectively mean-centering the rows or columns of any matrix it is applied to. It can be shown that the Gram matrix of a centered set of points can be recovered from the squared [distance matrix](@entry_id:165295) via the transformation:

$B = -\frac{1}{2} J D^{(2)} J$

Once the Gram matrix $B$ is obtained, we can recover the coordinates through **[eigendecomposition](@entry_id:181333)**. Since $B$ is a symmetric matrix, it can be decomposed as $B = V \Lambda V^\top$, where $V$ is an [orthogonal matrix](@entry_id:137889) whose columns are the eigenvectors of $B$, and $\Lambda$ is a diagonal matrix of the corresponding eigenvalues $\lambda_i$. If $B$ is a true Gram matrix of points in a $p$-dimensional space, it will be positive semidefinite and have at most $p$ positive eigenvalues. We can then construct a set of coordinates $X$ that generate this Gram matrix. A valid choice is:

$X_p = V_p \Lambda_p^{1/2}$

Here, $\Lambda_p$ is a diagonal matrix containing the $p$ largest positive eigenvalues, and $V_p$ is a matrix containing the corresponding $p$ eigenvectors. The rows of the resulting $n \times p$ matrix $X_p$ provide the coordinates for the $n$ stimuli in a $p$-dimensional space.

#### Interpreting the Classical MDS Solution

The elegance of classical MDS extends to the [interpretability](@entry_id:637759) of its components. The eigenvalues of the Gram matrix $B$ have a direct physical meaning: they represent the variance of the embedded points along each principal axis . The total variance of the centered [point cloud](@entry_id:1129856) is given by the sum of the squared distances of each point from the origin, which is equal to the trace of the Gram matrix:

$\text{Total Variance} = \sum_{i=1}^n \|x_i\|^2 = \sum_{i=1}^n B_{ii} = \text{tr}(B)$

By the properties of the trace, $\text{tr}(B) = \sum_{i=1}^n \lambda_i$. Furthermore, one can show that the variance of the point cloud projected onto the $k$-th principal axis (the axis defined by the $k$-th eigenvector) is precisely equal to the $k$-th eigenvalue, $\lambda_k$.

This leads to a natural measure of **goodness-of-fit** for a low-dimensional embedding. The fraction of total [variance explained](@entry_id:634306) by the first $p$ dimensions is the ratio of the sum of the first $p$ eigenvalues to the sum of all positive eigenvalues:

$\text{Fraction of Variance Explained}(p) = \frac{\sum_{k=1}^p \lambda_k}{\sum_{k, \lambda_k > 0} \lambda_k}$

For example, if the positive eigenvalues of a computed Gram matrix were $\{8.4, 3.6, 2.0, 1.0, 0.5\}$, the total variance is $15.5$. A 3-dimensional embedding would capture a variance of $8.4 + 3.6 + 2.0 = 14.0$, accounting for a fraction $14.0 / 15.5 \approx 0.903$ of the total variance .

An essential property of any MDS solution is its **geometric indeterminacy** . The input to MDS is a set of pairwise distances. These distances are invariant under certain [geometric transformations](@entry_id:150649) of the entire [point cloud](@entry_id:1129856). Specifically, if we take a valid coordinate solution $X$ and apply a **translation** (add a constant vector to all points), a **rotation**, or a **reflection** (multiply the coordinate matrix by an [orthogonal matrix](@entry_id:137889)), the pairwise distances between the points remain unchanged. Consequently, the MDS solution is only unique up to these [rigid motions](@entry_id:170523) (isometries). For metric MDS, there is an additional indeterminacy of **uniform scaling**. Scaling all coordinates by a factor $s$ will scale all distances by $|s|$. While this changes the numerical values in the RDM, it preserves the relative geometry and is often considered a trivial indeterminacy. This rotational and reflectional ambiguity is critical when comparing [embeddings](@entry_id:158103) from different sources (e.g., brain data vs. a computational model); a direct comparison of coordinates is meaningless without first aligning the configurations, for example, using an orthogonal Procrustes analysis.

#### The Challenge of Non-Euclidean Dissimilarities

The classical MDS procedure rests on the assumption that the input dissimilarities are Euclidean. However, in practice, many [dissimilarity measures](@entry_id:634100) used in neuroscience (e.g., $1 - \text{correlation}$) can violate the axioms of a [metric space](@entry_id:145912), particularly the [triangle inequality](@entry_id:143750) ($\delta_{ik} \le \delta_{ij} + \delta_{jk}$). When such **non-Euclidean dissimilarities** are fed into the classical MDS algorithm, the resulting matrix $B = -\frac{1}{2} J D^{(2)} J$ is not guaranteed to be positive semidefinite .

The consequence of this is the appearance of **negative eigenvalues** in the spectrum of $B$. Since a Gram matrix of real-valued coordinates cannot have negative eigenvalues, their presence is a definitive sign that the input dissimilarities cannot be perfectly represented by any configuration of points in any real Euclidean space. An exact embedding is mathematically impossible.

In this common scenario, the standard practice is to proceed by discarding the eigenvectors associated with negative eigenvalues and constructing an approximate embedding using only the positive part of the spectrum. This yields the best possible Euclidean approximation to the non-Euclidean data in a [least-squares](@entry_id:173916) sense, but it inevitably introduces distortion. The magnitude of the negative eigenvalues relative to the positive ones serves as a diagnostic, indicating the severity of the deviation from a Euclidean structure.

#### Iterative Metric MDS: Stress Minimization

An alternative to the analytic classical approach is to frame metric MDS as a [numerical optimization](@entry_id:138060) problem. Here, the goal is to find a configuration $X$ that directly minimizes a **stress function**, which quantifies the mismatch between the embedded distances $d_{ij}(X)$ and the input dissimilarities $\delta_{ij}$. A common form is the weighted raw stress:

$S(X) = \sum_{1 \le i  j \le n} w_{ij} (d_{ij}(X) - \delta_{ij})^2$

where $w_{ij}$ are non-negative weights. Unlike classical MDS, this approach requires an iterative algorithm to find the minimum. Understanding the optimization process can be aided by examining the gradient of the stress function with respect to the coordinates of a single point $x_k$ . The derived gradient is:

$\nabla_{x_k} S(X) = 2 \sum_{j \neq k} w_{kj} \left( 1 - \frac{\delta_{kj}}{d_{kj}(X)} \right) (x_k - x_j)$

This expression is intuitive: the force pulling or pushing point $x_k$ relative to point $x_j$ is proportional to the vector $(x_k - x_j)$. If the current distance $d_{kj}(X)$ is larger than the target dissimilarity $\delta_{kj}$, the term $(1 - \delta_{kj}/d_{kj})$ is positive, creating a force that pulls $x_k$ and $x_j$ together. Conversely, if $d_{kj}(X)$ is too small, the force is repulsive. The [optimization algorithm](@entry_id:142787) iteratively adjusts the positions of all points according to these forces until they settle into a low-stress configuration.

### Nonmetric Multidimensional Scaling: Preserving Rank Order

In many scientific contexts, particularly in neuroscience, the absolute scale of dissimilarities may be unreliable or lack theoretical meaning. For instance, fMRI response patterns might be distorted by nonlinearities in the hemodynamic response or variations in signal-to-noise across brain regions. In such cases, we may only trust the **rank order** of the dissimilarities. **Nonmetric MDS (NMDS)** is designed for precisely this situation.

#### The Ordinal Assumption and Alternating Optimization

The core assumption of NMDS is that the input dissimilarities $\delta_{ij}$ are on an [ordinal scale](@entry_id:899111). The goal is no longer to make $d_{ij}(X) \approx \delta_{ij}$, but rather to find a configuration $X$ and a **monotonic function** $f$ such that the embedded distances $d_{ij}(X)$ are as close as possible to the transformed dissimilarities, or **disparities**, $f(\delta_{ij})$. The only constraint on $f$ is that it must be non-decreasing: if $\delta_{ij} \le \delta_{kl}$, then $f(\delta_{ij}) \le f(\delta_{kl})$.

The objective is to minimize a stress function over both the coordinates $X$ and the function $f$. This is typically solved with an **alternating least-squares** algorithm :

1.  **Initialize Coordinates:** Start with an initial configuration $X^{(0)}$, often the solution from classical MDS.
2.  **Update Disparities:** Keeping the coordinates $X^{(t)}$ fixed, find the set of disparities $\{\hat{d}_{ij}\}$ that are monotonic with the original dissimilarities $\{\delta_{ij}\}$ and are closest to the current embedded distances $\{d_{ij}(X^{(t)})\}$. This is a standard statistical problem known as **[isotonic regression](@entry_id:912334)**. It finds the best non-decreasing approximation to the current distances.
3.  **Update Coordinates:** Keeping the disparities $\{\hat{d}_{ij}\}$ fixed, find the new configuration $X^{(t+1)}$ that minimizes the stress, i.e., makes the new distances $d_{ij}(X^{(t+1)})$ as close as possible to the target disparities $\{\hat{d}_{ij}\}$. This subproblem is itself a [non-convex optimization](@entry_id:634987) problem, typically solved using an iterative procedure called **Scaling by Majorizing a Complicated Function (SMACOF)**.
4.  **Iterate:** Repeat steps 2 and 3 until the stress value converges.

Because each step in this process is guaranteed to not increase the stress, the algorithm reliably converges to a (local) minimum.

#### The Robustness of Nonmetric MDS

The flexibility of the monotonic transformation $f$ gives NMDS a crucial advantage over metric MDS when the dissimilarity scale is unreliable . If the true underlying distances have been distorted by an unknown monotonic nonlinearity, metric MDS will attempt to fit this distorted scale, resulting in a "rugged" optimization landscape with many spurious local minima that can trap the algorithm. The geometric solution will be warped.

In contrast, NMDS can effectively "absorb" the nonlinear distortion into the function $f$. The algorithm finds a transformation that undoes the distortion, allowing it to fit the true, underlying geometry. This makes the optimization landscape for the coordinates "smoother" and makes the final solution more robust to [outliers](@entry_id:172866) and nonlinear scale artifacts. By decoupling the fit from the absolute magnitudes and focusing only on rank order, NMDS acts as a form of regularization, stabilizing the [geometric reconstruction](@entry_id:749855).

### Practical Considerations and Diagnostics

Successfully applying MDS requires careful consideration of several practical aspects, from the initial data processing to the final evaluation of the solution.

#### Choosing a Dissimilarity Metric

The first and most critical step is the construction of the RDM. The choice of [dissimilarity metric](@entry_id:913782) profoundly impacts the resulting representational geometry, as different metrics are sensitive to different aspects of the neural response patterns . Two common choices are Euclidean distance and [correlation distance](@entry_id:634939).

-   **Euclidean Distance**, $\|\mathbf{r}_i - \mathbf{r}_j\|$, where $\mathbf{r}_i$ is the response pattern vector for stimulus $i$, is sensitive to differences in both the overall magnitude (activation level) and the shape of the response patterns.
-   **Correlation Distance**, $1 - \text{corr}(\mathbf{r}_i, \mathbf{r}_j)$, first mean-centers and normalizes each pattern vector. It is therefore invariant to the overall activation level (mean response across voxels) and the global gain (norm of the mean-centered pattern). It exclusively measures differences in the "shape" or "profile" of the response patterns, which corresponds to the angle between the centered vectors.

Consider two response patterns where one is simply a scaled version of the other plus a constant offset, e.g., $\mathbf{r}_2 = a \mathbf{r}_1 + b\mathbf{1}$. The [correlation distance](@entry_id:634939) between them will be zero, collapsing them to a single point in the embedding. The Euclidean distance, however, will be non-zero, reflecting the differences in gain ($a$) and offset ($b$). The choice between these metrics should be driven by the scientific question: is the focus on the absolute response levels, or on the relative pattern of activity?

#### Evaluating the Solution: The Shepard Diagram

A primary diagnostic tool for any MDS solution is the **Shepard diagram** . This is a simple [scatter plot](@entry_id:171568) of the final embedded distances $d_{ij}$ (on the y-axis) against the original input dissimilarities $\delta_{ij}$ (on the x-axis).

-   For **metric MDS**, an ideal fit will show points tightly clustered around a straight line passing through the origin. The slope of this line corresponds to the scaling factor between the dissimilarities and the embedded distances.
-   For **nonmetric MDS**, a good fit will show points tightly clustered around a non-decreasing curve. The shape of this curve is informative; it is the estimated [monotonic function](@entry_id:140815) $f$. For example, a concave curve indicates that the embedding has "stretched" small dissimilarities and "compressed" large ones relative to a linear scale.

In both cases, the amount of scatter around the line or curve represents the stress, or lack of fit. A large scatter indicates a poor solution. It is important to note that even in a converged NMDS solution, there can be "monotonicity violations" in the Shepard diagram (i.e., instances where $\delta_{ij}  \delta_{kl}$ but $d_{ij} > d_{kl}$). This happens when the geometric constraints of the low-dimensional Euclidean space are incompatible with a perfectly monotonic fit, resulting in a high-stress solution. Systematic patterns in the residuals, such as residuals growing with increasing dissimilarity, can suggest that the chosen embedding dimensionality is too low and is unable to accommodate both local and global distance constraints.

#### Optimization and Convergence

Since most modern MDS applications rely on [iterative algorithms](@entry_id:160288) like SMACOF, understanding their convergence properties is essential . The stress minimization problem is non-convex, meaning it has multiple local minima. The algorithm is only guaranteed to find a [stationary point](@entry_id:164360) (where the gradient is zero), which may not be the [global minimum](@entry_id:165977).

-   **Initialization:** The choice of the starting configuration is critical. A common and effective strategy is to use the solution from classical MDS as the initial configuration for an iterative algorithm. This often provides a "warm start" that is already close to a good solution. However, when dissimilarities are highly non-Euclidean, the classical solution may be poor. In such cases, a more robust strategy is to perform **multiple random restarts**—running the algorithm from several different random initial configurations and retaining the solution with the lowest final stress.
-   **Convergence Criteria:** The iteration is typically stopped when the improvement becomes negligible. Standard criteria include the relative decrease in stress falling below a small threshold (e.g., $10^{-6}$) or the norm of the stress gradient becoming close to zero. These criteria signal that a [stationary point](@entry_id:164360) has been reached.

#### Computational Complexity and Scalability

The feasibility of MDS depends heavily on its computational demands, particularly for large numbers of stimuli $n$ .

-   **Memory:** Both classical and iterative MDS require storing the $n \times n$ [dissimilarity matrix](@entry_id:636728), and often one or more auxiliary $n \times n$ matrices. This leads to a [space complexity](@entry_id:136795) of $O(n^2)$. For double-precision numbers (8 bytes/entry), storing a single $20,000 \times 20,000$ matrix requires $3.2$ GB of RAM. This quadratic memory cost is often the primary bottleneck for very large $n$. For instance, at $n=50,000$, storing just two such matrices would require $40$ GB, exceeding the capacity of many standard workstations.

-   **Time:** The time complexities differ significantly.
    -   **Classical MDS** is dominated by the [eigendecomposition](@entry_id:181333) of the $n \times n$ Gram matrix, which has a [time complexity](@entry_id:145062) of $O(n^3)$. This cubic scaling makes it computationally infeasible for large $n$. For example, on a high-performance workstation, a classical MDS on $n=20,000$ might take on the order of 15-20 minutes.
    -   **Iterative MDS (SMACOF)** has a [time complexity](@entry_id:145062) per iteration of $O(n^2)$. The total time is this value multiplied by the number of iterations. For $n=20,000$, a single iteration might take a few seconds. A full run of 200 iterations might therefore complete in under 10 minutes.

For small to moderate $n$ (up to a few thousand), classical MDS is fast and provides a good starting point. For larger $n$, the $O(n^3)$ cost becomes prohibitive, and [iterative methods](@entry_id:139472) with their $O(n^2)$ per-iteration cost are the only viable option, with the $O(n^2)$ memory requirement ultimately setting the practical limit.