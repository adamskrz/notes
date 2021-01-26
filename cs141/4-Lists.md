# Lecture 4

## Lists

Use ```:``` cons operator for lists

```Haskell
# Empty list:
8 : []
# List with more elements
4 : (8 : (15 : []))
```

Indexing is linear in list, unlike arrays

## Types

```Haskell
[] :: [a]
```

All elements are same type
for example:

```Haskell
[1,2,3] :: [Int]
[True,False,True] :: [Bool]
etc
```

These are used as such:

```Haskell
[] :: [a]
(:) :: a -> [a] -> a

# or with syntactic sugar
[1] 
= 1 : []

[True, False]
= True : (False : [])
```

When used in a pattern not expression, cons is used to get items from a list:

```Haskell
head (x:xs) = x
tail (x:xs) = xs
x :: a
xs :: [a]
```

Examples of functions on lists:

```Haskell
head      :: [a] -> a
tail      :: [a] -> [a]
null      :: [a] -> Bool
take      :: Int -> [a] -> [a]
length    :: [a] -> Int
(++)      :: [a] -> [a] -> [a]
reverse   :: [a] -> [a]
concat    :: [[a]] -> [a]
and       :: [Bool] -> Bool
product   :: [Int] -> Int
replicate :: [Int] -> a -> [a]
```

## Split function

```Haskell
splitAt 2 [1,2,3,4,5]
splitAt :: Int -> [a] -> ([a],[a])
=> ([1,2],[3,4,5])
```

this can easity be defined using the take and drop functions from earlier!

```Haskell
splitAt :: Int -> [a] -> ([a],[a])
splitAt n xs = (take n xs, drop n xs)
```

## More types of lists

Lists can contain expressions eg:

```Haskell
    [1+2,3*4,6-5]
=>  [3,12,1]

    [even 5, odd 3, True, not True]
=>  [False,True,True,False]
```

## Ranges

These are very cool, works almost like Excel

```Haskell
[7..10]     => [7,8,9,10]
['A'..'D']  => ['A','B','C','D']
[1,3..9]    => [1,3,5,7,9]
```

You can also have infinte ranges:

```Haskell
[0..]     => [0,1,2,3,4,5,6,7....
[0,2..]   => [0,2,4,6,8,10....
```

These are useful as they will only be evaluated where used eg:

```Haskell
take 4 [0..] => [0,1,2,3]
```

I guess that's like Python ranges.

## List comprehensions

Apparently everyone loves these from Python

```Haskell
[n | n <- [0..5]]
=> [0,1,2,3,4,5]
```

This literally generates each number in the list on right, then adds it to list n. Not very useful, but can be extended e.g.

```Haskell
   [even n | n <- [0..5]]
=> [True,False,True,False,True,False]

   [n*m | n <- [0..2], m <- [0..2]]
=> [0*0,0*1,0*2,1*0,1*1,1*2,2*0,2*1,2*2]
=> [0,0,0,0,1,2,0,2,4]

   [n*m | n <- [0..2], m <- [0..n]]
=> [0*0,1*0,1*1,2*0,2*1,2*2]
```

can also have predicates in list comprehensions

```Haskell
   [n | n <- [0..4], mod n 2 = 0]
=> [0,2,4]
```

This is like having a for loop but all in a list expression
```[expression | generatorsAndPredicates]```.
A generator is any expression that outputs a list, a predicate is any expression that outputs boolean.

## Summary

- Lists are constructed by "cons"ing elements to the empty list
- We can pattern-match them in many ways
- There are loads of built-in functions
- Range syntax can be used to make lists with elemnts in a range
- Comprehensions can make lists with other lists and conditions
