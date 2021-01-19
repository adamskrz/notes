# Lecture 3

## Types

Haskell can infer all types
But definitionas can still be added

```Haskell
daysPerWeek :: Int
daysPerWeek = 7
```

like TypeScript - good for documentation and problem solving. This can alse be useful where Haskell is unable to infer the type correctly.

## Compiling

1. Parsing - Source code is truned into data in memory
2. Type checking - types are tested and inferred, any issues flag up a type error
3. Once type checking is passed, the types are all removed for runtime
4. Code generation - converted to binary file

## Function Types

### not Funciton

```Haskell
not :: Bool -> Bool

not b = case of 
   True -> True
  False -> True
```

If provided with Boolean value, Boolean is returned

### xor Function

`xor` is a function which takes a Bool, then another Bool, then outputs a Bool

```Haskell
xor :: Bool -> Bool -> Bool
```

### GHCI inferred types

use `:it xor` to get type from `xor` in GHCI

## Polymorphism

Some functions have many possible types:

```Haskell
\x -> x
f :: Int -> Int
f :: Bool -> Bool
f :: Char -> Char
...
```

These are all permissible, but it would be tedious to write out every possible option.

### Type Variables

```Haskell
f \x -> x :: a -> a
```

A function that takes something of type `a` as the argument and will return something also of type `a`.

F does not care about the argument types, and will evaluate with any.

## Tuples

Tuples can have as many components as you like, they contain any valid expression. Usually referred to number of components, e.g. 2-tuple, 3-tuple.

```Haskell
(4, 7) :: (Int, Int)
(4, 7.0) :: (Int, Double)
('a', 9, "Hello") :: (Char, Int, String)
(True, 4, 'c', 1) :: (Bool, Int, Char, Int)
((4, 'g'), False) :: ((Int, Char), Bool)
(\x > x, 8.15) :: (a > a, Double)
```

These can easily be used within functions

## Functions with pairs

```Haskell
fst :: (a,b) -> a
fst (x,y) = x

snd :: (a,b) -> b
snd (x,y) = y

swap :: (a, b) -> (b, a)
swap (x,y) = (y,x)
```

Having types means that in many cases there is no need to check the actual function definition to know what it does - the type makes it self explanatory. These functions are in the standard library, as working with pairs is very common.
