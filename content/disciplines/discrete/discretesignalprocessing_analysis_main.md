+++
title = "Transform analysis of discrete-time systems"

# date = {{ .Date }}
lastmod = 2019-10-13

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Transform analysis of discrete-time systems"
  weight = 60


+++



## Module overview
This module will analyze discrete-time filters not only in the time-domain, but also in other domains, such as the frequency domain.

1. <a href="../discretesignalprocessing_analysis_frequency/">Frequency response of finite impulse response filters</a> - The most basic filter is defined as a finite impulse response filter. This section discusses the behaviour of the filter in the frequency domain.
2. <a href="../discretesignalprocessing_analysis_lti/">Frequency response of LTI systems</a> (in progress) - The frequency response can be extended to infinite impulse response filters, where other aspects are also of importance, such as stability.
3. **System functions** (to be added) - The difference equation can easily be converted to a system function through the z-transform, which offers us with valuable insight of the operations of the filter.

## Exercises
In this section several exercises are available, including their answers. The exercises marked in <span style="color:blue">*blue*</span> are explained by means of more extensive pencast videos.

### Video quiz

<div class="example">
<button class="collapsible">Test your knowledge (click to expand)</button>
<div class="content">

<button class="collapsible">Question 1</button>
<div class="content">

<div class="scp-quizzes-data quiz">
   The input signal is $x[n] = \cos(0.5\pi n)$. This signal is applied to a filter with impulse response $h[n]$ and frequency response $H(e^{j\theta}) = 2\sin(\theta)$. Give a description of the output signal $y[n]$.
</br>
    <input type="radio" name="question1">
       <label>$y[n] = 0$</label><br/>
    <input type="radio" name="question1">
        <label>$y[n] = 2$</label><br/>
    <input type="radio"  id="answer1" name="question1">
        <label for="answer1">$y[n] = 2\cos(0.5\pi n)$</label><br/>
    <input type="radio"  name="question1">       
        <label>$y[n] = 2\cos(0.5\pi n + 0.5\pi)$</label><br/>
    <input type="radio"  name="question1">
        <label>None of the answers is correct.</label><br/>
 </div>
 </div>
 <br>


<button class="collapsible">Question 2</button>
<div class="content">
<div class="scp-quizzes-data quiz">

    Have a look at the following system: <br>
    <div style="max-width: 600px; margin: auto">
      <figure>
        <img
          src="/../files/7.Images/discrete/analysis/FIR/quiz/question2.PNG"
          alt="FIR filter, question 2."
        />
      </figure>
    </div>
    Signal $x[n]$ consists out of two frequencies $\theta_1 = \frac{\pi}{3}$ and $\theta_2=\pi$. Which frequencies does the output signal $y[n]$ contain?  
<br>
</br>
    <input type="radio" name="question2">
      <label>Both frequencies remain.</label><br/>
    <input type="radio" name="question2">
      <label>Both frequencies get cancelled out.</label><br/>
    <input type="radio" id="answer2" name="question2">
      <label for="answer2">Only $\theta=\frac{\pi}{3}$ remains.</label><br/>    
    <input type="radio"  name="question2">
      <label>Only $\theta=\pi$ remains.</label><br/>
    <input type="radio" name="question2">
      <label>None of the answers is correct.</label><br/>
 </div>
</div>
<br>

<button class="collapsible">Question 3</button>
<div class="content">

<div class="scp-quizzes-data quiz">
    What is the response of the following filter to a DC signal?
    <div style="max-width: 600px; margin: auto">
      <figure>
        <img
          src="/../files/7.Images/discrete/analysis/FIR/quiz/question3.PNG"
          alt="FIR filter, question 3."
        />
      </figure>
    </div>
<br>
</br>
    <input type="radio"  name="question3">
      <label>The DC signal remains the unchanged.</label><br/>
    <input type="radio" id="answer3"  name="question3">
      <label for="answer3">The DC signal gets filtered out.</label><br/>
    <input type="radio"  name="question3">
      <label>The DC signal gets doubled.</label><br/>
 </div>
</div>
<br>


<button class="collapsible">Question 4</button>
<div class="content">

<div class="scp-quizzes-data quiz">
    What is the response of the following cascaded filters to a DC signal?
    <div style="max-width: 600px; margin: auto">
      <figure>
        <img
          src="/../files/7.Images/discrete/analysis/FIR/quiz/question4.PNG"
          alt="cascaded FIR filter, question 4."
        />
      </figure>
    </div>
<br>
</br>
<input type="radio"  name="question4">
  <label>The DC signal remains the unchanged.</label><br/>
<input type="radio" id="answer4"  name="question4">
  <label for="answer4">The DC signal gets filtered out.</label><br/>
<input type="radio"  name="question4">
  <label>The DC signal gets doubled.</label><br/>
  <input type="radio"  name="question4">
    <label>The DC signal gets tripled.</label><br/>
 </div>
</div>
<br>

<button class="collapsible">Question 5</button>
<div class="content">

<div class="scp-quizzes-data quiz">
    What is does the system with the following phase response represent?
    <div style="max-width: 600px; margin: auto">
      <figure>
        <img
          src="/../files/7.Images/discrete/analysis/FIR/quiz/question5.PNG"
          alt="Phase response, question 5."
        />
      </figure>
    </div>
<br>
</br>
    <input type="radio" name="question5">
       <label>Delay by 2/3 samples.</label><br/>
    <input type="radio"  name="question5">
        <label>Delay by 2 samples.</label><br/>
    <input type="radio"  id="answer5" name="question5">
       <label for="answer5">Delay by 3 samples.</label><br/>
   <input type="radio"  name="question5">
      <label>Saw tooth</label><br/>
   <input type="radio" name="question5">
      <label>None of the answers is correct.</label><br/>
 </div>
</div>
<br>


</div>
</div>


### Exercise bundle

<object data="/../files/3.Exercises/5.FREQ-exercises.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/3.Exercises/5.FREQ-exercises.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/3.Exercises/5.FREQ-exercises.pdf">Download PDF</a>.</p>
    </embed>
</object>

### Answers
Download the answers <a href="/../files/3.Exercises/Answers/5.FREQ-answers.pdf">here</a>.

### Pencast videos
<iframe width="100%" height="450" src="https://www.youtube.com/embed/videoseries?list=PL2LT3LoI-pPHIiIx4l49DwPs8v4f0wptO" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

_The above video player contains a playlist of all pencast videos which can be expanded by clicking the playlist icon in the upper-right corner._

## MATLAB lab
Accompanied to this modules are some exercises in MATLAB, which will test your knowledge of the module and will help improve your MATLAB skills.

### Lab assignment
<object data="/../files/10.Matlab/Lab 6 - Frequency Response.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/10.Matlab/Lab 6 - Frequency Response.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/10.Matlab/Lab 6 - Frequency Response.pdf">Download PDF</a>.</p>
    </embed>
</object>

### MATLAB demo
<iframe width="100%" height="450" src="https://www.youtube.com/embed/7oas6xLIYhc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Summary frequency response of FIR filters

<b><u> Relationship impulse response and frequency response:</u></b>
$$
\boxed{
\begin{eqnarray}
\text{Time domain} & \circ  \hspace{-2.3mm} - \hspace{-1.1mm}  \circ & \text{Frequency domain} \newline
h[n]= \sum\_{k=0}^{M-1} h[k] \delta[n-k] & \circ  \hspace{-2.3mm} - \hspace{-1.1mm}  \circ &
H(e^{j{\theta}})= \sum\_{k=0}^{M-1} h[k] e^{-j{\theta k}}   
\end{eqnarray}
}
$$

<br>
<b><u> Basic FIR property: </u></b>
<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>When applying a sinusoidal signal with a single frequency $\theta=\theta_1$ to an FIR filter, the output is a sinusoidal signal with the same frequency $\theta_1$ as the input signal, only the amplitude and phase have changed. The change in amplitude is described by the magnitude response evaluated at frequency $\theta_1$, thus $|H(e^{j{\theta}})|\_{\theta=\theta_1}$, while the change in phase is described by the phase response evaluated at frequency $\theta_1$, thus $\angle{H(e^{j{\theta}})}|\_{\theta=\theta_1}$.</i></div>

<br>
When applying a sum of frequencies $x[n] = A_0 + \sum\_{k=1}^{N} A_k \cos ( \theta_k n + \phi_k)$ to an FIR filter with frequency response $H(e^{j{\theta}}) = |H(e^{j\theta})| e^{j{\angle{H(e^{j{\theta}})}}}$ then the output can be written as follows:
$$
y[n] = |H(e^{j0})| + \sum\_{k=1}^{N} |H(e^{j\theta_k})| A_k \cos (\theta_k n + \phi_k +
\angle{H(e^{j\theta_k})})
$$


<br>
<b><u> Properties frequency response </u></b>
$$
\boxed{
\begin{eqnarray}
\text{Periodic } & : & H(e^{j\theta})  =  H(e^{j(\theta + l \cdot 2 \pi)}) \newline
\text{Complex conjugated } & : & H(e^{-j\theta})  = (H(e^{j\theta}))^\ast
\end{eqnarray}
}
$$

<br>
<b><u> Graphical representation: </u></b>
<br>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i><ul><li>Both Magnitude- and phase- response are depicted in the Fundamental Interval (FI): $|\theta| \leq \pi$.</li><li>The phase response is depicted in the range $|\angle{H(e^{j\theta})}| \leq \pi$.</li><li>A phase jump of $\pm \pi$ is applied in the phase response plot for each zero crossing of the magnitude response.</li></ul></i></div>



<br>
<b><u> Cascading FIR filters: </u></b>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>When cascading two different FIR filters, one with frequency response $H_1(e^{j\theta})$ and the other with frequency response $H_2(e^{j\theta})$, we may combine these two FIR filters to one FIR filter of which the frequency response is given by the product of the individual frequency responses: $H(e^{j\theta})= H_1(e^{j\theta}) \cdot H_2(e^{j\theta})$.
</i></div>

<br>
<b><u> Convolution in time- is equivalent to multiplication in frequency-domain: </u></b>
$$
\boxed{
h_1[n] * h_2[n] \hspace{3mm} \circ  \hspace{-2.3mm} - \hspace{-1.1mm}  \circ \hspace{3mm} H_1(e^{j\theta}) \cdot H_2(e^{j\theta})
}
$$

<br>
<b><u> Steady state and transient behaviour: </u></b>
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i><ul><li><b> Transient region:</b> The complex multiplier $\left ( \sum_{k=0}^{{\color{red}{n}}} h[k] e^{-j\theta_1 k} \right )$ depends on the index $n$.</li><li><b>Steady state region:</b> The complex multiplier $\sum\_{k=0}^{{\color{blue}{M-1}}} h[k] e^{-j\theta_1 k}$ is constant. Output contains only input frequency ($\theta_1$ in this example).</li><li>If for $n > M-1$ the input changes to zero or to another frequency $\theta\_2 \neq \theta\_1$, then there will be a new transition- and steady state- region.</li></ul></i></div>
