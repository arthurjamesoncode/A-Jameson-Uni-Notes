## Building Data Structures
Arrays allow us access to any item in constant time. Sometimes, the ability to access any specific element can make writing programs messy.

That's why we use arrays to build other data structures that can only be accessed and added to in specific ways. This increased level of abstraction allows us to trust that the content of these data structures behave in some specific way, and implicitly stops attempts to access or change these arrays in any way other than this specific way.

Two common, simple data structures we might use when building programs are **queues** and **stacks**.
## Queues
Queues are a "First In First Out" **(FIFO)** data structure. This means that only the first element added to the queue can be accessed or removed from the queue.

Queues are used for many things:
- Customers waiting in line to be served
- Printing jobs to be completed
- Packets arriving at a router

Typically, queues only have two operations:
- **Enqueue** - Adds an item to the back of the queue (to its **tail**)
- **Dequeue** - Remove the first item (from its **head**) from the queue and return the value
These are the only operations we are concerned about on this course, but there may be others you see when dealing with queues. For example "Peek", which looks at the head of the queue without removing it.

A queue can be implemented using an array `Q[1..n]` with two pointer variables `head`, `tail`:
- `Enqueue` would save the data to `Q[tail]` and then increment `tail` by 1.
- `Dequeue` would retrieve the data from `Q[head]` and then increment `head` by 1.
Note that we would need to check if the array `Q[]` is full before enqueuing or empty before dequeuing as in either case they would not be able to perform the operation.

You can see an example of how this would work below.
![[queue_example.png]]
### Pseudocode
If we assume `n` to be infinite then we could implement **enqueue** operation like so
```
Enqueue(Q, x)
begin
	Q[tail] = x
	tail = tail + 1
end
```
and we can implement the **dequeue** operation like so
```
Dequeue(Q)
begin
	if head == tail then
		output "Queue is Empty"
	else
		x = Q[head]
		head = head + 1
		return x
	endif
end
```

What if `n` isn't infinite?

The first consequence of this is that our queue can now be full, and so we must check that array is full before we add anything to the queue.

The next consequence is, now that space matters, whenever we dequeue something, the space it took at the front of the array is wasted, and we will want to reuse it.

To do this we want to wrap around to the beginning of the queue. We can do this by using modulo operations (in this case `%`) to give us the remainder of dividing by `n`. If our `Q[]` was 0 indexed we could just use `head = (head+1)%n` and `tail = (tail+1)%n`, in order to increment head and tail. Since we are 1 indexed, we must instead must wrap around using a condition.

We also must consider how we will recognise if our queue is full. We can't use `tail == head` because we use `head == tail` to check if our queue is empty and using that condition would make it so our queue would be empty and full at the same time. 

Instead we use the condition `tail + 1 == head` (with some conditioning to allow for wrapping around). This is our only real option (without adding full and empty flags), but technically means that our queue can only ever hold `n-1` items, despite having an array of size `n` to store items in.

Now, with this in mind, we can represent our **enqueue** operation like so:
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
and we can implement our **dequeue** operation like so:
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
## Stacks
Stacks are "Last In First Out" **(LIFO)** data structures. This means that only the last element added to the stack can be accessed or removed.

Stacks are used for many things:
- Keeping a stack of plates
- Allocating memory to procedures
- Mathematical operations

They typically only have two operations:
- **Push** - add an element to the top of the stack
- **Pop** - access and remove the element currently on top of the stack
These are the only operations we are concerned about on this course, but there may be others you see when dealing with stacks. For example "Peek", which looks at the top of the stack without removing it.

A stack can be implemented using an array `S[1..n]` with a pointer variable `top`:
- `Push` would save the data to `S[top]` and then increment `top` by 1.
- `Pop` would retrieve the data from `S[top]` and then decrement `top` by 1.
Note that we would need to check if the array `S[]` is full before pushing or empty before popping as in either case they would not be able to perform the operation.

You can see an image of how this would work below.
![[stack_example.png]]
### Pseudocode 
You can see pseudocode for how we could implement this below.
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
