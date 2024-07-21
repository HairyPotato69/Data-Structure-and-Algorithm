# Part 1
>[!INFO]
> Amortisation is the process of spreading the repayment of a loan, or the cost of an intangible asset, over a specific timeframe

# Example no.1: Opening a Donut Franchise

**Assume the franchise is established 10 years ago**

### Approach no.1

*Franchise cost: $1, 000, 000*

*Cost per donut: $1*

*Question:* How much does it cost to make a Duncan Donut

*Answer:* The first one costs $1,000,001 and the rest costs $1

*Side Note:* If you want to make $1 profit per donut, each donut should be sold for $2. If this is the case, then the first donut would cost $1,000,002 with the rest of the donuts being $2. 

*Caveat:* No one wants to pay $2 for a donut

### Approach no.2

*Franchise cost: $1,000,000*

*Cost per donut: $1*

*Question:* How much does it cost to make a Duncan Donut

*Answer:* Assuming we're going to sell 1 million donuts, with the 1 million dollars franchise cost being scatter across each donut, each donut will now cost 2 dollars. To make a profit of $1, each donut would have to be sold for $ dollars. 

### Final thought

Both of these approaches are essentially the same - $1 profit on both approaches. The difference lies in how we, as the owner, allocate the expenses. 

# Example no.2: Binary counter

### Approach no.1 

| Digit | Binary number | Bits flipped  | Cost to increment, C |
| ---- | ---- | ---- | ---- |
| 0 | 0000 | 1 | 1 |
| 1 | 0001 | 2 | 2 |
| 2 | 0010 | 1 | 1 |
| 3 | 0011 | 3 | 3 |
| 4 | 0100 | 1 | 1 |
| 5 | 0101 | 2 | 2 |
| 6 | 0110 | 1 | 1 |
| 7 | 0111 | 4 | 4 |
| 8 | 1000 | 1 | 1 |
| 9 | 1001 | 2 | 2 |

*Assume that it take 1 to increment*

*Description:*

For an even number to move to an odd number, only one bit (*the first one from the right/ lowest big*) has to be flipped; however, for an odd number to become an even number, the bits, 1, starting from the lowest bit will flip until it reaches a bit 0. This means that 50% of the costs will be *1*

## Approach no.2

### *Take NOTE:* Ticket counter

*Ticket costs*

$10 per trip (*to Country A*)

*Total cost:* $20 (*back and forth*)

$20 for round trips

*Total cost:* $20 (*to-go*) but return is **free**

*What if we apply the same logic here - buying round trips. Basically, allocate the costs in advance*

| Digit | Binary number | Cost to increment, C |
| ---- | ---- | ---- |
| 0 | 000**0** | 2 |
| 1 | 000**1** | 2 |
| 2 | 0010 | 2 |
| 3 | 0011 | 2 |
| 4 | 0100 | 2 |
| 5 | 0101 | 2 |
| 6 | 0110 | 2 |
| 7 | 0111 | 2 |
| 8 | 1000 | 2 |
| 9 | 1001 | 2 |

*Explanation*

The cost to increment will be allocated in advance (*buying round-trips tickets*). From 0, *0000*, to 1, *0001*, costs of 2 will be allocated for the first digit. In that transition, the lowest bit will be flipped to 1 (*Going to Country A*) at a cost of 1 with the remaining cost deserved for flipping it back (*Returning from Country A*)

# Potential Function, $\phi$

A potential function , $\phi$ maps each data structure, $D_i$ to a real number $\phi$ ($D_i$) which is the potential associated with the data structure, $D_i$, which is the potential associated with the data structure $D_i \cdot D_0 = 0$ and $D_i \geq 0$ for all $i \geq 0$ 

$$The \; amortized\; cost, \; \hat{c} = c_i + \phi(D_i) - \phi(D_{i-1})$$

$$\sum_{i=1}^{n}\hat{c_i} = \sum^{n}_{n=1}(c_i+\phi(D_i)-\phi(D_{i-1}))$$

$$=\sum^{n}_{i-1} + \phi(D_n) - \phi(D_0)$$

*Explanation: Binary Counter example, think about the round trip example*

Let $\phi(D_i) = b_i$, the number of 1's in $i$

$$\hat{c} = c_i + \phi(D_i) - \phi(D_{i-1})$$

*From 0000 to 0001*

$$\hat{c} = 1 + 1 - 0 = 2$$

The first value is the actual cost of flipping the bit (*one way ticket)*. The second value is the potential value (*Going to Country A/one way ticket*) in the amortised cost. The third value is the (*The free return trip from the round way ticket/how much you "save"*)

*From 0011 to 0100* 

 $$\hat{c} = 3 + 1 - 2 = 2$$

*Explanation:*

 The first value is the actual cost of flipping the bit (*one way ticket)*. The second value is the potential value (*Going to Country A/one way ticket*) in the amortised cost. The third value is the (*The free return trip from the round way ticket/how much you "save"*)**

# Part 2

- [?] operations take t(n) amortised
	- If there are k operations
	- The running time would be at most $k\cdot t(n)$ 
		- $k$ refers to the number of operations
		- $t(n)$ refers to the time taken for each operation

**Example**

Paying rent of a room monthly. We can think  of it as paying a certain amount of money daily. 
