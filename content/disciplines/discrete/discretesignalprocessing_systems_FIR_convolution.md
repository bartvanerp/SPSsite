+++
title = "Convolution sum"

# date = {{ .Date }}
lastmod = 2019-10-10

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Convolution sum"
  weight = 2
  parent = "Systems I: Finite impulse response (FIR) filter"
+++

## Screencast video
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/7Q8w8XkYmHk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>

## Convolution sum
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/FIR/FIR.svg"
      alt="Realization scheme of a finite impulse response filter."
    />
    <figcaption class="numbered">
      Realization scheme of a finite impulse response filter.
    </figcaption>
  </figure>
</div>


Because of the fact that the impulse response coefficients of an FIR filter are equal to the weights of the filter, it follows from Fig. 1 that the DE can be written as:
$$
y[n] = \sum_{k=0}^{M-1} h[k] x[n-k]
$$
This equation performs the so called <b>convolution sum</b> operation: It describes the filter operation of an FIR. From this equation it follows that the procedure to compute the output samples $y[n]$, for any index $n$, can be described as follows:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px">
<b>Convolution sum procedure:</b>

<ol>
<li>Plot the impulse response weights $h[k]$ as a function of index $k$. </li>
<li>Plot the input signal samples $x[k]$ also as a function of index $k$. </li>
<li>Mirror (reverse) the input signal samples. That is replace $x[k]$ into $x[-k]$. </li>
<li>For each new index $n$, shift the mirrored signal samples $x[-k]$ to index $n$, resulting in $x[n-k]$. </li>
<li>For each new index $n$, the output signal sample $y[n]$ is equal to the sum of the element by element multiplication of the sequence $h[k]$ and the sequence $x[n-k]$ in the range $k=0,1, \cdots , M-1$, since $h[k]=0$ outside this range of indices. </li>
</ol>
</div>

In literature the symbol $\star$ is used to describe the convolution sum, thus:
\begin{equation*}
y[n] =  \sum_{k=0}^{M-1} h[k] x[n-k] \equiv h[n] \star x[n]
\end{equation*}


<div class="example">
<h4> Example </h4>
<hr>
Show in a plot the convolution sum result of $x[n]=\delta[n]+2 \delta[n-1]+3 \delta[n-2]$ with an FIR filter with coefficients $b_0=b_1=b_2=1$.
<button class="collapsible">Show solution</button>
<div class="content">
The impulse response of the FIR filter writes as: $h[n] = \delta[n] + \delta[n-1]+\delta[n-2]$.
The upper hand two plots of the figure below show the impulse response $h[k]$ and the input signal samples $x[k]$. The next step is to mirror the input signal samples into $x[-k]$. Now for each new sample $n$ we have to shift this mirrored sequence of input signal samples over  $n$ samples
and calculate the sum of the element by element multiplication of the two sequences $h[k]$ and $x[n-k]$. The intermediate results of the sequence $x[n-k]$, for ${\color{blue}{n=0}}, {\color{red}{n=1}}$ and ${\color{green}n=2}$, are depicted in the figure below, while the result of the convolution sum procedure for all indices $n$ is as follows:
\begin{eqnarray*}
\vdots & \vdots & \vdots \newline
n=-1 & \Rightarrow & y[-1]=h[0] x[-1] + h[1]x[-2] + h[2] x[-3] = 0 \newline
{\color{blue}{n=0}} & \Rightarrow & {\color{blue}{y[0]}}=h[0] x[{\color{blue}{0}}] + h[1]x[-1] + h[2] x[-2] = 1 \newline
{\color{red}{n=1}} & \Rightarrow & {\color{red}{y[1]}}=h[0] x[{\color{red}{1}}] + h[1]x[0] + h[2] x[-1] = 3 \newline
{\color{green}{n=2}} & \Rightarrow & {\color{green}{y[2]}}=h[0] x[{\color{green}{2}}] + h[1]x[1] + h[2] x[0] = 6 \newline
n=3 & \Rightarrow & y[3]=h[0] x[3] + h[1]x[2] + h[2] x[1] = 5 \newline
n=4 & \Rightarrow & y[4]=h[0] x[4] + h[1]x[3] + h[2] x[2] = 3 \newline
n=5 & \Rightarrow & y[5]=h[0] x[5] + h[1]x[4] + h[2] x[3] = 0 \newline
\vdots & \vdots & \vdots
\end{eqnarray*}
Thus the output signal samples can be described as:
$y[n] = \delta[n] + 3 \delta[n-1] + 6 \delta[n-2] + 5 \delta[n-3] + 3 \delta[n-4]$
which is depicted at the lower right corner of the figure below.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/FIR/exconvolution.svg"
      alt="Example of convolution sum procedure."
    />
    <figcaption>
      Example of convolution sum procedure.
    </figcaption>
  </figure>
</div>
</div>
</div>




From the previous example it follows that the convolution sum procedure results in a finite length sequence of output signal samples in case both the sequences of the input signal samples and the impulse response have finite length. In general:

<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>When the length of an input sequence of signal samples is $N$ and the length of the sequence of impulse response values is $M$, then the convolution sum procedure results in a sequence of length $N+M-1$ output signal samples $y[n]$.</i></div>
<br>
