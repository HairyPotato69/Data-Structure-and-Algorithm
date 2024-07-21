# Open addressing
Using fixed size array to implement a hash table
**Characteristics**
1. No chaining

![[Open Addressing|1000]]
*Explanation*
This is like an arrray
## Probing
We try and determine whether it's possible to insert a value into the table. If we fail, we try to recompute a slightly different hash for the key value pair we're trying to insert. We're going to keep doing this until we find an empty spot.

>[!TLDR] Too long didnt read
> We're going through a sequence of probes and our hash function will tell us what the sequence of insertion is 
### Hash function
The function specifies the order of slots to probe for a key (**insert, search, delete**). 
$$h=U \times \{0,1,...,m-1 \} \rightarrow \{0,1,....,m-1\}$$
- $U$ is the universe of keys
	- it takes a key
- $\{0,1,...,m-1 \}$
	- number of trials
	- **not the number of slots**
- **second**  $\{0,1,...,m-1 \}$
	- the order of slots that you can insert the key into
- **NOTE**
	- $m-1$ represents the final slot's index
	- $m$ refers to the table size
*Example*
$h(k,1), \; h(k,2), \; ... , h(k,m-1)$ 
$k$ is an arbitrary key. The way this works is that each hash function is to probe the slot and determine if it can accept a value. 
We want the **vector** to be a permutation of $0,1,... m-1$. We want to completely use the hash-table without leaving any unused slots
*Example*
If we have increasing $n$ number of data in the hash-table, it would eventually reach $m-1$ (*the number of slots*). The hash function here serves to probe each slot and determine which slot is available for housing **in sequence**; it can be slot 2, 16, 7, etc. 

![[Open addressing example|1000]]

**None: empty slot (flag)**
Insert(k,v) --> keep probing until an empty slot is found. Insert item when found
#### Search
As long as the slots encountered

# Uniform Hashing Analysis
# Cryptographic hashing