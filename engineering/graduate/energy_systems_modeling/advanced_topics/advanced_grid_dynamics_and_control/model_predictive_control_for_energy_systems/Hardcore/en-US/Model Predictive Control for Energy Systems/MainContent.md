## Introduction
Modern energy systems are characterized by increasing complexity, driven by intermittent renewables, dynamic pricing, and strict operational constraints. Traditional control strategies often struggle in this environment, lacking the foresight to manage these challenges optimally. Model Predictive Control (MPC) has emerged as a premier advanced control methodology to address this gap, providing a systematic framework for making optimal decisions by using a predictive model to anticipate future conditions and optimize performance. This article offers a comprehensive exploration of MPC, guiding you from core theory to advanced application in the energy sector.

We begin with **Principles and Mechanisms**, where we will dissect the receding horizon framework, break down the anatomy of the optimization problem, and examine fundamental techniques for ensuring stability and handling uncertainty. Next, in **Applications and Interdisciplinary Connections**, we will survey the practical power of MPC, from optimizing building energy and battery storage to coordinating microgrids and providing grid services, highlighting its connections to fields like finance and computer science. Finally, the **Hands-On Practices** chapter will solidify this knowledge through guided problems focused on key implementation steps, such as model derivation and robust controller design. This structured approach will equip you with a deep understanding of how to leverage MPC to solve critical challenges in modern energy systems.

## Principles and Mechanisms

Model Predictive Control (MPC) represents a paradigm shift from traditional control strategies. Instead of relying on a fixed, pre-computed control law, MPC repeatedly solves an explicit, finite-horizon optimal control problem online, using the current state of the system as the initial condition. This chapter delineates the fundamental principles and mechanisms that underpin the efficacy of MPC, particularly in the context of complex energy systems. We will explore its core receding horizon framework, the formulation of its central optimization problem, its methods for handling uncertainty and constraints, and the computational structures that enable its real-time application.

### The Receding Horizon Principle: Optimal Control with Feedback

At the heart of MPC lies the **receding horizon principle**, a strategy that elegantly transforms a finite-horizon open-loop optimization into a powerful closed-loop feedback controller. To appreciate this, let us first consider a basic finite-horizon optimal control problem. Given a model of an energy system, such as a microgrid, we could compute an entire sequence of control actions—for example, dispatch set-points for a battery—over a future planning horizon, say $N$ time steps. This "plan-and-commit" approach, also known as **open-loop optimal control**, involves solving the optimization problem once at the beginning of the horizon and then executing the pre-computed sequence of control moves without any further adjustments [@problem_id:4105349].

The primary deficiency of this open-loop strategy is its brittleness. Real-world energy systems are perpetually influenced by unforeseen disturbances (e.g., forecast errors in net-load) and are described by models that are inevitably imperfect. An open-loop plan, being blind to the actual evolution of the system, cannot correct for deviations from the predicted trajectory. Consequently, its performance can degrade severely, and it may even violate critical operational constraints.

MPC overcomes this limitation through the receding horizon mechanism, which consists of a repeating sequence of steps performed at each decision time $k$:

1.  **Measure and Estimate:** The current state of the system, $x_k$, is determined. This is typically achieved by taking sensor measurements, $y_k$, and using a state estimator to produce a state estimate, $\hat{x}_k$, which accounts for measurement noise and model inaccuracies.

2.  **Optimize:** A finite-horizon optimal control problem is solved for the time interval from the current time $k$ to $k+N-1$. This optimization uses the current state $\hat{x}_k$ as its initial condition and the most up-to-date forecasts for future disturbances (e.g., electricity prices, renewable generation). The solution is an entire sequence of optimal future control inputs, $u_{k:k+N-1}^\star = \{u_k^\star, u_{k+1}^\star, \dots, u_{k+N-1}^\star\}$.

3.  **Apply:** Crucially, **only the first element** of the optimal control sequence, $u_k^\star$, is applied to the actual system. The remainder of the planned sequence, $\{u_{k+1}^\star, \dots, u_{k+N-1}^\star\}$, is discarded.

4.  **Shift and Repeat:** Time advances to the next step, $k+1$. The optimization horizon "recedes," or shifts forward, to cover the interval from $k+1$ to $k+N$. The entire process then repeats from Step 1 with a new measurement of the state at time $k+1$.

This iterative process of measuring, re-optimizing, and applying only the first move creates a genuine feedback loop [@problem_id:4105331]. The controller continuously receives information about the actual state of the system and revises its plan accordingly. This provides **recourse**: the ability to adapt to new information and compensate for the effects of past disturbances. For instance, if an unexpected surge in demand causes a battery's state of charge to deviate from its planned trajectory, the MPC controller at the next step will observe this deviation, and the new optimization will naturally generate a corrective action. By re-solving the optimization problem at every step, MPC ensures that the chosen control action is always optimal with respect to the current reality of the system, not a potentially obsolete plan made in the past [@problem_id:4105349].

### Anatomy of the MPC Optimization Problem

The optimization problem solved at each time step is the computational engine of MPC. For a system with state $x$, control input $u$, and disturbance $d$, its canonical form at a given time $k$ is generally structured as follows [@problem_id:4105376]:

$$
\min_{\{u_{k+i|k}\}_{i=0}^{N-1}} \quad \sum_{i=0}^{N-1} \ell(x_{k+i|k}, u_{k+i|k}, d_{k+i|k}) + V_f(x_{k+N|k})
$$

subject to:

1.  **Initial State Constraint:** $x_{k|k} = \hat{x}_k$
2.  **System Dynamics:** $x_{k+i+1|k} = f(x_{k+i|k}, u_{k+i|k}, d_{k+i|k})$ for $i=0, \dots, N-1$
3.  **Path Constraints:** $x_{k+i|k} \in \mathcal{X}$, $u_{k+i|k} \in \mathcal{U}$ for $i=0, \dots, N-1$
4.  **Terminal Constraint:** $x_{k+N|k} \in \mathcal{X}_f$

Here, the notation $v_{k+i|k}$ denotes the predicted value of a variable $v$ at time $k+i$, based on information available at time $k$. Let us dissect each component:

-   The **objective function** is the heart of the economic or performance objective. It comprises two parts:
    -   The **stage cost**, $\ell(x,u,d)$, is summed over the prediction horizon $N$. It penalizes undesirable behavior at each step. In energy systems, this often represents a trade-off. For example, in building climate control, a quadratic stage cost like $\ell(x,u) = q(x - x^{\text{ref}})^2 + r u^2$ balances the penalty on temperature deviation from a setpoint (comfort, weighted by $q$) against the penalty on HVAC power usage (energy cost, weighted by $r$) [@problem_id:4105376] [@problem_id:4105345].
    -   The **terminal cost**, $V_f(x_{k+N|k})$, is a penalty applied to the state at the end of the prediction horizon. Its primary role is to ensure the stability of the closed-loop system by approximating the infinite-horizon cost-to-go from the terminal state.

-   The **constraints** define the feasible operating region of the system.
    -   The **system dynamics**, described by the function $f(\cdot)$, serve as the prediction model that the controller uses to forecast the consequences of its actions.
    -   The **path constraints** enforce operational limits at every step along the horizon. These can include physical limits like the minimum and maximum state of charge of a battery, or the maximum power output of a generator.
    -   The **terminal constraint**, $x_{k+N|k} \in \mathcal{X}_f$, confines the final predicted state to a specific region, which is often instrumental in proving stability.

The choice of the **prediction horizon length**, $N$, is a critical tuning parameter that embodies a fundamental trade-off. A longer horizon provides the controller with more foresight, enabling it to make more strategic decisions, such as pre-cooling a building before a predicted heat wave or charging a battery when electricity prices are forecasted to be low. This generally improves performance and provides more flexibility for constraint handling. However, a longer horizon increases the computational burden of solving the optimization problem and relies on long-range forecasts that are inherently more uncertain. The optimal choice of $N$ depends on the system's time constants, the predictability of disturbances, and the available computational power [@problem_id:4105376] [@problem_id:4105310].

### Managing Uncertainty: From Estimation to Forecasting

A key strength of MPC is its ability to systematically manage different sources of uncertainty. We can broadly classify these into two categories: uncertainty about the internal state of the system (model-plant mismatch) and uncertainty about external driving forces (disturbances and forecasts).

#### State Estimation and Model-Plant Mismatch

The MPC algorithm requires the current state of the system, $x_k$, to initialize its optimization. In many practical energy systems, not all state variables are directly measurable, and those that are may be corrupted by sensor noise. This necessitates the use of a **state estimator**.

For linear systems subject to Gaussian process and measurement noise, the **Kalman filter** is the optimal estimator in the minimum mean-square error sense [@problem_id:4105283]. The Kalman filter operates a two-step recursive loop:

1.  **Time Update (Predict):** Using the system model, the filter predicts the state and its uncertainty (covariance) one step into the future.
2.  **Measurement Update (Correct):** When a new, noisy measurement arrives, the filter computes the "innovation"—the difference between the actual measurement and its prediction. It then uses this innovation, weighted by the optimal **Kalman gain**, to correct the predicted state, yielding an updated, more accurate estimate.

The state estimate $\hat{x}_{k|k}$ produced by the Kalman filter serves as the initial state for the MPC optimization at time $k$. The theoretical justification for this combination comes from the **separation principle**, which, for Linear-Quadratic-Gaussian (LQG) systems, states that the optimal control and optimal estimation problems can be solved separately. This allows us to design the Kalman filter and the MPC controller independently and then connect them, a practice known as **certainty equivalence**, where the state estimate is simply treated as the true state within a deterministic MPC formulation [@problem_id:4105283].

Even in simpler cases, the feedback inherent in the receding horizon framework provides a powerful mechanism for correcting model errors. Consider an MPC scheme where the applied control $u_k$ is the sum of a nominal optimized input $v_k$ and a state-feedback correction term $k_f(x_k - z_k)$, where $z_k$ is the predicted nominal state. At the start of each time step, a "measurement update" resets the nominal state to the actual measured state, $z_k = x_k$. This single action nullifies the accumulated prediction error from all past steps. As a result, the prediction error at the next step, $x_{k+1} - z_{k+1}$, becomes solely a function of the disturbance, $\varepsilon_k$, that occurred during the current interval. It is not contaminated by the history of past errors, demonstrating how the constant re-initialization with measurements prevents errors from accumulating [@problem_id:4105301].

#### Incorporating Forecasts of Exogenous Disturbances

Energy systems are driven by external factors like weather, electricity prices, and energy demand. In the MPC formulation, these are modeled as exogenous disturbances, $d_k$. To plan optimally, the controller requires **forecasts** of these disturbances over the prediction horizon, denoted as $\{d_{k+i|k}\}_{i=0}^{N-1}$.

These forecasts are directly embedded into the optimization problem, influencing the predicted states, costs, and constraints. For example, a forecast of high electricity prices will directly increase the predicted stage cost, incentivizing the controller to reduce consumption. A forecast of high solar irradiance might relax a constraint on grid power import [@problem_id:4105310].

The quality of these forecasts is paramount. A controller acting on poor forecasts may make suboptimal decisions. The performance of an MPC controller can be benchmarked against a hypothetical **clairvoyant controller** that has perfect knowledge of future disturbances. The difference in performance is known as **regret**, and it is a fundamental principle that as forecast accuracy improves (i.e., the variance of forecast errors decreases), the expected regret decreases, and the controller's performance approaches that of the clairvoyant ideal [@problem_id:4105310]. Nonetheless, as previously discussed, the receding horizon feedback mechanism provides a degree of inherent robustness, allowing the controller to correct its course as forecast errors are realized and new, more accurate short-term forecasts become available.

### Ensuring Robustness and Stability

For MPC to be deployed in mission-critical energy applications, it must not only be performant but also safe and reliable. This requires guarantees of recursive feasibility (the controller will not run out of valid moves) and stability (the system will remain bounded and return to its desired operating point).

#### Constraint Handling: Hard, Soft, and Robust Constraints

MPC's ability to handle constraints explicitly is one of its greatest advantages. However, not all constraints are created equal.

-   **Hard Constraints** represent inviolable physical or safety limits. For instance, the power output of a generator cannot exceed its nameplate capacity, or the state of charge of a battery must remain within its specified minimum and maximum to prevent damage. These are formulated as strict inequalities in the optimization problem.

-   **Soft Constraints** represent performance targets or comfort bands that are desirable to maintain but can be temporarily violated if necessary, typically at a high cost. A classic example is the temperature comfort band in a building [@problem_id:4105345]. To model this, the constraint is relaxed using **slack variables**, which are then heavily penalized in the objective function. For example, a temperature constraint $x_{\min} \le x_k \le x_{\max}$ can be softened to $x_{\min} - s_k^- \le x_k \le x_{\max} + s_k^+$ where $s_k^-, s_k^+ \ge 0$ are slack variables. The objective function would then include a term like $\rho(s_k^- + s_k^+)$ with a large penalty weight $\rho$, ensuring that the optimizer will only use the slacks (i.e., violate the comfort band) as a last resort. This prevents the optimization from becoming infeasible due to aggressive disturbances while still strongly encouraging adherence to the desired operating range.

Furthermore, when disturbances are present, simply enforcing constraints on the nominal prediction is not enough to guarantee that the *actual* system will satisfy them. This leads to the problem of **recursive feasibility**: ensuring that if a feasible plan exists at time $k$, one will also exist at time $k+1$, no matter which disturbance occurs.

A powerful technique to achieve this is **Tube-Based MPC**. The core idea is to design a local feedback controller that keeps the actual state trajectory, $z_k$, within a "tube" surrounding a nominal, disturbance-free trajectory, $\bar{z}_k$. The size of this tube is determined by a **Robust Positive Invariant (RPI) set**, $\mathcal{S}$, which is a set with the property that if the state deviation $e_k = z_k - \bar{z}_k$ starts within $\mathcal{S}$, it will remain within $\mathcal{S}$ for all future times, for any possible sequence of bounded disturbances [@problem_id:4105343].

To guarantee robust constraint satisfaction, the constraints for the nominal trajectory are tightened. For example, if the original state constraint is $|z| \le r_x$ and the RPI set has a radius of $s$, the nominal state is constrained to $|\bar{z}| \le r_x - s$. This **constraint tightening**, based on the Pontryagin set difference $\mathcal{X} \ominus \mathcal{S}$, ensures that even in the worst-case scenario where the deviation reaches the edge of the tube, the actual state will still be within the original constraint boundary. This method provides a formal guarantee of recursive feasibility and robust constraint satisfaction [@problem_id:4105343].

#### Stability and the Role of Terminal Costs

A finite prediction horizon can make an MPC controller "myopic." It might take actions that are optimal over the short horizon $N$ but lead the system to a poor state from which future costs will be high, potentially leading to instability. To counteract this, a carefully designed **terminal cost** $V_f(x_{k+N|k})$ and **terminal constraint set** $\mathcal{X}_f$ are essential.

The ideal terminal cost should represent the true optimal cost-to-go from the terminal state $x_{k+N|k}$ to infinity. For linear systems with quadratic costs (LQR problems), this infinite-horizon cost function is known to be quadratic, $V(x) = x^\top P x$. The matrix $P$ is the unique positive semi-definite solution to the **Discrete Algebraic Riccati Equation (DARE)**, which arises from the Bellman optimality principle [@problem_id:4105360].

By setting the terminal cost $V_f(x)$ to be this infinite-horizon value function, we provide the optimizer with an accurate estimate of the long-term consequences of its terminal state choice. Economically, this terminal cost can be interpreted as the "shadow price" of the state. It quantifies the minimum total future cost (e.g., of energy and comfort deviations) that will be incurred starting from that state. By penalizing terminal states with a high long-run cost, the MPC is incentivized to steer the system towards a region of long-term optimality, thereby ensuring closed-loop stability and improving overall performance [@problem_id:4105360].

### Practical Implementation: The MPC Problem as a Quadratic Program

For the common and highly practical case of a linear system with quadratic costs and linear constraints, the MPC optimization problem becomes a **Quadratic Program (QP)**. A QP is an optimization problem of minimizing a quadratic function subject to linear inequality and equality constraints. The efficiency with which this QP can be solved at every time step is the determining factor for the real-time feasibility of MPC.

There are two primary ways to formulate the MPC problem as a QP [@problem_id:4105265]:

1.  **Sparse (or Structured) Formulation:** In this approach, both the future states $\{x_{k+i|k}\}$ and inputs $\{u_{k+i|k}\}$ over the horizon are treated as decision variables. The system dynamics equations act as linear equality constraints coupling these variables. This results in a QP with a large number of variables and constraints. However, the problem structure is highly sparse. The Hessian of the cost function is block-diagonal (since cost at time $i$ only depends on $x_i, u_i$), and the constraint matrix is block-bidiagonal (since dynamics only couple adjacent time steps). The resulting Karush-Kuhn-Tucker (KKT) system, which must be solved by optimizers like Interior-Point Methods (IPMs), is a large, sparse, banded matrix. Specialized sparse linear algebra routines can solve this system with a computational complexity that scales approximately linearly with the prediction horizon $N$.

2.  **Condensed (or Dense) Formulation:** In this approach, the state variables are eliminated algebraically using the system dynamics, expressing the entire future state trajectory as a linear function of the initial state $x_k$ and the input sequence $\{u_{k+i|k}\}$. The only remaining decision variables are the control inputs. This leads to a much smaller QP. However, this condensation comes at a cost: the resulting Hessian matrix of the new QP is generally dense. The computational cost of solving this dense QP using standard methods scales cubically with the number of decision variables, i.e., cubically with the horizon length $N$.

For applications with long horizons, which are common in energy systems to capture daily or weekly cycles, the sparse formulation is almost always preferred. Solvers like tailored IPMs or Active-Set (AS) methods are designed to exploit this sparse, banded structure, enabling the solution of large-scale problems within the tight time constraints required for real-time control [@problem_id:4105265].