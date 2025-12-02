## Introduction
Analyzing events that unfold over time, such as disease onset or treatment response, presents a fundamental challenge for researchers. How can we accurately model a reality where a patient's status, exposures, and characteristics are in constant flux? Traditional static datasets, with one row per subject, often fail to capture this dynamic nature, introducing critical errors like immortal time bias that can distort study conclusions.

This article delves into an elegant and powerful solution: the start-stop data format. It provides a comprehensive guide to understanding and utilizing this crucial technique for [time-to-event analysis](@entry_id:163785). First, the "Principles and Mechanisms" section will demystify how this format works, explaining how it slices a subject's timeline into manageable intervals to handle time-varying data with precision. Subsequently, the "Applications and Interdisciplinary Connections" chapter will showcase the method's versatility, exploring its use in fields from epidemiology to genomics to answer complex scientific questions. By mastering this format, researchers can unlock deeper insights from longitudinal data and embrace the true, dynamic nature of the processes they study.

## Principles and Mechanisms

To truly understand how we can study events that unfold over time—like the onset of a disease or the effect of a new medicine—we must first appreciate that time itself is not merely a backdrop. It is an active participant. A person's characteristics are not static; they evolve. A patient might start a new treatment, a biomarker level might rise or fall, and people may enter or leave a study at different points. How can a single statistical model possibly handle such a flowing, dynamic reality? The answer lies in a wonderfully clever and elegant [data structure](@entry_id:634264): the **start-stop format**.

### A Tale of Timelines: From Static Snapshots to Flowing Narratives

Imagine a simple study. We want to know if a particular gene, fixed from birth, increases the risk of a heart attack. For this, our data can be quite simple. For each person, we record their total follow-up time, whether they had a heart attack, and whether they have the gene. This gives us a dataset with one row per person. When we want to analyze the data using a powerful tool like the **Cox [proportional hazards model](@entry_id:171806)**, the central idea is to construct a **risk set** at the exact moment each heart attack occurs. The risk set is simply the group of all people who were still in the study and hadn't had a heart attack yet. The model then essentially asks: "Given that *someone* in this group had a heart attack right now, what was the probability it was this specific person, based on their gene status compared to everyone else's?" For fixed, unchanging covariates like a gene, this one-row-per-person structure is perfectly sufficient [@problem_id:4550959].

But life is rarely so simple. What if our covariate isn't a gene, but a drug treatment that a patient can start at any point?

Let's consider a classic scenario that has tripped up many researchers. Patient A starts a new drug 90 days after being discharged from a hospital and, sadly, passes away at 120 days. Patient B, who never takes the drug, passes away at 60 days. If we naively label Patient A as "treated" from day one, we fall into a logical trap. When we analyze Patient B's death at day 60, our model would look at Patient A, see them in the risk set, and count them as a "treated" person who survived. But this is wrong! At day 60, Patient A was *not* on the drug. The 90 days before they started treatment were a period of time where they *had* to survive in order to become treated. This period is often called **immortal time**, because it's impossible for a death-while-treated to occur during this window. Attributing this "immortal" survival time to the treated group creates a powerful illusion, making the drug seem far more effective than it might actually be. This is **immortal time bias**, a critical error that the right [data structure](@entry_id:634264) can eliminate [@problem_id:4829076].

So, what do we do? We need a way to tell our model the full story, as it unfolds. We need to slice up time.

### The Start-Stop Solution: Slicing Time into Stories

This is where the genius of the start-stop format, also known as the **counting process** format, reveals itself. Instead of one static row representing a person's entire history, we break their timeline down into a series of episodes. A new episode begins every time a key characteristic changes.

Let's revisit our patients. The history of Patient A (starts drug at day 90, event at day 120) is no longer a single data point, but a two-part story:

-   **Row 1:** `(start=0, stop=90, treated=0, event=0)`
-   **Row 2:** `(start=90, stop=120, treated=1, event=1)`

The first row tells us: "From day 0 to day 90, this person was at risk, was *not* treated, and no event occurred." The second row continues: "From day 90 to day 120, this person was at risk, *was* treated, and the event happened at the end of this period." Notice the event indicator is `1` only on the very last interval for that person, the one that terminates in the event [@problem_id:4550959].

For Patient B (never treated, event at day 60), the story is simpler, just one episode:

-   **Row 1:** `(start=0, stop=60, treated=0, event=1)`

And what about Patient C, who starts the drug at day 10 but is censored (leaves the study) at day 40? Their story is also two parts:

-   **Row 1:** `(start=0, stop=10, treated=0, event=0)`
-   **Row 2:** `(start=10, stop=40, treated=1, event=0)`

By splitting a person's follow-up at every change in their covariates, we create a dataset where, within any given row, the world is static again. The covariate values are constant over the interval $(start, stop]$ [@problem_id:4776321]. This simple reformatting is incredibly powerful. It allows the Cox model to look at any event time and know the precise status of every single person in the risk set at that exact moment [@problem_id:4961476].

### Handling Life's Late Arrivals and Shifting Landscapes

The true beauty of the start-stop format is its ability to handle even more of life's complexities with the same elegant principle.

#### Delayed Entry

What about patients who join a study late? This is known as **left truncation** or **delayed entry**. Suppose our study starts on January 1st, but a patient is only enrolled on April 1st (day 90). This person was not "at risk" *in our study* for any event that happened in February. We cannot include them in the risk sets for those earlier events. The start-stop format handles this effortlessly: the very first row for this patient simply begins with `start=90` [@problem_id:4906458]. The time before they entered is simply absent from the data, correctly and automatically excluding them from risk sets for any time $t \le 90$ [@problem_id:4550959].

The convention for defining the risk set, $R(t)$, at any time $t$ is to include any person whose current observation interval $(start, stop]$ satisfies the condition $start  t \le stop$ [@problem_id:4551005]. This precise rule ensures that someone who has an event at time $t$ is included in their own risk set, while someone who enters the study exactly at time $t$ is not, upholding a key theoretical property called predictability.

#### Time-Varying Strata and Offsets

This method is so flexible it can even handle situations where the fundamental rules of the analysis change over time. Imagine a hospital-wide protocol changes, affecting the standard of care for all current patients. We might want to model this by moving all patients from an "old protocol" stratum to a "new protocol" stratum. A **stratum** in a Cox model allows for completely different baseline hazard functions. The solution? It's the same as always: at the calendar time the protocol changes, we simply end the current interval for every affected patient and start a new one, updated with their new stratum identifier. The same logic applies to known, time-varying risk adjustments called **offsets**. The start-stop format gracefully incorporates these changes by simply slicing the timeline at each point of change [@problem_id:4991888].

### The Beauty of the Risk Set Revisited

Let's bring it all back to the core idea of the risk set. The Cox model's partial likelihood calculation is like taking a series of snapshots of the world, one at the precise moment of each event. At each snapshot, it asks two questions:
1.  Who was at risk of having the event right now?
2.  What were their characteristics (covariate values) at this exact moment?

The start-stop data format is the "film reel" that allows us to perfectly pause at any frame (any event time) and get a crystal-clear answer to both questions. For an event at time $t=6$, the model scans all the rows in the dataset. Any row where $start  6 \le stop$ corresponds to a person in the risk set. The covariate values from that specific row are the ones that enter the calculation. It's that simple, and it's that powerful [@problem_id:4961494].

This is the principle and mechanism of the start-stop format. It is not just a technical data-wrangling trick. It is a profound conceptual tool that allows a single, elegant statistical model to embrace the dynamic, flowing, and often messy nature of time. It transforms a complex narrative into a series of manageable episodes, allowing us to ask precise questions about risk at any given moment and thereby uncover deeper truths hidden in the timelines of life [@problem_id:4985834].