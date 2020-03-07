+++
title = "Elementary signals"

# date = {{ .Date }}
lastmod = 2020-03-07

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Elementary signals"
  weight = 2
  parent = "Discrete-time signals"


+++

Although most information-bearing signals of practical interest are complicated functions of time, there are some fundamental discrete-time signals that are frequently used in the representation and description of more complicated signals.
The first fundamental signal of interest is the discrete-time delta pulse:
$$
\delta[n] =
\begin{cases}
1 & n=0 \newline
0 & \text{elsewhere}
\end{cases}
$$
which is represented at the left hand side of Fig. 1.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/signals/fundamentalsignals.svg"
      alt="Some fundamental signals: Delta pulse $\delta[n]$, Unit step function $u[n]$ and exponential decaying function $x[n]=(-0.8)^n \cdot u[n]$."
    />
    <figcaption class=numbered>
      Some fundamental signals: Delta pulse $\delta[n]$, Unit step function $u[n]$ and exponential decaying function $x[n]=(-0.8)^n \cdot u[n]$.
    </figcaption>
  </figure>
</div>

The discrete-time delta pulse plays the same role in discrete-time signal processing as the continuous-time delta pulse $\delta(t)$ plays in continuous-time signal processing. However in contrast to the discrete-time delta pulse $\delta[n]$, the continuous-time delta pulse $\delta(t)$ is a mathematical defined signal which cannot be realized in practice: Its amplitude is infinite while its width is zero.

The second fundamental signal of interest is the unit step:
$$
u[n]=
\begin{cases}
1 & n \geq 0 \newline
0 & \text{elsewhere}
\end{cases}
$$
which is represented in the middle of Fig. 1.
From this definition of $u[n]$ it follows that the delta pulse $\delta[n]$ may also be written as the difference of two unit step functions while the unit step function itself can also be described as an infinite sum of delta pulses as denoted in the following equations:
$$
\delta[n]=u[n]-u[n-1] \hspace{3mm} \text{ and } \hspace{3mm} u[n]= \sum_{k=0}^{\infty} \delta[n-k]
$$
Another fundamental signal is an exponential decaying function
$$
x[n]= a^n \cdot u[n] \hspace{3mm} \text{ with } \hspace{3mm} |a| < 1
$$
in which the parameter $a$ is a real or complex number from which the absolute value is smaller than one.  An example is represented at the right hand side of Fig. 1.

Finally the complex exponential function
$$
x[n]= e^{jn \omega_0} = \cos (n \omega_0) + j \sin (n \omega_0)
$$
is also a fundamental signal of interest. It represents a discrete-time phasor from which the real and imaginary part behave as cosine and sine respectively.
