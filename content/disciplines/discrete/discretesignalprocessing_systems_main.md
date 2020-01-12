+++
title = "Discrete-time systems"

# date = {{ .Date }}
lastmod = 2019-10-10

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Discrete-time systems"
  weight = 40

+++

## Module overview
This module will introduce basic filter structures for filtering discrete-time signals.

1. <a href="../discretesignalprocessing_systems_fir/">Finite impulse response (FIR) filter</a> - The most basic filter is defined as a finite impulse response filter. This section also introduces the commonly used convolution operator.
2. **Infinite impulse response (IIR) filter** (to be added) - Besides filters with a finite impulse response, there also exist filters whose output depends on their previous outputs. This recursive operations leads to infinite impulse response filters, which posses different characteristics in comparison to finite impulse response filters.
3. **Special convolution methods** (to be added) - When performing filter calculations with a limited amount of memory, convolutions might not be possible to calculate if the signal length is very long. In order to circumvent this problem new procedures have been developed in order to split the convolution operation in multiple smaller ones.

<br></br>
