+++
title = "Real signal as sum of phasors"

# date = {{ .Date }}
lastmod = 2020-03-28

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "Real signal as sum of phasors"
  weight = 1
  parent = "Transforms I: Spectrum of sinusoidal signals"

+++

Let us start with a general description of a signal $x(t)$, which consists of a DC component, with value $A_0$, and a sum of $N$ sinusoidal components, each with a different frequency $f_k$, amplitude $A_k$ and phase $\phi_k$, as

$$
x(t) = A_0 + \sum\_{k=1}^{N} A_k\cos \left( 2\pi  f_k t+ \phi_k \right).
$$

Now by using the <a href="../../../disciplines/mathematicalbackground/mathematicalbackground_complex_euler">Euler equations</a> we can write this equation as the following sum of
rotating <a href="../../../disciplines/mathematicalbackground/mathematicalbackground_complex_phasors">phasors</a>:

$$
\begin{split}
x(t) &= A_0 + \sum\_{k=1}^N \bigg\\{ \left(\frac{A_k}{2}e^{j\phi_k}\right)e^{j2\pi f_k t} + \left(\frac{A_k}{2}e^{-j\phi_k}\right)e^{-j2\pi f_k t}\bigg\\} \newline
&= X_0 + \sum\_{k=1}^N \bigg\\{ \frac{X_k}{2}e^{j2\pi f_k t} + \frac{X_k^\*}{2}e^{-j2\pi f_k t} \bigg\\},
\end{split}
$$

where $X_0 = A_0$ and $X_k = A_ke^{j\phi_k}$. From this description we can derive the following general property:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>For real signals the values of the complex weights of the phasors with negative frequencies are the complex conjugated versions of the complex weights of the phasors with positive frequencies.</i></div>
