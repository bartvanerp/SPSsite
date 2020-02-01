+++
title = "5ESE0 - Signal processing basics"

# date = {{ .Date }}
lastmod = 2020-01-24

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Responsible teacher (email)
responsibleteacher = "R.Vullings@tue.nl"

# Add menu entry to sidebar.
[menu.5ese0]
name = "5ESE0 - Signal processing basics"
weight = 10

+++

## News
<i> No news is available </i>

## Learning goals

This course will teach the most fundamental principles in signal processing. The main topics covered include:

1. Basic properties of a sinusoidal signal, The relation between time- and phase-shift of a sinusoidal signal, The concept of complex exponentials and phasors, The Polar and Cartesian representation of a phasor, The phasor addition and multiplication rules, The rotating phasor interpretation, Both the Euler and Inverse Euler formulas, The interpretation of complex exponential signals.

2. The spectrum of a sum of sinusoids and its graphical interpretation, The result of multiplication and addition of sinusoidal signals and its relation with the concepts of beat notes and amplitude modulation, The concept of periodic and non-periodic waveforms, Derive the Fourier series expansion equations, both analysis and synthesis, The orthogonality property, The spectrum of the Fourier series, The Fourier analysis of a periodic signal, The concept of time-frequency spectrum, The concept of frequency modulation.

3. The concept of sampling a continuous-time sinusoidal signal, The concept of discrete-time sinusoidal signal, The concept of normalized discrete-time frequency, The spectrum of a discrete-time signal, The sampling theorem, The ideal reconstruction of an analog signal from its discrete-time samples, The spectrum view interpretation of sampling and reconstruction, The concept and results of over-sampling, The concept and results of under-sampling, such as aliasing and folding of spectra, The concept of Discrete-to-Continuous conversion: Interpolation with Pulses, Zero order hold and Linear interpolation, The concept of ideal band-limited interpolation.

4. The concept of a discrete-time system, The general Finite Impulse Response (FIR) filter, The concept of Impulse response of a filter, The concept of unit impulse or delta function, The concept of convolution, How to implement an FIR filter with basic building blocks like unit delays, multipliers and adders, The concept of Linear Time-Invariant (LTI) system, How to compute the convolution result of an LTI system, Basic properties of an LTI system, The result of cascading LTI systems.

5. The concept of frequency response of an FIR system, The concept of super position and the frequency response, The steady state and transition response, The relation of frequency response to impulse response and difference equation, Basic properties of the frequency response, The graphical representation of the frequency response, The result in the frequency domain of cascading LTI systems, The result of filtering sampled continuous-time signals in the discrete-time domain.

<br></br>

## Study material
The study material of this course has been split into several <i>modules</i>.
Each of these modules covers a specific topic corresponding to the learning goals of the course.
The available material consists out of:
<ul>
  <li> <b>Reading material</b> - This includes all study material for the course and is available under the below specified modules on this platform. </li>
  <li> <b>Lecture recordings</b> - Recordings of lectures of previous years are made available for TU/e students to study the subject matter. </li>
  <li> <b>Screencast videos</b> - Besides the extensive reading material, short informative videos are provided to explain the subject material. </li>
  <li> <b>MATLAB animations</b> - Visual animations that visualize difficult concepts.</li>
  <li> <b>Video quizzes</b> - Short quizzes to test whether you have fully understood the subject matter as explained in the screencast videos. </li>
  <li> <b>Exercises</b> - Homework exercises to help you fully understand the subject matter. Some exercises are mandatory for the tutorial sessions. </li>
  <li> <b>Pencast videos</b> - Of some homework exercises, pencast videos are available that walk through the entire exercise. </li>
  <li> <b>MATLAB labs</b> - Mandatory labs are available to apply the learned material using MATLAB. </li>
  <li> <b>MATLAB demos</b> - To get you kickstarted with MATLAB, some basic videos are provided to get you acquainted with the software. </li>
  <li> <b>Summaries</b> - To help you save time for your final exam, even summaries of the most important equations and rules are provided. </li>
</ul>

For the final examination only knowledge of the reading material and a good understanding of the homework exercises is required. However, all the other material will complement the learning process significantly.

The (sub)modules on this website that are covered in this course are:
<!--
<ol>
  <li>  <a href="../../disciplines/mathematicalbackground/mathematicalbackground_complex_main">Complex numbers and phasors</a> </li>
  <ul>
    <li>  <a href="../../disciplines/mathematicalbackground/mathematicalbackground_complex_numbersets">Number sets</a> </li>
    <li>  <a href="../../disciplines/mathematicalbackground/mathematicalbackground_complex_euler">Euler equations</a> </li>
    <li>  <a href="../../disciplines/mathematicalbackground/mathematicalbackground_complex_notation">Complex numbers</a> </li>
    <li>  <a href="../../disciplines/mathematicalbackground/mathematicalbackground_complex_phasors">Phasors</a>  </li>
  </ul>
  <li>  Spectrum and Fourier series</li>
  <ul>
    <li>  <a href="../../disciplines/continuous/continuoussignalprocessing_transforms_spectrum">Spectrum of sinusoidal signals</a> </li>
    <li>  <a href="../../disciplines/continuous/continuoussignalprocessing_transforms_Fourier">Fourier series</a> </li>
  </ul>
  <li>  <a href="../../disciplines/discrete/discretesignalprocessing_sampling_main">Sampling and reconstruction</a> </li>
  <ul>
    <li>  <a href="../../disciplines/discrete/discretesignalprocessing_sampling_sampling">Sampling of sinusoidal signals</a> </li>
    <li>  <a href="../../disciplines/discrete/discretesignalprocessing_sampling_reconstruction">Reconstruction of sinusoidal signals</a> </li>
  </ul>
  <li>  Discrete-time signals</li>
  <ul>
    <li>  <a href="../../disciplines/discrete/discretesignalprocessing_signals_basics">Elementary signals</a> </li>
  </ul>
  <li>  Discrete-time systems </li>
  <ul>
    <li>  <a href="../../disciplines/discrete/discretesignalprocessing_systems_fir">Finite impulse response filters</a> </li>
  </ul>
  <li>  Transform analysis of discrete-time systems </li>
  <ul>
    <li>  <a href="../../disciplines/discrete/discretesignalprocessing_analysis_frequency">Frequency response of finite impulse response filters</a> </li>
  </ul>
</ol>
-->
<ol>
  <li><a href="../mathematicalbackground_complex_main">Complex numbers and phasors</a> <i>(incl. all submodules)</i></li>
  <li>  <a href="../continuoussignalprocessing_transforms_spectrum">Spectrum of sinusoidal signals</a> </li>
  <li>  <a href="../continuoussignalprocessing_transforms_fourier">Fourier series</a> </li>
  <li>  <a href="../discretesignalprocessing_sampling_main">Sampling and reconstruction</a> <i>(incl. all submodules)</i></li>
  <li>  <a href="../discretesignalprocessing_signals_basics">Elementary signals</a> </li>
  <li>  <a href="../discretesignalprocessing_systems_fir">Finite impulse response filters</a> </li>
  <li>  <a href="../discretesignalprocessing_analysis_frequency">Frequency response of finite impulse response filters</a> </li>
</ol>

<!--
{{% alert note %}}
In the case that a module contains several submodules (such as the module <a href="../mathematicalbackground_complex_main">Complex numbers and phasors</a>) <b>all</b> submodules are covered during the course. When only a submodule is listed (such as the submodules <a href="../continuoussignalprocessing_transforms_spectrum">Spectrum of sinusoidal signals</a> and <a href="../continuoussignalprocessing_transforms_fourier">Fourier series</a>) <b>only the specified submodules</b> are covered during the course (so not the submodule <a href="../continuoussignalprocessing_transforms_ftc">Fourier transform for continuous-time signals</a>).
{{% /alert %}}
-->

### Additional reading material
The material covered in this course is based on the first six chapters of the book:

<i>"Signal Processing First" by James H. McClellan et. al. </i>


<br></br>

## Planning
<i>No planning is available</i>

<br></br>

## Lecture recordings

The below table provides the links to the lecture recordings of the course. The lectures were recorded in the academic year 2016/2017 and are available for students of the TU/e through the following links.

<table class="th" style="height: 345px;" border="s" width="654"><caption>&nbsp;</caption>
  <tbody>
    <tr>
    </tr>
    <tr>
      <td style="width: 86px;"><em><strong>Date</strong></em></td>
      <td style="width: 80px;"><em><strong>Lecture</strong></em></td>
      <td style="width: 460px;"><strong><em>Covered Content</em></strong></td>
    </tr>
    <tr>
    </tr>
    <tr>
      <td style="width: 86px;">14-11-2016</td>
      <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/c5c338870f814bdcbb4b66232a49cbad1d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 1a</a></td>
      <td style="width: 460px;">General course information,&nbsp;Introduction</td>
    </tr>
    <tr>
      <td style="width: 86px;"></td>
      <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/f0e1a9ce091e4a899134bf74b603911f1d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 1b</a></td>
      <td style="width: 460px;">Cody Coursework, Signals, Sinusoids</td>
    </tr>
    <tr>
      <td style="width: 86px;">17-11-2016</td>
      <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/6336c1ec672d49d3af8fa0649b46f04f1d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 2a</a></td>
      <td style="width: 460px;">Set theory, j, Complex exponentials, Polar/Cartesian notation</td>
    </tr>
    <tr>
      <td style="width: 86px;"></td>
      <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/dd10e4802ced4e7684b744edbd24a3931d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 2b</a></td>
      <td style="width: 460px;">Polar/Cartesian notation, Calculations</td>
    </tr>
    <tr>
      <td style="width: 86px;">21-11-2016</td>
      <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/23b301ba53da4532a360f5c3b51aea6e1d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture&nbsp;3a</a></td>
      <td style="width: 460px;">Complex calculations, Phasors</td>
    </tr>
    <tr>
      <td style="width: 86px;"></td>
      <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/f1da83d1967847868490eba840fe8d301d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 3b</a></td>
      <td style="width: 460px;">Phasor addition</td>
    </tr>
    <tr>
    </tr>
    <tr>
      <td style="width: 86px;"><em><strong>Date</strong></em></td>
      <td style="width: 80px;"><em><strong>Lecture</strong></em></td>
      <td style="width: 460px;"><strong><em>Covered Content</em></strong></td>
    </tr>
    <tr>
    </tr>
    <tr>
      <td style="width: 86px;">24-11-2016</td>
      <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/d99c37d385094db58cdf0c7542ba18931d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture&nbsp;4a</a></td>
      <td style="width: 460px;">Animations of phasors, spectrum</td>
    </tr>
    <tr>
      <td style="width: 86px;"></td>
      <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/8707c4ac802648d7a6de14cc7b4b1a311d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 4b</a></td>
      <td style="width: 460px;">Spectrum (continued), examples</td>
    </tr>
    <tr>
      <td style="width: 86px;">28-11-2016</td>
      <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/8de324408cc1422a9ef5ceca76d689b71d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 5a</a></td>
      <td style="width: 460px;">Spectrum (continued), Fourier Series</td>
    </tr>
    <tr>
      <td style="width: 86px;"></td>
      <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/3b366440cead4e28bfa255844cf508de1d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 5b</a></td>
      <td style="width: 460px;">Fourier Series (continued), examples</td>
    </tr>
    <tr>
      <td style="width: 86px;">01-12-2016</td>
      <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/8cc6f3f16da646ea9745449f399f79831d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 6a</a></td>
      <td style="width: 460px;">Fourier Series (continued), examples (square wave)</td>
    </tr>
    <tr>
      <td style="width: 86px;"></td>
      <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/57a7b51b3f9f45d7a3fa09f15c2f4d121d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 6b</a></td>
      <td style="width: 460px;">Fourier Series (continued)</td>
    </tr>
    <tr>
      <tr>
      </tr>
      <td style="width: 86px;"><em><strong>Date</strong></em></td>
      <td style="width: 80px;"><em><strong>Lecture</strong></em></td>
      <td style="width: 460px;"><strong><em>Covered Content</em></strong></td>
      <tr>
      </tr>
      <tr>
        <td style="width: 86px;">5-12-2016</td>
        <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/eeab37b1339c46db963c837977b655db1d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 7a</a></td>
        <td style="width: 460px;">Sampling, relative frequency, aliasing</td>
      </tr>
      <tr>
        <td style="width: 86px;"></td>
        <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/5d9bf1a3fa284c43a1b7828616ceb2801d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 7b</a></td>
        <td style="width: 460px;">Reconstruction</td>
      </tr>
      <tr>
        <td style="width: 86px;">8-11-2016</td>
        <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/32f8914a86ec46c19e23bea85f94798a1d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 8a</a></td>
        <td style="width: 460px;">Converters, Examples</td>
      </tr>
      <tr>
        <td style="width: 86px;"></td>
        <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/8b0f67198d8f4ec2810dd551a05fc2321d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 8b</a></td>
        <td style="width: 460px;">Examples</td>
      </tr>
      <tr>
      </tr>
      <td style="width: 86px;"><em><strong>Date</strong></em></td>
      <td style="width: 80px;"><em><strong>Lecture</strong></em></td>
      <td style="width: 460px;"><strong><em>Covered Content</em></strong></td>
      <tr>
      </tr>
      <tr>
        <td style="width: 86px;">12-12-2016</td>
        <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/05126cd4cc72462a8e14c9a53c84538b1d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 9a</a></td>
        <td style="width: 460px;">Difference equation, building blocks, convolution sum</td>
      </tr>
      <tr>
        <td style="width: 86px;"></td>
        <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/3070aaa23b3f431bb0d5f06e606bdced1d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 9b</a></td>
        <td style="width: 460px;">Impulse response, LTI systems</td>
      </tr>
      <tr>
        <td style="width: 86px;">15-12-2016</td>
        <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/bf4aa65929ea4a1aae59b051af56d6471d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 10a</a></td>
        <td style="width: 460px;">FIR convolution, cascaded systems</td>
      </tr>
      <tr>
        <td style="width: 86px;"></td>
        <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/0bf0c0e28b904b68b6bdea510b55091c1d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 10b</a></td>
        <td style="width: 460px;">Examples</td>
      </tr>
      <tr>
      </tr>
      <td style="width: 86px;"><em><strong>Date</strong></em></td>
      <td style="width: 80px;"><em><strong>Lecture</strong></em></td>
      <td style="width: 460px;"><strong><em>Covered Content</em></strong></td>
      <tr>
      </tr>
      <tr>
        <td style="width: 86px;">19-12-2016</td>
        <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/becfd8e5999a4385b564cf0b6cda7fd51d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 11a</a></td>
        <td style="width: 460px;">Frequency response: introduction by an example, properties</td>
      </tr>
      <tr>
        <td style="width: 86px;"></td>
        <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/7fee9f9aad8e4204b327b2c12ccf30f61d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 11b</a></td>
        <td style="width: 460px;">Properties, example</td>
      </tr>
      <tr>
        <td style="width: 86px;">22-12-2016</td>
        <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/41ef46e9e48547f3bdd9194755feb59b1d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 12a</a></td>
        <td style="width: 460px;">Cascading, example</td>
      </tr>
      <tr>
        <td style="width: 86px;"></td>
        <td style="width: 80px;"><a href="https://videocollege.tue.nl/Mediasite/Play/922ba8c47a32417db79201a54b2254d61d?catalog=c2530f3a-2738-42c4-80d4-0365fcbf2163">Lecture 12b</a></td>
        <td style="width: 460px;">Running averaging filter</td>
      </tr>
    </tbody>
  </table>

  <br></br>

## Mandatory tutorial exercises
  The following table specifies the exercises that are mandatory for the instruction hours.

  <table class="th" border="s" width="654">
    <tbody>
      <tr>
      </tr>
      <tr>
        <td><em><strong>Module</strong></em></td>
        <td><em><strong>Topic</strong></em></td>
        <td><em><strong>Mandatory exercises</strong></em></td>
      </tr>
      <tr>
      </tr>
      <tr>
        <td><a href="../mathematicalbackground_complex_main/#exercises">Complex numbers and phasors</a></td>
        <td>Sinusoidal signals</td>
        <td>Ex. 1 </td>
      </tr>
      <tr>
        <td></td>
        <td>Cartesian and polar notation</td>
        <td>Ex. 3b, 4a </td>
      </tr>
      <tr>
        <td></td>
        <td>Calculation rules for complex numbers</td>
        <td>Ex. 5b, 6b, 8a </td>
      </tr>
      <tr>
        <td></td>
        <td>Calculation rules for phasors</td>
        <td>Ex. 10 </td>
      </tr>
      <tr>
      </tr>
      <tr>
        <td>Spectrum and Fourier series</td>
        <td><a href="../continuoussignalprocessing_transforms_spectrum/#exercises">Spectrum</a></td>
        <td>Ex. 1, 2, 3, 5 </td>
      </tr>
      <tr>
        <td></td>
        <td><a href="../continuoussignalprocessing_transforms_fourier/#exercises">Fourier Series</a></td>
        <td>Ex. 4, 5, 7, 9 </td>
      </tr>
      <tr>
      </tr>
      <tr>
        <td><a href="../discretesignalprocessing_sampling_main/#exercises">Sampling and reconstruction</a></td>
        <td>C/D conversion</td>
        <td>Ex. 3 </td>
      </tr>
      <tr>
        <td></td>
        <td>D/C conversion</td>
        <td>Ex. 8 </td>
      </tr>
      <tr>
        <td></td>
        <td>C/D - D/C conversion (same rates)</td>
        <td>Ex. 11a, 11b, 11c </td>
      </tr>
      <tr>
        <td></td>
        <td>C/D - D/C conversion (different rates)</td>
        <td>Ex. 13 </td>
      </tr>
      <tr>
      </tr>
      <tr>
        <td><a href="../discretesignalprocessing_systems_fir/#exercises">FIR filters</a></td>
        <td>Linearity, LTI and causality</td>
        <td>Ex. 8c, 8d, 8e </td>
      </tr>
      <tr>
        <td></td>
        <td>From DE to filter coefficients</td>
        <td>Ex. 9 </td>
      </tr>
      <tr>
        <td></td>
        <td>Calculate output using LTI property</td>
        <td>Ex. 12 </td>
      </tr>
      <tr>
        <td></td>
        <td>Cascading filters</td>
        <td>Ex. 13 </td>
      </tr>
      <tr>
      </tr>
      <tr>
        <td><a href="../discretesignalprocessing_analysis_frequency/#exercises">Frequency response</a></td>
        <td>Calculating filter output</td>
        <td>Ex. 2 </td>
      </tr>
      <tr>
        <td></td>
        <td>From DE to frequency response</td>
        <td>Ex. 4 </td>
      </tr>
      <tr>
        <td></td>
        <td>Cascading filters</td>
        <td>Ex. 8 </td>
      </tr>
      <tr>
        <td></td>
        <td>Designing filters</td>
        <td>Ex. 12 </td>
      </tr>
    </tbody>
  </table>

<br></br>

## Contact
In case any of the above material is unclear, please contact the responsible teacher of this course. If there are any problems with the platform or with the material on the platform, please put the mail address sps.education@tue.nl in the CC of your email, or simply click <a href="mailto:{{< param responsibleteacher >}}?cc=sps.education@tue.nl&subject=[5ESE0]%20platform:%20{specify problem here}">here</a>. This will help us keep the platform up-to-date.
