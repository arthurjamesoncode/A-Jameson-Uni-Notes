## Topics:

- Recursive Custom Types
- Custom Lists
- Trees

## Recursive Custom Types
In a recursive custom type, some constructors contain the type itself.

**For Example:**
```
data IntList = Empty | Cons Int IntList  
	deriving(Show)  
```

The above is an (uglier) implementation of `[Int]`.
```
Empty -- []  
Cons 1 (Empty) -- [1]  
Cons 1 (Cons 2 Empty) -- [1,2]
```

>Recall how `[1,2]` can be represented as `(1:2:[])`.

A more general list data structure could be defined using a type variable like so:
```
data List a = Empty | Cons a (List a)  
	deriving(Show)
	
ghci> :t Cons 'a' (Cons 'b' Empty) -- ['a', 'b']  
List Char

ghci> :t Empty -- []  
List a
```

If you make the constructors infix using backticks you can see more clearly how this mimics the normal cons syntax. ``1 `Cons` (2 `Cons` Empty)`` is the same as `1:2:[]` which is the same as `[1,2]`.

>Any 2 argument function can be made infix with backticks. Since constructors are just functions this is also the case for them.

We can write functions using this custom list type.

**For Example:**
```
our_head :: List a -> a  
our_head Empty = error "Empty list"
our_head (Cons x _) = x
 
ghci> our_head (1 `Cons` (2 `Cons` Empty))  
1

our_tail :: List a -> List a  
our_tail Empty = error "Empty list"  
our_tail (Cons _ x) = x 
 
ghci> our_tail (1 `Cons` (2 `Cons` Empty))  
Cons 2 Empty

our_sum :: List Int -> Int  
our_sum Empty = 0  
our_sum (Cons x xs) = x + our_sum xs
 
ghci> our_sum (1 `Cons` (2 `Cons` Empty))  
3
```

>Notice how `our_sum` is a recursive function as uses pattern matching with `Empty` and `Cons x xs` in the same way that we would pattern match with `[]` and `(x:xs)` when writing recursive functions on lists.

## Custom Lists
The above just reimplements list but we can create types with more functionality than that.

**For Example:**
```
data TwoList a b = TwoEmpty | ACons a (TwoList a b) | BCons b (TwoList a b)  
	deriving (Show)
	  
gchi> :t 'a' `ACons` (False `BCons` TwoEmpty)  
TwoList Char Bool
```

This is a list that can store two different types `a` and `b`. In the given example it is storing `Char`s and `Bool`s.

>You may notice that `TwoList` is essentially an implementation of `[Either a b]` but it still a good example of how you can write recursive types.

## Trees
A tree is a a graph with no cycles. It essentially consists of a leaf nodes, which have no children, and branch nodes which can have many children.

A binary tree is a tree in which branch nodes contain at most 2 children.

**For Example:**
![[binary_tree_example.png.png]]

In Haskell we can implement a Binary Tree like so:
```
data Tree = Leaf | Branch Tree Tree deriving (Show)
```

>Notice how each node of a tree is either a `Leaf` and has no children or its a `Branch` and has 2 nodes as children. Since these nodes can either be Leaves or Branches we can use the type `Tree` to show this.
>
>This implementation only allows for 0 or 2 children, not 1 child. There is a way to allow this, which will be shown later.

We can write recursive functions that process trees.

**For Example:**
```
size :: Tree -> Int  
size (Leaf) = 1  
size (Branch x y) = 1 + size x + size y
  
ghci> size (Branch Leaf (Branch Leaf Leaf))  
5
```

The data type we've created so far cannot hold any data. In order for it to hold data, like the example image, we would need to define it as so:
```
data DTree a = DLeaf a | DBranch a (DTree a) (DTree a)  
	deriving (Show)
	
DBranch 1 (DBranch 2 (DLeaf 4) (DLeaf 5)) (DBranch 3 (DLeaf 6) (DLeaf 7))
--The above example corressponds to the example image from earlier.
```

Recursion on trees with data is very much the same. We can use pattern matching to pull out the relevant data for us.

**For Example:**
```
tree_sum :: Num a => DTree a -> a  
tree_sum (DLeaf x) = x  
tree_sum (DBranch x l r) = x + tree_sum l + tree_sum r

ghci> tree_sum (DBranch 11 (DLeaf 2) (DLeaf 9))  
22
```

Suppose we have a directory structure. We can formulate the files and folders as nodes in a tree, with files being `Leaf "file.txt"` and folders being `Branch "folder/"`.

**For Example:**
```
let fs = DBranch "home/" 
		 (DBranch "docs/" (DLeaf "a.txt") (DLeaf "b.txt")) 
		 (DLeaf "c.txt")
```

When searching for a file, it may not exist so we should use the Maybe type.

```
find_file file (DLeaf x)  
	| x == file = Just file  
	| otherwise = Nothing
  
find_file file (DBranch x l r) =  
	let  
		left = find_file file l  
		right = find_file file r  
	in  
		case (left, right) of  
			(Just y, _) -> Just (x ++ y)  
			(_, Just y) -> Just (x ++ y)  
			(_, _) -> Nothing

ghci> find_file "a.txt" fs  
Just "home/docs/a.txt"
 
ghci> find_file "d.txt" fs  
Nothing
```

### More Complex Trees
The following is outside the scope of 105 as we only need the definition of `Tree` and `DTree` given here, but as these definitions are quite limiting I wanted to include some more complicated ones.

The definition of `Tree` and `DTree` given are both implementations of Binary trees, and in both of them nodes either had 0 children (`Leaf`) or 2 children (`Branch`) . In reality nodes in a binary tree could also have 1 child.

To implement this you could use the following definition.

**Definition and Examples:**
```
data BTree a = BTreeEmpty | BTreeBranch a (BTree a) (BTree a)
	deriving (Show)

btree_size :: BTree a -> Int
btree_size BTreeEmpty = 0
btree_size (BTreeBranch _ l r) = 1 + btree_size l + btree_size r

btree_sum :: Num a => BTree a -> a
btree_sum BTreeEmpty = 0
btree_sum (BTreeBranch x l r) = x + btree_sum l + btree_sum r
```

In the above definition we add the `BTreeEmpty` constructor and remove the `Leaf` constructor. Leaves still exist in our tree but now would be defined as `BTreeBranch x BTreeEmpty BTreeEmpty`. 

>Since a branch can have `BTreeEmpty` as zero, one, or both of it's children, this data structure is not constrained to having just zero or two children per node.

You may also be wondering about how to implement a tree with no max number of children per node.

If you wanted to do this you could use the following definition.

**Definition and Examples:**
```
data Tree a = TreeEmpty | Branch a [Tree a]
	deriving (Show)
	
tree_size :: Tree a -> Int
tree_size TreeEmpty = 0
tree_size (Branch _ []) = 1
tree_size (Branch _ subtrees) = 1 + (sum . map tree_size $ subtrees)

tree_sum :: Num a => Tree a -> a
tree_sum TreeEmpty = 0
tree_sum (Branch x []) = x
tree_sum (Branch x subtrees) = x + (sum . map tree_sum $ subtrees)
```

In the above definition instead of giving two tree parameters to each branch we give `[Tree]`. This means that each branch can have an arbitrary number of subtrees instead of just 2.

>Notice how when we recursively traverse the tree we have to use `map` to apply our function to all trees in the subtree.
>
>`data Tree a = Branch a [Tree a]` is also a fine definition for this tree, as a branch with no children can be shown as `Branch x []`. The inclusion of `TreeEmpty` allows for the existence of a tree with no nodes, which depending on your use case, may be pointless.