# Dictionary Introduction
**Definition:** Abstract Data Type, *ADT*

*Code Snippet:* Python Dictionary
```python
dict = {1:"one", 2:"two"}
dict[1] # search
dict[1] = "ichi" # insert
del dict[key] # delete
```
A dictionary maintains set of items with a unique key assigned to each of them

**Operations**
1. insert(item)
	- Overwrites any existing key
2. delete(item)
	- deletes the item with the key if it exists
1. search(key)
	1. exact search
	2. report that it does not exist

**Time complexity**
$O(log n)$ via *AVL*(Binary search tree)

**Uses**
1. Docdist
2. Database
3. Compilers and interpreters
	1. Variable names and address of said variable
4. Network router
5. Substring search
6. File/directory synchronisation
7. Cryptographic hash function

>[!TLDR] 
> Key |Value |
> ---  | --- |
> 1     | one |
> 2     | two|

**Simple approaches**
1. [[Hash tables#Direct-access table|Direct-access table]]
## Direct-access table
- [?]  Stores items in array indexed by key
- [?] **Ordinary dictionary in python**

**Big array**

| Key | Value |
| ---- | ---- |
| 0 | NULL |
| 1 | NULL |
| 2 | item |
| 3 | NULL |
| 4 | item |
**Why its bad**
1. Keys may not be integers
2. Uses a lot of memory / **GIGANTIC  MEMORY HOG**

# Solution to issues
## [[Hash tables#Direct-access table|Direct-access table]]
### Prehashing
- [?] Maps keys to non-negative integers
- In theory, keys are finite and discrete 
	- String of bits
*Code snippet:* hash() function
```python
hash(x) #maps every object to the integer
```
### Hashing
- [?] Take all possible keys and reduce them to a **small** set of integers
![[Hashing|1000]]
### Chaining
- [?] linked list of colliding elements (keys) in each slot of hash
![[Chaining|1000]]
# Simple Uniform Hashing
- [!] **An assumption**
	- Each key is equally likely to be hashed to any slot of the table (*uniformity*) independent of where other keys hashing. (*independence*)
## Analysis
- [I] expected length of chain (*linked list*) for **n** keys, **m** slots
	- n is the number of keys 
	- m is the number of slots in the table
	- $\frac{n}{m} = \alpha$= load factor 
	- $O(1) \; if \; m=O(n)$
	- Running time = $O(1+lchain) = O(\alpha)$
# Hash functions
- [?] Mapping keys to hash table
## Division/modulo
$h(k) = k \; mod \;m(slots)$
**Problem**
- It becomes a problem when m  have common factors with k
**In practice**
- If **m** is prime, choose prime table size (avoid common factors)
- Avoid powers of 2 and powers of 10
## Multiplication
$$h(k)  =  (a*k \;mod \;2^w) >> (w-r)$$
- k is w bits long
![[Hash functions|10000]]
## Universal Hashing
$$h(k) = [(ak+b) \; mod \;p]\; mod \; m$$

- a and b are random numbers between p-1
- p is prime number > size of universe prime number
**Worst Case**
- $Pr (h(k_1) == h(k_2)) = \frac{1}{m}$

# Dynamism
## How to choose **M**/ Table doubling
Want $m=O(n)$
	- O(n) makes the space linear
- Start small, m = 8
- Grow and shrink as necessary
- **SEE** [[Chapter 2 - Amortised analysis]]
If m>n: grow table: $m-m^{'}$
- Make table of size $m^{'}$
- Build new hash function
	- **why?**
		- The old one would only hash the older part of the table
		- The new slots would be left untouched
- Rehash
	- insert the items from the original table to the new table 
	- Like [[Chapter 1 - Array#Reallocating array|reallocating array]]
	- O(n) -> you have to reiterate through every element in the table
	- O(n + m + m')
		- n is the linked list
		- m is the slots in the hash tables
		- m' is the new hash table
- **But how much bigger?**
	- if n (number of insertions) > m (slots of the table)
	- *Correct answer:* m' = 2m
		- see [[Chapter 2 - Amortised analysis]]
		- See cost of n insertions (we double each time)
			- 8, 16, 32, 64
				- We're **rebuilding the table** in linear time, n but we're **doing the rebuilding** in log n time
				- $n\; log \;n$ -> binary search tree
			- O(1 + 2 + 4 + 8 +16......)
			- O(n)
	- *Let say*
		- m' = m + 1
			- what is the cost of n inserts
			- O(1+ 2 +3 + 4 + 5......)
			- You have to keep creating every time you insert
			- O(n^2)
*k* inserts would take $\theta(k)$ time. This means that each insert by itself would take constant time, $\theta(1)$. *k* inserts would mean inserting (a constant time) over and over and over again, resulting in $\theta(k)$. 
*k* deletes would take $\theta(k)$ time because:
1. After deleting, the table size would still remain the same
2. The extra costs comes from **shrinking and growing** the table
## Shrinking table size
### Half-half
If the number of data $n = \frac{m}{2}$, we would shrink the table by $\frac{m}{2}$. ($n$ is the number of data, $m$ is the table size). In practice, this would be bad. 
*Example: Why it's bad*
When the number of data goes from 8 to 9, we have to expand the table to 16. But if we delete a data, the table has to shrink back down to 8. You're repeating this process over and over again. Insertion and deletion both takes linear time. 
$$
\begin{align}
2^k \rightarrow 2^k + 1 \; (insertion) \\
2^k + 1 \rightarrow 2^k \; (deletion)

\end{align}$$
### Quarter-half
If the number of data $n = \frac{m}{4}$, we would shrink the table by $\frac{m}{2}$. The amortised time would be $O(1)$. 
**Important:** $n\leq m \leq 4n$

## Amortisation
# Summaries
## Summary A
![[Summary 1.png]]**SEE:**
1. [[Hash tables#Direct-access table|Direct-access table]]
2. [[Hash tables#Solution to issues|Solutions to issues]]