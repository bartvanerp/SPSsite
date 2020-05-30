+++
title = "DFT properties"

# date = {{ .Date }}
lastmod = 2019-11-27

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "DFT properties [⯈]"
  weight = 3
  parent = "Transforms II: Discrete Fourier transform"

+++

## Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/0yRxU3HQWto" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>

In this section we will discuss the main DFT properties. We will see that most of these properties look similar to the properties of other Fourier transforms however there are some important differences which are caused by the fact that the DFT is a periodic, or circular, operation.

<br></br>
## Circular shift
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

The two figures at the left hand side of Fig. 1 show a signals $x[n]$ and its shifted version $x[n-1]$ which has been shifted over one sample to the right. More specifically the red sample at index $n=0$ moves to index $n=1$ and the blue sample at index $n=3$ moves to index $n=4$.
The two figures at the right hand side of Fig. 1 shows the Periodic Extended signal $x_p[n]$, with period $N=4$ samples, and its shifted version $x_p[n-1]$. From these figures it is clear that $x_p[n-1]$ and  $x[n-1]$ are not the same. More specifically for $x_p[n-1]$ the blue sample at index $n=3$ is moved out the FP at the right hand side while it enters again at the left hand side at index $n=0$.  This circular, or periodic, behavior can be represented by using modulo counting as follows: The samples denoted by $x_p[(n-1) \text{mod}N]$ represent the samples in the FP of $x_p[n]$ which has been shifted over one sample.

For the proof of the circular shift property, we need an explicit expression for this modulo representation, which can be derived as follows:

Fig. 2 represents the time index axis $n$ which ranges from $-\infty$ until $+\infty$. One interval of the periodic extended signal $x_p[n]$  consists of $N$ samples and the indices of the FP range from $0$ until $N-1$. Now we shift $x_p[n]$ over $n_0$ samples, in which we assume for simplicity $n_0 \leq 0$.
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
\begin{eqnarray*}
Y[k]
&=& \sum_{\in {\color{red}{\bf -}}} \color{red}{x_p[n-n_0 + \lambda N]} e^{-j\frac{2\pi}{N} k n}
+ \sum_{\in {\color{blue}{\bf -}}} \color{blue}{x_p[n-n_0 + \lambda N -N ]} e^{-j\frac{2\pi}{N} k n}
\end{eqnarray*}
Substitute a new index $m$ and replace the index $n$ with this new index in the complex exponent of both summations:
$$
Y[k]= \sum_{m \in {\color{red}{\bf -}}} \color{red}{x_p[m]} e^{-j\frac{2\pi}{N} k (m+n_0 - \lambda N)}
+ \sum_{m \in {\color{blue}{\bf -}}} \color{blue}{x_p[m]} e^{-j\frac{2\pi}{N} k (m+n_0 - \lambda N + N)}
$$
The complex exponent with index $n_0$ can be taken outside brackets:
\begin{eqnarray*}
Y[k] &=&\left (
\sum_{m \in {\color{red}{\bf -}}} {\color{red}x_p[m]} e^{-j\frac{2\pi}{N} k m } e^{j\frac{2\pi}{N}k \lambda N}
+ \sum_{m \in {\color{blue}{\bf -}}} {\color{blue}x_p[m]} e^{-j\frac{2\pi}{N} k m}
e^{j\frac{2\pi}{N} k (\lambda -1) N}
\right )  e^{-j\frac{2\pi}{N} k n_0} \\
&=&
\left ( \sum_{m \in {\color{red}{\bf -}}} {\color{red}x_p[m]} e^{-j\frac{2\pi}{N} k m } +
\sum_{m \in {\color{blue}{\bf -}}} {\color{blue}x_p[m]} e^{-j\frac{2\pi}{N} k m}
  \right ) \cdot e^{-j\frac{2\pi}{N} k n_0}
\end{eqnarray*}
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
\begin{eqnarray*}
y_p[n] = e^{-j\frac{2\pi}{5}2n} \cdot x_p[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
Y_p[k] = X_p[k+2]]
\end{eqnarray*}
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


<br></br>
## Circular convolution
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
is depicted in Fig. 3.

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
\begin{eqnarray*}
x\_p[n]&=&\delta[n]+ \delta[n-1] + \delta[n-2] + \frac{1}{2} \delta[n-3] \newline
h\_p[n]&=&\delta[n]+ \frac{3}{4} \delta[n-1] + \frac{1}{2}\delta[n-2] + \frac{1}{4} \delta[n-3]
\end{eqnarray*}
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
\begin{eqnarray*}
x_p[n] &=& \delta[n \text{mod}(4)] + 2\delta[(n-1) \text{mod}(4)] + \delta[(n-2) \text{mod}(4)] - \delta[(n-3) \text{mod}(4)] \newline
h_p[n] &=& \frac{1}{3} \delta[(n-1) \text{mod}(4)] -\frac{1}{3} \delta[(n-2) \text{mod}(4)] +\frac{1}{3} \delta[(n-3) \text{mod}(4)]
\end{eqnarray*}
<button class="collapsible">Show solution</button>
<div class="content">
A matlab animation is to be added.
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
\begin{eqnarray*}
Y[k]&=& \text{DFT}\left \{ x_p[n] \circledast h_p[n]\right \} =\sum_{n=0}^{N-1} \left (\sum_{i=0}^{N-1} x_p[i] h_p[n-i] \right ) e^{-j(2 \pi/N) k n}\\
&=&\sum_{i=0}^{N-1} x_p[i] \cdot \left \{ \sum_{n=0}^{N-1} h_p[n-i] e^{-j(2 \pi/N) k n} \right \}
\end{eqnarray*}
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
\begin{eqnarray*}
x_p[n] &=& \delta[n \text{mod}(4)] + 2\delta[(n-1) \text{mod}(4)] + \delta[(n-2) \text{mod}(4)] - \delta[(n-3) \text{mod}(4)] \\
h_p[n] &=& \frac{1}{3} \delta[(n-1) \text{mod}(4)] -\frac{1}{3} \delta[(n-2) \text{mod}(4)] +\frac{1}{3} \delta[(n-3) \text{mod}(4)]
\end{eqnarray*}
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
\begin{eqnarray*}
X_p[k] &=& 1 + 2 e^{-j\frac{2\pi}{4} k} + e^{-j\frac{2\pi}{4} 2k} - e^{-j\frac{2\pi}{4} 3k} \\
H_p[k] &=& \frac{1}{3} \left \{e^{-j\frac{2\pi}{4} k} -e^{-j\frac{2\pi}{4} 2k} + e^{-j\frac{2\pi}{4} 3k} \right \}
\end{eqnarray*}
resulting in $Y_p[k] = X_p[k] \cdot H_p[k]= e^{-j\frac{2\pi}{4} k}$.
</div>
</div>

<br></br>
## Complex conjugation
The periodic behavior of the DFT operation leads to a special result of the complex conjugation operation:
$$
\boxed{x_p^\ast[n] \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} X_p^\ast[N-k]}
$$

<div class="example">
<h4> Proof of complex conjugation property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
In the first step  of the proof we apply the DFT operation to the complex conjugated samples and take the complex operation outside the brackets and  multiply with 1:
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
\begin{eqnarray*}
x_p[n] &=& e^{j\theta_0} \cdot e^{j\frac{2\pi}{N} n} + e^{-j\theta_0} \cdot e^{j\frac{2\pi}{N}(N-1) n} \\
&=& e^{j\theta_0} \cdot e^{j\frac{2\pi}{N} n} + e^{-j\theta_0} \cdot e^{-j\frac{2\pi}{N} n} =
2 \cos (\frac{2\pi}{N} n + \theta_0)
\end{eqnarray*}
</div>
</div>

<br></br>
## Preserve energy (Parceval)
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
\begin{eqnarray*}
\text{Time} &:& \sum_{n=0}^{3} |x_p[n]|^2 = (1^2 + 1^2 + 1^2 + 1^2)=4 \\
\text{Frequency} &:& \frac{1}{4} \sum_{k=0}^{3} |X_p[k]|^2 = \frac{1}{4} ( 4^2 ) = 4
\end{eqnarray*}
which proves that the Parceval relation is indeed correct.
</div>
</div>
