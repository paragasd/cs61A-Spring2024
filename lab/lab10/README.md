Lab 10: Interpreters | CS 61A Spring 2024
========================================

Lab 10: Interpreters[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab10 "Direct link to Lab 10: Interpreters")
-------------------------------------------------------------------------------------------------

*   [lab10.zip](https://www.learncs.site/assets/files/lab10.zip)

_Due by 11:59pm on Wednesday, April 10._

Starter Files[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab10#starter-files "Direct link to Starter Files")
-------------------------------------------------------------------------------------------------

Download [lab10.zip](https://www.learncs.site/assets/files/lab10.zip). Inside the archive, you will find starter files for the questions in this lab, along with a copy of the [Ok](https://cs61a.org//lab/lab10/ok) autograder.

### Topics[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab10#topics "Direct link to Topics")
------------------------------------------------------------------------------------------------

Consult this section if you need a refresher on the material for this lab. It's okay to skip directly to the questions and refer back here should you get stuck.

An interpreter is a program that allows you to interact with the computer using a specific language. It takes the code you write, interprets it, and then executes the corresponding actions, often using a more fundamental language to communicate with the computer hardware.

In Project 4, you'll develop an interpreter for the Scheme programming language using Python. Interestingly, the Python interpreter you've been using throughout this course is primarily written in the C programming language. At the lowest level, computers operate by interpreting machine code, which is a series of ones and zeros that instructs the computer on performing basic tasks such as arithmetic operations and data retrieval.

When we talk about an interpreter, there are two languages at work:

- The language being interpreted: For Project 4, this is the Scheme language.
- The implementation language: This is the language used to create the interpreter itself, which, for Project 4, will be Python.

### REPL[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab10#repl "Direct link to REPL")
----------------------------------------------------------------------------------------------------

A common feature of interpreters is the Read-Eval-Print Loop (REPL), which processes user inputs in a cyclic fashion through three stages:

1. **Read**: The interpreter first reads the input string provided by the user. This input goes through a parsing process that involves two key steps:

    - The **lexical analysis** step breaks down the input string into tokens, which are the basic elements or "words" of the language you're interpreting. These tokens represent the smallest units of meaning within the input.
    - The **syntactic analysis** step takes the tokens from the previous step and organizes them into a data structure that the underlying language can understand. For our Scheme interpreter, we assemble the tokens into a Pair object (similar to a Link), to represent the structure of the original call expression.

2. **Eval**: This step evaluates the expressions you've written in that programming language to obtain a value. It involves the following two functions:

    - `eval` takes an expression and evaluates it based on the language's rules. When the expression is a call expression, `eval` uses the `apply` function to obtain the result. 
    - `apply` takes the evaluated operator (the function) and applies it to the evaluated operands (the arguments). 

3. **Print**: Display the result of evaluating the user input.

Here's how all the pieces fit together:

```scheme
(+ 1 2)   ; read, eval, and print result: 3
```

### Required Questions[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab10#required-questions "Direct link to Required Questions")
------------------------------------------------------------------------------------------------------------

### Getting Started Videos[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab10#getting-started-videos "Direct link to Getting Started Videos")
-------------------------------------------------------------------------------------------------------

These videos may provide some helpful direction for tackling the coding problems on this assignment.

> To see these videos, you should be logged into your berkeley.edu email.

[YouTube link](https://youtu.be/playlist?list=PLx38hZJ5RLZdwIF0I28zXMYAvd-BQ2nWY)

### Calculator[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab10#calculator "Direct link to Calculator")
------------------------------------------------------------------------------------------------------------

An interpreter is a program that executes programs. Today, we will extend the interpreter for Calculator, a simple made-up language that is a subset of Scheme. This lab is like Project 4 in miniature.

The Calculator language includes only the four basic arithmetic operations: `+`, `-`, `*`, and `/`. These operations can be nested and can take various numbers of arguments, just like in Scheme.

#### Pair Class
To represent Scheme lists in Python, we will use the Pair class (in both this lab and the Scheme project). A Pair instance has two attributes: `first` and `rest`. 

```python
class Pair:
    """Represents the built-in pair data structure in Scheme."""
    def __init__(self, first, rest):
        self.first = first
        self.rest = rest
```

### Q1: Using Pair[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab10#q1-using-pair "Direct link to Q1: Using Pair")
------------------------------------------------------------------------------------------------------

Answer the following questions about a Pair instance representing the Calculator expression `(+ (- 2 4) 6 8)`.

Use Ok to test your understanding:

    python3 ok -q using_pair -u

### Calculator Evaluation[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab10#calculator-evaluation "Direct link to Calculator Evaluation")
--------------------------------------------------------------------------------------------------------

For Question 2 (New Procedure) and Question 4 (Saving Values), you'll need to update the `calc_eval` function below, which evaluates a Calculator expression. For Question 2, you'll determine what are the operator and operands for a call expression in Scheme as well as how to apply a procedure to arguments the `calc_apply` line.

```python
def calc_eval(exp):
    """
    >>> calc_eval(Pair("define", Pair("a", Pair(1, nil))))
    'a'
    >>> calc_eval("a")
    1
    >>> calc_eval(Pair("+", Pair(1, Pair(2, nil))))
    3
    """
    if isinstance(exp, Pair):
        operator = ____________  # UPDATE THIS FOR Q2
        operands = ____________  # UPDATE THIS FOR Q2
        return calc_apply(___________, ___________)  # UPDATE THIS FOR Q2
```

### Q2: New Procedure[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab10#q2-new-procedure "Direct link to Q2: New Procedure")
---------------------------------------------------------------------------------------------------------

Add the `//` operation to Calculator, a floor-division procedure such that `(// dividend divisor)` returns the result of dividing dividend by divisor.

```python
def floor_div(args):
    """
    >>> floor_div(Pair(100, Pair(10, nil)))
    10
    >>> floor_div(Pair(5, Pair(3, nil)))
    1
    >>> floor_div(Pair(1, Pair(1, nil)))
    1
    >>> floor_div(Pair(5, Pair(2, nil)))
    2
    """
    "*** YOUR CODE HERE ***"
```

Use Ok to test your code:

    python3 ok -q floor_div

### Q3: New Form[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab10#q3-new-form "Direct link to Q3: New Form")
-------------------------------------------------------------------------------------------------------

Add `and` expressions to our Calculator interpreter as well as introduce the Scheme boolean values `#t` and `#f`, represented as Python `True` and `False`.

```python
def eval_and(expressions):
    """
    >>> calc_eval(Pair("and", Pair(1, nil)))
    1
    >>> calc_eval(Pair("and", Pair(False, Pair("1", nil))))
    False
    """
    "*** YOUR CODE HERE ***"
```

Use Ok to test your code:

    python3 ok -q eval_and

### Q4: Saving Values[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab10#q4-saving-values "Direct link to Q4: Saving Values")
-------------------------------------------------------------------------------------------------------

Implement a `define` special form that binds values to symbols. This should work like `define` in Scheme.

```python
bindings = {}

def eval_define(expressions):
    """
    >>> eval_define(Pair("a", Pair(1, nil)))
    'a'
    >>> eval_define(Pair("b", Pair(3, nil)))
    'b'
    >>> eval_define(Pair("c", Pair("a", nil)))
    'c'
    >>> calc_eval("c")
    1
    """
    "*** YOUR CODE HERE ***"
```

Use Ok to test your code:

    python3 ok -q eval_define

### Check Your Score Locally[​](https://www.learncs.site/docs/curriculum-resource/cs61a/lab/lab10#check-your-score-locally "Direct link to Check Your Score Locally")
-------------------------------------------------------------------------------------------------------------------

You can locally check your score on each question of this assignment by running:

```bash
python3 ok --score
```

### Submit
-------------------------------------------------------------------------------------------------------------

Submit this assignment by uploading any files you've edited to the appropriate Gradescope assignment.

