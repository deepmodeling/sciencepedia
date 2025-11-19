## Introduction
High-quality [mesh generation](@entry_id:149105) is a cornerstone of reliable computational analysis, particularly within the Finite Element Method (FEM). The geometric shape of mesh elements is not a mere aesthetic concern; it profoundly impacts the accuracy, stability, and efficiency of numerical simulations. Generating a mesh with poorly shaped elements can introduce significant errors and lead to unreliable results, creating a critical knowledge gap between theoretical models and their practical implementation. This article addresses this challenge by providing a deep dive into two dominant paradigms for unstructured [mesh generation](@entry_id:149105): the Advancing Front Method and Delaunay Triangulation. Across three comprehensive chapters, you will gain a robust understanding of the core concepts that drive modern [meshing](@entry_id:269463). The "Principles and Mechanisms" chapter will establish the mathematical foundations of [mesh quality](@entry_id:151343) and detail the algorithms behind both methods. Following this, the "Applications and Interdisciplinary Connections" chapter will explore how these techniques are adapted for complex geometries, error control, and specialized fields like CFD. Finally, the "Hands-On Practices" section will solidify your knowledge with practical exercises in geometric predicates. By navigating these topics, you will learn not just the 'how' but the 'why' of creating meshes that ensure high-fidelity computational results.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms underpinning the generation of high-quality triangular and tetrahedral meshes, focusing on two dominant paradigms: the Advancing Front Method and Delaunay Triangulation. We will begin by establishing why geometric quality is paramount in the context of the Finite Element Method (FEM), defining rigorous metrics to quantify it. We will then introduce the Delaunay [triangulation](@entry_id:272253) as a geometrically optimal construction, exploring its properties, algorithms for its computation, and its inherent limitations. Subsequently, we will examine how these idealized concepts are adapted to handle the practical complexities of real-world domains through constrained triangulations and the heuristic yet powerful [advancing front method](@entry_id:171934). Finally, we will briefly venture into three dimensions to highlight the unique challenges, such as sliver tetrahedra, that distinguish 3D from 2D [meshing](@entry_id:269463).

### Foundational Concepts: Defining and Motivating Mesh Quality

The accuracy and stability of a Finite Element simulation are inextricably linked to the geometric quality of the underlying mesh. A mesh composed of poorly shaped elements can lead to large interpolation errors, [ill-conditioned system](@entry_id:142776) matrices, and ultimately, unreliable numerical results. To formalize the notion of a "good" element, we must first define quantitative measures of quality.

#### Triangle Quality Metrics

For a given triangle $K$ in the plane, several metrics are used to characterize its shape. Let $h_K$ be its diameter (the length of its longest edge), $h_{\min}(K)$ be the length of its shortest edge, $\rho_K$ its inradius (radius of the largest inscribed circle), and $R_K$ its circumradius (radius of the smallest circumscribed circle). The interior angles are denoted $\theta_1, \theta_2, \theta_3$.

-   The **minimum angle**, $\theta_{\min}(K) = \min\{\theta_1, \theta_2, \theta_3\}$, is arguably the most intuitive quality measure. Triangles with very small angles are termed "skinny" or "degenerate" and are generally undesirable. A uniform lower bound $\theta_{\min}(K) \ge \theta_0 > 0$ for all triangles in a mesh family is a common requirement for ensuring shape regularity.

-   The **[aspect ratio](@entry_id:177707)**, often defined as $AR(K) = h_K / \rho_K$, measures the "roundness" of the triangle. For an equilateral triangle, this ratio is minimized. As a triangle becomes skinnier, its inradius $\rho_K$ shrinks relative to its diameter $h_K$, causing the aspect ratio to grow. Imposing a uniform upper bound on the [aspect ratio](@entry_id:177707) is equivalent to imposing a uniform lower bound on the minimum angle [@problem_id:2540787].

-   The **radius-edge ratio**, defined as $Q_{\mathrm{RE}}(K) = R_K / h_{\min}(K)$, relates the circumradius to the shortest edge length. This metric is directly connected to the minimum angle by the identity derived from the Law of Sines:
    $$ Q_{\mathrm{RE}}(K) = \frac{1}{2 \sin(\theta_{\min}(K))} $$
    This identity shows that bounding the radius-edge ratio from above is also equivalent to bounding the minimum angle from below [@problem_id:2540787].

The fundamental reason these geometric metrics are critical lies in their direct influence on the [interpolation error](@entry_id:139425), a key component of the total FEM error. For a sufficiently smooth function $u \in H^2(\Omega)$, the standard [a priori estimate](@entry_id:188293) for the error of linear interpolation ($I_h u$) on a single element $K$ is given by:
$$ |u - I_h u|_{H^1(K)} \le C(K) h_K |u|_{H^2(K)} $$
Here, $| \cdot |_{H^1(K)}$ and $| \cdot |_{H^2(K)}$ are Sobolev seminorms that measure the "energy" of the function's first and second derivatives, respectively. The crucial term is the constant $C(K)$, which depends on the shape of the triangle but not its size. This constant can be shown to be directly proportional to the [aspect ratio](@entry_id:177707), $C(K) \propto h_K / \rho_K$ [@problem_id:2540787]. Therefore, a mesh with elements of large [aspect ratio](@entry_id:177707) (or, equivalently, small minimum angle) will have a large [interpolation error](@entry_id:139425) constant, compromising accuracy.

Another way to see this is by considering the affine map $x = B \hat{x} + b$ that transforms a fixed reference triangle $\hat{K}$ to the physical triangle $K$. The condition number of the Jacobian matrix, $\kappa(B) = \sigma_{\max}(B)/\sigma_{\min}(B)$, where $\sigma_{\max}$ and $\sigma_{\min}$ are its largest and smallest singular values, measures the distortion of this mapping. A large $\kappa(B)$ corresponds to a highly stretched, anisotropic element. The [interpolation error](@entry_id:139425) constant $C(K)$ is directly proportional to $\kappa(B)$, meaning that large geometric distortion deteriorates interpolation accuracy [@problem_id:2540787].

#### The Consequences of Poor Quality on Numerical Stability

Beyond interpolation accuracy, poor element quality has severe consequences for the conditioning of the global stiffness matrix, $K_{fem}$. For a second-order elliptic problem like linear elasticity discretized with piecewise linear ($P_1$) elements, the condition number of the [stiffness matrix](@entry_id:178659), $\kappa(K_{fem}) = \lambda_{\max}(K_{fem}) / \lambda_{\min}(K_{fem})$, exhibits a dependence on both the mesh size $h$ and the minimum angle $\theta_{\min}$. A well-established scaling law is:
$$ \kappa(K_{fem}) \sim C \cdot h_{\max}^{-2} \cdot \frac{1}{\sin^2(\theta_{\min})} $$
where $h_{\max}$ is the maximum element diameter in the mesh [@problem_id:2540758].

This relation reveals two important facts. First, the condition number necessarily degrades as the mesh is refined ($h_{\max} \to 0$). Second, the degradation is dramatically accelerated by the presence of small angles. For instance, consider two meshes with comparable $h_{\max}$, one generated by a high-quality Delaunay method with $\theta_{\min} \approx 30^\circ$, and another generated by a less careful process that produces a region of skewed triangles with $\theta_{\min} \approx 1^\circ$. The factor $1/\sin^2(\theta_{\min})$ will cause the condition number of the second mesh's [stiffness matrix](@entry_id:178659) to be larger by a factor of approximately $(\sin 30^\circ / \sin 1^\circ)^2 \approx (0.5 / 0.01745)^2 \approx 820$. This severe ill-conditioning can make the linear system difficult for iterative solvers to converge and amplifies the effects of numerical round-off error [@problem_id:2540758]. Specifically, the relative error in the computed displacement vector $\mathbf{u}$ due to a perturbation $\delta\mathbf{f}$ in the [load vector](@entry_id:635284) $\mathbf{f}$ is bounded by $\kappa(K_{fem})$:
$$ \frac{\|\delta \mathbf{u}\|}{\|\mathbf{u}\|} \le \kappa(K_{fem}) \frac{\|\delta \mathbf{f}\|}{\|\mathbf{f}\|} $$
Thus, a mesh with poor angles leads to a system that is highly sensitive to small errors in the input data, undermining the reliability of the simulation results. It is also important to note that this conditioning behavior depends on the mesh geometry itself, not the algorithm used to generate it. If an [advancing front method](@entry_id:171934) and a Delaunay method both produce meshes with the same minimum angle guarantee, their conditioning behavior will be comparable [@problem_id:2540758].

### The Delaunay Triangulation: A Geometric Optimality Criterion

Given the importance of maintaining large minimum angles, a natural question arises: for a fixed set of vertices, what is the "best" way to connect them to form a [triangulation](@entry_id:272253)? The Delaunay [triangulation](@entry_id:272253) provides a powerful and elegant answer to this question.

#### Defining the Delaunay Triangulation and its Dual

The Delaunay triangulation can be defined through its intimate relationship with another fundamental geometric structure: the **Voronoi diagram**. Given a set of points $P = \{p_1, \dots, p_n\}$ in the plane, the Voronoi diagram partitions the plane into regions, or cells, where each cell $V(p_i)$ consists of all points in the plane that are closer to site $p_i$ than to any other site $p_j$ [@problem_id:2540771].
$$ V(p_i) = \{ x \in \mathbb{R}^2 : \|x - p_i\| \le \|x - p_j\| \text{ for all } j \neq i \} $$
The boundary between two cells, $V(p_i)$ and $V(p_j)$, is a segment of the [perpendicular bisector](@entry_id:176427) of the line segment connecting $p_i$ and $p_j$.

The **Delaunay triangulation**, denoted $\mathrm{DT}(P)$, is the geometric dual of the Voronoi diagram. This duality creates a precise correspondence between their features (assuming the points are in **general position**, meaning no three points are collinear and no four are cocircular):
-   Each site $p_i$ in $P$ corresponds to a Voronoi cell $V(p_i)$.
-   An edge connects two sites $p_i$ and $p_j$ in $\mathrm{DT}(P)$ if and only if their Voronoi cells $V(p_i)$ and $V(p_j)$ share a common boundary edge.
-   A triangle $\triangle p_i p_j p_k$ exists in $\mathrm{DT}(P)$ if and only if the Voronoi cells $V(p_i)$, $V(p_j)$, and $V(p_k)$ meet at a single vertex. This Voronoi vertex is the [circumcenter](@entry_id:174510) of the triangle $\triangle p_i p_j p_k$ [@problem_id:2540771].

While the dual relationship is profound, a more direct and commonly used definition of the Delaunay [triangulation](@entry_id:272253) is the **[empty circumcircle property](@entry_id:635047)**. A [triangulation](@entry_id:272253) $T$ of a point set $P$ is a Delaunay [triangulation](@entry_id:272253) if and only if for every triangle in $T$, its open circumdisk (the interior of the circle passing through its three vertices) contains no point from the set $P$ [@problem_id:2540770].

#### Key Properties and Characterizations

The [empty circumcircle property](@entry_id:635047) gives rise to several other important characterizations that are key to both understanding and computing Delaunay triangulations.

1.  **Angle Optimality**: The most celebrated property of the Delaunay [triangulation](@entry_id:272253) is that it is **angle-optimal**. Among all possible triangulations of a given point set $P$, the Delaunay triangulation maximizes the minimum interior angle. More strongly, it produces the lexicographically largest sorted vector of angles. This "max-min" property directly aligns with our goal of avoiding skinny triangles and makes the Delaunay triangulation a natural choice for FEM [mesh generation](@entry_id:149105) [@problem_id:2540757].

2.  **Local Delaunay Criterion**: Consider an interior edge $pq$ shared by two triangles $\triangle pqr$ and $\triangle pqs$, which together form a convex quadrilateral $prqs$. The edge $pq$ is locally Delaunay if the point $s$ does not lie inside the [circumcircle](@entry_id:165300) of $\triangle pqr$. This condition is equivalent to the sum of the angles opposite the shared edge being no more than $\pi$: $\angle prq + \angle psq \le \pi$. If this condition is violated (i.e., $\angle prq + \angle psq > \pi$), the edge $pq$ is not locally Delaunay and can be "flipped" to the alternative diagonal $rs$. This flip will improve the local angle configuration. A triangulation is globally Delaunay if and only if all of its interior edges satisfy this local criterion [@problem_id:2540770]. This property forms the basis of simple and effective edge-flipping algorithms for constructing the triangulation.

It is important to address the case of degeneracies. If four or more points are cocircular, the Delaunay [triangulation](@entry_id:272253) is not unique. For a convex quadrilateral with cocircular vertices, both diagonals satisfy the angle criterion with equality ($\angle prq + \angle psq = \pi$). In this case, either diagonal can be chosen, leading to multiple valid Delaunay triangulations. However, each of these triangulations correctly satisfies the [empty circumcircle property](@entry_id:635047) [@problem_id:2540770].

#### Strengths and Limitations

The max-min angle property explains why Delaunay [triangulation](@entry_id:272253) is so effective at producing well-shaped elements in the interior of a domain where points are quasi-uniformly distributed. The algorithm naturally avoids configurations that produce unnecessarily small angles by selecting diagonals that are locally optimal [@problem_id:2540757].

However, the standard Delaunay algorithm has a significant limitation: it can produce very skinny triangles near boundaries, particularly at sharp corners. Consider a sharp corner at the origin $O$ with two points $A$ and $B$ placed at an equal distance $r$ on the two rays forming a small angle $\phi$. The triangle $\triangle OAB$ will have a minimum angle of $\phi$, which can be arbitrarily small. If there are no other points inside the [circumcircle](@entry_id:165300) of $\triangle OAB$ (a condition easily satisfied by placing other points sufficiently far away), then $\triangle OAB$ satisfies the [empty circumcircle property](@entry_id:635047) and will be part of the Delaunay [triangulation](@entry_id:272253). The algorithm has no alternative "flip" to consider, as the edge $AB$ is on the [convex hull](@entry_id:262864) of the local point set. It legally and correctly includes this poor-quality triangle because its definition is purely geometric and oblivious to the notion of a "boundary" [@problem_id:2540757]. This limitation motivates the need for constrained triangulations, which we will discuss shortly.

### Algorithms for Delaunay Triangulation

Numerous algorithms have been developed to compute the Delaunay [triangulation](@entry_id:272253) of a set of $n$ points. Before examining specific methods, it is essential to understand the fundamental complexity of the problem. A reduction from the sorting problem (by mapping numbers $x_i$ to points $(x_i, x_i^2)$ on a parabola) establishes a worst-case lower bound of $\Omega(n \log n)$ for any comparison-based algorithm. Therefore, algorithms that achieve an $\mathcal{O}(n \log n)$ [time complexity](@entry_id:145062) are considered asymptotically optimal [@problem_id:2540801].

#### Incremental Insertion: The Bowyer–Watson Algorithm

One of the most popular and elegant methods is the incremental insertion algorithm, also known as the Bowyer–Watson algorithm. The idea is to build the triangulation by adding points one by one. Suppose we have a valid Delaunay [triangulation](@entry_id:272253) of a set of points $P_i$, and we want to insert a new point $p_{i+1}$. The algorithm proceeds in three steps:

1.  **Cavity Identification**: Find all triangles in the current [triangulation](@entry_id:272253) whose circumcircles contain the new point $p_{i+1}$. The union of these "bad" triangles forms a star-shaped polygonal region called the **cavity**.
2.  **Cavity Deletion**: Remove all the "bad" triangles from the triangulation, leaving the polygonal cavity.
3.  **Retriangulation**: Form new triangles by connecting the new point $p_{i+1}$ to all vertices on the boundary of the cavity.

By construction, the resulting set of triangles is guaranteed to be a valid Delaunay triangulation of the updated point set $P_{i+1}$.

Let's illustrate with a concrete example [@problem_id:2540812]. Suppose our initial points are $P_1=(0,0)$, $P_2=(5,0)$, and $P_3=(0,4)$, forming a single triangle $T_0 = \triangle P_1P_2P_3$.
-   **Insert $P_4=(1,1)$**: First, we check if $P_4$ is inside the [circumcircle](@entry_id:165300) of $T_0$. The [circumcenter](@entry_id:174510) of $T_0$ is the intersection of the [perpendicular bisectors](@entry_id:163148) $x=2.5$ and $y=2$, which is $C_0=(2.5, 2)$. The squared circumradius is $R_0^2 = (0-2.5)^2 + (0-2)^2 = 10.25$. The squared distance from $P_4$ to $C_0$ is $(1-2.5)^2 + (1-2)^2 = 3.25$. Since $3.25  10.25$, $P_4$ is inside the [circumcircle](@entry_id:165300). The cavity is the single triangle $T_0$. We delete $T_0$ and connect $P_4$ to the cavity boundary vertices ($P_1, P_2, P_3$), creating three new triangles: $\triangle P_1P_2P_4$, $\triangle P_2P_3P_4$, and $\triangle P_3P_1P_4$.
-   **Insert $P_5=(2, 1.5)$**: We now have three triangles. We must check $P_5$ against each of their circumcircles. After performing the calculations (by comparing squared distances to avoid costly square roots), we find that $P_5$ is inside the [circumcircle](@entry_id:165300) of $\triangle P_2P_3P_4$ but outside the others. Thus, the cavity consists only of $\triangle P_2P_3P_4$. We delete this triangle and form three new ones by connecting $P_5$ to the cavity vertices $P_2, P_3, P_4$: $\triangle P_2P_3P_5$, $\triangle P_3P_4P_5$, and $\triangle P_4P_2P_5$. The final [triangulation](@entry_id:272253) consists of 5 triangles.

The complexity of the incremental algorithm depends heavily on the point location step (finding the initial triangle containing the new point) and the insertion order. A naive implementation can have a [worst-case complexity](@entry_id:270834) of $\mathcal{O}(n^2)$. However, if the points are inserted in a **uniformly [random permutation](@entry_id:270972)** and a clever **history-based point location structure** (a [directed acyclic graph](@entry_id:155158) of all triangles ever created) is used, the algorithm achieves an optimal expected time of $\mathcal{O}(n \log n)$ with $\mathcal{O}(n)$ expected space [@problem_id:2540801].

#### Other Optimal Algorithmic Paradigms

Two other classical algorithms also achieve optimal worst-case performance:

-   **Divide and Conquer**: This algorithm, pioneered by Guibas and Stolfi, presorts the points by their x-coordinate and recursively splits the set in half. It computes the Delaunay triangulation of each half and then merges the two resulting triangulations. The merge step, which involves finding and adding the "cross edges" that connect the two point sets, can be performed in linear time. The resulting recurrence relation, $T(n) = 2T(n/2) + \mathcal{O}(n)$, solves to the optimal $\mathcal{O}(n \log n)$ [@problem_id:2540801].

-   **Sweepline Algorithm**: Fortune's algorithm computes the Voronoi diagram by sweeping a vertical line across the plane. The state of the algorithm is maintained in two [data structures](@entry_id:262134): an event queue (a priority queue storing "site events" and "circle events") and a [balanced binary search tree](@entry_id:636550) representing the "beach line" (the boundary of the computed Voronoi cells). Each of the $\mathcal{O}(n)$ events is processed in $\mathcal{O}(\log n)$ time, leading to an overall optimal [worst-case complexity](@entry_id:270834) of $\mathcal{O}(n \log n)$ [@problem_id:2540801].

### Meshing Practical Domains: Constraints and Advancing Fronts

Real-world engineering problems rarely involve triangulating a simple set of points. Instead, we must mesh complex domains with prescribed boundaries, internal interfaces, and holes. This requires more sophisticated tools.

#### Constrained Delaunay Triangulation (CDT)

To handle complex domains, we first represent the geometry as a **Planar Straight-Line Graph (PSLG)**. A PSLG is a collection of vertices and non-crossing line segments (constraints) that define the boundary of the domain and any internal features [@problem_id:2540772].

The **Constrained Delaunay Triangulation (CDT)** is a modification of the Delaunay [triangulation](@entry_id:272253) that is forced to include all the constraint segments from the PSLG. Because some constraint segments may not be "Delaunay" in the classical sense, the [empty circumcircle property](@entry_id:635047) must be relaxed. This is achieved through the concept of **visibility**. Two points are said to be visible to each other if the line segment connecting them does not properly intersect any constraint segment [@problem_id:2540772].

The CDT is then defined as a triangulation that includes all constraint segments and satisfies a modified Delaunay property: for any triangle $\triangle pqr$ in the CDT, its [circumcircle](@entry_id:165300) contains no vertex $v$ from the PSLG that is visible from the interior of the triangle. The local edge-flipping criterion is also modified: an edge can only be flipped if the new diagonal does not cross a constraint segment. This ensures that the essential geometric features of the domain are preserved in the final mesh [@problem_id:2540772].

#### The Advancing Front Method (AFM)

A popular alternative to Delaunay-based methods is the **Advancing Front Method (AFM)**. Unlike Delaunay methods, which are point-set driven, AFM is a boundary-driven heuristic. The algorithm initializes a "front" with the discretized boundary segments of the domain and systematically adds new triangles, advancing the front inwards until the entire domain is filled.

A typical step in an advancing front algorithm proceeds as follows [@problem_id:2604579]:
1.  Select an edge $(\mathbf{a}, \mathbf{b})$ of length $\ell$ from the current front.
2.  Choose a target size for the new triangle's edges. A simple strategy is to use a radius $r = \eta \ell$, where $\eta$ is a user-defined parameter.
3.  Construct an ideal new vertex $\mathbf{p}$ at one of the two intersections of circles of radius $r$ centered at $\mathbf{a}$ and $\mathbf{b}$. The point on the interior side of the front is chosen.
4.  Check for conflicts (e.g., if the new triangle $\triangle\mathbf{abp}$ would overlap with the existing mesh or cross the front). If there are no conflicts, add the triangle and update the front by removing edge $(\mathbf{a}, \mathbf{b})$ and adding edges $(\mathbf{a}, \mathbf{p})$ and $(\mathbf{p}, \mathbf{b})$.

This method provides direct control over element quality. The geometry of the newly formed isosceles triangle is determined entirely by the parameter $\eta$. To guarantee a minimum angle of at least $\beta$, one must choose $\eta$ within the interval:
$$ \frac{1}{2\cos \beta} \le \eta \le \frac{1}{2\sin(\beta/2)} $$
For example, to generate equilateral triangles ($\beta = 60^\circ = \pi/3$), one must choose $\eta=1$ [@problem_id:2604579].

Crucially, practical [mesh generation](@entry_id:149105) requires not just angle control but also size control. AFM, like other advanced methods, typically takes a background **sizing function** $h(\mathbf{x})$ as input, which specifies the desired local edge length at any point $\mathbf{x}$ in the domain. An effective algorithm will generate a mesh where element sizes conform to this function. For such a mesh, the total number of triangles $N$ is asymptotically related to the sizing function by the integral:
$$ N = \Theta\left(\int_{\Omega} h(\mathbf{x})^{-2}\, \mathrm{d}\mathbf{x}\right) $$
This result underscores that both shape quality (controlled by parameters like $\eta$) and size control (via $h(\mathbf{x})$) are essential for generating efficient and accurate meshes [@problem_id:2604579].

### Extending to Three Dimensions: The Challenge of Slivers

Extending these meshing concepts to three dimensions presents significant new challenges. While the definitions of Voronoi diagrams and Delaunay triangulations generalize directly, the guarantees of quality do not. In 2D, ensuring a lower bound on the minimum angle (or an upper bound on the radius-edge ratio) is sufficient to produce a high-quality mesh. In 3D, this is no longer true.

The primary [pathology](@entry_id:193640) in 3D meshing is the **sliver tetrahedron**. A sliver is a tetrahedron whose four vertices are nearly coplanar, resulting in extremely small or large dihedral (face-to-face) angles, even if all six of its edge lengths are comparable. Such elements are numerically disastrous in FEM.

The danger of slivers is that they can be perfectly valid Delaunay elements and can evade simple quality checks that work in 2D. Consider a canonical example: four points placed on a sphere of radius $R$ that are symmetric with respect to the coordinate planes but are only slightly perturbed from the $xy$-plane by a small height $\pm R\sin\varepsilon$ [@problem_id:2540762].
-   As the perturbation parameter $\varepsilon \to 0$, the four vertices become coplanar. The tetrahedron's volume approaches zero, and its [dihedral angles](@entry_id:185221) tend to the extreme values of $0$ and $\pi$.
-   However, all its edge lengths remain of the same order, $\Theta(R)$.
-   Its circumradius is fixed at $R$ by construction. Its shortest edge length approaches $R\sqrt{2}$.
-   Therefore, its radius-edge ratio $Q(\varepsilon) = R_c(\varepsilon)/l_{\min}(\varepsilon)$ approaches the perfectly reasonable value of $1/\sqrt{2}$.

This example demonstrates a critical lesson: a bounded radius-edge ratio, a reliable quality indicator in 2D, is **not sufficient** to exclude sliver tetrahedra in 3D [@problem_id:2540762]. Delaunay refinement algorithms in 3D must employ more sophisticated quality metrics (such as [dihedral angles](@entry_id:185221) or the condition number of the element Jacobian) and specialized sliver-exudation techniques to produce meshes suitable for robust numerical simulation.