+++
title = "Number sets"

# date = {{ .Date }}
lastmod = 2019-05-29

draft = false       # Is this a draft? true/false
toc = true          # Show table of contents? true/false
type = "docs"       # Do not modify.

# Add menu entry to sidebar.
[menu.mathematicalbackground]
  name = "Number sets"
  parent = "Complex numbers and phasors"
  weight = 1

+++

In mathematics, sets are defined as collections of objects.
Number sets can therefore be regarded as collections of numbers.
These number sets can be distinguished by the set to which they belong, each allowing for more flexibility when working with them.

## Natural numbers
Numbers have been present in human history since the ancient Egyptians (and possibly even earlier).
They used numbers for counting objects, such as the amount of camels or quarry stones (to stay within the theme of the ancient Egyptians).
The amount of these objects is discrete, i.e. they are either there or they are not. Partial objects do not exist.
The discrete countable set of these objects is called the set of natural numbers and is denoted by $ \mathbb{N} $.
The mathematical representation of this set is given by
$$ \mathbb{N} = \\{ 0, 1,2,\dots \\} .$$
_The presence of the number 0 in this set is often debatable, however, following conventions the number is included._

## Integer numbers
The set of natural numbers always allowed for addition, however, other mathematical operations, such as subtraction, were not always allowed.
Suppose you own €5 and you make a trade, which costs you €7.
This obviously means that you owe the other person €2.
Both the number 5 and 7 are in the set of natural numbers.
This can be written mathematically as $ \\{5,7 \\} \in \mathbb{N} $, where the symbol $ \in $ means "is part of".
The current financial balance of the person who made the trade is now -€2.
However, this number is not in the set of natural numbers and therefore this subtraction is not allowed.
From this we can conclude that performing subtraction in the set of natural numbers does not guarantee that you end up with a result in this same set.
In order to allow for subtraction in the set of natural numbers, the set needs to be expanded to include negative integer numbers.
This new set is called the set of integer numbers and is represented mathematically as
$$ \mathbb{Z} = \\{ \dots, -2, -1, 0, 1,2,\dots \\} .$$

## Rational numbers
With the numbers in this set, many operations like addition, subtraction and multiplication can be performed.
However, division of the numbers in this set might result in a number which is not an integer number (e.g. one divided by 2 results in 1/2 = 0.5, where 0.5 is not an integer).
To allow for division of all numbers in the set of integer numbers $\mathbb{Z}$, the set of all rational numbers $\mathbb{Q}$ is introduced, which in addition to all numbers in set Z also contains all fractions.
This set is denoted mathematically as
$$ \mathbb{Q} = \\{ \frac{a}{b}: a,b \in \mathbb{Z}, b \neq 0\\} .$$
This set can be described in easy words as: the set of fractions, $a$ divided by $b$, where $a$ and $b$ are integer numbers and $b$ is not equal to zero.

## Real numbers
With the set of rational numbers, almost all commonly used numbers can be described.
However, it still offers some limitations, since some numbers can not be written as a fraction.
Examples of these numbers are $\sqrt{2}$, $\pi$ and $e$.
In order to include these numbers, the set of real numbers $\mathbb{R}$ is defined as the set of all numbers between $-∞$ and $∞$.

## Complex numbers

### Derivation 1
One important property of the set of real numbers is that the square of an arbitrary number in that set is larger or equal than 0, i.e. $x^2 \geq 0 \quad \forall \quad x\in \mathbb{R}$.
This allows for solving most quadratic equations ($ax^2 + bx + c = 0$) easily using the quadratic formula, where the solution to these equations is given by
$$ x = \frac{-b\pm\sqrt{b^2-4ac}}{2a}.$$
Using this equation many quadratic equations can be solved very easily, however, sometimes the solution is not present in the set of real numbers.
To demonstrate this, let us focus on the following example, where we are trying to solve $x^2 + x + 1 = 0$.
From the quadratic equation our solutions follow as
$$ x=\frac{-1 \pm \sqrt{-3}}{2},$$
which can be rewritten as
$$ x = -\frac{1}{2} \pm \frac{\sqrt{3}}{2}\sqrt{-1}. $$
In this expression the only term that is not defined by the set of real numbers is $\sqrt{-1}$.
This means that the solution to the original equation cannot be found.
In order to still obtain a solution the imaginary unit $j$ (or $i$, but in the Electrical Engineering study this often causes confusion with current) is introduced as $j = \sqrt{-1}$.
Now, the solution to _any_ quadratic equation can be found as $x=a+j\cdot b$.
This expanded set of numbers is called the set of complex numbers $\mathbb{C}$ and is mathematically denoted as
$$ \mathbb{C} = \\{ a+j\cdot b: a,b \in \mathbb{R}\\}.$$

### Derivation 2
Besides the previous example describing the necessity of the complex numbers, another example is described.
In engineering it is quite common to describe a practical problem by a mathematical model.
For example a mathematical model that describes the movement $f(\theta)$, as a function of the position $\theta$, of a harmonic oscillator is given by the following (simplified) second order differential equation:
$$\frac{d^2}{d\theta^2}\\{ f(\theta)\\} + f(\theta) = 0$$
A general solution of this equation is given by the function $f(\theta)= e^{c\theta}$, in which $\theta \in \mathbb{R}$ is the function argument and $c \in \mathbb{R}$ is some unknown constant.
Substituting this solution in the differential equation results in the following:
$$c^2(e^{c\theta}) + e^{c\theta} = 0 $$
where the constant c is given by the solutions to the equation $c^2 +1 = 0$.
These solutions are given by $c = \pm \sqrt{-1}$.
Again we can see the necessity of introducing the imaginary unit $j$.

## Visualisation of the number sets
TODO: add image from reader
