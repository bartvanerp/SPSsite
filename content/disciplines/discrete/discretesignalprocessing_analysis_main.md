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
2. **Frequency response of LTI systems** (to be added)
3. **Solving difference equations with the Z-transform** (to be added)
4. **System functions with poles and zeros** (to be added)

## Exercises
In this section several exercises are available, including their answers. The exercises marked in <span style="color:blue">*blue*</span> are explained by means of more extensive pencast videos.


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
