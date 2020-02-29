+++
title = "From FTC to DFT"

# date = {{ .Date }}
lastmod = 2019-11-27

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "From FTC to DFT"
  weight = 1
  parent = "Transforms II: Discrete Fourier transform"

+++


## DFT Concept
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/SAq9y5t6FfY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>
In previous modules have seen that a Fourier transform can be used to calculate the frequency distribution of a signal. Various Fourier transforms have been discussed, each for a different type signal. In this section we will introduce again another Fourier transform: The Discrete Fourier Transform (DFT). The main advantage of the DFT is that this transform, in contrast to almost all other Fourier transforms, can be calculated on a computer. In this section we will give  a conceptual view of the DFT. In the first subsection we show how the DFT equation can be related, in different intermediate steps, to the Fourier Transform for Continuous time signals (FTC). In the second subsection we will discuss the periodic behaviour of the DFT. In order to calculate the frequency distribution on a computer, we will explain in the last subsection how the DFT can extract frequencies of a signal.

<br></br>
## From FTC via FTD to DFT
The purpose of this subsection is to derive a Fourier transform, the DFT, that can be calculated on a computer. So we have to find a transform whose variables are discrete in both time and frequency domain.

In a previous module we have seen that the FTC calculates the frequency distribution of a continuous time signal $x(t)$. In other words the FTC calculates for any frequency $\omega$, the frequency content of the signal $x(t)$ at that particular frequency $\omega$.
The FTC and its inverse, are mathematically defined as:
\begin{eqnarray}
X(f)=\int\_{-\infty}^{\infty} x(t) e^{-j2 \pi f t}  \text{d} t
& \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
x(t) = \int\_{-\infty}^{\infty} X(f) e^{j2 \pi f t} \text{d} f
\end{eqnarray}
with absolute frequency $f$ in Hertz, or as a function of $\omega=2 \pi f$ in radians per second:
\begin{eqnarray}
X(\omega) = \int\_{-\infty}^{\infty} x(t) e^{-j\omega t}  \text{d} t
& \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
x(t) = \frac{1}{2\pi} \int\_{-\infty}^{\infty} X(\omega) e^{j\omega t} \text{d} \omega
\end{eqnarray}
The top figure of Fig. 1 shows an example of such a frequency distribution of $x(t)$, from which the maximum frequency is denoted by $\omega_m$. From the mathematical definition of the FTC it is obvious that we can't evaluate this equation on a computer, since both time- and frequency- variables are continuous.
Because both time and frequency variables are continuous, we cannot calculate the FTC as such on a computer. In the following steps we will convert both continuous variables into discrete variables. During these steps we will see that the following general rule of thumb will play a very important role:

<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Sampling in one domain results in repetitions in the other domain.</i></div>


<figure>
<div class="rowimg4">
  <div class="columnimg4">
    <img src="/../files/7.Images/discrete/transforms/DFT/step1.svg"
    style="width:100%">
  </div>
  <div class="columnimg4">
    <img src="/../files/7.Images/discrete/transforms/DFT/step2a.svg"
    style="width:100%">
  </div>
  <div class="columnimg4">
    <img src="/../files/7.Images/discrete/transforms/DFT/step2b.svg"
    style="width:100%">
  </div>
  <div class="columnimg4">
    <img src="/../files/7.Images/discrete/transforms/DFT/step3a.svg"
    style="width:100%">
  </div>
</div>
<figcaption class="numbered">
  Different steps to relate FTC and DFT.
</figcaption>
</figure>


By using an A/D convertor, which runs at a sampling rate of $f_s =1/T_s$ [Samples/sec] or [Hz], we obtain discrete time signal samples $x[n T_s]$, in which $T_s$ is the inter sample distance. This step is depicted at the left hand side of the second figure of Fig. 1.
As a result of this sampling process we can apply the general rule of thumb, which implies that the frequency content, denoted by $X(e^{j\Omega})$, becomes a repeated function of the original frequency distribution with repetition factor $2 \pi / T_s$, as depicted at the right hand side of the second figure of Fig. 1.
This implies that the repetitions are inversely related to the inter sample distance $T_s$. In other words when increasing the inter sample distance $T_s$, thus taking less samples per second, the repetitions in frequency domain come closer to each other. This behavior is described by the sampling theorem, which states that in order to prevent the repeated frequency content from overlapping, we have to choose the sampling frequency $f_s=1/T_s$ in such a way that the maximum frequency $\omega_m < \pi/ T_s$. In case this is not true the repeated spectra will overlap which is called aliasing. Furthermore, because of the repetitions, we only need one of the repeated intervals. Typically we choose this interval in the range $- \pi/T_s$ until $+\pi/T_s$ and this interval is denoted as the Fundamental Interval, abbreviated with FI.

In many cases, when working on a computer, we do not need explicit knowledge of the inter sample distance $T_s$. In time domain we simply denote the samples by $x[n]$, in which $n$ is an integer variable which can range from $-\infty$ until $+ \infty$. In frequency domain this results in a normalization of the absolute frequency $f$ with the sampling frequency $f_s$. We  denote the resulting, so called relative frequency, by the continuous variable $\theta$ which equals $2 \pi f/f_s$. This step is depicted in the third figure of Fig. 1. One period of the relative frequency content has a width of $2\pi$ and typically the FI is chosen in the range $-\pi$ until $+\pi$. Furthermore it follows from the sampling theorem that in order not to obtain overlapped spectra or aliasing, we have to choose the sampling frequency $f_s > 2 f_m$. This follows from the figure since the frequency content does not overlap when $f_m < f_s/2$. The Fourier transformation that we obtain in such a way is the so called Fourier Transform for Discrete-time signals (abbreviated as FTD). The FTD and its inverse are mathematically defined as:
\begin{eqnarray}
X(e^{j\theta})=\sum\_{n=-\infty}^{\infty} x[n] e^{-jn \theta}
& \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
x[n] = \frac{1}{2\pi} \int\_{-\pi}^{\pi} X(e^{j\theta}) e^{jn \theta} \text{d} \theta
\end{eqnarray}
Because $\theta$ is a continuous variable, we cannot calculate the FTD as such with a computer. Thus we need to convert this variable also into a discrete variable, which leads to the following step.

In order to uniquely describe the function $X(e^{j\theta})$ we only need one period of width $2\pi$  Thus we can 'sample' the continuous frequency variable $\theta$ at $N$ equidistant positions with an inter frequency 'sampling' distance of $\frac{2\pi}{N}$, in which $N$ is an integer number. This step is depicted at the right hand side of the bottom figure of Fig. 1. Because of this sampling procedure we can apply again the general rule of thumb which leads to the following:
The sampling in frequency domain results in a repetition in the time domain. Because of the fact that the inter sample distance in frequency domain is proportional to $\frac{1}{N}$, the resulting repetition in time domain is proportional to $N$. In other words, by choosing $N$ equidistant samples in one FI in the frequency domain, we obtain a repeated or periodic function in time domain, from which one period consists of $N$ samples. Typically we choose one so called Fundamental Period, abbreviated by FP, from which the indices $n$ range from $0$ until $N-1$, as depicted at the left hand side of the bottom figure of Fig. 1.
The Fourier transformation that we obtain in such a way is the so called Discrete Fourier Transform (abbreviated as DFT), which is mathematically defined as:
$$
X[k] = \sum\_{n=0}^{N-1} x[n] e^{-j\frac{2\pi}{N} k n}
$$
Since all variables in this equation are integer numbers (real or complex) it follows that we can compute the DFT on a computer.

In the following subsection we will show that the Inverse DFT can be constructed in a similar way and is defined as follows:
$$
x[n] = \frac{1}{N} \sum\_{k=0}^{N-1} X[k] e^{j\frac{2\pi}{N} k n}
$$
The only differences of the Inverse DFT with the DFT are:
<ul>
<li>At the first place, the minus-sign in the complex exponent has been interchanged by a positive sign. In one of the following subsections we show that the DFT summation adds complex vectors which turn clock wise. The positive sign of the Inverse DFT results in the addition of complex vectors that turn anti clock wise, while the procedure is the same.</li>
<li>Secondly, all Fourier transforms, including the DFT, preserve energy. This means the energy in both time- and frequency-domain stays the same: A Fourier transform cannot change energy when going from one domain to the other. For this reason it can be shown that we need a factor $\frac{1}{N}$ in the Inverse DFT definition. </li>
</ul>

<br></br>
## DFT of sinusoidal signal example
To become more familiar with the concept of the DFT, let us first consider the following simple example in which we sketch the result of applying a 4-point DFT to the sampled version of a 1 Hertz sinusoidal signal $x(t)=\cos (2 \pi t)$ which is sampled at a sample rate of $f_s = 4$ [Hz]. The different steps as discussed in the previous subsection are depicted in Fig. 2.



<figure>
<div class="rowimg4">
  <div class="columnimg4">
    <img src="/../files/7.Images/discrete/transforms/DFT/example1a.svg"
    style="width:100%">
  </div>
  <div class="columnimg4">
    <img src="/../files/7.Images/discrete/transforms/DFT/example1b.svg"
    style="width:100%">
  </div>
  <div class="columnimg4">
    <img src="/../files/7.Images/discrete/transforms/DFT/example1c.svg"
    style="width:100%">
  </div>
  <div class="columnimg4">
    <img src="/../files/7.Images/discrete/transforms/DFT/example1d.svg"
    style="width:100%">
  </div>
</div>
<figcaption class="numbered">
  Different steps from FTC towards DFT for $x(t)=\cos (2 \pi t)$.
</figcaption>
</figure>


The frequency content of this continuous time signal $x(t)$ consists of two phasors with absolute frequencies $f= \pm 1$ [Hz], which results in two delta pulses for $f= \pm 1$ [Hz] as depicted at the right hand side of the top figure of Fig. 2. By sampling at a sample rate of $f\_s = 4$ [Hz], or with an inter sample distance of $T\_s = 1/ 4$ [sec], we obtain an infinite sequence of samples (...., 1,0,-1,0,1,0 ...) which can be described by the discrete-time function $x[n] = \cos (\frac{\pi}{2} n)$, as depicted at the left hand side of the second figure of Fig. 2. The absolute frequencies of the two phasors are mapped to delta functions at the relative frequencies $\theta = \pm \frac{\pi}{2}$. Above that we obtain repetitions and usually the FI is chosen in between $-\pi$ until $+\pi$.  But in fact it does not matter where we choose this interval, as long as the width equals $2\pi$. So in some cases, like in the DFT case, the FI interval is typically chosen from $0$ until $2 \pi$, as depicted at the right hand side of the second figure of Fig. 2. The 4-point DFT uses only 4 samples of the discrete-time signal $x[n]$. In the module FTD it was shown that a finite length sinusoidal $x\_{win}[n]$, which is obtained by windowing the infinite length sinusoidal $x[n]$, results in two smeared out pulses at the positions of the phasor frequencies, denoted by $X\_{win}(e^{j\theta})$. The finite length sinusoidal $x\_{win}[n]$ and its FTD result $X\_{win}(e^{j\theta})$ are depicted in the third figure of Fig. 2. By sampling the frequency content of $X\_{win}(e^{j\theta})$, that is taking $N=4$ samples at an inter sample distance of $2\pi/ 4$, we obtain the samples which are denoted by $X[k]$ in the right hand side figure of Fig. 2. From this 4-point DFT result we obtain two nonzero frequency components which represent the two phasors of the original continuous time signal $x(t)$.  Because of the sampling in frequency domain the original 4 samples of the FP are repeated in time domain.

Concluding it follows that the 4-point DFT result of the finite length sequence of samples (1,0,-1,0) results in two non zero DFT components. For this particular example these DFT components  define the exact location of the phasor frequencies of the original continuous time signal $x(t)$. However, this will not always be the case. For example the sampling grid of the DFT, which is related to $\frac{2 \pi}{N}$, does not have to coincide exactly with the location of the phasor frequencies of the underlying continuous time signal $x(t)$. Furthermore it is obvious that the width of the main lobe of the windowed FTD $X\_{win}(e^{j\theta})$, which also depends on the number of samples $N$ used to calculate the DFT, plays a very important role. These topics will be discussed in one of the following sections.

Up to now we have shown the main steps to obtain an equation of a Fourier transform that can be calculated on a computer. In the following subsection we will go into more detail of the periodic behavior of the DFT.
