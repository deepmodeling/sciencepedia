## Introduction
In the [representation theory of finite groups](@entry_id:143275), the [character table](@entry_id:145187) stands as a fundamental tool, encoding deep structural information in a compact matrix. While the [first orthogonality relation](@entry_id:143781) for rows provides powerful insights into the irreducible characters themselves, a complementary principle—the [second orthogonality relation](@entry_id:137603)—governs the columns, offering a distinct and equally potent lens for analyzing the group's [conjugacy classes](@entry_id:143916). This relation addresses the fundamental question of how [conjugacy classes](@entry_id:143916) relate to each other and how their properties are reflected in the character table, moving the focus from the characters as functions to the classes as structural units of the group.

This article unpacks the [second orthogonality relation](@entry_id:137603) in three comprehensive chapters. The first chapter, **Principles and Mechanisms**, will formally state the relation, explore its geometric interpretation, and delve into its algebraic origins within the [group algebra](@entry_id:145139). The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate its practical utility in determining group properties and reveal its connections to fields like Fourier analysis and physical chemistry. Finally, **Hands-On Practices** will provide opportunities to apply these concepts through guided problems. We begin by establishing the formal statement of the [second orthogonality relation](@entry_id:137603) and its immediate consequences.

## Principles and Mechanisms

In the study of [group representations](@entry_id:145425), the [character table](@entry_id:145187) of a [finite group](@entry_id:151756) $G$ serves as a powerful repository of its structural information. While the [first orthogonality relation](@entry_id:143781) illuminates the properties of the rows of this table—treating the [irreducible characters](@entry_id:145398) as [orthonormal functions](@entry_id:184701) on the group—a second, equally profound relation governs the columns. This **[second orthogonality relation](@entry_id:137603)** provides a different lens through which to view the group's structure, focusing on the relationships between its conjugacy classes. This chapter will formally state this relation, explore its geometric interpretation, detail its principal applications, and touch upon its deeper algebraic origins.

### The Second Orthogonality Relation: A Statement and Geometric View

The [character table](@entry_id:145187) of a [finite group](@entry_id:151756) $G$ is a square matrix where rows are indexed by the [irreducible characters](@entry_id:145398) $\chi_i$ and columns are indexed by the [conjugacy classes](@entry_id:143916) $C_j$. The entry $(i, j)$ is the value $\chi_i(g_j)$, where $g_j$ is any representative element from the class $C_j$. The [second orthogonality relation](@entry_id:137603), also known as the column orthogonality relation, is a statement about the inner product of these columns.

Formally, for any two elements $g, h \in G$, the relation is:
$$ \sum_{i=1}^{k} \chi_i(g) \overline{\chi_i(h)} = |C_G(g)| \delta_{g \sim h} $$
Here, the sum is over all $k$ irreducible characters of $G$. The term $C_G(g)$ denotes the **[centralizer](@entry_id:146604)** of $g$ in $G$, which is the subgroup of elements that commute with $g$, $\{x \in G \mid xg = gx\}$. The symbol $\delta_{g \sim h}$ is a generalized Kronecker delta, which equals 1 if $g$ and $h$ are conjugate in $G$ (i.e., they belong to the same conjugacy class) and 0 otherwise.

This single equation elegantly captures two distinct scenarios:

1.  **Orthogonality of Distinct Class Columns ($g$ and $h$ are not conjugate):** If $g$ and $h$ belong to different [conjugacy classes](@entry_id:143916), then $\delta_{g \sim h} = 0$, and the relation simplifies to:
    $$ \sum_{i=1}^{k} \chi_i(g) \overline{\chi_i(h)} = 0 $$
    This means that the column vectors of character values corresponding to different conjugacy classes are orthogonal to each other with respect to the standard Hermitian inner product. For instance, if an element $g$ is not conjugate to its own square $g^2$, a direct application of this principle shows that the [sum of products](@entry_id:165203) of their character values must vanish [@problem_id:1654190].

2.  **Norm of a Class Column ($g$ and $h$ are conjugate):** If $g$ and $h$ are in the same conjugacy class, we can set $h=g$. In this case, $\delta_{g \sim g} = 1$, and the relation becomes:
    $$ \sum_{i=1}^{k} \chi_i(g) \overline{\chi_i(g)} = \sum_{i=1}^{k} |\chi_i(g)|^2 = |C_G(g)| $$
    This states that the squared Euclidean norm of a column vector in the [character table](@entry_id:145187) is equal to the order of the [centralizer](@entry_id:146604) of any element in that column's [conjugacy class](@entry_id:138270). This provides a powerful method for computing [centralizer](@entry_id:146604) sizes directly from the character table [@problem_id:1654210], [@problem_id:1811801]. Recall that the order of the centralizer is related to the size of the [conjugacy class](@entry_id:138270) $|Cl(g)|$ by the [orbit-stabilizer theorem](@entry_id:145230): $|G| = |Cl(g)| \cdot |C_G(g)|$. Thus, the sum can also be written as $|G|/|Cl(g)|$ [@problem_id:1654195].

#### A Geometric Interpretation

The [second orthogonality relation](@entry_id:137603) invites a powerful geometric interpretation. If we consider the $k$ columns of the [character table](@entry_id:145187) as $k$ vectors in the [complex vector space](@entry_id:153448) $\mathbb{C}^k$, this relation tells us that these vectors form an **[orthogonal basis](@entry_id:264024)** for this space.

Let's illustrate this with the symmetric group $S_3$, which has three conjugacy classes $C_1=\{e\}$, $C_2=\{(12), (13), (23)\}$, and $C_3=\{(123), (132)\}$. Its [character table](@entry_id:145187) is:

|             | $C_1$ | $C_2$ | $C_3$ |
| :---------: | :---: | :---: | :---: |
| $\chi_1$    |   1   |   1   |   1   |
| $\chi_2$    |   1   |  -1   |   1   |
| $\chi_3$    |   2   |   0   |  -1   |

The column vectors are $\mathbf{v}_1 = (1, 1, 2)^T$, $\mathbf{v}_2 = (1, -1, 0)^T$, and $\mathbf{v}_3 = (1, 1, -1)^T$. Let's check their orthogonality:
- $\langle \mathbf{v}_1, \mathbf{v}_2 \rangle = 1 \cdot \overline{1} + 1 \cdot \overline{(-1)} + 2 \cdot \overline{0} = 1 - 1 + 0 = 0$.
- $\langle \mathbf{v}_2, \mathbf{v}_3 \rangle = 1 \cdot \overline{1} + (-1) \cdot \overline{1} + 0 \cdot \overline{(-1)} = 1 - 1 + 0 = 0$.
- $\langle \mathbf{v}_1, \mathbf{v}_3 \rangle = 1 \cdot \overline{1} + 1 \cdot \overline{1} + 2 \cdot \overline{(-1)} = 1 + 1 - 2 = 0$.
The columns are indeed orthogonal. Because they are three orthogonal (and thus linearly independent) vectors in $\mathbb{C}^3$, they form an orthogonal basis. This property can be exploited to simplify calculations. For example, to express an arbitrary vector $\mathbf{w} \in \mathbb{C}^3$ as a [linear combination](@entry_id:155091) $\mathbf{w} = \sum \alpha_j \mathbf{v}_j$, one can find the coefficients $\alpha_j$ using projections rather than solving a full system of linear equations: $\alpha_j = \frac{\langle \mathbf{w}, \mathbf{v}_j \rangle}{\langle \mathbf{v}_j, \mathbf{v}_j \rangle}$ [@problem_id:1654168].

#### The Matrix Formulation

A more holistic view combines both [orthogonality relations](@entry_id:145540) using matrix algebra. Let $X$ be the $k \times k$ character table matrix, with entries $X_{ij} = \chi_i(g_j)$. Let $D$ be a [diagonal matrix](@entry_id:637782) with entries $D_{jj} = |Cl(g_j)|$. The [first orthogonality relation](@entry_id:143781) for rows can be written as $X D X^\dagger = |G|I$, where $X^\dagger$ is the [conjugate transpose](@entry_id:147909) of $X$. Since for a [finite group](@entry_id:151756), matrices satisfying such a relation must be invertible, we can multiply by the inverse of $X$ to deduce that $X^\dagger X$ must also be a diagonal matrix. Indeed, the [second orthogonality relation](@entry_id:137603) is precisely the statement that $X^\dagger X$ is a [diagonal matrix](@entry_id:637782) whose entries are the orders of the centralizers [@problem_id:1654195]:
$$ (X^\dagger X)_{jl} = \sum_i \overline{\chi_i(g_j)} \chi_i(g_l) = |C_G(g_j)| \delta_{jl} $$
This matrix perspective shows that the row and column [orthogonality relations](@entry_id:145540) are two sides of the same coin, reflecting the underlying unitary structure of the [character theory](@entry_id:144021).

### Key Applications and Consequences

The [second orthogonality relation](@entry_id:137603) is not merely a theoretical curiosity; it is a workhorse in the practical analysis of groups.

#### Calculating Centralizer Sizes

The most direct application is the calculation of centralizer orders. Given a complete [character table](@entry_id:145187), one can find the order of the centralizer of any element $g$ by simply summing the squares of the magnitudes of the character values in the column corresponding to $g$'s conjugacy class.

For example, for the [dihedral group](@entry_id:143875) $D_4$ of order 8, the column for a rotation $r$ by $90^\circ$ has character values $(1, 1, -1, -1, 0)$. The order of its [centralizer](@entry_id:146604) is therefore:
$$ |C_{D_4}(r)| = |1|^2 + |1|^2 + |-1|^2 + |-1|^2 + |0|^2 = 1 + 1 + 1 + 1 + 0 = 4 $$
This tells us that four elements of $D_4$ commute with the rotation $r$ [@problem_id:1811801].

#### The Identity Column and the Order of the Group

A particularly important case is the column for the identity element, $e$. Since every element of $G$ commutes with the identity, its centralizer is the entire group, $C_G(e) = G$, so $|C_G(e)| = |G|$. The character value of the identity, $\chi_i(e)$, is the dimension of the $i$-th irreducible representation, denoted $d_i$. Applying the [second orthogonality relation](@entry_id:137603) to the identity column yields a celebrated result [@problem_id:1654221]:
$$ \sum_{i=1}^{k} |\chi_i(e)|^2 = \sum_{i=1}^{k} d_i^2 = |G| $$
The sum of the squares of the dimensions of the irreducible representations of a finite group is equal to the order of the group. This provides a fundamental consistency check for any valid character table and connects the representation theory of the group directly to its size.

#### Testing for Conjugacy

The [second orthogonality relation](@entry_id:137603) has profound consequences for the relationship between characters and [conjugacy](@entry_id:151754).
- **Uniqueness of Columns:** Can two different conjugacy classes have the same column of character values? Suppose $g_1$ and $g_2$ are not conjugate, but for some reason we find that $\chi_i(g_1) = \chi_i(g_2)$ for all $i$. The orthogonality for distinct classes would imply $\sum_i \chi_i(g_1)\overline{\chi_i(g_2)} = 0$. Substituting $\chi_i(g_2) = \chi_i(g_1)$, we get $\sum_i |\chi_i(g_1)|^2 = 0$. But we know this sum must equal $|C_G(g_1)|$, which is at least 1 (since $e \in C_G(g_1)$). This contradiction proves our initial assumption was wrong. Therefore, distinct [conjugacy classes](@entry_id:143916) must have distinct columns in the [character table](@entry_id:145187). The columns serve as unique "fingerprints" for the conjugacy classes [@problem_id:1654214].

- **Reality of Characters and Self-Inverse Classes:** What can be deduced if a column in the character table contains only real numbers? If $\chi_i(g)$ is real for all $i$, then $\chi_i(g) = \overline{\chi_i(g)}$. A general property of characters is that $\chi_i(g^{-1}) = \overline{\chi_i(g)}$. Combining these, we find $\chi_i(g) = \chi_i(g^{-1})$ for all $i$. As we just established that columns uniquely identify [conjugacy classes](@entry_id:143916), this implies that $g$ and its inverse $g^{-1}$ must belong to the same [conjugacy class](@entry_id:138270). In other words, $g$ is conjugate to its inverse. Such [conjugacy classes](@entry_id:143916) are called **real** or **self-inverse** classes [@problem_id:1654197].

#### Constructing Character Tables

When constructing a character table from scratch, the [orthogonality relations](@entry_id:145540) are indispensable tools. They provide a system of algebraic constraints that the character values must satisfy. Given partial information about a character table, one can often use the column [orthogonality relations](@entry_id:145540) to deduce the missing entries. For example, knowing the character values for two classes allows one to check their orthogonality, which may reveal relationships between unknown character values. Combined with the norms of the columns (determined by centralizer sizes, which can be found from class sizes via $|C_G(g)| = |G|/|Cl(g)|$), one can often solve for all unknown entries in a "puzzle-like" fashion [@problem_id:1654209].

### Deeper Connections: The Center of the Group Algebra

The [orthogonality relations](@entry_id:145540), while practically useful, are not arbitrary numerical coincidences. They are surface-level manifestations of deep algebraic structures. The [second orthogonality relation](@entry_id:137603), in particular, is intrinsically linked to the structure of the **center of the [group algebra](@entry_id:145139)**, denoted $Z(\mathbb{C}G)$.

The [group algebra](@entry_id:145139) $\mathbb{C}G$ is the vector space of all formal linear combinations of elements of $G$ with complex coefficients. Its center, $Z(\mathbb{C}G)$, consists of elements that commute with every element of $\mathbb{C}G$. This space has two natural and important bases:

1.  **The Class Sum Basis:** For each conjugacy class $K_j$, we can form the **class sum** $C_j = \sum_{g \in K_j} g$. The set of all such class sums, $\{C_j\}$, forms a basis for $Z(\mathbb{C}G)$.

2.  **The Central Idempotent Basis:** Associated with each [irreducible character](@entry_id:145297) $\chi_i$ is a special element $e_i \in Z(\mathbb{C}G)$ called a **central primitive idempotent**. These elements have the property that $e_i e_j = \delta_{ij} e_i$ and $\sum e_i = 1$ (the identity of $\mathbb{C}G$). The set $\{e_i\}$ also forms a basis for $Z(\mathbb{C}G)$.

The change-of-basis formulas between these two bases involve the [character table](@entry_id:145187) itself. Specifically, the coefficients that express the class sums in terms of the idempotents (and vice-versa) are functions of the character values $\chi_i(g_j)$, class sizes, and representation dimensions.

The [second orthogonality relation](@entry_id:137603) can be understood as a consequence of the fact that both of these bases are orthogonal with respect to a natural inner product on the [group algebra](@entry_id:145139) [@problem_id:1654230]. The [change-of-basis matrix](@entry_id:184480) between two orthogonal bases must be a multiple of a unitary matrix. The relations that define this matrix and its inverse are precisely the [second orthogonality relation](@entry_id:137603) and its counterpart, which relates the central idempotents to the class sums. Thus, the orthogonality of character table columns is a direct reflection of the decomposition of the center of the [group algebra](@entry_id:145139) into a [direct sum](@entry_id:156782) of one-dimensional algebras spanned by the central primitive idempotents.