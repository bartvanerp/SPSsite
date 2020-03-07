+++
title = "Signal manipulations"

# date = {{ .Date }}
lastmod = 2020-03-07

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Signal manipulations"
  weight = 6
  parent = "Discrete-time signals"


+++
Signal manipulations are generally decomposed of a few basic transformations. These transformations may be classified either as those that are transformations of the independent variable $n$ or those that are transformations of the amplitude of $x[n]$, i.e. the dependent variable.

The most common types of amplitude transformations are  addition,  multiplication and  scaling:
\begin{eqnarray*}
\color{blue}{\textit{Addition}} &:& y[n]=x_1[n]+x_2[n] \newline
\color{blue}{\textit{Multiplication}} &:& y[n]=x_1[n] \cdot x_2[n] \newline
\color{blue}{\textit{Scaling}} &:& y[n] = c \cdot x[n]
\end{eqnarray*}
Performing these operations is straightforward and involves only point-wise operations on the signal.

Sequences are often altered and manipulated by modifying the independent function variable $n$, where $f[n]$ is some function of the index $n$. If, for some value of $n$, $f[n]$ is not an integer, $y[n] = x[f[n]]$ is undefined.  The most common transformations include shifting (delaying or advancing),  reversal,  and time-scaling as summarized in the following equations:
\begin{eqnarray*}
\textit{Time shifting (delay or advance)} &:& f[n]=n-n_0 \newline
\textit{Time reversal} &:& f[n]=-n \newline
\textit{Time scaling = Down- or Up- sampling} &:& f[n]=M \cdot n \text{ or } f[n]=n/M
\end{eqnarray*}
Determining the effect of modifying the index $n$ may always be accomplished using a simple tabular approach of listing, for each value of the index $n$, the value of $f[n]$ and then setting $y[n] = x[f[n]]$. However, for many transformations this is not necessary, and the sequence may be determined or plotted directly. Examples of  delaying,  time-reversal and time scaling, such as  down sampling and  up-sampling are illustrated in Fig. 1.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/signals/exdelayrevupdown.svg"
      alt="Examples of transformation of the function variable."
    />
    <figcaption class="numbered">
      Examples of transformation of the function variable.
    </figcaption>
  </figure>
</div>
Note that shifting, reversal, and time scaling operations are order dependent. Therefore, one needs to be careful in evaluating compositions of these operations.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/signals/orderdelayrevupdown.svg"
      alt="Shifting and reversal are order dependent operations."
    />
    <figcaption class="numbered">
      Shifting and reversal are order dependent operations.
    </figcaption>
  </figure>
</div>
Fig. 2 shows an example in which a signal $x[n]$ is first delayed over $n_0$ samples, resulting in $x[n-n_0]$. Reversing this signal, that is replacing the running index $n$ by $-n$, results in the signal $x[-n-n_0]$. Switching the order of these two operations, that is first reverse and then delay results in another signal namely $x[-n+n_0]$.

Finally the delta pulse may be used to decompose an arbitrary signal $x[n]$ into a, possible infinite, sum of weighted and shifted delta pulses:
$$
x[n] = \sum_{k=- \infty}^{\infty} x[k] \delta[n-k]
$$
Each term in the sum, $x[k] \delta[n-k]$, is a signal that has amplitude $x[k]$ at index $n=k$ and a value of zero for all other values of the index $n$.

<div class="example">
<h4> Example </h4>
<hr>
Express the signal
$$
x[n] =
\begin{cases}
3 & n=0 \newline
2 & n=1 \newline
1 & n=2 \newline
0 & \text{elsewhere}
\end{cases}
$$
as a sum of scaled and shifted unit step functions.
<button class="collapsible">Show solution</button>
<div class="content">
First express $x[n]$ as a sum of weighted and shifted delta pulses:
$$
x[n]=3 \delta[n] + 2 \delta[n-1] + \delta[n-2].
$$
With $\delta[n] = u[n] - u[n-1]$ this becomes:
\begin{eqnarray*}
x[n] &=& 3u[n] - 3u[n-1] + 2u[n-1] - 2u[n-2] + u[n-2] - u[n-3] \newline
&=& 3u[n]-u[n-1] -u[n-2] - u[n-3]
\end{eqnarray*}
</div>
</div>

<div class="example">
<h4> Example </h4>
<hr>
The power in a real valued signal $x[n]$ is defined as the sum of squares of the sample values: $P= \sum_{n=-\infty}^{\infty} x^2[n]$.
Suppose that a signal $x[n]$ has an even part $x_e[n]= (\frac{1}{3})^{|n|}$. If the power
in $x[n]$ is $P=2$, find the power in the odd part $x_o[n]$ of $x[n]$.
<button class="collapsible">Show solution</button>
<div class="content">
\begin{eqnarray*}
P &=& \sum_{n=-\infty}^{\infty} x^2[n] = \sum_{n=-\infty}^{\infty} (x_e[n] + x_o[n])^2[n] \newline
&=& \sum_{n=-\infty}^{\infty} x_e^2[n] + \sum_{n=-\infty}^{\infty} x_o^2[n] + 2
\sum_{n=-\infty}^{\infty} x_e[n] \cdot x_o[n].
\end{eqnarray*}
The product $x_e[n] \cdot x_o[n]$ is odd and the sum of this odd signal is zero, thus we have:
$$
P =  \sum_{n=-\infty}^{\infty} x_e^2[n] + \sum_{n=-\infty}^{\infty} x_o^2[n] = P_e + P_o
$$
with
$$
P_e = \sum_{n=-\infty}^{\infty} (\frac{1}{3})^{2|n|} = -1 + 2 \sum_{n=0}^{\infty} (\frac{1}{3})^{2n} = \frac{5}{4}.
$$
From this we obtain the result:
$$
P_o = P - P_e = 2 - \frac{5}{4} = \frac{3}{4}.
$$
</div>
</div>
