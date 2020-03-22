+++
title = "Transforms II: Discrete Fourier transform"

# date = {{ .Date }}
lastmod = 2019-11-27

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Transforms II: Discrete Fourier transform"
  weight = 52


+++


## Summary

<b><u> Definition: </u></b>
$$
\boxed{
\begin{eqnarray*}
\text{DFT: } X\_p[k] = \sum\_{n=0}^{N-1} x\_p[n] e^{-j\frac{2 \pi}{N} k n}
\hspace{3mm} \color{red}{\bf \forall k}
\qquad
\text{IDFT: } x\_p[n] = \frac{1}{N} \sum\_{k=0}^{N-1} X\_p[k] e^{j\frac{2 \pi}{N} k n} \hspace{3mm} \color{red}{\bf \forall n}
\end{eqnarray*}}
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
\begin{eqnarray*}
\text{Time shift:} \hspace{8.5mm} x_p[n-n_0] &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& e^{-j\frac{2 \pi}{N} k n_0} \cdot X_p [k] \newline
\text{Frequency shift:} \hspace{3mm} e^{j\frac{2 \pi}{N} n k_0} \cdot x_p[n] &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X_p[k-k_0]
\end{eqnarray*}
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
