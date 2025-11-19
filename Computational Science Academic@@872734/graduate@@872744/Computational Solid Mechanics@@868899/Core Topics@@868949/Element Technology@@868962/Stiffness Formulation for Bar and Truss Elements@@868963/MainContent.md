## Introduction
The stiffness formulation for bar and truss elements represents a foundational pillar of the Finite Element Method (FEM), providing the essential link between a physical structure and its computational model. For students and engineers in computational mechanics, mastering this formulation is the first step toward analyzing complex structural systems. The primary challenge lies in systematically deriving the properties of a simplified one-dimensional element from continuum principles and correctly assembling these elements to represent an entire structure. This article addresses this by providing a comprehensive walkthrough of the stiffness method from first principles to advanced applications.

The journey begins in the **Principles and Mechanisms** chapter, which lays the theoretical groundwork. You will learn how kinematic assumptions, [shape functions](@entry_id:141015), and energy principles like the Principle of Virtual Work are used to derive the iconic [element stiffness matrix](@entry_id:139369). We will then cover the crucial steps of [coordinate transformation](@entry_id:138577) and the assembly of the global [system matrix](@entry_id:172230). Following this, the **Applications and Interdisciplinary Connections** chapter demonstrates the true power and versatility of the formulation, exploring its extension to [structural dynamics](@entry_id:172684), geometric and [material nonlinearity](@entry_id:162855), and [coupled-field problems](@entry_id:747960) in diverse fields from [aerospace engineering](@entry_id:268503) to biomechanics. Finally, the **Hands-On Practices** section provides targeted exercises to solidify your understanding and guide you through the critical verification steps needed for robust computational implementation.

## Principles and Mechanisms

### The Kinematic Foundation of Bar and Truss Elements

The formulation of a bar or [truss element](@entry_id:177354) in the Finite Element Method (FEM) begins with a series of crucial simplifying assumptions that reduce a three-dimensional physical member to a one-dimensional mathematical abstraction. These elements are structural members designed to carry loads only along their longitudinal axis. Consequently, they are assumed to be in a state of **uniaxial stress**. This fundamental assumption dictates the entire kinematic framework of the element.

Consider a straight, prismatic member in space. We define a [local coordinate system](@entry_id:751394) with the $\hat{\boldsymbol{e}}_{x}$ axis aligned with the member's centroidal axis. The core kinematic assumption is that the [displacement field](@entry_id:141476), $\boldsymbol{u}$, within the element is purely axial and varies only along this axis. That is, $\boldsymbol{u}(x, y, z) = u(x)\hat{\boldsymbol{e}}_{x}$.

This seemingly drastic simplification is justified within the context of [small-strain kinematics](@entry_id:192140), where the strain tensor $\boldsymbol{\varepsilon}$ is defined as the symmetric part of the [displacement gradient](@entry_id:165352): $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^{\mathsf{T}})$. If we only consider an axial displacement $u(x)$, the only non-zero component of the strain tensor is the [axial strain](@entry_id:160811), $\varepsilon_{xx} = \frac{du}{dx}$. All transverse normal strains ($\varepsilon_{yy}$, $\varepsilon_{zz}$) and all shear strains ($\varepsilon_{xy}$, $\varepsilon_{xz}$, $\varepsilon_{yz}$) are identically zero.

Why are transverse displacements and rotations excluded from the element's internal deformation model?
- **Transverse Displacements**: Any small, uniform transverse displacement of the element constitutes a [rigid-body motion](@entry_id:265795), which does not induce strain and therefore stores no internal energy. A differential transverse displacement between the element's ends would produce shear strains ($\varepsilon_{xy} = \frac{1}{2} \frac{dv}{dx}$), but a [truss element](@entry_id:177354) is assumed to possess no shear rigidity. To enforce this, we must kinematically constrain the element to have zero [shear strain](@entry_id:175241), which implies that transverse displacements must be constant along the element's length. Therefore, transverse displacements do not contribute to the element's deformational stiffness.
- **Rotational Degrees of Freedom (DOF)**: Truss elements are connected by pin joints, which, by definition, cannot transmit moments. In the framework of [virtual work](@entry_id:176403), nodal forces are energetically conjugate to nodal displacements, and nodal moments are conjugate to nodal rotations. Since no moments can be transmitted, nodal rotations can do no work on the element and cannot cause it to store [strain energy](@entry_id:162699). The [internal virtual work](@entry_id:172278), $\delta W_{\text{int}} = \int \boldsymbol{\sigma}:\delta\boldsymbol{\varepsilon}\, \mathrm{d}V$, contains only terms related to axial stress and [axial strain](@entry_id:160811). As there is no strain measure conjugate to a rotation in this formulation, rotational DOFs are irrelevant to the element's stiffness. [@problem_id:3602959]

This simplified model, which captures only axial elongation and compression, forms the basis for deriving the element's stiffness properties.

### Interpolation and Shape Functions

Having established that the element's behavior is governed by the one-dimensional axial [displacement field](@entry_id:141476) $u(x)$, we must approximate this continuous field using a finite number of parameters. In FEM, we use the values of the displacement at the element's endpoints, or **nodes**. A standard two-node [bar element](@entry_id:746680) of length $L$ has node 1 at $x=0$ and node 2 at $x=L$, with corresponding axial displacements $u_1$ and $u_2$.

The displacement $u(x)$ at any point along the element is interpolated from these nodal values using **shape functions**, $N_1(x)$ and $N_2(x)$:
$u(x) = N_1(x) u_1 + N_2(x) u_2$

These [shape functions](@entry_id:141015) are not arbitrary. They must satisfy several key properties to ensure physically meaningful behavior [@problem_id:3602955]:
1.  **Kronecker-Delta Property**: The shape function for a given node must be equal to one at that node and zero at all other nodes. This ensures that the interpolated displacement at a node is exactly equal to the prescribed nodal displacement. For our two-node element:
    - $N_1(0) = 1$ and $N_1(L) = 0$
    - $N_2(0) = 0$ and $N_2(L) = 1$

2.  **Partition of Unity**: The sum of the shape functions must equal one everywhere within the element: $N_1(x) + N_2(x) = 1$. This property guarantees that the element can exactly represent a **[rigid-body motion](@entry_id:265795)**. If both nodes translate by the same amount, $u_1 = u_2 = c$, then $u(x) = N_1(x) c + N_2(x) c = (N_1(x) + N_2(x))c = c$. The entire element correctly displaces by the constant amount $c$ without deforming.

3.  **Linear Completeness**: The chosen interpolation must be able to exactly represent a state of constant strain. Since [axial strain](@entry_id:160811) is $\varepsilon = du/dx$, a constant strain implies a linear displacement field, $u(x) = a + bx$. The shape functions must be able to reproduce this field.

For a two-node element, the simplest functions that satisfy these criteria are linear polynomials. By applying the Kronecker-delta properties to the general [linear form](@entry_id:751308) $N(x) = c_1 + c_2x$, we derive the unique linear [shape functions](@entry_id:141015) for the [bar element](@entry_id:746680):
$$
N_1(x) = 1 - \frac{x}{L}
$$
$$
N_2(x) = \frac{x}{L}
$$
The final answer for the [shape functions](@entry_id:141015) can be represented as:
$$
\begin{pmatrix} 1 - \frac{x}{L} & \frac{x}{L} \end{pmatrix}
$$

### From Displacements to Strains and Stresses

With the displacement field now defined in terms of nodal DOFs, we can derive the strain and stress fields. The small-strain [axial strain](@entry_id:160811) $\varepsilon$ is the spatial derivative of the axial displacement $u(x)$:
$$
\varepsilon(x) = \frac{du}{dx} = \frac{d}{dx} \left( N_1(x) u_1 + N_2(x) u_2 \right) = \frac{dN_1}{dx} u_1 + \frac{dN_2}{dx} u_2
$$
Substituting the derivatives of our linear [shape functions](@entry_id:141015), $\frac{dN_1}{dx} = -1/L$ and $\frac{dN_2}{dx} = 1/L$, we obtain:
$$
\varepsilon(x) = -\frac{1}{L} u_1 + \frac{1}{L} u_2 = \frac{u_2 - u_1}{L}
$$
This is a crucial result: for a two-node [bar element](@entry_id:746680) with linear shape functions, the [axial strain](@entry_id:160811) is **constant** throughout the element. This is why it is often called a Constant Strain Bar element. In matrix form, this is written as $\varepsilon = \mathbf{B} \mathbf{d}$, where $\mathbf{d} = \begin{pmatrix} u_1 \\ u_2 \end{pmatrix}$ is the vector of nodal displacements and $\mathbf{B}$ is the [strain-displacement matrix](@entry_id:163451):
$$
\mathbf{B} = \begin{pmatrix} -\frac{1}{L} & \frac{1}{L} \end{pmatrix}
$$
The stress field is then determined by the material's constitutive law, which for [linear elasticity](@entry_id:166983) is Hooke's Law, $\sigma = E\varepsilon$. If the Young's modulus $E$ is constant, the stress is also constant. However, if the material properties vary along the length of the bar, e.g., $E=E(x)$, then the stress will also vary despite the constant strain [@problem_id:3602990]:
$$
\sigma(x) = E(x)\varepsilon = E(x) \left( \frac{u_2 - u_1}{L} \right)
$$

### Derivation of the Element Stiffness Matrix

The **[stiffness matrix](@entry_id:178659)**, denoted $\mathbf{k}_e$, is the operator that relates the nodal displacements of an element to the internal nodal forces, $\mathbf{f}_{\text{int}}$, that resist this deformation: $\mathbf{f}_{\text{int}} = \mathbf{k}_e \mathbf{d}$. This matrix is the centerpiece of stiffness-based [finite element analysis](@entry_id:138109) and can be derived from fundamental energy principles.

#### The Principle of Minimum Potential Energy

For a conservative elastic system, the equilibrium configuration is the one that minimizes the total potential energy, $\Pi$. The [total potential energy](@entry_id:185512) is the sum of the internal strain energy, $U$, and the potential of the external loads. We focus on the [strain energy](@entry_id:162699), defined as the integral of the [strain energy density](@entry_id:200085) over the element's volume:
$$
U = \frac{1}{2} \int_V \sigma \varepsilon \, dV
$$
For a bar with constant cross-sectional area $A$, this becomes $U = \frac{1}{2} \int_0^L A \sigma(x) \varepsilon(x) \, dx$. We can express this entirely in terms of the nodal displacements $\mathbf{d}$ [@problem_id:3603024]:
1.  Substitute the [constitutive law](@entry_id:167255) $\sigma = E\varepsilon$: $U = \frac{1}{2} \int_0^L A E \varepsilon^2 \, dx$.
2.  Substitute the strain-displacement relation $\varepsilon = \mathbf{B}\mathbf{d}$: $U = \frac{1}{2} \int_0^L A E (\mathbf{B}\mathbf{d})^{\mathsf{T}}(\mathbf{B}\mathbf{d}) \, dx$.
3.  Using [matrix transpose](@entry_id:155858) properties, this becomes $U = \frac{1}{2} \int_0^L \mathbf{d}^{\mathsf{T}} \mathbf{B}^{\mathsf{T}} E A \mathbf{B} \mathbf{d} \, dx$.
4.  Since the nodal displacements $\mathbf{d}$ are not functions of $x$, they can be factored out of the integral:
    $$
    U = \frac{1}{2} \mathbf{d}^{\mathsf{T}} \left( \int_0^L \mathbf{B}^{\mathsf{T}} E A \mathbf{B} \, dx \right) \mathbf{d}
    $$
This gives the strain energy in a standard [quadratic form](@entry_id:153497), $U = \frac{1}{2}\mathbf{d}^{\mathsf{T}} \mathbf{k}_e \mathbf{d}$. By comparison, we can identify the [element stiffness matrix](@entry_id:139369) as:
$$
\mathbf{k}_e = \int_0^L \mathbf{B}^{\mathsf{T}} E A \mathbf{B} \, dx
$$
For a standard bar with constant $E$ and $A$, the integrand is constant. Substituting $\mathbf{B} = \frac{1}{L}\begin{pmatrix} -1 & 1 \end{pmatrix}$:
$$
\mathbf{k}_e = EA \int_0^L \frac{1}{L^2} \begin{pmatrix} -1 \\ 1 \end{pmatrix} \begin{pmatrix} -1 & 1 \end{pmatrix} \, dx = \frac{EA}{L^2} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix} \int_0^L dx
$$
The integral evaluates to $L$, yielding the iconic stiffness matrix for a two-node [bar element](@entry_id:746680):
$$
\mathbf{k}_e = \frac{EA}{L} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}
$$

#### The Principle of Virtual Work

An alternative and more general approach is the Principle of Virtual Work (PVW), which states that for a system in equilibrium, the [internal virtual work](@entry_id:172278) done by stresses over a virtual strain field is equal to the external virtual work done by external forces over a corresponding [virtual displacement](@entry_id:168781) field: $\delta W_{\text{int}} = \delta W_{\text{ext}}$.

The [internal virtual work](@entry_id:172278) for our bar is [@problem_id:3602996]:
$$
\delta W_{\text{int}} = \int_0^L A \sigma \delta\varepsilon \, dx = \int_0^L A (E\varepsilon) \delta\varepsilon \, dx
$$
Discretizing the virtual fields similarly to the real fields, $\delta\varepsilon = \mathbf{B}\delta\mathbf{d}$, we get:
$$
\delta W_{\text{int}} = \int_0^L A (E \mathbf{B}\mathbf{d})^{\mathsf{T}} (\mathbf{B}\delta\mathbf{d}) \, dx = \delta\mathbf{d}^{\mathsf{T}} \left( \int_0^L \mathbf{B}^{\mathsf{T}} E A \mathbf{B} \, dx \right) \mathbf{d}
$$
The external [virtual work](@entry_id:176403) done by internal nodal forces is $\delta W_{\text{int}} = \delta\mathbf{d}^{\mathsf{T}}\mathbf{f}_{\text{int}} = \delta\mathbf{d}^{\mathsf{T}} \mathbf{k}_e \mathbf{d}$. Comparing these expressions again identifies the stiffness matrix as $\mathbf{k}_e = \int_0^L \mathbf{B}^{\mathsf{T}} E A \mathbf{B} \, dx$, leading to the same result.

#### Physical Interpretation of the Stiffness Matrix

Each entry $k_{ij}$ of the stiffness matrix has a clear physical meaning: it is the force at degree of freedom $i$ required to produce a unit displacement at degree of freedom $j$, while all other degrees of freedom are held at zero. Let's analyze the matrix $\mathbf{k}_e = \frac{EA}{L} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}$ [@problem_id:3603005].

- **Diagonal Terms ($k_{11}, k_{22}$)**: Consider imposing a displacement $u_1 > 0$ while holding $u_2 = 0$. The bar is compressed. The resisting force at node 1 is $f^{\text{int}}_1 = k_{11}u_1 = \frac{EA}{L}u_1$. This force is positive (in the $+x$ direction) to resist the compression. Thus, the positive diagonal terms represent the direct stiffness at a node.
- **Off-Diagonal Terms ($k_{12}, k_{21}$)**: In the same experiment ($u_1 > 0, u_2=0$), the force at node 2 is $f^{\text{int}}_2 = k_{21}u_1 = -\frac{EA}{L}u_1$. This force is negative, representing the reaction at the fixed end. The negative off-diagonal terms represent the force transmitted to the opposite node, which for static equilibrium must be equal and opposite.
- **Rigid-Body Motion**: If we impose a rigid-body translation, $u_1=u_2=c$, the resulting forces are zero: $\mathbf{f}_{\text{int}} = \frac{EA}{L} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix} \begin{pmatrix} c \\ c \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$. This shows that the [stiffness matrix](@entry_id:178659) correctly produces no forces for a displacement that causes no strain.

#### Consistent Nodal Loads

The PVW framework also provides a rigorous method for converting [distributed loads](@entry_id:162746) into equivalent, or **consistent**, nodal forces. For a distributed axial load $p(x)$, the external virtual work is $\int_0^L p(x)\delta u(x) \, dx$. Discretizing the [virtual displacement](@entry_id:168781) $\delta u(x) = \mathbf{N}(x)\delta\mathbf{d}$, we get:
$$
\delta W_{\text{ext, distributed}} = \int_0^L p(x)\mathbf{N}(x)\delta\mathbf{d} \, dx = \delta\mathbf{d}^{\mathsf{T}} \int_0^L \mathbf{N}(x)^{\mathsf{T}}p(x) \, dx
$$
This term must equal $\delta\mathbf{d}^{\mathsf{T}}\mathbf{f}_p$, where $\mathbf{f}_p$ is the consistent nodal [load vector](@entry_id:635284). Therefore:
$$
\mathbf{f}_p = \int_0^L \mathbf{N}(x)^{\mathsf{T}}p(x) \, dx
$$
For a uniform load $p(x) = q$, the integral for our linear element becomes [@problem_id:3602990]:
$$
\mathbf{f}_p = q \int_0^L \begin{pmatrix} 1 - x/L \\ x/L \end{pmatrix} dx = q \begin{pmatrix} [x - x^2/(2L)]_0^L \\ [x^2/(2L)]_0^L \end{pmatrix} = \begin{pmatrix} qL/2 \\ qL/2 \end{pmatrix} = \frac{qL}{2}\begin{pmatrix} 1 \\ 1 \end{pmatrix}
$$
This familiar result—that a uniform load is split equally between the two nodes—is thus shown to be energetically consistent with the assumed linear displacement field.

### Transformation to Global Coordinates

Individual elements in a truss structure are oriented arbitrarily in space. To analyze the structure as a whole, we must express the stiffness properties of each element in a common **global coordinate system**. This is achieved through a [coordinate transformation](@entry_id:138577).

#### Kinematic Transformation

The key is to relate the element's local axial displacements, $\{u_{1a}, u_{2a}\}$, to the global translational displacements of its nodes. Let's consider a 3D [truss element](@entry_id:177354) connecting node 1 at $(x_1, y_1, z_1)$ to node 2 at $(x_2, y_2, z_2)$. The vector along the member is $\mathbf{V} = (x_2-x_1)\mathbf{i} + (y_2-y_1)\mathbf{j} + (z_2-z_1)\mathbf{k}$. The [unit vector](@entry_id:150575) along this axis is $\mathbf{\hat{e}} = \mathbf{V}/L$, where $L = ||\mathbf{V}||$. The components of $\mathbf{\hat{e}}$ are the **[direction cosines](@entry_id:170591)**: $(c_x, c_y, c_z)$.

The local axial displacement at a node is the [scalar projection](@entry_id:148823) of its global displacement vector onto the element's local axis. For node 1, with global [displacement vector](@entry_id:262782) $\mathbf{d}_1 = u_{1x}\mathbf{i} + u_{1y}\mathbf{j} + u_{1z}\mathbf{k}$, the local axial displacement $u_{1a}$ is [@problem_id:3602993]:
$$
u_{1a} = \mathbf{d}_1 \cdot \mathbf{\hat{e}} = c_x u_{1x} + c_y u_{1y} + c_z u_{1z}
$$
A similar relation holds for node 2. We can express this for the entire element in matrix form, $\mathbf{d}_{\text{local}} = \mathbf{T} \mathbf{d}_{\text{global}}$:
$$
\begin{pmatrix} u_{1a} \\ u_{2a} \end{pmatrix} = \begin{pmatrix} c_x & c_y & c_z & 0 & 0 & 0 \\ 0 & 0 & 0 & c_x & c_y & c_z \end{pmatrix} \begin{pmatrix} u_{1x} \\ u_{1y} \\ u_{1z} \\ u_{2x} \\ u_{2y} \\ u_{2z} \end{pmatrix}
$$
The $2 \times 6$ matrix $\mathbf{T}$ is the **transformation matrix** that maps the 6 global DOFs to the 2 local DOFs.

#### The Global Element Stiffness Matrix

The transformation of the [stiffness matrix](@entry_id:178659) follows from the invariance of strain energy. The [strain energy](@entry_id:162699) in [local coordinates](@entry_id:181200) is $U = \frac{1}{2} \mathbf{d}_{\text{local}}^{\mathsf{T}} \mathbf{k}_e \mathbf{d}_{\text{local}}$. Substituting $\mathbf{d}_{\text{local}} = \mathbf{T} \mathbf{d}_{\text{global}}$, we get:
$$
U = \frac{1}{2} (\mathbf{T} \mathbf{d}_{\text{global}})^{\mathsf{T}} \mathbf{k}_e (\mathbf{T} \mathbf{d}_{\text{global}}) = \frac{1}{2} \mathbf{d}_{\text{global}}^{\mathsf{T}} (\mathbf{T}^{\mathsf{T}} \mathbf{k}_e \mathbf{T}) \mathbf{d}_{\text{global}}
$$
By comparing this to $U = \frac{1}{2}\mathbf{d}_{\text{global}}^{\mathsf{T}} \mathbf{K}_g \mathbf{d}_{\text{global}}$, we identify the [element stiffness matrix](@entry_id:139369) in global coordinates, $\mathbf{K}_g$, as:
$$
\mathbf{K}_g = \mathbf{T}^{\mathsf{T}} \mathbf{k}_e \mathbf{T}
$$
For a 2D planar [truss element](@entry_id:177354) oriented at an angle $\theta$ to the global x-axis (with $c = \cos\theta, s = \sin\theta$), this operation yields a $4 \times 4$ global stiffness matrix [@problem_id:3603023]:
$$
\mathbf{K}_g = \frac{EA}{L} \begin{pmatrix} c^2 & cs & -c^2 & -cs \\ cs & s^2 & -cs & -s^2 \\ -c^2 & -cs & c^2 & cs \\ -cs & -s^2 & cs & s^2 \end{pmatrix}
$$
The off-diagonal terms containing $cs$ are **coupling terms**. They arise because the element's axial stiffness is not aligned with the global axes. For example, a vertical displacement $u_{iy}$ at node $i$ will cause the element to stretch or compress (unless it's perfectly vertical), inducing an axial force. This axial force, directed along the element, will have components in both the global $x$ and $y$ directions. The term $K_{12} = \frac{EA}{L}cs$ quantifies the force generated in the global $x$-direction at node $i$ due to a unit displacement in the global $y$-direction at the same node.

### Assembly of the Global System

Once the [stiffness matrix](@entry_id:178659) for each element is formulated in the common global coordinate system, they must be assembled into a single **[global stiffness matrix](@entry_id:138630)**, $\mathbf{K}$, for the entire structure. This matrix relates the global vector of all nodal displacements, $\mathbf{U}$, to the global vector of all external nodal forces, $\mathbf{F}$, via the system of equations $\mathbf{K}\mathbf{U} = \mathbf{F}$.

The assembly process, known as the **[direct stiffness method](@entry_id:176969)**, is a systematic book-keeping operation based on the principle of superposition [@problem_id:3603032]:
1.  **Global DOF Numbering**: Assign a unique index to every degree of freedom in the structure. For a 2D truss with $N$ nodes, there are $2N$ DOFs. A standard scheme is to number them node-by-node: for node $i$, the $x$-DOF is $2i-1$ and the $y$-DOF is $2i$.
2.  **Element Index Vector**: For each element connecting nodes $i$ and $j$, create an **index vector** (or location vector) that maps its local DOF ordering to the global DOF indices. For a 2D element connecting nodes $i$ and $j$, this vector is $\mathbf{I} = [2i-1, 2i, 2j-1, 2j]$.
3.  **Scatter-Add Assembly**: Initialize the global stiffness matrix $\mathbf{K}$ (of size $2N \times 2N$) with all zeros. Then, for each element $e$:
    a.  Calculate its global [element stiffness matrix](@entry_id:139369) $\mathbf{K}_g^{(e)}$.
    b.  For each entry $K_{g,pq}^{(e)}$ in the $4 \times 4$ element matrix, add its value to the global matrix at the location specified by the index vector: $K_{\mathbf{I}(p), \mathbf{I}(q)} \leftarrow K_{\mathbf{I}(p), \mathbf{I}(q)} + K_{g,pq}^{(e)}$.

This process ensures that the stiffness contributions of elements sharing a node are correctly summed at the corresponding global DOFs, reflecting the physical connection and force equilibrium at that node.

### Properties of the Global Stiffness Matrix: Stability and Rigid-Body Modes

The assembled [global stiffness matrix](@entry_id:138630) $\mathbf{K}$ contains profound information about the behavior of the entire structure. A key concept is its **null space**, which consists of all displacement vectors $\mathbf{U}$ for which $\mathbf{K}\mathbf{U} = \mathbf{0}$.

A displacement vector $\mathbf{U}$ resulting in zero nodal forces is a **[zero-energy mode](@entry_id:169976)**, as the [strain energy](@entry_id:162699) is $U = \frac{1}{2}\mathbf{U}^{\mathsf{T}}\mathbf{K}\mathbf{U} = 0$. These [zero-energy modes](@entry_id:172472) correspond to motions that do not deform the structure. For an unconstrained structure, these are the **rigid-body modes** [@problem_id:3602969]. A free-floating planar structure has three such modes:
1.  Translation in the $x$-direction: $\mathbf{U}_{Tx} = [1, 0, 1, 0, \dots, 1, 0]^{\mathsf{T}}$
2.  Translation in the $y$-direction: $\mathbf{U}_{Ty} = [0, 1, 0, 1, \dots, 0, 1]^{\mathsf{T}}$
3.  Infinitesimal rotation about a point (e.g., the origin): For a node $i$ at $(x_i, y_i)$, the displacement is $(-y_i, x_i)$. The corresponding global vector is $\mathbf{U}_R = [-y_1, x_1, -y_2, x_2, \dots, -y_N, x_N]^{\mathsf{T}}$.

These three vectors are [linearly independent](@entry_id:148207) and lie in the [null space](@entry_id:151476) of the [global stiffness matrix](@entry_id:138630) of any stable, unconstrained planar structure. This means the matrix $\mathbf{K}$ is necessarily **singular**, and its rank is less than its full dimension. The dimension of the null space (its nullity) is, by the [rank-nullity theorem](@entry_id:154441), $n - \text{rank}(\mathbf{K})$, where $n$ is the total number of DOFs.

If the structure is a stable arrangement, like a simple triangle, it has no internal "floppiness" or **mechanisms**. In this case, the only [zero-energy modes](@entry_id:172472) are the rigid-body motions. Therefore, for a stable, unconstrained planar truss, the dimension of the null space of $\mathbf{K}$ is exactly 3. The [stiffness matrix](@entry_id:178659) has three zero eigenvalues, and their corresponding eigenvectors are the rigid-body modes. For the structure to be solvable under external loads, these rigid-body modes must be eliminated by applying sufficient boundary conditions (supports), which renders the modified [stiffness matrix](@entry_id:178659) non-singular.