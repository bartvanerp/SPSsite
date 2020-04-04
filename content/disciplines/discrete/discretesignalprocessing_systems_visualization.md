+++
title = "System visualization"

# date = {{ .Date }}
lastmod = 2020-04-04

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "System visualization"
  weight = 2
  parent = "Discrete-time systems"
+++


## Basic building blocks LTI system
When realizing or implementing a discrete-time system, we need the following basic building blocks: A multiplier, which multiplies signal sample $x[n]$ by a scalar $\beta$ which results in a sample with value $y[n] = \beta \cdot x[n]$; An adder which adds two signal samples $x_1[n]$ and $x_2[n]$ together into $y[n]= x_1[n] + x_2[n]$ and finally an unit-delay operator which delays a signal sample $x[n]$ by one sample index into $y[n]=x[n-1]$. These basic building blocks are depicted in Fig. 1.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/basicbuildingblocks.svg"
      alt="Basic building blocks of a discrete-time system."
    />
    <figcaption class="numbered">
      Basic building blocks of a discrete-time system.
    </figcaption>
  </figure>
</div>

## Realization scheme and Difference Equation LTI system
Fig. 2 shows the realization scheme, or flow diagram, of a basic LTI system.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/flowdiagram.svg"
      alt="Signal flow diagram or realization scheme of a basic LTI system."
    />
    <figcaption class="numbered">
      Signal flow diagram or realization scheme of a basic LTI system.
    </figcaption>
  </figure>
</div>
The LTI systems that we consider in this reader can have both a feed forward path with coefficients $b_0$ until $b_{M-1}$ and feedback path with coefficients $a_1$ until $a_{N-1}$. From the figure it follows that we can describe such a basic LTI system with the following Difference Equation (DE):
\begin{equation}
y[n] = \sum_{k=0}^{M-1} b_k x[n-k] + \sum_{k=1}^{N-1} a_k y[n-k]
\end{equation}
