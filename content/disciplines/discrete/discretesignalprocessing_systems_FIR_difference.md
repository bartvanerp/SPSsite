+++
title = "Difference equation"

# date = {{ .Date }}
lastmod = 2019-10-10

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Difference equation"
  weight = 1
  parent = "Systems I: Finite impulse response (FIR) filter"
+++

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
\begin{eqnarray*}
\vdots & &  \newline
y[-1]=h[-1] &=& 0 \newline
y[0]=h[0] &=& b\_0 \newline
y[1]=h[1] &=& b\_1 \newline
\vdots & &  \newline
y[M-1]=h[M-1] &=& b\_{M-1} \newline
\vdots & &
\end{eqnarray*}
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
