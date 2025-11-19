## Introduction
In the study of [vector algebra](@entry_id:152340), combining vectors through operations like the dot and cross product unlocks the ability to describe the geometric and physical properties of our three-dimensional world. While single operations are foundational, the combination of these operations reveals deeper structural relationships. The **vector [triple product](@entry_id:195882)**, an expression involving three vectors and two cross products, stands out as a particularly powerful and elegant concept. Its mastery is essential for students and professionals in physics, engineering, and computer science, as it simplifies complex vector expressions and provides profound physical insight.

This article addresses the challenge of understanding and applying expressions involving repeated cross products, a common point of confusion that stems from the non-intuitive, non-associative nature of the cross product. We will demystify this operation by focusing on its primary algebraic tool, the "BAC-CAB" identity.

Across the following chapters, you will build a comprehensive understanding of the vector [triple product](@entry_id:195882). We will begin by exploring its fundamental principles and geometric meaning in **"Principles and Mechanisms."** Next, **"Applications and Interdisciplinary Connections"** will showcase its utility in solving real-world problems in mechanics, electromagnetism, and [computer graphics](@entry_id:148077). Finally, **"Hands-On Practices"** will allow you to solidify your knowledge by working through guided problems. Let's begin by dissecting the core algebraic identity that governs this powerful vector operation.

## Principles and Mechanisms

Having established the fundamental operations of vector algebra—addition, scalar multiplication, the scalar (dot) product, and the vector (cross) product—we now turn our attention to combined operations that reveal deeper structural properties of three-dimensional space. Among the most important of these is the **vector [triple product](@entry_id:195882)**, an operation that combines three vectors using two cross products. Its algebraic properties and geometric interpretations are not only elegant but also indispensable in fields ranging from classical mechanics and electromagnetism to [computer graphics](@entry_id:148077) and [tensor analysis](@entry_id:184019).

### The BAC-CAB Identity: Definition and Geometric Meaning

The vector [triple product](@entry_id:195882) involves three vectors, say $\vec{a}$, $\vec{b}$, and $\vec{c}$, combined as $\vec{a} \times (\vec{b} \times \vec{c})$. It is crucial to recognize that the parentheses are not optional; the order of operations matters profoundly. The expression is evaluated by first computing the cross product of $\vec{b}$ and $\vec{c}$, which results in a new vector, let's call it $\vec{d} = \vec{b} \times \vec{c}$. Then, the [cross product](@entry_id:156749) of $\vec{a}$ with this intermediate vector $\vec{d}$ is taken.

The primary utility of the vector [triple product](@entry_id:195882) stems from a remarkable identity that allows it to be expressed entirely in terms of dot products and [scalar multiplication](@entry_id:155971). This identity is often remembered by the mnemonic "BAC-CAB" and is stated as follows:

$$
\vec{a} \times (\vec{b} \times \vec{c}) = \vec{b}(\vec{a} \cdot \vec{c}) - \vec{c}(\vec{a} \cdot \vec{b})
$$

Here, $(\vec{a} \cdot \vec{c})$ and $(\vec{a} \cdot \vec{b})$ are scalar quantities that scale the vectors $\vec{b}$ and $\vec{c}$, respectively. This identity, also known as **Lagrange's formula**, is the cornerstone for understanding the vector [triple product](@entry_id:195882).

Let's dissect the geometric implications of the BAC-CAB rule.

First, the resulting vector, let's call it $\vec{v} = \vec{a} \times (\vec{b} \times \vec{c})$, is a **linear combination** of the vectors $\vec{b}$ and $\vec{c}$. This means that $\vec{v}$ must lie in the plane spanned by $\vec{b}$ and $\vec{c}$ (assuming $\vec{b}$ and $\vec{c}$ are not collinear). This is a powerful geometric constraint. For instance, if a vector $\vec{d}$ is defined as $\vec{d} = \vec{a} \times (\vec{b} \times \vec{c})$, we can immediately express it as $\vec{d} = \alpha \vec{b} + \beta \vec{c}$. By comparing this with the BAC-CAB identity, we can directly identify the scalar coefficients as $\alpha = (\vec{a} \cdot \vec{c})$ and $\beta = -(\vec{a} \cdot \vec{b})$ [@problem_id:2175583] [@problem_id:2175545].

Second, from the definition of the cross product, the vector $\vec{v} = \vec{a} \times (\vec{b} \times \vec{c})$ must be **orthogonal to** $\vec{a}$. This provides a useful check for calculations and another key geometric insight [@problem_id:2175555].

The BAC-CAB rule also allows us to determine the conditions under which the vector [triple product](@entry_id:195882) vanishes. For $\vec{a} \times (\vec{b} \times \vec{c})$ to be the [zero vector](@entry_id:156189) (assuming non-zero vectors), we must have $\vec{b}(\vec{a} \cdot \vec{c}) - \vec{c}(\vec{a} \cdot \vec{b}) = \vec{0}$. This can occur under two primary conditions [@problem_id:2175546]:
1.  If $\vec{b}$ and $\vec{c}$ are collinear, then their [cross product](@entry_id:156749) $\vec{b} \times \vec{c}$ is the zero vector, making the entire expression zero.
2.  If $\vec{a}$ is orthogonal to the plane of $\vec{b}$ and $\vec{c}$ (i.e., $\vec{a}$ is orthogonal to both $\vec{b}$ and $\vec{c}$), then both dot products $(\vec{a} \cdot \vec{c})$ and $(\vec{a} \cdot \vec{b})$ are zero, which again makes the final vector zero.

### The Non-Associativity of the Cross Product

A common pitfall for students is to assume that the [cross product](@entry_id:156749) is associative like ordinary multiplication. That is, it is tempting to believe that $(\vec{a} \times \vec{b}) \times \vec{c} = \vec{a} \times (\vec{b} \times \vec{c})$. This is fundamentally incorrect.

To see why, we can apply the BAC-CAB rule to the left-hand side. We first use the anticommutative property of the cross product, $\vec{x} \times \vec{y} = -\vec{y} \times \vec{x}$:
$$
(\vec{a} \times \vec{b}) \times \vec{c} = - \vec{c} \times (\vec{a} \times \vec{b})
$$
Now, applying the BAC-CAB rule to this new form gives:
$$
- \vec{c} \times (\vec{a} \times \vec{b}) = - [ \vec{a}(\vec{c} \cdot \vec{b}) - \vec{b}(\vec{c} \cdot \vec{a}) ] = \vec{b}(\vec{a} \cdot \vec{c}) - \vec{a}(\vec{b} \cdot \vec{c})
$$
Comparing the two expressions:
$$
\vec{a} \times (\vec{b} \times \vec{c}) = \vec{b}(\vec{a} \cdot \vec{c}) - \vec{c}(\vec{a} \cdot \vec{b})
$$
$$
(\vec{a} \times \vec{b}) \times \vec{c} = \vec{b}(\vec{a} \cdot \vec{c}) - \vec{a}(\vec{b} \cdot \vec{c})
$$
The difference between the two is generally non-zero [@problem_id:2175575]:
$$
(\vec{a} \times \vec{b}) \times \vec{c} - \vec{a} \times (\vec{b} \times \vec{c}) = \vec{c}(\vec{a} \cdot \vec{b}) - \vec{a}(\vec{b} \cdot \vec{c})
$$
This demonstrates that the cross product is **non-associative**. Geometrically, $\vec{a} \times (\vec{b} \times \vec{c})$ lies in the plane of $\vec{b}$ and $\vec{c}$, while $(\vec{a} \times \vec{b}) \times \vec{c}$ lies in the plane of $\vec{a}$ and $\vec{b}$. These planes are generally different.

However, there are special geometric arrangements where associativity holds. The [associativity](@entry_id:147258) condition $(\vec{a} \times \vec{b}) \times \vec{c} = \vec{a} \times (\vec{b} \times \vec{c})$ is satisfied if and only if the difference vector is zero: $\vec{c}(\vec{a} \cdot \vec{b}) - \vec{a}(\vec{b} \cdot \vec{c}) = \vec{0}$. This equality holds if [@problem_id:1563305]:
-   **$\vec{a}$ and $\vec{c}$ are collinear:** If $\vec{c} = k\vec{a}$ for some scalar $k$, the expression becomes $k\vec{a}(\vec{a} \cdot \vec{b}) - \vec{a}(\vec{b} \cdot k\vec{a}) = k(\vec{a} \cdot \vec{b})\vec{a} - k(\vec{a} \cdot \vec{b})\vec{a} = \vec{0}$.
-   **$\vec{b}$ is orthogonal to both $\vec{a}$ and $\vec{c}$:** If $\vec{a} \cdot \vec{b} = 0$ and $\vec{c} \cdot \vec{b} = 0$, the expression becomes $\vec{c}(0) - \vec{a}(0) = \vec{0}$. This includes the case where all three vectors are mutually orthogonal.
-   One or more of the vectors is the [zero vector](@entry_id:156189), which is a trivial case.

### Fundamental Identities and Applications

Beyond the BAC-CAB rule, the vector [triple product](@entry_id:195882) appears in other fundamental identities and has direct physical applications.

#### The Jacobi Identity

The non-[associativity](@entry_id:147258) of the cross product is captured in a more symmetric and profound relation known as the **Jacobi identity**:
$$
\vec{a} \times (\vec{b} \times \vec{c}) + \vec{b} \times (\vec{c} \times \vec{a}) + \vec{c} \times (\vec{a} \times \vec{b}) = \vec{0}
$$
This identity can be proven by simply expanding each of the three terms using the BAC-CAB rule and observing the cancellation [@problem_id:1563270]:
$$
[\vec{b}(\vec{a} \cdot \vec{c}) - \vec{c}(\vec{a} \cdot \vec{b})] + [\vec{c}(\vec{b} \cdot \vec{a}) - \vec{a}(\vec{b} \cdot \vec{c})] + [\vec{a}(\vec{c} \cdot \vec{b}) - \vec{b}(\vec{c} \cdot \vec{a})] = \vec{0}
$$
All terms cancel in pairs due to the [commutativity](@entry_id:140240) of the dot product (e.g., $\vec{b}(\vec{a} \cdot \vec{c})$ cancels with $-\vec{b}(\vec{c} \cdot \vec{a})$). The Jacobi identity reveals that the [cross product](@entry_id:156749) endows $\mathbb{R}^3$ with the structure of a Lie algebra, a concept of great importance in modern physics and [differential geometry](@entry_id:145818).

#### Applications in Physics and Geometry

The vector [triple product](@entry_id:195882) is not merely an abstract curiosity; it is a practical tool for solving problems.

One powerful application is in **[vector decomposition](@entry_id:156536)**. Suppose we want to decompose a vector $\vec{L}$ into components parallel and perpendicular to a given direction, defined by a [unit vector](@entry_id:150575) $\vec{N}$. The component of $\vec{L}$ parallel to $\vec{N}$ is simply $(\vec{L} \cdot \vec{N})\vec{N}$. The component perpendicular to $\vec{N}$ (i.e., lying in the plane normal to $\vec{N}$) is therefore $\vec{L} - (\vec{L} \cdot \vec{N})\vec{N}$. This very same perpendicular component can be elegantly expressed using a vector [triple product](@entry_id:195882). Consider the expression $\vec{N} \times (\vec{L} \times \vec{N})$. Applying the BAC-CAB rule:
$$
\vec{N} \times (\vec{L} \times \vec{N}) = \vec{L}(\vec{N} \cdot \vec{N}) - \vec{N}(\vec{N} \cdot \vec{L})
$$
Since $\vec{N}$ is a [unit vector](@entry_id:150575), $\vec{N} \cdot \vec{N} = |\vec{N}|^2 = 1$. The expression simplifies to:
$$
\vec{N} \times (\vec{L} \times \vec{N}) = \vec{L} - \vec{N}(\vec{L} \cdot \vec{N})
$$
This confirms that $\vec{N} \times (\vec{L} \times \vec{N})$ is precisely the projection of $\vec{L}$ onto the plane with normal $\vec{N}$. This formulation is widely used in physics and [computer graphics](@entry_id:148077) for reflection and projection calculations [@problem_id:1563287].

In physics, the vector [triple product](@entry_id:195882) naturally arises in the study of motion. For example, consider a charged particle with velocity $\vec{v}$ in a magnetic field $\vec{B}$. The "kinematic turning vector" $\vec{T} = \vec{v} \times (\vec{v} \times \vec{B})$ is related to the centripetal force. Using the BAC-CAB rule, we get [@problem_id:2175574]:
$$
\vec{T} = \vec{v}(\vec{v} \cdot \vec{B}) - \vec{B}(\vec{v} \cdot \vec{v}) = \vec{v}(\vec{v} \cdot \vec{B}) - \vec{B}|\vec{v}|^2
$$
In the common case where the particle's velocity is perpendicular to the magnetic field, $\vec{v} \cdot \vec{B} = 0$, and the expression simplifies dramatically to $\vec{T} = -|\vec{v}|^2 \vec{B}$. This shows the turning vector is directed opposite to the magnetic field and its magnitude is proportional to the square of the speed, which is characteristic of [uniform circular motion](@entry_id:178264).

Finally, we can also derive an expression for the squared magnitude of the vector [triple product](@entry_id:195882) purely in terms of dot products [@problem_id:2175533]. Let $\vec{v} = \vec{a} \times (\vec{b} \times \vec{c}) = \vec{b}(\vec{a} \cdot \vec{c}) - \vec{c}(\vec{a} \cdot \vec{b})$. Then $|\vec{v}|^2 = \vec{v} \cdot \vec{v}$ is:
$$
|\vec{v}|^2 = [\vec{b}(\vec{a} \cdot \vec{c}) - \vec{c}(\vec{a} \cdot \vec{b})] \cdot [\vec{b}(\vec{a} \cdot \vec{c}) - \vec{c}(\vec{a} \cdot \vec{b})]
$$
Expanding this dot product yields Lagrange's identity in another form:
$$
|\vec{a} \times (\vec{b} \times \vec{c})|^2 = (\vec{a}\cdot\vec{c})^{2}(\vec{b}\cdot\vec{b}) + (\vec{a}\cdot\vec{b})^{2}(\vec{c}\cdot\vec{c}) - 2(\vec{a}\cdot\vec{c})(\vec{a}\cdot\vec{b})(\vec{b}\cdot\vec{c})
$$

### A Rigorous Derivation with Index Notation

For a more formal and powerful approach, we can employ index (or tensor) notation. In a Cartesian basis, the $i$-th component of a cross product $\vec{U} \times \vec{V}$ is given by $(\vec{U} \times \vec{V})_i = \sum_{j,k} \epsilon_{ijk} U_j V_k$, where $\epsilon_{ijk}$ is the **Levi-Civita symbol**. The key to simplifying repeated cross products is the "epsilon-delta" identity:
$$
\sum_{k=1}^{3} \epsilon_{ijk} \epsilon_{klm} = \delta_{il}\delta_{jm} - \delta_{im}\delta_{jl}
$$
where $\delta_{ab}$ is the **Kronecker delta**.

Let's derive the BAC-CAB rule using this formalism [@problem_id:1563287]. We seek the $i$-th component of $\vec{a} \times (\vec{b} \times \vec{c})$:
$$
[\vec{a} \times (\vec{b} \times \vec{c})]_i = \sum_{j,k} \epsilon_{ijk} a_j (\vec{b} \times \vec{c})_k
$$
Substitute the expression for $(\vec{b} \times \vec{c})_k = \sum_{l,m} \epsilon_{klm} b_l c_m$:
$$
[\vec{a} \times (\vec{b} \times \vec{c})]_i = \sum_{j,k,l,m} \epsilon_{ijk} a_j (\epsilon_{klm} b_l c_m) = \sum_{j,l,m} \left( \sum_k \epsilon_{ijk} \epsilon_{klm} \right) a_j b_l c_m
$$
Now, apply the [epsilon-delta identity](@entry_id:195224):
$$
= \sum_{j,l,m} (\delta_{il}\delta_{jm} - \delta_{im}\delta_{jl}) a_j b_l c_m
$$
Distribute the sum over the two terms:
$$
= \sum_{j,l,m} \delta_{il}\delta_{jm} a_j b_l c_m - \sum_{j,l,m} \delta_{im}\delta_{jl} a_j b_l c_m
$$
In the first term, the deltas force $l=i$ and $m=j$. In the second, they force $m=i$ and $l=j$. The sums collapse:
$$
= \sum_{j} a_j b_i c_j - \sum_{j} a_j b_j c_i
$$
Rearranging and recognizing the definitions of the dot product ($\vec{x} \cdot \vec{y} = \sum_j x_j y_j$):
$$
= b_i \left( \sum_j a_j c_j \right) - c_i \left( \sum_j a_j b_j \right) = b_i (\vec{a} \cdot \vec{c}) - c_i (\vec{a} \cdot \vec{b})
$$
This is precisely the $i$-th component of the vector $\vec{b}(\vec{a} \cdot \vec{c}) - \vec{c}(\vec{a} \cdot \vec{b})$. This rigorous proof confirms the BAC-CAB identity and illustrates the power of [index notation](@entry_id:191923) for manipulating complex vector expressions.