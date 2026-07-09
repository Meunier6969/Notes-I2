# Functional Programing
**Teacher** : MAZELIER Gaylord
**Moodle Link** : https://moodle.myefrei.fr/course/view.php?id=20410

# Lambda Calculus
| What        | How                       | Example |
|-------------|---------------------------|---------|
| Variable    | \<name\>                  | a       |  
| Function    | λ\<params\>.\<body\>      | λa.a    |
| Application | (\<func\>)\<var of func\> | (λx.x)a |

## Church numerals
- ZERO (0) = λf.λx.x
- SUCC  = λn.λf.λx.(f((nf)x))  
- ONE   = SUCC(0) = λf.λx.(fx)
- TWO   = SUCC(1) = λf.λx.(f(fx))
- THREE = SUCC(2) = λf.λx.(f(f(fx)))

# Programming Concepts
- **Record** : Structured, immutable data that groups related values.
- **Closure** : A function bundled with the environemment (values) it captures from it's scope.
- **Concurrency** : Running multiple computation at the same time.
- **State** : Named, changing data over time, stored in memory.

# FP Concepts/Principles
**Pure function** : Function that depends only on it's inputs, without any side-effects. This means it's always predicatble, deterministic
**Immutability** : Data doesn't change after being created
**Higher-order function** : Function that take and/or return another function
**Currying** : Function that take multiple arguments, turned into a series of functions each taking one argument
**Recursion** : Function calling itself

# Scala
## Functions and primitives
```scala
// Primitive expressions: represent the simplest elements (and everything is an expression)
1
"hello"
true

// Expressions: more complex expressions can be created by combination using operators
// In Scala, almost everything is an expression returning a value
1 + 2
"Hello, " ++ "World"

// Evaluation: Scala evaluates expressions by reducing them to values
(1 + 2) * 3
3 * 3
9

// Method calls
// Another way to produce complex expressions, is to call methods on expression using the dot notation
"Hello, world".length
1.to(10)
1.toString

// Operators are methods, usually using symbols
42.+(1)
42.+(1) == 42 + 1
assert(42.+(1) == 42 + 1) // Assertions are lightweight executable "documentation"

// The compiler statically checks that you don’t combine incompatible expressions (types)
// This is called static typing
// In practice: be explicit on types
val x: Int = 42
x
// val badType: Int = "hello" // does not work

// Naming things, using meaningful names
val base: Int = 4
val height: Int = 6
val area = base * height / 2
s"area of triangle is equal to $area"

// Immutable
val z = 41
// z = 42 // does not work, cannot reassign a value to a `val`

// Mutable (reminder: we will prefer immutable values during the course)
var z2 = 41
z2 = 42

// Immutable collections
val xs = List(1, 2, 3)

// The list `ys` is mutable even if bound to a `val`
import scala.collection.mutable.ListBuffer
val ys = ListBuffer(1, 2)
ys.length
ys.append(3)
ys.length

// Functions: parameters are listed with their types
// In practice: be explicit on returned type
def identity(x: Int): Int = x
assert(identity(x) == x)

// Sum of two integers
def sum(x: Int, y: Int): Int = x + y
assert(sum(1, 2) == 3)

// Possible to give a default value to a parameter
// In practice: use this carefully, avoid too many default parameters
def sumWithDefault(x:Int, y: Int = 0): Int = sum(x, y)
sumWithDefault(1, 1)
sumWithDefault(1)
// Can also be useful to explicitly name parameters
// For functions with a lot of parameters, default values and/or more readability
sumWithDefault(x=1, y=1)

// Sum of two integers, renamed
def sumOfInts(x: Int, y: Int): Int = x + y
sumOfInts(2, 3)

// Sum of the square of each parameter
def sumOfSquares(x: Int, y: Int): Int = x * x + y * y
sumOfSquares(2, 3)

// Sum of the predecessor of each parameter
def sumOfPredecessors(x: Int, y: Int): Int = x - 1 + y - 1
sumOfPredecessors(2, 3)

// High-order function: a function that takes another function as a parameter
// Functions are values...
def sumOf(x: Int, y: Int, f: Int => Int): Int =  f(x) + f(y)
sumOf(1, 2, identity)

// Functions: expression evaluation is called the substitution model
// This model can be applied to all expressions, as long as they have no side effects
// The λ-calculus is a foundation for functional programming and formalises this model
// Reminder: x => x ↔ λx.x
sumOf(1, 1 + 1, identity)
sumOf(1, 2, identity)
identity(1) + identity(2)
1 + identity(2)
1 + 2
3

def square(a: Int): Int = a * a

def predecessor(b: Int): Int = b - 1

sumOf(2, 3, square)
sumOf(2, 3, predecessor)

// The function passed as an argument using a `val`
val identityVal: Int => Int = x => x
sumOf(2, 3, identityVal)

// Or even anonymous function
sumOf(2, 3, x => x)

// `val` evaluates when defined
// `def` evaluates on every call

// A function with no parameter that returns a function Int => Int
// Creates a new function every time the function is called
// The type if squareDef is Function0[Function1[Int, Int]
def squareDef(): Int => Int = {
  print(">>>def<<<") // `print` is a side effect!
  x => x * x
}

// A value, a single function Int => Int, evaluated at definition
val squareVal: Int => Int = {
  print(">>>val<<<")
  x => x * x
}

// A value, a single function Int => Int, evaluated when used for the first time
lazy val squareLazyVal: Int => Int = {
  print(">>>lazy val<<<")
  x => x * x
}

sumOf(2, 3, squareDef())
sumOf(2, 3, squareDef())

sumOf(2, 3, squareVal)
sumOf(2, 3, squareVal)

sumOf(2, 3, squareLazyVal)
sumOf(2, 3, squareLazyVal)

// Call-by-value and call-by-name
// Call-by-value and call-by-name are two evaluation strategies
// Both strategies reduce to the same final values as long as
// - the reduced expression consists of pure functions, and
// - both evaluations terminate.
// Call-by-value evaluates every function argument only once, even if not used in the function body.
// Call-by-name does not evaluate if the corresponding parameter is unused in the evaluation of the function body.
// Scala normally uses call-by-value.

def time(): Long = {
  println("Executing time()")
  java.lang.System.nanoTime()
  /*val rand = scala.util.Random
  rand.nextLong()*/
}

// `t` is now defined as a by-value parameter
// `time()` is called once
def execByValue(t: Long): Long = {
  println("Entered exec, calling t...")
  println(s"t is $t")
  println("Calling t again...")
  t
}

execByValue(time())

// `t` is now defined as a by-name parameter
// `time()` is called twice
def execByName(t: => Long) = {
  println("Entered exec, calling t...")
  println(s"t is $t")
  println("Calling t again...")
  t
}

execByName(time())

// `t` is now defined as a by-value parameter
// `time()` is called once
def execConstantByValue(t: Long): Long = 35221213909789L

execConstantByValue(time())

// `t` is now defined as a by-name parameter
// `time()` is never called
def execConstantByName(t: => Long) = 35221213909789L

execConstantByName(time())
```

## Type system
See [Scala 3 — Book : Variance](https://docs.scala-lang.org/scala3/book/types-variance.html)

Scala is statically-typed, and allows constraints on generic typing.
- `def function[T](arg: T): Unit = ...`
    - T represent an invariant type.
- `def function[+T](arg: T): Unit = ...`
    - T represent a covariant type.
- `def function[-T](arg: T): Unit = ...`
    - T represent a contravariant type. 
- `def function[T <: A](arg: T): Unit = ...`
    - T represent a subtype of A. 
- `def function[T >: A](arg: T): Unit = ...`
    - T represent a supertype of A. 
- `def function[T: A](arg: T): Unit = ...`
    - T represent a type that implements the trait A. 

## List representation
List are chained nodes, which are either Nil, or an element and another list :

`List(1, 2, 3) == 1 :: (2 :: (3 :: Nil))`

# RATTRAPAGE, TEST EXAM
## A - True or False
1. Programming languages are always tied to a specific paradigm. **False**
2. The type Null in Scala 3 is a subtype of every reference type.  **True *(but not of value type)***
3. The type Nothing in Scala 3 is a subtype of every other type. **True**
4. Scala 3's Try represents a computation that may either result in an exception, or return a value. **True**
5. In Scala 3, the Unit type is used to represent methods that do not return a value. **True**
6. Recursion is preferred over loops for iterating through collections. **True**
7. Scala 3 supports tail-call optimisation. **True**
8. Pure functions cannot have internal hidden states that affect their behaviour. **True**
9. Immutability means that once a data structure is created, its internal state cannot change. **True**
10. A mutable collection can be covariant without causing issues related to type safety. **False**
11. In Scala 3, for-comprehensions can only be used with List. **False**
12. Functors preserve the structure of a container while applying a function to its elements. **True**

## B. Fill in the missing parts
1. Implement the function filterEven that takes a list of integers and returns a new list containing only the even numbers. Use a method provided by the Scala standard library on Lists in the body. Complete the two usages of this function.
```scala
def filterEven(numbers: List[Int]): List[Int] =
    numbers.filter(n => n % 2 == 0)
    
filterEven(List(1, 3, 5, 9)) shouldBe List()
filterEven(List()) shouldBe List()
```

2.Implement the function filterSeven that takes a list of integers and returns a new list containingonly the numbers that are multiple of seven. Complete the two usages of this function.
```scala
def filterSeven(xs: List[Int]): List[Int] = xs match
    case Nil => Nil
    case head :: tail if (head % 7 == 0) => head :: filterSeven(tail)
    case _ :: tail => filterSeven(tail)
    
filterSeven(List(14, 11, 35, 36, 21, 9)) shouldBe List(14, 35, 21)
filterSeven(List()) shouldBe List()
```

3. Complete the following expressions. Consider Either is right biased.
```scala
Right(41).map((x: Int) => x + 1) shouldBe Right(42)
Right(4).flatMap((x: Int) => Right(x * x)) shouldBe Right(16)
Left("oops").map((x: Int) => x + 1) shouldBe Left("oops")
Right(24).filterOrElse(x => x % 2 == 1, "even") shouldBe Left("even")
```

4. Complete the for-comprehension expression, evaluation result and equivalent expression (?)
```scala
val result1: List[Int] = for {
    a <- List(1, 2, 3, 4)
    b <- Some(4) if (b + a) % 2 == 1
} yield a * b

result1 shouldBe List(4, 12)

List(1, 2, 3, 4).flatMap(a =>
    Some(4).filter(b => (b + a) % 2 == 1).map(b => a * b)
) shouldBe result1
```

5. Complete the missing types in the function `sumF` signature. Complete the usage of the sumId and sumSquare functions.
```scala
def sumF(f: Int => Int, xs: List[Int]): Int =
    xs.map(x => f(x)).sum

def sumId(xs: List[Int]) = sumF(x => x, xs)
def sumSquare(xs: List[Int]) = sumF(x => x * x, xs)

sumId(List(41, 1)) shouldBe 42
sumSquare(List(5, 4)) + 1 shouldBe 42
```

## C. Answer as clearly and as completely as you can
1. Write a tail recursive function `last` that returns an `Option` containing the last element of the List if it exists. See usages below:
```scala
last(List("a","b","c","d")) == Some("d")
last(Nil) == None

@tailrec
final def last[T](xs: List[T]): Option[T] =
    xs match
        case Nil => None
        case y :: Nil => Some(y)
        case y :: ys => last(ys)
```

2. Write a tail recursive function `nth` that returns an `Option` containing the element of the List at index i if it exists. See usages below:
```scala
nth(List("a","b","c","d","e"), 2) == Some("c")
nth(List("a"), 2) == None
nth(Nil, 0) == None

@tailrec
final def nth[T](xs: List[T], i: Int): Option[T] =
    xs match 
        case Nil => None
        case y :: _ if i == 0 => Some(y)
        case y :: ys => nth(ys, i - 1)
```

3. Write a tail recursive function reverse that returns the original List with its elements in reverse order. See usages below:
```scala
reverse(List("a","b","c")) == List("c","b","a")
reverse(Nil) == Nil

final def reverse[T](xs: List[T]): List[T] = {
    @tailrec
    def loop(ys: List[T], acc: List[T]): List[T] =
        ys match
            case Nil => acc
            case y :: ys => loop(ys, y :: acc)
        
    loop(xs, List())
}
```

4. Explain what is tail recursion and its main benefit.

Tail-recursion is a compiler optimization for recursive functions, which lets the computer reuse the same stack frame for each call of the function, leading to faster execution and no possibility of a stack overflow.

It is applicable if the recursive call met 3 conditions:
- It is the last instruction of the function
- It carries all needed information (no side-effect)
- It immediately returns
