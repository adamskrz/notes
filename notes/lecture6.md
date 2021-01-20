# Recursive functions

## Examples

### Factorial function

We start off by specifying the types for documentation purposes

```Haskell
factorial :: Int -> Int
```

There is a trick we could use in Haskell:

```Haskell
factorial n = product [1..n]
```

however, we want to do this with a recursive function:

```Haskell
# base case with pattern matching
factorial 0 = 1   
# definiton of factorial
factorial n = n * factorial (n-1)
```

this runs like so:

```Haskell
   factorial 2
=> 2 * factorial (2-1)
=> 2 * factorial 1
=> 2 * 1 * factorial (1-1)
=> 2 * 1 * factorial 0
=> 2 * 1 * 1
```

### Fibonacci function

As before, we specify the definition, by writing base cases then the general case.

```Haskell
fib :: Int -> Int
fib 0 = 1
fib 1 = 1
fib n = fib (n-1) + fib (n-2)
```

which is run like so:

```Haskell
   fib 3
=> fib (3-1) + fib (3-2)
=> fib 2 + fib 1
=> fib (2-1) + fib (2-2) + fib 1
=> fib 1 + fib 0 + fib 1
=> 1 + 1 + 1
=> 3
```

## Performance

the issue with basic recursive functions is the large amount of memeory used in stack
[insert pic]

Fortunately, the Haskell compiler is smart, and optimises recursive functions to not be as inefficient.

```Haskell
# Original Function
fac :: Int -> Int
fac 0 = 1   
fac n = n * fac (n-1)

# Optimised with accumulating factor
fac' :: Int -> Int -> Int
fac' 0 m = m
fac' n m = fac' (n-1) (n*m)

# Rewritten fac
fac :: Int -> int
fac n = fac' n 1
```

## Recursion on lists

### Product function

```Haskell
product :: [Int] -> Int
product []     = 1
product (n:ns) = n * product ns
```

runs as expected:

```Haskell
   product [1,2,3,4]
=> 1 * product [2,3,4]
=> 1 * 2 * product [3,4]
=> 1 * 2 * 3 * product [4]
=> 1 * 2 * 3 * 4 * product []
=> 1 * 2 * 3 * 4 * 1
=> 24
```

### `let` and `where`

```Haskell
splitAt :: Int -> [a] -> ([a], [a])
splitAt 0 xs     = ([], xs)
splitAt n []     = ([], [])
splitAt n (x:xs) = (x:ys, zs)
  where (ys, zs) = splitAt (n-1) xs

splitAt n xs = (ys, zs)
  where ys = take n xs
        zs = drop n xs
```

what this does is 

```Haskell
splitAt 2 [1,2,3]
=> (1:ys, zs)
   where (ys, zs) = splitAt 1 [2,3]
=> (1:ys, zs)
   where (ys, zs)  = (2:ys',zs')
         (ys',zs') = splitAt 0 [3]
=> (1:ys, zs)
   where (ys, zs)  = (2:ys',zs')
         (ys',zs') = ([],[3])
=> (1:ys, zs)
   where (ys, zs) = (2:[],[3])
=> (1:2:[], [3])
== ([1,2], [3])
```

### Testing data

```Haskell
and :: [Bool] -> Bool
and [] = True
and (x:xs) = x && and xs
```

This goes through the whole list, checking each is true

We can do a similar thing to check the length of a list:

```Haskell
length :: [a] -> Int
length [] = 0
length (_:xs) = 1 + length xs
```
