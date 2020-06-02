+++
title = "Length of DFT"

# date = {{ .Date }}
lastmod = 2019-11-27

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Length of DFT [⯈]"
  weight = 5
  parent = "Transforms II: Discrete Fourier transform"

+++

## Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/OXN9aW6ETKY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>

In practice we often use a DFT, or its efficient version the Fast Fourier Transform (FFT), algorithm to calculate a description of a signal in frequency domain. As discussed before, the DFT is related to the FTD and FTC but it is certainly not the same: The DFT uses only a finite set of $N$ samples, is discrete and periodic in both time and frequency domain. In this section we will explain which implications the choice of the length $N$ will have for the relation between the DFT and the FTD. We will do this for signals with finite duration, periodic signals and non-periodic signals with infinite duration.

<br></br>
## Signals with finite duration
An example of a finite duration signal of $M$ samples is depicted in Fig. 1.
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

The first example is a finite duration signal of $M=8$ samples, as depicted at the left hand side  Fig. 2. The FTD result $|X(e^{j\theta})|$, is depicted in a black drawn curve at the right hand side of the same figure. The relative frequency $\theta$ ranges from 0 until $2\pi$.

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



The result of an 8-point DFT $|X[k]|$, depicted in red bars at the right hand side of Fig. 2, which is clearly a sampled version of the FTD. The inter frequency sample distance is $\frac{2\pi}{8}$.

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


Increasing the signal length $x[n]$ with zeros, which is called <b> zero padding </b>, does not influence the resulting FTD equation. The zero padded signal and its FTD are shown in Fig. 3. On the other hand when applying a $N=16$-point DFT  to the zero padded signal, the resulting DFT samples $X[k]$ represent a sampled version of the FTD with an inter frequency sampling distance is $\frac{2\pi}{16}$, as shown in red bars at the right hand side of
Fig. 3.

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

<br></br>
## Periodic signals
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

The plot at the left hand side of Fig. 4 shows $N=12$ samples of the periodic sinusoidal signal $x[n]=\cos(\frac{2\pi}{6}n)$. Because of the fact that 12 is a 6-fold, the 12 samples represent exactly two periods of $x[n]$. The plot at the right hand side of the figure show the result of a 12-point DFT, in which we see two frequency peaks at indices $k=2$ and $k=10$. Via modulo counting it follows that the index $k=10$ is equivalent to index $k=10-12=-2$ in this case. Furthermore the inter frequency distance of the 12-point DFT is $\frac{2\pi}{12}$ which implies that the two frequency indices $k=2$ and $k=-2$ are related to the two relative frequencies $\theta= 2 \cdot \frac{2\pi}{12}= \frac{2\pi}{6} $ and $\theta= -2 \cdot \frac{2\pi}{12}= -\frac{2\pi}{6} $ which are indeed the two phasor frequencies of the sinusoidal signal $x[n]$.
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

However when using $N=16$ samples, which is not a 6-fold, the 16-point DFT result shows two smeared out peaks as shown at the right hand side of Fig. 5.
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
Concluding it follows that the 12-point DFT of the periodic sinusoidal signal $x[n]=\cos(\frac{2\pi}{6}n)$ results into two peaks at frequency indices $k=2$ and $k=10$ respectively, which is indeed the same result as shown at the right hand side of Fig. 4.
Applying similar steps for the evaluation of a 16-point DFT of the same periodic sinusoidal signal $x[n]=\cos(\frac{2\pi}{6}n)$ the result is as follows:
\begin{eqnarray*}
X[k]&=&\sum_{n=0}^{\color{red}{16}-1} \cos (\frac{2\pi}{\color{purple}{6}}n) e^{-j(\frac{2\pi}{\color{red}{16}})k n} =\frac{1}{2} \sum_{n=0}^{\color{red}{16}-1} \left \{ e^{j\frac{2\pi}{\color{brown}{6}} n}
+  e^{-j\frac{2\pi}{\color{brown}{6}} n}  \right \}
e^{-j\frac{2 \pi}{\color{red}{16}}k n} \nonumber \\
&=& \frac{1}{2} \sum_{n=0}^{\color{red}{16}-1} \left \{e^{j\frac{2\pi}{16} \color{yellow}{(\frac{16}{6} - k)}n} +
e^{-j\frac{2\pi}{16}\color{orange}{(\frac{16}{6} + k)}}n \right \}
\end{eqnarray*}
However when trying to apply the basic DFT summation property it follows that in the first summation the frequency index $k$ should be equal to $\frac{16}{6} \approx 2.7$, which is not an integer value. In other words the basic DFT summation property can not be applied to the first summation and the result of this summation will add up to a non zero value for all frequency indices $k$. A similar reasoning follows for the second summation: The frequency index $k$ should be equal to $-\frac{16}{6}$, which becomes $-\frac{16}{6}+ 16 \approx 13.3$ when taking into account modulo 16 calculation. This implies that the 16-point DFT result of the sinusoidal signal $x[n]=\cos(\frac{2\pi}{6}n)$ results in two <b> smeared out</b> peaks around integer indices $k$ which are close to the values 2.7 and 13.3, which is shown in the 16-point DFT plot of Fig. 5.
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

<br></br>
## Non periodic signals of infinite duration
In this subsection we will show that the $N$-point DFT of a signal of infinite duration will always be an approximation. As example we use the infinite duration signal $x[n]=(0.7)^n u[n]$:
An exponential decaying function which starts at time index $n=0$. The first samples of $x[n]$ are depicted at the left hand side of Fig. 6.
The FTD of this function is obtained as follows:
$$
X(e^{j\theta}) = \sum\_{n=-\infty}^{\infty} x[n] e^{-j\theta n}
= \sum\_{n=0}^{\infty} \left ( 0.7 \right )^n e^{-j\theta n} =
\sum\_{n=0}^{\infty} \left ( 0.7   e^{-j\theta } \right )^n =
\frac{1}{1 - 0.7 e^{-j\theta }}
$$
A plot of $|X(e^{j\theta}|$ is depicted in the right hand side of Fig. 6, which clearly shows the low frequency behavior of the exponential decaying function.

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

When applying a DFT of length $N=3$, we use the first 3 samples of $x[n]$, that is samples 0,1 and 2,  which results in 3 DFT coefficients $X[k]$ with an inter frequency sample distance of $2\pi/3$.  The samples $|X[k]|$ are shown in red at the right hand side of Fig. 6.
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

It is obvious that we can improve the result by using more samples of signal $x[n]$, that is increasing the length $N$ of the DFT. In the plots of Fig. 7 the DFT length $N$ is increased to $N=6$. In general however, the DFT will always be an approximation of the FTD when the signal has infinite length.
In general the use of a length $N$ DFT for a signal of infinite duration causes aliasing in time domain. This can be proven as follows, for $k,n = 0,1, \cdots, N-1$:
\begin{eqnarray*}
&Y[k]= X(e^{j\theta})|\_{\theta = k \cdot \frac{2 \pi}{N}} =
\sum\_{l=-\infty}^{\infty} x[l] e^{-j\frac{2 \pi}{N} kl}& \newline
&\hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm}& \newline
&y[n]=\frac{1}{N} \sum\_{k=0}^{N-1} Y[k] e^{j2 \pi nk/N} =
\sum\_{m=-\infty}^{\infty} x[n-m N]&
\end{eqnarray*}

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
