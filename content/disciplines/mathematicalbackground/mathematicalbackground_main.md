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

The signal processing field deals with the analysis and manipulation of spatiotemporal data.
In order to perform operations on this data, a mathematical maturity is required.
This module concerns several elementary but vital mathematical concepts, which are commonly used in the signal processing field.

The concepts covered in this discipline are:

1. <a href="../mathematicalbackground_complex_main">Complex numbers and phasors</a> - In addition to the set of real numbers that everyone is used to working with, a whole new dimension is introduced by complex numbers. These complex numbers can be used to describe sinusoidal signals through phasors, which has proven to be useful in many applications.

2. **Linear algebra** (to be added) - Mathematical operations involving multiple variables can often be simplified using linear algebra. It allows us to model complex systems and can be computed efficiently using the parallelism of graphics processing units (better known as GPU's).

3. **Univariate calculus** (to be added) - 
The field of univariate calculate deals with functions involving only a single variable. They allow us to model certain processes.

4. **Multivariate calculus** (to be added) - Multivariate calculus involves functions that depend on multiple variables. These functions allow us to model processes which involve multiple variables.

5. <a href="../mathematicalbackground_probability_main">Probability and random variables</a> - When uncertainty is involved in certain processes, exact values of these processes cannot be determined. We can, however, still measure the noisy signal and process it by taking this uncertainty into account using probability theory. This allows us to explicitely model the uncertainty involved and provides an approach for processing the noisy signal.
