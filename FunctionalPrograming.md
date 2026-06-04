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
ZERO (0) = λf.λx.x
SUCC = λn.λf.λx.(f((nf)x))  
ONE   = SUCC(0) = λf.λx.(fx)
TWO   = SUCC(1) = λf.λx.(f(fx))
THREE = SUCC(2) = λf.λx.(f(f(fx)))

# Programming Concepts
- **Record** : Structured, immutable data that groups related values.
- **Closure** : A function bundled with the environemment (values) it captures from it's scope.
- **Concurrency** : Running multiple computation at the same time.
- **State** : Named, changing data over time, stored in memory.

# FP Concepts/Principles
**Pure function** : Function that depends only on it's inputs, without any side-effects. This means it's always predicatble, deterministic
**Immutability** : Data doesn't change after being created
**Higher-order function**
**Currying**
**Recursion**

# Scala
## Functions and primitives
```scala
// Primitive expressions: represent the simplest elements
// (and everything is an expression)
1
"hello"
true

// Expressions: more complex expressions can be created by combination using operators
// https://scala-lang.org/api/3.x/scala/Int.html
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
z2
z2 = 42
z2

// Immutable collections
// https://www.scala-lang.org/api/2.12.7/scala/collection/immutable/List.html
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

def predecessor(b: Int): Int = b -1

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
