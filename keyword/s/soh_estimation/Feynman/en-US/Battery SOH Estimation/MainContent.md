## Introduction
From smartphones to electric vehicles and grid-scale storage, rechargeable batteries are the invisible engines of the modern world. While we are familiar with their immediate energy level—the State of Charge (SOC)—a more profound question governs their true value and safety: how healthy are they? This question of long-term degradation is answered by the State of Health (SOH), a critical metric that quantifies the aging process of a battery. The challenge, however, is that SOH is an internal property of a sealed, complex electrochemical system. We cannot see it directly; we must infer it from external measurements.

This article addresses this fundamental challenge, providing a comprehensive guide to the science and practice of SOH estimation. It bridges the gap between the internal chemistry of a battery and the external signals we can measure, revealing how to diagnose and predict the vitality of these essential devices.

The following chapters will guide you through this process. First, in "Principles and Mechanisms," we will explore the core concepts of SOH, defining the key signs of aging and detailing the powerful estimation techniques, such as Kalman filters and Incremental Capacity Analysis, used to track them. Subsequently, "Applications and Interdisciplinary Connections" will demonstrate how these methods are applied in the real world, unlocking the potential for digital twins, second-life batteries, and grid stabilization, while highlighting the field's deep connections to thermal engineering, data science, and even [cybersecurity](@entry_id:262820).

## Principles and Mechanisms

To truly understand a battery, we must learn to think on two different timescales. Imagine asking a friend, "How are you doing?" You might get two very different kinds of answers. One is about the present: "I'm full of energy today!" The other is about the long term: "My doctor says my blood pressure has been slowly creeping up over the last few years." The first is a statement about their immediate state; the second is about their underlying health.

For a battery, it's exactly the same. The question "How full is it?" corresponds to its **State of Charge (SOC)**. This is a measure of the available energy *right now*, a quantity that changes rapidly as you charge your phone or drive your electric car. The deeper question, "How well is it aging?", corresponds to its **State of Health (SOH)**. This is not about the immediate charge level but about the slow, irreversible degradation that occurs over hundreds or thousands of cycles.

In the language of physics and engineering, we make this distinction precise. SOC is a fast-changing **state variable** of the system, often denoted as $z(t)$. Its value evolves on a timescale of seconds to hours, governed by the current flowing in or out. SOH, on the other hand, is not a single state but is captured by a set of slowly-drifting **parameters** of the system, which we can call $\theta$. These parameters describe the fundamental properties of the battery itself, and they change over months and years  . This separation of timescales—fast states versus slow parameters—is the central principle of [battery health](@entry_id:267183) estimation.

### The Measurable Signs of Aging

If SOH is defined by these hidden internal parameters, how do we measure them? We can't just cut the battery open. Instead, like a doctor looking for symptoms, we must learn to read the external signs of aging. For a lithium-ion battery, there are two primary symptoms.

The first and most intuitive symptom is **capacity fade**. A brand-new battery might store, say, $3 \, \text{Ah}$ of charge. As it ages, chemical side reactions consume some of the lithium ions and active materials, effectively reducing the battery's storage space. After a few years, its maximum capacity might have faded to only $2.5 \, \text{Ah}$. We can define a capacity-based health metric, $SOH_C$, as the simple ratio of the current maximum capacity $Q$ to its nominal new capacity $Q_{new}$:

$$
SOH_C = \frac{Q}{Q_{new}}
$$

A brand-new battery has $SOH_C = 1$, and this value slowly decreases towards a defined end-of-life, often set at $0.8$.

The second major symptom is **power fade**, which we feel as a battery that struggles to deliver power. When you demand a large current from an old phone, its voltage might plummet, and it might even shut down, even if it reports having 30% charge left. This happens because its internal **ohmic resistance**, $R_0$, has grown. Think of it as a pipe that's getting clogged. For the same flow of current ($I$), Ohm's law tells us that the pressure drop—or in our case, the voltage drop—is larger: $\Delta V = I R_0$. This increased resistance turns more of the battery's precious energy into useless heat, limiting the power it can deliver. We can define a resistance-based health metric, $SOH_R$, that reflects this. Since lower resistance is better, we use an inverse ratio:

$$
SOH_R = \frac{R_{new}}{R_{current}}
$$

A battery's overall health is a combination of these factors. We can create a single, composite SOH by taking a weighted average of these two metrics, recognizing that for some applications, capacity is more important, while for others, power capability is key .

### The Challenge of a Moving Target: Decoupling Temperature

Here we run into our first practical puzzle. A battery's performance is exquisitely sensitive to temperature. A cold battery is a sluggish battery—its apparent capacity is lower, and its internal resistance is higher. So, if we measure a high resistance, is it because the battery is old, or is it just because it's a cold winter day?

This is a classic **confounding factor**. To get at the true, intrinsic health of the battery, we must "decouple" the reversible effects of temperature from the irreversible effects of aging. We need to find a way to correct our measurements to a standard reference temperature, say $25\,^\circ\text{C}$.

Fortunately, physics gives us simple models to do this. For small temperature ranges, the available capacity changes almost linearly with temperature. For resistance, the underlying chemical processes often follow an **Arrhenius relationship**, a beautiful law of physical chemistry that says reaction rates increase exponentially with temperature. Since resistance is inversely related to these reaction rates, it decreases exponentially as the battery warms up. By applying these physical corrections, we can take a raw measurement of capacity or resistance at any temperature and calculate what its value *would be* at the reference temperature, giving us a true picture of its health  .

### Becoming a Detective: How to Estimate Health

Now we know what to look for—[capacity fade](@entry_id:1122046) and resistance growth, corrected for temperature. But how do we find them in a sealed black box, using only the "clues" from its external terminals? We must become detectives, using a powerful technique called **state estimation**.

The idea is to build a mathematical model of the battery—a **digital twin**—that runs in real-time on the microchip of a Battery Management System (BMS). This model takes the same input as the real battery (the measured current, $i_k$) and tries to predict its output (the terminal voltage, $y_k$). The difference between the model's prediction and the real measurement is called the **residual**. If the model's parameters (our SOH metrics, $Q$ and $R_0$) are correct, the residual will be small. If they are wrong, the residual will be large. The job of an **estimator** is to continuously adjust the parameters in the model to keep the residual as small as possible, thereby tracking the true health of the battery as it ages.

The most famous tool for this job is the **Kalman filter**. It operates in a simple, elegant two-step dance:

1.  **Predict:** The filter uses the model and the last known state to predict where the battery's state and parameters will be at the next moment in time.
2.  **Update:** The filter takes the new measurement, compares it to the prediction, and uses the difference to correct its estimate.

The magic of the Kalman filter is how it performs this correction. It weighs the prediction against the measurement based on its uncertainty in each. If the model is known to be very accurate (low **process noise**), it will trust its prediction more. If the sensor is very precise (low **measurement noise**), it will trust the measurement more . To track the slowly drifting SOH parameters, we often use a clever trick called **state augmentation**. We tell the filter that the parameters are not perfect constants but can change slightly over time, modeling them with a "random walk" like $Q_{k+1} = Q_k + \text{a little noise}$. This gives the filter the freedom to gradually adjust the parameters over many cycles to match the battery's true aging trajectory .

This Bayesian approach of starting with a **prior** belief about the SOH, and then using data to arrive at an updated **posterior** belief, is a universal principle for learning from data in the face of uncertainty .

### Finding Hidden Clues: The Power of Incremental Capacity Analysis

Sometimes, the most revealing clues are hidden in plain sight. Instead of just looking at the voltage itself, we can examine how the voltage *changes* as we add charge. This leads us to a wonderfully insightful technique called **Incremental Capacity Analysis (ICA)**.

We look at the quantity $dQ/dV$, which tells us how much charge ($dQ$) we need to add to raise the battery's voltage by a tiny amount ($dV$). For most of the charging process, this value is relatively flat. But for certain battery chemistries, especially those with graphite anodes, something special happens. At specific points, the graphite undergoes a phase transition, like water turning to ice. During this transition, it can absorb a lot of lithium ions (charge) with very little change in its voltage. At this point, the $dQ/dV$ value shoots up, creating a sharp, distinct peak in the data.

Here is the brilliant part: the exact voltage at which these peaks occur is tied to the balance of lithium between the two electrodes. As a battery ages, it irreversibly loses some of its cyclable lithium. This loss subtly shifts the relative alignment of the electrodes, and as a result, the voltage positions of the ICA peaks shift as well. It turns out there is a beautifully simple, direct relationship: the amount of capacity that has been lost, $\Delta Q$, is directly proportional to the voltage shift of the peak, $\Delta V$. The constant of proportionality is simply the height of the peak, $H$ :

$$
\Delta Q \approx H \cdot \Delta V
$$

This gives us an elegant and powerful non-invasive diagnostic. By tracking these tiny shifts in voltage peaks over a battery's life, we can accurately measure the amount of capacity it has lost. It is the electrochemical equivalent of a doctor listening to a heartbeat to diagnose the health of the heart—an internal condition revealed by an external signal.

### From Health to Fate: Predicting the Future

Ultimately, the reason we are so obsessed with measuring State of Health is that it is the key to predicting the future—specifically, the **Remaining Useful Life (RUL)**. We want to know: how many more cycles can this battery endure before its capacity drops below an acceptable threshold (e.g., 80% of its original value)?

This is the final step in our journey. We take the SOH parameters we have so carefully estimated over time and fit them to a mathematical degradation model, such as $SOH(n) = 1 - \theta_1 \sqrt{n} - \theta_2 n$, where $n$ is the cycle number . This equation gives us a curve that describes the battery's aging trajectory.

To predict the RUL, we simply extrapolate this curve into the future and find the cycle number where it crosses the end-of-life threshold. But there's a crucial final touch. Our estimates of the parameters $\theta_1$ and $\theta_2$ are not single numbers; they are probability distributions that carry uncertainty. A good prognostic system must be honest about this uncertainty.

Using a statistical tool called the **[delta method](@entry_id:276272)**, we can propagate the uncertainty in our estimated parameters through the RUL calculation. This doesn't give us a single number for the RUL; it gives us a forecast with a [confidence interval](@entry_id:138194). The system doesn't just say, "The battery will last for 500 more cycles." It says, "We are 95% confident that the battery will last between 450 and 550 more cycles." This is the hallmark of true scientific prediction: a statement not just of what we know, but also of how well we know it.