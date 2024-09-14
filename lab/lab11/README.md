Lab 11: Programs as Data, Macros | CS 61A Spring 2024
=====================================================

Lab 11: Programs as Data, Macros[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab11 "Direct link to Lab 11: Programs as Data, Macros")
---------------------------------------------------------------------------------------------------------------

*   [lab11.zip](https://www.learncs.site/assets/files/lab11.zip)

_Due by 11:59pm on Wednesday, April 17._

Starter Files[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab11#starter-files "Direct link to Starter Files")
-------------------------------------------------------------------------------------------------------------------------------

Download [lab11.zip](https://www.learncs.site/assets/files/lab11.zip). Inside the archive, you will find starter files for the questions in this lab, along with a copy of the [Ok](https://cs61a.org//lab/lab11/ok) autograder.

### Required Questions[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab11#required-questions "Direct link to Required Questions")
------------------------------------------------------------------------------------------------------

### Getting Started Videos[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab11#getting-started-videos "Direct link to Getting Started Videos")
-----------------------------------------------------------------------------------------------------

These videos may provide some helpful direction for tackling the coding problems on this assignment.

> To see these videos, you should be logged into your berkeley.edu email.

[YouTube link](https://youtu.be/playlist?list=PLx38hZJ5RLZdwIF0I28zXMYAvd-BQ2nWY)

### Quasiquotation[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab11#quasiquotation "Direct link to Quasiquotation")
-----------------------------------------------------------------------------------------------------

Consult the drop-down if you need a refresher on quasiquotation. It's okay to skip directly to the questions and refer back here should you get stuck.

The normal quote `'` and the quasiquote `` ` `` are both valid ways to quote an expression. However, the quasiquoted expression can be unquoted with the "unquote" `,` (represented by a comma). When a term in a quasiquoted expression is unquoted, the unquoted term is evaluated, instead of being taken as literal text.

```scheme
scm> (define a 5)
a
scm> (define b 3)
b
scm> `(* a b)  ; Quasiquoted expression
(* a b)
scm> `(* a ,b)  ; Unquoted b, which evaluates to 3
(* a 3)
scm> `(* ,(+ a b) b)  ; Unquoted (+ a b), which evaluates to 8
(* 8 b)
```

### Q1: WWSD: Quasiquote[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab11#q1-wwsd-quasiquote "Direct link to Q1: WWSD: Quasiquote")
------------------------------------------------------------------------------------------------------------

Use Ok to test your knowledge with the following "What Would Scheme Display?" questions:

```bash
python3 ok -q wwsd-quasiquote -u
```

```scheme
scm> '(1 x 3)
scm> (define x 2)
scm> `(1 x 3)
scm> `(1 ,x 3)
scm> `(1 x ,3)
scm> `(1 (,x) 3)
scm> `(1 ,(+ x 2) 3)
scm> (define y 3)
scm> `(x ,(* y x) y)
scm> `(1 ,(cons x (list y 4)) 5)
```

### Programs as Data[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab11#programs-as-data "Direct link to Programs as Data")
------------------------------------------------------------------------------------------------------

Consult the drop-down if you need a refresher on Programs as Data. It's okay to skip directly to the questions and refer back here should you get stuck.

All Scheme programs are made up of expressions. There are two types of expressions: primitive (a.k.a atomic) expressions and combinations. Here are some examples of each:

- Primitive/atomic expression: `#f`, `1.7`, `+`
- Combinations: `(factorial 10)`, `(/ 8 3)`, `(not #f)`

Scheme represents combinations as a Scheme list. Therefore, a combination can be constructed through list manipulation.

```scheme
scm> (define expr (list '+ 2 2))
expr
scm> expr
(+ 2 2)
scm> (eval expr)
4
```

Quasiquotation is very helpful for building procedures that create expressions. Take a look at the following `add-program`:

```scheme
scm> (define (add-program x y)
       `(+ ,x ,y))
add-program
scm> (add-program 3 6)
(+ 3 6)
```

### Q2: If Program[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab11#q2-if-program "Direct link to Q2: If Program")
----------------------------------------------------------------------------------------------------

In Scheme, the `if` special form allows us to evaluate one of two expressions based on a predicate. Write a program `if-program` that takes in the following parameters:

- `predicate`: a quoted expression which will evaluate to the condition in our if-expression
- `if-true`: a quoted expression which will evaluate to the value we want to return if `predicate` evaluates to true (`#t`)
- `if-false`: a quoted expression which will evaluate to the value we want to return if `predicate` evaluates to false (`#f`)

```scheme
(define (if-program condition if-true if-false)
  'YOUR-CODE-HERE
)
```

Use Ok to test your code:

```bash
python3 ok -q if-program
```

### Q3: Exponential Powers[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab11#q3-exponential-powers "Direct link to Q3: Exponential Powers")
-------------------------------------------------------------------------------------------------------

Implement a procedure `(pow-expr base exp)` that returns an expression that, when evaluated, raises the number `base` to the power of the nonnegative integer `exp`. The body of `pow-expr` should not perform any multiplication (or exponentiation). Instead, it should just construct an expression containing only the symbols `square` and `*` as well as the number `base` and parentheses.

```scheme
scm> (pow-expr 2 0)
1
scm> (pow-expr 2 5)
(* 2 (square (square (* 2 1))))
```

```scheme
(define (pow-expr base exp)
    'YOUR-CODE-HERE
)
```

Use Ok to test your code:

```bash
python3 ok -q pow
```

### Macros[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab11#macros "Direct link to Macros")
------------------------------------------------------------------------------------------------------------

A macro is a code transformation that is created using `define-macro` and applied using a call expression. A macro call is evaluated by:

- Binding the formal parameters of the macro to the unevaluated operand expressions of the macro call.
- Evaluating the body of the macro, which returns an expression.
- Evaluating the expression returned by the macro in the frame of the original macro call.

```scheme
scm> (define-macro (twice expr) (list 'begin expr expr))
twice
scm> (twice (+ 2 2))  ; evaluates (begin (+ 2 2) (+ 2 2))
4
```

### Q4: Repeat[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab11#q4-repeat "Direct link to Q4: Repeat")
-------------------------------------------------------------------------------------------------------------

Define `repeat`, a macro that is called on a number `n` and an expression `expr`. Calling it evaluates `expr` in a local frame `n` times, and its value is the final result.

```scheme
(define-macro (repeat n expr)
  `(repeated-call ,n ___))
```

Use Ok to test your code:

```bash
python3 ok -q repeat-lambda
```

The `repeated-call` procedure takes a zero-argument procedure, so `(lambda () ___)` must appear in the blank.

### Check Your Score Locally[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab11#check-your-score-locally "Direct link to Check Your Score Locally")
-------------------------------------------------------------------------------------------------------------------

You can locally check your score on each question of this assignment by running:

```bash
python3 ok --score
```

### Submit[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab11#submit "Direct link to Submit")
-------------------------------------------------------------------------------------------------------------

Submit this assignment by uploading any files you've edited to the appropriate Gradescope assignment.

In addition, all students who are **not** in the mega lab must complete this [attendance form](https://go.cs61a.org/lab-att). The attendance form is not required for mega section students.
