## Introduction
The Lie bracket is a cornerstone of modern mathematics and physics, providing the algebraic structure that defines a Lie algebra. While abstractly it is just a [binary operation](@entry_id:143782) satisfying certain axioms, its true power is revealed in its concrete computations, which capture the essence of [non-commutativity](@entry_id:153545) in systems ranging from quantum mechanics to robotics. The significance of the Lie bracket lies in its ability to quantify the result of performing two infinitesimal transformations in different orders; the non-zero outcome of a Lie bracket is not a failure, but a rich source of new information about the system's structure.

This article addresses the gap between the abstract definition of the Lie bracket and its practical calculation. It serves as a comprehensive guide for computing this crucial operation in its most important contexts. By mastering these computational techniques, you will gain a deeper understanding of the structure of Lie algebras and their profound implications across science and engineering.

Over the next three chapters, we will embark on a journey from first principles to practical application. The first chapter, **"Principles and Mechanisms,"** will dissect the core computational methods, from the straightforward [matrix commutator](@entry_id:273812) to the geometric interpretation involving vector fields and the algebraic utility of [structure constants](@entry_id:157960). The second chapter, **"Applications and Interdisciplinary Connections,"** will demonstrate why these computations matter, exploring how the Lie bracket underpins concepts in physics, control theory, and advanced mathematics. Finally, the **"Hands-On Practices"** section will provide you with opportunities to apply these techniques to solve concrete problems, solidifying your understanding.

## Principles and Mechanisms

The Lie bracket is the defining operation of a Lie algebra, endowing a vector space with a non-associative algebraic structure that captures the essence of infinitesimal transformations. While the previous chapter introduced the abstract axioms of a Lie algebra, this chapter delves into the principles and mechanisms of computing the Lie bracket in its most important concrete realizations: as a [matrix commutator](@entry_id:273812), as an operator on [vector fields](@entry_id:161384), and through its abstract structural properties.

### The Matrix Commutator: A Concrete Realization

For Lie algebras composed of matrices, the Lie bracket is almost invariably defined as the **[matrix commutator](@entry_id:273812)**. Given two square matrices $X$ and $Y$ of the same dimension, their commutator, denoted $[X, Y]$, is defined as:

$$
[X, Y] = XY - YX
$$

This operation measures the degree to which [matrix multiplication](@entry_id:156035) fails to be commutative. If $XY = YX$, the matrices are said to commute, and their bracket is the [zero matrix](@entry_id:155836). The set of all $n \times n$ matrices over a field (e.g., $\mathbb{R}$ or $\mathbb{C}$), denoted $\mathfrak{gl}(n)$, forms a Lie algebra under this operation.

A key property of the commutator is that the trace of any commutator is identically zero. This follows from the cyclic property of the trace, $\text{Tr}(AB) = \text{Tr}(BA)$:

$$
\text{Tr}([X, Y]) = \text{Tr}(XY - YX) = \text{Tr}(XY) - \text{Tr}(YX) = 0
$$

This has a significant consequence: the set of all $n \times n$ matrices with zero trace, known as the special linear algebra $\mathfrak{sl}(n)$, is closed under the commutator. If $X$ and $Y$ are traceless, then $[X, Y]$ is also traceless, making $\mathfrak{sl}(n)$ a subalgebra of $\mathfrak{gl}(n)$.

Let us perform a direct computation to solidify this concept. Consider two matrices within the algebra $\mathfrak{gl}(2, \mathbb{C})$ of $2 \times 2$ [complex matrices](@entry_id:190650), parameterized by real variables $\alpha, \beta, \gamma, \delta$:

$$
X = \begin{pmatrix} \alpha & 1+i \\ 1-i & \beta \end{pmatrix}, \quad Y = \begin{pmatrix} \gamma & -i\delta \\ i\delta & 0 \end{pmatrix}
$$

To find their Lie bracket $[X, Y]$, we first compute the products $XY$ and $YX$:

$$
XY = \begin{pmatrix} \alpha\gamma+(1+i)(i\delta) & \alpha(-i\delta) \\ (1-i)\gamma+\beta(i\delta) & (1-i)(-i\delta) \end{pmatrix} = \begin{pmatrix} \alpha\gamma-\delta+i\delta & -i\alpha\delta \\ \gamma-i\gamma+i\beta\delta & -\delta-i\delta \end{pmatrix}
$$

$$
YX = \begin{pmatrix} \gamma\alpha+(-i\delta)(1-i) & \gamma(1+i)+(-i\delta)\beta \\ i\delta\alpha & i\delta(1+i) \end{pmatrix} = \begin{pmatrix} \alpha\gamma-\delta-i\delta & \gamma+i\gamma-i\beta\delta \\ i\alpha\delta & -\delta+i\delta \end{pmatrix}
$$

Subtracting the second result from the first yields the commutator:

$$
[X, Y] = XY - YX = \begin{pmatrix} 2i\delta & -\gamma-i\gamma-i\alpha\delta+i\beta\delta \\ \gamma-i\gamma+i\beta\delta-i\alpha\delta & -2i\delta \end{pmatrix}
$$

Notice that the resulting matrix is indeed traceless, as expected. We can further characterize this matrix by its determinant:
$$
\det([X, Y]) = (2i\delta)(-2i\delta) - (-\gamma(1+i)+i\delta(\beta-\alpha))(\gamma(1-i)+i\delta(\beta-\alpha))
$$
$$
= 4\delta^2 - (-\gamma(1+i)\gamma(1-i) - \gamma(1+i)i\delta(\beta-\alpha) + i\delta(\beta-\alpha)\gamma(1-i) - \delta^2(\beta-\alpha)^2)
$$
$$
= 4\delta^2 - (-2\gamma^2 + i\gamma\delta(\beta-\alpha)(-1-i+1-i) - \delta^2(\beta-\alpha)^2)
$$
$$
= 4\delta^2 - (-2\gamma^2 + 2\gamma\delta(\beta-\alpha) - \delta^2(\beta-\alpha)^2)
$$
$$
= \delta^2\bigl((\beta-\alpha)^2+4\bigr)-2\gamma\delta(\beta-\alpha)+2\gamma^2
$$
This calculation demonstrates that the Lie bracket is a well-defined [binary operation](@entry_id:143782) that takes two elements of the [matrix algebra](@entry_id:153824) and produces a third element, whose properties can be further analyzed. [@problem_id:647364]

### Fundamental Algebraic Properties and Structure Constants

The Lie bracket, regardless of its specific realization, must satisfy three fundamental axioms:

1.  **Bilinearity:** The bracket is linear in each of its arguments. For scalars $a, b$ and algebra elements $X, Y, Z$:
    $$ [aX + bY, Z] = a[X, Z] + b[Y, Z] $$
    $$ [Z, aX + bY] = a[Z, X] + b[Z, Y] $$

2.  **Anti-commutativity:** Swapping the arguments negates the result.
    $$ [X, Y] = -[Y, X] $$
    This implies $[X, X] = 0$ for any element $X$.

3.  **The Jacobi Identity:** This identity is the counterpart to the [associative law](@entry_id:165469) in other algebraic structures.
    $$ [X, [Y, Z]] + [Y, [Z, X]] + [Z, [X, Y]] = 0 $$

For the [matrix commutator](@entry_id:273812), [bilinearity](@entry_id:146819) and anti-commutativity are immediately evident from the definition. The Jacobi identity can be verified by direct expansion:
$$
[X, [Y, Z]] = X(YZ - ZY) - (YZ - ZY)X = XYZ - XZY - YZX + ZYX
$$
By cyclically permuting $X, Y, Z$, we find the other two terms:
$$
[Y, [Z, X]] = YZX - YXZ - ZXY + XZY
$$
$$
[Z, [X, Y]] = ZXY - ZYX - XYZ + YXZ
$$
Summing these three expressions, we see that all terms cancel in pairs, yielding zero.

To see the Jacobi identity in a physically significant context, consider the Lie algebra $\mathfrak{su}(2)$, which is fundamental to the quantum mechanical theory of spin. A basis for $\mathfrak{su}(2)$ can be given by the three Pauli matrices, $\sigma_1, \sigma_2, \sigma_3$. They satisfy the commutation relations $[ \sigma_i, \sigma_j ] = 2i \sum_{k=1}^3 \varepsilon_{ijk} \sigma_k$, where $\varepsilon_{ijk}$ is the Levi-Civita symbol. Let's verify the Jacobi identity for these basis elements.
We compute the inner commutators first:
$$[\sigma_2, \sigma_3] = 2i \varepsilon_{231} \sigma_1 = 2i\sigma_1$$
$$[\sigma_3, \sigma_1] = 2i \varepsilon_{312} \sigma_2 = 2i\sigma_2$$
$$[\sigma_1, \sigma_2] = 2i \varepsilon_{123} \sigma_3 = 2i\sigma_3$$
Substituting these into the Jacobi identity expression, which we may call the "Jacobiator" $J(\sigma_1, \sigma_2, \sigma_3)$:
$$ J(\sigma_1, \sigma_2, \sigma_3) = [\sigma_1, [\sigma_2, \sigma_3]] + [\sigma_2, [\sigma_3, \sigma_1]] + [\sigma_3, [\sigma_1, \sigma_2]] $$
$$ = [\sigma_1, 2i\sigma_1] + [\sigma_2, 2i\sigma_2] + [\sigma_3, 2i\sigma_3] $$
Since the commutator of any matrix with itself (or a scalar multiple of itself) is zero, each term vanishes:
$$ = 2i[\sigma_1, \sigma_1] + 2i[\sigma_2, \sigma_2] + 2i[\sigma_3, \sigma_3] = 0 + 0 + 0 = 0 $$
The Jacobi identity holds, and therefore the trace of the Jacobiator is also trivially 0. This confirms that the commutator operation on $\mathfrak{su}(2)$ indeed forms a valid Lie algebra. [@problem_id:647378]

#### Structure Constants

The [bilinearity](@entry_id:146819) of the Lie bracket implies that if we know the commutators of all basis elements of a Lie algebra, we can compute the bracket of any two arbitrary elements. If $\{T_1, T_2, \dots, T_n\}$ is a basis for a Lie algebra $\mathfrak{g}$, then the bracket $[T_i, T_j]$ must also be an element of $\mathfrak{g}$ and can thus be written as a [linear combination](@entry_id:155091) of the basis elements:
$$
[T_i, T_j] = \sum_{k=1}^n c^k_{ij} T_k
$$
The coefficients $c^k_{ij}$ are known as the **[structure constants](@entry_id:157960)** of the Lie algebra with respect to the basis $\{T_i\}$. They completely define the Lie bracket operation and therefore the entire algebraic structure.

For example, the [commutation relations](@entry_id:136780) for $\mathfrak{so}(3)$, the algebra of [infinitesimal rotations](@entry_id:166635), are often given abstractly in terms of generators $J_x, J_y, J_z$:
$$ [J_x, J_y] = J_z, \quad [J_y, J_z] = J_x, \quad [J_z, J_x] = J_y $$
Here, the [structure constants](@entry_id:157960) (relative to the ordered basis $\{J_x, J_y, J_z\}$) are simply components of the Levi-Civita symbol, e.g., $c^z_{xy} = 1$, $c^x_{xy}=0$, etc. These relations are sufficient to compute any bracket. For instance, consider two elements $A = a_x J_x + a_z J_z$ and $B = b_y J_y + b_z J_z$. Their commutator is:
$$ [A,B] = [a_x J_x + a_z J_z, b_y J_y + b_z J_z] $$
Using [bilinearity](@entry_id:146819), we expand this into four terms:
$$ [A,B] = a_x b_y [J_x, J_y] + a_x b_z [J_x, J_z] + a_z b_y [J_z, J_y] + a_z b_z [J_z, J_z] $$
Using the known relations ($[J_x, J_z] = -[J_z, J_x] = -J_y$, etc.), this becomes:
$$ [A,B] = a_x b_y J_z - a_x b_z J_y - a_z b_y J_x + 0 = -a_z b_y J_x - a_x b_z J_y + a_x b_y J_z $$
This result finds application in areas like the Baker-Campbell-Hausdorff formula, which relates Lie algebra elements to elements of the corresponding Lie group. [@problem_id:647373]

The [structure constants](@entry_id:157960) depend on the chosen basis. A particularly insightful example is the isomorphism between the Lie algebra $\mathfrak{so}(3)$ (real $3 \times 3$ [skew-symmetric matrices](@entry_id:195119)) and the vector space $\mathbb{R}^3$ equipped with the cross product. The [isomorphism](@entry_id:137127) $\phi: (\mathbb{R}^3, \times) \to (\mathfrak{so}(3), [\cdot, \cdot])$ is such that $\phi(\mathbf{v}_1 \times \mathbf{v}_2) = [\phi(\mathbf{v}_1), \phi(\mathbf{v}_2)]$. If we take the standard [orthonormal basis](@entry_id:147779) $\{\mathbf{e}_1, \mathbf{e}_2, \mathbf{e}_3\}$ for $\mathbb{R}^3$, the [cross product](@entry_id:156749) relations are $\mathbf{e}_i \times \mathbf{e}_j = \sum_k \varepsilon_{ijk} \mathbf{e}_k$. The Levi-Civita symbols $\varepsilon_{ijk}$ are the structure constants. If we change to a new basis, say $\mathbf{b}_1 = \mathbf{e}_1 + \alpha \mathbf{e}_2$, $\mathbf{b}_2 = \mathbf{e}_2 + \beta \mathbf{e}_3$, $\mathbf{b}_3 = \mathbf{e}_3 + \gamma \mathbf{e}_1$, the structure of the algebra remains the same, but the constants $d_{ijk}$ in the relation $[\phi(\mathbf{b}_i), \phi(\mathbf{b}_j)] = \sum_k d_{ijk} \phi(\mathbf{b}_k)$ will change. To find them, one computes the cross product in the new basis, e.g., $\mathbf{b}_1 \times \mathbf{b}_2 = \alpha\beta \mathbf{e}_1 - \beta \mathbf{e}_2 + \mathbf{e}_3$, and then expresses this resultant vector as a [linear combination](@entry_id:155091) of $\{\mathbf{b}_1, \mathbf{b}_2, \mathbf{b}_3\}$. The coefficients of this combination are the new structure constants. [@problem_id:647254]

A final example from particle physics involves the Lie algebra $\mathfrak{su}(3)$, whose generators are the eight Gell-Mann matrices $\lambda_a$. Let's consider two elements $X = \alpha(\lambda_4 + i\lambda_5)$ and $Y = \beta(\lambda_4 - i\lambda_5)$ in the [complexification](@entry_id:260775) $\mathfrak{sl}(3, \mathbb{C})$. Given the explicit matrix forms:
$$ \lambda_4 = \begin{pmatrix} 0 & 0 & 1 \\ 0 & 0 & 0 \\ 1 & 0 & 0 \end{pmatrix}, \quad \lambda_5 = \begin{pmatrix} 0 & 0 & -i \\ 0 & 0 & 0 \\ i & 0 & 0 \end{pmatrix} $$
We find that $\lambda_4 + i\lambda_5 = 2 \begin{pmatrix} 0 & 0 & 1 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix}$ and $\lambda_4 - i\lambda_5 = 2 \begin{pmatrix} 0 & 0 & 0 \\ 0 & 0 & 0 \\ 1 & 0 & 0 \end{pmatrix}$. Let's denote the matrix with a 1 in the $i$-th row and $j$-th column as $E_{ij}$. Then $X=2\alpha E_{13}$ and $Y=2\beta E_{31}$. Their commutator is:
$$ [X, Y] = 4\alpha\beta [E_{13}, E_{31}] = 4\alpha\beta (E_{13}E_{31} - E_{31}E_{13}) $$
Using standard [matrix multiplication](@entry_id:156035) rules, $E_{ij}E_{kl} = \delta_{jk}E_{il}$, we have:
$$ [X, Y] = 4\alpha\beta (E_{11} - E_{33}) = 4\alpha\beta \begin{pmatrix} 1 & 0 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & -1 \end{pmatrix} $$
To express this result in the Gell-Mann basis, we note that $\lambda_3 = \text{diag}(1, -1, 0)$ and $\lambda_8 = \frac{1}{\sqrt{3}}\text{diag}(1, 1, -2)$. The matrix $E_{11} - E_{33}$ can be decomposed as a linear combination of these. One finds $E_{11} - E_{33} = \frac{1}{2}\lambda_3 + \frac{\sqrt{3}}{2}\lambda_8$. Therefore:
$$ [X, Y] = 4\alpha\beta \left( \frac{1}{2}\lambda_3 + \frac{\sqrt{3}}{2}\lambda_8 \right) = 2\alpha\beta \lambda_3 + 2\sqrt{3}\alpha\beta \lambda_8 $$
From this, we can read off the coefficients of the resulting linear combination; for example, the coefficient of $\lambda_3$ is $c_3 = 2\alpha\beta$. This demonstrates the common procedure of computing a bracket and decomposing the result back into the chosen basis. [@problem_id:647368]

### The Geometric Interpretation: Vector Fields and Lie Derivatives

In differential geometry, the Lie bracket finds a natural and powerful interpretation as an operator on [vector fields](@entry_id:161384). A vector field $V$ on a manifold (e.g., $\mathbb{R}^n$) can be viewed as a first-order [linear differential operator](@entry_id:174781) that acts on smooth functions. In Cartesian coordinates $(x^1, \dots, x^n)$, it is written as:
$$ V = \sum_{i=1}^n V^i(x) \frac{\partial}{\partial x^i} $$
where the $V^i(x)$ are [smooth functions](@entry_id:138942).

The **Lie bracket** of two [vector fields](@entry_id:161384), $X$ and $Y$, is another vector field $[X, Y]$ defined by its action on any smooth function $f$:
$$ [X, Y](f) = X(Y(f)) - Y(X(f)) $$
This definition has a profound geometric meaning: it measures the failure of infinitesimal flows along the vector fields to commute. The operator $[X, Y]$ essentially corresponds to the displacement vector that results from moving an infinitesimal distance along $X$, then $Y$, then $-X$, then $-Y$.

Let's compute the action of a Lie bracket on a specific function. Consider two [vector fields](@entry_id:161384) on $\mathbb{R}^3$, $X = z \sin(y) \partial_x + x \cos(z) \partial_y - y \sin(x) \partial_z$ and $Y = y e^z \partial_x - z e^x \partial_y + x e^y \partial_z$, acting on the function $f(x, y, z) = x^2 + y^2 + z^2$. First, we compute the action of each vector field on $f$:
$$ Y(f) = (y e^z)(2x) - (z e^x)(2y) + (x e^y)(2z) = 2xy e^z - 2yz e^x + 2xz e^y $$
$$ X(f) = (z \sin y)(2x) + (x \cos z)(2y) - (y \sin x)(2z) = 2xz \sin y + 2xy \cos z - 2yz \sin x $$
Next, we apply the other operator to each of these results. This requires computing the [partial derivatives](@entry_id:146280) of $Y(f)$ and $X(f)$ and then applying the operators $X$ and $Y$, respectively. While tedious, the process is straightforward. Evaluating all terms at the point $p = (0, \frac{\pi}{2}, 0)$, one finds that $X(Y(f))$ evaluates to $0$ and $Y(X(f))$ evaluates to $\frac{\pi^2}{2}$. Therefore:
$$ [X, Y](f)\Big|_p = X(Y(f))\Big|_p - Y(X(f))\Big|_p = 0 - \frac{\pi^2}{2} = -\frac{\pi^2}{2} $$
This shows how the Lie bracket of vector fields produces a numerical value when applied to a function and evaluated at a point. [@problem_id:647201]

One can also compute the components of the resulting vector field $[X, Y]$ directly. If $X = \sum_i X^i \partial_i$ and $Y = \sum_j Y^j \partial_j$, then their bracket $W=[X,Y]$ has components $W^k$ given by:
$$ W^k = \sum_i (X^i \frac{\partial Y^k}{\partial x^i} - Y^i \frac{\partial X^k}{\partial x^i}) = X(Y^k) - Y(X^k) $$
Let's apply this to $V_1 = y^2 \partial_x + z^2 \partial_y + x^2 \partial_z$ and $V_2 = y \partial_x + z \partial_y + x \partial_z$. The $x$-component of $W=[V_1, V_2]$ is:
$$ W_x = V_1(V_{2,x}) - V_2(V_{1,x}) = V_1(y) - V_2(y^2) $$
$$ = (y^2 \partial_x y + z^2 \partial_y y + x^2 \partial_z y) - (y \partial_x y^2 + z \partial_y y^2 + x \partial_z y^2) = (z^2) - (z(2y)) = z^2 - 2yz $$
Similarly, we find $W_y = x^2 - 2xz$ and $W_z = y^2 - 2xy$. Thus, the resulting vector field is $W = (z^2-2yz)\partial_x + (x^2-2xz)\partial_y + (y^2-2xy)\partial_z$. It is interesting to note that the divergence of this particular field is zero: $\nabla \cdot W = \frac{\partial W_x}{\partial x} + \frac{\partial W_y}{\partial y} + \frac{\partial W_z}{\partial z} = 0+0+0=0$. [@problem_id:647367]

This concept generalizes to the **Lie derivative**, $L_V$, which measures the change of any geometric object (functions, vector fields, [differential forms](@entry_id:146747)) along the [flow of a vector field](@entry_id:180235) $V$. For a vector field $W$, the Lie derivative is precisely the Lie bracket: $L_V W = [V, W]$. For a differential form $\omega$, the change is given by Cartan's "magic" formula:
$$ L_V \omega = d(i_V \omega) + i_V(d\omega) $$
Here $d$ is the [exterior derivative](@entry_id:161900) and $i_V$ is the [interior product](@entry_id:158127). This powerful formula provides a practical method for computing the Lie derivative of forms, connecting the Lie bracket concept to the broader machinery of [exterior calculus](@entry_id:188487). [@problem_id:647241]

### The Adjoint Representation

The Lie bracket itself can be used to construct a representation of a Lie algebra, known as the **[adjoint representation](@entry_id:146773)**. For any element $X$ in a Lie algebra $\mathfrak{g}$, we define a [linear map](@entry_id:201112) $\text{ad}_X: \mathfrak{g} \to \mathfrak{g}$ by its action on any other element $Y \in \mathfrak{g}$:

$$
\text{ad}_X(Y) = [X, Y]
$$

The map $X \mapsto \text{ad}_X$ sends elements of the Lie algebra $\mathfrak{g}$ to [linear operators](@entry_id:149003) on $\mathfrak{g}$ itself (i.e., elements of $\mathfrak{gl}(\mathfrak{g})$). This map is a Lie algebra homomorphism, meaning it preserves the bracket structure:
$$
\text{ad}_{[X, Y]} = [\text{ad}_X, \text{ad}_Y]
$$
where the bracket on the right is the commutator of operators, $(\text{ad}_X \circ \text{ad}_Y - \text{ad}_Y \circ \text{ad}_X)$. This crucial identity is, in fact, just a restatement of the Jacobi identity.

Let's explore this with the algebra $\mathfrak{sl}(2, \mathbb{C})$, with its standard basis $\{e, f, h\}$ satisfying $[h, e] = 2e$, $[h, f] = -2f$, and $[e, f] = h$. Suppose we want to analyze the operator $L = [\text{ad}_X, \text{ad}_Y]$ for $X = e+f$ and $Y=h$. Instead of computing the action of $\text{ad}_X$ and $\text{ad}_Y$ separately and then their commutator, we can use the homomorphism property:
$$
L = \text{ad}_{[X, Y]}
$$
First, we compute the bracket $Z = [X, Y]$:
$$
Z = [e+f, h] = [e, h] + [f, h] = -[h, e] - [h, f] = -2e - (-2f) = -2e + 2f
$$
So, $L = \text{ad}_{-2e+2f}$. Now, to find the [matrix representation](@entry_id:143451) of this operator, we see how it acts on the basis vectors $\{e, f, h\}$:
$$ L(e) = [-2e+2f, e] = 2[f, e] = -2[e, f] = -2h $$
$$ L(f) = [-2e+2f, f] = -2[e, f] = -2h $$
$$ L(h) = [-2e+2f, h] = -2[e, h] + 2[f, h] = -2(-2e) + 2(2f) = 4e + 4f $$
Writing these results in the ordered basis $\{e, f, h\}$, we get the coordinate vectors $(0, 0, -2)^T$, $(0, 0, -2)^T$, and $(4, 4, 0)^T$. These form the columns of the matrix representation $M_L$:
$$
M_L = \begin{pmatrix} 0 & 0 & 4 \\ 0 & 0 & 4 \\ -2 & -2 & 0 \end{pmatrix}
$$
From here, one can analyze this matrix further. For example, its square is:
$$
M_L^2 = \begin{pmatrix} 0 & 0 & 4 \\ 0 & 0 & 4 \\ -2 & -2 & 0 \end{pmatrix} \begin{pmatrix} 0 & 0 & 4 \\ 0 & 0 & 4 \\ -2 & -2 & 0 \end{pmatrix} = \begin{pmatrix} -8 & -8 & 0 \\ -8 & -8 & 0 \\ 0 & 0 & -16 \end{pmatrix}
$$
The trace of this matrix is $\text{Tr}(M_L^2) = -8 - 8 - 16 = -32$. This example shows how the abstract properties of the [adjoint representation](@entry_id:146773) can greatly simplify calculations that would otherwise be much more cumbersome. [@problem_id:647240]