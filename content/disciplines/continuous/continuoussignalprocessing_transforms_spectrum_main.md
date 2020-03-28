+++
title = "Spectrum of sinusoidal signals"

# date = {{ .Date }}
lastmod = 2020-03-28

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "Transforms I: Spectrum of sinusoidal signals"
  weight = 41

+++

## Introduction
Many practical signals can be described as a set of sinusoidal signals. In this module we will first show how such a set can be rewritten as a set of weighted phasor components. From this description it follows that these weights represent the spectral information of the signal.


### Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/pQkFbM6gyIA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>
## Module overview
This module covers the following topics:

1. <a href="../continuoussignalprocessing_transforms_spectrum_sum">Real signal as sum of phasors</a> - This section will show that every real signal can be decomposed in the sum of complex phasors.

2. <a href="../continuoussignalprocessing_transforms_spectrum_spectral">Spectral plot</a> - Since a signal can be decomposed in a sum of phasors with different frequencies, it is also possible to represent this graphically in a spectral plot.

3. <a href="../continuoussignalprocessing_transforms_spectrum_product">Product versus sum of sinusoids</a> - Summing sinusoidal signals will simply results in a spectrum composed out of the combined original spectral components. However, the multiplication of two sinusoidal signals (better known as modulation) will have different consequences for the spectrum.

4. <a href="../continuoussignalprocessing_transforms_spectrum_special">Special cases</a> - This module will end with a brief section in which several special spectra are discussed.


<br></br>

## Exercises
In this module several exercises are available, including their answers. The exercises marked in <span style="color:blue">*blue*</span> are explained by means of more extensive pencast videos. These exercises also include topics relating to the Fourier series.


### Video quiz

<div class="example">
  <button class="collapsible">Test your knowledge (click to expand)</button>
  <div class="content">
  <button class="collapsible">Question 1</button>
  <div class="content">
  <div class="scp-quizzes-data quiz">
     Which spectral plot corresponds to the complex signal $z(t) = 2e^{-j(2\pi t - \frac{\pi}{6})}$?
  </br>
      <input type="radio" name="question1">
         <label>
         <div style="max-width: 600px; margin: auto">
           <figure>
             <img
               src="/../files/7.Images/continuous/transforms/Spectrum/quiz/question1a.PNG"
               alt="Spectral plot 1a."
             />
           </figure>
         </div>
         </label><br/>
      <input type="radio" name="question1">
          <label>
          <div style="max-width: 600px; margin: auto">
            <figure>
              <img
                src="/../files/7.Images/continuous/transforms/Spectrum/quiz/question1b.PNG"
                alt="Spectral plot 1b."
              />
            </figure>
          </div>
          </label><br/>
      <input type="radio" id="answer1" name="question1">
         <label for="answer1">
         <div style="max-width: 600px; margin: auto">
           <figure>
             <img
               src="/../files/7.Images/continuous/transforms/Spectrum/quiz/question1c.PNG"
               alt="Spectral plot 1c."
             />
           </figure>
         </div>
         </label><br/>
     <input type="radio"  name="question1">
        <label>
        <div style="max-width: 600px; margin: auto">
          <figure>
            <img
              src="/../files/7.Images/continuous/transforms/Spectrum/quiz/question1d.PNG"
              alt="Spectral plot 1d."
            />
          </figure>
        </div>
        </label><br/>
        <input type="radio"  name="question1">
           <label>None of the answers is correct.</label><br/>
   </div>
   </div>
   <br></br>
  <button class="collapsible">Question 2</button>
  <div class="content">
  <div class="scp-quizzes-data quiz">
     Which spectral plot corresponds to the signal $x(t) = 2 \cos(2\pi\cdot 100t - \frac{\pi}{3})$?
  <br>
  </br>
      <input type="radio" id="answer2" name="question2">
         <label for="answer2">
         <div style="max-width: 600px; margin: auto">
           <figure>
             <img
               src="/../files/7.Images/continuous/transforms/Spectrum/quiz/question2a.PNG"
               alt="Spectral plot 2a."
             />
           </figure>
         </div>
         </label><br/>
      <input type="radio" name="question2">
          <label>
          <div style="max-width: 600px; margin: auto">
            <figure>
              <img
                src="/../files/7.Images/continuous/transforms/Spectrum/quiz/question2b.PNG"
                alt="Spectral plot 2b."
              />
            </figure>
          </div>
          </label><br/>
      <input type="radio"  name="question2">
         <label>
         <div style="max-width: 600px; margin: auto">
           <figure>
             <img
               src="/../files/7.Images/continuous/transforms/Spectrum/quiz/question2c.PNG"
               alt="Spectral plot 2c."
             />
           </figure>
         </div>
         </label><br/>
      <input type="radio" name="question2">
        <label>
        <div style="max-width: 600px; margin: auto">
          <figure>
            <img
              src="/../files/7.Images/continuous/transforms/Spectrum/quiz/question2d.PNG"
              alt="Spectral plot 2d."
            />
          </figure>
        </div>
        </label><br/>
        <input type="radio"  name="question2">
           <label>None of the answers is correct.</label><br/>
   </div>
  </div>
  <br></br>
  <button class="collapsible">Question 3</button>
  <div class="content">
  <div class="scp-quizzes-data quiz">
     Which signal corresponds to the following spectral plot?
     <div style="max-width: 600px; margin: auto">
       <figure>
         <img
           src="/../files/7.Images/continuous/transforms/Spectrum/quiz/question3.PNG"
           alt="Spectral plot 3."
         />
       </figure>
     </div>
  <br>
  </br>
      <input type="radio" name="question3">
        <label>$x(t) = 2\sin(20\pi t - \frac{\pi}{3})$</label><br/>
      <input type="radio" name="question3">
        <label>$x(t) = \cos(20\pi t - \frac{\pi}{3})$</label><br/>
      <input type="radio"  name="question3">
        <label>$x(t) = 2\sin(20\pi t + \frac{\pi}{3})$</label><br/>
      <input type="radio"  name="question3">
        <label>$x(t) = \cos(20\pi t + \frac{\pi}{3})$</label><br/>
      <input type="radio"  id="answer3" name="question3">
        <label for="answer3">None of the answers is correct.</label><br/>
   </div>
  </div>
  <br></br>
  <button class="collapsible">Question 4</button>
  <div class="content">
  <div class="scp-quizzes-data quiz">
      Which signal corresponds to the following spectral plot?
      <div style="max-width: 600px; margin: auto">
        <figure>
          <img
            src="/../files/7.Images/continuous/transforms/Spectrum/quiz/question4.PNG"
            alt="Spectral plot 4."
          />
        </figure>
      </div>
     <br>
  </br>
      <input type="radio" name="question4">
         <label>$x(t) = 2\sin(2\pi t) + 4\cos(4\pi t +\frac{\pi}{4})$</label><br/>
      <input type="radio"  name="question4">
          <label>$x(t) = 2\cos(2\pi t) + 4\cos(4\pi t -\frac{\pi}{4})$</label><br/>
      <input type="radio"  name="question4">
         <label>$x(t) = 2\cos(2\pi t) + 4\cos(4\pi t +\frac{\pi}{4})$</label><br/>
     <input type="radio" id="answer4" name="question4">
        <label for="answer4">$x(t) = 2\sin(2\pi t) + 4\cos(4\pi t -\frac{\pi}{4})$</label><br/>
   </div>
  </div>
  <br></br>
  <button class="collapsible">Question 5</button>
    <div class="content">
    <div class="scp-quizzes-data quiz">
      Consider the spectral plot of an amplitude modulated signal depicted in the figure below. The signal is the porduct of the carrier signal $g(t)$ multiplied with the message signal $s(t)$. The signal $s(t)$ can be written as $s(t) = A_0 + A_1\cos(2\pi f_1 t + \Phi_1)$. Compute the parameters $A_0$, $A_1$, $f_c$, $f_1$ and $\Phi_1$.
      <div style="max-width: 600px; margin: auto">
        <figure>
          <img
            src="/../files/7.Images/continuous/transforms/Spectrum/quiz/question5.png"
            alt="Spectral plot 5."
          />
        </figure>
      </div>
    <br>
    </br>
        <input type="radio" name="question5">
           <label>$A_0 = 1$, $A_1= \frac{1}{4}$, $f_c= 5000$ Hz, $f_1 = 750$ Hz and $\Phi_1=\frac{\pi}{4}$</label><br/>
        <input type="radio" id="answer5" name="question5">
            <label for="answer5">$A_0 = 2$, $A_1= 1$, $f_c= 5000$ Hz, $f_1 = 750$ Hz and $\Phi_1=-\frac{\pi}{4}$</label><br/>
        <input type="radio" name="question5">
           <label>$A_0 = 2$, $A_1= 1$, $f_c= 750$ Hz, $f_1 = 5000$ Hz and $\Phi_1=\frac{\pi}{4}$</label><br/>
        <input type="radio" name="question5">
          <label>None of the answers is correct.</label><br/>
     </div>
    </div>
  <br>
  </div>
</div>

### Exercise bundle
<object data="/../files/3.Exercises/SpectrumExercises.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/3.Exercises/SpectrumExercises.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/3.Exercises/SpectrumExercises.pdf">Download PDF</a>.</p>
    </embed>
</object>


### Answers
Download the answers <a href="/../files/3.Exercises/Answers/SpectrumAnswers.pdf">here</a>.

### Pencast videos [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/videoseries?list=PL2LT3LoI-pPEoL814VlfZ5ZFv1eGh3PGB" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

_The above video player contains a playlist of all pencast videos which can be expanded by clicking the playlist icon in the upper-right corner._

<br></br>
## Summary
<ul>
<li> Sum of DC and $N$ sinusoids written as sum of phasors:
$$
\begin{split}
x(t) &= A_0 + \sum_{k=1}^{N} A_k\cos \left( 2\pi  f_k t+ \phi_k \right),\newline
&= X_0 + \sum_{k=1}^N \bigg\{ \frac{X_k}{2}e^{j2\pi f_k t} + \frac{X_k^\ast}{2}e^{-j2\pi f_k t} \bigg\},
\end{split}
$$

where $X_0 = A_0$ and $X_k = A_ke^{j\phi_k}$.

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>For real signals the values of the complex weights of the phasors with negative frequencies are the complex conjugated versions of the complex weights of the phasors with positive frequencies.</i></div>
</li>

<li>
By ordering the frequencies from low to high we can represent the phasor description in a frequency spectrum plot. In such a plot we denote the frequencies on the horizontal axis. The frequency on this axis can either be denoted by the values of $f_k$ in [Hz] or by the values of $\omega_k = 2\pi f_k$ in [rad/sec]. For each of these frequencies $f_k$ we plot a bar, denoting the complex weights $\frac{X_k}{2}$. These complex weights are related to the magnitude and phase of the original sinusoidal signal.

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>It is easiest to denote the complex numbers of the bars in the spectral plot in Polar notation.</i></div>
</li>

<li>
A product of sinusoids is related to a sum of sinusoids:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>We can write the <b>product</b> of two sinusoidal signals with frequencies $f_c$ and $f_\Delta$ as the <b>sum</b> of two sinusoidal signals with frequencies $f_c-f_\Delta$ and $f_c+f_\Delta$</i></div>
</li>

<li>
An Amplitude Modulated (AM) signal has the following property:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>When a message signal $m(t)$ is modulated by a carrier signal $c(t)$ with frequency $f_c$, the whole spectral content of the message is moved to both the positive and negative frequency component of the carrier signal.</i></div>
</li>
</ul>
