+++
title = "Absolute and relative frequency"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Absolute and relative frequency"
  weight = 22
  parent = "Sampling and reconstruction"

+++


When sampling the general signal
$$ x(t) = A \cos (\omega \cdot t + \phi) = A \cos( 2 \pi f \cdot t + \phi) $$
at a sampling frequency $f_s=1/T_s$ we obtain
$$ x[n] = x(t)|\_{t = n \cdot T_s}= A \cos (\omega \cdot n \cdot T_s + \phi) = A \cos\left( 2 \pi f \cdot n \cdot \frac{1}{f_s}\right), \qquad - \infty < n < \infty $$
which can be rewritten as
$$ x[n] = A \cos (2 \pi \frac{f}{f_s} n + \phi)= A \cos (\theta n + \phi). $$

In this equation we used the relative frequency symbol $\theta$, which is a dimensionless quantity [-].
Thus the relation between relative and absolute frequency is
$$ \boxed{\theta = \omega \cdot T_s = 2 \pi \frac{f}{f_s}} $$
and the frequency variables have the following dimensions:

<table style="width:100%">
  <tr>
    <th>Frequency</th>
    <th>Symbol</th>
    <th>Unit</th>
  </tr>
  <tr>
    <td>Absolute frequency</td>
    <td>$f$</td>
    <td>[Hz]</td>
  </tr>
  <tr>
    <td>Absolute radial frequency</td>
    <td>$\omega$</td>
    <td>[rad/sec]</td>
  </tr>
  <tr>
    <td>Relative frequency</td>
    <td>$\theta$</td>
    <td>[-]</td>
  </tr>
</table>

For a continuous-time sinusoidal signal $x(t)$ we have seen before that a representation of the spectral content of such a signal can be found easily by using <a href="../../mathematicalbackground/mathematicalbackground_complex_euler">Euler</a>, that is by rewriting $x(t)$ in terms of <a href="../../mathematicalbackground/mathematicalbackground_complex_phasors">phasors</a>. The weights of these <a href="../../mathematicalbackground/mathematicalbackground_complex_phasors">phasors</a> represent the spectral content of $x(t)$.

In a similar way we can use <a href="../../mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> to find a representation of the <a href="../../continuous/continuoussignalprocessing_transforms_fs/#spectrum">spectral content</a> of a discrete-time sinusoidal signal $x[n]$. Such a description is only valid if the sequence of samples $x[n]$ is periodic. This is true if there exists an integer number $N$ for which $x[n]=x[n+N]$, leading to:
$A \cos \left(2 \pi \frac{f}{f_s} n + \phi\right) = A \cos \left(2 \pi \frac{f}{f_s} (n+N) + \phi\right)$
or equivalently:
$2 \pi \frac{f}{f_s} \cdot N = \lambda \cdot 2 \pi \mbox{ with integer } \lambda$, which is similar to  $\frac{f}{f_s} = \frac{\lambda}{N}$, or in other words the fraction $\frac{f}{f_s}$ must be a rational number.

The <a href="../../continuous/continuoussignalprocessing_transforms_fs/#spectrum">spectral content</a> of $x[n]$ can be determined by rewriting $x[n]$ as
$$ x[n] = \left ( \frac{A}{2} e^{j\phi} \right ) \cdot e^{j\theta n} + \left ( \frac{A}{2} e^{-j\phi} \right ) \cdot e^{-j\theta n} $$
From this equation it follows that the <a href="../../continuous/continuoussignalprocessing_transforms_fs/#spectrum">spectral representation</a> of the discrete-time sinusoidal signal $x[n]$ contains two frequency components: One with the complex value $\left( \frac{A}{2} e^{j\phi} \right)$ for the relative frequency $+ \theta$ and another one with the complex value $\left( \frac{A}{2} e^{-j\phi} \right)$ for relative frequency $ - \theta$.

<div class="example">
<h4> Example </h4>
<hr>

In this example we convert the 200 [Hz] continuous-time signal $x(t) = \cos (400 \pi t)$ to the discrete-time domain signal samples $x[n]$ with an ideal C-to-D convertor which runs at a sample rate of $f_s=1000$ [samples/sec].
<br>
Make a plot of the frequency content of both the continuous-time signal $x(t)$ and the discrete-time signal samples $x[n]$.

<button class="collapsible">Show solution</button>
<div class="content">
  By using the <a href="../../mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> equations we can write the input signal of the C-to-D convertor as
  $$ x(t) = \cos (400 \pi t) = \frac{1}{2} e^{j2 \pi 200 t} + \frac{1}{2} e^{-j2 \pi 200 t}. $$
  The absolute frequency plot of $x(t)$ is depicted in the upper part of the figure below.
  <br>
  By using $\theta = 2 \pi \frac{f}{f_s}$, the output signal samples of the C-to-D convertor can mathematically be described as:
  $$ x[n] = \cos (0.4 \pi n) = \frac{1}{2} e^{j0.4 \pi n} + \frac{1}{2} e^{-j0.4 \pi n} $$
  In a similar way as with the absolute frequency plot, we can derive the relative frequency plot form this <a href="../../mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> equation, which results in the plot as depicted in the lower part of the figure below.

  <div style="max-width: 600px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/sampling/absolute_relative_frequency.svg"
        alt="Frequency plot containing the absolute and relative frequencies of a 200 [Hz] sinusoid sampled at $f_s=1000$ [samples/sec]."
      />
      <figcaption class="numbered">
        Frequency plot containing the absolute and relative frequencies of a 200 [Hz] sinusoid sampled at $f_s=1000$ [samples/sec].
      </figcaption>
    </figure>
  </div>

</div>
</div>
