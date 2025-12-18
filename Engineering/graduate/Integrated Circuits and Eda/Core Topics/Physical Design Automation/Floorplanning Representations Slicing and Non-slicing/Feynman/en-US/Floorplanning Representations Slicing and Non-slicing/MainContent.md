## Introduction
In modern integrated circuit (IC) design, [floorplanning](@entry_id:1125091) is the critical first step in translating an abstract circuit diagram into a physical reality. It involves arranging the major functional blocks on a silicon die, a task akin to city planning on a microscopic scale. This initial layout has profound consequences, dictating the chip's final area, performance, and power consumption. The central challenge, however, is not just finding a good arrangement, but first finding a way to describe and manipulate these arrangements algorithmically. This article addresses the need for a formal "blueprint" or language that can encode the complex spatial relationships between circuit blocks.

Across the following chapters, you will embark on a journey through these powerful geometric languages. In "Principles and Mechanisms," you will learn the fundamental representations, from the intuitive guillotine cuts of slicing floorplans to the abstract power of non-slicing methods like Sequence Pairs and B*-Trees. Next, "Applications and Interdisciplinary Connections" will reveal how these representations serve as the backbone for [optimization algorithms](@entry_id:147840) and connect the abstract geometry of the layout to real-world physical effects like signal delay and wiring congestion. Finally, "Hands-On Practices" will provide an opportunity to solidify your understanding by actively decoding and constructing these representations. Our exploration begins with the foundational question: how do we speak the language of placement?

## Principles and Mechanisms

Having grasped the grand challenge of [floorplanning](@entry_id:1125091)—akin to designing a miniature city on a pinhead—we must now ask a more practical question: How does one actually *describe* an arrangement of rectangular blocks? It’s not enough to just have a list of final coordinates; that’s like describing a building by listing the GPS coordinates of every brick. We need a language, a blueprint, that captures the *relationships* between the blocks. This blueprint must be compact, easy to manipulate by a computer, and powerful enough to describe all the ingenious layouts our optimization algorithms might dream up. This chapter is a journey through the beautiful languages invented to speak the poetry of placement.

### The Art of Tiling: The Mosaic Floorplan

At its core, every valid floorplan is a perfect rectangular tiling. We call this a **mosaic floorplan**: a collection of smaller, non-overlapping rectangular modules that, when pieced together, completely fill a larger bounding rectangle with no gaps or empty spaces .

The fundamental rule governing this puzzle is deceptively simple: no two blocks can overlap. What does this mean mathematically? For any two blocks, block $i$ and block $j$, they must be separated in space. This means one of four things must be true:
1.  Block $i$ is entirely to the left of block $j$.
2.  Block $j$ is entirely to the left of block $i$.
3.  Block $i$ is entirely below block $j$.
4.  Block $j$ is entirely below block $i$.

If we let the bottom-left corner of block $i$ be at $(x_i, y_i)$ with width $w_i$ and height $h_i$, these conditions are written as a disjunction:
$$(x_i + w_i \le x_j) \lor (x_j + w_j \le x_i) \lor (y_i + h_i \le y_j) \lor (y_j + h_j \le y_i)$$
This "OR" logic is the crux of the floorplanning problem. For a computer, making a single choice from a list of options is easy. But having to satisfy one of four options for *every single pair* of blocks creates a combinatorial explosion of possibilities. The cleverness of different [floorplanning](@entry_id:1125091) representations lies in how they tame this explosion by providing a structured way to make these choices.

### The Guillotine Cut: Slicing Floorplans

Perhaps the most intuitive way to tile a rectangle is to simply cut it in two. Imagine you have a rectangular piece of paper. A single straight cut from one edge to the opposite edge—a **guillotine cut**—divides it into two smaller rectangles. You can then take one of those smaller pieces and cut it again, and so on. A floorplan that can be created entirely through a sequence of such guillotine cuts is called a **slicing floorplan** .

This recursive, [divide-and-conquer](@entry_id:273215) process has a wonderfully elegant representation: the **slicing tree** . Imagine drawing this process as a family tree. Each time you make a cut, you create a node. A vertical cut is a `V` node, and a horizontal cut is an `H` node. The two new rectangles created are its children. You continue this until the final rectangles are your circuit blocks, which become the leaves of the tree.

This tree is not just a pretty picture; it is a complete blueprint. Given the dimensions of the leaf blocks, we can work our way back up the tree to find the size of the entire floorplan. The rules are beautifully simple:
-   At a `V` node (vertical cut), the children are side-by-side. The total width is the sum of their widths, and the total height is the height of the taller child: $W_{total} = w_{left} + w_{right}$ and $H_{total} = \max(h_{left}, h_{right})$.
-   At an `H` node (horizontal cut), the children are stacked. The total height is the sum of their heights, and the total width is the width of the wider child: $H_{total} = h_{top} + h_{bottom}$ and $W_{total} = \max(w_{top}, w_{bottom})$.

We can even distill this tree into a single line of text using a classic computer science idea: the **Polish postfix expression** . By traversing the tree and listing a node only *after* visiting its children (a [post-order traversal](@entry_id:273478)), we get a string like `A B V C H`. This string is a set of instructions for a stack-based calculator. You push blocks (`A`, `B`) onto a stack. When you see an operator (`V`), you pop two blocks, combine them, and push the new, larger composite block back.

For such an expression to be a valid floorplan blueprint, it must obey a "pay-as-you-go" rule known as the **balloting condition**. As you read the expression from left to right, the number of blocks (operands) you've seen must always be strictly greater than the number of cuts (operators) you've seen, until the very end. This ensures that whenever an operator arrives, there are always at least two blocks on the stack waiting to be combined. It's a simple, beautiful rule that guarantees our one-line description corresponds to a valid, constructible tree.

### The Interlocking Puzzle: Non-slicing Floorplans

The slicing approach is elegant, but is it complete? Can *every* possible mosaic floorplan be described by a sequence of guillotine cuts? A moment's thought with a pen and paper reveals the answer is no.

Consider an arrangement of five blocks in a "pinwheel" or "spiral" configuration, where four outer blocks surround a central one. Now, try to find a single, straight guillotine cut—either horizontal or vertical—that partitions the entire bounding box without slicing through the interior of one of the blocks. You can't! Any such cut is blocked by the central module. This is an example of a **non-slicing floorplan** . The modules are "interlocked" in a way that defies the simple [divide-and-conquer](@entry_id:273215) logic of the guillotine.

This discovery was profound. It showed that the language of slicing trees, while simple and useful, was not expressive enough to describe all possible layouts . A more powerful, more general language was needed.

### A Pair of Permutations: The Sequence Pair

How can we describe these complex, interlocking relationships without relying on a hierarchy of cuts? The breakthrough came in the form of the **[sequence pair](@entry_id:1131501)** representation, a wonderfully abstract yet powerful idea . Instead of a tree, the entire set of relative placements is encoded in just two permutations (ordered lists) of the module names. Let's call them $(\pi_x, \pi_y)$.

The rule is this: to find the relationship between any two blocks, say `A` and `B`, you just look at their relative order in the two lists.
- If `A` comes before `B` in *both* $\pi_x$ and $\pi_y$, then `A` must be to the left of `B`.
- If `A` comes before `B` in $\pi_x$ but *after* `B` in $\pi_y$, then `A` must be below `B`.

That's it. From these two simple lists, we can derive a complete set of "left-of" and "below" constraints for every single pair of blocks. This is a complete, non-contradictory set of instructions for assembling the floorplan.

To turn these relative constraints into absolute coordinates, we build two **[constraint graphs](@entry_id:267131)**: a horizontal one and a vertical one . In the horizontal graph, we draw an arrow from `A` to `B` if `A` is left of `B`. We can then imagine this as a flow chart where the length of a path is the sum of the widths of the blocks along it. The longest path through this graph determines the minimum required width of the entire floorplan. A similar process with the vertical graph and block heights gives us the minimum overall height. This elegant method connects the abstract permutations to a concrete, compacted, and valid floorplan.

Crucially, the [sequence pair](@entry_id:1131501) representation is *complete*: it can describe *any* mosaic floorplan, including all the slicing ones and all the tricky non-slicing ones that the slicing tree cannot handle .

### Another View: The B*-Tree and the Skyline

Another ingenious approach to non-slicing floorplans is the **B*-tree** . Like the slicing tree, it's a [binary tree](@entry_id:263879), but its rules have a completely different meaning. Here, the parent-child relationship encodes direct adjacency:
- A left child is placed to the immediate right of its parent.
- A right child is conceptually placed above its parent.

This local adjacency information guides a beautifully intuitive packing algorithm. Imagine building a city, one block at a time. To ensure you don't build on top of something else, you keep track of the city's **skyline**—the upper envelope of all the buildings placed so far.

When placing a new block, you first determine its horizontal position based on the B*-tree rules (e.g., to the right of its parent). Then, you look at the segment of the skyline where this new block will sit. To place it as low as possible without any overlap, you must set its base at the height of the *highest point* of the skyline in that interval. After placing the block, you update the skyline in that region to the new, higher level. This greedy, step-by-step process, guided by the tree's local rules, constructs a dense, valid, and non-slicing floorplan. With clever [data structures](@entry_id:262134) to manage the skyline, this entire process can be performed with remarkable efficiency.

### The Elegance of Language: Redundancy and Canonical Forms

We have seen these powerful languages—Polish expressions, sequence pairs, B*-trees. But do they have a perfect, one-to-one relationship with the floorplans they describe? The answer, fascinatingly, is no. Just like in human language where "big" and "large" are synonyms, these representations suffer from **redundancy**: multiple different encodings can describe the exact same floorplan topology.

Consider the slicing representation. A series of three horizontal cuts can be grouped as $(A \text{ on } B) \text{ on } C$ or $A \text{ on } (B \text{ on } C)$. This is the property of **[associativity](@entry_id:147258)**. Furthermore, $A \text{ on } B$ is just a mirror image of $B \text{ on } A$; if we consider mirror images to be the same topology, this is **[commutativity](@entry_id:140240)**. These properties mean that many different Polish expressions can decode to the same layout . To make the language more efficient for computers, we can introduce **normalization** rules—like grammatical rules—to choose a single, canonical "sentence" for each idea. For example, we can forbid consecutive identical operators (like `HH`) and always list the operands in alphabetical order. This collapses a whole family of equivalent expressions into one.

The [sequence pair](@entry_id:1131501) representation has its own beautiful redundancy, born from geometry itself . If you take a finished chip layout and rotate it by 90°, 180°, or flip it across an axis, you still have the same fundamental design. However, the [sequence pair](@entry_id:1131501) that describes this transformed layout will be completely different! It turns out there are 8 such symmetries (the [symmetry group](@entry_id:138562) of a square, for you mathematicians). This means that for any generic floorplan, there are up to **8 distinct sequence pairs** that all represent the same topological structure.

This journey from simple cuts to abstract [permutations](@entry_id:147130) reveals the deep and beautiful interplay between geometry, computer science, and even abstract algebra. The quest for the perfect floorplan representation is a search for a language that is not only powerful and complete but also elegant and efficient, turning the chaotic puzzle of chip layout into a structured and solvable problem.