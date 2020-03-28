+++
title = "Finite impulse response (FIR) filter"

# date = {{ .Date }}
lastmod = 2019-10-10

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Filter structures I: Finite impulse response (FIR) filter"
  weight = 91

+++
## Introduction
Finite impulse response filters are the most basic types of filters. They simply weigh different delayed inputs in order to calculate the output. Because of this simplicity, this filter structure allows for a thorough analysis.

<br></br>
## Module overview
This module will cover the following topics:

1. <a href="../discretesignalprocessing_filters_fir_difference">Difference equation</a> - The difference equation is the mathematical description of an FIR filter. It describes the relationship between the input and output samples.
2. <a href="../discretesignalprocessing_filters_fir_convolution">Convolution</a> - The output of an FIR filter can be calculated using the convolution operation.
3. <a href="../discretesignalprocessing_filters_fir_lti">Linear time invariant</a> - The FIR filter, as described in the previous sections, belongs to a general class of systems that is used very often in practice.

<br></br>
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

### Pencast videos [⯈]
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

### MATLAB demo [⯈]
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
