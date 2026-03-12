Today we will work through an extended programming example.
## Caesar Cipher
The Caesar Cipher is a way of encoding text by using a numeric **cipher key**. Each letter of the text is rotated around the alphabet by a number of places determined by the **cipher key**.

We say letters are **rotated** since when we get to **z** they wrap back around to **a**.

Today we will build 3 functions:
- `caesar_enc string offset` which will encode strings
- `caesar_dec string offset` which will decode strings
- `caesar_crack string` which will decode strings without knowing the offset

To make these slightly simple, we will only shift **lower case** letters. 
## Encoding and Decoding
### Implementing the Shift
In order to work with characters, we need to use some useful functions from the `Data.Char` package.

The `ord` function takes a character and turns it into an integer and the `chr` function does the opposite.

```
ghci> ord 'c'
99

ghci> chr 97
'a'
```

Using this we can write functions which convert **lower case characters** to numbers between 0 and 25 and back again.

```
char2int c = ord c - ord 'a'

int2char i = chr (i + ord 'a')

ghci> char2int 'c'
2

ghci> int2char 25
'z'
```

Now that we can work with characters, we can write a function that can rotate a character but a given offset.

```
shift c offset = 
	let 
		converted = char2int c 
	in int2char ((converted + offset) `mod` 26) 

ghci> shift 'a' 3 'd'
```

The `mod` function handles the wrapping.

If there are non-letter characters in the string, we want to ignore them. For simplicity we'll also ignore upper case letters.

```
shift c offset = 
	let 
		converted = char2int c #
		is_lower = converted >= 0 && converted < 26 
	in 
		if is_lower 
			then int2char ((converted + offset) `mod` 26) 
			else c 

ghci> shift ' ' 3
' '
```
### Encoding/Decoding a String
To encode a string, we want to apply our `shift` function to every character in the input string which we can do by using recursion.

```
caesar_enc [] _ = [] 
caesar_enc (x:xs) offset = 
	shift x offset : caesar_enc xs offset 

ghci> caesar_enc "hello there" 3 
"khoor wkhuh"
```

To decode we can just reuse our encoding function but provide the negative of the offset:
```
caesar_dec ls offset = caesar_enc ls (-offset)

ghci> caesar_dec "khoor wkhuh" 3 
"hello there"
```
## Cracking the Caesar Cipher
How can we crack some encoded text? We can do this by using **frequency analysis**.

Take the following **cipher text**:
```
"ukq sehh jaran xa wxha pk zaykza pdeo iaoowca"
```

If we look at the letter frequencies of this cipher text and compare them against the English language, we can see how close they are. You can see the comparison below:
![[freq_comparison.png]]
We can see from this comparison that the frequencies are very different, but if we shift the cipher text by 22 then we can see that they are a lot more similar.
![[freq_comparison_shifted.png]]
And if we see the cipher text shifted by 22 we can see
```
ghci> let msg = "ukq sehh jaran xa wxha pk zaykza pdeo iaoowca" 

ghci> caesar_dec msg 22 
"you will never be able to decode this message"
```
which shows us that we correctly decoded the message.

How about if we want to automate this?

We could do this by **measuring** how similar these frequencies are to English for all the different shifts of the cipher text and then return the shift that is the most similar.

We can measure the similarity of the frequencies by using the **chi-squared** score: $$
\sum^z_{i=a}\frac{(freq_i-english_i)^2}{english_i}
$$(You do not need to understand this in detail)
### Counting Frequencies in Strings
We can write a function using recursion which gets the count of a single letter in a string.
```
count _ [] = 0 
count c (x:xs) 
	| c == x    = 1 + rest 
	| otherwise = rest 
	where rest = count c xs
	
ghci> count 'a' "aabaa" 
4
```

We can then get the frequency by dividing the count by the length of the string.
```
freq c list = fromIntegral (count c list) / fromIntegral (length list)

ghci> freq 'a' "aabaa" 
0.8
```
>Note that we want a floating point (decimal) value, and our count and lengths are both integers. So we need to use `fromIntegral` to convert these numbers to floats.

We can then combine these functions to apply them to a full list
```
get_freqs_helper _ 26 = [] 
get_freqs_helper string c = freq (int2char c) string : get_freqs string (c + 1)

get_freqs string = get_freqs_helper string 0

ghci> get_freqs "abc"
[0.33333334,0.33333334,0.33333334,0.0,0.0,...
```
This will always return a list of 26 elements where each element corresponds to exactly 1 letter.
### Finding the Chi-Squared Score
The chi-squared score measures how similar 2 sets of frequencies are.

We can implement the formula for a chi-squared score like so:
```
chi_squared [] [] = 0 
chi_squared (x:xs) (y:ys) = 
	(x - y)**2/y + chi_squared xs ys
	
ghci> chi_squared [0.1, 0.9] [0.8, 0.2] 
3.0624998
```
Note that this assumes both lists of frequencies are the same length, and will crash otherwise.

To get the chi-squared score for a string, we need the letter frequencies of the English language we which we can define as:
```
eng_freqs = [0.0855, 0.0160, 0.0316, 0.0387, 0.1210, 0.0218, 0.0209, 0.0496,
			 0.0733, 0.0022, 0.0081, 0.0421, 0.0253, 0.0717, 0.0747, 0.0207,
			 0.0010, 0.0633, 0.0673, 0.0894, 0.0268, 0.0106, 0.0183, 0.0019,
			 0.0172, 0.0011]
```

Which lets us get the chi-squared score for a single string like so
```
chi_squared_string string = 
	let 
		string_freqs = get_freqs string 0 
	in 
		chi_squared string_freqs eng_freqs 

ghci> chi_squared_string "hello there" 1.5819808
```

We can then use recursion to get the chi-squared score for all possible shifts of a string:
```
chi_squared_list _ 26 = [] 
chi_squared_list string i = 
	let 
		decoded = caesar_dec string i 
		score = chi_squared_string decoded 
	in (score, decoded) : chi_squared_list string (i+1)

ghci> chi_squared_list "ifmmp" 0 
[(9.637143,"ifmmp"),(4.4730797,"hello"),(22.258533,"gdkkn"),(76.40909,"fcjjm"),...
```
### Choosing the Correct Option
Now that we can calculate a list of all the chi-squared scores for the different shifts of a given string, we just need to choose the option with the smallest chi-squared score.

```
get_best [(score, string)] = (score, string) 
get_best ((score, string):xs) = 
	let 
		(tail_score, tail_string) = get_best xs 
	in 
		if score < tail_score 
			then (score, string) 
			else (tail_score, tail_string) 

ghci> get_best (chi_squared_list "ifmmp" 0) 
(4.4730797,"hello")
```

And we can finally tie this all together in one final function
```
caesar_crack string = 
	let 
		scores = chi_squared_list string 0 
		(score, best) = get_best scores 
	in best
	
ghci> caesar_crack "lbh jvyy arire qrpbqr guvf" 
"you will never decode this"
```