# Functional Programing
**Teacher** : MAZELIER Gaylord \
**Moodle Link** : https://moodle.myefrei.fr/course/view.php?id=20410

# Lambda Calculus
| What        | How                       | Example |
|-------------|---------------------------|---------|
| Variable    | \<name\>                  | a       |  
| Function    | λ\<params\>.\<body\>      | λa.a    |
| Application | (\<func\>)\<var of func\> | (λx.x)a |

## Church numerals
``ZERO (0) = λf.λx.x`` \
``SUCC = λn.λf.λx.(f((nf)x))`` \
``ONE   = SUCC(0) = λf.λx.(fx)`` \
``TWO   = SUCC(1) = λf.λx.(f(fx))`` \
``THREE = SUCC(2) = λf.λx.(f(f(fx)))``

# Programming Concepts
- **Record** : Structured, immutable data that groups related values.
- **Closure** : A function bundled with the environemment (values) it captures from it's scope.
- **Concurrency** : Running multiple computation at the same time.
- **State** : Named, changing data over time, stored in memory.

# FP Concepts/Principles
- **Pure function** : Function that depends only on it's inputs, without any side-effects. This means it's always predicatble, deterministic
- **Immutability** : Data doesn't change after being created
- **Higher-order function**
- **Currying**
- **Recursion**
