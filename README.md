# Mathematics of Slot Machines

**Author:** André Filipe Monteiro Martins  
**Date:** June 2023

## Introduction
Consider a slot game machine with $5$ reels, a $(3\times5)$ play window, and one single payline. Each reel contains symbols labeled by numbers from $0$ to $8$, where $8$ is the symbol that pays the most. All reels spin independently of each other.

Suppose we have stored the symbols that occurred in Reels $1-5$ across some rows in an Excel table, as well as the amount of times the symbol $n$ occurs in reel $p$, denoted as $n_p$, where $n \in$ $`\{0,...,8\}`$ and $p \in$ $`\{1,...,5\}`$. <br />
Additionally, we have computed the total amount of times any symbol occurred in reel $p$, given by the sum:

```math
\Sigma_p = 0_1 \space + \space ... \space + \space 0_p
```

We used the Excel function COUNTIF to count the occurrence of a given value in a certain column and then considered the sum of all occurrences.

## Computing the Total Hits

A payline has a hit if there is a sequence of $n$ symbols (usually from left to right). We represent a sequence by an ordered tuple. <br />
The total number of times the paylines hit a prize corresponds to total hits, and each sequence size has a different prize given by a prize table. <br />

Since each reel can spin independently of each other, the following reasoning can be easily generalized to any symbol in the set $`\{0,...,8\}`$. For simplicity, let's consider the symbol $0$. <br />

For example, to compute the total amount of times the payline hits a prize corresponding to a sequence of size five for the symbol $0$, there's obviously only one possibility, namely $(0,0,0,0,0)$. The total amount of hits is then given by:

```math
0_1 \times 0_2 \times 0_3 \times 0_4 \times 0_5
```

Similarly, for a sequence of size four, there are two possibilities: $(X,0,0,0,0)$ or $(0,0,0,0,X)$, where $X$ represents any symbol other than $0$. The total hits can be computed as:

```math
(\Sigma_1 - 0_1) \times 0_2 \times 0_3 \times 0_4 \times 0_5  + 0_1 \times 0_2 \times 0_3 \times 0_4 \times (\Sigma_5 - 0_5)
```

Note that the amount of times $0$ doesn't land in the $k_{th}$ reel is equal to the amount of times any other symbol may land there, that is $(\Sigma_{th} - 0_{th})$.

For a sequence of size three, there are three different possibilities: $(0,0,0,X,X)$, $(X,0,0,0,X)$, and $(X,X,0,0,0)$. To compute the total amount of times the payline hits a prize corresponding to a sequence of size three for the symbol $0$, the computation is:

```math
0_1 \times 0_2 \times 0_3 \times (\Sigma_4 - 0_4) \times (\Sigma_5 - 0_5) + <br />
    (\Sigma_1 - 0_1) \times 0_2 \times 0_3 \times 0_4 \times (\Sigma_5 - 0_5) + <br />
    (\Sigma_1 - 0_1) \times (\Sigma_2 - 0_2) \times 0_3 \times 0_4 \times 0_5
```

Similarly, for sequences of size two and one, there are five and three possibilities, respectively. The computations follow a similar pattern.

I found that performing these calculations in Excel was exhausting, so I wrote a Python script using dictionaries and for loops to simplify the process, which you can find under the notebook folder.
