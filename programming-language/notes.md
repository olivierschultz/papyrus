https://danielwestheide.com/books/the-neophytes-guide-to-scala/

# Pattern Matching

Pattern Matching allows you to decompose a given data structure, binding the values it was constructed from to variables.

## Extractors

Constructor creates an object from a given list of parameters.
Extractors extracts the parameters from which an object passed to it was created. 

_note_: case classes automatically have a companion object for them (a singleton object) that contains apply method for creating new instances of the case class but also an unapply method.

## Patterns

Pattern matching are expressions, so their return value is what is returned by the block belonging to the first matched pattern.

You can use pattern matching in the left side of a value definition. A safe and handy way of using patterns in this way is for destructing case classes whose you know at compile time and when working with tuples for readibility.

## Pattern Matching Anonymous Functions

A pattern matching anonymous function is an anonymous function that is defined as a block consisting of a sequence of cases without a match keyword before the block.

## Partial Functions

A partial function is a unary function that is known to be defined for a certain input values and that allows clients to check whether it is defined for a specific input value.

`PartialFunction[-A, +B]` type extends the type `(A) -> B` or `FunctionA[A, B]` . Partial Functions trait provides an `isdefinedAt` method.

_note_: partial functions provide the means to be chained.

Resources:
- https://www.scala-lang.org/old/node/112
- https://danielwestheide.com/blog/the-neophytes-guide-to-scala-part-1-extractors/
- https://danielwestheide.com/blog/the-neophytes-guide-to-scala-part-2-extracting-sequences/
- https://danielwestheide.com/blog/the-neophytes-guide-to-scala-part-3-patterns-everywhere/
- https://danielwestheide.com/blog/the-neophytes-guide-to-scala-part-4-pattern-matching-anonymous-functions/

# Option Type

Option[A] is a container for an optional value of type A. If the value of type A is present, the Option[A] is an instance of Some[A], containing the present value of type A. If the value is absent, the Option[A] is the object None. 


Resources:
- https://danielwestheide.com/blog/the-neophytes-guide-to-scala-part-5-the-option-type/
