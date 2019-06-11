+++
title = "Complex numbers and phasors"
# date = {{ .Date }}
lastmod = 2019-06-05

draft = false       # Is this a draft? true/false
toc = true          # Show table of contents? true/false
type = "docs"       # Do not modify.

# Add menu entry to sidebar.
[menu.mathematicalbackground]
  name = "Complex numbers and phasors"
  weight = 0

+++

## Module overview
In addition to the set of real numbers that everyone is used to working with, a whole new dimension is introduced by complex numbers. These complex numbers can be used to describe sinusoidal signals through phasors, which has proven to be useful in many applications.
This module concerns the following topics:

1. <a href="../mathematicalbackground_complex_numbersets">Number sets</a> - This section covers the inevitable need for complex numbers for engineering practices.
2. <a href="../mathematicalbackground_complex_euler">Euler equations</a> - Through the use of Taylor expansions, we are allowed to rewrite sinusoids in terms of complex exponentials.
3. <a href="../mathematicalbackground_complex_notation">Complex numbers</a> - This section elaborates more on the notation of complex numbers and introduces mathematical operations on these complex numbers.
4. <a href="../mathematicalbackground_complex_phasors">Phasors</a> - This section introduces sinusoidal signals in terms of time varying complex exponentials.

### Introductory video
<div>
<video controls preload>
  <source src="/../files/8.Screencast/1aComplexConcept.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>
</div>



\
## Exercises
In this section several exercises are available, including their answers. The exercises marked in <span style="color:blue">*blue*</span> are explained by means of more extensive pencast videos.


### Exercise bundle

<object data="/../files/3.Exercises/1.CNAP-StudentExercises.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/3.Exercises/1.CNAP-StudentExercises.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/3.Exercises/1.CNAP-StudentExercises.pdf">Download PDF</a>.</p>
    </embed>
</object>

### Answers
Download the answers <a href="/../files/3.Exercises/Answers/1.CNAP-StudentAnswers.pdf">here</a>.

### Pencast videos
<script src='https://vjs.zencdn.net/7.4.1/video.js'></script>
<div class="grid-row reverse video-gallery">
 <input type="radio" value="1" name="video-list" id="video-1" checked="checked" /><label for="video-1">Exercise 2a</label>
 <input type="radio" value="2" name="video-list" id="video-2" /><label for="video-2">Exercise 5c</label>
 <input type="radio" value="3" name="video-list" id="video-3" /><label for="video-3">Exercise 6c</label>
 <input type="radio" value="4" name="video-list" id="video-4" /><label for="video-4">Exercise 8b</label>
 <input type="radio" value="5" name="video-list" id="video-5" /><label for="video-5">Exercise 11</label>


 <!-- videos -->
 <div class="video video-1">
 <video width="500" height="240" controls>
   <source src="/../files/6.Pencast/CNAP-2a.mp4" type="video/mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

 <div class="video video-2">
 <video width="500" height="240" controls>
   <source src="/../files/6.Pencast/CNAP-5c.mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

 <div class="video video-3">
 <video width="500" height="240" controls>
   <source src="/../files/6.Pencast/CNAP-6c.mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

 <div class="video video-4">
 <video width="500" height="240" controls>
   <source src="/../files/6.Pencast/CNAP-8b.mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

 <div class="video video-5">
 <video width="500" height="240" controls>
   <source src="/../files/6.Pencast/CNAP-11.mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

</div>

## Summary

<ul>
<li> The imaginary unit: $\boxed{\mbox{j} = \sqrt{-1}}$</li>
<li> Euler equation: $\boxed{\mbox{e}^{j\theta} = \cos({\theta}) + \mbox{j}\cdot \sin({\theta})}$</li>
<li> Alternative expression for $\sin(\cdot)$ and $\cos(\cdot)$ function:
$$ \boxed{\cos(\theta)= \frac{e^{j\theta}+e^{-j\theta}}{2} = \Re e \{ e^{j\theta} \} } \qquad \text{and} \qquad \boxed{\sin(\theta)=\frac{e^{j\theta}-e^{-j\theta}}{2j} = \Im m \{ e^{j\theta} \} } $$</li>
<li> Polar representation set of complex numbers:
$\boxed{\mathbb{C} = \{ z= r e^{j\theta} \ |\ r \in \mathbb{R} \mbox{ and } \theta \in \mathbb{R} \} }$</li>
<li> Cartesian representation set of complex numbers:
$\boxed{\mathbb{C} = \{ z=x+ j\cdot y\ |\ x \in \mathbb{R} \mbox{ and } y \in \mathbb{R} \}}
$</li>
<li> Conversion Cartesion to Polar representation:
$$
\boxed{r= \sqrt{x^2 + y^2} \mbox{ and }
\theta=
\left \{
\begin{array}{ll}
\arctan (\frac{y}{x}) & \mbox{for } x > 0 \\
\arctan (\frac{y}{x}) + \pi & \mbox{for } x < 0; y \geq 0 \\
\arctan (\frac{y}{x}) - \pi & \mbox{for } x < 0; y < 0 \\
\frac{\pi}{2} & \mbox{for } x=0; y > 0 \\
-\frac{\pi}{2} & \mbox{for } x=0; y < 0 \\
\mbox{undetermined} & \mbox{for } x=y=0
\end{array}
\right .
}
$$</li>
<li> Conversion Polar to Cartesion representation:
$$
\boxed{ x= r \cos(\theta)} \mbox{ and } \boxed{y = r \sin(\theta)}
$$</li>
<li> Complex conjugation: Replace $j$ by $-j$ (and vice versa!)</li>
<li> Length of complex vector:
$\boxed{|z| = \sqrt{z \cdot z^* }} \qquad \text{real and } \geq 0 $</li>
<li><i>It is the easiest to use Cartesian notation for addition and subtraction, and polar notation for multiplication and division.</i></li>
<li> Phasor representation of sinusoidal signals:
$$ \begin{eqnarray}
A \cos (\omega_o t +\phi) &=& \Re e \{ A e^{j(\omega_o t +\phi)} \} = \frac{A e^{j(\omega_o t +\phi)} + A e^{-j(\omega_o t +\phi)}}{2}   \newline
A \sin (\omega_o t +\phi) &=& \Im m \{ A e^{j(\omega_o t +\phi)} \} = \frac{A e^{j(\omega_o t +\phi)} - A e^{-j(\omega_o t +\phi)}}{2 j}
\end{eqnarray}$$</li>
<li> The sum of original sinusoidal signals, all with the same radian frequency $\omega_0$, results in one sinusoidal signal with the same radian frequency $\omega_0$. Amplitude and phase of this resulting signal can be found by adding the complex representation of amplitude and phase of the individual original sinusoidal signals.
$$
\boxed{
x(t) = \sum_{k=1}^{N} A_k \cos (\omega_0 t + \phi_k)= A \cos (\omega_0 t + \phi)}
\mbox{ with }
\boxed{A e^{j\phi} = \sum_{k=1}^N A_k e^{j\phi_k}}
$$</li>
</ul>
