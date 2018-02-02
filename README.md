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
### 1.7   Recursive Functions

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
