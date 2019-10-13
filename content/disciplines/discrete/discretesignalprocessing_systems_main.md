+++
title = "Discrete-time systems"

# date = {{ .Date }}
lastmod = 2019-10-10

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Discrete-time systems"
  weight = 40

+++

## Module overview
This module will introduce basic filter structures for filtering discrete-time signals.

1. <a href="../discretesignalprocessing_systems_fir/">Finite impulse response filters</a> - The most basic filter is defined as a finite impulse response filter. This section also introduces the commonly used convolution operator.
2. **Infinite impulse response filters** (to be added) - Besides filters with a finite impulse response, there also exist filters whose output depends on their previous outputs. This recursive operations leads to infinite impulse response filters, which posses different characteristics in comparison to finite impulse response filters.
3. **Special convolution methods** (to be added) - When performing filter calculations with a limited amount of memory, convolutions might not be possible to calculate if the signal length is very long. In order to circumvent this problem new procedures have been developed in order to split the convolution operation in multiple smaller ones.


## Exercises
In this section several exercises are available, including their answers. The exercises marked in <span style="color:blue">*blue*</span> are explained by means of more extensive pencast videos.


### Exercise bundle

<object data="/../files/3.Exercises/4.FIR-exercises.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/3.Exercises/4.FIR-exercises.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/3.Exercises/4.FIR-exercises.pdf">Download PDF</a>.</p>
    </embed>
</object>

### Answers
Download the answers <a href="/../files/3.Exercises/Answers/4.FIR-answers.pdf">here</a>.

### Pencast videos
<iframe width="100%" height="450" src="https://www.youtube.com/embed/videoseries?list=PL2LT3LoI-pPF8wIM4ys_57Vz18_18VQKJ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

_The above video player contains a playlist of all pencast videos which can be expanded by clicking the playlist icon in the upper-right corner._

## MATLAB lab
Accompanied to this modules are some exercises in MATLAB, which will test your knowledge of the module and will help improve your MATLAB skills.

### Lab assignment
<object data="/../files/10.Matlab/Lab 5 - FIR.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/10.Matlab/Lab 5 - FIR.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/10.Matlab/Lab 5 - FIR.pdf">Download PDF</a>.</p>
    </embed>
</object>

### MATLAB demo
<iframe width="100%" height="450" src="https://www.youtube.com/embed/GLhOpGsN0F8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Summary finite impulse response (FIR) filter
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
