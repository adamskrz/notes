# Lecture 16 - Folds and Functors

## Functors


```Haskell
class Functor f
    where fmap :: (a -> b) -> f a -> f b

instance Functor [] where
    fmap = map

instance Functor Maybe where
```

