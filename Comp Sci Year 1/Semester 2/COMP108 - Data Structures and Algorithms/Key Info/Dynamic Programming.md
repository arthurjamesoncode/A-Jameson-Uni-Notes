## Key Definitions
A **dynamic programming** algorithm is an algorithm which works by storing previous results so that they don't need to be recomputed.

**Memoisation** means storing the results of calling a pure function with specific arguments, such that when the function is called again it doesn't need to recompute them.

A **memoised** function is a function which uses memoisation.

>In the slides Prudence says **memorisation** instead of **memoisation**. I don't think that's right but it doesn't really matter. I'm putting the link to the [Wikipedia page](https://en.wikipedia.org/wiki/Memoization) for memoisation just to back myself up.
## Dynamic Fib
**Top Down (Memoised/Recursive):** $O(n)$
```
Wrapper(n)
begin
	table = [0..n]
	table[0] = 1
	table[1] = 1
	
	for i = 2 to n do
		table[i] = -1
	endfor
	
	return Fib(n)
end

Fib(n)
begin
	if table[n] = -1 then
		table[n] = Fib(n-1) + Fib(n-2)
	endif
	
	return table[n]
end
```

**Bottom Up (Iterative):** $O(n)$
```
Fib(n)
begin
	table = [0..n]
	table[0] = 1
	table[1] = 1
	
	for i = 2 to n do
		table[i] = table[i-1] + table[i-2]
	endfor
	
	return table[n]
end
```

Both of these implementations are $O(n)$ time complexity, and are both examples of dynamic programming, however the **iterative solution** is roughly twice as fast.
## Assembly Line Scheduling
Problem "There are 2 assembly lines with $n$ stations which feed into each other.

$S_{i,j}$ denotes station $j$ on line $i$. $S_{1,j}$ and $S_{2,j}$ perform the same task but the time taken is different. The input is first fed into $S_{1, 1}$ or $S_{2,1}$ and must be fed into one of $S_{1, j}$ and $S_{2, j}$ for all $j\leq n$.

The assembly time at station $S_{i, j}$ is denoted by $a_{i,j}$. After each machine $S_{i,j}$, the input can either be instantly fed into the next machine on line $i$ (the current line), or transferred to the other line, but this takes some time. The time to transfer from $S_{i,j}$ is denoted by $t_{i,j}$."

![[assembly-line.png]]

Our algorithm works by forming a table of the minimum time to reach each point in the assembly line, along with the machine it came from.

$n$ is the number of machines in any given line.

**Pseudocode:** $O(n)$
```
m1[1] = a1[1]
m2[1] = a2[1]

for j = 2 to n do
	m1[j] = min(m1[j-1] + a1[j], m2[j-1] + a1[j] + t2[j-1])
	m2[j] = min(m2[j-1] + a2[j], m1[j-1] + a2[j] + t1[j-1])
endfor

return min(m1[n], m2[n])
```

While time complexity is $O(n)$ when we have a fixed number of lines, if we have $m$ lines the time complexity becomes $O(m^2n)$. 

This is because the time taken to find the minimum of $m$ values is now $O(m)$, and instead of having $2n$ (or some other constant times $n$) machines we have $mn$ machines.