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

### 1.5   Control 控制循环语句

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
