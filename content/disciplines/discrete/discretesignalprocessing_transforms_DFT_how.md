+++
title = "The DFT"

# date = {{ .Date }}
lastmod = 2019-11-27

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "The DFT"
  weight = 2
  parent = "Transforms II: Discrete Fourier transform"

+++

<br></br>
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/cMsFFW8nyOU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>
## Periodicity DFT and Periodic Extension (PE)
In general a discrete time signal $x[n]$ can have an infinite amount of samples from which the sampling index $n$ ranges from $-\infty$ to $+\infty$, as depicted at the left hand side of Fig. 1. However when using the $N$-point DFT, we select $N$ samples of $x[n]$, typically ranging from time index $n=0$ until $n=N-1$. The frequency indices $k$ of the DFT resulting samples $X[k]$ also range from $k=0$ until $k=N-1$.
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
This periodic signal $x_p[n]$ can be constructed from the original signal $x[n]$  by first selecting the $N$ signal samples that are used in the DFT operation and then periodically repeat these samples. This Periodic Extension, abbreviated as PE, is depicted at the right hand side of Fig. 1. Obviously only one period of this period extended signal $x_p[n]$ is of importance.
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
\begin{eqnarray*}
\text{DFT: } X_p[k] = \sum\_{n=0}^{N-1} x_p[n] e^{-j\frac{2 \pi}{N} k n}
\hspace{3mm} {\color{red}\bf \forall k}
\qquad
\text{IDFT: } x_p[n] = \frac{1}{N} \sum\_{k=0}^{N-1} X_p[k] e^{j\frac{2 \pi}{N} k n} \hspace{3mm} {\color{red}\bf \forall n}
\end{eqnarray*}
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
\begin{eqnarray*}
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
\end{eqnarray*}
The 4-point DFT writes as:
$$
X_p[k] = \sum_{n=0}^{3} x_p[n] e^{-j\frac{2 \pi}{4} k n}= e^{-j\frac{2 \pi}{4} k} = (-j)^k
$$
Some values are:
\begin{eqnarray*}
& X_p[-4]= 1 \text{ ; } X_p[-3]= -j \text{ ; } X_p[-2] = -1 \text{ ; } X_p[-1]= j & \\
& X_p[0]= 1 \text{ ; } X_p[1]= -j \text{ ; } X_p[2] = -1 \text{ ; } X_p[3]= j & \\
& X_p[4]= 1 \text{ ; } X_p[5]= -j \text{ ; } X_p[6] = -1 \text{ ; } X_p[7]= j &
\end{eqnarray*}
</div>
</div>

<br></br>
## Basic DFT summation or orthogonality property
In order to understand how the DFT equations can extract frequencies of a signal, we will see that the complex exponent $W\_N=e^{j\frac{2\pi}{N}}$, the so called twiddle factor, plays a very important role. This can be shown by evaluating the following summation:
$$
S[k]= \sum\_{n=0}^{N-1} \\{ W\_N^k \\} ^n  = \sum\_{n=0}^{N-1} \\{ e^{j\frac{2 \pi}{N} k} \\} ^n
$$
which adds ,for each index $k$, $N$ terms of a discrete time phasor with relative frequency $\theta = k \cdot \frac{2\pi}{N}$.
For this evaluation we shown that $S[k]$ is periodic with period $N$. With $\lambda$ a positive or negative integer this can be proven as follows:
$$
\begin{eqnarray*}
S[k + \lambda \cdot N ] &=& \sum\_{n=0}^{N-1} \left \\{ e^{j\frac{2 \pi}{N} (k + \lambda \cdot N)} \right \\} ^n
= \sum\_{n=0}^{N-1} \left \\{ e^{j\frac{2 \pi}{N} k} \cdot  e^{j\frac{2 \pi}{N} \lambda \cdot N} \right \\} ^n \newline
&=& \left \\{ e^{j\frac{2 \pi}{N} k} \cdot  e^{j2 \pi \lambda } \right \\} ^n =
\left \\{ e^{j\frac{2 \pi}{N} k} \cdot  1  \right \\} ^n = S[k]
\end{eqnarray*}
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
\begin{eqnarray*}
S[k]|\_{k\neq0}&=& \sum\_{n=0}^{N-1} \\{ e^{j\frac{2 \pi}{N} k} \\} ^n =
\frac{1-e^{j\frac{2 \pi}{N} k N}}{1-e^{j\frac{2 \pi}{N} k}}
= \frac{1-e^{j2 \pi k}}{1-e^{j\frac{2 \pi}{N} k}} =
\frac{1-1}{1-e^{j\frac{2 \pi}{N} k}}=0
\end{eqnarray*}
$$
This leads to the following basic DFT summation or orthogonality property:

$$
\boxed{
\begin{eqnarray*}
S[k]= \sum\_{n=0}^{{\color{red}N}-1} \left \\{ W\_{{\color{red}N}}^k \right \\} ^n =
\sum\_{n=0}^{{\color{red}N}-1} \left \\{ \text{e}^{j \frac{2\pi}{{\color{red}N}} k } \right \\} ^n = {\color{red}N}  \delta [{\color{blue} k} \text{ mod}({\color{red}N})]
\end{eqnarray*}
}
$$

Thus, the summation $S[k]$ is always equal to zero, except for the cases that the index $k$ is an $N$-fold, thus for $k$ equal to $0$ or $\pm N$ or $\pm 2N$ or etc.  which can be described by the given delta function in which the index contains the modulo(N) operation.


<div class="example">
<h4> Example </h4>
<hr>
Calculate the values of $S[k]$ for $N=4$ and $k=-1,0,1,2,3,4$ explicitly.
<button class="collapsible">Show solution</button>
<div class="content">
\begin{eqnarray*}
S[-1] &=& \sum_{n=0}^{3} \left (e^{j\frac{\pi}{2} \cdot -1}\right )^n = \sum_{n=0}^{3} \left (e^{-j\frac{\pi}{2} \cdot 1}\right )^n = 1 - j - 1 +j =0 \\
S[0] &=& \sum_{n=0}^{3} \left (e^{j\frac{\pi}{2} \cdot 0}\right )^n =
\sum_{n=0}^{3} \left (1 \right )^n = 1 + 1 + 1 + 1 = 4 \\
S[1] &=& \sum_{n=0}^{3} \left (e^{j\frac{\pi}{2} \cdot 1}\right )^n = 1 + j - 1 -j =0 \\
S[2] &=& \sum_{n=0}^{3} \left (e^{j\frac{\pi}{2} \cdot 2}\right )^n = 1 - 1 +1 -1 =0 \\
S[3] &=& \sum_{n=0}^{3} \left (e^{j\frac{\pi}{2} \cdot 3}\right )^n = 1 - j -1 + j =0 \\
S[4] &=& \sum_{n=0}^{3} \left (e^{j\frac{\pi}{2} \cdot 4}\right )^n =
\sum_{n=0}^{3} \left (e^{j2 \pi }\right )^n =
\sum_{n=0}^{3} \left (1 \right )^n = 1 + 1 + 1 + 1 = 4
\end{eqnarray*}
</div>
</div>

<div class="example">
<h4> Example </h4>
<hr>
Give a mathematical expression in terms of a delta pulse of $A[k]=\sum_{n=0}^{7} e^{j\frac{2\pi}{4} \cdot n \cdot k}$ and calculate $A[k]$ for for $k=-8,-7, \cdots, 14, 15$.
<button class="collapsible">Show solution</button>
<div class="content">
\begin{eqnarray*}
A[k]&=\sum_{n=0}^{7} e^{j\frac{2\pi}{4} \cdot n \cdot k}  \\
&= \sum_{n=0}^{7} \left\{ e^{j\frac{2\pi}{8} 2k} \right\}^n \\
&= 8 \cdot \delta[2k \text{mod}(8)]
\end{eqnarray*}
Explicit evaluation of $A[k]$ are as follows:
$$
\begin{eqnarray*}
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
\end{eqnarray*}
$$
From these values it follows that we can write the result as follows:
$A[k] = 8 \delta[k \text{mod}(4)]$.
</div>
</div>


<br></br>
## How the DFT extracts a frequency
In this subsection we will show by an example, that the basic DFT summation property is used in the DFT algorithm to find the relative frequencies which are 'hidden' in the signal samples
$x[n]$ for $n=0,1, \cdots, N-1$. In this example we use a DFT of length $N=4$, so for each resulting DFT index $k$ the result of the DFT operation describes how much of the relative frequency $k \times \frac{2 \pi}{4}$ is contained in the signal samples $x[n]$ in the range $n=0$ until $n=3$.
In order to show how this works we use again the same sinusoidal example as before, namely $x[n]= \cos (\frac{\pi}{2} n)$:
$$
X[k] = \sum\_{n=0}^{3} x[n] e^{-j\frac{2\pi}{4} k n}
= \sum\_{n=0}^{3} \cos (\frac{\pi}{2} n) e^{-j\frac{\pi}{2} k n}
$$
By using Euler, we can split the cosine into two discrete-time phasors, split the summation into two separate summations and combine in each of these summations the complex exponents:

\begin{eqnarray*}
X[k]&=& \sum\_{n=0}^{3} \frac{1}{2} \cdot \left ( e^{j\frac{\pi}{2} n} +  e^{-j\frac{\pi}{2} n} \right ) e^{-j\frac{\pi}{2} k n} \newline
&=& \frac{1}{2} \sum\_{n=0}^{3} \left ( e^{j\frac{\pi}{2} n}  \right ) e^{-j\frac{\pi}{2} k n} +
\frac{1}{2} \sum\_{n=0}^{3} \left ( e^{-j\frac{\pi}{2} n}  \right ) e^{-j\frac{\pi}{2} k n} \newline
&=& \frac{1}{2} \sum\_{n=0}^{3} e^{-j\frac{\pi}{2} (k-1) n} + \frac{1}{2} \sum\_{n=0}^{3} e^{-j\frac{\pi}{2} (k+1) n}
\end{eqnarray*}

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
Calculate a trigonometric expression for the 16 point IDFT $x_p[n]$ of $X_p[k]$ which is defined as:
$$
X_p[k]= 2 \delta[(k-1) \text{mod}(16)] + \delta[(k-3) \text{mod}(16)]
+ \delta[(k-13) \text{mod}(16)] + 2 \delta[(k-15) \text{mod}(16)]
$$
<button class="collapsible">Show solution</button>
<div class="content">
$$
\begin{eqnarray*}
x_p[n] &=& \frac{1}{16} \sum_{k=0}^{15} \left \{ 2 \delta[(k-1) \text{mod}(16)] + \delta[(k-3) \text{mod}(16)] + \right .\\
& & \left . + \delta[(k-13) \text{mod}(16)] + 2 \delta[(k-15) \text{mod}(16)] \right \} e^{j\frac{2\pi}{16} k n}\\
&=& \frac{1}{16} \left \{
2 e^{j\frac{2\pi}{16} n} + e^{j\frac{2\pi}{16} 3n} + e^{j\frac{2\pi}{16} 13n} +2 e^{j\frac{2\pi}{16}15 n} \right \} \\
&=& \frac{1}{16} \left \{
2 e^{j\frac{\pi}{8} n} + e^{j\frac{\pi}{8} 3n} + e^{-j\frac{\pi}{8} 3n} +2 e^{-j\frac{\pi}{8} n} \right \} \\
&=& \frac{1}{16} \left \{ 4 \cos (\frac{\pi}{8} n) + 2 \cos (\frac{\pi}{8} 3n)
\right \} = \frac{1}{4} \cos (\frac{\pi}{8} n) + \frac{1}{8} \cos (\frac{3\pi}{8} n)
\end{eqnarray*}
$$
</div>
</div>
