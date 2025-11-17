## Introduction
In the worlds of modern design and engineering simulation, the ability to represent complex geometries with both precision and flexibility is paramount. For decades, a fundamental gap has existed between the smooth, exact representations used in Computer-Aided Design (CAD) and the faceted, approximate meshes required for Finite Element Analysis (FEA). This disconnect necessitates time-consuming and error-prone translation steps. Non-Uniform Rational B-Splines (NURBS) provide a powerful mathematical framework to bridge this divide. This article serves as a comprehensive guide to the construction and application of B-spline and NURBS bases, laying the groundwork for understanding their central role in both advanced geometric modeling and the revolutionary paradigm of Isogeometric Analysis.

The following chapters will guide you from foundational theory to practical application. We will begin in "Principles and Mechanisms" by deconstructing B-[splines](@entry_id:143749) and NURBS, exploring their mathematical building blocks like knot vectors and control points, and examining the core algorithms that govern their behavior. Next, "Applications and Interdisciplinary Connections" will demonstrate how these principles are leveraged to create exact geometric models in CAD and to unify design and simulation through Isogeometric Analysis. Finally, "Hands-On Practices" will provide opportunities to solidify your understanding by tackling practical problems related to spline construction and analysis.

## Principles and Mechanisms

Having established the motivation for employing [splines](@entry_id:143749) in both geometric design and [numerical analysis](@entry_id:142637), we now turn to the foundational principles and mechanisms that govern their construction and behavior. This chapter will deconstruct B-splines and NURBS from their elementary building blocks, revealing the elegant mathematical structure that provides their power and flexibility. We will explore how these [piecewise polynomial](@entry_id:144637) functions are defined, what properties they possess, and how they can be manipulated through a set of powerful algorithms.

### The Building Blocks of B-Splines

At the heart of any B-[spline](@entry_id:636691) construction are two fundamental choices: the polynomial degree and the [knot vector](@entry_id:176218). These two components, in concert, define the entire function space from which basis functions are drawn.

#### The Knot Vector

A **[knot vector](@entry_id:176218)**, denoted by $\mathbf{U}$, is a non-decreasing [sequence of real numbers](@entry_id:141090), $\mathbf{U} = \{\xi_0, \xi_1, \dots, \xi_m\}$, called [knots](@entry_id:637393). The knots are parameter values that partition the parametric domain into segments, known as **knot spans**. A knot span is an interval $[\xi_i, \xi_{i+1}]$; if $\xi_i  \xi_{i+1}$, the span is non-degenerate and forms the domain for a single polynomial piece of the spline. If $\xi_i = \xi_{i+1}$, the span is degenerate, having zero length.

The structure of the [knot vector](@entry_id:176218) is critical. An **open [knot vector](@entry_id:176218)** is one where the first and last knot values are repeated with a specific [multiplicity](@entry_id:136466). If this multiplicity is $p+1$, where $p$ is the polynomial degree, the vector is said to be **clamped**. Clamped knot vectors are standard in [isogeometric analysis](@entry_id:145267) because they ensure the basis functions interpolate the first and last control points, a property crucial for applying boundary conditions. A [knot vector](@entry_id:176218) is considered **uniform** if all its interior knots are equally spaced; otherwise, it is **non-uniform**. Non-uniformity allows for local control over the shape and continuity of the [spline](@entry_id:636691).

#### Polynomial Degree and Basis Function Space

The **polynomial degree**, denoted by $p$, specifies the degree of the polynomial pieces that constitute the [spline](@entry_id:636691). A B-[spline](@entry_id:636691) of degree $p=1$ is piecewise linear, $p=2$ is piecewise quadratic, and so on. The degree determines the smoothness and approximation power of the basis.

There is a fundamental relationship connecting the number of knots, the polynomial degree, and the number of B-spline basis functions, $N$, that can be constructed. For a [knot vector](@entry_id:176218) $\mathbf{U}$ with $m+1$ [knots](@entry_id:637393) (indexed from $0$ to $m$) and a given degree $p$, the number of basis functions is given by:

$N = m - p$

This is often written as $N = (\text{number of knots}) - (\text{degree}) - 1$. For instance, for a quadratic B-spline ($p=2$) defined on the [knot vector](@entry_id:176218) $\mathbf{U}=\{0,0,0,0.3,0.6,1,1,1\}$, the number of knots is $8$ (so $m=7$). The number of basis functions is $N = 8 - 2 - 1 = 5$ [@problem_id:2584872]. This relationship dictates the dimension of the resulting spline space. For a bivariate tensor-product space, the total dimension is simply the product of the dimensions in each parametric direction [@problem_id:2584832].

#### Continuity at Knots

The smoothness of a B-spline curve is controlled by the **[multiplicity](@entry_id:136466)** of the knots in the [knot vector](@entry_id:176218). The multiplicity of a knot $\bar{\xi}$, denoted $k_{\bar{\xi}}$, is the number of times its value appears in the [knot vector](@entry_id:176218). While a higher degree $p$ generally implies greater smoothness, repeated [knots](@entry_id:637393) can locally reduce this smoothness.

The continuity of a B-spline basis of degree $p$ at a knot $\bar{\xi}$ with multiplicity $k$ is given by $C^{p-k}$. The order of continuity, $r$, is therefore defined by the formula:

$r = p - k$

A continuity of $r=0$ implies the function is $C^0$, or continuous, but its first derivative is discontinuous (a "sharp corner" in the tangent). A continuity of $r=1$ implies the function and its first derivative are continuous ($C^1$), but the second derivative is not. A simple knot ($k=1$) provides the maximum possible smoothness for a given degree, which is $C^{p-1}$. Each additional repetition of the knot sacrifices one order of [differentiability](@entry_id:140863) [@problem_id:2584852].

Let us again consider the quadratic ($p=2$) [spline](@entry_id:636691) with [knot vector](@entry_id:176218) $\mathbf{U}=\{0,0,0,0.3,0.6,1,1,1\}$. The interior [knots](@entry_id:637393) are $0.3$ and $0.6$.
- At the knot $\xi=0.3$, the multiplicity is $k_{0.3}=1$. The continuity order is $r_{0.3} = p - k_{0.3} = 2 - 1 = 1$. The basis is $C^1$ continuous here.
- At the knot $\xi=0.6$, the multiplicity is also $k_{0.6}=1$. The continuity order is $r_{0.6} = p - k_{0.6} = 2 - 1 = 1$. The basis is also $C^1$ continuous here.

Note that at the endpoints $0$ and $1$, the multiplicity is $k=3$. For $p=2$, this gives a continuity of $r = 2 - 3 = -1$, which signifies a discontinuity. In the context of a [clamped spline](@entry_id:162763), this reduction in continuity to below $C^0$ is what forces the curve to pass through its endpoint control points.

### The B-[spline](@entry_id:636691) Basis Functions

With the foundational concepts in place, we can now formally define the B-[spline](@entry_id:636691) basis functions, denoted $N_{i,p}(\xi)$, where $i$ is the function index and $p$ is the degree.

#### The Cox-de Boor Recursion Formula

The B-[spline](@entry_id:636691) basis functions are defined recursively. The [recursion](@entry_id:264696) starts with the case of degree $p=0$, which are simple piecewise-constant functions:

$N_{i,0}(\xi) = \begin{cases} 1  \text{ if } \xi_i \le \xi  \xi_{i+1} \\ 0  \text{ otherwise} \end{cases}$

For degrees $p > 0$, the basis functions are constructed as a linear combination of two basis functions of degree $p-1$. This is the celebrated **Cox-de Boor [recursion](@entry_id:264696) formula**:

$N_{i,p}(\xi) = \frac{\xi - \xi_i}{\xi_{i+p} - \xi_i} N_{i,p-1}(\xi) + \frac{\xi_{i+p+1} - \xi}{\xi_{i+p+1} - \xi_{i+1}} N_{i+1,p-1}(\xi)$

In this formula, any term of the form $\frac{0}{0}$ is defined to be zero. This convention is essential for correctly handling repeated knots. The two coefficients in the formula, $\frac{\xi - \xi_i}{\xi_{i+p} - \xi_i}$ and $\frac{\xi_{i+p+1} - \xi}{\xi_{i+p+1} - \xi_{i+1}}$, are linear functions of $\xi$ that range from $0$ to $1$ over their respective intervals. This [recursive definition](@entry_id:265514) beautifully encodes all the properties of B-[splines](@entry_id:143749) [@problem_id:2584832].

#### Fundamental Properties

The [recursive definition](@entry_id:265514) gives rise to several crucial properties that make B-splines so useful.

**Local Support:** Each [basis function](@entry_id:170178) $N_{i,p}(\xi)$ is non-zero only over a limited portion of the parametric domain. Specifically, the **support** of $N_{i,p}(\xi)$ is the interval $[\xi_i, \xi_{i+p+1}]$. Outside this interval, the function is identically zero. This local support property is fundamental. When a B-[spline](@entry_id:636691) curve is defined as a weighted sum of these basis functions, moving a single control point only affects the shape of the curve within the local support of its corresponding [basis function](@entry_id:170178). This makes B-splines highly intuitive and efficient for both design and analysis. For a uniform [knot vector](@entry_id:176218) with spacing $h$, this locality can be quantified. The effect of moving a control point $P_i$ is confined to a region of radius $r = \frac{(p+1)h}{2}$ around the corresponding Greville abscissa (a characteristic parameter for the [basis function](@entry_id:170178)) [@problem_id:2584858].

**Partition of Unity:** For any parameter value $\xi$ in the domain, the sum of all B-[spline](@entry_id:636691) basis functions is exactly one:

$\sum_{i=0}^{n} N_{i,p}(\xi) = 1$

**Non-negativity:** For any $\xi$, every basis function is non-negative: $N_{i,p}(\xi) \ge 0$.

Together, the partition of unity and non-negativity properties imply that a B-[spline](@entry_id:636691) curve lies entirely within the **convex hull** of its control points. This is a powerful shape-preserving property, as it guarantees the curve will not oscillate wildly away from its defining control polygon.

#### Derivatives of B-[spline](@entry_id:636691) Basis Functions

The derivative of a B-spline basis function is also a spline, but of a lower degree. Differentiating the Cox-de Boor recursion formula yields a formula for the derivative of $N_{i,p}(\xi)$:

$N'_{i,p}(\xi) = p \left( \frac{N_{i,p-1}(\xi)}{\xi_{i+p} - \xi_i} - \frac{N_{i+1,p-1}(\xi)}{\xi_{i+p+1} - \xi_{i+1}} \right)$

This formula shows that the derivative of a degree-$p$ basis function can be expressed in terms of degree-$(p-1)$ basis functions. By applying this recursively, we can obtain explicit [piecewise polynomial](@entry_id:144637) expressions for the derivatives on each knot span. For instance, we can derive the piecewise linear expressions for the derivatives of a set of [quadratic basis functions](@entry_id:753898) [@problem_id:2584831]. A useful property that follows from the partition of unity is that the sum of the derivatives of all basis functions is zero: $\sum_i N'_{i,p}(\xi) = 0$.

### From Basis Functions to Geometric Curves and Surfaces

Once a set of basis functions is defined, we can construct geometric entities.

A **B-[spline](@entry_id:636691) curve** $\mathbf{C}(\xi)$ is a vector-valued function defined as a [linear combination](@entry_id:155091) of B-[spline](@entry_id:636691) basis functions $N_{i,p}(\xi)$ and a set of control points $\mathbf{P}_i$:

$\mathbf{C}(\xi) = \sum_{i=0}^{n} N_{i,p}(\xi) \mathbf{P}_i$

The control points form a **control polygon** that guides the shape of the curve. Thanks to the local support property, moving a control point $\mathbf{P}_k$ only influences the curve's shape in the region where $N_{k,p}(\xi)$ is non-zero.

This concept extends naturally to higher dimensions. A **tensor-product B-spline surface** $\mathbf{S}(\xi, \eta)$ is constructed from two univariate B-[spline](@entry_id:636691) bases, $\{N_{i,p}(\xi)\}$ and $\{M_{j,q}(\eta)\}$, and a grid of control points $\mathbf{P}_{i,j}$:

$\mathbf{S}(\xi, \eta) = \sum_{i=0}^{n} \sum_{j=0}^{k} N_{i,p}(\xi) M_{j,q}(\eta) \mathbf{P}_{i,j}$

The bivariate basis functions are simply the products of the univariate ones. The dimension of the resulting [function space](@entry_id:136890) is the product of the number of basis functions in each direction [@problem_id:2584832].

For applications in [isogeometric analysis](@entry_id:145267), it is useful to think of the geometry as being composed of **elements**. Each non-degenerate knot span $[\xi_j, \xi_{j+1}]$ defines a parametric element. On any given element, only a subset of the [global basis functions](@entry_id:749917) will be non-zero. The number of active basis functions on any element is always $p+1$. The indices of these active functions form the element's **connectivity array**, which is directly analogous to the element connectivity used in traditional [finite element methods](@entry_id:749389). This provides a clear bridge between the geometric representation and the analysis mesh [@problem_id:2584854].

### Non-Uniform Rational B-Splines (NURBS)

While B-splines are powerful, they cannot represent common shapes like circles and ellipses exactly. This limitation is overcome by **Non-Uniform Rational B-Splines (NURBS)**, which are a generalization of B-[splines](@entry_id:143749).

#### Introducing Weights and Homogeneous Coordinates

NURBS introduce a weight $w_i$ for each control point $\mathbf{P}_i$. The construction is most elegantly understood through the concept of [homogeneous coordinates](@entry_id:154569). Each control point $\mathbf{P}_i = (x_i, y_i, \dots)$ in $\mathbb{R}^d$ is lifted into a [projective space](@entry_id:149949) $\mathbb{R}^{d+1}$ by multiplying by its weight: $\mathbf{P}^w_i = (w_i x_i, w_i y_i, \dots, w_i)$. A standard B-spline curve is then constructed in this higher-dimensional space:

$\mathbf{C}^w(\xi) = \sum_{i=0}^{n} N_{i,p}(\xi) \mathbf{P}^w_i$

The physical NURBS curve $\mathbf{C}(\xi)$ is obtained by projecting $\mathbf{C}^w(\xi)$ back down to $\mathbb{R}^d$ by dividing by its last component:

$\mathbf{C}(\xi) = \frac{\sum_{i=0}^{n} N_{i,p}(\xi) w_i \mathbf{P}_i}{\sum_{i=0}^{n} N_{i,p}(\xi) w_i}$

The denominator, $W(\xi) = \sum_i N_{i,p}(\xi) w_i$, is the scalar weight function. The functions $R_{i,p}(\xi) = \frac{N_{i,p}(\xi) w_i}{W(\xi)}$ are the **rational basis functions**. They still form a [partition of unity](@entry_id:141893), provided $W(\xi) \neq 0$ [@problem_id:2584835].

#### The Role of Weights

The weights provide an extra degree of freedom for shaping the curve.

- **Positive Weights:** If all weights $w_i$ are positive, the denominator $W(\xi)$ is also always positive. In this case, the rational basis functions $R_{i,p}(\xi)$ remain non-negative, and the [convex hull property](@entry_id:168245) is preserved. This is the standard case used in nearly all practical applications.

- **Non-Positive Weights:** Allowing negative or zero weights has significant consequences. If a weight $w_k$ is negative, the corresponding rational [basis function](@entry_id:170178) $R_{k,p}(\xi)$ can become negative. This means the curve is no longer a convex combination of its control points, and it can, and generally will, lie outside the convex hull. Furthermore, the denominator $W(\xi)$ can become zero for certain parameter values. These values correspond to **poles** in the curve, where the geometry extends to infinity. A practical example with weights $\{1, -2, 1\}$ demonstrates both the loss of the [convex hull property](@entry_id:168245) and the existence of poles within the domain [@problem_id:2584835].

### Key Mechanisms and Algorithms

A set of stable and efficient algorithms exists for evaluating and manipulating B-spline and NURBS geometries.

#### Curve Evaluation: The de Boor Algorithm

**De Boor's algorithm** is a computationally efficient and numerically stable method for evaluating a point on a B-[spline](@entry_id:636691) curve. It is the geometric equivalent of the Cox-de Boor recursion. To evaluate $\mathbf{C}(\xi)$, the algorithm first identifies the knot span $[\xi_k, \xi_{k+1}]$ that contains $\xi$. Then, it performs $p$ stages of repeated linear interpolation, starting with the $p+1$ control points that influence the curve in that span. The process generates a triangular table of intermediate points, converging to the final point on the curve [@problem_id:2584869]. For NURBS curves, the algorithm is applied in [homogeneous coordinates](@entry_id:154569) before the final projection.

#### Knot Insertion (Boehm's Algorithm)

**Knot insertion** is a fundamental process for refining a B-spline or NURBS curve without changing its shape or [parameterization](@entry_id:265163). This process, also known as **Boehm's algorithm**, adds a new knot to the [knot vector](@entry_id:176218) and computes a new set of control points that define the exact same curve. The formulas for the new control points are derived directly from the Cox-de Boor recursion. This algorithm is essential for [mesh refinement](@entry_id:168565) in [isogeometric analysis](@entry_id:145267) and for creating Bézier segments from a B-spline. For NURBS, the procedure is carried out on the homogeneous control points [@problem_id:2584875].

#### Degree Elevation

It is also possible to increase the polynomial degree of a B-spline or NURBS curve without changing its geometry. This process, called **degree elevation**, introduces new control points and modifies the [knot vector](@entry_id:176218). A particularly clear way to understand degree elevation is to first decompose a B-[spline](@entry_id:636691) into its constituent **Bézier segments**. This can be done by inserting [knots](@entry_id:637393) until every interior knot has [multiplicity](@entry_id:136466) $p$. The resulting segments are Bézier curves, and the degree elevation formula for a Bézier curve is straightforward. After elevating the degree of each segment, the segments can be reassembled into a single B-spline of higher degree [@problem_id:2584845].

#### Interfacing and Boundary Conditions

In practical modeling, complex objects are often built from multiple NURBS patches. Ensuring continuity across patch interfaces is critical. For two patches to have **$C^0$ (positional) continuity** and form a conforming isogeometric mesh, their shared boundary must be geometrically identical. This requires that the boundary curves of the two patches have the same definition. This is achieved if, along the common boundary:
1. The polynomial degrees match.
2. The knot vectors match (up to orientation).
3. The control points are coincident.
4. The weights are identical (or proportional).
Failure to meet these conditions results in a [non-conforming mesh](@entry_id:171638) with gaps or overlaps, which poses challenges for numerical analysis [@problem_id:2584848].

Finally, the structure of NURBS provides an elegant way to handle boundary conditions. As mentioned, a **clamped [knot vector](@entry_id:176218)** (where the first and last knots have [multiplicity](@entry_id:136466) $p+1$) forces the B-[spline](@entry_id:636691) basis to be interpolatory at the domain endpoints. For example, $N_{0,p}(0)=1$ and $N_{i,p}(0)=0$ for $i0$. This property is inherited by the rational basis functions, regardless of the weights: $R_{0,p}(0)=1$. As a result, the value of the NURBS curve at the boundary is simply the first control point, $\mathbf{C}(0) = \mathbf{P}_0$. This allows for the **strong imposition of Dirichlet boundary conditions** in an isogeometric simulation by simply setting the value of the boundary control points to the desired boundary value [@problem_id:2584834]. This direct and exact imposition is a significant advantage of [isogeometric analysis](@entry_id:145267) over traditional FEM.