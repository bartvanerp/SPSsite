+++
title = "Special cases"

# date = {{ .Date }}
lastmod = 2020-05-18

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Special cases"
  weight = 4
  parent = "Analysis II: Frequency response LTI"
+++


This section will discuss two special cases which commonly occur in real-time applications. These special cases include an averaging filter and a low-pass filter.

<br></br>
## Averaging filter
An averaging filter is used to average over several values of the input signal, as the name suggests. Fig. 1 shows the flow diagram and impulse response of an average filter of length $N$. It should be noted that the normalization factor $1/N$ is omitted in the coefficients for simplicity.

The difference equation of an averaging filter can be determined from the flow diagram as
\begin{equation}
    y[n] = \sum_{k=0}^{N-1} b_k x[n-k] = \sum_{k=0}^{N-1} x[n-k].
\end{equation}
Evaluation of the difference response for an Dirac delta pulse as input leads to the impulse response
\begin{equation}
    h[n] = \sum_{k=0}^{N-1} \delta[n-k] = u[n] - u[n-N],
\end{equation}
where $u[n]$ represents the unit step function. This can be understood as regarding the impulse response as a finite block signal, which can be represented as an unit step function that is cancelled from sample $N$ onward by an $N$-delayed unit step function.

The frequency response can be determined from the impulse response using the FTD, where we make extensive use of the shift property, as
\begin{equation}
    H(e
    \mathrm{e}^{j\theta}) = \sum_{k=0}^{N-1} \mathrm{e}^{-jk\theta}.
\end{equation}
By using the equation of the sum of a geometric series, we are allowed to write this expression as
\begin{equation}
    H(\mathrm{e}^{j\theta})= \frac{1-\mathrm{e}^{-jN\theta}}{1-\mathrm{e}^{-j\theta}}.
\end{equation}
By taking out the center term in both the numerator and denominator and by multiplying by $1$ as $\frac{1/2j}{1/2j}$, we obtain
\begin{equation}
    H(\mathrm{e}^{j\theta}) = \frac{(\mathrm{e}^{j\frac{N}{2}\theta} - \mathrm{e}^{-j\frac{N}{2}\theta})/2j }{(\mathrm{e}^{j\frac{1}{2}\theta} - \mathrm{e}^{-j\frac{1}{2}\theta})/2j} \cdot \frac{\mathrm{e}^{-j\frac{N}{2}\theta}}{\mathrm{e}^{-j\frac{1}{2}\theta}}.
\end{equation}
Simplification of this expression by using the Euler equations, we finally obtain
\begin{equation}
    H(\mathrm{e}^{j\theta}) = \frac{\sin\left(\frac{N}{2}\theta\right)}{\sin\left(\frac{1}{2}\theta\right)} \mathrm{e}^{-j\left(\frac{N-1}{2}\right)\theta}.
\end{equation}
Fig. 2 shows the corresponding magnitude and phase response for different values of $N$.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/LTI/average_filter.svg"
      alt="Flow diagram and impulse response of an average filter of length $N$ without normalization factor $1/N$."
    />
    <figcaption class="numbered">
      Flow diagram and impulse response of an average filter of length $N$ without normalization factor $1/N$.
    </figcaption>
  </figure>
</div>
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/LTI/averagingfilter.svg"
      alt="Magnitude and phase response of an averaging filter of length $N$."
    />
    <figcaption class="numbered">
      Magnitude and phase response of an averaging filter of length $N$.
    </figcaption>
  </figure>
</div>



<br></br>
## Low-pass filter
The function of an ideal low-pass filter is to block out all frequency above a certain threshold $\theta_c$ and to leave all other frequencies in tact. The ideal frequency response can therefore be written as
\begin{equation}
    H(e^{j\theta}) =
    \begin{cases}
        1, & \text{for } \vert \theta \vert \leq \theta_c, \newline
        0, & \text{otherwise},
    \end{cases}
\end{equation}
which represents a block function.

From the common Fourier pairs, we can conclude that the impulse response is given by
\begin{equation}
    h[n] = \frac{\theta_c}{\pi}\left( \frac{\sin(\theta_c n)}{\theta_c n} \right).
\end{equation}
Although this impulse response could be determined analytically, two issues remain. The original impulse and frequency response and the consequences of the transformations that we will apply in order to get rid of these issues are shown in Fig. 3.

First is the fact that this sinc-function is infinitely long. For practical implementations, the function should be cropped. This cropping is possible by multiplying the impulse response function by a block wave. In the frequency domain, this would result in a convolution with a sinc-function. This is shown in the middle part of Fig. 3. From this we can conclude that the ideal low-pass filter is "smeared out" in order to be able to implement it.

The other issue is caused by the fact that the impulse response is non-zero for negative indices. This would imply that the system would produce an output before an input is presented. This non-causal behaviour cannot be implemented in practice, since it would mean that we could use future samples, which is impossible in practical applications. In order to make sure that the impulse response is causal, it needs to be shifted in time such that it is no longer non-zero for negative indices. This shift in time will inevitably lead to an additional phase response due to the FTD shift property. This is represented in the lower part of Fig. 3.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/LTI/LPF.svg"
      alt="{This figure visualizes the impulse and frequency response of (a) an ideal low-pass filter, (b) an ideal low-pass filter with a finite impulse response and (c) an ideal low-pass filter with a finite and causal impulse response."
    />
    <figcaption class="numbered">
      {This figure visualizes the impulse and frequency response of (a) an ideal low-pass filter, (b) an ideal low-pass filter with a finite impulse response and (c) an ideal low-pass filter with a finite and causal impulse response.
    </figcaption>
  </figure>
</div>
