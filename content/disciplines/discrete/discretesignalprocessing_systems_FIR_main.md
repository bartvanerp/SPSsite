+++
title = "Finite impulse response (FIR) filter"

# date = {{ .Date }}
lastmod = 2019-10-10

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Finite impulse response (FIR) filter"
  weight = 41
  parent = "Discrete-time systems"

+++

## Difference equation
An example of a filter operation is the calculation of the running average of a sequence of samples. The general expression for an $M$-point running average filter equals
$$
y[n] = \frac{1}{M} \left \\{ x[n] + x[n-1] + \cdots + x[n-(M-1)] \right \\} = \frac{1}{M} \sum\_{k=0}^{M-1} x[n-k]
$$
in which $M$ is an integer number.
From this equation it follows that each new output sample $y[n]$ is equal to the average of $M$ preceding input samples. Thus the equation describes the relation between the input and output signal samples of a discrete-time system or filter. Such an equation is called a *difference equation* (DE).

<div class="example">
<h4> Example </h4>
<hr>
Calculate and plot the 3-point running averaged output samples $y[n]$ when the input sequence of samples is given by:
$$
x[n]=2 \delta[n] + 4 \delta[n-1] + 6 \delta[n-2] + 4 \delta[n-3] + 2 \delta[n-4]
$$
<button class="collapsible">Show solution</button>
<div class="content">
The DE of a 3-point running average filter is as follows:
$$
y[n] = \frac{1}{3} \left \{ x[n] + x[n-1] + x[n-2] \right \}
$$
Together with the given input sequence of samples we obtain:
\begin{eqnarray*}
\vdots & & \vdots \\
y[-1] &=& \frac{1}{3} \left \{ x[-1] + x[-2] + x[-3] \right \} = 0\\
y[0] &=& \frac{1}{3} \left \{ x[0] + x[-1] + x[-2] \right \} = \frac{2}{3}\\
y[1] &=& \frac{1}{3} \left \{x[1] +  x[0] + x[-1]  \right \} = 2\\
y[2] &=& \frac{1}{3} \left \{x[2] + x[1] +  x[0] \right \} = 4\\
y[3] &=& \frac{1}{3} \left \{x[3] +  x[2] + x[1]  \right \} = \frac{14}{3}\\
y[4] &=& \frac{1}{3} \left \{x[4] +  x[3] + x[2]  \right \} = 4\\
y[5] &=& \frac{1}{3} \left \{x[5] +  x[4] + x[3]  \right \} = 2\\
y[6] &=& \frac{1}{3} \left \{x[6] +  x[5] + x[4]  \right \} = \frac{2}{3}\\
y[7] &=& \frac{1}{3} \left \{x[7] +  x[6] + x[5]  \right \} = 0\\
\vdots & & \vdots
\end{eqnarray*}
Thus we can write the sequence of output samples mathematically as follows:
$$
y[n]= \frac{2}{3}\delta[n] + 2 \delta[n-1] + 4 \delta[n-2] + \frac{14}{3} \delta[n-3] + 4 \delta[n-4] +2 \delta[n-5] + \frac{2}{3} \delta[n-6]
$$
which is depicted in the figure below.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/FIR/3pointaverage.svg"
      alt="Example of a 3-point running average operation."
    />
    <figcaption>
      Example of a 3-point running average operation.
    </figcaption>
  </figure>
</div>
</div>
</div>


Fig. 1 shows the effect of an $M$-point running average filter for increasing values of $M$. For this example the input signal $x[n]$ consists of a fluctuation ($0.5 \cos(2 \pi n/8 + \pi/4)$)on top of a 'trend' ($1.01^n$). When we are interested in the trend of $x[n]$, we need to get rid of the fluctuations. This can be achieved by applying an $M$-point running average filter. From Fig. 1 it follows that the larger we choose $M$, the more the fluctuations are removed since the averaging is performed over more samples.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/FIR/trendincosine.svg"
      alt="Result of averaging operation: For larger $M$ less fluctuations."
    />
    <figcaption class="numbered">
      Result of averaging operation: For larger $M$ less fluctuations.
    </figcaption>
  </figure>
</div>

From the difference equation of the $M$-point running average filter it follows that each of the $M$ input samples contributed by a factor $\frac{1}{M}$ to the output $y[n]$, or in other words each input sample is weighted by the same number $\frac{1}{M}$.
For a general filter operation these weights do not need to be the same. Thus we can generalize the difference equation by weighting each signal sample $x[n-k]$ by $b_k$:

$$
y[n]= b\_0 x[n] + b\_1 x[n-1] +\ldots + b\_{M-1} x[n-(M-1)]=\sum\_{k=0}^{M-1} b\_k x[n-k]
$$

Further on we will see that this is the DE of a so-called Finite Impulse Response (FIR) filter.

<br></br>

## Basic building blocks
When realizing or implementing a discrete-time filter, it follows from the general DE of an FIR filter, as denoted in the equation above, that we need the following basic building blocks: A multiplier, which multiplies signal sample $x[n]$ by a scalar $\beta$ which results in a sample with value $y[n] = \beta \cdot x[n]$; An adder which adds two signal samples $x_1[n]$ and $x_2[n]$ together into $y[n]= x_1[n] + x_2[n]$ and finally an unit delay operator which delays a signal sample $x[n]$ by one sample index into $y[n]=x[n-1]$. These basic building blocks are depicted in Fig. 2.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/FIR/basicbuildingblocks.svg"
      alt="Basic building blocks of discrete-time filters."
    />
    <figcaption class="numbered">
      Basic building blocks of discrete-time filters.
    </figcaption>
  </figure>
</div>


<div class="example">
<h4> Example </h4>
<hr>
Draw a realization scheme of the system which is described by the following DE: $y[n]=2x[n-1] -\frac{1}{2}x[n-3]$.
<button class="collapsible">Show solution</button>
<div class="content">
The realization scheme is depicted in the figure below. This scheme consists of 3 unit-delay elements, since we need delayed input signal samples up to $x[n-3]$. The signal sample $x[n-1]$ is multiplied by $2$, resulting in the signal sample $v_1[n]$., while the signal sample $x[n-3]$ is multiplied by $-\frac{1}{2}$, resulting in $v_2[n]$. Finally the output $y[n]$ is obtained by adding the signal samples $v_1[n]$ and $v_2[n]$.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/FIR/implementationexample.svg"
      alt="Implementation scheme (signal flow graph) of a simple discrete-time filter."
    />
    <figcaption>
      Implementation scheme (signal flow graph) of a simple discrete-time filter.
    </figcaption>
  </figure>
</div>
</div>
</div>


### Realization scheme finite impulse response (FIR) filter
From the DE of an FIR filter it follows that a general realization scheme of an FIR filter can be depicted as done in Fig. 3.

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


### Difference equation from realization scheme
Sometimes we have available the realization scheme and we want to evaluate the DE which describes the relation between the input- and output signal of the system. In case the system is very complex, it may be convenient to define intermediate signals in the realization scheme. Then find the DE's with respect to these intermediate signals and finally substitute all intermediate DE's into each other.

<div class="example">
<h4> Example </h4>
<hr>
Give the difference equation of the system as depicted in the following figure:
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/FIR/transpose2ndord.svg"
      alt="Implementation scheme (signal flow graph) of a simple discrete-time filter."
    />
    <figcaption>
      Implementation scheme (signal flow graph) of a simple discrete-time filter.
    </figcaption>
  </figure>
</div>
<br>
<button class="collapsible">Show solution</button>
<div class="content">
By defining the following intermediate signals together with their difference equation's:
\begin{eqnarray*}
y[n] &=& b_0 x[n] + {\color{blue}{v_1[n-1]}} \\
{\color{blue}{v_1[n]}} &=& b_1 x[n] + {\color{red}{v_2[n-1]}} \\
{\color{red}{v_2[n]}} &=& b_2 x[n]
\end{eqnarray*}
and by substituting these DE's into each other, we obtain:
\begin{eqnarray*}
\Rightarrow \mbox{ } {\color{blue}{v_1[n]}} &=& b_1 x[n] + {\color{red}{b_2 x[n-1]}} \\
\Rightarrow \mbox{ }y[n] &=& b_0 x[n] + {\color{blue}{ b_1 x[n-1] + b_2 x[n-2]}}
\end{eqnarray*}
</div>
</div>

<br></br>

## The impulse response

### Screencast video
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/20j0M8b_pu4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>
<br>

In the previous section we have seen that the DE describes the input-output relation of a system. In this section we will introduce yet another way to describe a system, namely by its impulse response, denoted by ${\color{red}{h[n]}}$. The impulse response of a system is defined as the response of a system when the input is a unit delta pulse, thus $x[n]={\color{red}{\delta[n]}}$. This is depicted in Fig. 4.

<div style="max-width: 500px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/FIR/impulseresponse.svg"
      alt="Impulse response ${\color{red}{h[n]}}$ of a system."
    />
    <figcaption class="numbered">
      Impulse response ${\color{red}{h[n]}}$ of a system.
    </figcaption>
  </figure>
</div>


<div class="example">
<h4> Example </h4>
<hr>
Given the following DE: $y[n]= \sum_{k=0}^{2} x[n-k]$. Draw the realization scheme. Furthermore, give a mathematical expression of the impulse response $h[n]$ of this system and draw a plot of $h[n]$ in the range $n = -1,0,1,2,3,4$.
<button class="collapsible">Show solution</button>
<div class="content">
The realization scheme is depicted in the figure below. When applying a unit delta pulse $x[n]=\delta[n]$ to the input we obtain the impulse response $y[n]=h[n]$. Thus:
\begin{eqnarray*}
\vdots & & \vdots \\
y[-1]=h[-1] &=& x[-1]+x[-2]+x[-3]=0 \\
y[0]=h[0] &=& x[0]+x[-1]+x[-2]=1 \\
y[1]=h[1] &=& x[1]+x[0]+x[-1]=1 \\
y[2]=h[2] &=& x[2]+x[1]+x[0]=1\\
y[3]=h[3] &=& x[3]+x[2]+x[1]=0\\
\vdots & & \vdots
\end{eqnarray*}
From this it follows that the impulse response of this system can mathematically be described as:
$$
h[n]= \delta[n] + \delta[n-1] + \delta[n-2] =\sum_{k=0}^{2} \delta[n-k]
$$
which is also depicted in the figure below.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/FIR/imprespexample.svg"
      alt="Example of an impulse response ${\color{red}{h[n]}}$ of a system."
    />
    <figcaption>
      Example of an impulse response ${\color{red}{h[n]}}$ of a system.
    </figcaption>
  </figure>
</div>
</div>
</div>

From the definition of the impulse response it follows that the impulse response $h[n]$ of an FIR filter, from which the realization scheme is depicted in Fig. 3, has the following weights:
$$
\begin{eqnarray}
\vdots & &  \newline
y[-1]=h[-1] &=& 0 \newline
y[0]=h[0] &=& b\_0 \newline
y[1]=h[1] &=& b\_1 \newline
\vdots & &  \newline
y[M-1]=h[M-1] &=& b\_{M-1} \newline
\vdots & &
\end{eqnarray}
$$
Thus the impulse response $h[n]$ of an FIR filter equals:

\begin{equation}
\boxed{
h[n] = \sum_{k=0}^{M-1} b_k \delta[n-k]}
\end{equation}
In other words, the impulse response values $h[n]$ of an FIR filter are equal to the weight of the FIR filter. Furthermore, since the number of weights in the realization scheme is finite,
it follows that the impulse response of an <b>F</b>IR has indeed <b>Finite</b> length $M$.

### Causality
From the realization scheme of an FIR, as depicted in Fig. 3, it follows that the output signal samples $y[n]$ only depend on the current and previous input signal samples. Thus the output sample $y[n]$ depends on input signal samples $x[n-k]$ for $k \geq 0$. This implies that the impulse  response $h[n]$ of the realization scheme of an FIR, as depicted in Fig. 3, can only have values for $n \geq 0$. Such a system is called a <b>causal</b> system.

<div class="example">
<h4> Example </h4>
<hr>
Is the system, which is described by the DE $y[n]=3 x[n+1] -x[n] + 2x[n-1]$, causal or non-causal?
<button class="collapsible">Show solution</button>
<div class="content">
From the DE it follows that the impulse response of this system equals $h[n]=3 \delta[n+1] - \delta[n] + 2 \delta[n-1] $. Since $h[-1]=3$, it follows that this system is {\bf Non-causal}: In order to calculate the output signal sample for time index $n$, we need input signal sample for index $n+1$, which in the future of index $n$. Thus we need an 'inverse' delay, which is impossible to realize such a non-causal system. In other words: We can't realize a non-causal system with an FIR scheme as depicted in Fig. 3, since we can't realize an 'inverse' delay $T^{-1}$.
</div>
</div>

<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>A causal system has an impulse response for which $h[n]=0$ for $n<0$.</i></div>
<br>

<br></br>

## The convolution sum

### screencast video
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/7Q8w8XkYmHk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>
<br>

Because of the fact that the impulse response coefficients of an FIR filter are equal to the weights of the filter, it follows from Fig. 3 that the DE can be written as:
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
\begin{equation}
y[n] =  \sum_{k=0}^{M-1} h[k] x[n-k] \equiv h[n] \star x[n]
\end{equation}


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

<br></br>

## Linear time invariance (LTI)

### Screencast video
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/JnP9ybC6wJc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>
<br>
The FIR filter, as described in the previous sections, belongs to a general class of systems that is used very often in practice: The so called <b>Linear Time Invariant (LTI)</b> systems.
In the first subsections the definitions Linearity and Time Invariance are given. In the last subsection it will be shown that the convolution sum operator is a result of LTI.

In this section the new symbol $x[n] \mapsto y[n]$ will be used with the following interpretation: The system maps the sequence of input signal samples $x[n]$ to the sequence of output signal samples $y[n]$.

### Linear systems
When a system results into the following mappings: $x_1[n] \mapsto y_1[n]$ and $x_2[n] \mapsto y_2[n]$, then such a system is Linear if for any linear combination of input sequences $x_1[n]$ and $x_2[n]$ the system maps this linear combination to the same linear combination of output sequences $y_1[n]$ and $y_2[n]$. With scalars $\alpha$ and $\beta$, this definition can mathematically be described as follows:
\begin{equation}
\boxed{
x[n]= \alpha x_1[n] + \beta x_2[n] \mapsto y[n]= \alpha y_1[n] + \beta y_2[n]}
\end{equation}
A visualisation of this definition is depicted in Fig. 5.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/FIR/linear.svg"
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
Referring to the left-hand side of Fig. 5 we obtain:
$$
y[n] = \left ( x[n] \right )^2 =
\left ( \alpha x_1[n] + \beta x_2[n] \right )^2 = \alpha ^2 x_1^2[n] + 2 \alpha \beta x_1[n] x_2[n] + \beta ^2 x_2^2[n]
$$
Referring to the right-hand side of Fig. 5 we obtain:
$$
w[n] = \alpha y_1[n] + \beta y_2[n] = \alpha x_1^2[n] + \beta x_2^2[n]
$$
Since $w[n] \neq y[n]$ it follows that the system $y[n]= ( x[n])^2$ is non-linear.
</div>
</div>


### Time Invariant systems
When a system results into the following mapping: $x[n] \mapsto y[n]$ then a system is Time Invariant
if a delayed sequence of input samples $x[n-n_0]$ is mapped by the system to a sequence of output samples $y[n-n_0]$, which is delayed by the same amount of samples. With integer delay $n_0$, this definition can mathematically be described as follows:
\begin{equation}
\boxed{
x[n] \mapsto y[n] \hspace{3mm} \Rightarrow \hspace{3mm} x[n-n_0] \mapsto y[n-n_0]}
\end{equation}
A visualisation of this definition is depicted in Fig. 6.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/FIR/timeinv.svg"
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
From the upper part of Fig. 6 it follows that
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
\begin{eqnarray}
\delta[n] \mapsto h[n] & \Rightarrow & \delta[n-k] \overset{\text{TI}}{\mapsto} h[n-k] \text{ for any } k\newline
& \Rightarrow & x[k] \delta[n-k] \overset{\text{L}}{\mapsto} x[k] h[n-k] \text{ for any } k \newline
& \Rightarrow & \sum\_k x[k] \delta[n-k] \overset{\text{L}}{\mapsto} y[n] = \sum\_k x[k] h[n-k] = x[n] \star h[n]
\end{eqnarray}
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
\begin{eqnarray}
y[n] &=& h[n] \star x[n] = \sum\_{k = - \infty}^{\infty} h[k] x[n-k] \newline
&\overset{p=n-k}{=}& \sum\_{p = +\infty}^{-\infty} h[n-p] x[p]= \sum\_{p = - \infty}^{\infty} x[p] h[n-p]= x[n] \star h[n]
\end{eqnarray}
$$

Note that for an FIR filter the range of the convolution sum is automatically limited by the finite length of the impulse response.
Thus in case of an FIR filter the commutative property of the convolution sum operator results on the one hand into:
\begin{equation}
y[n] = h[n] \star x[n] = \sum\_{k=-\infty}^{\infty} h[k] x[n-k] \overset{\text{FIR}}{=}\sum\_{k=0}^{M-1} h[k] x[n-k]
\end{equation}
where we used the fact that $h[n]=0$ for $n<0$ and $n>M$. On the other hand we have:
\begin{equation}
y[n]= x[n] \star h[n] = \sum\_{k=-\infty}^{\infty} x[k] h[n-k] \overset{\text{FIR}}{=} \sum\_{k=n-(M-1)}^{n} x[k] h[n-k]
\end{equation}
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
The upper left hand figure of Fig. 7 shows the cascading of two LTI systems, one with impulse response $h_1[n]$ and the other one with impulse response $h_2[n]$. When applying a delta pulse ${\color{red}{\delta[n]}}$ to the first LTI system, the output equals the impulse response ${\color{red}{h_1[n]}}$. When applying this sequence to the second LTI system, the result is the convolution sum result ${\color{red}{h_1[n] \star h_2[n]}}$.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/FIR/cascadeequiv.svg"
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
which is shown in the lower right part of Fig. 7. This combined impulse response can be split again into the cascading of two LTI systems, as shown in the upper right figure. In this last step however the LTI systems with impulse response $h_1[n]$ and $h_2[n]$ have interchanged from order.

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
      src="/../files/7.Images/discrete/systems/FIR/examplecascade.svg"
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


## Exercises
In this section several exercises are available, including their answers. The exercises marked in <span style="color:blue">*blue*</span> are explained by means of more extensive pencast videos.


### Video quiz

<div class="example">
<button class="collapsible">Test your knowledge (click to expand)</button>
<div class="content">
<button class="collapsible">Question 1</button>
<div class="content">
<div class="scp-quizzes-data quiz">
   Given the signal $x[n]$ below: <br>
   $x[n] = \begin{cases}0 & \text{for } n \text{ even} \\ 1 &\text{for } n \text{odd}\end{cases}$ <br>
   The Difference Equation (DE) is given as: <br>
   $y[n] = x[n] + x[n-1] + x[n-2]$ <br>
   Calculate $y[n]$ for $n$ even and $n$ odd.
   <br>
   </br>
       <input type="radio" name="question1">
       <label>$x[n] = \begin{cases}0 & \text{for } n \text{ even} \\ 1 &\text{for } n \text{ odd}\end{cases}$ </label><br/>
    <input type="radio" id="answer1" name="question1">
        <label for="answer1">$x[n] = \begin{cases}1 & \text{for } n \text{ even} \\ 2 &\text{for } n \text{ odd}\end{cases}$ </label><br/>
    <input type="radio"  name="question1">
        <label>$x[n] = \begin{cases}-1 & \text{for } n \text{ even} \\ 2 &\text{for } n \text{ odd}\end{cases}$ </label><br/>
    <input type="radio"  name="question1">       
        <label>$x[n] = \begin{cases}-1 & \text{for } n \text{ even} \\ -2 &\text{for } n \text{ odd}\end{cases}$ </label><br/>
    <input type="radio"  name="question1">       
        <label>$x[n] = \begin{cases}1 & \text{for } n \text{ even} \\ 0 &\text{for } n \text{ odd}\end{cases}$ </label><br/>
    <input type="radio"  name="question1">       
        <label>$x[n] = \begin{cases}1 & \text{for } n \text{ even} \\ -2 &\text{for } n \text{ odd}\end{cases}$ </label><br/>
    <input type="radio"  name="question1">
        <label>None of the answers is correct.</label><br/>
 </div>
 </div>
 <br>
<button class="collapsible">Question 2</button>
<div class="content">
<div class="scp-quizzes-data quiz">
  Given the impulse response of an LTI system: <br>
  $h_1[n] = \delta [n] + \delta[n-1] - \delta[n-2]$ <br>
  Let the input of this system be the unit step function:<br>
  $x[n] = u[n] = \begin{cases} 1 & \text{for } n \geq 0 \\ 0 & \text{elsewhere}\end{cases}$ <br>
  $y[n] = x[n] \ast h[n]$ <br>
Calculate the output of this system for the given input.
<br>
</br>
    <input type="radio" name="question2">
      <label>$y[n] = \delta[n] + \delta[n-1] + \delta[n-2]$</label><br/>
    <input type="radio" name="question2">
      <label>$y[n] = \delta[n] + \delta[n-1] - \delta[n-2]$</label><br/>
    <input type="radio"  name="question2">
      <label>$y[n] = \delta[n] + 2\delta[n-1] - \delta[n-2]$</label><br/>    
    <input type="radio"  name="question2">
      <label>$y[n] = \delta[n] + 2\delta[n-1] + \delta[n-2]$</label><br/>
    <input type="radio" id="answer2" name="question2">
      <label for="answer2">None of the answers is correct.</label><br/>
 </div>
</div>
<br>
<button class="collapsible">Question 3</button>
<div class="content">
<div class="scp-quizzes-data quiz">
    Given the cascade of 2 LTI systems in series, with the following individual impulse responses: <br>
    $h_1 [n] = \delta[n] + 2\delta[n-1]$ <br>
    $h_2 [n] = \delta[n] - \delta[n-1]$ <br>
    Whta is the total impulse response $h[n]$ of the LTI system?
<br>
</br>
    <input type="radio" id="answer3"  name="question3">
      <label for="answer3">$h[n] = \delta[n] + \delta[n-1] -2 \delta[n-2]$</label><br/>
    <input type="radio" name="question3">
      <label>$h[n] = 3\delta[n-1] $</label><br/>
    <input type="radio"  name="question3">
      <label>$h[n] = \delta[n] + 2\delta[n-1] + \delta[n-2] - \delta[n-3]$</label><br/>
      <input type="radio"  name="question3">
        <label>$h[n] = 2\delta[n] + \delta[n-1]$</label><br/>
    <input type="radio" name="question3">
      <label>None of the answers is correct.</label><br/>
 </div>
</div>
<br>
<button class="collapsible">Question 4</button>
<div class="content">
<div class="scp-quizzes-data quiz">
  Consider an LTI system where the output $y[n]$ has been recorded from two different inputs $x[n]$ as shown below:
  $x_1[n] = \delta[n] + \delta[n-1] \quad \rightarrow \quad y_1[n] = \delta[n] + \delta[n-1] - \delta[n-2] - \delta[n-3]$ <br>
  $x_2[n] = \delta[n] - \delta[n-1] \quad \rightarrow \quad y_2[n] = \delta[n] - \delta[n-1] - \delta[n-2] + \delta[n-3]$ <br>
  What is the impulse response $h[n]$ of this LTI system?
<br>
</br>
    <input type="radio" id="answer4" name="question4">
       <label for="answer4">$h[n] = \delta[n] - \delta[n-2]$</label><br/>
    <input type="radio"  name="question4">
        <label>$h[n] = \delta[n] + \delta[n-2]$</label><br/>
    <input type="radio"  name="question4">
       <label>$h[n] = \delta[n-1] - \delta[n-2]$</label><br/>
   <input type="radio"  name="question4">
      <label>$h[n] = \delta[n] + \delta[n-1]$</label><br/>
  <input type="radio"  name="question4">
      <label>$h[n] = \delta[n-1] + \delta[n-2]$</label><br/>
  <input type="radio"  name="question4">
      <label>$h[n] = -\delta[n-1] - \delta[n-2]$</label><br/>
  <input type="radio"  name="question4">
      <label>$h[n] = \delta[n] - \delta[n-1]$</label><br/>
  <input type="radio"  name="question4">
      <label>$h[n] = -\delta[n-1] + \delta[n-2]$</label><br/>
   <input type="radio" name="question4">
      <label>None of the answers is correct.</label><br/>
 </div>
</div>
<br>
<button class="collapsible">Question 5</button>
<div class="content">
<div class="scp-quizzes-data quiz">
  Given the following FIR filter from which the initial state is equal to zero, thus $y[n] = 0$ for $n<0$.
  <div style="max-width: 600px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/systems/FIR/quiz/question5.PNG"
        alt="FIR filter, question 5."
      />
    </figure>
  </div>
  What is the value of $y[3]$?
<br>
</br>
    <input type="radio" name="question5">
       <label>$y[3] = -3$</label><br/>
    <input type="radio"  name="question5">
        <label>$y[3] = -2$</label><br/>
    <input type="radio"  id="answer5" name="question5">
       <label for="answer5">$y[3] = -1$</label><br/>
   <input type="radio"  name="question5">
      <label>$y[3] = 0$</label><br/>
  <input type="radio"  name="question5">
      <label>$y[3] = 1$</label><br/>
  <input type="radio"  name="question5">
      <label>$y[3] = 2$</label><br/>
  <input type="radio"  name="question5">
      <label>$y[3] = 3$</label><br/>
   <input type="radio" name="question5">
      <label>None of the answers is correct.</label><br/>
 </div>
</div>
<br>
</div>
</div>

### Exercise bundle

<object data="/../files/3.Exercises/4.FIR-exercises.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/3.Exercises/4.FIR-exercises.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/3.Exercises/4.FIR-exercises.pdf">Download PDF</a>.</p>
    </embed>
</object>

### Answers
Download the answers <a href="/../files/3.Exercises/Answers/4.FIR-answers.pdf">here</a>.

### Pencast videos
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/videoseries?list=PL2LT3LoI-pPF8wIM4ys_57Vz18_18VQKJ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
_The above video player contains a playlist of all pencast videos which can be expanded by clicking the playlist icon in the upper-right corner._

<br></br>

## MATLAB lab
Accompanied to this modules are some exercises in MATLAB, which will test your knowledge of the module and will help improve your MATLAB skills.

### Lab assignment
<object data="/../files/10.Matlab/Lab 5 - FIR.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/10.Matlab/Lab 5 - FIR.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/10.Matlab/Lab 5 - FIR.pdf">Download PDF</a>.</p>
    </embed>
</object>

### MATLAB demo
<div class="video-container">
<iframe width="100%" height="450" src="https://www.youtube.com/embed/GLhOpGsN0F8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>

## Summary
$$
\boxed{\text{Unit delta pulse: }\qquad
\delta[n] = \begin{cases}
1 & n=0 \newline
0 & \text{elsewhere}
\end{cases}}
$$

<br>

$$
\boxed{\text{Unit step function: }\qquad
u[n] = \begin{cases}
1 & n \geq 0 \newline
0 & \text{elsewhere}
\end{cases}}
$$

<br>

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/FIR/FIR.svg"
      alt="Realization scheme of a finite impulse response filter."
    />
    <figcaption>
      Realization scheme of a finite impulse response filter.
    </figcaption>
  </figure>
</div>

<br>

$$
\boxed{\text{Difference Equation FIR: } \qquad y[n] = \sum_{k=0}^{M-1} b_k x[n-k] }
$$

<br>

$$
\boxed{\text{Impulse response FIR: } \qquad h[n] = \sum_{k=0}^{M-1} b_k \delta[n-k]}
$$

<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>A causal system has an impulse response for which $h[n]=0$ for $n<0$.</i></div>
<br>

$$
\boxed{\text{Convolution sum FIR: }\qquad
y[n] = \sum\_{k=0}^{M-1} h[k] x[n-k]= \sum\_{k=n-(M-1)}^{n} x[k] h[n-k] }
$$

<br>

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

<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>When the length of an input sequence of signal samples is $N$ and the length of the sequence of impulse response values is $M$, then the convolution sum procedure results in a sequence of length $N+M-1$ output signal samples $y[n]$.</i></div>
<br>


$$
\boxed{\text{Linearity:     }\qquad
x[n]= \alpha x_1[n] + \beta x_2[n] \mapsto y[n]= \alpha y_1[n] + \beta y_2[n]}
$$

<br>

$$
\boxed{\text{Time Invariance: }\qquad
x[n] \mapsto y[n] \hspace{3mm} \Rightarrow \hspace{3mm} x[n-n_0] \mapsto y[n-n_0]}
$$

<br>

$$
\boxed{
y[n]=h[n] \star x[n] = x[n] \star h[n]}
$$

<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The cascading of two LTI systems, one with impulse response $h_1[n]$ and the other one with impulse response $h_2[n]$, can be combined to one LTI system with impulse response $h[n]=h_1[n] \star h_2[n]$.</i></div>

<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The order of two LTI systems, one with impulse response $h_1[n]$ and the other one with $h_2[n]$, can be interchanged.</i></div>
<br>
