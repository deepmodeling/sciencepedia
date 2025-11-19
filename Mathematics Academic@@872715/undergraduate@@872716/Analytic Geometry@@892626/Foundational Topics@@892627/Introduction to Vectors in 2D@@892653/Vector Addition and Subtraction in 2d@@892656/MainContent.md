## Introduction
Vectors, quantities possessing both magnitude and direction, are fundamental tools for describing our world. While understanding what a vector *is* provides a starting point, the true power of vectors is unlocked when we learn how to combine them. This article addresses the essential operations of [vector addition](@entry_id:155045) and subtraction in a two-dimensional plane, moving from abstract definitions to concrete, practical mechanics. It bridges the gap between the visual intuition of vector graphics and the computational power of their algebraic forms.

This article is structured to build your expertise systematically. First, in **Principles and Mechanisms**, you will learn the core rules of vector arithmetic, exploring both the geometric "head-to-tail" method and the component-wise algebraic approach that is crucial for computation. Next, **Applications and Interdisciplinary Connections** will reveal how these simple operations serve as a foundational language in fields ranging from physics and engineering to computer graphics and finance. Finally, the **Hands-On Practices** section will allow you to solidify your understanding by applying these concepts to solve targeted problems in geometry and optimization.

## Principles and Mechanisms

In the preceding chapter, we introduced vectors as mathematical objects possessing both magnitude and direction. We now move from this abstract definition to the practical mechanics of how vectors interact. This chapter delves into the principles of vector addition and subtraction in a two-dimensional plane. We will begin with the intuitive geometric interpretation of these operations and then build a rigorous algebraic framework. Finally, we will explore how these simple operations provide a powerful language for describing and solving complex problems in geometry, physics, and engineering.

### Geometric Interpretation of Vector Operations

The most intuitive way to understand vector operations is by visualizing them as displacements. Imagine an autonomous rover on a flat plain, starting at an origin point $O$. A vector can represent a single leg of its journey.

#### Vector Addition: The Head-to-Tail Rule

If the rover first travels from the origin $O$ to a point $A$, this journey is described by a displacement vector $\overrightarrow{OA}$. If it then continues from point $A$ to a new point $B$, this second leg is described by vector $\overrightarrow{AB}$. The total, or **resultant**, displacement from the starting point $O$ to the final point $B$ is given by the vector $\overrightarrow{OB}$. The combination of these sequential journeys is the essence of [vector addition](@entry_id:155045). We write this as:

$$
\overrightarrow{OB} = \overrightarrow{OA} + \overrightarrow{AB}
$$

This is known as the **[head-to-tail rule](@entry_id:176302)**: to add vector $\vec{b}$ to vector $\vec{a}$, we draw $\vec{b}$ starting from the head (the tip) of $\vec{a}$. The resultant vector, $\vec{a} + \vec{b}$, is the vector drawn from the tail (the start) of $\vec{a}$ to the head of $\vec{b}$. This forms a triangle, which is why it is also called the **triangle rule of vector addition**. This principle is fundamental for tracking cumulative changes, such as the final position of a rover after multiple maneuvers [@problem_id:2174266].

An equivalent geometric construction is the **[parallelogram rule](@entry_id:154297)**. If two vectors $\vec{a}$ and $\vec{b}$ are drawn originating from the same point, they form two adjacent sides of a parallelogram. Their sum, $\vec{a} + \vec{b}$, is the vector corresponding to the long diagonal of that parallelogram, also starting from the common origin.

#### Vector Subtraction

Vector subtraction, $\vec{a} - \vec{b}$, can be defined as the addition of a negative vector: $\vec{a} + (-\vec{b})$. The vector $-\vec{b}$ has the same magnitude as $\vec{b}$ but points in the exact opposite direction.

Geometrically, subtraction has a particularly useful interpretation. When two vectors $\vec{a}$ and $\vec{b}$ are drawn from a common origin, the vector $\vec{a} - \vec{b}$ is the vector that points from the head of $\vec{b}$ to the head of $\vec{a}$. This can be seen by observing the triangle rule: $\vec{b} + (\vec{a} - \vec{b}) = \vec{a}$.

If we revisit the parallelogram formed by $\vec{a}$ and $\vec{b}$ originating from the same point, we find a remarkable geometric insight. While the sum $\vec{a} + \vec{b}$ represents the main diagonal, the difference $\vec{a} - \vec{b}$ (or $\vec{b} - \vec{a}$) represents the other diagonal, connecting the tips of the two vectors [@problem_id:2174281].

### Algebraic Representation in Cartesian Coordinates

While geometric rules provide intuition, the true computational power of vectors is unlocked through algebra. In a 2D Cartesian plane, we can represent any vector by its **components** along the horizontal (x) and vertical (y) axes. A vector $\vec{v}$ can be written as an [ordered pair](@entry_id:148349) $\vec{v} = \langle v_x, v_y \rangle$ or in terms of the [standard basis vectors](@entry_id:152417) $\hat{i} = \langle 1, 0 \rangle$ and $\hat{j} = \langle 0, 1 \rangle$ as $\vec{v} = v_x \hat{i} + v_y \hat{j}$.

The geometric operations of addition and subtraction translate into simple algebraic rules:

*   **Vector Addition**: To add two vectors, we add their corresponding components.
    If $\vec{a} = \langle a_x, a_y \rangle$ and $\vec{b} = \langle b_x, b_y \rangle$, then:
    $$
    \vec{a} + \vec{b} = \langle a_x + b_x, a_y + b_y \rangle
    $$

*   **Vector Subtraction**: To subtract two vectors, we subtract their corresponding components.
    $$
    \vec{a} - \vec{b} = \langle a_x - b_x, a_y - b_y \rangle
    $$

For instance, if a rover's displacement from an origin $O$ to point $A$ is $\vec{d}_{OA} = \langle 12.5, -8.3 \rangle$ km, and its subsequent displacement from $A$ to $B$ is $\vec{d}_{AB} = \langle -4.8, 15.1 \rangle$ km, the total displacement vector from the origin to its final position is the component-wise sum [@problem_id:2174266]:
$$
\vec{d}_{OB} = \vec{d}_{OA} + \vec{d}_{AB} = \langle 12.5 - 4.8, -8.3 + 15.1 \rangle = \langle 7.7, 6.8 \rangle \text{ km}
$$

The **magnitude** (or length) of a vector $\vec{v} = \langle v_x, v_y \rangle$, denoted $||\vec{v}||$, is found using the Pythagorean theorem:
$$
||\vec{v}|| = \sqrt{v_x^2 + v_y^2}
$$

A crucial distinction must be made between the magnitude of the resultant displacement and the total path distance traveled. The path distance is the sum of the magnitudes of each individual displacement vector, whereas the resultant displacement's magnitude is the length of the vector sum. The **[triangle inequality](@entry_id:143750)** formalizes this relationship:
$$
||\vec{a} + \vec{b}|| \le ||\vec{a}|| + ||\vec{b}||
$$
This inequality states that the length of one side of a triangle cannot be greater than the sum of the lengths of the other two sides. Equality holds only in the specific case where vectors $\vec{a}$ and $\vec{b}$ point in the same direction (i.e., are collinear). For any journey with a change in direction, the final displacement will always be shorter than the total distance traveled [@problem_id:2174265].

### Position Vectors and Geometric Applications

The algebraic framework becomes exceptionally powerful when we introduce the concept of a **[position vector](@entry_id:168381)**. The position vector of a point $P(p_x, p_y)$, denoted $\vec{r}_P$, is the vector from the origin $O$ to point $P$, so $\vec{r}_P = \langle p_x, p_y \rangle$.

This allows us to describe the relationship between points using vector subtraction. The displacement vector from a point $A$ to a point $B$ is simply the difference between their [position vectors](@entry_id:174826):
$$
\overrightarrow{AB} = \vec{r}_B - \vec{r}_A
$$
This simple expression is the key to translating complex geometric problems into the language of vector algebra.

#### Dividing Line Segments

A common geometric task is to find a point that divides a line segment in a specific ratio. Vector algebra provides an elegant solution.

Consider the line segment between points $A$ and $B$, with [position vectors](@entry_id:174826) $\vec{r}_A$ and $\vec{r}_B$. The **midpoint**, $M$, of this segment can be found by starting at $A$ and traveling halfway along the vector $\overrightarrow{AB}$.
$$
\vec{r}_M = \vec{r}_A + \frac{1}{2}\overrightarrow{AB} = \vec{r}_A + \frac{1}{2}(\vec{r}_B - \vec{r}_A) = \frac{1}{2}\vec{r}_A + \frac{1}{2}\vec{r}_B = \frac{1}{2}(\vec{r}_A + \vec{r}_B)
$$
The position vector of the midpoint is simply the average of the [position vectors](@entry_id:174826) of the endpoints.

This leads to a classic proof of the **Midpoint Theorem**. Let $P$ be the midpoint of side $AB$ and $Q$ be the midpoint of side $AC$ in a triangle $ABC$. The vector from $P$ to $Q$ is [@problem_id:2174236]:
$$
\overrightarrow{PQ} = \vec{r}_Q - \vec{r}_P = \frac{1}{2}(\vec{r}_A + \vec{r}_C) - \frac{1}{2}(\vec{r}_A + \vec{r}_B) = \frac{1}{2}(\vec{r}_C - \vec{r}_B) = \frac{1}{2}\overrightarrow{BC}
$$
This concise vector proof demonstrates that the segment connecting the midpoints of two sides of a triangle is parallel to the third side and exactly half its length.

We can generalize this to find any point $C$ that divides the segment $AB$ in a ratio $m:n$ (meaning the distance from $A$ to $C$ is $\frac{m}{m+n}$ of the total length). This is known as the **[section formula](@entry_id:163285)**. The position vector $\vec{r}_C$ is a weighted average of the endpoint vectors [@problem_id:2174273]:
$$
\vec{r}_C = \frac{n\vec{r}_A + m\vec{r}_B}{m+n}
$$
For example, a point that is four times farther from $A$ than from $B$ would divide the segment in the ratio $m:n = 4:1$.

A beautiful application of this principle is in locating the **[centroid](@entry_id:265015)** of a triangle, which is the physical center of mass and the intersection point of the medians. A median connects a vertex to the midpoint of the opposite side. Let's find the [centroid](@entry_id:265015) $P$ by finding the point on the median from vertex $A$ to the midpoint $M$ of side $BC$. The centroid is known to divide the median in a $2:1$ ratio ($AP:PM = 2:1$). Using the [section formula](@entry_id:163285) with $m=2$ and $n=1$ on segment $AM$ [@problem_id:2174287]:
$$
\vec{r}_P = \frac{1 \cdot \vec{r}_A + 2 \cdot \vec{r}_M}{1+2} = \frac{1}{3}(\vec{r}_A + 2\vec{r}_M)
$$
Since $M$ is the midpoint of $BC$, we have $\vec{r}_M = \frac{1}{2}(\vec{r}_B + \vec{r}_C)$. Substituting this in gives:
$$
\vec{r}_P = \frac{1}{3}\left(\vec{r}_A + 2 \cdot \frac{1}{2}(\vec{r}_B + \vec{r}_C)\right) = \frac{1}{3}(\vec{r}_A + \vec{r}_B + \vec{r}_C)
$$
The [position vector](@entry_id:168381) of the centroid is simply the average of the [position vectors](@entry_id:174826) of the three vertices.

#### Condition for Collinearity

Vectors also provide a straightforward test for whether three points lie on the same line. Three distinct points $P_1$, $P_2$, and $P_3$ are **collinear** if and only if the [displacement vector](@entry_id:262782) from $P_1$ to $P_2$ is parallel to the [displacement vector](@entry_id:262782) from $P_1$ to $P_3$. Two vectors are parallel if one is a scalar multiple of the other. Thus, the condition for collinearity is:
$$
\overrightarrow{P_1P_2} = k \cdot \overrightarrow{P_1P_3}
$$
for some non-zero scalar $k$. In component form, this gives two [linear equations](@entry_id:151487), which can be used to solve for unknown parameters that ensure collinearity [@problem_id:2174240].

### Advanced Principles and Strategies

The elementary operations of addition and subtraction form the basis for more sophisticated applications and problem-solving techniques.

#### Vector Decomposition and Basis Vectors

We typically express vectors in terms of the orthogonal basis vectors $\hat{i}$ and $\hat{j}$. However, it is often useful to express a vector as a sum of multiples of other, non-[orthogonal vectors](@entry_id:142226). Any two non-zero, non-parallel vectors $\vec{u}$ and $\vec{v}$ can form a **basis** for a 2D plane. This means that any other vector $\vec{w}$ in that plane can be uniquely expressed as a **linear combination** of $\vec{u}$ and $\vec{v}$:
$$
\vec{w} = c_1 \vec{u} + c_2 \vec{v}
$$
The scalars $c_1$ and $c_2$ are the components of $\vec{w}$ in the basis $\{\vec{u}, \vec{v}\}$. Finding these scalars involves solving a system of two [linear equations](@entry_id:151487). This is a common problem in physics and engineering, for example, when determining the required forces from two thrusters acting in different directions to produce a specific resultant force [@problem_id:2174254].

#### The Principle of Symmetry and Zero Sum

In systems with high degrees of symmetry, [vector addition](@entry_id:155045) can lead to powerful simplifications. Consider the vectors pointing from the center of a regular $N$-gon to each of its $N$ vertices. For every vector in the set, there is another vector (or combination of vectors) that exactly cancels it out. Therefore, the sum of all these vectors is the zero vector, $\vec{0}$.

This **zero-sum principle** is a potent problem-solving tool. Imagine a system where $N$ forces, symmetrically arranged, are in equilibrium (sum to zero). If some of these forces are removed, what is the resultant of the remaining ones? Let $\vec{F}_{active}$ be the sum of the remaining forces and $\vec{F}_{inactive}$ be the sum of the removed forces. Since the total sum was zero:
$$
\vec{F}_{active} + \vec{F}_{inactive} = \vec{0} \implies \vec{F}_{active} = - \vec{F}_{inactive}
$$
The resultant force of the many active components is simply the negative of the sum of the few inactive components. This can dramatically reduce the complexity of a calculation [@problem_id:2174253].

#### Vectors and Circular Geometry

Vector subtraction is the natural language for describing circles. A circle is defined as the set of all points equidistant from a center. In vector terms, a circle of radius $R$ centered at a point $C$ (with position vector $\vec{c}$) is the set of all points $P$ (with position vector $\vec{p}$) that satisfy the equation:
$$
||\vec{p} - \vec{c}|| = R
$$
This equation states that the magnitude of the displacement vector from the center $C$ to the point $P$ is constant.

This definition allows us to analyze geometric properties of circles using [vector algebra](@entry_id:152340). For example, consider two points $P_1$ and $P_2$ on this circle. The distance between them can be found by examining the square of the magnitude of their difference vector, $\vec{p}_1 - \vec{p}_2$. Letting $\vec{d}_1 = \vec{p}_1 - \vec{c}$ and $\vec{d}_2 = \vec{p}_2 - \vec{c}$ be the displacement vectors from the center, we know $||\vec{d}_1|| = ||\vec{d}_2|| = R$. The vector between the points is $\vec{p}_1 - \vec{p}_2 = \vec{d}_1 - \vec{d}_2$. The square of the distance is [@problem_id:2174270]:
$$
||\vec{p}_1 - \vec{p}_2||^2 = ||\vec{d}_1 - \vec{d}_2||^2 = (\vec{d}_1 - \vec{d}_2) \cdot (\vec{d}_1 - \vec{d}_2)
$$
$$
= ||\vec{d}_1||^2 + ||\vec{d}_2||^2 - 2(\vec{d}_1 \cdot \vec{d}_2)
$$
Using the definition of the dot product, $\vec{d}_1 \cdot \vec{d}_2 = ||\vec{d}_1|| ||\vec{d}_2|| \cos\theta = R^2 \cos\theta$, where $\theta$ is the angle between the two displacement vectors from the center. Substituting this in, we get:
$$
||\vec{p}_1 - \vec{p}_2||^2 = R^2 + R^2 - 2R^2 \cos\theta = 2R^2(1 - \cos\theta)
$$
This result is the Law of Cosines, derived entirely through vector operations, showcasing the unifying power of the vector framework.