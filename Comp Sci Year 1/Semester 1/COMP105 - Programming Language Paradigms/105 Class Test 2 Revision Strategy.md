I think I can get away with very little/no revision for this test but just in case I will go over the relevant lectures and make notes.

- Higher Order Functions/Functional Programming Idioms
- Types
- Custom Types
- IO and Models of Evaluation

This is the content from Lecture 11 onwards so I will be making those relevant notes in the lecture notes folder.

Make a spreadsheet and ensure you can get all of this.
## Retaking Practice Test
I have taken this once before but I am going to retake it now before he goes over this in tomorrow's lecture.
### Higher Order Functions
- 1 - C c
- 2 - A c
- 3 - A c
- 4 - B c
- 5 - C c
### Types
- 6 - D c
- 7 - D c
- 8 - A c
- 9 - B c
- 10 - C c
### Custom Types
- 11 - B c
- 12 - D x E 
- 13 - A c
- 14 - B c
- 15 - E c
### IO and Models of Evaluation
- 16 - B x D I was actually right the first time but when I checked with GHCI convinced myself I was wrong
- 17 - E c
- 18 - B c
- 19 - C c
- 20 - C c
## Remember for Test
Based on the things that tripped you up on this practice test, you need to remember the following things.

- Make sure to double check `deriving` when dealing with custom types. Make sure to do this for all questions that call back to custom types as well.
- Be careful not to constrain to `Eq` or `Ord` when the thing compared is `show x` as string is in the `Eq` and `Ord` type classes anyway.
- If a type derives `Ord` the earlier constructors are smaller.
- When asked what is returned by a query, it is asking for the exact value not the output to the GHCI console. Important for results of type `IO a`.
- Always prefer `foldr` over `foldl`. Even if there is some obscure use case for `foldl`, John will not show it since `foldl` both destroys laziness and does not have strict evaluation. 
- Prefer `foldl'` over `foldr` in situations where you will need to process the whole list and do not need to preserve laziness. Strict evaluation does not build up a call stack and therefore tends to be more efficient (except in the case of tail recursion, which also doesn't build a call stack).
- Tree functions can be checked by going up from the leaves and writing the value at each step.
- Go through quickly at first and then write out things slowly on a second pass over the test, or if you are at all unsure of a question.