+++
title = "DFT for continuous signals"

# date = {{ .Date }}
lastmod = 2019-11-27

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "DFT for continuous signals"
  weight = 6
  parent = "Transforms II: Discrete Fourier transform"

+++


In practice the DFT, or its efficient version the FFT, is often used to calculate the frequency content of (non periodic) continuous time signals. This will always result in an approximation from which the various causes of errors are shown for all intermediate steps in Fig. 17.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/DFT/contDFT1.svg"
      alt="Various errors causes in the approach of continuous frequency content using DFT."
    />
    <figcaption class="numbered">
      Various errors causes in the approach of continuous frequency content using DFT.
    </figcaption>
  </figure>
</div>

The top figure shows an example of a continuous time signal $h(t)$ and its frequency representation (FTC) $H(\omega)$. First of all we derive a finite length signal $\hat{h}(t)$ by multiplying $h(t)$ with a window function $w(t)$ from which the FTC is given by $W(\omega)$, as depicted in the second figure from the top. The FTC $\hat{H}(\omega)$ of the product $\hat{h}(t)=h(t) \cdot w(t)$ is given by the convolution $\hat{H}(\omega)=H(\omega) \star W(\omega)$, as depicted in the third figure from the top. Next we convert signal $\hat{h}(t)$ into the discrete time signal samples $h[n]= \hat{h}(t)|\_{t = n \cdot T}$. The fourth figure from the top represents $h[n]$ and its FTD spectrum $H(e^{j\omega})$. The relation between $H(e^{j\omega})$ and  $\hat{H}(\omega)$ can be expressed by the following equation:
$$
H(e^{j\omega}) = \frac{1}{T} \sum\_{k=-\infty}^{\infty} \hat{H}(\omega - \frac{2 \pi \cdot k}{T}).
$$
Finally we can consider the $N$ non zero samples of $h[n]$ as the Fundamental Period (FP) of the periodic extended signal $h_p[n]$. Applying the $N$ point DFT results into the periodic function $H_p[k]$ as depicted in the bottom figure. Within the Fundamental Interval (FI) we have the following equality:
$$
H_p[k] = H(e^{j\omega})|\_{\omega = k \cdot \frac{2\pi}{N}}.
$$
Apart from the factor $\frac{1}{T}$, which we can easily be corrected, we are dealing with the following two error causes:
The first one is the multiplication of $h(t)$ with the finite duration window function $w(t)$. As a result we are dealing with $\hat{H}(\omega)$ and not with $H(\omega)$. As we take a wider window, the function $\hat{H}(\omega)$ becomes a better approximation of $H(\omega)$. The second error is caused by the fact that the sampling of $\hat{h}(t)$ can result in aliasing in the frequency domain.
It can be shown that it is physically impossible that both $h(t)$ and $H(\omega)$ are of finite width. As a result, in practice we will always have to deal with
at least one of the error causes.

At the transition from $h(t)$ to $h_p[n]$, and from $H(\omega)$ to $H_p[k]$, we have to make a choice for the sampling interval $T$ and the number of samples $N$. At the one hand the product $N \cdot T$ determines the error that we introduce by considering only part of $h(t)$. On the other hand both parameters $N$ and $T$ are reflected in the DFT result: The approximated frequency interval of $H(\omega)$ has a width of $\frac{2\pi}{T}$ and the inter sample distance $\Delta \omega$ in between succeeding frequency samples is $\frac{2 \pi}{N \cdot T}$. Thus we have:
$$
\Delta \omega = \frac{2\pi}{N \cdot T} \hspace{3mm} \Rightarrow \hspace{3mm}
T \cdot \Delta \omega = \frac{2\pi}{N}.
$$
This equation reflect a fundamental property which implies that the time-bandwidth product is constant.
