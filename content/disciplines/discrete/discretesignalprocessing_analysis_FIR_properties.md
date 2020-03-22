+++
title = "Frequency response FIR: properties"

# date = {{ .Date }}
lastmod = 2019-10-13

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Propterties"
  weight = 2
  parent = "Analysis I: Frequency response FIR"
+++

### Screencast video
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/NfUhwbn5ANU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>

In the previous section, we found the following relation between the impulse response description in time domain $h[n]$ and the frequency response description in frequency domain $H(e^{j\theta})$:
$$
\boxed{
\begin{eqnarray*}
\text{Time domain} & \circ  \hspace{-2.3mm} - \hspace{-1.1mm}  \circ & \text{Frequency domain} \newline
h[n]= \sum\_{k=0}^{M-1} h[k] \delta[n-k] & \circ  \hspace{-2.3mm} - \hspace{-1.1mm}  \circ &
H(e^{j\theta})= \sum\_{k=0}^{M-1} h[k] e^{-j\theta k}
\end{eqnarray*} }
$$

The first important property of the Frequency response $H(e^{j\theta})$, is that it is a periodic function with period $2 \pi$. This can be verified by adding an integer number $l$ times $2\pi$ to the frequency $\theta$, which result into:
\begin{eqnarray*}
H(e^{j(\theta + l \cdot 2 \pi)})&=& \sum\_{k=0}^{M-1} h[k] e^{-j(\theta   + l \cdot 2 \pi )\cdot k} =
\sum\_{k=0}^{M-1} h[k] e^{-j\theta k } \cdot e^{-jl \cdot k \cdot 2 \pi} \newline
&=& \sum\_{k=0}^{M-1} h[k] e^{-j\theta k } \cdot 1 = H(e^{j\theta}).
\end{eqnarray*}
The fact that the frequency response is a periodic function of $\theta$, with period $2\pi$, is the main reason that we do not denote this function as $H(\theta)$, but in a special way, namely by $H(e^{j\theta})$.

The second important property is that the Frequency response of a real impulse response $h[n]$ is a conjugate symmetric function, thus:
$$
H(e^{-j\theta}) = H^\ast(e^{j\theta}).
$$
A proof of this property is as follows:

By using the fact that the impulse response $h[n]$ is real, thus the complex conjugate values of the impulse response coefficients are the same as the impulse response values themselves ($h[n]= h^\ast[n]$), we obtain:

$$
H(e^{-j\theta}) = \sum_{k=0}^{M-1} h[k] e^{j\theta k} = \sum\_{k=0}^{M-1} h[k]\ (e^{-j\theta k})^\ast =  (\sum\_{k=0}^{M-1} h[k] e^{j\theta k})^\ast = H^\ast (e^{j\theta}).
$$


Concluding the two most important properties of the frequency response of an FIR filter with real coefficients are:
$$
\boxed{
\begin{eqnarray*}
\text{Periodic } & : & H(e^{j\theta})  =  H(e^{j(\theta + l \cdot 2 \pi}) \newline
\text{Complex conjugated } & : & H(e^{-j\theta})  = (H(e^{j\theta}))^\ast
\end{eqnarray*} }
$$


<div class="example">
<h4> Example </h4>
<hr>
Calculate the frequency response $H(e^{j\theta})$ of the FIR filter as depicted in the figure below and show the two main basic properties as described above.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/FIR/example3.svg"
      alt="Example to show basic properties of Frequency response."
    />
    <figcaption>
      Example to show basic properties of Frequency response.
    </figcaption>
  </figure>
</div>
<br>
<button class="collapsible">Show solution</button>
<div class="content">
From the signal flow graph (or realization scheme) of the FIR filter it follows that the impulse response is given by:
$$
h[n] = -\delta[n] + 3 \delta[n-1] - \delta[n-2]
$$
and from this equation we obtain the following expression for the frequency response:
$$
H(e^{j\theta}) = -1 e^{-j0 \theta} + 3 e^{-j\theta} - e^{-j2\theta} =
-1  + 3 e^{-j\theta} - e^{-j2\theta}.
$$
The periodicity of this function can be demonstrated by adding for example $2 \pi$ to the frequency $\theta$. This results in:
\begin{eqnarray*}
H(e^{j(\theta + 2 \pi)}) &=& -1  + 3 e^{-j(\theta + 2 \pi)} - e^{-j2(\theta + 2 \pi)} \\
&=& -1  + 3 e^{-j\theta} \cdot e^{-j2 \pi} - e^{-j2\theta} \cdot e^{-j2 \cdot 2 \cdot 2 \pi} \\
&=&  -1  + 3 e^{-j\theta} - e^{-j2\theta} = H(e^{j\theta}).
\end{eqnarray*}
The complex conjugate property can be shown as follows:
\begin{eqnarray*}
H(e^{-j\theta}) &=& -1  + 3 e^{j\theta} - e^{j2\theta} = -1 + 3 (e^{-j\theta})^\ast - (e^{-j2\theta})^\ast \\
&=& (-1)^\ast + (3 e^{-j\theta})^* + (-e^{-j2\theta})^\ast \\
&=& (-1  + 3 e^{-j\theta} - e^{-j2\theta})^\ast = H^\ast(e^{j\theta})
\end{eqnarray*}
</div>
</div>

<br></br>

## Graphical Representation

In the module Complex Numbers And Phasors (CNAP) we have seen that a complex number can be represented as a vector in the complex plane. Such a complex vector can be represented either in the Cartesian way or in the Polar way. In order to represent the frequency response $H(e^{j\theta})$, we often choose the Polar representation. For this reason, we write the frequency response as:
\begin{equation*}
H(e^{j\theta}) = |H(e^{j\theta})| \cdot e^{j\angle{H(e^{j\theta})}}.
\end{equation*}
To represent the frequency response graphically, we can make two plots: One representing the magnitude response $|H(e^{j\theta})|$ and the other representing the phase response $\angle{H(e^{j\theta})}$, both as a function of frequency $\theta$.

In most signal processing software, like Matlab, the plot of the phase response is restricted to the range $-\pi \leq \angle{H(e^{j\theta})} \leq \pi$. This is allowed because we may add or subtract $2 \pi$ to the phase without changing the result, thus:
$$
e^{j\angle{H(e^{j\theta})} \pm 2 \pi} =
e^{j\angle{H(e^{j\theta})}} \cdot e^{j\pm 2 \pi} =
e^{j\angle{H(e^{j\theta})}}.
$$


<div class="example">
<h4> Example </h4>
<hr>
Calculate the frequency response of a system that consists of two delays in series. Make a plot of both the magnitude- and phase-response as a function of relative frequency $\theta$ inside the Fundamental Interval (FI), thus with $|\theta| \leq \pi$.
<button class="collapsible">Show solution</button>
<div class="content">
The impulse response of this system is given by $h[n]=\delta[n-2]$ and from this it follows that the frequency response equals $H(e^{j\theta}) = \color{red}{1} \cdot \text{e}^{j (\color{blue}{-2 \theta})}$. Thus the magnitude response is equal to $\color{red}{|H(e^{j\theta})| =1}$ and the phase response is equal to $\color{blue}{\angle{H(e^{j\theta})}= -2 \theta}$.
The graphical representation of the magnitude- and phase-response is depicted in the figure below. In the lower left-hand side figure we can see that, within the FI, the plot of the phase response of this system is in the range:
$-2\pi \leq e^{j\angle{H(e^{j\theta})}} \leq 2 \pi$.
However, the phase does not change if we add or subtract $2\pi$, since $e^{j2\pi} = e^{-j2\pi}=1$.
Thus, in the graphical representation of the phase response we can subtract $2\pi$ in case the phase response becomes larger than $2\pi$. Similarly we can add $2\pi$ in case the value becomes smaller than $2 \pi$. The lower right-hand plot depicts the phase response within these boundaries
$\color{blue}{|\angle{H(e^{j\theta})|}} \leq \pi$. This is usually automatically done in MATLAB.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/FIR/twodelays.svg"
      alt="Magnitude- and phase-response of a system with 2 delays."
    />
    <figcaption>
      Magnitude- and phase-response of a system with 2 delays.
    </figcaption>
  </figure>
</div>
</div>
</div>


The magnitude response $|H(e^{j\theta})|$ is a positive function of $\theta$. However, it may occur that by evaluation of the frequency response we obtain an expression that looks like:
$$
H(e^{j\theta}) = A(e^{j\theta}) \cdot e^{j\angle{H(e^{j\theta})}},
$$
in which $A(e^{j\theta})$ can become negative for some values of $\theta$. When representing the magnitude response $|H(e^{j\theta})|$, which is the absolute value of $A(e^{j\theta})$, we need to compensate for the fact that we plot a negative value as a positive value. So for frequencies for which $A(e^{j\theta})$ is negative we obtain the magnitude response plot $|H(e^{j\theta})|$ by multiplying $A(e^{j\theta})$ by $-1$. This is equal to a phase correction of $\pm \pi$, since $-1 = e^{j\pi}=e^{-j\pi}$.
Thus, due to the fact that we plot the magnitude response $|H(e^{j\theta})|$, we will see phase jumps of $\pm \pi$ in the phase response plot at those positions where we have zero crossings in the magnitude response. Concluding, we have the following rules for the graphical representation of the magnitude- and phase-response plots of the frequency response:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i><ul><li>Both Magnitude- and phase- response are depicted in the Fundamental Interval (FI): $|\theta| \leq \pi$.</li><li>The phase response is depicted in the range $|\angle{H(e^{j\theta})}| \leq \pi$.</li><li>A phase jump of $\pm \pi$ is applied in the phase response plot for each zero crossing of the magnitude response.</li></ul></i></div>


<div class="example">
<h4> Example </h4>
<hr>
Calculate the frequency response $H(e^{j\theta})$ of a first order difference system, from which the Difference Equation is given by: $y[n]=x[n]-x[n-1]$, and make a graphical plot for $\theta$ in the Fundamental Interval ($|\theta| \leq \pi$)of the magnitude response $|H(e^{j\theta})|$ and phase response $\angle{H(e^{j\theta})}$, with $|\angle{H(e^{j\theta})}| \leq \pi$.
<button class="collapsible">Show solution</button>
<div class="content">
The frequency response of this first order difference system is given by: $H(e^{j\theta}) = 1 - e^{-j\theta}$. In order to give the graphical representation of the magnitude- and phase-response we can rewrite the frequency response as follows:
\begin{eqnarray*}
H(e^{j\theta}) &=& \left ( e^{j\frac{\theta}{2}} - e^{-j\frac{\theta}{2}} \right ) \cdot e^{-j\frac{\theta}{2}} = 2 \sin (\frac{\theta}{2} ) \cdot j \cdot e^{-j\frac{\theta}{2}} \\
&=& \color{red}{2 \sin (\frac{\theta}{2} )} \cdot e^{j\color{blue}{(\frac{\pi}{2} - \frac{\theta}{2} )}} = \color{red}{|H(e^{j\theta})|} \cdot e^{j\color{blue}{\angle{H(e^{j\theta})}}}.
\end{eqnarray*}
Because of the fact that the function $\color{red}{2 \sin (\frac{\theta}{2} )}$ becomes negative in the frequency range $-\pi \leq \theta <0$, we have to compensate the phase with $-\pi$ in this range. Thus, the magnitude- and phase- response of this first order difference system are given by:
$$
\color{red}{|H(e^{j\theta})|} = \left | \color{red}{2 \sin (\frac{\theta}{2} )} \right | \text{ ; } \color{blue}{\angle{H(e^{j\theta})}} =
\left \{
\begin{array}{ll}
\frac{\pi}{2} - \frac{\theta}{2} & \text{ for } 0 \leq \theta \leq \pi \\
-\frac{\pi}{2} - \frac{\theta}{2} & \text{ for } -\pi \leq \theta < 0
\end{array}
\right .
$$
These plots are shown in the figure below. We can see a phase jump of $\pi$ at the zero crossing for frequency $\theta =0$.
<div style="max-width: 400px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/FIR/firstorder.svg"
      alt="Magnitude- and phase-response of first order difference system."
    />
    <figcaption>
      Magnitude- and phase-response of first order difference system.
    </figcaption>
  </figure>
</div>
</div>
</div>


### Moving average filter
A moving average filter is used to evaluate the average value of successive input signal samples. By averaging these values we typically expect the higher frequencies to be attenuated. This effect can be shown by evaluating and making plots of the frequency response of such an moving average filter. This is done as follows:

The Difference Equation (DE) of an $L$-point moving average filter is given by:
$$
y[n] = \frac{1}{L} \sum\_{k=0}^{L-1} x[n-k]
$$
From this we obtain the frequency response using the geometric series $\sum\_{k=0}^{L-1} a^k = \frac{1 - a^L}{1-a}$ as:
$$
\begin{eqnarray*}
H(e^{j\theta}) &=& \frac{1}{L} \sum\_{k=0}^{L-1} e^{-jk \theta} = \frac{1}{L} \frac{1 - e^{-jL \theta}}{1 - e^{-j\theta}} = \frac{1}{L} \frac{e^{jL \frac{\theta}{2}} - e^{-jL \frac{\theta}{2}}}{e^{j\frac{\theta}{2}} - e^{-j\frac{\theta}{2}}} \cdot \frac{e^{-jL \frac{\theta}{2}}}{e^{-j\frac{\theta}{2}}} \newline
&=& \color{red}{\frac{\sin (L \frac{\theta}{2})}{L \sin (\frac{\theta}{2})}} \cdot
e^{-j\color{blue}{(L-1) \frac{\theta}{2}}}
\end{eqnarray*}
$$
Thus the magnitude- and phase-response of a moving average filter are given by the following expressions:
\begin{eqnarray*}
|H(e^{j\theta})| &=& \left | \color{red}{\frac{\sin (L \frac{\theta}{2})}{L \sin (\frac{\theta}{2})}}
\right | \newline
\angle{H(e^{j\theta})} &=& \color{blue}{-(L-1) \frac{\theta}{2}}.
\end{eqnarray*}
An important value of the magnitude-response is the value for $\theta=0$. This value can be found  by approximate the sin-functions by the first component of its Taylor expansion, meaning that for small values of $x$ the value of $\sin(x)$ can be approximated by its first term of the geometric series: $\sin(x) = x - \frac{x^3}{3!} + \frac{x^5}{5!} + \cdots$. Thus for small values of $x$ we can approximate the fraction $\frac{\sin(L x)}{L sin(x)}$ by $\frac{(L x)}{L (x)} =1 $.
\begin{eqnarray*}
\frac{\sin (L \frac{\theta}{2})}{L \sin (\frac{\theta}{2})}\mid\_{\theta=0} &=& \lim_{\theta \rightarrow 0} \left\\{ \frac{\sin(L \theta)}{L \sin(\theta)} \right\\} = 1 .
\end{eqnarray*}
The other important values of the phase-response are the zero-crossings, because at these frequencies we will find phase jumps of $\pm \pi$ in the phase-response plot.
These zero-crossing can be found for those frequencies for which $|H(e^{j\theta})|$ is zero. Because the frequency of the numerator of $|H(e^{j\theta})|$ increases $L$ times faster than the frequency of the denominator, we can find these zero crossings by evaluating those frequencies for which the numerator is zero. Besides $\theta=0$ these values can be found as follows:
\begin{eqnarray*}
\sin (L \frac{\theta}{2}) = 0 & \Leftrightarrow & L \frac{\theta}{2} = k \pi \quad \Rightarrow \quad \theta=\frac{2\pi}{L} .
\end{eqnarray*}
An example is shown in Fig. 1, which is the graphical representation of the magnitude- and phase-response of an 11-point averaging filter.

<div style="max-width: 400px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/FIR/magphase11.svg"
      alt="Magnitude- and phase-response of 11-point averaging filter."
    />
    <figcaption class="numbered">
      Magnitude- and phase-response of 11-point averaging filter.
    </figcaption>
  </figure>
</div>


From the left-hand figure we clearly can see that indeed this 11-point averaging filter attenuates higher frequencies. Furthermore, we see 10 zero crossings at locations $\theta=k \cdot \frac{2 \pi}{11}$, for $k=\pm 1, \pm 2, \cdots \pm 5$.
In the right-hand side phase-response plot we see that the slope of the plot is $-(L-1)\frac{\theta}{2}= - 5 \theta$. Furthermore, at each of the 10 zero crossings of the magnitude-response we observe a phase jump of $\pm \pi$.

<br></br>

## Cascading FIR systems
In the previous module FIR we have seen that we can combine the impulse responses $h_1[n]$ and $h_2[n]$ of two cascaded FIR filters to one impulse response $h[n]$ which can be obtained as the convolution sum of the two individual impulse responses. Thus $h[n]=h_1[n] \star h_2[n]$.

Now let us see how this works when we use the frequency responses $H_1(e^{j\theta})$ and $H_2(e^{j\theta})$ of the two FIR filters. This is depicted in Fig. 2.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/FIR/cascade.svg"
      alt="Cascading of two FIR filters."
    />
    <figcaption class="numbered">
      Cascading of two FIR filters.
    </figcaption>
  </figure>
</div>


When applying a phasor with frequency $\color{red}{e^{j\theta n}}$ to the first filter, the resulting output signal can be described by $H_1(e^{j\theta}) \cdot \color{red}{e^{j\theta n}}$. This is a phasor with frequency $\theta$ and the magnitude and phase of this phasor are given by the complex number $H_1(e^{j\theta})$. Now we apply this phasor to the second filter, which results into $ \color{blue}{H_1(e^{j\theta}) \cdot H_2(e^{j\theta})} \cdot \color{red}{e^{j\theta n}}$. In other words the phasor $\color{red}{e^{j\theta n}}$ of the input signal results is changed in amplitude and phase by the complex value $ \color{blue}{H_1(e^{j\theta}) \cdot H_2(e^{j\theta})}$. From this we can conclude the following:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>When cascading two different FIR filters, one with frequency response $H_1(e^{j\theta})$ and the other with frequency response $H_2(e^{j\theta})$, we may combine these two FIR filters to one FIR filter of which the frequency response is given by the product of the individual frequency responses: $H(e^{j\theta})= H_1(e^{j\theta}) \cdot H_2(e^{j\theta})$.
</i></div>

<div class="example">
<h4> Example </h4>
<hr>
The following two FIR filters are cascaded:
$h_1[n] = \delta[n]+\delta[n+2]$ and $h_2[n] = \delta[n]-\delta[n+2]$. Calculate the impulse- and frequency- response when we cascade these two FIR filters.
<button class="collapsible">Show solution</button>
<div class="content">
Via the impulse responses:
$$
h[n]= h_1[n] \star h_2[n] = \left ( \delta[n] + \delta[n-2] \right ) \star \left ( \delta[n] -\delta[n-2] \right ) =\delta[n] -\delta[n-4]
$$
Via frequency responses:
$$
H(e^{j\theta})= H_1(e^{j\theta}) \cdot H_2(e^{j\theta}) = \left ( 1 + e^{-j2 \theta} \right ) \cdot
\left ( 1 - e^{-j2 \theta} \right ) = 1 - e^{-j4 \theta}
$$
</div>
</div>


In general we can conclude that a convolution in time domain is equivalent to multiplication in the frequency domain:
$$
\boxed{
h_1[n] * h_2[n] \hspace{3mm} \circ  \hspace{-2.3mm} - \hspace{-1.1mm}  \circ \hspace{3mm} H_1(e^{j\theta}) \cdot H_2(e^{j\theta})
}
$$

<br></br>

## Steady State and transient behaviour
Until now we assumed signals exist for all values of $n$ in the range $-\infty < n < \infty$. However, in practice this will not be the case. More realistically, a signal would for example start with index $n=0$, thus:
$$
x[n] = A e^{j(\theta_1 n + \phi)} \cdot u[n] =
\begin{cases}
A e^{j(\theta_1 n + \phi)} & \text{for } n \geq 0 \newline
0 & \text{ for } n < 0 .
\end{cases}
$$

We can use the convolution sum to find an expression for the output of an FIR filter with impulse response $h[n]$ to such an input signal. This result in:
$$
y[n] = \sum\_{k=0}^{M-1} h[k] x[n-k] = \sum\_{k=0}^{M-1} h[k] A e^{j(\theta_1 (n-k) + \phi)} \cdot u[n-k] .
$$

By using the fact that the unit step $u[n-k]$ is only 1 for indices $n-k \geq 0$, or equivalently for $\color{red}{k \leq n}$, this equation can be rewritten as follows:
$$
y[n] =
\begin{cases}
0 & n < 0 & \newline
\left ( \sum\_{k=0}^{\color{red}{n}} h[k] e^{-j\theta_1 k} \right ) \cdot A e^{j(\theta_1 n + \phi)} &
0 \leq n < M-1 & \textbf{Transient region} \newline
\left ( \sum\_{k=0}^{\color{blue}{M-1}} h[k] e^{-j\theta_1 k} \right ) \cdot A e^{j(\theta_1 n + \phi)} & n \geq M-1 & \textbf{Steady state region}
\end{cases}
$$

<b><u>Concluding:</u></b>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i><ul><li><b> Transient region:</b> The complex multiplier $\left ( \sum_{k=0}^{{\color{red}{n}}} h[k] e^{-j\theta_1 k} \right )$ depends on the index $n$.</li><li><b>Steady state region:</b> The complex multiplier $\sum_{k=0}^{{\color{blue}{M-1}}} h[k] e^{-j\theta_1 k}$ is constant. Output contains only input frequency ($\theta_1$ in this example).</li><li>If for $n > M-1$ the input changes to zero or to another frequency $\theta_2 \neq \theta_1$, then there will be a new transition- and steady state- region.</li></ul></i></div>


Fig. 3 shows the transient-region (in red samples) and steady- state region when we apply the signal $x[n]= \cos(\frac{\pi}{3}n) \cdot u[n]$ to an FIR filter with impulse response $h[k] = \delta[n] + 2 \delta[n-1] + \delta[n-2]$.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/FIR/transient.svg"
      alt="Example to show transient- and steady-state region."
    />
    <figcaption class="numbered">
      Example to show transient- and steady-state region.
    </figcaption>
  </figure>
</div>

<br></br>

## Filtering continuous signal
In practice we often filter a continuous-time signal in the discrete-time domain as depicted in Fig. 4. The main motivations for this, is that the implementation in discrete-time domain is much more flexible and cheaper compared to the implementation in the continuous-time domain.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/FIR/SUMfiltcont.svg"
      alt="Filtering continuous-time signal in the discrete-time domain."
    />
    <figcaption class="numbered">
      Filtering continuous-time signal in the discrete-time domain.
    </figcaption>
  </figure>
</div>

Of course in practice we have to take care of the aliasing effect, as discussed in the module on <a href="../../../disciplines/discrete/discretesignalprocessing_sampling_main/">sampling and reconstruction</a>, so the sampling frequencies of the C/D and D/C convertor are chosen at least twice the largest frequency of the continuous-time signal $x(t)$.

<div class="example">
<h4> Example </h4>
<hr>
Given the continuous-time signal $x(t)= 5 + 2 \cos(2100 \pi t + \frac{\pi}{4}) + 3 \cos(2800 \pi t - \frac{\pi}{6})$. We sample this signal with a C/D convertor that runs at a a sample rate $f_s = 1/T_s = 4200$ [samples/sec]. Next we filter the discrete-time signal samples $x[n]$ with an FIR filter of which the impulse response is given by $h[n]=\delta[n] + \delta[n-1]$. The discrete-time output signal samples $y[n]$ are converted back to the continuous-time signal $y(t)$ by a D/C convertor.
The D/C convertor runs at the same sampling frequency $f_s1/T_s = 4200$ [samples/sec] as the C/D convertor. Calculate the continuous-time signal $y(t)$.
<button class="collapsible">Show solution</button>
<div class="content">
With a sample rate $f_s = 1/T_s = 4200$ [samples/sec] of the C/D convertor we obtain the following expression for the discrete-time input signal samples:
$$
x[n] = 5 + 2 \cos(\frac{\pi}{2}n + \frac{\pi}{4}) + 3 \cos (\frac{2 \pi}{3}n - \frac{\pi}{6}).
$$
From the given impulse response it follows that the frequency response can be written as follows:
$$
H(e^{j\theta}) = 1 + e^{-j\theta} = 2 \cos (\frac{\theta}{2}) e^{-j\frac{\theta}{2}}
$$
The discrete-time input signal $x[n]$ consists of the frequencies: $\theta=0, \frac{\pi}{2}$ and $\frac{2\pi}{3}$, so we have to evaluate the frequency response $H(e^{j\theta})$ for these frequencies in order to find the output signal $y[n]$. Thus:
\begin{eqnarray*}
H(e^{j\theta})\mid_{\theta=0} &=& 2 \\
H(e^{j\theta})\mid_{\theta=\frac{\pi}{2}}= H^\ast(e^{j\theta})\mid_{\theta=-\frac{\pi}{2}}&=&
\color{red}{\sqrt{2} e^{-j\frac{\pi}{4}}} \\
H(e^{j\theta})\mid_{\theta=\frac{2\pi}{3}}= H^\ast(e^{j\theta})\mid_{\theta=-\frac{2\pi}{3}}&=&
\color{blue}{ e^{-j\frac{\pi}{3}}} .
\end{eqnarray*}
Based on these values the output $y[n]$ is as follows:
\begin{eqnarray*}
y[n] &=& 5 \cdot 2 + 2 \cdot \color{red}{\sqrt{2}} \cos(\frac{\pi}{2}n + \frac{\pi}{4}\color{red}{- \frac{\pi}{4}}) + 3 \cdot \color{blue}{1} \cos (\frac{2 \pi}{3}n - \frac{\pi}{6}\color{blue}{- \frac{\pi}{3}}) \\
&=& 10 + 2 \sqrt{2} \cos(\frac{\pi}{2}n ) + 3 \cos (\frac{2 \pi}{3}n - \frac{\pi}{2})
\end{eqnarray*}
With a sample rate $f_s = 1/T_s = 4200$ [samples/sec] of the D/C convertor the resulting continuous-time output signal becomes:
$$
y(t) = 10 + 2 \sqrt{2} \cos(2100 \pi t ) + 3 \cos (2800 \pi t - \frac{\pi}{2}).
$$
</div>
</div>
