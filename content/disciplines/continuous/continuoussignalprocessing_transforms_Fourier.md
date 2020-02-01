+++
title = "Fourier series"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "Fourier series"
  weight = 42
  parent = "Continuous-time transforms"

+++

In the <a href="../continuoussignalprocessing_transforms_spectrum">previous module</a> we studied the spectral behavior of the sum of sinusoidal signals. In this section we will study signals which are composed of a sum of harmonic related sine waves.

<br></br>

## Introductory video
<iframe width="100%" height="450" src="https://www.youtube.com/embed/8XKqEFoVY1I" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br></br>

## Periodic signals
In this subsection we will show that any periodic signal with a, so called, Fundamental period $T_0$ can be composed as the sum of sinusoidal signals from which each of these frequencies is related to the, so called, Fundamental frequency $F_0 = 1/T_0$ as an integer multiple. In order to show this Fig. 1 depicts a signal $y_2(t)$ which is composed of the sum of two sinusoidal signals $x_1(t)$ of frequency $f_1 = 6$ [Hz] and $x_2(t)$ of frequency $f_2 = 2$ [Hz]. From this figure it follows that $y_2(t)$ is periodic and we can measure that the period equals $T_0 = 1/F_0 = 0.5$ [sec]. The reason for this periodicity of signal $y_2(t)$ is that exactly three periods of $x_1(t)$ and one period of $x_2(t)$ fit into one period $T_0$ of signal $y_2(t)$. Thus after each $T_0 = 0.5$ [sec] the same composition of the signals $x_1(t)$ and $x_2(t)$ appears in the signal $y_2(t)$.

<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/fundamental_frequency.svg"
      alt="Signals of various frequencies with there cumulative signals."
    />
    <figcaption class="numbered">
      Signals of various frequencies with there cumulative signals.
    </figcaption>
  </figure>
</div>

The figure also shows another signal $y_3(t)$ which is composed of the sum three sinusoidal signals. The same sinusoidal signals $x_1(t)$, $x_2(t)$ and a new sinusoidal signal $x_3(t)$, with frequency $f_3 = 1.2$ [Hz]. Again it follows from the figure that $y_3(t)$ is periodic but now we can measure that the period equals $T_0 = 1/F_0 = 2.5$ [sec]. This is because of the fact that exactly fifteen periods of $x_1(t)$, five periods of $x_2(t)$ and three periods of $x_3(t)$ fit into one period $T_0$ of signal $y_3(t)$. Mathematically we can calculate $F_0 = 1/T_0$ of $y_3(t)$ as the Greatest Common Divisor (gcd) of the frequencies from the individual sinusoidal components, since $F_0 = \text{gcd}\\{f_1, f_2, f_3\\} = \text{gcd}\\{6, 2, 1.2\\} = 0.4$ [Hz]. The greatest common divisor of a set of numbers is the largest number that all numbers of that set can be _fully_ divided by. From this it follows that the Fundamental period of $y_3(t)$ equals $T_0 = 1/F_0 = 2.5$ [sec]. This leads to the following general statement:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>A real signal $x(t)$, which consists of a DC component and a sum of $N$ different frequencies $f_1, f_2,\ldots, f_N$, with $f_1 &lt f_2 &lt \ldots &lt f_N$, is a periodic signal with Fundamental period $T_0 = 1/F_0$ and has a Fundamental frequency $F_0 = \text{gcd}\{f_1,f_2,\ldots,f_N\} $.</i></div>

In the case that this general statement is true, all $N$ different frequencies of signal $x(t)$ are related by an integer number times the Fundamental frequency $F\_0$. Thus we can define the largest frequency by $f\_N = M\cdot F\_0$ with integer $M \geq N$. With this definition we can write such a periodic signal $x_(t)$ as a weighted sum of phasor components as
$$
x(t) = \sum\_{k=-M}^{M} \alpha_k e^{j2\pi kF_0 t},
$$
in which the complex weights $\alpha_k$ represent the amplitude and phase of the frequency components at frequency $k \cdot F_0$. Finally note that possible $\alpha_0$ and definitely only $N$ out of $M$ complex weights $\alpha_k$ are not equal to zero.


<div class="example">
<h4> Example </h4>
$$
x(t) = 2+2\cos\left(102\pi t-\frac{\pi}{8}\right) - \sin\left(238\pi t +\frac{\pi}{3}\right) + 3\cos\left(340\pi t+\frac{\pi}{2}\right)
$$
Determine if the above signal is periodic and if so calculate the Fundamental frequency $F_0=1/T_0$ and give the general expression for $x(t)$ as in the above equation and make a spectral plot of $x(t)$.
<button class="collapsible">Show solution</button>
<div class="content">
The signal consists out of a DC component and a sum of 3 sinusoids with frequencies $f_1=51$, $f_2=119$ and $f_3=170$ [Hz]. The Fundamental frequency can be determined as $F_0 = \text{gcd}\{ 51, 119, 170\} = 17$ [Hz]. Therefore $x(t)$ is a periodic signal with Fundamental period $T_0=1/F_0=1/17$ [sec]. The relationships between the three frequencies and the Fundamental frequencies are $f_1=51=3\cdot F_0$, $f_2=119=7\cdot F_0$ and $f_3=170=10\cdot F_0$ [Hz].
The highest frequency contains $10$ times the Fundamental frequency and therefore $x(t)$ can be written as
$$
x(t) = \sum_{k=-10}^{10} \alpha_k e^{j2\pi kF_0 t}.
$$
By using <a href="../../../disciplines/mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> we can write $x(t)$ as
$$
\begin{split}
x(t)
&= \frac{3}{2}e^{-j\frac{\pi}{2}}e^{-j2\pi 170t} + \frac{1}{2j}e^{-j\frac{\pi}{3}}e^{-j2\pi 119t} + e^{j\frac{\pi}{8}}e^{-j2\pi 51t} + 2 \newline
&\qquad + e^{-j\frac{\pi}{8}}e^{j2\pi 51t} + \frac{-1}{2j}e^{j\frac{\pi}{3}}e^{j2\pi 119t}  + \frac{3}{2}e^{j\frac{\pi}{2}}e^{j2\pi 170t}.
\end{split}
$$
When comparing the above two equations, the values of $\alpha_k$ can be determined as
$$
\alpha_k =
\begin{cases}
\frac{3}{2}e^{j\frac{\pi}{2}},        &\text{for }k=10\\
\frac{-1}{2j}e^{j\frac{\pi}{3}},      &\text{for }k=7\\
e^{-j\frac{\pi}{8}},                &\text{for }k=3\\
2,      &\text{for }k=0\\
e^{j\frac{\pi}{8}}=\alpha_3^\ast,   &\text{for }k=-3\\
\frac{1}{2j}e^{-j\frac{\pi}{3}}= \alpha_7^\ast,         &\text{for }k=-7\\
\frac{3}{2}e^{-j\frac{\pi}{2}} =\alpha_{10}^\ast,        &\text{for }k=-10\\
0.      &\text{otherwise}
\end{cases}
$$
The spectral plot of $x(t)$ is given in Fig. 2. The x-axis contains both the frequency as the integer values of $k$, which are the frequency divided by the Fundamental frequency.
<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/example3_spectrum.svg"
      alt="Spectral plot of the given function $x(t)$."
    />
    <figcaption class="numbered">
      Spectral plot of the given function $x(t)$.
    </figcaption>
  </figure>
</div>
</div>
</div>

<br></br>

## Fourier series synthesis
In the previous subsection we have seen that every periodic signal $x(t)$, with Fundamental period $T_0 = 1/F_0$, can be written as a sum of weighted harmonic related phasor components. In theory the summation can contain an infinite amount of components which leads to the following Fourier series expansion:

$$\bbox[5px,border:1px solid black]{
x(t) = \sum_{k=-\infty}^{\infty} \alpha_k e^{j2\pi kF_0 t}.}
$$

Thus when the spectral weights, which are represented by the complex numbers $\alpha_k$, are known we can construct (synthesize) the periodic signal $x(t)$ according the above general expression.

### Fourier series analysis
In this subsection we will show the other way around: when we are given the waveform in the time-domain of a periodic signal $x(t)$, how can we derive the spectral weights $\alpha_k$? In order to do so we need the following basic property of a phasor function:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The integral over one period $T_0=1/F_0$ of a phasor with a harmonic related frequency $k \cdot F_0$ results always in zero except for the case $k=0$.</i></div>

Mathematically this can be shown as follows:
$$
\int_0^{T_0} e^{j2\pi k F_0 t} \mathrm{d}t = \left[\frac{e^{j2\pi kF_0 t}}{j2\pi F_0 k}\right]\_{t=0}^{T_0} = \frac{e^{j2\pi k}-1}{j2\pi F_0 k} = \frac{1-1}{j2\pi F_0 k} = 0.
$$
Furthermore the integral can be evaluated for $k=0$ as
$$
\int_0^{T_0} e^{j2\pi 0 F_0 t}\mathrm{d}t = \int_0^{T_0}1\mathrm{d}t = \left[t\right]\_0^{T_0} = T_0-0 = T_0.
$$
What do the above two equation now actually mean? If we integrate a sinusoidal signal over a number of periods, we are actually summing the areas under the sinusoid. Since the sinusoid has an equal area under as above the horizontal axis per period, the area will sum to zero. However, if $k=0$, which means that we are talking about a DC signal, the signal does not oscillate around the horizontal axis and therefore the integral will not become zero.

When we normalize and combine the previous two equations we obtain the basic property of phasors

$$\bbox[5px,border:1px solid black]{
\frac{1}{T_0}\int_0^{T_0}e^{j2\pi kF_0 t}\mathrm{d}t =
\begin{cases}
1,      &\text{for }k=0\newline
0.      &\text{for }k\neq 0
\end{cases}}
$$

Since we are sure that a periodic signal $x(t)$, with Fundamental period $T_0 = 1/F_0$, only consists of harmonic related frequencies we can use the above phasor property as follows to analyze which harmonic related frequencies are present in $x(t)$ and what are the complex values of the spectral weights. For this we evaluate the normalized integral over one period $T_0$ of $x(t)$ multiplied by a phasor with harmonic related frequency $l \cdot F_0$. Thus with both $k$ and $l$ integer we obtain

$$
\begin{split}
\frac{1}{T_0}\int_0^{T_0}x(t)e^{-j2\pi lF_0 t}\mathrm{d}t
&= \frac{1}{T_0}\int_0^{T_0}\left(\sum\_{k=-\infty}^{\infty} \alpha_k e^{j2\pi kF_0 t}\right)e^{-j2\pi lF_0 t}\mathrm{d}t, \newline
&= \sum\_{k=-\infty}^{\infty} \alpha_k \left(\frac{1}{T_0} \int_0^{T_0} e^{j2\pi(k-l)F_0 t}\mathrm{d}t \right),
&= \alpha_l.
\end{split}
$$

In the last step we have used the phasor property to observe that the integral only becomes non-zero when $k=l$.

Thus when we are given a periodic signal $x(t)$ with period $T_0 = 1/F_0$ then we can find the spectral components $a_k$ by using the following Fourier series analysis equation
$$\bbox[5px,border:1px solid black]{
\alpha_k = \frac{1}{T_0}\int_0^{T_0}x(t)e^{-j2\pi kF_0t}\mathrm{d}t}.
$$

In practical application it is impossible to evaluate $\alpha_k$ for $-\infty<k<\infty$. Therefore we can approximate a period signal $x(t)$ with only a limited amount of terms as

$$
\hat{x}(t) = \sum_{k=-N}^{N} \alpha_k e^{j2\pi kF_0 t}.
$$
It is obvious that the approximation becomes better and better for larger $N$.

<div class="example">
<h4> Example </h4>
Given the following periodic signal $x(t)$, evaluate the spectral weights $\alpha_k$. Furthermore, show the approximated periodic signal $x(t)$ when using only up to the first 5 terms.
  <figure style="max-width: 600px; margin: auto">
    <img
      src="/../files/7.Images/continuous/transforms/block_ideal.svg"
      alt="Ideal periodic block wave."
    />
    <figcaption>
      Ideal periodic block wave $x(t)$.
    </figcaption>
  </figure>
<button class="collapsible">Show solution</button>
<div class="content">
From the figure it follows that $x(t)$ is a periodic signal with period $T_0=1/F_0=4$ [sec]. In most cases it is convenient to evaluate first the DC component $\alpha_0$ of the periodic signal (which can be regarded as just the average value of the signal). The DC component can be calculated simply by averaging as
$$
\alpha_0 = \frac{1}{T_0}\int_0^{T_0} x(t)\mathrm{d}t = \frac{1}{4} \bigg\{ \int_0^2 2\mathrm{d}t + \int_2^4 0\mathrm{d}t\bigg\} = \frac{1}{4}\{ 4+0\} = 1.
$$
Furthermore with $\omega_0=2\pi F_0 = \frac{2\pi}{4} = \frac{\pi}{2}$, we obtain for $\alpha_k$
$$
\begin{split}
\alpha_k
&= \frac{1}{T_0}\int_0^{T_0}x(t)e^{-j\omega_0 kt}\mathrm{d}t
= \frac{1}{4}\int_0^{2}2e^{-j\omega_0 kt}\mathrm{d}t
= \frac{1}{4} \left[ \frac{2e^{-j\omega_0 kt}}{-j\omega_0 k}\right]\_0^2, \newline
&= \frac{j}{2\omega_0 k}\left(e^{-j2\omega_0 k}-1\right)
= \frac{j}{k\pi}(e^{-j\pi k}-1) = \frac{\left(e^{-j\pi}\right)^k -1}{k\pi}j
= \frac{(-1)^k -1}{k\pi}e^{j\frac{\pi}{2}}, \newline
&= \frac{1-(-1)^k}{k\pi}e^{-j\frac{\pi}{2}}.
\end{split}
$$
Thus except for $k=0$ all Fourier coefficients with even index $k$ are equal to zero. The Fourier coefficients with odd indices are:
$$
\alpha_1 = \alpha_{-1}^\ast = \frac{2}{\pi}e^{-j\frac{\pi}{2}},
\quad \alpha_3 = \alpha_{-3}^\ast = \frac{2}{3\pi}e^{-j\frac{\pi}{2}},
\quad \alpha_5 = \alpha_{-5}^\ast = \frac{2}{5\pi}e^{-j\frac{\pi}{2}},
\quad \text{etc.}
$$
When approximating this periodic signal with the first $N$ terms we obtain
$$
\begin{split}
\hat{x}(t)
&= \alpha_0 + \sum_{k=1}^N \left(\alpha_k e^{jk\frac{\pi}{2} t} +\alpha_{-k} e^{-jk\frac{\pi}{2} t} \right), \newline
&= 1 + \frac{4}{k\pi}\sum_{k=1,3,5,\ldots}^N \cos\left(k\frac{\pi}{2}t - \frac{\pi}{2}\right), \newline
&= 1 + \frac{4}{k\pi}\sum_{k=1,3,5,\ldots}^N \sin\left(k\frac{\pi}{2}t\right).
\end{split}
$$
The figure below gives the approximation of the block wave for an increased number of Fourier coefficients, where $k$ is limited between $-N$ and $N$.
<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/block_approximate.gif"
      alt="Approximation of an ideal block wave."
    />
    <figcaption>
      Approximation of an ideal block wave, where the $k$ is limited between $-N$ and $N$. The value of $N$ is altered during the animation.
    </figcaption>
  </figure>
</div>
</div>
</div>

<br></br>

## Fourier series examples
The above example should give you some intuition on how the Fourier series works. For a better clarification of the subject matter the following screencast video will give some more examples

<iframe width="100%" height="450" src="https://www.youtube.com/embed/DETTPI_R0SY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

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
Download the answers <a href="/../files/3.Exercises/Answers/2.SPAFS-answers.pdf">here</a>.

### Pencast videos
<iframe width="100%" height="450" src="https://www.youtube.com/embed/videoseries?list=PL2LT3LoI-pPGMYQijO9BDFR3ryItuXb6w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

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

### MATLAB demo
<iframe width="100%" height="450" src="https://www.youtube.com/embed/UiN1Wom_F5Q" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

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
