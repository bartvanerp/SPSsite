+++
title = "Convolution"

# date = {{ .Date }}
lastmod = 2020-04-04

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Convolution"
  weight = 4
  parent = "Discrete-time systems"
+++



## Convolution sum operation
One of the most important consequences of an LTI system is that the output $y[n]$ can be described by applying the so called convolution sum procedure between the input $x[n]$ and  the impulse response $h[n]$.

The derivation of this procedure uses the general signal description as  a sequence of a, possible infinite, sum of weighted and shifted delta pulses:
$$
x[n] = \sum_{k=-\infty}^{\infty} x[k] \delta[n-k].
$$
For any LTI system we can now perform the following steps:

When applying a delta pulse to the input of the system, the result is the impulse response $h[n]$.  Because of the Time Invariance property a shifted delta puls over $k$ samples will result in a shifted impulse response $h[n-k]$:
\begin{eqnarray*}
\delta[n] \mapsto h[n] & \Rightarrow & \delta[n-k] \overset{\text{TI}}{\mapsto} h[n-k] \text{ for any } k
\end{eqnarray*}
Multiplying the shifted delta pulse with a constant $x[k]$ will result in $x[k] h[n-k]$ because of Linearity:
\begin{eqnarray*}
&&
x[k] \delta[n-k] \overset{\mbox{L}}{\mapsto} x[k] h[n-k] \mbox{ for any } k
\end{eqnarray*}
When summing over all indices $k$ will result into the output $y[n]$:
\begin{eqnarray*}
&&
\sum_k x[k] \delta[n-k] \overset{\mbox{L}}{\mapsto} y[n] = \sum_k x[k] h[n-k]
\end{eqnarray*}
Summarizing the convolution sum procedure is as follows:

<u><b>Convolution sum procedure:</b></u>
<ol>
  <li> Plot both input $x$ and impulse response $h$ as function of index $k$ </li>
  <li> Mirror (reverse) $h[k]$ $\Rightarrow$ $h[-k]$ </li>
  <li> For each new index $n$:
    <ol>
      <li> Shift mirrored $h[-k]$ to index $n$ $\Rightarrow$ $h[n-k]$. </li>
      <li> Output $y[n]$ is equal to the result of the sum of element by element multiplications of $x[k]$ and $h[n-k]$. </li>
    </ol>
  </li>
</ol>
Usually, the convolution sum procedure is described  by an operator,  which is symbolically denoted by a star:
\begin{equation}
y[n] = \sum_{k=-\infty}^{\infty} x[k] h[n-k] = x[n] \star y[n]
\end{equation}
Finally note the following:
<ol>
  <li> In general the summation index $k$ of the convolution sum runs from $k=-\infty$ to $k=+\infty$, while for an FIR filter this range is automatically limited because of the finite length of the impulse response. </li>
  <li> When the length of input signal samples is limited to $N$ and the length of the sequence of impulse response values is $M$, then the convolution sum procedure $y[n]=x[n] \star h[n]$ results in a sequence of length $N+M-1$ output signal samples. </li>
</ol>


<div class="example">
<h4> Example </h4>
<hr>
  Show in a plot the convolution sum result of $x[n]=\delta[n]+2 \delta[n-1]+3 \delta[n-2]$ with an FIR filter with coefficients $b_0=b_1=b_2=1$.
<button class="collapsible">Show solution</button>
<div class="content">
  The impulse response of the FIR filter writes as: $h[n] = \delta[n] + \delta[n-1]+\delta[n-2]$.
  The two plots at the top of the following figure show the impulse response $h[k]$ and the input signal samples $x[k]$.
  <div style="max-width: 800px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/systems/exconvolution.svg"
        alt="Solution to example."
      />
    </figure>
  </div>
  The next step is to mirror the input signal samples into $x[-k]$. Now for each new sample $n$ we have to shift this mirrored sequence of input signal samples over  $n$ samples
  and calculate the sum of the element by element multiplication of the two sequences $h[k]$ and $x[n-k]$. The intermediate results of the sequence $x[n-k]$, for ${\color{blue}n=0}, {\color{red}n=1}$ and ${\color{green}n=2}$, are depicted also depicted in the figure.
  Proceeding with these steps the output signal samples can be described as:
  $$
  y[n] = \delta[n] + 3 \delta[n-1] + 6 \delta[n-2] + 5 \delta[n-3] + 3 \delta[n-4]
  $$
  which is depicted at the lower right corner of the figure.
</div>
</div>


<br></br>
## Convolution sum properties
In this subsection we introduce properties of the convolution sum
that can be used to simplify the evaluation of the convolution sum procedure.

### Commutative property
The first property is the commutative property  which implies that the convolution sum of $x[n]$ with $h[n]$ behaves exactly the same as the other way around:
$$
\boxed{
y[n]=h[n] \star x[n] = x[n] \star h[n]}
$$
as represented in Fig. 1.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/commutative.svg"
      alt="Commutative property."
    />
    <figcaption class="numbered">
      Commutative property.
    </figcaption>
  </figure>
</div>

<div class="example">
<h4> Proof of commutative property</h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
\begin{eqnarray*}
y[n] &=& h[n] \star x[n] = \sum_{k = - \infty}^{\infty} h[k] x[n-k] \\
&\overset{p=n-k}{=}& \sum_{p = +\infty}^{-\infty} h[n-p] x[p]= \sum_{p = - \infty}^{\infty} x[p] h[n-p]= x[n] \star h[n]
\end{eqnarray*}
Note that for an FIR filter the range of the convolution sum is automatically limited by the finite length of the impulse response.
Thus in case of an FIR filter the commutative property of the convolution sum operator results on the one hand into:
\begin{equation}
y[n] = h[n] \star x[n] = \sum_{k=-\infty}^{\infty} h[k] x[n-k] \overset{FIR}{=}\sum_{k=0}^{M-1} h[k] x[n-k]
\end{equation}
where we used the fact that $h[n]=0$ for $n<0$ and $n>M$. On the other hand we have:
\begin{equation}
y[n]= x[n] \star h[n] = \sum_{k=-\infty}^{\infty} x[k] h[n-k] \overset{FIR}{=} \sum_{k=n-(M-1)}^{n} x[k] h[n-k]
\end{equation}
where we used the finite length of an FIR as follows:
$$
h[n-k] =0 \mbox{ for }
\left \{
\begin{array}{l}
n-k < 0 \mbox{ } \Rightarrow \mbox{ } k>n \\
n-k > M \mbox{ } \Rightarrow \mbox{ } k< n-M
\end{array}
\right .
$$
</div>
</div>


### Associative property
A second property is the associative property,  which implies that if two systems with impulse responses $h_1[n]$ and $h_2[n]$ are connected in cascade, an equivalent system is one that has impulse response equal to the convolution sum of $h_1[n]$ and $h_2[n]$:
$$
\boxed{
\\{ x[n] \ast h_1[n] \\} \ast h_2[n] = x[n] \ast \\{ h_1[n] \ast h_2[n] \\}}
$$
as represented in Fig. 2.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/associative.svg"
      alt="Associative property."
    />
    <figcaption class="numbered">
      Associative property.
    </figcaption>
  </figure>
</div>

### Distributive property
The third property is the distributive property  which implies that if two systems with impulse response $h_1[n]$ and $h_2[n]$ are connected in parallel, an equivalent system is one that has an impulse response that is equal to the sum of $h_1[n]$ and $h_2[n]$:
$$
\boxed{
x[n] \ast h_1[n] + x[n] \ast h_2[n] = x[n] \ast \\{ h_1[n] + h_2[n] \\}}
$$
as represented in Fig. 3.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/distributive.svg"
      alt="Distributive property."
    />
    <figcaption class="numbered">
    Distributive property.
    </figcaption>
  </figure>
</div>
