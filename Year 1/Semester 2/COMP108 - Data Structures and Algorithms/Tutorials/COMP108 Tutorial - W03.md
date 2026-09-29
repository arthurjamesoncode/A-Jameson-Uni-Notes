## Question 1
State the order of growth of the following functions in big-O notation. For example, the function $3n$ is $O(n)$. Remember you need to write the big-O notation.
### (a)
**Question:**
$$
10 + 3n + 2n^2 + n^4 + 5n^3
$$
**Answer:** $O(n^4)$
### (b)
**Question:** 
$$
5 + 3n^3 + 2n^2 \log n + 5n + 2n^2
$$
**Answer:** $O(n^3)$
### (c)
**Question:**
$$
\sqrt{n^5} + n^3
$$
**Answer:** $O(n^3)$
## Question 2
Consider each of the following algorithms. What is the time complexity in big-O notation? Give justifications. 

Note: If two loops are run one after another, the overall time complexity is the sum of the complexities of the two loops.
### (a) 
**Question:**
```
// Assume n and m are given positive integers 
x ← n 
while x > 1 do 
	x ← x − 2 
for y ← 1 to m do
	output y
```

**Answer:** The first while loop takes $n/2$ operations, as $x$ starts at $n$ and decreases by 2 every time. The second loop takes m operations. So the full number of operations is $\frac n2+m$, giving this algorithm a big-O of $O(n+m)$.
### (b)
**Question:**
```
// Assume n is a given positive integer being power of 2 
count ← 0 
x ← n 

while x > 1 do 
begin 
	x ← x/2 
	count ← count + 1 
end 

output count
```

**Answer:** Since $x$ is a power of 2, and the value of $x$ is halved each iteration it will end when $x=1$ after exactly $\log_2 n$ iterations. Giving this algorithm a big-O of $O(\log n)$.
### (c)
**Question:**
```
// Assume n is a given positive integer being power of 2
x ← n 
y ← n 
while x > 1 do 
	x ← x − 2 
while y > 1 do
	y ← y/2
```

**Answer:** The first loop takes exactly $\frac n2$ operations, the second loop takes exactly $\log_2 n$ operations, so the total number of operations of the algorithm is $\frac n2 + \log_2 n$ operations. We can get the big-O of this by taking the biggest $n$-term $(\frac n2)$, and ignoring constants. So the big-O of this algorithm is $O(n)$.
### (d)
**Question:**
```
// Assume n and m are given positive integers 
x ← n 
while x > 1 do 
begin 
	x ← x − 2 
	for y ← 1 to m do 
		output y
end
```

**Answer:** The outer while loop will execute $\frac n2$ times as $x$ starts at $n$ and decreases by 2 every time. The inner loop executes $m$ operations every time it occurs inside of the outside loop, and so this algorithm executes $\frac{nm}2$ operations, giving it a big-O of $O(nm)$
### (e)
**Question:**
```
// Assume n and m are given positive integers 
x ← n 
while x > 1 do 
begin 
	if x == n then 
	begin 
		for y ← 1 to m do 
		begin 
			output y 
		end 
	end 
	x ← x − 2
end
```

**Answer:** The outer loop executes the statements within its block $\frac n2$ times as $x$ starts at $n$, ends at 1 and decreases by 2 each iteration. The inner loop, executes $m$ operations each time, however as it only occurs when `x == n` it only executes once, at the beginning of the outer loop. So the total number of operations is $\frac n2 + m$, giving this algorithm a big-O of $O(n+m)$.
### (f)
**Question:**
```
// Assume n is a given positive integer being power of 2 
x ← 1 
while x ≤ n do 
begin 
	x ← x + 3 
	y ← 1 
	while y ≤ n do 
	begin 
		y ← y ∗ 2 
	end
end
```

**Answer:** The outer loop executes the statements within it's block a total of $\frac n3$ times, as $x$ starts at 1, ends at $n$ and increases by 3 each iteration. The inner loop executes $\log_2 n$ operations every time the outer loop runs. We know this because $y$ starts at 1 and ends at $y$ (or the first power of 2 greater than $y$), and doubles every time. This means that the algorithm executes a total of $\frac n3\log_2 n$ operations, giving it a big-O of $O(n\log n)$.
### (g)
**Question:**
```
// Assume n and m are given positive integers 
for x ← 1 to n do 
begin 
	for y ← 1 to m do 
	begin 
		for z ← 1 to n do 
		begin 
			output x + y + z 
		end 
	end
end
```

**Answer:** The outermost loop executes the inner 2 loops $n$-times. The middle loops executes the innermost loop $m$-times. The innermost loop executes $n$ operations. This means that the total number of operations is $n\cdot m\cdot n=n^2m$, giving this algorithm a time complexity of $O(n^2m)$.