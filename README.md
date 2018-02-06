# CS61a Structure and Interpretation of Computer Programs

Learning programming using Python

## Chapter 1: Building Abstractions with Functions

### 1.1   Getting Started
### 1.2   Elements of Programming

1. primitive expressions and statements, which represent the simplest building blocks that the language provides,
2. means of combination, by which compound elements are built from simpler ones, and
3. means of abstraction, by which compound elements can be named and manipulated as units.


##### 1.2.4   Names and the Environment

A critical aspect of a programming language is the means it provides for using names to refer to computational objects. If a value has been given a name, we say that the name binds to the value.

In Python, we can establish new bindings using the assignment statement, which contains a name to the left of = and a value to the right:

##### 1.2.5   Evaluating Nested Expressions

To evaluate a call expression, Python will do the following:

1. Evaluate the operator and operand subexpressions, then
2. Apply the function that is the value of the operator subexpression to the arguments that are the values of the operand subexpressions.

### 1.3   Defining New Functions

  ```python

  def <name>(<formal parameters>):
    return <return expression>


  ```

  Aspects of a functional abstraction.
  To master the use of a functional abstraction, it is often useful to consider its three core attributes.
  1.  The domain of a function is the set of arguments it can take.
  2. The range of a function is the set of values it can return.
  3. The intent of a function is the relationship it computes between inputs and output (as well as any side effects it might generate).


### 1.4   Designing Functions

1. Each function should have exactly one job. That job should be identifiable with a short name and characterizable in a single line of text. Functions that perform multiple jobs in sequence should be divided into multiple functions.
2. Don't repeat yourself is a central tenet of software engineering. The so-called DRY principle states that multiple fragments of code should not describe redundant logic. Instead, that logic should be implemented once, given a name, and applied multiple times. If you find yourself copying and pasting a block of code, you have probably found an opportunity for functional abstraction.
3. Functions should be defined generally. Squaring is not in the Python Library precisely because it is a special case of the pow function, which raises numbers to arbitrary powers.


##### 1.4.1   Documentation
A function definition will often include documentation describing the function, called a docstring, which must be indented along with the function body. Docstrings are conventionally triple quoted. The first line describes the job of the function in one line. The following lines can describe arguments and clarify the behavior of the function:

```python
>>> def pressure(v, t, n):
        """Compute the pressure in pascals of an ideal gas.

        Applies the ideal gas law: http://en.wikipedia.org/wiki/Ideal_gas_law

        v -- volume of gas, in cubic meters
        t -- absolute temperature in degrees kelvin
        n -- particles of gas
        """
        k = 1.38e-23  # Boltzmann's constant
        return n * k * t / v
```

#####1.4.2   Default Argument Values

```python

>>> def pressure(v, t, n=6.022e23):
      """Compute the pressure in pascals of an ideal gas.

      v -- volume of gas, in cubic meters
      t -- absolute temperature in degrees kelvin
      n -- particles of gas (default: one mole)
      """
      k = 1.38e-23  # Boltzmann's constant
      return n * k * t / v

```

### 1.5   Control

#### 1.5.1   Statements

Rather than being evaluated, statements are executed. Each statement describes some change to the interpreter state, and executing a statement applies that change. As we have seen for return and assignment statements, executing statements can involve evaluating subexpressions contained within them.

Sometimes it does make sense to have a function whose body is an expression, when a non-pure function like print is called.

```python
>>> def print_square(x):
        print(square(x))
```
#### 1.5.2   Compound Statements
Compound statements typically span multiple lines and start with a one-line header ending in a colon, which identifies the type of statement. Together, a header and an indented suite of statements is called a clause. A compound statement consists of one or more clauses:
```Python

<header>:
    <statement>
    <statement>
    ...
<separating header>:
    <statement>
    <statement>
    ...
...

```

We can understand the statements we have already introduced in these terms.

1. Expressions, return statements, and assignment statements are simple statements.
2. A def statement is a compound statement. The suite that follows the def header defines the function body.

#### 1.5.3   Defining Functions II: Local Assignment

Whenever a user-defined function is applied, the sequence of clauses in the suite of its definition is executed in a local environment — an environment starting with a local frame created by calling that function. A return statement redirects control: the process of function application terminates whenever the first return statement is executed, and the value of the return expression is the returned value of the function being applied.

```pythyon
>>> def percent_difference(x, y):
        return 100 * abs(x-y) / x
>>> percent_difference(40, 50)
25.0
```
#### 1.5.4   Conditional Statements
Conditional statements. A conditional statement in Python consists of a series of headers and suites: a required if clause, an optional sequence of elif clauses, and finally an optional else clause:

```python
if <expression>:
    <suite>
elif <expression>:
    <suite>
else:
    <suite>
```

When executing a conditional statement, each clause is considered in order. The computational process of executing a conditional clause follows.

1. Evaluate the header's expression.
2. If it is a true value, execute the suite. Then, skip over all subsequent clauses in the conditional statement.

Boolean operators. Three basic logical operators are also built into Python:

```python
>>> True and False
False
>>> True or False
True
>>> not False
True
```
#### 1.5.5   Iteration

We can use a while statement to enumerate n Fibonacci numbers. We need to track how many values we've created (k), along with the kth value (curr) and its predecessor (pred). Step through this function and observe how the Fibonacci numbers evolve one by one, bound to curr.

```python
def fib(n):
	    """Compute the nth Fibonacci number, for n >= 2."""
      pred, curr = 0, 1   # Fibonacci numbers 1 and 2
      k = 2               # Which Fib number is curr?
	    while k < n:
	        pred, curr = curr, pred + curr
	        k = k + 1
      return curr

	result = fib(8)
```
A while clause contains a header expression followed by a suite:

```python
while <expression>:
    <suite>
```

To execute a while clause:

1. Evaluate the header's expression.
2. If it is a true value, execute the suite, then return to step 1.

In step 2, the entire suite of the while clause is executed before the header expression is evaluated again.

In order to prevent the suite of a while clause from being executed indefinitely, the suite should always change some binding in each pass.

A while statement that does not terminate is called an infinite loop. Press <Control>-C to force Python to stop looping.

#### 1.5.6   Testing

Assertions. Programmers use assert statements to verify expectations, such as the output of a function being tested. An assert statement has an expression in a boolean context, followed by a quoted line of text (single or double quotes are both fine, but be consistent) that will be displayed if the expression evaluates to a false value.

```python
>>> assert fib(8) == 13, 'The 8th Fibonacci number should be 13'
```

A test function for fib should test several arguments, including extreme values of n.
```python
>>> def fib_test():
        assert fib(2) == 1, 'The 2nd Fibonacci number should be 1'
        assert fib(3) == 1, 'The 3rd Fibonacci number should be 1'
        assert fib(50) == 7778742049, 'Error at the 50th Fibonacci number'
```
When writing Python in files, rather than directly into the interpreter, tests are typically written in the same file or a neighboring file with the suffix _test.py.



### 1.6   Higher-Order Functions
#### 1.6.1   Functions as Arguments
Consider the following three functions, which all compute summations. The first, sum_naturals, computes the sum of natural numbers up to n:

```python
>>> def sum_naturals(n):
        total, k = 0, 1
        while k <= n:
            total, k = total + k, k + 1
        return total
>>> sum_naturals(100)
5050
```

The second, sum_cubes, computes the sum of the cubes of natural numbers up to n.

```python
>>> def sum_cubes(n):
        total, k = 0, 1
        while k <= n:
            total, k = total + k*k*k, k + 1
        return total
>>> sum_cubes(100)
25502500
```
The third, pi_sum, computes the sum of terms in the series


which converges to pi very slowly.
```python
>>> def pi_sum(n):
        total, k = 0, 1
        while k <= n:
            total, k = total + 8 / ((4*k-3) * (4*k-1)), k + 1
        return total
>>> pi_sum(100)
3.1365926848388144
```

These three functions clearly share a common underlying pattern. They are for the most part identical, differing only in name and the function of k used to compute the term to be added. We could generate each of the functions by filling in slots in the same template:

```python
def <name>(n):
    total, k = 0, 1
    while k <= n:
        total, k = total + <term>(k), k + 1
    return total

```

#### 1.6.2   Functions as General Methods

By tracing through the steps of evaluation, we can see how this result is computed. First, a local frame for improve is constructed with bindings for update, close, and guess. In the body of improve, the name close is bound to square_close_to_successor, which is called on the initial value of guess. Trace through the rest of the steps to see the computational process that evolves to compute the golden ratio.

```Python
def improve(update, close, guess=1):
    while not close(guess):
        guess = update(guess)
    return guess

def golden_update(guess):
    return 1/guess + 1

def square_close_to_successor(guess):
    return approx_eq(guess * guess, guess + 1)

def approx_eq(x, y, tolerance=1e-3):
    return abs(x - y) < tolerance

phi = improve(golden_update,square_close_to_successor)


```
This example illustrates two related big ideas in computer science. First, naming and functions allow us to abstract away a vast amount of complexity. While each function definition has been trivial, the computational process set in motion by our evaluation procedure is quite intricate. Second, it is only by virtue of the fact that we have an extremely general evaluation procedure for the Python language that small components can be composed into complex processes. Understanding the procedure of interpreting programs allows us to validate and inspect the process we have created.


#### 1.6.3   Defining Functions III: Nested Definitions
```python
>>> def sqrt(a):
        def sqrt_update(x):
            return average(x, a/x)
        def sqrt_close(x):
            return approx_eq(x * x, a)
        return improve(sqrt_update, sqrt_close)
```

Like local assignment, local def statements only affect the current local frame. These functions are only in scope while sqrt is being evaluated. Consistent with our evaluation procedure, these local def statements don't even get evaluated until sqrt is called.


Lexical scope. Locally defined functions also have access to the name bindings in the scope in which they are defined. In this example, sqrt_update refers to the name a, which is a formal parameter of its enclosing function sqrt. This discipline of sharing names among nested definitions is called lexical scoping. Critically, the inner functions have access to the names in the environment where they are defined (not where they are called).

We require two extensions to our environment model to enable lexical scoping.

1. Each user-defined function has a parent environment: the environment in which it was defined.
2. When a user-defined function is called, its local frame extends its parent environment.

```Python
def average(x, y):
    return (x + y)/2

def improve(update, close, guess=1):
	   while not close(guess):
	       guess = update(guess)
	   return guess

def approx_eq(x, y, tolerance=1e-3):
	   return abs(x - y) < tolerance

def sqrt(a):
	   def sqrt_update(x):
	       return average(x, a/x)
	   def sqrt_close(x):
	       return approx_eq(x * x, a)
	   return improve(sqrt_update, sqrt_close)

result = sqrt(256)
```
The most critical part of this evaluation procedure is the transfer of the parent for sqrt_update to the frame created by calling sqrt_update. This frame is also annotated with [parent=f1].

Extended Environments. An environment can consist of an arbitrarily long chain of frames, which always concludes with the global frame. Previous to this sqrt example, environments had at most two frames: a local frame and the global frame. By calling functions that were defined within other functions, via nested def statements, we can create longer chains. The environment for this call to sqrt_update consists of three frames: the local sqrt_update frame, the sqrt frame in which sqrt_update was defined (labeled f1), and the global frame.

The return expression in the body of sqrt_update can resolve a value for a by following this chain of frames. Looking up a name finds the first value bound to that name in the current environment. Python checks first in the sqrt_update frame -- no a exists. Python checks next in the parent frame, f1, and finds a binding for a to 256.

Hence, we realize two key advantages of lexical scoping in Python.

1. The names of a local function do not interfere with names external to the function in which it is defined, because the local function name will be bound in the current local environment in which it was defined, rather than the global environment.
2. A local function can access the environment of the enclosing function, because the body of the local function is evaluated in an environment that extends the evaluation environment in which it was defined.
The sqrt_update function carries with it some data: the value for a referenced in the environment in which it was defined. Because they "enclose" information in this way, locally defined functions are often called closures.

#### 1.6.4   Functions as Returned Values
#### 1.6.5   Example: Newton's Methods
#### 1.6.6   Currying
#### 1.6.7   Lambda Expressions
#### 1.6.8   Abstractions and First-Class Functions
#### 1.6.9   Function Decorators

### 1.7   Recursive Functions
#### 1.7.1   The Anatomy of Recursive Functions
#### 1.7.2   Mutual Recursion
#### 1.7.3   Printing in Recursive Functions
#### 1.7.4   Tree Recursion
#### 1.7.5   Example: Partitions
```Python
Syntax highlighted code block

# Header 1
## Header 2
### Header 3


[Link](url) and ![Image](src)
```



For more details see [Functions of Programming](http://composingprograms.com/pages/12-elements-of-programming.html).

## Chapter 2: Building Abstractions with Data

Building Abstractions with Data

```Python
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Building Abstractions with Data](http://composingprograms.com/pages/21-introduction.html).

## Chapter 3: Interpreting Computer Programs

Interpreting Computer Programs

```Python
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Interpreting Computer Programs](http://composingprograms.com/pages/31-introduction.html).



## Chapter 4: Data Processing

Data Processing

```Python
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Data Processing](http://composingprograms.com/pages/41-introduction.html).

## The course home page

The full course detail [Course info](https://cs61a.org/).
