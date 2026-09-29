## Proof By Induction
When we create algorithms, we often write processes that need to be repeated. These processes can be very important, so how can we prove that our algorithms do what we want it to do.

The way to do this is by proof by induction. This kind of proof works by showing some property holds for some state/number, and then showing that, if that property holds for that state/number, it also holds for the direct successor of that state/number.

Essentially, you prove that if a property holds up to state $k$, then it also holds for state $k+1$.

>Proof by induction will be briefly recapped here but if you want some more examples of proof by induction look to [[Lecture 8 - Indirect Proof Continued and Proof By Induction]] and it's successive lectures from the COMP109 module.

Proof by induction has 2 main steps:
- **Base Case** - Show that some property holds for some state, for example $n=1$.
- **Inductive Step/Hypothesis** - Assuming that a property holds for $n=k$, show that the property must hold for $n=k+1$. 

Using proof by induction allows us to show that a property holds for all $n$ greater than our base case. So if our base case is $n=1$, then we can prove that it holds for all $n\geq 1$.
## Proving Correctness of Programs
In order to prove the correctness of a program containing a loop we need to use an **invariant**, which results in the **consequence** we want.

The **invariant** is some property that holds at the end of every loop iteration. Once we've identified our invariant we can then prove it using induction and therefore prove our **consequence**.

The rest of this note will be running over examples, and the proof will always follow the same structure.
### Example 1 - Summing an Array
Consider the algorithm below:
```
// summing all elements of an array 
sum ← 0
i ← 1 

while i ≤ n do 
begin 
	sum ← sum + A[i]
	i ← i + 1 
end 

output sum
```

How can we prove that this program computes the **sum** of all values in the array?

First, let's identify the **consequence** we want to prove, which is "At the end of the last loop iteration `sum` holds the value `A[1]+...+A[n]`."

This lets us find our invariant which is "At the end of each loop iteration the value of `sum` holds the value `A[1]+...+A[i-1]`." 

We know that, as `i = n+1` is the value of `i` at the end of the loop, our **invariant** being true results in our **consequence** being true, and so we can prove our invariant by induction like so.

**Invariant:**
	At the end of each loop iteration the value of `sum` holds the value `A[1]+...+A[i-1]`.

**Base Case:** At the end of the first iteration.
	When the loop begins the value of `i` is 1 and the value of `sum` is 0. 
	Inside the loop we assign sum to the value of `sum + A[i]`, and then increment `i` by 1. 
	This means that at the end of the loop `sum` holds the value of `0 + A[1]` and `i == 2`. 
	This shows that our invariant is true at the end of the first iteration.

**Inductive Step:** 
	Assume that the invariant holds for index $i=k\leq n$. This means that at the start of our loop `sum` holds the value of `A[1]+...+A[k-1]`
	Inside of our loop we set sum to the value of `sum + A[k]` and then increment `i` by one.
	This means that at the end of our loop iteration `sum` holds the value `A[1]+...+A[k-1]+A[k]` and `i==k+1` meaning that if our invariant holds for $i=k\leq n$ then it also holds for $i=k+1$.

**Conclusion:** 
	As we have shown that our invariant holds at the end of the first loop iteration, and also proven it holds during our inductive step we know the invariant must hold at the end of the last loop iteration.
	Since the loop ends when `i == n+1` we know that the `sum` holds the value of `A[1]+...+A[n]` at the end of the loop.
	Therefore we can conclude that our program outputs the sum of the elements of the array.

You can see the structure of the proof follows this skeleton:
- State the **invariant** you will prove
- Prove the **invariant** is true for the **base case** (usually at the end of the first iteration)
- Prove that, if the **invariant** is true for $i=k$, then it will also be true for $i=k+1$ (**inductive step**).
- Write a **conclusion** explaining what you have proven, and how the **invariant** holding at the end of the loop proves the correctness of the program.
### Example 2 - Finding 1st and 2nd Maximum of an Array
Consider the algorithm below:
```
M1 ← max(A[1], A[2]) 
M2 ← min(A[1], A[2]) 
i ← 3 

while i ≤ n do 
	if A[i] > M1 then 
		M2 ← M1 
		M1 ← A[i] 
	else if A[i] > M2 then 
		M2 ← A[i] 
	endif
	
	i ← i + 1 
endwhile
	
output M1 and M2
```

How can we prove that this algorithm outputs the **first and second maximums** of the array?

Well first lets identify what **invariant** results in the **consequence** we want. 

We output `M1` and `M2` straight after the loop so we want the **consequence** of the invariant to be "At the end of the last iteration `M1` holds the maximum value, and `M2` holds the second maximum, of `A[1..n]`".

As $i=n+1$ at the end of the loop, the **invariant** we want to prove is "At the end of each iteration `M1` holds the maximum value, and `M2` holds the second maximum, of `A[1..(i-1)]`".

Now that we have our **invariant** we can prove the correctness of this by induction like so:

**Invariant:** 
	At the end of each iteration `M1` holds the maximum value, and `M2` holds the second maximum, of `A[1..(i-1)]`

**Base Case:** At the end of the first iteration
	Before the start of the loop `M1` is initialised to the maximum of `A[1]` and `A[2]`, `M2` is initialised to the minimum of `A[1]` and `A[2]`, and `i` is initialised to `3`.
	Inside the loop if `A[i]` (`A[3]`) is greater than `M1`, then `M2` becomes `M1` and `M1` becomes `A[3]`. 
		This makes `M1` the maximum, and `M2` the second maximum, of `A[1..3]`.
	Otherwise if `A[3]` is greater than `M2`, but less than `M1`, then `M2` becomes `A[3]`. 
		This also makes `M1` the maximum, and `M2` the second maximum, of `A[1..3]`.
	If neither of those conditions are true then we do nothing. 
		This means that `M1` and `M2` were already the maximum of `A[1..3]`
	Before the loop ends `i` is incremented by `1` and so at the end of the first loop `i==4` and `M1` and `M2` are the maximum and second maximum of `A[1..3]`.
	Hence our invariant holds for the base case.

**Inductive Step:**
	Assume the invariant holds for $i=k\leq n$. This means that `M1` and `M2` are the maximum and second maximum of `A[1..(k-1)]`.
	Inside the loop, if `A[k] > M1` then `M2` takes the value of `M1` and `M1` takes the value of `A[k]`. 
		In this case `A[k]` is the maximum over `A[1..k]` and `M1`'s original value is the second maximum. 
		So after the reassignments it must be the case that `M1` and `M2` are the maximum and second maximum over `A[1..k]`
	If, instead, `A[k] > M2` but not greater than `M1` then `M2` takes the value of `A[k]`. 
		In this case `A[k]` is the second maximum over `A[1..k]` so after the reassignment it must be the case that `M1` and `M2` are the maximum and second maximum over `A[1..k]`
	If `A[k] < M2` then we do nothing.
		In this case `M1` and `M2` are still the maximum and second maximum over `A[1..k]`
	Before ending the loop we increment `i` by `1` and so at the end of this loop iteration `i==k+1` and `M1` and `M2` are the maximum and second maximum of `A[1..k]`
	Hence our invariant holds for the inductive step.

**Conclusion:**
	As we have shown that our invariant holds for both the base case and inductive step, this means that the invariant must hold when the loop exits.
	As the loop exits when `i==n+1` it must be the case that `M1` and `M2` are the maximum and second maximum of `A[1..n]`.
	Therefore, we can conclude that this program outputs the maximum and second maximum of the array `A`.

### Example 3 - Binary Search
Consider the following algorithm:
```
min = 1
max = n //length of A
found = false

while (NOT found) AND min <= max do
	mid = (min + max)/2 truncated to an integer
	if A[mid] == key then
		found = true
	else if A[mid] < key then
		max = mid - 1
	else 
		min = mid + 1
	endif
endwhile

output found
```

How can we prove that this algorithm always returns `true` if `key` exists in the array and `false` if it does not exist?

This one is tricky, but let's start by figuring out what needs to be true. 

Our consequence is "When the loop ends, it is either because `key` has been found and `found` is set to true, or the `key` is not in the array and `min > max`."

Our invariant here is a bit trickier, the thing that results in our **consequence** being true is that "At the beginning of each loop iteration, if `key` is in `A` then it is in `A[min..max]`."

We now actually use the invariant to prove a **claim** that "If the invariant holds, the algorithm correctly finds the key".

Now, our base case is a little different as well. We don't start at the beginning of this loop and perform induction on the loop iteration itself, we start with an array of length `1`, and then perform induction on the size of the portion of the array we are looking at. So our base case is `n=max-min+1=1`.

We also must perform **strong induction** to prove this. Have a look at [[Lecture 9 - Proof By Induction Continued]] if you want to see/remind yourself what this is. It's very similar to normal induction.

So now we can write our proof:

**Invariant:** At the beginning of each loop iteration, if `key` is in `A` then it is in `A[min..max]`.

**Claim:** If the invariant holds, the algorithm will correctly find the key

**Base Case:** $n=1$
	When $n=1$, `min==max`. So if `key` is in `A` then it is in `A[min]` or equivalently `A[max]`, so therefore the invariant holds.
	If `key` is in `A` then `key==A[mid]` will be true and `found` will be set to true, causing the loop to exit and return `true`.
	If `key` isn't in `A` then `k==A[mid]` will be false and `min` and `max` will be updated so that `min > max` and the loop will exit and return `false`.
	Therefore the **claim** is true when $n=1$.

**Inductive Step:**
	Assume the claim is true for `max-min+1` being all values in `1..(n-1)`.
	Let `max-min+1=n`.
	If `key == A[mid]`
		`found` is changed to true, breaking the loop and returning `true` correctly
	If `key < A[mid]`
		then if `key` exists, it will be in `A[min..(mid-1)]`, meaning that after changing the value of `max` to `mid-1` the invariant will hold for the next iteration.
		As we are left with strictly smaller array ranges, our assumption that the claim is true for `max-min+1` being all values in `1..(n-1)` implies that the claim is true for `max-min+1=n`
	If `key > A[mid]`
		then if `key` exists, it will be in `A[(mid+1)..max]`, meaning that after changing the value of `min` to `mid+1` the invariant will hold for the next iteration.
		As we are left with strictly smaller array ranges, our assumption that the claim is true for `max-min+1` being true for all values in `1..(n-1)` implies that the claim is true for `max-min+1=n`

 **Conclusion:** 
	 As the **claim** is true for both our base case and our inductive step, we can conclude that this algorithm will output `true` when `key` exists in `A` and `false` when it does not.