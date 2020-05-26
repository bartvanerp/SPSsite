+++
title = "Non-parameteric methods"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-03-21

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Non-parametric methods"        # name of this item in that menu
  weight = 4                      # location in that menu
  parent = "Spectral estimation"
+++

This section will discuss several techniques to perform power spectral density estimation. Some methods aim at improving the periodogram, which was the direct method to estimate the power spectral density, while other apply to the correlogram. But first it is important to note what problems arise when estimating the power spectral density.

<br></br>
## Estimation performance
Previously, two methods were presented for the estimation of the power spectral density. These methods provided us with an estimated $\hat{P}(e^{j\theta})$. Since this is an estimate, the expected value and variance can be determined to determine its estimation performance.

### The expected value of the power spectral density estimator
The expected value of $\hat{P}(e^{j\theta})$ can be found as
\begin{equation}
    \begin{split}
        \mathrm{E}\left[\hat{P}(e^{j\theta})\right]
        &= \mathrm{E}\left[\sum_{l=-(N-1)}^{N-1} \hat{r}_x[l]e^{-jl\theta}\right], \newline
        &= \sum_{l=-(N-1)}^{N-1} \mathrm{E}\left[\hat{r}_x[l]\right]e^{-jl\theta}.
    \end{split}\label{eq:exp_corr}
\end{equation}
Closer examination of the expected value of the estimated auto-correlation function using its definition through
\begin{equation}
    \begin{split}
        \mathrm{E}\left[\hat{r}_x[l]\right]
        &= \mathrm{E}\left[\frac{1}{N}\sum_{n=0}^{N-1-|l|}x[n]x^\ast[n-|l|]\right], \newline
        &=\frac{1}{N}\sum_{n=0}^{N-1-|l|}\mathrm{E}\left[x[n]x^\ast[n-|l|]\right], \newline
        &= \frac{N-|l|}{N}r_x[l],
    \end{split}\label{eq:autocorr_est}
\end{equation}
shows that the estimator of the auto-correlation function is asymptotically unbiased. The difference between the expected value of the estimator and the true value disappears as $N\rightarrow \infty$. Because of this, the estimated power spectral density function is then also asymptotically unbiased. As a rule of thumb, use at least 50 samples and use the biased estimator of lags up to a quarter of the amount of samples.

Using the Wiener-Khinchine relationship, which relates the power spectral density and the auto-correlation function as
\begin{equation}\label{eq:wiener_k}
    P(e^{j\theta}) = \sum_{l=-\infty}^\infty r[l] e^{-jl\theta},
\end{equation}
it can be noted that the expected value of the estimated power spectral density $P(e^{j\theta})$ is very similar up to the point where if we were to define a window function $w_B[l]$ as
\begin{equation}
    w_B[l] =
    \begin{cases}
        \frac{N-|l|}{N},        & \text{for }|l| < N\newline
        0,                      & \text{otherwise}
    \end{cases}
\end{equation}
the expected value from (\ref{eq:exp_corr}) could be rewritten as
\begin{equation}
    \mathrm{E}\left[\hat{P}(e^{j\theta})\right] = \sum_{l=-\infty}^{\infty} w_B[l]r_x[l]e^{-jl\theta}.
\end{equation}
Closer examination of $w_B[l]$ reveals that this is actually a triangular or Bartlett window function of length $2N-1$. So it may be concluded that the estimated power spectral density is expected to be the Fourier transform of the windowed true auto-correlation function.

When this relationship is regarded in the Fourier domain the multiplication-convolution property of the Fourier transform should be taken into account. It states that a multiplication in the time domain results in a convolution in the frequency domain. Since the Bartlett window and the true auto-correlation function are multiplied, their spectra are convoluted in the frequency domain, leading to the estimated power spectral density. The spectrum of the true auto-correlation function is given by Wiener-Khintchine relationship in (\ref{eq:wiener_k}) as the true power spectral density and the spectrum of the Bartlett window $W_B(e^{j\theta})$ can be determined as
\begin{equation}\label{eq:ft_triang}
        W_B(e^{j\theta}) = \frac{1}{N}\left(\frac{\sin(N\theta/2)}{\sin(\theta/2)}\right)^2.
\end{equation}
The proof of (\ref{eq:ft_triang}) is beyond the scope of this reader, but it can easily be found by regarding the Bartlett window as a convolution between two rectangular windows and following the multiplication-convolution property.

To summarize, the expected value of the estimated power spectral density function can be interpreted as the convolution in frequency domain between the true power spectral density function and the spectrum of a triangular window function. This convolution is given by
\begin{equation}\label{eq:exp_p}
    \mathrm{E}\left[\hat{P}(e^{j\theta})\right] = \frac{1}{2\pi} P(e^{j\theta})\ast W_B(e^{j\theta}).
\end{equation}
As $N\rightarrow\infty$ the spectrum of the windowing function will approach a delta pulse function and the expected value of the estimated periodogram will become the true periodogram.

### Calculation of the biased auto-correlation function using the DFT
When dealing with windowed signals longer than 100 samples, the auto-correlation function is oftentimes more efficiently calculated using the DFT or FFT. Fig. 1 shows a schematic overview of the calculation procedure. Normally the signal is windowed using a window of length $N$. From this windowed signal the auto-correlation function of length $2N-1$ can be calculated through the definition of the auto-correlation function.
Another way of performing this calculation is as follows. First, the signal is windowed with length $N$ and zero-padded to length $M$. The windowed signal should be at least $2N-1$ samples long. From this signal the DFT or FFT is calculated and its magnitude is squared and normalized, after which the IDFT or IFFT is calculated. From the obtained signal, the auto-correlation function can be determined by shifting the signal segments as indicated in Fig. 1.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/spectrum/ACthroughDFT.svg"
      alt="Graphical illustration on the calculation of the auto-correlation function through the use of the DFT."
    />
    <figcaption class="numbered">
      Graphical illustration on the calculation of the auto-correlation function through the use of the DFT.
    </figcaption>
  </figure>
</div>

### The variance of the power spectral density estimator
The variance of the power spectral density estimator can be found to be
\begin{equation}
    \text{Var}\left[\hat{P}(e^{j\theta})\right] \approx  P(e^{j\theta})^2.
\end{equation}
The proof is beyond the scope of this reader, since it has dependencies on the fourth-order moment of the signal. From this it can be seen that $\hat{P}(e^{j\theta})$ is not a consistent estimator, since the variance does not converge to zero. It can also be shown that the same holds when using different kind of initial windowing function.
Similar conclusions can be obtained for the correlogram.

<br></br>
## Periodogram (direct method)}
When the power spectral density is estimated using the squared Fourier transform of the signal, it is referred to as a periodogram. There exist different methods to improve the "raw" periodogram, which will be discussed hereafter.


### Standard method
To briefly recap one of the previous sections, the periodogram estimate of the power spectral density is obtained as
\begin{equation}
    \hat{P}(e^{j\theta}) =\frac{1}{N}\left|\sum_{n=0}^{N-1} x[n]e^{-jn\theta}\right|^2 .
\end{equation}
which is the normalized squared magnitude of the spectrum of the windowed signal.

### Bartlett's method: average periodogram
The periodogram was determined as an asymptotically unbiased, non-consistent estimator of the power spectral density. If the window length goes to $\infty$, the bias reduces, however, the variance does not decrease.

Bartlett describes a procedure in which the variance can be decreased. He thought of a procedure consisting of averaging the estimated periodograms of smaller signal segments by splitting the total signal of length $N$ into $k$ segments of length $L$. In other words, the original signal $x[n]$ of length $N$ is split into $k$ smaller but equally long non-overlapping signals $x_i[n]$ of length $L$, from which the respective power spectral density estimators can be written as
\begin{equation}
    \hat{P}_i(e^{j\theta}) = \frac{1}{L}\left|\sum\_{n=0}^{L-1} x_i[n]e^{-jn\theta}\right|^2.  \qquad \text{for }i=1,2,\ldots,k
\end{equation}
The final power spectral density estimator can then be determined by averaging all the sub-periodograms as
\begin{equation}
    \hat{P}_B(e^{j\theta}) = \frac{1}{K} \sum\_{i=1}^K \hat{P}_i(e^{j\theta}).
\end{equation}
Fig. 2 shows a graphical representation of the described method.

To understand why this method actually decreases the variance, we first take a look at the estimators expected value. The expected value can be determined as
\begin{equation}
    \begin{split}
        \mathrm{E}\left[\hat{P}_B(e^{j\theta})\right]
        &= \mathrm{E}\left[\frac{1}{K} \sum\_{i=1}^K \hat{P}_i(e^{j\theta})\right], \newline
        &= \frac{1}{K} \sum\_{i=1}^K\mathrm{E}\left[ \hat{P}_i(e^{j\theta})\right], \newline
        &= \mathrm{E}\left[ \hat{P}(e^{j\theta})\right], \newline
        &= \frac{1}{2\pi} P(e^{j\theta})\ast W_B(e^{j\theta}),
    \end{split}
\end{equation}
which indeed shows a similar relationship as obtained previously; however, because the signal segments are now shorter ($L<N$) the bias increases because of poorer estimation of the auto-correlation function in (\ref{eq:autocorr_est}), which is calculated on a smaller number of samples. On the other hand, the variance can be determined as
\begin{equation}
    \begin{split}
        \text{Var}\left[\hat{P}_B(e^{j\theta})\right]
        &= \text{Var}\left[\frac{1}{K} \sum\_{i=1}^K \hat{P}_i(e^{j\theta})\right], \newline
        &= \frac{1}{K^2}\text{Var}\left[ \sum\_{i=1}^K \hat{P}_i(e^{j\theta})\right], \newline
        &= \frac{1}{K}\text{Var}\left[ \hat{P}_i(e^{j\theta})\right] \approx \frac{1}{K} P(e^{j\theta})^2,
    \end{split}\label{eq:bartlett}
\end{equation}
which proves that the variance indeed decreases for an increase in number of signal segments. From this it can be concluded that Bartlett's method reduces the variance of the periodogram at the cost of an increased bias.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/spectrum/bartlett_welch.svg"
      alt="A graphical representation of Bartlett's and Welch's method. In Bartlett's method periodograms of non-overlapping signal segment are averaged for the final periodogram and in Welch's method periodograms of overlapping windowed signal segment are averaged for the final periodogram."
    />
    <figcaption class="numbered">
      A graphical representation of Bartlett's and Welch's method. In Bartlett's method periodograms of non-overlapping signal segment are averaged for the final periodogram and in Welch's method periodograms of overlapping windowed signal segment are averaged for the final periodogram.
    </figcaption>
  </figure>
</div>


### Welch's overlapped segment averaging (WOSA) method
A very similar method to the one that Bartlett proposed is Welch's method. This is also known as Welch's overlapped segment averaging (WOSA) spectral density estimation. In this method, the signal is also split in different segments but now allowing overlapping between the segments (typically with 50\% or 75\% overlap); then these segments are windowed before calculating the individual periodograms, and then averaged, similarly to Bartlett's method. Fig. 2 shows a graphical visualisation of this method. The consequence of this overlap is that the individual segments are now no longer independent, which results in (\ref{eq:bartlett}) not being valid anymore. When applying this method the variance is still decreased, but with to a smaller extent compared to Bartlett's method. On the other hand, since the segments are now longer due to the overlap, the bias does not increase as much as with Bartlett's method.

<br></br>
## Correlogram (indirect method)
When the power spectral density is estimated using the Fourier transform of the estimated auto-correlation function, it is referred to as a correlogram. Hereafter, we will first recap the "raw" correlogram and then we will describe an improvement known as the Blackman-Tukey correlogram.

### Standard method
we briefly review the definition of correlogram, which has also already been defined as
\begin{equation}
    \hat{P}_N(e^{j\theta})= \sum\_{l=-(N-1)}^{N-1} \hat{r}_x[l]e^{-jl\theta}.
\end{equation}
The correlagram is the Fourier transform of the estimated auto-correlation function. This method strongly resembles the Wiener-Khintchine relationship from (\ref{eq:wiener_k}), but then for an estimated auto-correlation function.

### Blackman-Tukey method
The basic idea of The Blackman-Tukey correlogram is to apply a symmetric window function $w_L[n]$ of length $2L-1$ to the estimated auto-correlation function. The Blackman-Tukey estimate of the power spectral density $\hat{P}\_{BT}(e^{j\theta})$ can be defined as
\begin{equation}
    \hat{P}\_{BT}(e^{j\theta}) = \sum\_{l=-(L-1)}^{L-1} w\_L[l]\hat{r}[l]e^{-jl\theta}.
\end{equation}
Here the estimated auto-correlation function is windowed. The estimated auto-correlation function includes a relatively high uncertainty around its borders, since the auto-correlation is calculated at these locations with a very limited number of samples. Whereas the auto-correlation in the center of the window is computed with almost all samples available. Therefore, by using a suitable window, we can reduce the weight of the auto-correlation lags at the borders of the window, were only few samples are available. In the frequency domain, the Blackman-Tukey estimator can be interpreted as the convolution between the spectrum of the window and the estimated power spectral density as
\begin{equation}
    \hat{P}\_{BT}(e^{j\theta}) = \frac{1}{2\pi} \hat{P}(e^{j\theta})\ast W_L(e^{j\theta}).
\end{equation}
Let us know determine the performance of this method. The expected value of the estimator can be determined using (\ref{eq:exp_p}) as
\begin{equation}
    \begin{split}
        \mathrm{E}\left[\hat{P}\_{BT}(e^{j\theta})\right]
        &= \frac{1}{2\pi}\mathrm{E}\left[\hat{P}(e^{j\theta})\right] \ast W_L(e^{j\theta}), \newline
        &= \frac{1}{2\pi} P(e^{j\theta})\ast W_B(e^{j\theta})\ast W_L(e^{j\theta}), \newline
        &\approx \frac{1}{2\pi} P(e^{j\theta})\ast W_L(e^{j\theta}),
    \end{split}
\end{equation}
where it is assumed that the Blackman-Tukey window has a length significantly smaller than the length of the auto-correlation function. This assumption also results in the spectrum of the Blackman-Tukey window having wider lobes in comparison to the spectrum of the Bartlett window, which was a direct consequence in the definition of the auto-correlation estimator. Using the definition of the continuous convolution in the frequency domain, the expected value of the estimator can be rewritten as
\begin{equation}
     \mathrm{E}\left[\hat{P}\_{BT}(e^{j\theta})\right] \approx \frac{1}{2\pi} \int_{-\pi}^\pi P(e^{j\theta})W_L(e^{j(\theta-\phi)})\mathrm{d}\phi.
\end{equation}
If we now were to consider the window for an increasing length $2L-1$, we would find
\begin{equation}
 \lim_{L\rightarrow\infty} W_L(e^{j\theta}) = A\delta(\theta),
\end{equation}
which states that the frequency spectrum of the window function converges to a delta pulse, which is similar to the behaviour that has been shown in the previous section.
Combining the previous two equations leads to
\begin{equation}
 \mathrm{E}\left[\hat{P}_{BT}(e^{j\theta})\right] \approx (e^{j\theta})A\delta(\theta-\phi)\mathrm{d}\phi = A P(e^{j\theta})
\end{equation}
stating that the estimator is asymptotically unbiased if $A=1$.

The variance of the Blackman-Tukey estimator can be found as
\begin{equation}
    \text{Var}\left[\hat{P}\_{BT}(e^{j\theta})\right] \approx \frac{P(e^{j\theta})^2}{N}\left(\sum_{l=-(L-1)}^{L-1} w_L^2[l]\right),
\end{equation}
which shows that the estimator is consistent when $N \rightarrow \infty$. There is a compromise made for the length of the Blackman-Tukey window function $L$. A large value of $L$ will namely decrease the bias of the estimator, since the spectrum of the window will approach a delta pulse, and the variance of the estimator will increase, because of the longer summation.

<br></br>
## Methods summary
The "raw" periodogram and correlogram calculate the power spectral density by either the square of the absolute windowed signal spectrum or by the Fourier transform of the estimated auto-correlation function, respectively. They produce asymptotically unbiased estimators for an increasing length of the signal. However, there is no way to decrease the variance.

Bartlett's method improves the "raw" periodogram by averaging over multiple power spectral density estimators, which are calculated for non-overlapping segments of the signal. Using this approach the variance can be decreased by using more segments, but the bias is increased.

Welch's method is similar to Bartlett's method, but allows for overlap between the windowed segments. Because the estimators are no longer independent, the variance does not decrease as much, but neither will the bias increase as much.

Blackman-Tukey method uses a different approach and windows the auto-correlation estimator, because this estimator contains a lot of uncertainty around its borders due to the limited amount of samples used to calculate the auto-correlation at these points. This can be seen in the Fourier domain by convolving the true power spectral density with the spectrum of the window. A longer window allows for more uncertainty, increasing the variance, but reduces the effects of the convolution, therefore decreasing the bias.

Fig. 3 shows the estimated power spectral density of the signal
\begin{equation}
    x[n] = \cos(0.35\pi n) + \cos(0.4\pi n) + 0.25\cos(0.8 \pi n) + \epsilon[n],
\end{equation}
where $\epsilon[n]$ is standard Gaussian noise. In this figure several methods are used to estimate the power spectral density using various design parameters. Please note the important differences and characteristics of each method and see how the parameters affect the spectral estimation.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/spectrum/estimation.svg"
      alt="The estimated power spectral density of a signal using multiple methods and design parameters, which are depicted in the plot titles. It should be noted that the Blackman-Tukey method uses a Bartlett (triangular) window."
    />
    <figcaption class="numbered">
      The estimated power spectral density of a signal using multiple methods and design parameters, which are depicted in the plot titles. It should be noted that the Blackman-Tukey method uses a Bartlett (triangular) window.
    </figcaption>
  </figure>
</div>
