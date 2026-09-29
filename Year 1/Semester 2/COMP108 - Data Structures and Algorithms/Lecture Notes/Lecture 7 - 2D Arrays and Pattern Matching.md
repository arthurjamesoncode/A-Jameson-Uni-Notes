## Using Nested Loops to Traverse 2D Arrays
### Problem 1
Consider the following problem.

"Input: Suppose we have data of the daily rainfall every day for a year. For simplicity this data is a 2D array where there are $d$ days in a month and $m$ months in a year.

Output: Find the maximum monthly average rainfall over a year.

How could you design an algorithm to compute this output given this input?"

To solve this problem, lets first outline what the data we have is.

We have our input which is an $m\times d$ 2D array of numbers, or an array of $m$ arrays which each contain $d$ numbers. We can call this array `rainfall`. If we want the array representing the $i$th month, we can write `rainfall[i]`, and if we want the value of the $j$th day in the $i$th month we can write `rainfall[i][j]`. 

The above syntax is a widely known and convenient way to show 2D array indexing. It is what I recommend you use when writing pseudocode.

Now we have our data, we want to calculate the average rainfall of each month and then output the maximum average value we find. 

[[Lecture 6 - Finding Min & Max of Arrays|Last lecture]], we worked to build an algorithm for finding the max or min of an array. We could use this to find the max value of our averages after we find the averages of each month. While this would work, it would require looping over our array again, and so it will be faster for us to just check it as we go along, using a similar algorithm.

Now we just need a way to find the average rainfall over a month. To do this we can use a loop to sum together all the values in a month and then divide the sum by $d$.

You can see the full pseudocode for this below
```
max_average = 0
for i = 1 to m do
	sum = 0
	for j = 1 to d do 
		sum = sum + rainfall[i][j]
	endfor
	
	average = sum / d
	if average > max_average then
		max_average = average
	endif
endfor

output max_average
```

#### Time Complexity Analysis
To do time complexity analysis lets first decide on **important** operations for us to count. For this problem we can look at how many times we access this array.

We know that the outer loop executes exactly $m$ times, each time it does we know that the inner loop executes exactly $d$ times. As every time the inner loop executes we access the array once that means it will access the array exactly $dm$ times, giving this algorithm a time complexity of $O(dm)$.
### Problem 2
Consider the same problem as above, but instead of finding the maximum average rainfall of each month, we want to calculate the average rainfall of each day over every month.

So in this problem, we want to find the average of the 1st day of each month over all months and output it, the 2nd day of each month over all months and output it, etc.

This is actually very similar to the first problem. In fact we can view it the same except that instead of finding an average for **rows** of a 2D array (each contained array) we are finding an average for **columns** of a 2D array (corresponding elements of each contained array).

The average must be computed and output as part of the outer loop, and, as we are finding the average for the $i$th day of each month, the outer loop must track our day, while the inner loop must track our month.

Since we want to output all averages, we don't need a comparison and can just output the average after it is found.

The full pseudocode is below:
```
for i = 1 to d do
	sum = 0
	for j = 1 to m do
		sum = sum + rainfall[j][i]
	endfor
	
	average = sum/m
	output average
endfor
```

Note that we still index the `rainfall` array using first the month and then the day.

The time complexity for this problem is the same as the first.
## Patten Matching
We have seen how to search for an element of an array in some sorted or unsorted sequence, but what about matching a pattern of elements over some array.

I'm going to actually stop talking about arrays, as this problem works better when we consider **patterns of characters** over some **string**. The algorithm is exactly the same whether we look at patterns of elements or characters, but characters makes it easier to visualise.

Consider the following problem. 

"Given a string of $n$ characters called `text` and a string of $x$ characters $(x\leq n)$ called `pattern`.

Design an algorithm which returns a boolean value indicating if there is a substring of `text` equal to `pattern`."

The obvious solution for this would be to go to each position in the string and then check if the length $x$ substring starting at that position matches our `pattern`. This, while not the best solution, is the algorithm we will be creating today.

So first let's think about the structure of our algorithm. We are going to need 2 loops. The outer loop will move us to every position in the string, and the inner loop will check the next $x$ characters to see if there is a matching substring at this position.

To think about the bounds of our loop, we only need to check the first $n-x+1$ positions as this is the last position that will have enough characters following it for the pattern to exist. 

With all of this we can start to write our pseudocode:
```
found = false
i = 1
while (NOT found) AND i <= n-x+1 do
	j = 0
	while j < x AND text[i + j] == pattern[j + 1] do
		j++
	endwhile
	
	if j == x then
		found = true
	endif
	
	i++
endwhile

output found
```
### Time Complexity Analysis
To determine the time complexity of this algorithm we first need to choose an important operation to count. We can choose checking equality between `text[i + j]` and `pattern[j+1]`.

In the best case scenario the `pattern` we want to find would be right at the start of `text`. For example:
- `text = "ABCDEFG"`
- `pattern = "ABC"`
In this case we would need to check equality exactly $x$ times. And so the best case scenario has a big-O of $O(x)$. We don't usually care about best place big-O notations though.

In the worst case scenario the `pattern` we want to find would be at the end of `text`, or not in `text` at all, and the `text` would force us to check equality $x$ times at each position. For example:
- `text = "AAAAAAAAAAAAAAAAAAAAAAC"`
- `pattern = "AAC`
In this case we would need to check equality exactly $(n-x+1)x = nx - x^2 + x$ times. As we know that $x\leq n$ this means that $x^2\leq nx$, and therefore $nx$ is the greatest term. This means the time complexity of the worst case scenario has a big-O of $O(nx)$.
### Doing Better
The algorithm we have created is called the **"naïve string matching algorithm"**. It is called that because it is the most intuitive one to create, but has fairly poor performance compared to newer algorithms.

Some better options include:
- [Rabin–Karp algorithm](https://en.wikipedia.org/wiki/Rabin%E2%80%93Karp_algorithm) which has a similar worst case time complexity but a far better average time complexity of $O(n)$.
- [Knuth-Morris-Pratt algorithm](https://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm)which has a worst case time complexity of $O(m+n)$, which is far better.
- [Boyer-Moore algorithm](https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_string-search_algorithm) which as a similar worst case time complexity but is specialised for long patterns and large alphabets.