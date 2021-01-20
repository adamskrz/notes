# Lecture 5 - Type classes

## Type class constraints

if

```Haskell
(+) :: Int -> Int -> Int
```

then it should not work for doubles - as then it would be `Double -> Double -> Double`. One alternative posibility would be to use polymorphism:

```Haskell
(+) :: a -> a -> a
```

However, then it would break with other data types, e.g. Booleans - how would you evaluate `True + False`?

The solution is to use 'Type class constraints':

```Haskell
(+) :: Num a => a -> a -> a
```

Informally: `(+)` is an operator which:

- takes something of type `a` as argument
- then another thing of type `a` as argument
- returns something of type `a`
- where `a` must be a type that is an *instance* of `Num` (so `(+) :: Num -> Num -> Num` would not work)
  
Each type variable can have many type class constraints!

To summarise: Type class constraints are used to constrain type variables to only types
which support the functions or operators specified by the type class.
`Num` is a type class which represents all types that support arithmetic operators like +, -, *, etc.

## Type Classes

```Haskell
class Num a where
  (+) :: a -> a -> a
  (-) :: a -> a -> a
  abs :: a -> a
  ...
```

A type variable is declared, then the methods that are implemented by the class. Once the methods are declared on the class, they are 'in scope' and can be used elsewhere in the module, even if they are not defined/implemented. For example,

```Haskell
module Foo where

class Num a where
  (+) : a > a > a
  (-) : a > a > a
  abs : a > a

addAndSubtract x y = x + y - 5
```

would compile fine.

## Instance definitions

```Haskell
class OurShow a where
  ourShow :: a -> String

instance OurShow Bool where
  ourShow True  = "True"
  ourShow False = "False"
```

In this case, we have declared the OurShow class for all types, then overloaded the definition specifically for the Bool type.

## Standard library type classes

The standard library includes many type classes, some of the most common are:

- `Num` for numbers (arithmetic operators)
- `Eq` for equality operators (`==`, `/=`)
- `Ord` for inequality operators (`>`, `>=`, `<`, `<=`)
- `Show` for converting things to `String` (`show`)

To find more information about a type class and its definitions, use `:i Class` in the REPL.