+++
title = "Frequency response LTI"

# date = {{ .Date }}
lastmod = 2020-05-20

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Frequency response LTI"
  weight = 2
  parent = "Analysis II: Frequency response LTI"
+++


## Frequency-dependent input signals
From the previous module on <a href="../discretesignalprocessing_analysis_fir_main">FIR filters</a>, we have seen that the output $y[n]$ of a system with impulse response $h[n]$ driven by an input signal $x[n]$ can be determined using the convolution operator $\ast$ as
\begin{equation}\label{eq:outputconv}
    y[n] = x[n] \ast h[n] = h[n] \ast x[n] = \sum_{k=-\infty}^\infty h[k]x[n-k],
\end{equation}
where the convolution operator denotes the infinite sum of delayed input samples $x[n-k]$ weighted by the impulse response values $h[k]$.

In practice most signals contain multiple sinusoidal signals with different frequencies. A thorough understanding of the operations of a filter can be obtained by evaluating the output of a filter when applying a sinusoidal signal with arbitrary frequency. Suppose the input signal resembles a phasor with relative frequency $\theta$ as $x[n] = \mathrm{e}^{jn\theta}$. Using \eqref{eq:outputconv}, the output of a filter with impulse response $h[n]$ when driven by a phasor can be determined as
\begin{equation}
    \begin{split}
        y[n]
        &= \sum_{k=-\infty}^\infty h[k]x[n-k] \newline
        &= \sum_{k=-\infty}^\infty h[k]\mathrm{e}^{j(n-k)\theta} \newline
        &= \left( \sum_{k=-\infty}^\infty h[k]\mathrm{e}^{-jk\theta} \right) \ \mathrm{e}^{jn\theta} \newline
        &= H(\mathrm{e}^{j\theta}) \mathrm{e}^{jn\theta}.
    \end{split}\label{eq:outputphasor}
\end{equation}
The impact and consequences of this derivation are the main learning goal of this entire module. So, what have we shown? If an LTI system with impulse response $h[n]$ is driven by a phasor with relative frequency $\theta$, the output is a weighted version of the input signal. This weight is denoted in \eqref{eq:outputphasor} by the so-called frequency response $H(\mathrm{e}^{j\theta})$. This complex weight is frequency dependent and therefore different frequencies are affected to a different extent. The linearity property of LTI systems allows for simple calculations of the filter output when dealing with sums of sinusoidal signals with different frequencies.

<br></br>
## Frequency response using the FTD
From its definition in \eqref{eq:outputphasor} the frequency response is defined as
\begin{equation}\label{eq:FTDhH}
    H(\mathrm{e}^{j\theta}) = \sum_{n=-\infty}^\infty h[n] \mathrm{e}^{-jn\theta}.
\end{equation}
By comparison with the Fourier transform for discrete-time systems (FTD), we can concluded that the frequency response is the FTD pair of the impulse response. Similarly, we can conclude that the impulse response is then the IFTD pair of the frequency response as
\begin{equation}\label{eq:IFTDHh}
    h[n] = \frac{1}{2\pi}\int_{-\pi}^\pi H(\mathrm{e}^{j\theta})\mathrm{e}^{jn\theta} \mathrm{d}\theta.
\end{equation}


<br></br>
## Properties
The frequency response $H(\mathrm{e}^{j\theta})$ has interesting properties that often can be used to simplify analysis. This subsection will describe the most important properties of the frequency response to allow for easy calculations.

### Complex-valued
Since the frequency response $H(\mathrm{e}^{j\theta})$ is the FTD pair of the impulse response, it is at the same time complex-valued. In polar notation the frequency response can be written as
\begin{equation} \label{eq:propcomplex}
    H(\mathrm{e}^{j\theta}) = \vert H(\mathrm{e}^{j\theta}) \vert \mathrm{e}^{j\angle H(\mathrm{e}^{j\theta})},
\end{equation}
where $\vert H(\mathrm{e}^{j\theta}) \vert$ represents the amplitude of the frequency response and is commonly known as the magnitude response. Furthermore, $\angle H(\mathrm{e}^{j\theta})$ represents the phase angle of the frequency response, which is commonly known as the phase response.

### Periodicity
The frequency response is periodic over $\theta$ with period $2\pi$ as
\begin{equation}
    H(\mathrm{e}^{j\theta}) = H(\mathrm{e}^{j(\theta+k\cdot 2\pi)}),
\end{equation}
where $k$ is an integer. The periodicity in the frequency response is caused by the periodicity of the phasor $\mathrm{e}^{j\theta}$, since $\mathrm{e}^{j(\theta+k\cdot 2\pi)} = \mathrm{e}^{j\theta}(\mathrm{e}^{j2\pi})^k = \mathrm{e}^{j\theta}\cdot 1^k = \mathrm{e}^{j\theta}$.

### Conjugate symmetry
In the case that the impulse response $h[n]$ is real valued, the frequency response is a complex conjugated function of its relative frequency as
\begin{equation}
    H(\mathrm{e}^{-j\theta}) = H^\ast (\mathrm{e}^{j\theta}).
\end{equation}
This implies that the magnitude of the frequency response is an even function, i.e. $\vert H(\mathrm{e}^{j\theta}) \vert = \vert H(\mathrm{e}^{-j\theta}) \vert$ , and its phase is an odd function of frequency $\angle H(\mathrm{e}^{j\theta}) = - \angle H(\mathrm{e}^{-j\theta})$.

### Convolution
Similar as in the module on the FTD, convolution in the time-domain can be performed as a multiplication in the frequency domain as
\begin{equation}\label{eq:convprop}
    y[n] = x[n] \ast h[n] \qquad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \qquad Y(\mathrm{e}^{j\theta}) = X(\mathrm{e}^{j\theta}) \cdot H(\mathrm{e}^{j\theta}).
\end{equation}

The first step of the proof is to use the expression for the convolution sum between $x[n]$ and $h[n]$:
\begin{equation}
    \mathcal{F} \left\\{ x[n] \ast h[n] \right\\} = \sum_{n=-\infty}^{\infty} \left( \sum_{p=-\infty}^{\infty} x[p] h[n-p] \right) \mathrm{e}^{-jn \theta}
\end{equation}
Then we can interchange the two summations and multiply in the first summation the samples $x[p]$ with $\mathrm{e}^{-jp \theta}$, which has to be compensated in the second summation by $\mathrm{e}^{jp \theta}$:
\begin{equation}
    \mathcal{F} \left\\{ x[n] \ast h[n] \right\\} =
    \sum_{p=-\infty}^{\infty} x[p] \mathrm{e}^{-jp \theta} \cdot \left( \sum_{n=-\infty}^{\infty}h[n-p]  \mathrm{e}^{-j(n-p) \theta} \right)
\end{equation}
As a final step we substitute a new variable $m=n-p$ and since both variables $n$ and $p$ range from minus to plus infinity, this implies that the new variable also ranges from minus to plus infinity:
\begin{equation}
    \mathcal{F} \left\\{ x[n] \ast h[n] \right\\}
\overset{m= n-p}{=} \sum_{p=-\infty}^{\infty} x[p] \mathrm{e}^{-jp \theta} \cdot \left( \sum_{m=-\infty}^{\infty}h[m]  \mathrm{e}^{-jm \theta} \right)
= X(\mathrm{e}^{j\theta}) \cdot H(\mathrm{e}^{j\theta})
\end{equation}
which finalizes the proof.

<br></br>
## Frequency response from impulse response
The frequency response can be determined easily from the impulse response from the definition of \eqref{eq:FTDhH}. This approach will be explained through the following example.


<div class="example">
<h4> Example </h4>
<hr>
For the system with impulse response
\begin{equation}
    h[n] = \delta[n-1] + \delta[n-2] + \delta[n-3],
\end{equation}
determine the analytical expression of the frequency response and draw the corresponding magnitude and phase plots.
<br>
<button class="collapsible">Show solution</button>
<div class="content">
By using the shift property of the FTD and the definition of the frequency response from \eqref{eq:FTDhH} the frequency response can be determined as
\begin{equation}
    H(e^{j\theta}) = \mathrm{e}^{-j\theta} + \mathrm{e}^{-j2\theta} + \mathrm{e}^{-j3\theta}.
\end{equation}
By taking the center term $\mathrm{e}^{-j2\theta}$ out of brackets, an expression similar to \eqref{eq:propcomplex} is obtained as
\begin{equation}
    H(\mathrm{e}^{j\theta}) = (\mathrm{e}^{j\theta} + 1 + \mathrm{e}^{-j\theta})\mathrm{e}^{-j2\theta},
\end{equation}
which can be simplified using the Euler equations as
\begin{equation}\label{eq:H_unnorm}
    H(\mathrm{e}^{j\theta}) = (1+2\cos(\theta))\mathrm{e}^{-j2\theta}.
\end{equation}
Here the resemblance with \eqref{eq:propcomplex} should become apparent. By regarding the frequency response as a complex vector, the term within brackets can be regarded as the length of this complex vector, which can become negative in this case, and the real part of the power of the complex exponential represents the phase. Plotting these two parts would result in the two graphs of the figure below. The angle of the second term of \eqref{eq:propcomplex} is limited to the domain $[-\pi, \pi)$ to account for the periodicity in the phase.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/LTI/example_freq1_unnorm.svg"
      alt="Visual representation of equation \eqref{eq:H_unnorm}."
    />
    <figcaption>
      Visual representation of equation \eqref{eq:H_unnorm}.
    </figcaption>
  </figure>
</div>
However, still issues remain with this visualization and therefore these plots cannot be called the true magnitude and phase response of $H(\mathrm{e}^{j\theta})$. Comparison with \eqref{eq:propcomplex} will show that the first term in \eqref{eq:H_unnorm} is not always non-negative. In order to convert the first term in \eqref{eq:propcomplex} to a function that is always non-negative, the negative parts of this first term should be multiplied with $-1$. In order to compensate for this multiplication, we can add (or subtract) $\pi$ from the phase at the locations where this multiplication is required, i.e. at the zero-crossings. These "phase jump" of $\pi$ can be explained by the fact that $-1 = \mathrm{e}^{\pm j\pi}$. The correct magnitude and phase response plots are shown in the following figure.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/LTI/example_freq1.svg"
      alt="Magnitude and phase response of equation \eqref{eq:H_unnorm}."
    />
    <figcaption>
      Magnitude and phase response of equation \eqref{eq:H_unnorm}.
    </figcaption>
  </figure>
</div>
</div>
</div>



<br></br>
## Frequency response from the difference equation
Another way of calculating the frequency response is through the use of the difference equation. This method turns out to be particularly useful when dealing with IIR systems. This approach will be explained through the following example.

<div class="example">
<h4> Example </h4>
<hr>
Calculate the frequency response of a first-order auto-regressive filter with difference equation
\begin{equation}
    y[n] = x[n] + \alpha y[n-1],
\end{equation}
where $\vert \alpha \vert < 1$ and $y[n] = 0$ for $n<0$.
<br>
<button class="collapsible">Show solution</button>
<div class="content">

The frequency response can be determined from the difference equation by first calculating the FTD of both the left and right side of the difference equation by making use of the shift property of the FTD. This leads to
\begin{equation}
    Y(\mathrm{e}^{j\theta}) = X(\mathrm{e}^{j\theta}) + \alpha Y(\mathrm{e}^{j\theta}) e^{-j\theta}.
\end{equation}
The frequency response can be determined by first rearranging the terms, such that terms $X(\mathrm{e}^{j\theta})$ and $Y(\mathrm{e}^{j\theta})$ are both on the opposite side of the equality sign as
\begin{equation}
    Y(\mathrm{e}^{j\theta})(1-\alpha \mathrm{e}^{-j\theta}) = X(\mathrm{e}^{j\theta}).
\end{equation}
Using \eqref{eq:convprop}, the frequency response can then be determined as
\begin{equation}\label{eq:example:alpha}
    H(\mathrm{e}^{j\theta}) = \frac{Y(\mathrm{e}^{j\theta})}{X(\mathrm{e}^{j\theta})} = \frac{1}{1-\alpha \mathrm{e}^{-j\theta}}.
\end{equation}
The figure below shows several magnitude and frequency responses for different values of $\alpha$.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/LTI/example_alpha.svg"
      alt="Magnitude and phase response of \eqref{eq:example:alpha} for different values of $\alpha$."
    />
    <figcaption>
      Magnitude and phase response of \eqref{eq:example:alpha} for different values of $\alpha$.
    </figcaption>
  </figure>
</div>
</div>
</div>

<br></br>
## Impulse response from difference equation
Through the use of the FTD pairs and the convolution property, the impulse response can be modelled from the input and output signal. Instead of directly trying to solve
\begin{equation}
    y[n] = x[n] \ast h[n]
\end{equation}
for $h[n]$, the problem is transformed to the frequency domain for easier analysis. This procedure is as follows. The difference equatio can be transformed to the frequency domain through the FTD, under the assumption that the initial conditions are zero. Here the shift-property of the FTD is crucial. By calculating the FTD of both sides of the difference equation, the following equality
\begin{equation}
        Y(\mathrm{e}^{j\theta}) = \sum_{k=0}^{M-1} b_k X(\mathrm{e}^{j\theta})e^{-jk\theta} + \sum_{k=1}^{N-1} a_k Y(\mathrm{e}^{j\theta})e^{-jk\theta}
\end{equation}
is obtained. By rearranging the term we obtain
\begin{equation}
    Y(\mathrm{e}^{j\theta}) \left(1-\sum_{k=1}^{N-1}a_k \mathrm{e}^{-jk\theta}\right) = X(\mathrm{e}^{j\theta})\left(\sum_{k=0}^{M-1}b_k \mathrm{e}^{-jk\theta}\right).
\end{equation}
By using the convolution property from \eqref{eq:convprop}, the frequency response can be determined as
\begin{equation}
    H(\mathrm{e}^{j\theta}) = \frac{Y(\mathrm{e}^{j\theta})}{X(\mathrm{e}^{j\theta})} = \frac{\sum_{k=0}^{M-1}b_k  \mathrm{e}^{-jk\theta}}{1-\sum_{k=1}^{N-1}a_k\mathrm{e}^{-jk\theta}} = \frac{B(\mathrm{e}^{j\theta})}{A(\mathrm{e}^{j\theta})}.
\end{equation}
Finally, through \eqref{eq:IFTDHh} the impulse response can be determined as the IFTD from $H(\mathrm{e}^{j\theta})$.
