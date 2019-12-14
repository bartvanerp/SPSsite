+++
title = "Uniqueness issue"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Uniqueness issue"
  weight = 23
  parent = "Basics of sampling and reconstruction"

+++


In this section we will show that the C-to-D conversion will lead to an uniqueness issue in the discrete-time domain.

## Uniqueness issue viewed in relative frequency domain
In this subsection we will show there is no unique spectral representation of the discrete-time signal samples $x[n]$.
In order to show this let us start with the mathematical description of a sinusoidal signal as
$$ x[n] = \left ( \frac{A}{2} e^{j\phi} \right ) \cdot e^{j\theta n} + \left ( \frac{A}{2} e^{-j\phi} \right ) \cdot e^{-j\theta n}. $$
By using the fact that the number $1$ can be written as a complex exponent as
$$ 1 = 1^n = \left( e^{j2 \pi} \right)^n = \left( e^{-j2 \pi} \right)^n = e^{\pm j2 \pi n} \qquad \mbox{with integer } n ,$$
we can change the mathematical representation of the sequence of samples $x[n]$ as
$$\begin{eqnarray}
x[n] &=& \left( \frac{A}{2} e^{j\phi} \right) \cdot e^{j\theta n} \cdot 1 + \left(\frac{A}{2} e^{-j\phi} \right ) \cdot e^{-j\theta n} \cdot 1  \newline
&=& \left( \frac{A}{2} e^{j\phi} \right) \cdot e^{j\theta n} \cdot e^{j2\pi n} + \left( \frac{A}{2} e^{-j\phi} \right) \cdot e^{-j\theta n} \cdot e^{-j2 \pi n} \newline
&=& \left( \frac{A}{2} e^{j\phi} \right) \cdot e^{j(\theta + 2 \pi) n} + \left( \frac{A}{2} e^{-j\phi} \right) \cdot e^{-j(\theta + 2 \pi) n}
\end{eqnarray}$$
From this equation it follows that the <a href="../../continuous/continuoussignalprocessing_transforms_fs/#spectrum">spectral representation</a> of $x[n]$ consists again of the same two bars, but now at the relative frequencies $\theta + 2 \pi$ and $-(\theta + 2 \pi)$.
So we have found two different ways to represent the spectral information of the same sequence of samples $x[n]$. Moreover we can find an infinite amount of different <a href="../../continuous/continuoussignalprocessing_transforms_fs/#spectrum">spectral representations</a>, just by adding or subtraction an integer times $2\pi$ to the relative frequency $\theta$. Thus the same relative <a href="../../continuous/continuoussignalprocessing_transforms_fs/#spectrum">spectral content</a> is repeated every $2\pi$.

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The spectral representation of a discrete-time signal $x[n]$ is not unique. The relative frequency representation is periodic with period $2\pi$.</i></div>


<div class="example">
<h4> Example </h4>
<hr>

Plot the <a href="../../continuous/continuoussignalprocessing_transforms_fs/#spectrum">spectral representation</a> of the sequence of samples which are represented by $x[n]=2 \cos(0.4 \pi n + \frac{\pi}{4})$ in the range $-3 \pi < \theta < 3 \pi$.

<button class="collapsible">Show solution</button>
<div class="content">

By using <a href="../../mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> we can write $x[n]$ as
$$ x[n] = e^{j{\color{red}{(0.4 \pi n + \frac{\pi}{4})}}} + e^{-j{\color{blue}{(0.4 \pi n + \frac{\pi}{4})}}} \mbox{ } \left( = 2 \cos \left( 0.4 \pi n + \frac{\pi}{4}\right) \right).$$
So the spectral plot contains two bars: One at frequency $0.4 \pi$ (in red) and one at $-0.4 \pi$ (in blue) as depicted in the Figure below.
When adding or subtracting $2\pi$ to both frequency components we obtain the following possibilities within the range $-3 \pi < \theta < 3 \pi$:
$0.4 \pi + 2 \pi = 2.4 \pi$
$$
\Rightarrow \mbox{ }
x[n] = e^{j{\color{red}{(2.4 \pi n + \frac{\pi}{4})}}} + e^{-j{\color{blue}{(2.4 \pi n + \frac{\pi}{4})}}} \mbox{ } \left( = 2\cos \left(2.4 \pi n + \frac{\pi}{4} \right) \right)
$$
$0.4 \pi - 2 \pi = - 1.6 \pi$
\begin{eqnarray}
\Rightarrow \mbox{ }
x[n] &=& e^{j{\color{red}{(-1.6 \pi n + \frac{\pi}{4})}}} + e^{-j{\color{blue}{(-1.6 \pi n + \frac{\pi}{4})}}} \newline
&=& e^{j{\color{blue}{(1.6 \pi n - \frac{\pi}{4})}}} + e^{-j{\color{red}{(1.6 \pi n - \frac{\pi}{4})}}}
\mbox{ } \left( = 2\cos \left(1.6 \pi n - \frac{\pi}{4}\right) \right)
\end{eqnarray}
Note that for this last case the phase has changed from sign.

All these possibilities are depicted in the Figure below.
From this Figure it follows that the <a href="../../continuous/continuoussignalprocessing_transforms_fs/#spectrum">spectral representation</a> of $x[n]$ is indeed repeated every $2\pi$ outside the period $-\pi < \theta < \pi$.

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



## Uniqueness issue viewed in discrete-time domains
In this subsection we will show by an example that different continuous-time signals can convert via an C-to-D convertor into the same sequence of samples.

<div class="example">
<h4> Example </h4>
<hr>

In this example we convert two different continuous-time signals $x_1(t)=\cos (400 \pi t)$ and ${\color{red}{x_2(t)}} = \cos (2400 \pi t)$ with a C-to-D convertor, which runs at a sample rate of $f_s=1000$ [samples/sec], to the discrete-time domain. Calculate the sequence of samples $x_1[n]$ and $x_2[n]$ for two periods and make a plot which shows $x_1(t), {\color{red}{x_2(t)}}$ and the samples of $x_1[n]$ and $x_2[n]$.

<button class="collapsible">Show solution</button>
<div class="content">

The converted signals are as follows:
\begin{eqnarray}
x_1[n] &=& \cos \left( 400 \pi \cdot \frac{1}{1000} n \right)\newline
 &=& \cos (0.4 \pi n ) = {\color{blue} {\ldots, 1, 0.3, -0.8, -0.8, 0.3, 1, \ldots }}\newline
x_2[n] &=& \cos \left( 2400 \pi \cdot \frac{1}{1000} n \right) \newline
&=& \cos (2.4 \pi n) = {\color{blue}{\ldots, 1, 0.3, -0.8, -0.8, 0.3, 1, \ldots }}
\end{eqnarray}

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


## The Fundamental Interval (FI)
We have seen that the relative frequency representation of a discrete-time signal is periodic with period $2\pi$. So in general only one interval of width $2\pi$ is of importance. In most cases we will use the interval of relative frequencies $-\pi < \theta \leq \pi$. This interval is called the Fundamental Interval (FI). Furthermore from the definition of the <a href="../../discrete/discretesignalprocessing_sampling_frequency">relative frequency</a>
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
to the discrete-time domain samples $x[n]=x_1[n]+x_2[n]$, by an ideal C-to-D convertor which runs at a sample rate of $f_s=600$ [samples/sec]. Give a plot of the <a href="../../continuous/continuoussignalprocessing_transforms_fs/#spectrum">frequency representation</a> of the continuous-time signal $x(t)$ and give also a plot of the <a href="../../continuous/continuoussignalprocessing_transforms_fs/#spectrum">frequency representation</a> of the discrete-time signal $x[n]$ in the Fundamental Interval (FI).

<button class="collapsible">Show solution</button>
<div class="content">

The spectral components of the continuous-time domain signal $x(t)$ are depicted in the upper part of the Figure below.
This Figure also shows that frequencies smaller than 300 [Hz] map into the FI.
So the result of the C-to-D conversion of $x_1(t)$ is as follows:
$x_1(t)= 4 \cos\left(400 \pi t + \frac{\pi}{4}\right)$ $\Rightarrow$
\begin{eqnarray}
x_1[n]&=& 4 \cos \left(\frac{2 \pi}{3}n + \frac{\pi}{4}\right) = \left( 2 e^{j\frac{\pi}{4}} \right ) e^{j\frac{2 \pi}{3}n} + \left( 2 e^{-j\frac{\pi}{4}} \right) e^{-j\frac{2 \pi}{3}n}
\end{eqnarray}
Furthermore the  result of the C-to-D conversion of $x_2(t)$ is as follows:
$x_2(t)= 2 \sin \left(1000 \pi t - \frac{\pi}{3}\right)$ $\Rightarrow$
\begin{eqnarray}
x_2[n]&=& 2 \sin\left(\frac{5 \pi}{3} n - \frac{\pi}{3} \right) \newline
&=& \left( {\color{red}{\frac{1}{j} e^{-j\frac{\pi}{3}}} }\right) e^{j\frac{5 \pi}{3} n}  + \left( {\color{blue}{\frac{-1}{j} e^{j\frac{\pi}{3}}}} \right) e^{-j\frac{5 \pi}{3} n} \newline
&=& \left( {\color{red}{\frac{1}{j} e^{-j\frac{\pi}{3}}}} \right ) e^{-j\frac{\pi}{3} n}  +
\left( {\color{blue}{\frac{-1}{j} e^{j\frac{\pi}{3}}}} \right) e^{j\frac{\pi}{3} n} \newline
&=& - \left(
\left({\color{blue}{\frac{1}{j} e^{j\frac{\pi}{3}}}} \right) e^{j\frac{\pi}{3} n} +
\left( {\color{red}{\frac{-1}{j} e^{-j\frac{\pi}{3}}}} \right) e^{-j\frac{\pi}{3} n} \right) \newline
&=& - 2 \sin\left(\frac{\pi}{3} n + \frac{\pi}{3} \right)
\end{eqnarray}
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
