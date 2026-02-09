## Introduction
Accurate dynamic models are essential for the design, control, and optimization of modern energy systems. However, the components that constitute these systems—from heat pumps and power inverters to fuel cells and wind turbines—are fundamentally governed by nonlinear physical principles. While linear models offer simplicity, they are merely local approximations and fail to capture the complex behavior of these components across their full operating range. This knowledge gap necessitates the use of nonlinear system identification: the art and science of building mathematical models of dynamical systems from observed input-output data.

This article provides a comprehensive guide to this critical field. The first chapter, "Principles and Mechanisms," lays the theoretical foundation, exploring the physical origins of nonlinearity and the core concepts of identification, from model structures to optimization challenges. The second chapter, "Applications and Interdisciplinary Connections," demonstrates how these principles are applied to real-world energy components, showcasing a range of case studies. Finally, the "Hands-On Practices" section will allow you to apply these techniques to solve practical engineering problems. We begin by delving into the fundamental reasons why energy systems are nonlinear and the mathematical frameworks used to describe and identify them.

## Principles and Mechanisms

The behavior of energy system components is fundamentally governed by the laws of physics, particularly thermodynamics, fluid mechanics, and heat transfer. These first-principles relationships are seldom linear. Material properties, such as the resistance of a conductor or the enthalpy of a fluid, change with temperature and pressure. Heat transfer mechanisms, like radiation, are inherently nonlinear. Fluid flow can transition between laminar and turbulent regimes, altering system dynamics. Consequently, high-fidelity models of energy components are almost always nonlinear. This chapter elucidates the core principles for modeling these nonlinearities and the mechanisms by which their parameters can be identified from experimental data.

### The Physical Origins of Nonlinearity in Energy Systems

A mathematical model of an energy component typically begins with the application of conservation laws—conservation of mass, momentum, and energy—to a defined control volume. The resulting differential and algebraic equations are nonlinear due to the underlying physical phenomena.

Consider, for instance, a simple thermal model of a power electronic module [@problem_id:4108742]. Its temperature $T$ evolves according to the energy balance:
$$
C \frac{dT}{dt} = \text{Heat Generated} - \text{Heat Lost}
$$
The heat generated is due to Joule heating, given by $I^2 R(T)$, where $I$ is the current and $R(T)$ is the electrical resistance. The heat lost to the environment can be modeled using Newton's law of cooling, $h(T-T_a)$, where $T_a$ is the ambient temperature. A key nonlinearity arises because the resistance of semiconductor materials is temperature-dependent, often approximated by a linear relationship $R(T) = R_0(1 + \alpha(T - T_a))$. Substituting these into the energy balance yields a nonlinear ordinary differential equation:
$$
C \frac{dT}{dt} = I^2 R_0(1 + \alpha(T - T_a)) - h(T - T_a)
$$
Here, the state variable $T$ is multiplied by the input squared, $I^2$, creating a nonlinear dependence on both state and input.

The complexity escalates in components involving phase change, such as a drum boiler in a power plant [@problem_id:4108764]. The total energy $E$ stored in the drum is the sum of the energy of the liquid water and steam phases: $E = m_w h_w + m_s h_s$. The masses ($m_w, m_s$) and specific enthalpies ($h_w, h_s$) are strongly nonlinear functions of temperature $T$ and pressure $P$. Furthermore, the overall heat transfer coefficient $U$ from the hot flue gas to the water is not a constant; it depends on flow rates and the heat transfer regimes (e.g., nucleate boiling), which vary with the operating point (load). The resulting energy balance is a highly nonlinear function of the system's states and inputs. These physical realities necessitate the use of nonlinear models for accurate representation across a component's operating range.

### Linearization as a Local Approximation

While energy systems are inherently nonlinear, their behavior over a small range of operation can often be approximated by a linear model. This technique, known as **equilibrium linearization**, is a cornerstone of classical control theory. It involves approximating a nonlinear system with a linear one at a specific steady-state **operating point**.

Consider a general nonlinear state-space model with state vector $x$, input vector $u$, and output vector $y$:
$$
\dot{x} = f(x, u, \theta)
$$
$$
y = g(x, u, \theta)
$$
where $\theta$ is a vector of model parameters. An equilibrium point $(x^\star, u^\star)$ is a point where the state is constant for a constant input, i.e., $f(x^\star, u^\star, \theta) = 0$. By performing a first-order Taylor series expansion of $f$ and $g$ around this point, we obtain a Linear Time-Invariant (LTI) approximation for small perturbations $\delta x = x - x^\star$, $\delta u = u - u^\star$, and $\delta y = y - y^\star$:
$$
\delta \dot{x} = A \delta x + B \delta u
$$
$$
\delta y = C \delta x + D \delta u
$$
The matrices $A, B, C,$ and $D$ are the Jacobians of the nonlinear functions evaluated at the equilibrium point:
$$
A = \frac{\partial f}{\partial x}\bigg|_{(x^\star, u^\star)}, \quad B = \frac{\partial f}{\partial u}\bigg|_{(x^\star, u^\star)}, \quad C = \frac{\partial g}{\partial x}\bigg|_{(x^\star, u^\star)}, \quad D = \frac{\partial g}{\partial u}\bigg|_{(x^\star, u^\star)}
$$
As a concrete example, returning to the thermal module from [@problem_id:4108742], we can compute these Jacobian matrices. For a given operating current $I^\star$, we first find the equilibrium temperature $T^\star$ by solving $\dot{T}=0$. The linearized dynamics are then described by the scalar coefficients $A = \frac{\partial f}{\partial T}|_{(T^\star, I^\star)}$ and $B = \frac{\partial f}{\partial I}|_{(T^\star, I^\star)}$, and the linearized output equation by $C = \frac{\partial g}{\partial T}|_{(T^\star, I^\star)}$ and $D = \frac{\partial g}{\partial I}|_{(T^\star, I^\star)}$. This LTI model is valid for control design as long as the system operates in a small neighborhood of $(T^\star, I^\star)$, where the neglected higher-order terms of the Taylor expansion are small and the system's local controllability and observability properties (which depend on $B$ and $C$ being non-zero) hold.

The primary limitation of this approach is that the resulting LTI model is only a local snapshot. The matrices $A, B, C, D$ are functions of the operating point $(x^\star, u^\star)$. As the system moves to a different operating point (e.g., a higher load), these matrices change, and so do the system's dynamic characteristics, such as its time constants and gains [@problem_id:4108764]. In the boiler example, operating at high load versus low load leads to different fluid densities, mass inventories, and heat transfer coefficients, resulting in a significantly different local time constant for the drum temperature. A single LTI model is therefore inadequate to describe the boiler's behavior across its full load range. This operating-point dependency is the hallmark of nonlinearity and motivates more advanced modeling techniques like gain-scheduling or the identification of global nonlinear models.

### A Taxonomy of Nonlinear Behaviors

When approaching a system from a data-driven or "grey-box" perspective, it is useful to classify nonlinearities based on their mathematical properties, as this informs the choice of model structure and identification strategy.

#### Static versus Dynamic Nonlinearities

The most fundamental distinction is based on the concept of memory.

A **static nonlinearity** is memoryless. Its output at any given time $t$ is an instantaneous function of its input at that same time, i.e., $z(t) = f(u(t))$. Such a nonlinearity does not possess internal states that evolve over time. A classic example in energy systems is the saturation of an actuator [@problem_id:4108716]. In a variable-speed heat pump, the command signal $u(t)$ to the compressor results in a refrigerant mass flow rate. Due to physical limits of the motor or power electronics, this mass flow rate will saturate at a maximum value, no matter how large the command signal becomes. This relationship can be modeled by a static saturation function.

In contrast, a **dynamic nonlinearity** possesses memory. Its output depends not just on the current input but on the history of inputs. This memory is embodied by internal state variables that evolve according to differential equations. The refrigerant circuit of the heat pump provides a perfect example [@problem_id:4108716]. The evaporator and condenser are control volumes with finite inventories of refrigerant. The mass and energy stored within these components are state variables governed by the dynamic conservation laws:
$$
\frac{d}{dt}m_{cv}(t) = \sum \dot{m}_{in}(t) - \sum \dot{m}_{out}(t)
$$
$$
\frac{d}{dt}U_{cv}(t) = \dot{Q}(t) - \dot{W}(t) + \sum (\dot{m}h)_{in}(t) - \sum (\dot{m}h)_{out}(t)
$$
Because these governing equations involve time derivatives, they introduce time constants and lags into the system's response. The nonlinearity is dynamic because the relationships themselves (e.g., thermophysical properties like enthalpy $h$ as functions of state) are nonlinear.

#### Smooth versus Nonsmooth Nonlinearities

Nonlinearities can also be classified by their differentiability.

A **smooth nonlinearity** is a function that is continuously differentiable over its operating range. Examples include polynomial efficiency curves for pumps or turbines, or the exponential dependence of reaction rates on temperature in a chemical process like a fuel cell. These are often modeled using polynomials, splines, or neural networks [@problem_id:4108778].

A **nonsmooth nonlinearity** contains discontinuities or "kinks" in its function or its derivative. Common examples in energy components include:
*   **Deadzone**: A region of input for which there is no change in output. For example, a valve may require a minimum pressure command before it begins to open, or a pump may have a stiction-related deadzone at zero speed [@problem_id:4108778].
*   **Hysteresis**: A rate-independent memory effect where the output depends on the direction of input change. This is common in mechanical systems with backlash or in magnetic materials. This path-dependence means the output is not a unique function of the instantaneous input, but depends on its history [@problem_id:4108778].

The distinction between smooth and nonsmooth nonlinearities is critical for system identification, as they require different types of input signals to be properly characterized, a topic we will return to later.

### Common Structures for Nonlinear Models

To capture the diverse nonlinear behaviors observed in energy systems, system identification practice employs several standard model structures. These structures provide a framework for combining linear dynamics with static nonlinear functions.

#### Block-Oriented Models

Block-oriented models represent a system as an interconnection of LTI dynamic blocks and static nonlinear blocks. They are particularly effective when the physical system has a clear separation between dynamic and nonlinear phenomena.

The **Hammerstein model** consists of a static input nonlinearity followed by an LTI dynamic block [@problem_id:4108716]. Its structure is:
$$
v(t) = g_{in}(u(t))
$$
$$
y(t) = (h * v)(t) + n(t)
$$
where $g_{in}(\cdot)$ is a static nonlinear function, $h(t)$ is the impulse response of the LTI system, $*$ denotes convolution, and $n(t)$ is noise. This structure is physically motivated when an actuator nonlinearity precedes the main plant dynamics. For example, in a grid-tied inverter, the command signal is subject to saturation by the power electronics ($g_{in}$) before this limited voltage is applied to the linear dynamics of the output filter and grid impedance ($h$) [@problem_id:4108748].

The **Wiener model** reverses this order, with an LTI block followed by a static output nonlinearity. This is appropriate for modeling sensor nonlinearities, where the physical process is linear but the measurement device is not. The more general **Hammerstein-Wiener (HW)** model sandwiches an LTI block between two static nonlinearities (input and output). The HW structure can be a parsimonious choice if the dominant physics can be approximated this way, for example, modeling a fuel cell where static nonlinear polarization curves ($g_{in}, g_{out}$) bracket the linear dynamics of double-layer charging and mass transport ($h$) [@problem_id:4108690].

#### NARX Models

The **Nonlinear AutoRegressive with eXogenous input (NARX)** model is a highly flexible structure that represents the current output as a nonlinear function of past outputs and past inputs. In discrete time, a general NARX model has the form:
$$
y(k) = f\big(y(k-1), \dots, y(k-n_y), u(k), \dots, u(k-n_u)\big) + \varepsilon(k)
$$
where $f(\cdot)$ is a static nonlinear function (e.g., a polynomial or a neural network), $n_y$ and $n_u$ are the orders of the model, and $\varepsilon(k)$ is an innovation term [@problem_id:4108690]. The term $u(k)$ can be included, as dependence on the current input is causal in discrete-time systems.

NARX models are powerful general-purpose approximators. However, they typically offer less physical insight compared to a grey-box or block-oriented model. The single function $f(\cdot)$ combines all static and dynamic effects, making it difficult to interpret its parameters in physical terms. Furthermore, because NARX models use past measured outputs as inputs (regressors), they can suffer from biased parameter estimates when the output measurements are noisy, a problem known as "errors-in-variables" [@problem_id:4108690]. In contrast, a block-oriented model like the Hammerstein-Wiener structure simulates by propagating the clean input $u(k)$ through its internal states, avoiding this direct feedback of measurement noise.

### Principles of Nonlinear Identification

Identifying a nonlinear model involves two primary challenges: ensuring the model parameters are uniquely determinable from the data (identifiability) and solving the often-nonconvex optimization problem to find the best parameter values.

#### Structural Identifiability

Before conducting any experiment, a fundamental theoretical question must be asked: is it possible, even with perfect, noise-free data, to uniquely determine the values of the model parameters? This is the question of **structural identifiability**.

A parameter vector $\theta$ is structurally identifiable if the mapping from the parameters to the noise-free output is injective. That is, for any two distinct parameter vectors $\theta_1 \neq \theta_2$, they must produce distinct outputs, $y(t, \theta_1) \neq y(t, \theta_2)$, for some admissible input $u(t)$ [@problem_id:4108686]. If different parameter sets can produce the exact same input-output behavior, the parameters are structurally unidentifiable.

A common cause of unidentifiability is the algebraic confounding of parameters. Consider a thermal model with heat loss due to both convection and radiation:
$$
C(T)\,\dot{T} = q_{in} - h\,A\,(T-T_a) - \epsilon\,\sigma\,A\,(T^4 - T_a^4)
$$
Here, the unknown parameters are the convective coefficient $h$, the surface area $A$, and the emissivity $\epsilon$. However, they only appear in the model as the products $hA$ and $\epsilon A$. Any combination of individual values that keeps these products constant will yield the exact same temperature response $T(t)$. For instance, doubling $A$ and halving both $h$ and $\epsilon$ results in an observationally equivalent model. Therefore, the individual parameters $h, A,$ and $\epsilon$ are structurally unidentifiable; only the composite parameters $hA$ and $\epsilon A$ can be determined from input-output data [@problem_id:4108686]. This is an intrinsic property of the model structure that cannot be fixed by better data or more sophisticated algorithms.

#### The Role of Input Design and Persistent Excitation

Assuming a model is structurally identifiable, a second condition is required for practical identification: the experimental data must be sufficiently informative. The design of the input signal $u(t)$ is crucial for this. The input must "excite" all the relevant dynamics and nonlinearities of the system.

For models that are linear in their parameters, such as a polynomial NARX model, $y(k) \approx \phi^{\top}(k)\theta$, the least-squares estimate of $\theta$ is given by $\hat{\theta} = (X^{\top}X)^{-1}X^{\top}Y$, where $X$ is the matrix of regressors $\phi(k)$ stacked over time. A unique solution exists only if the Gram matrix $X^{\top}X$ is invertible. This requires the columns of $X$—the time series of each regressor—to be linearly independent.

The property of an input signal that ensures this condition is called **persistent excitation (PE)**. An input signal is persistently exciting of order $n$ if it can guarantee the linear independence of $n$ such regressors. For linear systems, this is equivalent to the input signal having at least $n/2$ distinct frequency components. For nonlinear systems, the situation is more complex, but the principle remains: the input must be rich enough to prevent the regressors from becoming linearly dependent [@problem_id:4108761]. A single sinusoid, for example, generates a highly structured set of harmonics and is often insufficient to identify a complex NARX model. A **multisine** input, composed of several sinusoids at carefully chosen frequencies, provides a much richer excitation and is a standard choice for nonlinear system identification [@problem_id:4108761].

The nature of the nonlinearity also dictates the required input. To identify a smooth polynomial, a broadband PE signal is effective. However, to identify nonsmooth features, the input must specifically probe them. To identify a deadzone, the input must cross the deadzone's threshold. To identify hysteresis, the input must contain reversals in direction to trace out both branches of the hysteresis loop [@problem_id:4108778].

#### The Challenge of Nonconvex Optimization

Most nonlinear identification problems, especially those involving grey-box models derived from physics, result in a nonlinear least-squares problem:
$$
\min_{\theta} J(\theta) = \sum_{i=1}^{N} \| y_i - \hat{y}_i(\theta) \|_W^2
$$
where $\hat{y}_i(\theta)$ is the model prediction. Unlike linear least-squares, this objective function $J(\theta)$ is generally **nonconvex**. This is because the model predictions $\hat{y}_i(\theta)$ are complex, nonlinear functions of the parameters $\theta$. For example, in a detailed heat pump model, parameters may appear in denominators (like $UA$ or efficiency $\eta_{comp}$), in products ($D/\eta_{comp}$), or within exponential functions (Clausius-Clapeyron relation), all of which destroy convexity [@problem_id:4108729].

A nonconvex function can have multiple local minima. Gradient-based optimization algorithms (like Gauss-Newton or Levenberg-Marquardt) are only guaranteed to find a local minimum, not the global one. Starting the optimization from a poor initial guess can lead to convergence to a physically meaningless set of parameters.

Several strategies are employed to mitigate this risk:
1.  **Physics-Informed Initialization**: Use physical knowledge, design specifications, or manufacturer data to make an educated initial guess $\theta_0$ that is likely close to the true solution [@problem_id:4108729].
2.  **Multi-Start Optimization**: Run the local optimization algorithm from many different, often randomly chosen, starting points. The best of the resulting local minima is then taken as the solution. This increases the probability of finding the global minimum [@problem_id:4108729].
3.  **Continuation or Homotopy Methods**: Instead of solving the hard problem directly, solve a sequence of easier problems that gradually "morph" into the final problem. For instance, one could first identify parameters using data from a low-power operating regime and use that solution as the starting point for an optimization over a wider regime [@problem_id:4108729].

### Physics-Informed Modeling: The Grey-Box Approach

The challenges of nonlinear identification underscore the value of the **grey-box** modeling paradigm, which stands between purely physics-driven "white-box" models and purely data-driven "black-box" models. A grey-box model has a structure derived from physical principles, but contains unknown parameters that are estimated from data.

The key advantage of this approach is the ability to embed fundamental physical laws as constraints, ensuring the identified model is not just a statistical fit but a physically consistent representation. For example, when modeling any thermal component, the First Law of Thermodynamics must hold [@problem_id:4108721]. This conservation law,
$$
\frac{dU}{dt} = \dot{Q}_{net} + \sum (\dot{m}h)_{in} - \sum (\dot{m}h)_{out}
$$
can be embedded in the identification problem in several ways:
*   As a hard equality constraint in the optimization problem, forcing the change in the model's stored energy to exactly match the net energy flows over each time step.
*   By structuring the model itself to be conservative by construction. For example, using a **Port-Hamiltonian** framework, where the change in the storage function (energy) is explicitly defined as the sum of power flows through ports, guarantees energy conservation for any parameter values [@problem_id:4108721].

By building physical knowledge into the model structure and identification process, we constrain the solution space, improve the physical interpretability of the results, enhance the model's ability to extrapolate beyond the training data, and often regularize the optimization problem, making it better-conditioned and easier to solve.