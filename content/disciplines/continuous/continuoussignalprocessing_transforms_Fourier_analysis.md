+++
title = "Fourier series analysis"

# date = {{ .Date }}
lastmod = 2020-03-28

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "Fourier series analysis"
  weight = 3
  parent = "Transforms II: Fourier series"
+++

In this section we will show the other way around: when we are given the waveform in the time-domain of a periodic signal $x(t)$, how can we derive the spectral weights $\alpha_k$? In order to do so we need the following basic property of a phasor function:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The integral over one period $T_0=1/F_0$ of a phasor with a harmonic related frequency $k \cdot F_0$ results always in zero except for the case $k=0$.</i></div>

Mathematically this can be shown as follows:
$$
\int_0^{T_0} e^{j2\pi k F_0 t} \mathrm{d}t = \left[\frac{e^{j2\pi kF_0 t}}{j2\pi F_0 k}\right]\_{t=0}^{T_0} = \frac{e^{j2\pi k}-1}{j2\pi F_0 k} = \frac{1-1}{j2\pi F_0 k} = 0.
$$
Furthermore the integral can be evaluated for $k=0$ as
$$
\int_0^{T_0} e^{j2\pi 0 F_0 t}\mathrm{d}t = \int_0^{T_0}1\mathrm{d}t = \left[t\right]\_0^{T_0} = T_0-0 = T_0.
$$
What do the above two equation now actually mean? If we integrate a sinusoidal signal over a number of periods, we are actually summing the areas under the sinusoid. Since the sinusoid has an equal area under as above the horizontal axis per period, the area will sum to zero. However, if $k=0$, which means that we are talking about a DC signal, the signal does not oscillate around the horizontal axis and therefore the integral will not become zero.

When we normalize and combine the previous two equations we obtain the basic property of phasors

$$\bbox[5px,border:1px solid black]{
\frac{1}{T_0}\int_0^{T_0}e^{j2\pi kF_0 t}\mathrm{d}t =
\begin{cases}
1,      &\text{for }k=0\newline
0.      &\text{for }k\neq 0
\end{cases}}
$$

Since we are sure that a periodic signal $x(t)$, with Fundamental period $T_0 = 1/F_0$, only consists of harmonic related frequencies we can use the above phasor property as follows to analyze which harmonic related frequencies are present in $x(t)$ and what are the complex values of the spectral weights. For this we evaluate the normalized integral over one period $T_0$ of $x(t)$ multiplied by a phasor with harmonic related frequency $l \cdot F_0$. Thus with both $k$ and $l$ integer we obtain

$$
\begin{split}
\frac{1}{T_0}\int_0^{T_0}x(t)e^{-j2\pi lF_0 t}\mathrm{d}t
&= \frac{1}{T_0}\int_0^{T_0}\left(\sum\_{k=-\infty}^{\infty} \alpha_k e^{j2\pi kF_0 t}\right)e^{-j2\pi lF_0 t}\mathrm{d}t, \newline
&= \sum\_{k=-\infty}^{\infty} \alpha_k \left(\frac{1}{T_0} \int_0^{T_0} e^{j2\pi(k-l)F_0 t}\mathrm{d}t \right),
&= \alpha_l.
\end{split}
$$

In the last step we have used the phasor property to observe that the integral only becomes non-zero when $k=l$.

Thus when we are given a periodic signal $x(t)$ with period $T_0 = 1/F_0$ then we can find the spectral components $a_k$ by using the following Fourier series analysis equation
$$\bbox[5px,border:1px solid black]{
\alpha_k = \frac{1}{T_0}\int_0^{T_0}x(t)e^{-j2\pi kF_0t}\mathrm{d}t}.
$$

In practical application it is impossible to evaluate $\alpha_k$ for $-\infty<k<\infty$. Therefore we can approximate a period signal $x(t)$ with only a limited amount of terms as

$$
\hat{x}(t) = \sum_{k=-N}^{N} \alpha_k e^{j2\pi kF_0 t}.
$$
It is obvious that the approximation becomes better and better for larger $N$.

<div class="example">
<h4> Example </h4>
Given the following periodic signal $x(t)$, evaluate the spectral weights $\alpha_k$. Furthermore, show the approximated periodic signal $x(t)$ when using only up to the first 5 terms.
  <figure style="max-width: 600px; margin: auto">
    <img
      src="/../files/7.Images/continuous/transforms/block_ideal.svg"
      alt="Ideal periodic block wave."
    />
    <figcaption>
      Ideal periodic block wave $x(t)$.
    </figcaption>
  </figure>
<button class="collapsible">Show solution</button>
<div class="content">
From the figure it follows that $x(t)$ is a periodic signal with period $T_0=1/F_0=4$ [sec]. In most cases it is convenient to evaluate first the DC component $\alpha_0$ of the periodic signal (which can be regarded as just the average value of the signal). The DC component can be calculated simply by averaging as
$$
\alpha_0 = \frac{1}{T_0}\int_0^{T_0} x(t)\mathrm{d}t = \frac{1}{4} \bigg\{ \int_0^2 2\mathrm{d}t + \int_2^4 0\mathrm{d}t\bigg\} = \frac{1}{4}\{ 4+0\} = 1.
$$
Furthermore with $\omega_0=2\pi F_0 = \frac{2\pi}{4} = \frac{\pi}{2}$, we obtain for $\alpha_k$
$$
\begin{split}
\alpha_k
&= \frac{1}{T_0}\int_0^{T_0}x(t)e^{-j\omega_0 kt}\mathrm{d}t
= \frac{1}{4}\int_0^{2}2e^{-j\omega_0 kt}\mathrm{d}t
= \frac{1}{4} \left[ \frac{2e^{-j\omega_0 kt}}{-j\omega_0 k}\right]\_0^2, \newline
&= \frac{j}{2\omega_0 k}\left(e^{-j2\omega_0 k}-1\right)
= \frac{j}{k\pi}(e^{-j\pi k}-1) = \frac{\left(e^{-j\pi}\right)^k -1}{k\pi}j
= \frac{(-1)^k -1}{k\pi}e^{j\frac{\pi}{2}}, \newline
&= \frac{1-(-1)^k}{k\pi}e^{-j\frac{\pi}{2}}.
\end{split}
$$
Thus except for $k=0$ all Fourier coefficients with even index $k$ are equal to zero. The Fourier coefficients with odd indices are:
$$
\alpha_1 = \alpha_{-1}^\ast = \frac{2}{\pi}e^{-j\frac{\pi}{2}},
\quad \alpha_3 = \alpha_{-3}^\ast = \frac{2}{3\pi}e^{-j\frac{\pi}{2}},
\quad \alpha_5 = \alpha_{-5}^\ast = \frac{2}{5\pi}e^{-j\frac{\pi}{2}},
\quad \text{etc.}
$$
When approximating this periodic signal with the first $N$ terms we obtain
$$
\begin{split}
\hat{x}(t)
&= \alpha_0 + \sum_{k=1}^N \left(\alpha_k e^{jk\frac{\pi}{2} t} +\alpha_{-k} e^{-jk\frac{\pi}{2} t} \right), \newline
&= 1 + \frac{4}{k\pi}\sum_{k=1,3,5,\ldots}^N \cos\left(k\frac{\pi}{2}t - \frac{\pi}{2}\right), \newline
&= 1 + \frac{4}{k\pi}\sum_{k=1,3,5,\ldots}^N \sin\left(k\frac{\pi}{2}t\right).
\end{split}
$$
The figure below gives the approximation of the block wave for an increased number of Fourier coefficients, where $k$ is limited between $-N$ and $N$.
<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/block_approximate.gif"
      alt="Approximation of an ideal block wave."
    />
    <figcaption>
      Approximation of an ideal block wave, where the $k$ is limited between $-N$ and $N$. The value of $N$ is altered during the animation.
    </figcaption>
  </figure>
</div>
</div>
</div>
