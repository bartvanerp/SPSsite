+++
title = "Reconstruction of sinusoidal signals"

# date = {{ .Date }}
lastmod = 2019-08-22

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Reconstruction of sinusoidal signals"
  weight = 22
  parent = "Basics of sampling and reconstruction"

+++

In this section we will describe the reconstruction process of the D-to-C convertor which converts the sequence of discrete-time samples $x[n]$ into the continuous-time signal $x(t)$.

## Conceptual video
<iframe width="100%" height="450" src="https://www.youtube.com/embed/xeW5RyqHVis" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Ideal D-to-C convertor
Because of the <a href="../../discrete/discretesignalprocessing_sampling_uniqueness">uniqueness issue</a> in the discrete-time domain, the ideal D-to-C convertor makes a choice which frequencies are used for the conversion to the continuous-time domain. For this reason the ideal D-to-C convertor selects only frequencies which are inside the FI.

<div style="max-width: 400px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/sampling/ideal_DC.svg"
      alt="Ideal D-to-C converter."
    />
    <figcaption>
      Ideal D-to-C converter.
    </figcaption>
  </figure>
</div>

Let's start the description of the reconstruction from discrete-time to continuous-time by using again a simple sinusoidal signal from which the sequence of samples is described by
$$ x[n] =  A \cos (\theta n + \phi). $$
Because of the <a href="../../discrete/discretesignalprocessing_sampling_uniqueness">uniqueness issue</a> we assume that the <a href="../../discrete/discretesignalprocessing_sampling_frequency">relative frequency</a> $\theta$ is within the <a href="../../discrete/discretesignalprocessing_sampling_uniqueness/#the-fundamental-interval-fi">Fundamental Interval (FI)</a>, thus $\theta < \pi$. In case this is not true, we first map the relative frequency into the FI. Furthermore we use the relation between relative and absolute frequency given by
$$\theta= 2 \pi \frac{f}{f_s},$$
from which we assume as before that the ratio $\frac{f}{f_s}$ is a rational number. Finally, since we have for this simple example the mathematical description of the signal samples as a sinusoidal function, we can obtain the mathematical description of the continuous-time signal $x(t)$ by replacing the integer index $n$ by the continuous-time variable $t \cdot f_s$, leading to
$$ x(t) = x[n]|\_{n=t \cdot f_s} = A \cos ( 2 \pi \frac{f}{f_s} \cdot f_s \cdot t + \phi) = A \cos (2 \pi f t + \phi) $$
Fig. 1 shows an example where we converted the sequence of samples $x[n]=\cos (0.4 \pi n)= \ldots, 1, 0.3, -0.8, -0.8, 0.3, 1, \ldots $ to the continuous-time signal $x(t)$, with an ideal D-to-C convertor, which runs at a sample rate of $f_s=1000$ [samples/sec].
In Fig. 2 the sequence of input signal samples $x[n]$ is represented in a plot.


<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/sampling/reconstruction_numbers.svg"
      alt="The reconstruction process where the input $x[n]$ is represented as a series of numbers."
    />
    <figcaption class="numbered">
      The reconstruction process where the input $x[n]$ is represented as a series of numbers.
    </figcaption>
  </figure>
</div>

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/sampling/reconstruction_plot.svg"
      alt="The reconstruction process where the input $x[n]$ is represented as a plot."
    />
    <figcaption class="numbered">
      The reconstruction process where the input $x[n]$ is represented as a plot.
    </figcaption>
  </figure>
</div>

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>An ideal D-to-C convertor chooses the relative frequencies within the FI: $- \pi < \theta \leq \pi$. In case a C-to-D convertor produces a frequency outside the FI, such a frequency will always first be mapped inside the FI and the D-to-C convertor will use this frequency for the conversion of the discrete-time signal into a continuous-time signal. This mapping back into the FI is called <b> Aliasing</b>.</i></div>




<div class="example">
<h4> Example </h4>
<hr>

A continuous-time input signal $x(t)$ is converted to the discrete-time domain samples $x[n]$ with an ideal C-to-D convertor which runs at a sample rate of $f_{s,in}$ [samples/sec]. After that the samples $x[n]$ are converted back to the continuous-time signal $y(t)$ with an ideal D-to-C convertor which runs at a sample rate of $f_{s,out}$ [samples/sec]. The input signal $x(t)$ and the sample rate $f_{s,in}$ are $x(t) = x_1(t) + x_2(t)$, with $x_1(t)= 4 \cos(400 \pi t + \frac{\pi}{4})$, $x_2(t)= 2 \sin (1000 \pi t - \frac{\pi}{3})$ and $f_{s,in}=600$ [samples/sec]. In first instance we choose the sample rate of the D-to-C convertor equal to the sample rate of the C-to-D convertor, thus $f_{s,out} = f_{s,in}=600$ [samples/sec]. After that we change the sample rate of the D-to-C convertor to $f_{s,out}=900$ [samples/sec].
<br>
Calculate an expression for the output signal $y(t)$ in both cases.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/sampling/ideal_CDC.svg"
      alt="The reconstruction chain represented by ideal converters."
    />
    <figcaption>
      The reconstruction chain represented by ideal converters.
    </figcaption>
  </figure>
</div>
<br>


<button class="collapsible">Show solution</button>
<div class="content">

The first steps are the same of the last example of the previous subsection. The largest absolute frequency of the FI after the C-to-D convertor equals $f_{s,in}/2=300$ [Hz]. Thus the frequency of $x_1(t)$ (200 [Hz]) is converted inside the FI, at relative frequency $\frac{2\pi}{3}$, while the frequency of $x_2(t)$ (500 [Hz]) is converted outside the FI, at relative frequency $\frac{5\pi}{3}$. After mapping back this frequency inside the FI, into relative frequency $\frac{\pi}{3}$, we obtain the following mathematical description of the sequence of discrete-time samples $x[n]$:
$$
x[n]= 4 \cos \left(\frac{2 \pi}{3}n + \frac{\pi}{4}\right) - 2 \sin\left(\frac{\pi}{3} n + \frac{\pi}{3} \right)
$$
When converting the relative frequencies of this discrete-time signal into absolute frequencies of a continuous-time signal, we can make use of $\theta=2\pi\frac{f}{f_s}$. In case the sample rate of the D-to-C convertor $f_{s,out}=f_{s,in}=600$ [samples/sec] this leads to the following continuous-time output signal:
$$
y(t) = 4 \cos \left(400 \pi t + \frac{\pi}{4}\right) - 2 \sin\left(200 \pi t + \frac{\pi}{3}\right).
$$
Thus the frequency of the first 200 [Hz] component did not change while the frequency of the second 500 [Hz] component has changed due to aliasing.
However if we change the sample rate of the D-to-C convertor into $f_{s,out}=900$ [samples/sec] the resulting continuous-time signal becomes:
$$
y(t) = 4 \cos \left(600 \pi t + \frac{\pi}{4}\right) - 2 \sin\left(300 \pi t + \frac{\pi}{3}\right).
$$
Thus both frequencies are changed. The frequency of $x_2(t)$ has changed because of aliasing while above that both frequencies of $x_1(t)$ and $x_2(t)$ have changed because of the fact that the sample rates of C-to-D and D-to-C are different.

</div>
</div>


## Reconstruction D-to-C convertor based on samples $x[n]$
The D-to-C convertor constructs a continuous-time signal $x(t)$, based on the discrete-time samples $x[n]$.
In the previous subsection we have seen that for sampled sinusoidal signals the D-to-C convertor in effect replaces the discrete-time integer variable $n$ by the continuous-time variable $t \cdot f_s$. As a result we can construct, for such a case, the continuous-time signal $x(t)$ based on the mathematical description of the sinusoidal function. This procedure is only valid and possible in case of sampled sinusoidal signals and an example is shown at the left-hand side plot of Fig. 3. The continuous-time sinusoidal signal $x(t)$ (in blue) is constructed by replacing $n$ into $t \cdot f_s$ in the sinusoidal description of the samples $x[n]$.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/sampling/reconstruction.svg"
      alt="The reconstruction process with different types of reconstruction waveforms."
    />
    <figcaption class="numbered">
      The reconstruction process with different types of reconstruction waveforms.
    </figcaption>
  </figure>
</div>

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Only in case of sampled sinusoidal signals the ideal D-to-C convertor in effect replaces $n$ by $t \cdot f_s$.</i></div>

In the more general case the continuous-time output signal $y(t)$ is constructed by placing a continuous-time function $p(t)$ at each new position of a sample $x[n]$ and adding together all the resulting continuous-time signals. This reconstruction is performed via the so called
$$
\boxed{
\text{Interpolation equation} \qquad y(t)= \sum_{n=-\infty}^{\infty} x[n] p(t-n \cdot T_s)}
$$
in which the continuous-time function $p(t)$ represents the characteristic of the D-to-C convertor. In practice there are many different characteristic forms $p(t)$, e.g. a square pulse:
$$
p(t) =
\begin{cases}
1, & - \frac{1}{2} T_s < t \leq \frac{1}{2} T_s \newline
0, & \text{otherwise}
\end{cases}
$$

which leads to the so called 'zero order hold' procedure, which is depicted in the middle-part of Fig. 3. In this procedure the electronics of the D-to-C convertor are build in such a way that around each new discrete-time sample a continuous-time signal is constructed which has the same value as the discrete-time sample, while this value is kept constant during one sampling period of $T_s$ [sec]. Thus the reconstructed continuous-time signal looks like a 'stair-case' approximation of the sinusoidal signal as depicted (in red) in the left-hand side figure. The electronics needed for this conversion procedure are very simple and cheap. For this reason the 'zero order hold' procedure is applied very often in practice.

Another characteristic form of $p(t)$ is a triangular pulse:
$$
p(t) =
\begin{cases}
1- \frac{|t|}{T_s} , & |t| \leq T_s \newline
0, & \text{otherwise}
\end{cases}
$$

which leads to the conversion as shown in the right-hand side of Fig. 3. The signal samples are interpolated in a linear way. The reconstructed continuous-time signal looks like a 'triangular-like' approximation of the sinusoidal signal as depicted (in red) in the left-hand side figure.

## Sampling theorem
From the previous section it follows that for a system as depicted in Fig. 1, with $f\_{s,in}=f\_{s,out}=f\_s$, the output $y(t)$ of the D-to-C convertor is equal to input $x(t)$ of the ideal C-to-D convertor if the continuous-time signal $x(t)$ contains no frequencies higher than $f_{max}$ and the sampling frequency $f_s$ is larger than $2 \cdot f\_{max}$. This results into the following important <b>sampling theorem</b>, which is usually assigned to Shannon, who introduced this theorem around 1940. Almost at the same time Kotelnikov did the same. However some years before the theoretical basis was created by E.T. and J.A. Whittaker. This theorem states:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>A continuous-time signal $x(t)$ with frequencies no higher than $f_{max}$ can be reconstructed exactly from its samples $x[n]= x(t)\mid_{t=n \cdot T_s}$, if samples are taken at a rate $f_s=1/T_s$, that is greater than $2 f_{max}$.</i></div>
