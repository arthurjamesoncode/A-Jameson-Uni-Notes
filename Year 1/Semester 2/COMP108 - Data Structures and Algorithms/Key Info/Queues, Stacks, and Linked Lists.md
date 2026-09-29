## Key Definitions

A **queue** is a first in first out (FIFO) data structure.

A **stack** is a last in first out (LIFO) data structure.

A **singly linked list** is a list data structure where every element carries a pointer to the next element, as well as some data value.

A **doubly linked list** is a list data structure where every element carries a pointer to the next and previous element.
## Queue Properties & Operations
Queue's can be implemented internally as an array with the attached pointers:
- `head` points to the item at the front of the queue
- `tail` points to the index after the item at the back of the queue
Assume the internal array implementation is 1 indexed, not 0 indexed.

**Enqueue:** Add an item to the back of the queue $O(1)$
```
Enqueue(Q, x)
begin
	nextTail = tail + 1
	if nextTail > n then
		nextTail = nextTail % n
	endif
	
	if nextTail == head then
		output "Queue is Full"
	else
		Q[tail] = x
		tail = nextTail
	endif
end
```

**Dequeue:** Remove an item from the front of the queue $O(1)$
```
Dequeue(Q)
begin
	if head == tail then
		output "Queue is Empty"
	else
		x = Q[head]
		nextHead = head + 1
		if nextHead > n then
			nextHead = nextHead % n
		endif
		
		head = nextHead
		return x
	endif
end
```

>Note that, since the indexes wrap around, we need a way to differentiate when the queue is full from when it is empty. 
>
>We can do this by using `nextTail == head` for full and `tail == head` for empty. This does mean a queue implemented with an array of size $n$ can only store $n-1$ elements.
## Stack Properties & Operations
A stack can be internally represented by an array with the attached pointer: `top` which is the index of the current top of the stack.

Assume the internal array implementation is 1 indexed, not 0 indexed.

**Push:** Add something to the top of the stack $O(1)$
```
Push(S, x)
begin
	if top == n then
		output "Stack is Full"
	else
		top = top + 1
		S[top] = x
	endif
end
```

**Pop:** Remove the top item from the stack $O(1)$
```
Pop(S)
begin
	if top == 0 then
		output "Stack is Empty"
	else
		x = S[top]
		top = top - 1
		return x
	endif
end
```
## Linked List Properties & Operations
Linked lists can be implemented as a series of **nodes** which have the following properties:
- `data` - The data the list node stores
- `next` - A pointer to the next list node
- `prev` - A pointer to the previous list node
`prev` would not exist in a singly linked list.

>Prudence seems to pretty much only work with doubly linked lists in exam questions, so I am (mostly) only going to refer to doubly linked lists from now on.

The linked list itself will have the properties:
- `head` - A pointer to the first item in the linked list 
- `tail` - A pointer to the last item in the linked list

Let $n$ be the size of the input list for all operations below.
### Traversing/Searching
**Traversing a linked list from the head:** $O(n)$
```
node = head
while node /= NIL do
	output node.data
	node = node.next
endwhile
```

**Traversing a doubly linked list from the tail:** $O(n)$
```
node = tail
while node /= NIL do
	output node.data
	node = node.prev
endwhile
```

**Searching an unsorted list:** $O(n)$
```
node = head

while node /= NIL AND node.data /= key do
	node = node.next
endwhile

output (node /= NIL)
```

**Searching a sorted list (ascending):** $O(n)$
```
node = head

while node /= nill AND node.data < key do
	node = node.next
endwhile

output (NOT node == NIL) AND (node.data == key)
```
You can change to the `>` sign to search a list sorted in descending order.
### Deleting
**Deleting the head of a linked list:** $O(1)$
```
List-Delete-Head(L)
begin
	node = head
	if node == NIL then // list is empty
		STOP and return NIL
	endif
	
	head = head.next
	if head == NIL then // list had one node
		tail = NIL
	else
		head.prev = NIL // no longer points at node
		node.next = NIL // seperates node from rest of list
	endif
	
	return node
end
```

**Deleting the tail of a doubly linked list:** $O(1)$
```
List-Delete-Tail(L)
begin
	node = tail
	
	if node == NIL then
		STOP and return NIL
	endif
	
	if node.prev == NIL then
		head = NIL
		tail = NIL
	else
		node.prev.next = NIL
		tail = node.prev
		node.prev = NIL
	endif
	
	return node
end
```
If this is instead a singly linked list, you must first traverse the list to find the second to last element meaning that it will have time complexity of $O(n)$ in that case.

**Deletion of node in the middle:** $O(1)$ given `curr`
```
List-Delete(L, curr)
begin
	nextNode = curr.next
	lastNode = curr.prev
	
	nextNode.prev = lastNode //No longer points to curr
	lastNode.next = nextNode //No longer points to curr
	
	curr.next = NIL
	curr.prev = NIL
	
	return curr
end
```
If not given `curr` and instead asked to delete a node based of position or `data` instead, the time complexity will be $O(n)$ since they must traverse the list to find a value for `curr`.
## Inserting
**Adding an element to the front of the list:** $O(1)$
```
List-Insert-Head(L, node)
begin
	node.next = head
	node.prev = NIL
	
	if head == NIL then
		tail = node
	else
		head.prev = node
	endif
	
	head = node
end
```

**Adding an element to the end of the list:** $O(1)$
```
List-Insert-Tail(L, node)
begin
	node.next = NIL
	node.prev = tail
	
	if tail == NIL then
		head = node
	else
		tail.next = node
	endif
	
	tail = node
end
```

**Inserting an element in the middle of a list:** $O(1)$ given `curr`
```
List-Insert-Curr(L, curr, node)
begin
	node.next = curr.next
	node.prev = curr
	curr.next.prev = node
	curr.next = node
end
```

**Inserting an element in the middle of sorted linked list while maintaining the order:** $O(n)$
```
List-Insert-Sorted(L, node)
begin
	if head == NIL then
		head = node
		tail = node
		STOP
	endif
	
	if head.data >= node.data then
		List-Insert-Head(L, node)
		STOP
	endif
	
	if tail.data <= node.data then
		List-Insert-Tail(L, node)
		STOP
	endif
	
	curr = head
	while curr.next.data < node.data do
		curr = curr.next
	endwhile
	
	List-Insert-Curr(L, curr, node)
end
```
### Note on Linked List Questions
Prudence likes to ask questions about the order of operations when inserting or deleting a node. I find that in an exam the best strategy for this is to just draw physical lines representing the pointers and go through the operations in the orders given to see if any match.

