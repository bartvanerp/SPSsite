+++
title = "System properties"

# date = {{ .Date }}
lastmod = 2020-04-04

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "System properties"
  weight = 1
  parent = "Discrete-time systems"
+++


A discrete-time system, as denoted in the figure, is a mathematical operator or mapping that transforms one signal, the input $x[n]$, into another signal, the output $y[n]$ by means of a fixed set of rules or operations. Discrete-time systems may be classified in terms of the properties that they possess.

<div style="max-width: 500px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/discretetimesystem.svg"
      alt="General discrete-time system."
    />
    <figcaption class="numbered">
      General discrete-time system.
    </figcaption>
  </figure>
</div>

The most important system properties are:

### Memoryless
A  system is memoryless if the output at any time $n=n_0$ depends only on the input at time $n=n_0$. In other words, a system is memoryless if, for any $n_0$, we are able to determine the output value $y[n_0]$ given only the input value $x[n_0]$.

### Causality
A system property that is important for real-time applications is causality, which implies that for any index $n_0$, the response of the system at time index $n_0$ depends only on the input up to time  index $n=n_0$. Thus, for a causal system, changes in the output cannot precede changes in the input.

### Invertibility
A system property that is important in applications such as channel equalization and de-convolution is invertibility. A system is said to be invertible if the input of the system uniquely can be determined from the output. In order for a system to be invertible, it is necessary for distinct inputs to produce distinct outputs.

### Additive
An additive system is one for which the response to a sum of inputs is equal to the sum of the outputs individually.

### Homogeneous
A system is homogeneous if scaling the input by a constant $c$ results in a scaling of the output by the same amount of $c$.

### Stability
In most practical cases it is important for a system to have a response, $y[n]$, that is bounded in amplitude whenever the input is bounded. A system with this property is said to be stable in the Bounded Input Bounded Output (BIBO) sense.

### Linearity
A system that is both additive and homogeneous is said to be linear.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/linear.svg"
      alt="A system is linear if both system configurations are the same."
    />
    <figcaption class="numbered">
      A system is linear if both system configurations are the same.
    </figcaption>
  </figure>
</div>
Referring to Fig. 2, assume that an input $x[n]$ which is applied to a discrete-time system, results in an output $y[n]$. Thus $x_1[n]$ results in $y_1[n]$ and $x_2[n]$ in $y_2[n]$.
On the one hand, we can first apply separately $x_1[n]$ and $x_2[n]$ to the same system and then weight and combine both output into a new output: $w[n] = \alpha y_1[n] + \beta y_2[n]$.
On the other hand, we can first weight, with the same parameters $\alpha$ and $\beta$, and combine both inputs into a new input $x[n]= \alpha x_1[n] + \beta x_2[n]$.
When applying this new input $x[n]$ to the same system it results in an output $y[n]$. A system is linear if both outputs $w[n]$ and $y[n]$ are the same.

### Time-Invariance
If a system has the property that a shift (a delay) of the input by $n_0$ samples results in a shift of the output by the same amount of $n_0$ samples, the system is said to by time-invariant.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/timeinv.svg"
      alt="A system is time invariant if both systems configurations are the same."
    />
    <figcaption class="numbered">
      A system is time invariant if both systems configurations are the same.
    </figcaption>
  </figure>
</div>
Referring to Fig. 3, let $y[n]$ be the response of a discrete-time system to an arbitrary input signal $x[n]$. The system is said to be time-invariant if, for any delay of $n_0$ samples, the response to $x[n-n_0]$ is $y[n-n_0]$. In effect a system is time invariant if its properties or characteristics do not change with time.

### Linear Time Invariance
A system that is both linear and time-invariant is referred to as a Linear Time Invariant system, abbreviated as LTI.
Both properties, Linearity and Time Invariance, of an LTI system are important to understand how to simplify the mathematical analysis to obtain a greater insight and understanding of system behavior.

<div class="example">
<h4> Example </h4>
<hr>
  Show that the system $y[n]= ( x[n])^2$ is non-linear.
<button class="collapsible">Show solution</button>
<div class="content">
  $$
  y[n] = \left ( x[n] \right )^2 =
  \left ( \alpha x_1[n] + \beta x_2[n] \right )^2 = \alpha ^2 x_1^2[n] + 2 \alpha \beta x_1[n] x_2[n] + \beta ^2 x_2^2[n]
  $$
  Referring to the right-hand side of Fig. 2 we obtain:
  $$
  w[n] = \alpha y_1[n] + \beta y_2[n] = \alpha x_1^2[n] + \beta x_2^2[n]
  $$
  Sine $w[n] \neq y[n]$ it follows that the system $y[n]= ( x[n])^2$ is non-linear.
</div>
</div>

<div class="example">
<h4> Example </h4>
<hr>
  Show that the system $y[n]= ( x[n])^2$ is Time Invariant.
<button class="collapsible">Show solution</button>
<div class="content">
  From the upper part of Fig. 3 it follows that
  $w[n] = x^2[n-n_0]$. From the lower part of the same Figure it follows:
  $$
  y[n] = x^2[n] \hspace{3mm} \Rightarrow \hspace{3mm} y[n-n_0] = x^2[n-n_0]
  $$
  The system $y[n]= ( x[n])^2$ is Time Invariant since $w[n]=y[n-n_0]$.
</div>
</div>
