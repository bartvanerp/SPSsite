+++
title = "Symmetry"

# date = {{ .Date }}
lastmod = 2020-03-07

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Symmetry"
  weight = 5
  parent = "Discrete-time signals"


+++

A discrete-time signal will often possess some form of symmetry that may be exploited in solving problems. Two symmetries of interest are as follows:  A real-valued signal is said to be even if, for all indices $n$, $x[n]=x[-n]$, whereas a signal is said to be odd if, for all indices $n$, $x[n]=-x[-n]$. For complex signals the symmetries of interest are slightly different namely a complex signal is conjugate symmetric if, for all indices $n$ $x[n]=x^\ast[-n]$  and a signal is said to be conjugate antisymmetric if, for all indices $n$ $x[n]=-x^\ast[-n]$.
Furthermore, any signal $x[n]$ may be decomposed into a sum of its even part, denoted by $x_e[n]$, and its odd part, denoted by $x_o[n]$.
The even part can be constructed as $x_e[n] = \frac{1}{2} (x[n] + x[-n])$, while the odd part can be constructed as $x_o[n] = \frac{1}{2} (x[n]-x[-n])$.

The following equations summarize all these symmetries:
\begin{eqnarray*}
\textit{Even } \color{blue}{\textit{Conjugate-symmetric}} &:& x[n]=x[-n] \hspace{3mm} \color{blue}{x[n]=x^\ast[-n]}\newline
\textit{Odd } \color{blue}{\textit{Conjugate-antisymmetric}} &:& x[n]=-x[-n] \hspace{3mm} \color{blue}{x[n]=-x^\ast[-n]} \newline
\textit{General: } \hspace{3mm} x[n]&=&x_e[n]+x_o[n] \newline
\text{with } \hspace{3mm} x_e[n]&=&\frac{1}{2} \left ( x[n] + x[-n] \right ) \newline
\text{and } \hspace{3mm} x_o[n]&=&\frac{1}{2} \left ( x[n] - x[-n] \right )
\end{eqnarray*}

<div class="example">
<h4> Example </h4>
<hr>
If $x[n]=0$ for $n<0$, derive an expression for $x[n]$ in terms of its even part, $x_e[n]=(0.8)^{|n|} u[n]$.
<button class="collapsible">Show solution</button>
<div class="content">
Note that for $x[n]=0$ for $n<0$ we have $x_e[n] = \frac{1}{2} x[n]$ for $n>0$ and $x_e[n] = x[n]$ for $n=0$. From this it follows that in this case we can write $x[n]$ in terms of its even part as follows:
$$
x[n] =
\begin{cases}
x_e[n] & \mbox{for } n=0 \\
2 x_e[n] & \mbox{for } n>0.
\end{cases}
$$
With $x_e[n]=(0.8)^{|n|} u[n]$ this results in the following:
$$
x[n] = \delta[n] + 2 (0.8)^{n} u[n-1].
$$
<i>Note:</i> If only the odd part is given for this case, it is not possible to recover $x[n]$.
</div>
</div>

<div class="example">
<h4> Example </h4>
<hr>
Is the complex signal $x[n]= j e^{jn \frac{\pi}{4}}$ conjugate-symmetric or
-antisymmetric?
<button class="collapsible">Show solution</button>
<div class="content">
$$
x_e[n] = \frac{1}{2} ( x[n] + x^\ast[-n] ) = \frac{1}{2} (
j e^{jn \frac{\pi}{4}} - j e^{jn \frac{\pi}{4}}) = 0
$$
Thus, this signal $x[n]$ is conjugate-antisymmetric.
</div>
</div>
