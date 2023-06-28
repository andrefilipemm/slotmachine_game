# Mathematics of Slot Machines

**Author:** André Filipe Monteiro Martins  
**Date:** June 2023

## Introduction
Consider a slot game machine with $5$ reels, a $(3\times5)$ play window, and one single payline. Each reel contains symbols labeled by numbers from $0$ to $8$, where $8$ is the symbol that pays the most. All reels spin independently of each other.

Suppose we have stored the symbols that occurred in Reels $1-5$ across some rows in an Excel table, as well as the amount of times the symbol $n$ occurs in reel $p$, denoted as $n_p$, where $n \in \{0,...,8\}$ and $p \in \{1,...,5\}$. Additionally, we have computed the total amount of times any symbol occurred in reel $p$, given by the sum:

```math
\Sigma_p = 0_1 \space + \space ... \space + \space 0_p
```

We used the Excel function COUNTIF to count the occurrence of a given value in a certain column and then considered the sum of all occurrences.

## Computing the Total Hits

Since each reel can spin independently of each other, the following reasoning can be easily generalized to any symbol in the range $\{0, ..., 8\}$. For simplicity, let's consider the symbol $0$.

For example, to compute the total amount of times the payline hits a prize corresponding to a sequence of size five for the symbol $0$, there's obviously only one possibility, namely $(0,0,0,0,0)$. The total amount of hits is given then by:

```math
0_1 \times 0_2 \times 0_3 \times 0_4 \times 0_5
```

Similarly, for a sequence of size four, there are two possibilities: (X,0,0,0,0) or (0,0,0,0,X), where X represents any symbol other than 0. The total hits can be computed as:

    (Σ_1 - 0_1) * 0_2 * 0_3 * 0_4 * 0_5  + 0_1 * 0_2 * 0_3 * 0_4 * (Σ_5 - 0_5)

Note that the amount of times 0 doesn't land in the kth reel is equal to the amount of times any other symbol may land there, that is (Σ_th - 0_th).

For a sequence of size 3, there are three different possibilities: (000XX), (X000X), and (XX000). To compute the total amount of times the payline hits a prize corresponding to a sequence of size 3 for the symbol 0, the computation is:

    0_1 * 0_2 * 0_3 * (Σ_4 - 0_4) * (Σ_5 - 0_5) +
    (Σ_1 - 0_1) * 0_2 * 0_3 * 0_4 * (Σ_5 - 0_5) +
    (Σ_1 - 0_1) * (Σ_2 - 0_2) * 0_3 * 0_4 * 0_5

Similarly, for sequences of size 2 and 1, there are five and three possibilities, respectively. The computations follow a similar pattern.

I found that performing these calculations in Excel was exhausting, so I wrote a Python script using dictionaries and for loops to simplify the process.