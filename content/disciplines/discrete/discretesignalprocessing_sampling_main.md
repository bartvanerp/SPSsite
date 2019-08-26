+++
title = "Sampling and reconstruction"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Sampling and reconstruction"
  weight = 20

+++

## Module overview
This module will cover one of the most fundamental aspects in signal processing, namely the principle behind converting a continuous-time signal into a discrete-time signal in order to process it with the help of computers.

1. <a href="../discretesignalprocessing_sampling_samplingprocess">Sampling process of C-to-D converter</a> - First the concept of sampling is discussed, which represents the conversion from the continuous-time to discrete-time domain.
2. <a href="../discretesignalprocessing_sampling_frequency">Absolute and relative frequency</a> - The frequency of the sampled signal is better to be described by a relative frequency, because of the effect of the sampling process.
3. <a href="../discretesignalprocessing_sampling_uniqueness">Uniqueness issue</a> - Through the sampling there can also be a loss of spectral information, known as aliasing. This is caused by the uniqueness issue.
4. <a href="../discretesignalprocessing_sampling_reconstruction">Reconstruction of D-to-C converter</a> - Similarly to the sampling, the signal can also be converted back from the discrete-time domain to the continuous-time domain.
5. <a href="../discretesignalprocessing_sampling_samplingtheorem">Sampling theorem</a> - In order to prevent aliasing the sampling theorem has to be satisfied.

## Examples
<iframe width="100%" height="450" src="https://www.youtube.com/embed/er2dUoPBKL4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## Exercises
In this section several exercises are available, including their answers. The exercises marked in <span style="color:blue">*blue*</span> are explained by means of more extensive pencast videos.


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
    <td>$\frac{f_s}{2} < f \leq \frac{f_s}{2}$</td>
  </tr>
  <tr>
    <td>Absolute radial frequency</td>
    <td>$\omega$</td>
    <td>$-\pi f_s < f \leq \pi f_s$</td>
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
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i><b> Sampling theorem:</b> A continuous-time signal $x(t)$ with frequencies no higher than $f_{max}$ can be reconstructed exactly from its samples $x[n]= x(t)\mid\_{t=n \cdot T_s}$, if samples are taken at a rate $f\_s=1/T\_s$, that is greater than $2 f\_{max}$.</i></div>
