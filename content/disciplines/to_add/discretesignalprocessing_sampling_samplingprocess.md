+++
title = "Sampling process of C-to-D converter"

# date = {{ .Date }}
lastmod = 2019-08-22

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Sampling process of C-to-D converter"
  weight = 21
  parent = "Basics of sampling and reconstruction"

+++
### Conceptual video
<iframe width="100%" height="450" src="https://www.youtube.com/embed/Xs8AS-F16P4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


### Sampling
In many practical situations signals are available as a continuous-time (or analog) signal $x(t)$. An example of such a continuous-time signal is the recording of an audio signal with a microphone. Manipulating such an continuous-time signal is, in most cases, done in the discrete-time (or digital) domain. For example equalizing an audio signal can easiest be performed in the discrete-time domain. So it is important to understand the sampling process, which is performed by a Continuous- to Discrete-time (C-to-D) convertor which converts the continuous-time signal $x(t)$ to the discrete-time domain signal samples $x[n]$. The continuous-time character of a signal is indicated by using round brackets $( \cdot )$ around the (continuous) variable $t$, while the discrete-time character of a signal is indicated by using square brackets $[ \cdot ]$ around the (integer) variable $n$.

In order to simplify the mathematical description of the sampling process we will assume the following sinusoidal continuous-time signal:
$$ x(t) = A \cos (\omega \cdot t + \phi) = A \cos( 2 \pi f \cdot t + \phi) $$

In this equation $\omega$ represents the absolute frequency in [rad/sec], or $f$ in [Hz], while $A$ denotes the amplitude and $\phi$, in [rad], the phase of $x(t)$.
The result of the sampling process, by an C-to-D convertor, is a set of numbers, denoted by $x[n]$. In the above case of a sinusoidal signal these numbers $x[n]$ can be obtained by evaluating $x(t)$ at regular time instances $n \cdot T_s$, in which the variable $n$ is an integer and $T_s$ is the inter-sample time, typically denoted in seconds [sec].
The sampling frequency of the C-to-D convertor equals $f_s=1/T_s$, typically denoted in samples per second [samples/sec] or Hertz [Hz]. Thus the relation between the discrete-time signal samples $x[n]$ and the continuous-time signal $x(t)$ can be described as follows:
$$ x[n] = x(t)|\_{t = n \cdot T_s}= A \cos (\omega \cdot n \cdot T_s + \phi) = A \cos\left( 2 \pi f \cdot n \cdot \frac{1}{f_s}\right) \qquad - \infty < n < \infty $$

<div class="example">
<h4> Example </h4>
<hr>

The left hand side of Fig. 1 shows two periods of the continuous-time signal $x(t)=\cos ( 400 \pi t)$. This continuous-time signal is sampled with an ideal C-to-D convertor, which runs at a sampling frequency of $f_s=1000$ [samples/sec]. Evaluate and plot the samples $x[n]$ is the discrete-time domain.

<button class="collapsible">Show solution</button>
<div class="content">
  The samples $x[n]$ can be evaluated as follows:
  $$ x[n] = \cos ( 400 \pi t)\mid_{t=n / f_s} = \cos (0.4 \pi n)= \ldots, \overset{\overset{n=0}{\downarrow}}{1}, 0.3, -0.8, -0.8, 0.3, 1, \ldots $$
as depicted at the right hand side of Fig. 1.

Usually we represent the set of numbers $x[n]$ in a plot as depicted at the right hand side of Fig. 2, where  the horizontal axis denotes the integer index $n$ and the vertical axis represents the sample value $x[n]$.
</div>
</div>

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/sampling/sampling_numbers.svg"
      alt="The output of an C-to-D convertor is a sequence of numbers (samples) $x[n]$."
    />
    <figcaption class="numbered">
      The output of an C-to-D convertor is a sequence of numbers (samples) $x[n]$.
    </figcaption>
  </figure>
</div>

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/sampling/sampling_plot.svg"
      alt="The output of an C-to-D convertor is a sequence of numbers (samples) $x[n]$, which can be represented in a plot."
    />
    <figcaption class="numbered">
      The output of an C-to-D convertor is a sequence of numbers (samples) $x[n]$, which can be represented in a plot.
    </figcaption>
  </figure>
</div>
