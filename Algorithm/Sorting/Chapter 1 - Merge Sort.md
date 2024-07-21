>[!WARNING]
>[Recursion](../Recursion/Notes/Recursion.md)

# Definition

>[!NOTE]
>It is a sorting algorithm that follows the **divide-and-conquer** approach.

It works by **recursively** halving the input array into smaller subarrays and sorting those subarrays into ascending or descending order and then merging those subarrays together. 

**How does it work**

1. **Divide**
	1. It divides the list recursively by halves until it can no longer be divided.
2. **Conquer**
	1. It sorts the divided subarrays into ascending and descending order.
3. **Merge**
	1. The sorted subarrays are merged back together until a full and complete array is produced.

# Demonstration

## Top-down Approach

![Top-Down Approach](../Sorting/Diagrams/Top-Down%20Approach.png)

**Pseudocode**

```python
algorithm TopDownApproach(S): # S is the array
# Input: array, S
# Output: sorted array, S
	if size_of_array > 1:
		divide_the_the_array_halves
		call TopDownApproach(first_half)
		call TopDownApproach(second_half)
		merge both halfs into a single arra
```

## Bottom-Up Apporoach

![Bottom-Up Approach](../Sorting/Diagrams/Bottom-Up%20Approach.png)

**Pseudocode**

```python
algorithm BottomUpApproach(S, n): # S is the array
# Input: array, S
# Output: sorted array, S
	if size_of_array < 2: 
		return
	let index = 1
	while index < n:
		let index2 = 0
		while index2 < size_of_array - index:
			if size_of_array < index2 + index * 2:
				merge( A + index2, A + index2 + index, A + size_of_array)
			else:
				merge( A + index2, A + index2 + index, A + index2 + index * 2)
			index2 = index2 + index * 2
		index = index * 2
```

# Coding Snippet

## Top Down Approach

*Snippet A: MergeSort*

```cpp
// left = 0, right = size - 1
void mergeSort(int array[], int const left, int const right){ 
	if (left >= right) return;
	// get the middle of the array
	int mid { left + (right - left) / 2 };
	// Call the function again with the middle index as the right index
	mergeSort(array, left, mid);
	mergeSort(array, mid+1, right);
	merge(array, left, mid, right);
}
```

*Snippet B: Merge*

```cpp
void merge(int array[], int const left, int const mid,
		  int const right)
{
	int const subArrayOne { mid - left + 1 };
	int const subArrayTwo { right - mid };
	
	/** Divide section **/
	
	// Create the temporary arrays
	int *leftArray { new int[subArrayOne] };
	int *rightArray { new int[subArrayTwo] };
	
	// copy data to the temporary arrays 
	for (int index { 0 }; index < subArrayOne; index++)
		leftArray[index] = array[left + index];
	for (int index { 0 }; index < subArrayTwo; index++)
		rightArray[index] = array[mid + 1 + index];
		
	/** Merge section **/
	
	int indexofSubArrayOne { 0 };
	int indexofSubArrayTwo { 0 };
	int indexofMergedArray { left };
	
	// Merge the arrays back into one
	while (indexofSubArrayOne < subArrayOne && indexofSubArrayTwo < subArrayTwo) {
		if (leftArray[indexofSubArrayOne] <= rightArray[indexofSubArrayTwo]){
			array[indexofMergedArray] = leftArray[indexofSubArrayOne];
			indexofSubArrayOne++;
		}
		else{
			array[indexofMergedArray] = rightArray[indexofSubArrayTwo];
			indexofSubArrayTwo++;
		}
		indexofMergedArray++;
	}
	
	// Copy the remaining elements of left array
	while (indexofSubArrayOne < subArrayOne){
		array[indexofMergedArray] = leftArray[indexofSubArrayOne];
		indexofSubArrayOne++;
		indexofMergedArray++;
	}
	
	// Copy the remaining elements of right array
	while (indexofSubArrayTwo < subArrayTwo){
		array[indexofMergedArray] = rightArray[indexofSubArrayTwo];
		indexofSubArrayTwo++;
		indexofMergedArray++;
	}
	delete[] leftArray;
	delete[] rightArray;
}
```

*Snippet C: Driver code*

```cpp
int main(){
	int arr[6]{12,11,13,5,6,7};
	int size { sizeof(arr) / sizeof(arr[0]) };
	
	std::cout << "The given array is: "
	for (int index{0}; index < size; index++)
		std::cout << arr[index] << " ";
	std::cout << '\n\n';
	
	mergeSort(arr, size);
	
	std::cout << "The given array is: "
	for (int index{0}; index < size; index++)
		std::cout << arr[index] << " ";
	
}
```

# Complexity analysis

## Time complexity

**Best Case**: $O(n\;log\;n)$; when the array is almost sorted

**Average Case**: $O(n\;log\;n)$; when the array is randomly ordered

**Worst Case**: $O(n\;log\;n)$; when the array is not sorted at all or sorted in reverse order.

## Space complexity

$O(n)$. Additional space is needed to store the temporary arrays used during merging

# Advantages and Disadvantages

## Advantages

1. Stability
	- The relative order of equal elements are maintained in the input array
2. Guaranteed performance
	- The Big-O notation of each cases is the same.
3. Simple to implement
	- The approach is straightforward.

## Disadvantages

1. Space complexity
	- Requires additional space to store the temporary subarrays
2. Time complexity
	- Since the time complexity is the same regardless of array size and condition of the array, it is not effective on smaller arrays.

# Application

1. Sorting large datasets
2. External sorting
3. Inversion conuting
4. Finding median of an array