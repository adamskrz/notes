# Lecture 9: Higher-order functions

## Associativity of anonymous functions

```Haskell
xor a b = (a || b) && not (a &&b)
```

which is syntactic sugar for:

```Haskell
xor = \a -> (\b -> (a || b) && not (a &&b))
```

- Functions are always nameless and have a single parameter
- Functions are expressions
- When a function is applied to an argument, it reduces to its body
- The body of a function is an expression

```Haskell
xor = \a -> (\b -> (a || b) && not (a &&b))

   (xor True) True
=> (((\a -> (\b -> (a || b) && not (a && b)) True) True
=> ((\b -> (True || b) && not (True && b)) True
=> (True || True) && not (True && True) 
```

Functions types associate to the right

```Haskell
xor :: Bool -> (Bool -> Bool)
xor = \a -> (\b -> (a || b) && not (a &&b))
```

### Summary of associatives

| No explicit parentheses | Explicit parentheses |
| ----------------------- | -------------------- |
| f x y                   | (f x) y              |
| \x > \y > .             | \x > (\y > .)        |
| Int > Int > Int         | Int > (Int > Int)    |

## Functions as arguments

We could have a recursive fucntion to apply to each element in a list:

```Haskell
incByOne :: [Int] -> [Int]
incByOne []     = []
incByOne (x:xs) = x+1 : incByOne xs

evens :: [Int] -> [Bool]
evens []     = []
evens (x:xs) = even x : evens xs
```

However, this is a bit of a waste, as both functions are basically the same, causing code to be rewritten.

if we replace the (+ 1) fcntion with f, and takes this as a paramenter (as such)

```Haskell
incByOne f []     = []
incByOne f (x:xs) = f : incByOne f xs
```

The only difference is `f`. This is known as the map function:

```Haskell
map : (a -> b) -> [a] -> [b]
map f [] = []
map f (x:xs) = f x : map f xs
```

Which we can use to make incByOne and evens as so:

```Haskell
incByOne : [Int] -> [Int]
incByOne = map (+1)

evens : [Int] -> [Bool]
evens = map even
```

Similarly, if we are filtering a list as such:

```Haskell
greaterThan42 :: [Int] -> [Int]
greaterThan42 [] = []
greaterThan42 (x:xs)
    | x > 42    = x : greaterThan42 xs
    | otherwise =     greaterThan42 xs

uppers :: [Char] -> [Char]
uppers [] = []
uppers (x:xs)
    | isUpper x = x : uppers xs
    | otherwise =     uppers xs
```

Then we can rewrite this to make a more general case:

```Haskell
filter :: (a -> Bool) -> [a] -> [a]
filter p [] = []
filter p (x:xs)
    | p x       = x : filter p xs
    | otherwise =     filter p xs
```

and recreate the easirlier functions as:

```Haskell
greaterThan42 :: [Int] -> [Int]
greaterThan42 = filter (> 42)

uppers :: [Char] -> [Char]
uppers = filter isUpper
```

### Haskell Syntax: sections

```Haskell
(+)   :: Num a -> a -> a -> a
(+ 4) :: Num a -> a -> a
(4 +) :: Num a -> a -> a
```

| Expression | Translation     | Type                   |
| ---------- | --------------- | ---------------------- |
| `(+)`      | `(+)`           | `Num a -> a -> a -> a` |
| `(+ 8)`    | `(\x -> x + 8)` | `Num a -> a -> a`      |
| `(4 +)`    | `(\y -> 4 + y)` | `Num a -> a -> a`      |

We can use these to make functions such as (+) neater by using them as such:

```Haskell
(+) 4 8 = 4 + 8
(+ 4) 8 = 8 + 4
(4 +) 8 = 4 + 8
```

## Curried vs un-curried functions

```Haskell
curriedAdd :: Int -> Int -> Int
curriedAdd = \a -> \b -> (a + b)

uncurriedAdd :: (Int, Int) -> Int
uncurriedAdd (x,y) = x + y
```

There are higher order functions(`curry` and `uncurry`) which do this conversion automatically:

```Haskell
curry :: ((a,b) -> c) -> a -> b -> c
curry f x y = f (x,y)

uncurry :: (a -> b -> c) -> (a,b) -> c
uncurry f (x,y) = f x y
```

which are used as

```Haskell
uncurriedAdd :: (Int, Int) -> Int
uncurriedAdd = uncurry (+)

curriedAdd :: Int -> Int -> Int
curriedAdd = curry uncurriedAdd
```

(these functions only work for functions with 2 parameters)

A useful example would be when working with pairs, like:

```Haskell
addPairs :: [Int]
addPairs = map (uncurry (+)) [(1,2), (4,8)]
```

## Folds

