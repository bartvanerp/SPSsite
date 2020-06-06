+++
title = "Special convolutions"

# date = {{ .Date }}
lastmod = 2020-04-04

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Special convolutions [⯈]"
  weight = 6
  parent = "Discrete-time systems"
+++

## Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/14CktMnfdl8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>

In many practical situations a measured signal $x[n]$, which is assumed to be zero for $n<0$, must first be cleaned up before further processing. This is done by filtering the measured samples of $x[n]$ with a filter with impulse response $\hat{h}[n]$. In such situations the number of samples of the measured signal $x[n]$ can be extremely long, while the length $L$ of the impulse response $\hat{h}[n]$ is much smaller. Thus the problem at hand is to calculate the following extreme, or '$\infty$', long convolution sum in an efficient way:
\begin{equation}\label{eq:longconv}
y[n]=\hat{h}[n] \ast x[n] = \sum_{k=0}^{L-1} \hat{h}[k] x[n-k]
\hspace{5mm} %x[n]=0 \mbox{ for } n<0
\color{red}{\text{Length  }}  x[n] {\color{red}{\bf \gg} }L.
\end{equation}
In a followup module we will show that the convolution sum of a signal $x[n]$ with a length $L$ impulse response $\hat{h}[n]$ can be computed very efficiently with the use of Fast Fourier Transforms (FFT's). Typically FFT's process each iteration one block of $N$ samples and for this approach it is necessary that all data is processed in blocks of $N$ samples. The block length $N$ can be long but certainly not as long as the '$\infty$' length of sequence $x[n]$. This efficient block processing approach implies that all sequences, the signal to be filtered, the impulse response and the output of our problem at hand, as described in equation (\ref{eq:longconv}), must be split in blocks of the same length of $N$ samples. In case a sequence does not have a length of $N$ samples it can easily be extended by padding it with zeros.

In the following subsections we will discuss two different of such block processing approaches to tackle the '$\infty$' long convolution problem (\ref{eq:longconv}).
For both approaches we assume a block length of ${\color{red}{N}}$ samples and a length ${\color{blue}{L}}$ impulse response $\hat{h}[n]$, with $L<N$. This impulse response is zero padded up to a length $N$ impulse response $h[n]$ as follows:
$$
h[n] = \left \\{
\begin{array}{cl}
\hat{h}[n] & n=0,1, \cdots L-1 \newline
0 & n=L, \cdots , N-1
\end{array}
\right .
$$
Note that with this zero padded description of the impulse response, the original convolution sum (\ref{eq:longconv}) can be written as:
\begin{equation}\label{eq:longconv1}
y[n] = \hat{h}[n] \star x[n] \equiv h[n] \star x[n] = \sum_{k=0}^{L-1} h[k] x[n-k]
\end{equation}

<br></br>
## Overlap-add method
The first, so called overlap-add, approach is based on the ${\color{red}{\text{complete convolution}}}$ of two blocks.

<div style="max-width: 400px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/completeconv.svg"
      alt="Complete convolution of two blocks."
    />
    <figcaption class="numbered">
      Complete convolution of two blocks.
    </figcaption>
  </figure>
</div>
Referring to Fig. 1 this can be explained as follows:

The convolution sum of a sequence $x[n]$ of $M$ samples with an impulse response of $L$ samples results in an output sequence $y[n]$ which consists of $N=M+L-1$ samples.
As indicated in the figure, the first and last $L-1$ samples are 'fade-in' (fi) and 'fade-out' (fo) samples respectively. In order not to have an overlap between fade-in and fade-out regions we assume $M \geq L$.

In the overlap-add method, as depicted in Fig. 2, the '$\infty$' long sequence $x[n]$ is partitioned into ${\color{red}{\text{non-overlapping}}}$ subsequences ('blocks') $x_i[n]$ of length $M$, thus:
\begin{eqnarray*}
x[n]= \sum_{i=0}^{\infty} x_i[n] &\text{with} &
x_i[n]= \left \\{
\begin{array}{cl}
x[n+M \cdot i] & n=0,1, \cdots M-1 \newline
0 & \mbox{else}
\end{array}
\right .
\end{eqnarray*}
With this non overlapped splitting we can rewrite the convolution sum
(\ref{eq:longconv1}) as follows:
\begin{eqnarray*}
y[n] = h[n] \star x[n] &=& \sum_{k=0}^{L-1} h[k] x[n-k] \newline
&=& \sum_{k=0}^{L-1} h[k] \left ( \sum_{i=0}^{\infty} x_i[n-k] \right ) \newline
&=& \sum_{i=0}^{\infty} \left (
\sum_{k=0}^{L-1} h[k] x_i[n-k]  \right ) \newline
&=& \sum_{i=0}^{\infty} \left ( h[n] \star x_i[n] \right ) = \sum_{i=0}^{\infty} y_i[n]
\end{eqnarray*}
Each of the intermediate convolution sum results $y_i[n]$ consist of maximal $N=M+L-1$ non zero samples in which the first and last $L-1$ samples of each subsequence $y_i[n]$ are due to fade-in and fade-out.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/overlapadd.svg"
      alt="Overlap-add method with $M \geq L$."
    />
    <figcaption class="numbered">
      Overlap-add method with $M \geq L$.
    </figcaption>
  </figure>
</div>
The overlap-add procedure consists of the following steps:
<ul>
  <li> $i=0$:
  <ul>
    <li> Zero pad length $L$ impulse response up to length $N$, </li>
    <li> Zero pad length $M$ input sequence $x_0[n]$ up to length $N$, </li>
    <li> Calculate length $N$ convolution sum $y_0[n]= h[n] \star x_0[n]$, </li>
    <li> The first $M$ samples are valid convolution sum results: </li>
$$
y[n] = y_0[n] \mbox{ for } n=0, \cdots M-1
$$
  </ul></li>
  <li> $i \geq 1$:
  <ul>
    <li> Zero pad length $M$ input sequence $x_i[n]$ up to length $N$, </li>
    <li> Calculate length $N$ convolution sum $y_i[n]= h[n] \star x_i[n]$, </li>
    <li> Add last $L-1$ 'fade-out' samples of block $i-1$ and first $L-1$ 'fade-in'
samples of block $i$: </li>
$$
y[n] = \left \{
\begin{array}{ll}
y_{i-1}[n] + y_i[n] & \mbox{ for } n=i \cdot M, \cdots , i \cdot M + L-1 \\
y_i[n] & \mbox{ for } n=i \cdot M + L , \cdots , (i+1) \cdot M -1
\end{array}
\right .
$$
</ul></li>
</ul>

<br></br>
## Overlap-save method
The second approach, which is called overlap-save, is based on the $\color{red}{\text{partial convolution}}$ of two blocks.
<div style="max-width: 400px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/partialconv.svg"
      alt="Partial convolution of two blocks."
    />
    <figcaption class="numbered">
      Partial convolution of two blocks.
    </figcaption>
  </figure>
</div>
Referring to Fig. 3. this can be explained as follows:
The impulse response $h[n]$ consists of $L$ samples, while now the
Now the sequence $x[n]$ now consists of $N$ samples and the impulse response $h[n]$ consists of $L$ samples. Again $N=L+M-1$ but now with $M \geq 1$. In this case the resulting sequence $y[n]$ consists of $N$ samples from which the first $L-1$ samples are 'fade-in' samples and the last $L-1$ 'fade-out' samples are not computed.

In the overlap-save method, as depicted in Fig. 3, the '$\infty$' long sequence $x[n]$ is partitioned into ${\color{red}{\text{overlapping}}}$ blocks $x_i[n]$ of length $N=L+M-1$ with an overlap of $L-1$ samples:
$$
x_i[n] = \left \\{
\begin{array}{ll}
x[n + i \cdot M] & \mbox{ for } n=0,1, \cdots , {\color{red}N}-1 \newline
0 & \text{ else}
\end{array}
\right .
$$
<div style="max-width: 400px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/overlapsave.svg"
      alt="Overlap-save method with $N=M+L-1$ and $M \geq 1$."
    />
    <figcaption class="numbered">
      Overlap-save method with $N=M+L-1$ and $M \geq 1$.
    </figcaption>
  </figure>
</div>
Each intermediate convolution sum result $y_i[n]$ consists of maximal $N$ non zero samples in which the first $L-1$ samples are due to fade-in. The last $L-1$ 'fade-out' samples are not computed.
The overlap-save procedure consist of the following steps:
<ul>
  <li> $i=0$:
    <ul>
      <li> Zero pad length $L$ impulse response up to length $N$, </li>
      <li> Calculate the first $N$ samples of the convolution sum $y_0[n]= h[n] \star x_0[n]$: </li>
      <li> The first $N$ samples are valid convolution sum results:
      $$
      y[n] = y_0[n] \mbox{ for } n=0, \cdots N-1
      $$ </li>
  </ul></li>
  <li> $i \geq 1$:
    <ul>
      <li> Calculate the first $N$ samples of the convolution sum $y_i[n]= h[n] \star x_i[n]$: </li>
      <li> Discard the first $L-1$ 'fade in' samples and the last $M$ samples are valid convolution sum results:
        $$
        y[n] = y_i[n] \mbox{ for } n=L, \cdots N-1
        $$ </li>
    </ul></li>
</ul>

<br></br>

## Final notes
> The overlap-add procedure is based on ${\color{red}{\text{complete convolution}}}$ of ${\color{red}{\text{non-overlapping}}}$ blocks while the overlap-save procedure is based on ${\color{red}{\text{partial convolution}}}$ of $\color{red}{\text{overlapping}}$ blocks.

> For applications in which the filter coefficients do not change during processing of the '$\infty$' long sequence $x[n]$, it is valid to add the 'fade out' samples of iteration $i-1$ and 'fade in' samples of iteration $i$ since both use the same fixed impulse response. However, in adaptive filter applications the filter coefficients will change during the processing of the '$\infty$' long sequence $x[n]$ and it is not valid to add the 'fade out' samples of iteration $i-1$ and 'fade in' samples of iteration $i$.
    For this reason the overlap-add procedure is mainly used when the filter coefficients of the impulse response do not change while overlap-save is mainly used for adaptive applications.

> In a follow up module we will show how both block processing approaches can be implemented efficiently with the use of FFT's.
