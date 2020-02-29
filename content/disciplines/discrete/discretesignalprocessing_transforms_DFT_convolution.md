+++
title = "Convolution implementation"

# date = {{ .Date }}
lastmod = 2019-11-27

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Convolution implementation"
  weight = 4
  parent = "Transforms II: Discrete Fourier transform"

+++


If we want to perform a filter operation in practice then we need a linear and not a circular convolution. In this section we will show how a circular convolution can be used to realize a linear convolution between two signals $x[n]$ and $h[n]$.

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

<br></br>
## Convolution of two finite duration signals
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
Fig. 2 shows an example of the linear convolution of $x[n]$ and $h[n]$, which are defined as follows:
\begin{eqnarray}
x[n]&=&\delta[n]+ \delta[n-1] + \delta[n-2] + \frac{1}{2} \delta[n-3] \\
h[n]&=&\delta[n]+ \frac{3}{4} \delta[n-1] + \frac{1}{2}\delta[n-2] + \frac{1}{4} \delta[n-3]
\end{eqnarray}
The result $y[n]=x[n] \star h[n]$ has finite duration of $N=N_1 + N_2 -1=7$ samples:
$$
y[n]=\delta[n]+ \frac{7}{4} \delta[n-1] + \frac{9}{4}\delta[n-2] + 2 \delta[n-3]+
\frac{9}{8} \delta[n-4]+ \frac{1}{2} \delta[n-5]+ \frac{1}{8} \delta[n-6]
$$
Despite the fact that within the FP both  $x_p[n]$ and $h_p[n]$ of Fig. 1 are the same as the signals $x[n]$ and $h[n]$ of Fig. 2, it is clear that the FP of the circular convolution result $y_p[n]$ does not result in the desired linear convolution result $y[n]$.
However when first pad both $x_p[n]$ and $h_p[n]$ with zeros up to a length of $N=7$, as depicted in Fig. 3 by $x_{p,b}[n]$ and $h_{p,b}[n]$, then applying a circular convolution the result of $y_{p,b}[n]= x_{p,b}[n] \circledast h_{p,b}[n]$ within the FP is exactly the same as the linear convolution result.
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


Combining the previous procedure with the fact that a circular convolution is equivalent to a multiplication in the DFT frequency domain we will present a procedure to calculate a linear convolution by a circular one which is implemented in the DFT frequency domain. Referring to Fig. 4 the derivation of this procedure goes as follows:
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
