+++
title = "Frequency response"

# date = {{ .Date }}
lastmod = 2019-10-13

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Frequency response of finite impulse response filters"
  weight = 61
  parent = "Transform analysis of discrete-time systems"

+++


## Frequency response FIR
Besides the impulse response, denoted by $h[n]$, and the Difference Equation (DE) we will see that the frequency response is an alternative description of an FIR filter. Obviously all these different descriptions are related to each other and each of the descriptions has its own advantage. The advantage of the frequency response description is that we can fairly easily see the response of the FIR to frequencies.

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

<br></br>

## Properties Frequency Response
In the previous section, we found the following relation between the impulse response description in time domain $h[n]$ and the frequency response description in frequency domain $H(e^{j\theta})$:
$$
\boxed{
\begin{eqnarray}
\text{Time domain} & \circ  \hspace{-2.3mm} - \hspace{-1.1mm}  \circ & \text{Frequency domain} \newline
h[n]= \sum\_{k=0}^{M-1} h[k] \delta[n-k] & \circ  \hspace{-2.3mm} - \hspace{-1.1mm}  \circ &
H(e^{j\theta})= \sum\_{k=0}^{M-1} h[k] e^{-j\theta k}
\end{eqnarray} }
$$

The first important property of the Frequency response $H(e^{j\theta})$, is that it is a periodic function with period $2 \pi$. This can be verified by adding an integer number $l$ times $2\pi$ to the frequency $\theta$, which result into:
\begin{eqnarray}
H(e^{j(\theta + l \cdot 2 \pi)})&=& \sum\_{k=0}^{M-1} h[k] e^{-j(\theta   + l \cdot 2 \pi )\cdot k} =
\sum\_{k=0}^{M-1} h[k] e^{-j\theta k } \cdot e^{-jl \cdot k \cdot 2 \pi} \newline
&=& \sum\_{k=0}^{M-1} h[k] e^{-j\theta k } \cdot 1 = H(e^{j\theta}).
\end{eqnarray}
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
\begin{eqnarray}
\text{Periodic } & : & H(e^{j\theta})  =  H(e^{j(\theta + l \cdot 2 \pi}) \newline
\text{Complex conjugated } & : & H(e^{-j\theta})  = (H(e^{j\theta}))^\ast
\end{eqnarray} }
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
\begin{equation}
H(e^{j\theta}) = |H(e^{j\theta})| \cdot e^{j\angle{H(e^{j\theta})}}.
\end{equation}
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
\begin{eqnarray}
H(e^{j\theta}) &=& \frac{1}{L} \sum\_{k=0}^{L-1} e^{-jk \theta} = \frac{1}{L} \frac{1 - e^{-jL \theta}}{1 - e^{-j\theta}} = \frac{1}{L} \frac{e^{jL \frac{\theta}{2}} - e^{-jL \frac{\theta}{2}}}{e^{j\frac{\theta}{2}} - e^{-j\frac{\theta}{2}}} \cdot \frac{e^{-jL \frac{\theta}{2}}}{e^{-j\frac{\theta}{2}}} \newline
&=& \color{red}{\frac{\sin (L \frac{\theta}{2})}{L \sin (\frac{\theta}{2})}} \cdot
e^{-j\color{blue}{(L-1) \frac{\theta}{2}}}
\end{eqnarray}
$$
Thus the magnitude- and phase-response of a moving average filter are given by the following expressions:
\begin{eqnarray}
|H(e^{j\theta})| &=& \left | \color{red}{\frac{\sin (L \frac{\theta}{2})}{L \sin (\frac{\theta}{2})}}
\right | \newline
\angle{H(e^{j\theta})} &=& \color{blue}{-(L-1) \frac{\theta}{2}}.
\end{eqnarray}
An important value of the magnitude-response is the value for $\theta=0$. This value can be found  by approximate the sin-functions by the first component of its taylor expansion, meaning that for small values of $x$ the value of $\sin(x)$ can be approximated by its first term of the geometric series: $\sin(x) = x - \frac{x^3}{3!} + \frac{x^5}{5!} + \cdots$. Thus for small values of $x$ we can approximate the fraction $\frac{\sin(L x)}{L sin(x)}$ by $\frac{(L x)}{L (x)} =1 $.
\begin{eqnarray}
\frac{\sin (L \frac{\theta}{2})}{L \sin (\frac{\theta}{2})}\mid\_{\theta=0} &=& \lim_{\theta \rightarrow 0} \left\\{ \frac{\sin(L \theta)}{L \sin(\theta)} \right\\} = 1 .
\end{eqnarray}
The other important values of the phase-response are the zero-crossings, because at these frequencies we will find phase jumps of $\pm \pi$ in the phase-response plot.
These zero-crossing can be found for those frequencies for which $|H(e^{j\theta})|$ is zero. Because the frequency of the numerator of $|H(e^{j\theta})|$ increases $L$ times faster than the frequency of the denominator, we can find these zero crossings by evaluating those frequencies for which the numerator is zero. Besides $\theta=0$ these values can be found as follows:
\begin{eqnarray}
\sin (L \frac{\theta}{2}) = 0 & \Leftrightarrow & L \frac{\theta}{2} = k \pi \quad \Rightarrow \quad \theta=\frac{2\pi}{L} .
\end{eqnarray}
An example is shown in Fig. 5, which is the graphical representation of the magnitude- and phase-response of an 11-point averaging filter.

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

Now let us see how this works when we use the frequency responses $H_1(e^{j\theta})$ and $H_2(e^{j\theta})$ of the two FIR filters. This is depicted in Fig. 6.

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


Fig. 7 shows the transient-region (in red samples) and steady- state region when we apply the signal $x[n]= \cos(\frac{\pi}{3}n) \cdot u[n]$ to an FIR filter with impulse response $h[k] = \delta[n] + 2 \delta[n-1] + \delta[n-2]$.

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
In practice we often filter a continuous-time signal in the discrete-time domain as depicted in Fig. 8. The main motivations for this, is that the implementation in discrete-time domain is much more flexible and cheaper compared to the implementation in the continuous-time domain.

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


<br></br>

## Exercises
In this section several exercises are available, including their answers. The exercises marked in <span style="color:blue">*blue*</span> are explained by means of more extensive pencast videos.

### Video quiz

<div class="example">
<button class="collapsible">Test your knowledge (click to expand)</button>
<div class="content">
<button class="collapsible">Question 1</button>
<div class="content">
<div class="scp-quizzes-data quiz">
   The input signal is $x[n] = \cos(0.5\pi n)$. This signal is applied to a filter with impulse response $h[n]$ and frequency response $H(e^{j\theta}) = 2\sin(\theta)$. Give a description of the output signal $y[n]$.
</br>
    <input type="radio" name="question1">
       <label>$y[n] = 0$</label><br/>
    <input type="radio" name="question1">
        <label>$y[n] = 2$</label><br/>
    <input type="radio"  id="answer1" name="question1">
        <label for="answer1">$y[n] = 2\cos(0.5\pi n)$</label><br/>
    <input type="radio"  name="question1">       
        <label>$y[n] = 2\cos(0.5\pi n + 0.5\pi)$</label><br/>
    <input type="radio"  name="question1">
        <label>None of the answers is correct.</label><br/>
 </div>
 </div>
 <br>
<button class="collapsible">Question 2</button>
<div class="content">
<div class="scp-quizzes-data quiz">
    Have a look at the following system: <br>
    <div style="max-width: 600px; margin: auto">
      <figure>
        <img
          src="/../files/7.Images/discrete/analysis/FIR/quiz/question2.PNG"
          alt="FIR filter, question 2."
        />
      </figure>
    </div>
    Signal $x[n]$ consists out of two frequencies $\theta_1 = \frac{\pi}{3}$ and $\theta_2=\pi$. Which frequencies does the output signal $y[n]$ contain?  
<br>
</br>
    <input type="radio" name="question2">
      <label>Both frequencies remain.</label><br/>
    <input type="radio" name="question2">
      <label>Both frequencies get cancelled out.</label><br/>
    <input type="radio" id="answer2" name="question2">
      <label for="answer2">Only $\theta=\frac{\pi}{3}$ remains.</label><br/>    
    <input type="radio"  name="question2">
      <label>Only $\theta=\pi$ remains.</label><br/>
    <input type="radio" name="question2">
      <label>None of the answers is correct.</label><br/>
 </div>
</div>
<br>
<button class="collapsible">Question 3</button>
<div class="content">
<div class="scp-quizzes-data quiz">
    What is the response of the following filter to a DC signal?
    <div style="max-width: 600px; margin: auto">
      <figure>
        <img
          src="/../files/7.Images/discrete/analysis/FIR/quiz/question3.PNG"
          alt="FIR filter, question 3."
        />
      </figure>
    </div>
<br>
</br>
    <input type="radio"  name="question3">
      <label>The DC signal remains the unchanged.</label><br/>
    <input type="radio" id="answer3"  name="question3">
      <label for="answer3">The DC signal gets filtered out.</label><br/>
    <input type="radio"  name="question3">
      <label>The DC signal gets doubled.</label><br/>
 </div>
</div>
<br>
<button class="collapsible">Question 4</button>
<div class="content">
<div class="scp-quizzes-data quiz">
    What is the response of the following cascaded filters to a DC signal?
    <div style="max-width: 600px; margin: auto">
      <figure>
        <img
          src="/../files/7.Images/discrete/analysis/FIR/quiz/question4.PNG"
          alt="cascaded FIR filter, question 4."
        />
      </figure>
    </div>
<br>
</br>
<input type="radio"  name="question4">
  <label>The DC signal remains the unchanged.</label><br/>
<input type="radio" id="answer4"  name="question4">
  <label for="answer4">The DC signal gets filtered out.</label><br/>
<input type="radio"  name="question4">
  <label>The DC signal gets doubled.</label><br/>
  <input type="radio"  name="question4">
    <label>The DC signal gets tripled.</label><br/>
 </div>
</div>
<br>
<button class="collapsible">Question 5</button>
<div class="content">
<div class="scp-quizzes-data quiz">
    What is does the system with the following phase response represent?
    <div style="max-width: 600px; margin: auto">
      <figure>
        <img
          src="/../files/7.Images/discrete/analysis/FIR/quiz/question5.PNG"
          alt="Phase response, question 5."
        />
      </figure>
    </div>
<br>
</br>
    <input type="radio" name="question5">
       <label>Delay by 2/3 samples.</label><br/>
    <input type="radio"  name="question5">
        <label>Delay by 2 samples.</label><br/>
    <input type="radio"  id="answer5" name="question5">
       <label for="answer5">Delay by 3 samples.</label><br/>
   <input type="radio"  name="question5">
      <label>Saw tooth</label><br/>
   <input type="radio" name="question5">
      <label>None of the answers is correct.</label><br/>
 </div>
</div>
<br>
</div>
</div>


### Exercise bundle

<object data="/../files/3.Exercises/5.FREQ-exercises.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/3.Exercises/5.FREQ-exercises.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/3.Exercises/5.FREQ-exercises.pdf">Download PDF</a>.</p>
    </embed>
</object>

### Answers
Download the answers <a href="/../files/3.Exercises/Answers/5.FREQ-answers.pdf">here</a>.

### Pencast videos
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/videoseries?list=PL2LT3LoI-pPHIiIx4l49DwPs8v4f0wptO" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

_The above video player contains a playlist of all pencast videos which can be expanded by clicking the playlist icon in the upper-right corner._

<br></br>

## MATLAB lab
Accompanied to this modules are some exercises in MATLAB, which will test your knowledge of the module and will help improve your MATLAB skills.

### Lab assignment
<object data="/../files/10.Matlab/Lab 6 - Frequency Response.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/10.Matlab/Lab 6 - Frequency Response.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/10.Matlab/Lab 6 - Frequency Response.pdf">Download PDF</a>.</p>
    </embed>
</object>

### MATLAB demo
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/7oas6xLIYhc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>

## Summary frequency response of FIR filters

<b><u> Relationship impulse response and frequency response:</u></b>
$$
\boxed{
\begin{eqnarray}
\text{Time domain} & \circ  \hspace{-2.3mm} - \hspace{-1.1mm}  \circ & \text{Frequency domain} \newline
h[n]= \sum\_{k=0}^{M-1} h[k] \delta[n-k] & \circ  \hspace{-2.3mm} - \hspace{-1.1mm}  \circ &
H(e^{j{\theta}})= \sum\_{k=0}^{M-1} h[k] e^{-j{\theta k}}   
\end{eqnarray}
}
$$

<br>
<b><u> Basic FIR property: </u></b>
<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>When applying a sinusoidal signal with a single frequency $\theta=\theta_1$ to an FIR filter, the output is a sinusoidal signal with the same frequency $\theta_1$ as the input signal, only the amplitude and phase have changed. The change in amplitude is described by the magnitude response evaluated at frequency $\theta_1$, thus $|H(e^{j{\theta}})\mid_{\theta=\theta_1}$, while the change in phase is described by the phase response evaluated at frequency $\theta_1$, thus $\angle{H(e^{j{\theta}})}\mid_{\theta=\theta_1}$.</i></div>

<br>
When applying a sum of frequencies $x[n] = A_0 + \sum_{k=1}^{N} A_k \cos ( \theta_k n + \phi_k)$ to an FIR filter with frequency response $H(e^{j{\theta}}) = |H(e^{j\theta})| e^{j{\angle{H(e^{j{\theta}})}}}$ then the output can be written as follows:
$$
y[n] = |H(e^{j0})| + \sum_{k=1}^{N} |H(e^{j\theta_k})| A_k \cos (\theta_k n + \phi_k +
\angle{H(e^{j\theta_k})})
$$


<br>
<b><u> Properties frequency response </u></b>
$$
\boxed{
\begin{eqnarray}
\text{Periodic } & : & H(e^{j\theta})  =  H(e^{j(\theta + l \cdot 2 \pi)}) \newline
\text{Complex conjugated } & : & H(e^{-j\theta})  = (H(e^{j\theta}))^\ast
\end{eqnarray}
}
$$

<br>
<b><u> Graphical representation: </u></b>
<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i><ul><li>Both Magnitude- and phase- response are depicted in the Fundamental Interval (FI): $|\theta| \leq \pi$.</li><li>The phase response is depicted in the range $|\angle{H(e^{j\theta})}| \leq \pi$.</li><li>A phase jump of $\pm \pi$ is applied in the phase response plot for each zero crossing of the magnitude response.</li></ul></i></div>



<br>
<b><u> Cascading FIR filters: </u></b>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>When cascading two different FIR filters, one with frequency response $H_1(e^{j\theta})$ and the other with frequency response $H_2(e^{j\theta})$, we may combine these two FIR filters to one FIR filter of which the frequency response is given by the product of the individual frequency responses: $H(e^{j\theta})= H_1(e^{j\theta}) \cdot H_2(e^{j\theta})$.
</i></div>

<br>
<b><u> Convolution in time- is equivalent to multiplication in frequency-domain: </u></b>
$$
\boxed{
h_1[n] * h_2[n] \hspace{3mm} \circ  \hspace{-2.3mm} - \hspace{-1.1mm}  \circ \hspace{3mm} H_1(e^{j\theta}) \cdot H_2(e^{j\theta})
}
$$

<br>
<b><u> Steady state and transient behaviour: </u></b>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i><ul><li><b> Transient region:</b> The complex multiplier $\left ( \sum_{k=0}^{{\color{red}{n}}} h[k] e^{-j\theta_1 k} \right )$ depends on the index $n$.</li><li><b>Steady state region:</b> The complex multiplier $\sum_{k=0}^{{\color{blue}{M-1}}} h[k] e^{-j\theta_1 k}$ is constant. Output contains only input frequency ($\theta_1$ in this example).</li><li>If for $n > M-1$ the input changes to zero or to another frequency $\theta_2 \neq \theta_1$, then there will be a new transition- and steady state- region.</li></ul></i></div>
