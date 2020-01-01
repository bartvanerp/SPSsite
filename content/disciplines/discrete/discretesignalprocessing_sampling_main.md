+++
title = "Basics of sampling and reconstruction"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Basics of sampling and reconstruction"
  weight = 20

+++

## Module overview
This module will cover one of the most fundamental aspects in signal processing, namely the principle behind converting a continuous-time signal into a discrete-time signal in order to process it with the help of computers.

1. <a href="../discretesignalprocessing_sampling_sampling">Sampling of sinusoidal signals</a> - First the concept of sampling is discussed, which represents the conversion from the continuous-time to discrete-time domain. The frequency of the sampled signal is better to be described by a relative frequency, because of the effect of the sampling process. Through the sampling there can also be a loss of spectral information, known as aliasing. This is caused by the uniqueness issue.
2. <a href="../discretesignalprocessing_sampling_reconstruction">Reconstruction of sinusoidal signals</a> - Similarly to the sampling, the signal can also be converted back from the discrete-time domain to the continuous-time domain. In order to prevent aliasing the sampling theorem has to be satisfied.

<br></br>

## Examples
<iframe width="100%" height="450" src="https://www.youtube.com/embed/er2dUoPBKL4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

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
   Given the following situation:
   <div style="max-width: 600px; margin: auto">
     <figure>
       <img
         src="/../files/7.Images/discrete/sampling/quiz/question1.PNG"
         alt="CD converter, question 1."
       />
     </figure>
   </div>
   where $x(t) = \cos(2\pi\cdot f_0 t)$ and $f_s > 2\cdot f_0$. Two cases are defined as: <br>
   case 1: $f_s = f_{s1} \rightarrow x_1[n]=\cos(\theta_1 n)$<br>
   case 2: $f_s = 1/3\cdot f_{s1} \rightarrow x_2[n]=\cos(\theta_2n)$<br>
   In the equation $\theta_2= \alpha\cdot \theta_1$, what is the value of $\alpha$?
</br>
    <input type="radio" name="question1">
       <label>$\alpha=\frac{1}{3}$</label><br/>
    <input type="radio" id="answer1" name="question1">
        <label for="answer1">$\alpha=3$</label><br/>
    <input type="radio"  name="question1">
        <label>$\alpha=6$</label><br/>
    <input type="radio"  name="question1">       
        <label>$\alpha=3\pi$</label><br/>
    <input type="radio"  name="question1">
        <label>None of the answers is correct.</label><br/>
 </div>
 </div>
 <br>
<button class="collapsible">Question 2</button>
<div class="content">
<div class="scp-quizzes-data quiz">
  Given the following situation:
  <div style="max-width: 600px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/sampling/quiz/question2.PNG"
        alt="CD and DC converter, question 2."
      />
    </figure>
  </div>
  where $x(t)=\cos(2\pi 50 t + \frac{\pi}{3})\cdot \sin(2\pi 700 t - \frac{\pi}{3})$. <br>
  What is the minimal sampling rate $f_s$ to obtain no aliasing, thus $y(t)=x(t)$.
<br>
</br>
    <input type="radio" name="question2">
      <label>$f_s > 700$ Hz</label><br/>
    <input type="radio" name="question2">
      <label>$f_s > 750$ Hz</label><br/>
    <input type="radio"  name="question2">
      <label>$f_s > 1400$ Hz</label><br/>    
    <input type="radio" id="answer2"  name="question2">
      <label for="answer2">$f_s > 1500$ Hz</label><br/>
    <input type="radio" name="question2">
      <label>None of the answers is correct.</label><br/>
 </div>
</div>
<br>
<button class="collapsible">Question 3</button>
<div class="content">
<div class="scp-quizzes-data quiz">
    Given the following situation:
    <div style="max-width: 600px; margin: auto">
      <figure>
        <img
          src="/../files/7.Images/discrete/sampling/quiz/question3.PNG"
          alt="CD and DC converter, question 3."
        />
      </figure>
    </div>
    where<br>
    $f_{si} = 500$ [samples/sec] <br>
    $f_{so} = 400$ [samples/sec] <br>
    $x(t) = \cos(2\pi\cdot100t)$ and $y(t) = \cos(2\pi\cdot f_y t)$<br>
    What is the value of $f_y$?
<br>
</br>
    <input type="radio" name="question3">
      <label>$f_y = 50$ [Hz]</label><br/>
    <input type="radio" id="answer3" name="question3">
      <label for="answer3">$f_y = 80$ [Hz]</label><br/>
    <input type="radio"  name="question3">
      <label>$f_y = 100$ [Hz]</label><br/>
      <input type="radio"  name="question3">
        <label>$f_y = 125$ [Hz]</label><br/>
        <input type="radio"  name="question3">
          <label>$f_y = 200$ [Hz]</label><br/>
    <input type="radio" name="question3">
      <label>None of the answers is correct.</label><br/>
 </div>
</div>
<br>
<button class="collapsible">Question 4</button>
<div class="content">
<div class="scp-quizzes-data quiz">
  Given the following situation:
  <div style="max-width: 600px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/sampling/quiz/question4.PNG"
        alt="CD and DC converter including input signal, question 4."
      />
    </figure>
  </div>
  How do we have to choose $f_s$ in order to obtain no aliasing, thus $y(t) = x(t)$?
<br>
</br>
    <input type="radio" name="question4">
       <label>$f_s = 1/2$ [Hz]</label><br/>
    <input type="radio"  name="question4">
        <label>$f_s = 1$ [Hz]</label><br/>
    <input type="radio"  name="question4">
       <label>$f_s = 2$ [Hz]</label><br/>
   <input type="radio" id="answer4" name="question4">
      <label for="answer4">None of the answers is correct.</label><br/>
 </div>
</div>
<br>
</div>
</div>


### Exercise bundle

<object data="/../files/3.Exercises/3.SAA-exercises.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/3.Exercises/3.SAA-exercises.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/3.Exercises/3.SAA-exercises.pdf">Download PDF</a>.</p>
    </embed>
</object>

### Answers
Download the answers <a href="/../files/3.Exercises/Answers/3.SAA-answers.pdf">here</a>.

### Pencast videos
<iframe width="100%" height="450" src="https://www.youtube.com/embed/videoseries?list=PL2LT3LoI-pPHjRcAglKEybG4eE5b9MtdP" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

_The above video player contains a playlist of all pencast videos which can be expanded by clicking the playlist icon in the upper-right corner._

<br></br>

## MATLAB lab
Accompanied to this modules are some exercises in MATLAB, which will test your knowledge of the module and will help improve your MATLAB skills.

### Lab assignment
<object data="/../files/10.Matlab/Lab 4 - Sampling.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/10.Matlab/Lab 4 - Sampling.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/10.Matlab/Lab 4 - Sampling.pdf">Download PDF</a>.</p>
    </embed>
</object>

### MATLAB demo
<iframe width="100%" height="450" src="https://www.youtube.com/embed/xk942JXSNxg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br></br>

## Summary
$$
\text{Relation absolute- and relative- frequency:}  \qquad
\boxed{\theta = \omega \cdot T_s= 2 \pi \frac{f}{f_s}}
$$

<br>
<table style="width:100%">
  <tr>
    <th>Frequency</th>
    <th>Symbol</th>
    <th>Unit</th>
  </tr>
  <tr>
    <td>Absolute frequency</td>
    <td>$f$</td>
    <td>[Hz]</td>
  </tr>
  <tr>
    <td>Absolute radial frequency</td>
    <td>$\omega$</td>
    <td>[rad/sec]</td>
  </tr>
  <tr>
    <td>Relative frequency</td>
    <td>$\theta$</td>
    <td>[-]</td>
  </tr>
</table>

<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The spectral representation of a discrete-time signal $x[n]$ is not unique.
The relative frequency representation is periodic with period $2\pi$.</i></div>

<br>
<table style="width:100%">
  <tr>
    <th>Frequency</th>
    <th>Symbol</th>
    <th>Fundamental Interval</th>
  </tr>
  <tr>
    <td>Relative frequency</td>
    <td>$\theta$</td>
    <td>$-\pi < \theta \leq \pi$</td>
  </tr>
  <tr>
    <td>Absolute frequency</td>
    <td>$f$</td>
    <td>$-\frac{f_s}{2} < f \leq \frac{f_s}{2}$</td>
  </tr>
  <tr>
    <td>Absolute radial frequency</td>
    <td>$\omega$</td>
    <td>$-\pi f_s < \omega \leq \pi f_s$</td>
  </tr>
</table>
</div>

<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>An ideal D-to-C convertor chooses the relative frequencies within the FI: $- \pi < \theta \leq \pi$. This implies that in case a continuous-time absolute frequency is converted with an C-to-D conversion outside the FI, such a frequency will always first be mapped inside the FI and the D-to-C convertor will use this frequency for the conversion of the discrete-time signal into a continuous-time signal. This mapping back into the FI is called <b>Aliasing</b></i></div>

<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Only in case of sampled sinusoidal signals the ideal D-to-C convertor in effect replaces $n$ by $t \cdot f_s$.</i></div>

<br>
$$
\boxed{
\text{Interpolation equation:} \qquad y(t)= \sum_{n=-\infty}^{\infty} x[n] p(t-n \cdot T_s)}
$$

<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i><b> Sampling theorem:</b> A continuous-time signal $x(t)$ with frequencies no higher than $f_{max}$ can be reconstructed exactly from its samples $x[n]= x(t)\mid_{t=n \cdot T_s}$, if samples are taken at a rate $f_s=1/T_s$, that is greater than $2 f_{max}$.</i></div>
