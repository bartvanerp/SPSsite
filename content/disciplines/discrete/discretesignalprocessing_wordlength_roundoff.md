+++
title = "Analysis of round-off noise"

# date = {{ .Date }}
lastmod = 2020-06-13

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Analysis of round-off noise"
  weight = 3
  parent ="Finite word length effects"

+++

The first processing step of a digital system in which we are dealing with quantization is the conversion of an analog into a digital signal. Besides the ideal C-to-D conversion from continuous time to discrete time samples $x[n]$ we quantize these samples into samples $\hat{x}[n]$,
as depicted in Fig. 1.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/finitewordlength/rounding.svg"
      alt="Error calculation of rounding a signal."
    />
    <figcaption class="numbered">
      Error calculation of rounding a signal.
    </figcaption>
  </figure>
</div>
For simplicity reasons we assume rounding for this quantization step with no overflow. The samples are numbers without a decimal fraction which are represented by $B$ bits. With quantization step $q$ we have:
$$
|\hat{x}[n]| < q \cdot 2^{B-1} \hspace{3mm} \mbox{and} \hspace{3mm}
|\hat{x}[n]-x[n]|=|e[n] < \frac{q}{2}
$$
The Signal to Noise Ratio (SNR) is defined as the power of $x[n]$ divided by the power of the error signal $e[n]$: $P_x/P_e$.  In order to overcome overflow we usually limit $|x[n]|$ to be much smaller than the maximum allowable absolute value of the quantized signal $\hat{x}[n]$. This can be achieved by multiplying signal $x[n]$ with a constant factor $K$ which is much smaller than 1. In practice the value $K = 1/4$ is often chosen.
With this $P_x$ is as follows:
$$
P_x= \left ( K \cdot q \cdot 2^{B-1} \right )^2
\hspace{2mm} \mbox{(typically} \hspace{2mm} K=1/4\mbox{)}
$$
The assumption made to evaluate the error power $P_e$ is that the error can be treated as a random variable which is uniformly distributed in the range $-q/2$ until $+q/2$ with probability $1/q$  which results in the following error power $P_e$:
$$
P_e = \int_{-\infty}^{\infty} e^2 \cdot \mbox{Prob}\{e\} d e = \int_{-q/2}^{q/2} e^2 \cdot \frac{1}{q} d e = q^2 / 12
$$
Together with $K=1/4$ the SNR becomes:
$$
\frac{P_x}{P_e} = \frac{3}{16} 2^{2B} \hspace{2mm} \rightarrow \hspace{2mm}
10 \cdot ^{10}\mbox{log} \left ( \frac{P_x}{P_e} \right ) \hat{=}  \color{red}{6  B} \mbox{[dB]}
$$
which implies that the SNR is linearly related to the used number of bits $B$. A practical rule of thumb is that the Signal to noise ratio $P_x/P_e$ improves 6 [dB] for each extra bit that we use to represent $x[n]$ by its quantized value $\hat{x}[n]$. For example a 16 bit representation of a signal $x[n]$ has a signal to noise ratio of approximately 96 [dB].

<br></br>
## Influence filtering of round-off noise
The influence of round-off noise when it propagates through a filter
can be analysed by using the model as depicted in Fig. 2.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/finitewordlength/noisemodel.svg"
      alt="Filtering of round-off noise."
    />
    <figcaption class="numbered">
      Filtering of round-off noise.
    </figcaption>
  </figure>
</div>
From this figure it follows that in case of an LTI filter with impulse response $h[n]$, the output $y[n]$ can be written as an sum of two components:
\begin{eqnarray}
y[n]&=& \hat{e}[n] \star h[n] =(x[n]+e[n]) \star h[n] \newline
&=& x[n] \star h[n] + e[n] \star h[n] = v[n] + g[n]
\end{eqnarray}
Signal $v[n]$ is the result of filtering $x[n]$ with filter $h[n]$ and Signal $g[n]$ is the result of filtering the quantization error $e[n]$ with filter $h[n]$.  Together with the fact that the spectra of signal $x$ and quantization error $e$ will be different it follows that the filter $h[n]$ influences the signal to noise ratio:
$$
\frac{P_x}{P_e} \neq \frac{P_v}{P_g} \hspace{3mm} \Leftrightarrow
\mbox{ SNR$_{in}$ $\neq$ SNR$_{out}$}
$$

<br></br>
## Pairing and ordering
Finally it can be noted that for a filter that is implemented in cascade or parallel form, there is a considerable flexibility in terms of selecting which poles are paired with which zeros and in selecting the order in which the sections are to be cascaded for a cascade structure. Pairing and ordering may have a significant effect on the shape of the output noise power. The rules of thumb that are generally followed for pairing and ordering are as follows:
<ul>
  <li> The pole that is closest to the unit circle is paired with the zero that is closest to it in the $Z$-plane, and this pairing is continued until all poles and zeros have been paired.</li>
  <li>  The resulting second order sections are then ordered in cascade realization according to how close the poles are with respect to the unit circle. The ordering may be done either in terms of increasing or decreasing closeness to the unit circle. Which ordering is used depends on different number of factors, including the shape of the output noise. </li>
</ul>
