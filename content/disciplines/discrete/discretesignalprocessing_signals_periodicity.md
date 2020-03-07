+++
title = "Periodicity"

# date = {{ .Date }}
lastmod = 2020-03-07

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Periodicity"
  weight = 4
  parent = "Discrete-time signals"


+++

A discrete-time signal may always be classified as either periodic or aperiodic. A signal $x[n]$ is said to be periodic if, for some positive real integer $N$ the following relation holds:
$$
x[n]=x[n+N].
$$
This is equivalent to saying that the sequence repeats itself every $N$ samples. If a signal is periodic with period $N$, it is also periodic with $2N$, period $3N$, and all other integer multiples of $N$. The fundamental period, which will be denoted by $N$, is the smallest positive integer for which $x[n]=x[n+N]$. If this equation is not satisfied for any integer $N$, the signal $x[n]$ is said to be an aperiodic signal.

Examples of periodic signals are:
$x[n]=\sin(n\pi/4)$ and $x[n] = e^{jn \frac{\pi}{8}}$. The first signal has a fundamental period of $N=8$ samples and the second signal has a period of $N=16$ samples.
Examples of aperiodic signals are: $x[n]=\sin(n)$ and $x[n]=a^n \cdot u[n]$
since there is no integer $N$ for which the signal repeats.

<div class="example">
<h4> Example </h4>
<hr>
Determine for which value(s) of the relative frequency $\theta$ the signal $x[n]= A \sin(n \theta + \phi)$ is periodic and calculate the period(s).
<button class="collapsible">Show solution</button>
<div class="content">
The function $x[n]$ is periodic for $\theta = 2 \pi K/N$, in which both $K$ and $N$ are
some positive real integers. Thus an equation for the period of $x[n]$ is given by
$N = 2 \pi K_{min}/\theta$, in which $K_{min}$ represents the smallest possible value of $K$. For example for $\theta = 0.23 \pi$ we have $K_{min}=23$ and $N=200$ while for $\theta = 0.24 \pi$ we have $K_{min}=3$ and $N=25$.
</div>
</div>

<div class="example">
<h4> Example </h4>
<hr>
Determine whether or not the complex signal $x[n] = e^{jn}$ is periodic or not.
<button class="collapsible">Show solution</button>
<div class="content">
Both real and imaginary parts of the signal $x[n] = e^{jn} = \cos (n) + j \sin (n)$ are aperiodic, since there is no integer $N$ for which $\cos(n)=\cos(n+N)$ and/or $\sin(n)=\sin(n+N)$.
</div>
</div>
