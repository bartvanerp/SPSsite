+++
title = "Linear time invariant (LTI)"

# date = {{ .Date }}
lastmod = 2019-10-10

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Linear time invariant (LTI)"
  weight = 3
  parent = "Filter structures I: Finite impulse response (FIR) filter"
+++


## Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/JnP9ybC6wJc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>
<br>
The FIR filter, as described in the previous sections, belongs to a general class of systems that is used very often in practice: The so called <b>Linear Time Invariant (LTI)</b> systems.
In the first subsections the definitions Linearity and Time Invariance are given. In the last subsection it will be shown that the convolution sum operator is a result of LTI.

In this section the new symbol $x[n] \mapsto y[n]$ will be used with the following interpretation: The system maps the sequence of input signal samples $x[n]$ to the sequence of output signal samples $y[n]$.

## Linear systems
When a system results into the following mappings: $x_1[n] \mapsto y_1[n]$ and $x_2[n] \mapsto y_2[n]$, then such a system is Linear if for any linear combination of input sequences $x_1[n]$ and $x_2[n]$ the system maps this linear combination to the same linear combination of output sequences $y_1[n]$ and $y_2[n]$. With scalars $\alpha$ and $\beta$, this definition can mathematically be described as follows:
\begin{equation*}
\boxed{
x[n]= \alpha x_1[n] + \beta x_2[n] \mapsto y[n]= \alpha y_1[n] + \beta y_2[n]}
\end{equation*}
A visualisation of this definition is depicted in Fig. 1.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/FIR/linear.svg"
      alt="Example of a linear system."
    />
    <figcaption class="numbered">
      Example of a linear system.
    </figcaption>
  </figure>
</div>

<div class="example">
<h4> Example </h4>
<hr>
Show that the system $y[n]= ( x[n])^2$ is non-linear.
<button class="collapsible">Show solution</button>
<div class="content">
Referring to the left-hand side of Fig. 1 we obtain:
$$
y[n] = \left ( x[n] \right )^2 =
\left ( \alpha x_1[n] + \beta x_2[n] \right )^2 = \alpha ^2 x_1^2[n] + 2 \alpha \beta x_1[n] x_2[n] + \beta ^2 x_2^2[n]
$$
Referring to the right-hand side of Fig. 1 we obtain:
$$
w[n] = \alpha y_1[n] + \beta y_2[n] = \alpha x_1^2[n] + \beta x_2^2[n]
$$
Since $w[n] \neq y[n]$ it follows that the system $y[n]= ( x[n])^2$ is non-linear.
</div>
</div>


## Time Invariant systems
When a system results into the following mapping: $x[n] \mapsto y[n]$ then a system is Time Invariant
if a delayed sequence of input samples $x[n-n_0]$ is mapped by the system to a sequence of output samples $y[n-n_0]$, which is delayed by the same amount of samples. With integer delay $n_0$, this definition can mathematically be described as follows:
\begin{equation*}
\boxed{
x[n] \mapsto y[n] \hspace{3mm} \Rightarrow \hspace{3mm} x[n-n_0] \mapsto y[n-n_0]}
\end{equation*}
A visualisation of this definition is depicted in Fig. 2.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/FIR/timeinv.svg"
      alt="Example of a time-invariant system."
    />
    <figcaption class="numbered">
      Example of a time-invariant system.
    </figcaption>
  </figure>
</div>

<div class="example">
<h4> Example </h4>
<hr>
Show that the system $y[n]= ( x[n])^2$ is Time Invariant.
<button class="collapsible">Show solution</button>
<div class="content">
From the upper part of Fig. 2 it follows that
$w[n] = x^2[n-n_0]$. From the lower part of the same Figure it follows:
$$
y[n] = x^2[n] \hspace{3mm} \Rightarrow \hspace{3mm} y[n-n_0] = x^2[n-n_0]
$$
The system $y[n]= ( x[n])^2$ is Time Invariant since $w[n]=y[n-n_0]$.
</div>
</div>



### Convolution sum as result of LTI
When a system is LTI then the sequence of output samples $y[n]$ can be expressed as a convolution sum of the sequence of input samples $x[n]$ with the impulse response $h[n]$ of the LTI system, thus $y[n]=x[n] \star h[n]$. The proof of this property is as follows:
$$
\begin{eqnarray*}
\delta[n] \mapsto h[n] & \Rightarrow & \delta[n-k] \overset{\text{TI}}{\mapsto} h[n-k] \text{ for any } k\newline
& \Rightarrow & x[k] \delta[n-k] \overset{\text{L}}{\mapsto} x[k] h[n-k] \text{ for any } k \newline
& \Rightarrow & \sum\_k x[k] \delta[n-k] \overset{\text{L}}{\mapsto} y[n] = \sum\_k x[k] h[n-k] = x[n] \star h[n]
\end{eqnarray*}
$$
Note that in general for an LTI system the summation index $k$ of the convolution sum runs from $k=-\infty$ to $k=+\infty$, while for an FIR filter this range is automatically limited because of the finite length of the impulse response.

<br></br>

## Cascading LTI systems
In the first subsection it is shown that the convolution sum operator has the commutative property. As a result it is sown in the next subsection that the cascading of two LTI systems can be combined to one LTI system, while above that the order of the cascaded LTI systems can be interchanged.

### Commutative property convolution sum operator
The convolution sum operator is a <b>commutative</b> operation. This implies that the result $y[n]$ of the convolution sum operator can be obtained by either convolving $h[n]$ by $x[n]$ or the other way around:
$$
\boxed{
y[n]=h[n] \star x[n] = x[n] \star h[n]}
$$
<i> Proof:</i>
$$
\begin{eqnarray*}
y[n] &=& h[n] \star x[n] = \sum\_{k = - \infty}^{\infty} h[k] x[n-k] \newline
&\overset{p=n-k}{=}& \sum\_{p = +\infty}^{-\infty} h[n-p] x[p]= \sum\_{p = - \infty}^{\infty} x[p] h[n-p]= x[n] \star h[n]
\end{eqnarray*}
$$

Note that for an FIR filter the range of the convolution sum is automatically limited by the finite length of the impulse response.
Thus in case of an FIR filter the commutative property of the convolution sum operator results on the one hand into:
\begin{equation*}
y[n] = h[n] \star x[n] = \sum\_{k=-\infty}^{\infty} h[k] x[n-k] \overset{\text{FIR}}{=}\sum\_{k=0}^{M-1} h[k] x[n-k]
\end{equation*}
where we used the fact that $h[n]=0$ for $n<0$ and $n>M$. On the other hand we have:
\begin{equation*}
y[n]= x[n] \star h[n] = \sum\_{k=-\infty}^{\infty} x[k] h[n-k] \overset{\text{FIR}}{=} \sum\_{k=n-(M-1)}^{n} x[k] h[n-k]
\end{equation*}
where we used the finite length of an FIR as follows:
$$
h[n-k] =0 \text{ for }
\begin{cases}
n-k < 0 \text{ } \Rightarrow \text{ } k>n \newline
n-k > M \text{ } \Rightarrow \text{ } k< n-M
\end{cases}
$$

<div class="example">
<h4> Example </h4>
<hr>
In the example of the section of the convolution sum it is shown that with $x[n] = \delta[n] + 2 \delta[n-1] + 3 \delta[n-2]$  and $h[n]= \delta[n] + \delta[n-1] + \delta[n-2]$ the convolution sum result $y[n]=h[n] \star x[n]$ was equal to $y[n] = \delta[n] + 3 \delta[n-1] + 6 \delta[n-2] + 5 \delta[n-3] + 3 \delta[n-4]$. Show that the result of $x[n] \star h[n]$ is the same.
<button class="collapsible">Show solution</button>
<div class="content">
The convolution sum operator for this FIR filter equals:
$
y[n] = x[n] \star h[n] = \sum_{k=n-2}^{n} h[n-k]x[k]
$
Writing this equation out step by step results into:
\begin{eqnarray*}
\vdots & \vdots & \vdots \newline
y[-1] &=& \sum_{k=-3}^{-1} h[-1-k]x[k] = h[2] x[-3] + h[1]x[-2] + h[0] x[-1] = 0 \newline
y[0] &=& \sum_{k=-2}^{0} h[0-k]x[k] = h[2] x[-2] + h[1]x[-1] + h[0] x[0] = 1 \newline
y[1] &=& \sum_{k=-1}^{1} h[1-k]x[k] = h[2] x[-1] + h[1]x[0] + h[0] x[1] = 3 \newline
y[2] &=& \sum_{k=0}^{2} h[2-k]x[k] = h[2] x[0] + h[1]x[1] + h[0] x[2] = 6 \newline
y[3] &=& \sum_{k=1}^{3} h[3-k]x[k] = h[2] x[1] + h[1]x[2] + h[0] x[3] = 5 \newline
y[4] &=& \sum_{k=2}^{4} h[4-k]x[k] = h[2] x[2] + h[1]x[3] + h[0] x[4] = 3 \newline
y[5] &=& \sum_{k=3}^{5} h[5-k]x[k] = h[2] x[3] + h[1]x[4] + h[0] x[5] = 0 \newline
\vdots & \vdots & \vdots
\end{eqnarray*}
This result is indeed equivalent to
$$
y[n] = h[n] \star x[n] = \delta[n] + 3 \delta[n-1] + 6 \delta[n-2] + 5 \delta[n-3] + 3 \delta[n-4].
$$
</div>
</div>

### Cascade equivalences
The upper left hand figure of Fig. 3 shows the cascading of two LTI systems, one with impulse response $h_1[n]$ and the other one with impulse response $h_2[n]$. When applying a delta pulse ${\color{red}{\delta[n]}}$ to the first LTI system, the output equals the impulse response ${\color{red}{h_1[n]}}$. When applying this sequence to the second LTI system, the result is the convolution sum result ${\color{red}{h_1[n] \star h_2[n]}}$.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/FIR/cascadeequiv.svg"
      alt="Equivalence of cascading LTI filters."
    />
    <figcaption class="numbered">
      Equivalence of cascading LTI filters.
    </figcaption>
  </figure>
</div>

The lower left hand figure shows one LTI system with impulse response $h[n] = h_1[n] \star h_2[n]$. When applying a delta pulse ${\color{red}{\delta[n]}}$ to this system the result is the same as above.

<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The cascading of two LTI systems, one with impulse response $h_1[n]$ and the other one with impulse response $h_2[n]$, can be combined to one LTI system with impulse response $h[n]=h_1[n] \star h_2[n]$.</i></div>
<br>

Finally it follows from the commutative property of the convolution sum operator that:
$$
h[n] =h_1[n] \star h_2[n] = h_2[n] \star h_1[n]
$$
which is shown in the lower right part of Fig. 3. This combined impulse response can be split again into the cascading of two LTI systems, as shown in the upper right figure. In this last step however the LTI systems with impulse response $h_1[n]$ and $h_2[n]$ have interchanged from order.

<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The order of two LTI systems, one with impulse response $h_1[n]$ and the other one with $h_2[n]$, can be interchanged.</i></div>
<br>


<div class="example">
<h4> Example </h4>
<hr>
The cascading of two LTI systems is depicted in the figure below. Give an expression for the impulse responses $h_1[n]$ and $h_2[n]$ of both systems and evaluate the impulse response $h[n]$ of the combined LTI system. Give also a realization scheme of this combined system.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/FIR/examplecascade.svg"
      alt="Example of cascading two LTI systems."
    />
    <figcaption>
      Example of cascading two LTI systems.
    </figcaption>
  </figure>
</div>
<br>
<button class="collapsible">Show solution</button>
<div class="content">
From the figure it follows that the impulse response are as follows:
$$
h_1[n] =
\begin{cases}
1 & 0 \leq n \leq 2 \newline
0 & \text{elsewhere}   
\end{cases}
$$
and
$$
h_2[n] =
\begin{cases}
1 & 0 \leq n \leq 2 \newline
0 & \text{elsewhere}
\end{cases}
$$
The combined impulse response can be found as follows:
\begin{eqnarray*}
h[n] &=& h_1[n] \star h_2[n] \\
&=& \left ( \delta[n] + \delta[n-1] + \delta[n-3] \right ) \star
\left ( \delta[n] + \delta[n-1] + \delta[n-3] \right ) \\
&=& \delta[n] + 2 \delta[n-1] + 3\delta[n-2]+ 2 \delta[n-3] + \delta[n-4]
\end{eqnarray*}
A realization scheme of this combined LTI system is depicted in the lower part of the figure above.
</div>
</div>
