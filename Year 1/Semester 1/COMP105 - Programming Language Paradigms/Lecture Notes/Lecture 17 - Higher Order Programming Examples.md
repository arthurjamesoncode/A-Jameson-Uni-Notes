## Examples

- Mark Averages
- Voting System

## Mark Averages
Say we have a file of student marks for assignment 1, 2, 3, and the class test 

**For Example:**
```
aaaa 70 65 67 60  
bbbb 55 60 55 65  
cccc 40 40 40 40  
dddd 80 60 75 60  
cccc 0 0 0 100
```

> Each line is in the format `name assingment1 assingment2 assingment3 class test`.
> Where each line is the students name followed by their marks all separated by a space.

We want to produce a file of mark averages.

**For Example:**
```
aaaa 65.5  
bbbb 58.75  
cccc 40.0  
dddd 68.75  
cccc 25.0
```

>To do this we need to read txt from a file and then output to a file. This is an IO action which will be covered later so I won't go into it. 
>
>For the rest of this example I will assume that I have the input file in the form of a string with lines separated by newline characters (`'\n'`). Assume this is what I am referencing whenever you see `file`.

The function `lines` gives a list of lines.

**For Example:**
```
ghci> lines "line 1\nline 2\nline 3\n"  
["line 1","line 2","line 3"]  
  
ghci> lines file  
["aaaa 70 65 67 60",  
"bbbb 55 60 55 65", ...
```

The `unlines` function does the opposites.

**For Example:**
```  
ghci> unlines ["line 1", "line 2", "line 3"]  
"line 1\nline 2\nline 3\n"
  
ghci> unlines . lines $ file  
"aaaa 70 65 67 60\nbbbb 55 60 55 65 ...
```

Using `words` and `lines` we can parse the file:
```
ghci> let parsed = map words . lines $ file  
ghci> parsed  
[["aaaa","70","65","67","60"],  
["bbbb","55","60","55","65"],  
["cccc","40","40","40","40"],  
["dddd","80","60","75","60"],  
["cccc","0","0","0","100"]]
```

We can then get the averages like so:
```
average :: [String] -> Float  
average [student, a1, a2, a3, ct] = (read a1 + read a2 + read a3 + read ct) / 4
  
ghci> let averages = map average parsed  
ghci> averages  
[65.5,58.75,40.0,68.75,25.0]
```

>The average function uses a pattern match to extract the data from a single line of the file. This is obviously partial but this isn't something that is avoidable when it comes to parsing user input.

We can get the students names like so:
```
name :: [String] -> String  
name (student:_) = student
  
ghci> let names = map name parsed  
ghci> names  
["aaaa","bbbb","cccc","dddd","cccc"]
```

And generate the report like this:
```
report_line :: String -> Float -> String  
report_line student average = student ++ " " ++ show average

ghci> let zipped = zipWith report_line names averages  
ghci> unlines zipped  
"aaaa 65.5\nbbbb 58.75\ncccc 40.0\ndddd 68.75\ncccc 25.0"
```

You can put it this all into one function like so:
```
report file =  
	let  
		parsed = map words . lines $ file  
		students = map name parsed  
		averages = map average parsed  
		zipped = zipWith report_line students averages  
	in  
		unlines zipped
```

## Voting

### First Past the Post
In a first past the post election, whoever gets the most votes wins.

A function to determine the winner of an election in a first past the post system could look like:
```
ghci> winner ["red", "blue", "red", "red", "green"]  
"red"
```

To implement this first we need to get all the unique candidates
```
uniq [] = []  
uniq (x:xs) = x : uniq (filter (/=x) xs)
 
ghci> uniq ["red", "red", "blue", "green", "red", "blue"]  
["red","blue","green"]
```

And then we need to count the votes for each candidate
```
count list x = length (filter (==x) list)

ghci> count ["red", "blue", "red", "red", "blue"] "red"
3
```

We can map this `count` function  to get the vote totals and then zip these totals with the names of the candidates to get a list of tuples containing each candidate and the vote count.

```
totals votes =  
	let  
		candidates = uniq votes  
		vote_counts = map (count votes) candidates  
	in  
		zip vote_counts candidates
```

Because tuples are ordered lexicographically, we can use maximum to find the candidate with the most votes.
```
ghci> maximum [(3, "red"), (2, "blue"), (4, "green")]  
(4,"green")
```

And so we can get the winner like this:
```
winner votes = (snd . maximum . totals) votes
 
ghci> winner ["red", "blue", "red", "red", "green"]  
"red"
```

>It's worth noting that this program doesn't handle tie breaks well at all. It just takes the first person in the list who tied.
>
>To get around this you could find the highest vote count and filter out anyone with less votes so that you were left with the tied winners, but you would then need some other tie break algorithm in place.

### Alternative Vote
In the alternative vote system, voters rank the candidates  
- In each round, the candidate with the least number of first preference votes is eliminated  
- The winner is the last candidate left once all others have been eliminated 

**For Example:**
```
ghci> let votes = [["red", "blue", "green"],  
				   ["blue", "green"],  
				   ["green", "red"],  
				   ["blue", "red"],  
				   ["red"]]

ghci> av_winner votes  
"red"
```

To get the first choice votes we can map `head` over the list of votes.
```
first_choice votes = map head votes
  
ghci> let votes = [["red", "blue", "green"],  
				   ["blue", "green"],  
				   ["green", "red"],  
				   ["blue", "red"],  
				   ["red"]]

ghci> first_choice votes  
["red","blue","green","blue","red"]
```

We can then use our previous `totals` function and a `sort` to rank the candidates.
```
import Data.List (sort)
rank votes = sort . totals . first_choice $ votes
 
ghci> let votes = [["red", "blue", "green"],  
				   ["blue", "green"],  
				   ["green", "red"],  
				   ["blue", "red"],  
				   ["red"]]

ghci> rank votes  
[(1,"green"),(2,"blue"),(2,"red")]
```

>Note that the `sort` function comes from the `Data.List` package.

We can then `map` a `filter` over our list of votes to remove the candidates with the least amount of votes.

```
remove_cand c votes = 
	rm_empty
	where
		rm_votes = map (filter (/=c)) votes  
		rm_empty = filter (/=[]) rm_votes

ghci> remove_cand "green" votes  
[["red","blue"],["blue"],["red"],["blue","red"],["red"]]

ghci> remove_cand "red" votes  
[["blue","green"],["blue","green"],["green"],["blue"]]
```

>Note that since our `first_choice` function uses head it is partial and won't work on any empty lists. This is why we must filter out the empty votes from the list of votes.

Finally, can then combine everything all into one function:
```
av_winner votes = 
	if length ranked == 1  
		then first  
		else av_winner (remove_cand first votes)
	where
		ranked = rank_candidates votes  
		first = head ranked 
 
ghci> av_winner votes  
"red"
```

>Note that we use recursion here to run the same function again if we are left with more than 1 valid candidate.