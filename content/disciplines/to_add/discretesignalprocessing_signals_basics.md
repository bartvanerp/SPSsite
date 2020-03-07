+++
title = "Elementary signals"

# date = {{ .Date }}
lastmod = 2019-10-07

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Elementary signals"
  weight = 32
  parent = "Discrete-time signals"


+++


## The (Dirac) delta pulse
The Dirac delta pulse is the most elementary signal in the discrete-time domain. It namely represents a single sample. The Dirac delta pulse is defined as
$$
\boxed{
\text{Dirac delta pulse:} \qquad
\delta[n] = \begin{cases}
1 & n=0 \newline
0 & \text{otherwise}
\end{cases}
}
$$

<br></br>

## The unit step function

Another important basic signal is the discrete-time unit step function, which is defined as
$$
\boxed{
\text{Unit step function: } \qquad
u[n] = \begin{cases}
1 & n \geq 0 \newline
0 & \text{otherwise}
\end{cases}
}
$$

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/signals/basic/basicsignals.svg"
      alt="The unit delta pulse $\delta[n]$ and unit step function $u[n]$."
    />
    <figcaption class="numbered">
      The unit delta pulse $\delta[n]$ and unit step function $u[n]$.
    </figcaption>
  </figure>
</div>


A plot of these two basic signals, within the range $-3 \leq n \leq 3$, is depicted in Fig. 1.

<div class="example">
<h4> Example </h4>
<hr>
Make a plot, in the range $-3 \leq n \leq 3$, of the following signals:
$x_1[n]= \delta[n-2]$,   $x_2[n]= \delta[n+2]$  and  $x_3[n]= u[-n+1]$.
<button class="collapsible">Show solution</button>
<div class="content">
By using the definition of the Dirac delta pulse we can find the integer index of the unit delta pulse of the signals $x_1[n]$ and $x_2[n]$ as follows:
$$
\begin{eqnarray}
x_1[n]= \delta[n-2] & = &
\left \{
\begin{array}{cl}
1 & n-2=0 \mbox{ } \Rightarrow \text{ } n=2\\
0 & \text{elsewhere}
\end{array}
\right . \\
x_2[n]= \delta[n+2] & = &
\left \{
\begin{array}{cl}
1 & n+2=0 \mbox{ } \Rightarrow \text{ } n=-2\\
0 & \text{elsewhere}
\end{array}
\right .
\end{eqnarray}
$$
In a similar way by using the definition of the unit step function we obtain:
$$
x_3[n]=u[-n+1] = \left \{
\begin{array}{cl}
1 & -n +1\geq 0 \text{ } \Rightarrow \mbox{ } n \leq 1 \\
0 & \mbox{elsewhere}
\end{array}
\right .
$$
The figure below shows a plot of these signals.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/signals/basic/examplebasicsignals.svg"
      alt="Example of discrete-time elementary signals."
    />
    <figcaption>
      Example of discrete-time elementary signals.
    </figcaption>
  </figure>
</div>
</div>
</div>
