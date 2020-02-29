+++
title = "Frequency response FIR: conceptual view"

# date = {{ .Date }}
lastmod = 2019-10-13

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Concept"
  weight = 1
  parent = "Analysis I: Frequency response FIR"
+++


## Frequency response FIR
Besides the impulse response, denoted by $h[n]$, and the Difference Equation (DE) we will see that the frequency response is an alternative description of an FIR filter. Obviously all these different descriptions are related to each other and each of the descriptions has its own advantage. The advantage of the frequency response description is that we can fairly easily see the response of the FIR to frequencies.

### Conceptual video
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/-p2D03X31uk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>

### Response FIR to phasor with single frequency
Since each single frequency can be viewed as the sum of two phasor components, we will first study the response of a very simple FIR filter, a delay, as a result of an input signal $x[n]$ which consists of one phasor frequency $\theta_1$, amplitude $A$ and phase $\phi$, thus $x[n]=\color{red}{ A e^{j(\theta_1 n + \phi)}}$. This is depicted in Fig. 1.

<div style="max-width: 400px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/FIR/delay.svg"
      alt="Response of a delay to signal $x[n]$."
    />
    <figcaption class="numbered">
      Response of a delay to signal $x[n]$.
    </figcaption>
  </figure>
</div>

The output can be calculated as follows:
$$
y[n]=x[n-1] =  A e^{j(\theta_1 (n-1) + \phi)} =
A e^{j(\theta_1 n + \phi - \theta_1)} =
\color{blue}{{e^{-j\theta}}} \cdot \color{red}{ {A e^{j(\theta_1 n + \phi)}}}
$$
From this result it follows that when applying a single phasor with frequency $\theta_1$ to a delay, then the output $y[n]$ contains exact the same phasor (denoted in red) with the same frequency $\theta_1$. Only the phase of the phasor has changed from $\color{red}{\phi}$ to $\color{red}{{\phi}} \color{blue}{- \theta_1}$.


<div class="example">
<h4> Example </h4>
<hr>
Given an FIR filter which consists of 4 delays, or equivalently, the impulse response equals $h[n]= \delta[n-4]$. Calculate the response of this filter when the input is a phasor with frequency $\theta_1=\frac{\pi}{8}$: $x[n] = \color{red}{2 e^{j(\frac{\pi}{8}n + \frac{\pi}{3})}}$.
<button class="collapsible">Show solution</button>
<div class="content">
The output of this FIR filter with 4 delays is as follows:
$$
\begin{eqnarray*}
y[n]&=& x[n-4]= 2 e^{j(\frac{\pi}{8}(n-4) + \frac{\pi}{3})} = 2 e^{j(\frac{\pi}{8}n - 4 \cdot \frac{\pi}{8} + \frac{\pi}{3})} \\
&=& \color{blue}{e^{-j\frac{\pi}{2}}} \cdot \color{red}{2 e^{j(\frac{\pi}{8}n + \frac{\pi}{3})}} = 2 e^{j(\frac{\pi}{8}n - \frac{\pi}{6})} .
\end{eqnarray*}
$$
Thus a system which contains 4 delays does only change the phase of the input phasor (from $+\frac{\pi}{3}$ into $- \frac{\pi}{6}$).
</div>
</div>


<div class="example">
<h4> Example </h4>
<hr>
Calculate the response of a simple FIR filter, as depicted in the figure below, when the input is the following phasor with frequency $\theta_1=\frac{\pi}{8}$: $x[n] = \color{red}{2 e^{j(\frac{\pi}{8}n + \frac{\pi}{3})}}$.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/FIR/example2.svg"
      alt="Simple FIR filter."
    />
    <figcaption>
      Simple FIR filter.
    </figcaption>
  </figure>
</div>
<br>
<button class="collapsible">Show solution</button>
<div class="content">
The output of this FIR filter is as follows:
$$
\begin{eqnarray*}
y[n]&=& x[n] + x[n-4]= 2 e^{j(\frac{\pi}{8}n + \frac{\pi}{3})} + 2 e^{j(\frac{\pi}{8}(n-4) + \frac{\pi}{3})} \\
&=& \color{blue}{( 1 + e^{-j\frac{\pi}{2}})} \cdot \color{red}{2 e^{j(\frac{\pi}{8}n + \frac{\pi}{3})}}
= \color{blue}{\sqrt{2} e^{-j\frac{\pi}{4}}} \cdot \color{red}{2 e^{j(\frac{\pi}{8}n + \frac{\pi}{3})}} = 2 \sqrt{2} e^{j(\frac{\pi}{8}n + \frac{\pi}{12})}.
\end{eqnarray*}
$$
So the phasor at the output has the same frequency ($\frac{\pi}{8}$) as the input, only the amplitude has changed from $2$ into $2\sqrt{2}$ and the phase has changed from $+\frac{\pi}{3}$ to $+\frac{\pi}{3}- \frac{\pi}{4} = \frac{\pi}{12}$.
</div>
</div>


The previous results can by generalized by using the following equation which describes the convolution sum of an FIR:
$$
y[n]= \sum_{k=0}^{M-1} h[k] x[n-k],
$$
in which $h[n]$, for $n=0,1, \cdots , M-1$ are the impulse response coefficients of the FIR filter. From this convolution sum we can calculate the following response of this system to the phasor $x[n]=\color{red}{ A e^{j(\theta_1 n + \phi)}}$:
$$
y[n] = \sum\_{k=0}^{M-1} h[k] A e^{j(\theta_1 (n-k) + \phi)} =
\left( \color{blue}{\sum\_{k=0}^{M-1} h[k]  e^{-j k \theta_1} }\right) \cdot \left( \color{red}{A e^{j(\theta_1 n + \phi)}} \right) .
$$
Thus we can split the result as a product of a complex quantity (in blue) multiplied with the phasor description of the input signal (in red). The complex quantity (in blue) only depends on the FIR impulse response $h[n]$ and the phasor frequency $\theta_1$ of the input signal.
Because of the fact that we can use any frequency for the frequency $\theta_1$, we can generalize this complex quantity as a function of $\theta$ which leads to the following definition:

\begin{equation}
\textbf{Frequency Response of FIR:} \hspace{6mm}
\boxed{H(e^{j\theta})= \sum_{k=0}^{M-1} h[k] e^{-j\theta k}}
\end{equation}
Here we denote the (discrete) impulse response with a small letter $h$, square brackets $[\cdot]$ and it is a function of discrete time function variable $n$. The frequency response is denoted by a capital letter $H$, round brackets $(\cdot)$ and it is a function of the continuous frequency variable $\theta$.
In fact we could denote the frequency response as $H(\theta)$. The reason that it is denoted as $H(e^{j\theta})$ will be explained in one of the following sections.

The frequency response $H(e^{j\theta})$ of an FIR describes how a phasor frequency of an input signal is changed in amplitude and phase by the FIR filter. E.g. for an input signal with phasor frequency $\theta_1$ the change in amplitude is a result of the magnitude of the frequency response evaluated at frequency $\theta=\theta_1$, denoted by $|H(e^{j\theta_1})|$. Furthermore the change in phase is a result of the phase of the frequency response evaluated at frequency $\theta=\theta_1$, denoted by $\angle{H(e^{j\theta_1})}$. This is depicted in Fig. 2.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/FIR/Freq1.svg"
      alt="Response of an FIR to a phasor input signal with frequency $\theta_1 $."
    />
    <figcaption class="numbered">
      Response of an FIR to a phasor input signal with frequency $\theta_1 $.
    </figcaption>
  </figure>
</div>


<div class="example">
<h4> Example </h4>
<hr>
First calculate the Frequency response $H(e^{j\theta})$ of the FIR filter with impulse response $h[n] = \delta[n] + 2 \delta[n-\color{red}{1}] + \delta[n-\color{blue}{2}]$ and then evaluate the response of this FIR filter to the phasor frequency $x[n]= e^{j(\frac{\pi}{3} n + \frac{\pi}{4})}$.
<button class="collapsible">Show solution</button>
<div class="content">
With the given impulse response $h[n]$ we obtain from the definition of the frequency response the following expression:
\begin{equation}
H(e^{j\theta})= 1 \cdot e^{-j0 \cdot \theta} + 2 \cdot e^{-j\color{red}{1} \cdot \theta} + 1 \cdot e^{-j\color{blue}{2} \cdot \theta}  = 1 +2 e^{-j\theta} + e^{-j2 \theta}.
\end{equation}
With the input signal $x[n]= \color{red}{e^{j(\frac{\pi}{3} n + \frac{\pi}{4})}}$ the resulting output signal can be found as follows:
\begin{eqnarray*}
y[n]&=& x[n] + 2 x[n-1] + x[n-2] \\
&=& e^{j(\frac{\pi}{3} n + \frac{\pi}{4})} + 2 e^{j(\frac{\pi}{3} (n-1) + \frac{\pi}{4})} + e^{j(\frac{\pi}{3} (n-2) + \frac{\pi}{4})} \\
&=& \left ( \color{blue}{ e^{-j0 \cdot \frac{\pi}{3}} + 2 e^{-j1 \cdot \frac{\pi}{3}} + e^{-j2 \cdot \frac{\pi}{3}}} \right ) \cdot \color{red}{e^{j(\frac{\pi}{3} n + \frac{\pi}{4})}}
\end{eqnarray*}
Alternatively, we can obtain the first part (in blue) of this last equation by evaluation the general description of the frequency response $H(e^{j\theta})$, as derived in the equation above, for frequency $\theta=\frac{\pi}{3}$. This will be denoted by $H(e^{j\theta})\mid_{\theta = \frac{\pi}{3}}$.
Thus for an input signal $x[n]= \color{red}{e^{j(\frac{\pi}{3} n + \frac{\pi}{4})}}$, which consists of a single phasor frequency $\theta=\frac{\pi}{3}$, with amplitude $A=1$ and phase $\phi=\frac{\pi}{4}$, we can alternatively obtain the output $y[n]$ of this FIR filter as follows:
$$
\begin{eqnarray*}
y[n] &=& \left ( \color{blue}{ H(e^{j\theta})\mid_{\theta = \frac{\pi}{3}} } \right ) \cdot \color{red}{e^{j(\frac{\pi}{3} n + \frac{\pi}{4})}}\newline
&=&
\left ( \color{blue}{ e^{-j0 \cdot \frac{\pi}{3}} + 2 e^{-j1 \cdot \frac{\pi}{3}} + e^{-j2 \cdot \frac{\pi}{3}}} \right ) \cdot \color{red}{e^{j(\frac{\pi}{3} n + \frac{\pi}{4})}} \newline
&=& \left ( \color{blue}{3 e^{-j\frac{\pi}{3}} } \right )
\cdot \color{red}{e^{j(\frac{\pi}{3} n + \frac{\pi}{4})}} = 3 e^{j(\frac{\pi}{3} n - \frac{\pi}{12})}.
\end{eqnarray*}
$$
Thus, the output signal $y[n]$ is also a phasor with the same frequency $\theta=\color{red}{\frac{\pi}{3}}$ as the input. However, the amplitude and phase of the input signal have been changed in a way which can be obtained by evaluating the frequency response $H(e^{j\theta})$ for the frequency $\theta = \frac{\pi}{3}$ of the input signal.
</div>
</div>




### Response FIR to sinusoidal signal with single frequency
Using the result of the previous subsection we can now find in a few steps,
as depicted in Fig. 3, the response of an FIR filter to a sinusoidal signal with a single frequency $x[n]=\color{red}{A \cos (\theta_1 n + \phi)}$.

  <div style="max-width: 600px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/analysis/FIR/Freq2.svg"
        alt="Response of an FIR to a sinusoidal signal with a single frequency."
      />
      <figcaption class="numbered">
        Response of an FIR to a sinusoidal signal with a single frequency.
      </figcaption>
    </figure>
  </div>

The first step is to split the sinusoidal signal into two phasor components, using Euler.
Next we can use the Linear Time Invariant (LTI) property of an FIR filter: Applying the sum of 2 signals to an FIR filter is equal to first applying the individual signals to the same FIR filters and than adding the results. This is depicted in the lower part of Fig. 3. In the upper branch of this figure the FIR filter is 'triggered' by a phasor with frequency $+ \theta_1$, while in the lower branch a copy of the same FIR filter is 'triggered' by a phasor with frequency $- \theta_1$.
As explained in the previous subsection, the change in amplitude and phase of both upper- and lower branch input signals follows from the magnitude $|H(e^{j\theta})|$ and phase $\angle{H(e^{j\theta})}$ of the frequency response evaluated at frequency $\theta_1$ and $-\theta_1$ respectively.
When adding the results of upper- and lower-branch, we obtain a sinusoidal signal at the output of the filter, of which the frequency is the same as the frequency of the input signal. The amplitude $\color{red}{A}$ of the input signal has been changed by the magnitude $\color{blue}{|H(e^{j\theta_1})|}$ of the frequency response of the FIR, while the phase
$\color{red}{\phi}$ of the input signal has been changed by the phase $\color{blue}{\angle{H(e^{j\theta_1})}}$ of the frequency response.
This is depicted in Fig. 4.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/FIR/sininLTIsinout.svg"
      alt="Response of an FIR to a sinusoidal input signal."
    />
    <figcaption class="numbered">
      Response of an FIR to a sinusoidal input signal.
    </figcaption>
  </figure>
</div>


Concluding, we have the following general result:
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>When applying a sinusoidal signal with a single frequency $\theta=\theta_1$ to an FIR filter, the output is a sinusoidal signal with the same frequency $\theta_1$ as the input signal, only the amplitude and phase have changed. The change in amplitude is described by the magnitude response evaluated at frequency $\theta_1$, thus $|H(e^{j{\theta}})\mid_{\theta=\theta_1}$, while the change in phase is described by the phase response evaluated at frequency $\theta_1$, thus $\angle{H(e^{j{\theta}})}\mid_{\theta=\theta_1}$.</i></div>
<br>

<div class="example">
<h4> Example </h4>
<hr>
In this example we use the same FIR filter as used in the previous example. Thus
$h[n] = \delta[n] + 2 \delta[n-1] + \delta[n-2]$ and from this it follows that the frequency response is given by $H(e^{j\theta}) = 1 + 2 e^{-j\theta} + e^{-j2 \theta}$. Now the input signal is given by the following sinusoidal signal: $x[n]= \cos(\frac{\pi}{3} n)$.
Calculate the output signal $y[n]$.
<button class="collapsible">Show solution</button>
<div class="content">
Now we can use the superposition property, which implies that
we can evaluate the output $y[n]$ to the input signal $x[n]=\cos(\frac{\pi}{3} n)$ by first splitting the cosine into its two phasor components $x_1[n]= e^{j\frac{\pi}{3}n}$ and $x_2[n]=e^{-j\frac{\pi}{3}n}$. Then evaluate the output of each of these two individual phasor components, which results into:
\begin{eqnarray*}
x_1[n]=e^{j\frac{\pi}{3} n} & \mapsto & y_1[n] = H(e^{j\frac{\pi}{3}}) \cdot e^{j\frac{\pi}{3} n} = 3 e^{-j\frac{\pi}{3}} \cdot e^{j\frac{\pi}{3} n} = \color{red}{3} e^{j(\frac{\pi}{3}n \color{blue}{- \frac{\pi}{3}})} \\
x_2[n] = e^{-j\frac{\pi}{3} n} & \mapsto & y_2[n] = H(e^{-j\frac{\pi}{3}}) \cdot e^{-j\frac{\pi}{3} n} = 3 e^{j\frac{\pi}{3}} \cdot e^{-j\frac{\pi}{3} n} = \color{red}{3} e^{-j(\frac{\pi}{3}n \color{blue}{- \frac{\pi}{3}})}
\end{eqnarray*}
By adding the two phasor components and dividing by 2, we obtain the given input signal:
$$
x[n]=\frac{1}{2} \left \{ x_1[n] + x_2[n] \right \} = \frac{1}{2} \left \{ e^{j\frac{\pi}{3}n} + e^{-j\frac{\pi}{3}n} \right \} = \cos (\frac{\pi}{3}n)
$$
Now because of the fact that an FIR filter is LTI, we can evaluate the output $y[n]$ by applying the same operations to the two individual output signals $y_1[n]$ and $y_2[n]$, thus:
$$
y[n] = \frac{1}{2} \left \{ y_1[n] + y_2[n] \right \}
$$
which results into:
\begin{eqnarray*}
x[n]=\frac{1}{2} \left \{ e^{j\frac{\pi}{3} n} + e^{-j\frac{\pi}{3} n} \right \} & \mapsto &
y[n]=\frac{1}{2} \left \{
\color{red}{3} e^{j(\frac{\pi}{3}n \color{blue}{- \frac{\pi}{3}})} + \color{red}{3} e^{-j(\frac{\pi}{3}n \color{blue}{- \frac{\pi}{3}})} \right \} \newline
\Rightarrow \hspace{2mm} x[n] = \cos (\frac{\pi}{3} n) & \mapsto & y[n]=
\color{red}{3} \cdot \cos (\frac{\pi}{3} n \color{blue}{- \frac{\pi}{3}})
\end{eqnarray*}
We can also obtain this result directly from the frequency response by evaluating the amplitude and phase of the frequency response for the input frequency $\theta= \frac{\pi}{3}$, as follows:
\begin{eqnarray*}
x[n] = \cos (\frac{\pi}{3} n) & \mapsto & y[n]=
 \color{red}{|H(e^{j\theta})\mid_{\theta=\frac{\pi}{3}}} \cdot \cos \left ( \frac{\pi}{3} n +
\color{blue}{\angle{H(e^{j\theta})\mid_{\theta=\frac{\pi}{3}}}} \right ) \\
& & = \color{red}{3} \cdot \cos (\frac{\pi}{3} n \color{blue}{- \frac{\pi}{3}})
\end{eqnarray*}
The result is depicted in the figure below.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/FIR/examplecosinout.svg"
      alt="Example response of FIR to sinusoidal signal with one frequency."
    />
    <figcaption>
      Example response of FIR to sinusoidal signal with one frequency.
    </figcaption>
  </figure>
</div>
</div>
</div>

<br></br>

## Superposition
Because an FIR filter is Time Invariant (LTI) system, we can use the superposition rule when an input signal consists of more than one frequency.
So let us assume the input signal of an FIR filter consists of a DC component and $N$ different frequencies as follows:
$$
x[n] = A_0 + \sum\_{k=1}^{N} A_k \cos ( \theta_k n + \phi_k).
$$
Furthermore the frequency response of an FIR is given by:
$$
H(e^{j\theta}) = |H(e^{j\theta})| e^{j\angle{H(e^{j\theta})}}
$$
Each of the individual frequencies $\theta_k$ of the input signal will 'trigger' the FIR filter only at frequency $\theta_k$. This implies that the amplitude $A_k$ of frequency $\theta_k$ is changed by $|H(e^{j\theta_k})|$ and the phase $\phi_k$ is changed by $\angle{H(e^{j\theta_k})}$. This results in the following output signal:
$$
y[n] = |H(e^{j0})| + \sum\_{k=1}^{N} |H(e^{j\theta_k})| A_k \cos (\theta_k n + \phi_k +
\angle{H(e^{j\theta_k})})
$$



<div class="example">
<h4> Example </h4>
<hr>
In this example we use the same FIR filter as in the previous example. Thus $h[n] = \delta[n] + 2 \delta[n-1] + \delta[n-2]$ and the frequency response is given by $H(e^{j\theta}) = 1 + 2 e^{-j\theta} + e^{-j2 \theta}$. Now, the input signal is given by the following frequencies: $x[n] = 1 + \frac{4}{3} \cos (\frac{\pi}{3} n) + 2 \cos(\frac{\pi}{2}n) + \cos(\pi n)$. Calculate the output signal $y[n]$.
<button class="collapsible">Show solution</button>
<div class="content">
Using superposition, we first calculate the response of the given FIR filter as a result of the individual frequency components of the input signal $x[n]$ and then we add the resulting outputs. With the individual frequency components $\theta =0, \pm \frac{\pi}{3}, \pm \frac{\pi}{2}$ and $\theta=\pm \pi$, this results in:
\begin{eqnarray*}
H(e^{j\theta})\mid_{\theta=0} &=& 4 \\
H(e^{j\theta})\mid_{\theta=\frac{\pi}{3}}= H^\ast(e^{j\theta})\mid_{\theta=-\frac{\pi}{3}}&=&
\color{red}{3 e^{-j\frac{\pi}{3}}} \\
H(e^{j\theta})\mid_{\theta=\frac{\pi}{2}}= H^\ast(e^{j\theta})\mid_{\theta=-\frac{\pi}{2}}&=&
\color{blue}{2 e^{-j\frac{\pi}{2}}} \\
H(e^{j\theta})\mid_{\theta=\pi}= H^\ast(e^{j\theta})\mid_{\theta=-\pi} &=& {\color{green}0}.
\end{eqnarray*}
Now the output becomes:
\begin{eqnarray*}
y[n] &=& 4 \cdot 1 + \color{red}{3} \cdot \frac{4}{3} \cos (\frac{\pi}{3}n \color{red}{- \frac{\pi}{3}})
+ \color{blue}{2} \cdot \cos(\frac{\pi}{2}n \color{blue}{- \frac{\pi}{2}})
+ {\color{green} 0} \cdot \cos(\pi n) \\
&=& 4 + 4 \cos (\frac{\pi}{3} n - \frac{\pi}{3}) + 4 \cos (\frac{\pi}{2} n - \frac{\pi}{2}).
\end{eqnarray*}
</div>
</div>
