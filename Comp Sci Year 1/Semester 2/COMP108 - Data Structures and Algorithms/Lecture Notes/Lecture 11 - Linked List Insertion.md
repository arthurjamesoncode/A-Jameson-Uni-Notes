## Insertion of a Node to the Front of a List
When we use a linked list, how can we insert a node to the front of the list.

Our answer here differs a little depending on if it's a **singly** or **doubly** linked list. First, lets consider a **singly** list list.

Since we are adding this to the head of the list, we mainly need the `head` of the list and our `node` to add, but we do still need the tail.

No matter what we are going to set `node.next` to the current `head`.

Then we need to check if `head == NIL`. If true, the list is empty and we need to set tail to our node. If the `head` is not `NIL` then we don't need to do anything else.

Be careful here, if we reassigned `head` before we set `node.next = head` then we would lose access to the rest of our list. We would have a broken list.

```
List-Insert-Head(L, node)
begin
	node.next = head
	
	if head == NIL then
		tail = node
	endif
	
	head = node
end
```

If, instead, we we're dealing with a **doubly** linked list we do more or less the same thing. We just need to also set `head.prev` to our new node, and set `node.prev` to `NIL`

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

As you can see, neither of the algorithms provided contain any kind of loop. This means that the number of operations to perform these algorithms is constant.

This gives inserting to the head of a linked list a big-O of $O(1)$.
## Insertion to the Tail of a Linked List
How about if we want to insert to the tail of a linked list?

Well again the process differs a little bit depending on if we have a **singly** or a **doubly** linked list. Again, lets start by considering a **singly** linked list.

First, we will always need to set `node.next` to `NIL` as we know there will be no successors. We will also always be setting `tail` to `node`, but we must do that after everything else to preserve the information of the list and stop it from breaking.

Then we need to check if `tail` is `NIL`. If it is, then we know the list is empty and we will also set `head` to node in addition to `tail`. If it isn't, we must set `tail.next` to `node`.

You can see the full algorithm below
```
List-Insert-Tail(L, node)
begin
	node.next = NIL
	
	if tail == NIL then
		head = node
	else
		tail.next = node
	endif
	
	tail = node
end
```

If we have a doubly linked list the process is very similar. The only difference is that we need to set `node.prev` to `tail`.

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

The algorithms to insert to the the tail of linked list are very similar to the ones to insert them to the head. Again, neither of these contain any kind of loop.

This gives inserting a node to the tail of a linked list a big-O of $O(1)$.
## Inserting a Node in the Middle of a Linked List
How about if, instead of at the head or tail of a list, we want to insert into the middle of a list. Let's say we want to insert after a node pointed to by `curr`.

You can see below an example of what we are trying to do (note that this example is a **doubly** linked list)
![[insertion_curr_linked.png]]

Again this algorithm will vary slightly depending on whether we have a **doubly** linked list or a **singly** linked list, and again we'll start with a **singly** linked list.

What will our new node need to point at to be in the correct position? Well, we know that it will need to point at the node that comes after `curr` which is `curr.next`.

Now we know what it is pointing at, what nodes will need to point at our new node? Again, this is easy, `curr` needs to point to our new node. so we need to set `curr.next` to `node`. We need to be careful that we set `node.next` to `curr.next` before we do this or we will end up with a broken list again.

You can see the full algorithm for this below
```
List-Insert-Curr(L, curr, node)
begin
	node.next = curr.next
	curr.next = node
end
```
This algorithm assumes that `curr` is not `NIL` and that it is not the `tail` of the list, meaning that it has nodes after it. 

If it was `NIL` it would cause an error, as `curr.next` would not exist/have a value. If it was `tail` it would cause issues as we wouldn't correctly reassign `tail`.

If we have a **doubly** linked list again this is similar, but we need to do a little more.

The only difference is we now need to be concerned about `prev` pointers. Our nodes `prev` pointer will need to point to `curr` as we know it comes after. We also know that we would need to set `curr.next.prev` to our node, as our node now comes directly before `curr.next`.

Note that we need to assign `curr.next.prev` before we reassign `curr.next` so that we don't break our list.

You can see the full version of this algorithm below:
```
List-Insert-Curr(L, curr, node)
begin
	node.next = curr.next
	node.prev = curr
	curr.next.prev = node
	curr.next = node
end
```
Again, This algorithm assumes that `curr` is not `NIL` and that it is not the `head` or `tail`. 

Like before if `curr` was `NIL` then we would get an error as `curr.next` would not exist. In addition, if `curr` is `tail`, then we will also get an error as `curr.next` would be `NIL` so `curr.next.prev` wouldn't exist.

Again both of these algorithms contain no loops, so they will complete in constant time. Giving them a big-O of $O(1)$
## Inserting into the Middle of a Sorted Linked List
Now consider if we want to insert into a sorted linked list and maintain the order. Now we don't know which node we want to insert after, and therefore we cant use the algorithms we already defined.

Let's consider a list which is sorted in **ascending** order, and a `node` which we want to insert. In this case, we need to traverse the list until we find a node `curr` for which `curr.data < node.data` and `curr.next.data > node.data`. Then we can insert using the algorithm above.

We do need to be careful now, our new `node` could need to be inserted at either the `tail` or the `head` so we need to check this as we go through our algorithm. We can actually reuse the algorithms we have already created, as long as we check certain conditions.

You can see the full pseudocode for this below, (note that `STOP` stops the execution of the whole algorithm):
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
This algorithm takes a sorted linked list and inserts a new node.

If the list is empty (`head == NIL`) then it just sets `head` and `tail` to `NIL`.

If `head.data >= node.data` then we know that our new node should become the head of this list and so we use our `List-Insert-Head` algorithm. Likewise if `tail.data <= node.data` then we know that our new node should be made the tail of the list and we use our `List-Insert-Tail` algorithm.

After the above conditions have been checked we know that the list has at least 2 nodes. This is because if it only had one then `head.data == tail.data` which would mean that at least one of `head.data >= node.data` or `tail.data <= node.data` would be true. 

This means we know both that `head.next /= NIL` and that at least `tail.data > node.data`. This allows us to set `curr` to `head` traverse the list until `curr.next >= node.data`. At the end of this loop `curr.data` will be the last piece of data in the list which is less than or equal to `node.data` and we can use our `List-Insert-Curr` algorithm.

In the worst case for this algorithm, the only value in the list which is greater than `node.data` is `tail.data`. In this case we have made $n+1$ comparisons (1 comparison against `head.data`, 2 comparisons against `tail.data` and 1 comparison against the data of all other nodes), which gives us a big-O of $O(n)$.

