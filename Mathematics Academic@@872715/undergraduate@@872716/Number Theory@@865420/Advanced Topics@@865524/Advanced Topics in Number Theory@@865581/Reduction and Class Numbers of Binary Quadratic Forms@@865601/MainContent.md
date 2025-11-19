## Introduction
The study of [binary quadratic forms](@entry_id:200380), expressions of the form $ax^2 + bxy + cy^2$, lies at the very heart of number theory, connecting elementary questions about integers to the profound structures of [modern algebra](@entry_id:171265). Pioneered by Lagrange and brought to a stunning level of completion by Gauss, this theory addresses a fundamental problem: how can we classify the infinite set of such forms into a finite, understandable structure? The key lies in grouping forms that are arithmetically "the same"—those that represent the same set of integers. The concept of the class number, which counts these distinct families of forms, emerges as a central invariant, measuring the complexity of this classification.

This article will guide you through this classical yet vibrant area of mathematics. You will learn the principles that underpin the classification, the algorithms that make it computable, and the deep connections it has to other mathematical fields.
- **Chapter 1, "Principles and Mechanisms,"** will introduce the foundational concepts of [discriminant](@entry_id:152620), equivalence, and primitivity. We will develop Gauss's elegant reduction algorithm for [positive definite forms](@entry_id:191092), which provides the essential tool for finding canonical representatives and computing the [class number](@entry_id:156164).
- **Chapter 2, "Applications and Interdisciplinary Connections,"** will explore the power of this theory. We will see how it helps solve the age-old problem of representing integers by forms and delve into the rich algebraic structure of the class group, including Gauss composition and [genus theory](@entry_id:192075). This chapter also illuminates the crucial link between [quadratic forms](@entry_id:154578) and the ideal [class groups](@entry_id:182524) of [quadratic number fields](@entry_id:191911).
- **Chapter 3, "Hands-On Practices,"** will provide an opportunity to apply these concepts through guided problems, solidifying your understanding by computing discriminants, finding reduced forms, and exploring the nuances of the theory.

By the end of this exploration, you will have a comprehensive understanding of how to reduce and classify [binary quadratic forms](@entry_id:200380) and an appreciation for their central role in number theory.

## Principles and Mechanisms

This chapter delves into the foundational principles and mechanisms governing the theory of [binary quadratic forms](@entry_id:200380). We will formalize the classification of these forms, explore the concept of equivalence that partitions them into classes, and develop the elegant reduction algorithm of Gauss for identifying a canonical representative within each class. This framework allows us to define and compute the [class number](@entry_id:156164), a crucial invariant that measures the complexity of this classification.

### Fundamental Concepts of Binary Quadratic Forms

A **binary quadratic form** is a [homogeneous polynomial](@entry_id:178156) of degree two in two variables, expressed as
$$
Q(x,y) = ax^2 + bxy + cy^2
$$
where the coefficients $a$, $b$, and $c$ are integers. Throughout our discussion, we will deal exclusively with such **integral forms**.

A central invariant associated with any binary [quadratic form](@entry_id:153497) is its **discriminant**, defined as:
$$
D = b^2 - 4ac
$$
The [discriminant](@entry_id:152620) is not merely a computational artifact; its sign provides a fundamental classification of the form's behavior over the real numbers [@problem_id:3089557]. To see this, we can complete the square (assuming $a \neq 0$):
$$
Q(x,y) = a\left(x + \frac{b}{2a}y\right)^2 + \left(c - \frac{b^2}{4a}\right)y^2 = \frac{1}{4a}\left( (2ax+by)^2 - (b^2-4ac)y^2 \right) = \frac{1}{4a}\left( (2ax+by)^2 - Dy^2 \right)
$$
This reformulation reveals three distinct cases based on the sign of $D$:

1.  **Definite Forms ($D  0$):** If the discriminant is negative, $-D$ is positive. The expression $(2ax+by)^2 - Dy^2$ becomes a [sum of two squares](@entry_id:634766) (multiplied by non-negative constants), which is zero only if $y=0$ and $2ax+by=0$, implying $x=y=0$. Thus, for any non-zero integer pair $(x,y)$, the form $Q(x,y)$ maintains a constant sign, determined by the sign of $a$.
    *   If $a > 0$, the form is **positive definite**, meaning $Q(x,y) > 0$ for all $(x,y) \neq (0,0)$. For example, $Q_1(x,y) = x^2+xy+y^2$ has $D=-3$ and is [positive definite](@entry_id:149459) [@problem_id:3089557].
    *   If $a  0$, the form is **[negative definite](@entry_id:154306)**, meaning $Q(x,y)  0$ for all $(x,y) \neq (0,0)$.

2.  **Indefinite Forms ($D > 0$):** If the discriminant is positive, the expression $(2ax+by)^2 - Dy^2$ can take both positive and negative values. For instance, one can choose integer pairs $(x,y)$ that make the term positive or negative. Such forms are called **indefinite**. The form $Q_2(x,y)=x^2-3xy+y^2$, with discriminant $D=5$, is an example of an [indefinite form](@entry_id:150990) [@problem_id:3089557].

3.  **Degenerate Forms ($D = 0$):** If the [discriminant](@entry_id:152620) is zero, the form simplifies to $Q(x,y) = \frac{1}{4a}(2ax+by)^2$. This form can be zero for non-zero pairs $(x,y)$ that lie on the line $2ax+by=0$. Such forms are called **degenerate**. For instance, $Q_3(x,y)=x^2+2xy+y^2=(x+y)^2$ has $D=0$ and is degenerate [@problem_id:3089557].

Another crucial property is **primitivity**. A form $Q(x,y)$ is called **primitive** if its coefficients are coprime, that is, $\gcd(a,b,c)=1$. If $\gcd(a,b,c)=d > 1$, the form is called **imprimitive**, and it can be written as $Q(x,y) = d \cdot Q'(x,y)$, where $Q'(x,y)$ is a primitive form. The integer $d$ is known as the **content** of the form $Q$ [@problem_id:3089518].

### Equivalence of Forms: The Group Action

The theory of [quadratic forms](@entry_id:154578) seeks to classify them into families with shared arithmetic properties. The fundamental tool for this classification is the concept of equivalence, defined through a group action on the set of forms.

Consider a linear change of variables:
$$
\begin{pmatrix} x' \\ y' \end{pmatrix} = M \begin{pmatrix} x \\ y \end{pmatrix} = \begin{pmatrix} p  q \\ r  s \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix}
$$
where the matrix $M$ has integer entries. We are interested in transformations that are invertible over the integers, which means that the inverse matrix $M^{-1}$ also has integer entries. This occurs precisely when the determinant of $M$ is $\pm 1$. The set of such matrices forms the **[general linear group](@entry_id:141275) over $\mathbb{Z}$**, denoted $\mathbf{GL_2(\mathbb{Z})}$.

A change of variables transforms a form $Q(x,y)$ into a new form $Q'(x,y) = Q(px+qy, rx+sy)$. By direct substitution, the new coefficients $(a', b', c')$ are found to be [@problem_id:3089549]:
$$
\begin{align*}
a' = ap^2 + bpr + cr^2 \\
b' = 2apq + b(ps+qr) + 2crs \\
c' = aq^2 + bqs + cs^2
\end{align*}
$$
A more compact way to see this relationship is to represent the form $Q(x,y)$ using a symmetric matrix $A = \begin{pmatrix} a  b/2 \\ b/2  c \end{pmatrix}$, such that $Q(x,y) = \mathbf{v}^T A \mathbf{v}$ where $\mathbf{v} = \begin{pmatrix} x \\ y \end{pmatrix}$. The [transformation of variables](@entry_id:185742) is $\mathbf{v} \mapsto M\mathbf{v}$. The new form is $Q'( \mathbf{v} ) = (M\mathbf{v})^T A (M\mathbf{v}) = \mathbf{v}^T (M^T A M) \mathbf{v}$. The matrix of the new form is therefore $A' = M^T A M$.

From this matrix formulation, we can elegantly prove the [invariance of the discriminant](@entry_id:170103). The [discriminant](@entry_id:152620) is related to the determinant of $A$ by $D = -4 \det(A)$. The new [discriminant](@entry_id:152620) is $D' = -4 \det(A') = -4 \det(M^T A M) = -4 \det(M^T)\det(A)\det(M) = -4 (\det M)^2 \det(A)$. Since $M \in \mathbf{GL_2(\mathbb{Z})}$, we have $\det(M) = \pm 1$, so $(\det M)^2 = 1$. It follows that $D' = D$. The discriminant is invariant under any invertible integer change of variables [@problem_id:3089549]. The content, $\gcd(a,b,c)$, is also an invariant, meaning an imprimitive form cannot be transformed into a primitive one [@problem_id:3089518].

We define two forms $Q$ and $Q'$ to be **equivalent** if they are related by a transformation in $\mathbf{GL_2(\mathbb{Z})}$. A more refined concept is **[proper equivalence](@entry_id:635057)**, where the [transformation matrix](@entry_id:151616) is restricted to the **[special linear group](@entry_id:139538)**, $\mathbf{SL_2(\mathbb{Z})}$, which consists of matrices in $\mathbf{GL_2(\mathbb{Z})}$ with determinant $+1$ [@problem_id:3089495]. An equivalence class under this more restrictive relation is called a **proper class**. Unless stated otherwise, "class" will refer to a proper class.

The study of [equivalence classes](@entry_id:156032) is arithmetically significant because equivalent forms represent the same set of integers. A form $Q$ is said to **represent an integer $n$** if there exist integers $x_0, y_0$ such that $Q(x_0, y_0) = n$. If $Q'$ is equivalent to $Q$ via a matrix $M$, say $Q'(x',y') = Q(x,y)$ where $\begin{pmatrix}x\\y\end{pmatrix}=M\begin{pmatrix}x'\\y'\end{pmatrix}$, then the invertibility of $M$ over the integers establishes a [one-to-one correspondence](@entry_id:143935) between the integer pairs $(x,y)$ and $(x',y')$. Consequently, if $Q$ represents $n$, so does $Q'$, and vice versa. All forms within an equivalence class represent exactly the same set of integers [@problem_id:3089553].

### Reduction of Positive Definite Forms

The concept of equivalence partitions the infinite set of forms of a given discriminant into a number of disjoint (and also infinite) equivalence classes. To study these classes, it is invaluable to find a unique, canonical representative for each one. For [positive definite forms](@entry_id:191092) ($D  0$), this is achieved through **Gauss reduction**.

A primitive [positive definite form](@entry_id:152124) $Q(x,y) = ax^2 + bxy + cy^2$ is said to be **reduced** if its coefficients satisfy the inequalities
$$
|b| \le a \le c
$$
with an additional tie-breaking rule to ensure uniqueness: if $|b|=a$ or if $a=c$, then we require $b \ge 0$ [@problem_id:3010138].

The power of this definition lies in two fundamental results. First, the number of reduced forms for any given negative discriminant is finite. Second, every primitive [positive definite form](@entry_id:152124) is properly equivalent to exactly one of these reduced forms.

The finiteness proof is a cornerstone of the theory [@problem_id:3083533]. From the reduction inequalities and the discriminant equation, we can derive a powerful constraint on the coefficient $a$. Since $a \le c$, we have $4a^2 \le 4ac$. The discriminant equation is $D = b^2 - 4ac$, which for $D  0$ we write as $|D| = 4ac - b^2$. Combining these, we get:
$$
|D| = 4ac - b^2 \ge 4a^2 - b^2
$$
The condition $|b| \le a$ implies $b^2 \le a^2$. Therefore,
$$
|D| \ge 4a^2 - a^2 = 3a^2
$$
This yields a crucial upper bound on the first coefficient of any reduced form:
$$
a \le \sqrt{\frac{|D|}{3}}
$$
Since $a$ must be a positive integer, there is only a finite number of possibilities for $a$. For each such $a$, the condition $|b| \le a$ limits $b$ to a [finite set](@entry_id:152247) of integer values. Finally, for each pair $(a,b)$, the coefficient $c$ is fixed by the discriminant equation: $c = \frac{b^2-D}{4a}$. We only need to check if this $c$ is an integer and if it satisfies $c \ge a$. This procedure generates all possible reduced forms for a given [discriminant](@entry_id:152620) $D$, and the bounds on $a$ and $b$ guarantee that this is a finite list [@problem_id:3010138] [@problem_id:3083533].

The second result is that this [finite set](@entry_id:152247) of reduced forms perfectly represents the equivalence classes.
**The Fundamental Theorem of Reduction for Positive Definite Forms:** Every [proper equivalence](@entry_id:635057) class of primitive [positive definite forms](@entry_id:191092) of discriminant $D  0$ contains exactly one reduced form [@problem_id:3010138] [@problem_id:3089499].
This theorem is profound. It establishes a canonical, finite set of representatives for the [equivalence classes](@entry_id:156032), transforming an abstract classification problem into a concrete computational one. It is important to note that the conditions for a reduced form are not arbitrary; they are precisely what is needed to guarantee a unique representative. For example, relaxing the conditions might allow multiple "simple" forms in one class, while tightening them might leave some classes with no representative at all.

### The Class Number and Its Computation

The insights from reduction theory lead directly to one of the most important concepts in the field.

The **[class number](@entry_id:156164)** of discriminant $D$, denoted $\mathbf{h(D)}$, is defined as the number of proper equivalence classes of primitive [binary quadratic forms](@entry_id:200380) of that [discriminant](@entry_id:152620) [@problem_id:3089495].

For negative discriminants, the Fundamental Theorem of Reduction provides a direct method for computing $h(D)$. Since there is a one-to-one correspondence between proper [equivalence classes](@entry_id:156032) and reduced forms, the [class number](@entry_id:156164) is simply the number of reduced primitive [positive definite forms](@entry_id:191092) of discriminant $D$.

Let's illustrate this with a complete example for the [discriminant](@entry_id:152620) $D=-23$ [@problem_id:3089518]. We seek all primitive integer triples $(a,b,c)$ with $b^2-4ac = -23$ that satisfy the reduction conditions $|b| \le a \le c$ and $a>0$.

1.  **Bound the coefficient $a$**: We have $a \le \sqrt{|-23|/3} \approx \sqrt{7.66...}$. Since $a$ is a positive integer, the possible values are $a=1$ and $a=2$.

2.  **Case $a=1$**: The condition $|b| \le a$ implies $b \in \{-1, 0, 1\}$. We use $4ac = b^2-D$, which is $4c = b^2+23$.
    *   If $b=0$, $4c = 23$, which gives no integer solution for $c$.
    *   If $b=1$, $4c = 1^2+23 = 24$, so $c=6$. We have the form $(1,1,6)$. Let's check the reduction conditions: $|1| \le 1 \le 6$. This holds. Since $|b|=a$, we must check the tie-breaker: $b \ge 0$. Since $b=1$, this is satisfied. The form $x^2+xy+6y^2$ is reduced. It is primitive as $\gcd(1,1,6)=1$.
    *   If $b=-1$, $4c = (-1)^2+23 = 24$, so $c=6$. This gives the form $(1,-1,6)$. Here, $|-1| \le 1 \le 6$ holds. However, since $|b|=a$, the tie-breaker $b \ge 0$ is violated. This form is not reduced.

3.  **Case $a=2$**: The condition $|b| \le a$ implies $b \in \{-2, -1, 0, 1, 2\}$. We use $8c = b^2+23$.
    *   If $b=0$, $8c=23$ (no integer solution).
    *   If $b=1$, $8c = 1^2+23=24$, so $c=3$. We have the form $(2,1,3)$. Let's check: $|1| \le 2 \le 3$. This holds. The tie-breaker conditions do not apply. The form $2x^2+xy+3y^2$ is reduced. It is primitive as $\gcd(2,1,3)=1$.
    *   If $b=-1$, $8c = (-1)^2+23=24$, so $c=3$. We have the form $(2,-1,3)$. Let's check: $|-1| \le 2 \le 3$. This holds. The form $2x^2-xy+3y^2$ is reduced. It is primitive as $\gcd(2,-1,3)=1$.
    *   If $|b|=2$, $8c = 2^2+23=27$ (no integer solution).

In total, we have found exactly three reduced primitive forms of discriminant $D=-23$:
$$
x^2+xy+6y^2, \quad 2x^2+xy+3y^2, \quad 2x^2-xy+3y^2
$$
Therefore, the class number for discriminant $-23$ is $h(-23) = 3$ [@problem_id:3089518].

### Automorphisms of Positive Definite Forms

The **proper automorphism group** of a form $Q$, denoted $\mathbf{Aut^+(Q)}$, is its stabilizer within $\mathbf{SL_2(\mathbb{Z})}$; that is, the set of matrices $M \in \mathbf{SL_2(\mathbb{Z})}$ that leave the form unchanged: $Q(px+qy, rx+sy) = Q(x,y)$ [@problem_id:3089513].

An analysis of the conditions for a matrix $M=\begin{pmatrix}p  q \\ r  s \end{pmatrix}$ to be an automorph reveals a remarkable connection to a Pell-type Diophantine equation. The [matrix coefficients](@entry_id:140901) must satisfy a system of equations that ultimately constrains its trace, $t = p+s$, via the equation:
$$
t^2 - Du^2 = 4
$$
where $u$ is an integer related to the coefficients of the matrix and the form. Since we are considering [positive definite forms](@entry_id:191092), $D  0$, and this becomes $t^2 + |D|u^2 = 4$.

We can analyze the integer solutions $(t,u)$ to this equation to classify the [automorphism](@entry_id:143521) groups [@problem_id:3089513]:
*   **The General Case ($D  -4$):** If $|D| > 4$, then for any non-zero integer $u$, $|D|u^2 > 4$. The only possibility is $u=0$. This gives $t^2=4$, so $t = \pm 2$. These two solutions correspond to the matrices $M = I_2$ (the identity) and $M = -I_2$. Thus, for most discriminants, the [automorphism group](@entry_id:139672) of any primitive form is the cyclic group of order 2, $\operatorname{Aut}^+(Q) = \{\pm I_2\}$.

*   **The Special Case ($D = -4$):** The equation becomes $t^2+4u^2=4$. The integer solutions for $(t,u)$ are $(\pm 2, 0)$ and $(0, \pm 1)$. There are four solutions in total, so the order of the automorphism group is 4. The unique class of primitive forms for $D=-4$ is represented by $Q(x,y)=x^2+y^2$. Its [automorphism group](@entry_id:139672) is cyclic of order 4, generated by the matrix $S = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}$, which corresponds to a 90-degree rotation of the square lattice $\mathbb{Z}^2$.

*   **The Special Case ($D = -3$):** The equation becomes $t^2+3u^2=4$. The integer solutions for $(t,u)$ are $(\pm 2, 0)$ and $(\pm 1, \pm 1)$. There are six solutions, so the order of the automorphism group is 6. The unique class for $D=-3$ is represented by $Q(x,y)=x^2+xy+y^2$. Its automorphism group is cyclic of order 6. This form's [level sets](@entry_id:151155) are ellipses whose geometry is governed by the hexagonal lattice, and the [automorphisms](@entry_id:155390) correspond to the six rotational symmetries of a regular hexagon.

Note that for any integral binary [quadratic form](@entry_id:153497), the matrix $-I_2$ is always an automorph, since $Q(-x, -y) = a(-x)^2 + b(-x)(-y) + c(-y)^2 = Q(x,y)$, and $\det(-I_2) = 1$ [@problem_id:3089513].

### Connection to Quadratic Fields

The theory of [binary quadratic forms](@entry_id:200380) does not exist in isolation. It is deeply and beautifully connected to the arithmetic of **[quadratic number fields](@entry_id:191911)**. This connection, one of the crowning achievements of 19th-century number theory, provides a more profound understanding of the class number and the structure of equivalence classes.

For any non-square [discriminant](@entry_id:152620) $D$, there exists a unique **quadratic order** $\mathcal{O}_D$ of [discriminant](@entry_id:152620) $D$ within the [quadratic field](@entry_id:636261) $\mathbb{Q}(\sqrt{D})$. This order is a subring of the field that is also a free $\mathbb{Z}$-module of rank 2. The most important case is when $D$ is a **fundamental discriminant**, in which case $\mathcal{O}_D$ is the full [ring of integers](@entry_id:155711) of $\mathbb{Q}(\sqrt{D})$.

The crucial result is a canonical bijection between the set of proper [equivalence classes](@entry_id:156032) of primitive [binary quadratic forms](@entry_id:200380) of discriminant $D$ and the **ideal class group** of the order $\mathcal{O}_D$ [@problem_id:3010138]. This [bijection](@entry_id:138092) can be described explicitly [@problem_id:3089558]:

To a primitive form $Q(x,y) = ax^2 + bxy + cy^2$ of [discriminant](@entry_id:152620) $D$, one associates the $\mathbb{Z}$-module
$$
I_Q = a\mathbb{Z} + \frac{-b+\sqrt{D}}{2}\mathbb{Z} = \text{span}_{\mathbb{Z}}\left\{a, \frac{-b+\sqrt{D}}{2}\right\}
$$
One can show that this module $I_Q$ is a proper (i.e., invertible) ideal of the order $\mathcal{O}_D$. The mapping $Q \mapsto I_Q$ has the following properties:
1.  Properly equivalent forms map to ideals in the same ideal class.
2.  The map induces a [bijection](@entry_id:138092) between the set of proper classes of forms and the set of ideal classes of $\mathcal{O}_D$.
3.  The norm of the ideal $I_Q$ is equal to the first coefficient, $a$.

This correspondence implies that the [class number](@entry_id:156164) $h(D)$ of [quadratic forms](@entry_id:154578) is precisely the same as the class number of the order $\mathcal{O}_D$, which is the size of its ideal class group. This reframes the study of [quadratic forms](@entry_id:154578) in the powerful language of modern [algebraic number](@entry_id:156710) theory, where tools like [ideal theory](@entry_id:184127) and [class field theory](@entry_id:155687) can be brought to bear.