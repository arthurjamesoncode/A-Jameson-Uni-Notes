## Question 1

Consider the following algorithm.
```
// Assume n is a given integer being power of 2
count ← 0
x ← n

while x > 1 do
begin
	x ← x/2
	count ← count + 1
end

output count
```
### (a)
**Question:** Give the trace table and the output when $n=32$.

**Answer:**

| iteration   | x   | count |
| ----------- | --- | ----- |
| before loop | 32  | 0     |
| 1           | 16  | 1     |
| 2           | 8   | 2     |
| 3           | 4   | 3     |
| 4           | 2   | 4     |
| 5           | 1   | 5     |
### (b)
**Question:**  In general, how many times the while loop is executed for input n being a positive power of 2 (e.g. when $n = 2, 4, 8, 16, 32, 64, . . .$)?

**Answer:** The while loop is executed $log_2(n)$ times.
## Question 2

**Question:** Write a pseudo code of a while-loop to find the sum of all multiples of $3$ between $x$ and $y$ inclusively. You can assume that $0 < x ≤ y$. For example, if $x = 4$ and $y = 12$, then your pseudo code should output $27$ (which equals to $6 + 9 + 12$).

**Answer:**
```
num = x
remainder = num % 3

if remainder /= 0 then
	num = num + 3 - remainder
endif

sum = 0
while num <= y do
	 sum = sum + num
	 num = num + 3
endwhile

output sum
```
## Question 3
**Question:**  A prime number is a number that can be divisible by 1 and itself only. Write a pseudo code of an algorithm to determine if a positive integer $x > 1$ is a prime number or not.

**Answer:**
```
i = 2
prime = true

while prime AND i <= x/i do
	if x % i == 0 then
		prime = false
	else
		i = i + 1
	endif
endwhile

output prime
```

We can use `x/i` as our endpoint since factors always come in pairs. If `i` is a factor `x/i` must be as well. As we are checking values of `i` in ascending order, this means that as soon as `x/i > i` we have checked 1 value out of all possible factor pairs and, if none were found to be factors, we know that `x` is prime.