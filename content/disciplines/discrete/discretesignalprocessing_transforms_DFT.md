+++
title = "Discrete-time Fourier transform"

# date = {{ .Date }}
lastmod = 2019-11-27

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Discrete-time Fourier transform"
  weight = 52
  parent = "Discrete-time transforms"


+++


## DFT Concept
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/SAq9y5t6FfY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

In previous modules have seen that a Fourier transform can be used to calculate the frequency distribution of a signal. Various Fourier transforms have been discussed, each for a different type signal. In this section we will introduce again another Fourier transform: The Discrete Fourier Transform (DFT). The main advantage of the DFT is that this transform, in contrast to almost all other Fourier transforms, can be calculated on a computer. In this section we will give  a conceptual view of the DFT. In the first subsection we show how the DFT equation can be related, in different intermediate steps, to the Fourier Transform for Continuous time signals (FTC). In the second subsection we will discuss the periodic behaviour of the DFT. In order to calculate the frequency distribution on a computer, we will explain in the last subsection how the DFT can extract frequencies of a signal.

### From FTC via FTD to DFT
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

#### DFT of sinusoidal signal example
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

<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/cMsFFW8nyOU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

### Periodicity DFT and Periodic Extension (PE)
In general a discrete time signal $x[n]$ can have an infinite amount of samples from which the sampling index $n$ ranges from $-\infty$ to $+\infty$, as depicted at the left hand side of Fig. 3. However when using the $N$-point DFT, we select $N$ samples of $x[n]$, typically ranging from time index $n=0$ until $n=N-1$. The frequency indices $k$ of the DFT resulting samples $X[k]$ also range from $k=0$ until $k=N-1$.
Both DFT and the Inverse DFT are periodic, or circular, operations. This periodic behavior can be shown for the Inverse DFT operation as follows:
\\
When increasing the index $n$ with $\lambda \times N$, in which $\lambda$ is a positive or negative integer, the Inverse DFT equation changes as follows:
$$
x[n+ \lambda N]= \frac{1}{N} \sum\_{k=0}^{N-1} X[k] e^{j\frac{2\pi}{N} k (n+ \lambda N)}
=\frac{1}{N} \sum\_{k=0}^{N-1} X[k] e^{j\frac{2\pi}{N} k n} \cdot e^{j\frac{2\pi}{N} k \lambda N}
$$
The last complex exponent is equal to one for all values of index $k$ and the result is equal to $x[n]$:
$$
x[n+ \lambda N]= \frac{1}{N} \sum\_{k=0}^{N-1} X[k] e^{j\frac{2\pi}{N} k n} \cdot e^{j2\pi k \lambda } = \frac{1}{N} \sum\_{k=0}^{N-1} X[k] e^{j\frac{2\pi}{N} k n} \cdot 1 = x[n]
$$
This implies that the Inverse DFT results in a periodic signal, denoted by $x_p[n]$, which has a period of $N$ samples.
This periodic signal $x_p[n]$ can be constructed from the original signal $x[n]$  by first selecting the $N$ signal samples that are used in the DFT operation and then periodically repeat these samples. This Periodic Extension, abbreviated as PE, is depicted at the right hand side of Fig. 3. Obviously only one period of this period extended signal $x_p[n]$ is of importance.
Typically we use the $N$ samples ranging from index $n=0$ until $n=N-1$ which is the so called Fundamental Period, abbreviated by FP.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/DFT/PE.svg"
      alt="Example of Periodic Extension (PE)."
    />
    <figcaption class="numbered">
      Example of Periodic Extension (PE).
    </figcaption>
  </figure>
</div>

In a similar way it can be shown that the DFT samples $X[k]$  are periodic:
$$
X[k + \lambda N] = \sum\_{n=0}^{N-1} x[n] e^{-j\frac{2\pi}{N}(k+ \lambda N) n}
=\sum\_{n=0}^{N-1} x[n] e^{-j\frac{2\pi}{N}k n} = X[k] \text{ } \Rightarrow \text{ } X_p[k].
$$
As a result of this periodic behavior we can redefine the DFT and IDFT operations in terms of
the periodic extended notations as follows:

$$
\boxed{
\begin{eqnarray}
\text{DFT: } X_p[k] = \sum\_{n=0}^{N-1} x_p[n] e^{-j\frac{2 \pi}{N} k n}
\hspace{3mm} {\color{red}\bf \forall k}
\qquad
\text{IDFT: } x_p[n] = \frac{1}{N} \sum\_{k=0}^{N-1} X_p[k] e^{j\frac{2 \pi}{N} k n} \hspace{3mm} {\color{red}\bf \forall n}
\end{eqnarray}
}
$$
In this definition the indices $n$ and $k$ range from $-\infty$ to $+\infty$. However we only need one period which is typically chosen in the index range from $0$ until $N-1$. In time domain this range of $N$ samples is the FP, representing the original $N$ signal samples of $x[n]$ which have been used for the DFT operation. In frequency domain this range of $N$ samples is the FI, which represents relative frequencies $\theta$ in the range $0$ until $2\pi$.

<i>Note: To simplify the notation, we will sometimes omit the sub-index $p$ in the sequel if it is clear that we are dealing with a periodic extended signal.</i>

<div class="example">
<h4> Example </h4>
<hr>
Give an expression for the 4-point periodic extended signal $x_p[n]$ of $x[n]=\delta[n-1]$ and calculate the 4-point DFT.
<button class="collapsible">Show solution</button>
<div class="content">
The periodic extended signal writes as $x_p[n]= \delta[(n-1)\text{mod}(4)]$. Some values are:
\begin{eqnarray}
x_p[-4]&=& \delta[(-5)\text{mod}(4)]=0 \text{ ; }
x_p[-3]= \delta[(-4)\text{mod}(4)]=1 \\
x_p[-2]&=& \delta[(-3)\text{mod}(4)]=0 \text{ ; }
x_p[-1]= \delta[(-2)\text{mod}(4)]=0 \\
x_p[0]&=& \delta[(-1)\text{mod}(4)]=0 \text{ ; }
x_p[1]= \delta[(0)\text{mod}(4)]=1 \\
x_p[2]&=& \delta[(1)\text{mod}(4)]=0 \text{ ; }
x_p[3]= \delta[(2)\text{mod}(4)]=0 \\
x_p[4]&=& \delta[(3)\text{mod}(4)]=0 \text{ ; }
x_p[5]= \delta[(4)\text{mod}(4)]=1 \\
x_p[6]&=& \delta[(5)\text{mod}(4)]=0 \text{ ; }
x_p[7]= \delta[(6)\text{mod}(4)]=0
\end{eqnarray}
The 4-point DFT writes as:
$$
X_p[k] = \sum_{n=0}^{3} x_p[n] e^{-j\frac{2 \pi}{4} k n}= e^{-j\frac{2 \pi}{4} k} = (-j)^k
$$
Some values are:
\begin{eqnarray}
& X_p[-4]= 1 \text{ ; } X_p[-3]= -j \text{ ; } X_p[-2] = -1 \text{ ; } X_p[-1]= j & \\
& X_p[0]= 1 \text{ ; } X_p[1]= -j \text{ ; } X_p[2] = -1 \text{ ; } X_p[3]= j & \\
& X_p[4]= 1 \text{ ; } X_p[5]= -j \text{ ; } X_p[6] = -1 \text{ ; } X_p[7]= j &
\end{eqnarray}
</div>
</div>


### Basic DFT summation or orthogonality property
In order to understand how the DFT equations can extract frequencies of a signal, we will see that the complex exponent $W\_N=e^{j\frac{2\pi}{N}}$, the so called twiddle factor, plays a very important role. This can be shown by evaluating the following summation:
$$
S[k]= \sum\_{n=0}^{N-1} \\{ W\_N^k \\} ^n  = \sum\_{n=0}^{N-1} \\{ e^{j\frac{2 \pi}{N} k} \\} ^n
$$
which adds ,for each index $k$, $N$ terms of a discrete time phasor with relative frequency $\theta = k \cdot \frac{2\pi}{N}$.
For this evaluation we shown that $S[k]$ is periodic with period $N$. With $\lambda$ a positive or negative integer this can be proven as follows:
$$
\begin{eqnarray}
S[k + \lambda \cdot N ] &=& \sum\_{n=0}^{N-1} \left \\{ e^{j\frac{2 \pi}{N} (k + \lambda \cdot N)} \right \\} ^n
= \sum\_{n=0}^{N-1} \left \\{ e^{j\frac{2 \pi}{N} k} \cdot  e^{j\frac{2 \pi}{N} \lambda \cdot N} \right \\} ^n \newline
&=& \left \\{ e^{j\frac{2 \pi}{N} k} \cdot  e^{j2 \pi \lambda } \right \\} ^n =
\left \\{ e^{j\frac{2 \pi}{N} k} \cdot  1  \right \\} ^n = S[k]
\end{eqnarray}
$$
Because of this periodic behavior, we only need to evaluate $S[k]$ for one period, e.g. for $k=0, 1, \cdots , N-1$. For $k=0$ the result is:
$$
S[k]|\_{k=0}= \sum\_{n=0}^{N-1} \\{ e^{j\frac{2 \pi}{N} 0} \\} ^n = \sum\_{n=0}^{N-1} \\{ 1\\} ^n = N
$$
To evaluate $S[k]$ for $k \neq 0$ we use the following general geometric series:
$$
\sum\_{n=0}^{N-1} a^n = \frac{1-a^N}{1-a}
$$
which results into the following:
$$
\begin{eqnarray}
S[k]|\_{k\neq0}&=& \sum\_{n=0}^{N-1} \\{ e^{j\frac{2 \pi}{N} k} \\} ^n =
\frac{1-e^{j\frac{2 \pi}{N} k N}}{1-e^{j\frac{2 \pi}{N} k}}
= \frac{1-e^{j2 \pi k}}{1-e^{j\frac{2 \pi}{N} k}} =
\frac{1-1}{1-e^{j\frac{2 \pi}{N} k}}=0
\end{eqnarray}
$$
This leads to the following basic DFT summation or orthogonality property:

$$
\boxed{
\begin{eqnarray}
S[k]= \sum\_{n=0}^{{\color{red}N}-1} \left \\{ W\_{{\color{red}N}}^k \right \\} ^n =
\sum\_{n=0}^{{\color{red}N}-1} \left \\{ \text{e}^{j \frac{2\pi}{{\color{red}N}} k } \right \\} ^n = {\color{red}N}  \delta [{\color{blue} k} \text{ mod}({\color{red}N})]
\end{eqnarray}
}
$$

Thus, the summation $S[k]$ is always equal to zero, except for the cases that the index $k$ is an $N$-fold, thus for $k$ equal to $0$ or $\pm N$ or $\pm 2N$ or etc.  which can be described by the given delta function in which the index contains the modulo(N) operation.


<div class="example">
<h4> Example </h4>
<hr>
Calculate the values of $S[k]$ for $N=4$ and $k=-1,0,1,2,3,4$ explicitly.
<button class="collapsible">Show solution</button>
<div class="content">
\begin{eqnarray}
S[-1] &=& \sum_{n=0}^{3} \left (e^{j\frac{\pi}{2} \cdot -1}\right )^n = \sum_{n=0}^{3} \left (e^{-j\frac{\pi}{2} \cdot 1}\right )^n = 1 - j - 1 +j =0 \\
S[0] &=& \sum_{n=0}^{3} \left (e^{j\frac{\pi}{2} \cdot 0}\right )^n =
\sum_{n=0}^{3} \left (1 \right )^n = 1 + 1 + 1 + 1 = 4 \\
S[1] &=& \sum_{n=0}^{3} \left (e^{j\frac{\pi}{2} \cdot 1}\right )^n = 1 + j - 1 -j =0 \\
S[2] &=& \sum_{n=0}^{3} \left (e^{j\frac{\pi}{2} \cdot 2}\right )^n = 1 - 1 +1 -1 =0 \\
S[3] &=& \sum_{n=0}^{3} \left (e^{j\frac{\pi}{2} \cdot 3}\right )^n = 1 - j -1 + j =0 \\
S[4] &=& \sum_{n=0}^{3} \left (e^{j\frac{\pi}{2} \cdot 4}\right )^n =
\sum_{n=0}^{3} \left (e^{j2 \pi }\right )^n =
\sum_{n=0}^{3} \left (1 \right )^n = 1 + 1 + 1 + 1 = 4
\end{eqnarray}
</div>
</div>

<div class="example">
<h4> Example </h4>
<hr>
Give a mathematical expression in terms of a delta pulse of $A[k]=\sum_{n=0}^{7} e^{j\frac{2\pi}{4} \cdot n \cdot k}$ and calculate $A[k]$ for for $k=-8,-7, \cdots, 14, 15$.
<button class="collapsible">Show solution</button>
<div class="content">
\begin{eqnarray}
A[k]&=\sum_{n=0}^{7} e^{j\frac{2\pi}{4} \cdot n \cdot k}  \\
&= \sum_{n=0}^{7} \left\{ e^{j\frac{2\pi}{8} 2k} \right\}^n \\
&= 8 \cdot \delta[2k \text{mod}(8)]
\end{eqnarray}
Explicit evaluation of $A[k]$ are as follows:
$$
\begin{eqnarray}
&
A[-8]=8 \text{ ; }
A[-7]=0 \text{ ; }
A[-6]=0 \text{ ; }
A[-5]=0 \text{ ; }
&\\
&
A[-4]=8 \text{ ; }
A[-3]=0 \text{ ; }
A[-2]=0 \text{ ; }
A[-1]=0 \text{ ; }
&\\
&
A[0]=8 \text{ ; }
A[1]=0 \text{ ; }
A[2]=0 \text{ ; }
A[3]=0 \text{ ; }
&\\
&
A[4]=8 \text{ ; }
A[5]=0 \text{ ; }
A[6]=0 \text{ ; }
A[7]=0 \text{ ; }
&\\
&
A[8]=8 \text{ ; }
A[9]=0 \text{ ; }
A[10]=0 \text{ ; }
A[11]=0 \text{ ; }
&\\
&
A[12]=8 \text{ ; }
A[13]=0 \text{ ; }
A[14]=0 \text{ ; }
A[15]=0 \text{ ; }
&
\end{eqnarray}
$$
From these values it follows that we can write the result as follows:
$A[k] = 8 \delta[k \text{mod}(4)]$.
</div>
</div>



### How the DFT extracts a frequency
In this subsection we will show by an example, that the basic DFT summation property is used in the DFT algorithm to find the relative frequencies which are 'hidden' in the signal samples
$x[n]$ for $n=0,1, \cdots, N-1$. In this example we use a DFT of length $N=4$, so for each resulting DFT index $k$ the result of the DFT operation describes how much of the relative frequency $k \times \frac{2 \pi}{4}$ is contained in the signal samples $x[n]$ in the range $n=0$ until $n=3$.
In order to show how this works we use again the same sinusoidal example as before, namely $x[n]= \cos (\frac{\pi}{2} n)$:
$$
X[k] = \sum\_{n=0}^{3} x[n] e^{-j\frac{2\pi}{4} k n}
= \sum\_{n=0}^{3} \cos (\frac{\pi}{2} n) e^{-j\frac{\pi}{2} k n}
$$
By using Euler, we can split the cosine into two discrete-time phasors, split the summation into two separate summations and combine in each of these summations the complex exponents:

\begin{eqnarray}
X[k]&=& \sum\_{n=0}^{3} \frac{1}{2} \cdot \left ( e^{j\frac{\pi}{2} n} +  e^{-j\frac{\pi}{2} n} \right ) e^{-j\frac{\pi}{2} k n} \newline
&=& \frac{1}{2} \sum\_{n=0}^{3} \left ( e^{j\frac{\pi}{2} n}  \right ) e^{-j\frac{\pi}{2} k n} +
\frac{1}{2} \sum\_{n=0}^{3} \left ( e^{-j\frac{\pi}{2} n}  \right ) e^{-j\frac{\pi}{2} k n} \newline
&=& \frac{1}{2} \sum\_{n=0}^{3} e^{-j\frac{\pi}{2} (k-1) n} + \frac{1}{2} \sum\_{n=0}^{3} e^{-j\frac{\pi}{2} (k+1) n}
\end{eqnarray}

Now we can use for each of these individual summations the previous described basic DFT summation property. The first summation will always result into zero except for the case when the DFT frequency index $k-1$ is a 4-fold, thus for $k=1$ or $k=5$ or $k=-3$ etc. Mathematically this can be described by a delta function from which the index contains a modulo-4 operation as given in the first part of the following result:
$$
X[k]= \frac{1}{2} \cdot 4 \delta[(k-1) \text{ mod}(4)]+ \frac{1}{2} \cdot 4 \delta[(k+1) \text{ mod}(4)]
$$
The second summation will always result into zero except for the case when the DFT frequency index $k+1$ is a 4-fold, thus for $k=-1$ or $k=-5$ or $k=3$ etc. which also results in a delta function.

In the FI, which ranges from frequency index $k=0$ until $k=3$ in this case, this leads to the same two delta pulses as we have found before, namely:
$$
\Rightarrow \hspace{2mm} \text{In FI: } X[k] = 2\delta[k-1] + 2\delta[k-3]
$$
This example shows how the basic DFT summation property is used in the DFT algorithm to extract the frequency components of the $N$ signal samples $x[n]$.

<!-- TODO:
\centerline{{\color{blue}ANIMATION DFT-animation.m here, or refer to video (contains explanation)}}
-->



<div class="example">
<h4> Example </h4>
<hr>
Calculate a trigoniometric expression for the 16 point IDFT $x_p[n]$ of $X_p[k]$ which is defined as:
$$
X_p[k]= 2 \delta[(k-1) \text{mod}(16)] + \delta[(k-3) \text{mod}(16)]
+ \delta[(k-13) \text{mod}(16)] + 2 \delta[(k-15) \text{mod}(16)]
$$
<button class="collapsible">Show solution</button>
<div class="content">
$$
\begin{eqnarray}
x_p[n] &=& \frac{1}{16} \sum_{k=0}^{15} \left \{ 2 \delta[(k-1) \text{mod}(16)] + \delta[(k-3) \text{mod}(16)] + \right .\\
& & \left . + \delta[(k-13) \text{mod}(16)] + 2 \delta[(k-15) \text{mod}(16)] \right \} e^{j\frac{2\pi}{16} k n}\\
&=& \frac{1}{16} \left \{
2 e^{j\frac{2\pi}{16} n} + e^{j\frac{2\pi}{16} 3n} + e^{j\frac{2\pi}{16} 13n} +2 e^{j\frac{2\pi}{16}15 n} \right \} \\
&=& \frac{1}{16} \left \{
2 e^{j\frac{\pi}{8} n} + e^{j\frac{\pi}{8} 3n} + e^{-j\frac{\pi}{8} 3n} +2 e^{-j\frac{\pi}{8} n} \right \} \\
&=& \frac{1}{16} \left \{ 4 \cos (\frac{\pi}{8} n) + 2 \cos (\frac{\pi}{8} 3n)
\right \} = \frac{1}{4} \cos (\frac{\pi}{8} n) + \frac{1}{8} \cos (\frac{3\pi}{8} n)
\end{eqnarray}
$$
</div>
</div>




<br></br>

## DFT properties
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/0yRxU3HQWto" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

In this section we will discuss the main DFT properties. We will see that most of these properties look similar to the properties of other Fourier transforms however there are some important differences which are caused by the fact that the DFT is a periodic, or circular, operation.

### Circular shift
As one of the first consequences of the periodic behavior we need to pay special attention to the shift operation.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/DFT/circularshift.svg"
      alt="Comparison shift and circular shift."
    />
    <figcaption class="numbered">
      Comparison shift and circular shift.
    </figcaption>
  </figure>
</div>

The two figures at the left hand side of Fig. 4 show a signals $x[n]$ and its shifted version $x[n-1]$ which has been shifted over one sample to the right. More specifically the red sample at index $n=0$ moves to index $n=1$ and the blue sample at index $n=3$ moves to index $n=4$.
The two figures at the right hand side of Fig. 4 shows the Periodic Extended signal $x_p[n]$, with period $N=4$ samples, and its shifted version $x_p[n-1]$. From these figures it is clear that $x_p[n-1]$ and  $x[n-1]$ are not the same. More specifically for $x_p[n-1]$ the blue sample at index $n=3$ is moved out the FP at the right hand side while it enters again at the left hand side at index $n=0$.  This circular, or periodic, behavior can be represented by using modulo counting as follows: The samples denoted by $x_p[(n-1) \text{mod}N]$ represent the samples in the FP of $x_p[n]$ which has been shifted over one sample.

For the proof of the circular shift property, we need an explicit expression for this modulo representation, which can be derived as follows:

Fig. 5 represents the time index axis $n$ which ranges from $-\infty$ until $+\infty$. One interval of the periodic extended signal $x_p[n]$  consists of $N$ samples and the indices of the FP range from $0$ until $N-1$. Now we shift $x_p[n]$ over $n_0$ samples, in which we assume for simplicity $n_0 \leq 0$.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/DFT/moduloshift.svg"
      alt="Circular shift as modulo counting."
    />
    <figcaption class="numbered">
      Circular shift as modulo counting.
    </figcaption>
  </figure>
</div>

An explicit expression for the indices of the samples of $x_p[n-n_0]$ within the FP can be found as follows:


As a first step we can represent the shifted sample at index $-n_0$ within the FP by adding $\lambda$ times $N$, with $\lambda \in \mathbb{N}$.  Then we must try to map $N$ consecutive samples into the FP. The samples in the red area map into the red area at the right hand side of the FP. In this range the samples are indexed by $n-n_0 + \lambda N$, as denoted in the following equation:
$$\label{eq:indexinFP}
x_p[(n-n_0) \text{mod}(N)]
= \begin{cases}
\color{red}{x_p[n-n_0 + \lambda N]} & \textit{index }\in \color{red}{{\bf -}}
\newline
\color{blue}{x_p[n-n_0 + \lambda N {\bf -N}]} & \textit{index }\in {\color{blue}{\bf -}}
\end{cases}
$$
In order to map the other samples, indicated in the blue area, inside the FP, an extra $N$ samples must be subtract, as denoted in the equation above.

The circular shift property states that a circular shift in time domain results in a multiplication with a complex exponent in frequency domain:
$$
\boxed{
x\_p[n-n\_0] \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} e^{-j\frac{2\pi}{N} k n\_0 } \cdot X\_p[k]}
$$

<div class="example">
<h4> Proof of circular shift property</h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
The DFT of the shifted samples $x_p[n-n_0]$ is denoted as:
$$
Y[k]= \sum_{n=0}^{N-1} x_p[n-n_0] e^{-j\frac{2\pi}{N} k n}.
$$
Now we can use the indexing as discussed above: Split the indices in a red and blue part. The red part contains the samples which are at the right end side of the FP and the blue part contains samples that are shifted outside the FP at the right end side and entering the FP again at the left end side:
\begin{eqnarray}
Y[k]
&=& \sum_{\in {\color{red}{\bf -}}} \color{red}{x_p[n-n_0 + \lambda N]} e^{-j\frac{2\pi}{N} k n}
+ \sum_{\in {\color{blue}{\bf -}}} \color{blue}{x_p[n-n_0 + \lambda N -N ]} e^{-j\frac{2\pi}{N} k n}
\end{eqnarray}
Substitute a new index $m$ and replace the index $n$ with this new index in the complex exponent of both summations:
$$
Y[k]= \sum_{m \in {\color{red}{\bf -}}} \color{red}{x_p[m]} e^{-j\frac{2\pi}{N} k (m+n_0 - \lambda N)}
+ \sum_{m \in {\color{blue}{\bf -}}} \color{blue}{x_p[m]} e^{-j\frac{2\pi}{N} k (m+n_0 - \lambda N + N)}
$$
The complex exponent with index $n_0$ can be taken outside brackets:
\begin{eqnarray}
Y[k] &=&\left (
\sum_{m \in {\color{red}{\bf -}}} {\color{red}x_p[m]} e^{-j\frac{2\pi}{N} k m } e^{j\frac{2\pi}{N}k \lambda N}
+ \sum_{m \in {\color{blue}{\bf -}}} {\color{blue}x_p[m]} e^{-j\frac{2\pi}{N} k m}
e^{j\frac{2\pi}{N} k (\lambda -1) N}
\right )  e^{-j\frac{2\pi}{N} k n_0} \\
&=&
\left ( \sum_{m \in {\color{red}{\bf -}}} {\color{red}x_p[m]} e^{-j\frac{2\pi}{N} k m } +
\sum_{m \in {\color{blue}{\bf -}}} {\color{blue}x_p[m]} e^{-j\frac{2\pi}{N} k m}
  \right ) \cdot e^{-j\frac{2\pi}{N} k n_0}
\end{eqnarray}
The resulting two summations are the same but each of the indices run over a different part of the FP.  When concatenating these two summations  the result between brackets writes as the DFT result $X_p[k]$, which end the proof:
$$
Y[k]= \left ( \sum_{m \in \text{ FP}} x_p[m] e^{-j\frac{2\pi}{N} k m} \right ) \cdot e^{-j\frac{2\pi}{N} k n_0} = X_p[k] \cdot e^{-j\frac{2\pi}{N} k n_0}
$$
Try to prove yourself that, in a similar way, it can be shown that a circular shift in frequency domain results in a multiplication with a complex exponent in time domain:
$$
\boxed{
e^{j\frac{2 \pi}{N} n k_0} \cdot x_p[n] \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} X_p[k-k_0]}
$$
</div>
</div>


<div class="example">
<h4> Example </h4>
<hr>
The values within the FI of the 5-point DFT of $x_p[n]$ are:
$$
X_p[k]= \begin{cases}
5 & \text{for } k=0 \\
6 & \text{for } k=1 \\
1 & \text{for } k=2 \\
2 & \text{for } k=3 \\
9 & \text{for } k=4 \\
\end{cases}
$$
A new signal is defined as $y_p[n] = W_5^{-2n} x_p[n]$, with twiddle factor $W_5 = e^{j\frac{2\pi}{5}}$. Calculate within the Fundamental Interval the values of $Y_p[k]$ which is the 5-point DFT of this new signal $y_p[n]$.
<button class="collapsible">Show solution</button>
<div class="content">
According to the shift property we obtain:
\begin{eqnarray}
y_p[n] = e^{-j\frac{2\pi}{5}2n} \cdot x_p[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
Y_p[k] = X_p[k+2]]
\end{eqnarray}
resulting into the following values with the FI:
$$
Y_p[k]= \begin{cases}
X_p[2] =1 & \text{for } k=0 \\
X_p[3]=2 & \text{for } k=1 \\
X_p[4]=9 & \text{for } k=2 \\
X_p[0]=5 & \text{for } k=3 \\
X_p[1]=6 & \text{for } k=4 \\
\end{cases}
$$
</div>
</div>



### Circular convolution
The circular convolution, indicated by the symbol $\circledast$, between the two periodic extended signals $x_p[n]$ and $h_p[n]$, both with an FP of $N$ samples, is defined as follows:
$$
x_p[n] \circledast h_p[n]
 =\sum\_{\color{red}{i=0}}^{\color{red}{N-1}} x_p[i] h_p[n-i] = \sum\_{\color{red}{i=0}}^{\color{red}{N-1}} x_p[n-i] h_p[i]
$$
The different steps of the circular procedure are as follows:
<ol>
<li> Eventually pad zeros in order to make the period of both periodic extended signals $x_p[n]$ and $h_p[n]$ the same. </li>
<li> Plot one of the signals, e.g. $h_p[n]$, as function of another index, e.g. $h_p[i]$. </li>
<li> Flip $h_p[i]$ to obtain $h_p[-i]$. </li>
<li> For $n=0,1, \cdots, N-1$:
Calculate $y\_p[n]=\sum_{i=0}^{N-1} x_p[i] h_p[n-i]$.</li>
</ol>
As an example the circular convolution result $y_{p} [n] = x_{p}[n] \circledast h_{p}[n]$
is depicted in Fig. 6.

<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/DFT/conv2finitesignalsa.svg"
      alt="Circular convolution."
    />
    <figcaption class="numbered">
      Circular convolution.
    </figcaption>
  </figure>
</div>

Within the FP these Periodic Extended signals are defined as:
\begin{eqnarray}
x\_p[n]&=&\delta[n]+ \delta[n-1] + \delta[n-2] + \frac{1}{2} \delta[n-3] \newline
h\_p[n]&=&\delta[n]+ \frac{3}{4} \delta[n-1] + \frac{1}{2}\delta[n-2] + \frac{1}{4} \delta[n-3]
\end{eqnarray}
resulting in:
$$
y\_{p} [n] = x\_{p}[n] \circledast h\_{p}[n] =
\frac{17}{8} \delta[n]+ \frac{18}{8} \delta[n-1] + \frac{19}{8}\delta[n-2] + \frac{16}{8}  \delta[n-3]
$$

<!-- TODO:
{\color{blue} \centerline{\bf Animation circular Convolution-cyclic.m here}}
-->

<div class="example">
<h4> Example </h4>
<hr>
Compute $y_p[n]=x_p[n] \circledast h_{p}[n]$ with
\begin{eqnarray}
x_p[n] &=& \delta[n \text{mod}(4)] + 2\delta[(n-1) \text{mod}(4)] + \delta[(n-2) \text{mod}(4)] - \delta[(n-3) \text{mod}(4)] \newline
h_p[n] &=& \frac{1}{3} \delta[(n-1) \text{mod}(4)] -\frac{1}{3} \delta[(n-2) \text{mod}(4)] +\frac{1}{3} \delta[(n-3) \text{mod}(4)]
\end{eqnarray}
<button class="collapsible">Show solution</button>
<div class="content">
<!-- TODO:
\centerline{\em SHOW SOLUTION}
Show solution step by step with Matlab animation.m. Result:
$$
y_p[n]=\delta[(n-1)\text{mod}(4)].
$$
-->
</div>
</div>

As in the FTD case it can be shown that for the DFT a circular convolution in time domain is equivalent to a circular multiplication in frequency domain:
$$
\boxed{
x_p[n] \circledast h_p[n] \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} X_p[k] \color{red}{\cdot} H_p[k]}
$$

<div class="example">
<h4> Proof of circular convolution property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
For the proof of this property we first apply  the DFT operation to the circular convolution  and then switch the order of the two summations:
\begin{eqnarray}
Y[k]&=& \text{DFT}\left \{ x_p[n] \circledast h_p[n]\right \} =\sum_{n=0}^{N-1} \left (\sum_{i=0}^{N-1} x_p[i] h_p[n-i] \right ) e^{-j(2 \pi/N) k n}\\
&=&\sum_{i=0}^{N-1} x_p[i] \cdot \left \{ \sum_{n=0}^{N-1} h_p[n-i] e^{-j(2 \pi/N) k n} \right \}
\end{eqnarray}
In between brackets we recognize the DFT of $h_p[n]$ which has been shifted in time domain.  As shown in the previous subsection the time domain shift results in a multiplication with a complex exponent in frequency domain:
$$
Y[k]= \sum_{i=0}^{N-1} x_p[i] \cdot \left \{ H_p[k] \cdot e^{-j(2 \pi/N) k i} \right \}
$$
Moving the complex exponent forward  finalizes the proof:
$$
Y[k]= \left ( \sum_{i=0}^{N-1} x_p[i] e^{-j(2 \pi/N) k i} \right ) \cdot H_p[k]
= X_p[k] \cdot H_p[k]
$$
Try to prove yourself that, in a similar way, that a circular convolution in frequency domain is equivalent to a multiplication in time domain:
$$
\boxed{
x_p[n] \cdot h_p[n] \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} X_p[k] \circledast H_p[k]
}
$$
</div>
</div>


<div class="example">
<h4> Example </h4>
<hr>
Given the same 4-point periodic extended signals as in the previous example:
\begin{eqnarray}
x_p[n] &=& \delta[n \text{mod}(4)] + 2\delta[(n-1) \text{mod}(4)] + \delta[(n-2) \text{mod}(4)] - \delta[(n-3) \text{mod}(4)] \\
h_p[n] &=& \frac{1}{3} \delta[(n-1) \text{mod}(4)] -\frac{1}{3} \delta[(n-2) \text{mod}(4)] +\frac{1}{3} \delta[(n-3) \text{mod}(4)]
\end{eqnarray}
Furthermore we have the following 4-point DFT's: $X_p[k] \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ x_p[n]$ and  $H_p[k] \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ h_p[n]$. Calculate $Y_p[k] = X_p[k] \cdot H_p[k]$
<button class="collapsible">Show solution</button>
<div class="content">
From the circular convolution property it follows that
$$
Y_p[k] = X_p[k] \cdot H_p[k] \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} y_p[n]= x_p[n] \circledast h_p[n]
$$
From the previous example we have $y_p[n]= x_p[n] \circledast h_p[n] =\delta[(n-1)\text{mod}(4)]$.
Thus the answer equals the 4-point DFT of $y_p[n]$:
$$
Y_p[k] = \text{DFT} \{ \delta[(n-1)\text{mod}(4)] \} = e^{-j\frac{2\pi}{4} k}.
$$
Another way to find the solution is to write out the product of the two 4-point DFT's:
\begin{eqnarray}
X_p[k] &=& 1 + 2 e^{-j\frac{2\pi}{4} k} + e^{-j\frac{2\pi}{4} 2k} - e^{-j\frac{2\pi}{4} 3k} \\
H_p[k] &=& \frac{1}{3} \left \{e^{-j\frac{2\pi}{4} k} -e^{-j\frac{2\pi}{4} 2k} + e^{-j\frac{2\pi}{4} 3k} \right \}
\end{eqnarray}
resulting in $Y_p[k] = X_p[k] \cdot H_p[k]= e^{-j\frac{2\pi}{4} k}$.
</div>
</div>


### Complex conjugation
The periodic behavior of the DFT operation leads to a special result of the complex conjugation operation:
$$
\boxed{x_p^\ast[n] \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} X_p^\ast[N-k]}
$$

<div class="example">
<h4> Proof of complex conjugation property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
In the first step  of the proof we apply the DFT operation to the complex conjugated samples and take the the complex operation outside the brackets and  multiply with 1:
$$
Y[k] = \sum_{n=0}^{N-1} x^\ast_p[n] e^{-j\frac{2 \pi}{N}kn} =
\left ( \sum_{n=0}^{N-1} x_p[n] e^{j\frac{2 \pi}{N}kn} \right )^\ast
=\left ( \sum_{n=0}^{N-1} x_p[n] e^{j\frac{2 \pi}{N}kn} \cdot 1 \right )^\ast
$$
The number 1 can be expressed as complex exponent $e^{-j\frac{2 \pi}{N}N n}$:
$$
Y[k]= \left ( \sum_{n=0}^{N-1} x_p[n] e^{j\frac{2 \pi}{N}kn} \cdot
e^{-j\frac{2 \pi}{N}N n} \right )^{\ast}
$$
Combining the two exponents finalizes the proof:
$$
\left ( \sum_{n=0}^{N-1} x_p[n] e^{-j\frac{2 \pi}{N} (N-k) n} \right )^\ast =X_p^\ast[N-k]
$$
As a result of this property we can derive the following property when signal $x[n]$ is real:
$$
\boxed{x[n] \text{ real } \Rightarrow \quad X_p[k]=X^\ast_p[N-k].}
$$
Thus when $x[n]$ is real we only need to calculate half of the DFT components, the other half can by obtained from the resulting symmetry property. More specifically the range of DFT coefficients that we need to calculate for a real signal is as follows:
<ul>
<li> $0 \leq k \leq (N-1)/2$, for $N$ <b>odd</b> </li>
<li> $0 \leq k \leq N/2$, for $N$ <b>even</b> </li>
</ul>
<i>Note that for $N$ even the coefficient $X_p[N/2]=X^\ast_p[N/2]$. In other words $X_p[N/2]$ is a real number.</i>
</div>
</div>

<div class="example">
<h4> Example </h4>
<hr>
The even samples of the 9-point DFT $X_p[k]$ of a real signal $x_p[n]$ are given as follows:
$$
X_p[0]=1 \text{ ; } X_p[2]=5-2 j \text{ ; } X_p[4]=-3 e^{-j\frac{\pi}{10}} \text{ ; }X_p[6]= 7 \text{ ; }X_p[8]=2+5 j
$$
Calculate the odd values of $X_p[k]$.
<button class="collapsible">Show solution</button>
<div class="content">
Signal $x_p[n]$ is real thus we have $X_p[k]= X^\ast[N-k]$ which results in this case, with $N=9$, in:
$$
X_p[1]= X_p^\ast[8]= 2-5 j \text{ ; }
X_p[3]= X_p^\ast[6]= 7 \text{ ; }
X_p[5]= X_p^\ast[4]= -3 e^{j\frac{\pi}{10}} \text{ ; }
X_p[7]= X_p^\ast[2]= 5+2 j
$$
</div>
</div>

<div class="example">
<h4> Example </h4>
<hr>
Given the $N$-point DFT
$$
X_p[k]= e^{j\theta_0} \delta[(k-1) \text{mod}(N)] + e^{-j\theta_0} \delta[(k-(N-1)) \text{mod}(N)]
$$
in which $\theta_0$ is some fixed value.
Calculate $x_p[n]$ the $N$-point IDFT. The answer should be a formula for $x_p[n]$ in terms of $n$ and $N$. Is $x_p[n]$ a real valued signal? If so simplify the resulting formula in such a way that it does not contain $j = \sqrt{-1}$.
<button class="collapsible">Show solution</button>
<div class="content">
The resulting signal $x_p[n]$ will be real since $X_p[k]=X_p^\ast[N-k]$ and can be expressed as follows:
\begin{eqnarray}
x_p[n] &=& e^{j\theta_0} \cdot e^{j\frac{2\pi}{N} n} + e^{-j\theta_0} \cdot e^{j\frac{2\pi}{N}(N-1) n} \\
&=& e^{j\theta_0} \cdot e^{j\frac{2\pi}{N} n} + e^{-j\theta_0} \cdot e^{-j\frac{2\pi}{N} n} =
2 \cos (\frac{2\pi}{N} n + \theta_0)
\end{eqnarray}
</div>
</div>


### Preserve energy (Parceval)
$$
\boxed{\color{red}{\sum\_{n=0}^{N-1}} |x\_p[n]|^2 = \frac{1}{N} \color{blue}{\sum\_{k=0}^{N-1}} |X\_p[k]|^2}
$$

<div class="example">
<h4> Proof of Parceval property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
Parceval has shown that the Fourier transform preserves energy. Here we will show that this property also holds for the DFT. First we write out according to the DFT definition the term $X^\ast_p[k]$:
$$
Y[k]= \frac{1}{N} \color{blue}{\sum_{k=0}^{N-1}} X_p[k] \cdot X^\ast_p[k]
=\frac{1}{N} \color{blue}{\sum_{k=0}^{N-1}} X_p[k] \cdot
\left (\color{red}{\sum_{n=0}^{N-1}} x_p[n] e^{-j\frac{2\pi}{N} kn}\right )^\ast
$$
Then bring the complex conjugation operation inside the brackets, change the order of the summations and combine the factor $\frac{1}{N}$ before the second summation:
$$
Y[k]= \frac{1}{N} \color{blue}{\sum_{k=0}^{N-1}} X_p[k] \cdot
\left (\color{red}{\sum_{n=0}^{N-1}} x^\ast_p[n] e^{j\frac{2\pi}{N} kn}\right )
=\color{red}{\sum_{n=0}^{N-1}} x^\ast_p[n] \cdot \left \{
\frac{1}{N} \color{blue}{\sum_{k=0}^{N-1}} X_p[k] e^{j\frac{2\pi}{N} kn} \right \}
$$
The second summation represents the Inverse DFT operation resulting in $x_p[n]$  which finalizes the proof:
$$
Y[k]=\color{red}{\sum_{n=0}^{N-1}} x^\ast_p[n] \cdot \left \{ x_p[n] \right \} =\color{red}{\sum_{n=0}^{N-1}} |x_p[n]|^2
$$
Note that it seems as if there is a difference of a factor $\frac{1}{N}$ between the energy in time- and frequency domain. However this is the result of the way that the DFT and Inverse DFT operations have been defined.
</div>
</div>

<div class="example">
<h4> Example </h4>
<hr>
Show the Parceval relation for the 4-point Periodic Extended signal
$$
x_p[n]=\delta[n \text{mod}(4)] +\delta[(n-1) \text{mod}(4)] +\delta[(n-2) \text{mod}(4)] +\delta[(n-3) \text{mod}(4)].
$$
<button class="collapsible">Show solution</button>
<div class="content">
First we calculate the 4-point DFT:
$$
X_p[k] = \sum_{n=0}^{3} x_p[n] e^{-j\frac{2\pi}{4} kn} = \sum_{n=0}^{3} e^{-j\frac{2\pi}{4} kn} =
4 \delta[k \text{mod}(4)]
$$
The energy in time- and frequency domain can be calculated as follows:
\begin{eqnarray}
\text{Time} &:& \sum_{n=0}^{3} |x_p[n]|^2 = (1^2 + 1^2 + 1^2 + 1^2)=4 \\
\text{Frequency} &:& \frac{1}{4} \sum_{k=0}^{3} |X_p[k]|^2 = \frac{1}{4} ( 4^2 ) = 4
\end{eqnarray}
which proves that the Parceval relation is indeed correct.
</div>
</div>




<br></br>

## Linear-  by circular-convolution
If we want to perform a filter operation in practice then we need a linear and not a circular convolution. In this section we will show how a circular convolution can be used to realize a linear convolution between two signals $x[n]$ and $h[n]$.

### Convolution of two finite duration signals
In the FTD module we have seen that the linear convolution $y[n]=x[n] \star h [n]$ of a finite duration signal $x[n]$ of $N\_1$ samples with a finite duration impulse response $h[n]$ of $N\_2$ samples results in a finite duration signal $y[n]$ of length $N=N\_1+N\_2-1$ samples.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/DFT/linconv2finitesignals.svg"
      alt="Linear convolution."
    />
    <figcaption class="numbered">
      Linear convolution.
    </figcaption>
  </figure>
</div>
Fig. 7 shows an example of the linear convolution of $x[n]$ and $h[n]$, which are defined as follows:
\begin{eqnarray}
x[n]&=&\delta[n]+ \delta[n-1] + \delta[n-2] + \frac{1}{2} \delta[n-3] \\
h[n]&=&\delta[n]+ \frac{3}{4} \delta[n-1] + \frac{1}{2}\delta[n-2] + \frac{1}{4} \delta[n-3]
\end{eqnarray}
The result $y[n]=x[n] \star h[n]$ has finite duration of $N=N_1 + N_2 -1=7$ samples:
$$
y[n]=\delta[n]+ \frac{7}{4} \delta[n-1] + \frac{9}{4}\delta[n-2] + 2 \delta[n-3]+
\frac{9}{8} \delta[n-4]+ \frac{1}{2} \delta[n-5]+ \frac{1}{8} \delta[n-6]
$$
Despite the fact that within the FP both  $x_p[n]$ and $h_p[n]$ of Fig. 6 are the same as the signals $x[n]$ and $h[n]$ of Fig. 7, it is clear that the FP of the circular convolution result $y_p[n]$ does not result in the desired linear convolution result $y[n]$.
However when first pad both $x_p[n]$ and $h_p[n]$ with zeros up to a length of $N=7$, as depicted in Fig. 8 by $x_{p,b}[n]$ and $h_{p,b}[n]$, then applying a circular convolution the result of $y_{p,b}[n]= x_{p,b}[n] \circledast h_{p,b}[n]$ within the FP is exactly the same as the linear convolution result.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/DFT/conv2finitesignalsb.svg"
      alt="Linear by circular convolution of zero padded signals."
    />
    <figcaption class="numbered">
      Linear by circular convolution of zero padded signals.
    </figcaption>
  </figure>
</div>

In general we can conclude with the following procedure:
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>If signal $x[n]$ consists of $N_1$ samples and impulse response $h[n]$ of $N_2$ samples the result of the linear convolution $y[n] = x[n] \star h[n]$ can be obtained from a circular convolution $y_p[n]=x_p[n] \circledast h_p[n]$ in which both periodic extended $x_p[n]$ and $h_p[n]$ are padded with zeros up to a length of $N \geq N_1 + N_2 -1$ samples.</i></div>


Combining the previous procedure with the fact that a circular convolution is equivalent to a multiplication in the DFT frequency domain we will present a procedure to calculate a linear convolution by a circular one which is implemented in the DFT frequency domain. Referring to Fig. 9 the derivation of this procedure goes as follows:
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/DFT/linearcircular.svg"
      alt="Linear by circular convolution in DFT domain."
    />
    <figcaption class="numbered">
      Linear by circular convolution in DFT domain.
    </figcaption>
  </figure>
</div>

The left hand side of the figure represents a linear convolution result of a finite length signal $x[n]$ of $N\_1$ samples with a finite length impulse response $h[n]$ of $N\_2$ samples, resulting in a finite length signal $y[n]= x[n] \star h[n]$ of $N=N\_1+N\_2-1$ samples. The middle figure represents the linear- by circular procedure as explained above: When padding both $x[n]$ and $h[n]$ up to a length of at least $N$ samples and then Periodic Extend both $x\_p[n]$ and $h\_p[n]$, the result of the samples in the FP of the circular convolution $y\_p[n]= x\_p[n] \circledast h\_p[n]$ is the same as the linear convolution $y[n] = x[n] \star h[n]$.
Finally, the right hand figure represents the the equivalence of a circular convolution to a multiplication in the DFT frequency domain: The circular convolution operation, as denoted in the red box of the middle figure, can be implemented by by the length $N$ Inverse DFT of an element-wise multiplication of the length $N$ DFT results of $x\_p[n]$ and $h\_p[n]$.

In one of the following sections we will show that the DFT can be implemented very efficiently by a so called Fast Fourier Transform (abbreviated by FFT). When applying FFT's it follows that the above described procedure is an extremely efficient way to implement a filter (or convolution) operation. This complexity reduction is one of the main reasons for existence of the DFT and FFT.

<div class="example">
<h4> Example </h4>
<hr>
Given two finite duration signals:
\begin{eqnarray}
x[n] =\delta[n] + \delta[n-1] & \text{and} & h[n]=\delta[n-1] + \delta[n-2]
\end{eqnarray}
Calculate the linear convolution result $y[n]= x[n] \star h[n]$ and show how you can obtain this result by using a circular convolution of the periodic extended signals.
Finally show that this result can be achieved via the DFT domain.
<button class="collapsible">Show solution</button>
<div class="content">
The linear convolution result is $y[n] = \delta[n-1] + 2 \delta[n-2] + \delta[n-3]$.
The 3-point circular convolution result of the periodic extended signals
\begin{eqnarray}
x_p[n] &=& \delta[n \text{mod}(3)] + \delta[(n-1)\text{mod}(3)] \\
h_p[n] &=& \delta[(n-1) \text{mod}(3)] + \delta[(n-2)\text{mod}(3)]
\end{eqnarray}
results in $y_p[n]= \delta[n \text{mod}(3)]+\delta[(n-1) \text{mod}(3)] + 2 \delta[(n-2)\text{mod}(3)]$, which is not the same as the linear convolution result.
Because of the fact that the length of the linear convolution result $y[n]$ is 4 samples long, we need to pad the periodic extended signals up to length 4, thus:
\begin{eqnarray}
x_p[n] &=& \delta[n \text{mod}(4)] + \delta[(n-1)\text{mod}(4)] \\
h_p[n] &=& \delta[(n-1) \text{mod}(4)] + \delta[(n-2)\text{mod}(4)]
\end{eqnarray}
The resulting circular convolution
$$
y_p[n] = \delta[(n-1) \text{mod}(4)] + 2 \delta[(n-2)\text{mod}(4)] + \delta[(n-3) \text{mod}(4)]
$$
which is, within the FP, the same result as the linear convolution $y[n]$.
Via the 4-point DFT we can obtain the same result. For simplicity reasons we calculate the 4-point DFT and IDFT results for indices within the FI and FP respectively, so we can skip the modulo notation:
\begin{eqnarray}
X_p[k] &=& 1 + e^{-j\frac{2\pi}{4} k} \\
H_p[k] &=& e^{-j\frac{2\pi}{4} k} + e^{-j\frac{2\pi}{4} 2k}\\
Y_p[k] &=& X_p[k] \cdot H_p[k] = e^{-j\frac{2\pi}{4} k} + 2e^{-j\frac{2\pi}{4} 2k} + e^{-j\frac{2\pi}{4} 3k} \\
y_p[k] &=& IDFT \{ Y_p[k] \} = \delta[n-1] + 2 \delta[n-2] + \delta[n-3]
\end{eqnarray}
</div>
</div>

<!-- TODO:
\subsection{Convolution infinite duration with finite duration signal}
{\em To be finalized}

\centerline{{\color{blue}Animation Matlab program overlapadd.m}}

\subsubsection{Overlap-add procedure}
\begin{figure}[h!]
\centering
\includegraphics[width=0.8\linewidth]{figs/overlapadd.pdf}
\caption{Overlap add procedure}
\label{Fig:overlapadd}
\end{figure}
As depicted in Fig. \ref{Fig:overlapadd}, the overlap-add procedure is as follows:
\begin{itemize}
\item Split $x[n]$ in length $M \geq 1 (L)$ non-overlapping segments
\item Calculate $y_i[n]=h[n] \star x_i[n]$ (efficiently with FFT's)
\item Add last $L-1$ samples previous segment with first samples current segment
\item $y[n]= \sum_{i=0}^{\infty} y_i[n-Mi]$
\end{itemize}

\subsubsection{Overlap-save procedure}
{\em To be finalized}

\centerline{{\color{blue}Animation Matlab program overlapsave.m}}

\begin{figure}[h!]
\centering
\includegraphics[width=0.8\linewidth]{figs/overlapsave.pdf}
\caption{Overlap save procedure}
\label{Fig:overlapsave}
\end{figure}
As depicted in Fig. \ref{Fig:overlapsave}, the overlap-save procedure is as follows:
\begin{itemize}
\item Split $x[n]$ in length $M \geq L-1$ overlapping segments, overlap $L-1$
\item Calculate $y_i[n]=h[n] \star x_i[n]$ (efficiently with FFT's)
\item Construct $\tilde{y}_i[n]$: Discard first $L-1$ samples, last $N=M-L+1$ are correct
\item $y[n]= \sum_{i=0}^{\infty} \tilde{y}_i[n-Mi]$
\end{itemize}


\centerline{{\color{blue}Video DFT length here}}

-->
<br></br>

## Implications of DFT length $N$
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/OXN9aW6ETKY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

In practice we often use a DFT, or its efficient version the Fast Fourier Transform (FFT), algorithm to calculate a description of a signal in frequency domain. As discussed before, the DFT is related to the FTD and FTC but it is certainly not the same: The DFT uses only a finite set of $N$ samples, is discrete and periodic in both time and frequency domain. In this section we will explain which implications the choice of the length $N$ will have for the relation between the DFT and the FTD. We will do this for signals with finite duration, periodic signals and non-periodic signals with infinite duration.

### Signals with finite duration
An example of a finite duration signal of $M$ samples is depicted in Fig. 10.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/DFT/periodicext.svg"
      alt="Example finite duration signal of $M$ samples."
    />
    <figcaption class="numbered">
      Example finite duration signal of $M$ samples.
    </figcaption>
  </figure>
</div>
When applying the FTD, the infinite summation reduces to the following finite summation, in which the relative frequency is represented by the continuous variable $\theta$:
$$
\text{FTD:} \hspace{2mm} X(e^{j\theta})= \sum_{n=-\infty}^{\infty} x[n] e^{-jn \theta}
= \sum_{n=0}^{\color{green}{M}-1} x[n] e^{-jn \color{red} {\theta}}
$$
On the other hand for $M \leq N$ the DFT results in the following equation:
$$
X[k]= \sum_{n=0}^{\color{blue}{N}-1} x[n] e^{-jn {\color{red}k \cdot \frac{2 \pi}{\color{blue}{N}}} } = \sum_{n=0}^{{\color{green}M}-1} x[n] e^{-jn \color{red}{k \cdot \frac{2 \pi}{\color{blue}{N}}} } \hspace{2mm} \text{for } k =0, \cdots , N-1
$$
When comparing the FTD and $N$-point DFT equations we can conclude the following:
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The $N$ DFT samples $X[k]$ of a finite duration signal $x[n]$ with $M \leq N$ samples,
represent the sampled version of the FTD of $x[n]$:
$$
X[k] = X(e^{j\theta})\mid_{\theta = k \cdot \frac{2\pi}{N}} \text{ for } k = 0,1, \cdots , N-1
$$</i></div>



<b> Examples of FTD and DFT of finite duration signal </b>

The first example is a finite duration signal of $M=8$ samples, as depicted at the left hand side  Fig. 11. The FTD result $|X(e^{j\theta})|$, is depicted in a black drawn curve at the right hand side of the same figure. The relative frequency $\theta$ ranges from 0 until $2\pi$.

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/DFT/example6aN8.svg"
    style="width:100%">
    <figcaption>
      Finite duration signal.
    </figcaption>
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/DFT/example6bN8.svg"
    style="width:100%">
    <figcaption>
      FTD, DFT of length $N=M=8$.
    </figcaption>
  </div>
</div>
<figcaption class="numbered">
  FTD and DFT result of finite duration signal of $M=8$ samples.
</figcaption>
</figure>



The result of an 8-point DFT $|X[k]|$, depicted in red bars at the right hand side of Fig. 11, which is clearly a sampled version of the FTD. The inter frequency sample distance is $\frac{2\pi}{8}$.

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/DFT/example6aN16.svg"
    style="width:100%">
    <figcaption>
      Finite duration signal.
    </figcaption>
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/DFT/example6bN16.svg"
    style="width:100%">
    <figcaption>
      FTD, DFT of length $N=M=16$.
    </figcaption>
  </div>
</div>
<figcaption class="numbered">
  FTD and DFT result of finite duration signal of $M=16$ samples.
</figcaption>
</figure>


Increasing the signal length $x[n]$ with zeros, which is called <b> zero padding </b>, does not influence the resulting FTD equation. The zero padded signal and its FTD are shown in Fig. 12. On the other hand when applying a $N=16$-point DFT  to the zero padded signal, the resulting DFT samples $X[k]$ represent a sampled version of the FTD with an inter frequency sampling distance is $\frac{2\pi}{16}$, as shown in red bars at the right hand side of
Fig. 12.

Concluding:
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The DFT of a zero padded signal results in a finer grid of the resulting DFT frequency samples. The zero padding does not influence the underlying FTD plot.</i></div>


<div class="example">
<h4> Example </h4>
<hr>
The FTD of $x[n]$ is given as $X(e^{j\theta})= 2 \cos (\frac{\theta}{2}) e^{-j\frac{3 \theta}{2}}$.
What is the minimal value of the parameter $N$, such that the $N$-point DFT $X_p[k]$ is a sampled version of $X(e^{j\theta})$. Calculate for this value of $N$ the resulting DFT samples $X_p[k]$.
<button class="collapsible">Show solution</button>
<div class="content">
We can rewrite $X(e^{j\theta})$ as follows:
$$
X(e^{j\theta}) = \left \{ e^{j\frac{\theta}{2}} +  e^{-j\frac{\theta}{2}} \right \} \cdot e^{-j\frac{3 \theta}{2}} = e^{-j\theta} + e^{-j2 \theta}
$$
which results into the following finite duration signal:
$x[n] = \delta[n-1] + \delta[n-2].$ Thus for any $N \geq 3$ the DFT $X_p[k]$ is a sampled version of
$X(e^{j\theta})$. For $N=3$ this results in:
$$
X_p[0] = 2 \text{ ; } X_p[1] = e^{-j\frac{2\pi}{3}} + e^{-j\frac{2\pi}{3}2} \text{ ; }
X_p[2] = e^{-j\frac{2\pi}{3}2} + e^{-j\frac{2\pi}{3}4}
$$
which is indeed a sampled version of $X(e^{j\theta})$.
</div>
</div>


### Periodic signals
For periodic signals it may seem obvious to choose the DFT length $N$ the same as the number of samples of one or more periods. In practice however this is not always trivial. In the following examples we will show the result of such a mismatch.
<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/DFT/example4N12M6time.svg"
    style="width:100%">
    <figcaption>
      12 samples of periodic signal.
    </figcaption>
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/DFT/example4N12M6freq.svg"
    style="width:100%">
    <figcaption>
      $N=12$ point DFT result.
    </figcaption>
  </div>
</div>
<figcaption class="numbered">
  Periodic signal $x[n]=\cos(\frac{2\pi}{6}n)$ and $N=12$ point DFT result.
</figcaption>
</figure>

The plot at the left hand side of Fig. 13 shows $N=12$ samples of the periodic sinusoidal signal $x[n]=\cos(\frac{2\pi}{6}n)$. Because of the fact that 12 is a 6-fold, the 12 samples represent exactly two periods of $x[n]$. The plot at the right hand side of the figure show the result of a 12-point DFT, in which we see two frequency peaks at indices $k=2$ and $k=10$. Via modulo counting it follows that the index $k=10$ is equivalent to index $k=10-12=-2$ in this case. Furthermore the inter frequency distance of the 12-point DFT is $\frac{2\pi}{12}$ which implies that the two frequency indices $k=2$ and $k=-2$ are related to the two relative frequencies $\theta= 2 \cdot \frac{2\pi}{12}= \frac{2\pi}{6} $ and $\theta= -2 \cdot \frac{2\pi}{12}= -\frac{2\pi}{6} $ which are indeed the two phasor frequencies of the sinusoidal signal $x[n]$.
<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/DFT/example4N16M6time.svg"
    style="width:100%">
    <figcaption>
      16 samples of periodic signal.
    </figcaption>
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/DFT/example4N16M6freq.svg"
    style="width:100%">
    <figcaption>
      $N=16$ point DFT result.
    </figcaption>
  </div>
</div>
<figcaption class="numbered">
  Periodic signal $x[n]=\cos(\frac{2\pi}{6}n)$ and $N=16$ point DFT result.
</figcaption>
</figure>

However when using $N=16$ samples, which is not a 6-fold, the 16-point DFT result shows two smeared out peaks as shown at the right hand side of Fig. 14.
In the following subsections we will give three different explanations for this phenomenon.
Each of these explanations will lead to another insight of the DFT operation.
The first explanation is a mathematical one, the second a physical one and the third is a mix of these two.

<div class="example">
<h4> Why the DFT smears out peaks: explanation 1 </h4>
<hr>
<button class="collapsible">Show explanation</button>
<div class="content">
For this first explanation we use the basic DFT summation property.
First we use this property for the evaluation of the 12-point DFT of the same sinusoidal signal $x[n]=\cos(\frac{2\pi}{6}n)$ as above.  In the first step we use Euler to write the sinusoidal signal as the sum of two phasors:
$$
X[k]= \sum_{n=0}^{11} \cos (\frac{2\pi}{\color{purple}{6}}n) e^{-j(\frac{2\pi}{12})k n}
= \frac{1}{2} \sum_{n=0}^{11} \left \{e^{j\frac{2\pi}{{\color{purple}6}}n} +  e^{-j\frac{2\pi}{\color{purple}{6}}n} \right \} e^{-j(\frac{2\pi}{12})k n}
$$
Then we combine the complex exponents  which lead to a summation of two basic DFT summation property results:
$$
X[k]= \frac{1}{2} \sum_{n=0}^{11} \left \{e^{j(\frac{2\pi}{12}n) \color{red}{(2-k)}} +  e^{-j(\frac{2\pi}{12}n) \color{blue}{(2+k)}} \right \}
$$
The first summation is always zero except for the case when the frequency index $2-k$ modulo 12 is equal to zero. Thus within the Fundamental Interval the first summation is equal to zero for all frequency indices $k$ except for $k=2$. For this index the result is $\frac{1}{2} \cdot 12 = 6$ as shown in the first part of the following resulting equation:
$$
X[k]= 6 \delta[\color{red}{(2-k)} \text{ mod}(12)] +
6 \delta[\color{blue}{(2+k)} \text{ mod}(12)]
$$
In a similar way it follows that the second summation is always zero except for the case when the frequency index $2+k$ modulo 12 is equal to zero. Thus within the Fundamental Interval the second summation is equal to zero for all frequency indices $k$ except for $k=-2+12=10$. For this index the result is  $\frac{1}{2} \cdot 12 = 6$, as indicated in the resulting equation above.
Concluding it follows that the 12-point DFT of the periodic sinusoidal signal $x[n]=\cos(\frac{2\pi}{6}n)$ results into two peaks at frequency indices $k=2$ and $k=10$ respectively, which is indeed the same result as shown at the right hand side of Fig. 13.
Applying similar steps for the evaluation of a 16-point DFT of the same periodic sinusoidal signal $x[n]=\cos(\frac{2\pi}{6}n)$ the result is as follows:
\begin{eqnarray}
X[k]&=&\sum_{n=0}^{\color{red}{16}-1} \cos (\frac{2\pi}{\color{purple}{6}}n) e^{-j(\frac{2\pi}{\color{red}{16}})k n} =\frac{1}{2} \sum_{n=0}^{\color{red}{16}-1} \left \{ e^{j\frac{2\pi}{\color{brown}{6}} n}
+  e^{-j\frac{2\pi}{\color{brown}{6}} n}  \right \}
e^{-j\frac{2 \pi}{\color{red}{16}}k n} \nonumber \\
&=& \frac{1}{2} \sum_{n=0}^{\color{red}{16}-1} \left \{e^{j\frac{2\pi}{16} \color{yellow}{(\frac{16}{6} - k)}n} +
e^{-j\frac{2\pi}{16}\color{orange}{(\frac{16}{6} + k)}}n \right \}
\end{eqnarray}
However when trying to apply the basic DFT summation property it follows that in the first summation the frequency index $k$ should be equal to $\frac{16}{6} \approx 2.7$, which is not an integer value. In other words the basic DFT summation property can not be applied to the first summation and the result of this summation will add up to a non zero value for all frequency indices $k$. A similar reasoning follows for the second summation: The frequency index $k$ should be equal to $-\frac{16}{6}$, which becomes $-\frac{16}{6}+ 16 \approx 13.3$ when taking into account modulo 16 calculation. This implies that the 16-point DFT result of the sinusoidal signal $x[n]=\cos(\frac{2\pi}{6}n)$ results in two <b> smeared out</b> peaks around integer indices $k$ which are close to the values 2.7 and 13.3, which is shown in the 16-point DFT plot of Fig. 14.
</div>
</div>


<div class="example">
<h4> Why the DFT smears out peaks: explanation 2 </h4>
<hr>
<button class="collapsible">Show explanation</button>
<div class="content">
A second, more physical, explanation is as follows: When applying a 6-point DFT to the sinusoidal signal $x[n]=\cos(\frac{2\pi}{6}n)$, as depicted in the top figure of the following figure, we use 6 samples (colored in red) which span exactly one period of $x[n]$. As discussed before, the DFT frequency samples represent the frequency content of a periodic extended signal in time domain. In this case the 6-point periodic extended signal is shown in the figure at the bottom of the following figure.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/DFT/PEN6cosine.svg"
      alt="Example one period of 6 samples of $x[n]=\cos(\frac{2\pi}{6}n)$ and its periodic extension."
    />
    <figcaption>
      Example one period of 6 samples of $x[n]=\cos(\frac{2\pi}{6}n)$ and its periodic extension.
    </figcaption>
  </figure>
</div>
Because of the fact that one period of $x[n]$ consists exactly of the 6 samples (in red), the samples of the periodic extended signal are exactly the same as the samples of the original periodic signal $x[n]$. In other words the peaks of the DFT frequency samples coincide exactly with the peaks of the phasor frequencies of $x[n]$ in this example. The same reasoning holds when choosing the length of the DFT any other 6-fold, thus 12, 18 etc.
On the other hand, when using a 16-point DFT (or another <b>non</b> 6-fold in this case),  the periodic extension will cause artifacts at the edges, as depicted in the next figure.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/DFT/PEN16cosine.svg"
      alt="Example one period of 16 samples of $x[n]=\cos(\frac{2\pi}{6}n)$ and its periodic extension."
    />
    <figcaption>
      Example one period of 16 samples of $x[n]=\cos(\frac{2\pi}{6}n)$ and its periodic extension.
    </figcaption>
  </figure>
</div>
As a result the peaks of the DFT frequency samples do not coincide with the peaks of the phasor frequencies of $x[n]$ in this example.  So we can conclude that the smearing out effect is caused by the mismatch of the periodic extension.
A practical way to reduce the smearing out effect is to minimize the artifacts at the edges which can be achieved by multiplying the original $N$ signal samples with a so called window function.
The shape of such a window function is typically close to 1 in the middle of the segment of $N$ samples and close to zero at the edges.  An example of such a window function is the Hanning window:
$$
\color{brown}{w[n]}=\frac{1 - \cos ((2 \pi/N)n)}{2}
$$
At the left hand side of the next figure we see (in red) the $N=16$ signal samples of the periodic sinusoidal signal $x[n]=\cos(\frac{2\pi}{6}n)$ which are windowed (multiplied) with a 16 point Hanning window.
<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/DFT/example5freq.svg"
    style="width:100%">
    <figcaption>
      Windowed periodic signal.
    </figcaption>
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/DFT/example5time.svg"
    style="width:100%">
    <figcaption>
      DFT result.
    </figcaption>
  </div>
</div>
<figcaption>
  Windowed periodic signal $x[n]=\cos(\frac{2\pi}{6}n)$ and $N=16$ point DFT result.
</figcaption>
</figure>
At the right hand side of this figure we see (in black) the original DFT result, thus without windowing.  The DFT result with windowing is shown in red. From this we can see that the smearing out behavior, especially in the range of frequency indices $k=5$ until $k=11$, is reduced.
</div>
</div>

<div class="example">
<h4> Why the DFT smears out peaks: explanation 3 </h4>
<hr>
<button class="collapsible">Show explanation</button>
<div class="content">
For the third explanation of the smearing out effect we will evaluate and compare the FTD and DFT  transforms of a sinusoidal signal with relative frequency $\theta = 0.28 \pi$. The results of 4 of these Fourier transforms are depicted in the next figure.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/DFT/fig4.svg"
      alt="Four Fourier transforms of unwindowed, windowed and zero padded signal."
    />
    <figcaption>
      Four Fourier transforms of unwindowed, windowed and zero padded signal.
    </figcaption>
  </figure>
</div>
The first plot in the figure represents the FTD which takes into account all infinite samples of the periodic signal $x[n]=\cos(0.28 \pi n)$. This transform results into two delta pulses at frequencies $\theta = \pm 0.28 \pi$, representing the two phasors of the sinusoidal signal. Delta pulses can not be measured as such in practice, and for this reason they are depicted as two arrows at frequencies $\theta = \pm 0.28 \pi$ in the figure, to indicate the location of the phasors.
In practice we can only measure and process a finite part of an infinite long signal. This can be achieved by a multiplication of the infinite long original signal $x[n]$ with a finite length window function $w[n]$. In this example we will use a length $N$ rectangular window which results in the following windowed signal $x_{win}[n]$:
$$
x_{win}[n] = x[n] \cdot {\color{blue}w[n]} \hspace{3mm} \text{with} \hspace{3mm}
\color{blue}{w[n]}=\begin{cases}
1 & n=0, \cdots , N-1 \newline
0 & \text{elsewhere}
\end{cases}
$$
The FTD of a rectangular function results in a Dirichlet function. Its main lobe width is inversely proportional to the window length $N$. Thus the longer the window length, the smaller the main lobe width. Furthermore, as a general rule of thumb, we have seen that multiplication in time domain results in convolution in frequency domain. As a result, the FTD of the finite length windowed signal $x_{win}[n]$ with $N=32$ is a continuous frequency function. This result is depicted as a solid line in blue: The delta pulses are smeared out by the shape of the Dirichlet function.

When applying a $N=32$ point DFT to this finite length signal $x\_{win}[n]$ the result is a sampled version of the blue solid line, the FTD of $x\_{win}[n]$, from which the inter frequency sampling distance equals $2\pi/32$. This DFT result is depicted by the green diamonds in the figure. From this result we can see that, depending on the relative frequency of the original signal $x[n]$ and on the choice of $N$, the DFT samples may or may not coincide exactly with the original phasor frequencies.
Finally, we apply zero padding, in this case up to a length of $4N=128$. The result of the $4N$-point DFT is a sampled version of the blue solid line, the FTD of $x\_{win}[n]$, from which the inter frequency sampling distance equals $2\pi/128$. This DFT result is depicted by red spots in the figure. The underlying FTD of the length $N$ windowed signal $x\_{win}[n]$ is sampled with a finer grid and the position of the phasor peaks is shown more accurate by the DFT result.
Finally it is important to note that by increasing the zero padding more and more, that is using a DFT which is much larger than the $N$ samples of $x\_{win}[n]$, we can make the sampling grid of the underlying FTD result of $x\_{win}[n]$ finer and finer. However the main lobe width of the underlying Dirichlet function, as depicted by the solid blue line in the figure, can not be reduced by zero padding. The smearing out behavior, or the resolution of the spectral content of the underlying signal $x[n]$, can only be reduced by increasing the window length $N$, thus taking more samples of the original signal $x[n]$ into account for the calculation of the DFT.
</div>
</div>


<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Zero padding increases the plot resolution but not the resolution of the spectral content of the underlying signal.</i></div>

<div class="example">
<h4> Example </h4>
<hr>
The frequency content of the sinusoidal signal $x[n]=\sin(n \cdot \frac{\pi}{2})$ contains two peaks representing the two phasor frequencies. Reason out in which region you can find these two peaks for a 6-point DFT of $x[n]$.
<button class="collapsible">Show solution</button>
<div class="content">
The phasor frequencies are located at the frequencies $\theta = \pm \frac{\pi}{2}$.
The number of samples in one period of $x[n]$ is 4. Because of the fact that 6 is not a 4-fold, the phasor peaks will be smeared out. The inter sample distance for the 6-point DFT domain is $\frac{2\pi}{6}= \frac{\pi}{3}$. Thus the phasor frequency $\theta = \frac{\pi}{2}$ is in between the frequency indices $k=1$ and $k=2$.
The phasor frequency $\theta = -\frac{\pi}{2}$ is in between the frequency indices $k=-1$ and $k=-2$, which becomes, by mod(6) counting, in between the frequency indices $k=4$ and $k=5$.
</div>
</div>


### Non periodic signals of infinite duartion
In this subsection we will show that the $N$-point DFT of a signal of infinite duration will always be an approximation. As example we use the infinite duration signal $x[n]=(0.7)^n u[n]$:
An exponential decaying function which starts at time index $n=0$. The first samples of $x[n]$ are depicted at the left hand side of Fig. 15.
The FTD of this function is obtained as follows:
$$
X(e^{j\theta} = \sum\_{n=-\infty}^{\infty} x[n] e^{-j\theta n}
= \sum\_{n=0}^{\infty} \left ( 0.7 \right )^n e^{-j\theta n} =
\sum\_{n=0}^{\infty} \left ( 0.7   e^{-j\theta } \right )^n =
\frac{1}{1 - 0.7 e^{-j\theta }}
$$
A plot of $|X(e^{j\theta}|$ is depicted in the right hand side of Fig. 15, which clearly shows the low frequency behavior of the exponential decaying function.

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/DFT/InfTimePEN3.svg"
    style="width:100%">
    <figcaption>
      $x[n]$ and periodic extension ($N=3$).
    </figcaption>
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/DFT/InfDFTN3.svg"
    style="width:100%">
    <figcaption>
      FTD and DFT ($N=3$).
    </figcaption>
  </div>
</div>
<figcaption class="numbered">
  FTD and DFT ($N=3$) of infinite duration signal.
</figcaption>
</figure>

When applying a DFT of length $N=3$, we use the first 3 samples of $x[n]$, that is samples 0,1 and 2,  which results in 3 DFT coefficients $X[k]$ with an inter frequency sample distance of $2\pi/3$.  The samples $|X[k]|$ are shown in red at the right hand side of Fig. 15.
From these samples we clearly see that the samples are not exactly the same as the sampled versions of the FTD result. The main reason is the period extended behavior of the DFT operation. The 3 resulting DFT samples, represent the frequency content of the first 3 samples of $x[n]$  which have been periodically extended, as shown by signal $x_p[n]$ at the left hand side figure. From this periodic extended signal we can clearly see the mismatch between the original signal samples $x[n]$ and the periodic extended signal $x_p[n]$.


<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/DFT/InfTimePEN6.svg"
    style="width:100%">
    <figcaption>
      $x[n]$ and periodic extension ($N=6$).
    </figcaption>
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/DFT/InfDFTN6.svg"
    style="width:100%">
    <figcaption>
      FTD and DFT ($N=6$).
    </figcaption>
  </div>
</div>
<figcaption class="numbered">
  FTD and DFT ($N=6$) of infinite duration signal.
</figcaption>
</figure>

It is obvious that we can improve the result by using more samples of signal $x[n]$, that is increasing the length $N$ of the DFT. In the plots of Fig. 16 the DFT length $N$ is increased to $N=6$. In general however, the DFT will always be an approximation of the FTD when the signal has infinite length.
In general the use of a length $N$ DFT for a signal of infinite duration causes aliasing in time domain. This can be proven as follows, for $k,n = 0,1, \cdots, N-1$:
\begin{eqnarray}
&Y[k]= X(e^{j\theta})|\_{\theta = k \cdot \frac{2 \pi}{N}} =
\sum\_{l=-\infty}^{\infty} x[l] e^{-j\frac{2 \pi}{N} kl}& \\
&\hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm}& \\
&y[n]=\frac{1}{N} \sum\_{k=0}^{N-1} Y[k] e^{j2 \pi nk/N} =
\sum\_{m=-\infty}^{\infty} x[n-m N]&
\end{eqnarray}

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The DFT of an infinite duration discrete time signal is always an approximation. Exact spectral content can only be obtained by an FTD.</i></div>


<div class="example">
<h4> Example </h4>
<hr>
The $N$-point DFT of an infinite length signal is always too short in order to capture all signal samples. As a result there will always be a mismatch between the FTD and the DFT frequency samples. In this example first calculate the FTD $X(e^{j\theta})$ of a signal which consists of 4 samples
$x[n]=\delta[n]+\delta[n-1]+\delta[n-2] +\delta[n-3$.
Then calculate a too short DFT of length 3 and show that this 3-point DFT result is not a sampled version of this FTD. Finally show that the 4-point DFT is a valid sampled version of the FTD.
<button class="collapsible">Show solution</button>
<div class="content">
$$
X(e^{j\theta}) = \sum_{n=0}^{3} e^{-jn \theta} = \frac{\sin(2 \theta)}{\sin (\frac{1}{2} \theta)} \cdot e^{-j\frac{3}{2} \theta}
$$
The FTD is depicted as a black solid line in the figure below.
For $N \leq 4$ the $N$-point DFT is equal to:
$$
X_p[k]= \sum_{n=0}^{N-1} e^{-j\frac{2\pi}{N} k n} = N \delta [k \text{mod}(N)]
$$
Thus for $N=3$ we have $X_p[k]=3 \delta [k \text{mod}(3)]$ and for $N=4$ the result is
$X_p[k]=4 \delta [k \text{mod}(4)]$. Besides the FTD results in the figure below, it also shows the 3-point DFT result (blue dots in figure at the top), which is clearly not a sampled version of the FTD, while the 4-point DFT result (red dots in the figure at the bottom) is a sampled version of the FTD.
<div style="max-width: 500px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/DFT/contExample.svg"
      alt="FTD of length 4 signal together with 3-point DFT (top figure, blue dots) and 4-point DFT (bottom figure, red dots)."
    />
    <figcaption>
      FTD of length 4 signal together with 3-point DFT (top figure, blue dots) and 4-point DFT (bottom figure, red dots).
    </figcaption>
  </figure>
</div>
</div>
</div>


<br></br>

## DFT for continuous time signals
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

<!--
\section{FFT}\label{sect:FFT}
{\em To be finilized}
\\
A very efficient implementation of the DFT is the so called Fast Fourier Transform, abbreviated as FFT. Together with the convolution property this is the main reason for the existence of the DFT.
-->
<br></br>

## Summary

<b><u> Definition: </u></b>
$$
\boxed{
\begin{eqnarray}
\text{DFT: } X\_p[k] = \sum\_{n=0}^{N-1} x\_p[n] e^{-j\frac{2 \pi}{N} k n}
\hspace{3mm} \color{red}{\bf \forall k}
\qquad
\text{IDFT: } x\_p[n] = \frac{1}{N} \sum\_{k=0}^{N-1} X\_p[k] e^{j\frac{2 \pi}{N} k n} \hspace{3mm} \color{red}{\bf \forall n}
\end{eqnarray}}
$$

<ul>
<li> Both DFT and IDFT <u>discrete</u> and <u>periodic</u>. </li>
<li> <u>Periodic extension (PE):</u> $\\ \qquad$ Choose $N$ succeeding samples of $x[n]$ (usually for $n=0,1, \cdots, N-1$) and repeat these samples. This results in the periodic signal $x_p[n]= x[(n \cdot \text{mod(N)})]$.
</ul>

<b><u> DFT properties: </u></b>
<ul>
<li> <u>DFT summation property:</u> With twiddle factor $W_N=e^{j\frac{2 \pi}{N}}$

$$
\boxed{
S[k]= \sum\_{n=0}^{\color{red}{N}-1} \left \\{ W\_{\color{red}{N}}^k \right \\} ^n =
\sum\_{n=0}^{\color{red}{N}-1} \left \\{ \text{e}^{j \frac{2\pi}{\color{red}{N}} k } \right \\} ^n = \color{red}{N}  \delta [\color{blue}{k} \text{ mod}(\color{red}{N})]
}
$$
</li>
<li> <u> Linearity:</u>
$$
a x_{p,1}[n]+bx_{p,2}[n] \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} a X_{p,1}[k] + b X_{p,2}[k]
$$
</li>
<li> <u> Circular shift: </u>
\begin{eqnarray}
\text{Time shift:} \hspace{8.5mm} x_p[n-n_0] &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& e^{-j\frac{2 \pi}{N} k n_0} \cdot X_p [k] \newline
\text{Frequency shift:} \hspace{3mm} e^{j\frac{2 \pi}{N} n k_0} \cdot x_p[n] &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X_p[k-k_0]
\end{eqnarray}
</li>
<li> <u> Circular convolution: </u>
$$
x_p[n] \circledast h_p[n] =\sum_{i=0}^{N-1} x_p[i] h_p[n-i]= \sum_{i=0}^{N-1} x_p[n-i] h_p[i]
\hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm}  X_p[k] \cdot H_p[k]
$$
$$
x_p[n] \cdot h_p[n] \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm}  X_p[k] \circledast H_p[k]
$$
</li>

<li> <u>Complex conjugation:</u>
$$
x_p^\ast[n] \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} X_p^\ast[N-k]
$$
$$
x[n] \text{ real } \Rightarrow \text{ } X_p[k]=X^\ast_p[N-k]
$$
</li>
<li> <u>Preserve energy (Parceval):</u>
$$
\sum_{n=0}^{N-1} |x_p[n]|^2 = \sum_{k=0}^{N-1} | X_p[k]|^2
$$
</li>
</ul>

<b><u>Linear by circular convolution:</u></b>
<ul>
<li><u>Convolution two finite duration signals:</u>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>If signal $x[n]$ consists of $N_1$ samples and $h[n]$ of $N_2$ samples the result of the linear convolution $y[n] = x[n] \star h[n]$ can be obtained from a circular convolution $y_p[n]=x_p[n] \circledast h_p[n]$ in which both periodic extended $x_p[n]$ and $h_p[n]$ are padded with zeros up to a length of $N \geq N_1 + N_2 -1$ samples.</i></div>
</li>
<li><u>Convolution infinite duration with finite duration signal:</u>
<!-- TODO: As depicted in Fig. \ref{Fig:overlapadd}, -->The overlap-add procedure is as follows:
<ol>
<li> Split $x[n]$ in length $M \geq 1 (L)$ non-overlapping segments </li>
<li> Calculate $y_i[n]=h[n] \star x_i[n]$ (efficiently with FFT's) </li>
<li> Add last $L-1$ samples previous segment with first samples current segment</li>
<li> $y[n]= \sum_{i=0}^{\infty} y_i[n-Mi]$</li>
</ol></li>
<!-- TODO: As depicted in Fig. \ref{Fig:overlapsave}, -->
The overlap-save procedure is as follows:
<ol>
<li> Split $x[n]$ in length $M \geq L-1$ overlapping segments, overlap $L-1$ </li>
<li> Calculate $y_i[n]=h[n] \star x_i[n]$ (efficiently with FFT's) </li>
<li> Construct $\tilde{y}_i[n]$: Discard first $L-1$ samples, last $N=M-L+1$ are correct </li>
<li> $y[n]= \sum_{i=0}^{\infty} \tilde{y}_i[n-Mi]$ </li>
</ol>
</ul>

<b><u>How choose DFT length $N$</u></b>

<ul>

<li> <u>Periodic signals: </u>
With integer $\lambda$, if DFT length $N$ $\neq \lambda \times \#$ samples in one period
$\Rightarrow$ Artefacts during PE $\Rightarrow$ Use windowing.
</li>

<li> <u>Signals of finite duration $M \leq N$:</u>
DFT coefficients sampled version of FTD: $X[k]= X(e^{j\theta})\mid_{\theta = k \cdot \frac{2 \pi}{N}}$
<br>
<i>Note: For $N>M$:Zero padding with $N-M$ zeros:</i>
<ul>
<li> Increase resolution spectral plot </li>
<li> No extra spectral information of underlying signal </li>
</ul>

</li>
<li> <u>Non periodic infinite length signals:</u>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The DFT of an infinite duration signal is always an approximation. Exact spectral content can only be obtained by an FTD.</i></div>
</li>
</ul>


<b><u>DFT for continuous signals:</u></b>
Time- bandwidth product constant $\Rightarrow$ $T \cdot \Delta \omega = 2 \pi /N$

<!-- TODO:
\section*{FFT:}
-->
