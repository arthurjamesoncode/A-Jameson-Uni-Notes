## Summary
This note is a bit weird compared to the other ones. It's not going to cover any content or explain anything, this is just for me to write down the structure of the exam, as well as what I think I may need to know going in and my strategy for it.

The exam is a 2hr programming exam that will take place on the 20th of May.

It will take place on university computers, and you can use any IDE on these computers. They are guaranteed to have both notepad++ and likely to have vscode. You cannot use any generative AI tools.

You need to bring:
- A pen/pencil to sign/fill in some forms
- Your phone for DUO authentication

In the beginning of the exam you should ensure that `java` and `javac` commands are working, and let an invigilator know if not.
## Structure
The exam is a total of 100 points, 5 of which are for Javadoc comments and following naming conventions. 

>Naming conventions means that all attributes and methods should be in camelCase, while classes should be in TitleCase. 
>
>Typically constant's should be in ALL_CAPS_SNAKE_CASE but I was marked down for that in one of the assignments. Specifically, I was marked down for it not being camelCase. I think they didn't expect people to use constants. You'll have to rely on CodeGrade on the day, but I would assume only camelCase.

The slides say the exam is split into 5 parts, but the practice exam (which is supposedly very similar) is only split into 4 with the following weights:
- Part 1 - Syntax Errors - 20%
- Part 2 - Multiple Simple Classes - 30%
- Part 3 - Single More Involved Class - 35%
- Part 4 - Main Method for Involved Class - 10%
My assumption is that the 5th part is conventions and documentations.

I'm now going to go over what each part is in the practice exam.

The first part is worth 20% and will involve fixing syntax issues for a given class, this honestly just seems super free.

The next part is a few simple classes where we are asked to add some attributes, a constructor and to override the `toString` method. In the practice exam this 3 classes and worth 30% in total, so I would assume that it is 10% per class, and this will be the same in the actual exam.

The third part is one more complicated class which incorporates the other classes. The methods are all pretty simple, it looks like as long as you read the exam carefully you shouldn't lose any marks. It does seem to hold back specific implementation details for example saying "Collection" instead of `ArrayList` but as long as you don't get tripped up by that it's fine.

The last part is confusing. It is labelled "Order Class Main Method" and then is just a snippet of code and an expected output. I'm not entirely sure, but I think they are giving us a specific test case along with code that should produce it as long as our implementations of the methods are correct.

>After going and listening to the recording for week 12, I think I am right. It is just copy and paste code snippet which relies on all the implementations so far written.
## Strategy
To be honest, this exam seems really easy.

25% is just free marks, since the compiler tells you syntax errors and adding Javadoc comments is very easy. Especially if you consider that it is all auto-marked and you don't need human readable Javadoc comments.

Conventions should be followed as we declare each variable/method, and Javadoc comments should be written before each method is implemented. I find that, although Javadoc comments are a waste of time, identifying what needs to be passed in and returned from a method is more useful before you write it than after. 

Plus I don't want to forget one and lose a mark because the conventions and documentation tests took to long to finish near the end of an exam.

The second part seems to be "Can you read and recreate this simple spec?" 3 times. Which is obviously easy. Just be careful to read it carefully to ensure you don't have to waste time changing anything.

The third part seems the hardest but is also pretty simple. My assumption is that the class you write for the third part is some kind of aggregate (collection) class for the other two. 

To be wholly prepared you should probably ensure you are familiar with a least 1 implementation of the `List`, `Set`, and `Map` interfaces, as well as the concept of iterators and how to use them. 

My assumption is that we will be asked to override the `toString` method of this class, and the order in which they will be returned is the order they were added. Since this is the default order for any collection's iterator, using the iterator is an easy way to ensure this.
## Note on CodeGrade
In the COMP105 exam, we were warned that the tests on CodeGrade can run pretty slowly, especially towards the end of the exam where more and more people start to submit. They haven't mentioned that in this module but I'm sure the same applies and John is just nicer for letting us know.

I know for sure I won't feel comfortable unless I keep seeing green on CodeGrade so I am going to:
- Submit after finishing each part
- Leave the tests running in the background
- Check that they are green when submitting the next part
- Repeat
Until the exam is finished.

One of the most important reasons to check is the ensure that conventions and documentations match, since this will be visible and it is easy to mess up by forgetting a line. Unfortunately I won't see green until I've finished coding entirely.

This is somewhat tempting me to write all the Javadoc comments first, but I think it's probably better to try and go in order so I can just forget about what I have written once it is complete.