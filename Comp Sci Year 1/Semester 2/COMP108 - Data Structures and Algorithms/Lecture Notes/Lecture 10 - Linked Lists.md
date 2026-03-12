## Linked Lists
Linked lists are a way of grouping data. The key point of a linked list is that, instead of indexing (as with arrays) each element has a data field with either 1 or 2 pointers which link it to the next or previous element of the list.

There are two types of linked linked lists:
- **Singly** linked lists have 1 pointer to the next element of the list
- **Doubly** linked lists have 2 pointers which point to the next and the previous element of the list.

We consider each element of the list as a **node**.
- To refer to the data contained in an element use `node.data`
- To refer to the next pointer use `node.next`
- To refer to the previous pointer use `node.prev`

If `node` is the last element of the list then `node.next == NIL`, and if `node` is the first element of the list then `node.prev == NIL`.

We call the first **node** of the list the **head** of the list, and the last node the **tail** of the list. 
- When `head` is referenced in pseudocode, it is a pointer to the **first** node of the list.
- When `tail` is referenced in pseudocode, it is a pointer to the **last** node of the list.

So in the example below of a doubly linked list we could say:
- `head.data == 15`
- `head.next.data == 10`   
- `tail.data == 20`
- `tail.prev.prev == head`
- `tail.next == NIL`
- etc.
![[doubly_linked_list_example.png]]
## Traversing a Linked List
Consider the task of designing an algorithm to traverse and output every element of the linked list.

How would we do this?

Well we can use a loop. Since we don't know how long a linked list is without traversing it, we must use a while loop. 

We can access the next node by using `node.next`, and we know that when `node.next` is `NIL` then we have reached the end of the list.

So with this we can write our pseudocode for traversing a linked list
```
node = head
while node /= NIL do
	output node.data
	node = node.next
endwhile
```
Pretty simple stuff.

If we instead wanted to traverse a doubly linked list from the tail we can do this by just changing 2 lines
```
node = tail
while node /= NIL do
	output node.data
	node = node.prev
endwhileprev
endwhile
```
## Searching Through a Linked List
Consider the task of designing an algorithm to determine if some data, called `key`, is present in a linked list.
### Unsorted List
If we assume an unsorted list we only really have one option. Which is to traverse the list while checking if each nodes `data` is the same as `key`.

```
node = head
found = false

while (NOT found) AND node /= NIL do
	if node.data == key then
		found = true
	else
		node = node.next
	endif
endwhile

output found
```

We have another way to do this as well, which is to add `node.data /= key` into our condition for the while loop.
```
node = head

while node /= NIL AND node.data /= key do
	node = node.next
endwhile

output (node /= NIL)
```
This second approach can cause problems depending on the way it is implemented. 

If `node /= NIL` being false doesn't cause the expression `node /= NIL AND node.data /= key` to immediately return `false` in a given programming language, it could attempt to evaluate `NIL.data` which would give an error, as that points to no value.

>Most modern, popular high level languages include "short circuiting" meaning that, if the part of a boolean expression that has been evaluated causes the whole expression to always be true or always be false, the rest of the boolean expression won't be evaluated.
>
>Essentially is a language has short circuiting then we get `true OR <code which will never run>` and `false AND <code which will never run>`. As if the first term of a `OR` expression is true it is always true, and if the first term of an `AND` expression is false it will always be false.
>
>Essentially in a language which has short circuiting then the second algorithm always works.

Both of these algorithms check every element (in the worst case) and so they both have a big-O of $O(n)$ where $n$ is the length of the linked list.
### Sorted List
What if the linked list is sorted?

If we were searching through a sorted array, then we could use binary search to quickly search through a list. Could we use the same trick with a linked list?

Unfortunately no. This is because arrays allow **instant random access**, meaning that we can instantly go to the `i`th position in an array. We use this in binary search to go to the midpoint of the array.

Linked lists, however, don't allow for **instant random access**. We only start with the `head` pointer (and maybe a `tail` pointer) and the only way to access the items in the list is to jump sequentially to the node stored in each nodes `next` or `prev` pointers. 

We don't even know the length of a linked list before we traverse it, so we couldn't calculate the midpoint even if we could access it easily.

But we can modify the algorithm in order to terminate the search slightly earlier.

A simple modification is to check is to compare the data of the current node with the key value:
- If the list is sorted in ascending order and `node.data > key` then the key cannot be in the list.
- If the list is sorted in descending order and `node.data < key` then the key cannot be in the list.

So we can add these conditions into our loop. Note I will be using the second, shorter form of the algorithm that requires short circuiting to work.

```
node = head

while node /= nill AND node.data < key do
	node = node.next
endwhile

output (NOT node == NIL) AND (node.data == key)
```

Now, in terms of time complexity of this search, we still have to check through every element of the array if `key` has a greater value than the last item of the array. So the big-O of this search is $O(n)$ where $n$ is the length of the list. 

We cannot do better than this when it comes to searching through a linked list.