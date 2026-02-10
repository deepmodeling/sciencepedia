## Introduction
How do the spinning blades of a pump propel water, or how does a turbine harness the power of steam? The answer to these fundamental questions lies not in complex, machine-specific rules, but in a single, elegant principle of physics. At the heart of all rotating fluid machinery—from simple fans to advanced jet engines—is the challenge of quantifying the energy exchange between a [rotor](@keyword=rotor|lang=en-US|style=Feynman) and a fluid. This article demystifies this process by exploring the Euler turbomachine equation, the cornerstone of [turbomachinery](@keyword=turbomachinery|lang=en-US|style=Feynman) theory. In the following sections, we will embark on a journey from first principles to practical applications. First, in "Principles and Mechanisms," we will derive the equation from the law of [conservation of angular momentum](@keyword=conservation_of_angular_momentum|lang=en-US|style=Feynman), explore it from an energy perspective, and uncover the concept of [rothalpy](@keyword=rothalpy|lang=en-US|style=Feynman) as a [conserved quantity](@keyword=conserved_quantity|lang=en-US|style=Feynman). Then, in "Applications and Interdisciplinary Connections," we will see how this single equation governs the design and analysis of a vast array of devices, bridging the gap between [fluid mechanics](@keyword=fluid_mechanics|lang=en-US|style=Feynman) and [thermodynamics](@keyword=thermodynamics|lang=en-US|style=Feynman).

## Principles and Mechanisms

### A Law of Motion for Rotating Machines

How does a machine like a pump or a turbine really work? How does a set of spinning blades manage to hurl a fluid forward or, conversely, extract energy from its motion? The answer, like so many deep truths in physics, boils down to one of Newton’s laws of motion, but dressed in rotational clothes: the [conservation of angular momentum](@keyword=conservation_of_angular_momentum|lang=en-US|style=Feynman).

Imagine a fluid flowing through the spinning [rotor](@keyword=rotor|lang=en-US|style=Feynman) of a turbomachine. Let's draw an imaginary, stationary boundary that encloses the entire [rotor](@keyword=rotor|lang=en-US|style=Feynman)—what engineers call a [control volume](@keyword=control_volume|lang=en-US|style=Feynman). The fluid enters this volume at some inner radius, $r_1$, and leaves at an outer radius, $r_2$. Just as a force is required to change an object's [linear momentum](@keyword=linear_momentum|lang=en-US|style=Feynman), a **[torque](@keyword=torque|lang=en-US|style=Feynman)** is required to change its [angular momentum](@keyword=angular_momentum|lang=en-US|style=Feynman). The [net torque](@keyword=net_torque|lang=en-US|style=Feynman), $\mathcal{T}$, that the [rotor](@keyword=rotor|lang=en-US|style=Feynman) exerts on the fluid must equal the rate at which the fluid carries [angular momentum](@keyword=angular_momentum|lang=en-US|style=Feynman) out of our boundary, minus the rate at which it carries it in.

The [angular momentum](@keyword=angular_momentum|lang=en-US|style=Feynman) of a tiny parcel of fluid is its [linear momentum](@keyword=linear_momentum|lang=en-US|style=Feynman) times its [lever arm](@keyword=lever_arm|lang=en-US|style=Feynman) (the radius), but we only care about the component of [momentum](@keyword=momentum|lang=en-US|style=Feynman) that contributes to rotation—the tangential component. So, the specific [angular momentum](@keyword=angular_momentum|lang=en-US|style=Feynman) ([angular momentum](@keyword=angular_momentum|lang=en-US|style=Feynman) per unit mass) of the fluid at any point is simply the product of its radius $r$ and its tangential velocity $V_t$. The total [rate of change](@keyword=rate_of_change|lang=en-US|style=Feynman) is then this value multiplied by the [mass flow rate](@keyword=mass_flow_rate|lang=en-US|style=Feynman), $\dot{m}$. This gives us a wonderfully simple and powerful relationship for the [torque](@keyword=torque|lang=en-US|style=Feynman) [@problem_id:1782445]:

$$
\mathcal{T} = \dot{m} (r_2 V_{t2} - r_1 V_{t1})
$$

This equation is the heart of the matter. The [torque](@keyword=torque|lang=en-US|style=Feynman) is simply the [mass flow rate](@keyword=mass_flow_rate|lang=en-US|style=Feynman) times the change in specific [angular momentum](@keyword=angular_momentum|lang=en-US|style=Feynman). Now, what about energy? Power is [torque](@keyword=torque|lang=en-US|style=Feynman) multiplied by the [angular velocity](@keyword=angular_velocity|lang=en-US|style=Feynman), $P = \mathcal{T} \omega$. If we want to know the work done *on each kilogram of fluid* as it passes through, we just divide the power by the [mass flow rate](@keyword=mass_flow_rate|lang=en-US|style=Feynman), $w = P / \dot{m}$. Performing this simple substitution, we arrive at a cornerstone of fluid machinery:

$$
w = \omega (r_2 V_{t2} - r_1 V_{t1})
$$

Since the speed of the blade itself at any radius $r$ is $U = \omega r$, we can write this in its most celebrated form, the **Euler turbomachine equation** [@problem_id:542191]:

$$
w = U_2 V_{t2} - U_1 V_{t1}
$$

This elegant equation tells us that the energy transferred to or from a unit mass of fluid is determined entirely by the blade speeds ($U_1, U_2$) and the fluid's absolute tangential velocities ($V_{t1}, V_{t2}$) at the inlet and outlet. Everything about the intricate curves of the blades and the complex [three-dimensional flow](@keyword=three_dimensional_flow|lang=en-US|style=Feynman) between them is ultimately distilled into this simple change in the quantity $U V_t$. This is the work done *on* the fluid. For a pump or [compressor](@keyword=compressor|lang=en-US|style=Feynman), this value is positive. For a turbine, which extracts work *from* the fluid, it is negative.

### An Energy Perspective: The View from the Merry-Go-Round

One of the beautiful things about physics is that fundamental principles are interconnected. If our [momentum](@keyword=momentum|lang=en-US|style=Feynman)-based derivation is correct, we should be able to arrive at the same result by considering [energy conservation](@keyword=energy_conservation|lang=en-US|style=Feynman). But there's a catch. The familiar Bernoulli equation, a statement of [energy conservation](@keyword=energy_conservation|lang=en-US|style=Feynman) along a [streamline](@keyword=streamline|lang=en-US|style=Feynman), doesn't work when you try to apply it across a pump. Why? Because the pump is actively adding energy to the system!

To get around this, we can perform a clever change of perspective. Instead of watching from a stationary "lab" frame, let's imagine we are riding on the spinning impeller itself, like a child on a merry-go-round. From this rotating vantage point, the flow looks steady, and we can write down a version of the Bernoulli equation. However, in a [rotating frame](@keyword=rotating_frame|lang=en-US|style=Feynman), we must account for the "fictitious" forces that appear, most notably the [centrifugal force](@keyword=centrifugal_force|lang=en-US|style=Feynman). This leads to the **rotating Bernoulli equation** [@problem_id:617082]:

$$
\frac{p}{\rho} + \frac{1}{2} w^2 - \frac{1}{2} u^2 + gz = \text{constant along a streamline}
$$

Here, $w$ is the fluid's velocity *relative* to the spinning blade, and $u = \omega r$ is the speed of the blade itself. That new term, $-\frac{1}{2}u^2$, is essentially the [potential energy](@keyword=potential_energy|lang=en-US|style=Feynman) associated with the [centrifugal force](@keyword=centrifugal_force|lang=en-US|style=Feynman).

Now, the magic happens when we connect the view from the merry-go-round back to the view from the ground. The absolute velocity $\vec{v}$ (seen from the ground) is related to the [relative velocity](@keyword=relative_velocity|lang=en-US|style=Feynman) $\vec{w}$ (seen from the blade) and the blade velocity $\vec{u}$ by the simple [vector addition](@keyword=vector_addition|lang=en-US|style=Feynman) $\vec{v} = \vec{w} + \vec{u}$. By applying the rotating Bernoulli equation between the inlet and outlet and using this velocity relationship to translate back to the stationary frame, we can calculate the change in the fluid's [total energy](@keyword=total_energy|lang=en-US|style=Feynman), or **total head** ($H = p/(\rho g) + v^2/(2g) + z$).

After some algebraic shuffling, a familiar result emerges. The ideal head rise supplied by the pump is:

$$
H_{ideal} = \frac{U_2 V_{t2} - U_1 V_{t1}}{g}
$$

This is exactly the Euler equation for work, divided by the [acceleration due to gravity](@keyword=acceleration_due_to_gravity|lang=en-US|style=Feynman) $g$ to express it as a height, or "head" [@problem_id:617082]. The fact that we get the same answer from two completely different starting points—one based on [momentum](@keyword=momentum|lang=en-US|style=Feynman) and [torque](@keyword=torque|lang=en-US|style=Feynman), the other on energy in a [rotating frame](@keyword=rotating_frame|lang=en-US|style=Feynman)—is a profound confirmation of the equation's validity. It reveals a deep unity between the laws of motion and the principle of [energy conservation](@keyword=energy_conservation|lang=en-US|style=Feynman).

### Rothalpy: A Hidden Constant of Motion

Physicists are always on the hunt for [conserved quantities](@keyword=conserved_quantities|lang=en-US|style=Feynman). In a simple, [steady flow](@keyword=steady_flow|lang=en-US|style=Feynman) without heat or work, the [stagnation enthalpy](@keyword=stagnation_enthalpy|lang=en-US|style=Feynman), $h_0 = h + V^2/2$ (where $h$ is static [enthalpy](@keyword=enthalpy|lang=en-US|style=Feynman) and $V$ is velocity), is constant. It represents the [total energy](@keyword=total_energy|lang=en-US|style=Feynman) of the fluid. But inside a turbomachine, the [rotor](@keyword=rotor|lang=en-US|style=Feynman) is constantly doing work, so $h_0$ is *not* conserved—it increases across a pump and decreases across a turbine.

This begs the question: is there *any* energy-like quantity that remains constant? The answer is yes, and it is a beautifully subtle concept known as **[rothalpy](@keyword=rothalpy|lang=en-US|style=Feynman)**.

Let's look at the Euler equation again: the change in [stagnation enthalpy](@keyword=stagnation_enthalpy|lang=en-US|style=Feynman) is precisely equal to the work done, $\Delta h_0 = h_{0,2} - h_{0,1} = U_2 V_{t2} - U_1 V_{t1}$. If we rearrange this equation, we find something remarkable:

$$
h_{0,2} - U_2 V_{t2} = h_{0,1} - U_1 V_{t1}
$$

This tells us that the quantity $I = h_0 - U V_{\theta}$ is constant as the fluid passes through the [rotor](@keyword=rotor|lang=en-US|style=Feynman)! This quantity is the [rothalpy](@keyword=rothalpy|lang=en-US|style=Feynman). But what *is* it? To gain intuition, we can again use our velocity relationship $\vec{V} = \vec{W} + \vec{U}$ to express [rothalpy](@keyword=rothalpy|lang=en-US|style=Feynman) in terms of the properties seen in the [rotating frame](@keyword=rotating_frame|lang=en-US|style=Feynman) [@problem_id:1792364]. The result is astonishingly simple:

$$
I = h + \frac{1}{2}W^2 - \frac{1}{2}U^2
$$

Let's dissect this expression. The term $h + \frac{1}{2}W^2$ is simply the [stagnation enthalpy](@keyword=stagnation_enthalpy|lang=en-US|style=Feynman) as measured by an observer on the spinning blade—the [total energy](@keyword=total_energy|lang=en-US|style=Feynman) in the relative frame. The final term, $-\frac{1}{2}U^2$, is, as we saw before, the [potential energy](@keyword=potential_energy|lang=en-US|style=Feynman) arising from the [centrifugal force](@keyword=centrifugal_force|lang=en-US|style=Feynman) field. Therefore, [rothalpy](@keyword=rothalpy|lang=en-US|style=Feynman) is nothing more than the [total energy](@keyword=total_energy|lang=en-US|style=Feynman) of the fluid as seen in the [rotating reference frame](@keyword=rotating_reference_frame|lang=en-US|style=Feynman). For an ideal, [adiabatic flow](@keyword=adiabatic_flow|lang=en-US|style=Feynman), this quantity is conserved along a [streamline](@keyword=streamline|lang=en-US|style=Feynman) [@problem_id:620936]. This concept is immensely powerful, forming the basis for analyzing flows in everything from steam turbines to the advanced compressors and turbines in a modern [jet engine](@keyword=jet_engine|lang=en-US|style=Feynman) [@problem_id:473960]. It is the proper statement of [energy conservation](@keyword=energy_conservation|lang=en-US|style=Feynman) for a fluid on a merry-go-round.

### From Ideal Theory to Real Machines

So far, we have been exploring a physicist's paradise of ideal fluids and perfectly guiding blades. The Euler turbomachine equation represents the absolute theoretical maximum [energy transfer](@keyword=energy_transfer|lang=en-US|style=Feynman) possible. However, the real world is always a bit messier, and the art of engineering lies in understanding and mitigating these messy realities.

The first dose of reality comes from [friction](@keyword=friction|lang=en-US|style=Feynman). When we use a pump to move water through a long pipe, as in a pumped-storage hydroelectric system, the Euler head isn't the whole story. The pump must not only lift the water against [gravity](@keyword=gravity|lang=en-US|style=Feynman) (the static head) but also push it against the [viscous drag](@keyword=viscous_drag|lang=en-US|style=Feynman) from the pipe walls (the [friction](@keyword=friction|lang=en-US|style=Feynman) head). The total head the pump must actually provide to the system is called the **manometric head**, $H_m$. The ratio of this useful head to the theoretical Euler head imparted by the impeller, $\eta_h = H_m / H_e$, is called the **[hydraulic efficiency](@keyword=hydraulic_efficiency|lang=en-US|style=Feynman)** [@problem_id:1735311]. It is a stark reminder that some of the energy given to the fluid by the blades is immediately lost to heating the pipe.

A second, more subtle imperfection arises from the fact that impellers have a *finite* number of blades. Our [ideal theory](@keyword=ideal_theory|lang=en-US|style=Feynman) implicitly assumes an infinite number of infinitesimally thin blades that perfectly guide the flow. In a real pump, with, say, 7 or 9 blades, the fluid in the channel between them doesn't perfectly follow the blade curvature. It tends to "slip" past the exit, failing to achieve the full tangential velocity predicted by the [ideal theory](@keyword=ideal_theory|lang=en-US|style=Feynman) [@problem_id:456879]. This phenomenon, known as **slip**, means that the actual tangential velocity $V_{t2}$ is less than the ideal value. Consequently, the actual theoretical head is lower than the ideal Euler head. This [head loss](@keyword=head_loss|lang=en-US|style=Feynman) due to slip can even be estimated with models like Stodola's, which show it depends on the geometry and rotation speed.

The Euler turbomachine equation is therefore not just a formula; it is a guiding principle. It sets the absolute benchmark for performance. Every real-world turbomachine falls short of this ideal, and its overall efficiency is a product of multiple factors: [hydraulic efficiency](@keyword=hydraulic_efficiency|lang=en-US|style=Feynman) (fighting external losses), slip (from finite blades), mechanical efficiency ([friction](@keyword=friction|lang=en-US|style=Feynman) in bearings and seals), and more. By starting with the pristine beauty of the Euler equation and systematically accounting for each of these real-world effects, we transform a fundamental principle of physics into a powerful tool for engineering design and analysis.

