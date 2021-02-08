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

# Scala

Scala combines OOP and FP.

Features:
- static types system
- JVM and JS runtimes
- Seamless JAVA interop (scala classes are JVM classes)
- Type inference
- Asynchronicity (with futures), Concurrency and distribution (with Actors)
- Traits, multiple traits can be mixed into a class to combine their interface and behavior
- Pattern Matching
- High-order functions, functions are first-class objects (or first-class citizen), they are values

Great for:
- Safe and high performant concurrent programming
- Actor systems on the JVM
- in-language custom DSLs

Resources:
- https://www.scala-lang.org/

# Style Guide

## Indentation

- 2 spaces
- 80 characters 
- methods with numerous arguments on a line by itself if more than 4

## Naming Conventions

- camel case (lowerCamelCase)
- name `_` is discouraged
- Classes and Traits are in upper camel case
- Objects are in upper camel case except when mimicking a package or function
- packages follow the Java package naming convention
- Methods
  - Textual (alphabetic) names for methods are in lower camel case
  - the name of the method should be the name of the property for accessors or properties
  - It is acceptable to preprend is on a boolean accessor (isEmpty), only if no corresponding mutator is provided
  - the name if the method should be the name of the property with _= appended for mutator, this convention will enable a call-site mutation syntax which mirrors assignment if a corresponding accessor is provided.
  - foo1() and foo2 are different method at compile-time (only applicable to methods of arity-0). So methods which act as accessors of any sort should be declared without parentheses except if they have side effects. The callsite should follow the declaration.
  - Symbolic Method Names have two valid use-cases: DSL (actor ! Msg) and logically mathematic operations (a + b). However, in the course of standard API design, symbolic method names should be strictly reserved for purely-functional operations.
- Constant names should be in upper camel case
- Methods, value and variable should be in lower camel case
- Type parameters 
  - should have first upper case letter (starting from A)
  - HKT and parameterized type are also in first upper case letter
- annotations should be in lower camel case

note: arity is the number of arguments or operands by a function or operation.

## Types

- Favoir explicitness in public APIs
- No need to annotate the type of a private field or local variable
- All public methods should have explicit type annotations because a change to te internals of a method or val could alter the public API of the class without warning, potentially breaking client code. They can also help to improve compile times.
- Annotation : value: Type
- Function types def foo(f: Int => String).
- Parenthese should be ommited for methods of arity-1
- Structural types should be declared on a single line if they are less than 50 characters in length def foo(a: { val bar: String })

## Nested blocks

- Opening curly braces must be on the same line as the declaration they represent

## Declarations

- Class, object, trait constructors should be declared all on one line unless the lines is 100+ characters long. In that case, each constructor argument on its own line
- If a class, object or trait extends anything, the same general rule applies
- All class, object and trait members should be declared interleaved with newlines except for var and val (only if they have a scaladoc).
- Fields should precede methods in a scope
- Methods with default parameter def foo(x: Int = 6, y: Int = 7): Int = x + y
- Specify a return type for all public members, consider it documentation checked by the compiler, it also helps in preserving binary compatibility. except for local methods or private methods
- modifiers order: annotation -> override -> access -> implicit -> final -> def
- you should use multiple parameter lists for :
  - fluent API
  - implicit parameters
  - type inference
		  def foldLeft[B](z: B)(op: (B, A) => B): B
		List("").foldLeft(0)(_ + _.length)

		// If, instead:
		def foldLeft[B](z: B, op: (B, A) => B): B
		// above won't work, you must specify types
		List("").foldLeft(0, (b: Int, a: String) => b + a.length)
		List("").foldLeft[Int](0, _ + _.length)

- in high-order functions, prefer placing the function parameter last, it enables invocation syntax like foldLeft(List(1, 2, 3, 4))(0)(_ + _)
- function values prefered syntax val f1 = ((a: Int, b: Int) => a + b) unless it has only two arguments val f4: (Int, Int) => Int = (_ + _)

## Control struture

- all control structures should be written with a space following the defining keyword
- curly-braces should be omitted in cases where the control structure represent a pure-functional operation and all branches of the control structure are single-line expressions
- for-comprehensions with multiple generators (<-) should be one generator on each line except if there is only one generator.
- Prefer for-comprehensions over chained map, flatMap, filter

## Method invocation

- Method invocation follows java conventions target.foo(42, bar)
- Named parameters foo(x = 6, y = 7)
- no need for parentheses on methods of arity-0 only if it has no side-effects (purely-functional).
- methods which take functions as parameters should be invoked using infix notation

## Files

- files should contain a single logical compilation unit (class, trait, object) and their companion objects. except for sealed trait for emulating ADTs
- multi-unit files should be given camel case names with a lower case first letter

## Scaladoc

- The first sentence should be a summary of what the method does. Subsequent sentences explain in further detail.
- get to the point quickly and document what the method does, not what the method should do.
- Java style
/**
 * Provides a service as described.
 *
 * This is further documentation of what we're documenting.
 * Here are more details about how it works and what it does.
 */
def member: Unit = ()
- A package's documentation should first document what sorts of classes are part of the package, then document the general sorts of things the package object itself provides with some basic examples.
- Provide a summary of what the class, trait or object does using @tparam, @param or @constructor.

Resources:
- https://docs.scala-lang.org/style/

