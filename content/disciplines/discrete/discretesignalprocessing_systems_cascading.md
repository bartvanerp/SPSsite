+++
title = "Cascading systems"

# date = {{ .Date }}
lastmod = 2020-04-04

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Cascading systems"
  weight = 5
  parent = "Discrete-time systems"
+++


The commutative and associative properties of an LTI system results into the following so called cascade equivalences, which imply that there are different representations of a cascade of LTI systems. Referring to Fig. 1 this can be shown as follows:
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/cascadeequiv.svg"
      alt="Cascade equivalences."
    />
    <figcaption class="numbered">
      Cascade equivalences.
    </figcaption>
  </figure>
</div>
The upper left hand figure of Fig. 1 shows the cascading of two LTI systems, one with impulse response $h_1[n]$ and the other one with impulse response $h_2[n]$. When applying a delta pulse ${\color{red}{\delta[n]}}$ to the first LTI system, the output equals the impulse response ${\color{red}{h_1[n]}}$. When applying this sequence to the second LTI system, the result is the convolution sum result ${\color{red}{h_1[n] \star h_2[n]}}$.

<p></p>
The lower left hand figure shows one LTI system with impulse response $h[n] = h_1[n] \star h_2[n]$. When applying a delta pulse ${\color{red}{\delta[n]}}$ to this system the result is the same as above.

> The cascading of two LTI systems, one with impulse response $h_1[n]$ and the other one with impulse response $h_2[n]$, can be   combined to one LTI system with impulse response $h[n]=h_1[n] \star h_2[n]$.}

Finally it follows from the commutative property of the convolution sum operator that:
$$
h[n] =h_1[n] \star h_2[n] = h_2[n] \star h_1[n]
$$
which is shown in the lower right part of Fig. 1. This combined impulse response can be split again into the cascading of two LTI systems, as shown in the upper right figure. In this last step however the LTI systems with impulse response $h_1[n]$ and $h_2[n]$ have interchanged from order.

> The order of two LTI systems, one with impulse response $h_1[n]$ and the other one with $h_2[n]$, can be interchanged.


<div class="example">
<h4> Example </h4>
<hr>
  Given the cascading of two LTI systems as depicted in the following figure:
  <div style="max-width: 800px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/systems/examplecascade.svg"
        alt="Cascade equivalences."
      />
    </figure>
  </div>
  Give an expression for the impulse responses $h_1[n]$ and $h_2[n]$ of both systems and evaluate the impulse response $h[n]$ of the combined LTI system. Give also a realization scheme of this combined system.
<button class="collapsible">Show proof</button>
<div class="content">
  From the figure it follows that the impulse response are as follows:
  $$
  h_1[n] = \left \{
  \begin{array}{ll}
  1 & 0 \leq n \leq 2 \\
  0 & \mbox{elsewhere}
  \end{array}
  \right .
  \hspace{5mm}
  h_2[n] = \left \{
  \begin{array}{ll}
  1 & 0 \leq n \leq 2 \\
  0 & \text{elsewhere}
  \end{array}
  \right .
  $$
  The combined impulse response can be found as follows:
  \begin{eqnarray*}
  h[n] &=& h_1[n] \star h_2[n] \\
  &=& \left ( \delta[n] + \delta[n-1] + \delta[n-3] \right ) \star
  \left ( \delta[n] + \delta[n-1] + \delta[n-3] \right ) \\
  &=& \delta[n] + 2 \delta[n-1] + 3\delta[n-2]+ 2 \delta[n-3] + \delta[n-4]
  \end{eqnarray*}
  A realization scheme of this combined LTI system is depicted in the following figure.
  <div style="max-width: 800px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/systems/solutioncascade.svg"
        alt="Cascade equivalences."
      />
    </figure>
  </div>
</div>
</div>
