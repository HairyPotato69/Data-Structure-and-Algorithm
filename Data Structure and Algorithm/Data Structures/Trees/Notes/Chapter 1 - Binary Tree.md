---
aliases:
  - BT
tags:
  - Notes
  - Tree
  - DSA
Date Completed: 2023-09-18
Completion: true
obsidianUIMode: preview
---
>[!WARNING] See these first
>[[Chapter 2 - Linked List]]
>[[Recursion]] 
# Tree Definition
A tree is a data structure that is used to store data in a hierarchical manner. Tree connects nodes via edges. Each tree consists of roots, branches and leaves that are connected with edges. The top most node is known as the **root** and other nodes beneath the root is known as **child**. Each node can have multiple children and each children can have their own children. 

Tree data structure is a non-linear data structure as each node is not stored sequentially but rather arranged on multiple levels.

![[Binary Tree|500]]
**Terminologies**
- Parent Node
	- The node that is the predecessor of another node
	- B is a parent node of C and D
- Child node 
	- The node that is the successor of another node
	- C and D is the children of B
- Leaf Node/External Node
	- Nodes that do not have children
	- C E F H I J are all leaf nodes

Each Tree consists of one or more subtrees. 
There are different types of tree:
1. Binary Tree
2. Ternary Tree
3. Generic Tree
There are also different types of Tree data structure
1. [[Binary Tree]]
2. [[Chapter 2 - Binary Search Tree|BST]]
3. [[Chapter 4 - Adelson-Velsky and Landis Tree|AVL Tree]]
This chapter will focus on **Binary Tree**
## Creation

The Node in Binary Tree is similar to the ones used in Linked List but with a few additions.

```cpp
class BTNode{
	private:
		int m_value{};
		BTNode* m_left{};
		BTNode* m_right{};
	public: 
		BTNode(int val, BTNode* left = nullptr, BTNode* right = nullptr);
};

BTNode::BTNode(int val, BTNode* left = nullptr, BTNode* right = nullptr)		
	: m_value { val }
	, m_left { left }
	, m_right { right }
	{}
```

^29dc32

![[Data Structure and Algorithm/Data Structures/Linked List/Diagram/Trees/Node|500]]

```cpp
class BT{
	private:
		BTNode* m_root{ };
		int m_size{ 0 };
	public:
		BT() = default;
		BTNode* find(BTNode*& root, const int val);
		int get_size() const;
		bool insert(const int father, const int val);
		bool remove(const int val);
		int height(const BTNode*&  root) const;
		
		bool insert2(BTNode*& root, const int father, BTNode*& node);
		BTNode* findDeepest(BTNode*& root) const;
		void deleteDeepest(BTNode*& root, BTNode*& node);
};
```
*Explanation*
Most operations in any tree is done through recursion rather than iteratively. Each function is just modified version of the basic traversal function. 

*Snippet: Tree traversal*
```cpp
void TT(BTNode* root){
	if (!root) return;
	// Operation here (pre order)
	TT(root->left);
	// Operation here (in order)
	TT(root->right);
	// Operation here (post order)
}
```

^26c09b

Before we can go on to explain each tree operation, we have to first understand how traversal works in a tree. 
Traversal in a tree can be done in 3 ways: ^504088
1. Pre-order
	1. Any operation is conducted in the first visit
2. In-order
	1. Any operation is conducted in the second visit
3. Post-order
	1. Any operation is conducted in the third visit
As there are 3 ways of traversal, each solution is based on any of these three. Before any solution is constructed, the type of traversal has to be determined first. 
### Pre-order
![[Tree example|750]]
As it has been established, in pre-order traversal, any operation is carried out in the first visit. For instance:
*Snippet: Pre-order Traversal*
```cpp
void TT(BTNode* root){
	if (!root) return;
	std::cout << root->value;
	TT(root->left);
	TT(root->right);
}
```
Based on the snippet, the value of the nodes will be printed in the first visit. 
*H E B A C D F G L J I K M* 

### In-Order
![[Tree example|750]]
In In-order traversal, any operation is carried out in the second visit. For instance:
*Snippet: In-order Traversal*
```cpp
void TT(BTNode* root){
	if (!root) return;
	TT(root->left);
	std::cout << root->value;
	TT(root->right);
}
```
Based on the snippet, the value of the nodes will be printed in the second visit.
*A B C D E F G H I J K L M*
### Post-Order
![[Tree example|750]]
In Post-order traversal, any operation is carried out in the third visit
*Snippet: Post-order Traversal*
```cpp
void TT(BTNode* root){
	if (!root) return;
	TT(root->left);
	TT(root->right);
	std::cout << root->value;
}
```
Based on the snippet, the value of each node will be printed in the third visit. 
*A D C B G F E I K J M L H*

# Operations

## `int get_size()`
>[!DEFINITION] Function
> Returns the number of nodes in the tree

```cpp
int BT::get_size() const{
	return size;
}
```

## `bool insert(const int val)` and `void insert2(const BTNode*& root, BTNode*& node)`
>[!DEFINITION] Function
>Insert operation requires two functions. The first function is to create a node and the second function is to iterate through the existing tree.
>The insert function works by specifying the parent node to insert

`bool insert(const int val)`
```cpp
bool BT::insert(const int father, const int val){
	BTNode* new_node {new BTNode(val)};
	# If there is not enough memory
	if (!new_node) return 0;
	m_size++;
	# if the tree is empty
	if (!size) 
		# make the new node the first node
		m_root = new_node;
	else
		# call the second function
		return insert2(m_root, father, new_node);
	# succesful 
	return 1;
}
```

`bool insert2(const BTNode*& root, BTNode*& node)`
```cpp
bool BT::insert2(const BTNode*& root, const int father, BTNode*& node){
	# cannot find the father
	if(!root) return 0; 
	# if the value is equivalent
	if (root->value == father){
		# if the node doesn't have a left node or doesn't have nodes in both sides
		if (!root->left || (!root->left && !root->right) 
			root->left = node;
		# doesn't have nodes on the right
		else 
			root->right = node;
		return 1;
	}
	else{
		return (insert2(root->left, father, node)) ? 1 : 0;
	}
}
```


## `int height(const BtNode*& root)`
>[!DEFINITION] Function
>Returns the height of the tree which is calculated based on the deepest node in the tree. $height \neq size$ 

```cpp
int BT::height(const BTNode*& root) const{
	if (!root) return 0;
	int left{ height(root->left) };
	int right{ height(root->right) };
	return (left > right) ? left + 1 : right + 1;
}
```
*Modify this to see if the tree is balanced.*

## `bool remove(const int val)` and `void findDeepest(BTNode*& root)` and `void deleteDeepest(BTNode*& root, BTNode*& node)`
>[!DEFINITION] Function
>Consists of 3 parts
>1. Finds the node to be deleted
>2. Finds the deepest node in the Tree
>3. Replace the node to be deleted with the deepest node

```cpp
bool BT::remove(const int val){
	if (!m_root) return 0;
	if (!m_root->left && !m_root->right)
		# The tree only has one single node
		return (m_root->value == val) ? 0 : 1; 
	Queue q; // Assume the peek function returns a node
	q.enqueue(m_root);
	BTNode* temp { nullptr };
	BTNode* keyNode { nullptr };

	while(!q.empty()){
		temp = q.peek();
		q.dequeue();
		if (temp->value == val) keyNode = temp;
		if (temp->left) q.enqueue(temp->left);
		if (temp->right) q.dequeue(temp->right);
	}
	if (keyNode){
		BTNode* deepestNode = findDeepest(m_root);
		keyNode->value = deepestNode->value;
		deleteDeepest(m_root, deepestNode);
	}
	m_size--;
	return 1;
}
```

```cpp
BTNode* findDeepest(BTNode*& root) const{
	if(!root) return nullptr;
	BTNode* temp { nullptr };
	Queue q; // Assume peek returns a node
	q.enqueue(root);
	while (!q.empty()){
		temp = q.peek();
		q.pop();
		if (temp->left) q.enqueue(temp->left);
		if (temp->right) q.enqueue(temp->right);
	}
	return temp;
}
```

```cpp
void deleteDeepest(BTNode*& root, BTNode*& deleteNode){
	if (!root) return;
	Queue q; // 
	q.enqueue(root);
	BTNode* temp { };
	while(!q.empty()){
		temp = q.peek();
		q.dequeue();
		if (temp == deleteNode){
			temp = nullptr;
			delete deleteNode;
			return;
		}
		if(temp->right){
			if(temp->right == deleteNode){
				temp->right = nullptr;
				delete deleteNode;
				return;
			}
			else
				q.enqueue(temp->right);
		}
		if(temp->right){
			if(temp->left == deleteNode){
				temp->left == nullptr;
				delete deleteNode;
				return;
			}
			else
				q.enqueue(temp->right);
		}
	}
}
```
# Searching
Searching algorithm in Trees can be divided into either Depth First Search, DFS, or Breadth First Search, BFS. ^d75fcf

Depth First Search, in terms of trees, is the standard tree traversal algorithm. 
![[Chapter 1 - Binary Tree#^26c09b]]

However, in Breadth First Search, a level is explored before moving down to the next level. There are different ways to produce BFS but the standard way will be shown here.

*Snippet: BFS* ^c0bec5
```cpp
bool BFS(BTNode* root){
	if(!root) return 0;
	Queue q;
	q.enqueue(root);
	int value{};
	while (!q.empty()){
		q.dequeue(root);
		std::cout << root->value << " ";
		if(root->right) q.enqueue(root->right);
		if(root->left) q.enqueue(root->left);
	}
	return 1;
}
```
# See next
[[Chapter 2 - Binary Search Tree]]
# Extra
## Balanced Tree Check
```cpp
int height(BTNode* root, bool& isBalanced){
	if(!root) return 0;
	int left{ height(root->left) };
	int right{ height(root->right) };
	if(abs(left-right) > 1) 
		isBalanced = 0;
	return max(left+1, right+1);
}
```
## BFS with height
```cpp
void BFS(BTNode* root, int level){
	if (!root) return;
	if (!level) std::cout << root->value;
	else{
		BFS(root->left, level-1);
		BFS(root->right, level-1);
	}
}
```
## Display all possible paths
```cpp
void paths(BTNode* root, vector<int>& path, vector<std::string>& solution){
	if(!root) return;
	path.push_back(root->value);
	if(!root->left && !root->right){
		std::string temp{};
		for (int index{0}; index< path.size(); index++){
			temp+=string(path[index]);
			if (index < path.size()-1)
				temp+="->"
		}
		solution.push_back(temp);
	}
	else{
		paths(root->left, path, solution);
		paths(root->right, path, solution);
	}
	path.pop_back();
}
```
```cpp
void paths2(BTNode* root, int path[], int length){
	if (!root) return;
	path[length] = root->value;
	length++;
	if (!root->left && !root->right){
		for (int index{0}; index < length; index++)
			std::cout << path[index] << " ";
		std::cout << "\n"
	}
	else{
		paths2(root->left, path, length);
		paths2(root->right, path, length);
	}
}
```