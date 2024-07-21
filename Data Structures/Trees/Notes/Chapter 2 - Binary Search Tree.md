>[!WARNING]
>[Binary Tree](../Notes/Chapter%201%20-%20Binary%20Tree.md)
>[Recursion](../../../Algorithm/Recursion/Notes/Recursion.md)
>This chapter assumes that binary tree has been covered.

# NOTE

Binary Search Tree, BST, is a type of [[Chapter 1 - Binary Tree|Binary Tree]] in which the value of the left node is always lesser than the value of the right node. This is known as the LCR rule. By enforcing this rule, the efficiency of deletion, insertion, and searching algorithm will be increased.

## Properties of BST:

1. The left subtree of a node contains only nodes with values lesser than the node's value.
2. The right subtree of a node contains only nodes with values larger than the node's value.
3. Any duplicate values will be stored on the left side of the subtree. 

# Creation 

## Binary Search Tree

```c++
class BST{
	private:
		BTNode* m_root{ };
		int m_size{ 0 };
	public:
		BST() = default;
		int get_size() const;
		bool isEmpty() const;
		bool insert2(BSTNode*& root, BSTNode*& new_node);
		bool remove2(BSTNode*& pre, BSTNode*& cur, const int value);
		
		bool insert(const int value);
		bool remove(const int value);
		bool case2(BSTNode*& pre, BSTNode*& cur);
		bool case3(BSTNode*& cur);
}
```

# Operation

Each of the operations that can be on a BST follow this format:

*Snippet A: Basic format*

```cpp
bool BSTT(BSTNode*& root, const int key){
	if (!root) return 0;
	if (root->value == key) return 1;
	// If the value of the current node is greater than the key, move left
	// If the vlaue of the current node is lesser than the key, move right
	return (root->value > key) ? BSTT(root->left , key) : BSTT(root->right, key);
}
```

## `int get_size()`

>[!NOTE]
>Returns the number of nodes in the tree

```cpp
int BT::get_size() const{
	return size;
}
```

## `bool insert2(BSTNode* root, BSTNode* new_node)` and `bool insert(const int value)`

>[!NOTE]
>Insert operation requires two functions. The first function is to create a node and the second function is to iterate through the existing tree. The insert function works by specifying the parent node to insert.

### `bool insert(const int value)`

```cpp
bool BST::insert(const int value){
	BSTNode* new_node { new BSTNode(type) };
	if (!new_node) return 0;
	m_size++;
	(isEmpty()) ? m_root = new_node : insert2(m_root, new_node);
	return 1;
}
```

### `bool insert2(BSTNode* root, BSTNode* new_node)`

```cpp
bool BST::insert2(BSTNode* root, BSTNode* new_node){
	// is the current
	if (root->value > new_node->value)
		(!root->left) ? root->left = new_node : insert(root->left, new_node);	
	else 
		(!root->right) ? root->right = new_node : insert(root->right, new_node);
}
```

## `bool remove(BSTNode* pre, BSTNode* cur, const int value)` and `bool remove(const int value)` and `bool case2(BSTNode* pre, BSTNode* cur)` and `bool case3(BSTNode* cur)`

>[!NOTE]
>Checks 3 cases
>1. Both sides of the target node is null
>2. Either one side of the target node is null
>3. Both sides of the target node is not null

### `bool remove(const int value)`

```cpp
bool BST::remove(const int value){
	return (!m_root) ? 0 : remove2(m_root, m_root, value); 
}
```

### `bool remove(BSTNode* pre, BSTNode* cur, const int value)`

```cpp
bool BST::remove2(BSTNode*& pre, BSTNode*& cur, const int value){
	if (!cur) return 0;
	if (cur->value == value){
		return (!cur->left || !cur->right) ? case2(pre, cur) : case3(cur);
	}
	return (cur->value > value) ? remove(cur, cur->left, value) : remove(cur, cur->right,value);
}
```

### `bool case2(BSTNode* pre, BSTNode* cur)`

```cpp
bool BST::case2(BSTNode*& pre, BSTNode*& cur){
	// root node
	if (pre == cur){
	// If the left node exists
	// Move the node up to be the parent node
		if (!cur->left)
			pre = cur->left;
	// If the right node exists
	// Move the node up to be the paret node
		else if (!cur->right)
			pre = cur->right;
		delete cur;
		size--;
		return 1;
	}
	if (pre->right == cur){
		if (!cur->left)
			pre->right = cur->left;
		else if(!cur->right)
			pre->right = cur->right;
	}
	else{
		if (!cur->left)
			pre->left = cur->left;
		else if(!cur->right)
			pre->left = cur->right;
	}
	delete cur;
	size--;
	return 1;
}
```

### `bool case3(BSTNode* cur)`

```cpp
bool BST::case3(BSTNode*& cur){
	BTNode* is{ nullptr };
	BTNode* isFather{ nullptr };
	// Find the in-order sucessor
	is = isFather = cur->right;
	
	while (!is->left){
		isFather = is;
		is = is->left;
	}
	cur->value = is->value;
	if(is == isFather)
		cur->right = is->right;
	else 
		isFather->left = is->right;
	delete cur;
	size--;
	return 1;
}
```

# So, why?

The issue with the normal binary tree is how easy it is to be out of balance.

![Tree or Linked List](../Diagram/Tree%20or%20linked%20list.png)

Although this is still possible in Binary Search Tree, it only happens when the values inserted are all smaller or larger than the prior values. 

## Application

1. Searching
	- Binary Search uses this concept to look for a value in a sorted list.
2. Sorting
	- Merge sort also uses this concept
3. Range queries
4. Data Storage
5. Databases
6. AI

## Advantages and Disadvantages

### Advantages

The time complexity when searching in a BST is $O(log\; n)$. The structure in a BST is also structured, easing the process of finding previous and next values.

### Disadvantages

In the worst-case scenario, the time complexity is a linear time complexity, $O(5)$. There aren't a lot of operations supported by a BST.

# See next

[AVL Tree](../Notes/Chapter%204%20-%20Adelson-Velsky%20and%20Landis%20Tree.md)
[Heap, Priority Queue and Complete Binary Tree|Heap, Priority Queue and Complete Binary Tree](../Notes/Chapter%203%20-%20Heap,%20Priority%20Queue%20and%20Complete%20Binary%20Tree.md)
