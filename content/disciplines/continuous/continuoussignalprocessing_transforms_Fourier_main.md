+++
title = "Fourier series"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "Transforms II: Fourier series"
  weight = 42

+++

## Introduction
In the module on the <a href="../continuoussignalprocessing_transforms_spectrum_main">spectrum of sinusoidal signals</a> we studied the spectral behavior of the sum of sinusoidal signals. In this module we will study signals which are composed of a sum of harmonic related sine waves.


### Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/eUcFlwXPFb0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>
## Module overview
This module covers the following topics:

1. <a href="../continuoussignalprocessing_transforms_fourier_periodic">Periodic signals</a> - Signals can have a repetitive structure which is inherently related to the frequency structure of the signal. This section will discuss when a signal is periodic and how this period can be determined from its frequency content.
2. <a href="../continuoussignalprocessing_transforms_fourier_synthesis">Fourier series synthesis</a> - This section will give the representation of the Fourier series, which is a weighted sum of harmonic related phasor components.
3. <a href="../continuoussignalprocessing_transforms_fourier_analysis">Fourier series analysis</a> - Similarly, a signal can be decomposed into these harmonic related phasor components. This section will describe the procedure for calculating the corresponding weights.
4. <a href="../continuoussignalprocessing_transforms_fourier_examples">Examples</a> - In order to make sure that the reader gets properly acquainted with the topic, some additional examples are provided.

<br></br>

## Exercises
In this section several exercises are available, including their answers. The exercises marked in <span style="color:blue">*blue*</span> are explained by means of more extensive pencast videos. These exercises also include topics relating to the spectrum of sinusoidal signals.


### Video quiz

<div class="example">
<button class="collapsible">Test your knowledge (click to expand)</button>
<div class="content">
<button class="collapsible">Question 1</button>
<div class="content">
<div class="scp-quizzes-data quiz">
   Define the Fundamental Frequency of the signal $x(t) = x_1 + x_2 + x_3$, where
   $x_1= 4 + \sin(500\pi t - \frac{\pi}{3})$, $x_2 = \cos(2.8\pi t - \frac{\pi}{8})$ and $x_3 = \sin(2\pi\cdot 22t - \frac{\pi}{4})$.
</br>
    <input type="radio" id="answer1" name="question1">
       <label for="answer1">$F_0 = 0.2$ Hz</label><br/>
    <input type="radio" name="question1">
        <label>$F_0 = 0.4$ Hz</label><br/>
    <input type="radio" name="question1">
       <label>$F_0 = 0.8$ Hz</label><br/>
      <input type="radio"  name="question1">
         <label>None of the answers is correct.</label><br/>
 </div>
 </div>
 <br></br>
<button class="collapsible">Question 2</button>
<div class="content">
<div class="scp-quizzes-data quiz">
   With $F_0 = 1/T_0$ and integer $k=0,\pm 1, \pm 2 , \ldots$, what holds for the following expression?
   $\int_{-T_0/2}^{T_0/2}e^{jk2\pi F_0 t}dt = ?$
<br>
</br>
    <input type="radio" name="question2">
       <label>$=0$ for $k=0$</label><br/>
    <input type="radio" name="question2">
        <label>$=0$ for all values of $k$</label><br/>
    <input type="radio" id="answer2" name="question2">
       <label for="answer2">$\neq 0$ for $k=0$</label><br/>
    <input type="radio" name="question2">
      <label>$\neq 0$ for all values of $k$</label><br/>
    <input type="radio"  name="question2">
       <label>None of the answers is correct.</label><br/>
 </div>
</div>
<br></br>
<button class="collapsible">Question 3</button>
<div class="content">
<div class="scp-quizzes-data quiz">
  For what value of $\alpha$ does the following integral with $F_0=1/T_0$ hold?
  $\int_{0}^{\alpha T_0}e^{j2\pi F_0 t}dt = 0$
<br>
</br>
    <input type="radio" name="question3">
      <label>$\alpha = 1/4$</label><br/>
    <input type="radio" name="question3">
      <label>$\alpha = 2/4$</label><br/>
    <input type="radio" name="question3">
      <label>$\alpha = 3/4$</label><br/>
    <input type="radio"  id="answer3"  name="question3">
      <label for="answer3">$\alpha = 4/4$</label><br/>
    <input type="radio" name="question3">
      <label>None of the answers is correct.</label><br/>
 </div>
</div>
<br></br>
<button class="collapsible">Question 4</button>
<div class="content">
<div class="scp-quizzes-data quiz">
      With $F_0 = 1/T_0$ and positive integers $k$ and $l$, when does the following hold?
      $\int_{T_0/2}^{T_0/2} \cos(k\cdot 2\pi F_0 t) \cdot \cos(l\cdot 2\pi F_0 t) \neq 0$
   <br>
</br>
    <input type="radio" name="question4">
       <label>$k>l$</label><br/>
    <input type="radio"  name="question4">
        <label> $k < l$ </label><br/>
    <input type="radio" id="answer4"  name="question4">
       <label for="answer4">$k=l$</label><br/>
   <input type="radio" name="question4">
      <label>$k\neq l$</label><br/>
 </div>
</div>
<br></br>
<button class="collapsible">Question 5</button>
<div class="content">
<div class="scp-quizzes-data quiz">
  Given the following periodic signal $x(t)$ and considering the fundamental frequency $F_0$, which of the following figures represent the spectral plot?
  $x(t) = 3 + 0.5\cos(7.8\pi t + \frac{\pi}{4}) + 2\sin(130\pi t)$
<br>
</br>
    <input type="radio" name="question5">
       <label>
       <div style="max-width: 600px; margin: auto">
         <figure>
           <img
             src="/../files/7.Images/continuous/transforms/Fourier/quiz/question5a.jpg"
             alt="Spectral plot 5a."
           />
         </figure>
       </div>
       </label><br/>
    <input type="radio" name="question5">
        <label>
        <div style="max-width: 600px; margin: auto">
          <figure>
            <img
              src="/../files/7.Images/continuous/transforms/Fourier/quiz/question5b.jpg"
              alt="Spectral plot 5b."
            />
          </figure>
        </div>
        </label><br/>
    <input type="radio" name="question5">
       <label>
       <div style="max-width: 600px; margin: auto">
         <figure>
           <img
             src="/../files/7.Images/continuous/transforms/Fourier/quiz/question5c.jpg"
             alt="Spectral plot 5c."
           />
         </figure>
       </div>
       </label><br/>
    <input type="radio"  id="answer5" name="question5">
      <label for="answer5">None of the answers is correct.</label><br/>
 </div>
</div>
<br>
</div>
</div>


### Exercise bundle
<object data="/../files/3.Exercises/FourierSeriesExercises.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/3.Exercises/FourierSeriesExercises.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/3.Exercises/FourierSeriesExercises.pdf">Download PDF</a>.</p>
    </embed>
</object>


### Answers
Download the answers <a href="/../files/3.Exercises/Answers/FourierSeriesAnswers.pdf">here</a>.

### Pencast videos [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/videoseries?list=PL2LT3LoI-pPGMYQijO9BDFR3ryItuXb6w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

_The above video player contains a playlist of all pencast videos which can be expanded by clicking the playlist icon in the upper-right corner._

<br></br>

## MATLAB lab
Accompanied to this modules are some exercises in MATLAB, which will test your knowledge of the module and will help improve your MATLAB skills.
These lab exercises also include topics relating to the spectrum of sinusoidal signals.

### Lab assignment
<object data="/../files/10.Matlab/Lab 3 - Fourier Transform.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/10.Matlab/Lab 3 - Fourier Transform.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/10.Matlab/Lab 3 - Fourier Transform.pdf">Download PDF</a>.</p>
    </embed>
</object>

### MATLAB demo [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/UiN1Wom_F5Q" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>

## Summary
<ul>

<li>
A periodic signal has the following property:
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>A real signal $x(t)$, which consists of a DC component and a sum of $N$ different frequencies $f_1, f_2,\ldots, f_N$, with $f_1 &lt f_2 &lt \ldots &lt f_N$, is a periodic signal with Fundamental period $T_0 = 1/F_0$ and has a Fundamental frequency $F_0 = \text{gcd}\{f_1,f_2,\ldots,f_N\} $.</i></div>
</li>

<li>
The integral over one period $T_0 = 1/F_0$ of a phasor with a harmonic related frequency $k \cdot F_0$ results always in zero except for the case $k = 0$.
Mathematically this can be written as follows:

$$\bbox[5px,border:1px solid black]{
\frac{1}{T_0}\int_0^{T_0}e^{j2\pi kF_0 t}\mathrm{d}t =
\begin{cases}
1      &\text{for }k=0\newline
0      &\text{for }k\neq 0
\end{cases}}
$$
</li>

<li>
Fourier analysis and synthesis equations for periodic signal $x(t)=x(t+T_0)$ with $T_0=1/F_0$:
$$\bbox[5px,border:1px solid black]{
\alpha_k = \frac{1}{T_0}\int_0^{T_0} x(t)e^{-j2\pi F_0 kt}\mathrm{d}t
\ \circ  \hspace{-1.7mm} - \hspace{-1.7mm} \circ \
x(t) = \sum_{k=-\infty}^\infty \alpha_k e^{j2\pi F_0 kt }\
}
$$
</li>

</ul>
