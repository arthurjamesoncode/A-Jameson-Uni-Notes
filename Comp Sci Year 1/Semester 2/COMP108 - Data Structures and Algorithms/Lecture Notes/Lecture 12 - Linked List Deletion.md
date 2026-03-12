## Deletion of the First Node
Consider the task of designing an algorithm to remove the first node of a linked list, and return the node.

How can we do this? Our answer is going to differ slightly depending on if our list is **singly** or **doubly** linked. First, we'll consider a **singly** linked list.

To delete a node from a linked list means to remove the pointers that allow us to access this node, and the pointers on the node which allow us to access the rest of the list. 

So if we are removing and returning the first node of the list (`head`) we just need to reassign `head` to the next node in the list and remove the pointer from our old `head` which points to our new `head`.

We also need to consider the case that the list only contains 1 node. In this case, we must be careful to also reassign `tail` to `NIL` as well.

We can see the full pseudocode of this algorithm below:
```
List-Delete-Head(L)
begin
	node = head
	if node /= NIL then // list is empty
		STOP and return NIL
	endif
	
	head = head.next
	if head == NIL then // new list is empty
		tail = NIL 
	else
		node.next = NIL // seperates node from rest of list
	endif
	
	return node
end
```

If instead we have a doubly linked list, we do the same except that we need to be concerned with the `prev` pointers. All this means is that we need to remove (set to `NIL`) the `prev` of the node just after head, as long as it exists.

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

The most important part of this algorithm is the order of the operations. If you reassign `head` before assigning `node` then you won't return the correct node, and would cut off access to the rest of the list when reassigning `node.next`. You also cut off access to the rest of the list if you reassign `node.next` to `NIL` before reassigning `head` to `head.next`. 

You can observe that the big-O of these algorithms is $O(1)$

>This is slightly outside the scope of this module but in terms of implementing a linked list in code, most languages have garbage collection. That means that after access to the node is removed the space in memory will be freed up. In a language without garbage collection, you would need to free up the memory manually.
>
>As these are low-level implementation details, we don't worry about them for the purposes of this module. But if you want to read more about garbage collection, you can visit [here](https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)).
## Deletion of the Last Node
Now lets consider if instead we want to delete the last node from a given list.

Again, the algorithm to do this depends on whether we have a **singly** or **doubly** linked list. First we'll consider a **singly** linked list.

So what does deleting mean in this case? 

If the list is empty, we don't need to do anything and we can just return `NIL`. Similarly if our list only has one node, then we just need to set `head` and `tail` to `NIL` and return `node`.

Otherwise, we know our last node is `tail` and is only pointed to by a single node. To delete our last node, we need to set the `next` pointer of the second last node to `NIL` and set `tail` to our second last node. So how can we access this second last node?

Unfortunately, since we are using a singly linked list, we don't actually have a way to access the second last node without **traversing** our list. This means we won't be able to make an algorithm that can delete the last element in constant time.

The full pseudocode for this algorithm is below
```
List-Delete-Tail(L)
begin
	node = tail
	
	if node == NIL then
		STOP and return NIL
	endif
	
	curr = head
	if curr.next == NIL then
		head = NIL
		tail = NIL
		STOP and return curr
	endif
	
	while curr.next /= tail then
		curr = curr.next
	endwhile
	
	curr.next = NIL
	tail = curr
	
	return node
end
```
As said above, there is no way to do this algorithm in constant time. Since, in the worst case, we traverse the whole list up to the tail this algorithm has a big-O of $O(n)$.

If, instead, we have a doubly linked list then we actually can make this algorithm happen in constant time. We can do this by making use of the `prev` pointer of `tail` to get the second to last node.

You can see the full pseudocode below:
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
As said above this algorithm has a big-O of $O(n)$.
## Deletion of a Middle Node
How about if we wanted to delete a node from the middle of the list, pointed to by `curr`? For simplicities sake we are going to assume that `curr` is never the `head` or `tail`, meaning it always has at least one successor and one predecessor, and that `curr` is always in the list.

Again this depends on if we've got a **singly** or **doubly** linked list, and again we will start by considering a singly linked list.

So what does it mean to delete `curr`? `curr` is pointed to by the node directly before it, and it points to the node directly after it. We need to reassign the pointer of the node directly behind `curr` to point at the node directly after `curr`. 

So how do we access the node directly behind `curr`? We have to traverse the list (since we don't have a `prev` pointer), so we can't do this in constant time.

You can see the full pseudocode below:
```
List-Delete(L, curr)
begin
	node = head
	
	while node.next /= curr do
		node = node.next
	endwhile
	
	node.next = curr.next
	
	curr.next = NIL
	
	return curr
```
As said above this is in **linear** time, not constant time. So the big-O of this algorithm is $O(1)$.

If we have a **doubly** linked list then we no longer need to traverse the list. We can access the node before `curr` by using `curr.prev`.

You can see how this algorithm works below
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
