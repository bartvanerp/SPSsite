+++
title = "The Z-transform"

# date = {{ .Date }}
lastmod = 2020-02-16

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Z-transform"
  weight = 1
  parent = "Transforms IV: Z-transform"


+++

## Conceptual video
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/k3HJyYWm6yI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>

The <a href="../../../disciplines/discrete/discretesignalprocessing_transforms_ftd/">Fourier Transform for Discrete-time signals and systems (FTD)</a>, is a complex function of the angular frequency $\theta$. It provides a frequency domain representation of discrete-time signals and LTI-systems. Moreover, because of the convergence conditions, in many cases the FTD of a sequence may not exist, and as a result, it is not possible to make use of such frequency domain characterization in these cases.

A generalization of the <a href="../../../disciplines/discrete/discretesignalprocessing_transforms_ftd/">FTD</a> leads to the Z-transform, abbreviated as ZT, which is a function of the complex variable $z$. It can exist for many sequences for which the <a href="../../../disciplines/discrete/discretesignalprocessing_transforms_ftd/">FTD</a> does not exist. Also, the use of ZT techniques permits simple algebraic manipulations. Consequently, the ZT has become an important tool in the analysis and design of digital filters and it can be viewed as the discrete-time counterpart of the Laplace transform for continuous-time signals and systems.

Finally, it is important to note that the 'time'-domain representation is the domain where the signals are generated and processed, and where the implementation of the filters takes place. On the other hand, the frequency domain has physical significance when analyzing frequencies, while the $z$-domain exist primarily for its convenience in mathematical analysis and synthesis.

## Definition of the $Z$-Transform (ZT)
The <a href="../../../disciplines/discrete/discretesignalprocessing_transforms_ftd/">FTD</a> of a sequence $x[n]$ is defined as follows:
\begin{equation}\label{eq:FTD}
X(e^{j\theta}) = \sum_{n=-\infty}^{\infty} x[n] e^{-jn \theta}
\end{equation}
However, in order for this series to converge, it is necessary that the sequence $x[n]$  be absolutely sumable. Unfortunately, many of the signals that we would like to consider are not absolutely sumable and, therefore, do not have a <a href="../../../disciplines/discrete/discretesignalprocessing_transforms_ftd/">FTD</a>.  An example is the sequence $x[n]=2^n[n]$ which is not absolute summable and thus the <a href="../../../disciplines/discrete/discretesignalprocessing_transforms_ftd/">FTD</a> does not exist.

The $Z$-transform is a generalization of <a href="../../../disciplines/discrete/discretesignalprocessing_transforms_ftd/">FTD</a> that allows one to deal with such not absolutely sumable sequences and is defined as follows:

\begin{equation}
\boxed{X(z) = \sum_{n=-\infty}^{\infty} x[n] z^{-n}} \label{eq:ZT}
\end{equation}

in which $z$ is a complex variable.  When comparing this equation with the <a href="../../../disciplines/discrete/discretesignalprocessing_transforms_ftd/">FTD</a> it follows that we can obtain the <a href="../../../disciplines/discrete/discretesignalprocessing_transforms_ftd/">FTD</a> from the $Z$-transform by replacing the complex variable $z$ by $e^{j\theta}$.  In other words:
The <a href="../../../disciplines/discrete/discretesignalprocessing_transforms_ftd/">FTD</a> can be viewed as the evaluation of the ZT on the unit circle $z=e^{j\theta}$:

$$
\boxed{
X(z)\bigg\vert_{z=e^{j\theta}} \equiv X(e^{j\theta})}
$$

and as such the ZT is a generalization of the <a href="../../../disciplines/discrete/discretesignalprocessing_transforms_ftd/">FTD</a> as depicted in Fig. 1.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/Z/Zplane.svg"
      alt="FTD is ZT evaluated on the unit circle."
    />
    <figcaption class="numbered">
      The FTD is the ZT evaluated on the unit circle.
    </figcaption>
  </figure>
</div>

From the definition of the ZT it follows that the ZT of a delta function $x[n]=\delta[n]$  equals 1  and the ZT of a shifted delta function $x[n]=\delta[n-1]$ is equal to $z^{-1}$:

$$
\begin{eqnarray}
x[n]=\delta[n] &\quad {\overset{\color{red}{\text{ZT}}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ}} \quad& X(z)=\sum\_{n=-\infty}^{\infty} \delta[n] z^{-n}= 1\cdot z^0 = 1 \newline
x[n]=\delta[n-{\color{green}{1}}] &{\overset{\color{red}{\text{ZT}}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ}} & X(z)=\sum\_{n=-\infty}^{\infty} \delta[n-{\color{green}{1}}] z^{-n}= {\color{green}{z^{-1}}} \quad \leftrightarrow \textbf{Delay}
\end{eqnarray}
$$

In general when $x[n]=\delta[n-p]$ its ZT is $z^{-p}$:

$$
\begin{eqnarray}
x[n]=\delta[n-p] & \quad {\overset{\color{red}{\text{ZT}}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ}} \quad& X(z)=\sum\_{n=-\infty}^{\infty} \delta[n-p] z^{-n}=z^{-p}
\end{eqnarray}
$$

As a result a causal sequence will result is a $Z$-transform represented by a polynomial of $z$ from which the powers are $\leq 0$. On the other hand, the $Z$-transform of a non-causal sequence results in a polynomial of $z$ from which the powers are $> 0$.

An example of the ZT $X(z)$ of a causal sequence $x[n]$ consisting of a sum of 11 delta pulses $\delta[n]$ until $\delta[n-10]$ is as follows:

$$
\begin{eqnarray}
x[n]=\sum_{p=0}^{10} \delta[n-p]
&\quad {\overset{\color{red}{\text{ZT}}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ}} \quad&
X(z) = \sum_{n=0}^{10} z^{-n}
\end{eqnarray}
$$

The summation over a finite number of elements can be written as a fraction of two polynomials:

$$
\begin{eqnarray}
x[n]=\sum_{p=0}^{10} \delta[n-p]
&\quad {\overset{\color{red}{\text{ZT}}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ}} \quad&
X(z) =\frac{1 - z^{-11}}{1-z^{-1}}
\end{eqnarray}
$$

By multiplying both numerator and denominator with $z^{11}$
the 11-th order polynomial of the numerator
can be written as a product of 11 first order polynomials:

$$
\begin{eqnarray}
X(z) &=& \frac{z^{11} -1}{z^{10} \cdot (z-1)}
= \frac{\Pi_{{\color{red}{k=0}}}^{10} (z - e^{-j\frac{2\pi}{11} k})}{z^{10}\cdot {\color{red}{(z-1)}}}
\end{eqnarray}
$$

The first term (for $k=0$) of the numerator writes as $z-1$. Because of the fact that the denominator also contains a term $z-1$,  the ZT writes as a numerator, which is the product of 10 first order polynomials, and a denominator which is equal to $z^{10}$:

$$
\begin{eqnarray}
X(z) &=&  \frac{\Pi_{{\color{red}{k=1}}}^{10} (z - e^{-j\frac{2\pi}{11} k})}{z^{10}}
\end{eqnarray}
$$

Because of the fact that the denominator also contains a term $z-1$,  the ZT writes as a numerator, which is the product of 10 first order polynomials, and a denominator which is equal to $z^{10}$.

A 3-dimensional plot of this function  in the complex $z$-domain is given in Fig. 2.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/Z/ZTandFTD.svg"
      alt="Plots of 20 log$|X(z)|$, the top-view and FTD which is the result when evaluated on unit circle."
    />
    <figcaption class="numbered">
      Plots of 20 log$|X(z)|$, the top-view and FTD which is the result when evaluated on unit circle.
    </figcaption>
  </figure>
</div>

The figure represents the 20 log of $X(z)$. From the denominator $z^{10}$ it is clear that for $z=0$ the function becomes infinite. This 10-fold root of the denominator is referred to as the 10-fold pole of $X(z)$.
On the other hand the roots of the numerator, referred to as the zeros, are given by 10 equally distributed values of $z$ on the unit circle $z=e^{-j\frac{2\pi}{11} k}$ with $k=1$ until $k=10$.

These 10 poles at $z=0$ and 10 zeros on the unit circle can be represented by a top-view figure of the 3-dimensional plot. Finally, as mentioned before, by evaluating the ZT on the unit circle, we obtain the FTD result as depicted in the lower right plot. More specifically, evaluating $X(z)$ at points around the unit circle, beginning at $z=1$ (which corresponds to $\theta =0$), through $z=j$ (which corresponds to $\theta =\pi/2$), to $z=1$ (which corresponds to $\theta =\pi$) we obtain values of the FTD $X(e^{j\theta})$ for $\theta$ in the range from $\theta=0$ until $\theta=\pi$. By going the other way around on the unit circle we obtain the FTD $X(e^{j\theta})$ for $\theta$ in the range from $\theta=0$ until $\theta=-\pi$.

## Region Of Convergence (ROC)
The values of $z$, for which the sum converges, define a region in the $z$-plane referred to as the Region Of Convergence, abbreviated as ROC. In the sequel we will show that this ROC of a ZT is an important concept for a variety of reasons.

With $z=r e^{j\theta}$  the ZT can be viewed as the FTD of an exponentially weighted sequence $x[n] r^{-n}$:

$$
X(z)= \sum_{n=-\infty}^{\infty} x[n] z^{-n}
\overset{z=r e^{j\theta}}{=\\! =\\! =\\! =}
\sum_{n=-\infty}^{\infty} \left (x[n] r^{-n}  \right ) e^{-j\theta n}
$$

From this expression it follows that the ROC is determined by the range of values of $r$ for which the given summation is limited

$$
\color{red}{\text{ROC}}\text{: Range $r$ for which }
\sum\_{n=-\infty}^{\infty} \lvert x[n] r^{-n} \rvert < \infty
$$

In the following example we calculate the ROC of the right sided sequence $x_1[n]= a^n u[n]$.

$$
\begin{eqnarray}
x_1[n]= a^n u[n] &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ&
X_1(z) = \sum_{p=0}^{\infty} (a z^{-1})^p
\end{eqnarray}
$$

Applying the ZT results in the given expression of $X_1(z)$ as an infinite summation.  In case the absolute value of the argument of this summation, $a z^{-1}$, is smaller than 1, the infinite summation converges to $\frac{1}{1-a z^{-1}}$:

$$
\begin{eqnarray}
x_1[n]= a^n u[n] &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ&
X_1(z) = \sum_{p=0}^{\infty} (a z^{-1})^p
\overset{|a z^{-1}| < 1}{=\\! =\\! =\\! =\\! =} \frac{1}{1 - a z^{-1}}
\end{eqnarray}
$$

From this we can compute the ROC for this example as follows:

$$
|a z^{-1}| < 1 \quad
\leftrightarrow \text{ } |z| > |a|
$$

Thus the ROC of $X_1(z)$ is described by all values of the complex variable $z$  outside a circle with radius $a$.
Furthermore, as mentioned before, the FTD can be viewed as the evaluation of the ZT on the unit circle $z=e^{j\theta}$. In other words the FTD of the sequence $x_1[n]$ only exists in case the unit circle is inside the ROC,  which implies that the absolute value of the parameter $a$ has to be smaller than 1. For example the FTD of the converging sequence $x_1[n]=(\frac{1}{2})^n u[n]$ exist, while the FTD of the diverging sequence $x_1[n] = (2)^n u[n]$ does not exist.

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>
FTD $\equiv$ ZT for $|z|=1$ only when the unit circle is in the ROC
</i></div>


## Uniqueness of ZT
In this subsection we will show that without knowledge of the ROC there is no unique relationship between a sequence $x[n]$ and its ZT $X(z)$.  As a first example we compute the ZT of the following left sided sequence $x_2[n]$:

$$
\begin{eqnarray}
x_2[n]=-(a)^n {\color{red}u[-n-1]} &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X_2(z)
\end{eqnarray}
$$

First substitute the variable  $-n$ with $p$, and taking the summation from $p=0$ instead of $p=1$:

$$
\begin{eqnarray}
X_2(z) &=& -\sum_{{\color{red}{n=-\infty}}}^{{\color{red}{-1}}} (a)^n z^{-n} \overset{p=-n}{=\\! = \\! =} -\sum_{p=1}^{\infty} (a^{-1} z)^p
=- \left ( \sum_{p={\color{green}{0}}}^{\infty} (a^{-1} z)^p {\color{green}{-1}} \right )
\end{eqnarray}
$$

The infinite summation can be replaced by $\frac{1}{1 -a^{-1} z }$ when the absolute value of the argument of the summation $a^{-1}z$ is smaller than one.

$$
\begin{eqnarray}
X_2(z) &
\overset{|a^{-1} z|<1}{=\\!=\\!=\\!=}&- \left ( \frac{1}{1 -a^{-1} z } -1 \right )=\frac{1}{1 - a z^{-1}}
\end{eqnarray}
$$

This last expression can be rewritten from which the ROC is given by all values of the complex variable $z$ inside a circle with radius $a$.

From this example it follows that although the sequences $x_1[n]$ and $x_2[n]$ are different, their ZT's $X_1(z)$ and $X_2(z)$ are the same but with different ROC.  The ROC's of divergent and convergent infinite length right- and left-sided sequences are indicated in the figure 3.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/Z/ROCexamplesx1x2.svg"
      alt="ROC's of divergent and convergent infinite length right- and left-sided sequences."
    />
    <figcaption class="numbered">
      ROC's of divergent and convergent infinite length right- and left-sided sequences.
    </figcaption>
  </figure>
</div>

From these two examples it follows that:  

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>
The ZT $X(z)$ is only uniquely related to a sequence $x[n]$ if the ROC is known. Hence, the ZT must always be specified with its ROC.
</i></div>

The ROC of other sequences is as follows:

From the following finite sequence and its ZT

$$
x_3[n] = a \delta[n+1] + b \delta[n] + c \delta[n-1]
\text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } X_3(z)=a z + b + c z^{-1}
$$

it simply follows that  the ROC of a finite sequence includes the entire $z$-plane, except, possibly, $z=0$ and $z=\infty$, as depicted in Fig. 4.
The point $z=\infty$ will be included for a causal finite sequence, thus when $x[n]=0$ for $n<0$. The point $z=0$ will be included for a non-causal finite sequence, thus when $x[n]=0$ for $n>0$.

From the following infinite sequence, which consists of a sum of a causal and a non-causal infinite sequence,

$$
x_4[n]=a^n u[n] - b^n u[-n-1]
\quad \text{with } |a| < 1 < |b|
$$

the ZT $X_4(z)$ can be found as an addition of the ZT of the two separate ZT's of each sequence separately:

$$
\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } X_4(z)= \frac{1}{1- a z^{-1}} + \frac{1}{1- b z^{-1}}
=\frac{2 - (a+b) z^{-1}}{(1 - a z^{-1}) (1 - b z^{-1})}
$$

From this it follows that the ROC can be described by an annulus  as depicted in Fig. 4.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/Z/ROCexamplesx3x4.svg"
      alt="ROC's of finite and infinite sequences."
    />
    <figcaption class="numbered">
      ROC's of finite and infinite sequences.
    </figcaption>
  </figure>
</div>

As a result of this last example, it follows that for the following rational function $X(z)$

$$
X(z) = \frac{1}{1 - a z^{-1}} + \frac{1}{1 - b z^{-1}}
\quad \text{with } |a| < 1 < |b|
$$

with two poles one at $z=a$, with absolute value of $a$ smaller than 1, and the other at $z=b$ with absolute value of $b$ larger than 1, it can be shown that in this case there are 3 different ROC's which are related to 3 different sequences $x[n]$.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/Z/DifferentROC.svg"
      alt="Different ROC's."
    />
    <figcaption class="numbered">
      Different ROC's.
    </figcaption>
  </figure>
</div>

In case the ROC is described by the region outside a circle with radius $b$, the first sequence $x[n]$ is as denoted by the equation in the first row of the following table:

<table style="width:100%">
  <tr>
    <th> ROC </th>
    <th> $x[n]$ </th>
    <th> Causal </th>
    <th> Convergent </th>
    <th> FTD </th>
  </tr>
  <tr>
    <td> $|z| > |b|$ </td>
    <td> $(a^n + b^n) u[n]$ </td>
    <td> Yes </td>
    <td> No </td>
    <td> No </td>
  </tr>
  <tr>
    <td> $|a| < |z| < |b|$ </td>
    <td> $a^n u[n] - b^n u[-n-1]$ </td>
    <td> No </td>
    <td> Yes </td>
    <td> Yes </td>
  </tr>
  <tr>
    <td> $|z| < |a|$ </td>
    <td> $-(a^n + b^n)u[-n-1]$ </td>
    <td> No </td>
    <td> No </td>
    <td> No </td>
  </tr>
</table>


Thus for this ROC the sequence $x[n]$ is a causal and divergent sequence of samples from which the FTD does not exist.  On the other hand if the ROC is an annulus which is described by the inner circle with radius $a$ and outer circle with radius $b$, the resulting second sequence $x[n]$ is given in the second row of the table, which is a non-causal, converging sequence, from which the FTD exist.  Finally, when the ROC is described by the region inside a circle with radius $a$, the resulting third sequence is given in the third row of the table, which is a non-causal, diverging sequence from which the FTD does not exist.

In general it can be shown that a rational function $X(z)$ which has poles with $R$ distinct magnitudes, has $R+1$ distinct ROC's and thus such a rational function $X(z)$ can be related to $R+1$ distinct sequences $x[n]$.

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>
If rational $X(z)$ has poles with $R$ distinct magnitudes $\Rightarrow$ $R+1$ distinct sequences $x[n]$ having same rational $X(z)$.
</i></div>
