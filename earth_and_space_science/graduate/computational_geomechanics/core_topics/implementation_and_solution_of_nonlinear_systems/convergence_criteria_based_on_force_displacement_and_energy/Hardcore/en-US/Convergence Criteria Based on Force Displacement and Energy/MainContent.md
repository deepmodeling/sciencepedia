## Introduction
In computational geomechanics, accurately solving nonlinear problems with the Finite Element Method (FEM) hinges on incremental-iterative procedures like the Newton-Raphson method. These algorithms progressively refine a solution within each load step, but they present a critical question: when is the solution "good enough" to stop iterating? Terminating too early compromises accuracy and physical validity, while iterating excessively wastes valuable computational time. This decision is governed by convergence criteria, which are the formal rules that assess whether an approximate solution has converged to the true equilibrium state.

This article provides a comprehensive exploration of the three pillars of convergence assessment: criteria based on force, displacement, and energy. It addresses the crucial knowledge gap between simply knowing the criteria exist and understanding how to apply them robustly in the face of complex geomechanical phenomena. Across three chapters, you will gain a deep, practical understanding of this fundamental topic. "Principles and Mechanisms" will lay the groundwork, defining each criterion, exploring its physical meaning, and discussing the vital role of normalization. "Applications and Interdisciplinary Connections" will examine how these criteria are adapted for advanced challenges like material plasticity, strain softening, and multiphysics coupling. Finally, "Hands-On Practices" will offer practical problems to solidify your ability to implement and interpret these criteria in real-world simulations.

## Principles and Mechanisms

In the preceding section, we established that solving nonlinear boundary value problems in geomechanics via the Finite Element Method (FEM) necessitates an incremental-iterative approach. Within each load increment, the system's state is unknown and must be found by an iterative procedure, such as the Newton-Raphson method, that progressively refines an approximate solution. The pivotal question at the heart of this process is: when do we stop iterating? A premature stop yields an inaccurate solution that violates fundamental physical principles, while excessive iteration wastes computational resources. The decision to terminate the iterative process is governed by **convergence criteria**.

This chapter delves into the principles and mechanisms of the three primary types of convergence criteria used in computational geomechanics: those based on **force**, **displacement**, and **energy**. We will define each criterion, explore its physical and numerical significance, discuss the critical importance of normalization, and examine how their interpretation becomes more nuanced in the context of advanced material behaviors such as plasticity and softening.

### The Foundation: The Residual Force Vector

The cornerstone of any static or quasi-static analysis is the principle of equilibrium. In a discrete finite element context, this principle translates into the requirement that the vector of internal nodal forces, $\mathbf{f}_{\mathrm{int}}(\mathbf{u})$, which arises from the stresses within the elements, must balance the vector of externally applied nodal forces, $\mathbf{f}_{\mathrm{ext}}$.

$$
\mathbf{f}_{\mathrm{int}}(\mathbf{u}) = \mathbf{f}_{\mathrm{ext}}
$$

During an iterative solution, an approximate displacement vector $\mathbf{u}^{(k)}$ at iteration $k$ will generally not satisfy this condition perfectly. The imbalance between the external and internal forces is quantified by the **residual force vector**, $\mathbf{r}(\mathbf{u})$:

$$
\mathbf{r}(\mathbf{u}^{(k)}) = \mathbf{f}_{\mathrm{ext}} - \mathbf{f}_{\mathrm{int}}(\mathbf{u}^{(k)})
$$

The residual vector represents the net nodal forces required to hold the system in equilibrium at the configuration $\mathbf{u}^{(k)}$. Consequently, the entire goal of the iterative algorithm is to find a displacement field $\mathbf{u}^*$ for which the residual vanishes, i.e., $\mathbf{r}(\mathbf{u}^*) = \mathbf{0}$. A **force-based convergence criterion**, therefore, directly measures the extent to which the fundamental law of equilibrium is satisfied.

A crucial distinction must be made between free and constrained degrees of freedom (DOFs) [@problem_id:3511055]. The iterative solver only seeks to find the unknown displacements for the free DOFs. The residual components corresponding to these free DOFs, $\mathbf{r}_f$, must be driven to zero. The residual components on the constrained DOFs, $\mathbf{r}_c$, where displacements are prescribed, are not driven to zero by the solver. Instead, upon convergence, they represent the negative of the **reaction forces**, $\mathbf{f}_{\mathrm{react}}$, required to enforce the prescribed displacements.

$$
\mathbf{f}_{\mathrm{react},c} = \mathbf{f}_{\mathrm{int},c} - \mathbf{f}_{\mathrm{ext},c} = - \mathbf{r}_c(\mathbf{u}^*)
$$

Therefore, a force-based convergence criterion must be evaluated *only* on the norm of the residual corresponding to the free degrees of freedom, $\lVert \mathbf{r}_f \rVert$. Including the constrained DOFs in the convergence norm is a common and critical error, as the non-zero reaction forces would prevent the criterion from ever being satisfied, masking the true convergence status of the solution.

### The Three Pillars of Convergence Assessment

While the force residual is the most direct measure of equilibrium, relying on it exclusively can be misleading in certain situations. A robust convergence assessment rests on three distinct but related pillars, each monitoring a different aspect of the solution's quality.

#### Force-Based Criteria: The Check on Physics

As established, a force-based criterion monitors a norm of the residual vector, $\lVert \mathbf{r}_f \rVert$. A small value indicates that the internal stresses have adjusted to the applied loads and the system is in a state of near-perfect force balance. This is the most fundamental physical check.

#### Displacement-Based Criteria: The Check on Kinematics

A displacement-based criterion monitors the magnitude of the change in the solution vector from one iteration to the next. The Newton-Raphson update is given by:

$$
\mathbf{u}^{(k+1)} = \mathbf{u}^{(k)} + \Delta \mathbf{u}^{(k)}
$$

where the displacement increment $\Delta \mathbf{u}^{(k)}$ is found by solving the linearized system $\mathbf{K}_t \Delta \mathbf{u}^{(k)} = \mathbf{r}^{(k)}$. A displacement-based criterion checks if the norm of the increment, $\lVert \Delta \mathbf{u}^{(k)} \rVert$, has become sufficiently small. This criterion does not directly measure equilibrium; instead, it measures the **stagnation of the iterative process** [@problem_id:3511131]. A small increment implies that further iterations are unlikely to significantly change the solution.

It is vital to understand that force and displacement criteria are not equivalent. The relationship $\Delta \mathbf{u}^{(k)} = \mathbf{K}_t^{-1} \mathbf{r}^{(k)}$ shows that their relative magnitudes are mediated by the tangent stiffness matrix $\mathbf{K}_t$. In a very stiff system (large $\mathbf{K}_t$), a large force residual might produce only a tiny displacement increment, leading a displacement-only criterion to declare convergence prematurely. Conversely, near a limit point or in a softening regime, the stiffness matrix becomes ill-conditioned or singular (small $\mathbf{K}_t$), and a small residual can cause a very large displacement increment, which a force-only criterion might miss. This dual perspective is why both criteria are necessary.

#### Energy-Based Criteria: The Integrated Check

An energy-based criterion provides a single, scalar measure that integrates both force and displacement information. The most common and physically meaningful energy measure is the **work done by the residual forces** during the current displacement increment [@problem_id:3511143]:

$$
W_{\mathrm{res}}^{(k)} = (\mathbf{r}^{(k)})^T \Delta \mathbf{u}^{(k)}
$$

This quantity represents the energy imbalance in the system. At convergence, as $\mathbf{r}^{(k)} \to \mathbf{0}$, this work should also vanish. An energy criterion is often considered a more global and robust measure than the force norm, as it is less sensitive to highly localized residual force peaks. It is important to define energy criteria with careful attention to physical dimensions; constructs such as $\lVert \mathbf{r} \rVert / \lVert \Delta \mathbf{u} \rVert$ are dimensionally inconsistent with energy (representing a stiffness) and do not approach zero at convergence, making them unsuitable as criteria [@problem_id:3511143].

### Practical Implementation: The Imperative of Normalization

To be universally applicable, convergence criteria must be independent of arbitrary choices like the system of units (e.g., Newtons vs. kilonewtons) or the physical scale of the problem (e.g., a lab sample vs. a dam) [@problem_id:3511109]. A raw tolerance value, such as $\lVert \mathbf{r} \rVert \lt 1.0$, is meaningless without knowing the units. This is achieved through **nondimensionalization**, where the computed norm is scaled by a relevant characteristic quantity of the same dimension.

A robust set of normalized criteria is as follows:

*   **Normalized Force Criterion:** The residual norm is normalized by a characteristic force, typically the norm of the total external loads, $\lVert \mathbf{f}_{\mathrm{ext}} \rVert$. A more robust denominator uses the maximum of the external load norm and the initial residual norm for the increment, $\lVert \mathbf{r}^{(0)} \rVert$, to handle cases with no applied loads (e.g., prescribed displacement steps).
    $$
    \frac{\lVert\mathbf{r}^{(k)}\rVert}{\max(\lVert\mathbf{f}_{\mathrm{ext}}\rVert, \lVert\mathbf{r}^{(0)}\rVert, \epsilon_F)} \le \varepsilon_r
    $$
    Here, $\varepsilon_r$ is a small, dimensionless tolerance (e.g., $10^{-3}$), and $\epsilon_F$ is a small absolute value to prevent division by zero.

*   **Normalized Displacement Criterion:** The displacement increment is normalized by a characteristic displacement. A common choice is the norm of the total displacement at the current iteration, $\lVert \mathbf{u}^{(k)} \rVert$.
    $$
    \frac{\lVert \Delta \mathbf{u}^{(k)} \rVert}{\lVert \mathbf{u}^{(k)} \rVert} \le \varepsilon_u
    $$
    This relative criterion, however, becomes ill-posed when $\lVert \mathbf{u}^{(k)} \rVert$ is close to zero, for example, at the beginning of an analysis [@problem_id:3511057]. A more robust implementation therefore uses a hybrid approach, normalizing by the maximum of the current displacement norm and a reference absolute displacement, $u_{\mathrm{ref}}$, or by adding a small absolute tolerance. For instance:
    $$
    \frac{\lVert \Delta \mathbf{u}^{(k)} \rVert}{\max(\lVert \mathbf{u}^{(k+1)} \rVert, u_{\mathrm{ref}})} \le \varepsilon_u
    $$

*   **Normalized Energy Criterion:** The residual work is normalized by a characteristic energy or work term. A logical choice is the work done by the external load increment, or the change in total internal energy during the increment.
    $$
    \frac{|(\mathbf{r}^{(k)})^T \Delta \mathbf{u}^{(k)}|}{|\Delta W_{\mathrm{ext}} - \Delta U_{\mathrm{int}}|} \le \varepsilon_E
    $$
    Careful definition of the reference work is crucial, especially in dissipative systems, as we will see later.

### Theoretical Underpinnings: The Ideal Case of Linear Elasticity

The use of three different criteria might seem redundant. However, their relationship is deeply rooted in the mathematical structure of the finite element problem. In the ideal case of a linear elastic system discretized with a shape-regular mesh family, the theory of numerical analysis provides a powerful justification. For such problems, the discrete operator (the stiffness matrix $\mathbf{K}$) is symmetric positive definite, and the underlying bilinear form is both **coercive** and **continuous** with mesh-independent bounds [@problem_id:3511113].

Under these conditions, it can be proven that the energy norm of the error, the natural norm of the displacement error (the $H^1$-norm), and the dual norm of the residual are all equivalent. This means that each can be bounded above and below by the others, with constants that do not degrade as the mesh is refined. In this ideal setting, driving any one of these norms to zero guarantees that the others also go to zero. This provides the theoretical foundation for why each of the three practical criteria is a valid measure of proximity to the true solution.

### Advanced Geomechanics: Complications and Nuances

Realistic geomechanical models rarely fit the ideal linear elastic template. Material nonlinearity, path dependency, and softening introduce complexities that require a more sophisticated interpretation of convergence criteria.

#### Convexity, Uniqueness, and Stability

For hyperelastic materials where a total potential energy functional $\Pi(\mathbf{u})$ can be defined, the shape of this functional governs the solution's behavior. If the material model and boundary conditions lead to a **strictly convex** $\Pi(\mathbf{u})$ (typical of hardening materials), the problem has a unique, stable equilibrium solution that corresponds to the global minimum of $\Pi$. In this case, an iterative solver that monotonically decreases the residual norm $\lVert \mathbf{r} \rVert = \lVert \nabla \Pi \rVert$ is guaranteed to be approaching this unique solution [@problem_id:3511074].

However, in post-peak analysis involving material softening, the potential energy functional becomes **non-convex**. It may possess multiple stationary points, including local minima and unstable saddle points. Here, a small residual norm only guarantees that the solver has found a stationary point ($\nabla \Pi = \mathbf{0}$), but it does not tell us if this point is a stable equilibrium (a minimum) or an unstable one (a saddle point). An energy criterion must also be interpreted carefully, as a line search may find a path of decreasing energy that leads toward a saddle point [@problem_id:3511074]. This loss of uniqueness and guaranteed stability makes convergence assessment far more challenging.

#### Global versus Local Convergence in Plasticity

Elastoplasticity introduces a two-level structure to the problem [@problem_id:3511082].
1.  **Global Level:** The solver seeks to satisfy structural equilibrium, i.e., $\mathbf{r}(\mathbf{u}) = \mathbf{0}$.
2.  **Local Level:** At each integration point, a constitutive routine (the "return mapping algorithm") must ensure the computed stress state satisfies the material's yield condition and flow rule (e.g., $\phi(\boldsymbol{\sigma}, \alpha) \le 0$).

These two levels of convergence are distinct and both must be satisfied. It is possible to achieve a small global residual $\lVert \mathbf{r} \rVert$ using stresses that are physically inadmissible (i.e., they lie outside the yield surface, a phenomenon known as "yield surface drift"). This violates the constitutive law and leads to incorrect predictions of plastic deformation and energy dissipation. Conversely, satisfying the local constitutive law at every point for a given displacement field $\mathbf{u}^{(k)}$ does not guarantee that this field is the one that satisfies global equilibrium. A correct solution must satisfy both global force balance and local material laws simultaneously. Therefore, both global convergence criteria (force, displacement, energy) and the tolerance of the local constitutive solver must be controlled [@problem_id:3511082] [@problem_id:3511074].

#### The Challenge of Non-Associated Plasticity

Many geomaterials, such as soils and rocks, are best described by **non-associated** plasticity models, where the plastic flow rule is derived from a plastic potential $g$ that is different from the yield function $f$. This has a profound consequence for the numerical algorithm: the consistent tangent stiffness matrix $\mathbf{K}_t$ becomes **non-symmetric** [@problem_id:3511144].

A non-symmetric tangent matrix means that the discrete system of equations is no longer the gradient of a scalar potential functional. The variational structure is lost. As a result, energy-based criteria lose their rigorous theoretical foundation. There is no guarantee that any energy-like measure will decrease monotonically during the Newton iterations. While the work of the residual, $(\mathbf{r}^{(k)})^T \Delta \mathbf{u}^{(k)}$, can still be monitored, it must be interpreted with extreme caution, as it may oscillate or behave erratically. In these common and important cases, the force and displacement criteria remain the most reliable and indispensable indicators of convergence.

### Synthesis: A Robust, Composite Strategy

Given the complexities of geomechanical analysis, relying on a single convergence criterion is fraught with risk. Best practice demands a **composite stopping rule** that requires the simultaneous satisfaction of force, displacement, and energy criteria (a logical 'AND' condition) [@problem_id:3511077]. This ensures that:
1.  The physical principle of equilibrium is met (force check).
2.  The numerical solution has stabilized (displacement check).
3.  The global error, integrated over the step, is negligible (energy check).

For the most challenging problems involving non-associated flow, contact, and softening, even this is not enough. An intelligent solver should employ an **adaptive policy**. Such a policy monitors not just the convergence status but the *quality* of convergence, using metrics like the rate of residual decay. If convergence is fast and stable, tolerances can be tightened for the next step to improve accuracy. If convergence is slow, oscillatory, or if signs of material instability are detected (e.g., from the tangent matrix), the solver should react by relaxing tolerances and, more importantly, reducing the size of the load increment to navigate the difficult nonlinear path more carefully [@problem_id:3511077]. This combination of a multi-faceted composite criterion and an adaptive solution strategy is the hallmark of a robust and reliable computational geomechanics simulation.