+++
title = "Impulse response"

# date = {{ .Date }}
lastmod = 2020-04-04

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Impulse response [⯈]"
  weight = 3
  parent = "Discrete-time systems"
+++

In the previous section we have seen that the DE describes the input- output- relation of a discrete-time system. In this section we will introduce yet another way to describe a discrete-time system, namely by its impulse response, denoted by ${\color{red}{h[n]}}$.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/impulseresponse.svg"
      alt="Impulse response ${\color{red}{h[n]}}$ of a discrete-time system."
    />
    <figcaption class="numbered">
      Impulse response ${\color{red}{h[n]}}$ of a discrete-time system.
    </figcaption>
  </figure>
</div>
The impulse response of a discrete-time system is defined as the response of a discrete-time system when the input is a delta pulse, thus $x[n]={\color{red}{\delta[n]}}$. This is depicted in Fig. 1.

For an LTI system BIBO stability and causality are easily checked by its impulse response $h[n]$ as follows:
\begin{eqnarray*}
\textbf{BIBO stablility} & : & \sum_{n=-\infty}^{\infty} |h[n]| < \infty \newline
\textbf{Causalilty} & : & h[n]=0 \text{ for } n<0
\end{eqnarray*}
Finally, in general we can distinguish the following two types of impulse responses:

<br></br>
## Finite Impulse Response (FIR) case [⯈]

<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/20j0M8b_pu4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>
In case all feedback coefficients are zero, the LTI system represents a Finite Impulse Response Filter, abbreviated as FIR.  The Difference Equation is a finite sum of weighted and delayed input samples.  As a result of the definition, by substituting $x[n]=\delta[n]$ we obtain an expression for the impulse response $h[n]$, which has finite length. Moreover the $M$ impulse response values $h[0]$ until $h[M-1]$ are the same as the $M$ filter coefficients $b_0$ until $b_{M-1}$ for the FIR case.
<div class="example">
<h4> Example </h4>
<hr>
  Derive the impulse response of the LTI system which is described by the following Difference Equation:
  $$
  y[n]=\frac{1}{2} x[n]+ x[n-1]-\frac{3}{4} x[n-2]-\frac{1}{4} x[n-3].
  $$
  Make a plot of this impulse response and draw the signal flow diagram.
<button class="collapsible">Show solution</button>
<div class="content">
  The impulse response can be found by substituting $x[n]$ with $\delta[n]$
  in the Difference Equation:
  $$
  h[n]=\frac{1}{2} \delta[n] + \delta[n-1] - \frac{3}{4} \delta[n-2] - \frac{1}{4} \delta[n-3]
  $$
  The impulse response and realization scheme are given in the following figure:
  <div style="max-width: 800px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/systems/exampleFIR.svg"
        alt="Solution to example."
      />
    </figure>
  </div>
</div>
</div>


<br></br>
## Infinite Impulse Response (IIR) case
In case at least one of the feedback coefficients is not equal to zero, the impulse response can have Infinite length. This can be shown by the following simple example. Consider an LTI system that can be described by the following Difference Equation:
$$
y[n]=x[n]+ a y[n-1] \hspace{3mm} |a| < 1 \text{ and } y[n]=0 \text{ for } n<0.
$$
This system has one feedback coefficient, denoted by the number $a$, which is assumed to have an absolute value smaller than one. Furthermore we assume the output $y[n]$ is equal to zero for all indices $n<0$.
A realization scheme is depicted at the left hand side of Fig. 2.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/expdecay.svg"
      alt="Signal flow diagram and impulse response of a simple IIR filter."
    />
    <figcaption class="numbered">
      Signal flow diagram and impulse response of a simple IIR filter.
    </figcaption>
  </figure>
</div>
We can rewrite the Difference Equation by evaluating it step by step as follows:  For $n=0$  the output $y[0]=x[0]$ because $y[n]=0$ for all indices smaller then zero.  For $n=1$  we can substitute the previous output value $y[0]=x[0]$ and $y[1]$ is equal to a sum of the two previous input signal sample $x[1] + a \cdot x[0]$.  Using this result for $n=2$  and writing it out  results in a sum of three previous input signal samples  $x[2] + a \cdot x[1] + a^2 \cdot x[0]$. When following this procedure  we can rewrite the Difference Equation as a weighted sum of delayed input signal samples as denoted in the following equation:
\begin{eqnarray*}
y[0] &=& x[0] + a y[-1] = x[0] \\
y[1] &=& x[1] + a y[0] = x[1] + a x[0] \\
y[2] &=& x[2] + a y[1] = x[2] +a \left ( x[1] + a x[0] \right ) =
\sum_{k=0}^{2} a^k x[2-k] \\
\vdots & \vdots & \vdots \\
y[n] &=& \sum_{k=0}^{n} a^k x[n-k]
\end{eqnarray*}
By substituting $x[n]=\delta[n]$ we obtain the following expression for the impulse response $h[n]$:
$$
h[n] = \sum_{k=0}^{n} a^k \delta[n-k] = a^n u[n]
$$
The upper bound of the summation is depending on the running index $n$. In other words the length of the impulse response becomes infinite long.  Another way to describe this impulse response $h[n]$ is with the unit step function $u[n]$.  The right hand side of Fig. 2 shows the resulting impulse response of this simple LTI system with one feedback loop for $a=-0.8$, which is an infinite long exponential decaying function.
