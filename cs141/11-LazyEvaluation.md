# Lecture 11: Lazy Evaulation

A fully reduced expression is called the *normal* form. An expression that can be reduced (such as `(4 + 8)`) is called a *redex*.

## Evaluation Methods

### Call by value

- reduce function arguments to normal forms before calling the function
- We may evaluate arguments even if they are never needed
  
### Call by name

- Only reduce expressions when their value is needed
- We may end up reducing the same expression over and over

### Sharing

The compiler tries to avoid duplicate evaluation, by replacing expressions with local variables/definitions
