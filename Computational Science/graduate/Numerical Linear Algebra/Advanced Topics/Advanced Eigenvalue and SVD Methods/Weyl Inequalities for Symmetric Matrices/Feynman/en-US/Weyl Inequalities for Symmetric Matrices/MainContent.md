## Introduction
Eigenvalues of symmetric matrices are more than just mathematical abstractions; they represent fundamental properties of physical and computational systems, from the [principal stresses](@entry_id:176761) in a material to the stability of a dynamic network. A crucial question for both theorists and practitioners is: how do these fundamental properties change when a system is perturbed? If we have a system described by matrix $A$ and we add a perturbation $B$, what can we say about the eigenvalues of the new system, $A+B$? While one might naively guess that the eigenvalues simply add up, this intuition quickly breaks down, revealing a more complex and beautiful underlying structure.

This article unravels this mystery by exploring the celebrated Weyl's inequalities. We will embark on a journey that begins with the core geometric principles that govern eigenvalues, then moves to the powerful applications of these principles, and concludes with practical exercises to reinforce the concepts.
- In **Principles and Mechanisms**, we build the theoretical foundation from the ground up, starting with the intuitive Rayleigh quotient landscape and deriving Weyl's inequalities through the profound Courant-Fischer [min-max principle](@entry_id:150229) and the geometry of intersecting subspaces.
- In **Applications and Interdisciplinary Connections**, we demonstrate the far-reaching impact of these inequalities, showing how they provide ironclad guarantees for stability in fields ranging from [numerical analysis](@entry_id:142637) and optimization to data science and computational mechanics.
- In **Hands-On Practices**, we offer a set of targeted problems designed to solidify your understanding by applying the inequalities to concrete examples.

By the end, you will not only understand the formulas but also appreciate the deep geometric intuition that makes Weyl's inequalities a cornerstone of modern linear algebra.

## Principles and Mechanisms

Imagine you are standing on a rolling, hilly landscape. The height of the ground beneath your feet depends on your position. For a symmetric matrix, this landscape has a special name: the **Rayleigh quotient**. If we think of any direction from the origin as a vector $x$, the "height" in that direction is given by the formula $R_A(x) = \frac{x^\top A x}{x^\top x}$. The eigenvalues of the matrix $A$ are the most important features of this landscape. The highest peak corresponds to the largest eigenvalue, $\lambda_1(A)$, and the lowest valley corresponds to the [smallest eigenvalue](@entry_id:177333), $\lambda_n(A)$.

But what about the eigenvalues in between? They aren't just random points; they correspond to other special geometric features. Imagine you've found the direction of the highest peak, the eigenvector $v_1$. Now, if you agree to only walk in directions orthogonal to $v_1$, what is the new highest peak you can find? That new peak is the second eigenvalue, $\lambda_2(A)$. This process of finding extremal values on constrained subspaces gives us a profound way to define and find all the eigenvalues. This is the essence of the **Courant-Fischer [min-max principle](@entry_id:150229)**, a powerful lens through which we can understand the soul of a [symmetric matrix](@entry_id:143130) . It defines the $k$-th eigenvalue, $\lambda_k(A)$, not as a mysterious root of a polynomial, but as the result of a geometric game:

$$
\lambda_k(A) = \max_{\substack{S \subset \mathbb{R}^n \\ \dim(S)=k}} \;\; \min_{\substack{x \in S \\ x \ne 0}} R_A(x)
$$

In plain English, to find the $k$-th eigenvalue, you get to choose any $k$-dimensional subspace $S$. Your opponent then tries to find the direction $x$ within your chosen subspace that makes the Rayleigh quotient $R_A(x)$ as small as possible. Your job is to choose the subspace $S$ so that this minimum value is as large as possible. The value of this game is precisely $\lambda_k(A)$. This principle is the bedrock upon which our entire understanding of eigenvalue perturbations is built.

### When Landscapes Collide

Now, let's ask a simple, fundamental question. If we have the landscape for a matrix $A$ and the landscape for another matrix $B$, what does the landscape for their sum, $A+B$, look like? Since the Rayleigh quotients simply add, $R_{A+B}(x) = R_A(x) + R_B(x)$, the new landscape is just the sum of the heights of the first two. How do the eigenvalues of this new landscape relate to the old ones?

The simplest observation we can make is a powerful one. For any direction $x$, the height contributed by $B$ is trapped between its own lowest valley and highest peak: $\lambda_n(B) \le R_B(x) \le \lambda_1(B)$. This means the new landscape $R_{A+B}(x)$ is just the old landscape $R_A(x)$ lifted up or pushed down by an amount that is itself bounded. This immediately tells us something about the eigenvalues of $A+B$. The $k$-th eigenvalue of the sum must be bounded by the $k$-th eigenvalue of $A$, plus or minus the extreme effects of $B$ :

$$
\lambda_k(A) + \lambda_n(B) \le \lambda_k(A+B) \le \lambda_k(A) + \lambda_1(B)
$$

This is a beautiful, intuitive result. It tells us that adding a matrix $B$ shifts the eigenvalues of $A$ by an amount no smaller than the [smallest eigenvalue](@entry_id:177333) of $B$ and no larger than the largest eigenvalue of $B$. This bound can be exact. If we add a [rank-one matrix](@entry_id:199014) $B=uu^\top$ where $u$ is itself an eigenvector of $A$, say $u=e_k$, then we can precisely shift the $k$-th eigenvalue by $\lambda_1(B)=1$ without changing the values of the Rayleigh quotient in subspaces orthogonal to $e_k$ .

### A Deceptively Simple Trap

The two-sided bound is wonderful, but it only involves the extremal eigenvalues of one of the matrices. What if we want to relate the intermediate eigenvalues of all three matrices? A naive guess might be to simply add them index by index, for instance, $\lambda_k(A+B) \le \lambda_k(A) + \lambda_k(B)$. This seems plausible, but it is fundamentally wrong.

Let's test it with a simple, concrete example . Consider the matrices:
$$
A \;=\; \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}, \qquad B \;=\; \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}
$$
It's easy to find their eigenvalues: $\lambda_1(A)=1, \lambda_2(A)=-1$ and $\lambda_1(B)=1, \lambda_2(B)=-1$. Their sum is $A+B = \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}$, which has eigenvalues $\lambda_1(A+B)=\sqrt{2}$ and $\lambda_2(A+B)=-\sqrt{2}$.

Now, let's check our naive inequality for the second eigenvalue ($k=2$):
$$
\lambda_2(A+B) \le \lambda_2(A) + \lambda_2(B)
$$
Plugging in the numbers gives $-\sqrt{2} \le -1 + (-1)$, which simplifies to $-\sqrt{2} \le -2$. This is false! The gap in this case is $\Delta = \lambda_2(A+B) - (\lambda_2(A) + \lambda_2(B)) = 2-\sqrt{2} > 0$.

Why did this fail? The Courant-Fischer principle gives us the answer. The subspace that "proves" the value of $\lambda_2(A)$ is different from the one that proves the value of $\lambda_2(B)$. We cannot assume that the worst-case scenarios for $A$ and $B$ happen in the same subspaces. The beauty of the landscape analogy breaks down if we only look at the labeled features without considering *where* they are located.

### The Geometric Dance of Subspaces: Weyl's Insight

So how do we fix this? The answer lies not in a simple algebraic tweak, but in a profound geometric insight, first articulated by Hermann Weyl. The correct inequalities involve a fascinating shift in indices. For any [symmetric matrices](@entry_id:156259) $A$ and $B$ with eigenvalues sorted in nonincreasing order, and for any choice of indices $i$ and $j$, we have two fundamental inequalities :

1.  If $i+j-1 \le n$, then $\lambda_{i+j-1}(A+B) \le \lambda_i(A) + \lambda_j(B)$.
2.  If $i+j-n \ge 1$, then $\lambda_{i+j-n}(A+B) \ge \lambda_i(A) + \lambda_j(B)$.

Where do these strange indices like $i+j-1$ and $i+j-n$ come from? They are not arbitrary; they are the direct consequence of the geometry of intersecting subspaces . Let's sketch the argument for the first inequality.

To get an upper bound on the eigenvalues of $A+B$, we use one of the Courant-Fischer formulas. We want to find a special subspace where we know the Rayleigh quotient of $A+B$ is small.
From the definition of $\lambda_i(A)$, we know there is a special subspace $U_A$ of dimension $n-i+1$ where for any vector $x$ inside it, $R_A(x) \le \lambda_i(A)$. Likewise, there is a subspace $U_B$ of dimension $n-j+1$ where for any vector $x$ inside it, $R_B(x) \le \lambda_j(B)$.

If we could find a vector $x$ that lies in *both* subspaces simultaneously, then for that vector we would have $R_{A+B}(x) = R_A(x) + R_B(x) \le \lambda_i(A) + \lambda_j(B)$. Such a vector must exist if the intersection $U_A \cap U_B$ is not empty. This is where a fundamental rule of linear algebra, **Grassmann's dimension formula**, comes into play. It tells us that the dimension of the intersection is at least $\dim(U_A) + \dim(U_B) - n$.

Plugging in the dimensions, we find that $\dim(U_A \cap U_B) \ge (n-i+1) + (n-j+1) - n = n-i-j+2$.
This is exactly the dimension of the subspace needed in the Courant-Fischer characterization for the eigenvalue $\lambda_{i+j-1}(A+B)$! The index shift is not magic; it is the precise number that falls out of the geometry of vector spaces. It guarantees we can find a testing ground where the behavior of $A$ and $B$ can be controlled simultaneously, leading to a [valid inequality](@entry_id:170492).

### A World of Perfect Stability

This entire beautiful structure—the real eigenvalues, the [variational principle](@entry_id:145218), and the elegant Weyl inequalities—is a special property of symmetric (or more generally, Hermitian) matrices. What happens if we try to apply this to a general, nonsymmetric matrix? The whole edifice crumbles .

-   First, the eigenvalues can be complex numbers, so there is no single, natural way to "order" them from largest to smallest.
-   Second, and more fatally, the Rayleigh quotient $R_A(x)$ becomes complex-valued. It no longer represents a simple height landscape. The Courant-Fischer principle, which relies on finding real-valued maxima and minima, no longer applies to the eigenvalues.

The perturbation theory for general matrices is a much wilder story. The **Bauer-Fike theorem** tells us that the eigenvalues of a perturbed matrix $A+E$ lie in disks around the eigenvalues of $A$, but the radius of these disks depends on the "condition number" of $A$'s eigenvectors . If the eigenvectors are nearly parallel (a sign of being "non-normal"), this condition number can be enormous, meaning the eigenvalues can be exquisitely sensitive to tiny perturbations. For a symmetric matrix, the eigenvectors are perfectly orthogonal, the condition number is $1$, and we live in a world of perfect stability, governed by the sharp, index-wise bounds of Weyl.

### Putting Bounds to the Test

Weyl's inequalities are not just an abstract curiosity; they are a practical tool of immense power. Consider a case where we add a dense matrix $E$ to a sparse matrix $T$ . A more general tool like the **Gershgorin circle theorem**, which draws disks around the diagonal entries, might see the [dense matrix](@entry_id:174457) as a huge, unstructured perturbation, leading to a very loose bound on the eigenvalues. In contrast, Weyl's inequality $\lambda_1(T+E) \le \lambda_1(T) + \lambda_1(E)$ uses the Rayleigh quotient to "see" the global structure of $E$. If $E$ is, for instance, a negative semidefinite matrix (like $-b \mathbf{1}\mathbf{1}^\top$), its largest eigenvalue $\lambda_1(E)$ could be zero, meaning the Weyl bound correctly predicts that $E$ does not increase the largest eigenvalue at all, whereas the Gershgorin bound might be off by a large amount.

Weyl's inequalities belong to a family of results concerning eigenvalues of [structured matrices](@entry_id:635736). For example, **Cauchy's interlacing theorem** states that the eigenvalues of a [principal submatrix](@entry_id:201119) interlace the eigenvalues of the original matrix. This can be seen as a special case of Weyl's inequalities, where we view the matrix as a block-diagonal piece plus a perturbation that fills in the missing block . In some cases, the more specific structure exploited by interlacing can provide even tighter bounds than the general Weyl inequalities.

This journey, from the simple picture of a landscape to the geometric dance of intersecting subspaces, reveals the deep unity and beauty inherent in the study of symmetric matrices. Weyl's inequalities are not just formulas to be memorized; they are a testament to the power of geometric intuition in understanding the abstract world of linear algebra.