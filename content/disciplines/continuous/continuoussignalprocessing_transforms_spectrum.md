+++
title = "Spectrum of sinusoidal signals"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "Spectrum of sinusoidal signals"
  weight = 41
  parent = "Continuous-time transforms"

+++

Many practical signals can be described as a set of sinusoidal signals. In this section we will first show how such a set can be rewritten as a set of weighted phasor components. From this description it follows that these weights represent the spectral information of the signal.

<br></br>

## Introductory video
<iframe width="100%" height="450" src="https://www.youtube.com/embed/lC1-SNdO8Lo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br></br>

## Real signal as sum of phasors
Let us start with a general description of a signal $x(t)$, which consists of a DC component, with value $A_0$, and a sum of $N$ sinusoidal components, each with a different frequency $f_k$, amplitude $A_k$ and phase $\phi_k$, as

$$
x(t) = A_0 + \sum\_{k=1}^{N} A_k\cos \left( 2\pi  f_k t+ \phi_k \right).
$$

Now by using the <a href="../../mathematicalbackground/mathematicalbackground_complex_euler">Euler equations</a> we can write this equation as the following sum of
rotating <a href="../../mathematicalbackground/mathematicalbackground_complex_phasors">phasors</a>:

$$
\begin{split}
x(t) &= A_0 + \sum\_{k=1}^N \bigg\\{ \left(\frac{A_k}{2}e^{j\phi_k}\right)e^{j2\pi f_k t} + \left(\frac{A_k}{2}e^{-j\phi_k}\right)e^{-j2\pi f_k t}\bigg\\} \newline
&= X_0 + \sum\_{k=1}^N \bigg\\{ \frac{X_k}{2}e^{j2\pi f_k t} + \frac{X_k^\*}{2}e^{-j2\pi f_k t} \bigg\\},
\end{split}
$$

where $X_0 = A_0$ and $X_k = A_ke^{j\phi_k}$. From this description we can derive the following general property:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>For real signals the values of the complex weights of the phasors with negative frequencies are the complex conjugated versions of the complex weights of the phasors with positive frequencies.</i></div>

<br></br>

## Spectral plot
By ordering the frequencies from low to high we can represent the phasor description in a frequency spectrum plot. In such a plot we denote the frequencies on the horizontal axis. The frequency on this axis can either be denoted by the values of $f_k$ in [Hz] or by the values of $\omega_k = 2\pi f_k$ in [rad/sec]. For each of these frequencies $f_k$ we plot a bar, denoting the complex weights $\frac{X_k}{2}$ as described previously. Note that these complex weights are related to the amplitude and phase of the original sinusoidal signal.

<div class="example">
<h4> Example </h4>
<hr>
Find the complex weights of the phasor components of the signal
$$ x(t) = 10 + 14 \cos\left(200\pi t -\frac{\pi}{3}\right) + 8\cos\left(500\pi t + \frac{\pi}{2}\right)$$
and make a spectral plot of the signal.
<button class="collapsible">Show solution</button>
<div class="content">
By using <a href="../../mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> the expression for $x(t)$ can be rewritten as
$$
\begin{split}
x(t)
&= 10 + 14 \cos\left(200\pi t -\frac{\pi}{3}\right) + 8\cos\left(500\pi t + \frac{\pi}{2}\right), \newline
&= 10\cdot 1 + 14\bigg\{ \frac{e^{j\left(200\pi t - \frac{\pi}{3}\right)} + e^{-j\left(200\pi t -\frac{\pi}{3}\right)}}{2}\bigg\} + 8\bigg\{ \frac{e^{j\left(500\pi t + \frac{\pi}{2}\right)} + e^{-j\left(500\pi t -\frac{\pi}{2}\right)}}{2}\bigg\}, \newline
&= \left(10\right) \cdot e^{j2\pi \cdot 0 \cdot t} + \left(7e^{-j\frac{\pi}{3}}\right) \cdot e^{j2\pi \cdot 100 \cdot t} + \left(7e^{j\frac{\pi}{3}}\right) \cdot e^{-j2\pi \cdot 100 \cdot t} \newline
&\qquad + \left(4e^{j\frac{\pi}{2}}\right) \cdot e^{j2\pi \cdot 250 \cdot t} + \left(4e^{-j\frac{\pi}{2}}\right) \cdot e^{-j2\pi \cdot 250 \cdot t}.
\end{split}
$$
From this it can be seen that the signal contains frequency components at the frequencies $f_0 = 0$, $f_1 = 100$, $-f_1 = -100$, $f_2 = 250$ and $-f_2 = -250$ [Hz], where each phasor is multiplied with its own complex weight, indicating the amplitude and phase of that respective phasor. These complex weights are given by
$$
X_0=10, \quad \frac{X_1}{2} = 7e^{-j\frac{\pi}{3}}, \quad  \frac{X_1^\ast}{2} = 7e^{j\frac{\pi}{3}}, \quad \frac{X_2}{2} = 4e^{j\frac{\pi}{2}}, \quad \frac{X_2^\ast}{2} = 4e^{-j\frac{\pi}{2}}.
$$
The spectral plot of the signal $x(t)$ is shown in Fig. 1.
<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/example1_spectrum.svg"
      alt="Spectrum of $x(t)$."
    />
    <figcaption class="numbered">
      Spectrum of $x(t)$.
    </figcaption>
  </figure>
</div>  
</div>
</div>

In a spectral plot, such as the one from the previous example, the phasor components of the signal are represented by bars and the corresponding weights are denoted by complex numbers above these bars. The amplitude or magnitude of the complex weights corresponds to the length of the bar. When denoting these complex weights in <a href="../../mathematicalbackground/mathematicalbackground_complex_notation">Polar notation</a> it becomes very easy to 'read from the spectral plot' and to convert the spectral plot back to the time-domain representation of the real signal $x(t)$.

From the spectral plot of the above example it can be noted that the spectrum is symmetric, indicating that we are dealing with a real signal. The spectrum consists of a DC term and two sinusoids. The DC term has a value of 10 and is by definition located at a frequency of $0$ [Hz]. The first sinusoid is located at $100$ [Hz] and has an amplitude of $2\times7 = 14$ and has a phase of $-\frac{\pi}{3}$, which is obtained from the right-hand side of the spectrum. The second sinusoid has an amplitude of $2\times4=8$ and has a phase of $\frac{\pi}{2}$. Keep in mind to read the phase of the sinusoid from the right-hand side of the spectrum, since the left-hand side contains the negated phase.
All together the spectral plot of the above example belongs to the following time-domain representation of signal $x(t)$:
$$ x(t) = 10 + 14 \cos\left(200\pi t -\frac{\pi}{3}\right) + 8\cos\left(500\pi t + \frac{\pi}{2}\right).$$

From the above interpretation of the spectral plot we can conclude

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>It is easiest to denote the complex weights corresponding to the individual phasor components in the spectral plot in Polar notation.</i></div>

<br></br>


## Product versus sum of frequencies
In the previous section we have seen that a spectral plot represents the spectral content of a signal. When a signal consists of a sum of sinusoids we have seen which spectral components belongs to which sinusoid. But what is the frequency content of a signal which consists of a multiplication of sinusoids? In practice this multiplication is commonly used when we apply ”Amplitude Modulation” (AM) to transmit a baseband signal, with relative low frequency content, over a long distance. In such a case the baseband signal is multiplied with a carrier signal which has a relative high carrier frequency $f_c$ [Hz].
So lets start our discussion by assuming that a signal $x(t)$ consists of the multiplication of two sinusoids, one with carrier frequency $f_c$ and the other with (baseband or message) frequency $f\_{\Delta}$ (typically with $f_c >> f\_{\Delta}$, i.e. the carrier frequency is way larger than the baseband frequency), as
$$ x(t) = 2\cos(2\pi f_c t) \cdot \cos(2\pi f\_\Delta t). $$

By using <a href="../../mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> we can rewrite this equation as

$$
\begin{split}
x(t)
&= 2\left(\frac{1}{2}e^{j2\pi f_c t}+ \frac{1}{2}e^{-j2\pi f_c t}\right) \cdot \left(\frac{1}{2}e^{j2\pi f\_\Delta t}+ \frac{1}{2}e^{-j2\pi f\_\Delta t}\right), \newline
&= \frac{1}{2} e^{j2\pi(f_c+f\_\Delta)t} + \frac{1}{2} e^{j2\pi(f_c-f\_\Delta)t} +\frac{1}{2} e^{-j2\pi(f_c-f\_\Delta)t} + \frac{1}{2} e^{-j2\pi(f_c+f\_\Delta)t}, \newline
&= \left(\frac{e^{j2\pi(f_c+f\_\Delta)t} + e^{-j2\pi(f_c+f\_\Delta)t}}{2}\right) + \left(\frac{e^{j2\pi(f_c-f\_\Delta)t} + e^{-j2\pi(f_c-f\_\Delta)t}}{2}\right), \newline
&= \cos(2\pi(f_c+f\_\Delta)t) + \cos(2\pi(f_c-f\_\Delta)t).
\end{split}
$$

From this expression we can conclude that

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The product of two sinusoidal signals with frequencies $f_c$ and $f_\Delta$ can be written as the sum of two sinusoidal signals with frequencies $f_c + f_\Delta$ and $f_c - f_\Delta$.</i></div>

Fig. 1 shows an example of what this multiplication now actually looks like in the time-domain. From the definition of $x(t)$ it can be understood as a sinusoid at a high carrier frequency, whose amplitude is slowly changing according to a baseband signal. In this case there is chosen for a carrier frequency $f_c$ of $200$ [Hz] and a baseband frequency $f\_\Delta$ of $20$ [Hz]. Fig. 2 shows what the new spectral plot of $x(t)$ looks like.

<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/modulation_time.svg"
      alt="Time-domain representation of modulated signal $x(t)$."
    />
    <figcaption class="numbered">
      Time-domain representation of modulated signal $x(t)$.
    </figcaption>
  </figure>
</div>

<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/modulation_spectrum.svg"
      alt="Spectrum of modulated signal $x(t)$."
    />
    <figcaption class="numbered">
      Spectrum of modulated signal $x(t)$.
    </figcaption>
  </figure>
</div>

One of the examples where we use this concept is when tuning a guitar or piano. With the previous example in mind: Assume a guitar string produces a, wrongly tuned, 180 [Hz] signal and we want it to be tuned at 220 [Hz]. Then by playing an external signal generator, which produces a 220 [Hz] pure tone, while playing the, wrongly tuned, 180 [Hz] guitar string, we will not hear a clear sound. The waveform of the sound (as a product) is shown in Fig. 1: The amplitude of the sound is not constant but it changes. This effect is called ”beat note”. Now we can tune the string by tightening it until the amplitude does not change anymore and we will hear one pure tone of 220 [Hz]. At that point our guitar string is tuned to 220 [Hz]. Another application of the previous concept is when transmitting a baseband signal, with relative low frequency content, over a long distance. An example of such a baseband signal is audio, e.g. speech or music, which has frequencies up to 20 [kHz]. It is impossible to transmit such an audio signal over a long distance in the air, because of attenuation. In such a case we can apply ”Amplitude modulation”: The baseband signal is multiplied with a carrier signal which has a relative high frequency $f_c$ [Hz] and the audio is then transmitted in the band around the less attenuating carrier frequency.

<div class="example">
<h4> Example </h4>
<hr>
Assume the baseband (message) signal $m(t)=4+2\cos(2\pi 6t-\frac{\pi}{4})$ is multiplied (modulated) with the carrier signal $c(t) = \cos(2\pi 1000t)$ to produce the Amplitude Modulated (AM) signal $x(t)=c(t)\cdot m(t)$. Determine the spectral plots of all three signals.
<button class="collapsible">Show solution</button>
<div class="content">
In order to create a spectral plot we first need to find the frequency components of all three signals. To do so, the signals are converted into <a href="../continuoussignalprocessing_transforms_fs/#real-signal-as-sum-of-phasors">phasor</a> notation. The message signal $m(t)$ can be written as
$$
\begin{split}
m(t)
&=4+2\cos(2\pi 6t-\frac{\pi}{4}),\newline
&= \left(4\right)e^{j2\pi 0 t} + \left(1e^{-j\frac{\pi}{4}}\right)e^{j2\pi 6 t} + \left(1e^{j\frac{\pi}{4}}\right)e^{-j2\pi 6 t}.
\end{split}$$
The carrier signal $c(t)$ can be written as
$$
\begin{split}
c(t)
&= \cos(2\pi 1000t), \newline
&= \left(\frac{1}{2}\right)e^{j2\pi 1000 t} + \left(\frac{1}{2}\right)e^{-j2\pi 1000 t}.
\end{split}
$$
Both these signals can already be represented in their spectral plots. In order to also be able to represent $x(t)$ in a spectral plot the signal also needs to be rewritten in <a href="../continuoussignalprocessing_transforms_fs/#real-signal-as-sum-of-phasors">phasor</a> notation as
$$
\begin{split}
x(t)
&= c(t)\cdot m(t), \newline
&= \bigg\{ \frac{1}{2}e^{j2\pi 1000 t} + \frac{1}{2}e^{-j2\pi 1000 t} \bigg\} \cdot \bigg\{ 4e^{j2\pi 0 t} + e^{-j\frac{\pi}{4}}e^{j2\pi 6 t} + e^{j\frac{\pi}{4}}e^{-j2\pi 6 t} \bigg\}, \newline
&= 2e^{j2\pi 1000 t} + \frac{1}{2}e^{-j\frac{\pi}{4}}e^{j2\pi (1000+6) t} + \frac{1}{2} e^{j\frac{\pi}{4}}e^{j2\pi (1000-6) t} \newline
&\qquad + 2e^{-j2\pi 1000 t} + \frac{1}{2}e^{-j\frac{\pi}{4}}e^{-j2\pi (1000-6) t} + \frac{1}{2} e^{j\frac{\pi}{4}}e^{-j2\pi (1000+6) t}.
\end{split}
$$
The spectral plots are shown in Fig. 3. From the spectral plots it follows that the whole spectral content of the message signal $m(t)$ has been 'shifted' (modulated) to the positive and negative carrier frequency components of the carrier signal $c(t)$.
<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/example2_spectrum.svg"
      alt="Spectrum of message signal $m(t)$, carrier signal $c(t)$ and modulated signal $x(t)$."
    />
    <figcaption class="numbered">
      Spectrum of message signal $m(t)$, carrier signal $c(t)$ and modulated signal $x(t)$.
    </figcaption>
  </figure>
</div>
</div>
</div>

From the previous example we may conclude that

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>When a message signal $m(t)$ is modulated by a carrier signal $c(t)$ with frequency $f_c$, the whole spectral content of the message is moved to both the positive and negative frequency component of the carrier signal.</i></div>

<br></br>


## Special cases
<iframe width="100%" height="450" src="https://www.youtube.com/embed/3XA-zK1XpQM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br></br>


## Exercises
In this section several exercises are available, including their answers. The exercises marked in <span style="color:blue">*blue*</span> are explained by means of more extensive pencast videos. These exercises also include topics relating to the Fourier series.


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
<object data="/../files/3.Exercises/2.SPAFS-exercises.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/3.Exercises/2.SPAFS-exercises.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/3.Exercises/2.SPAFS-exercises.pdf">Download PDF</a>.</p>
    </embed>
</object>


### Answers
Download the answers <a href="/../files/3.Exercises/Answers/2.SPAFS-answers.pdf">here</a>.

### Pencast videos
<iframe width="100%" height="450" src="https://www.youtube.com/embed/videoseries?list=PL2LT3LoI-pPGn3EuYqCpSPZ8TL5HRFNXs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

_The above video player contains a playlist of all pencast videos which can be expanded by clicking the playlist icon in the upper-right corner._

<br></br>

## MATLAB lab
Accompanied to this modules are some exercises in MATLAB, which will test your knowledge of the module and will help improve your MATLAB skills.
These lab exercises also include topics relating to the Fourier series.

### Lab assignment
<object data="/../files/10.Matlab/Lab 3 - Fourier Transform.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/10.Matlab/Lab 3 - Fourier Transform.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/10.Matlab/Lab 3 - Fourier Transform.pdf">Download PDF</a>.</p>
    </embed>
</object>

### MATLAB demo
<iframe width="100%" height="450" src="https://www.youtube.com/embed/UiN1Wom_F5Q" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

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
