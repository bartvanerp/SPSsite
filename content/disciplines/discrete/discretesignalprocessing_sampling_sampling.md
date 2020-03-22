+++
title = "Sampling of sinusoidal signals"

# date = {{ .Date }}
lastmod = 2019-08-22

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Sampling of sinusoidal signals"
  weight = 21
  parent = "Basics of sampling and reconstruction"

+++

## Sampling of sinusoidal signals

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

<br></br>

## Absolute and relative frequency

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

For a continuous-time sinusoidal signal $x(t)$ we have seen before that a representation of the spectral content of such a signal can be found easily by using <a href="../../../disciplines/mathematicalbackground/mathematicalbackground_complex_euler">Euler</a>, that is by rewriting $x(t)$ in terms of <a href="../../../disciplines/mathematicalbackground/mathematicalbackground_complex_phasors">phasors</a>. The weights of these <a href="../../../disciplines/mathematicalbackground/mathematicalbackground_complex_phasors">phasors</a> represent the spectral content of $x(t)$.

In a similar way we can use <a href="../../../disciplines/mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> to find a representation of the <a href="../../../disciplines/continuous/continuoussignalprocessing_transforms_spectrum">spectral content</a> of a discrete-time sinusoidal signal $x[n]$. Such a description is only valid if the sequence of samples $x[n]$ is periodic. This is true if there exists an integer number $N$ for which $x[n]=x[n+N]$, leading to:
$A \cos \left(2 \pi \frac{f}{f_s} n + \phi\right) = A \cos \left(2 \pi \frac{f}{f_s} (n+N) + \phi\right)$
or equivalently:
$2 \pi \frac{f}{f_s} \cdot N = \lambda \cdot 2 \pi \mbox{ with integer } \lambda$, which is similar to  $\frac{f}{f_s} = \frac{\lambda}{N}$, or in other words the fraction $\frac{f}{f_s}$ must be a rational number.

The <a href="../../../disciplines/continuous/continuoussignalprocessing_transforms_spectrum">spectral content</a> of $x[n]$ can be determined by rewriting $x[n]$ as
$$ x[n] = \left ( \frac{A}{2} e^{j\phi} \right ) \cdot e^{j\theta n} + \left ( \frac{A}{2} e^{-j\phi} \right ) \cdot e^{-j\theta n} $$
From this equation it follows that the <a href="../../../disciplines/continuous/continuoussignalprocessing_transforms_spectrum">spectral representation</a> of the discrete-time sinusoidal signal $x[n]$ contains two frequency components: One with the complex value $\left( \frac{A}{2} e^{j\phi} \right)$ for the relative frequency $+ \theta$ and another one with the complex value $\left( \frac{A}{2} e^{-j\phi} \right)$ for relative frequency $ - \theta$.

<div class="example">
<h4> Example </h4>
<hr>
In this example we convert the 200 [Hz] continuous-time signal $x(t) = \cos (400 \pi t)$ to the discrete-time domain signal samples $x[n]$ with an ideal C-to-D convertor which runs at a sample rate of $f_s=1000$ [samples/sec].
<br>
Make a plot of the frequency content of both the continuous-time signal $x(t)$ and the discrete-time signal samples $x[n]$.
<button class="collapsible">Show solution</button>
<div class="content">
  By using the <a href="../../../disciplines/mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> equations we can write the input signal of the C-to-D convertor as
  $$ x(t) = \cos (400 \pi t) = \frac{1}{2} e^{j2 \pi 200 t} + \frac{1}{2} e^{-j2 \pi 200 t}. $$
  The absolute frequency plot of $x(t)$ is depicted in the upper part of the figure below.
  <br>
  By using $\theta = 2 \pi \frac{f}{f_s}$, the output signal samples of the C-to-D convertor can mathematically be described as:
  $$ x[n] = \cos (0.4 \pi n) = \frac{1}{2} e^{j0.4 \pi n} + \frac{1}{2} e^{-j0.4 \pi n} $$
  In a similar way as with the absolute frequency plot, we can derive the relative frequency plot form this <a href="../../../disciplines/mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> equation, which results in the plot as depicted in the lower part of the figure below.
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

<br></br>

## Uniqueness issue

In this section we will show that the C-to-D conversion will lead to an uniqueness issue in the discrete-time domain.

### Uniqueness issue viewed in relative frequency domain
In this subsection we will show there is no unique spectral representation of the discrete-time signal samples $x[n]$.
In order to show this let us start with the mathematical description of a sinusoidal signal as
$$ x[n] = \left ( \frac{A}{2} e^{j\phi} \right ) \cdot e^{j\theta n} + \left ( \frac{A}{2} e^{-j\phi} \right ) \cdot e^{-j\theta n}. $$
By using the fact that the number $1$ can be written as a complex exponent as
$$ 1 = 1^n = \left( e^{j2 \pi} \right)^n = \left( e^{-j2 \pi} \right)^n = e^{\pm j2 \pi n} \qquad \mbox{with integer } n ,$$
we can change the mathematical representation of the sequence of samples $x[n]$ as
$$\begin{eqnarray*}
x[n] &=& \left( \frac{A}{2} e^{j\phi} \right) \cdot e^{j\theta n} \cdot 1 + \left(\frac{A}{2} e^{-j\phi} \right ) \cdot e^{-j\theta n} \cdot 1  \newline
&=& \left( \frac{A}{2} e^{j\phi} \right) \cdot e^{j\theta n} \cdot e^{j2\pi n} + \left( \frac{A}{2} e^{-j\phi} \right) \cdot e^{-j\theta n} \cdot e^{-j2 \pi n} \newline
&=& \left( \frac{A}{2} e^{j\phi} \right) \cdot e^{j(\theta + 2 \pi) n} + \left( \frac{A}{2} e^{-j\phi} \right) \cdot e^{-j(\theta + 2 \pi) n}
\end{eqnarray*}$$
From this equation it follows that the <a href="../../../disciplines/continuous/continuoussignalprocessing_transforms_spectrum">spectral representation</a> of $x[n]$ consists again of the same two bars, but now at the relative frequencies $\theta + 2 \pi$ and $-(\theta + 2 \pi)$.
So we have found two different ways to represent the spectral information of the same sequence of samples $x[n]$. Moreover we can find an infinite amount of different <a href="../../../disciplines/continuous/continuoussignalprocessing_transforms_spectrum">spectral representations</a>, just by adding or subtraction an integer times $2\pi$ to the relative frequency $\theta$. Thus the same relative <a href="../../../disciplines/continuous/continuoussignalprocessing_transforms_spectrum">spectral content</a> is repeated every $2\pi$.

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The spectral representation of a discrete-time signal $x[n]$ is not unique. The relative frequency representation is periodic with period $2\pi$.</i></div>


<div class="example">
<h4> Example </h4>
<hr>
Plot the <a href="../../../disciplines/continuous/continuoussignalprocessing_transforms_spectrum">spectral representation</a> of the sequence of samples which are represented by $x[n]=2 \cos(0.4 \pi n + \frac{\pi}{4})$ in the range $-3 \pi < \theta < 3 \pi$.
<button class="collapsible">Show solution</button>
<div class="content">
By using <a href="../../../disciplines/mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> we can write $x[n]$ as
$$ x[n] = e^{j{\color{red}{(0.4 \pi n + \frac{\pi}{4})}}} + e^{-j{\color{blue}{(0.4 \pi n + \frac{\pi}{4})}}} \mbox{ } \left( = 2 \cos \left( 0.4 \pi n + \frac{\pi}{4}\right) \right).$$
So the spectral plot contains two bars: One at frequency $0.4 \pi$ (in red) and one at $-0.4 \pi$ (in blue) as depicted in the Figure below.
When adding or subtracting $2\pi$ to both frequency components we obtain the following possibilities within the range $-3 \pi < \theta < 3 \pi$:
$0.4 \pi + 2 \pi = 2.4 \pi$
$$
\Rightarrow \mbox{ }
x[n] = e^{j{\color{red}{(2.4 \pi n + \frac{\pi}{4})}}} + e^{-j{\color{blue}{(2.4 \pi n + \frac{\pi}{4})}}} \mbox{ } \left( = 2\cos \left(2.4 \pi n + \frac{\pi}{4} \right) \right)
$$
$0.4 \pi - 2 \pi = - 1.6 \pi$
\begin{eqnarray*}
\Rightarrow \mbox{ }
x[n] &=& e^{j{\color{red}{(-1.6 \pi n + \frac{\pi}{4})}}} + e^{-j{\color{blue}{(-1.6 \pi n + \frac{\pi}{4})}}} \newline
&=& e^{j{\color{blue}{(1.6 \pi n - \frac{\pi}{4})}}} + e^{-j{\color{red}{(1.6 \pi n - \frac{\pi}{4})}}}
\mbox{ } \left( = 2\cos \left(1.6 \pi n - \frac{\pi}{4}\right) \right)
\end{eqnarray*}
Note that for this last case the phase has changed from sign.
All these possibilities are depicted in the Figure below.
From this Figure it follows that the <a href="../../../disciplines/continuous/continuoussignalprocessing_transforms_spectrum">spectral representation</a> of $x[n]$ is indeed repeated every $2\pi$ outside the period $-\pi < \theta < \pi$.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/sampling/uniqueness_frequency.svg"
      alt="Visualization of the uniqueness issue in the frequency domain."
    />
    <figcaption class="numbered">
      Visualization of the uniqueness issue in the frequency domain.
    </figcaption>
  </figure>
</div>
</div>
</div>



### Uniqueness issue viewed in discrete-time domains
In this subsection we will show by an example that different continuous-time signals can convert via an C-to-D convertor into the same sequence of samples.

<div class="example">
<h4> Example </h4>
<hr>
In this example we convert two different continuous-time signals $x_1(t)=\cos (400 \pi t)$ and ${\color{red}{x_2(t)}} = \cos (2400 \pi t)$ with a C-to-D convertor, which runs at a sample rate of $f_s=1000$ [samples/sec], to the discrete-time domain. Calculate the sequence of samples $x_1[n]$ and $x_2[n]$ for two periods and make a plot which shows $x_1(t), {\color{red}{x_2(t)}}$ and the samples of $x_1[n]$ and $x_2[n]$.
<button class="collapsible">Show solution</button>
<div class="content">
The converted signals are as follows:
\begin{eqnarray*}
x_1[n] &=& \cos \left( 400 \pi \cdot \frac{1}{1000} n \right)\newline
 &=& \cos (0.4 \pi n ) = {\color{blue} {\ldots, 1, 0.3, -0.8, -0.8, 0.3, 1, \ldots }}\newline
x_2[n] &=& \cos \left( 2400 \pi \cdot \frac{1}{1000} n \right) \newline
&=& \cos (2.4 \pi n) = {\color{blue}{\ldots, 1, 0.3, -0.8, -0.8, 0.3, 1, \ldots }}
\end{eqnarray*}
Thus the samples which result from the C-to-D conversion of the two different continuous-time signals $x_1(t)$ and ${\color{red}{x_2(t)}}$ result in the same sequence of samples $x_1[n]=x_2[n]=x[n]={\color{blue}{\ldots, 1, 0.3, -0.8, -0.8, 0.3, 1, \ldots }}$.
<br>
The Figure below shows a plot with two periods of the two different continuous-time $x_1(t)$ (in black) and ${\color{red}{x_2(t)}}$ (in red) and the resulting discrete-time signal samples $x[n]={\color{blue}{\ldots, 1, 0.3, -0.8, -0.8, 0.3, 1, \ldots }}$ (in blue).
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/sampling/uniqueness_time.svg"
      alt="Visualization of the uniqueness issue in the time domain."
    />
    <figcaption class="numbered">
      Visualization of the uniqueness issue in the time domain.
    </figcaption>
  </figure>
</div>
</div>
</div>


### The Fundamental Interval (FI)
We have seen that the relative frequency representation of a discrete-time signal is periodic with period $2\pi$. So in general only one interval of width $2\pi$ is of importance. In most cases we will use the interval of relative frequencies $-\pi < \theta \leq \pi$. This interval is called the Fundamental Interval (FI). Furthermore from the definition of the <a href="../../../disciplines/discretesignalprocessing_sampling_sampling/#absolute-and-relative-frequency">relative frequency</a>
 $\theta=2 \pi \frac{f}{f_s}$, the boundaries $\pm \pi$ of relative frequencies of the FI are related to the absolute frequencies $\pm \frac{f_s}{2}$.
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The Fundamental Interval is given for the following frequencies as:</i>
<table style="width:100%">
  <tr>
    <th>Frequency</th>
    <th>Symbol</th>
    <th>Fundamental Interval</th>
  </tr>
  <tr>
    <td>Relative frequency</td>
    <td>$\theta$</td>
    <td>$-\pi < \theta \leq \pi$</td>
  </tr>
  <tr>
    <td>Absolute frequency</td>
    <td>$f$</td>
    <td>$-\frac{f_s}{2} < f \leq \frac{f_s}{2}$</td>
  </tr>
  <tr>
    <td>Absolute radial frequency</td>
    <td>$\omega$</td>
    <td>$-\pi f_s < \omega \leq \pi f_s$</td>
  </tr>
</table>
</div>


<div class="example">
<h4> Example </h4>
<hr>
In this example we convert the continuous-time signal $x(t) = x_1(t) + x_2(t)$, which consists of frequencies 200 [Hz] and 500 [Hz] with
$$
x_1(t)= 4 \cos(400 \pi t + \frac{\pi}{4}) \mbox{  and  } x_2(t)= 2 \sin (1000 \pi t - \frac{\pi}{3}),
$$
to the discrete-time domain samples $x[n]=x_1[n]+x_2[n]$, by an ideal C-to-D convertor which runs at a sample rate of $f_s=600$ [samples/sec]. Give a plot of the <a href="../../../disciplines/continuous/continuoussignalprocessing_transforms_spectrum">frequency representation</a> of the continuous-time signal $x(t)$ and give also a plot of the <a href="../../../disciplines/continuous/continuoussignalprocessing_transforms_spectrum">frequency representation</a> of the discrete-time signal $x[n]$ in the Fundamental Interval (FI).
<button class="collapsible">Show solution</button>
<div class="content">
The spectral components of the continuous-time domain signal $x(t)$ are depicted in the upper part of the Figure below.
This Figure also shows that frequencies smaller than 300 [Hz] map into the FI.
So the result of the C-to-D conversion of $x_1(t)$ is as follows:
$x_1(t)= 4 \cos\left(400 \pi t + \frac{\pi}{4}\right)$ $\Rightarrow$
\begin{eqnarray*}
x_1[n]&=& 4 \cos \left(\frac{2 \pi}{3}n + \frac{\pi}{4}\right) = \left( 2 e^{j\frac{\pi}{4}} \right ) e^{j\frac{2 \pi}{3}n} + \left( 2 e^{-j\frac{\pi}{4}} \right) e^{-j\frac{2 \pi}{3}n}
\end{eqnarray*}
Furthermore the  result of the C-to-D conversion of $x_2(t)$ is as follows:
$x_2(t)= 2 \sin \left(1000 \pi t - \frac{\pi}{3}\right)$ $\Rightarrow$
\begin{eqnarray*}
x_2[n]&=& 2 \sin\left(\frac{5 \pi}{3} n - \frac{\pi}{3} \right) \newline
&=& \left( {\color{red}{\frac{1}{j} e^{-j\frac{\pi}{3}}} }\right) e^{j\frac{5 \pi}{3} n}  + \left( {\color{blue}{\frac{-1}{j} e^{j\frac{\pi}{3}}}} \right) e^{-j\frac{5 \pi}{3} n} \newline
&=& \left( {\color{red}{\frac{1}{j} e^{-j\frac{\pi}{3}}}} \right ) e^{-j\frac{\pi}{3} n}  +
\left( {\color{blue}{\frac{-1}{j} e^{j\frac{\pi}{3}}}} \right) e^{j\frac{\pi}{3} n} \newline
&=& - \left(
\left({\color{blue}{\frac{1}{j} e^{j\frac{\pi}{3}}}} \right) e^{j\frac{\pi}{3} n} +
\left( {\color{red}{\frac{-1}{j} e^{-j\frac{\pi}{3}}}} \right) e^{-j\frac{\pi}{3} n} \right) \newline
&=& - 2 \sin\left(\frac{\pi}{3} n + \frac{\pi}{3} \right)
\end{eqnarray*}
Thus the frequency component of $x_2(t)$ is converted outside the FI into relative frequency $\frac{5 \pi}{3}$. When mapping this component back inside the FI it results in the relative frequency $\frac{\pi}{3}$ and the phase changes from sign.
The lower part of the Figure below shows the spectral components.
The components outside the FI, which are periodic components, are denoted in dashed lines.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/sampling/uniqueness_example.svg"
      alt="Example visualization of a signal that is mapped into the Fundamental Interval."
    />
    <figcaption class="numbered">
      Example visualization of a signal that is mapped into the Fundamental Interval.
    </figcaption>
  </figure>
</div>
</div>
</div>
