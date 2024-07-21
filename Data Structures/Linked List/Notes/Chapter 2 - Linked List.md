# Linked List NOTE
Linked list allows values to be connected to one another without being contiguous - values can exist in different location in the memory grid. 

![Memory grid](../Diagram/Normal%20linked%20list/Memory%20grid.png)

Generally, linked list are presented as such,

![Linked List](../Diagram/Normal%20linked%20list/Linked%20list.png)

A linked list will have a head pointer that points to the first value in the linked list. A tail pointer that points to the final value in the linked list *may* be included. 

## Creation

The elements in a linked list is referred to as **Nodes**.

```cpp
class Node{
	private:
		int m_val{};
		Node* m_next{};
	public:
		Node(int value, Node* next = nullptr);
};

Node::Node(int value, Node* next = nullptr)
	: m_val{ value }
	, m_next { next } 
	{}
```

![Node](../Diagram/Normal%20linked%20list/Node.png)

Nodes should have a home to live in before any operations can be done. A home (*linked list*) can be created as shown.

```cpp
class LinkedList{
	private:
		Node* m_head{};
		Node* m_tail{}; // Optional
		int m_size{};
	public:
		LinkedList(Node* head, Node* tail = nullptr);
		Node* find(const int index) const;
		int get_size() const;
		bool insert(int index, const int value);
		bool value_at(const int index, int& value) const;
		bool remove(const int index);
		bool set(const int index, const int value);
};
```

*Explanation*
1. `Node* head{}`
	- The head is the pointer that points to the first node of the linked list
2. `Node* tail{}`
	- The tail is the pointer that points to the final node of the linked list
3. `int size{}`
	- This is to keep track of the number of nodes in the linked list
4. `LinkedList()`
	- This is a default constructor
5. `Node* find(const int index)`
	- This function returns the node at a specific index
6. `int get_size()`
	- This function returns the number of nodes in a linked list
7. `bool insert(int index, const int value)`
	- This function inserts node at a specific location
8. `bool value_at(const int index, int& value)`
	- This function returns the value of a node at a specific location
9. `bool remove(int index)`
	- This function remove a node at a specific index
8. `bool set(const int index, const int value)`
	- This function changes the value of a node at an index

# Operations

## `LinkedList()`

>[!NOTE]
> Default constructor is a constructor that is called automatically when no other constructor is used.

```cpp
LinkedList::LinkedList(Node* head, Node* tail = nullptr)
		: m_head {head}
		, m_tail {tail}
		{}
```

## `Node* find(const int index)`

>[!NOTE]
>Finds and returns a node at a specific location.

```cpp
Node* LinkedList::find(const int index) const{
	if((index <= 0 || index> size) || !(head)) return nullptr;
	Node* node{ m_head };
	for(int tracker{1}; tracker<index; tracker++)
		node = node->next;
	return node;
}
```

## `int get_size()`

>[!NOTE]
>Returns the number of nodes in the linked list.

```cpp
int LinkedList::get_size() const{
	return size;
}
```

## `bool LinkedList::insert(int index, const int value)`

>[!NOTE]
>Insert node at the front, end or anywhere in-between.

![Insertion](../Diagram/Normal%20linked%20list/insertion.png)

*Snippet A*

```cpp
bool LinkedList::insert(int index, const int value){
	if(index <= 0 || index > size) return 0;
	Node* new_node{new Node(value)};
	if(index == 1){
		m_head = new_node;
		m_tail = new_node;
	}
	else if (index == size){
		Node* prev{ find( index-1 ) };
		prev->next = new_node;
		m_tail = new_node;
	}
	else{
		Node* prev{ find(index-1) };
		new_node->next = prev->next;
		prev->next = new_node;
	}
	m_size++;
	return 1;
}
```

## `bool value_at(const int index, int& value)`

>[!NOTE]
>Finds and returns the value of the node at a specific location.

```cpp
bool LinkedList::value_at(const int index, int& value) const{
	if((index <= 0 || index > size) || !head) return 0;
	value = find(index)->val;
	return 0;
}
```

## `bool remove(int index)`

>[!NOTE]
>Finds and removes a node at a specific location

![Deletion](../Diagram/Normal%20linked%20list/deletion.png)

*Snippet B*

```cpp
bool remove::LinkedList(int index){
	if(index <= 0 || index > size || !head) return 0;
	if(index == 1){
		Node* node{ m_head };
		m_head = node->next;
		delete node;
	}
	Node* prev{ find(index-1) };
	Node* node{ find(index) };
	if(index == size){
		prev->next = nullptr;
		m_tail = prev;
		delete node;
	}
	else{
		prev->next = node->next;
		delete node;
	}
	m_size--;
	return 0;
}
```

## `bool set(const int index, const int value)`

>[!NOTE]
>Finds and changes the value of a node at a specific location

```cpp
bool LinkedList::set(const int index, const int value){
	if(index <= 0 || index > size || !head) return 0;
	Node* node{ find(index) };
	node->val = value;
	return 1;
}
```

# Variations

There are different types of linked list:
1. [[Chapter 3 - Queue and Stack|Queue]]
2. [[Chapter 3 - Queue and Stack|Stack]]
3. Doubly linked list
	- Largely similar with singly linked list.
2. Circular linked list (both singly and doubly)

# Techniques related to [Chapter 1 - Array](../Notes/Chapter%201%20-%20Array.md) and [Chapter 2 - Linked List](../Notes/Chapter%202%20-%20Linked%20List.md)

## Two pointer technique

Most problem regarding array and linked list can be solved using two pointers in same or different locations. 
One of the **must-know** algorithm in linked list is the **Hare and Tortoise Algorithm**.

### Hare and Tortoise Algorithm

![Hare and Tortoise](../Diagram/Normal%20linked%20list/Hare%20and%20Tortoise.png)

**How does it work?**
Imagine two runners on a looping track where there is a faster runner ahead of the slower runner. Since it is a loop, the faster runner will, at some point, intersect the slower runner. By applying the same logic we can determine if a linked list is a cyclic linked list. 

*Snippet C*: Basic Algorithm

**Time complexity: $O(n)$**

```cpp
bool HareandTortoise(Node* head){
	if(!head) return 0;
	Node* tortoise{head};
	Node* hare{head->next};
	while(hare && hare->next){
		if(tortoise == hare)
			return 1;
		(hare->next) ? hare = hare->next: hare = nullptr;
		(tortoise->next) ? tortoise = tortoise->next:tortoise=nullptr;
	}
	return 0;
}
```

*Snippet D*: Starting point of the cycle

**Time complexity: $O(n)$**

```cpp
Node* HareandTortoise(Node* head){
	if(!head) return 0;
	Node* tortoise{head};
	Node* hare{head->next};
	while(hare && hare->next){
		if(tortoise == hare){
			tortoise = head;
			while (tortoise != hare){
				tortoise = tortoise->next;
				hare = hare ->next;
			}		
			return tortoise;
			}
		}
		(hare->next) ? hare = hare->next: hare = nullptr;
		(tortoise->next) ? tortoise = tortoise->next:tortoise=nullptr;
	}
	return nullptr;
}
```
# See next

[Chapter 3 - Queue and Stack](../Notes/Chapter%203%20-%20Queue%20and%20Stack.md)