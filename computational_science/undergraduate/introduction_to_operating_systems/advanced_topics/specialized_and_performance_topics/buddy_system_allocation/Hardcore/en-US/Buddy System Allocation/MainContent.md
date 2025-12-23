## Introduction
Effective memory management is one of the most critical and complex tasks an operating system must perform. At the heart of this challenge lies the need for an allocation algorithm that can quickly provide memory to applications while minimizing waste. The [buddy system](@entry_id:637828) is a classic and elegant algorithm that directly confronts this problem by providing a fast, predictable method for managing blocks of physical memory. It strikes a specific balance between allocation speed and the inevitable issue of [memory fragmentation](@entry_id:635227), making it a cornerstone of many real-world operating system kernels.

This article provides a comprehensive examination of the [buddy system](@entry_id:637828) allocation algorithm, from its fundamental principles to its advanced applications. It addresses the knowledge gap between the basic concept of [memory allocation](@entry_id:634722) and the practical realities of implementing such a system in a modern OS. Through a structured exploration, you will gain a deep understanding of this powerful technique.

This article unfolds in three parts. First, the **"Principles and Mechanisms"** chapter will dissect the core algorithm, from its recursive binary partitioning and clever address calculations to its dynamic allocation and coalescing operations. Next, **"Applications and Interdisciplinary Connections"** will explore the [buddy system](@entry_id:637828)'s vital role in real-world scenarios, such as enabling DMA, managing [huge pages](@entry_id:750413), and navigating the complexities of modern NUMA architectures. Finally, **"Hands-On Practices"** will offer a series of targeted problems to reinforce these concepts, challenging you to apply the theory to practical situations involving fragmentation and hardware constraints.

## Principles and Mechanisms

The [buddy system](@entry_id:637828) is a [memory allocation](@entry_id:634722) algorithm that aims to provide fast allocation and deallocation by restricting block sizes to powers of two. This restriction simplifies the process of finding and merging free blocks, thereby controlling the problem of [external fragmentation](@entry_id:634663). This chapter delves into the core principles of its operation, its dynamic behavior, and its performance characteristics.

### The Buddy Principle: Binary Partitioning and Identification

The fundamental concept of the [buddy system](@entry_id:637828) is the recursive binary partitioning of a contiguous memory region. We begin by assuming the memory region to be managed has a total size that is a power of two, say $2^{K}$ bytes. This entire region is considered a single block of **order** $K$.

If an application requests a block of memory, and the only available block is of order $k$, but a block of order $k-1$ would suffice, the allocator can split the order-$k$ block. This split yields two new blocks, each of order $k-1$ and size $2^{k-1}$. These two blocks are known as **buddies**. They are physically adjacent and together reconstitute the original order-$k$ parent block. This splitting process can be applied recursively until a block of a suitable size is produced.

The efficiency of the [buddy system](@entry_id:637828) hinges on its ability to quickly locate the buddy of any given block. This is achieved through a clever exploitation of binary addresses. Let us first consider a memory region that starts at address $0$. The address of any block of order $k$ (size $2^k$) will be a multiple of $2^k$. In binary representation, this means the address of an order-$k$ block will have its $k$ least significant bits as zero.

When a parent block of order $k+1$ at relative address $p'$ is split, its two children of order $k$ will be located at relative addresses $p'$ and $p' + 2^k$. Since $p'$ is an address of an order-$(k+1)$ block, it is a multiple of $2^{k+1}$, meaning its $(k+1)$ least significant bits are zero. This implies that the $k$-th bit of $p'$ is $0$. The address of the second child, $p' + 2^k$, is formed by flipping the $k$-th bit of $p'$ from $0$ to $1$. Therefore, the addresses of two buddy blocks of order $k$ are identical in all bit positions except for bit $k$.

This leads to a simple and elegant rule for finding a buddy: the relative address of an order-$k$ block's buddy can be found by computing the bitwise exclusive OR (XOR) of the block's relative address with its size, $2^k$.

Let $a'$ be the relative address of a block of order $k$. Its buddy's relative address, $b'$, is given by:
$$ b' = a' \oplus 2^k $$
where $\oplus$ denotes the bitwise XOR operation .

This principle must be handled with care when the memory region being managed does not start at address $0$. If the [buddy allocator](@entry_id:747005) manages a region starting at a non-zero absolute address $R$, the buddy logic must be applied to the addresses *relative to $R$*. For a block at an absolute address $a$, its relative address is $a' = a - R$. The buddy's relative address is then $b' = (a - R) \oplus 2^k$. To find the buddy's absolute address, $b$, we add the base address $R$ back:
$$ b = ((a - R) \oplus 2^k) + R $$
This formula correctly identifies the physically adjacent buddy within the managed region, a crucial detail for implementing the allocator over arbitrary segments of physical memory  .

### Dynamic Operations: Allocation and Coalescing

The [buddy system](@entry_id:637828)'s logic is expressed through its two primary operations: allocation and deallocation.

#### Allocation

When the system receives a request for $s$ bytes of memory, the allocation process follows several steps:
1.  **Size Round-up**: The requested size $s$ is rounded up to the nearest power of two, $2^k$, that is large enough to satisfy the request. There is typically a minimum block size, $2^{k_{\min}}$, and the allocated size will not be smaller than this minimum. Any [metadata](@entry_id:275500) overhead required by the allocator must also be factored into the rounded-up size .

2.  **Find a Block**: The allocator searches its free lists for an available block of the required order, $k$. A common and effective strategy is **Closest-Order-First**, where the allocator first checks the free list for order $k$. If it is not empty, a block is taken from this list, allocated, and the process is complete.

3.  **Splitting**: If the free list for order $k$ is empty, the allocator searches for the next larger order, $k+1$, that has a free block. If found, this block is split. One of the resulting order-$k$ buddies is used to satisfy the request, and the other is placed on the free list for order $k$. If the free list for order $k+1$ is also empty, the allocator continues to search at higher orders ($k+2, k+3, \dots$) until it finds an available block, which it then splits recursively until a block of the required order $k$ is produced. All the intermediate buddies generated during this process are placed on their respective free lists.

The choice of which block to split is important. A naive policy like **Highest-Order-First**, which always splits the largest available block, can be detrimental. It may needlessly fragment large blocks to satisfy small requests, making the allocator unable to satisfy subsequent requests for large blocks. The Closest-Order-First policy is generally superior as it preserves large contiguous blocks for as long as possible .

#### Deallocation and Coalescing

Deallocation is the inverse of allocation and is where the [buddy system](@entry_id:637828)'s signature **coalescing** mechanism comes into play.
1.  **Mark as Free**: When a block of order $k$ is freed, it is initially placed on the free list for order $k$.

2.  **Check the Buddy**: The allocator immediately calculates the address of the freed block's buddy. It then checks the status of this buddy.

3.  **Coalesce or Stop**:
    *   If the buddy is also free, the two blocks are coalesced. They are both removed from the free list for order $k$, and they merge to form their single parent block of order $k+1$. This new, larger block is then treated as if it had just been freed: the allocator repeats the process from step 2, checking the buddy of this new order-$(k+1)$ block.
    *   If the buddy is currently allocated, coalescing is not possible. The process stops, and the original freed block simply remains on the free list for order $k$.

This greedy and recursive coalescing is a defining feature of the algorithm. It ensures that whenever two buddies are free, they are immediately merged. This invariant prevents the accumulation of adjacent free blocks that could have been combined, which is a key strategy for controlling [external fragmentation](@entry_id:634663).

For a tangible illustration, consider the sequence of operations from . A series of allocations splits the initial $2^{20}$-byte block into smaller allocated and free blocks. When a block is freed (e.g., block X of order 18 at address 0), the system checks its buddy (order 18 at address $2^{18}$). If that buddy is free (perhaps from a prior deallocation of block Y), they merge into a single block of order 19 at address 0. This new block is then checked against its own buddy (order 19 at address $2^{19}$). This [chain reaction](@entry_id:137566) of merging continues as far up the hierarchy as possible, efficiently reconstructing larger free blocks as memory is returned to the system. To fully restore the initial $2^{20}$-byte block, every single allocated fragment must eventually be freed, allowing the coalescing process to complete all the way to the top order .

### Performance and Fragmentation

While fast, the [buddy system](@entry_id:637828)'s rigid power-of-two sizing introduces specific [fragmentation patterns](@entry_id:201894).

#### Internal Fragmentation

**Internal fragmentation** refers to the wasted space within an allocated block. Because all requests are rounded up to the next power of two, some allocated memory goes unused. For a request of size $s$ that is allocated a block of size $B = 2^k$, the [internal fragmentation](@entry_id:637905) is $B - s$.

A key property of the binary [buddy system](@entry_id:637828) is that the amount of [internal fragmentation](@entry_id:637905) for any single allocation is bounded. Since $B$ is the *smallest* power of two greater than or equal to $s$ (for $s > B/2$), it must be that $s > B/2$. This leads to the bound:
$$ 0 \le B - s  B - \frac{B}{2} = \frac{B}{2} $$
This means [internal fragmentation](@entry_id:637905) is always less than 50% of the allocated block's size . However, this can still be a significant amount of waste. An adversarial sequence of requests can maximize this fragmentation. To get a block of size $2^k$ (for $k > k_{\min}$), one could request $2^{k-1} + 1$ bytes. The resulting fragmentation is $2^k - (2^{k-1} + 1) = 2^{k-1} - 1$, which is nearly half the block size. The most "efficient" way to generate fragmentation relative to the memory consumed is to make requests that are allocated the minimum block size. For example, requesting 1 byte with a minimum block size of $16$ bytes ($2^4$) results in $15$ bytes of waste. A sequence of $n$ such requests would lead to a total [internal fragmentation](@entry_id:637905) of $15n$ bytes .

#### External Fragmentation

**External fragmentation** occurs when there is enough total free memory to satisfy a request, but it is divided into non-contiguous blocks that cannot be combined. The [buddy system](@entry_id:637828) is designed to control this problem, but does not eliminate it.

The system maintains a **maximal [coalescence](@entry_id:147963) invariant**: the set of free blocks never contains a pair of buddies . This is because the greedy coalescing rule merges such pairs immediately upon deallocation. In this sense, the system avoids any "obvious" [external fragmentation](@entry_id:634663).

However, since only buddies can be merged, fragmentation can still occur. Consider a memory region that has been divided into four blocks of size $256$ bytes: $A_0, A_1, A_2, A_3$. The buddy pairs are $(A_0, A_1)$ and $(A_2, A_3)$. If a program allocates all four blocks and then frees $A_0$ and $A_2$, the system has $512$ bytes of free memory. However, a subsequent request for a $512$-byte block will fail. $A_0$ and $A_2$ are not buddies and cannot be coalesced. The largest available block is $256$ bytes, and the request fails despite sufficient total free memory existing . This is a classic example of [external fragmentation](@entry_id:634663) in a [buddy system](@entry_id:637828).

### Implementation in a Broader OS Context

Real-world [operating systems](@entry_id:752938) present additional challenges that a memory allocator must handle.

#### Metadata Management

The allocator must store [metadata](@entry_id:275500) for each block, primarily its size and status (free or allocated). Two common approaches exist :
1.  **Per-Block Headers**: A small header is stored at the beginning of each physical memory block. This keeps the metadata physically close to the data, but the space consumed by these headers contributes to [internal fragmentation](@entry_id:637905), especially if memory is partitioned into many small blocks.
2.  **Centralized Bitmaps**: The status of all possible blocks at all possible orders can be stored in a set of centralized bitmaps, separate from the managed memory itself. This avoids per-block overhead but requires a potentially large, contiguous region for the [metadata](@entry_id:275500) itself and can lead to less favorable [cache locality](@entry_id:637831), as accessing a block's data and its [metadata](@entry_id:275500) may involve different memory locations.

#### Discontiguous Physical Memory

Physical memory is often not one large, contiguous region; it may have "holes" reserved for hardware devices. The [buddy system](@entry_id:637828) can be adapted to this reality by instantiating an independent allocator for each contiguous physical memory zone. The logic of each allocator remains the same, but coalescing is strictly confined within the boundaries of its zone. This prevents any attempt to merge blocks across a physical memory hole, ensuring that all allocations remain physically contiguous .

#### Pinned Pages and Compaction

The [buddy system](@entry_id:637828)'s rigid coalescing rules can be stymied by a single, immovable allocation. If a page is **pinned** in memory (e.g., for DMA), it cannot be moved. If this pinned page occupies one buddy block, it prevents that block from being freed, which in turn prevents any coalescing up the hierarchy, potentially fragmenting a large region of memory. The [buddy system](@entry_id:637828) alone cannot solve this problem.

This is where the [buddy allocator](@entry_id:747005) must work in concert with other OS mechanisms. **Memory compaction** can relocate *movable* pages to consolidate them into one area, thereby creating a large, contiguous free block from the scattered free pages. While the pinned page remains in place, compaction can free up its buddy and other larger-order blocks, which the [buddy system](@entry_id:637828) can then manage effectively. This illustrates that the [buddy allocator](@entry_id:747005) is a powerful component, but it operates within a larger [memory management](@entry_id:636637) subsystem that may use complementary techniques to maintain system performance .