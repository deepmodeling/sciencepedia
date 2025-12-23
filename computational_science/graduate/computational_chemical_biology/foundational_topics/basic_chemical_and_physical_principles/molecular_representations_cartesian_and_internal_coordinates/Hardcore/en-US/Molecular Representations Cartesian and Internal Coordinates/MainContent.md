## Introduction
In the computational modeling of molecular systems, the description of a molecule's structure is the foundation upon which all theoretical models and simulations are built. The choice of a coordinate system—the language used to define atomic positions—is a critical decision with far-reaching consequences for computational efficiency and physical interpretation. This article addresses the fundamental dichotomy between two primary representations: the absolute, all-encompassing Cartesian coordinates and the relative, shape-focused internal coordinates. While Cartesians are straightforward, they entangle a molecule's intrinsic geometry with its physically irrelevant position and orientation in space, creating challenges for many algorithms.

This article will guide you through the principles and applications of these coordinate systems. In "Principles and Mechanisms," we will delve into the mathematical definitions of Cartesian and internal coordinates, exploring concepts of invariance, degrees of freedom, and the systematic construction of [molecular geometry](@entry_id:137852). Next, "Applications and Interdisciplinary Connections" will demonstrate how this choice impacts the performance of geometry optimization, molecular dynamics, and [vibrational analysis](@entry_id:146266), while also revealing powerful connections to fields like robotics and machine learning. Finally, the "Hands-On Practices" section will allow you to solidify these concepts through practical computational exercises. By the end, you will have a robust understanding of how to effectively represent molecules for computational analysis.

## Principles and Mechanisms

In the study of molecular systems, the choice of coordinate system is a foundational decision that profoundly influences the formulation of theoretical models, the efficiency of computational algorithms, and the interpretation of simulation results. While the absolute positions of atoms in a [laboratory frame](@entry_id:166991) are described most directly by Cartesian coordinates, the chemically and physically relevant properties of a molecule—its energy, shape, and vibrational motions—are intrinsically dependent on its internal geometry. This chapter elucidates the principles and mechanisms governing the two primary coordinate representations, Cartesian and internal, exploring their mathematical definitions, interrelationships, and practical implications.

### Cartesian vs. Internal Coordinates: Defining Molecular Shape

The description of a molecule containing $N$ atoms begins with specifying the location of each atom in three-dimensional Euclidean space. This seemingly simple task opens the door to different levels of abstraction, each with distinct advantages and disadvantages.

#### Cartesian Coordinates: An Absolute Description

The most straightforward representation is the set of **Cartesian coordinates**. For a system of $N$ atoms, we can define a vector $\mathbf{x} \in \mathbb{R}^{3N}$ by concatenating the individual [position vectors](@entry_id:174826) $\mathbf{x}_i \in \mathbb{R}^3$ of each atom $i$:
$$ \mathbf{x} = (\mathbf{x}_1, \mathbf{x}_2, \dots, \mathbf{x}_N)^{\top} $$
This representation is complete and unambiguous. Given $\mathbf{x}$, the position of every atom is known, and all geometric properties can be derived. However, this completeness comes at a cost. A molecule's potential energy, and thus its conformational stability and chemical identity, is independent of where it is in space or how it is oriented. A simple translation of the entire molecule by a vector $\mathbf{t}$ or a rotation by a matrix $\mathbf{R}$ changes the value of $\mathbf{x}$ but has no bearing on the molecule's internal state. Cartesian coordinates are therefore not an **invariant** representation; they conflate the six degrees of freedom associated with [rigid-body motion](@entry_id:265795) (three for translation, three for rotation) with the physically pertinent internal degrees of freedom that define the molecule's shape. As a result, for any non-identity [rigid motion](@entry_id:155339) $g$, the transformed [coordinate vector](@entry_id:153319) $g \cdot \mathbf{x}$ is generally not equal to $\mathbf{x}$ .

#### Internal Coordinates: A Relative and Invariant Description

To isolate the description of [molecular shape](@entry_id:142029) from its overall position and orientation, we introduce **[internal coordinates](@entry_id:169764)**. An internal coordinate system provides a parameterization of the molecule's geometry that is, by construction, invariant under global translations and rotations. These coordinates are functions of the relative positions of atoms.

The most common internal coordinates are **bond lengths**, **bond angles**, and **dihedral (or torsion) angles**. For a non-linear molecule with $N$ atoms, a set of $3N-6$ such coordinates is typically sufficient to uniquely define its shape. A change in any of these coordinates corresponds to a genuine change in the molecule's geometry, such as stretching a bond or twisting a functional group. Because they are defined by relative atomic positions, they remain unchanged when the entire molecule is translated or rotated. This invariance is a crucial property, making internal coordinates the natural language for describing potential energy surfaces, conformational changes, and vibrational dynamics.

This invariance can be formalized. A [rigid-body motion](@entry_id:265795) is an element $g$ of the Special Euclidean group, $\mathrm{SE}(3)$. Such a motion acts on the Cartesian coordinates, transforming $\mathbf{x}$ to $g \cdot \mathbf{x}$. Any internal coordinate, which we can denote generically as $q(\mathbf{x})$, is a function of the Cartesian coordinates. The defining property of an internal coordinate is its invariance under this group action:
$$ q(g \cdot \mathbf{x}) = q(\mathbf{x}) \quad \text{for all } g \in \mathrm{SE}(3) $$
This property is fundamental. For example, when comparing two different molecular conformations, $\mathbf{x}$ and $\mathbf{y}$, we are typically interested in the difference in their shapes, not their absolute positions. A common metric for this is the **Root Mean Square Deviation (RMSD)**, which is calculated after optimally superimposing the two structures to minimize their Cartesian differences . The optimal superposition finds the rotation $\mathbf{R}$ and translation $\mathbf{t}$ that minimize this deviation:
$$ \text{RMSD} = \sqrt{\frac{1}{N}\min_{\mathbf{R} \in \mathrm{SO}(3), \mathbf{t} \in \mathbb{R}^3} \sum_{i=1}^N \left\lVert (\mathbf{R}\mathbf{x}_i+\mathbf{t})-\mathbf{y}_i\right\rVert^2} $$
If the two conformations have the same shape (i.e., they are related by a [rigid motion](@entry_id:155339)), their RMSD is zero. Crucially, two such conformations will have identical sets of internal coordinates. The invariance of [internal coordinates](@entry_id:169764) makes them an ideal basis for defining a molecule's "[shape space](@entry_id:1131536)."

#### The Fundamental Internal Coordinates: Bonds, Angles, and Dihedrals

Let us formalize the definitions of the most common [internal coordinates](@entry_id:169764) for a chain of four atoms $i, j, k, l$ with Cartesian positions $\mathbf{x}_i, \mathbf{x}_j, \mathbf{x}_k, \mathbf{x}_l$. These definitions rely on geometric primitives like norms, dot products, and cross products, which have well-defined invariance properties under [rigid motions](@entry_id:170523) .

- **Bond Length ($r_{ij}$):** The bond length is the Euclidean distance between atoms $i$ and $j$. It is defined as the norm of the vector connecting their positions.
  $$ r_{ij} = \|\mathbf{x}_j - \mathbf{x}_i\| $$
  Since translations cancel in the difference and rotations preserve norms, the bond length is invariant under all rigid-body motions.

- **Bond Angle ($\theta_{ijk}$):** The bond angle is the angle formed by three atoms $i, j, k$ with atom $j$ as the vertex. It is the angle between the vectors pointing from the central atom $j$ to its neighbors, $\mathbf{u} = \mathbf{x}_i - \mathbf{x}_j$ and $\mathbf{v} = \mathbf{x}_k - \mathbf{x}_j$. Using the geometric definition of the dot product:
  $$ \theta_{ijk} = \arccos\left(\frac{(\mathbf{x}_i - \mathbf{x}_j) \cdot (\mathbf{x}_k - \mathbf{x}_j)}{\|\mathbf{x}_i - \mathbf{x}_j\| \|\mathbf{x}_k - \mathbf{x}_j\|}\right) $$
  The range of the arccosine function, $[0, \pi]$, naturally corresponds to the physical range of a bond angle. Since both dot products and norms of difference vectors are invariant under [rigid motions](@entry_id:170523), so too is the bond angle.

- **Dihedral Angle ($\phi_{ijkl}$):** The [dihedral angle](@entry_id:176389), or torsion, describes the twist around the central bond $j-k$. It is the signed angle between the plane defined by atoms $(i, j, k)$ and the plane defined by atoms $(j, k, l)$. To define this, we first construct normal vectors to these planes using the [cross product](@entry_id:156749). Let the bond vectors be $\mathbf{b}_1 = \mathbf{x}_j - \mathbf{x}_i$, $\mathbf{b}_2 = \mathbf{x}_k - \mathbf{x}_j$, and $\mathbf{b}_3 = \mathbf{x}_l - \mathbf{x}_k$. The normal vectors are:
  $$ \mathbf{n}_1 = \mathbf{b}_1 \times \mathbf{b}_2 \quad \text{and} \quad \mathbf{n}_2 = \mathbf{b}_2 \times \mathbf{b}_3 $$
  The [dihedral angle](@entry_id:176389) is the angle between $\mathbf{n}_1$ and $\mathbf{n}_2$. To capture the sign (e.g., to distinguish right- and left-handed helices), we must use a convention. The standard IUPAC convention defines a signed angle in the range $(-\pi, \pi]$. This is robustly computed using the two-argument arctangent function, $\operatorname{atan2}(y, x)$:
  $$ \phi_{ijkl} = \operatorname{atan2}\left( \left(\frac{\mathbf{n}_1 \times \mathbf{n}_2}{\|\mathbf{n}_1\| \|\mathbf{n}_2\|}\right) \cdot \frac{\mathbf{b}_2}{\|\mathbf{b}_2\|}, \quad \frac{\mathbf{n}_1 \cdot \mathbf{n}_2}{\|\mathbf{n}_1\| \|\mathbf{n}_2\|} \right) $$
  Because proper rotations (elements of $\mathrm{SO}(3)$) preserve the orientation of space (i.e., the "handedness" of [coordinate systems](@entry_id:149266)), the [cross product](@entry_id:156749) and the [scalar triple product](@entry_id:152997) used to define the sign are also invariant under the action of $\mathrm{SE}(3)$. This ensures that the signed [dihedral angle](@entry_id:176389) is a true internal coordinate .

### Degrees of Freedom: Counting Independent Motions

The concept of degrees of freedom (DOF) is central to understanding the dimensionality of a molecule's configuration space. The number of independent [internal coordinates](@entry_id:169764) required for a complete description of shape is precisely the number of internal DOFs.

#### Partitioning Degrees of Freedom

For a system of $N$ atoms, the total number of degrees of freedom is $3N$, corresponding to the three Cartesian coordinates for each atom. These can be partitioned into:
- **External (Rigid-Body) DOFs:** Motions of the molecule as a whole that do not change its shape. These are global translations and rotations.
- **Internal DOFs:** Motions that do change the molecule's shape, such as vibrations and conformational changes.

The number of translational DOFs is always three, corresponding to motion along the $x, y,$ and $z$ axes. The number of rotational DOFs, however, depends on the molecule's structure.

#### Rotational Degrees of Freedom and the Inertia Tensor

The number of independent [rotational degrees of freedom](@entry_id:141502) is equal to the number of [principal axes of rotation](@entry_id:178159) with non-zero [moments of inertia](@entry_id:174259). This can be determined by analyzing the molecule's **inertia tensor**, $\mathbf{I}$. For a set of point masses $m_k$ with [position vectors](@entry_id:174826) $\mathbf{r}_k$ relative to the center of mass, the inertia tensor is a $3 \times 3$ [symmetric matrix](@entry_id:143130):
$$ \mathbf{I} = \sum_{k=1}^{N} m_k \left( (\|\mathbf{r}_k\|^2)\mathbf{1} - \mathbf{r}_k \mathbf{r}_k^{\top} \right) $$
where $\mathbf{1}$ is the $3 \times 3$ identity matrix. The eigenvalues of $\mathbf{I}$ are the principal moments of inertia. A rotation is only physically meaningful (i.e., it changes the orientation of the molecule) if the moment of inertia about the [axis of rotation](@entry_id:187094) is non-zero. Thus, the number of rotational DOFs is the number of non-zero eigenvalues of $\mathbf{I}$ .

An eigenvalue of $\mathbf{I}$ is zero if and only if there exists a non-[zero vector](@entry_id:156189) $\mathbf{v}$ (the [axis of rotation](@entry_id:187094)) such that all atomic [position vectors](@entry_id:174826) $\mathbf{r}_k$ are parallel to $\mathbf{v}$. This leads to a crucial distinction:

1.  **Non-linear Molecule:** The atoms do not all lie on a single straight line. Therefore, no single axis $\mathbf{v}$ exists along which all atoms are aligned. The [inertia tensor](@entry_id:178098) is positive definite, having three non-zero eigenvalues. This gives **3 rotational DOFs**.

2.  **Linear Molecule:** All atoms lie on a single straight line. Let this line be along the unit vector $\mathbf{u}$. Then all $\mathbf{r}_k$ are parallel to $\mathbf{u}$, and the moment of inertia for rotation about this axis is zero. The inertia tensor has one zero eigenvalue and two non-zero eigenvalues. This gives **2 rotational DOFs**.

#### The $3N-6$ and $3N-5$ Rules

With the number of external DOFs established, we can find the number of internal DOFs by subtraction from the total of $3N$:

- For a **non-linear molecule**:
  $N_{\text{internal}} = 3N - N_{\text{trans}} - N_{\text{rot}} = 3N - 3 - 3 = 3N - 6$.
  A minimal set of [internal coordinates](@entry_id:169764) for a non-linear molecule must therefore contain exactly $3N-6$ independent parameters .

- For a **linear molecule**:
  $N_{\text{internal}} = 3N - N_{\text{trans}} - N_{\text{rot}} = 3N - 3 - 2 = 3N - 5$.
  A minimal set of internal coordinates for a linear molecule must contain $3N-5$ parameters .

These simple formulae are cornerstones of [molecular modeling](@entry_id:172257), defining the dimensionality of a molecule's conformational space.

### Systematic Construction: The Z-Matrix and its Properties

While the set of all bond lengths, bond angles, and dihedrals in a molecule is highly redundant, we need a systematic way to select a minimal, [independent set](@entry_id:265066) of $3N-6$ coordinates. The **Z-matrix** provides one such method, particularly for acyclic molecules.

#### The Hierarchical Construction of a Z-Matrix

A Z-matrix builds the [molecular geometry](@entry_id:137852) atom by atom in a hierarchical fashion. By fixing the first few atoms, we eliminate the external degrees of freedom . The procedure is as follows:
1.  **Atom 1:** Placed at the origin of the coordinate system. (Fixes 3 translational DOFs).
2.  **Atom 2:** Placed at a distance $r_{12}$ from atom 1, typically along an axis (e.g., the z-axis). (Fixes 2 rotational DOFs).
3.  **Atom 3:** Placed relative to atoms 1 and 2, using a [bond length](@entry_id:144592) $r_{23}$ and a bond angle $\theta_{123}$. This constrains it to a circle, and placing it in a specific plane (e.g., the xz-plane) fixes the final rotational DOF.
4.  **Atom $i \ge 4$:** Each subsequent atom is defined by a bond length to a preceding atom, a bond angle relative to two preceding atoms, and a [dihedral angle](@entry_id:176389) relative to three preceding atoms.

For an acyclic (tree-like) molecule, this construction results in a complete and minimal set of $3N-6$ [internal coordinates](@entry_id:169764): $(N-1)$ bond lengths, $(N-2)$ [bond angles](@entry_id:136856), and $(N-3)$ [dihedral angles](@entry_id:185221) .

#### Advantages in Computational Practice

The Z-[matrix representation](@entry_id:143451) offers significant advantages, particularly for geometry optimization .
- **Chemical Intuition:** The coordinates (bonds, angles, torsions) correspond directly to familiar chemical features.
- **Decoupling of Motions:** In many molecules, motions are locally coupled. Stretching a bond at one end of a protein has little direct effect on a [dihedral angle](@entry_id:176389) at the other end. This makes the potential energy Hessian matrix in internal coordinates more [diagonally dominant](@entry_id:748380) (or block-diagonal) than in Cartesians.
- **Optimization Efficiency:** Quasi-Newton optimizers, which build an approximation to the inverse Hessian, converge much faster when the Hessian is nearly diagonal. The steps taken by the optimizer align more naturally with the stiff (bond/angle) and soft (torsion) modes of the molecule.
- **Elimination of Rigid-Body Motion:** By working in internal coordinates, the six [zero-energy modes](@entry_id:172472) corresponding to translation and rotation are automatically eliminated from the problem, simplifying the [optimization algorithm](@entry_id:142787).

#### Singularities: The Achilles' Heel of Minimal Coordinates

Despite its advantages, the Z-matrix and other minimal coordinate sets suffer from the presence of **singularities**—specific geometric configurations where the mapping from internal to Cartesian coordinates becomes ill-defined or degenerate.

The most common singularity occurs at **linear bond angles** ($\theta = 0$ or $\pi$) . Consider the definition of a [dihedral angle](@entry_id:176389) $\phi_{ijkl}$, which requires the plane normal $\mathbf{n}_1 = (\mathbf{x}_i-\mathbf{x}_j) \times (\mathbf{x}_k-\mathbf{x}_j)$. If the angle $\theta_{ijk}$ becomes $\pi$ or $0$, the atoms $i, j, k$ become collinear. In this case, the vectors $(\mathbf{x}_i-\mathbf{x}_j)$ and $(\mathbf{x}_k-\mathbf{x}_j)$ are parallel, and their [cross product](@entry_id:156749) $\mathbf{n}_1$ becomes the [zero vector](@entry_id:156189). The plane $(i,j,k)$ is no longer uniquely defined, and consequently, the [dihedral angle](@entry_id:176389) $\phi_{ijkl}$ becomes undefined.

At such a singularity, the Jacobian matrix of the transformation from internal to Cartesian coordinates, $J(\mathbf{q}) = \partial \mathbf{x} / \partial \mathbf{q}$, loses rank . A change in the [dihedral angle](@entry_id:176389) coordinate produces no change in the Cartesian coordinates, meaning the internal coordinate set is no longer locally independent. Geometrically, this corresponds to a collapse of a fiber of the configuration space. For example, at a linear angle, an entire circle ($S^1$) of rotational positions of the fourth atom about the linear axis maps to a single point in the singular internal coordinate representation, creating a cone-like singularity in the manifold .

In contrast, configurations where four atoms are coplanar ($\phi = 0$ or $\pi$) but all bond angles are non-linear are generally not singular. The [dihedral angle](@entry_id:176389) is well-defined, and the [coordinate map](@entry_id:154545) remains smooth and full-rank. Such coplanar states represent a smooth boundary separating regions of opposite [chirality](@entry_id:144105), not a breakdown of the coordinate system itself .

### Advanced Formalism and Special Topologies

While the Z-matrix is a powerful tool for simple acyclic molecules, more complex systems require a more sophisticated mathematical framework to handle topological constraints and the geometry of the configuration space.

#### The Challenge of Cyclic Systems: Redundancy and Constraint

The tree-like, hierarchical structure of a Z-matrix is fundamentally unsuited for describing cyclic molecules. Attempting to define a ring with a Z-matrix involves building an open chain and discovering that the distance and angles required to "close the loop" are not independent parameters but are constrained by the other coordinates .

For a single closed ring of $N$ atoms, the number of internal degrees of freedom is still $3N-6$. However, a simple count of $N$ bond lengths, $N$ [bond angles](@entry_id:136856), and $N$ dihedral angles yields $3N$ parameters, which is far too many. These coordinates are not independent; they are coupled by the geometric requirement of ring closure. This can be formalized by associating a local coordinate frame with each atom and expressing the transformation between adjacent frames as a homogeneous matrix $A_i$ parameterized by the local [bond length](@entry_id:144592), bond angle, and [dihedral angle](@entry_id:176389) . For the ring to be closed, the product of these transformation matrices around the ring must equal the identity matrix:
$$ A_N(\phi_N) \cdots A_2(\phi_2) A_1(\phi_1) = I_{4 \times 4} $$
This single [matrix equation](@entry_id:204751) provides **six independent scalar [constraint equations](@entry_id:138140)** (three for positional closure and three for orientational closure) that the [internal coordinates](@entry_id:169764) must satisfy. If we consider the bond lengths and angles to be fixed, these six equations constrain the $N$ dihedral angles. The number of independently variable dihedrals in a ring is therefore not $N$, but rather $N-6$ (for $N \ge 6$) .

#### The Geometry of Torsion Space

The [dihedral angle](@entry_id:176389) $\phi$ is a periodic coordinate. A rotation of $2\pi$ about the central bond returns the molecule to its original Cartesian configuration. This means that $\phi$ and $\phi + 2\pi k$ for any integer $k$ describe the same physical state. Topologically, the space of a single [dihedral angle](@entry_id:176389) is not the real line $\mathbb{R}$, but a circle, $S^1 \cong \mathbb{R}/(2\pi\mathbb{Z})$ .

This circular topology has profound consequences for numerical algorithms, especially [geometry optimization](@entry_id:151817). Standard [optimization methods](@entry_id:164468) designed for $\mathbb{R}^n$ can fail when applied naively to periodic variables. For instance, the "distance" between two angles $\phi_1 = 0.9\pi$ and $\phi_2 = -0.9\pi$ is not $1.8\pi$, but $0.2\pi$ (the shorter arc on the circle). The correct distance metric is the **[geodesic distance](@entry_id:159682) on the circle**: $d(\phi_1, \phi_2) = \min_{k \in \mathbb{Z}} |\phi_1 - \phi_2 + 2\pi k|$ . Using a naive Euclidean penalty term like $(\phi - \phi_{\text{ref}})^2$ in an objective function can create artificial discontinuities in the potential energy or its gradient at the wrap-around boundary (e.g., at $\pm\pi$), causing optimizers to stall or behave erratically. Robust methods often handle this by embedding the angle into a higher-dimensional space, for example by using $(\cos\phi, \sin\phi)$ as the variables, subject to a constraint, which eliminates the boundary artifacts .

#### The Metric of Configuration Space: Kinetic Energy and the G-matrix

The relationship between internal and Cartesian coordinates is not merely geometric; it has a crucial dynamic aspect captured by the kinetic energy. In Cartesian coordinates, the kinetic energy is a simple sum of squares weighted by mass:
$$ T = \frac{1}{2} \sum_{i=1}^N m_i \|\dot{\mathbf{x}}_i\|^2 = \frac{1}{2} \dot{\mathbf{x}}^{\top} \mathbf{M} \dot{\mathbf{x}} $$
where $\mathbf{M}$ is the [diagonal mass matrix](@entry_id:173002).

To express the kinetic energy in [internal coordinates](@entry_id:169764) $\mathbf{q}$, we use the [chain rule](@entry_id:147422). The velocities are related by the Jacobian matrix $\mathbf{B}(\mathbf{q}) = \partial \mathbf{x} / \partial \mathbf{q}$, such that $\dot{\mathbf{x}} = \mathbf{B}(\mathbf{q}) \dot{\mathbf{q}}$. Substituting this into the kinetic energy expression yields:
$$ T = \frac{1}{2} (\mathbf{B}\dot{\mathbf{q}})^{\top} \mathbf{M} (\mathbf{B}\dot{\mathbf{q}}) = \frac{1}{2} \dot{\mathbf{q}}^{\top} (\mathbf{B}^{\top} \mathbf{M} \mathbf{B}) \dot{\mathbf{q}} $$
This expression has the general form for kinetic energy in [generalized coordinates](@entry_id:156576), $T = \frac{1}{2}\dot{\mathbf{q}}^{\top} \mathbf{G}(\mathbf{q}) \dot{\mathbf{q}}$. By comparison, we identify the **internal-coordinate metric tensor**, often called the **G-matrix**:
$$ \mathbf{G}(\mathbf{q}) = \mathbf{B}(\mathbf{q})^{\top} \mathbf{M} \mathbf{B}(\mathbf{q}) $$
This matrix is fundamental . It defines the Riemannian geometry of the mass-weighted configuration space. Because the Jacobian $\mathbf{B}(\mathbf{q})$ depends on the geometry $\mathbf{q}$, the metric tensor $\mathbf{G}(\mathbf{q})$ is itself a function of the [molecular conformation](@entry_id:163456). The [line element](@entry_id:196833) $ds^2 = d\mathbf{q}^{\top} \mathbf{G} d\mathbf{q}$ represents the squared infinitesimal distance in this mass-weighted space and is related to the kinetic energy by $ds^2 = 2T dt^2$. This metric tensor, which contains all information about masses and geometry, is distinct from the potential energy Hessian and is essential for formulating equations of motion in internal coordinates, such as in [molecular dynamics simulations](@entry_id:160737) or [normal mode analysis](@entry_id:176817).

#### The Jacobian and Volume Elements in Statistical Mechanics

The Jacobian of the coordinate transformation also plays a critical role in statistical mechanics, where it relates the volume elements of different [coordinate systems](@entry_id:149266) for the purpose of integration, for example, in calculating the partition function. The total volume element in the $3N$ Cartesian coordinate space, $dV = d^{3N}\mathbf{x}$, can be decomposed into contributions from external and [internal coordinates](@entry_id:169764). For a triatomic molecule described by bond lengths $b_1, b_2$ and bond angle $\theta$, the volume element can be shown to factorize as :
$$ dV = d^3\mathbf{t} \, d\mu_{\mathrm{SO(3)}}(R) \, J(b_1, b_2, \theta) \, db_1 db_2 d\theta $$
Here, $d^3\mathbf{t}$ is the [volume element](@entry_id:267802) for the center-of-mass translation, $d\mu_{\mathrm{SO(3)}}(R)$ is the volume element for the overall rotation (the Haar measure on $\mathrm{SO}(3)$), and $J(b_1, b_2, \theta)$ is the Jacobian determinant for the [internal coordinates](@entry_id:169764). A detailed derivation shows that for this triatomic case:
$$ J(b_1, b_2, \theta) = b_1^2 b_2^2 \sin\theta $$
This Jacobian factor is not constant; it depends on the internal configuration. The presence of the $\sin\theta$ term is particularly significant: it ensures that the volume of phase space associated with linear configurations ($\theta=0$ or $\pi$) vanishes. This reflects the fact that linear geometries are of lower dimensionality and thus have "zero measure" in the full configuration space of shapes, a principle that generalizes to more complex systems and singularities. The choice of coordinates thus imprints itself not only on the dynamics but also on the statistical properties of the system.