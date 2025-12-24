## Introduction
The ability to quantitatively describe and predict the behavior of living organisms is a central goal of modern biomedical science. At the heart of this endeavor lie the fundamental conservation laws of physics—the principles governing the balance of mass, charge, and energy. These laws provide the unyielding mathematical foundation required to translate complex biological phenomena into rigorous, mechanistic models. This article addresses the critical step of moving beyond qualitative description to quantitative prediction by elucidating how these universal principles are applied to physiological systems. The reader will gain a comprehensive understanding of this framework, starting with the core mathematical formulations, progressing to their practical application, and culminating in hands-on problem-solving.

The journey begins in the **Principles and Mechanisms** chapter, where we will derive the governing equations from first principles, including the integral Reynolds Transport Theorem and its application to both macroscopic [compartmental models](@entry_id:185959) (ODEs) and microscopic [continuum models](@entry_id:190374) (PDEs). Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate how these mathematical tools are used to build powerful models in diverse fields such as pharmacokinetics, [electrophysiology](@entry_id:156731), and [thermoregulation](@entry_id:147336). Finally, the **Hands-On Practices** section will offer a chance to solidify this knowledge by applying these conservation principles to solve concrete problems in [physiological modeling](@entry_id:1129671).

## Principles and Mechanisms

The conservation of mass, charge, and energy provides the unyielding foundation upon which quantitative models of physiological systems are built. These laws, which state that a given conserved quantity can be neither created nor destroyed, allow us to formulate precise mathematical balances that govern the dynamics of biological processes. This chapter delineates the core principles of conservation and explores the primary mechanisms through which these principles are expressed in [physiological modeling](@entry_id:1129671), from macroscopic compartments to the microscopic continuum, and finally to their numerical implementation.

### The Foundational Principle: Integral Conservation Laws

The most general statement of conservation is formulated over a finite region of space, known as a **control volume (CV)**. For any extensive property $B$ (such as mass, moles of a solute, or energy) with a corresponding volumetric density $\beta$, the fundamental balance within a control volume $\Omega(t)$ is:

*The time rate of accumulation of $B$ within $\Omega(t)$ equals the net rate at which $B$ flows into $\Omega(t)$ across its boundary $\partial\Omega(t)$, plus the net rate at which $B$ is generated within $\Omega(t)$.*

The mathematical expression of this statement depends critically on whether the control volume itself is fixed, deforming, or moving in space. The **Reynolds Transport Theorem (RTT)** provides a universal framework for relating the total rate of change of the integral of a property to integrals of its local behavior.

#### The General Case: Moving and Deforming Control Volumes

Consider a general scenario where the control volume $\Omega(t)$ is itself moving and deforming, with its boundary $\partial\Omega(t)$ moving at a velocity $\mathbf{u}_b(\mathbf{x},t)$. The material carrying the property $\beta$ moves with its own velocity field, $\mathbf{v}(\mathbf{x},t)$. The flux of the property across the boundary is driven by the velocity of the material *relative* to the boundary, which is $(\mathbf{v} - \mathbf{u}_b)$.

Let $s_\beta$ be the volumetric source rate of $\beta$. The [integral conservation law](@entry_id:175062) is then given by:
$$ \frac{d}{dt}\int_{\Omega(t)} \beta\,dV = -\int_{\partial\Omega(t)} \beta\,(\mathbf{v}-\mathbf{u}_b)\cdot\mathbf{n}\,dS + \int_{\Omega(t)} s_\beta\,dV $$
Here, $\mathbf{n}$ is the outward-pointing unit normal on the boundary, and the negative sign on the [surface integral](@entry_id:275394) reflects the convention that a net outward flux (positive integral) causes a decrease in the total amount of $\beta$ within the volume.

A pertinent physiological example is the modeling of a single lung alveolus during respiration ``. The alveolar wall moves due to breathing, so its velocity is $\mathbf{u}_b$. The air inside, with density $\beta$, moves with its own velocity field $\mathbf{v}$. The above equation correctly balances the change in air mass within the deforming alveolus with the convective flow of air relative to the moving wall (predominantly at the mouth of the alveolus, where it connects to the bronchial tree) and any sources or sinks (e.g., mass exchange of specific gases like oxygen or carbon dioxide).

#### A Special Case: Material Control Volumes

A particularly important case is the **material control volume**, which is defined as a volume that deforms and moves with the underlying material itself. In this case, the boundary velocity is identical to the material velocity at the boundary, i.e., $\mathbf{u}_b = \mathbf{v}$. Substituting this into the general RTT and applying the [divergence theorem](@entry_id:145271) yields a powerful alternative formulation:
$$ \frac{d}{dt}\int_{\Omega(t)}\beta\,dV = \int_{\Omega(t)}\left(\frac{D\beta}{Dt}+\beta\,\nabla\cdot\mathbf{v}\right)\,dV $$
Here, $\frac{D\beta}{Dt}$ is the **[material derivative](@entry_id:266939)** (or [total derivative](@entry_id:137587)), defined as $\frac{D\beta}{Dt} = \frac{\partial \beta}{\partial t}+\mathbf{v}\cdot\nabla\beta$. It represents the rate of change of the density $\beta$ experienced by an observer moving with a material particle.

This form of the RTT provides a profound insight: the change in the total property $B$ within a material volume is the sum of two effects integrated over that volume ``. The first term, $\int \frac{D\beta}{Dt} dV$, accounts for the change in the property density of the constituent material particles. The second term, $\int \beta(\nabla\cdot\mathbf{v}) dV$, accounts for the change in total property due to the expansion ($\nabla\cdot\mathbf{v} > 0$) or compression ($\nabla\cdot\mathbf{v}  0$) of the material volume itself. This formulation is indispensable in biomechanics, for example, when modeling the transport of metabolites or the change in energy content within a deforming region of myocardial tissue.

#### The Simplest Case: Fixed Control Volumes

For many [physiological modeling](@entry_id:1129671) problems, it is sufficient to consider a **fixed control volume**, where $\mathbf{u}_b = \mathbf{0}$. In this case, the general RTT simplifies to:
$$ \frac{d}{dt}\int_{\Omega} \beta\,dV + \int_{\partial\Omega} \beta\,\mathbf{v}\cdot\mathbf{n}\,dS = \int_{\Omega} s_\beta\,dV $$
This equation states that the rate of change of the total property in a fixed volume plus the net rate of outflow across its boundary must equal the total rate of generation within the volume. This is the starting point for developing both macroscopic compartment models and microscopic continuum models.

### Macroscopic Application: Compartmental Models

Compartmental models simplify physiological systems by lumping spatially distributed properties into a set of discrete, homogeneous compartments. The governing equations for these models are [ordinary differential equations](@entry_id:147024) (ODEs) derived directly from the [integral conservation law](@entry_id:175062).

#### The Well-Stirred Compartment

The most common building block is the **well-stirred compartment**, which is modeled as a fixed control volume wherein the concentration $C$ (the density of a solute) is assumed to be spatially uniform. The integral conservation law for the total mass of the solute, $M = V C$, in a compartment of volume $V$, becomes an ODE.

A crucial subtlety arises when the volume of the compartment, $V(t)$, is also a function of time, as can occur during intravenous infusion or [dehydration](@entry_id:908967). The accumulation term is the derivative of the total mass, which, by the product rule, is $\frac{dM}{dt} = \frac{d(V C)}{dt}$. The full mass balance for a solute in a plasma compartment with volumetric inflow $Q_{in}$ at concentration $C_{in}$, outflow $Q_{out}$, and a net transcompartmental exchange flux $J_{pi}$ is therefore ``:
$$ \frac{d}{dt}\big(V_p(t)\,C_p(t)\big) = Q_{in}(t)\,C_{in}(t) - Q_{out}(t)\,C_p(t) + J_{pi}(t) $$
The term on the left represents the rate of mass **storage**. On the right, $Q_{in}C_{in}$ is the mass **inflow**, $-Q_{out}C_p$ is the mass **outflow** (where the outflow concentration equals the internal concentration $C_p$ due to the [well-mixed assumption](@entry_id:200134)), and $J_{pi}$ is a general **exchange** term. Mistaking the storage term for $V_p \frac{dC_p}{dt}$ is a common error that violates mass conservation when volume changes.

#### Species Conservation and Fick's Principle

The compartmental approach can be applied to a specific chemical species. A classic example is the conservation of oxygen across an organ. Modeling the organ as a control volume with arterial inflow and venous outflow, we can write a balance for oxygen ``. At **steady state**, all time derivatives are zero, and any storage of oxygen within the tissue, $S_{O_2}$, is constant. If there is no other source of oxygen, the balance dictates that the rate of metabolic oxygen consumption, $\dot{V}_{O_2}$, must be exactly equal to the rate at which oxygen is extracted from the blood. This gives rise to the celebrated **Fick's principle**:
$$ \dot{V}_{O_2} = Q (C_{aO_2} - C_{vO_2}) $$
where $Q$ is blood flow rate and $C_{aO_2}$ and $C_{vO_2}$ are the arterial and venous oxygen contents, respectively.

Under **transient** conditions, such as the onset of exercise, this simple relationship does not hold. The rate of oxygen extraction from blood must balance both metabolic consumption and any changes in tissue oxygen stores:
$$ Q (C_{aO_2} - C_{vO_2}) = \dot{V}_{O_2} + \frac{dS_{O_2}}{dt} $$
During oxygen uptake, when $\frac{dS_{O_2}}{dt} > 0$, the measured arteriovenous difference overestimates the true [metabolic rate](@entry_id:140565). This highlights the importance of distinguishing steady-state from transient assumptions. Furthermore, one must use correct **[constitutive relations](@entry_id:186508)**. The relationship between total oxygen content and the [partial pressure of oxygen](@entry_id:156149) ($P_{O_2}$) is highly nonlinear due to hemoglobin binding, so one cannot simply substitute [partial pressures](@entry_id:168927) for contents in Fick's principle ``.

#### Conservation in Reaction Networks: Stoichiometric Modeling

Conservation laws can also be applied to systems without spatial extent, such as metabolic networks within a cell. Here, the "flow" is the flux through chemical reactions. For a network involving a set of internal metabolites, we can write a mass balance equation for each one. The rate of change of the amount of a metabolite is the sum of the fluxes of all reactions that produce it, minus the sum of the fluxes of all reactions that consume it.

This system of balance equations can be elegantly organized using the **stoichiometric matrix**, $\mathbf{S}$ ``. By convention, the rows of $\mathbf{S}$ correspond to metabolites and the columns correspond to reactions. An entry $S_{ij}$ is the [stoichiometric coefficient](@entry_id:204082) of metabolite $i$ in reaction $j$, with a positive sign for production and a negative sign for consumption. If $\mathbf{n}$ is the vector of metabolite amounts and $\mathbf{v}$ is the vector of reaction fluxes, the entire [system dynamics](@entry_id:136288) are captured by:
$$ \frac{d\mathbf{n}}{dt} = \mathbf{S} \mathbf{v} $$
In many systems biology applications, such as Flux Balance Analysis (FBA), internal metabolites are assumed to be at a **steady state**, meaning their concentrations are constant. This implies $\frac{d\mathbf{n}}{dt} = \mathbf{0}$, which imposes a powerful constraint on the possible reaction fluxes:
$$ \mathbf{S} \mathbf{v} = \mathbf{0} $$
This equation signifies that at steady state, the weighted sum of reaction fluxes that produce any given internal metabolite must exactly balance the weighted sum of fluxes that consume it. This [steady-state assumption](@entry_id:269399) applies only to internal species, as the cell is an [open system](@entry_id:140185) exchanging matter with its environment.

### Microscopic Application: Continuum Models (PDEs)

While compartment models are powerful, their core assumption of spatial homogeneity can be a significant limitation. When concentration gradients within a tissue are important, we must turn to continuum models, which describe properties as fields that vary continuously in space and time. These models take the form of partial differential equations (PDEs) derived from the local form of the conservation laws.

The well-stirred assumption fails when the underlying physics predicts spatial gradients that the assumption artificially removes ``. For instance, in a tissue with a spatially heterogeneous source of a solute, $r(x)$, local mass conservation requires a corresponding divergence of flux to maintain balance. The well-stirred assumption forces the flux divergence to zero, creating a physical contradiction unless the source term is also uniform. The significance of these gradients is often characterized by dimensionless quantities like the Péclet number (comparing advection to diffusion) and the Damköhler number (comparing reaction to transport).

#### From Integral to Local Conservation

To derive the [local conservation law](@entry_id:261997), we begin with the integral form for a fixed control volume $\Omega$. By applying the **Divergence Theorem** (or Gauss's Theorem), we can convert the [surface integral](@entry_id:275394) of the flux into a [volume integral](@entry_id:265381) of its divergence:
$$ \int_{\partial\Omega} \mathbf{J} \cdot \mathbf{n}\,dS = \int_{\Omega} \nabla \cdot \mathbf{J} \,dV $$
where $\mathbf{J}$ is the total flux vector. The integral balance $\frac{d}{dt}\int \beta dV = -\int \mathbf{J}\cdot\mathbf{n} dS + \int s_\beta dV$ becomes $\int (\frac{\partial \beta}{\partial t} + \nabla \cdot \mathbf{J} - s_\beta) dV = 0$. Since this must hold for *any* arbitrarily small control volume, the integrand itself must be zero everywhere. This yields the local, or pointwise, conservation law:
$$ \frac{\partial \beta}{\partial t} + \nabla \cdot \mathbf{J} = s_\beta $$
This PDE is the foundation of all continuum transport models. The specific nature of the model is determined by the constitutive expression for the total flux $\mathbf{J}$.

#### The Advection-Diffusion-Reaction Equation

For many solutes in biological tissues, the total flux is the sum of transport by the bulk motion of the fluid (**advection**) and transport by random molecular motion down a concentration gradient (**diffusion**). The advective flux is $\mathbf{J}_{adv} = c \mathbf{v}$, where $c$ is the concentration and $\mathbf{v}$ is the fluid velocity. The [diffusive flux](@entry_id:748422) is given by **Fick's first law**, $\mathbf{J}_{diff} = -D \nabla c$, where $D$ is the diffusion coefficient. The negative sign is critical, indicating that diffusion occurs from high to low concentration.

The total flux is $\mathbf{J} = c\mathbf{v} - D\nabla c$. Substituting this into the [local conservation law](@entry_id:261997) gives the general **Advection-Diffusion-Reaction (ADR) equation** ``:
$$ \frac{\partial c}{\partial t} + \nabla \cdot (c \mathbf{v}) = \nabla \cdot (D \nabla c) + r $$
where $r$ is the net volumetric production rate. The term $\nabla \cdot (c \mathbf{v})$ is the **[conservative form](@entry_id:747710)** of the advection term. It correctly accounts for changes in concentration due to both concentration gradients and fluid compressibility ($\nabla \cdot \mathbf{v} \neq 0$), which can occur in perfused tissue where fluid is exchanged with capillaries. The diffusion coefficient $D$ can be a scalar for isotropic media or a tensor for [anisotropic tissues](@entry_id:1121031) like muscle or brain white matter.

#### Electrodiffusion: The Nernst-Planck Equation

When modeling charged species like ions, we must account for their movement in response to an electric field $\mathbf{E}$. This gives rise to an additional flux component: **electromigration** or **drift**. The drift velocity of an ion is proportional to the electric field, and the resulting flux is $\mathbf{J}_{mig} = c_i \mathbf{v}_{drift}$. Given the drift velocity is $-z_i u_i \nabla \phi$, where $z_i$ is the ion's valence, $u_i$ is its [electrophoretic mobility](@entry_id:199466), and $\phi$ is the electric potential ($\mathbf{E}=-\nabla\phi$), the drift flux becomes $\mathbf{J}_{mig} = -z_i u_i c_i \nabla\phi$.

The total flux for an ionic species $i$ is the sum of all three transport mechanisms:
$$ \mathbf{J}_i = \underbrace{-D_i \nabla c_i}_{\text{Diffusion}} \underbrace{- z_i u_i c_i \nabla \phi}_{\text{Electromigration}} + \underbrace{c_i \mathbf{v}}_{\text{Advection}} $$
Substituting this comprehensive flux expression into the [local conservation law](@entry_id:261997) yields the **Nernst-Planck equation**, a cornerstone of [electrophysiology](@entry_id:156731) and biotransport that governs the concentration field of an ion under the combined influence of chemical gradients, electric fields, and [bulk flow](@entry_id:149773) ``.

### Coupling and Discretization: Bridging Scales and Models

Real physiological systems often involve multiple interacting domains and require numerical methods for their solution. Conservation principles remain paramount in these advanced contexts.

#### Coupling Domains: Interface Jump Conditions

Many biological models involve distinct domains, such as the intracellular and extracellular spaces, separated by a membrane. While the PDE governs transport within each domain, a special condition is needed to couple them at the interface. This condition is itself a statement of mass conservation at the interface.

By considering an infinitesimally thin "pillbox" control volume straddling the interface $\Gamma$, and taking the limit as its thickness goes to zero, we can derive an **interface [jump condition](@entry_id:176163)** ``. Assuming the membrane itself has negligible storage capacity, the law of mass conservation requires that any discontinuity (jump) in the normal component of the mass flux across the interface must be equal to the net rate of transport or reaction occurring *on the interface itself*, denoted $J_{mem}$:
$$ [\mathbf{n} \cdot \mathbf{J}] \equiv (\mathbf{n} \cdot \mathbf{J})_e - (\mathbf{n} \cdot \mathbf{J})_i = J_{mem} $$
where subscripts $e$ and $i$ denote the extracellular and intracellular sides, and $\mathbf{n}$ points from $i$ to $e$. This condition serves as a boundary condition for each domain's PDE, coupling the two problems through the kinetics of [membrane transport](@entry_id:156121) ($J_{mem}$) and ensuring that mass is conserved globally across the entire system.

#### From Continuum to Compartments: The Finite Volume Method

The need to resolve spatial gradients, as discussed earlier, leads to the development of [multi-compartment models](@entry_id:926863). The **Finite Volume Method (FVM)** provides a rigorous framework for creating such models from a continuum PDE, with the crucial feature that it guarantees discrete mass conservation.

The method begins by integrating the governing PDE over each of $N$ non-overlapping control volumes (or "finite volumes") that tessellate the domain. Application of the [divergence theorem](@entry_id:145271) converts the [volume integral](@entry_id:265381) of the flux divergence into a sum of fluxes over the faces of the cell. This yields a semi-discrete balance for each cell $i$:
$$ \frac{d}{dt}(|V_i|\, c_i) + \sum_{f \subset \partial V_i} \widehat{\Phi}_f = |V_i|\, r_i $$
where $c_i$ is the average concentration in cell $i$, and $\widehat{\Phi}_f$ is the numerical approximation of the total flux out of the cell through face $f$.

The key to conservation lies in the definition of the [numerical flux](@entry_id:145174). For any internal face shared by two cells, the scheme enforces that the flux leaving one cell is precisely the flux entering the other. When we sum the balance equations over all cells in the domain, the fluxes across all internal faces cancel out in a "[telescoping sum](@entry_id:262349)" ``. The total rate of change of mass in the entire discrete system is then perfectly balanced by the sum of boundary fluxes and the total integrated source term:
$$ \frac{d}{dt}\sum_{i=1}^{N} |V_i|\, c_i(t) + \sum_{f \subset \partial\Omega} \widehat{\Phi}_f(t) = \sum_{i=1}^{N} |V_i|\, r_i(t) $$
This property of **discrete conservation** is a direct and powerful consequence of the integral formulation. It holds regardless of the mesh geometry (structured or unstructured) and is a property of the [spatial discretization](@entry_id:172158), independent of the subsequent choice of time-stepping scheme. Even complex boundary conditions, such as Dirichlet conditions, can be implemented in a conservative manner by defining the boundary fluxes appropriately, for instance through the use of "[ghost cells](@entry_id:634508)" ``. The FVM thus provides a robust bridge from local continuum laws to globally conservative [multi-compartment models](@entry_id:926863), forming the backbone of many modern physiological simulation platforms.