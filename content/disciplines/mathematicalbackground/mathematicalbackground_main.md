+++
title = "Mathematical background"

# date = {{ .Date }}
lastmod = 2019-05-28

draft = false       # Is this a draft? true/false
toc = false         # Show table of contents? true/false
type = "docs"       # Do not modify.

# Add menu entry to sidebar.
[menu.mathematicalbackground]
  name = "Mathematical background: overview"
  weight = 1

+++

The signal processing field deals with the analysis and manipulation of data.
In order to perform operations on this data, a mathematical maturity is required.
This module concerns several elementary but vital mathematical concepts, which are commonly used in the signal processing field.

The concepts covered in this discipline are:

1. <a href="../mathematicalbackground_complex_main">Complex numbers and phasors</a> - In addition to the set of real numbers that everyone is used to working with, a whole new dimension is introduced by complex numbers. These complex numbers can be used to describe sinusoidal signals through phasors, which has proven to be useful in many applications.

2. **Linear algebra** (to be added) - Mathematical operations involving multiple variables can often be sped up significantly using the parallel computational power of graphics processing units (better known as GPU's). These GPU's rely on the underlying principles of linear algebra, which allows us to perform many mathematical operations very efficiently.

3. **Univariate calculus** (to be added) - Functions that describe the underlying principles of a data generating process can be useful in understanding the data originating from this process. These functions can be manipulated to extract important information about this data and to draw conclusions from it.

4. **Multivariate calculus** (to be added) - These functions usually are not only a function of a single variable, but often of multiple variables. Understanding these functions with respect to each of these variables gives insight into the underlying data generating process and allows for better understanding of the underlying process.

5. <a href="../mathematicalbackground_probability_main">Probability and random variables</a> - When uncertainty is involved in noisy signals, exact values cannot be determined. Embracing the random nature of these signals opens up a completely new field, called probability theory, which provides the analytical solution to problems where uncertainty is involved.
